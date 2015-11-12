# HelloTodo application for IBM MobileFirst Services on IBM Bluemix
---
The HelloTodo sample contains an Objective-C project that you can use to learn the Data component and StrongLoop integration.  
### Downloading the samples
Clone the samples from IBM DevOps Services with the following command:

git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellotodo

### Configure the back end for your Bluelist application
Before you can run the helloTodo application, you must set up an app on Bluemix.  For simplicity, the steps below outline how to create a MobileFirst Services Starter application which includes the following: Node.js runtime, IBM Push Notifications, Mobile Client Access, and Cloudant services.

1. Sign up for a [Bluemix](http://bluemix.net) Account.
2. Create a mobile app.  In the Boilerplates section Bluemix catalog, click **MobileFirst Services Starter**.  Choose a **Name** and click **Create**.
3. Get Familiar with StrongLoop Web App: The Bluemix Mobile Services Boilerplate has provided a web app built with StrongLoop that lets you build and modify data directly through the browser.

-Check out the web interface by going to your application in a browser: 
    Example: http://<APP_Name>.mybluemix.net

-Rest APIs have already been provided that can be viewed and used through a browser:
    Example: http://<App_Name>.mybluemix.net/explorer/#!/Item

### Configure the front end in the helloTodo sample
1. In a terminal, navigate to the bms-samples-ios-hellotodo directory where the project was cloned
2. Navigate to the helloTodo directory 
3. Install Cocoapod client if not already installed `sudo gem install cocoapods`
4. Configure the Cocoapod repository if not already configured `pod setup`
5. Run the `pod install` command to download and install dependecies.
6. Open the Xcode workspace: `open helloTodo.xcworkspace`. From now on, open the xcworkspace file since it contains all the dependencies and configuration.
7. Open the AppDelegate.m and add the corresponding ApplicationRoute and
ApplicationID in the application's' didFinishLaunchingWithOptions method:


Objective C:

(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

//initialize SDK with IBM Bluemix application ID and route
//TODO: Please Enter a valid ApplicationRoute for initializaWithBacken Route and a valid ApplicationId for backenGUID
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<APPLICATION_ROUTE>" backendGUID:@"<APPLICATION_ID>"];			

return YES;
}



### Run the iOS App

When you run the application you will see a single view application with a list of todo items. If you previously added data through your web application you will see the data automatically pulled into the application. You can create, add, modify and delete todo items directly in the application. You can also mark items as compelted by clicking to the left of the corresponding todo item. 

Note: This application has been built to run on the latest version of XCode (7.0). The application has been updated to set Enable Bitcode to No in the build-settings as a workaround for the these settings introduced in iOS 9. For more info please see the following blog:

[Connect Your iOS 9 App to Bluemix](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)

### License
This package contains sample code provided in source code form. The samples are licensed under the under the Apache License, Version 2.0 (the "License"). You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0 and may also view the license in the license.txt file within this package. Also see the notices.txt file within this package for additional notices.
