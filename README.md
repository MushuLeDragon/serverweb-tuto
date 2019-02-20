# Server Web Tuto

How to setup a linux web server

## Apache2

### Debian / Ubuntu

#### Installer et configurer Apache2

- Installer **apache2** : `apt-get install apache2`

#### Installer un ou plusieurs sites en local avec nom de domaine personnel

- Créer les dossiers qui hébergeront les sites et y mettre les droits utilisateur :
```shell
mkdir -p /var/www/blablabla.com/public_html
mkdir -p /var/www/trololo.com/public_html
chown -R $USER:$USER /var/www/blablabla.com/public_html
chown -R $USER:$USER /var/www/trololo.com/public_html
```

- Créer les pages HTML de chacun des sites dans le dossier créé préalablement `nano /var/www/blablabla.com/public_html/index.html` et `nano /var/www/trololo.com/public_html/index.html` :
```html
<html>
  <head>
    <title>Welcome to Blablabla.com!</title>
  </head>
  <body>
    <h1>Success! The blablabla.com virtual host is working!</h1>
  </body>
</html>
```

```html
<html>
  <head>
    <title>Welcome to Trololo.com!</title>
  </head>
  <body> <h1>Success! The Trololo.com virtual host is working!</h1>
  </body>
</html>
```

- Créer le Host virtuel dans le dossier `/etc/apache2/sites-available/` en le copiant à partir du fichier par défaut : `cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/blablabla.com.conf`
- Le modifier comme ci dessous : `nano /etc/apache2/sites-available/blablabla.com.conf`
```shell
<VirtualHost *:80>
        ServerAdmin admin@blablabla.com
        ServerName blablabla.com
        ServerAlias www.blablabla.com
        DocumentRoot /var/www/blablabla.com/public_html

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
