# Find Your Friends using Digits and AWS

This is a sample demonstrating [Digits](http://digits.com) "Find Your Friends" [feature] (https://docs.fabric.io/ios/digits/find-friends.html) with Amazon [Cognito] (https://aws.amazon.com/cognito/) and [DynamoDB] (https://aws.amazon.com/dynamodb/) as the backend. Digits is available via [Fabric] (https://fabric.io).

### Setup Digits

1. Sign up for [Fabric](https://fabric.io).
2. Download, install, and run the [Fabric Mac app] (https://fabric.io/downloads/xcode).
3. In Fabric.app, click "+ New App" and open `DigitsFYF.xcworkspace`.
  * Install the Digits kit via a Podfile. When prompted, ignore the suggested pod snippets as they are already includes.
4. In Xcode, open `DigitsFYF.xcworkspace`.
  * Add the Run Script Build Phase from Fabric.app to the DigitsFYF target.
  * Clean and Build the project.
5. In Fabric.app, when prompted, ignore the suggested Swift snippets as they are already included.
6. In Xcode, Clean and Run the project.  

### Setup Cognito

1. Log into the [Cognito console] (https://console.aws.amazon.com/cognito).
2. Create a new Identity Pool named `DigitsSample` and set the Twitter (Digits) API credentials. You can find the Consumer Key and Consumer Secret by opening `Info.plist` and drilling down the item named `Fabric`.
   
   <img src="/screenshots/cognito.png" width="600">
   <img src="/screenshots/plist.png" width="600">
3. Allow AWS to create new IAM roles for the identity pool. 
4. Set the identity pool id as the value of `CognitoIdentityPoolId` in `Constants.swift`. 
5. Log into the [IAM console] (https://console.aws.amazon.com/iam).
6. In the "Roles" tab, select `Cognito_DigitsSampleAuth_Role` and attach the policy named `AmazonDynamoDBFullAccess`.
   
   <img src="/screenshots/iam.png" width="600">

### Setup DynamoDB

1. Log into the [DynamoDB console] (https://console.aws.amazon.com/dynamodb).
2. Create a new table `users`.
3. Add a Primary Key hash named `cognitoId` (Type String).
4. Add Global Secondary indices named `digitsId` (Type String) and `phoneNumber` (Type String).

## Project

1. Run the app on the iPhone 5 simulator. 
  * Use your phone number to login and accept the prompt to upload the simulator's contacts to Digits. 
2. Run the app on the iPhone 6 simulator.
  * Minimize the app (Hardware > Home), open the Contacts app and add a contact named "Larry" with the number you've used in Step 1. 
  * Use another phone number to login and accept the prompt to upload the simulator's contacts to Digits. You can create a second phone number using [Google Voice] (https://www.google.com/voice). 
3. Run the app on the iPhone 5 simulator again. 

## Compatibility

This project was written in Swift 2 using Xcode 7. 

## License

Copyright 2015 Twitter, Inc.

Licensed under the Apache License, Version 2.0: http://www.apache.org/licenses/LICENSE-2.0
