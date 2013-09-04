####Necessary Changes####
1. AdColony Android now requires OS 2.3.3 or higher to play ads.
2. AdColonyVideoListener has been renamed to AdColonyAdListener.
3. In the AdColonyAdListener interface the following methods have been renamed:
  * `onAdColonyVideoStarted() --­> onAdColonyAdStarted(ad:AdColonyAd)`
  * `onAdColonyVideoFinished() --­> onAdColonyAdAttemptFinished(ad:AdColonyAd)`
5. Class AdColonyVideoAd has been refactored into two classes: “AdColonyVideoAd” for
standard ads and “AdColonyV4VCAd” for virtual currency ads.
6. Optional ad settings are now assigned through separate chainable calls rather than
through parameters. For example, in 1.9.x call “ad.show(listener)” is now “ad.withListener(listener).show()”. For more details see [[API Details]].
8. The signatures of virtual currency query methods in AdColonyV4VCAd have changed
slightly:
  * `getV4VCName():String --­> getRewardName():String` 
  * `getV4VCAmount():int --­> getRewardAmount():int`
10. The following should be added to your application tag in your AndroidManifest.xml:
```xml
android:hardwareAccelerated="true"
```
11. Your configChanges property inside of the AdColony activity tags in your AndroidManifest.xml should now look like this (unless your project targets less than API 13 - more details available in [[Project Setup]]):
```xml
android:configChanges="keyboardHidden|orientation|screenSize"
```