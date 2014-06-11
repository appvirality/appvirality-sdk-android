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

2) We are providing SDK in the form of <b>jar</b> file. Simply copy the <b>AppviralitySDK.jar</b> into your <b>libs</b> folder of Android eclipse project.

![Alt text](images/Add-Appvirality-SDK-to-libs.jpg?raw=true)

<H4>Set up your Appvirality Keys</H4>

3) Once you have registered on Appvirality.com website and added a new app, you will be given an App key.

![Alt text](images/App-key-obtaining.jpg?raw=true)

4) Create a configuration file in the <b>assets</b> path of your project called <b>appvirality.properties</b>

![Alt text](images/setup-av-keys.jpg?raw=true)

   Within this file, enter your Appvirality App key:
   
<pre><code>
#Appvirality App Key
appvirality.appkey = 02e1r5e99b94f56t69f42a32a00d2e7ff
</code></pre>

NOTE: Don't forget to replace the key "02e1r5e99b94f56t69f42a32a00d2e7ff" with your App key.

<H4>Configure your AndroidManifest.xml</H4>

5) Add the following lines to your AndroidManifest.xml within the 
<code>&lt;manifest...&gt;</code>

<pre><code>
&lt;manifest...&gt;

   &lt;uses-sdk android:minSdkVersion="8" android:targetSdkVersion="19" /&gt;

    &lt;uses-permission android:name="android.permission.INTERNET" /&gt;
    &lt;uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /&gt;       
    &lt;uses-permission android:name="android.permission.GET_ACCOUNTS" /&gt;
    &lt;uses-permission android:name="android.permission.USE_CREDENTIALS" /&gt;
    
     <application.../&gt;

&lt;/manifest&gt;
</code></pre>
Add the following lines to your AndroidManifest.xml within the <code>&lt;application...&gt;</code> element

<pre><code>
        &lt;!-- This activity required to identify campaign participants with Facebook Authorization. --&gt;
        &lt;activity
            android:name="com.appvirality.android.AuthorizeFacebook"
            android:theme="@android:style/Theme.NoDisplay" /&gt;

        &lt;!--This receiver will allow your application to record referrer parameters to 
                                                           track your app downloads--&gt;
        &lt;receiver
            android:name="com.appvirality.android.AppviralityInstallReferrerReceiver"
            android:exported="true" &gt;
            &lt;intent-filter&gt;
                &lt;action android:name="com.android.vending.INSTALL_REFERRER" /&gt;
            &lt;/intent-filter&gt;
        &lt;/receiver&gt;
</code></pre>

<H4>Configure Facebook Integration</H4>

6) To use Facebook as a action type (share to claim coupon, etc) in your campaign, you will need a Facebook App ID.
If you already have a Facebook App, you may want to verify the Facebook App creation process once again <a href="https://github.com/appvirality/appvirality-sdk-android/wiki/Facebook-Integration-with-Appvirality">here</a>. 

If you don't have a Facebook App, you can create one easily by followig the <a href="https://github.com/appvirality/appvirality-sdk-android/wiki/Facebook-Integration-with-Appvirality">steps to create Facebook App</a>.

Once you have your facebook app ID, you can add it to the <b>appvirality.properties</b> config file:
<pre><code>
#Appvirality App Key
appvirality.appkey = 02e1r5e99b94f56t69f42a32a00d2e7ff

#facebook
graph.facebook.com.consumer_key = 0000000000
</code></pre>
NOTE: Don't forget to replace "0000000000" with your Facebook App ID.

<H4>Initializing the Appvirality SDK</H4>

7) To use the Appvirality SDK , you must first initialize it by calling <b>AppviralityAPI.init</b> with your application context. This method in Appvirality must be called before you use other features. Please call this method on the <b>onResume()</b> method of your Activity class.(preferably in your main application activity). 
<pre><code>
AppviralityAPI.init(getApplicationContext());
</code></pre>
And add the following line where ever you want to show your offer created from Appvirality Dashboard.
<pre><code>
AppviralityAPI.showLaunchBar(MyActivity.this);
</code></pre>

NOTE: Replace "MyActivity" with your Activity Class Name.

<H4>Finished Integration</H4>

Congratulations!
You have successfully completed the integration process. 

<H4>Whats Next</H4>

Sitback and witch Appvirality in action by creating the campaigns from <a href="http://appvirality.com/DashBoard">Appvirality Dashboard.</a>

<H3>Proguard Configuration</H3>

If you use proguard with your application, there are a set of rules that you will need to include to get Appvirality to work. Appvirality will not function correctly if proguard obfuscates its classes.

<pre><code>
# Add the Appvirality JAR file as a library jar
-libraryjars libs/AppviralitySDK.jar

-keep class com.appvirality.android.** { *; }
-dontwarn com.appvirality.android.**
</code></pre>

<H3>[OPTIONAL]Launch Growth Hack Screen on Custom Event</H3>

You can also launch the Growth Hack screen when a user taps on a button or anyother event. You can simply call showGrowthHackScreen() method to launch GrowthHack screen.

Lets say you want to Launch GrowthHack screen on button click , use following code

<pre><code>
// Integrate GrowthHack Screen into a button on your view       
myCustomButton.setOnClickListener(new OnClickListener()
{
    @Override
    public void onClick(View view)
    {
        Appvirality.showGrowthHackScreen(MyActivity.this);                
    }
}
);
</code></pre>



