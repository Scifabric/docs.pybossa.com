You can list project statistics, such as number of tasks, volunteers and overall progress via:

    GET /api/projectstats

To filter this list, for example, by project ID:

    GET /api/projectstats?project_id=[1,2,3]

To include additional hour stats, day stats and user stats for the past 2 weeks, append **full=1** to the query, for example:

    GET /api/projectstats?full=1

These additional statistics will be included in the **info** field of each object returned.

!!! tip "Tip"

    These statistics can also be retrieved by adding the argument `stats=True`
    to requests made to the `/api/project` endpoint. In this case they will be
    added against a `stats` key returned with each Project.

## User progress

You can know how many tasks a user has completed for a given project by accessing
the following endpoint:

```
http://server.com/api/project/<id>/userprogress
```

or

```
http://server.com/api/project/<short_name>/userprogress
```

The user needs to be authenticated to get the value, otherwise it will use the anonymous IP to get the value.

If you are using **external_uid** for sending task runs, you can get the progress using the following parameter:



```
http://server.com/api/project/<id>/userprogress?external_uid=EXTERNAL_UID
```
