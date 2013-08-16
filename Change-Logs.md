**2.0.0 (Beta) – June 6, 2013** <br>
1. AdColony Android now requires OS 2.2 or higher.<br>
2. AdColonyVideoListener has been renamed to AdColonyAdListener.<br>
3. In the AdColonyAdListener interface the following methods have been renamed:
* onAdColonyVideoStarted() --­> onAdColonyAdStarted(ad:AdColonyAd)
* onAdColonyVideoFinished() ­--> onAdColonyAdAttemptFinished(ad:AdColonyAd)
4. When onAdColonyAdAttemptFinished() is called, the AdColonyAd parameter may be
queried for the status using one of the following methods:
* shown():boolean // returns true if an ad was shown as expected 
* canceled():boolean // true if a V4VC ad was user­canceled before being shown 
* noFill():boolean // true if no ad fill was available
* skipped():boolean // true if a skippable video ad was skipped during play

5. Class AdColonyVideoAd has been refactored into two classes: “AdColonyVideoAd” for
standard ads and “AdColonyV4VCAd” for virtual currency ads.<br>
6. Optional ad settings are now assigned through separate chainable calls rather than
through parameters. For example, in 1.9.x call “ad.show(listener)” is now “ad.withListener(listener).show()”. For more details see [[API-Details]].<br>
7. getAvailableViews():int is a new method available in both AdColonyVideoAd and
AdColonyV4VCAd. It returns the guaranteed number of ads that are available at a given
time. This replaces getV4VCAvailable():boolean in 1.x.<br>
8. The signatures of virtual currency query methods in AdColonyV4VCAd have changed
slightly:
* getV4VCName():String --­> getRewardName():String 
* getV4VCAmount():int --­> getRewardAmount():int

9. AdColony 2.0 supports fractional currency implemented as a number ad views required to receive the reward. AdColonyV4VCAd has the following new methods:
* getViewsPerReward():int
* getRemainingViewsUntilReward():int

10. The following application tag should be added to your AndroidManifest.xml:
```xml
android:hardwareAccelerated="true"
```