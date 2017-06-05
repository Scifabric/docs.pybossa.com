Importer interface
==================

Task importers are currently located in importers.py; each gets a class,
which should inherit from BulkTaskImport and provide the following
public interface:

-   importer\_id
-   tasks()
-   count\_tasks()
-   import\_metadata()

importer\_id is the name of the importer; any of the supported
importers: 'csv', 'gdocs', 'epicollect', 'flickr', 'dropbox', 'twitter',
's3' and 'youtube'.

tasks() should generate a list of tasks.

count\_tasks() should return the number of tasks that will be created.
This is because trying to import a large number of tasks (200 or more)
will be done as a background job.

import\_metadata() may return any information about the tasks that are
going to be imported. This is used for the autoimporters, and the
information returned by this method is stored and available to be used
by the next autoimport execution.

These classes are intended for private use within the importers.py
module. New ones can be created here to handle different kind of
importing mechanisms. The module exposes the public class Importer,
which will be the one resposible for actually do the job of importing
tasks, by using their public methods:

-   create\_tasks
-   count\_tasks\_to\_import
-   get\_all\_importer\_names
-   get\_autoimporter\_names

create\_importer takes as arguments task\_repo, project\_id,
importer\_id, and \*\*form\_data. task\_repo is a TaskRepository object
that will handle the store of the created Tasks. project\_id, the id of
the project to which the tasks belong. importer\_id being the name of
the importer, like described above. Finally, form\_data will be a
dictionary with the importer-specific form data (e.g. the
googledocs\_url for a gdocs importer).

count\_tasks\_to\_import takes as arguments the importer\_id and
\*\*form\_data, and will return, before creating any task, the number of
tasks that will be imported from the source. This is used for instance
for deciding whether to import the tasks in a synchronous or an
asynchronous way, depending on the amount of them.

get\_all\_importer\_names returns a list of all the available importers.
This list may vary depending on the configuration of the server (e.g. if
no API key for integration with the Flickr service is found, then the
Flickr importer won't be available).

get\_autoimporter\_names returns a list of the available importers for
using as autoimport background jobs. Again, this list may vary depending
on the server configuration.
