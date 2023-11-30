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


</details>

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


</details>

<details> 
<summary> MachSuite / kmp </summary>

The following image shows the process of converting the C/C++ file to verilog using vitis


![hls](https://github.com/mavi62/RISC-V/assets/57127783/33a267f0-a714-473c-b4ca-89116c6e90e8)


The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![vivado](https://github.com/mavi62/RISC-V/assets/57127783/9247de9a-4cf1-41b0-8513-a9ae6459b08f)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/b0694b21-be94-4e62-b2b4-0aea6b2e0688)


The i/o used in the design is displayed in this picture.


![xpe_io](https://github.com/mavi62/RISC-V/assets/57127783/a4adcf0a-5734-4dc2-a18b-c68fe0d497a0)


The static current by supply is displayed in this graphic.


![static_current_supply](https://github.com/mavi62/RISC-V/assets/57127783/d1bda56e-76ca-45df-9a50-8f85371ed66d)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/31d3aa72-793a-418c-a7a0-ea5574c68525)


</details>

<details> 
<summary> MachSuite / stencil / stencil2D </summary>

The following image shows the process of converting the C/C++ file to verilog using vitis


![hls](https://github.com/mavi62/RISC-V/assets/57127783/885e1307-cb08-443a-bccc-e708ba4c66d4)


The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![vivado](https://github.com/mavi62/RISC-V/assets/57127783/a91c2937-0f63-4ba3-9922-047f50d51b9d)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/f8349dac-e692-45bd-aead-9ae7b540034c)


The i/o used in the design is displayed in this picture.


![xpe_io](https://github.com/mavi62/RISC-V/assets/57127783/f0b52a42-d14f-44a6-9c05-facc9868d53a)


The static current by supply is displayed in this graphic.


![static_current_supply](https://github.com/mavi62/RISC-V/assets/57127783/5c0826cb-333b-4ab0-b6fb-9455923c3a97)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/f9cb26f6-178e-4b96-b843-ae388a4d279a)


</details>

<details> 
<summary> MachSuite / stencil / stencil3D </summary>

The following image shows the process of converting the C/C++ file to verilog using vitis


![hls](https://github.com/mavi62/RISC-V/assets/57127783/163efff7-bcbe-4dd9-b64d-eed6eb96ee1c)


The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![vivado](https://github.com/mavi62/RISC-V/assets/57127783/59f1822e-168f-45f8-8352-bf2f4e2ba177)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/c0c8cd28-829f-41cd-b829-d4ad083d498e)


The i/o used in the design is displayed in this picture.


![xpe_io](https://github.com/mavi62/RISC-V/assets/57127783/1742d306-f981-4be7-8c15-14fb7af76b35)


The static current by supply is displayed in this graphic.


![static_current_supply](https://github.com/mavi62/RISC-V/assets/57127783/803ae3cf-7a2f-4442-a3a4-bb4a51d1b80a)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/052bb038-b5ca-4cf7-8338-1227efb0c3c8)


</details>

<details> 
<summary> MachSuite / fft / strided </summary>

The following image shows the process of converting the C/C++ file to verilog using vitis


![hls](https://github.com/mavi62/RISC-V/assets/57127783/76991fcf-e47c-43ea-ba6a-7df50a3b375c)


The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![vivado](https://github.com/mavi62/RISC-V/assets/57127783/130f8d57-c0b3-4e89-aaed-2d59e56a60dd)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/60ce9524-4db8-4308-b050-86c5c884fbcc)


The i/o used in the design is displayed in this picture.


![xpe_io](https://github.com/mavi62/RISC-V/assets/57127783/7b7e83ca-6ba1-4fae-b039-10966db521bc)


The static current by supply is displayed in this graphic.


![static_current_supply](https://github.com/mavi62/RISC-V/assets/57127783/8cea6426-34fd-49ef-b088-cb9917ae7601)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/fa532611-0b19-4006-ae75-5104a61dd213)


</details>

<details> 
<summary> MachSuite / sort / merge </summary>

The following image shows the process of converting the C/C++ file to verilog using vitis


![hls](https://github.com/mavi62/RISC-V/assets/57127783/912a8882-9b28-4da2-adb7-1116bc1c4335)


The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![vivado](https://github.com/mavi62/RISC-V/assets/57127783/543a795b-03a9-4ea4-812a-358a4cc805e2)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/1c8c9ec2-a837-42fe-8f08-38665823f9a5)


The i/o used in the design is displayed in this picture.


![xpe_io](https://github.com/mavi62/RISC-V/assets/57127783/0472a4ee-cbfc-4162-ac37-f3b4fb87453d)


The static current by supply is displayed in this graphic.


![static_current_supply](https://github.com/mavi62/RISC-V/assets/57127783/d2263cdf-57fd-4f41-a7fe-9ae796c0a41b)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/93c7c342-bc27-4af1-9e54-bb09922f9c83)


</details>

<details> 
<summary> MachSuite / sort / radix </summary>

The following image shows the process of converting the C/C++ file to verilog using vitis


![hls](https://github.com/mavi62/RISC-V/assets/57127783/0fab4575-a84f-4284-833a-48d785606004)


The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![vivado](https://github.com/mavi62/RISC-V/assets/57127783/1a1f54fe-6bce-4d31-9866-87ac977ff169)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/ebbd5606-576e-479b-9a47-d9cef40d2245)


The i/o used in the design is displayed in this picture.


![xpe_10](https://github.com/mavi62/RISC-V/assets/57127783/29c59610-07a3-4c81-a61d-b1f00c555f28)


The static current by supply is displayed in this graphic.


![static_current_supply](https://github.com/mavi62/RISC-V/assets/57127783/3c607c62-874b-4b58-8810-6a4b413a555e)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/8b9434e7-d24b-420f-876e-12a601b4a868)


</details>

<details> 
<summary> MachSuite / gemm / ncubed </summary>

The following image shows the process of converting the C/C++ file to verilog using vitis


![hls](https://github.com/mavi62/RISC-V/assets/57127783/81c165a2-ce56-45d2-87a2-1222edd5f6ef)


The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![vivado](https://github.com/mavi62/RISC-V/assets/57127783/f6e4e64a-1aca-4cd2-98fd-df6486f7063e)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/8b333cd8-4ff5-4ac7-995f-ee626d6271a2)


The i/o used in the design is displayed in this picture.


![xpe_io](https://github.com/mavi62/RISC-V/assets/57127783/26975a54-103d-44ce-9690-cc7d480eca4f)


The static current by supply is displayed in this graphic.


![static_current_supply](https://github.com/mavi62/RISC-V/assets/57127783/87c15054-8521-4491-87ab-c6ba3532fca3)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/95cb3abd-9181-4d77-b39c-3a14dd22ea63)


</details>

<details> 
<summary> MachSuite / nw </summary>

The following image shows the process of converting the C/C++ file to verilog using vitis


![hls](https://github.com/mavi62/RISC-V/assets/57127783/457cee6a-d025-483b-a144-7de2a50cd197)


The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![vivado](https://github.com/mavi62/RISC-V/assets/57127783/e212d548-eb58-4a91-bf90-5f9b61f50bea)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/68f13cae-316c-4c63-b2bf-32d701bc5055)


The i/o used in the design is displayed in this picture.


![xpe_io](https://github.com/mavi62/RISC-V/assets/57127783/3f190a1f-fb79-4425-b670-ab5b56001551)


The static current by supply is displayed in this graphic.


![static_current_supply](https://github.com/mavi62/RISC-V/assets/57127783/a59cd8b2-a97a-4cf7-9d7a-cd9019cdef6f)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/f086ad7b-f59b-4e83-a633-d8ffb193b28d)


</details>

<details> 
<summary> float_mac_full </summary>

The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![vivado](https://github.com/mavi62/RISC-V/assets/57127783/83874e39-1edb-4f11-aa46-dcda79b9d5de)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/d8fea675-eb6d-4b4e-a8a6-c776e7c1147d)


The i/o used in the design is displayed in this picture.


![xpe_io](https://github.com/mavi62/RISC-V/assets/57127783/de69729f-ea2b-4d57-a1f9-ca66706f8e72)


The static current by supply is displayed in this graphic.


![static_current_supply](https://github.com/mavi62/RISC-V/assets/57127783/8ac6a6b2-48ab-4428-943e-120fa99e9501)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/dac5e2fb-eed1-453c-933a-6597c78ab8d8)


</details>

<details> 
<summary> systolic </summary>

The procedure of utilizing Xilinx Vivado to determine the design's power is summed up in the graphic below.


![vivado](https://github.com/mavi62/RISC-V/assets/57127783/51a47ed4-8895-4ee7-8ee7-57926b6d160e)


This image displays the power estimate for the design in advance using XPE.


![xpe_summary](https://github.com/mavi62/RISC-V/assets/57127783/5b650743-687d-41ed-adb6-9105b71ef7ab)


The i/o used in the design is displayed in this picture.


![xpe_io](https://github.com/mavi62/RISC-V/assets/57127783/b6e308f2-655e-4ac9-ba3f-e9b58cbd535f)


The static current by supply is displayed in this graphic.


![static_current_supply](https://github.com/mavi62/RISC-V/assets/57127783/32fce3d5-38f7-48e7-ba28-12882c9d1b0f)


This graph displays the overall power used by the design versus the design's static power consumption.


![total_vs_static](https://github.com/mavi62/RISC-V/assets/57127783/8ae3ff07-2256-4f3e-98f6-d7a209cc5d58)


</details>

## Word of Thanks
I sciencerly thank **Ms. Nandhita Rao** and my mentor **Lokesh Maji** for helping me out to complete this project.
  
## Reference 
- https://www.xilinx.com/video/fpga/estimate-ultrascale-device-power-using-xpe.html
- https://docs.xilinx.com/r/en-US/ug440-xilinx-power-estimator/Overview?tocId=Y1uKjFKcrvyAof2G4G~cmw
- https://www.xilinx.com/content/dam/xilinx/support/packagefiles/usapackages/xcku035fbva900pkg.txt
- https://verificationguide.com/verilog-examples/
- https://www.digikey.at/htmldatasheets/production/1952540/0/0/1/UltraScale-Ultrascale-FPGAs-Specification.pdf
- https://docs.xilinx.com/v/u/en-US/ug475_7Series_Pkg_Pinout
- https://www.xilinx.com/products/technology/power/xpe.html
