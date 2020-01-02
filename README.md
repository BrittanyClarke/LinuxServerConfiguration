# LinuxServerConfiguration
You will take a baseline installation of a Linux distribution on a virtual machine and prepare it to host your web applications, to include installing updates, securing it from a number of attack vectors and installing/configuring web and database servers.

# Server Instance:
##	Public IP Address: 3.91.54.23
##	SSH in: `ssh -i ~/<privateKey file> grader@3.91.54.23 -p 2200` (`ssh -i ~/.ssh/linuxCourse grader@3.91.54.23 -p 2200`)

# Completion Steps:
##	Start a new Ubuntu Server instance on Amazon Lightsail by following the steps listed under Udacity instructions.
##	SSH into the server by logging into Amazon Lightsail and then logging into the instance by clicking “Connect using SSH”
## Update all packages with `sudo apt-get update` command
##	Change SSH port to 2200 in the /etc/ssh/sshd_config file by updating “Port 22” to “Port 2200”. Configure Lightsail firewall to allow this by going into the console manager and adding the following configuration: Application = Custom, Protocol = TCP, and Port = 2200.
##	After updating port number for SSH, enter this command “sudo systemctl restart ssh” to restart ssh with updates
##	Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123) with the following commands:
 ### sudo ufw default deny incoming
 ###	sudo ufw default allow outgoing
 ###	sudo ufw allow 2200/tcp
 ###	sudo ufw allow 80/tcp
 ###	sudo ufw allow 123/udp
 ###	sudo ufw enable
##	Create a new account named “grader” with the command `sudo adduser grader`
##	Give the grader sudo permissions by adding `grader ALL=(ALL) NOPASSWD:ALL` to the /etc/sudoers.d/grader file and running the `usermod -aG sudo` command
##	On the local machine create the key-pair using command “ssh-keygen”. The file in which to save the key will be called “linuxCourse”
##	Switch the user on the server to the grader with the `sudo -u grader -i` command.
##	Create a directory on the server called “.ssh”
##	Create a new file within the .ssh directory to hold public keys called “authorized_keys”
##	Copy the contents of the linuxCourse.pub file from the local machine to the server’s authorized_keys file.
##	Change the file permissions by using the following commands:
 ###	chmod 700 .ssh
 ###	chmod 644 .ssh/authorized_keys
##	Restart ssh with `sudo systemctl restart ssh`
##	Login to the server with `ssh -i ~/<privateKey file> grader@3.91.54.23 -p 2200` (`ssh -i ~/.ssh/linuxCourse grader@3.91.54.23 -p 2200` on my machine) command
##	Switch timezone to UTC by running `sudo dpkg-reconfigure tzdata` and selecting UTC from list of timezones
##	Install and configure Apache to serve Python mod_wsgi application
 ###	Install Apache `sudo apt-get install apache2`
 ###	Install mod-wsgi `sudo apt-get install libapache2-mod-wsgi`
##	Login as postgres user with “sudo su - postgres”
##	Turn on postgre shell with `psql`
##	Create the new database and user named catalog that has limited permissions to the catalog application database with commands `CREATE DATABASE catalog` and `CREATE USER catalog` in the postgre shell
##	Give user permissions for app with “GRANT ALL PRIVILEGES ON DATABASE catalog TO catalog” on postgre shell
##	Change user’s password with `ALTER ROLE catalog WITH PASSWORD 'password';`
##	Quit the shell with `\q` and exit postgres shell with `exit`
##	Install Git with `sudo apt-get install git`
##	Make FlaskApp directory and clone the github repository here with `sudo git clone <repository url>` (`sudo git clone https://github.com/BrittanyClarke/ItemCatalog.git`)
##	Move project.py to __init__.py by using `sudo mv project.py __init__.py`
##	Update engine in database_setup.py, __init__.py, & populate_database.py by setting `engine = create_engine('postgresql://catalog:password@localhost/catalog')` in the files
##	Install pip and dependencies with the following commands:
 ###	sudo apt-get install python-pip --upgrade
 ###	sudo -H pip install httplib2 --upgrade
 ###	sudo -H pip install requests --upgrade
 ###	sudo -H pip install flask --upgrade
 ###	sudo -H pip install sqlalchemy --upgrade
 ###  sudo -H pip install psycopg2 --upgrade
 ###	sudo -H pip install oauth2client --upgrade
 ###	sudo -H pip install Flask-SQLAlchemy --upgrade
 ###	sudo -H pip install flask-seasurf --upgrade
#	Install psycopg2 with `sudo apt-get install postgresql python-psycopg2`
#	Create database schema with `sudo python database_setup.py`
# Create a file named "FlaskApp.conf" and configure the virtual host `sudo nano /etc/apache2/sites-available/FlaskApp.conf`
#	Create .wsgi file in the newly-created /FlaskApp/ directory with `sudo nano flaskapp.wsgi` (refer to file for code)
#	Add creation script to flaskapp.wsgi (refer to file for script)

# Sources used: 
## https://www.knownhost.com/wiki/security/misc/how-can-i-change-my-ssh-port
## https://www.cyberciti.biz/faq/howto-change-ssh-port-on-linux-or-unix-server/
## https://askubuntu.com/questions/1019891/connecting-to-amazon-lightsail-ubuntu-server-using-different-ssh-port
## https://www.digitalocean.com/community/questions/cannot-login-with-ssh-username-ipaddress-receive-permission-denied-publickey-despite-root-user-working
## https://askubuntu.com/questions/138423/how-do-i-change-my-timezone-to-utc-gmt
## https://www.digitalocean.com/community/tutorials/how-to-run-django-with-mod_wsgi-and-apache-with-a-virtualenv-python-environment-on-a-debian-vps
## https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps






