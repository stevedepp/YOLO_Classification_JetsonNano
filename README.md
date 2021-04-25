# YOLO_Classification_JetsonNano
tgif project: a day to create a YOLO model for object detection and classification running on my Jetson Nano

This video served as the 75% progress update for YOLO ASL project.

You can click this video to listen to sound or follow along with the slides and transcript below the video.

![demo](https://user-images.githubusercontent.com/38410965/111721866-20373580-8837-11eb-94ff-de4a4e55b454.mp4)

#

> Hi this is Steve Depp.

**Steve Depp   
### Final Project update 75%   
You Only Look Once   
Build —> Live detect in 7 steps** 



#

> I’m going to be giving you my 75% update on my final project.  We are going to be looking at You Only Look Once.  It’s only 7 steps, but ... 
 


#

> ... they’re all done on the Jetson Nano.  L4T is its operating system.  We’re going to first do a quick update of some files:

`sudo apt-get update`   

*(this code implementation is not shown in the video)*   



#

> Then we’re going to assign some environment variables.  Just to note, you should be using CUDA10 for all of this. 

`export PATH=/usr/local/cuda-10.0/bin${PATH:+:${PATH}}`   
`export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}`

*(this code implementation is not shown in the video)*     



#

> J Reddy and Alexy are the two principals.  J Reddy invented YOLO.  Alexy’s adopted it in the last 3 months.    

`git clone https://github.com/AlexeyAB/darknet.git`   

*(this code implementation is not shown in the video)*   



#

> We’re going to be using Reddy’s weights and Alexy’s model. 

`wget https://pjreddie.com/media/files/yolov3.weights`    
`wget https://pjreddie.com/media/files/yolov3-tiny.weights`    

*(this code implementation is not shown in the video)*   



#

> We’re going to adapt the model so that it uses the GPU and CUDA and OPENCV.

`sudo apt install nano`   
`nano Makefile`
   
	`GPU=1
	CUDNN=1
	OPENCV=1`

*(this code implementation is not shown in the video)*   



#

> And, we’re going to build it with “make”. 

‘make’   

*(this code implementation is not shown in the video)*   



#

> First thing we’re going to do is to run our 3 samples, ...     
	-	test50.mp4
	- test52.mp4
	- live



#

> ... but we are going to run first this one that comes from the library.  All you are going to do is see people walking through a train station, and the model will identify them and the objects that they’re carrying. 

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights **test50.mp4** -i 0 -thresh 0.25` 



#

> It builds really quickly even on the Jetson Nano.  You can see here.  

 `./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights **test50.mp4** -i 0 -thresh 0.25` 



#

> You will see they’re identifying people, handbags, suitcases and backpacks. 

 `./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights **test50.mp4** -i 0 -thresh 0.25` 



#

> Second one is more relevant to my project.  This is an example of people and then also of people using hand signs.  This guy’s at a concert.  I think a Beyonce concert, and he’s kinda, kinda boisterous in his hand signals.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights **test52.mp4** -i 0 -thresh 0.25`



#

> Once again, the model runs really quickly. 

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights **test52.mp4** -i 0 -thresh 0.25`



#

> Newscasters.  Identifying his tie and the two people.  This one’s a little slower.  It’s kind of at about 2 to 4 frames per second which you know normally it’s around 30 or 40 frames. 

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights **test52.mp4** -i 0 -thresh 0.25`



(This isn’t actually a set of misidentifications.  The video is slow and the model is already showing bounding boxes and classifications from the next frame before the video can catch up!) 



#

> You can see the cars are being identified here, … this person, … there will be multiple people identified on the left and the center.  You can see cars being identified in the distance, and two people on the left there.     

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights **test52.mp4** -i 0 -thresh 0.25`



#

> You can see the confidence levels over here just sorta going by.  These will be relevant when the guy shows up on stage.  You can see it’s identifying “traffic light” with low confidence.   

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights **test52.mp4** -i 0 -thresh 0.25`



#

> Here comes the fellow.  We’re at 5 frames per second.  It sorta loses him in the smoke, and you see the confidence level goes down to 30 or 40 percent.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights **test52.mp4** -i 0 -thresh 0.25`



# 

> When the smoke clears, it goes up to 90 percent.  It’s catching a chair.

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights **test52.mp4** -i 0 -thresh 0.25`


#

> And now we’re back up to 100%

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights **test52.mp4** -i 0 -thresh 0.25`

# 

> Getting out of that.  This last thing is just my desk, and I’m just going to show you how it doesn’t actually pick up much when the picture is upside down. 

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv **flip-method=0** ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`



#

> The computer really begins to slow down after running for this long.  It’s a very low energy computer.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv **flip-method=0** ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`
 


#

> It’s just picking up my hand and nothing else.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv **flip-method=0** ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`



#

> So, I kill this with either escape or control, and you see it kinda browns out there. That’s the loss of energy.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv **flip-method=0** ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`



#

> And we’ll rerun it with the “flip-method” at 2, which is just turning it upside down.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv **flip-method=2** ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`




#

> So, *(while this is running, I’ll mention that)* the next step is to set up custom classes, and that’s a real big deal because we have to build, I have to build, bounding boxes on about 2,000 images, but there’s a tool that allows me to do this in, kind of, an easier way.  

**Next step**.    
**24 custom classes for 24 hand signed letters**

- bounding boxes ~ 2400 samples
- training
- code amendments

**Motivation: Instant recognition is essential**

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv **flip-method=2** ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`


#

> And here you can just see it’s picking up on various things on my desk: a cell phone; it thinks something is a cat back there.  It sees my hand that I am a person.  It sees a bottle in the background, … my laptop.  The giraffe looks like a cat as well, but it picks up on everything.  Thanks very much for watching.  I do appreciate it.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv **flip-method=2** ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`




