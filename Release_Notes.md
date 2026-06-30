

# Release Notes for

# <mark> STM32CubeWL3 wM-Bus Middleware </mark>

Copyright &copy; 2024-2025 STMicroelectronics\

[![ST logo](../../../_htmresc/st_logo_2020.png)](https://www.st.com)

# Purpose

This Middleware provides the wM-Bus Middleware for the STM32WL3x products, according to EN 13757-4:2011.

This covers:

- STM32WL3x devices  

This driver is composed of 2 directories both with 2 subdirectories:

- DataLink
  - Inc
  - Src
- Phy
  - Inc
  - Src


# Update History

<label for="collapse-section4" checked aria-hidden="true">__V1.1.0 / 16-December-2025__</label>
<div>

## Main Changes
###  Improve handling of the RX_OK interrupt introducing a mechanism to recover the wM-Bus state machine by restarting the RX process

## Main features

- Supported wM-Bus modes:
  - **T-mode**: Frequent Transmit mode
  - **S-mode**: Stationary Mode
    - **S1-m mode**: Stationary mode with a mobile concentrator (one way only)
  - **C-mode**: Compact mode
- Support **Frame Format A** and **Frame Format B**
- Supported protocol layers:
  - **Phy**: unidirectional, can be used as a standalone MW
  - **DataLink**: bidirectional, following C-field packets are supported using callbacks that can be redefined by user:
    - *SND-NKE*: Reset Link after communication; Direction from Concentrator to Meter
    - *SND-UD*: Send User data; Direction from Concentrator to Meter. Meter shall respond with ACK
    - *SND-UD2*: Send User data; Direction from Concentrator to Meter. Meter shall respond with RSP-UD
    - *SND-NR*: Send Application Data; Direction from Meter to Concentrator without request Send/No reply
    - *SND-IR*: Installation Request; Direction from Meter to Concentrator; Concentrator shall respond with CNF-IR
    - *ACC-NR*: Access Request; Direction from Meter to Concentrator without request Send/No reply
    - *ACC-DMD*: Access Demand; Direction from Meter to Concentrator; Concentrator shall respond with ACK
    - *REQ-UD1*: Alarm request (Request User Data Class 1); Direction from Concentrator to Meter; Meter shall respond with RSP-UD or ACK
    - *REQ-UD2*: Data Request (Request User Data Class 2); Direction from Concentrator to Meter; Meter shall respond with RSP-UD
    - *ACK*: Acknowledgement; Both directions; Shall be sent after ACC-DMD, SND-UD or also REQ-UD1 when no alert happened
    - *CNF-IR*: Confirms the successful installation of the meter; Direction from Concentrator to Meter. Shall be sent after SND-IR
    - *RSP-UD*: Response of User Data; Direction from Meter to Concentrator. Shall be sent after REQ-UD1 or REQ-UD2
- Following macros can be defined to modify the functionality of the middleware:

  | **Name**                          | **Purpose**                                                                                                                                      |
  |-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
  | T1C1_ACTIVATED                    | Activate single protocol (Radio + packet) RX configuration for T1 + C1 gateway reception                                                         |
  | T1C1_ACTIVATED_C1_MODE            | Activate single protocol (Radio + packet) RX configuration for T1 + C1 gateway reception _only if C-mode is set_ (to be removed for other modes) |
  | AUTOMATIC_FORMAT_DETECTION_C_MODE | Activate dynamic frame format detection (A/B) in C-mode reception (to be removed for other modes)                                                |
  | PREAMBLE_AND_SYNC_IRQ_ENABLE      | Enable Radio event for Preamble detection and HW Sync detection                                                                                  |
  | WMBUS_RX_PERFORMANCE_ENABLED      | Enable RX performance optimizations                                                                                                              |
  | WMBUS_ACTIVE_POWER_MODE_ENABLED   | Enable active power mode to optimize RX, TX performances and power consumption                                                                   |
  | PROCESS_FRAME                     | Enable frame processing to populate RX Frame                                                                                                     |
  | WMBUS_FIRST_CRC_CHECK             | Activate 1st CRC verification                                                                                                                    |

## Contents

Contents of wM-Bus Middleware:

- DataLink:
  - Inc:
    - stm32wl3_wMBus_DataLink_timer.h: Header file of wM-Bus DataLink Timer module.
    - stm32wl3_wMBus_DataLink.h: Header file of wM-Bus DataLink module.
  - Src:
    - stm32wl3_wMBus_DataLink_timer.c: Source file of wM-Bus DataLink Timer module.
    - stm32wl3_wMBus_DataLink.c: Source file of wM-Bus DataLink module.
- Phy:
  - Inc:
    - stm32wl3_wMBus_Phy_pwr.h: Header file of wM-Bus Phy Power module.
    - stm32wl3_wMBus_Phy_radio.h: Header file of wM-Bus Phy Radio module.
  - Src:
    - stm32wl3_wMBus_Phy_pwr.c: Source file of wM-Bus Phy Power module.
    - stm32wl3_wMBus_Phy_radio.c: Source file of wM-Bus Phy Radio module.

## Known Limitations

- wM-Bus mode N not supported. 
- Frequent Access Cycle not supported.

</div>

<label for="collapse-section3" aria-hidden="true">__V1.0.9 / 22-October-2025__</label>
<div>

## Main Changes
###  Cleanup code: Macro removing and MCUAstyle adapting

## Main features

- Remove the following macros as they are always enabled by default:
  - WMBUS_NO_BLOCKING_HAL
  - WMBUS_CRC_IN_HAL
  - DEEPSTOP_ENABLE
- Cleanup code for better readability
- MCUAstyle adaptation for some MRSUBG structures

## Contents

Contents of wM-Bus Middleware:

- DataLink:
  - Inc:
    - stm32wl3_wMBus_DataLink_timer.h: Header file of wM-Bus DataLink Timer module.
    - stm32wl3_wMBus_DataLink.h: Header file of wM-Bus DataLink module.
  - Src:
    - stm32wl3_wMBus_DataLink_timer.c: Source file of wM-Bus DataLink Timer module.
    - stm32wl3_wMBus_DataLink.c: Source file of wM-Bus DataLink module.
- Phy:
  - Inc:
    - stm32wl3_wMBus_Phy_pwr.h: Header file of wM-Bus Phy Power module.
    - stm32wl3_wMBus_Phy_radio.h: Header file of wM-Bus Phy Radio module.
  - Src:
    - stm32wl3_wMBus_Phy_pwr.c: Source file of wM-Bus Phy Power module.
    - stm32wl3_wMBus_Phy_radio.c: Source file of wM-Bus Phy Radio module.

## Known Limitations

- Only supports mode T, S and C. 
- Frequent Access Cycle not supported.

</div>

<label for="collapse-section2" aria-hidden="true">__V1.0.7 / 27-June-2025__</label>
<div>

## Main Changes
###  Add support for **STM32CubeWL3** (STM32Cube for STM32WL3x lines) wM-Bus middleware supporting STM32WL3Rx devices 

## Main features

- Add support for STM32WL3Rx devices

## Contents

Contents of wM-Bus Middleware:

- DataLink:
  - Inc:
    - stm32wl3_wMBus_DataLink_timer.h: Header file of wM-Bus DataLink Timer module.
    - stm32wl3_wMBus_DataLink.h: Header file of wM-Bus DataLink module.
  - Src:
    - stm32wl3_wMBus_DataLink_timer.c: Source file of wM-Bus DataLink Timer module.
    - stm32wl3_wMBus_DataLink.c: Source file of wM-Bus DataLink module.
- Phy:
  - Inc:
    - stm32wl3_wMBus_Phy_pwr.h: Header file of wM-Bus Phy Power module.
    - stm32wl3_wMBus_Phy_radio.h: Header file of wM-Bus Phy Radio module.
  - Src:
    - stm32wl3_wMBus_Phy_pwr.c: Source file of wM-Bus Phy Power module.
    - stm32wl3_wMBus_Phy_radio.c: Source file of wM-Bus Phy Radio module.

## Known Limitations

- Only supports mode T, S and C. 
- Frequent Access Cycle not supported.

</div>

<label for="collapse-section1" aria-hidden="true">__V1.0.6 / 04-June-2025__</label>
<div>

## Main Changes
###  Add support for **STM32CubeWL3** (STM32Cube for STM32WL3x lines) wM-Bus DataLink middleware supporting STM32WL3x devices 

## Main features

- Support for all frame types using _weak_ functions that can be reimplemented in the application.
- ACC field increased on primary station messages and copied when generating response frames.

## Contents

Contents of wM-Bus Middleware:

- DataLink:
  - Inc:
    - stm32wl3_wMBus_DataLink_timer.h: Header file of wM-Bus DataLink Timer module.
    - stm32wl3_wMBus_DataLink.h: Header file of wM-Bus DataLink module.
  - Src:
    - stm32wl3_wMBus_DataLink_timer.c: Source file of wM-Bus DataLink Timer module.
    - stm32wl3_wMBus_DataLink.c: Source file of wM-Bus DataLink module.
- Phy:
  - Inc:
    - stm32wl3_wMBus_Phy_pwr.h: Header file of wM-Bus Phy Power module.
    - stm32wl3_wMBus_Phy_radio.h: Header file of wM-Bus Phy Radio module.
  - Src:
    - stm32wl3_wMBus_Phy_pwr.c: Source file of wM-Bus Phy Power module.
    - stm32wl3_wMBus_Phy_radio.c: Source file of wM-Bus Phy Radio module.

## Known Limitations

- Only supports mode T, S and C. 
- Frequent Access Cycle not supported.

</div>

<label for="collapse-section" aria-hidden="true">__V1.0.4 / 05-February-2025__</label>
<div>

## Main Changes
###  First Official Release of **STM32CubeWL3** (STM32Cube for STM32WL3x lines) wM-Bus Phy middleware supporting STM32WL3x devices 

## Contents

- Contents of wM-Bus Phy Middleware:
  - Inc:
    - stm32wl3_wmbphy_pwr.h: Header file of wM-Bus Phy Power module.
    - stm32wl3_wmbphy_radio.h: Header file of wM-Bus Phy Radio module.
  - Src:
    - stm32wl3_wmbphy_pwr.c: Source file of wM-Bus Phy Power module.
    - stm32wl3_wmbphy_radio.c: Source file of wM-Bus Phy Radio module.

## Known Limitations

- None

</div>

For complete documentation on STM32WL3x,visit: [[www.st.com/stm32WL3](http://www.st.com/stm32WL3)]

*This release note uses up to date web standards and, for this reason, should not be opened with Internet Explorer but preferably with popular browsers such as Google Chrome, Mozilla Firefox, Opera or Microsoft Edge.*