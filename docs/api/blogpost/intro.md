# Intro
This endpoint (api/blogpost) allows you to add JSON and media files (images, videos or sounds) that you can use within your project to build an interactive tutorial.

Blogposts allow you to upload images via the endpoint using the multipart/form-data Content-Type.

For example, imagine that you want to add a photo to your blogpost.
In this case, you can do the following (using the popular Python requests library, but you can
use any other programming language):

``` python
import requests
url = 'https://server/api/blogpost?api_key=YOURKEY'
# Upload a picture
files = {'file': open('test.jpg', 'rb')}
data = {'project_id': YOURPROJECT_ID, 'title': 'Title', 'body': 'body'}
r = requests.post(url, data=data, files=files)
```

!!! note 
     Only project owners can create blogposts.
