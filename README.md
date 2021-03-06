# Hardware-Software-Platforms---Ultrasound-Sensor
Project of the MA1 course Hardware/Software Platforms (UMONS).
This file contains all the explanations of the project. It explains what we have to do to use the ultrasound sensor SRF02.

Hello! We are two students of the Faculty of Engineering of the university of Mons (UMONS). This is our 4th year here, and we have a project for the course Hardware/Software. We specialise in Electrical Energy and Smart Grids.

The aim of this project is to implement an interface between a sensor and a computer through an FPGA. Some details about this project are available just below, but don't worry, there are many other informations in the Explanations.md file. You can find by the end of this document the link trough the project's video, hope you enjoy ;)

If you want to contact us for further informations, please find our names and adresses just here :

Antoine Hubert : antoine.hubert@student.umons.ac.be
Maxime Renard : maxime.renard@student.umons.ac.be

## Explanations of the project
This project consists in the creation of a tutorial to retrieve the values of an ultrasonic sensor via an FPGA board with an I2C structure. This project was done as part of the Hardware and Software course at the Faculty of Engineering of Mons. This project allows to make links between software development and the use of hardware. 
To do this, the available files make it possible to understand the operation of the I2C and interrupts by using a DE0_nano_SoC chip and an SRF02 distance sensor.</div>

Here's a first scheme to understand the general structure of the project :

<img width="710" alt="image" src="https://user-images.githubusercontent.com/83776433/117567011-3c7a8480-b0ba-11eb-8c25-865353123c6c.png">

The state machine controls the I2C block. We use two registers to communicate with the I2C driver: DEVICE and ADDR. The ADDR register contains the different values we want to write and the DEVICE register contains the I2C address of the sensor. The I2C driver communicates with the sensor via the SDA and SCL ports.

A C-code will be used to read all the values of distances from the sensor. The sensor data is placed by the control code on the output register (REG_OUT).

## State Machine

![state_machine](https://user-images.githubusercontent.com/83776433/118927038-84629c80-b941-11eb-9071-e70e7fad57a6.png)



## I2C driver

<img width="936" alt="Capture d???e??cran 2021-05-19 a?? 08 58 56" src="https://user-images.githubusercontent.com/83776433/118769426-73058b80-b880-11eb-9404-ce4b8b5c0674.png">

The I2C driver is a well-known part of this project, we can easily find informations on the Internet. The state machine helps us to understand the code we used in Altera Quartus.


# Ultrasound Captor

The register to read the values of our capter is Software Revision and its location is 0. Then we use the register 0 and the command 0x51. This command is an activation commande, it starts the mesure and reads the data in centimeters. We need 16 bits (2 bytes) to read the data : the high byte (0x02) and the lower byte (0x03). We combine these two mesures to obtain the resulting value.

The writing sequence is : 


![writing](https://user-images.githubusercontent.com/83776433/118824406-1de66b80-b8ba-11eb-8e38-000f55f64f75.png)

and the reading sequence is :

<img width="975" alt="Capture d???e??cran 2021-05-19 a?? 16 04 41" src="https://user-images.githubusercontent.com/83776433/118826610-ed073600-b8bb-11eb-983f-49ed5cd46112.png">

Our simulation shows the different states :

![s1](https://user-images.githubusercontent.com/83776433/118925969-e28e8000-b93f-11eb-8d58-ab76e4e2fcfd.png)
![s2](https://user-images.githubusercontent.com/83776433/118926046-f803aa00-b93f-11eb-9954-cceea8a6b755.png)
![s3](https://user-images.githubusercontent.com/83776433/118926148-26818500-b940-11eb-81f0-b0189a4bce2d.png)
![ModelSim_s4](https://user-images.githubusercontent.com/84465380/118986233-73d11700-b97f-11eb-8322-77ca6aaa0cd7.PNG)


# Video

https://youtu.be/KhrLss_JTB4


