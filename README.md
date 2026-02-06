# Chatbot Template

> **Drop-in AI chatbot components for any React project.**

![Version](https://img.shields.io/badge/version-0.1.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Build Status](https://img.shields.io/badge/status-Development-yellow.svg)

---

## What & Why

**The Problem:**
Adding an AI chatbot to your React app means wrestling with streaming APIs, state management, styling inconsistencies, and provider lock-in—all before your users can send a single message.

**Our Solution:**
Chatbot Template is a provider-agnostic component library that gives you a production-ready chat UI out of the box. Configure your AI provider, drop in `<ChatBot />`, and ship. Use the playground app to visually customize styles and export your config.

---

## Quick Start

```bash
# Clone and install
git clone https://github.com/G-Hensley/chatbot-template.git
cd chatbot-template
pnpm install

# Run the playground app
pnpm dev

# Run tests
pnpm test
```

### Using the Package (coming soon)

```bash
pnpm add @codaissance/chatbot
```

```tsx
import { ChatBot } from '@codaissance/chatbot';

function App() {
  return (
    <ChatBot
      provider="anthropic"
      model="claude-3-5-haiku-20241022"
      systemPrompt="You are a helpful assistant."
    />
  );
}
```

---

## Visual Preview

```
┌─────────────────────────────────────────────────────────────┐
│  PACKAGE                         PLAYGROUND                 │
│  ────────                        ──────────                 │
│  @codaissance/chatbot    ───▶    Visual Configurator        │
│                                                             │
│  • ChatBot component             • Style presets            │
│  • Streaming hooks               • Color schemes            │
│  • Provider abstraction          • Live preview             │
│  • Style presets                 • Export config            │
└─────────────────────────────────────────────────────────────┘
```

---

## Documentation

Full documentation is available in our **[Wiki](https://github.com/G-Hensley/chatbot-template/wiki)**:

| Guide | Description |
|-------|-------------|
| [Getting Started](https://github.com/G-Hensley/chatbot-template/wiki/Getting-Started) | Installation, configuration, first chatbot |
| [Configuration](https://github.com/G-Hensley/chatbot-template/wiki/Configuration) | All config options explained |
| [Styling](https://github.com/G-Hensley/chatbot-template/wiki/Styling) | Morphism presets, theming, customization |
| [Providers](https://github.com/G-Hensley/chatbot-template/wiki/Providers) | Anthropic, OpenAI, and adding your own |
| [API Reference](https://github.com/G-Hensley/chatbot-template/wiki/API) | GraphQL schema, component props, hooks |
| [Contributing](CONTRIBUTING.md) | How to contribute to this project |

---

## Tech Stack

| Category | Technology |
|----------|------------|
| Language | TypeScript |
| Framework | React, Next.js (playground) |
| Styling | Tailwind CSS |
| AI SDK | Vercel AI SDK |
| API | GraphQL (Apollo Server) |
| Testing | Vitest |
| Package Manager | pnpm (workspaces) |

**Default Model:** Claude 3.5 Haiku (configurable)

---

## Project Structure

```
chatbot-template/
├── packages/
│   └── chatbot-core/       # Reusable component library
│       ├── components/     # ChatBot, ChatWindow, ChatInput, etc.
│       ├── hooks/          # useChat, useChatConfig, useStreaming
│       ├── styles/         # Presets (flat, neumorphism, glass, clay)
│       └── providers/      # AI provider abstraction
├── apps/
│   └── playground/         # Next.js configurator webapp
│       ├── app/            # Pages and API routes
│       └── components/     # Configurator UI, Preview panel
├── docs/                   # Documentation
└── prompts/                # LLM prompt templates for setup help
```

---

## Features

- **Provider Agnostic** - Works with Anthropic, OpenAI, and custom providers
- **Streaming First** - Token-by-token rendering with abort support
- **Style Presets** - Flat, Neumorphism, Glassmorphism, Claymorphism
- **Visual Configurator** - Point-and-click styling in the playground
- **TypeScript Native** - Full type safety and IntelliSense
- **Accessible** - Keyboard navigation and screen reader support

---

## Contributors

| Contributor | Role |
|-------------|------|
| [@G-Hensley](https://github.com/G-Hensley) | Creator & Maintainer |

---

## License

This project is licensed under the [MIT License](LICENSE).
