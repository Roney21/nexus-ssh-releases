# Security & Privacy

Nexus.ssh handles SSH keys, passwords, and credentials for servers you
manage — this page documents exactly how that data is protected and what,
if anything, ever leaves your machine. No software can honestly claim to be
"100% secure" (that also means no known vulnerabilities, ever, forever), but
every claim below is a concrete, checkable fact about how the app is built,
not a marketing statement.

## Your data never leaves your machine, except where you tell it to

Nexus.ssh has no backend server of its own and no account/login system.
There is no cloud sync. The only network connections the app makes are:

| Connection | When it happens | What it sends |
|---|---|---|
| SSH / SFTP / RDP | Only when you connect to a host you configured | Standard protocol traffic to *that* host — nothing else, nowhere else |
| AI assistant | Only if you enable it and add your own API key | Your prompts + relevant terminal context, sent directly to the AI provider you chose (Anthropic/OpenAI/Google/OpenRouter) |
| Update check | Only when you click "Check for Updates" (About dialog) | A single unauthenticated request to the public `nexus-ssh-releases` GitHub Releases page — no identifying data included |
| Crash reporting | Never, unless you explicitly turn it on in Settings (off by default) | A stack trace, app version, and OS — see below |

There is no other telemetry, no usage analytics, no background "phone
home," and no ads or trackers.

## Everything sensitive is encrypted at rest

- **SSH key vault** — private keys and reusable credential sets are
  encrypted with **XChaCha20-Poly1305**, with the encryption key derived
  from your master password via **Argon2id** (OWASP-recommended desktop
  parameters: ~19 MiB memory, 2 passes). The vault file on disk is useless
  without that master password, which is never stored anywhere.
- **Saved session passwords / AI API keys** — sealed with
  XChaCha20-Poly1305 under a per-install device key, so no master password
  is needed for everyday use. That device key itself is protected by
  **Windows DPAPI** (tied to your Windows user account) on Windows, or a
  permissions-restricted (`0600`) file on macOS/Linux.
- **In memory** — key material is wrapped in zeroizing buffers that are
  overwritten (not just freed) as soon as they go out of scope, and private
  keys never cross into the frontend/UI layer at all — only the Rust
  backend ever touches raw key bytes.
- **Fail closed, not open** — if encryption fails for any reason, the app
  errors out rather than silently falling back to writing a secret in
  plaintext.

## Crash reporting, when you opt in

Off by default. If you turn it on in Settings:

- Only a stack trace, app version, and OS are sent — never session
  content, hostnames, IPs, file paths, or credentials.
- A scrubbing filter runs on every event before it's sent, redacting
  anything that looks like an IP address or a local file path, as a second
  layer of defense on top of the above.
- Turn it back off and no further events are ever sent.

## What this page is, and isn't

This describes the app's actual architecture and is kept in sync with the
code. It is **not** an independent third-party audit or a formal
certification — Nexus.ssh is a small independent project and the source is
currently private, so you're trusting this description rather than
verifying it yourself against public source. If that matters for your use
case (e.g. regulated environments), treat this as an architecture
disclosure, not a compliance attestation.

Out of scope for any client-side app like this one, no matter how it's
built: a compromised OS, physical access to an unlocked machine, or
malware already running as your user. Nexus.ssh protects the data at rest
and in transit; it can't protect a machine that's already compromised at a
lower level than the app itself.

## Found a security issue?

Please don't open a public issue for anything that looks like a real
vulnerability. Instead, reach out via [Ko-fi](https://ko-fi.com/vladyslavdubov)
or open an issue marked clearly as a security report with minimal detail,
and we'll follow up privately for the specifics.
