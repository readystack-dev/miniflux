[![ReadyStack](https://readystack.dev/logo.svg)](https://readystack.dev)

**Stable, Open-source Releases, Automated** · [readystack.dev](https://readystack.dev)

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-readystack%2Fminiflux-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/readystack/miniflux) [![Docker pulls](https://img.shields.io/docker/pulls/readystack/miniflux)](https://hub.docker.com/r/readystack/miniflux) [![Grade at release](https://img.shields.io/badge/grade%20at%20release-A%20%2894%25%29-2ea44f)](https://readystack.dev/products/miniflux) [![Signed: cosign](https://img.shields.io/badge/signed-cosign-2ea44f)](https://readystack.dev/keys/cosign.pub) ![SBOM: SPDX](https://img.shields.io/badge/SBOM-SPDX-2ea44f) ![Provenance: SLSA v1](https://img.shields.io/badge/provenance-SLSA%20v1-2ea44f) ![Offline rebuild: verified](https://img.shields.io/badge/offline%20rebuild-verified-2ea44f)

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

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/miniflux/recipe. The complete kit is the release download. Each release is a tag here. How to report a vulnerability: [SECURITY.md](SECURITY.md).

## About ReadyStack

**Stable, Open-source Releases, Automated.** ReadyStack releases popular open-source apps every week with every available critical and high security fix applied, plus full documentation, reference data, tests and a build recipe that recreates each release bit-for-bit. Each release is rebuilt from its pinned inputs with the network off, checked against its published digest, signed, and scanned and graded again every day. The images and build kits are free, and ReadyStack is soon to be a nonprofit.

[readystack.dev](https://readystack.dev) · [All products](https://readystack.dev/products.html) · [Build kits on GitHub](https://github.com/readystack-dev) · [Defect log](https://readystack.dev/defects.html) · contact@readystack.dev

— ReadyStack · https://readystack.dev
