**2.0.3 (Beta) - August 20, 2013**<br>
1. Dynamic end card related WebView bug fixes.

===
**2.0.2 (Beta) - August 9, 2013**<br>
1. Ad specific play limits now function off of starts rather than completes.<br>
2. General bug fixes.

===
**2.0.1 (Beta) - July 16, 2013**<br>
1. AdColony now uses SSL for ad configuration downloads.<br>
2. Fixed video request tracking.<br>
3. Added functionality for restricting ads and caching based on network type.<br>
4. Changes to overlay button scaling and sensitivity.<br>
5. Added support for self-hosted HTML5 video playing triggered by dynamic end card engagement.<br>
6. Other general dynamic end card related bug fixes.

===
**2.0.0 (Beta) – June 6, 2013** <br>
1. AdColony Android now requires OS 2.2 or higher.<br>
2. AdColonyVideoListener has been renamed to AdColonyAdListener.<br>
3. In the AdColonyAdListener interface the following methods have been renamed:<br>
`onAdColonyVideoStarted() --­> onAdColonyAdStarted(ad:AdColonyAd)`<br>
`onAdColonyVideoFinished() ­--> onAdColonyAdAttemptFinished(ad:AdColonyAd)`<br>
4. When onAdColonyAdAttemptFinished() is called, the AdColonyAd parameter may be
queried for the status using one of the following methods:<br>
`shown():boolean // returns true if an ad was shown as expected`<br> 
`canceled():boolean // true if a V4VC ad was user-­canceled before being shown`<br> 
`noFill():boolean // true if no ad fill was available`<br>
`skipped():boolean // true if a skippable video ad was skipped during play`<br>
5. Class AdColonyVideoAd has been refactored into two classes: “AdColonyVideoAd” for
standard ads and “AdColonyV4VCAd” for virtual currency ads.<br>
6. Optional ad settings are now assigned through separate chainable calls rather than
through parameters. For example, in 1.9.x call “ad.show(listener)” is now “ad.withListener(listener).show()”. For more details see [[API-Details]].<br>
7. getAvailableViews():int is a new method available in both AdColonyVideoAd and
AdColonyV4VCAd. It returns the guaranteed number of ads that are available at a given
time. This replaces getV4VCAvailable():boolean in 1.x.<br>
8. The signatures of virtual currency query methods in AdColonyV4VCAd have changed
slightly:<br>
`getV4VCName():String --­> getRewardName():String`<br>
`getV4VCAmount():int --­> getRewardAmount():int`<br>
9. AdColony 2.0 supports fractional currency implemented as a number ad views required to receive the reward. AdColonyV4VCAd has the following new methods:<br>
`getViewsPerReward():int`<br>
`getRemainingViewsUntilReward()`<br>
10. The following application tag should be added to your AndroidManifest.xml:
```xml
android:hardwareAccelerated="true"
```