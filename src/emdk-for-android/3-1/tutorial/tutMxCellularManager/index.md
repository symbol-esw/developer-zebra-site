---
title: Set the Roaming State using Cellular Manager
layout: guide.html
product: EMDK For Android
productversion: '2.3'
---

## Overview

This guide will walk you through creating an EMDK For Android application that will use some new Mx features introduced in EMDK for Android API to perform device configurations. Mx represents a suite of Enterprise Features on top of standard, commercially available Android Open Source Project. So this tutorial will focus on configuring roaming state of your Symbol Android device (Ex. Turn ON/OFF state of Data Roaming) using [Cellular Manager](../../mx/cellularmgr) feature of Mx. 

So now we will create a tutorial to turn the state of Data Roaming ON using Mx [Cellular Manager](../../mx/cellularmgr) feature on your Symbol Android device. 
        
###Prerequisites

* Java Development Kit (JDK)
* Android Developer Tools (ADT) ([Android Studio](http://developer.android.com/sdk/index.html)/[Eclipse with ADT](http://developer.android.com/tools/sdk/eclipse-adt.html)) 
* EMDK for Android V 3.0 and above 

For more information about setting up the EMDK please see the EMDK Overview.

## Creating The Project

> Note: Provide "CellularManagerTutorial" as the project name for this tutorial.

If you are using Android Studio, click [here](../tutCreateProjectAndroidStudio).

If you are using Eclipse with ADT, click [here](../tutCreateProjectEclipseADT).  

## Enabling the EMDK
If you are using Android Studio, you have already completed this step while creating the project by selecting `EMDK 3.1 (API 16) (Symbol Technologies, Inc.) (API 16)` or `EMDK 3.1 (API 19) (Symbol Technologies, Inc.) (API 19)` as the minimum SDK.

If you are using Eclipse with ADT, click [here](../tutEnableEMDKEclipseADT) for Enabling the EMDK tutorial as it would again be a common step for all of your projects that are using EMDK for Android API.  

 
## Adding The Cellular Manager Profile Feature
1. Click [here](../tutAddProfileManagerFeature) to see how to add a specific feature to the Profile Manager.

2. Provide "CellularProfile" as the Profile Name for this tutorial.

	> Note: You can provide any Profile Name but make sure to access it with the similar name in the Android code.  
  
3. Now, you can see all these MX features on the left hand side of the Profile Editor window. Select the "Cellular Manager" feature from the list and click "Right Arrow".

    ![img](../../images/MxCellularManagerTutorialImages/cellular_feature.jpg)   

4. Provide some name in the "Name" field (Ex. MyCellularManager). The "Name" field is used to identify each feature, which is required when editing features programmatically. You can also keep the "Name" field empty.

	Cellular Manager also allows you to configure (Turn ON/OFF) the state of Background Data on your Symbol devices.

	> Note: If you turn "State of Background Data" ON, some of the apps and services won't work unless you're connected to Wi-Fi.

    So as discussed, we will turn ON the state of Data Roaming using Cellular Manager feature of Mx through Profile Manager wizard. So click on "Set the state of Data Roaming" drop-down in the wizard and select the option "Turn on".    

    ![img](../../images/MxCellularManagerTutorialImages/cellular_manager_details.jpg)

    ![img](../../images/MxCellularManagerTutorialImages/cellular_manager_details_selected.jpg)    
 
5. Click Apply to apply the settings we provided    
  
    ![img](../../images/MxCellularManagerTutorialImages/cellular_profile_created.jpg)

6. Click Finish and your Cellular profile for configuring Roaming State is created.

    ![img](../../images/MxCellularManagerTutorialImages/cellular_manager_profile_created.jpg) 
  
7. Click "Close".

    >Note:  
    >Now the "EMDKConfig.xml" is created under "\assets" folder. This file will contain a definition of all of your profiles that you create. 
    
  
8. You can inspect the EMDKConfig.xml to see it is reflecting the changes made to the parameters via EMDK Profile Manager GUI earlier.  However, it is advised that this file not be manually updated and only be controlled via the Profile Manager.

    ![img](../../images/MxCellularManagerTutorialImages/emdk_config_file_entries.jpg)    

## Enabling Android Permissions
1. Modify the Application's Manifest.xml to use the EMDK library and to set permission for the EMDK.
  
    ![img](../../images/MxCellularManagerTutorialImages/manifest_file.jpg)

    You must first enable permissions for 'com.symbol.emdk.permission.EMDK':  
   
        :::xml
        <uses-permission android:name="com.symbol.emdk.permission.EMDK"/> 

    Then you must enable the library:  
      
        :::xml
        <uses-library android:name="com.symbol.emdk"/>

    When done, your manifest.xml should look like:

    ![img](../../images/MxCellularManagerTutorialImages/manifest_permissions_added.jpg) 

##Adding Some Code    
1. Now we will start to add some code. 

    First you must add references to the libraries:  
    
        :::java
        import com.symbol.emdk.*;  
        import com.symbol.emdk.EMDKManager.EMDKListener;  
		import android.widget.Toast;    

    Then you must extend the activity to implement EMDKListener. Use Eclipse's Content Assist to implement the unimplemented functions of `onOpened` and `onClosed`.    
    
        :::java
        public class MainActivity extends Activity implements EMDKListener {  
          
            .. .. .. .. .. .. ...  
          
            @Override  
            public void onClosed() {  
                   // TODO Auto-generated method stub  
            }  
          
            @Override  
            public void onOpened(EMDKManager emdkManager) {  
                   // TODO Auto-generated method stub  
            }  
          
        }      

    We will now create some global variables to hold the profile name as well as instance objects of EMDKManager and ProfileManager with a status variable while applying the profile. Some of the variables are used to hold the name, type and description in case of any errors. These variables would be used throughout the code. 

    >Note:
    >Verify the Profile name in the code with the one created in the Profile Manager. They both should be identical.    
    
        :::java
        // Assign the profile name used in EMDKConfig.xml
	    private String profileName = "CellularProfile";

	    // Declare a variable to store ProfileManager object
	    private ProfileManager profileManager = null;

	    // Declare a variable to store EMDKManager object
	    private EMDKManager emdkManager = null;

		// Contains the parm-error name (sub-feature that has error)
		private String errorName = "";

		// Contains the characteristic-error type (Root feature that has error)
		private String errorType = "";

		// contains the error description for parm or characteristic error.
		private String errorDescription = "";

		// contains status of the profile operation
		private String status = "";

    In the onCreate method, we call getEMDKManager so that the EMDK can be initialized and checked to see if it is ready. 

        :::java
        //The EMDKManager object will be created and returned in the callback.  
        EMDKResults results = EMDKManager.getEMDKManager(getApplicationContext(), this);  
          
        //Check the return status of getEMDKManager  
		if (results.statusCode == EMDKResults.STATUS_CODE.SUCCESS) {

			// EMDKManager object creation success

		} else {

			// EMDKManager object creation failed

		}


    So far your code should look like:
     
    ![img](../../images/MxCellularManagerTutorialImages/variables_added.jpg)

	![img](../../images/MxCellularManagerTutorialImages/on_create_added.jpg)
	 
2. Now we need to use the `onOpened` method to get a reference to the EMDKManager. The EMDKListener interface will trigger this event when the EMDK is ready to be used. The EMDKListener interface must be implemented in order to get a reference to the EMDKManager APIs. This event will pass the EMDKManager instance and we assign it to the global variable `emdkManager` that we created in the previous steps. We then use that instance object to get an instance of ProfileManager and assign it to the global variable `profileManager`. This is how we will interface with the APIs in the rest of the code:

    > Note: 
    > Rename the argument of `onOpened` method from `arg0` to `emdkManager`  

        :::java
        // This callback will be issued when the EMDK is ready to use.
		this.emdkManager = emdkManager;

		// Get the ProfileManager object to process the profiles
		profileManager = (ProfileManager) emdkManager
				.getInstance(EMDKManager.FEATURE_TYPE.PROFILE);         
    
    Now that we have a reference to ProfleManager, we use it to install and activate the profile we built earlier using the `processProfile` method. We could have also performed this action at a different time, say when someone pressed a button, but we chose to do it as soon as the EMDK was ready:

		:::java
		if (profileManager != null) {
			String[] modifyData = new String[1];

			// Call processPrfoile with profile name and SET flag to create the profile. The modifyData can be null.
			EMDKResults results = profileManager.processProfile(profileName,
					ProfileManager.PROFILE_FLAG.SET, modifyData);

			if (results.statusCode == EMDKResults.STATUS_CODE.CHECK_XML) {


			} else {
			  // Show dialog of Failure
				AlertDialog.Builder builder = new AlertDialog.Builder(this);
				builder.setTitle("Failure");
				builder.setMessage("Failed to apply profile...")
						.setPositiveButton("OK",
								new DialogInterface.OnClickListener() {
									public void onClick													(DialogInterface dialog,
											int id) {

									}
								});
				AlertDialog alert = builder.create();
				alert.show();
			}

		}

    This `processProfile` method returns the result of applying a particular profile that we set using EMDK Profile Wizard in [EMDKResults](../../api/core/EMDKResults) reference. If the profile is successfully processed, it retuns the status as `CHECK_XML` and then we go on and parse the response to get further details whether the profile was applied successfully or not. Otherwise we display a Failure message in a [dialog](http://developer.android.com/reference/android/app/AlertDialog.html).

	> Note: 1. There is a difference between processing a profile successfully and applying a profile successfully.

	> Note: 2. If the status is other than `CHECK_XML`, we are simply displaying a failure message. You can actually go ahead and check different types of status and display the appropriate message accordingly, which is not in the scope of this sample tutorial.


	In case of `CHECK_XML` status, We retrieve  XML response string from the result using `getStatusString` method.

		:::java
		// Get XML response as a String
		String statusXMLResponse = results.getStatusString();

	Further, we would parse this XML response string using [XML Pull Parser](http://developer.android.com/reference/org/xmlpull/v1/XmlPullParser.html) in order to get the status and error parameters if any. XML Pull Parser is an interface that defines parsing functionality provided in [XMLPULL V1 API](http://www.xmlpull.org/) (visit this website to learn more about API and its implementations). In the parsing we would be looking for specific status tags (Error Name, Error Type and Error Description) in case of any errors and if found, we would get those values in the respective global variables that we have declared in previous step.

		:::java
		try {
			// Create instance of XML Pull Parser to parse the response
			XmlPullParser parser = Xml.newPullParser();
			// Provide the string response to the String Reader that reads
			// for the parser
			parser.setInput(new StringReader(statusXMLResponse));
			// Call method to parse the response
			parseXML(parser);
			} catch (XmlPullParserException e) {
				e.printStackTrace();
			}

	> Note: Here we have called the method `parseXML` to parse XML response string. We will declare the method in the next step. 

	Once the response is parsed, we would display the result of applying this profile in a [dialog](http://developer.android.com/reference/android/app/AlertDialog.html) by calling `displayResults` method, which we would declare in coming steps.

		:::java
		// Method call to display results in a dialog
		displayResults();

    Your complete `onOpened` method should now look like:
    
    ![img](../../images/MxCellularManagerTutorialImages/on_opened_method_1.jpg) 

    ![img](../../images/MxCellularManagerTutorialImages/on_opened_method_2.jpg) 

3. You will see few errors as we have not declared the respective methods to parse the response and display result. Lets do it one by one. In this step, we will create a method `parseXML` that uses [XML Pull Parser](http://developer.android.com/reference/org/xmlpull/v1/XmlPullParser.html) to parse the XML string response and set the status and error parameters if any.

	In the reponse, we are supposed to capture `name` and `desc` for `parm-error` tag, `type` and `desc` for `characteristic-error` tag in case of any errors.

		:::java
		// Method to parse the XML response using XML Pull Parser
		public void parseXML(XmlPullParser myParser) {
		int event;
		try {
			event = myParser.getEventType();
			while (event != XmlPullParser.END_DOCUMENT) {
				String name = myParser.getName();
				switch (event) {
				case XmlPullParser.START_TAG:
					// Get Status, error name and description in case of
					// parm-error
					if (name.equals("parm-error")) {
						status = "Failure";
						errorName = myParser.getAttributeValue(null, "name");
						errorDescription = myParser.getAttributeValue(null,
								"desc");

						// Get Status, error type and description in case of
						// parm-error
					} else if (name.equals("characteristic-error")) {
						status = "Failure";
						errorType = myParser.getAttributeValue(null, "type");
						errorDescription = myParser.getAttributeValue(null,
								"desc");
					}
					break;
				case XmlPullParser.END_TAG:

					break;
				}
				event = myParser.next();

			  }
		    } catch (Exception e) {
			e.printStackTrace();
		    }
		}

    Your complete `parseXML` method should now look like:
    
    ![img](../../images/MxCellularManagerTutorialImages/parse_xml_1.jpg) 
	![img](../../images/MxCellularManagerTutorialImages/parse_xml_2.jpg)

4. You will still see one error as we need to declare `displayResults` method to display the result of profile operation in a [dialog](http://developer.android.com/reference/android/app/AlertDialog.html). Before displaying the results, we should form the content of the result to be shown first, specifically in case of errors. This could be done by creating `buildFailureMessage` method.
 
    In this method, the error message in case of error is formed using following way: 

    * Name and description of error if the response contains `parm-error`.
    * Type and description of error if the response contains `characteristic-error`.
    * Name, type and description of error if the response contains both `parm-error` and `characteristic-error`.

	The `buildFailureMessage` method would have following code to match the above mentioned criteria.  

		:::java
		// Method to build failure message that contains name, type and
		// description of respective error (parm, characteristic or both)
		public String buildFailureMessage() {
		  String failureMessage = "";
		  if (!TextUtils.isEmpty(errorName) && !TextUtils.isEmpty(errorType))
			 failureMessage = errorName + " :" + "\n" + errorType + " :" + "\n"
					+ errorDescription;
		  else if (!TextUtils.isEmpty(errorName))
			 failureMessage = errorName + " :" + "\n" + errorDescription;
		  else
			 failureMessage = errorType + " :" + "\n" + errorDescription;
		  return failureMessage;

		}

    `buildFailureMessage` method should look like:
    
    ![img](../../images/MxCellularManagerTutorialImages/build_failure_message.jpg)

5. In this step, we will add `displayResults` method to display the result of profile operation in a [dialog](http://developer.android.com/reference/android/app/AlertDialog.html). The dialog would display status as `Success` or `Failure` with corresponding message based on the response of profile operation.

		:::java
		// Method to display results (Status, Error Name, Error Type, Error
		// Description) in a
		// dialog
		public void displayResults() {
		  // Alert Dialog to display the status of the Profile creation
		  // operation of MX features
		  AlertDialog.Builder alertDialogBuilder = new AlertDialog.Builder(
				MainActivity.this);

		  if (TextUtils.isEmpty(errorDescription)) {
			alertDialogBuilder.setTitle("Success");
			alertDialogBuilder.setMessage("Profile Successfully Applied...");
		  } else {
			// set title
			alertDialogBuilder.setTitle(status);
			// call buildFailureMessage() method to set failure message in
			// dialog
			alertDialogBuilder.setMessage(buildFailureMessage());
		  }

		  alertDialogBuilder.setCancelable(false).setPositiveButton("OK",
				new DialogInterface.OnClickListener() {
					public void onClick(DialogInterface dialog, int id) {
					}
				});
		  // create alert dialog
		  AlertDialog alertDialog = alertDialogBuilder.create();

		  // show it
		  alertDialog.show();

	    }  

    The method `displayResults` should look like:
    
    ![img](../../images/MxCellularManagerTutorialImages/display_results.jpg)

	You can see that all the errors are gone.
           
    
6. Now let's override the "onDestroy" method so we can release the EMDKManager resources:  

        :::java
        @Override  
        protected void onDestroy() {  
            // TODO Auto-generated method stub  
            super.onDestroy();  
            //Clean up the objects created by EMDK manager  
            emdkManager.release();  
        } 

    Your onDestroy method should now look like this:  

    ![img](../../images/MxCellularManagerTutorialImages/on_destroy_method.jpg) 

That's it!!! We are done with all the coding and configuration part that will let us turn ON the state of Data Roaming on Symbol device. Now let's run the application.
 
## Running the Application

1. Connect the device (having the latest EMDK runtime) to USB port. 

    > Note:   
    > Make sure the device is in USB debug.

    Before running the application, We will make sure that Data Roaming of our Symbol device is turned OFF. 

    Go to device's Settings -> Mobile Networks and make sure that "Data Roaming" is unchecked.

    ![img](../../images/MxCellularManagerTutorialImages/data_roaming_off.png) 

2. Run the application.

    ![img](../../images/MxCellularManagerTutorialImages/home_screen.png)

    You can see an [Alert Dialog](http://developer.android.com/reference/android/app/AlertDialog.html) with a success message.

	> Note: In case of any errors, you will see a Failure status with respective error message in that dialog.
  
3. We will see the status of "Data Roaming" in the settings. So go to device's Settings -> Mobile Networks again and you would now see that "Data Roaming" has been turned ON by Cellular Manager that we had set in the profile wizard. 

    ![img](../../images/MxCellularManagerTutorialImages/data_roaming_on.png)

    This is how Cellular Manager lets us turn ON/OFF Data Roaming of the Symbol devices using Profile Wizard. 

##Important Programming Tips##

1. It is required to do the following changes in the application's AndroidManifest.xml:  
  
    >Note:
    >* Include the permission for EMDK:  
    
        :::xml
        <uses-permission android:name="com.symbol.emdk.permission.EMDK"/>
    
	>Note:
    >* Use the EMDK library:  
    
        :::xml
        <uses-library android:name="com.symbol.emdk"/>
  
2. Installing the EMDK for Android application without deploying the EMDK runtime on the Symbol device will fail because of missing shared library on the device.
 
4. Use the DataWedge v1.7.12 or higher version to test the ProfileManager.processProfile() for DataWedge profiles.

## What's Next
Now that you have learned how to set Roaming State using Cellular Manager on your Symbol devices through applications, let us try to understand and implement some of the other new Mx features introduced in EMDK for Android V 3.1. So in the next tutorial, we will concentrate on the "Display Manager" feature of Mx and try to explore this feature by creating a tutorial.











