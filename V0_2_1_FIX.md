# 0.2.1 — request-scoped Netlify Blobs clients

A live create-room request reproduced an expired Netlify storage token. The production entrypoint cached both the room handler and traffic limiter in module scope; both closures retained SDK clients initialized with earlier request credentials.

The entrypoint now constructs the room store, service, traffic limiter and handler for every invocation. Trusted-IP limiting runs through the handler's validated-command hook. Platform credential failures are not exposed as raw token errors to players. No room keys, player tokens, rules or persistent room data are migrated or removed.

The compiled-function integration test now invokes one loaded module against a local Blobs backend, stops that backend, rotates the SDK context to a new authenticated backend over the same stored data, then restores an existing player and creates a room with the same module. This covers both cached room and cached traffic clients. All 15 server checks passed; the strict production build passed. The test retains the previously disclosed local-emulator ETag header shim.

The new source ZIP supersedes the 0.2.0 preview package. Live verification is recorded after deployment.

## Live checks

After deployment, room creation returned HTTP 200. Two isolated live browser sessions passed create/join, Ready/start, synchronized rolling and reload recovery. A pre-existing private player session also restored its room with all three prior round histories intact.
