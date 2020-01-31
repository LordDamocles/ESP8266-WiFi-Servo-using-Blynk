# ESP8266 Servo using Blynk over WiFi
A simple servo project used to toggle a switch or button using Blynk.

My application here was to use a servo to push the on/off button for my Air Conditioner controller. Since Australian HVAC systems are more advanced when compared to the US systems, one couldn't just purchase a Nest and call it a day.

## Hardware Required:
- D1 Mini (ESP8266) [AliExpress](https://www.aliexpress.com/item/33036965281.html?spm=a2g0s.9042311.0.0.6b304c4d82dx4m)
- SG90 Servo [AliExpress](https://www.aliexpress.com/item/32278992782.html?spm=2114.12010615.8148356.3.755726d9OKTWID)
- Jumper Wires
- Breadboard (for prototyping)
- WiFi Network

## Software Required:
- Blynk App (head to your App Store)
- [Python](https://www.python.org/downloads/)
- [WeMos D1 Mini Driver CH340](https://docs.wemos.cc/en/latest/ch340_driver.html)
- [Arduino IDE](https://www.arduino.cc/en/main/software) + Libraries

## Method
### Blynk
1. Download and create a Blynk account. Remember, this can only be done from their mobile app.
2. Create a 'New Project' and give your project a name. Then, choose the device you're using. In this case, we're using an ESP8266. Of course, choose dark mode and click 'Create'.
3. Once created, a Token will be emailed to you. Keep this handy!
4. Ok, So now you're ready to design the function. In this case, we simply want a button to toggle the servo to go to one position and then return to 0. For this, will use the 'Button' widget. To add this, click on the plus '+' icon on the top bar and select 'Button'. If you wanted a slider to move the servo as you slide, select the 'Slider' widget.
5. Select the widget and give it a name, like 'Servo'. Under 'Output', click on 'PIN' and change to 'Virtual'. On the other side, change 'PIN' to 'V3' and click ok. This value (V3) will be reflected in our script later. Next to 'Output', you'll want to change the '1' value to the position you want your servo to go to when you activate it. This number will need to be between 0-180, so lets just go with 90 for the time being. Change the mode from 'Push' to 'Switch' and click the back arrow in the top left.

### Hardware
1. Take your D1 Mini and, using some jumper wires, add a wire to Pin G, 3v3 and D8. If you're using a Breadboard you can pin these into it and connect up your servo using the below diagram. Otherwise:
- G (Ground) will go to the Brown / Black pin of the servo.
- 3V3 (3 Volts) will go to the Red pin of the servo.
- D8 (GPIO8 / Pin 14) will go to the Orange pin of the servo.
<a href="https://ibb.co/xfV1x1V"><img src="https://i.ibb.co/nnh7x7h/Untitled-1.png" alt="Untitled-1" border="0"></a>
2. Plug the D1 Mini into your computer using a USB Micro B cable.

### Arduino
#### Arduino Libraries
1. First, we'll add the ESP8266 boards as an option. To do this, open up Arduino and head to the Preferences tab. In the space to the right of 'Additional Boards manager URLs' copy and paste the below and click 'OK'.
```
https://arduino.esp8266.com/stable/package_esp8266com_index.json
```
2. Lets add the Libraries. Under 'Sketch', click 'Include Library' then 'Manage Libraries'. In the search bar, enter the below and install one by one.
- Blynk
- Blynk_WiFiManager
- Adafruit Circuit Playground

3. Under 'Tools' click on 'Board' and select 'WeMos D1 R1'.
4. Again, Under 'Tools' click on 'Port'. For Windows PC's, you'd want to select the highest COM number. For MacOS users, select '/dev/cu.wchusbserialfd140'.

#### Arduino IDE
1. After downloading the Arduino IDE program, Python and the CH340 Driver, open up Arduino. Copy and paste the provided script into Arduino and enter your data. That being your Blynk Token (emailed to you), WiFi Name and Password.
```
char auth[] = "HERE";   //Blynk API key.
char ssid[] = "HERE";    // WiFi SSID (Name).
char pass[] = "HERE";   // WiFi Password.
```
2. The remainder of the script can be left as-is. 

3. The very last thing you might need to change is the Virtual Pin that was specified in the previous section. If you didn't use 'V3', then alter the section shown below and replace where it says V3 with what you used.
```
BLYNK_WRITE(V3)   // Blynk Virtual Pin.
```
4. Once the above has been sorted, you can test your script by clicking the checkmark / tick in the top left corner. This will run through your script and make sure it works. Once it's finished and it works, it'll say 'Done Compiling' and we're ready to go.

6. What we want to do now is write this script to the D1 Mini. Every time we make a change to the script we'll have to do this. Next to the checkmark / tick in the top left corner is an arrow that will upload the script. Click this and wait until 'Done Compiling' is shown.

### Finishing Up
With the script now loaded onto the D1 Mini we can now head back over to the Blynk app and try it out. In the top right hand corner of the project they'll be a play button, click that and the project will be live. You can now toggle the button on and off.

### What Now?
From here I need to design and 3D Print a housing and bracket for this to sit on the wall next to my Air Conditioner controller. In addition, I'd like to figure out how this could integrate with Home Assistant (Hass.io) so it can see temperature readings throughout my home and activate without my input.

### Thanks To:
- Pete Knight on the Blynk Forums
- Dave Bodnar's [Video](https://youtu.be/urd_OQhizIw)
- Bitluni's Lab's [Video](https://youtu.be/migRN4P1wGI)
