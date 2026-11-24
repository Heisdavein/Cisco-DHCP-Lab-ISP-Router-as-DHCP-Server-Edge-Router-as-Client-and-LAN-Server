# 04 - Edge Router Configuration


The Edge Router does two jobs: it is a DHCP client toward the ISP and a DHCP server for the LAN. Full file: `configs/edge-router.txt`.

## Contents

- WAN interface as DHCP client
- LAN DHCP server
- Verification

## WAN interface as DHCP client

```
interface FastEthernet0/0
 ip address dhcp
 no shutdown
```

`ip address dhcp` makes the interface send a DHCP Discover and take the address the ISP Router offers.


<img width="1024" height="572" alt="image" src="https://github.com/user-attachments/assets/3314a99f-d791-4948-a525-d60c9e3ab9a5" />
 Edge Router CLI showing `ip address dhcp` on `FastEthernet0/0`, and the address the interface received.

## LAN DHCP server

```
interface FastEthernet0/1
 ip address 192.168.1.1 255.255.255.0
 no shutdown
!
ip dhcp excluded-address 192.168.1.1 192.168.1.10
!
ip dhcp pool LAN-POOL
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8
```

- The LAN gateway address is static, since it is the address the clients will use as their default router.
- `.1` to `.10` are excluded so the gateway and any future static devices never collide with leased addresses.

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/29b28ef8-8e4d-4a62-9330-81748fc780b3" />
 Edge Router CLI showing the LAN interface, the exclusion range and `LAN-POOL`.

## Verification

| Command | What to check |
| --- | --- |
| `show ip interface brief` | `Fa0/0` has a leased address, `Fa0/1` has `192.168.1.1`, both up/up |
| `show ip dhcp pool` | `LAN-POOL` shows the network and leases in use |
| `show ip dhcp binding` | PC leases appear with their addresses |


<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/618b8ae5-f6be-4258-8f2e-754d300cd2b8" />
 `show ip interface brief` on the Edge Router.


<img width="1670" height="941" alt="image" src="https://github.com/user-attachments/assets/d3120408-44cd-47c3-b25c-bc3d809525d8" />
 `show ip dhcp pool` on the Edge Router.


<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/9c61f8a0-8343-403f-ae22-769f6cd77347" />
`show ip dhcp binding` on the Edge Router with the PC leases listed.

Next: Testing and Validation
