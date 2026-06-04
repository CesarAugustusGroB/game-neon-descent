# Neon Descent: Cyberpunk Roguelike

A dark, abstract cyberpunk dungeon crawler played through a deck of network "node" cards. Hack ever deeper through an infinite network, choosing rooms one card at a time while managing your Integrity (HP), RAM (power), Firewall (shield), Crypto (credits), and a rising Security Alert level. Buy modules, take contracts, fight Black Ice, and survive the digital abyss — with an optional Gemini-powered tactical AI to analyze your next move.

## Features

- Card-driven roguelike loop: each turn you choose one of several network nodes, with a "scout" preview of what the next layer may contain (`components/RoomCard.tsx`).
- Seven room types — Enemy, Elite, Boss, Treasure, Event, Rest, and Merchant — with procedurally chosen names per type (`App.tsx`).
- Security Alert system with DEFCON-style phases (Stealth, Active Sweep, Lockdown, Kill Switch); avoiding combat raises alert and makes enemies deadlier, while fighting lowers it (`components/StatsHeader.tsx`).
- Player progression via stackable Modules (Vampire Kernel, Thorns Protocol, Crypto Miner, Nano-Armor, Overclock, Logic Bomb, Guardian Angel), each altering strategy (`App.tsx`).
- Merchant nodes (Hardware / Software / General) where Crypto is spent on modules or repairs.
- Contract system — Ghost Run, Wetwork, Chaos Bet, Speedrun, Untouchable — with upfront costs, targets, durations, and payouts (`types.ts`).
- Treasure types (Data Cache, Crypto Miner, Dark Contract) and randomized events.
- Dynamic difficulty: boss spawn chance accumulates with depth and alert level.
- Keyboard shortcuts, an in-game help/data panel, and a running game log.
- AI Tactical Analysis: sends the current floor, player stats, and available node choices to Gemini for a deep-reasoning recommendation on which option to pick and why (`services/geminiService.ts`).

## Tech Stack

- React 19 + TypeScript
- Vite 6 (dev server, build, preview)
- `@google/genai` (Gemini) for tactical analysis and event flavor text
- `lucide-react` for icons

## Getting Started

### Prerequisites

- Node.js

### Installation

```bash
npm install
```

### Configure the Gemini API key

This app uses the Gemini API for tactical analysis. Create a `.env.local` file in the project root and set your key:

```bash
GEMINI_API_KEY=your_api_key_here
```

(Vite maps `GEMINI_API_KEY` to `process.env.API_KEY` at build time via `vite.config.ts`.)

### Run

```bash
npm run dev      # start the dev server (http://localhost:3000)
npm run build    # production build
npm run preview  # preview the production build
```

## Project Structure

```
.
├── App.tsx                       # Root component: game state, room generation, modules, contracts
├── index.tsx                     # React entry point
├── components/
│   ├── RoomCard.tsx              # Selectable node cards with scouting preview
│   ├── StatsHeader.tsx           # Player stats, alert phases, installed modules
│   └── GameLog.tsx               # Running event log
├── services/
│   └── geminiService.ts          # Gemini tactical analysis + event generation
├── types.ts                      # Enums and interfaces (RoomType, Module, Contract, PlayerStats, ...)
└── metadata.json
```
