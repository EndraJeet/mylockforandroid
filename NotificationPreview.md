# Introduction #

The primary purpose of MyLock is to enhance the convenience of android's already brilliant notification system by giving the user's notifications a default home right on the lock screen so they can be previewed in a timeline when the user returns to the sleeping device. The other functions of the program are secondary, and exist to support this goal in various ways. I also want to enhance notifications and allow the user to specify things like a custom LED flash or reminder vibration.


# Details #

This concept is the basic inspiration for the design of this app. It will put users in control of their own personal message timeline which grabs all communication while the device sleeps. by default it collects all notifications which contain text. this can also be used to set if you want to put custom LED notification for a specific event type. option filter out contacts/apps or just set a whitelist if you only need to preview specific contacts. eventually, great facebook and twitter (also potentially email to show you who the waiting email is from and a subject preview with tap and hold to load a tooltip with body text) integration will become available as well so that if you don't have twidroid or other clients you can still connect these accounts to your preview panel to grab posts on your wall and @ mentions. at initial I will only have it set so it can interact with apps that place notifications (I use twidroid so I am expecting in the earliest versions I can have it see twidroid notifications)

For a first release, I will design the logic that gathers information from the notification panel and populates it on the default lockscreen. After that is working well (and displaying all default events such as call, waiting email/gv, sms, gtalk) I will work on getting additional interfaces that interact with email accounts, google voice, facebook/twitter to pull in content that is not supplied in their default notifications. At that point when more complexity is introduced, I will also implement the framework for user customization to choose what app notifications are to appear in the preview timeline (for example, I would only have gtalk in my preview as it is my primary communication from my device).



Here is the information of how programs send the notifications we are interested in gathering on our preview panel, from the android documentation:

```
public void notify (String tag, int id, Notification notification)
```
Since: API Level 5

Persistent notification on the status bar,

Parameters
  * tag:	An string identifier for this notification unique within your application.
  * notification:	A Notification object describing how to notify the user, other than the view you're providing. Must not be null.

Returns
  * the id of the notification that is associated with the string identifier that can be used to cancel the notification


```
public static final String NOTIFICATION_SERVICE
```

Since: API Level 1

Use with getSystemService(String) to retrieve a NotificationManager for informing the user of background events.

Constant Value: "notification"

I can use this as a starting point for gathering the preview information, but I know we will also at some point need to create code that attempts to interact with the app sending the notification to get info that is not in the notification, such as for google voice to find out who the message is from and what it says. this may be beyond the scope of what we can actually do, but ultimately the vision of the notification preview itself is to be a message timeline capable of previewing content of any message received while device sleeps upon user's return.

## Application Interaction ##
For email items, show sender and subject, then allow tap and hold to pop up a preview of the body. Same for GV sms or trasncripted VM.

Possibly enable contact organization where you see the latest message, tap and hold on that cell to see all messages in a quick tooltip display