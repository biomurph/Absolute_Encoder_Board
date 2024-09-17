# Absolute Encoder
Welcome to the Open-Source Absolute Encoder Board Repository. Here you will find hardware and software files that support the Absolute Encoder.

## What is it?
Encoders come in different types. Most people are familiar with [quadrature encoders](https://en.wikipedia.org/wiki/Incremental_encoder#Quadrature_outputs), which use two pins that change state sequentially in different order depending on direction. One of the limitations is that a microcontroller needs to be paying attention (usually with interrupts) in order to keep track of each step and count accordingly CW or CCW steps, usually with a pin change interrupt scheme. In certain applications, the need for interrupts and constant attention can be limiting. Enter the Absolute encoder. This device can have 3 or more pins that maintian their coded state to show their rotational position. That means that any time you want to, you can read the encoder pins and get the state withoug having to always keep track. Why would you want an absolute encoder over a quadrature encoder?

- You are using a Raspberry Pi or other single board computer. These are powerful devices, but they run thier software under an operating system which can make it hard to catch fast changes in a quadrature signal. All you need is one missed step to be off track. 
- You have encoder inputs but no room or overhead to provide the user dynamic feedback. Say you have a couple of dials on your project box, with a sticker or other static indicator of dial position. The absolute encoder will reliably report it's rotational position whenever asked, without having to keep track of dial movement.

Those two reasons are good enough for me! 

## How does it work?
The encoders in the project use [Gray Code](https://en.wikipedia.org/wiki/Gray_code), also know as Reflected Binary Code. It was invented in order to avoid electro-mechanical glitches in rotary circuits. A rotoary switch, for example that outputs a Binary Coded Decimal (BCD) for example may have more than one binary digit switching during the transition between positions. This means that it can be possible to misread the rotational position at the transition point between rotational sections. With Gray Code, only one digit is changed during each rotational transition, making it far more stable and resistant to bad readings. Here is a chart of Decimal, Binary, and Grey encoding.

Decimal  | Binary  | Gray
-------- | ------- | -----
0  | 0000 | 0000
1  | 0001 | 0001
2  | 0010 | 0011
3  | 0011 | 0010
4  | 0100 | 0110
5  | 0101 | 0111
6  | 0110 | 0101
7  | 0111 | 0100
8  | 1000 | 1100
9  | 1001 | 1101
10  | 1010 | 1111
11  | 1011 | 1110
12  | 1100 | 1010
13  | 1101 | 1011
14  | 1110 | 1001
15  | 1111 | 1000

Here's another rendering of the Gray Code, arranged in a circle. This is the bit pattern of the dial when it is traveled counter clockwise.

![GrayCodeWheel](assets/GrayCodeWheel.bmp)

## Hardware

The hardware is in prototype. Current goal is to design a 2-up encoder board with a PISO shift register for acquiring the encoder positions. This 2-up board will be daisy-chainable with sister boards using the same PISO pins to add as many pairs of encoders that you want!

## Software

Arduino library is in the works that will read and decode as many Gray Code encoders that you have daisy chained together!

