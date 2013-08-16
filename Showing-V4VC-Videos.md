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

_[http://www .yourserver.com/anypath/callback_url.php]?id=[transaction id]&uid=[user id]&amount=[currency amount to award]&currency=[name of currency to award]&verifier=[security value]_<br><br>

If your application provides a custom ID to AdColony, you will need to add “&custom_id=[CUSTOM_ID]” to your zone’s callback URL or it will not be provided to your server.<br><br>

It is not necessary to use PHP for your callback URL. You can use any server side language that supports an MD5 hash check to respond to URL requests on your server.<br><br>

For your convenience, the following PHP with MySQL sample code illustrates how to access the URL parameters, perform an MD5 hash check, check for duplicate transactions, and how to respond appropriately from the URL:
```php
$MY_SECRET_KEY="Thiscomesfromadcolony.com";

$trans_id=mysql_real_escape_string($_GET['id']); 
$dev_id=mysql_real_escape_string($_GET['uid']); 
$amt=mysql_real_escape_string($_GET['amount']); 
$currency=mysql_real_escape_string($_GET['currency']); 
$verifier=mysql_real_escape_string($_GET['verifier']);

//verify hash 
$test_string="".$trans_id.$dev_id.$amt.$currency.$MY_SECRET_KEY; 
$test_result=md5($test_string);
if($test_result!=$verifier)
{
  echo"vc_decline";
  die; 
}

//check for a valid user 
$user_id=//get your internal user id from the device id here 
if(!$user_id)
{
  echo"vc_decline";
  die; 
}
//insert the new transaction 
$query="INSERT INTO AdColony_Transactions(id,amount,name,user_id,time)".
  "VALUES($trans_id,$amt,'$currency',$user_id,UTC_TIMESTAMP())"; 
$result=mysql_query($query);
if(!$result)
{
  //check for duplicate on insertion 
  if(mysql_errno()==1062)
  {
    echo"vc_success";
    die; 
  }
  //otherwise insert failed and AdColony should retry later 
  else
  {
    echo"mysql error number".mysql_errno();
    die; 
  }
}
//award the user the appropriate amount and type of currency here 
echo"vc_success";
```
The MySQL database table referenced by the previous PHP sample can be created using the following code:
```mysql
CREATE TABLE `AdColony_Transactions` (
`id` bigint(20) NOT NULL default '0',
`amount` int(11) default NULL,
`name` enum('Currency Name 1') default NULL, `user_id` int(11) default NULL,
`time` timestamp NULL default NULL,
PRIMARY KEY (`id`)
) ENGINE=MyISAM DEFAULT CHARSET=latin1;
```
To prevent duplicate transactions, you must make a record of the id of every transaction received, and check each incoming transaction id against that record after verifying the parameters. If a transaction is a duplicate, there is no need to reward the user, and you should return a success condition.<br><br>
After checking for duplicate transactions, you should reward your user the specified amount of the specified type of currency.

===
####Step 3####
You must ensure your callback returns the appropriate string to the AdColony server based on the result of the transaction:<br>
* "vc_success"
  * Transaction finished. Return this when the callback is received and user credited.
* "vc_decline"
  * Transaction finished. Return this when the uid is not valid or the security check is not passed.
* Anything else
  * AdColony will periodically retry to contact your server with this transaction. This should only be used in the case of some error.<br>
**Note:** The only acceptable reasons to not reward a transaction are if the uid was invalid, the security check did not pass, or the transaction was a duplicate which was already rewarded.
