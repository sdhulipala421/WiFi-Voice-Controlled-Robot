# WiFi Voice Controlled Robot
This WiFi Voice Controlled Robot takes commands from a NodeMCU to move the robot in a certain direction. The robot consists of four wheels, that are driven by 4 DC motors (LEFT and RIGHT motors) that allows for the robot to move forward, backward, left, right, and stop. The Voice Input by the user is translated from the Android device to move the robot. 

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Sindhu D | Monta Vista High School | Software Engineering | Incoming Senior

![Headstone Image](https://raw.githubusercontent.com/sdhulipala421/WiFi-Voice-Controlled-Robot/main/Screen%20Shot%202022-07-09%20at%203.23.54%20AM.png)

![Parts Info](https://raw.githubusercontent.com/sdhulipala421/WiFi-Voice-Controlled-Robot/main/Screen%20Shot%202022-07-09%20at%203.14.59%20AM.png)
  
# Final Milestone
My final milestone involved completing the voice control app and connecting it to my robot using an IP address. The app contains 5 block tabs which are programmed to function in a 3 step process: sending a command, creating an "echo" to the user, and outputing a sound from the android device. Some challenges I faced were that the robot was not receiving enough power from the battery pack, so I had to debug some hardware and identify the issue which was the ground and 12 volt wire were disconnecting often from the H Bridge. Once I was able to tighten the connection and connect it to my app, the robot began to work in full function. 

[![Final Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1657362025/video_to_markdown/images/youtube--nS1Xyf7iYL4-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/nS1Xyf7iYL4 "Final Milestone")

# Second Milestone
My second milestone was building my entire robot body by attaching all four motors to the car chassis. I connected the front two motors to the H Bridge using alligator clips, and the back two motors using a technique of soldering. By soldering, I was able to connect the copper tabs of the DC motors to the jumper wire which inserted into the H Bridge. An obstacle I faced was when soldering my first motor, I ripped out a chunk of the copper tab which made it difficult to connect the copper tab to the jumper wire. Because of this, I had to re-solder the wire to a minimal piece of copper tab to connect it to the H Bridge. I also began on developing my app this week which includes 5 different functions: forward, reverse, left, right, and stop. These commands prompt the robot to move in all these designated directions. 

[![Second Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1656358939/video_to_markdown/images/youtube--oa6gBuU8fng-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/oa6gBuU8fng "Second Milestone")
# First Milestone
  

My first milestone was setting up the H Bridge by wiring all the components from the H Bridge to the Arduino, Battery Pack, and DC Motors. I began with using alligator clips which used jumper wires to connect the pinholes to the copper tabs of the DC motors. The Battery Pack included a black and a red wire, which connected to the ground and 12 volt of the H Bridge. While fitting the battery wires into the H Bridge, the wire was too thin to fit into the slot, so I had to manually strip the wire to ensure a tight fit. I also connected 4 male headed wires, a ground wire, and a 5 volt wire from the H Bridge to the Arduino. To code the motor commands, I used a digitalWrite function with a combination of high or low settings to prompt the motors to move forward, backward, left, right, and stop.  

[![First Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1655496026/video_to_markdown/images/youtube--5IGHZCkltac-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/5IGHZCkltac "First Milestone")

## Code
'''cpp
<#include <WiFi.h>
WiFiClient client;
WiFiServer server(80);
const char* ssid = "Srinilayam";
const char* password = "niftyocean378";
String  command = "";
int LEDPin = 10;
int readValue = 0;
int LEDValue = 0;
int rightMotor2 = 13;
int rightMotor1 = 12;
int leftMotor2 = 25;
int leftMotor1 = 26;

void setup()
{
  Serial.begin(115200);
  pinMode(leftMotor1, OUTPUT);
  pinMode(leftMotor2, OUTPUT);
  pinMode(rightMotor1, OUTPUT);
  pinMode(rightMotor2, OUTPUT);


  digitalWrite(leftMotor1, LOW);
  digitalWrite(leftMotor2, LOW);
  digitalWrite(rightMotor1, LOW);
  digitalWrite(rightMotor2, LOW);

  connectWiFi();
  server.begin();
}

void loop()
{
  client = server.available();
  if (!client) return;
  command = checkClient();

  if (command == "forward" || command == "frente" || command == "a frente")  forwardMotor();
  else if (command == "reverse" || command == "reverso" || command == "voltar") reverseMotor();
  else if (command == "left"    || command == "esquerda") leftMotor();
  else if (command == "right"   || command == "direita") rightMotor();
  else if (command == "stop"    || command == "pare" || command == "parar" || command == "parando")     stopMotor();

  sendBackEcho(command); // send command echo back to android device
  command = "";
}

/* command motor forward */
void forwardMotor(void)
{

  digitalWrite(leftMotor1, HIGH);
  digitalWrite(leftMotor2, LOW);
  digitalWrite(rightMotor1, HIGH);
  digitalWrite(rightMotor2, LOW);
}

/* command motor backward */
void reverseMotor(void)
{

  digitalWrite(leftMotor1, LOW);
  digitalWrite(leftMotor2, HIGH);
  digitalWrite(rightMotor1, LOW);
  digitalWrite(rightMotor2, HIGH);
}

/* command motor turn left */
void leftMotor(void)
{

  digitalWrite(leftMotor1, LOW);
  digitalWrite(leftMotor2, HIGH);
  digitalWrite(rightMotor1, HIGH);
  digitalWrite(rightMotor2, LOW);
}

/* command motor turn right */
void rightMotor(void)
{

  digitalWrite(leftMotor1, HIGH);
  digitalWrite(leftMotor2, LOW);
  digitalWrite(rightMotor1, LOW);
  digitalWrite(rightMotor2, HIGH);
}

/* command motor stop */
void stopMotor(void)
{
  /*digitalWrite(eneLeftMotor,LOW);*/
  /* digitalWrite(eneRightMotor,LOW);*/

  digitalWrite(leftMotor1, LOW);
  digitalWrite(leftMotor2, LOW);
  digitalWrite(rightMotor1, LOW);
  digitalWrite(rightMotor2, LOW);
}

/* connecting WiFi */
void connectWiFi()
{
  Serial.println("Connecting to WIFI");
  WiFi.begin(ssid, password);
  while ((!(WiFi.status() == WL_CONNECTED)))
  {
    delay(300);
    Serial.print("..");
  }
  Serial.println("");
  Serial.println("WiFi connected");
  Serial.println("NodeMCU Local IP is : ");
  Serial.print((WiFi.localIP()));
}

/* check command received from Android Device */
String checkClient (void)
{
  while (!client.available()) delay(1);
  String request = client.readStringUntil('\r');
  request.remove(0, 5);
  request.remove(request.length() - 9, 9);
  return request;
}

/* send command echo back to android device */
void sendBackEcho(String echo)
{
  client.println("HTTP/1.1 200 OK");
  client.println("Content-Type: text/html");
  client.println("");
  client.println("<!DOCTYPE HTML>");
  client.println("<html>");
  client.println(echo);
  client.println("</html>");
  client.stop();
  delay(1);
}>
'''



