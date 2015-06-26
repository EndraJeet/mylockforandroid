# Things to know #

We need several things to be included in this component. This will have to be implemented as a self contained 4x2 widget for a first build. The point is to save space and provide utilities inspired by the regular lockscreen and other power/brightness widgets out there.

  * Large readable clock/date
  * Battery percentage text
  * Backlight brightness 4 stage toggle
  * Sound/Vibrate 3 stage toggle (Silent, Vibrate only, and Loudest)
  * Optional links to other power control like bluetooth, wifi, gps)


The biggest design goal of this is to maximize the size of the clock and make the other tools either hidden till an interaction point is touched or else very minimal and unobtrusive yet easy to interact with.

![http://mylockforandroid.googlecode.com/files/utility_widg_concept.jpg](http://mylockforandroid.googlecode.com/files/utility_widg_concept.jpg)


# Custom Lockscreen first implementation #

This idea is first going to be implemented by coding the functionality into a utility lockscreen, then once it is all working well we will adapt into a widget for those who aren't going to use custom or secure lockscreen modes.

First iteration will incorporate the clock, battery status, & buttons that can control music.
Next priority after that will be to update with the brightness & sound toggles.

I've got the idea that long press will control the toggles. Music will be one button when nothing is playing that you long press to start it and show the full controls. Brightness and sound mode also long press to do the switch/toggling