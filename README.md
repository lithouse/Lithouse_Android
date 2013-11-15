Lithouse_Android
================
This repository contains a library for building apps connected to Lithouse cloud. We also included a demo for quick start. Please visit http://lithouse.co for more information.

##Normal Usage
In order to use the library with [Eclipse ADT] (http://developer.android.com/sdk/index.html), please follow these steps:

###Setup

* Create an Android App (File > New > Android Application Project).
* Import the library `Lithouse` into your workspace (File > Import > Existing Project into Workspace).
* Refer the library from you app by right clicking on the app inside the Project Explorer. In the resulting pop-up select (Properties > Android > Add).
* Now, collect the following attributes from you developer account at http://lithouse.co.

```java
private final String appKey = "YOUR_APP_KEY";
private final String groupId = "TARGET_GROUP_ID";
private final String deviceId = "TARGET_DEVICE_ID";
```
* Finally, initialize `LithouseService` with your app key.

```java
private final LithouseService mLithouseService = new LithouseService ( this, appKey );	
```

###Sending Records

* Prepare an `ArrayList <Record>` with the records you want to send. Records may target different device or different channel within the same device. But, all target devices in a single call must belong to the same group.
* Implement a `LithouseService.Callback` for receiving the api response. `onSuccess` will receive the record list you just sent. 
 
###Receiving Records

Similar to sending record, implement a `LithouseService.Callback`. 
It is possible to call the `receive` in one of the following ways:

```java
//All records belonging to receiveChannel from deviceId1 and deviceId2
mLithouseService.receive ( mReceiveCallback, groupId, 
    Arrays.asList ( deviceId1, deviceId2 ), Arrays.asList ( receiveChannel ) );
				
//All records from all channels of this device
mLithouseService.receive ( mReceiveCallback, groupId, Arrays.asList ( deviceId ), null );

//All records from different devices with the same channel name
mLithouseService.receive ( mReceiveCallback, groupId, null, Arrays.asList ( receiveChannel ) ); 

//All records from all devices of this group
mLithouseService.receive ( mReceiveCallback, groupId, null, null );

```
##Exceptions
In `LithouseService.Callback` you have to implement `onFailure`. This method will be called with a `Throwable` 
object if something went wrong.
