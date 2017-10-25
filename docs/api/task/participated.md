For the Tasks endpoint, you can also do something else, which could be pretty handy for PYBOSSA projects that are built using only Javascript (Single Page Applications) and do not want to use the /new task endpoint. 

You can use any of the previous filters for the /api/task
endpoint and add the following argument: **participated=1** to remove from the results, the tasks that the user has participated in. In this way, you will be entirely in charge of how the tasks are presented to your users. You will design how they will be delivered.

This endpoint now accepts as well the **external\_uid** parameter, as by default it identifies authenticated users, as well as anonymous users. If you are using the external UID, include it.

