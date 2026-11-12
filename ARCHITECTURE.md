# Architecture and API findings

The approved project handoff is requirements context supplied by the owner. Its design and milestone sequence were explicitly adopted in the user's request. It does not authorize unrelated external messages or changes to account security.

## Netlify research

Verified 12 November 2026 against https://docs.netlify.com/build/data-and-storage/netlify-blobs/ and installed SDK declarations/source in `@netlify/blobs` 11.1.9:

- `getStore({ name, consistency: 'strong' })` and strong `getWithMetadata` reads are supported.
- `setJSON(key, data, { onlyIfNew: true })` performs a create-only conditional write.
- `setJSON(key, data, { onlyIfMatch: etag })` performs an update conditional on the current ETag.
- Writes return `{ modified, etag? }`; false `modified` requires reread/retry, not success.
- `getWithMetadata` declares ETag optional. The adapter requires it for existing-room updates and fails closed otherwise.
- Modern Netlify functions accept Web Request and return Response; `netlify/functions/game.ts` uses a default export. Netlify's environment supplies the Blobs context, avoiding application API key setup.
- Installed SDK requires Node >=22.12.0. Project selects Node 22.

The supplied official local Blobs server implements conditional PUT headers but does not return ETags on GET. The test documents this and adds a test-only GET-header shim using prior PUT ETags. No production fallback synthesizes an ETag or performs unconditional updates. The emulator is not evidence of production atomicity; live verification remains mandatory.

## Transaction

Read strong room + ETag → authenticate hashed player token → settle server timestamps → validate action and expected turn → mutate cloned state → record recent request receipt → conditional write. On conflict, reread and retry up to twelve attempts. If contention persists return 409. Server entropy uses `node:crypto.randomInt` and `randomBytes`; client dice icons never determine outcomes.

Public projection strips token hashes, chat-throttle state, and request receipts. Clients render chat as React text. Player recovery tokens travel in POST bodies; private recovery URL uses a fragment, which is removed on import. Public invitations contain only the room code.

No WebSockets, additional database, paid service, client authoritative roll, production memory state, or change to approved game rules has been introduced.
