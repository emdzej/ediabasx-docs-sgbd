# zcs1_e38.prg

- Jobs: [7](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Instrumenten-Kombination IKE E38 |
| ORIGIN | BMW VK-22 Waegner |
| REVISION | 3.11 |
| AUTHOR | BMW VK-22 Hillebrand, BMW TP-421 Drexel |
| COMMENT | SGBD zur Fahrzeugidentifikation E38, zcs1_e38.b2v |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer IKE
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Default ident job
- [ZCS_GM_LESEN](#job-zcs-gm-lesen)
- [PROD_DATUM_LESEN](#job-prod-datum-lesen)
- [DIAGNOSE_FORTSETZEN](#job-diagnose-fortsetzen) - Fortsetzen der Diagnose
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer IKE

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

<a id="job-diagnose-fortsetzen"></a>
### DIAGNOSE_FORTSETZEN

Fortsetzen der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (24 × 2)
- [ZCS_TEXTE](#table-zcs-texte) (43 × 7)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x02 | OKAY |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_SG_REJECTED |
| 0xB0 | ERROR_SG_PARAMETER |
| 0xB1 | ERROR_SG_FUNCTION |
| 0xFF | ERROR_SG_NACK |
| 0x00 | ERROR_SG_UNBEKANNTES_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 24 rows × 2 columns

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
| 0xXY | unbekannter Hersteller |

<a id="table-zcs-texte"></a>
### ZCS_TEXTE

Dimensions: 43 rows × 7 columns

| GM | TYP | BAUREIHE | MODELL | LA | TAIS | DESRS |
| --- | --- | --- | --- | --- | --- | --- |
| 4001 | GE01 | E38 | 725tds_A_M51_LIM | EUR_LL | X | X |
| 4011 | GE11 | E38 | 728i_M_M52_LIM | EUR_LL | X | X |
| 4021 | GE21 | E38 | 728i_A_M52_LIM | EUR_LL | X | X |
| 4022 | GE22 | E38 | 728i_A_M52_LIM | EUR_RL | X | X |
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
| 4221 | GG21 | E38 | 750i_A_M73_LIM | EUR_LL | X | X |
| 4222 | GG22 | E38 | 750i_A_M73_LIM | EUR_RL | X | X |
| 4321 | GH21 | E38 | 728iL_A_M52_LIM | EUR_LL | X | X |
| 4325 | GH25 | E38 | 728iL_A_M52_LIM | THA_RL | X | X |
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
| xxxx | xxxx | UNBEKANNT | UNBEKANNT | UNBEKANNT | - | - |
