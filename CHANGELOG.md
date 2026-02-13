# Changelog

## v1.7.0 — Clean Modern UI Redesign

> Requires Android 10+ (API 29)

### UI Overhaul

- **New Color System** — Replaced default Material 3 purple with a professional black/white palette and red (#DC2626) accent, inspired by Linear/Vercel design language
- **Inter Typography** — Added Google Fonts Inter across the entire app for a clean, modern feel
- **AppColors Class** — Centralized color constants for consistent theming (dark bg, surfaces, borders, status colors)
- **Dark Mode** — Near-black backgrounds (#0A0A0A), subtle surface (#121212), bordered cards
- **Light Mode** — Clean white backgrounds, light borders (#E5E5E5), bordered cards

### Component Redesign

- **Zero-Elevation Cards** — All cards now use 1px borders with 12px radius instead of drop shadows
- **Pill Status Badges** — Gateway and Node controls show pill-shaped badges (icon + label) instead of 12px status dots
- **Monochrome Dashboard** — Removed rainbow icon colors from quick action cards; all icons use neutral muted tones
- **Uppercase Section Headers** — Settings, Node, and Setup screens use letterspaced muted grey headers
- **Red Accent Buttons** — Primary actions (Start Gateway, Enable Node, Install) use red filled buttons; destructive/secondary actions use outlined buttons
- **Terminal Toolbar** — Aligned colors to new palette; CTRL/ALT active state uses red accent; bumped border radius

### Splash Screen

- **Fade-In Animation** — 800ms fade-in on launch with easeOut curve
- **App Icon Branding** — Uses ic_launcher.png instead of generic cloud icon
- **Inter Bold Wordmark** — "OpenClaw" displayed in Inter weight 800 with letter-spacing

### Polish

- **Log Colors** — INFO lines use muted grey (not red); WARN uses amber instead of orange
- **Installed Badges** — Package screens use consistent green (#22C55E) for "Installed" badges
- **Capability Icons** — Node screen capabilities use muted color instead of primary red
- **Input Focus** — Text fields highlight with red border on focus
- **Switches** — Red thumb when active, grey when inactive
- **Progress Indicators** — All use red accent color

### CI

- Removed OpenClaw Node app build from workflow (gateway-only CI now)

---

## v1.6.1 — Node Capabilities & Background Resilience

> Requires Android 10+ (API 29)

### New Features

- **7 Node Capabilities (15 commands)** — Camera, Flash, Location, Screen, Sensor, Haptic, and Canvas now fully registered and exposed to the AI via WebSocket node protocol
- **Proactive Permission Requests** — Camera, location, and sensor permissions are requested upfront when the node is enabled, before the gateway sends invoke requests
- **Battery Optimization Prompt** — Automatically asks user to exempt the app from battery restrictions when enabling the node

### Background Resilience

- **WebSocket Keep-Alive** — 30-second periodic ping prevents idle connection timeout
- **Connection Watchdog** — 45-second timer detects dropped connections and triggers reconnect
- **Stale Connection Detection** — Forces reconnect if no data received for 90+ seconds
- **App Lifecycle Handling** — Auto-reconnects node when app returns to foreground after being backgrounded
- **Exponential Backoff** — Reconnect attempts use 350ms-8s backoff to avoid flooding

### Fixes

- **Gateway Config** — Patches `/root/.openclaw/openclaw.json` to clear `denyCommands` and set `allowCommands` for all 15 commands (previously wrote to wrong config file)
- **Location Timeout** — Added 10-second time limit to GPS fix with fallback to last known position
- **Canvas Errors** — Returns honest `NOT_IMPLEMENTED` errors instead of fake success responses
- **Node Display Name** — Renamed from "OpenClaw Termux" to "OpenClawX Node"

### Node Command Reference

| Capability | Commands |
|------------|----------|
| Camera | `camera.snap`, `camera.clip`, `camera.list` |
| Canvas | `canvas.navigate`, `canvas.eval`, `canvas.snapshot` |
| Flash | `flash.on`, `flash.off`, `flash.toggle`, `flash.status` |
| Location | `location.get` |
| Screen | `screen.record` |
| Sensor | `sensor.read`, `sensor.list` |
| Haptic | `haptic.vibrate` |

---

## v1.5.5

- Initial release with gateway management, terminal emulator, and basic node support
