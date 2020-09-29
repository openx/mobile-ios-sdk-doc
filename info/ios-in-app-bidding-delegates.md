# In-App Bidding Delegates


The tables below list the delegate methods that the In-App Bidding SDK supports for banner, interstitial, and rewarded ads in the **Google Ad Manager** and **Pure In-App Bidding** facades.

## OXABannerViewDelegate protocol

| Delegate method        | Implementation | Invoked when                                             |
| ---------------------- |----------------| ------------------------------------------------------------ |
|`bannerViewPresentationController`         | **required** | Provides the certain View Controller to present modal view after click or expand for MRAID.|
| `bannerViewDidReceiveAd:adSize:`          | *optional* | An ad is loaded though not necessarily shown. |
| `bannerView:didFailToReceiveAdWithError:` | *optional* | The load process fails to produce a viable ad. |
| `bannerViewWillPresentModal`              | *optional* | Notifies delegate that the banner view will launch a modal on top of the current view controller, as a result of user interaction. |
| `bannerViewDidDismissModal`               | *optional* | Notifies delegate that the banner view has dismissed the modal on top of the current view controller.|
| `bannerViewWillLeaveApplication`          | *optional* | The ad's creative's navigation caused the user to exit the app. For example, the user clicked a link in the ad that opened the mobile browser. |


## OXAInterstitialAdUnitDelegate protocol


| Delegate method        | Implementation |Invoked when                                             |
| ---------------------- |----------------|------------------------------------------------------------ |
| `interstitialDidReceiveAd`                    | *optional* | An ad is loaded though not necessarily shown. |
| `interstitial:didFailToReceiveAdWithError:`   | *optional* | The load process fails to produce a viable ad.|
| `interstitialClickthroughDidClose`            | *optional* | The in-app browser, opened as a result of clicking an ad has closed. |
| `interstitialWillPresentAd`                   | *optional* | Called when the interstitial view will be launched,  as a result of the `show()` method.|
| `interstitialDidDismissAd`                    | *optional* | Called when the interstitial is dismissed by the user.|
| `interstitialDidClickAd`                      | *optional* | A user clicks an ad, an in-app browser is opened. |
| `interstitialWillLeaveApplication`            | *optional* | The navigation of the ad's creative caused the user to exit the app. For example, the user clicked a link in the ad that opened the mobile browser. |

## OXARewardedAdUnitDelegate protocol


| Delegate method        | Implementation |Invoked when                                             |
| ---------------------- |----------------|------------------------------------------------------------ |
| `rewardedAdDidReceiveAd`                    | *optional* | An ad is loaded though not necessarily shown. |
| `rewardedAdUserDidEarnReward`                    | *optional* |Called when user is able to receive a reward from the app. |
| `rewardedAd:didFailToReceiveAdWithError:`   | *optional* | The load process fails to produce a viable ad.|
| `interstitialClickthroughDidClose`            | *optional* | The in-app browser, opened as a result of clicking an ad has closed. |
| `rewardedAdWillPresentAd`                   | *optional* | Called when the interstitial view will be launched,  as a result of the `show()` method.|
| `rewardedAdDidDismissAd`                    | *optional* | Called when the interstitial is dismissed by the user. |
| `rewardedAdDidDismissAd`                      | *optional* | A user clicks an ad, an in-app browser is opened. |
| `rewardedAdWillLeaveApplication`            | *optional* | The navigation of the ad's creative caused the user to exit the app. For example, the user clicked a link in the ad that opened the mobile browser. |
