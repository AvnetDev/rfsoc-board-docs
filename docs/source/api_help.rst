Application Programming Interface (API)
=======================================
RFSoC Explorer® is a MATLAB toolbox that enables control of AMD Zynq™ UltraScale+™ RFSoC evaluation boards using MATLAB and Simulink. The toolbox includes a graphical interface and an intuitive API for programmatic control of all RF-ADC and RF-DAC parameters, signal generation and acquisition. System designers and test engineers who want to experiment with OTA signals can use RFSoC Explorer to control supported RF front-end cards.

To get started, view the help page in MATLAB:

::

  >> help RFSoC_Explorer

For a full listing of API functions and their usage, use the API itself:

::

  >> RFSoC_Explorer('help')

Use the API to narrow your search:

::

   >> RFSoC_Explorer('help', 'ADC')
   API_functions related to 'ADC':

   [error_flag, data, msg] = RFSoC_Explorer('ADC_tile_enable', <tile>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_tile_disable', <tile>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_tile_open', <tile>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_calibration_status', <tile>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_program', <tile>, <calibrate>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_memory_type' <tile>, <memtype>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_sample_rate', <tile>, <sample_rate_MHz>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_channel_enable', <tile>, <chan>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_channel_disable', <tile>, <chan>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_read', <tile>, <chan>, <nSamples>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_setDSA', <tile>, <chan>, <dB-attenuation>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_decimation', <tile>, <chan>, <rate_change>)
   [error_flag, data, msg] = RFSoC_Explorer('ADC_mixer', <tile>, <chan>, <params>)

Get help on a specific API:

::

    >> RFSoC_Explorer('help', 'ADC_calibration')

       [error_flag, data, msg] = RFSoC_Explorer('ADC_calibration_status', <tile>)

      Return RF-ADC calibration status.

      <data> is logical true when calibration is required;  otherwise false.

      Related API_function **ADC_program**


     Support & Documentation



Main API help
-------------

::

    RFSoC_Explorer  Application programmer interface (API) created by 
    Tria Technologies (an Avnet Company) to connect AMD Zynq™ UltraScale+™
    RFSoC gigasample data converters to MATLAB® and Simulink®.
   
    [ERROR_FLAG, DATA, MSG] = RFSoC_Explorer(API_FUNCTION, VARARGIN)
    executes the command string defined by API_FUNCTION and returns
    boolean ERROR_FLAG, any DATA values, and error/warning MSG. Use
    varargin to provide relevant additional paramters.
 
    For help with syntax and varargin:
 
        RFSoC_Explorer('help', API_FUNCTION);  % Syntax help for specific API
        RFSoC_Explorer('help', <string>);      % APIs related to search string
        RFSoC_Explorer('help','DTRX2');        % APIs for Otava mmWave RF addon card 
        RFSoC_Explorer('help','FJK_PAAM');     % APIs for Fujikura mmWave PAAM
 
    Support & Documentation
 
    API_FUNCTION strings for RFSoC:
  
    -- Global --
        'help'                  % Also try ('help', <string>)
        'startup'               % Use alone or with board_id
        'shutdown'              % Close GUI and release the application
        'status'                % Report app status, TCP connection, boardID
        'ipconfig'              % Board IP address
        'Memory_type'           % RFSoC Gen1/ZCU111 memory type is global
        'Program_CLK104_LMK'    % Program CLK104 module LMK PLL (ZCU208 only)
        'DTRX2'                 % RFSoC Gen3/ZCU208 with Otava DTRX2 mmW card
        'FJK_PAAM'              % RFSoC Gen3/ZCU208 with Fujikura mmW PAAM
 
    -- RF-ADC --
        'ADC_tile_enable'       % RFSoC Explorer parameter != RFDC IP setting
        'ADC_tile_disable'      % RFSoC Explorer parameter != RFDC IP setting
        'ADC_tile_open'         % Opens tile tab in the GUI
        'ADC_channel_enable'    % Performs tile enable if required
        'ADC_channel_disable'   % Resets channel parameters
        'ADC_memory_type'       % RFSoC Gen3/ZCU208 memory type is per tile
        'ADC_setDSA'            % Digital Step Attenuator (Gen3)
        'ADC_sample_rate'       % Tile internal PLL in MHz
        'ADC_decimation'        % Available integer factors depend on RFSoC Gen
        'ADC_mixer'             % Requires struct of mixer parameters
        'ADC_calibration_status'% Calibration of interleaved ADC required?
        'ADC_program'           % Program target board with user settings
        'ADC_read'              % Transfer samples from ADC buffer to PC
 
    -- RF-DAC --
        'DAC_tile_enable'       % RFSoC Explorer parameter != RFDC IP setting
        'DAC_tile_disable'      % RFSoC Explorer parameter != RFDC IP setting
        'DAC_tile_open'         % Opens tile tab in the GUI
        'DAC_channel_enable'    % Performs tile enable if required
        'DAC_channel_disable'   % Resets channel parameters
        'DAC_memory_type'       % RFSoC Gen3/ZCU208 memory type is per tile
        'DAC_setVOP'            % Variable Output Power (Gen3)
        'DAC_sample_rate'       % Tile internal PLL in MHz
        'DAC_interpolation'     % Available integer factors depend on RFSoC Gen
        'DAC_mixer'             % Requires struct of mixer parameters
        'DAC_DUC_mode'          % Image Rejection Modes (RFSoC Gen3)
        'DAC_VOP'               % Variable Output Power (RFSoC Gen3)
        'DAC_signal_source'     % Setup DAC signal type and parameter structure
        'DAC_program'           % Program target board with user settings
        'DAC_write'             % Transfer waveform from PC to DAC buffer for replay
        'DAC_signal_level'      % dBFS only
 
    Examples:
    
    Start the application using board select menu:
        RFSoC_Explorer();
 
    Start the application for ZCU208 standalone:
        RFSoC_Explorer('startup', 3);
 
        Valid boardID:
            1 - ZCU111
            2 - ZCU111 + Qorvo 2 Channel RF Front-end 1.8 GHz Card
            3 - ZCU208
            4 - ZCU208 + Otava DTRX2 mmWave RF Front-end
            5 - ZCU208 + Otava DTRX2 mmWave RF Front-end + Rohde & Schwarz Instrument Remote Control
            6 - RESERVED
            7 - ZCU208 + Fujikura mmWave PAAM
            8 - RESERVED
            9 - ZCU208 + Fujikura mmWave Type C PAAM Eval Board with MicroZed
  
    Enable DAC tile 3 chan 0:
        [error_flag, data, msg] = RFSoC_Explorer('DAC_channel_enable', 3, 0);
 
    Set ADC tile 0 sample rate to 4915.2 MHz :
        [error_flag, data, msg] = RFSoC_Explorer('ADC_sample_rate', 0, 4915.2);
 
    Program ADC tile 0 and read 8192 samples :
        RFSoC_Explorer('ADC_program', 0);
        RFSoC_Explorer('ADC_read', 0, 8192);
  
    Program DAC tile 1 chan 2 mixer:
        % Create structure with mixer parameters
        params.Freq        = +4700;      % MHz
        params.PhaseOffset = 0;          % Degrees
        params.MixerMode   = 'IQ->Real'; % 'Real->Real'|'IQ->Real'
        params.MixerType   = 'Fine';     % 'Fine'|'Coarse'
  
        % Set mixer parameters and program DAC tile 1
        RFSoC_Explorer('DAC_mixer', 1, 2, params);
        RFSoC_Explorer('DAC_program', 1);
  
    More API examples are located in the /test folder.
 
    `Support & Documentation <https://www.mathworks.com/matlabcentral/fileexchange/73665-avnet-rfsoc-explorer>`_


Otava DTRX2 mmWave API Help
-----------------------------------------

::

    RFSoC_Explorer   API to Otava DTRx2 mmWave Daughtercard for ZCU208
    
    Usage:
    
    RFSoC_Explorer('DTRX2',  <'dtrx2_cmd'>) sends the command defined by 'dtrx2_cmd' to DTRx mmWave Daughtercard for ZCU208
        ex. RFSoC_Explorer('DTRX2','TX_power_up')
    
        Available dtrx2_cmd API strings :
    
            TX_power_up             % TX power up: DSA is enabled; TX channels remain disabled until call to TX_Ch1_IfAmp/2_Enable
            TX_power_down
            TX_VCO_OutA_Enable      % turn on TX VCO A
            TX_VCO_OutA_Disable     % turn off TX VCO A
            TX_VCO_OutB_Enable      % turn on TX VCO B
            TX_VCO_OutB_Disable     % turn off TX VCO B
            TX_IF_AMP_Ch1_Enable    % turn on TX Channel 1
            TX_IF_AMP_Ch1_Disable   % turn off TX Channel 1
            TX_IF_AMP_Ch2_Enable    % turn on TX Channel 2
            TX_IF_AMP_Ch2_Disable   % turn off TX Channel 2
            TX_Update_GC_Button     % Update Gain Control (DSA) in TX chain; programmatic equivalent of user pressing GUI 'Update TX Gain Control' Button
            TX_Update_PLL_Button    % Update PLL in TX chain; programmatic equivalent of user pressing GUI 'Update PLL' Button
    
            RX_power_up             % RX power up: RF/IF DSAs are enabled; RX channels remain disabled until calls to RX_Ch1_RfAmp/2_Enable & RX_Ch1_IfAmp/2_Enable
            RX_power_down
            RX_VCO_OutA_Enable      % turn on RX VCO A
            RX_VCO_OutA_Disable     % turn off RX VCO A
            RX_VCO_OutB_Enable      % turn on RX VCO B
            RX_VCO_OutB_Disable     % turn off RX VCO B
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
            RX_Update_PLL_Button    % Update PLL in RX chain; programmatic equivalent of user pressing GUI 'Update PLL' Button
    
    RFSoC_Explorer('DTRX2', <'dtrx2_cmd'>, <parameter>)
        ex. RFSoC_Explorer('DTRX2', 'TX_RF_DSA_Attenuation', 10)  => set TX RF DSA Attenuation = 10 dB
    
        Available dtrx2_cmd strings with parameter :
    
            TX_VCO_Pwr_OutA, parameter = TX VCO A power code (0 ... 50) incl. (Note: by default VCO power is dependant on PLL frequency, but it can be forced / over-ridden by this property)
            TX_VCO_Pwr_OutB, parameter = TX VCO B power code (0 ... 50) incl.  "      "  ... 
            TX_RF_DSA_Attenuation, parameter = TX RF DSA Attenuation (dB), range 0 ... 15.5 dB of positive attenuation (- gain) in 1/2 dB step
            TX_mmWave_Fc, parameter = TX output mmWave center frequency (GHz)
            TX_IF_signal_BW, parameter = TX signal bandwidth (MHz)
            TX_IF_center_frequency, parameter = TX intermediate frequency (MHz)
    
            RX_VCO_Pwr_OutA, parameter = RX VCO A power code (0 ... 50) incl. (Note: by default VCO power is dependant on PLL frequency, but it can be over-ridden by this property)
            RX_VCO_Pwr_OutB, parameter = RX VCO B power code (0 ... 50) incl.  "      "  ... 
            RX_mmWave_Fc, parameter = RX input mmWave center frequency (GHz)
            RX_IF_signal_BW, parameter = RX signal bandwidth (MHz)
            RX_IF_center_frequency, parameter = RX intermediate frequency (MHz)
            RX_RF_DSA_Ch1_Attenuation, parameter = RX RF DSA Channel 1 Attenuation (dB), range 0 ... 14 dB of positive attenuation (- gain) in 2 dB step
            RX_IF_DSA_Ch1_Attenuation, parameter = RX I/F DSA Channel 1 Attenuation (dB), range 0 ... 32 dB of positive attenuation (- gain) in 1/2 dB step
            RX_RF_DSA_Ch2_Attenuation, parameter = RX RF DSA Channel 2 Attenuation (dB)
            RX_IF_DSA_Ch2_Attenuation, parameter = RX I/F DSA Channel 2 Attenuation (dB)

        `Support & Documentation <https://www.mathworks.com/matlabcentral/fileexchange/73665-avnet-rfsoc-explorer>`_

Fujikura 28GHz Phased Array Antenna Moduel (PAAM) API help
-----------------------------------------

::

    RFSoC_Explorer  API to Renesas 8V97003 RF synth and FJK PAAM module for ZCU208
    
    RFSoC_Explorer('FJK_PAAM', <'fjk_cmd'>) sends the command defined by 'fjk_cmd' to either PLL or PAAM
        ex. RFSoC_Explorer('FJK_PAAM', 'PLL_initialize') => initialize PLL
        ex. RFSoC_Explorer('FJK_PAAM', 'PAAM_send') => send current beam configuration to PAAM 
        ex. RFSoC_Explorer('FJK_PAAM', 'PAAM_set_TX_H_on') => set transmit horizontal polarization on
    
        Available fjk_cmd API strings :
            PLL_initialize
            PLL_update
    
            PAAM_initialize
            PAAM_initialized_successfully
            PAAM_reset
            PAAM_close
            PAAM_send
            PAAM_user_params_ingested
            PAAM_user_bias_ingested
            PAAM_set_TX_V_on
            PAAM_set_TX_V_off
            PAAM_set_TX_H_on
            PAAM_set_TX_H_off
            PAAM_set_RX_V_on
            PAAM_set_RX_V_off
            PAAM_set_RX_H_on
            PAAM_set_RX_H_off
            PAAM_write_user_bias
            PAAM_write_user_params
            PAAM_read_EEPROM
            PAAM_read_ADC_0 = Read from ADC IC U27 and store in return var "data"
            PAAM_read_ADC_1 = Read from ADC IC U29 and store in return var "data"
            PAAM_read_ADC_2 = Read from ADC IC U28 and store in return var "data"
            PAAM_read_ADC_3 = Read from ADC IC U30 and store in return var "data"
            PAAM_read_all_ADCs = Read from all ADCs and store as a 4x8 table in var "data"
    
    RFSoC_Explorer('FJK_PAAM', <'fjk_cmd'>, <param>)
        ex. RFSoC_Explorer('FJK_PAAM', 'PLL_input_doubler', 2)  => set PLL Doubler value = 2
        ex. RFSoC_Explorer('FJK_PAAM', 'PAAM_ingest_user_params', <user_params>') => ingest user params for PAAM operations where <user_params> is the file path to the user parameters JSON (ie, './Fujikura/ibm_fjkr_taskb/json/paam_taskb_params.json')
        ex. RFSoC_Explorer('FJK_PAAM', 'PAAM_edit_user_param',  {'beam_table.BeamSettings.gain_beam_index_sel', 3})
        ex. RFSoC_Explorer('FJK_PAAM', 'PAAM_edit_user_param',  {'beam_table.BeamSettings.beam_table_config.theta.angles', [-60,0,60,120]})
        ex. RFSoC_Explorer('FJK_PAAM', 'PAAM_set_attenuator_RX_IF_H', 27)
    
        Available fjk_cmd strings with param :
            PLL_input_frequency_MHz, param = Set PLL input frequency (default is 122.88MHz)
            PLL_input_doubler, param = Set PLL input double value. Range of accepted values is: [1, 2]
            PLL_input_divider, param = Set PLL input divider value. Range of accepted values is: [1, 2]
            
            PLL_VCO_RF_frequency_GHz, param = Set RF frequency for PLL VCO
            PLL_VCO_IF_frequency_GHz, param = Set IF frequency for PLL VCO
    
            PLL_PMOS_current, param = Set PMOS current for PLL charge pump control in mA
            PLL_NMOS_current, param = set NMOS current for PLL charge pump control in mA
            PLL_bleeder_current, param = Set bleeder current for PLL charge pump control in uA
    
            PLL_RF_power, param = Set channel A power for PLL in dBm
            PLL_attenuation, param = Set PLL attenuation in dB
    
            PAAM_ingest_user_bias, param = Ingest user bias settings from json file specified by param
            PAAM_edit_user_bias, {parameter1, parameter2} = Edit user bias setting specified by parameter1, formatted 'fieldname1.fieldname2.fieldname3'. Set to value of parameter2.
    
            PAAM_ingest_user_params, param = Ingest user parameters from json file specified by param
            PAAM_edit_user_param, {parameter1, parameter2} = Edit user param specified by parameter1, formatted 'fieldname1.fieldname2.fieldname3'. Set to value of parameter2.
                    To set an array of values, you can pass an array into parameter2 in the format [val1, val2, val3, etc]
            PAAM_edit_user_param_IP, param = Set IP for BT and OCC modes of ingested user params JSON
            PAAM_set_mode, param = Set PAAM mode to 'OCC' or 'BeamTable.' This should be set to the desired mode before calling PAAM_initialize.
            PAAM_set_beamformer, param, field, value = Set the value of 'field' of the beamformer specified by 'param' to the value in 'value'
                ex: RFSoC_Explorer('FJK_PAAM', 'PAAM_set_beamformer', 'RX_V', 'field', 'VGA_gain', 'value', 10)
            PAAM_set_attenuator_PLL, param, FjkController = Set PLL IF attenuator to the value given by param. Range is: [0, 31.75] dB
    
            PAAM_set_attenuator_TX_IF_V, param, FjkController = Set TX IF V attenuator to the value given by param. Range is: [0, 31.75] dB
            PAAM_set_TX_V_on = Sets TX IF V dir to 'tx'
            PAAM_set_TX_V_off = Sets TX IF H dir to 'pwrdn'
            PAAM_set_TX_V_fe_num, param = Set the active fe number for TX IF V 
            PAAM_set_TX_V_azimuth, param = Set the desired angle for the TX IF V Azimuth (phi). Range is: [-60, 60] degrees
            PAAM_set_TX_V_elevation, param = Set the desired angle for the TX IF V Elevation (theta). Range is: [-60, 60] degrees
            PAAM_set_TX_V_beam_index, param = Set the desired beam index for TX IF V in BeamTable mode. Range is [0, 255]
    
            PAAM_set_attenuator_TX_IF_H, param, FjkController = Set TX IF H attenuator to the value given by param. Range is: [0, 31.75] dB
            PAAM_set_TX_H_on = Sets TX IF H dir to 'tx'
            PAAM_set_TX_H_off = Sets TX IF H dir to 'pwrdn'
            PAAM_set_TX_H_fe_num, param = Set the active fe number for TX IF H 
            PAAM_set_TX_H_azimuth, param = Set the desired angle for the TX IF H Azimuth (phi). Range is: [-60, 60] degrees
            PAAM_set_TX_H_elevation, param = Set the desired angle for the TX IF H Elevation (theta). Range is: [-60, 60] degrees
            PAAM_set_TX_H_beam_index, param = Set the desired beam index for TX IF H in BeamTable mode. Range is [0, 255]
    
            PAAM_set_attenuator_RX_IF_V, param, FjkController = Set RX IF V attenuator to the value given by param. Range is: [0, 31.75] dB
            PAAM_set_RX_V_on = Sets RX IF V dir to 'tx'
            PAAM_set_RX_V_off = Sets RX IF V dir to 'pwrdn'
            PAAM_set_RX_V_fe_num, param = Set the active fe number for RX IF V 
            PAAM_set_RX_V_azimuth, param = Set the desired angle for the RX IF V Azimuth (phi). Range is: [-60, 60] degrees
            PAAM_set_RX_V_elevation, param = Set the desired angle for the RX IF V Elevation (theta). Range is: [-60, 60] degrees
            PAAM_set_RX_V_beam_index, param = Set the desired beam index for RX IF V in BeamTable mode. Range is [0, 255]
    
            PAAM_set_attenuator_RX_IF_H, param, FjkController = Set RX IF H attenuator to the value given by param. Range is: [0, 31.75] dB
            PAAM_set_RX_H_on = Sets RX IF H dir to 'tx'
            PAAM_set_RX_H_off = Sets RX IF H dir to 'pwrdn'
            PAAM_set_RX_H_fe_num, param = Set the active fe number for RX IF H 
            PAAM_set_RX_H_azimuth, param = Set the desired angle for the RX IF H Azimuth (phi). Range is: [-60, 60] degrees
            PAAM_set_RX_H_elevation, param = Set the desired angle for the RX IF H Elevation (theta). Range is: [-60, 60] degrees
            PAAM_set_RX_H_beam_index, param = Set the desired beam index for RX IF H in BeamTable mode. Range is [0, 255]
    
            PAAM_set_DAC, param = Send the value given by param to the DAC in hexadecimal format
            PAAM_set_ADC_clock_source = Set the clock source to 0 for external (default) and 1 for internal
    
            PAAM_set_ps_slope_BT, param = Set BeamTable ps_slope in ingested user parameters JSON.
                                Editing this value will require re-initialization to update the ps_slope of the PAAM in OCC mode.
            PAAM_set_ps_slope_OCC, param = Set OCC ps_slope in ingested user parameters JSON
                                Editing this value will require re-initialization to update the ps_slope of the PAAM in BeamTable mode.
            PAAM_set_taper_mode, param = Set taper mode for OCC and BT to: {'default', 'taylor', 'uniform'}
                                Editing this value will require re-initialization to update the tapering mode of the PAAM.
            PAAM_set_freq_ghz, param = Set PAAM frequency in GHz. Will update user parameters JSON and GUI
                                Editing this value will require re-initialization to update the frequency on the PAAM.
    
            PAAM_read_EEPROM, param = Read from EEPROM the fieldname given by param
    
    Related search results:

    FJK_PAAM

    For detailed help on an API_function:

    RFSoC_Explorer('help', <API_function>)

`Support & Documentation <https://www.mathworks.com/matlabcentral/fileexchange/73665-avnet-rfsoc-explorer>`_

