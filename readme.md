# CAT4004 dimmer Chip Class
The CAT4004 is a 4 channel LED dimmer chip form [ON Semiconductors](https://www.onsemi.com/).  
The current per channel is easily programmeble through a single resistor.  
The brightness bontrol is done by one input line only.  

There are different types of CAT4004 chips:
- no index  
the chip features 5 intensity settings 1/1, 1/2, 1/4, 1/8 and 1/16 with max. 40 mA per channel
- index A  
the chip features 32 intensity settings 31/31 ... 0/31 with max. 40 mA per channel
- index B  
the chip features 32 intensity settings 31/31 ... 0/31 with max. 25 mA per channel
 

## CAT4004 class
The CAT4004 class is a simple interface to set the LED brgihtness controlled by a CAT4004 chip.
It is build around Arduino Framework and makes use of
- pinMode
- digitlWrite
- millis

It should be no problem to adopt this to other platforms.

When using interrupts there is no need for the state machine and task process.
The current implementation features a semi non preemtive multitasking

it uses only 5 functions
1. Constructor: cat4004(uint8_t brightnessPin=0xFF,unsigned char Index=' ');
2. Task:		void process(void);
3. Enable:		void set_brightness(uint8_t brightness);
4. Disable:		void disable(void);
5. Query:		uint8_t get_brightness(void);		

###	cat4004
The consturctor of the class needs to be called with the used digital pin and the chip Index.

### process
The task funktion. It should be called in a less than 10 ms intervalls.

### set_brightness
call to set the desired brightness level in %. Any percentage above 100 % will disable the LED.
The LED will be set to the closes level less than the desired level.
E.g. requesting a brigtness of 20 % will result in 12.5 % on a CAT4004 and in 19.4% on a CAT4004B.    	
	
### disable 
equals to set_brigthness(0)	

### get_brightness
retrieves current brightness level
