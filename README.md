
# Robo: open-source hardware and software platform for general-purpose robot. 

* **Robopilot** : a python self driving library
* **Roborg** :  open hardware platform

The realization of autonomous movement of a robot within a given environment. Real-time mapping and recognition of objects through computer vision algorithms.

Robopilot is minimalist and modular autonomous library for Python. It is developed for hobbyists and students with a focus on allowing fast experimentation and easy
community contributions. It is based [donkeycar project](http://donkeycar.com), associated machine vision, communications and motor-control libraries and the CUDA and Tensor Flow deep-learning framework. 

In this study, computer vision and motor-control libraries are used together to design and develop a real-time visually and contextually intelligent autonomous robot that execute a given trajectory and provide a live, dense three-dimensional (3D) map of an area.

## Use Robopilot if you want to

* Make a robot pilot its self.
* Experiment with autopilots, mapping computer vision and neural networks.
* Log sensor data. (images, user inputs, sensor readings)
* Control your robot via a web or game controller.
* Leverage community contributed driving data.

### Test Platform
* Nvidia TX1
* RedCat Crawler 1/5
* Xbox Kinect for PC

![platform](https://user-images.githubusercontent.com/37585803/138308842-92476b43-2ebb-48f6-9952-89c73a331adc.png)
![device](https://user-images.githubusercontent.com/37585803/138308832-0560e7c5-758e-479b-a845-1b87ab2cc608.png)

### Get driving.
After building a Donkey2 you can turn on your car and go to http://localhost:8887 to drive.

### Modify your cars behavior.
The donkey car is controlled by running a sequence of events

```python
#Define a vehicle to take and record pictures 10 times per second.

import time
from donkeycar import Vehicle
from donkeycar.parts.cv import CvCam
from donkeycar.parts.tub_v2 import TubWriter
V = Vehicle()

IMAGE_W = 160
IMAGE_H = 120
IMAGE_DEPTH = 3

#Add a camera part
cam = CvCam(image_w=IMAGE_W, image_h=IMAGE_H, image_d=IMAGE_DEPTH)
V.add(cam, outputs=['image'], threaded=True)

#warmup camera
while cam.run() is None:
    time.sleep(1)

#add tub part to record images
tub = TubWriter(path='./dat', inputs=['image'], types=['image_array'])
V.add(tub, inputs=['image'], outputs=['num_records'])

#start the drive loop at 10 Hz
V.start(rate_hz=10)
```
