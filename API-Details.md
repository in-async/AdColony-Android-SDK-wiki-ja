[AdColony Class Reference](API-Details#wiki-adcolony-class-reference)<br>
[AdColonyVideoAd Class Reference](API-Details#wiki-adcolonyvideoad-class-reference)<br> 
[AdColonyV4VCAd Class Reference](API-Details#wiki-adcolonyv4vcad-class-reference)<br>
[AdColonyNativeAdView Class Reference]<br>
[AdColonyAdListener Interface Reference](API-Details#wiki-adcolonyadlistener-interface-reference)<br>
[AdColonyV4VCListener Interface Reference](API-Details#wiki-adcolonyv4vclistener-interface-reference)<br>
[AdColonyAdAvailabilityListener Interface Reference](API-Details#wiki-adcolonyadavailabilitylistener-interface-reference)<br>
[AdColonyNativeAdListener Interface Reference]<br>
[AdColonyNativeAdMutedListener Interface Reference]

==     
###AdColony Class Reference###
####Configuring AdColony####
[`configure( activity:Activity, client_options:String, app_id:String, zone_ids:String...)`](API-Details#wiki-configure-activity-activity-string-client_options-string-app_id-string-zone_ids-)
####Other AdColony Utilities####
[`setDeviceID( id:String )`](API-Details#wiki-setdeviceid-string-id-)<br>
[`setCustomID( id:String )`](API-Details#wiki-setcustomid-string-id-)<br>
[`getDeviceID() : String`](API-Details#wiki-getdeviceid)<br>
[`getCustomID() : String`](API-Details#wiki-getcustomid)<br>
[`addV4VCListener( listener:AdColonyV4VCListener )`](API-Details#wiki-addv4vclistener-adcolonyv4vclistener-listener-)<br>
[`removeV4VCListener( listener:AdColonyV4VCListener )`](API-Details#wiki-removev4vclistener-adcolonyv4vclistener-listener-)<br>
[`addAdAvailabilityListener( listener:AdColonyAdAvailabilityListener )`](API-Details#wiki-addadavailabilitylistener-adcolonyadavailabilitylistener-listener-)<br>
[`removeAdAvailabilityListener( listener:AdColonyAdAvailabilityListener )`](API-Details#wiki-removeadavailabilitylistener-adcolonyadavailabilitylistener-listener-)<br>
[`isTablet() : boolean`](API-Details#wiki-istablet)<br>
[`pause()`](API-Details#wiki-pause)<br>
[`resume( activity:Activity )`](API-Details#wiki-resume-activity-activity-)<br>
[`statusForZone( zone_id:String ) : String`](API-Details#wiki-statusforzone-string-zone_id-)<br>
[`cancelVideo()`](API-Details#wiki-cancelvideo)<br>

###Class Methods###

####configure( Activity activity, String client_options, String app_id, String... zone_ids )####
Configures AdColony specifically for your app; required for usage of the rest of the API. Please ensure that this method is only called once.
```java
static public void configure( Activity activity,String client_options, String app_id, String... zone_ids )
```
**Parameters**
* *activity*
  * Your Activity context (i.e. 'this').
* *client_options*
  * A String containing your app version, the origin store, and an optional "skippable" String that will enable users to cancel the ad experience using the back button. Publisher earnings will not occur for ads that are cancelled using this method (examples: “version:1.1,store:google” or "version:2.23,store:amazon,skippable"). Please note that if you are integrating into an Amazon app you will need to replace 'google' with 'amazon' in the client_options String.
* *app_id*  
  * The AdColony app ID for your app. This can be created and retrieved at the [Control Panel](http://clients.adcolony.com).  
* *zone_ids*  
  * Any number ( >= 1 ) of AdColony zone ID strings (an array of Strings is also acceptable). AdColony zone IDs can be created and retrieved at the [Control Panel](http://clients.adcolony.com). If null or inaccurate, your app will be unable to play ads and AdColony will only provide limited reporting and install tracking functionality.<br>
  * **NOTE: This is a zone specific key, and is different than your application's V4VC Secret Key. Your V4VC Secret Key should not be included in your configure call.**  

**Discussion**  
This method should be the first AdColony related call in your code, with the exception of [setDeviceID](API-Details#setdeviceid-string-id-) and [setCustomID](API-Details#setcustomid-string-id-). This method returns immediately; any long-running work such as network connections are performed in the background. AdColony does not begin preparing ads for display or performing reporting until after it is configured by your app.

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
The custom ID String is passed through as “&custom_id=...” and can be used at your discretion. Must be called before AdColony.configure().

---
####getDeviceID()####
Returns a globally unique identifier tied to the current installation of an app.
```java
static public String getDeviceID()
```
**Discussion**  
While an appropriate ID is generated automatically when the app is installed, you can also use [setDeviceID](API-Details#setdeviceid-string-id-) to set an ID of your choosing.

---
####getCustomID()####
Returns the String previously passed into [setCustomID](API-Details#setcustomid-string-id-)
```java
static public String getCustomID()
```
**Discussion**  
Returns an empty String if no custom ID is set.

---
####addV4VCListener( AdColonyV4VCListener listener )####
Registers a listener to be notified about V4VC results.
```java
static public void addV4VCListener( AdColonyV4VCListener listener )
```
**Parameters**   
* *listener*  
  * The AdColonyV4VCListener to be added.

**Discussion**  
Further discussion on how to implement a V4VCListener can be found [here](API-Details#adcolonyv4vclistener-interface-reference)

---
####removeV4VCListener( AdColonyV4VCListener listener )####
AdColony stops sending V4VC results to the specified listener.
```java
static public void removeV4VCListener( AdColonyV4VCListener listener )
```
**Parameters**   
* *listener*  
  * The AdColonyV4VCListener to remove.

**Discussion**  
Further discussion on how to implement a V4VCListener can be found [here](API-Details#adcolonyv4vclistener-interface-reference)

---
####addAdAvailabilityListener( AdColonyAdAvailabilityListener listener )####
Registers a listener to be notified changes in a zone's ad availability.
```java
static public void addAdAvailabilityListener( AdColonyAdAvailabilityListener listener )
```
**Parameters**   
* *listener*  
  * The AdColonyAdAvailabilityListener to be added.

**Discussion**  
Further discussion on how to implement an AdAvailabilityListener can be found [here](API-Details#adcolonyadavailabilitylistener-interface-reference)

---
####removeAdAvailabilityListener( AdColonyAdAvailabilityListener listener )####
AdColony will stop alerting this listener when ads become available or unavailable for a given zone.
```java
static public void removeAdAvailabilityListener( AdColonyAdAvailabilityListener listener )
```
**Parameters**   
* *listener*  
  * The AdColonyAdAvailabilityListener to remove.

**Discussion**  
Further discussion on how to implement an AdAvailabilityListener can be found [here](API-Details#adcolonyadavailabilitylistener-interface-reference)

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
Call this method from your Activity’s onResume() method.
```java
static public void resume(Activity activity)
```
**Parameters**   
* *activity*  
  * Your Activity reference.

---
####statusForZone( String zone_id )####
Returns a String that represents the state of the passed in zone id.
```java
static public String statusForZone(String zone_id)
```
**Parameters**
* *zone_id*
  * The zone id you wish to retrieve the status of.

**Returns**
* "invalid" - You've entered an incorrect zone id, or have not included this zone id in your configure call.
* "unknown" - You have not configured AdColony.
* "off"     - The zone is disabled.
* "loading" - The zone is enabled, but does not have any ads available to be played at this point.
* "active"  - The zone is enabled and has ads ready to be played.

---
####cancelVideo()####
Cancels the video ad, returning control to your application.
```java
static public void cancelVideo()
```
**Discussion**<br>
A video cancelled using this method will not count as a completed video view.




###AdColonyVideoAd Class Reference###
**Note:**
This section (minus the constructors) applies to both AdColonyVideoAd and AdColonyV4VCAd objects. Click [here](API-Details#wiki-adcolonyv4vcad-class-reference) for information specific to AdColonyV4VCAd objects.
####Creating an AdColonyVideoAd Object####
[`AdColonyVideoAd()`](API-Details#wiki-adcolonyvideoad)<br>
[`AdColonyVideoAd( zone_id:String )`](API-Details#wiki-adcolonyvideoad-string-zone_id-)<br>
####Interacting With an AdColonyVideoAd Object####
[`withListener( listener:AdColonyAdListener ) : AdColonyVideoAd`](API-Details#wiki-withlistener-adcolonyadlistener-listener-)<br>
[`isReady() : boolean`](API-Details#wiki-isready)<br>
[`show()`](API-Details#wiki-show)<br>
[`getAvailableViews() : int`](API-Details#wiki-getavailableviews)

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
**Parameters**   
* *zone_id*  
  * The zone you want the AdColonyVideoAd to play videos from.

**Discussion**  
You should create new AdColonyVideoAd objects every time you wish to play a video to avoid using outdated data internally.

---
####withListener( AdColonyAdListener listener )####
Registers a listener to be notified about when a video advertisement finishes. Returns the invoked AdColonyVideoAd object. 
```java
public AdColonyVideoAd withListener( AdColonyAdListener listener )
```
**Parameters**   
* *listener*  
  * The [AdColonyAdListener](API-Details#adcolonyadlistener-interface-reference) to use.

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
No ad will be shown if [isReady](API-Details#isready) returns false. You can chain together a call to show with the [withListener](API-Details#withlistener-adcolonyadlistener-listener-) method like so:<br>
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
AdColonyV4VCAd objects can be interacted with just as [AdColonyVideoAd objects](API-Details#wiki-interacting-with-an-adcolonyvideoad-object) can, with the following additions:
####Creating an AdColonyV4VCAd Object####
[`AdColonyV4VCAd()`](API-Details#wiki-adcolonyv4vcad)<br>
[`AdColonyV4VCAd( zone_id:String )`](API-Details#wiki-adcolonyv4vcad-string-zone_id-)<br>
####Interacting With an AdColonyV4VCAd Object####
[`withConfirmationDialog() : AdColonyV4VCAd`](API-Details#wiki-withconfirmationdialog)<br>
[`withResultsDialog() : AdColonyV4VCAd`](API-Details#wiki-withresultsdialog)<br>
[`getRewardName() : String`](API-Details#wiki-getrewardname)<br>
[`getRewardAmount() : int`](API-Details#wiki-getrewardamount)<br>
[`getViewsPerReward() : int`](API-Details#wiki-getviewsperreward)<br>
[`getRemainingViewsUntilReward() : int`](API-Details#wiki-getremainingviewsuntilreward)

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
**Parameters**   
* *zone_id*  
  * The zone you want the AdColonyV4VCAd to play videos from.

**Discussion**  
You should create new AdColonyV4VCAd objects every time you wish to play a video to avoid using outdated data internally.

---
####withConfirmationDialog()####
Enables a pre-­popup dialog to be shown prior to a V4VC video advertisement. Returns the invoked upon AdColonyV4VC object.
```java
public AdColonyV4VCAd withConfirmationDialog()
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
public AdColonyV4VCAd withResultsDialog()
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
[`onAdColonyAdStarted( ad:AdColonyAd )`](API-Details#wiki-onadcolonyadstarted-adcolonyad-ad-)<br>
[`onAdColonyAdAttemptFinished( ad:AdColonyAd )`](API-Details#wiki-onadcolonyadattemptfinished-adcolonyad-ad-)<br>
####Invoke on Returned AdColonyAd Object####
[`shown() : boolean`](API-Details#wiki-shown)<br>
[`notShown() : boolean`](API-Details#wiki-notshown)<br>
[`canceled() : boolean`](API-Details#wiki-canceled)<br>
[`noFill() : boolean`](API-Details#wiki-nofill)<br>
[`skipped() : boolean`](API-Details#wiki-skipped)

###Methods###
####onAdColonyAdStarted( AdColonyAd ad )####
This method, when implemented in your listener, is called when an ad starts playing.
```java
public void onAdColonyAdStarted( AdColonyAd ad )
```
**Parameters**   
* *ad*  
  * The ad that started playing.

**Discussion**  
This method is not called if the video ad fails to play.

---
####onAdColonyAdAttemptFinished( AdColonyAd ad )####
This method, when implemented in your listener, is called when an ad attempt finishes.
```java
public void onAdColonyAdAttemptFinished( AdColonyAd ad )
```
**Parameters**   
* *ad*  
  * The ad that has finished playing (or finished attempting to play).

**Discussion**  
This method **is** called if the video ad fails to play.

---
####shown()####
When invoked on the AdColonyAd object returned from [onAdColonyAdAttemptFinished](API-Details#onadcolonyadattemptfinished-adcolonyad-ad-), this method will return true if the ad was successfully shown.
```java
public boolean shown()
```

---
####notShown()####
When invoked on the AdColonyAd object returned from [onAdColonyAdAttemptFinished](API-Details#onadcolonyadattemptfinished-adcolonyad-ad-), this method will return true if the ad was **not** successfully shown.
```java
public boolean notShown()
```

---
####canceled()####
When invoked on the AdColonyAd object returned from [onAdColonyAdAttemptFinished](API-Details#onadcolonyadattemptfinished-adcolonyad-ad-), this method will return true if the ad was canceled.
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
[`onAdColonyV4VCReward( reward:AdColonyV4VCReward )`](API-Details#wiki-onadcolonyv4vcreward-adcolonyv4vcreward-reward-)<br>
####Invoke on Returned AdColonyV4VCReward Object####
[`success() : boolean`](API-Details#wiki-success)<br>
[`name() : String`](API-Details#wiki-name)<br>
[`amount() : int`](API-Details#wiki-amount)<br>
###Methods###
####onAdColonyV4VCReward( AdColonyV4VCReward reward )####
This method, when implemented, is called when a V4VC reward is attempted given you have added it to the list of AdColonyV4VCListeners ([see here](API-Details#wiki-addv4vclistener-adcolonyv4vclistener-listener-)).
```java
public void onAdColonyV4VCReward( AdColonyV4VCReward reward)
```
**Parameters**   
* *reward*  
  * The AdColonyV4VCReward object that contains information about the completed V4VC reward event.

**Discussion**<br>
In the event of a various network problems while using a server-side V4VC reward solution, a currency transaction will not be instantaneous which can result in this callback being executed by AdColony at any point during your application.

---
####success()####
When invoked on the returned [AdColonyV4VCReward](API-Details#wiki-onadcolonyv4vcreward-adcolonyv4vcreward-reward-) object, this method will return true if the V4VC reward event has occurred successfully. 
```java
public boolean success()
```

---
####name()####
When invoked on the returned [AdColonyV4VCReward](API-Details#wiki-onadcolonyv4vcreward-adcolonyv4vcreward-reward-) object, this method will return the name of the reward as set in the dashboard. 
```java
public String name()
```

---
####amount()####
When invoked on the returned [AdColonyV4VCReward](API-Details#wiki-onadcolonyv4vcreward-adcolonyv4vcreward-reward-) object, this method will return the amount of the reward awarded as set in the dashboard. 
```java
public int amount()
```



###AdColonyAdAvailabilityListener Interface Reference###
####Implement the Following####
[`onAdColonyAdAvailabilityChange( available:boolean, zone_id:String )`](API-Details#wiki-onadcolonyadavailabilitychange-boolean-available-string-zone_id-)<br>
###Methods###
####onAdColonyAdAvailabilityChange( boolean available, String zone_id )####
This method will be called when the ad availability of a zone changes (either from available to unavailable or from unavailable to available).
```java
public void onAdColonyAdAvailabilityChange(boolean available, String zone_id)
```
**Parameters**   
* *available*  
  * A boolean representing whether or not ads are now available (true) or ads are now not available (false).
* *zone_id*
  * The zone id in which ads are now available/unavailable.<br>

**Discussion**<br>
You can see an example of this listener in use in our Demo applications included in the SDK build distribution.