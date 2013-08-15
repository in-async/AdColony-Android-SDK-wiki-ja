[AdColony Class Reference](API-Details#adcolony-class-reference)<br>
[AdColonyVideoAd Class Reference](API-Details#adcolonyvideoad-class-reference)<br> 
[AdColonyV4VCAd Class Reference](API-Details#adcolonyv4vcad-class-reference)<br>
[AdColonyAdListener Interface Reference](API-Details#adcolonyadlistener-interface-reference)<br>
[AdColonyV4VCListener Interface Reference](API-Details#adcolonyv4vclistener-interface-reference)

==     
###AdColony Class Reference###
####Configuring AdColony####
[`+ configure( activity:Activity, client_options:String, app_id:String, zone_ids:String...)`](API-Details#configure)

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
  *
* *app_id*  
  * The AdColony app ID for your app. This can be created and retrieved at the [Control Panel](http://clients.adcolony.com)  
* *zoneIDs*  
  * An array of at least one AdColony zone ID string. AdColony zone IDs can be created and retrieved at the [Control Panel](http://clients.adcolony.com). If `nil`, app will be unable to play ads and AdColony will only provide limited reporting and install tracking functionality.  

**Discussion**  
This method returns immediately; any long-running work such as network connections are performed in the background. AdColony does not begin preparing ads for display or performing reporting until after it is configured by your app.

---