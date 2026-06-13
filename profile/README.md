<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo-dark.svg">
  <img alt="Quenchworks" src="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo.svg" width="460">
</picture>

### Hardened, 0-CVE Helm charts and container images. Built from source, signed, and pinned by digest.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/quenchworks)
[![Built with Wolfi](https://img.shields.io/badge/built%20with-Wolfi%20%2F%20apko-1d2b3a.svg)](https://github.com/wolfi-dev)
[![Signed with cosign](https://img.shields.io/badge/signed-cosign%20keyless-0a0a0c.svg)](https://docs.sigstore.dev/)
[![Pinned by digest](https://img.shields.io/badge/pinned-by%20digest-0a0a0c.svg)](https://quenchworks.mkabumattar.com/docs/pin-by-digest)

[**Website**](https://quenchworks.mkabumattar.com) · [**Charts**](https://quenchworks.mkabumattar.com/charts) · [**Images**](https://quenchworks.mkabumattar.com/images) · [**ArtifactHub**](https://artifacthub.io/packages/search?org=quenchworks) · [**GHCR**](https://github.com/orgs/quenchworks/packages)

</div>

---

## What is Quenchworks?

Quenchworks is an independent catalog of hardened container images and clean-room Helm charts for
the infrastructure you actually run: databases, caches, search, message queues, and coordination.

**28 datastores ship end to end today**, every image paired with a matching chart, across relational,
document, wide-column, key-value, search, time-series, analytical, graph, messaging, and coordination.
Browse them at [quenchworks.mkabumattar.com/charts](https://quenchworks.mkabumattar.com/charts).

Every image is built from source on [Wolfi](https://github.com/wolfi-dev) with
[melange](https://github.com/chainguard-dev/melange) and
[apko](https://github.com/chainguard-dev/apko). No Dockerfiles, and nothing inherited from another
distro. Each one:

- passes a hard **0 fixable CVE** gate (Trivy, fail-on-fixable) before it can publish,
- runs as **nonroot** on a **read-only root filesystem**,
- is **multi-arch** (linux/amd64 + linux/arm64),
- ships an **SBOM** and is **signed with cosign** (keyless),
- and is rebuilt **daily**, so "0 CVEs" stays true tomorrow and not just on release day.

Every chart pins its image strictly by `sha256` digest (a tag-only reference is refused on purpose),
shares one hardened security baseline through the `quench-common` library chart, is cosign-signed,
and is listed on ArtifactHub as a verified publisher with a Values schema.

> _Quench_ is the metallurgy step that hardens hot metal by cooling it fast. That is the idea.

## Why it exists

The free, hardened images many teams relied on moved behind a paywall and into a legacy registry.
Quenchworks rebuilds that in the open, from source, and for free: a drop-in hardened path off the
Bitnami catalog, kept honest with a daily rebuild and public provenance you can check yourself.

## The repositories

| Repo | What it is |
|------|------------|
| [**images**](https://github.com/quenchworks/images) | The image factory: melange + apko builds, the 0-CVE gate, cosign signing, GHCR publish. |
| [**charts**](https://github.com/quenchworks/charts) | Clean-room Helm charts, each pinned to a signed image digest and published as an OCI artifact. |
| [**common**](https://github.com/quenchworks/common) | `quench-common`, the shared library chart: hardened security contexts and the digest-only image resolver. |

## Verify anything we ship

```bash
cosign verify ghcr.io/quenchworks/images/postgresql \
  --certificate-identity-regexp 'https://github.com/quenchworks/.+' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
```

## A note on licensing

We lead with the truly-open option in every category. A few source-available datastores (MongoDB and
Elasticsearch under SSPL, CockroachDB and Dragonfly under BSL) are carried with a loud license note,
because they are **not** OSI-approved open source. Where a clean fork already covers the slot we say
so plainly: Valkey for Redis, OpenSearch for Elasticsearch, FerretDB and DocumentDB for MongoDB.

## License

MIT. Built independently, and not affiliated with any upstream distribution or vendor.

<div align="center">

---

**[quenchworks.mkabumattar.com](https://quenchworks.mkabumattar.com)** · made by [@mkabumattar](https://github.com/mkabumattar)

</div>
