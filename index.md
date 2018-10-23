# Driving a Continuous Rotation Servo with PCA9685 16-Channel PWM Driver using Raspberry Pi

## Table of Contents
1. [Useful Links](#Useful-Links)  
2. [Proof of Purchase](#proof-of-purchase)  
3. [Header Soldered](#soldered-the-header)  
4. [I2C Wiring](#i2c-to-rpi-wiring)  
5. [I2C Detected](#i2c-connected-to-the-rpi)  

### Useful Links
[CENG 320 Page](https://six0four.github.io/ceng317/)  
[Week 1](https://six0four.github.io/ceng317/wk01.html)  
[Week 2](https://six0four.github.io/ceng317/wk02.html)  
[Week 3](https://six0four.github.io/ceng317/wk03.html)  
[Week 4](https://six0four.github.io/ceng317/wk04.html)  
[Week 5](https://six0four.github.io/ceng317/wk05.html)  
[Week 6](https://six0four.github.io/ceng317/wk06.html)  
[Week 7](https://six0four.github.io/ceng317/wk07.html)  
[Week 8](https://six0four.github.io/ceng317/wk08.html)  
[Week 9](https://six0four.github.io/ceng317/wk09.html)  
[Week 10](https://six0four.github.io/ceng317/wk10.html)  

## Week 8
### I2C To RPi Wiring  
![Image of I2C To RPi Wiring](https://raw.githubusercontent.com/biodunduke/ServoMotorDriver/master/images/i2c-rpi-wiring.jpeg)  
### Wiring

The I2C Device PCA9685 can drive up to 16 Sevo Motors since it has 16 channels. In the above connection, I only used one continuous rotation servo motor for testing purpose (to show that the RPi can detect the I2C and run the motor using the Python code posted below. The RPi pinouts can be found [RPi Pinouts](https://pinout.xyz/pinout/i2c).  
Because of the RPi fluctuating voltage levels, it is advised to power the servo motor by a separate +5V source (there is provision for the connection on the I2C). The I2C (PCA9685) itself is powered from the the 3.3V output of the RPi.  
I connected I2C's VCC and GND to pins 1 and 6 respectively on the RPi. The Serial Clock (SCL) and Serial Data (SDA) were connected to pins 5 (BCM 3 - Clock) and 3 (BCM 2 - Data) of the RPi respectively. I connected one servo motor to channel 15 of the PCA9685 (Orange side to the PWM, Red to the V+, and Brown to GND). I made somme modifications to the sample code provided by [Adafruit](https://github.com/adafruit/Adafruit_Python_PCA9685/blob/master/examples/simpletest.py)  

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
