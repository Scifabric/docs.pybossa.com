You can list project statistics, such as number of tasks, volunteers and overall progress via:

    GET /api/projectstats

To filter this list, for example, by project ID:

    GET /api/projectstats?project_id=[1,2,3]

To include additional hour stats, day stats and user stats for the past 2 weeks, append **full=1** to the query, for example:

    GET /api/projectstats?full=1

These additional statistics will be included in the **info** field of each object returned.

