Using Interface Builder
==================================

After you [integrate the OpenX Mobile iOS SDK](ios-sdk-integration.md),
you can use Interface Builder to set up `OXMBannerView` and `OXMVideoAdView` when integrating banner or video ads into your app.

To set up ad views in Interface Builder:

1.  In Interface Builder, create and position a `UIView`.
2.  Set the `UIView` to the correct size for your ad unit.
3.  Select the `UIView` and navigate to the **Identity Inspector**.
4.  In the **Custom Class** section, set **Class** to the appropriate class, `OXMBannerView` or `OXMVideoAdView`.
5.  Continue to integrate your ad into your app:
    -   [Banner ad integration](ios-sdk-banner-integration.md)
    -   [300x250 Video integration](ios-sdk-video-300x250n.md)
