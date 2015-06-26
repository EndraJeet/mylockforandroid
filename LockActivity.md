# What is a Lock Activity? #

In android 2.0, two window flags were added allowing activities to inherently interact with the lockscreen.
  * FLAG\_SHOW\_WHEN\_LOCKED allows a window to get shown above the keyguard. It will only work with a non-translucent theme, even if you force fullscreen. It can only handle input from the user while awake. If asleep, no behavior change occurs, currently. When the window exits, the lockscreen immediately re-appears. It currently seems that one has to revert to the pre-2.0 lockscreen exit code while using this window if they wish for a seamless exit into another part of their app from this activity.
  * FLAG\_DISMISS\_KEYGUARD allows the window to get shown and cancel the keyguard completely. How this is different from the first flag is that when the activity is closed, the user will then see their last task in the stack instead of the lockscreen. If sleep occurs while activity is active, it also prevents the Keyguard from occurring where it would normally govern that sleep. This means any key will cause a wakeup, because the Keyguard is what mediates blocking wakeup from the side keys. There is no good way to get back to the lockscreen from this type of activity. However, we found that as long as we call DisableKeyguard from the pre-2.0 method at the same time as creating this activity to cancel, we can then use the corresponding Re-enable call that will actually cause the lockscreen to re-appear on demand.

# How do we make use of the Lock Activities to let the user customize their lockdown & wakeup experience? #
The implementation involves a life-cycle mediated by a remote service handling phone and screen events, which attempts to launch the Lock Activity at screen off. Two startCommand callbacks will be sent back to the mediator via simple implicit intent broadcasts, allowing it to know when the Lock Activity successfully started and when it successfully exited. This life cycle lets our activity pose as the lockscreen.

The real trickiness comes from the fact that key event mediation is not as we would expect with these lockscreen interaction flags. With show when locked, it seems we don't get any events unless awake. With dismiss, we get everything, and also have to deal with a wakeup from everything. The expected behavior for either would be the ability to handle key events first, then return false if we wanted to pass them on to the lockscreen for handling. It seems the case hasn't been considered, so the odd Always vs Never wake behavior is the end result.

Despite challenges, we've been able to create 3 types of custom lockscreens

Secure - happens on top of the lockscreen, regardless of whether there is a pattern. You have to slide the pattern or regular slider to get to anything else.

Guarded - simply replaces the stock lockscreen without trying to reinvent the power control functionality. Does exit the lockscreen when user exits, that's the only change from secure mode. Both use show\_when\_locked.

Advanced - the trickiest, as it totally disables the lockscreen (utilizing dismiss\_keyguard), allowing any button to wake it up. Various settings are available with it to determine which keys instant unlock and which are guarded so only lockscreen wakes. Additionally, advanced power saving can be enabled, allowing toggle of Locked mode for any key to keep the screen asleep in the case of a pocket-press, and optional shortened screen sleep time when a guarded key wakes the custom lockscreen.

# Example code #

When you want to replace the lockscreen only by using the show when locked flag (best practice since you want to keep side keys locked down), you also need a way to handle the user unlocking. The pre 2.0 method works (call disable keyguard, then call securely exit) but it is prone to problems. If your lockscreen gives the user access to the notification panel, or the user exits through home key, you have to use the pre 2.0 method. You can handle a home key exit since user pressing home causes onStop to get called while the activity was still resumed and had focus. Because the show when locked activity is going to force the keyguard back into play as soon as it is no longer the top most window, the workaround is to call disablekeyguard as soon as you detect that the user has pressed home or clicked on something in the notification panel, then follow it up in the next life cycle call with securely exit. See the basic guard mediator source for the examples of these lifecycle setups. I will be implementing them soon into guarded mode custom lockscreen.

I've developed a problem free method for unlocking utilizing the dismiss keyguard flag, which is used for user requested unlock. The Auto Unlock version just launches this at screen on while calls aren't in progress

Here is the method from the mediator service:

```
public void StartDismiss(Context context) {
            
    	//PowerManager myPM = (PowerManager) getApplicationContext().getSystemService(Context.POWER_SERVICE);
        //myPM.userActivity(SystemClock.uptimeMillis(), true);
    	ManageWakeLock.acquireFull(getApplicationContext());
    	
    Class w = AutoDismissActivity.class; 
                  
    Intent dismiss = new Intent(context, w);
    dismiss.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK//required for a service to launch activity
                    | Intent.FLAG_ACTIVITY_NO_HISTORY);
//No history tells the OS to finish the activity after it goes into the background
                    
    context.startActivity(dismiss);
}
```

Here is the auto dismiss activity

```
public class AutoDismissActivity extends Activity {
	public boolean done = false;
    
    protected void onCreate(Bundle icicle) {
    super.onCreate(icicle);

    
    requestWindowFeature(android.view.Window.FEATURE_NO_TITLE);
    getWindow().addFlags(WindowManager.LayoutParams.FLAG_DISMISS_KEYGUARD
  		  //| WindowManager.LayoutParams.FLAG_SHOW_WHEN_LOCKED
  		  | WindowManager.LayoutParams.FLAG_TURN_SCREEN_ON
  		  | WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON);
    
    Log.v("dismiss","creating dismiss window");
    
    updateLayout();
    
    //register for user present so we don't have to manually check kg with the keyguard manager
    IntentFilter userunlock = new IntentFilter (Intent.ACTION_USER_PRESENT);
    registerReceiver(unlockdone, userunlock);

}      
    protected View inflateView(LayoutInflater inflater) {
    return inflater.inflate(R.layout.dismisslayout, null);
}

private void updateLayout() {
    LayoutInflater inflater = LayoutInflater.from(this);

    setContentView(inflateView(inflater));
}

BroadcastReceiver unlockdone = new BroadcastReceiver() {
	    
	    public static final String present = "android.intent.action.USER_PRESENT";

	    @Override
	    public void onReceive(Context context, Intent intent) {
	    	if (!intent.getAction().equals(present)) return;
	    	if (!done) {
	    		Log.v("dismiss user present","sending to back");
	    		done = true;
	    		//callback mediator for final handling of the stupid wake lock
	            Intent i = new Intent("i4nc4mp.myLock.lifecycle.LOCKSCREEN_EXITED");
	            getApplicationContext().sendBroadcast(i);
	    	   	moveTaskToBack(true);
	    	   	finish();
	    	}
	    }
};

@Override
public void onDestroy() {
    super.onDestroy();      
   
    unregisterReceiver(unlockdone);
    Log.v("destroy_dismiss","Destroying");

    }
}
```


# How to transition from non-secure Keyguard screen to the Secure Pattern? #
We have implemented security interaction by having permission to access system settings and set the pattern flag to 0 when we start one of the mediator services. When we receive a disable toggle, the mediator will restore the pattern flag again as it closes down. The issue here is that the system still has the non-secure keyguard screen open when that happens in the background.
To create the Pattern Verification lockscreen, all we actually have to do is call the pre-2.0 DisableKeyguard, then wait 50 ms approx via a handler thread, then call re-enable.  There currently however isn't a better solution to move back and forth between fully having cancelled the non-secure lockscreen via the 2.0 dismiss flag and restoring it. However the same thing is true for using the Disable command just prior to doing the window-based dismiss. We can then use the re-enable command to force the Keyguard back on.

# Porting Dismiss Activity to 1.5 compatibility #
I created an activity to function exactly like the dismiss activity. It calls disable keyguard at create, then calls securely exit when it gains focus initially. then it exits per usualy at receiving user present.