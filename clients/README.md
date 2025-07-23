## 🖥️ Étape 3 : Clients  
- [x] Création d’une machine virtuelle Windows 11  
- [x] Tests de connexion et intégration au domaine Active Directory

---

### 🧱 Création de la machine virtuelle

- Création d’une VM sous VirtualBox avec les caractéristiques suivantes :  
  - 6 Go de RAM  
  - 3 cœurs CPU  
  - 50 Go de disque dur (VHD)  
  - ISO d’installation de Windows 11 Professionnel
  - Réseau configuré en Adaptateur Réseau Interne (même nom que le serveur: `intnet`)

---

### ⚙️ Installation de Windows 11

- Lancement de l’installation depuis l’ISO
- Choix de l’édition : Windows 11 Professionnel
- Formatage du disque et installation
- Création d’un compte local temporaire  

---

### 🖧 Configuration réseau 

Il faut vérifier que la VM cliente communique correctement avec le serveur `SRV-DHCP-01` :

- La VM cliente doit recevoir une adresse IP dynamique via DHCP
  - Ouvrir un terminal → `ipconfig /all` → Résultat :
    - IP dans la plage `192.168.1.100-200`
    - Passerelle : `192.168.1.1`
    - DNS : `192.168.1.2`

- Tester la résolution DNS :
  ```powershell
  ping 192.168.1.2
  ping srv-dhcp-01
  nslookup srv-dhcp-01
  nslookup batchzzard.local

---

### 🔗 Intégration au domaine Active Directory

#### Se connecter au domaine batchzzard.local :

- Ouvrir Ce PC → Clic droit → Propriétés → Modifier le nom de l'ordinateur (avancé)
- Cocher Domaine
   - Saisir : `batchzzard`
- Valider
- Saisir les identifiants d’un compte ayant les droits d’intégration au domaine :
  - Utilisateur : `philippe.etchebatch`
  - Mot de passe : `motdepasse123!`
- Message affiché : **Bienvenue dans le domaine batchzzard.local**
- Redémarrage nécessaire

---

### 🧑‍💼 Connexion avec un compte domaine

  - Sur l’écran de connexion → Cliquer sur Autre utilisateur
  - Renseigner les informations suivantes :
    - Nom d’utilisateur : `philippe.etchebatch@batchzzard.local`
    - Mot de passe : `motdepasse123!`
