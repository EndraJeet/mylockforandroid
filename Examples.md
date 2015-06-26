Keyguard disabler & Screenmodewidget - these use only the settings hack it seems. I can't detect that they are even calling disable keyguard. yet their permissions say they've called that permission, perhaps the hack doesn't accomplish the result without permission anyhow.

Lock 2.0 (also Lockbot I think) - worthless. using some crazy weird combo of home replacement non-default home and regular disable keyguard calls. they don't even do anything useful, just cosmetic.

dxTop - the only feature it has is a cosmetic slide unlock screen that comes with the home replacement app. The method it uses may perhaps be compelling, I never saw it displaying any semblance of the stock lockscreen but also would not wake on side keys. Will research further, to determine if this is something myLock could use for a full feature set release.

Flyscreen - not good. They are using the settings hack. the device is able to be awakened anytime with any key, and then flyscreen gets in your face, can't add any outside widgets.

Executive assistant - This dev is awesome. The app is very very good. When you place it in lockscreen mode, you will see the lockscreen for a second, then it is called up. They call it welcome mode if you use the regular lockscreen slider, and then immediately after get to their home activity automatically. This is really the best way.

They are using key event handling similar to how the alarm dialog does to have all side keys locked down. home still goes home (per lockscreen rules) but long press does not work (a la alpha 1 and 2a), so it is more likely a literal disable call than the window manager method.

This app is already accomplishing the best implementation of the idea of WakeHome, & gives you the choice to use their info utilities as a widget on home so you could pair it with myLock for the best total functionality. Possibly I will abandon the concept of wakeup homescreen and just point my users to this app, and take myLock into beta as a strict lockscreen skip with the other planned utilities.