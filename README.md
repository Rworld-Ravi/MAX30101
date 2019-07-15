# **MAX30101 Photoplethymography (PPG) Sensor**
Driver Library for Arduino and Simplelink Microcontrollers

## The MAX30101 PPG Sensor
The MAX30101 sensor is produced by Maxim Integrated and is designed in biomedical applications for the detection of heart rate and blood oxygen saturation (SpO2).

The sensor consists of three light emitting diodes (LEDs) emitting in the red (660nm), infrared (IR) (880nm) and green (537nm) parts of the electromagnetic spectrum. The sensor contains a single photodiode for detection of light emitted from the LEDs, or ambient light. This PPG sensor along with it's bi-wavelength companion sensor, the MAX30102, are the only PPG sensors with integrated analogue to digital converter (ADC) and I2C interface inside the sensor iteself. These features make the MAX30101 and MAX30102 sensors the smallest fully integrated PPG sensors on the market at about the size of a grain of rice.

## Using the MAX30101ACCEVKIT with an External Microcontroller
The development board for the MAX30101 is the MAX30101ACCEVKIT. This development kit contains a small board containing the MAX30101 sensor, included on this board is a 3-axis accelerometer, the LIS2DH. The kit includes a seperate board containing power regulators which step down USB voltage from 5v, to 4.4v, 3.3v and 1.8v required of the sensor board. The 4.4v is wired to the MAX30101 LEDs, the 1.8v is wired to the VDD of the MAX30101, while the 3.3v is wired to the VDD of the accelerometer. Additionally this board contains a microprocessor with custom firmware for intergration with the MAX30101ACCEVKIT software supplied by Maxim Integrated for testing from a Windows computer. Unlike the MAX30102, Maxim Integrated has not supplied demo code for the MAX30101 for Arduino or similar microprocessors, nor is the board included in the MAX30101ACCEVKIT immediately friendly for use with alternative microprocessors.

However, the included daugher board to the sensor board in the MAX30101ACCEVKIT can be made to work with an external microcontroller. In order to make this board work, you need to make a jumper to short the reset pin (pin 1) on J2 to ground (pin 3) on J2 (**Figure 1**). This will hold the onboard microcontroller in reset, allowing an external board to communicate via I2C with the sensors.

**INSERT FIGURE HERE WITH RESET PIN SHORTING**

Additionally, pins need to be added to the daugher board at SDA, SCL, INT1 (if desired), INT2 (if desired) GND and VBUS (5V in, if desired) (**Figure 2**). The SDA and SCL pins need to be connected to the SDA and SCL pins respectively on your microcontroller. Connect GND to the ground on your microcontroller (important, as both must have a common ground). If you want to power the daughter board from your microcontroller, connect the 5V or USB Power pin to the VBUS pin on the daughter board to supply 5V power. If you choose, you can omit the VBUS pin, however you must then power the daugher borad seperatly from your microcontroller, such as through a seperate USB power supply. This is stepped down on the daughter board to the voltages required of the sensor board as mentioned above. If desired the INT1 can be connected to a pin on your microcontroller for physical interrrupt for the MAX30101 sensor, however it is not necessary, nor is it used in this implementation of the driver. Additionally INT2 can be wired to your microcontroller for the acceleromoter physical interrupt. Please see the LIS2DH library for information on INT2.

**INSERT FIGURE HERE WITH SDA, SCL, VBUS, INT1 AND INT2 PIN LOCATIONS**

# Common Library Functions

The following are common to both the Arduino and Simplelink libraries

## The Initialiser
In the MAX30101 library a class named *Initialiser* is used to define the initialisation options for the MAX30101 sensor. The following sections describe how to create an * *Initialiser* * object, and the options available for initialisation of the MAX30101 sensor.

### Create an Initialiser Object
An *Initialiser* object is required in order to set the initialisation options of the MAX30101 sensor. This object is then passed into the Initialise function of the library configuring the MAX30101 sensor for use. To create an *Initialiser* function use the following syntax.
```
MAX30101::Initialiser *ObjectName*;
```
For example:
```
MAX30101::Initialiser initOptions;
```

