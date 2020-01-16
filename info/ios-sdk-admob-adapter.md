AdMob SDK adapter
=================

If you want to use OpenX as a source of demand on AdMob via the Google
Mobile Ads SDK, you can build a custom event adapter to integrate the
OpenX Mobile iOS SDK with the Google Mobile Ads SDK. 

To help you quickly build your adapter, OpenX provides sample adapter
code for banner, interstitial display, and opt-in (rewarded) video ads
in the AdMob adapter sample app. The sample adapters are built according
to [AdMob's instructions](https://developers.google.com/admob/ios/mediation/#custom_events).

[Download OpenX AdMob Adapter](https://ssl-i.cdn.openx.com/sdks/release-4.10.0/OpenX_Mobile_SDK_iOS_AdMob_Adapter_Demo_4.10.0.zip)


1. Get the following from OpenX:
	-   OpenX Mobile iOS SDK.
	-   AdMob adapter code. 
	-   For banner and interstitial display:
	    -   OpenX ad unit ID.
	    -   OpenX delivery domain (for example, `PUBLISHER-d.openx.net`).
2. In Xcode, add `OpenXCoreSDK.framework` to your project as described in
[Integrating the SDK with your app](ios-sdk-integration.md).
3. Add the Google Mobile Ads SDK to your project according to [AdMob's instructions](https://developers.google.com/admob/ios/quick-start).
4. Add the OpenX AdMob adapters to your project:
	-   `OXMAdMobCustomEventRewardedVideo.h` and `OXMAdMobCustomEventRewardedVideo.m`
	-   `OXMAdMobCustomEventBanner.h` and `OXMAdMobCustomEventBanner.m`
	-   `OXMAdMobCustomEventInterstitial.h` and `OXMAdMobCustomEventInterstitial.m`
	-   `OXMAdMobCustomEventInterstitialVideo.h` and `OXMAdMobCustomEventInterstitialVideo.m`
5. In the AdMob UI, choose the mediation group to which you will add OpenX. For example, if you want to mediate OpenX rewarded video ads, choose an iOS rewarded video mediation group that you have created.
6. In the AdMob UI, in the mediation group, define a custom event. Use the
following settings:

	-   **Label**: a label of your choice to describe this OpenX custom event.
	-   **eCPM**: an estimate of the revenue you receive for every thousand ad impressions.
	-   **Class Name**: the class name of your custom event adapter, for example, `OXMAdMobCustomEventRewardedVideo`.
	-   **Parameter**: the OpenX ad unit ID and delivery domain:
	    
	     -   Format for banner, interstitial and vido ads:
				
        ``` 
        {
            "AD_UNIT_ID": "[OPENX AD UNIT]", 
            "AD_DOMAIN": "[OPENX DELIVERY DOMAIN]"
        }           
        ```
              
        For example:
	    
        ``` 
        {
            "AD_UNIT_ID": "123456789"
            "AD_DOMAIN: "pub-d.openx.net"	
        }           
        ```
	    -   For OpenX SDK **4.9** format for video interstitial and opt-in video ads is:
    
        ```
        "[OPENX VAST URL]"
        ```
		
        For example:
    
        ```
        "http://pub-d.openx.net/v/1.0/av?auid=123456789"
        ```
7. Save the custom event and the mediation group.
8. Create a separate custom event for each ad format that you decide to use, such as banner, interstitial display, and rewarded video.
9. [Test](ios-sdk-self-test.md) your implementation and notify OpenX to
enable live traffic.
