# SBE2.prg

- Jobs: [23](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | SBE2 |
| ORIGIN | BMW TI-433 Winkler H.-J. |
| REVISION | 1.00 |
| AUTHOR | BMW TI-433 Winkler |
| COMMENT | Sitzbelegungserkennung 2 |
| PACKAGE | 1.24 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer AIRBAG MRS3
- [IDENT](#job-ident) - Ident-Daten fuer SBE2
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Quicktest auf Fehleranzahl
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [KODIERDATEN_LESEN](#job-kodierdaten-lesen) - Kodierdaten lesen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [SG_RESET](#job-sg-reset) - Ausloesen des Controller-Reset
- [STATUS_KAP_CE](#job-status-kap-ce) - CE-Kapazitaet (Elektrode-Masse) Antennen
- [STATUS_PHI_CE](#job-status-phi-ce) - CE-Phasen (Elektrode-Masse) Antennen
- [STATUS_KAP_CGE](#job-status-kap-cge) - CGE-Kapazitaet (Elektrode-Guard) Antennen
- [STATUS_PHI_CGE](#job-status-phi-cge) - CGE-Phasen (Elektrode-Guard) Antennen
- [STATUS_IO](#job-status-io) - IO-Stati ausgeben
- [STATUS_INTERN](#job-status-intern) - Interne IO-Stati ausgeben
- [STEUERN_DSP](#job-steuern-dsp) - (Temporaeres) Setzen der DSP-Bytes
- [STEUERN_SBE2](#job-steuern-sbe2) - (Temporaeres) Setzen der Sitzbelegung
- [STEUERN_OCE](#job-steuern-oce) - (Temporaeres) Ein-/Ausschalten der OCE-Kommunikation
- [HERSTELLERDATEN_LESEN](#job-herstellerdaten-lesen) - Lesen der herstellerspez. Daten
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Diagnose aufrechterhalten
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

Init-Job fuer AIRBAG MRS3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer SBE2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferant |
| ID_SW_NR | int | Softwarenummer |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Quicktest auf Fehleranzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ANZ | int | Anzahl Fehler |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_HEX_CODE | binary | Hex-Fehlerdaten je Fehler |
| F_ORT_NR | int | identisch Fehlerbytemaske |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl Fehlerarten, hier: 0 |
| F_UW_ANZ | int | Anzahl Umweltbedingungen, hier: 0 |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | long | Speicheradresse Bereich: 0x0000-0xFFFF |
| ANZAHL | int | Anzahl der Daten Bereich: 1 bis 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| DATEN | binary | ausgelesene Hex-Daten |

<a id="job-kodierdaten-lesen"></a>
### KODIERDATEN_LESEN

Kodierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Speicheradresse Bereich: 0x00-0x3F |
| ANZAHL | int | Anzahl der Daten Bereich: 1 bis 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| DATEN | binary | ausgelesene Hex-Daten |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| BYTE1 | int | Datenbyte 1 |
| BYTE2 | int | Datenbyte 2 |
| BYTE3 | int | Datenbyte 3 |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-sg-reset"></a>
### SG_RESET

Ausloesen des Controller-Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-status-kap-ce"></a>
### STATUS_KAP_CE

CE-Kapazitaet (Elektrode-Masse) Antennen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_KAP_CE_C1 | real | Antenne C1, CE-Kapazitaet in pF |
| STAT_KAP_CE_C2 | real | Antenne C2, CE-Kapazitaet in pF |
| STAT_KAP_CE_C3 | real | Antenne C3, CE-Kapazitaet in pF |
| STAT_KAP_CE_C4 | real | Antenne C4, Kapazitaet in pF |
| STAT_DSP_DATA_ID | int | intern |

<a id="job-status-phi-ce"></a>
### STATUS_PHI_CE

CE-Phasen (Elektrode-Masse) Antennen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_PHI_CE_C1 | real | Antenne C1, CE-Phase in Grad |
| STAT_PHI_CE_C2 | real | Antenne C2, CE-Phase in Grad |
| STAT_PHI_CE_C3 | real | Antenne C3, CE-Phase in Grad |
| STAT_PHI_CE_C4 | real | Antenne C4, CE-Phase in Grad |
| STAT_DSP_DATA_ID | int | intern |

<a id="job-status-kap-cge"></a>
### STATUS_KAP_CGE

CGE-Kapazitaet (Elektrode-Guard) Antennen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_KAP_CGE_C1 | real | Antenne C1, CGE-Kapazitaet in pF |
| STAT_KAP_CGE_C2 | real | Antenne C2, CGE-Kapazitaet in pF |
| STAT_KAP_CGE_C3 | real | Antenne C3, CGE-Kapazitaet in pF |
| STAT_KAP_CGE_C4 | real | Antenne C4, Kapazitaet in pF |
| STAT_DSP_DATA_ID | int | intern |

<a id="job-status-phi-cge"></a>
### STATUS_PHI_CGE

CGE-Phasen (Elektrode-Guard) Antennen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_PHI_CGE_C1 | real | Antenne C1, CGE-Phase in Grad |
| STAT_PHI_CGE_C2 | real | Antenne C2, CGE-Phase in Grad |
| STAT_PHI_CGE_C3 | real | Antenne C3, CGE-Phase in Grad |
| STAT_PHI_CGE_C4 | real | Antenne C4, CGE-Phase in Grad |
| STAT_DSP_DATA_ID | int | intern |

<a id="job-status-io"></a>
### STATUS_IO

IO-Stati ausgeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_FDS_KLASSE | int | FDS-Klasse (0=unbelebt, 1=Kindersitz, 2=Person) |
| STAT_FDS_GUETE | int | FDS-Guete (0 (=schlecht) bis 10 (=gut)) |
| STAT_OCE_KLASSE | int | OCE-Klasse (0=unbelebt, 1=Kindersitz, 2=Person) |
| STAT_OCE_GUETE | int | OCE-Guete (0 (=schlecht) bis 10 (=gut)) |
| STAT_SBE_KLASSE | int | SBE-Gesamtklasse (0=unbelebt, 1=Kindersitz, 2=Person) |
| STAT_DSP_MODUS | int | intern |
| STAT_DSP_FREQUENZ | int | intern |
| STAT_DSP_USB | int | intern |
| STAT_DSP_LSB | int | intern |
| STAT_DSP_DATA_ID | int | intern |
| STAT_OOP_FCHECK | int | intern |
| STAT_OCE_INPUT | int | intern, Low(=0) oder High (=1) |
| STAT_DCA_INPUT | int | intern, Low(=0) oder High (=1) |

<a id="job-status-intern"></a>
### STATUS_INTERN

Interne IO-Stati ausgeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_INVPROTO_ID | int | Intern |
| STAT_TEL_LEN | int | Intern |
| STAT_TC | int | Intern |
| STAT_IW | int | Intern |
| STAT_HA | int | Intern |
| STAT_CP | int | Intern |
| STAT_X_POS | int | Intern |
| STAT_Y_POS | int | Intern |
| STAT_PQ | int | Intern |
| STAT_LW | int | Intern |
| STAT_ES | int | Intern |
| STAT_VORLAST_LSHAPE | int | Intern |
| STAT_TEL_PS | int | Intern |

<a id="job-steuern-dsp"></a>
### STEUERN_DSP

(Temporaeres) Setzen der DSP-Bytes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DSP_BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| DSP_BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| DSP_BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| DSP_BYTE4 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-sbe2"></a>
### STEUERN_SBE2

(Temporaeres) Setzen der Sitzbelegung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BELEGUNG | int | 0x00 = Fehler 0x01 = Unbelegt 0x02 = Kindersitz 0x03 = Person 0x04 = Out-Of-Position (OOP) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-oce"></a>
### STEUERN_OCE

(Temporaeres) Ein-/Ausschalten der OCE-Kommunikation

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KOMMUNIKATION_EIN | int | 0x00 = Aus, 0x01 = Ein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-herstellerdaten-lesen"></a>
### HERSTELLERDATEN_LESEN

Lesen der herstellerspez. Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| DATEN | binary | ausgelesene Hex-Daten |

<a id="job-diagnose-erhalten"></a>
### DIAGNOSE_ERHALTEN

Diagnose aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

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

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (31 × 2)
- [FORTTEXTE](#table-forttexte) (38 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNKTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 31 rows × 2 columns

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
| 0x30 | NEC |
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 38 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Lehne: Elektrode-Guard Kurzschluss |
| 0x02 | Lehne: Stecker nicht gesteckt |
| 0x03 | Lehne: Guard am Stecker gebrochen |
| 0x04 | Lehne: Kurzschluss U-Batt |
| 0x05 | Lehne: Kurzschluss Elektrode-Masse |
| 0x06 | Lehne: Kurzschluss Guard-Masse |
| 0x07 | Lehne: Elektronikfehler bei Messung |
| 0x08 | Lehne: Unterbrechung Elektrode an der Antenne |
| 0x09 | Lehne: Unterbrechung Guard an der Antenne |
| 0x0A | Lehne: Phasenfehler |
| 0x0B | Lehne: Feuchtigkeit |
| 0x0C | Lehne: CGE zu gross |
| 0x0D | Sitz: Elektrode-Guard Kurzschluss |
| 0x0E | Sitz: Stecker nicht gesteckt |
| 0x0F | Sitz: Guard am Stecker gebrochen |
| 0x10 | Sitz: Kurzschluss U-Batt |
| 0x11 | Sitz: Kurzschluss Elektrode-Masse |
| 0x12 | Sitz: Kurzschluss Guard-Masse |
| 0x13 | Sitz: Elektronikfehler bei Messung |
| 0x14 | Sitz: Unterbrechung Elektrode an der Antenne |
| 0x15 | Sitz: Unterbrechung Guard an der Antenne |
| 0x16 | Sitz: Phasenfehler |
| 0x17 | Sitz: Feuchtigkeit |
| 0x18 | Sitz: CGE zu gross |
| 0x21 | OCE (Druckmatte): Kommunikationsfehler Empfang |
| 0x22 | OCE (Druckmatte): Kommunikationsfehler Senden |
| 0x23 | OCE (Druckmatte): Klassifikationsfehler |
| 0x24 | OCE (Druckmatte): Ungueltige Daten |
| 0x25 | OCE (Druckmatte): Unterspannung |
| 0x26 | DCA (Crashausgang): Timing-/Framefehler |
| 0x27 | DCA (Crashausgang): Kommunikationsfehler |
| 0x28 | SBE2: Signalfehler |
| 0x29 | OCE (Druckmatte) -&gt; FDS (Antennensystem): Plausibilitaetsfehler |
| 0x2A | FDS (Antennensystem) -&gt; OCE (Druckmatte): Plausibilitaetsfehler |
| 0x2B | SBE2: CS-Fehler Codierdaten |
| 0x2C | FDS (Antennensystem): Empfangsstoerung |
| 0x3F | SBE2: Interner Fehler |
| 0xFF | unbekannter Fehlerort |
