# EML12.prg

- Jobs: [9](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Elektronische-Motor-Leistungsregelung M70 |
| ORIGIN | BMW TP-421 Weber |
| REVISION | 1.56 |
| AUTHOR | BMW TP-421 Weber |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Auslesen der Motortemperatur aus ADC-Kanal 3
- [STATUS_PWG_SPANNUNG](#job-status-pwg-spannung) - Auslesen der Spannung am Pedalwertgeber-Poti aus ADC-Kanal 5
- [STATUS_DIGITAL_LESEN](#job-status-digital-lesen) - Auslesen von digitalen Eingangsstati

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

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| ID_HW_ZULIEFERER | string | Zulieferer-Hardwarenummer |
| ID_SW_ZULIEFERER | string | Zulieferer-Softwarenummer |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_SW_NR | string | BMW-Softwarenummer (Laufende Nummer) |
| ID_DATUM | string | Herstelldatum |
| ID_GETRIEBE_VARIANTE_NR | int | table HW_Tabelle HARDWARENR GETRIEBE |
| ID_GETRIEBE_VARIANTE_TEXT | string | table GetriebeText GNR GTEXT |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| F_ORT_NR | int | Nr des Fehlers |
| F_ORT_TEXT | string | Fehlertext |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_UW1_NR | int | Index auf den Text fuer die Umweltbedingung |
| F_UW1_WERT | long | Wert der Umweltbedingung |
| F_UW1_TEXT | string | Text fuer die Umweltbedingung |
| F_UW2_NR | int | Index auf den Text fuer die Umweltbedingung |
| F_UW2_WERT | long | Wert der Umweltbedingung |
| F_UW2_TEXT | string | Text fuer die Umweltbedingung |
| F_UW3_NR | int | Index auf den Text fuer die Umweltbedingung |
| F_UW3_WERT | long | Wert der Umweltbedingung |
| F_UW3_TEXT | string | Text fuer die Umweltbedingung |
| F_HFK | int | Haeufigkeit eines Fehlers |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Auslesen der Motortemperatur aus ADC-Kanal 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_MOTORTEMPERATUR_WERT | long | Motortemperatur in Grad C |
| STAT_MOTORTEMPERATUR_EINH | string | Einheit = Grad C |

<a id="job-status-pwg-spannung"></a>
### STATUS_PWG_SPANNUNG

Auslesen der Spannung am Pedalwertgeber-Poti aus ADC-Kanal 5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_PWG_SPANNUNG_WERT | long | Spannung am Pedalwertgeber-Poti in Volt |
| STAT_PWG_SPANNUNG_EINH | string | Einheit = Volt |

<a id="job-status-digital-lesen"></a>
### STATUS_DIGITAL_LESEN

Auslesen von digitalen Eingangsstati

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_LL_SIGNAL_ZYL_1_6_EIN | int | Leerlaufsignal (0 oder 1) |
| STAT_LL_SIGNAL_ZYL_7_12_EIN | int | Leerlaufsignal (0 oder 1) |
| STAT_VL_SIGNAL_ZYL_1_6_EIN | int | Vollastsignal (0 oder 1) |
| STAT_VL_SIGNAL_ZYL_7_12_EIN | int | Vollastsignal (0 oder 1) |

## Tables

### Index

- [HW_TABELLE](#table-hw-tabelle) (36 × 2)
- [GETRIEBETEXT](#table-getriebetext) (3 × 2)
- [FORTTEXTE](#table-forttexte) (23 × 3)

<a id="table-hw-tabelle"></a>
### HW_TABELLE

Dimensions: 36 rows × 2 columns

| HARDWARENR | GETRIEBE |
| --- | --- |
| 1720060 | 1 |
| 1725229 | 1 |
| 1725364 | 1 |
| 1725387 | 1 |
| 1725388 | 1 |
| 1725389 | 1 |
| 1725390 | 1 |
| 1725391 | 1 |
| 1725392 | 1 |
| 1725393 | 1 |
| 1725394 | 1 |
| 1725395 | 1 |
| 1725396 | 1 |
| 1725397 | 1 |
| 1725398 | 1 |
| 1725399 | 1 |
| 1725400 | 1 |
| 1725401 | 1 |
| 1729742 | 0 |
| 1729743 | 0 |
| 1729744 | 0 |
| 1729745 | 0 |
| 1729746 | 0 |
| 1731914 | 1 |
| 1733598 | 1 |
| 1733599 | 1 |
| 1733600 | 1 |
| 1733601 | 1 |
| 1733602 | 1 |
| 1401124 | 0 |
| 1401400 | 2 |
| 1401401 | 2 |
| 1401402 | 2 |
| 1401403 | 2 |
| 1401404 | 2 |
| XXXXXXX | 2 |

<a id="table-getriebetext"></a>
### GETRIEBETEXT

Dimensions: 3 rows × 2 columns

| GNR | GTEXT |
| --- | --- |
| 0x00 | Handschaltung |
| 0x01 | Automatik |
| 0x02 | unbekannt |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 23 rows × 3 columns

| CODE | ORT | ORTTEXT |
| --- | --- | --- |
| 0xff | 0x00 | unbekannter Fehlerort |
| 0xd4 | 0x01 | Motortemperatur T-mot |
| 0xd5 | 0x02 | Geschwindigkeitsignal |
| 0xd6 | 0x03 | Drehzahlsignal Td |
| 0xc3 | 0x04 | Steuergeraet, A/D-Wandler |
| 0xc4 | 0x05 | FGR-Bedientaste |
| 0xc5 | 0x06 | PWG Anschlag veraendert |
| 0xb2 | 0x07 | Verbindung EML zum ASC |
| 0x9a | 0x08 | Steuergeraet intern |
| 0x99 | 0x09 | EML-Systemfehler |
| 0x2b | 0x0a | Ti-Signal 7-12. Zyl. |
| 0x2c | 0x0b | Ti-Signal 1-6. Zyl. |
| 0x4d | 0x0c | SG oder DK |
| 0x71 | 0x0d | DK-Stellmotor 7-12. Zyl. |
| 0x17 | 0x0e | DK-Stellmotor 1-6. Zyl. |
| 0x8e | 0x0f | PWG Schalter |
| 0x8f | 0x10 | PWG Poti. |
| 0x66 | 0x11 | DK-Poti. 7-12. Zyl. |
| 0x00 | 0x12 | DK-Poti. 1-6. Zyl. |
| 0x3c | 0x13 | DK-Schalter 7-12. Zyl. |
| 0x3d | 0x14 | DK-Schalter 1-6. Zyl. |
| 0xa5 | 0x15 | DK-PWG-Schalter 7-12. Zyl |
| 0x5a | 0x16 | DK-PWG-Schalter 1-6. Zyl |
