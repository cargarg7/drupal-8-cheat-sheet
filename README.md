# Drupal 8 Cheat Sheet

## Drupal 8 Installation

This installation has been tested in **Ubuntu 15.10**

### Install `drush`

If you don't have `drush` installed, type the following:

```console
sudo apt-get install composer
composer global require drush/drush
```

Edit the file `.profile` and add the following line:

```console
PATH="$HOME/.composer/vendor/bin:$PATH"
```

Resource the new configuration:

```console
source ~/.profile
```

Check the installation:

```console
drush status
```

### Create `MySQL` database

Create database with name `mydrupal8`. Remember to enter the MySQL root password when you are prompted, not the system password.

```console
mysql -u root -p -e "CREATE DATABASE mydrupal8"
```

### Configure Apache

Edit the file `/etc/apache2/apache2.conf`:

```console
sudo gedit /etc/apache2/apache2.conf 
```

Find the section `<Directory /var/www/>` and set the option `AllowOverride` to `All` as follows:

```console
<Directory /var/www/>
	Options Indexes FollowSymLinks
	AllowOverride All
	Require all granted
</Directory>
```

Activate `mod_rewrite`:

```console
sudo a2enmod rewrite
```

Reload Apache:

```console
sudo service apache2 restart
```

### Download Drupal 8

```console
sudo chmod a+w /var/www/html/
cd /var/www/html/
drush dl drupal
mv drupal-8.0.3 mydrupal8
```

### Create configuration files and set permissions

Remember to type your real username instead of `myuser`.

```console
cd mydrupal8/sites/default/
cp default.settings.php settings.php
cp default.services.yml services.yml
chmod 0666 settings.php services.yml
mkdir files
sudo chown myuser:www-data files
chmod 0777 files
```

### Install Drupal 8

Open your web browser and go to <http://localhost/mydrupal8/>

Choose language.

![Choose language](images/drupal01.png)

Choose **Standar** profile.

![Choose profile](images/drupal02.png)

<!--Verify requirements. Don't worry if you get the `Clean URLs` alert message. Click on **Continue anyway**.

%%![Verify requirements](images/drupal03.png)
-->

Set up database. Type `mydrupal8` as **database name**. Enter your database administrator **username** and **password**.

![Set up database](images/drupal04.png)

Installation process may take a while.

![Set up database](images/drupal05.png)

Configure site. Enter the **site name**, **site email address**, **username** and **password** for the site maintenance account, etc. Click **Save and continue**.

![Configure site](images/drupal06.png)

### Protect `settings.php` and `services.yml`

```console
cd mydrupal8/sites/default/
chmod a-w settings.php services.yml 
```

¡Congratulations! You have your Drupal 8 site installed.
<!--
%%drush si standard --db-url=mysql://root:root@localhost/mydrupal8 --account-name="admin" --account-pass="123456" --account-mail="chiquito@condemor.com"

%%Now go to <http://localhost/mydrupal8/> and enter as administrator with user `admin` and password `123456`.
-->
