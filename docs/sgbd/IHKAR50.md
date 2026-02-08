# IHKAR50.prg

- Jobs: [22](#jobs)
- Tables: [11](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integrierte Heiz- Klimaautomatik R50 |
| ORIGIN | BMW TI-430 Drexel |
| REVISION | 1.3 |
| AUTHOR | SW-Style Rafferty, BMW TI-431 Küssel, BMW TI-430 Drexel |
| COMMENT | N/A |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Identification data
- [FS_LESEN](#job-fs-lesen) - Read faults
- [FS_LOESCHEN](#job-fs-loeschen) - Clears All Faults
- [SPEICHER_LESEN](#job-speicher-lesen) - Read ECU Memory by Address Speicher lesen mit adresse
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Write memory to a specified address Speicher schreiben mit adresse
- [STATUS_SYSTEM_PARAMETER](#job-status-system-parameter) - Read the system parameters
- [READ_MANUFACTURER_DATA](#job-read-manufacturer-data) - Read both blocks of manufacturer data
- [STEUERN_SELF_TEST](#job-steuern-self-test) - Enter Self test mode
- [SG_RESET](#job-sg-reset) - Reset ECU
- [STEUERN_ACTUATORS](#job-steuern-actuators) - Force the blend actuators IO block 0
- [STEUERN_LCD_LED](#job-steuern-lcd-led) - Force the LEDs and LCDs IO block 1
- [STEUERN_AIRCON_RECIRC](#job-steuern-aircon-recirc) - Force Air conditioning and recirculation IO block 2
- [STATUS_IO_DIGITAL](#job-status-io-digital) - Read IO States for block 0 - Push Buttons, LEDs and Set Points
- [STATUS_IO_ANALOGUE](#job-status-io-analogue) - Read IO States for block 0 - Push Buttons, LEDs and Set Points
- [CALIBRATE_MOTORS](#job-calibrate-motors) - Send manual calibration of blend and distribution motors message
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. Only the last 3 bytes can be written
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Ping message
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes

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

<a id="job-ident"></a>
### IDENT

Identification data

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_BMW_NR | string | BMW-Teilenummer BMW Part Number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW Week of manufacture |
| ID_DATUM_JAHR | int | Herstelldatum Jahr Year of manufacture |
| ID_SW_NR | int | Software version |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) 1, If AIF data is available |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-fs-lesen"></a>
### FS_LESEN

Read faults

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode Raw fault data from the ECU |
| F_ORT_NR | int | Index fuer Fehlerort Fault number |
| F_ORT_TEXT | string | Fehlerort als Text Fault description |
| F_HFK | int | Fehlerhaeufigkeit Frequency |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Count of Environment Data Items per fault |
| F_UW1_NR | int | Umweltbedingung 1 Index First Environment Result Index |
| F_UW1_TEXT | string | Umweltbedingung 1 Text First Environment Result Description |
| F_UW1_WERT | real | Umweltbedingung 1 Wert First Environment Result Value |
| F_UW1_EINH | string | Umweltbedingung 1 Einheit First Environment Result Units |
| F_UW2_NR | int | Umweltbedingung 2 Index Second Environment Result Index |
| F_UW2_TEXT | string | Umweltbedingung 2 Text Second Environment Result Description |
| F_UW2_WERT | real | Umweltbedingung 2 Wert Second Environment Result Value |
| F_UW2_EINH | string | Umweltbedingung 2 Einheit Second Environment Result Units |
| F_UW3_NR | int | Umweltbedingung 3 Index Third Environment Result Index |
| F_UW3_TEXT | string | Umweltbedingung 3 Text Third Environment Result Description |
| F_UW3_WERT | real | Umweltbedingung 3 Wert Third Environment Result Value |
| F_UW3_EINH | string | Umweltbedingung 3 Einheit Third Environment Result Units |
| F_UW4_NR | int | Umweltbedingung 4 Index Fourth Environment Result Index |
| F_UW4_TEXT | string | Umweltbedingung 4 Text Fourth Environment Result Description |
| F_UW4_WERT | real | Umweltbedingung 4 Wert Fourth Environment Result Value |
| F_UW4_EINH | string | Umweltbedingung 4 Einheit Fourth Environment Result Units |
| F_ART_ANZ | int | Anzahl der Fehlerarten Count of additional fault status information |
| F_ART1_NR | int | 1. (einzige) Fehlerart Fault status 1 |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text Fault status text 1 |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read quick fault memory response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read detailed fault memory response |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Clears All Faults

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet table JobResult STATUS_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Read ECU Memory by Address Speicher lesen mit adresse

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADDRESS | unsigned long | Address in EEPROM 0x0000 -&gt; 0x01FF |
| LENGTH | unsigned int | Length of memory to read, 1 -&gt; 32 Anzahl spiecher lesen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATA | binary | ECU data which is read |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Write memory to a specified address Speicher schreiben mit adresse

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADDRESS | unsigned long | Address in EEPROM 0x0000 -&gt; 0x01FF |
| LENGTH | unsigned int | Length of memory to read, 1 -&gt; 27 Anzahl spiecher schreiben |
| DATA | string | Data bytes to write |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write memory response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read memory response |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| R1 | int | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-system-parameter"></a>
### STATUS_SYSTEM_PARAMETER

Read the system parameters

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_SUN_LOAD_WERT | real | Sun load |
| STAT_SUN_LOAD_EINH | string |  |
| STAT_CABIN_TEMP_WERT | real | Cabin temperature |
| STAT_CABIN_TEMP_EINH | string |  |
| STAT_HEATER_AIR_OFF_TEMP_WERT | real | Heater air off temperature |
| STAT_HEATER_AIR_OFF_TEMP_EINH | string |  |
| STAT_BLENDDOOR_CURRENT_FDBK_WERT | real | Blend door feedback |
| STAT_BLENDDOOR_CURRENT_FDBK_EINH | string |  |
| STAT_DISTRIB_CURRENT_FDBK_WERT | real | Distribution feedback |
| STAT_DISTRIB_CURRENT_FDBK_EINH | string |  |
| STAT_MINUS_BLOWER_VOLTAGE_WERT | real | Blower- voltage |
| STAT_MINUS_BLOWER_VOLTAGE_EINH | string |  |
| STAT_PLUS_BLOWER_VOLTAGE_WERT | real | Blower+ voltage |
| STAT_PLUS_BLOWER_VOLTAGE_EINH | string |  |
| STAT_BATTERY_VOLTAGE_WERT | real | Battery Voltage |
| STAT_BATTERY_VOLTAGE_EINH | string |  |
| STAT_ASPIRATOR_DIAG_FREQ_WERT | real | Aspirator Distribution feedback |
| STAT_ASPIRATOR_DIAG_FREQ_EINH | string |  |
| STAT_CALIBRATION_DISTRI_MOTOR_WERT | string | Calibration Done = AA |
| STAT_CALIBRATION_DISTRI_MOTOR_EINH | string |  |
| STAT_CALIBRATION_BLEND_MOTOR_WERT | string | Calibration Done = AA |
| STAT_CALIBRATION_BLEND_MOTOR_EINH | string |  |
| STAT_SOFTWARE_VERSION_WERT | string | Software version |
| STAT_SOFTWARE_VERSION_EINH | string |  |
| STAT_SOFTWARE_INDEX_WERT | string | Software index |
| STAT_SOFTWARE_INDEX_EINH | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-read-manufacturer-data"></a>
### READ_MANUFACTURER_DATA

Read both blocks of manufacturer data

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Block 0 response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Block 1 response |
| SERIAL_NUM | string | Manufacturer Serial Number |
| BLOCK_0_TEST_BYTE | int | Manufacturer test byte |
| OPTIONAL_BYTE | int | Manufacturer optional byte |
| DAY_MANU | int | Day of Manufacturer |
| MONTH_MANU | int | Month of Manufacturer |
| YEAR_MANU | int | Year of Manufacturer |
| BLOCK_1_TEST_BYTE | int | Manufacturer test byte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-self-test"></a>
### STEUERN_SELF_TEST

Enter Self test mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-sg-reset"></a>
### SG_RESET

Reset ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-actuators"></a>
### STEUERN_ACTUATORS

Force the blend actuators IO block 0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FORCE_BLEND | int | Force Blend (1 = force, 0 = not force) |
| BLEND_PCT | int | Blend percentage 0 - 100% |
| FORCE_DISTRIB | int | Force Distrib (1 = force, 0 = not force) |
| DISTRIB_PCT | int | Distribution percentage 0 - 100% |
| FORCE_BLOWER | int | Force Blower (1 = force, 0 = not force) |
| BLOWER_LEVEL | int | Blower level 0 - 31 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-lcd-led"></a>
### STEUERN_LCD_LED

Force the LEDs and LCDs IO block 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FORCE_LCD_LED | int | Force LCDs and LEDs (1 = force, 0 = not force) |
| LCD_DUTY_CYCLE | int | LCD duty cycle wert 0 -&gt; 255 |
| LED_BIT_0_TO_7 | int | LEDs Bits 0 to 7 (BIT = 1 LED ON, 0 LED OFF) wert 0 -&gt; 255 |
| LED_BIT_8_TO_10 | int | LEDs Bits 8 to 10 (BIT = 1 LED ON, 0 LED OFF) Bits 11 -&gt; 15 unused. wert 0 -&gt; 7 |
| LCD_BIT_0_TO_7 | int | LCDs Bits 0 to 7 (BIT = 1 LCD ON, 0 LCD OFF) wert 0 -&gt; 255 |
| LCD_BIT_8_TO_15 | int | LCDs Bits 8 to 15 (BIT = 1 LCD ON, 0 LCD OFF) wert 0 -&gt; 255 |
| LCD_BIT_16_TO_23 | int | LCDs Bits 16 to 23 (BIT = 1 LCD ON, 0 LCD OFF) wert 0 -&gt; 255 |
| LCD_BIT_24_TO_29 | int | LCDs Bits 24 to 29 (BIT = 1 LCD ON, 0 LCD OFF) Bits 30 -&gt; 31 unused. wert 0 -&gt; 63 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-aircon-recirc"></a>
### STEUERN_AIRCON_RECIRC

Force Air conditioning and recirculation IO block 2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FORCE_AIRCON | int | Force Aircon (1 = force, 0 = not force) |
| AIRCON_ON | int | Air conditioning  value (1 = ON, 0 = OFF) |
| FORCE_RECIRC | int | Force Recirc (1 = force, 0 = not force) |
| RECIRC_ON | int | Recirculation value (1 - ON, 0 - OFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-digital"></a>
### STATUS_IO_DIGITAL

Read IO States for block 0 - Push Buttons, LEDs and Set Points

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DISTRIB_SCREEN_ACTIVE | int | Distribution to screen 1=activ, 0=nicht |
| STAT_DISTRIB_FEET_ACTIVE | int | Distribution to feet 1=activ, 0=nicht |
| STAT_DISTRIB_FACE_ACTIVE | int | Distribution to face 1=activ, 0=nicht |
| STAT_BLOWER_AUTO_ACTIVE | int | Automatic Blower 1=activ, 0=nicht |
| STAT_RECIRC_ACTIVE | int | Recirculation mode 1=activ, 0=nicht |
| STAT_AC_ACTIVE | int | AirCon mode 1=activ, 0=nicht |
| STAT_DISTRIB_AUTO_ACTIVE | int | Automatic Distribution 1=activ, 0=nicht |
| STAT_RECIRC_AUTO_ACTIVE | int | Automatic recirculation 1=activ, 0=nicht |
| STAT_BLUE_RED_LED_ON | int | Blue/red LED on 1 wenn ein / 0 wenn aus |
| STAT_LCD_LED_ON | int | LCD LED on 1 wenn ein / 0 wenn aus |
| STAT_BACKLIGHT_LED_ON | int | Backlight LED on 1 wenn ein / 0 wenn aus |
| STAT_DISTRIB_FACE_LED_ON | int | Touch LED for face distributiuon on 1 wenn ein / 0 wenn aus |
| STAT_DISTRIB_SCREEN_LED_ON | int | Touch LED for screen distributiuon on 1 wenn ein / 0 wenn aus |
| STAT_DISTRIB_FEET_LED_ON | int | Touch LED for feet distributiuon on 1 wenn ein / 0 wenn aus |
| STAT_AUTO_LED_ON | int | Touch LED Auto on 1 wenn ein / 0 wenn aus |
| STAT_AC_LED_ON | int | Touch LED for AirCon on 1 wenn ein / 0 wenn aus |
| STAT_RECIRC_LED_ON | int | Touch LED for recirculation on 1 wenn ein / 0 wenn aus |
| STAT_HRW_HFS_LED_ON | int | LED for heated rear window and heated fromt screen on 1 wenn ein / 0 wenn aus |
| STAT_TEMP_UNIT_FARENHEIT | int | Temperature unit 1 wenn Farenheit / 0 wenn Celsius |
| STAT_TEMP_PLUS_BUTTON_PRESSED | int | Temperature+ button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_TEMP_MINUS_BUTTON_PRESSED | int | Temperature- button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_BLOWER_PLUS_BUTTON_PRESSED | int | Blower+ button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_BLOWER_MINUS_BUTTON_PRESSED | int | Blower- button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_FACE_BUTTON_PRESSED | int | Distribution Face button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_SCREEN_BUTTON_PRESSED | int | Distribution Screen button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_FEET_BUTTON_PRESSED | int | Distribution Feet button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_AUTO_BUTTON_PRESSED | int | Automatic button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_AC_BUTTON_PRESSED | int | AirCon button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_OFF_BUTTON_PRESSED | int | Off button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_RECIRC_BUTTON_PRESSED | int | Recirculation button pressed 1 wenn einschalten / 0 wenn ausschalten |
| STAT_HRW_HFS_BUTTON_PRESSED | int | Heated rear window and heated front screen button pressed 1 wenn einschalten / 0 wenn ausschalten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-io-analogue"></a>
### STATUS_IO_ANALOGUE

Read IO States for block 0 - Push Buttons, LEDs and Set Points

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |
| STAT_TEMP_SET_POINT_WERT | real | Temperature Set Point |
| STAT_TEMP_SET_POINT_EINH | string |  |
| STAT_BLOWER_SET_POINT_WERT | real | Blower Set Point |
| STAT_BLOWER_SET_POINT_EINH | string |  |
| STAT_LCD_DUTY_CYCLE_WERT | real | LCD PWM Duty Cycle |
| STAT_LCD_DUTY_CYCLE_EINH | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-calibrate-motors"></a>
### CALIBRATE_MOTORS

Send manual calibration of blend and distribution motors message

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. Only the last 3 bytes can be written

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read teststamp response |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write teststamp telegram to ECU |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Write teststamp response |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG Read new teststamp response |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Ping message

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (59 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [ANALOGUE](#table-analogue) (17 × 4)
- [DIGITAL](#table-digital) (32 × 4)
- [FORTTEXTE](#table-forttexte) (12 × 2)
- [FARTTEXTE](#table-farttexte) (10 × 2)
- [FARTMATRIX](#table-fartmatrix) (12 × 13)
- [FUMWELTMATRIX](#table-fumweltmatrix) (12 × 7)
- [FUMWELTTEXTE](#table-fumwelttexte) (14 × 5)

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

Dimensions: 59 rows × 2 columns

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

<a id="table-analogue"></a>
### ANALOGUE

Dimensions: 17 rows × 4 columns

| NAME | FACT_A | FACT_B | EINH |
| --- | --- | --- | --- |
| TEMP_SET_POINT | 0.1 | 0.0 | C |
| BLOWER_SET_POINT | 1.0 | 0.0 |  |
| LCD_DUTY_CYCLE | 1.0 | 0.0 |  |
| SUN_LOAD | 1.0 | 0.0 | W/m2 |
| CABIN_TEMP | 0.1 | 0.0 | C |
| HEATER_AIR_OFF_TEMP | 0.1 | 0.0 | C |
| BLENDDOOR_CURRENT_FDBK | 1.0 | 0.0 | % |
| DISTRIB_CURRENT_FDBK | 1.0 | 0.0 | % |
| MINUS_BLOWER_VOLTAGE | 0.1 | 0.0 | V |
| PLUS_BLOWER_VOLTAGE | 0.1 | 0.0 | V |
| BATTERY_VOLTAGE | 0.1 | 0.0 | V |
| ASPIRATOR_DIAG_FREQ | 1.0 | 0.0 | Hz |
| CALIBRATION_DISTRI_MOTOR | 0.0 | 0.0 |  |
| CALIBRATION_BLEND_MOTOR | 0.0 | 0.0 |  |
| SOFTWARE_VERSION | 0.0 | 0.0 |  |
| SOFTWARE_INDEX | 0.0 | 0.0 |  |
| ?? | 0.0 | 0.0 | ?? |

<a id="table-digital"></a>
### DIGITAL

Dimensions: 32 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| DISTRIB_SCREEN | 8 | 0x01 | 0x01 |
| DISTRIB_FEET | 8 | 0x02 | 0x02 |
| DISTRIB_FACE | 8 | 0x04 | 0x04 |
| BLOWER_AUTO | 8 | 0x08 | 0x08 |
| RECIRC | 8 | 0x10 | 0x10 |
| AC | 8 | 0x20 | 0x20 |
| DISTRIB_AUTO | 8 | 0x40 | 0x40 |
| RECIRC_AUTO | 8 | 0x80 | 0x80 |
| BLUE_RED_LED | 9 | 0x01 | 0x01 |
| LCD_LED | 9 | 0x02 | 0x02 |
| BACKLIGHT_LED | 9 | 0x04 | 0x04 |
| DISTRIB_FACE_LED | 9 | 0x08 | 0x08 |
| DISTRIB_SCREEN_LED | 9 | 0x10 | 0x10 |
| DISTRIB_FEET_LED | 9 | 0x20 | 0x20 |
| AUTO_LED | 9 | 0x40 | 0x40 |
| AC_LED | 9 | 0x80 | 0x80 |
| RECIRC_LED | 10 | 0x02 | 0x02 |
| HRW_HFS_LED | 10 | 0x04 | 0x04 |
| TEMP_UNIT_FARENHEIT | 10 | 0x80 | 0x80 |
| TEMP_PLUS_BUTTON | 11 | 0x01 | 0x01 |
| TEMP_MINUS_BUTTON | 11 | 0x02 | 0x02 |
| BLOWER_PLUS_BUTTON | 11 | 0x04 | 0x04 |
| BLOWER_MINUS_BUTTON | 11 | 0x08 | 0x08 |
| FACE_BUTTON | 11 | 0x10 | 0x10 |
| SCREEN_BUTTON | 11 | 0x20 | 0x20 |
| FEET_BUTTON | 11 | 0x40 | 0x40 |
| AUTO_BUTTON | 11 | 0x80 | 0x80 |
| AC_BUTTON | 12 | 0x01 | 0x01 |
| OFF_BUTTON | 12 | 0x02 | 0x02 |
| RECIRC_BUTTON | 12 | 0x04 | 0x04 |
| HRW_HFS_BUTTON | 12 | 0x08 | 0x08 |
| ?? | 0 | 0x00 | 0x00 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 12 rows × 2 columns

| ORTNR | ORTTEXT |
| --- | --- |
| 0x01 | Solarsensor Fehler |
| 0x02 | Innenraumtemperaturfuehler Fehler |
| 0x03 | Heizluft aus Fehler |
| 0x04 | Verteilung Fehler |
| 0x05 | Mischklappe Fehler |
| 0x06 | Geblaese (-) Fehler |
| 0x07 | Geblaese (+) Fehler |
| 0x08 | Absauggeraet Fehler |
| 0x09 | Luftverteilungsmotor Fehler |
| 0x0A | Mischklappenmotor Fehler |
| 0xFE | Energiesparmode aktiviert |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Leitungsunterbrechung or Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung or Gebläse Kurzschluss |
| 0x04 | Frequenz &lt; 15Hz |
| 0x05 | ungueltiger Wert fuer U-Batt |
| 0x06 | Rueckmeldung konstant |
| 0x07 | ungueltiger Wert fuer Masse |
| 0x08 | Flag = 1 |
| 0xFF | unbekannter Status |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 12 rows × 13 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 0xFF | 0x02 | 0xFF | 0x01 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x02 | 0xFF | 0x02 | 0xFF | 0x01 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x03 | 0xFF | 0x02 | 0xFF | 0x01 | 0xFF | 0xFF |  0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x04 | 0xFF | 0x02 | 0xFF | 0x01 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x05 | 0xFF | 0x02 | 0xFF | 0x01 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x06 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x05 | 0xFF | 0x07 |
| 0x07 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x03 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x08 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x04 | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x09 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x06 | 0xFF | 0x08 |
| 0x0A | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x06 | 0xFF | 0x08 |
| 0xFE | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0x05 | 0xFF | 0x07 |
| 0x00 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 12 rows × 7 columns

| ORT | UW_ANZ | UW_SATZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 3 | 1 | 0x01 | 0x02 | 0x03 | -- |
| 0x02 | 3 | 1 | 0x01 | 0x02 | 0x04 | -- |
| 0x03 | 3 | 1 | 0x01 | 0x02 | 0x05 | -- |
| 0x04 | 3 | 1 | 0x01 | 0x02 | 0x06 | -- |
| 0x05 | 3 | 1 | 0x01 | 0x02 | 0x07 | -- |
| 0x06 | 4 | 1 | 0x01 | 0x02 | 0x08 | 0x09 |
| 0x07 | 3 | 1 | 0x01 | 0x02 | 0x08 | -- |
| 0x08 | 3 | 1 | 0x01 | 0x02 | 0x0A | -- |
| 0x09 | 3 | 1 | 0x01 | 0x0B | 0x0C | -- |
| 0x0A | 3 | 1 | 0x01 | 0x0B | 0x0D | -- |
| 0xFE | 4 | 1 | 0x01 | 0x02 | 0x08 | 0x09 |
| 0x00 | 0 | 0 | 0x00 | 0x00 | 0x00 | 0x00 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 14 rows × 5 columns

| UWNR | UWTEXT | UW_EINH | UW_A | UW_B |
| --- | --- | --- | --- | --- |
| 0x01 | Batterie Spannung |  | 1.0 | 0 |
| 0x02 | IP Wert |  | 1.0 | 0 |
| 0x03 | FA2 + FA3 |  | 1.0 | 0 |
| 0x04 | FA1 + FA3 |  | 1.0 | 0 |
| 0x05 | FA1 + FA2 |  | 1.0 | 0 |
| 0x06 | FA5 |  | 1.0 | 0 |
| 0x07 | FA4 |  | 1.0 | 0 |
| 0x08 | Geblaese PWM |  | 1.0 | 0 |
| 0x09 | Geblaese + |  | 1.0 | 0 |
| 0x0A | Innenraumtemperatur |  | 1.0 | 0 |
| 0x0B | Rueckmeldung Wert |  | 1.0 | 0 |
| 0x0C | Luftverteilung Strom |  | 1.0 | 0 |
| 0x0D | Mischer Strom |  | 1.0 | 0 |
| 0x00 | ?? |  | 0.0 | 0 |
