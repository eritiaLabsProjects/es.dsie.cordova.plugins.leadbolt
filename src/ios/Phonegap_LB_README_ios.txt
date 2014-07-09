READ ME - LeadBolt iOS Cordova/Phonegap library

Version 2.0      date: 2014-02-10
================================================================================================================== 

Scope
--------
This zip package provides a wrapping library to allow Phonegap users on iOS to include the LeadBolt SDK within their Applications.

Requirements
------------

1. You must have a LeadBolt app publisher account (http://www.leadbolt.com)

2. You must have accessed your leadbolt account to register your android app and have created ads, retrieved the relevant section ids.

3. From the help/faq section of the leadbolt portal, you must have downloaded the latest (version 4.01 and above) LeadBolt iOS publisher SDK.

Integration
------------
The following steps need to be followed in xCode (v5 and above)

1. Unzip and copy the LeadBolt iOS SDK (lb_ios_sdk_v4.1 zip file) into your xcode project. This should contain both the libLeadboltOverlay.a and the LBHeaders folder containing JSONKit.h, JSONKit.m and LeadboltOverlay.h files

2. Unzip and copy the LeadBolt iOS Phonegap Plugin (lb_ios_sdk_phonegap_v2.00 zip file) into your xcode project. This should contain the libLBPhonegapPlugin.a, LBPhonegapPlugin.h and AdController.js files.

3. Go to the "Build Phases" of your Project's Target and under "Compile Sources", double click on the JSONKit.m file and enter the following: "-fno-objc-arc" (without quotes).

3. Edit the config.xml of your Phonegap Project. Add the following lines along with the other features already defined there:
	<feature name="AdController">
		<param name="ios-package" value="LBPhonegapPlugin" />
		<param name="onload" value="true" />
	</feature>

4. In the config.xml file, please make sure <access> tag is set to the following:
	<access origin="*" />

5. Move the AdController.js file into the "www/js" foldeer in your PhoneGap Project. Next add the following javascript jag in your index.html file
	<script type="text/javascript" src="js/AdController.js"></script>

6. Now in your index.html file add the following line:

    document.addEventListener('deviceready', function() {
        loadLeadBolt();
    }, false);

    function loadLeadBolt()
    {
        AdController.loadAd("YOUR_LB_SECTION_ID");

        // Optional paramaters for Ad Display
        // AdController.setLandscapeMode("1"); // 0 for Portrait mode
        // AdController.setLocationControl("1"); // To try and serve location specific Ads to the User

        // to load an Audio Ad
        AdController.loadAudioAd("YOUR_LB_AUDIO_ID");

        // to load an Audio Track
        AdController.loadAudioTrack("YOUR_LB_AUDIO_ID", 2);

        // to load a App Re-Engagement
        AdController.loadReEngagement("YOUR_LB_REENGAGEMENT_ID");

        // to load a Quick Start Ad
        AdController.loadStartAd("YOUR_LB_SECTION_ID", "YOUR_LB_REENGAGEMENT_ID", "YOUR_LB_AUDIO_ID");
    }

7. To Destroy Ad add the following line to your code
    AdController.destroyAd();

8. Display Ad Advanced Option - To cache an Audio Ad, call the following line of code in your JavaScript code at the start of your App.
    AdController.loadAdToCache("YOUR_LB_SECTION_ID");

    Then simply, at a specific point in your App, call this line of JavaScript:  AdController.displayAd();
    
9. Audio Ad Advanced Option - To cache an Audio Ad, call the following line of code in your JavaScript code at the start of your App.
    AdController.loadAdToCache("YOUR_LB_AUDIO_ID");

    Then simply, at the specific point in your App, call this line of JavaScript:  AdController.playAudio();


Going Live 
-----------
Once your app is working you can now go-live with real ads.

1. Access the LeadBolt publisher portal and for your app click the go-live button if present.

2. Your app will be submited for approval and once approved will receive live ads.