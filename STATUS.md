# Current implementation checklist

## Implemented and locally verified

- [x] Typed authoritative engine and traditional 10×10 board.
- [x] Strong-consistency conditional Netlify Blobs room persistence and compiled function.
- [x] 2–8 guest players, secure private sessions, Ready-only start, randomized board/order/dice.
- [x] Exact finish, overshoot, one connection per landing, no extra turn for six, cosmetic treasure/awards.
- [x] Timers, disconnect grace/skips, recovery, chat/reactions, invitations/QR, history/rematches.
- [x] Five-region 3D Floating Kingdom, castle, themed connections and procedural heroes.
- [x] Cosmetic customization, step/connection animations, cinematic/overview camera, orbit/zoom, local skip.
- [x] 3D die, victory presentation, synthesized region music/effects and sound controls.
- [x] Reduced motion, accessible board, WebGL fallback, mobile controls and collapsible panels.
- [x] Guest device departure, saved adventures, private-link return and network retry handling.
- [x] 15 automated server checks; desktop/mobile-emulated browser flow and WebGL-disabled fallback.
- [x] Both requested source/documentation repositories accessible and maintained.

## Release acceptance pending

- [x] Published version 0.2 verified at the live URL; both guest/recovery and WebGL-disabled browser suites passed against hosted functions. Pre-update room histories restored after deployment.
- [ ] Owner test on two physical devices, including touch input, visual legibility, frame rate and listening.
- [ ] Owner visual acceptance of the original procedural art against the detailed approved brief.
- [ ] Broader long-running storage/history/abuse and load checks beyond the exercised rooms.
- [x] Verified complete downloadable source ZIP supplied under `releases/`, with SHA-256 and delivery instructions. Static Netlify Drop alone cannot build the function; the existing Git-based Netlify build is the supported deployment path.

No sign-up/sign-in account system is being added: the owner clarified that guest entry and recovery should be tested. Host privileges remain with the original private host session; automatic host transfer has not been introduced.

See `V0_2_VERIFICATION.md` for evidence and limits; `LIVE_VERIFICATION.md` records earlier hosted core checks. A tested implementation does not establish physical-device or artistic acceptance.
