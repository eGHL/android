![eghl.png](http://e-ghl.com/assets/img/logo.png)

*Software Development Kit (SDK)* makes it easier to integrate your mobile application with eGHL Payment Gateway. This repository is intended as a technical guide for merchant developers and system integrators who are responsible for designing or programming the respective applications to integrate with Payment Gateway.

[eGHL](http://e-ghl.com) | [Wiki](https://bitbucket.org/eghl/android/wiki/Home) | [Downloads](https://bitbucket.org/eghl/android/downloads/?tab=tags) | [Follow eGHL Repos](https://bitbucket.org/eghl/follow)

****

# **Change Log** 

### [**v2.1.5](https://bitbucket.org/eghl/android/commits/tag/v2.1.5)
* added the following scenario:
	* if user press back button before eghl landing page finish load, SDK would return Cancelled Status,
	* If user press back button after eghl landing page finish load, SDK will return exactly like when the user click cancel link at the bottom of eGHL landing page.

### [**v2.1.4](https://bitbucket.org/eghl/android/commits/tag/v2.1.4)
* Fixed on user able to terminate requery by tapping the back button
* Fixed on Merchant app receiving Pending status when user click cancel in eGHL Payment Page

### [**v2.1.0](https://bitbucket.org/eghl/android/commits/tag/v2.1.0)
* fixed unable to make payment when passing MerchantCallbackURL to SDK 
* fixed callback not trigger after transaction done
* added SDK timeout to prevent user from making payment at bank side after Transaction time limit reached 
* Added Masterpass integration