Hello, I am Kunal Agarwal from VJTI, Mumbai. This is the first time I'll be applying for GSoC. After going through a vast array of Organisations and learning about their projects, I finally found "*OpenGL/OpenCL software ISP*" project of **libcamera** most interesting.

## Getting Started

I joined the IRC, subscribed to libcamera's mailing list and started exploring the project in detail. After discussion with mentors on IRC, I started with the Warmup tasks listed under my project. And to sum up my journey of completing all the warmup tasks, along with the challenges faced by me and how I solved them, I am writing this blog.

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
`` and running `build/src/qcam/qcam `, got the qcam running :). 
<h1 align ="center">
<image src="https://user-images.githubusercontent.com/83249996/162377050-68ea8781-6c1c-4fa5-94a3-8f2a65888759.png" alt = "original"  width = 600> 
   
</h1>

<br>

### 2. Testing OpenGL on RaspberryPi 
- To run openGL on Rpi, I first enabled ***OpenGL drivers*** using `sudo raspi-config` and performed a reboot.
- Next step involved installing glfw and other required packages.(You can find the installation steps in my Github repository. Link is shared in the next section of blog)
- Finally i wrote a small test program and compiled it using

```
   g++ test.cpp -lGL -lGLEW -lm -lglfw -o success
```
- An executable was created named 'success' and on running it, boom! glfw window was displayed.
   
 <h1 align ="center">
<image src="https://user-images.githubusercontent.com/83249996/162379029-2bccfd43-743e-48b5-86c4-adf411a8be84.png" alt = "original"  width = 600>
   
 </h1>  
    
<br>

### 3. Writing a standalone OpenGL application which takes an image and applies ISP function on it.
- This was one of the most interesting yet overwhelming task for me as this made me learn a new language - OpenGL from scratch.   
P.S. OpenGl is not exactly a language, but a kind of API, which helps in interacting with GPU, to achieve hardware-accelerated rendering
- My interest in Image processing drove me towards completing this task. As a beginner, I started looking at few tutorials and documentation of OpenGl.
- Next step involved setting up OpenGl by installing all dependencies. (All installation steps are mentioned in my github repository, shared below)
- Finally after setting it up, I wrote a test (hello world) program in openGl which created a window and a triangle on it.
One issue I faced here was while compiling the program. After tinkering and searching for about 30 mins, I figured out that we need to use linker flags for linking few libraries while compiling, for eg `-lGL -lglfw -lGLEW -lm` and got it running.
- Consequently, I had to understand the pipeline and the workflow of openGL which involved use of ***Shaders*** and ***Textures*** for GPU processing.
- One setback here was the inexperience with Cmake build system. It took me a day to get a hang of it. Finally I was able to write my own CMakeLists along with adding linkers to it. As soon as my program got built, it gave me immense joy and satisfaction.
- After dodging all the bullets, Finally i was able to load a Image and perform post-processing on it. Here is my Github repository link to view the source code and the outputs. A detailed description about implemented algorithms and their outputs are given in the Readme file.  
Repository link : [https://github.com/KunalA18/IP-openGL](https://github.com/KunalA18/IP-openGL)
- Few glimpses ;)
   
Original Image            |  Gamma correction
:-------------------------:|:-------------------------:
<image src="https://user-images.githubusercontent.com/83249996/162069982-9b99476b-c0a7-42c9-bab3-6ec0a5f695ff.png" alt = "original" width = 350> |   <image src="https://user-images.githubusercontent.com/83249996/162070112-c7bce182-80f7-4010-82b8-201f4f90118a.png" alt = "gamma_correction" width = 350> 
   





