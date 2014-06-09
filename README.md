Appvirality Android SDK
=======================

<H3>Introduction:</H3>
Appvirality is a Plug and Play Growth Hacking Toolkit for Mobile Apps.Identify and Implement the right growth hacks, within seconds. No Coding Required.

We are providing easy to integrate SDK's for Android, iOS(coming soon) and Windows Phone(coming soon) Platforms.

Integrating Appvirality into your App
-------------------------------------

<H3>Getting Started:</H3>

1) Download the latest Appvirality SDK from http://www.appvirality.com and unzip the archive.<br/>

![Alt text](images/download-SDK.jpg?raw=true "You can see this in Appvirality Dashboard")

2) We are providing SDK in the form of <b>jar</b> file. Simply copy the <b>Appvirality.jar</b> into your <b>libs</b> folder of Android eclipse project.

![Alt text](images/Add-Appvirality-SDK-to-libs.jpg?raw=true)

<H4>Set up your Appvirality Keys</H4>

3) Once you have registered on Appvirality.com website and added a new app, you will be given an App key.

![Alt text](images/App-key-obtaining.jpg?raw=true)

4) Create a configuration file in the <b>assets</b> path of your project called <b>oauth_consumer.properties</b>

![Alt text](images/setup-av-keys.jpg?raw=true)

   Within this file, enter your Appvirality App key:
   
<pre>
<code>
#Appvirality App Key
appvirality.appkey = 02e1r5e99b94f56t69f42a32a00d2e7ff
</code>
</pre>

Don't forget to replace the key "02e1r5e99b94f56t69f42a32a00d2e7ff" with your App key.

<H4>Configure your AndroidManifest.xml</H4>

5) Add the following lines to your AndroidManifest.xml within the 
<code>&lt;manifest...&gt;</code>

<pre>
<code>
&lt;manifest...&gt;

   &lt;uses-sdk android:minSdkVersion="8" android:targetSdkVersion="19" /&gt;

    &lt;uses-permission android:name="android.permission.INTERNET" /&gt;
    &lt;uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /&gt;       
    &lt;uses-permission android:name="android.permission.GET_ACCOUNTS" /&gt;
    &lt;uses-permission android:name="android.permission.USE_CREDENTIALS" /&gt;
    
     <application.../&gt;

&lt;/manifest&gt;
</code>
</pre>
Add the following lines to your AndroidManifest.xml within the <code>&lt;application...&gt;</code> element

<pre>
<code>
 &lt;activity android:name="com.appvirality.android.AuthorizeFacebook" android:theme="@android:style/Theme.NoDisplay" /&gt;
&lt;receiver android:name="com.appvirality.android.AppviralityInstallReferrerReceiver" android:exported="true" &gt;
    &lt;intent-filter&gt;
         &lt;action android:name="com.android.vending.INSTALL_REFERRER" /&gt;
    &lt;/intent-filter&gt;
&lt;/receiver&gt;
</code>
</pre>
