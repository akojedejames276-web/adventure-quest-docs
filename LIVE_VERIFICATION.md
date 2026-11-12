# Live core verification — 12 November 2026

Deployment tested: https://adventure-quest-snakladder.netlify.app/

Public page and `/.netlify/functions/game` returned HTTP 200 without a Netlify login. Tests used isolated QA rooms and server-issued private sessions. Tokens and recovery links are not included in this report.

## Hosted API

Three full two-player rounds passed in 23, 5 and 12 moves (40 total). Both independent sessions polled after every move and agreed on turn ID, move result and board state. Exact square 100 victories, all three cosmetic awards, rematches and successive room history passed. During these rounds the suite observed three overshoots with no movement, two snake effects, seven ladder effects and four treasure collections.

Two simultaneous requests sharing one roll request ID committed one turn only. A stale distinct roll was rejected with 409. Invalid private session was rejected with 401. Chat synchronized between participants.

Separate timed tests confirmed a connected current player auto-rolled once after a 30-second deadline; a disconnected player retained the turn during grace; after the 60-second grace period expired, the disconnected turn was skipped without a roll. The original private session returned with its saved square.

These hosted tests use actual deployed persistence, without the local emulator's missing-header shim. They demonstrate the exercised conflict/retry cases, not a claim of unlimited-load or exhaustive production correctness.

## Browser

Two isolated headless Chromium contexts (desktop 1440×1000 and mobile-emulated 390×844) passed room creation, invitation join, Ready/start, one move synchronized to both browsers, chat delivery and reload recovery. No browser page errors or horizontal mobile overflow were observed. Full-page screenshots were inspected.

The screenshots exposed missing diagonal-arrow font glyphs and a cramped square-100 castle icon on mobile. A small follow-up replaces endpoint arrow glyphs with inline SVG, uses text in the legend, and adjusts the mobile castle/number contrast. Its strict TypeScript, production build and ten automated tests passed; deployment of that follow-up must be confirmed separately.

## Remaining gate

The owner still needs to play on two physical devices and review this first playable core. Mobile emulation is not a physical-device check. Heavy 3D world/animation/audio work waits for that review, as specified by the approved handoff.
