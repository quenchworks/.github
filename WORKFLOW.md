# How QuenchWorks work flows

This page describes how an app gets into the catalog, how it stays patched, and where to watch
each step. Everything here runs in the public repos of the
[quenchworks](https://github.com/quenchworks) organization, and every step leaves a record you can
open: a ticket, a commit, a workflow run, a scan result.

## Where to look

| What you want to see | Where it is |
|---|---|
| What is being worked on now, what is next, what is held | The project board: [QuenchWorks work](https://github.com/orgs/quenchworks/projects/1) |
| One piece of work, its reasons and its history | The ticket (an issue in `images`, `charts` or `website`) |
| Every image build, gate and publish | [images Actions](https://github.com/quenchworks/images/actions) |
| Every chart install gate, release and signature | [charts Actions](https://github.com/quenchworks/charts/actions) |
| Open CVEs in every published image, scanned nightly | [Security report](https://quench-works.com/security) and [security.json](https://quench-works.com/api/v1/security.json) |
| What ships next and what is held, with dated notes | [Roadmap](https://quench-works.com/roadmap) |

## Tickets and the board

Every piece of work has one ticket, and every ticket is on the board.

Labels say what kind of work it is:

| Label | Meaning |
|---|---|
| `new-app` | A new image, or an image plus a chart, for the catalog |
| `cve` | An open CVE in a published image: it ends fixed, VEXed with evidence, or held |
| `held` | Blocked upstream. The ticket says why and when it is re-checked |
| `improvement` | A better gate, a chart feature, a smaller or safer image, a website feature |

The board's Status column says where it is:

| Status | Meaning |
|---|---|
| Todo | Queued. Roadmap rows marked `next` are at the top |
| In progress | A recipe or chart is being written or gated right now |
| Held | Waiting on upstream. The ticket carries the re-check date or condition |
| Done | Shipped and verified. The closing comment links the commits and runs |

A ticket closes only when its done condition holds: an app is live on GHCR, ArtifactHub, in the
catalog lock and on the website; a CVE shows 0 in the next nightly scan.

## Shipping a new app

1. **Pick.** Apps come from the roadmap: `next` rows first, then `planned` rows with a clean OSI
   license and no hold note. The ticket moves to In progress.
2. **Recipe** (`images/apps/<app>/`). `build.conf` (versions, source sha256, notes),
   `melange.yaml` (the build from source on Wolfi), `apko.yaml` (the image: nonroot uid 1001,
   multi-arch), `test.sh` (the smoke test, in Go under `tools/qw/internal/smoke`), a version
   checker row, and `.github/workflows/build-<app>.yml`.
3. **Local gate.** The image is built for real and scanned with Trivy in comprehensive mode. Any
   fixable CVE fails it. Then the smoke test boots the image read-only and exercises it (log in,
   write data, read it back, restart, read it again). Both have to pass.
4. **Image build** (`build-<app>.yml`). CI builds both arches on native runners, runs the same CVE
   gate and boot test, publishes to `ghcr.io/quenchworks/images`, signs with cosign (keyless), and
   attaches an SPDX SBOM and SLSA provenance.
5. **Chart** (`charts/quench/<app>/`), on the `quench-common` library, with the image pinned by
   digest. `release-<app>.yml` installs it in a kind cluster and runs a real check against the
   running app (for example: refuse a wrong password, upload a file, restart the pod, read the file
   back, repeat over TLS). Only then does it push the chart to `oci://ghcr.io/quenchworks/charts`,
   sign it and publish its ArtifactHub metadata.
6. **Catalog.** `images/catalog.lock.yaml` is regenerated (every published version and digest),
   then the website syncs from it and the app leaves the roadmap.

## Keeping images patched

| Workflow | When | What it does |
|---|---|---|
| `website/security-scan.yml` | Nightly, 01:00 UTC | Scans every published digest and publishes the results |
| `images/rebuild-drifted.yml` | Nightly, after the scan | Rebuilds images whose open CVEs a rebuild fixes |
| `images/drift-scan.yml` | Sundays | Re-scans what was clean when built |
| `images/recheck-blocked.yml` | Mondays | Re-gates every held app to see if upstream moved |
| `charts/check-pins.yml` | Daily and on push | Fails if a chart pins a superseded digest |
| `charts/on-image-published.yml` | After each image build | Re-pins the chart that uses the image |
| `website/docs-refs.yml` | On push | Fails if the docs name a tag or version that does not exist |

Every open CVE gets a `cve` ticket and ends one of three ways:

- **Fixed:** a version bump, a dependency floor, or a rebuild. Closed after the nightly scan
  shows 0.
- **VEXed:** the vulnerable code is provably not reachable, with file and line evidence, published
  in the VEX feed.
- **Held:** the fix does not exist upstream yet. The ticket carries the `held` label and a dated
  note saying what to re-check.

The site never says the images have zero CVEs. They are CVE-gated at build, and the open CVEs are
published.

## Rules every change follows

- The CVE gate is never weakened to make a build pass.
- Images are pinned by digest, never by tag.
- Every image runs as a nonroot user and is signed.
- Commits stage explicit paths and never force-push.
- Recipes are written from upstream sources and docs, independent of other catalogs.
