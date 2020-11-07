# Administrating PYBOSSA

PYBOSSA provides an admin section where administrators will be able to see a dashboard with global statistics, manage the background jobs, featured projects, categories, administrators, and users.

## Roles

PYBOSSA has four type of users: anonymous, authenticated, pro and administrators. By default the first created user in a PYBOSSA server
will become an administrator and manage the site with full privileges.

And admin user will be able to access the admin page by clicking on the username and then in the link *Admin site*.

![image](https://i.imgur.com/5YWAJ8E.png)

Administrators have full privileges on the server. They can modify anything within the server. Especially, they will be able to handle the following areas of the server:

1.  Background jobs.
2.  Featured projects.
3.  Categories.
4.  Administrators.
5.  Users.

![image](https://i.imgur.com/cfUF6K2.png:width:100%)

Admins can also modify all projects. An admin can hide a project, update its task presenter, add new tasks, delete tasks or results. In other words, it can modify any aspect of any project within the server.

### Adding new administrators
In the admin area you will see a specific card for managing the administrators. In this card, you will be able to search by username to add new administrators. Also, you will see the list of current admins. From there, you will be able to remove them by clicking on the remove button below each username.

![image](https://i.imgur.com/WSwNFxy.png:width:100%)

### Adding pro users
This feature is not available at the moment.  However, you can add a pro user within your server by modifying the user field **pro** via SQL.

## Dashboard
This card provides an overview of the PYBOSSA server within the last seven days.

The dashboard is updated every 24 hours via the background jobs. These jobs are scheduled in the *low* queue.

### Active users
It provides the total number of active users (registered) as well as a graph showing the number of users active per day.

### Active anonymous users
It provides the total number of active anonymous users (registered) as well as a graph showing the number of them active per day.

### Draft projects
It gives you a list of draft projects created within the last seven days.  It also provides the total number of this type of projects.

PYBOSSA considers a project to be in draft mode when it does not have a task and a task presenter.

### Published projects
It gives you a list of published projects published within the last seven days.  It also provides the total number of this type of projects.

PYBOSSA considers a project to be published when it does have at least a task and a task presenter.

### Updated projects
It gives you a list of updated projects within the last seven days.  It also provides the total number of this type of projects.

PYBOSSA considers a project to be updated when anything related to it has been updated: a new blog post, new tasks, new task runs, edits on the task presenter, etc.

### New tasks
It provides the total number of new tasks created in the PYBOSSA server as well as a chart showing how many each day were created.

### New answers (or task runs)
It provides the total number of new answers (task runs) created in the PYBOSSA server as well as a chart showing how many each day were created.

### New users
It provides the total number of new registered users within the last seven days. It also includes a chart showing how many new users each day registered.

### Returning users
This chart shows how many users have contributed at least a task to a project, two, three, four, five, six and seven days in a row.

This statistic shows how many users you have in the system that contribute a lot and come back every day to contribute to your projects.

### Recent activity feed
This section shows the action of the PYBOSSA system in real time. You will be able to see the last 20 events of the system regarding new registrations, when a task has been completed, or a new blog post has been published.

## Background jobs
This section allows you to see if any of your jobs and workers are performing well. Just take a look at them from time to time. In recent versions of PYBOSSA when a job fails more than three times in a row, you will get notified. Check this [section](configuration.md#background-jobs-error-notifications) for more information.

## Featured Projects
In this section, admins can add/remove projects to the front page of the site.

![image](https://i.imgur.com/K9deWZo.png:width:100%)

You will see an "Add to Featured" link to add a project to the featured front page or a "Remove from Featured" to remove it.

## Categories

PYBOSSA provides by default two categories:

1.  **Thinking**: for projects where the users can use their skills to
    solve a problem (i.e., image or sound pattern recognition).
2.  **Sensing**: for projects where the users can help gathering data
    using tools like [EpiCollect](http://plus.epicollect.net) and then
    analyze the data in the PYBOSSA server.

Admins can add as many categories as they want, just type then and its description and click on the green button labeled: Add category.

![image](https://i.imgur.com/FlTowJ7.png)

!!! note
    You cannot delete a category if it has one or more projects associated with it. You can, however, rename the category or remove it when all the associated projects are not linked to the given category.

## Project's Audit log

When a project is created, deleted or updated, the system registers its actions on the server. Admins will have access to all the logged activities in every project page, in a section named **Audit log**.

![image](https://i.imgur.com/BjcJQW7.png)

The section will let you know the following information:

-   **When**: when the action was taken.
-   **Action**: which action was taken: 'created', 'updated', or
    'deleted.'
-   **Source**: if it was done the action via the API or the WEB
    interface.
-   **Attribute**: which attributes of the project has been changed.
-   **Who**: the user who took action.
-   **Old value**: the previous value before the action.
-   **New value**: the new value after the action.

!!! note:
    Only admins and users marked as *pro* can see the audit log.


