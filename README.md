# AD/SOC Detection Lab — Windows Detection Engineering

## Objectif
Construire un environnement Active Directory réaliste afin de simuler des comportements offensifs, collecter la télémétrie Windows, créer des règles de détection et produire des analyses SOC exploitables.

## Architecture
- pfSense : segmentation réseau et isolation du lab
- DC01 : contrôleur de domaine Active Directory
- Windows 10 : poste utilisateur joint au domaine
- Sysmon : télémétrie avancée Windows
- WEF : centralisation des logs Windows
- Wazuh : SIEM open-source
- Atomic Red Team : simulation contrôlée de techniques adverses

## Compétences démontrées
- Administration Active Directory
- Durcissement Windows par GPO
- Déploiement Sysmon
- Collecte et centralisation de logs
- Création de règles Wazuh
- Détection de comportements suspects
- Mapping MITRE ATT&CK
- Analyse d’incident
- Réduction des faux positifs

## Scénarios couverts
| Scénario | Technique MITRE | Source log | Détection |
|---|---|---|---|
| Brute-force Windows | T1110 | Security 4625 | Wazuh |
| Honeytoken svc_backup | T1078 / T1110 | Security 4625 | Wazuh |
| whoami.exe | T1033 | Sysmon Event ID 1 | Règle custom |
| LSASS dump via rundll32 | T1003.001 | Sysmon Event ID 1 | Règle custom |
| WMI + PowerShell encodé | T1047 / T1059.001 | Sysmon Event ID 1 | Règle custom |
| Création compte local | T1136.001 | Sysmon / Security | Atomic Red Team + Wazuh |

## Résultats
- Collecte Sysmon fonctionnelle
- Logs centralisés dans Wazuh
- Alertes déclenchées sur comportements simulés
- Règles personnalisées mappées MITRE
- Rapports d’incident rédigés pour les scénarios critiques

## Limites
Ce lab reste un environnement réduit. Les règles nécessitent une phase de tuning en environnement réel afin de réduire les faux positifs.
