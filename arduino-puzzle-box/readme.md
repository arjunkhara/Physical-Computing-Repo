<h1>Arduino Puzzle Box</h1>

<h3>PUZZLE BOX: INTRODUCTION</h3>
The Puzzle Box is a mid-term challenge to assess two criteria: (1) how much of Arduino and physical computing have students learned; (2) willingness to step beyond comfort zones and test learnings by building a puzzle box with familiar and unfamiliar components, the latter requiring self-initiative and exploration. I was quite excited, if also apprehensive, about this assignment, but I felt the result had a distinctive and somewhat whimsical quality that invited conversations and further questions from all who saw it. I ended up building a force-driven puzzle box with LEDs, Piezo speaker, accelerometer, sound sensor, servo motors, two Arduino boards, laser-cut box with polarisation properties, and an overarching theme from Star Wars. The following entry documents this week’s topics and processes. The accompanying blog entries detail my thoughts, insights, analysis, and code blocks + recommendations (where feasible) on the week’s topic(s). References and bibliographies for all sourced and cited content has been provided at the end of this page. Note: The references made to Star Wars themes and related items have been used here strictly for educational and personal project purposes only, and are not intended for commercial or official use of any kind whatsoever. Nothing in this project is endorsed or sponsored by the Star Wars brand.

<h3>PUZZLE BOX: ESSENCE</h3>
The essence of this puzzle box is to tilt the box along different axes and listen to each tone that plays. For those who are familiar with Star Wars, the clue easily suffices. The addition of the laser-cut Darth Vader head in the front of the box is probably a dead giveaway. For people with hearing disabilities, I also integrated a lighting system to indicate the combination. When the tones are played in the correct order, and all three LEDs light up, the box opens. However, to counter this easiness for those without impairment, I used a particular colour of acrylic for my box. Orange has a polarising effect on blue LEDs, the last one required to open the box. Therefore while the box is transparent, there is no way to tell whether the blue LED is on or off just by looking at it, since the orange acrylic cuts out the blue emission. This makes it more of a challenge to open the box. The result is a puzzle box that uses the force of light, the force of sound, the force of planetary spin, and “the Force” or instinct to open.

<h3>PUZZLE BOX: INSPIRATION</h3>
Having covered LEDs, buttons, and speakers quite extensively in the first few weeks, I decided to create a theme for my project along forces and energy. Essentially the LEDs are light energy, and speakers are sound energy. This gave me an idea for using “the Force” to open the box. From the various components I considered and experimented with, the accelerometer held most utility, which gave rise to the thinking: how cool would it be to use the Earth’s spin to open a puzzle box? Plus the idea of tying in the project with a favourite show was appealing enough to title the project, ‘Use the M•A’. In this instance the M•A serves as both the qualification of this masters as well as the elements of Newton’s famous equation: Force (F) = Mass (M) x Acceleration (A). Combining an accelerometer with Star Wars made perfect sense. However, I also wanted to create a box that would serve a purpose beyond just opening and closing, which I figured would get stale quite quickly, no matter how appealing the initial process of opening the box might be.

<h3>PUZZLE BOX: ACCELEROMETER</h3>
I set out to first build the circuitry for the accelerometer. Figuring out how the physics of how an accelerometer worked was fairly straightforward. The challenges came from learning how to code, attach, and update the libraries and scripts for the accelerometer, then orienting the device’s code and physical structure to produce readouts that were useful and accurate enough to cause conditional behaviour. I consulted several more sources than initially anticipated, all of which have been included in the reference section below. Briefly, the accelerometer has six degrees of freedom along the axes it moves. Each movement produces a value of motion. Perhaps the most amazing thing about the accelerometer is how these values are produced. An accelerometer works of tiny capacitance changes when the device is moved along the X, Y, and Z axes, in relation to the spin-charge of the rotating Earth. These changes are what is measured in the values produced. In other words, an accelerometer uses the spinning of the Earth and its resultant changes in orientation, which produce minute voltage differences, to effect orientation. By moving the accelerometer and generating these values, I was able to harness these differences from the Earth’s spin and use them to cause other actions. This device was literally using the force of the Earth, which is amazing to think about.

<h3>PUZZLE BOX: PIEZO SPEAKER AND NOTES</h3>
Once I was able to integrate all the libraries and scripts into the programme, I needed to create booleans and conditionals for these values to work with the LEDs and Piezo speaker. I setup the code such that a tilt along the X axis lights up an LED and plays a particular note, while tilting it along the Y and Z axes causes other LEDs and notes to activate. Once I had figured out the accelerometer’s six axes of freedom, I focused on making LEDs and speaker. Lighting up the LEDs was quite straightforward. The Piezo, however, posed plenty of opportunities, limited only by the Arduino’s internal 64K memory. Fortunately, the Imperial March theme from Star Wars only has three notes: F, C, and A. Once I integrated the Piezo library and assigned the tone, the Piezo played each note depending on where and how the box with the accelerometer was tilted. The challenge came from having the Piezo play each note for as long as I needed it to, followed by stops of appropriate duration. More research led to discovering the that the tone function took more than one parameter: it also took frequency and pause. Once I had this settled, the Piezo played each tone perfectly. Plus, when the box lid opened, the speaker played the entire bar from of the Imperial March, the reward for figuring out the combination of tilts and motion.

<h3>PUZZLE BOX: LEDS</h3>
I used LEDs as conditional statements to instruct the servos to turn, since the tones played by the Piezo were of insufficient analog output for the Arduino sensors to pick up straightaway, and initial tests of sound as a condition to operate the servos proved unreliable. LEDs on the other hand worked perfectly and drove the conditions to operate the servos to open the box. The orange acrylic did a fine job of cutting out the blue wavelength, which added an additional twist to the puzzle.

<h3>PUZZLE BOX: SERVOS</h3>
I initially though of using the servo motors as locks pushed through a slit in the box and spun perpendicular to act as a door jam, but then noticed that servo arms are incredibly difficult to turn without the correct command and source of power. I therefore decided to hack the servo as a hinged lifting device, that raised the lid of the box like a submarine hatch. This required the use of two servo motors, since one was not strong enough. And this caused additional challenges. Because both servos had to lift at exactly the right time, both had to be programmed with identical code. This seemed easy enough, till it came to the construction of the box mechanics. In order to lift the lid, the servos had to be placed on either side of the box, arms facing each other.This meant that if both servos were fed the same code, they would turn synchronously, each opposing the spin of the other; one would push up, the other pull down and the lid would break. As a result, I had to programme the servos to perform opposite functions, which added a significant level of complexity to the project, because the angles and turn speeds on each servo vary in tiny degrees from others. With some trial and error and the addition of the servo library, I was able to figure out the best combination of asynchronous turn directions and finally got the servos to work in tandem with each other. The result was a lid that lifted like a hatch when the box tilted, the LEDs lit up, and the Piezo sounded.

<h3>PUZZLE BOX: SOUND SENSOR</h3>
Once the basic mechanism of the box was sorted, I wanted to give the project utility beyond the classroom, by creating something I could use repeatedly. I was still intrigued by the idea of Star Wars, and so, after creating the Darth Vader mask, I decided to use two red LEDs as eyes, with the initial intention of getting them to flash when the box opened. However, the Piezo playing the Imperial March was adequate, and I wanted the eyes to flash independent of the box opening and closing. I therefore looked into using a sound sensor that caused the red LEDs to flash according to music. The process required not just setting up the sound sensor and library, but tuning it physically (with the built-in potentiometer) and through code by setting a threshold that was suitable for both, the sound sensor as well as the ambient noise gain. After a lot of trial and error, I was able to figure out the threshold (i.e. 80 worked best, 79 did not work at all, and 81 was overkill). The result was quite frankly spectacular, perhaps even more exciting than figuring out the accelerometer. The lights in Darth Vader’s eyes flashed in response and time to music of any scale, but particularly to voice-driven songs, a nice, unintended side effect. When placed next to a speaker, the puzzle box almost appears to come alive with an in-built force, another happy theme from Star Wars.

<h3>PUZZLE BOX: LASER CUTTING AND 3D PRINTING</h3>
I was tempted to use a cardboard box for this project as it seemed the easiest solution, but the idea of keeping this box beyond the classroom or project necessitated a more permanent solution. I therefore researched more on the acrylics available at the College’s computer lab, and discovered the properties of light polarisation, which was sufficient motivation to build the entire puzzle box from laser-cut acrylic. Plus, what’s the point of a Star Wars themed box that does not use lasers? I first prototyped by box out of paper; with the dimensions set and positions of holes, battery holders, and container depth set, I moved on to cutting the actual box with orange acrylic — also the colour of Sith lightsabers, together with its embellishments in a deep purple — a popular colour of lightsaber blades for the Jedi. With the box done, I also cut out the lid. However, the weight of the acrylic, light though it is, was too much even for two servo motors. I proceeded to cut out gears to make turning easier but the servo motors in the standard Arduino kit lack sufficient power to lift anything slightly heavier than cardboard. I therefore created my box cover by 3D printing a lid and manually cutting it along its contours so that it would not interfere with the servo motors. Once I acquire stronger servo motors, I will swap out the 3D-printed lid with the original acrylic design, and attach the gears to the mechanism for further lifting strength.


<h3>PUZZLE BOX: CODE PART 1</h3>
Below is the code and circuit diagram for the puzzle box, with the accelerometer, servo motors, LEDs, and Piezo speaker.
<pre><code>
/*Arduino Puzzle Box Part 1: (Code for the Puzzle Box)*/
/*LIBRARY SOURCE FOR THIS PROJECT: ARDUINO COMMUNITY FORUM 423364.0*/
/*NOTE: While the variable names have been changed to align with my understanding, the underlying code structure and knowledge that I have gained and used here have been sourced from the Arduino Community Forum 423364.0 and listed in the reference section, together with the other books, websites, and video tutorials that I consulted in figuring out how to make this project work.*/ 

#include 
#include 
Servo servo1;
Servo servo2;
int servopos = 0;
int pzPin = 8;

long XaxisForce, YaxisForce, ZaxisForce;
long XgyroF, YgyroF, ZgyroF;
float currentY; //let the serial monitor know if motion is detected
float XgyroForce, YgyroForce, ZgyroForce;
float XrotationForce, YrotationForce, ZrotationForce;

/*EXCODE*/
int xval=A4;
int yval=A5;
int out1=11; //red LED
int out2=12; //green LED
int out3=13; //green LED

void setup() {
  servo1.attach(3);
  servo1.write(90);
 servo2.attach(5);
  servo2.write(90);
  servo1.write(0);
  servo2.write(180);
  
  Serial.begin(9600);
  Wire.begin();
  setupMPU();
  
  /*EXCODE*/
  pinMode(xval,INPUT);
  pinMode(yval,INPUT);
  pinMode(out1,OUTPUT);
  pinMode(out2,OUTPUT);
  pinMode(out3,OUTPUT);
  
  digitalWrite(out1,LOW);
  digitalWrite(out2,LOW);
  digitalWrite(out3,LOW);
}

void loop() {
  YaxisForce = float(accelY);
  currentY = YaxisForce;
  recordAccelRegisters();
  recordGyroRegisters();
  printData();
  delay(333);
  
  /*EXCODE*/
  int xPin=analogRead(xval);
  int yPin=analogRead(yval);
  //Serial.println(xval); // bug testing
  //Serial.println(yval); // bug testing
  
  if (XgyroForce >= 0.30){ //red
    digitalWrite(out1,HIGH);  
    tone(pzPin, 440, 800);
  }
  
  if (YgyroForce >= 0.30){ //red
    digitalWrite(out2,HIGH);  
    tone(pzPin, 349, 800);
  }
  
  if (XgyroForce <= -0.30){ //red
    digitalWrite(out3,HIGH);  
    tone(pzPin, 523, 800);
  }
    
  if (out1 == HIGH && out2 == HIGH && out3 == HIGH){
    //OPEN SERVO DOORS
    for(servopos = 0; servopos < 93; servopos++){
    servo1.write(88);
    delay(30);
    servo2.write(58); //make servo2 spin in phase opposites to servo1
    delay(30);
    }
    //OPEN SERVO DOORS
    
     //PLAY TONES
    tone(pzPin, 440, 800);
    delay(800);
    tone(pzPin, 440, 800);
    delay(800);
    tone(pzPin, 440, 800);
    delay(800);
    tone(pzPin, 349, 800);
    delay(800);
    tone(pzPin, 523, 600);
    delay(300);
    tone(pzPin, 440, 800);
    delay(800);
    tone(pzPin, 349, 800);
    delay(800);
    tone(pzPin, 523, 600);
    delay(300);
    tone(pzPin, 440, 800);
    delay(800);
    //PLAY TONES
    
  } else if (out1 == LOW && out2 == LOW && out3 == LOW){ //green
    digitalWrite(out1,LOW); 
    digitalWrite(out2,LOW); 
    digitalWrite(out3,LOW); 
    //CLOSE SERVO DOORS
    for(servopos <= 93; servopos > 0; servopos--){
    servo1.write(0);
    delay(30);
    servo2.write(180);
    delay(30);
    }
    //CLOSE SERVO DOORS
    
    } else if (XgyroForce < 0.30 && XgyroForce > -0.30 ){  //blue LED test condition
    Serial.println("I AM working"); //blue LED test results
    
    }else{
    Serial.println("I am outside the range");
    }
}
  
/*LIBRARY SOURCE: ARDUINO COMMUNITY FORUM 423364.0*/

void setupMPU(){
  Wire.beginTransmission(0b1101000); //This is the I2C address of the MPU (b1101000/b1101001 for AC0 low/high datasheet sec. 9.2)
  Wire.write(0x6B); //Accessing the register 6B - Power Management (Sec. 4.28)
  Wire.write(0b00000000); //Setting SLEEP register to 0. (Required; see Note on p. 9)
  Wire.endTransmission();  
  Wire.beginTransmission(0b1101000); //I2C address of the MPU
  Wire.write(0x1B); //Accessing the register 1B - Gyroscope Configuration (Sec. 4.4) 
  Wire.write(0x00000000); //Setting the gyro to full scale +/- 250deg./s 
  Wire.endTransmission(); 
  Wire.beginTransmission(0b1101000); //I2C address of the MPU
  Wire.write(0x1C); //Accessing the register 1C - Acccelerometer Configuration (Sec. 4.5) 
  Wire.write(0b00000000); //Setting the accel to +/- 2g
  Wire.endTransmission(); 
}

void recordAccelRegisters() {
  Wire.beginTransmission(0b1101000); //I2C address of the MPU
  Wire.write(0x3B); //Starting register for Accel Readings
  Wire.endTransmission();
  Wire.requestFrom(0b1101000,6); //Request Accel Registers (3B - 40)
  while(Wire.available() < 6);
  XaxisForce = Wire.read()<<8|Wire.read(); //Store first two bytes into XaxisForce
  YaxisForce = Wire.read()<<8|Wire.read(); //Store middle two bytes into YaxisForce
  ZaxisForce = Wire.read()<<8|Wire.read(); //Store last two bytes into ZaxisForce
  processAccelData();
}

void processAccelData(){
  XgyroForce = XaxisForce / 16384.0;
  YgyroForce = YaxisForce / 16384.0; 
  ZgyroForce = ZaxisForce / 16384.0;
}

void recordGyroRegisters() {
  Wire.beginTransmission(0b1101000); //I2C address of the MPU
  Wire.write(0x43); //Starting register for Gyro Readings
  Wire.endTransmission();
  Wire.requestFrom(0b1101000,6); //Request Gyro Registers (43 - 48)
  while(Wire.available() < 6);
  XgyroForce = Wire.read()<<8|Wire.read(); //Store first two bytes into XaxisForce
  YgyroForce = Wire.read()<<8|Wire.read(); //Store middle two bytes into YaxisForce
  ZgyroForce = Wire.read()<<8|Wire.read(); //Store last two bytes into ZaxisForce
  processGyroData();
}

void processGyroData() {
  XrotationForce = XgyroF / 131.0;
  YrotationForce = YgyroF / 131.0; 
  ZrotationForce = ZgyroF / 131.0;
}

void printData() {
  //Serial.print("Gyro (deg)");
  //Serial.print(" X=");
  //Serial.print(XrotationForce);
  //Serial.print(" Y=");
  //Serial.print(YrotationForce);
  //Serial.print(" Z=");
  //Serial.print(ZrotationForce);
  //Serial.print(" Accel (g)");
  Serial.print(" X=");
  Serial.print(XgyroForce);
  Serial.print(" Y=");
  Serial.print(YgyroForce);
  //Serial.print(" Z=");
  //Serial.println(ZgyroForce);
}
</code></pre>


<h3>PUZZLE BOX: CODE PART 2</h3>
Below is the code and circuit diagram for the sound sensor and corresponding flashing lights, built on the second Arduino board.
<pre><code>
/*Arduino Puzzle Box Part 2: (Code for the Sound Sensor)*/
int led1 = 13;
int led2 = 12;
int led3 = 11;
int led4 = 10;
int threshold = 80; //DO NOT Change This (configured)
int volume; //To be read by the microphone

void setup() {                
    Serial.begin(9600); // For debugging
    pinMode(led1, OUTPUT);    
    pinMode(led2, OUTPUT); 
    pinMode(led3, OUTPUT);
    pinMode(led4, OUTPUT); 
}

void loop() {
    volume = analogRead(A0); // Reads the value from the Analog PIN A0

  if(volume >= threshold){
    digitalWrite(led1, HIGH); //Turn ON RED Led
    digitalWrite(led2, HIGH); //Turn ON RED Led
    digitalWrite(led3, HIGH); //Turn ON RED Led
    digitalWrite(led4, HIGH); //Turn ON RED Led
  } else {
    digitalWrite(led1, LOW); //Turn OFF RED Led
    digitalWrite(led2, LOW); //Turn OFF RED Led
    digitalWrite(led3, LOW); //Turn OFF RED Led
    digitalWrite(led4, LOW); //Turn OFF RED Led
  }
}
</code></pre>

<h3>PUZZLE BOX: MATERIALS AND DIMENSIONS</h3>
Below are the materials and dimensions used to build the housing frame and attachments for the puzzle box.
![alt tag](https://www.nano.training/wp-content/uploads/2017/11/MA-Puzzle-Box.png "Materials List and Diagram of Parts for the Box")

<h3>PUZZLE BOX: CONCLUDING THOUGHTS</h3>
Building this puzzle box has given me plenty more food for thought when approaching physical computing as both a serious subject and a regular hobby. The idea, that everything human beings utilise on a daily basis across society is designed, is impossible to appreciate without building something with significant manufacturing input. From the lamps in our bedrooms to the machines that lift and drop elevators to the treadmills in the gym and the automatic bus doors that swing open and shut, everything has been designed and carefully manufactured. The process of building this puzzle box, modest by comparison, nonetheless runs along these tracks. The prevalence of sensors, actuators, motors, and drivers in our society is blindingly powerful once we begin to see the world through this lens. The quiet development of the Internet of Things vis-à-vis the Internet of Information, is a silent nod towards the importance of physical computing and its yet untapped effect on society. What can we say of the twenty billion devices waiting to network with each other? or indeed of the immense neural-like network these devices will form? Yorick Wilks talks about 'get[ting] to a more people-friendly web precisely by making it machine-friendly, by realising Berner-Lee's original vision of a web that machines themselves understand.' (Wilks 2014, p.372). Wilks is referring here to semantic and other machine-learning capabilities being deployed across the Internet, which are revolutionising information-sharing beyond our wildest dreams. Yet the significance of the future is best encapsulated not in the vast imaginations of tomorrow, but in the little changes that power the world each day, and each day bring our world closer to that truly puzzling notion of a utopian society that our species has consistently endeavoured towards ever since we first emerged onto this existence.

