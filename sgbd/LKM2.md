# LKM2.prg

- Jobs: [10](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Lampenkontrollmodul LKM2 E31 |
| ORIGIN | BMW ET-421 Teepe |
| REVISION | 1.41 |
| AUTHOR | Softing, BMW ET-421 Teepe |
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
- [STEUERN_AUSGAENGE](#job-steuern-ausgaenge) - Einlesen der Ausgangsinformation
- [ZAEHLERSTAENDE_LESEN](#job-zaehlerstaende-lesen) - Auslesen der Zaehlerstaende
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten (Hier nur Laendervariante)
- [STATUS_LESEN](#job-status-lesen) - Abfrage der aktuellen Stati

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
| ID_GEN_NR | int | Generationsnummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_SW_NR | int | Softwarenummer |
| ID_PP_NR | int | Pruefplannummer |
| ID_LIEF_NR | int | Herstellernummer |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |

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
| F_ART_ANZ | int | Anzahl der Fehlerarten (hier immer 1) |
| F_ART1_NR | int | Index des Fehlerarttextes |
| F_ART1_TEXT | string | Fehlerarttext |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen (hier immer 0) |
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

<a id="job-steuern-ausgaenge"></a>
### STEUERN_AUSGAENGE

Einlesen der Ausgangsinformation

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGAENGE | string | Anzusteuernder Ausgang table Ansteuern SELECTOR BYTE1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-zaehlerstaende-lesen"></a>
### ZAEHLERSTAENDE_LESEN

Auslesen der Zaehlerstaende

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | vgl. Tabelle JobResult |
| ZAEHLER_FL_RELAIS_AKTIV | int | Zaehler fuer Fernlicht-Relais-Betaetigungen |
| ZAEHLER_LH_RELAIS_AKTIV | int | Zaehler fuer Lichthupen-Relais-Betaetigungen |
| ZAEHLER_AL_EIN | int | Zaehler fuer Abblendlicht-Betaetigungen |
| ZAEHLER_NSW_EIN | int | Zaehler fuer Nebelscheinwerfer-Betaetigungen |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten (Hier nur Laendervariante)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | vgl. Tabelle JobResult |
| LAENDERVARIANTE_TEXT | string | Laendervariante als Klartext (vgl. Tabelle Laender) |
| LAENDERVARIANTE_BYTE | string | Laendervariante (original Byte) |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Abfrage der aktuellen Stati

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | vgl. Tabelle JobResult |
| STAT_SL_LINKS_EIN | int | Standlicht links ein |
| STAT_SL_RECHTS_EIN | int | Standlicht rechts ein |
| STAT_RL_LINKS_EIN | int | Ruecklicht links ein |
| STAT_RL_RECHTS_EIN | int | Ruecklicht rechts ein |
| STAT_AL_LINKS_EIN | int | Abblendlicht links ein |
| STAT_AL_RECHTS_EIN | int | Abblendlicht rechts ein |
| STAT_FL_RELAIS_AKTIV | int | Fernlicht-Relais ein |
| STAT_LH_RELAIS_AKTIV | int | Lichthupen-Relais ein |
| STAT_BL_LINKS_EIN | int | Bremslicht links ein |
| STAT_BL_RECHTS_EIN | int | Bremslicht rechts ein |
| STAT_BL_MITTE_EIN | int | Bremslicht Mitte ein |
| STAT_NSW_LINKS_EIN | int | Nebelscheinwerfer links ein |
| STAT_NSW_RECHTS_EIN | int | Nebelscheinwerfer rechts ein |
| STAT_NSL_LINKS_EIN | int | Nebelschlusslicht links ein |
| STAT_NSL_RECHTS_EIN | int | Nebelschlusslicht rechts ein |
| STAT_KZL_EIN | int | Kennzeichenleuchte ein |
| STAT_AL_SCHALTER_AKTIV | int | Abblendlichtschalter ist aktiv |
| STAT_FL_SCHALTER_AKTIV | int | Fernlichtschalter ist aktiv |
| STAT_NSW_SCHALTER_AKTIV | int | Nebelscheinwerfer-Schalter ist aktiv |
| STAT_KSW_ZU_LINKS_AKTIV | int | Klappscheinw.-Endschalter 'links zu' ist aktiv |
| STAT_KSW_ZU_RECHTS_AKTIV | int | Klappscheinw.-Endschalter 'rechts zu' ist aktiv |
| STAT_BL_SCHALTER_AKTIV | int | Bremslichtschalter ist aktiv |
| STAT_KSW_AUF_LINKS_AKTIV | int | Klappscheinw.-Endschalter 'links offen' ist aktiv |
| STAT_KSW_AUF_RECHTS_AKTIV | int | Klappscheinw.-Endschalter 'rechts offen' ist aktiv |
| STAT_MELDUNG1 | string | LKM-Meldung Byte 1 |
| STAT_MELDUNG2 | string | LKM-Meldung Byte 2 |
| STAT_MELDUNG3 | string | LKM-Meldung Byte 3 |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (24 × 4)
- [FARTTEXTE](#table-farttexte) (2 × 2)
- [ANSTEUERN](#table-ansteuern) (18 × 3)
- [LAENDER](#table-laender) (7 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 24 rows × 4 columns

| ORT | ORTTEXT | FA_BYTE | FA_MASK |
| --- | --- | --- | --- |
| 0x01 | Abblendlicht links | 4 | 0x02 |
| 0x02 | Abblendlicht rechts | 4 | 0x02 |
| 0x03 | Standlicht links | 4 | 0x01 |
| 0x04 | Standlicht rechts | 4 | 0x01 |
| 0x05 | Ruecklicht links | 4 | 0x04 |
| 0x06 | Ruecklicht rechts | 4 | 0x04 |
| 0x07 | NSW links | 5 | 0x01 |
| 0x08 | NSW rechts | 5 | 0x01 |
| 0x09 | Kennzeichenlicht links | 4 | 0x80 |
| 0x0A | Kennzeichenlicht rechts | 4 | 0x80 |
| 0x0B | Nebelschlussleuchte links | 5 | 0x02 |
| 0x0C | Nebelschlussleuchte rechts | 5 | 0x02 |
| 0x0D | Bremslicht links | 4 | 0x08 |
| 0x0E | Bremslicht rechts | 4 | 0x08 |
| 0x0F | Bremslicht mitte | 4 | 0x20 |
| 0x10 | Sicherung NSW | 5 | 0x40 |
| 0x11 | Sicherung Nebelschlussl. | 5 | 0x20 |
| 0x12 | Sicherung Bremslicht | 4 | 0x40 |
| 0x13 | Relais Abblendlicht | 4 | 0x02 |
| 0x14 | Relais NSW | 5 | 0x01 |
| 0x15 | Klappscheinwerfer links | 0 | 0x00 |
| 0x16 | Klappscheinwerfer rechts | 0 | 0x00 |
| 0x17 | Bremslichtschalter | 5 | 0x08 |
| 0x00 | unbekannter Fehlerort | 0 | 0x00 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 2 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x01 | Fehler momentan vorhanden |

<a id="table-ansteuern"></a>
### ANSTEUERN

Dimensions: 18 rows × 3 columns

| SELECTOR | BYTE1 | FLAG |
| --- | --- | --- |
| AL_EIN | 0x01 | 1 |
| AL_AUS | 0x00 | 0 |
| NSW_EIN | 0x02 | 1 |
| NSW_AUS | 0x00 | 0 |
| FL_EIN | 0x04 | 1 |
| FL_AUS | 0x00 | 0 |
| LH_EIN | 0x08 | 1 |
| LH_AUS | 0x00 | 0 |
| KSW_EIN | 0x30 | 1 |
| KSW_AUS | 0x00 | 0 |
| KSW_L_EIN | 0x10 | 1 |
| KSW_L_AUS | 0x00 | 0 |
| KSW_R_EIN | 0x20 | 1 |
| KSW_R_AUS | 0x00 | 0 |
| KAU_EIN | 0x40 | 1 |
| KAU_AUS | 0x00 | 0 |
| ALLES_EIN | 0x7F | 1 |
| ALLES_AUS | 0x00 | 0 |

<a id="table-laender"></a>
### LAENDER

Dimensions: 7 rows × 2 columns

| LV | LAENDERVARIANTE |
| --- | --- |
| 0x00 | ECE |
| 0x01 | Nordland |
| 0x72 | USA |
| 0x02 | Australien/Golf |
| 0x25 | Norwegen |
| 0x40 | Japan |
| 0xFF | ERROR_UNBEKANNTE_LAENDERVARIANTE |
