# Design of 3-bit Flash ADC

This repository contains the design of 3-bit flash ADC which was created as part of the Mixed-Signal Marathon conducted by FOSSEE, IIT-Bombay and VSD Corp

# Contents

- [Abstract](#abstract)
- [Reference Circuit diagram](#reference-circuit-diagram)
- [Circuit Design](#circuit-design)
- [Tools Used](#tools-used)
- [Verilog Code](#verilog-code)
- [Makerchip and NgVeri](#makerchip-and-ngveri)
- [Schematics](#schematics)
- [Waveform](#waveform)
- [Netlist](#netlist)
- [Author](#author)
- [Acknowledgements](#acknowledgements)
- [References](#references)
- 
# Abstract

This study presents a 3-bit Flash Analog to Digital Converter for low-power integrated circuits and system applications, which will be implemented using the ngspice and verilog programming languages. The circuit design, implementation and analysis will be done using FOSSEE’s eSim software. he 3-bit Flash ADC is designed using comparator and a priority encoder to facilitate the conversion of analog to digital signals. This 3-bit Flash ADC can be used in the design of large integrated circuits which has many digital decoding functions.

# Reference Circuit diagram

![ckt_photo_2022-02-28_14-53-48](https://user-images.githubusercontent.com/89923461/157565405-db661ece-1fdd-49a7-b383-3e466015440c.jpg)

# Circuit Design

The Flash ADC is a kind of analog - to - digital that works by comparing analog inputs to reference voltages and then converting them to digital data. A resistor ladder, comparator, and encoder are all common elements of a Flash ADC. 

In the Flash ADC, the voltage divider circuit is a basic network of series resistors with an input voltage that is scaled down along the resistors. The main goal of this circuit is to scale down and produce a voltage ratio based on the resistor's position. For dividing the voltage with regard to the reference voltage, we utilise a voltage divider circuit with 8 resistors in this circuit.

The comparator circuit is used to compare the inputs with the Vref reference voltage and the voltage divider inputs. We use a basic opamp to compare the voltages in the comparator circuit. The output voltage will be Vcc if the voltage Vin is higher than Vref. The output voltage will be -Vcc if the voltage Vin is less than Vref.

The encoding of 2<sup>N</sup> inputs to N outputs is performed by an encoder, which is a type of combinational circuit. When numerous inputs are high at the same time, this basic encoder has a difficulty. The priority encoder is used to solve this problem. The output of Priority Encoder is based on the highest priority input. We'll utilise an 8 x 3 priority encoder as the encoding circuit in this circuit. We'll use ngspice and verilog software to build a 3-bit Flash ADC circuit and test it with the waveform received as an output.

# Tools Used

- eSim: *a open-source EDA tool*
- Makerchip: *online verilog/SV simulator*

# Verilog Code

The digital part of the circuit, priority encoder is designed using verilog.

```
module prior(d_out, d_in);

   output [2:0] d_out;
   input [7:0] d_in ;

assign d_out = (d_in[7] ==1'b1 ) ? 3'b111:
               (d_in[6] ==1'b1 ) ? 3'b110:
               (d_in[5] ==1'b1 ) ? 3'b101:
               (d_in[4] ==1'b1) ? 3'b100:
               (d_in[3] ==1'b1) ? 3'b011:
               (d_in[2] ==1'b1) ? 3'b010:
               (d_in[1] ==1'b1) ? 3'b001:
               (d_in[0] ==1'b1) ? 3'b000: 3'bxxx;

endmodule

```

# Makerchip and NgVeri

```
\TLV_version 1d: tl-x.org
\SV
/* verilator lint_off UNUSED*/  /* verilator lint_off DECLFILENAME*/  /* verilator lint_off BLKSEQ*/  /* verilator lint_off WIDTH*/  /* verilator lint_off SELRANGE*/  /* verilator lint_off PINCONNECTEMPTY*/  /* verilator lint_off DEFPARAM*/  /* verilator lint_off IMPLICIT*/  /* verilator lint_off COMBDLY*/  /* verilator lint_off SYNCASYNCNET*/  /* verilator lint_off UNOPTFLAT */  /* verilator lint_off UNSIGNED*/  /* verilator lint_off CASEINCOMPLETE*/  /* verilator lint_off UNDRIVEN*/  /* verilator lint_off VARHIDDEN*/  /* verilator lint_off CASEX*/  /* verilator lint_off CASEOVERLAP*/  /* verilator lint_off PINMISSING*/   /* verilator lint_off BLKANDNBLK*/  /* verilator lint_off MULTIDRIVEN*/   /* verilator lint_off WIDTHCONCAT*/  /* verilator lint_off ASSIGNDLY*/  /* verilator lint_off MODDUP*/  /* verilator lint_off STMTDLY*/  /* verilator lint_off LITENDIAN*/  /* verilator lint_off INITIALDLY*/  

//Your Verilog/System Verilog Code Starts Here:
module prior(d_out, d_in);

   output [2:0] d_out;
   input [7:0] d_in ;

assign d_out = (d_in[7] ==1'b1 ) ? 3'b111:
               (d_in[6] ==1'b1 ) ? 3'b110:
               (d_in[5] ==1'b1 ) ? 3'b101:
               (d_in[4] ==1'b1) ? 3'b100:
               (d_in[3] ==1'b1) ? 3'b011:
               (d_in[2] ==1'b1) ? 3'b010:
               (d_in[1] ==1'b1) ? 3'b001:
               (d_in[0] ==1'b1) ? 3'b000: 3'bxxx;

endmodule


//Top Module Code Starts here:
	module top(input logic clk, input logic reset, input logic [31:0] cyc_cnt, output logic passed, output logic failed);
		logic  [2:0] d_out;//output
		logic  [7:0] d_in;//input
//The $random() can be replaced if user wants to assign values
		assign d_in = $random();
		prior prior(.d_out(d_out), .d_in(d_in));
	
\TLV
//Add \TLV here if desired                                     
\SV
endmodule

```
![mk_Picture1](https://user-images.githubusercontent.com/89923461/157566824-a685a9ed-c547-4493-9335-c768f9c2d5ca.png)

![mk2_Picture1](https://user-images.githubusercontent.com/89923461/157566820-8fb86fa1-5e14-4167-8750-9f49fb97fb18.png)

After debugging some errror in the code via the makerchip IDE, we can use the Verilog to Ngspice converter in the Ngveri tab in the simulator and create a successful model.

![ngveri_Picture1](https://user-images.githubusercontent.com/89923461/157567322-37cc172c-6886-4d01-b4b9-1468a5417804.png)

# Schematics

Using eSim's schematic editor software KiCad, we can design the ADC circuit. The Analog part of this design consists of the compartors and the resistor ladder circuit. The digital part of the circuit is priority encoder, which can be found in the components list once created a model.

![sch_Picture1](https://user-images.githubusercontent.com/89923461/157567646-220d6f87-4d49-40a4-bf6a-9a3933f11cd8.png)

We use the adc and dac bridges to facilate the functioning of priority encoder ( or any other digital circuit) for understanding the inputs. 

# Waveform

After creating the schematics, we can set the source voltage's parameters and add the sub circuits used in the schematics. And click KiCad to ngspice converter. After conversion, click the simulation button for simulating the circuit.

![wave_wv_Picture1](https://user-images.githubusercontent.com/89923461/157568158-312aab51-e15f-48ab-9e53-8f19ff875242.png)

From the wave form we can see when the voltage are higher than that of the 7Vref/8 voltages it converts it to the bits 111 and when the voltage drop to zero it comes down to the bits 000.

# Netlist

```
* /home/ramachandra14519/esim-workspace/adc/adc.cir

.include lm_741.sub
* u2  net-_u2-pad1_ net-_u2-pad2_ net-_u2-pad3_ net-_u2-pad4_ net-_u2-pad5_ net-_u2-pad6_ net-_u2-pad7_ net-_u2-pad8_ net-_u2-pad9_ net-_u2-pad10_ net-_u2-pad11_ prior
* u3  net-_u3-pad1_ net-_u3-pad2_ net-_u3-pad3_ net-_u3-pad4_ net-_u3-pad5_ net-_u3-pad6_ net-_u3-pad7_ gnd net-_u2-pad1_ net-_u2-pad2_ net-_u2-pad3_ net-_u2-pad4_ net-_u2-pad5_ net-_u2-pad6_ net-_u2-pad7_ net-_u2-pad8_ adc_bridge_8
* u4  net-_u2-pad9_ net-_u2-pad10_ net-_u2-pad11_ b2 b1 b0 dac_bridge_3
r4  net-_r3-pad2_ net-_r4-pad2_ 1k
r5  net-_r4-pad2_ net-_r5-pad2_ 1k
r3  net-_r2-pad2_ net-_r3-pad2_ 1k
r2  +8v net-_r2-pad2_ 1k
r6  net-_r5-pad2_ net-_r6-pad2_ 1k
r7  net-_r6-pad2_ net-_r7-pad2_ 1k
r8  net-_r7-pad2_ net-_r8-pad2_ 1k
x2 ? net-_r3-pad2_ in -5v ? net-_u3-pad2_ +5v ? lm_741
x3 ? net-_r4-pad2_ in -5v ? net-_u3-pad3_ +5v ? lm_741
x4 ? net-_r5-pad2_ in -5v ? net-_u3-pad4_ +5v ? lm_741
x5 ? net-_r6-pad2_ in -5v ? net-_u3-pad5_ +5v ? lm_741
x7 ? net-_r8-pad2_ in -5v ? net-_u3-pad7_ +5v ? lm_741
r9  net-_r8-pad2_ gnd 1k
x6 ? net-_r7-pad2_ in -5v ? net-_u3-pad6_ +5v ? lm_741
v1  in gnd sine(3 0 0 0 0)
* u1  in plot_v1
* u7  b2 plot_v1
* u6  b1 plot_v1
* u5  b0 plot_v1
x1 ? net-_r2-pad2_ in -5v ? net-_u3-pad1_ +5v ? lm_741
a1 [net-_u2-pad1_ net-_u2-pad2_ net-_u2-pad3_ net-_u2-pad4_ net-_u2-pad5_ net-_u2-pad6_ net-_u2-pad7_ net-_u2-pad8_ ] [net-_u2-pad9_ net-_u2-pad10_ net-_u2-pad11_ ] u2
a2 [net-_u3-pad1_ net-_u3-pad2_ net-_u3-pad3_ net-_u3-pad4_ net-_u3-pad5_ net-_u3-pad6_ net-_u3-pad7_ gnd ] [net-_u2-pad1_ net-_u2-pad2_ net-_u2-pad3_ net-_u2-pad4_ net-_u2-pad5_ net-_u2-pad6_ net-_u2-pad7_ net-_u2-pad8_ ] u3
a3 [net-_u2-pad9_ net-_u2-pad10_ net-_u2-pad11_ ] [b2 b1 b0 ] u4
* Schematic Name:                             prior, NgSpice Name: prior
.model u2 prior(rise_delay=1.0e-9 fall_delay=1.0e-9 input_load=1.0e-12 instance_id=1 ) 
* Schematic Name:                             adc_bridge_8, NgSpice Name: adc_bridge
.model u3 adc_bridge(in_low=1.0 in_high=2.0 rise_delay=1.0e-9 fall_delay=1.0e-9 ) 
* Schematic Name:                             dac_bridge_3, NgSpice Name: dac_bridge
.model u4 dac_bridge(out_low=0.0 out_high=5.0 out_undef=0.5 input_load=1.0e-12 t_rise=1.0e-9 t_fall=1.0e-9 ) 
.tran 1e-00 5e-00 0e-00

* Control Statements 
.control
run
print allv > plot_data_v.txt
print alli > plot_data_i.txt
plot v(in)
plot v(b2)
plot v(b1)
plot v(b0)
.endc
.end

```

# Author

Ramachandra T, BE. ECE, Madras Institute of Technology, Anna University

# Acknowledgements

- Kunal Ghosh, VSD Corp
- Sumanto Kar, IIT-B
- Steve Hoover, Redwood EDA
- FOSSEE, IIT-Bombay

# References

1. J. Nidagundi, S. Bettakusugal, “Design and Implementation of 3-bit Flash Analog to Digital Converter (ADC),” International Journal of Latest Trends in Engineering and Technology, vol. 10, no. 3, pp.208-214

2. S. Franco, Design with Operational Amplifiers and Analog Integrated Circuits. New York: McGraw-Hill Education, 2015











