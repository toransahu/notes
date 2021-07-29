# Python Production Servers

[TOC]

# Basics

## Web Server

### ngnix

## Application Server

### django developement server

### gunicorn

## Database

### MySQL
### PostgreSQL


# Github Pages Hosting
Source1: https://medium.freecodecamp.org/hosting-custom-domain-on-github-pages-8c598248d2bc
Source2: https://medium.com/employbl/launch-a-website-with-a-custom-url-using-github-pages-and-google-domains-3dd8d90cc33b


# PythonAnywhere

## Settings

## WSGI

## Static Files:
- make a folder sitewide say 'allstatic'
- by default in settings.py STATIC_URL = '/static/' (don't change it)
- in pythonanywhere web, set URL = /static/ same as above & Directory = path to the dir 'allstatic'


# Heroku

## Pre-requisites
 - a working django app
 - app in a git repo

## Install heroku CLI

## Create app
- create heroku app from existing code (it will only create empty git repo in heroku's private git)
```
heroku create appname
```

- add heroku remote to your local git repo
```
git remote add heroku https://git.heroku.<app_name>.git
```

## Add Procfile
- its starter script which heroku follows
- add web: gunicorn --pythonpath toransahu-site toransahu.wsgi  
(here --pythonpath is used if `toransahu` is not root dir, or if wsgi.py is not directly under toransahu-site)

## Dependencies
- add all requirements inside requirements.txt
- including gunicorn

## Push code
- push code to heroku's git repo named <app_name>
```
git push heroku dev:master
```

- here
    - heroku is remote name (same as origin by deafult)
    - dev is local repo's brach name from which we want to push code
    - master is heroku's master branch (in master branch only build happens)

## Add .env file
Unknown

## Add app.json file
Unknown

## Troubleshoot
- using 
    - heroku local
    - heroku local web
    - heroku logs
- disable static files
```
heroku config:set DISABLE_COLLECTSTATIC=1 
```


# AWS
- https://pipelines.puppet.com/docs/tutorials/how-to-set-up-aws-ec2/
- https://www.agiliq.com/blog/2014/08/deploying-a-django-app-on-amazon-ec2-instance/
- https://medium.com/@bsadkhin/deploying-a-django-app-to-amazon-ec2-3f17a735a561

## Create AMI (Amazon Machine Instance)
- choose os, server
- edit configs (optional)
- launch
- create/choose private key
    - name it 
    - **download it**
    - put it in your ~/.ssh/ dir
    - change permission to read only chmod 400
- notedown DNS of your instance
    ec2-18-136-106-117.ap-southeast-1.compute.amazonaws.com
- if os was ubuntu, default user will be ubuntu
- create security group & make changes in inbound tab like:
    
|Type|Port|Source|
|----------------|
|HTTP|80|Anywhere|
|HTTPS|443|Anywhere|
|SSH|22|Anywhere|
|Custom TCP|8000|Anywhere|

## SSH to your instance
- using instance dns  
    `ssh -i ~/.ssh/ethereal-site-backend.pem ubuntu@ec2-18-136-106-117.ap-southeast-1.compute.amazonaws.com`

- or use public ip  
    `ssh -i ~/.ssh/ethereal-site-backend.pem ubuntu@18.136.106.117` 
    
- if `.pem` file is downloaded from some storage, then give proper permission
```bash
chmod 600 ~/.ssh/ethereal-site-backend.pem
```

## Update
```bash
   sudo apt-get update
   sudo apt-get upgrade
```

## Set Password 
Source: https://comtechies.com/password-authentication-aws-ec2.html
```bash
#1.open
sudo vi /etc/ssh/sshd_config

#2.edit no to yes
PasswordAuthentication yes

#3.save and close

#4.change/set password
sudo passwd ubuntu

#5.restart service
sudo service sshd restart
```

## Install Prerequisites

### Python Stuff

#### Recommanded Way

- Using miniconda

```bash

#download miniconda - for deployment, testing, build
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh

#install
sudo sh Miniconda3-latest-Linux-x86_64.sh 


#alias & activate miniconda
echo "alias anaconda='. ~/miniconda3/bin/activate'" >> ~/.bashrc

anaconda

(base) sudo /home/ubuntu/miniconda3/bin/python3.6 -m pip install -U pipenv

#clone repo
(base) git clone https://toransahu@bitbucket.org/toransahu/ethereal-machines-backend.git 

#cd to repo & create venv using pipenv & install dependencies
(base) pipenv --python 3 install
```

#### Original Way

```bash

sudo wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tar.xz
sudo tar xJf Python-3.6.4.tar.xz 
cd Python-3.6.4/
./configure

sudo make
sudo make install

cd ..
sudo rm Python-3.6.4.tar.xz
sudo rm -rf Python-3.6.4


sudo apt install python3-pip

#link pip, python

cd /usr/bin
unlink python
unlink pip
unlink virtualenv

ln -s python35 python
ln -s pip-3.5 pip
ln -s virtualenv-3.5 virtualenv

#clone repo

git clone https://toransahu@bitbucket.org/toransahu/ethereal-machines-backend.git 
```

- if sudo ./configure gives error
    - Error: `no acceptable C compiler found in PATH when installing python`
    - install build-essential 
    `sudo apt install build-essential`
    

#### Test your project by starting up the Django development server with this command:
- before this, disable other https/secure settings in prod_settings.py or test with dev_settings.py
- allow server to listen on port 8000
    - `sudo ufw allow 8000`
- `python manage.py runserver 0.0.0.0:8000`
    - if you get error, add host to allowed host.
        - `ec2-18-136-106-117.ap-southeast-1.compute.amazonaws.com`
    - hit the website
        - ec2-18-136-106-117.ap-southeast-1.compute.amazonaws.com:8000 **(without http://)**

### Server Stuff

#### Gunicorn

- will server dynamic contents of the site (works as app server)

- install in venv using `pipenv --python 3`
    - `(app-venv) pipenv --python 3 install gunicorn`
    
- test django app with gunicorn
    - allow server to listen on port 8000
        - `sudo ufw allow 8000`
    - cd ethereal-machines-backend/src (where manage.py is)
    - disable other https/secure settings in prod_settings.py
    - to degug, enable DEBUG
    - gunicorn --bind  0.0.0.0:8000 backend.wsgi (try website with http://), 
    
    
- create script to start gunicorn
    - cd ethereal-machines-backend/src (where manage.py is)
    - vim start_gunicorn.sh
        - make sure to write #! /bin/bash in first line
    - chmod a+x start_gunicorn.sh
    - start_gunicorn.sh should look like this: https://gist.github.com/toransahu/31874def1bd661db676d0dfe02e1c651

#### celery
- start rabbitmq
    - starts automatically on boot

    ```bash
    sudo systemctl enable rabbitmq-server
    sudo systemctl start rabbitmq-server
    
    #- in WSL do this
    sudo service rabbitmq-server start
    ```

        
        

- start celery worker
    - need to run inside src folder
    - need to be in virtual env

    ```bash
    celery -A project_name worker -l info
    ```

- or create script to start celery
    - cd ethereal-machines-backend/src (where manage.py is)
    - vim start_celery.sh
        - make sure to write #! /bin/bash in first line
    - chmod a+x start_celery.sh
    - start_celery.sh should look like this: https://gist.github.com/toransahu/31874def1bd661db676d0dfe02e1c651


#### supervisor
- chmod a+x all the start.sh scripts
- copy gunicorn.conf & celery.conf to /etc/supervisor/conf.d/
- create logs folder inside repo dir
- sudo supervisorctl reread
- sudo supervisorctl update
- sudo supervisorctl reload
- sudo supervisorctl status
- sudo supervisorctl restart gunicorn
- sudo supervisorctl restart celery
src: https://gist.github.com/toransahu/31874def1bd661db676d0dfe02e1c651

#### nginx

- will create proxy and redirect to gunicorn for dynamic contents
- will server static & media contents

src: https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-16-04

- install  
    - `sudo apt install nginx`

- start nginx
    - `sudo service nginx start`

- hit the [site](ec2-18-136-106-117.ap-southeast-1.compute.amazonaws.com)  
    - `ec2-18-136-106-117.ap-southeast-1.compute.amazonaws.com`
    - check whether you are getting a msg `Welcome to nginx!` or not
    
- stop nginx
    - `sudo service nginx stop`
    

- Configure nginx to proxy pass to gunicorn
    - configuration file : https://gist.github.com/toransahu/f5a38976967715e31543dbcf9b01c7d9
    - `sudo vim /etc/nginx/sites-available/ethereal_backend`
        - open up new server block
            - should listen on normal port 80
            - should respond to our server domain name or ip i.e. 18.136.106.117 (try both)
                - for longer name you may have to increase buffer by editing
                    - sudo vim /etc/nginx/nginx.conf
                        - change count at server_names_hash_bucket_size 512;
                        
                        
            - **didn't find it usefull without custom domain** create a location / {} block to
                - tell Nginx to ignore any problems with finding a favicon
                - tell Nginx to find static files
                    - here prefix will be same as STATIC_URL
                    - and alias will be same as STATIC_ROOT
                - tell Nginx to find media files
                    - here prefix will be same as MEDIA_URL
                    - and alias will be same as MEDIA_ROOT
                    
            - **didn't find it usefull without custom domain** create a location / {} block to match all other requests
                - include the standard proxy_params file included with the Nginx installation
                - then pass the traffic to the socket that our Gunicorn process created i.e. http://0.0.0.0:8000
                    - or may be now you need to provide link with server_name and different port on which application is running
                    - e.g http://server_name:8000
                    
                    
                    
    - enable the file by linking it to the sites-enabled directory
        - `sudo ln -s /etc/nginx/sites-available/ethereal_backend /etc/nginx/sites-enabled`
    - test nginx config for syntax errors
        - `sudo nginx -t`
    - if no errors reported then go ahead & restart nginx
        - `sudo systemctl restart nginx`
    
    - Finally, we need to open up our firewall to normal traffic on port 80. Since we no longer need access to the development server, we can remove the rule to open port 8000 as well
        - `sudo ufw delete allow 8000`
        - `sudo ufw allow 'Nginx Full'`
        

- set host (for custom root/domain url for hyperlinks inside django app)
    - e.g. https://api.etherealmachines.com/file/media/1/djklfjkdflkfsdaf.png
    - need to set in /etc/nginx/sites-available/ethereal_backend
        - proxy_set_header Host "api.etherealmachines.com"
    - refer: https://gist.github.com/toransahu/f5a38976967715e31543dbcf9b01c7d9
    - make sure "api.etherealmachines.com" is included in `ALLOWED_HOSTS` in `prod_settings.py`

- for size limit issues
    - if total cient body exceeds defined limit in `nginx.conf` file, it (web server) throws HTTP error 413, request before reaching to the application server
    - to handle the size limit, mention `client_max_body_size 10M;` in `nginx.conf` inside `http {}` block


Note: comment out SSL on and redirect HTTPS line in ethereal_backend file if don't using ssl & https

## Setup Database

### AWS RDS MySQL (Free Tier)

#### RDS Config

- source: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateInstance.html
- in selected security group add
    - Type:MYSQL/Aurora;Protocol:TCP;Range:3306;Source:Anywhere(0.0.0.0/0)
    
- enable public use/access
    - to access db over internet
    
- http://ec2-18-136-106-117.ap-southeast-1.compute.amazonaws.com:8000/api/v1/ (optional)    


#### Installation
- install mysqlclient in venv
    - pipenv install mysqlclient
    - if it gives error: `mysql_config not found`
        - install following
            - sudo apt-get install libmysqlclient-dev

#### Django Configuration

- instance
    - etherealbackend
- db
    - ethereal
    
- host
    - etherealbackend.cg17v7dkjshh.ap-southeast-1.rds.amazonaws.com
- port
    - 3306

- master user
    - ethereal 

- master pwd
    - machines

#### Test Django with RDS MySQL
- python manage.py makemigrations <app_name>
- python manage.py migrate
- python manage.py runserver 0.0.0.0:8000


## Run 

### Confirm before run
```bash
python manage.py makemigrations <apps>

python manage.py migrate

python manage.py createsuperuser

python manage.py collectstatic
```

- `cd /home/ubuntu/ethereal-machines/ethereal-machines-backend/`
- `./start_gunicorn.sh`
- `sudo systemctl restart nginx`


## Enable HTTPS in aws ec2 with nginx
- [Blog source](https://medium.freecodecamp.org/going-https-on-amazon-ec2-ubuntu-14-04-with-lets-encrypt-certbot-on-nginx-696770649e76) 
- [Official Source- Ubuntu 16.04 + nginx](https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx) 
- using lets-encrypt  CA (certificate authority)
    - provides free SSL certificates
    - for few weeks/ 3 months
- using Certbot - the official lets-encrypt client
    - automatically fetches & deploys SSL/TLS certificates in the server
    

### Make sure HTTP & HTTPS are opened in Security Groups
- inside inbound rules

- note down public IP & DNS of the aws ec2 instance


### Setup domain's CNAME record to the public DNS of ec2
- here domain is: etherealmachines.com
- public dns is: ec2-18-136-106-117.ap-southeast-1.compute.amazonaws.com
- Go to your DNS config in CloudFlare & create an entry in DNS Records
    - type: CNAME
    - Name: api.etherealmachines.com
    - value: ec2-18-136-106-117.ap-southeast-1.compute.amazonaws.com
    - TTL: Automatic
    
### Install Certbot in aws instance
- cd to your home or project root
- `wget https://dl.eff.org/certbot-auto`
- `chmod a+x certbot-auto`

### Stop any existing servers running on the port 80 and 443
- because those will be used by certbot to verify the domain & generate certificates
- after generating certificates, restart servers

### Generate certificates
- `./certbot-auto certonly --standalone -d api.etherealmachines.com`

- we can generate certificates for multiple domains also, like
    - `./certbot-auto certonly --standalone -d api.etherealmachines.com -d www.etherealmachines.com`
    
    
### Change nginx configurations in /etc/nginx/nginx.conf to enable SSL
- https://gist.github.com/toransahu/7b546d1d1a6afdf51dfa6602ecda22fc
- The Strict-Transport-Security (HSTS) header ensures that any internal links that are not HTTPS will automatically be routed to the HTTPS version during a HTTPS session

### Reload nginx config
- test config for syntaxt errors:
    - `sudo nginx -t`
- `sudo service nginx reload`

### Finish
- now https://api.etherealmachines.com will redirect requests to http://ec2-18-136-106-117.ap-southeast-1.compute.amazonaws.com/
    
### Check Certificate Expiry Date
- Install `ssl-cert-check`

```bash
sudo apt install ssl-cert-check
```

- Run

```bash
sudo ssl-cert-check -c /etc/letsencrypt/live/api.etherealmachines.com/fullchain.pem
```

or awk the final result

```bash
sudo ssl-cert-check -c /etc/letsencrypt/live/api.etherealmachines.com/fullchain.pem | awk 'END { print <dollar_sign>NF }'
```

### Renew Certificate

- if cloudflare DNS + HTTP proxy is configured, then it will interfere while renewal and creation of ssl certificate
    - so, disable http proxy (DNS only should be there in status column) from status column
    - source: https://www.tautvidas.com/blog/2018/06/certbot-renewal-of-letsencrypt-certificate-fails-with-failed-authorization-procedure/

- Let's encrypt certificates are only valid for 3 months after issue. So renewal is required. 
    - before using `renew` command turn off nginx to open the port 80
- to check/dry run renewal do:
    ```bash
    sudo certbot renew --dry-run
    ```
    
- automate autonewal using cron job: 
    ```
    0 6 * * * /path/to/certbot/certbot-auto renew --text >> /path/to/certbot/certbot-cron.log && sudo service nginx reload
    ```
    
### delete the certificate
```bash
sudo certbot delete --cert-name  api.etherealmachines.com
```
    
### Troubleshoots
- while certificate renew/new if it fails with TLS handshake/auth issue:
    - remove certificate entry from `/etc/nginx/nginx.conf`
- while renew/new if you get `too many request`/`auth failure`/ `blocked` then wait for 1 hr and retry
    - there is 5 limit per account    


## AWS S3 Storage

Source: 
- https://simpleisbetterthancomplex.com/tutorial/2017/08/01/how-to-setup-amazon-s3-in-a-django-project.html
- http://django-storages.readthedocs.io/en/latest/backends/amazon-S3.html#model
- http://boto3.readthedocs.io/en/latest/guide/quickstart.html#configuration

https://ethereal-erp.s3.amazonaws.com

Credentials
- Users with AWS Management Console access can sign-in at:  
    - https://908866068066.signin.aws.amazon.com/console
- username
    - ethereal
- group
    - erp-programatic
- access key id
    - AKIAIBBFQZVDCT7BR6QA 
- secret access key
    - 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


# Cloudflare

## Manage DNS

## Manage Cache 
### Purge Cache
-  By API

    ```bash
    curl -X DELETE "https://api.cloudflare.com/client/v4/zones/<site-id>/purge_cache" \
         -H "X-Auth-Email: <email>" \
         -H "X-Auth-Key: <apikey>" \
         -H "Content-Type: application/json" \
         --data '{"purge_everything":true}')"
    ```    

    - source: https://www.supertechcrew.com/clear-cloudflare-cache-when-pushing-from-git-github-pages/

- By Git while Pushing 
    - Sources: 
        - https://www.supertechcrew.com/clear-cloudflare-cache-when-pushing-from-git-github-pages/
        - https://www.binarymoon.co.uk/2017/06/using-git-hooks-clear-cloudflares-cache/

- By Website

# TODO:   
- before nginx   
    - ~~correct  start_gunicorn.sh  with log & workers~~
    - ~~if possible see pipenv shell~~
    - ~~MySQL setup~~
- nginx
    - ~~proxy~~
    - ~~static issue~~
        - ~~try by removing STATIC_FINDER in PROD_.py~~
    - ~~media issue~~

- ~~bind with https://api.etherealmachines.com~~

- in code:
    - utils/__init__.py
        - ~~mysql case: db name dynamic~~
    - ~~dev & prod settings~~
    - ~~media url append in urls.py ~~
        - ~~remove DEBUG is True condition~~
- implement task queue using Celery
    - to make post_save faster
    - http://www.dougalmatthews.com/2011/Oct/10/making-djangos-signals-async-with-celery/
- configure https in django+aws level        

