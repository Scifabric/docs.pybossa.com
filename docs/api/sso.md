Disqus Single Sign On (SSO)
---------------------------

If the PYBOSSA server is configured with Disqus SSO keys (see disqus),
then you can get the authentication parameters in this endpoint:
*api/disqus/sso*

The endpoint will return a JSON object with two keys: *api\_key* and
*remote\_auth\_s3*. Use those values to authenticate the user in Disqus.
Check their official [documentation]().

