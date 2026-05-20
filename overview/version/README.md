# Relay 版本索引

## 目录结构

```
versions/
├── README.md                 # 本文件
├── TAG_TIMELINE.md           # 标签时间线（线性 feat 历史）
└── features/                 # 独立 Feature 文档（41 个）
    ├── F-001-drag-to-deliver.md
    ├── F-002-delivery-target.md
    ├── ...
    └── F-041-cross-org-delivery.md
```

## 标签总览

| Tag | 名称 | Feature 数 | 累计 |
|-----|------|-----------|------|
| v0.0.1 | MVP | F-001 ~ F-006 | 6 |
| v0.0.2 | 文件夹监听 | F-007 ~ F-010 | 10 |
| v0.0.3 | AI 识别 | F-011 ~ F-014 | 14 |
| v0.1.0 | 收件箱（Inbox）★ 闭环 | F-015 ~ F-019 | 19 |
| v0.1.1 | 格式转换 | F-020 ~ F-022 | 22 |
| v0.2.0 | 多通道 | F-023 ~ F-028 | 28 |
| v0.2.1 | 组织导入 | F-029 | 29 |
| v0.3.0 | 协商协议 ★ 核心 | F-030 ~ F-034 | 34 |
| v0.4.0 | 智能交付 | F-035 ~ F-036 | 36 |
| v0.4.1 | 反向交付 | F-037 ~ F-038 | 38 |
| v0.5.0 | 开放生态 | F-039 ~ F-041 | 41 |

## Feature 快速索引

### v0.0.1 MVP
| 编号 | Feature | 文件 |
|------|---------|------|
| F-001 | 拖拽交付触发 | [features/F-001](features/F-001-drag-to-deliver.md) |
| F-002 | 交付对象 | [features/F-002](features/F-002-delivery-target.md) |
| F-003 | 交付窗口 | [features/F-003](features/F-003-delivery-window.md) |
| F-004 | 规则模板 | [features/F-004](features/F-004-rule-templates.md) |
| F-005 | 邮件投递 | [features/F-005](features/F-005-email-delivery.md) |
| F-006 | 交付记录 | [features/F-006](features/F-006-delivery-history.md) |

### v0.0.2 文件夹监听
| 编号 | Feature | 文件 |
|------|---------|------|
| F-007 | 文件夹监听引擎 | [features/F-007](features/F-007-folder-watcher.md) |
| F-008 | 静默交付 | [features/F-008](features/F-008-silent-delivery.md) |
| F-009 | 交付前校验 | [features/F-009](features/F-009-rule-validation.md) |
| F-010 | 托盘状态指示 | [features/F-010](features/F-010-tray-indicator.md) |

### v0.0.3 AI 识别
| 编号 | Feature | 文件 |
|------|---------|------|
| F-011 | AI 分类器 | [features/F-011](features/F-011-ai-classifier.md) |
| F-012 | 分类反馈学习 | [features/F-012](features/F-012-feedback-learning.md) |
| F-013 | 元数据自动提取 | [features/F-013](features/F-013-metadata-extraction.md) |
| F-014 | 收件人智能推荐 | [features/F-014](features/F-014-smart-recipient.md) |

### v0.1.0 收件箱（Inbox）
| 编号 | Feature | 文件 |
|------|---------|------|
| F-015 | 收件箱界面 | [features/F-015](features/F-015-inbox-ui.md) |
| F-016 | 邮件入站监听 | [features/F-016](features/F-016-mail-inbound.md) |
| F-017 | 每日摘要通知 | [features/F-017](features/F-017-daily-digest.md) |
| F-018 | AI 收件预处理 | [features/F-018](features/F-018-ai-preprocessing.md) |
| F-019 | 免打扰模式 | [features/F-019](features/F-019-dnd-mode.md) |

### v0.1.1 格式转换
| 编号 | Feature | 文件 |
|------|---------|------|
| F-020 | 接收方格式偏好 | [features/F-020](features/F-020-format-preference.md) |
| F-021 | 格式转换引擎 | [features/F-021](features/F-021-conversion-pipeline.md) |
| F-022 | 转换预览 | [features/F-022](features/F-022-conversion-preview.md) |

### v0.2.0 多通道
| 编号 | Feature | 文件 |
|------|---------|------|
| F-023 | 通道抽象层 | [features/F-023](features/F-023-channel-abstraction.md) |
| F-024 | IM Bot 通道 | [features/F-024](features/F-024-im-bot-channel.md) |
| F-025 | Webhook 通道 | [features/F-025](features/F-025-webhook-channel.md) |
| F-026 | Agent 直连通道 | [features/F-026](features/F-026-agent-direct-channel.md) |
| F-027 | 通道选择策略 | [features/F-027](features/F-027-channel-selection.md) |
| F-028 | 通道健康检查 | [features/F-028](features/F-028-channel-health.md) |

### v0.2.1 组织导入
| 编号 | Feature | 文件 |
|------|---------|------|
| F-029 | 企业通讯录导入 | [features/F-029](features/F-029-org-contact-import.md) |

### v0.3.0 协商协议
| 编号 | Feature | 文件 |
|------|---------|------|
| F-030 | Inbox 能力声明 | [features/F-030](features/F-030-inbox-capability-profile.md) |
| F-031 | 协商握手协议 | [features/F-031](features/F-031-negotiation-handshake.md) |
| F-032 | 协商失败处理 | [features/F-032](features/F-032-negotiation-fallback.md) |
| F-033 | 批处理协商 | [features/F-033](features/F-033-batch-negotiation.md) |
| F-034 | 协商日志 | [features/F-034](features/F-034-negotiation-log.md) |

### v0.4.0 智能交付
| 编号 | Feature | 文件 |
|------|---------|------|
| F-035 | 活的交付物 | [features/F-035](features/F-035-live-delivery.md) |
| F-036 | 可撤回交付 | [features/F-036](features/F-036-retractable-delivery.md) |

### v0.4.1 反向交付
| 编号 | Feature | 文件 |
|------|---------|------|
| F-037 | 反向交付（需求声明） | [features/F-037](features/F-037-reverse-delivery.md) |
| F-038 | 需求-交付匹配 | [features/F-038](features/F-038-requirement-matching.md) |

### v0.5.0 开放生态
| 编号 | Feature | 文件 |
|------|---------|------|
| F-039 | 开放交付协议 | [features/F-039](features/F-039-open-protocol.md) |
| F-040 | Agent SDK | [features/F-040](features/F-040-agent-sdk.md) |
| F-041 | 跨组织交付 | [features/F-041](features/F-041-cross-org-delivery.md) |
