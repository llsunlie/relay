# Relay 版本索引

## 目录结构

```
versions/
├── README.md                 # 本文件
├── TAG_TIMELINE.md           # 标签时间线（线性 feat 历史）
└── features/                 # 独立 Feature 文档（57 个）
    ├── F-001-system-share-menu.md
    ├── F-002-relationship-graph.md
    ├── ...
    └── F-057-delivery-marketplace.md
```

## 标签总览

| Tag | 名称 | Feature 数 | 累计 |
|-----|------|-----------|------|
| v0.0.1 | MVP | F-001 ~ F-006 | 6 |
| v0.0.2 | 文件夹监听 | F-007 ~ F-011 | 11 |
| v0.0.3 | AI 识别 | F-012 ~ F-015 | 15 |
| v0.1.0 | 收件箱（Inbox）★ 闭环 | F-016 ~ F-021 | 21 |
| v0.1.1 | 格式转换 | F-022 ~ F-025 | 25 |
| v0.2.0 | 多通道 | F-026 ~ F-031 | 31 |
| v0.2.1 | 组织导入 | F-032 ~ F-036 | 36 |
| v0.3.0 | 协商协议 ★ 核心 | F-037 ~ F-042 | 42 |
| v0.4.0 | 智能交付 | F-043 ~ F-047 | 47 |
| v0.4.1 | 可执行 + 反向交付 | F-048 ~ F-052 | 52 |
| v0.5.0 | 开放生态 | F-053 ~ F-057 | 57 |

## Feature 快速索引

### v0.0.1 MVP
| 编号 | Feature | 文件 |
|------|---------|------|
| F-001 | 系统分享菜单集成 | [features/F-001](features/F-001-system-share-menu.md) |
| F-002 | 关系图谱（手动建立） | [features/F-002](features/F-002-relationship-graph.md) |
| F-003 | 交付确认弹窗 | [features/F-003](features/F-003-delivery-confirm-dialog.md) |
| F-004 | 规则模板（5个预置） | [features/F-004](features/F-004-rule-templates.md) |
| F-005 | 邮件投递 | [features/F-005](features/F-005-email-delivery.md) |
| F-006 | 交付记录（本地） | [features/F-006](features/F-006-delivery-history.md) |

### v0.0.2 文件夹监听
| 编号 | Feature | 文件 |
|------|---------|------|
| F-007 | 文件夹监听引擎 | [features/F-007](features/F-007-folder-watcher.md) |
| F-008 | 子目录→类型映射 | [features/F-008](features/F-008-subfolder-mapping.md) |
| F-009 | 静默交付模式 | [features/F-009](features/F-009-silent-delivery.md) |
| F-010 | 交付前规则校验 | [features/F-010](features/F-010-rule-validation.md) |
| F-011 | 托盘状态指示 | [features/F-011](features/F-011-tray-indicator.md) |

### v0.0.3 AI 识别
| 编号 | Feature | 文件 |
|------|---------|------|
| F-012 | 文件内容 AI 分类器 | [features/F-012](features/F-012-ai-classifier.md) |
| F-013 | 分类结果反馈学习 | [features/F-013](features/F-013-feedback-learning.md) |
| F-014 | 元数据自动提取 | [features/F-014](features/F-014-metadata-extraction.md) |
| F-015 | 交付确认弹窗升级 | [features/F-015](features/F-015-confirm-dialog-v2.md) |

### v0.1.0 收件箱（Inbox）
| 编号 | Feature | 文件 |
|------|---------|------|
| F-016 | 本地收件箱界面 | [features/F-016](features/F-016-inbox-ui.md) |
| F-017 | 每日摘要通知 | [features/F-017](features/F-017-daily-digest.md) |
| F-018 | AI 预处理（影子收件人） | [features/F-018](features/F-018-ai-preprocessing.md) |
| F-019 | 收件动作 | [features/F-019](features/F-019-inbox-actions.md) |
| F-020 | 免打扰模式 | [features/F-020](features/F-020-dnd-mode.md) |
| F-021 | 发送方状态回传 | [features/F-021](features/F-021-status-feedback.md) |

### v0.1.1 格式转换
| 编号 | Feature | 文件 |
|------|---------|------|
| F-022 | 接收方格式偏好声明 | [features/F-022](features/F-022-format-preference.md) |
| F-023 | 格式转换管线 | [features/F-023](features/F-023-conversion-pipeline.md) |
| F-024 | 转换预览 | [features/F-024](features/F-024-conversion-preview.md) |
| F-025 | 转换质量指标 | [features/F-025](features/F-025-conversion-quality.md) |

### v0.2.0 多通道
| 编号 | Feature | 文件 |
|------|---------|------|
| F-026 | 通道抽象层 | [features/F-026](features/F-026-channel-abstraction.md) |
| F-027 | 邮件通道升级 | [features/F-027](features/F-027-smtp-upgrade.md) |
| F-028 | IM Bot 通道 | [features/F-028](features/F-028-im-bot-channel.md) |
| F-029 | Webhook 通道 | [features/F-029](features/F-029-webhook-channel.md) |
| F-030 | 通道选择策略 | [features/F-030](features/F-030-channel-selection.md) |
| F-031 | 通道健康检查 | [features/F-031](features/F-031-channel-health.md) |

### v0.2.1 组织导入
| 编号 | Feature | 文件 |
|------|---------|------|
| F-032 | 企业通讯录导入 | [features/F-032](features/F-032-org-contact-import.md) |
| F-033 | 学校教务系统导入 | [features/F-033](features/F-033-edu-system-import.md) |
| F-034 | 关系智能推荐 | [features/F-034](features/F-034-relationship-suggestion.md) |
| F-035 | 关系图谱可视化 | [features/F-035](features/F-035-graph-visualization.md) |
| F-036 | 临时关系 | [features/F-036](features/F-036-temp-relationship.md) |

### v0.3.0 协商协议
| 编号 | Feature | 文件 |
|------|---------|------|
| F-037 | Inbox 能力声明 | [features/F-037](features/F-037-inbox-capability-profile.md) |
| F-038 | 协商握手协议 | [features/F-038](features/F-038-negotiation-handshake.md) |
| F-039 | 协商失败处理 | [features/F-039](features/F-039-negotiation-fallback.md) |
| F-040 | Agent 直连通道 | [features/F-040](features/F-040-agent-direct-channel.md) |
| F-041 | 批处理协商 | [features/F-041](features/F-041-batch-negotiation.md) |
| F-042 | 协商日志与调试 | [features/F-042](features/F-042-negotiation-log.md) |

### v0.4.0 智能交付
| 编号 | Feature | 文件 |
|------|---------|------|
| F-043 | 活的交付物 | [features/F-043](features/F-043-live-delivery.md) |
| F-044 | 条件交付 | [features/F-044](features/F-044-conditional-delivery.md) |
| F-045 | 可撤回交付 | [features/F-045](features/F-045-retractable-delivery.md) |
| F-046 | 交付物生命周期管理 | [features/F-046](features/F-046-delivery-lifecycle.md) |
| F-047 | 交付链追踪 | [features/F-047](features/F-047-delivery-chain.md) |

### v0.4.1 可执行 + 反向交付
| 编号 | Feature | 文件 |
|------|---------|------|
| F-048 | 可执行交付物框架 | [features/F-048](features/F-048-executable-delivery.md) |
| F-049 | 操作结果回执 | [features/F-049](features/F-049-action-receipt.md) |
| F-050 | 反向交付（需求声明） | [features/F-050](features/F-050-reverse-delivery.md) |
| F-051 | 需求模板 | [features/F-051](features/F-051-requirement-templates.md) |
| F-052 | 需求-交付匹配 | [features/F-052](features/F-052-requirement-matching.md) |

### v0.5.0 开放生态
| 编号 | Feature | 文件 |
|------|---------|------|
| F-053 | 开放交付协议（DDP） | [features/F-053](features/F-053-open-protocol.md) |
| F-054 | Agent SDK | [features/F-054](features/F-054-agent-sdk.md) |
| F-055 | App 集成适配器 | [features/F-055](features/F-055-app-integrations.md) |
| F-056 | 跨组织交付 | [features/F-056](features/F-056-cross-org-delivery.md) |
| F-057 | 交付市场（模板） | [features/F-057](features/F-057-delivery-marketplace.md) |
