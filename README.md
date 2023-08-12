# VSD_HDP

## The development of the **VSD-HDP** tapeout program is outlined in this github repository. 

## Contents

***
***
[Day 0](#day-0)
 
[Day 1](#day-1)

[Day 2](#day-2)

## Day 0

<details>
 <summary> Summary </summary>


  System/Tools setup. Installed all necessary tools and is shown below.

</details>	


<details>
 <summary> Yosys </summary>

 Installed Yosys using the commands specified in system check and tool installation document.

 `code`

  
  ``` zsh
  $ git clone https://github.com/YosysHQ/yosys.git
  $ cd yosys
  $ sudo apt install make (If make is not installed please install it) 
  $ sudo apt-get install build-essential clang bison flex \
      libreadline-dev gawk tcl-dev libffi-dev git \
      graphviz xdot pkg-config python3 libboost-system-dev \
      libboost-python-dev libboost-filesystem-dev zlib1g-dev
  $ make config-gcc
  $ make 
  $ sudo make install
  ```

Screenshot of tool launching

![Screenshot from 2023-08-11 16-23-16](https://github.com/fall1n7/vsd_hdp/assets/140475909/c172e242-3266-4af6-aa4b-bc75a234932c)

</details>	

<details>
 <summary> iVerilog </summary>

 Installed iVerilog using the commands specified in system check and tool installation document.

 `code`

  ```zsh

   sudo apt-get install iverilog

  ```
Screenshot of tool launching


![Screenshot from 2023-08-11 16-31-59](https://github.com/fall1n7/vsd_hdp/assets/140475909/72811e7a-cd13-4a99-9b7e-b34b8cf46787)


</details>	

<details>
 <summary> GTKwave </summary>

Installed gtkwave using the commands specified in system check and tool installation document.

 `code`

  ```zsh

   sudo apt install gtkwave

  ```
Screenshot of tool launching


![Screenshot from 2023-08-11 16-37-56](https://github.com/fall1n7/vsd_hdp/assets/140475909/44d9f725-a7cc-4932-b734-6b2f75fd1bfa)

</details>	

## Day 1

<details>
 <summary> Summary </summary>

 Introduction to Verilog RTL Design and Synthesis.

 + Brief introduction about on what is a simulator, Design, Verification Environment(Testbench) and Synthesis process.
   
    * The Design and the Testbench are the inputs to a Simulator(iverilog) which gives the output as a value change dump file(VCD) which is then read gtkwave
      to see the waveform and verify the functionality of the design.
    * The Design and the .lib are the inputs to the synthesizer(Yosys) which gives the output as netlist. The netlist is then compared with the testbench using
      iverilog to verify the functionality of the generated netlist.
    * Used an example of a 2:1 MUX for simulation and synthesis using iverilog and Yosys.

 </details>	

 <details>
  <summary> Design </summary>

 The verilog design and the library files were cloned from this repo : https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

 The example used in this module is good_mux.v

 </details>	

 <details>
  <summary> Simulation </summary>

 The simulation of the verilog file was done using iverilog and the vcd file is read using gtkwave followed by verification of the functionality of the design.
  + commands used `code`
  ```bash
  iverilog <name verilog: good_mux.v> <name testbench: tb_good_mux.v>
  ./a.out
  gtkwave tb_good_mux.vcd
  ```
  + Simulation Results
   ![Screenshot from 2023-08-10 12-22-01](https://github.com/fall1n7/vsd_hdp/assets/140475909/eaf8d3ea-5676-45e9-95d2-f0e3b941e287)

</details>

<details>
 <summary> Synthesis </summary>

 The synthesis was done using Yosys and netlist was generated. 
  + commands used - Synthesis `code`
  ```bash
  yosys> read_liberty -lib <path to lib file>
  yosys> read_verilog <path to verilog file>
  yosys> synth -top <top_module_name> 
  yosys> abc -liberty <path to lib file>
  yosys> show
  ```
  Synthesis Result
   ![Screenshot from 2023-08-10 23-25-53](https://github.com/fall1n7/vsd_hdp/assets/140475909/7621e845-d200-480a-95bb-e60c9392fc54)

  + Commands used - Netlist Generation  `code`
  ```bash
  yosys> write_verilog <file_name_netlist.v>
  yosys> write_verilog -noattr <file_name_netlist.v>
  ```
  Generated Netlist 
   ![Screenshot from 2023-08-10 23-53-26](https://github.com/fall1n7/vsd_hdp/assets/140475909/864e2d99-25fb-4658-982b-e60ada89a0de)

 </details>

 ## Day 2

 <details>
 <summary> Summary </summary>

 Introduction to timing.libs

 + Brief Introduction was given on the following:
   * What is a .lib file?
   * Why different flavours of standard cells are required?
   * What is setup time, hold time and timing violations
   * Faster vs Slower cells
   * Selection of cells - synthesys constraints
   * PVT Corners
   * Informations in .lib file
   

 


 



       
 






