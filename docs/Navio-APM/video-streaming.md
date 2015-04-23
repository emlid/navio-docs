####Raspberry PI2 + NavIO + APM = FPV

Streaming real-time video from a drone powered by a Raspberry Pi 2 has never been easier. 

There is only only a handful of actions that you need to make to get a drone streaming real-time video to a remote PC, tablet, phone or whatnot.

####Raspberry PI2

First things first. You need to install some packages on RPi2

```bash
sudo apt-get install gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-libav
```

After the installation has completed you can choose whatever platform you want to stream FPV to.

####Ubuntu
If you're going to stream to a Ubuntu PC, install the same packages locally.

```bash
sudo apt-get install gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-libav
```

Launch gstreamer

```bash
gst-launch-1.0 -v udpsrc port=9000 caps='application/x-rtp, media=(string)video, clock-rate=(int)90000, encoding-name=(string)H264' ! \ 
    rtph264depay ! \
    avdec_h264 ! \
    videoconvert ! \
    autovideosink sync=f
```

From now on, your PC will be waiting for the input stream from Raspberry PI2. Once it gets a stream, you'll see the real-time video from your drone.

####Android
You can also use an Android for the same purpose. Check out [this](http://diydrones.com/profiles/blogs/how-to-run-a-mav-link-heads-up-display-on-android-or-windows-with) article to get it up and running. Use our [our](http://docs.emlid.com/Navio-APM/installation-and-running/) tutorial to run APM.

We've managed to get the video stream using an Android

![apm](http://www.emlid.com/wp-content/uploads/2014/10/APM.png)

Unfortunately, the cable length was not enough to make a selfie but at least we'd tried. 

####Windows
The tutorial is coming.

####Launching

Now we have everything set up for streaming!

ssh into your Raspberry once again and launch

```bash
raspivid -n -w 1280 -h 720 -b 1000000 -fps 15 -t 0 -o - | \
    gst-launch-1.0 -v \
    fdsrc !  \
    h264parse ! \
    rtph264pay config-interval=10 pt=96 ! \ 
    udpsink host=<remote_ip> port=9000
```
where <remote_ip> is the IP of the device you're streaming to.

Feel free to ask on out Discourse if you stumble upon any problems. We're always there at your convenience.  
