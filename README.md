# Lab 5: Useless Box

*A lab report by Chris Brownell*

## 3D Printing

**a. Include a photo of your printed part here.**

We used the 3D printer to create the blue servo mount in the picture below:
![servomount](https://github.com/chrisbrownell/IDD-Fa18-Lab5-ckb77/blob/master/IMG_5706.JPG)

**b. Include `.stl` or `.svg` files for your bopper, if 3d-printing.**
I chose to laser cut my bopper. The svg can be downloaded [here](https://github.com/chrisbrownell/IDD-Fa18-Lab5-ckb77/blob/master/uselessarm.svg) but the GitHub preview seems to show nothing... a screeshot is included below. For my bopper I used inkscape to draw an arm that would (1) rest below the top of the box in the "LOW" state and (2) fully extend outside the box toward a switch location when rotated 60-90 degrees by a servo in the "HIGH" state. At first I tried to add just one "tounge" piece (the smaller component that fits into the tip of the bopper. After testing a bit, it became clear that one tongue was not sufficient so I added two more (with deeper grooves) to glue on the top and bottom of the initial tongue piece.

SVG screenshot:
![svgscreenshot](https://github.com/chrisbrownell/IDD-Fa18-Lab5-ckb77/blob/master/bopper.png)

Initial bopper with one tongue:
![t1](https://github.com/chrisbrownell/IDD-Fa18-Lab5-ckb77/blob/master/IMG_1557.PNG)

v2 bopper with three tongues:
![t1](https://github.com/chrisbrownell/IDD-Fa18-Lab5-ckb77/blob/master/IMG_1558.PNG)


## Laser Cutting

**b. Include a photo of your box here.**

I added a little smiley-face on the side of my box before sending to the laser cutter. 
![box](https://github.com/chrisbrownell/IDD-Fa18-Lab5-ckb77/blob/master/IMG_5935.JPG)

## Electronics

**c. Upload code & a photo of your electronic circuit here.**

I added an LED to the inside of my box hoping that the light would shine through the smiley face holes, but with the lights on in the lab the light emitted by the LED was not discernable. The logic was to light up whenever the box was "working". 

Code for my servo arm and LED:
```
#include <Servo.h> 

#define servoPin  10
#define switchPin 2

#define closePos  0
#define openPos  70

Servo servo;
int switchState;
int previousSwitchState;
int ledState;

const int ledPin = 1;

// call this when the input on pin 2 changes (LOW to HIGH *or* HIGH to LOW)
void ToggleSwitch(int switchState)
{    
  if (switchState == HIGH)
  { // turn on LED, open up the box
    ledState = HIGH; 
    digitalWrite(ledPin,ledState);
    servo.write(openPos);
  }
  else
  { // close the box, turn off LED
    servo.write(closePos);
    ledState = LOW;
    digitalWrite(ledPin,ledState);
  }
  previousSwitchState = switchState;  // remember that the switch state has changed 
}

void setup()
{
  // start with the box closed and the switch in the off postion and LED off
  switchState = LOW;
  previousSwitchState = LOW;
  ledState = LOW;

  // connect to our servo and make sure it is in the closed position
  servo.attach(servoPin);
  servo.write(closePos);

  // we should probably pay attention to the switch and we want to talk to LED pin
  pinMode(switchPin, INPUT); 
  pinMode(ledPin, OUTPUT);

}

void loop()
{ 
  int switchState = digitalRead(switchPin);
  if (switchState != previousSwitchState)
    ToggleSwitch(switchState);

  delay(70);
}
```

Photo of setup:
![board](https://github.com/chrisbrownell/IDD-Fa18-Lab5-ckb77/blob/master/IMG_4784.JPG)


## Putting it All Together

Include here:
1. Your Arduino code.

    - See above
    
1. `.stl` or `.svg` files for your "bopper" — if you use some other technique, include the respective supporting material.

1. At least one photo of your useless box taken in the MakerLab's Portable Photo Studio (or somewhere else, but of similar quality).
1. A video of your useless box in action.
