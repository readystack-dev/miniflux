# Miniflux: ReadyStack build kit

The offline build kit for the Docker image `readystack/miniflux:2.3.5-CE-ubuntu24.04-r4`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [2.3.5-CE-ubuntu24.04-r4](https://github.com/readystack-dev/miniflux/releases/tag/2.3.5-CE-ubuntu24.04-r4)
- Image: [`docker.io/readystack/miniflux:2.3.5-CE-ubuntu24.04-r4`](https://hub.docker.com/r/readystack/miniflux/tags), manifest digest `sha256:d2b7bbf466fd39c1928fd8e609ddd9d757eae1d5a8285949834dbb8f92c7b98d`
- Product page: https://readystack.dev/products/miniflux
- Source and build recipe: https://readystack.dev/products/miniflux/recipe
- Build trail: https://readystack.dev/products/miniflux/trail/2.3.5-CE-ubuntu24.04-r4
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=miniflux

## The image

ReadyStack Miniflux Community Edition build kit.

## Who uses Miniflux and why

Individuals and small teams who follow news, blogs and podcasts through feeds and want a simple self-hosted reader.

Miniflux is a minimalist, self-hosted feed reader designed for readability. It can fetch the full original article and removes pixel trackers and tracking parameters.

A typical use: A developer follows many blogs, release notes and news sites. Miniflux checks every feed, shows unread articles in a clean layout that works from the keyboard, fetches the full text when a feed carries only a summary, and strips trackers along the way.

From the upstream project's own description: https://github.com/miniflux/v2, https://miniflux.app/.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-20 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 7 packages with copyleft licences (GPL, LGPL, MPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`miniflux`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-20; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/miniflux.

Miniflux is distributed under its upstream licence (Apache-2.0); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [2.3.5-CE-ubuntu24.04-r4 release](https://github.com/readystack-dev/miniflux/releases/tag/2.3.5-CE-ubuntu24.04-r4): `ReadyStack-miniflux-2.3.5-CE-ubuntu24.04-r4.tar.gz` (434.5 MB), SHA-256 `c3f29ec9985a195509432ac4ef3f58ddea1245680f4064bd96120f78542e7b5f`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-miniflux-2.3.5-CE-ubuntu24.04-r4.rebuild.json.sigstore ReadyStack-miniflux-2.3.5-CE-ubuntu24.04-r4.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-miniflux-2.3.5-CE-ubuntu24.04-r4.tar.gz
cd 2.3.5-CE-ubuntu24.04-r4
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-miniflux-2.3.5-CE-ubuntu24.04-r4.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/miniflux/recipe. The complete kit is the release download. Each release is a tag here.

— ReadyStack · https://readystack.dev
