AdColony interstitial ads are a video ad immediately followed by an end-card (described in more detail in the AdColony Product Overview).

###Instructions###
Once you've performed the required [[Project Setup]], you can display an AdColony interstitial ad in your app in two easy steps:
####Step 1: Configure AdColony####
In your **main Activity's** onCreate method, call configure like so:
```java
AdColony.configure(this, client_options, app_id, zone_ids);
````
Replace client_options with your client options String (e.g. "version:2.1,store:google" - see [[API Details]] for more information on this) and app_id/zone_ids with your app and zone ids gathered from the [Control Panel](http://clients.adcolony.com).<br><br>
**Note:** you should only ever call configure **once** and make sure it is done in your **main Activity's** onCreate method.

===
