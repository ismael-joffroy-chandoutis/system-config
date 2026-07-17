**English** · [Français](README.fr.md)

# System Configuration — Filmmaker + AI Workflow

> MacBook Air M3 — 16 GB RAM — 500 GB SSD — macOS 26.3 (Tahoe)
> Last updated: 2026-07-17

A filmmaker and digital artist running Claude Code as the primary intelligence layer across multiple machines. This documents the full stack: hardware, software, AI agents, automation, and creative production tools.

---

## 1. Hardware

### Primary Machine
| Spec | Value |
|------|-------|
| Model | MacBook Air M3 |
| Chip | Apple M3 |
| RAM | 16 GB |
| SSD | 500 GB (APFS) |
| macOS | 26.3 (Tahoe) |

### Multi-Machine Setup (Tailscale)
| Machine | Role |
|---------|------|
| MacBook Air M3 | Primary (portable) |
| Mac Mini M4 | Server (Paris) — always-on, tmux sessions |
| PC Windows | GPU compute (RTX 5090), DaVinci Resolve |

Connected via Tailscale VPN. SSH + mosh for remote sessions. AnyDesk/Jump Desktop/Parsec for GUI access.

### Storage
| Volume | Size | Purpose |
|--------|------|---------|
| NavTGV1 | 15 TB | Film rushes (primary) |
| NavTGV2 | 15 TB | Film rushes (mirror) |
| 4T_IJC_th4 | 3.6 TB | Archive |
| lexar2_2TB | 1.9 TB | Working SSD |
| Camera cards (A009, A010) | ~1 TB | Active shoot media |
| Zoom SD | 119 GB | Audio recordings |
| UGREEN NAS | — | Network backup |
| Cloudflare R2 | — | Cloud rushes backup (~50 MiB/s) |

---

## 2. Development Environment

### Runtimes
| Runtime | Version | Manager |
|---------|---------|---------|
| Node.js | 20.20.0 (default), 22.22.1 | mise |
| Python | 3.10 (default), 3.12, 3.13, 3.14 | mise + Homebrew |
| Ruby | 3.3.6 | mise |
| Go | latest | Homebrew |
| Deno | latest | Homebrew |
| Bun | latest | Homebrew |

### Shell
- **zsh** with custom aliases for Claude Code workflows
- **Ghostty** terminal (primary), iTerm2 (secondary)
- **tmux** with resurrect plugin, custom layouts for multi-agent sessions

### Git
- GitHub CLI (`gh`) for auth and PR workflows
- Git LFS enabled
- Global gitignore configured

---

## 3. Claude Code — The Intelligence Layer

### Configuration
- **Version**: 2.1.81 (latest)
- **Model**: Claude Opus 4.6 (1M context)
- **Thinking**: Always on
- **Effort**: High
- **Agent Teams**: Enabled (experimental)

### Hooks (Event-Driven Automation)
| Event | Action |
|-------|--------|
| UserPromptSubmit | Tab title update, context alerts, session backup |
| SessionStart | Terminal tab title |
| Stop | Notification (sound + Telegram push) |
| SubagentStop | Subagent completion notification |
| Notification | Attention alert |
| PostToolUse (Edit/Write) | Language consistency check |

### Security Denials
Hardcoded denials for dangerous operations: `mkfs`, `dd`, force-push, SSH key reading, keychain access.

### Plugins (39 active)
Categories: development (superpowers, code-review, commit-commands, github, feature-dev), design (frontend-design, figma), AI (agent-sdk-dev, huggingface-skills), observability (sentry, vercel), productivity (Notion, slack, linear, stripe), and more.

### MCP Servers (13 configured)
| Server | Purpose |
|--------|---------|
| Gmail (custom) | Email management |
| Telegram | Messaging |
| Slack (binary) | Team communication |
| Spotify | Music control |
| Instagram DMs | Social messaging |
| Apple Shortcuts | macOS automation |
| AppleScript | macOS scripting |
| Krea | AI image generation |
| DoorDash | Delivery ordering |
| Postiz | Social media scheduling |
| FCP XML | Final Cut Pro integration |
| DaVinci Resolve (x2) | Color grading / editing |
| DataGouv | French open data |

### Skills (108 installed)
Organized in `~/.agents/skills/`, shared between Claude Code and Cursor. Includes: design suite (18 skills), creative writing suite, Vercel/Next.js suite, SEO suite, cinema/screenplay analysis tools, and custom filmmaker tools.

---

## 4. Automated Agents (LaunchAgents)

### Daily Intelligence
| Agent | Schedule | Purpose |
|-------|----------|---------|
| Morning Brief | AM | Daily briefing (Gmail, Calendar, Discord, GitHub) |
| Afternoon Check | PM | Status check-in |
| Deadline Scanner | Daily | Scan for approaching deadlines |
| Mentions Monitor | Periodic | Track mentions across platforms |

### Accounting (ComptaOS)
| Agent | Purpose |
|-------|---------|
| Compta Scan | Receipt scanning |
| Compta Missing | Missing receipt alerts |
| Compta Report | Financial reporting |
| Compta Subscriptions | Subscription tracking |

### Content & Research
| Agent | Purpose |
|-------|---------|
| Tech Watch | Technology news monitoring |
| Art Watch | Art world monitoring |
| GitHub Stars Digest | Weekly new stars analysis |
| X/Twitter Digest | Social media digest |
| LLM Visibility | AI industry monitoring |

### System
| Agent | Purpose |
|-------|---------|
| Heartbeat | Agent health monitoring |
| Telegram Bridge | Telegram bot for notifications |
| WhatsApp Bridge | WhatsApp integration |
| CC Changelog Monitor | Claude Code update checker |
| Claude Desktop Backup | Hourly config backup |
| Skills Watcher | Skills update detection |
| Failover Watchdog | System failover monitoring |
| Voice Memo Processor | Auto-transcribe voice memos |

### Data Sync
| Agent | Purpose |
|-------|---------|
| DataGouv Sync | French open data (daily/weekly/monthly) |
| Music Sync | Music library sync |

---

## 5. Applications

### Creative / Film Production
| Category | Apps |
|----------|------|
| Editing | Adobe Premiere Pro 2025, DaVinci Resolve, Recut |
| Color/Compositing | DaVinci Resolve, Adobe Photoshop 2025 |
| Motion/VFX | Adobe After Effects, Compressor |
| Audio | MacWhisper, Descript, Soundly, Remixlive, VoiceInk |
| Encoding | Shutter Encoder, Adobe Media Encoder 2025 |
| Media Management | Kyno, FCPX Cut Finder, CommandPost, MediaInfo |
| Design | Figma, Pixelmator Pro, Adobe InDesign 2025 |
| Capture | ScreenFlow, 4K Video Downloader+ |
| AI Generation | Mochi Diffusion, LTX Desktop, ntsc-rs |
| Subtitles | Captionator |

### AI Tools
| App | Purpose |
|-----|---------|
| Claude (Desktop) | Primary AI assistant |
| Claude Code (CLI) | Development + OS layer |
| ChatGPT | Alternative AI |
| Perplexity | Research |
| Codex | OpenAI agent |
| VoiceInk | Voice-to-text |
| MacWhisper | Audio transcription |

### Communication
Beeper Desktop, Discord, Telegram, WhatsApp, Zoom

### Development
Ghostty, iTerm, cmux, Xcode, BBEdit, CotEditor, Obsidian, CodexBar, breadboard

### Browsers
Google Chrome, Brave Browser, Safari

### Utilities
Bitwarden, CleanMyMac 5, Carbon Copy Cloner, Keka, Magnet, boringNotch, PDF Squeezer, Tailscale, NordVPN, OrbStack, VLC, Toggl Track, Karabiner-Elements

---

## 6. Key Packages

### Global npm
| Package | Purpose |
|---------|---------|
| `@anthropic-ai/claude-code` | Claude Code CLI |
| `@google/gemini-cli` | Gemini CLI |
| `@openai/codex` | OpenAI Codex |
| `vercel` | Vercel CLI |
| `n8n` | Workflow automation |
| `dmux` | tmux multiplexer |
| `obsidian-cli` | Obsidian CLI |

### Homebrew (Key)
**CLI**: gh, git, lazygit, tmux, yazi, glow, watch, rclone, rsync, mosh
**Media**: ffmpeg, yt-dlp, whisper-cpp, tesseract, mupdf-tools, poppler
**Data**: mongodb-community, mongosh, sqlite
**Network**: cloudflared, wireguard-tools, tailscale
**AI**: recall (conversation search), pinecone, mirroir-mcp

### Python (Key)
**AI/ML**: torch 2.8, transformers, diffusers, accelerate, huggingface-hub, anthropic, google-genai, datasets, pytorch-lightning
**Audio**: faster-whisper, whisperx, speechbrain, pyannote.audio, DeepFilterNet, librosa
**Video**: opencv-python, scenedetect, ffmpeg-python
**Web**: fastapi, playwright, httpx, fastmcp, mcp
**Data**: pandas, numpy, scipy, duckdb, openpyxl
**Apple**: pyobjc, osxphotos, pymobiledevice3
**Creative**: manim (animation), pillow, reportlab

---

## 7. Project Structure

### Film Projects
| Project | Description |
|---------|-------------|
| The Goldberg Variations | Feature documentary (Villa Albertine 2026) |
| Virus | Film on Mihai Ionut Paunescu |
| Moon Metropolis | — |
| Rewild | — |

### Dev Projects (Active)
| Project | Description |
|---------|-------------|
| Custom MCP Servers | Gmail, Telegram, Slack, Spotify, Instagram, Krea, DoorDash, FCP, Resolve |
| Heartbeat Agent | Persistent daemon agent |
| LLM Council | Multi-LLM debate system |
| Life Intelligence | Personal intelligence system ("Vaisseau Amiral") |
| Spectre | Claude Code as OS concept |
| Vibe Ribbon | Dashboard web for Claude Code |
| Agent Viewer | Kanban view of tmux agents |
| Claude Code Workflow | Public documentation of CC workflow |

### Film/AI Research
| Project | Description |
|---------|-------------|
| AI Cinema Research | Public research on AI in cinema |
| Filmmaker AI Brain | AI-augmented filmmaker system |
| Film Production Intelligence | Production management tools |
| StoryCurve | Non-linear narrative visualization (D3.js) |
| StoryExplorer | Story exploration tool |
| Buttercut | Video processing tool (Ruby) |
| OBLITERATUS | Art project |

### Narrative Tools
| Tool | Stack | Purpose |
|------|-------|---------|
| storycurve | D3.js | Non-linear narrative visualization |
| storyexplorer | — | Story exploration |
| mcp-server-tmdb | TypeScript | TMDB API for film data |
| cc-wf-studio | VSCode ext | Claude Code workflow studio |

---

## 8. Obsidian Second Brain

- 3093+ markdown files
- iCloud synced
- MCP server integration (port 27124)
- Structure: numbered folders (00-09)
- Voice memo pipeline: auto-transcribe → route to Obsidian

---

## 9. Philosophy

**Claude Code as OS**: Not a dev tool. An intelligence layer that unifies and drives the entire computing system across machines and operating systems. One intelligence, one memory, one continuity of action.

**Concept name**: Spectre — "the ghost above the shell"

**Workflow**: Specs-driven development (`/interview` before coding), creative specs (`/pitch` before production), liquid writing methodology for screenwriting.

---

## 10. Metrics (2026-03-24 Snapshot)

| Metric | Value |
|--------|-------|
| Running processes | ~930 |
| Claude Code sessions | 8 parallel |
| MCP servers per session | ~25 |
| LaunchAgents | 42 |
| Installed skills | 108 |
| Installed plugins | 39 |
| External storage | ~40 TB connected |
| Python packages | ~350 |
| Homebrew formulae | ~130 |
| Applications | ~110 |

By [Ismaël Joffroy Chandoutis](https://ismaeljoffroychandoutis.com).
