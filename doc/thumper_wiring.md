## Thumper demo wiring

Below you can find how the  hardware components should be connected.

<br>

|PmodRF2	 | Olimex STM32-E407 |
|:-----------:|:-----------:|
|VCC/12| 3V3|
|GND/11| GND|
|INT/7| D8|
|RST/8| D9|
|CS/1| D10|
|MOSI/2| D11|
|MISO/3| D12|
|SCLK/4| D13|

<br>

|RoboClaw | Olimex STM32-E407 |
|:-----------:|:-----------:|
|S1| USART6_TX (UEXT/3)|
|GND| GND (UEXT/2)|

<br>


|Logitech Extreme 3D PRO | Olimex STM32-E407 |
|:-----------:|:-----------:|
|Joystick USB<sup>1</sup>| USB_OTG2|


<br>
  
______
  


<sup>1)</sup> connected to the external 5 VDC power supply