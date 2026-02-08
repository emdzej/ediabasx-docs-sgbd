# mrma22.prg

- Jobs: [12](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Steuergeräte MA2.1 und MA2.2 |
| ORIGIN | I+ME Actia R&D ABT, KA |
| REVISION | 1.004 |
| AUTHOR | I+ME R&D Axel Bäthge, KA |
| COMMENT | N/A |
| PACKAGE | 1.52 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Fakeantwort notwendig wegen ISTA zur Steuerung SG-Baum
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INIT_FS_LESEN](#job-init-fs-lesen) - Initialisierung und k_line offen
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler)
- [INIT_FS_LOESCHEN](#job-init-fs-loeschen) - Initialisierung und reiz_k_line
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [INIT_LUEFTERTEST](#job-init-lueftertest) - Initialisierung und reiz_k_line
- [LUEFTERTEST](#job-lueftertest) - Reizen beenden, Fehlercode lesen
- [INIT_DK_EINSTELLEN](#job-init-dk-einstellen) - Initialisierung und reiz_k_line
- [ENDE_DK_EINSTELLEN](#job-ende-dk-einstellen) - Initialisierung und reiz_k_line
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Deinitialisierung

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

<a id="job-ident"></a>
### IDENT

Fakeantwort notwendig wegen ISTA zur Steuerung SG-Baum

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | immer NOTOKAY in ISTA wird damit Steuergerät gelb markiert |
| JOB_STATUS2 | string | immer OKAY in ISTA wird damit Steuergerät grün markiert |
| VARIANTE_IND | string | Name der SGBD |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HINWEIS | string | folgende Massnahmen |
| DONE | int | 1, wenn Okay |

<a id="job-init-fs-lesen"></a>
### INIT_FS_LESEN

Initialisierung und k_line offen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| HINWEIS | string | folgende Massnahmen |
| _TEL_ANTWORT | binary | INIT_FS_LESEN erfolgreich |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers für KWP-2000 immer 2 |
| HINWEIS | string | folgende Massnahmen |
| F_ORT_NR | long | Index für den Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text Table FOrteTexte als ORTTEXT |
| F_SYMPTOM_NR | int | Index für die Fehlerart |
| F_SYMPTOM_TEXT | string | Fehlerart als Text Table FArtTexte als ARTTEXT |
| F_READY_NR | int | Readyness Flag als Zahl |
| F_READY_TEXT | string | Readyness Flag als Text |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard Fehlerart) als Text Fehlerart table ArtTexte als Text |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard Fehlerart) als Zahl Status Bit 7 |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard Fehlerart) als Text |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hex Code |
| _TEL_ANTWORT | binary | FS_LESEN erfolgreich |

<a id="job-init-fs-loeschen"></a>
### INIT_FS_LOESCHEN

Initialisierung und reiz_k_line

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| HINWEIS | string | folgende Massnahmen |
| _TEL_ANTWORT | binary | INIT_FS_LOESCHEN erfolgreich |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| HINWEIS | string | folgende Massnahmen |
| _TEL_ANTWORT | binary | FS_LOESCHEN erfolgreich |

<a id="job-init-lueftertest"></a>
### INIT_LUEFTERTEST

Initialisierung und reiz_k_line

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| HINWEIS | string | folgende Massnahmen, gleich zu INIT_FS_LOESCHEN |
| _TEL_ANTWORT | binary | INIT_LUEFTERTEST erfolgreich |

<a id="job-lueftertest"></a>
### LUEFTERTEST

Reizen beenden, Fehlercode lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| HINWEIS | string | folgende Massnahmen |
| F_ORT_NR | long | Index für den Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text Table FOrteTexte als ORTTEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hex Code |
| _TEL_ANTWORT | binary | LUEFTERTEST erfolgreich |

<a id="job-init-dk-einstellen"></a>
### INIT_DK_EINSTELLEN

Initialisierung und reiz_k_line

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| HINWEIS | string | folgende Massnahmen |
| _TEL_ANTWORT | binary | INIT_DK_EINSTELLEN erfolgreich |

<a id="job-ende-dk-einstellen"></a>
### ENDE_DK_EINSTELLEN

Initialisierung und reiz_k_line

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| HINWEIS | string | folgende Massnahmen |
| _TEL_ANTWORT | binary | ENDE_DK_EINSTELLEN erfolgreich |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Deinitialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (10 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FORTTEXTE](#table-forttexte) (16 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 10 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | FEHLER |
| 0x02 | INITIALISIEREN VON ICOM_E FEHLGESCHLAGEN |
| 0x03 | LINIE SETZEN FEHLGESCHLAGEN |
| 0x04 | BLINKCODE LESEN FEHLGESCHLAGEN |
| 0x05 | INITIALISIEREN DER BLINKZAHLERFASSUNG FEHLGESCHLAGEN |
| 0x06 | BEENDEN DER BLINKZAHLERFASSUNG FEHLGESCHLAGEN |
| 0x07 | BEENDEN VON ICOM_E FEHLGESCHLAGEN |
| 0xFF | UNBEKANNTER FEHLER |
| 0xXY | ERROR_UNKNOWN |

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 6 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | Allgemeiner Fertigungs- und Energiesparmode | Hier deaktivierte Funktionen gemäß FeTra-Liste festhalten |
| 0x01 | Spezieller Energiesparmode | - |
| 0x02 | ECOS-Mode | - |
| 0x03 | MOST-Mode | - |
| 0x04 | Rollenmode | - |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 16 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x4444 | 4444 - kein Fehler gespeichert | 0 |
| 0x1111 | 1111 - CO-Potentiometer | 0 |
| 0x1122 | 1122 - Hallsignal 2 fehlt | 0 |
| 0x1133 | 1133 - Hallsignal 1 fehlt | 0 |
| 0x1223 | 1223 - Sensor Motortemperatur | 0 |
| 0x1224 | 1224 - Sensor Lufttemperatur | 0 |
| 0x1215 | 1215 - Drosselklappengeber | 0 |
| 0x2342 | 2342 - Signal Lambda-Sonde unrealistisch | 0 |
| 0x2341 | 2341 - Lambda-Regelgrenze erreicht | 0 |
| 0x2343 | 2343 - Anpassungsgrenze für Gemisch errreicht | 0 |
| 0x2344 | 2344 - Masseschluss Lambda-Sonde | 0 |
| 0x2345 | 2345 - Kurzschluss Lambda-Sonde nach Batterie(+) | 0 |
| 0x3333 | 3333 - Lüfteransteuerung | 0 |
| 0x0000 | 0000 - Kein weiterer Fehler gespeichert | 0 |
| 0x9999 | Falscher Fehlercode | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |
| F_HLZ_VIEW | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
