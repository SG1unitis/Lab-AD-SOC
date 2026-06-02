# LAPS — Gestion des mots de passe administrateurs locaux

## Objectif

Déployer LAPS afin d’éviter la réutilisation d’un même mot de passe administrateur local sur plusieurs postes.

## Risque traité

Sans LAPS, un attaquant qui compromet le mot de passe administrateur local d’un poste peut tenter de le réutiliser sur d’autres machines du domaine.

## Mise en œuvre

- Extension du schéma Active Directory
- Installation du module PowerShell LAPS
- Délégation des permissions sur l’OU cible
- Création de la GPO `SEC_LAPS_Policy`
- Déploiement du client LAPS sur le poste utilisateur
- Validation de la rotation du mot de passe local

## Résultat

Le poste utilisateur dispose d’un mot de passe administrateur local unique, complexe et automatiquement renouvelé.

## Apport sécurité

- Réduction du risque de mouvement latéral
- Limitation de la réutilisation de credentials locaux
- Meilleure hygiène d’administration Windows
