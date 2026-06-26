[README.md](https://github.com/user-attachments/files/29382618/README.md)
# nextcloud-mint-setup
Cloud privé Nextcloud sur Linux mint - Projet LAMP Apache PHP MariaDB
#Nextcloud Cloud Privé - Linux Mint 

I - 

Déploiement d'un cloud privé type Google Drive en local pour usage personnel. 

 compétences Linux, Apache, PHP, MariaDB. 

Objectif

 Installer et configurer Nextcloud sur Linux Mint avec stack LAMP complète, sécurisation des dossiers et accès administrateur. 

Stack technique 
OS : Linux Mint 22 cinnammon
Serveur web : Apache2
PHP : PHP 8.x + extensions
BDD : SQLite pour l'install initiale, migrable vers MariaDB
Nextcloud : Version 29.x

Procédure d'installation 

1. Installation des dépendances
'''bash 
sudo apt update
sudo apt install apache2 php-mysql php-sqlite3 php-curl php-gd php-intl php-mbstring php-xml php-zip php-bcmath php-gmp libache2-mod-php unzip wget 

2. Activation modules Apache.

sudo a2enmod rewrite headers env dir mime
sudo systemctl restart apache2

3. Téléchargement Nexcloud

cd /tmp
wget https://fownload.nextcloud.com.server.releases/latest.zip
Sudo unzip latest.zip -d /var/www/html/
sudo chown -R www-data:www-data /var/www/html/nextcloud

4. Créatio  dossier data sécurité

sudo mkdir -p /var/www/html/nextcloud/data
sudo chown www-data:www-data /var/www/html/nextcloud/data
sudo chomd 750 /var/www/html/nextcloud/data

5. Configuration Apache VirtualHost - Code Apache

<VirtualHost *:80>
   ServerName Localhost
   DocumentRoot /var/www/html/nextcloud
   
   <Directory /var/www/html/nextcloud/>
    Require all granted 
    AllowOverride All
    Options FollowSymLinks MultiViews
  </Directory>

</VirtalHost>

Activation

sudo a2ensite nextcloud.conf
sudo systemctl reload apache2

Installation via interface web

Accès à http://localhost/nextcloud

Créer compte admin :
Dossier data : /var/www/html/nextcloud/data


Points de sécurisation appliqués 

1. Dossier data hors accès web chmod 750
2. Propriété www-data sur tous les fichiers Nextcloud 
3. Modules Apache sécurité activés : headers, rewrite









