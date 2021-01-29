Transmitter Configuration and operation
---------------------------------------
In this procedure, we will run the transmitters to the default mmW output frequency of 25GHz. 
Set the spectrum analyzer center frequency to 25GHz then, to observe the signal transmitted after power up.
From the RFSOC Explorer application, go to the “Otava DTRX” tab and hit the **“TX Power up”** button. This powers-up both TX channels and performs a default configuration of the 2 RF transmit channels.

**Insert picture of the RFSOC Explorer DTRX2 page**

The average current drawn on the 12V supply should then be about 760mA. 

By defaults, both TX channels should be ON, and in the following state:
-	The default RF frequency is 25GHz and the TX PLL is programmed to an LO at 14.6GHz, for a default IF frequency of 4.2GHz.
-	The TX PLL visual lock indicator D2 should be lit (green LED)
-	Both TX channel 1 and channel 2 are enabled and powered
-	Both Ch1 and Ch2 RF attenuators are set to max attenuation at -15.5dB

ZCU208 RFSOC DAC configuration and signal generation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

