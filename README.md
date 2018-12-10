# ServoMotorDriver  
## Links
1. [Introduction](#introduction)  
2. [Bills of Materials](#bills-of-materials)  
3. [Time Commitment](#time-commitment)  
4. [Mechanical Assembly](#mechanical-assembly)  
5. [PCB/Soldering](#pcb-soldering)  
6. [Power Up](#power-up)  
7. [Unit Testing](#unit-testing)  
8. [Production Testing](#production-testing)  

![System Diagram](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/systemdiag.png)


### Introduction  
For moving objects, it is imperative that they have parts that aid in the movement. Motors are mostly used in the movement of objects. This project focuses on powering a servo motor using Raspberry Pi.
#### Limitation:   
The Raspberry Pi only has one PWM (Pulse Width Modulation) channel on its GPIO. To overcome this limitation, I used the Adafruit's 16-channel 12-bit PWM/Servo driver (PCA9685). The PCA9685 connects to the Raspberry Pi with two pins on the Pi's I2C channel. It can drive up to 16 PWM simultaneously with adding extra overhead processing to the Pi. One can chain up to 62 PCA9685 together to drive a total of 992 servo motors, very cool!   

### Bills of Materials  
The materials withtheir costs used for the project is as shown below:  ![](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/budget.PNG):  

### Time Commitment  
The project was done over the course of the semester (15 weeks) but can be reproduced with a week if all the parts listed above have been purchased. Below is my timeline:  
![](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/timeline.jpg)  
To get ahead and also cope with the course loads of other courses, I ensured that I did most of the task way before due dates.  

### Mechanical Assembly  
#### PCA9685 Pinouts  
![](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/pinouts.jpg)  

##### Power Pins   
**GND** - This is the power and signal ground pin, must be connected.  
**VCC** - This is the logic power pin, connect this to the logic level you want to use for the PCA9685 output, should be 3 - 5V max! It's also used for the 10K pullups on SCL/SDA so unless you have your own pullups, have it match the microcontroller's logic level too!  
**V+** - This is an optional power pin that will supply distributed power to the servos. This is not used in this project. Instead, an extra 5VDC is used to power the servo.  
##### Control Pins  
**SCL** - I2C clock pin, connect to your microcontrollers I2C clock line. Can use 3V or 5V logic, and has a weak pullup to VCC  
**SDA** - I2C data pin, connect to your microcontrollers I2C data line. Can use 3V or 5V logic, and has a weak pullup to VCC  

##### Assembly  
The PCA9685 comes with the control headers and 4 3X4 pin male headers. Solder them neatly as shown below:  
![Image of Soldering3](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/pca9685soldered.jpg)  

### PCB / Soldering  


### Power Up  


### Unit Testing  


### Production Testing  
