# HelloTodo application for IBM MobileFirst Services on IBM Bluemix
---
The HelloTodo sample contains an Objective-C project to be used to communicate with a StrongLoop based backend created as when using the MobileFirst Services Boilerplate on Bluemix. 

### Creating a mobile backend
Start by creating a mobile backend on IBM Bluemix by using the MobileFirst Services Boilerplate

1. Log in into your IBM Bluemix account
2. Open Bluemix Catalog [https://console.ng.bluemix.net/catalog/](https://console.ng.bluemix.net/catalog/)
3. Find and select the MobileFirst Services Starter under the Boilerplates section
4. Select the space you want to add your mobile backend to
5. Enter the name and host for your mobile backend. 
6. Optionally you can change the plans
7. Click CREATE button

As a result of the above steps IBM Bluemix will provision a Node.JS runtime and populate it with with a default HelloTodo application written using StrongLoop. The application uses LoopBack framework to expose an /Items API which will be used by both Web UI and the mobile app sample stored in this Github repository. 

Once provisioning process is complete you'll be taken to the Bluemix Dashboard for your newly provisioned mobile backend. Client the Mobile Options link in top right part of a screen to find your appRoute and appGUID. You will use them shortly. 

Open the appRoute URL in your browser. You will see the web interface for the HelloTodo backend. Start by following the guided experience of the web UI. Eventually you'll try to DELETE a todo item and will find out that this an action can only be performed by using mobile app sample stored in this Github repository. This is due to a fact that the mobile backend is by default protected by a Mobile Client Access service. Below steps will guide you through obtaining and running the sample. 

Optionally you might want to hit the "View API Reference" button on web UI to see the API specs. 

### Cloning the sample
Clone the sample to your local development environment

	git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellotodo

### Installing Cocoapods

The easiest way of getting a Bluemix Mobile Services SDK is to install it using Cocoapods, a dependency manager for iOS projects. Start by making sure that you have Cocoapods installed

1. Open Terminal
2. Run the `pod --version` command. You can skip this section if you see the installed Cocoapods version, continue otherwise. 
3. Install Cocoapods by running `sudo gem install cocoapods`. Refer to Cocoapods website in case additional guidance is required [https://cocoapods.org/](https://cocoapods.org/)

### Installing Bluemix Mobile Services SDK using Cocoapods

Now that you have Cocoapods installed on you system you can use it to add the required dependencies to the previously cloned sample project. 

1. Open Terminal
2. Navigate to the bms-samples-ios-hellotodo/helloTodo directory where the project was cloned
5. Run the `pod install` command to download and install dependecies. This might take several minutes
6. Open the Xcode workspace by running this commend - `open helloTodo.xcworkspace`. Always open .xcworkspace file when working with Cocoapods enabled projects since since it contains all the dependencies and configuration
7. Open the `AppDelegate.m` file, find the `application:didFinishLaunchingWithOptions` method and add the appRoute and appGUID you previously got from your Bluemix application dashboard to the SDK initialization API

```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	IMFClient *imfClient = [IMFClient sharedInstance];
	[imfClient initializeWithBackendRoute:@"<APPLICATION_ROUTE>" 
							  backendGUID:@"<APPLICATION_ID>"];
	return YES;
}
```
You can now hit `CMD+R` to run your application. 

### Using the HelloTodo sample application

The HelloTodo sample a single view application with a simple list of todo items. If you previously added data through your web application you will see the data automatically pulled into the application. You can create, add and modify items directly in the application. Note that unlike the web UI you can also DELETE items since you're using the Bluemix Mobile Services SDK which knows how to handle Mobile Client Access security. You can also mark items as compelted by clicking to the left of the corresponding todo item. When you update an item in the mobile app it will automatically be updated in the web app (you will need to refresh the web UI). If you make a change in the web UI and want to see it reflected in the mobile app, simply pull down the todo list to refresh.

As you recall the DELETE endpoint can only be accessed by mobile applications since it is protected by a Mobile Client Access service. That said, currently Mobile Client Access is not configured to require any authentication. Next step is learning how to use Bluemix Mobile Services would be to configure authentication using the Mobile Client Access dashboard and instrument your app with required components. You can see full tutorial explaining how to do that in this blog [link](http://)



Note: This HelloTodo iOS sample requires XCode 7.1 to run. Also, the project has bitcode support disabled since currently the Bluemix Mobile Services SDK does not support it. You can read more about this in this blog [Connect Your iOS 9 App to Bluemix](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)

### License
This package contains sample code provided in source code form. The samples are licensed under the under the Apache License, Version 2.0 (the "License"). You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0 and may also view the license in the license.txt file within this package. Also see the notices.txt file within this package for additional notices.
