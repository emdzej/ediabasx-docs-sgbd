# MRS4.prg

- Jobs: [29](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MRS4 fuer Airbag SG E39 (Temic), E46 E53 R50 R53 (Bosch) |
| ORIGIN | BMW TI-430 Crichton N |
| REVISION | 2.00 |
| AUTHOR | BMW TI-430 Crichton N, BMW TI-431 Dennert, BERATA M.Chafigoulline, BERATA GmbH Oliver Schieferstein |
| COMMENT | N/A |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer AIRBAG MRS4
- [IDENT](#job-ident) - Ident-Daten fuer AIRBAG MRS4
- [SECURITY_CHANGE](#job-security-change) - Wechseln zum Sicherheitslevel 2 Change to security level 2
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Error memory quicktest High-Konzept nach Lastenheft
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Read error memory
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen Clear error memory
- [SPEICHER_LESEN](#job-speicher-lesen) - Speicher lesen Read memory
- [AUSSTATTUNG_LESEN](#job-ausstattung-lesen) - Ausstattung lesen Read equipment configuration
- [HERSTELLERDATEN_LESEN](#job-herstellerdaten-lesen) - Kodierte KFZ-Herstellerdaten lesen Read coded productiondata
- [TYP_LESEN](#job-typ-lesen) - Lesen des Fahrzeugtyps (Baureihe) Read vehicle model
- [PARAMETER_LESEN](#job-parameter-lesen) - 16 Byte aus Parametersatz 1 lesen Read 16 bytes from block stated
- [BARCODE_LESEN](#job-barcode-lesen) - Lesen der MRSZ4 barcode infos Read unique ECU barcode
- [BARCODE_MRSA_L_LESEN](#job-barcode-mrsa-l-lesen) - Lesen der MRSA (links) barcode infos Read unique MRSA (left) barcode
- [BARCODE_MRSA_R_LESEN](#job-barcode-mrsa-r-lesen) - Lesen der MRSA (rechts) barcode infos Read unique MRSA (right) barcode
- [STATUS_LESEN](#job-status-lesen) - Status des MRS4 lesen Read status of MRS4
- [VERRIEGELUNG_LESEN](#job-verriegelung-lesen) - Auslesen der Verriegelung (= Pruefstempel) Read lock byte status
- [VERRIEGELUNG_SCHREIBEN](#job-verriegelung-schreiben) - Verriegelungsbytes setzen Set lock byte
- [CONTROLLER_RESET](#job-controller-reset) - Zuruecksetzen des Controllers Reset ECU
- [SG_LOGIN](#job-sg-login) - Berechtigung fuer EEPROM-Zugriffe Login to ECU
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Diagnose aufrechterhalten Diagnosis wake up
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden Diagnosis end
- [AUSSTATTUNG_LESEN_EWS](#job-ausstattung-lesen-ews) - Ausstattung lesen Read equipment for EWS
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Lesen des Pruefcodes, besteht aus Identifikationsdaten, Ausstattungsdaten und dem FS-Inhalt, jedes Telegrammpaket ist durch ein 0x00 abgeschlossen Read test codes (identdata, equipdata, errordata) Returned as strings separated by 0x00
- [C_FS_LESEN](#job-c-fs-lesen) - 24 Byte aus Crashtelegram lesen Read 24 bytes from crashtelegram block stated
- [C_FS_LOESCHEN](#job-c-fs-loeschen) - Crashtelegram loeschen Delete crash telegram
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen Read codingdata
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren Write and check codingdata
- [C_FG_LESEN](#job-c-fg-lesen) - Kodierte KFZ-Herstellerdaten lesen Read coded productiondata

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

Init-Job fuer AIRBAG MRS4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer AIRBAG MRS4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| ID_BMW_NR | string | BMW-Teilenummer BMW part number |
| ID_HW_NR | int | BMW-Hardwarenummer BMW hardware number |
| ID_COD_INDEX | int | Codier-Index Coding index |
| ID_DIAG_INDEX | int | Diagnose-Index Diagnostic index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW Production week |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Production year |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier number |
| ID_LIEF_TEXT | string | Lieferant Supplier text |
| ID_SW_NR | int | Softwarenummer |

<a id="job-security-change"></a>
### SECURITY_CHANGE

Wechseln zum Sicherheitslevel 2 Change to security level 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Error memory quicktest High-Konzept nach Lastenheft

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ANZ | int | Anzahl Fehler Number of errors |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Read error memory

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_HEX_CODE | binary | Hex-Fehlerdaten je Fehler Hex format errordata |
| F_ORT_NR | int | identisch Fehlerbytemaske Error location number |
| F_ORT_TEXT | string | Fehlerort als Text Error location text |
| F_HFK | int | Fehlerhaeufigkeit Error frequency (occurences) |
| F_ART_ANZ | int | Anzahl der Fehlerarten (hier: immer 8) Number of errortypes (always 8 here) |
| F_ART1_NR | int | Index der 1. Fehlerart Index of 1st errortype |
| F_ART1_TEXT | string | 1. Fehlerart als Text Text of 1st errortype |
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
| F_UW_ANZ | int | Anzahl der Umweltbedingungen (hier: immer 2) Number of environment conditions (always 2 here) |
| F_UW_SATZ | int | Anzahl der Umweltsaetze (hier: immer 1) Number of environment blocks (always 1 here) |
| F_UW1_NR | int | Index der 1. Umweltbedingung (hier: immer 1) Index of 1st environment condition (always 1 here) |
| F_UW1_TEXT | string | Text zur 1. Umweltbedingung (hier: immer Beginnfehleruhr) Text of 1st environment condition |
| F_UW1_WERT | long | Wert der 1. Umweltbedingung Value of 1st environment condition |
| F_UW1_EINH | string | Einheit der 1. Umweltbedingung (hier: immer Sek.) Unit of 1st environment condition |
| F_UW2_NR | int | Index der 2. Umweltbedingung (hier: immer 2) |
| F_UW2_TEXT | string | Text zur 2. Umweltbedingung (hier: immer Endefehleruhr) |
| F_UW2_WERT | long | Wert der 2. Umweltbedingung |
| F_UW2_EINH | string | Einheit der 2. Umweltbedingung (hier: immer Sek.) |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen Clear error memory

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Speicher lesen Read memory

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | string | Speicher Segment |
| H_ADR | string | Startadresse High-Byte |
| M_ADR | string | Startadresse Mitte-Byte |
| L_ADR | string | Startadresse Low-Byte |
| ANZ_BYTE | string | Anzahl der zu lesenden Bytes (1 - 32) Number of bytes to read (1 - 32) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Speicherinhalt |

<a id="job-ausstattung-lesen"></a>
### AUSSTATTUNG_LESEN

Ausstattung lesen Read equipment configuration

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| BYTE_0 | int | Byte 0 der 7 Ausstattungsbytes |
| BYTE_1 | int | Byte 1 der 7 Ausstattungsbytes |
| BYTE_2 | int | Byte 2 der 7 Ausstattungsbytes |
| BYTE_3 | int | Byte 3 der 7 Ausstattungsbytes |
| BYTE_4 | int | Byte 4 der 7 Ausstattungsbytes |
| BYTE_5 | int | Byte 5 der 7 Ausstattungsbytes |
| BYTE_6 | int | Byte 6 der 7 Ausstattungsbytes |
| BYTE_7 | int | Byte 7 der 7 Ausstattungsbytes |
| ZK0_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut 0 = not included,  1 = included ZK = ignition circuit |
| ZK1_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK2_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK3_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK4_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK5_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK6_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK7_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK8_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK9_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK10_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK11_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK12_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK13_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK14_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK15_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK16_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK17_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK18_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK19_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK20_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK21_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK22_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| ZK23_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| GURTSCHLOSS_F_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Buckle - driver |
| GURTSCHLOSS_BF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Buckle - passenger |
| GURTSCHLOSS_HL_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Buckle - rear left |
| GURTSCHLOSS_HR_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Buckle - rear right |
| GURTSCHLOSS_HM_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Buckle - rear middle |
| GURTSCHLOESSER_VORNE_STROMSCHNITTST_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Buckles front current interface |
| GURTSCHLOESSER_VORNE_SPANNUNGSSCHNITTST_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Buckles front voltage interface |
| SBE_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Seat occupancy recognition |
| OC3_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Occupant Classification System |
| SLV_FAHRER_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Seat position sensor - driver |
| SLV_BEIFAHRER_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Seat position sensor- passenger |
| SBE_1_STATUS | int | 0 = keine Verzoegerung, 1 = Verzoegerung Seat occupancy recognition status delay |
| MRSA_FRONT_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| MRSA_FOND_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| OPTION_VERBAUT | int | (Ueberrollsensor) Roll sensor 0 = nicht verbaut, 1 = verbaut |
| LAENDERVERSION | int | 0 = ECE, 1 = USA Country variant, same result as US_VERSION |
| US_VERSION | int | 0 = ECE, 1 = USA Country variant, same result as LAENDERVERSION |
| LENKSEITE | int | 0 = linkslenker, 1 = rechtslenker 0 = LHD,         1 = RHD |
| POL_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut PassengerAirbagoffLamp |
| ITS_FRONTCRASH_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| BYTE_1_0 | int | Byte 0 der 7 Ausstattungsbytes (wiederholt) |
| BYTE_1_1 | int | Byte 1 der 7 Ausstattungsbytes (wiederholt) |
| BYTE_1_2 | int | Byte 2 der 7 Ausstattungsbytes (wiederholt) |
| BYTE_1_3 | int | Byte 3 der 7 Ausstattungsbytes (wiederholt) |
| BYTE_1_4 | int | Byte 4 der 7 Ausstattungsbytes (wiederholt) |
| BYTE_1_5 | int | Byte 5 der 7 Ausstattungsbytes (wiederholt) |
| BYTE_1_6 | int | Byte 6 der 7 Ausstattungsbytes (wiederholt) |
| BYTE_1_7 | int | Byte 7 der 7 Ausstattungsbytes (wiederholt) |

<a id="job-herstellerdaten-lesen"></a>
### HERSTELLERDATEN_LESEN

Kodierte KFZ-Herstellerdaten lesen Read coded productiondata

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TYP | string | Baureihe z.B: E31 / 03h , E34 / 01h ... Vehicle e.g: L30, R50... |
| CODIERDATUM | string | z.B: 21.4.93 ... Coding date |
| WERKSKENNUNG | string | 4-stellige Dezimalzahl als String 4 character plant code (decimal) |
| HAENDLERKENNUNG | string | 5-stellige Dezimalzahl als String 5 character supplier code (decimal) |
| FGNUMMER | string | Kurze Fahrgestellnummer Short VIN |
| DATEN | binary | Antworttelegramm |
| DATEN1 | binary | Antworttelegramm |

<a id="job-typ-lesen"></a>
### TYP_LESEN

Lesen des Fahrzeugtyps (Baureihe) Read vehicle model

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TYP | string | Baureihe z.B: E31 / 03h , E34 / 01h ... Vehicle e.g: L30, R50.... |

<a id="job-parameter-lesen"></a>
### PARAMETER_LESEN

16 Byte aus Parametersatz 1 lesen Read 16 bytes from block stated

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCKNR | string | (0 &lt;= BLOCKNR &lt;= 10) --&gt; 16 Parameterbytes ab Byte (16*BLOCKNR) werden angefordert Between 0 and 10, byte 16*BLOCKNR returned |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Spezifizierte Parameterdaten Specified parameterdata |

<a id="job-barcode-lesen"></a>
### BARCODE_LESEN

Lesen der MRSZ4 barcode infos Read unique ECU barcode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Antworttelegramm |
| DATEN_STRING | string | Barcode, decodiert als String Barcode, decoded as String |
| SACHNUMMER | string | Sachnummer Part number |
| AENDERUNGS_INDEX | string | Aenderungs-Index Change/version index |
| HERSTELLER_INFO | string | Hersteller-Info Production info |

<a id="job-barcode-mrsa-l-lesen"></a>
### BARCODE_MRSA_L_LESEN

Lesen der MRSA (links) barcode infos Read unique MRSA (left) barcode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Antworttelegramm |
| DATEN_STRING | string | Barcode, decodiert als String Barcode, decoded as String |
| SACHNUMMER | string | Sachnummer Part number |
| AENDERUNGS_INDEX | string | Aenderungs-Index Change/version index |
| HERSTELLER_INFO | string | Hersteller-Info Production info |

<a id="job-barcode-mrsa-r-lesen"></a>
### BARCODE_MRSA_R_LESEN

Lesen der MRSA (rechts) barcode infos Read unique MRSA (right) barcode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Antworttelegramm |
| DATEN_STRING | string | Barcode, decodiert als String Barcode, decoded as String |
| SACHNUMMER | string | Sachnummer Part number |
| AENDERUNGS_INDEX | string | Aenderungs-Index Change/version index |
| HERSTELLER_INFO | string | Hersteller-Info Production info |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Status des MRS4 lesen Read status of MRS4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG Hex answer from ECU |
| STAT_ZK0 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error |
| STAT_ZK1 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK2 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK3 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK4 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK5 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK6 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK7 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK8 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK9 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK10 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK11 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK12 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK13 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK14 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK15 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK16 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK17 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK18 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK19 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK20 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK21 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK22 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ZK23 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_GURTSCHLOSS_F_1 | int | 0 = nicht gesteckt, 1 = i.0 Buckle - driver, 0 = not plugged in |
| STAT_GURTSCHLOSS_F_2 | int | 0 = gesteckt, 1 = i.0 Buckle - driver, 0 = plugged in |
| STAT_GURTSCHLOSS_F_3 | int | 0 = fehler, 1 = i.0 Buckle - driver, 0 = error |
| STAT_GURTSCHLOSS_BF_1 | int | 0 = nicht gesteckt, 1 = i.0 Buckle - passenger |
| STAT_GURTSCHLOSS_BF_2 | int | 0 = gesteckt, 1 = i.0 |
| STAT_GURTSCHLOSS_BF_3 | int | 0 = fehler, 1 = i.0 |
| STAT_GURTSCHLOSS_HL_1 | int | 0 = nicht gesteckt, 1 = i.0 Buckle - rear left |
| STAT_GURTSCHLOSS_HL_2 | int | 0 = gesteckt, 1 = i.0 |
| STAT_GURTSCHLOSS_HL_3 | int | 0 = fehler, 1 = i.0 |
| STAT_GURTSCHLOSS_HR_1 | int | 0 = nicht gesteckt, 1 = i.0 Buckle - rear right |
| STAT_GURTSCHLOSS_HR_2 | int | 0 = gesteckt, 1 = i.0 |
| STAT_GURTSCHLOSS_HR_3 | int | 0 = fehler, 1 = i.0 |
| STAT_GURTSCHLOSS_HM_1 | int | 0 = nicht gesteckt, 1 = i.0 Buckle - rear middle |
| STAT_GURTSCHLOSS_HM_2 | int | 0 = gesteckt, 1 = i.0 |
| STAT_GURTSCHLOSS_HM_3 | int | 0 = fehler, 1 = i.0 |
| STAT_SBE_1 | int | 0 = Beifahrersitz belegt durch Insasse, 1 = i.0 Seat occupancy recog, 0 = passenger seat occupied by person |
| STAT_SBE_2 | int | 0 = Beifahrersitz nicht belegt durch Insasse, 1 = i.0 Seat occupancy recog, 0 = passenger seat not occupied by person |
| STAT_SBE_3 | int | 0 = fehler, 1 = i.0 Seat occupancy recog, 0 = error |
| STAT_OC3_1 | int | 0 = OC-3 Beifahrersitz belegt durch Insasse, 1 = i.0 0 = passenger seat occupied by person |
| STAT_OC3_2 | int | 0 = OC-3 Beifahrersitz nicht belegt durch Insasse, 1 = i.0 0 = passenger seat not occupied by person |
| STAT_OC3_3 | int | 0 = OC-3 Beifahrersitz belegt durch Kindersitz, 1 = i.0 0 = passenger seat occupied by child seat |
| STAT_OC3_4 | int | 0 = OC-3 meldet OOP, 1 = i.0 |
| STAT_OC3_5 | int | 0 = OC-3 fehler, 1 = i.0 0 = error |
| STAT_LEHNE_F_1 | int | 0 = nicht verriegelt, 1 = i.0 Seat position sensor driver, 0 = not locked |
| STAT_LEHNE_F_2 | int | 0 = korrekt verriegelt, 1 = i.0 Seat position sensor driver, 0 = correctly locked |
| STAT_LEHNE_F_3 | int | 0 = Modul meldet sich selbst defekt, 1 = i.0 Seat position sensor driver, 0 = error with module |
| STAT_LEHNE_F_4 | int | 0 = Sammelfehler, 1 = i.0 Seat position sensor driver, 0 = collective error |
| STAT_LEHNE_BF_1 | int | 0 = nicht verriegelt, 1 = i.0 Seat position sensor passenger |
| STAT_LEHNE_BF_2 | int | 0 = korrekt verriegelt, 1 = i.0 |
| STAT_LEHNE_BF_3 | int | 0 = Modul meldet sich selbst defekt, 1 = i.0 |
| STAT_LEHNE_BF_4 | int | 0 = Sammelfehler, 1 = i.0 |
| STAT_MRSA_L_1 | int | 0 = sendet fehler, 1 = i.0 |
| STAT_MRSA_L_2 | int | 0 = Kommunikationsfehler, 1 = i.0 |
| STAT_MRSA_L_3 | int | 0 = Leitungsfehler, 1 = i.0 |
| STAT_MRSA_L_4 | int | 0 = falscher Typ / Algo, 1 = i.0 |
| STAT_MRSA_R_1 | int | 0 = sendet fehler, 1 = i.0 |
| STAT_MRSA_R_2 | int | 0 = Kommunikationsfehler, 1 = i.0 |
| STAT_MRSA_R_3 | int | 0 = Leitungsfehler, 1 = i.0 |
| STAT_MRSA_R_4 | int | 0 = falscher Typ / Algo, 1 = i.0 |

<a id="job-verriegelung-lesen"></a>
### VERRIEGELUNG_LESEN

Auslesen der Verriegelung (= Pruefstempel) Read lock byte status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| BYTE1 | int | Datenbyte 1 |
| BYTE2 | int | Datenbyte 2 |
| BYTE3 | int | Datenbyte 3 |
| PRUEFSTEMPEL | binary | Gesamter Pruefstempel |

<a id="job-verriegelung-schreiben"></a>
### VERRIEGELUNG_SCHREIBEN

Verriegelungsbytes setzen Set lock byte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| ERROR_CODE | string | Bei NIO Fehlertext, sonst Leerstring |

<a id="job-controller-reset"></a>
### CONTROLLER_RESET

Zuruecksetzen des Controllers Reset ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-sg-login"></a>
### SG_LOGIN

Berechtigung fuer EEPROM-Zugriffe Login to ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-diagnose-erhalten"></a>
### DIAGNOSE_ERHALTEN

Diagnose aufrechterhalten Diagnosis wake up

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden Diagnosis end

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-ausstattung-lesen-ews"></a>
### AUSSTATTUNG_LESEN_EWS

Ausstattung lesen Read equipment for EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| AUSSTATTUNG | string | x Ausstattungsbytes als String Equipment bytes as String |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Lesen des Pruefcodes, besteht aus Identifikationsdaten, Ausstattungsdaten und dem FS-Inhalt, jedes Telegrammpaket ist durch ein 0x00 abgeschlossen Read test codes (identdata, equipdata, errordata) Returned as strings separated by 0x00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| PRUEFCODE | binary | Daten in Hex-Format |

<a id="job-c-fs-lesen"></a>
### C_FS_LESEN

24 Byte aus Crashtelegram lesen Read 24 bytes from crashtelegram block stated

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCKNR | string | (1 &lt;= BLOCKNR &lt;= 8) --&gt; 24 Parameterbytes ab Between 0 and 10, 24 bytes returned |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Spezifizierte Crashdaten Specified crashdata |

<a id="job-c-fs-loeschen"></a>
### C_FS_LOESCHEN

Crashtelegram loeschen Delete crash telegram

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| ERROR_CODE | string | Bei NIO Fehlertext, sonst Leerstring |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen Read codingdata

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten Codingdata |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten Codingdata |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren Write and check codingdata

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten Codingdata |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Kodierte KFZ-Herstellerdaten lesen Read coded productiondata

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| FG_NR | string | Kurze Fahrgestellnummer Short VIN |
| _TELEGRAMM | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (6 × 2)
- [LIEFERANTEN](#table-lieferanten) (31 × 2)
- [FORTTEXTE](#table-forttexte) (70 × 2)
- [FARTMATRIX](#table-fartmatrix) (70 × 17)
- [FARTTEXTE](#table-farttexte) (38 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (2 × 3)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 6 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNKTION |
| 0xFF | ERROR_ECU_UNKNOWN_KONTROLLBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 31 rows × 2 columns

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
| 0x30 | NEC |
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 70 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Zuendkreis ZK0 / Airbag Fahrer Stufe 1 |
| 0x02 | Zuendkreis ZK1 / Gurtstrammer Fahrer |
| 0x03 | Zuendkreis ZK2 / Gurtstrammer Beifahrer |
| 0x04 | Zuendkreis ZK3 / Airbag Beifahrer Stufe 1 |
| 0x05 | Zuendkreis ZK4 / Seitenairbag vorne links |
| 0x06 | Zuendkreis ZK5 / Seitenairbag vorne rechts |
| 0x07 | Zuendkreis ZK6 / Seitenairbag hinten links |
| 0x08 | Zuendkreis ZK7 / Seitenairbag hinten rechts |
| 0x09 | Zuendkreis ZK8 / Kopfairbag (ITS) links |
| 0x0A | Zuendkreis ZK9 / Kopfairbag (ITS) rechts |
| 0x0B | Zuendkreis ZK10 / Sicherheits-Batterie-Klemme 1 |
| 0x0C | Zuendkreis ZK11 / Airbag Beifahrer Stufe 2 |
| 0x0D | Zuendkreis ZK12 / Airbag Fahrer Stufe 2 |
| 0x0E | Zuendkreis ZK13 / Kopfairbag hinten links |
| 0x0F | Zuendkreis ZK14 / Kopfairbag hinten rechts |
| 0x10 | Zuendkreis ZK15 / Sicherheits-Batterie-Klemme 2 |
| 0x11 | Zuendkreis ZK16 / Gurtstrammer hinten links |
| 0x12 | Zuendkreis ZK17 / Gurtstrammer hinten rechts |
| 0x13 | Zuendkreis ZK18 / Gurtstrammer hinten mitte |
| 0x14 | Zuendkreis ZK19 |
| 0x15 | Zuendkreis ZK6 / Airbag Fahrer Stufe 2 |
| 0x16 | Zuendkreis ZK7 |
| 0x30 | Zuendkreis ZK0 / Airbag Fahrer Stufe 1 |
| 0x31 | Zuendkreis ZK1 / Gurtstrammer Fahrer |
| 0x32 | Zuendkreis ZK2 / Gurtstrammer Beifahrer |
| 0x33 | Zuendkreis ZK3 / Airbag Beifahrer Stufe 1 |
| 0x34 | Zuendkreis ZK4 / Seitenairbag vorne links |
| 0x35 | Zuendkreis ZK5 / Seitenairbag vorne rechts |
| 0x36 | Zuendkreis ZK6 / Seitenairbag hinten links |
| 0x37 | Zuendkreis ZK7 / Seitenairbag hinten rechts |
| 0x38 | Zuendkreis ZK8 / Kopfairbag (ITS) links |
| 0x39 | Zuendkreis ZK9 / Kopfairbag (ITS) rechts |
| 0x3A | Zuendkreis ZK10 / Sicherheits-Batterie-Klemme 1 |
| 0x3B | Zuendkreis ZK11 / Airbag Beifahrer Stufe 2 |
| 0x3C | Zuendkreis ZK12 / Airbag Fahrer Stufe 2 |
| 0x3D | Zuendkreis ZK13 / Kopfairbag hinten links |
| 0x3E | Zuendkreis ZK14 / Kopfairbag hinten rechts |
| 0x3F | Zuendkreis ZK15 / Sicherheits-Batterie-Klemme 2 |
| 0x40 | Zuendkreis ZK16 / Gurtstrammer hinten links |
| 0x41 | Zuendkreis ZK17 / Gurtstrammer hinten rechts |
| 0x42 | Zuendkreis ZK18 / Gurtstrammer hinten mitte |
| 0x43 | Zuendkreis ZK19 |
| 0x44 | Zuendkreis ZK6 / Airbag Beifahrer Stufe 2 |
| 0x45 | Zuendkreis ZK7 |
| 0x50 | Versorgungsspannung |
| 0x51 | Fehlerlampe (AWL) |
| 0x52 | PassengerAirbagOffLampe (POL) |
| 0x60 | Gurtschloss Fahrer |
| 0x61 | Gurtschloss Beifahrer |
| 0x62 | Gurtschloss hinten links |
| 0x63 | Gurtschloss hinten rechts |
| 0x64 | Gurtschloss hinten mitte |
| 0x70 | Sitz-Belegungs-Erkennung |
| 0x71 | OC3 |
| 0x72 | Sitz-Lehnen-Verriegelung und K-Bus |
| 0x73 | Sitz-Lehnen-Verriegelung Fahrer |
| 0x74 | Sitz-Lehnen-Verriegelung Beifahrer |
| 0x75 | Externer Ueber-Roll-Sensor |
| 0x80 | MRSA vorne |
| 0x81 | MRSA vorne links |
| 0x82 | MRSA vorne links |
| 0x83 | MRSA vorne links |
| 0x84 | MRSA vorne rechts |
| 0x85 | MRSA vorne rechts |
| 0x86 | MRSA vorne rechts |
| 0x87 | MRSA vorne rechts |
| 0x88 | MRSA vorne links |
| 0x90 | Codierung Blocke (CBD-Block) |
| 0x91 | Crashtelegramspeicher |
| 0xF0 | Interne Fehler |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 70 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x02 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x03 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x04 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x05 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x06 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x07 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x08 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x09 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0A | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0B | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0C | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0D | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0E | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0F | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x10 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x11 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x12 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x13 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x14 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x15 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x16 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x30 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x31 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x32 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x33 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x34 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x35 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x36 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x37 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x38 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x39 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3A | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3B | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3C | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3D | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3E | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3F | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x40 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x41 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x42 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x43 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x44 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x45 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x50 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x1F | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x51 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x20 | 0xFF | 0x21 | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x52 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x20 | 0xFF | 0x21 | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x60 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x61 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x62 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x63 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x64 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x70 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x0E | 0xFF | 0x0F | 0xFF | 0x10 | 0xFF | 0x11 | 0x08 | 0x09 |
| 0x71 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x12 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x72 | 0xFF | 0x23 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x73 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x13 | 0xFF | 0x14 | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x74 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x13 | 0xFF | 0x14 | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x75 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x12 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x80 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x15 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x81 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x12 | 0xFF | 0x16 | 0xFF | 0x17 | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x82 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x18 | 0xFF | 0x19 | 0xFF | 0x1A | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x83 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x1B | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x84 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x12 | 0xFF | 0x16 | 0xFF | 0x17 | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x85 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x18 | 0xFF | 0x19 | 0xFF | 0x1A | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x86 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x1B | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x87 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x22 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x88 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x22 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x90 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x1D | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x91 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x1E | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0xF0 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 38 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Plausibilitaetsfehler |
| 0x01 | Fehler nicht vorhanden |
| 0x02 | Fehler aktuell vorhanden |
| 0x03 | -- |
| 0x04 | Masse-Schluss |
| 0x05 | U-Batterie-Schluss |
| 0x06 | Widerstand zu klein |
| 0x07 | Widerstand zu gross |
| 0x08 | Fehler nicht sporadisch |
| 0x09 | Fehler sporadisch |
| 0x0A | Widerstand nicht definiert oder Graubereich |
| 0x0B | Masseschluss / Widerstand zu klein |
| 0x0C | U-Batterie-Schluss / Unterbrechung / Widerstand zu gross |
| 0x0D | Kommunikationsstoerung |
| 0x0E | Leitung gegen Masse |
| 0x0F | Leitung gegen Plus |
| 0x10 | Unterbrechung Sitzmatte |
| 0x11 | Kurzschluss Sitzmatte |
| 0x12 | Sendet Fehler |
| 0x13 | Modul sendet Fehler |
| 0x14 | Sammelfehler SLV |
| 0x15 | Typen untershiedlich |
| 0x16 | Falsche Algoparameter |
| 0x17 | Type Fehlerhaftp |
| 0x18 | Leitungsfehler |
| 0x19 | Leitung Masse-Schluss |
| 0x1A | Leitung U-Batterie-Schluss |
| 0x1B | Programmierung fehlegeschlagen |
| 0x1C | Programmierung nicht mehr moeglich |
| 0x1D | CRC Fehler durch Schreiben Codierdaten |
| 0x1E | Mindestens ein Crashtelegramm gespeichert |
| 0x1F | Unterspannung |
| 0x20 | Masse-Schluss / Unterbrechung |
| 0x21 | U-Batterie-Schluss / Ansteuerungdefekt |
| 0x22 | Leitung verkoppelt |
| 0x23 | Zuendkreis verkoppelt |
| 0x23 | SLV codiert aber nicht k-Bus |
| 0xFF | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW_ANZ | UW_SATZ | UW1_NR | UW2_NR |
| --- | --- | --- | --- | --- |
| 0xFF | 0x02 | 0x01 | 0x01 | 0x02 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 2 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x01 | Beginnfehleruhr | Sek. |
| 0x02 | Endefehleruhr | Sek. |
