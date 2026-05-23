# 🤖 AI-Powered Conversational Chatbot

A real-time AI chat application built with **React** and the **OpenAI API**, featuring token-by-token streaming responses, multi-turn conversation memory, and a clean dark-mode UI.

---

## ⚡ Features

- **Real-time streaming** — responses appear token-by-token using OpenAI's SSE stream (no waiting for full response)
- **Multi-turn memory** — sliding-window context manager maintains coherent conversations up to 20+ exchanges
- **State machine UI** — handles loading, streaming, error, and retry states cleanly
- **Blinking cursor** — visual feedback during streaming, just like modern AI chat apps
- **Keyboard shortcuts** — Enter to send, Shift+Enter for new line
- **Auto-scroll** — chat window follows the latest message automatically

---

## 🏗️ Architecture

```
User types message
       │
       ▼
  React State (messages[])
       │
       ▼
  Sliding Window (last 10 msgs)  ←── keeps token usage within limits
       │
       ▼
  OpenAI API (stream: true)
       │
       ▼
  ReadableStream → SSE chunks
       │
       ▼
  onToken() callback → updates UI per token
       │
       ▼
  Real-time bubble update in React
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| UI Framework | React 18 + Vite |
| AI Backend | OpenAI GPT-3.5-turbo |
| Streaming | Fetch API + ReadableStream (SSE) |
| Styling | Plain CSS (no framework) |
| Language | JavaScript (ES2022) |

---

## 🚀 Run Locally

```bash
# 1. Clone the repo
git clone https://github.com/iam-hariii/ai-chatbot.git
cd ai-chatbot

# 2. Install dependencies
npm install

# 3. Set up your API key
cp .env.example .env
# Edit .env and add your OpenAI API key

# 4. Start the dev server
npm run dev
```

App will be live at: `http://localhost:5173`

---

## 📁 Project Structure

```
ai-chatbot/
├── src/
│   ├── App.jsx              # Root component — conversation state & logic
│   ├── api.js               # OpenAI streaming API integration
│   ├── App.css
│   └── components/
│       ├── ChatWindow.jsx   # Scrollable message list
│       ├── ChatInput.jsx    # Textarea + send button
│       ├── MessageBubble.jsx # Individual message with streaming cursor
│       ├── ChatWindow.css
│       ├── ChatInput.css
│       └── MessageBubble.css
├── index.html
├── package.json
├── vite.config.js
└── .env.example
```

---

## 🧠 Key Design Decisions

- **SSE over WebSockets** — OpenAI's API uses Server-Sent Events for streaming; Fetch + ReadableStream handles this natively without extra libraries
- **Sliding window (last 10 msgs)** — prevents token limit overflow in long conversations while preserving recent context
- **Optimistic UI** — assistant bubble is added immediately with a blinking cursor, then filled token-by-token
- **Error boundary** — failed API calls remove the placeholder bubble and show a recoverable error banner

---

## 👤 Author

**Hari Balaji C** — [LinkedIn](https://linkedin.com/in/haribalaji) · [GitHub](https://github.com/iam-hariii)
