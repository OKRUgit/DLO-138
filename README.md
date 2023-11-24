# DLO-138
An open source firmware for DSO-138 Oscilloscope. 
![Photo](https://github.com/ardyesp/DLO-138/blob/master/pics/pic4.png)

DSO-138-отличная часть аппаратного обеспечения на основе процессора ARM Cortex M3 Core STM32F103 и достаточным для большинства начинающих пользователей.Стоковая прошивка, хотя и довольно отзывчивая, может использовать несколько улучшений.Основным недостатком, который вызвал разработку прошивки DLO-138, является неспособность довести данные о форме волны в компьютер для дальнейшего анализа и отсутствия второго канала.Инженеры по устранению неисправностей аппаратного обеспечения необходимо отметить контрольные точки на форме волны, чтобы наличие другого аналогового или цифрового канала может значительно улучшить анализ.Эта прошивка надеется улучшить эти проблемы.

## Функции
- два аналоговых канала
- Два цифровых логических канала (SWDIO и SWDIO PINS (PA13 и PA14) на борту)
- Интерфейс последовательного порта для полученных данных формы сигнала
- триггер -источник выбирается из аналогового канала 1 или цифрового канала
- Опция для использования роторного энкодера вместо + - и SEL -переключателей
- Глубина выборки 2K

This firmware can be used on stock DSO-138 hardware as well. Select one of the pre-compiled binaries to suit the board. Follow the firmware upgrade instructions for DSO-138. At any time, you can reflash DSO-138 with JYE Tech provided firmware.

# Cost
Extra features come at an additional cost. In the case of DLO-138, it is the loss of lowest timebase. Maximum sampling rate in DLO-138 is 20 µs/div instead of 10 µs/div. In the 20 µs/div range, firmware under-samples ADC channels, often reading same data twice. To use the second analog channel, analog front end has to be duplicated on a daughter board. On a stock hardware, this firmware can be used to provide two digital logic channels.

# Build
The build environment uses Arduino. For help with setting up IDE visit http://www.stm32duino.com

For graphics output, this project depends on the Adafruit GFX Library v1.1.4.
Install it via the Library Manager of your Arduino IDE.
Other/newer versions of this library are likely to not compile or will give you a black screen.

# Hardware
Following changes can be applied selectively, to get maximum functionality from board. The firmware can be run on unmodified hardware as well.
![Mod Schematic](https://github.com/ardyesp/DLO-138/blob/master/pics/HardwareMod.png)

# Usage:
	Push button in encoder (SEL if using switches) moves focus to next parameter
	Left/Right turn in encoder (+/- if using switches) changes the parameter which is in focus
	Short press OK to HOLD the waveform and output it on serial port
	Long press OK button:
	
		Focus				Action
		Trigger Level		Zero the trigger level to Analog channel 1
		Wave X scrollbar	Center waveform on screen (at trigger point)
		Wave Y cursor		Zero the cursor. If Analog CH1 coupling is GND, waveform reference base is set 
		Other				Toggle on screen Analog CH1 statistics display

	Press and hold OK button at power up to reset settings to default
	
# Flash binaries directly via serial interface

When using Windows you can follow the guide from jyetech:
https://jyetech.com/wp-content/uploads/2018/07/dso138-firmware-upgrade.pdf

The guide uses the graphical programming tool provided by ST:
https://www.st.com/en/development-tools/flasher-stm32.html

---

When using Linux, you can use the open source command line tool stm32flash:

Install stm32flash:
```
sudo apt-get install stm32flash
```

Connect your TTL-UART-to-USB converter to the DSO138 and bridge jumpers J1 and J2 on the back of the PCB just like in the above manual.

Unlock the flash of the STM32:
```
sudo stm32flash /dev/ttyUSB0 -k -b 115200

sudo stm32flash /dev/ttyUSB0 -u -b 115200
```

Flash new firmware:
```
sudo stm32flash /dev/ttyUSB0 -w binaries/DLO-138_switches_1.0.bin -b 115200
```

Remove the solder bridges on J1 and J2 and enjoy the alternative firmware on your DSO138.
 		

# References
DSO-138 - http://www.jyetech.com/Products/LcdScope/e138.php

STM32Duino - http://www.stm32duino.com

STM32F103 - http://www.st.com/en/microcontrollers/stm32f103.html

Adafruint Graphics Library - https://github.com/adafruit/Adafruit-GFX-Library

Parallel 8 bit ILI9341 library - https://github.com/stevstrong/Adafruit_TFTLCD_8bit_STM32


