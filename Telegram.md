# Stappenplan
Ik heb de site: https://www.electromaker.io/project/view/telegram-bot-with-esp8266-154 gebruikt voor mijn manual

## 1: Installeer telegram

Als eerst moet je de app telegram op je telefoon installeren en een account maken.

## 2: Maak een bot
Na de het maken van een account moet je je eigen bot installeren. 

## 3: Zoek je ID

## 4: Installeer het juiste bord
Voordat je kan beginnen is het belangrijk dat je Arduino goed is geinstalleerd door de juiste borden en libraries te hebben. We beginnen bij de borden installeren, voor deze manual heb je het bord esp8266 nodig. 
Ik had deze al geinstalleerd dus kon ik deze stap overslaan, maar als je dat nog niet hebt gebruik dan de link hieronder.

https://randomnerdtutorials.com/how-to-install-esp8266-board-arduino-ide/


## 5: Installeer de juiste libraries

## 6: Zet je code in Arduino
Hieronder zie je de code die ik had gebruikt om het telegram te koppelen aan mijn arduino. Vergeet niet om in je eigen botcodde en wifi gegevens in te vullen.

Dit ging helaas niet perfect, bij het kopje error, vanaf error 3, merkte je wat er allemaal fout ging bij deze code.


``` Arduino
    #include <ESP8266WiFi.h>
    #include <WiFiClientSecure.h>
    #include <TelegramBot.h>
    #define LED 1
    // Initialize Wifi connection to the router
    const char* ssid     = "xxxx";
    const char* password = "yyyy";
    // Initialize Telegram BOT
    const char BotToken[] = "xxxxxxxxxxx";
    WiFiClientSecure net_ssl;
    TelegramBot bot (BotToken, net_ssl);
     // the number of the LED pin  
    void setup() 
    {  
     Serial.begin(115200);  
     while (!Serial) {}  //Start running when the serial is open 
     delay(3000);  
     // attempt to connect to Wifi network:  
     Serial.print("Connecting Wifi: ");  
     Serial.println(ssid);  
     while (WiFi.begin(ssid, password) != WL_CONNECTED) 
           {  
       Serial.print(".");  
       delay(500);  
     }  
     Serial.println("");  
     Serial.println("WiFi connected");  
     bot.begin();  
     pinMode(LED, OUTPUT);  
    }  
    void loop() 
    {  
     message m = bot.getUpdates(); // Read new messages  
     if (m.text.equals("on")) 
           {  
       digitalWrite(LED, 1);   
       bot.sendMessage(m.chat_id, "The Led is now ON");  
     }  
     else if (m.text.equals("off")) 
           {  
       digitalWrite(LED, 0);   
       bot.sendMessage(m.chat_id, "The Led is now OFF");  
     }  
    }  
```

## 7: uittesten of het werkt in telegram!

# Errors
### Error compiling for board NodeMCU 1.0 (ESP-12E Module).
Deze error was de eerste error die ik kreeg bij het gebruiken van dit stappenplan https://randomnerdtutorials.com/telegram-control-esp32-esp8266-nodemcu-outputs/.
Ik begon met deze error weg te halen door een leeg Arduino bestand te openen en te uploaden. Om te controleren of het probleem bij de hardware of software zat.
Bij het nieuwe bestand bleef de error er staan dus kon ik hieruit concluderen dat het probleem bij de hardware lag. 
Nadat ik dat wist keek ik opnieuw naar de tutorial en merkte ik dat ik stap 4 en 5 niet perfect had uitgevoert, dus ging ik dat weer opnieuuw bekijken.

###  Failed uploading: uploading error: exit status 2
![error2](https://user-images.githubusercontent.com/95106559/195098728-52d76a31-6831-4571-91a8-c88f016f641d.jpg)

fatal error occurred: This chip is ESP8266 not ESP32. Wrong --chip argument?
Deze error kreeg ik na stap 4 toen ik een esp32 bord had geinstalleerd en de tutorial volgde om te controleren of het wertke. De error spreekt best voorzich, ik had een ESP8266 chip aangesloten ipv een esp32 en voor mijn opdracht heb ik ook geen esp32 chip gekregen, dus kon ik uberhaupt de eerste tutorial niet gebruiken

### StaticJsonBuffer is a class from ArduinoJson 5. Please see https://arduinojson.org/upgrade to learn how to upgrade your program to ArduinoJson version 6
enmaal een nieuwe tutorial begonnen die alleen een ESP8266 chip gebruikt kwam ik al snel bij de volgende error terecht:
E![error3](https://user-images.githubusercontent.com/95106559/195110969-ab83bda5-fc43-4d7d-8337-af88c07b9162.jpg)

Deze error kon ik oplossen door bij library mangager mijn arduinoJson bestand te downgraden naar een 5.13.5. Zo werkte de geschreven code namelijk weer wel.
https://arduinojson.org/v6/error/jsonbuffer-is-a-class-from-arduinojson-5/

![arduinojson](https://user-images.githubusercontent.com/95106559/195114105-d886c5ac-f5b2-416a-89bc-8d339d0e5343.jpg)

Door de arduinoJson bestand te downgraden naar 5.13.5 verdwenen alle errors gelijk, waardoor nu ik nu wel de code kon uploaden naar mijn arduino.

### Telegram doet niks
Nadat mijn code eindelijk geen errors meer gaf en ik uitteste of telegram werkte gebeurde er helemaal niks. 
Ik heb de app opnieuw geinstalleerd, alleen werkte dat helaas niet. Ook heb ik de chat opnieuw opgestart.
Ik denk zelf dat de error is ontstaan, doordat er een verkeerde led input is en er daarom niks veranderd. Dit kan ik helaas niet oplossen in mijn eentje, dus laat ik het hierbij.


# Bronnen
- https://randomnerdtutorials.com/telegram-control-esp32-esp8266-nodemcu-outputs/
- https://randomnerdtutorials.com/how-to-install-esp8266-board-arduino-ide/
- https://www.electromaker.io/project/view/telegram-bot-with-esp8266-154
- https://arduinojson.org/v6/error/jsonbuffer-is-a-class-from-arduinojson-5/
