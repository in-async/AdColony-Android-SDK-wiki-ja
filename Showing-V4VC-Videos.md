AdColony V4VC (Videos-for-Virtual-Currency) is a system built on top of our [[interstitial ads|Showing Interstitial Videos]] that allows you to reward your app's users with the app's virtual currency upon completion of an ad. AdColony V4VC does not keep track of your users' currency balances for you; it provides notifications to you when a user needs to be credited with a reward.<br><br>
[Basics](Showing-V4VC-Videos#basics)<br>
[Advanced Usage](Showing-V4VC-Videos#advanced-usage)
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
Or
```java
AdColonyV4VCAd ad = new AdColonyV4VCAd(v4vc_zone_id).show();
```
Where v4vc_zone_id is a String matching your V4VC enabled zone gathered from the dashboard/included in your configure call.<br><br>
**Note:** this is a minimal example, please see below and make note of the [[API Details]] page for more advanced usage.

===
###Advanced Usage###
[AdColonyV4VCListener](Showing-V4VC-Videos#adcolonyv4vclistener)<br>
[Pre and Post-Popups](Showing-V4VC-Videos#pre-and-post-popups)<br>
[Server-Side Rewards](Showing-V4VC-Videos#server-side-rewards)
####AdColonyV4VCListener####
After a V4VC video plays AdColony will inform your app of the results. Create a class that implements the AdColonyV4VCListener interface and add the listener to AdColony immediately after calling configure:
```java
AdColonyV4VCListener listener = new AdColonyV4VCListener()
{
  public void onAdColonyV4VCReward(AdColonyV4VCReward reward)
  {
    //Just an example, see API Details page for more information.
    if(reward.success())
    {
      //Reward user
    }
  }
};

AdColony.addV4VCListener(listener);
```
===
####Pre and Post-Popups####
AdColony offers pre and post-popup dialogs that alert the user of your application with a confirmation and/or results message as appropriate.<br><br>
To use only pre-popups, your show method call would look like this:
```java
AdColonyV4VCAd ad = new AdColonyV4VCAd(v4vc_zone_id).withConfirmationDialog().show();
```
To use only post-popups, your show method call would look like this:
```java
AdColonyV4VC ad = new AdColonyV4VCAd(v4vc_zone_id).withResultsDialog().show();
```
And the following would be your show method call if you want to use both dialogs:
```java
AdColonyV4VC ad = new AdColonyV4VCAd(v4vc_zone_id).withConfirmationDialog().withResultsDialog().show();
```

===
####Server-Side Rewards####
To provide security for your virtual currency economy, AdColony issues callbacks which use message hashing for security directly to your servers that handle your virtual currency. In order to reward your users with the virtual currency rewarded by AdColony, you should create a callback URL on your game’s server system. AdColony will pass URL parameters to your game’s server via this URL, which are then used to update a user’s virtual currency balance in your system. <br><br>
In AdColony we have an option to enable client­-side handling of virtual currency. Please note that use of this option is not advised because there is no way to create a secure client-­side virtual currency system. While we do our best to obfuscate our client­-side system, it is not possible to ensure its security. If you are unable to use a server to manage your virtual currency system, contact support@adcolony.com for usage guidelines.
####Step 1####
You must create a URL on your servers to receive the AdColony callback. The callback URL must not require any authentication to reach your server. Once you have chosen this URL, you should input it in the video zone configuration page on the [Control Panel](http://clients.adcolony.com).

===
####Step 2####
You must make your URL respond appropriately to the AdColony callback. The format of the URL that AdColony will call is as follows, where brackets indicate strings that will vary based on your application and the details of the transaction:<br><br>

_[[http://www.yourserver.com/anypath/callback_url.php](http://www.yourserver.com/anypath/callback_url.php)<http://www.yourserver.com/anypath/callback_url.php%5D(http://www.yourserver.com/anypath/callback_url.php)>]?id=[transaction id]&uid=[user id]&amount=[currency amount to award]&currency=[name of currencyto award]&verifier=[security value]_<br><br>