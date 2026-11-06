
# WINDOWS SID & RID — SOC CHEAT SHEET

*Quick reference for Windows and Active Directory event analysis.*

## 1. Built-in Accounts — RID

| RID | Account | Description |
|---:|---|---|
| **500** | Administrator | Built-in administrator account |
| 501 | Guest | Built-in guest account |
| 502 | krbtgt | Active Directory Kerberos service account |
| 503 | DefaultAccount | Default system-managed account |
| 504 | WDAGUtilityAccount | Windows Defender Application Guard account |

## 2. Active Directory Groups — RID

| RID | Group | Description |
|---:|---|---|
| **512** | Domain Admins | Domain administration |
| 513 | Domain Users | Domain users |
| 514 | Domain Guests | Domain guests |
| 515 | Domain Computers | Domain computers |
| **516** | Domain Controllers | Domain controllers |
| 517 | Cert Publishers | Certificate publishing |
| **518** | Schema Admins | Active Directory schema administration |
| **519** | Enterprise Admins | Forest-wide administration |
| 520 | Group Policy Creator Owners | Group Policy creation and management |
| 521 | Read-only Domain Controllers | RODC accounts |

## 3. Windows Built-in Groups — RID

SID prefix: `S-1-5-32`

| RID | Group | Description |
|---:|---|---|
| **544** | Administrators | Local administrators |
| 545 | Users | Local users |
| 546 | Guests | Local guests |
| 547 | Power Users | Advanced local users |
| 548 | Account Operators | Account management in a domain |
| 549 | Server Operators | Server administration |
| 550 | Print Operators | Printer management |
| 551 | Backup Operators | Backup-related privileges |
| 552 | Replicators | Directory replication |

*Note: Account Operators, Server Operators, Print Operators, and Backup Operators are domain built-in groups. Their RIDs belong to the domain's built-in account domain, not the `S-1-5-32` local alias namespace.*

## 4. Well-known SIDs — Accounts and Logon Contexts

| SID | Identity | Description |
|---|---|---|
| `S-1-1-0` | Everyone | All users |
| `S-1-5-2` | Network | Network logon context |
| `S-1-5-3` | Batch | Batch logon context |
| `S-1-5-4` | Interactive | Interactive logon context |
| `S-1-5-6` | Service | Service logon context |
| `S-1-5-7` | Anonymous | Anonymous logon |
| `S-1-5-11` | Authenticated Users | Authenticated users |
| **`S-1-5-18`** | SYSTEM | Local system account |
| `S-1-5-19` | LOCAL SERVICE | Local service account |
| `S-1-5-20` | NETWORK SERVICE | Network service account |

## 5. Mandatory Integrity Levels

| SID | Level | Description |
|---|---|---|
| `S-1-16-0` | Untrusted | Untrusted integrity level |
| `S-1-16-4096` | Low | Low integrity |
| `S-1-16-8192` | Medium | Standard integrity |
| `S-1-16-8448` | Medium Plus | Medium-plus integrity |
| `S-1-16-12288` | High | High integrity |
| `S-1-16-16384` | System | System integrity |

## 6. SID Anatomy

Example:

`S-1-5-21-3149041863-46454470-2014795773-500`

- `S`: Security Identifier.
- `1`: SID revision.
- `5`: NT Authority.
- `21`: Identifier of a domain or local computer account authority.
- `3149041863-46454470-2014795773`: Unique domain or machine identifier (relative to its issuing authority).
- `500`: RID of the built-in Administrator account.

**Key takeaway:** The RID is the last component of a SID. It identifies an account or group within its issuing authority.

## 7. SOC Priorities — RIDs to Remember

| Priority | RID / SID | Why it matters |
|---|---|---|
| 🔴 | 500 | Built-in Administrator account |
| 🔴 | 512 | Domain Admins |
| 🔴 | 518 | Schema Admins |
| 🔴 | 519 | Enterprise Admins |
| 🔴 | 544 | Local Administrators |
| 🟠 | 502 | krbtgt account |
| 🟠 | 516 | Domain Controllers |
| 🟠 | 551 | Backup Operators |
| 🟠 | `S-1-5-18` | SYSTEM |
| 🟠 | `S-1-5-11` | Authenticated Users |

## 8. Microsoft References

- [Understand Security Identifiers (Microsoft Learn)](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-identifiers)
- [Well-known SIDs (Microsoft Learn)](https://learn.microsoft.com/en-us/windows/win32/secauthz/well-known-sids)

*Note: A RID alone is not sufficient to identify an account or group. Always consider the complete SID and its local or Active Directory context.*
