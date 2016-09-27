# Building from sources

![](img/APM.png)

####Where to get the code

Navio is supported in the main [APM repository](https://github.com/ArduPilot/ardupilot).

#### How to build
APM binary for Navio can be built using two ways:  

1) Directly on your Raspberry Pi. It will take approximately 15 minutes.

2) Using a cross-compiler (on Linux PC or virtual machine). This is much faster, but requires one-time setup.

If you'd like to build on Raspberry Pi or use Waf build system (either on Raspberry Pi or Linux PC) skip the next step.

####Cross-compiler setup on Linux (optional)
Standard ARM compiler from Ubuntu repositories is not suitable for cross-compiling for Raspberry Pi since it does not support hard float for ARMv6 architecture, instead use compiler provided by Raspberry Pi Foundation that is available <a href="https://github.com/raspberrypi/tools" target="_blank" >here</a>.


Download and extract it somewhere, for example in /opt/:

```bash
sudo git clone --depth 1 https://github.com/raspberrypi/tools.git /opt/tools
```


If you're using 32-bit distro add the following to your PATH:

```bash
export PATH=/opt/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian/bin:$PATH
```

For 64-bit distro add this to your PATH

```bash 
export PATH=/opt/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin:$PATH
```

If you would like to add the compiler to the PATH permanently edit /etc/environment.

####Building APM  using make-based build system
These steps are the same both for compiling APM directly on Raspberry Pi and cross-compiling.

Download the APM code and update submodules:

```bash
git clone https://github.com/ArduPilot/ardupilot.git
cd ardupilot
git submodule update --init
```
Navigate to the autopilot’s directory: APMrover, ArduCopter or ArduPlane. For example ArduCopter:
```bash
cd ArduCopter
```

Build for quadcopter:
```bash
make navio-quad
```

To build for other frame types replace quad with one of the following options:

```bash
quad tri hexa y6 octa octa-quad heli single obc nologging
```

In the end of compilation binary file with the name ArduCopter.elf will be placed in the same directory.

If you're using cross-compiler transfer the binary to your Raspberry Pi:

```bash
rsync -avz ArduCopter.elf pi@192.168.1.3:/home/pi/
```

Where 192.168.1.3 is an IP address of your Raspberry Pi with Navio.

####Building APM using Waf build system

These steps are the same both for compiling APM directly on Raspberry Pi and cross-compiling.

Download the APM code and update submodules:
```bash
git clone https://github.com/ArduPilot/ardupilot.git
cd ardupilot
git submodule update --init
```
Note that Waf should always be called from the ardupilot's root directory.

To keep access to Waf convenient, use the following alias from the root ardupilot directory:
```bash
alias waf="$PWD/modules/waf/waf-light"
```
Differently from the make-based build, with Waf there's a configure step to choose the board to be used:
```bash
waf configure --board=navio
```
Now you can build arducopter. For quadrocopter use the following command:
```bash
waf --targets bin/arducopter-quad
```
To build for other frame types replace quad with one of the following options:
```bash
coax heli hexa octa octa-quad single tri y6
```
In the end of compilation binary file with the name arducopter-quad will be placed in ardupilot/build/navio/bin/ directory.

If you're using cross-compiler transfer the binary to your Raspberry Pi:
```bash
rsync -avz ardupilot/build/navio/bin/arducopter-quad pi@192.168.1.3:/home/pi/
```
Where 192.168.1.3 is an IP address of your Raspberry Pi with Navio.

For further information read [ardupilot WAF Build](https://github.com/ArduPilot/ardupilot/blob/master/BUILD.md).

Instructions how to run APM on Raspberry and to connect GCS to it are available  [here](installation-and-running.md).
