In PYBOSSA most of the domain objects are related to a project.
Therefore, you can query (or filter) a list of project IDs directly via
the API to reduce the number of queries that you need to do. This is
especially useful for Single Page Applications that only use the PYBOSSA JSON endpoints.

For example, you can get all the tasks for a list of projects like this:

    GET http://{pybossa-site-url}/api/task?project_id=[1,2,3]

That filter will return tasks for project IDs 1, 2 and 3. The same can
be done for task runs and blog posts.


