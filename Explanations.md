# Explanations step by step

## Dor this project, we need
1) Altera Quartus
2) soc EDS
3) PuTTY
4) a chip DE0_nano_SoC
5) an ultrsound sensor SRF02

## Altera Quartus
1) Install Altera Quartur (last version, pro or lite)
2) Find the DE0soc golden to start a new project.
3) Double-click on "soc_system.qsf". A Quartus window opens. The top-level entity is the file ghrd.v.
4) Create a BLOC file, which is vhdl. Define all the connections, the clock and the sda. (see BLOC.vhd)
5) Complete the ghrd file with the connections from BLOC, as shown in the code ghrd.v.
6) Add an I2C protocol in the BLOC file (see BLOC.vhd)
7) Go to Tools -> Platform Designer

## Platform Designer
1) Load the file of the project
2) Search "parallel" in the search bar, and double-click on PIO (Parallel I/O) Intel FPGA IP
3) Add the input and output registers we created in the Bloc file, rename it and modify the base for every new register (ex: if REG1 =0x0000 0010, REG2 must be 0x0000 0020 ...)
4) Make the connections of the clock, the reset and s1 as shown below :

<img width="1142" alt="Capture d’écran 2021-05-20 à 09 01 43" src="https://user-images.githubusercontent.com/83776433/118933878-00f97900-b94a-11eb-8e8f-30ff2183822e.png">

5) Click on "Generate HDL"
