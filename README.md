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
