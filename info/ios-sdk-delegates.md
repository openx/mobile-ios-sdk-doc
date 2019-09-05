Delegates
=========

The tables below list the delegate methods that OpenX Mobile iOS SDK supports for banner, interstitial, video interstitial, and opt-in video integration.

> **Note:** All methods are required.

OXMBannerViewDelegate protocol
--------------------------------------------------------

| Delegate method        | **Invoked when**                                             |
| ---------------------- | ------------------------------------------------------------ |
|viewControllerForModalPresentation|Provides the certain View Controller to present modal view including interstitial ads|
| adDidLoad              | An ad is loaded though not necessarily shown.<br />**Note:**  `AdDetails` includes a `transactionId` that uniquely identifies the ad, which you can use for managing and reporting ad quality issues. |
| adDidFailToLoad        | The load process fails to produce a viable ad.               |
| adClickthroughDidClose | The in-app browser, opened as a result of clicking an ad, has closed. |
| adDidComplete          | An ad has finished displaying all of its creatives.          |
| adDidDisplay           | An ad has rendered to the device's screen, after loading.    |
| adWasClicked           | A user clicks an ad, opening an in-app browser.              |
| adDidExpand            | The MRAID ad was expanded.            |
| adDidCollapse          | The MRAID ad was collapsed.                                  |
| adDidLeaveApplication  | The ad's creative's navigation caused the user to exit the app. For example, the user clicked a link in the ad that opened the mobile browser. |

 

OXMInterstitialControllerDelegate protocol
--------------------------------------------------------------------------------

| Delegate method        | **Invoked when**                                             |
| ---------------------- | ------------------------------------------------------------ |
|viewControllerForModalPresentation|Provides the certain View Controller to present modal view including interstitial ads|
| adDidLoad              | An ad is loaded though not necessarily shown.<br />**Note:**  `AdDetails` includes a `transactionId` that uniquely identifies the ad, which you can use for managing and reporting ad quality issues. |
| adDidFailToLoad        | The load process fails to produce a viable ad.               |
| adClickthroughDidClose | The in-app browser, opened as a result of clicking an ad, has closed. |
| adDidComplete          | An ad has finished displaying all of its creatives.          |
| adDidDisplay           | An ad has rendered to the device's screen, after loading.    |
| adInterstitialDidClose | The interstitial window has closed.                          |
| adWasClicked           | A user clicks an ad, opening an in-app browser.              |
| adDidExpand            | The MRAID ad was expanded.                                   |
| adDidCollapse          | The MRAID ad was collapsed.                                  |
| adDidLeaveApplication  | The ad's creative's navigation caused the user to exit the app. For example, the user clicked a link in the ad that opened the mobile browser. |

OXMVideoAdViewDelegate protocol
--------------------------------------------------------------------------------

| Delegate method        | **Invoked when**                                             |
| ---------------------- | ------------------------------------------------------------ |
|viewControllerForModalPresentation|Provides the certain View Controller to present modal view including interstitial ads|
| videoAdViewDidLoad              | An ad is loaded though not necessarily shown.<br />**Note:** `AdDetails` includes a `transactionId` that uniquely identifies the ad, which you can use for managing and reporting ad quality issues. |
| videoAdViewDidFailToLoad        | The load process fails to produce a viable ad.               |
| videoAdViewDidDisplay           | An ad has rendered to the device's screen, after loading.    |
| videoAdViewDidComplete          | An ad has finished displaying all of its creatives.          |
| videoAdViewInterstitialDidOpen  | Called when the ad is opened in the interstitial mode and continue playing|
| videoAdViewInterstitialDidClose | Called when a user closed an interstitial|
| videoAdViewClickthroughDidOpen  | Called when a user opens a clickthrough for the ad. |
| videoAdViewClickthroughDidClose | Called when the user closes a clickthrough.                          |
| videoAdViewDidLeaveApplication  | The ad's creative's navigation caused the user to exit the app. For example, the user clicked a link in the ad that opened the mobile browser. |
