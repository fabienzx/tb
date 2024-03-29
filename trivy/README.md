# Static code analysis Trivy

- [Trivy](#trivy)
- [Results](#results)


## Trivy

Installation according to :
https://aquasecurity.github.io/trivy/v0.49/getting-started/installation/

In order to use Trivy to find already known CVE within TB container, we first need to pull Trivy's latest build image

```bash
docker pull aquasec/trivy:0.49.0 
```

Then we can run the following command to make Trivy analyze the container :

```bash
docker run -v /var/run/docker.sock:/var/run/docker.sock -v $HOME/Library/Caches:/root/.cache/ aquasec/trivy:0.49.0 image thingsboard/tb-postgres --format json > rapport_vulnerabilites.json
```

Result: [vulnerabilities.json](https://github.com/fabienzx/tb/blob/main/trivy/vulnerabilities.json)

To make sure we get an appropriate and friendly list of the different CVE that were found out thanks to Trivy, we will format the output (full details remain available in the json file) 

```bash
docker run -v /var/run/docker.sock:/var/run/docker.sock -v $HOME/Library/Caches:/root/.cache/ aquasec/trivy:0.49.0 image --severity HIGH,CRITICAL thingsboard/tb-postgres --format json | jq -r '.Results[].Vulnerabilities[] | "\(.VulnerabilityID) \(.Title) (\(.Severity)) - Status: \(.Status)"' > cve-format.txt
```

Result:

```txt
CVE-2022-3715 a heap-buffer-overflow in valid_parameter_transform (HIGH) - Status: affected
CVE-2022-1304 e2fsprogs: out-of-bounds read/write via crafted filesystem (HIGH) - Status: affected
CVE-2023-4911 glibc: buffer overflow in ld.so leading to privilege escalation (HIGH) - Status: fixed
CVE-2023-4911 glibc: buffer overflow in ld.so leading to privilege escalation (HIGH) - Status: fixed
CVE-2022-1304 e2fsprogs: out-of-bounds read/write via crafted filesystem (HIGH) - Status: affected
CVE-2019-8457 heap out-of-bound read in function rtreenode() (CRITICAL) - Status: affected
CVE-2022-1304 e2fsprogs: out-of-bounds read/write via crafted filesystem (HIGH) - Status: affected
CVE-2021-33560 mishandles ElGamal encryption because it lacks exponent blinding to address a side-channel attack against mpi_powm (HIGH) - Status: affected
CVE-2023-29499 glib: GVariant offset table entry size is not checked in is_normal() (HIGH) - Status: affected
CVE-2024-0567 gnutls: rejects certificate chain with distributed trust (HIGH) - Status: affected
CVE-2023-25193 harfbuzz: allows attackers to trigger O(n^2) growth via consecutive marks (HIGH) - Status: affected
CVE-2023-2953 null pointer dereference in  ber_memalloc_x  function (HIGH) - Status: affected
CVE-2023-29491 ncurses: Local users can trigger security-relevant memory corruption via malformed data (HIGH) - Status: fixed
CVE-2023-29491 ncurses: Local users can trigger security-relevant memory corruption via malformed data (HIGH) - Status: fixed
CVE-2024-0743 firefox: unchecked return value in TLS handshake code could have caused a potentially exploitable crash (HIGH) - Status: affected
CVE-2020-16156 perl-CPAN: Bypass of verification of signatures in CHECKSUMS files (HIGH) - Status: affected
CVE-2023-31484 perl: CPAN.pm does not verify TLS certificates when downloading distributions over HTTPS (HIGH) - Status: affected
CVE-2023-47038 perl: Write past buffer end via illegal user-defined Unicode property (HIGH) - Status: affected
CVE-2021-31239 sqlite: denial of service via the appendvfs.c function (HIGH) - Status: affected
CVE-2023-7104 sqlite: heap-buffer-overflow at sessionfuzz (HIGH) - Status: affected
CVE-2022-1304 e2fsprogs: out-of-bounds read/write via crafted filesystem (HIGH) - Status: affected
CVE-2023-0464 openssl: Denial of service by excessive resource usage in verifying X509 policy constraints (HIGH) - Status: fixed
CVE-2023-29491 ncurses: Local users can trigger security-relevant memory corruption via malformed data (HIGH) - Status: fixed
CVE-2022-2309 lxml: NULL Pointer Dereference in lxml (HIGH) - Status: affected
CVE-2022-4899 zstd: mysql: buffer overrun in util.c (HIGH) - Status: affected
CVE-2022-1304 e2fsprogs: out-of-bounds read/write via crafted filesystem (HIGH) - Status: affected
CVE-2023-29491 ncurses: Local users can trigger security-relevant memory corruption via malformed data (HIGH) - Status: fixed
CVE-2023-29491 ncurses: Local users can trigger security-relevant memory corruption via malformed data (HIGH) - Status: fixed
CVE-2024-20918 OpenJDK: array out-of-bounds access due to missing range check in C1 compiler (8314468) (HIGH) - Status: fixed
CVE-2024-20952 OpenJDK: RSA padding issue and timing side-channel attack against TLS (8317547) (HIGH) - Status: fixed
CVE-2024-20918 OpenJDK: array out-of-bounds access due to missing range check in C1 compiler (8314468) (HIGH) - Status: fixed
CVE-2024-20952 OpenJDK: RSA padding issue and timing side-channel attack against TLS (8317547) (HIGH) - Status: fixed
CVE-2024-20918 OpenJDK: array out-of-bounds access due to missing range check in C1 compiler (8314468) (HIGH) - Status: fixed
CVE-2024-20952 OpenJDK: RSA padding issue and timing side-channel attack against TLS (8317547) (HIGH) - Status: fixed
CVE-2024-20918 OpenJDK: array out-of-bounds access due to missing range check in C1 compiler (8314468) (HIGH) - Status: fixed
CVE-2024-20952 OpenJDK: RSA padding issue and timing side-channel attack against TLS (8317547) (HIGH) - Status: fixed
CVE-2020-16156 perl-CPAN: Bypass of verification of signatures in CHECKSUMS files (HIGH) - Status: affected
CVE-2023-31484 perl: CPAN.pm does not verify TLS certificates when downloading distributions over HTTPS (HIGH) - Status: affected
CVE-2023-47038 perl: Write past buffer end via illegal user-defined Unicode property (HIGH) - Status: affected
CVE-2020-16156 perl-CPAN: Bypass of verification of signatures in CHECKSUMS files (HIGH) - Status: affected
CVE-2023-31484 perl: CPAN.pm does not verify TLS certificates when downloading distributions over HTTPS (HIGH) - Status: affected
CVE-2023-47038 perl: Write past buffer end via illegal user-defined Unicode property (HIGH) - Status: affected
CVE-2020-16156 perl-CPAN: Bypass of verification of signatures in CHECKSUMS files (HIGH) - Status: affected
CVE-2023-31484 perl: CPAN.pm does not verify TLS certificates when downloading distributions over HTTPS (HIGH) - Status: affected
CVE-2023-47038 perl: Write past buffer end via illegal user-defined Unicode property (HIGH) - Status: affected
CVE-2023-45853 zlib: integer overflow and resultant heap-based buffer overflow in zipOpenNewFileInZip4_6 (CRITICAL) - Status: will_not_fix
CVE-2023-6378 logback: serialization vulnerability in logback receiver (HIGH) - Status: fixed
CVE-2023-6378 logback: serialization vulnerability in logback receiver (HIGH) - Status: fixed
CVE-2024-23684 Inefficient Algorithmic Complexity in com.upokecenter:cbor (HIGH) - Status: fixed
GHSA-fj2w-wfgv-mwq6 Denial of service in CBOR library (HIGH) - Status: fixed
CVE-2023-1428 Reachable Assertion (HIGH) - Status: fixed
CVE-2023-32731 sensitive information disclosure (HIGH) - Status: fixed
GHSA-xpw8-rcwv-8f8p io.netty:netty-codec-http2 vulnerable to HTTP/2 Rapid Reset Attack (HIGH) - Status: fixed
CVE-2023-1370 json-smart: Uncontrolled Resource Consumption vulnerability in json-smart (Resource Exhaustion) (HIGH) - Status: fixed
CVE-2023-1370 json-smart: Uncontrolled Resource Consumption vulnerability in json-smart (Resource Exhaustion) (HIGH) - Status: fixed
CVE-2023-46589 tomcat: HTTP request smuggling via malformed trailer headers (HIGH) - Status: fixed
CVE-2023-44981 zookeeper: Authorization Bypass in Apache ZooKeeper (CRITICAL) - Status: fixed
CVE-2022-2576 Eclipse Californium denial of service (DoS) via Datagram Transport Layer Security (DTLS) handshake on parameter mismatch (HIGH) - Status: fixed
CVE-2022-39368 Failing DTLS handshakes may cause throttling to block processing of records (HIGH) - Status: fixed
CVE-2023-4759 jgit: arbitrary file overwrite (HIGH) - Status: fixed
CVE-2021-40660 Regular expression denial of service in Delight Nashorn Sandbox (HIGH) - Status: fixed
CVE-2023-20873 spring-boot: Security Bypass With Wildcard Pattern Matching on Cloud Foundry (CRITICAL) - Status: fixed
CVE-2023-20883 spring-boot: Spring Boot Welcome Page DoS Vulnerability (HIGH) - Status: fixed
CVE-2023-34034 spring-security-webflux: path wildcard leads to security bypass (CRITICAL) - Status: fixed
CVE-2023-20863 Spring Expression DoS Vulnerability (HIGH) - Status: fixed
CVE-2016-1000027 spring: HttpInvokerServiceExporter readRemoteInvocation method untrusted java deserialization (CRITICAL) - Status: fixed
CVE-2023-34455 snappy-java: Unchecked chunk length leads to DoS (HIGH) - Status: fixed
CVE-2023-43642 snappy-java: Missing upper bound check on chunk length in snappy-java can lead to Denial of Service (DoS) impact (HIGH) - Status: fixed
```
---
*Some CVE may appear multiple times (i.e. CVE-2023-4911 is a vulnerabilty that can be exploited both in/with libc-bin AND libc6, thus two entries)*


## Results


**We therefore denote :**

| Vulnerability Type                  | HIGH | CRITICAL | TOTAL | UNIQUE | FIXED | AFFECTED | WILL-NOT-FIX |
|-------------------------------------|:----:|:--------:|:-----:|:------:|:-----:|:--------:|:---:|
| Docker Image Vulnerabilities (system) |  46  |    2     |   46  |   29   |   16 (*35%*) |    29 (*63%*)   |  1 (*2%*)  |
| Application (JAVA jar) Vulnerabilities |  18  |    4     |   22  |   20   |   22 (*100%*)  |    0 (*0%*)    |  0 (*0%*)  |


<br>

**Definitions:**

- **Fixed:** A solution or patch has been identified and deployed. However, the system is still utilizing a potentially vulnerable version. Updating to the latest version should resolve the issue.

- **Affected:** No solution or patch has been identified yet, leaving the system vulnerable to potential threats.

- **Will-not-fix:** The developer or responsible team acknowledges the existence of a vulnerability but has no plans to release a patch. This decision is often made when the vulnerability is deemed insignificant/not worth it.

<br>

*Note: cve-2023-45853 is tagged as "WILL-NOT-FIX" but a patch has been released in the latest build.*

The CVE PoC consist of a crafted ZIP file that has to be opened on victim's end.

According to Red Hat :
>This may allow an attacker to craft a malicious ZIP file that will lead to an overflow on the length field. This value is further used in memory allocations and indexing, which can cause an out-of-bounds >write, leading to heap corruption and possible arbitrary code execution
>Additionally, the user would need to be tricked into opening the crafted file from an attacker to be successful.

However it is required to have MiniZIP from zlib in the container.

zlib is indeed present in the container but MiniZIP isn't integrated by default.

<br>
It is noteworthy that all the CVEs associated with the application itself have an available patch and merely necessitate an update to the latest version or nothing at all depending on the use of the different libraries.

Additionally, it is crucial to emphasize that although certain CVEs may be deemed impactful, their harm potential is contingent on specific circumstances that may or may not be applicable to Thingsboard.
