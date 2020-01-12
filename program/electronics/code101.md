# Introduction to embedded programming in C

Programming is a powerful skill. Not just useful, not just good for your career, not just a moneymaker, but powerful.

- [Introduction to embedded programming in C](#introduction-to-embedded-programming-in-c)
  - [Embedded programming](#embedded-programming)
  - [I know Arduino scripting language. Do I still need to learn C?](#i-know-arduino-scripting-language-do-i-still-need-to-learn-c)
  - [The datasheet](#the-datasheet)
  - [Setting up AVR-GCC Toolchain on Linux](#setting-up-avr-gcc-toolchain-on-linux)
  - [The basic idea behind a microcontroller](#the-basic-idea-behind-a-microcontroller)
  - [Setting Inputs and Outputs. The DDR (Data Direction Registers)](#setting-inputs-and-outputs-the-ddr-data-direction-registers)
  - [PORT Registers](#port-registers)
  - [PIN Registers](#pin-registers)
  - [Hello world program](#hello-world-program)
  - [The button and LED program](#the-button-and-led-program)
  - [Bitwise operations](#bitwise-operations)
  - [Making your life easier: Macros](#making-your-life-easier-macros)
  - [Compiling the program](#compiling-the-program)
  - [The Makefile](#the-makefile)
  - [The programmer](#the-programmer)
- [Resources for AVR Programming](#resources-for-avr-programming)
  - [- A beginnersGuide to AVR (by Aravind E Vijayan from NIT-Calicut)](#a-beginnersguide-to-avr-by-aravind-e-vijayan-from-nit-calicut)

## Embedded programming

In this section we are going to learn to program an Atmel family microcontroller (attiny44 in the examples below) using AVR-GCC toolchain in C language. Programming is a huge topic. It will take long time to master.

For learning to code you **have to** code. There is a difference between **knowing** the path and **walking** the path. Walk-the-path.

* Basics about writing code
  * Important: Always add Author, date, description and license to the header of your code
  * Always comment your code
  * Init and loop sections
  * Digital output
  * Analog output (PWM)
  * Digital input
  * Analog input (ADC) 8 bit/10bit
  * Pull up / down resistors (10k)
  * Multitasking? Polling
  * Debounce buttons
* Embedded Programming. 3 levels depending on proficiency:
  * Beginners: Arduino IDE
  * Intermediates: C
  * Advanced: Assembly
* Why C? [https://www.youtube.com/watch?v=ERY7d7W-6nA&feature=youtu.be](https://www.youtube.com/watch?v=ERY7d7W-6nA&feature=youtu.be)
* Why Assembly? [https://en.wikipedia.org/wiki/Apollo_Guidance_Computer](https://en.wikipedia.org/wiki/Apollo_Guidance_Computer)

## I know Arduino scripting language. Do I still need to learn C?

Please watch this video https://www.youtube.com/watch?v=ERY7d7W-6nA

## The datasheet

The first thing you should know about embedded programming is that **you cannot program a microcontroller without reading the datasheet** of that specific microcontroller.

> Download the [Attiny 44 Datasheet](http://www.atmel.com/images/doc8006.pdf) and browse through it.

## Setting up AVR-GCC Toolchain on Linux

For writing code you just need a text editor, like atom. AVR-GCC is a tool-chain that will help you with the software development process, but doesn’t do anything about burning the final executable (the hex file) to the microcontroller. For that we need to install ** AVR D**ownloader ** U**ploa**DE**r (avrdude).

In Ubuntu

`sudo apt install avrdude gcc-avr binutils-avr avr-libc`

## The basic idea behind a microcontroller

A microcontroller is an electronic device with a CPU, memory and some other hardware that interfaces with the external world through a number of pins.

![](img/101/t85.jpg)

Some pins have a fixed function and cannot be changed, like VCC or GND. The rest of the pins can be configured as inputs (for receiving data from sensors) or outputs (to move motors or turn on lights).

![](img/101/t85pinout.jpg)

The general workflow is that you hook your inputs and outputs to the microcontroller pins and then later in your code you program the logic that enables reading from the sensors and actions in the actuators. This way, someone with little knowledge in electronics engineering can design and program a circuit board.

## Setting Inputs and Outputs. The DDR (Data Direction Registers)

To tell the microcontroller if a pin is an input or an output we have modify a register called Data Direction Register. A register is like a DIP switch with 8 independently switches that can be set to 0 (off) or 1 (on).

![](img/101/register.jpg)

There is one of these for each port A and B, named DDRA and DDRB.

By default all pins are configured as input.

> Exercise: Read this tutorial https://www.arduino.cc/en/Tutorial/DigitalPins

## PORT Registers

PORT registers write data (0 or 1) to the pins, when they are configured as outputs. If the pins are set as inputs, PORT activates or deactivates the internal pull-up resistor.

## PIN Registers

PIN registers read data from the pins when they are configured as inputs.

## Hello world program

If you are creating a new program, do not start from scratch. Start by editing an existing program.

```c
#define F_CPU 1000000UL
#include <avr/io.h>
#include <util/delay.h>

int main (void)
{

 DDRB = 0b00000100; // set PB2 as output in DDRB

 while(1) {
          // set PB2 high to turn led on
          PORTB = 0b00000100;
          _delay_ms(1000);
          // set PB2 low to turn led off
          PORTB = 0b00000000;
          _delay_ms(1000);
          }
}
```

## The button and LED program

```c
#define F_CPU 1000000UL
#include <avr/io.h>

// This program turns LED ON when the button is pressed

int main (void)
{

  DDRB |= (1 << PB2);
  // set PB2 as output in DDRB

  DDRA &= ~(1 << PA3);
  // set PA3 as input in DDRA

  PORTA = 0B00001000;
  // SET PULL UP RESISTOR IN PA3

 while(1) {
   if (testbit(PINA,PA3))

   PORTB = 0b00000000;
   // set PB2 low to turn led off

   else

   PORTB = 0b00000100;
   // set PB2 high to turn led on
        }
}
```

## Bitwise operations

So far we have been writing a full register. But it is also possible to operate in a single bit of a register. The syntax in C is rather complex. That is why the first thing we will do is defining macros.

## Making your life easier: Macros

Macros are aliases that you can use to avoid typing complex syntax.

```c
#define setbit(register, bit)   (register) |=  (1 << (bit))
#define clearbit(register, bit) (register) &= ~(1 << (bit))
#define testbit(register, bit)  (register) &   (1 << (bit))
```

Then you can simply use

```c
setbit(PORTA, PA0)
clearbit(PORTB, PB3)
testbit (PORTA, PA2)
```

This makes your code much easier to understand. The precompiler will substitute the macros out at compile time and you will be left with the exact same code in your AVR.

## Compiling the program

The microcontroller does not understand C code. C, like other programming languages was created for humans. Microcontrollers only understand hex instructions, but those are difficult to write or remember. It is necessary to compile the program to obtain a `.hex` file that will be flashed in the microcontroller.

## The Makefile

http://www.ladyada.net/learn/avr/avrdude.html

## The programmer

To flash the `.hex` code to the microcontroller we need a ISP programmer. We are going to fabricate our custom ISP.



# Resources for AVR Programming 

- [avr-tutorials.com](https://www.avr-tutorials.com/)
- [A beginnersGuide to AVR (by Aravind E Vijayan from NIT-Calicut)](https://www.researchgate.net/publication/263084656_A_Beginners_Guide_to_AVR)
---
[Back to Summary](../summary.md)
