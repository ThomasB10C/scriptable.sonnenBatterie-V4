#### scriptable.sonnenBatterie V4

# sonnenBatterie-Widget V4
Widget für die sonnenBatterien Eco 8.0/SB10

![sbv4d](sbv4-2.jpeg)  - Übersicht der Daten im Day-Mode

![sbv4n](sbv4-3.jpeg)  - Darstellung der Daten im Night-Mode

Download: >>> [hier](SonnenBatterieV4.01.js)

## Kurzbeschreibung
Das Widget sonnenBatterie V4 dient dem Monitoring der sonnenBatterien Eco 8.0 und SB10. Es fragt ausgewählte Betriebsdaten der sonnenBatterie über API-Schnittstellen der REST-API ab und stellt diese im Widget in einer Übersicht zur Verfügung. Das Widget läuft mit Unterstützung der iPhone-/iPad-App **Scriptable** ab **iOS14**.

Die folgenden Daten werden im Widget dargestellt:

**1. Zeile**
- 🔅/☁️/🌔 - Status für die gestartete Produktion/Erzeugung der PV-Anlage On/Off
🔅 - sonnig, die PV-Anlage erzeugt Strom
☁️ - bewölkt, die PV-Anlage liefert keinen Strom
🌔 - nachts liefert die PV-Anlage keinen Strom

- 19:44 - Uhrzeit des letzten Datenupdates der Abfrage der sonnenBatterie (Timestamp)
- Online/⚡️Offline - Status der Verbindung der sonnenBatterie zum Internet (Status der Eclipse)

**2. Zeile**
- Name des Scriptes

**3. Zeile**
- **99% ↑** - Ladezustand der sonnenBatterie mit Trendanzeige bei Ladung= On.

**4. bis 7. Zeile**
- **Produktion** in kW, Erzeugung der PV-Anlage
- **Verbrauch** in kW, Verbrauch im Haus
- **Einspeisung/Bezug** in kW, die Anzeige wechselt zwischen Einspeisung und Bezug, abhängig vom Status
- **Ladung/Entladung** in kW, die Anzeige wechselt zwischen Ladung und Entladung, abhängig vom Status

**8. Zeile**
- **Grid:0/1 ** - Status der Verbindung der sonnenBatterie zum Stromnetz, "0" bedeutet "⚡️OffGrid, "1" bedeutet "OnGrid"
- **R1**:0/1 **R2**:0/1 - Status der Abregelung der Limitstufe1 (Reduction1) und der Limitstufe2 (Reduction2), 0= Off, 1= On
- **R3**:0/1 - Status des Self Consumption Relay, 0= Off, 1= On

**9. Zeile**
- **999**⤒ - Stand der vollständigen Ladezyklen der sonnenBatterie (Zykluszähler)
- **23,45º** -**25,77º** - Temperaturwerte der Zellen, minimaler Temperaturwert, maximaler Temperaturwert

Zur Beachtung: Die Aktualisierung der Betriebsdaten der Batterie kann (zurzeit) nur dann durchgeführt werden, wenn sich das iPhone im Empfangsbereich des WLAN befindet. Sollte die Firma sonnen die für das Widget erforderlichen iCloud-Daten der Batterien freischalten, dann wird das Widget daauf angepaßt.

## Settings, Parameter

Im Script selbst sind in den dafür markierten Zeilen die folgenden Parameter einzugeben:

1. **IP-Adresse**: Gültige IP-Adresse der sonnenBatterie, über die die Batterie im LAN zu erreichen ist, in der Form 999:999:999:99
2. **Token**: Gültiger Token für den Zugriff auf die REST-API der sonnenBatterie. Dieser kann dem Dashboard der Batterie, Menü 'Softwareintegration' entnommen werden
3. **TimeoutInterval**: Zeit für den Abbruch der API-Abfrage, wenn keine Antwort zurück kommt, Standard = 1 Sekunde.
4. **FileManagerMode**: Parameter für die Speicherung der temporären Daten im iPhone-Speicher (LOKAL) oder in der Cloud (iCLOUD), Standard = ICLOUD

### Statuswerte

**Online-/Offline-status**

Der Offline-Status der Batterie wird mit dem folgenden Bild angezeigt.
Dafür wechselt die Anzeige in der obersten Zeile im WIdget von "Online" auf "⚡️Offline"

![Offline](sbv3-4.jpeg)

**OnGrid-/OffGrid-Status**

OnGrid/OffGrid - die Trennung von Stromnetz wird in der vorletzten Zeile angezeigt, 
die Anzeige wechselt von "Grid:1" auf "Grid:0"

**Status der Abregelungs-Relais**

R1/R2: 0/1 - das Widget prüft auch den Status des Reduction-Relais R1 und R2, 
R1/R2: "0" = Off, "1"= On.
Im Bild wurden die beiden Relais aktuell auf Abregelung= On gesetzt.

![R1&R2](sbv4-1.jpeg)

**Status des Self Consumption Relais**
R3: 0/1 - der Status des Self Consumption Realy wird in dieser Zeile als 3. Position angezeigt, 
R3: "0" = Off, "1"= On

## API-Schnittstellen

Die JSON-Daten der folgenden API-Schnittstellen werden verarbeitet:

````APIurl1 ="http://xxx.xxx.xxx.xx:80/api/v2/latestdata"````

````APIurl2 ="http://xxx.xxx.xxx.xx:80/api/v2/status"````

````APIurl3 ="http://xxx.xxx.xxx.xx:8080/api/battery"````

````APIurl4 ="http://xxx.xxx.xxx.xx:8080/api/ios"````

Die ausgelesenen Daten werden sofort für das Monitoring zur Anzeige gebracht, Statuswerte der Batterie werden bewertet und ggf. besonders gekennzeichnet. Eine Langzeitspeicherung der Daten, bspw. in einer Datenbank für die Visualisierung von 24-h-Tagestrends, erfolgt nicht. Nach jedem Lesezyklus der API-Daten werden diese jeweils in einer temporären JSON-Datei gespeichert, diese Daten werden bei Störung der Internetverbindung zur Anzeige gebracht und nach Wiederherstellung der Verbindungen sofort wieder überschrieben. 

Das Widget läuft im Homescreen des iPhones, es wird vom Betriebssystem in festen Zeitzyklen gestartet und aktualisiert dann die Daten durch Abfrage der Batterie. Dieser Zeitzyklus kann zurzeit nicht beeinflusst werden. Allerdings startet ein Tippen auf das Widget die Datenabfrage manuell, dann werden die aktuellen Daten der Batterie durch das Widget mit Hilfe der App Scriptable sofort angezeigt und aktualisiert.

Das Widget speichert für das Monitoring eine eigene JSON-Datei ab, die den folgenden Aufbau hat:

##### JSON - Monitoring-Datei

``

{

  "jsonVersion": 1,
  "MonitoringCounter": 5,
  "Timestamp": "2021-01-12 18:37:16",
  "ConnectState": true,
  
  "SystemState": "OnGrid",
  "Production_W": 0,
  "Consumption_W": 560,
  "Pac_total_W": -5,
  "GridFeedIn_W": -565,
  "RSOC": 4,
  "USOC": 0,
  "BatteryCharging": false,
  "BatteryDischarging": false,
  "cyclecount": "802",
  "stateofhealth": "93.2",
  "minimumcelltemperature": "20.85",
  "maximumcelltemperature": "21.95",
  "selfConsumptionRelay": 0,
  "PV_Reduction_state": {
    "PV_Reduction_1": 0,
    "PV_Reduction_2": 0
  },
  "Eclipse_Led": {
    "Pulsing_White": true,
    "Pulsing_Orange": false,
    "Solid_Red": false,
    "Pulsing_Green": false
  }
}

``

## Changelog

2021/01/12: sonnenBatterie V4.0 (Widget) init
