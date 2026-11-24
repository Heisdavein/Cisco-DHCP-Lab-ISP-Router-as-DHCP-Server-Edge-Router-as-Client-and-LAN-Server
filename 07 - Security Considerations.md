# 07 - Security Considerations

The lab ran in a simulator. No DHCP security features were configured, and none are claimed. This page lists what a reviewer would raise.

## Contents

- Measures in the lab
- Gaps and hardening not covered

## Measures in the lab

| Area | Measure | Reason |
| --- | --- | --- |
| Address conflicts | Router and gateway addresses excluded from pools | Prevents leasing an address that is already in use |
| Private addressing | LAN uses RFC 1918 `192.168.1.0/24` | Not routable on the public internet |
| Persistence | `write memory` | Keeps the intended configuration after a reload |

## Gaps and hardening not covered

| Observation | Why it matters |
| --- | --- |
| No DHCP snooping | A rogue DHCP server on the LAN could hand clients a false gateway or DNS server |
| No DHCP rate limiting or port security | A client could exhaust the pool with repeated requests |
| No access control on the DHCP servers | Any device on the segment can request a lease |
| Public DNS server (`8.8.8.8`) given to clients | Fine for a lab. Production networks usually point clients at internal DNS |
| No management hardening | No passwords, SSH or banner were configured in the lab |

These are listed as future improvements.
