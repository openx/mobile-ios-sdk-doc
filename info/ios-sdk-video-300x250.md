300x250 Video integration
==============================

Starting from version **4.10** you can integrate video ads directly into your UI. The supported video ad formats include .mp4, .3gpp, .webm, and .mkv.

Before integrating a video interstitial ad in your app do the following:

1.  Either [create a linear video ad unit](https://docs.openx.com/Content/publishers/inventory-adunits-video-linear.html) or make sure you know which existing ad unit to use.
2.  Complete the integration steps, as described in [Integrating the SDK with your app](ios-sdk-integration.md).

Integration
------------------------

1.  In your view controller, import `OpenXSDKCore`.
2.  Conform your view controller to the [`OXMVideoViewDelegate`](ios-sdk-delegates.md#oxminterstitialcontrollerdelegate-protocol) protocol.
3.  Create a variable to reference `OXMVideoAdView` and instantiate it.
4.  In your view controller, set [parameters](ios-sdk-parameters.md) in the `viewDidLoad` method:  
    - Set the `adUnitId`. 
    - Set the `domain`.
    - Assign `delegate` and set it to `self`.
6. (Recommended) Enrich the request by setting values on the [`userParameters`](ios-sdk-parameters.md#oxmuserparameters) property.    
6.  Call `load()` on `OXMVideoAdView`.
7.  Implement the [OXMVideoAdViewDelegate](ios-sdk-delegates.md#OXMVideoAdViewDelegate-protocol) methods.
8.  Display the video interstitial.

Objective-C code sample
------------------------------------

``` objc
- (void) viewDidLoad {
    [super viewDidLoad]
        
    videoAdVC.videoAdView.delegate = self;
        
    videoAdView.domain = @"mobile-d.openx.net";
    videoAdView.adUnitId = @"540851418";
        
    [self.videoAdView load];
}

#pragma mark - OXMVideoAdViewDelegate

- (void)videoAdViewDidLoad:(OXMVideoAdView *)videoAdView adDetails:(OXMAdDetails *)adDetails {
    // Start playback since video is loaded
    [self.videoAdView play];
}
```

Swift code sample
----------------------------

``` swift
override func viewDidLoad() {
    super.viewDidLoad()
     
    videoAdView.delegate = self
        
    videoAdView.domain = "mobile-d.openx.net"
    videoAdView.adUnitId = "540851418"
    	
    videoAdView.load()
}

// MARK: - OXMVideoAdViewDelegate

    func videoAdViewDidLoad(_ videoAdView: OXMVideoAdView, adDetails: OXMAdDetails) {
    // Start playback since video is loaded
    videoAdView.play()
}
```
