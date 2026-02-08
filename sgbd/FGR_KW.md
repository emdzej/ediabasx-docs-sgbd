# FGR_KW.PRG

- Jobs: [14](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | FGR_KW |
| ORIGIN | BMW TI-435 Crichton N.D. |
| REVISION | 1.00 |
| AUTHOR | BMW TI-435 Crichton N.D., BMW TI-433 Winkler |
| COMMENT | Tempomat KWP2000* |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer FGR_KW
- [DIAGNOSE_START](#job-diagnose-start) - Starten der Diagnose FGR_KW
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose FGR_KW
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Erhalten der Diagnose FGR_KW
- [IDENT](#job-ident) - Identdaten FGR_KW
- [STATUS_LESEN](#job-status-lesen) - Auslesen Status FGR_KW mit ReadDataByLocalIdentifier 0x01
- [FS_LESEN](#job-fs-lesen) - Lesen Fehlerspeicher FGR_KW mit ReadDataByLocalIdentifier 0x04
- [STATUS_LESEN_EINGANG](#job-status-lesen-eingang) - Auslesen Eingangsstatus FGR_KW mit ReadDataByLocalIdentifier 0x05
- [STATUS_LESEN_AUSGANG](#job-status-lesen-ausgang) - Auslesen Ausgangsstatus FGR_KW mit ReadDataByLocalIdentifier 0x06
- [STATUS_LESEN_GESCHWINDIGKEIT](#job-status-lesen-geschwindigkeit) - Auslesen Geschwindigkeitsinformationen FGR_KW mit ReadDataByLocalIdentifier 0x07
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers FGR_KW
- [SG_UNLOCK_0](#job-sg-unlock-0) - Security Access 'Third Party'
- [SG_UNLOCK_1](#job-sg-unlock-1) - Security Access 'Dealer'

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

Init-Job fuer FGR_KW

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-diagnose-start"></a>
### DIAGNOSE_START

Starten der Diagnose FGR_KW

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose FGR_KW

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-erhalten"></a>
### DIAGNOSE_ERHALTEN

Erhalten der Diagnose FGR_KW

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident"></a>
### IDENT

Identdaten FGR_KW

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_SYS_INDEX | int | Diagnose-Index |
| ID_DATUM_TAG | int | Herstelldatum Tag |
| ID_DATUM_MONAT | int | Herstelldatum Monat |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferant |
| ID_SW_NR | int | Softwarenummer |
| ID_BUS_INDEX | int | Bus-Index |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Auslesen Status FGR_KW mit ReadDataByLocalIdentifier 0x01

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_VERSTAERKUNG_P | int |  |
| STAT_VERSTAERKUNG_D | int |  |
| STAT_HYSTERESE_PUMPE | int |  |
| STAT_HYSTERESE_VENTIL | int |  |
| STAT_SETZIMPULSE_OFFSET | int |  |
| STAT_SETZIMPULSE_GRADIENT | int |  |
| STAT_BESCHLEUNIGUNG | int |  |
| STAT_BESCHLEUNIGUNG_GRADIENT | int |  |
| STAT_FEHLERZAEHLER_E2 | int |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

Lesen Fehlerspeicher FGR_KW mit ReadDataByLocalIdentifier 0x04

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ANZAHL | int | Anzahl der Fehler im Fehlerspeicher |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexdaten |
| F_ORT_NR | int | Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl an Fehlerarten, hier 2 |
| F_ART1_NR | int | Index der 1. Fehlerart |
| F_ART1_TEXT | string | 1. Fehlerart als Text |
| F_ART2_NR | int | Index der 2. Fehlerart |
| F_ART2_TEXT | string | 2. Fehlerart als Text |
| F_UW_ANZ | int | Anzahl an Umweltbedingungen, hier 5 |
| F_UW_SATZ | int | Anzahl der Umweltsaetze, hier 1 |
| F_UW1_NR | int | Index der 1. Umweltbedingung |
| F_UW1_TEXT | string | 1. Umweltbedingung als Text |
| F_UW1_WERT | int | Wert der 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit der 1. Umweltbedingung |
| F_UW2_NR | int | Index der 2. Umweltbedingung |
| F_UW2_TEXT | string | 2. Umweltbedingung als Text |
| F_UW2_WERT | int | Wert der 2. Umweltbedingung |
| F_UW2_EINH | string | Einheit der 2. Umweltbedingung |
| F_UW3_NR | int | Index der 3. Umweltbedingung |
| F_UW3_TEXT | string | 3. Umweltbedingung als Text |
| F_UW3_WERT | int | Wert der 3. Umweltbedingung |
| F_UW3_EINH | string | Einheit der 3. Umweltbedingung |
| F_UW4_NR | int | Index der 4. Umweltbedingung |
| F_UW4_TEXT | string | 4. Umweltbedingung als Text |
| F_UW4_WERT | int | Wert der 4. Umweltbedingung |
| F_UW4_EINH | string | Einheit der 4. Umweltbedingung |
| F_UW5_NR | int | Index der 5. Umweltbedingung |
| F_UW5_TEXT | string | 5. Umweltbedingung als Text |
| F_UW5_WERT | int | Wert der 5. Umweltbedingung |
| F_UW5_EINH | string | Einheit der 5. Umweltbedingung |

<a id="job-status-lesen-eingang"></a>
### STATUS_LESEN_EINGANG

Auslesen Eingangsstatus FGR_KW mit ReadDataByLocalIdentifier 0x05

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_PEDAL | int | 0 = Bremse/Kupplung nicht betaetigt, 1 = betaetigt |
| STAT_BREMSLICHT | int | 0 = Bremse nicht betaetigt, 1 = Bremse betaetigt |
| STAT_CRUISE_EIN | int | 0 = nicht betaetigt, 1 = betaetigt |
| STAT_CRUISE_AUS | int | 0 = nicht betaetigt, 1 = betaetigt |
| STAT_GESCHWINDIGKEIT_ERKENNUNG | int | 0 = Periodendauer &gt; 1.5s, 1 = sonst |
| STAT_GESCHWINDIGKEIT_SCHWELLE | int | 0 = groesser Minimalgeschwindigkeit, 1 = sonst |
| STAT_GESCHWINDIGKEIT_WERT | real | Geschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit der Geschwindigkeit, hier: km/h |

<a id="job-status-lesen-ausgang"></a>
### STATUS_LESEN_AUSGANG

Auslesen Ausgangsstatus FGR_KW mit ReadDataByLocalIdentifier 0x06

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_AUSGANG_GETESTET | int | 0 = Tests nicht abgeschlossen, 1 = abgeschlossen |
| STAT_CRUISE_AKTIV | int | 0 = Nein, 1 = Ja |

<a id="job-status-lesen-geschwindigkeit"></a>
### STATUS_LESEN_GESCHWINDIGKEIT

Auslesen Geschwindigkeitsinformationen FGR_KW mit ReadDataByLocalIdentifier 0x07

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_GESCHWINDIGKEIT_IST_WERT | real | Ist-Geschwindigkeit |
| STAT_GESCHWINDIGKEIT_IST_EINH | real | Einheit der Ist-Geschwindigkeit, hier: km/h |
| STAT_GESCHWINDIGKEIT_SOLL_WERT | real | Ist-Geschwindigkeit |
| STAT_GESCHWINDIGKEIT_SOLL_EINH | real | Einheit der Ist-Geschwindigkeit, hier: km/h |
| STAT_CRUISE_AKTIV | int | 0 = Nein, 1 = Ja |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers FGR_KW

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sg-unlock-0"></a>
### SG_UNLOCK_0

Security Access 'Third Party'

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-sg-unlock-1"></a>
### SG_UNLOCK_1

Security Access 'Dealer'

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (63 × 2)
- [LIEFERANTEN](#table-lieferanten) (47 × 2)
- [FORTTEXTE](#table-forttexte) (10 × 2)
- [FARTMATRIX](#table-fartmatrix) (3 × 5)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 8)
- [FUMWELTTEXTE](#table-fumwelttexte) (30 × 3)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 63 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED__INVALID_FORMAT |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0x23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED__SECURITY_ACCESS_REQUESTED |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0x40 | ERROR_ECU_DOWNLOAD_NOT_ACCEPTED |
| 0x41 | ERROR_ECU_IMPROPER_DOWNLOAD_TYPE |
| 0x42 | ERROR_ECU_CANNOT_DOWNLOAD_TO_SPECIFIED_ADDRESS |
| 0x43 | ERROR_ECU_CANNOT_DOWNLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x50 | ERROR_ECU_UPLOAD_NOT_ACCEPTED |
| 0x51 | ERROR_ECU_IMPROPER_UPLOAD_TYPE |
| 0x52 | ERROR_ECU_CANNOT_UPLOAD_FROM_SPECIFIED_ADDRESS |
| 0x53 | ERROR_ECU_CANNOT_UPLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x71 | ERROR_ECU_TRANSFER_SUSPENDED |
| 0x72 | ERROR_ECU_TRANSFER_ABORTED |
| 0x74 | ERROR_ECU_ILLEGAL_ADDRESS_IN_BLOCK_TRANSFER |
| 0x75 | ERROR_ECU_ILLEGAL_BYTE_COUNT_IN_BLOCK_TRANSFER |
| 0x76 | ERROR_ECU_ILLEGAL_BLOCK_TRANSFER_TYPE |
| 0x77 | ERROR_ECU_BLOCKTRANSFER_DATA_CHECKSUM_ERROR |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x79 | ERROR_ECU_INCORRECT_BYTE_COUNT_DURING_BLOCK_TRANSFER |
| 0x80 | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_DIAGNOSTIC_MODE |
| ?00? | OKAY |
| ?02? | ERROR_ECU_INCORRECT_RESPONSE_ID |
| ?10? | ERROR_F_CODE |
| ?11? | ERROR_TABLE |
| ?12? | ERROR_INTERPRETATION |
| ?20? | ERROR_SEGMENT |
| ?21? | ERROR_ADDRESS |
| ?22? | ERROR_NUMBER |
| ?30? | ERROR_DATA |
| ?40? | ERROR_MODE |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?60? | ERROR_DATA_OUT_OF_RANGE |
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| ?73? | ERROR_NO_BIN_BUFFER |
| ?74? | ERROR_BIN_BUFFER |
| ?75? | ERROR_DATA_TYPE |
| ?80? | ERROR_FLASH_SIGNATURE_CHECK |
| ?81? | ERROR_VIHICLE_IDENTFICATON_NR |
| ?82? | ERROR_PROGRAMMING_DATE |
| ?83? | ERROR_ASSEMBLY_NR |
| ?84? | ERROR_CALIBRATION_DATASET_NR |
| ?85? | ERROR_EXHAUST_REGULATION_OR_TYPE_APPROVAL_NR |
| ?86? | ERROR_REPAIR_SHOP_NR |
| ?87? | ERROR_TESTER_SERIAL_NR |
| ?88? | ERROR_MILAGE |
| ?89? | ERROR_PROGRAMMING_REFERENCE |
| ?8A? | ERROR_LARGE_UIF_FOUND |
| ?8B? | ERROR_SMALL_UIF_FOUND |
| ?8C? | ERROR_NO_FREE_UIF |
| ?8D? | ERROR_MAX_UIF |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 47 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 10 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Pegel Spannungsausgang: Niedrig, hoch erwartet |
| 0x02 | Pegel Ventilausgang: Niedrig, hoch erwartet |
| 0x03 | Pegel Pumpenausgang: Niedrig, hoch erwartet |
| 0x04 | Steuergeraet: Interner Fehler |
| 0x05 | Pegel Spannungsausgang: Hoch, niedrig erwartet |
| 0x06 | Pegel Ventilausgang: Hoch, niedrig erwartet |
| 0x07 | Pegel Pumpenausgang: Hoch, niedrig erwartet |
| 0x08 | Geschwindigkeitseingabe: Eingabefehler |
| 0x09 | Fehlerspeicher: Lesefehler |
| 0xFF | unbekannter Fehlerort |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 3 rows × 5 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 |
| --- | --- | --- | --- | --- |
| 0x00 | 0xFF | 0x00 | 0xFF | 0x01 |
| 0x09 | 0xFF | 0xFF | 0xFF | 0xFF |
| 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Permanenter Fehler |
| 0x01 | Sporadischer Fehler |
| 0xFF | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 8 columns

| ORT | UW_ANZ | UW_SATZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0x00 | 0x05 | 0x01 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 30 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x01 | Aktionen seit letztem Spannungsfehler | Aktionen |
| 0x02 | Aktionen seit letztem Ventilfehler | Aktionen |
| 0x03 | Aktionen seit letztem Pumpenfehler | Aktionen |
| 0x04 | Aktionen seit letztem Geschwindigkeitseingabefehler | Aktionen |
| 0x05 | Initialwert nach RESET | LAG-Nr. |
| 0x07 | Sollgeschwindigkeit &gt; V_max | LAG-Nr. |
| 0x08 | Keine Vorgabe | LAG-Nr. |
| 0x0A | Relais-Ausgang niedrig | LAG-Nr. |
| 0x0B | Ventilkontrolle niedrig waehrend Benutzung | LAG-Nr. |
| 0x0C | Pumpenkontrolle niedrig waehrend Benutzung | LAG-Nr. |
| 0x0D | Istgeschwindigkeit &gt; V_max | LAG-Nr. |
| 0x0E | Istgeschwindigkeit &lt; V_min | LAG-Nr. |
| 0x0F | Beschleunigungsgrenze ueberschritten | LAG-Nr. |
| 0x10 | Pumpenkontrolle niedrig beim Einschalten | LAG-Nr. |
| 0x11 | Ventilkontrolle niedrig beim Einschalten | LAG-Nr. |
| 0x12 | Relaisausgang niedrig beim Einschalten | LAG-Nr. |
| 0x13 | Relaisausgang hoch waehrend Nichtbenutzung | LAG-Nr. |
| 0x14 | Brems- oder Kupplungsschalter offen | LAG-Nr. |
| 0x15 | Bremslicht an | LAG-Nr. |
| 0x16 | Fehler in redundanter V_min-Hardware | LAG-Nr. |
| 0x17 | Masseschluss Relais | LAG-Nr. |
| 0x18 | Differenz Soll-Ist-Geschwindigkeit zu gross | LAG-Nr. |
| 0x19 | Unterschiedliche Sollgeschwindigkeiten | LAG-Nr. |
| 0x1A | Relaisausgang hoch beim Ausschalten | LAG-Nr. |
| 0x1C | Fehler in redundanter Ventilkontrolle | LAG-Nr. |
| 0x1D | Fehler in redundanter Pumpenkontrolle | LAG-Nr. |
| 0x1F | Betaetigung AUS-Schalter | LAG-Nr. |
| 0x20 | Pumpenkontrolle bleibt hoch | LAG-Nr. |
| 0x21 | Ventilkontrolle bleibt hoch | LAG-Nr. |
| 0xFF | Unbekannt | LAG-Nr. |
