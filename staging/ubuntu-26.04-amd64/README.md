# Staging candidate: Ubuntu 26.04 amd64

This is an unqualified candidate for explicitly authorized staging acceptance. It is not a customer release. The ordinary `--install` path rejects candidate metadata. Existing installations must not use this first-install path.

The [current card](current.json) has sequence 11 and expires **2026-10-21 12:13:09 UTC**. Read it directly from this independently authenticated maintainer repository before proceeding. A missing, expired or changed card means stop. The stable channel remains unavailable.

## Before the first execution

Use a fresh Ubuntu 26.04 amd64 test host. Enter its root shell using your ordinary authenticated access (`sudo -i` where appropriate). The native image and its pathname must remain root-owned; running it from an ordinary user's home via sudo is not supported.

Establish authenticated time using the distribution's existing Chrony NTS configuration. Inspect the installed OS tools `chronyc -n sources`, `chronyc -n tracking`, `chronyc -n authdata`, and `chronyc -n ntpdata <selected numeric source>`. The selected source must match across those readings, use NTS with valid key/cookies, and show authenticated accepted NTP packets. Require normal leap status, a sample no older than 120 seconds, tracking error below five seconds and skew below 100 ppm. A selected plain NTP source, `NTPSynchronized=yes`, a saved timestamp or `date` alone is insufficient. If these conditions are not met, wait for authenticated convergence or repair the OS time service before continuing; do not execute this installer to authenticate its own first execution.

This time-readiness procedure and the complete candidate remain under native acceptance. The commands below use installed OS tools and fixed values from the independently read card. They do not execute downloaded verification code.

```sh
set -eu
test "$(id -u)" -eq 0
cd /root
umask 077
mkdir -m 700 sb-native-6a72a59bd46f5d6b85e21201fb06c5004594477793208e7f743c3ff3e5721e88
cd sb-native-6a72a59bd46f5d6b85e21201fb06c5004594477793208e7f743c3ff3e5721e88
test "$(uname -m)" = x86_64
test "$(. /etc/os-release; printf '%s:%s' "$ID" "$VERSION_ID")" = ubuntu:26.04
test "$(date -u +%s)" -ge 1792498389
test "$(date -u +%s)" -lt 1792584789
printf '%s\n' 'ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAXLjsBybAXAYqAhUJOl0vAKnT9+z9LFk2TFlHgni/c0' > release-key.pub
test "$(ssh-keygen -lf release-key.pub -E sha256 | cut -d ' ' -f 2)" = 'SHA256:396creISv40oxTauVqTOQ2TBDgtjGFe0zgYuJTtz7Vo'
curl --fail --proto '=https' --tlsv1.2 --max-time 120 --output smarterbrain-installer 'https://dl.smarterbrain.ai/native/sha256/6a72a59bd46f5d6b85e21201fb06c5004594477793208e7f743c3ff3e5721e88/smarterbrain-installer'
curl --fail --proto '=https' --tlsv1.2 --max-time 120 --output smarterbrain-installer.sig 'https://dl.smarterbrain.ai/native/sha256/6a72a59bd46f5d6b85e21201fb06c5004594477793208e7f743c3ff3e5721e88/smarterbrain-installer.sig'
test "$(wc -c < smarterbrain-installer)" -eq 9239544
printf '%s\n' '6a72a59bd46f5d6b85e21201fb06c5004594477793208e7f743c3ff3e5721e88  smarterbrain-installer' | sha256sum --check --strict -
printf '%s\n' 'smarterbrain-bootstrap namespaces="smarterbrain-agent-bootstrap-v1" ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAXLjsBybAXAYqAhUJOl0vAKnT9+z9LFk2TFlHgni/c0' > allowed-signers
ssh-keygen -Y verify -f allowed-signers -I smarterbrain-bootstrap -n smarterbrain-agent-bootstrap-v1 -s smarterbrain-installer.sig < smarterbrain-installer
test "$(date -u +%s)" -lt 1792584789

chmod 0500 smarterbrain-installer
./smarterbrain-installer --install-candidate
```

When prompted, paste the short-lived connection code from your own staging customer app. Do not supply a VPS password, SSH key or provider credential to the app. The code is read from standard input, not a command argument or environment variable.

On an interrupted attempt, retain its files and original installation directory. The supported same-transaction entrypoint is `./smarterbrain-installer --resume`; it retains the original candidate choice and enrollment identity. A refused or held attempt is not proof of successful recovery. Do not delete its state or mint repeated replacement codes to conceal an uncertain enrollment.

Initial installation selects this baseline through the absent-installation edge. Staging candidate updates require separate explicit root-local authorization; ordinary automatic updates continue to accept only qualified releases. No customer-qualified target or stable release is published. [Corresponding source](https://dl.smarterbrain.ai/native/sha256/776d9a6240e6505fd2a404fb039ac08296df344089521ae89ab816b0cb6b3b02/corresponding-source.tar.gz) accompanies the package, with its distribution notices and source manifest.

This build checks its current supported account tools, time profile and reporting tools before installation changes or connection-code input. It refuses missing or unsupported prerequisites; it does not install missing distribution packages. These checks do not establish fresh Hostinger qualification or complete customer setup.

This candidate retains the currently serving staging operation and receipt public keys. It has no update edge from an existing installation; matching keys does not establish installed qualification. Preserve all enrolled-host state, old keys and receipt archives. The existing dashboard operation pin already matches this candidate.

This candidate includes the fixed owner-only temporary lifecycle for generation-bound personal AI connection tests. Compiled-entry acceptance passed; installed owner cleanup, provider and Telegram replies still require actual staging acceptance.

This candidate targets the rebuilt Wave staging app and repairs private Ansible scratch storage. Compilation, Clippy, three focused regressions and independent artifact/source review passed. Full Devguard verification exceeded its fixed runner timeout; whole-suite completion, changed-line coverage and broken-control evidence remain incomplete. This release is for the explicitly authorized staging VM qualification only.

Sequence 10 fixes the transient time-helper namespace setting across systemd reload. The fixed capability and privilege restrictions still deny namespace operations: an isolated OVH probe denied 28 cases before and after reload. Installer recovery and customer acceptance remain unqualified. Full Devguard verification remains incomplete; this candidate is restricted to the authorized staging VM qualification.

Sequence 11 handles the global reload advisory only within the fixed transient helper, admitted enablement and authenticated reload. Ordinary persistent checks remain strict. The local lifecycle has one 180-second window, with a 45-second per-helper ceiling and bounded renewal/recovery supervision. Installer recovery and customer acceptance remain unqualified. Full Devguard verification remains incomplete; this candidate is restricted to authorized staging VM qualification.
