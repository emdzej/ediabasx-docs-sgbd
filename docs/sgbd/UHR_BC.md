# UHR_BC.prg

- Jobs: [7](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Uhr und Bordcomputer E36/5 E36/7 |
| ORIGIN | BMW TP-421 Spoljarec |
| REVISION | 1.05 |
| AUTHOR | BMW TP-421 Spoljarec |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer UHRBC
- [IDENT](#job-ident) - Ident-Daten fuer UhrBC
- [COD_LESEN](#job-cod-lesen) - Auslesen der BC-Codierung
- [STATUS_LESEN](#job-status-lesen) - alle analogen Stati des Uhr-BC 5 lesen
- [RESET_UHR_BC](#job-reset-uhr-bc) - power on Reset Uhr-BC
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode beenden

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

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer UHRBC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer UhrBC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| ID_LIEF_TEXT | string | Lieferantenname |

<a id="job-cod-lesen"></a>
### COD_LESEN

Auslesen der BC-Codierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Ergebnis des Jobs |
| COD_DATEN | binary | 8 Byte Codierdaten nicht dekodiert fixe und variable Codierdaten |
| K_ZAHL | int | Wegeimpulse K-Zahl |
| EINSPRITZKENNZAHL | int | Steigung Einspitzkennlinie im BC (s = sBC*1638400/6144) |
| EINSPRITZSTEIGUNG | long | Einspritzsteigung s (Division durch Zylinderanzahl: -&gt; s') |
| ZEITBASIS | string | 12h/24h-Stundenbasis (nur bei BC-Variante relevant) |
| TEMPERATURBASIS | string | Temperatureinheit C/F |
| WARNTON | string | nit/ohne Warnton |
| GESCHWINDIGKEITSBASIS | string | km/h oder MPH |
| VERBRAUCHSBASIS | string | l/100km MPG km/l |
| REICHWEITENBASIS | string | km oder Meilen |
| UHR_BC | string | Codierung als Uhr oder Uhr/Bc |

<a id="job-status-lesen"></a>
### STATUS_LESEN

alle analogen Stati des Uhr-BC 5 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| STAT_TASTE_UHR_EIN | int | 1 -&gt; Taste UHR gedrueckt |
| STAT_TASTE_SET_RES_EIN | int | 0 -&gt; Taste SET/RES gedrueckt, 1 -&gt; Taste SET/RES gedrueckt |
| STAT_LSS_EIN | int | 0 -&gt; Lenkstockschalter aus, 1 -&gt; LSS gedrueckt |
| STAT_ADC_KL_R | long | Spannung am A/D-Wandler Kl.R in mV |
| STAT_ADC_TEMP | long | Spannung am A/D-Wandler Temperaturgeber in mV |
| STAT_ADC_TANK | long | Spannung am A/D-Wandler Tankgeber in mV |
| STAT_ADC_KL_58G | long | Spannung am A/D-Wandler Kl.58g in mV |
| STAT_TKVA | long | Lowphase T KVA in us |
| STAT_TACHO_A | long | Frequenz Wegsignal in Hz |

<a id="job-reset-uhr-bc"></a>
### RESET_UHR_BC

power on Reset Uhr-BC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Ergebnis des Jobs |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (6 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 6 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xB0 | ERROR_ECU_PARAMETER |
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
