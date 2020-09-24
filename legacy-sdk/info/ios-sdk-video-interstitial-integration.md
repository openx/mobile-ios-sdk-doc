Video Interstitial integration
==============================

You can integrate video interstitial ads in the OpenX Mobile iOS SDK.
The supported video ad formats include .mp4, .3gpp, .webm, and .mkv. 

Before integrating a video interstitial ad in your app, please do the
following:

1.  Either [create a linear video ad unit](https://docs.openx.com/Content/publishers/inventory-adunits-video-linear.html) or make sure you know which existing ad unit to use.
2.  Complete the integration steps, as described in [Integrating the SDK with your app](ios-sdk-integration.md).

> **Note:** OpenX SDK preloads video content by default. It means that all file will be loaded before playback.

Integration
------------------------
Some integration steps vary as indicated, depending on which OpenX Mobile SDK version you are using.

1.  In your view controller, import `OpenXSDKCore`.
2.  Conform your view controller to the `OXMInterstitialControllerDelegate` protocol.
3.  Create a variable to reference `OXMInterstitialController` and instantiate it.
4.  In your view controller, set [parameters](ios-sdk-parameters.md) in the `viewDidLoad` method:
    - Set `adUnitIdentifierType` to `AdUnitIdentifierTypeVast`.
    - Set the `adUnitId`. 
    - Set the `domain`.
    - Assign `delegate` and set it to `self`.
    - Set `autoDisplayOnLoad` to `false`.
5. (Recommended) Enrich the request by setting values on the [`OXBTargeting`](ios-sdk-parameters.md) shared instance.
6.  If needed, set the desired `closeDelay` on [`OXMInterstitialDisplayProperties`](ios-sdk-parameters.html#oxminterstitialdisplayproperties).
    -   Videos that span 2 seconds or less cannot be closed early.
    -   Videos longer than 2 seconds will display a Close button at 2
        seconds by default (recommended).
7.  Call `load()` on `OXMInterstitialController`.
8.  Implement the `OXMInterstitialControllerDelegate` methods.
9.  Display the video interstitial.


If you prefer customizing video duration, set the limits as
    described below. All values are in seconds.

> **Note:** The upper limit is the end of video or 30 seconds, whichever is less.


|Video ad duration  |Custom value                |Result        |
|------------------ |--------------------------- |--------------|
|<= 2               |Ignored                     |End of video  |
|> 2                |Nil, value < 2              |2             |
|> 2                |2 <= value <= upper limit   |Value         |
|> 2                |Value > upper limit         |Upper limit   |

Swift code sample
----------------------------

``` swift
override func viewDidLoad() {
    super.viewDidLoad()
     
    self.interstitialController = OXMInterstitialController();
    self.interstitialController.adUnitIdentifierType = .vast
    self.interstitialController.domain = "mobile-d.openx.net"
    self.interstitialController.adUnitId = "540851203"
    self.interstitialController.delegate = self
    self.interstitialController.autoDisplayOnLoad = false
    	
    self.interstitialController.load()
}
                
// MARK: - OXMInterstitialControllerDelegate

func viewControllerForModalPresentation() -> UIViewController {
    return self
}

func interstitialDidLoad(_ interstitialController: OXMInterstitialController) {
    // Show the interstitial.
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
        
    [self.interstitialController load];
}

#pragma mark - OXMInterstitialControllerDelegate

- (UIViewController *)viewControllerForModalPresentation {
    return self;
}

- (void) interstitialDidLoad:(OXMInterstitialController *)interstitialController {
    // Show the interstitial.
    [self.interstitialController show];
}
```


