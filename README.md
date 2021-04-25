# YOLO Classification on the JetsonNano: Newscasters, ASL at a Beyonce concert, and is it a cat or a giraffe?

TGIF project: a day to create a YOLO model for object detection and classification running on my Jetson Nano.

This video served as the 75% progress update for YOLO ASL project.

You can click this video to listen to sound or follow along with the slides and transcript below the video.

![demo](https://user-images.githubusercontent.com/38410965/111721866-20373580-8837-11eb-94ff-de4a4e55b454.mp4)

#

> Hi this is Steve Depp.

**Steve Depp   
Final Project update 75%   
You Only Look Once   
Build —> Live detect in 7 steps** 

<img width="1088" alt="Pasted Graphic 8" src="https://user-images.githubusercontent.com/38410965/116006810-db8f7e80-a5da-11eb-8492-f0b1b3bff46c.png">

#

> I’m going to be giving you my 75% update on my final project.  We are going to be looking at You Only Look Once.  It’s only 7 steps, but ... 
 
<img width="794" alt="Pasted Graphic 1" src="https://user-images.githubusercontent.com/38410965/116006807-d6caca80-a5da-11eb-9a06-07ad735fac61.png">

#

> ... they’re all done on the Jetson Nano.  L4T is its operating system.  We’re going to first do a quick update of some files:

`sudo apt-get update`   

*(this code implementation is not shown in the video)*   

<img width="794" alt="Pasted Graphic 2" src="https://user-images.githubusercontent.com/38410965/116006789-c9addb80-a5da-11eb-939a-06482f6c46b0.png">

#

> Then we’re going to assign some environment variables.  Just to note, you should be using CUDA10 for all of this. 

`export PATH=/usr/local/cuda-10.0/bin${PATH:+:${PATH}}`   
`export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}`

*(this code implementation is not shown in the video)*     

<img width="794" alt="Pasted Graphic 3" src="https://user-images.githubusercontent.com/38410965/116006781-c31f6400-a5da-11eb-8c9a-c29fe6b5dbc5.png">

#

> J Reddy and Alexy are the two principals.  J Reddy invented YOLO.  Alexy’s adopted it in the last 3 months.    

`git clone https://github.com/AlexeyAB/darknet.git`   

*(this code implementation is not shown in the video)*   

<img width="794" alt="Pasted Graphic 4" src="https://user-images.githubusercontent.com/38410965/116006779-bd298300-a5da-11eb-9899-d6771870ed71.png">

#

> We’re going to be using Reddy’s weights and Alexy’s model. 

`wget https://pjreddie.com/media/files/yolov3.weights`    
`wget https://pjreddie.com/media/files/yolov3-tiny.weights`    

*(this code implementation is not shown in the video)*   

<img width="794" alt="Pasted Graphic 5" src="https://user-images.githubusercontent.com/38410965/116006773-b6027500-a5da-11eb-9b9e-93af76d402f7.png">

#

> We’re going to adapt the model so that it uses the GPU and CUDA and OPENCV.

`sudo apt install nano`   
`nano Makefile`
   
	`GPU=1
	CUDNN=1
	OPENCV=1`

*(this code implementation is not shown in the video)*   

<img width="794" alt="Pasted Graphic 6" src="https://user-images.githubusercontent.com/38410965/116006768-adaa3a00-a5da-11eb-9c09-6afd36d99220.png">

#

> And, we’re going to build it with “make”. 

‘make’   

*(this code implementation is not shown in the video)*   

<img width="794" alt="Pasted Graphic 7" src="https://user-images.githubusercontent.com/38410965/116006757-9408f280-a5da-11eb-9510-5c8d1986c8fc.png">

#

> First thing we’re going to do is to run our 3 samples, ...     
	- test50.mp4
	- test52.mp4
	- live

<img width="794" alt="Pasted Graphic 11" src="https://user-images.githubusercontent.com/38410965/116006751-8f443e80-a5da-11eb-9316-02f36c9e9031.png">

#

> ... but we are going to run first this one that comes from the library.  All you are going to do is see people walking through a train station, and the model will identify them and the objects that they’re carrying. 

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test50.mp4 -i 0 -thresh 0.25` 

<img width="1088" alt="Pasted Graphic 10" src="https://user-images.githubusercontent.com/38410965/116006741-881d3080-a5da-11eb-8403-c2e01949ce0b.png">

#

> It builds really quickly even on the Jetson Nano.  You can see here.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test50.mp4 -i 0 -thresh 0.25` 

<img width="1088" alt="Pasted Graphic 12" src="https://user-images.githubusercontent.com/38410965/116006735-80f62280-a5da-11eb-8b4c-6a119db47564.png">

<img width="1088" alt="Pasted Graphic 13" src="https://user-images.githubusercontent.com/38410965/116006731-7d629b80-a5da-11eb-9711-5eb736e54c32.png">

#

> You will see they’re identifying people, handbags, suitcases and backpacks. 

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test50.mp4 -i 0 -thresh 0.25` 

<img width="1088" alt="Pasted Graphic 14" src="https://user-images.githubusercontent.com/38410965/116006721-73d93380-a5da-11eb-9cf3-31a8550720d7.png">

#

> Second one is more relevant to my project.  This is an example of people and then also of people using hand signs.  This guy’s at a concert.  I think a Beyonce concert, and he’s kinda, kinda boisterous in his hand signals.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test52.mp4 -i 0 -thresh 0.25`

<img width="1088" alt="Pasted Graphic 15" src="https://user-images.githubusercontent.com/38410965/116006713-6ae86200-a5da-11eb-8831-30a7dda7b078.png">

#

> Once again, the model runs really quickly. 

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test52.mp4 -i 0 -thresh 0.25`

<img width="1088" alt="Pasted Graphic 16" src="https://user-images.githubusercontent.com/38410965/116006707-6459ea80-a5da-11eb-9ff8-2a78939f63b0.png">

<img width="1088" alt="Pasted Graphic 17" src="https://user-images.githubusercontent.com/38410965/116006697-5ad08280-a5da-11eb-8036-75eb271ce6fc.png">

#

> Newscasters.  Identifying his tie and the two people.  This one’s a little slower.  It’s kind of at about 2 to 4 frames per second which you know normally it’s around 30 or 40 frames. 

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test52.mp4 -i 0 -thresh 0.25`

<img width="1088" alt="Pasted Graphic 18" src="https://user-images.githubusercontent.com/38410965/116006693-5310de00-a5da-11eb-99c6-d27dcbc04179.png">

(This isn’t actually a set of misidentifications.  The video is slow and the model is already showing bounding boxes and classifications from the next frame before the video can catch up!) 

<img width="1088" alt="Pasted Graphic 50" src="https://user-images.githubusercontent.com/38410965/116006681-4a200c80-a5da-11eb-9abf-de0199f72308.png">

#

> You can see the cars are being identified here, … this person, … there will be multiple people identified on the left and the center.  You can see cars being identified in the distance, and two people on the left there.     

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test52.mp4 -i 0 -thresh 0.25`

<img width="1088" alt="IYANI HUGHES" src="https://user-images.githubusercontent.com/38410965/116006676-42606800-a5da-11eb-8431-4debcbdd6f0f.png">

<img width="1088" alt="IYANI HUGHES" src="https://user-images.githubusercontent.com/38410965/116006671-3e344a80-a5da-11eb-9ac7-4e19451ee80c.png">

#

> You can see the confidence levels over here just sorta going by.  These will be relevant when the guy shows up on stage.  You can see it’s identifying “traffic light” with low confidence.   

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test52.mp4 -i 0 -thresh 0.25`

<img width="1088" alt="PRIDE SIGN LANGUAGE INTERPRETER GOES VIRAL" src="https://user-images.githubusercontent.com/38410965/116006665-35dc0f80-a5da-11eb-9719-cad214504467.png">

#

> Here comes the fellow.  We’re at 5 frames per second.  It sorta loses him in the smoke, and you see the confidence level goes down to 30 or 40 percent.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test52.mp4 -i 0 -thresh 0.25`

<img width="1088" alt="PRIDE SIC  LANGUAGE INTERPRETER GOES VIRAL" src="https://user-images.githubusercontent.com/38410965/116006660-31aff200-a5da-11eb-9f63-10511d76889c.png">

<img width="1088" alt="PRIDE SIG I LANGUAGE INTERPRETER GOES VIRAL" src="https://user-images.githubusercontent.com/38410965/116006654-2bba1100-a5da-11eb-840e-5529ab809748.png">

# 

> When the smoke clears, it goes up to 90 percent.  It’s catching a chair.

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test52.mp4 -i 0 -thresh 0.25`

<img width="1088" alt="PRIDE SIG I LANGUAGE INTERPRETER GOES VIRAL" src="https://user-images.githubusercontent.com/38410965/116006648-22c93f80-a5da-11eb-825c-946a77a183b4.png">

<img width="1088" alt="Pasted Graphic 28" src="https://user-images.githubusercontent.com/38410965/116006641-1e048b80-a5da-11eb-9e29-41f970e7653c.png">

#

> And now we’re back up to 100%

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test52.mp4 -i 0 -thresh 0.25`

<img width="1088" alt="PRIDE SIG I LANGUAGE INTERPRETER GOES VIRAL" src="https://user-images.githubusercontent.com/38410965/116006636-1644e700-a5da-11eb-9685-8801926250c6.png">

# 

> Getting out of that.  This last thing is just my desk, and I’m just going to show you how it doesn’t actually pick up much when the picture is upside down. (**flip_method=0**)

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv flip-method=0 ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`

<img width="1088" alt="Pasted Graphic 30" src="https://user-images.githubusercontent.com/38410965/116006631-0decac00-a5da-11eb-90a8-d342122d4aa7.png">

<img width="1088" alt="Pasted Graphic 31" src="https://user-images.githubusercontent.com/38410965/116006627-0af1bb80-a5da-11eb-96ab-3f29c0955158.png">

#

> The computer really begins to slow down after running for this long.  It’s a very low energy computer.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv flip-method=0 ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`
 
<img width="1088" alt="Pasted Graphic 32" src="https://user-images.githubusercontent.com/38410965/116006619-01685380-a5da-11eb-8984-7665c89a6fc6.png">

<img width="1088" alt="Pasted Graphic 33" src="https://user-images.githubusercontent.com/38410965/116006616-fd3c3600-a5d9-11eb-8a3c-612ab7a6b05a.png">

#

> It’s just picking up my hand and nothing else.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv flip-method=0 ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`

<img width="1088" alt="Pasted Graphic 34" src="https://user-images.githubusercontent.com/38410965/116006603-f3b2ce00-a5d9-11eb-9a1a-3a59d15082dd.png">

<img width="1088" alt="Pasted Graphic 35" src="https://user-images.githubusercontent.com/38410965/116006599-ee558380-a5d9-11eb-81f5-8f0a0a79ace8.png">

#

> So, I kill this with either escape or control, and you see it kinda browns out there. That’s the loss of energy.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv flip-method=0 ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`

<img width="1088" alt="Pasted Graphic 36" src="https://user-images.githubusercontent.com/38410965/116006587-e4338500-a5d9-11eb-8179-b4f04ef44516.png">

<img width="1088" alt="Pasted Graphic 37" src="https://user-images.githubusercontent.com/38410965/116006580-ded63a80-a5d9-11eb-8436-28c9c11b35c4.png">

#

> And we’ll rerun it with the **“flip-method” at 2**, which is just turning it upside down.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv flip-method=2 ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`

<img width="1088" alt="Pasted Graphic 39" src="https://user-images.githubusercontent.com/38410965/116006573-d41ba580-a5d9-11eb-90e3-248fe042ab2c.png">

<img width="1088" alt="Pasted Graphic 40" src="https://user-images.githubusercontent.com/38410965/116006566-ccf49780-a5d9-11eb-8ce6-de6a3d8c559a.png">

<img width="1088" alt="Pasted Graphic 41" src="https://user-images.githubusercontent.com/38410965/116006564-c82fe380-a5d9-11eb-800a-cac4943c30f0.png">

#

> So, *(while this is running, I’ll mention that)* the next step is to set up custom classes, and that’s a real big deal because we have to build, I have to build, bounding boxes on about 2,000 images, but there’s a tool that allows me to do this in, kind of, an easier way.  

**Next step**.    
**24 custom classes for 24 hand signed letters**

- bounding boxes ~ 2400 samples
- training
- code amendments

**Motivation: Instant recognition is essential**

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv flip-method=2 ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`

<img width="1088" alt="Pasted Graphic 42" src="https://user-images.githubusercontent.com/38410965/116006551-bf3f1200-a5d9-11eb-8599-5b938e29cdd9.png">

<img width="1088" alt="Pasted Graphic 45" src="https://user-images.githubusercontent.com/38410965/116006543-b8180400-a5d9-11eb-94c0-19cdb4fcac06.png">

#

> And here you can just see it’s picking up on various things on my desk: a cell phone; it thinks something is a cat back there.  It sees my hand that I am a person.  It sees a bottle in the background, … my laptop.  The giraffe looks like a cat as well, but it picks up on everything.  Thanks very much for watching.  I do appreciate it.  

`./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights "nvarguscamerasrc auto-exposure=1 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)NV12, framerate=(fraction)60/1 ! nvvidconv flip-method=2 ! video/x-raw, width=(int)1280, height=(int)720, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink -e”`

<img width="1088" alt="Pasted Graphic 46" src="https://user-images.githubusercontent.com/38410965/116006533-aafb1500-a5d9-11eb-9316-4d3d99a3b663.png">

<img width="1088" alt="Pasted Graphic 49" src="https://user-images.githubusercontent.com/38410965/116006523-a5053400-a5d9-11eb-9063-b8b80a22301e.png">
