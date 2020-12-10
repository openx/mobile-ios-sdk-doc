# GAM: Native Ads Integration

## Unified Native Ads

The rendering using native components is not supported yet. This ad format is scheduled for the next version - **Apollo SDK 1.2**.

## Native Styles 

[See Google Ad Manager Integration page](ios-in-app-bidding-gam-info.md) for more info about GAM order setup and GAM Event Handler integration.

To integrate a banner ad you need to implement three easy steps:

``` swift
// 1. Create an Event Handler
let eventHandler = OXAGAMBannerEventHandler(adUnitID: GAM_AD_UNIT_ID,
                                            validGADAdSizes: [NSValueFromGADAdSize(adSize)])
       
// 2. Create a Banner View
let banner = OXABannerView(configId: APOLLO_CONFIG_ID,
                           eventHandler: eventHandler)
banner.delegate = self

// 3. Setup Native Ad Configuration
banner.nativeAdConfig = OXANativeAdConfiguration(testConfigWithAssets: assets)
        
// 4. Load an Ad
banner.loadAd()
```


#### Step 1: Create Event Handler

GAM's event handlers are special containers that wrap GAM Ad Views and help to manage collaboration between GAM and OpenX views.

**Important:** you should create and use a unique event handler for each ad view.

To create the event handler you should provide a GAM Ad Unit Id and the list of available sizes for this ad unit.


#### Step 2: Create Ad View

**OXABannerView** - is a view that will display the particular ad. It should be added to the UI. To create it you should provide:

- **configId** - an ID of Stored Impression on the Apollo server
- **eventHandler** - the instance of the banner event handler

Also, you should add the instance of `OXABannerView` to the UI.

And assign the [delegate](../ios-in-app-bidding-delegates.md) for processing ad events.

#### Step 3: Create and provide Native Assets

The make a proper bid request publishers should provide the needed assets to the OXANativeAdConfiguration class. Each asset describes the UI element of the ad according to the [OpenRTB standarts](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf). 

``` swift
let assets = [
    {
        let title = OXANativeAssetTitle(length: 90)
        title.required = true
        return title
    }(),
    {
        let icon = OXANativeAssetImage()
        icon.widthMin = 50
        icon.heightMin = 50
        icon.required = true
        icon.imageType = NSNumber(value: OXAImageAssetType.icon.rawValue)
        return icon
    }(),
    {
        let image = OXANativeAssetImage()
        image.widthMin = 150
        image.heightMin = 50
        image.required = true
        image.imageType = NSNumber(value: OXAImageAssetType.main.rawValue)
        return image
    }(),
    {
        let desc = OXANativeAssetData(dataType: .desc)
        desc.required = true
        return desc
    }(),
    {
        let cta = OXANativeAssetData(dataType: .ctaText)
        cta.required = true
        return cta
    }(),
    {
        let sponsored = OXANativeAssetData(dataType: .sponsored)
        sponsored.required = true
        return sponsored
    }(),
]
```

See the full descriptionn of OXANativeAdConfiguration options [here](../native/ios-native-ad-configuration.md).

#### Step 4: Load the Ad

Simply call the `loadAd()` method to start [In-App Bidding](../ios-in-app-bidding-getting-started.md) flow.