# TMC4671-LearningNote
***
## Prewritten
  The purpose of this project is to record my learning steppes of TMC4671 in case I forgot one day. If this project gives someone with the same confusion on that chip some little help, I will be happy.
***
## What is TMC4671 and what can it do?
  TMC4671 is a fully `integrated servo controller` that provides Field Oriented Control for BLDC/PMSM and 2-phase Stepper Motors as well as DC motors and voice coils. That is the Official introduction of the datasheet.  
  It can drive all motors under this line. In this project, I am going to learn how to drive `PMSM` with TMC4671.
|Motor|Picture|Motor|Picture|
|----|----|----|----
|BLDC|<img src="https://github.com/WalterWFeng/TMC4671-LearningNote/blob/main/img/BLDC.png" width="200" />|PMSM|<img src="https://github.com/WalterWFeng/TMC4671-LearningNote/blob/main/img/PMSM.png" width="200" />
|Stepper Motor|<img src="https://github.com/WalterWFeng/TMC4671-LearningNote/blob/main/img/Stepper.jpg" width="200" />|DC Motor|<img src="https://github.com/WalterWFeng/TMC4671-LearningNote/blob/main/img/DC.png" width="200" />
|Voice coils|<img src="https://github.com/WalterWFeng/TMC4671-LearningNote/blob/main/img/Voice.jpg" width="200" />
***
## Hardware Structure
As we can see, we can control TMC4671 with SPI interface or USART through STM32 or other MicroChip.We can write some specific value into a register of the chip to implement specific functions. Such as we can Select Motor Type or something. When we have set up the chip, the chip will automatically output a signal to the motor driver which is composed of Gate Driver and MOSFEt.Then, the motor will turn. At last, sensors will collect motor data and trans back to TMC4671, such as current and rotor position.TMC4671 will process data and adjust the output signal automatically to control the motor. We can find the Simplified Block Diagram in the chip datasheet which I have posted down there.  
<img src="https://github.com/WalterWFeng/TMC4671-LearningNote/blob/main/img/Hardware1.png" width="700" />  
<img src="https://github.com/WalterWFeng/TMC4671-LearningNote/blob/main/img/Hardware2.png" width="700" />
## Communication Interfaces (SPI)
I have used the SPI communication interface to communicate with TMC4671 successfully. And Here are my steps.  
### Step 1 - Set up a project through STM32 CubeIDE.
It is easy to find a tutorial on the internet. like this https://www.youtube.com/watch?v=szMGedsp9jc.
### Step 2 - Instruct a SPI in STM32.
|Mode|Full-Duplex Master
|---|---
|Configuration|
|Data Size|8 Bit
|Frist Bit|MSB Frist
|Prescale|16
|Baud Rate|1000.0 KBits/s
|CPOL|High
|CPHA|2 Edge
Note:  
  The SPI of the TMC4671 for the user application has an easy command and control structure. The TMC4671
user SPI acts as a subnode. The SPI datagram length is 40 bit with a clock rate up to 8 MHz (1 MHz for the
TMC4671-ES).  
• The MSB (bit#39) is sent first. The LSB (bit#0) is sent last.
• The MSB (bit#39) is the WRITE_notREAD (WRnRD) bit.
• The bits (bit#39 to bit#32) are the address bits (ADDR).
• Bits (bit#31) to (bit#0) are 32 data bits.  
  The SPI of the TMC4671 immediately responds within the actual SPI datagram on read and write for ease of use communication and uses SPI mode 3 with CPOL = 1 and CPHA = 1. There is no support for daisy chain multiple ICs using MISO and MOSI. Datagrams longer or shorter than 40-bit should be avoided and might lead to unexpected behavior.
### Step 3 - Edite Code.
