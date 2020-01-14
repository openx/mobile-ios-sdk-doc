Getting started
===============

To get started with the OpenX Mobile iOS SDK, make sure you meet the
following requirements:

-   iOS version 8 or newer for your deployment target. Users on these versions will get ads. Beta versions are not supported.
-   Xcode versions 9 or later. Beta versions are not supported.
-   For display ads, the ad unit ID and OpenX delivery domain provided by OpenX.
-   For video ads, including opt-in and 300x250 video, the ad unit ID and OpenX delivery domain provided by OpenX. 

For new features and upgrades, please see [Release notes](ios-sdk-release-notes.md) and [Upgrading the OpenX Mobile iOS SDK](ios-sdk-upgrading.md).


Ad Formats and Tips
-------------------------

**Ad Formats and  Integration:**

- [Integrating the SDK with your app](ios-sdk-integration.md)
- [Banner ad integration](ios-sdk-banner-integration.md)
- [Interstitial ad integration](ios-sdk-interstitial-integration.md)
- [Video interstitial integration](ios-sdk-video-interstitial-integration.md)
- [Opt-in video integration](ios-sdk-video-optin-integration.md)
- [Video 300x250 integration](ios-sdk-video-300x250.md) (New in 4.10)

**Behavior and Parameterization**

- [Delegates](ios-sdk-delegates.md)
- [Parameters](ios-sdk-parameters.md)

**Ad Network Adapters:**

- [MoPub Adapter](ios-sdk-mopub-adapter.md)
- [AdMob Adapter](ios-sdk-admob-adapter.md)

**Integration Fetures and Tips:**

- [Launching the demo app](ios-sdk-demo-app.md)
- [iOS App Transport Security (ATS)](ios-sdk-ats.md)
- [Testing and troubleshooting](ios-sdk-self-test.md)
- [Ad Quality](ios-sdk-ad-quality.md)
- [Submitting your app to App Store](ios-sdk-final-steps.md)


Integration process overview
----------------------------

To integrate the OpenX Mobile iOS SDK, complete the following steps. To
explore the provided sample implementations
[download](http://sdk.prod.gcp.openx.org/ios/4.11.0/OpenX_Mobile_SDK_iOS_4.11.0.zip)
the SDK and [launch the demo app](ios-sdk-demo-app.md).

> **Tip:** You may use these steps as a high-level checklist to ensure a successful
integration.

1.  Make sure you meet the above [requirements](#getting-started).
2.  [Download](http://sdk.prod.gcp.openx.org/ios/4.11.0/OpenX_Mobile_SDK_iOS_4.11.0.zip)
    the [OpenX Mobile iOS SDK zip file](#sdk-zip-file-contents).
3.  [Integrate the SDK with your app](ios-sdk-integration.md) and
    [initialize the SDK](ios-sdk-integration.md#initializing-the-sdk-for-video-pre-caching).
4.  If you want to use OpenX as a source of demand on MoPub and/or AdMob
    via their respective SDKs, build [MoPub](ios-sdk-mopub-adapter.md)
    and/or [AdMob](ios-sdk-admob-adapter.md) SDK adapter and skip to
    step 6.

5.  Integrate the desired ad unit into your app by following the
    appropriate instructions below:
    -   [Banner ad integration](ios-sdk-banner-integration.md)
    -   [Interstitial ad
        integration](ios-sdk-interstitial-integration.md)
    -   [Video interstitial
        integration](ios-sdk-video-interstitial-integration.md)
    -   [Opt-in video integration](ios-sdk-video-optin-integration.md)
    -   [Video 300x250 integration](ios-sdk-video-300x250.md) (New in 4.10)
6.  [Test](ios-sdk-self-test.md) your integration.
7.  Complete the [final steps](ios-sdk-final-steps.md) and notify
    OpenX to enable live traffic before submitting your app to the App
    Store.

If you need any assistance during the integration process, please visit
the [OpenX Support Community](https://community.openx.com/s/).

SDK zip file contents
-----------------------------

The OpenX Mobile iOS SDK zip file contains the following:

| Item                      | **Description**                                              |
| ------------------------- | ------------------------------------------------------------ |
| OpenXSDKCore.framework    | The SDK framework in Objective-C.                            |
| OpenXDemoApp              | The folder housing the following [test apps](ios-sdk-demo-app.md):<br />- **OpenXDemoAppSwift.** A Swift test app which includes many helpful examples of how to integrate the SDK.<br />- **OpenXDemoAppObjC.** An Objective-C test app which includes many helpful examples of how to integrate the SDK. |
