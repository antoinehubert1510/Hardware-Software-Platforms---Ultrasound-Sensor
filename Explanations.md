# Explanations step by step

## Dor this project, we need
1) Altera Quartus
2) soc EDS
3) PuTTY
4) a chip DE0_nano_SoC
5) an ultrsound sensor SRF02

## Altera Quartus
1) Install Altera Quartur (last version, pro or lite).
2) Find the DE0soc golden to start a new project.
3) Double-click on "soc_system.qsf". A Quartus window opens. The top-level entity is the file ghrd.v.
4) Create a BLOC file, which is vhdl. Define all the connections, the clock and the sda. (see BLOC.vhd)
5) Complete the ghrd file with the connections from BLOC, as shown in the code ghrd.v.
6) Add an I2C protocol in the BLOC file (see BLOC.vhd).
7) Go to Tools -> Platform Designer.

## Platform Designer
1) Load the file of the project.
2) Search "parallel" in the search bar, and double-click on PIO (Parallel I/O) Intel FPGA IP.
3) Add the input and output registers we created in the Bloc file, rename it and modify the base for every new register (ex: if REG1 =0x0000 0010, REG2 must be 0x0000 0020 ...).
4) Make the connections of the clock, the reset and s1 as shown below :

<img width="1142" alt="Capture d’écran 2021-05-20 à 09 01 43" src="https://user-images.githubusercontent.com/83776433/118933878-00f97900-b94a-11eb-8e8f-30ff2183822e.png">

5) Click on "Generate HDL"
6) Once it is done, go back to Altera Quartus and compile all the files.

## C code
To mahe the sensor work, we need to implement a C code. We will be able to know the distances with this code.

1) Open soc EDS, this is a command window.
2) Navigate trough you files to reach the project's folder.
3) Enter the command "./generate_hps_qsys_header.sh", this will generate the .h file.
4) Complete the C file as the main.c file.

## Other steps
To access the board using the USB port (serial communication), we use PuTTY. With PUTTY, we can connect to the board and use the terminal to see the execution of the program running on the ARM processors. Any printf on the program will appear on that terminal.

1) Install PuTTY.
2) Select "serial".
3) Enter a speed of 115200.
4) Find the good serial line (ex: COM16). In order to do that, go on "gestionnaire de périphériques" and check the serial line COMXX of the board.
5) Click "open", a command window is opening.
6) Start the chip. Linux installed on the SD card will run.
7) Put the C code on the chip.

Last but not least, we need to put the VHDL code on the FPGA.

1) Go on Quartus.
2) Click on the button "Programmer" (the button circled in a red square).

![Quartus-II-Development-Environment-from-Altera](https://user-images.githubusercontent.com/83776433/118959218-68bbbe00-b962-11eb-9f57-33a97dec61fd.png)
