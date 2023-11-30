# Power-Estimation-Using-Xilinx-XPE

[XPE : Introduction to Xilinx Power Estimator](#XPE)

[MachSuite & Package Used](#Machsuite)

[Power Estimation](#Power-Estimation)

[Day 4 : Basic RISC-V CPU Micro-Architecture](#day-4)

[Day 5 : Pipelined RISC-V CPU Micro-architecture](#day-5)

## XPE 

<details> 
<summary> Introduction </summary>

Xilinx Power Estimator (XPE) is a power estimating tool commonly used in the pre-design and pre-implementation stages of a project. For our application, XPE helps with device selection, architectural evaluation, choosing the right power supply components, and selecting components for thermal control.

To compute the expected power distribution, XPE takes into account toggling rates, I/O loading, resource utilization in your design, and a host of other aspects that it integrates with the device models. The device models are taken via extrapolation, modeling, and/or measurements. Two main sets of inputs determine the accuracy of XPE:
  - Information we enter into the tool, such as device consumption, component configuration, clock, enable, and toggling rates
  - Integrated device data models within the tool

We provide as much complete and realistic information as we can for our application to be estimated accurately. Unrealistic estimations can arise when a particular feature of the design is modeled too conservatively or when the design is not sufficiently understood.

</details>

<details> 
<summary> Getting Started </summary>

1. Microsoft Office 365 must be installed before using XPE.
2. For the device we are targeting, we get the most recent spreadsheet available. The XPE spreadsheets are available [here](https://www.xilinx.com/products/technology/power/xpe.html)
3. Verify that macro executions are permitted in the Microsoft Excel settings. Several macros included in the XPE spreadsheet are used by XPE.

Because power estimation for programmable devices, such as FPGAs, is highly reliant on the quantity and arrangement of logic in the design, it is a complicated procedure. The power estimation procedure needs precise input numbers, such as resource utilization, clock rates, and toggling rates, in order to generate reliable estimations.

We need the following in order to provide the minimal input required for XPE to estimate power with a decent degree of accuracy:
- A target device-package-grade combination
- A good estimate of resources we expect to use in the design (for example, flip-flops, look-up tables, I/Os, block RAMs, DCMs or MMCMs, and PLLs.)
- The clock frequency or frequencies for the design
- An estimate of the data toggle rates for the design
- The external memory and transceiver based interfaces with their data rates for the design
- The thermal environment in which the design operates

Generally speaking, enter as much information as you can about the design and then set the rest of the options to default. We can calculate the device's power supply and heat dissipation needs using this method.

</details>

<details> 
<summary> XPE User Interface </summary>

We can enter and modify all of the environment and device parameters on the Summary sheet. A summary of the power distribution is also shown on this sheet, along with options for data import into XPE, results export, and global setting adjustments.


![summary](https://github.com/mavi62/RISC-V/assets/57127783/b1fc0884-950d-4d5d-9e33-ee8b8bf0b939)


### Using the Settings Panel

To configure the device, board, cooling, and ISE or AMD VivadoTM Design Suite parameters, use the parameters page. The targeted device determines how this panel changes. The figure below shows an example of a Kintex UltraScale device.

Certain options rely on other settings. The dependent cell transforms to a gray background and loses its ability to be edited at that point.


![settings](https://github.com/mavi62/RISC-V/assets/57127783/e794ebdd-af32-4e3c-84f9-ee38f92f48ab)


### Using the XPE Toolbar

XPE facilitates the import of data from various sources and enables global configuration changes to facilitate data entry into the tool. The toolbar is displayed in the figure that follows:


![toolbar](https://github.com/mavi62/RISC-V/assets/57127783/de950195-08ee-462c-b972-fca21b0d22d8)


</details>

## Machsuite

<details> 
<summary> MachSuite </summary>

MachSuite is a benchmark suite intended for accelerator-centric research.

To know more about it check [here](https://github.com/breagen/MachSuite)

I utilized [HLS Vitis](https://www.xilinx.com/products/design-tools/vitis/vitis-hls.html) to synthesize the C/C++ codes from Machsuite into verilog files, which I then used in [Xilinx Vivado](https://www.xilinx.com/products/design-tools/vivado.html) to further synthesize the design.

</details>

<details> 
<summary> Device Used </summary>

For the project I have used [xcku035-fbva900-1-c](https://docs.xilinx.com/v/u/en-US/ug475_7Series_Pkg_Pinout).

This figure shows the I/O Banks in the device.


![pinout - 1](https://github.com/mavi62/RISC-V/assets/57127783/9dfe9f10-a58c-44e6-835c-9d1c03842efb)


This figure shows the Configuration/Power diagram


![pinout - 2](https://github.com/mavi62/RISC-V/assets/57127783/f08c5eec-58f8-4ad7-b13d-a31359567523)


Banks in FBVA900 package.


![banks](https://github.com/mavi62/RISC-V/assets/57127783/61aa99a3-d322-43cb-8d53-339d03c9d1f1)


</details>

## Power Estimation

<details> 
<summary> MachSuite / bfs / bulk </summary>

The following image shows the process of converting the C/C++ file to verilog using vitis


![hls](https://github.com/mavi62/RISC-V/assets/57127783/e1f7b4ba-b9c0-4969-9d77-67f2a1d1bc47)


The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![synth_vivado](https://github.com/mavi62/RISC-V/assets/57127783/32836b28-bcd7-4155-b393-fa9a8d30191b)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/614a6fa5-7956-4042-8b11-6726274251aa)


The i/o used in the design is displayed in this picture.


![xpe_io](https://github.com/mavi62/RISC-V/assets/57127783/7c0c3152-eb69-4163-b3ac-8600b320c5b9)


The static current by supply is displayed in this graphic.


![static_current _supply](https://github.com/mavi62/RISC-V/assets/57127783/069bcd6d-0b90-4719-ad6d-940246e58c89)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/3ca0f017-c67e-4770-8ac5-450886f6a444)


<details>

<details> 
<summary> MachSuite / bfs / queue </summary>

The following image shows the process of converting the C/C++ file to verilog using vitis


![hls](https://github.com/mavi62/RISC-V/assets/57127783/a2ad9cc8-e906-4bf2-8ad3-e6c9cad47079)


The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![synth_vivado](https://github.com/mavi62/RISC-V/assets/57127783/5a3a1c1a-9c7c-4ed1-b374-9a479a27075d)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/7fc39b4d-a840-4aaf-948c-935373846385)


The i/o used in the design is displayed in this picture.


![xpe_io](https://github.com/mavi62/RISC-V/assets/57127783/6bac1382-8804-41d8-9ce3-67e5d336ab1e)


The static current by supply is displayed in this graphic.


![static_current_supply](https://github.com/mavi62/RISC-V/assets/57127783/3e4c50fa-48d7-4584-bad2-df0820994448)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/9ab43755-92ad-450e-8024-70548645f0e4)


