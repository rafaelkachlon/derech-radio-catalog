# Derech Radio station catalog

Public station metadata for רדיו דרך. This repository contains only the catalog and its documentation. It does not contain application source, APKs, signing keys, credentials, user favorites, or listening history.

## Live catalog

https://raw.githubusercontent.com/rafaelkachlon/derech-radio-catalog/main/stations.json

The application can refresh this HTTPS JSON without an APK rebuild after it has been configured with this endpoint. Existing older APKs are not automatically configured by publishing this repository.

## Format and maintenance

The document is `{ "schemaVersion": 1, "stations": [...] }`. Each station has a stable `id`, display `name`, `aliases`, `mark`, `color`, `streamUrl`, `format`, `website`, `source`, `verification`, and `lastChecked`.

- Keep station IDs unchanged when correcting a stream URL so local favorites continue to match.
- Use direct HTTPS broadcaster/CDN endpoints, never credentials or expiring personal/session tokens.
- Preserve source provenance. A directory-discovered endpoint must not be relabeled as official without evidence.
- Update verification status and lastChecked only after actually checking the endpoint. An edit or successful JSON download alone is not an audio test.
- Keep schemaVersion 1, 1–500 stations and the complete UTF-8 document under 262144 bytes. IDs must be unique and match `[a-z0-9][a-z0-9_-]{0,79}`. Names must be nonempty and at most 150 characters. Aliases: at most 50 strings, each at most 150 characters. streamUrl must be HTTPS with a host, no username/password, and at most 4096 characters.
- Validate JSON and compare IDs before committing; verify the public raw URL afterward. Revert the relevant commit to roll back an incorrect edit.
- Clients should retain the last valid cached catalog and bundled fallback; a failed download or invalid document must not erase favorites or disable listening. Refreshes must be bounded, not loops on every playback error.

## Coverage and verification

Initial snapshot: 16 November 2026, 106 listening entries. This includes multiple themed channels from the same broadcaster and is **not** 106 independent radio broadcasters or a claim of complete Israeli coverage.

The per-entry verification and lastChecked fields are preserved from the source catalog. Some entries were HTTP/codec checked; others also had a short audio decode. These checks are historical observations, not guarantees of current availability, geographic availability, or in-car compatibility. Directory-sourced entries are marked in their verification values. Educational/community and other coverage gaps may remain.

ECO99 uses `https://eco01.livecdn.biz/ecolive/99fm_aac/icecast.audio`; the previous endpoint redirected through HTTP. The replacement was checked for HTTP 200, AAC-LC 48 kHz stereo and a short decode on 16 November 2026. Its stable ID remains `eco99`.

No audio is hosted, recorded or relayed here. Station names and stream endpoints identify third-party services. A publicly reachable endpoint is not a grant of redistribution, trademark or commercial-use rights. Broadcasters retain their rights and their audio may include advertising. No third-party logo artwork is included in this snapshot.
