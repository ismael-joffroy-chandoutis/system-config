[English](README.md) · **Français**

# Configuration système — Cinéaste + Workflow IA

> MacBook Air M3 — 16 Go RAM — SSD 500 Go — macOS 26.3 (Tahoe)
> Dernière mise à jour : 2026-07-17

Un cinéaste et artiste numérique faisant tourner Claude Code comme couche d'intelligence principale sur plusieurs machines. Ce document couvre l'ensemble de la stack : matériel, logiciels, agents IA, automatisation et outils de production créative.

---

## 1. Matériel

### Machine principale
| Caractéristique | Valeur |
|------|-------|
| Modèle | MacBook Air M3 |
| Puce | Apple M3 |
| RAM | 16 Go |
| SSD | 500 Go (APFS) |
| macOS | 26.3 (Tahoe) |

### Configuration multi-machines (Tailscale)
| Machine | Rôle |
|---------|------|
| MacBook Air M3 | Principale (portable) |
| Mac Mini M4 | Serveur (Paris) — toujours actif, sessions tmux |
| PC Windows | Calcul GPU (RTX 5090), DaVinci Resolve |

Connectées via VPN Tailscale. SSH + mosh pour les sessions distantes. AnyDesk/Jump Desktop/Parsec pour l'accès GUI.

### Stockage
| Volume | Taille | Usage |
|--------|--------|-------|
| NavTGV1 | 15 To | Rushes film (primaire) |
| NavTGV2 | 15 To | Rushes film (miroir) |
| 4T_IJC_th4 | 3,6 To | Archive |
| lexar2_2TB | 1,9 To | SSD de travail |
| Cartes caméra (A009, A010) | ~1 To | Média de tournage actif |
| Zoom SD | 119 Go | Enregistrements audio |
| UGREEN NAS | — | Sauvegarde réseau |
| Cloudflare R2 | — | Sauvegarde cloud des rushes (~50 Mio/s) |

---

## 2. Environnement de développement

### Runtimes
| Runtime | Version | Gestionnaire |
|---------|---------|--------------|
| Node.js | 20.20.0 (défaut), 22.22.1 | mise |
| Python | 3.10 (défaut), 3.12, 3.13, 3.14 | mise + Homebrew |
| Ruby | 3.3.6 | mise |
| Go | dernière | Homebrew |
| Deno | dernière | Homebrew |
| Bun | dernière | Homebrew |

### Shell
- **zsh** avec alias personnalisés pour les workflows Claude Code
- **Ghostty** (terminal principal), iTerm2 (secondaire)
- **tmux** avec plugin resurrect, layouts personnalisés pour sessions multi-agents

### Git
- GitHub CLI (`gh`) pour l'authentification et les workflows PR
- Git LFS activé
- Gitignore global configuré

---

## 3. Claude Code — La couche d'intelligence

### Configuration
- **Version** : 2.1.81 (dernière)
- **Modèle** : Claude Opus 4.6 (contexte 1M)
- **Thinking** : toujours activé
- **Effort** : élevé
- **Agent Teams** : activé (expérimental)

### Hooks (automatisation événementielle)
| Événement | Action |
|-------|--------|
| UserPromptSubmit | Mise à jour du titre d'onglet, alertes de contexte, sauvegarde de session |
| SessionStart | Titre d'onglet du terminal |
| Stop | Notification (son + push Telegram) |
| SubagentStop | Notification de fin de sous-agent |
| Notification | Alerte d'attention |
| PostToolUse (Edit/Write) | Vérification de cohérence linguistique |

### Refus de sécurité
Refus codés en dur pour les opérations dangereuses : `mkfs`, `dd`, force-push, lecture de clé SSH, accès au trousseau (keychain).

### Plugins (39 actifs)
Catégories : développement (superpowers, code-review, commit-commands, github, feature-dev), design (frontend-design, figma), IA (agent-sdk-dev, huggingface-skills), observabilité (sentry, vercel), productivité (Notion, slack, linear, stripe), et plus.

### Serveurs MCP (13 configurés)
| Serveur | Usage |
|--------|-------|
| Gmail (custom) | Gestion des emails |
| Telegram | Messagerie |
| Slack (binaire) | Communication d'équipe |
| Spotify | Contrôle musical |
| Instagram DMs | Messagerie sociale |
| Apple Shortcuts | Automatisation macOS |
| AppleScript | Scripting macOS |
| Krea | Génération d'images IA |
| DoorDash | Commande de livraison |
| Postiz | Planification réseaux sociaux |
| FCP XML | Intégration Final Cut Pro |
| DaVinci Resolve (x2) | Étalonnage / montage |
| DataGouv | Données ouvertes françaises |

### Skills (108 installés)
Organisés dans `~/.agents/skills/`, partagés entre Claude Code et Cursor. Inclut : suite design (18 skills), suite écriture créative, suite Vercel/Next.js, suite SEO, outils d'analyse cinéma/scénario, et outils personnalisés pour cinéaste.

---

## 4. Agents automatisés (LaunchAgents)

### Intelligence quotidienne
| Agent | Fréquence | Usage |
|-------|----------|---------|
| Morning Brief | Matin | Brief quotidien (Gmail, Calendar, Discord, GitHub) |
| Afternoon Check | Après-midi | Point de statut |
| Deadline Scanner | Quotidien | Scan des échéances à venir |
| Mentions Monitor | Périodique | Suivi des mentions sur les plateformes |

### Comptabilité (ComptaOS)
| Agent | Usage |
|-------|-------|
| Compta Scan | Scan des reçus |
| Compta Missing | Alertes reçus manquants |
| Compta Report | Reporting financier |
| Compta Subscriptions | Suivi des abonnements |

### Contenu & recherche
| Agent | Usage |
|-------|-------|
| Tech Watch | Veille technologique |
| Art Watch | Veille art contemporain |
| GitHub Stars Digest | Analyse hebdomadaire des nouveaux stars |
| X/Twitter Digest | Digest réseaux sociaux |
| LLM Visibility | Veille industrie IA |

### Système
| Agent | Usage |
|-------|-------|
| Heartbeat | Surveillance santé des agents |
| Telegram Bridge | Bot Telegram pour notifications |
| WhatsApp Bridge | Intégration WhatsApp |
| CC Changelog Monitor | Vérificateur de mises à jour Claude Code |
| Claude Desktop Backup | Sauvegarde horaire de config |
| Skills Watcher | Détection de mises à jour de skills |
| Failover Watchdog | Surveillance de bascule système |
| Voice Memo Processor | Auto-transcription des mémos vocaux |

### Synchronisation de données
| Agent | Usage |
|-------|-------|
| DataGouv Sync | Données ouvertes françaises (quotidien/hebdo/mensuel) |
| Music Sync | Synchronisation bibliothèque musicale |

---

## 5. Applications

### Créatif / production film
| Catégorie | Applications |
|----------|------|
| Montage | Adobe Premiere Pro 2025, DaVinci Resolve, Recut |
| Étalonnage/Compositing | DaVinci Resolve, Adobe Photoshop 2025 |
| Motion/VFX | Adobe After Effects, Compressor |
| Audio | MacWhisper, Descript, Soundly, Remixlive, VoiceInk |
| Encodage | Shutter Encoder, Adobe Media Encoder 2025 |
| Gestion média | Kyno, FCPX Cut Finder, CommandPost, MediaInfo |
| Design | Figma, Pixelmator Pro, Adobe InDesign 2025 |
| Capture | ScreenFlow, 4K Video Downloader+ |
| Génération IA | Mochi Diffusion, LTX Desktop, ntsc-rs |
| Sous-titres | Captionator |

### Outils IA
| Application | Usage |
|-----|-------|
| Claude (Desktop) | Assistant IA principal |
| Claude Code (CLI) | Développement + couche OS |
| ChatGPT | IA alternative |
| Perplexity | Recherche |
| Codex | Agent OpenAI |
| VoiceInk | Voix-vers-texte |
| MacWhisper | Transcription audio |

### Communication
Beeper Desktop, Discord, Telegram, WhatsApp, Zoom

### Développement
Ghostty, iTerm, cmux, Xcode, BBEdit, CotEditor, Obsidian, CodexBar, breadboard

### Navigateurs
Google Chrome, Brave Browser, Safari

### Utilitaires
Bitwarden, CleanMyMac 5, Carbon Copy Cloner, Keka, Magnet, boringNotch, PDF Squeezer, Tailscale, NordVPN, OrbStack, VLC, Toggl Track, Karabiner-Elements

---

## 6. Packages clés

### npm global
| Package | Usage |
|---------|-------|
| `@anthropic-ai/claude-code` | CLI Claude Code |
| `@google/gemini-cli` | Gemini CLI |
| `@openai/codex` | OpenAI Codex |
| `vercel` | CLI Vercel |
| `n8n` | Automatisation de workflows |
| `dmux` | multiplexeur tmux |
| `obsidian-cli` | CLI Obsidian |

### Homebrew (clés)
**CLI** : gh, git, lazygit, tmux, yazi, glow, watch, rclone, rsync, mosh
**Média** : ffmpeg, yt-dlp, whisper-cpp, tesseract, mupdf-tools, poppler
**Data** : mongodb-community, mongosh, sqlite
**Réseau** : cloudflared, wireguard-tools, tailscale
**IA** : recall (recherche de conversations), pinecone, mirroir-mcp

### Python (clés)
**IA/ML** : torch 2.8, transformers, diffusers, accelerate, huggingface-hub, anthropic, google-genai, datasets, pytorch-lightning
**Audio** : faster-whisper, whisperx, speechbrain, pyannote.audio, DeepFilterNet, librosa
**Vidéo** : opencv-python, scenedetect, ffmpeg-python
**Web** : fastapi, playwright, httpx, fastmcp, mcp
**Data** : pandas, numpy, scipy, duckdb, openpyxl
**Apple** : pyobjc, osxphotos, pymobiledevice3
**Créatif** : manim (animation), pillow, reportlab

---

## 7. Structure des projets

### Projets film
| Projet | Description |
|---------|-------------|
| The Goldberg Variations | Documentaire long métrage (Villa Albertine 2026) |
| Virus | Film sur Mihai Ionut Paunescu |
| Moon Metropolis | — |
| Rewild | — |

### Projets dev (actifs)
| Projet | Description |
|---------|-------------|
| Custom MCP Servers | Gmail, Telegram, Slack, Spotify, Instagram, Krea, DoorDash, FCP, Resolve |
| Heartbeat Agent | Agent daemon persistant |
| LLM Council | Système de débat multi-LLM |
| Life Intelligence | Système d'intelligence personnelle (« Vaisseau Amiral ») |
| Spectre | Concept Claude Code comme OS |
| Vibe Ribbon | Tableau de bord web pour Claude Code |
| Agent Viewer | Vue Kanban des agents tmux |
| Claude Code Workflow | Documentation publique du workflow CC |

### Recherche film/IA
| Projet | Description |
|---------|-------------|
| AI Cinema Research | Recherche publique sur l'IA au cinéma |
| Filmmaker AI Brain | Système augmenté par IA pour cinéaste |
| Film Production Intelligence | Outils de gestion de production |
| StoryCurve | Visualisation de récit non-linéaire (D3.js) |
| StoryExplorer | Outil d'exploration narrative |
| Buttercut | Outil de traitement vidéo (Ruby) |
| OBLITERATUS | Projet artistique |

### Outils narratifs
| Outil | Stack | Usage |
|------|-------|---------|
| storycurve | D3.js | Visualisation de récit non-linéaire |
| storyexplorer | — | Exploration narrative |
| mcp-server-tmdb | TypeScript | API TMDB pour données film |
| cc-wf-studio | Extension VSCode | Studio de workflow Claude Code |

---

## 8. Second cerveau Obsidian

- 3093+ fichiers markdown
- Synchronisé via iCloud
- Intégration serveur MCP (port 27124)
- Structure : dossiers numérotés (00-09)
- Pipeline mémos vocaux : auto-transcription → routage vers Obsidian

---

## 9. Philosophie

**Claude Code comme OS** : pas un outil de développement. Une couche d'intelligence qui unifie et pilote l'ensemble du système informatique à travers les machines et systèmes d'exploitation. Une seule intelligence, une seule mémoire, une seule continuité d'action.

**Nom du concept** : Spectre — « le fantôme au-dessus du shell »

**Workflow** : développement piloté par les specs (`/interview` avant de coder), specs créatives (`/pitch` avant la production), méthodologie liquid writing pour l'écriture de scénario.

---

## 10. Métriques (instantané du 2026-03-24)

| Métrique | Valeur |
|--------|-------|
| Processus en cours | ~930 |
| Sessions Claude Code | 8 en parallèle |
| Serveurs MCP par session | ~25 |
| LaunchAgents | 42 |
| Skills installés | 108 |
| Plugins installés | 39 |
| Stockage externe | ~40 To connectés |
| Packages Python | ~350 |
| Formules Homebrew | ~130 |
| Applications | ~110 |

Par [Ismaël Joffroy Chandoutis](https://ismaeljoffroychandoutis.com).
