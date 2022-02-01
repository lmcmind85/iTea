# iTea

# 12/6/21

```python

pwm = pwmio.PWMOut(board.A4, frequency=50)
my_servo = servo.ContinuousServo(pwm)

def dunkage():
    print("Dunk")
    my_servo.throttle = 1.0
    time.sleep(1.0)
    print("stop")
    my_servo.throttle = 0.0
    time.sleep(1.0)
    print("reverse")
    my_servo.throttle = -1.0
    time.sleep(1.0)
    print("stop")
    my_servo.throttle = 0.0
    time.sleep(1.0) 
    ```


lcd.print()



import board
import time
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
import pwmio
from adafruit_motor import servo
import rotaryio
import digitalio


i2c = board.I2C()
lcd = LCD(I2CPCF8574Interface(i2c, 0x3F), num_rows=2, num_cols=16)

pwm = pwmio.PWMOut(board.A4, frequency=50)
my_servo = servo.ContinuousServo(pwm)

pwm = pwmio.PWMOut(board.A3, duty_cycle=2 ** 15, frequency=50)
my_servo1 = servo.Servo(pwm)


encoder = rotaryio.IncrementalEncoder(board.D5, board.D6)
last_position = None

button = digitalio.DigitalInOut(board.D3)
button.direction = digitalio.Direction.INPUT
button.pull = digitalio.Pull.UP

button_state = None
while True:
    position = encoder.position
    time.sleep(0.1)
    if last_position is None or position != last_position:
        print(position)
    last_position = position
    if position != 0 or 1 or 2:
        lcd.clear()
    if position == 0:
        lcd.home()
        lcd.print("Welcome!")
        time.sleep(1)
    if position == 1:
        lcd.home()
        lcd.print("English \nBreakfast")
        time.sleep(1)
    if position == 2:
        lcd.print("Something \nDifferent")
        time.sleep(1)
    if not button.value and button_state is None:
        button_state = "pressed"
    if button.value and button_state == "pressed":
        print("Button pressed.")
        button_state = None
 ```
    
