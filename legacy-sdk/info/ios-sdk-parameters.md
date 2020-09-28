Request parameters
==================

The tables below list the methods and properties that the OpenX Mobile iOS SDK allows to customize. The more actual info about the user, the app, and the device you provide the more chances to win an impression. Please strictly follow the recommendations in the below tables and provide all ❗ **Required** and **Highly Recommended** values.


1. [OXBTargeting Variables](#oxbtargeting-variables)
1. [OXBTargeting Methods](#oxbtargeting-methods)
1. [OXMSDKConfiguration](#oxmsdkconfiguration)
1. [OXMBannerView](#oxmbannerview)
1. [OXMInterstitialController](#oxminterstitialcontroller)
1. [OXMInterstitialDisplay Properties](#oxminterstitialdisplayproperties)

OXBTargeting variables
-------------------------------------------------
| **Variable**         | **Type**         | **Description**                                              | **Required?**            |
| -------------------- | ---------------- | ------------------------------------------------------------ | ------------------------ |
| appStoreMarketURL    | NSString         | Store URL for the mobile application. For example: `"https://itunes.apple.com/us/app/your-app/id123456789"` | ❗ Required              |
| networkType          | OXMNetworkType   | Network connection type of the user (offline, wifi, or cell).For example: `OXMNetworkTypeWifi` | ❗ Required |
| IP                   | NSString         | The IP address of the carrier gateway. If this is not present, OpenX retrieves it from the request header. For example: `"192.168.0.1"` | ❗ Highly Recommended                 |
| userAge              | UInt16           | Age of the user in years. For example: `35`             | ❗ Highly Recommended |
| userAnnualIncomeInUS | UInt32           | Annual income of the user in US dollars. For example: `55000` | ❗ Highly Recommended |
| userGender           | OXMGender        | The gender of the user (Male, Female, Other, Unknown). For example: `OXMGenderFemale` | ❗ Highly Recommended  |
| userID               | NSString         | ID of the user within the app. For example: `"24601"`   | ❗ Highly Recommended  |
| userMaritalStatus    | OXMMaritalStatus | The marital status of the user (Single, Married, Divorced, Unknown). For example: `OXMMaritalStatusDivorced` | Recommended if available |
| carrier              | NSString         | Mobile carrier - Defined by the Mobile Country Code (MCC) and Mobile Network Code (MNC), using the format: <MCC>-<MNC>. For example: `"310-410"` | Optional                 |
| DMA                  | NSString         | For US locations, indicates the user's Designated Market Area. For example: `"803"` | Optional                 |
| keywords             | NSString         | Comma separated list of keywords, interests, or intent | Optional |

The code sample:

``` swift
let targeting = OXBTargeting.shared()
targeting.userGender = .male
targeting.userAge = 99
targeting.userAnnualIncomeInUS = 9999
targeting.setLatitude(123.0, longitude: 456.0)
``` 


OXBTargeting methods
------------------------------------------------------
| **Method**                              | **Description**                                              |
| --------------------------------------- | ------------------------------------------------------------ |
| addCustomParam:@"val1" withName:@"key1" | Adds the custom parameters. The name will be auto-prepended with `c.` to avoid collisions. Example: `addCustomParam:@"73" withName:@"temperature"` |
| setCustomParams:@["key1":@"val1"]       | Adds a dictionary of name-value parameter pairs, where each parameter name will be prepended with `c.` to avoid name collisions. Example: `setCustomParams:@["key1":@"val1"]` |
| addParam:@"val1" withName:@"key1"       | Adds a new OpenX `param` by name and set its needed value. If an ad call parameter doesn't exist in this SDK, you can set it manually using this method.<br />Example: `addParam:@"73" withName:@"temperature"` |
| setLatitude:latitude longitude:longitude | Sets the latitude and longitude of a geographic location.<br> Latitude from -90.0 to +90.0, where negative is south. <br> Longitude from -180.0 to +180.0, where negative is west. |

OXMSDKConfiguration
-------------------------------------------

| **Method**                             | **Description**                                              | **Default** |
| -------------------------------------- | ------------------------------------------------------------ | ----------- |
| defaultDomain                          | This value is used for `domain` whenever you do not otherwise set it in `OXMInterstitialController` or `OXMBannerView`. Useful if the same domain is in use throughout your app. | nil         |
| defaultAdUnitId                        | This value is used for `adUnitID` whenever you do not otherwise set it in `OXMInterstitialController` or `OXMBannerView`. Useful if the same ad unit is in use throughout your app. | nil         |
| defaultAutoRefreshDelay                | Controls the initial value of `autoRefreshDelay` for all newly created `OXMInterstitialController` or `OXMBannerView` in seconds. | 60          |
| creativeFactoryTimeout                 | Controls how long in seconds each creative has to load before it is considered a failure. | 3           |
| creativeFactoryTimeoutPreRenderContent | Controls how long (in seconds) the video and display interstitial creative has to completely pre-render before it is considered a failure. | 30          |
| useInternalClickthroughBrowser         | Controls whether to use in-app browser from OpenX or the Safari app for displaying ad click-through content. | true        |
| sendMRAIDSupportParams                 | If `true`, the SDK sends "`af=3,5`", indicating support for MRAID. | true        |
| <img src="res/Beta-banner.png"> sendMRAID3SupportParams                | If `true`, the SDK sends "`af=3,5,6`", indicating support for MRAID 3. **Note:** this flag will make effect only if sendMRAIDSupportParams is **true**. | false        |
| logLevel                               | Controls the verbosity of OpenXSDKCore's internal logger. Options are (from most to least noisy):<br />- .info<br />- .warn<br />- .error<br />- .none | .info       |
| debugLogFileEnabled                    | If `true`, the output of OpenXSDKCore's internal logger is written to a text file. This can be helpful for debugging. See [Logging](ios-sdk-logging.md). | false       |

The code sample:

``` swift
OXMSDKConfiguration.singleton.defaultDomain = "mobile-d.openx.net"
OXMSDKConfiguration.singleton.creativeFactoryTimeout = 5.0
```


OXMBannerView
--------------------------

| **Property**               | **Type**                                                     | **Description**                                              | **Required?**                                                |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| adUnitID                   | NSString                                                     | OpenX ad unit ID. For example: `"123456789"`            | Required |
| domain                     | NSString                                                     | Your app's OpenX delivery domain, provided to you by OpenX. For example: `"PUBLISHER-d.openx.net"` | Required |
| delegate                   | [OXMBannerViewDelegate](ios-sdk-delegates.md#oxmbannerviewdelegate-protocol) | [Delegate](ios-sdk-delegates.md) for the `oxmBannerView`. Typically a `UIViewController`. | Required                                                  |
| flexAdSize                 | NSString                                                     | Allows multiple ad sizes for an ad unit (flex ads) which allows for better monetization. See [Flex ads](ios-sdk-flex-ads.md). | Recommended                     |
| autoRefreshDelay           | NSTimeInterval                                               | Amount of time in seconds between refreshes. This value will be overwritten with any values received from the server. Prevent an auto-refresh by using a value of `0` or less. | Optional   <br />Default is `60`                                                  |
| autoRefreshMax             | NSUInteger                                                   | Maximum number of times the `oxmBannerView`should refresh. This value will be overwritten with any values received from the server. Using a value of 0 indicates there is no maximum. | Optional                                                      <br />Default is `0`|
| connectionTimeoutInSeconds | NSTimeInterval                                               | Maximum amount of time the `oxmBannerView` has to complete an ad request. | Optional <br />Default is `3`.   |

The code sample:

``` swift
bannerView.delegate = bannerVC
bannerView.domain = "mobile-d.openx.net"
bannerView.adUnitId = self.getExampleId(for: .banner)
bannerView.flexAdSize = OXMFlexAdSize.banner_320x50
bannerView.autoRefreshDelay = 30.0

bannerView.load()
```                                                 

OXMInterstitialController
-------------------------------------------------------

| **Property**                  | **Type**                                                     | **Description**                                              | **Required?**                                                |
| ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| adUnitIdentifierType          | AdUnitIdentifierType                                         | Type of ad unit.<br />Options include:<br />- `AdUnitIdentifierTypeAuid`. Use for loading display ads.<br />- `AdUnitIdentifierTypeVast`. Use for loading a video ads.<br />The default is `AdUnitIdentifierTypeAuid`. | Required                                                     |
| adUnitID                      | NSString                                                     | OpenX ad unit ID. For example: `"123456789"`            | Required |
| domain                        | NSString                                                     | Your app's OpenX delivery domain, provided to you by OpenX. For example: `"PUBLISHER-d.openx.net"` | Required  |
| delegate                      | [OXMInterstitialControllerDelegate](ios-sdk-delegates.md#oxminterstitialcontrollerdelegate-protocol) | [Delegate](ios-sdk-delegates.md#oxminterstitialcontrollerdelegate-protocol) for the `interstitialController`. Typically a `UIViewController`. | Required                                                  |
| interstitialDisplayProperties | [OXMInterstitialDisplayProperties](#oxminterstitialdisplayproperties) | Data structure containing [properties](#oxminterstitialdisplayproperties) for displaying interstitials. | Required                       |
| flexAdSize                    | NSString                                                     | Allows multiple ad sizes for an ad unit (flex ads) which allows for better monetization. See [Flex ads](ios-sdk-flex-ads.md). | Recommended                      |
| connectionTimeoutInSeconds    | NSTimeInterval                                               | Maximum amount of time the `interstitialController` has to complete an ad request.<br />Default is `3`. | Optional                                                     |
| isRewarded                    | BOOL                                                         | Sets a video interstitial ad unit as an opt-in video. | Required for [opt-in interstitial video](ios-sdk-video-optin-integration.md) (rewarded video) ad units |

The code sample: 

``` swift
interstitialController.delegate = interstitialVC
interstitialController.adUnitId = self.getExampleId(for: .htmlInterstitial)
interstitialController.domain = "mobile-d.openx.net"
interstitialController.flexAdSize = "320x480"

interstitialController.load()
```


OXMInterstitialDisplayProperties
---------------------------------------------------------------------
| **Property**        | **Type**                    | **Description**                                              |
| ------------------- | --------------------------- | ------------------------------------------------------------ |
| closeButtonImage    | UIImage                     | Image to use for the close button.<br />Default is an OpenX-provided close button image if no image is set. |
| closeDelay          | NSTimeInterval              | The number of seconds at which you want to display the close button. The default is five (5) seconds. For details, see [Video interstitial integration](ios-sdk-video-interstitial-integration.md) or [(Beta) Opt-in video integration](android-sdk-video-optin-integration.md). |
| contentFrame        | CGRect                      | Size of the content frame.                                   |
| contentViewColor    | UIColor                     | Background color of the interstitial.<br />Default is `[UIColor clearColor]`. |

The code sample: 

``` swift
interstitialController.adUnitId = self.getExampleId(for: .htmlInterstitial)
interstitialController.domain = "mobile-d.openx.net"

interstitialController.interstitialDisplayProperties.closeDelay = 3.0
    
interstitialController.load()
```


