## Spot Micro Robot
This was a fun project where I 3d printed the robot, planned the hardware, assembled, and used a fellow robot builder's ROS Repo to get it walking. I contributed a bit to the robot builder's ROS repo as well. 
![spot_micro_demo](screenshots/spot_micro_demo.gif)    

### Intro
Take a moment and touch your left shoulder and then move your mouse to the top left of your computer screen. What parts of your body moved to accomplish that task? If you do it again slowly, did you move your wrist? Your elbow? Your shoulder? Your torso? I assume that most of us moved multiple body parts in coordination, and I'd also assume that the force applied with your body parts was carefully controlled and that nobody broke their laptop.    

Now imagine you were programming a robot to do this task. Assuming you had a robot arm that had the same joints as your human arm, you'd have to move all of those joints in coordination, to a pretty high degree of precision and accuracy, and carefully control the force applied from the arm to objects in the real world so as to not break anything. For a human these tasks are intuitive. For a robot they can be complex to model. When programming Spot Micro, to acheive complicated motion like walking, sitting, and standing, I used code that Mike4192 published that implements kinematic modelling to command the robot in space and solve for these joint positions.    

### Presentation Plan
We'll talk about:
* The project and it's phases for me. This was the biggest and most complex thing I'd built to date.
* The software and Robot Operating System (ROS).
* Inverse kinematic models and how to coordinate movement across multiple joints.

### Project Phases
1. Planning Electronics
2. Gather Electronics
3. 3d Print Parts
4. Assemble hardware
5. Integrate Software

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
* Acheived goal of walking 

### Planning the Electronics
Before you can buy parts, you have to decide what parts you need! This involved looking through various pieces of documentation [here,](https://spotmicroai.readthedocs.io/en/latest/gettingStarted/) and planning out my electronics.  
Here is an early plan of my electronics circuit, though I didn't use a breadboard in the final build due to space constraints.  
![electronics](screenshots/electronics_diagram.jpg)  

One big consideration is what servos to use. Deok-yeon Kim went with MG 996R servos to start with, but they and the community eventually realized these were underpowered and didn't have the torque required to let the robot stand. They observed shaking when the robot was standing, indicating motors couldn't produce the torque needed to keep the robot standing. An alternative proposed, that I settled on, were the PDI-HV5523MG. These have higher torque compared to MG 996R servos, so I expected better performance when standing and walking, and additionally they could run at higher voltages than 5V, namely 7.4V-8.4V, the voltage produced by a 2 cell Lipo battery. That made connecting it easier.  

Another big consideration is how to power the servos. The PCA9685 servo controller board I used could connect to the servos to power, but had a limit of 3 Amps or so. With 12 servos, if each servo consumed 1 amp (and they could consume up to 3 amps if stalled) I would be way over that limit. So, I connected servos directly to power which isn't advised. One addition would be a BMS to prevent overdrawing the lipo and make the whole circuit more safe.  

Another big consideration was what Microprocessor to use. Various community members had used Jetson Nanos, Arduino Megas, and Raspberry Pi 3b+ in their builds. I settled on a Raspberry Pi 4 as I'd worked with Pi's before and knew the Pi 4 was a substantial upgrade in terms of ram and processing power to the 3b+. This also meant I could avoid doing a partition of the SD card to swap in wiht the limited ram on a 3b+ as some of the community had done.  

One last consideration would be cable management. This picture looks quite chaotic, and I needed to think through how to simplify wiring both for safety reasons as well as ease of repair. Building this into my schema would probably have been a good idea instead of leaving this to the last minute.  

I asked for some feedback on this plan from members of the Spot Micro community and got some great feedback like how to do power management.  
![electronics_feedback](screenshots/feedback_electronics.PNG)  

I then planned a spreadsheet of all the parts I would need to buy, where to source them, and how much they would cost. The entire project cost about $800, give or take. Plus four months of my life, which you know, priceless :)  
![example_spreadsheet](screenshots/example_spreadsheet_plan.png)  

### Gathering the Parts
Seems like buying stuff should be the easiest step, simply hit add to cart and pay, but I actually had a lot of trouble with this step. Specifically with the servos.  

The servo motors are one of the most important parts of the build, as each leg needs 3 servos (shoulder, elbow, wrist), and they all need to operate well to acheive coordinated movement like walking. If you pay $13 per servo, and you buy 14 of them (to have 2 extra in case you break stuff, which I do a lot), that's $182 which is the most expensive component of this robot. I wanted very specific servos that could operate at a higher voltage (~7.4v-8v) and had higher torque (23kg/cm). Turns out a lot of other people wanted these at the same time, and they weren't easy to find.  

I started at bangood.com which is a site where you can buy from chinese suppliers cheaply. Shipping takes a couple weeks so I ordered early. Unfortunately a couple weeks into the order the date got pushed back to due to supply problems. This was the start of my trouble. I wasn't willing to wait an extra month or two, so I cancelled this order and moved to another supplier.  

I then ordered from Aliexpress, waiting a couple weeks for the servos to arrive, unpacked them, and realized with horror that I while I had received 12 servos, 6 of them were the wrong type of servo. 6 were cheaper, less powerful servos that I knew I couldn't use in the robot. Here you can see the horror:  
![servo_mixup](screenshots/ae_1602964513627.jpg)  

I then had to start the process with Aliexpress to get a refund which turned out to be complicated. Aliexpress has a dispute system, where they act as an arbiter between you the buyer, and the seller you bought from. Unfortunately my seller was useless to the point of trying to sabotage my dispute process. They recommended simply waiting for the dispute timer to run out, cancelling the dispute, and other things that would give them power and allow them to walk away without addressing my grievances. Also, Aliexpress didn't let me speak to a human for customer service. I tried a lot of things with their chat bot, but never got past it. Thankfully a couple months after starting the process, after the first dispute closed and I escalated it to re-open it and after I sent some servos back, I got the resolution I wanted (a partial refund).  

Here's the seller asking me to cancel the dispute, which would remove my sole avenue to address my grievances and allow them to walk away.  
![dispute](screenshots/seller_cancel_ask.PNG)  

And here's Eva, the chatbot who I spent hours pleading with to put me through to customer service. I like to think that she is blissfully unaware of the trauma she can cause.  
![eva](screenshots/eva.PNG)  

I ended up sourcing servos partially from another Aliexpress seller, partially from Amazon. In the future I would order big ticket items like 12 servos in batches from different sellers to help remediate the risk of issues like this occuring. I'd also take careful pictures of every box received and its contents as soon as they arrived in case, those pictures were needed in the dispute process. I'd also make sure I understood who pays for return shipping in case of a dispute before ordering.  

Thankfully the rest of the gathering electronics was rather uneventfull and I received what I ordered. I used Bangood, Aliexpress, and Amazon for all of the electronics.

### Hardware (3d-printed Body)
I sometimes get asked, "how easy is 3d Printing?" Variations of that could include "I broke my toy, can you 3d print me a part?"  

To address the first question: in my opinion 3d Printing is an amazing technology but it's not foolproof. It happens to me regularly, many months into using this technology, that my prints fail and I don't know why and have to research issues. With the printers at my office, that print ink on paper, every job I send to them works perfectly. Not so with my 3d Printer at home. So, to people looking to get into the hobby I say, "It's amazingly powerful to create and prototype. But, go into it with the mindset that stuff will break and you'll need to Google your way through and fix things on your printer."  

To address the second question, to 3d print something you first have to have a 3d model of it, then slice that into layers that the 3d printer will print, then convert that into GCODE to put on the printer, then print it. Of all these steps the first is by far the hardest. To create something to precisely the measurements you need, make it look nice, and then format it as a .stl file to slice requires lots of knowledge about 3d Modelling and Computer Aided Design. Then it requires a lot of time to build the 3d Model. That's something I didn't need for this project because amazing community members like Deok-yeon Kim created the design and community members then remodelled this and published the files in a different format that is easy to edit.  

Here's the 3d Model that I used from the community: 
![3d_model_spot](screenshots/3d_model_demo.png)  

I did make some changes to parts, and to show you how long this process of editing a 3d model, printing, and fixing any issues in the part you printed can take, see the below. This was me editing a part of the dog, a part that is a mounting plate for my electronics and goes inside of the dog. This was one of my first time editing files, and I had to do edit the model, print it out, test it, and repeat 6 times before I finally fixing all the issues. I was particularly sleep deprived that day and also learning a lot of new skills, but still it shows you what an iterative process it can be!  
![iterative_process](screenshots/20210417_133236.jpg)  

Once you have the model you open up a piece of it and slice it into layers using specialized software. This software will also generate the gcode for you.  

Here you can see me opening the piece of the model I want to print:
![part_to_print](screenshots/slicing_a_model.png)  

The software will slice it into layers for the 3d Printer and generate any support needed (as you can't print on air).  
![all_layers](screenshots/all_layers_slice.png)  

Behind the scenes it will generate the gcode for the printer, which is a set of instructions like move the nozzle to this xyz point and extrude this amount of plastic. Here I'm highlighting one of the first lines where it sends to head of the printer to the bottom left corner, "homing it". Then I'm highlighting one section where the print starts which is a series of commands to move the nozzle and extrude plastic. That later section basically says go to 79X and 56Y and extrude to the .18mm fillament point.  
![gcode](screenshots/g_code_example_2.png)  

The head of the printer will move around during the print printing:  
![3d_print_movement](screenshots/3d_printing_part.gif)  

And the end result is somewhat magical, of the piece rising up layer by layer:  
![3d_print_timelapse](screenshots/3d_printing_timelapse.gif)  

You can imagine how rotating a part and printing it on its side could change how the layers would be construct and the print would work faster or slower. There are more efficient ways to print some parts by rotating, laying it flat, changing supports, ect. So, the community was also very helpful in guiding me towards efficient ways to print:  
![feedback_printing](screenshots/feedback_printing.PNG)  

### Hardware (Electronics)

### Software (OS)

### Software (Walking Algo)

### Lessons Learned

### Future Extensions

### Collaborate

### Links to Resources
[Homepage for SpotMicro Community](https://spotmicroai.readthedocs.io/en/latest/). This has links to various 3d modelling files, instructions on one version of software, and links to other resources.  
[Homepage for SpotMicro Community Collect Parts Page](https://spotmicroai.readthedocs.io/en/latest/gettingStarted/). This has a rough list of parts, though isn't comprehensive and some stuff is outdated like the choice of servos.  
[Homepage for SpotMicro Community](https://spotmicroai.readthedocs.io/en/latest/). This has links to various 3d modelling files, instructions on one version of software, and links to other resources.  
[Slack for SpotMicro Community](https://spotmicroai-inviter.herokuapp.com/). Lots of builders hang out here and are generally quite helpful in answering questions and giving tips.  
[Repo I used for software](https://github.com/mike4192/spotMicro). There are many different code repositories with different approaches to programming SpotMicro. I chose to use this one as it supported ROS and I liked the walking gait implemented. I contributed to this code repository as I was setting up my robot.  
[Slack for SpotMicro Community](https://spotmicroai-inviter.herokuapp.com/). Lots of builders hang out here and are generally quite helpful in answering questions and giving tips.  
[Repo I used for software](https://github.com/mike4192/spotMicro). There are many different code repositories with different approaches to programming SpotMicro. I chose to use this one as it supported ROS and I liked the walking gait implemented. I contributed to this code repository as I was setting up my robot.  

