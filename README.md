# Hardware-Software-Platforms---Ultrasound-Sensor
Project of the MA1 course Hardware/Software Platforms (UMONS).
This file contains all the explanations of the project. It explains what we have to do to use the ultrasound sensor SRF02.

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

<img width="936" alt="Capture d’écran 2021-05-19 à 08 58 56" src="https://user-images.githubusercontent.com/83776433/118769426-73058b80-b880-11eb-9404-ce4b8b5c0674.png">

The I2C driver is a well-known part of this project, we can easily find informations on the Internet. The state machine helps us to understand the code we used in Altera Quartus.


# Steps to run our project
1. Open the progect Altera Quartus with the good golden (the golden is the quartus project correspondong to the chip we use). In our case, we use the chip DE0_nano_SoC. More informations about this chip can be found here : https://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&CategoryNo=167&No=941
2. Create a BLOC file (.vhd file). We descibe in this bloc all the registers we want to use. In our case, we only need one register out to read the sensor's values. We also descibe the I2C structure into this file BLOC.
3. We need to specify the registers we use in the ghrd.v file and our bloc. By the way, this file ghrd is the top file of our project. In the ghrd file, we specify "My wires" : wire [7:0] reg_out_to_bloc; .reg_out_external_connection(reg_out_to_bloc) dans la partie soc_system u0 (), et une partie de code qui correspond à notre bloc de base.
4. We need to make connections to create a link between the codes. To do that, we go in tools -> Platform Designer, we load our project, then we look for "parallel" in the search bar. We double-click on parallel I/O and we can add registers (input or output).


# Ultrasound Captor

The register to read the values of our capter is Software Revision and its location is 0. Then we use the register 0 and the command 0x51. This command is an activation commande, it starts the mesure and reads the data in centimeters. We need 16 bits (2 bytes) to read the data : the high byte (0x02) and the lower byte (0x03). We combine these two mesures to obtain the resulting value.

The writing sequence is : 


![writing](https://user-images.githubusercontent.com/83776433/118824406-1de66b80-b8ba-11eb-8e38-000f55f64f75.png)

and the reading sequence is :

<img width="975" alt="Capture d’écran 2021-05-19 à 16 04 41" src="https://user-images.githubusercontent.com/83776433/118826610-ed073600-b8bb-11eb-983f-49ed5cd46112.png">

Our simulation shows the different states :

![s1](https://user-images.githubusercontent.com/83776433/118925969-e28e8000-b93f-11eb-8d58-ab76e4e2fcfd.png)
![s2](https://user-images.githubusercontent.com/83776433/118926046-f803aa00-b93f-11eb-9954-cceea8a6b755.png)
![s3](https://user-images.githubusercontent.com/83776433/118926148-26818500-b940-11eb-81f0-b0189a4bce2d.png)
![s4](https://user-images.githubusercontent.com/83776433/118926211-3b5e1880-b940-11eb-8413-7deb2a5c9657.png)


# Video

https://youtu.be/KhrLss_JTB4


