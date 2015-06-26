# Prefs reset after a reboot (updates from pre 1.3.2 caused this) #
To resolve this uninstall then redownload the app and any addon packages. There is no other way to fix this.

# HTC security lockscreen and alarm clock #
HTC has chosen to place their lockscreen on top of the pattern verify screen, and has chosen to have their alarm exist in the lockscreen itself instead of a new window like the stock android one. myLock cannot disable to HTC slider that is required before the pattern, nor can I detect the HTC alarm. If you plan to use the alarm, toggle myLock off first. That's why there is a toggle widget. HTC has simply made the idea of not having the lockscreen more difficult by attaching important functionality like the alarm to their lockscreen.

# HTC standby time / battery usage #
We don't use any extra battery to run myLock. All we are doing is skipping lockscreen at wakeup, or replacing it at sleep. We aren't stopping your phone from sleeping and mining your data to send off to the mothership, I'm afraid. My theory is that HTC has made the mistake of tying standby tracking to their customized lockscreen, thus as we are disabling it in advanced mode, you would no longer see standby time counted correctly.

# Make it so Nav Button can unlock and keep the others locked #
I'm looking in to the possibility under rooted conditions, however the SDK does not allow us to do this.

# MOST IMPORTANT: get Log Collector #
The market now autoreports code errors, but most errors you may encounter will not be crashes, but something not working as expected. If you can email me a log immediately after a problem happens, I can know exactly why the problem happened and actually roll out a fix or a message to the dev of the app that caused the issue if it was a conflict. All you have to do is open Log Collector and put in our email (mylockandroid at gmail). In the subject, put the time you think the problem happened and what the problem was (IE: Lockscreen came back and wouldn't go away, Screen Came on but flashed back off, etc). If you can, please also go to Settings => Applications => Running Services and tell me what is running, that will give me an idea if any other persistent app is going that might not be putting things in the Log.

# UNINSTALL YOUR TASK KILLER #
Task killers cause the phone to run slower and cause massive problems for many apps. There is no benefit or upside.

# MAKE SURE YOU HAVE THE CORRECT KERNELS FOR SETCPU OVERCLOCK #
I've had tons of reports of problems from setCPU users. It appears the fix is to install the latest version of the recommended custom kernel into your rom to support the setCPU app. Most often the problems come during underclocking in sleep mode. Your results may vary drastically when reunning setCPU. I haven't tried it, but I may soon.

# What is the point of the status icon #
We've tried, but there is no way to work around the benefits of the status icon. Without it, you might experience a sudden loss of functionality and have to go back into settings & re-toggle the app. In my testing this seems quite rare, but I have posted a log with comments of a scenario I observed the error under while using browser. For more about this, check out the official android development post that explains- http://android-developers.blogspot.com/2010/02/service-api-changes-starting-with.html

# Why do the volume or camera buttons wake it back up sometimes? #
This is one of the rules of the lockscreen. When a timeout sleep occurs you have a short grace period in which the lockscreen isn't yet engaged, thus allowing any action at all to awaken it again quickly. That means any button, as well as even sliding the slider closed which normally doesn't trigger a wakeup.

## It stopped working and won't work again even though I've uninstalled and reinstalled (alpha 2c) ##

To get it working again the device needs to be rebooted by removing the battery for a few seconds. No other method of restart or re-install will get past the safety block the lockscreen imposes. The block will stop all apps from interacting with the lockscreen. I know this from testing with early versions that had different crashes which were fixed on the path from alpha 1 to alpha 2c. I have not yet had any crash scenarios for 2c reported, so things are looking good.