# OpenX Apollo iOS SDK

The OpenX Apollo iOS SDK allows you to integrate  into your apps prebid solution hosted by OpenX to increase revenue through mobile advertising.

> **_NOTE:_**  The documentation for the legacy OpenX SDK is available [here](legacy_sdk/LEGACY_SDK_README.md).

## Getting Started

For requirements and integration overview, see [Getting Started](info/ios-in-app-bidding-getting-started.md).

The current SDK version is **1.0.0**.
Go to [release notes](info/ios-in-app-bidding-release-notes.md) for all SDK versions.

#### CocoaPods integration

To download and integrate the SDK into your project using CocoaPods, add the following line to your project’s podfile:

```
pod 'openx-apollo-sdk'
```

If you integrate Apollo with GAM or MoPub add these pods respectively

```
# + Google Ad Manager (optional)
pod 'openx-apollo-gam-event-handlers'

# + MoPub (optional)
pod 'openx-apollo-mopub-adapters'
```

#### Download SDK and demo applications

Also, you can download and integrate all needed components manually:

- [Apollo SDK](http://sdk.prod.gcp.openx.org/apollo/ios/sdk/1.0.0/OpenX_Apollo_SDK_iOS_1.0.0.zip)
- [GAM Event Handlers](http://sdk.prod.gcp.openx.org/apollo/ios/event-handlers/GAM/1.0.0/OpenX_Apollo_GAMEventHandlers_iOS_1.0.0.zip)
- [MoPub Adapters](http://sdk.prod.gcp.openx.org/apollo/ios/event-handlers/MoPub/1.0.0/OpenX_Apollo_MoPub_Adapters_iOS_1.0.0.zip)
- [Demo Application](http://sdk.prod.gcp.openx.org/apollo/ios/demo/1.0.0/OpenX_Apollo_DemoApp_iOS_1.0.0.zip)


## In-App Bidding SDK Overview

Here are key capabilities of the iOS In-App Bidding SDK:

-   **Integration Scenarios**
    - [Google Ad Manager](info/integration-gam/ios-in-app-bidding-gam-info.md)
    - [MoPub](info/integration-mopub/ios-in-app-bidding-mopub-info.md)
    - [Pure In-App Bidding](info/integration-pb/ios-in-app-bidding-pb-info.md)


<img src="info/res/IAB_Cert.png" alt="Pipeline Screenshot" height="320" width="320" align="right">


-   **Support of these premium ad formats:**
    -   Banner
    -   Interstitial
    -   Rich media and MRAID 3.0 support
    -   Video Interstitial
    -   Rewarded Video
    -   Outstream Video
-   **Open Measurement Support**. The In-App Bidding SDK is based on the former OpenX SDK which is certificated with IAB, IAS and MOAT.
-   **Direct SDK integration**. Allows you to pass first-party app data,
    user data, device data, and location data.  
-   **Privacy Regulation Compliance**. The In-App Bidding SDK meets **GDPR**, **CCPA**, **COPPA** requirements according to the IAB specifications.
-   **App targeting campaigns**. With the [support of deeplink+](info/ios-sdk-deeplinkplus.md) SDK is able to manage the ads with premium UX for retargeting campaigns.
-    **Targeting**. Use [custom ad parameters](info/ios-sdk-parameters.md) to increase the chance to win an impression and to improve ad views' UX.
-   **Tracking of render impression**. The OpenX In-App Bidding SDK tracks [render impressions](info/ios-sdk-impression-tracking.md) according to the IAB Measurement Guidelines for all managed ads. Ads rendered by Primary Ad Server SDK track an impression beacon according to the internal algorithms.
-   **Demo app** that serves as an implementation guide and test environment.
-   **Fast and seamless integration.**


## Contact Us

If you have any questions or need help, go to [OpenX Support](https://docs.openx.com/Content/support.html).
