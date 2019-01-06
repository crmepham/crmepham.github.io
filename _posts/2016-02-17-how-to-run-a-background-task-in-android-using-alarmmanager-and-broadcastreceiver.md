In some circumstance it will be necessary for your application to run background tasks whether the app. is open or not. For example: an alarm clock will sound when a certain time has been reached, or updating a users location so other users can see where that user is on a map.

Android provides an excellent framework for managing the registering of a background task which will run specific code at a recurring interval indefinitely, even after the phone has been rebooted.

The following is a reference example of implementing a Receiver class which will be registered using AlarmManager.

First we must add some permissions to our Android project to enable the application to set alarms, register receivers and run them after the device has been rebooted.
<script src="https://gist.github.com/final60/a8fa4d0ce03d56204165.js"></script>

We will start an alarm task by pushing a button. Add it to a standard blank activity. 

<script src="https://gist.github.com/final60/559c9328fcdb8bbbb2d2.js"></script>
You will notice there are two buttons; one to start the alarm and another to stop it.

<script src="https://gist.github.com/final60/0889ac9f2f8b8b5e32d1.js"></script>
Above are the associated event handlers for our two buttons.

<script src="https://gist.github.com/final60/2b1405a0180575a44da7.js"></script>
The above code demonstrates a self-contained Receiver class that will register itself with Androids AlarmManager. One thing to note here:

<strong>setRepeating(int, Long, Long, PendingIntent)</strong>
This will tell the AlarmManager to run the receiver code repeatedly, although the interval is only approximate to the value you specify - taking into account the phones battery and available resources. An alternative is <strong>set()</strong> which will run the receiver code just once after being set and the interval reached.
