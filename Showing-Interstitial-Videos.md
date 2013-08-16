AdColony interstitial ads are a video ad immediately followed by an end-card.

###Instructions###
Once you've performed the required [[Project Setup]], you can display an AdColony interstitial ad in your app in 3 easy steps:
####Step 1: Configure AdColony####
First, make sure you have imported the AdColony library:
```java
import com.jirbo.adcolony.*;
```
Next, in your **main Activity's** onCreate method, call configure like so:
```java
AdColony.configure(this, client_options, app_id, zone_ids);
```
Replace client_options with your client options String (e.g. "version:2.1,store:google" - see [[API Details]] for more information on this) and app_id/zone_ids with your app and zone ids gathered from the [Control Panel](http://clients.adcolony.com).<br><br>
**Note:** you should only ever call configure **once** and make sure it is done in your **main Activity's** onCreate method.

===
####Step 2: Pause and Resume####
Override your Activity’s onPause() and onResume() methods to call corresponding AdColony methods as follows:
```java
public void onPause() 
{
  super.onPause();
  AdColony.pause(); 
}

public void onResume() 
{
  super.onResume();
  AdColony.resume( this ); 
}
```

===
####Step 3: Create AdColonyVideoAd Object and Call Show####
To show an AdColony interstitial video advertisement, create an AdColonyVideoAd object and call show on it as follows:
```java
AdColonyVideoAd ad = new AdColonyVideoAd().show();
```
Or:
```java
AdColonyVideoAd ad = new AdColonyVideoAd(zone_id).show();
```
Where zone_id is a String matching a specific zone gathered from the dashboard and included in your configure call.<br><br>
**Note:** this is a minimal example, please make note of the [[API Details]] page for more advanced usage.