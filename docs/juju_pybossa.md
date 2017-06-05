Installing PYBOSSA with Juju
============================

With this guide you can deploy PYBOSSA using the
[Juju](https://jujucharms.com/docs/stable/getting-started) technology
inside a Virtualbox Virtual Machine (VM) locally. We will use
[Vagrant](https://www.vagrantup.com/) as it will help us to setup the
new VM. This should work on all supported OSes where Vagrant and
Virtualbox run: Windows, OS X, GNU/Linux.

<div class="admonition note">

We use the local installation, but you can use any cloud provider
supported by [Juju](https://jujucharms.com/docs/stable/getting-started).
If you want to use a cloud provider, you only have to instruct Juju to
use a specific cloud one. The charm will work in any of them without
problems. Please check the official documentation for information about
how to configure
[Juju](https://jujucharms.com/docs/stable/getting-started) for [Amazon
EC2](https://jujucharms.com/docs/stable/config-aws) or
[Openstack](https://jujucharms.com/docs/stable/config-openstack).

</div>

Install Virtualbox & Vagrant
----------------------------

We will install PYBOSSA in a local virtual machine so you can delete it
afterwards if you want. This will ensure that your computer is not
polluted with libraries that you will not need any future, containing
everything within the virtual machine.

<div class="admonition note">

If you have access to a cloud service provider like [Amazon EC2](https://jujucharms.com/docs/stable/config-aws) or any

:   [Openstack](https://jujucharms.com/docs/stable/config-openstack)
    solution, you can just skip this section. Be sure to configure juju
    with your cloud credentials. You can find more guides and cloud
    provider configurations
    [here](https://jujucharms.com/docs/stable/getting-started).

</div>

Install Vagrant and Virtualbox if they are not available on your
machine.

### Ubuntu

Just install it using the package manager

    sudo apt-get update 
    sudo apt-get -y install virtualbox vagrant

### Windows & OS X

Install and download [Virtualbox](https://www.virtualbox.org) and
[Vagrant](http://www.vagrantup.com) manually.

Get latest version of PYBOSSA Juju charm
----------------------------------------

You have two options to get the latest version of PYBOSSA Juju charm.
You get a ZIP file with the latest version from this link:
<https://github.com/Scifabric/pybossa-jujucharm/archive/master.zip>

Or you use git to clone it:

    git clone https://github.com/Scifabric/pybossa-jujucharm.git

<div class="admonition note">

If you use the ZIP file, please unzip it before proceeding.

</div>

Go the source code folder

    cd pybossa-jujucharm

Start the VM
------------

This is very easy:

    vagrant up

Setup Juju
----------

SSH to the Vagrant box and **stay** in the VM

    vagrant ssh

Prepare Juju for initial usage:

    juju init
    juju switch local
    juju bootstrap

PYBOSSA bundle
--------------

Install the Pybossa charm bundle which will install PYBOSSA charm and
PostgreSQL charm and connect them to eachother.

    juju deployer -c bundle.yaml

Once is installed, we can install PYBOSSA and connect both of them.

Sentinel and Redis
------------------

You can also install Redis and Sentinel at a later stage using Juju.
This will allow you to add new Redis slave nodes as well as Sentinels to
manage the Redis infrastructure using the load-balanced solution of
Sentinel.

Adding Redis Master and Slave nodes
-----------------------------------

First you need to deploy at least two nodes of Redis: a master and a
slave:

    juju deploy cs:~juju-gui/trusty/redis-1
    juju deploy cs:~juju-gui/trusty/redis-1 redis2

Then, you need link them:

    juju add-relation redis:master redis2:slave

Adding Sentinel node
--------------------

Now you can add the Sentinel

    juju git-deploy Scifabric/redis-sentinel-jujucharm

<div class="admonition note">

If you don't have the git-deploy command for juju, you can install it
with these commands: :

sudo apt-get install python3-pip sudo pip install juju-git-deploy

</div>

And monitor Redis master

    juju add-relation redis-sentinel redis:master

Finally, you can link PYBOSSA to sentinel

    juju add-relation pybossa redis-sentinel

<div class="admonition note">

For more info regarding the Juju charm for Sentinel, please

:   check the official
    [site](https://github.com/Scifabric/redis-sentinel-jujucharm/).

</div>

Access PYBOSSA
--------------

Look for the machine IP of PYBOSSA service here:

    juju status

Copy & Paste the IP and pass it to the following script

    sudo natpybossa 10.0.3.x

Which will map the PYBOSSA server port to your localhost's port 7000.

You can now view PYBOSSA in your browser:

    http://localhost:7000

Email server
------------

PYBOSSA does not need an email server by default, but we encourage you
to install one.

Sending email properly is a bit complicated, as nowadays you have
configure several authentication methods so your emails are not marked
as SPAM or black listed. This configuration involves not only modifying
the config file of your email server, but also the DNS entries of your
server so you can include the proper
[DKIM](https://en.wikipedia.org/wiki/Email_authentication#Authentication_methods)
and
[SPF](https://en.wikipedia.org/wiki/Email_authentication#Authentication_methods)
entries. Therefore, the Juju charm only installs a testing server.

Please, use the official documentation of your preferred server to
configure the email properly.

sshuttle whole network mapping (optional)
-----------------------------------------

This is an alternative way for mapping internal ports to the VM ones.
Instead of using the shell scripts that you have seen before for NAT
configuration, you can use **sshuttle**. In Ubuntu you can install it
with apt-get or in OS X with Homebrew.

The Virtualbox network is only internally visible on the VM side. If you
want to see it on your local browser you need to redirect the VBox
network with your current network (make sure the 10.x.x.x is not already
used!).

The VBox is typically on 10.0.3.xxx. Open a new console on your local
machine and type:

    sshuttle -r vagrant@localhost:2222 10.0.3.0/24

`sshuttle` maybe asks for local sudo password. If it asks for vagrant's
password: `vagrant`

Finally open your browser with the IP you got from `juju status` and
HAProxy, e.g.:

    http://10.0.3.89

Juju GUI (optional)
-------------------

If you prefer a graphical interface, you are covered. Juju provides a
very nice web interface from where you can handle PYBOSSA services. To
use it, follow these steps:

    juju deploy juju-gui

When juju-gui is deployed (can take some time), the command will return
a public IP. You can check the IP also with this command as well as the
status of the deployment of the GUI:

    juju status

Then, copy & paste the IP and pass it as an argument to the following
script

    sudo natgui 10.0.3.x

This file will map the Juju-GUI to your localhost's port 8000, and
return the password for your Juju-GUI. Copy the password, and open the
Juju-GUI in your browser

    https://localhost:8000

If you've used Sentinel, Redis, PostgreSQL, HAProxy and PYBOSSA, your
GUI should show something similar to this:

![image](http://i.imgur.com/XraGePO.png)
