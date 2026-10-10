# FoloToy AI Passport — 小智 AI 对话机器人（玩法分支）

> 本分支：`feature/xiaozhi-ai-chatbot`
> 分支基线：`upstream/main`（`a06235e`，2026-10-10 与上游同步）
> 玩法来源：[官方作品页](https://ai-passport.folotoy.cn/plays/xiaozhi-ai-chatbot/) · [FoloToy 开源仓库](https://github.com/FoloToy/folo-ai-passport-xiaozhi)

## 这是什么

**小智 AI 对话机器人**是 FoloToy AI Passport 的官方玩法之一：把设备变成一个能对话的 AI 旅行伴侶。按住设备按键说话，云端小智（XiaoZhi）AI 听懂并回复，屏幕与扬声器给出状态与声音反馈。

### 设备边界（务必先读）

AI Passport **不是**一台在本地运行大模型的独立 AI 电脑。本玩法依赖 **网络 + 云端服务（xiaozhi.me）中转**：

| 设备负责 | 依赖网络/云端 |
|---|---|
| 按键（录音开始/结束） | 语音识别（STT） |
| 麦克风录音 | 大模型对话（LLM） |
| 屏幕状态显示 | 语音合成（TTS） |
| 扬声器播放 | 多语言/角色配置 |
| Wi-Fi 连接与状态 | 账号与服务器连接 |

设备本地不跑大模型；断网时对话类能力不可用，仅有基础状态反馈。

## 固件来源（重要）

本玩法固件本体是**独立仓库** `FoloToy/folo-ai-passport-xiaozhi`（xiaozhi-esp32 v2.5.0 核心 + FoloToy AI Passport 板级定义），**不是本仓库 fork 的一部分**。本分支只承载**玩法编排层**（说明、构建方式、集成配置），固件源码以该独立仓库为唯一事实源。

- 固件仓库：<https://github.com/FoloToy/folo-ai-passport-xiaozhi>
- 板级工程：仅含 ESP32-C3 板卡实现（`folotoy/ai-passport`）
- SDK 要求：ESP-IDF **v6.0.1+**（推荐 6.1，v5.x 不再支持）

## 构建与烧录

按固件仓库 [README](https://github.com/FoloToy/folo-ai-passport-xiaozhi) 执行（以下为其标准流程）：

```bash
# 1. 准备 ESP-IDF v6.1 环境（见固件仓库 README）
# 2. 克隆并进入固件仓库
git clone https://github.com/FoloToy/folo-ai-passport-xiaozhi.git
cd folo-ai-passport-xiaozhi

# 3. 构建 ai-passport 板级固件（中文）
python scripts/build.py folotoy/ai-passport --name ai-passport --language zh-CN

# 4. 烧录（设备 USB 连接电脑后）
idf.py -p <串口> flash monitor
```

> 串口路径：macOS 常见 `/dev/cu.usbmodem*`；Windows 常见 `COMx`。

## 使用流程

1. 首次使用：设备配网（参见官方 App/小程序引导，将 Wi-Fi 信息写入设备）
2. 开机联网后，设备连接默认服务器 `xiaozhi.me`
3. 按下设备按键 → 说话 → 松开 → 云端回复并播放
4. 屏幕显示对话/录音/网络状态

## 服务器与账号

- 默认连接官方 xiaozhi.me 服务（免费/需注册账号）
- 自定义 API Key 与大模型服务商配置方式见固件仓库文档（本文不展开，以固件仓库为准）

## 分支说明

- `main`：官方基线，用于同步 `FoloToy/ai-passport` 上游（本 fork 的 `main` 保持最小差异）
- `feature/xiaozhi-ai-chatbot`：**本分支**，只包含小智玩法的编排层内容
- 玩法调整/固件定制：在固件仓库 `folo-ai-passport-xiaozhi` 内进行，不在本分支改固件

## 相关链接

- 作品页：<https://ai-passport.folotoy.cn/plays/xiaozhi-ai-chatbot/>
- 固件仓库：<https://github.com/FoloToy/folo-ai-passport-xiaozhi>
- 官方主仓：<https://github.com/FoloToy/ai-passport>
- 项目工作区（规范/文档）：<https://github.com/Richardkaka/MyFoloToy>