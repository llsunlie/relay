# Relay 标签时间线

## v0.0.1 — MVP（手动交付通道）

```
F-001 ──→ F-002 ──→ F-003 ──→ F-004
  │                                │
  └──── F-005 ──→ F-006 ──────────┘
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-001 | [拖拽交付触发](features/F-001-drag-to-deliver.md) | 拖拽文件 → 投放卡片 → Relay |
| F-002 | [交付对象](features/F-002-delivery-target.md) | 管理交付对象（个人/系统） |
| F-003 | [交付窗口](features/F-003-delivery-window.md) | 类型、收件人、摘要、留言、确认 |
| F-004 | [规则模板](features/F-004-rule-templates.md) | 文件名关键词匹配收件人角色 |
| F-005 | [邮件投递](features/F-005-email-delivery.md) | SMTP 直发 |
| F-006 | [交付记录](features/F-006-delivery-history.md) | 历史列表 + 重发 + 搜索 |

---

## v0.0.2 — 文件夹监听

```
F-007 ──┬──→ F-008
        ├──→ F-009
        └──→ F-010
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-007 | [文件夹监听引擎](features/F-007-folder-watcher.md) | 监控 ~/.relay/outbox/ |
| F-008 | [静默交付](features/F-008-silent-delivery.md) | 规则匹配直接发不弹窗 |
| F-009 | [交付前校验](features/F-009-rule-validation.md) | 收件人存在性校验 |
| F-010 | [托盘状态指示](features/F-010-tray-indicator.md) | 绿/黄/红三色 + 快捷面板 |

---

## v0.0.3 — AI 识别

```
F-011 ──┬──→ F-012
        ├──→ F-013
        └──→ F-014
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-011 | [AI 分类器](features/F-011-ai-classifier.md) | 本地推理判断交付类型 |
| F-012 | [分类反馈学习](features/F-012-feedback-learning.md) | 用户修正 → 本地调优 |
| F-013 | [元数据自动提取](features/F-013-metadata-extraction.md) | 提取周期、课程、金额等 |
| F-014 | [收件人智能推荐](features/F-014-smart-recipient.md) | AI 分析内容推荐具体收件人 |

---

## v0.1.0 — 收件箱（Inbox）★ 闭环

```
F-015 ──┬──→ F-016 ──→ F-017
        ├──→ F-018
        └──→ F-019
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-015 | [收件箱界面](features/F-015-inbox-ui.md) | 待处理/已归档两区 + 搜索筛选 |
| F-016 | [邮件入站监听](features/F-016-mail-inbound.md) | IMAP 监听邮箱，邮件进入收件箱 |
| F-017 | [每日摘要通知](features/F-017-daily-digest.md) | 每天 8:30 推送摘要 |
| F-018 | [AI 收件预处理](features/F-018-ai-preprocessing.md) | 摘要 + 待办提取 |
| F-019 | [免打扰模式](features/F-019-dnd-mode.md) | 时段内不推送通知 |

---

## v0.1.1 — 格式转换

```
F-020 ──→ F-021 ──→ F-022
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-020 | [接收方格式偏好](features/F-020-format-preference.md) | 按类型声明偏好格式 |
| F-021 | [格式转换引擎](features/F-021-conversion-pipeline.md) | md↔html/pdf/txt, docx↔md/pdf |
| F-022 | [转换预览](features/F-022-conversion-preview.md) | 预览转换结果，可切换原格式 |

---

## v0.2.0 — 多通道

```
F-023 ──┬──→ F-024
        ├──→ F-025
        ├──→ F-026
        ├──→ F-027 ──→ F-028
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-023 | [通道抽象层](features/F-023-channel-abstraction.md) | 统一通道接口，新增通道实现适配器 |
| F-024 | [IM Bot 通道](features/F-024-im-bot-channel.md) | 飞书/企微/Slack Bot 私信卡片 |
| F-025 | [Webhook 通道](features/F-025-webhook-channel.md) | 自定义 Webhook，JSON 投递 |
| F-026 | [Agent 直连通道](features/F-026-agent-direct-channel.md) | 端到端加密直连，断点续传 |
| F-027 | [通道选择策略](features/F-027-channel-selection.md) | 优先级 + 自动降级 + 手动指定 |
| F-028 | [通道健康检查](features/F-028-channel-health.md) | 发送前检查 + 状态面板 |

---

## v0.2.1 — 组织导入

```
F-029
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-029 | [企业通讯录导入](features/F-029-org-contact-import.md) | LDAP/M365/飞书/企微自动导入 |

---

## v0.3.0 — 协商协议 ★ 核心差异化

```
F-030 ──→ F-031 ──┬──→ F-032
                   ├──→ F-033
                   └──→ F-034
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-030 | [Inbox 能力声明](features/F-030-inbox-capability-profile.md) | 声明交付类型/格式/通道/窗口 |
| F-031 | [协商握手协议](features/F-031-negotiation-handshake.md) | 查询→响应→适配→推送→确认 |
| F-032 | [协商失败处理](features/F-032-negotiation-fallback.md) | 无格式→转换/取消，无通道→降级邮件 |
| F-033 | [批处理协商](features/F-033-batch-negotiation.md) | 同类型同对象自动打包 |
| F-034 | [协商日志](features/F-034-negotiation-log.md) | 全链路记录可追溯 |

---

## v0.4.0 — 智能交付

```
F-035
F-036
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-035 | [活的交付物](features/F-035-live-delivery.md) | 传指针不传副本，接收方实时拉取 |
| F-036 | [可撤回交付](features/F-036-retractable-delivery.md) | Agent 直连下未读可撤回 |

---

## v0.4.1 — 反向交付

```
F-037 ──→ F-038
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-037 | [反向交付（需求声明）](features/F-037-reverse-delivery.md) | 接收方发布需求，发送方匹配提交 |
| F-038 | [需求-交付匹配](features/F-038-requirement-matching.md) | 产出自动匹配需求声明 |

---

## v0.5.0 — 开放生态

```
F-039 ──┬──→ F-040
        └──→ F-041
```

| 序号 | Feature | 说明 |
|------|---------|------|
| F-039 | [开放交付协议](features/F-039-open-protocol.md) | 公开规范文档，版本化向后兼容 |
| F-040 | [Agent SDK](features/F-040-agent-sdk.md) | Node.js/Python/Go SDK |
| F-041 | [跨组织交付](features/F-041-cross-org-delivery.md) | user@org 身份 + 安全校验 |

---

## 完整线性历史

```
v0.0.1              v0.0.2              v0.0.3
[MVP]               [文件夹监听]         [AI识别]
  │                    │                    │
F-001                  F-007                F-011
F-002                  F-008                F-012
F-003                  F-009                F-013
F-004                  F-010                F-014
F-005
F-006

v0.1.0              v0.1.1              v0.2.0
[收件箱 ★闭环]       [格式转换]           [多通道]
  │                    │                    │
F-015                  F-020                F-023
F-016                  F-021                F-024
F-017                  F-022                F-025
F-018                                      F-026
F-019                                      F-027
                                           F-028

v0.2.1              v0.3.0              v0.4.0
[组织导入]           [协商协议 ★核心]      [智能交付]
  │                    │                    │
F-029                  F-030                F-035
                       F-031                F-036
                       F-032
                       F-033
                       F-034

v0.4.1              v0.5.0
[反向交付]           [开放生态]
  │                    │
F-037                  F-039
F-038                  F-040
                       F-041
```
