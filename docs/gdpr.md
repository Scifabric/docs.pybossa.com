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

### Migrating from a PYBOSSA server version < v2.9.3

If you server is running a version smaller than v2.9.3 then, you will need to upgrade
the server to the latest version to be GDPR compliant. Then, you will need to anonymize
your stored IPs. PYBOSSA provides a script for doing this task:

``` bash
  python cli.py anonymize_ips
```


!!! note
    We highly recommend to do a backup before running the upgrade and the migration of the DB.
