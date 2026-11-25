# Phase 3 - Enterprise Active Directory Environment

## Objective

Simulate a small enterprise environment using organizational
units, employee accounts, and role-based security groups.

## Organizational Unit Structure

    homelab.test
    ├── Employees
    │   ├── IT
    │   ├── Human Resources
    │   ├── Finance
    │   └── Sales
    ├── Workstations
    ├── Servers
    ├── Security Groups
    ├── Service Accounts
    └── Administrators

## Employee Accounts

| Employee | Username | Department |
|---|---|---|
| Will Welch | will.welch | IT |
| Gabe Day | gabe.day | IT |
| Sarah Johnson | sarah.johnson | Human Resources |
| Emily Davis | emily.davis | Human Resources |
| Michael Johnson | michael.johnson | Finance |
| Steve Smith | steve.smith | Finance |
| David Anderson | david.anderson | Sales |
| Ashley Brown | ashley.thomas | Sales |

All employee accounts represent fictional individuals.

## Security Groups

| Group | Scope | Type |
|---|---|---|
| SG-IT | Global | Security |
| SG-HR | Global | Security |
| SG-Finance | Global | Security |
| SG-Sales | Global | Security |

The SG- naming convention was selected to maintain
consistency and simplify group identification.

## Computer Management

Moved WS01 from the default Computers container
to the Workstations OU to support targeted Group Policy
configuration.

DC01 remains in the default Domain Controllers OU.

## Security Considerations

- Principle of least privilege.
- Role-based access control (RBAC).
- Separation of standard and administrative accounts.
- Protection of OUs from accidental deletion.

## Lessons Learned

- Differences between containers and organizational units.
- Active Directory group scopes and types.
- Organizing directory objects for targeted Group Policy.
- Assigning permissions through security groups rather than individual accounts simplifies access management and improves scalability.
