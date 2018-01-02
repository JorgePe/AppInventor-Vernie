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
