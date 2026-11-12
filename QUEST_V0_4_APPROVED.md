# Approved expanded quest rules — version 0.4

The owner approved the interpreted design in chat after requesting faces, colorful two dice, timeout/restart/end, clearer layouts, educational snakes, guards, lives and coins. This approval supersedes the original single-die/cosmetic-only brief for the new quest mode. Player appearance and food collectibles remain cosmetic; earned coins can now restore lives.

## Rules implemented

- Two independently server-generated six-sided dice are added together. From square 94 onward, one die is used so square 99 can finish. Exactly 100 still wins; overshoots do not move; neither sixes nor doubles grant an extra turn.
- Five starting lives per round. On finishing a roll in the castle region (81–99), a wizard guard aims at that player. Square 100 wins immediately without another shot.
- A visible 10-second warning gives the targeted player a chance to dodge. A timely authenticated dodge avoids damage. A missed warning removes exactly one life, then turns continue. Each completed castle-region roll triggers at most one warning. Guard effects never push the hero to another square.
- Zero-life heroes retain their positions but their turns are skipped. A life purchase puts them back into the normal order. If everyone is out of lives, the room waits without declaring a winner; a purchase resumes play, or the host can restart/end.
- Finish a move at or past 50 without having taken a snake to earn 100 coins, once per round. A snake during that first crossing invalidates the clean start. Ladders are allowed. Later snakes do not remove an already earned reward.
- 100 room coins buy one life, up to five. Coins persist within the room, including reconnects/rematches/restarts. Starting/restarting a round restores five lives and resets that round's clean-start eligibility. Coins never move between rooms or become cash.
- Host pause freezes both turn time and any pending guard warning. Resume restores the remaining durations. Restart resets the round/board/order without deleting history or coins. End closes the current round without inventing a winner.
- Existing active classic rounds keep their original rules until restart/rematch. New quest rules are enabled at a new round boundary.

The 10-second warning, per-completed-roll attack timing and five-life refill cap are concrete implementation choices for the approved warned-shot/five-chance design. They are shown in the lobby rules and interface.

## Advertising and payment boundary

The owner approved building controls while provider setup remains pending. Watch-ad and buy-coin controls are visibly disabled. No ad completion, payment, coin credit or charge is simulated. No client action can grant ad rewards or purchased coins. Real activation needs an authorized rewarded-ad provider with verified completion, a payment account, approved packs/prices and server-side verification. No credentials should be pasted into chat.

## Education and layout

Ten distinct snake species have named colors/patterns, relevant silhouette details, habitat/fact/venom information and a find-on-board action. They are stylized educational illustrations. Smaller numbers and spatially scored shorter connections leave more open board space while retaining ten snakes and ten ladders, two starts of each kind per 20-square region, unique endpoints and a reachable finish.
