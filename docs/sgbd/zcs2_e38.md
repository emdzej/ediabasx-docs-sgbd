# zcs2_e38.prg

- Jobs: [10](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Elektronische Wegfahrsperre - alle Typen |
| ORIGIN | BMW VS-221 Waegner |
| REVISION | 3.06 |
| AUTHOR | BMW MK-4 Hillebrand, BMW TP-421 Drexel |
| COMMENT | SGBD zur Fahrzeugidentifikation E38, zcs2_e38.b2v |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer EWS automatischer Aufruf beim ersten Zugriff auf SGBD
- [INFO](#job-info) - Info fuer Anwender
- [IDENT](#job-ident) - Ident-Daten fuer EWS
- [ZCS_GM_LESEN](#job-zcs-gm-lesen)
- [PROD_DATUM_LESEN](#job-prod-datum-lesen)
- [FGNR_LESEN](#job-fgnr-lesen) - Auslesen der Fahrgestellnummer aus der EWS
- [AIF_ZCS_LESEN](#job-aif-zcs-lesen) - Auslesen des Zentralen Codierschluessels aus KD-Daten
- [KD_DATEN_LESEN](#job-kd-daten-lesen) - Auslesen der Kundendienstdaten aus der EWS
- [DIAGNOSE_FORTSETZEN](#job-diagnose-fortsetzen) - Diagnose mit EWS aufrecht erhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer EWS automatischer Aufruf beim ersten Zugriff auf SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-info"></a>
### INFO

Info fuer Anwender

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergerat im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch / english |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | int | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-zcs-gm-lesen"></a>
### ZCS_GM_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| TYP_TXT | string | Typschluessel |
| BR_TXT | string | Baureihe |
| MO_TXT | string | Modell |
| LA_TXT | string | Laenderausfuehrung mit Typschluessel |

<a id="job-prod-datum-lesen"></a>
### PROD_DATUM_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| TAG_TXT | string |  |
| TAG_DEC | int |  |
| MONAT_TXT | string |  |
| MONAT_DEC | int |  |
| JAHR_TXT | string |  |
| JAHR_DEC | int |  |

<a id="job-fgnr-lesen"></a>
### FGNR_LESEN

Auslesen der Fahrgestellnummer aus der EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-aif-zcs-lesen"></a>
### AIF_ZCS_LESEN

Auslesen des Zentralen Codierschluessels aus KD-Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| GM | string | Zentralcode C1 - Grundmerkmal |
| SA | string | Zentralcode C2 - Sonderausstattung |
| VM | string | Zentralcode C3 - Versionsmerkmal |
| _TEL_ANTWORT1 | binary |  |
| _TEL_ANTWORT2 | binary |  |

<a id="job-kd-daten-lesen"></a>
### KD_DATEN_LESEN

Auslesen der Kundendienstdaten aus der EWS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | int | 0 bis 11 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| KD_BLOCK | int | 0 bis 11 |
| KD_DATEN | binary | 16 Byte |
| KD_DATEN_TEXT | string | 16 Byte |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnose-fortsetzen"></a>
### DIAGNOSE_FORTSETZEN

Diagnose mit EWS aufrecht erhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [LIEFERANTEN](#table-lieferanten) (24 × 2)
- [ZCS_TEXTE](#table-zcs-texte) (75 × 7)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_SG_REJECTED |
| 0xB0 | ERROR_SG_PARAMETER |
| 0xB1 | ERROR_SG_FUNKTION |
| 0xFF | ERROR_SG_NACK |
| 0x00 | ERROR_SG_UNBEKANNTES_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 24 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
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
| 0xXY | unbekannter Hersteller |

<a id="table-zcs-texte"></a>
### ZCS_TEXTE

Dimensions: 75 rows × 7 columns

| GM | TYP | BAUREIHE | MODELL | LA | TAIS | DESRS |
| --- | --- | --- | --- | --- | --- | --- |
| 4001 | GE01 | E38 | 725tds_A_M51_LIM | EUR_LL | X | X |
| 4011 | GE11 | E38 | 728i_M_M52_LIM | EUR_LL | X | X |
| 4021 | GE21 | E38 | 728i_A_M52_LIM | EUR_LL | X | X |
| 4022 | GE22 | E38 | 728i_A_M52_LIM | EUR_RL | X | X |
| 4031 | GE31 | E38 | 728i_M_M52/TU_LIM | EUR_LL | X | X |
| 4041 | GE41 | E38 | 728i_A_M52/TU_LIM | EUR_LL | X | X |
| 4042 | GE42 | E38 | 728i_A_M52/TU_LIM | EUR_RL | X | X |
| 4061 | GE61 | E38 | 730d_A_M57_LIM | EUR_LL | X | X |
| 4081 | GE81 | E38 | 740d_A_M67_LIM | EUR_LL | X | X |
| 4091 | GE91 | E38 | 725tds_M_M51_LIM | EUR_LL | X | X |
| 4111 | GF11 | E38 | 730i_M_M60/1_LIM | EUR_LL | X | X |
| 4121 | GF21 | E38 | 730i_A_M60/1_LIM | EUR_LL | X | X |
| 4122 | GF22 | E38 | 730i_A_M60/1_LIM | EUR_RL | X | X |
| 4125 | GF25 | E38 | 730i_A_M60/1_LIM | THA_RL | X | X |
| 4131 | GF31 | E38 | 735i_M_M62_LIM | EUR_LL | X | X |
| 4141 | GF41 | E38 | 735i_A_M62_LIM | EUR_LL | X | X |
| 4142 | GF42 | E38 | 735i_A_M62_LIM | EUR_RL | X | X |
| 4151 | GF51 | E38 | 740i_M_M60/2_LIM | EUR_LL | X | X |
| 4161 | GF61 | E38 | 740i_A_M60/2_LIM | EUR_LL | X | X |
| 4162 | GF62 | E38 | 740i_A_M60/2_LIM | EUR_RL | X | X |
| 4163 | GF63 | E38 | 740i_A_M60/2_LIM | USA_LL | X | X |
| 4171 | GF71 | E38 | 740i_M_M62_LIM | EUR_LL | X | X |
| 4181 | GF81 | E38 | 740i_A_M62_LIM | EUR_LL | X | X |
| 4182 | GF82 | E38 | 740i_A_M62_LIM | EUR_RL | X | X |
| 4183 | GF83 | E38 | 740i_A_M62_LIM | USA_LL | X | X |
| 4201 | GG01 | E38 | 750i_A_M73/TU_LIM | EUR_LL | X | X |
| 4202 | GG02 | E38 | 750i_A_M73/TU_LIM | EUR_RL | X | X |
| 4221 | GG21 | E38 | 750i_A_M73_LIM | EUR_LL | X | X |
| 4222 | GG22 | E38 | 750i_A_M73_LIM | EUR_RL | X | X |
| 4241 | GG41 | E38 | 735i_A_M62/TU_LIM | EUR_LL | X | X |
| 4242 | GG42 | E38 | 735i_A_M62/TU_LIM | EUR_RL | X | X |
| 4281 | GG81 | E38 | 740i_A_M62/TU_LIM | EUR_LL | X | X |
| 4282 | GG82 | E38 | 740i_A_M62/TU_LIM | EUR_RL | X | X |
| 4283 | GG83 | E38 | 740i_A_M62/TU_LIM | USA_LL | X | X |
| 4301 | GH01 | E38 | 740iL_A_M62/TU_LIM_PL | EUR_LL | X | X |
| 4303 | GH03 | E38 | 740iL_A_M62/TU_LIM_PL | USA_LL | X | X |
| 4321 | GH21 | E38 | 728iL_A_M52_LIM | EUR_LL | X | X |
| 4325 | GH25 | E38 | 728iL_A_M52_LIM | THA_RL | X | X |
| 4341 | GH41 | E38 | 728iL_A_M52/TU_LIM | EUR_LL | X | X |
| 4345 | GH45 | E38 | 728iL_A_M52/TU_LIM | THA_RL | X | X |
| 4361 | GH61 | E38 | 735iL_A_M62/TU_LIM | EUR_LL | X | X |
| 4362 | GH62 | E38 | 735iL_A_M62/TU_LIM | EUR_RL | X | X |
| 4367 | GH67 | E38 | 735iL_A_M62/TU_LIM | IDN_RL | X | X |
| 4381 | GH81 | E38 | 740iL_A_M62/TU_LIM | EUR_LL | X | X |
| 4382 | GH82 | E38 | 740iL_A_M62/TU_LIM | EUR_RL | X | X |
| 4383 | GH83 | E38 | 740iL_A_M62/TU_LIM | USA_LL | X | X |
| 4385 | GH85 | E38 | 740iL_A_M62/TU_LIM | THA_RL | X | X |
| 4401 | GJ01 | E38 | 750iL_A_M73/TU_LIM | EUR_LL | X | X |
| 4402 | GJ02 | E38 | 750iL_A_M73/TU_LIM | EUR_RL | X | X |
| 4403 | GJ03 | E38 | 750iL_A_M73/TU_LIM | USA_LL | X | X |
| 4411 | GJ11 | E38 | 730iL_M_M60/1_LIM | EUR_LL | X | X |
| 4421 | GJ21 | E38 | 730iL_A_M60/1_LIM | EUR_LL | X | X |
| 4422 | GJ22 | E38 | 730iL_A_M60/1_LIM | EUR_RL | X | X |
| 4427 | GJ27 | E38 | 730iL_A_M60/1_LIM | IDN_RL | X | X |
| 4441 | GJ41 | E38 | 735iL_A_M62_LIM | EUR_LL | X | X |
| 4442 | GJ42 | E38 | 735iL_A_M62_LIM | EUR_RL | X | X |
| 4447 | GJ47 | E38 | 735iL_A_M62_LIM | IDN_RL | X | X |
| 4461 | GJ61 | E38 | 740iL_A_M60/2_LIM | EUR_LL | X | X |
| 4462 | GJ62 | E38 | 740iL_A_M60/2_LIM | EUR_RL | X | X |
| 4463 | GJ63 | E38 | 740iL_A_M60/2_LIM | USA_LL | X | X |
| 4481 | GJ81 | E38 | 740iL_A_M62_LIM | EUR_LL | X | X |
| 4482 | GJ82 | E38 | 740iL_A_M62_LIM | EUR_RL | X | X |
| 4483 | GJ83 | E38 | 740iL_A_M62_LIM | USA_LL | X | X |
| 4485 | GJ85 | E38 | 740iL_A_M62_LIM | THA_RL | X | X |
| 4487 | GJ87 | E38 | 740iL_A_M62_LIM | MEX_LL | X | X |
| 4521 | GK21 | E38 | 750iL_A_M73_LIM | EUR_LL | X | X |
| 4522 | GK22 | E38 | 750iL_A_M73_LIM | EUR_RL | X | X |
| 4523 | GK23 | E38 | 750iL_A_M73_LIM | USA_LL | X | X |
| 4561 | GK61 | E38 | 750iXL_A_M73_LIM | EUR_LL | X | X |
| 4562 | GK62 | E38 | 750iXL_A_M73_LIM | EUR_RL | X | X |
| 4581 | GK81 | E38 | 750iXL_A_M73/TU_LIM | EUR_LL | X | X |
| 4582 | GK82 | E38 | 750iXL_A_M73/TU_LIM | EUR_RL | X | X |
| 4591 | GK91 | E38 | 750iL_A_M73/TU_LIM_PL | EUR_LL | X | X |
| 4593 | GK93 | E38 | 750iL_A_M73/TU_LIM_PL | USA_LL | X | X |
| xxxx | xxxx | UNBEKANNT | UNBEKANNT | UNBEKANNT | - | - |
