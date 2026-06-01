# Architecture du lab

## Objectif

Créer un environnement Windows Active Directory isolé permettant de simuler des comportements adverses et de tester une chaîne de détection SOC.

## Composants

| Machine | Rôle | Adresse IP | Description |
|---|---|---|---|
| pfSense | Routeur / pare-feu | 10.0.0.1 | Isolation du lab et accès Internet contrôlé |
| DC01 | Contrôleur de domaine | 10.0.0.5 | Active Directory, DNS, GPO, collecte WEF |
| Windows 10 | Poste utilisateur | DHCP | Poste joint au domaine corpo.local |
| Ubuntu / Wazuh | SIEM | À compléter | Serveur Wazuh pour centralisation et alerting |

## Domaine

- Nom de domaine : `corpo.local`
- Contrôleur de domaine : `DC01`
- Utilisateur de test : `j.dupond`
- Compte honeytoken : `svc_backup`

## Flux principaux

```text
Poste Windows
   ↓ logs Sysmon / Security
WEF / Wazuh Agent
   ↓
Wazuh Manager
   ↓
Alertes / Dashboard / Investigation
