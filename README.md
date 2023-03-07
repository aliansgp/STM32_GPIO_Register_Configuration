# Intro
project modified with CubeMX with no pin as output

but with GPIO registers, GPIOD Pin 14 and 15 are set as output and turned ON.

## Start working with GPIO registers
first of all you need to know the address of target GPIO

you can find it in your microcontroller mannual, Memory-map session

![Screenshot 2023-03-07 094222](https://user-images.githubusercontent.com/38432834/223335862-35838572-5a52-4cb9-8c6f-4e607559fac8.png)

this address are defined as GPIOx_BASE in editor

## Set GPIO pin as output
to set GPIO as output you need to configure GPIO-port-mode-register(GPIOx_MODER) and set pin bit as 01 for output 

![image](https://user-images.githubusercontent.com/38432834/223341411-8c78dea1-b178-484c-a2ac-446ebd388213.png)


offset for this register is 0x00 (first of each GPIO Address is this register).

use this code to Define GPIOx Mode register:
```
#define GPIOx_MOD (*((volatile unsigned long *)(GPIOx_BASE + 0x00)))
```
then you need to set LSB of pin bits as 1

for example for pin 15, just SET bit 30.

![image](https://user-images.githubusercontent.com/38432834/223338710-1dc50711-e5c2-4f87-813f-5127bfbe2579.png)


in main function write this code:
```
SET_BIT(GPIOD_MOD,1<<30);
```
SET_BIT is build-in and  shift '1' , 30 times to SET bit 30.

**Done!** now our GPIOx pin 15 is set as output.

## SET The Pin
to SET the pin, you need to to configure GPIO-port-bit-set/reset-register(GPIOx_BSRR) and set pin bit as 1 for SET

![image](https://user-images.githubusercontent.com/38432834/223341668-39c8a624-6f90-495f-a88c-e3a8f8caee4a.png)

offset for this register is 0x18

![image](https://user-images.githubusercontent.com/38432834/223344345-5c94e396-724d-4a7d-843c-12b20c8793f3.png)


use this code to Define GPIOx set/reset register:
```
#define GPIOx_SET (*((volatile unsigned long *)(GPIOx_BASE + 0x18)))
```

then you need to set pin bit

for our modified pin (pin 15), use this code in main function:
```
SET_BIT(GPIOx_SET,1<<15);
```
SET_BIT shift '1' , 15 times to SET bit 15.

**Done!** now GPIOx pin 15 is ON.




