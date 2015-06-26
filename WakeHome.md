# Things to know #

This handy component gives users the option of a new home screen that takes over the role of the default lockscreen, an app that will be launched when the device is awakened.

This is quite literally nothing more than an app that gets resumed immediately after the keyguard skip on awakening.

The user has the option of interacting with the widgets/shortcuts they have placed on the screen, pressing menu to open the customization options (add or remove widgets & shortcuts), press back to hop back to what you were last doing before sleep, or press home to access the regular home environment, as always.

# Usefulness for pattern lock users #
This can actually be used to push a home screen up when device is awakened that can be used without having to pattern unlock. The test release for this mode works during pattern unlock. The behavior is that you can interact with the device after the wakehome finishes itself and closes, but the pattern lock will come back when we try the home key.

# Research #
http://developer.android.com/reference/android/appwidget/AppWidgetHost.html explains what we will use to add widget functionality to our wakehome activity. It's almost that simple, we also need to learn how to put app Launcher intent icons.

This description comes straight out of the android developer documentation:
_Widget hosts are the containers in which widgets can be placed. Most of the look and feel details are left up to the widget hosts. For example, the home screen has one way of viewing widgets, but the lock screen could also contain widgets, and it would have a different way of adding, removing and otherwise managing widgets._