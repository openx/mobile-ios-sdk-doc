Integrating the SDK with your app
===============================================

> **Note:** Please make sure you meet all [requirements](ios-sdk-getting-started.md).

To manually integrate the SDK with your Xcode project:

1.  In Xcode, open your project and remove any previously installed
    versions of OpenXSDKCore.
2.  If you have any existing code integrating the SDK, compare the code
    samples and instructions in this documentation for each ad type to
    determine what you must change.
3.  Expand the zip file.
4.  Drag OpenXSDKCore.framework from the expanded zip file into your
    project.
5.  Verify that the **Copy items into destination's group folder
    option** is selected and click **OK**.
6.  Open your project's target settings.
7.  Remove the frameworks from **Linked Frameworks and Libraries**.
    Then, drag the SDK frameworks into **Embedded Binaries**. 
    **Note:** The frameworks should appear only once in the **Linked Frameworks
    and Libraries** and only once in **Embedded Binaries**.
8.  Select the **Build Settings** tab.
9.  In the **Deployment Info** section of the **General** tab, set
    **Deployment Target** for your app to **8.0** or later.
10. Open the Info.plist file of your app as a **Property List**:
    -  Add the **App Transport Security Settings** key and set its **Allow Arbitrary Loads** property to **Yes**. For more information, see [ATS support](#ats-support) below.
    -  For MRAID ads, include all orientations you wish to support.
11. [Initialize](#initializing-the-sdk) the SDK.

ATS support
--------------------

For versions 4.9 and later, the OpenX Mobile iOS SDK makes secure ad requests (HTTPS) by default. owever, many network calls related to the ad are not secure (HTTP), such as those related to resources and events.

To support non-secure requests, set the `NSAllowsArbitraryLoads` key to `YES` in the app\'s Info.plist file. This allows non-secure requests in iOS 9 or later from the app directly as well as web views.

Initializing the SDK
-------------------------------------------------------

Make sure to initialize the OpenX SDK early on in your app, as this ensures the SDK has more time for data enrichment, and will ultimately help with monetization.

Initialize the SDK using [`OXMSDKConfiguration`](ios-sdkparameters.md#oxmsdkconfiguration). You can initialize without video pre-caching, as in the following examples:

**Swift**

``` swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
    OXMSDKConfiguration.initializeSDK()
}
```

**Objective-C**

``` objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [OXMSDKConfiguration initializeSDK];
}
```

Initializing the SDK for video pre-caching
-------------------------------------------------------
In OpenX SDK versions 4.9 and later, you can also enable video pre-caching, which causes an ad video to load on a device before the user views it. This alternative to streaming ensures that the video plays without delays for a better user experience.

To enable pre-caching, integrate [video interstitial ads](ios-sdk-video-interstitial-integration.md), [opt-in video ads](ios-sdk-video-optin-integration.md) or [300x250 Video](ios-sdk-video-300x250.md) into your app. Also, modify initialization for the SDK:

**Swift**

``` swift
// Create a container for initialization with custom options.
let options = OXMSDKInitializationOptions()
        
// Provide a list of ad configurations to preload.
let adConfig = AdConfiguration()
adConfig.oxmAdUnitIdentifierType = .vast
adConfig.domain = "mobile-d.openx.net"
adConfig.auid = "540396661"
        
options.preloadVastConfigurations = [adConfig]
        
// Start SDK Initialization with custom options.
// OpenX SDK will initiate the loading of ads for provided vast tags immediately.
OXMSDKConfiguration.initializeSDK(with:options)
```

**Objective-C**

``` objc
// Create a container for initialization with custom options.
OXMSDKInitializationOptions* options = [OXMSDKInitializationOptions new];
    
// Provide a list of ad configurations to preload.
OXMAdConfiguration *adConfig = [OXMAdConfiguration new];
adConfig.oxmAdUnitIdentifierType = OXMAdUnitIdentifierTypeVast;
adConfig.domain = @"mobile-d.openx.net";
adConfig.auid = @"540396661";
    
options.preloadVastConfigurations = @[adConfig];
    
// Start SDK Initialization with custom options.
// OpenX SDK will initiate the loading of ads for provided vast tags immediately.
[OXMSDKConfiguration initializeSDKWithOptions:options];
```

Now you are ready to continue with specific integration steps for each
ad type, or see the relevant adapter instructions:

-   [Banner ad integration](ios-sdk-banner-integration.md)
-   [Interstitial integration](ios-sdk-interstitial-integration.md)
-   [Video interstitial
    integration](ios-sdk-video-interstitial-integration.md)
-   [Opt-in video integration](ios-sdk-video-optin-integration.md)
-   [MoPub adapter](ios-sdk-mopub-adapter.md)
-   [AdMob adapter](ios-sdk-admob-adapter.md)
