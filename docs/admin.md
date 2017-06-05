Administrating PYBOSSA
======================

PYBOSSA has three type of users: anonymous, authenticated and
administrators. By default the first created user in a PYBOSSA server
will become an administrator and manage the site with full privileges.

And admin user will be able to access the admin page by clicking in the
user name and then in the link *Admin site*.

![image](http://i.imgur.com/5YWAJ8E.png)

Administrators can manage different areas of the server:

> 1.  Background jobs
> 2.  Featured projects
> 3.  Categories
> 4.  Administrators
> 5.  Users

![image](http://i.imgur.com/cfUF6K2.png%0A%20:width:100%)

<div class="admonition note">

Admins can also modify all projects, and also see which projects are marked

:   as **Draft**: projects that do not have at least one task and a
    task-presenter to allow other volunteers to participate.

</div>

<div class="admonition note">

In the users option, admins will be able

:   to obtain a list of all registered users in the PYBOSSA system, in
    either json or csv formats.

</div>

<div class="admonition note">

In addition, admins can access an extension called [RQ dashboard](https://github.com/nvie/rq-dashboard) from where to

:   monitor all the background jobs and even cancel them or retry failed
    ones.

</div>

Featured Projects
-----------------

In this section, admins can add/remove projects to the front page of the
site.

![image](http://i.imgur.com/K9deWZo.png%0A%20:width:100%)

You will see a "Add to Featured" link to add a a project to featured
front page or a "Remove from Featured" to remove it.

Categories
----------

PYBOSSA provides by default two type of categories:

1.  **Thinking**: for projects where the users can use their skills to
    solve a problem (i.e. image or sound pattern recognition).
2.  **Sensing**: for projects where the users can help gathering data
    using tools like [EpiCollect](http://plus.epicollect.net) and then
    analyze the data in the PYBOSSA server.

Admins can add as many categories as they want, just type then and its
description and click in the green button labeled: Add category.

![image](http://i.imgur.com/FlTowJ7.png){width="100%"}

<div class="admonition note">

You cannot delete a category if it has one or more projects associated

:   with it. You can however rename the category or delete it when all
    the associated projects are not linked to the given category.

</div>

Administrators
--------------

In this section an administrator will be able to add/remove users to the
admin role. Basically, you can search by user name -nick name- and add
them to the admin group.

![image](http://i.imgur.com/WSwNFxy.png%0A%20:width:100%)

As with the categories section, a green button will allow you to add the
user to the admin group, while a red button will be shown to remove the
user from the admin group.

Audit log
---------

When a project is created, deleted or updated, the system registers its
actions in the server. Admins will have access to all the logged actions
in every project page, in a section named **Audit log**.

![image](http://i.imgur.com/BjcJQW7.png){width="100%"}

The section will let you know the following information:

-   **When**: when the action was taken.
-   **Action**: which action was taken: 'created', 'updated', or
    'deleted'.
-   **Source**: if it was done the action via the API or the WEB
    interface.
-   **Attribute**: which attribute of the project has been changed.
-   **Who**: the user who took the action.
-   **Old value**: the previous value before the action.
-   **New value**: the new value after the action.

<div class="admonition note">

Only admins and users marked as *pro* can see the audit log.

</div>

Dashboard
---------

The dashboard allows you to see what's going on in your PYBOSSA server.

![image](http://i.imgur.com/TmB0dx2.png)

<div class="admonition note">

This feature requires PostgreSQL &gt;= 9.3. Please upgrade as soon as possible your

:   server to have this feature.

</div>

The dashboard shows the following information for the last 7 days:

-   **Active users**: Number of users that have contributed at least 1
    task\_run in the last 7 days.
-   **Active anonymous users**: Number of anonymous users that have
    contributed at least 1 task\_run in the last 7 days.
-   **New projects**: Projects created in the last 7 days.
-   **Updated projects**: Updated projects in the last 7 days.
-   **Updated projects**: Updated projects in the last 7 days.
-   **New users**: Number of new users registered in the last 7 days.
-   **Number of returning users**: Number of returning users in the last
    7 days classified by number of days coming back.
-   **Recent activity feed**: Last events in real time of the server.

The dashboard is updated every 24 hours via the background jobs. These
jobs are scheduled in the *low* queue.
