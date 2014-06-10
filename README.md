Appvirality Android SDK
=======================

<H3>Introduction:</H3>
Appvirality is a Plug and Play Growth Hacking Toolkit for Mobile Apps.

It helps to identify and implement the right growth hacks, within seconds. No Coding Required. We are providing easy to integrate SDK's for Android, iOS(coming soon) and Windows Phone(coming soon) Platforms.

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

NOTE: Don't forget to replace the key "02e1r5e99b94f56t69f42a32a00d2e7ff" with your App key.

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
&lt;!-- This activity required to identify campaign participants with Facebook Authorization.--&gt;
 &lt;activity android:name="com.appvirality.android.AuthorizeFacebook" 
                                  android:theme="@android:style/Theme.NoDisplay" /&gt;
&lt;!-- This receiver will allow your application to record referrer
             parameters to track your app downloads --&gt;                                  
&lt;receiver android:name="com.appvirality.android.AppviralityInstallReferrerReceiver"
                                  android:exported="true"&gt;
    &lt;intent-filter&gt;
         &lt;action android:name="com.android.vending.INSTALL_REFERRER" /&gt;
    &lt;/intent-filter&gt;
&lt;/receiver&gt;
</code>
</pre>

<H4>Configure Facebook Integration</H4>

6) To user facebook in your Appvirality campaign as an <b>action</b>(i.e coupon unlocking action) , you will need a Facebook App ID.
If you already have a Facebook App, you can verify the Facebook App creation process once again <a href="#">here</a>

Once you have your facebook app ID, you can add it to the <b>oauth_consumer.properties</b> config file:
<pre>
<code>
#Appvirality App Key
appvirality.appkey = 02e1r5e99b94f56t69f42a32a00d2e7ff

#facebook
graph.facebook.com.consumer_key = 0000000000
</code>
</pre>
NOTE: Don't forget to replace "0000000000" with your Facebook App ID.

<H4>Include Appvirality in Your App</H4>

Now you have done all the configurations required. It's time to include Appvirality into your App

Just add the following line of code in your project(preferably in MainActivity.java). 
<pre>
<code>
AppviralityAPI.Initialize(context);
</code>
</pre>
And add the following line where ever you want to show your offer created from Appvirality Dashboard.
<pre>
<code>
AppviralityAPI.showLaunchBar(ClassName.this);
</code>
</pre>

NOTE: Replace "ClassName" with your Activity Class Name where you are calling "ShowLaunchBar".

Boom..Sitback and witch the show by creating the campaigns from Appvirality Dashboard. 


