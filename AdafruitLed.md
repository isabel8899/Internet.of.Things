# Guide to add colorpicker for Led
By Isabel Erven

Date 12 - 10 - 22

## Intro
In this guide I want to change my led lights trough a color picker in Adafruit.

## materials
- Arduino installed on computer
- arduino bord
- ledstrip

# Steps
## 1: Install thhe correct library
Search for 'Adafruit IO Arduino' and install the latest version.

![adafruit library](https://user-images.githubusercontent.com/95106559/195298950-bcf14ce7-a393-414d-9864-18aced9958fd.jpg)
![afbeelding](https://user-images.githubusercontent.com/95106559/195323470-f88a0d5a-bd13-4b2b-948b-78ac1c5ebb57.png)


## 2: Make an adafruit account
Go to 'https://io.adafruit.com/' and make an account.
After you've made an account go to the tab 'IO' and then press the key in the right corner.

![Key image](https://user-images.githubusercontent.com/95106559/195300046-88569ed1-2921-4828-adca-b06e5090df62.jpg)

Safe your key and user name.

## 3: Create color picker
In adafruit create a color picker by going to dashbord and making a new one.
Then Create a new block in the settings and make in the block a color picker witch a color of choice.

## 4: Edit code
Open in arduino the exemple 'Adafruit IO Arduino > Adafruitio_14_neopixel'. After opening the file, add your own username and key from adafruit in the config.h file.
Also add your WIFI in the config.h file.

Change in the Adafruitio_14_neopixel file the 'Pixel_PIN 5' to 'Pixel_PIN D5'

## Upload code
Upload your code and check in the serial monitor if adafruit connects to your wifi. If yes then go to adafruit to change the color of your ledstrip

# Error

### first error
De eerste error die ik tegenkwam was bij stap 4. Hier moest ik bij exemples een stukje code aanpassen. Alleen de exemple die ik nodig had, kwam niet naar voren. Als eerst dacht ik dat de fout kwam doordat ik een verouderde versie had gedownload, maar nadat ik een zip had handmatig toegevoegd aan mijn libary, meet een nieuwere versie, werkte het nog steeds niet. Na een klasgenoot te hebben gevraagd bleek dat ik de verkeerd library had gedownload. Eenmaal de juiste gedownload kon ik weer verder.
![afbeelding](https://user-images.githubusercontent.com/95106559/195435687-e33fe70f-fc96-403f-9b3e-747f3069e8cc.png)




