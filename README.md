# MPU6050 IMU Visualization Test for NodeMCU V2
Project to visualize the accelerometer and gyroscope readings of the MPU6050 sensor under the presence of its built-in Digital Motion Processor(DMP) with the NodeMCU V2(ESP8266) as a host. The project is based on the [i2cdev library](https://github.com/jrowberg/i2cdevlib/tree/master/Arduino) by Jeff Rowberg. The project also contains the Processing sketch to visualize a model that constantly updates itself based on the quaternions received by the MPU6050's FIFO. 

## Software Required
1. [PlatformIO](https://platformio.org/) Extension on VSCode.
1. [Processing](https://processing.org/download).
1. [Toxiclibs](https://github.com/postspectacular/toxiclibs/releases/tag/0021)

## Hardware Connections
1. The MPU6050's VCC and GND pins have been connected to the 3.3v and GND pins of the NodeMCU.
1. The MPU6050's SCL and SDA pins have been connected to D2 and D1 of the NodeMCU respectively.
1. The MPU6050's INT pin is connected to D5 on the NodeMCU
1. The MPU6050's AD0 pin may be left unconnected or connected to GND on the NodeMCU to ensure that the I2C address remains 0x68. Incase the AD0 pin is connected to high this address changes to 0x69 and changes need to be made to the main.cpp file. The ADO pin was left unconnected during my tests.

## Accelerometer and Gyroscope Calibration
After compiling and uploading the source code to the NodeMCU, you'll have to send any character to through the serial monitor in order to trigger the initialization of the DMP. Once this is done the calibration functions run in order to print out the appropriate offsets for your MPU6050.

The 6 values printed out in the serial monitor now represent the offsets for acceleration in the X, Y, Z directions and rotation rate(angular velocity) about the X, Y, Z directions respectively.

These values can now be set in:

https://github.com/scar027/imu-test-visual-nodemcuv2/blob/cc2f0256e39aa256e1ca2098fe5810a56c5c6d9d/src/main.cpp#L206-L210

Now if you run the code on your board again you should get more accurate values for yaw, pitch and roll(y, p, r) respectively.

## Visualization
The values produced by the IMU can be graphically visualized in the Processing environment by running the [.pde file](processing/MPUTeapot/MPUTeapot.pde) in the processing folder on Processing.

The visualization demo also depends on toxiclibs which should be added in the libraries folder of the folder where your Processing is installed.

Windows users need to set the correct serial port by commenting out:

https://github.com/scar027/imu-test-visual-nodemcuv2/blob/cc2f0256e39aa256e1ca2098fe5810a56c5c6d9d/processing/MPUTeapot/MPUTeapot.pde#L71-L71

and uncommenting:

https://github.com/scar027/imu-test-visual-nodemcuv2/blob/cc2f0256e39aa256e1ca2098fe5810a56c5c6d9d/processing/MPUTeapot/MPUTeapot.pde#L74-L74

and setting the appropriate COM port.

The current code has been tested for Linux x86_64.