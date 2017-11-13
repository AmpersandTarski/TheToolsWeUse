# Sentinel

**Sentinel has ceased to exist. We no longer use it. However, we are grateful for the good work it once did!**

---

The [sentinel](http://sentinel.tarski.nl) is a server on which some tests are run every night. It is the machine where we have regression tests.

The source code of sentinel is on github too, in the repo called Sentinel

## Access to the sentinel server

The procedure below describes how to create and install an ssl certificate on the Sentinel web server.

First create certificate:

```
cd /home/sentinel/authentication
openssl req -new -x509 -days 999 -keyout tarski.nl.key -out tarski.nl.crt -nodes -subj  '/C=NL/O=Tarski Systems/CN=sentinel.tarski.nl'
```

This creates the files `~/authentication/tarski.nl.key` and `~/authentication/tarski.nl.crt`. Now add the SSL module to the apache configuration:

```
sudo a2enmod ssl
```

Edit the apache configuration to allow .htaccess files and use the created SSL certificates:

```
sudo nano /etc/apache2/sites-available/default-ssl
```

* In section `<Directory /var/www/>` change `AllowOverride None` to `AllowOverride All`
* Comment out old  SSLCertificateFile and SSLCertificateKeyFile entries \(using `#`\)
* Add `SSLCertificateFile /home/sentinel/authentication/tarski.nl.crt`
* Add `SSLCertificateKeyFile /home/sentinel/authentication/tarski.nl.key`

Finally, restart apache:

```
sudo /etc/init.d/apache2 restart
```

Old ubuntu install log. This was constructed over a period of 4 years, so there might be some small inconsistencies, but it will be a good guide if we need to reinstall sentinel.tarski.nl.

#### Add sentinel user

Open Terminal add new user and \(in second step\) give that user admin rights

```
sudo adduser sentinel
sudo adduser sentinel admin

sudo apt-get update
```

\(gets stuck on 0%, and suddenly finishes after a couple of minutes\)

#### SSH

```
sudo apt-get install openssh-server
ssh-keygen -t rsa
```

\(3x enter: default location, empty passphrase, empty passphrase\)  
\(Only necessary to create `.ssh` directory with correct permissions\)

Add public key \(`~/.ssh/id_rsa.pub`\) to sentinel repository on GitHub.

#### Apache, PHP, and MySQL

\(from: [http://connectwww.com/how-to-install-and-configure-apachephpmysql-and-phpmyadmin-on-ubuntu/727/](http://connectwww.com/how-to-install-and-configure-apachephpmysql-and-phpmyadmin-on-ubuntu/727/)\)

```
sudo apt-get install apache2
sudo apt-get install php5 libapache2-mod-php5
sudo /etc/init.d/apache2 restart
sudo apt-get install mysql-server
```

\(password empty, couple of times\)

```
sudo apt-get install phpmyadmin
```

\(choose apache2, no\)

```
sudo cp /etc/phpmyadmin/apache.conf /etc/apache2/conf.d
```

Allow empty password for mysql:  \(_probably no longer necessary now we have passwords on all databases_\)

`sudo nano /etc/phpmyadmin/config.inc.php` add this line

```
$cfg['Servers'][$i]['AllowNoPassword'] = TRUE;
```

`sudo /etc/init.d/apache2 restart`

Check [http://sentinel.tarski.nl/phpmyadmin/](http://sentinel.tarski.nl/phpmyadmin/)

#### Git

```
git config --global user.name "Ampersand Sentinel"
git config --global user.email stef.joosten@ou.nl

mkdir ~/git
cd ~/git
git clone git@github.com:AmpersandTarski/ampersand.git
git clone git@github.com:AmpersandTarski/prototype.git
git clone git@github.com:AmpersandTarski/ampersand-models.git
git clone git@github.com:AmpersandTarski/sentinel.git
```

Create symbolic link to use `.profile` from sentinel repo:

```
ln -fs git/sentinel/scripts/.profile .profile
```

#### Haskell

Ghc from apt-get haskell is not recent enough, so instead, follow [http://www.haskell.org/platform/linux.html](http://www.haskell.org/platform/linux.html)  
\(Don't like unpacking at root, so we do it in a separate directory and move the haskell directories after that\)

```
wget http://www.haskell.org/platform/download/2014.2.0.0/haskell-platform-2014.2.0.0-unknown-linux-x86_64.tar.gz
sudo tar xvf haskell-platform-2014.2.0.0-unknown-linux-x86_64.tar.gz
sudo mv usr/local/haskell/ghc-7.8.3-x86_64 /usr/local/haskell
sudo /usr/local/haskell/ghc-7.8.3-x86_64/bin/activate-hs
sudo rm -rf /home/sentinel/usr
rm haskell-platform-2014.2.0.0-unknown-linux-x86_64.tar.gz
```

#### Ampersand

Prototype depends on HDBC-odbc package, which needs an odbc c library

```
sudo apt-get install unixodbc-dev
sudo apt-get install graphviz
sudo apt-get install texlive-full
```

#### SSH access

Add public keys \(`~/.ssh/id_rsa.pub`\) from computers that need access to sentinel to `/home/sentinel/.ssh/authorized_keys`, and disable password access:

`sudo nano /etc/sshd_config` add these three lines to disable logging in with username & password \(which is too unsafe\)

```
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
```

#### Sentinel

Calling and compiling the sentinel through apache requires php to first execute a script as root, which the executes a script as sentinel. This is rather awkward and not very secure. A better way most likely exists but has not been found in the available time.

Make a symbolic link for the Sentinel www directory in `/var/www` on the test server

```
sudo ln -s /home/sentinel/git/sentinel/www /var/www/sentinel
```

and also for the output directory for generated prototypes

```
sudo ln -s /home/sentinel/git/sentinel/www/ampersand/ /var/www/ampersand
```

Make sure that the generated runSentinel.log.txt can be written by both crontab-spawned runSentinel and php-spawned runSentinel \(run as different users\)

```
sudo touch /home/sentinel/git/sentinel/www/logs/runSentinel.log.txt
sudo chmod ugo+rwx /home/sentinel/git/sentinel/www/logs/runSentinel.log.txt
```

Add crontab entries for runSentinel with `crontab -e`:

```
# for real, every night at 5 (once a week, delete the sandbox)
0 5 * * sun $HOME/git/sentinel/scripts/crontabRunSentinel --deleteSandbox
0 5 * * mon-sat $HOME/git/sentinel/scripts/crontabRunSentinel

# for testing, every two minutes
#*/2 * * * * $HOME/git/sentinel/scripts/crontabRunSentinel
```

Allow apache to run sentinel scripts as user `sentinel`: execute `sudo visudo` and add these lines:

```
# allow apache to execute the following scripts as user sentinel
www-data ALL=(sentinel) NOPASSWD: /home/sentinel/git/sentinel/scripts/phpKillAndRunSentinel
www-data ALL=(sentinel) NOPASSWD: /home/sentinel/git/sentinel/scripts/phpFetchAllRepos
www-data ALL=(sentinel) NOPASSWD: /home/sentinel/git/sentinel/scripts/phpCompileSentinel
```

`sudo nano /var/www/.htaccess` and enter:

```
Options +FollowSymLinks
RewriteEngine on
RewriteRule ^()$ /www/sentinel.php [R=300,L]
```

`sudo nano /etc/apache2/sites-available/default`  
and change `AllowOverride None` to `AllowOverride All` in `<Directory /var/www/>`.

_Not entirely sure if this one is necessary:_

```
sudo a2enmod rewrite
```

Restart apache:

```
sudo /etc/init.d/apache2 restart
```

#### Done

The sentinel can now be compiled and run through the web interface

[http://sentinel.oblomov.com/www/sentinel.php](http://sentinel.oblomov.com/www/sentinel.php)

We don't use index.html, so sentinel.tarski.com allows us to see the directory in the web browser.

# Password protect Sentinel WWW directory

The following should be done from the `sentinel` account on sentinel.tarski.nl. We assume the passwords are kept in `/home/sentinel/authentication/nvwa.htpasswords`, but this can be any file, as long as it's not reachable by the www server.

First, create a `.htaccess` file in the directory that needs protection \(e.g. `git/sentinel/www/ampersand/NVWA/`\):

```
nano git/sentinel/www/ampersand/NVWA/.htaccess
```

Paste the contents below \(after changing `AuthName` to an appropriate description.\)

```
# Redirect http request to https
RewriteEngine On
RewriteCond %{HTTPS} !=on
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

# Require password
AuthName "Beveiligd NVWA prototype"
AuthType Basic
AuthUserFile /home/sentinel/authentication/nvwa.htpasswords
require valid-user
```

If not present yet, create an empty password file:

```
touch /home/sentinel/authentication/nvwa.htpasswords
```

And add each user with:

```
htpasswd /home/sentinel/authentication/nvwa.htpasswords USERNAME
```

\(Instead of using `touch`, it is also possible to add `-c` to the first call of `htpasswd`\)

