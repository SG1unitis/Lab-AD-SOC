# T1047 — WMI + PowerShell encodé

## Objectif

Détecter une exécution distante suspecte via Windows Management Instrumentation.

## Contexte

WMI est un composant natif de Windows utilisé pour l’administration locale et distante. Il peut être détourné par un attaquant pour exécuter du code sur une machine cible sans déposer d’outil externe.

Dans ce scénario, l’anomalie recherchée est la relation parent/enfant suivante :

```text
WmiPrvSE.exe → powershell.exe
```
## Simulation

Une commande distante est exécutée via wmic, provoquant le lancement d’un processus PowerShell encodé en Base64 sur la machine cible.

Télémétrie attendue
```text
Source	Sysmon
Event ID	1
ParentImage	WmiPrvSE.exe
Image	powershell.exe
Indicateur	Commande encodée Base64
```
## Logique de détection
La règle recherche une relation parent/enfant suspecte :

- ParentImage contient WmiPrvSE.exe
- Image contient powershell.exe ou cmd.exe
- CommandLine contient -enc ou -encodedcommand
 
## Mapping MITRE
- T1047 — Windows Management Instrumentation
- T1059.001 — PowerShell

## Faux positifs possibles
- Scripts d’administration distante légitimes
- Outils de supervision utilisant WMI
- Maintenance système automatisée
  
## Réduction du bruit
- Exclure les comptes d’administration connus
- Corréler avec l’horaire d’exécution
- Vérifier la machine source
- Contrôler la présence d’autres événements suspects autour de l’alerte
  
## Résultat

Wazuh a collecté l’événement Sysmon et déclenché une alerte de criticité élevée. Le log permet d’identifier le processus parent, le processus enfant et la ligne de commande utilisée.
