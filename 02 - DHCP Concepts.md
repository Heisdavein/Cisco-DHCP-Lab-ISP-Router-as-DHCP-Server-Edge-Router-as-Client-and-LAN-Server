# 02 - DHCP Concepts

Background the lab relies on. This is the theory behind the configuration, not a record of results.

## Contents

- What DHCP does
- The DORA process
- Ways to assign addresses
- IOS pieces used in the lab

## What DHCP does

DHCP gives a device its network settings automatically: IP address, subnet mask, default gateway and DNS server. Doing this by hand does not scale, and typing the same address on two devices causes an IP conflict.

## The DORA process

| Step | Message | Direction |
| --- | --- | --- |
| D | Discover | Client broadcasts a request for a DHCP server |
| O | Offer | Server proposes an address and settings |
| R | Request | Client asks to use the offered address |
| A | Acknowledge | Server confirms the lease |

## Ways to assign addresses

| Method | Used when | Trade-off |
| --- | --- | --- |
| Static | A few fixed devices such as routers and servers | No dependency on a server, but manual and easy to duplicate |
| Router as DHCP server | Small networks with no dedicated server (this lab) | Simple to set up. Limited features compared with a dedicated server |
| Dedicated DHCP server | Larger networks | Central management, more control |

## IOS pieces used in the lab

| Piece | Purpose |
| --- | --- |
| `ip address dhcp` | Makes an interface a DHCP client |
| `ip dhcp excluded-address` | Keeps addresses out of the pool so they are never leased |
| `ip dhcp pool <name>` | Creates a pool and enters DHCP configuration mode |
| `network` | Address range the pool hands out |
| `default-router` | Gateway given to clients |
| `dns-server` | DNS server given to clients |

Next: ISP Router Configuration
