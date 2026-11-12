# Adventure Quest — Approved Design and Codex Build Handoff

## Mission and authority
Build a genuine, publicly playable, responsive 3D multiplayer Snakes and Ladders web game named **Adventure Quest**. The human project owner approved the complete design below. **Do not reopen approved design decisions or silently change rules.** Build in stages, test, fix issues, and ask the human explicitly whenever their input, approval, or an external action is necessary. No coding has been done in the original conversation as of this handoff.

**Human-in-the-loop rule:** Call attention to every action that requires the human as the vibe coder (account connection, deployment, credentials, approvals, paid services, platform limitations). Clearly state exactly what they must do and pause at decision gates. Never claim a site is live or a test passed unless verified.

## Core game rules (approved)
- Traditional **10 × 10 board**, squares **1–100**, numbered in the classic serpentine/back-and-forth arrangement, transformed into a 3D sky kingdom. Start at square **1**; finish at square **100**.
- 2–8 players in one room, on different devices. Six-sided die (1–6). The **server** generates dice outcomes and validates all turns/moves.
- Move forward by the exact dice result. Must **land exactly on square 100** to win. A roll that overshoots 100 results in **no movement**.
- **10 snakes and 10 ladders**, their endpoints randomized for each new round, identical for all participants and fixed for that round. Snakes always descend (mouth on higher square, tail on lower square); ladders always ascend (base on lower square, top on higher square). Generate nonconflicting legal endpoints and ensure a playable board. Clearly mark connections.
- Snakes and ladders trigger **only when landing exactly on their start**, not when passing over. Avoid unintended chaining unless explicitly approved; treat a landing as at most one snake/ladder transition.
- Rolling a six grants **no extra turn**. First player and initial order randomized by server at round start. Turns rotate automatically after movement and effects/rewards are resolved.
- Player characters may share squares freely; no collision, capturing, pushing, or blocking.
- Treasures spawn at randomized locations per round; shared layout for all players, collected when landing exactly on a treasure square. Treasure and achievements are **cosmetic only**, never modify odds or rules.
- First player to reach 100 wins immediately. Show cinematic castle victory, trophy, results, and fun cosmetic awards (Treasure Hunter, Snake Survivor, Ladder Champion). Keep room-level history of winners/awards for successive rounds.

## Floating Kingdom — approved visual world
- 3D **traditional 10×10 board**, not a winding alternative; board floats in a cloud kingdom. It is recognizable and readable at a glance.
- Five visually distinctive regions, **20 numbered squares each**:
  1. **1–20 Emerald Sky Gardens:** lush greenery, flowers, waterfalls, trees, wood and rope ladders.
  2. **21–40 Crystal Cloud Caves:** luminous crystals, blue/violet skies, glowing crystal ladders.
  3. **41–60 Golden Sky Ruins:** ancient temples, golden sunset, ornate golden ladders and glowing steps.
  4. **61–80 Frostwind Heights:** snowy floating mountains, auroras, ice ladders and bridges.
  5. **81–100 Royal Cloud Village:** suspended village, houses, lanterns, marble/gold ladders, and a **magnificent royal castle at square 100**.
- Detailed environmental landmarks for each region; regions transition gracefully without hiding tile numbering. Tiles vary in material by region but always show large high-contrast numbers. Highlight current/active tile; tapping a tile shows its number and snake/ladder connection if any.
- **Hybrid camera:** elevated overview during normal play, cinematic zoom/follow during significant actions, then return to overview. Optional manual zoom/rotate; reduced motion option.
- **10 visually varied ladders:** wood and rope climbed physically; crystal ladders magically lift; golden ladders create glowing steps; ice ladders glide upward. All are just visual treatments of the same upward transition rule.
- **10 realistic and magical snakes:** natural scales and movement mixed with themed fantasy variants (emerald python, crystal serpent, icy serpent, etc.). On exact mouth landing, camera zooms in, snake opens mouth, non-graphically swallows hero, a moving bulge or magical glow travels along body, and hero exits unharmed from tail at lower square. **Cinematic with skip/shorten option**; skipping locally must never alter synchronized game state or other players' turns.
- Customizable fantasy heroes (knights, wizards, elves, warriors, explorers; colors, outfits, accessories) with no gameplay buffs. When multiple heroes share a square, automatically arrange them, use colored rings/name labels, and compact player indicators when zoomed out.
- Responsive adaptive UI: mobile emphasizes board, large roll button, compact/collapsible chat/standings/treasure; desktop/tablet can show expanded side panels. Clear current turn, dice result, positions, progress, active player and victory status.
- **Interactive magical die:** click/tap 3D die or Roll Dice button; magical rolling effects and sound. Actual number is server-generated, animation merely reveals it.
- Dynamic region-specific background music and action effects (roll, steps, ladders, snakes, treasure, victory). Independent music/SFX sliders and mute. Respect browser audio autoplay restrictions, reduced motion and accessibility preferences.

## Multiplayer and room lifecycle
- Host creates room with unique short code. Join via **room code, invitation URL, or QR code**, without an account or app installation. Players choose display name, hero, and Ready status.
- Host can start whenever **at least two players are Ready**, without waiting for every person in lobby; only Ready players participate in that round. Max eight players.
- **Host-controlled per-round turn timer:** 30, 60, or 90 seconds, or No Timer. Setting locked for round. On timeout for a connected player, server automatically rolls/moves. Must define server-side timing and idempotency to prevent double rolls.
- **Disconnect recovery:** 60-second grace period. After it expires, disconnected player's turns are skipped (not auto-rolled), keeping their hero and progress saved. Player can securely return during the active round, using original browser session or private recovery link, and resume; **public room code alone must not allow account/hero takeover**. Carefully handle turns during grace period so room does not stall indefinitely.
- **Chat and quick emoji reactions**, with mute controls; basic input validation, message length/rate limits and safe text rendering. Do not let chat affect game state.
- After winning: host chooses **Quick Rematch** (same available players confirm Ready) or **Return to Lobby** (new players can join/change heroes). Room code persists; new round rerandomizes snakes, ladders, and treasure and randomizes first player/order again. Room match history records winners and cosmetic awards.

## Technical implementation and release constraints
- Build a **real multiplayer** web app, not independent local simulations. Server is source of truth for rooms, randomized board, dice, moves, turn ownership, timers, disconnect/reconnect, results and rematches. Clients synchronize via robust polling or another deployment-compatible method; never pretend serverless polling is WebSocket real time.
- Proposed stack: React + TypeScript frontend, Three.js / React Three Fiber for 3D, modular TypeScript game engine with deterministic/testable rule helpers. Prioritize performant mobile rendering and accessible fallback controls.
- Preferred delivery target: **Netlify**. The original project brief calls for a self-contained Netlify deploy ZIP with root `netlify.toml`, `package.json`, lockfile, frontend source/assets, and serverless endpoint at **`netlify/functions/game.ts`**, called by frontend at **`/.netlify/functions/game`**. Persistent multiplayer state via **Netlify Blobs**, with strong consistency and conditional-write / optimistic-concurrency safeguards where supported; investigate current API and deployment compatibility, and do not assume atomic compare-and-swap without verification. No GitHub, command-line work, environment variables, API keys, or manual database setup should be required **of the human**. If the platform cannot meet these requirements, explain the limitation and request approval for a change rather than quietly switching architecture.
- Security: issue unguessable player session tokens; keep privileged actions server-side; verify room membership, host privileges, active turn, allowed transitions, anti-replay/idempotency and room capacity. Validate all client input and sanitize chat.
- Deliver first a playable core loop; test with two independent sessions/devices; then layer 3D world and animation without changing mechanics. Test **at least three full rounds** with two players, including winner/scoring, disconnect/reconnect, exact landing/overshoot, simultaneous roll requests, timeout, rematch, chat and production build. Verify the packaged Netlify function works after build and that a public URL is reachable from separate devices before claiming completion.
- If sophisticated 3D models/animations cannot be fully achieved with available assets or time, transparently report status and seek approval before substituting simplified art. Avoid unlicensed third-party assets/music.

## Recommended execution sequence
1. Inspect working environment and verify current Netlify Functions/Blobs APIs, especially consistency/conditional updates. Outline implementation architecture and any risks. Ask human only for genuinely necessary decisions/actions.
2. Implement typed game rules, room state model, secure actions and tests.
3. Implement Netlify function and persistence/concurrency handling, and test multi-client turn synchronization.
4. Implement responsive frontend, lobby, game board, hero tokens, dice, chat, timer, reconnect, rematch, awards.
5. Add five-region 3D Floating Kingdom, different ladder/snake visuals and cinematics, accessibility/audio, and performance tuning.
6. Build and test production bundle, package deployable ZIP, test 3 rounds with independent sessions, and guide human through Netlify deployment if needed. Verify actual public play.

## Required human checkpoints
- Before changing any approved gameplay rule, major visual concept, deployment approach, or introducing paid services/credentials: ask and wait.
- When a human must connect or authorize a service, perform a deployment step, test on another physical device, or approve a milestone: clearly flag **ACTION NEEDED** with concise instructions.
- Show first playable multiplayer milestone and get human review before heavy 3D polish.
- Do not claim completed builds, tests, or deployment without evidence. Keep a running checklist of implemented, tested, pending and blocked features.

**Start now with the architecture and working game foundation.** The human already approved the overall game design; do not ask them to choose the same options again.
