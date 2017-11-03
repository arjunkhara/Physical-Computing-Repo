# arduino
My physical computing and arduino projects

I’m Arjun. This is my weekly blog for the Physical Computing Module for my MA at Goldsmiths (2017 – 2018). I built this site to document my work, learnings, and insights on a weekly basis spanning this module’s duration. This repository also serves as a learning portal to question and experiment beyond the scope of what the module asks, in order to gain the deepest possible appreciation of physical computing and its evolving role as a companion in our digitally nebulous societies. Once completed, I hope to leave this blog as an active reference for future students of the subject.

Topics 1 through 4 introduce students to the Arduino platform — a circuit board with a micro-controller, capable of integration with both software and hardware. In this respect, the Arduino is a driver of the Internet of Things (IOT), an ecosystem in which connectivity and data-driven decisions extend to physical devices and multi-material computing components. The seemingly simple ability of the board to react to sensors and activate actuators provides an almost limitless array of possibilities across industries, from performance and art to bio-medical and communication applications. In other words, the Arduino is a tangible ambassador of the digital humanities — the confluence of technology, philosophy, form, and function.

<h1>Topic 1</h1>

I began by using the Arduino IDE (desktop version) but after some research found the web version much easier to use, with the added benefits that cloud provides. The link to Arduino’s web editor and playground can be accessed here [+]. It is interesting to think of Arduino, first, as a simple interface for power despite its ability to convey much more. The topic requires wiring the board to an LED with a switch and a resistor, and powering the circuit with a USB cable via a computer. The project was a success, and given the relative simplicity of the task, I decided to experiment with more than one LED. The purpose was to satisfy my curiosity and the inclusion of an additional LED was easy to accomplish. That, however, led to an idea of a simple game of quick click — a test of reflexes. I added another LED, resistor and switch circuit to the board and within a few minutes had a classic reflect game of red versus blue. The switches were placed on either side of the board for both players to quickly close their circuit in order to light up their respective LED.

I considered doing a version where if one player clicked, the other’s circuit would break. At this point I started considering resource allocation, given the size and power of the board and its components. With this in mind, I rewired my circuits to accomplish the same effect, i.e. whoever presses late stands out, but with a single blue LED and two switches. The faster player’s response triggers the LED to come on. The slower player is indicated by a brightening of the LED to indicate an action. The game design is simple but the principles of play coupled with this nascent insight into resource management will, I suspect, be of immense use in later projects.

It was natural, with all the flashing LEDs, to notice the board itself had light indicators built-in. After some research online I found a tutorial, <a href="https://www.youtube.com/watch?v=fCxzA9_kg6s" target="_blank">accessible here [+]</a>, on how to manipulate the light on the board itself via pin 13. The process was, in many ways, the complete opposite to the requirements of topic 1, since topic 1 required pure hardware to make lights blink. This additional exercise required pure software, other than the board itself. This experiment is also my first sketch with Arduino and an exciting introduction into the confluence of software and hardware that is physical computing. The video and code for this sketch is below.
https://youtu.be/ygo-j65H6bQ
<pre><code>
/* Topic 1 Beyond: Experiment with Native Pin 13 Flashing LED */
/* This is my first custom-built programme (learned with Jeremy Blum from YouTube) */

int ledPin = 13; //initialises (or targets) Pin 13 on the Arduino Board itself
void setup() {
    pinMode (ledPin, OUTPUT);
}
void loop() {
    digitalWrite(ledPin, HIGH);
    delay(500); //adjust this value for variety
    digitalWrite(ledPin, LOW);
    delay(1000); //adjust this value for variety
}
</code></pre>

A final word on transducers, sensors and actuators. The Arduino projects book explained how the board listens to sensors and talks to actuators, which is an interesting description of how physical computing works. In attempting to further understand the mechanics and management of physical computing, I recalled watching a video on the nature and nurturing processes of physical computing given by Professor Neil Gershenfeld (MIT) on how to make almost anything [+]. I can therefore surmise that the applications of this field are indeed virtually limitless, and suddenly this little blue board started to seem a little more inspiring and promising.



<h1>Topic 2</h1>

Topic 2 focused on blinking LEDs to create a spaceship like effect. The project required wiring three LEDs to the breadboard then using code from the Arduino IDE to control how the LEDs flashed. The task required that the green LED remained on but when the switch was pressed, the green LED would turn off (go low) while the additional two red LEDs would start to blink in sequence. The task was a success so I proceeded to complete optional challenge in the book, which was to see if the effect could be reversed. This was accomplished by switching around the if/else code blocks. As I am somewhat familiar with JavaScript and its corresponding conditional statements in programming, this process made sense and I was also able to complete the optional challenge.

Building on the previous topic’s tasks and from the videos and books I had accessed so far, I wanted to experiment with fades rather than harsh blinking. Since this was to be a spaceship-style project, the idea of having fading lights rather than blinking ones was appealing. I read further on the topic of pulse-width modulation (PWM) and attempted to create a scenario in which the lights faded on and off. The code required the inclusion of analogWrite, a command that appears in the book’s more advanced sections. However, understanding and applying the principles to this project was not as abstruse as I first suspected and with more help from online tutorials and a book called ‘Exploring Arduino’ by Jeremy Blum I was able to figure out how PWM worked and its applications to my intention of creating a fading effect.

The snippet below contains the complete code for the PWM (fade-in / fade-out) effect on the green LED, set at 100 milliseconds. Change the delay value from 100 to any integer you desire. The source code for this project is also available here [+]. The video and code for this sketch is below.
https://youtu.be/doQ4acDMMeI

<pre><code>
/* Topic 2 Beyond: Experiment with PWM and Fading Effect */
int switchState = 0;
int led = 3;           // the PWM pin the LED is attached to (i.e the green LED)
int brightness = 0;    // how bright the LED is
int fadeAmount = 5;    // how many points to fade the LED by


void setup() {
  // put your setup code here, to run once:
pinMode(3,OUTPUT);
pinMode(4,OUTPUT);
pinMode(5,OUTPUT);
pinMode(2,INPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
   analogWrite(led, brightness);

  // change the brightness for next time through the loop:
  brightness = brightness + fadeAmount;

  // reverse the direction of the fading at the ends of the fade:
  if (brightness <= 0 || brightness >= 255) {
    fadeAmount = -fadeAmount;
  }
  // wait for 30 milliseconds to see the dimming effect
  delay(30);
  
switchState = digitalRead(2);
if (switchState == LOW) {
  digitalWrite(3, HIGH); //the green LED
  digitalWrite(4, LOW); //the first red LED
  digitalWrite(5, LOW); //the second red LED

} 
else {
  digitalWrite(3, LOW); //the green LED
  digitalWrite(4, LOW); //the first red LED
  digitalWrite(5, HIGH); //the second red LED

  delay(250);
  digitalWrite(4, HIGH); //the first red LED
  digitalWrite(5, LOW); //the second red LED
  delay(250);
}
}
</code></pre>

Topic 2 introduces the PWM function which is essentially the Arduino turning on and off the LED extremely quickly to produce a square wave that emulates the properties of the sine wave of electric current and PWM synchronocity. In future projects I believe the PWM function will be essential to emulating, if not also controlling, the circuit properties and attached transducer components.


<h1>Topic 3</h1>

Topic 3 focuses on creating a love-o-meter, which is essentially an introduction to sensors — in this case for temperature. The objective is to build a sensor that measures body temperature vis-a-vis ambient air temperature. Then, using the differences in voltage due to thermodynamic fluctuation, a score is given as indicated by the number of LEDs that light up. Higher the temperature, the more LEDs light up.

This initial introduction to sensor technology was fascinating. I was able to wire up the circuit with some difficulty given the number of parts and regard for the temperature sensor’s orientation (the curved head has to face away from the board). The variable voltage pin (the middle leg on the temperature sensor) is plugged directly into an analog pin on the Arduino.

The task worked fine. Owing to my room being heated the temperatures registered accurately around 26°C and fluctuated to about 27.73°C upon moving my fingers close to the sensor. I was able to make two LED pins light up by placing my fingers on and around the temperature sensor, thus rendering me a somewhat promising candidate for love, but not quite the hottie. More importantly, this project was also an introduction to the serial monitor, which, from what I am able to extrapolate, is similar in function to the console.log command used in JavaScript for websites. The serial monitor provides real-time readings of the voltage differences due to temperature fluctuations. This voltage is converted to temperature via a simple equation provided in the project book.

I was interested in why the sensor value is between 0 and 1023 (making a total of 1024 point values, or the equivalent of bytes to 1 Kilobyte, kilobytes to 1 megabyte, megabytes to 1 gigabyte and so on). Upon conducting further searches in Arduino’s community forum [+] and on Arduino Stackexchange [+] I discovered that 1023 is the maximum possible value of a 10-bit unassigned integer. Since the index count starts from 0, not 1, 1023 represents the entirety of 1024. There is also some debate on whether the divisor value for the conversion formula should be 1023 or 1024, since both provide nearly similar answers but for specificity purposes, 1024 as the divisor makes for a more accurate conversion reading. Interestingly, the formula in the book states a divisor of 1024, yet when applied to the equation sensorVal * 5 / 1023 provides a more accurate estimation of the 5V, which is what the Arduino power supply is purported to be. However, the incremental difference between 1023 and 1024 accounts for approximately 0.1% difference, and in practice the board will approximate 5V though this will never be accurately achieved — more like 4.995V. I nonetheless felt it was important to note such details, minute though the values are, especially when starting off in a new field.

I was therefore able to accomplish the task, and then turned to a new problem that I was pondering — how hot could the sensor really get before it skewed its values.

I read up on the tutorial section on the official Arduino website which details calibrating sensor input [+] with five-second measurements and analog sensors, and will be applying this to future projects. At this stage, I re-wired the board to pass the current directly through the sensors (please see the video above) and reloaded the sketch into the board. Within a minute, the temperature readings on the serial monitor were reaching 247 °C. At this point an LED shorted, whereupon I unplugged the USB cable. For the sake of safety I have not included this circuit’s diagram. Nonetheless the findings from this experiment are incredibly useful to me for future projects since it is evident that the sensor and the board are able to withstand boiling point temperatures and still function normally for a reasonable duration. Apart from the LED, both the temperature sensor and the Arduino board were in perfect state and when I repeated the task from the book the values registered normally.

I also considered the optional challenge to determine an interface that best determines compatibility. Given the current limitations of this task so far, my recommendation would be a simple matter of two people blowing on the sensor at the same time to see which couple can provide maximum heat levels possible.

At this point I noted that all the projects so far had been using light as an indicator, and so I began to think about using sound instead. However, I lacked the necessary equipment — a microphone, which I will acquire soon. As a side project I intend to replace the LEDs with the microphone and, with some help from Henry’s Bench Online Tutorial on Sound with Arduino [+], will set up the project to test temperature variances and indicate the differences in voltage through sound. I am hoping this future project will highlight another important step to understanding physical computing. The use of all of our senses, not just sight, to enrich creative experiences and, among its myriad uses, provide the critical element of accessibility across a wider spectrum of users.

Needless to say I am confident this foray into sound-based actuators (instead of just light) will be a welcome addition to my slowly-growing repertoire in physical computing. I am also compelled to say that I am now thoroughly enjoying this module, not just for its academic value but also its practical applications which open up a world of creative ideas. The link to the video and code is below.
https://youtu.be/iJo9BfdIr7o

<pre><code>
/* Topic 3: Introduction to Serial Monitors */

const int sensorPin = A0;
const float baselineTemp = 17.0;

void setup() {
Serial.begin(9600); //serial port with baud rate set
for(int pinNumber = 2; pinNumber<5; pinNumber++){
  pinMode(pinNumber,OUTPUT);
  digitalWrite(pinNumber, LOW);
  //above for loop similar to Javascript for and while loops
}
}

void loop() {
    int sensorVal = analogRead(sensorPin);
    Serial.print("Sensor Value: ");
    Serial.print(sensorVal);
    float voltage = (sensorVal/1024.0) * 5.0;
    Serial.print(", Volts: ");
    Serial.print(voltage);
    Serial.print(", degrees C: ");
    float temperature = (voltage - .5) * 100;
    Serial.println(temperature);
    
    if(temperature < baselineTemp){
      digitalWrite(2, LOW);
      digitalWrite(3, LOW);
      digitalWrite(4, LOW);
    } else if (temperature >= baselineTemp+2 && temperature < baselineTemp+4){
      digitalWrite(2, HIGH);
      digitalWrite(3, LOW);
      digitalWrite(4, LOW);
    }else if (temperature >= baselineTemp+4 && temperature < baselineTemp+6){
      digitalWrite(2, HIGH);
      digitalWrite(3, HIGH);
      digitalWrite(4, LOW);
    }else if (temperature >= baselineTemp+6){
      digitalWrite(2, HIGH);
      digitalWrite(3, HIGH);
      digitalWrite(4, HIGH);
    }
    delay(1);
}
</code></pre>


<h1>Topic 4</h1>

Topic 4 covers the fundamentals of a colour mixing lamp — the common cathode RGB LED, and introduces the use of photo resistors with red, green, and blue coloured strips. The requirements of the task are to make the LED change colour depending on how much light one or more of the three photo resistors receive along their respective wavelengths of colour (provided by the strips). The project can be conducted in a darkened room or by simply covering the resistors with an object. The LED changes colour accordingly, thus acting as a gauge for the amount of light passing through each of the photo resistors.

The code for this project (the longest yet) builds on past topics and integrates the serial monitor to display readouts of the change in voltage as the amount of light is varied. This project was a success and I was able to accomplish the tasks set in the book. The additional challenge asks what possible uses this type of system could be used for, and how, for example, this setup might provide an indication of the weather. I am able to see that this setup might work well for sky changes — overcast versus sunny, but would not be optimum for weather types involving precipitation — rain, snow, hail etc. I am confident, though, that future projects in this book and through other channels will involve greater specificity for such goals.

Upon completing the basic task, I wondered at how temperature (from topic 3) might affect the LED and if I could either devise or find or customise such an experiment in which the coloured LED would change depending on how hot the temperature got. I found a similar reference in ‘Exploring Arduino’ by Jeremy Blum and in ‘Arduino Programming’ by Mark Torvalds. I chose ‘Exploring Arduino’, which provides only the basic code base and does not include any details on the crucial serial monitor, which I would need for such an experiment. But drawing from topic 3’s learnings, I was able to extrapolate the code to create my own custom variables and serial log through which I would be able to measure the temperature that corresponded with the type of light — blue for cool, red for warm, and green for optimum. The following code snippet is a result of this customisation and extrapolation. Here is the link to the video demo for this topic: https://youtu.be/JRQLpgBBIS8

<pre><code>
/* Topic 4 Beyond: Experiment with LED and temperature sensor setup (custom project combining topics 3 and 4) */
/* Special thanks to Jeremy Blum, author, Exploring Arduino, for the tutorial on the basics for this project. */
/* Code for serial monitor and custom vals from extrapolation of past learnings, Arduino Projects Topics 1 - 3 */

const int blueLED = 9;
const int greenLED = 10;
const int redLED = 11;
const int sensorPin = A0;
const float baselineTemp = 17.0;

const int LOWER_BOUND = 156;
const int UPPER_BOUND = 163;

int sensorVal = 0;

void setup() {
  Serial.begin(9600); //serial port with baud rate set
for(int pinNumber = 9; pinNumber<12; pinNumber++){
  pinMode(pinNumber,OUTPUT);
  digitalWrite(pinNumber, LOW);
  //above for loop similar to Javascript for and while loops
}
  
    pinMode (blueLED, OUTPUT);
    pinMode (greenLED, OUTPUT);
    pinMode (redLED, OUTPUT);
}

void loop() {
   int sensorVal = analogRead(sensorPin);
    Serial.print("Sensor Value: ");
    Serial.print(sensorVal);
    float voltage = (sensorVal/1024.0) * 5.0;
    Serial.print(", Volts: ");
    Serial.print(voltage);
    Serial.print(", degrees C: ");
    float temperature = (voltage - .5) * 100;
    Serial.println(temperature);
    
    //begin conditional statement
    
    if(sensorVal < LOWER_BOUND) {
      digitalWrite (redLED, LOW);
      digitalWrite (greenLED, HIGH);
      digitalWrite (blueLED, LOW);
    } else if (sensorVal > UPPER_BOUND){
      digitalWrite (redLED, HIGH);
      digitalWrite (greenLED, LOW);
      digitalWrite (blueLED, LOW);
    } else {
      digitalWrite (redLED, LOW);
      digitalWrite (greenLED, LOW);
      digitalWrite (blueLED, HIGH);
    }
}
</code></pre>

It is interesting to note that the temperature sensor can be outputted through a variety of experiences — light, sound, sequencing, monitor output etc. This has made me think about the possibilities of experimental outputs as performance items themselves, for example publishing in real-time to a web server the readouts from several serial monitors performing the same experiment and highlighting minute differences as a black and white collage. Once again the real takeaway from all these basic tasks and additional experimentation is the possibilities that open up once physical computing integrates with natural environments. In fact it is already difficult to define where a natural environment ends and a computational system begins.

Whatever the case, I believe this is a path from which there is no return, and I for one am excited about that. The next step is most likely to acquire a second Arduino kit and experiment with dual-level circuitry. This week has been exciting to say the least and I am thoroughly enjoying physical computing as both a practical hands-on process as well as a philosophical avenue into understanding the human condition. Here is the link to the image of this topic's circuit diagram: https://github.com/arjunkhara/physical-computing-repo/blob/master/topic-4-beyond-circuitry.png


Here are the references and bibliography for the first four topics of Physical Computing. These are useful sources which I have consulted during my first week of learning Physical Computing.

• Adafruit – Using a Temp Sensor, Adafruit (2017) on Adafruit Website (accessed October 2017) at https://learn.adafruit.com/tmp36-temperature-sensor/using-a-temp-sensor

• Arduino Community Forum, Arduino (2017) on Arduino Website (accessed October 2017) at https://forum.arduino.cc/index.php?topic=353524.0

• Arduino Stackexchange, Stack Exchange (2017) on Stack Exchange Website (accessed October 2017) at https://arduino.stackexchange.com/questions/1667/significance-of-the-numbers-used-in-the-manual

• Arduino Tutorials, Arduino (2017) on Arduino Website (accessed October 2017) at www.arduino.cc

• Exploring Arduino: Tools and Techniques for Engineering Wizardry, Blum, J. (2013), Indiana:John Wiley & Sons

• Getting Acquainted With Arduino Tutorial 1, Jeremy Blum (2011), on YouTube (accessed October 2017) at https://www.youtube.com/watch?v=fCxzA9_kg6s

• Henry’s Bench Arduino Tutorials, Henry’s Bench (2016) on Henry’s Bench Website (accessed October 2017) at http://henrysbench.capnfatz.com/

• How To Make (Almost) Anything, Niels Gershenfeld (2014), on YouTube (accessed October 2017) at https://www.youtube.com/watch?v=FVOHo9YFuyg

• Practical Electronics for Inventors (4th Edition), Scherz, P. and Monk, S. (2016), New York:McGraw-Hill Education

<h1>Topic 5</h1>

Topic 5 introduces, among other elements, two major components of Arduino: calling native libraries for software, and the mechanisms and functions of the servo motor for hardware. The project was to build a mood meter by manipulating a potentiometer, which in turn affected the servo motor. As the book and external tutorials explain (please see reference and bibliography for titles) the servo motor only completes a 180 degree turn cycle. I learned that servo motors are made up of a small DC motor and controlled through PWM. The servo motor is in fact a highly efficient system, using just enough energy to get from its current position to its desired position. That means the servo motor only has to work as hard as the distance it needs to travel across. The potentiometer basically acts as a resistor to vary the voltage flowing into the servo. When a servo motor reaches its end position i.e. either 0 degrees or 180 degrees, it typically cuts the current flowing through it causing it to stop, and/or has in-built gear mechanisms to stop further motion. This stop is done for a definite purpose. There are also AC servo motors, typically used in ecosystems with higher currents – mainly for large-scale industrial use. Because servo motors convert rotary motion to linear output, they are extremely useful for radar sensing and sweep sensing over a 180 degree arc, though from further research online, the optimum arc is 120 degrees.

A possible final project could be building a device that recognises the colour of different marbles, and the servo motor spins as far as needed to point to the corresponding coloured dish in which the mechanism can dispense that marble. This colour sorter could be very interesting using sensors and actuators that we have already learned so far in this module. Coupled with future tutorials on laser cutting and moulding, a rig of the sorter can be designed and prototyped by weeks 6 through 8.

Such a project, I speculate, would require a sorting mechanism made up of a claw attached to a servo motor. A camera using RGB tricolour sensors could pick up the frequency of the coloured marble emitted and match that value range to the corresponding colour in the code. The code could then execute to move the servo motor as far as needed along a pre-programmed rotary route – the dispense position. When the servo motor reaches its desired position it will stop and the claw after a few seconds delay can release the ball into its corresponding colour, thus creating an efficient colour sorting machine.
<pre><code>
/*
 Arduino Week 2 Project 5
 */
 
#include <Servo.h>
Servo myServo;
int const potPin = A0;
int potVal;
int angle; 

void setup() {
  myServo.attach(9);
 Serial.begin(9600); 
}

void loop() {
 potVal = analogRead(potPin);
 Serial.print("potVal: ");
 Serial.print(potVal);
 angle = map(potVal, 0, 1023, 0, 179);
 Serial.print(", angle: ");
 Serial.println(angle);
 myServo.write(angle);
 delay(15);
}

</code></pre>

Here is the link to the video for this topic: https://youtu.be/L4PMdpOmEG8

<h1>Topic 6</h1>

Topic 6 focuses on using a photo resistor to vary the amount of voltage, and outputting the changes through a piezo. The setup was quite straightforward and the results were good. This was our first project with sound as a significant component of an intelligent circuit. The applications for such a mechanism are indeed countless, from a weather monitoring station that buzzes when the sky is overcast, to an alarm clock that sounds when the room is light enough – something that was easy enough to replicate by simply switching the code around so that when more light fell on the photo resistor the more the piezo sounded.

I found out (referenced below) that a piezo aggregates charge in a solid material as a result of a strain applied across a circuit. Interestingly, several piezos can be stacked like pizzas to create a piezo stack or piezo assembly. These stacks can act as delivery systems in diesel engines or drilling equipment. The standard microphone and the quartz watch mechanism also uses piezoelectricity to keep time through oscillation.

Piezoelectricity can also be generated simply by walking. When a piezo stack is installed in a shoe or piece of footwear, the motion and contact of the shoe with the ground and up again causes a charge to accumulate within the piezo, thus generating free electricity, albeit in relatively tiny quantities. However, the applications of such technology are far-reaching. It is also interesting to note that the sound produced by the piezo is the result of creating an imbalance in the particles / crystals / material that results in a force of charges, which induces the flow of electricity. The device used in this task is therefore known as a piezo transducer – a vehicle to facilitate piezoelectric charges. The term piezoelectricity comes from the Greek word piezein which literally means to press. Here is the link to the video of this demo: https://youtu.be/bN5AUppz_tg

And here is the code base for this project:
<pre><code>
/*
 Arduino Week 2 Project 6
 */

/*
This is the theremin and piezo circuit code with light detection as an alternative to capacitance
*/
int sensorValue;
int sensorLow = 1023;
int sensorHigh = 0;
const int ledPin = 13;
void setup() {
pinMode(ledPin, OUTPUT);
digitalWrite(ledPin, HIGH);
/* The while loop */
while (millis() < 5000) {
  sensorValue = analogRead(A0);
 if (sensorValue > sensorHigh) {
 sensorHigh = sensorValue;
 }
 if (sensorValue < sensorLow) {
 sensorLow = sensorValue;
 }
 }
 digitalWrite(ledPin, LOW);
}

void loop() {
  sensorValue = analogRead(A0);
  int pitch = map(sensorValue,sensorLow,sensorHigh, 50, 4000);
  tone(8,pitch,20);
  delay(10);
}
</code></pre>

<h1>Topic 7</h1>
Topic 7 built on the learnings of past week’s topics as well as topic 6 to create a rudimentary piano with four switches, connected in parallel. The switches controlled the current passing through and the voltage was mapped to a set of tones that the Arduino was programmed to emit via the piezo. The setup was straightforward and the result was a success. I was particularly interested in how the frequency of notes related to the sound produced and quickly realised that – within the limitations of the Arduino’s power output (5V) and the space on the breadboard, an entire piano layout could be constructed. But given resource limitations, I decided to use go beyond the basic task required – now that I was more familiar with sound through the Arduino -and decided to reprogram the keys to different frequencies using a conversion chart that can be accessed here: https://sites.google.com/a/bvsd.org/smith-multimedia/programming-arduino

By varying the note frequency I was able to compose the rudimentary theme of the Imperial March from Star Wars – a dream for Star Wars fans and a necessary rite of passage for Arduino beginners. The most interesting thing about going beyond the required scope of the task, was the discovery that virtually any sound scale, including the pentatonic scale, can be mapped to the switches and pre-programmed to output that particular note. With more space and more power, one may actually build an entire 88-key piano. This of course is one of several applications, and this particular task drove me to further research sound through Arduino – now a firmly embedded player in my physical computing environment. I have to add I thoroughly enjoyed this project and have included the resources I consulted in the references and bibliography section below. I am planning to use this for the next project, if feasible.

It must be noted that the code provided in the book for this task resulted in an error, which, I am happy to say, I was able to circumnavigate on my own through some trial and error. Basically the error resulted from the int buttons coming up as undefined and so the code block could not execute. I read through the rest of the code and realised that the declaration was redundant any way since the code ran independent of these declarations, given the runtime order was already enclosed in the void loop section of the code. Also, to add more impact to this task, it is easy to connect LEDs to each switch so that when the switch is pressed the sound comes on and the LED lights up. Here is the link to the video for topic 7: https://youtu.be/khOdr-NppUU

The code block to play just the introduction to the Imperial March for Star Wars is below. Strictly, on int notes 261, 329,
and 400 are needed and so this code block and corresponding circuit setup can run with just three switches.

<pre><code>
/*
Resistor Ladder - parallel circuit with differing voltages - switch controlled - into analog pin
*/

/*int buttons[6];
int buttons[0] = 2;
This block of code causes an error. On further investigation this code is redunant since these variables are not utilised elsewhere in the sketch. It should work fine without them.
*/

int notes[] = {261, 294, 329, 400}; //these notes are for the imperial march from Star Wars

void setup() {
  Serial.begin(9600);
}

void loop() {
  // local variable to hold input on pin A0
  int keyVal = analogRead(A0);
  Serial.println(keyVal);

  if(keyVal == 1023){
    // play first frequency in array on pin 8
    tone(8, notes[0]);
  }
  else if(keyVal >= 990 && keyVal <= 1010){
    // play second frequency in array on pin 8
    tone(8, notes[1]);
  }
  else if(keyVal >= 505 && keyVal <= 515){
    // play third frequency in array on pin 8
    tone(8, notes[2]);
  }
  else if(keyVal >= 5 && keyVal <= 10){
    // play fourth frequency in array on pin 8
    tone(8, notes[3]);
  }
  else{
    // if the value is out of range, play no tone
    noTone(8);
  }
}
</code></pre>

<h1>Topic 8</h1>

Topic 8 was the culmination of every topic, from 1 through 7. The task was to create an hourglass that measured the passing of a block of time - in this case an hour - by switching on an LED. The task required the setup of 6 LEDs for a total cumulative hourglass reading of 6 hours. The task was fun and the result was perfect. For the sake of time I brought down the time value to 0.6 seconds. The task worked as expected and every 0.6 seconds an LED came on.

With the sound projects from the previous tasks still fresh, I decided to see if I could create a sketch and circuit that not only lit up - as the basic task required - but also worked in conjunction with the piezo to sound at every time interval. I returned to task 7 and with some trial and error, managed to write in a code block within a conditional statement, using the OR logic operator, to tell the Arduino that with every time interval and corresponding LED to high, the piezo should also buzz - but only when the time interval has passed and the LED comes on together. The result of this customised experiment was awesome and the sketch worked exactly as I intended it to.

It is important to note how useful it is to experiment by fusing bits of discrete code and knowledge to extrapolate new ideas. As the tasks are getting more complex, I am also learning how to manage by workflow and processes. SO for this particular custom experiment, I first designed the circuit using Tinkercad. With the circuit in place I began focusing on the code, working through the errors one by one, till I figured out the best solution so far (I am sure there are better ones which I will discover as I make more progress). The result was a satisfying blend of several learnings, and a system that used both sound and light to alert for each time interval. I can see further applications to this project now that I am beginning to figure out how to make light and sound work in tandem. With the introduction of motion to the mix, it will very soon be possible to create much more complex (and satisfying) structures towards the final project, and hopefully beyond this masters programme.

I got my second taste with Tinkercad to draw circuit diagrams and run simulations. (Tinkercad has replaced circuits.io). The following image is the circuit diagram of the above-mentioned experiment using the piezo as well as LEDs to alert. My code for the circuit diagram and custom light and sound hourglass is below. Here is the link to the video for this topic: https://youtu.be/YGnfJx7Z-P8

<pre><code>
/*
Arduino digital hour glass topic 8 of week 2 - going beyond to include sound
 */

const int switchPin = 8;
const int pzoPin = 12; // the piezo is hooked up to pin 12
int notes[] = {261, 294, 329, 400};
unsigned long previousTime = 0;
int switchState = 0;
int prevSwitchState = 0;
int led = 2;


long interval = 6000; //for the sake of experimentation set timer to 6000ms

void setup() {
  Serial.begin(9600); //to monitor the piezo sound if needed
  for(int x = 2;x<8;x++){
    pinMode(x, OUTPUT);
  }
  pinMode(switchPin, INPUT);
  pinMode(pzoPin, OUTPUT);
}

void loop(){ 
  int keyVal = analogRead(A0);
  Serial.println(keyVal);
  
  unsigned long currentTime = millis(); 
  if(currentTime - previousTime > interval) {
    previousTime = currentTime; 
    // Turn LED on
    digitalWrite(led, HIGH);
    //progress led variable
    led++; //led+1 cycles through
    
    if(led == 7 || led == 6 || led == 5 || led == 4 || led == 3 || led ==2 || led == 1){  //OR statement to work for each interval
      pinMode(pzoPin, HIGH);
      tone(pzoPin, 200, 1000);
    }
  }

  switchState = digitalRead(switchPin); 
  if(switchState != prevSwitchState){
    // turn all LEDs off
    for(int x = 2;x<8;x++){    
      digitalWrite(x, LOW);
      pinMode(pzoPin, LOW);
    }  
    led = 2;
    previousTime = currentTime;
  }
  prevSwitchState = switchState;
}
</code></pre>

Here is the link to the image of the circuit: https://github.com/arjunkhara/physical-computing-repo/blob/master/Piezo-Hourglass.png

<h1>Topic 9</h1>

Topic 9 introduces the motor - a staple of physical computing and component activity. The essential setup is extremely similar to the servo motor in topic 8, with the exception of the introduction of a 9V battery to provide power to the motor. Two more components introduced in this topic are the transistor (concepts of gates and drains vis-a-vis voltage changes) and the single-direction diode to regulate which way the motor will spin — in this case anticlockwise. The importance of this diode is essential to understanding and therefore controlling motor direction spin. For example if in a later project I wanted to build a drone, the spin directions of the main rotor blades are completely reliant on the use of an H-bridge and the way the diode is installed. I will be using an H-bridge in topic 10 and so will be attempting to regulate motor speed instead, as my additional activity challenge.

While changing motor rotation direction is a relatively simple concept, I wanted to challenge myself to see if I could adjust the motor's speed. The same concept is used for a virtually infinite number of applications, from helicopter blades and fan speeds to robotics and wind and hydroelectric energy. I searched for a few tutorials online but ended up learning from Jeremy Blum's Exploring Arduino. Using PWM (a concept we have already learned) I figured out that a potentiometer could be used a simple speed regulator, and the serial monitor provides readouts (through mapping) of how fast the motor is turning.

This was incredibly interesting since now I have control over my build, and having control especially of something as important as motor speed is always a good thing. The code snippet for this additional activity is below, together with the circuit diagram. The reference used for this additional activity is 'Exploring Arduino, by Jeremy Blum, p. 69 - 72' and has also been listed in the references and bibliography section at the end of this page. Here is the link to the video for topic 9: https://youtu.be/_9LCoNPrPfc

<h1>Topic 10</h1>

Topic 10 focuses on building a circuit to control the speed and direction of a motor, through the example of a zoetrope. In this project I wired up the circuit as shown in the Arduino Project Book but instead of a zoetrope I added two copper wires to emulate both a helicopter drone (which I would like to later build) as well as a potential introduction to a magnetic flux induction. The project worked perfectly. One switch turned the motor on and off. Another switch changed the direction of the motor, while the potentiometer controlled the motor spin speed. The bi-directional rotation was achieved through use of an H-Bridge.

The H-Bridge plays an important role in electronics and physical computing, and warrants further examination. Essentially an H-Bridge performs four primary operations: Open; Forward; Backward; Braking. All four operations (or states of the bridge) are required for a motor to perform effectively. In the open state, all the switches remain open and the motor is at rest. In the forward and backward states opposite switches are running (converse configuration between forward and backward) to provide spin. The braking state is much like the open state except that the motor may still be running under its own momentum and will continue to do so till inertial forces slow it to a halt. If the switches on opposite sides were instead closed on the same side, the power source would short circuit causing a direct voltage to the ground and thus ruining the motor and perhaps its attached components.

In this Arduino task, a button switch was used to start and stop the motor, and another button switch was used to alternate the motor direction. While flipping the direction with the latter switch made little difference to the circuitry, standard safety practice dictates that the motor be turned off (using the former button switch) before reversing the rotor direction in order to prevent leak-back of current into the circuits, which often causes harm to the components. Here is the link for the video demo for topic 10: https://youtu.be/tZTVSqjM_QU

<h1>Week 3: References & Bibliography</h1>

• Arduino Community Forum, Arduino (2017) on Arduino Website (accessed October 2017) at https://forum.arduino.cc/index.php?topic=353524.0

• Arduino for Beginners: Essential Skills Every Maker Needs, Baichtal, J. (2014), United States of America: Pearson Education, Inc

• Arduino Project Handbook: 25 Practical Projects To Get You Started (1st Edition), Geddes, M. (2015), San Francisco: No Starch Press

• Arduino Tutorials, Arduino (2017) on Arduino Website (accessed October 2017) at www.arduino.cc

• Beginning C++ Through Game Programming, Dawson, M (2015), United States of America:Cengage Learning

• Exploring Arduino: Tools and Techniques for Engineering Wizardry, Blum, J. (2013), Indiana:John Wiley & Sons

• Games, Design and Play, A Detailed Approach to Iterative Game Design, Macklin, C and Sharp, J. (2016), New York: Addison-Wesley

• Practical Electronics for Inventors (4th Edition), Scherz, P. and Monk, S. (2016), New York:McGraw-Hill Education

<h1>Week 4</h1>

Topics 11 through 15 complete the foundations of Arduino, and encourage the integration of past learnings to more complex projects as well to extrapolate biggers ideas into custom-built projects. From LCD timers to projects involving the integration of software and firmware, this week’s learnings push students to apply all their skills to-date in more holistic ways, encouraging the use of independent thinking towards building self-imagined sketches and hardware. As in the previous weeks, the learning process remains imbricated as the complexities increase, providing more challenges and more opportunities to create unique sketches and creative outputs.

The following videos document this week’s topics and processes. The accompanying blog entries detail my thoughts, insights, analysis, and code blocks + recommendations (where feasible) on the week’s topic(s). References and bibliographies for all sourced and cited content has been provided at the end of this page:

<h1>Topic 11</h1>
Topic 11 introduces, among other elements, the use of LCDs and for the first time outputs information in the familiar medium of text-based interaction. The LCD in this topic was initially used to output random strings based on the arbitrary motion of the tilt switch. The tilt switch contains a little ball at rest. When moved or shaken the horizontal and vertical positions of the ball cause random pins to fire on cue, thus producing the pre-programmed response of that particular pin to be printed onto the LCD. The effect is likened to that of an 8-Ball or Seer’s Crystal Effect, producing seemingly prophetic responses to any questions asked. The random function is very similar to that used in programmes such as JavaScript to provide a number or hexadecimal colour value when a user clicks for a specific style. The basic project was fine and the results were just as the book was aiming for. However, the possibilities of LCDs with familiar text output warranted a greater urge to delve deeper and conjoin past projects to create something more useful.

As a result, I consulted several books and online tutorials and came across an interesting project from Jeremy Blum’s Exploring Arduino book, referenced below. By combining the thrust of Blum’s tutorials with a few other Arduino tutorials (also referenced below) I was able to figure out a simple code that made the LCD output the cardinal series numbers as seconds. This was achieved by first setting a variable, called timer, to zero, then incrementing its value up by one, with a delay between increments of 1000ms, or one second.

While Blum’s tutorial called for a simpler approach, I instead combined the layout of topic 11 with my own requirements to further challenge myself – in this case to have a potentiometer and tilt switch as component parts of the circuit but with independent controls over each. The result, simple in nature, was nonetheless fascinating. I got the LCD to act as an upward counter that would go on counting to 16 places, well beyond the lifetime of humanity. Likewise, a simple adjustment to the code, in this case setting the timer variable to any number (eg 300 seconds) and decrementing the value with code –1, I can build a countdown timer from any time point. The code for this challenge is below.

<pre><code>

/*
Arduino Week 4 Project 11 (Beyond Part 1)
*/

/*
LCD timer (source credit: Jeremy Blum, Exploring Arduino)
*/

// linking to the library
#include <LiquidCrystal.h>
int timer = 0; //starts the timer at zero
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
void setup() {
    lcd.begin(16, 2); //rows of 16 and columns of 2 for the LCD display
    lcd.print("Your Time is Now");
}

void loop() {
  lcd.setCursor(0, 1); //begin display on second line
  lcd.print(timer);
  delay (1000); //increments of 1 second
  timer++; //increment up from zero by value of 1
}
</code></pre>

This next block of code is to decrement the timer from a value starting at 30000ms (5 minutes). Also, as a quick aside, when writing code within pre tags use ampersandHex60; and ampersandHex62 for opening and closing < >.

<pre><code>
/*
Arduino Week 4 Project 11 (Beyond Part 2)
*/

// linking to the library
#include <LiquidCrystal.h>
int timer = 30000; //starts the timer at zero
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
void setup() {
    lcd.begin(16, 2); //rows of 16 and columns of 2 for the LCD display
    lcd.print("Your Time is Over");
}

void loop() {
  lcd.setCursor(0, 1); //begin display on second line
  lcd.print(timer);
  delay (1000); //increments of 1 second
  timer--; //increment up from zero by value of 1
}
</code></pre>

The link to my video documentation for this topic is here: https://youtu.be/daDIy5bMseEAs 

I progress through this course I am getting more interested in the mechanics of user-interface and information output as a means to exercise control over physical computing devices. Like the serial monitor, the LCD has enormous applications for such intentions, and I am exploring creating a temperature readout, from previous topics, that displays the temperature on the LCD rather than as a serially mapped value in the monitor. I will be exploring these and other potential projects in the coming week, both on my own and as part of any corresponding group work.

<h1>Topic 12</h1>

Topic 12 focuses on creating a knock knock lock, which rocks! The primary component in this task is the Piezo being used as an intensity gauge for vibration. These vibrations are registered in a combination, via the sketch, and then fed to a servo motor that turns according to the state of the sketch. Three LEDs provide additional visual confirmation of each state – green for unlocked, yellow for register, and red for locked. The yellow LED in particular has a fascinating function. Just like in JavaScript with Event Listeners that ‘listen’ for mouse clicks or other actions performed on a website, the yellow LED acts as a physical listener for the combination of pre-arranged taps and then hands off to the next state of the sketch. Likewise, the inclusion of Booleans makes perfect sense given the two primary states of locked and unlocked – true and false. I am beginning to understand better the relationships between Booleans, conditional statements, and event listeners, all of which come together within functions and commands to output a specific result. Approached in this context the term ‘physical computing’ resonates deeper.

As a review from the previous projects, piezoelectricity can also be generated simply by walking. When a piezo stack is installed in a shoe or piece of footwear, the motion and contact of the shoe with the ground and up again causes a charge to accumulate within the piezo, thus generating free electricity, albeit in relatively tiny quantities. However, the applications of such technology are far-reaching. It is also interesting to note that the sound produced by the piezo is the result of creating an imbalance in the particles / crystals / material that results in a force of charges, which induces the flow of electricity. The device used in this task is therefore known as a piezo transducer – a vehicle to facilitate piezoelectric charges. The term piezoelectricity comes from the Greek word piezein which literally means to press.

I am getting more confident with the wiring and schematics of the board, so in this task I decided to override the schematics provided in the project book for a configuration that felt right and easier for me. Needless to say I was exceedingly happy to find that this challenge worked and my circuit and sketch performed flawlessly. Apart from the several applications of this task – from combination-driven interactions to noise detectors – what got my attention is the fact that it is not only code that can be rewritten to perform the same functions, but hardware as well. Configurations provided in this book are therefore recommendations but by no means the only way to achieve an end result. These small hacks are incredibly useful for learning and I am encouraged to keep going beyond the curriculum and experiment with my own set of learnings and understanding of physical computing systems. I believe this challenge to go beyond the guidebook and apply my own design is arguably the most critical lesson of this module.

<pre><code>
/*
Arduino Week 4 Project 12 
*/

#include <Servo.h>
// create an instance of the servo library
Servo myServo;
const int piezo = A0;
const int switchPin = 2;    // switch pin
const int yellowLed = 3;    // Yellow LED pin
const int greenLed = 4;    // Green LED pin
const int redLed = 5;   // Red LED pin

int knockVal;
int switchVal;

const int quietKnock = 10;
const int loudKnock = 100;


boolean locked = false; // true or false boolean
int numberOfKnocks = 0;

void setup(){
myServo.attach(9); // Servo pin

pinMode(yellowLed, OUTPUT);
pinMode(redLed, OUTPUT);
pinMode(greenLed, OUTPUT);

pinMode(switchPin, INPUT);

Serial.begin(9600);

digitalWrite(greenLed, HIGH);

myServo.write(0);

Serial.println("the box is unlocked!");
}

void loop(){

  if(locked == false){
  switchVal = digitalRead(switchPin);
  if(switchVal == HIGH){
  locked = true;

  digitalWrite(greenLed,LOW);
  digitalWrite(redLed,HIGH);
  myServo.write(90);
  Serial.println("the box is locked!");
  delay (1000);
    }
  }

  if(locked == true){
  knockVal = analogRead(piezo);
  if(numberOfKnocks < 3 && knockVal > 0){
  if(checkForKnock(knockVal) == true){
  numberOfKnocks++;
      }
      
  Serial.print(3 - numberOfKnocks);
  Serial.println(" more knocks to go");
    }
    
  if(numberOfKnocks >= 3){
  locked = false;
  myServo.write(0);
  delay(20);
  digitalWrite(greenLed,HIGH);
  digitalWrite(redLed,LOW);
  Serial.println("the box is unlocked!");
    }
  }
}

boolean checkForKnock(int value){
  if(value > quietKnock && value < loudKnock){
  digitalWrite(yellowLed, HIGH);
  delay(50);
  digitalWrite(yellowLed, LOW);
  Serial.print("Valid knock of value ");
  Serial.println(value);
  return true;
  }

  else {
  Serial.print("Bad knock value ");
  Serial.println(value);  
  return false;
  }
}
</code></pre>

<h1>Topic 13</h1>

Topic 13 uses capacitance to run a current through the circuit, owing to differences in charges of different materials. The project required setup of an LED, two resistors, and cables connected to pins on the Arduino. Only a ground wire was required for this project since the power to the sensor was coming from digital pin 4. The project also required access to the capacitance library which was more straightforward to link to via the Arduino Web Editor, available here [+]. The project was a success and I tried various materials, from batteries to an aluminium can. However only by touching the wire with my hand was I able to light up the LED, since the difference in charge exceeded the threshold initially set to 1000. If I were to decrease the threshold to 10 or less, the LED would light up more often with different materials.

The project was a success and it got me thinking about its uses as a proximity sensor as well as a materials detector, once I inputted the capacitance of different materials. There is a very interesting article I discovered on the National Center for Biotechnology Information’s PMC journal, which discusses the influence of parasitic capacitance on output voltages, accessible here [+] and describes the relationship between initial and equilibrium charges, expressed by a simultaneous matrix equation, where A, C, and Cp are n × n matrices:

AQ’ + IQp = AQ<br/>
CQ’ + CpQp = 0

<cite>Kensuke Kanda, Takashi Saito, Yuki Iga, Kohei Higuchi,2 and Kazusuke Maenaka, “Influence of Parasitic Capacitance on Output Voltage for Series-Connected Thin-Film Piezoelectric Devices”, Sensors Basel. National Center for Biotechnology Information, December 4, 2012, https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3571804/ (accessed October 31, 2017).</cite>

The applications of parasitic capacitance, with regards to healthcare, is discussed at length in the paper cited above, and this project is a rudimentary but essential introduction to the topic in general. In addition, the idea of a proximity sensor also got me thinking about the use of sound as an indicator, which might prove more useful. I decided therefore to set myself another challenge and see if I could code the Arduino and setup a physical circuit to make this possible, based on everything I have learned so far.

I set up the circuit and coded the Arduino with help from topic 6 which introduced the Piezo. The challenge, to my delight, worked beautifully and I was able to hold the end of the wire and have the piezo produce a higher tone, val 330. When I let go the piezo reverted to its initial lower tone, val 230. I programmed both of these tones using a conversion chart that is accessible here[+]. I very much enjoyed this project, and have included the resources I consulted in the references and bibliography section below. The use of both sound and light is always an exciting prospect and, as my confidence slowly continues to grow, I am looking forward to moving away from the guide book and assigning myself even more challenging tasks. The code block for the additional challenge, as well as the accompanying circuit diagram, are detailed below:

<pre><code>

/*
Arduino Week 4 Project 13 (Beyond)
This is the code to use a piezo instead of an LED to play different sounds given the same variables for capacitance connections
*/

#include 

CapacitiveSensor capSensor = CapacitiveSensor(4,2);

int notes[] = {230, 330}; // change these notes to any value. See this document for corresponding value codes.
int threshold = 1000;
int sensorValue;
const int ledPin = 12;

void setup() {
Serial.begin(9600);
pinMode(ledPin, OUTPUT);
}

void loop() {
long sensorValue = capSensor.capacitiveSensor(30);
Serial.println(sensorValue); 

if(sensorValue > threshold) {
tone(12, notes[1]);
  }

else {
tone(12, notes[0]); // here you can change the code to make the piezo go silent, for example by adding note 0 as the third item in the int notes array, then calling for that note and appending it here eg notes[2].
  }

delay(10);
}
</code></pre>

Here is the circuit diagram for the touchy-feely Piezo. The code block (above) can be changed to a variety of combinations, from the piezo remaining silent till contact is made, to a variety of notes based on contact. I have made a note in the code block above as to where these changes can be made: https://github.com/arjunkhara/physical-computing-repo/blob/master/Piezo-Touchy-Feely.png
