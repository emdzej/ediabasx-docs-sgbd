# EWS3D.prg

- Jobs: [34](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EWS3D |
| ORIGIN | BMW TI-433 Guecker |
| REVISION | 1.04 |
| AUTHOR | BMW TI-433 Mario Spoljarec, BMW TI-433 Andreas Guecker |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer EWS3 automatischer Aufruf beim ersten Zugriff auf SGBD
- [IDENT](#job-ident) - Ident-Daten fuer EWS3D
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [DIAGNOSE_FORTSETZEN](#job-diagnose-fortsetzen) - Diagnose mit EWS3D aufrecht erhalten
- [COD_LESEN](#job-cod-lesen) - Auslesen der Codierdaten der EWS3D
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten EWS3D in hex (4Bytes)
- [HERSTELLDATEN_SCHREIBEN](#job-herstelldaten-schreiben) - Beschreiben der Herstellerdaten
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [STATUS_LESEN](#job-status-lesen) - Stati der EWS
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern / Vorgeben digitaler Stati der EWS3D
- [ISN_LESEN](#job-isn-lesen) - Auslesen der ISN-Nummer aus der EWS
- [ISN_SCHREIBEN](#job-isn-schreiben) - Schreiben der ISN-Nummer in die EWS
- [WECHSELCODE_SYNC_DME](#job-wechselcode-sync-dme) - Wechselcodesynchronisation EWS 3 - DME anstossen
- [SCHL_SPERREN_FREIGEBEN](#job-schl-sperren-freigeben) - Schluessel freischalten und sperren
- [PASSWORT_LESEN](#job-passwort-lesen) - Auslesen des Passworts aus der EWS
- [PASSWORT_SCHREIBEN](#job-passwort-schreiben) - Schreiben des Passworts in die EWS
- [SCHL_DATEN_LESEN](#job-schl-daten-lesen) - Auslesen der Schluesseldaten aus der EWS
- [SCHL_DATEN_SCHREIBEN](#job-schl-daten-schreiben) - Schreiben der Schluesseldaten in die EWS
- [KD_DATEN_LESEN](#job-kd-daten-lesen) - Auslesen der Kundendienstdaten aus der EWS
- [KD_DATEN_SCHREIBEN](#job-kd-daten-schreiben) - Schreiben der Kundendienst in die EWS
- [KD_INIT](#job-kd-init) - Schreiben der VK-Daten in das EWS
- [FGNR_LESEN](#job-fgnr-lesen) - Auslesen der Fahrgestellnummer aus der EWS
- [FGNR_SCHREIBEN](#job-fgnr-schreiben) - Schreiben der 17-stelligen Fahrgestellnummer inkl. PZ
- [FGNR_K_SCHREIBEN](#job-fgnr-k-schreiben) - Schreiben der 7-stelligen Fahrgestellnummer
- [ZCS_LESEN](#job-zcs-lesen) - Auslesen des Zentralen Codierschluessels aus KD-Daten
- [SCHLUESSEL_DATEN_0_BIS_3_LESEN](#job-schluessel-daten-0-bis-3-lesen) - Auslesen der Schluesseldaten aus der EWS
- [COD_ZEIT_WS_SCHREIBEN](#job-cod-zeit-ws-schreiben) - Schreiben der Schaerfzeit der WS
- [COD_EWS_DME3_SCHREIBEN](#job-cod-ews-dme3-schreiben) - Schreiben der Schaerfzeit der WS
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Schreibzugriff auf den Transponder via EWS-SG
- [STATUS_SW_VERSION](#job-status-sw-version) - Ermittlung der internen SG-SW

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

Init-Job fuer EWS3 automatischer Aufruf beim ersten Zugriff auf SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer EWS3D

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

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Wertebereich 0 - 31 |
| F_ART_ANZ | int | immer 1 |
| F_UW_ANZ | int | immer 0 |
| F_ART1_NR | int | momentan identisch Art-Bit |
| F_ART1_TEXT | string | Fehlerart als Text table FArtTexte ARTTEXT |
| _TEL_ANTWORT0 | binary |  |
| _TEL_ANTWORT1 | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

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

<a id="job-diagnose-fortsetzen"></a>
### DIAGNOSE_FORTSETZEN

Diagnose mit EWS3D aufrecht erhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-cod-lesen"></a>
### COD_LESEN

Auslesen der Codierdaten der EWS3D

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN | string | 5 Codierbytes |
| COD_GETRIEBE | string | Schaltgetriebe oder Automatik |
| COD_DME_SS | int | 2 oder 3 |
| COD_ABSCHALTDREHZAHL | real | (5 bis 254)/0.3 1/s |
| COD_ABSCHALTZEIT | real | (1 bis 255)*2 s |
| COD_ZEIT_WS_SCHAERFEN | int | 0 bis 255 s |
| COD_WEITERSCHALTSCHWELLE | string | 0 bis 255 (Dummyergebnis bei DME-Schnittstelle 2) |
| _TEL_ANTWORT | binary |  |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen der Herstelldaten EWS3D in hex (4Bytes)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| BYTE4 | int | kann beliebig verwendet werden |
| _TEL_ANTWORT | binary |  |

<a id="job-herstelldaten-schreiben"></a>
### HERSTELLDATEN_SCHREIBEN

Beschreiben der Herstellerdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| BYTE4 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

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

<a id="job-status-lesen"></a>
### STATUS_LESEN

Stati der EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ANLASSER_FREIGESCHALTET | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ANLASSER_AUS_DREHZAHL | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ANLASSER_AUS_P_N | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ANLASSER_AUS_ZV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ANLASSER_AUS_BC | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_WEITERE_SELBSTINIT_KEYS | int | 1, noch nicht alle zur Selbstinitialisierung freigeschalteten Schluessel initialisiert |
| STAT_DME_LEITUNG_FREI | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_EWS_JUNGFRAEULICH | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_P_N_EINGANG | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_KL_R_EINGANG | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_ZV_GESICHERT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_BC_CODE | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_MOTORDREHZAHL | real | (5 bis 254)/0.3 1/s |
| STAT_SCHLUESSEL_SENDET | int | 0, wenn FALSE / 1, Datenformat stimmt, Schluessel wird identifiziert |
| STAT_SCHLUESSEL_GESPERRT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SCHLUESSEL_NIO_ID | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SCHLUESSEL_NIO_PW | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SCHLUESSEL_NIO_WC | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_AKTUELLE_SCHLUESSELNUMMER | int | 0 bis 9 (aus der ID berechnet) |
| STAT_AKTUELLE_SCHLUESSEL_ID | binary | 10 Bytes vom Block 3 im Schluessel |
| STAT_AKTUELLE_SCHLUESSEL_ID_TEXT | string | 8 Byte |
| STAT_AKTUELLER_WC | binary | 12 Byte |
| STAT_AKTUELLER_WC_TEXT | string | 12 Byte |
| STAT_VORGABE_DME | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VORGABE_ANLASSERRELAIS | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VORGABE_DME_AUSFUEHREN | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VORGABE_ANLASSERRELAIS_AUSFUEHREN | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_UNLOCK_VORGABEWERT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_VORGABE_UNLOCK_AUSFUEHREN | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern / Vorgeben digitaler Stati der EWS3D

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT1 | string | 1. Signal table BITS NAME MASK TEXT |
| ORT2 | string | 2. Signal |
| ORT3 | string | 3. Signal |
| ORT4 | string | 4. Signal |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-isn-lesen"></a>
### ISN_LESEN

Auslesen der ISN-Nummer aus der EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| ISN | string | 16 Bit |
| _TEL_ANTWORT | binary |  |

<a id="job-isn-schreiben"></a>
### ISN_SCHREIBEN

Schreiben der ISN-Nummer in die EWS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ISN | string | 16 Bit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-wechselcode-sync-dme"></a>
### WECHSELCODE_SYNC_DME

Wechselcodesynchronisation EWS 3 - DME anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-schl-sperren-freigeben"></a>
### SCHL_SPERREN_FREIGEBEN

Schluessel freischalten und sperren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NUMMER | int | 0 bis 9 |
| FREIGABE | int | 0 : sperren / &gt;0 : freischalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-passwort-lesen"></a>
### PASSWORT_LESEN

Auslesen des Passworts aus der EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| PASSWORT | binary | 6 Byte |
| PASSWORT_TEXT | string | 6 Byte |
| _TEL_ANTWORT | binary |  |

<a id="job-passwort-schreiben"></a>
### PASSWORT_SCHREIBEN

Schreiben des Passworts in die EWS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PASSWORT | string | 6 Byte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-schl-daten-lesen"></a>
### SCHL_DATEN_LESEN

Auslesen der Schluesseldaten aus der EWS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NUMMER | int | 0 bis 9 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| SCHL_NUMMER | int | 0 bis 9 |
| SCHL_IDENT | binary | 8 Byte |
| SCHL_IDENT_TEXT | string | 8 Byte |
| SCHL_FREIGABE | int | 0 - 3 |
| SCHL_FREIGABE_TEXT | string | gesperrt oder freigeschaltet |
| SCHL_SELBSTINIT_ERFOLGT | int | 1-&gt;Selbstprogrammierung des Schluessels ist erfolgt |
| SCHL_SELBSTINIT | int | 0-&gt;false, 1-&gt;Selbstprogrammierung des Schluessels durch das SG |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-schl-daten-schreiben"></a>
### SCHL_DATEN_SCHREIBEN

Schreiben der Schluesseldaten in die EWS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHL_NUMMER | int | 0 bis 9 |
| SCHL_IDENT | string | 8 Byte |
| SCHL_FREIGABE | int | Bit 1 : freischalten Bit 7: selbstinit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

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

<a id="job-kd-daten-schreiben"></a>
### KD_DATEN_SCHREIBEN

Schreiben der Kundendienst in die EWS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KD_BLOCK | int | 0 bis 11 |
| KD_DATEN | string | 16 Byte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-kd-init"></a>
### KD_INIT

Schreiben der VK-Daten in das EWS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VK_STRING | string | VK-Daten-String bis zu 222 Byte Laenge, es erfolgt derzeit keine Bearbeitung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-fgnr-lesen"></a>
### FGNR_LESEN

Auslesen der Fahrgestellnummer aus der EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |
| FG_PZ | string | Pruefziffer der Fahrgestellnummer inkl. FP nach Modulo 36 berechnet |
| _TEL_ANTWORT | binary |  |

<a id="job-fgnr-schreiben"></a>
### FGNR_SCHREIBEN

Schreiben der 17-stelligen Fahrgestellnummer inkl. PZ

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (17-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-fgnr-k-schreiben"></a>
### FGNR_K_SCHREIBEN

Schreiben der 7-stelligen Fahrgestellnummer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (7-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-zcs-lesen"></a>
### ZCS_LESEN

Auslesen des Zentralen Codierschluessels aus KD-Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| GM | string | Zentralcode C1 - Grundmerkmal |
| SA | string | Zentralcode C2 - Sonderausstattung |
| VM | string | Zentralcode C3 - Versionsmerkmal |
| C3 | string | Zentralcode C3 - ohne Prefix |
| _TEL_ANTWORT1 | binary |  |
| _TEL_ANTWORT2 | binary |  |

<a id="job-schluessel-daten-0-bis-3-lesen"></a>
### SCHLUESSEL_DATEN_0_BIS_3_LESEN

Auslesen der Schluesseldaten aus der EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| SCHL0_FREIGABE | int | 0 - 3 |
| SCHL0_FREIGABE_TEXT | string | gesperrt oder freigeschaltet |
| SCHL1_FREIGABE | int | 0 - 3 |
| SCHL1_FREIGABE_TEXT | string | gesperrt oder freigeschaltet |
| SCHL2_FREIGABE | int | 0 - 3 |
| SCHL2_FREIGABE_TEXT | string | gesperrt oder freigeschaltet |
| SCHL3_FREIGABE | int | 0 - 3 |
| SCHL3_FREIGABE_TEXT | string | gesperrt oder freigeschaltet |

<a id="job-cod-zeit-ws-schreiben"></a>
### COD_ZEIT_WS_SCHREIBEN

Schreiben der Schaerfzeit der WS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT_WS | int | Schaerfzeit der WS in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-cod-ews-dme3-schreiben"></a>
### COD_EWS_DME3_SCHREIBEN

Schreiben der Schaerfzeit der WS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Schreibzugriff auf den Transponder via EWS-SG

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | int | 0 bis 7, Transponderblocknummer |
| POSITION | int | 0 bis 15, Byteposition innerhalb des Blocks |
| DATENBYTE | int | Datenbyte fuer den Transponder |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| TRANSP_DATEN | binary | 16 Byte |
| TRANSP_DATEN_TEXT | string | 16 Byte |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-status-sw-version"></a>
### STATUS_SW_VERSION

Ermittlung der internen SG-SW

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BETRIEBSSYSTEM | string | Betriebssystemversion |
| EEPROM_TREIBER | string | EEPROM-Treiber-Verion |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)
- [FORTTEXTE](#table-forttexte) (49 × 2)
- [FARTTEXTE](#table-farttexte) (2 × 2)
- [BITS](#table-bits) (9 × 3)

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
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 27 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 49 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Schluessel Nr.0 ungueltig wegen fehlerhafter Identifikation |
| 0x10 | Schluessel Nr.1 ungueltig wegen fehlerhafter Identifikation |
| 0x20 | Schluessel Nr.2 ungueltig wegen fehlerhafter Identifikation |
| 0x30 | Schluessel Nr.3 ungueltig wegen fehlerhafter Identifikation |
| 0x40 | Schluessel Nr.4 ungueltig wegen fehlerhafter Identifikation |
| 0x50 | Schluessel Nr.5 ungueltig wegen fehlerhafter Identifikation |
| 0x60 | Schluessel Nr.6 ungueltig wegen fehlerhafter Identifikation |
| 0x70 | Schluessel Nr.7 ungueltig wegen fehlerhafter Identifikation |
| 0x80 | Schluessel Nr.8 ungueltig wegen fehlerhafter Identifikation |
| 0x90 | Schluessel Nr.9 ungueltig wegen fehlerhafter Identifikation |
| 0x01 | Schluessel Nr.0 ungueltig wegen fehlerhaftem Passwort |
| 0x11 | Schluessel Nr.1 ungueltig wegen fehlerhaftem Passwort |
| 0x21 | Schluessel Nr.2 ungueltig wegen fehlerhaftem Passwort |
| 0x31 | Schluessel Nr.3 ungueltig wegen fehlerhaftem Passwort |
| 0x41 | Schluessel Nr.4 ungueltig wegen fehlerhaftem Passwort |
| 0x51 | Schluessel Nr.5 ungueltig wegen fehlerhaftem Passwort |
| 0x61 | Schluessel Nr.6 ungueltig wegen fehlerhaftem Passwort |
| 0x71 | Schluessel Nr.7 ungueltig wegen fehlerhaftem Passwort |
| 0x81 | Schluessel Nr.8 ungueltig wegen fehlerhaftem Passwort |
| 0x91 | Schluessel Nr.9 ungueltig wegen fehlerhaftem Passwort |
| 0x02 | Schluessel Nr.0 ungueltig wegen fehlerhaftem Wechselcode |
| 0x12 | Schluessel Nr.1 ungueltig wegen fehlerhaftem Wechselcode |
| 0x22 | Schluessel Nr.2 ungueltig wegen fehlerhaftem Wechselcode |
| 0x32 | Schluessel Nr.3 ungueltig wegen fehlerhaftem Wechselcode |
| 0x42 | Schluessel Nr.4 ungueltig wegen fehlerhaftem Wechselcode |
| 0x52 | Schluessel Nr.5 ungueltig wegen fehlerhaftem Wechselcode |
| 0x62 | Schluessel Nr.6 ungueltig wegen fehlerhaftem Wechselcode |
| 0x72 | Schluessel Nr.7 ungueltig wegen fehlerhaftem Wechselcode |
| 0x82 | Schluessel Nr.8 ungueltig wegen fehlerhaftem Wechselcode |
| 0x92 | Schluessel Nr.9 ungueltig wegen fehlerhaftem Wechselcode |
| 0x03 | WC-Toleranz erhoeht bei Schluessel Nummer 0 |
| 0x13 | WC-Toleranz erhoeht bei Schluessel Nummer 1 |
| 0x23 | WC-Toleranz erhoeht bei Schluessel Nummer 2 |
| 0x33 | WC-Toleranz erhoeht bei Schluessel Nummer 3 |
| 0x43 | WC-Toleranz erhoeht bei Schluessel Nummer 4 |
| 0x53 | WC-Toleranz erhoeht bei Schluessel Nummer 5 |
| 0x63 | WC-Toleranz erhoeht bei Schluessel Nummer 6 |
| 0x73 | WC-Toleranz erhoeht bei Schluessel Nummer 7 |
| 0x83 | WC-Toleranz erhoeht bei Schluessel Nummer 8 |
| 0x93 | WC-Toleranz erhoeht bei Schluessel Nummer 9 |
| 0xFF | Reset allgemein |
| 0x0F | Power-On-Reset |
| 0x1F | Clock-Monitor-Reset |
| 0x2F | Watchdog-Reset |
| 0x3F | Illegal-Opcode-Trap |
| 0x7F | Software-Interrupt |
| 0x0E | DME-Wechselcode XOR-Fehler |
| 0x1E | DME-Wechselcode verloren |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 2 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |

<a id="table-bits"></a>
### BITS

Dimensions: 9 rows × 3 columns

| NAME | MASK | TEXT |
| --- | --- | --- |
| DME_V | 0x01 | Vorgabe DME-Leitung |
| ANL_V | 0x02 | Vorgabe Anlasserrelais |
| TRP_V | 0x04 | Vorgabe Transponder |
| USE_V | 0x08 | Vorgabe Gebrauchen |
| DME_A | 0x10 | Vorgabe DME-Leitung ausfuehren |
| ANL_A | 0x20 | Vorgabe Anlasserrelais ausfuehren |
| TRP_A | 0x40 | Vorgabe Transponder ausfuehren |
| USE_A | 0x80 | Vorgabe Gebrauchen ausfuehren |
| XY | 0xXY | nicht definiertes Signal |
