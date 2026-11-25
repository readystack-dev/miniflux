# GENERATED L-009 hermetic build (--network=none, SBOM+SLSA-attestation-producing).
# Pinned bases from BASE_IMAGE_DIGESTS.lock; vendored Go tree + debs from Dockerfile.vendor.
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_miniflux
WORKDIR /src
COPY vendored/miniflux-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161110
RUN go build -trimpath -ldflags='-s -w -X miniflux.app/v2/internal/version.Version=2.3.5 -X miniflux.app/v2/internal/version.Commit=faecfa2f' -o /miniflux . && /miniflux -version && \
    { readelf -lW /miniflux | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /miniflux | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /miniflux.needs
# rs-probe: the HEALTHCHECK helper (standard library only, from the kit's rs-probe.go)
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_rs_probe
WORKDIR /probe
COPY rs-probe.go main.go
COPY rs-probe.mod go.mod
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOFLAGS="-buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161110
RUN go build -trimpath -ldflags='-s -w' -o /rs-probe .
# the chiselled rootfs (vendored/chisel, cut by Dockerfile.vendor), the service user, the binaries
FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289 AS rootfs
ARG SOURCE_DATE_EPOCH=1795161110
ADD vendored/chisel/rootfs.tar /rootfs/
RUN printf 'miniflux:x:999:999::/var/lib/miniflux:/bin/sh\n' >> /rootfs/etc/passwd && printf 'miniflux:x:999:\n' >> /rootfs/etc/group && \
    mkdir -p /rootfs/var/lib/miniflux && chown -R 999:999 /rootfs/var/lib/miniflux
COPY --from=build_miniflux /miniflux /rootfs/usr/bin/miniflux
COPY --from=build_miniflux /miniflux.needs /tmp/needs/miniflux
COPY --from=build_rs_probe /rs-probe /rootfs/usr/local/bin/rs-probe
RUN chmod 755 /rootfs/usr/bin/miniflux /rootfs/usr/local/bin/rs-probe
RUN --mount=type=bind,source=vendored/chisel,target=/chisel set -eu; \
    for n in /tmp/needs/*; do while read -r lib; do [ -n "$lib" ] || continue; \
      case "$lib" in /*) [ -e "/rootfs$lib" ] ;; *) [ -n "$(find /rootfs/usr/lib /rootfs/usr/lib64 -name "$lib" 2>/dev/null | head -1)" ] ;; esac || \
      { echo "$(basename "$n") needs $lib, which the chiselled rootfs does not have: add its slice to runtime_base.slices" >&2; exit 1; }; \
    done < "$n"; done; rm -rf /tmp/needs; \
    [ -e /rootfs/etc/os-release ] || { echo "no /etc/os-release: base-files_release-info is missing" >&2; exit 1; }; \
    [ "$(grep -c '^Package: ' /rootfs/var/lib/dpkg/status)" = "$(wc -l < /chisel/packages.tsv)" ] || \
      { echo "/var/lib/dpkg/status does not list every package of vendored/chisel/packages.tsv" >&2; exit 1; }; \
    rm -rf /rootfs/var/log/dpkg.log /rootfs/var/log/alternatives.log /rootfs/var/log/apt /rootfs/var/cache/ldconfig/aux-cache /rootfs/var/cache/fontconfig
FROM scratch
ARG SOURCE_DATE_EPOCH=1795161110
COPY --from=rootfs /rootfs/ /
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin LISTEN_ADDR=0.0.0.0:8080 RUN_MIGRATIONS=1
LABEL org.opencontainers.image.licenses="Apache-2.0"
LABEL org.opencontainers.image.title="Miniflux"
LABEL org.opencontainers.image.source="https://github.com/miniflux/v2"
LABEL org.opencontainers.image.version="2.3.5-CE-ubuntu24.04-r4"
LABEL org.opencontainers.image.revision="faecfa2fac61a91f4f69550bb1afd506c4b51749"
HEALTHCHECK --interval=5s --timeout=30s --start-period=30s \
  CMD /usr/local/bin/rs-probe http://127.0.0.1:8080/healthcheck || exit 1
USER miniflux
EXPOSE 8080
ENTRYPOINT ["miniflux"]
