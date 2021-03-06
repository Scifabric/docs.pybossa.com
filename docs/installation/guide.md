# Setting things up

Before proceeding to install PYBOSSA, you will need to configure some other applications and libraries in your system. In this page, you will get a step by step guide on how to install all the required packages and libraries for PYBOSSA using the latest [Ubuntu Server Long Term Support](https://wiki.ubuntu.com/LTS) version available at the moment:

- [Ubuntu 18.04 LTS](http://www.ubuntu.com/download/server)


??? Tip "PYBOSSA hosted servers"
    Checkout Scifabric's [hosted PYBOSSA servers](https://scifabric.com/pricing/).

## Installing git - a distributed version control system

PYBOSSA uses the [git](http://git-scm.com/) distributed version control
system for handling the PYBOSSA server source code as well as the
template projects.

[Git](http://git-scm.com/) is a free and open source distributed version control system designed to handle everything from small to extensive projects with speed and efficiency.

To install the software, all you have to do is:

``` bash
sudo apt-get install git
```

## Installing the PostgreSQL database

[PostgreSQL](http://www.postgresql.org/) is a powerful, open source
object-relational database system. It has more than 15 years of active
development and a proven architecture that has earned it a strong
reputation for reliability, data integrity, and correctness.

PYBOSSA uses [PostgreSQL](http://www.postgresql.org/) as the main
database for storing all the data. To install it follow the next steps:

``` bash
sudo apt-get install postgresql postgresql-server-dev-all libpq-dev python3-psycopg2 libsasl2-dev libldap2-dev libssl-dev python3-dev
```

## Installing virtualenv (optional, but recommended)

We recommend installing PYBOSSA using a
[virtualenv](http://pypi.python.org/pypi/virtualenv) as it will create a
an isolated Python environment, helping you to manage different
dependencies and versions without having to deal with root permissions
in your server machine.

[virtualenv](http://pypi.python.org/pypi/virtualenv) creates an
environment that has its installation directories that doesn't
share libraries with other virtualenv environments (and optionally
doesn't access the globally installed libraries either).

You can install the software if you want at the system level if you have root privileges; however, this may lead to broken dependencies in the OS for all your Python packages, so if possible, avoid this solution and use the [virtualenv]http://pypi.python.org/pypi/virtualenv) solution.

Installing [virtualenv](http://pypi.python.org/pypi/virtualenv) in the
Ubuntu server:

``` bash
sudo apt-get install python3-venv
```

After installing the software you will be able to create independent virtual environments for the PYBOSSA installation as well as for the template projects.

## Installing the PYBOSSA Python requirements

Installing the required libraries for PYBOSSA is a step that will need to use some compilers and dev libraries to work. Thus, you will need to install the following packages:

``` bash
sudo apt-get install python-dev build-essential libjpeg-dev libssl-dev libffi-dev
sudo apt-get install dbus libdbus-1-dev libdbus-glib-1-dev libldap2-dev libsasl2-dev
```

Then, you are ready to download the code and install the required
libraries for running PYBOSSA.

!!! note
    We recommend you to install the required libraries using a **virtual environment** with the command virtualenv (you can install the package python-virtualenv). This will allow having all the libraries for PYBOSSA in one folder of your choice, so cleaning the installation would be as simple as deleting that folder without affecting your system.

!!! note
    You might need to use pyenv to install a python 3.6 version in order to run the right version. Please check the official documentation of pyenv.

If you decide to use a **virtualenv** then, follow these steps (lines
starting with **#** are comments):

``` bash
# get the source code
git clone --recursive https://github.com/Scifabric/pybossa
# Access the source code folder
cd pybossa
python3 -mvenv env
# Activate the virtual environment
source env/bin/activate
# Upgrade pip to latest version
pip install -U pip
# Install the required libraries
pip install -r requirements.txt
```

Otherwise, you should be able to install the libraries in your system
like this:


``` bash
# get the source
git clone --recursive https://github.com/Scifabric/pybossa
# Access the source code folder
cd pybossa
# Upgrade pip to latest version
pip install -U pip
# Install the required libraries
pip install -r requirements.txt
```

!!! note
    [Vim](http://www.vim.org/) editor is a very popular text editor for GNU/Linux systems, however, it
    may be difficult for some people if you have never used it before.
    Thus, if you want to try another and much simpler editor for editing
    the configuration files you can use the [GNU
    Nano](http://www.nano-editor.org/) editor.

Create a settings file and enter your SQLAlchemy DB URI (you can also
override default settings as needed):

``` bash
cp settings_local.py.tmpl settings_local.py
# now edit ...
vim settings_local.py
```

!!! note
    Alternatively, if you want your config elsewhere or with different name:
    cp settings_local.py.tmpl */my/config/file/somewhere*
    export PYBOSSA_SETTINGS=/my/config/file/somewhere.

Create the alembic config file and set the sqlalchemy url to point to
your database:

``` bash
    cp alembic.ini.template alembic.ini
    # now set the sqlalchemy.url ...
```

## Installing Redis

PYBOSSA uses Redis not only for caching objects
and speed up the site, but also for limiting the usage of the API
requests.

You can install the latest Redis version downloading the package directly from its official [site](http://redis.io/) site. Since Ubuntu 14.04 you can also, use the internal package:

``` bash
sudo apt-get install redis-server
```

Once you have downloaded it and installed it, you will need to run two
instances:

- **Redis-server**: as a master node, accepting read and write
  operations.
- **Redis-sentinel**: as a sentinel node, to configure the master and
  slave Redis nodes.

### Server

If you have installed the server via your distribution package system,
then, the server will be running already. If this is not the case, check
the official documentation of [Redis](http://redis.io/) to configure it
and run it. The default values should be OK.

!!! warning
    Please, make sure that you are running version >= 2.6


!!! tip
    If you have installed the software using the source code, then, check the contrib folder, as there is a specific folder for Redis with init.d  start scripts. You only have to copy that file to /etc/init.d/ and adapt it to your needs.

### Sentinel

You can run Redis in sentinel mode with the **--sentinel** arg, or by its command named: redis-sentinel. This will vary from your distribution and version of Redis, so check its help page to know how you can run it.

In any case, you will need to run a sentinel node, as PYBOSSA uses it to load-balance the queries, and also to autoconfigure the master and
slaves automagically.

To run PYBOSSA, you will need first to configure a Sentinel node. Create a config file named **sentinel.conf** with something like
this:

```
sentinel monitor mymaster 127.0.0.1 6379 2
sentinel down-after-milliseconds mymaster 60000
sentinel failover-timeout mymaster 180000
sentinel parallel-syncs mymaster 1
```

In the contrib folder, you will find a file named **sentinel.conf** that
should be enough to run the sentinel node. Thus, for running it:

```bash
redis-server contrib/sentinel.conf --sentinel
```

!!! warning
    Please, make sure that you are running version >= 2.6

!!! tip
    If you have installed the software using the source code, then, check the contrib folder, as there is a specific folder for Redis with init.d   start scripts. You only have to copy that file to /etc/init.d/ and adapt it to your needs.

## Speeding up the site

PYBOSSA comes with a cache system that *is disabled by default*. PYBOSSA uses the [Redis](http://redis.io/) server to cache some objects like projects, statistics, etc. The system uses the [Sentinel](http://redis.io/topics/sentinel) feature of [Redis](http://redis.io/), so you can have several master/slave nodes configured with [Sentinel](http://redis.io/topics/sentinel), and your PYBOSSA server will use them "automagically."

### Enabling the cache

Once you have started your master Redis-server to accept connections, Sentinel will manage it and its slaves. If you add a slave, Sentinel will find it and start using it for load-balancing queries in PYBOSSA Cache system.

For more details about [Redis](http://redis.io/) and
[Sentinel](http://redis.io/topics/sentinel), please, read the official
[documentation](http://redis.io/topics/sentinel).

If you want to disable it, you can do it with an environment variable:

``` python
export PYBOSSA_REDIS_CACHE_DISABLED='1'
```

Then start the server, and nothing will be cached.

!!! warning
    We highly recommend you not to disable the cache, as it will boost the performance of the server caching SQL queries as well as page views. If you have lots of projects with hundreds of tasks, you should enable it.

### Running asynchronous tasks in the background

PYBOSSA uses the Python libraries [RQ](http://python-rq.org/) and
[RQScheduler](https://github.com/ui/rq-scheduler) to allow slow or
computationally-heavy tasks to be run in the background in an
asynchronous way.

Some of the tasks are run on a periodic, scheduled, basis, like the
refreshment of the cache and notifications sent to users, while others, like the sending of emails, are created in real time, responding to events that may happen inside the PYBOSSA server (i.e. sending an email with a recovery password).

To allow all this, you will need two additional Python processes to run in the background: the **worker** and the **scheduler**. The scheduler will create the periodic tasks while other tasks will be generated dynamically. The worker will process each of them.

To run the scheduler, just run the following command in a terminal:

``` bash
rqscheduler --host IP-of-your-redis-master-node
```

Similarly, to get the tasks done by the worker, run:

``` bash
python app_context_rqworker.py scheduled_jobs super high medium low email maintenance
```

We also recommend using [supervisor](http://supervisord.org/)
for simply running these processes with a single command.

!!! note
    PYBOSSA relies on the scheduler and the worker for the normal functioning of the server, so make sure you run both services.

## Configuring the DataBase

You need first to add a user to your [PostgreSQL](http://www.postgresql.org/) database:

``` bash
sudo su postgres
createuser -d -P pybossa
```

Use password `tester` when prompted.

!!! note
    You should use the same username that you have used in the
    settings_local.py and alembic.ini files.

After running the last command, you may also have to answer to these questions:

- Shall the new role be a super user? Answer **n** (press the **n**
  key).
- Shall the new role be allowed to create databases? Answer **y**
  (press the **y** key).
- Shall the new role be allowed to create more new roles? Answer **n**
  (press the **n** key).

And now, you can create the database:

``` bash
createdb pybossa -O pybossa
```

Finally, exit the postgresql user:

``` bash
exit
```

Then, populate the database with its tables:

``` bash
python cli.py db_create
```

Run the web server:
``` bash
python run.py
```

Open in your web browser the following URL: [http://localhost:5000](http://localhost:5000)

And if you see the following home page, then, your installation has been
completed:

![image](https://i.imgur.com/hPtgo6S.png)

## Updating PYBOSSA

PYBOSSA v2.9.0 starts using JSONB data type format within the PostgreSQL database. The upgrade should not break anything,
but be aware that all the materalized views will need to be dropped. This is required because some of these views use
the info field and we cannot migrate to JSONB without recreating them.

Thus, be sure to take a full backup before upgrading of your database. Then, delete all your materialized views that create a conflict (by default
PYBOSSA handles the basic ones, but if you have created your own leaderboards, this will not be handled by the script).

Run the migration (see next section) and re-create your materialized views. Most of these views are automatically handled by the background
jobs, so all of them should be recreated by the system without your intervention.

### Updating PYBOSSA core and migrating the database table structure

Sometimes, the PYBOSSA developers add a new column or table to the PYBOSSA server, forcing you to carry out a **migration** of the
database. PYBOSSA uses [Alembic](http://pypi.python.org/pypi/alembic) for performing the migrations, so in case that your production server needs to upgrade the DB structure to a new version, all you have to do is to:
```bash
git pull origin master
pip install -U pip
pip install -U -r requirements.txt
alembic upgrade head
```

The first command will get you the latest source code. The second command updates the libraries. Finally, Alembic upgrades the database structure.

Very occasionally, updates to the core system will also be required. For example, updating [pybossa.js](https://github.com/Scifabric/pybossa.js) in your PYBOSSA theme. To update the default theme, you can do this:

``` bash
cd home/pybossa/pybossa/themes/default
git pull origin master
```

!!! note
    If you are using the [virtualenv](http://pypi.python.org/pypi/virtualenv) be sure to activate it before running the [Alembic](http://pypi.python.org/pypi/alembic) upgrade command.

## Migrating Your Old DB Records

In versions before v0.2.3, the default supported option for the 'long_description' field in projects was HTML. In new versions of PYBOSSA, the default option is Markdown. However, you can use HTML instead of Markdown by modifying the default PYBOSSA theme or using your own forked from the default one.

If you were have been using PYBOSSA for a while you might have projects in your database whose 'long_description' is in HTML format. Hence, if you are using the default theme for PYBOSSA, you will no longer see them rendered as HTML and may have some issues.

To avoid this, you can run a simple script to convert all the
DB project's 'long_description' field from HTML to Markdown, just by
running the following commands:

``` bash
pip install -U pip
pip install -U -r requirements.txt
python cli.py markdown_db_migrate
```

The first command will install a Python package that will handle the
HTML to Markdown conversion, while the second one will convert your DB
entries.

!!! note
    As always, if you are using the [virtualenv](http://pypi.python.org/pypi/virtualenv) be sure to activate it before running the pip install command.

!!! note
    The latest version of PYBOSSA requires PostgreSQL &gt;= 9.3 as it is using materialized views for the dashboard. This feature is only available from PostgreSQL 9.3, so please upgrade the DB as soon as possible. For more information about upgrading the PostgreSQL database check this [page](http://www.postgresql.org/docs/9.3/static/upgrading.html).
