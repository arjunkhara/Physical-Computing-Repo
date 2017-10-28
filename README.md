# arduino
My physical computing and arduino projects

I’m Arjun. This is my weekly blog for the Physical Computing Module for my MA at Goldsmiths (2017 – 2018). I built this site to document my work, learnings, and insights on a weekly basis spanning this module’s duration. This repository also serves as a learning portal to question and experiment beyond the scope of what the module asks, in order to gain the deepest possible appreciation of physical computing and its evolving role as a companion in our digitally nebulous societies. Once completed, I hope to leave this blog as an active reference for future students of the subject.

Topics 1 through 4 introduce students to the Arduino platform — a circuit board with a micro-controller, capable of integration with both software and hardware. In this respect, the Arduino is a driver of the Internet of Things (IOT), an ecosystem in which connectivity and data-driven decisions extend to physical devices and multi-material computing components. The seemingly simple ability of the board to react to sensors and activate actuators provides an almost limitless array of possibilities across industries, from performance and art to bio-medical and communication applications. In other words, the Arduino is a tangible ambassador of the digital humanities — the confluence of technology, philosophy, form, and function.

I began by using the Arduino IDE (desktop version) but after some research found the web version much easier to use, with the added benefits that cloud provides. The link to Arduino’s web editor and playground can be accessed here [+]. It is interesting to think of Arduino, first, as a simple interface for power despite its ability to convey much more. The topic requires wiring the board to an LED with a switch and a resistor, and powering the circuit with a USB cable via a computer. The project was a success, and given the relative simplicity of the task, I decided to experiment with more than one LED. The purpose was to satisfy my curiosity and the inclusion of an additional LED was easy to accomplish. That, however, led to an idea of a simple game of quick click — a test of reflexes. I added another LED, resistor and switch circuit to the board and within a few minutes had a classic reflect game of red versus blue. The switches were placed on either side of the board for both players to quickly close their circuit in order to light up their respective LED.

I considered doing a version where if one player clicked, the other’s circuit would break. At this point I started considering resource allocation, given the size and power of the board and its components. With this in mind, I rewired my circuits to accomplish the same effect, i.e. whoever presses late stands out, but with a single blue LED and two switches. The faster player’s response triggers the LED to come on. The slower player is indicated by a brightening of the LED to indicate an action. The game design is simple but the principles of play coupled with this nascent insight into resource management will, I suspect, be of immense use in later projects.

It was natural, with all the flashing LEDs, to notice the board itself had light indicators built-in. After some research online I found a tutorial, accessible here [+], on how to manipulate the light on the board itself via pin 13. The process was, in many ways, the complete opposite to the requirements of topic 1, since topic 1 required pure hardware to make lights blink. This additional exercise required pure software, other than the board itself. This experiment is also my first sketch with Arduino and an exciting introduction into the confluence of software and hardware that is physical computing. The video and code for this sketch is below.
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
