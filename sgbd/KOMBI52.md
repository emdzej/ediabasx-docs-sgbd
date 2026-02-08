# KOMBI52.prg

- Jobs: [42](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | KOMBI E52 |
| ORIGIN | BMW TI-431 Dennert |
| REVISION | 2.10 |
| AUTHOR | BMW TI-44 Zender, BMW TI-431 Dennert |
| COMMENT | N/A |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [IDENT](#job-ident) - Default ident job
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicherinhalt aus SG lesen
- [SIA_RESET](#job-sia-reset) - Ruecksetzen der Service-Intervall-Anzeige
- [GWSZ_RESET](#job-gwsz-reset)
- [STATUS_IO_LESEN](#job-status-io-lesen) - Eingangs- und Ausgangsstati lesen
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - SG - Selbsttest ausloesen
- [STEUERN_ANZEIGE](#job-steuern-anzeige) - Anzeigenkomponenten steuern
- [STEUERN_TACHO_A](#job-steuern-tacho-a) - TACHO_A steuern
- [STEUERN_GONG3](#job-steuern-gong3) - Anzeigenkomponenten steuern
- [STEUERN_LC_DISPLAY](#job-steuern-lc-display) - Steuern LC-Display
- [STEUERN_LEUCHTE](#job-steuern-leuchte) - Leuchten in der Anzeigeeinheit steuern
- [STEUERN_LICHTSUMMER](#job-steuern-lichtsummer) - Anzeigenkomponenten steuern
- [RAM_LESEN](#job-ram-lesen)
- [ROM_LESEN](#job-rom-lesen)
- [EEPROM_LESEN](#job-eeprom-lesen)
- [DPRAM_LESEN](#job-dpram-lesen)
- [AIF_GWSZ_LESEN](#job-aif-gwsz-lesen) - Gesamtwegstreckenzaehlers aus Anwenderinfofeld auslesen
- [GWSZ_MINUS_OFFSET_LESEN](#job-gwsz-minus-offset-lesen) - Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen und Offset abziehen
- [AIF_FG_NR_LESEN](#job-aif-fg-nr-lesen) - Auslesen der Fahrgestellnummer
- [AIF_SIA_DATEN_LESEN](#job-aif-sia-daten-lesen) - Anwenderinfofeld Block 3 auslesen
- [AIF_ZENTRALCODE_LESEN](#job-aif-zentralcode-lesen) - Anwenderinfofeld Block 4 auslesen
- [AIF_DATUM_FZ_LESEN](#job-aif-datum-fz-lesen) - Auslesen des Herstelldatums des FZ
- [STATUS_CAN_MOTORDREHZAHL_LESEN](#job-status-can-motordrehzahl-lesen)
- [STATUS_CAN_KUEHLMITTELTEMP_LESEN](#job-status-can-kuehlmitteltemp-lesen)
- [STATUS_CAN_EINSPRITZMENGE_LESEN](#job-status-can-einspritzmenge-lesen)
- [STATUS_CAN_SIGNALE_LESEN](#job-status-can-signale-lesen)
- [PROD_DATUM_LESEN](#job-prod-datum-lesen)
- [STATUS_ANALOG_LESEN](#job-status-analog-lesen) - Spezielle Eingaenge lesen
- [STATUS_TANKINHALT_LESEN](#job-status-tankinhalt-lesen) - Tankinhalt lesen
- [STATUS_VERRIEGELUNGSBITS_GESETZT](#job-status-verriegelungsbits-gesetzt) - Verrieglungsbits gesetzt
- [STATUS_CAN_FUNKTION_LESEN](#job-status-can-funktion-lesen) - Zeigt an, ob CAN-Funktionalitaet vorhanden ist
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [SOFTWARE_RESET](#job-software-reset) - Kombi loest selbststaendig einen Reset aus
- [SIA_KORREKTUR_SCHREIBEN](#job-sia-korrektur-schreiben) - Toggeln der SIA Inspektions- bzw. Oelservices
- [C_ZCS_LESEN](#job-c-zcs-lesen) - Anwenderinfofeld Block 4 auslesen

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

<a id="job-ident"></a>
### IDENT

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
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
| F_ART8_NR | int | Fehlerart-Nr |
| F_ART8_TEXT | string | Fehlerart-Text |
| F_UW_ANZ | int | immer 0 |
| F_HEX_CODE | binary | Hexdaten des Fehlers |

<a id="job-sia-reset"></a>
### SIA_RESET

Ruecksetzen der Service-Intervall-Anzeige

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | moegliche Uebergabeparameter: Oel_Reset, Weg_Reset, Zeit_Reset |
| ARG2 | string | Oel/Weg oder Zeit - Reset |
| ARG3 | string | Oel/Wegs oder Zeit - Reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-gwsz-reset"></a>
### GWSZ_RESET

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Eingangs- und Ausgangsstati lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B ACK) |
| STAT_PARKBREMSE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_SIA_RESET_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KL50_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_GONGT3_EIN | int | 1, wenn "TRUE" , 0, wenn "FALSE" |
| STAT_LICHTWARNUNG_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KLR_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KL15_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KOMBITASTE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| TELEGRAMM | binary |  |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

SG - Selbsttest ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-steuern-anzeige"></a>
### STEUERN_ANZEIGE

Anzeigenkomponenten steuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Zu steuernde Komponente, siehe table Komponenten |
| WERT | int | Winkelgrade im Bereich von (10-90) Grad, Mit Spruengen von mehr als 90 Grad sollten die Messwerke nicht beaufschlagt werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| TELEGRAMM | binary |  |

<a id="job-steuern-tacho-a"></a>
### STEUERN_TACHO_A

TACHO_A steuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | int | Geschwindigkeit in km/h, Wertebereich (3 bis 250) km/h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| TELEGRAMM | binary |  |

<a id="job-steuern-gong3"></a>
### STEUERN_GONG3

Anzeigenkomponenten steuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| TELEGRAMM | binary |  |

<a id="job-steuern-lc-display"></a>
### STEUERN_LC_DISPLAY

Steuern LC-Display

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int |  |
| BYTE1 | int |  |
| BYTE2 | int |  |
| BYTE3 | int |  |
| BYTE4 | int |  |
| BYTE5 | int |  |
| BYTE6 | int |  |
| BYTE7 | int |  |
| BYTE8 | int |  |
| BYTE9 | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary |  |
| ANTWORT | binary |  |

<a id="job-steuern-leuchte"></a>
### STEUERN_LEUCHTE

Leuchten in der Anzeigeeinheit steuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| TELEGRAMM | binary |  |
| ANTWORT | binary |  |

<a id="job-steuern-lichtsummer"></a>
### STEUERN_LICHTSUMMER

Anzeigenkomponenten steuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| TELEGRAMM | binary |  |

<a id="job-ram-lesen"></a>
### RAM_LESEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAM_TYPE | string | "INTERN" oder "EXTERN" |
| ADRESSE | string | Hexwert (0x000) der Adresse ,ab der das Ram gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Bytes (max. 32 !) die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| DATEN | binary | Datenfeld |

<a id="job-rom-lesen"></a>
### ROM_LESEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x000) der Adresse ,ab der das Ram gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Bytes (max. 32 !) die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| DATEN | binary | Datenfeld |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x00) der Adresse ,ab der das EEPROM gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Worte (max. 16 !) die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| DATEN | binary | Datenfeld |

<a id="job-dpram-lesen"></a>
### DPRAM_LESEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x00) der Adresse ,ab der das DPRAM gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Bytes (max. 32 !) die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| DATEN | binary | Datenfeld |

<a id="job-aif-gwsz-lesen"></a>
### AIF_GWSZ_LESEN

Gesamtwegstreckenzaehlers aus Anwenderinfofeld auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_GWSZ_WERT | long | Gesamtwegstreckenzaehler |
| STAT_GWSZ_EINH | string | Einheit des GWSZ [km] |
| TELEGRAMM | binary |  |

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

<a id="job-aif-fg-nr-lesen"></a>
### AIF_FG_NR_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| AIF_FG_NR | string | Fahrgestellnummer |
| TELEGRAMM | binary |  |

<a id="job-aif-sia-daten-lesen"></a>
### AIF_SIA_DATEN_LESEN

Anwenderinfofeld Block 3 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| STAT_MOTORTYP_NR | int | 0 = Benzinmotor |
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
| STAT_SERVICE_ART | int | Art des letzten Service: 0 = Inspektion, 1 = Oelservice |
| STAT_SERVICE_TEXT | string | "Weginspektion", "Oelservice" |
| TELEGRAMM | binary |  |

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

<a id="job-status-can-motordrehzahl-lesen"></a>
### STATUS_CAN_MOTORDREHZAHL_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| STAT_MOTORDREHZAHL_WERT | long | Ausgabe der Motordrehzahl in U/min |
| STAT_MOTORDREHZAHL_EINH | string | Einheit [U/min] |
| TELEGRAMM | binary |  |

<a id="job-status-can-kuehlmitteltemp-lesen"></a>
### STATUS_CAN_KUEHLMITTELTEMP_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| STAT_KUEHLMITTELTEMP_WERT | long | Ausgabe der Kuehlmitteltemperatur in [Grad Celsius] |
| STAT_KUEHLMITTELTEMP_EINH | string | Einheit [Grad Celsius] |
| TELEGRAMM | binary |  |

<a id="job-status-can-einspritzmenge-lesen"></a>
### STATUS_CAN_EINSPRITZMENGE_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| STAT_EINSPRITZMENGE_WERT | long | Ausgabe der Einspritzmenge in [ul] |
| STAT_EINSPRITZMENGE_EINH | string | Einheit [ul] |
| TELEGRAMM | binary |  |

<a id="job-status-can-signale-lesen"></a>
### STATUS_CAN_SIGNALE_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| STAT_LAMPE_EBV_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LAMPE_ASC_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LAMPE_CHECK_ENGINE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_DDE_DIAGNOSELAMPE_EML_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LAMPE_UEBERTEMPERATUR_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_UMGEBUNGSTEMPERATUR_WERT | int | gemessene Aussentemperatur des Fahrzeugs in [Grad Celsius] |
| STAT_UMGEBUNGSTEMPERATUR_EINH | string | [Grad Celsius] |
| STAT_FZG_GESCHWINDIGKEIT_WERT | int | Geschwindigkeit des Fahrzeugs in [km/h] |
| STAT_FZG_GESCHWINDIGKEIT_EINH | string | [km/h] |
| STAT_DREHZAHLSTUFE_ELUEFTER_WERT | int | Drehzahl/Stufe des Elektro-Luefters |
| STAT_KILOMETERSTAND_WERT | long | gesamte Fahrleistung des Fahrzeugs in [km] |
| STAT_KILOMETERSTAND_EINH | string | [km] |
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

<a id="job-status-analog-lesen"></a>
### STATUS_ANALOG_LESEN

Spezielle Eingaenge lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| STAT_5V_WERT | int | AD - Kanal 0, 5V fixe Spannung |
| STAT_5V_EINH | string | Einheit [ADC-WERT] |
| STAT_HEBELGEBER1_WERT | int | AD - Kanal 1, Wert des 1. Hebelgebers |
| STAT_HEBELGEBER1_EINH | string | Einheit [ADC-WERT] |
| STAT_FOTOTRANSISTOR_WERT | int | AD - Kanal 3, Wert des Fototransistors |
| STAT_FOTOTRANSISTOR_EINH | string | Einheit [ADC-WERT] |
| STAT_KUEHLMITTELTEMP_WERT | int | AD - Kanal 5, Wert der Kuehlmittel`temperatur |
| STAT_KUEHLMITTELTEMP_EINH | string | Einheit [ADC-WERT] |
| STAT_BREMSVERSCHLEISS_WERT | int | Wert AD - Kanal 6, Wert des Bremsbelagverschleisses |
| STAT_BREMSVERSCHLEISS_EINH | string | Einheit [ADC-WERT] |
| STAT_AUSSENTEMP_WERT | int | Wert AD - Kanal 7, Wert der Aussen`temperatur |
| STAT_AUSSENTEMP_EINH | string | Einheit [ADC-WERT] |
| STAT_GESCHWINDIGKEIT_WERT | long | Wert des Wegeingangs, Wert der Geschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit [km/h] |
| TELEGRAMM | binary |  |

<a id="job-status-tankinhalt-lesen"></a>
### STATUS_TANKINHALT_LESEN

Tankinhalt lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| STAT_TANKINHALT_WERT | int | Tankinhalt in Liter |
| STAT_TANKINHALT_EINH | string | Einheit Tankinhalt |
| TELEGRAMM | binary |  |

<a id="job-status-verriegelungsbits-gesetzt"></a>
### STATUS_VERRIEGELUNGSBITS_GESETZT

Verrieglungsbits gesetzt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| STAT_VERRIEGELUNG_WERT | int |  |
| STAT_VERRIEGELUNG_TEXT | string | Verriegelungszustand im Klartext |

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

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-software-reset"></a>
### SOFTWARE_RESET

Kombi loest selbststaendig einen Reset aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-sia-korrektur-schreiben"></a>
### SIA_KORREKTUR_SCHREIBEN

Toggeln der SIA Inspektions- bzw. Oelservices

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-c-zcs-lesen"></a>
### C_ZCS_LESEN

Anwenderinfofeld Block 4 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| GM | string | C1 Zifferncode fuer Grundmerkmal |
| SA | string | C2 Zifferncode fuer Sonderausstattung |
| VN | string | C3 Zifferncode fuer Versionsnummer |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (72 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (24 × 2)
- [FARTTEXTE](#table-farttexte) (10 × 2)
- [SIARESET](#table-siareset) (3 × 2)
- [KOMPONENTEN](#table-komponenten) (5 × 2)
- [GETRIEBETYPEN](#table-getriebetypen) (2 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 13 rows × 2 columns

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
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 72 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen =&gt; Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe =&gt; Lear |
| 0x10 | VDO |
| 0x11 | Valeo |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine |
| 0x18 | Continental Teves |
| 0x19 | Elektromatik Suedafrika |
| 0x20 | Becker |
| 0x21 | Preh |
| 0x22 | Alps |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto |
| 0x26 | MotoMeter |
| 0x27 | Delphi PHI |
| 0x28 | DODUCO =&gt; BERU |
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
| 0x47 | ZF |
| 0x48 | GMPT |
| 0x49 | Harman Kardon |
| 0x50 | Remes |
| 0x51 | ZF Lenksysteme |
| 0x52 | Magneti Marelli |
| 0x53 | Borg Instruments |
| 0x54 | GETRAG |
| 0x55 | BHTC (Behr Hella Thermocontrol) |
| 0x56 | Siemens VDO Automotive |
| 0x57 | Visteon |
| 0x58 | Autoliv |
| 0x59 | Haberl |
| 0x60 | Magna Steyr |
| 0x61 | Marquardt |
| 0x62 | AB-Elektronik |
| 0x63 | Siemens VDO Borg |
| 0x64 | Hirschmann Electronics |
| 0x65 | Hoerbiger Electronics |
| 0x66 | Thyssen Krupp Automotive Mechatronics |
| 0x67 | Gentex GmbH |
| 0x68 | Atena GmbH |
| 0x69 | Magna-Donelly |
| 0x70 | Koyo Steering Europe |
| 0x71 | NSI B.V |
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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 24 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x3E | Messwerktreiberfehler |
| 0x3F | Messwerktreiber (latch up) |
| 0x83 | Tacho A |
| 0x87 | K-Bus |
| 0x8B | Gong_3 |
| 0x8C | Klemme R |
| 0x8F | Ueberspannung (U&gt;16V) |
| 0x90 | Klemme 15 |
| 0xBC | Bremsfluessigkeitsstand |
| 0xBD | EBV |
| 0xBE | Lichtmodul-EEPROM-Fehler |
| 0xBF | KOMBI-EEPROM-Fehler, Codierung fehlerhaft/unvollstaendig |
| 0xC1 | Signal TWEG+ (Tacho) |
| 0xC7 | Tank-Hebelgeber_1 |
| 0xCE | Aussentemperatur |
| 0xCF | SIA-Reset |
| 0xD3 | Kuehlmitteltemperatur |
| 0xF0 | CAN BUS OFF |
| 0xF4 | keine CAN ID |
| 0xF5 | keine CAN ID ASC1 |
| 0xF6 | keine CAN ID DME1 |
| 0xF7 | keine CAN ID DME2 |
| 0xF8 | keine CAN ID DME4 |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | ungueltiger Arbeitsbereich |
| 0x05 | Fehler durch externes Steuergeraet |
| 0x06 | unbekannte Fehlerart |
| 0x07 | Fehler momentan vorhanden |
| 0x08 | sporadischer Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-siareset"></a>
### SIARESET

Dimensions: 3 rows × 2 columns

| SELECTOR | RESET |
| --- | --- |
| OEL_RESET | 0x01 |
| WEG_RESET | 0x02 |
| ZEIT_RESET | 0x04 |

<a id="table-komponenten"></a>
### KOMPONENTEN

Dimensions: 5 rows × 2 columns

| ORT | BYTE |
| --- | --- |
| TACHO | 0x0A |
| DREHZAHL | 0x0B |
| TANKINHALT | 0x0C |
| KUEHLMITTELTEMPERATUR | 0x0D |
| FEHLER | 0xFF |

<a id="table-getriebetypen"></a>
### GETRIEBETYPEN

Dimensions: 2 rows × 2 columns

| GETRIEBEART | GETRIEBETEXT |
| --- | --- |
| 0x00 | Schaltgetriebe |
| 0xFF | unbekannte Getriebeinfo |
