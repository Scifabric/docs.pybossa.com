# Deploying PYBOSSA with nginx and uwsgi

This section describes how to make PYBOSSA run as a service or daemon permanently in the background. This is useful if you want to run a production-ready single PYBOSSA web server. 

??? Tip "PYBOSSA hosted servers."
    Checkout Scifabric's [hosted PYBOSSA servers](https://scifabric.com/pricing/).

Pre-requisites:

- nginx
- uwsgi
- supervisord
- Redis and sentinel as service (with supervisord)
- RQ-Scheduler and RQ-Worker as service (with supervisord)
- PYBOSSA as service (with supervisord)

## First steps

First things first, be sure that you have followed the [installation guide](guide.md) before starting the deployment. We highly recommend installing PYBOSSA under a regular user (without any privileges) to run the PYBOSSA technology. We will refer to this user as *pybossa*.

## Installing nginx and uwsgi

You have to install nginx and uwsgi on your server machine. In a
Debian/Ubuntu machine you can install them running the following
commands:

``` bash
sudo apt-get install nginx
```

In the (virtualenv-)installation directory of pybossa, you need to
install uwsgi:

``` bash
pip install -U uwsgi
```

## Configuring nginx and uwsgi for PYBOSSA

We assume you only want to run PYBOSSA on your nginx web server. If you need to run also other services on the same server, you need to modify the nginx config files!

You have to copy and adapt the following files from your local PYBOSSA installation:

- contrib/nginx/pybossa
- contrib/pybossa.ini

The PYBOSSA virtual host file (**contrib/nginx/pybossa**) has the
following directives:

```
location / { try_files $uri @pybossa; }

location @pybossa {
    include uwsgi_params;
    uwsgi_pass unix:/tmp/pybossa.sock;
}

location  /static {

            # change that to your pybossa static directory
            alias /home/Scifabric/pybossa/pybossa/themes/default/static;

            autoindex on;
            expires max;
        }
```

You can specify a user and group from your machine with lower privileges to improve the security of the site. You can also use the www-data user and group name.

Once you have adapted the PATH in the alias in that file, copy it into
the folder:

``` bash
sudo cp contrib/nginx/pybossa /etc/nginx/sites-available/.
```

Please delete the default config in sites-enabled (do not worry there is a backup):

``` bash
sudo rm /etc/nginx/sites-enabled/default
```

Enable the PYBOSSA site:

``` bash
sudo ln -s /etc/nginx/sites-available/pybossa /etc/nginx/sites-enabled/pybossa
```

And restart the server:
``` bash
sudo service nginx restart
``` 

## Creating the pybossa.ini file for uwsgi

You have to copy the **pybossa.ini.template** file to pybossa.ini in
your PYBOSSA installation and adapt the paths to match your
configuration!

The content of this file is the following:

``` python
[uwsgi]
socket = /tmp/pybossa.sock
chmod-socket = 666
chdir = /home/pybossa/pybossa
pythonpath = ..
virtualenv = /home/pybossa/pybossa/env
module = run:app
cpu-affinity = 1
processes = 2
threads = 2
stats = /tmp/pybossa-stats.sock
buffer-size = 65535
```

## Install supervisord

[Supervisord](http://supervisord.org/) is used to let PYBOSSA and its RQ system run as Daemon in the background. It shares some of the same goals of programs like launchd, daemontools, and runit.

Install it:

``` bash
sudo apt-get install supervisor
```

## Configure Redis and sentinel as a service with supervisord

First stop Redis service and all running Redis instances with:

``` bash
sudo service redis-server stop
killall redis-server
```

We want to run redis and sentinel with supervisord because supervisord is more reliable when redis crashes (which can happen when you do not have enough RAM). So we disable redis-server daemon service with:

``` bash
sudo rm /etc/init.d/redis-server
```

Go to your pybossa installation directory and copy following files:

``` bash
sudo cp contrib/supervisor/redis-server.conf /etc/supervisor/conf.d/
sudo cp contrib/supervisor/redis-sentinel.conf /etc/supervisor/conf.d/
sudo cp contrib/redis-supervisor/redis.conf /etc/redis/
sudo cp contrib/redis-supervisor/sentinel.conf /etc/redis/
sudo chown redis:redis /etc/redis/redis.conf
sudo chown redis:redis /etc/redis/sentinel.conf
```

Now we restart supervisord (please do a full stop and start as
described):

``` bash
sudo service supervisor stop
sudo service supervisor start
```

To verify the installation,  you can list all redis processes, and you should see a *redis-server* at port 6379 and *redis-sentinel* at port 26379:

``` bash
ps aux | grep redis
```

These two services will now run whenever the server is running (even after reboot).

## Configure RQ-Scheduler and RQ-Worker to run with supervisord

You need to adjust the paths and user account in this two config files according to your installation. Then copy them to supervisor (do not
forget to edit them):

``` bash
sudo cp contrib/supervisor/rq-scheduler.conf.template /etc/supervisor/conf.d/rq-scheduler.conf
sudo cp contrib/supervisor/rq-worker.conf.template /etc/supervisor/conf.d/rq-worker.conf
```

Restart supervisor:

``` bash
sudo service supervisor stop
sudo service supervisor start
```

Verify that the service is running. You should see a rqworker and rqscheduler instance in the console:

``` bash
ps aux | grep rq
```

## Setup PYBOSSA itself

As we are going to run PYBOSSA via nginx, we have to remove from the settings file the HOST and PORT sections. You can also comment them:

``` python
# HOST = '0.0.0.0'
# PORT = 12000
```

After modifying the settings file, add the full server URL where your PYBOSSA is reachable:

``` python
SERVER_NAME = mypybossa.com
PORT = 80
```

## Let PYBOSSA run as service

Finally, we need to let pybossa run as service. Adjust the paths and username again in this file and copy it to the supervisor config directory:

``` bash
sudo cp contrib/supervisor/pybossa.conf.template /etc/supervisor/conf.d/pybossa.conf
```

Edit now the file and adjust the paths & username.

Restart supervisor:

``` bash
sudo service supervisor stop
sudo service supervisor start
```

You should have now a running PYBOSSA production web server on your nginx installation. Open your browser and check your configured domain: http://example.com.

Congratulations! :smile:

## How to update the PYBOSSA service

Upgrading and updating PYBOSSA as service works the same as for the standalone version. Please follow instructions on the [installation instructions](guide.md). Once you have upgraded the code, you will need to restart all supervisor controlled services to get the changes:

``` bash
sudo supervisorctl restart rq-scheduler
sudo supervisorctl restart rq-worker
sudo supervisorctl restart pybossa
```

## Logs of PYBOSSA services

You can find logs of all PYBOSSA services in this directory:

``` bash
cd /var/log/supervisor
```

## Last words about Security and Scaling

This guide does not cover how to secure your PYBOSSA installation. As every web server, you have to make it secure (like, e.g., strong passwords, automatic Ubuntu security updates, firewall, access restrictions). Please use guides on the Internet to do so.

PYBOSSA can also be scaled horizontally to run with redundant servers and with zero downtime over many redis, DB and web servers with load balancers in between.

If you need a secure and scalable PYBOSSA installation, please contact us. We offer hosted PYBOSSA servers, and we will handle all the hosting, customization, administration and setup for you. Check our  [pricing page](https://scifabric.com/pricing/) and get in touch.
