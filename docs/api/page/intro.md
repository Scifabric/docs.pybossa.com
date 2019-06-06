# Intro
This endpoint (api/page) allows you to add JSON and media files (images, videos or sounds) that you can use within your project to build a headless CMS.

Pages allow you to upload images (or any allowed file) via the endpoint using the multipart/form-data Content-Type.

For example, imagine that you want to add a page for your SPA or #jamstack
solution. In this case, you can do
the following (using the popular Python requests library, but you can
use any other programming language):

``` python
import requests
url = 'https://server/api/page?api_key=YOURKEY'
# Upload a picture
files = {'file': open('test.jpg', 'rb')}
data = {'project_id': YOURPROJECT_ID, 'slug': 'aboutus'}
r = requests.post(url, data=data, files=files)
# Get the created helping material
hp = r.json()
# Add the meta-data of the picture
url = 'https://server/api/page/%s?api_key=YOURKEY' % hp['id']
info = {'structure': ['Header', 'About', 'Footer']}
r = requests.put(url, json={'info': info})
```

You can add as many pages as you want. Then, within your frontend framework
(i.e. nuxt) you can match URLs in your router to request the page's structure
from PYBOSSA. In this way, you will be able to handle structure to PYBOSSA, so
your site is more flexible than ever.

!!! note 
     Only project owners and admins can create pages.
