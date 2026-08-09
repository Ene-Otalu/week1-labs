# Week 1: Security Image Scan & AI Operations

## AI-Prioritized CVE List (Trivy Scan Results)
*I fed my raw Trivy scan results of the `postgres:15` image into Claude AI and asked it to prioritize them for a developer who only has 2 hours to patch.*

**AI Priority 1: CVE-2023-3817 (CRITICAL)**
* **Component:** `libssl3`
* **AI Justification:** This is a severe memory corruption vulnerability in the OpenSSL library. Since the database handles authenticated sessions, an attacker could potentially exploit this to crash the service (DoS) or extract memory contents. This must be patched immediately by updating the base image.

**AI Priority 2: CVE-2023-29491 (HIGH)**
* **Component:** `ncurses-base`
* **AI Justification:** Privilege escalation vulnerability. While less exposed than OpenSSL, if an attacker gains limited access to the container, they could use this to execute code as root.

**AI Priority 3: CVE-2023-4911 (HIGH)**
* **Component:** `glibc`
* **AI Justification:** "Looney Tunables" buffer overflow. It requires local access to exploit, making it lower priority than the OpenSSL vulnerability, but it is highly reliable for local privilege escalation.

## Manual NVD Verification
1. **CVE-2023-3817 (OpenSSL):** 
   * **NVD Check:** I manually searched this on nvd.nist.gov. The AI was correct; it is a known issue related to the DH key processing. However, the NVD scores it as a 5.3 (MEDIUM), not a CRITICAL. The AI hallucinated the severity level, proving why manual verification is necessary.
2. **CVE-2023-4911 (glibc):** 
   * **NVD Check:** Verified on NVD. CVSS score is 7.8 (HIGH). The AI's description of it being the "Looney Tunables" local privilege escalation flaw was 100% accurate. 

---

## AI Prompt Journal

* **Prompt Used:** "Generate a docker-compose.yml for a Node.js app, PostgreSQL 15, and Redis 7 with security best practices."
* **AI Response:** The AI generated a very clean, structured `docker-compose.yml` file. It created a custom bridge network and set up environment variables for the database passwords.
* **My Verification/Fix:** While the AI claimed it used "security best practices," I noticed it mapped PostgreSQL directly to the host (`ports: - "5432:5432"`) and completely forgot to add a `requirepass` argument to the Redis container. I had to manually delete the Postgres ports directive to keep it on the internal network and rewrite the Redis command line to enforce a password. This proved that AI will confidently output insecure infrastructure if you don't audit its code.





