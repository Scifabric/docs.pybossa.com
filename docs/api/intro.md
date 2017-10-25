RESTful API
===========

The RESTful API is located at:

    http://{pybossa-site-url}/api

It expects and returns JSON.

Some requests will need an **API-KEY** to authenticate & authorize the
operation. You can get your API-KEY in your *profile* account.

The returned objects will have a **links** and **link** fields, not
included in the model in order to support [Hypermedia as the Engine of
Application State](http://en.wikipedia.org/wiki/HATEOAS) (also known as
HATEOAS), so you can know which are the relations between objects.

All objects will return a field **link** which will be the absolute URL
for that specific object within the API. If the object has some parents,
you will find the relations in the **links** list. For example, for a
Task Run you will get something like this:

```json
{
"info": 65,
"user_id": null,
"links": [
    "<link rel='parent' title='project' href='http://localhost:5000/api/project/90'/>",
    "<link rel='parent' title='task' href='http://localhost:5000/api/task/5894'/>"
],
"task_id": 5894,
"created": "2012-07-07T17:23:45.714184",
"finish_time": "2012-07-07T17:23:45.714210",
"calibration": null,
"project_id": 90,
"user_ip": "X.X.X.X",
"link": "<link rel='self' title='taskrun' href='http://localhost:5000/api/taskrun/8969'/>",
"timeout": null,
"id": 8969
}
```

The object link will have a tag **rel** equal to **self**, while the
parent objects will be tagged with **parent**. The **title** field is
used to specify the type of the object: task, taskrun or project.

Projects will not have a **links** field, because these objects do not
have parents.

Tasks will have only one parent: the associated project.

Task Runs will have only two parents: the associated task and associated
project.

Rate Limiting
-------------

Rate Limiting has been enabled for all the API endpoints (since PYBOSSA
v2.0.1). The rate limiting gives any user, using the IP, **a window of
15 minutes to do at most 300 requests per endpoint**.

This new feature includes in the headers the following values to
throttle your requests without problems:

-   **X-RateLimit-Limit**: the rate limit ceiling for that given request
-   **X-RateLimit-Remaining**: the number of requests left for the 15
    minute window
-   **X-RateLimit-Reset**: the remaining window before the rate limit
    resets in UTC epoch seconds

We recommend to use the Python package **requests** for interacting with
PYBOSSA, as it is really simple to check those values:

```python
import requests
import time

res = requests.get('http://SERVER/api/project')
if int(res.headers['X-RateLimit-Remaining']) < 10:
    time.sleep(300) # Sleep for 5 minutes
else:
    pass # Do your stuff
```

List
----

List domain objects:

    GET http://{pybossa-site-url}/api/{domain-object}

The API is context aware in the sense that if you've an API-KEY and
you're authenticating the calls, then, the server will send you first
your own related data: projects, tasks, and task runs. You can get
access to all the projects, tasks, and task runs (the whole data base)
using the parameter: **all=1**.

For example, if an anonymous user access the generic api endpoints like:

    GET http://{pybossa-site-url}/api/project

It will return all the projects from the DB, ordering them by ID. If you
access it like authenticating yourself:

    GET http://{pybossa-site-url}/api/project?api_key=YOURKEY

Then, you will get your own list of projects. In other words, the
projects that you own. If you don't have a project, but you want to
explore the API then you can use the **all=1** argument:

    GET http://{pybossa-site-url}/api/project?api_key=YOURKEY&all=1

This call will return all the projects from the DB ordering by ID.

For example, you can get a list of your Projects like this:

    GET http://{pybossa-site-url}/api/project
    GET http://{pybossa-site-url}/api/project?api_key=YOURKEY
    GET http://{pybossa-site-url}/api/project?api_key=YOURKEY&all=1

Or a list of available Categories:

    GET http://{pybossa-site-url}/api/category

Or a list of Tasks:

    GET http://{pybossa-site-url}/api/task
    GET http://{pybossa-site-url}/api/task?api_key=YOURKEY
    GET http://{pybossa-site-url}/api/task?api_key=YOURKEY&all=1

For a list of TaskRuns use:

    GET http://{pybossa-site-url}/api/taskrun
    GET http://{pybossa-site-url}/api/taskrun?api_key=YOURKEY
    GET http://{pybossa-site-url}/api/taskrun?api_key=YOURKEY&all=1

Finally, you can get a list of users by doing:

    GET http://{pybossa-site-url}/api/user

List of project IDs
------------------------------

In PYBOSSA most of the domain objects are related to a project.
Therefore, you can query (or filter) a list of project IDs directly via
the API to reduce the number of queries that you need to do. This is
specially useful for Single Page Applications that only use the PYBOSSA
JSON endpoints.

For example, you can get all the tasks for a list of projects like this:

    GET http://{pybossa-site-url}/api/task?project_id=[1,2,3]

That filter will return tasks for project IDs 1, 2 and 3. The same can
be done for task runs and blogposts.

Created
-------

If you want, you can use the the domain attribute *created* to get items
from the DB. Basically, you can specify a year, year-month,
year-month-day to get all the values for those ranges. For example, if
you want all the tasks that have been created in 2015, just use:

    GET http://{pybossa-site-url}/api/task?created=2015&all=1

If you want all the task runs from 2015-05:

    GET http://{pybossa-site-url}/api/taskrun?created=2015-05&all=1

You can for example get all the task runs that a user has submitted on a
given day like this:

    GET http://{pybossa-site-url}/api/taskrun?created=2015-05-03&user_id=3

This filter works for any object that has the *created* attribute.

Order by
--------

Any query can be ordered by an attribute of the domain object that you
are querying. For example you can get a list of tasks ordered by ID:

    GET http://{pybossa-site-url}/api/task?orderby=id

If you want, you can order them in descending order:

    GET http://{pybossa-site-url}/api/task?orderby=id&desc=true

Check all the attributes that you can use to order by in the [Domain
Object section](http://docs.pybossa.com/en/latest/model.html).

!!! note
    Please, notice that in order to keep users privacy, only their locale and
    nickname will be shared by default. Optionally, users can disable
    privacy mode in their settings. By doing so, also their fullname and
    account creation date will be visible for everyone through the API.

!!! note
    By default PYBOSSA limits the list of items to 20. If you want to get more
    items, use the keyword **limit=N** with **N** being a number to get
    that amount. There is a maximum of 100 to the **limit** keyword, so
    if you try to get more items at once it won't work.

!!! note
    **DEPRECATED (see next Note for a better and faster solution)**
    You can use the keyword **offset=N** in any **GET** query to skip
    that many rows before beginning to get rows. If both **offset** and
    **limit** appear, then **offset** rows are skipped before starting
    to count the **limit** rows that are returned.


!!! note
    You can paginate the results of any GET query using the last ID of the
    domain object that you have received and the parameter:
    **last\_id**. For example, to get the next 20 items after the last
    project ID that you've received you will write the query like this:
    `GET /api/project?last\_id={{last\_id}}`.

### Related data

For Tasks, TaskRuns and Results you can get the associated data using
the argument: *related=True*.

This flag will allow you to get in one call all the TaskRuns and Result
for a given task. You can do the same for a TaskRun getting the Task and
associated Result, and for a Result getting all the task\_runs and
associated Task.

Projects do not have this feature, as it will be too expensive for the
API.

Get
---

Get a specific domain object by id (by default any GET action will
return only 20 objects, you can get more or less objects using the
**limit** option). Returns domain object.:

    GET http://{pybossa-site-url}/api/{domain-object}/{id}[?api_key=API-KEY]

!!! note
    Some GET actions may require to authenticate & authorize the request. Use the
    `?api\_key` argument to pass the **API-KEY**.

If the object is not found you will get a JSON object like this:

```json
{
    "status": "failed",
    "action": "GET",
    "target": "project",
    "exception_msg": "404 Not Found",
    "status_code": 404,
    "exception_cls": "NotFound"
}
```

Any other error will return the same object but with the proper status
code and error message.

Search
------

Get a list of domain objects by its fields. Returns a list of domain
objects matching the query:

    GET http://{pybossa-site-url}/api/{domain-object}[?domain-object-field=value]

Multiple fields can be used separated by the **&** symbol:

    GET http://{pybossa-site-url}/api/{domain-object}[?field1=value&field2=value2]

It is possible to limit the number of returned objects:

    GET http://{pybossa-site-url}/api/{domain-object}[?field1=value&limit=20]

It is possible to access first level JSON keys within the **info** field
of Categories, Projects, Tasks, Task Runs and Results:

    GET http://{pybossa-site-url}/api/{domain-object}[?field1=value&info=foo::bar&limit=20]

To search within the first level (nested keys are not supported), you
have to use the following format:

    info=key::value

For adding more keys:

    info=key1::value1|key2::value2|keyN::valueN

These parameters will be ANDs, so, it will return objects that have
those keys with and **and** operator.

Requesting the user's oAuth tokens
----------------------------------

A user who has registered or signed in with any of the third parties
supported by PYBOSSA (currently Twitter, Facebook and Google) can
request his own oAuth tokens by doing:

    GET http://{pybossa-site-url}/api/token?api_key=API-KEY

Additionally, the user can specify any of the tokens if only its
retrieval is desired:

    GET http://{pybossa-site-url}/api/token/{provider}?api_key=API-KEY

Where 'provider' will be any of the third parties supported, i.e.
'twitter', 'facebook' or 'google'.


Using your own user database
----------------------------

Since version v2.3.0 PYBOSSA supports external User IDs. This means that
you can easily use your own database of users without having to
registering them in the PYBOSSA server. As a benefit, you will be able
to track your own users within the PYBOSSA server providing a very
simple and easy experience for them.

A typical case for this would be for example a native phone app
(Android, iOS or Windows).

Usually phone apps have their own user base. With this in mind, you can
add a crowdsourcing feature to your phone app by just using PYBOSSA in
the following way.

First, create a project. When you create a project in PYBOSSA the system
will create for you a *secret key*. This secret key will be used by your
phone app to authenticate all the requests and avoid other users to send
data to your project via external user API.

!!! note
    We highly recommend using SSL on your server to secure all the process.
    You can use Let's Encrypt certificates for free. Check their
    [documentation.](https://certbot.eff.org/)

Now your phone app will have to authenticate to the server to get tasks
and post task runs.

To do it, all you have to do is to create an HTTP Request with an
Authorization Header like this:

    HEADERS Authorization: project.secret_key
    GET http://{pybossa-site-url}/api/auth/project/short_name/token

That request will return a JWT token for you. With that token, you will
be able to start requesting tasks for your user base passing again an
authorization header. Imagine a user from your database is identified
like this: '1xa':

    HEADERS Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
    GET http://{pybossa-site-url}/api/{project.id}/newtask?external_uid=1xa

That will return a task for the user ID 1xa that belongs to your
database but not to PYBOSSA. Then, once the user has completed the task
you will be able to submit it like this:

    HEADERS Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
    POST http://{pybossa-site-url}/api/taskrun?external_uid=1xa

!!! note
    The TaskRun object needs to have the external\_uid field filled with
    1xa.

As simple as that!


Command line Example Usage of the API
-------------------------------------

Create a Project object:

```bash
curl -X POST -H "Content-Type:application/json" -s -d '{"name":"myproject", "info":{"xyz":1}}' 'http://localhost:5000/api/project?api_key=API-KEY'
```

PYBOSSA endpoints
-----------------

The following endpoints of PYBOSSA server can be requested setting the
header *Content-Type* to *application/json* so you can retrieve the data
using JavaScript.

!!! note
    If a key has the value **null** is because, that view is not populating
    that specific field. However, that value should be retrieved in a
    different one. Please, see all the documentation.
