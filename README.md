# Wear OS AlarmManager
A new platform called Wear OS was created especially for wearable technology. Despite being focused on Android, it has a distinctive appearance and a range of special features. Users can build a list of things with a reminder time assigned to each task using the alarm manager on Wear OS application.
It aids in keeping track of one's critical responsibilities.
Also, it is helpful for starting and carrying out additional activities when used with broadcast receivers.
Besides, it lessens one's reliance on timers or background processes that run all the time. 

Access to the Android AlarmManager, which functions quite differently from iOS Local Notifications, is made available via this module. 


![The-Google-Clock-71-debuts-a-new-design-in-Wear](https://user-images.githubusercontent.com/86880351/180390156-35f735b4-187f-42d1-a62a-0663a1588e82.jpg)


## Features 
* Set a once off alarm
* Set a recurring alarm on set days of the week
* Disable and re-enable an alarm
* Play a looped ringtone for the alarm that is active
* Play a vibration effect for the alarm that is active
* Show a notification for the alarm this is active
* Dismiss or snooze an alarm   

## Components
* Time Picker
* Alarm Manager
* Broadcast Receivers
* Services   
* Vibrator 
* Ringtone
* Intent, Pending Intent and Intent Extras   
* Manifest and Permissions
* Calendar
* MVVM Design Pattern
* LiveData, Observer and Repository

## Steps to follow
### Step 1: Capturing the Alarm Time 
TimePicker is used to capture the alarm time and ToggleButton is added to set the alarm on or off. Initially, ToggleButton is set to off. It is set on when an alarm is set. In __AlarmSet.java__ class `onToggleClicked( )` method is implemented in which the current hour and the minute is set using the calendar. 

The `getCurrentHour()` and `getCurrentMinute()` methods were required to retrieve the hour and minute from the TimePicker widget prior to Android API level 23.
But now use the `getHour()` and `getMinute()` methods are used since the earlier methods have been deprecated. 

### Step 2: Scheduling an Alarm
The alarm is scheduled using the AlarmManager.
The `setExact(...)` function on the AlarmManager with the arguments is used to schedule the alarm if it is not recurring. __AlarmManager.RTC_WAKEUP__ alarm type (meaning it will wake up the device to fire the alarm if the screen is off), the time of the alarm in milliseconds and the pending intent previously created. If the alarm is recurring, it is scheduled using the `AlarmManager.setRepeating(...)` function with the parameters __AlarmManager.RTC WAKEUP__ alarm type, the alarm's millisecond duration, the repeat interval (which is set to 1 day), and the previously established pending intent.

<b>Sample Code:</b>
<pre><code>
alarmManager.setRepeating(AlarmManager.RTC_WAKEUP, time, 30000, pendingIntent);
</code></pre>

### Step 3: Starting the Alarm Service



### Step 4: Cancelling an Alarm
Using an __AlarmManager__ to schedule an alarm, the procedure is quite similar to the process using an __AlarmManager__ to cancel an alarm. 
We first get a reference to the __AlarmManager __by executing `getSystemService(ALARM SERVICE)` in the `cancel()` method.
Then, using the __AlarmBroadcastReceiver__, we build an intent and use it to generate a pending intent with a reference to the alarm id we specified when setting the alarm.
The alarm will be cancelled once we use the __AlarmManager's__ `cancel(PendingIntent)` method, handing it the __PendingIntent__ we generated as a parameter. 

<b>Sample Code:</b>
<pre><code>
else {
            alarmManager.cancel(pendingIntent);
            Toast.makeText(AlarmSet.this, "Stop Alarm", Toast.LENGTH_SHORT).show();
        }

</code></pre>



