# MFL.prg

- Jobs: [8](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Multifunktionslenkrad E38 |
| ORIGIN | BMW TI-430 Stübinger |
| REVISION | 1.17 |
| AUTHOR | BMW TP-421 Spoljarec |
| COMMENT | N/A |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer MFL E38
- [IDENT](#job-ident) - Ident-Daten fuer MFL
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [STATUS_LESEN](#job-status-lesen) - alle Stati des MFL lesen
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Herstelldaten lesen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

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

Init-Job fuer MFL E38

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer MFL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| ID_LIEF_TEXT | string | Lieferantenname |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| F_ORT_NR | int | Fehlercode |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ART1_NR | int | Index der 1. Fehlerart (entweder 0 oder 32) |
| F_ART1_TEXT | string | 1. Fehlerart als Text |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-status-lesen"></a>
### STATUS_LESEN

alle Stati des MFL lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| STAT_RADIO_VARIANTE | int | 0 -&gt; MFL ohne Radio, 1 -&gt; MFL mit Radio |
| STAT_TELEFON_VARIANTE | int | 0 -&gt; MFL ohne Telefon, 1 -&gt; MFL mit Telefon |
| STAT_UMLUFT_VARIANTE | int | 0 -&gt; MFL ohne Umluft, 1 -&gt; MFL mit Umluft |
| STAT_TEMPOMAT_VARIANTE | int | 0 -&gt; MFL ohne Tempomat, 1 -&gt; MFL mit Tempomat |
| STAT_TEMP_WA_BETAETIGT | int | rechte Taste Tempomat Wiederaufnahme betaetigt ? |
| STAT_TEMP_SB_BETAETIGT | int | rechte Taste Tempomat setzen beschleunigen betaetigt ? |
| STAT_TEMP_VER_BETAETIGT | int | rechte Taste Tempomat Verzoegerung betaetigt ? |
| STAT_TEMP_AUS_BETAETIGT | int | rechte Taste Tempomat aus betaetigt ? |
| STAT_UMLUFT_BETAETIGT | int | rechte Taste Umluft betaetigt ? |
| STAT_SEEK_UP_BETAETIGT | int | linke Taste Suchlauf aufwaerts betaetigt ? |
| STAT_VOL_UP_BETAETIGT | int | linke Taste Lautstaerke plus betaetigt ? |
| STAT_VOL_DOWN_BETAETIGT | int | linke Taste Lautstaerke minus betaetigt ? |
| STAT_SEEK_DOWN_BETAETIGT | int | linke Taste Suchlauf abwaerts betaetigt ? |
| STAT_R_T_BETAETIGT | int | linke Taste Radio_Telefon betaetigt ? |
| STAT_TELEFON_BETAETIGT | int | linke Taste Telefon betaetigt ? |
| STAT_U_SG_WERT | long | Betriebsspannung am MFL_SG in Volt |
| STAT_U_SG_EINH | string | Einheit zur Betriebsspannung am MFL_SG in Volt |
| STAT_U_SCHALTER_WERT | long | Betriebsspannung am Schalter |
| STAT_U_SCHALTER_EINH | string | Einheit zur Betriebsspannung am Schalter in Volt |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Herstelldaten lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| BYTE1 | int | Datenbyte 1 |
| BYTE2 | int | Datenbyte 2 |
| BYTE3 | int | Datenbyte 3 |
| BYTE4 | int | Datenbyte 4 |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (5 × 2)
- [FORTTEXTE](#table-forttexte) (6 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [SG_BETRIEBSMODE](#table-sg-betriebsmode) (4 × 2)
- [EINGANG_RECHTS](#table-eingang-rechts) (5 × 2)
- [EINGANG_LINKS](#table-eingang-links) (6 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 5 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xFF | ERROR_ECU_NACK |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 6 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Datenunterbrechung Signalleitung zum MFL |
| 0x02 | Tasten rechts SB und VER gleichzeitig betaetigt |
| 0x03 | Tasten links Radio-laut und leise gleichzeitig betaetigt |
| 0x07 | Kurzschluss Versorgungsspannung Lenkrad gegen Masse |
| 0x0A | EEPROM Schreibfehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler nicht aktiv |
| 0x20 | Fehler aktiv |
| 0xXY | unbekannte Fehlerart |

<a id="table-sg-betriebsmode"></a>
### SG_BETRIEBSMODE

Dimensions: 4 rows × 2 columns

| B_ART | B_ART_TEXTE |
| --- | --- |
| 0x01 | Radio |
| 0x02 | Telefon |
| 0x04 | Umluft |
| 0x08 | Tempomat |

<a id="table-eingang-rechts"></a>
### EINGANG_RECHTS

Dimensions: 5 rows × 2 columns

| TASTE_R | TASTE_R_TEXTE |
| --- | --- |
| 0x09 | Tempomat Wiederaufnahme |
| 0x12 | Tempomat Setzen Beschleunigen |
| 0x40 | Tempomat Verzoegerung |
| 0x24 | Tempomat Aus |
| 0x80 | Umluft |

<a id="table-eingang-links"></a>
### EINGANG_LINKS

Dimensions: 6 rows × 2 columns

| TASTE_L | TASTE_L_TEXTE |
| --- | --- |
| 0x83 | Suchlauf aufwaerts |
| 0x43 | Lautstaerke plus |
| 0x23 | Lautstaerke minus |
| 0x13 | Suchlauf abwaerts |
| 0x0B | Radio/Telefon |
| 0x07 | Telefon |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 27 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |
