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

## 3:

# Errors
### hoi
