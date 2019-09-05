Request parameters
==================

The tables below list the methods and properties that the OpenX Mobile
iOS SDK supports.

[OXMSDKConfiguration](#oxmsdkconfiguration)

[OXMBannerView](#oxmbannerview)

[OXMInterstitialController](#oxminterstitialcontroller)

[OXMUserParameters Variables](#oxmuserparameters-variables)

[OXMUserParameters Methods](#oxmuserparameters-methods)

[OXMInterstitialDisplay Properties](#oxminterstitialdisplayproperties)

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
| logLevel                               | Controls the verbosity of OpenXSDKCore's internal logger. Options are (from most to least noisy):<br />- .info<br />- .warn<br />- .error<br />- .none | .info       |
| debugLogFileEnabled                    | If `true`, the output of OpenXSDKCore's internal logger is written to a text file. This can be helpful for debugging. See [Logging](ios-sdk-logging.md). | false       |

OXMBannerView
--------------------------

| **Property**               | **Type**                                                     | **Description**                                              | **Required?**                                                |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| adUnitIdentifierType       | AdUnitIdentifierType                                         | Type of ad unit.<br />Options include:<br />- `AdUnitIdentifierTypeAuid`. Use for loading ads via a domain and ad unit combo.<br />- `AdUnitIdentifierTypeVast`. Use for loading a video ad via VAST URL.<br />The default is `AdUnitIdentifierTypeAuid`. | Required                                                     |
| adUnitID                   | NSString                                                     | OpenX ad unit ID.<br />For example: `"123456789"`            | Required only if `adUnitIdentifierType` is `AdUnitIdentifierTypeAuid` |
| domain                     | NSString                                                     | Your app's OpenX delivery domain, provided to you by OpenX.<br />For example: `"PUBLISHER-d.openx.net"` | Required if `adUnitIdentifierType` is `AdUnitIdentifierTypeAuid`. |
| delegate                   | [OXMBannerViewDelegate](ios-sdk-delegates.md#oxmbannerviewdelegate-protocol) | [Delegate](ios-sdk-delegates.md) for the `oxmBannerView`. Typically a `UIViewController`. | Recommended                                                  |
| flexAdSize                 | NSString                                                     | Allows multiple ad sizes for an ad unit (flex ads) which allows for better monetization. See [Flex ads](ios-sdk-flex-ads.md). | Recommended if displaying interstitials                      |
| userParameters             | [OXMUserParameters](ios-sdk-parameters.md#oxmuserparameters-variables) | Data structure containing [properties](ios-sdk-parameters.md#oxmuserparameters-variables) for enriching requests with user data. | Recommended                                                  |
| autoDisplayOnLoad          | BOOL                                                         | Determines whether the ad immediately displays upon loading or if one of the following must be called: `show()` or `showAsInterstitialFromRoot()`.<br />Default is `true`. | Optional                                                     |
| autoRefreshDelay           | NSTimeInterval                                               | Amount of time in seconds between refreshes. This value will be overwritten with any values received from the server. Prevent an auto-refresh by using a value of `0` or less.<br />Default is `60`. | Optional                                                     |
| autoRefreshMax             | NSUInteger                                                   | Maximum number of times the `oxmBannerView`should refresh. This value will be overwritten with any values received from the server. Using a value of 0 indicates there is no maximum.<br />Default is `0`. | Optional                                                     |
| backgroundColor            | UIColor                                                      | Background color of the `OXMBannerView`. This color will be displayed until the ad loads.<br />Default is `[UIColor clearColor]`. | Optional                                                     |
| connectionTimeoutInSeconds | NSTimeInterval                                               | Maximum amount of time the `oxmBannerView` has to complete an ad request.<br />Default is `3`. | Optional                                                     |

OXMInterstitialController
-------------------------------------------------------

| **Property**                  | **Type**                                                     | **Description**                                              | **Required?**                                                |
| ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| adUnitIdentifierType          | AdUnitIdentifierType                                         | Type of ad unit.<br />Options include:<br />- `AdUnitIdentifierTypeAuid`. Use for loading ads via a domain and ad unit combo.<br />- `AdUnitIdentifierTypeVast`. Use for loading a video ad via VAST URL.<br />The default is `AdUnitIdentifierTypeAuid`. | Required                                                     |
| adUnitID                      | NSString                                                     | OpenX ad unit ID.<br />For example: `"123456789"`            | Required |
| domain                        | NSString                                                     | Your app's OpenX delivery domain, provided to you by OpenX.<br />For example: `"PUBLISHER-d.openx.net"` | Required  |
| delegate                      | [OXMInterstitialControllerDelegate](ios-sdk-delegates.md#oxminterstitialcontrollerdelegate-protocol) | [Delegate](ios-sdk-delegates.md#oxminterstitialcontrollerdelegate-protocol) for the `interstitialController`. Typically a `UIViewController`. | Recommended                                                  |
| flexAdSize                    | NSString                                                     | Allows multiple ad sizes for an ad unit (flex ads) which allows for better monetization. See [Flex ads](ios-sdk-flex-ads.md). | Recommended                      |
| interstitialDisplayProperties | [OXMInterstitialDisplayProperties](#oxminterstitialdisplayproperties) | Data structure containing [properties](#oxminterstitialdisplayproperties) for displaying interstitials. | Recommended                       |
| userParameters                | [OXMUserParameters](#oxmuserparameters-variables) | Data structure containing [properties](#oxmuserparameters-variables) for enriching requests with user data. | Recommended                                                  |
| autoDisplayOnLoad             | BOOL                                                         | Determines whether the ad immediately displays upon loading or if one of the following must be called: `show()` or `showAsInterstitialFromRoot()`.<br />Default is `true`. | Optional                                                     |
| autoRefreshDelay              | NSTimeInterval                                               | Amount of time in seconds between refreshes. This value will be overwritten with any values received from the server. Prevent an auto-refresh by using a value of `0` or less.<br />Default is `60`. | Optional                                                     |
| autoRefreshMax                | NSUInteger                                                   | Maximum number of times the `interstitialController` should refresh. This value will be overwritten with any values received from the server. Using a value of `0` indicates there is no maximum.<br />Default is `0`. | Optional                                                     |
| backgroundColor               | UIColor                                                      | Background color of the `OXMInterstitialController`. This color will be displayed until the ad loads.<br />Default is `[UIColor clearColor]`. | Optional                                                     |
| connectionTimeoutInSeconds    | NSTimeInterval                                               | Maximum amount of time the `interstitialController` has to complete an ad request.<br />Default is `3`. | Optional                                                     |
| isRewarded                    | BOOL                                                         | (Beta) Sets a video interstitial ad unit as an opt-in video. | Required for [opt-in interstitial video](ios-sdk-video-optin-integration.md) (rewarded video) ad units |

OXMUserParameters variables
-------------------------------------------------
| **Variable**         | **Type**         | **Description**                                              | **Required?**            |
| -------------------- | ---------------- | ------------------------------------------------------------ | ------------------------ |
| appStoreMarketURL    | NSString         | Store URL for the mobile application.<br />For example: `"https://itunes.apple.com/us/app/your-app/id123456789"` | Recommended              |
| networkType          | OXMNetworkType   | Network connection type of the user (offline, wifi, or cell).<br />For example: `OXMNetworkTypeWifi` | Recommended if available |
| userAge              | UInt16           | Age of the user in years.<br />For example: `35`             | Recommended if available |
| userAnnualIncomeInUS | UInt32           | Annual income of the user in US dollars.<br />For example: `55000` | Recommended if available |
| userEthnicity        | OXMEthnicity     | Ethnicity of the user (African American, Asian, Hispanic, White, Other).<br />For example: `OXMEthnicityAsian` | Recommended if available |
| userGender           | OXMGender        | The gender of the user (Male, Female, Other, Unknown).<br />For example: `OXMGenderFemale` | Recommended if available |
| userID               | NSString         | ID of the user within the app.<br />For example: `"24601"`   | Recommended if available |
| userMaritalStatus    | OXMMaritalStatus | The marital status of the user (Single, Married, Divorced, Unknown).<br />For example: `OXMMaritalStatusDivorced` | Recommended if available |
| carrier              | NSString         | Mobile carrier - Defined by the Mobile Country Code (MCC) and Mobile Network Code (MNC), using the format: <MCC>-<MNC>.<br />For example: `"310-410"` | Optional                 |
| DMA                  | NSString         | For US locations, indicates the user's Designated Market Area.<br />For example: `"803"` | Optional                 |
| IP                   | NSString         | The IP address of the carrier gateway. If this is not present, OpenX retrieves it from the request header.<br />For example: `"192.168.0.1"` | Optional                 |


OXMUserParameters methods
------------------------------------------------------
| **Method**                              | **Description**                                              |
| --------------------------------------- | ------------------------------------------------------------ |
| addCustomParam:@"val1" withName:@"key1" | Add custom parameters. The name will be auto-prepended with `c.` to avoid collisions.<br />Example: `addCustomParam:@"73" withName:@"temperature"` |
| addParam:@"val1" withName:@"key1"       | Add a new OpenX `param` by name and set its needed value.<br />If an ad call parameter doesn't exist in this SDK, you can set it manually using this method.<br />Example: `addParam:@"73" withName:@"temperature"` |
| setCustomParams:@["key1":@"val1"]       | Add a dictionary of name-value parameter pairs, where each parameter name will be prepended with `c.` to avoid name collisions.<br />Example: `setCustomParams:@["key1":@"val1"]` |

OXMInterstitialDisplayProperties
---------------------------------------------------------------------
| **Property**        | **Type**                    | **Description**                                              |
| ------------------- | --------------------------- | ------------------------------------------------------------ |
| closeButtonImage    | UIImage                     | Image to use for the close button.<br />Default is an OpenX-provided close button image if no image is set. |
| closeDelay          | NSTimeInterval              | The number of seconds at which you want to display the close button. The default is five (5) seconds. For details, see [Video interstitial integration](ios-sdk-video-interstitial-integration.md) or [(Beta) Opt-in video integration](android-sdk-video-optin-integration.md). |
| contentFrame        | CGRect                      | Size of the content frame.                                   |
| contentViewColor    | UIColor                     | Background color of the interstitial.<br />Default is `[UIColor clearColor]`. |

