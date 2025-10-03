# Level-2: Practical understanding of BabySoC structure and simulation results

## List of Objectives

- :microscope: <b>Practical Objective-1:</b> []()
- :microscope: <b>Practical Objective-2:</b> []()
- :microscope: <b>Practical Objective-3:</b> []()
 

 <div align="center">:star::star::star::star::star::star:</div> 
 
## :microscope: Setup the directory `VSDBabySoC`
   
   :zap: Open terminal and clone the project directory-

   ```
   $ git clone https://github.com/manili/VSDBabySoC.git

   ```
   ![set_clone](images/set_clone.png)
     
   :zap: Go to `src` directory and observe the nested directory -
   
   ```
   $ cd VSDBabySoC/src
   $ ls

   ```
   ![set_src](images/set_src.png)
   
   :bulb: `include` (header files) and `module` (design files) directories have the required files for `babysoc` simulation.
   
   :zap: Go to the `module` directory-

   ```
   $ cd module
   $ ls
   ```
   ![set_mod](images/set_mod.png)

   :bulb: `vsdbabysoc.v`, `rvmyth.tlv`, `avsddac.v`, `avsdpll.v`, `testbench.v` are the required files for simulation.

   :bulb: This is our working directory.

   :bulb: `.tlv` file is used for easy pipeline design, timing abstraction and transaction level modeling than the plain verilog.

   :bulb: We can observe the pipelined design of `RVMYTH core` from `rvmyth.tlv` file using [https://makerchip.com/sandbox/#](https://makerchip.com/sandbox/#)

   ![set_tlv](images/set_tlv.png)
   
   :warning: Here `rvmyth.tlv` can not be compiled using iverilog. 

   <div align="center">:star::star::star::star::star::star:</div> 
   
  ### :microscope: Convert `rvmyth.tlv` to `rvmyth.v`
  
  :dart: Install `sandpiper-saas` compiler to convert `.tlv` to `.v`-

  :zap: Virtual environment setup for pip install `sandpiper-saas` in home directory-
   
   ```
   $ mkdir sandpiper_env
   $ cd sandpiper_env
   $ python3 -m venv venv 
   ```
   ![venv_1](images/venv_1.png)
   
  :zap: Activate the virtual environment-

   ```
   $ source venv/bin/activate
   ```

  ![venv_2](images/venv_2.png)

  :zap: Install `sandpiper-saas`-

   ```
   $ pip install sandpiper
   ```

  ![venv_3](images/venv_3.png)

  :zap: Go to working directory-

  ```
  $ cd ../VSDBabySoC/src/module
  ```
  :dart: Convert `rvmyth.tlv` to `rvmyth.v`-
  
   ```
   $ sandpiper-saas -i rvmyth.tlv -o rvmyth.v
   ```

  ![venv_4](images/venv_4.png)

  :bulb: `rvmyth.v` and `rvmyth_gen.v` files are generated after compilation.

  :warning: Comment out the lines like <mark> ```line 2 "rvmyth.tlv" 0 </mark> in `rvmyth.v` file to prevent compile time error.

  <div align="center">:star::star::star::star::star::star:</div> 
     
  ### :microscope: Lab-3: Compare area,power of variants of same cell
  :zap: We have opened three different flavours of same cell using line number-
  ```
  :36663
  :vsp
  :vsp
  :36904
  :37145
  ```
  ![cell_comp](images/cell_comp.png)
  
   :zap: Compare three cells-

   - `and2_0`,`and2_1`,`and2_2` cells are opened.
   - Area is increasing from `and2_0` to`and2_2`.
   - Speed is increasing from `and2_0` to `and2_2`.
   - Power is increasing from `and2_0` to `and2_2`.
     
  <div align="center">:star::star::star::star::star::star:</div> 
 
## :dart: Lab on Hierarchial vs Flatten synthesis
 ### :microscope: Lab-4: Hierarchial synthesis
   
  :zap: Synthesize `multiple_modules.v` as hierarchial-
     
   ```
  $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ read_verilog multiple_modules.v
  $ synth -top multiple_modules
  ```
  ![hier_synth_1](images/hier_synth_1.png)
  
  ```
  $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ show
  ```
  ![hier_synth_2](images/hier_synth_2.png)

  ```
  $ write_verilog multiple_modules_net.v 
  ```

   ![hier_net_v](images/hier_net_v.png)
   
   ### :microscope: Lab-5: Flat synthesis
   
  :zap: Synthesize `multiple_modules.v` as flatten-
     
   ```
  $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ read_verilog multiple_modules.v
  $ synth -top multiple_modules
  $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ flatten
  $ show
  ```
  ![flat_synth_1](images/flat_synth_1.png)

  ```
  $ write_verilog multiple_modules_flat.v 
  ```

   ![flat_net](images/flat_net.png)
   
 
  ### :microscope: Lab-6: Compare hierarchical and flat synthesis
  :zap: Hierarchial vs Flat netlist
   ```
   $ gvim multiple_modules_hier.v
   :vsp
   :sp multiple_modules_flat.v
   :exit
   ```
   ![comp_flat_hier](images/comp_flat_hier.png)

  :bulb: Significance of `synth -top`-

  - If a submodule is instantiated multiple times the multiple time synthesis of same submodule is problematic.
  - We can synthesize submodule one time and use this multiple time.
  - This is the significance of `synth -top`-
    
    ```
    synth -top `submodule_name`
    ```

 <div align="center">:star::star::star::star::star::star:</div>   
  
## :dart: Labs on flip-flop design,simulation,synthesis and optimization
 ### :microscope: Lab-7: Analyze different flip-flop designs 
 
   :zap: Open different D flip-flop reset type designs -
   ```
   $ gvim dff*syn*s.v -o
   ```
   ![dff_res](images/dff_res.png)
   
   :zap: Analysis of reset type flip-flop verilog code-

   - D-flipflops ,so `posedge clk` in sensitivity list.
   - When asynchronous reset high then, output of D flip-flop is set to zero immediately,no change on `clk` edge.
   - When synchronous reset high then, output of D flip-flop is set to zero on next positive `clk` edge.
   - For asynchronous reset `posedge reset` in sensitivity list also.
   - For synchronous reset `posedge clk` in sensitivity list only.
   - Non-blocking assignments are used inside `always` block.
     
  :zap: Open different D flip-flop reset type designs -
   ```
   $ gvim dff_async_set.v
   ```
        
   ![dff_set](images/dff_set.png)  
   
   :zap: Analysis of reset type flip-flop verilog code-

   - D-flipflops ,so `posedge clk` in sensitivity list.
   - For asynchronous reset `posedge reset` in sensitivity list also.
   - When asynchronous eset high then, output of D flip-flop is set to one immediately,no change on `clk` edge.
   - 
### :microscope: Lab-8: Simulate different flip-flop designs 
:zap: Simulate `dff_asyncres.v` using iverilog-

```
$ iverilog dff_asyncres.v tb_dff_asyncres.v
$ ./a.out
$ gtkwave tb_dff_asyncres.vcd
```
![w_dff_ares](images/w_dff_ares.png)

:zap: Simulate `dff_syncres.v` using iverilog-

```
$ iverilog dff_syncres.v tb_dff_syncres.v
$ ./a.out
$ gtkwave tb_dff_syncres.vcd
```
![w_dff_sres](images/w_dff_sres.png)

:zap: Simulate `dff_async_set.v` using iverilog-

```
$ iverilog dff_async_set.v tb_dff_async_set.v
$ ./a.out
$ gtkwave tb_dff_async_set.vcd
```
![w_dff_aset](images/w_dff_aset.png)

### :microscope: Lab-9: Synthesize different flip-flop designs   
:zap: Synthesize `dff_asyncres.v` using Yosys and SKY130 PDK-

```
$ yosys
$ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ read_verilog dff_asyncres.v
$ synth -top dff_asyncres
```

![s_dff_ares_1](images/s_dff_ares_1.png)

```
$ dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![s_dff_ares_2](images/s_dff_ares_2.png)

```
$ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ show
```

![s_dff_ares_3](images/s_dff_ares_3.png)

:bulb: In the library D flip-flops has `active low` reset, but we designed `active high` reset. So reset signal is passed through an inverter before connecting to the reset port of D flip-flop.

```
$ write_verilog -noattr dff_asyncres_net.v
$ !gvim dff_asyncres_net.v
```

![s_dff_ares_4](images/s_dff_ares_4.png)

:zap: Synthesize `dff_syncres.v` using Yosys and SKY130 PDK-

```
$ yosys
$ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ read_verilog dff_syncres.v
$ synth -top dff_syncres
$ dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ show
```

![s_dff_sres_1](images/s_dff_sres_1.png)

```
$ write_verilog -noattr dff_syncres_net.v
$ !gvim dff_syncres_net.v
```

![s_dff_sres_2](images/s_dff_sres_2.png)

:zap: Synthesize `dff_async_set.v` using Yosys and SKY130 PDK-

```
$ yosys
$ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ read_verilog dff_async_set.v
$ synth -top dff_async_set
$ dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ show
```

![s_dff_aset_1](images/s_dff_aset_1.png)

```
$ write_verilog -noattr dff_async_set_net.v
$ !gvim dff_async_set_net.v
```

![s_dff_aset_2](images/s_dff_aset_2.png)

### :microscope: Lab-10: Interesting synthesis optimization (No haedware block generate)
:zap: `mult_2.v` design -

```
$gvim mult_2.v
```

![mult_2_des](images/mult_2_des.png)

:zap: Synthesize `mult_2.v` and observe the optimization-

```
$ yosys
$ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ read_verilog mult_2.v
$ synth -top mul2
$ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ show
```

![mult_2_synt](images/mult_2_synt.png)

:bulb: No hardware block generated

:bulb: 3 bit number multipliesd with 2 results 4 bit number first three bits from MSB of result is same as 3 bit number and LSB is zero.

:zap: `mult_8.v` design -

```
$gvim mult_8.v
```

![mult_8_des](images/mult_8_des.png)

:zap: Synthesize `mult_8.v` and observe the optimization-

```
$ yosys
$ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ read_verilog mult_8.v
$ synth -top mult8
$ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$ show
```

![mult_8_synt](images/mult_8_synt.png)

:bulb: No hardware block generated.

:bulb: 3 bit number multipliesd with 9 results 6 bit number where the 3 bit number repeats two times.


   <div align="center">:star::star::star::star::star::star:</div> 
   
## :trophy: Level Status: 

- All objectives completed.
- I have learned about `.lib`, hierarchial vs flat synthesis , flop design, simulation, synthesis and some interseting optimization.
- :white_check_mark: Map Completed.



