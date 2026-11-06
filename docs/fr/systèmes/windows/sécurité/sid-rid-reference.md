# WINDOWS SID & RID — SOC CHEAT SHEET

*Référence rapide pour l'analyse des événements Windows et Active Directory.*

## 1. Comptes intégrés — RID

| RID | Compte | Description |
|---:|---|---|
| **500** | Administrator | Administrateur intégré |
| 501 | Guest | Invité intégré |
| 502 | krbtgt | Compte Kerberos AD |
| 503 | DefaultAccount | Compte système par défaut |
| 504 | WDAGUtilityAccount | Windows Defender Application Guard |

## 2. Groupes Active Directory — RID

| RID | Groupe | Description |
|---:|---|---|
| **512** | Domain Admins | Administration du domaine |
| 513 | Domain Users | Utilisateurs du domaine |
| 514 | Domain Guests | Invités du domaine |
| 515 | Domain Computers | Ordinateurs du domaine |
| **516** | Domain Controllers | Contrôleurs de domaine |
| 517 | Cert Publishers | Publication de certificats |
| **518** | Schema Admins | Administration du schéma AD |
| **519** | Enterprise Admins | Administration de la forêt |
| 520 | Group Policy Creator Owners | Création de GPO |
| 521 | Read-only Domain Controllers | RODC |

## 3. Groupes intégrés Windows — RID

Préfixe SID : `S-1-5-32`

| RID | Groupe | Description |
|---:|---|---|
| **544** | Administrators | Administrateurs locaux |
| 545 | Users | Utilisateurs locaux |
| 546 | Guests | Invités locaux |
| 547 | Power Users | Utilisateurs avancés |
| 548 | Account Operators | Gestion de comptes AD |
| 549 | Server Operators | Administration des serveurs |
| 550 | Print Operators | Gestion des imprimantes |
| 551 | Backup Operators | Privilèges de sauvegarde |
| 552 | Replicators | Réplication |

## 4. Well-known SIDs — Comptes et contextes

| SID | Identité | Description |
|---|---|---|
| `S-1-1-0` | Everyone | Tout le monde |
| `S-1-5-2` | Network | Accès réseau |
| `S-1-5-3` | Batch | Connexion batch |
| `S-1-5-4` | Interactive | Connexion interactive |
| `S-1-5-6` | Service | Contexte service |
| `S-1-5-7` | Anonymous | Connexion anonyme |
| `S-1-5-11` | Authenticated Users | Utilisateurs authentifiés |
| **`S-1-5-18`** | SYSTEM | Système local |
| `S-1-5-19` | LOCAL SERVICE | Service local |
| `S-1-5-20` | NETWORK SERVICE | Service réseau |

## 5. Mandatory Integrity Levels

| SID | Niveau | Description |
|---|---|---|
| `S-1-16-0` | Untrusted | Non fiable |
| `S-1-16-4096` | Low | Faible |
| `S-1-16-8192` | Medium | Standard |
| `S-1-16-8448` | Medium Plus | Intermédiaire |
| `S-1-16-12288` | High | Élevé |
| `S-1-16-16384` | System | Système |
| `S-1-16-20480` | Protected Process | Processus protégé |

## 6. Anatomie d'un SID

Exemple :

`S-1-5-21-3149041863-46454470-2014795773-500`

- `S` : identifiant de sécurité.
- `1` : version du SID.
- `5` : autorité NT.
- `21` : identifiant de domaine ou de machine.
- `3149041863-46454470-2014795773` : identifiant unique du domaine ou de la machine.
- `500` : RID du compte Administrator.

**À retenir :** le RID est la dernière partie du SID. Il identifie le compte ou groupe dans son périmètre.

## 7. Priorités SOC — Les RID à mémoriser

| Priorité | RID / SID | Pourquoi ? |
|---|---|---|
| 🔴 | 500 | Compte Administrator |
| 🔴 | 512 | Domain Admins |
| 🔴 | 518 | Schema Admins |
| 🔴 | 519 | Enterprise Admins |
| 🔴 | 544 | Administrateurs locaux |
| 🟠 | 502 | Compte krbtgt |
| 🟠 | 516 | Domain Controllers |
| 🟠 | 551 | Backup Operators |
| 🟠 | S-1-5-18 | SYSTEM |
| 🟠 | S-1-5-11 | Authenticated Users |

## 8. Ressources Microsoft

- https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-identifiers
- https://learn.microsoft.com/en-us/windows/win32/secauthz/well-known-sids

*Note : un RID seul ne suffit pas à identifier un compte. Toujours considérer le SID complet et son contexte local ou Active Directory.*
