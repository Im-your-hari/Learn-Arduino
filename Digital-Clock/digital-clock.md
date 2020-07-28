# Digital Clock

In this workhop we will learn how to how to make a digital clock using arduino and RTC module. 


### Objective 

Build a digitalClock using arduino and RTC module, that will keep the time even arduino is turne off . 


### Prototype Building

Here we are using an Arduino as controller and DS323 Real Time Clock module to Count and keep the time and 16x2 LCD Display to Display the Time and Date. 

![digram](src/images/diagram.png)



### Things we need 

1. Arduino Uno
2. Real Time Clock Module
3. 16x2 LCD Module
4. 10k ohm potentiometer
5. 220 ohm resistor
6. Jumper Wires
7. Breadboard

<hr>

#### DS3231 Real Time Clock

![ds321](src/images/ds.jpeg)

The **DS3231** is a low-cost, highly accurate Real Time Clock which can maintain hours, minutes and seconds, as well as, day, month and year information. Also, it has automatic compensation for leap-years and for months with fewer than 31 days.

The module can work on either 3.3 or 5 V which makes it suitable for many development platforms or microcontrollers. The battery input is 3V and a typical CR2032 3V battery can power the module and maintain the information for more than a year.

The module uses the I2C Communication Protocol which makes the connection to the Arduino Board very easy.

#### LCD Module
An LCD is an electronic display module which uses liquid crystal to produce a visible image. The 16×2 LCD display is a very basic module commonly used in DIYs and circuits. The 16×2 translates o a display 16 characters per line in 2 such lines. In this LCD each character is displayed in a 5×7 pixel matrix.

![LCD Pinout](../Digital-Scale/src/images/lcd_pinouts.png)

#### Pin Description 

![LCD Pin Description](../Digital-Scale/src/images/lcd_pinouts_des.png)

<hr>

### Step 1: Arduino Setup

#### 1.1: Install Arduino IDE

Download the [Arduino IDE](https://www.arduino.cc/en/Main/Software) and install it on your computer.

![Arduino IDE Download](../docs/images/arduinoide01.JPG)

#### 1.2 walk-through the Arduino Introduction page to learn basics
If you are new to the arduino system, you can learn the [ Arduino basics from here](Arduino-basics/arduino-basics.md) , after reading then go to the next step.

### Step 2: Programming

#### 2.1 Algorithm

![algorithm](src/images/alogo.png)

<hr>

#### 2.2 Open Arduino IDE and Start a new Sketch 

![Arduino IDE Sketch](../docs/images/arduinoide02.JPG)

#### 2.3 Read then Copy and Paste the Code

#### Testing the RTC Module.

To test the RTC you need to downlaod two Arduino Library.

* [DS1307RTC Library](https://github.com/PaulStoffregen/DS1307RTC): [click here to download](https://github.com/PaulStoffregen/DS1307RTC/archive/master.zip)

* [Time Library](https://github.com/PaulStoffregen/Time): [click here to download](https://github.com/PaulStoffregen/Time/archive/master.zip)

after downlaoding we need to add the libraries into arduino ide. for that open Libraray manager by clicking **Sketch -> Include Library -> Add .ZIP Library**

![add lib](src/images/libManager.png)

Click the **Add .ZIP Library** 

![ add lib 1](src/images/libManage02.png)

#### SetTime

First we need to set the RTC Module Time, for that insert Coin (CR2032) Cell battery on RTC Module and Connct with Arduino Uno.

![pinOut](src/images/setTime_PinOut.png)

#### Upload Sktech 

<pre>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><font color="#d35400">Wire</font><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><font color="#d35400">TimeLib</font><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><font color="#000000">DS1307RTC</font><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>

<font color="#00979c">const</font> <font color="#00979c">char</font> <font color="#434f54">*</font><font color="#000000">monthName</font><font color="#000000">[</font><font color="#000000">12</font><font color="#000000">]</font> <font color="#434f54">=</font> <font color="#000000">{</font>
 &nbsp;<font color="#005c5f">&#34;Jan&#34;</font><font color="#434f54">,</font> <font color="#005c5f">&#34;Feb&#34;</font><font color="#434f54">,</font> <font color="#005c5f">&#34;Mar&#34;</font><font color="#434f54">,</font> <font color="#005c5f">&#34;Apr&#34;</font><font color="#434f54">,</font> <font color="#005c5f">&#34;May&#34;</font><font color="#434f54">,</font> <font color="#005c5f">&#34;Jun&#34;</font><font color="#434f54">,</font>
 &nbsp;<font color="#005c5f">&#34;Jul&#34;</font><font color="#434f54">,</font> <font color="#005c5f">&#34;Aug&#34;</font><font color="#434f54">,</font> <font color="#005c5f">&#34;Sep&#34;</font><font color="#434f54">,</font> <font color="#005c5f">&#34;Oct&#34;</font><font color="#434f54">,</font> <font color="#005c5f">&#34;Nov&#34;</font><font color="#434f54">,</font> <font color="#005c5f">&#34;Dec&#34;</font>
<font color="#000000">}</font><font color="#000000">;</font>

<font color="#000000">tmElements_t</font> <font color="#000000">tm</font><font color="#000000">;</font>

<font color="#00979c">void</font> <font color="#5e6d03">setup</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;<font color="#00979c">bool</font> <font color="#d35400">parse</font><font color="#434f54">=</font><font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">bool</font> <font color="#d35400">config</font><font color="#434f54">=</font><font color="#00979c">false</font><font color="#000000">;</font>

 &nbsp;<font color="#434f54">&#47;&#47; get the date and time the compiler was run</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">getDate</font><font color="#000000">(</font><font color="#5e6d03">__DATE__</font><font color="#000000">)</font> <font color="#434f54">&amp;&amp;</font> <font color="#d35400">getTime</font><font color="#000000">(</font><font color="#5e6d03">__TIME__</font><font color="#000000">)</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">parse</font> <font color="#434f54">=</font> <font color="#00979c">true</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; and configure the RTC with this info</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">RTC</font><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#000000">)</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#d35400">config</font> <font color="#434f54">=</font> <font color="#00979c">true</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#000000">}</font>

 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">9600</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">while</font> <font color="#000000">(</font><font color="#434f54">!</font><b><font color="#d35400">Serial</font></b><font color="#000000">)</font> <font color="#000000">;</font> <font color="#434f54">&#47;&#47; wait for Arduino Serial Monitor</font>
 &nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">200</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">parse</font> <font color="#434f54">&amp;&amp;</font> <font color="#d35400">config</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;DS1307 configured Time=&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#5e6d03">__TIME__</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;, Date=&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#5e6d03">__DATE__</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font> <font color="#5e6d03">else</font> <font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">parse</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;DS1307 Communication Error :-{&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;Please check your circuitry&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font> <font color="#5e6d03">else</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Could not parse info from the compiler, Time=\&#34;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#5e6d03">__TIME__</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;\&#34;, Date=\&#34;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#5e6d03">__DATE__</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;\&#34;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
<font color="#000000">}</font>

<font color="#00979c">void</font> <font color="#5e6d03">loop</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>
<font color="#000000">}</font>

<font color="#00979c">bool</font> <font color="#d35400">getTime</font><font color="#000000">(</font><font color="#00979c">const</font> <font color="#00979c">char</font> <font color="#434f54">*</font><font color="#000000">str</font><font color="#000000">)</font>
<font color="#000000">{</font>
 &nbsp;<font color="#00979c">int</font> <font color="#000000">Hour</font><font color="#434f54">,</font> <font color="#000000">Min</font><font color="#434f54">,</font> <font color="#000000">Sec</font><font color="#000000">;</font>

 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">sscanf</font><font color="#000000">(</font><font color="#000000">str</font><font color="#434f54">,</font> <font color="#005c5f">&#34;%d:%d:%d&#34;</font><font color="#434f54">,</font> <font color="#434f54">&amp;</font><font color="#000000">Hour</font><font color="#434f54">,</font> <font color="#434f54">&amp;</font><font color="#000000">Min</font><font color="#434f54">,</font> <font color="#434f54">&amp;</font><font color="#000000">Sec</font><font color="#000000">)</font> <font color="#434f54">!=</font> <font color="#000000">3</font><font color="#000000">)</font> <font color="#5e6d03">return</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Hour</font> <font color="#434f54">=</font> <font color="#000000">Hour</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Minute</font> <font color="#434f54">=</font> <font color="#000000">Min</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Second</font> <font color="#434f54">=</font> <font color="#000000">Sec</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">return</font> <font color="#00979c">true</font><font color="#000000">;</font>
<font color="#000000">}</font>

<font color="#00979c">bool</font> <font color="#000000">getDate</font><font color="#000000">(</font><font color="#00979c">const</font> <font color="#00979c">char</font> <font color="#434f54">*</font><font color="#000000">str</font><font color="#000000">)</font>
<font color="#000000">{</font>
 &nbsp;<font color="#00979c">char</font> <font color="#000000">Month</font><font color="#000000">[</font><font color="#000000">12</font><font color="#000000">]</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">int</font> <font color="#000000">Day</font><font color="#434f54">,</font> <font color="#000000">Year</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">uint8_t</font> <font color="#000000">monthIndex</font><font color="#000000">;</font>

 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">sscanf</font><font color="#000000">(</font><font color="#000000">str</font><font color="#434f54">,</font> <font color="#005c5f">&#34;%s %d %d&#34;</font><font color="#434f54">,</font> <font color="#000000">Month</font><font color="#434f54">,</font> <font color="#434f54">&amp;</font><font color="#000000">Day</font><font color="#434f54">,</font> <font color="#434f54">&amp;</font><font color="#000000">Year</font><font color="#000000">)</font> <font color="#434f54">!=</font> <font color="#000000">3</font><font color="#000000">)</font> <font color="#5e6d03">return</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">for</font> <font color="#000000">(</font><font color="#000000">monthIndex</font> <font color="#434f54">=</font> <font color="#000000">0</font><font color="#000000">;</font> <font color="#000000">monthIndex</font> <font color="#434f54">&lt;</font> <font color="#000000">12</font><font color="#000000">;</font> <font color="#000000">monthIndex</font><font color="#434f54">++</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">strcmp</font><font color="#000000">(</font><font color="#000000">Month</font><font color="#434f54">,</font> <font color="#000000">monthName</font><font color="#000000">[</font><font color="#000000">monthIndex</font><font color="#000000">]</font><font color="#000000">)</font> <font color="#434f54">==</font> <font color="#000000">0</font><font color="#000000">)</font> <font color="#5e6d03">break</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">monthIndex</font> <font color="#434f54">&gt;=</font> <font color="#000000">12</font><font color="#000000">)</font> <font color="#5e6d03">return</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Day</font> <font color="#434f54">=</font> <font color="#000000">Day</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Month</font> <font color="#434f54">=</font> <font color="#000000">monthIndex</font> <font color="#434f54">+</font> <font color="#000000">1</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Year</font> <font color="#434f54">=</font> <font color="#000000">CalendarYrToTm</font><font color="#000000">(</font><font color="#000000">Year</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">return</font> <font color="#00979c">true</font><font color="#000000">;</font>
<font color="#000000">}</font>


</pre>

Upload the sktech and open the Serial Monitor and it will shows like this

``DS1307 configured Time=11:24:26, Date=Mar 10 2020``

That means our RTC module is set with the time.

<hr>

### Tesing LCD Module

Here we are using LCD Module with **12C addons** for I2C Communication , which will only need two wires for communication, in other way we need to use 14 pins. 

Since the I2C is a addon we need  to insert the library on Arduino IDE first. For that first downlaod the [Arduino-LiquidCrystal-I2C-library.zip](src/lib/Arduino-LiquidCrystal-I2C-library.zip), Then click **Sketch -> Include Library -> Add .ZIP Library**

![inlcude lib](../Digital-Scale/src/images/includeLib.png)

then select the **.Zip** file and click open.
![add zip file](../Digital-Scale/src/images/openLib.png)

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

 ![lcd connection](../Digital-Scale/src/images/LCD_test.png)

<hr>

![lcd demo](../Digital-Scale/src/images/lcd_demo.gif)

<hr>

### Step 3: Combine both RTC and LCD Module Sktech

We tested both and now we need to combine the both hardware and progrmmes into one.

### Pin Diagram.

![pin diagram](src/images/finalPinOut.png)

Connect the RTC and I2C LCD module with the arduino using same VCC and GND also , we can use same SDA and SCL since I2C based on I2C 

#### Sketch.

<pre>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><font color="#d35400">Wire</font><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><b><font color="#d35400">LiquidCrystal_I2C</font></b><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><font color="#d35400">TimeLib</font><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><font color="#000000">DS1307RTC</font><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>

<font color="#434f54">&#47;&#47; Set the LCD address to 0x27 for a 16 chars and 2 line display</font>
<b><font color="#d35400">LiquidCrystal_I2C</font></b> <b><font color="#d35400">lcd</font></b><font color="#000000">(</font><font color="#000000">0x27</font><font color="#434f54">,</font> <font color="#000000">16</font><font color="#434f54">,</font> <font color="#000000">2</font><font color="#000000">)</font><font color="#000000">;</font>

<font color="#00979c">void</font> <font color="#5e6d03">setup</font><font color="#000000">(</font><font color="#000000">)</font>
<font color="#000000">{</font>
 &nbsp;<font color="#434f54">&#47;&#47; initialize the LCD</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">9600</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#434f54">&#47;&#47; Turn on the blacklight and print a message.</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">backlight</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>

<font color="#000000">}</font>

<font color="#00979c">void</font> <font color="#5e6d03">loop</font><font color="#000000">(</font><font color="#000000">)</font>
<font color="#000000">{</font>
 &nbsp;<font color="#000000">tmElements_t</font> <font color="#000000">tm</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">RTC</font><font color="#434f54">.</font><font color="#d35400">read</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#000000">)</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">0</font><font color="#434f54">,</font> <font color="#000000">0</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Time: &nbsp;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Hour</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#00979c">&#39;:&#39;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Minute</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#00979c">&#39;:&#39;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Second</font><font color="#000000">)</font><font color="#000000">;</font>


 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Time: &nbsp;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Hour</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#00979c">&#39;:&#39;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Minute</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#00979c">&#39;:&#39;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Second</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">0</font><font color="#434f54">,</font> <font color="#000000">1</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Date: &nbsp;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Day</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#00979c">&#39;&#47;&#39;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Month</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#00979c">&#39;&#47;&#39;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tmYearToCalendar</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Year</font><font color="#000000">)</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Ok, Time = &#34;</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;&nbsp;&nbsp;<font color="#000000">print2digits</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Hour</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#00979c">&#39;:&#39;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">print2digits</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Minute</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#00979c">&#39;:&#39;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">print2digits</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Second</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;, Date (D&#47;M&#47;Y) = &#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Day</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#00979c">&#39;&#47;&#39;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Month</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#00979c">&#39;&#47;&#39;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">tmYearToCalendar</font><font color="#000000">(</font><font color="#000000">tm</font><font color="#434f54">.</font><font color="#000000">Year</font><font color="#000000">)</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>


 &nbsp;&nbsp;&nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">1000</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">clear</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#5e6d03">else</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">RTC</font><font color="#434f54">.</font><font color="#d35400">chipPresent</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;The DS1307 is stopped. &nbsp;Please run the SetTime&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;example to initialize the time and begin running.&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;run SetTime&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">clear</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">else</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;DS1307 read error! &nbsp;Please check the circuitry.&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;RTC Error&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">clear</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">9000</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
<font color="#000000">}</font>

<font color="#00979c">void</font> <font color="#000000">print2digits</font><font color="#000000">(</font><font color="#00979c">int</font> <font color="#000000">number</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">number</font> <font color="#434f54">&gt;=</font> <font color="#000000">0</font> <font color="#434f54">&amp;&amp;</font> <font color="#000000">number</font> <font color="#434f54">&lt;</font> <font color="#000000">10</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#00979c">&#39;0&#39;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">number</font><font color="#000000">)</font><font color="#000000">;</font>
<font color="#000000">}</font>

</pre>

Upload the sketch to the arduino and connect power. 

<hr>

#### Final Demo

![Demo](src/images/demo.gif)

<hr><hr>

#### ToDO

- [ ] Add button to display time when only the button pressed.

- [ ] Add buzzer and set alarms.

- [ ] Designa and 3D Print Enclosure.

<hr><hr>

### Thank You, Hope you enjoyed!
Please share your feedback.



