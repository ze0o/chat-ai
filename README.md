# 💬 Abo AL3Z AI: Flutter Chatbot with Google Gemini

A clean, single-screen AI chat app built with **Flutter** and the **Google Gemini API**.
Type a question, get an answer, and keep the conversation going: the app keeps the chat
history in a session, so Gemini remembers what you said earlier in the conversation.

![Flutter](https://img.shields.io/badge/Flutter-02569B?logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?logo=dart&logoColor=white)
![Gemini](https://img.shields.io/badge/Google%20Gemini-8E75B2?logo=googlegemini&logoColor=white)
![Material 3](https://img.shields.io/badge/Material%203-757575?logo=materialdesign&logoColor=white)

---

## Features

- **Multi-turn chat with memory**: messages go through a Gemini `ChatSession`, so follow-up questions keep their context
- **Chat bubbles** for user and AI messages, with auto-scroll to the newest message
- **Loading indicator** while the model is answering
- **Clear conversation** button that empties the screen *and* resets the AI's memory
- **Error handling**: network or API errors are shown in the chat instead of crashing the app
- Material 3 design, runs on Android, iOS, web and desktop

## Tech stack

| Layer | Technology |
|---|---|
| UI | Flutter (Material 3) |
| Language | Dart |
| AI model | Google Gemini via [`google_generative_ai`](https://pub.dev/packages/google_generative_ai) |
| State | `StatefulWidget` + `setState` |

## How it works

```
User types a message
        │
        ▼
_handleSubmitted() ──► adds the message to the list, shows the loading bar
        │
        ▼
ChatSession.sendMessage()  ──►  Gemini API (keeps the history of this session)
        │
        ▼
Reply added as an AI bubble ──► list scrolls to the bottom
```

All the app code is in [`chat_ai/lib/main.dart`](chat_ai/lib/main.dart):

| Part | Role |
|---|---|
| `ChatBotApp` | App entry, theme |
| `ChatMessage` | Model for one message (text + who sent it) |
| `ChatScreen` | Chat screen: message list, input box, send and clear actions |

## Getting started

**Requirements:** Flutter SDK (Dart 3), a free Gemini API key from [Google AI Studio](https://aistudio.google.com/app/apikey).

```bash
git clone https://github.com/ze0o/chat-ai.git
cd chat-ai/chat_ai
flutter pub get
flutter run
```

Put your own API key where the `GenerativeModel` is created in `lib/main.dart`.
For anything beyond local testing, don't keep the key in source code: pass it at build time
(`--dart-define=GEMINI_API_KEY=...` and read it with `String.fromEnvironment`) or call Gemini
from a small backend.

## Project structure

```
chat-ai/
└── chat_ai/            Flutter project
    ├── lib/main.dart   the whole app
    ├── test/           widget test
    └── android/ ios/ web/ linux/ macos/ windows/
```

## What I learned

- Calling a large language model API from a mobile app
- Keeping conversation context with a chat session instead of single prompts
- Handling async calls, loading states and errors in Flutter UI
- Why API keys should never be shipped inside client code

## Ideas for next steps

- Streaming responses (word by word) with `sendMessageStream`
- Markdown rendering for code blocks and lists in AI answers
- Saving chat history locally
- Moving the API key to a backend proxy

---

Made by **Abdulaziz Abdulhadi** · [GitHub](https://github.com/ze0o) · [LinkedIn](https://www.linkedin.com/in/abdulaziz-abdulhadi-5510a1332) · [Portfolio](https://3ziz-portfolio.netlify.app/)
