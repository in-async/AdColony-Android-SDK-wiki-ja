AdColony delivers high-definition Instant-Play video ads that can be displayed anywhere within your application. AdColony also contains V4VC, a secure system for rewarding users of your app with virtual currency upon the completion of video plays. 

===
###Notes###
* Our current version of the AdColony Android SDK is 2.1.2.
* The minimum Android OS on a specific device to ensure AdColony Ad playback is 2.3.3 (API 10).
* The minimum memory class (per-app memory limit) for a specific device to play AdColony Ads is 32MB.  An older device with a smaller memory class will never play ads.
* If your application targets API 18+ and you have ProGuard enabled, you will not be able to export a signed APK unless you add the following line to your proguard-project.txt file: `-dontwarn android.webkit.**`
* Google Advertising Id will be collected as long as you've added Google Play Services into your project. Android Id will only be collected when the Google Advertising Id is not available.
* Please see our page regarding data collection [here](http://support.adcolony.com/customer/portal/articles/1605954-data-and-clickstream-collection).

===
###Contents###
* [[Project Setup]]
* [[Showing Interstitial Videos]]
* [[Showing V4VC Videos]]
* [[Showing Instant-Feed™ Videos]]
* [[API Details]]
* [[Change Logs]]