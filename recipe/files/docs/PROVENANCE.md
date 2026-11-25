# Provenance — Miniflux (`2.3.5-CE-ubuntu24.04-r4`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/miniflux/v2
- Revision built: `2.3.5` (commit `faecfa2fac61a91f4f69550bb1afd506c4b51749`)
- Source tree: `0f56ee14b8860f3a29387d4aba9e2a3bc569f003173c77f7f8a352760ea5be21` over 676 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-go`; base image `scratch + a chiselled Ubuntu 24.04 runtime (vendored/chisel/slices.txt, packages.tsv)`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795161110` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/miniflux:2.3.5-CE-ubuntu24.04-r4` — index digest `sha256:ded09950105a1a6be04d64c82c00214f69e8c0173d9e7905e3bca5653a273465` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:d2b7bbf466fd39c1928fd8e609ddd9d757eae1d5a8285949834dbb8f92c7b98d` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/miniflux:2.3.5-CE-ubuntu24.04-r4`

## Pinned inputs, and why

- 29 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, dependency versions readystack sets 4, pins in the kit's dockerfiles 8, readystack's build engine 5, dependencies upstream chose 2, services the release checks run beside 3).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-miniflux-2.3.5-CE-ubuntu24.04-r4.trail.json`, published beside this archive and signed with the release key (`ReadyStack-miniflux-2.3.5-CE-ubuntu24.04-r4.trail.json.sigstore`), and readable at https://readystack.dev/products/miniflux/trail/2.3.5-CE-ubuntu24.04-r4.

