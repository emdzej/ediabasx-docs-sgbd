# KOMBI46R.prg

- Jobs: [55](#jobs)
- Tables: [13](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | KOMBI E46 Redesign |
| ORIGIN | BMW TI-431 Dennert |
| REVISION | 2.10 |
| AUTHOR | BMW TI-431 Dennert |
| COMMENT | N/A |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [INFO](#job-info) - Information SGBD
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [IDENT](#job-ident) - Default ident job
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [GWSZ_OFFSET_LESEN](#job-gwsz-offset-lesen) - OFFSET-Wert des GWSZ aus EEPROM lesen
- [GWSZ_OFFSET_SCHREIBEN](#job-gwsz-offset-schreiben) - OFFSET-Wert des GWSZ in EEPROM schreiben
- [SIA_KORREKTUR_SCHREIBEN](#job-sia-korrektur-schreiben) - Toggeln der SIA Inspektions- bzw. Oelservices
- [ZEITINSPEKTION_VORZIEHEN](#job-zeitinspektion-vorziehen) - Vorziehen der Zeitinspection vor der Zeitgrenze
- [ZEITINSPEKTIONSDATUM_SCHREIBEN](#job-zeitinspektionsdatum-schreiben) - Beschreiben des Monats- u. Jahres-Bytes im EEPROM
- [ZEITINSPEKTIONSDATUM_LESEN](#job-zeitinspektionsdatum-lesen) - Monats- u. Jahres-Byte des Zeitinspektionsdatums aus EEPROM WortAdr. 1C
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicherinhalt aus SG lesen
- [SOFTWARE_RESET](#job-software-reset) - Kombi loest selbststaendig einen Reset aus
- [SIA_RESET](#job-sia-reset) - Ruecksetzen der Service-Intervall-Anzeige
- [GWSZ_RESET](#job-gwsz-reset) - GWSZ zuruecksetzen, nur moeglich wenn Km-Stand &lt; 255
- [STATUS_AIF_GWSZ_LESEN](#job-status-aif-gwsz-lesen) - Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen
- [GWSZ_MINUS_OFFSET_LESEN](#job-gwsz-minus-offset-lesen) - Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen und Offset abziehen
- [STATUS_AIF_FG_NR_LESEN](#job-status-aif-fg-nr-lesen) - Auslesen der Fahrgestellnummer
- [STATUS_AIF_SIA_DATEN_LESEN](#job-status-aif-sia-daten-lesen) - Anwenderinfofeld Block 3 auslesen
- [STATUS_AIF_TANKDATEN_LESEN](#job-status-aif-tankdaten-lesen) - Tankdaten aus Anwenderinfofeld auslesen
- [STATUS_AIF_AUSSENTEMP_LESEN](#job-status-aif-aussentemp-lesen) - Tankdaten aus Anwenderinfofeld auslesen
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Codierdaten auslesen
- [TACHO_ENDWERT_LESEN](#job-tacho-endwert-lesen) - Auslesen des Tacho-Endausschlags aus dem EEPROM
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - SG - Selbsttest ausloesen
- [STEUERN_ANZEIGE](#job-steuern-anzeige) - Anzeigenkomponenten steuern
- [STEUERN_GONG3](#job-steuern-gong3) - Gong3 ansteuern
- [STEUERN_PIEZO](#job-steuern-piezo) - interner Piezo ansteuern
- [STEUERN_LEUCHTE](#job-steuern-leuchte) - Leuchten in der Anzeigeeinheit ansteuern Es muessen 6 Argumente uebergeben werden. Die Belegung der Datenbytes ist separat beschrieben.
- [STATUS_IO_LESEN](#job-status-io-lesen) - Eingangs- und Ausgangsstati lesen
- [STATUS_ANALOG_LESEN](#job-status-analog-lesen) - Spezielle analoge Eingaenge lesen
- [RAM_LESEN](#job-ram-lesen) - RAM-Speicher auslesen
- [EEPROM_LESEN](#job-eeprom-lesen) - EEPROM-Speicher auslesen
- [STATUS_CAN_MOTORDREHZAHL_LESEN](#job-status-can-motordrehzahl-lesen) - Motordrehzahl ueber CAN auslesen
- [STATUS_CAN_KUEHLMITTELTEMP_LESEN](#job-status-can-kuehlmitteltemp-lesen) - Kuehlmitteltemperatur ueber CAN auslesen
- [STATUS_CAN_GETRIEBEINFO_LESEN](#job-status-can-getriebeinfo-lesen) - Getriebeinformationen (nur EGS) ueber CAN auslesen
- [STATUS_CAN_EINSPRITZMENGE_LESEN](#job-status-can-einspritzmenge-lesen) - Einspritzmenge (Verbrauch) ueber CAN auslesen
- [STATUS_CAN_SIGNALE_LESEN](#job-status-can-signale-lesen) - weitere CAN-Signale auslesen
- [STATUS_TOENS_IO](#job-status-toens-io) - Termischer Oelniveau Sensor Status I/O lesen
- [STATUS_TOENS_SG](#job-status-toens-sg) - Termischer Oelniveau Sensor Status SG lesen
- [ZCS_LESEN](#job-zcs-lesen) - Anwenderinfofeld Wortadr. 34-3D auslesen
- [STATUS_SIA_FINISH](#job-status-sia-finish) - SIA-Daten auslesen zur Fertigungskontrolle
- [C_S_AUFTRAG](#job-c-s-auftrag) - Codierdaten schreiben und verifizieren
- [C_S_SCHREIBEN](#job-c-s-schreiben) - Codierdaten schreiben
- [C_S_LESEN](#job-c-s-lesen) - Codierdaten schreiben und verifizieren
- [C_CHECKSUM](#job-c-checksum) - Berechnung und Speicherung der Checksumme
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen der Fahrgestellnummer
- [C_ZCS_LESEN](#job-c-zcs-lesen) - Anwenderinfofeld Wortadr. 34-3D auslesen
- [C_ZEIT_RESET](#job-c-zeit-reset) - Ruecksetzen des Zeitinspektionsintervall
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen Gueltiger Adressbereich: 0x10 - 0xDF (416 Bytes) für E46 (Codierindex &lt; 7 und 19 &lt; Codierindex &lt;= 22) Gueltiger Adressbereich: 0xC2 - 0x181 (384 Bytes) für E46 (Codierindex &gt; 22 und 7 &lt;= Codierindex  &lt;= 19)
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben Fahrzeugauftrag lesen Gueltiger Adressbereich: 0x10 - 0xDF (416 Bytes) für E46 (Codierindex &lt; 7 und 19 &lt; Codierindex &lt;= 22) Gueltiger Adressbereich: 0xC2 - 0x181 (384 Bytes) für E46 (Codierindex &gt; 22 und 7 &lt;= Codierindex  &lt;= 19)
- [C_FA_LOESCHEN](#job-c-fa-loeschen) - Fahrzeugauftrag Löschen Gueltiger Adressbereich: 0x10 - 0xDF (416 Bytes) für E46 (Codierindex &lt; 7 und 19 &lt; Codierindex &lt;= 22) Gueltiger Adressbereich: 0xC2 - 0x181 (384 Bytes) für E46 (Codierindex &gt; 22 und 7 &lt;= Codierindex  &lt;= 19)

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

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

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Pruefstempel 1. Byte (0-255), kann beliebig verwendet werden |
| BYTE2 | int | Pruefstempel 2. Byte (0-255), kann beliebig verwendet werden |
| BYTE3 | int | Pruefstempel 3. Byte (0-255), kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| _TEL_AN_SG | binary | Telegramm an SG |
| _TEL_ANTWORT | binary | Antworttelegramm von SG |

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

<a id="job-sia-korrektur-schreiben"></a>
### SIA_KORREKTUR_SCHREIBEN

Toggeln der SIA Inspektions- bzw. Oelservices

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-zeitinspektion-vorziehen"></a>
### ZEITINSPEKTION_VORZIEHEN

Vorziehen der Zeitinspection vor der Zeitgrenze

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATUM_MONAT | int | Monatsangabe [1-12], aktuelles Datum |
| DATUM_JAHR | int | Jahresangabe [0-99], akuelles Datum |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM_1_ZEITGRENZE_LESEN | binary | Telegramm an SG: Zeitgrenze lesen |
| SG_ANTWORT_1_ZEITGRENZE_LESEN | binary | Antworttelegramm von SG: Zeitgrenze lesen |
| TELEGRAMM_2_ZEITGRENZE_SCHREIBEN | binary | Telegramm an SG: Zeitgrenze schreiben |
| SG_ANTWORT_2_ZEITGRENZE_SCHREIBEN | binary | Antworttelegramm von SG: Zeitgrenze schreiben |
| TELEGRAMM_3_ZEITINSPEKTION_LESEN | binary | Telegramm an SG: Zeitinspektionsdatum lesen |
| SG_ANTWORT_3_ZEITINSPEKTION_LESEN | binary | Antworttelegramm von SG: Zeitinspektionsdatum lesen |
| TELEGRAMM_4_ZEITINSPEKTION_SCHREIBEN | binary | Telegramm an SG: Zeitinspektionsdatum schreiben |
| SG_ANTWORT_4_ZEITINSPEKTION_SCHREIBEN | binary | Antworttelegramm von SG: Zeitinspektionsdatum schreiben |
| TELEGRAMM_5_CS_LESEN | binary | Telegramm an SG: Checksum lesen |
| SG_ANTWORT_5_CS_LESEN | binary | Antworttelegramm von SG: Checksum lesen |
| TELEGRAMM_6_CS_SCHREIBEN | binary | Telegramm an SG: Checksum schreiben |
| SG_ANTWORT_6_CS_SCHREIBEN | binary | Antworttelegramm von SG: Checksum schreiben |
| TELEGRAMM_7_SW_RESET | binary | Telegramm an SG: Software-Reset ausfuehren |
| SG_ANTWORT_7_SW_RESET | binary | Antworttelegramm von SG: Software-Reset ausfuehren |
| TELEGRAMM_8_ZEITINSPEKTIONS_RESET | binary | Telegramm an SG: Zeitinspektionsreset ausfuehren |
| SG_ANTWORT_8_ZEITINSPEKTIONS_RESET | binary | Antworttelegramm von SG: Zeitinspektionsreset ausfuehren |
| TELEGRAMM_9_ZEITGRENZE_SCHREIBEN | binary | Telegramm an SG: Zeitinspektionsgrenze schreiben |
| SG_ANTWORT_9_ZEITGRENZE_SCHREIBEN | binary | Antworttelegramm von SG: Zeitinspektionsdatum schreiben |
| TELEGRAMM_10_CS_SCHREIBEN | binary | Telegramm an SG: Checksum schreiben |
| SG_ANTWORT_10_CS_SCHREIBEN | binary | Antworttelegramm von SG: Checksum schreiben |
| TELEGRAMM_11_SW_RESET | binary | Telegramm an SG: Software-Reset ausfuehren |
| SG_ANTWORT_11_SW_RESET | binary | Antworttelegramm von SG: Software-Reset ausfuehren |

<a id="job-zeitinspektionsdatum-schreiben"></a>
### ZEITINSPEKTIONSDATUM_SCHREIBEN

Beschreiben des Monats- u. Jahres-Bytes im EEPROM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEITINSPEKTION_MONAT | int | Monatsangabe [1-12] |
| ZEITINSPEKTION_JAHR | int | Jahresangabe [0-99] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-zeitinspektionsdatum-lesen"></a>
### ZEITINSPEKTIONSDATUM_LESEN

Monats- u. Jahres-Byte des Zeitinspektionsdatums aus EEPROM WortAdr. 1C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ZEITINSPEKTION_MONAT | int | Monatsangabe [1-12] |
| ZEITINSPEKTION_JAHR | int | Jahresangabe [0-99] |
| SERVICE_INTERVALL | int | 0 = US, 1 = Japan, 2 = ECE |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| ANTWORT | binary | Antworttelegramm von SG |

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
| ARG1 | string | moegliche Uebergabeparameter: Oel_Reset, Weg_Reset, Zeit_Reset, Weg_Reset_Werk |

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

<a id="job-status-aif-gwsz-lesen"></a>
### STATUS_AIF_GWSZ_LESEN

Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_GWSZ_WERT | long | Gesamtwegstreckenzaehler |
| STAT_GWSZ_EINH | string | Einheit des GWSZ [km] |
| ANTWORT | binary | Antworttelegramm von SG |

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

<a id="job-status-aif-fg-nr-lesen"></a>
### STATUS_AIF_FG_NR_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_AIF_FG_NR | string | Fahrgestellnummer |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-aif-sia-daten-lesen"></a>
### STATUS_AIF_SIA_DATEN_LESEN

Anwenderinfofeld Block 3 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_MOTORTYP_NR | int | 0 = Benzinmotor, 1 = Dieselmotor |
| STAT_MOTORTYP_TEXT | string | "Benzinmotor", "Dieselmotor" |
| STAT_GETRIEBE_NR | int | 0 = Schaltgetriebe, 1 = Automatikgetriebe, 2 = SMG (AG) (siehe table Getriebetypen) |
| STAT_GETRIEBE_TEXT | string | "Schaltgetriebe", "Automatikgetriebe", (siehe table Getriebetypen) |
| STAT_ZEITINSPEKTION | int | keine Zeitinspektion = 0 |
| STAT_VORGEZOGENE_ZEITINSPEKTION | int | 1 wenn vorgezogene Zeitinspektion moeglich |
| STAT_INSPEKTIONSGRENZE_WERT | int | Inspektionsgrenze |
| STAT_INSPEKTIONSGRENZE_EINH | string | Einheit "Liter" |
| STAT_ZEITGRENZE_WERT | int | Zeitgrenze |
| STAT_ZEITGRENZE_EINH | string | Einheit "Tage" |
| STAT_KRAFTSTOFFMENGE_WERT | int | verbrauchte SI-Kraftstoffmenge |
| STAT_KRAFTSTOFFMENGE_EINH | string | Einheit "Liter" |
| STAT_ZEIT_INSP_ZAEHLER_WERT | int | Zeitinspektionszaehler |
| STAT_ZEIT_INSP_ZAEHLER_EINH | string | Einheit "Tage" |
| STAT_SERVICE_ART | int | Art des letzten Service: 0 = Inspektion, 1 = Oelservice |
| STAT_SERVICE_TEXT | string | "Inspektion", "Oelservice" |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-aif-tankdaten-lesen"></a>
### STATUS_AIF_TANKDATEN_LESEN

Tankdaten aus Anwenderinfofeld auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_TANKINHALT_HEBEL1_WERT | real | Tankinhalt Hebelgeber1 in Liter |
| STAT_TANKINHALT_HEBEL2_WERT | real | Tankinhalt Hebelgeber2 in Liter |
| STAT_TANKINHALT_UNGEF_WERT | real | Tankinhaltanzeige gesamt in Liter (ungefiltert) |
| STAT_TANKINHALT_GEF_WERT | real | Tankinhaltanzeige gesamt in Liter (gefiltert) |
| STAT_TANKINHALT_HEBEL1_EINH | string | Einheit Tankinhalt Hebelgeber1: "Liter" |
| STAT_TANKINHALT_HEBEL2_EINH | string | Einheit Tankinhalt Hebelgeber2: "Liter" |
| STAT_TANKINHALT_UNGEF_EINH | string | Einheit Tankanzeigewert gesamt (ungefiltert): "Liter" |
| STAT_TANKINHALT_GEF_EINH | string | Einheit Tankanzeigewert gesamt (gefiltert): "Liter" |
| STAT_RESERVE | string | Tankreserve erreicht ("EIN" oder "AUS") |

<a id="job-status-aif-aussentemp-lesen"></a>
### STATUS_AIF_AUSSENTEMP_LESEN

Tankdaten aus Anwenderinfofeld auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_AUSSENTEMP_GEF_WERT | real | Aussentemperatur in "Grad Celsius" (gefiltert) |
| STAT_AUSSENTEMP_GEF_EINH | string | Einheit Aussentemperatur: "Grad Celsius" (gefiltert) |
| STAT_AUSSENTEMP_UNGEF_WERT | real | Aussentemperatur in "Grad Celsius" (ungefiltert) |
| STAT_AUSSENTEMP_UNGEF_EINH | string | Einheit Aussentemperatur: "Grad Celsius" (ungefiltert) |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Codierdaten auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_KOMBI_CODIERT | int | 1, wenn Kombi codiert ist |
| STAT_BC_FUNKTION_AKTIV | int | 1, wenn BC-Funktion aktiv |
| STAT_ATEMP_SENSOR_VERBAUT | int | 1, wenn Atemp.-Sensor verbaut |
| STAT_GONG_FUNKTION_AKTIV | int | 1, wenn eine akustische Ausgabe auf Gong codiert ist |
| STAT_OPT_GURTWARNUNG_AKTIV | int | 1, wenn opt. Gurtwarnung (solange Gurt offen) codiert ist |
| STAT_ZUENDSCHLUESSELWARNUNG_AKTIV | int | 1, wenn Zundschluesselwarnung codiert ist |
| STAT_AKUSTIKWARNUNG_HANDBREMSE_AKTIV | int | 1, wenn Zundschluesselwarnung codiert ist |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-tacho-endwert-lesen"></a>
### TACHO_ENDWERT_LESEN

Auslesen des Tacho-Endausschlags aus dem EEPROM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation: OKAY, ERROR_ECU_NACK... |
| TACHO_ENDWERT_CODE | string | gibt den Codierwert zum Tachoendwert als String aus |
| SG_ANTWORT | binary | Antworttelegramm vom SG |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

SG - Selbsttest ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |

<a id="job-steuern-anzeige"></a>
### STEUERN_ANZEIGE

Anzeigenkomponenten steuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Zu steuernde Komponente, siehe table Komponenten moegliche Uebergabeparamter: TACHO, DREHZAHL, TANKINHALT, KUEHLMITTELTEMPERATUR, VERBRAUCH |
| WERT | int | Winkelgrade im Bereich von (10-90) Grad, Mit Spruengen von mehr als 90 Grad sollten die Messwerke nicht beaufschlagt werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-gong3"></a>
### STEUERN_GONG3

Gong3 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-piezo"></a>
### STEUERN_PIEZO

interner Piezo ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |

<a id="job-steuern-leuchte"></a>
### STEUERN_LEUCHTE

Leuchten in der Anzeigeeinheit ansteuern Es muessen 6 Argumente uebergeben werden. Die Belegung der Datenbytes ist separat beschrieben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Belegung 1. Datenbytes: (0-0xFF) Bit0: Kuehlmitteltemperatur Bit1: frei Bit2: RDC gelb Bit3: RDC rot Bit4: Gurtwarnung Bit5: Bremsbelag Bit6: frei Bit7: frei |
| BYTE2 | int | Belegung 2. Datenbytes: (0-0xFF) Bit0: Tempomat Bit1: Tempomat Bit2: DBC gelb Bit3: Allgemeine Bremsleuchte rot Bit4: ASC Bit5: Ladekontrolle Bit6: Oelstand gelb Bit7: Oelstand rot |
| BYTE3 | int | Belegung 3. Datenbytes: (0-0xFF) Bit0: CC-Ruecklicht rechts Bit1: CC-Ruecklicht links Bit2: CC-Heckklappe Bit3: CC-Tuer hinten rechts Bit4: CC-Tuer hinten links Bit5: CC-Tuer vorne rechts Bit6: frei Bit7: frei |
| BYTE4 | int | Belegung 4. Datenbytes: (0-0xFF) Bit0: CC-Kontur Bit1: CC-Tuer vorne links Bit2: CC-Abblendlicht links Bit3: CC-Abblendlicht rechts Bit4: Kuehlmittelstand Bit5: Waschwasser Bit6: Vorgluehen Bit7: frei |
| BYTE5 | int | Belegung 5. Datenbytes: (0-0xFF) Bit0: Check Engine Bit1: Tankverriegelung Bit2: Nebelschlussleuchte Bit3: Nebelscheinwerfer Bit4: Nebelscheinwerfer Bit5: Tankreserve Bit6: frei Bit7: Fernlicht |
| BYTE6 | int | Belegung 6. Datenbytes: (0-0xFF) Bit0: Blinkerklopfer Bit1: Blinker links Bit2: Blinker rechts Bit3: Tacho-A statisch Bit4: Gong T3 statisch Bit5: Tankreserve Bit6: frei Bit7: Fernlicht |

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
| STAT_KL30_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_TASTE_UHR_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_UHRTASTE_RUECKLAUF_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KL50_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_SIA_RESET_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_UHRTASTE_VORLAUF_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_GONGT3_EIN | int | 1, wenn "TRUE" , 0, wenn "FALSE" |
| STAT_SUMMER_EIN | int | 1, wenn "TRUE" , 0, wenn "FALSE" |
| STAT_BREMSFLUESSIGKEIT_EIN | int | 1, wenn "TRUE" , 0, wenn "FALSE" |
| STAT_KLR_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KL15_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_KUEHLMITTELSTAND_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_TASTE_TWSZ_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| STAT_LSS_EIN | int | 1, wenn "TRUE", 0, wenn "FALSE" |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-analog-lesen"></a>
### STATUS_ANALOG_LESEN

Spezielle analoge Eingaenge lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_5V_WERT | unsigned int | AD - Kanal 0, 5V fixe Spannung |
| STAT_5V_LONG_WERT | long | AD - Kanal 0, 5V fixe Spannung |
| STAT_5V_EINH | string | Einheit [ADC-Wert] |
| STAT_HEBELGEBER1_WERT | unsigned int | AD - Kanal 1, Wert des 1. Hebelgebers |
| STAT_HEBELGEBER1_LONG_WERT | long | AD - Kanal 1, Wert des 1. Hebelgebers |
| STAT_HEBELGEBER1_EINH | string | Einheit [ADC-Wert] |
| STAT_HEBELGEBER2_WERT | unsigned int | AD - Kanal 2, Wert des 2. Hebelgebers |
| STAT_HEBELGEBER2_LONG_WERT | long | AD - Kanal 2, Wert des 2. Hebelgebers |
| STAT_HEBELGEBER2_EINH | string | Einheit [ADC-Wert] |
| STAT_BREMSVERSCHLEISS1_WERT | unsigned int | Wert AD - Kanal 6, Wert des Bremsbelagverschleisses1 |
| STAT_BREMSVERSCHLEISS1_LONG_WERT | long | Wert AD - Kanal 6, Wert des Bremsbelagverschleisses1 |
| STAT_BREMSVERSCHLEISS1_EINH | string | Einheit [ADC-Wert] |
| STAT_AUSSENTEMP_WERT | unsigned int | Wert AD - Kanal 7, Wert der Aussentemperatur |
| STAT_AUSSENTEMP_LONG_WERT | long | Wert AD - Kanal 7, Wert der Aussentemperatur |
| STAT_AUSSENTEMP_EINH | string | Einheit [ADC-Wert] |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-ram-lesen"></a>
### RAM_LESEN

RAM-Speicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAM_TYPE | string | "EXTERN" |
| ADRESSE | string | Hexwert (0x000-0xFFFF) der Adresse ,ab der das Ram gelesen werden soll |
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
| ADRESSE | string | Hexwert (0x0000-0x03FF) der WortAdresse ,ab der das EEPROM gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der 2-Byte-Worte (max. 16 Worte = 32 Bytes), die ausgelesen werden koennen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| DATEN | binary | Datenfeld |

<a id="job-status-can-motordrehzahl-lesen"></a>
### STATUS_CAN_MOTORDREHZAHL_LESEN

Motordrehzahl ueber CAN auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_MOTORDREHZAHL_WERT | long | Motordrehzahl in U/min |
| STAT_MOTORDREHZAHL_EINH | string | Einheit Motordrehzahl [U/min] |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-can-kuehlmitteltemp-lesen"></a>
### STATUS_CAN_KUEHLMITTELTEMP_LESEN

Kuehlmitteltemperatur ueber CAN auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_KUEHLMITTELTEMP_WERT | long | Kuehlmitteltemperatur in [Grad Celsius] |
| STAT_KUEHLMITTELTEMP_EINH | string | Einheit [Grad Celsius] |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-can-getriebeinfo-lesen"></a>
### STATUS_CAN_GETRIEBEINFO_LESEN

Getriebeinformationen (nur EGS) ueber CAN auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_GANG_INFO_WERT | int | gibt an in welchem Gang sich zur Zeit das Getriebe befindet |
| STAT_GANG_INFO_TEXT | string | gibt an in welchem Gang sich zur Zeit das Getriebe befindet |
| STAT_GANG_WHL_ANZ_WERT | int | gibt Waehlhebelposition an: 1,2,3,4,D,N,R,P,5,6,Zwischenstellung |
| STAT_GANG_WHL_ANZ_TEXT | string | gibt Waehlhebelposition an: 1,2,3,4,D,N,R,P,5,6,Zwischenstellung |
| STAT_PRG_INF_ANZ_WERT | int | gibt Programminfo aus: E,M,S,W,A,Anzeige aus |
| STAT_PRG_INF_ANZ_TEXT | string | gibt Programminfo aus: E,M,S,W,A,Anzeige aus |
| STAT_L_GETR_STEUERUNG_WERT | int | gibt Zustand der Getriebesteuerung an: Getriebenotprogramm ein |
| STAT_L_GETR_STEUERUNG_TEXT | string | gibt Zustand der Getriebesteuerung an: Getriebenotprogramm ein |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-can-einspritzmenge-lesen"></a>
### STATUS_CAN_EINSPRITZMENGE_LESEN

Einspritzmenge (Verbrauch) ueber CAN auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Job-Status: OKAY, ERROR_.. |
| STAT_EINSPRITZMENGE_WERT | long | Einspritzmenge in [ul] |
| STAT_EINSPRITZMENGE_EINH | string | Einheit [ul] |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-can-signale-lesen"></a>
### STATUS_CAN_SIGNALE_LESEN

weitere CAN-Signale auslesen

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
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-status-toens-io"></a>
### STATUS_TOENS_IO

Termischer Oelniveau Sensor Status I/O lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TOG_HIGH_WERT | int | gemessene TOENS-Signal-Highzeit |
| STAT_TOG_HIGH_EINH | string | ms |
| STAT_TOG_LOW_WERT | int | gemessene TOENS-Signal-Lowzeit |
| STAT_TOG_LOW_EINH | string | ms |
| STAT_DREHZAHL_WERT | int | gemessene Motordrehzahl |
| STAT_DREHZAHL_EINH | string | 1/min |
| ANTWORT | binary | Antworttelegramm |

<a id="job-status-toens-sg"></a>
### STATUS_TOENS_SG

Termischer Oelniveau Sensor Status SG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TOG_LOW_WERT | int | gemessene TOENS-Signal-Lowzeit |
| STAT_TOG_LOW_EINH | string | ms |
| STAT_TOG_HIGH_WERT | int | gemessene TOENS-Signal-Highzeit |
| STAT_TOG_HIGH_EINH | string | ms |
| STAT_STATUS_FLAG_WERT | int | Status Flags |
| STAT_STATUS_FLAG_EINH | string | -- |
| STAT_DELAY_EIN | int | Startverzoegerung abgelaufen |
| STAT_OELKALT_EIN | int | kaltes Oel erkannt |
| STAT_OELWARM_EIN | int | warmes Oel erkannt |
| STAT_FKWREADY_EIN | int | orient. Messung abgelaufen |
| STAT_FIRSTAML_EIN | int | erster, vorgezogener Mittelwert |
| STAT_IGNOREMW_EIN | int | Messwertausblendung |
| STAT_FUNKTION_EIN | int | Funktionsanz. im TOENS-Takt |
| STAT_TOG_IMP_COUNTER_WERT | int | Messwertzaehler fuer Kurzzeit-Mittelwert |
| STAT_TOG_IMP_COUNTER_EINH | string | -- |
| STAT_MITTEL_LANG_COUNT_WERT | int | Messwertzaehler fuer Langzeit-Mittelwert |
| STAT_MITTEL_LANG_COUNT_EINH | string | -- |
| STAT_DREHZAHL_MITTEL_WERT | int | Mittelwert der Motordrehzahl |
| STAT_DREHZAHL_MITTEL_EINH | string | 1/min |
| STAT_TOG_HIGH_MITTEL_WERT | int | Kurzzeitmittelwert der TOENS-Heizzeit |
| STAT_TOG_HIGH_MITTEL_EINH | string | ms |
| STAT_TOG_NIVEAU_MITTEL_1_WERT | real | Kurzzeitmittelwert des Oelniveaus |
| STAT_TOG_NIVEAU_MITTEL_1_EINH | string | mm |
| STAT_TOG_NIVEAU_MITTEL_KORR_WERT | real | drehzahlkorregierter Kurzzeitmittelwert des Oelniveaus |
| STAT_TOG_NIVEAU_MITTEL_KORR_EINH | string | mm |
| STAT_TOG_NIVEAU_MITTEL_WERT | real | Langzeitmittelwert des Oelniveaus |
| STAT_TOGINFO_WERT | int | TOGINFO Flags |
| STAT_TOGINFO_EINH | string | -- |
| STAT_WARNUNGH_EIN | int | Warnung Oelverlust |
| STAT_WARNUNGL_EIN | int | Warnung Oelverbrauch |
| STAT_NOSIGNAL_EIN | int | Kein Sensorsignal |
| ANTWORT | binary | Antworttelegramm |

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
| STAT_BITSTATUS_0x28 | int | Bitstatus oberstes Bit Adresse 0x0F |
| SIA_SPEICHER_CHECK | string | Gesamtergebnis des Speicherchecks |

<a id="job-c-s-auftrag"></a>
### C_S_AUFTRAG

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-s-schreiben"></a>
### C_S_SCHREIBEN

Codierdaten schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-s-lesen"></a>
### C_S_LESEN

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-checksum"></a>
### C_CHECKSUM

Berechnung und Speicherung der Checksumme

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CHECKSUM | binary | berechnete Checksumme |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-c-zcs-lesen"></a>
### C_ZCS_LESEN

Anwenderinfofeld Wortadr. 34-3D auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| GM | string | C1 Zifferncode fuer Grundmerkmal |
| SA | string | C2 Zifferncode fuer Sonderausstattung |
| VN | string | C3 Zifferncode fuer Versionsnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-c-zeit-reset"></a>
### C_ZEIT_RESET

Ruecksetzen des Zeitinspektionsintervall

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK od. ERROR_PARAMETER |

<a id="job-c-fa-lesen"></a>
### C_FA_LESEN

Fahrzeugauftrag lesen Gueltiger Adressbereich: 0x10 - 0xDF (416 Bytes) für E46 (Codierindex &lt; 7 und 19 &lt; Codierindex &lt;= 22) Gueltiger Adressbereich: 0xC2 - 0x181 (384 Bytes) für E46 (Codierindex &gt; 22 und 7 &lt;= Codierindex  &lt;= 19)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | Daten des Fahrzeugauftrages |
| SPEICHER_STATUS | string | BELEGT bzw. UNBELEGT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-fa-auftrag"></a>
### C_FA_AUFTRAG

Fahrzeugauftrag schreiben Fahrzeugauftrag lesen Gueltiger Adressbereich: 0x10 - 0xDF (416 Bytes) für E46 (Codierindex &lt; 7 und 19 &lt; Codierindex &lt;= 22) Gueltiger Adressbereich: 0xC2 - 0x181 (384 Bytes) für E46 (Codierindex &gt; 22 und 7 &lt;= Codierindex  &lt;= 19)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-fa-loeschen"></a>
### C_FA_LOESCHEN

Fahrzeugauftrag Löschen Gueltiger Adressbereich: 0x10 - 0xDF (416 Bytes) für E46 (Codierindex &lt; 7 und 19 &lt; Codierindex &lt;= 22) Gueltiger Adressbereich: 0xC2 - 0x181 (384 Bytes) für E46 (Codierindex &gt; 22 und 7 &lt;= Codierindex  &lt;= 19)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (72 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [SIARESET](#table-siareset) (4 × 2)
- [FORTTEXTE](#table-forttexte) (24 × 2)
- [FARTTEXTE](#table-farttexte) (8 × 2)
- [GETRIEBETYPEN](#table-getriebetypen) (5 × 2)
- [GANGINFO](#table-ganginfo) (9 × 2)
- [WAEHLHEBELINFO](#table-waehlhebelinfo) (12 × 2)
- [PROGRAMMINFO](#table-programminfo) (7 × 2)
- [KOMPONENTEN](#table-komponenten) (7 × 2)
- [TOENS_IO](#table-toens-io) (5 × 4)
- [TOENS_SG](#table-toens-sg) (5 × 12)

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

<a id="table-siareset"></a>
### SIARESET

Dimensions: 4 rows × 2 columns

| SELECTOR | RESET |
| --- | --- |
| OEL_RESET | 0x01 |
| WEG_RESET | 0x02 |
| ZEIT_RESET | 0x04 |
| WEG_RESET_WERK | 0x08 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 24 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x11 | TOG |
| 0x21 | unplausible SMG-Inhalte |
| 0x83 | Tacho A |
| 0x87 | K-Bus |
| 0x8C | Klemme R |
| 0x8F | Ueberspannung (U&gt;16V) |
| 0xBB | Checksumme Fehler EEPROM Bosch-Bereich |
| 0xBE | Lichtmodul-EEPROM-Fehler |
| 0xBF | Checksumme Fehler EEPROM BMW-Bereich |
| 0xC1 | Signal TWEG+ (Tacho) |
| 0xC7 | Tank-Hebelgeber_links |
| 0xCE | Aussentemperatur |
| 0xCF | SIA-Reset |
| 0xD7 | Tank-Hebelgeber_rechts |
| 0xF0 | CAN BUS OFF |
| 0xF4 | keine CAN ID |
| 0xF5 | keine CAN ID ASC1 |
| 0xF6 | keine CAN ID DME1 |
| 0xF7 | keine CAN ID DME2 |
| 0xF8 | keine CAN ID DME4 |
| 0xF9 | keine CAN ID ASC3 |
| 0xFB | keine CAN ID EGS1 |
| 0xFC | keine CAN ID SMG1 |
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
| 0x05 | Fehler momentan vorhanden |
| 0x06 | sporadischer Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-getriebetypen"></a>
### GETRIEBETYPEN

Dimensions: 5 rows × 2 columns

| GETRIEBEART | GETRIEBETEXT |
| --- | --- |
| 0x00 | Schaltgetriebe |
| 0x01 | Automatikgetriebe |
| 0x02 | SMG (AG) |
| 0x03 | SMG Motorsport |
| 0xFF | unbekannte Getriebeart |

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

Dimensions: 7 rows × 2 columns

| ORT | BYTE |
| --- | --- |
| TACHO | 0x0A |
| DREHZAHL | 0x0B |
| TANKINHALT | 0x0C |
| KUEHLMITTELTEMPERATUR | 0x0D |
| VERBRAUCH | 0x0E |
| Fehler | 0xFF |
| unbekannt | 0xEE |

<a id="table-toens-io"></a>
### TOENS_IO

Dimensions: 5 rows × 4 columns

| SOFTWARE | ADRESSE1 | ADRESSE2 | ADRESSE3 |
| --- | --- | --- | --- |
| 0x04 | 0x04A9 | 0x04C8 | 0x04B7 |
| 0x05 | 0x04A9 | 0x04C8 | 0x04B7 |
| 0x06 | 0x04A9 | 0x04C8 | 0x04B7 |
| 0x07 | 0x04A7 | 0x04C6 | 0x04B5 |
| 0xFF | 0xFFFF | 0xFFFF | 0xFFFF |

<a id="table-toens-sg"></a>
### TOENS_SG

Dimensions: 5 rows × 12 columns

| SOFTWARE | ADRESSE1 | ADRESSE2 | ADRESSE3 | ADRESSE4 | ADRESSE5 | ADRESSE6 | ADRESSE7 | ADRESSE8 | ADRESSE9 | ADRESSE10 | ADRESSE11 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x04 | 0x04A9 | 0x04C8 | 0x04B6 | 0x04CC | 0x04BD | 0x04B7 | 0x04D1 | 0x04FA | 0x04DD | 0x04DD | 0x04E3 |
| 0x05 | 0x04A9 | 0x04C8 | 0x04B6 | 0x04CC | 0x04BD | 0x04B7 | 0x04D1 | 0x04FA | 0x04DD | 0x04DD | 0x04E3 |
| 0x06 | 0x04A9 | 0x04C8 | 0x04B6 | 0x04CC | 0x04BD | 0x04B7 | 0x04D1 | 0x04FA | 0x04DD | 0x04DD | 0x04E3 |
| 0x07 | 0x04A7 | 0x04C6 | 0x04B4 | 0x04CA | 0x04BB | 0x04B5 | 0x04CF | 0x04F8 | 0x04DB | 0x04DB | 0x04E1 |
| 0xFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
