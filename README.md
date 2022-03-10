# Design of 3-bit Flash ADC

This repository contains the design of 3-bit flash ADC which was created as part of the Mixed-Signal Marathon conducted by FOSSEE, IIT-Bombay and VSD Corp

# Abstract

This study presents a 3-bit Flash Analog to Digital Converter for low-power integrated circuits and system applications, which will be implemented using the ngspice and verilog programming languages. The circuit design, implementation and analysis will be done using FOSSEE’s eSim software. he 3-bit Flash ADC is designed using comparator and a priority encoder to facilitate the conversion of analog to digital signals. This 3-bit Flash ADC can be used in the design of large integrated circuits which has many digital decoding functions.

# Reference Circuit diagram

![ckt_photo_2022-02-28_14-53-48](https://user-images.githubusercontent.com/89923461/157565405-db661ece-1fdd-49a7-b383-3e466015440c.jpg)

# Circuit Design

The Flash ADC is a kind of analog - to - digital that works by comparing analog inputs to reference voltages and then converting them to digital data. A resistor ladder, comparator, and encoder are all common elements of a Flash ADC. 

In the Flash ADC, the voltage divider circuit is a basic network of series resistors with an input voltage that is scaled down along the resistors. The main goal of this circuit is to scale down and produce a voltage ratio based on the resistor's position. For dividing the voltage with regard to the reference voltage, we utilise a voltage divider circuit with 8 resistors in this circuit.

The comparator circuit is used to compare the inputs with the Vref reference voltage and the voltage divider inputs. We use a basic opamp to compare the voltages in the comparator circuit. The output voltage will be Vcc if the voltage Vin is higher than Vref. The output voltage will be -Vcc if the voltage Vin is less than Vref.

The encoding of 2^^N inputs to N outputs is performed by an encoder, which is a type of combinational circuit. When numerous inputs are high at the same time, this basic encoder has a difficulty. The priority encoder is used to solve this problem. The output of Priority Encoder is based on the highest priority input. We'll utilise an 8 x 3 priority encoder as the encoding circuit in this circuit. We'll use ngspice and verilog software to build a 3-bit Flash ADC circuit and test it with the waveform received as an output.















