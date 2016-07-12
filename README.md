
## Summary

This project is an SOC (System on a Chip) coded in VHDL and implemented for the Lattice iCE40-hx8k dev board. The SOC contains the following components: 6805 CPU + UART + Timer + I/O Ports

## Required Hardware

* Lattice iCE40-hx8k dev board (can be ordered online at www.latticesemi.com)
* USB-to-Serial 3.3V adapter (can be ordered from eBay)
* misc USB cables and wires for connecting the USB-to-Serial adapter

NOTE: Make sure the USB-to-serial adapter is a 3.3V version. Some adapters have 5V interface signals which could damage your iCE40-hx8k dev board.

## Tools

* IceCube2 (from Lattice Semiconductor) was used for synthesis and FPGA Routing.
* Icestorm (https:/github.com/cliffordwolf/icestorm) was used for programming.


## Build Flow

I used the Lattice IceCube2 software to generate the SOC_bitmap.bin programming file and then I used this command line "iceprog SOC_bitmap.bin" the program the iCE40-hx8k dev board over the USB cable (iceprog is part of the icestorm tool suite).

## Console Interface

I used the minicom program (on Ubuntu Linux) as a console to communicate with the 6805 SOC over the USB-to-Serial connection. Configure minicom using the command line "minicom -s" to configure the serial port for ttyUSB0 and turn of the hardware handshaking. There are probably other alternatives to minicom. Any ANSI terminal-emulator program should work for this application.

## Pinout

The iCE40 pins are defined as follows:
```
UART_RXD   G1 -pullup yes
UART_TXD   G2
PORTA[0]   B5
PORTA[1]   B4
PORTA[2]   A2
PORTA[3]   A1
PORTA[4]   C5
PORTA[5]   C4
PORTA[6]   B3
PORTA[7]   C3
RESET      N3 -pullup yes
CLK        J3 -pullup yes
```

## 6805 CPU Background Info

The 6805 is an eight-bit microprocessor introduced by Motorola in the early 1980's. The 6805 was intended for low cost embedded application and it had on-chip RAM, ROM, I/O ports and a timer. Its instruction-set architecture is influenced by the earlier Motorola 6800 processor, but it is not at all code-compatible. The 6805 is missing some 6800 instructions  but is has additional bit-oriented instructions as well as additional addressing modes. The 6805 has only one accumulator (A) vs. the two accumulators of the 6800 and the index register (X) is only 8-bits vs. 16-bits for the 6800. Like the 6800, the 6805 has a 16-bit stack pointer (SP) but unlike the 6800, the memory location of the beginning stack is fixed, and  the 6805 has no push or pull opcodes. The stack is used only implicitly by the JSR instruction and by hardware interrupts.


## Contributors

* Scott L Baker - SOC design

## License

See the **LICENSE** file in this repository
