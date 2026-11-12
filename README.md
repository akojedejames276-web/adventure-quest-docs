# Adventure Quest — playable core milestone

Server-authoritative multiplayer Snakes and Ladders, built for Netlify Functions and Netlify Blobs. This is the first review milestone, **not the finished 3D game or a verified public deployment**.

## Included

React/TypeScript responsive client; traditional serpentine 10×10 board; five region colors; inspectable snake/ladder connections; shared hero tokens; lobby and Ready states; 2–8 players; randomized turn order, 10 snakes, 10 ladders and treasure; server dice; exact finish and overshoot; cosmetic awards and room history; server timer; disconnect grace and private recovery; chat and emoji; rematch and open lobby; invitation URL and QR.

## Architecture

`src/shared/rules.ts` contains deterministic board/move helpers. `src/server/engine.ts` owns transitions. `src/server/service.ts` validates sessions and commits through `RoomStore`. `netlify/functions/game.ts` is the real production endpoint; it uses strong-consistency Netlify Blobs reads and conditional `onlyIfNew`/`onlyIfMatch` writes. Missing ETags cause a safe failure. No production in-memory fallback exists.

Each room is one record. A transaction retries on ETag conflict, rereads state, and repeats validation. Server-issued 256-bit random bearer tokens are stored hashed; public state excludes hashes and receipts. Roll commands include the expected monotonically increasing turn ID. Recent action request IDs are deduplicated. A stale roll never becomes a new turn's roll even when receipt history is pruned.

Clients poll every 1.5 seconds. This is polling, not WebSocket realtime. Server timestamps are authoritative. A connected current player is auto-rolled when a request observes an expired deadline. Presence becomes away after 15 seconds without a heartbeat, followed by 60 seconds of grace; then that player's turn is skipped. With nobody online, no background worker runs; the next authenticated request settles presence/turns. A reconnect proves ownership with the existing token. A public invitation cannot take over a player. Recovery downloads contain a private bearer link; keep them private.

Board generation uses distinct endpoints (excluding 1 and 100), prevents chains, and checks that 100 is reachable using legal die outcomes. Treasures use unused endpoints and are shared, consumed cosmetics. Hero changes have no gameplay effect. A six always ends the turn. Quick Rematch accepts only the existing roster; Return to Lobby opens room joining again.

## Validation

`npm ci` then `npm test` runs strict TypeScript checking, the Vite production build, compiled function build, and tests. `npm run dev` is a developer-only memory-backed harness; state is lost on restart. The deployed function uses Blobs instead.

See `docs/STATUS.md` for precise test evidence and remaining work. No browser UI or public-device test has passed yet. The Netlify SDK local emulator omits read ETags; its integration test explicitly tests fail-closed behavior and then uses a **test-only** missing-header shim. The shim is absent from production.

## Netlify packaging and deployment

The source ZIP contains root `netlify.toml`, `package.json`, lockfile, frontend source, tests, compiled client, and `netlify/functions/game.ts`. Netlify's Git-based build uses the detected build command `npm run build`, publish directory `dist`, and functions directory `netlify/functions`. Node 22.12+ is required by the locked Blobs SDK; the supplied `.nvmrc` selects Node 22. Netlify supplies the function's Blobs context; no database or application secret setup is designed into this app.

**Do not drag only `dist/` into Netlify Drop. Static Drop does not build the TypeScript function and would leave multiplayer unavailable.** This milestone archive is buildable Netlify source, not a verified one-click deploy archive. Account authorization and an actual deploy are pending. The final release ZIP, hosted conditional-write verification, and two physical-device test remain release requirements. Do not substitute static hosting or another persistence architecture.

## Repositories

Repository pair: `akojedejames276-web/adventure-quest` (code) and `akojedejames276-web/adventure-quest-docs` (approved handoff, architecture, status). Both remote repositories are now accessible. Existing repository history is preserved. The source and documentation are prepared for publication to their default branches.

## Next gate

Review the first playable milestone after a preview/deployment can be accessed. Heavy 3D Floating Kingdom work waits for human review as required by the approved handoff. All sophisticated models, snake cinematics, hybrid camera, animation, and audio remain pending; the readable board is the implementation-sequence core milestone, not a proposed replacement visual design.
