The installation gives you a step by step guide. However, it is your responsibility to secure the server following the standard Linux security guidelines that you should know before going live with your project. 

We would recommend you to follow some of the following links:

* [Linux Security Best Practices](https://devops.profitbricks.com/tutorials/linux-security-best-practices-1/)
*[Rackspace Linux Server Best Practices]( https://support.rackspace.com/how-to/linux-server-security-best-practices/)
* [Linux Security](https://www.cyberciti.biz/tips/linux-security.html)

!!! note
    Some of these links might not work because the owners would change them, or even remove them.

## PYBOSSA server security
Use always an unprivileged user to run PYBOSSA. Also, add secure passwords in all the variables, as this will be key to ensure that your signatures cannot be broken easily. 

## Redis and Sentinel
To secure these services, read the [official documentation](https://redis.io/topics/security).

## PostgreSQL 
To secure the database, read the [official documentation](https://www.postgresql.org/docs/9.5/static/admin.html).

## Data security
PYBOSSA keeps everything private for anonymous users unless you specify in the settings_local.py file fields that you want to disclose.

PYBOSSA can store any information within the **info** field of the following domain objects:

* Announcement.
* Blogpost.
* Category.
* Helpingmaterial,
* Page,
* Project, and
* User.

### Announcement 
PYBOSSA includes the following fields in a GET API call:

* created
* updated
* id
* user_id
* title
* body
* media_url
* published
* info

From info, everything is public for users that are anonymous or are not the owner of the announcement.

### Blogpost
PYBOSSA includes the following fields in a GET API call:

* created
* updated
* project_id
* id
* user_id
* title
* body
* media_url
* published
* info

From info, everything is public for users that are anonymous or are not the owner of the blogpost.

### Category
PYBOSSA includes the following fields in a GET API call:

* description
* short_name
* created 
* id
* name
* info

From info, everything is public for users that are anonymous or are not the owner of the category.

### Helpingmaterial
PYBOSSA includes the following fields in a GET API call:

* created
* id
* info
* media_url
* priority

From info, everything is public for users that are anonymous or are not the owner of the helpingmaterial.

### Page
PYBOSSA includes the following fields in a GET API call:

* created
* id
* info
* media_url
* slug

From info, everything is public for users that are anonymous or are not the owner of the page.


### Project
PYBOSSA includes the following fields in a GET API call:

* id
* description
* info
* n_tasks
* n_volunteers
* name
* overall_progress
* short_name
* created
* category_id
* long_description
* last_activity
* last_activity_raw
* n_task_runs
* n_results
* owner
* updated
* featured
* owner_id
* n_completed_tasks
* n_blogposts
* owners_ids

From info, only the following items are public:
* container
* thumbnail
* thumbnail_url
* task_presenter
* tutorial
* sched

Any other key will be private except for the owner or an admin. If you want to add more keys, just use the following flag in the settings_local.py file:

```python
PROJECT_INFO_PUBLIC_FIELDS = ['key1', 'key2', .., 'keyN']
```

### User
PYBOSSA includes the following fields in a GET API call:

* created
* name
* fullname
* info
* n_answers
* registered_ago
* rank
* score
* locale

From info, only the following items are public:

* avatar
* container
* extra
* avatar_url

Any other key will be private except for the owner or an admin. If you want to add more keys, just use the following flag in the settings_local.py file:

```python
USER_INFO_PUBLIC_FIELDS = ['key1', 'key2', .., 'keyN']
```
