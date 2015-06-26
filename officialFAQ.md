# What is myLock? #

It is an app whose primary function is to replace the lockscreen. It has several sub-features that go along with this goal.

# Why did you make it? #
The guiding principle is one simple fact: we don't like having to slide to unlock.
We want to use the device on the first interaction, and not require a redundant slide action. It's a little surprising that the option not to have the lockscreen isn't already built into the OS. Off, keyguard, or pattern lock seem like suitable choices for end users, so myLock wants to step in to provide the Off category. Although the OS has provided tools for making the lockscreen go away, they are only designed for use cases like pushing a popup to the screen automatically (such as the default alarm clock). As a result we might go as far as doing a firmware mod for install on root devices to accomplish parts of the goal that are off-limits to regular apps.

# But I want a quick way to disable pattern lock also, can myLock do this? #
Not anymore. As of android 2.2 the permission to edit system security settings is locked to system level. Every past version except the secure custom lockscreen automatically suppresses pattern mode when myLock starts. It will automatically retain your pattern in the system settings and restart lockdown mode when you stop myLock. We also had an idle timeout option where myLock will disable itself and restore the pattern lock after a number of minutes left idle. These features are dead thanks to the security tightening actions implemented in the recent android updates.

# Froyo adds pin/password based lockscreen options, can myLock interact with these? #
Actually the case here is opposite. Froyo appears to be closing the security hole which let the setting of requiring security be accessed from apps that had permission to change settings. myLock will have no security control in Froyo.

# Make a locale plugin #
Ok. But I don't have locale. My app is free, but locale is 10 bucks. So I need to get it first so I can test the plugin.

# Make better icons / visuals #
Not my forte, feel free to send me your submissions. Open source means the community can and should contribute. The greatness of the project is directly relative to the level of community participation.

# Will myLock also offer customization for backlight timers? #
Probably. At the moment we have very little priority on this. The only implementation will be under the Custom mode lockscreen. This will offer advanced power save options which can stop the screen from waking up with specific buttons or reduce the timeout to a minimal 5 or 6 seconds while lockscreen is showing. Don't confuse the lockscreen functionality with auto-sleep or auto-dim functionalities, which are governed separately. I recommend screebl, and all development of the app has been with screebl running to ensure good interaction.

# Can you program customization for different buttons or touching the screen or touch buttons to wake it or unlock it? #
We can, but it is a little bit complicated due to the functions that allow us access are new to android 2.0 and so offer very little flexibility. Two versions will be available - Advanced, which has any key/event waking up the screen with options for customizing power saving features, and Guarded, which only wakes up with power, slider, and keypad buttons.

# So, does this mean you can also program shake unlocking? #
Yes. We have learned how to get shake implemented but it is also pretty complicated and won't be a big priority for support till later in development. I have a test build which can get the shake from sleep but it needs work to properly interact with shake at a good sensetivity level.

# Can you create a custom lockdown mode requiring a password? #
We're researching this. It is definitely possible. There is an app called wave secure which has a lockdown like this. We just aren't sure how useful a standalone lockdown would be in the long run. It wouldn't be able to stop incoming call usage. We'd also recommend Smart Lock, the dev is excellent and has provided the best program for stopping usage of apps by going through a locked down approved home screen.

# Can you give preferences to answer incoming call without using the touchscreen too? #
Up till android 2.2 we can. Android 2.3 locked the phone answer/end permission to system level so the functionality is dead.

# Can you have a favorite app launch at every unlock? #
Yes, we can have the app put out an App Start request, for example I've had one user request that the phone dialer launch after instant unlock.

# What's the custom lockscreen? #
The inspiration to create this was the existing silencer slider/clock display on the default lockscreen. Why not just make it an extra homescreen and let the user decide what to put there? So far we almost have widget adding fully functional & a clock, battery readout, and basic music buttons. I gave up on developing it due to the insufficiency of the current lockscreen superceding window tools. Widget Locker and GOTO lockscreen have still tried despite the gaps in functionality present in the current lockscreen replacement techniques.

# Can you make a custom lockscreen we can bring up in front of the pattern lock screen, for controlling music, etc? #
Yes. This is a priority for the updates we have been working on. It is currently available in the custom lockscreen version beta 1.0.

# It makes <insert app name> stop working... WTF? #
It is hard to make the app play nice with other home or screenwake mods because they all rely on workarounds in android to work cleanly. when all these workarounds go in and try to execute in near-tandem, unexpected results will happen. See the Troubleshooting FAQ for more details and info on apps that may interfere with myLock's operation.

# How do I send you my idea/feedback/bug complaint? #
Email the project mylockandroid at gmail. You can also follow us on twitter and tweet at us if your comment is short. Can't guarantee I'll notice your comments elsewhere like blog, wiki, or will be aware of posts on forums. [is retired at the moment, i am posting my android thoughts only in my personal twitter as of feb 2011.](twitter.md)

# Why should I donate #
If my app was 99 cents, it would severely decrease its accessibility. People just wouldn't try it out. I rely on as many installs with feedback as possible to build myLock into the best & most customizable lockscreen modifying app. I want those out there who really love what we've done to have a way to elevate themselves above the average user, and feel acknowledged by me for their support. I don't exactly need money/donations to continue this project. The option is just something I've made available to let those who have most benefitted from myLock make their voices heard and make a greater influence on the project's overall direction.