rapitag native API
===================

Events
-------------
The communication between the rapitag API is per default always asynchronous and event based. The format always follows the same structure:

```
{ 
	'name': 'Init',
	'payload: {
		'showAlert': True
	}
}
```

----------

### Essential Events

#### Init
At first you always have to call init on the api. This also initialises the Bluetooth interface.

- You can add an optional paylod `showAlert` of type `Boolean`. On iOS it shows or hides the alert if the bluetooth is turned off during initialisation.

#### Search
This tells the smartphone to start searching for rapitags within the closest area to the phone. This state will be active until you send a StopSearch event or make a connection to a rapitag.

#### StopSearch
This stops the searching of rapitags.

#### Callback Event: FoundDevices
This callback is fired when rapitags are within reach.

The payload could look like this:
```
{ 
	'devices': [
		 { 'id: 'XXXXX-XXXXX-XXXXXX-XXXXX', ... }, 
		 // If additional information are available (maybe product data), they will be added where the dots are
		 { 'id: 'XXXXX-XXXXX-XXXXXX-XXXXX', ... },
		 { 'id: 'XXXXX-XXXXX-XXXXXX-XXXXX', ... }
		}
	]
}
```
#### Reserve
This event is used when a user is interested in a product. This has the following effects:
- A connection to the rapitag is established.
- The rapitag gives an optical feedback to the user that it is reserved now.
- The rapitag increases the transmission rate to 40dB (about 20m).
- The rapitag is exclusive available to the connected user. No other customers can find the rapitag.

This call expects a payload of type `{'deviceId': 'XXXXX-XXXXX-XXXXXX-XXXXX'}`
