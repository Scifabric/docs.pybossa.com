# Configuring PYBOSSA

The PYBOSSA [settings_local.py.tmpl](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl) file has all the available configuration options for your server. This section, explains each of them and how you should/could use them on your server.

## Official support

If you need help configuring your PYBOSSA server, [contact us](https://scifabric.com/pricing/).
We offer official support and we would love to work with your PYBOSSA server.


## Debug mode

The [DEBUG](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L19) mode is disabled by default in the configuration file, as this should be only used when you are running the server for development purposes. You should not enable this option unless you need to do some debugging in the PYBOSSA server.

## Debug Toolbar

PYBOSSA includes a flag to enable a debug toolbar that can give you more insights about the performance of PYBOSSA. We strongly recommend keeping the toolbar disabled in production environments, as it will slow down considerably all the execution of the code. However, if you are testing the server, feel free to enable it adding the following variable to the settings file:

``` python
ENABLE_DEBUG_TOOLBAR = True
```

## Profiling

PYBOSSA installs [Flask-Profiler](https://github.com/muatik/flask-profiler), an extension that allows you to know which endpoints are being called, and how much time it
takes for them to process each request. You can enable it by setting this config variable in the settings_local.py file:

``` python
FLASK_PROFILER = {
    "enabled": True,
    "storage": {
        "engine": "sqlite"
    },
    "basicAuth":{
        "enabled": True,
        "username": "admin",
        "password": "admin"
    },
    "ignore": [
	    "^/static/.*"
	]
}
```

Now you can access the profiling page: http://server/flask-profiler/.

!!! warning
    Be sure to use a strong password to protect this view as well as HTTPS.

## Host and Port

The [HOST](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L22) and [PORT](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L23) config variables can be used to force the server to listen on specific addresses of your server, as well as at a given port. Usually, you will only need to uncomment the [HOST](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L22) variable to listen on all the network interfaces.

## Securing the server

PYBOSSA uses the [Flask Sessions](http://flask.pocoo.org/docs/quickstart/#sessions) feature that signs the cookies cryptographically for storing information. This improves the security of the server, as the user could look at the contents of the cookie but not modify it, unless they know the [SECRET](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L25) and [SECRET_KEY](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L26).

Therefore, **it is essential that you create a new SECRET and
SECRET_KEY keys for your server and keep them private**. Please, check the [Flask Sessions](http://flask.pocoo.org/docs/quickstart/#sessions) documentation for instructions on how to create proper secret keys.

## Ensuring Anonymous IPs

PYBOSSA uses CryptoPAn to anoymize the user's IPs when they participate as anonymous users. This is a feature that's mandatory, and you will have to create
a KEY for it, specially this one:

``` python
CRYPTOPAN_KEY = '32-char-str-for-AES-key-and-pad.'
```

!!! warning
    Be sure to use a strong key to protect your user IPs.

## Database username and password

PYBOSSA uses the [SQLAlchemy](http://www.sqlalchemy.org/) SQL toolkit to access the DB. In the settings file, you only need to modify the name of the user, password and database name, so it fits your needs in the field SQLALCHEMY_DATABASE_URI:

``` python
SQLALCHEMY_DATABASE_URI = 'postgresql://username:userpassword@localhost/databasename'
```

## Load balancing SQL Queries

If you have a master/slave PostgreSQL setup, you can instruct PYBOSSA to use the slave node for load balancing queries between the master and slave node.

For enabling this mode, all you have to do is adding to the
settings_local.py config file the following:

``` python
SQLALCHEMY_BINDS = {
    'slave': 'postgresql://user:password@server/pybossadb'
}
```

## It's dangerous, so better sign this

PYBOSSA uses the [It's dangerous Python library](http://pythonhosted.org/itsdangerous/) that allows you to send some data to untrusted environments but signing it. It uses a key that the server only knows and uses it for signing the data.

This library is used to send the recovery password e-mails to your
PYBOSSA users, posting a link with a signed key that will be verified by the server. Thus, **it is vital that you create a secure and private key for it in your configuration file**. To do it, just modify the [ITSDANGEROUSKEY](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L35) variable.

## CORS configuration

By default, PYBOSSA has the API endpoints configured with **Access-Control-Allow-Origin:**\*. However, you can change it to whatever you want via the config file. Take a look at the official documentation for [Flask-CORS](http://flask-cors.readthedocs.io/en/latest/) for all the available options.

### Fine tuning CORS

You can fine tune the CORS of PYBOSSA:

```python
CORS_RESOURCES = {
    r"/api/*":
        {
            "origins": "*",
            "allow_headers":
                [
                'Content-Type',
                'Authorization'
                ],
            "max_age": 21600
        }
}
```


!!! note
    You can customize as much as you want CORS. Check the [official documentation](https://flask-cors.readthedocs.io/en/latest/).

## Modifying the Brand name

You can configure your project with a different name, instead of the
default one: PYBOSSA. You only need to change the string [BRAND](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L38) to the name of your organization or project.

## Adding a Logo

By default, PYBOSSA does not provide a logo for the server side, so you will have to copy your logo into the folder: **pybossa/pybossa/static/img**. If the logo name is, **my_brand.png**, the [LOGO](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L40) variable should be updated with the name of the file.

## Multiple languages

By default PYBOSSA only speaks English. However, the default theme comes with a few translations (Spanish, French, Italian, Japanese, Greek and German).

You can enable those translations (mostly user interface strings and
actions) by doing the following: creating a symlink to the translations folders:

``` bash
$ cd pybossa && ln -s themes/default/translations
```

This step will enable the default translations of PYBOSSA for your server. We recommend using these translations with the default theme. If you use your theme, the best thing is to do your translation, (see [translating](/translating.md)), as you might want to name things differently on the templates.

You can disable/enable different languages in your config file
**settings_local.py**. For example, to remove French you can add this configuration to the settings file:

``` python
LOCALES = [('en', 'English'), ('es', u'Español'),
           ('it', 'Italiano'), ('ja', u'日本語')]
```

Also, you can always specify a different default locale using the
following snippet in the same settings file:

``` python
DEFAULT_LOCALE = 'es'
```

!!! note
    PYBOSSA tries first to match the user preferred language from their browser. This will work for anonymous users, while registered ones can specify the language they want using their user preferences.

!!! note
    As an alternative way to allow anonymous users to *force* a different language, PYBOSSA looks for a cookie named **language** where it expects the key of any of the supported languages in the LOCALES list. You can use JavaScript to set it up.

## Creating a theme

PYBOSSA supports themes. By default, it provides its theme that you can use, or if you prefer, you can adapt it to create yours. The default theme for PYBOSSA is available in the [pybossa-default-theme repository](https://github.com/Scifabric/pybossa-default-theme).

To create your theme, all you have to do is to fork the default
theme to your account, and then start modifying it. A theme has a simple structure:

-   info.json: this file includes some information about the author,
    license, and name.
-   static: this folder has all the CSS, JavaScript, images, etc. In
    other words, the static content.
-   templates: this folder has the templates for PYBOSSA.

Therefore, if you want to change the look and feel (i.e., colors of the
top bar) all you have to do is to modify the styles.css file of the
static folder. Or if you prefer, create your own.

However, if you want to modify the structure, let's say you want to
change the order of the elements of the navigation bar: the first item should be the about link, then you will have to modify the files included in the templates folder.

As you can see, you will be able to give a full personality to your own PYBOSSA server without problems.

### Using SASS and minifying JavaScript

PYBOSSA supports SASS thanks to Flask-Assets. If you want to compile SASS or SCSS, just add to your theme static folder a new one named: sass. Then, you can request the compiled version from the templates like this:

``` html
{% assets filters="libsass", output="css/gen/yourcss.min.css",
          "sass/yourcss.scss"%}
    <link rel="stylesheet" type="text/css" href="{{ ASSET_URL }}">
{% endassets %}
```

The same can be done for Javascript using the filter minjs:

``` html
{% assets filters="jsmin", output="gen/packed.js",
          "common/jquery.js", "site/base.js", "site/widgets.js" %}
    <script type="text/javascript" src="{{ ASSET_URL }}"></script>
{% endassets %}
```

## Results page

PYBOSSA allows you to present a results page for your server. Add a file named results.html to the home directory in the templates folder, and you'll be able to show results about your project from one place:

```
 <http://server/results>
```

## Adding your Contact Information

By default, PYBOSSA provides e-mail, and a Twitter handle to show some contact information. If you want, you can change it to your e-mail and Twitter account. You can do it, modifying the following variables in the **settings_local.py** file:

``` python
CONTACT_EMAIL = '<your@email.com>'
CONTACT_TWITTER = 'yourtwitterhandle'
```

## Terms of Use

You can change and modify the [TERMSOFUSE](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L43) for your server, by overriding the provided URL that we use by default.
You can also modify the license used for the data, just change the
DATAUSE link to the open license that you want to use.

## Adding Help page

By default, PYBOSSA provides a help endpoint where you can have your FAQ or similar information for your users. However, it's empty, as each project is unique. For adding that information, create in the theme folder: templates/help/ a file named **index.html** and write your information in there. This will render the information under http://youserver.com/help/


!!! note
    PYBOSSA has dropped support for Social Network logins. If you were using social logins in your project, please, before upgrading double-check that your social login users have added their emails. With their emails you can run the cli.py script to migrate the accounts to local ones. This will delete all their info regarding their social login IDs and make them local accounts. Then the users will be able to request a reset password and log in.


## Receiving e-mails with errors

If you want to receive an e-mail when an error occurs in the PYBOSSA server (webhooks, background jobs, etc.), uncomment the
[ADMINS](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L64) config variable and add a list of e-mails.

### Background jobs error notifications

You can change the default behavior for receiving emails regarding failed background jobs. The two config variables are the following:

```python
FAILED_JOBS_MAILS = 7
FAILED_JOBS_RETRIES = 3
```

FAILED_JOBS_MAILS instructs the system to send you a reminder after seven days if you have not solved the issue with the background job.

FAILED_JOBS_RETRIES instructs the system to retry the job N times. By default is 3.

## Enabling Logging

PYBOSSA can log errors to a [file](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L75) or to a [Sentry](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L73) server. If none of the above configurations are used, you will get the errors in the log file of the web server that you are using (i.e., in nginx the errors will be in /var/log/nginx/error.log).

## Mail Setup

PYBOSSA needs a mail server to validate new accounts, send
e-mails for recovering passwords, etc. , so it is critical that you
configure a server. Please, check the section [Mail setup](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl#L80) in the config file for setting it.

## Global Announcements for the users

Sometimes you will need to send a message to all your users while they are browsing the server. For example, a scheduled shutdown for installing new hardware or a database migration.

PYBOSSA provides a general solution for these announcements via the [settings_local.py.tmpl](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl) configuration file. The announcement feature allows you to send messages to the following type of users:

-   **Authenticated users**, basically all the registered users in the
    server.
-   **Admin users**, all the users that are admins/root on the server.
-   **Project owners**, all the users that have created one or more projects on the server.

Therefore, let's say that you want to warn all your admins that a new configuration will be deployed in your system. In this case, all you have to do is to modify the **ANNOUNCEMENT** variable to display the message for the given type of users:

``` python
ANNOUNCEMENT = {'root': 'Your secret message'}
```

There is an example of the **ANNOUNCEMENT** variable in the
[settings_local.py.tmpl](https://github.com/Scifabric/pybossa/blob/master/settings_local.py.tmpl) file, so you can quickly adapt it for your server. The announcement variable has a **key** and an associated *message**. The supported keys are:

-   **admin**: for admin users.
-   **user**: for all the registered users (even admins).
-   **owner**: for all registered users that have one or more projects.

!!! note
    You can use a mix of messages at the same time without problems, so, for example, you can display a message for Admins and Owners at the same time.

## Disable email notifications

When a PYBOSSA project publishes a blog post, users will get an email (and webpush notification if it is enabled) with the update.

You can disable this behavior with the following flag:

``` python
DISABLE_EMAIL_NOTIFICATIONS = True
```

## Cache

By default PYBOSSA uses Redis to cache a lot of data in order to serve it as fast as possible. PYBOSSA comes with a default set of timeouts for different views that you can change or modify to your own taste. All you have to do is modify the following variables in your settings file:

```python
# Project cache
APP_TIMEOUT = 15 * 60
REGISTERED_USERS_TIMEOUT = 15 * 60
ANON_USERS_TIMEOUT = 5 * 60 * 60
STATS_FRONTPAGE_TIMEOUT = 12 * 60 * 60
STATS_APP_TIMEOUT = 12 * 60 * 60
STATS_DRAFT_TIMEOUT = 24 * 60 * 60
N_APPS_PER_CATEGORY_TIMEOUT = 60 * 60
BROWSE_TASKS_TIMEOUT = 3 * 60 * 60
# Category cache
CATEGORY_TIMEOUT = 24 * 60 * 60
# User cache
USER_TIMEOUT = 15 * 60
USER_TOP_TIMEOUT = 24 * 60 * 60
USER_TOTAL_TIMEOUT = 24 * 60 * 60
```

!!! note
    Every value is in seconds, so bear in mind to multiply it by 60 to have minutes in the configuration values.

### Disabling the Cache

If you want to disable the cache, you only have to export the following env variable:

``` python
PYBOSSA_REDIS_CACHE_DISABLED='1'
```

## Redis configuration

You can configure how you connect to Redis via the following config variables.
If you can't use Redis Sentinel, just set `REDIS_SENTINEL` to `[]` and use
`REDIS_HOST`, `REDIS_PORT` and `REDIS_PASSWORD` instead to specify the
connection details for a vanilla Redis server.

### Redis python prefix

```python
REDIS_KEYPREFIX = 'pybossa_cache'
```

### Redis Sentinel

Specify where the Redis sentinel is listening.

```python
REDIS_SENTINEL = [('localhost', 26379)]
```

### Redis host

Specify the host where the non-Sentinel Redis server is listening.
This option, along with `REDIS_PORT` and `REDIS_PASSWORD`, will be ignored if
`REDIS_SENTINEL` is set.

```python
REDIS_HOST = 'localhost'
```

### Redis port

Specify the port where the non-Sentinel Redis server is listening.
This option, along with `REDIS_HOST` and `REDIS_PASSWORD`, will be ignored if
`REDIS_SENTINEL` is set.

```python
REDIS_PORT = 6379
```

### Redis password

Specify the password of the non-Sentinel Redis server.
This option, along with `REDIS_HOST` and `REDIS_PORT`, will be ignored if
`REDIS_SENTINEL` is set.

```python
REDIS_PASSWORD = '53cr37'
```

### Redis master

Specify the name of the master node.

```python
REDIS_MASTER = 'mymaster'
```

### Redis DB

Specify the DB.

```python
REDIS_DB = 0
```

### Redis Socket timeout

```python
REDIS_SOCKET_TIMEOUT = 0.1
```

### Redis retry on timeout

```python
REDIS_RETRY_ON_TIMEOUT = True
```

## Rate limit for the API

By default, PYBOSSA limits the usage of the API with the following
values:

``` python
LIMIT = 300
PER = 15 * 60
```

Those values mean that when a user sends a request to an API endpoint, a window of 15 minutes is open, and during those 15 minutes the number of allowed requests to the same endpoint is 300. By adding these values to your settings_local.py file, you can adapt it to your own needs.

!!! note
    Please, be sure about what you are doing by modifying these values. This is the recommended configuration, so do not change it unless you are sure.

## Configuring upload method

PYBOSSA by default allows you to upload avatars for users, icons for
projects, etc. using the local file system of your server. While this is
nice for small setups, when you need to add more nodes to serve the same content, this feature could become a problem. For this reason, PYBOSSA also supports cloud solutions to save the files and serve them from there correctly.

#### Local Uploader

The local uploader is configured by default. We recommend having a separate folder for the assets, outside the pybossa folder. In any case, for enabling this method use the following the config settings:

``` python
UPLOAD_METHOD = 'local'
UPLOAD_FOLDER = '/absolute/path/to/your/folder/to/store/assets/'
```

#### Rackspace Cloud Files

PYBOSSA comes with support for Rackspace CloudFiles service, allowing you to grow the services horizontally. Supporting cloud-based system is as simple as having an account in Rackspace, and setting up the following config variables:

``` python
UPLOAD_METHOD = 'rackspace'
RACKSPACE_USERNAME = 'username'
RACKSPACE_API_KEY = 'api_key'
RACKSPACE_REGION = 'region'
```

Once the server is started, it will authenticate against Rackspace and
since that moment, your PYBOSSA server will save files in the cloud.

## Customizing the Layout and FrontPage text

PYBOSSA allows you to override two items:
- **Front Page Text**
- **Footer**

If you want to override those items, you have to create a folder named **custom** and place it in the **template** dir. Then for replacing:

- **The Front Page Text**: create a file named.
  **front_page_text.html** and write there some HTML.
- **The Footer**: create a file named **_footer.html**, and write
  some HTML.

## Tracking the server with Google Analytics

PYBOSSA provides an easy way to integrate Google Analytics with your PYBOSSA server. To enable it you only have to create a file with the name: **_ga.html** in the **pybossa/template** folder with the Google Tracking code. PYBOSSA will be including your Google Analytics tracking code on every page since that moment.

The file **_ga.html** should contain something like this:

``` javascript
<script type="text/javascript">
  var _gaq = _gaq || [];
  _gaq.push(['_setAccount', 'UA-XXXXXXXX-X']);
  _gaq.push(['_trackPageview']);

  (function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
  })();
</script>
```

## Adding a Search box: Google Custom Search

PYBOSSA provides a simple way to search within the server pages: Google Custom Search. To enable it you will have to apply for a Google Custom Search API key and then follow the next steps:

- Copy the Google Custom Search **script** code
- Create a new file called **_gcs.html** in the templates folder
- Paste the previous snippet of code (be sure to delete the
  <gcs:search></gcse:search>; line from it.
- Copy the **_gcs_form.html.template** as **_gcs_form.html** and
  add your key in the input field **cx** (you will find a text like
  XXXXX:YYYY where you should paste your key).

The **_gcs.html** file will have something like this:

``` html
<script>
  (function() {
    var cx = 'XXXXX:YYYY';
    var gcse = document.createElement('script'); gcse.type = 'text/javascript'; gcse.async = true;
    gcse.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') +
        '//www.google.com/cse/cse.js?cx=' + cx;
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(gcse, s);
  })();
</script>
```

And the **_gcs_form.html** will be like this:

``` html
    <form class="navbar-form" style="padding-top:20px;" action="/search">
          <input type="hidden" name="cx" value="partner-pub-XXXXX:YYYYY"/>
          <input type="hidden" name="cof" value="FORID:10" />
          <input type="hidden" name="ie" value="ISO-8859-1" />
          <div class="input-append">
          <input type="text" name="q" size="21" class="input-small" placeholder="Search"  />
          <span class="add-on"><i class="icon-search" style="color:black"></i></span>
          </div>
    </form>
```

After these steps, your site will be indexed by Google, and Google Custom Search will be working, providing for your users a search tool.

## Adding web maps for project statistics (deprecated since v2.9.5)

!!! note
    PYBOSSA does not support this feature anymore since version v2.9.5 as now
    it anonymizes the IPs (following GDPR EU law), so these maps don't make sense anymore.
    For more info, check the [GDPR](/gdpr) section.

PYBOSSA creates for each project a statistics page, where the creators of the project and the volunteers can check the top 5 anonymous and authenticated users, an estimation of time about when all the tasks will be completed, etc.

One exciting feature of the statistics page is that it can generate a
web map showing the location of the anonymous volunteers that have been participating in the project. By default, the maps are disabled, because you will need to download the GeoLiteCity DAT file database that will be used for generating the maps.

[GeoLite](http://dev.maxmind.com/geoip/geolite) is a free geolocalisation database from MaxMind that they release under a
[Creative Commons Attribution-ShareAlike 3.0 Uported
License](http://creativecommons.org/licenses/by-sa/3.0/). You can
download the required file: GeoLite City from this [page](http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz).
Once you have downloaded the file, all you have to do is to uncompress it and place it in the folder **dat** of the pybossa root folder.

After copying the file, all you have to do to start creating the maps is
to restart the server.

## Using your Terms of Use

PYBOSSA has a default Terms of Service page that you can customize it to fit your institutional needs. In the case that you do not want to use the default one, please, create a **_tos.html** file in the **custom** folder. You can re-use the template  **help/_tos.html** and adapt it (it is located in the **template/help** folder.

## Using your Cookies Policy

PYBOSSA has a default cookies policy page, but you can customize it to fit your institutional needs. In the case that you do not want to use the default one, please, create a **_cookies_policy.html** file in the **custom** folder. You can re-use the template **help/_cookies_policy.html** and adapt it (it is located in the
**template/help** folder.

## Using your Privacy Policy

PYBOSSA has a blank privacy policy page. We recommend you to add one, so your users know how you are using their data. To add it, just create a file named **_privacy_policy.html** file in the **custom** folder.

## Exporting data to a CKAN server

[CKAN](http://ckan.org) is a powerful data management system that makes data accessible – by providing tools to streamline publishing, sharing, finding and using data. [CKAN](http://ckan.org) is aimed at data publishers (national and regional governments, companies and
organizations) wanting to make their data open and available.

PYBOSSA can export project's data to a [CKAN](http://ckan.org) server. To use this feature, you will need to add the following config variables to the settings_local.py file:

``` python
# CKAN URL for API calls
CKAN_NAME = "Demo CKAN server"
CKAN_URL = "http://demo.ckan.org"}
```

As [CKAN](http://ckan.org) is open source, you can install your own
[CKAN](http://ckan.org) server and configure it to host the data generated by your PYBOSSA projects quite quickly, making it the data repository for your projects. Another alternative is to use the [the
Data hub](http://datahub.io) service that it is a free CKAN service for hosting your data.

## Enforce Privacy mode

Some projects sometimes need a way to protect their contributors due to their nature. In these cases, where privacy is critical, PYBOSSA allows you to **lock** all the public pages related to the users and statistics about the site and projects. Specifically,
by enabling this mode, only administrators will be able to see the
following pages:

- http://server/stats
- http://server/account/
- http://server/account/user/
- http://server/project/stats

Anonymous and authenticated will see a warning message like this:

![image](https://i.imgur.com/a1aqSCC.png)

Additionally, the footer and front page top users will be removed with links to all these pages. If your project needs this type of protection you can enable it by changing the following config variable in your **settings_local.py** file from:

``` python
ENFORCE_PRIVACY = False
```

To:

``` python
ENFORCE_PRIVACY = True
```

!!! note
    This feature is disabled by default.

## Making extra key/value pairs in info field public

By default, PYBOSSA protects all the information the info field except for those values that are public like the URL of the image of the project, the container where that picture is stored and a few extra. While this will be more than enough for most projects, sometimes, a server will need to expose more information publicly via the info field for the User and Project Domain Objects.

Imagine that you want to give badges to users. You can store that
information in the User domain object, within the info field in a field
named *badges*. While this will work, the API will hide all that
information except for the owner. Thus, it will be impossible to show
user's badges to anonymous people.

With projects, it could be the same. You want to highlight some info to anyone, but hide everything else.

As PYBOSSA hides everything by default, you can always turn on which other fields from the info field can be shown to anonymous users, making them public.

!!! warning
    Be very careful. If you expose your private data via this field, it's your responsibility as this is disabled by default in PYBOSSA.

If you want to make some key/values public, all you have to do is add them to the settings_local.py file the following config variables:

``` python
PROJECT_INFO_PUBLIC_FIELDS = ['key1', 'key2']
USER_INFO_PUBLIC_FIELDS = ['badges', 'key2', ...]
CATEGORY_INFO_PUBLIC_FIELDS = ['key1', 'key2']
```

Add as many as you want/need. But please, be careful about which information you disclose.

## Adding custom project templates

PYBOSSA supports different types of templates that you can offer for
every project. By default, PYBOSSA comes with the following templates:

- **Basic**: the most basic template. It only has the necessary structure to develop your project.
- **Image**: this template is for image pattern recognition.
- **Sound**: similar to the image template, but for sound clips
  hosted on SoundCloud.
- **Video**: similar to the image template, but for video clips
  hosted on Vimeo or Youtube.
- **Map**: this template is for geocoding projects.
- **PDF**: this template is for transcribing documents.

If you want to add your templates or remove one, just create in the
settings_local.py file a variable named **PRESENTERS** and add remove the ones you want:

``` python
PRESENTERS = ["basic", "image", "sound", "video", "map", "pdf", "yourtemplate"]
```

**yourtemplate** should be a template that you have to save in the theme folder: **/templates/projects/snippets/** with the same name. Check the other templates to use them as a base layer for your template.

After adding the template, the server will start offering this new template to your users.

In addition to the project templates themselves, you can add some test tasks for those projects so that the users can import them into their projects and start "playing" with them or taking their format as a starting point to create their own. These tasks can be imported from Google Docs spreadsheets, and you can add them, remove them, or modify the URLs of the spreadsheets changing the value of the variable **TEMPLATE_TASKS** in settings_local.py:

``` python
TEMPLATE_TASKS = {
    'image':
    "<https://docs.google.com/spreadsheet/ccc?key=0AsNlt0WgPAHwdHFEN29mZUF0czJWMUhIejF6dWZXdkE&usp=sharing>",
    'sound':
    "<https://docs.google.com/spreadsheet/ccc?key=0AsNlt0WgPAHwdEczcWduOXRUb1JUc1VGMmJtc2xXaXc&usp=sharing>",
    'video':
    "<https://docs.google.com/spreadsheet/ccc?key=0AsNlt0WgPAHwdGZ2UGhxSTJjQl9YNVhfUVhGRUdoRWc&usp=sharing>",
    'map':
    "<https://docs.google.com/spreadsheet/ccc?key=0AsNlt0WgPAHwdGZnbjdwcnhKRVNlN1dGXy0tTnNWWXc&usp=sharing>",
    'pdf':
    "<https://docs.google.com/spreadsheet/ccc?key=0AsNlt0WgPAHwdEVVamc0R0hrcjlGdXRaUXlqRXlJMEE&usp=sharing>"}
```

## Setting an expiration time for project passwords

PYBOSSA allows the owner of a project to set a password so that only people (both anonymous or authenticated) that know it can contribute. By entering this password, the user will have access to the project for a time specified by:

``` python
PASSWD_COOKIE_TIMEOUT = 60 * 30
```
This variable is configured by default to 30 minutes.

## Validation of new user accounts

Whenever a new user wants to sign up, PYBOSSA allows you to add some extra security steps to the process by asking the users to validate a real email account.

However, if you don't need this feature, it can be disabled (as it is enabled by default) with this configuration parameter:

``` python
ACCOUNT_CONFIRMATION_DISABLED = True
```

## Two-factor authentication on login

If you need an extra layer of security for user authentication, PYBOSSA allows you to enable two-factor authentication by setting this configuration value:

``` python
ENABLE_TWO_FACTOR_AUTH = True
```

With this parameter set, after password verification users will receive a one-time code in their email, and will be redirected to a page where they can insert the code to complete the login process.

## Sending weekly email stats to project owners

Project owners that have the pro-flag set to True can receive every week an update with the latest statistics about their projects in their email box.

By default, this email is sent every Sunday. You can modify it in the
settings file by changing it to another day:

``` python
WEEKLY_UPDATE_STATS = 'Tuesday'
```

!!! note
    For the moment the only way to toggle the pro-flag is via the database. It will be fixed in the future.

## Newsletters with Mailchimp

PYBOSSA can show a subscription page to users when they create an
account. By default is disabled.  You can enable it, revealing a page to recently registered users, to check if they want to subscribe or not.

To support newsletters, you'll have to create an account in Mailchimp and get an API_KEY as well as a LIST_ID to add the users.

Once you have those two items you can enable the newsletter subscription adding them to your settings_local.py file:

``` python
MAILCHIMP_API_KEY = "your-key"
MAILCHIMP_LIST_ID = "your-list-id"
```

Restart the server, and you will be done. Now in your MailChimp account, you will be able to create campaigns and communicate with your registered and interested users.

## Enabling the Dropbox Task importer

PYBOSSA also offers the Dropbox importer, which allows importing all kind of files from a Dropbox account directly. To use it,
you'll need to register your PYBOSSA server as a Dropbox app, as
explained [here](https://www.dropbox.com/developers/dropins/chooser/js#setup).

Don't worry about the Javascript snippet part; we've already handled that for you. Instead, get the App key you will be given and add it to
your settings_local.py:

``` python
DROPBOX_APP_KEY = 'your-key'
```


## Enabling the Youtube's Task importer

The Youtube's task importer needs a Youtube server key which you need to create in the [Google API Console](https://console.developers.google.com/) in YouTube Data API.

Once you have an API key, you'll have to add it to your
settings_local.py file:

``` python
YOUTUBE_API_SERVER_KEY = "your-key"
```

For more information on how to get a Youtube server key, please refer to [the official documentation](https://developers.google.com/youtube/registering_an_application#Create_API_Keys).

## Enabling Server-Sent Events

Since PYBOSSA v1.1.0, PYBOSSA supports Server-Sent Events (SSE) in some views. This feature is powerful. However, it brings some issues with it: it needs to run PYBOSSA in asynchronous mode.

As this is not a necessity, by default PYBOSSA has this feature
disabled. PYBOSSA uses SSE to notify users about specific actions (i.e., the result of a webhook in real time).

If you want to enable it, you will have to add to your settings_local.py:

``` python
SSE = True
```

Also, you will need to configure uwsgi and nginx to support SSE events. This is not trivial, as there are several different scenarios, libraries, and options, so instead of recommending one solution, we invite you to read the [uwsgi documentation about it](http://uwsgi-docs.readthedocs.org/en/latest/Async.html), so you can take a decision based on your infrastructure and preferences.

## Latest news from PYBOSSA

Since v1.2.1 PYBOSSA gets the latest news of its new releases, as well as anything related to what Scifabric blogs about regarding the crowdsourcing world. You can add more items if you want, by just adding to your settings_local.py file new ATOM URLs:

``` python
NEWS_URL = ['http:/http:///atomurl1', 'http://atomurl2', ...]
```

## Enabling pro user features

Since version v1.2.2 PYBOSSA, you can specify which features can be only available to pro users or everyone. To modify them, just locate them in the settings_local.py file. By default, they look
like:

``` python
PRO_FEATURES = {
    'auditlog':              True,
    'webhooks':              True,
    'updated_exports':       True,
    'notify_blog_updates':   True,
    'project_weekly_report': True,
    'autoimporter':          True,
    'better_stats':          True
}
```

By choosing "True" on each of them, you are making that specific feature available only to pro users. On the other hand, selecting "False" makes them available to regular users as well.

## Strict Slashes

By default, PYBOSSA distinguishes between two types of URLs for its
endpoints: with and without a trailing slash. In other words, if an endpoint is not declared within the code as accepting both options,
accessing the same endpoint with a trailing slash will return a 404.

For example, the about endpoint:

    GET /about

Will return the page, but with the default configuration it will return
a 404 if you add a trailing slash to it:

    GET /about/

To disable this behavior, enable the STRICT_SLASHES option and set it to False. That option will ensure that both endpoints work with and without the trailing slash.

## Forums

PYBOSSA does not provide its own forum. However, you can use Disqus and integrate it in your PYBOSSA server.

### Disqus Single Sign-On (SSO)

PYBOSSA supports Disqus SSO. However, it is disabled by default. You need to register a Disqus application (see their [documentation](https://help.disqus.com/customer/portal/articles/236206)) and then update your settings_local.py file with the following two keys:

``` python
DISQUS_SECRET_KEY = 'secret'
DISQUS_PUBLIC_KEY = 'publickey'
```

Then, this will enable you to use a new Jinja2 filter for  authenticating PYBOSSA users directly in their Disqus server. The filter is *disqus_sso*. You can use it like this:

``` jinja2
{% if current_user.is_authenticated() %}
{{ current_user | disqus_sso | safe }}
{% else %}
{{ None | disqus_sso | safe }}
{% endif %}
```

Also, if you are building a Single Page Application, you can use our API endpoint: *api/disqus/sso* to get the credentials and authenticate the users within your javascript. Check the [endpoint information Disqus-API](../build/api.md#disqus-single-sign-on-sso).

## Background jobs timeout

By default PYBOSSA timeout for every job is 10 minutes. In principle, it should be fine, but each project and server is unique, so if you start
seeing too many jobs failing because the job timed out, then, increase the value using these config variables:

``` python
MINUTE = 60
TIMEOUT = 20 * 60
```

Web Push notifications
----------------------

!!! note
    You need to have HTTPS enabled for your site. Otherwise, you will need to use a subdomain from onesignal.com to support this feature. If you cannot use HTTPS, we recommend to disable it.

PYBOSSA can send web push notifications to Google Chrome, Mozilla
Firefox and Safari browsers.

For supporting this feature, PYBOSSA uses the Onesignal.com service. You will need an account and create an app for your PYBOSSA server. Then follow their documentation to download the WebPush SDK and configure your PYBOSSA theme.

For more info regarding Onesignal, check their [documentation.](https://documentation.onesignal.com/docs/web-push-setup)

!!! note
    You can host the SDK files in the static folder of your theme. However, you will need to modify your web server (Apache or Nginx) to serve those files as from the root of your server. If this is not done correctly, it will not work.


Once you have created the app in Onesignal, get the API KEY and APP ID. Then copy them and put it in your settings_local.py file:

``` python
ONESIGNAL_APP_ID = 'app-id'
ONESIGNAL_API_KEY = 'app-key'
```

Restart the server, and add one background worker for the *webpush* queue. This queue will handle the creation of the apps, as well as sending the push notifications.

Then you will need to update your PYBOSSA theme to allow your
users to subscribe. As this could vary a lot from one project to
another, we do not provide a template but some guidelines:

- Use the JS SDK to subscribe a user to a given project using the
  *tags* option of Onesignal.
- PYBOSSA sends notifications using those tags thanks to the   *filters* option that allows us to segment traffic. PYBOSSA is
  expecting the project.id as the tag key for segmenting.
- The JS SDK allows you to subscribe/unsubscribe a user to a given project (not only the whole server) with unique methods for adding tags and deleting them. This works independently if the user is authenticated or not.

For more info regarding Onesignal JS SDK, check their [documentation.](https://documentation.onesignal.com/docs/web-push-sdk)

## Ignore specific keys when exporting data in CSV format

Sometimes your PYBOSSA project saves information like GeoJSON within the tasks or task_runs. This is a bad thing for the exporter, as it will try to flatten it. In such scenarios, you want to instruct PYBOSSA to ignore those keys, as they will be included in the JSON export files, and reduce all the overhead (as well as destroying the format due to the normalization).

For ignoring a key (or a list of keys), just add the following config
variable to your settings_local.py file:

``` python
IGNORE_FLAT_KEYS = [ 'geojson', 'key1', ...]
```

## Specify a new root key instead of info for CSV exporter

Sometimes you need to change the root key for the CSV exporter. This usually happens, when you have to store one ore more answers within the same info object. For this reason, you can instruct PYBOSSA to use that key instead of *info* for flattening the data:

``` python
TASK_CSV_EXPORT_INFO_KEY = 'key'
TASK_RUN_CSV_EXPORT_INFO_KEY = 'key2'
RESULT_CSV_EXPORT_INFO_KEY = 'key3'
```

In this way, if key, key2 or key3 have an array or list of dictionaries, PYBOSSA will iterate over them, flat them, and then generate the CSV for you.


## Disable task presenter check for pure JavaScript apps

When you are using PYBOSSA native JSON support, you will not be building your project presenter within the PYBOSSA structure, but within the JS framework of your choice.

In such a case, you would like to disable the check for the task_presenter when publishing a project. If you need this, just add
this flag to your settings_local.py file:

``` python
DISABLE_TASK_PRESENTER = True
```

## Consent field for users

Sometimes you will need the users to click on a checkbox before
creating an account to get the agreement for sending them email
notifications or of any other type. By default, PYBOSSA provides this
flag, and it's set to False.

Change in the theme (or your frontend) the label of the field to
whatever you prefer: Terms of Service, Communications, etc. so you will be able to keep track of who has accepted/declined to get notifications from you.

## Custom Leaderboards

By default, PYBOSSA provides a unique leaderboard. This leaderboard is based on the number of task runs that a user has submitted. However, you may want more flexibility. For this reason, you can use use the "user".info field to store any other "badges" or values that you want to score your users.

If your users have identified very complicated stuff, and you want to
give points to them based on that, just use the info field and instruct
PYBOSSA to create a leaderboard for you.

!!! note
    It is essential that this key, projectsvalue pair is computed by you. You can use the API to update these values, so this will not be handled by PYBOSSA but by yourself.

Imagine the score is named: foo, then, PYBOSSA will create for you a leaderboard using that key like this: edit the settings_local.py file
and add the following config variable:

``` python
LEADERBOARDS = ['foo']
```

Then, you can access the specific leaderboard using the endpoint:
/leaderboard/?info=foo

As simple as that.

!!! note
    This feature relies on background jobs. Be sure that you are running them.

### Default number of users for the leaderboard

You can specify the default number of users shown in the leaderboard. By default we show the top 20 users.

```
LEADERBOARD = 20
```

## Unpublish inactive projects

PYBOSSA by default unpublishes projects that have not been active in the last three months. You can disable this feature by changing this config variable in your settings_local.py file:

``` python
UNPUBLISH_PROJECTS = False
```

## LDAP integration

PYBOSSA can use LDAP for authenticating users. You will need to add a few config variables to the settings\_local.py file to
make it work.

PYBOSSA supports LDAP and OpenLDAP protocols, so you should be able to use any of them.

!!! note
    By enabling PYBOSSA LDAP integration, all other means for creating accounts and sign in will be disabled.

### LDAP_HOST

This variable should have the IP or domain name of your LDAP server.

### LDAP_BASE_DN

This is the LDAP Base DN for your organization.

### LDAP_USERNAME

This variable should have the admin account so that PYBOSSA can access the LDAP server and search for users.

### LDAP_PASSWORD

The admin account password.

### LDAP_OBJECTS_DN

The DN.

### LDAP_OPENLDAP

Set it to True if you are using it.

### LDAP_USER_OBJECT_FILTER

This is important. The filter that you write in here needs to be
adapted to your institution, otherwise, it will not work when
authenticating and validating your users.

Don't use the default configuration in the settings template. You will
need to adapt it to your needs.

### LDAP_USER_FILTER_FIELD

If you use a different field in the previous configuration, update the
LDAP_USER_FILTER_FIELD. It's important to reflect which key are you using within your LDAP server to identify your users uniquely.

### LDAP_PYBOSSA_FIELDS

Use this configuration variable to match/link PYBOSSA fields to LDAP fields.

## Uploading files to PYBOSSA

PYBOSSA has a generic uploader that will check for valid extensions, avoiding for example that a user could upload a video, as only
images are allowed.

### ALLOWED_EXTENSIONS

Use this configuration variable, to specify which types of files will you allow in your server to be uploaded via the API. By default, the following extensions
are enabled:

``` python
ALLOWED_EXTENSIONS = ['js', 'css', 'png', 'jpg', 'jpeg', 'gif', 'zip']
```

## SPAM protection

You can blacklist disposable email accounts by listing them in the SPAM config. Just add them like this:

``` python
SPAM = ['spam.com', 'fake.es']
```

## Failed Jobs

Sometimes background jobs fail. For example, an email is rejected. By default
PYBOSSA retries 3 times, before marking them as failed. You can customize it.

```python
FAILED_JOBS_RETRIES = 3
```

## Fulltext search language

PYBOSSA uses PostgreSQL fulltex search support. Thus, you can instruct PYBOSSA
to use only a given language to do it properly:

```python
FULLTEXTSEARCH_LANGUAGE = 'english'
```

## Absolute links to Avatars

If you are building a Single Page Application or a Universal App, you will need to
get absolute paths to the avatars. Use the following config:

```python
AVATAR_ABSOLUTE = True
```

## Delete inactive accounts

PYBOSSA will delete inactive accounts after a period of time. For this purpose,
PYBOSSA uses two different background jobs, one for warning users about the
action, and another one to delete them.

The warning job is run on a monthly basis, while the deletion is done on a
bi-monthly basis.

You can customize the the time period that you consider to warn users as well as
to delete them. For these purposes you can use the following two variables:

```python
USER_INACTIVE_NOTIFICATION = 5
USER_DELETE_AFTER_NOTIFICATION = '1 month'
```

Thus, after 5 months of not contributing a single task run, the user will get an
email warning her about the deletion. Then, the next month if the user has not
sent a task run, the account will be deleted.

For deleting the accounts, PYBOSSA uses the the same method as if the user
requested it herself. The action anonymizes the user's contributions, and
deletes all her personal data.


!!! note
    PYBOSSA will not delete users with the restrict flag set to true (to respect
    GDPR) as well as if they have projects.
