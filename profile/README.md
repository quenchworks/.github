<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo-dark.svg">
  <img alt="Quenchworks" src="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo.svg" width="460">
</picture>

### Hardened, 0-CVE Helm charts and container images. Built from source, signed, and pinned by digest.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/quenchworks)
[![Built with Wolfi](https://img.shields.io/badge/built%20with-Wolfi%20%2F%20apko-1d2b3a.svg)](https://github.com/wolfi-dev)
[![Signed with cosign](https://img.shields.io/badge/signed-cosign%20keyless-0a0a0c.svg)](https://docs.sigstore.dev/)

[**Website**](https://quenchworks.mkabumattar.com) · [**Charts on ArtifactHub**](https://artifacthub.io/) · [**Images on GHCR**](https://github.com/orgs/quenchworks/packages)

</div>

---

## What is Quenchworks?

Quenchworks is an independent catalog of hardened container images and clean-room Helm charts for
the infrastructure you actually run: databases, caches, gateways, and message queues.

We build every image from source on [Wolfi](https://github.com/wolfi-dev) with
[melange](https://github.com/chainguard-dev/melange) and
[apko](https://github.com/chainguard-dev/apko). No Dockerfiles, and nothing inherited from another
distro. Each one is small, runs as nonroot on a read-only filesystem, ships an SBOM, and is signed
with cosign. We rebuild daily, so "0 CVEs" stays true tomorrow and not just on release day.

> _Quench_ is the metallurgy step that hardens hot metal by cooling it fast. That is the idea.

## Why it exists

The free, hardened images many teams relied on moved behind a paywall and into a legacy registry.
Quenchworks rebuilds that in the open, from source, and for free, then keeps it honest with a daily
rebuild and public provenance you can check yourself.

## License

MIT. Built independently, and not affiliated with any upstream distribution or vendor.

<div align="center">

---

**[quenchworks.mkabumattar.com](https://quenchworks.mkabumattar.com)** · made by [@mkabumattar](https://github.com/mkabumattar)

</div>
