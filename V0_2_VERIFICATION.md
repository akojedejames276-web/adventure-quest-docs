# Version 0.2 verification

## Added

- Three.js Floating Kingdom with a traditional 100-tile board, region terrain and original procedural landmarks.
- Themed snakes/ladders; hero class models, name labels/rings, cosmetic colors, outfits and accessories.
- Local step/climb/swallow-and-exit effects, recent server move stream, cinematic/overview camera, orbit/zoom, skip and reduced motion.
- Animated CSS 3D die revealing the server roll; castle camera victory presentation.
- Original synthesized region music and action effects, explicit audio enable, separate sliders and mute.
- Mobile roll bar, narrow-screen camera fit, collapsible party/chat and automatic WebGL fallback.
- Saved guest adventures and improved private recovery downloads. Account registration was deliberately excluded following the owner's clarification.
- Authenticated retry IDs, duplicate join rejection, per-IP create/join limits and lobby reopening from rematch.

## Automated evidence before publication

15 server tests passed, with strict TypeScript and production client/function builds. The suite includes 500 legal/playable board generations; three full two-player rounds; a full eight-player round; exact finish/overshoot; simultaneous request/replay protection; all 30/60/90-second timer settings; disconnect grace/private recovery; Ready-only participation; cosmetic validation; chat/security; recent move order; room rate-limit counters; and the compiled function against the documented local emulator shim.

Two production-client browser tests passed in Chromium:

1. Isolated desktop and mobile contexts: create/join, hero customization, Ready/start, synchronized movement, accessible-board tile inspection, chat, enabling audio/reduced motion/mute, downloaded private link in a third context, URL-fragment removal, reload, device departure and returning to the saved adventure. No page errors or horizontal mobile overflow observed.
2. A browser launched with WebGL disabled: automatic fallback, accessible square inspection and clear fallback notice.

The latest generated snake-skin texture is a visual follow-up; its final build and hosted rendering smoke check are recorded with publication. Screenshots in `docs/images` are from production-client local QA; they are not photographs of physical devices.

## Acceptance still requires human action

- Play the new deployment from two physical devices; check touch controls, reconnect and acceptable frame rate on the actual hardware.
- Review the original procedural/stylized art against the approved detail level, particularly hero and snake fidelity and small-screen numbering. Detailed visual acceptance has not been assumed.
- Audio controls and context startup are automated; perceived loudness and musical preference require listening.

A complete final-release claim depends on those checks. No new paid service, mandatory account, database, or gameplay rule change was introduced.

## Published deployment results

The served client `index-CRZtUV4f.js` and lazy 3D chunk match the final build including generated snake scales. Both browser suites passed again against https://adventure-quest-snakladder.netlify.app/ using real Netlify Functions/Blobs. Guest recovery was tested with a downloaded private link in an independent third browser context, and the private fragment was removed after import.

A host session created before this update successfully polled its original room after the new deployment; all three prior round histories were intact. This verifies persistence across the exercised deployment boundary.

The verified source ZIP is tracked under `releases/` because the connected GitHub integration rejected binary release-asset uploads. ZIP integrity and required root files were checked. SHA-256: `c119d0a88f0b076ea64091e2f2c3de193bd9a30e4bd7dbb182106e1926da61ea`.

Remaining human acceptance is physical-device play, art fidelity and listening. No physical-device test or subjective artistic approval is claimed.
