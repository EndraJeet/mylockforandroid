# Introduction #

So far I've researched and the only thing turned up is some info on system settings. I need to check out the source for the stock settings activity to determine how feasible this is. I'm told there is an app AutoLock which seems like it might be skipping the lock in an interesting fashion, doing a delay before lockscreen kicks in. To me this seems to mean that you wake it back up without any unlock slider until the set time elapses, then you would see the pattern or lockscreen.

_<uses-permission android:name="android.permission.WRITE\_SETTINGS" />_

I've got some code that works in myLock lite, allowing the widget to double as a quick disengage for secure pattern mode and re-engage it with your same stored pattern when you turn it off.

At first start of the service (happens on click of the widget button
```
try {
			patternsetting = android.provider.Settings.System.getInt(getContentResolver(), android.provider.Settings.System.LOCK_PATTERN_ENABLED);
		} catch (SettingNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		if (patternsetting == 1) {    	
    	android.provider.Settings.System.putInt(getContentResolver(), 
    			android.provider.Settings.System.LOCK_PATTERN_ENABLED, 0); 
    	//tries turning off the lock pattern
		}
```

At ondestroy
```
if (patternsetting == 1) {
			android.provider.Settings.System.putInt(getContentResolver(), 
    			android.provider.Settings.System.LOCK_PATTERN_ENABLED, 1);
    	//re-enable pattern lock if applicable
```

# Levels of security needs #
  * no security, any key full unlock
  * minimal to moderate- want some or all keys to wake up a lockscreen but also some actions to complete immediate unlock
  * full guarding - want only certain actions to cause any wakeup and want a safety check like slide to unlock
  * full lockdown - want to retain pattern security or alternative pin code security at all times in conjunction with an enhanced lockscreen.

Idle timeout security - with any lesser security method allow a time period (or locale preference) where the most secure mode starts itself.

# How to force a sleep/lockdown #
Coming from non-secure, if the device is awake and in use and we want to force lockdown, we first change system lock pref from above to 1 (on), then we launch an activity with the flag keep screen on, and use window manager to set its brightness to 0.0. This forces screen off, and the user will try to wake back up, but when they press power, it is the real system sleep on first press. Then the secure lockscreen occurs. The 2nd press wakes up to the secure lockscreen.

With this activity I also intercept key events to return true, basically enforcing a no-input lockdown. This was first implemented in v1.3.4a to help enforce security after a reboot.

This isn't working on the HTC device (incredible, eris if ever updated to 2.0). The set bright doesn't cause the screen to go off, so instead we should make a black screen appear that hints the user to press power to continue. Hopefully they will fall for it.
Home key protection is something we just can't circumvent at all...