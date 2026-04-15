# LAUNCH.OS

A futuristic biometric launch sequence for official ceremonies, school events, and VIP launches. Put your finger on the scanner, hold for 3 seconds, and watch the video cinema roll in with cyberpunk flair.

Built because the humble YouTube "play" button does no justice to a proper ceremonial launch.

**Live demo:** https://ceremony.zafranudin.my

## What It Does

Replaces the tired "VIP taps tablet -> YouTube video plays" pattern with a full cinematic sequence:

1. **Biometric scan** - hold finger on the scanner for 3 seconds (scanline, ring progress, ticks)
2. **Authorization** - "AUTHORIZED" glitch text with RGB chromatic aberration
3. **Countdown** - 3 / 2 / 1 with hazard stripes, hex matrix cascade, diagnostic HUD
4. **Launch** - "OFFICIALLY LAUNCHED" with boom flash
5. **Cinema** - YouTube video in a cyberpunk HUD frame (no YouTube branding visible)

All driven by query params. Configure via the admin page, share the URL.

## Usage

### Quick start (any static host)

Two files, no build. Serve the folder.

```
├── index.html   Admin console (configure + generate URL)
└── launch.html  Launch experience
```

### Configure a ceremony

1. Open `index.html`
2. Paste YouTube URL (watch, shorts, or youtu.be all work)
3. Fill event title, VIP name, organization
4. Click **GENERATE LAUNCH URL**
5. Copy the URL or scan the QR from a phone/tablet on the day

### Query params

Both pages read the same params so admin URLs are themselves shareable templates.

| Param      | Purpose                                   |
|------------|-------------------------------------------|
| `v`        | YouTube video ID or full URL              |
| `title`    | Main title above scanner                  |
| `subtitle` | Secondary line under title                |
| `vip`      | VIP name, shown dramatically after AUTH   |
| `event`    | Event label in cinema HUD top-left        |
| `org`      | Organization name in cinema HUD bottom-left |

Example:

```
launch.html?v=dQw4w9WgXcQ&title=INTEGRASI+2026&vip=YB+DATO%27+SRI&org=SMK+XYZ
```

## Deploy

### Cloudflare Pages

```bash
wrangler pages deploy . --project-name=your-project --commit-dirty=true
```

### GitHub Pages / Netlify / Vercel

Drop the folder. No build step.

## Keyboard shortcuts

- **F** - toggle fullscreen
- **Esc** - abort sequence / close cinema / exit fullscreen

## Known limitations

- YouTube removed the official way to hide the player's title overlay when they deprecated `showinfo=0` in 2018. This project uses a CSS mask workaround (the industry standard). For a fully clean player, self-host video (Cloudflare Stream, Bunny, R2) or use Vimeo Pro with `title=0&byline=0`.
- YouTube end-screen cards are paused ~0.6s before video ends so the final frame stays visible without the subscribe/related overlays.
- `pointer-events: none` is set on the iframe so users cannot click through to YouTube.

## Contribute

PRs welcome. Ideas:

- Vimeo / Cloudflare Stream / self-hosted MP4 support
- Webcam-based hand detection (MediaPipe)
- Multi-VIP synchronized launch (two fingers required)
- More palette themes (current: cyberpunk yellow; maybe royal gold / national colors)
- i18n for labels (currently mixed EN/BM)

## License

MIT - see [LICENSE](LICENSE).
