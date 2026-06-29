<div align="center">

[English](README.md) · [العربية](README.ar.md) · **Español**

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo-dark.svg">
  <img alt="QuenchWorks" src="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo.svg" width="460">
</picture>

# Imágenes de contenedor reforzadas y gratuitas y Helm charts firmados.

### Imágenes de contenedor con 0 CVE y Helm charts firmados. Compiladas desde el código fuente, firmadas con cosign, fijadas por digest. Gratuitas e independientes.

[![Images](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/images.json)](https://quench-works.com/images)
[![Charts](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/charts.json)](https://quench-works.com/charts)
[![Fixable CVEs](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/fixable.json)](https://quench-works.com/security)
[![Built with Wolfi](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/wolfi.json)](https://github.com/wolfi-dev)
[![Signed with cosign](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/cosign.json)](https://docs.sigstore.dev/)
[![Multi-arch](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/multiarch.json)](https://quench-works.com/images)
[![ArtifactHub](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/artifacthub.json)](https://artifacthub.io/packages/search?org=quenchworks)
[![License](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/license.json)](https://github.com/quenchworks)

[**Sitio web**](https://quench-works.com) · [**Charts**](https://quench-works.com/charts) · [**Imágenes**](https://quench-works.com/images) · [**Hoja de ruta**](https://quench-works.com/roadmap) · [**Documentación**](https://quench-works.com/docs) · [**ArtifactHub**](https://artifacthub.io/packages/search?org=quenchworks)

<p align="center">
  <a href="https://quench-works.com"><img src="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/demo.gif" alt="QuenchWorks en una terminal: ejecuta una imagen con 0 CVE, verifícala con cosign, despliega el Helm chart y observa cómo el pod llega a Running." width="760"></a>
</p>

</div>

---

## El catálogo se movió. Tu stack no.

Muchas plataformas se construyeron sobre imágenes gratuitas y reforzadas del catálogo de Bitnami. Esas imágenes se movieron detrás de un muro de pago y a un registro heredado, con el reloj corriendo. El trabajo que hacían no desapareció: aún necesitas una base de datos, una caché, una cola, una puerta de enlace, que arranque, se ejecute como nonroot y no arrastre un montón de CVE a tu clúster.

Reconstruir todo eso tú mismo es trabajo real, y mantenerlo en cero CVE es un trabajo que nunca para.

## QuenchWorks lo reconstruye, en abierto, gratis.

**90+ imágenes reforzadas** y **50+ Helm charts firmados** para la infraestructura que realmente ejecutas. Cada imagen se compila desde el código fuente sobre [Wolfi](https://github.com/wolfi-dev) con [melange](https://github.com/chainguard-dev/melange) y [apko](https://github.com/chainguard-dev/apko). Sin Dockerfiles, nada heredado de otra distro. Luego cada una:

- supera una estricta puerta de **0 CVE corregibles** (Trivy, fail-on-fixable) antes de poder publicarse,
- se ejecuta como **nonroot** en un **sistema de archivos raíz de solo lectura**,
- se distribuye como un índice **multi-arch** (linux/amd64 + linux/arm64),
- lleva un **SBOM** y una firma sin clave de **cosign**,
- se **reconstruye a diario**, para que un escaneo limpio siga siendo válido mañana en lugar de quedar obsoleto.

Cada chart fija su imagen estrictamente por digest `sha256` (una referencia solo por tag se rechaza a propósito), comparte una única base de seguridad reforzada a través del chart de biblioteca `quench-common`, está firmado con cosign y se distribuye en ArtifactHub como **verified publisher** con un esquema de Values.

> _Quench_ es el paso de la metalurgia que endurece el metal caliente enfriándolo rápido. La misma idea, menos CVE.

## 30 segundos hasta un Redis reforzado

```bash
# install the chart (the image is already signed and pinned by digest for you)
helm install cache oci://ghcr.io/quenchworks/charts/redis

# verify any image we ship, yourself (images are tagged by version, no :latest)
cosign verify ghcr.io/quenchworks/images/redis:8.8.0 \
  --certificate-identity-regexp 'https://github.com/quenchworks/.+' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
```

Sin cuenta, sin token, sin muro de pago. Cambia `redis:8.8.0` por cualquier aplicación y versión del catálogo.

## Qué hay en el catálogo

| | |
|---|---|
| **Relacional** | PostgreSQL · MariaDB · MySQL · CockroachDB |
| **Documental** | CouchDB · FerretDB · DocumentDB · MongoDB |
| **Clave-valor / caché** | Valkey · Redis · Memcached · Dragonfly |
| **Columna ancha** | Cassandra · ScyllaDB |
| **Búsqueda / vectorial** | OpenSearch · Solr · Meilisearch · Qdrant · Elasticsearch |
| **Streaming / mensajería** | Kafka · NATS · RabbitMQ · Pulsar |
| **Coordinación** | etcd · ZooKeeper · Temporal |
| **Observabilidad** | Prometheus · Grafana · Loki · Tempo · VictoriaMetrics · OpenTelemetry Collector · Vector · Fluent Bit |
| **Puertas de enlace / proxies** | Nginx · Caddy · Traefik · HAProxy |
| **Almacenamiento de objetos** | Garage · RustFS · SeaweedFS |
| **Secretos / identidad** | OpenBao · Keycloak |
| **Registro · Git · CI/IaC** | Harbor · Gitea · Atlantis |

Explóralo todo, con versiones, digests y procedencia, en [quench-works.com](https://quench-works.com).

## Los repositorios

| Repo | Qué es |
|------|------------|
| [**images**](https://github.com/quenchworks/images) | La fábrica de imágenes: compilaciones con melange + apko, la puerta de 0 CVE, firma con cosign, publicación en GHCR. |
| [**charts**](https://github.com/quenchworks/charts) | Helm charts de sala limpia, cada uno fijado a un digest de imagen firmado y publicado como artefacto OCI. |
| [**common**](https://github.com/quenchworks/common) | `quench-common`, el chart de biblioteca compartido: la base de seguridad reforzada y el resolvedor de imágenes solo por digest. |
| [**website**](https://github.com/quenchworks/website) | El sitio del catálogo, generado directamente desde los repositorios de imágenes y charts. |

## Honestos sobre las licencias

Encabezamos con la opción verdaderamente abierta en cada categoría. Dos almacenes de datos source-available, MongoDB y Elasticsearch (ambos SSPL-1.0), se incluyen con una nota de licencia bien visible porque **no** son código abierto aprobado por la OSI, y nombramos el fork limpio que cubre el hueco: OpenSearch para Elasticsearch, FerretDB más DocumentDB para MongoDB.

## Licencia

MIT. Construido de forma independiente. No afiliado a ninguna distribución o proveedor upstream.

<div align="center">

---

**[quench-works.com](https://quench-works.com)** · hecho por [@mkabumattar](https://github.com/mkabumattar)

</div>
