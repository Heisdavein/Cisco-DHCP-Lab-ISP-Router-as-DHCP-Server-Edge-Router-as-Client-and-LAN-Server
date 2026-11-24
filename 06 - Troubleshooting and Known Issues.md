# 06 - Troubleshooting and Known Issues

## Contents

- Approach
- Common symptoms
- Inconsistencies in the source documentation

## Approach

Work up the stack and check both ends of every link:

1. Layer 1: cables and port lights.
2. Layer 2: interface status (`show ip interface brief` should show up/up).
3. Layer 3: addresses, masks and gateways.
4. Services: DHCP pool, exclusions and bindings.

## Common symptoms

| Symptom | Likely cause | Check |
| --- | --- | --- |
| Interface shows administratively down | `no shutdown` missing | `show ip interface brief` |
| Edge WAN interface has no address | ISP pool missing, interface down on either side, or `ip address dhcp` not set | `show ip dhcp binding` on the ISP Router |
| PC has no address or a `169.254.x.x` address | DHCP not enabled on the PC, LAN interface down, or pool missing | `ipconfig /all`, `show ip dhcp pool` |
| Duplicate address | Gateway or static device inside the pool range | `show ip dhcp pool`. Check `ip dhcp excluded-address` |
| First ping times out | ARP resolving the next hop | Repeat the ping |
| Configuration gone after reload | `write memory` not run | `show startup-config` |

The lab documentation records three troubleshooting problems. Add the exact wording and your captures here if you want them listed individually.

## Inconsistencies in the source documentation

Recorded so the repository stays honest about what the lab actually shows.

| Item | Detail |
| --- | --- |
| PC ports | The text says PC1 and PC2 connect to Edge `Fa0/1` and `Fa0/2`. Only `Fa0/1` is configured as the LAN interface and no switch is described |
| LAN range | An infographic mentions `192.168.1.11 - 192.168.1.100`. The pool configuration uses the whole /24 with `.1` to `.10` excluded |
| Return path | A ping from a PC to the ISP Router is recorded as successful, but no NAT or return route is documented |
| Lease details | Timestamps and MAC values in the infographics are illustrative and are not used as evidence here |
| Numbering | Some sections of the source repeat content, and one sub-section number appears twice |
| Author name | The cover shows two spellings of the name |

Next: Security Considerations
