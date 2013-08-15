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
[`+ setDeviceID( id:String )`](API-Details#setdeviceid)

###Class Methods###

####configure####
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
####setDeviceID####
Specifies the string identifier to use throughout the app instead of the automatically generated ID.
```java
+ static public void setDeviceID( String id )
```
**Parameters**   
* *id*  
  * The String identifier to use.  

**Discussion**  
Calls to [getDeviceID](API-Details#getdeviceid) will return this new ID as well. Must be called before AdColony.configure(). **Note: setting your own device ID is completely optional.**

---