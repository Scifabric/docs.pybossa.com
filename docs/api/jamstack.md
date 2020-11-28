# Jamstack for PYBOSSA

If you want to use a frontend server like NuxtJS or Next, you will have to configure PYBOSSA properly to run within your frontend framework.


## Authentication

PYBOSSA uses signed cookies to authenticate the users and keep their sessions. As we use cookies, we will have to tell PYBOSSA how to configure them to work with you.

### Cookies configuration

In your settings_local.py file add the following:

```python
REMEMBER_COOKIE_DOMAIN = 'yourdomain.com'
SESSION_COOKIE_DOMAIN = 'yourdomain.com'
SESSION_COOKIE_SAMESITE = None
```

This will ensure that the cookie will be set for your session from the frontend site, and will be sent back to the backend for authenticating the user.

### NuxtJS configuration

If you are using NuxtJS with Axios, you will have to configure first Axios like this in the nuxt.config.js file:

```json
  axios: {
    baseURL: 'https://yourpybossaserver.com/',
    credentials: true,
    proxyHeaders: true,
    headers: {
      'Content-Type': 'application/json',
    },
  },
```

Then be sure to make a first request from the client side to get the cookie and get it stored on the browser. Then you can authenticate the user:

* First use axios to get the login page: this.$axios.$get('/account/signin?response_format=json')
* This request will return the CSRF token that you will need to send as a header (check the API section for more details)
* Then do a post with the user login credentials: this.$axios.$post('/account/siginin?response_format=json')

Thant's all. Be sure to have the domain set it up properly, as any typo will make things harder to debug.

!!! note
    If you are not setting the cookie properly you will get a CSRF token error, as it is not validated properly.

!!! note
    If you want to develop in your own machine, be sure to set up in your /etc/hosts a subdomain from your server so you can run the NuxtJS server from there. This will ensure that you can test the cookis without having to deploy it.


## Project publication

As you will not need a task template, you can disable it in the config of PYBOSSA:

```
DISABLE_TASK_PRESENTER = True
```

