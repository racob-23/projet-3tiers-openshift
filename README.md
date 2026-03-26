# Projet 3-tiers — Déploiement sur OpenShift Virtualization

## Description
Déploiement d'une architecture réseau 3-tiers virtualisée sur OpenShift.
Architecture composée d'une passerelle/firewall, d'un serveur web et d'un serveur de base de données.

## Architecture
- **VM1 - Firewall** : passerelle Internet, iptables, IP 192.168.100.1 (DMZ) et 192.168.10.1 (LAN)
- **VM2 - Serveur Web** : Nginx + Node.js, IP 192.168.100.10 (DMZ)
- **Pod - MySQL** : base de données, zone LAN isolée

## Réseaux
- **DMZ** : 192.168.100.0/24 — serveur web exposé
- **LAN** : 192.168.10.0/24 — base de données protégée
- **Internet** → VM1 firewall → DMZ → Web → LAN

## Règles réseau
- Internet accède uniquement au serveur web (port 80/443)
- La BD n'est pas accessible depuis Internet
- Le LAN accède au web et à Internet via le firewall

## Technologies
- OpenShift Virtualization (KubeVirt)
- Fedora Linux (VMs)
- Nginx + Node.js (serveur web)
- MySQL 8.0 (base de données)
- iptables (firewall)
- NetworkPolicy (isolation réseau)

## Fichiers
- `vm1-firewall.yaml` — VM passerelle/firewall
- `vm2-web.yaml` — VM serveur web
- `mysql-deployment.yaml` — Déploiement MySQL + Service
- `networkpolicies.yaml` — Politiques réseau LAN/DMZ
