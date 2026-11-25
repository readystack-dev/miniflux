# Miniflux 2.3.5 — ReadyStack release `2.3.5-CE-ubuntu24.04-r4`

Generated 2026-11-20 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/miniflux:2.3.5-CE-ubuntu24.04-r4` (linux/amd64). Index digest `sha256:ded09950105a1a6be04d64c82c00214f69e8c0173d9e7905e3bca5653a273465` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:d2b7bbf466fd39c1928fd8e609ddd9d757eae1d5a8285949834dbb8f92c7b98d` [`TARGET_DIGEST.txt`].
- **Upstream:** Miniflux 2.3.5 built from source at `2.3.5` of https://github.com/miniflux/v2 — upstream notes: https://github.com/miniflux/v2/releases/tag/2.3.5 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** none (`FROM scratch`): a chiselled Ubuntu 24.04 runtime, the files Canonical's chisel cut from Ubuntu's own packages (`vendored/chisel/slices.txt`, `vendored/chisel/packages.tsv`); runtime user `miniflux`.
- **Build:** `source-rebuild-go`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `2.3.5-CE-ubuntu24.04-r3`.

## What changed in this release

- Upstream version unchanged (2.3.5); ReadyStack rebuild.
- Minimum dependency versions ReadyStack enforces on top of upstream (raised only where upstream's own version was lower); shipped versions from the SBOM [`docs/sbom/SBOM.json`]:
  - `golang.org/x/net` at least `v0.60.0`: not raised, upstream already pins `v0.62.0` (shipped: `v0.62.0`)
  - `github.com/go-jose/go-jose/v4` at least `v4.1.6`: not raised, upstream already pins `v4.1.7` (shipped: `v4.1.7`)
- Miniflux 2.3.5 is unchanged from the release this supersedes (2.3.5-CE-ubuntu24.04-r3); this release rebuilds it. Changes: the image is rebuilt on the current ubuntu:24.04 image (sha256:9c7f200c07e3…), which its maintainers updated after 2.3.5-CE-ubuntu24.04-r3 was built on sha256:2198e4c65076…. Settings and ports are those of 2.3.5-CE-ubuntu24.04-r3 (this image keeps no data volume; all state is in PostgreSQL): replace the container with this image, keeping the same `DATABASE_URL`.

## Security status at release (measured 2026-11-20)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `miniflux` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/miniflux:2.3.5-CE-ubuntu24.04-r4` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:d2b7bbf466fd39c1928fd8e609ddd9d757eae1d5a8285949834dbb8f92c7b98d`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 6 of 6 use cases passed (6 authored) against the running image [`docs/validation/test-results.json`].

## Known issues

- None recorded.

## Defects fixed

- 8 problems found before release and fixed before it shipped (8 by review); each is listed in `docs/defects/defects.json`.

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/miniflux:2.3.5-CE-ubuntu24.04-r4
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

