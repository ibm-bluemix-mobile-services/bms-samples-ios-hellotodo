# iOS HelloTodo sample for IBM MobileFirst Services on IBM Bluemix
---
This HelloTodo sample contains an Objective-C project to be used to communicate with a StrongLoop based mobile backend created using MobileFirst Services Boilerplate on IBM Bluemix. You can either watch the video tutorial or follow the below instructions that take you step by step through a process of creating a mobile backend and getting this sample running.

![image](video-coming-soon.png)
> We're working on creating a video tutorial. It will be published here once ready

### Creating a mobile backend

> If you have already followed steps described in other tutorials and created a mobile backend using MobileFirst Services Boilerplate you might want to skip to `Cloning the sample` section

Start by creating a mobile backend on IBM Bluemix by using the MobileFirst Services Boilerplate

1. Log in into your IBM Bluemix account
2. Open Bluemix Catalog [https://console.ng.bluemix.net/catalog/](https://console.ng.bluemix.net/catalog/)
3. Find and select the MobileFirst Services Starter under the Boilerplates section
4. Select the space you want to add your mobile backend to
5. Enter the name and host for your mobile backend. 
6. Optionally you can change the plans
7. Click CREATE button

As a result of the above steps IBM Bluemix will provision a Node.JS runtime and populate it with with a default HelloTodo application created using StrongLoop. This application uses LoopBack framework to expose the `/api/Items` API which will be used by both Web UI and the HelloTodo app sample from this Github repository. 

Once the above provisioning process is complete you'll be taken to a Bluemix Dashboard for your newly provisioned mobile backend. Click the `Mobile Options` link in top right part of a screen to find your `appRoute` and `appGUID`. Keep this screen open in your browser as you you will need these parameters shortly. 

Open the appRoute URL in your browser. You will see the web interface for the HelloTodo backend. Start by following the guided experience steps described in the web UI. Eventually you will try to DELETE a todo item and will discover that this action can only be complete when using the HelloTodo mobile apps sample from this Github repository. This is due to a fact that the mobile backend is by default protected by a Mobile Client Access - a Bluemix service that provides security and monitoring functionality for mobile backends. Following steps will guide you through obtaining and running the HelloTodo mobile application. 

(Optionally you might want to hit the "View API Reference" button on web UI to see the API specs)

### Cloning the sample
Clone the sample to your local development environment

```Shell
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellotodo
```

### Installing Cocoapods

The easiest way of getting a Bluemix Mobile Services SDK is to install it using Cocoapods, a dependency manager for iOS projects. Start by making sure that you have Cocoapods installed

1. Open Terminal
2. Run the `pod --version` command. If you see the installed Cocoapods version you can skip step 3 and continue to the next section of this tutorial
3. Install Cocoapods by running `sudo gem install cocoapods`. Refer to Cocoapods website in case additional guidance is required [https://cocoapods.org/](https://cocoapods.org/)

### Installing Bluemix Mobile Services SDK using Cocoapods

Now that you have Cocoapods installed on you Mac you can use it to automatically add the required dependencies to the previously cloned sample project. 

1. Open Terminal
2. Navigate to the `bms-samples-ios-hellotodo/helloTodo` directory where the project was cloned
5. Run the `pod install` command to download and install dependecies. This might take several minutes
6. Open the Xcode workspace by running `open helloTodo.xcworkspace` command. Remember to always open .xcworkspace file when working with Cocoapods enabled projects since since it contains all the dependencies and configuration.
7. Open the `AppDelegate.m` file and find the `application:didFinishLaunchingWithOptions` method. 
8. Add `appRoute` and `appGUID` parameters you previously got from your Bluemix application dashboard to the SDK initialization API instead of placeholders

```Objective-C
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	IMFClient *imfClient = [IMFClient sharedInstance];
	[imfClient initializeWithBackendRoute:@"<APPLICATION_ROUTE>" 
							  backendGUID:@"<APPLICATION_ID>"];
	return YES;
}
```

You can now hit `CMD+R` to run your application. 

### Using the HelloTodo sample application

The HelloTodo sample a single view application with a simple list of todo items. If you previously added data through your web application you will see the data automatically pulled into the application. You can create, add and modify items directly in the application. Note that the HelloTodo sample applications uses Bluemix Mobile Services SDK which knows how to handle Mobile Client Access security. Therefore, unlike the web UI, you can also DELETE items from mobile app by swiping them. You can also mark items as completed by clicking to the left of the corresponding todo item. When you update an item in the mobile app it will automatically be updated in the web app (you will need to refresh the web UI). If you make a change in the web UI and want to see it reflected in the mobile app, simply pull down the todo list to refresh.

As you recall the DELETE endpoint can only be accessed by mobile applications since it is protected by a Mobile Client Access service. That said, by default Mobile Client Access is not configured to require any interactive authentication (e.g. ask for username and password). Next step is learning how to configure authentication using the Mobile Client Access dashboard and instrument your app with required components. You can either check [Mobile Client Documentation](https://www.ng.bluemix.net/docs/services/mobileaccess/index.html) for that or watch the below video showing the process in details. 

![image](video-coming-soon.png)
> We're working on creating a video tutorial. It will be published here once ready

.

> Note: This HelloTodo iOS sample requires XCode 7.1 to run. Also, the project has bitcode support disabled since currently the Bluemix Mobile Services SDK does not support it. You can read more about this in this blog [Connect Your iOS 9 App to Bluemix](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)

### License
This package contains sample code provided in source code form. The samples are licensed under the under the Apache License, Version 2.0 (the "License"). You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0 and may also view the license in the license.txt file within this package. Also see the notices.txt file within this package for additional notices.
