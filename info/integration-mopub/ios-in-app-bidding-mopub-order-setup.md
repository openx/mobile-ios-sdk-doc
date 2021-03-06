# MoPub Setup

## Overview

One of the most used kind of In-App Bidding integration is to run a parallel auction and receive a winning bid first and then inject an opportunity to display this bid into the waterfall running on the Primary Ad Server. 

This can be achieved by adding special Line Items marked with particular targetting keywors. Each line item should serve a custom creative, which will signal Apollo SDK that  the winning bid should be rendered. 

If such line item wins on the Primary Ad Server the winning bid will be displayed, otherwise, some other ad from the watterfal will be rendered. This document describes how to setup Apollo Line Items on the MoPub server. 

### Best Practises 

From the very beginning publishers should pay attention to the Best Practices of configuring orders on the Primary Ad Server. It will help to improve monetization from the first steps. 

In order to get the best revenue publishers have to create Line Items with unique price targets according to the [price granularity](http://prebid.org/prebid-mobile/adops-price-granularity.html#autoGranularityBucket) policy. That means that it is necessary to create more than one hundred line items to get the best coverage.

Publishers can do it by hands, develop special scripts, or using some tool for generating orders like [PubMonkey](https://chrome.google.com/webstore/detail/pubmonkey/cjbdhopmleoleednpeaknmmbepfkhaml?hl=en)
 
## Order Setup

### Step 1: Create New Order

 <img src="../res/orders/order-mopub-create.png" alt="Pipeline Screenshot" align="center">
 
### Step 2: Create Line Item
 
#### Line Item: Display, Video

To integrate the In-App Bidding into your app you have to create a Custom Ad Network Line Item with a specific Targeting keyword. Note that `Custom Ad Network` type is not suitable for Native Style Ads, see [Native Style Line Item and creative](#native-style-line-item-and-creative) for more details.

Regardless of the ability to name a Line Item in any way we strongly suggest using the price or targeting keyword in the name. It will help you when you will create a hundred of them.

- **Line Item Name**: hb_pb 0.10
- **Type & Priority**: Network Line Item
- **Network**: Custom SDK network
- **Custom event class**: 
    - For Banner API: **OXAMoPubBannerAdapter**  
    - For Interstitial API: **OXAMoPubInterstitialAdapter**
    - For Rewarded API: **OXAMoPubRewardedVideoAdapter**
    - For Native API: ***TODO***
- **Custom event data**: {}

<img src="../res/orders/order-mopub-li-type.png" alt="Pipeline Screenshot" align="center">

#### Line Item: Native

If you integrate Native Ads not via mediation you should create regular line tiems

<img src="../res/orders/order-mopub-order-native.png" alt="Pipeline Screenshot" align="center">

After that you should create a custom Native creative with **obligatory** property **isApolloCreative** and value **true**.

<img src="../res/orders/order-mopub-creative-native.png" alt="Pipeline Screenshot" align="center">

This property will show Apollo SDK that it should render the ad from the winning bid.

#### Line Item: Native Style

Native styles ads are using `non-guaranteed` line item type and Medium Rectangle format HTML creative.

<img src="../res/orders/order-mopub-native-ad-li.png" alt="Pipeline Screenshot" align="center">

MoPub 300x250 Medium Rectangle format HTML creative example:

<img src="../res/orders/order-mopub-native-ad-creative.png" alt="Pipeline Screenshot" align="center">

**The sample of Native Styles Creative:**

``` html
<div class="sponsored-post">
  <div class="thumbnail"></div>
  <div class="content" class="pb-click">
	<h2><p><span style="display:inline-block;"><img src="hb_native_icon" alt="hb_native_icon" width="40" height="40"></span> hb_native_title</p></h2>
	<p>hb_native_body</p>
	<a target="_blank" href="hb_native_linkurl" class="pb-click">hb_native_cta</a>
	<img src="hb_native_image" alt="hb_native_image" width="300" height="50">
	<div class="attribution">hb_native_brand</div>
  </div>
</div>
<script src="https://cdn.jsdelivr.net/npm/prebid-universal-creative@latest/dist/native-trk.js"></script>
<script>
  var pbNativeTagData = {};
  pbNativeTagData.uuid = "%%KEYWORD:hb_cache_id%%";
  pbNativeTagData.env = "%%KEYWORD:hb_env%%";
  pbNativeTagData.cacheHost = "%%KEYWORD:hb_cache_host%%";
  pbNativeTagData.cachePath = "%%KEYWORD:hb_cache_path%%";
  window.pbNativeTag.startTrackers(pbNativeTagData);
</script>
```

#### Ad Unit Targeting

<img src="../res/orders/order-mopub-li-ad-unit.png" alt="Pipeline Screenshot" align="center">

#### Audience Targeting

The **Keyword targeting** property should contain a special keyword with the price of winning bid.

<img src="../res/orders/order-mopub-li-audience.png" alt="Pipeline Screenshot" align="center">


