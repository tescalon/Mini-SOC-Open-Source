# 🛡️ Déploiement d'un SOC Open Source Pédagogique (LAB CYBER)

[![Statut du Projet](https://img.shields.io/badge/Statut-En%20Cours-orange)](./documentation/objectifs.md)
[![Technologies Principales](https://img.shields.io/badge/Tech-SIEM%20(ELK)%2C%20CTI%20(OpenCTI)%2C%20SOAR%20(TheHive%2FCortex)-blue)](./documentation/architecture.md)
[![Focus Technique](https://img.shields.io/badge/Focus-Cybers%C3%A9curit%C3%A9%20Avanc%C3%A9-red)](./documentation/rapport_technique.md)

## 🎯 Objectif du Projet

Ce projet vise à mettre en place une **chaîne complète de gestion des événements de sécurité** (SIEM, SOAR et Threat Intelligence) en environnement de laboratoire. L'objectif est de simuler les fonctions d'un **SOC léger** pour la détection, la corrélation et l'investigation des menaces (Brute Force, Scans, etc.) dans un cadre pédagogique et non-productif.

Ce lab permet de maîtriser l'intégration de solutions Open Source, de pratiquer la réponse aux incidents (IR - Incident Response) et d'appliquer les principes du **GRC (Gouvernance, Risque et Conformité)** en matière de sécurité des systèmes d'information.

---

## 🗺️ Architecture Fonctionnelle du LAB

Le laboratoire est segmenté en trois zones principales pour isoler les composants : Internet (Zone Rouge), la Zone d'Administration/Gestion (Zone Jaune) et la Zone Protégée (Zone Verte).

### ➡️ Schéma d'Architecture



### ➡️ Composants Réseau et Adressage (Niveau 3)

| Élément | Rôle | Adresse IP | Sous-réseau | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **Box Internet** | Routeur/Passerelle vers le WAN | `192.168.1.XX` | `/24` | Accès Internet pour Kali et la box du lab. |
| **PC A (Hôte VMware)** | Hôte de tous les services SOC (Docker) | `192.168.10.2` | `/24` (LAN OPNsense) | Serveur des composants Wazuh, TheHive, Cortex, OpenCTI. |
| **OPNsense (WAN)** | Point d'entrée de la zone protégée | `192.168.1.X` | `/24` | Se connecte au même segment que la Box. |
| **OPNsense (LAN)** | Pare-feu de la zone cible | `192.168.10.1` | `/24` | Passerelle de tous les PC protégés. |
| **PC B (Debian Cible)** | Système d'information protégé | `192.168.10.3` | `/24` | Équipé d'un agent Wazuh pour la collecte de logs. |
| **Kali Attaquant** | Machine simulant les menaces (externe) | IP publique ou NAT | N/A | Simule des attaques provenant d'Internet. |

---

## 🛠️ Stack Technologique (Composants Clés du SOC)

L'ensemble de la plateforme SOC est déployé et orchestré via **Docker/Docker-Compose** sur le **PC A (Hôte VMware)** pour garantir une portabilité et une gestion simplifiée.

| Composant | Rôle Sécurité | Fonctionnalités Clés |
| :--- | :--- | :--- |
| **OPNsense + Suricata** | **Firewall & IDS/IPS** | Séparation des zones, filtrage de flux (ACL), détection d'intrusion (Suricata). |
| **Wazuh** | **SIEM / Corrélation** | Collecte centralisée des logs (Système, applicatif), détection d'anomalies, corrélation des événements (ex: tentatives SSH/RDP multiples). |
| **TheHive** | **Gestion d'Incidents (SOAR léger)** | Plateforme collaborative pour l'investigation, gestion du workflow des alertes, ticketing et documentation. |
| **Cortex** | **Enrichissement & Analyse** | Moteur d'exécution des *Analyzers* (ex: VirusTotal, Shodan, Whois) pour enrichir les observations d'incidents transmises par TheHive. |
| **OpenCTI** | **Threat Intelligence (CTI)** | Centralisation et visualisation des IOCs (Indicators of Compromise), cartographie de la menace via le framework MITRE ATT&CK. |
| **Docker / Portainer** | **Orchestration & Administration** | Déploiement rapide et gestion des conteneurs pour garantir l'homogénéité de l'environnement applicatif. |

<p align="center">
<img width="650" src="https://github.com/tescalon/Mini-SOC-open-source/blob/main/Architecture%20r%C3%A9elle.png" alt="Architecture réelle" />
</p>
---

## ✅ Compétences Démontrées

Ce projet couvre des aspects critiques de la Cybersécurité et du GRC, valorisant les compétences suivantes pour une alternance en Bac+5 :

* **Architecture Sécurité :** Maîtrise de la segmentation réseau (LAN/WAN) et du rôle des firewalls/IDS/IPS.
* **Administration Système :** Déploiement et gestion d'environnements virtualisés (VMware) et conteneurisés (Docker).
* **Opérations de Sécurité (SecOps) :** Configuration d'agents de collecte (Wazuh Agents), corrélation de logs et gestion des faux positifs.
* **Gestion des Incidents :** Utilisation des plateformes TheHive et Cortex pour l'investigation structurée et la prise de décision.
* **Threat Intelligence :** Intégration et utilisation de la CTI via OpenCTI pour contextualiser les attaques.

Ce lab sert de base pour l'étude et l'application des procédures de sécurité, un pilier essentiel pour un métier dans la cybersécurité ( que ça soit dans la sécurité défensive ou la GRC).

---

**Le projet est actuellement en cours de réalisation. La documentation détaillée de l'architecture, de la configuration et des analyses de sécurité sera mise à jour et publiée dans les prochains jours / semaines / mois.**
