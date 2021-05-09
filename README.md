# Hardware-Software-Platforms---Ultrasound-Sensor
Project of the MA1 course Hardware/Software Platforms (UMONS).

## Explanations of the project
This project consists in the creation of a tutorial to retrieve the values of an ultrasonic sensor via an FPGA board with an I2C structure. This project was done as part of the Hardware and Software course at the Faculty of Engineering of Mons. This project allows to make links between software development and the use of hardware. 
To do this, the available files make it possible to understand the operation of the I2C and interrupts by using a WHAT CHIP ? chip and an SRF02 distance sensor.</div>

Here's a first scheme to understand the general structure of the project :

<img width="710" alt="image" src="https://user-images.githubusercontent.com/83776433/117567011-3c7a8480-b0ba-11eb-8c25-865353123c6c.png">

The state machine controls the I2C block. We use two registers to communicate with the I2C driver: DEVICE and ADDR. The ADDR register contains the different values we want to write and the DEVICE register contains the I2C address of the sensor. The I2C driver communicates with the sensor via the SDA and SCL ports.
