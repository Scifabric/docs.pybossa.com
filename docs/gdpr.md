# GDPR

As you probably know, as of the 25 of May 2018 a new data protection law comes into place in the European Union called 
General Data Protection Regulation (GDPR) impacting how businesses collect and process data
[GDPR law](https://www.eugdpr.org/).

Below we explain how PYBOSSA meets the requested requirements to be fully GDPR compliant.

## Anonymous contributor IPs

PYBOSSA has two types of users:

* Authenticated, and
* Anonymous

PYBOSSA has always used IP addresses to identify ANONYMOUS USERS, however as these don't have an account, 
we can´t know who is the user behind the IP. In order to improve this security, PYBOSSA (v2.9.3) 
encodes the IP address using the technique [Cryptography-based  Prefix-preserving Anonymization](https://www.cc.gatech.edu/computing/Telecomm/projects/cryptopan/) to ensure that all IPs are anonymous.

Therefore when downloading results or a project task run, one won´t get the real user IP as all of them have 
been made anonymous.

We use the following [Python module](https://github.com/keiichishima/yacryptopan) to complete this task.


## Forget me (or delete your account)

PYBOSSA now allows users (without a project) to delete their accounts. This action cannot be undone.

When users delete their accounts, PYBOSSA will:

* Anonymize their task runs. The user_id will be removed, and for each task run PYBOSSA will generates a fake IP address, so that it is not possible to know what is it that users have sent to the server.
* If the server is using Mailchimp integration, PYBOSSA will delete the user from the Mailchimp list sholuld the user subscribed to it.
* Delete all personal data from the server (DB).
* Email to the user and the server administrator so that the user knows everything has been deleted.

!!! NB:
    If the server is using DISQUS SSO, PYBOSSA will note in the removal confirmation email that 
    - as of the 10th of May 2018, DISQUS does not provide an API method to delete the user account. 
    Therefore, PYBOSSA will inform the user that he/she will have to delete their DISQUS account.

## Export your own data

From your personal PYBOSSA account you will be able to export the following data in list of zip files:

* All your personal data
* All your projects created by you
* All your contributions (task runs)

PYBOSSA will create a ZIP file and send an email with links to your email. Those links will only be valid
for 3 days - default configuration, after that they will be removed.

These ZIP files have your data in JSON format, so you can view it with any text editor - standard format.

## See all my data

You can get all your data first, so you can see it with any text editor in any platform. 

### Migrating from a PYBOSSA server version < v2.9.3

If your server is running a version smaller than v2.9.3 you will need to upgrade the 
server to the latest version in order to be GDPR compliant. You then have to anonymize
your stored IPs. PYBOSSA provides a script for doing this task:

``` bash
  python cli.py anonymize_ips
```


!!! note
    We strongly recommend you to do a backup before running the upgrade and the migration of the DB.


Lastly you will have to unsubscribe all your users from project updates. PYBOSSA has a DB migration
for achiving it. Just run the following command:

```bash
  alembic upgrade head
```

This will ensure that all your users are unsubscribed, and they can now subscribe if they want.
