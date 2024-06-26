# MPU6050 IMU Visualization Test for NodeMCU V2
Project to visualize the accelerometer and gyroscope readings of the MPU6050 sensor with the NodeMCU V2(ESP8266) as a host. The project is based on the [i2cdev library](https://github.com/jrowberg/i2cdevlib/tree/master/Arduino) by Jeff Rowberg. The project also contains the Processing sketch to visualize a model that constantly updates itself based on the quaternions received by the MPU6050's FIFO. 

## Software Required
1. [PlatformIO](https://platformio.org/) Extension on VSCode.
2. [Processing](https://processing.org/download).

## Hardware Connections
1. The MPU6050's VCC and GND pins have been connected to the 3.3v and GND pins of the NodeMCU.
1. The MPU6050's SCL and SDA pins have been connected to D2 and D1 of the NodeMCU respectively.
1. The MPU6050's INT pin is connected to D5 on the NodeMCU
1. The MPU6050's AD0 pin may be left unconnected or connected to GND on the NodeMCU to ensure that the I2C address remains 0x68. Incase the AD0 pin is connected to high this address changes to 0x69 and changes need to be made to the main.cpp file. The ADO pin was left unconnected during my tests.