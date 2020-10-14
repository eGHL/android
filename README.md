![eghl.png](http://e-ghl.com/assets/img/logo.png)

*Software Development Kit (SDK)* makes it easier to integrate your mobile application with eGHL Payment Gateway. This repository is intended as a technical guide for merchant developers and system integrators who are responsible for designing or programming the respective applications to integrate with Payment Gateway.

## Supported Platform

 - Ready for Android API 19 and above
 - Minimum Android version 4.4 and above
 - Android Studio
 
 ## Integration
 
 1. Create a libs folder (if needed) at path your-project/android/app/libs & copy .aar file to libs folder
 
 2. Open your project build.gradle file, in the application level gradle script, declare the following
```
repositories{  
     flatDir{  
	  dirs 'libs'  
    }  
}
```
 3. Compile the .aar, volley, gson, appcompay and design in the dependency block
 ```
dependencies {  
    implementation(name:'eghl-sdk-v2.5.X', ext:'aar')
    implementation 'com.android.volley:volley:1.1.1'
    implementation 'com.google.code.gson:gson:2.8.6'
    implementation 'androidx.appcompat:appcompat:1.2.0'
    implementation 'com.google.android.material:material:1.2.1'
}
```
 
 ## Implementation
 
 In this section we will discuss on two mainly used function, which is making payment and query payment status.
 
 We can leave the importing part to Android Studio to auto add it. But just incase conflict happen with other package classes, please note that eGHL package will   start with com.eghl.sdk
 
 ### Make Payment
 
 ```PaymentParams.Builder``` class will be use to create the parameters.
 
```
final String paymentID = eghl.generateId("DEMO");
final PaymentParams.Builder params = new PaymentParams.Builder()  
    .setMerchantReturnUrl("SDK") 
    .setServiceId("SIT") 
    .setPassword("sit12345")
    .setMerchantName("GHL ePayment Testing")
    .setAmount("1.00")
    .setPaymentDesc("eGHL Payment testing")
    .setCustName("Somebody")
    .setCustEmail("somebody@somesite.com")  
    .setCustPhone("60123456789")  
    .setPaymentId(paymentID)
    .setOrderNumber(paymentID)  
    .setCurrencyCode"MYR")
    .setLanguageCode("EN")
    .setPageTimeout("500")  
    .setTransactionType("SALE")      
    .setPaymentMethod("ANY")
    .setPaymentGateway("https://test2pay.ghl.com/IPGSG/Payment.aspx");
```
Build the parameters by calling the build() method on the ```PaymentParams.Builder``` object. It will generate a Bundle object with the payment parameters that you've set.

### Execute Payment
Execute the payment by calling the ```executePayment(Bundle params, Activity activity)``` on the ```EGHL``` instance.
The first parameter is the ```Bundle``` object from the previous step and the second parameter is the ```Activity``` that will handle the result of the payment.
```
Bundle paymentParams = params.build();  
    eghl.executePayment(paymentParams,MainActivity.this);
```

### Payment Results
Override the ```onActivityResult()``` inside the ```Activity``` that you’ve passed-in as the second parameter of the ```executePayment()``` from the previous step. After the payment is finished, the result will be returned to this method and the request code will be ```EGHL.REQUEST_PAYMENT```. You can handle the different responses from the server here. All the available constants for the result codes are at the Payment Result Codes section below.

```
@Override  
 protected void onActivityResult(int requestCode, int resultCode,
 Intent data) {  
 if(requestCode == EGHL.REQUEST_PAYMENT){  
         switch(resultCode){  
         case EGHL.TRANSACTION_SUCCESS:  
             Log.d(TAG, "onActivityResult: payment successful");  
             String status = data.getStringExtra(EGHL.TXN_STATUS);  
             String message = data.getStringExtra(EGHL.TXN_MESSAGE);  
             String raw = data.getStringExtra(EGHL.TXN_RAW_RESPONSE);
         break;  
         case EGHL.TRANSACTION_FAILED:  
             Log.d(TAG, "onActivityResult: payment failure");  
         break;  
         default:  
             Log.d(TAG, "onActivityResult: "+resultCode);  
         break;  
         }  
    }  

 }
```

* The following are the full list of payment result code (`resultCode`);

| Status Code | Constant Name                            | Description                                                                                                                                     |
|-------------|------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| 0           | EGHL.TRANSACTION_SUCCESS                 | Transaction successful (for transaction type SALE)                                                                                              |
| 1           | EGHL.TRANSACTION_FAILED                  | Transaction failed                                                                                                                              |
| 2           | EGHL.TRANSACTION_PENDING                 | Sale pending, retry Query                                                                                                                       |
| 10          | EGHL.TRANSACTION_REFUNDED                | Transaction refunded                                                                                                                            |
| 15          | EGHL.TRANSACTION_AUTHORIZED              | Transaction authorized (for transaction type AUTH)                                                                                              |
| 16          | EGHL.TRANSACTION_CAPTURED                | Transaction captured                                                                                                                            |
| 31          | EGHL.TRANSACTION_REVERSAL_PENDING        | Reversal pending, merchant system can retry Reversal if merchant system initiated the Reversal request or else merchant system can retry Query. |
| -1          | EGHL.TRANSACTION_NOT_EXISTING            | Transaction not exists/not found                                                                                                                |
| 9           | EGHL.TRANSACTION_REVERSED                | Transaction reversed                                                                                                                            |
| -2          | EGHL.TRANSACTION_INTERNAL_ERROR          | Internal system error                                                                                                                           |
| -999        | EGHL.TRANSACTION_CANCELLED               | Transaction cancelled by the user                                                                                                               |
| -888        | EGHL.TRANSACTION_NO_STATUS               | Can't determine the status, try to query again.|                                                                           
| -6767       | EGHL.TRANSACTION_ERROR_IN_WEBVIEW        | There's an error in the WebView loading the payment gateway.|
| -5454       | EGHL.TRANSACTION_NO_INTERNET_CONNECTION  | There's no internet connection.

* The following are additional info regarding the `Intent` object(`data`). The constants are the keys available in the extras:

| Constant Name      | Description                                                                                                    |
|--------------------|----------------------------------------------------------------------------------------------------------------|
| EGHL.TXN_STATUS    | Key constant that can be used in getting the transaction status in a Bundle object returned from the payment.  |
| EGHL.TXN_MESSAGE   | Key constant that can be used in getting the transaction message in a Bundle object returned from the payment. |
| EGHL.RAW_RESPONSE  | Key constant that can be used in getting the raw string response from the server.                              |

* The following are the params will be returned in EGHL.RAW_RESPONSE in JSON.

|     Parameters      | Description                               |
|---------------------|-------------------------------------------|
|TransactionType      |   Requested transaction type              |
|PymtMethod           |   Payment method                          |
|ServiceID            |   Service ID provided by eGHL             |
|PaymentID            |   Unique Value                            |
|OrderNumber          |   Unique Value                            |
|Amount               |   Transaction amount                      |
|CurrencyCode         |   Transaction currency                    |
|HashValue            |   Message digest value                    |
|HashValue2           |   Message digest value                    |
|TxnID                |   Transaction ID                          |
|IssuingBank          |   Issuing transaction bank                |
|TxnStatus            |   Transaction status                      |
|AuthCode             |   Authentication Code                     |
|BankRefNo            |   Bank Reference Number.                  |
|CardNoMask           |   Masked Card Number eg. 444433XXXXXX1111 |
|CardType             |   Credit Card Type                        |
|CardHolder           |   Card holder's name                      |
|TokenType            |   Token Type eg. OCP                      |
|Token                |   One Click Payment(OCP) purpose          |
|Param6               |   Extend value 1                          |
|Param7               |   Extend value 2                          |
|RespTime             |   Response time                           |
|TxnMessage           |   Transaction response message            |
|CardExp              |   YYYYMM                                  |


## Query Transaction Status

```QueryParams.Builder``` class will be use to create the parameters.

```
QueryParams.Builder builder = new QueryParams.Builder();  
    builder.setCurrencyCode("MYR");  
    builder.setPaymentMethod("ANY");  
    builder.setAmount("10.00");  
    builder.setPaymentId("CNASIT77918966729033");  
    builder.setServiceId("GHL");
```
Build the parameters by calling the ```build()``` method on the ```QueryParams.Builder``` object. It will generate a Bundle object with the query parameters that you've set.

### Execute Query
Execute the query by calling the ```executeQuery(Context context, Bundle params, QueryCallback callback)``` on the ```EGHL``` instance. Pass in the object that you've created from the previous step as the second parameter and a callback object as the third parameter.

```
eghl.executeQuery(MainActivity.this, queryParams,
    new QueryCallback() {  
            @Override  
            public void onResponse(QueryResponse response) {  

            }  

            @Override  
            public void onError(Exception e) {  

            }  
    });
```
The ```QueryResponse``` object in the onResponse() clause contains the result of the query.

### Adding credential to Android Manifest
If you prefer not to set the credential such as password in the payment request parameter, you can add it to android manifest.

The list of meta-data tag are depending on merchant request. Currently, the following meta-data are the tags that was requested previously:

* `com.epay.eghl.sdk.PASSWORD`
* `com.epay.eghl.sdk.PAYMENT_GATEWAY`

Add the desire meta-data tags inside the application tag in your manifest.

```
#!xml

 <manifest
    xmlns:android="http://schemas.android.com/apk/res/android"  
    package="com.eghl.demosdk">

    <uses-permission
    android:name="android.permission.INTERNET"/> 
        <application  
        android:allowBackup="true"  
        android:icon="@mipmap/ic_launcher"  
        android:label="@string/app_name"  
        android:supportsRtl="true"  
        android:theme="@style/AppTheme">
    
        <meta-data android:name="com.epay.eghl.sdk.PASSWORD"
        android:value="Replace with merchant password"/>  
        <meta-data android:name="com.epay.eghl.sdk.PAYMENT_GATEWAY"
        android:value="Replace with EGHL payment gateway"/>
    
        </application> 
      
    </manifest>

```

## Customize String Messages

You can customize SDK messages by overriding the library strings

```
 <string name="eghl_progress_message">Please wait..</string>
<string name="eghl_verification_message">Verifying Payment...</string>
<string name="eghl_cancel_dialog_title">Are you sure you want to quit</string>
<string name="eghl_cancel_dialog_message">Pressing EXIT button will close and abandon the payment session.</string>
<string name="eghl_prevent_back_toast_message">In progress...</string>
<string name="eghl_ssl_error_dialog_title">Are you sure you want to continue</string>
<string name="eghl_ssl_error_dialog_message">Error in SSL certificate</string>
<string name="eghl_masterpass_prevent_exit">Masterpass payment is ongoing...</string>
```

| String name                          | Description                                                                                     |
|--------------------------------------|-------------------------------------------------------------------------------------------------|
| eghl_verification_message            | The progress message when the SDK is verifying the transaction                                  |
| eghl_cancel_dialog_title             | The title of the exit dialog of the payment                                                     |
| eghl_cancel_dialog_message           | The message of the exit dialog of the payment                                                   |
| eghl_prevent_back_toast_message      | The Toast message when the user attempts to exit while verifying                                |
| eghl_ssl_error_dialog_title          | The title of the SSL error dialog                                                               |
| eghl_ssl_error_dialog_message        | The message of the SSL error dialog                                                             |
| eghl_progress_message                | The progress message while the SDK is loading the payment gateway or Masterpass lightbox        |
|eghl_masterpass_prevent_exit          | The toast message when user tries to exit in masterpass express when gateway is not yet loaded  |
|eghl_no_internet_connection           | The toast message when the user attempts to make a payment with no internet connection          |

#**Helper**
* ELogger - setting `ELogger.setLoggable()` to `true` will enabled debug logs.
* Demo app - provided in this repo for your reference. 


