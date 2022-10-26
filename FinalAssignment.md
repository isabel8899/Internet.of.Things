# Steps for using Google agenda to trigger your arduino
Isabel Erven 

26 - 10 - 2022

## Intro
In this manual I will walk through on how to link a google agenda event to your trigger the led light on and off. I did this by first following the steps on how to get the time from the internet, then I looked up another manual on how to link google agenda to your adafruit and lastly I wanted to link the google event to my led lights, but sadly that didn't work. So you will see in my manual only how to gain the time now and the time of your google agenda event.

## Materials
- Arduino IDE with esp 8226 fully set up
- Adafruit account 
- Zapier account
- Wi-Fi

# Steps

## Getting the current time
As I said in the intro, the first thing I did was getting the current time. I started with the manual below:
https://www.instructables.com/Getting-Time-From-Internet-Using-ESP8266-NTP-Clock/
But after I did all the steps, I found out it didn't get the actual current time. You had to fill it in yourself and then it started counting. (See the first error for more explination) 
The manual above wasn't what I was looking for. So then I used another manual:
https://randomnerdtutorials.com/esp8266-nodemcu-date-time-ntp-client-server-arduino/
Below you see the steps I did, to get the actual current time.

### 1: Install libraries

Install the library NTPclient. See the image.

![afbeelding](https://user-images.githubusercontent.com/95106559/198037407-4b290359-27aa-40fa-93ac-e3ca16e44082.png)

### 2: Add the code in arduino

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
  timeClient.setTimeOffset(0);
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


```
const char *ssid = "***********";
const char *password = "***********";
```

in your code and add your own WIFI credentials

Also search for


```
  timeClient.setTimeOffset(0);
}
```

and change the number 0 to your own time zone. You can see in the notes of the code on how to fill in your own timezone.

after this you should see the date and time in you serial monitor. See the picture below


![afbeelding](https://user-images.githubusercontent.com/95106559/198058025-546967a8-b7e4-4ad1-8ad5-aa06a97e06dd.png)

## Showing a Google agenda event in your arduino
For the second big step I made a new arduino file and followed a tutorial on how to show your upcomming Google agenda event in your arduino serial monitor.

I used this manual: https://www.instructables.com/Google-Calendar-Events-to-ESP8266/

### Step 1: Create a New feed in your adafruit account
you can do this by going to "IO > Feeds > New Feeds 


![afbeelding](https://user-images.githubusercontent.com/95106559/198136362-d48d4d8e-b292-412d-a5a7-1360b4338496.png)

### Step 2: Make a new Zap
You can do this by pressing the "create Zap" button.


![afbeelding](https://user-images.githubusercontent.com/95106559/198136861-2409239e-2127-4281-9dab-fc500021c460.png)

### Step 3: Connect your google Calander to your account
Firstly you need to search for Google calendar. There you need to follow the steps on connecting your account to Zappier by:

- choosing "event start" under "event"

- Choose your own Google account

- Under "calandar" choose one you can edit all the time (this is usefull for later)

- Under "times before" edit to 16 (first time I didn't do this and then it didn't link correctly! So don't forget)

- And then push test trigger. If you don't see your own upcomming event, then something went wrong. See error "Error with serial monitor".

### Step 4: Connect adafruit to Zappier
After adding Google Calender you need to add adafruit as well.
You start by searching for "Adafruit IO" and then following the steps

- choosing "Create Feed Data" under "event"

- Then log in with your adafruit account

- then choose the Feed that you created in step 1 under "Feed key"

- Under "Value" add "event begins" and "event end" (NOT the pretty version, that won't work with the upcomming code that we'll use) See picture below on what to choose.


![afbeelding](https://user-images.githubusercontent.com/95106559/198139362-8f7805b4-00cc-4b47-ab08-6a1a041f3772.png)

### Step 5: Test Zap
Press test zap and look in tour Adafruit feed if zappier sended a trigger. It will look like this:


![afbeelding](https://user-images.githubusercontent.com/95106559/198139694-68b11c8f-6c1a-4319-89c8-14421f4813da.png)

### Step 6: add the code to your arduino
Copy and paste the code from this github page to your own arduino:
https://github.com/SummerDanoe/ReadGoogleCalFeed/tree/master/readfeedtutorial
(so add the config AND readfeedtutorial)

### Step 7: personalize the code
in the config.h look for:

```
#define IO_USERNAME   "YOUR_USERNAME"
#define IO_KEY        "YOUR_IO_KEY"
```

and fill in your own adafruit data

also look for

```
#define WIFI_SSID   "YOUR_SSID"
#define WIFI_PASS   "YOUR_PASSWORD"
```

and fill in your own wifi

In the main file look for:

```
#define FEED_OWNER "YOUR_USERNAME"
```
and add your username from your adafruit account

and look for 

```
AdafruitIO_Feed *sharedFeed = io.feed("YOUR_FEED_NAME", FEED_OWNER);
```
and add your adafruit feed name

### Step 8: Upload your file to your board
Now the code is supposed to work and show you:


![afbeelding](https://user-images.githubusercontent.com/95106559/198140912-c3ad67ae-6fe1-4836-b18a-e6a29fa5be3f.png)
this didn't work for me, see at "error with serial monitor" on how I fixed it.

## Adding the files together
After I tried to add all codes togheter at once (see error "Playing with combining 3 files") , I did a different approach by doing it step for step.

### Step 1: Minimize what you actually need in time retrieval file
First I minimized the data I retrieved in my serial monitor. For exemple I didnt need the month or date in my time retrieval. So I deleted the following code:

After I deleted the useless code I added the line:

```
int timeNow = currentHour*60 + currentMinute + currentSecond%60;
```
This is a calculation in the current time in minutes. You will need this later.
Minimize what you actually need in Event retrieval file
### Step 2: Minimize what you actually need in event retrieval file

# Errors

### wrong timezone

The first error I got was when I tried to get the current time with the first source. The error was that my serial monitor didn't gave me the correct day and time. As you can see in the picture below.


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

But even after changing this it did work, but the code didn't give me the current time. So i looked up antoher code, witch then worked correctly.


### Error with serial monitor
When I did the step "Showing a Google agenda event in your arduino"I had multiple errors with my serial monitor. I will walk through them all in here.
The first one I had was:

![afbeelding](https://user-images.githubusercontent.com/95106559/198141401-b06c3c98-535c-4db8-b10a-bb9b1f7732b4.png)

Here it only showd that my adafruit was connected, but it didn't show my next appointment. Luckily the manual I was working with also had the most common errors lined up.

![afbeelding](https://user-images.githubusercontent.com/95106559/198141634-e39362fd-3f3d-4fe2-8e8e-3c7c7c880ec5.png)
So I walked throug them all and ended up on redooing everything. So I started at step one again and this time read everything thourough and found out that my error was at step 3. Because when I tested my google calander it showed me an actual appointment I recognized, while the first time it didn't.

So then I hoped it worked, but then the serial monitor showed me nothing. Not even that it's connected to adafruit. See below


![afbeelding](https://user-images.githubusercontent.com/95106559/198142279-b9575be1-6399-4401-9289-c25313d0066d.png)

So after playing with my wifi and adafruit. I also tried moving my event in google calander. Then I found out that only if my event was at the exact time that I was also working in my arduino. Only then it would show in my serial monitor. So then i moved my event and it finaly worked!


![afbeelding](https://user-images.githubusercontent.com/95106559/198142545-20f79190-79dd-4935-a5f6-265d80f6c996.png)
I also renamed the event and moved it some more to see if this actually was the sollution. And in the end it was, because renaming or moving the event had no other effects.

### Playing with combining 3 files
After I succesfully done step 1 "getting the current time" and step 2: "Showing a Google agenda event in your arduino" I added them both together in the same file and also added the file "FirstLight". It ended up on beeing a really big and unorganized file with many errors. For exemple the ones below:


![afbeelding](https://user-images.githubusercontent.com/95106559/198144056-072d6186-3665-40c9-b95a-9338df3a1651.png)

I wanted to solve the errors, but I knew once I solve 1, 5 more will come up. That was because my file was so unorganized and chaotic. So I scraped that idea and started again, but then adding only codes that I wrote and understand.



## sources
- https://www.instructables.com/Getting-Time-From-Internet-Using-ESP8266-NTP-Clock/
- https://randomnerdtutorials.com/esp8266-nodemcu-date-time-ntp-client-server-arduino/
- https://io.adafruit.com/
- https://zapier.com/
- https://www.instructables.com/Google-Calendar-Events-to-ESP8266/
- https://github.com/SummerDanoe/ReadGoogleCalFeed/tree/master/readfeedtutorial
