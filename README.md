# CircuitPython
## My CircuitPython assignments

### LEDFade:
#### Objective
Make a LED fade up to the full brightness (255) and back down to the lowest (0).

#### Lessons
In this assignment we learned how to use the new metro express board as well as CircuitPython using Mu.
#### Important Code
`FadeNew.py`
``` python
    
#Cap touch servo
import time
import board
import pulseio
from adafruit_motor import servo
import touchio


touch_A1 = touchio.TouchIn(board.A1)
touch_A2 = touchio.TouchIn(board.A2)
# create a PWMOut object on Pin A2.
pwm = pulseio.PWMOut(board.D5, duty_cycle=2 ** 15, frequency=50)
angle = 0
# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)

while True:
    if touch_A1.value:
        print("Touched A1!")
        if angle < 180:
            angle = angle +5
        my_servo.angle = angle
        time.sleep(0.05)
    if touch_A2.value:
        print("Touched A1!")
        if angle > 0:
            angle = angle -5
        my_servo.angle = angle
        time.sleep(0.05)
```
Our variable counts up, but once it reaches 6000, it multiplies it by a negative and it counts down until it reaches 2000, where it begins to count up. 

### Circuit Python Servo:
#### Objective
Using duty cycle and capacitive touch to make a servo turn back and forth. 

#### Lessons
Learned how to use pwm(pulse width modulation) as well as capacitive touch. 
#### Important Code
`Code_180.py`
``` python

import time

import board
import pulseio


# Initialize PWM output for the servo (on pin D5):
servo = pulseio.PWMOut(board.D5, frequency=50)

# Create a function to simplify setting PWM duty cycle for the servo:
def servo_duty_cycle(pulse_ms, frequency=50):
    period_ms = 1.0 / frequency * 1000.0
    duty_cycle = int(pulse_ms / (period_ms / 65535.0))
    return duty_cycle

# Main loop will run forever moving between 1.0 and 2.0 mS long pulses:
while True:
    servo.duty_cycle = servo_duty_cycle(.5)
    time.sleep(1.0)
    servo.duty_cycle = servo_duty_cycle(2.4)
    time.sleep(1.0)
    
```
    
### CircuitPython LCD:
#### Objective 
Use a button to have a lcd screen count the number of times you click it.
    
#### Lessons
How to code a lcd screen from your serial monitor.
#### Important code
`lcdbutton.py`
 ``` python
import time
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
from digitalio import DigitalInOut, Direction, Pull
from lcd.lcd import CursorMode
import board
# Talk to the LCD at I2C address 0x27.
# The number of rows and columns defaults to 4x20, so those
# arguments could be omitted in this case.
lcd = LCD(I2CPCF8574Interface(0x3F), num_rows=2, num_cols=16)
# 0x27 or 0x3F
button = DigitalInOut(board.D2)
button.direction = Direction.INPUT
button.pull = Pull.UP
button_state = None
last_state = None
value = 0
lcd.print("  CircuitPython    	LCD ")
time.sleep(2)
lcd.clear()

lcd.set_cursor_pos(1, 0)
lcd.print("ButtonPresses:")
# Make the cursor visible as a line.
lcd.set_cursor_mode(CursorMode.LINE)
while True:
    if button.value:
        print("not pressed")
    else:
        value = value + 1
        print(value)
        button_state = None
        # lcd.set_cursor_pos(1, 14)
        # lcd.print(value)
# if button is high and last_state = low
    time.sleep(0.01)

```

### CircuitPython Photointerrupters:
#### Objective 
Wire and code a photo interupter and have the serial monitor tell you how many times it was interupted.
    
#### Lessons
How to use and code a photo interupter.
#### Important code
``
 ``` python

