# iOS App Transport Security (ATS)

App Transport Security (ATS) is an iOS app default setting which prevents apps from making non-secure connections. At the time of this publication, Apple has not yet required secure connections (see [Apple iOS release documentation](https://developer.apple.com/library/content/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html)). 

In versions 4.10 and later, the OpenX Mobile iOS SDK makes secure ad requests (HTTPS) by default. However, many network calls related to the ad are not secure (HTTP), such as those related to resources and events.

If you decide to enable ATS for your app, review and implement the changes described here for tag-based and server-to-server integrations. 

To support non-secure requests, you need to set the `NSAllowsArbitraryLoads` key to `YES` in the app\'s Info.plist file. This will allow non-secure requests in iOS 9 or later from the app directly as well as web views.

>**Important:** Contact OpenX if you have not yet been migrated to an SSL-enabled delivery domain, which includes _.openx.net_ in the URL. Example: example-d.openx.net

## Tag-based integrations

If your app serves ads via a [tag-based integration](https://docs.openx.com/getting_ad_tags.html), you can make your OpenX requests SSL-compliant by:

1. Changing all references of `HTTP` to `HTTPS`. 
2. Ensuring you have an SSL-enabled delivery domain.

### Example

After src=", this tag uses http, which is not SSL-compliant.

``` javascript
<script type="text/javascript" src="http://ox-d.your-instance.servedbyopenx.com/ma/1.0/jstag"></script>
```

This tag becomes SSL-compliant after you change `http` to `https` and migrate to an SSL-enabled delivery domain, as shown below.

```javascript
<script type="text/javascript" src="https://example-d.openx.net/ma/1.0/jstag"></script>
```

## Server-to-server (API) integrations

If your app serves ads via a [server-to-server](https://docs.openx.com/developers/ad_request_api/mobile_ads.html) (S2S), or API integration, you can make your OpenX requests SSL-compliant by:

1. Changing your request protocol from `HTTP` to `HTTPS`.
2. Ensuring your have an SSL-enabled delivery domain.

### Example

This request protocol is **not** SSL-compliant.

```http
http://ox-d.your-instance.servedbyopenx.com/ma/1.0/arj?auid=123456789​
```

This request protocol becomes SSL-compliant after you change `http` to `https` and migrate to an SSL-enabled delivery domain, as shown below.

```http
https://example-d.openx.net/ma/1.0/arj?auid=123456789​
```


