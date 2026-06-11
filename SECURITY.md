# Security Policy

Security is the whole point of Quenchworks, so we hold our own artifacts to the same bar we ask
you to.

## Verify before you trust

Every image is built by org CI and signed with cosign keyless (Sigstore). Verify it:

```bash
cosign verify ghcr.io/quenchworks/images/<app> \
  --certificate-identity-regexp 'https://github.com/quenchworks/.+' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
```

Inspect the SBOM and build provenance attached to the image:

```bash
cosign download sbom ghcr.io/quenchworks/images/<app>          # SPDX SBOM
cosign verify-attestation ghcr.io/quenchworks/images/<app> \
  --type slsaprovenance \
  --certificate-identity-regexp 'https://github.com/quenchworks/.+' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
```

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
