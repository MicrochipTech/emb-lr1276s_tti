# EMB-LR1276S_TTI
> “Wireless Made Easy!" - Develop with the EMBIT EMB-LR1276S LoRaWAN Module and Microchip LoRaWAN stack on TTI join server

<p>

<a href="http://www.embit.eu/products/wireless-modules/emb-lr1276s/" target="_blank">
<img border="0" alt="Embit_logo" src"http://www.embit.eu/wp-content/uploads/Embit_round_logo_23.png" width="150">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp

<a href="https://www.microchip.com/design-centers/security-ics/trust-platform/trust-go/trust-go-lora-secure-authentication-with-join-servers" target="_blank">
<img border="0" alt="Microchip_logo" src="Doc/Microchip_logo.png" width="150">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp

<a href="https://www.thethingsindustries.com" target="_blank">
<img border="0" alt="TTI_logo" src="Doc/TTI_logo.png" width="150">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp

<a href="https://youtu.be/eXXl485fbBE" target="_blank">
<img src="https://img.youtube.com/vi/eXXl485fbBE/0.jpg" 
alt="Secure Authentication for LoRa with the ATECC608A and The Things Industries (TTI) Join Server" width="240"></a>

</p>
</a>

**This guide will direct you through the process of getting started with developing a secure LoRa end device product using Embit EMB-LR1276S module along with TTI Join server.**
</br>
The Things Industries created a product and a service that delivers secure join, secure communication and secure key provisioning.

1. [Material required](#step1)
2. [Software](#step2)
3. [Hardware setup](#step3)
4. [Sample Application Code](#step4)
5. [Claiming and Activating the device](#step5)
6. [Running the demo](#step6)

## Material required <a name="step1"></a>

Here we will use the Evaluation Board EMB-LR1276S-Dev_Board from EMBIT.</br>
This board allows the user to exploit all the capabilities of Embit’s module EMB-LR1276S, simplifying the implementation of a prototype of a LoRa® communication system.</br>
The board provides a simple connection to a computer or an external processor via USB. </br>
For testing purpose, several pin headers are present to exploit the capabilities of the module and ease the development of custom designs.</br>

![](Doc/EMB-LR1276S-Dev_Board.png)
</br>

The EMB-LR1276S LoRaWAN module embeds a Microchip SAM R34 LoRa(r) device and the ATECC608A Secure element.</br>
<p>

<a href="http://www.embit.eu/products/wireless-modules/emb-lr1276s/" target="_blank">
<img border="0" alt="EMB-LR127S Block Diagram" src="Doc/EMB-LR1276S_Block_Diagram.png" width="150">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp

<a href="http://www.embit.eu/products/wireless-modules/emb-lr1276s/" target="_blank">
<img border="0" alt="EMB-LR127S" src="Doc/EMB-LR1276S.png" width="150">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp

<a href="https://www.microchip.com/wwwproducts/en/ATSAMR34J18" target="_blank">
<img border="0" alt="ATSAMR34" src="Doc/ATSAMR34.png" width="150">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp

<a href="https://www.microchip.com/wwwproducts/en/ATECC608A-TNGLORA" target="_blank">
<img border="0" alt="ATECC608A" src="Doc/ATECC608A.png" width="150">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp

</p>
</a>

Purchase the <a href="http://www.embit.eu/products/evaluation-kits/emb-lr1276s-evk/" target="_blank">EMB-LR1276S Evaluation board</a>
</br>
![](Doc/EMB-LR1276S-Dev_Board.png)
</br>

Purchase a LoRa(r) Gateway from <a href="https://www.thethingsindustries.com/technology/hardware#gateway" target="_blank">The Things Industries</a>
</br>
![](Doc/TTI_Hardware.png)
</br>


## Software <a name="step2"></a>

- Download and install Atmel Studio 7.0 IDE. </br>
https://www.microchip.com/mplab/avr-support/atmel-studio-7

- Open Atmel Studio 7.0 IDE. </br>
- Then, you need Advanced Software Framework (ASFv3) v3.47.0 release or upper release. </br>
Install ASFv3 as an extension to Atmel Studio from the menu: Tools -> Extensions and Updates …
- Once the installation is complete, you must restart Atmel Studio. </br>
- Download and install a serial terminal program like Tera Term. </br>
https://osdn.net/projects/ttssh2/releases/

Note: ASFv3 is an MCU software library providing a large collection of embedded software for AVR® and SAM flash MCUs and Wireless devices. ASFv3 is configured by the ASF Wizard in Atmel Studio 7.0 (installed as an extension to Studio). ASFv3 is also available as a standalone (.zip) with the same content as Studio extension (https://www.microchip.com/mplab/avr-support/advanced-software-framework).

Important:
Until the next Atmel Studio IDE release, you have to manually install the Device Part Pack for developing with SAMR34/R35 on Atmel Studio 7.0 IDE.
(all products released in between IDE releases of Atmel Studio should be manually added by user to develop applications).
- Go to Tools -> Device Pack Manager </br>
- Check for Updates </br>
- Search for SAMR34 and click install </br>
- Repeat the same for SAMR35 </br>
- Restart Atmel Studio 7.0 IDE </br>

- Download and install Segger J-Link Software and Documentation pack (version 6.42 or higher)</br>
https://www.segger.com/downloads/jlink/#J-LinkSoftwareAndDocumentationPack
</br>


## Hardware setup <a name="step3"></a>

- Plug the antenna to the SMA connector ANT
- Attach a USB cable to EMB-LR1276S-DEV_BOARD's CMD_USB micro-B port. The USB ports powers the board and enables the user to communicate with the kits over a serial console.
- Plug the Segger J-Link Lite board to the EMB-LR1276S-DEV_BOARD's JTAG connector (2x10 ways 2.54mm pitch male header)
- Attach a USB cable to J-Link Lite board
</br>
![](Doc/setup.png)
</br>

- Wait for USB driver installation and COM ports mounting. </br>
- Launch Tera Term program and configure the serial ports mounted with: **115200 bps, 8/N/1**

## Sample Application Code <a name="step4"></a>

Open the "APPS_ENDDEVICE_DEMO" project with Atmel Studio 7 IDE</br>
From the top menu, go to Project -> APPS_ENDDEVICE_DEMO Properties</br>
From Tool settings, select your board as SAM-ICE with SWD interface</br>
Make sure to select ATSAMR34J18 from the list</br>
![](Doc/J-LINK_PROGRAMMING.png)
</br>
Build and download the project by clicking the empty green "Run without debugging" triangle
</br>
![](Doc/AtmelStudio.png)
</br>
Open the Tera Term UART console previously configured at 115200 bps, 8-data bits/No parity/1-stop bit
</br>
Press the "Reset" button on the EMB-LR1276S-DEV_BOARD to see output printed to the console
</br>
Observe the following identifiers coming from the ATECC608A Secure Element
</br>
![](Doc/UART_Console1.png)
</br>


In order to pre-commission a device using ATECC608A secure element in TTI Activation, the following idenfiers are required:

- DevEUI: LoRaWAN device 64-bit unique identifier assigned by the Device manufacturer (or using Secure Element default value)
- JoinEUI: LoRaWAN JS 64-bit unique identifier of the Join Server on which AppKey of the device is stored


## Claiming and Activating the device <a name="step5"></a>

TTI and Microchip developed a security solution for LoRaWAN that enables secure key provisioning and secure cryptographic operations using secure elements.
</br>
- <a href="https://www.thethingsindustries.com/technology/security-solution" target="_blank">End-to-end LoRaWAN Security solution</a></br>

Claiming and Activating the device within TTI Servers are the next steps described in the guides below:</br>
- <a href="https://enterprise.thethingsstack.io/v3.3.2/guides/claim-atecc608a/" target="_blank">Claim ATECC608A Secure Elements</a></br>
- <a href="https://enterprise.thethingsstack.io/v3.3.2/guides/cloud-hosted/tti-join-server/activate-devices-cloud-hosted/" target="_blank">Activate devices on the Things Industries Cloud Hosted</a></br>

You can also refer to the Microchip Workshop which was provided at The Things Conference 2020.</br>
<a href="https://github.com/MicrochipTech/secure_lorawan_with_tti" target="_blank">“Wireless Made Fun!" - Secure Authentication with SAMR34 & ATECC608A and The Things Industries’s Join Server</a></br>


## Running the demo <a name="step6"></a>

Go back to the Tera Term UART console
</br>
![](Doc/UART_Console2.png)
</br>
Press "1" to start the Demo Application
</br>
Select the band where your device is operating
</br>
![](Doc/UART_Console3.png)
</br>
Then, the end device application transmits a Join Request message. If a Join Accept message was received and validated, the SAM R34 Xplained Pro board will be joined to the Join Server.
</br>
![](Doc/UART_Console4.png)
</br>
Press "2" to send a packet consisting of a temperature sensor reading
</br>
![](Doc/UART_Console5.png)
</br>

