# 03 - ISP Router Configuration

The ISP Router acts as the DHCP server for the WAN segment. Full file: `configs/isp-router.txt`.

## Contents

- Configuration
- Why it is built this way
- Verification

## Configuration

```
interface GigabitEthernet0/0/0
 ip address 200.1.1.1 255.255.255.0
 no shutdown
!
ip dhcp excluded-address 200.1.1.1
!
ip dhcp pool ISP-POOL
 network 200.1.1.0 255.255.255.0
 default-router 200.1.1.1
 dns-server 8.8.8.8
!
end
write memory
```

<img width="1024" height="572" alt="image" src="https://github.com/user-attachments/assets/12c89bce-41e9-4171-a42a-eaac9b836384" />
 ISP Router CLI showing the interface address, the excluded address and the `ISP-POOL` configuration.

## Why it is built this way

- The interface address is set by hand because the router is the server. It cannot lease an address to itself.
- `ip dhcp excluded-address 200.1.1.1` keeps the router’s own address out of the pool, which prevents an IP conflict.
- `no shutdown` brings the interface up. Interfaces on Cisco routers are down by default.
- `write memory` saves the running configuration to the startup configuration so it survives a reload.

## Verification

| Command | What to check |
| --- | --- |
| `show ip interface brief` | `GigabitEthernet0/0/0` has `200.1.1.1` and is up/up |
| `show ip dhcp pool` | `ISP-POOL` exists, with the network and lease counts |
| `show ip dhcp binding` | The Edge Router’s WAN lease appears here |


<img width="1024" height="572" alt="image" src="https://github.com/user-attachments/assets/787c8f7d-df3f-4903-9f84-ff1a0cdc3bc9" />
`show ip interface brief` on the ISP Router.


<img width="1024" height="572" alt="image" src="https://github.com/user-attachments/assets/5e39f177-1841-46f4-a89a-0caa94f44cb9" />
 `show ip dhcp pool` on the ISP Router.


<img width="1024" height="572" alt="image" src="https://github.com/user-attachments/assets/9013e954-3357-4f0b-b154-2fd5cf01c996" />
 `show ip dhcp binding` on the ISP Router after the Edge Router has leased an address.


Next: Edge Router Configuration
