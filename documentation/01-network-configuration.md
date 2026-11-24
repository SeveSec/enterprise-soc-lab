# Phase 1 - Network Configuration

## Objective

Configure an isolated virtual network to simulate a small
enterprise environment for cybersecurity testing.

## Virtual Machines

| Machine | RAM | CPU Cores | Storage |
|---|---|---|---|
| Windows Server 2019 | 4 GB | 2 | 60 GB |
| Windows 11 Pro | 4 GB | 2 | 80 GB |
| Kali Linux | 2 GB | 4 | 80 GB |

## Network Configuration

- Hypervisor: VMware Workstation
- Virtual Network: VMnet1
- Network Type: Host-only
- Subnet: 192.168.213.0/24
- Subnet Mask: 255.255.255.0
- Default Gateway: None

| Machine | IP Address | DNS Server |
|---|---|---|
| DC01 | 192.168.213.10 | 192.168.213.10 |
| WS01 | 192.168.213.20 | 192.168.213.10 |

## Troubleshooting

### Issue

Windows 11 was unable to ping the Windows Server,
resulting in request timeouts.

### Resolution

Created a custom inbound rule using Windows Defender
Firewall with Advanced Security on DC01.

| Firewall Setting | Value |
|---|---|
| Rule Name | Lab - Allow ICMPv4 Ping |
| Direction | Inbound |
| Protocol | ICMPv4 |
| ICMP Type | Echo Request |
| Remote Scope | 192.168.213.0/24 |
| Action | Allow |
| Profiles | Domain, Private, Public |

### Results

Successfully established ICMP connectivity from
Windows 11 to Windows Server without disabling
Windows Defender Firewall.

## Lessons Learned

- Host-only networking isolates virtual machines from external networks.
- Static IP addressing provides consistent network identification.
- Host-based firewalls can block traffic despite correct IP configurations.
- Restricting firewall rules to necessary traffic follows the principle of least privilege.
