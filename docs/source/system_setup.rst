System Setup
============

This document will show you how to get started with the `Avnet Wideband mmWave Radio Development Kit for RFSoC Gen-3 <https://www.avnet.com/rfsoc-mmw>`_. Follow the step-by-step instructions to assemble the kit, setup your computer, and use Avnet RFSoC Explorer® in MATLAB to configure the Otava DTRX2 Dual Transceiver mmWave Radio Card, generate and acquire signals.

.. image:: images_system_setup/zcu208_dtrx2_kit.png

Kit Overview
------------
The Avnet Wideband mmWave Radio Development Kit for RFSoC Gen-3 is ideal for prototyping RF applications in mmW bands including 5G NR FR2, wireless backhaul, as well as K/Ka band radar and SATCOM. This platform combines the Otava DTRX2 Dual Transceiver mmWave Radio Card — jointly developed by Otava and Avnet — with the Xilinx Zynq ® UltraScale+ ™ RFSoC ZCU208 Evaluation Kit.

.. warning:: This kit can radiate radio frequency energy and has not been tested for CE, FCC, or IC compliance. The intended use is for demonstration, engineering development, or evaluation purposes. See :doc:`Regulatory Compliance Information <./compliance>`

Kit Includes
^^^^^^^^^^^^
* Xilinx Zynq UltraScale+ RFSoC ZCU208 Evaluation Kit (full OEM kit)
* Otava DTRX2 mmWave Radio Daughtercard
* DC barrel jack to banana plug cable for DTRX2
* Avnet RFSoC Explorer for MATLAB and Simulink

.. image:: images_system_setup/mmw_full_kit_PB.jpg

Required Equipment
------------------
In addition to the mmWave kit, you will need the following.

* Laptop or PC running Windows 10 OS
* Bench power supply for 12V, 2A min 
* 40GHz Spectrum analyzer for Transmitter tests
* 40GHz Signal generator for Receiver tests
* 1x or more RF coaxial cables (2.92mm to 2.92 or 2.4mm on test equipment)
* 3x 2.92mm male 50-ohm terminations (rated for 40GHz, 0.5W or higher)
* 1x RF SMA coax cable to connect the CLK104 Reference Clock (in the kit)
* 1x 10dB SMA coaxial attenuator (for DTRX2 Ref clock input port)
* Optional – n258, n257, n260 band-pass filters
* 12V jack to banana plug DC electrical wires (in the kit)


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
The Xilinx ZCU208 Evaluation Kit has many jumpers and switches that are shipped with default states, which do not need to change for this tutorial. In the following steps we describe the minimal configuration. For a comprehensive setup guide, refer to the `ZCU208 Software Install and Board Setup <https://www.xilinx.com/support/documentation/boards_and_kits/zcu208/2020_1/xtp607-zcu208-setup-c-2020-1.pdf>`_

.. image:: images_system_setup/hw-setup.jpg

**Refer to the diagram above when making the following connections.**

#. Connect the Xilinx CLK104 module to the ZCU208 with the included screws
#. Connect the Otava DTRX2 mmWave Card to the ZCU208 with the included screws
#. Connect the ZCU208 to your PC with Ethernet and USB cables. *USB is optional for terminal access to Linux running on the board.*
#. **DO NOT CONNECT POWER TO THE DTRX2 CARD** (this will be done later)
#. Use a Carlisle SMA cable from the ZCU208 kit to connect **CLK104** OUTPUT_REF (J10) to **DTRX2** REF CLK IN (J21). 

.. note:: For reference clock spurious mitigation, we recommend a 10dB coaxial attenuator between the CLK104 output and the REF_CLK_IN input on the DTRX2 card

6. Connect DTRX2 RF inputs/outputs to test equipment using 2.92mm mmW coaxial cables

   * TX outputs @ J3 (Ch1) and J6 (Ch2)
   * RX inputs @ J10 (Ch1) and J15 (Ch2)

.. warning:: All unused RF channels input/output connectors on the DTRX2 radio card must be terminated with 50 ohms 2.92mm terminations.

7. Set ZCU208 to boot from the SD card by setting (SW6) switches as shown below

.. image:: images_system_setup/zcu208-dip-sw.png

Prepare SD Card
---------------
The ZCU208 requires custom software to control DTRX2 card via RFSoC Explorer.

#. Remove the SD card from the ZCU208, insert into your PC, and format as FAT using a tool like `SD Memory Card Formatter <https://www.sdcard.org/downloads/formatter_4/>`_

#. Download the file **avnet_rfsocX_zcu208_boot_v1_0.zip** @ *>>> TBC SURL <<<*

#. Unzip the archive and copy the files to the root level of the SD card

#. Safely eject the SD card from the PC and replace into ZCU208

Boot & Network Configuration
----------------------------
The default way to connect to the board is by setting a static IP address on your host PC. We also include instructions for connecting the board to a networked router and allowing the board to use DHCP to obtain an IP address.

Static IP (default)
^^^^^^^^^^^^^^^^^^^
Use this method when connecting the ZCU208 directly to your PC.

#. Ensure no power is applied to DTRX2

#. Turn the ZCU208 power switch ON (near the 12V connector) 

#. The application auto-start function creates an IP connection for the board at address **169.254.10.2**

#. Set a static IP for your host PC's Local Ethernet adapter.  Make sure your PC and the board are on the same subnet and gateway. See example below

.. image:: images_system_setup/network-cfg.png
.. image:: images_system_setup/laptop-ip.jpg

The static IP address of the board can be changed by modifying the **autostart.sh** file on the SD card. Simply change the ``IPADDR`` field as needed and reboot. 

::

    # Static IP address (you can set to this to whatever works for you)
    IPADDR="169.254.10.2"

DHCP IP
^^^^^^^
Use this method when connecting the ZCU208 to your PC using a network (via Ethernet router for instance). You will need a USB cable connected to the mini-USB port on the ZCU208 board and your PC.

#. First, remove the SD card from the ZCU208 and insert into your PC
#. Open the **autostart.sh** file and set ``USE_DHCP=true``

::

    # Set true if your network assigns an IP address via DHCP
    # Set false for static IP address
    USE_DHCP=true

5. Safely eject the SD card from the PC and replace into ZCU208
6. Open a serial terminal emulator on your PC and select the COM port assigned to the board. You may need to experiment with the list of connected COM ports to find which one is assigned to the ZCU208
7. Turn the ZCU208 power switch ON (near the 12V connector)
   
.. note:: For help installing the ZCU208 USB-UART driver and setting up a serial terminal emulator, consult `ZCU208 Software Install and Board Setup <https://www.xilinx.com/support/documentation/boards_and_kits/zcu208/2020_1/xtp607-zcu208-setup-c-2020-1.pdf>`_

8. Login into the ZCU208 as ``login: root  Password: root``
9. Discover the board IP address using the command ``ifconfig``. 
   **Take note of this IP address** You will use it in the next section to connect RFSoC Explorer.

.. image:: images_system_setup/ifconfig.jpg


Start RFSoC Explorer
--------------------

#. Open MATLAB and start RFSoC Explorer by entering the following command: 

   ``rfx = Avnet_RFSoC_Explorer(‘target board’, 4);``

.. image:: images_system_setup/rfsocX_main_tab.jpg

#. On the Main tab, under "System", enter the IP address of the ZCU208 -- default addess: **169.254.10.2**

.. image:: images_system_setup/rfsocX_ipaddress.jpg
    :scale: 75%
    :align: center

.. note:: You may need to maximize the RFSoC Explorer window to reveal the IP Address dropdown

Configure System Reference Clocks
----------------------------------
The CLK104 module provides an ultra low-noise, wideband RF clock source for the ZCU208 RF-ADCs and RF-DACs. We use the RFSoC Explorer to configure CLK104 to ouptut a coherent 122.88MHz reference for the DTRX2 LO PLLs. For more information refer to `Xilinx UG1437 - CLK104 RF Clock Add-onCard <https://www.xilinx.com/support/documentation/boards_and_kits/zcu216/ug1437-clk104.pdf>`_

The following picture shows the details of the CLK104 module. The bottom SMA is the 122.88MHz reference clock output to be connected to the DTRX2 input reference clock port. And the other SMA connector above, labelled "INPUT_REF_CLK" is a provision for an external 10MHz master reference clock signal (used for synchronization with test equipments for instance).  
When an external 10MHz is not provided, the CLK104 module needs to be configured to use the internal 10MHz TCXO, as decribed in the steps below.

.. figure:: images_system_setup/CLK104.png
    :align: center

    Xilinx CLK104 System Clock Module

#. Go to the RFSoC Explorer Main tab
#. Select **CLK104 Configuration > 122.88MHz REFCLKOUT_10MHz TCXO REF**

.. image:: images_system_setup/clk104_config.jpg
    :scale: 75%

.. note:: The **122.88MHz REFCLKOUT_10MHz TCXO REF** configuration uses the CLK104 on-board 10MHz TCXO reference for the LMK04828B. If you wish to synchronize the setup up to a test instrument 10MHz clock, use the **122.88MHz REFCLKOUT_10MHz EXT REF** configuration (typically recommended for demodulation and for EVM measurements). 

Power Up DTRX2
---------------
#. Connect your test equipment to the DTRX2 RF and TX ports
#. Terminate unused channels with a 2.92mm 50 ohms termination
#. Apply 12V DC power to the DTRX2 card, using the DC barrel jack-to-banana plugs cable provided.

Both D4 and D6 "Power Good" red LEDs should be lit. The idle current drawn from the 12V supply should be about 45mA.

Click NEXT to setup the DTRX2 transmit chains.