Introduction
-------------
This document will show you how to get started with the `Avnet Wideband mmWave Radio Development Kit for RFSoC Gen-3 <https://www.avnet.com/rfsoc-mmw>`_. Follow the step-by-step instructions to configure the kit, setup your computer, and use Avnet RFSoC Explorer® in MATLAB to generate and acquire signals through the Otava DTRX2 Dual Transceiver mmWave Radio Card.

.. image:: images_system_setup/zcu208_dtrx2_kit.png

Kit Overview
------------
The Avnet Wideband mmWave Radio Development Kit for RFSoC Gen-3 is ideal for prototyping RF applications in mmW bands including 5G NR FR2, wireless backhaul, as well as K/Ka band radar and SATCOM. This platform combines the Otava DTRX2 Dual Transceiver mmWave Radio Card — jointly developed by Otava and Avnet — with the Xilinx Zynq ® UltraScale+ ™ RFSoC ZCU208 Evaluation Kit.

.. warning:: This kit can radiate radio frequency energy and has not been tested for CE, FCC, or IC compliance. The intended use is for demonstration, engineering development, or evaluation purposes. See :ref:`compliance`

Required Equipment
------------------
In addition to the mmWave kit, you will need the following.

* Laptop or PC running Windows 10 OS
* Bench power supply for 12V, 2A min 
* 40GHz Spectrum analyzer for Transmitter tests
* 40GHz Signal generator for Receiver tests


Install RFSoC Explorer
----------------------
Avnet RFSoC Explorer provides native connection to MATLAB ® and Simulink ®, featuring graphical control of the platform and intuitive APIs for programmatic access.

.. image:: images_system_setup/rfsocX-concept.jpg

Your computer will need the following MathWorks software. 

* MATLAB R2021a or later 
* DSP System Toolbox
* Fixed-Point Designer
* Communications Toolbox
* Communications Toolbox Support Package for Xilinx Zynq-Based Radio
* Signal Processing Toolbox
* LTE Toolbox (optional)
* 5G Toolbox (optional)

`Get a Free MATLAB Trial Package for RFSoC <https://www.mathworks.com/rfsoc>`_

RFSoC Explorer installs easily using the MATLAB Add-Ons store.

1)	From **MATLAB > Add-Ons**, search for **Avnet RFSoC Explorer** and click install
2)	From **MATLAB > Add-Ons**, search for **Communications Toolbox Support Package for Xilinx Zynq-Based Radio** and click install
3) If prompted, click **Setup Later**

.. image:: images_system_setup/mw-addon.png

Hardware Setup
----------------
The Xilinx ZCU208 Evaluation Kit has many jumpers and switches that are shipped with default states, which do not need to change for this tutorial. In the following steps we describe the minimal configuration. For a comprehensive setup guide, refer to the online `Xilinx ZCU208 Quick Start Wiki <https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/569017820/RF+DC+Evaluation+Tool+for+ZCU208+board+-+Quick+Start>`_

.. image:: images_system_setup/hw-setup.jpg


#. Connect the Xilinx CLK104 module to the ZCU208 with the included screws
#. Connect the Otava DTRX2 mmWave Card to the ZCU208 with the included screws
#. Connect the ZCU208 to your host PC with Ethernet and USB cables as shown in the picture
#. **DO NOT CONNECT POWER TO THE DTRX2 CARD** (this will be done later)
#. Use a Carlisle SMA cable from the ZCU208 kit to connect **CLK104** OUTPUT_REF (J10) to **DTRX2** REF CLK IN (J21). 

.. note:: For reference clock spurious mitigation, we recommend a 10dB coaxial attenuator between the CLK104 output and the REF_CLK_IN input on the DTRX2 card

6. Connect DTRX2 RF inputs/outputs to test equipment using 2.92mm mmW coaxial cables

   * TX output @ J3 (Ch1) and J6 (Ch2)
   * RX input @ J10 (Ch1) and J15 (Ch2)

.. warning:: All unused channels on DTRX2 must be connected to 50 ohm terminations.

7. Set ZCU208 to boot from the SD card by setting (SW6) switches as shown below

.. image:: images_system_setup/zcu208-dip-sw.png

SD Card
-------
The ZCU208 requires custom software to control DTRX2 card via RFSoC Explorer.

#. Remove the SD card from the ZCU208, insert into your PC, and format as FAT using a tool like `SD Memory Card Formatter <https://www.sdcard.org/downloads/formatter_4/>`_

#. Download the file **avnet_rfsocX_zcu208_boot_v1_0.zip** @ *>>> TBC SURL <<<*

#. Unzip the archive and copy the files to the root level of the SD card. 

#. Safely eject the SD card from the PC and replace into ZCU208.

Boot ZCU208
------------
#. Ensure no power is applied to DTRX2

#. Turn the ZCU208 power switch ON (near the 12V connector) 

#. The application auto-start function creates an IP connection for the board at address **169.254.10.2**. 

#. Set a static IP for your host PC's Local Ethernet adapter.  Make sure your PC and the board are on the same subnet and gateway. See example below.

.. image:: images_system_setup/network-cfg.png
.. image:: images_system_setup/laptop-ip.jpg


.. note:: The auto-start IP address can be changed in the autostart.sh file on your SD card. 


Start RFSoC Explorer
--------------------

#. Open MATLAB and start RFSoC Explorer by entering the following command: 

   ``rfx = Avnet_RFSoC_Explorer(‘target board’, 4);``

.. image:: images_system_setup/rfsocX_main_tab.jpg

#. On the Main tab, enter the IP address of the ZCU208 -- default addess: **169.254.10.2**

.. image:: images_system_setup/rfsocX_ipaddress.jpg
    :scale: 75%
    :align: center

.. note:: You may need to maximize the RFSoC Explorer window to reveal the IP Address dropdown

Configure System Reference Clocks
----------------------------------
The CLK104 module provides an ultra low-noise, wideband RF clock source for the ZCU208 RF-ADCs and RF-DACs. We use RFSoC Explorer to configure CLK104 to ouptut a coherent reference for the DTRX2 LO PLLs.

.. image:: images_system_setup/CLK104.png

#. Go to the RFSoC Explorer Main tab
#. Select **CLK104 Configuration > 122.88MHz REFCLKOUT_10MHz TCXO REF**

.. image:: images_system_setup/clk104_config.jpg
    :scale: 75%

.. note:: The **122.88MHz REFCLKOUT_10MHz TCXO REF** configuration uses the CLK104 on-board 10MHz TCXO reference for the LMK04828B. If you wish to synchronize the setup up to a test instrument 10MHz clock, use the **122.88MHz REFCLKOUT_10MHz EXT REF** configuration (typically useful for EVM measurements). 

Power Up DTRX2
---------------
#. Connect your test equipment to the DTRX2 RF and TX ports
#. Terminate unused channels with a 2.92mm 50 ohms termination
#. Apply 12V DC power to the DTRX2 card

Both D4 and D6 "Power Good" red LEDs should be lit. The idle current drawn from the 12V supply should be about 45mA.
