# MRS5K.prg

- Jobs: [34](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MRS5K fuer Airbag SG R50/R52/R53 |
| ORIGIN | BMW AG EE-52 K.Achatz |
| REVISION | 1.02 |
| AUTHOR | BERATA EngineeringConsulting Chafigoulline, BERATA EngineeringConsulting Schieferstein |
| COMMENT | SGBD MRS5 fuer K-Bus Anwendungen |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete Reset ausloesen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [IDENT](#job-ident) - Ident-Daten fuer AIRBAG MRS5K
- [SECURITY_CHANGE](#job-security-change) - Wechseln zum Sicherheitslevel 2 Change to security level 2
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Error memory quicktest High-Konzept nach Lastenheft
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Read error memory
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen Clear error memory
- [SPEICHER_LESEN](#job-speicher-lesen) - Speicher lesen Read memory
- [EAM_FLAGS_LESEN](#job-eam-flags-lesen) - Lesen der EAM (Ergebnis Ausloese Matrix) Flags read EAM
- [TYP_LESEN](#job-typ-lesen) - Lesen des Fahrzeugtyps (Baureihe) Read vehicle model
- [PARAMETER_LESEN](#job-parameter-lesen) - 16 Byte aus Parametersatz 1 lesen Read 16 bytes from block stated
- [BARCODE_LESEN](#job-barcode-lesen) - Lesen der MRSZ5K barcode infos Read unique ECU barcode
- [SG_LOGIN](#job-sg-login) - Berechtigung fuer EEPROM-Zugriffe Login to ECU
- [C_FS_LESEN](#job-c-fs-lesen) - 24 Byte aus Crashtelegram lesen Read 24 bytes from crashtelegram block stated
- [C_FS_LOESCHEN](#job-c-fs-loeschen) - Crashtelegram loeschen Delete crash telegram
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen Read codingdata
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren Write and check codingdata
- [C_FG_LESEN](#job-c-fg-lesen) - Kodierte KFZ-Herstellerdaten lesen Read coded productiondata
- [SYSTEMZEIT_LESEN](#job-systemzeit-lesen) - aktuelle Systemzeit lesen Read current system time
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Lesen des Pruefcodes, besteht aus Identifikationsdaten, Ausstattungsdaten, Systemzeit, System Zeit der letzten Fehlerloeschung, Barcode Daten und dem FS-Inhalt, jedes Telegrammpaket ist durch ein 0x00 abgeschlossen Read test codes (identdata, equipdata, system time, last error system time, barcode, errordata) Returned as strings separated by 0x00
- [STATUS_LESEN](#job-status-lesen) - Status des MRS5K lesen Read status of MRS5K
- [HERSTELLER_SPEZDATEN](#job-hersteller-spezdaten) - Herstellerspezifische Daten X = Gruppe Modus  : Default
- [HERSTELLERDATEN_LESEN](#job-herstellerdaten-lesen) - Kodierte KFZ-Herstellerdaten lesen Read coded productiondata
- [VERRIEGELUNG_LESEN](#job-verriegelung-lesen) - Auslesen der Verriegelung (= Pruefstempel) Read lock byte status
- [VERRIEGELUNG_SCHREIBEN](#job-verriegelung-schreiben) - Verriegelungsbytes setzen Set lock byte
- [MRSA_LESEN](#job-mrsa-lesen) - Lesen Seriennummer fuer jeden Satellit Read seriell number of all satellits
- [CONTROLLER_RESET](#job-controller-reset) - Zuruecksetzen des Controllers Reset ECU
- [STATUS_AUSSTATTUNG_EWS](#job-status-ausstattung-ews) - Ausstattung lesen Read equipment for EWS
- [STATUS_AUSSTATTUNG](#job-status-ausstattung) - Ausstattung lesen Read equipment configuration

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

Initialisierung und Kommunikationsparameter DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ARGUMENT, wenn Argumente nicht uebergeben oder ausser Bereich |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Steuergeraete Reset ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer AIRBAG MRS5K

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
| ANZ_BYTE | string | Anzahl der zu lesenden Bytes (1 - 16) Number of bytes to read (1 - 16) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Speicherinhalt |

<a id="job-eam-flags-lesen"></a>
### EAM_FLAGS_LESEN

Lesen der EAM (Ergebnis Ausloese Matrix) Flags read EAM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| BYTE_0 | int | Byte 0 der 1 EAM Flagsbytes |
| BYTE_1 | int | Byte 1 der 1 EAM Flagsbytes |
| LENKSEITE | int | 0 = Links-Lenker, 1 = Rechts-Lenker |
| US_SCHWELLEN | int | 0 = Flag ausgeschaltet, 1 = Flag eingeschaltet |
| CURTAIN_ITS_SCHRAEGCRASH | int | 0 = Flag ausgeschaltet, 1 = Flag eingeschaltet |
| GURTSTRAMMER_SEITENCRASH | int | 0 = Flag ausgeschaltet, 1 = Flag eingeschaltet |
| CURTAIN_ITS_GEGENUEBER | int | 0 = Flag ausgeschaltet, 1 = Flag eingeschaltet |
| LANGER_CURTAIN | int | 0 = ITS, 1 = Curtain |
| BYTE_1_0 | int | Byte 0 der 1 EAM Flagsbytes (wiederholt) |
| BYTE_1_1 | int | Byte 1 der 1 EAM Flagsbytes (wiederholt) |

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
| BLOCKNR | string | (0 &lt;= BLOCKNR &lt;= 43) --&gt; 16 Parameterbytes ab Byte (16*BLOCKNR) werden angefordert Between 0 and 43, byte 16*BLOCKNR returned |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Spezifizierte Parameterdaten Specified parameterdata |

<a id="job-barcode-lesen"></a>
### BARCODE_LESEN

Lesen der MRSZ5K barcode infos Read unique ECU barcode

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

<a id="job-sg-login"></a>
### SG_LOGIN

Berechtigung fuer EEPROM-Zugriffe Login to ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-c-fs-lesen"></a>
### C_FS_LESEN

24 Byte aus Crashtelegram lesen Read 24 bytes from crashtelegram block stated

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCKNR | string | (1 &lt;= BLOCKNR &lt;= 6) --&gt; 24 Parameterbytes ab Between 1 and 6, 24 bytes returned |

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

<a id="job-systemzeit-lesen"></a>
### SYSTEMZEIT_LESEN

aktuelle Systemzeit lesen Read current system time

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| SYSTEMZEIT | string | Systemzeit system time |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Lesen des Pruefcodes, besteht aus Identifikationsdaten, Ausstattungsdaten, Systemzeit, System Zeit der letzten Fehlerloeschung, Barcode Daten und dem FS-Inhalt, jedes Telegrammpaket ist durch ein 0x00 abgeschlossen Read test codes (identdata, equipdata, system time, last error system time, barcode, errordata) Returned as strings separated by 0x00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| PRUEFCODE | binary | Daten in Hex-Format |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Status des MRS5K lesen Read status of MRS5K

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG Hex answer from ECU |
| STAT_ZK0 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Airbag Fahrer Stufe 1 |
| STAT_ZK1 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Gurtstrammer Fahrer |
| STAT_ZK2 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Gurtstrammer Beifahrer |
| STAT_ZK3 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Airbag Beifahrer Stufe 1 |
| STAT_ZK4 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Sitzairbag vorne links |
| STAT_ZK5 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Sitzairbag vorne rechts |
| STAT_ZK6 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Seitenairbag vorne links |
| STAT_ZK7 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Seitenairbag vorne rechts |
| STAT_ZK8 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Curtain links / Knieairbag Fahrer |
| STAT_ZK9 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Curtain rechts / Knieairbag Beifahrer |
| STAT_ZK10 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Sicheheitsbattarieklemme |
| STAT_ZK11 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Airbag Beifahrer Stufe 2 |
| STAT_ZK12 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Airbag Fahrer Stufe 2 |
| STAT_ZK13 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Gurtstrammer hinten links |
| STAT_ZK14 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = ignition circuit, externer Fehler = external error Gurtstrammer hinten rechts |
| STAT_GKF_1 | int | 0 = nicht gesteckt, 1 = i.0 Buckle - driver, 0 = not plugged in Gurtkontakt Fahrer |
| STAT_GKF_2 | int | 0 = gesteckt, 1 = i.0 Buckle - driver, 0 = plugged in Gurtkontakt Fahrer |
| STAT_GKF_3 | int | 0 = Fehler, 1 = i.0 Buckle - driver, 0 = error Gurtkontakt Fahrer |
| STAT_GKBF_1 | int | 0 = nicht gesteckt, 1 = i.0 Buckle - passenger Gurtkontakt Beifahrer |
| STAT_GKBF_2 | int | 0 = gesteckt, 1 = i.0 Gurtkontakt Beifahrer |
| STAT_GKBF_3 | int | 0 = Fehler, 1 = i.0 Gurtkontakt Beifahrer |
| STAT_GKHL_1 | int | 0 = nicht gesteckt, 1 = i.0 Gurtkontakt hinten links |
| STAT_GKHL_2 | int | 0 = gesteckt, 1 = i.0 Gurtkontakt hinten links |
| STAT_GKHL_3 | int | 0 = Fehler, 1 = i.0 Gurtkontakt hinten links |
| STAT_GKHR_1 | int | 0 = nicht gesteckt, 1 = i.0 Gurtkontakt hinten rechts |
| STAT_GKHR_2 | int | 0 = gesteckt, 1 = i.0 Gurtkontakt hinten rechts |
| STAT_GKHR_3 | int | 0 = Fehler, 1 = i.0 Gurtkontakt hinten rechts |
| STAT_POS_1 | int | 0 = nicht geschaltet, 1 = i.0 Passenger Airbag Off Schalter |
| STAT_POS_2 | int | 0 = geschaltet, 1 = i.0 Passenger Airbag Off Schalter |
| STAT_POS_3 | int | 0 = Fehler, 1 = i.0 Passenger Airbag Off Schalter |
| STAT_POSI_1 | int | 0 = nicht geschaltet, 1 = i.0 Passenger Airbag Off Schalter Inverse |
| STAT_POSI_2 | int | 0 = geschaltet, 1 = i.0 Passenger Airbag Off Schalter Inverse |
| STAT_POSI_3 | int | 0 = Fehler, 1 = i.0 Passenger Airbag Off Schalter Inverse |
| STAT_SBE_OC3_1 | int | 0 = Beifahrer Sitz belegt, 1 = i.0 |
| STAT_SBE_OC3_2 | int | 0 = Beifahrer Sitz nicht belegt, 1 = i.0 |
| STAT_SBE_OC3_3 | int | 0 = Fehler, 1 = i.0 |
| STAT_SITZBELEGUNG | int | SBE/OC3 Sitzbelegung 0: Sitz unbelegt 1: Sitz belegt -1: SBE(OC3) nicht verbaut / Fehler SBE(OC3) |
| STAT_FEHLER | int | SBE/OC3 Sitzbelegung SBE/OC3 Fehler-Status 0: kein Fehler 1: SBE/OC3-Fehler |
| STAT_SBE_VERBAUT | int | SBE Sitzbelegung 0: System nicht verbaut 1: System verbaut |
| STAT_OC3_VERBAUT | int | OC3 Sitzbelegung 0: kein Fehler 1: System verbaut |
| STAT_FREIGABE | int | OC3 Sitzbelegung 0: kein Fehler 1: System nicht freigegeben |
| STAT_DATENSPEICHER | int | OC3 Sitzbelegung OC3 Datenspeicher-Status 0: kein Fehler 1: Datenspeicher voll |
| STAT_GEWICHTSKLASSE | int | OC3 Sitzbelegung OC3 Gewichtsklasse PL2 US 0: Gewichtsklasse "0" (Leerer Sitz) 1: Gewichtsklasse "1" (Kindersitz) 2: Gewichtsklasse "2" (&gt;=5% Frau / 45kg) 3: Gewichtsklasse "3" (95% Mann) Vorgehalten 4: Gewichtsklasse "4" -1: OC3 nicht verbaut / Fehler OC3  Hinweis: Switch von Klasse 0 auf Belegungsstatus erfolgt sofort Switch von Belegungsstatus auf Klasse 0 erfolgt mit einer Verzoegerung von 6 Sekunden. |
| STAT_GEWICHTSKLASSE_KINDERSITZ | int | OC3 Sitzbelegung 0: kein Fehler 1: OC3 Gewichtsklasse 1: (Kindersitz) siehe Hinweis bei Result "STAT_GEWICHTSKLASSE"! |
| STAT_GEWICHTSKLASSE_SITZ_BELEGT | int | OC3 Sitzbelegung 0: kein Fehler OC3 Gewichtsklasse 2: (&gt;=5% Frau / 45kg) siehe Hinweis bei Result "STAT_GEWICHTSKLASSE"! |
| STAT_GEWICHTSKLASSE_UNDEFINIERT | int | OC3 Sitzbelegung 0: OC3 Gewichtsklasse definiert 1: OC3 Gewichtsklasse nicht definiert |
| STAT_OC3_1 | int | 0 = System verbaut, 1 = i.0 Occupant Clasification System |
| STAT_OC3_2 | int | 0 = noch nicht freigegeben, 1 = i.0 Occupant Clasification System |
| STAT_OC3_3 | int | 0 = Datenspeicher voll, 1 = i.0 Occupant Clasification System |
| STAT_OC3_KLASSE0 | int | 0 = OC3 Klasse 0, 1 = i.0 Occupant Clasification System |
| STAT_OC3_KLASSE1 | int | 0 = OC3 Klasse 1, 1 = i.0 Occupant Clasification System |
| STAT_OC3_KLASSE2 | int | 0 = OC3 Klasse 2, 1 = i.0 Occupant Clasification System |
| STAT_OC3_KLASSE3 | int | 0 = OC3 Klasse 3, 1 = i.0 Occupant Clasification System |
| STAT_OC3_KLASSE4 | int | 0 = OC3 Klasse 4, 1 = i.0 Occupant Clasification System |
| STAT_UFL_1 | int | 0 = sendet Fehler, 1 = i.0 UPFRONT-Sensor links |
| STAT_UFL_2 | int | 0 = Kommunikationsfehler, 1 = i.0 UPFRONT-Sensor links |
| STAT_UFL_3 | int | 0 = Leitungsfehler, 1 = i.0 UPFRONT-Sensor links |
| STAT_UFL_4 | int | 0 = falscher Typ, 1 = i.0 UPFRONT-Sensor links |
| STAT_UFR_1 | int | 0 = sendet Fehler, 1 = i.0 UPFRONT-Sensor rechts |
| STAT_UFR_2 | int | 0 = Kommunikationsfehler, 1 = i.0 UPFRONT-Sensor rechts |
| STAT_UFR_3 | int | 0 = Leitungsfehler, 1 = i.0 UPFRONT-Sensor rechts |
| STAT_UFR_4 | int | 0 = falscher Typ, 1 = i.0 UPFRONT-Sensor rechts |
| STAT_SSTL_1 | int | 0 = sendet Fehler, 1 = i.0 Seitensensor Tür links |
| STAT_SSTL_2 | int | 0 = Kommunikationsfehler, 1 = i.0 Seitensensor Tür links |
| STAT_SSTL_3 | int | 0 = Leitungsfehler, 1 = i.0 Seitensensor Tür links |
| STAT_SSTL_4 | int | 0 = falscher Typ, 1 = i.0 Seitensensor Tür links |
| STAT_SSTR_1 | int | 0 = sendet Fehler, 1 = i.0 Seitensensor Tür rechts |
| STAT_SSTR_2 | int | 0 = Kommunikationsfehler, 1 = i.0 Seitensensor Tür rechts |
| STAT_SSTR_3 | int | 0 = Leitungsfehler, 1 = i.0 Seitensensor Tür rechts |
| STAT_SSTR_4 | int | 0 = falscher Typ, 1 = i.0 Seitensensor Tür rechts |
| STAT_SSBL_1 | int | 0 = sendet Fehler, 1 = i.0 Seitensensor B-Saeule links |
| STAT_SSBL_2 | int | 0 = Kommunikationsfehler, 1 = i.0 Seitensensor B-Saeule links |
| STAT_SSBL_3 | int | 0 = Leitungsfehler, 1 = i.0 Seitensensor B-Saeule links |
| STAT_SSBL_4 | int | 0 = falscher Typ, 1 = i.0 Seitensensor B-Saeule links |
| STAT_SSBR_1 | int | 0 = sendet Fehler, 1 = i.0 Seitensensor B-Saeule links |
| STAT_SSBR_2 | int | 0 = Kommunikationsfehler, 1 = i.0 Seitensensor B-Saeule rechts |
| STAT_SSBR_3 | int | 0 = Leitungsfehler, 1 = i.0 Seitensensor B-Saeule rechts |
| STAT_SSBR_4 | int | 0 = falscher Typ, 1 = i.0 Seitensensor B-Saeule rechts |

<a id="job-hersteller-spezdaten"></a>
### HERSTELLER_SPEZDATEN

Herstellerspezifische Daten X = Gruppe Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT Hex-Auftrag an SG Fkt. NR. = 0C Gruppe = Freigabestatus Zuendkreiswiderstaende |
| _TEL_ANTWORT | binary | Fkt. Nr. = 0C Gruppe = Freigabestatus Zuendkreiswiderstaende |
| STAT_ABF1_ZK0_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ABF1 = Airbag Fahrer Stufe 1 |
| STAT_GSF_ZK1_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit GSF = Gurtstrammer Fahrer |
| STAT_GSBF_ZK2_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit GSBF = Gurtstrammer Beifahrer |
| STAT_ABBF1_ZK3_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ABBF1 = Airbag Beifahrer Stufe 1 |
| STAT_SAVL_ZK4_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SAVL = Sitzairbag vorne links |
| STAT_SAVR_ZK5_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SAVR = Sitzairbag vorne rechts |
| STAT_SAHL_ZK6_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SAHL = Seitenairbag hinten links |
| STAT_SAHR_ZK7_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SAHR = Seitenairbag vorne rechts |
| STAT_CURTAIN_L_ZK8_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit Curtain links (E93 Knieairbag Fahrer) |
| STAT_CURTAIN_R_ZK9_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit Curtain rechts (E93 Knieairbag Beifahrer) |
| STAT_SBK_1_ZK10_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SBK = Sicheheitsbatterieklemme |
| STAT_ABBF2_ZK11_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ABBF2 = Airbag Beifahrer Stufe 2 |
| STAT_ABF2_ZK12_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ABF2 = Airbag Fahrer Stufe 2 |
| STAT_GSHL_ZK13_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit GSHL = Gurtstrammer hinten links |
| STAT_GSHR_ZK14_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit GSHR = Gurtstrammer hinten rechts |

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

<a id="job-mrsa-lesen"></a>
### MRSA_LESEN

Lesen Seriennummer fuer jeden Satellit Read seriell number of all satellits

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| UFR_DATA | binary | MRSA1=Upfront rechts |
| DOM_DATA_UFR | binary | Ergebnis fuer DOM-Datenbank |
| UFR_HERSTELLER | string |  |
| UFR_PRODUKT_JAHR | int |  |
| UFR_PRODUKT_WOCHE | int |  |
| UFR_SN | string |  |
| SSTR_DATA | binary | MRSA2=MRSA Tuere rechts |
| DOM_DATA_SSTR | binary | Ergebnis fuer DOM-Datenbank |
| SSTR_HERSTELLER | string |  |
| SSTR_PRODUKT_JAHR | int |  |
| SSTR_PRODUKT_WOCHE | int |  |
| SSTR_SN | string |  |
| SSBRX_DATA | binary | MRSA3=MRSA B-Saeule x rechts |
| DOM_DATA_SSBRX | binary | Ergebnis fuer DOM-Datenbank |
| SSBRX_HERSTELLER | string |  |
| SSBRX_PRODUKT_JAHR | int |  |
| SSBRX_PRODUKT_WOCHE | int |  |
| SSBRX_SN | string |  |
| SSBRY_DATA | binary | MRSA4=MRSA B-Saeule y rechts |
| DOM_DATA_SSBRY | binary | Ergebnis fuer DOM-Datenbank |
| SSBRY_HERSTELLER | string |  |
| SSBRY_PRODUKT_JAHR | int |  |
| SSBRY_PRODUKT_WOCHE | int |  |
| SSBRY_SN | string |  |
| SSBLX_DATA | binary | MRSA5=MRSA B-Saeule x links |
| DOM_DATA_SSBLX | binary | Ergebnis fuer DOM-Datenbank |
| SSBLX_HERSTELLER | string |  |
| SSBLX_PRODUKT_JAHR | int |  |
| SSBLX_PRODUKT_WOCHE | int |  |
| SSBLX_SN | string |  |
| SSBLY_DATA | binary | MRSA6=MRSA B-Saeule y links |
| DOM_DATA_SSBLY | binary | Ergebnis fuer DOM-Datenbank |
| SSBLY_HERSTELLER | string |  |
| SSBLY_PRODUKT_JAHR | int |  |
| SSBLY_PRODUKT_WOCHE | int |  |
| SSBLY_SN | string |  |
| UFL_DATA | binary | MRSA7=Upfront links |
| DOM_DATA_UFL | binary | Ergebnis fuer DOM-Datenbank |
| UFL_HERSTELLER | string |  |
| UFL_PRODUKT_JAHR | int |  |
| UFL_PRODUKT_WOCHE | int |  |
| UFL_SN | string |  |
| SSTL_DATA | binary | MRSA8=MRSA Tuere links |
| DOM_DATA_SSTL | binary | Ergebnis fuer DOM-Datenbank |
| SSTL_HERSTELLER | string |  |
| SSTL_PRODUKT_JAHR | int |  |
| SSTL_PRODUKT_WOCHE | int |  |
| SSTL_SN | string |  |

<a id="job-controller-reset"></a>
### CONTROLLER_RESET

Zuruecksetzen des Controllers Reset ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-status-ausstattung-ews"></a>
### STATUS_AUSSTATTUNG_EWS

Ausstattung lesen Read equipment for EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_AUSSTATTUNG_EWS | string | x Ausstattungsbytes als String Equipment bytes as String |

<a id="job-status-ausstattung"></a>
### STATUS_AUSSTATTUNG

Ausstattung lesen Read equipment configuration

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_BYTE_0 | int | Byte 0 der 7 Ausstattungsbytes |
| STAT_BYTE_1 | int | Byte 1 der 7 Ausstattungsbytes |
| STAT_BYTE_2 | int | Byte 2 der 7 Ausstattungsbytes |
| STAT_BYTE_3 | int | Byte 3 der 7 Ausstattungsbytes |
| STAT_BYTE_4 | int | Byte 4 der 7 Ausstattungsbytes |
| STAT_BYTE_5 | int | Byte 5 der 7 Ausstattungsbytes |
| STAT_BYTE_6 | int | Byte 6 der 7 Ausstattungsbytes |
| STAT_BYTE_7 | int | Byte 7 der 7 Ausstattungsbytes |
| STAT_ABF1_ZK0_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut 0 = not included,  1 = included ZK = ignition circuit ABF1 = Airbag Fahrer Stufe 1 |
| STAT_GSF_ZK1_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit GSF = Gurtstrammer Fahrer |
| STAT_GSBF_ZK2_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit GSBF = Gurtstrammer Beifahrer |
| STAT_ABBF1_ZK3_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit ABBF1 = Airbag Beifahrer Stufe 1 |
| STAT_SAVL_ZK4_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit SAVL = Sitzairbag vorne links |
| STAT_SAVR_ZK5_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit SAVR = Sitzairbag vorne rechts |
| STAT_SAHL_ZK6_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit SAHL = Seitenairbag vorne links |
| STAT_SAHR_ZK7_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit SAHR = Seitenairbag vorne rechts |
| STAT_CURTAIN_L_ZK8_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit Curtain links |
| STAT_KNAF_ZK8_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit KNAF = Knieairbag Fahrer |
| STAT_CURTAIN_R_ZK9_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit Curtain rechts |
| STAT_KNABF_ZK9_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit KNABF = Knieairbag Beifahrer |
| STAT_SBK_1_ZK10_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit SBK = Sicheheitsbattarieklemme |
| STAT_ABBF2_ZK11_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit ABBF2 = Airbag Beifahrer Stufe 2 |
| STAT_ABF2_ZK12_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit ABF2 = Airbag Fahrer Stufe 2 |
| STAT_GSHL_ZK13_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit GSHL = Gurtstrammer hinten links |
| STAT_GSHR_ZK14_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit GSHR = Gurtstrammer hinten rechts |
| STAT_UPFRONT_L_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut UPFRONT-Sensor links |
| STAT_UPFRONT_R_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut UPFRONT-Sensor rechts |
| STAT_MRSA_TUERE_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Seitensensor Tür |
| STAT_GKF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Buckle - driver Gurtkontakt Fahrer |
| STAT_GKBF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Buckle - passenger Gurtkontakt Beifahrer |
| STAT_GKHL_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Gurtkontakt hinten links |
| STAT_GKHR_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Gurtkontakt hinten rechts |
| STAT_POS_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Passenger Airbag Off Schalter |
| STAT_POSI_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Passenger Airbag Off Schalter Inverse |
| STAT_SBE_1_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Seat occupancy recognition 1 |
| STAT_OC3_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Occupant Clasification System |
| STAT_SBE_1_STATUS | int | 0 = keine Verzoegerung, 1 = Verzoegerung Seat occupancy recognition status delay |
| STAT_SLVF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut SLV Fahrer |
| STAT_SLVBF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut SLV Beifahrer |
| STAT_ROLLOVER_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| STAT_POL_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| STAT_AWL_DIREKT_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| STAT_AGW_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut AGW = Akustische Gurtwarnung |
| STAT_SBR_FA_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| STAT_SBR_BF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| STAT_BYTE_1_0 | int | Byte 0 der 7 Ausstattungsbytes (wiederholt) |
| STAT_BYTE_1_1 | int | Byte 1 der 7 Ausstattungsbytes (wiederholt) |
| STAT_BYTE_1_2 | int | Byte 2 der 7 Ausstattungsbytes (wiederholt) |
| STAT_BYTE_1_3 | int | Byte 3 der 7 Ausstattungsbytes (wiederholt) |
| STAT_BYTE_1_4 | int | Byte 4 der 7 Ausstattungsbytes (wiederholt) |
| STAT_BYTE_1_5 | int | Byte 5 der 7 Ausstattungsbytes (wiederholt) |
| STAT_BYTE_1_6 | int | Byte 6 der 7 Ausstattungsbytes (wiederholt) |
| STAT_BYTE_1_7 | int | Byte 7 der 7 Ausstattungsbytes (wiederholt) |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (72 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (79 × 2)
- [FARTMATRIX](#table-fartmatrix) (79 × 17)
- [FARTTEXTE](#table-farttexte) (45 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (2 × 3)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 13 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| ?10? | ERROR_ARGUMENT |
| ?20? | ERROR_FEHLERANZAHL |
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 72 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen =&gt; Delphi |
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
| 0xFF | unbekannter Hersteller |

<a id="table-roverpartnumprefix"></a>
### ROVERPARTNUMPREFIX

Dimensions: 21 rows × 2 columns

| ROVER_NR | PREFIX |
| --- | --- |
| 0xA0 | AMR |
| 0xA1 | HHF |
| 0xA2 | JFC |
| 0xA3 | MKC |
| 0xA4 | SCB |
| 0xA5 | SRB |
| 0xA6 | XQC |
| 0xA7 | XQD |
| 0xA8 | XQE |
| 0xA9 | XVD |
| 0xAA | YAC |
| 0xAB | YDB |
| 0xAC | YFC |
| 0xAD | YUB |
| 0xAE | YWC |
| 0xAF | YWQ |
| 0xB0 | EGQ |
| 0xB1 | YIB |
| 0xB2 | YIC |
| 0xB3 | YIE |
| 0xXY | ??? |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 79 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Zuendkreis ZK0 / Airbag Fahrer Stufe 1 |
| 0x02 | Zuendkreis ZK1 / Gurtstrammer Fahrer |
| 0x03 | Zuendkreis ZK2 / Gurtstrammer Beifahrer |
| 0x04 | Zuendkreis ZK3 / Airbag Beifahrer Stufe 1 |
| 0x05 | Zuendkreis ZK4 / Sitzairbag vorne links |
| 0x06 | Zuendkreis ZK5 / Sitzairbag vorne rechts |
| 0x07 | Zuendkreis ZK6 / Sitzairbag hinten links |
| 0x08 | Zuendkreis ZK7 / Sitzairbag hinten rechts |
| 0x09 | Zuendkreis ZK8 / Curtainairbag links |
| 0x11 | Zuendkreis ZK8 / Knieairbag Fahrer |
| 0x0A | Zuendkreis ZK9 / Curtainairbag rechts |
| 0x12 | Zuendkreis ZK9 / Knieairbag Beifahrer |
| 0x0B | Zuendkreis ZK10 / Sicherheits-Batterie-Klemme |
| 0x0C | Zuendkreis ZK11 / Airbag Beifahrer Stufe 2 |
| 0x0D | Zuendkreis ZK12 / Airbag Fahrer Stufe 2 |
| 0x0E | Zuendkreis ZK13 / Gurtstrammer hinten links |
| 0x0F | Zuendkreis ZK14 / Gurtstrammer hinten rechts |
| 0x10 | Zuendkreis ZK15 / AUX1 |
| 0x30 | Zuendkreis ZK0 / Airbag Fahrer Stufe 1 |
| 0x31 | Zuendkreis ZK1 / Gurtstrammer Fahrer |
| 0x32 | Zuendkreis ZK2 / Gurtstrammer Beifahrer |
| 0x33 | Zuendkreis ZK3 / Airbag Beifahrer Stufe 1 |
| 0x34 | Zuendkreis ZK4 / Sitzairbag vorne links |
| 0x35 | Zuendkreis ZK5 / Sitzairbag vorne rechts |
| 0x36 | Zuendkreis ZK6 / Sitzairbag hinten links |
| 0x37 | Zuendkreis ZK7 / Sitzairbag hinten rechts |
| 0x38 | Zuendkreis ZK8 / Curtainairbag links |
| 0x40 | Zuendkreis ZK8 / Knieairbag Fahrer |
| 0x39 | Zuendkreis ZK9 / Curtainairbag rechts |
| 0x41 | Zuendkreis ZK9 / Knieairbag Beifahrer |
| 0x3A | Zuendkreis ZK10 / Sicherheits-Batterie-Klemme |
| 0x3B | Zuendkreis ZK11 / Airbag Beifahrer Stufe 2 |
| 0x3C | Zuendkreis ZK12 / Airbag Fahrer Stufe 2 |
| 0x3D | Zuendkreis ZK13 / Gurtstrammer hinten links |
| 0x3E | Zuendkreis ZK14 / Gurtstrammer hinten rechts |
| 0x3F | Zuendkreis ZK15 / AUX1 |
| 0x60 | Gurtkontakt Fahrer |
| 0x6A | Gurtkontakt Fahrer |
| 0x61 | Gurtkontakt Beifahrer |
| 0x6B | Gurtkontakt Beifahrer |
| 0x62 | Gurtkontakt hinten links |
| 0x6C | Gurtkontakt hinten links |
| 0x63 | Gurtkontakt hinten rechts |
| 0x6D | Gurtkontakt hinten rechts |
| 0x67 | Passenger Airbag Off Schalter (POS) |
| 0x6E | Passenger Airbag Off Schalter (POS) |
| 0x68 | Passenger Airbag Off Schalter (POS) inverse |
| 0x6F | Passenger Airbag Off Schalter (POS) inverse |
| 0x69 | Passenger Airbag Off Schalter (POS) |
| 0x70 | Sitz-Belegungs-Erkennung |
| 0x71 | Occupant Classification System (OC3) |
| 0x72 | Occupant Classification System (OC3) |
| 0x84 | UPFRONT  links |
| 0x85 | UPFRONT  links |
| 0x86 | UPFRONT  rechts |
| 0x87 | UPFRONT  rechts |
| 0x88 | B-Säule X-Richtung links |
| 0x89 | B-Säule X-Richtung links |
| 0x8A | B-Säule X-Richtung rechts |
| 0x8B | B-Säule X-Richtung rechts |
| 0x8C | B-Säule Y-Richtung links |
| 0x8D | B-Säule Y-Richtung links |
| 0x8E | B-Säule Y-Richtung rechts |
| 0x8F | B-Säule Y-Richtung rechts |
| 0x80 | MRSA Tuer links |
| 0x81 | MRSA Tuer links |
| 0x82 | MRSA Tuer rechts |
| 0x83 | MRSA Tuer rechts |
| 0x50 | Versorgungsspannung |
| 0x51 | Airbag Warnleuchte (AWL) |
| 0x52 | Passenger Airbag OFF Leuchte (POL) |
| 0x55 | TCU - Ausgang |
| 0x90 | EEPROM |
| 0x91 | Crashtelegramspeicher |
| 0x92 | Crashtelegramspeicher |
| 0x94 | Alert-Schwelle |
| 0x93 | Zentralsteuergeraet |
| 0xF0 | Zentralsteuergeraet - Interner Fehler |
| 0xFF | Zentralsteuergeraet - Unbekannter Fehler |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 79 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x02 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x03 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x04 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x05 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x06 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x07 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x08 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x09 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0A | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0B | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0C | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0D | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0E | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x0F | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x10 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x11 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x12 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0x05 | 0xFF | 0x06 | 0xFF | 0x07 | 0x08 | 0x09 |
| 0x30 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x31 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x32 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x33 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x34 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x35 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x36 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x37 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x38 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x39 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3A | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3B | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3C | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3D | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3E | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x3F | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x40 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x41 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x23 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x50 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x1F | 0xFF | 0x18 | 0x08 | 0x09 |
| 0x51 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x20 | 0xFF | 0x21 | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x52 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x20 | 0xFF | 0x21 | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x55 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x20 | 0xFF | 0x21 | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x60 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0x05 | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x6A | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x22 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x61 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0x05 | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x6B | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x22 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x62 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0x05 | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x6C | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x22 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x63 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0x05 | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x6D | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x22 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x67 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0x05 | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x6E | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x22 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x68 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0A | 0xFF | 0xFF | 0xFF | 0x05 | 0xFF | 0x0B | 0xFF | 0x0C | 0x08 | 0x09 |
| 0x6F | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0x22 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x69 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x03 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x70 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x0E | 0xFF | 0x0F | 0xFF | 0x10 | 0xFF | 0x11 | 0x08 | 0x09 |
| 0x71 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x24 | 0xFF | 0x25 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x72 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0xFF | 0xFF | 0x29 | 0xFF | 0x26 | 0xFF | 0x27 | 0x08 | 0x09 |
| 0x80 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x13 | 0xFF | 0x2C | 0xFF | 0x17 | 0xFF | 0x2A | 0x08 | 0x09 |
| 0x81 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x12 | 0xFF | 0x19 | 0xFF | 0x1A | 0xFF | 0x2D | 0xFF | 0x2B | 0x08 | 0x09 |
| 0x82 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x13 | 0xFF | 0x2C | 0xFF | 0x17 | 0xFF | 0x2A | 0x08 | 0x09 |
| 0x83 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x12 | 0xFF | 0x19 | 0xFF | 0x1A | 0xFF | 0x2D | 0xFF | 0x2B | 0x08 | 0x09 |
| 0x84 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x13 | 0xFF | 0xFF | 0xFF | 0x17 | 0xFF | 0x2A | 0x08 | 0x09 |
| 0x85 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x12 | 0xFF | 0x19 | 0xFF | 0x1A | 0xFF | 0x2D | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x86 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x13 | 0xFF | 0xFF | 0xFF | 0x17 | 0xFF | 0x2A | 0x08 | 0x09 |
| 0x87 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x12 | 0xFF | 0x19 | 0xFF | 0x1A | 0xFF | 0x2D | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x88 | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x13 | 0xFF | 0xFF | 0xFF | 0x17 | 0xFF | 0x2A | 0x08 | 0x09 |
| 0x89 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x12 | 0xFF | 0x19 | 0xFF | 0x1A | 0xFF | 0x2D | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x8A | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x13 | 0xFF | 0xFF | 0xFF | 0x17 | 0xFF | 0x2A | 0x08 | 0x09 |
| 0x8B | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x12 | 0xFF | 0x19 | 0xFF | 0x1A | 0xFF | 0x2D | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x8C | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x13 | 0xFF | 0xFF | 0xFF | 0x17 | 0xFF | 0x2A | 0x08 | 0x09 |
| 0x8D | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x12 | 0xFF | 0x19 | 0xFF | 0x1A | 0xFF | 0x2D | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x8E | 0xFF | 0x00 | 0x01 | 0x02 | 0xFF | 0x0D | 0xFF | 0x13 | 0xFF | 0xFF | 0xFF | 0x17 | 0xFF | 0x2A | 0x08 | 0x09 |
| 0x8F | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x12 | 0xFF | 0x19 | 0xFF | 0x1A | 0xFF | 0x2D | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x90 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x1C | 0xFF | 0x1D | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x91 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x1E | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x92 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x14 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0x94 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x28 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x93 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0x15 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0xF0 | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |
| 0xFF | 0xFF | 0xFF | 0x01 | 0x02 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x08 | 0x09 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 45 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Plausibilitaetsfehler |
| 0x01 | Fehler nicht vorhanden |
| 0x02 | Fehler aktuell vorhanden |
| 0x03 | POS-Ausgang Positiv und Inverse nicht komplementaer |
| 0x04 | Fehler Kurzschluss gegen Masse |
| 0x05 | Fehler Kurzschluss gegen U-Batt |
| 0x06 | Widerstand zu klein |
| 0x07 | Widerstand zu gross |
| 0x08 | Fehler nicht sporadisch |
| 0x09 | Fehler sporadisch |
| 0x0A | Widerstand nicht definiert oder Graubereich |
| 0x0B | Kriechstrom gegen Masse / Widerstand zu klein |
| 0x0C | Unterbrechung / Widerstand zu gross |
| 0x0D | Kommunikationsstoerung |
| 0x0E | Leitung gegen Masse |
| 0x0F | Leitung gegen Plus |
| 0x10 | Unterbrechung Sitzmatte |
| 0x11 | Kurzschluss Sitzmatte |
| 0x12 | kein ID-Telegramm empfangen |
| 0x13 | Sensorfehler |
| 0x14 | Drei Crashtelegramme sind gespeichert |
| 0x15 | Geraet ist nicht verriegelt |
| 0x17 | Falscher Messbereich |
| 0x18 | Ueberspannung |
| 0x19 | Leitung Masse-Schluss |
| 0x1A | Leitung U-Batterie-Schluss |
| 0x1C | EEPROM Layout passt nicht zur SW-Version |
| 0x1D | CRC Fehler durch Schreiben Codierdaten |
| 0x1E | Mindestens ein Crashtelegramm gespeichert |
| 0x1F | Unterspannung |
| 0x20 | Masse-Schluss / Unterbrechung |
| 0x21 | U-Batterie-Schluss / Ansteuerungdefekt |
| 0x22 | Leitung verkoppelt |
| 0x23 | Zuendkreis verkoppelt |
| 0x24 | OC3 sendet nicht |
| 0x25 | OC3 sendet Fehler |
| 0x26 | Datenspeicher voll |
| 0x27 | System noch nicht freigegeben |
| 0x28 | Ueberpruefung Ausloeseschwelle |
| 0x29 | System konnte nicht freigegeben werden |
| 0x2A | Sensordaten inplausibel |
| 0x2B | Drucksensor ausserhalb des Messbereichs |
| 0x2C | Absolutdruck - Uebertragungsstoerung |
| 0x2D | Leitungsfehler / MRSA verkoppelt |
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

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 17 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
| an | 1 |
| yes | 1 |
| no | 0 |
| on | 1 |
| off | 0 |
| up | 1 |
| down | 0 |
| true | 1 |
| false | 0 |
| 1 | 1 |
| 0 | 0 |
