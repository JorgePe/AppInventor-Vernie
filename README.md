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
