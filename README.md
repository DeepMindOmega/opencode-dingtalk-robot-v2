# 🤖 OpenCode DingTalk Robot Integration

<div align="center">

![Version](https://img.shields.io/badge/version-v1.1-blue)
![Python](https://img.shields.io/badge/python-3.7%2B-green)
![License](https://img.shields.io/badge/license-MIT-purple)
![Status](https://img.shields.io/badge/status-production%20ready-success)
![GitHub](https://img.shields.io/badge/github-open--dark)

**⚡ Seamlessly integrate OpenCode AI with DingTalk for intelligent team collaboration**

[Quick Start](#-quick-start) • [Features](#-features) • [Screenshots](#-screenshots) • [Documentation](#-documentation)

</div>

---

## ✨ Features

### 🎯 Core Capabilities

| Feature | Description |
|---------|-------------|
| 🤖 **AI-Powered Responses** | OpenCode processes queries intelligently with context awareness |
| 💬 **Multi-Chat Support** | Works in both group chats and private conversations |
| 🔄 **Session Management** | Automatic session isolation and context memory |
| 📊 **Token Tracking** | Real-time token usage display after every message |
| 🗜️ **Auto-Compact** | Automatically compresses sessions when tokens exceed 100,000 |
| 🖼️ **Media Support** | Send and receive images, screenshots, and files |
| 💾 **Smart Caching** | Leverages token caching for cost optimization |
| 🔄 **Auto-Reconnect** | Heartbeat monitoring with automatic connection recovery |

### 🚀 Advanced Features

\`\`\`
┌─────────────────────────────────────────────────────────────┐
│  🔐 Secure Token Management                              │
│  • Automatic refresh before expiration                      │
│  • Cached tokens for performance                           │
│  • Local config protection (config.local.json)               │
├─────────────────────────────────────────────────────────────┤
│  🧠 Intelligent Context Handling                           │
│  • Separate sessions for group & private chats               │
│  • Persistent memory across conversations                     │
│  • Automatic cleanup with /compact command                   │
├─────────────────────────────────────────────────────────────┤
│  🛡️ Robust Error Handling                                │
│  • Automatic retry with exponential backoff                   │
│  • Graceful degradation on failures                          │
│  • Detailed logging for debugging                             │
└─────────────────────────────────────────────────────────────┘
\`\`\`

---

## 🎬 Screenshots

### Setup Flow

\`\`\`\`
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   1. Clone   │  →  │   2. Config  │  →  │  3. Start    │
│              │     │              │     │              │
│  git clone   │     │  Edit config │     │ ./start.sh   │
└──────────────┘     └──────────────┘     └──────────────┘
                                               ↓
┌──────────────────────────────────────────────────────────────┐
│                    4. Ready to Use!                    │
│                                                            │
│    @OpenCodeBot in DingTalk group              │
│    User: "What's the weather?"                               │
│    Bot: ☁️ "Checking weather..." (shows processing)            │
│    Bot: 🌤 "Current: 25°C, Sunny" (AI response)           │
│                                                            │
│    📊 Token: 本次 1,234, 累计 45,678                    │
└──────────────────────────────────────────────────────────────┘
\`\`\`\`

### Token Display

\`\`\`\`
─────────────────────────────────────────────────────────────────
Your AI Response:
─────────────────────────────────────────────────────────────────
Here's the Python code to calculate fibonacci sequence...

\`\`\`python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)
\`\`\`

─────────────────────────────────────────────────────────────────
📊 **Token Usage**
─────────────────────────────────────────────────────────────────
• **Total**:  1,234,567
• **Input**:   987,654
• **Output**:  123,456
• **Reasoning**: 45,678
• **Cache Read**: 77,779
• **Session**: 1,234,567
─────────────────────────────────────────────────────────────────
\`\`\`\`

### Architecture Diagram

\`\`\`\`
┌──────────────────────────────────────────────────────────────────────────┐
│                        DingTalk Platform                           │
│                                                                  │
│   ┌──────────────┐    ┌──────────────┐    ┌──────────────┐   │
│   │  Group Chat  │    │ Private Chat │    │   Private Chat│   │
│   └──────┬───────┘    └──────┬───────┘    └──────┬───────┘   │
│          │                     │                     │            │
└──────────┼─────────────────────┼─────────────────────┼────────────┘
           │                     │                     │
           ↓                     ↓                     ↓
┌──────────────────────────────────────────────────────────────────────┐
│                   WebSocket Gateway                              │
│                  (gateway.py)                                    │
│                                                                  │
│  • Receives messages                                           │
│  • Queues tasks                                               │
│  • Manages connections                                         │
│  • Auto-refreshes token ⏰                                   │
└────────────────────┬───────────────────────────────────────────────┘
                     │
                     ↓
              ┌──────────────────┐
              │    Task Queue   │
              │ (queue_manager) │
              └──────┬──────────┘
                     │
                     ↓
┌──────────────────────────────────────────────────────────────────────┐
│                   OpenCode Processor                              │
│                  (processor.py)                                   │
│                                                                  │
│  • Pops tasks from queue                                    │
│  • Calls OpenCode CLI                                         │
│  • Tracks tokens 📊                                          │
│  • Auto-compacts sessions 🗜️                                  │
│  • Returns responses                                           │
└────────────────────┬───────────────────────────────────────────────┘
                     │
                     ↓
              ┌──────────────────┐
              │   OpenCode CLI  │
              └──────┬──────────┘
                     │
                     ↓
┌──────────────────────────────────────────────────────────────────────┐
│                     OpenCode AI                               │
│                                                                  │
│  • Processes queries                                           │
│  • Maintains context                                          │
│  • Generates responses                                         │
└────────────────────┬───────────────────────────────────────────────┘
                     │
                     ↓
              ┌──────────────────┐
              │   Response      │
              └──────┬──────────┘
                     │
                     ↓
              ┌──────────────────┐
              │  Send to       │
              │  DingTalk       │
              └──────┬──────────┘
                     │
                     ↓
              ┌──────────────────┐
              │   User sees    │
              │   Response ✨  │
              └──────────────────┘
\`\`\`\`

---

## 📦 Installation

### Step 1️⃣: Clone Repository

\`\`\`bash
git clone https://github.com/DeepMindOmega/opencode-dingtalk-robot-v2.git
cd opencode-dingtalk-robot-v2
\`\`\`

**Progress:** \`[████████████████████████████████] 100%\`

### Step 2️⃣: Configure Bot

🔐 **Create your local config:**

\`\`\`bash
cp config.example.json config.local.json
nano config.local.json
\`\`\`

**Edit \`config.local.json\`:**

\`\`\`json
{
  "CLIENT_ID": "your_dingtalk_app_key",
  "CLIENT_SECRET": "your_dingtalk_app_secret",
  "AUTHORIZED_USERS": [
    "user_id_1",
    "user_id_2"
  ],
  "QUEUE_DIR": "/path/to/queue"
}
\`\`\`

**Progress:** \`[████████████████████████████████] 100%\`

### Step 3️⃣: Get DingTalk Credentials

\`\`\`\`
┌─────────────────────────────────────────────────────────┐
│  1️⃣  Visit: https://open-dev.dingtalk.com/     │
│                                                      │
│  2️⃣  Create "Enterprise Internal Robot"            │
│                                                      │
│  3️⃣  Copy AppKey & AppSecret                      │
│                                                      │
│  4️⃣  Add to config.local.json                   │
│                                                      │
│  5️⃣  Add robot to your DingTalk group          │
└─────────────────────────────────────────────────────────┘
\`\`\`

**Progress:** \`[████████████████████████████████] 100%\`

### Step 4️⃣: Start Services

\`\`\`bash
./start.sh
\`\`\`

**Progress:** \`[████████████████████████████████] 100%\`

### 🎉 Installation Complete!

\`\`\`\`
╔═════════════════════════════════════════════════════════╗
║                                                               ║
║   ✓ OpenCode DingTalk Robot is now running!                 ║
║                                                               ║
║   Go to your DingTalk group and @OpenCodeBot         ║
║                                                               ║
║   Try: "Hello, who are you?"                                  ║
║                                                               ║
╚═════════════════════════════════════════════════════════╝
\`\`\`\`

---

## 🎮 Usage

### Basic Commands

| Command | Description | Example |
|---------|-------------|---------|
| List files | View current directory | \`列出文件\` |
| Read file | Read file contents | \`查看 README.md\` |
| Execute command | Run system command | \`执行 ls -la\` |
| System status | Check system info | \`状态\` |
| Help | Show help message | \`帮助\` |
| New conversation | Clear context | \`新对话\` |

---

## 📝 Changelog

### [v1.1] - 2026-02-16

\`\`\`\`
✨ New Features:
• 📊 Detailed token tracking (total, input, output, reasoning, cache)
• 🗜️ Automatic compact when tokens exceed 100,000
• ⏰ Auto-refresh Access Token in heartbeat (prevents expiration)
• 🔐 Fixed private & group chat session isolation
• 🐛 Fixed OpenCode token parsing path error
• 🎨 Enhanced token display format with comma-separated numbers

🐛 Bug Fixes:
• Fixed "无输出" issue in group chats
• Fixed session ID reuse across chat types
• Fixed token always showing 0
\`\`\`\`

---

## 🤝 Contributing

\`\`\`\`
╔═════════════════════════════════════════════════════════╗
║           We love contributions! 🎉                      ║
╚═════════════════════════════════════════════════════════╝

How to contribute:

1️⃣  Fork this repository
2️⃣  Create your feature branch: git checkout -b feature/AmazingFeature
3️⃣  Commit your changes: git commit -m 'Add some AmazingFeature'
4️⃣  Push to the branch: git push origin feature/AmazingFeature
5️⃣  Open a Pull Request
\`\`\`\`

---

## 📄 License

MIT License - See LICENSE file

---

<div align="center">

\`\`\`\`
╔═════════════════════════════════════════════════════════════════════╗
║                                                                     ║
║    ⭐ If you find this project helpful, please give it a star! ⭐   ║
║                                                                     ║
║     Made with ❤️ by DeepMindOmega                                    ║
║                                                                     ║
╚═════════════════════════════════════════════════════════════════════╝
\`\`\`\`

</div>
