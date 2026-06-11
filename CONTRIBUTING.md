# Contributing to Quenchworks

Thanks for helping build free, hardened, verifiable infrastructure images. 🛠️

## Ways to contribute

- **Request an app** — open an issue on [`images`](https://github.com/quenchworks/images/issues/new/choose)
  with the app, upstream source, version, and license. We tier it and queue it.
- **Report a bug** — a chart that won't render/install, an image that won't start, a failing scan.
- **Improve a chart or build** — PRs welcome on `images`, `charts`, and `common`.
- **Report a vulnerability** — see [SECURITY.md](./SECURITY.md) (do not open a public issue).

## The one hard rule: clean room

Quenchworks is **independent**. Charts must be authored from each application's **own upstream
documentation** — never copied or adapted from another vendor's charts (structure, values
schemas, or image layout). PRs that copy third-party chart implementations will be declined.
When you open a chart PR, note the upstream docs you worked from.

## Quality bar (what a PR must pass)

**Images**
- Built from source via melange on pinned Wolfi packages; source pinned by `expected-sha256`
- Trivy `--exit-code 1 --ignore-unfixed` is clean (scanned **before** publish)
- Nonroot, read-only rootfs, dropped caps, multi-arch (amd64 + arm64), SBOM emitted
- Correct SPDX license; a smoke test that boots the image and checks health

**Charts**
- Depends on the pinned `quench-common` library version
- Image referenced by `repository@sha256:digest` only (the helper rejects tags)
- `helm lint` + `helm template` clean; installs green in `kind`
- `artifacthub.io/*` annotations present (including the signing key)

## Workflow

1. Fork and branch from `main` (`feat/<app>`, `fix/<thing>`).
2. Keep commits focused; reference the issue ID.
3. Open a PR — CI runs the gates above. Green CI is required to merge.
4. Be kind and patient; see the [Code of Conduct](./CODE_OF_CONDUCT.md).

By contributing you agree your work is licensed under the project's MIT license.
