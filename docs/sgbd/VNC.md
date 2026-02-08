# VNC.prg

- Jobs: [14](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | VNC fuer E36 M3 |
| ORIGIN | BMW TP-421 Weber |
| REVISION | 1.01 |
| AUTHOR | BMW TP-421 Weber |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Ident-Daten fuer die VNC
- [VERSION_LESEN](#job-version-lesen) - Auslesen der Versionsnummer
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [STATUS_LESEN](#job-status-lesen) - Einlesen der Betriebswerte
- [MESSE_VERSTELLZEIT](#job-messe-verstellzeit) - Messen der minimalen und maximalen Verstellzeit
- [ANFAHREN_POSITION](#job-anfahren-position) - Anfahren einer vorgegebenen Position
- [STEUERN_DICHTHEIT_PRUEF](#job-steuern-dichtheit-pruef) - Messen der Dichtheit der Ventile
- [STEUERN_VENTILE](#job-steuern-ventile) - Ansteuern der Ventile
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - Ansteuern des E-Luefters
- [STEUERN_BEENDEN](#job-steuern-beenden) - Beenden von Ansteuerungen

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

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

Ident-Daten fuer die VNC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |
| ID_LIEF_NR | string | Lieferanten-Nummer |
| _TEL_ANTWORT | binary |  |

<a id="job-version-lesen"></a>
### VERSION_LESEN

Auslesen der Versionsnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| VERSIONSNUMMER | string | VNC Versionsnummer |
| _TEL_ANTWORT | binary |  |

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
| F_ART1_NR | int | Index des Fehlerarttextes |
| F_ART1_TEXT | string | Fehlerarttext |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_HFK | int | Haeufigkeit eines Fehlers |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Einlesen der Betriebswerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| _TEL_ANTWORT | binary |  |
| STAT_TIMER0_WERT | unsigned int | Timer 0 Wert |
| STAT_TIMER0_EINH | string | Timer 0 Einheit [1] |
| STAT_TIMER1_WERT | unsigned int | Timer 1 Wert |
| STAT_TIMER1_EINH | string | Timer 1 Einheit [1] |
| STAT_VERSTW_SOLL_WERT | int | Verstellwinkel Sollwert |
| STAT_VERSTW_SOLL_EINH | string | Verstellwinkel Sollwert Einheit [Grad KW] |
| STAT_VERSTW_IST_WERT | int | Verstellwinkel Istwert |
| STAT_VERSTW_IST_EINH | string | Verstellwinkel Istwert Einheit [Grad KW] |
| STAT_DKPOTI_WERT | real | Spannung am Drosselklappenpoti |
| STAT_DKPOTI_EINH | string | Spannungseinheit [Volt] |
| STAT_TEMP_ANSAUGL_WERT | int | Ansauglufttemperatur |
| STAT_TEMP_ANSAUGL_EINH | string | Ansauglufttemperatur in [Grad C] |
| STAT_TEMP_MOTOR_WERT | int | Motortemperatur |
| STAT_TEMP_MOTOR_EINH | string | Motortemperatur in [Grad C] |
| STAT_DREHZAHL_WERT | int | Drehzahl |
| STAT_DREHZAHL_EINH | string | Drehzahl in [1/min] |
| STAT_GESCHW_WERT | int | Geschwindigkeit |
| STAT_GESCHW_EINH | string | Geschwindigkeit in [km/h] |

<a id="job-messe-verstellzeit"></a>
### MESSE_VERSTELLZEIT

Messen der minimalen und maximalen Verstellzeit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| _TEL_ANTWORT | binary |  |
| STAT_MAX_WERT | unsigned int | Maximale Verstellzeit |
| STAT_MAX_EINH | string | in [ms] |
| STAT_MIN_WERT | unsigned int | Minimale Verstellzeit |
| STAT_MIN_EINH | string | in [ms] |

<a id="job-anfahren-position"></a>
### ANFAHREN_POSITION

Anfahren einer vorgegebenen Position

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SOLLWINKEL | int | Sollwinkel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary |  |
| STAT_SOLL_WERT | unsigned int | Sollwert |
| STAT_SOLL_EINH | string | Sollwert |
| STAT_IST_WERT | unsigned int | Istwert |
| STAT_IST_EINH | string | Istwert |

<a id="job-steuern-dichtheit-pruef"></a>
### STEUERN_DICHTHEIT_PRUEF

Messen der Dichtheit der Ventile

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SOLLWINKEL | int | Sollwinkel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary |  |
| STAT_SOLL_WERT | unsigned int | Sollwert |
| STAT_SOLL_EINH | string | Sollwert |
| STAT_IST_WERT | unsigned int | Istwert |
| STAT_IST_EINH | string | Istwert |

<a id="job-steuern-ventile"></a>
### STEUERN_VENTILE

Ansteuern der Ventile

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL | int | Anzusteuerndes Ventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

Ansteuern des E-Luefters

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-beenden"></a>
### STEUERN_BEENDEN

Beenden von Ansteuerungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [FORTTEXTE](#table-forttexte) (9 × 2)
- [FARTTEXTE](#table-farttexte) (2 × 2)

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
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 9 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Ventil 1 defekt |
| 0x02 | Fehler auf dem CAN-Bus |
| 0x03 | nicht belegt |
| 0x04 | nicht belegt |
| 0x06 | Geber 1 defekt |
| 0x08 | Pruefsummenfehler festgestellt |
| 0x09 | Ventil 2 defekt |
| 0x0E | Geber 2 defekt |
| 0x00 | unbekannte Fehlerart |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 2 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x01 | momentan   |
| 0x00 | sporadisch |
