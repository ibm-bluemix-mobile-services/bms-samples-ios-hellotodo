# iOS helloTodo Sample Application for Bluemix Mobile Services
---
This helloTodo sample contains an Objective-C project to be used to communicate with a StrongLoop based mobile backend created using MobileFirst Services Boilerplate on IBM Bluemix. You can either watch the video tutorial or follow the below instructions that take you step by step through a process of creating a mobile backend and getting this sample running.

![image](video-coming-soon.png)
> We're working on creating a video tutorial. It will be published here once ready

Use the following steps to configure the helloTodo sample for Objective-C:

1. [Downloading the helloTodo sample](#downloading-the-hellotodo-sample)
2. [Configuring the mobile backend for your helloTodo application](#configuring-the-mobile-backend-for-your-hellotodo-application)
3. [Configuring the front end in the helloTodo sample](#configuring-the-front-end-in-the-hellotodo-sample)
4. [Running the helloTodo sample application](#running-the-hellotodo-sample-application)

### Before you begin
Before you start, make sure you have the following:

- A [Bluemix](http://bluemix.net) account.

### Downloading the helloTodo sample
Clone the sample from Github with the following command:

```git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellotodo```

### Configuring the mobile backend for your helloTodo application
> If you have already followed steps described in other tutorials and created a mobile backend using MobileFirst Services Boilerplate you might want to skip to the [Configuring the front end in the helloTodo sample](#configuring-the-front-end-in-the-hellotodo-sample) section.

Before you can run the helloTodo application, you must set up an app on Bluemix.  The following procedure shows you how to create a MobileFirst Services Starter application. This will provision a Node.JS runtime and populate it with with a default helloTodo application created using StrongLoop. This application uses LoopBack framework to expose the `/api/Items` API which will be used by both Web UI and the helloTodo app sample from this Github repository. . The Cloudant®NoSQL DB, IBM Push Notifications, and Mobile Client Access services are also added to the app.

Create a mobile backend in the  Bluemix dashboard:

1.	In the Boilerplates section of the Bluemix catalog, click MobileFirst Services Starter.
2.	Enter a name and host for your mobile backend and click Create.
3.	Click **Finish**.

Once the above provisioning process is complete you'll be taken to a Bluemix Dashboard for your newly provisioned mobile backend. Click the **Mobile Options** link in top right part of a screen to find your **appRoute* and *appGUID*. Keep this screen open in your browser as you you will need these parameters shortly. 

Open the appRoute URL in your browser. You will see the web interface for the helloTodo backend. Start by following the guided experience steps described in the web UI. Eventually you will try to DELETE a todo item and will discover that this action can only be complete when using the helloTodo mobile apps sample from this Github repository. This is due to a fact that the mobile backend is by default protected by a Mobile Client Access - a Bluemix service that provides security and monitoring functionality for mobile backends. Following steps will guide you through obtaining and running the helloTodo mobile application. 

(Optionally you might want to hit the "View API Reference" button on web UI to see the API specs)

### Configuring the front end in the helloTodo sample
1. In a terminal, navigate to the `bms-samples-ios-hellotodo` directory where the project was cloned
2. Navigate to the helloTodo folder
3. If the CocoaPods client is not installed, install it using the following command: `sudo gem install cocoapods`
4. If the CocoaPods repository is not configured, configure it using the following command: `pod setup`
5. Run the `pod install` command to download and install the required dependencies.
6. Open the Xcode workspace: `open helloPush.xcworkspace`. From now on, open the xcworkspace file since it contains all the dependencies and configuration.
7. Open the **AppDelegate.m** and add the corresponding **ApplicationRoute** and
**ApplicationID** (found in the `Mobile Options` link on the Bluemix Dashboard) in the application **didFinishLaunchingWithOptions** method:


Objective C:
```objective-c
(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

//initialize SDK with IBM Bluemix application ID and route
//TODO: Enter a valid ApplicationRoute for initializaWithBacken Route and a valid ApplicationId for backenGUID
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<APPLICATION_ROUTE>" backendGUID:@"<APPLICATION_ID>"];			

return YES;
}
```


### Running the helloTodo sample application

The helloTodo sample a single view application with a simple list of todo items. If you previously added data through your web application you will see the data automatically pulled into the application. You can create, add and modify items directly in the application. Note that the helloTodo sample applications uses Bluemix Mobile Services SDK which knows how to handle Mobile Client Access security. Therefore, unlike the web UI, you can also DELETE items from mobile app by swiping them. You can also mark items as completed by clicking to the left of the corresponding todo item. When you update an item in the mobile app it will automatically be updated in the web app (you will need to refresh the web UI). If you make a change in the web UI and want to see it reflected in the mobile app, simply pull down the todo list to refresh.

As you recall the DELETE endpoint can only be accessed by mobile applications since it is protected by a Mobile Client Access service. That said, by default Mobile Client Access is not configured to require any interactive authentication (e.g. ask for username and password). Next step is learning how to configure authentication using the Mobile Client Access dashboard and instrument your app with required components. You can either check [Mobile Client Documentation](https://www.ng.bluemix.net/docs/services/mobileaccess/index.html) for that or watch the below video showing the process in details. 

![image](video-coming-soon.png)
> We're working on creating a video tutorial. It will be published here once ready


**Note:** This helloTodo iOS sample requires XCode 7.1 to run. Also, the project has bitcode support disabled since currently the Bluemix Mobile Services SDK does not support it. You can read more about this in this blog entry: [Connect Your iOS 9 App to Bluemix](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)

### License
This package contains sample code provided in source code form. The samples are licensed under the under the Apache License, Version 2.0 (the "License"). You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0 and may also view the license in the license.txt file within this package. Also see the notices.txt file within this package for additional notices.
