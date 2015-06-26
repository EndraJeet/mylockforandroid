# Introduction #

When myLock began with android 2.0 we set out with certain goals. The realization of the goals has been partial only, and functionality has been lost as v2.x of android has evolved.


# History of lost features #

  * Up to 2.1 eclair -- able to toggle security modes, enabling idle lock plug-in and useful one click switch between secure lockscreen on and myLock quick unlock.
  * Up to 2.2 froyo -- able to accept or reject incoming calls via customized window on screen or through button commands

# Goals still pending #

  * Replace lockscreen with full access to button customization, allowing user to choose how the device should wake up or unlock. The technique allowing a window to supersede the lockscreen provides only the choices of all keys wake or no change to keys that wake (dismiss keyguard flag vs show when locked). The system keyguard retains full mediation of wakeup.
  * Replace lockscreen with personalization options, resulting in a lockscreen the user can interact with for tools such as music, tools, widgets or quick app shortcuts. To do this in a polished, airtight fashion we would need a way to return control to the lockscreen from the custom lockscreen and a way to cleanly unlock the keyguard from user request in the custom lockscreen. Google has not provided any tools to fill these gaps when using the technique of show when locked or dismiss keyguard flags in the lock replacement window. The apps executive assistant, goto lockscreen, and widget locker have all proceeded with the somewhat impaired functionality. I do not wish to proceed with this goal while the experience is as flawed as it is.