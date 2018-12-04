# Capture data with PYBOSSA

Since version 2.10.0 PYBOSSA allows you to capture data with the crowd.

This basically means that you don't need anymore the EpiCollect+ integration (unless you want to keep using it, of course).

With PYBOSA 2.10.0 you can ask the crowd to submit any type of data via the API

## Configuring data capturing

PYBOSSA has this feature enabled by default for the following extensions:

``` json
['js', 'css', 'png', 'jpg', 'jpeg', 'gif', 'zip']
```

You can simply force a different set of extensions by using this config variable:

``` python
ALLOWED_EXTENSIONS = ['mp4', 'wav']
```

## Sending files within the taskrun

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
