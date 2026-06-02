# T1136.001 — Création de compte local

## Objectif

Détecter la création suspecte d’un compte local, comportement compatible avec une tentative de persistance.

## Contexte

Après une compromission initiale, un attaquant peut créer un compte local afin de conserver un accès au système. L’utilisation de `net.exe` est intéressante à surveiller car il s’agit d’un binaire natif Windows.

## Simulation

Un test Atomic Red Team est utilisé pour simuler la création d’un compte local.

Technique testée : T1136.001 — Create Account: Local Account


Télémétrie attendue :

|Élément	| Valeur
|---|---|
| Source |	Sysmon / Security
| Processus |	net.exe
| Arguments |	user /add
| Event ID possible |	4720
| SIEM	| Wazuh

## Logique de détection

Déclencher une alerte lorsque net.exe est exécuté avec les arguments suivants :

- user
/add
## Mapping MITRE
- T1136.001 — Create Account: Local Account

## Faux positifs possibles
- Création légitime d’un compte par un administrateur
- Script d’administration
- Déploiement ou maintenance système

## Réduction du bruit
- Vérifier l’utilisateur ayant exécuté la commande
- Vérifier l’heure d’exécution
- Corréler avec un ajout au groupe Administrateurs
- Contrôler le nom du compte créé
- Vérifier le parent process

## Résultat
Après exécution du scénario Atomic Red Team, Wazuh détecte la commande liée à la création du compte local.
