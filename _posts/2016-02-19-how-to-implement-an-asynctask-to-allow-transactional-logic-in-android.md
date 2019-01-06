<strong>What is an AsyncTask?</strong>
AsyncTask is an abstract class that Android provides to do potentially time-consuming tasks that would otherwise hang-up the user interface whilst it waits for the task to finish.

Android relies on AsyncTasks to be able to perform remote server API calls, for example: for transferring data to and from a database. This kind of task could potentially take a long time, especially with a mobile device that has an intermittent data connection.

In more technical terms - when Android launches an app. it will run on a single Thread. AsyncTask allows a task to be carried out on a separate/background Thread with the ability to perform actions on the main UI thread before, during and after the AsyncTask has completed. This enables the UI to keep track of the progress of the AsyncTask and perform an action once it is complete.

The following is a reference implementation of an AsyncTask used to authenticate a persons username and password against a remote database.
<script src="https://gist.github.com/final60/e69f9413d040cfe9a61b.js"></script>
