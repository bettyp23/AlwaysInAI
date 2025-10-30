# AlwaysInAI

AlwaysInAI is a next‑generation social media + intelligent assistant app for mobile. It functions like Siri, but instead of simple voice commands, it performs autonomous agent tasks: scheduling, sending messages, generating posts, summarizing articles, managing reminders, and interacting with AI agents for personal and professional productivity.

## Key Features

- Real‑time speech recognition (always‑listening mode with wake phrase)
- AI agent orchestration (task automation via tools)
- Social sharing (share AI‑generated actions)
- Cloud storage for command history and analytics
- Cross‑platform mobile app (React Native / Expo)
- Privacy‑safe voice activation and opt‑in listening

## Goals

- Build a fully functional prototype
- Integrate real‑time voice recognition and command parsing
- Connect with agent APIs (OpenAI Assistants primary, custom LLM optional)
- Provide dashboard for activity history, feedback, and social feed
- Maintain high standards of security, privacy, and data management
- Optimize UX for continuous passive AI interaction

## Tech Stack

- Frontend: React Native (Expo)
- Voice: iOS Speech Framework / SiriKit; Android SpeechRecognizer / Google ASR
- AI: OpenAI Assistants API (primary) / Custom LLM backend (optional)
- Database: SQLite (local cache) + Firebase Cloud Firestore
- Authentication: OAuth / Firebase Auth
- Deployment: Android Studio & Xcode
- Optional: Supabase social graph, Google Cloud STT for accuracy

## Architecture Overview

- Voice Listener: continuous mic input with wake‑word detection (e.g., "Hey Always")
- Agent Processor: interprets commands, connects to AI models
- Task Executor: runs actions (calendar, messaging, summarization, content)
- Social Feed: shows recent AI actions, shares, and trends
- Privacy Manager: permissions, consent, opt‑in/out of always‑on mode
- Cloud Sync: secure history, analytics; local cache for offline (SQLite)

## Repository Structure (planned)

- `src/components/` – UI components and related logic
- `src/agents/` – agent command processing, config
- `src/screens/` – Home, Feed, Settings, Voice Command
- `src/services/` – API clients (OpenAI, custom LLM, Firebase)
- `assets/` – icons, sounds
- `PROMPTS.md` – consolidated system prompts (role, tools, safety)

## Setup

### Prerequisites

- Node.js LTS, pnpm/yarn/npm
- Expo CLI (`npm i -g expo`)
- Android Studio (Android SDK, emulator); Xcode (iOS Simulator)
- Firebase project (Firestore + Auth) if using social features

### Environment Variables

Create a `.env` (or use your config system) with:

- `OPENAI_API_KEY` – for OpenAI Assistants (primary backend)
- `CUSTOM_LLM_BASE_URL` – base URL of optional custom LLM backend
- `CUSTOM_LLM_API_KEY` – API key/token for custom LLM
- `FIREBASE_API_KEY`, `FIREBASE_AUTH_DOMAIN`, `FIREBASE_PROJECT_ID`, etc.

### Platform Permissions & Entitlements

iOS (Info.plist):

- `NSSpeechRecognitionUsageDescription`
- `NSMicrophoneUsageDescription`
- Background audio mode if streaming in background

Android (AndroidManifest.xml):

- `RECORD_AUDIO`
- `INTERNET`
- Foreground service / mic usage indicators as required by SDK level

### Install & Run

```
# install deps (example)
pnpm install  # or yarn install / npm install

# start
npx expo start
```

Open in iOS Simulator or Android Emulator from the Expo Dev Tools.

## AI Backend Configuration

OpenAI (primary):

- Set `OPENAI_API_KEY`.
- Use model `gpt-4o-mini` (recommended) or another Assistants‑compatible model.
- Load instructions from `PROMPTS.md` sections.

Custom LLM (optional fallback):

- Set `CUSTOM_LLM_BASE_URL` and `CUSTOM_LLM_API_KEY`.
- Provide model name in config and point to the same prompts.

See `src/agents/assistant-config.example.json` for a reference configuration.

## JSON Command Schema (example)

When actionable, the assistant should emit a single JSON command:

```
{
  "intent": "schedule_event",
  "parameters": { "title": "Meeting with team", "time": "2025-11-01T10:00:00-05:00", "duration_min": 60, "attendees": ["team@example.com"] }
}
```

Additional example intents: `send_message`, `summarize_url`, `generate_post`, `create_reminder`, `share_social` (see PROMPTS.md for more examples).

## Privacy & Security

- Explicit opt‑in for always‑on listening
- Microphone indicators when active; easy toggle to pause
- Encrypted storage for voice and command history
- Minimal retention; PII redaction in logs unless user opts in

See `privacy_policy.md` (to be added) for the full policy.

## Roadmap (aligned to project steps)

1. Define core architecture (modular RN/Expo)
2. Implement voice recognition and wake phrase
3. Build agent command system (OpenAI/custom)
4. Design UI/UX (Home, Voice, Feed, Settings)
5. Social integration (share, follow, like/comment) via Firebase/Supabase
6. Privacy & security (consent flows, indicators, dashboard)
7. Deliverables (demo, docs, diagrams, example logs)
8. Quality & evaluation (latency, accuracy, UX polish)

## Deliverables Checklist

- [x] README (this file)
- [ ] PROMPTS.md (system prompts)
- [ ] `src/agents/assistant-config.example.json`
- [ ] Privacy documentation and consent flow screenshots
- [ ] System architecture diagram
- [ ] Example JSON task logs

## License

TBD