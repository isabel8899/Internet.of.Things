# Stappenplan

## 1: Installeer telegram

Als eerst moet je de app telegram op je telefoon installeren

## 2: Maak een bot


## 3: Zoek je ID

## 4: Installeer het juiste bord
Voordat je kan beginnen is het belangrijk dat je Arduino goed is geinstalleerd door de juiste borden en libraries te hebben. We beginnen bij de borden installeren, voor deze manual heb je het bord esp8266 nodig. 
Ik had deze al geinstalleerd dus kon ik deze stap overslaan, maar als je dat nog niet hebt gebruik dan de link hieronder.

https://randomnerdtutorials.com/how-to-install-esp8266-board-arduino-ide/


## 5: Installeer de juiste libraries

## 6: Zet je code in Arduino

## 7: Pas je code aan op je eigen waarden

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

# Bronnen
- https://randomnerdtutorials.com/telegram-control-esp32-esp8266-nodemcu-outputs/
