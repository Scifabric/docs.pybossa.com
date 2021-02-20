## Project creation

**Endpoint: /project/new**

*Allowed methods*: **GET/POST**

**GET**

Gives you the list of required fields in the form to create a project.

-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.
-   **form**: The form fields that need to be sent for creating the
    project. It contains the CSRF token for validating the POST, as well
    as an errors field in case that something is wrong.

**Example output**

```json
{
  "errors": false,
  "form": {
    "csrf": "token",
    "description": null,
    "errors": {},
    "long_description": null,
    "name": null,
    "short_name": null
  },
  "template": "projects/new.html",
  "title": "Create a Project"
}
```

## Project blog list

**Endpoint: /project/&lt;short\_name&gt;/blog**

*Allowed methods*: **GET**

**GET**

Gives you the list of posted blogs by the given project short name.

-   **blogposts**: All the blog posts for the given project.
-   **project**: Info about the project.

The project and owner fields will have more information if the owner of
the project does the request, providing its private information like
api\_key, password keys, etc. Otherwise, it will be removed and only show
public info.

**Example public output**

```json
{
  "blogposts": [
    {
      "body": "Please, e-mail us to alejasan 4t ucm dot es if you find any bug. Thanks.",
      "created": "2014-05-14T14:25:04.899079",
      "id": 1,
      "project_id": 1377,
      "title": "We are working on the Alpha version.",
      "user_id": 3927
    },
  ],
  "n_completed_tasks": 137051,
  "n_task_runs": 1070561,
  "n_tasks": 169671,
  "n_volunteers": 17499,
  "overall_progress": 80,
  "owner": {
    "created": "2014-02-13T15:28:08.420187",
    "fullname": "John Doe",
    "info": {
      "avatar": "avatar.png",
      "container": "container"
    },
    "n_answers": 32814,
    "name": "johndoe",
    "rank": 4,
    "registered_ago": "3 years ago",
    "score": 32814
  },
  "pro_features": {
    "auditlog_enabled": false,
    "autoimporter_enabled": false,
    "webhooks_enabled": false
  },
  "project": {
    "created": "2014-02-22T15:09:23.691811",
    "description": "Image pattern recognition",
    "featured": true,
    "id": 1,
    "info": {
      "container": "container",
      "thumbnail": "58.png"
    },
    "last_activity": null,
    "last_activity_raw": null,
    "n_tasks": null,
    "n_volunteers": null,
    "name": "Dark Skies ISS",
    "overall_progress": null,
    "owner": null,
    "short_name": "darkskies",
    "updated": "2017-01-31T09:18:28.491496"
  },
  "template": "projects/blog.html"
}
```

## Project task presenter editor

**Endpoint: /project/&lt;short\_name&gt;/tasks/taskpresentereditor**

*Allowed methods*: **GET/POST**

**GET**

This endpoint allows you to get the list of available templates for the
current project. This will only happen when the project has an empty template, otherwise, it will load the template for you.

-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.
-   **presenters**: List of available templates (in HTML format). The
    name of them without the '.html' will be the argument for the endpoint.
-   **last\_activit**: last activity of the project.
-   **n\_task\_runs**: number of task runs.
-   **n\_tasks**: number of tasks.
-   **n\_volunteers**: number of volunteers.
-   **owner**: information about the owner.
-   **pro\_features**: which pro features are enabled.
-   **pro\_features**: which pro features are enabled.
-   **project**: info about the project.
-   **status**: status of the flash message.
-   **flash**: flash message.

**Example output**

```json
{
 "flash": "<strong>Note</strong> You will need to upload the tasks using the<a href=\"/project/asdf123/tasks/import\"> CSV importer</a> or download the project bundle and run the <strong>createTasks.py</strong> script in your computer",
 "last_activity": null,
 "n_completed_tasks": 0,
 "n_task_runs": 0,
 "n_tasks": 0,
 "n_volunteers": 0,
 "overall_progress": 0,
 "owner": {
   "admin": false,
   "api_key": "key",
   "confirmation_email_sent": false,
   "created": "2016-09-15T11:30:42.660450",
   "email_addr": "prueba@prueba.com",
   "fullname": "prueba de json",
   "id": 12030,
   "info": {
     "avatar": "avatar.png",
     "container": "user"
   },
   "n_answers": 5,
   "name": "pruebaadfadfa",
   "rank": 4411,
   "registered_ago": "6 months ago",
   "score": 5,
   "total": 11134,
   "valid_email": true
 },
 "presenters": [
   "projects/presenters/basic.html",
   "projects/presenters/image.html",
   "projects/presenters/sound.html",
   "projects/presenters/video.html",
   "projects/presenters/map.html",
   "projects/presenters/pdf.html"
 ],
 "pro_features": {
   "auditlog_enabled": false,
   "autoimporter_enabled": false,
   "webhooks_enabled": false
 },
 "project": {
   "allow_anonymous_contributors": true,
   "category_id": 4,
   "contacted": false,
   "contrib_button": "draft",
   "created": "2017-01-11T09:37:43.613007",
   "description": "adsf",
   "featured": false,
   "id": 3,
   "info": {
     "passwd_hash": null,
     "task_presenter": ""
   },
   "long_description": "adsf",
   "n_blogposts": 0,
   "n_results": 0,
   "name": "asdf1324",
   "owner_id": 12030,
   "published": false,
   "secret_key": "73aee9df-be47-4e4c-8192-3a8bf0ab5161",
   "short_name": "asdf123",
   "updated": "2017-03-15T13:20:48.022328",
   "webhook": ""
 },
 "status": "info",
 "template": "projects/task_presenter_options.html",
 "title": "Project: asdf1324 &middot; Task Presenter Editor"
```

> }

If you want to preload the template from one of the available prenters, you have to pass the following argument: **?template=basic** for the basic or **?template=iamge** for the image template.

**Example output**

```json
{
 "errors": false,
 "flash": "Your code will be <em>automagically</em> rendered in                       the <strong>preview section</strong>. Click in the                       preview button!",
 "form": {
   "csrf": "token",
   "editor": "<div class=\"row\">\n    <div class=\"col-md-12\">\n        <h1>Write here your HTML Task Presenter</h1>\n    </div>\n</div>\n<script type=\"text/javascript\">\n(function() {\n    // Your JavaScript code\n    pybossa.taskLoaded(function(task, deferred){\n        // When the task is loaded, do....\n    });\n\n    pybossa.presentTask(function(task, deferred){\n        // Present the current task to the user\n        // Load the task data into the HTML DOM\n    });\n\n    pybossa.run('asdf123');\n})();\n</script>",
   "errors": {},
   "id": 3
 },
 "last_activity": null,
 "n_completed_tasks": 0,
 "n_task_runs": 0,
 "n_tasks": 0,
 "n_volunteers": 0,
 "overall_progress": 0,
 "owner": {
   "admin": false,
   "api_key": "key",
   "confirmation_email_sent": false,
   "created": "2016-09-15T11:30:42.660450",
   "email_addr": "prueba@prueba.com",
   "fullname": "prueba de json",
   "id": 0,
   "info": {
     "avatar": "avatar.png",
     "container": "user"
   },
   "n_answers": 5,
   "name": "pruebaadfadfa",
   "rank": 4411,
   "registered_ago": "6 months ago",
   "score": 5,
   "total": 11134,
   "valid_email": true
 },
 "pro_features": {
   "auditlog_enabled": false,
   "autoimporter_enabled": false,
   "webhooks_enabled": false
 },
 "project": {
   "allow_anonymous_contributors": true,
   "category_id": 4,
   "contacted": false,
   "contrib_button": "draft",
   "created": "2017-01-11T09:37:43.613007",
   "description": "adsf",
   "featured": false,
   "id": 3,
   "info": {
     "passwd_hash": null,
     "task_presenter": ""
   },
   "long_description": "adsf",
   "n_blogposts": 0,
   "n_results": 0,
   "name": "asdf1324",
   "owner_id": 0,
   "published": false,
   "secret_key": "73aee9df-be47-4e4c-8192-3a8bf0ab5161",
   "short_name": "asdf123",
   "updated": "2017-03-15T13:20:48.022328",
   "webhook": ""
 },
 "status": "info",
 "template": "projects/task_presenter_editor.html",
 "title": "Project: asdf1324 &middot; Task Presenter Editor"
```

> }

Then, you can use that template, or if you prefer you can do a POST
directly without that information. As in any other request involving a POST you will need the CSRFToken to validate it.

**POST**

To send a valid POST request, you need to pass the *csrf token* in the headers. Use the following header: "X-CSRFToken". You will have to POST the data fields found in the previous example, as it contains the information about the fields: specifically **editor** with the
HTML/CSS/JS that you want to provide.

If the post is successful, you will get the following output:

**Example output**

```json
{
  "flash": "<i class=\"icon-ok\"></i> Task presenter added!",
  "next": "/project/asdf123/tasks/",
  "status": "success"
}
```

## Project delete

**Endpoint: /project/&lt;short\_name&gt;/delete**

*Allowed methods*: **GET/POST**

**GET**

The GET endpoint allows you to get all the info about the project (see
the Project endpoint as well) as well as the csrf token. As this
endpoint does not have any form, the csrf token is not inside the form
field.

**Example output**

```json
{
  "csrf": "token",
  "last_activity": null,
  "n_tasks": 0,
  "overall_progress": 0,
  "owner": {
    "admin": false,
    "api_key": "key",
    "confirmation_email_sent": false,
    "created": "2016-09-15T11:30:42.660450",
    "email_addr": "prueba@prueba.com",
    "fullname": "prueba de json",
    "id": 0,
    "info": {
      "avatar": "avatar.png",
      "container": "0"
    },
    "n_answers": 5,
    "name": "pruebaadfadfa",
    "rank": 4411,
    "registered_ago": "6 months ago",
    "score": 5,
    "total": 11134,
    "valid_email": true
  },
  "pro_features": {
    "auditlog_enabled": false,
    "autoimporter_enabled": false,
    "webhooks_enabled": false
  },
  "project": {
    "allow_anonymous_contributors": true,
    "category_id": 2,
    "contacted": false,
    "created": "2017-03-15T15:02:12.160810",
    "description": "asdf",
    "featured": false,
    "id": 3,
    "info": {},
    "long_description": "asdf",
    "name": "algo",
    "owner_id": 12030,
    "published": false,
    "secret_key": "c5a77943-f5a4-484a-86bb-d69559e80357",
    "short_name": "algo",
    "updated": "2017-03-15T15:02:12.160823",
    "webhook": null
  },
  "template": "/projects/delete.html",
  "title": "Project: algo &middot; Delete"
}
```

**POST**

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken".

**Example output**

```json
{
  "flash": "Project deleted!",
  "next": "/account/pruebaadfadfa/",
  "status": "success"
}
```

## Project update

**Endpoint: /project/&lt;short\_name&gt;/update**

*Allowed methods*: **GET/POST**

**GET**

It returns a JSON object with the following information:

-   **form**: the form fields that need to be sent for updating the
    project. It contains the csrf token for validating the post, as well as an errors field in case that something is wrong.
-   **upload\_form**: the form fields that need to be sent for updating
    the project's avatar. It contains the csrf token for validating the
    post, as well as an errors field in case that something is wrong.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: The title for the view.

**Example output**

```json
{
  "form": {
    "allow_anonymous_contributors": false,
    "category_id": 2,
    "csrf": "token",
    "description": "description",
    "errors": {},
    "id": 3117,
    "long_description": "long description",
    "name": "name",
    "password": null,
    "protect": false,
    "short_name": "slug",
    "webhook": null
  },
  "last_activity": null,
  "n_completed_tasks": 0,
  "n_task_runs": 0,
  "n_tasks": 2,
  "n_volunteers": 0,
  "overall_progress": 0,
  "owner": {
    "admin": false,
    "api_key": "key",
    "confirmation_email_sent": false,
    "created": "2012-06-06T06:27:18.760254",
    "email_addr": "email.com",
    "fullname": "John Doe",
    "id": 0,
    "info": {
      "avatar": "avatar.png",
      "container": "user",
    },
    "n_answers": 2414,
    "name": "johndoe",
    "rank": 69,
    "registered_ago": "4 years ago",
    "score": 2414,
    "total": 11134,
    "valid_email": false
  },
  "pro_features": {
    "auditlog_enabled": true,
    "autoimporter_enabled": true,
    "webhooks_enabled": true
  },
  "project": {
    "allow_anonymous_contributors": false,
    "category_id": 2,
    "contacted": false,
    "contrib_button": "can_contribute",
    "created": "2015-06-29T08:23:14.201331",
    "description": "description",
    "featured": false,
    "id": 0,
    "info": {
      "container": "user",
      "passwd_hash": null,
      "task_presenter": "HTML+CSS+JS,
      "thumbnail": "thumbnail.png"
    },
    "long_description": "long description",
    "n_blogposts": 0,
    "n_results": 0,
    "name": "name",
    "owner_id": 0,
    "published": true,
    "secret_key": "key",
    "short_name": "slug",
    "updated": "2017-03-16T14:50:45.055331",
    "webhook": null
  },
  "template": "/projects/update.html",
  "title": "Project: name &middot; Update",
  "upload_form": {
    "avatar": null,
    "csrf": "token",
    "errors": {},
    "id": null,
    "x1": 0,
    "x2": 0,
    "y1": 0,
    "y2": 0
  }
}
```

**POST**

To send a valid POST request, you need to pass the *csrf token* in the headers. Use the following header: "X-CSRFToken."

As this endpoint supports **two** different forms, you must specify
which form are you targeting adding an extra key: **btn**. The options
for this key are:

> **Upload**: to update the **upload\_form**.

The other one does not need this extra key.

!!! note
    Be sure to respect the Uppercase in the first letter. Otherwise, it will fail.

It returns a JSON object with the following information:

-   **flash**: A success message, or error indicating if the request was
    successful.
-   **form**: the form fields with the sent information. It contains the
    csrf token for validating the post, as well as an errors field in    the case that something is wrong.

**Example output**

```json
{
  "flash": "Your profile has been updated!",
  "next": "/account/pruebaadfadfa/update",
  "status": "success"
}
```

If there's an error in the form fields, you will get them in the
**form.errors** key:

```json
{
  "flash": "Please correct the errors",
  "form": {
    "allow_anonymous_contributors": false,
    "category_id": 2,
    "csrf": "token",
    "description": "description",
    "errors": {
      "short_name": [
        "This field is required."
      ]
    },
    "id": 3117,
    "long_description": "new description",
    "name": "new name",
    "password": null,
    "protect": true,
    "short_name": "",
    "webhook": null
  },
  ...
}
```

!!! note
    For updating the avatar is very important to not set the *Content-Type*. If
    you  are using jQuery, set it to False, so the file is handled properly.
    To still recieve a JSON response you can add the response_format=json query
    paramater to your request.

    The (x1,x2,y1,y2) are the coordinates for cutting the image and create
    the avatar.

    (x1,y1) are the offset left of the cropped area and the offset top of the cropped area respectively; and (x2,y2) are the width and height of the crop. And don't forget to add an extra key to the form-data: 'btn' with a value Upload to select this form.

## Project reset secret key

**Endpoint: /project/&lt;short\_name&gt;/resetsecretkey**

*Allowed methods*: **POST**

Resets the secret key of a project.

To send a valid POST request, you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken" retrieved from the GET
endpoint **/project/&lt;short\_name&gt;/update**.

**Example output**

```json
{
  "flash": "New secret key generated",
  "next": "/project/flickrproject2/update",
  "status": "success"
}
```

## Project tasks browse

**Endpoint: /project/&lt;short\_name&gt;/tasks/browse/** **Endpoint:
/project/&lt;short\_name&gt;/tasks/browse/&lt;int:page&gt;**

*Allowed methods*: **GET**

-   **n\_completed\_tasks**: number of completed tasks
-   **n\_tasks**: number of tasks
-   **n\_volunteers**: number of volunteers
-   **overall\_progress**: overall progress
-   **owner**: project owner
-   **pagination**: pagination information
-   **pro\_features**: pro features enabled or not
-   **project**: project information
-   **tasks**: tasks, paginated
-   **template**: the Jinja2 template that should be rendered in case of
    text/html.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "n_completed_tasks": 0,
  "n_tasks": 1,
  "n_volunteers": 0,
  "overall_progress": 0,
  "owner": {
    "created": "2017-04-17T23:56:22.892222",
    "fullname": "John Doe",
    "info": {},
    "locale": null,
    "n_answers": 0,
    "name": "johndoe",
    "rank": null,
    "registered_ago": "3 hours ago",
    "score": null
  },
  "pagination": {
    "next": false,
    "page": 1,
    "per_page": 10,
    "prev": false,
    "total": 1
  },
  "pro_features": {
    "auditlog_enabled": false,
    "autoimporter_enabled": false,
    "webhooks_enabled": false
  },
  "project": {
    "created": "2017-04-17T23:56:23.416754",
    "description": "Description",
    "featured": false,
    "id": 1,
    "info": {},
    "last_activity": null,
    "last_activity_raw": null,
    "n_tasks": null,
    "n_volunteers": null,
    "name": "Sample Project",
    "overall_progress": null,
    "owner": null,
    "short_name": "sampleapp",
    "updated": "2017-04-17T23:56:23.589652"
  },
  "tasks": [
    {
      "id": 1,
      "n_answers": 10,
      "n_task_runs": 0,
      "pct_status": 0.0
    }
  ],
  "template": "/projects/tasks_browse.html",
  "title": "Project: Sample Project &middot; Tasks"
}
```

## Project tasks import

**Endpoint: /project/&lt;short\_name&gt;/tasks/import**

*Allowed methods*: **GET/POST**

**GET**

It returns a JSON object with the following information:

-   **available\_importers**: A list of available importers for the
    server. To use one of the items, you have to add to the endpoint the
    following argument: *?type=name* where the name is the string that you will find in the list of importers in the format:
    *projects/tasks/name.html*.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: The title for the view.

**Example output**

```json
{
  "available_importers": [
    "projects/tasks/epicollect.html",
    "projects/tasks/csv.html",
    "projects/tasks/s3.html",
    "projects/tasks/youtube.html",
    "projects/tasks/gdocs.html",
    "projects/tasks/dropbox.html",
    "projects/tasks/iiif.html"
  ],
  "form": null,
  "loading_text": "Importing tasks, this may take a while, wait...",
  "n_completed_tasks": 0,
  "n_tasks": 5,
  "n_volunteers": 0,
  "overall_progress": 0,
  "owner": {
    "admin": false,
    "api_key": "key",
    "confirmation_email_sent": false,
    "created": "2012-06-06T06:27:18.760254",
    "email_addr": "johndoe@gmail.com",
    "fullname": "John Doe",
    "id": 0,
    "info": {
      "avatar": "avatar.png",
      "container": "user",
    },
    "n_answers": 2414,
    "name": "johndoe",
    "rank": 69,
    "registered_ago": "4 years ago",
    "score": 2414,
    "total": 11134,
    "valid_email": false
  },
  "pro_features": {
    "auditlog_enabled": true,
    "autoimporter_enabled": true,
    "webhooks_enabled": true
  },
  "project": {
    "allow_anonymous_contributors": false,
    "category_id": 2,
    "contacted": false,
    "contrib_button": "can_contribute",
    "created": "2015-06-29T08:23:14.201331",
    "description": "old",
    "featured": false,
    "id": 3117,
    "info": {
      "container": "user",
      "passwd_hash": null,
      "task_presenter": "HTML+CSS+JS"
      "thumbnail": "avatar.png"
    },
    "long_description": "algo",
    "n_blogposts": 0,
    "n_results": 0,
    "name": "name",
    "owner_id": 3,
    "published": true,
    "secret_key": "f",
    "short_name": "name",
    "updated": "2017-03-17T09:15:46.867215",
    "webhook": null
  },
  "target": "project.import_task",
  "task_tmpls": [
    "projects/tasks/gdocs-sound.html",
    "projects/tasks/gdocs-map.html",
    "projects/tasks/gdocs-image.html",
    "projects/tasks/gdocs-video.html",
    "projects/tasks/gdocs-pdf.html"
  ],
  "template": "/projects/task_import_options.html",
  "title": "Project: bevan &middot; Import Tasks"
}
```

Therefore, if you want to import tasks from a CSV link, you will have to
do the following GET:

    GET server/project/<short_name>/tasks/import?type=csv

That query will return the same output as before, but instead of the
available\_importers, you will get the the form fields and CSRF token
for that importer.

**POST**

To send a valid POST request, you need to pass the *csrf token* in the headers. Use the following header: "X-CSRFToken."

It returns a JSON object with the following information:

-   **flash**: A success message, or error indicating if the request was
    successful.

**Example output**

```json
{
  "flash": "Tasks imported",
  "next": "/project/<short_name>/tasks/",
  "status": "success"
}
```

## Project tutorial

**Endpoint: /project/&lt;short\_name&gt;/tutorial**

**GET**

It returns a JSON object with the following information:

-   **owner**: owner information
-   **project**: project information
-   **template**: The Jinja2 template that could be rendered.
-   **title**: The title for the view.

**Example output**

```json
{
  "owner": {
    "created": "2014-02-13T15:28:08.420187",
    "fullname": "John Doe",
    "info": {
      "avatar": "1410769844.15_avatar.png",
      "avatar_url": null,
      "container": "user_3927",
      "extra": null
    },
    "locale": null,
    "n_answers": 43565,
    "name": "jdoe",
    "rank": 3,
    "registered_ago": "3 years ago",
    "score": 43565
  },
  "project": {
    "created": "2014-02-22T15:09:23.691811",
    "description": "Image pattern recognition",
    "featured": true,
    "id": 1377,
    "info": {
      "container": "user_3927",
      "thumbnail": "app_1377_thumbnail_1410772569.58.png",
      "thumbnail_url": null
    },
    "last_activity": null,
    "last_activity_raw": null,
    "n_tasks": null,
    "n_volunteers": null,
    "name": "myproject",
    "overall_progress": null,
    "owner": null,
    "short_name": "johndoeproject",
    "updated": "2017-03-02T21:00:33.965587"
  },
  "template": "/projects/tutorial.html",
  "title": "Project: myproject"
}
```
## Project shortname

**Endpoint: /project/&lt;short\_name&gt;/**

*Allowed methods*: **GET**

**GET**

Shows project information and owner information.

If you are not the owner of the project or anonymous, then you will get only available public information for the owner and the project itself.

-   **last\_activity**: Last activity on the project.
-   **n\_completed\_tasks**: Number of completed tasks.
-   **n\_task\_runs**: Number of task runs.
-   **n\_tasks**: Number of tasks.
-   **n\_volunteers**: Number of volunteers.
-   **overall\_progress**: Overall progress.
-   **owner**: Owner user information.
-   **pro\_features**: Enabled pro features for the project.
-   **project**: Project information
-   **template**: Jinja2 template.
-   **title**: the title for the endpoint.

**Example output**

for logged in user JohnDoe:

```json
{
  "last_activity": "2015-01-21T12:01:41.209270",
  "n_completed_tasks": 0,
  "n_task_runs": 3,
  "n_tasks": 8,
  "n_volunteers": 1,
  "overall_progress": 0,
  "owner": {
    "admin": false,
    "api_key": "akjhfd85-8afd6-48af-f7afg-kjhsfdlkjhf1",
    "confirmation_email_sent": false,
    "created": "2014-08-11T08:59:32.079599",
    "email_addr": "johndoe@johndoe.com",
    "fullname": "John Doe",
    "id": 1234,
    "info": {
      "container": "user_1234"
    },
    "n_answers": 56,
    "name": "JohnDoe",
    "rank": 1813,
    "registered_ago": "2 years ago",
    "score": 56,
    "total": 11093,
    "valid_email": true
  },
  "pro_features": {
    "auditlog_enabled": true,
    "autoimporter_enabled": true,
    "webhooks_enabled": true
  },
  "project": {
    "allow_anonymous_contributors": true,
    "category_id": 2,
    "contacted": true,
    "contrib_button": "can_contribute",
    "created": "2015-01-21T11:59:36.519541",
    "description": "flickr678",
    "featured": false,
    "id": 4567,
    "info": {
      "task_presenter": "<div> .... "
    },
    "long_description": "flickr678\r\n",
    "n_blogposts": 0,
    "n_results": 0,
    "name": "flickr678",
    "owner_id": 9876,
    "published": true,
    "secret_key": "veryverysecretkey",
    "short_name": "flickr678",
    "updated": "2016-04-13T08:07:38.897626",
    "webhook": null
  },
  "template": "/projects/project.html",
  "title": "Project: flickr678"
}
```

Anonymous and other user output:

```json
{
  "last_activity": "2015-01-21T12:01:41.209270",
  "n_completed_tasks": 0,
  "n_task_runs": 3,
  "n_tasks": 8,
  "n_volunteers": 1,
  "overall_progress": 0,
  "owner": {
    "created": "2014-08-11T08:59:32.079599",
    "fullname": "John Doe",
    "info": {
      "avatar": null,
      "container": "user_4953"
    },
    "n_answers": 56,
    "name": "JohnDoe",
    "rank": 1813,
    "registered_ago": "2 years ago",
    "score": 56
  },
  "pro_features": {
    "auditlog_enabled": false,
    "autoimporter_enabled": false,
    "webhooks_enabled": false
  },
  "project": {
    "created": "2015-01-21T11:59:36.519541",
    "description": "flickr678",
    "id": 4567,
    "info": {
      "container": null,
      "thumbnail": null
    },
    "last_activity": null,
    "last_activity_raw": null,
    "n_tasks": null,
    "n_volunteers": null,
    "name": "flickr678",
    "overall_progress": null,
    "owner": null,
    "short_name": "flickr678",
    "updated": "2016-04-13T08:07:38.897626"
  },
  "template": "/projects/project.html",
  "title": "Project: flickr678"
}
```

## Project settings

**Endpoint: /project/&lt;short\_name&gt;/settings**

*Allowed methods*: **GET**

**GET**

Shows project information and owner information. Only works for
authenticated users for their projects (or admins). Anonymous users
will get a 302 to the login page. Logged in users with access rights will get a 403 when it's not their project.

-   **last\_activity**: Last activity on the project.
-   **n\_completed\_tasks**: Number of completed tasks.
-   **n\_task\_runs**: Number of task runs.
-   **n\_tasks**: Number of tasks.
-   **n\_volunteers**: Number of volunteers.
-   **overall\_progress**: Overall progress.
-   **owner**: Owner user information.
-   **pro\_features**: Enabled pro features for the project.
-   **project**: Project information
-   **template**: Jinja2 template.
-   **title**: the title for the endpoint.

The example output matches **/project/&lt;short\_name&gt;/**

## Project results

**Endpoint: /project/&lt;short\_name&gt;/results**

*Allowed methods*: **GET**

**GET**

Shows information about a project results template. If the logged in
user is the owner of the project you will get a more detailed owner
information and project information.

-   **last\_activity**: Last activity on the project.
-   **n\_completed\_tasks**: Number of completed tasks.
-   **n\_results**: Number of results
-   **n\_task\_runs**: Number of task runs.
-   **n\_tasks**: Number of tasks.
-   **n\_volunteers**: Number of volunteers.
-   **overall\_progress**: Overall progress.
-   **owner**: Owner user information.
-   **pro\_features**: Enabled pro features for the project.
-   **project**: Project information
-   **template**: Jinja2 template for results
-   **title**: the title for the endpoint.

**Example output**

For an anonymous user or when you are not the project owner:

```json
{
  "last_activity": "2015-01-21T12:01:41.209270",
  "n_completed_tasks": 0,
  "n_results": 0,
  "n_task_runs": 3,
  "n_tasks": 8,
  "n_volunteers": 1,
  "overall_progress": 0,
  "owner": {
    "created": "2014-08-11T08:59:32.079599",
    "fullname": "John",
    "info": {
      "avatar": null,
      "container": "user_4953"
    },
    "n_answers": 56,
    "name": "JohnDoe",
    "rank": 1813,
    "registered_ago": "2 years ago",
    "score": 56
  },
  "pro_features": {
    "auditlog_enabled": false,
    "autoimporter_enabled": false,
    "webhooks_enabled": false
  },
  "project": {
    "created": "2015-01-21T11:59:36.519541",
    "description": "flickr678",
    "featured": false,
    "id": 2417,
    "info": {
      "container": null,
      "thumbnail": null
    },
    "last_activity": null,
    "last_activity_raw": null,
    "n_tasks": null,
    "n_volunteers": null,
    "name": "flickr678",
    "overall_progress": null,
    "owner": null,
    "short_name": "flickr678",
    "updated": "2016-04-13T08:07:38.897626"
  },
  "template": "/projects/results.html",
  "title": "Project: flickr678"
}
```

## Project stats

**Endpoint: /project/&lt;short\_name&gt;/stats**

*Allowed methods*: **GET**

**GET**

Shows project statistics if available.

If you are not the owner of the project or anonymous, then you will get only available public information for the owner and the project itself.

-   **avg\_contrib\_time**: Average contribution time (NOT existing when
    no statistics there!).
-   **projectStats**: Project statistics (NOT existing when no
    statistics there!).
-   **userStats**: User statistics (NOT existing when no statistics
    there!).
-   **n\_completed\_tasks**: Number of completed tasks.
-   **n\_tasks**: Number of tasks.
-   **n\_volunteers**: Number of volunteers.
-   **overall\_progress**: Progress (0..100).
-   **owner**: Owner user information
-   **pro\_features**: Enabled pro features for the project.
-   **project**: Project information
-   **template**: Jinja2 template.
-   **title**: the title for the endpoint.

**Example output** Statistics are existing in this output:

```json
{
  "avg_contrib_time": 0,
  "n_completed_tasks": 2,
  "n_tasks": 2,
  "n_volunteers": 59,
  "overall_progress": 100,
  "owner": {
    "created": "2012-06-06T06:27:18.760254",
    "fullname": "Daniel Lombraña González",
    "info": {
      "avatar": "1422360933.8_avatar.png",
      "container": "user_3"
    },
    "n_answers": 2998,
    "name": "teleyinex",
    "rank": 66,
    "registered_ago": "4 years ago",
    "score": 2998
  },
  "pro_features": {
    "auditlog_enabled": false,
    "autoimporter_enabled": false,
    "better_stats_enabled": true,
    "webhooks_enabled": false
  },
  "project": {
    "created": "2013-01-10T19:58:55.454015",
    "description": "Facial expressions that convey feelings",
    "featured": true,
    "id": 253,
    "info": {
      "container": "user_3",
      "thumbnail": "project_253_thumbnail_1460620575.png"
    },
    "last_activity": null,
    "last_activity_raw": null,
    "n_tasks": null,
    "n_volunteers": null,
    "name": "The Face We Make",
    "overall_progress": null,
    "owner": null,
    "short_name": "thefacewemake",
    "updated": "2016-04-14T07:56:16.114006"
  },
  "projectStats": "{\"userAuthStats\": {\"top5\": [], \"values\": [], \"label\": \"Authenticated Users\"} ...",
  "template": "/projects/stats.html",
  "title": "Project: The Face We Make &middot; Statistics",
  "userStats": {
    "anonymous": {
      "pct_taskruns": 0,
      "taskruns": 0,
      "top5": [],
      "users": 0
    },
    "authenticated": {
      "pct_taskruns": 0,
      "taskruns": 0,
      "top5": [],
      "users": 0
    },
    "geo": false
  }
}
```

## Project tasks

**Endpoint: /project/&lt;short\_name&gt;/tasks**

*Allowed methods*: **GET**

**GET**

Shows project tasks.

If you are not the owner of the project or anonymous, then you will get
only available public information for the owner and the project itself.

-   **autoimporter\_enabled**: If autoimporter is enabled.
-   **last\_activity**: Last activity.
-   **n\_completed\_tasks**: Number of completed tasks.
-   **n\_task\_runs**: Number of task runs.
-   **n\_tasks**: Number of tasks.
-   **n\_volunteers**: Number of volunteers.
-   **overall\_progress**: Progress (0..100).
-   **owner**: Owner user information
-   **pro\_features**: Enabled pro features for the project.
-   **project**: Project information.
-   **template**: Jinja2 template.
-   **title**: the title for the endpoint.

**Example output**

for another project where you are not the owner:

```json
{
  "autoimporter_enabled": true,
  "last_activity": "2017-03-02T21:00:33.627277",
  "n_completed_tasks": 184839,
  "n_task_runs": 1282945,
  "n_tasks": 193090,
  "n_volunteers": 20016,
  "overall_progress": 95,
  "owner": {
    "created": "2014-02-13T15:28:08.420187",
    "fullname": "John Smith",
    "info": {
      "avatar": "1410769844.15_avatar.png",
      "container": "user_3927",
      "extra": null
    },
    "locale": null,
    "n_answers": 43565,
    "name": "pmisson",
    "rank": 3,
    "registered_ago": "3 years ago",
    "score": 43565
  },
  "pro_features": {
    "auditlog_enabled": true,
    "autoimporter_enabled": true,
    "webhooks_enabled": true
  },
  "project": {
    "created": "2014-02-22T15:09:23.691811",
    "description": "Image pattern recognition",
    "featured": true,
    "id": 1377,
    "info": {
      "container": "user_3927",
      "thumbnail": "app_1377_thumbnail_1410772569.58.png"
    },
    "last_activity": null,
    "last_activity_raw": null,
    "n_tasks": null,
    "n_volunteers": null,
    "name": "Cool Project",
    "overall_progress": null,
    "owner": null,
    "short_name": "coolproject",
    "updated": "2017-03-02T21:00:33.965587"
  },
  "template": "/projects/tasks.html",
  "title": "Project: Cool project"
}
```

## Project task id

**Endpoint: /project/&lt;short\_name&gt;/task/&lt;int:task\_id&gt;**

*Allowed methods*: **GET**

**GET**

Shows a project task based on id.

If you are not the owner of the project or anonymous, then you will get
only available public information for the owner and the project itself.

-   **owner**: Owner user information
-   **project**: Project information.
-   **template**: Jinja2 template of the task HTML template.
-   **title**: the title for the endpoint.

**Example output**

for another project where you are not the owner:

```json
{
  "owner": {
    "created": "2014-08-11T08:59:32.079599",
    "fullname": "John Doe",
    "info": {
      "avatar": "1458638093.9_avatar.png",
      "container": "user_4953",
      "extra": null
    },
    "locale": null,
    "n_answers": 257,
    "name": "JohnD",
    "rank": 840,
    "registered_ago": "2 years ago",
    "score": 257
  },
  "project": {
    "created": "2015-01-21T11:59:36.519541",
    "description": "flickr678",
    "featured": false,
    "id": 2417,
    "info": {
      "container": null,
      "thumbnail": null
    },
    "last_activity": null,
    "last_activity_raw": null,
    "n_tasks": null,
    "n_volunteers": null,
    "name": "flickr678",
    "overall_progress": null,
    "owner": null,
    "short_name": "flickr678",
    "updated": "2017-03-22T13:03:55.496660"
  },
  "template": "/projects/presenter.html",
  "title": "Project: flickr678 &middot; Contribute"
}
```

## Project Category

**Endpoint: /project/category/&lt;short\_name&gt;/**

*Allowed methods*: **GET**

**GET**

Gives you the list of projects in a category.

-   **pagination**: A pagination object for getting projects from this
    category.
-   **active\_cat**: Active category.
-   **projects**: List of projects belonging to this category.
-   **categories**: List of available categories in this server.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "active_cat": {
    "created": null,
    "description": "Social projects",
    "id": 2,
    "name": "Social",
    "short_name": "social"
  },
  "categories": [
    {
      "created": null,
      "description": "Featured projects",
      "id": null,
      "name": "Featured",
      "short_name": "featured"
    },
    {
      "created": null,
      "description": "Social projects",
      "id": 2,
      "name": "Social",
      "short_name": "social"
    },
    {
      "created": "2013-06-18T11:13:44.789149",
      "description": "Art projects",
      "id": 3,
      "name": "Art",
      "short_name": "art"
    },
  ],
  "pagination": {
    "next": false,
    "page": 1,
    "per_page": 20,
    "prev": false,
    "total": 1
  },
  "projects": [
    {
      "created": "2014-02-22T15:09:23.691811",
      "description": "Image pattern recognition",
      "id": 1377,
      "info": {
        "container": "7",
        "thumbnail": "58.png"
      },
      "last_activity": "2 weeks ago",
      "last_activity_raw": "2017-01-31T09:18:28.450391",
      "n_tasks": 169671,
      "n_volunteers": 17499,
      "name": "Name",
      "overall_progress": 80,
      "owner": "John Doe",
      "short_name": "name",
      "updated": "2017-01-31T09:18:28.491496"
    },
  ],
  "template": "/projects/index.html",
  "title": "Projects"
}
```

!!! note
    To override the default ranking you pass the **orderby** query parameter to sort projects by any of the attributes listed above, such as  *n\_volunteers* or *n\_tasks*. The **desc** query parameter can also be added to sort in descending order. For example: GET
    /project/category/&lt;short\_name&gt;/?orderby=n\_tasks&desc=True


## Project Category Featured

**Endpoint: /project/category/featured/**

*Allowed methods*: **GET**

**GET**

Gives you the list of featured projects.

-   **pagination**: A pagination object for getting new featured
    projects from this category.
-   **active\_cat**: Active category.
-   **projects**: List of projects belonging to this category.
-   **categories**: List of available categories in this server.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "active_cat": {
    "created": null,
    "description": "Featured projects",
    "id": null,
    "name": "Featured",
    "short_name": "featured"
  },
  "categories": [
    {
      "created": null,
      "description": "Featured projects",
      "id": null,
      "name": "Featured",
      "short_name": "featured"
    },
    {
      "created": null,
      "description": "Social projects",
      "id": 2,
      "name": "Social",
      "short_name": "social"
    },
    {
      "created": "2013-06-18T11:13:44.789149",
      "description": "Art projects",
      "id": 3,
      "name": "Art",
      "short_name": "art"
    },
  ],
  "pagination": {
    "next": false,
    "page": 1,
    "per_page": 20,
    "prev": false,
    "total": 1
  },
  "projects": [
    {
      "created": "2014-02-22T15:09:23.691811",
      "description": "Image pattern recognition",
      "id": 1377,
      "info": {
        "container": "7",
        "thumbnail": "58.png"
      },
      "last_activity": "2 weeks ago",
      "last_activity_raw": "2017-01-31T09:18:28.450391",
      "n_tasks": 169671,
      "n_volunteers": 17499,
      "name": "Name",
      "overall_progress": 80,
      "owner": "John Doe",
      "short_name": "name",
      "updated": "2017-01-31T09:18:28.491496"
    },
  ],
  "template": "/projects/index.html",
  "title": "Projects"
}
```

!!! note
    To override the default ranking, you pass the **orderby** query parameter to sort projects by any of the attributes listed above, such as *n\_volunteers* or *n\_tasks*. The **desc** query parameter can also be added to sort in descending order. For example: GET
    /project/category/featured/?orderby=n\_tasks&desc=True


## Project Category Draft

**Endpoint: /project/category/draft/**

*Allowed methods*: **GET**

**GET**

Gives you the list of featured projects.

-   **pagination**: A pagination object for getting new draft projets
    from this category.
-   **active\_cat**: Active category.
-   **projects**: List of projects belonging to this category.
-   **categories**: List of available categories in this server.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "active_cat": {
    "created": null,
    "description": "Draft projects",
    "id": null,
    "name": "Draft",
    "short_name": "draft"
  },
  "categories": [
    {
      "created": null,
      "description": "Draft projects",
      "id": null,
      "name": "Draft",
      "short_name": "draft"
    },
    {
      "created": null,
      "description": "Social projects",
      "id": 2,
      "name": "Social",
      "short_name": "social"
    },
    {
      "created": "2013-06-18T11:13:44.789149",
      "description": "Art projects",
      "id": 3,
      "name": "Art",
      "short_name": "art"
    },
  ],
  "pagination": {
    "next": false,
    "page": 1,
    "per_page": 20,
    "prev": false,
    "total": 1
  },
  "projects": [
    {
      "created": "2014-02-22T15:09:23.691811",
      "description": "Draft 1",
      "id": 17,
      "info": {
        "container": "7",
        "thumbnail": "58.png"
      },
      "last_activity": "2 weeks ago",
      "last_activity_raw": "2017-01-31T09:18:28.450391",
      "n_tasks": 0,
      "n_volunteers": 0,
      "name": "Name",
      "overall_progress": 0,
      "owner": "John Doe",
      "short_name": "name",
      "updated": "2017-01-31T09:18:28.491496"
    },
  ],
  "template": "/projects/index.html",
  "title": "Projects"
}
```

!!! note
    To override the default ranking, you pass the **orderby** query parameter to
    sort projects by any of the attributes listed above, such as
    *n\_volunteers* or *n\_tasks*. The **desc** query parameter can also be added to sort in descending order. For example: GET
    /project/category/draft/?orderby=n\_tasks&desc=True
