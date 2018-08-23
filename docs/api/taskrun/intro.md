# Intro

TaskRuns are exactly as other domain objects with two exceptions:

1. You cannot create a taskrun without filling a few requirements.
2. You can upload files as part of it.

## Creating a TaskRun

For creating a TaskRun a project needs to be published. If the project
only allows authenticated contributions, PYBOSSA will reject the creation
of TaskRuns via the API. Then, in order to save a TaskRun you, your user,
needs to request it first. This is mandatory to avoid scripts creating hundreds
of task runs in a few minutes.

### Requesting the task

In order to request a task, all you have to do is basically an API call to any of 
the following endpoints:

http://server/api/project/id/newtask

or

http://server/project/short_name/task/ID

In the first case, you will be able to send a TaskRun only for the task that has been
returned for your user via the *newtask* endpoint. In the second one, you are in charge
to supply the task.ID. 

### Attaching a file to the TaskRun

You can create a TaskRun with an image, video, PDF, audio (or any file) by doing a POST
request with the following Content-Type: multipart/form-data.

For example, in Python you could do it like this:

``` python
import requests
import json
url = 'https://server/api/taskrun?api_key=YOURKEY'
# Upload a picture
files = {'file': open('test.jpg', 'rb')}
data = {'project_id': YOURPROJECT_ID, 'task_id': TASK_ID, 'info': json.dumps(dict(foo="bar"))}
r = requests.post(url, data=data, files=files)
```
As you can see, you can submit in one HTTP request not only the file but also some extra
info. The only requirement is to escape it, so PYBOSSA can parse it later on when the file
has been succesfully uploaded.

This feature is pretty handy if you need to send the latitude and longitude of a picture taken
by a phone. You will be able to upload the file, but also its coordinates at once.
