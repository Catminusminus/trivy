<div align="center">
<img src="docs/imgs/logo.png" width="200">

[![GitHub Release][release-img]][release]
[![Test][test-img]][test]
[![Go Report Card][go-report-img]][go-report]
[![License: Apache-2.0][license-img]][license]
[![GitHub Downloads][github-downloads-img]][release]
![Docker Pulls][docker-pulls]

[📖 Documentation][docs]
</div>

Trivy ([pronunciation][pronunciation]) is a comprehensive and versatile security scanner.
Trivy has *scanners* that look for security issues, and *targets* where it can find those issues.

Targets (what Trivy can scan):

- Container Image
- Filesystem
- Git Repository (remote)
- Virtual Machine Image
- Kubernetes
- AWS

Scanners (what Trivy can find there):

- OS packages and software dependencies in use (SBOM)
- Known vulnerabilities (CVEs)
- IaC issues and misconfigurations
- Sensitive information and secrets
- Software licenses

## Quick Start

### Get Trivy

Trivy is available in most common distribution methods. The full list of installation options is available in the [Installation] page, here are a few popular options:

- `apt-get install trivy`
- `yum install trivy`
- `brew install aquasecurity/trivy/trivy`
- `docker run aquasec/trivy`
- Download binary from <https://github.com/aquasecurity/trivy/releases/latest/>

Trivy is integrated with many popular platforms and applications. The full list of integrations is available in the [Ecosystem] page. Here are a few popular options:

- [GitHub Actions](https://github.com/aquasecurity/trivy-action)
- [CircleCI](https://circleci.com/developer/orbs/orb/fifteen5/trivy-orb)
- [Kubernetes operator](https://github.com/aquasecurity/trivy-operator)
- [VS Code plugin](https://github.com/aquasecurity/trivy-vscode-extension)

### General usage

```bash
trivy <target> [--security-checks <scanner1,scanner2>] <subject>
```

Examples:

```bash
trivy image python:3.4-alpine
```

<details>
<summary>Result</summary>

https://user-images.githubusercontent.com/1161307/171013513-95f18734-233d-45d3-aaf5-d6aec687db0e.mov

</details>

```bash
trivy fs --security-checks vuln,secret,config myproject/
```

<details>
<summary>Result</summary>

https://user-images.githubusercontent.com/1161307/171013917-b1f37810-f434-465c-b01a-22de036bd9b3.mov

</details>

```bash
trivy k8s --report summary cluster
```

<details>
<summary>Result</summary>

![k8s summary](docs/imgs/trivy-k8s.png)

</details>

## Highlights

- Comprehensive vulnerability detection
    - OS packages (Alpine Linux, Red Hat Universal Base Image, Red Hat Enterprise Linux, CentOS, AlmaLinux, Rocky Linux, CBL-Mariner, Oracle Linux, Debian, Ubuntu, Amazon Linux, openSUSE Leap, SUSE Enterprise Linux, Photon OS and Distroless)
    - **Language-specific packages** (Bundler, Composer, Pipenv, Poetry, npm, yarn, Cargo, NuGet, Maven, and Go)
    - High accuracy, especially [Alpine Linux][alpine] and RHEL/CentOS
- Supply chain security (SBOM support)
    - Support CycloneDX
    - Support SPDX
    - Generating and Scanning SBOM
    - Leveraging in-toto attestations
    - Integrated with [Sigstore]
- Misconfiguration detection (IaC scanning) 
    - Wide variety of security checks are provided **out of the box**
    - Kubernetes, Docker, Terraform, and more
    - User-defined policies using [OPA Rego][rego]
- Secret detection
    - A wide variety of built-in rules are provided **out of the box**
    - User-defined patterns
    - Efficient scanning of container images
- Simple
    - Available in apt, yum, brew, dockerhub
    - **No pre-requisites** such as a database, system libraries, or eny environmental requirements. The binary runs anywhere.
    - The first scan will finish within 10 seconds (depending on your network). Consequent scans will finish instantaneously.
- Fits your workflow
    - **Great for CI** such as GitHub Actions, Jenkins, GitLab CI, etc.
    - Available as extension for IDEs such as vscode, jetbrains, vim
    - Available as extension for Docker Desktop, Rancher Desktop
    - See [Ecosystem] section in the documentation.

## FAQ

### How to pronounce the name "Trivy"?

`tri` is pronounced like **tri**gger, `vy` is pronounced like en**vy**.

---

Trivy is an [Aqua Security][aquasec] open source project.  
Learn about our open source work and portfolio [here][oss].  
Contact us about any matter by opening a GitHub Discussion [here][discussions]

[test]: https://github.com/aquasecurity/trivy/actions/workflows/test.yaml
[test-img]: https://github.com/aquasecurity/trivy/actions/workflows/test.yaml/badge.svg
[go-report]: https://goreportcard.com/report/github.com/aquasecurity/trivy
[go-report-img]: https://goreportcard.com/badge/github.com/aquasecurity/trivy
[release]: https://github.com/aquasecurity/trivy/releases
[release-img]: https://img.shields.io/github/release/aquasecurity/trivy.svg?logo=github
[github-downloads-img]: https://img.shields.io/github/downloads/aquasecurity/trivy/total?logo=github
[docker-pulls]: https://img.shields.io/docker/pulls/aquasec/trivy?logo=docker&label=docker%20pulls%20%2F%20trivy
[license]: https://github.com/aquasecurity/trivy/blob/main/LICENSE
[license-img]: https://img.shields.io/badge/License-Apache%202.0-blue.svg
[docs]: https://aquasecurity.github.io/trivy
[pronunciation]: #how-to-pronounce-the-name-trivy

[Installation]:https://aquasecurity.github.io/trivy/latest/getting-started/installation/
[Ecosystem]: https://aquasecurity.github.io/trivy/latest/ecosystem/

[alpine]: https://ariadne.space/2021/06/08/the-vulnerability-remediation-lifecycle-of-alpine-containers/
[rego]: https://www.openpolicyagent.org/docs/latest/#rego
[sigstore]: https://www.sigstore.dev/

[aquasec]: https://aquasec.com
[oss]: https://www.aquasec.com/products/open-source-projects/
[discussions]: https://github.com/aquasecurity/trivy/discussions
