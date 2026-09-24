# SmarterBrain agent release trust

This public metadata repository is the independently maintained release trust channel for the SmarterBrain Ubuntu agent. Its fixed address is https://github.com/x-vibe/smarterbrain-agent-trust.

No native installer is currently qualified for customer installation. There is no current release card. A missing or expired card means fresh installation is unavailable; it must never be treated as permission to run an unsigned installer.

The accepted Ed25519 release root public key is [release-key.pub](release-key.pub), with fingerprint:

```
SHA256:396creISv40oxTauVqTOQ2TBDgtjGFe0zgYuJTtz7Vo
```

The planned stable card location is `stable/ubuntu-26.04-amd64/current.json`. Staging has a separate channel. A future qualified card will identify the exact platform, installer SHA-256 and byte length, current root version and trust epoch, sequence and validity interval. No installer URL supplied by a management backend can replace that authority.

Installer bytes will be distributed from the fixed content-addressed path `https://dl.smarterbrain.ai/native/sha256/{installer_sha256}/smarterbrain-installer`, with a detached SSH signature using namespace `smarterbrain-agent-bootstrap-v1`. These coordinates describe the release protocol; they are not an available download or installation instruction.

Customer verification must authenticate this maintainer identity independently, establish current UTC using authenticated time, validate the card and platform, and use the installed operating-system tools to check the public-key fingerprint, exact artifact hash and length, and SSH signature before executing any downloaded installer. The installer cannot authenticate its own first execution.

This repository contains public metadata only. It contains no private signing keys, deployment credentials, customer information, runtime binaries or private product source.
