# zcs_e46.prg

- Jobs: [10](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Elektronische Wegfahrsperre - alle Typen |
| ORIGIN | VS-221 Waegner |
| REVISION | 1.07 |
| AUTHOR | TP-421 Huber, Drexel, VK-22 Hillebrand |
| COMMENT | SGBD zur Fahrzeugidentifikation E46, zcs_e46.b2v |
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
- [ZCS_TEXTE](#table-zcs-texte) (198 × 7)

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

Dimensions: 198 rows × 7 columns

| GM | TYP | BAUREIHE | MODELL | LA | TAIS | DESRS |
| --- | --- | --- | --- | --- | --- | --- |
| 6511 | AL11 | E46 | 316i_M43/TU_LIM | EUR_LL | X | X |
| 6512 | AL12 | E46 | 316i_M43/TU_LIM | EUR_RL | X | X |
| 6518 | AL18 | E46 | 318i_M43/TU_LIM | VNM_LL | X | X |
| 6531 | AL31 | E46 | 318i_M43/TU_LIM | EUR_LL | X | X |
| 6532 | AL32 | E46 | 318i_M43/TU_LIM | EUR_RL | X | X |
| 6534 | AL34 | E46 | 318i_M43/TU_LIM | MYS_RL | X | X |
| 6535 | AL35 | E46 | 318i_M43/TU_LIM | THA_RL | X | X |
| 6536 | AL36 | E46 | 318i_M43/TU_LIM | EGY_LL | X | X |
| 6537 | AL37 | E46 | 318i_M43/TU_LIM | IDN_RL | X | X |
| 6539 | AL39 | E46 | 318i_M43/TU_LIM | PHL_LL | X | X |
| 6551 | AL51 | E46 | 316i_M43/TU_LIM | EUR_LL | X | X |
| 6555 | AL55 | E46 | 316i_M43/TU_LIM | PHL_LL | X | X |
| 6771 | AL71 | E46 | 320d_M47_LIM | EUR_LL | X | X |
| 6772 | AL72 | E46 | 320d_M47_LIM | EUR_RL | X | X |
| 6781 | AL91 | E46 | 330d_M57_LIM | EUR_LL | X | X |
| 6782 | AL92 | E46 | 330d_M57_LIM | EUR_RL | X | X |
| 6611 | AM11 | E46 | 320i_M52/TU_LIM | EUR_LL | X | X |
| 6612 | AM12 | E46 | 320i_M52/TU_LIM | EUR_RL | X | X |
| 6631 | AM31 | E46 | 323i_M52/TU_LIM | EUR_LL | X | X |
| 6632 | AM32 | E46 | 323i_M52/TU_LIM | EUR_RL | X | X |
| 6633 | AM33 | E46 | 323i_M52/TU_LIM | USA_LL | X | X |
| 6635 | AM35 | E46 | 323i_M52/TU_LIM | THA_RL | X | X |
| 6636 | AM36 | E46 | 323i_M52/TU_LIM | VNM_LL | X | X |
| 6637 | AM37 | E46 | 323i_M52/TU_LIM | IDN_RL | X | X |
| 6638 | AM38 | E46 | 323i_M52/TU_LIM | MEX_LL | X | X |
| 6639 | AM39 | E46 | 323i_M52/TU_LIM | PHL_LL | X | X |
| 6651 | AM51 | E46 | 328i_M52/TU_LIM | EUR_LL | X | X |
| 6652 | AM52 | E46 | 328i_M52/TU_LIM | EUR_RL | X | X |
| 6653 | AM53 | E46 | 328i_M52/TU_LIM | USA_LL | X | X |
| 6654 | AM54 | E46 | 328i_M52/TU_LIM | MYS_RL | X | X |
| 6657 | AM57 | E46 | 328i_M52/TU_LIM | MEX_LL | X | X |
| 6671 | AN11 | E46 | 320i_M52/TU_LIM | EUR_LL | X | X |
| 6672 | AN12 | E46 | 320i_M52/TU_LIM | EUR_RL | X | X |
| 6661 | AN15 | E46 | 320i_M54_LIM | EUR_LL | X | X |
| 6662 | AN16 | E46 | 320i_M54_LIM | EUR_RL | X | X |
| 66A1 | AN31 | E46 | 323i_M52/TU_LIM | EUR_LL | X | X |
| 66A2 | AN32 | E46 | 323i_M52/TU_LIM | EUR_RL | X | X |
| 66A3 | AN33 | E46 | 323i_M52/TU_LIM | USA_LL | X | X |
| 66B1 | AN35 | E46 | 325i_M54_LIM | EUR_LL | X | X |
| 66B2 | AN36 | E46 | 325i_M54_LIM | EUR_RL | X | X |
| 66B3 | AN37 | E46 | 325i_M54_LIM | USA_LL | X | X |
| 66C1 | AN51 | E46 | 328i_M52/TU_LIM | EUR_LL | X | X |
| 66C2 | AN52 | E46 | 328i_M52/TU_LIM | EUR_RL | X | X |
| 66D1 | AN55 | E46 | 330i_M54_LIM | EUR_LL | X | X |
| 66D2 | AN56 | E46 | 330i_M54_LIM | EUR_RL | X | X |
| 6572 | AN72 | E46 | 316i_M43/TU_LIM | EUR_RL | X | X |
| 6591 | AN91 | E46 | 318i_M43/TU_LIM | EUR_LL | X | X |
| 6592 | AN92 | E46 | 318i_M43/TU_LIM | EUR_RL | X | X |
| 6831 | AP31 | E46 | 318i_M43/TU_TOUR | EUR_LL | X | X |
| 6832 | AP32 | E46 | 318i_M43/TU_TOUR | EUR_RL | X | X |
| 67D1 | AP51 | E46 | 318d_M47_TOUR | EUR_LL | X | X |
| 67A1 | AP71 | E46 | 320d_M47/TU_TOUR | EUR_LL | X | O |
| 67A2 | AP72 | E46 | 320d_M47/TU_TOUR | EUR_RL | X | O |
| 6891 | AP91 | E46 | 330d_M57_TOUR | EUR_LL | X | X |
| 6892 | AP92 | E46 | 330d_M57_TOUR | EUR_RL | X | X |
| 6911 | AR11 | E46 | 320i_M52/TU_TOUR | EUR_LL | X | X |
| 6933 | AR33 | E46 | 323i_M52/TU_TOUR | USA_LL | X | X |
| 6951 | AR51 | E46 | 328i_M52/TU_TOUR | EUR_LL | X | X |
| 6952 | AR52 | E46 | 328i_M52/TU_TOUR | EUR_RL | X | X |
| 67E1 | AS51 | E46 | 318d_M47_LIM | EUR_LL | X | X |
| 67B1 | AS71 | E46 | 320d_M47/TU_LIM | EUR_LL | X | O |
| 67B2 | AS72 | E46 | 320d_M47/TU_LIM | EUR_RL | X | O |
| 6693 | AS93 | E46 | M3_S54_LIM | USA_LL | X | O |
| 6C11 | AT11 | E46 | 318ti_N40_COMP | EUR_LL | X | O |
| 6C21 | AT31 | E46 | 325ti_M54_COMP | EUR_LL | X | O |
| 6C22 | AT32 | E46 | 325ti_M54_COMP | EUR_RL | X | O |
| 6C31 | AT51 | E46 | 318ti_N42_COMP | EUR_LL | X | O |
| 6C32 | AT52 | E46 | 318ti_N42_COMP | EUR_RL | X | O |
| 6C41 | AT71 | E46 | 320td_M47/TU_COMP | EUR_LL | X | O |
| 6C42 | AT72 | E46 | 320td_M47/TU_COMP | EUR_RL | X | O |
| 6C71 | AU51 | E46 | 318ti_N42_COMP | EUR_LL | X | O |
| 6C72 | AU52 | E46 | 318ti_N42_COMP | EUR_RL | X | O |
| 6C61 | AU91 | E46 | 318tii_N44_COMP | EUR_LL | X | O |
| 6621 | AV11 | E46 | 320i_M54_LIM | EUR_LL | X | X |
| 6622 | AV12 | E46 | 320i_M54_LIM | EUR_RL | X | X |
| 6623 | AV13 | E46 | 320i_M54_LIM | USA_LL | X | X |
| 6541 | AV31 | E46 | 325i_M54_LIM | EUR_LL | X | X |
| 6542 | AV32 | E46 | 325i_M54_LIM | EUR_RL | X | X |
| 6543 | AV33 | E46 | 325i_M54_LIM | USA_LL | X | X |
| 6545 | AV35 | E46 | 325i_M54_LIM | MYS_RL | X | X |
| 6546 | AV36 | E46 | 325i_M54_LIM | IDN_RL | X | X |
| 6547 | AV37 | E46 | 325i_M54_LIM | PHL_LL | X | X |
| 6548 | AV38 | E46 | 325i_M54_LIM | VNM_LL | X | X |
| 6549 | AV39 | E46 | 325i_M54_LIM | MEX_LL | X | X |
| 6561 | AV51 | E46 | 330i_M54_LIM | EUR_LL | X | X |
| 6562 | AV52 | E46 | 330i_M54_LIM | EUR_RL | X | X |
| 6563 | AV53 | E46 | 330i_M54_LIM | USA_LL | X | X |
| 6569 | AV59 | E46 | 330i_M54_LIM | MEX_LL | X | X |
| 6722 | AV72 | E46 | 320d_M47_LIM | EUR_RL | X | X |
| 6921 | AW11 | E46 | 320i_M54_TOUR | EUR_LL | X | X |
| 6922 | AW12 | E46 | 320i_M54_TOUR | EUR_RL | X | X |
| 6971 | AW31 | E46 | 325i_M54_TOUR | EUR_LL | X | X |
| 6972 | AW32 | E46 | 325i_M54_TOUR | EUR_RL | X | X |
| 6973 | AW33 | E46 | 325i_M54_TOUR | USA_LL | X | X |
| 6981 | AW51 | E46 | 330i_M54_TOUR | EUR_LL | X | X |
| 6982 | AW52 | E46 | 330i_M54_TOUR | EUR_RL | X | X |
| 6851 | AX51 | E46 | 318i_N42_TOUR | EUR_LL | X | O |
| 6852 | AX52 | E46 | 318i_N42_TOUR | EUR_RL | X | O |
| 67C1 | AX71 | E46 | 320d_M47_TOUR | EUR_LL | X | X |
| 67C2 | AX72 | E46 | 320d_M47_TOUR | EUR_RL | X | X |
| 6521 | AY11 | E46 | 316i_N40_LIM | EUR_LL | X | O |
| 6525 | AY15 | E46 | 316i_N40_LIM | PHL_LL | X | O |
| 6526 | AY16 | E46 | 316i_N40_LIM | EGY_LL | X | O |
| 6581 | AY31 | E46 | 316i_N42_LIM | EUR_LL | X | O |
| 6582 | AY32 | E46 | 316i_N42_LIM | EUR_RL | X | O |
| 65B1 | AY71 | E46 | 318i_N42_LIM | EUR_LL | X | O |
| 65B2 | AY72 | E46 | 318i_N42_LIM | EUR_RL | X | O |
| 65B4 | AY74 | E46 | 318i_N42_LIM | MYS_RL | X | O |
| 65B5 | AY75 | E46 | 318i_N42_LIM | THA_RL | X | O |
| 65B6 | AY76 | E46 | 318i_N42_LIM | EGY_LL | X | O |
| 65B7 | AY77 | E46 | 318i_N42_LIM | IDN_RL | X | O |
| 65B8 | AY78 | E46 | 318i_N42_LIM | VNM_LL | X | O |
| 65B9 | AY79 | E46 | 318i_N42_LIM | PHL_LL | X | O |
| 67F2 | AZ12 | E46 | 320d_M47/TU_LIM | EUR_RL | X | O |
| 6031 | BL31 | E46 | 318Ci_M43/TU_COUPE | EUR_LL | X | X |
| 6032 | BL32 | E46 | 318Ci_M43/TU_COUPE | EUR_RL | X | X |
| 6051 | BL51 | E46 | 316Ci_M43/TU_COUPE | EUR_LL | X | X |
| 6191 | BL91 | E46 | M3_S54_COUPE | EUR_LL | X | X |
| 6192 | BL92 | E46 | M3_S54_COUPE | EUR_RL | X | X |
| 6193 | BL93 | E46 | M3_S54_COUPE | USA_LL | X | X |
| 6111 | BM11 | E46 | 320Ci_M52/TU_COUPE | EUR_LL | X | X |
| 6131 | BM31 | E46 | 323Ci_M52/TU_COUPE | EUR_LL | X | X |
| 6132 | BM32 | E46 | 323Ci_M52/TU_COUPE | EUR_RL | X | X |
| 6133 | BM33 | E46 | 323Ci_M52/TU_COUPE | USA_LL | X | X |
| 6151 | BM51 | E46 | 328Ci_M52/TU_COUPE | EUR_LL | X | X |
| 6152 | BM52 | E46 | 328Ci_M52/TU_COUPE | EUR_RL | X | X |
| 6153 | BM53 | E46 | 328Ci_M52/TU_COUPE | USA_LL | X | X |
| 6071 | BM71 | E46 | 316Ci_N40_COUPE | EUR_LL | X | O |
| 6121 | BN11 | E46 | 320Ci_M54_COUPE | EUR_LL | X | X |
| 6122 | BN12 | E46 | 320Ci_M54_COUPE | EUR_RL | X | X |
| 6141 | BN31 | E46 | 325Ci_M54_COUPE | EUR_LL | X | X |
| 6142 | BN32 | E46 | 325Ci_M54_COUPE | EUR_RL | X | X |
| 6143 | BN33 | E46 | 325Ci_M54_COUPE | USA_LL | X | X |
| 6161 | BN51 | E46 | 330Ci_M54_COUPE | EUR_LL | X | X |
| 6162 | BN52 | E46 | 330Ci_M54_COUPE | EUR_RL | X | X |
| 6163 | BN53 | E46 | 330Ci_M54_COUPE | USA_LL | X | X |
| 6331 | BP71 | E46 | 318Ci_N42_CABRIO | EUR_LL | X | O |
| 6332 | BP72 | E46 | 318Ci_N42_CABRIO | EUR_RL | X | O |
| 6431 | BR31 | E46 | 323Ci_M52/TU_CABRIO | EUR_LL | X | X |
| 6432 | BR32 | E46 | 323Ci_M52/TU_CABRIO | EUR_RL | X | X |
| 6433 | BR33 | E46 | 323Ci_M52/TU_CABRIO | USA_LL | X | X |
| 6491 | BR91 | E46 | M3_S54_CABRIO | EUR_LL | X | X |
| 6492 | BR92 | E46 | M3_S54_CABRIO | EUR_RL | X | O |
| 6493 | BR93 | E46 | M3_S54_CABRIO | USA_LL | X | X |
| 6421 | BS11 | E46 | 320Ci_M54_CABRIO | EUR_LL | X | X |
| 6422 | BS12 | E46 | 320Ci_M54_CABRIO | EUR_RL | X | X |
| 6441 | BS31 | E46 | 325Ci_M54_CABRIO | EUR_LL | X | X |
| 6442 | BS32 | E46 | 325Ci_M54_CABRIO | EUR_RL | X | X |
| 6443 | BS33 | E46 | 325Ci_M54_CABRIO | USA_LL | X | X |
| 6461 | BS51 | E46 | 330Ci_M54_CABRIO | EUR_LL | X | X |
| 6462 | BS52 | E46 | 330Ci_M54_CABRIO | EUR_RL | X | X |
| 6463 | BS53 | E46 | 330Ci_M54_CABRIO | USA_LL | X | X |
| 6081 | BV71 | E46 | 318Ci_N42_COUPE | EUR_LL | X | O |
| 6082 | BV72 | E46 | 318Ci_N42_COUPE | EUR_RL | X | O |
| 67D1 | EL51 | E46 | 318d_M47_TOUR | EUR_LL | X | X |
| 6891 | EL91 | E46 | 330d_M57_TOUR | EUR_LL | X | X |
| 6892 | EL92 | E46 | 330d_M57_TOUR | EUR_RL | X | X |
| 6911 | EM11 | E46 | 320i_M52/TU_TOUR | EUR_LL | X | X |
| 6921 | EN11 | E46 | 320i_M54_TOUR | EUR_LL | X | X |
| 6922 | EN12 | E46 | 320i_M54_TOUR | EUR_RL | X | X |
| 6971 | EN31 | E46 | 325i_M54_TOUR | EUR_LL | X | X |
| 6972 | EN32 | E46 | 325i_M54_TOUR | EUR_RL | X | X |
| 6973 | EN33 | E46 | 325i_M54_TOUR | USA_LL | X | X |
| 6981 | EN51 | E46 | 330i_M54_TOUR | EUR_LL | X | X |
| 6982 | EN52 | E46 | 330i_M54_TOUR | EUR_RL | X | X |
| 6511 | ER11 | E46 | 316i_M43/TU_LIM | EUR_LL | X | X |
| 6512 | ER12 | E46 | 316i_M43/TU_LIM | EUR_RL | X | X |
| 6551 | ER51 | E46 | 316i_M43/TU_LIM | EUR_LL | X | X |
| 6555 | ER55 | E46 | 316i_M43/TU_LIM | PHL_LL | X | X |
| 6781 | ER91 | E46 | 330d_M57_LIM | EUR_LL | X | X |
| 6782 | ER92 | E46 | 330d_M57_LIM | EUR_RL | X | X |
| 6611 | ES11 | E46 | 320i_M52/TU_LIM | EUR_LL | X | X |
| 6635 | ES35 | E46 | 323i_M52/TU_LIM | THA_RL | X | X |
| 6671 | ET11 | E46 | 320i_M52/TU_LIM | EUR_LL | X | X |
| 6661 | ET15 | E46 | 320i_M54_LIM | EUR_LL | X | X |
| 6662 | ET16 | E46 | 320i_M54_LIM | EUR_RL | X | X |
| 66B1 | ET35 | E46 | 325i_M54_LIM | EUR_LL | X | X |
| 66B2 | ET36 | E46 | 325i_M54_LIM | EUR_RL | X | X |
| 66B3 | ET37 | E46 | 325i_M54_LIM | USA_LL | X | X |
| 66D1 | ET55 | E46 | 330i_M54_LIM | EUR_LL | X | X |
| 66D2 | ET56 | E46 | 330i_M54_LIM | EUR_RL | X | X |
| 67E1 | EU51 | E46 | 318d_M47_LIM | EUR_LL | X | X |
| 6621 | EV11 | E46 | 320i_M54_LIM | EUR_LL | X | X |
| 6622 | EV12 | E46 | 320i_M54_LIM | EUR_RL | X | X |
| 6623 | EV13 | E46 | 320i_M54_LIM | USA_LL | X | X |
| 6541 | EV31 | E46 | 325i_M54_LIM | EUR_LL | X | X |
| 6542 | EV32 | E46 | 325i_M54_LIM | EUR_RL | X | X |
| 6543 | EV33 | E46 | 325i_M54_LIM | USA_LL | X | X |
| 6545 | EV35 | E46 | 325i_M54_LIM | MYS_RL | X | X |
| 6546 | EV36 | E46 | 325i_M54_LIM | IDN_RL | X | X |
| 6547 | EV37 | E46 | 325i_M54_LIM | PHL_LL | X | X |
| 6548 | EV38 | E46 | 325i_M54_LIM | VNM_LL | X | X |
| 6549 | EV39 | E46 | 325i_M54_LIM | MEX_LL | X | X |
| 6561 | EV51 | E46 | 330i_M54_LIM | EUR_LL | X | X |
| 6562 | EV52 | E46 | 330i_M54_LIM | EUR_RL | X | X |
| 6563 | EV53 | E46 | 330i_M54_LIM | USA_LL | X | X |
| 6569 | EV59 | E46 | 330i_M54_LIM | MEX_LL | X | X |
| xxxx | xxxx | UNBEKANNT | UNBEKANNT | UNBEKANNT | - | - |
