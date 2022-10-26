# Steps for sending signals through Adafruit
Isabel Erven 

26 - 10 - 2022

## Intro
In this manual I will walk through on how to

## Materials
- Arduino IDE 
- Adafruit account 

# Steps
serach send time to esp8266 with "adafruit" ----------------------------------- later verwijderen

## 1: Install libraries

Install the library NTPclient. See the image.
![afbeelding](https://user-images.githubusercontent.com/95106559/198037407-4b290359-27aa-40fa-93ac-e3ca16e44082.png)

## 2: Add code

add the code below in your arduino.

``` arduino
#include "NTPClient.h"
#include "ESP8266WiFi.h"
#include "WiFiUdp.h"

const char *ssid = "***********";
const char *password = "***********";

const long utcOffsetInSeconds = 19800;

char daysOfTheWeek[7][12] = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};

// Define NTP Client to get time
WiFiUDP ntpUDP;
NTPClient timeClient(ntpUDP, "pool.ntp.org", utcOffsetInSeconds);

void setup(){
Serial.begin(115200);

WiFi.begin(ssid, password);

while ( WiFi.status() != WL_CONNECTED ) {
delay ( 500 );
Serial.print ( "." );
}

timeClient.begin();
}

void loop() {
timeClient.update();

Serial.print(daysOfTheWeek[timeClient.getDay()]);
Serial.print(", ");
Serial.print(timeClient.getHours());
Serial.print(":");
Serial.print(timeClient.getMinutes());
Serial.print(":");
Serial.println(timeClient.getSeconds());
//Serial.println(timeClient.getFormattedTime());

delay(1000);
}
```

## 3: personalize code
search for 

const char *ssid = "***********";
const char *password = "***********";

in your code and add your own WIFI credentials

Also search for

const long utcOffsetInSeconds = 19800;

and change the number to your own time zone. You can calculate this by --------------------nog geen idee hoe, later opzoeken maybe gwn minus twee uur... kijken of dat werkt

## 4: 

# Errors

### wrong timezone

The first error I got was that my serial monitor didn't gave me the correct day and time. I already thought that would happen, because in the tutori

![afbeelding](https://user-images.githubusercontent.com/95106559/198044269-c3735647-5d0e-491b-8a65-abf2cfdd0659.png)


## sources
- https://www.instructables.com/Minimalist-IoT-Clock-using-ESP8266-Adafruitio-IFTT/ /-------------------------------/delete?
- https://www.instructables.com/Getting-Time-From-Internet-Using-ESP8266-NTP-Clock/
