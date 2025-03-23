# Benchtop HEPA Filter with variable speed fan control using an ESP32

Inspired by https://github.com/opennukit/Nukit-Open-Air-Purifier

![Finished Filter Assembly](https://github.com/ssosik/Benchtop-HEPA-Filter/blob/main/images/20250316_174557.jpg)

[Box Parameters I used][link0]

## Materials I used:
- HPA300 HEPA Air Filters (165mm X 261mm X 41mm)
- 12"x12"x1/8" balsa sheets
- An ESP32
- DC - DC Buck converter (step 12v down to 5v)
- 4-pin PC PWM Fan connectors (female)
- 2x Arctic P14 PWM 140mm case fans
- On/Off Rocker Switch
- 5.5mm x 2.1mm female barrel jack
- B10k rotary potentiometer
- 1 Red LED + 220Ω resistor
- Hookup wire
- A 12V voltage source (or 5V for 5V fans)

I'm very fortunate to have access to a great local library system with a well-funded makerspace, including a GlowForge laser cutter. I used that to cut out the balsa wood sheets into the box sides.

I used https://github.com/FAB1150/ESP32_fan_control as a good starting point for doing PWM fan control.

#### notes:
* [Check the pinout of your ESP32][link4] to avoid headaches! Not all boards are the same!
* If you want to put everything on a breadboard, the ESP32s without silkscreen legends are thinner
* If you use 12V fans, the voltage regulators linked above are configurable. Get a thin blade and some solder
* If you use small 5V fans you don't need to step down the voltage and can just use a 5V supply for everything

## Getting Started
  * download pwm_fan_control.ino from its folder and open it with the arduino IDE
  * Wire everything up
  * set up the code and flash it to the ESP32
  * if you don't know how to flash to the ESP32 from Arduino IDE, follow [this tutorial][link6] to get started
  * you're done!

## Wiring
Wiring everything up should be pretty straightforward. Make sure to [check the pinout of your board][link4].

Follow this image for reference:

  ![Breadboard](https://github.com/ssosik/Benchtop-HEPA-Filter/blob/main/esp32-circuit_bb.png)

  * Be careful with connecting the fan wires correctly! the PWM signal wire is NOT next to the power wires, but the one on the other side of the connector! be careful or you will fry your esp32!

## Set up the code
We're almost done! Now you need to set up the code.

This README guides you through the basic settings, they'll easily get you up and running. It skips some of the settings you don't need to edit for it to work correctly, but they're all described in the code and pretty straight forward!

#### It is well documented, but make sure to follow this readme at least for the thermistor calibration!

  * After downloading it, open pwm_fan_control.ino with the Arduino IDE
  * If you have never used an ESP32 with the Arduino IDE yet, follow [this tutorial][link6] to get started. Now that you see the esp32 code correctly, we can go on editing our settings.
  * define the correct pins by editing these two variables, if you used the same pins as me you don't have to modify this
``` c++
//setting the I/O pins
//the fan PWM output pin
const int fanOutput = 33;
//rotary potentiometer pin
const int rotPot = 32;
// power led pin
const int ledPin = 18;
```

### Opening the serial monitor
For the next two steps we're gonna need to see the values that the ESP is reading. We'll be able to by using the serial monitor of the Arduino IDE

  * In the code, uncomment DEBUG to enable it, in line 4
    ``` c++
    #define DEBUG
    ```
  * Now flash the code to the ESP32. This also lets you know if you made any mistakes in the fan curve configuration!
  * With the ESP32 still connected, in the IDE go to tools > Serial Monitor. Select Baud 115200 and you'll see a flow of numbers!

    ![serial monitor][img7]

## License
[GNU GPLv3.0](https://choosealicense.com/licenses/gpl-3.0/)

[link0]: https://d3t2bqcgejmujs.cloudfront.net/AirPurifier?FingerJoint_angle=90.0&FingerJoint_style=rectangular&FingerJoint_surroundingspaces=2.0&FingerJoint_bottom_lip=0.0&FingerJoint_edge_width=1.0&FingerJoint_extra_length=0.0&FingerJoint_finger=2.0&FingerJoint_play=0.0&FingerJoint_space=2.0&FingerJoint_width=1.0&DoveTail_angle=50&DoveTail_depth=1.0&DoveTail_radius=0.2&DoveTail_size=2&x=165&y=261&filter_height=41&rim=20&fan_diameter=140.0&filters=1&split_frames=0&fans_left=-1&fans_right=-1&fans_top=0&fans_bottom=0&screw_holes=5.0&thickness=4&format=svg&tabs=0.0&qr_code=0&qr_code=1&debug=0&labels=0&labels=1&reference=100&inner_corners=backarc&burn=0.1&language=None&render=0
[link4]: https://www.upesy.com/blogs/tutorials/esp32-pinout-reference-gpio-pins-ultimate-guide
[link6]: https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/

[img7]: https://github.com/FAB1150/ESP32_fan_control/blob/main/images/serial%20monitor.jpg?raw=true
