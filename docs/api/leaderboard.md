### Leaderboard

**Endpoint: /leaderboard/** **Endpoint:
/leaderboard/window/&lt;int:window&gt;**

*Allowed methods*: **GET**

**GET**

Shows you the top 20 contributors rank in a sorted leaderboard. If you
are logged in you will also get the rank of yourself even when you are
not visible on the top public leaderboard.

By default the window is zero, adding the authenticated user to the
bottom of the top 20, so the user can know the rank. If you want, you
can use a window to show the previous and next users taking into account
authenticated user rank. For example, you can get the previous 3 and
next 3 accessing this URL: /leaderboard/window/3.

-   **template**: Jinja2 template.
-   **title**: the title for the endpoint.
-   **top\_users**: Sorted list of leaderboard top users.

**Example output**

for logged in user JohnDoe (normally not visible in public leaderboard):

```json
{
    "template": "/stats/index.html",
    "title": "Community Leaderboard",
    "top_users": [
        {
            "created": "2014-08-17T18:28:56.738119",
            "fullname": "Buzz Bot",
            "info": {
                "avatar": "1410771548.09_avatar.png",
                "container": "user_5305"
            },
            "n_answers": null,
            "name": "buzzbot",
            "rank": 1,
            "registered_ago": null,
            "score": 54259
        },
        ... ,
        {
            "created": "2014-08-11T08:59:32.079599",
            "fullname": "JohnDoe",
            "info": {
                "avatar": null,
                "container": "user_4953"
            },
            "n_answers": null,
            "name": "JohnDoe",
            "rank": 1813,
            "registered_ago": null,
            "score": 56
        }
    ]
}
```


