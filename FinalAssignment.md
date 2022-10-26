# Steps for sending signals through Adafruit
Isabel Erven 

26 - 10 - 2022

## Intro
In this manual I will walk through on how to link a google agenda event to your trigger the led light on and off. I did this by furst following the steps on how to get the time from the internet, then I looked up another manual on how to link google agenda to your adafruit and lastly I wanted to link the google event to my led lights, but sadly that didn't work. So you will see in my manual only how to gain the time now and the time of your google agenda event.

## Materials
- Arduino IDE with esp 8226 fully set up
- Adafruit account 
- Zapier account
- Wi-Fi

# Steps

### 1: Install libraries

Install the library NTPclient. See the image.

![afbeelding](https://user-images.githubusercontent.com/95106559/198037407-4b290359-27aa-40fa-93ac-e3ca16e44082.png)

### 2: Add code

add the code below in your arduino.

``` arduino
#include <ESP8266WiFi.h>
#include <NTPClient.h>
#include <WiFiUdp.h>

// Replace with your network credentials
const char *ssid = "********";
const char *password = "********";

// Define NTP Client to get time
WiFiUDP ntpUDP;
NTPClient timeClient(ntpUDP, "pool.ntp.org");

//Week Days
String weekDays[7]={"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};

//Month names
String months[12]={"January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"};

void setup() {
  // Initialize Serial Monitor
  Serial.begin(115200);
  
  // Connect to Wi-Fi
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

// Initialize a NTPClient to get time
  timeClient.begin();
  // Set offset time in seconds to adjust for your timezone, for example:
  // GMT +1 = 3600
  // GMT +8 = 28800
  // GMT -1 = -3600
  // GMT 0 = 0
  timeClient.setTimeOffset(7200);
}

void loop() {
  timeClient.update();

  time_t epochTime = timeClient.getEpochTime();
  Serial.print("Epoch Time: ");
  Serial.println(epochTime);
  
  String formattedTime = timeClient.getFormattedTime();
  Serial.print("Formatted Time: ");
  Serial.println(formattedTime);  

  int currentHour = timeClient.getHours();
  Serial.print("Hour: ");
  Serial.println(currentHour);  

  int currentMinute = timeClient.getMinutes();
  Serial.print("Minutes: ");
  Serial.println(currentMinute); 
   
  int currentSecond = timeClient.getSeconds();
  Serial.print("Seconds: ");
  Serial.println(currentSecond);  

  String weekDay = weekDays[timeClient.getDay()];
  Serial.print("Week Day: ");
  Serial.println(weekDay);    

  //Get a time structure
  struct tm *ptm = gmtime ((time_t *)&epochTime); 

  int monthDay = ptm->tm_mday;
  Serial.print("Month day: ");
  Serial.println(monthDay);

  int currentMonth = ptm->tm_mon+1;
  Serial.print("Month: ");
  Serial.println(currentMonth);

  String currentMonthName = months[currentMonth-1];
  Serial.print("Month name: ");
  Serial.println(currentMonthName);

  int currentYear = ptm->tm_year+1900;
  Serial.print("Year: ");
  Serial.println(currentYear);

  //Print complete date:
  String currentDate = String(currentYear) + "-" + String(currentMonth) + "-" + String(monthDay);
  Serial.print("Current date: ");
  Serial.println(currentDate);

  Serial.println("");

  delay(2000);
}

```

### 3: personalize code
search for 

const char *ssid = "***********";
const char *password = "***********";

in your code and add your own WIFI credentials

Also search for

  timeClient.setTimeOffset(0);
}

and change the number 0 to your own time zone. see in the code how.


after this you should see the date and time in you serial monitor. See the picture below


![afbeelding](https://user-images.githubusercontent.com/95106559/198058025-546967a8-b7e4-4ad1-8ad5-aa06a97e06dd.png)

### 4: 

# Errors

### wrong timezone

The first error I got was that my serial monitor didn't gave me the correct day and time. As you can see in the picture below.


![afbeelding](https://user-images.githubusercontent.com/95106559/198044269-c3735647-5d0e-491b-8a65-abf2cfdd0659.png)

I already thought that would happen, because in the tutorial it said to change the number that was given, first i didn't understood how, but after playing with the numbers I figured out that you needed to use your own time at that moment for the number and that in the code I needed to change 

```
char daysOfTheWeek[7][12] = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};
```

to 

```
char daysOfTheWeek[7][12] = {"Saturday", "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday"};
```

to have the correct day.

But even after changing this it did work, but the code didn't give me th elive time. So i looked up antoher code, with then worked correctly.



## sources
- https://www.instructables.com/Getting-Time-From-Internet-Using-ESP8266-NTP-Clock/
- https://randomnerdtutorials.com/esp8266-nodemcu-date-time-ntp-client-server-arduino/
