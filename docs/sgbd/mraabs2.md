# mraabs2.prg

- Jobs: [26](#jobs)
- Tables: [16](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ABS Steuergerät ABS2 |
| ORIGIN | I+ME Actia GmbH, Keck |
| REVISION | 1.070 |
| AUTHOR | I+ME Actia GmbH, Keck und BMW Motorrad, Kufer |
| COMMENT | N/A |
| PACKAGE | 1.52 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [START_KOMMUNIKATION](#job-start-kommunikation)
- [STOP_KOMMUNIKATION](#job-stop-kommunikation) - Beenden der Diagnose
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht)
- [BAUDRATE_SETZEN](#job-baudrate-setzen)
- [FS_LESEN](#job-fs-lesen)
- [FS_LOESCHEN](#job-fs-loeschen)
- [IDENT](#job-ident) - Steuergeräte Identifikation lesen
- [SG_SOFTWARESTAND](#job-sg-softwarestand)
- [STATUS_ABS_TASTER](#job-status-abs-taster) - Status ABS Quittiertaste auslesen
- [STATUS_CODIERUNG_KABELBAUM](#job-status-codierung-kabelbaum) - Kodierung Kabelbaum auslesen
- [STATUS_CODIERUNG_EEPROM](#job-status-codierung-eeprom) - Codierung EEPROM auslesen
- [STATUS_SENSORFREQUENZ](#job-status-sensorfrequenz) - Raddrehzahlfrequenzen auslesen
- [STATUS_RADGESCHWINDIGKEIT](#job-status-radgeschwindigkeit)
- [STATUS_EEPROM_LESEN](#job-status-eeprom-lesen)
- [STATUS_ANALOG_WERTE](#job-status-analog-werte) - Auslesen von analogen Messwerten
- [STEUERN_WARNLAMPE_1](#job-steuern-warnlampe-1) - Testbrett Lampe W, Warnlampe 1, Warnlampen Relais (Öffner)
- [STEUERN_WARNLAMPE_2](#job-steuern-warnlampe-2) - Testbrett Lampe K, Warnlampe 2
- [STEUERN_WARNLAMPE_ZURUECKSETZEN](#job-steuern-warnlampe-zuruecksetzen) - Hardware TestModus ausschalten, für Warnlampe 1, 2
- [STEUERN_WARNLAMPEN_TEST](#job-steuern-warnlampen-test) - Testbrett Lampe K, Warnlampe 2 Testbrett Lampe W, Warnlampe 1, Warnlampen Relais (Öffner)
- [STEUERN_FMW_TEST](#job-steuern-fmw-test) - FMW - Find Maximum Way Vorderrad und Hinterrad PWM/Weg Kennlinie, Spec Punkt 4.9.1
- [STEUERN_ELG_TEST](#job-steuern-elg-test) - ELG - Entlastungsgradient Vorderrad und Hinterrad Spec Punkt 4.9.2
- [STEUERN_PUMPENMOTOR](#job-steuern-pumpenmotor) - Pumpenmotor ansteuern Messung der Batteriespannung unter Last Angabe Parameter Zeit ist optional Spec Punkt 4.5
- [STEUERN_ABS_RELAIS](#job-steuern-abs-relais) - Messung Motor Relais Schließzeit Spec Punkt 4.9.3
- [STEUERN_CODIERUNG_EEPROM_LOESCHEN](#job-steuern-codierung-eeprom-loeschen) - Codierung EEPROM löschen

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

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-start-kommunikation"></a>
### START_KOMMUNIKATION

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-stop-kommunikation"></a>
### STOP_KOMMUNIKATION

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-baudrate-setzen"></a>
### BAUDRATE_SETZEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BAUDRATEN_WERT | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANFRAGE | binary | Hex Antwort zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers für KWP-2000 immer 2 |
| F_ANZAHL | int | Anzahl der Fehler im Speicher |
| F_ORT_NR | unsigned char | Index für den Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text Table FOrteTexte als ORTTEXT |
| F_SYMPTOM_NR | int | Index für die Fehlerart |
| F_SYMPTOM_TEXT | string | Fehlerart als Text Table FArtTexte als ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard Fehlerart) als Text |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard Fehlerart) als Text Fehlerart table ArtTexte als Text |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard Fehlerart) als Text |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hex Code |
| FEHLERCODE_MASTER_DUMP | binary |  |
| FEHLERCODE_SLAVE_DUMP | binary |  |
| FEHLERCODE_EEPROM_DUMP | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-ident"></a>
### IDENT

Steuergeräte Identifikation lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT1 | binary | Hex Antwort vom SG |
| _TEL_ANTWORT2 | binary | Hex Antwort vom SG |
| SG_NR | int | Steuergeräte Nr |
| JAHR | int | Herstellungsjahr |
| KALENDERWOCHE | int | Kalenderwoche |
| HERSTELLERCODE | int | Hersteller Index |
| HERSTELLER_TEXT | string | Hersteller |
| AENDERUNGSINDEX | int | Änderungsindex der ABS Baustufe |
| SG_KENNZEICHEN | int | Kennzeichnung Steuergerät |
| VARIANTE_IND | string | Name der SGBD, hier immer MRAABS2 |

<a id="job-sg-softwarestand"></a>
### SG_SOFTWARESTAND

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_CODE_VERSION | string | Software Version |
| ID_DATUM | string | Herstell Datum Tag.Monat.Jahr |
| ISO_DATENSTAND | string | ISO Datenstand |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-abs-taster"></a>
### STATUS_ABS_TASTER

Status ABS Quittiertaste auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STATUS_WERT | int | Wert als Zahl |
| STATUS_TASTER_TEXT | string | EIN/AUS |

<a id="job-status-codierung-kabelbaum"></a>
### STATUS_CODIERUNG_KABELBAUM

Kodierung Kabelbaum auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STATUS_CODIERUNG | int | Codierung als Zahl |
| STATUS_CODIERUNG_TEXT | string | Codierung als Text table KabelCodierung |

<a id="job-status-codierung-eeprom"></a>
### STATUS_CODIERUNG_EEPROM

Codierung EEPROM auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STATUS_CODIERUNG | int | Codierung als Zahl |
| STATUS_CODIERUNG_TEXT | string | Codierung als Text table KabelCodierung |

<a id="job-status-sensorfrequenz"></a>
### STATUS_SENSORFREQUENZ

Raddrehzahlfrequenzen auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ADRESSE | binary | Hex Antwort vom SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| FREQUENZ_VORDERRAD_WERT | int |  |
| FREQUENZ_VORDERRAD_EINH | string |  |
| FREQUENZ_HINTERRAD_WERT | int |  |
| FREQUENZ_HINTERRAD_EINH | string |  |

<a id="job-status-radgeschwindigkeit"></a>
### STATUS_RADGESCHWINDIGKEIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ADRESSE | binary | Hex Antwort vom SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| RAD_GESCHW_VORN_WERT | real | Rad Geschwindigkeit vorn |
| RAD_GESCHW_HINTEN_WERT | real | Rad Geschwindigkeit vorn |
| RAD_GESCHW_VORN_EINH | string | Einheit Geschwindigkeit vorn in km/h |
| RAD_GESCHW_HINTEN_EINH | string | Einheit Geschwindigkeit hinten in km/h |

<a id="job-status-eeprom-lesen"></a>
### STATUS_EEPROM_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| EEPROM_HEXDUMP | binary | Hexdump von 0x00-0x7f, wortweise High Byte, Low Byte |

<a id="job-status-analog-werte"></a>
### STATUS_ANALOG_WERTE

Auslesen von analogen Messwerten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| KLEMME_30_WERT | real |  |
| KLEMME_30_EINH | string |  |
| SPANNUNG_VORDERRAD_WERT | real |  |
| SPANNUNG_VORDERRAD_EINH | string |  |
| SPANNUNG_HINTERRAD_WERT | real |  |
| SPANNUNG_HINTERRAD_EINH | string |  |
| KLEMME_15_WERT | real |  |
| KLEMME_15_EINH | string |  |
| ANTWORT1 | binary |  |
| ANTWORT2 | binary |  |

<a id="job-steuern-warnlampe-1"></a>
### STEUERN_WARNLAMPE_1

Testbrett Lampe W, Warnlampe 1, Warnlampen Relais (Öffner)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | string | Ein, Aus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Antwort vom SG |

<a id="job-steuern-warnlampe-2"></a>
### STEUERN_WARNLAMPE_2

Testbrett Lampe K, Warnlampe 2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | string | Ein, Aus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Antwort vom SG |

<a id="job-steuern-warnlampe-zuruecksetzen"></a>
### STEUERN_WARNLAMPE_ZURUECKSETZEN

Hardware TestModus ausschalten, für Warnlampe 1, 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-steuern-warnlampen-test"></a>
### STEUERN_WARNLAMPEN_TEST

Testbrett Lampe K, Warnlampe 2 Testbrett Lampe W, Warnlampe 1, Warnlampen Relais (Öffner)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-fmw-test"></a>
### STEUERN_FMW_TEST

FMW - Find Maximum Way Vorderrad und Hinterrad PWM/Weg Kennlinie, Spec Punkt 4.9.1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| FEHLERCODE | unsigned long | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-steuern-elg-test"></a>
### STEUERN_ELG_TEST

ELG - Entlastungsgradient Vorderrad und Hinterrad Spec Punkt 4.9.2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ENTLASTUNGSZEIT_VORDERRAD | real | Entlastungszeit Vorderrad in ms Zeit 60 ... 105 ms |
| ENTLASTUNGSZEIT_HINTERRAD | real | Entlastungszeit Hinterrad in ms Zeit 60 ... 105 ms |
| ENTLASTUNGSZEIT_EINHEIT | string | Einheit Entlastungszeit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-steuern-pumpenmotor"></a>
### STEUERN_PUMPENMOTOR

Pumpenmotor ansteuern Messung der Batteriespannung unter Last Angabe Parameter Zeit ist optional Spec Punkt 4.5

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | int | Zeit in Sekunden, max. 20 Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| KLEMME_30_MAX_WERT | real | maximal gemessene Batteriespannung |
| KLEMME_30_MAX_EINH | string |  |
| KLEMME_30_MIN_WERT | real | minimal gemessene Batteriespannung |
| KLEMME_30_MIN_EINH | string |  |

<a id="job-steuern-abs-relais"></a>
### STEUERN_ABS_RELAIS

Messung Motor Relais Schließzeit Spec Punkt 4.9.3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-codierung-eeprom-loeschen"></a>
### STEUERN_CODIERUNG_EEPROM_LOESCHEN

Codierung EEPROM löschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (57 × 2)
- [FARTTEXTE](#table-farttexte) (9 × 2)
- [FEHLERCODETEST](#table-fehlercodetest) (3 × 2)
- [FEHLERSTATUS](#table-fehlerstatus) (5 × 2)
- [WARNLAMPE](#table-warnlampe) (3 × 2)
- [JOBRESULT](#table-jobresult) (7 × 2)
- [FMW_TEST](#table-fmw-test) (8 × 2)
- [ELG_TEST](#table-elg-test) (7 × 2)
- [MOT_TEST](#table-mot-test) (6 × 2)
- [PUMPENMOTOR](#table-pumpenmotor) (5 × 2)
- [STATUSWARNLAMPE](#table-statuswarnlampe) (5 × 2)
- [KABELCODIERUNG](#table-kabelcodierung) (11 × 2)
- [BAUDRATE](#table-baudrate) (17 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (3 × 2)
- [RESPONSECODE](#table-responsecode) (7 × 2)
- [LIEFERANTEN](#table-lieferanten) (81 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 57 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Warnlampen defekt |
| 0x02 | Sensor Vorderrad |
| 0x03 | Sensor Hinterrad |
| 0x04 | Laufzeit ABS-Motor zu lang |
| 0x05 | ISO defekt |
| 0x06 | Fahrzeugkodierung falsch |
| 0x07 | Interne Störung |
| 0x08 | Überlastung Modulator |
| 0x09 | Regelgüte Lageregler |
| 0x0A | ABS-Kolben Vorderrad |
| 0x0B | Sensorversorgung |
| 0x0C | ABS-Kolben Hinterrad |
| 0x0D | Plungertestfehler |
| 0x0E | Elektronikfehler |
| 0x0F | ABS-Relais |
| 0x10 | ABS-Kolbenfehler |
| 0x11 | Sensor Vorderrad |
| 0x12 | Vorderrad Elektronik |
| 0x13 | Sensor Vorderrad |
| 0x14 | ABS-Kolben Vorderrad |
| 0x15 | Sensor Hinterrad |
| 0x16 | Hinterrad-Elektronik |
| 0x17 | Sensor Hinterrad |
| 0x18 | ABS-Kolben Hinterrad |
| 0x19 | Elektronikfehler |
| 0x1A | ABS-Relais |
| 0x1B | ABS-Kolbenfehler |
| 0x1C | Radblockierer Vorn |
| 0x1D | - |
| 0x1E | Modulator defekt |
| 0x1F | Modulator defekt |
| 0x20 | Radblockierer Hinten |
| 0x21 | - |
| 0x22 | Elektronikfehler |
| 0x23 | EEPROM-Fehler |
| 0x24 | Unzulässige Fahrzeugkodierung |
| 0x25 | Batterieüberspannung |
| 0x26 | Interne Störung |
| 0x27 | Interne Störung |
| 0x28 | Interne Störung |
| 0x29 | Interne Störung |
| 0x2A | - |
| 0x2B | Interne Störung |
| 0x2C | Interne Störung |
| 0x2D | Interne Störung |
| 0x2E | Interne Störung |
| 0x2F | Interne Störung |
| 0x30 | Batterieunterspannung |
| 0x31 | Interne Störung |
| 0x32 | Interne Störung |
| 0x33 | Interne Störung |
| 0x34 | Interne Störung |
| 0x35 | Interne Störung |
| 0x36 | Interne Störung |
| 0x37 | Interne Störung |
| 0x38 | Interne Störung |
| 0xFF | unbekannter Fehler |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 9 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 |  |
| 0x01 | Unterbrechung oder Kurzschluss nach Plus |
| 0x02 | Kurzschluss nach Masse |
| 0x04 | kein Signal |
| 0x08 | Signal unplausibel |
| 0xFF | unbekannte Fehlerart |
| 0x21 | SPORADISCH |
| 0x22 | MOMEMTAN VORHANDEN |
| 0x23 | MOMEMTAN VORHANDEN |

<a id="table-fehlercodetest"></a>
### FEHLERCODETEST

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | TEST VOLLSTAENDIG |
| 0x01 | TEST UNVOLLSTAENDIG |
| 0xFF | UNBEKANNT |

<a id="table-fehlerstatus"></a>
### FEHLERSTATUS

Dimensions: 5 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 |  |
| 0x01 | SPORADISCH |
| 0x02 | MOMEMTAN VORHANDEN |
| 0x03 | MOMEMTAN VORHANDEN |
| 0xFF | STATUS: UNBEKANNT |

<a id="table-warnlampe"></a>
### WARNLAMPE

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Aus |
| 0x01 | Ein |
| 0xFF | UNBEKANNT |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | FEHLER |
| 0x02 | FEHLER: ARGUMENTE |
| 0x03 | FEHLER: AUSSERHALB BEREICH |
| 0x04 | FEHLER: ZUGRIFF VERWEIGERT |
| 0x05 | FEHLER: FORMATFEHLER DATEN (NICHT HEX) |
| 0xFF | FEHLER: UNBEKANNT |

<a id="table-fmw-test"></a>
### FMW_TEST

Dimensions: 8 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | FEHLER: FMW Test Vorderrad |
| 0x02 | FEHLER: FMW Test Hinterrad |
| 0x03 | FEHLER: FMW Test Vorderrad und Hinterrad |
| 0x04 | FEHLER: Baudrate nicht 10416 Baud |
| 0x08 | FEHLER: Motor nicht ein- oder ausgeschaltet |
| 0x0A | FEHLER: Kommunikationsfehler |
| 0xFF | FEHLER: UNBEKANNT |

<a id="table-elg-test"></a>
### ELG_TEST

Dimensions: 7 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | FEHLER: ELG Test Vorderrad |
| 0x02 | FEHLER: ELG Test Hinterrad |
| 0x03 | FEHLER: ELG Test Vorder- und Hinterrad |
| 0x04 | FEHLER: Baudrate nicht 10416 Baud |
| 0x08 | FEHLER: Motor nicht ausgeschaltet |
| 0xFF | FEHLER: UNBEKANNT |

<a id="table-mot-test"></a>
### MOT_TEST

Dimensions: 6 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | Fehler: Baudrate nicht 10416 Baud |
| 0x02 | Fehler: Relais nicht aus oder Motor ein |
| 0x03 | Fehler: Motor nicht ausgeschaltet |
| 0x04 | NICHT OK |
| 0xFF | FEHLER: UNBEKANNT |

<a id="table-pumpenmotor"></a>
### PUMPENMOTOR

Dimensions: 5 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | Fehler: Baudrate nicht 10416 Baud |
| 0x02 | Fehler: Motor nicht ausgeschaltet |
| 0x03 | NICHT OK: Batteriespannung unter Last &lt; 9 Volt |
| 0xFF | FEHLER: UNBEKANNT |

<a id="table-statuswarnlampe"></a>
### STATUSWARNLAMPE

Dimensions: 5 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | Fehler: Warnlampe W, Relais defekt |
| 0x02 | Fehler: Warnlampe K |
| 0x03 | Fehler: Warnlampe K und Warnlampe W, Relais defekt |
| 0xFF | FEHLER: UNBEKANNT |

<a id="table-kabelcodierung"></a>
### KABELCODIERUNG

Dimensions: 11 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Test/Produktion |
| 0x02 | R 1100 RS |
| 0x03 | K 1200 RS / K 1200 LT |
| 0x04 | R 850 GS / R 1100 GS / R 1150 GS |
| 0x06 | R 850 C / R 1200 C |
| 0x07 | K 1100 RS |
| 0x08 | R 850 RT / R 1100 RT |
| 0x09 | R 1100 S |
| 0x0B | K 1100 LT |
| 0x0C | R 850 R / R 1100 R |
| 0xFF | UNBEKANNT |

<a id="table-baudrate"></a>
### BAUDRATE

Dimensions: 17 rows × 2 columns

| BAUDRATENWERT | WERT |
| --- | --- |
| 300 | 103 |
| 600 | 51 |
| 1201 | 25 |
| 2403 | 12 |
| 2604 | 11 |
| 2840 | 10 |
| 3125 | 9 |
| 3472 | 8 |
| 3906 | 7 |
| 4464 | 6 |
| 5208 | 5 |
| 6250 | 4 |
| 7812 | 3 |
| 10416 | 2 |
| 15625 | 1 |
| 31250 | 0 |
| 0xFFFF | 0xFF |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |
| 0xFF | UNBEKANNT |

<a id="table-responsecode"></a>
### RESPONSECODE

Dimensions: 7 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | KEIN FEHLER |
| 0x11 | 0x11: SERVICE NICHT UNTERSTUETZT |
| 0x12 | 0x12: TEILFUNKTION NICHT UNTERSTUETZT |
| 0x22 | 0x22: BEDINGUNGEN NICHT KORREKT |
| 0x23 | 0x23: ANFORDERUNG NOCH NICHT BEENDET |
| 0x78 | 0x78: ANFORDERUNG NOCH NICHT BEENDET |
| 0xFF | UNBEKANNT |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 81 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | FTE |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe =&gt; Lear |
| 0x10 | VDO |
| 0x11 | Valeo |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine |
| 0x18 | Continental Teves |
| 0x19 | Elektromatik Suedafrika |
| 0x20 | Becker |
| 0x21 | Preh |
| 0x22 | Alps |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto |
| 0x26 | MotoMeter |
| 0x27 | Delphi PHI |
| 0x28 | DODUCO =&gt; BERU |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0x33 | Jatco |
| 0x34 | Fuba |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0x38 | Sachs |
| 0x39 | ITT |
| 0x40 | FTE |
| 0x41 | Megamos |
| 0x42 | TRW |
| 0x43 | Wabco |
| 0x44 | ISAD Electronic Systems |
| 0x45 | HEC (Hella Electronics Corporation) |
| 0x46 | Gemel |
| 0x47 | ZF |
| 0x48 | GMPT |
| 0x49 | Harman Kardon |
| 0x50 | Remes |
| 0x51 | ZF Lenksysteme |
| 0x52 | Magneti Marelli |
| 0x53 | Borg Instruments |
| 0x54 | GETRAG |
| 0x55 | BHTC (Behr Hella Thermocontrol) |
| 0x56 | Siemens VDO Automotive |
| 0x57 | Visteon |
| 0x58 | Autoliv |
| 0x59 | Haberl |
| 0x60 | Magna Steyr |
| 0x61 | Marquardt |
| 0x62 | AB-Elektronik |
| 0x63 | Siemens VDO Borg |
| 0x64 | Hirschmann Electronics |
| 0x65 | Hoerbiger Electronics |
| 0x66 | Thyssen Krupp Automotive Mechatronics |
| 0x67 | Gentex GmbH |
| 0x68 | Atena GmbH |
| 0x69 | Magna-Donelly |
| 0x70 | Koyo Steering Europe |
| 0x71 | NSI B.V |
| 0x72 | ASIN AWCO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
| 0x76 | CEL |
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
| 0xFF | unbekannter Hersteller |
