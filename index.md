# Driving a Continuous Rotation Servo with PCA9685 16-Channel PWM Driver using Raspberry Pi

## Table of Contents
1. [Useful Links](#Useful-Links)  
2. [Proof of Purchase](#proof-of-purchase)  
3. [Header Soldered](#soldered-the-header)  
4. [I2C Wiring](#i2c-to-rpi-wiring)  
5. [I2C Detected](#i2c-connected-to-the-rpi)  
6. [Changing the PCA9685 Address](#changing-pca9685-address)
7. [PCB Design](#pcb-design)  
8. [Schematic Diagram](#schematic-diagram)  
9. [Video of Working Servomotor](#video)

### Useful Links
[CENG 320 Page](https://six0four.github.io/ceng317/)  [GitHubpage](https://biodunduke.github.io/ServoMotorDriver/)   
[Week 1](https://six0four.github.io/ceng317/wk01.html) | [Week 2](https://six0four.github.io/ceng317/wk02.html) | [Week 3](https://six0four.github.io/ceng317/wk03.html)  
[Week 4](https://six0four.github.io/ceng317/wk04.html) | [Week 5](https://six0four.github.io/ceng317/wk05.html) | [Week 6](https://six0four.github.io/ceng317/wk06.html)  
[Week 7](https://six0four.github.io/ceng317/wk07.html) | [Week 8](https://six0four.github.io/ceng317/wk08.html) | [Week 9](https://six0four.github.io/ceng317/wk09.html)  
[Week 10](https://six0four.github.io/ceng317/wk10.html) | [Week 11](https://six0four.github.io/ceng317/wk11.html) | [Week 12](https://six0four.github.io/ceng317/wk12.html)  
[Week 13](https://six0four.github.io/ceng317/wk13.html) | [Week 14](https://six0four.github.io/ceng317/wk14.html) | [Week 15](https://six0four.github.io/ceng317/wk15.html)  

## Week 12 - Nov. 20, 2018  
### Due today:  
[Enclosure](#Enclosure-Design)  
The enclosure was designed in Corel Draw which is not free for use. The college, however, have it installed in the lab for student use. Accurate measurement has to be made and the design file modified accordingly to fit the Raspberry and the Broadcom Development platform. The design can be downloaded [here](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/documentation/pi3case.cdr) for modification.  
#### Assembled Enclosure:  
![Enclosure](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/enclosure.jpeg) 
#### Enclosure Design
![Enclosure](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/pi3case.jpg)
## Week 11 - Nov. 13, 2018  
### Due today:  
Powerup
### Progress Report:  
The project is on track according to the [project timeline](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/documentation/projecttimeline.pdf), I was able to achieve power up since last [week](#week-10). No additional cost incurred since the last purchase.   
I demonstrated the power up to the professor in class. Video is posted [here](#video).  
  
## Week 10 - Nov. 6, 2018  
### Due today:  
PCB soldered
### Progress Report:  
The project is on track according to the [project timeline](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/documentation/projecttimeline.pdf). I made additional expenses to buy [pin and stackable headers at Creatron](https://www.creatroninc.com/product/stackable-header-for-raspberry-pi/) which made the [project's budget](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/documentation/projectestimate.pdf) to be a little over the budget by __$9.29__ plus time and mileage.  
So far, I have been able to connect my PCB to the Raspberry Pi and the servomotor controlled successfully.  
### Video   

<iframe width="896" height="504" src="https://www.youtube.com/embed/oR9lkV447pY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  

  
## Week 9  
### Status Update  
Additional parts [Pin Headers](#pin-headers) have been purchased so the project is a little over the budget by __$9.29__.  
The project is on track according to the [project timeline](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/documentation/projecttimeline.pdf).  
### PCB Design  
I used the free software Fritzing to make the Schematic Diagram and the PCB design as shown in the images below.  
After the design, the fritzing file was exported as an extended grubber file and emailed to the Humber Prototype Lab in order to manufacture the PCB.   
### Pin Headers  
Pin headers are required for connecting the I2C (PCA9685) to the PCB and also to stack the PCB to the Raspberry Pi.  
The following pin headers were purchased:  
* 6Pin Stackable(CONHD-330060) - This will be soldered to the PCB and the PCA9685 will be mounted on it.  
* 40pin header (CONPH-100400) - This is breakable to required number of pin headers. I broke out 2 X 6 pins, to solder to the PCA9685 to serve as connection and support for the PCA9685 on the PCB.  
* Extra stackable 2 x 20p (CONPH-402749) - This will be soldered to the PCB to extend the Raspberry Pi3 40 pins out of the PCB.
![Pin Headers](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/headerpins.jpeg)
#### PCB Design
![PCB Design](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/servomotor_pcb.png)  
#### Schematic Diagram  
![Schematic Diagram for One Servo Motor](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/servomotor_schem.png)  

## Week 8  
### Changing PCA9685 Address
For this project, I have been assigned address 0x75. The PCA9685 default address is 0x40. Below are the steps in changing the address.  
![Image of PCA9685 Address Modification](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/addressbits.jpeg) 
There are six address bits (labeled A0 to A5, A0 being the least significant bit (LSB)) on the board that are turned off by default. The addressing starts at 0x40 (Hexadecimal) which in Binary is 0100 0000. To get 0x75 as the address, the address bits will have to be turned on by soldering a piece of solder to bridge the plates, hence turning on the bits.  
0x75 in Binary is 0111 0101. To achieve this, I put solder on A0, A2, A4, and A5.  
Below is the screenshot showing the new address.  
![Screenshot after address change](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/addresschanged.png)  
### I2C To RPi Wiring  
![Image of PCA9685 To RPi Wiring](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/i2c-rpi-wiring.jpeg)  
### Wiring  

The I2C Device PCA9685 can drive up to 16 Sevo Motors since it has 16 channels. In the above connection, I only used one continuous rotation servo motor for testing purpose (to show that the RPi can detect the I2C and run the motor using the Python code posted below. The RPi pinouts can be found [RPi Pinouts](https://pinout.xyz/pinout/i2c).  
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

### I2C Connected to the RPi  
![Image of I2C Connected](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/i2c-to-rpi.jpeg)  
![Screenshot of I2C Detected](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/i2cdetected.PNG)  

## Week 7
### Soldered the Header 
![Image of Soldering](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/soldering.jpeg)  
![Image of Soldering2](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/backsolder.jpeg)  
![Image of Soldering3](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/solderedheader.jpeg)  

## Week 6
### Proof of Purchase  
![Image of Parts](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/purchaseproof.jpeg)  
