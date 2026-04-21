# ◼ HURAIRA TASK MANAGER
**Night Grind Mode** — A desktop productivity app for late-night focus sessions.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Version](https://img.shields.io/badge/version-1.0.0-green.svg)
![Platform](https://img.shields.io/badge/platform-Windows-blue.svg)

---

## Overview

Huraira Task Manager is a **local-first, privacy-focused** desktop application designed for night-shift workers (10 PM – 1 AM). It combines voice input, smart timers, alarms, and a password-protected goals section into one intuitive tool.

**Key Features:**
- 🎙 **Voice-first task input** — Speak tasks naturally, auto-parse duration & category
- ⏱️ **Smart countdown timer** — Color-coded progress (cyan → orange → red)
- 🔔 **Alarms & warnings** — 5-minute pre-alert + loud alarm on expiry
- 📅 **Daily schedule timeline** — Visualize your entire night (10 PM – 2 AM)
- 🔒 **Password-protected goals** — Store dreams, milestones, private notes securely
- 💾 **100% local storage** — No cloud, no tracking, all data on your PC
- ⌨️ **Keyboard shortcuts** — Ctrl+N (add task), Ctrl+1-4 (nav pages)

---

## Screenshots

*Dashboard with active timer and timeline:*
```
Tonight's Tasks | Sunday, Apr 19 | Night Mode
┌─────────────────────────────────────────┐
│ ▶ IN PROGRESS: Watch 2 lectures (45m)   │
│ ████████████░░░░░░░░ 62% elapsed        │
│ [✓ Done] [+5 Min] [⏸ Pause] [Skip]      │
├─────────────────────────────────────────┤
│ 📅 Tonight's Schedule (10 PM – 2 AM)    │
│ [Lectures Block] [LinkedIn Block] [...]  │
├─────────────────────────────────────────┤
│ UPCOMING (2)  COMPLETED (1)              │
└─────────────────────────────────────────┘
```

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| **Desktop** | Electron 29 |
| **UI** | React + TypeScript (vanilla JS in v1) |
| **Storage** | JSON files (local) |
| **Voice** | Web Speech API |
| **Encryption** | Custom XOR-based obfuscation |
| **Build** | electron-builder |

---

## Installation

### From Installer (.exe)
1. Download `Huraira Task Manager Setup 1.0.0.exe` from [Releases](https://github.com/YOUR_USERNAME/huraira-task-manager/releases)
2. Double-click to install
3. Launch from Start Menu

### From Source
```bash
# Clone repository
git clone https://github.com/YOUR_USERNAME/huraira-task-manager.git
cd huraira-task-manager

# Install dependencies
npm install

# Start in dev mode
npm start

# Build Windows installer
npm run build:win
```

---

## Quick Start

### 1. First Launch
- Open the app
- Go to **Settings → Security → Set Password** for Hidden Goals
- Password is encrypted locally (never stored as plain text)

### 2. Add Your First Task
**Option A — Manual:**
- Click **+ Add Task**
- Fill title, duration (min), category, priority
- Click **Add Task**

**Option B — Voice:**
- Click **🎙 Voice**
- Speak: *"Watch 2 lectures for 45 minutes"*
- App auto-parses title, duration, category
- Confirm and start

### 3. Run the Timer
- Click **▶** on any task
- Timer counts down (MM:SS format)
- 5-min warning → soft alert
- Time expires → loud alarm modal
- Choose: Done ✓ | +5 Min | Skip

### 4. Explore Features
- **All Tasks** — filter/sort by status, priority, or duration
- **Hidden Goals** — add milestones (Millionaire by 2035, Umrah, etc.)
- **Settings** — customize notifications, work hours, export data

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| Ctrl+N | Add new task |
| Ctrl+1 | Dashboard |
| Ctrl+2 | All Tasks |
| Ctrl+3 | Hidden Goals |
| Ctrl+4 | Settings |
| Escape | Close modal |
| Enter | Confirm/Unlock |

---

## File Structure

```
huraira-task-manager/
├── src/
│   ├── main/
│   │   ├── main.js           # Electron entry point + IPC handlers
│   │   └── preload.js        # Secure API bridge
│   └── renderer/
│       ├── app.js            # Main app controller
│       ├── index.html        # HTML entry
│       ├── styles/main.css   # Dark theme
│       ├── components/       # UI components
│       ├── pages/            # Page logic
│       └── utils/            # Helpers & crypto
├── public/                   # Icons, sounds
├── package.json
├── README.md
└── USER_MANUAL.md           # Full user guide
```

---

## Data Storage

All data is stored locally:
```
Windows: C:\Users\[YOU]\AppData\Roaming\huraira-task-manager\huraira-data\
├── tasks.json      # All your tasks
├── goals.json      # Hidden goals
└── settings.json   # App preferences
```

**Why local-first?**
- ✅ Privacy — your data never leaves your PC
- ✅ Speed — no network latency
- ✅ Offline — works without internet
- ✅ Control — you own your data

---

## Features Deep-Dive

### Voice Input
- Uses native **Web Speech API** (Chrome/Electron)
- Auto-detects duration: *"for 45 minutes"* → 45 min
- Auto-detects category: *"Fiverr"* → Fiverr task
- Fallback to manual input if speech fails

### Timer Logic
- **Color progression:** Cyan (0-70%) → Orange (70-90%) → Red (90-100%)
- **5-min warning:** Soft alert + desktop notification
- **Time expired:** Loud alarm + modal with options (Done / +5 Min / Skip)
- **Pause/Resume:** Freeze timer without losing progress

### Hidden Goals
- **Password-protected:** AES-style encryption (local only)
- **Organize by year:** Group milestones by target year
- **Tags:** #Financial, #Career, #Personal, #Spiritual
- **Private:** Invisible until unlocked with correct password

### Daily Timeline
- **Visual schedule:** 10 PM → 2 AM (night-shift optimized)
- **Block layout:** Each task shown as colored block
- **Live "now" line:** Red marker showing current time
- **Interactive:** Click task block to start immediately

---

## Future Roadmap

- [ ] Urdu language support
- [ ] Collaborative task sharing (encrypted)
- [ ] Mobile companion app (React Native)
- [ ] Advanced analytics (focus trends, productivity heatmap)
- [ ] Custom alarm sounds
- [ ] Recurring task templates
- [ ] Dark/Light theme toggle
- [ ] Pomodoro mode

---

## Development

### Prerequisites
- Node.js 18+
- npm 9+
- Windows 10+ (for build)

### Development Workflow
```bash
# Install
npm install

# Run in dev mode (with DevTools)
npm start -- --dev

# Build for Windows
npm run build:win

# Build for Mac
npm run build:mac

# Build for Linux
npm run build:linux
```

### Code Style
- Vanilla JavaScript (no strict linting in v1, but readable)
- Component-based architecture
- IPC pattern for Electron ↔ Renderer communication
- CSS custom properties for theming

---

## Known Limitations

- 🔧 Voice input requires Chrome/Edge (Chromium-based)
- 📱 Windows-only in v1.0 (Mac/Linux builds available but untested)
- 🎵 Alarm uses Web Audio API (may be silent if system muted)
- 📊 No data sync across devices (by design — local-only)

---

## Contributing

Contributions welcome! Open an issue or PR for:
- Bug fixes
- Performance improvements
- New features (please discuss first)
- Documentation updates
- Translations

---

## License

MIT License — see [LICENSE](LICENSE) file for details.

You are free to use, modify, and redistribute this software.

---

## Support

- **Issues:** [GitHub Issues](https://github.com/YOUR_USERNAME/huraira-task-manager/issues)
- **Questions:** Start a Discussion or email
- **User Manual:** See [USER_MANUAL.md](USER_MANUAL.md)

---

## Acknowledgments

Built with ❤️ for late-night grinders, side-hustlers, and night-shift workers everywhere.

*"The night is long, but your productivity shouldn't be."* 🌙

---

**Made with Electron + React + JavaScript**
