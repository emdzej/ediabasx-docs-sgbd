# C_KMB46.prg

- Jobs: [22](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | C-SGBD I-Kombi E46 |
| ORIGIN | BMW TI-431 Lothar Dennert |
| REVISION | 1.12 |
| AUTHOR | BMW TI-433 Mario Spoljarec, BMW TI-431 Lothar Dennert |
| COMMENT | Verifiziert |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer Kombi
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Default ident job
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [AIF_GWSZ_LESEN](#job-aif-gwsz-lesen) - Gesamtwegstreckenzaehler aus Anwenderinfofeld auslesen
- [GWSZ_OFFSET_LESEN](#job-gwsz-offset-lesen) - OFFSET-Wert des GWSZ aus EEPROM lesen
- [GWSZ_OFFSET_SCHREIBEN](#job-gwsz-offset-schreiben) - OFFSET-Wert des GWSZ in EEPROM schreiben
- [ZEITINSPEKTIONSDATUM_SCHREIBEN](#job-zeitinspektionsdatum-schreiben) - Beschreiben des Monats- u. Jahres-Bytes im EEPROM
- [ZEITINSPEKTIONSDATUM_LESEN](#job-zeitinspektionsdatum-lesen) - Monats- u. Jahres-Byte des Zeitinspektionsdatums aus EEPROM WortAdr. 1C
- [C_ZEIT_RESET](#job-c-zeit-reset) - Ruecksetzen des Zeitinspektionsintervall
- [SOFTWARE_RESET](#job-software-reset) - Kombi loest selbststaendig einen Reset aus
- [SIA_RESET](#job-sia-reset) - Ruecksetzen der Service-Intervall-Anzeige
- [C_S_AUFTRAG](#job-c-s-auftrag) - Codierdaten schreiben und verifizieren
- [C_S_SCHREIBEN](#job-c-s-schreiben) - Codierdaten schreiben
- [C_S_LESEN](#job-c-s-lesen) - Codierdaten schreiben und verifizieren
- [C_CHECKSUM](#job-c-checksum) - Berechnung und Speicherung der Checksumme
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen der Fahrgestellnummer
- [C_ZCS_LESEN](#job-c-zcs-lesen) - Anwenderinfofeld Wortadr. 34-3D auslesen
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen Gueltiger Adressbereich: 0x10 - 0xDF (416 Bytes) für E46 (Codierindex &lt; 7 und 19 &lt; Codierindex &lt;= 22) Gueltiger Adressbereich: 0xC2 - 0x181 (384 Bytes) für E46 (Codierindex &gt; 22 und 7 &lt;= Codierindex  &lt;= 19)
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben Fahrzeugauftrag lesen Gueltiger Adressbereich: 0x10 - 0xDF (416 Bytes) für E46 (Codierindex &lt; 7 und 19 &lt; Codierindex &lt;= 22) Gueltiger Adressbereich: 0xC2 - 0x181 (384 Bytes) für E46 (Codierindex &gt; 22 und 7 &lt;= Codierindex  &lt;= 19)
- [C_FA_LOESCHEN](#job-c-fa-loeschen) - Fahrzeugauftrag Löschen Gueltiger Adressbereich: 0x10 - 0xDF (416 Bytes) für E46 (Codierindex &lt; 7 und 19 &lt; Codierindex &lt;= 22) Gueltiger Adressbereich: 0xC2 - 0x181 (384 Bytes) für E46 (Codierindex &gt; 22 und 7 &lt;= Codierindex  &lt;= 19)
- [STATUS_AIF_SIA_DATEN_LESEN](#job-status-aif-sia-daten-lesen) - Anwenderinfofeld Block 3 auslesen

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer Kombi

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

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
| ID_CAN_INDEX | string | CAN-Index |
| ID_AENDERUNGSINDEX | int | Aenderungsindex |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

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

<a id="job-c-zeit-reset"></a>
### C_ZEIT_RESET

Ruecksetzen des Zeitinspektionsintervall

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK od. ERROR_PARAMETER |

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
| ARG3 | string | Oel/Wegs oder Zeit - Reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK od. ERROR_PARAMETER |

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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (9 × 2)
- [LIEFERANTEN](#table-lieferanten) (29 × 2)
- [SIARESET](#table-siareset) (3 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 9 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x02 | OKAY |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 29 rows × 2 columns

| LIEF_NR | LIEF_NAME |
| --- | --- |
| 0x01 | Reinshagen |
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
| 0xFF | unbekannter Hersteller |

<a id="table-siareset"></a>
### SIARESET

Dimensions: 3 rows × 2 columns

| SELECTOR | RESET |
| --- | --- |
| OEL_RESET | 0x01 |
| WEG_RESET | 0x02 |
| ZEIT_RESET | 0x04 |
