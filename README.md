**Guide ,** https://docs.moodle.org/402/en/Installing_Moodle

**Guide ,** https://docs.moodle.org/402/en/Step-by-step_Installation_Guide_for_Ubuntu#Step_1:_Install_Ubuntu

<br>

### Step 1: Install Ubuntu,

`anup@ubuntu-22042-100-REALMREGAL:~$ cat /etc/os-release `

<br>

### Step 2: Install Apache/MySQL/PHP,

**Apache,**

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo apt install software-properties-common`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo apt-get update`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo apt install apache2`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo systemctl status apache2.service `

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo systemctl enable apache2.service `

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo journalctl -xeu apache2.service`

<br>

**Open your browser and go to ,** http://192.168.56.100/

<br>

**MySQL,**

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo apt-get install mysql-client`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo apt-get install mysql-server`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo MySQL`

`mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '!7EC9%JtYjJ3M';`

`mysql> exit`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo mysql_secure_installation`

    !7EC9%JtYjJ3M

**Note :** 

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo mysql_secure_installation`

... Failed! Error: SET PASSWORD has no significance

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo killall -9 mysql_secure_installation`

<br>

**PHP,**

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo add-apt-repository ppa:ondrej/php`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo apt-get update`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo apt-get install php7.4`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo apt-get install libapache2-mod-php`

<br>

### Step 3: Install Additional Software

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo apt install graphviz aspell ghostscript clamav php7.4-pspell php7.4-curl php7.4-gd php7.4-intl php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-ldap php7.4-zip php7.4-soap php7.4-mbstring`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo systemctl status apache2.service `

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo systemctl restart apache2.service`

<br>

### Step 4: Download Moodle

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo apt install git`

`anup@ubuntu-22042-100-REALMREGAL:~$ cd /opt`

`anup@ubuntu-22042-100-REALMREGAL:/opt$ sudo git clone git://git.moodle.org/moodle.git`

`anup@ubuntu-22042-100-REALMREGAL:/opt$ cd moodle/`

`anup@ubuntu-22042-100-REALMREGAL:/opt/moodle$ sudo git branch -a`

`anup@ubuntu-22042-100-REALMREGAL:/opt/moodle$ sudo git branch --track MOODLE_400_STABLE origin/MOODLE_400_STABLE`

`anup@ubuntu-22042-100-REALMREGAL:/opt/moodle$ sudo git checkout MOODLE_400_STABLE`

<br>

### Step 5: Copy local repository to /var/www/html/

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo cp -R /opt/moodle /var/www/html/`

`anup@ubuntu-22042-100-REALMREGAL:~$ ls -ltr /var/www/html`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo chmod -R 0755 /var/www/html/moodle`

<br>

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo mkdir /var/moodledata`

`anup@ubuntu-22042-100-REALMREGAL:~$ ls -ltr /var/`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo chown -R www-data /var/moodledata`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo chmod -R 777 /var/moodledata`

<br>

### Step 6: Setup MySQL Server

`anup@ubuntu-22042-100-REALMREGAL:~$ mysql --version`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo systemctl status mysql.service `

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo mysql -u root -p`

    !7EC9%JtYjJ3M

`mysql> CREATE DATABASE moodle DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;`

`mysql> create user 'moodledude'@'localhost' IDENTIFIED BY '!7EC9%JtYjJ3M';`

`mysql> GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,CREATE TEMPORARY TABLES,DROP,INDEX,ALTER ON moodle.* TO 'moodledude'@'localhost';`

`mysql> quit;`

<br>

### Step 7: Complete Setup

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo chmod -R 777 /var/www/html/moodle`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo chmod -R 0755 /var/www/html/moodle`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo systemctl status apache2.service`

`anup@ubuntu-22042-100-REALMREGAL:~$ sudo systemctl status mysql.service`

<br>

**Open your browser and go to ,** http://192.168.56.100/moodle/

<br>

If **config.php** doesn't gets created automatically, 

`anup@ubuntu-22042-100-REALMREGAL:~$ cd /var/www/html/moodle/`

`anup@ubuntu-22042-100-REALMREGAL:/var/www/html/moodle$ `

`anup@ubuntu-22042-100-REALMREGAL:/var/www/html/moodle$ sudo nano config.php`

    <?php  // Moodle configuration file
    
    unset($CFG);
    global $CFG;
    $CFG = new stdClass();
    
    $CFG->dbtype    = 'mysqli';
    $CFG->dblibrary = 'native';
    $CFG->dbhost    = 'localhost';
    $CFG->dbname    = 'moodle';
    $CFG->dbuser    = 'moodledude';
    $CFG->dbpass    = '!7EC9%JtYjJ3M';
    $CFG->prefix    = 'mdl_';
    $CFG->dboptions = array (
      'dbpersist' => 0,
      'dbport' => '',
      'dbsocket' => '',
      'dbcollation' => 'utf8mb4_unicode_ci',
    );
    
    $CFG->wwwroot   = 'http://192.168.56.100/moodle';
    $CFG->dataroot  = '/var/moodledata';
    $CFG->admin     = 'admin';
    
    $CFG->directorypermissions = 0777;
    
    require_once(__DIR__ . '/lib/setup.php');
    
    // There is no php closing tag in this file,
    // it is intentional because it prevents trailing whitespace problems!

<br>
