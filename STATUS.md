# Implementation checklist — 12 November 2026

## Implemented

- [x] Milestone 1: Netlify API research and architecture; locked `@netlify/blobs` 11.1.9.
- [x] Milestone 2: typed model, deterministic rule helpers, secure server actions and tests.
- [x] Milestone 3 implementation: Netlify function, strong Blobs reads, conditional writes, optimistic retries, turn IDs, recent request deduplication.
- [x] Milestone 4 core UI: responsive readable board, hero selection, tokens, die/button, lobby, Ready, timer, chat/mute/emoji, recovery, QR invitation, results, history, rematch.
- [x] Board playability verified by graph traversal; all endpoints distinct, no chaining.
- [x] Local code and documentation Git repositories prepared.

## Tested

- [x] Strict TypeScript checks and production frontend/function builds.
- [x] 500 generated boards: 10 snakes, 10 ladders, legal/distinct endpoints, eight treasures, reachable finish.
- [x] Three full two-player engine/service rounds: 223 legal turns total, winners, awards, reset and history.
- [x] Exact finish, overshoot, passing a connection, one transition per roll, treasure, no extra turn on six.
- [x] Simultaneous rolls and retry requests: one committed move; stale distinct request rejected.
- [x] Timeout and concurrent polling; 60-second disconnect grace, skip, secure return, No Timer.
- [x] Host and membership authorization, Ready-only roster, max eight, timer locking, chat validation/rate limit, public token exclusion.
- [x] Official Blobs emulator: create-if-new conflicts; missing GET ETag safely rejects update.
- [x] Test-only ETag header shim: stale conditional writes rejected; actual compiled function loaded and exercised by two separate player credentials through create/join/start/roll/poll. This does not establish hosted atomicity.

## Pending / blocked

- [ ] Human review of playable milestone before heavy 3D polish — explicit handoff gate.
- [x] Desktop/mobile-emulated Chromium browser core checks passed on the live URL; screenshots inspected. See LIVE_VERIFICATION.md.
- [x] Remote GitHub repository access confirmed for both requested repositories; existing initial history retained. Source publication is recorded by the repository commits.
- [x] Owner deployed the project to https://adventure-quest-snakladder.netlify.app/; page and multiplayer endpoint are publicly reachable.
- [x] Hosted duplicate-roll concurrency, stale roll rejection, independent-session synchronization, timed auto-roll, grace expiry and private recovery passed. Cold-start persistence isolation and physical devices remain unchecked.
- [ ] Owner test on separate physical devices; public URL and two isolated desktop/mobile-emulated browser sessions have been verified.
- [ ] Complete 3D Floating Kingdom, varied snake/ladder meshes, hero customization beyond class/color, castle cinematic, camera, skip/shorten, audio controls, accessible animation and rendering performance.
- [ ] Final deploy archive proven against Netlify deployment workflow. Current ZIP is buildable source plus compiled client/function, not a verified Netlify Drop artifact.
- [ ] Broader release hardening: room creation/join abuse limits; reconnect network retry UX; host departure/lobby roster management; storage quota/history growth handling; full browser accessibility and mobile performance audit.

## Evidence limits

The three-round suite uses two server-issued player sessions and deterministic injected random entropy against an isolated memory repository. The compiled function suite uses real Request/Response objects and the official SDK's local HTTP emulator, with the disclosed ETag shim. These are not browser sessions, physical devices, hosted storage, or a live public game. Tests are local development evidence only.

## Human checkpoints

1. Repository access checkpoint resolved: both requested private repositories are accessible. No additional GitHub setup is currently requested.
2. Netlify deployment requires account-side authorization. After repository push, a UI import may be used if the owner agrees; Codex must not silently change the approved deployment approach. No secret values should be pasted into chat.
3. Once accessible, review the board and multiplayer core. Approve proceeding to 3D polish or give feedback. This is review of implementation, not reopening approved rules.
4. After deployment, open the public URL on two physical devices and report any synchronization/recovery issue; Codex will also verify available hosted endpoints before claiming completion.

## Live follow-up

See [LIVE_VERIFICATION.md](LIVE_VERIFICATION.md) for the hosted three-round and browser test results. Earlier local-emulator limitations remain documented as historical evidence; hosted tests do not use the emulator shim.
