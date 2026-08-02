# Cough Counter

OBS cough counter with **manual** controls, **mic auto-detect** on the control page, and **live sync** to the OBS overlay.

## Live

https://franklinelliott.github.io/cough-counter/

## Stream workflow

1. Open the control page  
2. **Create live room**  
3. **Copy overlay URL** (must include `room=`)  
4. OBS → Browser Source → paste · ~500×320 · transparent  
5. Control page: **Enable mic** + optional auto  
6. Keep the control page open  

Coughs on the control page update OBS within ~0.5s.

## Notes

- Rooms last about **24 hours** — create a new one each stream if needed  
- Auto-detect can false-trigger — use **−1**  
- Control mic is the source of truth when using live rooms  

## Repo

https://github.com/FranklinElliott/cough-counter
