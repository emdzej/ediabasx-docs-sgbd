# EGS.PRG

- Jobs: [25](#jobs)
- Tables: [1](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DME 5.2 M62 und MS41.x M52 |
| ORIGIN | BMW ET-421 Weber |
| REVISION | 1.40 |
| AUTHOR | BMW ET-421 Weber |
| COMMENT | Master - Datei fuer Flashprog. |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [EDIC_RESET](#job-edic-reset) - EDIC-Reset
- [initialisierung](#job-initialisierung) - Default Init-Job
- [INFO](#job-info) - Information SGBD
- [UPROG_EIN](#job-uprog-ein) - Programmierspannung einschalten
- [UPROG_AUS](#job-uprog-aus) - Programmierspannung ausschalten
- [BLOCKLAENGE_MAX](#job-blocklaenge-max) - maximale Blocklaenge
- [DATEN_REFERENZ](#job-daten-referenz) - Job DATEN-Referenz
- [HW_REFERENZ](#job-hw-referenz) - Job HW-Referenz
- [ZIF](#job-zif) - Job ZIF
- [ZIF_BACKUP](#job-zif-backup) - Job ZIF_BACKUP
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [FLASH_LESEN](#job-flash-lesen) - Beliebige FLASH - Zellen auslesen
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash  - Zellen loeschen
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Beliebige Flash Zellen mit 02 beschreiben
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Beliebige EPROM - Zellen auslesen
- [DATENBEREICH_LOESCHEN_0E](#job-datenbereich-loeschen-0e) - Beliebige EPROM - Zellen auslesen
- [SEED_KEY](#job-seed-key) - Schutzmechanismus SEED_KEY
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [DME_LINKS_VORHANDEN](#job-dme-links-vorhanden) - Linkes Stg vorhanden
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Codier - Checksumme abfragen
- [SCHALTE_PROTOKOLL_DS2_NACH_K2](#job-schalte-protokoll-ds2-nach-k2) - Umschaltung DS2
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Loeschen des Fehlerspeichers
- [SCHALTE_K2_DS2](#job-schalte-k2-ds2)

<a id="job-edic-reset"></a>
### EDIC_RESET

EDIC-Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-initialisierung"></a>
### initialisierung

Default Init-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn job erfolgreich 0 wenn job nicht erfolgreich |

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

<a id="job-uprog-ein"></a>
### UPROG_EIN

Programmierspannung einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_UPROG_WERT | real | Programmierspannung als Info zurueck |
| STATUS_UPROG_EINH | string | Einheit V |

<a id="job-uprog-aus"></a>
### UPROG_AUS

Programmierspannung ausschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-blocklaenge-max"></a>
### BLOCKLAENGE_MAX

maximale Blocklaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| BLOCKLAENGE_MAX_WERT | int | Blocklaenge fuer Telegramm |

<a id="job-daten-referenz"></a>
### DATEN_REFERENZ

Job DATEN-Referenz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| DATEN_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| DATEN_REF_PROJEKT | string | Projektkennzeichnung |
| DATEN_REF_PROGRAMM_STAND | string | Programmstand |
| DATEN_REF_DATENSATZ | string | Datensatzkennung |
| DATEN_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-hw-referenz"></a>
### HW_REFERENZ

Job HW-Referenz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| HW_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| HW_REF_PROJEKT | string | Projektkennzeichnung |
| HW_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-zif"></a>
### ZIF

Job ZIF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| ZIF_PROJEKT | string | Projektkennzeichnung |
| ZIF_PROGRAMM_STAND | string | Programmstand |
| ZIF_BMW_HW | string | BMW HW |
| ZIF_BMW_PST | string | BMW Programmstand |
| ZIF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-zif-backup"></a>
### ZIF_BACKUP

Job ZIF_BACKUP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_BACKUP_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| ZIF_BACKUP_PROJEKT | string | Projektkennzeichnung |
| ZIF_BACKUP_PROGRAMM_STAND | string | Programmstand |
| ZIF_BACKUP_BMW_HW | string | BMW HW |
| ZIF_BACKUP_BMW_PST | string | BMW Programmstand |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender-Info-Feldes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIF_ADRESSE | long | AIF Basisadresse |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_SW_NR | long | Softwarenummer |
| AIF_BEHOERDEN_NR | long | Behoerdennummer |
| AIF_ZB_NR | long | Zusbaunummer |
| AIF_STATUS | int | Bei Status = FF , AIF leer |

<a id="job-flash-lesen"></a>
### FLASH_LESEN

Beliebige FLASH - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low HEX |
| FLASH_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_LESEN_WERT | binary | nichts |

<a id="job-flash-loeschen"></a>
### FLASH_LOESCHEN

Flash  - Zellen loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN_ADRESSE_DATEN | binary | Uebergabeparameter, Startadresse High-Middle-Low und Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_LOESCHEN_ADRESSE | binary | nichts |
| FLASH_LOESCHEN_STATUS | int | nichts |
| FLASH_LOESCHEN_ANZAHL | int | nichts |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Beliebige Flash Zellen mit 02 beschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_ADRESSE_DATEN | binary | Uebergabeparameter, Startadresse High-Middle-Low und Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_SCHREIBEN_ADRESSE | binary | nichts |
| FLASH_SCHREIBEN_STATUS | int | nichts |
| FLASH_SCHREIBEN_ANZAHL | int | nichts |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Beliebige EPROM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_ENDE_ADRESSE_DATEN | binary | Uebergabeparameter, Startadresse High-Middle-Low und Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_SCHREIBEN_ENDE_ADRESSE | binary | nichts |
| FLASH_SCHREIBEN_ENDE_STATUS | int | nichts |
| FLASH_SCHREIBEN_ENDE_ANZAHL | int | nichts |

<a id="job-datenbereich-loeschen-0e"></a>
### DATENBEREICH_LOESCHEN_0E

Beliebige EPROM - Zellen auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-seed-key"></a>
### SEED_KEY

Schutzmechanismus SEED_KEY

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SEED_KEY | binary | Rueckgabewert Status |
| Z_ZAHL | int | Zufallszahl |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer DME

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
| ID_SW_NR | string | Softwarenummer |
| ID_AI_NR | string | Aenderungsindex |
| ID_PROD_NR | string | Produktionsnummer |

<a id="job-dme-links-vorhanden"></a>
### DME_LINKS_VORHANDEN

Linkes Stg vorhanden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_CODEHEX | binary | 5 Fehlerbyte |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-codier-checksumme"></a>
### STATUS_CODIER_CHECKSUMME

Codier - Checksumme abfragen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_CHECKSUMME_WERT | int | Ergebnis |

<a id="job-schalte-protokoll-ds2-nach-k2"></a>
### SCHALTE_PROTOKOLL_DS2_NACH_K2

Umschaltung DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-schalte-k2-ds2"></a>
### SCHALTE_K2_DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_SG_REJECTED |
| 0xB0 | ERROR_SG_PARAMETER |
| 0xB1 | ERROR_SG_FUNCTION |
| 0xB2 | ERROR_SG_NUMBER |
| 0xFF | ERROR_SG_NACK |
| 0x00 | ERROR_SG_UNBEKANNTES_STATUSBYTE |
