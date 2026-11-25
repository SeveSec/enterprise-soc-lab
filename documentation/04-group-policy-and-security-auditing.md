# Phase 4 - Group Policy and Security Auditing

**Status:** In Progress

## Objective

Configure Windows security auditing to establish endpoint
and domain controller visibility in preparation for SIEM
deployment and security monitoring.

## Group Policy Objects

| GPO | Linked OU |
|---|---|
| Workstation - Security Auditing | Workstations |
| Domain Controller - Security Auditing | Domain Controllers |

Dedicated GPOs were created instead of modifying the
default domain policies.

## Workstation Audit Configuration

| Audit Policy | Setting |
|---|---|
| Logon | Success and Failure |
| Logoff | Success |
| Special Logon | Success |
| Process Creation | Success |
| User Account Management | Success and Failure |
| Security Group Management | Success and Failure |
| Audit Policy Change | Success and Failure |
| Sensitive Privilege Use | Success and Failure |
| Security System Extension | Success and Failure |

Additional configurations:

- Advanced audit policy subcategory enforcement.
- Command-line logging for process creation events.

## Policy Verification

Used the following commands to apply and verify Group Policy:

```cmd
gpupdate /force
gpresult /r /scope computer
auditpol /get /category:*
```

## Authentication Event Testing

Generated failed and successful authentication events
on WS01 by intentionally entering an incorrect password
before successfully logging in.

Reviewed the Windows Security log using Event Viewer.

| Timestamp | Event ID | Description |
|---|---|---|
| 19:38:03 | 4625 | Failed logon |
| 19:38:06 | 4625 | Failed logon |
| 19:38:11 | 4624 | Successful logon |

Test date: November 24, 2026.

This confirmed that workstation authentication auditing
was functioning correctly.

Repeated authentication failures followed by a successful
logon can be useful when investigating suspicious
authentication activity. Additional context is required
before classifying such activity as malicious.

## Domain Controller Audit Configuration

| Audit Policy | Setting |
|---|---|
| Credential Validation | Success and Failure |
| Kerberos Authentication Service | Success and Failure |
| Kerberos Service Ticket Operations | Success and Failure |
| User Account Management | Success and Failure |
| Security Group Management | Success and Failure |
| Directory Service Changes | Success and Failure |
| Logon | Success and Failure |
| Special Logon | Success |
| Process Creation | Success |
| Audit Policy Change | Success and Failure |

## Troubleshooting

### Issue

The domain controller audit policies appear in the Group
Policy results report but are not reflected in the
effective audit policy output.

Several configured subcategories continue to display
"No Auditing" when queried using auditpol.

### Troubleshooting Performed

1. Verified that DC01 resides in the Domain Controllers OU.
2. Confirmed that the custom GPO appears under Applied
   Group Policy Objects.
3. Changed the custom GPO to Link Order 1.
4. Generated an HTML Group Policy results report.
5. Confirmed that the custom GPO is the winning policy.
6. Enabled advanced audit policy subcategory enforcement.
7. Verified the SCENoApplyLegacyAuditPolicy registry value
   was set to 0x1.
8. Reviewed the Group Policy Operational event log.
9. Found no visible critical events, errors, or warnings
   in the filtered operational log.

### Diagnostic Commands

```cmd
gpresult /h C:\gpo-report.html /f

reg query HKLM\SYSTEM\CurrentControlSet\Control\Lsa /v SCENoApplyLegacyAuditPolicy

auditpol /get /category:*
```

### Current Status

Unresolved. The GPO is correctly linked and appears in
the Group Policy results report, but the effective
audit configuration does not match the intended settings.

Root cause has not yet been identified.

### Next Steps

- Restart DC01 and verify the effective audit policy.
- Continue investigating security policy processing.
- Identify and document the root cause.
- Verify domain controller security event generation.
- Deploy Sysmon after resolving the auditing issue.

## Lessons Learned

- A GPO appearing as applied does not guarantee that
  every security setting is functioning as intended.
- Effective security controls must be independently verified.
- Group Policy reports, registry values, and event logs
  are useful troubleshooting resources.
- Security event generation should be validated before
  integrating endpoints into a SIEM.
