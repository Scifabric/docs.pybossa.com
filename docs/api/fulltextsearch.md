You can use the full-text search engine of PYBOSSA using the RESTful API. This feature is available for the **info** fields of the domain objects, as that's where you will be storing the information.

PYBOSSA only searches within the first level keys (as seen before) of the JSON data stored in the info field. 

Full-text search is amazing because it means that the server will understand verbs, plurals, singulars, etc. By default, PYBOSSA uses English for the searches. You can customize this behavior using any of the supported languages by PostgreSQL changing the settings_local.py config variable: 

```python
   FULLTEXTSEARCH_LANGUAGE = 'spanish'.
```

If you want to search using this method, just add the following argument:

    info=key1::value1&fulltextsearch=1

That will return every object in the DB that has a key equal to key1 and contains he value the word value1.

Another option could be the following:

    info=key1::value1|key2:word1%26word2&fulltextsearch=1

This second query will return objects that have the words word1 and
word2. It's important to escape the & operator with %26 to use the and operator.

When you use the fulltextsearch argument, the API will return the
objects enriched with the following two fields:

-   **headline**: The matched words of the key1::value1 found, with
    &lt;b&gt;&lt;/b&gt; items to highlight them.
-   **rank**: The ranking returned by the database. Ranking attempts  to measure how relevant documents are to a particular query, so that when there are many matches the most relevant ones can be shown first.

Here you have an example of the expected output for an api call like
this:

    /api/task?project_id=1&info=name::ipsum%26bravo&fulltextsearch=1

```json
[
  {
    "info": {
      "url": "https://domain.com/img.png",
      "name": "Lore ipsum delta bravo",
    },
    "n_answers": 1,
    "quorum": 0,
    "links": [
      "<link rel='parent' title='project' href='http://localhost:5000/api/project/1'/>"
    ],
    "calibration": 0,
    "headline": "Lore <b>ipsum</b> delta <b>bravo</b>",
    "created": "2016-05-10T11:20:45.005725",
    "rank": 0.05,
    "state": "completed",
    "link": "<link rel='self' title='task' href='http://localhost:5001/api/task/1'/>",
    "project_id": 1,
    "id": 1,
    "priority_0": 0
  },
]
```

!!! note
    When you use the fulltextsearch API, the results are always sorted by rank, showing first the most relevant ones to your query.


!!! note
    We use PostgreSQL ts_rank_cd with the following configuration:
    ts_rank_cd(textsearch, query, 4). For more details check the official
    documentation of PostgreSQL.

If the search does not find anything, the server will return an empty JSON list []

