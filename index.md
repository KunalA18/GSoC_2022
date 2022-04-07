Hello, I am Kunal Agarwal from VJTI, Mumbai. This is the first time I'll be applying for GSoC. After going through a vast array of Organisations and learning about their projects, I finally found "*OpenGL/OpenCL software ISP*" project of **libcamera** most interesting.

## Getting Started

I joined the IRC and subscribed to libcamera's mailing list and started exploring the project in detail. After discussion with mentors on IRC, I started with the Warmup tasks listed under my project. And to sum up my journey of completing all the warmup tasks, along with the challenges faced by me and how I solved them, I am writing this blog.

## Getting Warmed up
Warmup tasks were provided under each project for new contributors to get familiar with the code base and complete the pre-requisites of the project interested in. I too started understanding and implementing these tasks.

### 1. Building libcamera with the raspberrypi pipeline enabled and running qcam.
- First I followed the [getting started](https://libcamera.org/getting-started.html) section on libcamera's website, which involved installing all dependencies and building libcamera. I was able to successfully build and test its working on my Linux PC.
- To build and test it on my Raspberry Pi 3B, first I had to upgrade my Raspbian version from buster to bullseye. Also had to buy a 5MP Raspberry Pi 3B Camera Module for testing.
-  Since the Raspbian bullseye had libcamera and required libraries perbuilt, I was easily capture an image using 
```
libcamera-jpeg -o test.jpg
```
- My next target was to build libcamera on Rpi from source. Installed all the dependencies and built libcamera successfully using same steps as on PC.
- Next step was running qcam. For this I enabled raspberryPi pipeline using `-Dpipelines=raspberrypi`, enabled ipa on Rpi `-Dipas=raspberrypi` and enabled qcam using `-Dqcam=enabled` while building meson.
- Finally after 
``
sudo ninja -C build install
``, got the qcam running :).

### 2. Testing OpenGL on RaspberryPi 
- To run openGL on Rpi, I first enabled ***OpenGL drivers*** using `sudo raspi-config` and performed a reboot.
- Next step involved installing glfw and other required packages.(You can find the installation steps in my Github repository. Link is shared in the next section of blog)
- Finally i wrote a small test program and compiled it using 

```
gcc test.cpp -lGL -lGLEW -lm -lglfw -o success
```
- An executable was created named 'success' and on running it, boom! glfw window was displayed.

### 3. Writing a standalone OpenGL application which takes an image and applies ISP function on it.








