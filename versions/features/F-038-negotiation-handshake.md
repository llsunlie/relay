# F-038 协商握手协议

**里程碑**: v0.3.0 (协商协议)

## 描述

Sender 在发送前发起 CAPABILITY_QUERY → Inbox 返回 CAPABILITY_RESPONSE → Sender 做适配决策（格式/通道/时机）→ DELIVERY_PUSH → Inbox 返回 DELIVERY_ACK。TCP 式语义层握手。

## 依赖

- F-037 Inbox 能力声明

## 成功标准

- 协商全流程 < 2 秒
- 协商成功率 > 95%
