# Cough Counter

OBS-friendly **cough counter** with:

- **Manual** +1 / −1 / reset (and hotkeys)
- **Optional mic auto-detect** (Web Audio — approximate)
- Session timer + coughs/hour
- Transparent **overlay** mode for Browser Source

## Live

**https://franklinelliott.github.io/cough-counter/**

## Modes

| Mode | URL | Use |
|------|-----|-----|
| Control | `/` | Settings, mic test, manual buttons |
| Overlay | `?mode=overlay` | Transparent OBS Browser Source |

## OBS setup

1. Open the control page, set sensitivity / cooldown / label
2. **Copy overlay URL**
3. OBS → Sources → **Browser**
   - URL: pasted overlay link
   - Width: **500**, Height: **320**
   - ✅ Shutdown source when not visible (optional)
   - ✅ **Transparent background**
4. For **auto mic** in OBS:
   - Right-click Browser Source → **Interact**
   - Click **Enable mic** / allow permission when prompted  
   - Or turn auto on from the control page and re-copy URL with `auto=1`

> Control page and OBS Browser Source are **different browsers**. They do **not** share a live count.  
> Run auto-detect **in the overlay** (mic permission there), or use manual +1 from the control page only for that window’s count — best practice: **auto on overlay**, manual undo via Interact or by adjusting `count` in the URL / reopening control then copying a new overlay URL with the fixed count.

### Practical stream workflow

1. Use **overlay** with `auto=1` as the on-stream counter (mic granted via Interact once)
2. Keep **control page** open on a second monitor for sensitivity tweaks and manual fixes  
3. After fixing the count on control, **copy overlay URL again** and refresh the Browser Source (or edit the URL’s `count=`)

## Auto-detect notes

- Looks for **short mid-band energy bursts** (cough-ish), with a **cooldown**
- **Higher sensitivity** = easier to trigger
- Will sometimes count laughs / yells / chair noise — hit **−1**
- Not medical-grade; for entertainment stats only

## URL params

| Param | Meaning |
|-------|---------|
| `mode=overlay` | Overlay UI |
| `count` | Starting / current count |
| `auto=1` | Auto-detect on |
| `sensitivity` | 15–95 |
| `cooldown` | ms between auto counts (500–4000) |
| `label` | Header text (default `COUGHS`) |
| `sessionStart` | Unix seconds for timer |

## Stack

Static HTML/CSS/JS on GitHub Pages. No server. Mic stays in your browser.

## License

Use freely on stream.
