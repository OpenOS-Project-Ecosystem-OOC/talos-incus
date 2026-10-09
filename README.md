[update-readmes]   Mode: rewrite — migrating to template structure...
# talos-incus

[![Built with Ona](https://ona.com/build-with-ona.svg)](https://app.ona.com/#https://github.com/Interested-Deving-1896/talos-incus) [![KDE Eco](https://img.shields.io/badge/KDE%20Eco-certified-brightgreen?logo=kde&logoColor=white&style=flat-square)](https://eco.kde.org/) [![Blue Angel](https://img.shields.io/badge/Blue%20Angel-DE--UZ%20215-0055a4?style=flat-square)](https://www.blauer-engel.de/en/certification/criteria)



<!-- AI:start:what-it-does -->
This project provides Talos Linux releases specifically packaged for use with Incus, a container and virtual machine manager. It automates workflows for building, deploying, and maintaining these releases, simplifying integration for developers and operators working with Talos Linux in Incus environments.
<!-- AI:end:what-it-does -->

## Architecture

<!-- AI:start:architecture -->
The project packages Talos Linux releases for Incus and automates related workflows. Key components include shell scripts for building and deploying releases, GitHub Actions workflows for CI/CD, and configuration files for managing Cloudflare Workers. The directory structure organizes scripts, templates, and metadata for streamlined automation. Workflows handle tasks such as multi-architecture builds (`build-multiple.yml`), deployment (`deploy-worker.yml`), repository mirroring (`mirror-osp-to-ooc.yaml`), and pull request updates (`rebase-prs.yml`).

```plaintext
.
├── .github/                 # GitHub Actions workflows
├── .gitignore               # Git ignore rules
├── LICENSE                  # Project license
├── README.md                # Project documentation
├── cloudflare-worker.js     # Cloudflare Worker script
├── scripts/                 # Helper scripts for build and deployment
├── wrangler.toml.template   # Template for Cloudflare Wrangler configuration
```
<!-- AI:end:architecture -->

## Install

<!-- Add installation instructions here. This section is yours — the AI will not modify it. -->

```bash
git clone https://github.com/Interested-Deving-1896/talos-incus.git
cd talos-incus
```

## Usage


```bash
# Use simplestreams remote (recommended)
incus remote add talos-incus https://images.interested-deving-1896.dev --protocol simplestreams
incus image list windsor:
incus launch windsor:talos/v1.12.0/amd64 my-instance
```

If you are using the Incus Terraform provider, you can add remotes in the `provider` block:

```
# Configure Incus provider with remotes for image pulls
provider "incus" {
  remote {
    name     = "talos-incus"
    address  = "https://images.interested-deving-1896.dev"
    protocol = "simplestreams"
    public   = true
  }
}

resource "incus_instance" "talos_controller" {
  name        = "talos-controller"
  description = "Talos control plane node"
  type        = "virtual-machine"
  image       = "talos-incus:talos/v1.12.0/arm64"
  ...
}
```

## Configuration

<!-- Document configuration options here. This section is yours — the AI will not modify it. -->

## CI

<!-- AI:start:ci -->
- **build-multiple.yml**: Builds Talos Linux images for multiple architectures. No secrets required.
- **deploy-worker.yml**: Deploys the `cloudflare-worker.js` script using Wrangler. Requires `CF_API_TOKEN` and `CF_ACCOUNT_ID` secrets.
- **mirror-osp-to-ooc.yaml**: Syncs Talos Linux releases from an upstream source to an output channel. Requires `GITHUB_TOKEN` secret.
- **rebase-prs.yml**: Automatically rebases open pull requests on the default branch. Requires `GITHUB_TOKEN` secret.
<!-- AI:end:ci -->

## Mirror chain

<!-- AI:start:mirror-chain -->
This repo is maintained in [`Interested-Deving-1896/talos-incus`](https://github.com/Interested-Deving-1896/talos-incus) and mirrored through:

```
Interested-Deving-1896/talos-incus  ──►  OpenOS-Project-OSP/talos-incus  ──►  OpenOS-Project-Ecosystem-OOC/talos-incus
```

Changes flow downstream automatically via the hourly mirror chain in
[`fork-sync-all`](https://github.com/Interested-Deving-1896/fork-sync-all).
Direct commits to OSP or OOC are detected and opened as PRs back to `Interested-Deving-1896`.
<!-- AI:end:mirror-chain -->

## Contributors

<!-- AI:start:contributors -->
| Contributor | Commits |
|---|---|
| [@Interested-Deving-1896](https://github.com/Interested-Deving-1896) | 184 |
| [@rmvangun](https://github.com/rmvangun) | 13 |
| [@renovate[bot]](https://github.com/apps/renovate) | 10 |
<!-- AI:end:contributors -->

## Origins

<!-- AI:start:origins -->
_Original project — no upstream influences recorded._
<!-- AI:end:origins -->

## Resources

<!-- AI:start:resources -->
_No additional resource files found._
<!-- AI:end:resources -->

## Accessibility

<!-- AI:start:accessibility -->
This repo uses automated accessibility auditing via `check-accessibility.yml`.

Checks include: CODEOWNERS ownership coverage, README screen-reader compatibility,
WCAG 2.1 AA HTML compliance, audio overview (espeak-ng), and Braille output (liblouis).




Run the [Check Accessibility](https://github.com/Interested-Deving-1896/talos-incus/actions/workflows/check-accessibility.yml)
workflow to generate the first report and accessibility artifacts.
See the [W3C Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/standards-guidelines/wcag/)
for the underlying accessibility reference.
<!-- AI:end:accessibility -->

## License

<!-- AI:start:license -->
[MPL-2.0](https://github.com/Interested-Deving-1896/talos-incus/blob/main/LICENSE) © 2026 [Interested-Deving-1896](https://github.com/Interested-Deving-1896)
<!-- AI:end:license -->
