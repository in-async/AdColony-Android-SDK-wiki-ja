[AdColony Class Reference](API-Details#adcolony-class-reference)<br>
[AdColonyVideoAd Class Reference](API-Details#adcolonyvideoad-class-reference)<br> 
[AdColonyV4VCAd Class Reference](API-Details#adcolonyv4vcad-class-reference)<br>
[AdColonyAdListener Interface Reference](API-Details#adcolonyadlistener-interface-reference)<br>
[AdColonyV4VCListener Interface Reference](API-Details#adcolonyv4vclistener-interface-reference)

==     
###AdColony Class Reference###
####Configuring AdColony####
[`+ configure( activity:Activity, client_options:String, app_id:String, zone_ids:String...)`](API-Details#configure)
####Other AdColony Utilities####
[`+ setDeviceID( id:String )`](API-Details#setdeviceid)<br>
[`+ setCustomID( id:String )`](API-Details#setcustomid)<br>
[`+ getDeviceID( id:String ) : String`](API-Details#getdeviceid)<br>
[`+ getCustomID( id:String ) : String`](API-Details#getcustomid)<br>
[`+ addV4VCListener( listener:AdColonyV4VCListener )`](API-Details#addv4vclistener)<br>
[`+ removeV4VCListener( listener:AdColonyV4VCListener )`](API-Details#removev4vclistener)<br>
[`+ isTablet() : boolean`](API-Details#istablet)<br>
[`+ pause()`](API-Details#pause)<br>
[`+ resume( activity:Activity )`](API-Details#resume)

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
####setCustomID ( String id )####
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

###Class Methods###

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