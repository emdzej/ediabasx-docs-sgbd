# KOMBI39C.prg

- Jobs: [43](#jobs)
- Tables: [10](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | KOMBI E39C, E53 |
| ORIGIN | BMW TI-431 Dennert |
| REVISION | 2.19 |
| AUTHOR | BMW TP-422 Zender, BMW TI-431 Dennert, Siemens VDO Schneider |
| COMMENT | CAN-Funktionalitaet ist erst ab PU 98 gegeben |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer IKE
- [IDENT](#job-ident) - Default ident job
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Default pruefstempel_lesen job
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicherinhalt aus SG lesen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Fortsetzen der Diagnose
- [SELBSTTEST](#job-selbsttest) - SG - Selbsttest ausloesen
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - SG - Selbsttest ausloesen
- [SOFTWARE_RESET](#job-software-reset) - Kombi loest selbststaendig einen Reset aus
- [SIA_RESET](#job-sia-reset) - Ruecksetzen der Service-Intervall-Anzeige
- [GWSZ_RESET](#job-gwsz-reset)
- [AIF_GWSZ_LESEN](#job-aif-gwsz-lesen) - Gesamtwegstreckenzaehlers aus Anwenderinfofeld auslesen
- [GWSZ_MINUS_OFFSET_LESEN](#job-gwsz-minus-offset-lesen) - Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen und Offset abziehen
- [AIF_FG_NR_LESEN](#job-aif-fg-nr-lesen) - Auslesen der Fahrgestellnummer
- [AIF_SIA_DATEN_LESEN](#job-aif-sia-daten-lesen) - Anwenderinfofeld Block 3 auslesen
- [AIF_ZENTRALCODE_LESEN](#job-aif-zentralcode-lesen) - Anwenderinfofeld Block 4 auslesen
- [AIF_DATUM_FZ_LESEN](#job-aif-datum-fz-lesen) - Auslesen des Herstelldatums des FZ
- [PROD_DATUM_LESEN](#job-prod-datum-lesen)
- [STEUERN_ANZEIGE](#job-steuern-anzeige) - Anzeigenkomponenten steuern
- [STEUERN_TACHO_A](#job-steuern-tacho-a) - TACHO_A steuern
- [STEUERN_EISWARNUNG](#job-steuern-eiswarnung) - Anzeigenkomponenten steuern
- [STEUERN_LICHTSUMMER](#job-steuern-lichtsummer) - Anzeigenkomponenten steuern
- [STEUERN_GONG3](#job-steuern-gong3) - Anzeigenkomponenten steuern
- [STEUERN_LEUCHTE](#job-steuern-leuchte) - Leuchten in der Anzeigeeinheit steuern
- [STATUS_IO_LESEN](#job-status-io-lesen) - Eingangs- und Ausgangsstati lesen
- [STATUS_ANALOG_LESEN](#job-status-analog-lesen) - Spezielle Eingaenge lesen
- [STATUS_TANKINHALT_LESEN](#job-status-tankinhalt-lesen) - Tankinhalt lesen
- [RAM_LESEN](#job-ram-lesen)
- [EEPROM_LESEN](#job-eeprom-lesen)
- [DPRAM_LESEN](#job-dpram-lesen)
- [STATUS_CAN_MOTORDREHZAHL_LESEN](#job-status-can-motordrehzahl-lesen)
- [STATUS_CAN_KUEHLMITTELTEMP_LESEN](#job-status-can-kuehlmitteltemp-lesen)
- [STATUS_CAN_GETRIEBEINFO_LESEN](#job-status-can-getriebeinfo-lesen)
- [STATUS_CAN_EINSPRITZMENGE_LESEN](#job-status-can-einspritzmenge-lesen)
- [STATUS_CAN_SIGNALE_LESEN](#job-status-can-signale-lesen)
- [STATUS_CAN_FUNKTION_LESEN](#job-status-can-funktion-lesen) - Zeigt an, ob CAN-Funktionalitaet vorhanden ist
- [STATUS_SIA_FINISH](#job-status-sia-finish) - SIA-Daten auslesen zur Fertigungskontrolle
- [C_ZCS_LESEN](#job-c-zcs-lesen) - Anwenderinfofeld Block 4 auslesen
- [CLOCK_ADJUSTMENT_LESEN](#job-clock-adjustment-lesen) - Liest die Konstante zum Uhrenabgleich aus dem EEPROM

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

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x9B) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x9D) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer IKE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

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

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Default pruefstempel_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| BYTE1 | int |  |
| BYTE2 | int |  |
| BYTE3 | int |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

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
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicherinhalt aus SG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zum Fehlerort |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_ART2_NR | int |  |
| F_ART2_TEXT | string |  |
| F_ART3_NR | int |  |
| F_ART3_TEXT | string |  |
| F_ART4_NR | int |  |
| F_ART4_TEXT | string |  |
| F_ART5_NR | int |  |
| F_ART5_TEXT | string |  |
| F_ART6_NR | int |  |
| F_ART6_TEXT | string |  |
| F_ART7_NR | int |  |
| F_ART7_TEXT | string |  |
| F_UW_ANZ | int |  |
| F_HEX_CODE | binary | Hexdaten des Fehlers |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Fortsetzen der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-selbsttest"></a>
### SELBSTTEST

SG - Selbsttest ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

SG - Selbsttest ausloesen

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

<a id="job-sia-reset"></a>
### SIA_RESET

Ruecksetzen der Service-Intervall-Anzeige

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | Oel/Weg oder Zeit - Reset |
| ARG2 | string | Oel/Weg oder Zeit - Reset |
| ARG3 | string | Oel/Weg oder Zeit - Reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK od. ERROR_PARAMETER |

<a id="job-gwsz-reset"></a>
### GWSZ_RESET

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |

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
| WERT | int | Geschwindigkeit in km/h, Wertebereich (3 bis 300) km/h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| TELEGRAMM | binary |  |

<a id="job-steuern-eiswarnung"></a>
### STEUERN_EISWARNUNG

Anzeigenkomponenten steuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| TELEGRAMM | binary |  |

<a id="job-steuern-lichtsummer"></a>
### STEUERN_LICHTSUMMER

Anzeigenkomponenten steuern

_No arguments._

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

<a id="job-steuern-leuchte"></a>
### STEUERN_LEUCHTE

Leuchten in der Anzeigeeinheit steuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| BYTE4 | int | kann beliebig verwendet werden |
| BYTE5 | int | kann beliebig verwendet werden |
| BYTE6 | int | kann beliebig verwendet werden |
| BYTE7 | int | kann beliebig verwendet werden |
| BYTE8 | int | kann beliebig verwendet werden |
| BYTE9 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| TELEGRAMM | binary |  |
| ANTWORT | binary |  |

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
| STAT_EISWARNUNG_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LICHTWARNUNG_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KLR_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KL15_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_AGS_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KOMBITASTE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LSS_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| TELEGRAMM | binary |  |

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
| STAT_HEBELGEBER2_WERT | int | AD - Kanal 2, Wert des 2. Hebelgebers |
| STAT_HEBELGEBER2_EINH | string | Einheit [ADC-WERT] |
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
| STAT_DREHZAHL_WERT | long | Wert des Drehzahleingangs als string |
| STAT_DREHZAHL_EINH | string | Einheit [U/min] |
| STAT_TKVA1_WERT | long | Wert des Verbrauchssignal 1 |
| STAT_TKVA1_EINH | string | Einheit [ms] |
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

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x00) der Adresse ,ab der das EEPROM gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Bytes (max. 32 !) die ausgelesen werden sollen |

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

<a id="job-status-can-getriebeinfo-lesen"></a>
### STATUS_CAN_GETRIEBEINFO_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| STAT_GANG_INFO_WERT | int | gibt an in welchem Gang sich zur Zeit das Getriebe befindet |
| STAT_GANG_INFO_TEXT | string | gibt an in welchem Gang sich zur Zeit das Getriebe befindet |
| STAT_GANG_WHL_ANZ_WERT | int | gibt Waehlhebelposition an: 1,2,3,4,D,N,R,P,5,6,Zwischenstellung |
| STAT_GANG_WHL_ANZ_TEXT | string | gibt Waehlhebelposition an: 1,2,3,4,D,N,R,P,5,6,Zwischenstellung |
| STAT_PRG_INF_ANZ_WERT | int | gibt Programminfo aus: E,M,S,W,A,Anzeige aus |
| STAT_PRG_INF_ANZ_TEXT | string | gibt Programminfo aus: E,M,S,W,A,Anzeige aus |
| STAT_L_GETR_STEUERUNG_WERT | int | gibt Zustand der Getriebesteuerung an: Getriebenotprogramm ein |
| STAT_L_GETR_STEUERUNG_TEXT | string | gibt Zustand der Getriebesteuerung an: Getriebenotprogramm ein |
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
| STAT_VORGLUEHLAMPE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LAMPE_CHECK_ENGINE_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LAMPE_TEMPOMAT_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
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

<a id="job-status-sia-finish"></a>
### STATUS_SIA_FINISH

SIA-Daten auslesen zur Fertigungskontrolle

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_LITER_WERT | int | Verbrauchte Benzinmenge |
| STAT_LITER_EINH | string | Einheit der verbrauchten Benzinmenge |
| STAT_TAGES_WERT | int | Zeit seit letztem Zeitreset |
| STAT_TAGES_EINH | string | Einheit des Wertes vom letzten Zeitreset |
| STAT_BITSTATUS_0x15 | int | Bitstatus oberstes Bit Adresse 0x0F |
| SIA_SPEICHER_CHECK | string | Gesamtergebnis des Speicherchecks |

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

<a id="job-clock-adjustment-lesen"></a>
### CLOCK_ADJUSTMENT_LESEN

Liest die Konstante zum Uhrenabgleich aus dem EEPROM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| CLOCK_ADJUSTMENT | int | Datenfeld |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [SIARESET](#table-siareset) (3 × 2)
- [FORTTEXTE](#table-forttexte) (31 × 2)
- [FARTTEXTE](#table-farttexte) (9 × 2)
- [LIEFERANTEN](#table-lieferanten) (30 × 2)
- [GETRIEBETYPEN](#table-getriebetypen) (4 × 2)
- [GANGINFO](#table-ganginfo) (9 × 2)
- [WAEHLHEBELINFO](#table-waehlhebelinfo) (12 × 2)
- [PROGRAMMINFO](#table-programminfo) (7 × 2)
- [KOMPONENTEN](#table-komponenten) (6 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0x02 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

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

Dimensions: 31 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xCD | Signal KVA1 |
| 0xC1 | Signal TWEG+ (Tacho) |
| 0xC3 | Signal TD (Drehzahl) |
| 0xD3 | Kuehlmitteltemperatur |
| 0xCE | Aussentemperatur |
| 0xC7 | Tank-Hebelgeber_1 |
| 0xD7 | Tank-Hebelgeber_2 |
| 0x8F | Ueberspannung (U&gt;16V) |
| 0x8D | Signal AGS : Telegrammfehler oder kein Telegramm |
| 0x90 | Klemme 15 |
| 0x8C | Klemme R |
| 0xCF | SIA-Reset |
| 0x44 | Oeldruck |
| 0x8B | Gong_3 |
| 0x3F | Messwerktreiber |
| 0xBC | Bremsfluessigkeitsstand |
| 0xBD | EBV |
| 0xBE | Lichtmodul-EEPROM-Fehler |
| 0xBF | KOMBI-EEPROM-Fehler, Codierung fehlerhaft/unvollstaendig |
| 0x83 | Tacho A |
| 0x88 | I-Bus |
| 0x87 | K-Bus |
| 0xF0 | CAN BUS OFF |
| 0xF4 | keine CAN ID |
| 0xF5 | keine CAN ID ASC1 |
| 0xF6 | keine CAN ID DME1 |
| 0xF7 | keine CAN ID DME2 |
| 0xF8 | keine CAN ID DME4 |
| 0xFB | keine CAN ID EGS1 |
| 0xFC | kein CAN MST1 |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 9 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | ungueltiger Arbeitsbereich |
| 0x05 | Fehler momentan vorhanden |
| 0x06 | sporadischer Fehler |
| 0x07 | Fehler durch externes Steuergeraet |
| 0xFF | unbekannte Fehlerart |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 30 rows × 2 columns

| LIEF_NR | LIEF_NAME |
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
| 0xFF | unbekannter Hersteller |

<a id="table-getriebetypen"></a>
### GETRIEBETYPEN

Dimensions: 4 rows × 2 columns

| GETRIEBEART | GETRIEBETEXT |
| --- | --- |
| 0x00 | Schaltgetriebe |
| 0x01 | 5-Gang Automatik (EGS) |
| 0x02 | 4-Gang Automatik (EGS) |
| 0x03 | 5-Gang Schrittschaltung |

<a id="table-ganginfo"></a>
### GANGINFO

Dimensions: 9 rows × 2 columns

| GANGINFO | GANGTEXT |
| --- | --- |
| 0x00 | N oder P |
| 0x01 | 1. Gang |
| 0x02 | 2. Gang |
| 0x03 | 3. Gang |
| 0x04 | 4. Gang |
| 0x05 | 5. Gang |
| 0x06 | 6. Gang |
| 0x07 | Rueckwaertsgang |
| 0xFF | unbekannte Getriebeinfo |

<a id="table-waehlhebelinfo"></a>
### WAEHLHEBELINFO

Dimensions: 12 rows × 2 columns

| WAEHLHEBELINFO | WAEHLHEBELTEXT |
| --- | --- |
| 0x00 | Zwischenstellung |
| 0x01 | 1 |
| 0x02 | 2 |
| 0x03 | 3 |
| 0x04 | 4 |
| 0x05 | D |
| 0x06 | N |
| 0x07 | R |
| 0x08 | P |
| 0x09 | 5 |
| 0x0A | 6 |
| 0xFF | unbekannte Waehlhebelinfo |

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
| VERBRAUCH | 0x0E |
| FEHLER | 0xFF |
