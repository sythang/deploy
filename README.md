
##1. The first step is to install some dependencies for Ruby.

```
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev
```

##2. The installation for rvm is pretty simple:
```
sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev

gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3

curl -sSL https://get.rvm.io | bash -s stable

source ~/.rvm/scripts/rvm

rvm install 2.2.2

rvm use 2.2.2 --default

ruby -v
```
##3. Install Apache
```
sudo apt-get install apache2
```

##4. Install postgresql
```
sudo apt-get update

sudo apt-get install postgresql postgresql-contrib

createdb vto_commerce_development;

create user vto-user password 'Vt0_development';

GRANT ALL PRIVILEGES ON DATABASE mydb TO vto-user;

sudo -u postgres createdb vto_commerce_development --owner=vto_ecommerce

sudo -u postgres createdb vto_commerce_dev --owner=vto_ecommerce

create role vto_development_user with createdb login password 'Vt0Development';

CREATE USER vto_user WITH PASSWORD 'Vt0_development';

GRANT ALL PRIVILEGES ON DATABASE "vto_commerce_development" to vto_user;
```

```
sudo su - postgres
psql
create role rolename with createdb login password 'password';
```
##5. Install imagemagick
```
apt-get install imagemagick
apt-get install libmagick9-dev
gem install rmagick
```
##6. Install Passenger
First, install the PGP key for the repository server:
```sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 561F9B9CAC40B2F7```

Create an APT source file:
```
sudo nano /etc/apt/sources.list.d/passenger.list
```

Insert the following line to add the Passenger repository to the file:

```
deb https://oss-binaries.phusionpassenger.com/apt/passenger trusty main
```
Press CTRL+X to exit, type Y to save the file, and then press ENTER to confirm the file location.

Change the owner and permissions for this file to restrict access to root:

```
sudo chown root: /etc/apt/sources.list.d/passenger.list

sudo chmod 600 /etc/apt/sources.list.d/passenger.list
```
Update the APT cache:

```
sudo apt-get update
```
Finally, install Passenger:

```
sudo apt-get install libapache2-mod-passenger
```
Make sure the Passenger Apache module; it maybe enabled already:

```
sudo a2enmod passenger
```
Restart Apache:

```
sudo service apache2 restart
```
This step will overwrite our Ruby version to an older one. To resolve this, simply remove the incorrect Ruby location and create a new symlink to the correct Ruby binary file:
