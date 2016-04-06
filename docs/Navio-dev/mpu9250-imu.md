**MPU9250**  

MPU9250 is one of the best in class inertial sensors, which combines a gyroscope, an accelerometer and a magnetometer in one device. MPU sensor family is not only popular as a part of drone autopilot projects, but is also widely used in devices like cellphones, tablets, etc.

**IMU example**  

If you haven't already done that, download Navio drivers and examples code [here](navio-repository-cloning/).

***C++***  
Move to the folder with the source code, compile and run the example:

```bash
cd C++/Examples/AccelGyroMag
make
./AccelGyroMag
```

***Python***  
Move to the folder with the source code, compile and run the example:
```bash
cd Python
python AccelGyroMag.py
```

You should immediately see 9 values, updated in real time. Try to move the device around and see them change. They include Accelerometer, Gyroscope and Magnetometer data, three axis each.  
```bash
Acc:  +0.014  +0.139  +9.974  Gyr:   -0.042   +0.022   +0.011  Mag: -3525.450 +29.584  +0.000
Acc:  -0.010  +0.268 +10.036  Gyr:   -0.042   +0.019   +0.015  Mag: -14.963 +43.390 -50.130
Acc:  -0.010  +0.278  +9.888  Gyr:   -0.043   +0.021   +0.012  Mag: -16.566 +42.852 -50.302
Acc:  +0.010  +0.187 +10.041  Gyr:   -0.039   +0.021   +0.011  Mag: -14.963 +42.314 -50.817
Acc:  -0.062  +0.158  +9.855  Gyr:   -0.039   +0.020   +0.011  Mag: -15.497 +42.493 -49.959
Acc:  -0.067  +0.196 +10.056  Gyr:   -0.044   +0.020   +0.013  Mag: -14.963 +43.748 -50.130
```  

For further information see source code. The first thing we should pay attention to is the line ```imu.initialize()```, as it does an important job of setting internal device parameters. Note that this function also sets scales for both Accelerometer and Gyroscope. The function is defined in ```C++/Navio/MPU9250.cpp```.  
The main function loop is pretty straightforward: read the data, print the data.

You can find additional information about the chips in [MPU-9250 datasheet](http://store.invensense.com/datasheets/invensense/MPU9250REV1.0.pdf).
