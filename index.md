---
layout: default
---

# EP1001 Further Digital Fabrication & Prototyping

[Link to another page](./another-page.html).

**Weekly Progress**

# Week 1

This is a normal paragraph following a header. GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

# Week 2

I was introduced to WOKWI which is an online electronic simulator. In WOKWI, I was able to porgram different microcontrollers with their repective programming languages to simulate circuits. For my first excersise I programmed an ESP32-C3 in C++ language. For the next 2 excersies, instead of using C++ to program, I used micropython to progam the ESP32-C3 & the RP2040. For Excersie 4 I was tasked to use Generative AI chat to create a program for the ESP32-C3 to read input values from a potentiometer and use it to control the intensity of an LED. For Excersie 5 I was tasked to use Generative AI chat to create a program for the Raspberry Pi Pico to control a neopixel ring display using a pushbutton.

For My Challenge exersice 1, I was tasked to develop a portable environmental monitoring device, comprising of an ESP32-C3 board with 128x64 OLED screen which will sample and display the ambient temperature and humidity using GEN AI to create the code and simulate it in WokWi.
The prompt that I use was "Can you create me a code for an ESP32-C3 board that uses a 128x64 OLED screen which will sample and display the ambient temperature and humidity and a DHT22 Sensor.".

### The code that I used

```C++
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include <DHT.h>

// OLED Configuration
#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_RESET    -1 // Reset pin # (or -1 if sharing Arduino reset pin)
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

// DHT22 Configuration
#define DHTPIN 2          // Digital pin connected to the DHT sensor
#define DHTTYPE DHT22     // DHT 22  (AM2302), AM2321
DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(115200);

  // Initialize DHT sensor
  dht.begin();

  // Initialize OLED display
  // Address 0x3C is common for 128x64 OLEDs
  if(!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    Serial.println(F("SSD1306 allocation failed"));
    for(;;); // Don't proceed, loop forever
  }

  display.clearDisplay();
  display.setTextColor(SSD1306_WHITE);
  display.setTextSize(1);
  display.setCursor(0,0);
  display.println("Initializing...");
  display.display();
  delay(2000);
}

void loop() {
  // Wait a few seconds between measurements
  delay(2000);

  float h = dht.readHumidity();
  float t = dht.readTemperature(); // Celsius

  // Check if any reads failed and exit early (to try again).
  if (isnan(h) || isnan(t)) {
    Serial.println(F("Failed to read from DHT sensor!"));
    return;
  }

  // Clear previous data
  display.clearDisplay();
  
  // Header
  display.setTextSize(1);
  display.setCursor(0, 0);
  display.println("ENV MONITOR");
  display.drawLine(0, 12, 128, 12, SSD1306_WHITE);

  // Display Temperature
  display.setTextSize(1);
  display.setCursor(0, 25);
  display.print("Temp: ");
  display.setTextSize(2);
  display.print(t, 1);
  display.cp437(true);
  display.write(167); // Degree symbol
  display.print("C");

  // Display Humidity
  display.setTextSize(1);
  display.setCursor(0, 50);
  display.print("Hum:  ");
  display.setTextSize(2);
  display.print(h, 1);
  display.print("%");

  // Update screen
  display.display();
}



```
For My Challenge exersice 2, I was tasked to develop a portable environmental monitoring device, comprising of an ESP32-C3 board with 128x64 OLED screen which will sample and display the ambient temperature and humidity using GEN AI to create the code and simulate it in WokWi.
The prompt that I use was "Can you create me a code for an ESP32-C3 board that uses a 128x64 OLED screen which will sample and display the ambient temperature and humidity and a DHT22 Sensor.".


#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)

