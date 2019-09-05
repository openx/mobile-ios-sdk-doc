Testing and troubleshooting
===========================

After you have integrated the OpenX Mobile iOS SDK, you should test your
implementation.

> **Important:** For troubleshooting and diagnostic purposes, please [turn on
logging](#getting-log-files) in the SDK and [install an HTTP debugging
proxy](#installing-charles-web-proxy) such as Charles Web Proxy. You may need to provide logs to OpenX.

General testing requirements
----------------------------

Please make sure that you:

-   Provide a good communication connection on the device, such as reliable wireless network signal. If you can\'t reproduce your problem, it could be a communications issue.
-   Provide a valid user agent if you are expecting live ads through the OpenX Ad Exchange. Testing with a real device that does not have ad tracking limited will help buyers bid on the inventory.
-   Make sure you have embedded the SDK in your app.
-   Make sure you have set the [delegate methods](ios-sdk-delegates.md), which are all required.
-   Make sure you are using the latest version of the SDK. To check for the latest, see [Release notes](ios-sdk-release-notes.md). When the application launches, you should see the version of the SDK that you have installed in the console in Xcode: `OpenXSDK x.x.x Initialized`
-   Make sure you are using the correct delivery domain and ad unit ID provided by OpenX. For incorrect domain and ad unit ID error examples, see [error types and examples](#error-types-and-examples) below.
-   Make sure you are [using Charles](#using-charles) to verify network requests are passing correctly.
-   Make sure you have followed the instructions in [Submitting your app to App Store](ios-sdk-final-steps.md) before you submit your app.

> **Important:** If you encounter issues, see a list of [possible problems and solutions](#troubleshooting) below. If you still can't resolve your issues, get help in [OpenX Community](https://community.openx.com/s/) and make sure to include your Charles logs and any [SDK log files](#getting-log-files).

Turning on logging
------------------------------

To log messages from the SDK, set the [OXMSDKConfiguration](ios-sdk-parameters.md#omxsdkconfiguration) methods below as follows:

-   `debugLogFileEnabled` set to `true`.
-   `logLevel` set to `Info`.

Getting log files
-----------------------------

> **Important:** To get log files from your test device, make sure the device is
connected to Xcode, has the test app on it, and the SDK has logging
enabled.

1.  In Xcode, go to **Window \> Devices and Simulators**.
2.  Navigate to your test device or simulator.
3.  Select your app, click the gear icon next to it, and in the menu that appears, select **Download Container**. This allows you to download the whole container for the app as an .xcappdata package.
4.  Click **Save** to save the package to your local drive.
5.  In the .xcappdata file, Ctrl+click, select **Show package contents** and navigate to the following file:

    App Data \> Documents \> OXMLog.txt

    OXMLog.txt is the log file of the SDK. You can now view, save, or
    share the file as needed. Note that log file contents are in clear
    text and are not encrypted, so you know what you are sending to
    OpenX.

For examples, see [error types and examples](#error-types-and-examples) below.

Installing Charles Web Proxy
-----------------------------------------

An HTTP debugging proxy, such as Charles Web Proxy, allows you to observe network traffic coming from iOS simulators and devices and diagnose issues with your OpenX Mobile iOS SDK implementation. You can download and install Charles from <https://www.charlesproxy.com/>. It works with simulators right out of the box. To get it working with a device, complete the steps in the following documents:

-   <https://www.charlesproxy.com/documentation/faqs/using-charles-from-an-iphone/>
-   <https://www.charlesproxy.com/documentation/configuration/browser-and-system-configuration/>

Using Charles
-----------------------

Use Charles to verify network requests are passing correctly. For
example, to verify that you are sending a valid ad request, copy the ad
request URL from Charles and paste it in your browser and see if you are
getting a valid response.

>  **Tip:** Consider using a filter such as \"openx\" to avoid sifting through a lot of unrelated traffic.

This is an example of a banner ad request where OpenX wins the bid:

![](res/ios-sdk-charles.png)

In a successful implementation, you are likely to see the following
items in the **Path** column:

-   /ma/1.0/acj - The ad request sent to OpenX
-   /ma/1.0/ri - The impression event sent to OpenX
-   /ma/1.0/rc - The click event sent to OpenX, if the OpenX ad is
    clicked

Troubleshooting
----------------------------

| **Problem**                                                  | **Possible reasons**                                         | **What to do**                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Ad not displayed.                                            | No fill (most common).                                       | - Make sure geo data is included and set `autoDetectLocation` to `true` in [OXMBannerView](ios-sdk-parameters.md#oxmbannerview) and/or [OXMInterstitialController](ios-sdk-parameters.md#oxminterstitialcontroller).<br />- Enrich with more user data. See [OXMUserParameters](ios-sdk-parameters.md#oxmuserparameters-variables) |
|                                                              | Incorrect delivery domain .                                  | Make sure you are using the OpenX delivery domain provided by OpenX. |
|                                                              | Incorrect ad unit ID (see [error types and examples](#error-types-and-examples) below). | Make sure you are using the ad unit ID provided by OpenX.    |
|                                                              | Issues with the creative.                                    | Check where creative is coming from. You may need to block certain advertisers, for example. |
|                                                              | App Transport Security (ATS) issue. You may be trying to send HTTP requests over HTTPS. | Set the `NSAllowsArbitraryLoads` key to `YES` in the app's Info.plist file. See [ATS support](ios-sdk-integration.md#ats-support). |
| Ad not displayed correctly, such as a landscape ad appearing for a portrait ad unit. | Line item configuration issue.                               | On your ad server, make sure the line item is trafficking the same orientation as the ad unit. |
| No geo data or other expected auto-detected data.            | - `autoDetectLocation` could be set to `false`.<br />- OpenX Mobile iOS SDK not initialized early enough.<br />- User may not be allowing data to be shared within the app settings. | - Set `autoDetectLocation` to `true` in [OXMBannerView](ios-sdk-parameters.md#oxmbannerview) and/or [OXMInterstitialController](ios-sdk-parameters.md#oxminterstitialcontroller).<br />- Make sure you are initializing the OpenX Mobile iOS SDK early enough for the SDK to get data.<br />- Make sure the user is allowing data to be shared within the app settings. |
| No navigation occurs when user taps on ad, or user sees blank white screen after clicking. | - Creative does not have a click-through link.<br />- Another UI element is laying over the ad.<br />- Creative redirecting to a server that is not set up properly. | Check your creative and your UI view hierarchy to make sure they are set up as expected. |
| No user enrichment data.                                     | - You may not have set all of the user enrichment data that you expected.<br />- User may not be allowing data to be shared within the app settings. | - Make sure you have set all desired user data to be included in ad requests as described in [OXMUserParameters variables](ios-sdk-parameters.md#oxmuserparameters-variables) and [OXMUserParameters methods](ios-sdk-parameters.md#oxmuserparameters-methods).<br />- Make sure the user is allowing data to be shared within the app settings. |
| Ad is refreshing or not refreshing unexpectedly.             | Refresh is not set as expected, either in the OpenX Mobile iOS SDK ad configuration or in your ad server configuration. | Check your refresh setup in the OpenX Mobile iOS SDK and your ad server. See [Request parameters](ios-sdk-parameters.md). |
| No impression or no click tracking recorded.                 |                                                              | Request resolution assistance through the [OpenX Support Community](https://community.openx.com/s/). |
| When attempting to submit to the App Store, an error is displayed: "Code signing OpenXSDKCore.framework failed". Unable to submit to App Store. | You have not removed the simulator architectures from your app. | Follow the instructions in [Submitting your app to App Store](ios-sdk-final-steps.md). |



Error types and examples
----------------------------------

If you have turned on logging on the SDK, you can use error messages to
get information about configuration issues or possible issues that need
to be resolved by OpenX. The following table summarizes the types of
errors that may occur.

| **Error type** | **Reason**                                                   | **What to do**                                               |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| InvalidRequest | Indicates that there could be a problem with your configuration. | Check your configuration. Invalid request errors usually inform you of a missing required setting, such as no ad unit ID specified, no creative specified, or no delivery domain specified. If you need help with troubleshooting configuration errors, please visit the [OpenX Support Community](https://community.openx.com/s/). |
| InternalError  | Indicates a problem with the SDK that needs to be resolved by OpenX. | Please request resolution assistance through the [OpenX Support Community](https://community.openx.com/s/). Make sure to include the error message. |
| ServerError    | Indicates a problem that needs to be resolved by OpenX.      | Please request resolution assistance through the [OpenX Support Community](https://community.openx.com/s/). Make sure to include the error message. |

Below are examples of an `adDidFailToLoad` and error messages that
appear when you use incorrect delivery domain or ad unit ID.

-   If the *delivery domain is incorrect*:

    ``` 
    Error Domain=com.openx Code=0 "SDK internal error: No OXMMediatedAdResult" UserInfo={NSLocalizedDescription=SDK internal error: No OXMMediatedAdResult}
    ```

-   If the *delivery domain is correct*, but the *ad unit is incorrect*:

    ``` 
    Error Domain=com.openx Code=0 "SDK internal error: Ads is empty" UserInfo={NSLocalizedDescription=SDK internal error: Ads is empty}
    ```
