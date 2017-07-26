# Enschedata

Enschedata is een data platform waar data van sensoren via TTN gepusht kunnen worden. Het platform is te vinden op http://enschedata.nl

## Gebruik

### Bouw een LoRa node  ;)
Zie bijvoorbeeld: [https://github.com/TTNEnschede/SensorNode](https://github.com/TTNEnschede/SensorNode)

### Payload function.
Wanneer de data van de node succesvol door de TTN backend wordt ontvangen moet het worden vertaald naar een formaat dat door het enschedata platform wordt begrepen. Het platform gaat uit van de JSON formaat van het payload_fields element in TTN bericht. Om de payload_fields in het juiste formaat te krijgen kan gebruik worden gemaakt van een payload function. Hieronder wordt een voorbeeld gegeven hoe zo'n payload function eruit ziet.

Het platform ondersteund op dit moment de volgende elementen in de payload fields:

```
{
  ...
  payload_fields : {
    battery_level: 100,
    temperature: 27.5,
    barometric_pressure: 1005,
    humidity: 80
  }
  ...
}
```

Hieronder is een payload function weergegeven die de 4 bytes (eerste twee temperature en de laatste twee voor de druk) vertaald na een valide JSON formaat:

```
function Decoder(bytes, port) {
  var pressure = ((bytes[2] << 8) | bytes[3]);
  var temperature = (((bytes[0] << 8) | bytes[1]) / 10.0) - 40.0;
  temperature = Math.round(temperature * 10)/10;
  
  var decoded = {
    temperature : temperature,
    barometric_pressure : pressure
  };
  return decoded;
}
```
Controleer in de TTN dashboard, na het toevoegen van de payload function, of de data correct wordt vertaald.

### Integratie met platform

Configureer een HTTP integration op de TTN dashboard om de data te pushen naar het enschedata platform. De volgende parameters moeten worden ingevuld:

* Process ID: (geeft het een label)
* Access key: (vul hier je acces key zodat het integration component bij je data kan, meestal default key)
* URL: *http://enschedata.nl/api/ingest/ttn*
* Method: *POST*
* Authorization: (leeg laten)
* Custom Header Name: *apikey*
* Custom Header Value: (apikey)


### Visualiseer
Zie data op het platform [http://enschedata.nl](http://enschedata.nl)

### API's voor het uitlezen van de data
(work in progress)

De volgende api endpoints kunnen worden gebruikt (dit zijn open api's waar geen apikey voor nodig is):
* [GET] /api/devices
* [GET] /api/measurements[?limit=10&start=2017-07-01&end=2017-07-21&device_id=001&application_id=123]
Optional parameters:
  * limit: het aantal te tonen resultaten (default is 10).
  * start: de startdatum waarop moet worden gefiltered.
  * end: de einddatum waarop moet worden gefiltered.
  * application_id: filter op application (dit is de TTN application id uit je dashboard).
  * device_id: filter op één device (node) (dit is de TTN device id uit je dashboard). Om deze parameter te gebruiken moet de application_id ook worden meegegeven.

