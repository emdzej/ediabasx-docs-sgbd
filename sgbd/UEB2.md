# UEB2.prg

- Jobs: [32](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Ueberrollschutzssensor |
| ORIGIN | BMW TI-431 Mellersh |
| REVISION | 1.01 |
| AUTHOR | BMW TP-422 Zender, BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | 0.12 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer UER2
- [IDENT](#job-ident) - Ident-Daten fuer UEB2
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Fehlerzaehler lesen
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen bedingtes High-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [COD_LESEN](#job-cod-lesen) - Auslesen der Codierdaten der UEB2
- [COD_AUSSTATTUNG_LESEN](#job-cod-ausstattung-lesen) - Auslesen der Ausstattungsbytes des UEB2
- [COD_PARAMETERSATZ1_LESEN](#job-cod-parametersatz1-lesen) - Auslesen Parametersatz1 des UEB2
- [COD_PARAMETERSATZ2_LESEN](#job-cod-parametersatz2-lesen) - Auslesen Parametersatz2 des UEB2
- [COD_VERRIEGELUNG_LESEN](#job-cod-verriegelung-lesen) - Auslesen der Verriegelungsbytes des UEB2
- [COD_KFZ_DATEN_LESEN](#job-cod-kfz-daten-lesen) - Auslesen Kfz-Herstellerdaten des UEB2
- [STATUS_FEHLERZUSTAENDE_LESEN](#job-status-fehlerzustaende-lesen)
- [STATUS_ANZAHL_AUSLOESUNGEN_LESEN](#job-status-anzahl-ausloesungen-lesen) - Anzahl der Ausloesungen
- [STATUS_BORDSPANNUNG_LESEN](#job-status-bordspannung-lesen)
- [STATUS_G_SENSOR_LESEN](#job-status-g-sensor-lesen)
- [STATUS_CRASHDATEN_G_SENSOR_LESEN](#job-status-crashdaten-g-sensor-lesen)
- [STATUS_CRASHDATEN_LIBELLE1_LESEN](#job-status-crashdaten-libelle1-lesen)
- [STATUS_CRASHDATEN_LIBELLE2_LESEN](#job-status-crashdaten-libelle2-lesen)
- [STATUS_CRASHDATEN_DIAGNOSE_LESEN](#job-status-crashdaten-diagnose-lesen)
- [STATUS_TRANSPORTSICHERUNG_LESEN](#job-status-transportsicherung-lesen) - Zustand der Transportsicherung
- [STEUERN_BUEGEL](#job-steuern-buegel) - Ausfahren des Buegels
- [STEUERN_TRANSPORTSICHERUNG_AN](#job-steuern-transportsicherung-an) - Transportsicherung setzen
- [STEUERN_TRANSPORTSICHERUNG_AUS](#job-steuern-transportsicherung-aus) - Transportsicherung entfernen
- [LOGIN](#job-login) - login-procedure
- [LOGIN2](#job-login2) - login-procedure
- [KFZ_DATEN_SCHREIBEN](#job-kfz-daten-schreiben) - KFZ-Herstellerdaten schreiben
- [VERRIEGELUNG_SETZEN](#job-verriegelung-setzen) - Verriegelung setzen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - Diagnose aufrechterhalten
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

Init-Job fuer UER2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer UEB2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| ANTWORT | binary | Antworttelegramm |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Fehlerzaehler lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| F_ANZ | int | Fehlerzaehler |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen bedingtes High-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Fehlercode |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
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

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-cod-lesen"></a>
### COD_LESEN

Auslesen der Codierdaten der UEB2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN_0 | string | Block 0 |
| COD_DATEN_1 | string | Block 1 |
| COD_DATEN_2 | string | Block 2 |
| COD_DATEN_3 | string | Block 3 |
| COD_DATEN_4 | string | Block 4 |
| COD_DATEN_5 | string | Block 5 |
| COD_DATEN_6 | string | Block 6 |
| COD_DATEN_7 | string | Block 7 |
| COD_DATEN_8 | string | Block 8 |

<a id="job-cod-ausstattung-lesen"></a>
### COD_AUSSTATTUNG_LESEN

Auslesen der Ausstattungsbytes des UEB2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN_0 | string | Block 0 |

<a id="job-cod-parametersatz1-lesen"></a>
### COD_PARAMETERSATZ1_LESEN

Auslesen Parametersatz1 des UEB2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN_1 | string | Block 1 |
| COD_DATEN_2 | string | Block 2 |
| COD_DATEN_3 | string | Block 3 |

<a id="job-cod-parametersatz2-lesen"></a>
### COD_PARAMETERSATZ2_LESEN

Auslesen Parametersatz2 des UEB2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN_4 | string | Block 4 |
| COD_DATEN_5 | string | Block 5 |
| COD_DATEN_6 | string | Block 6 |

<a id="job-cod-verriegelung-lesen"></a>
### COD_VERRIEGELUNG_LESEN

Auslesen der Verriegelungsbytes des UEB2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN_7 | string | Block 7 |

<a id="job-cod-kfz-daten-lesen"></a>
### COD_KFZ_DATEN_LESEN

Auslesen Kfz-Herstellerdaten des UEB2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN_8 | string | Block 8 |
| COD_DATEN_KONVERTIERT | string | Block 8 umgewandelt |

<a id="job-status-fehlerzustaende-lesen"></a>
### STATUS_FEHLERZUSTAENDE_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_FEHLERLAMPE_UNTERBRECHUNG | int | 0: Unterbrechung oder Masseschluss der Fehlerlampe |
| STAT_FEHLERLAMPE_UBATTSCHLUSS | int | 0: Kurzschluss Fehlerlampe nach Ubatt |
| STAT_UNTERSPANNUNG | int | 0: Unterspannung |
| STAT_SCHLUSS_MAGNETEN | int | 0: Schluss zwischen den Magneten |
| STAT_HELLSPG_L1_LOW | int | 0: Hellspannung L1 zu niedrig |
| STAT_SCHWELLE_L1_LOW | int | 0: Ausloeseschwelle L1 zu niedrig |
| STAT_HELLSPG_L2_LOW | int | 0: Hellspannung L2 zu niedrig |
| STAT_SCHWELLE_L2_LOW | int | 0: Ausloeseschwelle L2 zu niedrig |
| STAT_WIDERSTAND_M1_LOW | int | 0: Widerstand Magnet 1 zu niedrig |
| STAT_WIDERSTAND_M1_HIGH | int | 0: Widerstand magnet 1 zu hoch |
| STAT_UBATTSCHLUSS_M1 | int | 0: Ubatt Schluss Magnet 1 |
| STAT_WIDERSTAND_M2_LOW | int | 0: Widerstand Magnet 2 zu niedrig |
| STAT_WIDERSTAND_M2_HIGH | int | 0: Widerstand Magnet 2 zu hoch |
| STAT_UBATTSCHLUSS_M2 | int | 0: Ubatt Schluss Magnet 2 |
| ANTWORT | binary | Antworttelegramm |

<a id="job-status-anzahl-ausloesungen-lesen"></a>
### STATUS_ANZAHL_AUSLOESUNGEN_LESEN

Anzahl der Ausloesungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_AUSLOESUNGEN_HIGHBYTE | int | Ausloesungen Highbyte |
| STAT_AUSLOESUNGEN_LOWBYTE | int | Ausloesungen Lowbyte |
| STAT_AUSLOESUNGEN | long | Ausloesungen Lowbyte |
| ANTWORT | binary | Antworttelegramm |

<a id="job-status-bordspannung-lesen"></a>
### STATUS_BORDSPANNUNG_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_BORDSPANNUNG | long | Bordspannung lesen |
| ANTWORT | binary | Antworttelegramm |

<a id="job-status-g-sensor-lesen"></a>
### STATUS_G_SENSOR_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_G_SENSOR | int | 1: G-Sensor schwerelos, ansonsten 0 |
| ANTWORT | binary | Antworttelegramm |

<a id="job-status-crashdaten-g-sensor-lesen"></a>
### STATUS_CRASHDATEN_G_SENSOR_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_BORDSPANNUNG | long | Bordspannung zur Ausloesezeit in [V] |
| STAT_AUSLOESUNGEN_HIGHBYTE | int | Ausloesungen Highbyte |
| STAT_AUSLOESUNGEN_LOWBYTE | int | Ausloesungen Lowbyte |
| STAT_AUSLOESUNGEN | long | Ausloesungen Lowbyte |
| CRASH_DATEN_1 | string | Kennung 1 |

<a id="job-status-crashdaten-libelle1-lesen"></a>
### STATUS_CRASHDATEN_LIBELLE1_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_BORDSPANNUNG | long | Bordspannung zur Ausloesezeit in [V] |
| STAT_AUSLOESUNGEN_HIGHBYTE | int | Ausloesungen Highbyte |
| STAT_AUSLOESUNGEN_LOWBYTE | int | Ausloesungen Lowbyte |
| STAT_AUSLOESUNGEN | long | Ausloesungen Lowbyte |
| CRASH_DATEN_2 | string | Kennung 2 |

<a id="job-status-crashdaten-libelle2-lesen"></a>
### STATUS_CRASHDATEN_LIBELLE2_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_BORDSPANNUNG | long | Bordspannung zur Ausloesezeit in [V] |
| STAT_AUSLOESUNGEN_HIGHBYTE | int | Ausloesungen Highbyte |
| STAT_AUSLOESUNGEN_LOWBYTE | int | Ausloesungen Lowbyte |
| STAT_AUSLOESUNGEN | long | Ausloesungen Lowbyte |
| CRASH_DATEN_3 | string | Kennung 3 |

<a id="job-status-crashdaten-diagnose-lesen"></a>
### STATUS_CRASHDATEN_DIAGNOSE_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_BORDSPANNUNG | long | Bordspannung zur Ausloesezeit in [V] |
| STAT_AUSLOESUNGEN_HIGHBYTE | int | Ausloesungen Highbyte |
| STAT_AUSLOESUNGEN_LOWBYTE | int | Ausloesungen Lowbyte |
| STAT_AUSLOESUNGEN | long | Ausloesungen Lowbyte |
| CRASH_DATEN_4 | string | Kennung 4 |

<a id="job-status-transportsicherung-lesen"></a>
### STATUS_TRANSPORTSICHERUNG_LESEN

Zustand der Transportsicherung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_TRANSPORTSICHERUNG_BYTE1 | int | Transportsicherung Byte 1 |
| STAT_TRANSPORTSICHERUNG_BYTE2 | int | Transportsicherung Byte 2 |
| STAT_TRANSPORTSICHERUNG_EIN | int | 1, wenn Transportsicherung gesetzt, sonst 0 |
| ANTWORT | binary | Antworttelegramm |

<a id="job-steuern-buegel"></a>
### STEUERN_BUEGEL

Ausfahren des Buegels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-transportsicherung-an"></a>
### STEUERN_TRANSPORTSICHERUNG_AN

Transportsicherung setzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| ANTWORT | binary | Antworttelegramm |

<a id="job-steuern-transportsicherung-aus"></a>
### STEUERN_TRANSPORTSICHERUNG_AUS

Transportsicherung entfernen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| ANTWORT | binary | Antworttelegramm |

<a id="job-login"></a>
### LOGIN

login-procedure

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-login2"></a>
### LOGIN2

login-procedure

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-kfz-daten-schreiben"></a>
### KFZ_DATEN_SCHREIBEN

KFZ-Herstellerdaten schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE_ADRESSE | int | gibt Startbyte an [1-16] |
| ANZAHL_BYTES | int | gibt die Anzahl, der einzuschreibenden Bytes ein |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| BYTE4 | int | kann beliebig verwendet werden |
| BYTE5 | int | kann beliebig verwendet werden |
| BYTE6 | int | kann beliebig verwendet werden |
| BYTE7 | int | kann beliebig verwendet werden |
| BYTE8 | int | kann beliebig verwendet werden |
| BYTE9 | int | kann beliebig verwendet werden |
| BYTE10 | int | kann beliebig verwendet werden |
| BYTE11 | int | kann beliebig verwendet werden |
| BYTE12 | int | kann beliebig verwendet werden |
| BYTE13 | int | kann beliebig verwendet werden |
| BYTE14 | int | kann beliebig verwendet werden |
| BYTE15 | int | kann beliebig verwendet werden |
| BYTE16 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| TELEGRAMM | binary | Telegramm an SG |
| ANTWORT | binary | Antworttelegramm von SG |

<a id="job-verriegelung-setzen"></a>
### VERRIEGELUNG_SETZEN

Verriegelung setzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| COD_DATEN_7 | string | Block 7 |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnose-weiter"></a>
### DIAGNOSE_WEITER

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

- [JOBRESULT](#table-jobresult) (7 × 2)
- [FORTTEXTE](#table-forttexte) (15 × 2)
- [FARTTEXTE](#table-farttexte) (10 × 2)
- [FARTMATRIX](#table-fartmatrix) (14 × 17)
- [LIEFERANTEN](#table-lieferanten) (30 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xFF | ERROR_ECU_NACK |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 15 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | interner Fehler |
| 0x02 | Fehlerlampe |
| 0x03 | Versorgungsspannung |
| 0x04 | Magnet 1 und 2 |
| 0x05 | Magnet 1 |
| 0x06 | Magnet 2 |
| 0x07 | Zaehler fuer Ausloesungen |
| 0x08 | Libelle 1 |
| 0x09 | Libelle 1 |
| 0x0A | Libelle 1 Ausloeseschwelle |
| 0x0B | Libelle 2 |
| 0x0C | Libelle 2 |
| 0x0D | Libelle 2 Ausloeseschwelle |
| 0x0E | g-Sensor |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Leckwiderstand oder Kurzschluss gegen U-Batt |
| 0x02 | Leckwiderstand oder Kurzschluss gegen Masse |
| 0x04 | Leitungsunterbrechung |
| 0x08 | unbekannte Fehlerart |
| 0x10 | Grenzwertunterschreitung |
| 0x20 | Grenzwertueberschreitung |
| 0x40 | Fehler momentan vorhanden |
| 0x80 | sporadischer Fehler |
| 0xFF | -- |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 14 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x02 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x03 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x04 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x05 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x06 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x07 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x08 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x09 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x0A | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x0B | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x0C | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x0D | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |
| 0x0E | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 30 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |
