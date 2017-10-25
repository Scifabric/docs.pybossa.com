Create
------

Create a domain object. Returns created domain object.:

    POST http://{pybossa-site-url}/api/{domain-object}[?api_key=API-KEY]

!!! note
    Some POST actions may require to authenticate & authorize the request. Use the
    `?api\_key` argument to pass the **API-KEY**.

If an error occurs, the action will return a JSON object like this:

```json
{
    "status": "failed",
    "action": "POST",
    "target": "project",
    "exception_msg": "type object 'Project' has no attribute 'short_ame'",
    "status_code": 415,
    "exception_cls": "AttributeError"
}
```

Where **target** will refer to a Project, Task or TaskRun object.

Update
------

Update a domain object:

    PUT http://{pybossa-site-url}/api/{domain-object}/{id}[?api_key=API-KEY]

!!! note
    Some PUT actions may require to authenticate & authorize the request. Use the
    ?api\_key argument to pass the **API-KEY**.

If an error occurs, the action will return a JSON object like this:

```json
{
    "status": "failed",
    "action": "PUT",
    "target": "project",
    "exception_msg": "type object 'Project' has no attribute 'short_ame'",
    "status_code": 415,
    "exception_cls": "AttributeError"
}
```

Where **target** will refer to a project, Task or TaskRun object.

Delete
------

Delete a domain object:

    DELETE http://{pybossa-site-url}/api/{domain-object}/{id}[?api_key=API-KEY]

!!! note
    Some DELETE actions may require to authenticate & authorize the request. Use the
    `?api\_key` argument to pass the **API-KEY**.

If an error occurs, the action will return a JSON object like this:

```json
{
    "status": "failed",
    "action": "DELETE",
    "target": "project",
    "exception_msg": "type object 'Project' has no attribute 'short_ame'",
    "status_code": 415,
    "exception_cls": "AttributeError"
}
```

Where **target** will refer to a Project, Task or TaskRun object.


