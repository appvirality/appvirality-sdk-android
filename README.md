Appvirality Android SDK
=======================

<H3>Introduction:</H3>
Appvirality is a Plug and Play Growth Hacking Toolkit for Mobile Apps.

It helps to identify and implement the right growth hacks, within seconds. No Coding Required. We are providing easy to integrate SDK's for Android, iOS(coming soon) and Windows Phone(coming soon) Platforms.

Appvirality Android SDK supports from Android (API level 8) and higher.

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
    &lt;!-- Optional permissions. GET_ACCOUNTS is used to pre-populate customer's email in form fields. --&gt;
    &lt;uses-permission android:name="android.permission.GET_ACCOUNTS" /&gt;
    &lt;!-- Optional permissions. USE_CREDENTIALS is used to user experience white using twitter tweet. --&gt;
    &lt;uses-permission android:name="android.permission.USE_CREDENTIALS" /&gt;
    &lt;!-- Optional permissions. WRITE_EXTERNAL_STORAGE is used to improve the performance by storing campaign images. --&gt;
    &lt;uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /&gt;
    
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

If you don't have a Facebook App, you can create one easily by following the <a href="https://github.com/appvirality/appvirality-sdk-android/wiki/Facebook-Integration-with-Appvirality">steps to create Facebook App</a>.

Once you have your facebook app ID, you can add it to the <b>appvirality.properties</b> config file:
<pre><code>
#Appvirality App Key
appvirality.appkey = 02e1r5e99b94f56t69f42a32a00d2e7ff

#facebook
graph.facebook.com.consumer_key = 0000000000
</code></pre>
NOTE: Don't forget to replace "0000000000" with your Facebook App ID.

<H4>Initializing the Appvirality SDK</H4>

7) To use the Appvirality SDK , you must first initialize it by calling <b>AppviralityAPI.init</b> with your application context. This method in Appvirality must be called before you use other features. Please call this method on the <b>onCreate()</b> method of your Activity class.(preferably in your main application activity). 
<pre><code>
AppviralityAPI.init(getApplicationContext());
</code></pre>
And add the following line where ever you want to show your offer created from Appvirality Dashboard.
<pre><code>
AppviralityAPI.showLaunchBar(MyActivity.this);
</code></pre>

NOTE: Replace "MyActivity" with your Activity Class Name.

Now , Little clean up. Call <b>AppviralityAPI.onStop()</b> in your Activity <b>onStop()</b> method.
<pre><code>
@Override
	protected void onStop() {
		super.onStop();
		AppviralityAPI.onStop();
	}
</code></pre>

<H4>Finished Integration</H4>

Congratulations!
You have successfully completed the integration process. 

<H4>Whats Next</H4>

Sitback and witch Appvirality in action by creating the campaigns from <a href="http://www.appvirality.com/DashBoard">Appvirality Dashboard.</a>

<H3>Proguard Configuration</H3>

If you use proguard with your application, there are a set of rules that you will need to include to get Appvirality to work. Appvirality will not function correctly if proguard obfuscates its classes.

<pre><code>
# Add the Appvirality JAR file as a library jar
-libraryjars libs/AppviralitySDK.jar

-keep class com.appvirality.android.** { *; }
-dontwarn com.appvirality.android.**
</code></pre>

<H3>[Optional]Custom UI & Launch Growth Hack on Custom Event</H3>

You can also launch the Growth Hack screen when a user taps on a button or any other event. You can simply call showGrowthHackScreen() method to launch GrowthHack screen.

Let's say you want to Launch GrowthHack screen on button click , use following code

<pre><code>
// Handle onClick event of your custom UI to launch the Growth Hack screen       
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

Before presenting your custom UI i.e button or some custom UI, please check for campaign availability using <code>AppviralityAPI.isCampaignReady</code>. <code>isCampaignReady</code> returns true, if Campaigns details and associated images downloaded from server on background thread.

<pre><code>
// Check for campaign availability 
if(AppviralityAPI.isCampaignReady())
{
 myCustomButton.setText(AppviralityAPI.launchMessage);
 // make your button or custom UI visible, since we have everything ready.
 myCustomButton.setVisibility(View.VISIBLE);
}
else
{
// makes button or custom UI invisible, and it doesn't take any space for layout purposes.
 myCustomButton.setVisibility(View.GONE);
}
</code></pre>

<H3>[Optional]Handle "Remind Me Later"</H3>

If user clicks on RemindMeLater for a campaign then he will be presented the same growth hack after 1 day by default. This value is configurable, you can set "after how many days" you want to show the same campaign to that user.

If you are implementing your own UI to launch the growth hack, you may want to pass the "RemindMeLater" click event to record that user action & user want to see the growth hack later.

<pre><code>
// Handle RemindMeLater and Pass the event to Appvirality SDK       
remindMeLaterButton.setOnClickListener(new OnClickListener()
{
    @Override
    public void onClick(View view)
    {
        Appvirality.remindLater(); 
        //Hide your custom UI
        myCustomButton.setVisibility(View.GONE);
    }
}
);
</code></pre>

<H3>[Optional]Event Listener on Campaign Availability</H3>

This is useful when you are implementing "Launch Growth Hack on Custom Event". 
Appvirality SDK fetches available campaigns and images asynchronously. You can get notified whenever campaign details are available. To get notified please implement <code>CampaignHandlerInterface</code> interface and set the handler for event listener <code>AppviralityAPI.setHandlerListener</code>.

For Example you want to show your custom event UI based on campaign details availability, follow the given sample
<pre><code>
// implement "CampaignHandlerInterface" interface to handle the event
AppviralityAPI.CampaignHandlerInterface setListener = new AppviralityAPI.CampaignHandlerInterface() {   
   @Override
   public void onCampaignReady() {
    myCustomButton.setText(AppviralityAPI.getLaunchMessage());
    myCustomButton.setVisibility(View.VISIBLE);   
   }
  };
  
// Check if campaign available and if campaign not available, subscribe to event listener
if(AppviralityAPI.isCampaignReady())
  {
   myCustomButton.setText(AppviralityAPI.getLaunchMessage());
   myCustomButton.setVisibility(View.VISIBLE);  
  }
  else
  {
   myCustomButton.setVisibility(View.GONE);
   //set the handler for event listener
   AppviralityAPI.setHandlerListener(setListener);
  }

</code></pre>

<H3>[Optional]Exclude Premium Users</H3>

Premium app users can be excluded from showing growth hacks. At the time of initializing the Appvirality SDK, you can set the property <code>isPremiumUser</code>

<pre><code>
<s>AppviralityAPI.init(getApplicationContext());</s>
AppviralityAPI.isPremiumUser = Premium.Yes;
</code></pre>
<H3>[Optional]Custom Fonts</H3>

If you are using any custom fonts in your app, you can set the same to your Appvirality SDK. This makes the GrowthHack UI screens look more native to your mobile app.

1) Make sure that your custom font files are in "assets" folder

![Alt text](images/custom-fonts.jpg?raw=true)

2) Let Appvirality SDK know your custom font Location, Font name and Font Size. You can set two font variants i.e Blod font <code>AppviralityAPI.setBoldFontStyle</code> for Titles and Normal font <code>AppviralityAPI.setNormalFontStyle</code> for description in Growth Hack Screens.

For example, if you want to set custom font located in "assets/fonts" folder with font size of "14".
This will set Growth Hack Title font & font size
<pre><code>AppviralityAPI.setBoldFontStyle("fonts/Geometric_slab_serif_703_bold.ttf", 14);</code></pre>

You an also set only font name. In this case default font size will be considered.
This will set Growth Hack Title font
<pre><code>AppviralityAPI.setBoldFontStyle("fonts/Geometric_slab_serif_703_bold.ttf");</code></pre>

This will set Growth Hack description font and normal text font
<pre><code>AppviralityAPI.setNormalFontStyle("fonts/Geometric_slab_serif_703_bold.ttf");</code></pre>

If you are not using custom fonts but using different default fonts available in android. you can switch between fonts using following code
<pre><code>AppviralityAPI.setNormalFontStyle(Typeface.SERIF, Typeface.NORMAL);</code></pre>
