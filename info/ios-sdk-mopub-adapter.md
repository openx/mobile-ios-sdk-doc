MoPub SDK adapter
=================

If you want to use OpenX as a source of demand on MoPub via the MoPub
SDK, you can build an adapter to integrate the OpenX Mobile iOS SDK with
the MoPub SDK.

To help you quickly build your adapter, OpenX provides sample adapter
code for banner, interstitial, video interstitial, and opt-in (rewarded)
video.

[Download OpenX MoPub Adapter](http://sdk.prod.gcp.openx.org/ios/4.11.0/OpenX_Mobile_SDK_iOS_MoPub_Adapter_Demo_4.11.0.zip)

 The sample adapters are built according to [MoPub's instructions](https://www.mopub.com/resources/docs/mopub-network-mediation/writing-custom-events-for-non-supported-networks-ios/).
You will need to customize the adapters to meet your needs as instructed
below.

1. Add `OpenXCoreSDK.framework` to your project.
2. Add the MoPub SDK to your project according to [MoPub's instructions](https://www.mopub.com/resources/docs/ios-sdk-integration/ios-getting-started/).
3. Add the `OXMMoPubAdapterConfiguration` class to your project
3. Add the OpenX MoPub adapters to your project:
    -   `OXMMoPubAdapterConfiguration.h` and `OXMMoPubAdapterConfiguration.m`
    -   `OXMMoPubBannerAdapter.h` and `OXMMoPubBannerAdapter.m`
    -   `OXMMoPubInterstitialAdapter.h` and `OXMMoPubInterstitialAdapter.m`
    -   `OXMMoPubVideoInterstitialAdapter.h` and `OXMMoPubVideoInterstitialAdapter.m`
    -   `OXMMoPubRewardedVideoAdapter.h` and `OXMMoPubRewardedVideoAdapter.m`
4. In the MoPub web interface, in an order, create a network line item using the **Custom Native Network** type. In the **Custom Class** field, enter the class name of your custom event (for example, `OXMMoPubBannerAdapter`).
5. In the **Data** field, use the following formats:

    -   Format for banner, interstitial and video ads:

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


Enabling Video Pre-Caching
========
To enable the video pre-chaching, add OXMMoPubAdapterConfiguration to your project and pass the JSON-based ad configurations string to the `MPMoPubConfiguration`:

```json
{
  "precache_configuration":
  [
    {
      "domain":"YOUR_DOMAIN",
      "auid":"YOUR_AUID",
      "pgid": "YOUR_PGID"
    }
  ]
}
```

The code sample:

``` swift
let mopubConfig = MPMoPubConfiguration(adUnitIdForAppInitialization: "")
mopubConfig.loggingLevel = .info
mopubConfig.additionalNetworks = [OXMMoPubAdapterConfiguration.self]

let preloadConfig = """
{
  "precache_configuration":
  [
    {
      "domain":mobile-d.openx.net",
      "auid":"540397906",
    }
  ]
}
"""
mopubConfig.setNetwork([OXM_MOPUB_INITIALIZATION_OPTIONS_KEY: preloadConfig], forMediationAdapter: "OXMMoPubAdapterConfiguration")
```
