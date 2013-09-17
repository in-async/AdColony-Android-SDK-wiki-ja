**Special Note:** If your application targets API 18 and you have ProGuard enabled, you will not be able to export a signed APK unless you add the following line to your proguard-project.txt file:`-dontwarn android.webkit.**`<br><br>
There are 3 quick steps that must be taken prior to integrating AdColony video ads into your source code:
####Step 1: Insert Library####
* Place adcolony.jar in your project’s "libs" folder.
  * The adcolony.jar library can be found in the distribution's "Library" folder.

=== 
####Step 2: Edit Manifest####
Ensure the following 4 permissions are set in your project's "AndroidManifest.xml":<br><br>
1. INTERNET<br>
2. WRITE_EXTERNAL_STORAGE<br>
3. ACCESS_NETWORK_STATE<br>
4. READ_PHONE_STATE <br><br>
You can do this by pasting the following lines before the \<application...> tag:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> 
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> 
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```
In order for our Dynamic End Cards to perform optimally, please enable hardware acceleration by adding the following line to your application tag in your manifest:<br>
```xml
android:hardwareAccelerated="true"
```
Next, copy and paste the following three activity definitions just before the end application tag near the bottom:
```xml
<activity android:name="com.jirbo.adcolony.AdColonyOverlay"
android:configChanges="keyboardHidden|orientation|screenSize"
android:theme="@android:style/Theme.Translucent.NoTitleBar.Fullscreen" />

<activity android:name="com.jirbo.adcolony.AdColonyFullscreen"
android:configChanges="keyboardHidden|orientation|screenSize"
android:theme="@android:style/Theme.Black.NoTitleBar.Fullscreen" />

<activity android:name="com.jirbo.adcolony.AdColonyBrowser"
android:configChanges="keyboardHidden|orientation|screenSize"
android:theme="@android:style/Theme.Black.NoTitleBar.Fullscreen" />
```
**Note:** if your application targets below API 13, you will likely need to remove screenSize from the configChanges property of the above activity tags.

===
####Step 3: Gather Information From Your AdColony Account####
Log in to the AdColony [Control Panel](http://clients.adcolony.com) and create an app and desired zones on the website by following the instructions provided there (please refer to "[Setting up Apps and Zones](http://support.adcolony.com/customer/portal/articles/761987-setting-up-apps-zones)" for help). Then retrieve your app ID and your corresponding zone IDs for integration (see [[Showing Interstitial Videos]] and [[Showing V4VC Videos]]).