# UAVcast

Complete Drone casting software for Raspberry PI in conjuction with 3G / 4G or WiFi. Can be used with Ardupilot or Navio boards (Emlid.com)

Discussion forum thread
[UAVcast. Casting software for Raspberry PI. Supports 3G / 4G / WiFi](http://uavmatrix.com/viewpost/5/110/741/0/Raspberry-Pi/UAVcast.-Casting-software-for-Raspberry-PI.-Supports-3G-/-4G-/-WiFi.)


[![UAVcast get started](https://img.youtube.com/vi/bz7Jlo1rRl0/0.jpg)](https://www.youtube.com/watch?v=bz7Jlo1rRl0)


### Installation

```
sudo apt-get update
sudo apt-get install git
sudo git clone -b Web_UI https://github.com/UAVmatrix/UAVcast.git
cd UAVcast/install
sudo ./install.sh web (notice the web argument)
```

## How it works
UAVcast uses regular software such as wvdial, inadyn. gstreamer, uqmi, and will fire up each program in the correct order users has defined in the DroneConfig.cfg file. 
 
After you have successfully installed UAVcast, reboot Raspberry and you should be able to access the web portal by opening your browser
and type the rpi IP address.

```
http://ip_to_rpi
```
 

## Commands
UAVcast uses systemd process handler. use the below commands if you want to start stopp service from comand line.

# Start
```sudo systemctl start UAVcast```

# Stop
```
sudo systemctl stop UAVcast
```

# Restart
```
sudo systemctl restart UAVcast
```

# Start on boot 
```
sudo systemctl enable UAVcast
```

# Not run on boot (for troubleshooting or other tasks)
```
sudo systemctl disable UAVcast
```


 
### Video
If you are using UAVcast with camera, its highly recommended to use gstreamer on the receiver end to achieve minimal latency.
Download [gstreamer](https://gstreamer.freedesktop.org/download/)

Use this client pipeline to receive video feed from UAVcast.

``` 
gst-launch-1.0.exe -e -v udpsrc port=5000 ! application/x-rtp, payload=96 ! rtpjitterbuffer ! rtph264depay ! avdec_h264 ! fpsdisplaysink sync=false text-overlay=false 
```

## Troubleshooting

Start ```UAVcast/DroneStart.sh ``` if you want a more verbose output of what exactly going on when UAVcast is started.
Also check the logfiles located in the /UAVcast/log folder.


If you are using PiCam, remember to enable the camera in ```Raspi-Config```


## Authors

* **Bernt Christian Egeland** - *creator and founder of UAVmatrix.com* - (http://uavmatrix.com)
