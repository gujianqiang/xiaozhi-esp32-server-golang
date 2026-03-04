# OpenClaw 接入说明

## 架构图

```mermaid
flowchart LR
  Device[设备语音输入] --> ASR[主服务 STT/ChatSession]
  ASR --> Route{OpenClaw关键词路由}
  Route -- 打开龙虾 / 进入龙虾 --> OCSession[OpenClaw 会话]
  Route -- 其他文本 --> LLM[普通 LLM 对话链路]
  OCSession --> Plugin[xiaozhi 插件]
  Plugin --> Endpoint[接入点 URL<br/>ws://.../ws/openclaw?token=...]
  Endpoint --> OCSession
```

## 安装步骤

1. 确保 OpenClaw 已正常运行。
2. openclaw 执行插件安装命令：
   `openclaw plugins install @xiaozhi_openclaw/xiaozhi`
3. 重启openclaw `openclaw gateway restart` 
4. 查看插件是否安装成功 `openclaw plugins list | grep xiaozhi`

## 使用方法

1. 将接入点 URL 发送给 OpenClaw。
2. 在 OpenClaw 会话中让它配置 `xiaozhi` 插件（使用该接入点 URL）。
例:
`ws://xxx.xxx.cn:8990/ws/openclaw?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoyLCJhZ2VudF9pZCI6IjIiLCJlbmRwb2ludF9pZCI6ImFnZW50XzIiLCJwdXJwb3NlIjoib3BlbmNsYXctZW5kcG9pbnQifQ.XBAwpEvagasgsmGvbw7nqySrBk_LA45NRSBvW1-9IQg 配置下xiaozhi 渠道`
3. 安装和配置完成后，即可在 OpenClaw 会话中调用 xiaozhi 插件能力。
4. 在 `查看openclaw` 弹层可使用“发送测试”验证连通性与回复。
5. 在设备侧可通过 `打开龙虾` / `进入龙虾` 进入 OpenClaw 模式，通过 `关闭龙虾` / `退出龙虾` 退出模式。

## 排查建议

- 状态显示未连接：确认 OpenClaw 已用接入点 URL 建立会话。
- 对话测试超时：检查插件是否安装成功、接入点 URL 是否正确、OpenClaw 会话是否在线。
