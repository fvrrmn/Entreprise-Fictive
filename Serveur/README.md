## 🖥️ Étape 2 : Serveur
- [x] Création d’une machine virtuelle Windows Server 2019 Standard
- [x] Installation et configuration du serveur DHCP
- [ ] Mise en place et configuration du serveur DNS
- [ ] Déploiement d’Active Directory et des stratégies de groupe (GPO)

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
  - Adresse IP : 192.168.1.2
  - Masque : 255.255.255.0
  - Passerelle : 192.168.1.1
  - DNS : (provisoirement l’IP du serveur lui-même)
- Renommage de la machine :
  - Nouveau nom : SRV-DHCP-01  
  - Redémarrage nécessaire pour appliquer

---

### 📦 Installation et configuration du serveur DHCP

#### Installation

- Ouvrir le Gestionnaire de serveur → Cliquer sur Ajouter des rôles et des fonctionnalités → Sélectionner :
  - Installation basée sur un rôle ou une fonctionnalité
  - Le serveur local : SRV-DHCP-01
  - Le rôle : Serveur DHCP
  - Terminer l’assistant

#### Configuration

- Ouvrir DHCP depuis le gestionnaire d’outils → Développer le serveur → Clic droit sur IPv4 → Nouvelle étendue → Paramétrer :
  - Nom de l’étendue : ETENDUE-BATCHZZARD
  - Plage d’adresses IP : 192.168.1.100 à 192.168.1.200
  - Masque de sous-réseau : 255.255.255.0
  - Passerelle par défaut : 192.168.1.1
  - Serveur DNS : 192.168.1.2
  - Durée de bail : 8 Jours (par défaut)

---

## 📌 À suivre...
