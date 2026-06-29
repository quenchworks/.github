<div align="center">

[English](README.md) · **العربية** · [Español](README.es.md)

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo-dark.svg">
  <img alt="QuenchWorks" src="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/logo.svg" width="460">
</picture>

# صور حاويات مُحصَّنة ومجانية ومخططات Helm موقَّعة.

### صور حاويات بصفر ثغرات (0-CVE) ومخططات Helm موقَّعة. مبنية من المصدر، موقَّعة بـ cosign، ومثبَّتة بالبصمة الرقمية (digest). مجانية ومستقلة.

[![Images](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/images.json)](https://quench-works.com/images)
[![Charts](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/charts.json)](https://quench-works.com/charts)
[![Fixable CVEs](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/fixable.json)](https://quench-works.com/security)
[![Built with Wolfi](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/wolfi.json)](https://github.com/wolfi-dev)
[![Signed with cosign](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/cosign.json)](https://docs.sigstore.dev/)
[![Multi-arch](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/multiarch.json)](https://quench-works.com/images)
[![ArtifactHub](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/artifacthub.json)](https://artifacthub.io/packages/search?org=quenchworks)
[![License](https://img.shields.io/endpoint?url=https://quench-works.com/api/v1/badge/license.json)](https://github.com/quenchworks)

[**الموقع**](https://quench-works.com) · [**المخططات**](https://quench-works.com/charts) · [**الصور**](https://quench-works.com/images) · [**خارطة الطريق**](https://quench-works.com/roadmap) · [**التوثيق**](https://quench-works.com/docs) · [**ArtifactHub**](https://artifacthub.io/packages/search?org=quenchworks)

<p align="center">
  <a href="https://quench-works.com"><img src="https://raw.githubusercontent.com/quenchworks/.github/main/profile/assets/demo.gif" alt="QuenchWorks في طرفية: شغّل صورة بصفر ثغرات (0-CVE)، تحقّق منها باستخدام cosign، انشر مخطط Helm، وراقب الجراب (pod) حتى يصل إلى حالة Running." width="760"></a>
</p>

</div>

---

## الكتالوج انتقل. حزمتك التقنية لم تنتقل.

بُنيت الكثير من المنصّات على صور مجانية ومُحصَّنة من كتالوج Bitnami. تلك الصور انتقلت خلف جدار دفع وإلى سجلّ قديم (legacy registry)، وعلى مؤقّت زمني. المهمّة التي كانت تؤدّيها لم تختفِ: ما زلت بحاجة إلى قاعدة بيانات، وذاكرة تخزين مؤقّت (cache)، وطابور (queue)، وبوّابة (gateway)، تُقلِع، وتعمل بدون صلاحيات الجذر (nonroot)، ولا تجرّ كومة من الثغرات (CVEs) إلى عنقودك (cluster).

إعادة بناء كل ذلك بنفسك عمل حقيقي، والحفاظ عليه عند صفر ثغرات (CVEs) عمل لا يتوقّف أبدًا.

## QuenchWorks يعيد بناءه، بشكل مفتوح، ومجانًا.

**90+ صورة مُحصَّنة** و**50+ مخطط Helm موقَّع** للبنية التحتية التي تشغّلها فعليًا. كل صورة مبنية من المصدر على [Wolfi](https://github.com/wolfi-dev) باستخدام [melange](https://github.com/chainguard-dev/melange) و[apko](https://github.com/chainguard-dev/apko). لا ملفات Dockerfile، ولا شيء موروث من توزيعة أخرى. ثم كل واحدة منها:

- تجتاز بوّابة صارمة بـ **0 ثغرات قابلة للإصلاح (0 fixable CVE)** (Trivy، مع الفشل عند القابلة للإصلاح) قبل أن تتمكّن من النشر،
- تعمل **بدون صلاحيات الجذر (nonroot)** على **نظام ملفات جذر للقراءة فقط (read-only root filesystem)**،
- تُشحن كفهرس **متعدّد المعماريات (multi-arch)** (linux/amd64 + linux/arm64)،
- تحمل **SBOM** وتوقيع **cosign** بدون مفاتيح (keyless)،
- **يُعاد بناؤها يوميًا**، فيبقى الفحص النظيف صحيحًا غدًا بدلًا من أن يتقادم.

كل مخطط يثبّت صورته بصرامة عبر البصمة الرقمية `sha256` (يُرفض المرجع المعتمد على الوسم فقط عن قصد)، ويتشارك خط أساس أمني مُحصَّن واحد عبر مخطّط مكتبة `quench-common`، وموقَّع بـ cosign، ويُشحن على ArtifactHub كـ **ناشر موثَّق (verified publisher)** مع مخطط قيم (Values schema).

> _Quench_ هي خطوة المعالجة المعدنية التي تُصلّب المعدن الساخن عبر تبريده بسرعة. الفكرة نفسها، مع ثغرات (CVEs) أقل.

## 30 ثانية للوصول إلى Redis مُحصَّن

```bash
# install the chart (the image is already signed and pinned by digest for you)
helm install cache oci://ghcr.io/quenchworks/charts/redis

# verify any image we ship, yourself (images are tagged by version, no :latest)
cosign verify ghcr.io/quenchworks/images/redis:8.8.0 \
  --certificate-identity-regexp 'https://github.com/quenchworks/.+' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
```

لا حساب، ولا رمز (token)، ولا جدار دفع. استبدل `redis:8.8.0` بأي تطبيق وإصدار في الكتالوج.

## ما الموجود في الكتالوج

| | |
|---|---|
| **علائقية** | PostgreSQL · MariaDB · MySQL · CockroachDB |
| **مستندية** | CouchDB · FerretDB · DocumentDB · MongoDB |
| **مفتاح-قيمة / تخزين مؤقت** | Valkey · Redis · Memcached · Dragonfly |
| **عمودية عريضة** | Cassandra · ScyllaDB |
| **بحث / متّجهات** | OpenSearch · Solr · Meilisearch · Qdrant · Elasticsearch |
| **بثّ / مراسلة** | Kafka · NATS · RabbitMQ · Pulsar |
| **تنسيق** | etcd · ZooKeeper · Temporal |
| **قابلية الملاحظة** | Prometheus · Grafana · Loki · Tempo · VictoriaMetrics · OpenTelemetry Collector · Vector · Fluent Bit |
| **بوّابات / وكلاء** | Nginx · Caddy · Traefik · HAProxy |
| **تخزين كائنات** | Garage · RustFS · SeaweedFS |
| **أسرار / هوية** | OpenBao · Keycloak |
| **سجلّ · Git · CI/IaC** | Harbor · Gitea · Atlantis |

تصفّح كل ذلك، مع الإصدارات والبصمات الرقمية (digests) والمصدر (provenance)، على [quench-works.com](https://quench-works.com).

## المستودعات

| المستودع | ما هو |
|------|------------|
| [**images**](https://github.com/quenchworks/images) | مصنع الصور: عمليات بناء melange + apko، وبوّابة صفر ثغرات (0-CVE)، وتوقيع cosign، والنشر على GHCR. |
| [**charts**](https://github.com/quenchworks/charts) | مخططات Helm من الغرفة النظيفة، كل واحدة مثبَّتة على بصمة رقمية لصورة موقَّعة ومنشورة كأداة OCI. |
| [**common**](https://github.com/quenchworks/common) | `quench-common`، مخطّط المكتبة المشترك: خط الأساس الأمني المُحصَّن ومُحلِّل الصور المعتمد على البصمة الرقمية فقط. |
| [**website**](https://github.com/quenchworks/website) | موقع الكتالوج، مُولَّد مباشرة من مستودعَي الصور والمخططات. |

## صادقون بشأن الترخيص

نتصدّر بالخيار المفتوح حقًا في كل فئة. قاعدتا بيانات متاحتان من حيث المصدر (source-available)، هما MongoDB وElasticsearch (كلاهما SSPL-1.0)، تُحمَلان مع ملاحظة ترخيص واضحة لأنهما **ليستا** برمجيات مفتوحة المصدر معتمدة من OSI، ونسمّي الفرع النظيف الذي يغطّي المكان: OpenSearch لـ Elasticsearch، وFerretDB إضافة إلى DocumentDB لـ MongoDB.

## الترخيص

MIT. مبني بشكل مستقل. غير مرتبط بأي توزيعة أو مورّد مُنبع (upstream).

<div align="center">

---

**[quench-works.com](https://quench-works.com)** · صُنع بواسطة [@mkabumattar](https://github.com/mkabumattar)

</div>
