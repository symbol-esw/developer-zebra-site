---
title: ScannerInfo
layout: guide.html
product: EMDK For Xamarin
productversion: '1.0'
---
ScannerInfo provides information of the scanner device.

**Type** - Java.Lang.Object

##Methods
###GetConnectionType
**public virtual Symbol.XamarinEMDK.Barcode.ScannerInfo.ConnectionType GetConnectionType ();**

Returns the scanner connection type to mobile computer Note: The connection type information is not available on Scanner Framework 1.18.P03 on TC55 REV A device.


**Returns** - Symbol.XamarinEMDK.Barcode.ScannerInfo+ConnectionType

###GetDecoderType
**public virtual Symbol.XamarinEMDK.Barcode.ScannerInfo.DecoderType GetDecoderType ();**

Returns the barcode scanning type supported by scanner. Note: The decoder type information is not available on Scanner Framework 1.18.P03 on TC55 REV A device.


**Returns** - Symbol.XamarinEMDK.Barcode.ScannerInfo+DecoderType

###GetDeviceType
**public virtual Symbol.XamarinEMDK.Barcode.ScannerInfo.DeviceType GetDeviceType ();**

Returns the scanner device type


**Returns** - Symbol.XamarinEMDK.Barcode.ScannerInfo+DeviceType

##Properties

###FriendlyName
Returns the friendly name of the Device..

**Type** - System.String
###IsConnected

        

**Type** - System.Boolean
###IsDefaultScanner
Returns true if it is a default scanner else false.

**Type** - System.Boolean
###ModelNumber
Returns the scanner device model number. This information will be available only after the scanner is enabled. Note: The model number is supported on the Scanner Framework version 3.0.11 or later.

**Type** - System.String















