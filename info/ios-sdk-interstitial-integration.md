Interstitial integration
========================


Before integrating an interstitial ad in your app, please do the
following:

1.  Either [create a mobile ad unit](https://www.openx.com/publishers/inventory_createmobilead.html) or make sure
    you know which existing ad unit to use.
2.  Complete the integration steps, as described in [Integrating the SDK with your app](ios-sdk-integration.md).

Integration
------------------------

1.  In your view controller, import `OpenXSDKCore`.
2.  Conform your view controller to the `OXMInterstitialControllerDelegate` protocol.
3.  Create a variable to reference `OXMInterstitialController` and instantiate it.
4.  In your view controller, set [parameters](ios-sdk-parameters.md#oxminterstitialcontroller) in the `viewDidLoad` method:
    -  Set the `adUnitID`.
    -  Set the `domain`.
    -  Assign the `delegate` and set it to `self`.
    -  (Recommended) Enrich the request by setting values on the [`userParameters`](ios-sdk-parameters.md) property.
    -  Set `autoDisplayOnLoad` to `false`.
5.  Call `load()` on the `OXMInterstitialController`.
6.  Implement the [OXMInterstitialControllerDelegate](ios-sdk-delegates.md#oxminterstitialcontrollerdelegate-protocol) methods.
7.  If you want to use flex ads to allow multiple ad sizes for an ad unit, use the `flexAdSize` parameter. For details, see [Flex ads](ios-sdk-flex-ads.md).
8.  Display the interstitial.

Swift code sample
---------------------------

``` swift
import OpenXSDKCore
 
class MyViewController : UIViewController, OXMInterstitialControllerDelegate{
 
    @IBOutlet weak var interstitialController:OXMInterstitialController!
    @IBOutlet weak var showButton:UIButton!
 
    override func viewDidLoad() {
        super.viewDidLoad()
        self.showButton.isEnabled = false
 
        self.interstitialController.adUnitId = "123456789"
        self.interstitialController.domain = "pub-d.openx.net"
        self.interstitialController.delegate = self
        self.interstitialController.flexAdSize = OXMFlexAdSize.Interstitial_1024x768_480x320_300x250
        self.interstitialController.userParameters.userGender = OXMGender.male
        self.interstitialController.userParameters.userAge = 21
        self.interstitialController.autoDisplayOnLoad = false
        self.interstitialController.load()
    }
 
    // MARK: OXMInterstitialControllerDelegate
    // Called every time an ad has loaded and is ready for display. If you
    // experience an ad quality issue, you can identify the ad by the
    // transactionId in the adDetails object.
    func adDidLoad(interstitialController:OXMInterstitialController, adDetails:OXMAdDetails) {
        NSLog("OpenX ad loaded: \(interstitialController) Transaction ID = \(adDetails.transactionId)")
                
        // When appropriate, show the interstitial.
        self.interstitialController.showAsInterstitialFromRoot(self)   
    }
 
    // Called whenever the load process fails to produce a viable ad.
    func adDidFailToLoad(interstitialController:OXMInterstitialController, error:Error) {
        NSLog("adDidFailToLoad: \(interstitialController), error: \(error)")
    }
 
    // Called after an ad has rendered to the device's screen.
    func adDidDisplay(interstitialController:OXMInterstitialController) {
        NSLog("adDidDisplay: \(interstitialController)")
    }
 
    // Called once an ad has finished displaying all of its creatives.
    func adDidComplete(interstitialController:OXMInterstitialController) {
        NSLog("adDidComplete: \(interstitialController)")
    }
 
    // Called when the user clicks on an ad and a click-through is
    // about to occur.
    func adWasClicked(interstitialController:OXMInterstitialController) {
        NSLog("adWasClicked: \(interstitialController)")
    }
 
    // Called when the user closes a click-through.
    func adClickthroughDidClose(interstitialController:OXMInterstitialController) {
        NSLog("adClickthroughDidClose: \(interstitialController)")
    }
 
    // Called when an MRAID ad expands.
    func adDidExpand(interstitialController:OXMInterstitialController) {
        NSLog("adDidExpand: \(interstitialController)")
    }
 
    // Called when an MRAID ad collapses.
    func adDidCollapse(interstitialController:OXMInterstitialController) {
        NSLog("adDidCollapse: \(interstitialController)")
    }
 
    // Called when the ad leaves the app.
    func adDidLeaveApplication(interstitialController:OXMInterstitialController) {
        NSLog("adDidLeaveApplication: \(interstitialController)")
    }
 
    // Called when a displayed interstitial, closes by user.
    func adInterstitialDidClose(interstitialController:OXMInterstitialController) {
        NSLog("adInterstitialDidClose: \(interstitialController)")
    }
 
}
```

Objective-C code sample
------------------------------------

**ViewController.h**

``` objc
// Contents of file: ViewController.h
#import <UIKit/UIKit.h>
#import <OpenXSDKCore/OpenXSDKCore.h>
  
@interface ViewController : UIViewController <OXMInterstitialControllerDelegate>
  
@property IBOutlet OXMInterstitialController* interstitialController;
@property IBOutlet UIButton* showButton;
  
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
    [self.showButton setEnabled: NO];
 
    self.interstitialController.adUnitId = @"123456789";
    self.interstitialController.domain = @"pub-d.openx.net";
    self.interstitialController.delegate = self;
    self.interstitialController.flexAdSize = OXMFlexAdSize.Interstitial_1024x768_480x320_300x250;
    self.interstitialController.userParameters.userGender = OXMGenderMale;
    self.interstitialController.userParameters.userAge = 21;
    self.interstitialController.autoDisplayOnLoad = NO;
    [self.interstitialController load];
}
 
#pragma mark OXMInterstitialControllerDelegate
// Called every time an ad has loaded and is ready for display. If you
// experience an ad quality issue, you can identify the ad by the transactionId
// in the adDetails object.
- (void)adDidLoad:(nonnull OXMInterstitialController *)interstitialController adDetails:(nonnull OXMAdDetails *)adDetails {
    NSLog(@"Openx ad loaded: %@ with transaction id: %@", interstitialController, adDetails.transactionId);
                
    // When appropriate, show the interstitial.
    [self.interstitialController showAsInterstitialFromRoot:self];
}
 
// Called whenever the load process fails to produce a viable ad.
- (void)adDidFailToLoad:(nonnull OXMInterstitialController *)interstitialController error:(nonnull NSError *)error {
    NSLog(@"adDidFailToLoad: %@, error: %@", interstitialController, error);
}
 
// Called after an ad has rendered to the device's screen.
- (void)adDidDisplay:(nonnull OXMInterstitialController *)interstitialController {
    NSLog(@"adDidDisplay: %@", interstitialController);
}
 
// Called once an ad has finished displaying all of its creatives.
- (void)adDidComplete:(nonnull OXMInterstitialController *)interstitialController {
    NSLog(@"adDidComplete: %@", interstitialController);
}
 
// Called when the user clicks on an ad and a click-through is about to occur.
- (void)adWasClicked:(nonnull OXMInterstitialController *)interstitialController {
    NSLog(@"adWasClicked: %@", interstitialController);
}
 
// Called when the user closes a click-through.
- (void)adClickthroughDidClose:(nonnull OXMInterstitialController *)interstitialController {
    NSLog(@"adClickthroughDidClose: %@", interstitialController);
}
 
// Called when an MRAID ad expands.
- (void)adDidExpand:(OXMInterstitialController * _Nonnull)interstitialController{
    NSLog(@"adDidExpand: %@", interstitialController);
}
 
// Called when an MRAID ad collapses.
- (void)adDidCollapse:(OXMInterstitialController * _Nonnull)interstitialController{
    NSLog(@"adDidCollapse: %@", interstitialController);
}
 
// Called when a displayed interstitial, closes by user.
- (void)adInterstitialDidClose:(nonnull OXMInterstitialController *)interstitialController {
    NSLog(@"adInterstitialDidClose: %@", interstitialController);
}
 
@end
```
