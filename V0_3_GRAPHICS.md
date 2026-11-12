# 0.3 — player identification and graphics

## Player identification

Player numbers are stable within a room and match the board key, roster, accessible tokens, 3D badges and screen-space nameplates. The local player has a YOU label and gold outline. Player positions explicitly say SQ to distinguish them from player numbers. Labels keep a readable screen size when the camera moves, use collision-aware placement and connect to heroes with leader lines. Tapping a player follows that hero; Show whole board returns to the overview. Lobby heroes are now visible too. Crowded shared squares use smaller 2D badges and arranged 3D heroes.

## Graphics

Beveled textured tiles, inlaid borders, refined lighting and stronger materials replace the flatter tiles. Ladders use textured wood, larger rails/rungs and metal details, with crystalline/golden/icy/royal variants. Snake bodies taper toward their tails and have generated scale/bump textures, breathing/slithering shader motion, head movement, tongue flicks and the existing landing cinematic. The numbered endpoints remain fixed. Reduced motion stops idle snake movement.

The palace now includes masonry and roof textures, layered roofs, towers, battlements, arched lit windows, a rose window, portcullis, steps, flags and lamps. View castle provides a close-up.

Bonuses are plated food models: apples, pears, grapes, oranges, strawberries, bread, bananas and carrots. The accessible board uses matching food icons. Food types are derived deterministically from the square so clients agree. They remain cosmetic; treasure/award state and all movement rules are unchanged.

## Evidence

17 automated server/helper checks passed, including eight-label collision/bounds tests and supported food mapping. The existing desktop/mobile guest, recovery and WebGL fallback browser tests passed. A new graphics browser test uses eight authenticated players in one room and checks readable non-overlapping nameplates, stable label size during focus, animated frames, eight food bonuses, castle camera controls, mobile viewport layout and absence of WebGL shader/page errors. Screenshots were inspected.

This remains original procedural/stylized art, not a claim of photorealistic assets. The Netlify request-scoped credential fix is retained. Publication is verified separately after the source push.

## Published verification

The final `index-DYnKS52t.js` client is publicly served by the existing Netlify site. The eight-player graphics test passed again against real hosted room endpoints, including readable non-overlapping labels, stable zoom sizing, food bonuses, motion, castle controls, mobile layout and no shader/page errors. The existing server rules and private-session persistence are retained.
