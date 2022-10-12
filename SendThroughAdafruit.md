# Steps for sending signals through Adafruit
Isabel Erven & Sophie Bouman

12 - 10 - 22

## Intro
In this manual I will walk through on how to give a signal through a button from pc to pc.

## Materials
- Arduino IDE 2x
- Push button
- Adafruit account 2x

# Steps
## 1: Create feed
First you need to have an adafruit account. I already had one, so I skipped this step. In your adafruit account you need to make a new feed called 'kussiekussielove'.

## 2: Create example file in arduino
After you've made an new feed in adafruit the first person with the button needs to open:

examples > adafruit io > Adafruitio_20_shared_feed_write


Here we only had to add:

In Adafruitio_20_shared_feed_write.ino:

#define BUTTON_PIN D5 
#define FEED_OWNER "*****" 
AdafruitIO_Feed sharedFeed = io.feed("**FEED NAME*", FEED_OWNER); 
In config.h:

#define IO_USERNAME  "*****"
#define IO_KEY       "*******"
#define WIFI_SSID "*******"
#define WIFI_PASS "******"


And the one without the button went to:

examples > adafruit io > Adafruitio_21_feed_read

In Adafruitio_21_feed_read:

#define FEED_OWNER "*****" 
AdafruitIO_Feed sharedFeed = io.feed("**FEED NAME*", FEED_OWNER); 

In config.h:

#define IO_USERNAME  "*****"
#define IO_KEY       "*******"
#define WIFI_SSID "*******"
#define WIFI_PASS "******"

## 3: Connect button to arduino
After you fixed the exemple forms, you need to attach the butoon to your arduino. 

Add the button to the Arduino board (Red to 3.3, Black to gnd, yellow to D0)

## 4: check if button works

# Errors
### Button didn't work
The first error we had was when we filled in the exemple file, but nothing happend in the serial monitor. We quikly found out we had the wrong exemple file. We used Arduino example 07, but we needed to use 20 (for the one with the button) and 21 (The one without the button).

### Upload error
![afbeelding](https://user-images.githubusercontent.com/95106559/195335310-6eb8b560-6fc6-48b5-ad13-0a213d561700.png)
The second error we found was easy. First when we read it, we didn't know what went wrong, but as soon as we looked it up, we found out we didn't had the good port selected.

### signals didn't go to other pc
The last error we had was when we pushed the button on one pc, but nothing append on the other persons pc. After looking at the code, we saw that we typed the user name wrong. So that was easily fixed.
