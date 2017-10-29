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

Upon completing the basic task, I wondered at how temperature (from topic 3) might affect the LED and if I could either devise or find or customise such an experiment in which the coloured LED would change depending on how hot the temperature got. I found a similar reference in ‘Exploring Arduino’ by Jeremy Blum and in ‘Arduino Programming’ by Mark Torvalds. I chose ‘Exploring Arduino’, which provides only the basic code base and does not include any details on the crucial serial monitor, which I would need for such an experiment. But drawing from topic 3’s learnings, I was able to extrapolate the code to create my own custom variables and serial log through which I would be able to measure the temperature that corresponded with the type of light — blue for cool, red for warm, and green for optimum. The following code snippet is a result of this customisation and extrapolation.

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
