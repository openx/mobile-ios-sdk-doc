Banner integration
==================


Before integrating a banner ad in your app, please do the following:

1.  Either  [create a mobile ad unit](https://docs.openx.com/Content/publishers/inventory_createmobilead.html)
    or make sure you know which existing ad unit to use.
2.  Complete the integration steps, as described in [Integrating the SDK with your app](ios-sdk-integration.md).

Integration
------------------------

1.  In your view controller, import `OpenXSDKCore`.
2.  Conform your view controller to the `OXMBannerViewDelegate`
    protocol.
3.  Create a variable to reference `OXMBannerView` and instantiate it.
4.  In your view controller, set [parameters](ios-sdk-parameters.md)
    in the `viewDidLoad` method:
    - Set the `adUnitID`.
    - Set the `domain`.
    - Assign the `delegate` and set it to `self`.
    - (Recommended) Enrich the request by setting values on the [`OXBTargeting`](ios-sdk-parameters.md) shared instance.
5.  Call `load()` on the `OXMBannerView`.
6.  Implement the [`OXMBannerViewDelegate`](ios-sdk-delegates.md) methods.
7.  If you want to use flex ads to allow multiple ad sizes for an ad
    unit, see [Flex ads](ios-sdk-flex-ads.md).
    
> **Note:** In addition you can use [Interface Builder](ios-sdk-using-interface-builder.md) to assist with your OXMBannerView integration.

Swift code sample
---------------------------

**MyViewController.swift**

``` swift
import OpenXSDKCore
class MyViewController : UIViewController, OXMBannerViewDelegate {
	 
    var oxmBannerView = OXMBannerView()
     
    override func viewDidLoad() {
        super.viewDidLoad()
     
        self.oxmBannerView.adUnitId = "540848492"
        self.oxmBannerView.domain = "mobile-d.openx.net"
        self.oxmBannerView.delegate = self
        self.oxmBannerView.flexAdSize = OXMFlexAdSize.Banner_320x50
        self.view.addSubview(oxmBannerView);
        self.oxmBannerView.load()
    }
     
    // MARK: OXMBannerViewDelegate
    // Called every time an ad has loaded and is ready for display. If you
    // experience an ad quality issue, you can identify the ad by the
    // transactionId in the adDetails object.
    func bannerDidLoad(oxmBannerView:OXMBannerView, adDetails:OXMAdDetails) {
        NSLog("OpenX ad loaded: \(oxmBannerView) Transaction ID = \(adDetails.transactionId)")
    }
     
    // Called whenever the load process fails to produce a viable ad.
    func bannerDidFailToLoad(oxmBannerView:OXMBannerView, error:Error) {
        NSLog("adDidFailToLoad: \(oxmBannerView), error: \(error)")
    }
     
    // Called after an ad has rendered to the device's screen.
    func bannerDidDisplay(oxmBannerView:OXMBannerView) {
        NSLog("adDidDisplay: \(oxmBannerView)")
    }
     
    // Called once an ad has finished displaying all of its creatives.
    func bannerDidComplete(oxmBannerView:OXMBannerView) {
        NSLog("adDidComplete: \(oxmBannerView)")
    }
     
    // Called when the user clicks on an ad and a click-through is
    // about to occur.
    func bannerWasClicked(oxmBannerView:OXMBannerView) {
        NSLog("adWasClicked: \(oxmBannerView)")
    }
     
    // Called when the user closes a click-through.
    func bannerClickthroughDidClose(oxmBannerView:OXMBannerView) {
        NSLog("adClickthroughDidClose: \(oxmBannerView)")
    }
     
    // Called when an MRAID ad expands.
    func bannerDidExpand(oxmBannerView:OXMBannerView) {
        NSLog("adDidExpand: \(oxmBannerView)")
    }
     
    // Called when an MRAID ad collapses.
    func bannerDidCollapse(oxmBannerView:OXMBannerView) {
        NSLog("adDidCollapse: \(oxmBannerView)")
    }
                                    
    // Called when the ad leaves the app.
    func bannerDidLeaveApplication(oxmBannerView:OXMBannerView) {
        NSLog("adDidLeaveApplication: \(oxmBannerView)")
    }
}
```

Objective-C code sample
------------------------------------

**ViewController.h**

``` objc
// Contents of file: ViewController.h
#import <UIKit/UIKit.hh>
#import <OpenXSDKCore/OpenXSDKCore.hh>

@interface ViewController : UIViewController, OXMBannerViewDelegate
 
@property IBOutlet OXMBannerView* oxmBannerView;
@end
```

**ViewController.m**

``` objc
  // Contents of file: ViewController.m
#import "ViewController.h"

@interface ViewController ()
@end

@implementation ViewController
- (void)viewDidLoad {
    [super viewDidLoad];
 
    self.oxmBannerView = [[OXMBannerView alloc] init];
    self.oxmBannerView.adUnitId = @"540848492";
    self.oxmBannerView.domain = @"mobile-d.openx.net";
    self.oxmBannerView.delegate = self;
    [self.oxmBannerView load];
}
 
#pragma mark OXMBannerViewDelegate
// Called every time an ad has loaded and is ready for display. If you
// experience an ad quality issue, you can identify the ad by the transactionId
// in the adDetails object.
- (void)bannerDidLoad:(nonnull OXMBannerView *)oxmBannerView adDetails:(nonnull OXMAdDetails *)adDetails {
    NSLog(@"Openx ad loaded: %@ with transaction id: %@", oxmBannerView, adDetails.transactionId);
}
 
// Called whenever the load process fails to produce a viable ad.
- (void)bannerDidFailToLoad:(nonnull OXMBannerView *)oxmBannerView error:(nonnull NSError *)error {
    NSLog(@"adDidFailToLoad: %@, error: %@", oxmBannerView, error);
}
                                
// Called after an ad has rendered to the device's screen.
- (void)bannerDidDisplay:(nonnull OXMBannerView *)oxmBannerView {
    NSLog(@"adDidDisplay: %@", oxmBannerView);
}
 
// Called once an ad has finished displaying all of its creatives.
- (void)bannerDidComplete:(nonnull OXMBannerView *)oxmBannerView {
    NSLog(@"adDidComplete: %@", oxmBannerView);
}
 
// Called when the user clicks on an ad and a click-through is about to occur.
- (void)bannerWasClicked:(nonnull OXMBannerView *)oxmBannerView {
    NSLog(@"adWasClicked: %@", oxmBannerView);
}
 
// Called when the user closes a click-through.
- (void)bannerClickthroughDidClose:(nonnull OXMBannerView *)oxmBannerView {
    NSLog(@"adClickthroughDidClose: %@", oxmBannerView);
}
 
// Called when an MRAID ad expands.
- (void)adDidExpand:(OXMBannerView * _Nonnull)oxmBannerView {
NSLog(@"bannerDidExpand: %@", oxmBannerView);
}
 
// Called when an MRAID ad collapses.
- (void)bannerDidCollapse:(OXMBannerView * _Nonnull)oxmBannerView {
    NSLog(@"adDidCollapse: %@", oxmBannerView);
}
@end
```
