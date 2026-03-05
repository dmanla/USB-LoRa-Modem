# USB-LoRa-Modem: Long-Range P2P Terminal

## Overview
**USB-LoRa-Modem** is an open-hardware radio terminal designed to enable any USB-equipped device to communicate over long distances using LoRa modulation. It is optimized for **secure, off-grid text communication** and provides a robust link in environments where cellular or Wi-Fi infrastructure is unavailable.

The core of the device is the **EByte E22-900T30S**, providing high-power **1-Watt (30dBm)** transmission in the US-legal **915MHz** ISM band, with a focus on maximum range and hardware-level signal isolation.

---

## Key Security & Design Features
* **Active-Discharge Kill Switch**: A physical SPDT slide switch (**SW1**) that disconnects the buck converter and actively shorts the internal power rail to ground through a **10Ω** resistor (**R4**). This ensures the **1080µF** bulk capacitance is drained instantly, preventing any residual "heartbeat" transmissions after power-off.
* **EMI & Signal Integrity**: **22Ω** series resistors (**R3, R7**) are placed on the UART data lines (TX, RX). This dampens high-frequency harmonics and limits radiated EMI, ensuring the device remains quiet and the signal remains clean.
* **Hardware Flow Control**: The LoRa module's **AUX** pin is tied to the **CTS** line of the **CH343P**. This allows the host software to automatically manage data buffers, preventing packet loss during high-volume wireless transmissions.
* **High-Current Power Path**: Features a **TPS62A01** synchronous buck converter capable of delivering **1A peak current** to handle the significant power draw of 30dBm LoRa transmissions without voltage brownouts.

---

## Major Components
| Component | Part Number | Description |
| :--- | :--- | :--- |
| **LoRa Module** | **E22-900T30S** | 30dBm (1W) LoRa Transceiver (SX1262 based). |
| **USB-UART Bridge** | **WCH CH343P** | High-speed USB to serial converter with CTS support. |
| **Power Regulator** | **TPS62A01ADRL** | 1000mA Synchronous Buck Converter (5V to 3.3V). |
| **ESD Protection** | **USBLC6-2SC6** | Low-capacitance ESD protection for USB data lines. |

---

## Technical Specifications
* **Input Power**: USB VBUS (+5V, up to 700mA peak).
* **Frequency**: 902–928 MHz (Standard US ISM Band).
* **Range**: ~10km+ Line-of-Sight (Antenna dependent).
* **Logic Level**: 3.3V TTL.
* **EDA Software**: **KiCad 9.0.7**.

---

## Usage
1.  **Enable Device**: Flip **SW1** to the `ON` position.
2.  **Communication**: Open a serial terminal (e.g., `pyserial` or `minicom`) at **9600** baud (default).
3.  **Configuration**: To send **AT Commands**, the device must be in Configuration Mode (Requires M0/M1 pins to be set according to your hardware strapping).
4.  **Kill Session**: Flip **SW1** to the `OFF` position. The power rail is immediately grounded, and the radio is physically silenced.

## Front 3D Render
<img width="373" height="775" alt="image" src="https://github.com/user-attachments/assets/a93cab7e-2109-431f-94ba-68f9ee4b5f28" />


## Back 3D Render
<img width="395" height="760" alt="image" src="https://github.com/user-attachments/assets/1a2695de-6383-49ff-9a8e-2c50c4d4cf55" />


## License

All PCB design files and hardware are released under the [Creative Commons Attribution Share Alike 4.0](https://choosealicense.com/licenses/cc-by-sa-4.0/) license.
