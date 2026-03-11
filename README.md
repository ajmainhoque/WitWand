# WitWand

A competitive coding battle game where two players solve programming challenges in real-time to power up their wizards and cast spells. Built for [Hopper Hacks 2026](https://hopperhacks.org/).

**Play now at [witwand.xyz](https://witwand.xyz/)**

![WitWand Title Screen](public/title.png)

## How It Works

1. **Choose your language** — JavaScript, Python, C, C++, or Java
2. **Pick your wizards** — Each player selects 2 characters from 6 unique wizards
3. **Solve coding problems** — Both players race to solve algorithmic challenges simultaneously
4. **Cast spells in combat** — Correct solutions award mana to fuel your spells and abilities
5. **Win the duel** — Defeat your opponent's characters to claim victory

## Features

- **Turn-based RPG combat** with coding puzzles as the core mechanic
- **6 playable characters** — Harry, Hermione, Ron, Voldemort, Hagrid, and Bellatrix — each with unique spells and items
- **5 supported languages** — JavaScript, Python, C, C++, Java
- **Real-time code execution** — JavaScript runs in Web Workers, Python via Pyodide WASM, and C/C++/Java via the Piston API
- **Status effects** — Poison, Bleed, Stun, Shield, Dodge, and more
- **Retro pixel-art UI** with animations and sound effects
- **AI-powered debugging** — "Why?" button explains errors using LLM

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 19, TypeScript, Vite |
| Code Editor | CodeMirror (via @uiw/react-codemirror) |
| Code Execution | Web Workers, Pyodide WASM, Piston API |
| Backend | Express (API proxying + static serving) |
| LLM Fallback | Snowflake Cortex (Llama 3.1-405B) |
| Styling | CSS with pixel-art theme, Press Start 2P font |

## Getting Started

### Prerequisites

- Node.js (v18+)
- npm

### Installation

```bash
git clone https://github.com/ajmainhoque/hopper-hacks-2026.git
cd hopper-hacks-2026
npm install
```

### Development

```bash
npm run dev
```

Starts the Vite dev server with hot module replacement.

### Production Build

```bash
npm run build
npm start
```

Builds the app and starts the Express server on port `8080` (or `$PORT`).

### Environment Variables

Create a `.env` file in the project root:

```env
# Piston API for C/C++/Java code execution
PISTON_URL=<your-piston-instance-url>

# Snowflake Cortex for LLM fallback
VITE_SNOWFLAKE_ACCOUNT_URL=<your-snowflake-account-url>
VITE_SNOWFLAKE_PAT=<your-snowflake-pat>
VITE_SNOWFLAKE_MODEL=llama3.1-405b
```

> JavaScript and Python execution works in-browser without any environment variables. The Piston API and Snowflake Cortex are only needed for C/C++/Java execution and the AI debugging feature.

## Project Structure

```
src/
├── screens/        # Title, Character Select, Battle, Victory screens
├── components/     # UI components (BattleField, CodingEditor, ActionPanel, etc.)
├── engine/         # Game logic (combat, turns, characters, status effects)
├── coding/         # Code execution (runners, problem cache, test validation)
├── hooks/          # React hooks (game state, coding phase, timer)
├── audio/          # Background music and sound effects
├── styles/         # CSS theme, pixel-art styles, animations
└── assets/         # Character sprites and visual effects
```

## Game Flow

```
Title Screen → Character Select → Battle Loop → Victory Screen
                                      ↓
                              ┌───────────────┐
                              │ Coding Phase   │ ← Both players solve problems
                              │ (120-180s)     │
                              └───────┬───────┘
                                      ↓
                              ┌───────────────┐
                              │ Action Phase   │ ← Characters cast spells/use items
                              │ (30s per turn) │
                              └───────┬───────┘
                                      ↓
                                 Loop until
                               a team falls
```

## License

This project was built for Hopper Hacks 2026.
