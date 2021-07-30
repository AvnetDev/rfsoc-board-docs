Application Programming Interface (API)
=======================================
Avnet RFSoC Explorer 2.0 introduces an API for programmatic control of all RF-ADC and RF-DAC parameters, signal generation, acquisition and Otava DTRX2 mmwave functions.

To get started, use the MATLAB R2021a built in help:

::

  >> help Avnet_RFSoC_Explorer

For a full listing of API functions and their usage, use the API itself:

::

  >> Avnet_RFSoC_Explorer('help')

Use the API to search help:

::

  >> Avnet_RFSoC_Explorer('help', 'ADC')

  [status, data] = Avnet_RFSoC_Explorer('ADC_tile_enable', <tile>)
  [status, data] = Avnet_RFSoC_Explorer('ADC_tile_disable', <tile>)
  [status, data] = Avnet_RFSoC_Explorer('ADC_tile_open', <tile>)
  [status, data] = Avnet_RFSoC_Explorer('ADC_channel_enable', <tile>, <chan>)
  [status, data] = Avnet_RFSoC_Explorer('ADC_channel_disable', <tile>, <chan>)
  [status, data] = Avnet_RFSoC_Explorer('ADC_memory_type' <tile>, <memtype>)
  [status, data] = Avnet_RFSoC_Explorer('ADC_sample_rate' <tile>, <sample_rate_MHz>)
  [status, data] = Avnet_RFSoC_Explorer('ADC_decimation' <tile>, <chan>, <rate_change>)
  [status, data] = Avnet_RFSoC_Explorer('ADC_mixer', <tile>, <chan>, <mixer_struct>)
  [status, data] = Avnet_RFSoC_Explorer('ADC_calibration_status', <tile>)
  [status, data] = Avnet_RFSoC_Explorer('ADC_program', <tile>, <calibrate>)
      Set optional input arg <calibrate> to logical true to force calibration.
      Return arg status.ADCcalibrationModeChange is logical [true|false]

  [status, data] = Avnet_RFSoC_Explorer('ADC_read' <tile>, <chan>, <nSamples>)

Main API help
-------------
::

  Avnet_RFSoC_Explorer application programmer interface (API)
   [status, data] = Avnet_RFSoC_Explorer(API_function, varargin) executes the
     command string defined by 'API_function' and returns pass/fail 'status'
     and any relevant 'data'. Use varargin to provide relevant paramters.

     For a full listing of API_function and usage :

         Avnet_RFSoC_Explorer('help')

     Available API_function strings :
  
     -- Global --
         'help'
         'startup'
         'shutdown'
         'ipconfig'
         'Memory_type'           % RFSoC Gen-2/ZCU111 memory type is global
         'DTRX2'                 % RFSoC Gen-3/ZCU208 with Otava DTRX2 mmW

     -- RF-ADC --
         'ADC_tile_enable'
         'ADC_tile_disable'
         'ADC_tile_open'         % Opens tile tab in the GUI
         'ADC_channel_enable'    % Performs tile enable if required
         'ADC_channel_disable'   % Resets channel parameters
         'ADC_memory_type'       % RFSoC Gen-2/ZCU111 only
         'ADC_sample_rate'       % Tile internal PLL in MHz
         'ADC_decimation'
         'ADC_mixer'
         'ADC_calibration_status'
         'ADC_program'           % Program target board with user settings
         'ADC_read'              % Transfer samples from ADC buffer to PC

     -- RF-DAC --
         'DAC_tile_enable'
         'DAC_tile_disable'
         'DAC_tile_open'         % Opens tile tab in the GUI
         'DAC_channel_enable'    % Performs tile enable if required
         'DAC_channel_disable'
         'DAC_memory_type'       % RFSoC Gen-3/ZCU208 only
         'DAC_sample_rate'
         'DAC_interpolation'
         'DAC_mixer'
         'DAC_DUC_mode'          % RFSoC Gen-3/ZCU208 only
         'DAC_signal_source'     % Setup DAC signal type and parameter structure
         'DAC_program'           % Program target board with user settings
         'DAC_write'             % Transfer samples from PC to DAC buffer for replay

     Examples
     To enable DAC tile 3 chan 0 :
         [status, data] = Avnet_RFSoC_Explorer('DAC_channel_enable', 3, 0);

     To set ADC tile 0 sample rate to 4915.2 MHz :
         [status, data] = Avnet_RFSoC_Explorer('ADC_sample_rate', 0, 4915.2);

     To program ADC tile 0 and read 8192 samples :
         [status, data] = Avnet_RFSoC_Explorer('ADC_program', 0);
         [status, data] = Avnet_RFSoC_Explorer('ADC_read', 0, 8192);

     To program DAC tile 1 chan 2 mixer :
         % Create structure with mixer parameters
         mixerDAC.Freq        = +4700;      % MHz
         mixerDAC.PhaseOffset = 0;          % Degrees
         mixerDAC.MixerMode   = 'IQ->Real'; % 'Real->Real'|'IQ->Real'
         mixerDAC.MixerType   = 'Fine';     % 'Fine'|'Coarse'
         % Set mixer parameters and program the board
         [status, data] = Avnet_RFSoC_Explorer('DAC_mixer', 1, 2, mixerDAC);
         [status, data] = Avnet_RFSoC_Explorer('DAC_program', 1);

     To get get help :
         help Avnet_RFSoC_Explorer;    % List full API help
         Avnet_RFSoC_Explorer('help'); % List full API help
         Avnet_RFSoC_Explorer('help', 'ADC_read');  % Usage for specific function
         Avnet_RFSoC_Explorer('help', 'ADC');       % Usage for all ADC functions

     More extensive examples are located in the /scripts folder. 


Otava DTRX2 mmWave API Help (ZCU208 only)
-----------------------------------------
::

   Avnet_RFSoC_Explorer API to Otava DTRx2 mmWave Daughtercard for ZCU208

   Usage :
   Avnet_RFSoC_Explorer('DTRX2',  <dtrx2_cmd>) sends the command defined by 'dtrx2_cmd' to DTRx mmWave Daughtercard for ZCU208
      ex. Avnet_RFSoC_Explorer('DTRX2','TX_power_up')

   Available dtrx2_cmd API strings :

           TX_power_up             % TX power up: DSA is enabled; TX channels remain disabled until call to TX_Ch1_IfAmp/2_Enable
           TX_power_down           % TX power down
           TX_VCO_OutA_Enable      % turn on TX VCO A
           TX_VCO_OutB_Enable      % turn on TX VCO B
           TX_IF_AMP_Ch1_Enable    % turn on TX Channel 1
           TX_IF_AMP_Ch1_Disable   % turn off TX Channel 1
           TX_IF_AMP_Ch2_Enable    % turn on TX Channel 2
           TX_IF_AMP_Ch2_Disable   % turn off TX Channel 2
           TX_Update_GC_Button     % Update Gain Control (DSA) in TX chain; programmatic equivalent of user pressing GUI 'Update TX Gain Control' Button

           RX_power_up             % RX power up: RF/IF DSAs are enabled; RX channels remain disabled until calls to RX_Ch1_RfAmp/2_Enable & RX_Ch1_IfAmp/2_Enable
           RX_power_down
           RX_Ch1_RfAmp_Enable     % turn on RX Channel 1 RF LNA
           RX_Ch1_IfAmp_Enable     % turn on RX Channel 1 IF LNA  -> Both LNA switches On -> will turn on RX Channel 1
           RX_Ch1_RfAmp_Disable    % turn off RX Channel 1 RF LNA
           RX_Ch1_IfAmp_Disable    % turn off RX Channel 1 IF LNA -> When both switches Off -> disable RX channel 1, leaving DSAs at current attenutation settings
           RX_Ch2_RfAmp_Enable
           RX_Ch2_IfAmp_Enable
           RX_Ch2_RfAmp_Disable
           RX_Ch2_IfAmp_Disable
           RX_Update_GC_ch1_Button % Update Gain Control (DSA) in RX chain; programmatic equivalent of user pressing GUI 'Update RX Gain Control' Button
           RX_Update_GC_ch2_Button

   Avnet_RFSoC_Explorer('DTRX2', <dtrx2_cmd>, <parameter>)
      ex. Avnet_RFSoC_Explorer('DTRX2', 'TX_RF_DSA_Attenuation', 10)  => set TX RF DSA Attenuation = 10 dB

   Available dtrx2_cmd strings with parameter :
   
           TX_VCO_Pwr_OutA, parameter = TX VCO A power code (0 ... 50) incl. (Note: by default VCO power is dependant on PLL frequency, but it can be forced / over-ridden by this property)
           TX_VCO_Pwr_OutB, parameter = TX VCO B power code (0 ... 50) incl.  "      "  ... 
           TX_RF_DSA_Attenuation, parameter = TX RF DSA Attenuation (dB), range 0 ... 15.5 dB of positive attenuation (- gain) in 1/2 dB step
           TX_mmWave_Fc, parameter = TX output mmWave center frequency (GHz)
           TX_IF_signal_BW, parameter = TX signal bandwidth (MHz)

           RX_VCO_Pwr_OutA, parameter = RX VCO A power code (0 ... 50) incl. (Note: by default VCO power is dependant on PLL frequency, but it can be over-ridden by this property)
           RX_VCO_Pwr_OutB, parameter = RX VCO B power code (0 ... 50) incl.  "      "  ... 
           RX_mmWave_Fc, parameter = RX input mmWave center frequency (GHz)
           RX_IF_signal_BW, parameter = RX signal bandwidth (MHz)
           RX_RF_DSA_Ch1_Attenuation, parameter = RX RF DSA Channel 1 Attenuation (dB), range 0 ... 14 dB of positive attenuation (- gain) in 2 dB step
           RX_IF_DSA_Ch1_Attenuation, parameter = RX I/F DSA Channel 1 Attenuation (dB), range 0 ... 32 dB of positive attenuation (- gain) in 1/2 dB step
           RX_RF_DSA_Ch2_Attenuation, parameter = RX RF DSA Channel 2 Attenuation (dB)
           RX_IF_DSA_Ch2_Attenuation, parameter = RX I/F DSA Channel 2 Attenuation (dB)

