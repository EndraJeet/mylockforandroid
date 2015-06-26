# Initial project plans #

I have identified 3 steps to the realization of the myLock vision in the first weeks of research and initial alpha programming.

  * The existing keyguard is an obstruction to end user convenience on the Droid since the device has no face buttons; since the only way to even awaken it is the power button on top (impossible to pocket-press accidentally vs the volume or camera keys could be) we will begin this project by simply bypassing the lockscreen automatically.
  * The existing keyguard is not 100% obstruction. It does give us some examples of useful ideas that we want to retain. On the first screen the user sees on wakeup, it is a nice option to have clock display and some shortcuts. We will create a utility widget of sorts to converge the idea of the clock display, battery %, some power controls such as a brightness level button and optional switches for other power-consuming componenets, and of course the silent mode/vibrate toggle similar to the one on the default lockscreen.
  * Finally, it would be useful to see a timeline of waiting events that have occurred while the device has slept in the wakeup or regular homescreen. The creation of this will be most complicated, as it seems it will require programming mini clients for email, twitter, SMS handling, and phone-event handling. I am not sure we have any way to talk to the existing notification panel or pull information from the default email client at all.

# On backwards compatibility #
in 2.0 the change to onstartcommand and startforeground are used instead of onstart and setforeground

also, the welcomeactivity code doesn't exist in the older versions. will have to try to grab some source and see if they had alarm clocks and what their method was.
for now this isn't really a goal.. i'm guessing android will go forward at 2.0 and up pretty strongly considering the announcements that g1 should receive it officially.

However, it seems that it will be beneficial for the purpose of compatibility troubleshooting that a pre-2.0 built basic version could be useful

See Versions page for current planned feature releases.

# How the features work #

  * Alpha 2c uses the pre-android-2.0 lockscreen interaction code. There is no custom lockscreen code in it, just a detection of screen wakeups to execute a few commands to dismiss it automatically.
  * The custom lockscreen uses new android 2.0 code to put a replacement lockscreen up when the screen sleeps. Then it can handle the release of keys to react as we choose. THe catch is that every key will create a wakeup. The custom lockscreen stops the screen from turning unless the key being released is defined as a wakeup or unlock key. This wake suppression will be called Advanced power save key lockdown in the advanced replacement lockscreen mode.
  * Shake wakeup is something I can do with or without the custom lockscreen mode. It simply accesses the sensor for the accelerometer to detect shake and accesses the power manager to create a wakeup. This feature is not a priority yet.