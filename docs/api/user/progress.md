# User progress

You can know how many tasks a user has completed for a given project by accessing
the following endpoint:

```
http://server.com/api/project/<id>/userprogress
```

or

```
http://server.com/api/project/<short_name>/userprogress
```


The user needs to be authenticated to get the value. You cannot query another user, just
the current one that it is authenticated in the system.
