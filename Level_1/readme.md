# Level-1: Introduction to Verilog RTL design and Synthesis

## List of Objectives

- :book: <b>Learning Objective-1:</b> [Introduction to iverilog simulaor](#book-Introduction-to-iverilog-simulator)
- :dart: <b>Practiccal Objective-1:</b> [Lab using iverilog and gtkwave](#dart-Lab-using-iverilog-and-gtkwave)
   - :microscope: <b>Lab-1:</b> [Clone SKY130 open source process design kit(PDK) on Ubuntu VM as test file library](#microscope-lab-1-clone-sky130-open-source-process-design-kitpdk-on-ubuntu-vm-as-test-file-library)
   - :microscope: <b>Lab-2:</b> [ Simulate a RTL design using iverilog](#microscope-lab-2-simulate-a-rtl-design-using-iverilog-test-design-21-mux-verilog-file-named-as-good_muxv)
   - :microscope: <b>Lab-3:</b> [ Read and edit (editing process only) verilog file using text editor](#microscope-lab-3-read-and-edit-editing-process-only-verilog-file-using-text-editor-observe-the-verilog-code-syntax-for-test-design-21-mux-verilog-file-named-as-good_muxv)
- :book: <b>Learning Objective-2:</b> [Introduction to Yosys and Logic synthesis](#book-Introduction-to-Yosys-and-Logic-synthesis)
- :dart: <b>Practical Objective-2:</b> [Labs using Yosys and SKY130 PDK](#dart-lab-using-yosys-and-sky130-pdk)
    - :microscope: <b>Lab-4:</b> [Synthesize a design using Yosys and SKY130 PDK (Test design: 2:1 MUX (Verilog file named as "good_mux.v"))](#microscope-lab-4-synthesize-a-design-using-yosys-and-sky130-pdk-test-design-21-mux-verilog-file-named-as-good_muxv)

 <div align="center">:star::star::star::star::star::star:</div> 
 
## :book: Introduction to iverilog simulator

### :bulb: Simulator
   - RTL design is checked for matching with the specification by simulating the design.
   - The tool used for `simulating the design` is known as `simulator`.
   - `Icarus Verilog (iverilog)` is an example of simulator.
 
---
### :bulb: Design
   - Design is the actual verilog code or set of verilog codes which has the intended functionality to meet with the required specification.
   - Written in hardware description language (HDL) like Verilog.
   - Functional verification is used to validate the RTL design.
---
### :bulb: Testbench
   - Testbench is the setup to apply stimulus `(test_vectors)` to the design to check its functionality.
   - It is the integration the `Design`, `Stimulus generator`, `Stimulus observer`.
   - `Stimulus generator` give `primary inputs` to the design under test (DUT).
   - `Stimulus observer` take `primary outputs` from the design under test (DUT).
   - Testbench has no primary inputs or outputs.
---
### :bulb: How Simulator Works
   - Simulator looks for the changes in input values.
   - Output is evaluated based on the change of input `(if no change in input, no change in output)`.
     
     ![testbench_img](images/tb_rv.png)  
---
### :bulb: Iverilog Based simulation flow
   1. Design and testbench files are given to iverilog simulatior.
   2. iverilog simulator generate .vcd file.
   3. .vcd file is given to gtkwave.
   4. gtkwave helps to visualize the input-output waveform (timing diagram).
      
   ![iverilog_flow](images/iv_sim_flow.png)

  <div align="center">:star::star::star::star::star::star:</div> 

## :dart: Lab using iverilog and gtkwave 
 ### :microscope: Lab-1: Clone SKY130 open source process design kit(PDK) on Ubuntu VM as test file library
   
   :zap: Open the Ubuntu terminal and clone the SKY130 PDK repository using the following command-
     
   ```
   $ git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
     
   ```
   :zap: Go to the Workshop directory cloned recently-
   ```
   $ cd sky130RTLDesignAndSynthesisWorkshop
   ```
   :zap: Here all test verilog files and standard cell libraries are available-
   - Check test verilog files-
   ```
   $ cd verilog_files
   $ ls
   ```
   ![test_verilog_files](images/ts_ver.png)
   
   - Check Standard cell library-
   ```
   $ cd lib
   $ ls
   ```
   ![standard_cell](images/std_cell.png)
   
  ### :microscope: Lab-2: Simulate a RTL design using iverilog (Test design: 2:1 MUX (Verilog file named as "good_mux.v"))
  :zap: Go to verilog_files directory-
  ```
  $ cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
  ```
  :zap: Give the design file "good_mux.v" and testbench file"tb_good_mux.v" to iverilog for compiling-
  ```
  $ iverilog good_mux.v tb_good_mux.v
  ```
  ![iverilog_log](images/iverilog_log.png)
  
  :zap: An executable file a.out is generated.Now execute this file-
  ```
  $ ./a.out
  ```
  ![a_out_log](images/a_out_log.png)
  
  :zap: A `.vcd file` is produced named as "tb_good_mux.vcd".Give this file to GTKWave-
  ```
  $ gtkwave tb_good_mux.vcd
  ```
  ![gtkwave_op](images/gtkwave_op.png)
    
  ### :microscope: Lab-3: Read and edit (editing process only) verilog file using text editor (Observe the verilog code syntax for Test design: 2:1 MUX (Verilog file named as "good_mux.v"))
  :zap: Open verilog files on gvim text editor ('-o' is used to open multiple files in same window)-
  ```
  $ gvim good_mux.v tb_good_mux.v -o  
  ```
  ![verilog_file_text](images/text_vim.png)
  
   :zap: Analysis of the design `good_mux.v`-

   - It has `i0,i1,sel` three primary inputs.
   - It has `y` as the primary output.
   - Ports are declared after module keyword.
   - `MUX functionality` is coded in the body (Inside module and endmodule).
  
  :zap: Analysis of the testbench `tb_good_mux.v`-

   - It has no primary inputs or primary outputs.
   - Design 'good_mux' is instantiated in this testbench.
   - Stimulus to the design are generated.
   - Primary outputs from design under test `(DUT)` or unit under test `(UUT)` are dumped into `.vcd file` as per the variation of primary inputs to UUT.
  
  :zap: Edit file in gvim text editor-

   - Press `i` to enter into the `insert` mode
   - Press `Esc` to enter into the `normal` mode
   - `:w` for saving the file
<div align="center">:star::star::star::star::star::star:</div> 
 
## :book: Introduction to Yosys and Logic synthesis

### :bulb: Synthesizer
   - RTL design to gate level design.
   - RTL design is the behavoural representation of the required specification.
   - Gate level design means representation of the required specification as the connection of logic gates.
   - `Netlist` is the file which includes the required locgic gates and connections between gates after synthesizing.
   - The tool used for synthesizing the RTL design is known as synthesizer.
   - `Yosys` is an example of open source synthesizer.
  
---
### :bulb: Yosys based synthesis flow
   - Start yosys
   - `.lib file` is given to yosys.
   - `.v design file` is given to yosys
   - Top module is synthesized as interconnection of logical block.
   - Logical blocks/gates are translated to standard cells from process design kit (PDK) libray.
   - Netlist is generated.
   - The netlist is also simulated using iverilog with the `RTL design testbench` to prevent `synthesis-simulation mismatch`.

   ![yosys_flow](images/yosys_flow.png)
    
---
### :bulb: `.lib` file
   - `.lib` file is the collection of logical modules (blocks or gates).
   - Logic gates like `and, or, not` and blocks like `mux, or_and_invert,D flip-flop` etc.
   - There are different flavors of same gate `slow`, `medium`, `fast`.
   - Here we are using `sky130_fd_sc_hd__tt_025C_1v80.lib` open source library.
---
### :bulb: Reason for different flavours of gate

   ![fast_cell](images/fast_slow_cell.png)

- #### Why fast cell ?
  - Combinational delay in logic path determines the maximum speed of digital logic circuit.
    
   ![fast_cell_1](images/fast_cell_1.png)
  - We need faster cells to make T<sub>comb</sub> small and thus increase mcircuit speed.
  - We can understand `setup time` with the train boarding analogy that we have to go to the station some time before the departure of the train.
  - Setup time is the time duration before clock edge from which the data should be stable in D flip-flop data input port.
  - Used for preventing Setup time violation and critical path issues.
- #### Why slow cell ?
  
  - Reliable data flow (launch and capture) between flip-flops.
    
   ![slow_cell](images/slow_cell_1.png)
  - We need faster cells to make T<sub>comb</sub> small and thus increase mcircuit speed.
  - Suppose DFF-A launch data in a clk-edge and DFF-B receive that data in next clk-edge.
  - DFF-B should not receive the new data of DFF-A in clk-edge-1.DFF-B should receive clk-edge-0 data of DFF-A in clk-edge-1.
  - DFF-A propagation delay (T<sub>CQ_A</sub>) and T<sub>comb</sub> are used to slow the DFF-A new data to reach the DFF-B in same clock edge.
  - Hold time is the time duration after clock edge till which the data should be stable in D flip-flop data input port.
  - Used for preventing hold time violation.
    
  ![slow_cell_2](images/slow_cell_2.png)
---    
### :bulb: Problems with fast cell and slow cell
  - Capacitence is the load in digital circuit
  - Faster charging or discharging of capacitance  means smaller the cell delay.
  - For faster charging/discharging, we need transistors capable of sourcing more current (wide transistors).
  - For the slower cells narrow transistors so power and are less.
  - #### Fast cell problem
    - Wide transistors
    - More area, more power
    - Hold time violation
  - #### Slow cell problem
    - Sluggish circuit
    - More delay
    - Setup time violation
### :bulb: Selection of cells
  - Guidance by the user in terms of `constraints` for selecting cells as per requirement.
 
<div align="center">:star::star::star::star::star::star:</div> 
 
## :dart: Lab using Yosys and SKY130 PDK 
 ### :microscope: Lab-4: Synthesize a design using Yosys and SKY130 PDK (Test design: 2:1 MUX (Verilog file named as "good_mux.v"))
   
   :zap: Go to verilog_files directory-
   ```
   $ cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
   ```
   :zap: Start yosys-
   ```
   $ yosys
   ```
   ![yosys](images/yosys.png)

   :zap: Give the `.lib` file to yosys for checking the availavle cells-
   ```
   $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
   ![read_lib](images/read_lib.png)
   
   :zap: Give the `.v` file `good_mux.v` to yosys for reading the design-
   ```
   $ read_verilog good_mux.v
   ```
   ![read_ver](images/read_ver.png)
   
   :zap: Specify the module `good_mux` which to be synthesized as root design-
   ```
   $ synth -top good_mux
   ```
   ![synth](images/synth.png)
   
   :zap: Generate the netlist for the design using the standard cell library-
   ```
   $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
   ![abc](images/abc.png)

   :zap: Visualize the synthesized design-
   ```
   $ show
   ```
   ![show](images/show.png)

   :zap: Write the netlist as `.v` file `good_mux_net.v` with or without attribute (use only one)-
   ```
   $ write_verilog good_mux_net.v
   $ write_verilog -noattr good_mux_net.v
   ```
   ![write_ver](images/write_ver.png)
   
   :zap: Read the netlist-
   ```
   $ !gvim good_mux_net.v
   ```
   ![net_vim](images/net_vim.png)

   <div align="center">:star::star::star::star::star::star:</div> 
   
## :trophy: Level Status: 

- All objectives completed.
- I have learned simulation using iverilog,GTKWave (for timing diagram viewing) and synthesis using Yosys and SKY130 PDK.
- 🔓 Next level unlocked 🔜 [Level-2(Day-2): Timing libraries,hierarchial vs flat synthesis, efficient flip-flop coding styles](../Level_2/readme.md).


