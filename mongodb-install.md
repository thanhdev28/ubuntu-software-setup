# ubuntu-software-setup
With Ubuntu 18.04 LTS released, I have installed it on my VMware lab machine for testing purposes… the steps below is how I got MongoDB installed on Ubuntu 18.04 LTS servers… if you want to install it, the steps below should be a great place to start…

MongoDB, a free open source, NoSQL High-performance, schema-free document-oriented database can be used to create powerful websites and applications… This brief tutorial is going to show students and new users how to install MongoDB on Ubuntu 18.04 LTS servers.

MongoDB is already in Ubuntu default repositories… however, the version in Ubuntu repositories isn’t the latest and greatest… In order to install the latest, you must install MongoDB package repository on Ubuntu, and this tutorial will show you how.

When you’re ready to get MongoDB installed, follow the steps below:

Step 1: Add MongoDB Package repository to Ubuntu
In order to get the latest version of MongoDB, you must add its repository to Ubuntu.. to do that, run the commands below to add the official repository key.

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5

After adding the repository key to Ubuntu, run the commands below to add MongoDB repository to your system…

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list

Step 2: Install MongoDB on Ubuntu 18.04
Now that the repository and key have been added to Ubuntu, run the commands below to install the package.

sudo apt update
sudo apt install -y mongodb-org
Step 3: Manage MongoDB
After installing MongoDB, the commands below can be used to stop, start and enable MongoDB to automatically startup when the systems boots up.

sudo systemctl stop mongod.service
sudo systemctl start mongod.service
sudo systemctl enable mongod.service
By default, MongoDB listens on port 27017.. after installing, the local server should be able to communicate with MongoDB.. to verify whether MongoDB is running and active, run the commands below:

sudo systemctl status mongod

You should see something like the lines below:

richard@ubuntu1604:~$ sudo systemctl status mongod
● mongod.service - High-performance, schema-free document-oriented database
   Loaded: loaded (/lib/systemd/system/mongod.service; enabled; vendor preset: enabled)
   Active: active (running) since Sat 2018-01-27 08:53:42 CST; 13min ago
     Docs: https://docs.mongodb.org/manual
 Main PID: 2383 (mongod)
    Tasks: 23
   Memory: 60.7M
      CPU: 2.613s
   CGroup: /system.slice/mongod.service
           └─2383 /usr/bin/mongod --config /etc/mongod.conf

Jan 27 08:53:42 ubuntu1604 systemd[1]: Started High-performance, schema-free document-oriented database.
Jan 27 09:05:49 ubuntu1604 systemd[1]: Started High-performance, schema-free document-oriented database.
To connect to MongoDB shell, run the commands below:

mongo --host 127.0.0.1:27017

You should see something like the lines below:

MongoDB shell version v3.6.2
connecting to: mongodb://127.0.0.1:27017/
MongoDB server version: 3.6.2
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
        http://docs.mongodb.org/
Questions? Try the support group
        http://groups.google.com/group/mongodb-user
Server has startup warnings:
Step 4: Adding Admin User
If you want to enable authentication, run the commands to create a new admin user after you’ve logged into MongoDB server.

> use admin

Then run the commands below to create a new admin user

> db.createUser({user:"admin", pwd:"new_password_here", roles:[{role:"root", db:"admin"}]})

You should see a successful admin user created

Successfully added user: {
	"user" : "admin",
	"roles" : [
		{
			"role" : "root",
			"db" : "admin"
		}
	]
}
Exit and continue below to enable MongoDB logon authentication… Run the commands below to open MongoDB config file..

sudo nano /lib/systemd/system/mongod.service

Then change the highlighted line to look like the one below and save…

[Unit]
Description=High-performance, schema-free document-oriented database
After=network.target
Documentation=https://docs.mongodb.org/manual

[Service]
User=mongodb
Group=mongodb
ExecStart=/usr/bin/mongod --auth --config /etc/mongod.conf
PIDFile=/var/run/mongodb/mongod.pid
# file size
Save and exit

Restart MongDB to make the changes apply.

sudo systemctl daemon-reload
sudo service mongod restart
Now only authetication users will be allowed to access the database server…

mongo -u admin -p new_password_here --authenticationDatabase admin

Step 5: Completely Remove MongoDB
To completely remove MongoDB from a system, you must remove the MongoDB applications themselves, the configuration files, and any directories containing data and logs.

Stop the database server

sudo systemctl stop mongod.service

Remove all packages

sudo apt purge mongodb-org*

Finally, remove MongoDB databases and log files.

sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
