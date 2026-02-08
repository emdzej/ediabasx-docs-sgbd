# C_RADIO.prg

- Jobs: [10](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Radio C4X |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 1.03 |
| AUTHOR | BMW TP-421 Spoljarec, BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer das Radio
- [IDENT](#job-ident) - Ident-Daten fuer das Radio
- [STATUS_LESEN](#job-status-lesen) - alle Stati des RADIO lesen
- [STEUERN_RADIO_POWER](#job-steuern-radio-power) - Ein-/Ausschalten des Radios
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben des Pruefstempels mit der FG-Nummer
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

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

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer das Radio

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer das Radio

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
| ID_GERAETE_NAME | string | Entwicklungsbezeichnung des Radios ohne Unterstrich |
| ID_RADIO_NAME | string | Entwicklungsbezeichnung des Radios mit Unterstrich |
| ID_TASTE_DIAG | string | auslesen des Tastaturstatus moeglich |
| ID_SUCHSCHWELLE_DIAG | string | auslesen des Suchlaufschwellenstatus moeglich |
| ID_VF_DIAG | string | auslesen des VF-Status moeglich |
| ID_AN_AUS_DIAG | string | auslesen ob Radio ein aus moeglich |

<a id="job-status-lesen"></a>
### STATUS_LESEN

alle Stati des RADIO lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| STAT_RADIO_TASTE_BETAETIGT | int | 0 -&gt; keine Taste betaetigt, 1 -&gt; bel. Taste betaetigt !! Achtung: bei Bordmonitorvarianten immer result=0 ! mit "Radio aus" nur Dummyergebnis ! |
| STAT_TELEFON_MUTE_AKTIV | int | 0 -&gt; Mute inaktiv, 1 -&gt; Mute aktiv ! mit "Radio aus" nur Dummyergebnis ! |
| STAT_GAL_KURVE | int | Gal-Kurve 1,2,3,4 eingestellt (auch mit "Radio aus" moeglich) |
| STAT_SEEK_SCHWELLE | int | Suchlaufschwelle 1:empfindlich oder 2:unempfindlich !! Achtung: bei nicht ECE-Varianten result immer=1 (auch mit "Radio aus" moeglich) |
| STAT_MIT_DSP | int | DSP verbaut oder nicht verbaut (auch mit Radio aus" moeglich) |
| STAT_VF_LAUT_WERT | int | Zahlenwert der VF-Lautstaerke (inkl. Vorzeichen) !! Achtung: bei nicht ECE-Varianten result = -0 ! mit "Radio aus" nur Dummyergebnis |
| STAT_GAL_GESCHW_WERT | int | Zahlenwert Geschw.-abhaengige Lautstaerkenregelung-Frequenz ! mit "Radio aus" nur Dummyergebnis ! Unterschiedliche Behandlung bei ZIS und BM-Varianten ! |
| STAT_GAL_GESCHW_EINH | string | Einheit der GAL-Geschwindigkeit (Km/h) |
| STAT_FELDSTAERKE_WERT | int | FELDSTAERKE des empf. Senders (relativ, 0-15) ! mit "Radio aus" nur Dummyergebnis |
| STAT_RADIO_EIN | int | 1: Radio ist eingeschaltet 0: Radio ist ausgeschaltet bei ausgeschaltetem Radio ist keine DSP-Diagnose moeglich |

<a id="job-steuern-radio-power"></a>
### STEUERN_RADIO_POWER

Ein-/Ausschalten des Radios

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | EIN/AUS,ON/OFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen des Pruefstempels und Interpretation als FG-Nummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Beschreiben des Pruefstempels mit der FG-Nummer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Ergebnis ist immer OKAY, da nur Dummy |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (31 × 2)
- [DIAGINDEX](#table-diagindex) (67 × 7)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 31 rows × 2 columns

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
| 0x29 | DENSO |
| 0x30 | NEC |
| 0xFF | unbekannter Hersteller |

<a id="table-diagindex"></a>
### DIAGINDEX

Dimensions: 67 rows × 7 columns

| DIAG_NR | RADIO_NAME | RADIO_NAME_NEU | TASTE | SUCHSCHWELLE | VF | AN_AUS |
| --- | --- | --- | --- | --- | --- | --- |
| 0x00 | C23 MID ECE | C23_MID_ECE | 1 | 1 | 1 | 1 |
| 0x01 | C23 BM ECE | C23_BM_ECE | 0 | 1 | 1 | 1 |
| 0x02 | C23 MID US | C23_MID_US | 1 | 0 | 0 | 1 |
| 0x03 | C23 BM JPN | C23_BM_JPN | 0 | 0 | 0 | 1 |
| 0x04 | C33 JPN | C33_JPN | 1 | 0 | 0 | 0 |
| 0x05 | C23 BM OCN | C23_BM_OCN | 0 | 0 | 0 | 1 |
| 0x07 | CD23 | CD23 | 1 | 1 | 1 | 1 |
| 0x08 | C24 DIN | C24_DIN | 1 | 1 | 1 | 1 |
| 0x09 | C24 MID | C24_MID | 1 | 1 | 1 | 1 |
| 0x0A | C34 | C34 | 1 | 1 | 1 | 0 |
| 0x0B | C32 | C32 | 1 | 1 | 1 | 0 |
| 0x0C | CD33 | CD33 | 1 | 1 | 1 | 0 |
| 0x0D | C33 ECE | C33_ECE | 1 | 1 | 1 | 0 |
| 0x0E | C33 US | C33_US | 1 | 0 | 0 | 0 |
| 0x0F | C33 OCN | C33_OCN | 1 | 0 | 0 | 0 |
| 0x10 | C43 ECE | C43_ECE | 1 | 1 | 1 | 0 |
| 0x11 | CD43 | CD43 | 1 | 1 | 1 | 0 |
| 0x12 | C43 USA | C43_USA | 1 | 0 | 0 | 0 |
| 0x13 | C43 JPN | C43_JPN | 1 | 0 | 0 | 0 |
| 0x14 | C43 OCN | C43_OCN | 1 | 0 | 0 | 0 |
| 0x15 | C44 | C44 | 1 | 1 | 1 | 0 |
| 0x16 | C24 BM | C24_BM | 1 | 1 | 1 | 1 |
| 0x17 | C42 | C42 | 1 | 1 | 1 | 0 |
| 0x18 | C42R-RD1 Euro | C42R-RD1_Euro | 1 | 1 | 1 | 0 |
| 0x19 | RC42-Tempest US | RC42-Tempest_US | 1 | 1 | 0 | 0 |
| 0x1A | RD42-Tempest Ja | RD42-Tempest_Ja | 1 | 1 | 0 | 0 |
| 0x1B | RC43-RD1 Jap | RC43-RD1_Jap | 1 | 1 | 0 | 0 |
| 0x1C | RC43-RD1 Euro | RC43-RD1_Euro | 1 | 1 | 1 | 0 |
| 0x1D | RC43-Tempest US | RC43-Tempest_US | 1 | 1 | 0 | 0 |
| 0x1E | RC43-Tempest Ja | RC43-Tempest_Ja | 1 | 1 | 0 | 0 |
| 0x1F | RC43-Tempest Eu | RC43-Tempest_Eu | 1 | 1 | 1 | 0 |
| 0x20 | RC43-38a Euro | RC43-38a_Euro | 1 | 1 | 1 | 0 |
| 0x21 | RC43-38a US | RC43-38a_US | 1 | 1 | 0 | 0 |
| 0x22 | RC43-38a Jap | RC43-38a_Jap | 1 | 1 | 0 | 0 |
| 0x23 | C43 US E38 | C43_US_E38 | 1 | 1 | 0 | 0 |
| 0x24 | C43 US E39 | C43_US_E39 | 1 | 1 | 0 | 0 |
| 0x25 | C43 US BM | C43_US_BM | 1 | 1 | 0 | 0 |
| 0x26 | CD43 E39 | CD43_E39 | 1 | 1 | 1 | 0 |
| 0x27 | C42 R50 | C42_R50 | 1 | 1 | 1 | 1 |
| 0x28 | C53 MID L30 | C53_MID_L30 | 1 | 1 | 1 | 1 |
| 0x29 | CD53 L30 | CD53_L30 | 1 | 1 | 1 | 1 |
| 0x2A | MD53 L30 | MD53_L30 | 1 | 1 | 1 | 1 |
| 0x2B | CD54 L30 | CD54_L30 | 1 | 1 | 1 | 1 |
| 0x2C | CD54 E39 | CD54_E39 | 1 | 1 | 1 | 1 |
| 0x2D | CD54 E46 | CD54_E46 | 1 | 1 | 1 | 1 |
| 0x2E | C53 R50 | C53_R50 | 1 | 1 | 1 | 1 |
| 0x2F | CD53 R50 | CD53_R50 | 1 | 1 | 1 | 1 |
| 0x30 | MD53 R50 | MD53_R50 | 1 | 1 | 1 | 1 |
| 0x31 | C53 MID E39 | C53_MID_E39 | 1 | 1 | 1 | 1 |
| 0x32 | BM53 E39 | BM53 | 1 | 1 | 1 | 1 |
| 0x33 | C53 E46 | C53_E46 | 1 | 1 | 1 | 1 |
| 0x34 | MD53 E46 | MD53_E46 | 1 | 1 | 1 | 1 |
| 0x35 | CD53 E46 | CD53_E46 | 1 | 1 | 1 | 1 |
| 0x36 | CD53 E39 | CD53_E39 | 1 | 1 | 1 | 1 |
| 0x37 | MD53 E39 | MD53_E39 | 1 | 1 | 1 | 1 |
| 0x39 | BM54 | BM54 | 1 | 1 | 1 | 1 |
| 0x3A | C53 MIR E46 | C53_MIR_E46 | 1 | 1 | 1 | 1 |
| 0x3B | MIR E52 | MIR_E52 | 1 | 1 | 1 | 1 |
| 0x3C | C33B E39 CKD | C33B_E39_CKD | 1 | 1 | 1 | 1 |
| 0x3D | C33B E46 CKD | C33B_E46_CKD | 1 | 1 | 1 | 1 |
| 0x3E | BM24 MMC | BM24_MMC | 1 | 1 | 1 | 1 |
| 0x3F | C52 E39 | C52_E39 | 1 | 1 | 1 | 1 |
| 0x40 | C52 E53 | C52_E53 | 1 | 1 | 1 | 1 |
| 0x41 | C53 E39 | C53_E39 | 1 | 1 | 1 | 1 |
| 0x42 | C53 E53 | C53_E53 | 1 | 1 | 1 | 1 |
| 0x43 | MIR E85 | MIR_E85 | 1 | 1 | 1 | 1 |
| 0xFF | unknown kind of radio | unknown kind of radio | 0 | 0 | 0 | 0 |
