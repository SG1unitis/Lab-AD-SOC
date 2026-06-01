# Télémétrie — Sysmon, WEF et Wazuh

## Objectif

Mettre en place une chaîne de collecte permettant de capturer les événements Windows pertinents et de les centraliser dans Wazuh.

## Chaîne de collecte

```text
Windows endpoint
    ↓
Sysmon / Windows Security logs
    ↓
WEF ou agent Wazuh
    ↓
Wazuh Manager
    ↓
Alertes / Dashboard / Investigation
```
# Sysmon

Sysmon est utilisé pour enrichir la visibilité sur le poste Windows, notamment :


- création de processus ;
- ligne de commande complète ;
- processus parent ;
- connexions réseau ;
- création de fichiers suspects.
- Événements utiles

```text
Source	Event ID	Utilité
Sysmon	     1	    Création de processus
Sysmon	     3	    Connexion réseau
Security	4624	Connexion réussie
Security	4625	Connexion échouée
Security	4720	Création de compte utilisateur
Security	4732	Ajout à un groupe local
```

## WEF

WEF permet de centraliser les événements Windows vers DC01 sans agent tiers.

# Wazuh

Wazuh est utilisé comme SIEM open-source pour :

- collecter les événements ;
- appliquer des règles ;
- générer des alertes ;
- visualiser les techniques MITRE détectées.
### Résultat

La chaîne permet d’observer les comportements simulés dans le lab et de déclencher des alertes exploitables dans Wazuh.
