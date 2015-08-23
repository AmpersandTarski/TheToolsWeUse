# Sentinel

The [sentinel](http://sentinel.tarski.nl) is a server on which some tests are run every night. It is the machine where we have regression tests. 

The source code of sentinel is on github too, in the repo called Sentinel

## Access to the sentinel server
The procedure below describes how to create and install an ssl certificate on the Sentinel web server.

First create certificate:

    cd /home/sentinel/authentication
    openssl req -new -x509 -days 999 -keyout tarski.nl.key -out tarski.nl.crt -nodes -subj  '/C=NL/O=Tarski Systems/CN=sentinel.tarski.nl'

This creates the files ```~/authentication/tarski.nl.key``` and ```~/authentication/tarski.nl.crt```. Now add the SSL module to the apache configuration:

    sudo a2enmod ssl

Edit the apache configuration to allow .htaccess files and use the created SSL certificates:

    sudo nano /etc/apache2/sites-available/default-ssl

* In section ```<Directory /var/www/>``` change ```AllowOverride None``` to ```AllowOverride All```
* Comment out old  SSLCertificateFile and SSLCertificateKeyFile entries (using ```#```)
* Add ```SSLCertificateFile /home/sentinel/authentication/tarski.nl.crt```
* Add ```SSLCertificateKeyFile /home/sentinel/authentication/tarski.nl.key```

Finally, restart apache:

    sudo /etc/init.d/apache2 restart
    