# **My First Time On GitHub - Jack McRogers**
<!--
Welcome to your project page for Electronics for the Rest of Us. You'll use this page to describe and showcase your work throughout the module. 
A place for each deliverable has been created below for you in this markdown document. 
Note that comments (such as this) will not appear in the final markdown document (which you can view with the "Preview" button).
-->


## Day 1: Reflection
<!--
In this section, provide a ~250 word reflection on your first day of the module, and discuss why you're interested in this module and what you hope to take away from it.

You're also asked to insert a photo that represents your accomplishments on your first day. 
- Take a photo of you working or one of your circuits and upload it to the /docs/images/ folder of this repository. 
- Then, insert your photo into your document by modifying the markdown example that has been inserted below.
-->
Jack McRogers - 400083804

Inspire 1A03 - Electronics for the Rest of Us

Professor Jay Brodeur

Tuesday, May 26, 2020

                                             **Reflection #1**
   During day 1 of the module Electronics for the Rest of Us I was throughly impressed with what I had been able to accomplish and learn in the short 2 hours. In my mind electronics and technology has always been a very daunting thing, and despite my interest I have never even attempted to understand it. That being considered I must admit it was absolutely thrilling and rewarding to build my first circuit and see the little red LED light illuminate on my breadboard. For me it was particularly interesting to learn about how the button works. I had always had a rough guess at how the mechanics of something like that may work and it was very satisfying to have my hypothesis confirmed. I now understand that when the button is pushed that a gate inside becomes closed allowing for current to run through and complete the circuit. This made me realize that light switches must use a very similar mechanism as this button. A seemingly obvious connection between what I had just learned in class and the real world. But then I got thinking that countless other everyday devices must also use something similar to this “button” interface technology to interact with users. Some of the first items that came to mind were a kettle, toaster, and blender. But when considering an object with different settings like a fan I wondered if depending on what button you pushed it completed a different circuit with a different strength resistor within. I believe that is why I am interested in this module, I like learning about basic technology and wondering about all the applications in the real world and how you would modify them. From this module I would like to take away a deeper understanding of the technology in the world around me.

![Jack and His Circuit](https://github.com/inspire-1a03/intersession-2020-jmcrogers/blob/master/docs/images/IMG_0721.jpeg "Built my first ever circuit")

## Day 2: Results
<!--
Upload your fully-commented Arduino sketch from your final Day 2 build task--a thermometer connected to an RDB LED--into your GitHub repository.
Provide a short (~150 words) summary of your work on this circuit:
- How does your device work?
- What was challenging? 
- What worked? What didn't? 
- Be sure to link to your code (in your GitHub repository) in the text of your response.
-->

Jack McRogers - 400083804
Inspire 1A03 - Electronics for the Rest of Us
Professor Jay Brodeur
Tuesday, May 26, 2020
                                            **Reflection #2**
	This device uses thermistor to vary the resistance in the circuit which connects to the Ardunio. That voltage change is then used to calculate a temperature, this temperature is then reflected in the colour change of the LED. I found the most challenge portion of this activity was combining the code from the Thermistor into the RGB LED script using the Ardunio software. I struggled with the coding as every time I hit verify it came back with an error message and wouldn’t allow me to upload it to the Ardunio. The if/elseif/else prompted further issues and confusion. As this was my first time coding I did not understand the issue. After some research and conversing with a friend he put it simply that the code needs to be in a specific langue that the computer understands. What worked for me was trial and error. When I tried to verify and it stopped me I would trouble shoot that error until it resolved. What didn’t work for me was trying to rewire the board. I found more often that not I was able to follow the diagrams to build my board properly but sometimes wasted time rearranging when the issue really lay elsewhere.
  

/*
Adafruit Arduino - Lesson 3. RGB LED
*/

int redPin = 11;
int greenPin = 10;
int bluePin = 9;

//uncomment this line if using a Common Anode LED
//#define COMMON_ANODE

#include <math.h>

#define ThermistorPIN 0                 // Analog Pin 0

float vcc = 4.91;                       // only used for display purposes, if used
                                        // set to the measured Vcc.
float pad = 9850;                       // balance/pad resistor value, set this to
                                        // the measured resistance of your pad resistor
float thermr = 10000;                   // thermistor nominal resistance

float Thermistor(int RawADC) {
  long Resistance;  
  float Temp;  // Dual-Purpose variable to save space.

  Resistance=pad*((1024.0 / RawADC) - 1); 
  Temp = log(Resistance); // Saving the Log(resistance) so not to calculate  it 4 times later
  Temp = 1 / (0.001129148 + (0.000234125 * Temp) + (0.0000000876741 * Temp * Temp * Temp));
  Temp = Temp - 273.15;  // Convert Kelvin to Celsius                      

  // BEGIN- Remove these lines for the function not to display anything
  //Serial.print("ADC: "); 
  //Serial.print(RawADC); 
  //Serial.print("/1024");                           // Print out RAW ADC Number
  //Serial.print(", vcc: ");
  //Serial.print(vcc,2);
  //Serial.print(", pad: ");
  //Serial.print(pad/1000,3);
  //Serial.print(" Kohms, Volts: "); 
  //Serial.print(((RawADC*vcc)/1024.0),3);   
  //Serial.print(", Resistance: "); 
  //Serial.print(Resistance);
  //Serial.print(" ohms, ");
  // END- Remove these lines for the function not to display anything

  // Uncomment this line for the function to return Fahrenheit instead.
  //temp = (Temp * 9.0)/ 5.0 + 32.0;                  // Convert to Fahrenheit
  return Temp;                                      // Return the Temperature
}

void setup()
{
  Serial.begin(115200);
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);  
}

void loop()
{
if(temp > 22 and temp < 25) 
{
  setColor(255, 0, 0);  // red
}
else if(temp > 25)
{
  setColor(0, 255, 0);  // green
}
else
{
  setColor(0, 0, 255); //blue
}

  delay(2000);
}

void setColor(int red, int green, int blue)
{
  #ifdef COMMON_ANODE
    red = 255 - red;
    green = 255 - green;
    blue = 255 - blue;
  #endif
  analogWrite(redPin, red);
  analogWrite(greenPin, green);
  analogWrite(bluePin, blue); 
   float temp;
  temp=Thermistor(analogRead(ThermistorPIN));       // read ADC and  convert it to Celsius
  Serial.print("Celsius: "); 
  Serial.print(temp,1);                             // display Celsius
  //temp = (temp * 9.0)/ 5.0 + 32.0;                  // converts to  Fahrenheit
  //Serial.print(", Fahrenheit: "); 
  //Serial.print(temp,1);                             // display  Fahrenheit
  Serial.println("");                                   
  delay(5000);                                      // Delay a bit... 
}
## Arduino build-off results
<!--
Upload your fully-commented Arduino sketch from the final product of your Arduino build-off into the top-level of your module GitHub repository.
In ~300 words, provide a final device description and product pitch: 
- What does it do? Use a table (created in markdown) to list and describe the features. You can use the template provided below. 
- Describe briefly how it works.
- How could it be used in everyday life (or maybe just in rare cases)? 
- Be sure to link to your code (in your GitHub repository) in the text of your response.
- Include a snippet of code using the ``` ``` characters to display the code properly. 
Finally, record a short (30 second) video of a 'product pitch' for your device. 
- Upload the video to Youtube, and use the sample code below to embed your video.
-->


<!--
Below is a general markdown table template. 
You can find more information at these links: 
- https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#tables

-->
| Feature | Description | Other Notes |
|---------|-------------|-------------|
|         |             |             |
|         |             |             |
|         |             |             |
|         |             |             |


<!--
Below is an example of embedding a YouTube video in a markdown document for use in GitHub pages. 
Note that this video won't show when previewing the document in GitHub--it only works on the GitHub pages webpage. 
- Once your YouTube video is uploaded, right click and select ```<> Copy embed code```. 
- You can paste this code directly into your markdown document. 
- Note that you may want to adjust the width and height parameters to make it fit well in your webpage
-->

<iframe width="789" height="444" src="https://www.youtube.com/embed/dQw4w9WgXcQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Final reflection & summary
<!--
In ~300 words:
- Summarize your experience in this module. What you learned, what you liked, what you found challenging.
- Reflect upon your learning and its relevance in your life.
-->
