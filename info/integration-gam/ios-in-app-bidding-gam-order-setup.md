# Google Ad Manager Setup

## Overview

The sense of Prebid technology is to run the header bidding auction first and inject an opportunity to display a winning bid into a preconfigured waterfall on the Primary Ad Server. This could be achieved by adding special Line Items which point to the Prebid creative. If such line item wins on the Primary Ad Server the Prebid ad will be rendered on the client, otherwise, the ad from the predefined waterfall will be rendered.

This scenario is totally supported by Apollo.

So the essential part of the Apollo integration is creating special Line Items on the Google Ad Manager.  

## Best Practices

According to Prebid's suggestions, you have to create a set of line items with unique price targets to get the best revenue. Line Items should be created according to the [price granularity](http://Prebid.org/Prebid-mobile/adops-price-granularity.html#autoGranularityBucket) policy. That means that you have to create more than one hundred line items to get the best coverage.

You can either do this manually, develop special scripts, or use some tool to generate orders like [PubMonkey](https://chrome.google.com/webstore/detail/pubmonkey/cjbdhopmleoleednpeaknmmbepfkhaml?hl=en).

## Order Setup

### Manual

#### Step 1: Create New Order

 <img src="../res/orders/order-gam-create.png" alt="Pipeline Screenshot" align="center">

### Step 2: Create Line Item

To integrate the In-App Bidding into the app you have to create a Line Item with a specific price and targeting keyword.

Regardless of the ability to name a Line Item in any way we strongly suggest using the price or targeting keyword in the name. It will help you when you create a hundred of them.

#### Line Item Type

Create a Line Item depending on the type of expected creative type.

<img src="../res/orders/order-gam-li-create.png" alt="Pipeline Screenshot" align="center">

#### Line Item Price

The Line Item price should be chosen according to the price granularity policy.

<img src="../res/orders/order-gam-li-price.png" alt="Pipeline Screenshot" align="center">

#### Line Item Targeting

The **Custom targeting** property should contain a special keyword with the price of winning bid. The same as a Rate of the Line Item.

<img src="../res/orders/order-gam-li-targeting.png" alt="Pipeline Screenshot" align="center">


### Creative

The In-App Bidding SDK renders the Apollo's bid when GAM SDK receives a creative with special meta information.  

#### Display Banner, Display Interstitial, Video Interstitial, Outstream Video.


The In-App Bidding Facade for GAM is based on the [App Events](https://developers.google.com/ad-manager/mobile-ads-sdk/ios/banner#app_events) feature almost for all kinds of ads. That means that a creative should contain a special tag that will be processed by GAM Event Handlers.

``` js
<script type="text/javascript" src="https://media.admob.com/api/v1/google_mobile_app_ads.js">
</script>
<script type="text/javascript">admob.events.dispatchAppEvent("oxbSdkAppEvent","");</script>
```

<img src="../res/orders/order-gam-creative-banner.png" alt="Pipeline Screenshot" align="center">


#### Rewarded Video

The In-App Bidding facade for Rewarded video ads is based on [GADRewardedAdMetadataDelegate](https://developers.google.com/admob/ios/api/reference/Protocols/GADRewardedAdMetadataDelegate). So you need to set up a special VAST tag in the creative.

``` js
https://sdk.prod.gcp.openx.org/ads/inapp_bidding/gam_rewarded.xml
```

<img src="../res/orders/order-gam-creative-rewarded.png" alt="Pipeline Screenshot" align="center">

### Automatic


To implement proper [price granularity](http://Prebid.org/Prebid-mobile/adops-price-granularity.html#autoGranularityBucket) you have to create more than a hundred Line Items. You can either do this manually or by using the free Chrome extension [PubMonkey](https://chrome.google.com/webstore/detail/pubmonkey/cjbdhopmleoleednpeaknmmbepfkhaml?hl=en).

#### Setup Order Properties

To generate an Order you just need to set generic parameters and the custom creative code:

<img src="../res/orders/order-gam-pubmonkey-form.png" alt="Pipeline Screenshot" align="center">


#### Inspect the Line Items

After a few minutes the Order with **170 Line Items** is ready to work:

<img src="../res/orders/order-gam-pubmonkey-result.png" alt="Pipeline Screenshot" align="center">
