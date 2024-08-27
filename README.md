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
As we can see, we can control TMC4671 with SPI interface or USART through STM32 or other MicroChip.We can write some specific value into a register of the chip to implement specific functions. Such as we can Select Motor Type or something. When we have set up the chip, the chip will automatically output a signal to the motor driver which is composed of Gate Driver and MOSFEt.Then, the motor will turn. At last, sensors will collect motor data and trans back to TMC4671, such as current and rotor position.TMC4671 will process data and adjust the output signal automatically to control the motor. 
<img src="https://github.com/WalterWFeng/TMC4671-LearningNote/blob/main/img/Hardware1.png" width="700" />  
<img src="https://github.com/WalterWFeng/TMC4671-LearningNote/blob/main/img/Hardware2.png" width="700" />
