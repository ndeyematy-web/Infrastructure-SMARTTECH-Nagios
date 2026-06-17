# 🖥️ Infrastructure SMARTTECH DSI — Supervision Nagios4

> Déploiement d'une infrastructure réseau complète avec supervision Nagios4  
> Rapport TP — ESTM Dakar | L3 Réseaux & Télécommunications | 2025-2026  
> Réalisé en binôme : **Ndeye Maty GUEYE** & **Fatima DIBA**

---

## 📌 Description

Déploiement et supervision d'une infrastructure réseau complète pour la **DSI SMARTTECH** (Diamniadio) sur Ubuntu 24.04 LTS virtualisé sous VMware. L'infrastructure intègre DNS, Web, SSH, base de données, FTP, SNMP, journalisation centralisée et supervision Nagios4.

---

## 🏗️ Environnement

| Paramètre | Valeur |
|-----------|--------|
| Hostname | srv.smarttech.sn |
| OS | Ubuntu 24.04.4 LTS |
| Virtualisation | VMware Workstation |
| IP VM | 192.168.1.252/24 |

---

## ✅ Services déployés

### TP1 — Infrastructure SMARTTECH (domaine smarttech.sn)

| Service | Technologie | Port | Statut |
|---------|------------|------|--------|
| DNS | BIND9 9.18 | 53 | ✅ |
| Web | Apache2 2.4 | 80 | ✅ |
| SSH | OpenSSH 9.6 (bannière sécurisée) | 22 | ✅ |
| Base de données | MariaDB 10.11 | 3306 | ✅ |
| SNMP | Net-SNMP snmpd | 161/UDP | ✅ |
| Journaux | Syslog-ng | local | ✅ |

### TP2 — Services réseau essentiels (zone montp.local)

| Service | Technologie | Port | Statut |
|---------|------------|------|--------|
| DNS | BIND9 (zone montp.local) | 53 | ✅ |
| FTP | vsftpd 3.0.5 | 21 | ✅ |
| Web | Apache2 (VirtualHost) | 80 | ✅ |
| Base de données | MySQL | 3306 | ✅ |
| SNMP + Syslog-ng | Net-SNMP + Syslog-ng | 161 | ✅ |

---

## 📊 Supervision Nagios4

### Installation & configuration
- Installation Nagios4 + plugins + **NRPE** (agent de supervision à distance)
- Configuration des hôtes supervisés :
  - `srv.smarttech.sn` (VM Ubuntu)
  - Machine physique Windows hôte
- Définition des services Nagios : PING, SSH, HTTP, DISK, LOAD, PROCS

### Validation
```bash
# Vérifier la configuration Nagios
sudo /usr/sbin/nagios4 -v /etc/nagios4/nagios.cfg

# Redémarrer Nagios
sudo systemctl restart nagios4

# Accès dashboard web
http://localhost/nagios4
```

### Simulation d'incidents
- Arrêt Apache2 → alerte détectée automatiquement par Nagios ✅
- Arrêt SSH → état CRITICAL visible dans le dashboard ✅
- Reprise service → retour état OK détecté ✅

---

## 🔑 Commandes clés

```bash
# DNS — vérification zone
named-checkzone smarttech.sn /etc/bind/db.smarttech.sn

# Web — test
curl http://www.smarttech.sn

# SSH — connexion sécurisée avec bannière
ssh maty@srv.smarttech.sn

# SNMP — test agent
snmpget -v2c -c estm localhost sysDescr.0

# Nagios — vérifier config
sudo /usr/sbin/nagios4 -v /etc/nagios4/nagios.cfg
```

---

## 👩‍💻 Auteures

**Ndèye Maty GUEYE** & **Fatima DIBA** — L3 Réseaux & Télécommunications, ESTM Dakar  
[![Email](https://img.shields.io/badge/Email-ndeyematygueye5%40gmail.com-blue?style=flat&logo=gmail)](mailto:ndeyematygueye5@gmail.com)

---

> TP réalisé sous la direction du **Dr. Kéba GUEYE** — ESTM Dakar 2025-2026
