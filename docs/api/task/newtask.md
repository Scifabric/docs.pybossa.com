You can request a new task for the current user (anonymous or
authenticated) by:

    GET http://{pybossa-site-url}/api/{project.id}/newtask

This will return a domain Task object in JSON format if there is a task available for the user. Otherwise, it will return **None**.

You can also use **limit** to get more than 1 task for the user like
this:

    GET http://{pybossa-site-url}/api/{project.id}/newtask?limit=100

That query will return 100 tasks for the user.

!!! note
    That's the maximum of tasks that a user can get at once. If you pass an argument of 200, PYBOSSA will convert it to 100.

You can also, use **offset** to get the next tasks, if you want,
allowing you to preload:

    GET http://{pybossa-site-url}/api/{project.id}/newtask?offset=1

That query will return the next task for the user, once it solves the
previous task.

Both arguments, limit and offset can be used together:

    GET http://{pybossa-site-url}/api/{project.id}/newtask?limit=2offset=2

That will load the next two tasks for the user.

Also, you can request the tasks to be sorted by a Task attribute (like
ID, created, etc.) using the following arguments: **orderby** and
**desc** to sort them in descending order:

    GET http://{pybossa-site-url}/api/{project.id}/newtask?orderby=priority_0&desc=true

That query will return the tasks order by priority in descending order, in other words, it will return first the tasks with higher priority.


