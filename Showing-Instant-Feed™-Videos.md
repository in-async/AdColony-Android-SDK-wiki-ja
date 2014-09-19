**If you are interested in integrating Instant-Feed™ ads into your app, please contact us at support@adcolony.com.**

**In order to comply with contractual requirements regarding implementation and valid impressions, we require the following from Publishers:
1. The video player must be in a viewable area and nothing should be covering it.
2. Ads will automatically start/pause/resume in accordance with contractual requirements. No unauthorized tactics may be used to alter this behavior<br>

Note: For those also developing for iOS, you must manage start/resume and pause behavior in your implementation on that platform.**

AdColony Instant-Feed™ is a new ad unit that allows you to blend AdColony ads directly into your app’s content, closely matching the form and function of your existing user experience. Prior to Instant-Feed™, all AdColony ads were displayed as full-screen interstitials. 

Instant-Feed™ ads consist of two experiences: the first is the native experience where the AdColony SDK provides text, images, and a native video container that you use to construct your customized native ad experience. The second is triggered if a user taps on the video container, at which point the AdColony SDK will display a full-screen interstitial experience automatically.
<div align="center">
<img src="assets/IFExample.png" alt="Instant-Feed Example"/>
</div>

###Instructions###
Once you've performed the required [[Project Setup]], you can display an AdColony Instant-Feed™ ad in your app by following these steps:
####Step 1: Configure AdColony####
First, make sure you have imported the AdColony library:
```java
import com.jirbo.adcolony.*;
```
Next, in your **main Activity's** onCreate method, call configure like so:
```java
AdColony.configure(this, client_options, app_id, zone_ids);
```
Replace client_options with your client options String (e.g. "version:2.1,store:google" - see [[API Details]] for more information on this) and app_id/zone_ids with your app and zone ids gathered from the [Control Panel](http://clients.adcolony.com) (please refer to "[Setting up Apps and Zones](http://support.adcolony.com/customer/portal/articles/761987-setting-up-apps-zones)" for help).<br><br>
**Note:** you should only ever call configure **once** and make sure it is done in your **launching Activity's** onCreate method.

===
####Step 2: Pause and Resume####
Override each of your Activities' onPause() and onResume() methods to call corresponding AdColony methods as follows:
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
####Step 3: Create AdColonyNativeAdView Object####
Next you'll need to request an AdColonyNativeAdView object and create it's placement in your application's layout. For best performance, the following steps should not take place on the UI thread (AsyncTasks are great for this.) **If you will be adding the ad unit into a ListView, make sure to call the prepareForListView() method**
```java
AdColonyNativeAdView ad = new AdColonyNativeAdView(activity, zone_id, width);
ad.prepareForListView(); //Call this if you will be adding into a ListView
if (ad.isReady())
{
  //Continue at Step 4
}
```

Where activity is your Activity reference, zone_id is a String matching a specific zone gathered from the dashboard and included in your configure call, and width is the integer width of the ad unit desired. If the ad is ready you can begin construction of your placement.

===
####Step 4: Retrieve More Information to Include in Your Placement####
Use the public API to retrieve more information to complete your ad placement:
```java
ad.getAdvertiserName(); //Required
ad.getAdvertiserImage(); //Optional
ad.getTitle(); //Optional
ad.getDescription(); //Optional
```

===
####Step 5: Include a Sponsored Content Indicator####
Ensure that your ad placement includes some text (and an optional image) indicating that the content is paid/sponsored by the advertiser. A simple example of this can be seen in the provided demo application.

===
####Step 6: Insert Ad Unit Into Your Layout####
When you have completed the construction of your ad unit, add it to your layout and it will begin playback once it is rendered on screen. Please note that AdColonyNativeAdView objects can only be used in a hardware accelerated window.

===
####Step 7: Removing the Ad Unit####
When you are completely finished using the ad unit (i.e. replacing it with a new one or otherwise permanently removing from your layout) be sure to call destroy() after removing it:
```java
ad.destroy();
```
This will remove our internal reference to this object such that the memory can be freed via GC.<br><br>

**Note:** this is a minimal example, please make note of the [[API Details]] and the demo project included in the distribution for more advanced usage.