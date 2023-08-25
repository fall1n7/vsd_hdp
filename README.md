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
   * Selection of cells - synthesis constraints
   * PVT Corners
   * Informations in .lib file
   * Hierarachial vs Flat synthesis
   * Why flipflops?
   * Custom Optimisation
  
</details>

<details>
 <summary> Synthesis </summary>

 The Synthesis was performed using the following code
  
 + commands used - Synthesis `code`
  ```bash
  yosys> read_liberty -lib <path to lib file>
  yosys> read_verilog <path to verilog file>
  yosys> synth -top <top_module_name> 
  yosys> abc -liberty <path to lib file>
  yosys> show
  ```
Synthesis Result 

 ![Screenshot from 2023-08-21 19-26-36](https://github.com/fall1n7/vsd_hdp/assets/140475909/0bcf86e4-bed3-4c99-9ae8-42107faccd54)

Netlist 

 ![Screenshot from 2023-08-25 14-55-25](https://github.com/fall1n7/vsd_hdp/assets/140475909/92606e13-92e6-493d-a4b4-59ac96c935f8)


Flat version of synthesis

+ commands used - Synthesis `code`
 ```bash
yosys> flatten
yosys> write_verilog -noattr <file name>
```
Synthesis Result 

 ![Screenshot from 2023-08-25 14-59-08](https://github.com/fall1n7/vsd_hdp/assets/140475909/c79944aa-fbbd-4b6f-86ef-85c17050eeed)

Netlist 

 ![Screenshot from 2023-08-25 15-01-49](https://github.com/fall1n7/vsd_hdp/assets/140475909/fab1abe4-18a8-43f6-b146-bffd72a47af0)

</details>


<details>
 <summary> Synthesis - Submodule Level </summary>

The Sub-Module level Synthesis was performed using the following code

+ commands used - Synthesis `code`
  ```bash
  yosys> read_liberty -lib <path to lib file>
  yosys> read_verilog <path to verilog file>
  yosys> synth -top <Sub_module_name> 
  yosys> abc -liberty <path to lib file>
  yosys> show
  ```

Sub_Module-1 Synthesis Result 

 ![Screenshot from 2023-08-25 15-15-54](https://github.com/fall1n7/vsd_hdp/assets/140475909/ad9ad7e7-94b4-4999-a126-406681d9e6af)

Sub_Module-2 Synthesis Result

 ![Screenshot from 2023-08-25 15-17-47](https://github.com/fall1n7/vsd_hdp/assets/140475909/4772087c-cd31-42fb-87ba-f12708d9ca80)

</details>

<details>
 <summary> Simulation of Asynchronous Reset </summary>


 


 


 



       
 






