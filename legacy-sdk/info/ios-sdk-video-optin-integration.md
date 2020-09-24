Opt-in video integration
========================

You can integrate opt-in video ads in the OpenX Mobile iOS SDK. The supported video ad formats include .mp4, .3gpp, .webm, and .mkv.

Before integrating an opt-in video (rewarded video) ad in your app, please do the following:

1.  Either [create  a linear video ad unit](https://docs.openx.com/Content/publishers/inventory-adunits-video-linear.html) with the **Is Rewarded** check box selected or make sure you know which existing ad unit to use.
2.  Complete the integration steps, as described in [Integrating the SDK with your app](ios-sdk-integration.md).

> **Note:** OpenX SDK preloads video content by default. It means that all file will be loaded before playback.

Integration
------------------------

1.  In your view controller, import `OpenXSDKCore`.
2.  Conform your view controller to the `OXMInterstitialControllerDelegate` protocol.
3.  Create a variable to reference `OXMInterstitialController` and instantiate it.
4.  In your view controller, set [parameters](ios-sdk-parameters.md) in the `viewDidLoad` method:
    -  Set `adUnitIdentifierType` to `AdUnitIdentifierTypeVast`.
    -  Set `vastURL` using the URL from your video ad unit. Please note
        that a VAST tag always looks like this:
        `"DOMAIN/v/1.0/av?auid=AUID"` (where
        `DOMAIN`{style="font-style: italic;"} is your OpenX delivery
        domain, and `AUID`{style="font-style: italic;"} is the OpenX ad
        unit ID).
    -  Assign `delegate` and set it to `self`.
    -  Set `autoDisplayOnLoad` to `false`.
    -  (Recommended) Enrich the request by setting values on the [`OXBTargeting`](ios-sdk-parameters.md) shared instance.
5.  To set the ad unit as an opt-in video, set the `isRewarded` flag to
    `YES`.
6.  Call `load()` on `OXMInterstitialController`.
7.  Implement the [OXMInterstitialControllerDelegate](ios-sdk-delegates.md#oxminterstitialcontrollerdelegate-protocol) methods.
8.  Display the opt-in video.

Swift code sample
---------------------------

``` swift
override func viewDidLoad() {
    	tialController.load()
}
                
//MARK: OXMInterstitialControllerDelegate

func adDidLoad(_ interstitialController: OXMInterstitialController) {
    // Show the ad.
    self.interstitialController.show()          
}
```

Objective-C code sample
------------------------------------

``` objc
- (void) viewDidLoad {
    self.showButton.enabled = NO;
        
    self.interstitialController = [[OXMInterstitialController alloc] init];
    self.interstitialController.adUnitIdentifierType = AdUnitIdentifierTypeVast;
    self.interstitialController.domain = @"mobile-d.openx.net"
    self.interstitialController.adUnitId = @"540851203"
    self.interstitialController.delegate = self;
    self.interstitialController.autoDisplayOnLoad = NO;
    	
    self.interstitialController.isRewarded = YES;
    	
        
    [self.interstitialController load];
}

#pragma mark - OXMInterstitialControllerDelegate
- (void) adDidLoad:(OXMInterstitialController *)interstitialController {
    // Show the ad.
    [self.interstitialController show];
}
```


