#### scriptable.sonnenBatterie V2.0
![sbWidget](sb1.jpeg)

# sonnenBatterie-Widget
Widget für die sonnenBatterien ECO 8.0/SB10

Download: >>> [hier](SonnenBatterieV2.0.js)

## Kurzbeschreibung
Das Widget für die sonnenBatterie liest ausgewählte Betriebsdaten der sonnenBatterie über deren API-Schnittstelle aus und stellt diese in einer Übersicht zur Verfügung. Das Script läuft mit Unterstützung der App **Scriptable** auf dem iPhone mit **iOS14**.

- **Produktion** in kW, Erzeugung der PV-Anlage
- **Verbrauch** in kW, Verbrauch im Haus
- **Einspeisung/Bezug** in kW, die Anzeige wechselt zwischen Einspeisung und Bezug, abhängig vom Status
- **Ladung/Entladung** in kW, die Anzeige wechselt zwischen Ladung und Entladung, abhängig vom Status
- **SOC** in %, Ladezustand der Batterie in %

Zur Beachtung: Die Betriebsdaten der Batterie werden (zurzeit) nur angezeigt, wenn sich das iPhone im Empfangsbereich des WLAN befindet.

## Settings, Parameter
Im Script ist in der oberen Zeile die gültige URL der sonnenBatterie einzugeben, über die die Batterie im LAN zu erreichen ist.

**APIurl:** - IP-Adresse der sonnenBatterie in der Form 999:999:999:99

## API-Schnittstelle

````APIurl ="http://xxx.xxx.xxx.xx:8080/api/v1/status"````

Die ausgelesenen Daten werden zur Anzeige gebracht, eine Speicherung der Daten, bspw. in einer Datenbank für die Visualisierung von Trends, erfolgt nicht.

Die folgenden JSON-Daten der Batterie werden verarbeitet:

##### JSON

````
{
...,
"Consumption_W":358,
...,
"GridFeedIn_W":5065,
...,
"Pac_total_W":-1031,
"Production_W":6458,
"USOC":58,
...
}
````
## Changelog

2020/11/11: sonnenBatterie V1.0 (Widget) init
