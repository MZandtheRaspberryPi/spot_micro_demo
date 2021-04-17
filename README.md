## Spot Micro Robot
This was a fun project where I 3d printed the robot, planned the hardware, assembled, and used a fellow robot builder's ROS Repo to get it walking. I contributed a bit to the robot builder's ROS repo as well. Check it out [here](https://github.com/MZandtheRaspberryPi/spot_micro_demo).    
![spot_micro_demo](screenshots/spot_micro_demo.gif)    

### Intro
Take a moment and move your mouse to the top left of your computer screen. What parts of your body moved to accomplish that task? If you do it again slowly, did you move your wrist? Your elbow? Your shoulder? Your torso? I assume that most of us moved multiple body parts in coordination, and I'd also assume that the force applied with your body parts was carefully controlled and that nobody broke their laptop.    

Now imagine you were programming a robot to do this task. Assuming you had a robot arm that had the same joints as your human arm, you'd have to move all of those joints in coordination, to a pretty high degree of precision and accuracy, and carefully control the force applied from the arm to objects in the real world so as to not break anything. For a human these tasks are intuitive. For a robot they can be complex to model. When programming Spot Micro, to acheive complicated motion like walking, sitting, and standing, I used code that Mike4192 published that implements kinematic modelling to command the robot in space and solve for these joint positions.    

### Presentation Plan
We'll talk about the project and it's phases for me; we'll talk about the software and Robot Operating System (ROS); and then we'll talk about inverse kinematic models and how to coordinate movement across multiple joints.

### Project Phases
1. Planning Electronics
2. Gather Electonrics
3. 3d Print Parts
4. Assembly hardware
5. Integrate Software

### Links to Resources
[Homepage for SpotMicro Community](https://spotmicroai.readthedocs.io/en/latest/). This has links to various 3d modelling files, instructions on one version of software, and links to other resources.  
[Slack for SpotMicro Community](https://spotmicroai-inviter.herokuapp.com/). Lots of builders hang out here and are generally quite helpful in answering questions and giving tips.  
[Repo I used for software](https://github.com/mike4192/spotMicro). There are many different code repositories with different approaches to programming SpotMicro. I chose to use this one as it supported ROS and I liked the walking gait implemented. I contributed to this code repository as I was setting up my robot.  

### Timeline
August 2020  
* Thoroughly read documentation
* Planned Electronics
* Planned which 3d Models to Use
* Ordered 14 Servos from Bangood  

September 2020
* Banggood servo order delayed due to no supply, I cancelled in response
* Re-ordered servos from Aliexpress
* Miscellaneous other orders from Bangood, Aliexpress, and Amazon for other parts
* Started 3d Printing parts 
  * Printed Chasis
  * Printed some leg pieces (later realized they were misprinted, and had to re-print them)
* Assembled an Arduino-based Controller
* Gathered most of the other electronics (except Servos)

October 2020
* Received some servos. Order was half the servos I ordered, half another type of (cheaper) servos that didn't meet my specifications. Began negotiations with Aliexpress and Seller for refund
* Ordered 4 servos from a different Aliexpress seller, paying for fast shipping, expecting Aliexpress dispute process on other order to result in a partial refund
* Started to assemble legs, with the limited servos I had
* had initial hardware trouble with legs and ended up cutting one open to extract the servo. Learned to glue nuts in place so that they don't rotate with screw when extracating

November 2020
* Tested power system
* Continued with leg assembly
* Was able to do hardware tests with power
* Promptly broke a servo. Unfortunately I only had the exact number I needed, so I then needed to order more. Given the horror, I order some from Amazon and paid for shipping $$$
* Continued assembly and hardware testing
* 1st contribution to Mike4192's spotMicro repository 

December 2020
* Received Servos from Amazon
* Settled dispute with Aliexpress. Worked out as expected, but seller was of no hope, it was Aliexpress that helped
* Continued assembly, got to a point where could test with power again
* Sprinted through config and testing to meet Dec 31st goal of walking
* Tested a Lidar I received for Christmas, but in isolation, not with Spot Micro
* Acheived Goal  

### Planning the Electronics
Before you can buy parts, you have to decide what parts you need! This involved looking through various pieces of documentation [here,](https://spotmicroai.readthedocs.io/en/latest/gettingStarted/) and planning out my electronics.  
One big consideration is what servos to use. Deok-yeon Kim went with MG 996R servos to start with, but they and the community eventually realized these were underpowered and didn't have the torque required to let the robot stand. They observed shaking when the robot was standing, indicating motors couldn't produce the torque needed to keep the robot standing. An alternative proposed, that I settled on, were the PDI-HV5523MG. These have higher torque compared to MG 996R servos, so I expected better performance when standing and walking, and additionally they could run at higher voltages than 5V, namely 7.4V-8.4V, the voltage produced by a 2 cell Lipo battery. That made connecting it easier.  
Another big consideration was what Microprocessor to use. Various community members had used Jetson Nanos, Arduino Megas, and Raspberry Pi 3b+ in their builds. I settled on a Raspberry Pi 4 as I'd worked with Pi's before and knew the Pi 4 was a substantial upgrade in terms of ram and processing power to the 3b+. This also meant I could avoid doing a partition of the SD card to swap in wiht the limited ram on a 3b+ as some of the community had done.  


### Gathering the Parts

### Hardware (3d-printed Body)

### Hardware (Electronics)

### Software (OS)

### Software (Walking Algo)

### Lessons Learned

### Future Extensions

### Collaborate
