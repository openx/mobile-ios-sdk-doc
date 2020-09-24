OpenX Mobile iOS SDK Release notes
==================================

Version 4.13
-----------

Jun 22, 2020


* Update the Open Measurement SDK to version **1.3.5**. 
* More precise support of **MRAID 3**.
* Minor improvements and fixes.


Version 4.12
-----------

May 4, 2020

**Features**

* Update the Open Measurement SDK to version **1.3**. 
* <img src="res/Beta-banner.png"> **MRAID 3** support. To enable it you need to set the `sendMRAID3SupportParams` property in the [OXMSDKConfiguration] (ios-sdk-parameters.md#OXMSDKConfiguration) to **true**.

**Changes and Improvements**

* Renew the IAB certification for the Open Measurement framework.
* New internal viewability measurement component that works according to the MRC and IAB guidances. 
* Minor improvements and fixes 

Version 4.11
-----------

Jan 14, 2020

**Features**

* Support the deeplink+. The SDK is able to manage the app-targeting campaigns.
* Track [render impressions](ios-sdk-impression-tracking.md). The SDK tracks impressions according to the MRC Guidelines.
* Support CCPA.
* Update the Transparency and Consent Framework (GDPR) to TCF v2.
* Support iOS 13.
* Support Vertical Video ads.
* Support MoPub’s custom AdapterConfiguration.

**Changes and Improvements**

* The configuration settings for ad requests was changed. The access to the sensitive fields was limited to prevent inappropriate bidding.
* The behavior between several active ad views was improved. Now you can place different ad units on the same view.
* ⚠️ The methods in some [protocols](ios-sdk-delegates.md) were renamed to support the managing of different ad views by single controller.
* Improvements and corrections for the logging system.


Version 4.10
-----------

July 30, 2019


**Features**

* SSL connection for all ad requests. In versions 4.10 and later, OpenX SDK performs only secure ad requests.
* 300x250 Video ad format. You can integrate the video ads into UI.

**Changes and Improvements**

* Changed initialization of video ad classes: Provide the domain and ad unit ID values instead of vastURL.
* Improved the UI/UX for Interstitial ads.
* Updates to the OMSDK library and improve support.
* Improvements and fixes for MRAID  
* Corrections for precaching of video ads
* The Ad Mob adapter is introduced


Version 4.9.1
-----------

August 27, 2019

This version of the OpenX Mobile iOS SDK includes a critical bug fix to resolve the bidding issue for display ads.


Version 4.9
-----------

June 6, 2019

**The OpenX Mobile SDK features enhancements that improve bidding insights and user experience:**

* Integration with the [IAB's Open Measurement SDK](https://iabtechlab.com/standards/open-measurement-sdk/) provides viewability tracking to enable marketers to reach users in high-viewability inventory across all their devices.
* An AdChoices icon appears with every mobile ad served through the SDK. This icon indicates that an ad is being displayed. If the user clicks the icon, they are redirected to the [OpenX privacy page](https://www.openx.com/legal/privacy-policy/), which shows the information that is being collected about them and that may be used for targeting them in future ads.
* Video precaching enables ads to load before viewing so that they can run without delay.

**Major design changes and removed features:**

* Non-modal behavior is applied for MRAID resize.
* Completed videos with no end cards automatically close.

**Major bug fixes:**

* For MoPub Adapter, the clickthrough appears after the user taps on the banner ad.
* Invalid lat/lon degree precision sent in ad requests has been corrected.

Version 4.8.1
-------------

October 23, 2018

This version of the OpenX Mobile iOS SDK includes:

-   **Bitcode support**. The OpenX Mobile iOS SDK now supports Bitcode.
-   **Fix for interstitial ads on iPhone X**. Previously, on iPhone X
    running iOS 11 or higher, the status bar could overlap the ad
    creative Close button. This no longer occurs.

Version 4.8.0
---------------------

August 24, 2018

This version of the OpenX Mobile iOS SDK includes:

-   ![](res/Beta-banner.png)**Opt-in** **(rewarded)**
    **video with end card support.** This feature in the SDK is in Beta release only. For details, see [Opt-in video integration](ios-sdk-video-optin-integration.md).
-   **AdMob adapter integration.** For details, see [AdMob adapter](ios-sdk-admob-adapter.md).
-   **API changes.** For details, see [Upgrading OpenX Mobile iOS SDK](ios-sdk-upgrading.md).

Version 4.7.1
-------------

May 24, 2018

This version of the OpenX Mobile iOS SDK includes critical bug fixes to
resolve crashes on iOS versions 8 and 9.

Version 4.7.0
-------------------------

May 11, 2018

This version of the OpenX Mobile iOS SDK includes:

-   **Objective-C implementation.** Previous versions were built with
    Swift. Now, apps built using Objective-C no longer need to include
    the Swift framework.
-   **IAB GDPR Transparency and Consent Framework compliance.** The
    OpenX Mobile iOS SDK now retrieves the user consent values set by an
    IAB-compliant Consent Management Provider (CMP) SDK. See the [IAB website](https://www.iab.com/news/iab-europe-releases-gdpr-transparency-consent-framework-public-comment/)
    for more details about the proposed framework.

For upgrade steps from a previous version to 4.7.0, see [Upgrading the OpenX Mobile iOS SDK](ios-sdk-upgrading.md).

Version 4.6.3
-------------

April 11, 2018

This version of the OpenX Mobile iOS SDK includes:

-   Upgrade to Xcode 9.3.
-   Bug fixes.

Version 4.6.1
-------------

January 5, 2018

This version of the OpenX Mobile iOS SDK includes:

-   Upgrade to Xcode 9.2.

Version 4.6.0
-------------

October 4, 2017

This version of the OpenX Mobile iOS SDK includes:

-   Support for [video interstitial
    ads](ios-sdk-video-interstitial-integration.md).
-   Improved [error messaging](ios-sdk-logging.md).
-   Bug fixes.

Version 4.5.3
-------------

September 20, 2017

This version of the OpenX Mobile iOS SDK includes:

-   Upgrade to Xcode 9.
-   Support for iOS 11.

Version 4.5.2
-------------

September 13, 2017

This version of the OpenX Mobile iOS SDK includes bug fixes.

Version 4.5.1
-------------

August 23, 2017

The OpenX Mobile iOS SDK has been completely re-architected in Swift to
provide a faster, safer user experience. It includes:

-   Support for [flex ads](ios-sdk-flex-ads.md).
-   Ability to mediate OpenX in MoPub using a [MoPub SDK
    adapter](ios-sdk-mopub-adapter.md).
-   A unique `transactionId` for identifying an ad, so that you can
    troubleshoot ad quality issues.
-   Improved MRAID support.

The OpenX Mobile SDK has been tested on:

-   iOS 8, 9, and 10.
-   Xcode 8.3.3.
