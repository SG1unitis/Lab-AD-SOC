# Couverture MITRE ATT&CK

## Objectif

Documenter les techniques MITRE ATT&CK simulées dans le lab, les sources de logs utilisées et les règles de détection associées.

| Technique | Nom | Simulation | Source log | Détection | Statut |
|---|---|---|---|---|---|
| T1033 | System Owner/User Discovery | Exécution de `whoami.exe` | Sysmon Event ID 1 | Règle Wazuh custom | Détecté |
| T1003.001 | LSASS Memory | Dump LSASS via `rundll32` / `comsvcs.dll` | Sysmon Event ID 1 | Règle Wazuh custom | Détecté |
| T1047 | Windows Management Instrumentation | Exécution distante via WMI | Sysmon Event ID 1 | Parent `WmiPrvSE.exe` | Détecté |
| T1059.001 | PowerShell | PowerShell encodé Base64 | Sysmon Event ID 1 | CommandLine suspecte | Détecté |
| T1136.001 | Local Account | Création compte local via Atomic Red Team | Sysmon / Security | `net user /add` | Détecté |
| T1078 | Valid Accounts | Tentative sur honeytoken `svc_backup` | Security 4625 | Compte leurre | Détecté |
| T1110 | Brute Force | Multiples échecs de connexion | Security 4625 | Règle Wazuh native/custom | Détecté |

## Analyse

La couverture se concentre sur des techniques Windows pertinentes pour un environnement Active Directory :

- découverte ;
- credential access ;
- mouvement latéral ;
- persistance ;
- abus de comptes ;
- brute-force.

## Limites

Cette matrice ne représente pas une couverture exhaustive de MITRE ATT&CK. Elle documente uniquement les techniques effectivement simulées et observées dans le lab.
