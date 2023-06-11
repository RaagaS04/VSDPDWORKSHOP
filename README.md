# VSDPDWORKSHOP
This is an overview of the notes that I wrote during the 5-day Advanced Physical Design using OpenLANE/Sky130 workshop. The aim is to utilize the open-source flow OpenLane with SKY130nm PDK to cover the whole RTL2GDS flow.
## 1. How to Talk to Computers?
   ![now-1](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4c89ffc3-5a14-4656-9cb6-e4173e176139)
   * The core of the packaging will contain the chip. According to the figure, Chip is attached to the packaging.

      * **PADS** : A chip's internal or external signals can be sent it.
      * **CORE** : This is the location of all the digital logic.
      * **DIE**  : The DIE is the total chip size. The silicon wafer will be used to produce die.
                ![now-2](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/345c311b-e41b-4f01-8d65-c044e0a88aa9)
   * Other details
      * **Foundry**– Place where the chips get manufactured.
      * **IP (Intelligent Properties)**– An Intellectual Property (IP) core in Semiconductors is a reusable unit of logic or functionality or a cell or a layout design that is normally developed with the idea of licencing to                                          multiple vendor for using as building blocks in different chip designs.
      * **Macros**– Digital logic blocks
      * **RISC-V**- Instruction Set Architecture
      * **ISA**   - The way we interact with computers.
                     ![now -3](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/7845c1f3-b13e-4e38-a7e8-792e0cacd18f)
  * Suppose we want a C program to run on a particular layout. The C program is compiled into an assembly language program (RISC-V assembly language program). This assembly language program is converted into a machine             language program (binary language program). The bits here will be executed in a layout, and we will get the required output.
                     ![now -4](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/ad7e3b50-7b97-4642-96e6-dc4fc541f215)
  * The interface between RISC-V architecture and the layout is hardware description language. We implement RISC-V specifications in RTL.
## From software applications to hardware
 * The application software enters a block called system software. The system software converts the application software into binary language.
   
   ![now-4](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/741f1d57-890c-4640-8b26-cf44c47d4f95)
## The flow of System Software:
   **1.OPERATING SYSTEM**
  *  OS Handles IO operations and allocates memory and low-level system functions. Converts the app into an assembly language program and finally into the binary language program so that the hardware understands it. The            output of the operating system is the small functions in C, C++, Java, and VB.
   
   **2.COMPILER**
 *   These functions are taken by the respective compiler and convert them into instructions. The syntax of the instructions will depend on the type of hardware used (If the hardware is ARM, then the instructions will be          in the ARM format) -.exe file.
   * The instructions here will act as the abstract ISA between the hardware and the C programs.
                   ![now -5](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/7097c50a-1610-47d5-8489-74075b578128)
  * We need an RTL to implement instruction specifications. The RTL is converted into a synthesized netlist (high-level specification into synthesized netlist). This will be in the form of gates.
     Above netlist generation, we follow physical design implementation.
                   ![now -6](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/889e3218-8f73-44fb-84c8-87bfa7e013fb)
    **3.ASSEMBLER**
  *  The job of the assembler is to take the instructions and convert them into binary numbers (machine language program). Based on machine language programs, the hardware executes the functions and accordingly generates          the output.
          Example: Stopwatch app
               ![now -7](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/67baa987-70d9-43c1-b3fb-a410521cdec6)
## 2. SOC DESIGN AND OPENLANE
  *  **Introduction to all components of open-source digital ASIC design**
   * Digital ASIC design requires RTL IPs, EDA Tools (qflow, OpenROAD, OpenLANE), and PDK data.
   * What is a PDK? The interface between the FAB and the designers.
       * PDK – Process Design Kit
         * Collection of files used to model a fabrication process of EDA tools used to design IC.
               * Process design rules: DRC, LVS, PEX
               * Device Models
               * Digital Standard Cell Libraries
               * I/0 Libraries
    ![NOW -17](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/989b1234-c5fb-49b4-b945-6dbe492f9799)
   *  Google releaseD open-source PDK for ASIC implementation using open-source or close source tools.
    ![NOW -18](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4f2a78df-5338-415f-9b0c-0f9538764fc7)
   *  The fabrication process of SkyWater 130 nm is cheaper than advanced nodes. It covers over 6% of IC technology nodes used in the market.
    ![NOW -19](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/2f57e2a6-7aee-4224-a6da-b17ea4057f04)

 ### **ASIC Flow objective: RTL to GDS II - Also called Automated PnR and/or Physical Implementation.**
   ![NOW-20](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/73c22ffd-a930-41a8-ba95-5a1cdd40c862)
 ### **Simplified RTL to GDSII Flow**
   ![NOW -21](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/cf8634d2-427e-4916-bb56-c791c9ba1ce6)
   #### **1.Synthesis:**
   ![NOW-22](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/3e09d1f3-4870-4ee4-a0cb-14189a42515b)
   *    Converts RTL to a circuit out of components from the standard cell library (SCL). The resulting circuit is referred to as a gate-level netlist. Gate level netlist is functional equivalent to RTL.
   *    The library building blocks, or the cells, have regular layouts. Typically, the cell layout is enclosed by a fixed-height rectangle. The cell width is variable but discrete. It is an integer of                                 multiple units called site width.
   *    Standard cells have a regular layout – Each has different views/ models.
   *    Liberty View – Has an electrical model for the cells, such as delay and power models.
   *    HDL and SPICE behavior views for the cells. Layout view for the cells.
   *    GDS View, LEF view- abstract view.
   ###  **2.Floor planning and power planning:**
   ![NOW-23](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/3d030bda-53c7-4396-97ef-8258e3e55b8b)
   
   *    The objective here is to plan the silicon area and create robust power distribution to the circuits.
   *    Chip floor-planning: Partition the chip die between different system building blocks and place the I/P pads.
   *    Macro Floor Planning: Dimensions, pin locations, rows or routing tracks are definition.
   ![NOW-24](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/93265324-4cad-4d1e-a063-61ebbcc92c05)
   
   *    In power planning the power network is constructed.
   *    A chip is powered by multiple VDD and GND pins. The power pins are connected to all the components through rings and horizontal/ vertical power straps. Such parallel structures are meant to reduce                             the resistance hence the IR Drop, and to address the electromigration problem. Usually, the power distribution network uses upper metal layers as they are thicker than the lower metal layers. Hence have less                   resistance.
   ###  **3.Placement:**
   ![NOW-25](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/56ce3d7e-9caa-434b-92f9-c588bd99130e)
   *    Place the cells on the floorplan rows aligned with the site rows. Connected cells are placed very close to each other to reduce the interconnect delay and allow successful routing afterward.
         * Done in two steps:
            * Global - Tries to find the optimal placement of all the cells. Such positions are not necessarily legal. So cells may overlap or go off the sites.
            
            * Detailed - The positions obtained from the global placement are minimally altered to be legal
   
   ![NOW-26](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/5d6e9e7b-fe54-418f-94bf-24ece75f0fff)
### 4. Clock Tree Distribution:
   ![now-27](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/099d432e-84e0-46e5-866b-1f249fe411d1)
  *   Deliver the clock to all sequential elements (eg, FF) with minimum skew.
  *   Clock skew – The arrival of the clock to the different components at different times.
### 5. Routing:
  ![now-28](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/e28387b5-6aba-4128-8436-adb55f2c43e3)
   
  *  Given the placement and fixed number of metal layers, it’s required to find a valid pattern of horizontal and vertical wires to implement the nets that connect the cells together. The routing uses the available metal          layers defined by the PDK. The PDK defines the pitch, tracks, and minimum width. Also, it defines the vias that are used to connect the wire signals present on the different metal layers.
  *  The Skywater 130 nm PDK defines six routing layers. The lowest layer is called the local interconnect layer (TiN layer). All the other metal layers are aluminum layers.
      *  Most of the routers are grid routers. They construct the routing grid out of the metal layer tracks. As the routing grid is huge, we follow the divide-and-conquer method for routing.
         *  Global Routing: Generated routing guides.
         *  Detailed Routing: Uses the routing guides to implement the actual wiring.
  *  Once done with routing, we can construct the final layout.
### 6. Physical Verification:
  *   DRC - To make sure that the final layout follows the design rules.
  *   LVS – To ensure the final layout matches the gate level netlist.
  *   Timing Verification:
      *   STA – To make sure that all the timing constraints are met. And the circuit will run at a designated clock frequency.
### Files of Physical Design:
 *  **Tech file**: .tech contains the metal layer, connectivity between layers, DRC rules, and other definitions needed by Magic layout tool to view a single cell.

 *  **LEF file**: .lef is combination of tech lef (contains metal layer geometries) and cell lef (contains geometries for all cells in the standard cell library). This lef file does not contain the logic part of cells, only                     the footprint that is needed by the PnR tool.
 *  **DEF file**: .def is derived from LEF file and is used to transfer the design data from one EDA tool to another EDA tool and contains connectivity of cells of the design and is just a footprint (does not contain the                        logic part of cells) that the PnR needs. Each EDA tool to run will need to read first the LEF file runs/[date]/tmp/merged.nom.lef and the DEF file output of the previous stage's EDA tool (e.g. CTS EDA                          tool TritonCTS must first read DEF file from placement stage). So before running a stage, make sure the $::env(CURRENT_DEF) points to DEF file of previous stage or else there will be bunch of errors.
### 2.3. Introduction to OpenLANE and Strive chipsets
*   OpenLANE started as an open-source flow for a true open-source tape-out experiment.
*   striVe is a family of open sourcing everything, including SoCs. (Open PDK, Open EDA, Open RTL)  
   ![now -29](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/1df7a114-fbd2-4ec2-9361-ea94d1bbb303)
*  OpenLANE main goal: 
   To produce a clean GDSII with no human intervention. Tuned for SkyWater 130nm Open PDK. Also, support XFAB180 and GF130G. It can harden Macros and Chips to generate the final layout.

*  Two modes of operation:
   *  autonomous – push button flow
   *  Interactive – run commends one by one to check intermediate steps.
### 4. OpenLANE ASIC DESIGN FLOW
   ![now -30](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/04e0e31d-4927-4518-8364-6ce612800870)
### RTL Design
*  The flow starts with the design RTL and generating the final layout in GDSII format. OpenLANE is based on several open-source projects.
   ![now-29](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/9736bd5b-8bb2-4b91-b1f5-80027e48d4b8)
*  The flow starts with the RTL synthesis. The RTL is fed to yosys with the design constraints. Yosys translates the RTL to logic circuits. These circuits can be optimized and mapped into a standard cell library using the ABC    tool. ABC should be guided during the optimization. This guidance will come in the form of the ABC script. OpenLANE comes with several open-source scripts. We refer to them as synthesis strategies. We have strategies to      target the least area and for the best timing. Different designs can use different strategies to achieve the best objective. For this, we have synthesis exploration utility. This is used to generate a report that shows the    design delay concerning the area effected by synthesis strategy.
   ![now-31](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/57a145ed-9dce-4eb0-bfdf-5a840a6e6866)
### Design Exploration Utility
*  OpenLANE also has the design exploration utility. This can be used to sweep the design configurations. And generates a report, as shown below.
   ![now-32](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/d70a3573-ee6e-44d0-bf24-8dedb802b970)
*  This report shows the different design metrics. We have more than 35 of them in a report. It also shows the number of violations after generating the final layout. It is recommended to explore the design first and then use    the best configurations for a particular design to result in a clean layout.
*  Also, design exploration can be used for regression testing (CI). So, we can run the design on several exploration configurations to get the best-optimized configurations. Currently, we have 70 designs. This utility will      generate a report as shown below.
   ![now -33](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/2043941d-3f30-4ce3-8c75-9eb153632f8f)

*  This report shows the design metrics given different configurations and the number of violations. The results will be compared to the best-known results.
### Design for Test
*  If we want our design to be tested after the fabrication, we can enable DFT. This step uses open-source project Fault. To perform scan insertion, ATPG, test patterns comparison, fault coverage, and fault simulation.
### Place and Route
*  After this comes the physical implementation, also called automated Place and Route, done by the OpenROAD application.
### Logic Equivlence Check
*  We need to perform LEC checking using yosys. We compare the netlist resulting from the optimization step in PD flow with the gate-level netlist generated in synthesis. To make sure they are functionally equivalent.
*  During the physical implementation, we have a step–fake antenna diodes insertion script to address the antenna rules violations.
### ANTENNA Rules Violations
*  Dealing with Antenna Rules Violations:
   *  When a metal wire segment is fabricated, it can act as an antenna.
      *  Reactive ion etching causes charge to accumulate on the wire.
      *  Transistor gates can be damaged during fabrication.
   ![now-33](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/24d43342-4248-44bb-bbb3-02c5c978aaf6)
*  Usually, this is the job of the router.
   *  Solutions:
      *  a.Bridging – Attaches a higher layer intermediary. Requires the router awareness.
      *  b.Antenna diode – Add antenna diode cell to leak away charges. Antenna diodes are provided by the SCL.
   ![now-34](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/7211541b-ae5f-48b0-8baf-1d8ec0285d4f)
*  Fake Antenna Diode Cells are used for every cell input after placement and run antenna checker (Magic) on the routed layout. If the checker reports a violation, we replace the fake diode with the real one.
### STA, DRC and LVS:
*  The final steps in OpenLANE involve STA, DrC, and LVS.
   *  Timing sign-off involves doing RC extraction from the routed layout using OpenSTA to highlight any timing violations, if there are any.
   *  DRC – Magic has used for DRC and SPICE extraction from the layout.
   *  LVS – Magic and Netgen are used for LVS. Extracted SPICE by MAGIC vs. Verilog netlist.
## Open Source EDA Tools
*  PDK - Process Design Kit
*  PDK has the timing libraries, the LEF files, TECH files, and Cell LEF. open_pdks directory: These foundry files are compatible and made to work with commercial EDA tools. Open PDK mitigates the issue by using scripts and      files to convert the foundry level PDKs to be compatible with the opensource EDA tools (like MAGIC, NetGen)
   *  sky130A directory: The PDK that is made compatible with our open-source environment. Here sky130A is the PDK variant.
      ![now-35](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/6a2da05e-6537-40cd-903b-c78f690ad201)
   *  libs.ref: contains all the process-specific files (timing, lef and cell lef)
   *  libs.tech: specific to the tool

   ![now-36](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/606cef5b-e76f-4ae1-99f5-81f21848047b)

*  We are working with sky130_fd_sc_hd
   Here, sky130: process name, 130 nm
   *  fd: for skywater foundry
   *  sc: for standard cell library files
   *  hd: variant of the PDK (hd: high density)
   ![now -37](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/ec1454b2-903b-4e0c-952f-46dfcd2dcf2e)
*  techlef contains all the layer information.
*  mag: all the MAGIC-related files
*  lib: all the timing files containing all the process corners.
   ![now -38](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/c5c2fe58-b994-4578-91da-d67b55971a17)
*  tt: for typical, ss: for slow slow, ff: for fast fast and PVT corners
   ![now -39](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/853b1c46-aee7-4f9e-8b94-4285499c9314)
*  lef files
*  Tool environment directory:
   ![now -40](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4365b433-0b2b-48fb-aeed-826cf25263e2)
## Designing Preparation Step
### Running OpenLANE EDA
![picture-1](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/f85f34e2-c90f-4d6a-b899-bea9dfaaf1ca)
*  Without the interactive switch, the tool will run the complete flow.
*  Importing the required packages
*  All the designs run by OpenLANE will be extracted from the design folder.
*  Here we consider the picorv32a design
   ![now -41](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/586b4d1e-a2e0-43dc-9826-dce8e83dc5cd)
   *  src: where the Verilog file for our RTL will be present. As well as the SDC information.
   *  config.tcl: by default, characteristics of the design information are mentioned. This will override the default OpenLANE settings.
   ![now -42](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/0618feb3-fff7-4fbe-909e-57e9dec7d98e)
*  Setting up the file system for the design:
   ![picture-2](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/f48430d5-de6f-48dc-b80d-15a2cc2bf28a)
*  Here the tech.lef (layer level information) and cell level lef merged into one.
### Reviewing files after design prep and run synthesis
*  Here the runs directory has been created after running command run-synthesis.
   *  tmp folder: where the temporary files are stored, and the rest of the folders will be empty.
      ![picture-3](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/b8684d48-6fcb-49ff-907f-6cb6de645d90)
      ![now -43](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/27b5d3f6-dfc9-4920-b31a-a77542f776e2)
*  **config.tcl**: show all the default parameters taken by the run.
*  **For synthesis**: this will run the yosys and abc synthesis
*  **OpenLANE project :[Git link](https://github.com/efabless/openlane)** 
*  **Calculating the D-Flip Flop count for the design**: 1613/14876= 10.8%  
*  If we check the synthesis folder for results after running run_synthesis we can see that there is a new file generated named picorv32a.synthesios.v
   ![now -44](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/0a3fd524-2f83-4e2d-affe-10a605f6efeb)
   ![dflipflopsno](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/3775eb04-221a-4bb3-9a80-bbcaffb565ad)
   ![No of cells](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/abaeea3c-b2ea-4d1f-8165-af844abac4bc)
*  To check the synthesis statistic report
   ![now -45](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/d36d7ce0-4ed2-4e16-8832-29c97ba9cfe6)
## DAY 2
### Utilization factor and aspect ratio

*  Define the width and height of the core and die. This is the first step in the physical design flow.
   ![now -46](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/3329facd-a116-4c48-9712-719545878cb4)
*  Netlist defines the connectivity between all the components.
*  In defining the dimensions of the chip, it mostly depends on the dimensions of the logic gates.
   ![now -47](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/6eabb2e5-5867-46a7-aef3-6a99bf88223e)
*  To get the dimensions of the core and die, we are interested in the dimensions of the standard cells, not considering the wires in between them.
*  Standard cells are given rough dimensions as shown below.
   ![now -48](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/533dea53-c2ef-4613-a1aa-b761e44e77be)
*  Let’s calculate the area occupied by the below netlist on a silicon wafer by bringing the cells together.
*  What is the core and die section of a chip?
   ![now -49](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a61a6662-7fbb-41ea-8416-81dcdc9b3fb9)
*  Core: where we place the fundamental logic.
*  Die piece of the area where our circuit is built so that our circuit will not exceed this area. We imprint this die multiple times on a silicon wafer to increase its throughput.
   ![now - 50](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/afb98e18-8272-4497-894b-3681fa81c3e2)
* As we can see that the netlist of 4 sq units occupies a complete area of the core. This means we have utilized the core 100%.
   ![now -51](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/3adcad8b-84c0-4974-9b09-7ad2bfd2c746)
*  Utilization Factor: Area occupied by netlist/ Total area of the core = 4 x 1sq.unit/ 2 unit x 2 unit = 1
   *  In practice, we go for a 50 to 60% utilization.
*  Aspect Ratio = Height/ width = 2 unit/ 2 unit = 1
*  When the aspect ratio is 1, the chip is squared in shape. Ex:
      ![now -52](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/6d6c662d-2f0c-4da6-8521-2fbe80bb33e3)
### Concept of pre-placed cells
   ![now -53](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/2db31397-5592-4842-881b-5fc669aad044)
*  The figure above shows that the utilization factor is 25%, and 75% is utilized for the optimization.
   *  On top of this, we do the routing.
    ![now -54](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/ce274a47-50fb-453b-8f60-1a82d934ee20)
*  It is supposed to be a squared chip where we have the aspect ratio as 1.
### Locations of pre-placed cells:
*  The cells can be divided into two blocks, as shown in the figure below. These blocks are implemented separately.
   ![now -55](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/406c4880-2c32-4b0a-8733-937f614e561c)
   ![now -56](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/c8427e3c-fa3e-446c-9172-f3a75d2e0ecb)
*  These blocks are invisible if we look from the top. Looking into the main netlist.
      ![now -57](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4b6c3417-8e6b-4adb-845c-db657fc12b5e)
*  These blocks can be used multiple times in the netlist. This concept is useful when we want the blocks to be reused. Similarly, we can have other IPs also available.
*  All these blocks can be implemented once and can be instantiated multiple times on to a netlist.
   ![now -58](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a2333c9c-3a70-4cff-8a1c-fdab62200c13)
*  The placement of these cells on the top-level netlist is fixed. They are called pre-placed cells since they are placed before placement and routing. Once these locations are placed, they are not moved by automated            placement or routing tools.
### De-coupling Capacitors
*  These pre-placed cells should be surrounded by de-coupling capacitors.
#### De-coupling Capacitors
   ![now -59](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a4e042a7-290b-4954-b648-2c34c0f06e82)
*  If there is a large distance between the power supply and a circuit in the design, there might be a voltage drop across the wire from vdd to the circuit due to the resistance, inductance, and capacitance of the wire being    used. This problem is solved using de-coupling capacitors.
      ![now -60](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/8a168cd9-6da5-4582-bdef-71d3702c8198)
* De-coupling capacitors are huge capacitors that are filled with charge. The voltage across the de-coupling capacitor is like that across the power supply. Whenever the circuit switches, the de-coupling capacitance provides   a power supply to the circuit. This means the de-coupling capacitor de-couples the circuit from the main supply. Whenever the switching happens, the de-coupling capacitor will send the current to the circuit. These           decoupling capacitors are placed close to the circuit to reduce the voltage drop. The de-coupling capacitor supplies the amount of current needed by the circuit during switching. We use the de-coupling capacitor to charge     the circuit. Whenever there is a switching activity, the de-coupling capacitor loses some charge to the circuit. Whenever there is no switching activity, the de-coupling capacitor replenishes its charge from the power         supply.
   ![now -61](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/33ab5cd9-58af-48cb-80f9-36883e5dfb67)
*  This also reduces the crosstalk problem.
### Power Planning
*  Consider a scenario where a signal is sent from the driver to load. We must ensure the load receives the exact shape of the signal.
*  Tapping of blocks to Vdd, and all the block ground lines are tapped to the ground.
   ![now -62](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/864b4741-97e5-418d-9a53-efd2f624feae)
*  To retain the same signal from the driver to the load, we need the power supply. In this region, we don’t have any de-coupling capacitor that will take the power supply switching. So, there is a possibility of voltage drop    across the line (shown in orange). Let’s assume that the line from driver to load is a 16-bit bus.
   ![now -64](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/2a4d8ced-eaaa-40e4-8f7c-b0a9504fc4cc)
*  The capacitors shown here are charged to Vdd for logic 1 and GND for logic 0. When we pass this 16-bit bus as input to the inverter, we get the inverted output. So all the capacitors with logic 0 as output is discharged,      and with logic 1 will be charged to Vdd.
   ![now -65](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/48180ffc-1a4d-4d4f-ad23-9ddcad2d5081)
*  We have a single ground line for the 16-bit bus. Due to this, there is a bump over the ground line. If the size of the bump exceeds the noise margin, it will enter an undefined state. Due to the undefined state, it might      logic 1 or logic 0. This phenomenon is called a ground bounce.
*  When all the capacitance is charged from logic 0 to logic 1 we have a voltage droop as all the capacitors are demanding the power supply at the same time. Here the voltage droop can get into to undefined region.
   ![now -66](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/5d320b02-dc06-41c3-a235-4fd6c620784f)
*  The problem arises as the power supply is provided from one point.
   *  Solution:
      *  Instead of having single power supply we need to have multiple power supplies.
   ![now -67](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/2698ce3b-c395-4d17-8cc7-ee443f1211dd)
*  Then the current demanded by the circuit can be taken from the nearest power supply. Or it will drop the current to the nearest ground. This is the reason we have multiple power and ground pins in chips.
      ![now -68](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4aa76922-c2b1-4b47-9961-bcdc776f4f31)
### Pin placement and logical cell placement blockage
   ![now -69](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/da22f0fd-8f23-4540-99a6-243b39111d70)
*  The connectivity information between the gates is coded using VHDL/ Verilog language called the “netlist.”
*  The placement of input and output ports depends according to the cell placement in the core. And no FFs can be placed in this area where the blocks are placed. The backend team must decide on the pin placement.
*  The CLK ports are bigger in size than the data ports. The reason for this is the CLK is the one driving all the FFs in the core. So, we need the least resistance path for clocks 1 and 2. Bigger the size lowers the            resistance.
*  We do logical placement blockage for blocking the area so that the automated place and route tool doesn’t place cells in this area, as this area is reserved for the pin locations.
### Running floorplan in OpenLANE
*  Standard cells placement is done in the placement stage.
   ![now -70](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/5ef15a89-1999-4e57-b285-1bbba751367d)
*  Here we have all the variables for the floorplan stage in the READ.md file.
*  These variables are also called as switches in the floorplan stage.
      ![now -71](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/758db91f-2a15-4488-9086-bdcd5e78b714)
*  All the default values of the variables are shown here.
*  To check all the variables associated with all PD stages.
   ![now -72](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/2b260176-336a-421a-ba15-4f01d8fc85ff)
*  Default parameters set for floorplan stage in OpenLANE
      ![now -73](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/efe5b780-38a7-499e-9b21-96817349be46)
*  The lowers priority will be given to system defaults (floorplan.tcl in configurations folder), and height priority will be given to config.tcl and then sky120A_fd_sc_hd_config.tcl for setting floorplan stage variables.
      ![now -74](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/6a000a04-0cb0-490b-862a-bd53afdaba0d)
*  Contents of config.tcl file
   ![now -75](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/ea03ba0a-e833-4ce3-8cdc-face65fdfbf6)
*  In OpenLANE flow, the vertical and horizontal metal is one more than what we specify here.
*  After changing the config.tcl file with core utilization of 65%, clock period 10 and vertical metal as 4, and horizontal metal as 3.
   In OpenLANE flow, the vertical and horizontal metal is one more than what we specify here.
   ![now -76](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/9a094241-856c-440d-8af0-e6e63d2f22b4)
*  Command to run floorplan: run_floorplan
### Floorplan Files
   ![picture -4](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/25f7e0ea-4522-409b-8bbb-210b25e4bfe0)
   ![diearea](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/5aefb4d9-bf4b-4a25-8529-a929fb1b0db1)
*  Check for the variable settings
      ![now -77](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/3b332130-b492-427b-82d0-b2e18d587a7b)
*  The highest priority will be given to sky130_sky130_fd_sc_hd_config.tcl. So, the core utilization should be changed here—then config.tcl, and then the system default variable values will be given priority for setting          variables in .tcl files.
*  To check the floorplan results – looking at the def file, we don’t know where what is placed.
   ![now -78](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/fac20b5c-8c01-4c09-91f9-74c6612570f1)
*  To see the actual layout after the floorplan 
*  Command to run magic layout: magic -T 
*/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/bibs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def
   ![now -79](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/f97df854-5b64-4e00-95a7-06d65ee0a507)
   ![now -80](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/076ef72a-f879-4ba8-8688-2af54895ab05)
 
 ### Review floorplan layout in MAGIC
 ![magic layo![picture 5](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/6aca00e2-8085-48c1-a151-46914144cbc6)
 ![picture 5](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/667c3573-8e2f-48f6-828b-7fe0cf2cc166)
* To check vertical metal type
![what](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/778b390c-22ad-4168-ad87-fc20b48938b8)
   ![now -81](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/b6120aa7-cafb-4155-8b50-b47a2a70956e)
* Tap Cells: Avoids latch-up conditions in the CMOS devices. They connect n-well to Vdd and substrate to the ground.
   ![nand](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/7815c33c-5952-49b0-a670-357fd9854d9d)
* Standard cell are placed during the placement stage
### Placement and Routing

*  Here binding the netlist with physical cells takes place. All the gates have a physical view while representing the core like an FF, which is square in shape.
*  In the real world, we give physical dimensions for all the gates by giving width and height. So every component of the netlist is given a proper width and height.
   ![now -82](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/841db8c6-94c2-4fb3-b34a-ad811761766f)
   ![now -83](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/17a19ecb-ec8f-4d41-877d-50406cf3b1c7)
*  And the block already has the proper shape
*  The dimensions of the cells in a design are present in a library. Library also have the timing information of all the gates.
   *  Library files are divided into two categories:
      *  Library files containing the shapes and sizes of cells.
      *  Timing information of the cells.
*  It also contains the various shapes of all the gates. Gates that are bigger and have the least resistance path. And it will be faster.
      ![now -84](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/42b78241-875e-4f3b-aa53-4ea5ac0b5562)
### Placement
   ![now -85](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/9f2c69c6-61d0-42e4-8d5b-bc96838dc4a5)
*  The library has various flavors of cells in the library. We select these cells based on the timing conditions (delay information) and the size of the floorplan requirements. Placement.
   ![now -86](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/8ee6a6b2-fd23-41be-99bd-1fabf2e8093f)
*  We must place the physical view of the netlist for the placement. We placed the cells according to the logical connectivity and placed them close together concerning the input and output pin placement.
*  The cells are placed according to the input and output ports of the circuit, as shown in the figure. We estimate the wire length and capacitance, and based on that, we insert repeaters.
*  If we have a large wire, we have huge resistance and capacitance associated with that wire. To maintain the signal integrity, we will reproduce the signal using buffers which are called repeaters.
   ![now -87](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/dbdad93f-a4d1-49a4-a3f5-6018c2b82963)
*  Based on the wire length estimation, we calculate the capacitance using the transition of a waveform using timing analysis. The higher the value of the capacitor, the amount of charge required to charge the capacitor will    be high and have the worst slew.
*  We use buffers from Din2 to FF1, which will receive the proper signal even though we have a large wire length.
*  The internal routes of FF2 (Yellow) are in some layers, say metal 1 and metal 2. And the connection from 1 to 2 (green) will be on metal 3.
*  Based on the ideal conditions of the clock, we do a timing analysis. Based on this setup timing analysis, we will determine whether the placement is reasonable based on the given specifications.
### Need for library characterization:
*  Logic Synthesis: Convert functionality into legal hardware. The output of logic synthesis is an arrangement of gates that represent the original functionality described using an RTL. This is the proper connection of the      gates to represent the original functionality.2
*  Floorplanning: We import the netlist that we get from logic synthesis and decide the size of the core and the die. So the width and height of the core and die are dependent on the number of gates and their sizes.
*  Placement: We place the logic cells in the chip in such a fashion that the initial timing is met.
*  CTS: We want the clock signal to be spread to the logic cells simultaneously at an equal time. The buffers in the figure will take care of the clock signal has got equal rise and fall times.
*  Routing: Routing the cells. There are certain properties of the cell that should be taken care of while routing.
*  STA: Here, we find the maximum achievable frequency of the circuit.
   ![now -88](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/36d409b0-4099-45ba-8b04-1b0c7d5f9089)
   ![now -89](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/e2b07160-6104-433c-bf14-0edad262b65d)
*  One thing that is common across all stages is GATES or Cells. The collection of these cells is referred to as library. The EDA tool needs to understand are timing characteristics of the gate and how it is represented in a    tool.
   ![now -90](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/912bca1b-9513-45d5-afc9-2192f9456eee)
### OpenLANE Placement
*  Placement takes place in 2 stages:
   *  1. Global Placement: Corse placement and there is no legalization. Legalization: The standard cell should be placed inside the standard cell rows, with no overlaps. We require legalization from a timing point of view.
   *  2.Detailed placement
*  Command: run_placement
*  Then global placement happens. In OpenLANE, the placement takes place using a half-parameter wire length. Our objective is to reduce the overflow. If the overflow value converges, we can assume the placement is right.
*  Command to run magic layout:
   *magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/bibs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def

*  Then we need to check our design after placement:
   ![picture -6](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/fd9f735a-fb3d-4639-a7e2-e8b82e5eb94a)
   ![picture 6](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/2c8a77a2-8ffc-419c-8604-b9555dbec7b5)
*  We know that in placement the standard cells are placed and fixed.
*  The power and ground network will be created during the placement.
*  Standard cells are placed in a section called a library. We also have DECAP cells and MACROS placed in the library.
*  The library also contains different gates with different functionality. It also got cells of different sizes. Based on the sizes of cells, we can decide the drive strength of cells. The bigger cells have larger drive          strength. For example, the smaller buffers have the least drive strength. It also contains cells with different threshold voltages. The variation in threshold voltage decides the speed of the cell. For example, a 0.4 Vth      inverter takes more time to switch than a 0.3 Vth inverter.
### CELL DESIGN FLOW
*  A cell, for example, an inverter, should follow a cell design flow. Steps:
      *  1.Inputs: PDKs (DRC and LVS rules, SPICE models, library, and user-defined specs)
      ![now -91](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a8d06031-7b5f-4557-93e3-539c70d42df2)
*  SPICE model parameters: We get these parameters from the foundry.
   ![now -92](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/25e75e66-d5ad-486d-b6b4-71a91527de90)
### Library and User-defined Specs:

*  The separation between the power rail and the ground rail decides the cell height. The cell width is dependent on the timing information. This depends on the drive strength of the cell. Lowering the value of the drive        strength of the cell can drive a few other cells at the output.
*  The library developer must consider the supply voltage to design the cell, and they also need to take care of noise margin levels to take care of the supply voltage of the cell.
*  Certain libraries should be built on certain metal layers. This should be taken into consideration.
*  Pin locations are also important for developing a library.
   ![now -93](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/8dbdc152-66a0-4763-8e4a-003d12c0fcdb)
*  The library developer is responsible for taking these inputs and developing a library cell that adheres to these inputs. 
*  2. Design steps: circuit design, layout design, and characterization Circuit Design: 
   We should design PMOS and NMOS transistors in such a fashion to meet the library requirements. These are mostly based on SPICE simulations.
      ![now -94](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/d76fa2c8-3fa8-4ecd-87e0-4dbf5be58608)
      ![now -95](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/bb0187b2-2ce6-4bae-a727-7a876d784ace)
*  Characterization: This is a step to get timing, noise, and power information (power.libs) and circuit functionality.
*  Layout Design:
      ![now -96](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/30eedf40-7c67-4aba-9fe5-dfb672950cac)
*  First, we need to implement the function and derive the pmos and nmos network graphs.
*  Art of layout – Euler’s path + stick diagram
*  Euler’s path: The path that is traced out only once.
      ![now -97](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/94167021-c0f7-405b-b706-e859504d2a8b)
*  Based on Euler’s path we need to draw a stick diagram out of it.
   ![now -98](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/14f63897-5ef3-4561-86db-d6fb1192a6ca)
*  Then we convert this stick diagram into a layout that adheres to the DRC rules given by the foundry.
   ![now -99](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/8631dfcb-4a5b-4c71-ae16-e489874ec6ba)
*  Typical layout from MAGIC Design tool
*  From the layout, we can calculate cell width and cell height.
*  Then we need to extract parasitic out of the layout and characterize that in terms of timing.
*  CDL File: Circuit Description Language
*  Output from a layout is GDSII, LEF (defines the width and height of the cell), extracted spice netlist (.cir)- R, C of every element in the circuit.
### Typical characterization flow
   ![now -100](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/6e87a4d1-d09d-43f0-b048-47f16ff6bc83)
   ![now 101](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/d8ddcc4a-7194-4946-9661-6bc11a81cc85)
*  Steps:
   *  1.Read the model file.
   *  2.Read extracted SPICE netlist.
   *  3.Recognize the behavior of the buffer.
   *  4.Read the subcircuits of the inverter.
   *  5.Attach the necessary power sources.
   *  6.Apply the stimulus.
   *  7.Vary output load capacitance.
   *  8.Provide necessary simulation.
   *  9.Feed in all these inputs through a configuration file to characterization software called GUNA.
   ![now -101](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/3e382266-e968-4fc4-b4bf-4ade5984d5f4)
*  GUNA – Generates timing, noise, and power.libs
Timing Characterization Timing threshold definitions: variables related to waveform

*  slew_low_rise_thr: points toward the lower side of the power supply. (About 20%)
   ![now -102](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/d8c77f93-10dc-4346-8165-e24576b27173)
*  slew_high_rise_thr: points towards the higher side of the power supply. (About 20%)
   ![now -103](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/41ffb6d6-05d6-4fe2-8d45-bb6d3bc7213d)
*  slew_low_fall_thr
   ![now -104](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a0acb2c6-8576-44d6-aaff-b15220ccbea3)
*  slew_high_fall_thr
     ![now-104](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/84ccb695-43d7-45dc-b49a-3b6fcb2e11b2)
*  in_rise_thr: Related to the input waveform. The threshold for the input waveform delay. (About 50%)
   ![now -105](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/b301c3de-5b24-419b-a2da-669150c203f3)
*  in_fall_thr
    ![now -106](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4860f8c8-502b-40bf-be80-98217a96bbc6)
*  out_rise_thr: Related to the output waveform. The threshold for the output waveform delay. (About 50%)
   ![now -107](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/e8dc1465-bb51-4e12-9e1d-b446a6e9f639)
*  out_fall_thr
   ![now -108](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/549cb181-1f7d-4297-9e3c-c87a77f86651)
*  Below are the timing variables for slew. This is two inverters in series, red is output of first inverter and blue is output of second inverter:
   ![now -109](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/0f2fcc58-1cf1-40d7-aac1-5197ff75bea4)
*  Below are the timing variables for propagation delay. The red is input waveform and blue is output waveform of the buffer. The left side is rise delay and right side is fall delay.
   ![now -110](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/fb0278ac-06ba-4041-89dc-e2f21a94a05a)
*  Negative propagation delay is unexpected. That means the output comes before the input so designer needs to choose correct threshold point to produce positive delay. Delay threshold is usually 50% and slew rate threshold      is usually 20%-80%.
### IO Placer
*  PnR is an iterative flow.
*  Run synthesis and floorplan steps.
*  How to change input and output pins along the core?
*  After floorplan input and output pins are placed randomly around the core area.
   ![now -111](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/518ca3d7-f3a5-49b0-8163-3b8db37910dc)
*  Open the MAGIC layout tool to check the floorplan of the design
   ![now-112](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/99403587-a98e-4a87-bdf5-84e91280c3ef)
*  From the figure, we can see that the pins are placed at equal distances with respect to each other.
   ![now -113](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/7af3b19f-ca8a-459a-a1b5-6709762a30eb)
*  IO placer supports 4 strategies to place our IO pins.
   ![now -114](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/6b090c21-cdce-443e-8785-b2934b6db4c5)
   ![now -115](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a7f89545-cea6-489a-a4c4-301592da4b5a)
*  From floorplan.tcl we can see that the IO pins are placed with mode 1 with set ::env(FP_IO_MODE) variable. With mode 1 all IO’s are placed with equal distance.
*  Set this variable to 2 and run the floorplan again.
*  Then again check the IO placement with the MAGIC layout tool.
   ![changemode2](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4555994d-adda-46b2-89ce-f73756d65bb4)
   ![picture-8](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/b770ba80-1d77-4fea-a074-5625add311c1)
*  From the layout, we can see that the IO pins are stacked on top of one another.
### VTC – SPICE Simulations (Spice deck creation for CMOS inverter)
*  SPICE deck
   ![now -116](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/79b1ea55-3e01-4956-b986-2ae4eabfe10d)
1.connectivity information about the netlist. It also has the inputs that are to be provided to the simulation and tap points from where we collect the output. In the SPICE deck, we need to mention the connectivity of the       substrate too. Here we take the example of the inverter and assume the Cload value is 10fF.
2.Define component values: The values for PMOS and NMOS. Ideally, the size of PMOS should be bigger than the NMOS. Define the values of input gate voltage. The voltages are kept in the multiples of channel length. Also,         assume the supply voltage is 2.5V.
3.Identify the nodes: Those two points between which there is a component.
4.Name nodes
   ![now -116](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/996b68d3-e208-4dc1-9a0b-3ab817055838)
   ![now -117](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/64a8ddac-e494-486b-b0ae-4e7dbe6de1e1)
### Running ngspice
   ![now -118](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/06daeb26-01ad-454a-933b-57befb195877)
*  SPICE waveform conditions: Wn=Wp=0.375u, Ln,p=0.25u device (Wn/Ln=Wp/Lp=1.5)
   ![now -119](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/6aa71e9d-65ca-4743-a97f-1f0d27f3ef54)
*  SPICE waveform conditions: Wn=0.375u, Wp=0.9375u, Ln,p=0.25u device (Wn/Ln=1.5, Wp/Lp=2.5)
   ![now -120](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/5c4edf8f-d9ae-4f6e-88e5-f3dd508c36dd)
### CMOS robustness depends on:
*  Switching threshold = Vin is equal to Vout. This the point where both PMOS and NMOS is in saturation or kind of turned on, and leakage current is high. If PMOS is thicker than NMOS, the CMOS will have higher switching        threshold (1.2V vs 1V) while threshold will be lower when NMOS becomes thicker.
*  Propagation delay = rise or fall delay
*  DC transfer analysis is used for finding switching threshold. SPICE DC analysis below uses DC input of 2.5V. Simulation operation is DC sweep from 0V to 2.5V by 0.05V steps
Dynamic Simulation of CMOS Inverter
   
![picture -9](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/62291c81-a07e-452c-bce1-7c27bb1e7ae9)
![picture-10](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/c5b759c7-4de6-40f6-ab5a-419942d664ad)
![nmos](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/03d8b056-050e-4d65-8842-e8c2472d61a7)
![gitclone](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/443b0836-23e9-41cf-9262-63410e7380f1)
![picture-11](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4161d231-7173-42d3-b951-e8ba3efeedce)
![picture-12](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/c97acf68-9a4f-4cff-b2b5-9f439a7035ca)
![vimfile](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/8010c08e-f73d-4e49-bc0e-dce694cf8a67)
![picture-13](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a2c65dce-14ba-4549-9bc9-4720ddc78bca)
![picture-14](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/e96a98e3-753f-4662-9bea-deaf863edd28)
![correct ouput for ngspice with 2 f](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/1af6fee1-f02f-474b-bda9-f7aa0b1776f7)
![y value](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/efda29db-b748-4d01-908a-27738e6b759e)
![risetime](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/0592c7a9-1b81-4e55-9be7-e3afb10b3dce)
![0 66 rise time graph](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4e012c28-738c-4717-8fcc-8106ae1eb885)
![falltime](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/822a9864-c6c8-4d47-ac0b-d74663d8ce8e)
![cellrisedelay cal](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/5e141322-58b8-479b-ad40-8d8e42c6958e)
![picture-15](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/9091c4e8-93e4-4fab-b081-826701af0b27)
![openingmagictool](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/70d6e12b-97a2-4a31-8802-967538335746)
![picture-16](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/8f62bd56-54ce-4515-91d4-c1bf995f8be9)
![drcwhy](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/3f77a0cd-1d14-4416-91c2-ea69f3ef4ee6)

![drcwhy2](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/33ccf175-7d09-44a9-be12-cfc9d0d6f616)
![cifseeVIA2](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/cda40377-45ef-415c-9635-31b7a3c75411)
![polyres](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/60355cb2-cbcf-40da-ac74-b7a56ed5bf2e)
![box violation](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/b8fd1478-5a52-4f19-8864-27cccc75f6e4)
![tech load](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4b8ec39c-1195-4b00-98a7-bca87e7982ed)
![tracksinfo](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4355dc57-ea9d-4d32-88a8-df2c14197f99)
![convergegridtotrack](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/0b909dfa-5acf-4183-a846-b3e644e36167)
![rule1checkedforrouting](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/58d73fa4-a25f-4c31-b06d-beaa46d94e1d)
![widthshouldbeinoddmultiplesofpitch](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/d6fb6148-52e6-4f9e-8aa6-32c5dd981434)
![lef file creation](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a5d11fc3-060d-4d3d-a224-c86056f9ac33)
![leffilecontents](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/322211b2-6f7f-4a38-a2c8-934410484832)
![newrunsynthesisprep](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/811eaf29-366e-4f9c-8b5c-e7e51efbc37c)
![taking our lef file ](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/e6a9fe29-c756-4683-897f-8deb1b90b608)
![synthesis of our custom cell](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/6c367d84-4c92-498c-a314-ad5f8d1a5e04)
![adjusting synthesis settings](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/f0124c51-3851-4459-9c26-da2decf72a26)
![leffileadded](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/e5954398-3c5a-45f5-826e-062d7b6cfeef)

![finalfloorplanrun](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/8d535dbc-ad28-4eff-b1a7-e528373f0f9b)

![sta slack value](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/2e1cfa5f-d1f7-4d85-a4f0-3ae633f5ad96)
![report net connections](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a94cb1ea-b236-4c7b-a07d-3bf3d655e012)


![report net connections-2](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a32f286b-d1c0-42d7-a231-bffd35fd70d3)
![picture-17](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/c9af6fd7-9659-4465-8b4a-b3b7eea12449)

![cts_run](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/cb39bdc1-5edb-48ed-b96d-9aca0882e8c1)
![cts file is added](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/11801e5c-9ff7-40e9-89cb-dbeccb25f0eb)
![db is created](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/79db48d5-354e-46f4-af95-0e5e2a91ffd0)
![writedb](https://github.com/RaagaS04/VSDPDW![can't read min and max](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/cd1037d2-d28f-4589-a073-471c0d019ead)
![reading sdc folder](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/3692de39-87f6-4cf8-bf7b-66ca5dc1a21c)
![slackmet](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/354c168d-a7f1-495b-b3e2-b33a02369fb4)
![now -8](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/da5ae1cc-21b2-4a5e-88a6-5925c5d63168)
![now-9](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/5243a798-6626-4313-872c-22a2c85506b4)

![checking procs](h![tocheck cell delay](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/fba5ab1c-83e8-41a9-b079-0aaa21581055)

![tocheck cell delay](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/96e5d0ec-821f-4920-8b30-02ee232387c4)

![includetypicallib](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/cb3f7197-6b02-4454-a037-2e98c5de7e51)

![slack for typical corner](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/5a79881d-37e0-421c-8b49-32dc78d92449)
![slack for typical corner2 ](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/f0da2dfd-634f-49ad-a363-776d37269f08)

![checking timing analysis with ideal clocks](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a4fd5e49-fafa-46e9-9461-1415f9eb1772)


![checking timing analysis with ideal clocks2](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/97239240-6b04-4e61-8473-c1e4ba3efd09)

![checking timing analysis with ideal clocks3](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/9af35104-47ea-464c-89db-2518ae222f1f)
![checking timing analysis with ideal clocks4](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/fb4a1e23-ad9e-44d1-95c3-2a46df9faec3)
![checking timing analysis with ideal clocks5](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/de441b04-2907-4a8d-89ff-b106bcf3f431)


![chec](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/05948729-46b0-4438-b1a3-27e5648515e9)



![checking timing analysis with ideal clocks6](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/a48553b0-290e-44b5-abf7-8dc92bb24868)

![now-10](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/08d79c1d-4475-4055-b4b8-96329f4f8e27)

![now-11](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/43066092-e976-4120-9406-b41e2d8d8b46)

![now-12](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/ae38df87-c77a-490d-82a3-d695f939f30d)
![now -13](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/b69970ca-a3f3-4373-859a-82a3e8e2ea49)
![now -14](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/e395a6ad-ea24-40e3-a534-dae3eddf7b44)

![now-15](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/936354a9-9492-4af5-97ba-c8d2c8d3e9aa)

![now-16](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/ac332451-dab0-4032-8254-32185c967de0)




