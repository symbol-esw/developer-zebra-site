---
publish: true
title: Barcode APIs
description: 'This sample application will allow you to scan barcodes based on selected scanner device, trigger type and a few decoder Decoder Params.'
download: 'https://github.com/developer-zebra/samples-emdkforxamarin-1_0/archive/BarcodeSample1.zip'
source: 'https://github.com/developer-zebra/samples-emdkforxamarin-1_0/tree/BarcodeSample1'
features:
  - Profile Manager
  - Barcode
  - 'C# APIs'
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
  - 3.png
  - 4.png
  - 5.png
  - 6.png
layout: sample.html
product: EMDK For Xamarin
productversion: '1.0'
---

##Overview
The Barcode API's are used when you wish to handle all barcode scanning entirely in C# using [Barcode/Scanning APIs](/emdk-for-xamarin/1-0/api/). These API's work independently of any Data Capture profiles.  

The available actions in the [Barcode/Scanning API](/emdk-for-xamarin/1-0/api/barcode/) are:
  
* Set Scanner Device  
* Set [TriggerType](/emdk-for-xamarin/1-0/api/barcode/Scanner_TriggerTypes)
* Set [Decoder Params](/emdk-for-xamarin/1-0/api/barcode/ScannerConfig_DecoderParameters)
* Set [Reader Params](/emdk-for-xamarin/1-0/api/barcode/ScannerConfig_ReaderParameters)
* Set [Scan Params](/emdk-for-xamarin/1-0/api/barcode/ScannerConfig_ScanParameters)
* Scan barcodes based on selected features   

This sample application will allow you to scan barcodes based on selected scanner device, trigger type and few decoder [Decoder Params](/emdk-for-xamarin/1-0/api/barcode/ScannerConfig_DecoderParameters).


## Opening The Component Sample
This sample is also included with the EMDK Component, follow this guide to [open Sample included in Component](../../guide/component-sample).

##Loading the Sample Application

1. Choose a sample and click the **See Details** button.
2. Now click the **Download** button 
3. Extract the downloaded project zip file.
4. Navigate to the root of the unzipped project folder and double-click the **.sln** file. The project will load in the default IDE for that file type.

Alternatively, you can Launch your prefered IDE ( Visual Studio or Xamarin Studio ) and load the project via the File > Open menu.  

##Running The Sample
###Visual Studio

Visual Studio will detect your device connected via USB, it will display the name of that device next to the "Play" button.

![img](../../images/samples/vsPlayButton.png)

Press the "Play" button next to the devices name.  The IDE will build, deploy and start the sample app on your device.

###Xamarin Studio
In Xamarin Studio, you may need to select your attached device from the devices dropdown under `Physical Devices`.

![img](../../images/samples/xs-select-device.png)

Now press the "Play" button. The IDE will build, deploy and start the sample app on your device.

![img](../../images/samples/xsPlayButton.png)

## Using the Sample
1. When the application starts it should look like the following.
  
	![img](../../images/samples/barcode_1.png)
  
2. Set scanner to "Serial SSI Scanner", which is the default one". 

	![img](../../images/samples/barcode_2.png)

3. Set Trigger Type to "HARD".

	![img](../../images/samples/barcode_3.png)

	> Note: Trigger Type "HARD" lets you scan the barcode using device's hard scan key whereas "SOFT" allows you to scan without using device's hard scan key.

4. Keep all checkboxes checked for decoder params and this is how it should look after setting all fields.
    
	![img](../../images/samples/barcode_4.png)  	

5. Click "Start" button and the status will be updated.

	![img](../../images/samples/barcode_5.png) 
 
6. Since we selected Trigger Type as "HARD", press the hard scan key of Symbol device and scan a particular barcode. It will get the scanned barcode data in "Data" field of UI.
   
	![img](../../images/samples/barcode_6.png) 

















