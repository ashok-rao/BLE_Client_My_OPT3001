TL;DR : You can find the ".bin" file to be flashed into the target under the BUILD directory.

# BLE Client for OPT3001

This example demonstrates using the ``GattClient`` API to control BLE client devices.

The example uses two applications running on two different devices:

1. The first device - the central - runs the application ``BLE_Server_MY_OPT3001`` from https://github.com/ashok-rao/BLE_Server_MY_OPT3001.git repository. This application sends light data sensed from OPT3001 from I2C (BOOSTXL-Sensors breakout board) over BLE.

1. The second device - the peripheral - runs the application ``BLE_Client_My_OPT3001`` to read the data sent over BLE.

	The data can be seen in hex in the serial terminal for the client after a successful connection.

# Running the application

## Requirements

Hardware requirements:
1. NUCLEO_F429ZI board (running mbed firmware) - You'll need 2x (1 for the server and 1 for the client)
2. X-NUCLEO-IDB05A1 BLE shields running v7.2 or later firmware. The latest firmware is here: https://developer.mbed.org/teams/ST/code/BlueNRG-MS-Stack-Updater/
3. An OPT3001 sensor board.
4. A couple of jumpers / USB cables etc.

This example requires *two* devices.

## Building instructions

You will need to build both applications and flash each one to a different board.

Please note: The application ``BLE_Client_My_OPT3001`` in this repository initiate a connection to all ble devices which advertise "OPT3001" as complete local name. By default, the application `BLE_Server_My_OPT3001` advertise "OPT3001" as complete local name. If you change the local name advertised by the application `BLE_Sever_My_OPT3001` you should reflect your change in this (Client) application by changing the value of the constant `PEER_NAME` in `main.cpp`.

Building instructions for all mbed OS samples are in the [main readme](https://github.com/ARMmbed/mbed-os-example-ble/blob/master/README.md).

## Checking for success

1. Build both applications and install one on each device, as explained in the building instructions.

## Monitoring the application through a serial port

You can run ``BLE_Cleint_My_OPT3001`` and see that it works properly by monitoring its serial output.

You need a terminal program to listen to the output through a serial port. You can download one, for example:

* Tera Term / PuTTY for Windows.
* CoolTerm for Mac OS X.
* GNU Screen for Linux.

To see the application's output:

1. Check which serial port your device is connected to.
1. Run a terminal program with the correct serial port and set the baud rate to 9600. For example, to use GNU Screen, run: ``screen /dev/tty.usbmodem1412 9600``.
1. The application should start printing the light sensor's value to the terminal.

**Note:** ``BLE_Client_My_OPT3001`` will not run properly if the ``BLE_Server_My_OPT3001`` application is not running on a second device. The terminal will show a few print statements, but you will not be able to see the application in full operation.
