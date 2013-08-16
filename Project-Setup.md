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
You can do this by pasting the following lines before the <application...> tag:
```xml
<uses-­permission android:name="android.permission.INTERNET" />
<uses­-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> 
<uses-­permission android:name="android.permission.ACCESS_NETWORK_STATE" /> 
<uses-­permission android:name="android.permission.READ_PHONE_STATE" />
```