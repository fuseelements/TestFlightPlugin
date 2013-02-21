TestFlight Plugin for Apache Cordova
=====================================
created by Shazron Abdullah

[Apache 2.0 License](http://www.apache.org/licenses/LICENSE-2.0.html) except for the TestFlight1.1 SDK that is under **src/ios/TestFlight1.1**

Follows the [Cordova Plugin spec](https://github.com/alunny/cordova-plugin-spec), so that it works with [Plugman](https://github.com/imhotep/plugman), or you can install it manually below.
 
1. Add the TestFlight SDK 1.1 files **(libTestFlight.a, and TestFlight.h)** in Xcode (add as a group)
2. Add the plugin files **(CDVTestFlight.h, CDVTestFlight.m)** in Xcode (add as a group)
3. Add **testflight.js** to your **www** folder, and reference it in a script tag, after your cordova.js
4. In __Cordova.plist__, under the **'Plugins'** key, add a new row: key is **"TestFlightSDK"** and the value is **"CDVTestFlight"**
5. In __Cordova.plist__, under the **'ExternalHosts'** key, add a new value **"*.testflightapp.com"**
6. Add the lib **"libz.dylib"** in your Build Phases tab of your Project
    
The plugin's JavaScript functions are called after getting the plugin object thus:
 
        var tf = cordova.require("cordova/plugin/testflightsdk");
        tf.takeOff(win, fail, "some_team_token");
 
See the functions below (and the TestFlight SDK docs) for usage. Unfortunately all of TestFlight's SDK functions return void,
and errors can only be gleaned from the run console, so check that for errors.

        // Get a reference to the plugin first
        var tf = cordova.require("cordova/plugin/testflightsdk");

        /*
         Add custom environment information
         If you want to track a user name from your application you can add it here
     
         @param successCallback function
         @param failureCallback function
         @param key string
         @param information string
         */
        tf.addCustomEnvironmentInformation(successCallback, failureCallback, 'key', 'information');

        /*
         Starts a TestFlight session
     
         @param successCallback function
         @param failureCallback function
         @param teamToken string
         */
        tf.takeOff(successCallback, failureCallback, 'teamToken');
    
        /*
         Sets custom options
     
         @param successCallback function
         @param failureCallback function
         @param options object i.e { reinstallCrashHandlers : true }
         */
        tf.setOptions(successCallback, failureCallback, options);
    
        /*
         Track when a user has passed a checkpoint after the flight has taken off. Eg. passed level 1, posted high score
     
         @param successCallback function
         @param failureCallback function
         @param checkpointName string
         */
        tf.passCheckpoint(successCallback, failureCallback, 'checkpointName');
    
        /*
         Opens a feeback window that is not attached to a checkpoint
     
         @param successCallback function
         @param failureCallback function
         */
        tf.openFeedbackView(successCallback, failureCallback);

        /*
          Submits custom feedback to the site. Sends the data in feedback to the site. 
          This is to be used as the method to submit feedback from custom feedback forms.
         
          @param feedback Your users feedback, method does nothing if feedback is nil
        */
        tf.submitFeedback(successCallback, failureCallback, 'feedback');
        
        /*
         Sets the Device Identifier. 
         The SDK no longer obtains the device unique identifier. This method should only be
         used during testing so that you can identify a testers test data with them. 
         If you do not provide the identifier you will still see all session data, with
         checkpoints and logs, but the data will be anonymized.
         
          @param deviceIdentifer The current devices device identifier
        */
        tf.setDeviceIdentifier(successCallback, failureCallback, 'deviceIdentifier');
