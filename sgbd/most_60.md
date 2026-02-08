# most_60.prg

- Jobs: [9](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MOST_60 |
| ORIGIN | BMW VS-42 Christian Waas |
| REVISION | 0.951 |
| AUTHOR | BMW VS-42 Benoit Blaser, Armin David, Christian Waas |
| COMMENT | MOST-Busanalyse |
| PACKAGE | 1.41 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [DIAGNOSEPROTOKOLL_LESEN](#job-diagnoseprotokoll-lesen) - Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück
- [DIAGNOSEPROTOKOLL_SETZEN](#job-diagnoseprotokoll-setzen) - Wählt ein Diagnoseprotokoll aus
- [IDENT](#job-ident) - Identdaten
- [FS_LOESCHEN_DETAIL](#job-fs-loeschen-detail) - Einzelne DTC loeschen fürs Head-Unit
- [FS_LOESCHEN](#job-fs-loeschen) - Infospeicher loeschen in Abhängigkeit von der Steuergeraete-Gruppe siehe ClearDiagnosticInformation in LH Diagnose Teil 2
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen in Abhängigkeit von der Steuergeraete-Gruppe siehe ClearDiagnosticInformation in LH Diagnose Teil 2
- [FS_LESEN](#job-fs-lesen) - Auswertung Fehlerspeicher lesen detail + Infospeicher lesen detail Tester benötigt den Job-Namen FS_LESEN KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

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

<a id="job-diagnoseprotokoll-lesen"></a>
### DIAGNOSEPROTOKOLL_LESEN

Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_DIAG_PROT |
| DIAG_PROT_IST | string | Gibt das aktuelle gewählte Protokoll aus table KONZEPT_TABELLE KONZEPT_TEXT |
| DIAG_PROT_ANZAHL | int | Anzahl der Diagnoseprotokolle |
| DIAG_PROT_NR1 | string | Alle möglichen Diagnose-Protokolle Falls mehrere Protokolle möglich sind werden die entsprechenden Results DIAG_PROT_NRx dynamisch erzeugt |

<a id="job-diagnoseprotokoll-setzen"></a>
### DIAGNOSEPROTOKOLL_SETZEN

Wählt ein Diagnoseprotokoll aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_PROT | string | Diagnoseprotokoll table KONZEPT_TABELLE KONZEPT_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

<a id="job-ident"></a>
### IDENT

Identdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-fs-loeschen-detail"></a>
### FS_LOESCHEN_DETAIL

Einzelne DTC loeschen fürs Head-Unit

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Fehlercode |
| DIAG_ADRESSE | int | Diagnose Adresse des SGs Defaultwert 0x62 MOST-GW |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Infospeicher loeschen in Abhängigkeit von der Steuergeraete-Gruppe siehe ClearDiagnosticInformation in LH Diagnose Teil 2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | int | FUNKTIONALE_ADRESSE = 0xE9: K-CAN Steuergeräte FUNKTIONALE_ADRESSE = 0xEA: PT-CAN Steuergeräte FUNKTIONALE_ADRESSE = 0xEB: BYTEFLIGHT Steuergeräte FUNKTIONALE_ADRESSE = 0xEC: MOST Steuergeräte FUNKTIONALE_ADRESSE = 0xED: BOS und CBS Steuergeräte FUNKTIONALE_ADRESSE = 0xEE: Personalisierungs Steuergeräte FUNKTIONALE_ADRESSE = 0xEF: alle Steuergeräte Defaultwert: 0xEC ( MOST Steuergeräte ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen in Abhängigkeit von der Steuergeraete-Gruppe siehe ClearDiagnosticInformation in LH Diagnose Teil 2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | int | FUNKTIONALE_ADRESSE = 0xE9: K-CAN Steuergeräte FUNKTIONALE_ADRESSE = 0xEA: PT-CAN Steuergeräte FUNKTIONALE_ADRESSE = 0xEB: BYTEFLIGHT Steuergeräte FUNKTIONALE_ADRESSE = 0xEC: MOST Steuergeräte FUNKTIONALE_ADRESSE = 0xED: BOS und CBS Steuergeräte FUNKTIONALE_ADRESSE = 0xEE: Personalisierungs Steuergeräte FUNKTIONALE_ADRESSE = 0xEF: alle Steuergeräte Defaultwert: 0xEC ( alle MOST-Steuergeräte ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auswertung Fehlerspeicher lesen detail + Infospeicher lesen detail Tester benötigt den Job-Namen FS_LESEN KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GEWICHT_ERROR_NCE | char | Wert entspricht der Gewichtung für die Verdächtigung Default-Wert = 2 |
| GEWICHT_ERROR_REGISTRY_NEW | char | Wert entspricht der Gewichtung für die Verdächtigung Default-Wert = 3 |
| GEWICHT_ERROR_MONITORING | char | Wert entspricht der Gewichtung für die Verdächtigung Default-Wert = 2 |
| KM_BEGINN | char | Bis zu diesem Kilometer-Stand werden die Fehlerspeichereinträge unterdrückt Default-Wert = 50 km |
| KM_OFFSET | char | Vom aktuellen Kilometerstand vom KOMBI wird dieser Offset-Wert abgezogen Bei den letzten 16 km (Default) werden die Fehlerspeichereinträge unterdrückt Somit Fehlerbewertung in den km-Grenzen: KM_BEGINN bis KM_ENDE = KM_AKTUELL_KOMBI - KM_OFFSET Default-Wert = 16 km |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_ORT_NR | long | Wenn keine Kommunikation mit dem Gateway-SG (= CCC CHAMP CICR M-ASK CICM oder CHAMP2) möglich ist =&gt; 0xFFF1 Wenn keine Kommunikation mit anderen MOST_SG'en (= Ringbruch) möglich ist =&gt; 0xFFF2 Wenn nach der MOST-Systemanalyse als Ergebnis ein MOST-SG verdächtigt werden kann dann wird der Fehlerort 0xFFF3 ausgegeben Wenn nach der MOST-Systemanalyse als Ergebnis zwei MOST-SG'e verdächtigt werden können dann wird der Fehlerort 0xFFF4 ausgegeben Wenn OPPS/OPS Error_Registry_New verursacht hat =&gt; 0xFFF5 |
| F_UW_KM | long | Umweltbedingung: aktueller Kilometerstand vom Kombi Wertebereich: 0 - 524280 km |
| VARIANTE_CCC_MASK_CHAMP | unsigned char | 5: CICMR 4:CHAMP2R 3: CICR verbaut 2: CHAMP verbaut, 1: CCC verbaut, 0: M-ASK oder M-ASK2 verbaut |
| OPPS_OPS_IN_SOLLKONFIG | unsigned char | 1: OPPS/OPS in der Sollkonfiguration gespeichert , 0: Kein OPPS/OPS in der Sollkonfiguration gespeichert |
| MOST_SG_ANZAHL | unsigned char | gibt die Anzahl der verbauten MOST-SG'e zurück MOST_SG_ANZAHL = 1: nur CICR, CCC, CHAMP, M-ASK, CHAMP2 bzw. CICMR verbaut |
| HFK_RESET_DVDC | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_TEL | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_AMP | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_KHI | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_CDC | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_HUD | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_NAV | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_VID | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_RAD | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_IBOC | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_DAB | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_MULF2 | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| HFK_RESET_CCC_MASK_CHAMP | unsigned char | Reset-Häufigkeit als Zahl für je 5 wirklich gespeicherte Resets im SG wird im Result 1 Reset angezeigt Wertebereich Resets im SG: 0 - 255 Somit Wertebereich für Result: 0 - 51 |
| ERROR_NCE_SG_ADR_1 | unsigned char | Steuergeräte-Adresse in der Umweltbedingung 2 vom CCC bzw. Umweltbedingung 1 vom M-ASK/M-ASK2/CHAMP Gültiger Wertebereich 0 - 255 Default: 0 (wenn keine Umweltbedingung gespeichert ist) |
| ERROR_NCE_SG_ADR_2 | unsigned char | Steuergeräte-Adresse in der Umweltbedingung 2 vom CCC bzw. Umweltbedingung 1 vom M-ASK/M-ASK2/CHAMP Gültiger Wertebereich 0 - 255 Default: 0 (wenn keine Umweltbedingung gespeichert ist) |
| ERROR_NCE_SG_ADR_3 | unsigned char | Steuergeräte-Adresse in der Umweltbedingung 2 vom CCC bzw. Umweltbedingung 1 vom M-ASK/M-ASK2/CHAMP Gültiger Wertebereich 0 - 255 Default: 0 (wenn keine Umweltbedingung gespeichert ist) |
| ERROR_REGISTRY_NEW_ADR_1 | unsigned char | Steuergeräte-Adresse in der Umweltbedingung 2 vom CCC bzw. Umweltbedingung 1 vom M-ASK/M-ASK2/CHAMP Gültiger Wertebereich 0 - 255 Default: 0 (wenn keine Umweltbedingung gespeichert ist) |
| ERROR_REGISTRY_NEW_ADR_2 | unsigned char | Steuergeräte-Adresse in der Umweltbedingung 2 vom CCC bzw. Umweltbedingung 1 vom M-ASK/M-ASK2/CHAMP Gültiger Wertebereich 0 - 255 Default: 0 (wenn keine Umweltbedingung gespeichert ist) |
| ERROR_REGISTRY_NEW_ADR_3 | unsigned char | Steuergeräte-Adresse in der Umweltbedingung 2 vom CCC bzw. Umweltbedingung 1 vom M-ASK/M-ASK2/CHAMP Gültiger Wertebereich 0 - 255 Default: 0 (wenn keine Umweltbedingung gespeichert ist) |
| ERROR_MONITORING_ADR_1 | unsigned char | Steuergeräte-Adresse in der Umweltbedingung 2 vom CCC bzw. Umweltbedingung 1 vom M-ASK/M-ASK2/CHAMP Gültiger Wertebereich 0 - 255 Default: 0 (wenn keine Umweltbedingung gespeichert ist) |
| ERROR_MONITORING_ADR_2 | unsigned char | Steuergeräte-Adresse in der Umweltbedingung 2 vom CCC bzw. Umweltbedingung 1 vom M-ASK/M-ASK2/CHAMP Gültiger Wertebereich 0 - 255 Default: 0 (wenn keine Umweltbedingung gespeichert ist) |
| ERROR_MONITORING_ADR_3 | unsigned char | Steuergeräte-Adresse in der Umweltbedingung 2 vom CCC bzw. Umweltbedingung 1 vom M-ASK/M-ASK2/CHAMP Gültiger Wertebereich 0 - 255 Default: 0 (wenn keine Umweltbedingung gespeichert ist) |
| HFK_IPC_OPERATION_MASK | unsigned char | Reset-Häufigkeit als Zahl Wertebereich 0 - 255 |
| HFK_IPC_STARTUP_MASK | unsigned char | Reset-Häufigkeit als Zahl Wertebereich 0 - 255 |
| MOST_DVDC | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_TEL | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_AMP | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_KHI | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_CDC | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_HUD | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_NAV | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_VID | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_RAD | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_IBOC | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_DAB | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_MULF2 | char | Rückgabewert = Summe der Verdächtigungen |
| MOST_CCC_MASK_CHAMP | char | Rückgabewert = Summe der Verdächtigungen |
| MAX_VERDACHT_1 | unsigned char | SG mit maximalen Verdächtigungen: Rückgabewert ist die SG-Adresse |
| MAX_VERDACHT_2 | unsigned char | SG mit zweit-maximalen Verdächtigungen: Rückgabewert ist die SG-Adresse |
| QUALITAET_STERNE_1 | unsigned char | Aussage der Qualität der Verdächtigungen von Steuergerät MAX_VERDACHT_1 5 Sterne =&gt; Aussage der Qualität sehr gut 0 Sterne =&gt; Aussage der Qualität sehr schlecht =&gt; führt im Kurztest am Diagnosetester zu keinem Kreuz |
| QUALITAET_STERNE_2 | unsigned char | Aussage der Qualität der Verdächtigungen von Steuergerät MAX_VERDACHT_2 5 Sterne =&gt; Aussage der Qualität sehr gut 0 Sterne =&gt; Aussage der Qualität sehr schlecht =&gt; führt im Kurztest am Diagnosetester zu keinem Kreuz |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (116 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (5 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 95 rows × 2 columns

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
| ?03? | ERROR_ECU_INCORRECT_LEN |
| ?04? | ERROR_ECU_INCORRECT_LIN_RESPONSE_ID |
| ?05? | ERROR_ECU_INCORRECT_LIN_LEN |
| ?10? | ERROR_F_CODE |
| ?11? | ERROR_TABLE |
| ?12? | ERROR_INTERPRETATION |
| ?13? | ERROR_F_POS |
| ?20? | ERROR_SEGMENT |
| ?21? | ERROR_ADDRESS |
| ?22? | ERROR_NUMBER |
| ?30? | ERROR_DATA |
| ?40? | ERROR_MODE |
| ?41? | ERROR_BAUDRATE |
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
| ?76? | ERROR_CHECKSUM |
| ?80? | ERROR_FLASH_SIGNATURE_CHECK |
| ?81? | ERROR_VEHICLE_IDENTIFICATION_NR |
| ?82? | ERROR_PROGRAMMING_DATE |
| ?83? | ERROR_ASSEMBLY_NR |
| ?84? | ERROR_CALIBRATION_DATASET_NR |
| ?85? | ERROR_EXHAUST_REGULATION_OR_TYPE_APPROVAL_NR |
| ?86? | ERROR_REPAIR_SHOP_NR |
| ?87? | ERROR_TESTER_SERIAL_NR |
| ?88? | ERROR_MILAGE |
| ?89? | ERROR_PROGRAMMING_REFERENCE |
| ?8A? | ERROR_NO_FREE_UIF |
| ?8B? | ERROR_MAX_UIF |
| ?8C? | ERROR_SIZE_UIF |
| ?8D? | ERROR_LEVEL |
| ?8E? | ERROR_KEY |
| ?8F? | ERROR_AUTHENTICATION |
| ?90? | ERROR_NO_DREF |
| ?91? | ERROR_CHECK_PECUHN |
| ?92? | ERROR_CHECK_PRGREF |
| ?93? | ERROR_AIF_NR |
| ?94? | ERROR_CHECK_DREF |
| ?95? | ERROR_CHECK_HWREF |
| ?96? | ERROR_CHECK_HWREF |
| ?97? | ERROR_CHECK_PRGREFB |
| ?98? | ERROR_CHECK_VMECUH*NB |
| ?99? | ERROR_CHECK_PRGREFB |
| ?9A? | ERROR_CHECK_VMECUH*N |
| ?9B? | ERROR_MOST_CAN_GATEWAY_DISABLE |
| ?9C? | ERROR_NO_P2MIN |
| ?9D? | ERROR_NO_P2MAX |
| ?9E? | ERROR_NO_P3MIN |
| ?9F? | ERROR_NO_P3MAX |
| ?A0? | ERROR_NO_P4MIN |
| ?B0? | ERROR_DIAG_PROT |
| ?B1? | ERROR_SG_ADRESSE |
| ?B2? | ERROR_SG_MAXANZAHL_AIF |
| ?B3? | ERROR_SG_GROESSE_AIF |
| ?B4? | ERROR_SG_ENDEKENNUNG_AIF |
| ?B5? | ERROR_SG_AUTHENTISIERUNG |
| ?C0? | ERROR_TELEGRAM_LEN_OUT_OFF_RANGE |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 116 rows × 2 columns

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
| 0x72 | AISIN AW CO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
| 0x76 | CEL |
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
| 0x81 | Tyco Electronics |
| 0x82 | Paragon AG |
| 0x83 | IEE S.A |
| 0x84 | TEMIC AUTOMOTIVE of NA |
| 0x85 | AKsys GmbH |
| 0x86 | META System |
| 0x87 | Hülsbeck & Fürst GmbH & Co KG |
| 0x88 | Mann & Hummel Automotive GmbH |
| 0x89 | Brose Fahrzeugteile GmbH & Co |
| 0x90 | Keihin |
| 0x91 | Vimercati S.p.A. |
| 0x92 | CRH |
| 0x93 | TPO Display Corp. |
| 0x94 | KÜSTER Automotive Control |
| 0x95 | Hitachi Automotive |
| 0x96 | Continental Automotive |
| 0x97 | TI-Automotive |
| 0x98 | Hydro |
| 0x99 | Johnson Controls |
| 0x9A | Takata- Petri |
| 0x9B | Mitsubishi Electric B.V. (Melco) |
| 0x9C | Autokabel |
| 0x9D | GKN-Driveline |
| 0x9E | Zollner Elektronik AG |
| 0x9F | PEIKER acustics GmbH |
| 0xA0 | Bosal-Oris |
| 0xA1 | Cobasys |
| 0xA2 | Lighting Reutlingen GmbH |
| 0xA3 | CONTI VDO |
| 0xA4 | ADC Automotive Distance Control Systems GmbH |
| 0xA5 | Funkwerk Dabendorf GmbH |
| 0xA6 | Lame |
| 0xA7 | Magna/Closures |
| 0xA8 | Wanyu |
| 0xA9 | Thyssen Krupp Presta |
| 0xFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 14 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Signal oder Wert oberhalb Schwelle |
| 0x02 | Signal oder Wert unterhalb Schwelle |
| 0x04 | kein Signal oder Wert |
| 0x08 | unplausibles Signal oder Wert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

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

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 14 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Signal oder Wert oberhalb Schwelle |
| 0x02 | Signal oder Wert unterhalb Schwelle |
| 0x04 | kein Signal oder Wert |
| 0x08 | unplausibles Signal oder Wert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 5 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFF1 | Keine Kommunikation mit der Headunit |
| 0xFFF2 | MOST Ringbruch |
| 0xFFF3 | MOST Systemanalyse (1) |
| 0xFFF4 | MOST Systemanalyse (2) |
| 0xFFF5 | Fehler: OPS/OPPS in Sollkonfiguration gespeichert |
