---
publish: true
title: Scan and Pair
description: This sample application will show how the Scan and Pair API can be used to pair two bluetooth devices programmatically.
downloads:
  - title: Android Studio Project
    url: 'https://github.com/developer-zebra/samples-emdkforandroid-4_0/archive/ScanAndPairSample1.zip'
  - title: ADT Eclipse Project
    url: 'https://github.com/developer-zebra/samples-emdkforandroid-4_0-ADT/archive/ScanAndPairSample1.zip'
sources:
  - title: Android Studio Project
    url: 'https://github.com/developer-zebra/samples-emdkforandroid-4_0/tree/ScanAndPairSample1'
  - title: ADT Eclipse Project
    url: 'https://github.com/developer-zebra/samples-emdkforandroid-4_0-ADT/tree/ScanAndPairSample1'
features:
  - Profile Manager
  - Scan and Pair
  - Java APIs
devices:
  - MC18KK
  - MC32N0JB
  - MC40JB
  - MC40KK
  - MC67JB
  - MC92KK
  - TC55JB
  - TC55KK
  - TC70KK
  - TC75KK
image: 1.png
screenshots:
  - 1.png
  - 2.png
layout: sample.html
product: EMDK For Android
productversion: '4.0'
---

##Overview
This sample application will show how the Scan and Pair API can be used to pair two bluetooth devices programmatically.

##Prerequisites
- Java JDK 
- Eclipse with ADT plugin or  Android Studio
- EMDK for Android  
- An EMDK supported Android device

For more information about setting up the EMDK please see the [EMDK Setup Guide](/emdk-for-android/4-0/guide/setup).

For this sample, you will need two Android Bluetooth devices, one must be an EMDK for Android supported device. You will also need a barcode that contains the Bluetooth MAC address of the remote bluetooth device that we will be pairing with(The one not running the EMDK app).

##Loading the Sample Application
The following guide will walk you through setting up the EMDK samples in your IDE.

* [Android Studio](/emdk-for-android/4-0/guide/emdksamples_androidstudio)
* [Eclipse/ADT](/emdk-for-android/4-0/guide/emdksamples_eclipse)
##Using This Sample

1.  When the application starts it should look like the following. Leave the **Always Scan** and **Hard Trigger** check boxes selected, and insure the **ScanData Type** spinner is set to **MAC ADDRESS**.  

  ![img](scanandpair1.png)  

2. Press the **Pair** button. The Status label will update, stating that the Scan and Pair process has started, and then prompt the user to press the hard scan trigger.

  ![img](scanandpair3.png)   

3. Now place the Pairing Barcode in view of the devices scan window, and then press the devices Hard Scan Trigger. The Scan and Pair sample app will retrieve MAC address from the barcode and place it in the **Bluetooth Address** field, then it will initiate the pairing and connection process. Press **Pair** in the Pairing Request dialog, to complete the pairing process. 
After pairing is complete, the status label will display "Bluetooth device is paired successfully".

  ![img](scanandpair4.png) 















