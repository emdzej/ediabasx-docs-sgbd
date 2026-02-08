# FUNKKOMP.prg

- Jobs: [18](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Funk-kompakt Schliess-System |
| ORIGIN | BMW TP-422 Teepe |
| REVISION | 1.33 |
| AUTHOR | BMW TP-422 Teepe |
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
- [STATUS_LESEN](#job-status-lesen) - Auslesen der IO-Ports
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [TEST_FUNK_STRECKE](#job-test-funk-strecke) - Status des letzten, vor Kl.R ein empfangenen Telegramms
- [CODIERUNG_LESEN](#job-codierung-lesen) - Codierdaten
- [LAENDERCODIERUNG_LESEN](#job-laendercodierung-lesen) - Codierdaten
- [BATTERIE_MELDUNG_LESEN](#job-batterie-meldung-lesen) - Status der Batteriemeldung
- [BATTERIE_MELDUNG_LOESCHEN](#job-batterie-meldung-loeschen) - Loeschen der Batteriemeldung
- [RAM_LESEN](#job-ram-lesen) - Auslesen des RAM-Bereiches
- [EEPROM_LESEN](#job-eeprom-lesen) - Auslesen des EEPROM-Bereiches
- [STEUERN_IO](#job-steuern-io) - Ansteuern der IO-Ports
- [INIT_SPERRE_SCHREIBEN](#job-init-sperre-schreiben) - Aufheben der Initialisiersperre
- [FUNKTIONSSPERRE_SCHREIBEN](#job-funktionssperre-schreiben) - Setzen der Funktionssperre
- [FUNKTIONSSPERRE_AUFHEBEN](#job-funktionssperre-aufheben) - Aufheben der Funktionssperre

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
| ID_GEN_NR | string | Generationsnummer |
| ID_HW_NR | string | Hardwarenummer |
| ID_SW_NR | string | Softwarenummer |
| ID_PP_NR | string | Pruefplannummer |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| F_ORT_NR | int | Nr des Fehlers (entspricht dem Fehlercode) |
| F_ORT_TEXT | string | Fehlertext |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int | Textindex fuer Fehlerart 1 |
| F_ART1_TEXT | string | Text fuer Fehlerart 1 |
| F_ART2_NR | int | Textindex fuer Fehlerart 2 |
| F_ART2_TEXT | string | Text fuer Fehlerart 2 |
| F_ART3_NR | int | Textindex fuer Fehlerart 3 |
| F_ART3_TEXT | string | Text fuer Fehlerart 3 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ZAHL | int | Anzahl der Fehler |
| F_HFK | int | Haeufigkeit des Einzelfehler |
| F_HEX_CODE | binary | Hex-Werte des Einzelfehler |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Auslesen der IO-Ports

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_ZS2_EIN | int | Status von ZS2, 0 oder 1 |
| STAT_VR_EIN | int | Status von VR, 0 oder 1 |
| STAT_ZS22_EIN | int | Status von ZS22, 0 oder 1 |
| STAT_TGK_EIN | int | Status Tuergriffkontakt, 0 oder 1 |
| STAT_KLEMME_R_EIN | int | Status von Klemme R, 0 oder 1 |
| STAT_UNTERSPANNUNG_AUS | int | Status Unterspannungserkennung, 0 oder 1 |
| STAT_RxD_EIN | int | Status von RxD, 0 oder 1 |
| STAT_EMPFAENGERDATEN_EIN | int | Status der Empfaengerdaten, 0 oder 1 |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-test-funk-strecke"></a>
### TEST_FUNK_STRECKE

Status des letzten, vor Kl.R ein empfangenen Telegramms

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_FUNK_STRECKE | string | Liefert: IN_ORDNUNG, FALSCHE_DATEN, NICHT_EMPFANGEN, UNBEKANNT |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| FUNKTIONSSPERRE_AKTIV | int | Liefert: 0 oder 1 |
| CODIERUNG_FUNKTIONSSPERRE_AKTIV | int | Liefert: 0 oder 1 |
| INITIALISIERUNGSSPERRE_AKTIV | int | Liefert: 0 oder 1 |
| IMPULSAUSGABEZEIT_WERT | int | Liefert: 0 bis 12,75 |
| IMPULSAUSGABEZEIT_EINH | string | Liefert: "s" |
| PAUSENZEIT_WERT | int | Liefert: 0 bis 12,75 |
| PAUSENZEIT_EINH | string | Liefert: "s" |
| SPERRZEIT_WERT | int | Liefert: 0 bis 12,75 |
| SPERRZEIT_EINH | string | Liefert: "s" |
| CODIERUNG_TASTE1 | string | Liefert: "VERRIEGELN","ENTRIEGELN","INNENLICHT/PANICMODE" |
| CODIERUNG_TASTE2 | string | Liefert: "VERRIEGELN","ENTRIEGELN","INNENLICHT/PANICMODE" |
| CODIERUNG_TASTE3 | string | Liefert: "VERRIEGELN","ENTRIEGELN","INNENLICHT/PANICMODE" |
| PANIC_MODE_AKTIV | int | Liefert: 0 oder 1 |
| PANIC_MODE_AUSLOESEZEIT_WERT | int | Liefert: 0 bis 12,75 |
| PANIC_MODE_AUSLOESEZEIT_EINH | string | Liefert: s (Sekunden) |
| ZS_OHNE_VR_CODIERT | int | Liefert: 0 oder 1 Sichern mit oder ohne vorheriges Verriegeln |
| KOMFORT_OEFFNEN | string | Liefert: aktiv, inaktiv, begrenzt |
| KOMFORT_SCHLIESSEN | string | Liefert: aktiv, inaktiv, begrenzt |
| LAENDER_FREQUENZ | string | Liefert: USA, ECE, unkekannt |

<a id="job-laendercodierung-lesen"></a>
### LAENDERCODIERUNG_LESEN

Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| PANIC_MODE_CODIERT | int | Liefert: 0 oder 1 |
| ZS_OHNE_VR_CODIERT | int | Liefert: 0 oder 1 Sichern mit oder ohne vorheriges Verriegeln |
| PANIC_MODE_AUSLOESEZEIT_WERT | int | Liefert: 0 bis 12,75 |
| PANIC_MODE_AUSLOESEZEIT_EINH | string | Liefert: s (Sekunden) |
| KOMFORT_OEFFNEN | string | Liefert: aktiv, inaktiv, begrenzt |
| KOMFORT_SCHLIESSEN | string | Liefert: aktiv, inaktiv, begrenzt |
| LAENDER_FREQUENZ | string | Liefert: USA, ECE, unkekannt |

<a id="job-batterie-meldung-lesen"></a>
### BATTERIE_MELDUNG_LESEN

Status der Batteriemeldung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| BATTERIE_SCHLUESSEL_1 | string | Liefert: IO, NICHT_IO, UNBEKANNT |
| BATTERIE_SCHLUESSEL_2 | string | Liefert: IO, NICHT_IO, UNBEKANNT |
| BATTERIE_SCHLUESSEL_3 | string | Liefert: IO, NICHT_IO, UNBEKANNT |
| BATTERIE_SCHLUESSEL_4 | string | Liefert: IO, NICHT_IO, UNBEKANNT |

<a id="job-batterie-meldung-loeschen"></a>
### BATTERIE_MELDUNG_LOESCHEN

Loeschen der Batteriemeldung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-ram-lesen"></a>
### RAM_LESEN

Auslesen des RAM-Bereiches

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | Anzahl Bytes von 1 (0x01) bis 112 (0x70) |
| ADRESSE | int | Startadresse LSB |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| DATENBEREICH | binary | Liefert: Hexdump |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

Auslesen des EEPROM-Bereiches

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | Anzahl Bytes von 1 (0x01) bis 255 (0xFF) |
| ADRESSE | int | Startadresse LSB |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK, ERROR_ARGUMENT |
| DATENBEREICH | binary | Liefert: Hexdump |

<a id="job-steuern-io"></a>
### STEUERN_IO

Ansteuern der IO-Ports

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PIN | string | anzusteuernder Ausgang als String moeglich sind: ZS2, VR, ZS22, TGK, ENTRIEGELN, VERRIEGELN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK, ERROR_ARGUMENT |

<a id="job-init-sperre-schreiben"></a>
### INIT_SPERRE_SCHREIBEN

Aufheben der Initialisiersperre

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-funktionssperre-schreiben"></a>
### FUNKTIONSSPERRE_SCHREIBEN

Setzen der Funktionssperre

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK |
| FUNKTIONSSPERRE | string | Liefert: aktiv, inaktiv, nicht moeglich |

<a id="job-funktionssperre-aufheben"></a>
### FUNKTIONSSPERRE_AUFHEBEN

Aufheben der Funktionssperre

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK |
| FUNKTIONSSPERRE | string | Liefert: aufgehoben, nicht aufgehoben, nicht moeglich |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (5 × 2)
- [FARTTEXTE](#table-farttexte) (9 × 2)
- [STEUERN](#table-steuern) (7 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 5 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Signal ZS2 |
| 0x02 | Signal VR |
| 0x03 | Signal ZS22 |
| 0x04 | Tuergriffkontakt TGK |
| 0x05 | EEPROM |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 9 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Kurzschluss gegen U-Batt |
| 0x01 | Kurzschluss gegen Masse |
| 0x02 | Leitungsunterbrechung |
| 0x03 | ungueltiger Arbeitsbereich |
| 0x04 | sporadischer Fehler |
| 0x05 | statischer Fehler |
| 0x06 | Fehler momentan nicht vorhanden |
| 0x07 | Fehler momentan vorhanden |
| 0xFF | unbekannte Fehlerart |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 7 rows × 2 columns

| PIN | AUSGANG |
| --- | --- |
| 0x52 | ZS2 |
| 0x32 | VR |
| 0x42 | ZS22 |
| 0x62 | TGK |
| 0xF6 | ENTRIEGELN |
| 0xF1 | VERRIEGELN |
| 0xFF | unbekannt |
