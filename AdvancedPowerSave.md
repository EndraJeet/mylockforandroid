# Concepts #

With myLock, we want to save power in other ways so we can drop the militant keyguarding that comes standard. There are actually a few plausible approaches to this.

  * Strategy 1 - ensure screen uptime on the possible pocket wake is minimal. It is easy to do this by having the custom lockscreen lifecycle supply the system with a screen timeout value of 0, then restore the user's known real preference at unlock. This timeout causes a short 5-6 second minimum timeout like the one used by the stock lockscreen.

  * Strategy 2 - ensure screen power usage on the possible pocket wake is minimal. This one actually requries a split approach. AMOLED uses less power based on the actual light vs dark needed onscreen. Darker is literally more "off". LCD has no such dynamic
  * On the LCD, we can have the screen actually _remain off_ by forcing the activity brightness to 0.0.
  * On the amoled, the best we can do is show an all black blank layout while specifying the lowest brightness as well. The screen still "wakes" but will be using the least power

  * Strategy 3 - Access the accelerometer to make the power saving smart and intuitive. Phone takes the most aggressive power saving when in a "not in use" orientation. When orientation at time of wake is detected in a usable orientation, engage auto unlock instead of power save.

I've suggested this type of integration to the developer of screebl, but it seems more like a project we ought to take on head-first. Screebl is about keeping your screen awake. myLock all about getting your phone unlocked, or keeping it locked when needed.