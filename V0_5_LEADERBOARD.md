# 0.5 — longer routes and room championship

The owner requested more/longer ladders, longer snakes and a visible leaderboard with set totals. The owner confirmed 10 points per set win; every additional 20 points awards 50 room coins.

## Delivered behavior

The leaderboard is an expanded panel above the board on desktop and mobile. It shows each player's numbered identity, set wins, cumulative points, current square and coin balance; tied leaders share the crown. It also shows who is furthest in the current set, completed sets, sets started and progress toward the next coin bonus.

Scores come from unique authoritative set results. A finished win adds 10 points. Reaching 20, 40, 60, etc. points adds 50 coins each time. Spending coins does not spend points. Host-ended/restarted sets do not create winners or points. Existing saved histories count toward scores; any previously earned milestone coins are credited once on the next authenticated room request. The private payout ledger and conditional room writes prevent reconnects, retries or concurrent polls from paying twice. These coins are separate from Perfect-50 rewards.

New boards have 12 ladders and 10 snakes: four ladders climb at least 25 squares, and three snakes descend at least 30. Routes retain distinct endpoints, region-distributed starts, crossing/spacing penalties, eight food bonuses and a reachability check. Existing boards stay fixed until a new round/restart. Long ladder arches rise higher in the 3D view.

## Verification

The strict production build and all 32 server/helper checks passed. Four scoring checks cover historical migration under concurrent polls, consecutive wins through 40 points, idempotent retries, private ledger projection, rejected client-side point claims, spending coins, host end/restart and duplicate historical results. Board checks generate 500 legal boards and verify the route counts and minimum long-route counts.

Desktop/mobile browser results are recorded below. Live publication is pending confirmation. Physical-device art/performance acceptance still requires the owner's device. Ads and real-money purchases retain the agreed disabled state pending provider setup.

Local desktop/mobile leaderboard testing completed three legal two-player sets in 81 rolls, verified both clients' scores/coins, reloaded the session and confirmed that a host-ended fourth set left the completed count at three. The eight-player 3D graphics/identity check also passed with the longer routes. Screenshots were visually inspected: `images/v05-leaderboard-desktop.png`, `images/v05-leaderboard-mobile.png` and `images/v05-long-routes.png`.

The remaining five browser regression checks also passed: guest entry/customization/shared play/settings/private recovery/device return; WebGL-disabled fallback; dice/species/host controls; animated guard warning/hit; and legal earned-coin life purchase/dodge/wallet recovery. Together with the two focused checks above, all seven browser checks passed against the compiled client.

A second local leaderboard run passed three more legal sets in 92 rolls while saving the delivery screenshots. GitHub source commit `839311e` contains the implementation. At the publication check the public Netlify URL still served the prior 0.4 client (`index-ChjTHqBu.js`); the expected 0.5 client is `index-xnKgWd4f.js`. Do not treat local results as a live 0.5 pass until that build is published and rechecked.
