AdColony V4VC (Videos-for-Virtual-Currency) is a system built on top of our [[interstitial ads|Showing Interstitial Videos]] that allows you to reward your app's users with the app's virtual currency upon completion of an ad. AdColony V4VC does not keep track of your users' currency balances for you; it provides notifications to you when a user needs to be credited with a reward.
###Basics###
####Step 1: Configure AdColony####
First, make sure you have imported the AdColony library:
```java
import com.jirbo.adcolony.*;
```
Next, in your **main Activity's** onCreate method, call configure like so:
```java
AdColony.configure(this, client_options, app_id, zone_ids);
```
Replace client_options with your client options String (e.g. "version:2.1,store:google" - see [[API Details]] for more information on this) and app_id/zone_ids with your app and zone ids gathered from the [Control Panel](http://clients.adcolony.com). Make sure the zone you are using to create your AdColonyV4VCAd object is V4VC enabled.<br><br>
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
####Step 3: Create AdColonyV4VCAd Object and Call Show####
To show an AdColony V4VC video advertisement, create an AdColonyV4VCAd object and call show on it as follows:
```java
AdColonyV4VCAd ad = new AdColonyV4VCAd().show();
```
or
```java
AdColonyV4VCAd ad = new AdColonyV4VCAd(v4vc_zone_id).show();
```
where v4vc_zone_id is a String matching your V4VC enabled zone gathered from the dashboard/included in your configure call.<br>
**Note:** this is a minimal example, please see below and make note of the [[API Details]] page for more advanced usage.

===
###Advanced Usage###