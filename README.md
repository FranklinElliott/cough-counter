# Cough Counter

Transparent **OBS Browser Source** cough counter for streams.

- **Manual** +1 / −1 / reset (buttons + hotkeys)
- **Mic auto-detect** on the control page (approximate)
- **Live room sync** so the OBS overlay updates when the control page counts a cough
- Session timer + coughs per hour
- Event log

> Auto-detect is for fun stream stats — not medical-grade. Laughs/yells can false-trigger; hit **−1**.

## Live demo

**https://franklinelliott.github.io/cough-counter/**

| Page | URL |
|------|-----|
| Control | https://franklinelliott.github.io/cough-counter/ |
| Overlay | same site with `?mode=overlay&room=…` (copy from control) |

## Recommended stream setup

1. Open the **control page**
2. Click **Create live room**
3. Click **Copy overlay URL** (must include `room=`)
4. OBS → **Sources → Browser**
   - URL: pasted overlay link
   - Width **500** · Height **320**
   - Enable **transparent background**
5. On the control page: **Enable mic**
6. Optional: turn on **auto cough detection** and tune sensitivity / cooldown
7. **Keep the control page open** while streaming

Coughs counted on the control page (mic auto or manual) push to the overlay in about **0.5 seconds**.

### Why a “live room”?

Chrome (control) and OBS Browser Source are **different browsers** — they don’t share memory.  
The live room is a short-lived shared state so both stay in sync.

- Rooms last about **24 hours**
- Make a **new room** each stream if the old one expired
- After creating a new room, **update the OBS Browser Source URL**

## Manual controls

| Action | Control UI | Hotkey (control page) |
|--------|------------|------------------------|
| +1 cough | **+1 Cough** | `Space` or `+` |
| −1 undo | **−1** | `-` |
| Reset | **Reset** | `R` (asks to confirm) |

Manual changes also **sync to OBS** when a live room is active.

## Mic auto-detect

- Runs on the **control page** (not required inside OBS)
- Watches mid-band audio bursts with a **cooldown** so one cough doesn’t count many times
- **Higher sensitivity** = easier to trigger
- Use **−1** when it miscounts

You do **not** need to grant mic permission inside OBS if you use live room + control-page mic.

## URL parameters

| Param | Meaning |
|-------|---------|
| `mode=overlay` | Transparent overlay UI for OBS |
| `room` | Live sync room id (**required** for control → OBS) |
| `count` | Current / starting count |
| `auto=1` | Auto-detect on (control page) |
| `sensitivity` | 15–95 (higher = more sensitive) |
| `cooldown` | Milliseconds between auto counts (500–4000) |
| `label` | Header text (default `COUGHS`) |
| `sessionStart` | Unix seconds for session timer |

Example overlay URL shape:

```text
https://franklinelliott.github.io/cough-counter/?mode=overlay&room=YOUR_ROOM_ID&count=0&label=COUGHS
```

## Stats shown

- **Count**
- **Session** time since session start
- **Per hour** (count ÷ session hours)
- Overlay shows **LIVE** when the room is syncing

## Stack

- Static HTML / CSS / JS on **GitHub Pages**
- Mic: Web Audio API in your browser
- Live room: temporary JSON blob host (no account required)
- No app install, no server you maintain

## Privacy

- Mic audio is processed **locally** in your browser for detection
- Only the **count and settings** are written to the live room (not audio)

## Limitations

- Auto-detect will never be perfect
- Live rooms expire (~24h)
- Control page must stay open for mic + publishing
- If sync fails, the pill shows an error — create a new room and update OBS

## Repo

https://github.com/FranklinElliott/cough-counter

## License

Free to use on stream.
