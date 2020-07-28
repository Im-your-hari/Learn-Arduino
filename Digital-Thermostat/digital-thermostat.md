# Digital Thermostat

In this workhop we will learn how to how to make a digital thermostat to measure and display temprature and Humidity. 


### Problem Statement 

In order to measure temprature and Humidity we using online service , but the probel is that, they are getting the data not your place where you searched so value might have difference, we don't know about that. also we can't make action like turing on A/C when temperature is High/Low like that  using data from online services, for this we need absoulte data.
### Idea

What if, we have a system that can be continually monitor and display temprature and Humidity, that can also be used for trigger some actions.


### Solution

Build a device that can be controled continually monitor the temprature and Humidity and make actions like getting notification ike turing on A/C when temperature is High/Low, notification that can be help to refrigerate our food...etc.

<hr>

### Prototype Building

Build a device that can be display temprature and Humidity also can be make action depends on the temprature and Humidity .

![prototype](src/images/prototype.png)

<hr>

### Things we need

* Arduino Uno
* DHT11- Digital Humidty and Temperature Sensor
* Jumber Wires
* Breadboard

<hr>

### DHT11

The DHT11 is a basic, ultra low-cost digital temperature and humidity sensor. It uses a capacitive humidity sensor and a thermistor to measure the surrounding air, and spits out a digital signal on the data pin (no analog input pins needed). Its fairly simple to use, but requires careful timing to grab data. The only real downside of this sensor is you can only get new data from it once every 2 seconds, so when using our library, sensor readings can be up to 2 seconds old.

![dht11 pinout](src/images/dht11pin.jpg)

<hr>

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
If you are new to the arduino system, you can learn the [ Arduino basics from here](arduino-basics.md) , after reading then go to the next step. 

### Step 2: Programming

#### 2.1 Algorithm

![algorithm](src/images/alogorithm.png)

<hr>

#### 2.2 Open Arduino IDE and Start a new Sketch 

![Arduino IDE Sketch](../docs/images/arduinoide02.JPG)

#### 2.3 Read then Copy and Paste the Code

### Tesing DHT11 Sensor Module
Since the DHT11 dones't comes with arduino IDE need to add the library on Arduino IDE first. Open the Library manager from **Sketch -> Include Library- > Manage Libraries**

![inlcude lib](src/images/libManager.png)

from the follwing window search **DHT11**

![lib search](src/images/libInstall.png)

Select the **DHT Sensor library** by Adafruit, and click **Install**.so we successfully added the DHT11 library. 

<hr>

#### 2.4 Uplaod and Compaile Code

<pre>
<font color="#5e6d03">#include</font> <font color="#005c5f">&#34;DHT.h&#34;</font>

<font color="#5e6d03">#define</font> <font color="#000000">DHTPIN</font> <font color="#000000">2</font> &nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Digital pin connected to the DHT sensor</font>

<font color="#5e6d03">#define</font> <font color="#000000">DHTTYPE</font> <font color="#000000">DHT11</font> &nbsp;&nbsp;<font color="#434f54">&#47;&#47; set DHT mode to &nbsp;dht11</font>

<b><font color="#d35400">DHT</font></b> <font color="#000000">dht</font><font color="#000000">(</font><font color="#000000">DHTPIN</font><font color="#434f54">,</font> <font color="#000000">DHTTYPE</font><font color="#000000">)</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; Initialize DHT sensor with pin and mode.</font>

<font color="#00979c">void</font> <font color="#5e6d03">setup</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">9600</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">dht</font><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Initialize DHT sensor.</font>
<font color="#000000">}</font>

<font color="#00979c">void</font> <font color="#5e6d03">loop</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>

 &nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">2000</font><font color="#000000">)</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; Wait a few seconds between measurements.</font>

 &nbsp;<font color="#434f54">&#47;&#47; Reading temperature or humidity takes about 250 milliseconds!</font>
 &nbsp;<font color="#434f54">&#47;&#47; Sensor readings may also be up to 2 seconds &#39;old&#39; (its a very slow sensor)</font>
 &nbsp;<font color="#00979c">float</font> <font color="#000000">humi</font> <font color="#434f54">=</font> <font color="#000000">dht</font><font color="#434f54">.</font><font color="#d35400">readHumidity</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#434f54">&#47;&#47; Read temperature as Celsius (the default)</font>
 &nbsp;<font color="#00979c">float</font> <font color="#000000">temp</font> <font color="#434f54">=</font> <font color="#000000">dht</font><font color="#434f54">.</font><font color="#d35400">readTemperature</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Humidity: &#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">humi</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;print humudity</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34; &nbsp;&nbsp;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Temperature: &#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">temp</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>

<font color="#000000">}</font>

</pre>


#### Connect DHT11 Module with Arduino

Connect the **Data** to Arduino **Digital Pin 2** . 

![wiring](src/images/wiring.png)

After open the Serial monitor

![wiring](src/images/DHTserial.PNG)


### Tesing LCD Module.

Here we are using LCD Module with **12C addons** for I2C Communication , which will only need two wires for communication, in other way we need to use 14 pins. 

Since the I2C is a addon we need  to insert the library on Arduino IDE first. For that first downlaod the [Arduino-LiquidCrystal-I2C-library.zip](../Digital-Scale/src/lib/Arduino-LiquidCrystal-I2C-library.zip), Then click **Sketch -> Include Library -> Add .ZIP Library**

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


### Step 3: Combine both DHT11 and LCD Module

#### Read code then Upload

<pre>
<font color="#5e6d03">#include</font> <font color="#005c5f">&#34;DHT.h&#34;</font>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><font color="#d35400">Wire</font><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><b><font color="#d35400">LiquidCrystal_I2C</font></b><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>

<font color="#434f54">&#47;&#47; Set the LCD address to 0x27 for a 16 chars and 2 line display</font>
<b><font color="#d35400">LiquidCrystal_I2C</font></b> <b><font color="#d35400">lcd</font></b><font color="#000000">(</font><font color="#000000">0x27</font><font color="#434f54">,</font> <font color="#000000">16</font><font color="#434f54">,</font> <font color="#000000">2</font><font color="#000000">)</font><font color="#000000">;</font>

<font color="#5e6d03">#define</font> <font color="#000000">DHTPIN</font> <font color="#000000">2</font> &nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Digital pin connected to the DHT sensor</font>

<font color="#5e6d03">#define</font> <font color="#000000">DHTTYPE</font> <font color="#000000">DHT11</font> &nbsp;&nbsp;<font color="#434f54">&#47;&#47; set DHT mode to &nbsp;dht11</font>

<b><font color="#d35400">DHT</font></b> <font color="#000000">dht</font><font color="#000000">(</font><font color="#000000">DHTPIN</font><font color="#434f54">,</font> <font color="#000000">DHTTYPE</font><font color="#000000">)</font><font color="#000000">;</font> <font color="#434f54">&#47;&#47; Initialize DHT sensor with pin and mode.</font>

<font color="#00979c">void</font> <font color="#5e6d03">setup</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">9600</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">dht</font><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; Initialize DHT sensor.</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; initialize the LCD</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">backlight</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;<font color="#434f54">&#47;&#47; Turn on the blacklight and print a message.</font>

 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">0</font><font color="#434f54">,</font> <font color="#000000">0</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Humi Temp&#34;</font><font color="#000000">)</font><font color="#000000">;</font>

<font color="#000000">}</font>

<font color="#00979c">void</font> <font color="#5e6d03">loop</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>

 &nbsp;<font color="#434f54">&#47;&#47;delay(2000); &#47;&#47; Wait a few seconds between measurements.</font>

 &nbsp;<font color="#434f54">&#47;&#47; Reading temperature or humidity takes about 250 milliseconds!</font>
 &nbsp;<font color="#434f54">&#47;&#47; Sensor readings may also be up to 2 seconds &#39;old&#39; (its a very slow sensor)</font>
 &nbsp;<font color="#00979c">float</font> <font color="#000000">humi</font> <font color="#434f54">=</font> <font color="#000000">dht</font><font color="#434f54">.</font><font color="#d35400">readHumidity</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#434f54">&#47;&#47; Read temperature as Celsius (the default)</font>
 &nbsp;<font color="#00979c">float</font> <font color="#000000">temp</font> <font color="#434f54">=</font> <font color="#000000">dht</font><font color="#434f54">.</font><font color="#d35400">readTemperature</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Humidity: &#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">humi</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34; &nbsp;&nbsp;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Temperature: &#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">temp</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">0</font><font color="#434f54">,</font> <font color="#000000">0</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34;Humi(%) &nbsp;Temp(C)&#34;</font><font color="#000000">)</font><font color="#000000">;</font>

 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">setCursor</font><font color="#000000">(</font><font color="#000000">0</font><font color="#434f54">,</font> <font color="#000000">1</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">humi</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#005c5f">&#34; &nbsp;&nbsp;&nbsp;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">print</font><font color="#000000">(</font><font color="#000000">temp</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">2000</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<b><font color="#d35400">lcd</font></b><font color="#434f54">.</font><font color="#d35400">clear</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
<font color="#000000">}</font>

</pre>

<hr>

#### Wiring

![final wiring](src/images/final.png)

<hr>

#### Demo

![final demo](src/images/final.gif)


#### ToDO


- [ ] Add buzzer and trigger when a when temprature high.

- [ ] Design and 3D Print an Enclosure.

<hr><hr>

### Thank You, Hope you enjoyed!
Please share your feedback.
