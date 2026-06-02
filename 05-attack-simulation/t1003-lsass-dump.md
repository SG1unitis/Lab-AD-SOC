# T1003.001 — Dump LSASS via rundll32

## Objectif

Détecter une tentative de dump mémoire du processus LSASS à l’aide d’un binaire Windows natif.

## Contexte

LSASS stocke des éléments sensibles liés à l’authentification. Un attaquant peut tenter de dumper sa mémoire afin d’extraire des identifiants ou des secrets d’authentification.

Dans ce scénario, l’attaquant abuse de `rundll32.exe` et de `comsvcs.dll` pour déclencher une fonction de dump mémoire.

## Simulation

Exécution d’une commande utilisant `rundll32.exe` avec `comsvcs.dll` et `MiniDump`.

## Télémétrie attendue

| Élément | Valeur |
|---|---|
| Source | Sysmon |
| Event ID | 1 |
| Image | rundll32.exe |
| CommandLine | comsvcs.dll |
| CommandLine | MiniDump |
| Cible | LSASS |

## Logique de détection

La règle ne doit pas détecter tout usage de `rundll32.exe`, car ce binaire est utilisé légitimement par Windows.

La détection doit cibler la combinaison :

- `rundll32.exe`
- `comsvcs.dll`
- `MiniDump`

## Mapping MITRE

- T1003.001 — OS Credential Dumping: LSASS Memory

## Faux positifs possibles

Faibles : la règle exige simultanément `rundll32.exe`, `comsvcs.dll` et `MiniDump`.

## Réduction du bruit

- Ne pas alerter sur `rundll32.exe` seul
- Contrôler la ligne de commande complète
- Vérifier le chemin du fichier de sortie
- Corréler avec les droits du compte utilisateur

## Résultat

L’événement Sysmon permet d’identifier la tentative de dump via la ligne de commande complète. Une règle Wazuh personnalisée peut déclencher une alerte sur cette combinaison.
