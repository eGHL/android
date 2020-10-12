![eghl.png](http://e-ghl.com/assets/img/logo.png)

*Software Development Kit (SDK)* makes it easier to integrate your mobile application with eGHL Payment Gateway. This repository is intended as a technical guide for merchant developers and system integrators who are responsible for designing or programming the respective applications to integrate with Payment Gateway.

[eGHL](http://e-ghl.com) | [Wiki](https://bitbucket.org/eghl/android/wiki/Home) | [Downloads](https://bitbucket.org/eghl/android/downloads/?tab=tags) | [Follow eGHL Repos](https://bitbucket.org/eghl/follow)

****

# **Change Log** 
### [**v2.5.4](https://bitbucket.org/eghl/android/commits/tag/v2.5.4)
* Implemented EMandate

### [**v2.5.3](https://bitbucket.org/eghl/android/commits/tag/v2.5.3)
* Added CustID parameter

### [**v2.5.2](https://bitbucket.org/eghl/android/commits/tag/v2.5.2)
* Include Javascript to remove Popup in WebView

### [**v2.5.1](https://bitbucket.org/eghl/android/commits/tag/v2.5.1)
* Update dependencies and deprecated class

### [**v2.5.0](https://bitbucket.org/eghl/android/commits/tag/v2.5.0)
* Migrate to AndroidX

### [**v2.4.7](https://bitbucket.org/eghl/android/commits/tag/v2.4.7)
* Created setQueryHashValue params to prioritize query HashValue when .setPassword() is not used 

### [**v2.4.6](https://bitbucket.org/eghl/android/commits/tag/v2.4.6)
* Fixed Amount issue when the device's language is set to Indonesia 

### [**v2.4.5](https://bitbucket.org/eghl/android/commits/tag/v2.4.5)
* Fixed JavaScript console issue
* Fixed CardPage validation issue
* Excluded QueryCount from payment URL

### [**v2.4.4](https://bitbucket.org/eghl/android/commits/tag/v2.4.4)
* Fixed decimal formatter bug
* Added QueryCount parameter

### [**v2.4.3](https://bitbucket.org/eghl/android/commits/tag/v2.4.3)
* Enhanced SSL certificate error URL exclusion

### [**v2.4.2](https://bitbucket.org/eghl/android/commits/tag/v2.4.2)
* Enchanced eGHL Optimize 
* Added URL SSL certificate error exclusion

### [**v2.4.1](https://bitbucket.org/eghl/android/commits/tag/v2.4.1)
* Disable popup webview in staging environment

### [**v2.4.0](https://bitbucket.org/eghl/android/commits/tag/v2.4.0)
* Introduce eGHL Optimize
* Fixed cardPan validation error in card page

### [**v2.3.5](https://bitbucket.org/eghl/android/commits/tag/v2.3.5)
* Update card page to retrieve tokenized card.

### [**v2.3.4](https://bitbucket.org/eghl/android/commits/tag/v2.3.4)
* Allow merchant to send HashValue.

### [**v2.3.3](https://bitbucket.org/eghl/android/commits/tag/v2.3.3)
* Fixed sending empty card will cause crash for subsequent payment.
* Fixed added flag to make checkbox for tokenizing become mandatory (by default is not mandatory)
* Added some gap between two card type image.
* Update card default card image to square.

### [**v2.3.2](https://bitbucket.org/eghl/android/commits/tag/v2.3.2)
* Fixed issue wrong card format display when user edit in the middle of the card. 

### [**v2.3.1](https://bitbucket.org/eghl/android/commits/tag/v2.3.1)
* Fixed SDK redirect to Unknown page after key in otp. 
* Fixed SDK redirect to akward page after returing from HOST SIMULATOR for Card payment in staging

### [**v2.3](https://bitbucket.org/eghl/android/commits/tag/v2.3)
* Added card UI

### [**v2.2.10](https://bitbucket.org/eghl/android/commits/tag/v2.2.10)
* fixed issue setting MerchantReturnURL with non-url string will trigger error on nativescript
* fixed issue unable to accept MerchantReturnURL with semicolons
* fixed issue setting TriggerReturnURL will still trigger MerchantReturnURL
* fixed issue SDK returning wrong transaction type

### [**v2.2.9](https://bitbucket.org/eghl/android/commits/tag/v2.2.9)
* Added payment parameter for trigerring return URL ([setTriggerReturnURL()](https://bitbucket.org/eghl/android/src/151f54665198825ad7343217960e8c85f97a3b9d/Demo/app/src/main/java/com/eghl/demosdk/MainActivity.java?at=master&fileviewer=file-view-default#MainActivity.java-107)).

### [**v2.2.8](https://bitbucket.org/eghl/android/commits/tag/v2.2.8)
* Added delayed exit when user exits while SDK is processing the 2nd MPE request.

### [**v2.2.7](https://bitbucket.org/eghl/android/commits/tag/v2.2.7)
* Internal improvement
* New demo layout
* Moved callback detection to onPageStarted (Lightbox)
* will only return WEBVIEW_ERROR on SSL handshake error (Lightbox)
* SSL error dialog references the ones in string.xml (Lightbox)
* Orientation change support for all activities
* Added setRequestBasicCheckout() in LightboxParams.Builder()
* Added no internet connection detection, will show a Toast (Can also be overriden. [See Integration guide](https://bitbucket.org/eghl/android/wiki/Integration%20Guide%20for%20eGHL%20SDK%20v2.x%20in%20Android) Extra Customization section).
* `PaymentActivity` is now in `com.eghl.sdk.payment` package.

### [**v2.2.6](https://bitbucket.org/eghl/android/commits/tag/v2.2.6)
* Prevent exit on masterpass express payment when gateway is not yet loaded

### [**v2.2.5](https://bitbucket.org/eghl/android/commits/tag/v2.2.5)
* Deprecated setExitTitle() and setExitMessage()
* Added ways to override strings messages of the SDK [for example](https://bitbucket.org/eghl/android/src/4121306cbecc13f85dad7a97fe6f620e22ac41b8/Demo/app/src/main/res/values/strings.xml?at=master&fileviewer=file-view-default#strings.xml-5,6,7,8,9,10,11)
* SDk will only return -6767 for SSL error

### [**v2.2.4](https://bitbucket.org/eghl/android/commits/tag/v2.2.5)


* Fix for issue #4: SDK crashing when MerchantReturnURL has a query strings

### [**v2.2.3](https://bitbucket.org/eghl/android/commits/tag/v2.2.3)
* Removed retry policy in all transactions


### [**v2.2.2](https://bitbucket.org/eghl/android/commits/tag/v2.2.2)
* Fixed issue #1 Crash when triggering capture


### [**v2.2.1](https://bitbucket.org/eghl/android/commits/tag/v2.2.1)
* Converted all query strings raw response into a JSON format
* Fixed the bug on backpress when the user went straight to the bank website via IssuingBank parameter and DD value on PaymentMethod


### [**v2.2.0](https://bitbucket.org/eghl/android/commits/tag/v2.2.0)
* TokenType can now be set in MasterpassParams.
* Added Capture transation
* Added way to override the payment gateway and password via Java Code in all EGHL.executeXXX() methods.

### [**v2.1.8](https://bitbucket.org/eghl/android/commits/tag/v2.1.8)
* added support to set the gateway in java instead of setting it in android manifest

### [**v2.1.7](https://bitbucket.org/eghl/android/commits/tag/v2.1.7)
* Added TRANSACTION_ERROR_IN_WEBVIEW result code when there’s an error in loading the page in the WebView 
* Fixed issue in executeQuery() in Kitkat 4.4.2
* Added setExitMessage() and setExitTitle() to the PaymentParams. This will override the default exit message.
* Changed the default message from "Pressing BACK button will...” to "Pressing EXIT button will…” 

### [**v2.1.6](https://bitbucket.org/eghl/android/commits/tag/v2.1.6)
* added instant status instead of doing requery same like iOS behaviour

### [**v2.1.5](https://bitbucket.org/eghl/android/commits/tag/v2.1.5)
* added the following scenario:
	* if user press back button before eghl ladning page finish load, SDK would return Cancelled Status,
	* If user press back button after eghl landing page finish load, SDK will return exactly like when the user click cancel link at the bottom of eGHL landing page.

### [**v2.1.4](https://bitbucket.org/eghl/android/commits/tag/v2.1.4)
* Fixed on user able to terminate requery by tapping the back button
* Fixed on Merchant app receiving Pending status when user click cancel in eGHL Payment Page

### [**v2.1.0](https://bitbucket.org/eghl/android/commits/tag/v2.1.0)
* fixed unable to make payment when passing MerchantCallbackURL to SDK 
* fixed callback not trigger after transaction done
* added SDK timeout to prevent user from making payment at bank side after Transaction time limit reached 
* Added Masterpass integration
