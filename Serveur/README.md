## 🖥️ Étape 2 : Serveur
- [x] Création d’une machine virtuelle Windows Server 2019 Standard
- [x] Installation et configuration du serveur DHCP
- [x] Mise en place et configuration du serveur DNS
- [x] Déploiement d’Active Directory et des stratégies de groupe (GPO)

---

### 🧱 Création de la machine virtuelle

- Création d’une VM sous VirtualBox avec les caractéristiques suivantes :
  - 4 Go de RAM
  - 2 cœurs CPU
  - 50 Go de disque dur (VHD)
  - ISO d’installation de Windows Server 2019 Standard
  - Réseau configuré en Adaptateur Réseau Interne

---

### ⚙️ Installation de Windows Server 2019

- Lancement de l’installation depuis l’ISO
- Choix de l’édition : Windows Server 2019 Standard (Desktop Experience)
- Formatage du disque et installation
- Premier démarrage avec configuration du mot de passe Administrateur

---

### 🔄 Windows Update

- Connexion temporaire à Internet via un second adaptateur (NAT)
- Téléchargement et installation de toutes les MàJ via Windows Update
- Redémarrage nécessaire

---

### 🖧 Configuration réseau

- Attribution d’une adresse IP statique :
  - Adresse IP : `192.168.1.2`
  - Masque : `255.255.255.0`
  - Passerelle : `192.168.1.1`
  - DNS : (provisoirement l’IP du serveur lui-même)
- Renommage de la machine :
  - Nouveau nom : `SRV-DHCP-01`  
  - Redémarrage nécessaire pour appliquer

---

### 📦 Installation et configuration du serveur DHCP

#### Installation

- Ouvrir le Gestionnaire de serveur → Cliquer sur Ajouter des rôles et des fonctionnalités → Sélectionner :
  - Installation basée sur un rôle ou une fonctionnalité
  - Le serveur local : `SRV-DHCP-01`
  - Le rôle : `Serveur DHCP`
  - Terminer l’assistant

#### Configuration

- Ouvrir DHCP depuis le gestionnaire d’outils → Développer le serveur → Clic droit sur IPv4 → Nouvelle étendue → Paramétrer :
  - Nom de l’étendue : `ETENDUE-BATCHZZARD`
  - Plage d’adresses IP : `192.168.1.100` à `192.168.1.200`
  - Masque de sous-réseau : `255.255.255.0`
  - Passerelle par défaut : `192.168.1.1`
  - Serveur DNS : `192.168.1.2`
  - Durée de bail : `8 Jours` (par défaut)
- Clic droit → Activer

---

### 🌐 Mise en place et configuration du serveur DNS

#### Installation

- Ouvrir Gestionnaire DNS :
  - Zone de recherche directe :
    - Nouvelle zone → Zone principale → IPv4 
    - Nom : `batchzzard.local`  
    - Fichier créé : `batchzzard.local.dns`  
    - Sert à résoudre les noms vers des adresses IP

  - Zone de recherche inverse :
    - Nouvelle zone → Zone principale → IPv4  
    - ID réseau : `192.168.1`  
    - Fichier créé : `1.168.192.in-addr.arpa.dns`  
    - Sert à résoudre les adresses IP vers les noms

#### Configuration

Pour chaque hôte :
- Clic droit sur la zone `batchzzard.local` → *Nouvel hôte (A ou AAAA)*  
- Saisir le nom et l’IP correspondante  
- Cocher Créer un enregistrement de pointeur associé (PTR)

Pour rappel, le plan d'adressage IP est le suivant:

| Nom d'hôte              | Adresse IP               |
|-------------------------|--------------------------|
| `srv-dhcp-01`           | `192.168.1.2`            |
| `srv-file-01`           | `192.168.1.3`            |
| `printer-vente-01`      | `192.168.1.10`           |
| `printer-production-01` | `192.168.1.13`           |
| `printer-logistique-01` | `192.168.1.16`           |
| `srv-dns-01`            | `192.168.1.2`            |

---

### 🧑‍💼 Déploiement d’Active Directory (AD DS)

#### Promotion du serveur en contrôleur de domaine

- Dans le Gestionnaire de serveur → Cliquer sur Ajouter le rôle Services AD DS
  - Une fois installé → Cliquer sur Promouvoir ce serveur en contrôleur de domaine
  - Options :
    - Nouvelle forêt
    - Nom du domaine racine : `batchzzard.local`
    - Niveau fonctionnel : Windows Server 2016
    - Rôles : Serveur DNS et Catalogue Global
    - Mot de passe du mode de restauration : `T9g*vLP2aXzW` (Généré aléatoirement)
    - Ne pas déléguer
    - Nom NetBIOS : `BATCHZZARD`
    - Chemins d'installation par défaut
  - Lancer l’installation → Le serveur redémarre automatiquement

---

### 👥 Création d’utilisateurs Active Directory

- Ouvrir Utilisateurs et ordinateurs Active Directory
- Créer une Unité d’organisation (OU) → Ici on a créé "Direction" pour gérer uniquement les membres de la direction
- Clic droit → Nouvel utilisateur :
  - Nom d'utilisateur : `philippe.etchebatch@batchzzard.local`
  - Mot de passe : `motdepasse123!`
  - Cocher "Le mot de passe n’expire Jamais" (mot de passe faible, et sans expiration uniquement pour la simulation)

---

## 📌 À suivre : Tests de toutes les fonctionnalités avec des commandes Powershell
