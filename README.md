#### scriptable.sonnenBatterie V3.0
![sb1Widget](sbv3-1.jpeg)![sb2Widget](sbv3-2.jpeg)

# sonnenBatterie-Widget
Widget für die sonnenBatterien Eco 8.0/SB10

Download: >>> [hier](SonnenBatterieV2.0.js)

## Kurzbeschreibung
Das Widget V3.0 dient dem Monitoring der sonnenBatterien Eco 8.0 und SB10. Es fragt ausgewählte Betriebsdaten der sonnenBatterie über API-Schnittstellen der REST-API ab und stellt diese im Widget in einer Übersicht zur Verfügung. Das Widget läuft mit Unterstützung der iPhone-App **Scriptable** ab **iOS14**.

Die folgenden Daten werden im Widget dargestellt:

1. Zeile
- 🔅/☁️ - Status für die gestartete Produktion/Erzeugung der PV-Anlage On/Off
- 19:44 - Uhrzeit des letzten Datenupdates der Abfrage der sonnenBatterie (Timestamp)
- Online/⚡️Offline - Status der Verbindung der sonnenBatterie zum Internet (Status der Eclipse)

2. Zeile
- Name des Scriptes

3. Zeile
- **99% ↓↑** - Ladezustand der sonnenBatterie mit Trendanzeige

4. bis 7. Zeile
- **Produktion** in kW, Erzeugung der PV-Anlage
- **Verbrauch** in kW, Verbrauch im Haus
- **Einspeisung/Bezug** in kW, die Anzeige wechselt zwischen Einspeisung und Bezug, abhängig vom Status
- **Ladung/Entladung** in kW, die Anzeige wechselt zwischen Ladung und Entladung, abhängig vom Status

8. Zeile
- **OnGrid/⚡️OffGrid** - Status der Verbindung der sonnenBatterie zum Stromnetz
- **R1:Off/On R2:Off/On** - Status der Abregelung der Limitstufe1 (Reduction1) und der Limitstufe2 (Reduction2)

9. Zeile
- **999**⤒ - Stand des Zykluszählers der Ladezyklen der sonnenBatterie
- **23,45º** -**25,77º** - Temperaturwerte der Zellen, minimaler Temperaturwert, maximaler Temperaturwert

Zur Beachtung: Die Betriebsdaten der Batterie werden (zurzeit) nur angezeigt, wenn sich das iPhone im Empfangsbereich des WLAN befindet.

## Settings, Parameter

Im Script selbst sind in den dafür markierten Zeilen die folgenden Parameter einzugeben:

- 1. **IP-Adresse**: Gültige IP-Adresse der sonnenBatterie, über die die Batterie im LAN zu erreichen ist, in der Form 999:999:999:99
- 2. **Token**: Gültiger Token für den Zugriff auf die REST-API der sonnenBatterie. Dieser kann dem Dashboard der Batterie, Menü 'Softwareintegration' entnommen werden
- 3. **TimeoutInterval**: Zeit für den Abbruch der API-Abfrage, wenn keine Antwort zurück kommt, Standard = 1 Sekunde.
- 4. **KZ: FileManagerMode**: Parameter für die Speicherung der temporären Daten im iPhone-Speicher (LOKAL) oder in der Cloud (iCLOUD), Standard = ICLOUD

## API-Schnittstellen

````APIurl1 ="http://xxx.xxx.xxx.xx:80/api/v2/latestdata"````

````APIurl2 ="http://xxx.xxx.xxx.xx:80/api/v2/status"````

````APIurl3 ="http://xxx.xxx.xxx.xx:8080/api/battery"````

````APIurl4 ="http://xxx.xxx.xxx.xx:8080/api/ios"````

Die ausgelesenen Daten werden sofort für das Monitoring zur Anzeige gebracht, Statuswerte der Batterie werden bewertet und ggf. besonders gekennzeichnet. Eine Langzeitspeicherung der Daten, bspw. in einer Datenbank für die Visualisierung von Tagestrends, erfolgt nicht. Nach jedem Lesezyklus der API-Daten werden diese jeweils in einer temporären Datei gespeichert, diese Daten werden bei Störung der Internetverbindung zur Anzeige gebracht und nach Wiederherstellung der Verbindungen sofort wieder überschrieben. 

Das Widget auf dem Homescreen des iPhones wird vom Betriebssystem in festen Zeitzyklen gestartet und aktualisiert dann die Daten durch Abfrage der Batterie. Diser Zeitzyklus kann zurzeit noch nicht beeinflusst werden. Allerdings startet ein Tippen auf das Widget die Datenabfrage manuell, dann werden die aktuellen daten der Batterie sofort angezeigt.

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

2020/12/29: sonnenBatterie V3.0 (Widget) init
