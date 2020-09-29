Logging
=======

Last updated on July 11, 2018

If you have `OXASDKConfiguration.debugLogFileEnabled` set to `true` and `OXASDKConfiguration.logLevel` set to `Info`, `Warn`, or `Error`, you will be able to log messages from the SDK.

How to get logs
---------------

You may have to provide your logs for troubleshooting purposes, for example, through the [OpenX Support Community](https://community.openx.com/s/). You can get logs from your test device if it is connected to Xcode and your device has the test app on it. Note that logs are in plain text and are not encrypted, so you know what you are sending to OpenX. The log file is in the Documents directory of the container.

1.  In Xcode, go to **Window \> Devices and Simulators**.
2.  Navigate to your test device or simulator.
3.  Click to select your app and then click the gear icon. In the menu
    that appears, select **Download Container**. This allows you to
    download the whole container for the app as an .xcappdata package.
4.  Click **Save** to save the package to your local drive.
5.  On the .xcappdata file, Ctrl+click and select **Show package contents** to navigate to the following file:

    App Data \> Documents \> OXALog.txt

    This is the log file of the SDK. You can now view, save, or share the file as needed.

The SDK creates this file and logs events as long as
`debugLogFileEnabled = true`. See [Request parameters](ios-sdk-parameters.md) for details.

Error types
-----------

Error messages can inform you of configuration or any possible issue that need to be resolved by OpenX. The following table summarizes the types of errors that may occur.

|Error type         |Reason                                                                 |What to do|
|-------------------|-----------------------------------------------------------------------|-----------|
|`InvalidRequest`   |Indicates that there could be a problem with your configuration.       |Check your configuration. Invalid request errors usually inform you of a missing required settings, such as server account ID, configuration ID or creative. If you need help with troubleshooting configuration errors, please visit the [OpenX Support Community](https://community.openx.com/s/).|
|`InternalError`    |Indicates a problem with the SDK that needs to be resolved by OpenX.   |Please request resolution assistance through the [OpenX Support Community](https://community.openx.com/s/). Make sure to include the error message.|
|`ServerError`      |Indicates a problem that needs to be resolved by OpenX.                |Please request resolution assistance through the [OpenX Support Community](https://community.openx.com/s/). Make sure to include the error message.|
