# CVE Identification

- [Trivy](#trivy)


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

Result expected : Available in [vulnerabilities.json](https://github.com/fabienzx/tb/blob/main/cve/vulnerabilities.json)

To make sure we get an appropriate and friendly list of the different CVE that were found out thanks to Trivy, we will format the output (full details remain available in the json file) 

```bash
docker run -v /var/run/docker.sock:/var/run/docker.sock -v $HOME/Library/Caches:/root/.cache/ aquasec/trivy:0.49.0 image --severity HIGH,CRITICAL thingsboard/tb-postgres --format json | jq -r '.Results[].Vulnerabilities[] | "\(.VulnerabilityID) \(.Title) (\(.Severity))"' > format.json
```

Result expected :

```json
CVE-2022-3715 a heap-buffer-overflow in valid_parameter_transform (HIGH)
CVE-2022-1304 e2fsprogs: out-of-bounds read/write via crafted filesystem (HIGH)
CVE-2023-4911 glibc: buffer overflow in ld.so leading to privilege escalation (HIGH)
CVE-2023-4911 glibc: buffer overflow in ld.so leading to privilege escalation (HIGH)
CVE-2022-1304 e2fsprogs: out-of-bounds read/write via crafted filesystem (HIGH)
CVE-2019-8457 heap out-of-bound read in function rtreenode() (CRITICAL)
CVE-2022-1304 e2fsprogs: out-of-bounds read/write via crafted filesystem (HIGH)
CVE-2021-33560 mishandles ElGamal encryption because it lacks exponent blinding to address a side-channel attack against mpi_powm (HIGH)
CVE-2023-29499 glib: GVariant offset table entry size is not checked in is_normal() (HIGH)
CVE-2024-0567 gnutls: rejects certificate chain with distributed trust (HIGH)
CVE-2023-25193 harfbuzz: allows attackers to trigger O(n^2) growth via consecutive marks (HIGH)
CVE-2023-2953 null pointer dereference in  ber_memalloc_x  function (HIGH)
CVE-2023-29491 ncurses: Local users can trigger security-relevant memory corruption via malformed data (HIGH)
CVE-2023-29491 ncurses: Local users can trigger security-relevant memory corruption via malformed data (HIGH)
CVE-2024-0743 firefox: unchecked return value in TLS handshake code could have caused a potentially exploitable crash (HIGH)
CVE-2020-16156 perl-CPAN: Bypass of verification of signatures in CHECKSUMS files (HIGH)
CVE-2023-31484 perl: CPAN.pm does not verify TLS certificates when downloading distributions over HTTPS (HIGH)
CVE-2023-47038 perl: Write past buffer end via illegal user-defined Unicode property (HIGH)
CVE-2021-31239 sqlite: denial of service via the appendvfs.c function (HIGH)
CVE-2023-7104 sqlite: heap-buffer-overflow at sessionfuzz (HIGH)
CVE-2022-1304 e2fsprogs: out-of-bounds read/write via crafted filesystem (HIGH)
CVE-2023-0464 openssl: Denial of service by excessive resource usage in verifying X509 policy constraints (HIGH)
CVE-2023-29491 ncurses: Local users can trigger security-relevant memory corruption via malformed data (HIGH)
CVE-2022-2309 lxml: NULL Pointer Dereference in lxml (HIGH)
CVE-2022-4899 zstd: mysql: buffer overrun in util.c (HIGH)
CVE-2022-1304 e2fsprogs: out-of-bounds read/write via crafted filesystem (HIGH)
CVE-2023-29491 ncurses: Local users can trigger security-relevant memory corruption via malformed data (HIGH)
CVE-2023-29491 ncurses: Local users can trigger security-relevant memory corruption via malformed data (HIGH)
CVE-2024-20918 OpenJDK: array out-of-bounds access due to missing range check in C1 compiler (8314468) (HIGH)
CVE-2024-20952 OpenJDK: RSA padding issue and timing side-channel attack against TLS (8317547) (HIGH)
CVE-2024-20918 OpenJDK: array out-of-bounds access due to missing range check in C1 compiler (8314468) (HIGH)
CVE-2024-20952 OpenJDK: RSA padding issue and timing side-channel attack against TLS (8317547) (HIGH)
CVE-2024-20918 OpenJDK: array out-of-bounds access due to missing range check in C1 compiler (8314468) (HIGH)
CVE-2024-20952 OpenJDK: RSA padding issue and timing side-channel attack against TLS (8317547) (HIGH)
CVE-2024-20918 OpenJDK: array out-of-bounds access due to missing range check in C1 compiler (8314468) (HIGH)
CVE-2024-20952 OpenJDK: RSA padding issue and timing side-channel attack against TLS (8317547) (HIGH)
CVE-2020-16156 perl-CPAN: Bypass of verification of signatures in CHECKSUMS files (HIGH)
CVE-2023-31484 perl: CPAN.pm does not verify TLS certificates when downloading distributions over HTTPS (HIGH)
CVE-2023-47038 perl: Write past buffer end via illegal user-defined Unicode property (HIGH)
CVE-2020-16156 perl-CPAN: Bypass of verification of signatures in CHECKSUMS files (HIGH)
CVE-2023-31484 perl: CPAN.pm does not verify TLS certificates when downloading distributions over HTTPS (HIGH)
CVE-2023-47038 perl: Write past buffer end via illegal user-defined Unicode property (HIGH)
CVE-2020-16156 perl-CPAN: Bypass of verification of signatures in CHECKSUMS files (HIGH)
CVE-2023-31484 perl: CPAN.pm does not verify TLS certificates when downloading distributions over HTTPS (HIGH)
CVE-2023-47038 perl: Write past buffer end via illegal user-defined Unicode property (HIGH)
CVE-2023-45853 zlib: integer overflow and resultant heap-based buffer overflow in zipOpenNewFileInZip4_6 (CRITICAL)
CVE-2023-6378 logback: serialization vulnerability in logback receiver (HIGH)
CVE-2023-6378 logback: serialization vulnerability in logback receiver (HIGH)
CVE-2024-23684 Inefficient Algorithmic Complexity in com.upokecenter:cbor (HIGH)
GHSA-fj2w-wfgv-mwq6 Denial of service in CBOR library (HIGH)
CVE-2023-1428 Reachable Assertion (HIGH)
CVE-2023-32731 sensitive information disclosure (HIGH)
GHSA-xpw8-rcwv-8f8p io.netty:netty-codec-http2 vulnerable to HTTP/2 Rapid Reset Attack (HIGH)
CVE-2023-1370 json-smart: Uncontrolled Resource Consumption vulnerability in json-smart (Resource Exhaustion) (HIGH)
CVE-2023-1370 json-smart: Uncontrolled Resource Consumption vulnerability in json-smart (Resource Exhaustion) (HIGH)
CVE-2023-46589 tomcat: HTTP request smuggling via malformed trailer headers (HIGH)
CVE-2023-44981 zookeeper: Authorization Bypass in Apache ZooKeeper (CRITICAL)
CVE-2022-2576 Eclipse Californium denial of service (DoS) via Datagram Transport Layer Security (DTLS) handshake on parameter mismatch (HIGH)
CVE-2022-39368 Failing DTLS handshakes may cause throttling to block processing of records (HIGH)
CVE-2023-4759 jgit: arbitrary file overwrite (HIGH)
CVE-2021-40660 Regular expression denial of service in Delight Nashorn Sandbox (HIGH)
CVE-2023-20873 spring-boot: Security Bypass With Wildcard Pattern Matching on Cloud Foundry (CRITICAL)
CVE-2023-20883 spring-boot: Spring Boot Welcome Page DoS Vulnerability (HIGH)
CVE-2023-34034 spring-security-webflux: path wildcard leads to security bypass (CRITICAL)
CVE-2023-20863 Spring Expression DoS Vulnerability (HIGH)
CVE-2016-1000027 spring: HttpInvokerServiceExporter readRemoteInvocation method untrusted java deserialization (CRITICAL)
CVE-2023-34455 snappy-java: Unchecked chunk length leads to DoS (HIGH)
CVE-2023-43642 snappy-java: Missing upper bound check on chunk length in snappy-java can lead to Denial of Service (DoS) impact (HIGH)
```

*Some CVE may appear multiple times (i.e. CVE-2023-4911 is a vulnerabilty that has been detected for libc-bin AND libc6, thus two entries)*

**Out of those 60+ CVEs, we denote :**

>Related to the docker image vulnerabilities: \t
46 (HIGH), 2 (CRITICAL), TOTAL : 46

>Related to the application itself (JAVA jar): \t
18 (HIGH), 4 (CRITICAL), TOTAL : 22


