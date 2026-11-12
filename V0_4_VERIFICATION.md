# 0.4 quest verification

## Implemented

The approved rules in `QUEST_V0_4_APPROVED.md` are implemented: two colored dice, single-die final six squares, faces, region-distributed shorter snake/ladder connections, ten educational snake species, wizard guards with a ten-second warning and dodge, five lives, clean-crossing-50 reward, room coins, a 100-coin life purchase, zero-life skip/wait/revival, pause/resume/restart/end and preserved legacy rounds.

## Server evidence

28 automated checks passed after a strict production client/function build. These include 500 generated legal/playable boards, new spacing constraints, three full two-player rounds with guard dodges and the final-six finish rule, a full eight-player round, all turn timers, host control authorization, warning ownership/replay protection, concurrent hit settlement, warning pause/resume, zero-life skips, concurrent life purchases, all-out recovery, coin award limits, wallet persistence, ad/payment action rejection and old single-die round compatibility. The compiled function still passes the request-scoped credential rotation regression using the disclosed local-emulator header shim.

Focused browser checks also passed a legal-play flow: earning coins through real rolls, reaching a guard warning, missing a shot, buying a life using earned coins, reloading the wallet and dodging. No wallet or position was injected through a test endpoint.

The full desktop/mobile, fallback, controls, graphics and 3D guard suite is completed before publication; results are recorded below. Real ad/payment activation remains intentionally unavailable and requires provider configuration. No fake ad, payment, credit or charge is implemented.

## Full browser results

All six browser checks passed in the compiled-client QA harness: desktop/mobile guest entry/customization/chat/recovery; WebGL-disabled fallback; two colored dice, field guide and host controls; eight-player identity/graphics/mobile bounds; 3D guard aiming/warning/shot and health display; and the earned-coin/hit/purchase/dodge/recovery flow. The guard test pauses the authoritative warning while loading/inspecting the 3D view, then resumes and lets the real server deadline produce a hit. No test API grants coins or changes positions.

The complete run passed 28 server tests and six browser tests. The coin-limit fixture additionally re-crosses 50 to verify that the reward cannot be farmed within one round. Screenshots were inspected. Live deployment checks follow publication; these local results do not establish physical-device performance or actual ad/payment integration.

## Live publication

The served client `index-ChjTHqBu.js` matches the tested 0.4 build. The 3D guard test and legal-play wallet test both passed again against the real Netlify deployment. The latter earned its coins through normal rolls, missed a real warning, bought a life, dodged and reloaded the saved wallet.

Three additional hosted two-player rounds completed in 31, 26 and 25 rolls (82 total), with 19 authenticated dodges and six final-stretch single-die rolls. Every move was checked by the other player's session; exact wins, no post-win shot, all awards/history, five undamaged lives after successful dodges and the expected cumulative coin balances were verified. Final QA coin balances were 100 and 200. The test used no injected dice, positions, lives or coins.

Live URL: https://adventure-quest-snakladder.netlify.app/

Actual rewarded ads and real-money purchases remain disabled by the agreed provider-setup boundary. Physical-device performance/listening/art acceptance are human checks; browser mobile emulation is not a physical device.
