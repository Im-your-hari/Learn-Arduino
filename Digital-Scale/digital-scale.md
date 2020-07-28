# Digital Scale

In this workhop we will learn how to how to make a digital scale to measure distance.


### Problem Statement 

In order to measure distance from some physical thing we can use scale or measuing tap, but what if we need to need to take continous measurement and analyize the differnce, or we need to make an action depends on the distance like water level, waste level, oil level etc. repetitive continous measurement cost too much human resource. 

### Idea

What if, we have a system that can be continually monitor the level and make actions. 

### Solution

Build a device that can be controled wcontinually monitor the level and make actions like getting notification when a waste bin is full or getting a notification that can be help to prevent flood by monitoring water level..etc

<hr>

### Prototype Building

* Build a device that Measure distace and displayed on LCD Screen

Here we are using an Arduino as controller and HCSR04 Ultrasonic Module to measure the distance and 16x2 LCD Display to Display the Distance. 

![digram](src/images/diagram.png) 

<hr>

### Things we need 

1. Arduino Uno
2. HCSR04 Ultrasonic sensor
3. 16x2 LCD Module
4. 10k ohm potentiometer
5. 220 ohm resistor
6. Jumper Wires
7. Breadboard

<hr>


#### Ultrasonic Sensor

Ultrasonic sensors work by sending out a sound wave at a frequency above the range of human hearing.  The transducer of the sensor acts as a microphone to receive and send the ultrasonic sound. 

It emits an ultrasound at 40 000 Hz which travels through the air and if there is an object or obstacle on its path It will bounce back to the module. Considering the travel time and the speed of the sound you can calculate the distance.

![HCSR04](src/images/hcsr04working.png)

The HC-SR04 Ultrasonic Module has 4 pins, Ground, VCC, Trig and Echo. The Ground and the VCC pins of the module needs to be connected to the Ground and the 5 volts pins on the Arduino Board respectively and the trig and echo pins to any Digital I/O pin on the Arduino Board.


![HCSR04](src/images/HCSR04pinout.jpg)
<hr>


#### LCD Module
An LCD is an electronic display module which uses liquid crystal to produce a visible image. The 16×2 LCD display is a very basic module commonly used in DIYs and circuits. The 16×2 translates o a display 16 characters per line in 2 such lines. In this LCD each character is displayed in a 5×7 pixel matrix.

![LCD Pinout](src/images/lcd_pinouts.png)

#### Pin Description 

![LCD Pin Description](src/images/lcd_pinouts_des.png)


<hr>

### Step 1: Arduino Setup

#### 1.1: Install Arduino IDE

Download the [Arduino IDE](https://www.arduino.cc/en/Main/Software) and install it on your computer.

![Arduino IDE Download](../docs/images/arduinoide01.JPG)

#### 1.2 walk-through the Arduino Introduction page to learn basics
If you are new to the arduino system, you can learn the [ Arduino basics from here](Arduino-basics/arduino-basics.md) , after reading then go to the next step.

### Step 2: Programming

#### 2.1 Algorithm

![algorithm](src/images/algorithm.png)

<hr>

#### 2.2 Open Arduino IDE and Start a new Sketch 

![Arduino IDE Sketch](../docs/images/arduinoide02.JPG)

#### 2.3 Read then Copy and Paste the Code

### Tesing HCSR04 UltraSonic Module

<pre>

<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">trigPin</font> <font color="#434f54">=</font> <font color="#000000">9</font><font color="#000000">;</font> &nbsp;&nbsp;<font color="#434f54">&#47;&#47; defines Pin 9 as Trigger Pin</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">echoPin</font> <font color="#434f54">=</font> <font color="#000000">10</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; define Pin 10 as Echo Pin</font>

<font color="#434f54">&#47;&#47;define Variables</font>
<font color="#00979c">long</font> <font color="#000000">duration</font><font color="#000000">;</font>
<font color="#00979c">int</font> <font color="#000000">distance</font><font color="#000000">;</font>


<font color="#00979c">void</font> <font color="#5e6d03">setup</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>

 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">trigPin</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; Sets the trigPin as an Output</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">echoPin</font><font color="#434f54">,</font> <font color="#00979c">INPUT</font><font color="#000000">)</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; Sets the echoPin as an Input</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">9600</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Starts the serial communication</font>

<font color="#000000">}</font>
<font color="#00979c">void</font> <font color="#5e6d03">loop</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>

 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">trigPin</font><font color="#434f54">,</font> <font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Clears the trigPin</font>
 &nbsp;<font color="#d35400">delayMicroseconds</font><font color="#000000">(</font><font color="#000000">2</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; wait for 2 micro second</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">trigPin</font><font color="#434f54">,</font> <font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;<font color="#434f54">&#47;&#47; Sets the trigPin on HIGH state</font>
 &nbsp;<font color="#d35400">delayMicroseconds</font><font color="#000000">(</font><font color="#000000">10</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; wait 10 micro second</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">trigPin</font><font color="#434f54">,</font> <font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; Sets the trigPin on LOW state</font>

 &nbsp;<font color="#000000">duration</font> <font color="#434f54">=</font> <font color="#d35400">pulseIn</font><font color="#000000">(</font><font color="#000000">echoPin</font><font color="#434f54">,</font> <font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; Reads the echoPin, returns the sound wave travel time in microseconds</font>

 &nbsp;<font color="#000000">distance</font> <font color="#434f54">=</font> <font color="#000000">duration</font> <font color="#434f54">*</font> <font color="#000000">0.034</font> <font color="#434f54">&#47;</font> <font color="#000000">2</font><font color="#000000">;</font> &nbsp;<font color="#434f54">&#47;&#47; Calculating the distance</font>

 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Distance: &#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#000000">distance</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Prints the distance on the Serial Monitor</font>

 &nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">500</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; wait 500 milli second</font>
<font color="#000000">}</font>

</pre>

#### 2.4 Compile the code 

You can Compile and verify your code by clicking the **Verify** button on Arduino IDE, this process will check syntax errors. 

![verify code](../docs/images/verifycode.png)

after successful compilation you can see **Done Compiling**

![done verify](../docs/images/doneverify.JPG)
<hr>

#### 2.5 Upload the code into Arduino uno 

After successful compilation we can upload the code into Arduino Uno Devlopment board. for that we need click ***Upload* button.

![uploadcode](../docs/images/uploadcode.png)

before upaloading we need to select the devlopment board from the from Arduino IDE **Tools -> Board**  and **Port** from Arduino IDE **Tools -> Port**. 

![selectport](../docs/images/selectport.png) 
<br><br>

![selectboard](../docs/images/selectboard.png)


here I selected **Arduino Uno** as board and **COM26** as **Port**. 

Then click **Upload**

![doneupload](../docs/images/doneupload.JPG)

<hr>



#### 2.5 Connect the HCSR04 Module to Arduino

![HCSR04 Connection](src/images/testhcsr04.png)

<hr>

We can test the project from halfway without LCD module by using **Serial Monitor** .

After connecting the HCSR04 on arduino connect the USB cable and Open **Serial Monitor** .

![serial monitor](../docs/images/serialmonitor.png)

![Distance Test](src/images/distanceTest.gif)

We can see the distance measured from the Ultrasonic sensor from the Serial Monitor Window

![Serial Distance](src/images/serialDistance.PNG)


<hr>

### Tesing LCD Module

Here we are using LCD Module with **12C addons** for I2C Communication , which will only need two wires for communication, in other way we need to use 14 pins. 

Since the I2C is a addon we need  to insert the library on Arduino IDE first. For that first downlaod the [Arduino-LiquidCrystal-I2C-library.zip](src/lib/Arduino-LiquidCrystal-I2C-library.zip), Then click **Sketch -> Include Library -> Add .ZIP Library**

![inlcude lib](src/images/includeLib.png)

then select the **.Zip** file and click open.
![add zip file](src/images/openLib.png)

now we successfully added the I2C library. 


#### Uplaod and Compaile Code 

<pre>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><font color="#d35400">Wire</font><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font> 
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><b><font color="#d35400">LiquidCrystal_I2C</font></b><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>

<font color="#434f54">&#47;&#47; Set the LCD address to 0x27 for a 16 chars and 2 line display</font>
<b><font color="#d35400">LiquidCrystal_I2C</font></b> <b><font color="#d35400">lcd</font></b><font color="#000000">(</font><font color="#000000">0x27</font><font color="#434f54">,</font> <font color="#000000">16</font><font color="#434f54">,</font> <font color="#000000">2</font><font color="#000000">)</font><font color="#000000">;</font>

<font color="#00979c">void</font> <font color="#5e6d03">setup</font><font color="#000000">(</font><font color="#000000">)</font>
<font color="#000000">{</font>
&#09;<font color="#434f54">&#47;&#47; initialize the LCD</font>
&#09;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>

&#09;<font color="#434f54">&#47;&#47; Turn on the blacklight and print a message.</font>
&#09;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">backlight</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
&#09;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Hello, world!&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
<font color="#000000">}</font>

<font color="#00979c">void</font> <font color="#5e6d03">loop</font><font color="#000000">(</font><font color="#000000">)</font>
<font color="#000000">{</font>
&#09;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">0</font><font color="#434f54">,</font> <font color="#000000">1</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#d35400">millis</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#434f54">&#47;</font> <font color="#000000">1000</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;
<font color="#000000">}</font>

</pre>

#### Connect LCD Module with Arduino

 Demonstrates the use a 16x2 LCD display.  The I2C LiquidCrystal Module comes with 4-pins and connect them with follwing model.

 * LCD SCL - Arduino SCL
 * LCD SDA - Arduino SDA
 * LCD GND - Arduino GND
 * LCD VCC - Arduino VCC

 This sketch prints "Hello World!" to the LCD
 and shows the time.

 ![lcd connection](src/images/LCD_test.png)

<hr>

![lcd demo](src/images/lcd_demo.gif)

<hr>

### Step 3: Combine both HCSR04 and LCD Module

We tested both and now we need to combine the both hardware and progrmmes into one.

#### 3.1: Upload code.


<pre>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><font color="#d35400">Wire</font><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><b><font color="#d35400">LiquidCrystal_I2C</font></b><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>

<font color="#434f54">&#47;&#47; Set the LCD address to 0x27 for a 16 chars and 2 line display</font>
<b><font color="#d35400">LiquidCrystal_I2C</font></b> <b><font color="#d35400">lcd</font></b><font color="#000000">(</font><font color="#000000">0x27</font><font color="#434f54">,</font> <font color="#000000">16</font><font color="#434f54">,</font> <font color="#000000">2</font><font color="#000000">)</font><font color="#000000">;</font>

<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">trigPin</font> <font color="#434f54">=</font> <font color="#000000">9</font><font color="#000000">;</font> &nbsp;&nbsp;<font color="#434f54">&#47;&#47; defines Pin 9 as Trigger Pin</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">echoPin</font> <font color="#434f54">=</font> <font color="#000000">10</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; define Pin 10 as Echo Pin</font>

<font color="#434f54">&#47;&#47;define Variables</font>
<font color="#00979c">long</font> <font color="#000000">duration</font><font color="#000000">;</font>
<font color="#00979c">int</font> <font color="#000000">distance</font><font color="#000000">;</font>


<font color="#00979c">void</font> <font color="#5e6d03">setup</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>

 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">trigPin</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; Sets the trigPin as an Output</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">echoPin</font><font color="#434f54">,</font> <font color="#00979c">INPUT</font><font color="#000000">)</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; Sets the echoPin as an Input</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">9600</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Starts the serial communication</font>

 &nbsp;<font color="#434f54">&#47;&#47; initialize the LCD</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;<font color="#434f54">&#47;&#47; Turn on the blacklight and print a message.</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">backlight</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Digital Scale-cm&#34;</font><font color="#000000">)</font><font color="#000000">;</font>

<font color="#000000">}</font>
<font color="#00979c">void</font> <font color="#5e6d03">loop</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">0</font><font color="#434f54">,</font> <font color="#000000">0</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Digital Scale-cm&#34;</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">trigPin</font><font color="#434f54">,</font> <font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Clears the trigPin</font>
 &nbsp;<font color="#d35400">delayMicroseconds</font><font color="#000000">(</font><font color="#000000">2</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; wait for 2 micro second</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">trigPin</font><font color="#434f54">,</font> <font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;<font color="#434f54">&#47;&#47; Sets the trigPin on HIGH state</font>
 &nbsp;<font color="#d35400">delayMicroseconds</font><font color="#000000">(</font><font color="#000000">10</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; wait 10 micro second</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">trigPin</font><font color="#434f54">,</font> <font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; Sets the trigPin on LOW state</font>

 &nbsp;<font color="#000000">duration</font> <font color="#434f54">=</font> <font color="#d35400">pulseIn</font><font color="#000000">(</font><font color="#000000">echoPin</font><font color="#434f54">,</font> <font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; Reads the echoPin, returns the sound wave travel time in microseconds</font>

 &nbsp;<font color="#000000">distance</font> <font color="#434f54">=</font> <font color="#000000">duration</font> <font color="#434f54">*</font> <font color="#000000">0.034</font> <font color="#434f54">&#47;</font> <font color="#000000">2</font><font color="#000000">;</font> &nbsp;<font color="#434f54">&#47;&#47; Calculating the distance</font>
 &nbsp;<font color="#434f54">&#47;&#47;String dist = distance + &#34;cm&#34; ;</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Distance: &#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#000000">distance</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Prints the distance on the Serial Monitor</font>

 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">0</font><font color="#434f54">,</font> <font color="#000000">1</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;Set cursor to second line</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">distance</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Print distnace on LCD</font>

 &nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">500</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; wait 500 milli second</font>

 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">clear</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;Clear the LCD.</font>
<font color="#000000">}</font>

</pre>

<hr>

#### Wiring 

![Wiring](src/images/finalwiring.png)

<hr>

#### Final Demo 

![Demo](src/images/demo.gif)


<hr><hr>

#### ToDO

- [ ] Add button and measure only when the button pressed.

- [ ] Add buzzer and trigger when a speacial requirment.

- [ ] Designa and 3D Print Enclosure.

<hr><hr>

### Thank You, Hope you enjoyed!
Please share your feedback.









