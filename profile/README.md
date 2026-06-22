<div align="center">

**English** · [العربية](README.ar.md) · [Español](README.es.md)

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo-dark.svg">
  <img alt="QuenchWorks" src="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo.svg" width="460">
</picture>

# Free, hardened container images and signed Helm charts.

### 0-CVE container images and signed Helm charts. Built from source, cosign-signed, pinned by digest. Free and independent.

[![Images](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fquench-works.com%2Fapi%2Fv1%2Fimages.json&query=%24.total&label=images&suffix=%20hardened&color=0a0a0c)](https://quench-works.com/images)
[![Charts](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fquench-works.com%2Fapi%2Fv1%2Fcharts.json&query=%24.total&label=charts&suffix=%20signed&color=0a0a0c)](https://quench-works.com/charts)
[![Fixable CVEs](https://img.shields.io/badge/fixable%20CVEs-0-1d2b3a.svg)](https://quench-works.com/security)
[![Built with Wolfi](https://img.shields.io/badge/built%20from%20source-Wolfi%20%2F%20apko-1d2b3a.svg)](https://github.com/wolfi-dev)
[![Signed with cosign](https://img.shields.io/badge/signed-cosign%20keyless-0a0a0c.svg)](https://docs.sigstore.dev/)
[![Multi-arch](https://img.shields.io/badge/arch-amd64%20%2B%20arm64-0a0a0c.svg)](https://quench-works.com/images)
[![ArtifactHub](https://img.shields.io/badge/ArtifactHub-verified%20publisher-417598.svg)](https://artifacthub.io/packages/search?org=quenchworks)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/quenchworks)

[**Website**](https://quench-works.com) · [**Charts**](https://quench-works.com/charts) · [**Images**](https://quench-works.com/images) · [**Roadmap**](https://quench-works.com/roadmap) · [**Docs**](https://quench-works.com/docs) · [**ArtifactHub**](https://artifacthub.io/packages/search?org=quenchworks)

<p align="center">
  <a href="https://quench-works.com"><img src="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/demo.gif" alt="QuenchWorks in a terminal: run a 0-CVE image, verify it with cosign, deploy the Helm chart, and watch the pod reach Running." width="760"></a>
</p>

</div>

---

## The catalog moved. Your stack didn't.

A lot of platforms were built on free, hardened images from the Bitnami catalog. Those images moved behind a paywall and into a legacy registry, on a clock. The job they did didn't go away: you still need a database, a cache, a queue, a gateway, that boots, runs nonroot, and doesn't drag a pile of CVEs into your cluster.

Rebuilding all of that yourself is real work, and keeping it at zero CVEs is work that never stops.

## QuenchWorks rebuilds it, in the open, for free.

**92 hardened images** and **54 signed Helm charts** for the infrastructure you actually run. Every image is built from source on [Wolfi](https://github.com/wolfi-dev) with [melange](https://github.com/chainguard-dev/melange) and [apko](https://github.com/chainguard-dev/apko). No Dockerfiles, nothing inherited from another distro. Then each one:

- clears a hard **0 fixable CVE** gate (Trivy, fail-on-fixable) before it can publish,
- runs **nonroot** on a **read-only root filesystem**,
- ships as a **multi-arch** index (linux/amd64 + linux/arm64),
- carries an **SBOM** and a **cosign** keyless signature,
- is **rebuilt daily**, so a clean scan stays true tomorrow instead of aging out.

Every chart pins its image strictly by `sha256` digest (a tag-only reference is refused on purpose), shares one hardened security baseline through the `quench-common` library chart, is cosign-signed, and ships on ArtifactHub as a **verified publisher** with a Values schema.

> _Quench_ is the metallurgy step that hardens hot metal by cooling it fast. Same idea, fewer CVEs.

## 30 seconds to a hardened Redis

```bash
# install the chart (the image is already signed and pinned by digest for you)
helm install cache oci://ghcr.io/quenchworks/charts/redis

# verify any image we ship, yourself (images are tagged by version, no :latest)
cosign verify ghcr.io/quenchworks/images/redis:8.8.0 \
  --certificate-identity-regexp 'https://github.com/quenchworks/.+' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
```

No account, no token, no paywall. Swap `redis:8.8.0` for any app and version in the catalog.

## What's in the catalog

| | |
|---|---|
| **Relational** | PostgreSQL · MariaDB · MySQL · CockroachDB |
| **Document** | CouchDB · FerretDB · DocumentDB · MongoDB |
| **Key-value / cache** | Valkey · Redis · Memcached · Dragonfly |
| **Wide-column** | Cassandra · ScyllaDB |
| **Search / vector** | OpenSearch · Solr · Meilisearch · Qdrant · Elasticsearch |
| **Streaming / messaging** | Kafka · NATS · RabbitMQ · Pulsar |
| **Coordination** | etcd · ZooKeeper · Temporal |
| **Observability** | Prometheus · Grafana · Loki · Tempo · VictoriaMetrics · OpenTelemetry Collector · Vector · Fluent Bit |
| **Gateways / proxies** | Nginx · Caddy · Traefik · HAProxy |
| **Object storage** | Garage · RustFS · SeaweedFS |
| **Secrets / identity** | OpenBao · Keycloak |
| **Registry · Git · CI/IaC** | Harbor · Gitea · Atlantis |

Browse all of it, with versions, digests, and provenance, at [quench-works.com](https://quench-works.com).

## The repositories

| Repo | What it is |
|------|------------|
| [**images**](https://github.com/quenchworks/images) | The image factory: melange + apko builds, the 0-CVE gate, cosign signing, GHCR publish. |
| [**charts**](https://github.com/quenchworks/charts) | Clean-room Helm charts, each pinned to a signed image digest and published as an OCI artifact. |
| [**common**](https://github.com/quenchworks/common) | `quench-common`, the shared library chart: the hardened security baseline and the digest-only image resolver. |
| [**website**](https://github.com/quenchworks/website) | The catalog site, generated straight from the images and charts repos. |

## Honest about licensing

We lead with the truly-open option in every category. Two source-available datastores, MongoDB and Elasticsearch (both SSPL-1.0), are carried with a loud license note because they are **not** OSI-approved open source, and we name the clean fork that covers the slot: OpenSearch for Elasticsearch, FerretDB plus DocumentDB for MongoDB.

## License

MIT. Built independently. Not affiliated with any upstream distribution or vendor.

<div align="center">

---

**[quench-works.com](https://quench-works.com)** · made by [@mkabumattar](https://github.com/mkabumattar)

</div>
