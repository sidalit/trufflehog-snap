<div align="center">

<img src="snap/gui/trufflehog.png" alt="TruffleHog logo" width="128" />

# TruffleHog

**Find leaked credentials in your code and files.**

[![trufflehog](https://snapcraft.io/trufflehog/badge.svg)](https://snapcraft.io/trufflehog)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64 and arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [TruffleHog](https://github.com/trufflesecurity/trufflehog), a tool for finding and verifying secrets in repositories, files and cloud services.

</div>

---

## Getting Started

<a href="https://snapcraft.io/trufflehog"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install trufflehog
trufflehog
```

Scan files or Git history without contacting services to verify detected credentials:

```bash
trufflehog filesystem ~/projects/my-project --no-verification
trufflehog git "file://$HOME/projects/my-project" --no-verification
```

## Configure

There are no `snap set` options. Use `trufflehog --help` or the help for a scan subcommand. Supply credentials through its supported environment variables or files in an accessible directory.

| Optional access | Command |
| --- | --- |
| Files on removable storage | `sudo snap connect trufflehog:removable-media` |
| Existing SSH keys, configuration and known hosts | `sudo snap connect trufflehog:ssh-keys` |

For SSH hosts not already trusted, store newly accepted host keys in the snap's data directory:

```bash
GIT_SSH_COMMAND="ssh -o UserKnownHostsFile=$HOME/snap/trufflehog/common/known_hosts" \
  trufflehog git ssh://git@github.com/OWNER/REPOSITORY.git
```

## Limitations

- Scan files in normal home folders or connected removable storage. Hidden folders directly under your home and arbitrary system paths are restricted.
- Host cloud credentials, Git credential helpers and SSH agents are not imported automatically. SSH access to `~/.ssh` is read-only.
- Scanning the host Docker daemon is unavailable; scan registry images instead.
- Application updates are managed by snapd.

## Build

```bash
git clone https://github.com/sidalit/trufflehog-snap.git
cd trufflehog-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/trufflehog-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/trufflesecurity/trufflehog/issues).

## License

Snap packaging: [MIT](https://github.com/sidalit/trufflehog-snap/blob/main/LICENSE).
