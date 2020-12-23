Introduction
-------------
This document will show you how to get started with the Avnet Wideband mmWave Radio Dev Kit for RFSoC Gen-3. Follow the step-by-step instructions to configure the kit, setup your computer, and use Avnet RFSoC Explorer® in MATLAB to generate and acquire signals through the Otava mmWave Dual Trancseiver RF Card.

.. image:: images_system_setup/zcu208_dtrx2_kit.png

Kit Overview
------------
The Avnet Wideband mmWave Radio Development Kit for RFSoC Gen-3 is ideal for prototyping RF applications in mmW bands including 5G NR FR2, wireless backhaul, as well as K/Ka band radar and SATCOM. This platform combines the Otava DTRX2 Dual Transceiver mmWave Radio Card — jointly developed by Otava and Avnet — with the Xilinx Zynq ® UltraScale+ ™ RFSoC ZCU208 Evaluation Kit.

.. warning:: This kit can radiate radio frequency energy and has not been tested for CE, FCC, or IC compliance. The intended use is for demonstration, engineering development, or evaluation purposes. See :ref:`compliance`

Install RFSoC Explorer
----------------------
Avnet RFSoC Explorer provides native connection to MATLAB ® and Simulink ®, featuring graphical control of the platform and intuitive APIs for programmatic access.

.. image:: images_system_setup/rfsocX-concept.jpg

You will need a computer running Windows 10 OS and the following MathWorks software. 

`Get a Free MATLAB Trial Package for RFSoC <https://www.mathworks.com/rfsoc>`_

   * MATLAB R2020b or later 
   * DSP System Toolbox
   * Fixed-Point Designer
   * Communications Toolbox
   * Communications Toolbox Support Package for Xilinx Zynq-Based Radio
   * Signal Processing Toolbox
   * LTE Toolbox (optional)
   * 5G Toolbox (optional)


RFSoC Explorer installs easily in the MATLAB APPS tab without modifying your registry or other applications.

1)	From **MATLAB > Add-Ons**, search for **Avnet RFSoC Explorer** and click install
2)	From **MATLAB > Add-Ons**, search for **Communications Toolbox Support Package for Xilinx Zynq-Based Radio** and click install
3) If prompted, click **Setup Later**

.. image:: images_system_setup/mw-addon.png

Hardware Setup
----------------
The Xilinx ZCU208 Evaluation Kit has many jumpers and switches that are shipped with default states, which do not need to change for this tutorial. In the following steps we describe the minimal configuration. For a comprehensive setup guide, refer to the online `Xilinx ZCU208 Quick Start Wiki <https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/569017820/RF+DC+Evaluation+Tool+for+ZCU208+board+-+Quick+Start>`_

.. image:: images_system_setup/hw-setup.jpg

#. Connect the Otava DTRX2 mmWave Card, the ZCU208, and cables as shown in the picture

#. Plug Ethernet and USB cables into your host PC

#. Set the ZCU208 DIP switches (SW6) as shown in the figure below, which allows the ZCU208 board to boot from the SD card

.. image:: images_system_setup/zcu208-dip-sw.png


SD Card
-------
#. Remove the SD card from the ZCU208, insert into your PC, and format as FAT using a tool like `SD Memory Card Formatter <https://www.sdcard.org/downloads/formatter_4/>`_

#. Download the file **avnet_rfsocX_zcu111_boot_v1_0.zip** This archive contains the software for the ZCU111 evaluation board. Unzip the archive to a convenient location on your hard disk, then copy the files to the root level of the SD card. 

#. Safely eject the SD card from the PC and replace into ZCU208.


Boot ZCU208
------------
#. Turn the ZCU208 power switch ON (near the 12V connector) 

#. The application auto-start function creates an IP connection for the board at address **169.254.10.2**. 

#. Set a static IP for your host PC's Local Ethernet adapter.  Make sure your PC and the board are on the same subnet and gateway. See example below.

.. image:: images_system_setup/network-cfg.png
.. image:: images_system_setup/laptop-ip.jpg


.. note:: The auto-start IP address can be changed in the autostart.sh file on your SD card. 



.. _compliance:

Regulatory Compliance Information
-----------------------------------
This kit can radiate radio frequency energy and has not been tested for CE, FCC, or IC compliance. The intended use is for demonstration, engineering development, or evaluation purposes.

FCC WARNING
^^^^^^^^^^^
This kit is designed to allow:
 
(1) Product developers to evaluate electronic components, circuitry, or software associated with the kit to determine whether to incorporate such items in a finished product and
 
(2) Software developers to write software applications for use with the end product. 

This kit is not a finished product and when assembled may not be resold or otherwise marketed unless all required FCC equipment authorizations are first obtained. Operation is subject to the condition that this product not cause harmful interference to licensed radio stations and that this product accept harmful interference. Use of the kit should be limited to a development lab environment only.

CE WARNING
^^^^^^^^^^
This evaluation kit is for use by professionals for their research and development purposes. The kit may not be put into service for use on a regular basis, or integrated into an end product (Annex I.4 of the RED). This kit is does not bare the CE mark of certification. As such, this kit may be operated only within the requirements of RED section 1.6.2.5, Custom-built evaluation kits.




