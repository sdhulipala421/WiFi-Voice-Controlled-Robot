# WiFi Voice Controlled Robot
This WiFi Voice Controlled Robot takes commands from a NodeMCU to move the robot in a certain direction. The robot consists of four wheels, that are driven by 4 DC motors (LEFT and RIGHT motors) that allows for the robot to move forward, backward, left, right, and stop. The Voice Input by the user is translated from the Android device to move the robot. 

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Sindhu D | Monta Vista High School | Software Engineering | Incoming Senior

![Headstone Image](https://raw.githubusercontent.com/sdhulipala421/WiFi-Voice-Controlled-Robot/main/292570339_821212712598233_3879414798837582761_n.jpg)
  
# Final Milestone
My final milestone is the increased reliability and accuracy of my robot. I ameliorated the sagging and fixed the reliability of the finger. As discussed in my second milestone, the arm sags because of weight. I put in a block of wood at the base to hold up the upper arm; this has reverberating positive effects throughout the arm. I also realized that the forearm was getting disconnected from the elbow servo’s horn because of the weight stress on the joint. Now, I make sure to constantly tighten the screws at that joint. 

[![Final Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1612573869/video_to_markdown/images/youtube--F7M7imOVGug-c05b58ac6eb4c4700831b2b3070cd403.jpg )](https://www.youtube.com/watch?v=F7M7imOVGug&feature=emb_logo "Final Milestone"){:target="_blank" rel="noopener"}

# Second Milestone
My second milestone was building my entire robot body by attaching all four motors to the car chassis. I connected the front two motors to the H Bridge using alligator clips, and the back two motors using a technique of soldering. By soldering, I was able to connect the copper tabs of the DC motors to the jumper wire which inserted into the H Bridge. An obstacle I faced was when soldering my first motor, I ripped out a chunk of the copper tab which made it difficult to connect the copper tab to the jumper wire. Because of this, I had to re-solder the wire to a minimal piece of copper tab to connect it to the H Bridge. I also began on developing my app this week which includes 5 different functions: forward, reverse, left, right, and stop. These commands prompt the robot to move in all these designated directions. 

[![Second Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1656358939/video_to_markdown/images/youtube--oa6gBuU8fng-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/oa6gBuU8fng "Second Milestone")
# First Milestone
  

My first milestone was setting up the H Bridge by wiring all the components from the H Bridge to the Arduino, Battery Pack, and DC Motors. I began with using alligator clips which used jumper wires to connect the pinholes to the copper tabs of the DC motors. The Battery Pack included a black and a red wire, which connected to the ground and 12 volt of the H Bridge. While fitting the battery wires into the H Bridge, the wire was too thin to fit into the slot, so I had to manually strip the wire to ensure a tight fit. I also connected 4 male headed wires, a ground wire, and a 5 volt wire from the H Bridge to the Arduino. To code the motor commands, I used a digitalWrite function with a combination of high or low settings to prompt the motors to move forward, backward, left, right, and stop.  

[![First Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1655496026/video_to_markdown/images/youtube--5IGHZCkltac-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/5IGHZCkltac "First Milestone")

Code


