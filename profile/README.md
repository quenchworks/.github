<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo-dark.svg">
  <img alt="Quenchworks" src="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo.svg" width="460">
</picture>

### Hardened, 0-CVE Helm charts & container images — built from source, signed, and pinned by digest.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/quenchworks)
[![Built with Wolfi](https://img.shields.io/badge/built%20with-Wolfi%20%2F%20apko-1d2b3a.svg)](https://github.com/wolfi-dev)
[![Signed with cosign](https://img.shields.io/badge/signed-cosign%20keyless-0a0a0c.svg)](https://docs.sigstore.dev/)

[**Website**](https://quenchworks.mkabumattar.com) · [**Charts on ArtifactHub**](https://artifacthub.io/) · [**Images on GHCR**](https://github.com/orgs/quenchworks/packages)

</div>

---

## What is Quenchworks?

Quenchworks is an independent catalog of **hardened container images** and **clean-room Helm
charts** for the infrastructure you actually run — databases, caches, gateways, message queues.

Every image is **built from source** on [Wolfi](https://github.com/wolfi-dev) with
[melange](https://github.com/chainguard-dev/melange) + [apko](https://github.com/chainguard-dev/apko)
— no Dockerfiles, no upstream distro binaries, no vendor lineage. Each one is minimal, runs as
nonroot on a read-only root filesystem, ships an SBOM, is **signed with cosign**, and is
**rebuilt daily** so "0 CVEs" stays true tomorrow, not just on release day.

> _Quench_ — the metallurgy step that hardens hot metal by rapid cooling. That's the whole idea.

## Why it exists

The free, hardened images many teams relied on moved behind a paywall and a legacy registry.
Quenchworks rebuilds that capability **in the open, from source, for free** — and keeps it
honest with a daily rebuild loop and public provenance you can verify yourself.

## License

MIT. Built independently — not affiliated with any upstream distribution or vendor.

<div align="center">

---

**[quenchworks.mkabumattar.com](https://quenchworks.mkabumattar.com)** · made by [@mkabumattar](https://github.com/mkabumattar)

</div>
