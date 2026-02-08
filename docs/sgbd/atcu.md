# atcu.prg

- Jobs: [21](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Automatik-Getriebesteuergeraet FPO ATCU |
| ORIGIN | BMW TI-433 Mellersh |
| REVISION | 0.03 |
| AUTHOR | BMW TI-433 Mellersh |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer AGS
- [START_MODUS](#job-start-modus) - Starten eines Diagnose-Modus fuer ECU
- [STOP_MODUS](#job-stop-modus) - Stop des aktuellen Diagnose-Modus fuer ECU
- [TESTER_PRESENT](#job-tester-present)
- [SECURITY_ACCESS](#job-security-access)
- [IDENT](#job-ident) - Ident-Daten fuer AGS
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers High-Konzept nach Lastenheft Codierung/Diagnose komplizierte Umweltbedingungen: analog, digital, diskret
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen fuer AGS
- [CODIER_CS_PRUEFEN](#job-codier-cs-pruefen) - Ueberpruefen der Codier-Checksumme fuer AGS
- [CENTRAL_CODE_PRUEFEN](#job-central-code-pruefen) - Ueberpruefen der Codier-Checksumme fuer AGS
- [STATUS_TEMP_LESEN](#job-status-temp-lesen) - Status der Temperatur-Eingaenge
- [STATUS_SPEED_LESEN](#job-status-speed-lesen) - Status der speed-Eingaenge
- [STATUS_TORQUE_LESEN](#job-status-torque-lesen)
- [STATUS_PRESSURE_LESEN](#job-status-pressure-lesen)
- [STATUS_THROTTLE_LESEN](#job-status-throttle-lesen)
- [STATUS_DIGITAL_IN_LESEN](#job-status-digital-in-lesen)
- [STATUS_DIGITAL_OUT_LESEN](#job-status-digital-out-lesen)
- [STATUS_GEARS_LESEN](#job-status-gears-lesen)
- [STEUERN_STELLGLIED](#job-steuern-stellglied) - Ansteuern der Stellglieder

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

Init-Job fuer AGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-start-modus"></a>
### START_MODUS

Starten eines Diagnose-Modus fuer ECU

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODUS | string | gewuenschter Diagnose-Modus table DiagModus MODUS MODUS_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-modus"></a>
### STOP_MODUS

Stop des aktuellen Diagnose-Modus fuer ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-tester-present"></a>
### TESTER_PRESENT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _JOB_DATA | binary |  |
| _RESPONSE_DATA | binary |  |
| ATCU_PRESENT | int |  |

<a id="job-security-access"></a>
### SECURITY_ACCESS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS1 | string |  |
| JOB_STATUS | string |  |
| _JOB_DATA1 | binary |  |
| _JOB_DATA2 | binary |  |
| LOOPS | int |  |
| _RESPONSE_DATA1 | binary |  |
| _RESPONSE_DATA2 | binary |  |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer AGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_JAHR | int | Herstelldatum (Jahr) |
| ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| ID_DATUM_TAG | int | Herstelldatum (Tag) |
| ID_DATUM | string | Herstelldatum (TT.MM.JJJJ) |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_SW_NR | string | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender-Info-Feldes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_ZB_NR | string | Zusbaunummer |
| AIF_PROGG_NR | string | Programmiergeraet Seriennummer |
| AIF_KM_STAND | long | km-Stand |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers High-Konzept nach Lastenheft Codierung/Diagnose komplizierte Umweltbedingungen: analog, digital, diskret

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_ART_ANZ | int | Anzahl der Fehlerarten (hier immer 8) |
| F_ART1_NR | int | Fehlerartenbyte |
| F_ART1_TEXT | string | Fehlerart als Text |
| F_ART2_NR | int | Fehlerartenbyte |
| F_ART2_TEXT | string | Fehlerart als Text |
| F_ART3_NR | int | Fehlerartenbyte |
| F_ART3_TEXT | string | Fehlerart als Text |
| F_ART4_NR | int | Fehlerartenbyte |
| F_ART4_TEXT | string | Fehlerart als Text |
| F_ART5_NR | int | Fehlerartenbyte |
| F_ART5_TEXT | string | Fehlerart als Text |
| F_VORHANDEN | int | Fehler momentan vorhanden (Fehlerart) |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen fuer AGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-codier-cs-pruefen"></a>
### CODIER_CS_PRUEFEN

Ueberpruefen der Codier-Checksumme fuer AGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| CS_PROGRAMM | string | Programmbereich |
| CS_DATEN | string | Datenbereich |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-central-code-pruefen"></a>
### CENTRAL_CODE_PRUEFEN

Ueberpruefen der Codier-Checksumme fuer AGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| CENTRAL_CODING_KEY | binary | Antworttelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-temp-lesen"></a>
### STATUS_TEMP_LESEN

Status der Temperatur-Eingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_MOTORTEMPERATUR_WERT | int | MOTORTEMPERATUR |
| STAT_MOTORTEMPERATUR_EINH | string | MOTORTEMPERATUR |
| STAT_GETRIEBETEMPERATUR_WERT | int | GETRIEBETEMPERATUR |
| STAT_GETRIEBETEMPERATUR_EINH | string | GETRIEBETEMPERATUR |
| STAT_UBAT_WERT | real | UBat |
| STAT_UBAT_EINH | string | UBat |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-speed-lesen"></a>
### STATUS_SPEED_LESEN

Status der speed-Eingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_MOTORDREHZAHL_WERT | int |  |
| STAT_MOTORDREHZAHL_EINH | string |  |
| STAT_TURBINENDREHZAHL_WERT | int | Turbinendrehzahl |
| STAT_TURBINENDREHZAHL_EINH | string | Turbinendrehzahl |
| STAT_ABTRIEBSDREHZAHL_WERT | int | Abtriebsdrehzahl |
| STAT_ABTRIEBSDREHZAHL_EINH | string | Abtriebsdrehzahl |
| STAT_RADDREHZAHL_WERT | int |  |
| STAT_RADDREHZAHL_EINH | string |  |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-torque-lesen"></a>
### STATUS_TORQUE_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_TORQUE_WERT | int |  |
| STAT_TORQUE_EINH | string |  |
| STAT_TORQUE_OR_WERT | int |  |
| STAT_TORQUE_OR_EINH | string |  |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-pressure-lesen"></a>
### STATUS_PRESSURE_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_LINE_PRES_WERT | int |  |
| STAT_LINE_PRES_EINH | string |  |
| STAT_LOCK_UP_WERT | int |  |
| STAT_LOCK_UP_EINH | string |  |
| STAT_2T4ORB_WERT | int |  |
| STAT_2T4ORB_EINH | string |  |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-throttle-lesen"></a>
### STATUS_THROTTLE_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_DKG_WERT | int | DKG/WDK_BL |
| STAT_DKG_EINH | string | DKG/WDK_BL |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-digital-in-lesen"></a>
### STATUS_DIGITAL_IN_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_SPORT_MODE_EIN | int | 0 oder 1 |
| STAT_SNOW_MODE_EIN | int | 0 oder 1 |
| STAT_NORMAL_MODE_EIN | int | 0 oder 1 |
| STAT_MANUAL_MODE_EIN | int | 0 oder 1 |
| STAT_TIP_UP_EIN | int | 0 oder 1 |
| STAT_TIP_DOWN_EIN | int | 0 oder 1 |
| STAT_STOPSIGNAL_EIN | int | 0 oder 1 |
| STAT_BREMSSIGNAL_EIN | int | 0 oder 1 |
| STAT_OBD_FAULTS_EIN | int | 0 oder 1 |
| STAT_ATFL_OVERTEMP_EIN | int | 0 oder 1 |
| STAT_IGN_EIN | int | 0 oder 1 |
| STAT_CRUISE_EIN | int | 0 oder 1 |
| STAT_SH_INT_FAULT_EIN | int | 0 oder 1 |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-digital-out-lesen"></a>
### STATUS_DIGITAL_OUT_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_SHIFT_SOL_A | int | 0 oder 1 |
| STAT_SHIFT_SOL_B | int | 0 oder 1 |
| STAT_SHIFT_SOL_C | int | 0 oder 1 |
| STAT_LOWC_TIM_SOL | int | 0 oder 1 |
| STAT_RDCN_TIM_SOL | int | 0 oder 1 |
| STAT_24B_TIM_SOL | int | 0 oder 1 |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-gears-lesen"></a>
### STATUS_GEARS_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_GANG | int | 1. 2. 3. 4. 5.Gang |
| STAT_GANG_TEXT | string | Gang im Klartext |
| STAT_WAEHLHEBEL_POSITION | string | P, R, N, D, 4, 3, 2 |
| STAT_WAEHLHEBEL_POSITION_NR | int |  |
| STAT_SCHALTUNGSART_AKTUELL | string | 11 Texte, aktuelle Schaltung |
| STAT_SCHALTUNGSART_AKTUELL_NR | int |  |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-steuern-stellglied"></a>
### STEUERN_STELLGLIED

Ansteuern der Stellglieder

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STELLGL | string | Anzusteuerndes Stellglied table Stellglieder STELLGLIED PIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (63 × 2)
- [FORTTEXTE](#table-forttexte) (33 × 2)
- [FARTMATRIX](#table-fartmatrix) (1 × 14)
- [FARTTEXTE](#table-farttexte) (11 × 2)
- [STELLGLIEDER](#table-stellglieder) (9 × 2)

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 33 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0748 | Relais PL |
| 0x1748 | Relais 24/B |
| 0x0702 | GND Rueckleitung       |
| 0x0743 | Relais LU |
| 0x0753 | Magnetventil A |
| 0x0758 | Magnetventil B |
| 0x0763 | Magnetventil C |
| 0x1785 | Low/C Zeitrelais |
| 0x1786 | RDCN Zeitrelais |
| 0x1787 | 24/B Zeitrelais |
| 0x0705 | Blockierschalter |
| 0x0790 | Modusschalter |
| 0x1815 | Tiptronic Eingaenge |
| 0x1715 | Zwischensensor |
| 0x0720 | Fahrzeuggeschwindigkeitssensor |
| 0x0715 | Turbinensensor |
| 0x0710 | ATF Temp Sensor |
| 0x0731 | 1. Gangverhaeltnis |
| 0x0732 | 1. Gangverhaeltnis |
| 0x0733 | 1. Gangverhaeltnis |
| 0x0734 | 1. Gangverhaeltnis |
| 0x0735 | 1. Gangverhaeltnis |
| 0x0736 | Rueckwaertsgangverhaeltnis |
| 0x0740 | Wandlerkupplung |
| 0x1562 | Stromversorgunsspannung |
| 0x1605 | EEPROM |
| 0x1840 | CAN Bus |
| 0x1841 | CAN Bus-Monitor |
| 0x1842 | CAN Pegel-Monitor |
| 0x1843 | CAN Timeout-Monitor |
| 0x1844 | Motordrehzahl/Temp/Drehmoment/Drossel |
| 0x1825 | Shift-Verriegelung SGU |
| 0xFFFF | Unbekannter Fehler |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 1 rows × 14 columns

| ORT | A1_0 | A1_1 | A1_2 | A1_3 | A1_4 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 0xFE | 0x01 | 0x02 | 0x04 | 0x08 | 0x00 | 0x10 | 0x00 | 0x20 | 0x00 | 0x40 | 0x00 | 0x80 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 11 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Oberhalb maximaler Pegel |
| 0x02 | Unterhalb minimaler Pegel |
| 0x04 | Kein Signal |
| 0x08 | Ungueltiges Signal |
| 0x10 | Test fertig |
| 0x20 | Fehler gespeichert |
| 0x40 | Fehler jetzt vorhanden |
| 0x80 | Warnlampe ein |
| 0xFE | Symptom kein Fehler |
| 0xFF | Unbekannte Fehlerart |

<a id="table-stellglieder"></a>
### STELLGLIEDER

Dimensions: 9 rows × 2 columns

| STELLGLIED | PIN |
| --- | --- |
| ALL_OFF | 0x0000 |
| 24/B_DUTY_SOL | 0x0080 |
| SHIFT_SOL_A | 0x0100 |
| SHIFT_SOL_B | 0x0200 |
| SHIFT_SOL_C | 0x0400 |
| LOW/C_TIM_SOL | 0x0800 |
| RDCN_TIM_SOL | 0x1000 |
| 24/B_TIM_SOL | 0x2000 |
| LU_DUTY_SOL | 0x4000 |
