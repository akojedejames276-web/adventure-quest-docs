# 0.5.1 — switching rooms

The owner reported that trying to join another room returned them to their existing game. The home link previously reloaded the active saved session, and the only exit control was below the board. A live browser probe also reproduced a stale invitation URL preventing a newly created room from restoring after reload. Fresh invitation joins themselves succeeded on the live service.

The header now has a visible Switch room button. It clears the active session and room view, opens entry, clears the old invitation query and retains private saved-room recovery. The home logo performs the same navigation. Adopting a room clears stale invitation queries. Entering a room scrolls to its heading; the mobile header wraps without horizontal overflow. This navigation does not delete the shared room or alter other players.

The production build and two focused browser checks passed: mobile room switching, entry after reload, joining a different room, recovery after reload, logo navigation, return to a saved room and creating a room after an invitation; plus three legal leaderboard sets (87 rolls) with correct scores and coin rewards. Multiplayer server code is unchanged.

Publication remains pending Netlify owner action: the public URL still serves the prior 0.4 build. Publish the latest GitHub main build to enable this fix; live 0.5.1 verification must follow publication.
