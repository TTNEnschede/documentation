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

### Integration to platform

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
