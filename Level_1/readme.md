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
   - :zap: Any computing system has some basic functions and some specialized functions.
      - `Basic functions` are processing , storage, Synchronization managemnet (clock), peripheral interface management , power management.
      - `Specialized functions` communication interface, secure data management, image/video/audio processing.

   - :zap: Generally for high performance computing (Desktop computer) different chips or different hardware blocks are separate entities, these are connected together through wires.
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

## :book: Components of typical SoC

### :bulb: Processing Units
   - :zap: Central Processing Unit (CPU) (Basic unit):
      - Usually it is a general purpose processor.
      - It has general fetch, decode, execute stages.
      - ALU (arithmetic and logic unit) operations, memory operations are performed by this.
        
   - :zap: Graphics Processing unit (GPU) (Special unit):
      - Perform graphic rendering and parallel computing task.
      - Used for Virtual Games,images,videos.
        
   - :zap: Digial Signal Processor (DSP) (Special unit):
      - Optimized processing of digital signals (audio, video, communications).
      - 
   - :zap: AI/ML Accelerators (TPU) (Special unit):
      - Optimized processing of neural networks and machine learning tasks.
        
---

### :bulb: Memory Units
 Nowdays, Havard architecture is preferred, where program/instruction memory and data memory are different to avoid overwrite issue.
   - :zap: On-chip SRAM (Static random access memory):
     - Used for cache.
     
   - :zap: ROM (Read only memory):
      - For storing boot codes.
      
   - :zap: DRAM controller:
      - Interface with external dynamic random access memory.
      - 
   - :zap: Flash/NVM controller:
      - For program and data storage.
---

### :bulb: Peripheral interface Units
 
   - :zap: I/O interfaces:
     - Universal serial Bus (USB).
     - Peripheral component interface express (PCIe).
     - HDMI,MIPI (Camera/display).
     - Universal Asynchronous  receiver and transmitter
   - :zap: Storage interface:
      - eMMC, UFS, SD card.
      
   - :zap: Serial interface:
      - Serial peripheral interface (SPI).
      - Controller area network (CAN).
      - Inter integrated circuit (I2C).
      - 
   - :zap: Flash/NVM controller:
      - For program and data storage.

    - :zap: GPIOs:
      - General purpose input output interface for control and signals.

---

### :bulb: Interconnect and Communication Units
 
   - :zap: Bus/Network on chip:
     - Advanced extensible interface (AXI) to connect processor, memory, interface blocks.
     - Advanced high performance bus (AHB) to connect different cores.
     
   - :zap: Direct memory access controller (DMA):
      - Enable high speed data transfer between memories without CPU supervision.

   - :zap: Cache coherency logic:
      - Ensures data consistency across multiple cores.

      
   <div align="center">:star::star::star::star::star::star:</div> 
   
## :trophy: Level Status: 

- All objectives completed.
- I have learned simulation using iverilog,GTKWave (for timing diagram viewing) and synthesis using Yosys and SKY130 PDK.
- 🔓 Next level unlocked 🔜 [Level-2(Day-2): Timing libraries,hierarchial vs flat synthesis, efficient flip-flop coding styles](../Level_2/readme.md).


