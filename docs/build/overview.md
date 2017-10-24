# Quickstart: Creating a Project

This is a short guide on how you can create a PYBOSSA project. You may wish to start with the [step by step tutorial](tutorial.md); which walks through creating a simple photo classification project if you want to understand all the details about how a project works.

First of all, we have to create a project for the project. To create a project, you will have to provide the following information:

1. **Name**,
2. **Short name** or **slug**, and
3. **Description**

The **slug** or **short name** is a shortcut for accessing the project
via the web (short URLs like this http://domain.com/project/slug).

The **description** is a short sentence that will be used to describe
your project (think about it as a Tweet long description).

A project can be created using two different methods:

- web interface, or
- API interface.

## Using the Web Interface

Creating a project using the web interface involves four steps:

1. Building the project,
2. Import the tasks using one of the available [task importers](intro.md#adding-tasks-to-a-project),
3. Write the task-presenter for the users, and
4. Publish the project.

### Creating the project

To create a project using the web interface you have
to: 

#### Create a PYBOSSA account

You can create an account filling a form.

![PYBOSSA Register](http://i.imgur.com/MMnUQr7.png)

If PYBOSSA has Twiter, Facebook or Google authentication methods enabled, you will be able to create an account using them. See the [documentation](../installation/configuration.md) for more information about these alternatives.

![PYBOSSA sign-in methods](http://i.imgur.com/GxhfjGL.png)

#### Creating the project 
Once you have an account, click in **create the ** link of the navigation bar. After clicking on the previous link, you will have to fill in a    form with the fundamental information to create your project:
    1.  **Name**: the full name of your project, i.e., *Flickr Person
        Finder*.
    2.  **Short Name**: the *slug* or short name used in the URL for         accessing your project, i.e., *flickrperson*.
    3.  **Long Description**: A *long* description where you can use
        Markdown to format the description of your project. This field
        is usually used to provide information about the project, the
        developer, the researcher group or institutions involved in the
        project, etc.

![PYBOSSA Create link](http://i.imgur.com/Js4YgVg.png)

!!! note
    PYBOSSA usually provides two Project Categories by default: *thinking* and *sensing*. The *thinking* category represents the standard PYBOSSA project where users contribute helping with their skills. *Sensing* category refers to projects that are using volunter sensing tools like EpiCollect or Raspberry Pi with PYBOSSA for gathering data.

Once you have filled all the fields, click in the **Create the project** button, and you will have created your first project :thumbsup:

After creating the project, you should be redirected to the **Settings'**  project page, where you will be able to customize your project by adding some extra information or changing some settings. There, you will find a form with the same fields as in the previous step (just in case you've changed your mind and wanted to change any of them) plus the following:

-  **Description**: A **short** description of the project, e.g., *A    project to classify cancer cells*. By default, this field is automatically populated with the information that you provided in the **Long description** field.
-  **Allow Anonymous Contributors**: By default, anonymous and authenticated users can participate in all the projects. However, you can change it only to allow authenticated volunteers to participate.
-  **Password**: If you want to control who can access your project, you can set a password here to share with those you allow to do it. If you leave it blank, then no password will protect your project.
-  **Category**: Select a category that fits your project. Categories
   are added and managed by the server administrators.

!!! note
    Also, you will be able to select and upload a **image** from your local computer to set it as the project image throughout the server.

![PYBOSSA Project Update page](http://i.imgur.com/UbSOAcZ.png)

### Importing the tasks via the built-in CSV Task Importer

Tasks can be imported from different services like Dropbox or Amazon S3 via the importers. To use one, just do the following:  
1. Navigate to your project's page (you can directly access it using
   the *slug* project name: <http://server/project/slug>).
2. Click in the **Tasks** section -on the left side local navigation
   menu:

![Image](http://i.imgur.com/nauht7l.png)

3. And click again on the **Import Tasks** card. After clicking on it, you will see several options. The first ones are for using the different kinds of importers supported by PYBOSSA: Amazon S3, Twitter, Dropbox, Flickr, Youtube, Google Spreadsheet, CSV URL, and EpiCollect Plus.

![Image](http://i.imgur.com/eWBxSyS.png)

For example, the Flickr importer will allow importing a Flickr album by typing its ID or if you have an account, by logging into Flickr and
showing your public (and creative commons licensed) albums:

![Image](http://i.imgur.com/lF9LJVO.jpg) 

Select one of the albums, click import and all the pictures will be
imported as tasks for your PYBOSSA project. As simple as that :ok_hand:.

The other importers are very similar. In most cases, you'll provide a URL to the resource, like for the CSV and Google Spreadsheet importer, while the Dropbox, Amazon S3, Twitter, Youtube, and EpiCollect Plus importers will have a friendly interface to import data automagically for you.

!!! note
    If you're trying to import from a Google Spreadsheet, ensure the file is accessible to everyone via the Share option, choosing: "Public on the web - Anyone on the Internet can find and view."


!!! note
    Your spreadsheet/CSV file must contain a header row. All the fields in the CSV will be serialized to JSON and stored in the **info** field. If your field name is one of **state**, **quorum**, **calibration**,    **priority_0**, or **n_answers**, it will be saved in the respective     columns. Your spreadsheet must be visible to the public or everyone with an URL.

In the Task Importer section, you'll also find other pre-loaded Google Spreadsheets URLs. Those templates are examples that you can use
to learn how to create your spreadsheets and import data for image,
sound, video, pdf mining and mapping projects.

![Image](http://i.imgur.com/eGwKDpB.png)

By using these templates, you'll be able to learn the structure of the
tasks, and directly re-use the task-presenter templates that know the
structure (name of the columns) for presenting the task.

Additionally, you can re-use the templates by downloading the CSV files from Google Docs, or even copying them to your own Google Drive account (click in *File* :arrow_right: *Make a copy* in the Google Doc Spreadsheet). Scifabric provides the following templates:

- [Image Pattern Recognition](https://docs.google.com/spreadsheet/ccc?key=0AsNlt0WgPAHwdHFEN29mZUF0czJWMUhIejF6dWZXdkE&usp=sharing#gid=0)
- [Sound Pattern Recognition](https://docs.google.com/spreadsheet/ccc?key=0AsNlt0WgPAHwdEczcWduOXRUb1JUc1VGMmJtc2xXaXc#gid=0)
- [Video Pattern Recognition](https://docs.google.com/spreadsheet/ccc?key=0AsNlt0WgPAHwdGZ2UGhxSTJjQl9YNVhfUVhGRUdoRWc#gid=0)
- [Geo-coding](https://docs.google.com/spreadsheet/ccc?key=0AsNlt0WgPAHwdGZnbjdwcnhKRVNlN1dGXy0tTnNWWXc&usp=sharing)
  and
- [PDF transcription](https://docs.google.com/spreadsheet/ccc?key=0AsNlt0WgPAHwdEVVamc0R0hrcjlGdXRaUXlqRXlJMEE&usp=sharing).

!!! tip
    If you import the same URL again, only new records will be added to the project.

### Importing the tasks from an EpiCollect Plus Public Project

[EpiCollect](http://plus.epicollect.net) provides a web tool for the
generation of forms for many kinds of mobile data collection projects.

Data can be collected using multiple mobile phones running either the Android Operating system or the iPhone (using the EpiCollect mobile app) and all data can be synchronized from the phones and viewed centrally (using Google Maps) via the Project website or directly on the phones.

EpiCollect can help you to recollect data samples according to a form that could include multimedia like photos. Moreover, EpiCollect can geolocate the data sample as it supports the built-in GPS that all modern smartphones have.

For example, you can create an EpiCollect project where the form will ask the user to take a picture of a lake, geo-locate it automatically via the built-in smartphone GPS and upload the image to the EpiCollect server. If the user does not have Internet access at that moment, the user will be able to synchronize the data afterward, i.e., when the user has access to an Internet WIFI hotspot.

PYBOSSA can automatically import data from a public EpiCollect Plus project that you own or that it is publicly available on the
web site. Then you will be able to validate, analyze, etc. the data that has been obtained via EpiCollect.

If you want to import the data points submitted to a **public**
EpiCollect project, you will have to follow the next steps:

1. Navigate to your project's page (you can directly access it using
   the *slug* project name: <http://server/project/slug>).
2. Click in the **Tasks** section -on the left side local navigation
   menu.
3. And click on the **Import Tasks** button. After clicking on it you
   will see several different options.
4. Click on the **Use an EpiCollect Project** one. 
    ![image](http://i.imgur.com/A50La7O.png)
5. Then, type the **name of the EpiCollect project** and the name of the **form** that you want to import and click on the import button.

All the data points should be imported now in your project.

!!! note
    EpiCollect projects will be gathering data mostly all the time, for this reason, if you import again the same EpiCollect project, only  **new data points** will be imported. This feature will allow you to easily add new data points to the PYBOSSA project without having to do anything special.

### Importing the tasks from a Flickr photo set

PYBOSSA also allows importing tasks for projects based on images (like image pattern recognition ones) directly from a [Flickr](https://www.flickr.com/) [set]https://www.flickr.com/help/photos/#150321191) (also called
album).

When importing tasks from a Flickr set, a new task will be created for each of the photos in the specified set. The tasks will include the
following data about each picture (which will be later available to be
used in the task presenter):

- title: the title of the photograph, as it appears on Flickr.
- URL: the URL to the raw .jpg image, in its original size.
- url_b: the url to the image, 'big sized.
- url_m: the url to the image, 'medium' sized.
- link: a link to the photo page on Flickr (not to the raw image).

You can import tasks from a Flickr photo set (a.k.a. album) in either of the following ways: using your Flickr account, or by typing the album ID.

The easiest one is to give the PYBOSSA server permission to access your Flickr list of albums. To do so, you'll have to log in to your Flickr
account by clicking the "Log in Flickr" button. Then you'll be
redirected to Flickr, where you will be asked if you want to allow
PYBOSSA to access your Flickr information. If you say yes, then you'll be again redirected to PYBOSSA, and you'll see all of your albums. Choose one of them and then click the "Import" button to get all the photos created as tasks for your project.

!!! note
    Next time you try to import photos using the Flickr importer, you'll see the albums for your account again. If you don't want PYBOSSA to access them anymore, or just want to use another Flickr account, then click "Revoke access."


Another option to import from a Flickr album is by specifying the ID of the set (collection) directly. This option is a bit more advanced, but  it allows you to import from a photo set that you don't own (although, it will have to be public. Also check the rights of the photos on it!). Another advantage is that you don't need to log in to Flickr, so you don't even need to have a Flickr account.

These are the steps:

1. Navigate to your project's page and click in the **Tasks** section.
2. Then click on the **Import Tasks** button, and select the **Flickr
   importer**.
3. Type the ID of the Flickr set you want to import the photos from, then click on the import button.

![Image](http://i.imgur.com/UZRBj8y.png)

If you cannot find the ID or don't know which one it is, just browse to the Flickr photo set and check the URL. Can you see that last long number right at the end of it? That's what you're looking for!

![Imge](http://i.imgur.com/h6qNDX2.png)

Just like with the other importers, each task will be created only once, even if you import twice from the same Flickr set (unless you add new photos to it, of course!).

!!! note
    You will need to make sure that every photo belonging to the set has the visibility set to public, so the PYBOSSA server can then access and present them to the volunteers of your project.


### Importing the tasks from a Dropbox account

You can import tasks from arbitrary data hosted on a Dropbox account with the Dropbox importer. When you import tasks in this way, the following information will be added to the info field of each task, available later to be used in the task presenter of the project:

- filename: just it, the name of the file you're importing as a task.
- link: the link to the Dropbox page showing the file.
- link_raw: the link to the raw file served by Dropbox. This is the
  one you'll have to use if you want to direct link to the file from
  the presenter (e.g., for using an image in a <img> tag, you'd
  do: <img src=task.info.link_raw>).

In addition to this generic information, the Dropbox importer will also recognize some files by their extension and will attach some extra information to them.

For pdf files (.pdf extension), the following fields will be obtained
too:

- pdf_url: direct link to the raw pdf file, with CORS support.

For image files (.png, jpg, .jpeg and .gif extensions) the following
data will be available:

- url_m: the same as link_raw
- url_b: the same as link_raw
- title: the same as the filename

For audio files (.mp4, .m4a, .mp3, .ogg, .oga, .webm and .wav
extensions):

- audio_url: raw link to the audio file, which can be used inside an
  HTML 5 &lt;audio&gt; tag and supports CORS.

For video files (.mp4, .m4v, .ogg, .ogv, .webm and .avi extensions):

- audio_url: raw link to the video file, which can be used inside an
  HTML 5 &lt;video&gt; tag and supports CORS.

The tasks created with the Dropbox importer are ready to be used with the template project presenters available in PYBOSSA, as they include the described fields.

Thus, importing your images from Dropbox will allow you to use the image pattern recognition template with them immediately. If you import videos, audio files or PDFs  you will also be able to use the presenter templates for video pattern recognition, sound pattern recognition or documents transcription, respectively, with no additional modifications and have them working right away (as long as the files have any of the mentioned file extensions, of course).

For using this importer, just follow these are the steps:

1. Navigate to your project's page and click in the **Tasks** section.
2. Then click on the **Import Tasks** button, and select the **Dropbox importer**.
3. Click on the "Choose from Dropbox" icon. You will be asked your    Dropbox account credentials. Then select as many files as you want:
    ![Image](http://i.imgur.com/dsgM0Tg.png)
4. You can repeat step 3 as many times as you want, and more files will be added to your import. Then, click on "Import".

### Importing the tasks from a Twitter account or search result

Another option for importing tasks is using the built-in Twitter
importer. It allows importing tweets as tasks from either a specified
Twitter user account, or from the results returned from a search to the Twitter search API.

Tasks imported with it will have the tweet data attached to their info field, and can later be used from within the task presenter. This data
is a direct transcription of the data returned by the Twitter API, in
particular a [Tweet](https://dev.twitter.com/overview/api/tweets)
object.

Please notice that the values returned by the Twitter API may vary.
However, the following fields are guaranteed to be always included in the info field of the tasks:

- created_at: the date and time the tweet was published.
- favorite_count: number of times the tweet has been marked as
  'favorite.'
- retweet_count: number of times the tweet has been retweeted.
- coordinates: geographic coordinates of the place the tweet was published.
  from. Note that this is not always available for every tweet.
- tweet_id: the internal ID handled by Twitter to identify this
  tweet.
- user: an [object](https://dev.twitter.com/overview/api/users) with
  information about the tweet author, as returned by the Twitter API.
- text: the actual content of the tweet.

Also, an extra field "user_screen_name" has been added to the
info field:

- user_screen_name: the screen name (or 'handle') of the author of
  the tweet.

For more information, please refer to the [Twitter](https://dev.twitter.com) documentation. 

!!! warning
    When importing tweets from a search, retweets will be ignored!


So, to import tasks with the Twitter importer, do as follows:

1. Navigate to your project's page and click in the **Tasks** section.
2. Then click on the **Import Tasks** button, and select the **Twitter importer**:
3. You can provide your own Twitter credentials and make API requests on behalf of them, or use the credentials provided by us. (The later only allows to import the number of tweets returned by a single Twitter API call, which is 100 for searches and 200 for user
   timelines.)
4. Fill in the two fields you will find in the form. The first one is the source of your tweets. If you want them to be imported from a user account, then write it with the "@" symbol, like "@PYBOSSA". If you just want to import tweets containing a word on them (or a #hashtag), then type it there. The second field is for you to specify how many tweets you want to import. You can import as many as you want!

Finally, click on the "Import" button, and you are done:

![Image](http://i.imgur.com/l5PG2WX.png)

## Importing tasks from an Amazon S3 bucket

Tasks can be imported from data hosted on the Amazon S3 service.
Similarly to the Dropbox importer, these tasks can use different kind of data, like images, videos, audios, PDF files, etc. hosted on any S3
bucket.

The S3 importer will work pretty much the same as the Dropbox one. When using it, the created tasks will contain the following data in the info field:

- filename: just it, the name of the file you're importing as a task.
- link: the link to the raw file served from Amazon S3.
- URL: same as the above.

In addition to this generic information, the S3 importer will also
recognize some files by their extension and will attach some extra information to them.

For pdf files (.pdf extension), the following field will be obtained
too:

- pdf_url: direct link to the raw pdf file.

For image files (.png, jpg, .jpeg and .gif extensions) the following
data will be available:

- url_m: the same as the link.
- url_b: the same as the link.
- title: the same as the filename.

For audio files (.mp4, .m4a, .mp3, .ogg, .oga, .webm and .wav
extensions):

- audio_url: raw link to the audio file, which can be used inside an
  HTML 5 <audio/> tag.

For video files (.mp4, .m4v, .ogg, .ogv, .webm and .avi extensions):

- audio_url: raw link to the video file, which can be used inside an
  HTML 5 <video/> tag.

The tasks created with the S3 importer are ready to be used with the
template project presenters available in PYBOSSA, as they include the described fields.

Thus, importing your images from S3 will allow you to use immediately the image pattern recognition template with them; importing videos, audio files or PDFs with the S3 importer will also grant you to use the presenter templates for video pattern recognition, sound pattern recognition or documents transcription, respectively, with no additional modifications and have them working right away (as long as the files have any of the mentioned file extensions, of course).

Importing from an S3 bucket requires that the bucket visibility is set
to *public* so its content can be seen and listed by PYBOSSA. To make a bucket public, go to your AWS management console and select the S3 service. Then select the bucket you want to make public and click on "Properties." Click on "Add more Permissions" and add a new one with "Grantee: Everyone" and the "List" checkbox selected, like in the following image:

![Image](http://i.imgur.com/FuN9XAS.png)

You may also need to enable CORS in the bucket. In the same menu as above, click on "Edit CORS Configuration" and configure it. You can
learn more [here](http://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html).

Finally, you need to make sure that every file inside the bucket that
you want to use in a task has a *public* link too. Go to the bucket
content and select the files. Then click on "Actions" and select "Make
Public". Your files will now be visible for everyone, including a
PYBOSSA server.

![image](http://i.imgur.com/AHBVQCk.png)

Once your S3 bucket is ready, you can follow these steps to import tasks from it:

1. Navigate to your project's page and click in the **Tasks** section.
2. Then click on the **Import Tasks** button, and select the **S3
   importer**.
3. Type the name of the bucket from which you will be importing your tasks and click on "Search in the bucket." If you followed the steps above and your bucket is public, you will see a list of the items it contains. Select as many as you want:

    ![image](http://i.imgur.com/6RAMqd9.png)

4. When you're ready, click on "Import."

### Importing the tasks from Youtube

Tasks can be imported from Youtube. Currently, the importer supports importing from Youtube with:

- Playlists

When importing the video, the importer parses all videos information and creates tasks with info fields:

- video_url: the URL of the youtube video which can be embedded in
  the task form.
- oembed: embeddable code for the (old) PYBOSSA video templates.

The tasks created with the Youtube importer are ready to be used with the youtube and video templates.

### Flushing all the tasks

The project settings gives you an option to automatically **delete all
the tasks and associated task runs** from your project.

!!! danger
    This action cannot be un-done, so please, be sure that you want to actually, delete all the tasks.


!!! warning
    This action will only allow you to delete tasks that are not associated with a result. When a result is created, that task and its task runs cannot be deleted so the volunteers can always have access to their contributions.


If you are sure that you want to flush all the tasks and task runs for
your project, go to the project page (http://server/project/slug/tasks/) and click in the **Settings** option of the left local navigation menu:

![image](http://i.imgur.com/nauht7l.png)

Then, you will see that there is a subsection called: **Task Settings** and a button with the label: **Delete the tasks**. Click on that button and a new page will be shown:

![image](http://i.imgur.com/DKPV6dc.png)

As you can see, a **red warning alert** is shown, warning you that if
you click on the **yes** button, you will be deleting not only the
project tasks, but also the answers (task runs) that you have
recollected for your project. Be sure before proceeding that you want to delete all the tasks. After clicking on the **yes** button, you will see that all the tasks have been flushed.

### Creating the Task Presenter

Once you have the project and you have imported some tasks, you can start working with the task-presenter, which will be the web project that will get the tasks of your project, present them to the volunteer and save the answers provided by the users.

If you have followed all the steps described in this section, you will
be already on the page of your project, however, if you are not, you only need to access your project URL to work with your project. If  your project *slug* or *short name* is *flickrperson* you will be able to access the project managing options in this URL:

    http://PYBOSSA-SERVER/project/flickrperson

!!! note
    You need to be logged in. Otherwise, you will not be able to modify the project.

Another way of accessing your project (or projects) is clicking on your *username* (at the navbar) and select the *My Projects* item from the drop down menu. From there you will be able to manage your projects:

![image](http://i.imgur.com/3S497Ct.png)

![image](http://i.imgur.com/9sO21Zd.png)

Once you have chosen your project, you can add a task-presenter by
clicking on the **Tasks** local navigation link, and then clickickin on  the button named **Editor** under the **Task Presenter** box.

![image](http://i.imgur.com/nauht7l.png)

After clicking this button, a new web page will be shown where you
can choose a template to start coding your project, so you don't have to start from scratch.

![image](http://i.imgur.com/psC5m6Q.png)

After choosing one of the templates, you will be able to adapt it to fit
your project needs in a web text editor.

![image](http://i.imgur.com/g9gAvWw.png)

Click on the **Preview button** to get an idea of how it will look
like your task-presenter.

![imae](http://i.imgur.com/DsDDBia.png)

We recommend reading the [Step by step tutorial](tutorial.md) as you will understand how to create the task presenter, which is basically adding some HTML skeleton to load the task data, input fields to get the answer from the users, and some JavaScript to make it work.

### Publishing the project

After completing the previous three steps, your project will be almost ready. The final step is to publish it, because now it will still be a draft, and it will be hidden to everyone but you (and admins).

When your project is a draft, you can contribute to it, and the answers (task runs) and results will be stored in the database so you can have access to them (and test the webhooks solution if you want to do real-time analysis). However, in the moment of publishing the project all the task runs and results (as well as the webhooks log entries) will be flushed, so don't be afraid and try it as much as you can until you are sure that everything works as expected. Once you think the project is ready for the world to see it, just click on the Publish button:

![image](http://i.imgur.com/A7m4aa6.png)

!!! note
    Publishing a project *cannot* be undone, so please double check everything before taking the step.


!!! note
    You can allow other users to give you feedback and let them try and see your project before it has been published. To do it so, just protect it with a password, and people will be able to access it (as long as they have the password, of course).

After publishing it, you will be able to access your project using the
slug, or under your account in the *Published* projects section.

Also, results will begin to be created every time a task is completed.
Enjoy!

## Using the API

Creating a project using the API involves these steps:

1. Create the project,
2. Create the tasks for the project, and
3. Create the task-presenter for the users.
4. Publish it. This needs to be done via the web interface.

### Creating the project

You can create a project via the API URL **/api/project** with a POST request (See [api](api.md)).

You have to provide the following information about the project and
convert it to a JSON object (the actual values are taken from the
[Flickr Person demo project](http://github.com/Scifabric/app-flickrperson)):

``` json
name = u'Flickr Person Finder'
short_name = u'FlickrPerson'
description = u'Do you see a human in this photo?'
info = { 'task_presenter': u'<div> Skeleton for the tasks</div>' }
data = dict(name = name, short_name = short_name, description = description, info = info, hidden = 0)
data = json.dumps(data)
```

Flickr Person Finder, which is a **demo template** that **you can
re-use** to create your own project, simplifies this step by using a
simple file named **project.json**:

``` Javascript
{
"name": "Flickr Person Finder",
"short_name": "flickrperson",
"description": "Image pattern recognition",
}
```

The file provides the basic configuration for your project.

### Adding tasks

As in all the previous steps, we are going to create a JSON object and
POST it using the following API URL **/api/task** to add tasks
to a project that you own.

For PYBOSSA all the tasks are JSON objects with a field named **info** where the owners of the project can add any JSON object that will represent a task for their project. For example, using again the [Flickr Person demo project](http://github.com/Scifabric/app-flickrperson) template, we need to create a JSON object that should have the link to the photo that we want to identify:

``` python
info = dict (link=photo['link'], 
             url=photo['url_m'],
             question='Do you see a human face in this photo?')
data = dict (project_id=project_id,
             state=0,
             info=info,
             calibration=0,
             priority_0=0)
data = json.dumps(data)
```

!!! note
    'url_m' is a pattern to describe the URL to the **m** medium size of the photo used by Flickr. It can be whatever you want, but as we are using Flickr, we use the same patterns for storing the data.

The most important field for the task is the **info** one. This field
will be used to store a JSON object with the required data for the task. As [Flickr Person](https://github.com/Scifabric/app-flickrperson) is trying to figure out if there is a human or not in a photo, the provided information is:

1. the Flickr web page posting the photo, and
2. the direct URL to the image, the <img src> value.

The **info** field is a free-form field that can be populated with any
structure. If your project needs more fields, you can add them and use the format that best fits your needs.

These steps are usually coded in a script. The Flickr Person
Finder projects provides a template for the task-creator that can be
re-used without any problems (check the createTasks.py script).

!!! note 
    **The API request has to be authenticated and authorized**. You can get an API-KEY creating an account on the server, and checking the API-KEY created for your user, check the profile account (click on your user name) and copy the field **API-KEY**.

    This API-KEY should be passed as a POST argument like this with the previous data:

    [POST] <http://domain/api/task/?api_key=API-KEY>


One of the benefits of using the API is that you can create tasks
polling other web services like Flickr, where you can use an
API. Once we have created the tasks, we will need to create the
task-presenter for the project.

### Creating the Task Presenter

The task-presenter is usually a template of HTML and JavaScript that will present the tasks to the users, and save the answers in the
database. The [Flickr Person demo project](http://github.com/Scifabric/app-flickersperson) provides a template which has a <div/> to load the input files, in this case the photo, and another <div/> to load the action buttons that the users will be able to press to answer the question and save it in the database. Please, check the [tutorial](tutorial.md) for more details about the task-presenter.

As we will be using the API for creating the task presenter, we will have to create an HTML file in our computer, read it from a
a script, and post it into PYBOSSA using the API.

Once the presenter has been posted to the project, you can edit it
locally with your editor, or using the PYBOSSA interface (see
previous section).

!!! note
    **The API request has to be authenticated and authorized**. You can get an API-KEY creating an account on the server, and checking the API-KEY created for your user, check the profile account (click on your user name) and copy the field **API-KEY**.
    
    This API-KEY should be passed as a POST argument like this with the previous data: [POST] <http://domain/api/project/?api_key=API-KEY>

### Using PYBOSSA API from the command line

While you can use your preferred programming language to access the API, we recommend you to use the [PYBOSSA PBS command line
tool](https://github.com/Scifabric/pbs) as it simplifies the usage of
PYBOSSA for any given project.

Creating a project is as simple as creating a project.json file and then
run the following command:

``` bash
pbs --server server --api-key yourkey create_project 
```
Please, read the section [pbs](pbs.md) for more details.
