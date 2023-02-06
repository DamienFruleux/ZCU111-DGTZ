# ZCU111 - Digitizer

## Summary : 

[Introduction](https://github.com/DamienFruleux/ZCU111-DGTZ/#introduction)

[ZCU111 Caracteristics](https://github.com/DamienFruleux/ZCU111-DGTZ/#ZCU111-Caracteristics)

[Key Features](https://github.com/DamienFruleux/ZCU111-DGTZ/##-Key-Features)

[Project Description](https://github.com/DamienFruleux/ZCU111-DGTZ/#Project-Description)

[Quick Start](https://github.com/DamienFruleux/ZCU111-DGTZ/#Quick-Start)

[Build the project](https://github.com/DamienFruleux/ZCU111-DGTZ/#Build-the-project)

[License](https://github.com/DamienFruleux/ZCU111-DGTZ/#License)

# Introduction

This project provides example designs for working with the [Zynq UltraScale+ RFSoC RF Data Converter](https://www.xilinx.com/products/intellectual-property/rf-data-converter.html) on the [Zynq UltraScale+ RFSoC ZCU111 Evaluation Kit](https://www.xilinx.com/products/boards-and-kits/zcu111.html). 

You can read the [Zynq UltraScale+ RFSoC RF Data Converter v2.6 Gen 1/2/3 Product Guide (PG269)](https://www.xilinx.com/content/dam/xilinx/support/documentation/ip_documentation/usp_rf_data_converter/v2_6/pg269-rf-data-converter.pdf) for more details on the IP core.

Specifically, we will use the ZCU111 as an fully customizable [Digitizer](https://en.wikipedia.org/wiki/Data_acquisition) (DGTZ). In this way, we will be able to acquire any signal with the [Analog to Digital Converter](https://en.wikipedia.org/wiki/Analog-to-digital_converter) (ADC) integrated to the ZCU111.

The big advantage of using a solution like this is the flexibility of the platform. In addition to using a fully customizable solution, it is possible to use IPs to enrich or accelerate our application with DSP, filters...

# ZCU111 Caracteristics

The ZCU111 features 8 12-bit ADCs that can sample a signal up to 4.096 GSa/s. 

Moreover, the board has 2 RAMs, both of which can be used in these examples: 

- 4GB DDR4 Component, attached to Programmable Logic (PL)

- 4GB DDR4 SODIMM (scalable up to 32GB), attached to Processor Subsystem (PS) 

Of course, the card has its limits (which depend among other things on the memory used), which I detail [here](https://github.com/DamienFruleux/ZCU111-Doc/tree/main/1-AXI_DMA).

# Key Features

These examples allow to acquire 2 analog signals at a sampling frequency previously established. The duration of the signal (or the number of samples) and the sampling frequency will depend on the type of memory used: PS or PL.

In order to have 2 perfectly synchronized signals, I use a single signal which contains on the even numbers a signal A and on the odd numbers a signal B. It is thus necessary to send to the DMA a global signal which alternates the samples of signals A and B. I then realized an IP which separates this signal in 2 independent signals. More informations available [here](https://github.com/DamienFruleux/ZCU111-Doc/tree/main/2-AXI-Stream_RF-Data-Converter).

In each example file, you will find more details about the features of this example.

# Project Description

I use **Vivado 2018.3** to design and generate the bitstream and **Pynq 2.6** to run Jupyter Notebooks (or C programs).

Each example of DGTZ has a different sampling frequency and therefore adapted clocks and memory used. In each example folder, you will find 2 subfolders: 

- The project already built in the *build* folder. This can be useful for a first quick test.

- The design sources available in the *vivado* folder. If you need to modify it.

In order to use these different examples, you have to use the PS. However, there are different possibilities 

- In the folder *pynq_notebook* you will find an example of a notebook that uses the pynq libraries. This one is quite simple to use, but limited for some features However, it is perfectly suitable for running the AWG in an initial instance.

- In the *C_codes* folder (in progress), you will find a C code that uses the standard POSIX libraries. This one is more complicated to use, but allows more flexibility, especially by being able to choose the memory used. This one allows a programming closer to the machine, what I like most.

- In the *python_notebook* folder (in progress), you will find an example notebook that uses the standard python libraries. It does the same thing as the C code (in fact, the python notebook is a simple rewriting of the C code). I wrote a python notebook because it is easier to use at first, especially for people not experienced with C. However, keep in mind that C being more powerful than python, it may be necessary in some cases.

Be careful, in these last 2 cases, I suppose you have changed the SODIMM memory for a capacity higher than 8 Gb. 

In any case, you will find more informations [here](https://github.com/DamienFruleux/ZCU111-Doc/tree/main/3-Processing-System_C-programming-method).

# Quick Start (using build project & pynq_notebook)

You can follow the same instructions as [here](https://github.com/strath-sdr/rfsoc_qpsk#quick-start) and [here](https://github.com/strath-sdr/rfsoc_qpsk#zcu111-setup). 

Specifically, you need to :

- clone the repo directly in the ZCU111 (or clone it on a computer and copy files to the ZCU111) : ```git clone https://github.com/DamienFruleux/ZCU111-DGTZ```
- load the **pynq_notebook** in Jupyter : ```http://<board_ip_address>:9090/lab```
- and run it :)

# Build the project (in progress)

In your computer :

- source the Vivado 2018.3 path : ```<path_to_vivado>/2018.3/settings64.sh```
- clone the repo : ```git clone https://github.com/DamienFruleux/ZCU111-AWG```
- move into the vivado folder : ```cd ZCU111-AWG/vivado```
- run ```make```
- import the freshly generated files into the ZCU111: ```scp -r /my_build/* xilinx@<board_ip_address>/ZCU111-DGTZ/```.
- load the **pynq_notebook** in Jupyter : ```http://<board_ip_address>:9090/lab```
- and run it :)

# License

[BSD 3-Clause](https://github.com/DamienFruleux/ZCU111-AWG/blob/main/LICENSE)
