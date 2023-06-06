# VSDPDWORKSHOP
This is an overview of the notes that I wrote during the 5-day Advanced Physical Design using OpenLANE/Sky130 workshop. The aim is to utilize the open-source flow OpenLane with SKY130nm PDK to cover the whole RTL2GDS flow.
## 1. How to Talk to Computers?
![now-1](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/4c89ffc3-5a14-4656-9cb6-e4173e176139)
The core of the packaging will contain the chip. According to the figure, Chip is attached to the packaging.

PADS : A chip's internal or external signals can be sent it.

CORE: This is the location of all the digital logic.

The DIE is the total chip size. The silicon wafer will be used to produce die.
![now-2](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/345c311b-e41b-4f01-8d65-c044e0a88aa9)
Other details

<b> Foundry</b> – Place where the chips get manufactured.

<b> IP (Intelligent Properties)</b> – An Intellectual Property (IP) core in Semiconductors is a reusable unit of logic or functionality or a cell or a layout design that is normally developed with the idea of licencing to multiple vendor for using as building blocks in different chip designs.

<b>Macros</b> – Digital logic blocks

<b>RISC-V </b>-Instruction Set Architecture

<b>ISA </b> - The way we interact with computers.
![now -3](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/7845c1f3-b13e-4e38-a7e8-792e0cacd18f)

Suppose we want a C program to run on a particular layout. The C program is compiled into an assembly language program (RISC-V assembly language program). This assembly language program is converted into a machine language program (binary language program). The bits here will be executed in a layout, and we will get the required output.
![now -4](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/ad7e3b50-7b97-4642-96e6-dc4fc541f215)
The interface between RISC-V architecture and the layout is hardware description language. We implement RISC-V specifications in RTL.
## From software applications to hardware
The application software enters a block called system software. The system software converts the application software into binary language.
![now-4](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/741f1d57-890c-4640-8b26-cf44c47d4f95)
## The flow of System Software:
### OPERATING SYSTEM
OS Handles IO operations and allocates memory and low-level system functions. Converts the app into an assembly language program and finally into the binary language program so that the hardware understands it. The output of the operating system is the small functions in C, C++, Java, and VB.

These functions are taken by the respective compiler and convert them into instructions. The syntax of the instructions will depend on the type of hardware used (If the hardware is ARM, then the instructions will be in the ARM format) - .exe file.
### COMPILER
The instructions here will act as the abstract ISA between the hardware and the C programs.
![now -5](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/7097c50a-1610-47d5-8489-74075b578128)
We need an RTL to implement instruction specifications. The RTL is converted into a synthesized netlist (high-level specification into synthesized netlist). This will be in the form of gates. Above netlist generation, we follow physical design implementation.
![now -6](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/889e3218-8f73-44fb-84c8-87bfa7e013fb)
### ASSEMBLER
The job of the assembler is to take the instructions and convert them into binary numbers (machine language program). Based on machine language programs, the hardware executes the functions and accordingly generates the output.
Example: Stopwatch app
![now -7](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/67baa987-70d9-43c1-b3fb-a410521cdec6)
## Open Source EDA Tools

![picture-1](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/f85f34e2-c90f-4d6a-b899-bea9dfaaf1ca)


![picture-2](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/f48430d5-de6f-48dc-b80d-15a2cc2bf28a)

![picture-3](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/b8684d48-6fcb-49ff-907f-6cb6de645d90)
![dflipflopsno](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/3775eb04-221a-4bb3-9a80-bbcaffb565ad)
![No of cells](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/abaeea3c-b2ea-4d1f-8165-af844abac4bc)
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
ORKSHOP/assets/111308508/b9acce24-0ce7-4308-9360-7d0e2d3a931f)
![reading sdc folder](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/3692de39-87f6-4cf8-bf7b-66ca5dc1a21c)
![slackmet](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/354c168d-a7f1-495b-b3e2-b33a02369fb4)
![now -8](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/da5ae1cc-21b2-4a5e-88a6-5925c5d63168)
![now-9](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/5243a798-6626-4313-872c-22a2c85506b4)

![checking procs](h![tocheck cell delay](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/fba5ab1c-83e8-41a9-b079-0aaa21581055)

![tocheck cell delay](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/96e5d0ec-821f-4920-8b30-02ee232387c4)

![includetypicallib](https://github.com/RaagaS04/VSDPDWORKSHOP/assets/111308508/cb3f7197-6b02-4454-a037-2e98c5de7e51)

