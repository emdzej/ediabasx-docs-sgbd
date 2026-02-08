# TELIBUS.prg

- Jobs: [87](#jobs)
- Tables: [13](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | TELIBUS |
| ORIGIN | BMW TI-431 Weber |
| REVISION | 3.002 |
| AUTHOR | Motorola Spengler, Manns, BMW EE-43 Villiers, Doyen, Snijders, BMW TI-431 Weber |
| COMMENT | basiert auf SGBD fuer BIT II (BMW TI-433 Krueger) |
| PACKAGE | 0.12 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob
- [IDENT_SCHREIBEN](#job-ident-schreiben) - Identdaten schreiben
- [IO_PORTS_SCHREIBEN_UND_TESTEN](#job-io-ports-schreiben-und-testen) - Set/test verschiedener I/O Ports
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status von IO-Ports lesen
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Durchfuehrung des spez. Selbsttests
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [RESET_MODE](#job-reset-mode) - Durchfuehrung eines resets ca. 2 Sek. nach senden von ACK erfolgt der Reset
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben ohne Verifikation
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [TCU_TYPE_LESEN](#job-tcu-type-lesen) - Lesen der 1-byte TCU ID
- [FAHRGESTELLNUMMER_VIN_LESEN](#job-fahrgestellnummer-vin-lesen) - Lesen der 7-byte Fahrgestellnummer aus den Codierdaten
- [ECALL_BCALL_BUTTON_TEST](#job-ecall-bcall-button-test) - Test Ecall, Bcall buttons
- [STATUS_GPS](#job-status-gps) - Status des GPS wird ausgegeben KWP2000: $21 ReadDataByLocalIdentifier $02 recordLocalIdentifier Modus  : Default
- [STATUS_SIM_READER_LESEN](#job-status-sim-reader-lesen) - Read status of TCU built-in and attached SIM card readers
- [BT_PAIRING_START](#job-bt-pairing-start) - Initiate Bluetooth Pairing
- [BT_PAIRING_RESULT_LESEN](#job-bt-pairing-result-lesen) - Lesen von Bluetooth Pairing Ergebnis
- [BT_FIX_PASSKEY_SCHREIBEN](#job-bt-fix-passkey-schreiben) - Write Bluetooth fix passkey
- [BT_FIX_PASSKEY_LESEN](#job-bt-fix-passkey-lesen) - Read Bluetooth fix passkey
- [BT_DEVICE_ADDRESS_LESEN](#job-bt-device-address-lesen) - Read Bluetooth address
- [BT_USER_FRIENDLY_NAME_SCHREIBEN](#job-bt-user-friendly-name-schreiben) - Set Bluetooth user-friendly name
- [BT_USER_FRIENDLY_NAME_LESEN](#job-bt-user-friendly-name-lesen) - Read Bluetooth user-friendly name
- [FG_ALS_BT_USER_FRIENDLY_NAME_SCHREIBEN](#job-fg-als-bt-user-friendly-name-schreiben) - Write "BMW" + last 5 digits of FG as BT User-Friendly name Based on standard Codierjob C_FG_SCHREIBEN
- [BT_PAIRED_DEVICES_LESEN](#job-bt-paired-devices-lesen) - Read Bluetooth paired devices
- [BT_PAIRED_DEVICES_LIST_LESEN](#job-bt-paired-devices-list-lesen) - Lesen von Liste mit Bluetooth Paired Devices
- [BT_PAIRED_DEVICES_LIST_LOESCHEN](#job-bt-paired-devices-list-loeschen) - Delete list with Bluetooth paired devices
- [BT_PAIRED_DEVICES_LOESCHEN](#job-bt-paired-devices-loeschen) - Delete list with Bluetooth paired devices
- [BT_DISCOVERABLE_MODE](#job-bt-discoverable-mode) - Bring Bluetooth Server into discoverable mode
- [BT_ENABLE](#job-bt-enable) - Enable Bluetooth operation
- [BT_DISABLE](#job-bt-disable) - Disable Bluetooth operation
- [BT_OPERATIONMODE_LESEN](#job-bt-operationmode-lesen) - read if BT operation is enabled or disabled
- [DSP_ACOUSTIC_PROFILE_LESEN](#job-dsp-acoustic-profile-lesen) - GAL: read DSP acoustic profile (1-16)
- [GAL_KMH_PER_STAGE_SCHREIBEN](#job-gal-kmh-per-stage-schreiben) - GAL: set km/h per amplification stage (10 - 60)
- [GAL_KMH_PER_STAGE_LESEN](#job-gal-kmh-per-stage-lesen) - GAL: read km/h per amplification stage (10 - 60)
- [ECALL_ENABLE](#job-ecall-enable) - Enable ecall
- [ECALL_DISABLE](#job-ecall-disable) - Disable E-call
- [ECALL_STATUS_LESEN](#job-ecall-status-lesen) - read if E-call is enabled or disabled
- [TELEMATICS_STATUS_LESEN](#job-telematics-status-lesen) - read if telematics operation is enabled or disabled
- [NON_TELEMATICS_E_CALL_STATUS_LESEN](#job-non-telematics-e-call-status-lesen) - read if non-telematic E-call (call 911/112) is enabled or disabled
- [US_CUST_CALLS_ENABLE](#job-us-cust-calls-enable) - Enable customer calls over NAD with GMIN
- [US_CUST_CALLS_DISABLE](#job-us-cust-calls-disable) - Disable customer calls over NAD with GMIN
- [US_CUST_CALLS_LESEN](#job-us-cust-calls-lesen) - Read if customer calls over NAD using telematic GMIN are enabled or disabled
- [BACKUP_EMERGENCY_NO_SCHREIBEN](#job-backup-emergency-no-schreiben) - Set emergency number (e.g. 112/911) for non-telematic E-calls
- [BACKUP_EMERGENCY_NO_LESEN](#job-backup-emergency-no-lesen) - Read backup emergency number used for non-telematic E-calls (e.g.112/911)
- [US_CALL_SERVICE_CENTER_STATUS_LESEN](#job-us-call-service-center-status-lesen) - read if call service center (e.g. Verizon)is enabled or disabled
- [US_CALL_SERVICE_CENTER_NUMBER_SCHREIBEN](#job-us-call-service-center-number-schreiben) - Set phone number of call service number (Verizon)
- [US_CALL_SERVICE_CENTER_NUMBER_LESEN](#job-us-call-service-center-number-lesen) - Read phone number of call service center (Verizon)
- [US_MIN_SCHREIBEN](#job-us-min-schreiben) - Set MIN in Ericsson CM-42 NAD for US telenatics
- [FG_SCHREIBEN_AS_US_MIN](#job-fg-schreiben-as-us-min) - Write last 5 digits of FG in GMIN Based on standard Codierjob C_FG_SCHREIBEN
- [US_CDMA_DIRECTORY_SCHREIBEN](#job-us-cdma-directory-schreiben) - Set US CM-42 CDMA Directory 00000 00000 - 99999 99999
- [US_CDMA_DIRECTORY_LESEN](#job-us-cdma-directory-lesen) - CDMA Directory 00000 00000 00000 - 99999 99999 99999 -&gt; 0x31..0x31 - 0x39..0x39
- [US_SID_NID_SCHREIBEN](#job-us-sid-nid-schreiben) - Set US CM-42 System ID and Network ID
- [US_SID_NID_LESEN](#job-us-sid-nid-lesen) - Read US CM-42 Home SID/NID list
- [US_CDMA_PRIMARY_CH_A_SCHREIBEN](#job-us-cdma-primary-ch-a-schreiben) - Set US CM-42 CDMA Primary Channel A
- [US_CDMA_PRIMARY_CH_A_LESEN](#job-us-cdma-primary-ch-a-lesen) - Read US CM-42 CDMA Primary Channel (1-311, 689-694, 1013-1023 as ASCII bytes)
- [US_CDMA_SECONDARY_CH_A_SCHREIBEN](#job-us-cdma-secondary-ch-a-schreiben) - Set US CM-42 CDMA Secondary Channel A
- [US_CDMA_SECONDARY_CH_A_LESEN](#job-us-cdma-secondary-ch-a-lesen) - Read US CM-42 CDMA Secondary Channel A  (1-311, 689-694, 1013-1023 as ASCII bytes)
- [US_CDMA_PRIMARY_CH_B_SCHREIBEN](#job-us-cdma-primary-ch-b-schreiben) - Set US CM-42 CDMA Primary Channel B
- [US_CDMA_PRIMARY_CH_B_LESEN](#job-us-cdma-primary-ch-b-lesen) - Read US CM-42 CDMA Primary Channel B  (365-644, 739-777 as ASCII bytes)
- [US_CDMA_SECONDARY_CH_B_SCHREIBEN](#job-us-cdma-secondary-ch-b-schreiben) - Set US CM-42 CDMA Secondary Channel B
- [US_CDMA_SECONDARY_CH_B_LESEN](#job-us-cdma-secondary-ch-b-lesen) - Read US CM-42 CDMA Secondary Channel B (365-644, 739-777 as ASCII bytes)
- [US_HOME_ONLY_ENABLE](#job-us-home-only-enable) - Enable Home Only
- [US_HOME_ONLY_DISABLE](#job-us-home-only-disable) - Disable Home Only
- [US_HOME_ONLY_LESEN](#job-us-home-only-lesen) - read status of home only
- [US_A_B_SIDE_SCHREIBEN](#job-us-a-b-side-schreiben) - Set Home Only Status (0-3)
- [ENERGIESPARMODE](#job-energiesparmode) - MTS/FETRAWE Mode (00 Exit) (01 Manufacturing) (02 Service) (03 Production)
- [US_ESN_MIN_LESEN](#job-us-esn-min-lesen) - Read MIN in Ericsson CM-42 NAD for US telematics
- [IMEI_LESEN](#job-imei-lesen) - Read IMEI
- [US_K633_ENABLE](#job-us-k633-enable) - Enable Bluetooth portable support for US (K633)
- [US_K633_LESEN](#job-us-k633-lesen) - Read status of US Bluetooth portable support (K633)
- [US_K633_DISABLE](#job-us-k633-disable) - Disable Bluetooth portable support for US (K633)
- [NAD_EQUIPPED_ENABLE](#job-nad-equipped-enable) - Enable NAD equipped coding parameter
- [NAD_EQUIPPED_LESEN](#job-nad-equipped-lesen) - Read status of the NAD equipped coding parameter
- [NAD_EQUIPPED_DISABLE](#job-nad-equipped-disable) - Disable NAD equipped coding parameter
- [HW_SELBTEST_STATUS_LESEN](#job-hw-selbtest-status-lesen) - Read results of the HW selftest

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

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-c-fg-schreiben"></a>
### C_FG_SCHREIBEN

Fahrgestellnummer schreiben Standard Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-ident-schreiben"></a>
### IDENT_SCHREIBEN

Identdaten schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ID_BMW_NR | string | BMW-Teilenummer  e.g. 06924544 |
| ID_HW_NR | string | BMW-Hardwarenummer 00-99 |
| ID_COD_INDEX | string | Codier-Index von CBD 00-99 e.g. 01 |
| ID_DIAG_INDEX | string | Diagnose-Index - always 20 |
| ID_BUS_INDEX | string | Bus-Index 00 - 99, 01 |
| ID_DATUM_KW | string | Herstelldatum KW 01 - 52 |
| ID_DATUM_JAHR | string | Herstelldatum Jahr  00 - 99 |
| ID_LIEF_NR | string | Lieferanten-Nummer Motorola 23 |
| ID_SW_NR | string | Softwarenummer 00 - 99 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-io-ports-schreiben-und-testen"></a>
### IO_PORTS_SCHREIBEN_UND_TESTEN

Set/test verschiedener I/O Ports

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 1.byte with portdata |
| BYTE2 | int | 2.byte with portdata |
| BYTE3 | int | 3.byte with portdata |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_SOS_LED_EIN | int | 1=active, 0=not active |
| STAT_MUTE_EIN | int | 1=active, 0=not active |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Status von IO-Ports lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_E_CALL_EIN | int | e-call line from button 1=open, 0=closed(button pressed) |
| STAT_B_CALL_EIN | int | b-call line from button 1=open, 0=closed(button pressed) |
| STAT_BLUETOOTH_EIN | int | status of bluetooth 1=enable, 0=disable |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Durchfuehrung des spez. Selbsttests

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

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

<a id="job-reset-mode"></a>
### RESET_MODE

Durchfuehrung eines resets ca. 2 Sek. nach senden von ACK erfolgt der Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-c-c-schreiben"></a>
### C_C_SCHREIBEN

Codierdaten schreiben ohne Verifikation

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

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

<a id="job-tcu-type-lesen"></a>
### TCU_TYPE_LESEN

Lesen der 1-byte TCU ID

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TCU_ID | int | 1-byte TCU ID, 0x05 - I-bus ECE, 0x06 - I-bus US |
| TCU_TYPE | int | OKAY, wenn fehlerfrei |
| TCU_TYPE_TEXT | string | Text, welche Variante verbaut ist |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-fahrgestellnummer-vin-lesen"></a>
### FAHRGESTELLNUMMER_VIN_LESEN

Lesen der 7-byte Fahrgestellnummer aus den Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VIN | binary | 7 byte Vehicle Identification Number in I-bus TCU |
| VIN_TEXT | string | 7 byte Vehicle Identification Number in I-bus TCU |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-ecall-bcall-button-test"></a>
### ECALL_BCALL_BUTTON_TEST

Test Ecall, Bcall buttons

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| TEST_STATUS | int | 1-byte 0x00 fail (DTCS logged) 0x01 pass (No DTCS logged) |
| RESULT | string | status |

<a id="job-status-gps"></a>
### STATUS_GPS

Status des GPS wird ausgegeben KWP2000: $21 ReadDataByLocalIdentifier $02 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GPS | int | GPS-Status 0x00 = Not supported: No GPS 0x01 = Not supported: Communication error 0x02 = Receiver error 0x03 = No almanac 0x04 = Searching satellites 0x05 = Tracking 1 satellite 0x06 = Tracking 2 satellites 0x07 = Tracking 3 satellites 0x08 = Tracking 4 satellites 0x09 = Tracking 5 satellites 0x0A = Tracking 6 satellites 0x0B = 2D positioning 0x0C = 3D positioning |
| STAT_GPS_TEXT | string | GPS-Status als Textausgabe |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sim-reader-lesen"></a>
### STATUS_SIM_READER_LESEN

Read status of TCU built-in and attached SIM card readers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_TELEM_READER | int | 1 = telematic SIM card reader accessible |
| STAT_EXT_READER | int | 1 = external SIM card reader accessible |

<a id="job-bt-pairing-start"></a>
### BT_PAIRING_START

Initiate Bluetooth Pairing

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-bt-pairing-result-lesen"></a>
### BT_PAIRING_RESULT_LESEN

Lesen von Bluetooth Pairing Ergebnis

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| PAIRING_RESULT | int | table PairingResult SB |
| PAIRING_STATUS | string | OKAY, wenn fehlerfrei table PairingResult STATUS_TEXT |

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

<a id="job-bt-fix-passkey-lesen"></a>
### BT_FIX_PASSKEY_LESEN

Read Bluetooth fix passkey

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| BT_FIX_PASSKEY | string | 1 - 16 byte Bluetooth Fix Passkey |

<a id="job-bt-device-address-lesen"></a>
### BT_DEVICE_ADDRESS_LESEN

Read Bluetooth address

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| BT_ADDRESS | binary | 6 byte Bluetooth Adresse von TCU |

<a id="job-bt-user-friendly-name-schreiben"></a>
### BT_USER_FRIENDLY_NAME_SCHREIBEN

Set Bluetooth user-friendly name

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BT_USER_FRIENDLY_NAME | string | Bluetooth user-friendly name (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-bt-user-friendly-name-lesen"></a>
### BT_USER_FRIENDLY_NAME_LESEN

Read Bluetooth user-friendly name

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BT_USER_FRIENDLY_NAME | string | 1 - 18 byte Bluetooth User-Friendly Name |

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

<a id="job-bt-paired-devices-lesen"></a>
### BT_PAIRED_DEVICES_LESEN

Read Bluetooth paired devices

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| NUM_PAIRED_DEVICES | int | OKAY, wenn fehlerfrei |

<a id="job-bt-paired-devices-list-lesen"></a>
### BT_PAIRED_DEVICES_LIST_LESEN

Lesen von Liste mit Bluetooth Paired Devices

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BT_PAIRED_DEVICES_LIST | binary | 1-5 Blutetooth 6-byte paired devices addresses |

<a id="job-bt-paired-devices-list-loeschen"></a>
### BT_PAIRED_DEVICES_LIST_LOESCHEN

Delete list with Bluetooth paired devices

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-bt-paired-devices-loeschen"></a>
### BT_PAIRED_DEVICES_LOESCHEN

Delete list with Bluetooth paired devices

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-bt-discoverable-mode"></a>
### BT_DISCOVERABLE_MODE

Bring Bluetooth Server into discoverable mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-bt-enable"></a>
### BT_ENABLE

Enable Bluetooth operation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-bt-disable"></a>
### BT_DISABLE

Disable Bluetooth operation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-bt-operationmode-lesen"></a>
### BT_OPERATIONMODE_LESEN

read if BT operation is enabled or disabled

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BLUETOOTH_FLAG | int | 1-byte BT flag: 0x00 - disabled, 0x01 - enabled |

<a id="job-dsp-acoustic-profile-lesen"></a>
### DSP_ACOUSTIC_PROFILE_LESEN

GAL: read DSP acoustic profile (1-16)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| DSP_ACOUSTIC_PROFILE | int | 1-byte DSP acoustic profile (1-16) |

<a id="job-gal-kmh-per-stage-schreiben"></a>
### GAL_KMH_PER_STAGE_SCHREIBEN

GAL: set km/h per amplification stage (10 - 60)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | km/h per amplification stage (10-60) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-gal-kmh-per-stage-lesen"></a>
### GAL_KMH_PER_STAGE_LESEN

GAL: read km/h per amplification stage (10 - 60)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| GAL_KMH_PER_STAGE | int | 1-byte km/h value per amplification stage for speed-dependent loudness |

<a id="job-ecall-enable"></a>
### ECALL_ENABLE

Enable ecall

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-ecall-disable"></a>
### ECALL_DISABLE

Disable E-call

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-ecall-status-lesen"></a>
### ECALL_STATUS_LESEN

read if E-call is enabled or disabled

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| E_CALL_FLAG | int | 1-byte E-call flag: 0x00 - disabled, 0x01 - enabled |

<a id="job-telematics-status-lesen"></a>
### TELEMATICS_STATUS_LESEN

read if telematics operation is enabled or disabled

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| TELEMATICS_FLAG | int | 1-byte telematics flag: 0x00 - disabled, 0x01 - enabled |

<a id="job-non-telematics-e-call-status-lesen"></a>
### NON_TELEMATICS_E_CALL_STATUS_LESEN

read if non-telematic E-call (call 911/112) is enabled or disabled

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| NON_TELEMATIC_E_CALL_FLAG | int | 1-byte non-telematic E-call flag: 0x00 - disabled, 0x01 - enabled |

<a id="job-us-cust-calls-enable"></a>
### US_CUST_CALLS_ENABLE

Enable customer calls over NAD with GMIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-cust-calls-disable"></a>
### US_CUST_CALLS_DISABLE

Disable customer calls over NAD with GMIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-cust-calls-lesen"></a>
### US_CUST_CALLS_LESEN

Read if customer calls over NAD using telematic GMIN are enabled or disabled

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CALLS_WITH_GMIN_FLAG | int | 1-byte calls with GMIN flag: 0x00 - disabled, 0x01 - enabled |

<a id="job-backup-emergency-no-schreiben"></a>
### BACKUP_EMERGENCY_NO_SCHREIBEN

Set emergency number (e.g. 112/911) for non-telematic E-calls

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EMERGENCY_NUM | string | (20 bytes, ASCII) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-backup-emergency-no-lesen"></a>
### BACKUP_EMERGENCY_NO_LESEN

Read backup emergency number used for non-telematic E-calls (e.g.112/911)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| BACKUP_EMERGENCY_NUMBER | string | 20-byte phone number (ASCII, left-justified, unused bytes 0x00) |

<a id="job-us-call-service-center-status-lesen"></a>
### US_CALL_SERVICE_CENTER_STATUS_LESEN

read if call service center (e.g. Verizon)is enabled or disabled

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CALL_SERVICE_CENTER_FLAG | int | 1-byte temporary storage of cutomer PIN flag: 0x00 - disabled, 0x01 - enabled |

<a id="job-us-call-service-center-number-schreiben"></a>
### US_CALL_SERVICE_CENTER_NUMBER_SCHREIBEN

Set phone number of call service number (Verizon)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERV_CENT_NO | string | Service center number |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-call-service-center-number-lesen"></a>
### US_CALL_SERVICE_CENTER_NUMBER_LESEN

Read phone number of call service center (Verizon)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| US_CALL_SERVICE_CENTER_NUMBER | string | 20-byte phone number (ASCII, left-justified, unused bytes 0x00) |

<a id="job-us-min-schreiben"></a>
### US_MIN_SCHREIBEN

Set MIN in Ericsson CM-42 NAD for US telenatics

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| US_MIN | string | 10-stellige US MIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |

<a id="job-fg-schreiben-as-us-min"></a>
### FG_SCHREIBEN_AS_US_MIN

Write last 5 digits of FG in GMIN Based on standard Codierjob C_FG_SCHREIBEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-us-cdma-directory-schreiben"></a>
### US_CDMA_DIRECTORY_SCHREIBEN

Set US CM-42 CDMA Directory 00000 00000 - 99999 99999

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CDMA_DIR | string | OKAY, wenn fehlerfrei CDMA Directory |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-cdma-directory-lesen"></a>
### US_CDMA_DIRECTORY_LESEN

CDMA Directory 00000 00000 00000 - 99999 99999 99999 -&gt; 0x31..0x31 - 0x39..0x39

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CDMA_DIR | string | 1 - 15 digit CDMA Directory |

<a id="job-us-sid-nid-schreiben"></a>
### US_SID_NID_SCHREIBEN

Set US CM-42 System ID and Network ID

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INDEX | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SID | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| NID | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-sid-nid-lesen"></a>
### US_SID_NID_LESEN

Read US CM-42 Home SID/NID list

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CM42_SID_NID_LIST | string | &lt;index&gt;:&lt;sid&gt;:&lt;nid&gt; ........ &lt;index&gt;:&lt;sid&gt;:&lt;nid&gt;  in ASCII |
| SID | string | System ID |
| NID | string | Network ID |
| INDEX | string | Index |

<a id="job-us-cdma-primary-ch-a-schreiben"></a>
### US_CDMA_PRIMARY_CH_A_SCHREIBEN

Set US CM-42 CDMA Primary Channel A

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CDMA_PA | string | 1.byte of Primary Channel A (1-311, 689-694, 1013-1023 as ASCII bytes) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-cdma-primary-ch-a-lesen"></a>
### US_CDMA_PRIMARY_CH_A_LESEN

Read US CM-42 CDMA Primary Channel (1-311, 689-694, 1013-1023 as ASCII bytes)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CDMA_PA | string | 1 - 4-byte CDMA Primary Channel A |

<a id="job-us-cdma-secondary-ch-a-schreiben"></a>
### US_CDMA_SECONDARY_CH_A_SCHREIBEN

Set US CM-42 CDMA Secondary Channel A

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CDMA_SA | string | 1.byte of Secondary Channel A (1-311, 689-694, 1013-1023 as ASCII bytes) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-cdma-secondary-ch-a-lesen"></a>
### US_CDMA_SECONDARY_CH_A_LESEN

Read US CM-42 CDMA Secondary Channel A  (1-311, 689-694, 1013-1023 as ASCII bytes)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CDMA_SA | string | 1 - 4-byte CDMA Secondary Channel A |

<a id="job-us-cdma-primary-ch-b-schreiben"></a>
### US_CDMA_PRIMARY_CH_B_SCHREIBEN

Set US CM-42 CDMA Primary Channel B

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CDMA_PB | string | 1.byte of Primary Channel B (365-644, 739-777 as ASCII bytes) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-cdma-primary-ch-b-lesen"></a>
### US_CDMA_PRIMARY_CH_B_LESEN

Read US CM-42 CDMA Primary Channel B  (365-644, 739-777 as ASCII bytes)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CDMA_PB | string | 1 - 4-byte CDMA Primary Channel B |

<a id="job-us-cdma-secondary-ch-b-schreiben"></a>
### US_CDMA_SECONDARY_CH_B_SCHREIBEN

Set US CM-42 CDMA Secondary Channel B

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CDMA_SB | string | 1.byte of Secondary Channel B (365-644, 739-777 as ASCII bytes) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-cdma-secondary-ch-b-lesen"></a>
### US_CDMA_SECONDARY_CH_B_LESEN

Read US CM-42 CDMA Secondary Channel B (365-644, 739-777 as ASCII bytes)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CDMA_SB | string | 1 - 4-byte CDMA Secondary Channel B |

<a id="job-us-home-only-enable"></a>
### US_HOME_ONLY_ENABLE

Enable Home Only

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-home-only-disable"></a>
### US_HOME_ONLY_DISABLE

Disable Home Only

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-home-only-lesen"></a>
### US_HOME_ONLY_LESEN

read status of home only

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| HOME_ONLY_FLAG | int | 1-byte 0x00 disabled, 0x01 - enabled |

<a id="job-us-a-b-side-schreiben"></a>
### US_A_B_SIDE_SCHREIBEN

Set Home Only Status (0-3)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Home Only Status (0-3) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

MTS/FETRAWE Mode (00 Exit) (01 Manufacturing) (02 Service) (03 Production)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRODUKTIONSMODE | string | "ein,1" -&gt; Produktions Mode ein "aus,0" -&gt; Produktions Mode aus table DigitalArgument TEXT Default: "aus" |
| TRANSPORTMODE | string | "ein,1" -&gt; Transport Mode ein "aus,0" -&gt; Transport Mode aus table DigitalArgument TEXT Default: "aus" |
| WERKSTATTMODE | string | "ein,1" -&gt; Werkstatt Mode ein "aus,0" -&gt; Werkstatt Mode aus table DigitalArgument TEXT Default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-esn-min-lesen"></a>
### US_ESN_MIN_LESEN

Read MIN in Ericsson CM-42 NAD for US telematics

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| US_MIN | string | 10-byte US-MIN in ASCII |
| US_ESN | string | 12-digits ESN |

<a id="job-imei-lesen"></a>
### IMEI_LESEN

Read IMEI

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| IMEI | string | 15 byte |

<a id="job-us-k633-enable"></a>
### US_K633_ENABLE

Enable Bluetooth portable support for US (K633)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-us-k633-lesen"></a>
### US_K633_LESEN

Read status of US Bluetooth portable support (K633)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| US_K633_FLAG | int | 1-byte 0x00 disabled, 0x01 - enabled |

<a id="job-us-k633-disable"></a>
### US_K633_DISABLE

Disable Bluetooth portable support for US (K633)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-nad-equipped-enable"></a>
### NAD_EQUIPPED_ENABLE

Enable NAD equipped coding parameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-nad-equipped-lesen"></a>
### NAD_EQUIPPED_LESEN

Read status of the NAD equipped coding parameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| NAD_EQUIPPED_FLAG | int | 1-byte 0x00 disabled, 0x01 - enabled |

<a id="job-nad-equipped-disable"></a>
### NAD_EQUIPPED_DISABLE

Disable NAD equipped coding parameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-hw-selbtest-status-lesen"></a>
### HW_SELBTEST_STATUS_LESEN

Read results of the HW selftest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| HW_SELFTEST_RESULT_BYTE | int | 2 bytes result bytes |

## Tables

### Index

- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [PAIRINGRESULT](#table-pairingresult) (3 × 2)
- [TCUTYPE_STATUS](#table-tcutype-status) (3 × 2)
- [FORTTEXTE](#table-forttexte) (22 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IORTTEXTE](#table-iorttexte) (14 × 2)
- [IARTTEXTE](#table-iarttexte) (3 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [TGPSSTATUS](#table-tgpsstatus) (14 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (67 × 2)

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 16 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
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

<a id="table-pairingresult"></a>
### PAIRINGRESULT

Dimensions: 3 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | SUCCESS |
| 0x01 | FAILURE |
| 0x02 | WAITING |

<a id="table-tcutype-status"></a>
### TCUTYPE_STATUS

Dimensions: 3 rows × 2 columns

| TCU_TYPE | TCU_TYPE_TEXT |
| --- | --- |
| 0x05 | I-bus ECE |
| 0x06 | I-bus US |
| 0xXY | unbekannte TCU |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 22 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x68 | Kurzschluss in der GPS Antenne |
| 0x69 | GPS Antenne nicht angeschlossen |
| 0x6A | Hardware Fehler im GPS Modul |
| 0x6B | Kommunikation mit dem GPS Modul gestoert |
| 0x6D | E-call nicht angeschlossen |
| 0x6E | Fehler mit der E-call LED |
| 0x70 | E-call ist kurzgeschlossen |
| 0x73 | Fehler non-volatile Speicherbereich |
| 0x74 | E-call button stuck |
| 0x79 | Interne Fehler mit dem BT Interface |
| 0x7A | Energiesparmode aktiv |
| 0x7E | Fehler mit der backup Battery |
| 0x7F | B-call ist kurzgeschlossen |
| 0x80 | B-call nicht angeschlossen |
| 0x81 | B-call button stuck |
| 0x98 | Microphone 1 Error |
| 0xA0 | Prefit SIM Not Present |
| 0xA1 | Prefit SIM Lesen Error |
| 0xA2 | Prefit SIM Pin Locked |
| 0x90 | Backup Antenna Disconnected |
| 0x97 | BT Cradle Stuck Button |
| 0xXY | unbekannte Fehlerart |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x20 | Fehler momentan vorhanden |
| 0xXY | unbekannte Fehlerart |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x08 | Software Reset Fehler |
| 0x11 | I-Bus Fehler |
| 0x12 | low RF  |
| 0x13 | NVM korrumpiert |
| 0x14 | Fehler mit der Codierung |
| 0x15 | Fehler mit dem Transceiver |
| 0x16 | Fehler mit dem Handy |
| 0x17 | E-call LED not ok / Fehler mit der E-call LED |
| 0x18 | GPS COMMS Failure / Kommunikation mit dem GPS Modul gestoert |
| 0x1A | Prefit SIM Not Present |
| 0x1B | Prefit SIM Lesen Error |
| 0x1C | Prefit SIM Pin Locked |
| 0x1D | Prefit SIM Network Error |
| 0xXY | unbekannte Fehlerart |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x20 | Fehler momentan vorhanden |
| 0xXY | unbekannte Fehlerart |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-tgpsstatus"></a>
### TGPSSTATUS

Dimensions: 14 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Kein GPS |
| 0x01 | Kommunikationsfehler |
| 0x02 | GPS Empfängerfehler |
| 0x03 | Kein Almanach |
| 0x04 | Suche Satellit |
| 0x05 | Verfolge 1 Satellit |
| 0x06 | Verfolge 2 Satelliten |
| 0x07 | Verfolge 3 Satelliten |
| 0x08 | Verfolge 4 Satelliten |
| 0x09 | Verfolge 5 Satelliten |
| 0x0A | Verfolge 6 Satelliten |
| 0x0B | 2D Positionierung |
| 0x0C | 3D Positionierung |
| 0xXY | nicht definiert |

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

Dimensions: 67 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |
