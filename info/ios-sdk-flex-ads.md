Flex ads for OpenX Mobile iOS SDK
=================================

Last updated on June 26, 2018

The OpenX user interface supports choosing multiple ad sizes for an ad
unit. By default, the setting in the UI will result in ad delivery of
any one of these sizes based on best possibility of monetization. If you
want to specify a subset of your ad units\' supported ad sizes at
delivery time, you can provide the allowed sizes in the `flexAdSize`
parameter.

> **Note:** This approach does not apply to video interstitial ads, because VAST
specifications already support multiple media files.

Allowing multiple ad sizes for an ad unit (flexible ad sizes) allows for
better monetization because more ad sizes can fill an impression, but it
also means that in some cases, a smaller ad may fill, and this could
create more blank space. If user experience is important, you may prefer
to use a single ad size.

-   Example using a predefined value:
    `oxmBannerView.flexAdSize = OXMFlexAdSize.Interstitial_320x480_300x250`
-   Example using a comma-delimited list of sizes:
    `oxmBannerView.flexAdSize = "728x90,320x50"`
-   Example using a single custom size:
    `oxmBannerView.flexAdSize = "728x90"`

If you do not set these values programmatically, then the values set in
the UI will be used for bid requests.

The following are predefined values that you can use for this parameter:

``` swift
OXMFlexAdSize.Banner_320x50
OXMFlexAdSize.Banner_300x250
OXMFlexAdSize.Banner_320x50_300x250
OXMFlexAdSize.Interstitial_320x480
OXMFlexAdSize.Interstitial_300x250
OXMFlexAdSize.Interstitial_480x320
OXMFlexAdSize.Interstitial_768x1024
OXMFlexAdSize.Interstitial_1024x768

// Flexible ad sizes for portrait, phone
OXMFlexAdSize.Interstitial_320x480_300x250

 
// Flexible ad sizes for landscape, phone
OXMFlexAdSize.Interstitial_480x320_300x250

// Flexible ad sizes for portrait, tablet
OXMFlexAdSize.Interstitial_768x1024_320x480_300x250
 
// Flexible ad sizes for landscape, tablet
OXMFlexAdSize.Interstitial_1024x768_480x320_300x250
```