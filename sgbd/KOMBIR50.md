# KOMBIR50.prg

- Jobs: [56](#jobs)
- Tables: [11](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | KOMBIR50 |
| ORIGIN | BMW TI-431 Lothar Dennert |
| REVISION | 1.05 |
| AUTHOR | Software-Style Mike Rafferty, BMW TI-431 Lothar Dennert, BMW TI-431 Robert Kuessel |
| COMMENT | V6.9 of Diag Spec |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [IDENT](#job-ident) - Ident-Daten fuer Instrument Pack
- [AIF_SIA_DATEN_LESEN](#job-aif-sia-daten-lesen) - Read the SIA from the User Information
- [AIF_DATUM_FZ_LESEN](#job-aif-datum-fz-lesen) - Read the Build Data from the User Information Auslesen Herstelldatum des FZ
- [AIF_GWSZ_LESEN](#job-aif-gwsz-lesen) - Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen Read the Kilometers from the User Information Memory Block
- [GWSZ_OFFSET_LESEN](#job-gwsz-offset-lesen) - OFFSET-Wert des GWSZ aus EEPROM lesen
- [GWSZ_MINUS_OFFSET_LESEN](#job-gwsz-minus-offset-lesen) - Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen und Offset abziehen
- [GWSZ_OFFSET_SCHREIBEN](#job-gwsz-offset-schreiben) - OFFSET-Wert des GWSZ in EEPROM schreiben
- [GWSZ_RESET](#job-gwsz-reset) - GWSZ zuruecksetzen, nur moeglich wenn Km-Stand &lt; 255
- [AIF_ZENTRALCODE_LESEN](#job-aif-zentralcode-lesen) - Anwenderinfofeld Block 4 auslesen Read the ZCS from the AIF record
- [C_ZCS_LESEN](#job-c-zcs-lesen) - Anwenderinfofeld Block 4 auslesen Read the ZCS from the AIF record
- [C_ZCS_AUFTRAG](#job-c-zcs-auftrag) - Write and verify the Central code
- [AIF_FG_NR_LESEN](#job-aif-fg-nr-lesen) - Read the VIN from the User Information Auslesen der Fahrgestellnummer aus dem Anwenderinfofeld
- [C_FG_LESEN](#job-c-fg-lesen) - Read the VIN from the User Information Auslesen der Fahrgestellnummer aus dem Anwenderinfofeld
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Schreiben der 7-stelligen Fahrgestellnummer Write the 7 digit VIN into block 2 of the AIF record
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen Read the coding data
- [CODIERBLOCK_LESEN](#job-codierblock-lesen) - Codierblock auslesen Read the coding data
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren Write and then verify the coding data
- [RAM_LESEN](#job-ram-lesen) - RAM-Speicher auslesen Read internal and external RAM
- [ROM_LESEN](#job-rom-lesen) - ROM-Speicher auslesen Read ROM out of IKE
- [EEPROM_LESEN](#job-eeprom-lesen) - EEPROM-Speicher auslesen Read EEPROM out of IKE
- [PSEUDO_EEPROM_LESEN](#job-pseudo-eeprom-lesen) - PSEUDO-EEPROM-Speicher auslesen Read EEPROM out of IKE
- [STATUS_IO_POWER](#job-status-io-power) - Read Power digital inputs from Port 0
- [STATUS_IO_TRIP_RESET](#job-status-io-trip-reset) - Read Trip Reset digital input from Port 3
- [STATUS_IO_DIMMER_SW](#job-status-io-dimmer-sw) - Read dimmer switch digital inputs from Port 1
- [STATUS_IO_MISC](#job-status-io-misc) - Read miscellaneous digital inputs from Port 2
- [STATUS_IO_HAZARD_SW](#job-status-io-hazard-sw) - Read hazard switch digital input from Port 4
- [STATUS_IO_WAKE_UP](#job-status-io-wake-up) - Read 10 minute wake up status from port 2
- [STATUS_IO_LCD_BACKLIGHT](#job-status-io-lcd-backlight) - Read LCD Backlight input from port 4
- [STATUS_IO_CAN_SHUTDOWN](#job-status-io-can-shutdown) - Read status of CAN shutdown output from port 4
- [STATUS_IO_KBUS_INTERRUPT](#job-status-io-kbus-interrupt) - Read status of Kbus interrupt from port 2
- [STATUS_IO_DIMMER_DRIVER](#job-status-io-dimmer-driver) - Read dimmer driver digital input from Port 4
- [STATUS_IO_LED_DIG_INPUTS](#job-status-io-led-dig-inputs) - Read LED 19, LED 20 and LED A9 digital inputs from Port 3
- [STATUS_IO_MOTOR_DRIVERS](#job-status-io-motor-drivers) - Read status of the motor drivers from port 2
- [READ_DIGITAL](#job-read-digital) - Read all Digital Inputs for a specified port
- [STATUS_ANALOG](#job-status-analog) - Read Analogue Input States
- [STATUS_TANKINHALT_LESEN](#job-status-tankinhalt-lesen) - Tankinhalt lesen
- [STATUS_AUSSENTEMP_LESEN](#job-status-aussentemp-lesen) - Read Temprature
- [STEUERN_LEUCHTE](#job-steuern-leuchte) - Force the warning lamps in byte blocks
- [STEUERN_ANZEIGE](#job-steuern-anzeige) - Force an instrument gauge
- [STEUERN_ALL_GAUGES](#job-steuern-all-gauges) - Force all instrument gauges
- [STEUERN_PANEL_LIGHT](#job-steuern-panel-light) - Force the Panel Illumination
- [STEUERN_BACKLIGHT](#job-steuern-backlight) - Force the Odometer and trip computer backlight
- [STEUERN_GONG](#job-steuern-gong) - Force the gong
- [STEUERN_LCD_ODO](#job-steuern-lcd-odo) - Force the LCD Odometer
- [STEUERN_LCD_TRIP](#job-steuern-lcd-trip) - Force the LCD trip computer
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Perform ECU Self Test
- [SIA_RESET](#job-sia-reset) - Force an SIA reset
- [ZEITINSPEKTIONSZAEHLER_LESEN](#job-zeitinspektionszaehler-lesen) - Zeitinspektionszaehler auslesen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Read the Test Stamp Default pruefstempel_lesen job
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Read the Test Stamp Beschreiben des Pruefstempels
- [SOFTWARE_RESET](#job-software-reset) - Instrument cluster will reset itself Kombi loest selbststaendig einen Reset aus
- [SLEEP_MODE](#job-sleep-mode) - Send the ECU into sleep mode
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - ECU Pinging message
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden Terminate the diagnostic session

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

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer Instrument Pack

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_BMW_NR | string | BMW-Teilenummer BMW Part number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW Week of manufacture |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Year of manufacture |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_SW_NR | int | Softwarenummer |
| ID_CAN_INDEX | int | Can Index |
| ID_AENDERUNG_INDEX | int | Modification Index (minor software modifications) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-aif-sia-daten-lesen"></a>
### AIF_SIA_DATEN_LESEN

Read the SIA from the User Information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORTYP_NR | int | Fuel type of vehicle 0=Petrol, 1=Diesel 0=Benzinmotor, 1=Dieselmotor |
| STAT_MOTORTYP_TEXT | string | Fuel type of vehicle as text |
| STAT_GETRIEBE_NR | int | Transmission type of vehicle 1=Manual, 0=Automatic 1=Schaltgetriebe, 0=Automatikgetriebe |
| STAT_GETRIEBE_TEXT | string | Transmission type of vehicle as text |
| STAT_ZEITINSPEKTION | int | time inspection enabled = 1 Zeitinspektion enabled = 1 |
| STAT_VORGEZOGENE_ZEITINSPEKTION | int | premature time inspection = 1 vorgezogene Zeitinspektion = 1 |
| STAT_INSPEKTIONSGRENZE_WERT | int | Allowed volume of fuel between service Inspektionsgrenze [Liter] |
| STAT_INSPEKTIONSGRENZE_EINH | string | Unit = Litre |
| STAT_ZEITGRENZE_WERT | int | Number of days between time service Zeitgrenze [Tage] |
| STAT_ZEITGRENZE_EINH | string | Unit = Days |
| STAT_KRAFTSTOFFMENGE_WERT | int | Consumed litres since last service verbrauchte SI-Kraftstoffmenge [Liter] |
| STAT_KRAFTSTOFFMENGE_EINH | string | Unit = Litre |
| STAT_ZEIT_INSP_ZAEHLER_WERT | int | Number of days since last service Zeitinspektionszaehler [Tage] |
| STAT_ZEIT_INSP_ZAEHLER_EINH | string | Unit = Days |
| STAT_SERVICE_ART | int | Type of last service ( 1=oil, 0=Inspection ) Gibt die letzte durchgefuehrte Serviceart an 0 = Inspektion, 1 = Oelservice |
| STAT_SERVICE_TEXT | string | Type of last service as text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-aif-datum-fz-lesen"></a>
### AIF_DATUM_FZ_LESEN

Read the Build Data from the User Information Auslesen Herstelldatum des FZ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATUM_FZ | string | Build date as a string Herstelldatum des FZ |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-aif-gwsz-lesen"></a>
### AIF_GWSZ_LESEN

Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen Read the Kilometers from the User Information Memory Block

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GWSZ_WERT | long | Gesamtwegstreckenzaehler Distance counter |
| STAT_GWSZ_EINH | string | Einheit des GWSZ [km] |
| _TEL_ANTWORT | binary | Antworttelegramm vom SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-gwsz-offset-lesen"></a>
### GWSZ_OFFSET_LESEN

OFFSET-Wert des GWSZ aus EEPROM lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| GWSZ_OFFSET_WERT | int | absoluter Offset-Wert des GWSZ (0-255) |

<a id="job-gwsz-minus-offset-lesen"></a>
### GWSZ_MINUS_OFFSET_LESEN

Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen und Offset abziehen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_GWSZ_MINUS_OFFSET_WERT | long | Gesamtwegstreckenzaehler minus Offset |
| STAT_GWSZ_EINH | string | Einheit des GWSZ [km] |

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

<a id="job-gwsz-reset"></a>
### GWSZ_RESET

GWSZ zuruecksetzen, nur moeglich wenn Km-Stand &lt; 255

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-aif-zentralcode-lesen"></a>
### AIF_ZENTRALCODE_LESEN

Anwenderinfofeld Block 4 auslesen Read the ZCS from the AIF record

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos + 1 ASCII c/sum) Centralcode C1 - Basic features |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos + 1 ASCII c/sum) Centralcode C2 - Particular equipment |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos + 1 ASCII c/sum) Centralcode C3 - Version information |
| STAT_ZENTRALCODE_ANLIEFERCODIERUNG | int | True falls der Zentralcode der Anliefercodierung entspricht 0 = Empty ZCS record, 1 = ZCS has been coded |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-zcs-lesen"></a>
### C_ZCS_LESEN

Anwenderinfofeld Block 4 auslesen Read the ZCS from the AIF record

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos + 1 ASCII c/sum) Basic features |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos + 1 ASCII c/sum) Particular equipment |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos + 1 ASCII c/sum) Version information |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-zcs-auftrag"></a>
### C_ZCS_AUFTRAG

Write and verify the Central code

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos + 1 ASCII c/sum) Basic features |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos + 1 ASCII c/sum) Particular equipment |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos + 1 ASCII c/sum) Version information |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write ZCS telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write ZCS response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read ZCS response |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-aif-fg-nr-lesen"></a>
### AIF_FG_NR_LESEN

Read the VIN from the User Information Auslesen der Fahrgestellnummer aus dem Anwenderinfofeld

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Vehicle identification Fahrgestellnummer |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read ident response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read user information response |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Read the VIN from the User Information Auslesen der Fahrgestellnummer aus dem Anwenderinfofeld

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Vehicle identification Fahrgestellnummer |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read ident response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read user information response |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Schreiben der 7-stelligen Fahrgestellnummer Write the 7 digit VIN into block 2 of the AIF record

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) VIN Either 17 or 18 characters - if 18 the last character is ignored |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write empty VIN response |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write new VIN telegram to ECU |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Write new VIN response |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG Read VIN response |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen Read the coding data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Byte 0:               01=Daten 02=Maskenbyte (nicht unterstuetzt) Byte 1:               Wortbreite (0:Byte, 2:Word, 3:DW Byte 2:               Byteordnung (0:LSB zuerst, 1 MSB Byte 3:               Adressierung (0: freie Adressier Byte 4:               Byteparameter 1 Byte 5,6:             WordParameter 1 (low/high) Byte 7,8:             WordParameter 2 (low/high) Byte 9,10,11,12:      Maske (linksbuendig) Byte 13,14:           Anzahl Bytedaten (low/high) Byte 15,16:           Anzahl Wortdaten (low/high) Byte 17:              Byteadresse im Block Byte 18,19,20:        Blockadresse (low, middle, high) Byte 21,....:         Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-codierblock-lesen"></a>
### CODIERBLOCK_LESEN

Codierblock auslesen Read the coding data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | int | Blockadresse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BLOCKINHALT | binary | Codierdaten des Blocks |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren Write and then verify the coding data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Byte 0:               01=Daten 02=Maskenbyte (nicht unterstuetzt) Byte 1:               Wortbreite (0:Byte, 2:Word, 3:DW Byte 2:               Byteordnung (0:LSB zuerst, 1 MSB Byte 3:               Adressierung (0: freie Adressier Byte 4:               Byteparameter 1 Byte 5,6:             WordParameter 1 (low/high) Byte 7,8:             WordParameter 2 (low/high) Byte 9,10,11,12:      Maske (linksbuendig) Byte 13,14:           Anzahl Bytedaten (low/high) Byte 15,16:           Anzahl Wortdaten (low/high) Byte 17:              Byteadresse im Block Byte 18,19,20:        Blockadresse (low, middle, high) Byte 21,....:         Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write coding data telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write coding data response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read coding data response |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ram-lesen"></a>
### RAM_LESEN

RAM-Speicher auslesen Read internal and external RAM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | ECU address in RAM Hexwert (0x000-0x3FFF) der Adresse, ab der das Ram gelesen werden soll |
| BYTE_ANZAHL | int | Number of bytes of data to read, 1 -&gt; 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Data read from RAM Datenfeld |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-rom-lesen"></a>
### ROM_LESEN

ROM-Speicher auslesen Read ROM out of IKE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | ECU address in ROM Hexwert (0x8000-0xFEFF) der Adresse, ab der das Rom gelesen werden soll |
| BYTE_ANZAHL | int | Number of bytes of data to read, 1 -&gt; 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Data read from ROM Datenfeld |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

EEPROM-Speicher auslesen Read EEPROM out of IKE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x0000-0xFFFF) der WortAdresse, ab der das EEPROM gelesen werden soll |
| BYTE_ANZAHL | int | Number of bytes of data to read, 1 -&gt; 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Datenfeld |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-pseudo-eeprom-lesen"></a>
### PSEUDO_EEPROM_LESEN

PSEUDO-EEPROM-Speicher auslesen Read EEPROM out of IKE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x0000-0xFFFF) der WortAdresse, ab der das Pseudo- EEPROM gelesen werden soll |
| BYTE_ANZAHL | int | Number of bytes of data to read, 1 -&gt; 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Datenfeld |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-power"></a>
### STATUS_IO_POWER

Read Power digital inputs from Port 0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_KLR_ON | int | 1 wenn ein / 0 wenn aus 1=Ignition switch at AUX, 0=ignition switch not at AUX |
| STAT_KLR_15_ON | int | 1 wenn ein / 0 wenn aus 1=Ignition switch at IGN, 0=ignition switch not at IGN |
| STAT_KLR_50_ON | int | 1 wenn ein / 0 wenn aus 1=Ignition switch not at CRANK, 0=Ignition switch at CRANK |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-trip-reset"></a>
### STATUS_IO_TRIP_RESET

Read Trip Reset digital input from Port 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_TRIP_RESET_PRESSED | int | 1 wenn einschalten / 0 wenn ausschalten 1=SIA reset switch pressed, 0=not pressed |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-dimmer-sw"></a>
### STATUS_IO_DIMMER_SW

Read dimmer switch digital inputs from Port 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_DIMMER_1_PRESSED | int | 1 wenn einschalten / 0 wenn ausschalten 1=pressed 0=not pressed |
| STAT_DIMMER_2_PRESSED | int | 1 wenn einschalten / 0 wenn ausschalten 1=pressed 0=not pressed |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-misc"></a>
### STATUS_IO_MISC

Read miscellaneous digital inputs from Port 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_PDC_INPUT_ON | int | 1=ON, 0=OFF |
| STAT_LOW_OIL_INPUT_ON | int | 1=Oel druck niedrig, 0=Oel druck nicht niedrig 1=ON, 0=OFF |
| STAT_TRIP_COMPUTER_INPUT_ON | int | 1 wenn einschalten / 0 wenn ausschalten 1=ON, 0=OFF |
| STAT_LOW_BRAKE_FLUID_INPUT_ON | int | 1=Bremsfluessigkeit niedrig, 0=Bremsfluessigkeit nicht niedrig 1=ON, 0=OFF |
| STAT_ALTERNATOR_CHARGE_INPUT_ON | int | 1=ON, 0=OFF |
| STAT_REVERSE_GEAR_INPUT_ON | int | 1=Rueckwaertsgang activ, 0=nicht activ 1=ON, 0=OFF |
| STAT_SEAT_BELT_INPUT_ON | int | 1=ein, 0=aus 1=on, 0=off |
| STAT_HAND_BRAKE_INPUT_ON | int | 1 wenn Handbremse ein / 0 wenn Handbremse aus 1=on, 0=off |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-hazard-sw"></a>
### STATUS_IO_HAZARD_SW

Read hazard switch digital input from Port 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_HAZARD_SWITCH_PRESSED | int | 1 wenn einschalten / 0 wenn ausschalten 1=pressed, 0=not pressed |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-wake-up"></a>
### STATUS_IO_WAKE_UP

Read 10 minute wake up status from port 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_10_MIN_TIMER_CHARGED | int | 1 wenn laden / 0 wenn nicht laden 1=timer capacitor charged, 0=not charged |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-lcd-backlight"></a>
### STATUS_IO_LCD_BACKLIGHT

Read LCD Backlight input from port 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LCD_BACKLIGHT_ON | int | 1 wenn ein / 0 wenn aus 1=on, 0=off |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-can-shutdown"></a>
### STATUS_IO_CAN_SHUTDOWN

Read status of CAN shutdown output from port 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_SHUTDOWN_OUTPUT_HIGH | int | 1 wenn ein / 0 wenn aus 1=CAN shutdown output high, 0=CAN shutdown output low |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-kbus-interrupt"></a>
### STATUS_IO_KBUS_INTERRUPT

Read status of Kbus interrupt from port 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_KBUS_INTERRUPT_ON | int | 1 wenn ein / 0 wenn aus 1=on, 0=off |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-dimmer-driver"></a>
### STATUS_IO_DIMMER_DRIVER

Read dimmer driver digital input from Port 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_DIMMER_ACTIVE | int | 1=active (over heat / sc load / ac load), 0=not active |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-led-dig-inputs"></a>
### STATUS_IO_LED_DIG_INPUTS

Read LED 19, LED 20 and LED A9 digital inputs from Port 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_TACHO_RED_LINE_LED_19_ON | int | 1 wenn ein / 0 wenn aus 1=on, 0=off |
| STAT_TACHO_RED_LINE_LED_20_ON | int | 1 wenn ein / 0 wenn aus 1=on, 0=off |
| STAT_SPARE_LED_A9_ON | int | 1 wenn ein / 0 wenn aus 1=on, 0=off |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-motor-drivers"></a>
### STATUS_IO_MOTOR_DRIVERS

Read status of the motor drivers from port 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_MOTOR_DRIVERS_RESET_ON | int | 1 wenn ein / 0 wenn aus 1=on, 0=off |
| STAT_MOTOR_DRIVERS_ERROR_ON | int | 1 wenn ein / 0 wenn aus 1=Error generated by stepper motor drivers, 0=no error |
| STAT_CENTRE_GAUGE_MOTOR_SELECTED | int | 1 wenn ein / 0 wenn aus 1=Centre gauge motor selected, 0=not selected |
| STAT_TEMP_AND_FUEL_MOTORS_SELECTED | int | 1 wenn ein / 0 wenn aus 1=temp or fuel motors selected, 0=not selected |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-read-digital"></a>
### READ_DIGITAL

Read all Digital Inputs for a specified port

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PORT | int | Port of the micro controller in the instrument pack ECU 1 -&gt; 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BYTE | unsigned char | Raw byte value for this port |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Read Analogue Input States

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FUEL_SENDER_1_WERT | real | Fuel sender tank 1 |
| STAT_FUEL_SENDER_1_EINH | string | Output in Ohm |
| STAT_FUEL_SENDER_2_WERT | real | Fuel sender tank 2 |
| STAT_FUEL_SENDER_2_EINH | string | Output in Ohm |
| STAT_AD0_FUEL_SENDER_2_WERT | real | Fuel sender tank 2 |
| STAT_AD0_FUEL_SENDER_2_EINH | string |  |
| STAT_AD1_FUEL_SENDER_1_WERT | real | Fuel sender tank 1 |
| STAT_AD1_FUEL_SENDER_1_EINH | string |  |
| STAT_AMBIENT_TEMP_RESISTANCE_WERT | real | Resistance for ambient temperature sensor |
| STAT_AMBIENT_TEMP_RESISTANCE_EINH | string | Output in Ohm |
| STAT_AD2_AMBIENT_TEMP_WERT | real | Ambient temperature (raw ADC value) |
| STAT_AD2_AMBIENT_TEMP_EINH | string |  |
| STAT_AMBIENT_TEMP_WERT | real | Ambient temperature (calculated value) |
| STAT_AMBIENT_TEMP_EINH | string | Celsius |
| STAT_AD3_AMBIENT_LIGHT_LEVEL_WERT | real | Ambient light level |
| STAT_AD3_AMBIENT_LIGHT_LEVEL_EINH | string |  |
| STAT_AD4_WERT | real | AD Channel 4 |
| STAT_AD4_EINH | string |  |
| STAT_AD5_BATTERY_VOLTS_WERT | real | Battery Voltage |
| STAT_AD5_BATTERY_VOLTS_EINH | string |  |
| STAT_AD6_WERT | real | AD Channel 6 |
| STAT_AD6_EINH | string |  |
| STAT_AD7_WERT | real | AD Channel 7 |
| STAT_AD7_EINH | string |  |
| STAT_BOOST_PRESSURE_CAN_WERT | real | Boost pressure |
| STAT_BOOST_PRESSURE_CAN_EINH | string |  |
| STAT_ROAD_SPEED_CAN_WERT | real | Vehicle speed |
| STAT_ROAD_SPEED_CAN_EINH | string |  |
| STAT_TACHO_CAN_WERT | real | Engine speed |
| STAT_TACHO_CAN_EINH | string |  |
| STAT_FUEL_CONSUMPTION_CAN_WERT | real | Fuel consumption |
| STAT_FUEL_CONSUMPTION_CAN_EINH | string |  |
| STAT_ENGINE_TEMP_CAN_WERT | real | Engine temperature |
| STAT_ENGINE_TEMP_CAN_EINH | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-tankinhalt-lesen"></a>
### STATUS_TANKINHALT_LESEN

Tankinhalt lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_TANKINHALT_HEBEL1_WERT | real | Tankinhalt Hebelgeber1 in Liter |
| STAT_TANKINHALT_HEBEL2_WERT | real | Tankinhalt Hebelgeber2 in Liter |
| STAT_TANKINHALT_WERT | real | Tankinhalt gesamt in Liter |
| STAT_TANKINHALT_HEBEL1_EINH | string | Einheit Tankinhalt: "Liter" |
| STAT_TANKINHALT_HEBEL2_EINH | string | Einheit Tankinhalt: "Liter" |
| STAT_TANKINHALT_EINH | string | Einheit Tankinhalt gesamt: "Liter" |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-aussentemp-lesen"></a>
### STATUS_AUSSENTEMP_LESEN

Read Temprature

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_AUSSENTEMP_SENSOR_WERT | real | Temp. Value |
| STAT_AUSSENTEMP_SENSOR_EINH | string | Temp. Unit in: "Grad Celsius" |
| ANTWORT | binary |  |

<a id="job-steuern-leuchte"></a>
### STEUERN_LEUCHTE

Force the warning lamps in byte blocks

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Bit0 = Spare Bit1 = EPAS warning lamp Bit2 = Engine Coolant Temp Warning Lamp Bit3 = Battery Charge Warning Lamp Bit4 = ABS Warning Lamp Bit5 = Low Fuel Warning Lamp Bit6 = Hazard Warning Lamp Bit7 = Saudi Overspeed Warning Lamp (KMH Packs Only) |
| BYTE1 | int | Bit0 = Deflation Warning System Lamp Bit1 = Seat Belt Warning Lamp Bit2 = SRS Warning Lamp Bit3 = Drive By Wire Warning Lamp Bit4 = Cruise Control Active Lamp Bit5 = Rear Facing Infant Seat Indicator Bit6 = Traction Control Warning Lamp Bit7 = Red Line 1 |
| BYTE2 | int | Bit0 = Red Line 2 Bit1 = Red Line 3 Bit2 = Red Line 4 Bit3 = Red Line 5 Bit4 = Main Beam (twin) Bit5 = Oil Pressure (twin) Bit6 = OBD (MIL) (twin) Bit7 = Brake System (twin) |
| BYTE3 | int | Bit0 = Bonnet + Boot Open (twin) Bit1 = Directional Indicators (twin) Bit2 = Cruise Control Active Lamp (twin) or Main Beam (single) Bit3 = Drive By Wire Warning Lamp (twin) or Oil Pressure (single) Bit4 = Saudi Overspeed Warning Lamp (twin) or OBD (MIL) (single) Bit5 = Engine Coolant Temp Warning Lamp (twin) or Brake System (single) Bit6 = ABS Warning Lamp (twin) or Bonnet + Boot Open (single) Bit7 = Battery Charge Warning Lamp (twin) or Directional Indicators (single) |
| BYTE4 | int | Bit0 = Red Line 1 Lamp Bit1 = Red Line 2 Lamp Bit2 = Red Line 3 Lamp Bit3 = Red Line 4 Lamp Bit4 = Red Line 5 Lamp Bit5 = Traction Control Warning Lamp Bit6 = EPAS Warning Lamp Bit7 = Deflation Warning System Lamp |
| BYTE5 | int | Bit0 = Spare Bit1 = Spare Bit2 = Spare Bit3 = Seat Belt Bit4 = SRS Bit5 = Rear Facing Infant Seat Indicator Bit6 = Spare Bit7 = Low Fuel Warning |
| BYTE6 | int | Bit0 = Fuel level indicator Bit1 = Fuel level indicator Bit2 = Fuel level indicator Bit3 = Fuel level indicator Bit4 = Fuel level indicator Bit5 = Fuel level indicator Bit6 = Fuel level indicator Bit7 = Spare |
| BYTE7 | int | Bit0 = Spare Bit1 = Spare Bit2 = Spare Bit3 = Spare Bit4 = not used Bit5 = not used Bit6 = not used Bit7 = not used |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-anzeige"></a>
### STEUERN_ANZEIGE

Force an instrument gauge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Instrument gauge to force TACHO, DREHZAHL, TANKINHALT, TEMPERATUR Parameter "ORT" in table "Komponenten" |
| WERT | int | Forcing value for the gauge 0 -&gt; 100% full scale deflection |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-all-gauges"></a>
### STEUERN_ALL_GAUGES

Force all instrument gauges

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPEEDO | int | Steuern TACHO Force the speedometer (0 - 100% full scale deflection) |
| TACHO | int | Steuern DREHZAHL Force the tachometer (0 - 100% fsd) |
| FUEL_GAUGE | int | Steuern TANKINHALT Force the fuel gauge (0 - 100% fsd) |
| TEMP_GAUGE | int | Steuern TEMPERATUR Force the temperature gauge (0 - 100% fsd) |
| BOOST_GAUGE | int | Steuern BOOST Force the boost pressure gauge (0 - 100% fsd) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-panel-light"></a>
### STEUERN_PANEL_LIGHT

Force the Panel Illumination

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LIGHT_LEVEL | int | Illumination level (0 -&gt; 100 percent) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet table JobResult STATUS_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-backlight"></a>
### STEUERN_BACKLIGHT

Force the Odometer and trip computer backlight

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LIGHT_LEVEL | int | light level (0 - 100 percent) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-gong"></a>
### STEUERN_GONG

Force the gong

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | Forcing mode of gong 0=No sound, 1=Single high note, 2=Single low note, 3=Tic Toc |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-lcd-odo"></a>
### STEUERN_LCD_ODO

Force the LCD Odometer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEST_MAP | int | Which test map to use (0x00 - 0x03) 0 = All on 1 = All off 2 = Pattern 2 3 = Pattern 3 |
| TEST_SEGMENT | int | Test segment (0x00 -&gt; 0x08) Segment 00 = (Blank) Segment 01 = 'k' Segment 02 = 'm' Segment 03 = 'iles' Segment 04 = 'Inspection' Segment 05 = 'Oil Service' Segment 06 = (Clock Face) Segment 07 = (Blank) Segment 08 = '.' Segments 0x09 - 0xFF = Not Used |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-lcd-trip"></a>
### STEUERN_LCD_TRIP

Force the LCD trip computer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEST_MAP | int | Which test map to use (0x00 - 0x03) 0 = All on 1 = All off 2 = Pattern 2 3 = Pattern 3 |
| TEST_SEGMENT | int | Test segment (0x00 - 0x11) Segment 00 = 'Range' Segment 01 = 'trip 2' Segment 02 = 'Speed' Segment 03 = 'timer' Segment 04 = ' C' - Deg C (Grad C) Segment 05 = ' F' - Deg F (Grad F) Segment 06 = 'S' Segment 07 = 'mph' Segment 08 = 'km' Segment 09 = 'miles' Segment 0A = 'k/h' Segment 0B = 'm' Segment 0C = 'mpg' Segment 0D = 'km/' Segment 0E = 'L' Segment 0F = 'Temp' Segment 10 = 'Ave.S' Segment 11 = 'Cons' Segment 12 = '.' Segment 13 = '/100K' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Perform ECU Self Test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-sia-reset"></a>
### SIA_RESET

Force an SIA reset

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | moegliche Uebergabeparameter: OEL_RESET, WEG_RESET, ZEIT_RESET parameter "SELECTOR" from table "SiaReset" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-zeitinspektionszaehler-lesen"></a>
### ZEITINSPEKTIONSZAEHLER_LESEN

Zeitinspektionszaehler auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ZAEHLER_WERT | int | Number of days since last service Zeitinspektionszaehler [Tage] |
| ZAEHLER_EINH | string | Unit = Days |
| SERVICE_ART | int | Type of last service ( 1=oil, 0=Inspection ) Gibt die letzte durchgefuehrte Serviceart an 0 = Inspektion, 1 = Oelservice |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Read the Test Stamp Default pruefstempel_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Pruefstempel Datenbyte1 |
| BYTE2 | int | Pruefstempel Datenbyte2 |
| BYTE3 | int | Pruefstempel Datenbyte3 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Read the Test Stamp Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden (0x00-0xFF) |
| BYTE2 | int | kann beliebig verwendet werden (0x00-0xFF) |
| BYTE3 | int | kann beliebig verwendet werden (0x00-0xFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-software-reset"></a>
### SOFTWARE_RESET

Instrument cluster will reset itself Kombi loest selbststaendig einen Reset aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

Send the ECU into sleep mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

ECU Pinging message

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden Terminate the diagnostic session

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (6 × 2)
- [LIEFERANTEN](#table-lieferanten) (47 × 2)
- [DIGITAL](#table-digital) (28 × 4)
- [ANALOG](#table-analog) (14 × 4)
- [LEDDATA](#table-leddata) (29 × 3)
- [ROVERPARTPREFIX](#table-roverpartprefix) (22 × 2)
- [SIARESET](#table-siareset) (4 × 3)
- [KOMPONENTEN](#table-komponenten) (6 × 3)
- [FORTTEXTE](#table-forttexte) (22 × 2)
- [FARTTEXTE](#table-farttexte) (8 × 2)
- [SUPPLIERDATA](#table-supplierdata) (2 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 6 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

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

<a id="table-digital"></a>
### DIGITAL

Dimensions: 28 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| KLR | 3 | 0x01 | 0x01 |
| KLR_15 | 3 | 0x02 | 0x02 |
| KLR_50 | 3 | 0x04 | 0x04 |
| TRIP_RESET | 3 | 0x08 | 0x08 |
| DIMMER_1 | 3 | 0x04 | 0x04 |
| DIMMER_2 | 3 | 0x08 | 0x08 |
| PDC_INPUT | 3 | 0x01 | 0x01 |
| LOW_OIL_INPUT | 3 | 0x02 | 0x02 |
| TRIP_COMPUTER_INPUT | 3 | 0x04 | 0x04 |
| LOW_BRAKE_FLUID_INPUT | 3 | 0x08 | 0x08 |
| ALTERNATOR_CHARGE_INPUT | 3 | 0x10 | 0x10 |
| REVERSE_GEAR_INPUT | 3 | 0x20 | 0x20 |
| SEAT_BELT | 3 | 0x40 | 0x40 |
| HAND_BRAKE_INPUT | 3 | 0x80 | 0x80 |
| HAZARD_SWITCH | 3 | 0x01 | 0x01 |
| DIMMER | 3 | 0x04 | 0x04 |
| SPARE_LED_A9 | 3 | 0x20 | 0x20 |
| TACHO_RED_LINE_LED_19 | 3 | 0x40 | 0x40 |
| TACHO_RED_LINE_LED_20 | 3 | 0x80 | 0x80 |
| MOTOR_DRIVERS_RESET | 3 | 0x02 | 0x02 |
| MOTOR_DRIVERS_ERROR | 3 | 0x20 | 0x20 |
| CENTRE_GAUGE_MOTOR | 3 | 0x40 | 0x40 |
| TEMP_AND_FUEL_MOTORS | 3 | 0x80 | 0x80 |
| 10_MIN_TIMER | 3 | 0x01 | 0x01 |
| LCD_BACKLIGHT | 3 | 0x08 | 0x08 |
| CAN_SHUTDOWN_OUTPUT | 3 | 0x80 | 0x80 |
| KBUS_INTERRUPT | 3 | 0x10 | 0x10 |
| ?? | FF | 0x00 | 0xFF |

<a id="table-analog"></a>
### ANALOG

Dimensions: 14 rows × 4 columns

| NAME | FACT_A | FACT_B | EINH |
| --- | --- | --- | --- |
| AD1_FUEL_SENDER_1 | 1.0 | 0.0 |  |
| AD0_FUEL_SENDER_2 | 1.0 | 0.0 |  |
| AD2_AMBIENT_TEMP | 1.0 | 0.0 |  |
| AD3_AMBIENT_LIGHT_LEVEL | 1.0 | 0.0 |  |
| AD4 | 1.0 | 0.0 |  |
| AD5_BATTERY_VOLTS | 0.019698 | 0.93 | Volts |
| AD6 | 1.0 | 0.0 |  |
| AD7 | 1.0 | 0.0 |  |
| BOOST_PRESSURE_CAN | 1.0 | -100.0 | kPa |
| ROAD_SPEED_CAN | 0.0625 | 0.0 | km/h |
| TACHO_CAN | 0.15625 | 0.0 | Umdrehunge pro Minute |
| FUEL_CONSUMPTION_CAN | 1.0 | 0.0 | Mikroliter |
| ENGINE_TEMP_CAN | 0.75 | -48.0 | Grad C |
| Unknown item | 0.0 | 0 |  |

<a id="table-leddata"></a>
### LEDDATA

Dimensions: 29 rows × 3 columns

| NAME | BYTE | VALUE |
| --- | --- | --- |
| HIGH_COOLANT_TEMP | 0 | 0x04 |
| BATTERY_CHARGE | 0 | 0x08 |
| LOW_OIL_PRESSURE | 0 | 0x10 |
| LOW_FUEL | 0 | 0x20 |
| HAZARD | 0 | 0x40 |
| MAIN_BEAM | 0 | 0x80 |
| BONNET | 1 | 0x01 |
| ABS | 1 | 0x02 |
| BRAKE_SYSTEM | 1 | 0x04 |
| DRIVE_BY_WIRE | 1 | 0x08 |
| MIL | 1 | 0x10 |
| DI | 1 | 0x20 |
| SEAT_BELT | 1 | 0x40 |
| RED_LINE_3 | 2 | 0x01 |
| RED_LINE_1 | 2 | 0x02 |
| RED_LINE_4 | 2 | 0x04 |
| CAN_CRUISE_ACTIVE | 3 | 0x01 |
| CAN_TRACTION_CONTROL | 3 | 0x02 |
| CAN_SEAT_BELT | 3 | 0x04 |
| CAN_SAUDI_OVERSPEED | 3 | 0x08 |
| CAN_DRIVE_BY_WIRE | 3 | 0x10 |
| CAN_MIL | 3 | 0x20 |
| CAN_MAIN_BEAM | 3 | 0x40 |
| CAN_ABS | 3 | 0x80 |
| CAN_BREAK_SYSTEM | 4 | 0x01 |
| CAN_BONNET | 4 | 0x02 |
| CAN_DI | 4 | 0x04 |
| CAN_TIRE_DEFLATION | 4 | 0x08 |
| Unknown item | 0 | 0x00 |

<a id="table-roverpartprefix"></a>
### ROVERPARTPREFIX

Dimensions: 22 rows × 2 columns

| CODE | PREFIX |
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
| 0xB6 | YUW |
| 0xFF | ??? |

<a id="table-siareset"></a>
### SIARESET

Dimensions: 4 rows × 3 columns

| SELECTOR | RESET | TEXT |
| --- | --- | --- |
| OEL_RESET | 0x01 | Oel Service Reset |
| WEG_RESET | 0x02 | Inspektion Reset |
| ZEIT_RESET | 0x04 | Zeit Service Reset |
|  | 0x00 |  |

<a id="table-komponenten"></a>
### KOMPONENTEN

Dimensions: 6 rows × 3 columns

| ORT | BYTE | TEXT |
| --- | --- | --- |
| TACHO | 0x0A | Tachometer |
| DREHZAHL | 0x0B | Tachometer |
| TANKINHALT | 0x0C | Tankuhr |
| TEMPERATUR | 0x0D | Temperaturmesser |
| BOOST | 0x0E | Ladedruckmesser |
| unbekannt | 0xFF |  |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 22 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x87 | K-Bus Kurzschluss gegen Masse oder Batteriespannung |
| 0x8F | Batteriespannung &gt; 16V - Fehler in Lichtmaschine |
| 0xC7 | Ölsender Eingang input Kurzschluss gegen Masse oder Batteriespannung |
| 0xCE | Aussentmperatur Sensor Kurzschluss zu Masse oder Batteriespannung |
| 0x8C | KL.R unplausible Bedingung |
| 0xCF | SIA Reset Fehler - DS2 PIN Kurschluss gegen Masse länger als 1 Minute |
| 0xBE | LM-EEPROM-Fehler |
| 0xBF | EEPROM Checksum Fehler |
| 0xC1 | TWEG + (Tacho) - Motordrehzahl oberhalb 3000 Umdrehungen für 10 Minuten ohne zurückgelegtem Weg |
| 0xC3 | TD - Fuel used but engine speed is 0 for longer than 1 second |
| 0x8D | Notprogramm - Getriebe SG hat Getriebe falsches Flag gesendet |
| 0xF0 | CAN: Bus Off - CAN HI Kurschluss gegen Masse, CAN Low gegen Batteriespannung oder CAN HI gegen CAN LO |
| 0xF4 | CAN: Keine ID - Kein CAN- Signal für 1500ms und bus ist nicht ausgeschaltet |
| 0xF5 | CAN: Kein ASC1 - Keine ABS- Meldung für 1500ms |
| 0xF6 | CAN: Keine DME1 - Kein Telegramm erhalten 1 von EMS for 1500ms |
| 0xF7 | CAN: Keine DME2 - Kein Telegramm erhalten 2 von EMS for 1500ms |
| 0xF8 | CAN: Keine DME4 - Kein Telegramm erhalten 4 von EMS for 1500ms |
| 0xFD | CAN: Keine DME5 - Kein Telegramm erhalten 5 von EMS for 1500ms |
| 0xFB | CAN: Kein EGS1 - Kein Telegramm erhalten von ATCU für 1500ms |
| 0xFC | CAN: Kein RIP1 - Kein Telegramm erhalten von 'Remote Instrument Pack (RIP) |
| 0xFF | Unbekannter Fehler |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 8 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen Batterie |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | Unplausibler Wert, ungueltiger Arbeitsbereich |
| 0x07 | Fehler momentan vorhanden |
| 0x08 | Älterer Fehler |
| 0xFF | Unbekannter Status |

<a id="table-supplierdata"></a>
### SUPPLIERDATA

Dimensions: 2 rows × 2 columns

| INDEX | INFO |
| --- | --- |
| 0x00 | Zusätliche Software Identifikation |
| 0x01 | Elektronik / PCB Index |
