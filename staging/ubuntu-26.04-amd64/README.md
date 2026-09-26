# Staging candidate: Ubuntu 26.04 amd64

This is an unqualified candidate for explicitly authorized staging acceptance. It is not a customer release. The ordinary `--install` path rejects candidate metadata. Existing installations must not use this first-install path.

The [current card](current.json) has sequence 5 and expires **2026-09-27 18:43:51 UTC**. Read it directly from this independently authenticated maintainer repository before proceeding. A missing, expired or changed card means stop. The stable channel remains unavailable.

## Before the first execution

Use a fresh Ubuntu 26.04 amd64 test host. Enter its root shell using your ordinary authenticated access (`sudo -i` where appropriate). The native image and its pathname must remain root-owned; running it from an ordinary user's home via sudo is not supported.

Establish authenticated time using the distribution's existing Chrony NTS configuration. Inspect the installed OS tools `chronyc -n sources`, `chronyc -n tracking`, `chronyc -n authdata`, and `chronyc -n ntpdata <selected numeric source>`. The selected source must match across those readings, use NTS with valid key/cookies, and show authenticated accepted NTP packets. Require normal leap status, a sample no older than 120 seconds, tracking error below five seconds and skew below 100 ppm. A selected plain NTP source, `NTPSynchronized=yes`, a saved timestamp or `date` alone is insufficient. If these conditions are not met, wait for authenticated convergence or repair the OS time service before continuing; do not execute this installer to authenticate its own first execution.

This time-readiness procedure and the complete candidate remain under native acceptance. The commands below use installed OS tools and fixed values from the independently read card. They do not execute downloaded verification code.

```sh
set -eu
test "$(id -u)" -eq 0
cd /root
umask 077
mkdir -m 700 sb-native-ef1eed24b04407775174469cc83806ab95632a2817d803b25e9d721b810a67e9
cd sb-native-ef1eed24b04407775174469cc83806ab95632a2817d803b25e9d721b810a67e9
test "$(uname -m)" = x86_64
test "$(. /etc/os-release; printf '%s:%s' "$ID" "$VERSION_ID")" = ubuntu:26.04
test "$(date -u +%s)" -ge 1790448231
test "$(date -u +%s)" -lt 1790534631
printf '%s\n' 'ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAXLjsBybAXAYqAhUJOl0vAKnT9+z9LFk2TFlHgni/c0' > release-key.pub
test "$(ssh-keygen -lf release-key.pub -E sha256 | cut -d ' ' -f 2)" = 'SHA256:396creISv40oxTauVqTOQ2TBDgtjGFe0zgYuJTtz7Vo'
curl --fail --proto '=https' --tlsv1.2 --max-time 120 --output smarterbrain-installer 'https://dl.smarterbrain.ai/native/sha256/ef1eed24b04407775174469cc83806ab95632a2817d803b25e9d721b810a67e9/smarterbrain-installer'
curl --fail --proto '=https' --tlsv1.2 --max-time 120 --output smarterbrain-installer.sig 'https://dl.smarterbrain.ai/native/sha256/ef1eed24b04407775174469cc83806ab95632a2817d803b25e9d721b810a67e9/smarterbrain-installer.sig'
test "$(wc -c < smarterbrain-installer)" -eq 6593808
printf '%s\n' 'ef1eed24b04407775174469cc83806ab95632a2817d803b25e9d721b810a67e9  smarterbrain-installer' | sha256sum --check --strict -
printf '%s\n' 'smarterbrain-bootstrap namespaces="smarterbrain-agent-bootstrap-v1" ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAXLjsBybAXAYqAhUJOl0vAKnT9+z9LFk2TFlHgni/c0' > allowed-signers
ssh-keygen -Y verify -f allowed-signers -I smarterbrain-bootstrap -n smarterbrain-agent-bootstrap-v1 -s smarterbrain-installer.sig < smarterbrain-installer
test "$(date -u +%s)" -lt 1790534631

chmod 0500 smarterbrain-installer
./smarterbrain-installer --install-candidate
```

When prompted, paste the short-lived connection code from your own staging customer app. Do not supply a VPS password, SSH key or provider credential to the app. The code is read from standard input, not a command argument or environment variable.

On an interrupted attempt, retain its files and original installation directory. The supported same-transaction entrypoint is `./smarterbrain-installer --resume`; it retains the original candidate choice and enrollment identity. A refused or held attempt is not proof of successful recovery. Do not delete its state or mint repeated replacement codes to conceal an uncertain enrollment.

Initial installation selects this baseline through the absent-installation edge. Staging candidate updates require separate explicit root-local authorization; ordinary automatic updates continue to accept only qualified releases. No customer-qualified target or stable release is published. [Corresponding source](https://dl.smarterbrain.ai/native/sha256/696b48f0d825a31e18901d38a5935bb715fb253c0c881d5e77b0256409dc9a61/corresponding-source.tar.gz) accompanies the package, with its distribution notices and source manifest.
