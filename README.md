# Power-Estimation-Using-Xilinx-XPE

[XPE : Introduction to Xilinx Power Estimator](#XPE)

[Day 2 : Introduction to ABI and Basic Verification Flow](#day-2)

[Day 3 : Digital Logic with TL-Verilog and Makerchip](#day-3)

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

dia

### Using the Settings Panel

To configure the device, board, cooling, and ISE or AMD VivadoTM Design Suite parameters, use the parameters page. The targeted device determines how this panel changes. The figure below shows an example of a Kintex UltraScale device.

Certain options rely on other settings. The dependent cell transforms to a gray background and loses its ability to be edited at that point.

dia

