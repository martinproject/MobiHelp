##Freshdesk MobiHelp SDK for iOS apps
===================================

The Freshdesk MobiHelp SDK lets you bring your knowledge base and customer support right into your iOS apps. 
Once set, users can learn the basics of your app, ask questions and give you feedback right from inside your application.

This document will guide you through setting up Freshdesk MobiHelp inside your mobile apps.
__________________________________________________________________________________________________________________________

###Step 1. Getting the MobiHelp SDK

You will need the Freshdesk MobiHelp SDK to get started. Download the Latest SDK from https://github.com/freshdesk/MobiHelp/tags the zip file will contains FreshdeskSDK-iosuniversal compiled for (i386,armv7,armv7s) and FreshdeskSDK-iosdevice compiled for (armv7, armv7s), we have done this mainly not increase your app size. Choose which ever fits your need and both the folder contains:

+ FreshdeskSDK.framework - Contains the interfaces for setting up MobiHelp inside your app
+ FreshdeskSDKResources.bundle - Contains images and resources required for the MobiHelp library

Unless you are an iOS ninja, you probably don't want to mess with these folders too much.

You will also need a Freshdesk account. If you haven't already, get a free Freshdesk account AND [download the SDK](https://github.com/freshdesk/MobiHelp/).
__________________________________________________________________________________________________________________________

###Step 2. Adding MobiHelp to your iOS project

Once you've downloaded the zip file, unzip it and drag-drop it right into the Frameworks section of the Project Navigator in your XCode project. 

Though MobiHelp is pretty slick by itself, the SDK needs a few buddy frameworks to make sure everything works great.
Make sure you add the QuartzCore, SystemConfiguration, and Foundation frameworks in "Link Binary with Libraries".
Also make sure FreshdeskSDKResources.bundle is in "Copy Bundle Resources". 

Great! MobiHelp is geared to win you some love from your users already!

Integrating MobiHelp SDK with Cocoapods

Mobihelp can also be included in the project by using Cocoapods 

Cocoapods is a dependency manager for iOS. It fetches source code and resolves dependency issues between 3rd party libraries. In order to use cocoa pods , you first need to install the gem by typing the command- 

     gem install cocoapods

To add MobiHelp to your xcode project 

  1) Create a file named "podfile" in the project root.
  2) Add the following lines in podfile

    platform:ios
      
    pod 'FreshdeskSDK'

and type the following command from the console.

    pod install 

As a result of the above command  a workspace is now generated. In the workspace all the dependencies are stored in a file called Pods. You will notice that all library and framework dependancies for the FreshdeskSDK have now been added to your project. 

You can proceed to Step 3. Linking your app with your Freshdesk account 
and complete the MobiHelp integration with your application.
__________________________________________________________________________________________________________________________

###Step 3. Linking your app with your Freshdesk account

To bring your "how-to"s and knowledge base articles into your iOS app, you will need to link MobiHelp with your Freshdesk account. Here's what you need:

+ Freshdesk Domain: This is the URL of the Freshdesk account you just created (like "yourcompany.freshdesk.com"). And unless you were born in the 17th century nobody starts a domain with "http" anymore, so remember to NOT INCLUDE the "http://" part.
+ API Key: The API key lets your mobile app "talk" to your Freshdesk support portal. To get your API key, login to your Freshdesk account as the administrator (the guy who created the account). Click on your name, on the top right corner of the screen, and go to profile settings. You can find the API Key on the right. Copy the code - you'll need it soon!

This is the part where you get into your hardcore hacking gear and dive into the code. Open your app delegate file. You'll first need to import the FreshdeskSDK.h header file.  

    #import <FreshdeskSDK/FreshdeskSDK.h>

Now add these lines inside application:didFinishLaunchingWithOptions: 

    [FDSupport setUpWithSite: @"<mycompany.freshdesk.com>" andApikey: @"<B0yW4sTh4t3asy>"];


Remember to replace <mycompany.freshdesk.com> with your Freshdesk domain, and <B0yW4sTh4t3asy> with your API key. 
__________________________________________________________________________________________________________________________

###Step 4. Showing the in-app User Support Portal

Of course, the reason you did this whole thing is to bring your knowledge base, and let users talk to you right from your app. That means you need to pass the name of the viewcontroller on which the support screen will show up. 

You can add a support link or feedback button right inside your application. From inside a viewcontroller you can then call Freshdesk by passsing the argument “self”.

    [[FDSupport sharedInstance] presentSupport:self];

This will show your customer all the glories of your knowledge base and the status of all previous feedback they have given you. Instead if you'd like to get a little bit more "plain vanilla", you can just show the option to give feedback to users, without worrying them with FAQs and feedback histories. If that's what makes you happy, you'd have to call "presentFeedback" in your viewcontroller instead of "presentSupport".
    
    [[FDSupport sharedInstance] presentFeedback:self];

__________________________________________________________________________________________________________________________

###Step 5. Customizing the support portal

You can customize the navigation bar color of the knowledge base and feedback area to match your app theme. 

    [FDSupport setUpColor:[NSDictionary dictionaryWithObjectsAndKeys:[UIColor colorWithRed:.9 green:.4 blue:.7 alpha:2], FD_NAVBAR_COLOR], nil];

The NavBar Color that you set here will be maintained in the knowledge base section within your app, and in the detailed view when your users click on a specific solution as well.
__________________________________________________________________________________________________________________________

###Step 6. Advanced Configurations

With the basic configuration, your users can pass their feedback to you directly. However, you can uniquely identify each user only based on their Device and App IDs. Instead, if you already have additional information about a user, you can pre-define them so your users don't have to enter them again.   

    [FDSupport setUseremail:@"leo@tnmt.com"];
  
    [FDSupport setUsername:@"leonardo tutle"];   

    [FDSupport setUserUID:@"UUID-0203-938EW"];   


For example, if you already enforce a login in your application, you can pass the user ID or unique identifier along with the feedback.
__________________________________________________________________________________________________________________________

