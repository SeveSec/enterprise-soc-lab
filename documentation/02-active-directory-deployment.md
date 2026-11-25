# Phase 2 - Active Directory Deployment

## Objective

Deploy Active Directory Domain Services and DNS to establish
a centralized authentication and management environment.

## Domain Configuration

| Setting | Value |
|---|---|
| Domain Controller | DC01 |
| Operating System | Windows Server 2019 |
| Domain | homelab.test |
| NetBIOS Name | HOMELAB |
| IP Address | 192.168.213.10 |
| Forest Functional Level | Windows Server 2016 |
| Domain Functional Level | Windows Server 2016 |
| DNS Server | Enabled |
| Global Catalog | Enabled |

## Implementation

- Installed Active Directory Domain Services.
- Promoted DC01 to a domain controller.
- Created a new Active Directory forest.
- Configured integrated DNS services.
- Verified the domain using Active Directory Users and Computers.

## Workstation Domain Join

Joined the Windows 11 Pro workstation (WS01) to homelab.test.

Verified that WS01 appeared in the Computers container
in Active Directory.

## Results

Successfully established an Active Directory domain
with a domain-joined Windows 11 workstation.

## Lessons Learned

- The difference between a forest, domain, and domain controller.
- Proper DNS configuration is essential for domain discovery, authentication, and joining computers to Active Directory.
- The process of joining endpoints to a centralized domain.

