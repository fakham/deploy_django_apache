# Deploy Django app on linux (apache2 server)

### Video : 

 [YouTube link](https://youtu.be/L0ZiVIXy7w8)

### Commandes : 

```
sudo apt-get update
sudo apt-get install python3-pip apache2 libapache2-mod-wsgi-py3
sudo pip3 install virtualenv
virtualenv myprojectenv
source myprojectenv/bin/activate
pip3 install django
./manage.py collectstatic
sudo nano /etc/apache2/sites-available/000-default.conf

sudo chown :www-data ~/myproject/db.sqlite3
sudo ufw delete allow 8000
sudo ufw allow 'Apache Full'
sudo apache2ctl configtest
sudo systemctl restart apache2
```

### Apache2 config : 

```
Alias /static /home/fakham/MyProject/TestProject/static
<Directory /home/fakham/MyProject/TestProject/static>
    Require all granted
</Directory>

<Directory /home/fakham/MyProject/TestProject/TestProject>
    <Files wsgi.py>
        Require all granted
    </Files>
</Directory>

WSGIDaemonProcess TestProject python-home=/home/fakham/MyProject/myenv python-path=/home/fakham/MyProject/TestProject
WSGIProcessGroup TestProject
WSGIScriptAlias / /home/fakham/MyProject/TestProject/TestProject/wsgi.py
```
