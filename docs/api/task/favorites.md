Authenticated users can mark a task as a favorite. This is useful for
users when they want to see all the tasks they have done to remember them. For example, a user can mark as a favorite a picture that's beautiful and that he/she has characterized as favorited.

For serving this purpose, PYBOSSA provides the following API endpoint:

    GET /api/favorites

If the user is authenticated, it will return all the tasks the user has
marked as favorited.

To add a task as a favorite, a POST should be done with a payload of
{'task\_id': Task.id}:

    POST /api/favorites

For removing one task from the favorites, do a DELETE:

    DEL /api/favorites/task.id

Be sure to have always the user authenticated. Otherwise, the user will not be able to see it.


