# Level-1: Theoratical understanding of SoC and basic outline of BabySoC

## List of Objectives

- :book: <b>Learning Objective-1:</b> []()
- :book: <b>Learning Objective-2:</b> []()
- :book: <b>Learning Objective-3:</b> []()
- :book: <b>Learning Objective-4:</b> []()
- :book: <b>Learning Objective-5:</b> []()



 <div align="center">:star::star::star::star::star::star:</div> 
 
## :book: Introduction to System on Chip (SoC) 

### :bulb: Computer system overview
  :zap: Any computing system has some basic functions and some specialized functions.
      - `Basic functions` are processing , storage, Synchronization managemnet (clock), peripheral interface management , power management.
      - `Specialized functions` communication interface, secure data management, image/video/audio processing.

  :zap: Generally for high performance computing (Desktop computer) different chips or different hardware blocks are separate entities, these are connected together through wires.
  
---

### :bulb: System on Chip (SoC) overview

  Here, most or all components of a `computer system`  are integrated into a `single chip`.Basic SoC is made by integating processor, memory, peripheral interface, clock management, power management block onto a silicon die. Others hardware blocks can be integrated into the chip for specialized function. It is used to improve performance, reduce power consumption and physical space. 
  
   ![soc_over](Level_1/images/soc_over.png)

---
### :white_check_mark: SoC advantages
   - Reduce requirements of external ICs.
   - Smaller physical size and compact design.
   - Power efficient.
   - On chip communcation and less signal delay produce higher performance.
   - Cost effective as high-volume manufacturing lowers the cost.
   - Optimized for specific application.
---
### :warning: SoC disadvantages
   - Design become very complex.
   - Heat Dissipation issue is a very big problem in SoC.
   - Different `level of power supplies` to different hardware blocks is problematic.
   - No upgradability.
   - If any failure occurs in any block of SoC, it will affect the whole system and replacement of the SoC is the only option to solve this issue.
---
### :bulb: SoC application
   - Smartphones: Qualcomm Snapdragon.
   - Communication device: SoC in wifi router.
   - Automobile: Car infotainment control.
   - Industrial control systems.
   - Aerospace and defense.
   - Wearables and IoT systems: Smart watch, Amazon alexa.
   - AI and Edge computing.
   - Robotics.
   - Consumer electronics: Smart TV.
    
---

  <div align="center">:star::star::star::star::star::star:</div> 

## :book: Instruction Set Architecure (ISA)

## :bulb: Introduction to ISA

 :zap: ISA is a very important part of processor design. 
 
 :zap: It is very crucial in hardware software interfacing. 

 :zap: It give the rules which combinations of N- bit for which instruction.(N word length)

 :zap: ARM V7 ISA (Mobile device), AMD X86 ISA (Desktop computer).

  :zap: RISC-V gives open source instruction set architecture. 

 

## :bulb: Importance of ISA

:zap: If different procesing unit has different ISA designed by different companies then complexity increase.

:zap: It is the low level interface of hardware-software. Compiler maps high level language instructions to these instructions.

:zap: Open source ISA gives the oppurtunity to design different cores with the same ISA.It ease the design process.

 


## :book: Components of typical SoC

### :bulb: Processing Units
   :zap: <mark>Central Processing Unit (CPU) (Basic unit):</mark>
      - Usually it is a general purpose processor.
      - It has general fetch, decode, execute stages.
      - ALU (arithmetic and logic unit) operations, memory operations are performed by this.
        
   :zap: <mark>Graphics Processing unit (GPU) (Special unit):</mark>
      - Perform graphic rendering and parallel computing task.
      - Used for Virtual Games,images,videos.
        
   :zap: <mark>Digial Signal Processor (DSP) (Special unit):</mark>
      - Optimized processing of digital signals (audio, video, communications).
      - 
   :zap: <mark>AI/ML Accelerators (TPU) (Special unit):</mark>
      - Optimized processing of neural networks and machine learning tasks.
        
---

### :bulb: Memory Units

 Nowdays, Havard architecture is preferred, where program/instruction memory and data memory are different to avoid overwrite issue.
 
   :zap: <mark>On-chip SRAM (Static random access memory):</mark>
     - Used for cache.
     
   :zap: <mark>ROM (Read only memory):
      - For storing boot codes.
      
   :zap: <mark>DRAM controller:</mark>
      - Interface with external dynamic random access memory.

   :zap: <mark>Flash/NVM controller:</mark>
      - For program and data storage.
      
---

### :bulb: Peripheral interface Units

 Digital to analog converter (DAC) and Analog to Digital converter (ADC) are used for interfacing.
 
    :zap: <mark>I/O interfaces:</mark>
    
     - Universal serial Bus (USB).
     - Peripheral component interface express (PCIe).
     - HDMI,MIPI (Camera/display).
     - Universal Asynchronous  receiver and transmitter
     
    :zap: <mark>Storage interface:</mark>
    
      - eMMC, UFS, SD card.
      
    :zap: <mark>Serial interface:</mark>
    
      - Serial peripheral interface (SPI).
      - Controller area network (CAN).
      - Inter integrated circuit (I2C).
      - 
    :zap: <mark>Flash/NVM controller:</mark>
      - For program and data storage.

    :zap: <mark>GPIOs:</mark>
      - General purpose input output interface for control and signals.

---

### :bulb: Power and Synchronization management Units
 
  :zap: <mark>Power Management:</mark>
  
  - Buried rail power supply in transistor level is used to provide efficient power transfer line.
  - Clock gating is used for preventing leakege power loss.
  - Voltage regulation and level shifting are used for different block operating in different power supply.
  - Nowdays dynamic power control is used.
  
  :zap: <mark>Synchronization management:</mark>
  
  - Generally sequential logic is used. So,clock is very important.
  - Clock source (Crystal oscillator) used to generate clock.
  - Clock Global buffer used for synchronization in different location.
  - PLL is used to generate stable higher frequencies from source clock.
  - Divider is used to generate lower frequencies from source clock.

   :zap: <mark>Cache coherency logic:</mark>
   
  - Ensures data consistency across multiple cores.

      
   <div align="center">:star::star::star::star::star::star:</div> 

## :book: Intoduction to BabySoC : a simplified model of SoC

### :bulb: BabySoC outline
   :zap: BabySoC is integration of a `RVMYTH core` , a 10 bit DAC unit and a Phase locked loop (PLL).
   
      - `RVMYTH  core` is the CPU designed with RISC-V 32 bit integer Base Instruction Set Architecture (ISA).
      - A 10 bit DAC is used to convert 10 bit output to analog signal fro external interface.
      - A PLL is used for stable and accurate high frequency `CLK` generation from source clock.

 ---
      
### :bulb: Why simplified
:zap: It has small instruction and data memory.

:zap: It has a 5 stage pipelined CPU core.

:zap: It has 32 x 32 register file.

:zap: Wordlength is 32 bit.

:zap: RV32I BASE ISA used.

:zap: SoC has only CPU core, DAC, PLL no other external memory or special extension is given.

:zap: It is a very simplifed model interms of integration and simplified base ISA is used.

:zap: Simple program are hardcoded in instruction for easy simulation. Simulation is performed in the next level.


 <div align="center">:star::star::star::star::star::star:</div> 
 
## :book: Importance of functional modeling of SoC before RTL and physical design stages

### :bulb: Functional modeling of SoC
 :zap: Usually `RVMYTH core` is `digital` circuit, `DAC` and `PLL` are `analog` IPs. 
 :zap: It is used for behavioral validation.
 :zap: Non-synthesizable , no hardware generated.
 :zap: Instruction execution is observed.
 :zap: High level programming language is used for behavioral modeling.
 :zap: Untimed behaviour.
 :zap: Abstract variable instead of registers.

---

### :bulb: Functional modeling provide faster simulation than RTL modeling

---

### :bulb: It is a very good reference against RTL and Physical design verification

---

### :bulb: Why Functional modeling before physical design

 :zap: Physical design is very complex and time consuming task. To get required functionality and less error, functional modeling is used before physical design.

  <div align="center">:star::star::star::star::star::star:</div> 
  
## :trophy: Level Status: 

- All objectives completed.
- I have learned fundamental theories of SoC and BabySoc outline.
- 🔓 Next level unlocked 🔜 [Level-2(Day-2): Practical understanding of BabySoC structure and simulation results](../Level_2/readme.md).


