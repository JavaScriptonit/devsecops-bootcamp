https://gitlab.com/devsecops-bootcamp2/juice-shop-github/-/jobs/8273157681

## Detecting Debian vulnerabilities:
```
====================================
Total: 11 (UNKNOWN: 0, LOW: 0, MEDIUM: 7, HIGH: 3, CRITICAL: 1)
+-----------+------------------+----------+-------------------+---------------+-----------------------------------------+
|  LIBRARY  | VULNERABILITY ID | SEVERITY | INSTALLED VERSION | FIXED VERSION |                  TITLE                  |
+-----------+------------------+----------+-------------------+---------------+-----------------------------------------+
| libc6     | CVE-2019-1010022 | CRITICAL | 2.31-13+deb11u10  |               | glibc: stack guard protection bypass    |
|           |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2019-1010022 |
+           +------------------+----------+                   +---------------+-----------------------------------------+
|           | CVE-2018-20796   | HIGH     |                   |               | glibc: uncontrolled recursion in        |
|           |                  |          |                   |               | function check_dst_limits_calc_pos_1    |
|           |                  |          |                   |               | in posix/regexec.c                      |
|           |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2018-20796   |
+           +------------------+          +                   +---------------+-----------------------------------------+
|           | CVE-2019-1010023 |          |                   |               | glibc: running ldd on malicious ELF     |
|           |                  |          |                   |               | leads to code execution because of...   |
|           |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2019-1010023 |
+           +------------------+          +                   +---------------+-----------------------------------------+
|           | CVE-2019-9192    |          |                   |               | glibc: uncontrolled recursion in        |
|           |                  |          |                   |               | function check_dst_limits_calc_pos_1    |
|           |                  |          |                   |               | in posix/regexec.c                      |
|           |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2019-9192    |
+           +------------------+----------+                   +---------------+-----------------------------------------+
|           | CVE-2010-4756    | MEDIUM   |                   |               | glibc: glob implementation              |
|           |                  |          |                   |               | can cause excessive CPU and             |
|           |                  |          |                   |               | memory consumption due to...            |
|           |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2010-4756    |
+           +------------------+          +                   +---------------+-----------------------------------------+
|           | CVE-2019-1010024 |          |                   |               | glibc: ASLR bypass using                |
|           |                  |          |                   |               | cache of thread stack and heap          |
|           |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2019-1010024 |
+           +------------------+          +                   +---------------+-----------------------------------------+
|           | CVE-2019-1010025 |          |                   |               | glibc: information disclosure of heap   |
|           |                  |          |                   |               | addresses of pthread_created thread     |
|           |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2019-1010025 |
+-----------+------------------+          +-------------------+---------------+-----------------------------------------+
| libssl1.1 | CVE-2007-6755    |          | 1.1.1w-0+deb11u1  |               | Dual_EC_DRBG: weak pseudo               |
|           |                  |          |                   |               | random number generator                 |
|           |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2007-6755    |
+           +------------------+          +                   +---------------+-----------------------------------------+
|           | CVE-2010-0928    |          |                   |               | openssl: RSA authentication weakness    |
|           |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2010-0928    |
+-----------+------------------+          +                   +---------------+-----------------------------------------+
| openssl   | CVE-2007-6755    |          |                   |               | Dual_EC_DRBG: weak pseudo               |
|           |                  |          |                   |               | random number generator                 |
|           |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2007-6755    |
+           +------------------+          +                   +---------------+-----------------------------------------+
|           | CVE-2010-0928    |          |                   |               | openssl: RSA authentication weakness    |
|           |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2010-0928    |
+-----------+------------------+----------+-------------------+---------------+-----------------------------------------+
```