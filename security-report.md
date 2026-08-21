# Container Vulnerability Security Report

**Scan tool:** Trivy
**Scope:** `redis:7.0` (debian 12.7) and `postgres:15` (debian 13.6) container images, including embedded `gosu` binaries
**Report date:** _fill in scan date_
**Prepared by:** DevSecOps
**Classification:** Internal

---

## 1. Executive Summary

Two production-adjacent container images — Redis and PostgreSQL — were scanned for known vulnerabilities and exposed secrets. Both images carry a large volume of low-impact base-OS findings typical of any Debian-derived image, but each also surfaces a small number of **CRITICAL/HIGH severity issues with plausible exploitability through the application's actual runtime surface** (TLS handling, XML parsing, privilege-drop tooling). One container also exposes a **private key file** that warrants immediate verification.

| Image | Total CVEs | Critical | High | Medium | Low | Unknown | Secrets |
|---|---|---|---|---|---|---|---|
| redis:7.0 (debian 12.7) | 279 | 8 | 47 | 118 | 103 | 3 | 0 |
| usr/local/bin/gosu (Redis image) | 111 | 4 | 52 | 50 | 4 | 1 | – |
| postgres:15 (debian 13.6) | 325 | 17 | 68 | 101 | 127 | 12 | 0 |
| usr/local/bin/gosu (Postgres image) | 46 | 1 | 21 | 21 | 2 | 1 | – |
| /etc/ssl/private/ssl-cert-snakeoil.key (Postgres image) | – | – | – | – | – | – | **1** |

**Bottom line:** Neither image is "clean," but the overwhelming majority of findings are either unfixed upstream, local-shell-only in exploitability, or outside the application's real code path. A focused set of ~6 findings across both images accounts for nearly all of the actionable near-term risk.

---

## 2. Critical Action Items (Next 2 Hours)

### Redis (redis:7.0)

| Rank | CVE | Component | Severity | Fix Available | Why It Matters |
|---|---|---|---|---|---|
| 1 | CVE-2026-31789 | libssl3 (OpenSSL) | CRITICAL | Yes — `3.0.19-1~deb12u2` | OpenSSL backs Redis's TLS handling directly. A malicious/oversized X.509 cert during handshake is a remotely triggerable heap overflow. |
| 2 | CVE-2026-33845 | libgnutls30 | CRITICAL | Yes — `3.7.9-2+deb12u7` | DoS via DTLS zero-length fragment. Base-image dependency; cheap to clear. |
| 3 | CVE-2026-4878 | libcap2 | HIGH | Yes — `1:2.66-4+deb12u3` | TOCTOU race in `cap_set_file()`. Directly relevant to this image's privilege-drop model (gosu + capability handling at startup). |

**Immediate command:**
```bash
apt-get update && apt-get install --only-upgrade libssl3 libgnutls30 libcap2
```

### PostgreSQL (postgres:15)

| Rank | CVE | Component | Severity | Fix Available | Why It Matters |
|---|---|---|---|---|---|
| 1 | CVE-2026-6653 | libxml2 | CRITICAL | Not yet published for deb13u | Backs Postgres's `xml`/`xpath()` extension — remotely triggerable DoS via crafted XML if that extension is loaded. |
| 2 | CVE-2025-68121 | Go stdlib (in gosu) | CRITICAL | Yes — `1.24.13` / `1.25.7` / `1.26.0-rc.3` | TLS certificate validation bypass during session resumption. Requires gosu rebuild with patched Go toolchain. |
| 3 | CVE-2026-24882 | GnuPG family (dirmngr, gnupg, gpg, gpg-agent, gpgconf, gpgsm) | HIGH | Not yet published | Stack overflow enabling arbitrary code execution. One root cause spans 6 packages. Relevant only if entrypoint/backup scripts pipe untrusted data through `gpg`. |

**Immediate command:**
```bash
apt-get update && apt-get install --only-upgrade libxml2
apt-cache policy libxml2   # confirm patched build availability
```

**Mitigation while awaiting patches:**
```sql
SELECT * FROM pg_extension;              -- check if xml2 is loaded
-- DROP EXTENSION IF EXISTS xml2;        -- if unused
```

---

## 3. Secret Exposure — PostgreSQL Image

```
/etc/ssl/private/ssl-cert-snakeoil.key — 1 secret detected
```

This is Debian's default self-signed TLS key, present in every `debian:13`-based image. Because the same key ships in countless public images, any TLS connection actually terminated with it is effectively unauthenticated and MITM-able.

- **Action:** Confirm `ssl_cert_file` / `ssl_key_file` in `postgresql.conf` do not reference this file in production. Replace with a properly issued certificate if they do.
- No equivalent secret was flagged in the Redis image scan.

---

## 4. Cross-Image Observations

- **Both images ship the same `gosu` privilege-drop binary pattern**, and both carry a stdlib-class CRITICAL in it (Redis: `CVE-2023-24538`, an `html/template` bug with effectively no exploit path in a non-templating binary; Postgres: `CVE-2025-68121`, a TLS validation bug that's more directly concerning). Recommend standardizing on a single, regularly-rebuilt `gosu` base across both images rather than patching each independently.
- **util-linux/libblkid TOCTOU CVEs** (`CVE-2026-53612`–`53615` family) appear repeatedly across both images' package lists (mount, libmount1, libblkid1, util-linux-extra, etc.). These require local shell/mount access to exploit and are not part of either database's network-facing attack surface. Low urgency, but low-cost to clear in a routine patch cycle since fixes exist for most.
- **Perl-related CRITICALs** (`CVE-2026-13221`) appear duplicated across multiple sub-packages in both images (5+ listings in Postgres alone) — this inflates raw CVE counts without representing 5 distinct issues. No fix is currently published for either image; treat as one tracked item, not five.
- **Neither database engine directly executes GnuPG or Perl at runtime** under normal operation — both toolchains are typically vestiges of the base OS image rather than active dependencies. Confirming this via entrypoint script review is a fast way to de-scope a large share of the remaining HIGH/CRITICAL count on both images.

---

## 5. Deprioritized Findings

| Image | CVE | Reason |
|---|---|---|
| Redis | CVE-2023-45853 (zlib1g, CRITICAL) | `will_not_fix`; vulnerable function not in Redis's code path. |
| Redis | util-linux/libblkid TOCTOU family (HIGH) | Requires local shell access. |
| Postgres | CVE-2026-53612 family (util-linux, HIGH) | Requires local shell access; fix available for future cycle. |
| Postgres | CVE-2026-14456 (openssl, HIGH) | `fix_deferred`; QUIC-specific, not used by PostgreSQL. |

---

## 6. Recommended Next Steps

1. Apply the immediate `apt-get` upgrades listed in Section 2 to both images and rebuild.
2. Verify TLS configuration on both containers (Redis TLS usage; Postgres snakeoil cert usage).
3. Audit entrypoint/backup scripts on both images for GnuPG or Perl invocations against untrusted input.
4. Schedule a `gosu` binary rebuild against a current Go toolchain, shared across both images.
5. Re-run Trivy after remediation to confirm the CRITICAL/HIGH counts have dropped and re-baseline.
6. Route the remaining ~600 combined LOW/MEDIUM findings into standard patch cadence rather than emergency handling.

---

*This report reflects point-in-time scan results and does not account for deployment-specific configuration (TLS enablement, loaded extensions, entrypoint scripts) unless explicitly noted. Confirm findings against actual running configuration before closing out remediation items.*
