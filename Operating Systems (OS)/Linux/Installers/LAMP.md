## LAMP Install

Script file to install Linux, Apache, MySQL and PHP on Ubuntu (Debian).

#### Update Aptitude

	sudo apt-get update

#### Configure MySQL

	sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
	sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'

#### Install dependencies

	sudo apt-get install -y vim curl python-software-properties software-properties-common

#### Register repository

	sudo add-apt-repository -y ppa:ondrej/php5

#### Update again

	sudo apt-get update

#### Install another dependencies

	sudo apt-get install -y php5 apache2 libapache2-mod-php5 php5-curl php5-gd php5-mcrypt php5-readline mysql-server-5.5 php5-mysql git-core php5-xdebug

#### Configure Xdebug

	cat << EOF | sudo tee -a /etc/php5/mods-available/xdebug.ini
	xdebug.scream=1
	xdebug.cli_color=1
	xdebug.show_local_vars=1
	EOF

#### Enable rewrite module in Apache

	sudo a2enmod rewrite

#### Enable error reporting

	sudo sed -i "s/error_reporting = .*/error_reporting = E_ALL/" /etc/php5/apache2/php.ini
	sudo sed -i "s/display_errors = .*/display_errors = On/" /etc/php5/apache2/php.ini
	sudo sed -i "s/disable_functions = .*/disable_functions = /" /etc/php5/cli/php.ini

#### Restart Apache

	sudo service apache2 restart

