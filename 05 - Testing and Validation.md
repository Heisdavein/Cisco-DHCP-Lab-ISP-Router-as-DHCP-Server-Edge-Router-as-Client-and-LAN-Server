# 05 - Testing and Validation


The lab was verified layer by layer: interfaces first, then DHCP state, then connectivity. Compare this page with your own captures before publishing. It describes what the lab documentation records and nothing more.

## Contents

- Test order
- Client lease check
- Connectivity tests
- Not tested

## Test order

1. Interfaces up/up on both routers (`show ip interface brief`).
2. Edge Router WAN interface has a leased address and appears in the ISP Router’s `show ip dhcp binding`.
3. PCs set to obtain an address automatically, then checked with `ipconfig /all`.
4. Pings between the PCs, the Edge Router and the ISP Router.

## Client lease check

Each PC should show an address in `192.168.1.0/24` outside `.1` to `.10`, mask `255.255.255.0`, gateway `192.168.1.1` and DNS `8.8.8.8`.

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/a9acaf8b-97e8-407b-83e8-f3e5c9f3d832" />
  `ipconfig /all` on PC1 showing DHCP enabled and the leased settings.

<img width="1670" height="941" alt="image" src="https://github.com/user-attachments/assets/c7a7d87f-9783-432f-bb69-c78f5d82286b" />
`ipconfig /all` on PC2 showing DHCP enabled and the leased settings.



## Connectivity tests

| Test | Purpose |
| --- | --- |
| PC to Edge Router LAN address `192.168.1.1` | Confirms the LAN and default gateway |
| PC to ISP Router `200.1.1.1` | Confirms the path across the WAN. The lab records this ping as successful |
| Edge Router to ISP Router | Confirms the DHCP-leased WAN link |

In Packet Tracer the first ping can time out while ARP resolves the next hop. Later replies succeed. This is expected behaviour, not a fault.


<img width="1671" height="941" alt="image" src="https://github.com/user-attachments/assets/35f34dba-579b-4353-aa5b-a892c29b3aa2" />
 Ping from a PC to `192.168.1.1` (only if you captured it).


<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/5eab6ab6-f449-4dc3-9f28-527b96397d97" />
 Ping from a PC to `200.1.1.1`.


<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/10681c06-2fb6-4769-9756-e00a36a83e79" />
Ping from the Edge Router to `200.1.1.1` (only if you captured it).

## Not tested

The lab does not cover these, and none is claimed:

- Lease renewal and expiry
- DHCP relay
- More than two clients, or a switch in the LAN
- DNS resolution through `8.8.8.8`
- NAT or internet access beyond the ISP Router
- DHCP snooping or other DHCP security features
- Real hardware

Next: Troubleshooting and Known Issues
