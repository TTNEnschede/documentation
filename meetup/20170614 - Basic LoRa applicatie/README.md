# Bouw een basis LoRa node (deel 2 van 3)
https://www.meetup.com/The-Things-Network-Enschede/events/239850678/

*Locatie:* Trimm

In deze meetup zijn voorbeelden van het koppelen van een basis LoRa aan applciaties besproken.

## LoRaWAN - the easy way
Cayenne Low Power Payload: https://www.thethingsnetwork.org/docs/applications/Cayenne/

Stappenplan:
* Device programmeren voor Cayenne. 
	* Zie ook: https://github.com/TTNEnschede/SensorNode 
	* CayenneLPP library is onderdeel van TTN Arduino Library. In je Arduino IDE ga naar '**Sketch -> Include Library -> Manage Libraries..**'. Zoek vervolgende naar *TheThingsNetwork*. Als het goed is zijn er dan twee resultaten. Installeer de '**TheThingsNetwork** by **TheThingsNetwork**' library.
* Payload functie configureren.
	* Ga in de TTN dashboard naar je applicatie en klik daar op *Payload Formats*. Kies in de dropdown de *Cayenne LPP* payload format.
* Cayenne Integration configureren.
	* Ga in de TTN dashboard naar je applicatie en klik daar op *Integrations*. Voeg de *Cayenne* integration toe aan je applicatie.
* Simpele visualisaties van data van de node.
	* Account aanmaken op http://mydevices.com.
	* Voeg een new Device/Widget toe. Let er op dat je LoRa kiest en het netwerk van The Things Network.
	* Voeg de Device EUI uit je TTN dashboard toe aan je widget en zie je data verschijnen in op de mydevices dashboard.


## Resources
* Presentatie van de meetup: [20170614 - LoRa applicatie.pdf](https://github.com/TTNEnschede/documentation/blob/master/meetup/20170614%20-%20Basic%20LoRa%20applicatie/20170614%20-%20LoRa%20applicatie.pdf)

## Impressie van de meetup
![alt text](https://github.com/TTNEnschede/documentation/blob/master/meetup/20170614%20-%20Basic%20LoRa%20applicatie/20170714-Applicatie_bouwavond.jpg "Bouwavond")
