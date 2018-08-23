# Intro
This endpoint (api/helpingmaterial) allows you to add JSON and media files (images, videos or sounds) that you can use within your project to build an interactive tutorial.

Helping materials allow you to upload images via the endpoint using the multipart/form-data Content-Type.

For example, imagine that you want to add a photo of an animal and it's description, so users can easily identify it (or use it as pre-loaded
answer for classifying pictures of animals). In this case, you can do
the following (using the popular Python requests library, but you can
use any other programming language):

``` python
import requests
url = 'https://server/api/helpingpoint?api_key=YOURKEY'
# Upload a picture
files = {'file': open('test.jpg', 'rb')}
data = {'project_id': YOURPROJECT_ID}
r = requests.post(url, data=data, files=files)
# Get the created helping material
hp = r.json()
# Add the meta-data of the picture
url = 'https://server/api/helpingpoint/%s?api_key=YOURKEY' % hp['id']
info = {'popular_name': 'elephant', 'scientific_name': 'loxodonta'}
r = requests.put(url, json={'info': info})
```

You can add as many files as you want. Then, from any place you can
query the helping material endpoint to retrieve the example/tutorial
materials for helping your users.

!!! tip PBS and helping materials
     You can use PBS to add helping materials from an Excel or CSV file. Check the [documentation](pbs.md#helping-materials).

!!! note 
     Only project owners can create helping materials.
