# 0.6 — manage adventurers during play

The owner requested removing adventurers and admitting guests while a game is running. This supersedes the previous fixed-roster/no-midgame-join design.

## Behavior

The owner's Manage adventurers panel shows admission requests with Admit/Decline and current members with Remove. The owner cannot remove themselves. New invitation/code joins during play create waiting requests rather than active players. Waiting guests can poll/watch but cannot roll, chat, dodge or issue game actions. Approval starts the guest at square 1 with five lives and appends them to the turn order without resetting the board, other players, current turn or rewards. Existing spectators can also be admitted.

At most eight active members and eight pending requests are allowed. A full room can queue a replacement; an existing member must be removed before admission. Duplicate/concurrent approval cannot add the same player twice. Rejected or removed player credentials are revoked; their browser returns to entry with an explanation. Removal frees a member slot. Historical set results remain in room history. A returning removed user submits a new request rather than restoring revoked membership.

Removing a nonactive player preserves the current turn and guard warning. Removing the active player cancels their guard shot and advances safely to the next living player. Paused rooms stay paused with a fresh successor turn budget. An all-out room resumes when a new player is admitted. Removing the last participant from a legacy room whose host was spectating ends the round without inventing a win.

The 3D view reconciles added/removed heroes, updates numbered badges and drops removed players' queued movements. Other participants cannot use host controls; the server enforces permission checks. Public room projections omit private hashes and payout ledgers for both members and waiting guests.

## Verification

The production build and 38 server/helper checks plus a focused existing-spectator admission check passed. Six new checks cover pending-session restrictions, private projection, admission without resetting progress, host-only controls, session revocation, nonactive/active removals, paused guard cancellation, rejected requests, all-out revival, concurrent idempotent approval and full-room replacement.

Three focused mobile browser checks passed with the accessible board: joining a new room/recovery, new-player readiness/turn inclusion and host admission/removal while play continues. The same host-membership flow also passed with the 3D board, checking hero labels increase to three after admission and return to two after removal.

Live publication still requires the owner to publish the latest GitHub main build in Netlify. Local verification is not live deployment verification. Real ads/payments remain unavailable pending provider setup.
