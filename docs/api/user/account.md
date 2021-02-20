### Account index

**Endpoint: /account/page/&lt;int:page&gt;**

*Allowed methods*: **GET**

**GET**

It returns a JSON object with the following information:

-   **accounts**: this key holds the list of accounts for the given
    page.
-   **pagination**: this key holds the pagination information.
-   **top\_users**: this key holds the top users (including the user if
    authenticated) with their rank and scores.
-   **update\_feed**: the latest actions in the server (users created,
    contributions, new tasks, etc.).
-   **template**: the Jinja2 template that should be rendered in case of
    text/html.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "accounts": [
    {
      "created": "2015-06-10T15:02:38.411497",
      "fullname": "Scifabric",
      "info": {
        "avatar": "avatar.png",
        "container": "user_234234dd3"
      },
      "locale": null,
      "name": "Scifabric",
      "rank": null,
      "registered_ago": "1 year ago",
      "score": null,
      "task_runs": 3
    },
  ],
  "pagination": {
    "next": true,
    "page": 3,
    "per_page": 24,
    "prev": true,
    "total": 11121
  },
  "template": "account/index.html",
  "title": "Community",
  "top_users": [
    {
      "created": "2014-08-17T18:28:56.738119",
      "fullname": "Buzz Bot",
      "info": {
        "avatar": "avatar.png",
        "container": "user_55"
      },
      "locale": null,
      "name": "buzzbot",
      "rank": 1,
      "registered_ago": null,
      "score": 54247,
      "task_runs": null
    },
  ],
  "total": 11121,
  "update_feed": []
}
```

### Account registration

**Endpoint: /account/register**

*Allowed methods*: **GET/POST**

**GET**

It returns a JSON object with the following information:

-   **form**: The form fields that need to be sent for creating an
    account. It contains the CSRF token for validating the POST, as well
    as an errors field in case that something is wrong.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title of the page.

**Example output**

```json
{
  "form": {
    "confirm": null,
    "csrf": "token,"
    "email_addr": null,
    "errors": {},
    "fullname": null,
    "name": null,
    "password": null
  },
  "template": "account/register.html",
  "title": "Register"
}
```

**POST**

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken".

It returns a JSON object with the following information:

-   **next**: URL that you JavaScript can follow as a redirect. It is
    not mandatory.

**Example output**

```json
{
    "next":"/about"
}
```

If there's an error in the form fields, you will get them in the
**form.errors** key:

```json
{
  "form": {
    "confirm": "daniel",
    "csrf": "token",
    "email_addr": "daniel",
    "errors": {
      "email_addr": [
        "Invalid email address."
      ],
      "name": [
        "The user name is already taken"
      ]
    },
    "fullname": "daniel",
    "name": "daniel",
    "password": "daniel"
  },
  "template": "account/register.html",
  "title": "Register"
}
```

If email confirmation is required for registering you will get this
account validation result when all input data is correct. Note: Keep in
mind that account is not created fully until the user confirmed his
email.

```json
{
  "status": "sent",
  "template": "account/account_validation.html",
  "title": "Account validation"
}
```

### Account sign in

**Endpoint: /account/signin**

*Allowed methods*: **GET/POST**

**GET**

It returns a JSON object with the following information:

-   **form**: the form fields that need to be sent for signing a user.
    It contains the csrf token for validating the post, as well as an
    errors field in case that something is wrong.
-   **template**: The Jinja2 template that could be rendered.

**Example output**

```json
{
  "form": {
    "csrf": "token",
    "email": null,
    "errors": {},
    "password": null
  },
  "next": null,
  "template": "account/signin.html",
  "title": "Sign in"
}
```

**POST**

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken".

It returns a JSON object with the following information:

-   **flash**: A success message, or error indicating if the request was
    successful.
-   **form**: the form fields with the sent information. It contains the
    csrf token for validating the post, as well as an errors field in
    case that something is wrong.

**Example output**

```json
{
  "auth": {
    "facebook": true,
    "google": true,
    "twitter": true
  },
  "flash": "Please correct the errors",
  "form": {
    "csrf": "token",
    "email": "prueba@prueba.com",
    "errors": {
      "password": [
        "You must provide a password"
      ]
    },
    "password": ""
  },
  "next": null,
  "status": "error",
  "template": "account/signin.html",
  "title": "Sign in"
}
```

If the login is successful, then, you will get something like this:

```json
{
  "flash": "Welcome back John Doe",
  "next": "/",
  "status": "success"
}
```

### Account sign out

**Endpoint: /account/signout**

*Allowed methods*: **GET**

It returns a JSON object with the following information:

-   **next**: suggested redirection after the sign out.
-   **message**: message displaying success for sign out.

### Account recover password

**Endpoint: /account/forgot-password**

*Allowed methods*: **GET/POST**

**GET**

It returns a JSON object with the following information:

-   **form**: the form fields that need to be sent for creating an
    account. It contains the csrf token for validating the post, as well
    as an errors field in case that something is wrong.
-   **template**: The Jinja2 template that could be rendered.

**Example output**

```json
{
  "form": {
    "csrf": "token,"
    "email_addr": null
  },
  "template": "account/password_forgot.html"
}
```

**POST**

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken".

It returns a JSON object with the following information:

-   **flash**: A success message, or error indicating if the request was
    succesful.
-   **form**: the form fields with the sent information. It contains the
    csrf token for validating the post, as well as an errors field in
    case that something is wrong.

**Example output**

```json
{
  "flash": [
    "We don't have this email in our records."
  ],
  "form": {
    "csrf": "1483549683.06##cc1c7ff101b2a14a89cac5462e5028e6235ddb31",
    "email_addr": "algo@algo.com",
    "errors": {}
  },
  "template": "/account/password_forgot.html"
}
```

If there's an error in the form fields, you will get them in the
**form.errors** key:

```json
{
  "flash": "Something went wrong, please correct the errors on the form",
  "form": {
    "csrf": "1483552042.97##f0e36b1b113934532ff9c8003b120365ff45f5e4",
    "email_addr": "algoom",
    "errors": {
      "email_addr": [
        "Invalid email address."
      ]
    }
  },
  "template": "/account/password_forgot.html"
}
```

### Account name

\*\*Endpoint: /account/&lt;name&gt;

*Allowed methods*: **GET**

**GET**

It returns a JSON object with the following information:

-   **projects\_contrib**: a list of projects the user has contributed
    too.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: The title for the view.
-   **user**: User information, including fullname, rank etc.

**Example output**

If you are not logged in or requesting details of another user you will
only get public viewable information. If you are logged in you will also
get private information in the user field. Sample output of public
information:

```json
{
    "projects_contrib": [
        {
            "description": "this is a project",
            "info": {
                "container": "123",
                "thumbnail": "thumbnailx"
            },
            "n_tasks": 4,
            "n_volunteers": 0,
            "name": "test12334",
            "overall_progress": 0,
            "short_name": "test12334"
        }
    ],
    "projects_created": [
        {
            "description": "Youtube 1",
            "info": {
                "container": "345",
                "thumbnail": "thumbnaily"
            },
            "n_tasks": 15,
            "n_volunteers": 0,
            "name": "JohnDoe Youtube 1",
            "overall_progress": 0,
            "short_name": "johnyoutube1"
        },
    ]
    "template": "/account/public_profile.html",
    "title": "John &middot; User Profile",
    "user": {
        "fullname": "Joen Doe",
        "info": {
            "container": "user_4953"
        },
        "n_answers": 56,
        "name": "JohnDoe",
        "rank": 1813,
        "score": 56
    }
}
```

Example of logged in user:

```json
{
    ...
    "user": {
        "admin": false,
        "api_key": "aa3ee485-896d-488a-83f7-88a29bf45171",
        "confirmation_email_sent": false,
        "created": "2014-08-11T08:59:32.079599",
        "email_addr": "johndoe@johndoe.com",
        "facebook_user_id": null,
        "fullname": "John Doe",
        "google_user_id": null,
        "id": 4953,
        "info": {
            "container": "user_4953"
        },
        "n_answers": 56,
        "name": "JohnDoe",
        "rank": 1813,
        "registered_ago": "2 years ago",
        "score": 56,
        "total": 10046,
        "twitter_user_id": null,
        "valid_email": true
    }
}
```

### Account profile

\*\*Endpoint: /account/profile

*Allowed methods*: **GET**

**GET**

If logged in you will get the same information as on
/account/&lt;name&gt; (see above). If you are not logged in you will get
the following example output

**Example output**

```json
{
  "next": "/account/signin",
  "status": "not_signed_in"
}
```

### Account projects

**Endpoint: /account/&lt;name&gt;/projects**

*Allowed methods*: **GET**

**GET**

The user needs to be logged in. It returns a JSON object with the
following information:

-   **projects\_draft**: a list of draft projects of the user.
-   **projects\_published**: a list of published projects of the user.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: The title for the view.

**Example output**

```json
{
  "projects_draft": [
    {
      "description": "This should be the Youtube Project",
      "id": 3169,
      "info": {
        "task_presenter": "..."
      },
      "n_tasks": 0,
      "n_volunteers": 0,
      "name": "Youtube_Test1",
      "overall_progress": 0,
      "owner_id": 4953,
      "short_name": "youtube_test1"
    },
    ...
  ],
  "projects_published": [
    {
      "description": "Youtube 1",
      "id": 3206,
      "info": {
        "results": "",
        "task_presenter": ".."
        "tutorial": ""
      },
      "n_tasks": 15,
      "n_volunteers": 0,
      "name": "Youtube 1",
      "overall_progress": 0,
      "owner_id": 4953,
      "short_name": "youtube1"
    },
    ...
  ],
  "template": "account/projects.html",
  "title": "Projects"
}
```

### Account update profile

**Endpoint: /account/&lt;name&gt;/update**

*Allowed methods*: **GET/POST**

**GET**

It returns a JSON object with the following information:

-   **form**: the form fields that need to be sent for updating account.
    It contains the csrf token for validating the post, as well as an
    errors field in case that something is wrong.
-   **password\_form**: the form fields that need to be sent for
    updating the account's password. It contains the csrf token for
    validating the post, as well as an errors field in case that
    something is wrong.
-   **upload\_form**: the form fields that need to be sent for updating
    the account's avatar. It contains the csrf token for validating the
    post, as well as an errors field in case that something is wrong.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: The title for the view.

**Example output**

```json
{
  "flash": null,
  "form": {
    "ckan_api": null,
    "csrf": "token",
    "email_addr": "email@emai.com",
    "errors": {},
    "fullname": "John Doe",
    "id": 0,
    "locale": "en",
    "name": "johndoe",
    "privacy_mode": true,
    "subscribed": true
  },
  "password_form": {
    "confirm": null,
    "csrf": "token",
    "current_password": null,
    "errors": {},
    "new_password": null
  },
  "show_passwd_form": true,
  "template": "/account/update.html",
  "title": "Update your profile: John Doe",
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

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken".

As this endpoint supports **three** different forms, you must specify
which form are you targeting adding an extra key: **btn**. The options
for this key are:

-   **Profile**: to update the **form**. **Upload**: to update the
    **upload\_form**. **Password**: to update the **password\_form**.
    **External**: to update the **form** but only the external services.

!!! note
    Be sure to respect the Uppercase in the first letter, otherwise it will
    fail.

It returns a JSON object with the following information:

-   **flash**: A success message, or error indicating if the request was
    successful.
-   **form**: the form fields with the sent information. It contains the
    csrf token for validating the post, as well as an errors field in
    case that something is wrong.

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
    "ckan_api": null,
    "csrf": "token",
    "email_addr": "pruebaprueba.com",
    "errors": {
      "email_addr": [
        "Invalid email address."
      ]
    },
    "fullname": "prueba de json",
    "id": 0,
    "locale": "es",
    "name": "pruebaadfadfa",
    "privacy_mode": true,
    "subscribed": true
  },
  "password_form": {
    "confirm": "",
    "csrf": "token",
    "current_password": "",
    "errors": {},
    "new_password": ""
  },
  "show_passwd_form": true,
  "template": "/account/update.html",
  "title": "Update your profile: John Doe",
  "upload_form": {
    "avatar": "",
    "csrf": "token",
    "errors": {},
    "id": 0,
    "x1": 0,
    "x2": 0,
    "y1": 0,
    "y2": 0
  }
}
```

!!! note
    For updating the avatar is very important to not set the *Content-Type*. If you
    are using jQuery, set it to False, so the file is handled properly. To still
    recieve a JSON response you can add the response_format=json query
    paramater to your request.

    The (x1,x2,y1,y2) are the coordinates for cutting the image and create
    the avatar.

    (x1,y1) are the offset left of the cropped area and the offset top of
    the cropped area respectively; and (x2,y2) are the width and height of
    the crop.

### Account reset password

**Endpoint: /account/reset-password**

*Allowed methods*: **GET/POST**

**GET**

*Required arguments*: **key** a string required to validate the link for
updating the password of the user. This key is sent to the user via
email after requesting to reset the password.

It returns a JSON object with the following information:

-   **form**: the form fields that need to be sent for updating account.
    It contains the csrf token for validating the post, as well as an
    errors field in case that something is wrong.
-   **template**: The Jinja2 template that could be rendered.

**Example output**

```json
{
  "form": {
    "confirm": null,
    "csrf": "token",
    "current_password": null,
    "errors": {},
    "new_password": null
  },
  "template": "/account/password_reset.html"
```

**POST**

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken".

It returns a JSON object with the following information:

-   **flash**: A success message, or error indicating if the request was
    succesful.
-   **status**: A status message, indicating if something went wrong.
-   **next**: Suggested URL to redirect the user.

**Example output**

```json
{
    "status": "success",
    "flash": "You reset your password successfully!",
    "next": "/"
}
```

### Account reset API Key

**Endpoint: /account/&lt;user&gt;/resetapikey**

*Allowed methods*: **GET/POST**

**GET**

It returns a JSON object with the following information:

-   **csrf**: The CSRF token for validating the post.

**Example output**

```json
{
    "form":
        {
            "csrf": "token",
        }
}
```

**POST**

To send a valid POST request you need to pass the *csrf token* in the
headers. Use the following header: "X-CSRFToken".

It returns a JSON object with the following information:

-   **flash**: A success message, or error indicating if the request was
    succesful.
-   **status**: A status message, indicating if something went wrong.
-   **next**: Suggested URL to redirect the user.

**Example output**

```json
{
    "status": "success",
    "flash": "New API-KEY generated",
    "next": "/account/<user>"
}
```

### Account subscribe to newsletter

\*\*Endpoint: /account/newsletter

*Allowed methods*: **GET**

**GET**

It returns a JSON object with the following information:

-   **template**: The template that Jinja2 will render.
-   **title**: The title of the endpoint.
-   **next**: The next URL.

**Example output**

```json
{
    "template": "account/newsletter.html",
    "title": "Subscribe to our Newsletter",
    "next": "/"
}
```

If you want to subscribe a user, then you have to call the same endpoint
with the following argument: *subscribe=true*

**Example output**

```json
{
    "flash": "You are subscribed to our newsletter",
    "status": "success",
    "next": "/"
}
```

### Account confirm email

**Endpoint: /account/confirm-email**

*Allowed methods*: **GET**

**GET**

If account validation is enabled, then, using this endpoint the user
will receive an email to validate its account. It returns a JSON object
with the following information:

-   **flash**: A message stating that an email has been sent.
-   **status**: The status of the call.
-   **next**: The next url.

**Example output**

```json
{
    "flash": 'Ane email has been sent to validate your e-mail address.',
    'status': 'info',
    'next': '/account/<username>/'
}
```

### Account delete

**Endpoint: /account/<name>/delete**

*Allowed methods*: **GET**

**GET**

If you send a GET request to this endpoint, PYBOSSA will enequeue a job to delete the user account.

!!! note
    You should build a confirmation check before hitting this enpoint, as this action cannot be undone.

**Example output**

```json
{
    "template": None
    'job': 'enqueued'
}
```

### Account export

**Endpoint: /account/<name>/export**

*Allowed methods*: **GET**

**GET**

If you send a GET request to this endpoint, PYBOSSA will enequeue a job to create zip files for the <user> with his/her personal data.

**Example output**

```json
{
    "flash": "GDPR export started",
    "next": "/account/user2/",
    "status": "success"
}
```
