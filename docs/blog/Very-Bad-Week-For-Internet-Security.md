---
layout: default
title: A very bad week for Internet Security (October 19-22)
nav_exclude: false
has_children: false
parent: Blog and personal opinions
search_exclude: false
last_modified_date: 2026-10-22
---

# A very bad week for Internet Security
{: .no_toc }

{% include toc.md %}

## What the hell is happening?
So it started out with one single tweet about two critical PHP vulnerabilities (`CVE-2026-109618` and `CVE-2026-109619`), which came to be known as PHP2Shell Vulnerability that was announced just a few days ago at the time of writing (Tuesday 20 October). Emergency security patches were released for these two immediately, following an earlier-than-planned release after details of these vulnerabilities were released.

Since then, even more vulnerabilities (not just from PHP) came to surface, one after another, affecting different services, platforms, etc., some straight up being extremely severe (such as the PHP one), others, not as much. All in all, it marked the beginning of a really, really bad week.

![../../assets/img/Blog/How-did-we-get-here.png](../../assets/img/Blog/How-did-we-get-here.png)

## Time to make a list
This list basically is a list of every single vulnerability classified as date-first, severity second sorting, which covers some of the most impactful vulnerabilities and issues, along with a few of my own comments, which I came across (and informed via friends). Without further ado, allow me to list the following Hell on Earth: A very bad week for Internet Security. (Currently documenting October 19-22)

### Major Vulnerabilities & Security Updates

- Oct 22 - [Linux kernel - multiple prematurely disclosed vulnerabilities](https://www.phoronix.com/news/LKML-New-Trend-Vulnerabilities) - CVSS up to 9.0: Apparently accidental public reports expose SMB-related RCE, local privilege-escalation, and information-disclosure flaws before mainline fixes are available. (Six reports discussed; one was posted the previous day. Exposure depends on the affected components; some fixes are undergoing testing or queued.)
  - *Additional note: Greg Kroah-Hartman’s response to Trend Micro: "Again, no patch, and sent to a public list? Please fix your submission process..." Responsible disclosure, apparently sent to everyone responsible for reading LKML.*

- Oct 21 - [GitLab CE/EE](https://docs.gitlab.com/releases/patches/patch-release-gitlab-19-5-1-released/) - CVSS 10.0: Regex compiler overflow can permit unauthenticated server takeover; release fixes 12 vulnerabilities.
  - *Additional note: GitLab.com is already patched; self-managed administrators have to apply the fix themselves. Unfortunately, hosting your own GitLab also means hosting your own emergency.*

- Oct 21 - [PHP - PHP2Shell](https://www.php.net/archive/2026.php) - CVSS v4.0 9.2: Two memory-safety flaws let unauthenticated web requests execute server-side code. (CVE-2026-109618 and CVE-2026-109619; fixed in 8.5.12, 8.4.27, 8.3.36, and 8.2.35.)
  - *Additional note: This is a PHP runtime problem, not something your application’s input validation fixes. With the demonstrated Apache `mod_php` exploit, the application does not even get a turn before things go wrong.*

- Oct 21 - [Apache Traffic Server](https://github.com/advisories/GHSA-4h97-h3mf-j6w7) - CVSS 9.1 for CVE-2025-31699; score unverified for [CVE-2025-55702](https://app.opencve.io/cve/CVE-2025-55702): Connection-reuse and unread-request-body flaws enable request smuggling, response desynchronization, and potentially cache poisoning or access-control bypass. (Fixed in 9.2.16, 10.1.5, and 10.2.1.)
  - *Additional note: Connections get reused while somebody is still expecting a request body-or leftover body bytes become another request. HTTP meal prep: yesterday’s leftovers are now somebody else’s security incident.*

- Oct 21 - [Node.js - Node2Shell](https://nodejs.org/en/blog/vulnerability/october-2026-security-releases) - High maximum: Brotli decoder memory corruption permits remote code execution; nine additional flaws affect DNS handling, TLS verification, HTTP handling, randomness, ZIP processing, and filesystem permissions. (RCE: CVE-2026-111497; fixed in 22.23.4, 24.22.1, and 26.12.1.)
  - *Additional note: One flaw preserves cached randomness inside startup snapshots, allowing separate processes to repeat supposedly random values. "Random once, reproducible forever" is a build feature-not an ideal security property.*

- Oct 21 announcement; Oct 21–22 releases - [Fortinet - FortiOS, FortiManager, FortiAnalyzer, FortiMail & FortiAuthenticator](https://www.fortinet.com/blog/ciso-collective/fortinet-releases-security-hardening-release-for-multiple-products) - Critical/High; individual CVEs and CVSS scores pending: Coordinated updates address vulnerabilities found through AI-assisted testing; prioritize internet-facing devices. (Detailed advisories scheduled for Nov 10; no active exploitation confirmed in the announcement.)
  - *Additional note: Despite the "security hardening" label, these are vulnerability fixes-not optional improvements. Until patched, restrict administrative interfaces to trusted networks; MFA and reduced exposure do not replace upgrading. "Hardening" is doing some heavy lifting in that headline.*
  - *Personal note: Considering the urgency of this report, it can be considered that 

- Oct 20 - [Google Chrome](https://www.tenable.com/cve/CVE-2026-113072) - CVSS 9.6: CSS memory corruption lets a crafted HTML page potentially execute arbitrary code outside the browser sandbox. (CVE-2026-113072; fixed in 156.0.8078.47.)

- Oct 20 - [Next.js](https://www.csa.gov.sg/alerts-and-advisories/alerts/al-2026-148/) - CVSS v4.0 9.5: Two RCE flaws affect specific caching configurations and glibc-based image processing. (CVE-2026-96889 and GHSA-673q-mjm6-r5xr; advisory identifies fixes in 15.5.28 and 16.4.1.)

### Breaches, Infrastructure Incidents & Active Exploitation

- Oct 22 - [Capcom - CAPCOM ID](https://www.capcom.co.jp/ir/english/news/html/e261022.html) - Confirmed breach; no CVSS or exploit disclosed: Email addresses and account metadata exposed for 11,774,247 accounts worldwide; 196 accounts had passwords illicitly changed and subsequently reset. (Credit-card information excluded; no leakage of user-set passwords confirmed; containment measures completed, with investigation ongoing.)

- Oct 21 - [Railway](https://blog.railway.com/p/security-disclosure-wednesday-october-21st) - Potential secret exposure; no CVSS listed: Unauthorized access may have exposed customer environment variables, including some decrypted secrets.

- Oct 21 reporting - [Palo Alto PAN-OS GlobalProtect](https://www.helpnetsecurity.com/2026/10/21/ransomware-groups-exploit-palo-alto-globalprotect-cve-2026-0257/) - Active exploitation; score not verified: Ransomware groups exploit an older authentication bypass to enter vulnerable networks. (CVE-2026-0257; retained for new exploitation reporting, not as a newly disclosed vulnerability.)

- Oct 19 reporting - [BeyondTrust Remote Support - formerly Bomgar](https://www.rapid7.com/blog/post/etr-cve-2026-102764-critical-beyondtrust-remote-support-authentication-bypass-exploited-in-the-wild/) - CVSS v4.0 9.3: Actively exploited authentication bypass allows unauthenticated file operations, potentially leading to appliance takeover and credential exposure. (CVE-2026-102764; affects versions through 26.2.3 unless patched with BT26-05-RS; original disclosure Oct 15.)

- Oct 19 reporting - [Plex Media Server](https://arstechnica.com/security/2026/10/recently-fixed-plex-media-vulnerabilities-are-being-exploited-to-install-malware/) - CVSS 8.6, highest component: Four previously patched flaws are chained to install miners and proxy malware. (CVE-2026-96652, -96654, -96655, and -96656; retained for new exploitation reporting.)

- Oct 19 - [TiDB Cloud/PingCAP](https://www.pingcap.com/trust-hub/security/security-update-october-2026/) - Confirmed breach; no CVSS listed: Stolen service credentials exposed source code and customer records; database-content theft remains unestablished.

### Certificate-Authority Compromise & Cross-Ecosystem Updates

- Oct 20 public response; downstream updates Oct 20–21 - [eMudhra/emSign](https://www.csoonline.com/article/4238338/google-mozilla-revoke-emudhra-intermediates-after-private-key-compromise.html) - CA key compromise: Eight recoverable intermediate CA keys enable forged certificates against clients that still trust them. Related remediation includes [Oracle Java SE/GraalVM](https://www.oracle.com/security-alerts/alert-cve-2026-91403.html) (CVE-2026-91403; CVSS 9.1), [Go](https://thehackernews.com/2026/10/eight-emudhra-ca-keys-compromised.html) (CVE-2026-111943), and [Firefox/NSS](https://blog.mozilla.org/security/2026/10/20/protecting-firefox-users-following-the-compromise-of-emudhra-intermediate-certificates/).
  - *Additional note: One private key was literally `4`; two others were `56` and `115`. Researchers reportedly recovered all eight in less than a second. The memes generated from this one are glorious (search up "eMudhra 4" on Google).*
  - *Remediation note: This is one CA failure with several ecosystems’ emergency updates-not independent compromises of Java, Go, and Firefox. Standard Firefox configurations received an automatic block on Oct 17; affected Go applications need rebuilding.*
  - *Nail in the coffin note: [eMudhra officially announced they are exiting the global SSL/TLS Certificate business](https://emudhra.com/en/press-release/emudhra-to-exit-global-ssl-tls-certificate-business), to nobody's surprise.*

### Supply-Chain Compromises

- Oct 21 - [LiteLLM](https://www.wiz.io/blog/litellm-compromised-steals-credentials) - Confirmed supply-chain compromise; no CVSS listed: Malicious version 1.107.0 installs credential-stealing Python startup hooks and a remote-code loader. (Affected PyPI and container artifacts require rebuilding and exposed-secret rotation, not merely an upgrade.)

### Specialist Infrastructure & Developer Risks

These are more niche issues that affect a smaller band of users, even if the issues themselves are quite severe to anyone having these (if you work with any of these, congratulations to your weekends becoming weekdays).

- Oct 22 - [TianoCore EDK II - PXE network boot](https://github.com/tianocore/edk2/security/advisories/GHSA-99cj-7hg9-mp4m) - CVSS 9.5: Crafted ICMP error messages during IPv4/IPv6 PXE boot overflow firmware memory, potentially executing attacker code before the operating system loads. (CVE-2026-97631; requires the affected network-boot path; advisory lists no patched version, with a proposed fix referenced.)

- Oct 22 - [Better Auth](https://app.opencve.io/cve/CVE-2026-114607) - CVSS 3.1 9.1: Certain Magic Link/OAuth configurations accept OAuth sign-in state as a login token, allowing unauthenticated user impersonation or account creation with falsely verified email. (CVE-2026-114607; affects 1.4.0-beta.18 through versions before 1.7.7; fixed in 1.7.7.)
  - *Additional note: This depends on a particular combination of enabled features and token-storage settings-not every Better Auth deployment is vulnerable.*

- Oct 21 - [Best Practice Software Bp Premier](https://github.com/advisories/GHSA-hmqc-m6cv-3c9r) - CVSS 9.8: Shared hardcoded SQL Server administrator credentials allow database takeover and potentially SYSTEM command execution. (CVE-2026-114119; affects versions before 1.14.1.1128; requires database-network access.)
  - *Additional note: The administrator password is shared across installations, and changing it breaks the application. "Best Practice" is the company name, not an architectural description.*

- Oct 21 - [Amazon SageMaker Python SDK](https://aws.amazon.com/security/security-bulletins/2026-142-aws/) - CVSS v4.0 9.4: Missing ownership checks let attackers pre-create a predictable S3 bucket, potentially executing code in a victim’s SageMaker environment and stealing IAM credentials. (CVE-2026-112408; attacker must claim the expected bucket first; fixed in SDK V2 2.257.3 and V3 3.10.0.)

- Oct 19, date provisional - [IBM DataStage on Cloud Pak for Data](https://www.rapid7.com/db/vulnerabilities/cve-2026-81212/) - CVSS 10.0: Unauthenticated attackers can overwrite other tenants’ Redis keys, undermining credential-encryption boundaries and cached flow data. (CVE-2026-81212; affects 5.4.0.0.)
  - *Additional note: "Shared Redis" should mean shared infrastructure, not permission to write another tenant’s keys. Apparently, the tenant boundary was more of a suggestion.*

- Oct 19 reporting - [EG Secure Solutions SiteGuard Server Edition](https://securityaffairs.com/201258/security/japans-siteguard-waf-flaw-cve-2026-106931-is-already-being-exploited.html) - CVSS v4.0 8.5: Actively exploited statistics-feature command injection lets a low-privileged local attacker execute commands as root or SYSTEM. (CVE-2026-106931; original disclosure Oct 14; fixes available.)

- Oct 19 - [Siemens Software Center](https://productcert.siemens.com/news/2026/10/19/active-exploitation-of-cve-2026-110936-in-siemens-software-center/) - CVSS v4.0 8.4: Attackers exploit DLL side-loading to execute malicious code with the application’s privileges. (CVE-2026-110936; exploitation confirmed by Siemens; fixed in 4.0.9.8.)

### Developing Reports & Research

- Oct 21 - [CyberCartel - Latin American financial targets](https://www.straiker.ai/blog/inside-carliy0s-how-cybercartel-used-multiple-ai-models-to-attack-latin-american-banks) - Reported attack campaign; no CVSS: AI agents using Claude, Grok, and Moonshot models reportedly automated attacks against 400+ financial targets. (According to Straiker research; target count is not a confirmed breach count.)

- Disclosure date unverified - [Header Accordions - Bun 1.4.3, Hyperium h3, and aioquic/mitmproxy](https://foxio.io/blog/header-accordions-qpack-amplification-attacks-against-http-3-servers) - Remote DoS; CVSS unverified: QPACK-compressed HTTP/3 headers expand into excessive allocations, exhausting memory. (These implementations were reported as unpatched; exact disclosure date and maintainer-confirmed patch status remain unverified.)

---

![../../assets/img/Blog/Hell-on-earth.png](../../assets/img/Blog/Hell-on-earth.png)

---
## Credits:
Thank you to my friends at the discord servers for [r/techsupport](https://www.reddit.com/r/techsupport/), [PCHH](https://pchelphub.com/) and [r/buildaPC](https://www.reddit.com/r/buildapc/): `beandotmp3`, `solus_bellator`, `itsblados`, `codepanda`, `sleepyhampter` and `goodblobplsgivecookie` for feeding me info into what CVEs to look for to make this list.

