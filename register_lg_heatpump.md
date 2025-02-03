# Register <a name="register"></a>
### Coil Register (0x01)

| **Register** | **Homeassistant** | **Description**                                | **Explanation of the values**             | **LG Doc** | **Note**      |
|---------------|-------------------|------------------------------------------------|-------------------------------------      |------------|---------------|
| 00001         | 0                 | Aktivieren / Deaktivieren (Heizung / Kühlung)  | 0 : Betrieb AUS / 1 : Betrieb EIN         | TRUE       |               |
| 00002         | 1                 | Aktivieren / Deaktivieren (DHW)                | 0 : Betrieb AUS / 1 : Betrieb EIN         | TRUE       |               |
| 00003         | 2                 | Einstellung Silent Modus                       | 0: Ruhemodus AUS / 1: Ruhemodus EIN       | TRUE       |               |
| 00004         | 3                 | Auslösung Desinfektionsbetrieb                 | 0: Status halten / 1: Betriebsstart       | TRUE       |               |
| 00005         | 4                 | Notaus                                         | 0: Normaler Betrieb / 1: Notaus           | TRUE       |               |
| 00006         | 5                 | Auslöser Notaus-Betrieb                        | 0: Status halten / 1: Betriebsstart       | TRUE       |               |

### Diskretes Register (0x02)

| **Register** | **Homeassistant** | **Description**                             | **Explanation of the values**                        | **LG Doc** | **Note**      |
|---------------|-------------------|----------------------------------------------|-----------------------------------------------------|------------|---------------|
| 10001         | 0                 | Status Wasserdurchfluss                      | 0: Durchflussrate OK / 1: Durchflussrate zu niedrig | TRUE       |               |
| 10002         | 1                 | Wasserpumpenstatus                           | 0: Wasserpumpen AUS / 1: Wasserpumpen EIN           | TRUE       |               |
| 10003         | 2                 | Ext. Wasserpumpenstatus                      | 0: Wasserpumpen AUS / 1: Wasserpumpen EIN           | TRUE       |               |
| 10004         | 3                 | Kompressorstatus                             | 0: Kompressor AUS / 1: Kompressor EIN               | TRUE       |               |
| 10005         | 4                 | Abtaustatus                                  | 0: Abtauen AUS / 1: Abtauen EIN                     | TRUE       |               |
| 10006         | 5                 | DHW-Heizstatus                               | 0: DHW inaktiv / 1: DHW aktiv                       | TRUE       |               |
| 10007         | 6                 | Desinfektionsstatus DHW-Speicher             | 0: Desinfektion inaktiv / 1: Desinfektion aktiv     | TRUE       |               |
| 10008         | 7                 | Status Silent Modus                          | 0: Ruhemodus inaktiv / 1: Ruhemodus aktiv           | TRUE       |               |
| 10009         | 8                 | Kühlstatus                                   | 0: Keine Kühlung / 1: Kühlbetrieb                   | TRUE       |               |
| 10010         | 9                 | Status der Solarpumpe                        | 0: Solarpumpe AUS / 1: Solarpumpe EIN               | TRUE       |               |
| 10011         | 10                | Status Zusatzheizung (Schritt 1)             | 0: AUS / 1: EIN                                     | TRUE       |               |
| 10012         | 11                | Status Zusatzheizung (Schritt 2)             | 0: AUS / 1: EIN                                     | TRUE       |               |
| 10013         | 12                | Status DHW-Verstärkerheizung                 | 0: AUS / 1: EIN                                     | TRUE       |               |
| 10014         | 13                | Fehlermeldung                                | 0: Kein Fehler / 1: Fehlerstatus                    | TRUE       |               |
| 10015         | 14                | Notbetrieb verfügbar (Raumheizung/-Kühlung)  | 0: Nicht verfügbar / 1: Verfügbar                   | TRUE       |               |
| 10016         | 15                | Notbetrieb verfügbar (WW)                    | 0: Nicht verfügbar / 1: Verfügbar                   | TRUE       |               |
| 10017         | 16                | Status Mischpumpe                            | 0: Mischpumpe AUS / 1: Mischpumpe EIN               | TRUE       |               |

### Input Register (0x04) 

| **Register** | **Homeassistant** | **Description**                     | **Explanation of the values**                                                        | **LG Doc** | **Note**                           |
|---------------|-------------------|---------------------------------    |-------------------------------------------------------------------------------------|------------|------------------------------------|
| 30001         | 0                 | Fehlerkennung                       | Fehlerkennung                                                                       | TRUE       |                                    |
| 30002         | 1                 | ODU-Betriebszyklus                  | 0: Standby (AUS) / 1: Kühlung / 2: Heizung                                          | TRUE       |                                    |
| 30003         | 2                 | Wassereinlasstemp.                  | [0.1 °C ×10]                                                                        | TRUE       |                                    |
| 30004         | 3                 | Wasserauslasstemp.                  | [0.1 °C ×10]                                                                        | TRUE       |                                    |
| 30005         | 4                 | Auslasstemp. Ersatzheizgerät        | [0.1 °C ×10]                                                                        | TRUE       |                                    |
| 30006         | 5                 | DHW Temperatur                      | [0.1 °C ×10]                                                                        | TRUE       |                                    |
| 30007         | 6                 | Sonnenkollektortemp.                | [0.1 °C ×10]                                                                        | TRUE       |                                    |
| 30008         | 7                 | Raumlufttemp. (Kreis 1)             | [0.1 °C ×10]                                                                        | TRUE       |                                    |
| 30009         | 8                 | Aktuelle Durchflussrate             | [0.1 l/min ×10]                                                                     | TRUE       |                                    |
| 30010         | 9                 | Durchflusstemp. (Kreis 2)           | [0.1 °C ×10]                                                                        | TRUE       |                                    |
| 30011         | 10                | Raumlufttemp. (Kreis 2)             | [0.1 °C ×10]                                                                        | TRUE       |                                    |
| 30012         | 11                | Energiezustand-Eingang              | 0 : Energiezustand 0<br>1 : Energiezustand 1….                                      | TRUE       |                                    |
| 30013         | 12                | Außenlufttemp.                      | [0.1 °C ×10]                                                                        | TRUE       |                                    |
| 30014         | 13                | Water pressure                      | [0.1 bar ×10]                                                                       | TRUE       |                                    |
| 30037         | 36                | ENERGY_INSTANTANEOUS_TOTAL (High)   | [Wh]                                                                                | TRUE       |                                    |
| 30038         | 37                | ENERGY_INSTANTANEOUS_TOTAL (Low)    | [Wh]                                                                                | TRUE       |                                    |
| 30039         | 38                | ENERGY_ACCUMULATIVE_TOTAL (High)    | [Wh]                                                                                | TRUE       |                                    |
| 30040         | 39                | ENERGY_ACCUMULATIVE_TOTAL (Low)     | [Wh]                                                                                | TRUE       |                                    |
| 30041         | 40                | ENERGY_INSTANTANEOUS_HEAT (High)    | [Wh]                                                                                | TRUE       |                                    |
| 30042         | 41                | ENERGY_INSTANTANEOUS_HEAT (Low)     | [Wh]                                                                                | TRUE       |                                    |
| 30043         | 42                | ENERGY_ACCUMULATIVE_COOL (High)     | [Wh]                                                                                | TRUE       |                                    |
| 30044         | 43                | ENERGY_ACCUMULATIVE_COOL (Low)      | [Wh]                                                                                | TRUE       |                                    |
| 30045         | 44                | ENERGY_ACCUMULATIVE_DHW (High)      | [Wh]                                                                                | TRUE       |                                    |
| 30046         | 45                | ENERGY_ACCUMULATIVE_DHW (Low)       | [Wh]                                                                                | TRUE       |                                    |
| 30017         | 16                | Temperatur Flüssiggas               | [0.1 °C ×1]                                                                         | FALSE      |                                    |
| 30019         | 18                | Temperatur Absaugung                | [0.1 °C ×1]                                                                         | FALSE      |                                    |
| 30020         | 19                | Heißgastemperatur                   | [0.1 °C ×1]                                                                         | FALSE      |                                    |
| 30021         | 20                | Dampftemperatur vor Verdampfer      | [0.1 °C ×1]                                                                         | FALSE      |                                    |
| 30022         | 21                | Dampftemperatur nach Verdampfer     | [0.1 °C ×1]                                                                         | FALSE      |                                    |
| 30023         | 22                | Dampfdruck Kondensator              | [0.1 °C ×1]                                                                         | FALSE      |                                    |
| 30024         | 23                | Dampfdruck Kondensator              | [0.1 °C ×1]                                                                         | FALSE      |                                    |
| 30025         | 24                | Kompressordrehzahl                  | [Hz]                                                                                | TRUE       | only higher fw version 3.0.6.7a    |
| 39998         | 39997             | Gerätegruppe                        | 0x8X (0x80, 0x83, 0x88, 0x89)                                                       | TRUE       |                                    |
| 39999         | 39998             | Geräteinfo                          | Split: 0<br>Monoblock: 3<br>Hochtemp. : 4<br>Mittlere Temp. : 5<br>System-Boiler: 6 | TRUE       |                                    |

### Holding Register (0x03)

| **Register** | **Homeassistant** | **Description**                         | **Explanation of the values**                                                               | **LG Doc** | **Note**                               |
|---------------|-------------------|-------------------                      |---------------------------                                                                  |------------|--------------                          |
| 40001         | 0                 | Betriebsmodus (Kreis 1/2)               | 0: Kühlung / 4: Heizung / 3: Auto                                                           | TRUE       |                                        |
| 40002         | 1                 | Steuermethode (Kreis 1/2)               | 0: Wasserauslasstemp. Steuerung <br>1: Wassereinlasstemp. Steuerung<br>2: Raumluftsteuerung | TRUE       |                                        | 
| 40003         | 2                 | Zieltemp. (Heizung / Kühlung) Kreis 1   | [0.1 °C ×10]                                                                                | TRUE       |                                        |
| 40004         | 3                 | Raumlufttemp. Kreis 1                   | [0.1 °C ×10]                                                                                | TRUE       |                                        |
| 40005         | 4                 | Schaltwert (Ziel) im Auto-Modus Kreis 1 | 1K                                                                                          |            |                                        |
| 40006         | 5                 | Zieltemp. (Heizung / Kühlung) Kreis 2   | [0.1 °C ×10]                                                                                | TRUE       |                                        |
| 40008         | 7                 | Schaltwert (Ziel) im Auto-Modus Kreis 2 | 1K                                                                                          | TRUE       |                                        |
| 40009         | 8                 | DHW Ziel Temp.                          | [0.1 °C ×10]                                                                                | TRUE       |                                        |
| 40010         | 9                 | Energiezustand-Eingang                  | 0: Nicht verwenden<br>1: Erzwungen Aus (gleich TB_SG1=schließen /<br>TB_SG2=öffnen)<br>2: Normalbetrieb (gleich TB_SG1=öffnen /<br>TB_SG2=öffnen)<br>3 : Ein-Empfehlung (gleich TB_SG1=öffnen /<br>TB_SG2=schließen)<br>4 : Ein-Befehl (gleich TB_SG1=schließen /<br>TB_SG2=schließen)<br>5 : Ein-Befehl Schritt 2 (++ Stromverbrauch<br>verglichen mit Normal)<br>6 : Ein-Empfehlung Schritt 1 (+ Stromverbrauch<br>verglichen mit Normal)<br>7 : Energiesparmodus (- Stromverbrauch<br>verglichen mit Normal)<br>8 : Superenergiesparmodus (-- Stromverbrauch<br>verglichen mit Normal)                                                                                                                                                                                                                                  | TRUE       | Wird über Template Sensor ausgewertet. |
| 40024         | 23                | Compressor Modulation                   | 0: Not Used /40~100:Compressor Modulation                                                   | TRUE       |                                        |
| 49999         | 9998              | Produktinfo                             |                                                                                             | TRUE       |                                        |
