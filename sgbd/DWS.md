# DWS.prg

- Jobs: [14](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Deflation Warning System DWS |
| ORIGIN | BMW TI-431 Stadlhofer |
| REVISION | 1.7 |
| AUTHOR | BMW TI-433 Krueger, BMW TI-433 Winkler, GTI Peter Gross-Grueber, BMW TI-433 Kuessel |
| COMMENT | Info_Kommentar |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung / Kommunikationsparameter fuer Reifendruck-Control automatischer Aufruf beim ersten Zugriff auf die SGBD
- [IDENT](#job-ident) - Ident-Daten fuer DWS
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Quicktest High-Konzept nach Lastenheft
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [STATUS_IO](#job-status-io) - Auslesen der Statusbytes
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern einiger Signale
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten

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

Initialisierung / Kommunikationsparameter fuer Reifendruck-Control automatischer Aufruf beim ersten Zugriff auf die SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer DWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| FZ_TYP | string | DWS-Variante (FZ-Typ) anhand Diagnoseindex Varianten: E38/2_PL, E39/3, E52 oder M5 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Quicktest High-Konzept nach Lastenheft

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
| F_ART_ANZ | int | Anzahl der Fehlerarten (hier: immer 8) |
| F_ART1_NR | int | Index der 1. Fehlerart |
| F_ART1_TEXT | string | 1. Fehlerart als Text |
| F_ART2_NR | int | Index der 2. Fehlerart |
| F_ART2_TEXT | string | 2. Fehlerart als Text |
| F_ART3_NR | int | Index der 3. Fehlerart |
| F_ART3_TEXT | string | 3. Fehlerart als Text |
| F_ART4_NR | int | Index der 4. Fehlerart |
| F_ART4_TEXT | string | 4. Fehlerart als Text |
| F_ART5_NR | int | Index der 5. Fehlerart |
| F_ART5_TEXT | string | 5. Fehlerart als Text |
| F_ART6_NR | int | Index der 6. Fehlerart |
| F_ART6_TEXT | string | 6. Fehlerart als Text |
| F_ART7_NR | int | Index der 7. Fehlerart |
| F_ART7_TEXT | string | 7. Fehlerart als Text |
| F_ART8_NR | int | Index der 8. Fehlerart |
| F_ART8_TEXT | string | 8. Fehlerart als Text |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen (hier: immer 3,6,9) |
| F_UW_SATZ | int | Anzahl der Umweltsaetze (hier: immer 1,2,3) |
| F_UW1_NR | int | Index der 1. Umweltbedingung (hier: immer 1) |
| F_UW1_TEXT | string | Text zur 1. Umweltbedingung |
| F_UW1_WERT | int | Wert der 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit der 1. Umweltbedingung |
| F_UW2_NR | int | Index der 2. Umweltbedingung (hier: immer 2) |
| F_UW2_TEXT | string | Text zur 2. Umweltbedingung |
| F_UW2_WERT | int | Wert der 2. Umweltbedingung |
| F_UW2_EINH | string | Einheit der 2. Umweltbedingung |
| F_UW3_NR | int | Index der 3. Umweltbedingung (hier: immer 3) |
| F_UW3_TEXT | string | Text zur 3. Umweltbedingung |
| F_UW3_WERT | int | Wert der 3. Umweltbedingung |
| F_UW3_EINH | string | Einheit der 3. Umweltbedingung |
| F_UW4_NR | int | Index der 4. Umweltbedingung (hier: immer 4) |
| F_UW4_TEXT | string | Text zur 4. Umweltbedingung |
| F_UW4_WERT | int | Wert der 4. Umweltbedingung |
| F_UW4_EINH | string | Einheit der 4. Umweltbedingung |
| F_UW5_NR | int | Index der 5. Umweltbedingung (hier: immer 5) |
| F_UW5_TEXT | string | Text zur 5. Umweltbedingung |
| F_UW5_WERT | int | Wert der 5. Umweltbedingung |
| F_UW5_EINH | string | Einheit der 5. Umweltbedingung |
| F_UW6_NR | int | Index der 6. Umweltbedingung (hier: immer 6) |
| F_UW6_TEXT | string | Text zur 6. Umweltbedingung |
| F_UW6_WERT | int | Wert der 6. Umweltbedingung |
| F_UW6_EINH | string | Einheit der 6. Umweltbedingung |
| F_UW7_NR | int | Index der 7. Umweltbedingung (hier: immer 7) |
| F_UW7_TEXT | string | Text zur 7. Umweltbedingung |
| F_UW7_WERT | int | Wert der 7. Umweltbedingung |
| F_UW7_EINH | string | Einheit der 7. Umweltbedingung |
| F_UW8_NR | int | Index der 8. Umweltbedingung (hier: immer 8) |
| F_UW8_TEXT | string | Text zur 8. Umweltbedingung |
| F_UW8_WERT | int | Wert der 8. Umweltbedingung |
| F_UW8_EINH | string | Einheit der 8. Umweltbedingung |
| F_UW9_NR | int | Index der 1. Umweltbedingung (hier: immer 1) |
| F_UW9_TEXT | string | Text zur 1. Umweltbedingung |
| F_UW9_WERT | int | Wert der 1. Umweltbedingung |
| F_UW9_EINH | string | Einheit der 1. Umweltbedingung |
| F_UW10_NR | int | Index der 2. Umweltbedingung (hier: immer 2) |
| F_UW10_TEXT | string | Text zur 2. Umweltbedingung |
| F_UW10_WERT | int | Wert der 2. Umweltbedingung |
| F_UW10_EINH | string | Einheit der 2. Umweltbedingung |
| F_UW11_NR | int | Index der 3. Umweltbedingung (hier: immer 3) |
| F_UW11_TEXT | string | Text zur 3. Umweltbedingung |
| F_UW11_WERT | int | Wert der 3. Umweltbedingung |
| F_UW11_EINH | string | Einheit der 3. Umweltbedingung |
| F_UW12_NR | int | Index der 4. Umweltbedingung (hier: immer 4) |
| F_UW12_TEXT | string | Text zur 4. Umweltbedingung |
| F_UW12_WERT | int | Wert der 4. Umweltbedingung |
| F_UW12_EINH | string | Einheit der 4. Umweltbedingung |
| F_UW13_NR | int | Index der 5. Umweltbedingung (hier: immer 5) |
| F_UW13_TEXT | string | Text zur 5. Umweltbedingung |
| F_UW13_WERT | int | Wert der 5. Umweltbedingung |
| F_UW13_EINH | string | Einheit der 5. Umweltbedingung |
| F_UW14_NR | int | Index der 6. Umweltbedingung (hier: immer 6) |
| F_UW14_TEXT | string | Text zur 6. Umweltbedingung |
| F_UW14_WERT | int | Wert der 6. Umweltbedingung |
| F_UW14_EINH | string | Einheit der 6. Umweltbedingung |
| F_UW15_NR | int | Index der 7. Umweltbedingung (hier: immer 7) |
| F_UW15_TEXT | string | Text zur 7. Umweltbedingung |
| F_UW15_WERT | int | Wert der 7. Umweltbedingung |
| F_UW15_EINH | string | Einheit der 7. Umweltbedingung |
| F_UW16_NR | int | Index der 8. Umweltbedingung (hier: immer 8) |
| F_UW16_TEXT | string | Text zur 8. Umweltbedingung |
| F_UW16_WERT | int | Wert der 8. Umweltbedingung |
| F_UW16_EINH | string | Einheit der 8. Umweltbedingung |
| F_UW17_NR | int | Index der 1. Umweltbedingung (hier: immer 1) |
| F_UW17_TEXT | string | Text zur 1. Umweltbedingung |
| F_UW17_WERT | int | Wert der 1. Umweltbedingung |
| F_UW17_EINH | string | Einheit der 1. Umweltbedingung |
| F_UW18_NR | int | Index der 2. Umweltbedingung (hier: immer 2) |
| F_UW18_TEXT | string | Text zur 2. Umweltbedingung |
| F_UW18_WERT | int | Wert der 2. Umweltbedingung |
| F_UW18_EINH | string | Einheit der 2. Umweltbedingung |
| F_UW19_NR | int | Index der 3. Umweltbedingung (hier: immer 3) |
| F_UW19_TEXT | string | Text zur 3. Umweltbedingung |
| F_UW19_WERT | int | Wert der 3. Umweltbedingung |
| F_UW19_EINH | string | Einheit der 3. Umweltbedingung |
| F_UW20_NR | int | Index der 4. Umweltbedingung (hier: immer 4) |
| F_UW20_TEXT | string | Text zur 4. Umweltbedingung |
| F_UW20_WERT | int | Wert der 4. Umweltbedingung |
| F_UW20_EINH | string | Einheit der 4. Umweltbedingung |
| F_UW21_NR | int | Index der 5. Umweltbedingung (hier: immer 5) |
| F_UW21_TEXT | string | Text zur 5. Umweltbedingung |
| F_UW21_WERT | int | Wert der 5. Umweltbedingung |
| F_UW21_EINH | string | Einheit der 5. Umweltbedingung |
| F_UW22_NR | int | Index der 6. Umweltbedingung (hier: immer 6) |
| F_UW22_TEXT | string | Text zur 6. Umweltbedingung |
| F_UW22_WERT | int | Wert der 6. Umweltbedingung |
| F_UW22_EINH | string | Einheit der 6. Umweltbedingung |
| F_UW23_NR | int | Index der 7. Umweltbedingung (hier: immer 7) |
| F_UW23_TEXT | string | Text zur 7. Umweltbedingung |
| F_UW23_WERT | int | Wert der 7. Umweltbedingung |
| F_UW23_EINH | string | Einheit der 7. Umweltbedingung |
| F_UW24_NR | int | Index der 8. Umweltbedingung (hier: immer 8) |
| F_UW24_TEXT | string | Text zur 8. Umweltbedingung |
| F_UW24_WERT | int | Wert der 8. Umweltbedingung |
| F_UW24_EINH | string | Einheit der 8. Umweltbedingung |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | Speichersegment Bereich: 0x00-0xFF |
| ADRESSE | long | Speicheradresse Bereich: 0x0000-0xFFFF |
| ANZAHL | int | Anzahl der Daten Bereich: 1 bis 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |
| DATEN | binary | ausgelesene Hex-Daten |

<a id="job-status-io"></a>
### STATUS_IO

Auslesen der Statusbytes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STANDARD | int | Status Standardisierung (1=ein) |
| STAT_FEHLERKONZ | int | Status Fehlerspeicherkonzept(1=disable) |
| STAT_FEHLERAUSW | int | Status Fehlerauswirkung |
| STAT_PANNENMELD | int | Status Pannenmeldung    (1=ein) |
| STAT_DB00_4 | int | Frei |
| STAT_DB00_5 | int | Frei |
| STAT_DB00_6 | int | Frei |
| STAT_DB00_7 | int | Frei |
| STAT_BANDMODE | int | Bandmode |
| STAT_SYSAKTIV | int | Systemfunktion aktiv |
| STAT_BLINDPH | int | Blindphase |
| STAT_TASTER | int | Taster |
| STAT_DB01_4 | int | Bildet Basis fuer STAT_BREMSE |
| STAT_DB01_5 | int | Bildet Basis fuer STAT_BREMSE |
| STAT_DB01_6 | int | Frei |
| STAT_DB01_7 | int | Frei |
| STAT_WEG | unsigned long | Wegstrcke (seit letzter Standardisierung) |
| STAT_DSC_ABS_VL | int | Rohsignal vom DSC/ABS VL (Impulse/sec) |
| STAT_DSC_ABS_VR | int | Rohsignal vom DSC/ABS VR (Impulse/sec) |
| STAT_DSC_ABS_HL | int | Rohsignal vom DSC/ABS HL (Impulse/sec) |
| STAT_DSC_ABS_HR | int | Rohsignal vom DSC/ABS HR (Impulse/sec) |
| STAT_SI | int | geschwindigkeitsunabh. Standardisierungsfortschritt fuer M5 |
| STAT_SV1 | int | geschwindigkeitsabh. Standardisierungsfortschritt 1 fuer M5 |
| STAT_SV2 | int | geschwindigkeitsabh. Standardisierungsfortschritt 2 fuer M5 |
| STAT_7SI | int | geschwindigkeitsunabh. Standardisierungsfortschritt fuer Exx |
| STAT_7SV1 | int | geschwindigkeitsabh. Standardisierungsfortschritt 1 fuer Exx |
| STAT_7SV2 | int | geschwindigkeitsabh. Standardisierungsfortschritt 2 fuer Exx |
| STAT_7SV3 | int | geschwindigkeitsabh. Standardisierungsfortschritt 3 fuer Exx |
| STAT_7SV4 | int | geschwindigkeitsabh. Standardisierungsfortschritt 4 fuer Exx |
| STAT_7SV5 | int | geschwindigkeitsabh. Standardisierungsfortschritt 5 fuer Exx |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_BREMSE | int | Brems(lichtschalter)status (E46-relevant) 0=Bremse nicht betaetigt, 1=Bremse betaetigt 2=Keine Verbindung vorgesehen (alle ausser E46), 3=Status unplausibel |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern einiger Signale

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| START_STANDARD | int | 1 = Standardisierung starten |
| BANDMODE_CLR | int | 1 = Bandmode loeschen |
| BANDMODE_SET | int | 1 = Bandmode setzen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen der Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE4 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [LIEFERANTEN](#table-lieferanten) (32 × 2)
- [FORTTEXTE](#table-forttexte) (13 × 2)
- [FARTMATRIX](#table-fartmatrix) (1 × 17)
- [FARTTEXTE](#table-farttexte) (9 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 27)
- [FUMWELTTEXTE](#table-fumwelttexte) (9 × 3)
- [LN](#table-ln) (10 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNKTION |
| 0xFF | ERROR_ECU_NOT_ACKNOWLEDGE |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 32 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
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
| 0x37 | Dunlop |
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 13 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | ROM-Fehler |
| 0x02 | RAM-Fehler |
| 0x03 | EEPROM-Fehler (W/R,CHKSUM) |
| 0x04 | System-Fehler (main loop) |
| 0x05 | System-Fehler (stack) |
| 0x06 | DWS-Taster Masseschluss (Plausibilitaet |
| 0x07 | Geschwindigkeitsimpulse VL |
| 0x08 | Geschwindigkeitsimpulse VR |
| 0x09 | Geschwindigkeitsimpulse HL |
| 0x0A | Geschwindigkeitsimpulse HR |
| 0x0B | Kbus (60s kein Empfang bei KL15) |
| 0x0C | EEPROM: write check (standard) |
| 0xFF | unbekannter Fehlerort |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 1 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xFF | 0xFF | 0x00 | 0xFF | 0x01 | 0xFF | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 9 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Batterieschluss |
| 0x01 | Masseschluss |
| 0x02 | Leitungsunterbrechung |
| 0x03 | Wert unplausibel |
| 0x04 | -- |
| 0x05 | -- |
| 0x06 | Fehler momentan vorhanden |
| 0x07 | Fehler sporadisch |
| 0xFF | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 27 columns

| ORT | UW_ANZ | UW_SATZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR | UW17_NR | UW18_NR | UW19_NR | UW20_NR | UW21_NR | UW22_NR | UW23_NR | UW24_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xFF | 0x8 | 0x3 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 9 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x01 | Geschwindigkeit | km/h |
| 0x02 | Batteriespannung | Volt |
| 0x03 | Status Standardisierung | 1=ein     / 0=aus    |
| 0x04 | Status Fehlerspeicherkonzept | 1=disable / 0=enable |
| 0x05 | Status Fehlerauswirkung | 1=disable / 0=enable |
| 0x06 | Bandmode | 1=ja      / 0=nein   |
| 0x07 | Systemfunktion aktiv | 1=ja      / 0=nein   |
| 0x08 | Blindphase | 1=ja      / 0=nein   |
| 0xFF | unbekannte Umweltbedingung |  |

<a id="table-ln"></a>
### LN

Dimensions: 10 rows × 2 columns

| VEL | ROH |
| --- | --- |
| 0x00 | 0x00 |
| 0x19 | 0xBB8 |
| 0x32 | 0xBB8 |
| 0x4b | 0xBB8 |
| 0x5A | 0xBB8 |
| 0x6C | 0xBB8 |
| 0x7E | 0xBB8 |
| 0x69 | 0xBB8 |
| 0xb0 | 0xBB8 |
| 0xbb | 0xBB8 |
