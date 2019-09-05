Upgrading the OpenX Mobile iOS SDK
================================================

Complete these steps if you are upgrading from a version older than
4.8.0.

To upgrade to 4.8.1:

1. Replace the old `OpenXSDKCore.framework` with the new version.
2. Since the `OXMAdView` class is no longer supported:
    -   For interstitial display ad integrations, use the new `OXMInterstitialController` class.
    -   For banner ad integrations, you must use the new `OXMBannerView` class.
3.  Update your classes that conform to the respective `OXMBannerViewDelegate` and `OXMInterstitialControllerDelegate` protocols to have implementations of all their methods. These methods are now all required in order to support Swift types that do not inherit from `NSObject`.
4.  For interstitial ad integrations, remove any usage of `OXMInterstitialDisplayProperties.closeButtonText` as the SDK no longer supports a text Close button. You can use `OXMInterstitialDisplayProperties.closeButtonImage` instead. If you don\'t set this property, a default image will be used.
5.  If you previously added `OXMAdView` in Interface Builder, remove \"OpenXSDKCore\" from the **Module** field in the Identify Inspector:
    
![](res\ios-sdk-id-inspector.png)

To validate your upgrade, see the complete list of differences in the
appropriate section:

-   [Changes required for apps developed in Objective-C](#changes-required-for-apps-developed-in-objective-c)
-   [Changes required for apps developed in Swift](#changes-required-for-apps-developed-in-swift)

You are now ready to use version 4.8.1.

Changes required for apps developed in Objective-C
--------------------------------------------------------------

This section lists all updates that you should be aware of if your app
is built in Objective-C.

### Updated classes
| **Class**              | **Change**        | **Description**                                              |
| ---------------------- | ----------------- | ------------------------------------------------------------ |
| OXMSDKConfiguration    | Modified method   | Modified `defaultDomain`.                                    |
|                        | Modified method   | Modified `defaultAdUnitId`.                                  |
|                        | Removed method    | Removed `returnToInterstitialAfterClickthrough`.             |
|                        | Added method      | Added `creativeFactoryTimeoutPreRenderContent`.<br />`creativeFactoryTimeoutPreRenderContent` sets the duration (in seconds) in which the video or display interstitial creative must completely pre-render before considered a failure. Default: `30` |
| OXMUserParameters      | Removed variables | Removed:<br />city,<br />coordinates,<br />country,<br />state,<br />zipCode,<br />Geo parameters have been removed and are now set on this class' `oxmORTBBidRequest` property. |
| OXMInterstitialDisplay | Modified property | Modified `closeButtonImage`.<br />`closeButtonImage` now sets an OpenX-provided close button as the default for the `closeButtonImage`. The `closeButtonImage`can no longer be set to `nil`. |
|                        | Removed property  | Removed `closeButtonText`.<br />This is no longer supported. |

### Deprecated classes

| **Class** | **Change** | **Description**                                              |
| --------- | ---------- | ------------------------------------------------------------ |
| OXMAdView | deprecated | Use `OXMBannerView` and `OXMInterstitialController` instead. |

### Added classes

| **Class**                 | **Change** | **Description**                                            |
| ------------------------- | ---------- | ---------------------------------------------------------- |
| OXMBannerView             | New class  | Allows loading and showing banners.                        |
| OXMInterstitialController | New class  | Allows loading and showing interstitial and opt-in videos. |

### Deprecated protocols

| **Class**         | **Change** | **Description**                                              |
| ----------------- | ---------- | ------------------------------------------------------------ |
| OXMAdViewDelegate | deprecated | Use `OXMBannerViewDelegate` and `OXMInterstitialControllerDelegate` instead. |


### Added protocols

| **Class**                         | **Change**   | **Description**                                            |
| --------------------------------- | ------------ | ---------------------------------------------------------- |
| OXMBannerViewDelegate             | New protocol | Allows loading and showing banners.                        |
| OXMInterstitialControllerDelegate | New protocol | Allows loading and showing interstitial and opt-in videos. |

Changes required for apps developed in Swift
---------------------------------------------------------

This section lists all updates that you should be aware of if your app
is built in Swift.

### Updated classes

| **Class**              | **Change**        | **Description**                                              |
| ---------------------- | ----------------- | ------------------------------------------------------------ |
| OXMSDKConfiguration    | Modified method   | Modified `defaultDomain`.                                    |
|                        | Modified method   | Modified `defaultAdUnitId`.                                  |
|                        | Removed method    | Removed `returnToInterstitialAfterClickthrough`.             |
|                        | Added method      | Added `creativeFactoryTimeoutPreRenderContent`.<br />`creativeFactoryTimeoutPreRenderContent` sets the duration (in seconds) in which the video or display interstitial creative must completely pre-render before considered a failure. Default: `30` |
| OXMUserParameters      | Removed variables | Removed:<br />city,<br />coordinates,<br />country,<br />state,<br />zipCode,<br />Geo parameters have been removed and are now set on this class' `oxmORTBBidRequest` property. |
| OXMInterstitialDisplay | Modified property | Modified `closeButtonImage`.<br />`closeButtonImage` now sets an OpenX-provided close button as the default for the `closeButtonImage`. The `closeButtonImage`can no longer be set to `nil`. |
|                        | Removed property  | Removed `closeButtonText`.<br />This is no longer supported. |

### Deprecated classes

| **Class** | **Change** | **Description**                                              |
| --------- | ---------- | ------------------------------------------------------------ |
| OXMAdView | deprecated | Use `OXMBannerView` and `OXMInterstitialController` instead. |

### Added classes

| **Class**                 | **Change** | **Description**                                            |
| ------------------------- | ---------- | ---------------------------------------------------------- |
| OXMBannerView             | New class  | Allows loading and showing banners.                        |
| OXMInterstitialController | New class  | Allows loading and showing interstitial and opt-in videos. |

### Deprecated protocols

| **Class**         | **Change** | **Description**                                              |
| ----------------- | ---------- | ------------------------------------------------------------ |
| OXMAdViewDelegate | deprecated | Use `OXMBannerViewDelegate` and `OXMInterstitialControllerDelegate` instead. |

### Added protocols

| **Class**                         | **Change**   | **Description**                                            |
| --------------------------------- | ------------ | ---------------------------------------------------------- |
| OXMBannerViewDelegate             | New protocol | Allows loading and showing banners.                        |
| OXMInterstitialControllerDelegate | New protocol | Allows loading and showing interstitial and opt-in videos. |
