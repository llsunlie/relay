# Relay 标签时间线

## v0.0.1 — MVP（手动交付通道）

```
F-001 ──→ F-002 ──→ F-003 ──→ F-004
  │                                │
  └──── F-005 ──→ F-006 ──────────┘
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-001 | [系统分享菜单集成](features/F-001-system-share-menu.md) | 文件右键 → Relay |
| F-002 | [关系图谱（手动建立）](features/F-002-relationship-graph.md) | 手动创建联系人 + 标注关系 |
| F-003 | [交付确认弹窗](features/F-003-delivery-confirm-dialog.md) | 类型、收件人、留言、确认 |
| F-004 | [规则模板（5个预置）](features/F-004-rule-templates.md) | 文件名关键词匹配收件人 |
| F-005 | [邮件投递](features/F-005-email-delivery.md) | mailto / SMTP |
| F-006 | [交付记录（本地）](features/F-006-delivery-history.md) | 历史列表 + 重发 |

---

## v0.0.2 — 文件夹监听

```
F-007 ──┬──→ F-008
        │
        ├──→ F-009
        │
        ├──→ F-010
        │
        └──→ F-011
```

| 序号 | Feature | 说明 | 依赖 |
|------|---------|------|------|
| F-007 | [文件夹监听引擎](features/F-007-folder-watcher.md) | inotify/FSEvents 监控 relay-outbox | F-003, F-004 |
| F-008 | [子目录→类型映射](features/F-008-subfolder-mapping.md) | weekly/ → 周报 | F-007 |
| F-009 | [静默交付模式](features/F-009-silent-delivery.md) | 匹配规则不弹窗直接发 | F-007, F-004 |
| F-010 | [交付前规则校验](features/F-010-rule-validation.md) | 格式+收件人校验 | F-007, F-002 |
| F-011 | [托盘状态指示](features/F-011-tray-indicator.md) | 常亮/闪烁/红点 | F-007 |

---

## v0.0.3 — AI 识别

```
F-012 ──┬──→ F-013
        │
        ├──→ F-014
        │
        └──→ F-015
```

| 序号 | Feature | 说明 | 依赖 |
|------|---------|------|------|
| F-012 | [文件内容 AI 分类器](features/F-012-ai-classifier.md) | 本地推理判断产出类型 | F-007 |
| F-013 | [分类结果反馈学习](features/F-013-feedback-learning.md) | 用户修正 → 本地模型微调 | F-012, F-003 |
| F-014 | [元数据自动提取](features/F-014-metadata-extraction.md) | 周期、课程、金额等 | F-012 |
| F-015 | [交付确认弹窗升级](features/F-015-confirm-dialog-v2.md) | AI 类型+元数据+推荐收件人 | F-003, F-012, F-014 |

---

## v0.1.0 — 收件箱（Inbox） ★ 闭环

```
F-016 ──┬──→ F-017 ──→ F-020
        │
        ├──→ F-018
        │
        └──→ F-019 ──→ F-021
```

| 序号 | Feature | 说明 | 依赖 |
|------|---------|------|------|
| F-016 | [本地收件箱界面](features/F-016-inbox-ui.md) | 三区布局 + 搜索筛选 | F-011 |
| F-017 | [每日摘要通知](features/F-017-daily-digest.md) | 定时推送/实时推送 | F-016 |
| F-018 | [AI 预处理](features/F-018-ai-preprocessing.md) | 摘要+待办+异常+上下文 | F-016 |
| F-019 | [收件动作](features/F-019-inbox-actions.md) | 同意/拒绝/批注/退回/转发 | F-016 |
| F-020 | [免打扰模式](features/F-020-dnd-mode.md) | 时段内不推送 | F-017 |
| F-021 | [发送方状态回传](features/F-021-status-feedback.md) | 已送达/已读/已处理/已退回 | F-019, F-006 |

---

## v0.1.1 — 格式转换

```
F-022 ──→ F-023 ──┬──→ F-024
                   │
                   └──→ F-025
```

| 序号 | Feature | 说明 | 依赖 |
|------|---------|------|------|
| F-022 | [接收方格式偏好声明](features/F-022-format-preference.md) | 每种类型声明偏好的格式 | F-016 |
| F-023 | [格式转换管线](features/F-023-conversion-pipeline.md) | IR 管线 md↔html/pdf, csv→png | F-022 |
| F-024 | [转换预览](features/F-024-conversion-preview.md) | 弹窗中预览对方看到的格式 | F-023, F-015 |
| F-025 | [转换质量指标](features/F-025-conversion-quality.md) | 自动检查+低质量告警 | F-023, F-024 |

---

## v0.2.0 — 多通道

```
F-026 ──┬──→ F-027
        ├──→ F-028
        ├──→ F-029
        ├──→ F-030 ──→ F-031
```

| 序号 | Feature | 说明 | 依赖 |
|------|---------|------|------|
| F-026 | [通道抽象层](features/F-026-channel-abstraction.md) | 统一 DeliveryChannel 接口 | F-005 |
| F-027 | [邮件通道升级](features/F-027-smtp-upgrade.md) | SMTP + HTML 模板 | F-026 |
| F-028 | [IM Bot 通道](features/F-028-im-bot-channel.md) | 飞书/企微/Slack Bot | F-026 |
| F-029 | [Webhook 通道](features/F-029-webhook-channel.md) | 自定义 Webhook | F-026 |
| F-030 | [通道选择策略](features/F-030-channel-selection.md) | 优先级 + 自动降级 | F-026, F-027, F-028, F-029 |
| F-031 | [通道健康检查](features/F-031-channel-health.md) | 可达性预检 + 面板 | F-026, F-030 |

---

## v0.2.1 — 组织导入

```
F-032 ──┬──→ F-033
        ├──→ F-034
        ├──→ F-035
        └──→ F-036
```

| 序号 | Feature | 说明 | 依赖 |
|------|---------|------|------|
| F-032 | [企业通讯录导入](features/F-032-org-contact-import.md) | LDAP/M365/飞书/企微 | F-002 |
| F-033 | [学校教务系统导入](features/F-033-edu-system-import.md) | API/CSV 导入课程-师生关系 | F-002 |
| F-034 | [关系智能推荐](features/F-034-relationship-suggestion.md) | 邮件/日历/IM 分析推荐 | F-002 |
| F-035 | [关系图谱可视化](features/F-035-graph-visualization.md) | 力导向图 + 交互 | F-002 |
| F-036 | [临时关系](features/F-036-temp-relationship.md) | 一次性关系 + 有效期 | F-002 |

---

## v0.3.0 — 协商协议 ★ 核心差异化

```
F-037 ──→ F-038 ──┬──→ F-039
                   ├──→ F-040
                   ├──→ F-041
                   └──→ F-042
```

| 序号 | Feature | 说明 | 依赖 |
|------|---------|------|------|
| F-037 | [Inbox 能力声明](features/F-037-inbox-capability-profile.md) | 格式/通道/窗口/负载注册 | F-016 |
| F-038 | [协商握手协议](features/F-038-negotiation-handshake.md) | QUERY→RESPONSE→PUSH→ACK | F-037 |
| F-039 | [协商失败处理](features/F-039-negotiation-fallback.md) | 无格式/无通道/免打扰/高负载 | F-038 |
| F-040 | [Agent 直连通道](features/F-040-agent-direct-channel.md) | WebRTC/QUIC E2E 加密直连 | F-038 |
| F-041 | [批处理协商](features/F-041-batch-negotiation.md) | 同类聚合投递 | F-038 |
| F-042 | [协商日志与调试](features/F-042-negotiation-log.md) | 全链路可追溯 | F-038 |

---

## v0.4.0 — 智能交付

```
F-043 ──→ F-046
F-044
F-045
F-047
```

| 序号 | Feature | 说明 | 依赖 |
|------|---------|------|------|
| F-043 | [活的交付物](features/F-043-live-delivery.md) | 传指针不传副本 | F-038 |
| F-044 | [条件交付](features/F-044-conditional-delivery.md) | 审批流/时间/数据/状态条件 | F-004, F-038 |
| F-045 | [可撤回交付](features/F-045-retractable-delivery.md) | 未读前可撤回 | F-021, F-006 |
| F-046 | [交付物生命周期管理](features/F-046-delivery-lifecycle.md) | 阅后即焚/定时失效/版本管理 | F-043, F-038 |
| F-047 | [交付链追踪](features/F-047-delivery-chain.md) | 转发链路可视化 | F-021 |

---

## v0.4.1 — 可执行交付物 + 反向交付

```
F-048 ──→ F-049
F-050 ──┬──→ F-051
        └──→ F-052
```

| 序号 | Feature | 说明 | 依赖 |
|------|---------|------|------|
| F-048 | [可执行交付物框架](features/F-048-executable-delivery.md) | 8 种收件内操作 | F-019 |
| F-049 | [操作结果回执](features/F-049-action-receipt.md) | 操作回传 + 审批流触发 | F-048, F-044 |
| F-050 | [反向交付（需求声明）](features/F-050-reverse-delivery.md) | 接收方发布需求驱动提交 | F-002 |
| F-051 | [需求模板](features/F-051-requirement-templates.md) | 3 个预置模板 | F-050 |
| F-052 | [需求-交付匹配](features/F-052-requirement-matching.md) | 产出自动匹配需求 | F-050, F-012 |

---

## v0.5.0 — 开放生态

```
F-053 ──┬──→ F-054 ──→ F-055
        ├──→ F-056
        └──→ F-057
```

| 序号 | Feature | 说明 | 依赖 |
|------|---------|------|------|
| F-053 | [开放交付协议 (DDP)](features/F-053-open-protocol.md) | 公开规范，三层协议 | F-038 |
| F-054 | [Agent SDK](features/F-054-agent-sdk.md) | 5 语言 SDK | F-053 |
| F-055 | [App 集成适配器](features/F-055-app-integrations.md) | VS Code/Jupyter/WPS/Notion | F-054 |
| F-056 | [跨组织交付](features/F-056-cross-org-delivery.md) | user@org + 安全校验 | F-053, F-037 |
| F-057 | [交付市场（模板）](features/F-057-delivery-marketplace.md) | 社区模板市场 | F-053 |

---

## 完整线性历史

```
v0.0.1              v0.0.2              v0.0.3
[MVP]               [文件夹监听]         [AI识别]
  │                    │                    │
F-001                  F-007                F-012
F-002                  F-008                F-013
F-003                  F-009                F-014
F-004                  F-010                F-015
F-005                  F-011
F-006

v0.1.0              v0.1.1              v0.2.0
[收件箱 ★闭环]       [格式转换]           [多通道]
  │                    │                    │
F-016                  F-022                F-026
F-017                  F-023                F-027
F-018                  F-024                F-028
F-019                  F-025                F-029
F-020                                      F-030
F-021                                      F-031

v0.2.1              v0.3.0              v0.4.0
[组织导入]           [协商协议 ★核心]      [智能交付]
  │                    │                    │
F-032                  F-037                F-043
F-033                  F-038                F-044
F-034                  F-039                F-045
F-035                  F-040                F-046
F-036                  F-041                F-047
                       F-042

v0.4.1              v0.5.0
[可执行+反向]         [开放生态]
  │                    │
F-048                  F-053
F-049                  F-054
F-050                  F-055
F-051                  F-056
F-052                  F-057
```
