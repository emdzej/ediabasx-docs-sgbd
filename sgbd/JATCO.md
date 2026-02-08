# JATCO.prg

- Jobs: [22](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Getriebesteuerung JATCO |
| ORIGIN | BMW TP-421 Mellersh |
| REVISION | 1.43 |
| AUTHOR | Softing SAG Ta, BMW TP-421 Mellersh |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [ENDE](#job-ende) - Abbruch der Kommunikation
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [RAM_LESEN](#job-ram-lesen) - RAM lesen
- [ROM_LESEN](#job-rom-lesen) - ROM lesen
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Auslesen der Motordrehzahl
- [STATUS_DREHZAHLF_INTERN](#job-status-drehzahlf-intern) - Auslesen des internen Drehzahlfuehlers
- [STATUS_LASTWSENSOR](#job-status-lastwsensor) - Auslesen des Lastwinkelsensors DKG
- [STATUS_BATTERIESPANNUNG](#job-status-batteriespannung) - Auslesen der Batteriespannung
- [STATUS_GETRIEBETEMP](#job-status-getriebetemp) - Auslesen der Getriebeoeltemperatur
- [STATUS_DROSSELKLAPPE](#job-status-drosselklappe) - Auslesen der Drosselklappenstellung
- [STATUS_TACHO_A_SIGNAL](#job-status-tacho-a-signal) - Auslesen des Tacho-A-Signals
- [STATUS_MV_HAUPTDRUCK](#job-status-mv-hauptdruck) - Auslesen des MV-Hauptdruck
- [STATUS_MV_WANDLERUEBERBR](#job-status-mv-wandlerueberbr) - Auslesen der MV-Wanderueberbrueckung
- [STATUS_DIGITAL_EINGAENGE](#job-status-digital-eingaenge) - Auslesen der digitalen Eingangsstati
- [STATUS_DIGITAL_AUSGAENGE](#job-status-digital-ausgaenge) - Auslesen der digitalen Eingangsstati
- [STEUERN_STELLGLIED_GETAKTET](#job-steuern-stellglied-getaktet) - Getaktetes Ansteuern der Stellglieder mit variablen Tastverhaeltnis und variabler Periodendauer
- [STATUS_KICKDOWN_SCHALTER](#job-status-kickdown-schalter) - Auslesen des KD-Schalters

<a id="job-info"></a>
### INFO

Info fuer Anwender

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergerat im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch / english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-ende"></a>
### ENDE

Abbruch der Kommunikation

_No arguments._

_No results._

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| ID_HW_ZULIEFERER | string | Zulieferer-Hardwarenummer |
| ID_SW_ZULIEFERER | string | Zulieferer-Softwarenummer |
| ID_GEN_NR | string | BMW Generationsnummer |
| ID_SW_NR | string | BMW-Softwarenummer (Laufende Nummer) |
| ID_DATUM | string | Herstelldatum |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten des SG |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_ART1_NR | int | Fehlerart 1 des einzelnen Fehlers als Index |
| F_ART1_TEXT | string | Fehlerart 1 des einzelnen Fehlers als Text |
| F_ART2_NR | int | Fehlerart 2 des einzelnen Fehlers als Index |
| F_ART2_TEXT | string | Fehlerart 2 des einzelnen Fehlers als Text |
| F_ART3_NR | int | Fehlerart 3 des einzelnen Fehlers als Index |
| F_ART3_TEXT | string | Fehlerart 3 des einzelnen Fehlers als Text |
| F_ART4_NR | int | Fehlerart 4 des einzelnen Fehlers als Index |
| F_ART4_TEXT | string | Fehlerart 4 des einzelnen Fehlers als Text |
| F_ART5_NR | int | Fehlerart 5 des einzelnen Fehlers als Index |
| F_ART5_TEXT | string | Fehlerart 5 des einzelnen Fehlers als Text |
| F_ART6_NR | int | Fehlerart 6 des einzelnen Fehlers als Index |
| F_ART6_TEXT | string | Fehlerart 6 des einzelnen Fehlers als Text |
| F_ART7_NR | int | Fehlerart 7 des einzelnen Fehlers als Index |
| F_ART7_TEXT | string | Fehlerart 7 des einzelnen Fehlers als Text |
| F_ART8_NR | int | Fehlerart 8 des einzelnen Fehlers als Index |
| F_ART8_TEXT | string | Fehlerart 8 des einzelnen Fehlers als Text |
| F_UW1_NR | int | Umweltbedingung 1 des einzelnen Fehlers als Index |
| F_UW1_TEXT | string | Umweltbedingung 1 des einzelnen Fehlers als Text |
| F_UW1_WERT | real | Umweltbedingung 1 des einzelnen Fehlers als Wert |
| F_UW2_NR | int | Umweltbedingung 2 des einzelnen Fehlers als Index |
| F_UW1_EINH | string | Umweltbedingung 2 des einzelnen Fehlers Einheit |
| F_UW2_TEXT | string | Umweltbedingung 2 des einzelnen Fehlers als Text |
| F_UW2_WERT | real | Umweltbedingung 2 des einzelnen Fehlers als Wert |
| F_UW2_EINH | string | Umweltbedingung 2 des einzelnen Fehlers  Einheit |
| F_CODEHEX | binary | 5 Fehlerbyte |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-ram-lesen"></a>
### RAM_LESEN

RAM lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Startadresse |
| ANZAHL | int | Anzahl zu lesender Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Inhalt der Speicherzellen |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-rom-lesen"></a>
### ROM_LESEN

ROM lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Startadresse |
| ANZAHL | int | Anzahl zu lesender Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Inhalt der Speicherzellen |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Auslesen der Motordrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_MOTORDREHZAHL_WERT | long | Motordrehzahl als Wert |
| STAT_MOTORDREHZAHL_EINH | string | Einheit der Motordrehzahl [1/min] |

<a id="job-status-drehzahlf-intern"></a>
### STATUS_DREHZAHLF_INTERN

Auslesen des internen Drehzahlfuehlers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_DREHZAHLF_INTERN_WERT | long | Wert des internen Drehzahlfuehlers |
| STAT_DREHZAHLF_INTERN_EINH | string | Einheit des internen Drehzahlfuehlers [km/h] |

<a id="job-status-lastwsensor"></a>
### STATUS_LASTWSENSOR

Auslesen des Lastwinkelsensors DKG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_LASTWSENSOR_WERT | long | Lastwinkelsensor DKG als Wert |
| STAT_LASTWSENSOR_EINH | string | Einheit des Lastwinkelsensors DKG [ms] |

<a id="job-status-batteriespannung"></a>
### STATUS_BATTERIESPANNUNG

Auslesen der Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_BATTERIESPANNUNG_WERT | long | Batteriespannung als Wert |
| STAT_BATTERIESPANNUNG_EINH | string | Einheit der Batteriespannung [Volt] |

<a id="job-status-getriebetemp"></a>
### STATUS_GETRIEBETEMP

Auslesen der Getriebeoeltemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_GETRIEBETEMP_WERT | long | Getriebeoeltemperatur als Wert |
| STAT_GETRIEBETEMP_EINH | string | Einheit der Getriebeoeltemperatur [Grad C] |

<a id="job-status-drosselklappe"></a>
### STATUS_DROSSELKLAPPE

Auslesen der Drosselklappenstellung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_DROSSELKLAPPE_WERT | long | Drosselklappenimpuls als Wert |
| STAT_DROSSELKLAPPE_EINH | string | Einheit der Drosselklappenstellung [%] |

<a id="job-status-tacho-a-signal"></a>
### STATUS_TACHO_A_SIGNAL

Auslesen des Tacho-A-Signals

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_TACHO_A_SIGNAL_WERT | long | Tacho-A-Signals als Wert |
| STAT_TACHO_A_SIGNAL_EINH | string | Einheit des Tacho-A-Signals [km/h] |

<a id="job-status-mv-hauptdruck"></a>
### STATUS_MV_HAUPTDRUCK

Auslesen des MV-Hauptdruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_MV_HAUPTDRUCK_WERT | long | MV-Hauptdruck als Wert 0 bedeutet dauerhaft aus 50000 bedeutet dauerhaft ein |
| STAT_MV_HAUPTDRUCK_EINH | string | Einheit des MV-Hauptdruck [ms] |

<a id="job-status-mv-wandlerueberbr"></a>
### STATUS_MV_WANDLERUEBERBR

Auslesen der MV-Wanderueberbrueckung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_MV_WANDLERUEBERBR_WERT | long | MV-Wanderueberbrueckung als Wert 0 bedeutet dauerhaft aus 50000 bedeutet dauerhaft ein |
| STAT_MV_WANDLERUEBERBR_EINH | string | Einheit der MV-Wanderueberbrueckung [ms] |

<a id="job-status-digital-eingaenge"></a>
### STATUS_DIGITAL_EINGAENGE

Auslesen der digitalen Eingangsstati

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POSITIONSHEBEL | string | Stellung des Positionshebels (D,3,N,2,R,4,P,unplaus.) |
| STAT_STUFE_L1_EIN | int | Zustand der Codierschalter L1 |
| STAT_STUFE_L2_EIN | int | Zustand der Codierschalter L2 |
| STAT_STUFE_L3_EIN | int | Zustand der Codierschalter L3 |
| STAT_STUFE_L4_EIN | int | Zustand der Codierschalter L4 |
| STAT_PROGRAMMTASTER | string | Programmtasterauswertung (M,E,S,unplaus.) |
| STAT_MV_A_EIN | int | Magnetventil A ein |
| STAT_MV_B_EIN | int | Magnetventil B ein |
| STAT_MV_C_EIN | int | Magnetventil C ein |
| STAT_MV_FREILAUF_EIN | int | Magnetventil Freilauf ein |
| STAT_MV_RUECKSCHSICH_EIN | int | Magnetventil Rueckschaltsicherung ein |
| STAT_MV_SHIFT_LOCK_EIN | int | Magnetventil Shift-Lock ein |
| STAT_BREMSTEST_EIN | int | Bremstest ein |
| STAT_BREMSLICHT_EIN | int | Bremslicht ein |
| STAT_KICKDOWN_EIN | int | Kickdownschalter ein |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-digital-ausgaenge"></a>
### STATUS_DIGITAL_AUSGAENGE

Auslesen der digitalen Eingangsstati

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MV_A_EIN | int | Magnetventil A ein |
| STAT_MV_B_EIN | int | Magnetventil B ein |
| STAT_MV_C_EIN | int | Magnetventil C ein |
| STAT_MV_FREILAUF_EIN | int | Magnetventil Freilauf ein |
| STAT_MV_RUECKSCHSICH_EIN | int | Magnetventil Rueckschaltsicherung ein |
| STAT_MV_SHIFT_LOCK_EIN | int | Magnetventil Shift-Lock ein |
| STAT_PROGRAMMTASTER_E_EIN | int | Programmtasterauswertung |
| STAT_PROGRAMMTASTER_W_EIN | int | Programmtasterauswertung |
| STAT_PROGRAMMTASTER_S_EIN | int | Programmtasterauswertung |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-steuern-stellglied-getaktet"></a>
### STEUERN_STELLGLIED_GETAKTET

Getaktetes Ansteuern der Stellglieder mit variablen Tastverhaeltnis und variabler Periodendauer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STELLGL | string | Anzusteuerndes Stellglied MAGNETVENTIL_A MAGNETVENTIL_B MAGNETVENTIL_C MV_FREILAUF MV_RUECKSCHSICH MV_SHIFT_LOCK MV_WANDLERUBERBR MV_HAUPTDRUCK E_ANZEIGE S_ANZEIGE W_ANZEIGE FEHLERLAMPE MOTOREINGRIFF |
| EINSCHZ | long | Einschaltzeit in Prozent (0 bis 100 %) |
| PERIODE | long | Periodendauer in Millisekunden (0 bis 25500 ms) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_ANSTEUERUNG | int | Ansteuerergebnis 0: Stellglied kann angesteuert werden 1: PIN-Nummer ist unbekannt 2: Positionshebel ist nicht in N oder P 3: Abtriebsdrehzahl ist zu hoch 4: Relais ist abgefallen, ein Fehler ist vorhanden |

<a id="job-status-kickdown-schalter"></a>
### STATUS_KICKDOWN_SCHALTER

Auslesen des KD-Schalters

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KICKDOWN_EIN | int | Kickdownschalter ein |
| JOB_STATUS | string | OKAY, ERROR_NACK |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (24 × 4)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [FARTMATRIX](#table-fartmatrix) (24 × 17)
- [FUMWELTTEXTE](#table-fumwelttexte) (17 × 5)
- [STATUSAMATRIX](#table-statusamatrix) (9 × 5)
- [STELLGLIEDER](#table-stellglieder) (13 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 24 rows × 4 columns

| ORT | ORTTEXT | UW_1 | UW_2 |
| --- | --- | --- | --- |
| 0x01 | Ueberwachung Magnetventile | 0x0a | 0x0e |
| 0x02 | Magnetventil Hauptdruck | 0x08 | 0x0a |
| 0x04 | UBATT-Versorgung | 0x05 | 0x01 |
| 0x06 | Magnetventil A | 0x0a | 0x03 |
| 0x07 | Magnetventil B | 0x0a | 0x03 |
| 0x0a | Motoreingriff | 0x0a | 0x01 |
| 0x14 | Programmtaster | 0x0b | 0x0f |
| 0x17 | Speicherfehler | 0x05 | 0x04 |
| 0x18 | Drehzahlsignal n-mot | 0x03 | 0x07 |
| 0x19 | Leitung Drehzahlfuehler | 0x01 | 0x0a |
| 0x1b | Tacho A-Signal | 0x01 | 0x0a |
| 0x1d | MV Wandlerueberbrueckung | 0x0a | 0x09 |
| 0x21 | Getriebeoel-Temperaturgeber | 0x01 | 0x04 |
| 0x22 | Drosselklappensensor | 0x03 | 0x01 |
| 0x29 | Kick-Down-Schalter | 0x07 | 0x0d |
| 0x2b | Magnetventil Freilauf | 0x0a | 0x0e |
| 0x2c | MV Rueckschaltsicherung | 0x0a | 0x0e |
| 0x2e | Magnetventil C | 0x0a | 0x03 |
| 0x2f | Magnetventil Shift-Lock | 0x0a | 0x0e |
| 0x32 | Drehzahlschlupf | 0x01 | 0x03 |
| 0x33 | Getriebesteuergeraet | 0x01 | 0x03 |
| 0x34 | Ueberdrehzahl Motor | 0x03 | 0x0a |
| 0x35 | AD-Wandler | 0x04 | 0x0b |
| 0xXY | unbekannter Fehlerort | 0x00 | 0x00 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 14 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | Keine Plausibilitaet |
| 0x05 | Plausibilitaet |
| 0x06 | Fehler momentan nicht vorhanden |
| 0x07 | Fehler momentan vorhanden |
| 0x08 | Pruefbedingung nicht erreicht |
| 0x09 | Pruefbedingung erreicht |
| 0x0a | Fehler nach Filterzeit nicht vorh. |
| 0x0b | Fehler nach Filterzeit vorhanden |
| 0x0c | statischer Fehler |
| 0x0d | sporadischer Fehler |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 24 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x01 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x02 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x04 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x06 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x07 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x0a | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x14 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x17 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x18 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x19 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x1b | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x1d | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x21 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x22 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x29 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x2b | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x2c | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x2e | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x2f | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x32 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x33 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x34 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x35 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 17 rows × 5 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B |
| --- | --- | --- | --- | --- |
| 0x00 | -- | -- | 1.0 | 0.0 |
| 0x01 | Motordrehzahl | [1/min] | 32.0 | 0.0 |
| 0x02 | Tacho-A-Signal | [km/h] | 1.0 | 0.0 |
| 0x03 | Drehzahlfuehler | [km/h] | 1.0 | 0.0 |
| 0x04 | Getriebetemperatur | [Grad C] | 1.0 | 0.0 |
| 0x05 | Batteriespannng | [Volt] | 0.078 | 0.0 |
| 0x06 | Lastsignal DKG | [ms] | 0.256 | 0.0 |
| 0x07 | Drosselklappe | [%] | 0.392 | 0.0 |
| 0x08 | Hauptdruck (aus) | [ms] | 0.256 | 0.0 |
| 0x09 | Wandlerueberbr. (ein) | [ms] | 0.256 | 0.0 |
| 0x0a | Statusbyte 00 | -- | 1.0 | 0.0 |
| 0x0b | Statusbyte 01 | -- | 1.0 | 0.0 |
| 0x0c | Statusbyte 02 | -- | 1.0 | 0.0 |
| 0x0d | Statusbyte 03 | -- | 1.0 | 0.0 |
| 0x0e | Statusbyte 80 | -- | 1.0 | 0.0 |
| 0x0f | Statusbyte 83 | -- | 1.0 | 0.0 |
| 0xXY | unbekannte Umweltbedingung | -- | 1.0 | 0.0 |

<a id="table-statusamatrix"></a>
### STATUSAMATRIX

Dimensions: 9 rows × 5 columns

| SNAME | TYP | FAKT_A | FAKT_B | EINH |
| --- | --- | --- | --- | --- |
| Motordrehz | 1 | 32000 | 0 | 1/min |
| DrehzInt | 1 | 1000 | 0 | km/h |
| Lastwsensor | 1 | 256 | 0 | ms |
| Ubatt | 1 | 78 | 0 | Volt |
| Getroelt | 2 | 0 | 0 | Grad C |
| DKI | 1 | 392 | 0 | % |
| TachoA | 1 | 1000 | 0 | km/h |
| MVHauptd | 1 | 256 | 0 | ms |
| MVWandlerue | 1 | 256 | 0 | ms |

<a id="table-stellglieder"></a>
### STELLGLIEDER

Dimensions: 13 rows × 2 columns

| STELLGLIED | PIN |
| --- | --- |
| MAGNETVENTIL_A | 6 |
| MAGNETVENTIL_B | 7 |
| MAGNETVENTIL_C | 46 |
| MV_FREILAUF | 43 |
| MV_RUECKSCHSICH | 44 |
| MV_SHIFT_LOCK | 47 |
| MV_WANDLERUBERBR | 29 |
| MV_HAUPTDRUCK | 2 |
| E_ANZEIGE | 12 |
| S_ANZEIGE | 45 |
| W_ANZEIGE | 13 |
| FEHLERLAMPE | 11 |
| MOTOREINGRIFF | 10 |
