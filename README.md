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

##### Get your RPi ready  
On your Raspberry Pi, open a terminal and enter the following:  

    sudo apt-get install python-smbus  
    sudo apt-get install i2c-tools   
    sudo apt-get install git build-essential python-dev   
    cd ~  
    git clone https://github.com/adafruit/Adafruit_Python_PCA9685.git  
    cd Adafruit_Python_PCA9685  
    sudo python setup.py install  
# if you have python3 installed:
    sudo python3 setup.py install 
    
##### Connecting to the Raspberry Pi  
The RPi pinouts can be found [RPi Pinouts](https://pinout.xyz/pinout/i2c).  
Because of the RPi fluctuating voltage levels, it is advised to power the servo motor by a separate +5V source (there is provision for the connection on the I2C). The I2C (PCA9685) itself is powered from the the 3.3V output of the RPi.  
I connected I2C's VCC and GND to pins 1 and 6 respectively on the RPi. The Serial Clock (SCL) and Serial Data (SDA) were connected to pins 5 (BCM 3 - Clock) and 3 (BCM 2 - Data) of the RPi respectively. I connected one servo motor to channel 15 of the PCA9685 (Orange side to the PWM, Red to the V+, and Brown to GND). I made some modifications to the sample code provided by [Adafruit](https://github.com/adafruit/Adafruit_Python_PCA9685/blob/master/examples/simpletest.py)  

### Sample Code  
    # Simple demo of of the PCA9685 PWM servo/LED controller library.
    # This will move channel 15 from min to max position repeatedly.
    # Author: Tony DiCola
    # Edited by Abiodun Ojo
    # License: Public Domain
    from __future__ import division
    import time

    # Import the PCA9685 module.
    import Adafruit_PCA9685


    # Uncomment to enable debug output.
    #import logging
    #logging.basicConfig(level=logging.DEBUG)

    # Initialise the PCA9685 using the default address (0x40).
    pwm = Adafruit_PCA9685.PCA9685()
    #pwm = Adafruit_PCA9685.PCA9685(address=0x75) was what I used eventually after I changed my address
    # Alternatively specify a different address and/or bus:
    #pwm = Adafruit_PCA9685.PCA9685(address=0x41, busnum=2)
    # Configure min and max servo pulse lengths
    servo_min = 150  # Min pulse length out of 4096
    servo_max = 600  # Max pulse length out of 4096

    # Helper function to make setting a servo pulse width simpler.
    def set_servo_pulse(channel, pulse):
    pulse_length = 1000000    # 1,000,000 us per second
    pulse_length //= 60       # 60 Hz
    print('{0}us per period'.format(pulse_length))
    pulse_length //= 4096     # 12 bits of resolution
    print('{0}us per bit'.format(pulse_length))
    pulse *= 1000
    pulse //= pulse_length
    pwm.set_pwm(15, 0, pulse)

    # Set frequency to 60hz, good for servos.
    pwm.set_pwm_freq(60)

    print('Moving servo on channel 15, press Ctrl-C to quit...')
    while True:
    # Move servo on channel 15 between extremes.
    # pwm.set_pwm(15, 0, servo_min)
    #   time.sleep(1)
    #    	pwm.set_pwm(15, 0, servo_max)
    #    	time.sleep(1)

	pwm.set_pwm(15, 0, 10) # Rotate
    	time.sleep(1) #Sleep
	pwm.set_pwm(15, 0, 0)  #Do not rotate
	time.sleep(1)

##### I2C Connected to the RPi  
![Image of I2C Connected](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/i2c-to-rpi.jpeg)  
After connecting do below to detect the PCA9685  

    sudo i2cdetect -y 1  //To detect the address of the PCA9685 (default address is 0x40)
    
![Screenshot of I2C Detected](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/i2cdetected.PNG)  

To change the address, follow the instruction below:  
Below are the steps in changing the address.  
There are six address bits (labeled A0 to A5, A0 being the least significant bit (LSB)) on the board that are turned off by default. The addressing starts at 0x40 (Hexadecimal) which in Binary is 0100 0000. To get 0x75 (which is my address for this project) as the address, the address bits will have to be turned on by soldering a piece of solder to bridge the plates, hence turning on the bits.  
0x75 in Binary is 0111 0101. To achieve this, I put solder on A0, A2, A4, and A5.  
Below is the screenshot showing the new address.  
![Screenshot after address change](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/addresschanged.png)  

### PCB / Soldering  
I used the free software Fritzing to make the Schematic Diagram and the PCB design as shown in the images below.  
After the design, the fritzing file was exported as an extended grubber file and emailed to the Humber Prototype Lab in order to manufacture the PCB.  
![PCB Design](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/servomotor_pcb.png)  

### Power Up  


### Unit Testing  


### Production Testing  
