# Analyzing your project in real-time

When you have your project running, you will want to analyze the contributions sent by the
volunteers. For doing this task, you can do it offline, with our [Enki](https://github.com/Scifabric/enki) software, or take advantage
of the PYBOSSA webhooks feature.

PYBOSSA webhooks is a notification system, that will send an HTTP POST request to another server of your
choice, sending the following data:

```json

{'fired_at':,
 'project_short_name': 'project-slug',
 'project_id': 1,
 'task_id': 1,
 'result_id': 1,
 'event': 'task_completed'} 

```

As you can see, the data specifies which task has been completed, when, and which **empty** result has been
created for you. In this way, you can ask Enki to download the task, its associated task runs and do the statistical
analysis in real time. Moreover, as PYBOSSA creates an empty result for you, you can use again enki to POST the
statistical analysis back to PYBOSSA, so you can then search through the API for example for all the pictures classified
as red.

In order to simplify your workflow, we have created a small microservice named [webhooks](https://github.com/Scifabric/webhooks), that gives you the basics to start.

While the main purpose of this microservice is to do the analysis of the results,
you can customize and fork it to do other things like:

 * Post to Twitter that your project has completed a task.
 * Upload the results to your DropBox folder by writing the results in a file.
 * Create a new task in another project, because the statistics met a given criteria.
 * Send an email with the result as an attachment, and in the body of the email the statistical analysis.
 * Give badges to users that correctly answered the task.
 * etc.

The template that we provide, only shows how you can easily 
get the most voted option for an image pattern recognition project.

## Installation

To install the microservice all you need is to run the following command (we recommend
you to use a virtual environment):

```bash
pip install -r requirements.txt
```

!!! note
    Clone or [download](https://github.com/Scifabric/webhooks) the software before proceed.

Now, copy the settings.py.template file to: **settings.py** and fill in the
information. Once you are done with this file, you'll be ready to run the
server.

!!! note 
    Be sure to have a PYBOSSA API-KEY as the analysis will be stored in the 
    PYBOSSA results table.

!!! note
    It requires a PYBOSSA server >= 1.2.0.


## Running the microservice

Now that you've the required libraries installed, running the server is as
simple as this:

```bash
python app.py
```

Then, copy the domain or IP and port where it's running and save that address in your
project's settings page, in the webhooks field. PYBOSSA will check if the webhooks server
is running. If it is not, it will fail and it will not allow you to save the URL.

## Configuring background jobs

By default, this project has disabled the creation of queues in your system. If
you expect to have lots of contributions in your project, we recommend you to
enable them.

To support queues you will need to install in your machine a Redis server.
Then, change the flag: **enable_background_jobs** to True in your settings.py
file, and restart the server. 

!!! note
    If you are already running a Redis server and queues, you can customize
    the name of your queue in the settings file. Check out the config variable:
    **queue_name**.

### Running the background jobs

Now that you have the project running background jobs, you need to process
them. This is very simple, in another terminal run the following command:

```bash
rqworker mywebhooks
```

!!! note
    If you've changed the name of the queue, please, update the previous
    command with your new queue name. That's all! Enjoy!!!

## Debugging your analysis

While you are developing the analysis module for your project, you will want to test it.
For this reason, PYBOSSA provides a way of re-running all the created webhooks, one specific, or
all the failed ones. In this way, you will be able to fix your code, without having to stop your project.

Go to your webhooks project section, and check the available options.


!!! note
    PYBOSSA sends you a **rerun** argument when doing the POST if you use any of the previous options,
    so you can handle that specific case in your code. All you have to do is check for that argument in
    the POST.

## Creating missing webhooks

Sometimes, you might start your project without the webhooks solution in mind. This will lead to a project
where you have several completed tasks, without any associated webhooks. This is because you didn't enabled the
webhooks solution, and therefore PYBOSSA didn't created it for you.

For those cases, you can use the cli.py script. It has a specific command that will allow you to create all
the missing webhooks in one row. For doing it, all you need is your project ID and then run the following command:

```bash
python cli.py create_webhooks projectID
```

Then, from your project, enable the webhooks server, and you will only have to hit the button re-run all webhooks.
This action, will enqueue all the webhooks and you will get your data analysis done!
