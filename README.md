# refArduinoCBlink
Reference for communicating with arduino uno r3 in Mint linux 18 with avrdude

HOW TO on this website: [click here](http://linuxg.net/how-to-install-avrdude-6-1-on-ubuntu-14-10-ubuntu-14-04-and-derivative-systems/)

* Installed avr-gcc and helpers
```
sudo apt-get install gcc-avr avr-libc gcc-doc
```

* Install avrdude
```
sudo apt-get install avrdude
```

* Git this repo


* Compile .c file to generate .o
```
avr-gcc -Os -DF_CPU=16000000UL -mmcu=atmega328p -c -o longblink.o longblink.c
```
```
-DF_CPU defines the cpu freq for _delay_ms function.  UL = unsigned long
-mmcu specifies AVR/MCU instruction set
```

* generate object file
```
avr-gcc -mmcu=atmega328p longblink.o -o longblink
```

* translate object file
```
avr-objcopy -O ihex -R .eeprom longblink longblink.hex
```
```
-O output target
-R remove section
```

* write to arduino
```
avrdude -F -V -c arduino -p ATMEGA328P -P /dev/ttyACM0 -b 115200 -U flash:w:longblink.hex 
```
```
-F override invalid signature
-V do not verify
-c specify programmer
-p specify device
-P port for device comms
-b baudrate
-U memory specification; flash/write/filename
```
