# GDPR

As of the 25 of May 2018, every European project has to be GDPR compliant [GDPR law](https://www.eugdpr.org/).

Below we explain how PYBOSSA meets the requested requirements to be GDPR compliant.

## Anonymous contributor IPs

PYBOSSA has two types of users:

* Authenticated, and
* Anonymous

For Anonymous Users, PYBOSSA has used always their IP address to identify them, however as they don't have an
account, we can´t know who is the user behind that IP. In order to improve this security, PYBOSSA (v2.9.5) 
encodes the IP address using the technique [Cryptography-based  Prefix-preserving Anonymization](https://www.cc.gatech.edu/computing/Telecomm/projects/cryptopan/) to
ensure that all IPs are anonymous.

Therefore when downloading results or a project task run, you won´t get the real user IP as all of them have 
been made anonymous.

We use the following [Python module](https://github.com/keiichishima/yacryptopan) to perform this task.


## Forget me (or delete your account)

PYBOSSA now allows any user (without a project) to delete his/her own account. This action cannot be undone.

When users deletes their account, PYBOSSA will:

* Anonymize their task runs. The user_id will be removed, and for each task run PYBOSSA will generates a fake IP address, so that it is not possible to know what users have sent to the server.
* If the server is using Mailchimp integration, PYBOSSA will delete the user from the Mailchimp list sholuld the user subscribed to it.
* Delete all personal data from the server (DB).
* Email to the user and the server administrator so that the user knows everything has been deleted.

!!! note:
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


## Restrict processing

If you don't want to delete your account, but you want to restrict processing you can do that from your
user's profile page. Just go to your settings, hit the update link and there check the *restrict processing* checkbox.

This will ensure that no one access your data, not even the admins. By checking that box, you will be completely removed
from the user API (only you can access your account under your ID), your User is not going to be part of the api USER filtering,
you are not included in any leaderboard (including top 5 users for projects, and active users in the last 24 hours).

### Migrating from a PYBOSSA server version < v2.9.5

If your server is running a version smaller than v2.9.5 you will need to upgrade the 
server to the latest version in order to be GDPR compliant. You then have to anonymize
your stored IPs. PYBOSSA provides a script for doing this task:

``` bash
  python cli.py anonymize_ips
```

If you have custom leaderboards, then, you will have to drop those materialized views by hand. Why?
Because we're adding a new column to them. If you only use the default leaderboard, everything should
work as expected. To delete your materialized views for your leaderboards, just run this command within
the DB:

``` sql
  drop materialized view users_rank_{your_name};
```

Replace the {} text with your names, and you will be fine. This will not delete any data, as the materialized
views will be recreated by the jobs in the next tick. If you need them recreated now, just open a terminal and
run the following command:

```python
from run import create_app
from pybossa.leadeboard.jobs import leaderboard

app = create_app(False)

with app.app_context():
   leaderboard(info='your_name')
   leaderboard(info='your_second')
   ...
   leaderboard(info='your_n')
```

That will recreate the views for you, and you will be ready to use them.

!!! note
    We strongly recommend you to do a backup before running the upgrade and the migration of the DB.


Lastly you will have to unsubscribe all your users from project updates. PYBOSSA has a DB migration
for achiving it. Just run the following command:

```bash
  alembic upgrade head
```

This will ensure that all your users are unsubscribed, and they can now subscribe if they want.
