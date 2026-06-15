# Security Policy

Security is the whole point of Quenchworks, so we hold our own artifacts to the same bar we ask
you to.

## Verify before you trust

Every image is built by org CI and signed with cosign keyless (Sigstore). Images are tagged by
version (there is no `:latest`), so verify a version tag. Swap `redis:8.8.0` for any image and the
version shown on its page:

```bash
cosign verify ghcr.io/quenchworks/images/redis:8.8.0 \
  --certificate-identity-regexp 'https://github.com/quenchworks/.+' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
```

Each image also carries an SPDX SBOM and a SLSA build-provenance attestation on the same digest, as
Sigstore-signed OCI referrers. List them with `cosign tree`, and verify them with the GitHub CLI
(the version tag resolves to the current attested digest):

```bash
cosign tree ghcr.io/quenchworks/images/redis:8.8.0   # signature + attestations

# build provenance (SLSA): which workflow built it, from what
gh attestation verify oci://ghcr.io/quenchworks/images/redis:8.8.0 \
  --owner quenchworks

# SPDX SBOM: the package inventory
gh attestation verify oci://ghcr.io/quenchworks/images/redis:8.8.0 \
  --owner quenchworks \
  --predicate-type https://spdx.dev/Document
```

See the [SBOM & provenance guide](https://quenchworks.mkabumattar.com/docs/sbom) for reading the
SBOM document itself and using these checks in CI.

Charts are pinned to images by `sha256` digest, never a mutable tag, so what you install is
exactly the artifact that passed the scan-and-sign gate.

## What "0-CVE" means

The CI gate runs Trivy with `--exit-code 1 --ignore-unfixed`, so a build fails on any fixable CVE.
That is what "0-CVE" means here: zero fixable CVEs. Unfixable upstream CVEs, where no patch exists
yet, cannot be removed, and where it matters we publish notes or VEX. Images are rebuilt and
rescanned daily, because a clean scan only describes the day it ran.

## Reporting a vulnerability

If you find a vulnerability in a Quenchworks image, chart, or pipeline:

- **Preferred:** open a [private security advisory](https://github.com/quenchworks/images/security/advisories/new)
  on the relevant repo (GitHub → Security → Report a vulnerability).
- **Or email:** `quenchworks@mkabumattar.com` with details and reproduction steps.

Please do not open a public issue for an undisclosed vulnerability. We try to acknowledge within
72 hours and will work out a fix and disclosure timeline with you.

## Supported versions

Quenchworks rebuilds the current supported version of each cataloged app daily. Older pinned
digests remain available but only the latest green build receives security rebuilds.
