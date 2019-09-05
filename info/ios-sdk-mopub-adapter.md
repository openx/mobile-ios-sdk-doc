MoPub SDK adapter
=================

If you want to use OpenX as a source of demand on MoPub via the MoPub
SDK, you can build an adapter to integrate the OpenX Mobile iOS SDK with
the MoPub SDK.

To help you quickly build your adapter, OpenX provides sample adapter
code for banner, interstitial, video interstitial, and opt-in (rewarded)
video.

[Download OpenX MoPub Adapter](https://ssl-i.cdn.openx.com/sdks/OpenX_Mobile_SDK_iOS_MoPub_Adapter_Demo_4.10.0.zip)

 The sample adapters are built according to [MoPub's instructions](https://www.mopub.com/resources/docs/mopub-network-mediation/writing-custom-events-for-non-supported-networks-ios/).
You will need to customize the adapters to meet your needs as instructed
below.

1. Add `OpenXCoreSDK.framework` to your project.
2. Add the MoPub SDK to your project according to [MoPub's instructions](https://www.mopub.com/resources/docs/ios-sdk-integration/ios-getting-started/).
3. Add the OpenX MoPub adapters to your project:
    -   `OXMMoPubBannerAdapter.h` and `OXMMoPubBannerAdapter.m`
    -   `OXMMoPubInterstitialAdapter.h` and `OXMMoPubInterstitialAdapter.m` 
    -   `OXMMoPubVideoInterstitialAdapter.h` and `OXMMoPubVideoInterstitialAdapter.m`
    -   `OXMMoPubRewardedVideoAdapter.h` and `OXMMoPubRewardedVideoAdapter.m`
4. In the MoPub web interface, in an order, create a network line item using the **Custom Native Network** type. In the **Custom Class** field, enter the class name of your custom event (for example, `OXMMoPubBannerAdapter`).
5. In the **Data** field, use the following formats:

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
    -   For OpenX SDK **4.9** Format for video interstitial and opt-in video ads is:
        
        ```
        {
            "VAST_URL": "[OPENX VAST URL]"
        }
        ```
        
        For example:
        
        ```
        {
            "VAST_URL": "http://pub-d.openx.net/v/1.0/av?auid=123456789"
        }
        ```
    
6. Select the app and ad unit for the line item to target.
7. If using multiple adapters (banner, interstitial, video interstitial, and/or opt-in video), create a separate line item for each adapter.
8. [Test](ios-sdk-self-test.md) your implementation and notify OpenX to enable live traffic.
