# Disqus Single Sign-On (SSO)
If the PYBOSSA server is configured with Disqus SSO keys (see [documentation](configuration.md#disqus-single-sign-on-sso)), then you can get the authentication parameters in this endpoint: *api/disqus/sso*.

The endpoint will return a JSON object with two keys: *api\_key* and *remote\_auth\_s3*. Use those values to authenticate the user in Disqus. Check their official [documentation](https://help.disqus.com/customer/portal/articles/236206-integrating-single-sign-on).

