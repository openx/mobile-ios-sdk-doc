Delegates
=========

The tables below list the delegate methods that OpenX Mobile iOS SDK supports for banner, interstitial, video interstitial, and opt-in video integration.

OXMBannerViewDelegate protocol
--------------------------------------------------------

| Delegate method        | Implementation | Invoked when                                             |
| ---------------------- |----------------| ------------------------------------------------------------ |
|`viewControllerForModalPresentation`| **required** | Provides the certain View Controller to present modal view including interstitial ads.|
| `bannerDidLoad`         | *optional* | An ad is loaded though not necessarily shown.<br />**Note:**  `AdDetails` includes a `transactionId` that uniquely identifies the ad, which you can use for managing and reporting ad quality issues. |
| `bannerDidFailToLoad`       | *optional* | The load process fails to produce a viable ad.               |
| `bannerClickthroughDidClose` | *optional* | The in-app browser, opened as a result of clicking an ad, has closed. |
| `bannerDidComplete`          | *optional* | An ad has finished displaying all of its creatives.          |
| `bannerDidDisplay`           | *optional* | An ad has rendered to the device's screen, after loading.    |
| `bannerWasClicked`           | *optional* | A user clicks an ad, opening an in-app browser.              |
| `bannerDidExpand`           | *optional* | The MRAID ad was expanded.            |
| `bannerDidCollapse`          | *optional* | The MRAID ad was collapsed.                                  |
| `bannerDidLeaveApplication`  | *optional* | The ad's creative's navigation caused the user to exit the app. For example, the user clicked a link in the ad that opened the mobile browser. |

 
OXMInterstitialControllerDelegate protocol
-------------------------------------------------------------------------

| Delegate method        | Implementation |Invoked when                                             |
| ---------------------- |----------------|------------------------------------------------------------ |
|`viewControllerForModalPresentation`| **required** | Provides the certain View Controller to present modal view including interstitial ads.|
| `interstitialDidLoad`              | *optional* | An ad is loaded though not necessarily shown.<br />**Note:**  `AdDetails` includes a `transactionId` that uniquely identifies the ad, which you can use for managing and reporting ad quality issues. |
| `interstitialDidFailToLoad`         | *optional* | The load process fails to produce a viable ad.               |
| `interstitialClickthroughDidClose`  | *optional* | The in-app browser, opened as a result of clicking an ad, has closed. |
| `interstitialDidComplete`          | *optional* | An ad has finished displaying all of its creatives.          |
| `interstitialDidDisplay`            | *optional* | An ad has rendered to the device's screen, after loading.    |
| `interstitialDidClose`              | *optional* | The interstitial window has closed.                          |
| `interstitialWasClicked`           | *optional* | A user clicks an ad, opening an in-app browser.              |
| `interstitialDidLeaveApplication`   | *optional* | The ad's creative's navigation caused the user to exit the app. For example, the user clicked a link in the ad that opened the mobile browser. |

OXMVideoAdViewDelegate protocol
--------------------------------------------------------------------------------

| Delegate method        | Implementation | Invoked when                                             |
| ---------------------- |----------------| ------------------------------------------------------------ |
|`viewControllerForModalPresentation`| **required** | Provides the certain View Controller to present modal view including interstitial ads.|
| `videoAdViewDidLoad`             | *optional* | An ad is loaded though not necessarily shown.<br />**Note:** `AdDetails` includes a `transactionId` that uniquely identifies the ad, which you can use for managing and reporting ad quality issues. |
| `videoAdViewDidFailToLoad`        | *optional* | The load process fails to produce a viable ad.               |
| `videoAdViewDidDisplay`           | *optional* | An ad has rendered to the device's screen, after loading.    |
| `videoAdViewDidComplete`          | *optional* | An ad has finished displaying all of its creatives.          |
| `videoAdViewInterstitialDidOpen`  | *optional* | Called when the ad is opened in the interstitial mode and continue playing|
| `videoAdViewInterstitialDidClose` | *optional* | Called when a user closed an interstitial|
| `videoAdViewClickthroughDidOpen`  | *optional* | Called when a user opens a clickthrough for the ad. |
| `videoAdViewClickthroughDidClose` | *optional* | Called when the user closes a clickthrough.                          |
| `videoAdViewDidLeaveApplication`  | *optional* | The ad's creative's navigation caused the user to exit the app. For example, the user clicked a link in the ad that opened the mobile browser. |
