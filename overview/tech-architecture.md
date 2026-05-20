# Relay 技术架构

## 整体架构

```
┌─────────────────────────────────────────────────────────┐
│                      用户机器                            │
│                                                         │
│  ┌──────────┐     gRPC (localhost)    ┌──────────────┐ │
│  │  Flutter  │ ◄──────────────────► │    Go 后端     │ │
│  │  客户端    │                       │   (relayd)    │ │
│  └──────────┘                        └──────┬───────┘ │
│                                              │          │
│                                stdin/stdout  │          │
│                               ┌──────────────┘          │
│                               ▼                         │
│                        ┌──────────┐                     │
│                        │ AI 推理   │                     │
│                        │ (Python)  │                     │
│                        └──────────┘                     │
└─────────────────────────────────────────────────────────┘
```

三个进程运行在同一台机器上：
- **Flutter 客户端**：UI 层（系统托盘、交付窗口、收件箱、设置）
- **Go 后端（relayd）**：业务逻辑、数据持久化、通道投递、文件监听
- **Python AI**：onnxruntime 本地推理，stdin/stdout 与 Go 父进程通信，即用即走

---

## 技术选型总结

| # | 决策项 | 选择 | 说明 |
|---|--------|------|------|
| 1 | 客户端技术栈 | Flutter | 包体积、性能、移动端扩展潜力 |
| 2 | 后端语言 | Go（Golang） | 单一二进制分发、并发优势、gRPC 原生支持 |
| 3 | 通信协议 | gRPC | proto 定义服务接口，客户端与后端均通过 gRPC 通信 |
| 4 | 本地存储 | SQLite | 统一数据存储，用 sqlc 生成类型安全查询代码 |
| 5 | AI 方案 | 混合方案 | 分类/元数据提取用本地 onnxruntime，摘要/待办用云 LLM |
| 6 | AI 运行时 | Python + PyInstaller | 核心推理用 Python 写，PyInstaller 打包为独立二进制 |
| 7 | 配置管理 | 应用配置存 SQLite，运行时配置用 .env | 运行时不涉及业务敏感数据 |
| 8 | 状态管理 | Riverpod | Flutter 端编译安全、社区活跃 |
| 9 | 日志 | slog（Go）+ logging（Python）+ logging（Flutter） | 统一输出到 `~/.relay/logs/`，按天滚动 |
| 10 | gRPC 安全 | 裸 gRPC | localhost 通信，OS 层面已隔离 |
| 11 | Proto 策略 | 跟随 feat 动态演进 | 不提前设计，按版本逐步定义 |
| 12 | 打包 | PyInstaller + flutter_distributor | Go 编译为 relayd 单二进制，Python 打包为 relay-ai 单二进制，Flutter 编译为本地应用 |

---

## 项目目录结构

```
relay/
├── client/                     # Flutter 桌面端
│   ├── lib/
│   │   ├── main.dart
│   │   ├── app.dart            # MaterialApp + 全局 ProviderScope
│   │   ├── core/               # 跨域共享
│   │   │   ├── grpc/           #   gRPC client 管理
│   │   │   ├── theme/          #   主题
│   │   │   └── util/           #   工具
│   │   ├── target/             #   交付对象
│   │   │   ├── data/           #     gRPC 调用
│   │   │   ├── domain/         #     model
│   │   │   └── ui/             #     页面/组件
│   │   ├── delivery/           #   交付
│   │   │   ├── data/
│   │   │   ├── domain/
│   │   │   └── ui/
│   │   ├── tray/               #   系统托盘
│   │   └── settings/           #   设置
│   └── pubspec.yaml
│
├── backend/                    # Golang 本地后端
│   ├── cmd/
│   │   └── relayd/             #   主入口，启动 gRPC server + 各模块
│   ├── internal/
│   │   ├── bootstrap/          #   组装启动（DI 组装、composite handler）
│   │   ├── config/             #   配置加载（.env + 环境变量）
│   │   ├── module/             #   业务模块（按版本逐步添加）
│   │   │   ├── target/         #     交付对象管理
│   │   │   ├── delivery/       #     交付执行
│   │   │   ├── rule/           #     规则模板
│   │   │   ├── channel/        #     通道管理
│   │   │   ├── inbox/          #     收件箱（v0.1.0）
│   │   │   ├── watcher/        #     文件监听（v0.0.2）
│   │   │   └── ai/             #     AI 调度（v0.0.3）
│   │   └── platform/           #   基础设施
│   │       ├── sqlite/         #     SQLite 连接管理 + sqlc queries
│   │       ├── smtp/           #     SMTP 邮件发送
│   │       ├── imap/           #     IMAP 邮件监听
│   │       └── python/         #     Python 进程管理（spawn/stdin-stdout）
│   └── go.mod
│
├── proto/                      # protobuf 定义（client/backend 共享）
│   └── relay/
│       └── v1/
│           └── ...             #   按 feat 动态添加
│
├── ai/                         # Python 推理脚本
│   ├── classifier.py           #   文件类型分类
│   ├── extractor.py            #   元数据提取
│   └── requirements.txt
│
└── overview/                   # 产品文档
    ├── README.md
    ├── product-design.md
    ├── tech-architecture.md    # 本文件
    └── version/
```

---

## 模块分层规范

Go 后端每个模块遵循三层架构，参照 bridge 项目结构：

```
module/<name>/
├── domain/           # 领域层：struct + interface，仅依赖 stdlib
│   ├── <entity>.go   #   实体 struct
│   ├── store.go      #   Store 接口（持久化 port）
│   ├── ports.go      #   其他基础设施 port
│   └── errors.go     #   哨兵错误
├── app/              # 应用层：用例编排，仅依赖 domain + stdlib
│   └── service.go    #   Service struct，用例方法
├── adapter/          # 适配器层：实现 domain port，做翻译
│   ├── grpc/         #   gRPC handler：proto ↔ domain 翻译
│   │   └── handler.go
│   └── sqlite/       #   SQLite store（按需，部分模块可能无持久化）
│       └── store.go
└── module.go         # DI 组装入口
```

### 依赖方向

```
platform/  ──►  adapter/  ──►  app/  ──►  domain/
```

- **domain/** 不导入任何项目内部包
- **app/** 仅导入 domain/ + stdlib，禁止导入 platform/、adapter/、pb/
- **adapter/** 导入 domain/（实现 port）+ platform/（使用基础设施）+ pb/（gRPC handler）
- **module.go** 导入所有层，仅做 DI 组装

### 错误翻译规则

- **sqlite adapter**：`sql.ErrNoRows` → `domain.ErrNotFound`
- **gRPC adapter**：domain 错误 → gRPC status codes（`ErrValidation` → `InvalidArgument`，`ErrNotFound` → `NotFound`，其他 → `Internal`）

---

## MVP 模块清单（v0.0.1）

| 模块 | 对应 Feature | 职责 |
|------|-------------|------|
| target | F-002 | 交付对象增删改查 |
| rule | F-004 | 规则模板匹配 |
| delivery | F-001, F-003, F-006 | 交付执行 + 记录 |
| channel | F-005 | 通道管理（首期仅 SMTP） |

后续模块按版本添加：watcher（v0.0.2）、ai（v0.0.3）、inbox（v0.1.0）。

---

## 进程通信与生命周期

```
[Flutter 启动]
      │
      ├── spawn Go binary (relayd)
      │     ├── Go 监听 localhost:0（随机端口）
      │     ├── stdout 打印端口号
      │     └── 启动 gRPC server
      │
      ├── 读取 stdout 端口号
      ├── 建立 gRPC 连接
      ├── 健康检查（定期）
      │
      ├── [用户操作] → gRPC 请求 → Go 后端处理
      │
      ├── Go 按需调用 Python AI script
      │     └── stdin 传文本 → stdout 拿结果，即用即走
      │
[Flutter 退出]
      │
      ├── 发送 Shutdown gRPC
      ├── Go 优雅退出
      └── 进程结束
```

- **端口分配**：Go 监听 `localhost:0`（OS 随机分配），stdout 输出端口号，Flutter 解析后连接
- **崩溃恢复**：Flutter 检测到 Go 进程退出后自动重启，托盘图标变红提示
- **日志**：Go（slog JSON handler）、Python（logging → stderr）、Flutter（logging package 写文件），统一输出到 `~/.relay/logs/`，按天滚动

---

## 数据存储

所有数据统一使用 SQLite，sqlc 管理 schema 和查询：

```sql
-- 核心表（v0.0.1）
CREATE TABLE targets (       -- 交付对象
    id TEXT PRIMARY KEY,
    name TEXT NOT NULL,
    target_type TEXT NOT NULL,   -- 'person' | 'system'
    email TEXT,
    relation_type TEXT,          -- 'supervisor' | 'peer' | 'subordinate' | ...
    channel_address TEXT,
    created_at TEXT NOT NULL,
    updated_at TEXT NOT NULL
);

CREATE TABLE rules (          -- 规则模板
    id TEXT PRIMARY KEY,
    pattern TEXT NOT NULL,        -- 文件名匹配模式
    delivery_type TEXT NOT NULL,
    role TEXT NOT NULL,
    created_at TEXT NOT NULL
);

CREATE TABLE deliveries (     -- 交付记录
    id TEXT PRIMARY KEY,
    target_id TEXT NOT NULL,
    delivery_type TEXT NOT NULL,
    subject TEXT NOT NULL,
    content_path TEXT,
    status TEXT NOT NULL,         -- 'pending' | 'sent' | 'failed'
    created_at TEXT NOT NULL,
);

CREATE TABLE channel_configs ( -- 通道配置
    id TEXT PRIMARY KEY,
    channel_type TEXT NOT NULL,   -- 'smtp' | 'im' | 'webhook' | 'agent'
    config_json TEXT NOT NULL,    -- JSON 配置
    enabled INTEGER NOT NULL DEFAULT 1,
    created_at TEXT NOT NULL
);
```

应用用户配置（SMTP 账号、IMAP 账号等）也通过 channel_configs 表存储，不走文件。

---

## AI 推理流程

```
[Go 后端]
      │
      ├── 检测到新文件 / 收件箱有新条目
      │
      ├── 判断任务类型：
      │
      ├── 分类 / 元数据提取 ──► spawn Python relay-ai binary
      │     ├── stdin 传入 {"task": "classify", "text": "..."}
      │     ├── Python 加载 onnxruntime 模型推理
      │     ├── stdout 输出 {"type": "weekly_report", "confidence": 0.92}
      │     └── Python 进程退出
      │
      ├── 摘要 / 待办提取 ──► 调用云 LLM API
      │     └── 仅在网络可用时触发，失败静默降级
      │
      └── 结果写入 SQLite / 返回给 Flutter
```

---

## 打包分发

| 目标平台 | 产物 | 工具 |
|---------|------|------|
| Linux | `.deb` / `.AppImage` | flutter_distributor |
| macOS | `.dmg` | flutter_distributor |
| Windows | `.msi` / `.exe` | flutter_distributor |

每个安装包内包含三个组件：

```
relay/
├── relay                    # Flutter 编译的本地应用
├── relayd                   # Go 编译的单二进制
└── relay-ai                 # Python PyInstaller 打包的独立二进制
```

Python 依赖（onnxruntime + 推理脚本）通过 PyInstaller 打包为 `relay-ai` 单二进制，Go 通过 `os/exec` 调用。

---

## 关键技术约束

- **本地优先**：所有核心功能离线可用，云 LLM 仅用于增强（摘要/待办）
- **隐私**：文件内容不离开本机（分类和元数据提取完全本地推理）
- **零配置启动**：首次运行自动创建 `~/.relay/` 目录结构，无需用户手动配置
- **优雅降级**：Python AI 不可用时交付流程不受阻（仅跳过分类/提取，使用规则模板兜底）
