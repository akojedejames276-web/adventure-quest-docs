# 0.6.1 — extra-long snake and ladder

The owner requested longer snakes and ladders again. Every newly generated board now includes a ladder climbing 60–80 squares and a snake descending 60–80 squares. These two routes span at least 6.5 board-cell units physically; the allowed maximum is 11.5. They supplement the other long/medium/short routes within the existing 12 ladders and 10 snakes, keeping the route count steady.

Distinct endpoints, no chaining, region-distributed starts, crossing/spacing penalties, reserved square 50, eight food bonuses and reachability validation remain enforced. Active boards stay fixed; restart or start a new round after publication to generate the longer routes.

All 39 server/helper checks passed after the production build, including 500 generated playable boards and explicit long-snake/ladder constraints. Browser graphics and three-set leaderboard verification are recorded after completion below.

Netlify publication remains pending owner publishing access. Source changes alone do not update the public site.

The eight-player animated graphics check passed on desktop/mobile, including castle view, non-overlapping identities and mobile bounds. The screenshot was visually inspected and saved as `images/v061-extra-long-routes.png`. Three legal browser sets completed in 76 rolls with correct leaderboard and coin rewards. The returning-player turn-cycle regression checks one complete cycle: with the extra-long ladder, a lucky player can now win on their second turn.
