# Rapport d’incident — Exécution distante via WMI et PowerShell encodé

## Résumé exécutif

Une activité suspecte a été détectée sur un poste Windows du domaine `corpo.local`. Le processus `WmiPrvSE.exe` a lancé `powershell.exe` avec une commande encodée en Base64, comportement compatible avec une exécution distante via WMI.

## Gravité

Élevée.

## Contexte

WMI est un mécanisme natif d’administration Windows. Son usage pour lancer PowerShell à distance peut être légitime dans certains contextes administratifs, mais constitue aussi une technique fréquemment utilisée pour le mouvement latéral.

## Timeline

| Étape | Événement |
|---|---|
| T0 | Exécution du test WMI |
| T1 | Création du processus `WmiPrvSE.exe` |
| T2 | Lancement de `powershell.exe` |
| T3 | Génération d’un événement Sysmon Event ID 1 |
| T4 | Collecte par Wazuh |
| T5 | Déclenchement de l’alerte |

## Éléments observés

| Champ | Valeur |
|---|---|
| Parent process | WmiPrvSE.exe |
| Child process | powershell.exe |
| Indicateur | Commande encodée Base64 |
| Source log | Sysmon Event ID 1 |
| SIEM | Wazuh |

## Analyse

La relation parent/enfant `WmiPrvSE.exe → powershell.exe` est suspecte dans un contexte utilisateur standard. La présence d’une commande encodée renforce le niveau de suspicion.

Ce comportement peut correspondre à une tentative d’exécution distante ou de mouvement latéral.

## Mapping MITRE

- T1047 — Windows Management Instrumentation
- T1059.001 — PowerShell

## Impact potentiel

- Exécution de code à distance
- Mouvement latéral
- Reconnaissance interne
- Déploiement de charge utile

