# 0.5.2 — include newly joined players in the turn order

The owner reported that new guests could join by invitation but only the existing players received turns. The start action selected connected Ready players and silently excluded connected unready guests. This behavior is a supported explanation of the report; the owner's exact private room state was not inspected.

Start now requires every connected lobby member to tap I’m Ready and at least two connected members. The server rejects early start requests with the waiting players' names. The client disables Start and displays who is not ready. The authoritative randomized turn order includes every connected member once they are all ready. Away members remain excluded, and the UI explains this. A round's roster stays fixed after start. Restart preserves that roster; to include excluded players, end the round, return to the open lobby, ready everyone and start a new round.

All 33 server/helper checks passed after a production build. New regression coverage starts an old two-person round, returns to the lobby, joins two guests, rejects starts before both guests are ready, verifies all four IDs in the new turn order and rotates eight turns through all four. It also checks that genuinely away members sit out. The existing Ready-only test now verifies rejection rather than silently excluding an online unready member.

A three-browser mobile check passed: two returning players plus a new invitation guest, disabled Start with the guest named as waiting, enabled Start after the guest is ready, and an actual UI dice roll for each of the three players.

The live URL still serves the older `index-ChjTHqBu.js` client. The fix is in GitHub and the 0.5.2 source ZIP; Netlify publication and live verification remain pending owner publishing access. The tested client is `index-DwAZGNb9.js`.
