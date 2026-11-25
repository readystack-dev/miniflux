# Miniflux: ReadyStack build kit

The offline build kit for the Docker image `readystack/miniflux:2.3.5-CE-ubuntu24.04-r4`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [2.3.5-CE-ubuntu24.04-r4](https://github.com/readystack-dev/miniflux/releases/tag/2.3.5-CE-ubuntu24.04-r4)
- Image: [`docker.io/readystack/miniflux:2.3.5-CE-ubuntu24.04-r4`](https://hub.docker.com/r/readystack/miniflux/tags), manifest digest `sha256:d2b7bbf466fd39c1928fd8e609ddd9d757eae1d5a8285949834dbb8f92c7b98d`
- Product page: https://readystack.dev/products/miniflux
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=miniflux

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
