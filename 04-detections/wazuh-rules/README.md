# Règles de détection Wazuh

## Objectif

Ce dossier contient les règles Wazuh personnalisées créées pour détecter les comportements simulés dans le lab.

Les règles sont conçues pour détecter des comportements observables dans les logs Windows/Sysmon, puis les mapper sur MITRE ATT&CK.

## Règles couvertes

| Règle | Comportement détecté | Source | MITRE |
|---|---|---|---|
| whoami | Découverte utilisateur | Sysmon Event ID 1 | T1033 |
| rundll32 LSASS dump | Dump mémoire LSASS | Sysmon Event ID 1 | T1003.001 |
| WMI PowerShell | Exécution distante suspecte | Sysmon Event ID 1 | T1047 / T1059.001 |
| net user add | Création de compte local | Sysmon / Security | T1136.001 |
| svc_backup honeytoken | Usage compte leurre | Security 4625 | T1078 / T1110 |

## Principes de conception

Chaque règle doit préciser :

- le comportement recherché ;
- la source de log utilisée ;
- les champs déclencheurs ;
- le niveau de criticité ;
- le mapping MITRE ;
- les faux positifs possibles.

## Limite

Ces règles sont écrites pour un environnement de lab. En environnement réel, elles nécessiteraient une phase de tuning afin de réduire les faux positifs.
