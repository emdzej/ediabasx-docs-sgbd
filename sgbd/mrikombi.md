# mrikombi.prg

- Jobs: [37](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Kombiinstrument K1200 |
| ORIGIN | I+ME Actia GmbH, Keck |
| REVISION | 1.00 |
| AUTHOR | I+ME Actia GmbH, Keck |
| COMMENT | N/A |
| PACKAGE | 1.00 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [SEC_ACCESS](#job-sec-access) - SG für erweiterte Diagnose freischalten Simple Protection Mode Algorithmus
- [STATUS_TEILENUMMER](#job-status-teilenummer) - Lesen der Teilenummer Byte 4-7
- [STATUS_HARDWARESTAND](#job-status-hardwarestand) - Lesen des Hardwarestandes Byte 8
- [STATUS_CODIERBARKEIT](#job-status-codierbarkeit) - Lesen der Codierbarkeit Byte 9
- [STATUS_DIAGNOSEINDEX](#job-status-diagnoseindex) - Lesen des Diagnoseindex Byte 10
- [STATUS_BUSINDEX](#job-status-busindex) - Lesen des BusIndex Byte 11
- [STATUS_HERSTELLUNGSKALENDERWOCHE](#job-status-herstellungskalenderwoche) - Lesen der Kalenderwoche Byte 12
- [STATUS_HERSTELLUNGSKALENDERJAHR](#job-status-herstellungskalenderjahr) - Lesen des Kalenderjahrs Byte 13
- [STATUS_ZULIEFERER](#job-status-zulieferer) - Lesen des Zulieferers Byte 14
- [STATUS_SOFTWARESTAND](#job-status-softwarestand) - Lesen des Softwaretandes Byte 15
- [FS_ANZAHL](#job-fs-anzahl) - Fehlerspeicher lesen (alle Fehler) Security Access Level 1 notwendig
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler)
- [FS_LESEN_FELD](#job-fs-lesen-feld) - Fehlerspeicher lesen (ein Fehlerfeld)
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher Löschen Security Access Level 2 notwendig
- [STATUS_AD_KANAL](#job-status-ad-kanal) - analoge A/D Werte lesen Security Access Level 1 notwendig
- [STATUS_DREHZAHL](#job-status-drehzahl) - aktuelle Drehzahl lesen Security Access Level 1 notwendig
- [STATUS_GESCHWINDIGKEIT](#job-status-geschwindigkeit) - aktuelle Geschwindigkeit lesen Security Access Level 1 notwendig
- [STATUS_VERBRAUCH](#job-status-verbrauch) - Verbrauch lesen Security Access Level 1 notwendig
- [STATUS_DIGITAL_EA](#job-status-digital-ea) - alle digitalen Ein und Ausgänge lesen Security Access Level 1 notwendig
- [STATUS_TANKINHALT](#job-status-tankinhalt) - Tankinhalt lesen Security Access Level 1 notwendig
- [STATUS_TEMP_MOTOR](#job-status-temp-motor) - angezeigte Kühlmittel Temperatur lesen Security Access Level 1 notwendig
- [STATUS_GANG](#job-status-gang) - Anzeige aktueller Gang Security Access Level 1 notwendig
- [STATUS_RESERVEANZEIGE](#job-status-reserveanzeige) - Warnung TankAnzeige Security Access Level 1 notwendig
- [STATUS_TEMP_LUFT](#job-status-temp-luft) - Lufttemperatur lesen Security Access Level 1 notwendig
- [STATUS_TASTER_BORDCOMPUTER](#job-status-taster-bordcomputer) - Zustand Taster Bordcomputer auslesen Security Access Level 1 notwendig
- [STATUS_BATTERIE](#job-status-batterie) - Batteriespannung, Radio Eingang, Zündung lesen Security Access Level 1 notwendig
- [STEUERN_DREHZAHLMESSER](#job-steuern-drehzahlmesser) - Drehzahlmesser ansteuern Security Access Level 1 notwendig
- [STEUERN_GESCHWINDIGKEIT](#job-steuern-geschwindigkeit) - Geschwindigkeit ansteuern Security Access Level 1 notwendig
- [STEUERN_TANK_ANZEIGE](#job-steuern-tank-anzeige) - Tankanzeige ansteuern Security Access Level 1 notwendig
- [STEUERN_KUEHLMITTEL_ANZEIGE](#job-steuern-kuehlmittel-anzeige) - Kühlmittel Anzeige ansteuern Security Access Level 1 notwendig
- [STEUERN_GANG_ANZEIGE](#job-steuern-gang-anzeige) - Ganganzeige ansteuern Security Access Level 1 notwendig
- [STEUERN_SELBSTTEST_AKTIVIEREN](#job-steuern-selbsttest-aktivieren) - Selbst-Test starten Security Access Level 1 notwendig
- [STEUERN_SELBSTTEST_DEAKTIVIEREN](#job-steuern-selbsttest-deaktivieren) - Selbst-Test starten Security Access Level 1 notwendig
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [ECU_RESET](#job-ecu-reset)

<a id="job-info"></a>
### INFO

Information SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergerät im Klartext |
| ORIGIN | string | Steuergeräte-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| PACKAGE | string | Include-Paket-Nummer |
| SPRACHE | string | deutsch, english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-sec-access"></a>
### SEC_ACCESS

SG für erweiterte Diagnose freischalten Simple Protection Mode Algorithmus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LEVEL | int | Security Level Werte 1 oder 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-teilenummer"></a>
### STATUS_TEILENUMMER

Lesen der Teilenummer Byte 4-7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | BMW-Teilenummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-hardwarestand"></a>
### STATUS_HARDWARESTAND

Lesen des Hardwarestandes Byte 8

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Hardwarestand Wert BCD |
| STAT_WERT_TEXT | string | Hardwarestand Text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-codierbarkeit"></a>
### STATUS_CODIERBARKEIT

Lesen der Codierbarkeit Byte 9

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Codierbarkeit |
| STAT_WERT_TEXT | string | Wert Codierbarkeit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-diagnoseindex"></a>
### STATUS_DIAGNOSEINDEX

Lesen des Diagnoseindex Byte 10

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Diagnoseindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-busindex"></a>
### STATUS_BUSINDEX

Lesen des BusIndex Byte 11

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Busindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-herstellungskalenderwoche"></a>
### STATUS_HERSTELLUNGSKALENDERWOCHE

Lesen der Kalenderwoche Byte 12

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Kalenderwoche |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-herstellungskalenderjahr"></a>
### STATUS_HERSTELLUNGSKALENDERJAHR

Lesen des Kalenderjahrs Byte 13

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Kalenderjahr |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-zulieferer"></a>
### STATUS_ZULIEFERER

Lesen des Zulieferers Byte 14

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Zulieferer |
| STAT_WERT_TEXT | string | Text Zulieferer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-softwarestand"></a>
### STATUS_SOFTWARESTAND

Lesen des Softwaretandes Byte 15

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Softwarestand Wert BCD |
| STAT_WERT_TEXT | string | Softwarestand Text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-fs-anzahl"></a>
### FS_ANZAHL

Fehlerspeicher lesen (alle Fehler) Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ANZAHL | int | Anzahl der Fehler im Speicher |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers |
| F_ANZAHL | int | Anzahl der Fehler im Speicher |
| F_ORT_NR | long | Index für den Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text Table FOrteTexte als ORTTEXT |
| F_SYMPTOM_NR | int | Index für die Fehlerart |
| F_SYMPTOM_TEXT | string | Fehlerart als Text Table FArtTexte als ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard Fehlerart) als Text |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard Fehlerart) als Text Fehlerart table ArtTexte als Text |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard Fehlerart) als Text |
| F_HFK | int | Haeufigkeitszaehler |
| F_UW_KL30 | real | Umweltbedingung Batteriespannung |
| F_UW_KL30_EINH | string | Einheit Batteriespannung  in Volt |
| F_UW_KM | long | Umweltbedingung Kilometerstand |
| F_UW_KM_EINH | string | Einheit Kilometerstand km |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hex Code |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| _TEL_ANTWORT2 | binary | Hex Antwort vom SG |
| _TEL_ANTWORT3 | binary | Hex Antwort vom SG |

<a id="job-fs-lesen-feld"></a>
### FS_LESEN_FELD

Fehlerspeicher lesen (ein Fehlerfeld)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NUMMER | int | Eingabe Fehler Feld 1..3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers |
| F_ANZAHL | int | Anzahl der Fehler im Speicher |
| F_ORT_NR | long | Index für den Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text Table FOrteTexte als ORTTEXT |
| F_SYMPTOM_NR | int | Index für die Fehlerart |
| F_SYMPTOM_TEXT | string | Fehlerart als Text Table FArtTexte als ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard Fehlerart) als Text |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard Fehlerart) als Text Fehlerart table ArtTexte als Text |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard Fehlerart) als Text |
| F_HFK | int | Haeufigkeitszaehler |
| F_UW_KL30 | real | Umweltbedingung Batteriespannung |
| F_UW_KL30_EINH | string | Einheit Batteriespannung  in Volt |
| F_UW_KM | long | Umweltbedingung Kilometerstand |
| F_UW_KM_EINH | string | Einheit Kilometerstand km |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hex Code |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher Löschen Security Access Level 2 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-ad-kanal"></a>
### STATUS_AD_KANAL

analoge A/D Werte lesen Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_KL30_WERT | unsigned int | A/D Wert Batteriespannung |
| STAT_FOTOZELLE_WERT | unsigned int | A/D Wert Spannung Foto Transistor |
| STAT_LCD_WERT | unsigned int | A/D Wert negative Spannung LCD Display |
| STAT_TEMP_WERT | unsigned int | A/D Wert Spannung Sensor Kuehlmittel Temperatur |
| STAT_TANK_WERT | unsigned int | A/D Wert Spannung Sensor Füllstand Tank |
| STAT_OAT_WERT | unsigned int | A/D Wert Spannung Sensor OAT |
| STAT_LCD_TEMP_WERT | unsigned int | A/D Wert Spannung LCD Temperatur |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-drehzahl"></a>
### STATUS_DREHZAHL

aktuelle Drehzahl lesen Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT | int | Motordrehzahl im Kombiinstrument |
| STAT_EINH | string | Einheit 1/min |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-geschwindigkeit"></a>
### STATUS_GESCHWINDIGKEIT

aktuelle Geschwindigkeit lesen Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT | int | Geschwindigkeit im Kombiinstrument |
| STAT_EINH | string | Einheit km/h |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-verbrauch"></a>
### STATUS_VERBRAUCH

Verbrauch lesen Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_ZAEHLER_WERT | unsigned long |  |
| STAT_VERBRAUCH_WERT | real | Verbrauch |
| STAT_VERBRAUCH_EINH | string | Einheit Verbrauch |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-digital-ea"></a>
### STATUS_DIGITAL_EA

alle digitalen Ein und Ausgänge lesen Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_DDR_PORT_0 | unsigned char | DDR Port 0 |
| STAT_PDR_PORT_0 | unsigned char | PDR Port 0 |
| STAT_DDR_PORT_1 | unsigned char | DDR Port 1 |
| STAT_PDR_PORT_1 | unsigned char | PDR Port 1 |
| STAT_DDR_PORT_2 | unsigned char | DDR Port 2 |
| STAT_PDR_PORT_2 | unsigned char | PDR Port 2 |
| STAT_DDR_PORT_3 | unsigned char | DDR Port 3 |
| STAT_PDR_PORT_3 | unsigned char | PDR Port 3 |
| STAT_DDR_PORT_4 | unsigned char | DDR Port 4 |
| STAT_PDR_PORT_4 | unsigned char | PDR Port 4 |
| STAT_DDR_PORT_5 | unsigned char | DDR Port 5 |
| STAT_PDR_PORT_5 | unsigned char | PDR Port 5 |
| STAT_DDR_PORT_6 | unsigned char | DDR Port 6 |
| STAT_PDR_PORT_6 | unsigned char | PDR Port 6 |
| STAT_DDR_PORT_7 | unsigned char | DDR Port 7 |
| STAT_PDR_PORT_7 | unsigned char | PDR Port 7 |
| STAT_DDR_PORT_8 | unsigned char | DDR Port 8 |
| STAT_PDR_PORT_8 | unsigned char | PDR Port 8 |
| STAT_DDR_PORT_9 | unsigned char | DDR Port 9 |
| STAT_PDR_PORT_9 | unsigned char | PDR Port 9 |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-tankinhalt"></a>
### STATUS_TANKINHALT

Tankinhalt lesen Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_MESSWERT_WERT | int | Messwert vom Geber |
| STAT_ANZEIGE_WERT | int | Anzeigewert im Kombiinstrument |
| STAT_ANZEIGE_EINH | string | Einheit Tankinhalt |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-temp-motor"></a>
### STATUS_TEMP_MOTOR

angezeigte Kühlmittel Temperatur lesen Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT | unsigned int |  |
| STAT_EINH | string | Prozent |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-gang"></a>
### STATUS_GANG

Anzeige aktueller Gang Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT | string |  |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-reserveanzeige"></a>
### STATUS_RESERVEANZEIGE

Warnung TankAnzeige Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT | string | EIN - Warnalmape an, AUS - Warnlampe aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-temp-luft"></a>
### STATUS_TEMP_LUFT

Lufttemperatur lesen Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT | real | Lufttemperatur |
| STAT_EINH | string | °F - Fahrenheit, °C - Celsius |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-taster-bordcomputer"></a>
### STATUS_TASTER_BORDCOMPUTER

Zustand Taster Bordcomputer auslesen Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT | string | EIN/AUS |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-batterie"></a>
### STATUS_BATTERIE

Batteriespannung, Radio Eingang, Zündung lesen Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_KL30_WERT | real | Batteriespannung |
| STAT_EINH | string | Spannung in Volt |
| STAT_KL15_WERT | string | Zustand Ein, Aus |
| STAT_RADIO_EINGANG | string | Zustand Ein, Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-drehzahlmesser"></a>
### STEUERN_DREHZAHLMESSER

Drehzahlmesser ansteuern Security Access Level 1 notwendig

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | int | Zeit Ansteuerung in Sekunden, 1..20 Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-geschwindigkeit"></a>
### STEUERN_GESCHWINDIGKEIT

Geschwindigkeit ansteuern Security Access Level 1 notwendig

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | int | Zeit Ansteuerung in Sekunden, 1..20 Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-tank-anzeige"></a>
### STEUERN_TANK_ANZEIGE

Tankanzeige ansteuern Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-kuehlmittel-anzeige"></a>
### STEUERN_KUEHLMITTEL_ANZEIGE

Kühlmittel Anzeige ansteuern Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-gang-anzeige"></a>
### STEUERN_GANG_ANZEIGE

Ganganzeige ansteuern Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-selbsttest-aktivieren"></a>
### STEUERN_SELBSTTEST_AKTIVIEREN

Selbst-Test starten Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-selbsttest-deaktivieren"></a>
### STEUERN_SELBSTTEST_DEAKTIVIEREN

Selbst-Test starten Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-ecu-reset"></a>
### ECU_RESET

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (12 × 2)
- [FORTTEXTE](#table-forttexte) (14 × 2)
- [FARTTEXTE](#table-farttexte) (7 × 2)
- [FEHLERSTATUS](#table-fehlerstatus) (5 × 2)
- [FEHLERCODETEST](#table-fehlercodetest) (3 × 2)
- [WARNLAMPE](#table-warnlampe) (3 × 2)
- [LIEFERANTEN](#table-lieferanten) (3 × 2)
- [VERBRAUCH](#table-verbrauch) (4 × 2)
- [GANG](#table-gang) (10 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 12 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | FEHLER |
| 0x02 | FEHLER: ARGUMENTE |
| 0x03 | FEHLER: AUSSERHALB BEREICH |
| 0x04 | FEHLER: ZUGRIFF VERWEIGERT |
| 0x05 | FEHLER: FORMATFEHLER DATEN (NICHT HEX) |
| 0x08 | FEHLER: ZUGRIFF VERWEIGERT |
| 0xA0 | OKAY |
| 0xB0 | FEHLER: PARAMETER |
| 0xB1 | FEHLER: FUNKTION |
| 0xFF | FEHLER: AUSFUEHRUNG NICHT MOEGLICH |
| 0x00 | FEHLER: UNBEKANNT |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | EHKS Fehler |
| 0x02 | IBUS Fehler |
| 0x03 | Kühlmitteltemperatur Fehler |
| 0x04 | Kraftstoffüllstand Fehler |
| 0x05 | Falscher Key |
| 0x06 | Umgebungstemperatur Fehler |
| 0x07 | Geschwindigkeitswert Fehler |
| 0x08 | Überspannung |
| 0x09 | Unterspannung |
| 0x0A | Power On Rest |
| 0x0B | Verbrauchwert Fehler |
| 0x0C | Radio Fehler |
| 0x10 | Interner Fehler |
| 0xFF | unbekannt |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 7 rows × 2 columns

| WERT | ARTTEXT |
| --- | --- |
| 0x00 |  |
| 0x01 | Kurzschluss nach Plus |
| 0x02 | Kurzschluss nach Masse |
| 0x04 | Unterbrechung |
| 0x05 | Kurzschluss nach Plus oder Unterbrechung |
| 0x08 | Unplausibel |
| 0xFF | unbekannte Fehlerart |

<a id="table-fehlerstatus"></a>
### FEHLERSTATUS

Dimensions: 5 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Fehler nicht vorhanden |
| 0x01 | Fehler vorhanden |
| 0x02 | Fehler sporadisch |
| 0x03 | Fehler vorhenden und gespeichert |
| 0xFF | unbekannt |

<a id="table-fehlercodetest"></a>
### FEHLERCODETEST

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | TEST VOLLSTAENDIG |
| 0x01 | TEST UNVOLLSTAENDIG |
| 0xFF | UNBEKANNT |

<a id="table-warnlampe"></a>
### WARNLAMPE

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Aus |
| 0x01 | Ein |
| 0xFF | UNBEKANNT |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 3 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x46 | Gemel |
| 0x56 | Siemens VDO Automotive |
| 0xFF | Hersteller unbekannt |

<a id="table-verbrauch"></a>
### VERBRAUCH

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | L/100km |
| 0x01 | mpgUK |
| 0x02 | mpgUS |
| 0xFF | UNBEKANNT |

<a id="table-gang"></a>
### GANG

Dimensions: 10 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | Leerlauf |
| 0x01 | 1. Gang |
| 0x02 | 2. Gang |
| 0x03 | 3. Gang |
| 0x04 | 4. Gang |
| 0x05 | 5. Gang |
| 0x06 | 6. Gang |
| 0x07 | 7. Gang |
| 0x08 | 8. Gang |
| 0xFF | UNBEKANNT |
