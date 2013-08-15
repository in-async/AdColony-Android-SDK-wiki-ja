[AdColony Class Reference](API-Details#adcolony-class-reference)<br>
[AdColonyVideoAd Class Reference](API-Details#adcolonyvideoad-class-reference)<br> 
[AdColonyV4VCAd Class Reference](API-Details#adcolonyv4vcad-class-reference)<br>
[AdColonyAdListener Interface Reference](API-Details#adcolonyadlistener-interface-reference)<br>
[AdColonyV4VCListener Interface Reference](API-Details#adcolonyv4vclistener-interface-reference)

==     
###AdColony Class Reference###
####Configuring AdColony####
[`+ configure( activity:Activity, client_options:String, app_id:String, zone_ids:String...)`](API-Details#configure-activity-activity-string-client_options-string-app_id-string-zone_ids-)
####Other AdColony Utilities####
[`+ setDeviceID( id:String )`](API-Details#setdeviceid-string-id-)<br>
[`+ setCustomID( id:String )`](API-Details#setcustomid-string-id-)<br>
[`+ getDeviceID() : String`](API-Details#getdeviceid)<br>
[`+ getCustomID() : String`](API-Details#getcustomid)<br>
[`+ addV4VCListener( listener:AdColonyV4VCListener )`](API-Details#addv4vclistener-adcolonyv4vclistener-listener-)<br>
[`+ removeV4VCListener( listener:AdColonyV4VCListener )`](API-Details#removev4vclistener-adcolonyv4vclistener-listener-)<br>
[`+ isTablet() : boolean`](API-Details#istablet)<br>
[`+ pause()`](API-Details#pause)<br>
[`+ resume( activity:Activity )`](API-Details#resume-activity-activity-)

###Class Methods###

####configure( Activity activity, String client_options, String app_id, String... zone_ids )####
Configures AdColony specifically for your app; required for usage of the rest of the API.
```java
static public void configure( Activity activity,String client_options, String app_id, String... zone_ids )
```
**Parameters**
* *activity*
  * Your Activity context (i.e. 'this').
* *client_options*
  * A String containing your app version, origin store, and optionally a 'skippable' parameter to enable skippable ads in your app (example: “version=1.1,store:google,skippable”). **Note: no publisher earnings or V4VC rewards will occur if an ad is canceled using this method.**
* *app_id*  
  * The AdColony app ID for your app. This can be created and retrieved at the [Control Panel](http://clients.adcolony.com)  
* *zone_ids*  
  * Any number ( >= 1 ) of AdColony zone ID strings (an array of Strings is also acceptable). AdColony zone IDs can be created and retrieved at the [Control Panel](http://clients.adcolony.com). If null or inaccurate, your app will be unable to play ads and AdColony will only provide limited reporting and install tracking functionality.  

**Discussion**  
This method should be the first AdColony related call in your code, with the exception of [setDeviceID](API-Details#setdeviceid). This method returns immediately; any long-running work such as network connections are performed in the background. AdColony does not begin preparing ads for display or performing reporting until after it is configured by your app.

---
####setDeviceID( String id )####
Specifies the string identifier to use throughout the app instead of the automatically generated ID.
```java
static public void setDeviceID( String id )
```
**Parameters**   
* *id*  
  * The String identifier to use.  

**Discussion**  
Calls to [getDeviceID](API-Details#getdeviceid) will return this new ID as well. Must be called before AdColony.configure(). **Note: setting your own device ID is completely optional.**

---
####setCustomID( String id )####
Sets a custom ID String that is passed through to server-­side V4VC callbacks
```java
static public void setCustomID( String id )
```
**Parameters**   
* *id*  
  * The String identifier to use.  

**Discussion**  
The custom ID String is passed through as “&custom_id=...” and can be used at your discretion.

---
####getDeviceID()####
Returns a globally unique identifier tied to the current installation of an app.
```java
static public String getDeviceID()
```
**Discussion**  
While an appropriate ID is generated automatically when the app is installed, you can also use [setDeviceID](API-Details#setdeviceid) to set an ID of your choosing. In either case, make sure that the device ID you use to contact the virtual currency server with is the same device ID that AdColony is using.

---
####getCustomID()####
Returns the String previously passed into [setCustomID](API-Details#setcustomid)
```java
static public String getCustomID()
```
**Discussion**  
Returns an empty String if no custom ID is set.

---
####addV4VCListener( AdColonyV4VCListener listener )####
Registers a listener to be notified about V4VC results.
```java
static public void addV4VCListener()
```
**Discussion**  
Further discussion on how to implement a V4VCListener can be found [here](API-Details#adcolonyv4vclistener-interface-reference)

---
####removeV4VCListener( AdColonyV4VCListener listener )####
AdColony stops sending V4VC results to the specified listener.
```java
static public void removeV4VCListener()
```
**Discussion**  
Further discussion on how to implement a V4VCListener can be found [here](API-Details#adcolonyv4vclistener-interface-reference)

---
####isTablet()####
Returns "true" when run on Android tablets.
```java
static public boolean isTablet()
```

---
####pause()####
Call this method from your Activity’s onPause() method.
```java
static public void pause()
```

---
####resume( Activity activity )####
Call this method from your Activity’s onPause() method.
```java
static public void resume(Activity activity)
```
**Parameters**   
* *activity*  
  * Your Activity context.



###AdColonyVideoAd Class Reference###
**Note:**
This section (minus the constructors) applies to both AdColonyVideoAd and AdColonyV4VCAd objects. Click [here](API-Details#adcolonyv4vcad-class-reference) for information specific to AdColonyV4VCAd objects.
####Creating an AdColonyVideoAd Object####
[`+ AdColonyVideoAd()`](API-Details#adcolonyvideoad)<br>
[`+ AdColonyVideoAd( zone_id:String )`](API-Details#adcolonyvideoad-string-zone_id-)<br>
####Interacting With an AdColonyVideoAd Object####
[`+ withListener( listener:AdColonyAdListener ) : AdColonyVideoAd`](API-Details#withlistener-adcolonyadlistener-listener-)<br>
[`+ isReady() : boolean`](API-Details#isready)<br>
[`+ show()`](API-Details#show)<br>
[`+ getAvailableViews() : int`](API-Details#getavailableviews)

###Instance Methods###

####AdColonyVideoAd()####
Creates a video ad that will play from the first available zone.
```java
public AdColonyVideoAd()
```
**Discussion**  
You should create new AdColonyVideoAd objects every time you wish to play a video to avoid using outdated data internally.

---
####AdColonyVideoAd( String zone_id )####
Creates a video ad that will play from specified zone.
```java
public AdColonyVideoAd( String zone_id )
```
**Discussion**  
You should create new AdColonyVideoAd objects every time you wish to play a video to avoid using outdated data internally.

---
####withListener( AdColonyAdListener listener )####
Registers a listener to be notified about when a video advertisement finishes. Returns the invoked AdColonyVideoAd object. 
```java
public AdColonyVideoAd withListener( AdColonyAdListener listener )
```

---
####isReady()####
Returns true if a video advertisement is ready to be played, or false otherwise.
```java
public boolean isReady()
```
**Discussion**  
If isReady returns false, more information about why is logged out.

---
####show()####
Shows a video advertisement if possible.
```java
public void show()
```
**Discussion**  
No ad will be shown if [isReady](API-Details#isready) returns false. You can chain together a call to show with the [withListener](API-Details#withlistener-adcolonyadlistener-listener-) like so:<br>
```java
AdColonyVideoAd ad = new AdColonyVideoAd().withListener( listener ).show();
```

---
####getAvailableViews()####
Returns the remaining number of plays available today.
```java
public int getAvailableViews()
```



###AdColonyV4VCAd Class Reference###
**Note:**
AdColonyV4VCAd objects can be interacted with just as [AdColonyVideoAd objects](API-Details#interacting-with-an-adcolonyvideoad-object) can, with the following additions:
####Creating an AdColonyV4VCAd Object####
[`+ AdColonyV4VCAd()`](API-Details#adcolonyv4vcad)<br>
[`+ AdColonyV4VCAd( zone_id:String )`](API-Details#adcolonyv4vcad-string-zone_id-)<br>
####Interacting With an AdColonyV4VCAd Object####
[`+ withConfirmationDialog() : AdColonyV4VCAd`](API-Details#withconfirmationdialog)<br>
[`+ withResultsDialog() : AdColonyV4VCAd`](API-Details#withresultsdialog)<br>
[`+ getRewardName() : String`](API-Details#getrewardname)<br>
[`+ getRewardAmount() : int`](API-Details#getrewardamount)<br>
[`+ getViewsPerReward() : int`](API-Details#getviewsperreward)<br>
[`+ getRemainingViewsUntilReward() : int`](API-Details#getremainingviewsuntilreward)

###Instance Methods###

####AdColonyV4VCAd()####
Creates a V4VC ad that will play from the first available zone.
```java
public AdColonyV4VCAd()
```
**Discussion**  
You should create new AdColonyV4VCAd objects every time you wish to play a video to avoid using outdated data internally.

---
####AdColonyV4VCAd( String zone_id )####
Creates a V4VC ad that will play from specified zone.
```java
public AdColonyV4VCAd( String zone_id )
```
**Discussion**  
You should create new AdColonyV4VCAd objects every time you wish to play a video to avoid using outdated data internally.

---
####withConfirmationDialog()####
Enables a pre-­popup dialog to be shown prior to a V4VC video advertisement. Returns the invoked upon AdColonyV4VC object.
```java
public void withConfirmationDialog()
```
**Discussion**  
You can chain this method together with [show](API-Details#show) as follows:<br>
```java
AdColonyV4VCAd ad = new AdColonyV4VCAd().withConfirmationDialog().show();
```

---
####withResultsDialog()####
Enables a post-­popup dialog to be shown after a V4VC video advertisement.
```java
public void withResultsDialog()
```
**Discussion**  
You can chain this method together with [show](API-Details#show) as follows:<br>
```java
AdColonyV4VCAd ad = new AdColonyV4VCAd().withResultsDialog().show();
```

---
####getRewardName()####
Returns the name of your virtual currency as set on the dashboard.
```java
public String getRewardName()
```
**Discussion**  
The value that this method returns may not be valid if a successful ad config has not finished downloading (triggered by [configure](API-Details#configure-activity-activity-string-client_options-string-app_id-string-zone_ids-)).

---
####getRewardAmount()####
Returns the amount of virtual currency rewarded as set on the dashboard.
```java
public int getRewardAmount()
```
**Discussion**  
The value that this method returns may not be valid if a successful ad config has not finished downloading (triggered by [configure](API-Details#configure-activity-activity-string-client_options-string-app_id-string-zone_ids-)).

---
####getViewsPerReward()####
Returns the number of video views needed to receive a reward (1 by default).
```java
public int getViewsPerReward()
```
**Discussion**  
The value that this method returns may not be valid if a successful ad config has not finished downloading (triggered by [configure](API-Details#configure-activity-activity-string-client_options-string-app_id-string-zone_ids-)).

---
####getRemainingViewsUntilReward()####
Returns the number of video views needed until the next reward will be given (1 by default).
```java
public int getRemainingViewsUntilReward()
```
**Discussion**  
The value that this method returns may not be valid if a successful ad config has not finished downloading (triggered by [configure](API-Details#configure-activity-activity-string-client_options-string-app_id-string-zone_ids-)).



###AdColonyAdListener Interface Reference###
####Implement the Following####
[`+ onAdColonyAdStarted( ad:AdColonyAd )`](API-Details#onadcolonyadstarted-adcolonyad-ad-)<br>
[`+ onAdColonyAdAttemptFinished( ad:AdColonyAd )`](API-Details#onadcolonyadattemptfinished-adcolonyad-ad-)<br>
####Invoke on Returned AdColonyAd Object####
[`+ shown() : boolean`](API-Details#shown)<br>
[`+ canceled() : boolean`](API-Details#canceled)<br>
[`+ noFill() : boolean`](API-Details#nofill)<br>
[`+ skipped() : boolean`](API-Details#skipped)

###Methods###
####onAdColonyAdStarted( AdColonyAd ad )####
This method, when implemented in your listener, is called when an ad starts playing.
```java
public void onAdColonyAdStarted( AdColonyAd ad )
```
**Discussion**  
This method is not called if the video ad fails to play.

---
####onAdColonyAdAttemptFinished( AdColonyAd ad )####
This method, when implemented in your listener, is called when an ad attempt finishes.
```java
public void onAdColonyAdAttemptFinished( AdColonyAd ad )
```
**Discussion**  
This method **is** called if the video ad fails to play.

---
####shown()####
When invoked on the AdColonyAd object returned from [onAdColonyAdAttemptFinished](API-Details#onadcolonyattemptfinished-adcolonyad-ad-), this method will return true if the ad was successfully shown.
```java
public boolean shown()
```

---
####canceled()####
When invoked on the AdColonyAd object returned from [onAdColonyAdAttemptFinished](API-Details#onadcolonyattemptfinished-adcolonyad-ad-), this method will return true if the ad was canceled.
```java
public boolean canceled()
```
**Discussion**  
An example of when this method would return true would be if a user skips an ad (skippable ads must be enabled for this to occur).

---
####noFill()####
When invoked on the AdColonyAd object returned from [onAdColonyAdAttemptFinished](API-Details#onadcolonyattemptfinished-adcolonyad-ad-), this method will return true if there was no no ad played due to no ad fill.
```java
public boolean noFill()
```

---
####skipped()####
When invoked on the AdColonyAd object returned from [onAdColonyAdAttemptFinished](API-Details#onadcolonyattemptfinished-adcolonyad-ad-), this method will return true if the ad was skipped due to an interval play setting (set on the dashboard).
```java
public boolean skipped()
```



###AdColonyV4VCListener Interface Reference###
####Implement the Following####
[`+ onAdColonyV4VCReward( reward:AdColonyV4VCReward )`](API-Details#onadcolonyv4vcreward-adcolonyv4vcreward-reward-)<br>
####Invoke on Returned AdColonyV4VCReward Object####
[`+ success() : boolean`](API-Details#success)<br>
[`+ name() : String`](API-Details#name)<br>
[`+ amount() : int`](API-Details#amount)<br>
###Methods###
####onAdColonyV4VCReward( AdColonyV4VCReward reward )####
This method, when implemented, is called when a V4VC reward is attempted given you have added it to the list of AdColonyV4VCListeners ([see here](API-Details#addAdColonyV4VCListener-adcolonyv4vclistener-listener-)).
```java
public void onAdColonyV4VCReward( AdColonyV4VCReward reward)
```

---
####success()####
When invoked on the returned [AdColonyV4VCReward](API-Details#onadcolonyv4vcreward-adcolonyv4vcreward-reward-) object, this method will return true if the V4VC reward event has occurred successfully. 
```java
public boolean success()
```
**Discussion**
In the event of a various network problems, a currency transaction will not be instantaneous, which can result in this callback being executed by AdColony at any point during your application.

---
####name()####
When invoked on the returned [AdColonyV4VCReward](API-Details#onadcolonyv4vcreward-adcolonyv4vcreward-reward-) object, this method will return the name of the reward as set in the dashboard. 
```java
public String name()
```

---
####amount()####
When invoked on the returned [AdColonyV4VCReward](API-Details#onadcolonyv4vcreward-adcolonyv4vcreward-reward-) object, this method will return the amount of the reward awarded as set in the dashboard. 
```java
public int amount()
```