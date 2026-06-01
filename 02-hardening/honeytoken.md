# Honeytoken — Compte leurre svc_backup

## Objectif

Créer un compte leurre destiné à détecter une tentative d’authentification suspecte dans l’environnement Active Directory.

## Principe

Un compte honeytoken ne doit jamais être utilisé dans un fonctionnement normal. Toute tentative d’authentification sur ce compte est donc considérée comme suspecte.

## Configuration

- Compte créé : `svc_backup`
- Description volontairement attractive : `Domain Admin`
- Aucun usage opérationnel légitime
- Surveillance des échecs d’authentification

## Télémétrie attendue

| Élément | Valeur |
|---|---|
| Event ID | 4625 |
| Compte ciblé | svc_backup |
| Source | Windows Security logs |
| SIEM | Wazuh |

## Logique de détection

Déclencher une alerte lorsqu’un événement d’échec d’authentification concerne le compte `svc_backup`.

## Mapping MITRE

- T1078 — Valid Accounts
- T1110 — Brute Force

## Faux positifs

Très faibles. Le compte n’a aucune raison d’être utilisé légitimement.

## Intérêt SOC

Cette détection permet d’identifier rapidement une tentative de reconnaissance ou d’usage de credentials internes.
