# Pi-In-the-Sky


## Spin-Copter

#### Goal 
For this project we need to get a Pi into the Sky. The payload must survive and function post-flight. We also need to collect data throughout the flight and save that data to the Pico’s onboard storage. For our project we decided to make a Spin Copter. We would record the wind speed and shoot the copter into the sky and it would record the height and amount of time it takes to fall back down. We would then see how wind speed affected the height and time it takes for the copter to reach the ground. 

## Table of Contents
* [Planning](#Planning)
* [Final](#Images)

### Planning

[Link to Planning Document](https://docs.google.com/document/d/1Hr9R5iVlL1ZFCEMLIhlKDtE9QW_wassNP-DMbSHPYS0/edit?usp=sharing)

### Prototype

#### Images

 <div class="row">
<!DOCTYPE png>
<png>
<body>

<figure>
  <img src="https://github.com/sgupta70/Spin-Copter---Pi-In-the-Sky/assets/71406905/d68b4344-4b22-46bb-9112-bfa1765b2c7f" alt="Answer 1" style ="width:25%">
</figure>

</body>
</png>

<!DOCTYPE png>
<png>
<body>

<figure>
  <img src="https://github.com/sgupta70/Spin-Copter---Pi-In-the-Sky/assets/71406905/6cbc7017-5f9c-41ab-a1be-02342d43c4a0" style ="width:47%">
 
</figure>

</body>
</png>
 </div>


Minus hook because Sahana broke it off 2 seconds before the picture

#### Wiring

![5678](https://github.com/sgupta70/Spin-Copter---Pi-In-the-Sky/assets/71406905/c492dff7-44f0-4ea8-9877-a3b86df8e97b)

### Final Project

#### Materials 
- Acrylic
- 3D printed parts
- Wires
- Raspberry Pico
- Pico Cowbell
- Switch
- Altimeter
- Battery

#### CAD

<div class="row">
<!DOCTYPE png>
<png>
<body>

<figure>

 <img src="https://github.com/sgupta70/Spin-Copter---Pi-In-the-Sky/assets/71406905/4c5a5fe3-7c59-41f8-80e8-40c6e86fb162" style ="width:45%">
 
</figure>

</body>
</png>

<!DOCTYPE png>
<png>
<body>

<figure>

  <img src="https://github.com/sgupta70/Spin-Copter---Pi-In-the-Sky/assets/71406905/b1e15580-b288-45cc-b243-82de10305d341" style ="width:45%">

</figure>

</body>
</png>

<!DOCTYPE png>
<png>
<body>

<figure>

  <img src="https://github.com/sgupta70/Spin-Copter---Pi-In-the-Sky/assets/71406905/9975e601-a422-4a24-ab55-fad226584ced" style ="width:45%">

</figure>

</body>
</png>

<!DOCTYPE png>
<png>
<body>

<figure>

 <img src="https://github.com/sgupta70/Spin-Copter---Pi-In-the-Sky/assets/71406905/86df8aa9-d854-415d-9b12-8a54c9012f46" style ="width:45%">

</figure>

</body>
</png>
 </div>


#### Final Wiring
![Screenshot (6)](https://github.com/sgupta70/Spin-Copter---Pi-In-the-Sky/assets/71406905/350fa1fa-858b-4343-ad7d-ff025bd16bc7)

#### Code
```
# type: ignore
# libraries: adafruit_mpu6050.mpy | adafruit_bus_device | adafruit_register
import adafruit_mpu6050
import busio
import board
import time
import digitalio
import displayio
import storage # imports
import adafruit_mpl3115a2

displayio.release_displays() # this needs to be first in the code

sda_pin = board.GP14
scl_pin = board.GP15
i2c = busio.I2C(scl_pin, sda_pin) 
#mpu = adafruit_mpu6050.MPU6050(i2c) # set up for variables and pin locations
sensor = adafruit_mpl3115a2.MPL3115A2(i2c)

#sensor.sealevel_pressure = 1000

while True: 
    altitude = sensor.altitude
    #acc = mpu.acceleration
    #print(f"X: {acc[0]}m/s² Y: {acc[1]}m/s² Z: {acc[2]}m/s²")
    print("Altitude: {0:0.2f} meters".format(altitude)) 
    time.sleep(0.25)
    with open("/data.csv", "a") as datalog:
        time_elapsed = time.monotonic()
        csv_string = f"{time_elapsed},{altitude},\n"
        # f string showing time, acc, and whether or not it's tilted
        datalog.write(csv_string)
        time.sleep(0.1) 
        datalog.flush() # record to the datalog
        time.sleep(0.25)
```

