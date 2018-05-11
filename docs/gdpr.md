# GDPR

Since 25 of May of 2018, every European project has to follow the [GDPR law](https://www.eugdpr.org/).

This section explains how PYBOSSA is compliant with it.

## Anonymous contributor IPs

PYBOSSA has two types of users:

* Authenticated, and
* Anonymous.

For the anonymous users, PYBOSSA has used always the IP to identify them, however as they don't have an
account, we cannot know who is the user behind that IP. In order to improve the security, PYBOSSA (since v2.9.3) 
encodes the IP using the technique [Cryptography-based  Prefix-preserving Anonymization](https://www.cc.gatech.edu/computing/Telecomm/projects/cryptopan/) to
ensure that the IPs are anonymous.

Thus, when you download the results or task runs from a project, you will never get the real user's IP as all of them
have been anonymized.

We use the following [Python module](https://github.com/keiichishima/yacryptopan) to perform this task.


## Forget me (or delete your account)

PYBOSSA now allows any user (without a project) to delete its own account. This action cannot be undone.

When a user deletes its account, PYBOSSA will do the following actions:

* Anonymize your task runs. Your user_id will be removed and for each task run PYBOSSA generates a fake IP, so it's impossible to know what have you sent to the server.
* If the server is using Mailchimp integration, delete the user from the Mailchimp list in case the user subscribed to it.
* Delete all personal data from the server (DB).
* Send an email to the user and the administrators of the server, so the user knows that everything has been deleted.

!!! note
    If the server is using DISQUS SSO, PYBOSSA will include a line in the email explaining that as (10 of May 2018) 
    DISQUS does not provide an API method to delete the user account. Therefore, PYBOSSA informs the user that he/she
    will have to delete their account from DISQUS.

## Export your own data

From your personal PYBOSSA account you will be able to export the following data in list of zip files:

* All your personal data.
* All your projects created by you.
* All your contributions (task runs).

PYBOSSA will create a ZIP file and send an email with links to your email. Those links will be only valid
for 3 days (the default configuration) and after that they will be removed.

The ZIP files have your data in JSON format, so you can view it with any text editor as this is a standard format.

## See all my data

You can get all your data first, so you can see it with any text editor in any platform. 

### Migrating from a PYBOSSA server version < v2.9.3

If you server is running a version smaller than v2.9.3 then, you will need to upgrade
the server to the latest version to be GDPR compliant. Then, you will need to anonymize
your stored IPs. PYBOSSA provides a script for doing this task:

``` bash
  python cli.py anonymize_ips
```


!!! note
    We highly recommend to do a backup before running the upgrade and the migration of the DB.


Next, you will have to unsubscribe all your users from project updates. PYBOSSA has a DB migration
for achiving it. Just run the following command:

```bash
  alembic upgrade head
```

This will ensure that all your users are unsubscribed, and they can now subscribe if they want.
