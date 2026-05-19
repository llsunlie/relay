# F-029 Webhook 通道

**里程碑**: v0.2.0 (多通道)

## 描述

接收方可注册自定义 Webhook URL，交付器以标准 JSON 格式 POST 到 Webhook。支持自定义 Header（Token 鉴权等）。用于对接自建系统（课程平台、OA 等）。

## 依赖

- F-026 通道抽象层

## 成功标准

- Webhook 注册和投递完整可用
- 鉴权失败时正确报错
