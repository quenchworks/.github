# `.github`

**English** · [العربية](README.ar.md) · [Español](README.es.md)

Org-level defaults and community-health files for [QuenchWorks](https://github.com/quenchworks), the 0-CVE hardened replacement for the Bitnami catalog. This repo doesn't ship images or charts; it sets the house rules that apply across every repo in the org.

The hero you see at [github.com/quenchworks](https://github.com/quenchworks) lives in [`profile/README.md`](./profile/README.md). Everything else here is the boring-but-load-bearing stuff: how to report a vulnerability, how to propose an app, how we behave.

| Path | What it is |
|------|------------|
| [`profile/README.md`](./profile/README.md) | The org landing page rendered at [github.com/quenchworks](https://github.com/quenchworks) |
| [`profile/assets/`](./profile/assets/) | The iso-layered-cube mark and icons (light/dark) used by the profile |
| [`SECURITY.md`](./SECURITY.md) | Disclosure policy, plus how to verify our signatures and SBOMs yourself |
| [`CONTRIBUTING.md`](./CONTRIBUTING.md) | How to propose an app, file issues, and open PRs (including the clean-room rule) |
| [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md) | Contributor Covenant |
| [`ISSUE_TEMPLATE/`](./ISSUE_TEMPLATE/) | Org-default issue forms |

Files here apply to every repo in the org unless that repo overrides them.

## Where the actual catalog is

- **Images**: [quenchworks/images](https://github.com/quenchworks/images), the build factory.
- **Charts**: [quenchworks/charts](https://github.com/quenchworks/charts), the signed Helm charts.
- **Common**: [quenchworks/common](https://github.com/quenchworks/common), the `quench-common` library chart.
- **Website**: [quench-works.com](https://quench-works.com), browse the whole catalog.

> Brand note: the mark is the iso-layered cube, monochrome only. Don't recolor it or change the proportions.
