# kombir40.prg

- Jobs: [34](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | KOMBI R40 |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 2.01 |
| AUTHOR | BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Default ident job
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicherinhalt aus SG lesen
- [SOFTWARE_RESET](#job-software-reset) - Kombi loest selbststaendig einen Reset aus
- [SIA_RESET](#job-sia-reset) - Ruecksetzen der Service-Intervall-Anzeige
- [GWSZ_RESET](#job-gwsz-reset) - GWSZ zuruecksetzen, nur moeglich wenn Km-Stand &lt; 255
- [AIF_GWSZ_LESEN](#job-aif-gwsz-lesen) - Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen
- [AIF_ZENTRALCODE_LESEN](#job-aif-zentralcode-lesen) - Anwenderinfofeld Block 4 auslesen
- [AIF_FG_NR_LESEN](#job-aif-fg-nr-lesen) - Auslesen der Fahrgestellnummer
- [AIF_DATUM_FZ_LESEN](#job-aif-datum-fz-lesen) - Auslesen des Herstelldatums des FZ
- [PROD_DATUM_LESEN](#job-prod-datum-lesen)
- [AIF_SIA_DATEN_LESEN](#job-aif-sia-daten-lesen) - Anwenderinfofeld Block 3 auslesen
- [STEUERN_ANZEIGE](#job-steuern-anzeige) - Anzeigenkomponenten steuern
- [STEUERN_GONG](#job-steuern-gong) - Gong ansteuern
- [STEUERN_LEUCHTE](#job-steuern-leuchte) - Leuchten in der Anzeigeeinheit ansteuern Es muessen 7 Argumente uebergeben werden. Die Belegung der Datenbytes ist separat beschrieben.
- [STEUERN_IO](#job-steuern-io) - I/O-Port-Ausgaenge steuern
- [STATUS_IO_LESEN](#job-status-io-lesen) - Eingangs- und Ausgangsstati lesen
- [STATUS_ANALOG_LESEN](#job-status-analog-lesen) - Spezielle analoge Eingaenge lesen
- [RAM_LESEN](#job-ram-lesen) - RAM-Speicher auslesen
- [ROM_LESEN](#job-rom-lesen) - ROM-Speicher auslesen
- [EEPROM_LESEN](#job-eeprom-lesen) - EEPROM-Speicher auslesen
- [DPRAM_LESEN](#job-dpram-lesen) - DPRAM-Speicher auslesen
- [ZCS_LESEN](#job-zcs-lesen) - Anwenderinfofeld Wortadr. 34-3D auslesen
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - SG - Selbsttest ausloesen
- [GWSZ_OFFSET_LESEN](#job-gwsz-offset-lesen) - OFFSET-Wert des GWSZ aus EEPROM lesen
- [GWSZ_OFFSET_SCHREIBEN](#job-gwsz-offset-schreiben) - OFFSET-Wert des GWSZ in EEPROM schreiben
- [STATUS_CAN_FUNKTION_LESEN](#job-status-can-funktion-lesen) - Zeigt an, ob CAN-Funktionalitaet vorhanden ist

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ARGUMENT, wenn Argumente nicht uebergeben oder ausser Bereich |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-info"></a>
### INFO

Information SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergeraet im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Name aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch, english |

<a id="job-ident"></a>
### IDENT

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_COD_INDEX | int | Codierindex |
| ID_DIAG_INDEX | int | Diagnoseindex |
| ID_BUS_INDEX | int | Busindex |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferantennummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| ID_CAN_INDEX | int | CAN-Index |
| ID_AENDERUNGSINDEX | int | Aenderungsindex |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicherinhalt aus SG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zum Fehlerort |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int | Fehlerart-Nr |
| F_ART1_TEXT | string | Fehlerart-Text |
| F_ART2_NR | int | Fehlerart-Nr |
| F_ART2_TEXT | string | Fehlerart-Text |
| F_ART3_NR | int | Fehlerart-Nr |
| F_ART3_TEXT | string | Fehlerart-Text |
| F_ART4_NR | int | Fehlerart-Nr |
| F_ART4_TEXT | string | Fehlerart-Text |
| F_ART5_NR | int | Fehlerart-Nr |
| F_ART5_TEXT | string | Fehlerart-Text |
| F_ART6_NR | int | Fehlerart-Nr |
| F_ART6_TEXT | string | Fehlerart-Text |
| F_ART7_NR | int | Fehlerart-Nr |
| F_ART7_TEXT | string | Fehlerart-Text |
| F_UW_ANZ | int | immer 0 |
| F_HEX_CODE | binary | Hexdaten des Fehlers |

<a id="job-software-reset"></a>
### SOFTWARE_RESET

Kombi loest selbststaendig einen Reset aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-sia-reset"></a>
### SIA_RESET

Ruecksetzen der Service-Intervall-Anzeige

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | moegliche Uebergabeparameter: Oel_Reset, Weg_Reset, Zeit_Reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-gwsz-reset"></a>
### GWSZ_RESET

GWSZ zuruecksetzen, nur moeglich wenn Km-Stand &lt; 255

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-aif-gwsz-lesen"></a>
### AIF_GWSZ_LESEN

Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_GWSZ_WERT | long | Gesamtwegstreckenzaehler |
| STAT_GWSZ_EINH | string | Einheit des GWSZ [km] |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-aif-zentralcode-lesen"></a>
### AIF_ZENTRALCODE_LESEN

Anwenderinfofeld Block 4 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| GM | string | C1 Zifferncode fuer Grundmerkmal |
| SA | string | C2 Zifferncode fuer Sonderausstattung |
| VM | string | C3 Zifferncode fuer Versionsmerkmal |
| STAT_ZENTRALCODE_ANLIEFERCODIERUNG | int | True falls der Zentralcode der Anliefercodierung entspricht |
| TELEGRAMM | binary |  |

<a id="job-aif-fg-nr-lesen"></a>
### AIF_FG_NR_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| AIF_FG_NR | string | Fahrgestellnummer |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-aif-datum-fz-lesen"></a>
### AIF_DATUM_FZ_LESEN

Auslesen des Herstelldatums des FZ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATUM_FZ | string | Herstelldatum des FZ |
| TELEGRAMM | binary |  |

<a id="job-prod-datum-lesen"></a>
### PROD_DATUM_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| TAG | string |  |
| MONAT | string |  |
| JAHR | string |  |

<a id="job-aif-sia-daten-lesen"></a>
### AIF_SIA_DATEN_LESEN

Anwenderinfofeld Block 3 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| STAT_MOTORTYP_NR | int | 0 = Benzinmotor, 1 = Dieselmotor |
| STAT_MOTORTYP_TEXT | string | "Benzinmotor", "Dieselmotor" |
| STAT_GETRIEBE_NR | int | 0, 1, (siehe table Getriebetypen) |
| STAT_GETRIEBE_TEXT | string | siehe table Getriebetypen |
| STAT_ZEITINSPEKTION_AUS | int | keine Zeitinspektion = 1 |
| STAT_VORGEZOGENE_ZEITINSPEKTION_AUS | int | keine Zeitinspektion = 1 |
| STAT_INSPEKTIONSGRENZE_WERT | int | Inspektionsgrenze |
| STAT_INSPEKTIONSGRENZE_EINH | string | Einheit "Liter" |
| STAT_ZEITGRENZE_WERT | int | Zeitgrenze |
| STAT_ZEITGRENZE_EINH | string | Einheit "Tage" |
| STAT_KRAFTSTOFFMENGE_WERT | int | verbrauchte SI-Kraftstoffmenge |
| STAT_KRAFTSTOFFMENGE_EINH | string | Einheit "Liter" |
| STAT_ZEIT_INSP_ZAEHLER_WERT | int | Zeitinspektionszaehler |
| STAT_ZEIT_INSP_ZAEHLER_EINH | string | Einheit "Tage" |
| STAT_SERVICE_ART | int | 0 = Inspektion, 1 = Oelservice |
| TELEGRAMM | binary |  |

<a id="job-steuern-anzeige"></a>
### STEUERN_ANZEIGE

Anzeigenkomponenten steuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Zu steuernde Komponente, siehe table Komponenten moegliche Uebergabeparamter: TACHO, DREHZAHL, TANKINHALT, KUEHLMITTELTEMPERATUR |
| WERT | int | Winkelgrade im Bereich von (10-90) Grad, Mit Spruengen von mehr als 90 Grad sollten die Messwerke nicht beaufschlagt werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-gong"></a>
### STEUERN_GONG

Gong ansteuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | 0 = Gong 'aus', 1 = Gong 'ein' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-leuchte"></a>
### STEUERN_LEUCHTE

Leuchten in der Anzeigeeinheit ansteuern Es muessen 7 Argumente uebergeben werden. Die Belegung der Datenbytes ist separat beschrieben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Belegung 0. Datenbytes: (0-0xFF) Bit0: Bulb Failure Bit1: Rear Fogs Bit2: Front Fogs Bit3: open Bit4: open Bit5: Check Engine Bit6: Overspeed Bit7: open |
| BYTE1 | int | Belegung 1. Datenbytes: (0-0xFF) Bit0: open Bit1: Trailer warning Bit2: Glow Plug Bit3: Brake Pad Wear Bit4: Traction Control Bit5: Low Engine Coolant Bit6: Door Open Bit7: Low Washer Level |
| BYTE2 | int | Belegung 2. Datenbytes: (0-0xFF) Bit0: open Bit1: Mil RED Bit2: Brake Failure Bit3: High Coolant Temp Bit4: MIL Yellow Bit5: Low Fuel Level Bit6: Cruise Control Bit7: High Beam |
| BYTE3 | int | Belegung 3. Datenbytes: (0-0xFF) Bit0: open Bit1: open Bit2: open Bit3: open Bit4: open Bit5: open Bit6: open Bit7: open |
| BYTE4 | int | Belegung 4. Datenbytes: (0-0xFF) Bit0: open Bit1: open Bit2: open Bit3: open Bit4: open Bit5: open Bit6: open Bit7: open |
| BYTE5 | int | Belegung 5. Datenbytes: (0-0xFF) Bit0: open Bit1: open Bit2: open Bit3: open Bit4: open Bit5: open Bit6: open Bit7: open |
| BYTE6 | int | Belegung 6. Datenbytes: (0-0xFF) Bit0: open Bit1: open Bit2: open Bit3: open Bit4: open Bit5: open Bit6: Left DI (inc. Tick tock) Bit7: Right DI (inc. Tick tock) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-io"></a>
### STEUERN_IO

I/O-Port-Ausgaenge steuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PORT4 | int | Belegung Datenbyte: (0-0x0F) Bit0: open Bit1: open Bit2: open Bit3: open Bit4: open Bit5: open Bit6: Flasher Left Bit7: Flasher Right |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Eingangs- und Ausgangsstati lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_HANDBREMSE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_GURTKONTAKT_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_OELDRUCK_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KL50_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" 1, wenn "TRUE" , 0, wenn "FALSE" |
| STAT_KLR_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KL15_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KUEHLMITTELSTAND_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KOMBITASTE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-analog-lesen"></a>
### STATUS_ANALOG_LESEN

Spezielle analoge Eingaenge lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_5V_WERT | int | AD - Kanal 0, 5V fixe Spannung |
| STAT_5V_EINH | string | Einheit [ADC-Wert] |
| STAT_HEBELGEBER1_WERT | int | AD - Kanal 1, Wert des 1. Hebelgebers |
| STAT_HEBELGEBER1_EINH | string | Einheit [ADC-Wert] |
| STAT_AUSSENTEMP_WERT | int | Wert AD - Kanal 7, Wert der Aussentemperatur |
| STAT_AUSSENTEMP_EINH | string | Einheit [ADC-Wert] |
| STAT_GESCHWINDIGKEIT_WERT | long | Wert des Wegeingangs, Wert der Geschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit [km/h] |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-ram-lesen"></a>
### RAM_LESEN

RAM-Speicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAM_TYPE | string | "INTERN" ,"EXTERN" oder "DP_RAM" |
| ADRESSE | string | Hexwert (0x000-0xFFF) der Adresse ,ab der das Ram gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Bytes (max. 32 !) die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| DATEN | binary | Datenfeld |

<a id="job-rom-lesen"></a>
### ROM_LESEN

ROM-Speicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x0000-0xFFFF) der Adresse ,ab der das Rom gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Bytes (max. 32 !) die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| DATEN | binary | Datenfeld |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

EEPROM-Speicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x00-0xFF) der WortAdresse ,ab der das EEPROM gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der 2-Byte-Worte (max. 16 Worte = 32 Bytes), die ausgelesen werden koennen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| DATEN | binary | Datenfeld |

<a id="job-dpram-lesen"></a>
### DPRAM_LESEN

DPRAM-Speicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x80-0xDF) der Adresse ,ab der gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Bytes (max. 16 !) die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| DATEN | binary | Datenfeld |

<a id="job-zcs-lesen"></a>
### ZCS_LESEN

Anwenderinfofeld Wortadr. 34-3D auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| GM | string | C1 Zifferncode fuer Grundmerkmal |
| SA | string | C2 Zifferncode fuer Sonderausstattung |
| VM | string | C3 Zifferncode fuer Versionsmerkmal |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

SG - Selbsttest ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-gwsz-offset-lesen"></a>
### GWSZ_OFFSET_LESEN

OFFSET-Wert des GWSZ aus EEPROM lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| GWSZ_OFFSET_WERT | int | absoluter Offset-Wert des GWSZ (0-255) |

<a id="job-gwsz-offset-schreiben"></a>
### GWSZ_OFFSET_SCHREIBEN

OFFSET-Wert des GWSZ in EEPROM schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GWSZ_OFFSET_WERT | int | absoluter Offset-Wert des GWSZ |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-status-can-funktion-lesen"></a>
### STATUS_CAN_FUNKTION_LESEN

Zeigt an, ob CAN-Funktionalitaet vorhanden ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| STAT_CAN_FUNKTION_EIN | int | 0 = keine CAN-Funktionalitaet,d.h. konventionelles Kombi, 1 = CAN-Kombi |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (10 × 2)
- [LIEFERANTEN](#table-lieferanten) (47 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [SIARESET](#table-siareset) (3 × 2)
- [FORTTEXTE](#table-forttexte) (19 × 2)
- [FARTTEXTE](#table-farttexte) (8 × 2)
- [GETRIEBETYPEN](#table-getriebetypen) (3 × 2)
- [PROGRAMMINFO](#table-programminfo) (7 × 2)
- [KOMPONENTEN](#table-komponenten) (6 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 10 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| ?10? | ERROR_ARGUMENT |
| ?20? | ERROR_FEHLERANZAHL |
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 47 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe |
| 0x10 | VDO |
| 0x11 | Valeo |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine |
| 0x18 | Teves |
| 0x19 | Elektromatik Suedafrika |
| 0x20 | Becker |
| 0x21 | Preh |
| 0x22 | Alps |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto |
| 0x26 | MotoMeter |
| 0x27 | Delphi PHI |
| 0x28 | DODUCO |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0x33 | Jatco |
| 0x34 | Fuba |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0x38 | Sachs |
| 0x39 | ITT |
| 0x40 | FTE |
| 0x41 | Megamos |
| 0x42 | TRW |
| 0x43 | Wabco |
| 0x44 | ISAD Electronic Systems |
| 0x45 | HEC (Hella Electronics Corporation) |
| 0x46 | Gemel |
| 0xFF | unbekannter Hersteller |

<a id="table-roverpartnumprefix"></a>
### ROVERPARTNUMPREFIX

Dimensions: 21 rows × 2 columns

| ROVER_NR | PREFIX |
| --- | --- |
| 0xA0 | AMR |
| 0xA1 | HHF |
| 0xA2 | JFC |
| 0xA3 | MKC |
| 0xA4 | SCB |
| 0xA5 | SRB |
| 0xA6 | XQC |
| 0xA7 | XQD |
| 0xA8 | XQE |
| 0xA9 | XVD |
| 0xAA | YAC |
| 0xAB | YDB |
| 0xAC | YFC |
| 0xAD | YUB |
| 0xAE | YWC |
| 0xAF | YWQ |
| 0xB0 | EGQ |
| 0xB1 | YIB |
| 0xB2 | YIC |
| 0xB3 | YIE |
| 0xXY | ??? |

<a id="table-siareset"></a>
### SIARESET

Dimensions: 3 rows × 2 columns

| SELECTOR | RESET |
| --- | --- |
| OEL_RESET | 0x01 |
| WEG_RESET | 0x02 |
| ZEIT_RESET | 0x04 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 19 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x87 | Kurzschluss gegen U-Batt oder Masse |
| 0x8C | Klemme R |
| 0x8F | Ueberspannung (U&gt;16V) |
| 0xBE | Lichtmodul-EEPROM-Fehler |
| 0xBF | KOMBIR40-EEPROM, Codierung fehlerhaft/unvollstaendig |
| 0xC1 | Signal TWEG+ (Tacho) |
| 0xC3 | TD |
| 0xC7 | Tank-Hebelgeber |
| 0xCE | Aussentemperatur |
| 0xCF | SIA-Reset |
| 0xF0 | CAN BUS OFF |
| 0xF4 | keine CAN ID |
| 0xF5 | keine CAN ID ASC1 |
| 0xF6 | keine CAN ID DME1 |
| 0xF7 | keine CAN ID DME2 |
| 0xF8 | keine CAN ID DME4 |
| 0xFB | keine CAN ID EGS1 |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 8 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | ungueltiger Arbeitsbereich |
| 0x07 | Fehler momentan vorhanden |
| 0x08 | sporadischer Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-getriebetypen"></a>
### GETRIEBETYPEN

Dimensions: 3 rows × 2 columns

| GETRIEBEART | GETRIEBETEXT |
| --- | --- |
| 0x00 | Schaltgetriebe |
| 0x01 | Automatikgetriebe (EGS) |
| 0xFF | unbekannte Getriebeart |

<a id="table-programminfo"></a>
### PROGRAMMINFO

Dimensions: 7 rows × 2 columns

| PROGRAMMINFO | PROGRAMMTEXT |
| --- | --- |
| 0x00 | E |
| 0x01 | M |
| 0x02 | S |
| 0x03 | W |
| 0x04 | A |
| 0x05 | Anzeige aus |
| 0xFF | unbekannte Programminfo |

<a id="table-komponenten"></a>
### KOMPONENTEN

Dimensions: 6 rows × 2 columns

| ORT | BYTE |
| --- | --- |
| TACHO | 0x0A |
| DREHZAHL | 0x0B |
| TANKINHALT | 0x0C |
| KUEHLMITTELTEMPERATUR | 0x0D |
| Fehler | 0xFF |
| unbekannt | 0xEE |
