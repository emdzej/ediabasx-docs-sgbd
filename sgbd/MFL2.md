# MFL2.prg

- Jobs: [5](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MFL2 - Multifunktionslenkrad |
| ORIGIN | BMW TI-430 Stübinger |
| REVISION | 1.03 |
| AUTHOR | BMW TP-421 Spoljarec,BMW TI-431 Stadlhofer |
| COMMENT | N/A |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer MFL E38
- [IDENT](#job-ident) - Ident-Daten fuer MFL
- [STATUS_LESEN](#job-status-lesen) - alle Stati des MFL lesen
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
| STAT_LENKRADHEIZUNG_VARIANTE | int | 0 -&gt; MFL ohne Lenkradheizung, 1 -&gt; MFL mit Lenkradheizung |
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
| STAT_LENKRADHEIZUNG_BETAETIGT | int | linke Taste Lenkradheizung betaetigt ? |
| STAT_U_SG_WERT | real | Betriebsspannung am MFL_SG in Volt |
| STAT_U_SG_EINH | string | Einheit zur Betriebsspannung am MFL_SG in Volt |

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
