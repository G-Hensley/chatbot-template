# Chatbot Template - MVP Roadmap

## Project Overview

A provider-agnostic, reusable chatbot component system with two delivery methods:
1. **pnpm package** - Drop into any React project
2. **Playground webapp** - Test configurations and preview UI styles

**Default Model:** Claude 3.5 Haiku (configurable)
**Tech Stack:** React, TypeScript, Tailwind CSS, GraphQL, Vercel AI SDK

---

## Phase 1: Core Foundation

### 1.1 Project Setup
- [✅] Initialize monorepo structure (pnpm workspaces)
  - `/packages/chatbot-core` - The reusable component library
  - `/apps/playground` - The standalone webapp
- [ ] Configure TypeScript, ESLint, Prettier
- [ ] Set up Vitest for testing
- [ ] Create basic README with project vision

### 1.2 Basic Chat UI Component
- [ ] Build `<ChatWindow />` component with message list
- [ ] Build `<ChatInput />` component with send button
- [ ] Build `<ChatMessage />` component (user vs assistant styling)
- [ ] Build `<ChatBubble />` wrapper component
- [ ] Implement basic Tailwind styling (clean default look)
- [ ] Add loading/typing indicator component

### 1.3 State Management
- [ ] Create chat context/store for message history
- [ ] Implement localStorage persistence
- [ ] Add clear conversation functionality
- [ ] Handle message timestamps

---

## Phase 2: AI Integration & Streaming

### 2.1 Vercel AI SDK Integration
- [ ] Install and configure `ai` package
- [ ] Create streaming hook (`useChat` or custom)
- [ ] Implement token-by-token rendering
- [ ] Handle stream errors gracefully
- [ ] Add abort/cancel streaming functionality

### 2.2 GraphQL API Layer
- [ ] Set up Apollo Server in playground app
- [ ] Define schema:
  ```graphql
  type Message {
    id: ID!
    role: String!
    content: String!
    timestamp: DateTime!
  }

  type ChatResponse {
    message: Message!
    stream: Boolean!
  }

  type Mutation {
    sendMessage(content: String!, config: ChatConfigInput): ChatResponse!
  }

  input ChatConfigInput {
    provider: String
    model: String
    systemPrompt: String
    temperature: Float
    maxTokens: Int
  }
  ```
- [ ] Implement streaming over GraphQL (subscriptions or SSE)
- [ ] Create provider abstraction layer
- [ ] Add Anthropic provider (Claude 3.5 Haiku default)
- [ ] Document how to add other providers (OpenAI, etc.)

### 2.3 Configuration System
- [ ] Create `chatbot.config.ts` schema
- [ ] Support environment variables for API keys
- [ ] Create `SYSTEM_PROMPT.md` file convention
- [ ] Build config validation with Zod
- [ ] Document all configuration options

---

## Phase 3: UI Configurator

### 3.1 Style System Architecture
- [ ] Create CSS variable system for theming
- [ ] Build style presets structure:
  ```typescript
  interface StylePreset {
    name: string;
    shadows: ShadowConfig;
    borders: BorderConfig;
    colors: ColorConfig;
    effects: EffectConfig;
  }
  ```

### 3.2 Visual Style Options
- [ ] **Morphism Styles:**
  - [ ] Flat (default/minimal)
  - [ ] Neumorphism (soft shadows, embossed look)
  - [ ] Glassmorphism (blur, transparency)
  - [ ] Claymorphism (soft, rounded, 3D-ish)
- [ ] **Corner Radius Slider:** 0px → 24px
- [ ] **Shadow Controls:**
  - [ ] Shadow intensity slider
  - [ ] Shadow color picker
  - [ ] Inner vs outer shadow toggle
- [ ] **Spacing Controls:**
  - [ ] Message padding
  - [ ] Gap between messages

### 3.3 Color Scheme System
- [ ] Build color palette generator
- [ ] Create color picker for:
  - [ ] Primary color (user messages)
  - [ ] Secondary color (assistant messages)
  - [ ] Background color
  - [ ] Text colors (primary, secondary, muted)
  - [ ] Accent color (send button, links)
- [ ] Add preset color schemes (light, dark, custom)
- [ ] Support dark mode toggle

### 3.4 Playground Configurator UI
- [ ] Build sidebar with all style controls
- [ ] Live preview panel
- [ ] Export configuration button (generates config file)
- [ ] Import configuration from file
- [ ] Reset to defaults button

---

## Phase 4: Package & Documentation

### 4.1 NPM/PNPM Package
- [ ] Configure package.json for publishing
- [ ] Set up build pipeline (tsup or similar)
- [ ] Generate TypeScript declarations
- [ ] Create package exports:
  ```typescript
  // Main components
  export { ChatBot } from './components/ChatBot';
  export { ChatWindow, ChatInput, ChatMessage } from './components/';

  // Hooks
  export { useChat, useChatConfig } from './hooks';

  // Types
  export type { ChatConfig, Message, StylePreset } from './types';

  // Utilities
  export { createChatConfig, applyStylePreset } from './utils';
  ```
- [ ] Test installation in fresh project

### 4.2 Documentation
- [ ] **README.md** - Quick start, installation, basic usage
- [ ] **CONFIGURATION.md** - All config options explained
- [ ] **SYSTEM_PROMPT_GUIDE.md** - How to write effective system prompts
- [ ] **STYLING.md** - Customization guide with examples
- [ ] **API.md** - GraphQL schema reference
- [ ] **PROVIDERS.md** - How to use different AI providers

### 4.3 LLM Prompt Templates
- [ ] Create `/prompts/setup-assistant.md` - Prompt users can give to ChatGPT/Claude to help configure their chatbot
- [ ] Create `/prompts/system-prompt-generator.md` - Prompt to help users write their SYSTEM_PROMPT.md
- [ ] Create `/prompts/troubleshooting.md` - Prompt for debugging issues

---

## Phase 5: Polish & Release

### 5.1 Testing
- [ ] Unit tests for all components
- [ ] Integration tests for chat flow
- [ ] Test with multiple AI providers
- [ ] Test style configurator outputs
- [ ] Accessibility audit (keyboard nav, screen readers)

### 5.2 Playground Deployment
- [ ] Deploy playground to Vercel
- [ ] Set up demo with limited API access
- [ ] Add example configurations gallery

### 5.3 Release
- [ ] Publish to npm (`@codaissance/chatbot` or similar)
- [ ] Create GitHub release with changelog
- [ ] Announce on LinkedIn (content pillar opportunity!)

---

## File Structure (Target)

```
chatbot-template/
├── packages/
│   └── chatbot-core/
│       ├── src/
│       │   ├── components/
│       │   │   ├── ChatBot.tsx          # Main wrapper component
│       │   │   ├── ChatWindow.tsx       # Message container
│       │   │   ├── ChatInput.tsx        # Input field + send
│       │   │   ├── ChatMessage.tsx      # Individual message
│       │   │   └── TypingIndicator.tsx
│       │   ├── hooks/
│       │   │   ├── useChat.ts           # Main chat hook
│       │   │   ├── useChatConfig.ts     # Config context hook
│       │   │   └── useStreaming.ts      # Streaming logic
│       │   ├── styles/
│       │   │   ├── presets/
│       │   │   │   ├── flat.ts
│       │   │   │   ├── neumorphism.ts
│       │   │   │   ├── glassmorphism.ts
│       │   │   │   └── claymorphism.ts
│       │   │   └── variables.css
│       │   ├── providers/
│       │   │   ├── anthropic.ts
│       │   │   └── base.ts              # Provider interface
│       │   ├── types/
│       │   │   └── index.ts
│       │   └── index.ts                 # Package exports
│       ├── package.json
│       └── tsconfig.json
├── apps/
│   └── playground/
│       ├── src/
│       │   ├── app/
│       │   │   ├── api/
│       │   │   │   └── graphql/         # GraphQL endpoint
│       │   │   ├── page.tsx             # Main playground
│       │   │   └── layout.tsx
│       │   ├── components/
│       │   │   ├── Configurator.tsx     # Style controls sidebar
│       │   │   ├── Preview.tsx          # Live chat preview
│       │   │   └── ExportModal.tsx
│       │   └── graphql/
│       │       ├── schema.ts
│       │       └── resolvers.ts
│       ├── package.json
│       └── next.config.js
├── docs/
│   ├── README.md
│   ├── CONFIGURATION.md
│   ├── SYSTEM_PROMPT_GUIDE.md
│   ├── STYLING.md
│   └── PROVIDERS.md
├── prompts/
│   ├── setup-assistant.md
│   ├── system-prompt-generator.md
│   └── troubleshooting.md
├── templates/
│   ├── SYSTEM_PROMPT.md                 # Template users copy
│   └── chatbot.config.example.ts
├── pnpm-workspace.yaml
├── package.json
└── README.md
```

---

## Learning Checkpoints

As you build, you'll gain hands-on experience with:

| Phase | Skills Learned |
|-------|----------------|
| Phase 1 | React component architecture, TypeScript, pnpm monorepos |
| Phase 2 | **GraphQL** (Apollo Server, schemas, resolvers), **Vercel AI SDK**, **Streaming (SSE)** |
| Phase 3 | CSS variables, Tailwind theming, UI/UX for configurators |
| Phase 4 | npm package publishing, technical documentation |
| Phase 5 | Testing strategies, deployment, release management |

---

## Success Criteria (MVP)

- [ ] Can install package via `pnpm add @codaissance/chatbot`
- [ ] Can render a working chatbot with `<ChatBot config={...} />`
- [ ] Streaming responses work with Claude 3.5 Haiku
- [ ] Can customize appearance via style presets or config
- [ ] Playground allows visual configuration and exports config
- [ ] Clear documentation for setup and customization
- [ ] System prompt is a simple file edit

---

## Future Enhancements (Post-MVP)

- Voice input/output
- Image/file uploads
- Multi-turn context window management
- Conversation branching
- Analytics/usage tracking
- More AI providers (OpenAI, Groq, Ollama)
- Widget embed mode (iframe/web component)
- TemperedUI integration for secure inputs

---

*Last Updated: February 4, 2026*
