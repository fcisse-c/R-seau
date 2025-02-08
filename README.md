# 1 - DHCP avec Windows Server
Installation et configuration d'un serveur DHCP avec Windows Server.

## Prérequis
- Une VM sous Windows Server installée et fonctionnelle
- Une carte réseau configurée en **Réseau Interne**
- Un client connecté à ce même réseau
- Un snapshot de la VM pour backup

## Étape 1 : Configurer la carte réseau en mode Réseau Interne
1. Ouvrir le gestionnaire de votre hyperviseur (VirtualBox, VMware, Hyper-V).
2. Accéder aux paramètres de la VM Windows Server.
3. Aller dans la section **Carte Réseau**.
4. Sélectionner **Réseau Interne** comme mode d'attachement.
5. Démarrer la VM.

## Étape 2 : Installer et configurer le serveur DHCP
1. **Ouvrir le Gestionnaire de serveur**.
2. Aller dans **Ajouter des rôles et fonctionnalités**.
3. Sélectionner **Installation basée sur un rôle ou une fonctionnalité**.
4. Choisir le serveur local et cliquer sur **Suivant**.
5. Cocher **Serveur DHCP** et cliquer sur **Suivant**, puis **Installer**.
6. Une fois l'installation terminée, cliquer sur **Fermer**.
7. Aller dans **Outils d'administration** > **Gestionnaire DHCP**.

## Étape 3 : Configurer la plage d'adresses DHCP
1. Dans le Gestionnaire DHCP, développer le serveur DHCP.
2. Clic droit sur **IPv4** > **Nouvelle étendue**.
3. Donner un nom à l’étendue (ex : `Réseau Interne`), cliquer sur **Suivant**.
4. Définir la plage d'adresses :
   - **Début** : `172.20.0.100`
   - **Fin** : `172.20.0.200`
   - **Masque de sous-réseau** : `255.255.255.0`
5. Exclure certaines adresses si nécessaire, puis **Suivant**.
6. Définir la durée du bail (ex : 8 jours), puis **Suivant**.
7. Activer la configuration DHCP et finaliser l'assistant.

## Étape 4 : Configurer une réservation d'adresse IP statique
1. Dans le Gestionnaire DHCP, développer **IPv4** > **Étendues**.
2. Sélectionner l’étendue créée, puis **Réservations**.
3. Clic droit > **Nouvelle réservation**.
4. Renseigner les informations :
   - **Nom** : `Client-Statique`
   - **Adresse IP** : `172.20.0.10`
   - **Adresse MAC** : Adresse MAC du client
   - **Type de prise en charge** : cocher **BOOTP** et **DHCP**.
5. Valider avec **Ajouter**, puis **Fermer**.


