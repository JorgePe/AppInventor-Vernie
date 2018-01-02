# AppInventor-Vernie

This is an App I made with MIT App Inventor 2 for my Android phone.
It allows me to control LEGO BOOST Vernie movement with a basic joystick and to shoot the "cannon" with a button.
The color sensor status is also continuously shown.

Will soon document the process of creating such an app.

A screenshot:

![screenshot](/Screenshot_2018-01-02-12-54-57.png):

The user can [Choose] from a list of several Vernies. For the moment, this list is prebuild so you need to edit the .aia file and use the BLE address of your own devices then [Connect] to the chosen one.

The joystick controls both tracks at the same time. Speed is proportional to amplitude and the direction of motion is related to the angle so moving joystick to:
- Front: moves forward
- Back: moves backwards
- Right: turns right
- Left: turns left

And moving somewhere between these directions gives a mix forward/backward and rotation.

The joystick doesn't return to center when not in use. This is intended, so you can fix a direction and speed until you press 
the [Reset] button or move yourself the joystick back to center (not easy).

The [Shoot] button makes the head turn enough to trigger the "cannon"... most of the times.


# Requirements

You need [MIT App Inventor 2](http://ai2.appinventor.mit.edu). It's a great tool but for the moment it only builds Android apps altough it is expected to support iOS very soon.

For Bluetooth Low Energy you need the BluetoothLE extension. Current official version is [here](http://iot.appinventor.mit.edu/assets/resources/edu.mit.appinventor.ble.aix) but I used the [2.1 Release Candidate 4](https://www.google.com/url?q=https%3A%2F%2Fwww.dropbox.com%2Fs%2Fsic9kvft8atynly%2FBLE-v2.1-rc4.aix%3Fdl%3D0&sa=D&sntz=1&usg=AFQjCNHFymz0G27-XELIu0mMk3016QMn_g) without issues.

For the moment, you need to know the BLE address of your LEGO BOOST Move Hub. You can use a free Android app from Nordic, nRF Connect, to get this address.
It's easy to get a dynamic list of the BLE devices found nerarby but my office has so many that my phone screen was cluttered, will later try a better version that filters BLE addresses by manufacturer and shows only LEGO devices.


# Explaining the App

If you import the .aia file you will see on the Designer View that the App uses the follow visual components, all on the same default Screen:


- BtnConnection
- ListPicker1
- Image1
- LblRadius
- LblXY
- LabelJoystick
- BtnRst
- CanvasJoystick
- ImgSpriteJoystick
- BtnShoot


For convenience these UI components are arranged inside Horizontal Arrangements and there also a few labels that I
use as spacers, not listed above.


There are also some non-visual objects:

- One extension, BluetoothLE1. This contains all Bluetooth Low Energy components required to talk with Vernie.
- Two sensors (ClockTracks and ClockShoot). The first is used to regularly send motor commands to Vernie and the second to implement a delay between back and forth movements of the head when triggering the "cannon".
- Three image files (two for the joystick Canvas and Sprite and the other one, a photo of Vernie, used as Image1 and
also used as the Application Icon)


When the Application starts, it initializes the Screen and defines a few global variables:

![Initialization](/initialization.png)


MAXRADIUS, X0 and Y0 are constants used with the joystick. If you change joystick properties you need to update
these values.

SpeedA and SpeedB are global variables contain the speed of motors A and B. Every TRACKSPERIOD milliseconds a BLE
command is sent to update motors speed.

ServiceUUID and CharUUID are the Bluetooth Low Energy UUIDs implemented by LEGO for the BOOST Move Hub (Vernie's core)
and are required by the BluetoothLE extension components.

SHOOTDELAY, SHOOTROTATION and SHOOTSPEED are constants used for triggering Vernie's "cannon" with its head.


On Screen initialization we start BLE scanning, this is required before we can stablish a BLE connection to Vernie.
Then we create a static list with our Vernies nicknames and BLE Addresses, set the text and color of some buttons
and labels and create the Joystick, moving the smaller circled sprite to the center of the larger circled canvas
at (X0,Y0). Finally we initialize both clocks timers, disabling them until they are required.


Before we can connect to Vernie we need to **Choose** which Vernie from a list availabe in **ListPicker1**.
Each Vernie in this list is also a list of two elements: a nickname defined by us (like 'My1stVernie') and a BLE
address.

![List of Vernies](listofvernies.png)

![ListPicker](/listpicker.png)


We update the ListPick1 Text property with the nickname of the device we chose (that's first element of the pair;
the second element, the BLE address, will be used on the connection).

Connection (and disconnection) is done through BtConnection. As soon as a connection is made we start sending
motor commands to motor A+B (tracks) and receiving notifications from the Color/Distance Sensor (in fact we receive all
kind of notifications from Vernie's Move Hub but only pay attention to data related to the Color/Distance Sensor).


![BLEConnection](/BLEconnection.png)
