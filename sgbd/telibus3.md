# telibus3.prg

- Jobs: [67](#jobs)
- Tables: [24](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | TCU 1.5 Malapert I-Bus |
| ORIGIN | BMW EI-43 Snijders |
| REVISION | 1.400 |
| AUTHOR | BMW EI-43 Snijders |
| COMMENT | N/A |
| PACKAGE | 1.03 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Identdaten
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete Reset ausloesen
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob
- [HW_SELFTEST](#job-hw-selftest) - Start hardware selftest
- [HW_SELFTEST_STATUS](#job-hw-selftest-status) - Status of hardware selftest
- [TCU_TYPE_LESEN](#job-tcu-type-lesen) - Read the hardware type ID of the TCU
- [US_ESN_MIN_LESEN](#job-us-esn-min-lesen) - Read ESN, MDN and MIN from the TCU US NAD
- [ECALL_BCALL_BUTTON_TEST](#job-ecall-bcall-button-test) - Test E-Call and B-Call button
- [ECALL_COMPONENT_TEST](#job-ecall-component-test) - Test microphone and antenna
- [BT_ANTENNA_TEST](#job-bt-antenna-test) - bt_antenna_test
- [BT_USER_FRIENDLY_NAME_LESEN](#job-bt-user-friendly-name-lesen) - Read Bluetooth user friendly name
- [BT_USER_FRIENDLY_NAME_SCHREIBEN](#job-bt-user-friendly-name-schreiben) - Write Bluetooth user friendly name
- [BT_PAIRED_DEVICES_LOESCHEN](#job-bt-paired-devices-loeschen) - Delete list with Bluetooth paired devices
- [US_NAM_SELECT](#job-us-nam-select) - Switch between NAM1 and NAM2 (Number Assignment Module) Note: New NAM becomes active after ending Diagnostic Mode
- [US_NAM_STATUS](#job-us-nam-status) - Read active NAM (Number Assignment Module)
- [US_SID_NID_LESEN](#job-us-sid-nid-lesen) - Read US Home System ID and Network ID list
- [US_SID_NID_SCHREIBEN](#job-us-sid-nid-schreiben) - Set US Home System ID and Network ID Requires US_NAD_SCANNING_STOP to be executed before writing
- [RESET_MODE](#job-reset-mode) - Force software reset of the TCU control unit Reset occurs approx. 2 seconds after sending
- [BT_PAIRABLE_MODE](#job-bt-pairable-mode) - Bring Bluetooth server into pairable (and discoverable) mode
- [US_HOME_ONLY_A_B_SIDE](#job-us-home-only-a-b-side) - Read or set home only and A/B side scanning Requires US_NAD_SCANNING_STOP to be executed before writing
- [US_CUSTOMER_CALLS](#job-us-customer-calls) - Read or set customer calls over NAD
- [NAD_INFORMATION](#job-nad-information) - Read information about the current NAD Status
- [US_NAD_SCANNING_START](#job-us-nad-scanning-start) - Start scanning of the US CDMA/AMPS NAD Ignition cycle will also re-start NAD scanning
- [US_NAD_SCANNING_STOP](#job-us-nad-scanning-stop) - Stop scanning of the US CDMA/AMPS NAD Job needs to be sent before writing NAD parameters Stopping NAD scanning takes up to 5 seconds
- [FAHRGESTELLNUMMER_VIN_LESEN](#job-fahrgestellnummer-vin-lesen) - Read 7 digit Vehicle Identification Number from TCU coding data
- [FAHRGESTELLNUMMER_VIN_SCHREIBEN](#job-fahrgestellnummer-vin-schreiben) - Write 7 digit Vehicle Identification Number into TCU coding data
- [NAD_EQUIPPED](#job-nad-equipped) - Read or set NAD equipped
- [US_CDMA_CHANNELS](#job-us-cdma-channels) - Read or set primary/secondary CDMA channel A/B Requires US_NAD_SCANNING_STOP to be executed before writing
- [US_AMPS_PAGING_CHANNEL](#job-us-amps-paging-channel) - Read or set AMPS paging channel Requires US_NAD_SCANNING_STOP to be executed before writing
- [US_AMPS_SID_LESEN](#job-us-amps-sid-lesen) - Read US CM-42 AMPS Home System ID    0 - 16387
- [US_AMPS_SID_SCHREIBEN](#job-us-amps-sid-schreiben) - Set US CM-42 AMPS Home System ID  0 - 16387 Requires US_NAD_SCANNING_STOP to be executed before writing
- [BT_FIX_PASSKEY_LESEN](#job-bt-fix-passkey-lesen) - Read Bluetooth fix passkey
- [BT_FIX_PASSKEY_SCHREIBEN](#job-bt-fix-passkey-schreiben) - Write Bluetooth fix passkey
- [GPS_DATE_TIME](#job-gps-date-time) - Read date and time of the external (NAVI) or internal GPS
- [STATUS_GPS](#job-status-gps) - Status of the internal GPS module
- [STATUS_IO_LESEN](#job-status-io-lesen) - Read I/O port status
- [STATUS_IO_SCHREIBEN](#job-status-io-schreiben) - Set and read I/O port status
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [FG_ALS_BT_USER_FRIENDLY_NAME_SCHREIBEN](#job-fg-als-bt-user-friendly-name-schreiben) - Write "BMW" + last 5 digits of FG as BT User-Friendly name Based on standard Codierjob C_FG_SCHREIBEN
- [BT_OPERATIONMODE_LESEN](#job-bt-operationmode-lesen) - read if BT operation is enabled or disabled
- [BT_DISABLE](#job-bt-disable) - Unset Bluetooth Masterbit
- [BT_ENABLE](#job-bt-enable) - Set Bluetooth Masterbit
- [ECALL_STATUS_LESEN](#job-ecall-status-lesen) - read if E-call is enabled or disabled
- [ECALL_DISABLE](#job-ecall-disable) - Unset E-Call Masterbit
- [ECALL_ENABLE](#job-ecall-enable) - Set E-Call Masterbit
- [BT_PAIRED_DEVICES_LESEN](#job-bt-paired-devices-lesen) - Read Bluetooth paired devices
- [US_CALL_SERVICE_CENTER_NUMBER_LESEN](#job-us-call-service-center-number-lesen) - Read phone number of call service center
- [US_CALL_SERVICE_CENTER_NUMBER_SCHREIBEN](#job-us-call-service-center-number-schreiben) - Set phone number of call service center
- [US_MIN_LESEN](#job-us-min-lesen) - Read MIN (Mobile Identification Number)
- [US_MIN_SCHREIBEN](#job-us-min-schreiben) - Set MIN (Mobile Identification Number) Requires US_NAD_SCANNING_STOP to be executed before writing
- [US_MDN_LESEN](#job-us-mdn-lesen) - Read MDN (CDMA Mobile Directory Number)
- [US_MDN_SCHREIBEN](#job-us-mdn-schreiben) - Set MDN (CDMA Mobile Directory Number) Requires US_NAD_SCANNING_STOP to be executed before writing
- [IMEI_LESEN](#job-imei-lesen) - Read IMEI
- [ICC_ID_LESEN](#job-icc-id-lesen) - Read ICC ID

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter DS2

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

<a id="job-ident"></a>
### IDENT

Identdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen immer 0 |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string | table FArtTexte ARTTEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort table IOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen immer 0 |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string | table IArtTexte ARTTEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Steuergeraete Reset ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRODUKTIONSMODE | string | "ein" -&gt; Produktions Mode ein "aus" -&gt; Produktions Mode aus table DigitalArgument TEXT Default: "aus" |
| TRANSPORTMODE | string | "ein" -&gt; Transport Mode ein "aus" -&gt; Transport Mode aus table DigitalArgument TEXT Default: "aus" |
| WERKSTATTMODE | string | "ein" -&gt; Werkstatt Mode ein "aus" -&gt; Werkstatt Mode aus table DigitalArgument TEXT Default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x9B) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x9D) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
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

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen Standard Codierjob

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | die letzten vier Stellen der Fahrgestellnummer |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Fahrgestellnummer schreiben und ruecklesen Standard Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-hw-selftest"></a>
### HW_SELFTEST

Start hardware selftest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hw-selftest-status"></a>
### HW_SELFTEST_STATUS

Status of hardware selftest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| RESULT_BYTE1 | char |  |
| RESULT_BYTE2 | char |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-tcu-type-lesen"></a>
### TCU_TYPE_LESEN

Read the hardware type ID of the TCU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurred |
| TCU_TYPE | int | TCU Type |
| TCU_TYPE_TEXT | string | TCU Type |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-esn-min-lesen"></a>
### US_ESN_MIN_LESEN

Read ESN, MDN and MIN from the TCU US NAD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| US_ESN | string | NAD Electronic Serial Number |
| US_MDN | string | NAD Mobile Directory Number |
| US_MIN | string | NAD Mobile Identification Number |
| _ESN_ANTWORT | binary | Hex-Antwort von SG |
| _MDN_ANTWORT | binary | Hex-Antwort von SG |
| _MIN_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecall-bcall-button-test"></a>
### ECALL_BCALL_BUTTON_TEST

Test E-Call and B-Call button

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| TEST_STATUS | int | 0x00 fail (DTCS logged) 0x01 pass (No DTCS logged) |
| RESULT | string | status |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecall-component-test"></a>
### ECALL_COMPONENT_TEST

Test microphone and antenna

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| TEST_STATUS | int | 0x00 fail (DTCS logged) 0x01 pass (No DTCS logged) |
| RESULT | string | status |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-antenna-test"></a>
### BT_ANTENNA_TEST

bt_antenna_test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurred |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| BT_ANTENNA_FLAG | int | Bluetooth Antenna Flag 0x00: Passed 0x01: Failed |
| BT_ANTENNA_FLAG_TEXT | string | Bluetooth Antenna Flag als Textausgabe |

<a id="job-bt-user-friendly-name-lesen"></a>
### BT_USER_FRIENDLY_NAME_LESEN

Read Bluetooth user friendly name

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| BT_USER_FRIENDLY_NAME | string | Bluetooth user friendly name |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-user-friendly-name-schreiben"></a>
### BT_USER_FRIENDLY_NAME_SCHREIBEN

Write Bluetooth user friendly name

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BT_USER_FRIENDLY_NAME | string | Bluetooth user friendly name |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-paired-devices-loeschen"></a>
### BT_PAIRED_DEVICES_LOESCHEN

Delete list with Bluetooth paired devices

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-nam-select"></a>
### US_NAM_SELECT

Switch between NAM1 and NAM2 (Number Assignment Module) Note: New NAM becomes active after ending Diagnostic Mode

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAM | int | 0x01 = NAM1 0x02 = NAM2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-nam-status"></a>
### US_NAM_STATUS

Read active NAM (Number Assignment Module)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| NAM | int | 0x01 = NAM1 0x02 = NAM2 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-sid-nid-lesen"></a>
### US_SID_NID_LESEN

Read US Home System ID and Network ID list

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| CM42_SID_NID_LIST | string | &lt;index&gt;:&lt;sid&gt;:&lt;nid&gt; ........ &lt;index&gt;:&lt;sid&gt;:&lt;nid&gt; in ASCII |
| SID | string | System ID |
| NID | string | Network ID |
| INDEX | string | Index |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-sid-nid-schreiben"></a>
### US_SID_NID_SCHREIBEN

Set US Home System ID and Network ID Requires US_NAD_SCANNING_STOP to be executed before writing

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INDEX | string | Range 0-256 |
| SID | string | Range 0-32176 |
| NID | string | Range 0-65535 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-reset-mode"></a>
### RESET_MODE

Force software reset of the TCU control unit Reset occurs approx. 2 seconds after sending

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-pairable-mode"></a>
### BT_PAIRABLE_MODE

Bring Bluetooth server into pairable (and discoverable) mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-home-only-a-b-side"></a>
### US_HOME_ONLY_A_B_SIDE

Read or set home only and A/B side scanning Requires US_NAD_SCANNING_STOP to be executed before writing

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT | char | Empty to read current status, or 0x00 for Normal 0x01 for Home only 0x02 for A side scanning 0x03 for B side scanning |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| STATUS | char | Status of home only or A/B side scanning (-&gt; INPUT parameter) |
| STATUS_TEXT | string | Status als Textausgabe |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-customer-calls"></a>
### US_CUSTOMER_CALLS

Read or set customer calls over NAD

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT | char | Empty to read current status, or 0x00 to disable 0x01 to enable |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| STATUS | char | Status of customer calls over NAD (-&gt; INPUT parameter) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-nad-information"></a>
### NAD_INFORMATION

Read information about the current NAD Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| NAD_REGISTERSTATE | unsigned char | NAD Register State 0x00 = not registered 0x01 = registered on GSM/CDMA/AMPS network |
| NAD_REGISTERSTATE_TEXT | string | NAD Register State als Textausgabe |
| NAD_SIGNALSTRENGTH | unsigned char | NAD Signal Strength 0    = -113 dBm or less 1-30 = -111 to -53 dBm, 2 dBm steps 31   = -51 dBm or greater 99   = unknown or not detectable |
| NAD_SIGNALSTRENGTH_DBM | char | NAD Signal Strength in dBm -113..-51 dBm 99 = unknown or not detectable |
| NAD_SIGNALBARS | unsigned char | NAD Signal in bars 0x00-0x05 = 0-5 bars 0xFF = unknown or not detectable |
| NAD_ROAMING | char | NAD Roaming Status 0x00 = not roaming 0x01 = Roaming on network 0x02 = Roaming off network 0xFF = unknown or not detectable |
| NAD_ROAMING_TEXT | string | NAD Roaming Status als Textausgabe |
| SID | string | System ID SID on which NAD is registered |
| NID | string | Network ID NID on which NAD is registered |
| MCC | string | Mobile Country Code MCC on which NAD is registered |
| MNC | string | Mobile Network Code MNC on which NAD is registered |
| PRL | string | Preferred Roaming List PRL |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-nad-scanning-start"></a>
### US_NAD_SCANNING_START

Start scanning of the US CDMA/AMPS NAD Ignition cycle will also re-start NAD scanning

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| RESULT | char | Result 0x00 Success, 0x01 Error |
| RESULT_TEXT | string | Result als Textausgabe |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-nad-scanning-stop"></a>
### US_NAD_SCANNING_STOP

Stop scanning of the US CDMA/AMPS NAD Job needs to be sent before writing NAD parameters Stopping NAD scanning takes up to 5 seconds

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| RESULT | char | Result 0x00 Success, 0x01 Error |
| RESULT_TEXT | string | Result als Textausgabe |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fahrgestellnummer-vin-lesen"></a>
### FAHRGESTELLNUMMER_VIN_LESEN

Read 7 digit Vehicle Identification Number from TCU coding data

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| VIN | binary | Vehicle Identification Number |
| VIN_TEXT | string | Vehicle Identification Number |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fahrgestellnummer-vin-schreiben"></a>
### FAHRGESTELLNUMMER_VIN_SCHREIBEN

Write 7 digit Vehicle Identification Number into TCU coding data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VIN | string | Vehicle Identification Number |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-nad-equipped"></a>
### NAD_EQUIPPED

Read or set NAD equipped

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT | char | Empty to read current status, or 0x00 = NAD not equipped 0x01 = NAD equipped |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| STATUS | char | Status of NAD equipped (see INPUT parameter) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-cdma-channels"></a>
### US_CDMA_CHANNELS

Read or set primary/secondary CDMA channel A/B Requires US_NAD_SCANNING_STOP to be executed before writing

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRIMARY_SECONDARY | char | Priority: 1 = primary, 2 = secondary |
| A_B | string | Channel: A, B |
| VALUE | string | Empty to request current value, or value to be programmed for CDMA channel Channel A: 1-311, 689-694, 1013-1023 Channel B: 356-644, 739-777 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| CHANNEL | string | Value of requested CDMA channel |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-amps-paging-channel"></a>
### US_AMPS_PAGING_CHANNEL

Read or set AMPS paging channel Requires US_NAD_SCANNING_STOP to be executed before writing

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | string | Empty to request current value, or value to be programmed for AMPS paging channel Channel: 1-799, 990-1023 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| CHANNEL | string | Value of AMPS paging channel |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-amps-sid-lesen"></a>
### US_AMPS_SID_LESEN

Read US CM-42 AMPS Home System ID    0 - 16387

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CM42_AMPS_SID | string | 1 - 5-byte AMPS Home SID (0 - 16387 -&gt; 0x30 - 0x31 0x36 0x33 0x38 0x37) |

<a id="job-us-amps-sid-schreiben"></a>
### US_AMPS_SID_SCHREIBEN

Set US CM-42 AMPS Home System ID  0 - 16387 Requires US_NAD_SCANNING_STOP to be executed before writing

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AMPS_SID | string | 1.byte of AMPS Home SID (0 - 16387 -&gt; 0x30 - 0x31 0x36 0x33 0x38 0x37) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-bt-fix-passkey-lesen"></a>
### BT_FIX_PASSKEY_LESEN

Read Bluetooth fix passkey

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| BT_FIX_PASSKEY | string | 1 - 16 byte Bluetooth Fix Passkey |

<a id="job-bt-fix-passkey-schreiben"></a>
### BT_FIX_PASSKEY_SCHREIBEN

Write Bluetooth fix passkey

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BT_FIX_PASSKEY | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-gps-date-time"></a>
### GPS_DATE_TIME

Read date and time of the external (NAVI) or internal GPS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| GPS_DATE | string | Current GPS date (dd.mm.yyyy) |
| GPS_TIME | string | Current GPS time (hh:mm:ss) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gps"></a>
### STATUS_GPS

Status of the internal GPS module

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| STAT_GPS | char | GPS status 0x00 = Not supported: No GPS 0x01 = Not supported: Communication error 0x02 = Receiver error 0x03 = No almanac 0x04 = Searching satellites 0x05 = Tracking 1 satellite 0x06 = Tracking 2 satellites 0x07 = Tracking 3 satellites 0x08 = Tracking 4 satellites 0x09 = Tracking 5 satellites 0x0A = Tracking 6 satellites 0x0B = 2D positioning 0x0C = 3D positioning |
| STAT_GPS_TEXT | string | GPS status als Textausgabe |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Read I/O port status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| STAT_E_CALL_EIN | int | e-call line from button 1=open, 0=closed (button pressed) |
| STAT_B_CALL_EIN | int | b-call line from button 1=open, 0=closed (button pressed) |
| STAT_BLUETOOTH_EIN | int | status of bluetooth 1=enable, 0=disable |

<a id="job-status-io-schreiben"></a>
### STATUS_IO_SCHREIBEN

Set and read I/O port status

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 1.byte with portdata |
| BYTE2 | int | 2.byte with portdata |
| BYTE3 | int | 3.byte with portdata |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| STAT_SOS_LED_EIN | int | 1=active, 0=not active |
| STAT_MUTE_EIN | int | 1=active, 0=not active |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-fg-als-bt-user-friendly-name-schreiben"></a>
### FG_ALS_BT_USER_FRIENDLY_NAME_SCHREIBEN

Write "BMW" + last 5 digits of FG as BT User-Friendly name Based on standard Codierjob C_FG_SCHREIBEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (17 oder 18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-bt-operationmode-lesen"></a>
### BT_OPERATIONMODE_LESEN

read if BT operation is enabled or disabled

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BLUETOOTH_FLAG | int | 1-byte BT flag: 0x00 - disabled, 0x01 - enabled |

<a id="job-bt-disable"></a>
### BT_DISABLE

Unset Bluetooth Masterbit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-enable"></a>
### BT_ENABLE

Set Bluetooth Masterbit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecall-status-lesen"></a>
### ECALL_STATUS_LESEN

read if E-call is enabled or disabled

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| E_CALL_FLAG | int | 1-byte E-call flag: 0x00 - disabled, 0x01 - enabled |

<a id="job-ecall-disable"></a>
### ECALL_DISABLE

Unset E-Call Masterbit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecall-enable"></a>
### ECALL_ENABLE

Set E-Call Masterbit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-paired-devices-lesen"></a>
### BT_PAIRED_DEVICES_LESEN

Read Bluetooth paired devices

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| NUM_PAIRED_DEVICES | int | Number of Bluetooth paired devices |
| BT_PAIRED_DEVICES_LIST | binary | Bluetooth 6-byte paired devices addresses |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-call-service-center-number-lesen"></a>
### US_CALL_SERVICE_CENTER_NUMBER_LESEN

Read phone number of call service center

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| US_CALL_SERVICE_CENTER_NUMBER | string | Service center number |

<a id="job-us-call-service-center-number-schreiben"></a>
### US_CALL_SERVICE_CENTER_NUMBER_SCHREIBEN

Set phone number of call service center

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERV_CENT_NO | string | Service center number |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |

<a id="job-us-min-lesen"></a>
### US_MIN_LESEN

Read MIN (Mobile Identification Number)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| US_MIN | string | Mobile Identification Number |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-min-schreiben"></a>
### US_MIN_SCHREIBEN

Set MIN (Mobile Identification Number) Requires US_NAD_SCANNING_STOP to be executed before writing

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| US_MIN | string | Value to be programmed for MIN (10 digits) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-mdn-lesen"></a>
### US_MDN_LESEN

Read MDN (CDMA Mobile Directory Number)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| US_MDN | string | CDMA Mobile Directory Number |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-mdn-schreiben"></a>
### US_MDN_SCHREIBEN

Set MDN (CDMA Mobile Directory Number) Requires US_NAD_SCANNING_STOP to be executed before writing

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| US_MDN | string | Value to be programmed for MDN (15 digits) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if no error occurs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-imei-lesen"></a>
### IMEI_LESEN

Read IMEI

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| IMEI | string | 15 byte |

<a id="job-icc-id-lesen"></a>
### ICC_ID_LESEN

Read ICC ID

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ICC_ID | string | 10 byte |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (86 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (3 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (23 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (11 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IARTTEXTE](#table-iarttexte) (3 × 2)
- [BLUETOOTHANTENNASTATUSTEXTE](#table-bluetoothantennastatustexte) (3 × 2)
- [GPSSTATUSTEXTE](#table-gpsstatustexte) (14 × 2)
- [NADSTATUSTEXTE](#table-nadstatustexte) (3 × 2)
- [PAIRINGRESULTTEXTE](#table-pairingresulttexte) (4 × 2)
- [TCUTYPETEXTE](#table-tcutypetexte) (4 × 2)
- [VOICERECLANGTEXTE](#table-voicereclangtexte) (8 × 2)
- [VOICERECPROGSTATUSTEXTE](#table-voicerecprogstatustexte) (4 × 2)
- [ROAMINGSTATUSTEXTE](#table-roamingstatustexte) (4 × 2)
- [PRLSTATUSTEXTE](#table-prlstatustexte) (10 × 2)
- [RESULTTEXTE](#table-resulttexte) (3 × 2)
- [HOMEONLYABSIDETEXTE](#table-homeonlyabsidetexte) (5 × 2)

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

Dimensions: 86 rows × 2 columns

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
| 0x72 | ASIN AWCO.LTD |
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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 3 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 23 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x069 | GPS antenna not connected |
| 0x06A | GPS hardware failure |
| 0x06B | GPS communication error |
| 0x06C | NAD fatal error |
| 0x06D | E-call switch not connected |
| 0x06E | E-call LED not connected |
| 0x070 | E-call switch shorted to 12V |
| 0x073 | NVM device error |
| 0x074 | E-call switch stuck or shorted to ground |
| 0x079 | Bluetooth interface error |
| 0x07A | Control unit in MTS mode |
| 0x07F | B-call switch shorted to 12V |
| 0x080 | B-call switch not connected |
| 0x081 | B-call switch stuck or shorted to ground |
| 0x091 | Main antenna or compensator/combiner disconnected or shortcut |
| 0x097 | Bluetooth cradle button stuck |
| 0x098 | Microphone disconnected |
| 0x068 | GPS antenna shortcut |
| 0x0A0 | Prefit SIM not physically present |
| 0x0A1 | Prefit SIM cannot be read |
| 0x0A2 | Prefit SIM PUK-locked; PIN input failed |
| 0x0A3 | Bluetooth antenna not connected |
| 0xXY | Undefined |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 11 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x008 | Reset after software watchdog timeout |
| 0x011 | I-Bus access error |
| 0x012 | Low RF field detected |
| 0x013 | NVM corrupted |
| 0x014 | Coding data error |
| 0x015 | NAD transceiver failure |
| 0x01A | Prefit SIM not physically present |
| 0x01B | Prefit SIM cannot be read |
| 0x01C | Prefit SIM PUK-locked; PIN input failed |
| 0x01D | Prefit SIM denied in the network |
| 0xXY | Undefined |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Currently not available |
| 0x01 | Currently available |
| 0xXY | Undefined |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Currently not available |
| 0x01 | Currently available |
| 0xXY | Undefined |

<a id="table-bluetoothantennastatustexte"></a>
### BLUETOOTHANTENNASTATUSTEXTE

Dimensions: 3 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Passed |
| 0x01 | Failed |
| 0xXY | Undefined |

<a id="table-gpsstatustexte"></a>
### GPSSTATUSTEXTE

Dimensions: 14 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | No GPS |
| 0x01 | Communication error |
| 0x02 | Receiver error |
| 0x03 | No almanac |
| 0x04 | Searching satellites... |
| 0x05 | Tracking 1 satellite |
| 0x06 | Tracking 2 satellites |
| 0x07 | Tracking 3 satellites |
| 0x08 | Tracking 4 satellites |
| 0x09 | Trackiing 5 satellites |
| 0x0A | Tracking 6 satellites |
| 0x0B | 2D positioning |
| 0x0C | 3D positioning |
| 0xXY | Undefined |

<a id="table-nadstatustexte"></a>
### NADSTATUSTEXTE

Dimensions: 3 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Not registered |
| 0x01 | Registered |
| 0xXY | Undefined |

<a id="table-pairingresulttexte"></a>
### PAIRINGRESULTTEXTE

Dimensions: 4 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Success |
| 0x01 | Failure |
| 0x02 | Waiting |
| 0xXY | Undefined |

<a id="table-tcutypetexte"></a>
### TCUTYPETEXTE

Dimensions: 4 rows × 2 columns

| TCU_TYPE | TCU_TYPE_TEXT |
| --- | --- |
| 0x03 | TCU 1.5 Malapert I-Bus ECE |
| 0x04 | TCU 1.5 Malapert I-Bus US |
| 0x05 | TCU 1.5 Malapert I-Bus ECE Superthin |
| 0xXY | Undefined |

<a id="table-voicereclangtexte"></a>
### VOICERECLANGTEXTE

Dimensions: 8 rows × 2 columns

| WERT | LANGUAGE_TEXT |
| --- | --- |
| 0x00 | German |
| 0x01 | US English |
| 0x02 | UK English |
| 0x03 | Italien |
| 0x04 | French |
| 0x05 | Spanish |
| 0xFF | No language, flash programming failed |
| 0xXY | Undefined |

<a id="table-voicerecprogstatustexte"></a>
### VOICERECPROGSTATUSTEXTE

Dimensions: 4 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Flash programming successful |
| 0x01 | Flash programming ongoing |
| 0x02 | Flash programming failed |
| 0xXY | Undefined |

<a id="table-roamingstatustexte"></a>
### ROAMINGSTATUSTEXTE

Dimensions: 4 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Not roaming |
| 0x01 | Roaming on network |
| 0x02 | Roaming off network |
| 0xXY | Unknown or not detectable |

<a id="table-prlstatustexte"></a>
### PRLSTATUSTEXTE

Dimensions: 10 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | PRL stored |
| 0x01 | PRL loading... |
| 0x02 | PRL packet size error |
| 0x03 | PRL sequence error |
| 0x04 | PRL invalid |
| 0x05 | PRL size error |
| 0x06 | PRL memory error |
| 0x07 | PRL not loaded |
| 0x08 | PRL disabled |
| 0xXY | Undefined |

<a id="table-resulttexte"></a>
### RESULTTEXTE

Dimensions: 3 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Success |
| 0x01 | Error |
| 0xXY | Undefined |

<a id="table-homeonlyabsidetexte"></a>
### HOMEONLYABSIDETEXTE

Dimensions: 5 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Normal |
| 0x01 | Home only enabled |
| 0x02 | Side A scanning |
| 0x03 | Side B scanning |
| 0xXY | Undefined |
