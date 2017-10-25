## Using your user database

Since version v2.3.0 PYBOSSA supports external User IDs. This means that you can efficiently use your database of users without having to register them in the PYBOSSA server. As a benefit, you will be able to track your users within the PYBOSSA server providing a straightforward and easy experience for them.

A typical case for this would be for example a native phone app
(Android, iOS or Windows).

Usually, phone apps have their user database. With this in mind, you can add a crowdsourcing feature to your phone app by just using PYBOSSA in the following way.

First, create a project. When you build a project in PYBOSSA, the system will create for you a *secret key*. This secret key will be used by your phone app to authenticate all the requests and avoid other users to send data to your project via external user API.

!!! note
    We highly recommend using SSL on your server to secure all the process. You can use Let's Encrypt certificates for free. Check their
    [documentation.](https://certbot.eff.org/)

Now your phone app will have to authenticate to the server to get tasks and post task runs.

To do it, all you have to do is to create an HTTP Request with an
Authorization Header like this:

    HEADERS Authorization: project.secret_key
    GET http://{pybossa-site-url}/api/auth/project/short_name/token

That request will return a JWT token for you. With that token, you will be able to start requesting tasks for your user base passing again an authorization header. Imagine a user from your database is identified like this: '1xa':

    HEADERS Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
    GET http://{pybossa-site-url}/api/{project.id}/newtask?external_uid=1xa

That will return a task for the user ID 1xa that belongs to your database but not to PYBOSSA. Then, once the user has completed the task you will be able to submit it like this:

    HEADERS Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
    POST http://{pybossa-site-url}/api/taskrun?external_uid=1xa

!!! note
    The TaskRun object needs to have the external_uid field filled with 1xa.

As simple as that!

