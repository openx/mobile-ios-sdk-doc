# Apollo: Native Ads Integration

## Unified Native Ads

The rendering using native components is not supported yet. This ad format is scheduled for the next version - **Apollo SDK 1.2**.

## Native Styles

[See Pure In-App Bidding Integration page](../integration-gam/ios-in-app-bidding-gam-info.md) for more details about SDK integration and supported ad types.

To display an ad using Native Styles you'll need to implement these easy steps:

``` swift
// 1. Create an Ad View
let banner = OXABannerView(configId: APOLLO_CONFIG_ID,
                           adSize: adSize)
    
banner.delegate = self

// 2. Set the Native Ad Configurations
let nativeAdConfig = OXANativeAdConfiguration(testConfigWithAssets: assets)
nativeAdConfig.nativeStylesCreative = nativeStylesCreative

banner.nativeStylesCreative = nativeAdConfig
    
// 3. Load an Ad
banner.loadAd()
```

And assign the [delegate](../ios-in-app-bidding-delegates.md) for processing ad events.

#### Step 1: Create Ad View

In the Pure In-App Bidding scenario you just need to initialize the Banner Ad View using correct properties:

- **configId** - an ID of Stored Impression on the Apollo server.
- **size** - the size of the ad unit which will be used in the bid request.


**IMPORTANT:**

You should add HTML and CSS to define your native ad template with universal creative and provide it via the nativeStylesCreative  property of OXANativeAdConfiguration.

#### Step 2: Create and provide Native Assets

To make a proper bid request publishers should provide the needed assets to the OXANativeAdConfiguration class. Each asset describes the UI element of the ad according to the [OpenRTB standarts](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf). 

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

Native Styles creative example:

``` html
<div class="sponsored-post">
    <div class="thumbnail">
        <img src="hb_native_icon" alt="hb_native_icon" width="50" height="50"></div>
    <div class="content">
        <h1><p>hb_native_title</p></h1>
        <p>hb_native_body</p>
        <a target="_blank" href="hb_native_linkurl" class="pb-click">hb_native_cta</a>
        <div class="attribution">hb_native_brand</div>
    </div>
    <img src="hb_native_image" alt="hb_native_image" width="320" height="50">
</div>
<script src="https://cdn.jsdelivr.net/npm/prebid-universal-creative@latest/dist/native-trk.js"></script>
<script>
  let pbNativeTagData = {};
  pbNativeTagData.targetingMap = %%PATTERN:TARGETINGMAP%%;

  window.pbNativeTag.startTrackers(pbNativeTagData);
</script>
```


See the full descriptionn of OXANativeAdConfiguration options [here](../native/ios-native-ad-configuration.md).


#### Step 3: Load the Ad

Simply call `loadAd()` and SDK will:

- make a bid request to Apollo
- render the winning bid on display


