# Google Ad Manager Integration

The integration of Apollo SDK with Google Ad Manager (GAM) assumes that publisher has an account on GAM and has already integrated the GAM SDK into the app project. Apollo SDK was tested with **GAM SDK 7.61.0**. If you have any trouble with this or other versions, please, contact the [Apollo Support](https://www.openx.com/prebid/#form).

If you do not have GAM SDK in the app yet, refer the the [Google Integration Documentation](https://developers.google.com/ad-manager/mobile-ads-sdk/ios/quick-start).


## Order Setup 

To integrate header bidding with GAM you have to prepare a specific Order following the [instructions](ios-in-app-bidding-gam-order-setup.md) for particular ad kind.

### Rendering of vanilla prebid orders

If you want to run In-App Biding with Apollo using your Prebid orders on GAM you do not have to change anything on GAM. **Apollo SDK is able to work with prebid orders**. Just replace Prebid SDK with Apollo SDK and follow the current integration instructions. 

> Subsequently, we recommend to switch to Apollo orders in order to get better rendering, measurement and targeting.
 
## GAM Integration Overview

<img src="../res/Apollo-In-App-Bidding-Overview-GAM.png" alt="Pipeline Screenshot" align="center">

**Steps 1-2** Apollo SDK makes a bid request. Apollo server runs an auction and returns the winning bid to the SDK.

**Step 3** Apollo SDK via GAM Event Handler sets up targeting keywords into the GAM's ad unit.

**Step 4** GAM SDK makes an ad request. GAM returns the winner of the waterfall.

**Step 5** Basing on the ad response Apollo GAM Event Handler decided who won on the GAM - the Apollo bid or another ad source on GAM.

**Step 6** The winner is displayed in the App with the respective rendering engine.
  

Apollo SDK supports these ad formats:

- Display Banner
- Display Interstitial
- Native
- [Native Styles](ios-in-app-bidding-gam-native-integration.md)
- Video Interstitial 
- Rewarded Video
- Outstream Video

They can be integrated using these API categories.

- [**Banner API**](#Banner-API) - for *Display Banner* and *Outstream Video*
- [**Interstitial API**](#Interstitial-API) - for *Display* and *Video* Interstitials
- [**Rewarded API**](#Rewarded-API) - for *Rewarded Video*
- [**Native API**](ios-in-app-bidding-gam-native-integration.md) - for *Native Ads*


## Init Apollo SDK

Add the following line to your project’s podfile and install the pod:

```
pod 'openx-apollo-sdk'
```

Provide an **Account Id** of your organization on Apollo server:

```
OXASDKConfiguration.singleton.accountID = YOUR_ACCOUNT_ID
```

The best place to do it is the `application:didFinishLaunchingWithOptions` method. 

> **NOTE:** The account ID is an identifier of the **Stored Request** of your organization in the Apollo UI. 

### Event Handlers

GAM Event Handlers is a set of classes that wrap the GAM Ad Units and manage them respectively to the In-App Bidding flow. These classes are provided in the form of framework that could be added to the app via CocoaPods:

```
pod 'openx-apollo-gam-event-handlers'
```

Or you can [download](http://sdk.prod.gcp.openx.org/apollo/ios/event-handlers/GAM/1.2.0/OpenX_Apollo_GAMEventHandlers_iOS_1.2.0.zip) it manually and add to the project as any other third-party framework.


## Banner API

To integrate a banner ad you have to implement three easy steps:


``` swift
// 1. Create an Event Handler
let eventHandler = OXAGAMBannerEventHandler(adUnitID: GAM_AD_UNIT_ID,
                                            validGADAdSizes: [NSValueFromGADAdSize(adSize)])
       
// 2. Create a Banner View
let banner = OXABannerView(configId: APOLLO_CONFIG_ID,
                           eventHandler: eventHandler)
banner.delegate = self

addBannerToUI(banner: banner)
        
// 3. Load an Ad
banner.loadAd()
```

#### Step 1: Create Event Handler

GAM event handlers are special containers that wrap GAM Ad Views and help to manage collaboration between GAM and OpenX views.

**Important:** you should create and use a unique event handler for each ad view.

To create the event handler you should provide a GAM Ad Unit Id and the list of available sizes for this ad unit.


#### Step 2: Create Ad View

**OXABannerView** - is a view that will display the particular ad. It should be added to the UI. To create it you should provide:

- **configId** - an ID of Stored Impression on the Apollo server
- **eventHandler** - the instance of the banner event handler

Also, you should add the instance of `OXABannerView` to the UI.

And assign the [delegate](../ios-in-app-bidding-delegates.md) for processing ad events.


#### Step 3: Load the Ad

Simply call the `loadAd()` method to start the [In-App Bidding](../ios-in-app-bidding-getting-started.md) flow. Apollo SDK will start the bidding process right away.

### Outstream Video

For **Outstream Video** you also need to specify the kind of expected ad:

``` swift
banner.adFormat = .video
```

And all the rest code will be the same as for integration of display banner.


## Interstitial API

To integrate interstitial ad you need to implement four easy steps:


``` swift
// 1. Create Event Handler
let eventHandler = OXAGAMInterstitialEventHandler(adUnitID: GAM_AD_UNIT_ID)
    
// 2. Create Interstitial Ad Unit
interstitial = OXAInterstitialAdUnit(configId: APOLLO_CONFIG_ID,
                                     minSizePercentage: CGSize(width: 30, height: 30),
                                     eventHandler: eventHandler)
    
interstitial.delegate = self
    
// 3. Load an Ad
interstitial.loadAd()

/// .......

// 4. Show Ad
if interstitial.isReady {
    interstitial.show(from: self)
}

```

The way of displaying **Video Interstitial Ad** is almost the same with two differences:

- Need to customize the ad unit kind
- No need to set up `minSizePercentage`

``` swift
 // 1. Create Event Handler
let eventHandler = OXAGAMInterstitialEventHandler(adUnitID: GAM_AD_UNIT_ID)
    
// 2. Create Interstitial Ad Unit
interstitial = OXAInterstitialAdUnit(configId: APOLLO_CONFIG_ID,
                                     eventHandler: eventHandler)
    
interstitial.adFormat = .video
interstitial.delegate = self
    
// 3. Load an Ad
interstitial.loadAd()

/// .......

// 4. Show Ad
if interstitial.isReady {
    interstitial.show(from: self)
}

```


#### Step 1: Create Event Handler

GAM's event handlers are special containers that wrap the GAM Ad Views and help to manage collaboration between GAM and OpenX views.

**Important:** you should create and use a unique event handler for each ad view.

To create an event handler you should provide a GAM Ad Unit.

#### Step 2: Create Interstitial Ad Unit

**OXAInterstitialAdUnit** - is an object that will load and display the particular ad. To create it you should provide: 

- **configId** - an ID of Stored Impression on the Apollo server
- **minSizePercentage** - specifies the minimum width and height percent an ad may occupy of a device’s real estate.
- **eventHandler** - the instance of the interstitial event handler

Also, you can assign the [delegate](../ios-in-app-bidding-delegates.md) for processing ad events.

> **NOTE:** minSizePercentage - plays an important role in a bidding process for display ads. If provided space is not enough demand partners won't respond with the bids.


#### Step 3: Load the Ad

Simply call the `loadAd()` method to start [In-App Bidding](../ios-in-app-bidding-getting-started.md) flow. The ad unit will load an ad and will wait for explicit instructions to display the Interstitial Ad.


#### Step 4: Show the Ad when it is ready


The most convenient way to determine if the interstitial ad is ready for displaying is to subscribe to the particular [delegate](../ios-in-app-bidding-delegates.md) method:

``` swift
// MARK: OXAInterstitialAdUnitDelegate
    
func interstitialDidReceiveAd(_ interstitial: OXAInterstitialAdUnit) {
    // Now the ad is ready for display
}
```

## Rewarded API

To display an Rewarded Ad need to implement four easy steps:


``` swift
 // 1. Create an Event Handler
let eventHandler = OXAGAMRewardedEventHandler(adUnitID: GAM_AD_UNIT_ID)
    
// 2. Create an Ad Unit
rewardedAd = OXARewardedAdUnit(configId: APOLLO_CONFIG_ID,
                               eventHandler: eventHandler)
    
rewardedAd.delegate = self
    
// 3. Load an Ad
rewardedAd.loadAd()

/// .......

// 4. Display Ad
if rewardedAd.isReady {
    rewardedAd.show(from: self)
}

```

The way of displaying the **Rewarded Ad** is totally the same as for the Interstitial Ad. 


To be notified when user earns a reward - implement the method of `OXARewardedAdUnitDelegate`:

``` swift
- (void)rewardedAdUserDidEarnReward:(OXARewardedAdUnit *)rewardedAd;
```

The actual reward object is stored in the `OXARewardedAdUnit`: 

```
if let reward = rewardedAd.reward as? GADAdReward {
    // ...
}
```

#### Step 1: Create Event Handler

GAM's event handlers are special containers that wrap the GAM Ad Views and help to manage collaboration between GAM and OpenX views.

**Important:** you should create and use a unique event handler for each ad view.

To create an event handler you should provide a GAM Ad Unit.


#### Step 2: Create Rewarded Ad Unit

**OXARewardedAdUnit** - is an object that will load and display the particular ad. To create it you should provide:

- **configId** - an ID of Stored Impression on the Apollo server
- **eventHandler** - the instance of rewarded event handler

Also, you can assign the [delegate](../ios-in-app-bidding-delegates.md) for processing ad events.


#### Step 3: Load the Ad

Simply call the `loadAd()` method to start [In-App Bidding](../ios-in-app-bidding-getting-started.md) flow. The ad unit will load an ad and will wait for explicit instructions to display the Interstitial Ad.


#### Step 4: Show the Ad when it is ready


The most convenient way to determine if the ad is ready for displaying is to subscribe to the particular [delegate](../ios-in-app-bidding-delegates.md) method:

``` swift
// MARK: OXARewardedAdUnitDelegate
    
func rewardedAdDidReceiveAd(_ rewardedAd: OXARewardedAdUnit) {
    // Now the ad is ready for display
}
```
