# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.
コードコメント、readmeは日本語で書くこと。

## Project Overview

This is a Next.js TypeScript application demonstrating advanced voice agent patterns using the OpenAI Realtime API and OpenAI Agents SDK. The app showcases two main architectural patterns:

1. **Chat-Supervisor Pattern**: A realtime chat agent handles basic interactions while deferring complex tasks to a text-based supervisor model (gpt-4.1)
2. **Sequential Handoff Pattern**: Specialized agents transfer users between them to handle specific intents (inspired by OpenAI Swarm)

## Development Commands

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Start production server
npm start

# Run linting
npm run lint
```

## Environment Setup

- Copy `.env.sample` to `.env` and add your `OPENAI_API_KEY`
- Or add `OPENAI_API_KEY` to your shell environment

## Architecture Overview

### Core Application Structure

- **`src/app/App.tsx`**: Main application component managing session state, agent selection, and UI
- **`src/app/page.tsx`**: Next.js page wrapper with context providers (TranscriptProvider, EventProvider)
- **`src/app/hooks/useRealtimeSession.ts`**: Core hook managing WebRTC connection and session lifecycle

### Agent Configuration System

- **`src/app/agentConfigs/index.ts`**: Central registry mapping scenario keys to agent arrays
- **Agent Scenarios**:
  - `chatSupervisor/`: Chat-supervisor pattern implementation
  - `customerServiceRetail/`: Complex customer service flow with authentication, returns, sales
  - `simpleHandoff/`: Basic handoff demonstration between greeter and haiku writer

### Key Components

- **`BottomToolbar.tsx`**: Connection controls, PTT toggle, codec selection
- **`Transcript.tsx`**: Chat interface with message history and guardrail indicators
- **`Events.tsx`**: Real-time event log showing client/server communications

### Context & State Management

- **`TranscriptContext`**: Manages conversation history and message state
- **`EventContext`**: Handles logging of client/server events for debugging
- **Session Management**: Handles WebRTC connection, audio streaming, and agent handoffs

## Agent Development Patterns

### Adding New Agent Scenarios

1. Create new directory in `src/app/agentConfigs/`
2. Define agents using `RealtimeAgent` from `@openai/agents/realtime`
3. Configure handoffs by setting `handoffs` array on each agent
4. Add scenario to `allAgentSets` in `src/app/agentConfigs/index.ts`

### Agent Configuration Structure

```typescript
import { RealtimeAgent } from '@openai/agents/realtime';

export const exampleAgent = new RealtimeAgent({
  name: 'agentName',
  handoffDescription: 'Description for handoff context',
  instructions: 'Detailed agent instructions...',
  tools: [], // Tool definitions
  handoffs: [otherAgent], // Agents this can hand off to
});
```

### Tool Implementation

- Tools are defined with JSON schema in agent configurations
- Tool logic is implemented in corresponding files (e.g., `authentication.ts`, `returns.ts`)
- Default tool calls return `True` unless custom `toolLogic` is defined

## Key Technical Details

### Audio & WebRTC

- Codec selection support (Opus 48kHz vs PCMU/PCMA 8kHz) via URL parameter `?codec=`
- Audio streaming handled by `@openai/agents/realtime` SDK
- PTT (Push-to-Talk) mode toggles server VAD on/off

### Session Management

- Ephemeral keys fetched from `/api/session` endpoint
- WebRTC connection established through `OpenAIRealtimeWebRTC` transport
- Agent handoffs trigger session updates without reconnection

### Guardrails

- Output moderation implemented via `createModerationGuardrail()`
- Messages marked as IN_PROGRESS, PASS, or FAIL based on guardrail results
- Guardrail events handled in transcript display

### URL-based Configuration

- Agent scenario selected via `?agentConfig=` parameter
- Specific agent selection via agent dropdown (triggers reconnection)
- Codec preference via `?codec=` parameter

## Testing Scenarios

- **Chat Supervisor**: Ask complex questions that require tool calls (billing, account info)
- **Customer Service**: Request returns, authenticate with fake credentials
- **Simple Handoff**: Ask for haikus to trigger agent transfer

## Dependencies

- `@openai/agents`: Core agents SDK for realtime interactions
- `next`: React framework
- `openai`: OpenAI API client
- `react-markdown`: Markdown rendering in transcript
- `uuid`: ID generation for messages
- `zod`: Schema validation