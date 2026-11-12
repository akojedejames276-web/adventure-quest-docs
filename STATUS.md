# Current implementation checklist — 0.6

## Implemented and tested

- [x] Authoritative multiplayer, secure guest recovery, strong conditional Netlify room persistence and request-scoped storage clients.
- [x] Two colorful server dice; one die on squares 94–99; exact finish and overshoot.
- [x] Smaller board numbers and spatially scored regional distribution of ten snakes and twelve ladders, with four long climbs and three long descents.
- [x] Visible hero faces, cosmetic equipment, numbered nameplates, YOU markers and player follow controls.
- [x] Ten educational 3D snake species with distinct colors/patterns/silhouettes and a field guide.
- [x] Castle wizard guards, ten-second warnings, authenticated dodging, animated shots and one-life damage.
- [x] Five lives per round; zero-life skip/wait; 100-coin life purchase; room wallet recovery.
- [x] Perfect-50 clean crossing pays 100 coins once per round; coins carry within the room.
- [x] Host pause/resume, frozen guard/turn timers, restart and end without a false winner.
- [x] Chat, QR invitations, awards/history/rematches, audio, reduced motion, accessible fallback and mobile controls.
- [x] 39 server checks and ten browser checks available, with focused membership/readiness/recovery browser checks verified on 0.6; three full two-player rounds and an eight-player round in automated server tests.
- [x] Original classic rounds keep their prior rules until restart/rematch.

- [x] Visible room leaderboard, completed/started set totals, 10 points per win, and one 50-coin award per additional 20 points. Scores survive spending and reconnects.

- [x] Host admission queue, decline/remove controls, live roster updates, revoked-session entry and 3D hero reconciliation.

## Intentionally unavailable pending external setup

- [ ] Rewarded ads: requires an authorized provider and verified completions. The control is disabled; no fake reward.
- [ ] Real-money coin packs: requires a payment provider, approved pricing and server-side verification. The control is disabled; no fake charge/credit.

## Release acceptance

- [x] 0.4 publication verified: live 3D guard/wallet browser checks and three complete rounds, 82 rolls, 19 dodges, exact finishing and saved balances.
- [ ] Human test on physical devices for touch behavior, frame rate, audio and art acceptance. Browser mobile emulation is not a physical-device test.

See `V0_5_LEADERBOARD.md` for championship/long-route changes and current verification. See `QUEST_V0_4_APPROVED.md` for the owner's approved changes and `V0_4_VERIFICATION.md` for evidence. The historical original handoff is preserved; its single-die/cosmetic-only parts are superseded for new quest rounds by the later approval.

0.6 source is ready in GitHub. Netlify publication and live checks remain pending owner access; see `V0_6_ROOM_MANAGEMENT.md`.
