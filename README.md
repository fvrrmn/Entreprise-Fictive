# 🚀 Entreprise-Fictive

**Simulation complète de l’infrastructure réseau d’une entreprise fictive sous Windows Server 2019**

---

## 📖 Synopsis

Batchzzard est une entreprise fictive spécialisée dans l'achat et la revente de matériel informatique ainsi que de solutions logicielles destinées aux professionnels.

L’infrastructure IT repose sur un serveur **Windows Server 2019 Standard** assurant :

- 🌐 Attribution automatique des adresses IP via **DHCP**
- 🔍 Résolution des noms de domaine internes via **DNS**
- 👥 Gestion centralisée des utilisateurs via **Active Directory** et des stratégies de groupe (**GPO**)

La société compte une vingtaine d’utilisateurs répartis en plusieurs services, chacun dirigé par un responsable.

---

## 📂 Contenu du projet

### 🛠️ Étape 1 : Conception
- [x] Schéma de l’architecture réseau physique
- [x] Plan d’adressage IP

### 🖥️ Étape 2 : Serveur
- [x] Création d’une machine virtuelle Windows Server 2019 Standard
- [x] Installation et configuration du serveur DHCP
- [x] Mise en place et configuration du serveur DNS
- [x] Déploiement d’Active Directory et des stratégies de groupe (GPO)
- [ ] Tests de toutes les fonctionnalités avec des commandes Powershell

### 🖥️ Étape 3 : Clients
- [x] Création d’une machine virtuelle Windows 11
- [x] Tests de connexion et intégration au domaine Active Directory

### ✨ Étape 4 : Extensions
- [ ] Mise en place d’un serveur de fichiers pour centraliser les données
- [ ] Configuration d’une stratégie de sauvegarde automatisée
- [ ] Ajout d’un serveur Web interne (IIS)
- [ ] Mise en place d’un système de monitoring réseau (ex : Nagios, Zabbix)
- [ ] Déploiement d’un serveur VPN pour accès distant sécurisé

---

## 🛠️ Technologies et outils utilisés

- Cisco Packet Tracer
- VirtualBox
- Windows Server 2019
- Windows 11
- DHCP
- DNS
- Active Directory
- Invite de commandes (CMD)
- PowerShell
