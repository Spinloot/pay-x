# rn-upi

Unlock the power of UPI payments within your React Native applications with the revolutionary react-native-upi plugin. Crafted to seamlessly integrate the cutting-edge UPI payment interface developed by NPCI, this compact yet robust plugin empowers you to effortlessly enable peer-to-peer payments through UPI in your React Native apps. Say goodbye to payment hurdles and embrace the future of secure, swift transactions."

## Installation
```bash
npm install rn-upi
```

or 
```bash
yarn add rn-upi
```

### Android
#### Automatic Installation
```
react-native run link
```

#### Manual Installation
Open `android/settings.gradle` add the following
```
include ':react-native-upi-payment'
project(':react-native-upi-payment').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-upi-payment/android')

```

Open `android/build.gradle` add the following in the dependencies section
```
dependencies {
    compile project(':react-native-upi-payment')
}
```

Open `MainApplication.java`
```java
// Other imports
import com.upi.payment.UpiPaymentPackage;

  // Add this in the Main Application Class
  @Override
  protected List<ReactPackage> getPackages() {
    return Arrays.<ReactPackage>asList(
       //... Other packages
          new UpiPaymentPackage() // <- Add this line
    );
  }
```




## Usage

```javascript
RNUpiPayment.initializePayment({
  vpa: 'john@upi', // or can be john@ybl or mobileNo@upi
  payeeName: 'John Doe',
  amount: '1',
  transactionRef: 'aasf-332-aoei-fn'
}, successCallback, failureCallback);

```

## Config docs
```javascript
{
  /*
  * REQUIRED
  * vpa is the address of the payee given to you
  * by your bank
  */
  vpa: 'somehandle@upi',

  /*
  * REQUIRED
  * payeeName is the name of the payee you want
  * to make a payment too. Some upi apps need this
  * hence it is a required field
  */
  payeeName: 'Payee name',

  /*
  * REQUIRED
  * This is a reference created by you / your server
  * which can help you identify this transaction
  * The UPI spec doesnt mandate this but its a good to have
  */
  transactionRef: 'some-hash-string',

  /*
  * REQUIRED
  * The actual amount to be transferred
  */
  amount: '200',

  /*
  * OPTIONAL
  * Transactional message to be shown in upi apps
  */
  transactionNote: 'for food'
}
```

## Callbacks 
```javascript
function successCallback(data) {
  // do whatever with the data
}

function failureCallback(data) {
  // do whatever with the data
}

```

## Responses

SUCCESS CASE
```javascript
{
/**
* SUCCESS STATUS
* */
Status: "SUCCESS",
/**
* Transaction Id of bank to which upi has been initiated
* */
txnId: "AXId8c71205eb7d459889bb7018bdf2c056", 
/**
* 00 response code, for success
* transaction is successful money has been debited
* */
responseCode: "00",
/**
* Transaction reference stated in init obect
* */
txnRef: "aasf-332-aoeifn"

}
```
FAILURE CASES
```javascript
{
  /**
   * Status Sent on transaction
   * If the user presses back or closes app
   * */
  status: "FAILURE",

  /**
  * If the user presses back or closes app
  * */
  message: "No action taken"
} // No action
```
```javascript
{
  /**
  * FAILURE STATUS
  * */
  Status: "FAILURE",
  /**
  * Transaction Id of bank to which upi has been initiated
  * */
  txnId: "AXIa463c7ca81a24e168df5ac9c1359c38c", 
  /**
  * Non 0 response code,
  * If the user enters the wrong pin
  * */
  responseCode: "ZM",
  /**
  * Transaction reference stated in init obect
  * */
  txnRef: "aasf-332-aoeifn"
  
  }
```



