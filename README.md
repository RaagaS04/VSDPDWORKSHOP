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


![picture -4](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/25f7e0ea-4522-409b-8bbb-210b25e4bfe0)
![diearea](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/5aefb4d9-bf4b-4a25-8529-a929fb1b0db1)
![magic layo![picture 5](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/6aca00e2-8085-48c1-a151-46914144cbc6)
![picture 5](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/667c3573-8e2f-48f6-828b-7fe0cf2cc166)
![what](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/778b390c-22ad-4168-ad87-fc20b48938b8)
![nand](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/7815c33c-5952-49b0-a670-357fd9854d9d)

![picture -6](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/fd9f735a-fb3d-4639-a7e2-e8b82e5eb94a)
![picture 6](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/2c8a77a2-8ffc-419c-8604-b9555dbec7b5)

![picture-8](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/b770ba80-1d77-4fea-a074-5625add311c1)

![changemode2](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4555994d-adda-46b2-89ce-f73756d65bb4)
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




