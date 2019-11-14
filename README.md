# CircuitPython
## My CircuitPython assignments

### LEDFade:
#### Objective
Make a LED fade from full brightness (255) to 

#### Lessons
In this assignment we learned how to use the new metro express board as well as CircuitPython using Mu.
#### Important Code
`FadeNew.py`
``` python
    
while True: #essesialy a void loop
    for i in range(0, 65535, 1): #counts from 0 to 65535 and then writes it to the LED
        analog_out.value = i
    for j in range(65535, 0, -1): #counts from 65535 down to 0 and then writes it to the LED
        analog_out.value = j
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
