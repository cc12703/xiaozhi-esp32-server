

## 项目概述

xiaozhi-esp32-server 是面向 ESP32 设备的 AI 语音助手服务端

## 重要
* MUST 

## 技术栈
* Python 3.10
* 基于 asyncio 


## 架构

### 服务端（两个并发的 asyncio 服务）
- **WebSocket**（`core/websocket_server.py`，端口 8000）— 主要的设备通信和音频流传输
- **HTTP**（`core/http_server.py`，端口 8003）— OTA 固件更新和视觉分析 API

### 消息流
```
ESP32 设备 → WebSocket → ConnectionHandler (core/connection.py)
  → ASR（语音转文字）→ LLM（生成回复）→ TTS（文字转语音）
  → 音频通过 WebSocket 流式回传
```

## 文件说明
* `app.py` 入口文件
* `core/providers/` 服务提供者
  - `llm/` LLM 提供者 
  - `tts/` TTS 提供者（讯飞、腾讯、阿里云、Edge TTS 等），基类：`TTSProviderBase`
  - `asr/` ASR 提供者，基类：`ASRProviderBase`
  - `vad/` 语音活动检测 
  - `vllm/` 视觉语言模型
  - `intent/` 意图识别
  - `memory/` 上下文记忆（本地、mem0ai）
  - `tools/`  函数调用工具实现
* `core/connection.py` 连接处理
* `core/handle/` 消息处理器
* `core/utils/` 关键工具模块
* `plugins_func/` 插件系统





