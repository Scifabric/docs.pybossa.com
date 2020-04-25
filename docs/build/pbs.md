# Using the command line

In this section we'll learn how we can use the command line to interact with our project in a PYBOSSA server, using the command line tool: **PBS** built by Scifabric.

## PBS

**PBS** is a simple command line interface to a PYBOSSA server. The command allows you to:

* create projects, 
* add tasks from a CSV, Excel or JSON file, 
* show progress when adding tasks
* delete tasks,
* updated redundancy for tasks, 
* and update the project templates.

## Installation

PBS is available in Pypi so that you can install the software with pip:

``` bash
pip install pybossa-pbs
```

!!! note
    We recommend to use virtual environments to install new Python libraries and packages, so please, before installing the PBS command line tool consider using a virtual environment.

If you have all the dependencies, the package will be installed, and you will be able to use it from the command line. The command is **pbs**.

## Configuring PBS

By default, PBS does not need a config file. However, you will have to specify for every command the server and your API key to add tasks, create a project, etc. For determining the server and API key
that you want to use, all you have to do is pass it as an argument:

``` bash
pbs --server http://server.com --api-key yourkey subcommand
```

If you work with two or more servers, then, remembering all the keys, and server URLs could be problematic, as well as you will be leaving a trace in your BASH history file. For this reason, pbs has a
configuration file where you can add all the servers that you are
working with.

To create the config file, all you have to do is creating a
**.pybossa.cfg** file in your home folder:

``` bash
cd ~
vim .pybossa.cfg
```

The file should have the following structure:

``` python
[default]
server: https://theserver.com
apikey: yourkey
```

If you are working with more servers, add another section below it. For example:

``` python
[default]
server: https://theserver.com
apikey: yourkey

[yourserver]
server: https://yourserver.org
apikey: yourkeyinyourserver.org
```

By default, pbs will use the credentials of the default section, so you don't have to type anything to use those values. However, if you want to do actions on another server, all you have to do is the following:

``` bash
pbs --credentials yourserver --help
```

That command will use the values of the yourserver section.

## Project

This section shows how you can handle a project using PBS.

### Creating a project

Creating a project is very simple. All you have to do is create a file
named **project.json** with the following fields:

``` javascript
{
    "name": "Flickr Person Finder",
    "short_name": "flickrperson",
    "description": "Image pattern recognition"
}
```

If you use the name **project.json** you will not have to pass the file
name via an argument, as it's the name used by default. Once you have the file created, run the following command:

``` bash
pbs create_project
```

That command should create the project. If you want to see all the
available options, please check the **--help** command:

``` bash
pbs create_project --help
```

### Updating templates

Now that you have added tasks, you can work in your templates. All you have to do to add/update the templates of your project is running the following command:

``` bash
pbs update_project
```

That command needs to have in the same folder where you are running it, the following files:

- template.html
- results.html
- long_description.md
- tutorial.html

If you want to use another template, just use these arguments:

``` .bash
pbs update_project --template /tmp/template.html
```

If you want to see all the available options, please check the
**--help** command:

``` bash
pbs update_project --help
```

### Using an external JavaScript file

Since PBS >= 2.3.0, PBS will check for an external JavaScript file named *bundle.js* or *bundle.min.js*. If any of those files exist, then, they will be added at the bottom of your template (like you have been doing so far with your projects).

This solution allows you to use for example webpack plus babel to transpile your code, minimize it and add it to your PYBOSSA project.

To use this solution, just transpile to a file named bundle.js or bundle.min.js.

!!! note
    If there's a minified version of the file, bundle.min.js, that file will always be used instead of bundle.js. 

### Auto-updating while developing a PYBOSSA project

At some point, you will end up running lots of PBS update_project commands, as you will be using your chosen editor for fixing CSS, HTML or JavaScript. For these scenarios, PBS comes with a handy flag: **--watch**. This argument will tell PBS to run the update_project command automatically when bundle.js, bundle.min.js, template.html, tutorial.html or long_description.md are modified in the file system. As simple as that.

You can run it like this:

```bash
    pbs update_project --watch
```

And the output will be similar to this:

![GIF of pbs in action](https://i.imgur.com/QoYC4oV.gif)


!!! tip "Using webpack and PBS"
    This also works with bundle.js files. Thus, you can have webpack transpiling automatically your code, and PBS will update your project with the new code. Cheers :beers:



## Tasks

This section shows how you can handle project's tasks.

### Adding tasks to a project

Adding tasks is very simple. You can have your tasks in these formats:

- JSON
- CSV
- Excel (xlsx from 2010. It imports the first sheet)
- PO (any po file that you want to translate)
- PROPERTIES (any PROPERTIES file that you want to translate)

Therefore, adding tasks to your project is as simple as this command:

``` bash 
pbs add_tasks --tasks-file tasks_file.json
```

If you want to see all the available options, please check the
**--help** command:

!!! note
    By default, PYBOSSA servers use a rate limit for avoiding abuse of the API. For this reason, you can only do usually 300 requests per every 15 minutes. If you are going to add more than 300 tasks, pbs will detect it and warn you, auto-enabling the throttling for you to respect the limits. Please, see [the rate-limiting section](api.md#rate-limiting) for more details.

``` bash
pbs add_tasks --help
```


### Updating tasks redundancy from a project

If you need it, you can update the redundancy of a task using its ID or all the tasks skipping the ID. For example, to update the redundancy of one task to 5:

```bash
    pbs update-task-redundancy --task-id 34234 --redundancy 5
```

To update all of them:

```bash
    pbs update-task-redundancy --redundancy 5
```

!!! note
    Without the **--redundancy** argument it will revert the redundancy to the default value: 30.

This last command will confirm that you want to update all the tasks.

If you want to see all the available options, please check the **--help** command:

```bash
    pbs update-task-redundancy --help
```

### Deleting tasks from a project

If you need it, you can delete all the tasks from your project, or only one using its task.id. For removing all the tasks, all you've to do is
run the following command:

``` bash
pbs delete_tasks
```

This command will confirm that you want to delete all the tasks and
associated task_runs.

If you want to see all the available options, please check the
**--help** command:

``` bash
pbs delete_tasks --help
```

!!! warning
    Only tasks that are not associated with a result will be deleted.


### Getting out of the API context

PYBOSSA by default returns first your projects, meaning that if you want to work on a project that you don't own, it will return an error as the project will not be found. For solving this issue you have two options:

 * In the config file, by adding a new flag: all:1
 * On the command line, passing the --all=1 flag

## Helping Materials

This section shows how you can handle project's helping materials.

### Adding helping materials to a project

Adding helping materials is very simple. You can have your materials in three formats:

 * JSON
 * Excel (xlsx from 2010. It imports the first sheet)
 * CSV

Therefore, adding helping materials to your project is as simple as this command:

```bash
    pbs add_helpingmaterials
    --helping-materials-lfile file.xlsx --helping-type xlsx
```

If you want to see all the available options, please check the **--help** command:

!!! note
    By default, PYBOSSA servers use a rate limit for avoiding abuse of the API. For this reason, you can only do usually 300 requests per every 15 minutes. If you are going to add more than 300 tasks, pbs will detect it and warn you, auto-enabling the throttling for you to respect the limits.


!!! tip
    PYBOSSA helping materials allow you to upload media files like videos, images, or sounds to support your project tutorials. The command line PBS will check for a column in your file with the name *file_path* so it can upload it first to the server. Please, be sure that the file (or files) path is reachable from the helping materials file.

```bash
    pbs add_helpingmaterials --help
```
