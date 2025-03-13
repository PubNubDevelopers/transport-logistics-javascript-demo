# Transport & Logistics, and Asset Management Demo written in JavaScript

> Application to show how PubNub can be used for transport & logistics use cases, displaying and controlling worldwide assets in real time

Using PubNub you can communicate bidirectionally with global assets in real time with minimum latency.  This dashboard shows how a transport & logistics solution managed by PubNub might look, specifically:

- Vehicles will report their delivery status (remaining deliveries, next destination)
- A temperature sensor on that vehicle will periodically report it's reading.  Rebooting the sensor will cause it to go temporarily offline, and its corresponding PubNub presence will show this online / offline state.
- You can send a push message to the driver's mobile phone.

> This application is designed to show how a T&L solution with PubNub might look and is deliberately a **canned demo, though you can localize it if you grant location permissions to the page**.  For information on how to take this concept to production, please see the "Further Information" section in this ReadMe.  

![Screenshot](https://raw.githubusercontent.com/PubNubDevelopers/transport-logistics-javascript-demo/main/media/screenshot_square.png)

## Demo

A hosted version of this demo can be found at https://www.pubnub.com/demos/transport-logistics/

## Features

* Communicates over the PubNub network - devices send sensor data and location which is displayed on the dashboard
* Administrative tasks such as rerouting and remote device reboot can be performed from the dashboard 
* Uses JavaScript WebWorkers to simulate real hardware.
* Experience the real time, scalable performance delivered by PubNub

## Installing / Getting started

This dashboard shows how a PubNub transport & logistics dashboard might look.  For ease of use, devices are simulated but PubNub offers [over 50 SDKs](https://www.pubnub.com/docs/sdks), enabling you to connect to any solution..

To run this project yourself you will need a PubNub account and a Google Maps API key, as explained later in this ReadMe.

### Requirements
- [PubNub Account](#pubnub-account) (*Free*)

<a href="https://admin.pubnub.com/register">
	<img alt="PubNub Signup" src="https://i.imgur.com/og5DDjf.png" width=260 height=97/>
</a>


### Get Your PubNub Keys

1. You’ll first need to sign up for a [PubNub account](https://dashboard.pubnub.com/signup/). Once you sign up, you can get your unique PubNub keys from the [PubNub Developer Portal](https://admin.pubnub.com/).

1. Sign in to your [PubNub Dashboard](https://admin.pubnub.com/).

1. Click Apps, then **Create New App**.

1. Give your app a name, and click **Create**.

1. Click your new app to open its settings, then click its keyset.

1. Enable the Presence feature for your keyset.

1. Enable the Stream Controller feature for your keyset.

1. Enable the Persistence feature for your keyset.

1. Copy the Publish and Subscribe keys and paste them into your app as specified in the next step.

### Building and Running

1. You'll need to run the following commands from your terminal.

1. Clone the GitHub repository.

	```bash
	git clone https://github.com/PubNubDevelopers/transport-logistics-javascript-demo.git
	```
1. Navigate to the application directory.

	```bash
	cd transport-logistics-javascript-demo
	```

1. Add your pub/sub keys to `js/keys.js`

1. Add your Google Maps API key which supports the JS Maps API and Geocoding to `js/keys.js`.  See 'Using your own Google Maps API key', below.

1. Start a local web server, for example if you have python installed you can run `python3 -m http.server 8080`.  This is required since the demo application uses web workers.

1. Load `localhost:8080` within your browser (or whichever port you are running the server on). 


## Contributing
Please fork the repository if you'd like to contribute. Pull requests are always welcome. 

## Links


## Further Information

Checkout the following lins for more information on developing transport, delivery, & logistics solutions with PubNub:

- Transport, Delivery, & Logistics with PubNub: https://www.pubnub.com/solutions/transport-delivery/

## Using your own Google Maps API key

The steps to provide your own Google Maps API key are as follows:

1. Visit https://developers.google.com/maps/documentation/javascript/get-api-key and follow the instructions to create a project and API keys
1. Make sure you have the following APIs enabled: 'Maps Embed API', 'Maps JavaScript API', Geocoding API.  
1. Add your Google Maps API key to `js/keys.js`.

## Architectural Notes, Next Steps and Future Work

**A Note about Signals**

PubNub offers the `signal()` method as an alternative to `publish()` for short lived, ephemeral data which goes out of date quickly.  The same delivery guarantees do not exist for signals but signal pricing can be lower than publish.  The primary limitation of signals, besides not being able to be stored in history or trigger push messages, is that they are limited to **64bytes**.  This demo uses `signal()` to exchange both location and sensor reading data, which is the most common approach our customers take, whilst using `publish()` for data that requires reliable delivery, for example this demo uses publish() to exchange delivery and route data.

**Message Persistence:**

- For ease of use, this demo lacks any kind of serverside message persistence.  Most customers deploying this kind of solution with PubNub will choose to use **[PubNub App Context](https://www.pubnub.com/docs/sdks/javascript/api-reference/objects)** to store attributes of the device.  This is analogous to a 'device shadow' in AWS or 'twin device' in Azure.
- Because entities are only stored locally, if you refresh the page you will lose any created simulators (JavaScript web workers).  **This is a limitation of the demo, not a limitation of PubNub**.

