# EMS2K.prg

- Jobs: [123](#jobs)
- Tables: [11](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EMS2K |
| ORIGIN | BMW TI-431 Majerus |
| REVISION | 1.15 |
| AUTHOR | Software Style Mike Rafferty, Ricardo Ian Short |
| COMMENT | R00  Software |
| PACKAGE | 1.14 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [START_DIAGNOSTIC_SESSION](#job-start-diagnostic-session) - Begins a diagnostic session
- [SEED_KEY](#job-seed-key) - Obtain security access to the ECU Schutzmechanismus SEED_KEY
- [IDENT_OLD](#job-ident-old) - Ident-Daten fuer EMS2000
- [IDENT](#job-ident) - Ident-Daten fuer EMS2000
- [IDENT_CODING](#job-ident-coding) - Ident-Daten fuer EMS2000
- [IDENT_EXTENDED](#job-ident-extended) - Read additional ECU Ident information
- [IDENT_AIF](#job-ident-aif) - Ident und AIF zusammen lesen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Tester present message
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden Stop the diagnostic session
- [SG_RESET](#job-sg-reset) - Reset the ECU
- [STAT_FREEZEFRAME](#job-stat-freezeframe) - Read the freeze frame data
- [FS_LESEN](#job-fs-lesen) - Read all faults
- [FS_LOESCHEN](#job-fs-loeschen) - Clears All Faults
- [READ_MEMORY](#job-read-memory) - Read ECU Memory by Address Speicher lesen mit Adresse
- [WRITE_MEMORY](#job-write-memory) - Write data to a specified memory address Speicher schreiben mit Adresse
- [ACCESS_TIMING_PARAMETERS](#job-access-timing-parameters) - Read the comms timing parameters Kommunikationsparameter lesen
- [CHANGE_TIMING_PARAMETERS](#job-change-timing-parameters) - Set timing parameters for standard or programming mode Diagnosetimeout aendern
- [CODE_LOESCHEN](#job-code-loeschen) - Erase the software code and calibration data within flash Das kalibrabrierung daten und software schluessel in flash loeshen
- [DATA_LOESCHEN](#job-data-loeschen) - Erase the calibration data within flash Das kalibrabrierung daten in flash loeshen
- [CHECK_REPROG_DEPENDING](#job-check-reprog-depending) - Calculate the checksum and check the coherence system
- [REPORT_REPROG_STATUS](#job-report-reprog-status) - Get the status of reprogramming after a mistake Programmieren status nach fehler auslesen
- [LEARN_IMOB_SEED](#job-learn-imob-seed) - The ECM learns the immobolisation seed
- [RESYNC_IMOB_SEED](#job-resync-imob-seed) - The ECM resynchronises the immobolisation seed
- [SLEEP_MODE](#job-sleep-mode) - Stop the power latch phase
- [START_MAN_TEST](#job-start-man-test) - Start the end of line test Hersteller test
- [START_CAT_TEST](#job-start-cat-test) - Start catalyst test Katalysator test
- [GIB_SELF_TEST](#job-gib-self-test) - Run the Gearbox Interface Box self test routine Getriebe Interface test
- [LDP_TEST](#job-ldp-test) - Run the Leak Detection Pump test Leckdiagnosepumpen test
- [EXECUTE_RAM_ROUTINE](#job-execute-ram-routine) - Start a routine which is stored within RAM (MTOS)
- [SWITCH_TO_BOOT](#job-switch-to-boot) - Allow activation of the boot software mode Needed for programming
- [SWNR_SCHREIBEN](#job-swnr-schreiben) - Write the Software number
- [TUNE_NR_SCHREIBEN](#job-tune-nr-schreiben) - Write the tune part number
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Request download
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Transfer data to the ECU
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Exit data transfer
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [AIF_SCHREIBEN](#job-aif-schreiben) - Write the AIF record
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen der Fahrgestellnummer aus dem Anwenderinfofeld Read the VIN from the current AIF record
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Schreiben der 17-stelligen Fahrgestellnummer in dem Anwenderinfofeld Write the VIN into the AIF record
- [C_ZCS_LESEN](#job-c-zcs-lesen) - Read the ZCS record
- [C_ZCS_AUFTRAG](#job-c-zcs-auftrag) - Write and verify the Central code
- [C_AZCS_LESEN](#job-c-azcs-lesen) - Read the auxiliary ZCS record
- [C_AZCS_AUFTRAG](#job-c-azcs-auftrag) - Write and verify the Auxiliary Central code
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren Write and verify coding data
- [C_CHECKSUM](#job-c-checksum) - Berechnung und Speicherung der Checksumme
- [CONFIG_BYTES_LESEN](#job-config-bytes-lesen) - Read the Configuraton Bytes
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Pruefcode-Daten in Hex auslesen
- [STEUERN_ACTUATOR](#job-steuern-actuator) - Actuator test
- [STEUERN_APPLICATION_CORRECTION](#job-steuern-application-correction) - Application correction. Non volatile adjustment
- [STEUERN_ADAPTIVE_VALUES](#job-steuern-adaptive-values) - Reset adaptive values
- [STATUS_ANA_WHEEL_SPEED](#job-status-ana-wheel-speed) - Read Analogue Input and Output States for LID 02 Read Anti Slip Control 2 analogue information (wheel speeds)
- [STATUS_ANA_CAN_ASC4](#job-status-ana-can-asc4) - Read Analogue Input and Output States for LID 04 Read Anti Slip Control 4 analogue information
- [STATUS_ANA_CAN_DME1](#job-status-ana-can-dme1) - Read Analogue Input and Output States for LID 05 Read Digital Motor Electronics 1 analogue information
- [STATUS_ANA_CAN_DME2](#job-status-ana-can-dme2) - Read Analogue Input and Output States for LID 06 Read Digital Motor Electronics 2 analogue information
- [STATUS_ANA_FUEL_CONS](#job-status-ana-fuel-cons) - Read Analogue Input and Output States for LID 07 Read Digital Motor Electronics 4 analogue information - Fuel Consumption
- [STATUS_ANA_CAN_DME5](#job-status-ana-can-dme5) - Read Analogue Input and Output States for LID 08 Read Digital Motor Electronics 5 analogue information
- [STATUS_ANA_WHEEL_TORQUE](#job-status-ana-wheel-torque) - Read Analogue Input and Output States for LID 09 Read Digital Motor Electronics 6 analogue information (wheel torques)
- [STATUS_ANA_CAN_EGS1](#job-status-ana-can-egs1) - Read Analogue Input and Output States for LID 0B Read Electonic Gear Selector 1 analogue information
- [STATUS_ANA_CVT1](#job-status-ana-cvt1) - Read Analogue Input and Output States for LID 0C Read Constant Velocity Transmission 1 analogue information
- [STATUS_ANA_CAN_INSTR2](#job-status-ana-can-instr2) - Read Analogue Input and Output States for LID 0D Read Instruments 2 analogue information
- [STATUS_ANA_AC_EVAP](#job-status-ana-ac-evap) - Read Analogue Input and Output States for LID 0F Read Instruments 2 analogue information - Air Conditioner Evaporator temperature
- [STATUS_ANA_ENGINE2](#job-status-ana-engine2) - Read Analogue Input and Output States for LID 11 Read Engine 2 analogue information
- [STATUS_ANA_ENGINE3](#job-status-ana-engine3) - Read Analogue Input and Output States for LID 12 Read Engine 3 analogue information
- [STATUS_ANA_ENGINE4](#job-status-ana-engine4) - Read Analogue Input and Output States for LID 13 Read Engine 4 analogue information
- [STATUS_ANA_ENGINE5](#job-status-ana-engine5) - Read Analogue Input and Output States for LID 14 Read Engine 5 analogue information
- [STATUS_ANA_O2_HEATER](#job-status-ana-o2-heater) - Read Analogue Input and Output States for LID 15 Read Engine 6 analogue infomation - oxygen  heaters
- [STATUS_ANA_ENGINE7](#job-status-ana-engine7) - Read Analogue Input and Output States for LID 16 Read Engine 7 analogue information
- [STATUS_ANA_FUEL_TRIM](#job-status-ana-fuel-trim) - Read Analogue Input and Output States for LID 17 Read Engine 8 analogue information - fuel trim
- [STATUS_ANA_ENGINE9](#job-status-ana-engine9) - Read Analogue Input and Output States for LID 18 Read Engine 9 analogue information
- [STATUS_ANA_INJ_TIME](#job-status-ana-inj-time) - Read Analogue Input and Output States for LID 19 Read Engine 10 analogue information - injection times
- [STATUS_ANA_EWS](#job-status-ana-ews) - Read Analogue Input and Output States for LID 20 Read Immobiliser information
- [STATUS_ANA_MAN_TEST](#job-status-ana-man-test) - Read Analogue Input and Output States for LID 21 Read Manufacturing Test information
- [STATUS_ANA_CVT2](#job-status-ana-cvt2) - Read Analogue Input and Output States for LID 23 Read Constant Velocity Transmission 2 analogue information
- [STATUS_ANA_CVT_RATIO_ADAPTION](#job-status-ana-cvt-ratio-adaption) - Read Analogue Input and Output States for LID 25 Read CVT ratio adaption information
- [STATUS_ANA_CVT_CLUTCH_ADAPTION](#job-status-ana-cvt-clutch-adaption) - Read Analogue Input and Output States for LID 26 Read CVT clutch adaption information
- [STATUS_ANA_BASE_ENGINE](#job-status-ana-base-engine) - Read Analogue Input and Output States for LID 27 Read Base Engine information
- [STATUS_ANA_OBD2](#job-status-ana-obd2) - Read Analogue Input and Output States for LID 28 Read OBD 2 information
- [STATUS_IO_CAN_ASC1](#job-status-io-can-asc1) - Read Digital Input States for LID 01 Read Anti Slip Control 1 digital information
- [STATUS_IO_DRIVING_STABILITY](#job-status-io-driving-stability) - Read Digital Input States for LID 03 Read Driving Stability control status
- [STATUS_IO_CAN_ASC4](#job-status-io-can-asc4) - Read Digital Input States for LID 04 Read Anti Slip Control 4 digital information
- [STATUS_ADAPTION_CVI](#job-status-adaption-cvi) - Read Digital Input States for LID 26 
- [STATUS_IO_CAN_DME1](#job-status-io-can-dme1) - Read Digital Input States for LID 05 Read Digital Motor Electronics 1 digital information
- [STATUS_IO_CAN_DME4](#job-status-io-can-dme4) - Read Digital Input States for LID 07 Read Digital Motor Electronics 4 digital information
- [STATUS_IO_WHEEL_TORQUE](#job-status-io-wheel-torque) - Read Digital Input States for LID 09 Read Digital Motor Electronics 6 digital information - torque
- [STATUS_IO_SHIFTING](#job-status-io-shifting) - Read Digital Input States for LID 0B Read State of Gear Shifting
- [STATUS_IO_CVT1](#job-status-io-cvt1) - Read Digital Input States for LID 0C Read Constant Vehicle Transmission 1 digital information
- [STATUS_IO_INSTR3](#job-status-io-instr3) - Read Digital Input States for LID 0E Read Instruments 3 digital information
- [STATUS_IO_ENGINE1](#job-status-io-engine1) - Read Digital Input States for LID 10 Read Engine 1 digital information
- [STATUS_IO_ENGINE2](#job-status-io-engine2) - Read Digital Input States for LID 11 Read Engine 2 digital information
- [STATUS_IO_EWS](#job-status-io-ews) - Read Digital Input States for LID 20 Read Immobiliser digital information
- [STATUS_IO_MAN_TEST](#job-status-io-man-test) - Read Digital Input States for LID 21 Read Manufacturing Test digital information
- [STATUS_IO_CRUISE](#job-status-io-cruise) - Read Digital Input States for LID 22 Read Cruise digital information
- [STATUS_IO_OIL_TEST_OK](#job-status-io-oil-test-ok) - Read Digital Input States for LID 23 Read whether it is OK to measure the oil level
- [STATUS_IO_READY_CODE](#job-status-io-ready-code) - Read Digital Input States for LID 24 Read Readiness code digital information
- [STATUS_IO_CVT_CLUTCH_ADAPTION](#job-status-io-cvt-clutch-adaption) - Read Digital Input States for LID 26 Read clutch adaption information
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Motordrehzahl Read the engine speed
- [STATUS_LL_SOLLDREHZAHL](#job-status-ll-solldrehzahl) - Solldrehzahl Leerlaufregler auslesen Read the target idle speed
- [STATUS_ZUENDWINKEL](#job-status-zuendwinkel) - Zuendwinkel Zyl1 Read the spark advance angle
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - Luftmasse Read the air mass
- [STATUS_EINSPRITZZEIT](#job-status-einspritzzeit) - Einspritzzeit EV1 Read the injection duration
- [STATUS_LAST](#job-status-last) - Lastsignal auslesen Read the calculated load value
- [STATUS_DKP_WINKEL](#job-status-dkp-winkel) - DK-Winkel Read the throttle angle
- [STATUS_SYSTEMCHECK_LAUFUNRUHE](#job-status-systemcheck-laufunruhe) - Laufunruhe lesen Read the engine roughness for each cylinder
- [STATUS_LS_VKAT_HEIZUNG_TV_1](#job-status-ls-vkat-heizung-tv-1) - norm. Heizleist. L-Sonde vKat1 Read the upstream oxygen  heater
- [STATUS_LS_NKAT_HEIZUNG_TV_1](#job-status-ls-nkat-heizung-tv-1) - norm. Heizleist. L-Sonde hKat1 Read the downstream oxygen  heater
- [STATUS_LS_VKAT_SIGNAL_1](#job-status-ls-vkat-signal-1) - Lambdasondenspannung v Kat Read the voltage of the upstream oxygen
- [STATUS_LS_NKAT_SIGNAL_1](#job-status-ls-nkat-signal-1) - Lambdasondenspannung n Kat Read the voltage of the downstream oxygen
- [STATUS_LAMBDA_INTEGRATOR_1](#job-status-lambda-integrator-1) - Lambdaregler1 Read the fuel control bank 1
- [STATUS_TE_TASTVERHAELTNIS](#job-status-te-tastverhaeltnis) - Tastverhaeltnis TEV Read solenoid valve, tank ventillation (purge cannister)
- [STATUS_MDK_POTI_SPANNUNG](#job-status-mdk-poti-spannung) - Potentiometer Motordrosselklappe auslesen Read the throttle potentiometer signals
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung) - Fahrerwunsch Read the pedal  signals
- [STATUS_PWG_WINKEL](#job-status-pwg-winkel) - PWG-Winkel auslesen Read the pedal  angle
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - Ansauglufttemperatur Read the air intake temperature
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Motortemperatur Read the engine coolant temperature
- [STATUS_UBATT](#job-status-ubatt) - Ubatt Read the battery voltage after relay
- [STATUS_GEBERRAD_ADAPTION](#job-status-geberrad-adaption) - Geberradadaption Read the crank  adaption (engine is synchonized switch)
- [STATUS_DIGITAL](#job-status-digital) - Status Schalteingaenge Read switches and I/O states
- [STATUS_LAMBDA_ADD_1](#job-status-lambda-add-1) - Gemischadaption additiv 1 Read adaption mixture additive bank 1
- [STATUS_LAMBDA_MUL_1](#job-status-lambda-mul-1) - Gemischadaption multipl. 1 Read adaption mixture multiplicative bank 1
- [STATUS_DIGITAL_OBDII](#job-status-digital-obdii) - Status Schalteingaenge Read OBD2 Readiness flags

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

<a id="job-start-diagnostic-session"></a>
### START_DIAGNOSTIC_SESSION

Begins a diagnostic session

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | Diagnostic mode: 0x81=Standard, 0x83=EOL, 0x86=Development 0x85=Programming at 9.6k, 0xFF=Programming at 62.5k |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-seed-key"></a>
### SEED_KEY

Obtain security access to the ECU Schutzmechanismus SEED_KEY

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | Security access mode Typ zugang 1 = breakdown, 3 = dealer, 5 = End of line 7 = programming, 9 = development |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Request seed response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Send key response |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ident-old"></a>
### IDENT_OLD

Ident-Daten fuer EMS2000

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_ORIG_BMW_NR | string | Urspruenglich BMW-Teilenummer Original BMW part number |
| ID_BMW_NR | string | Zurzeit BMW-Teilenummer Current BMW part number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_TAG | int | Herstelldatum tag Day of manufacture |
| ID_DATUM_MON | int | Herstelldatum monat Month of manufacture |
| ID_DATUM_JAHR_4_CHAR | int | Herstelldatum Jahr Year of manufacture |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) Is AIF data available 0=no 1=yes |
| ID_LAMBDA_STEREO | int | Parameter fuer MoTest 0=Mono, 1=STEREO Single or dual oxygen sensors |
| ID_EML | int | Parameter fuer MoTest 0=Kein EML verb, 1=EML M70, 2=EML M73 |
| ID_LU_MESSUNG | int | Parameter fuer MoTest 1=Laufunruhemessung, sonst 0 |
| ID_OBD2 | int | Parameter fuer MoTest 0=ECE, 1=OBD2-Fahrzeug |
| ID_SG_HERSTELLER | int | Parameter fuer MoTest 0=Bosch, 1=Siemens-Fahrzeug |
| ID_MOTOR | string | Parameter fuer MoTest Motorkennung |
| ID_SW_NR | string | Part of Siemens ECU software number |
| ID_AI_NR | string | Part of Siemens ECU software number |
| ID_PROD_NR | string | Siemens logistic information - Serial number |
| ID_CONFIG_BYTES | binary | Configuration Bytes |
| ID_HW_REF | binary | ID_HW_REF |
| ID_PROGRAMM_REF | binary | ID_PROGRAMM_REF |
| ID_DATEN_REF | binary | ID_DATEN_REF |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response for start diagnostic session |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response for request seed |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG ECU response for send key |
| _TEL_ANTWORT4 | binary | Hex-Antwort von SG ECU response for read ident |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer EMS2000

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_ORIG_BMW_NR | string | Urspruenglich BMW-Teilenummer Original BMW part number |
| ID_BMW_NR | string | Zurzeit BMW-Teilenummer Current BMW part number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_TAG | int | Herstelldatum tag Day of manufacture |
| ID_DATUM_MON | int | Herstelldatum monat Month of manufacture |
| ID_DATUM_JAHR_4_CHAR | int | Herstelldatum Jahr Year of manufacture |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) Is AIF data available 0=no 1=yes |
| ID_LAMBDA_STEREO | int | Parameter fuer MoTest 0=Mono, 1=STEREO Single or dual oxygen sensors |
| ID_EML | int | Parameter fuer MoTest 0=Kein EML verb, 1=EML M70, 2=EML M73 |
| ID_LU_MESSUNG | int | Parameter fuer MoTest 1=Laufunruhemessung, sonst 0 |
| ID_OBD2 | int | Parameter fuer MoTest 0=ECE, 1=OBD2-Fahrzeug |
| ID_SG_HERSTELLER | int | Parameter fuer MoTest 0=Bosch, 1=Siemens-Fahrzeug |
| ID_MOTOR | string | Parameter fuer MoTest Motorkennung |
| ID_SW_NR | string | Part of Siemens ECU software number |
| ID_AI_NR | string | Part of Siemens ECU software number |
| ID_PROD_NR | string | Siemens logistic information - Serial number |
| ID_CONFIG_BYTES | binary | Configuration Bytes |
| ID_HW_REF | binary | ID_HW_REF |
| ID_PROGRAMM_REF | binary | ID_PROGRAMM_REF |
| ID_DATEN_REF | binary | ID_DATEN_REF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response for read ident |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ident-coding"></a>
### IDENT_CODING

Ident-Daten fuer EMS2000

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_ORIG_BMW_NR | string | Urspruenglich BMW-Teilenummer Original BMW part number |
| ID_BMW_NR | string | Zurzeit BMW-Teilenummer Current BMW part number |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_TAG | int | Herstelldatum tag Day of manufacture |
| ID_DATUM_MON | int | Herstelldatum monat Month of manufacture |
| ID_DATUM_JAHR_4_CHAR | int | Herstelldatum Jahr Year of manufacture |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer Supplier code |
| ID_LIEF_TEXT | string | Lieferanten-Text Supplier Name |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) Is AIF data available 0=no 1=yes |
| ID_LAMBDA_STEREO | int | Parameter fuer MoTest 0=Mono, 1=STEREO Single or dual oxygen sensors |
| ID_EML | int | Parameter fuer MoTest 0=Kein EML verb, 1=EML M70, 2=EML M73 |
| ID_LU_MESSUNG | int | Parameter fuer MoTest 1=Laufunruhemessung, sonst 0 |
| ID_OBD2 | int | Parameter fuer MoTest 0=ECE, 1=OBD2-Fahrzeug |
| ID_SG_HERSTELLER | int | Parameter fuer MoTest 0=Bosch, 1=Siemens-Fahrzeug |
| ID_MOTOR | string | Parameter fuer MoTest Motorkennung |
| ID_SW_NR | string | Part of Siemens ECU software number |
| ID_AI_NR | string | Part of Siemens ECU software number |
| ID_PROD_NR | string | Siemens logistic information - Serial number |
| ID_CONFIG_BYTES | binary | Configuration Bytes |
| ID_HW_REF | binary | ID_HW_REF |
| ID_PROGRAMM_REF | binary | ID_PROGRAMM_REF |
| ID_DATEN_REF | binary | ID_DATEN_REF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response for read ident |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ident-extended"></a>
### IDENT_EXTENDED

Read additional ECU Ident information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_SIEMENS_PRODUCT | string | Siemens logistic information - Product ID |
| ID_SIEMENS_SERIAL_NR | string | Siemens logistic information - Serial number |
| ID_SIEMENS_TEST_DATE | string | Siemens logistic information - Date of final test |
| ID_SUB_SYSTEM_BOOT_SW_NR | string | Sub-system Boot software number |
| ID_SUB_SYSTEM_ECU_SW_NR | string | Sub-system ECU software number |
| ID_SUB_SYSTEM_CALIB_NR | string | Sub-system calibration number |
| ID_SIEMENS_ECU_SW_NR | string | Siemens ECU software number |
| ID_SYSTEM_NAME | int | System name |
| ID_ECU_SW_NR | long | ECU Software number |
| ID_TUNE_PART_NR | long | Tune part number |
| ID_SW_NR | string | Part of Siemens ECU software number |
| ID_AI_NR | string | Part of Siemens ECU software number |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ident-aif"></a>
### IDENT_AIF

Ident und AIF zusammen lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_SW_NR | string | Softwarenummer |
| ID_AI_NR | string | Aenderungsindex |
| ID_PROD_NR | string | Produktionsnummer |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_SW_NR | string | Softwarenummer |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_ZB_NR | string | Zusbaunummer |
| AIF_PROGG_NR | string | Programmiergeraet Seriennummer |
| AIF_WERKSCODE | string | Haendlernummer (Werkscode) |
| AIF_KM_STAND | string | km-Stand |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG ECU response packet |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Tester present message

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden Stop the diagnostic session

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-sg-reset"></a>
### SG_RESET

Reset the ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORTB | binary | Hex-Antwort von SG ECU response packet - last response Only received if first ECU response was "response pending" |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-stat-freezeframe"></a>
### STAT_FREEZEFRAME

Read the freeze frame data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DTC | int | Diagnostic trouble code See "ORT" column in table "FOrtTexte" Fehler ort nummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FTL_WERT | real | Fuel tank level |
| STAT_FTL_EINH | string |  |
| STAT_OBD_TPS_WERT | real | Throttle opening |
| STAT_OBD_TPS_EINH | string |  |
| STAT_OBD_PV_AV_WERT | real | Driver demand |
| STAT_OBD_PV_AV_EINH | string |  |
| STAT_VB_RLY_WERT | real | Battery voltage |
| STAT_VB_RLY_EINH | string |  |
| STAT_LV_CAN_TQ_STATE | int | ABS/ASC Activity Status |
| STAT_LV_VS_ERR | int | Vehicle speed error status |
| STAT_LV_ACCOUT_RLY | int | Air conditioner status |
| STAT_LV_DRI | int | Gear status 1 = Drive position selected, 0 = not selected |
| STAT_OBD_MAP_UP_WERT | real | Upstream manifold pressure |
| STAT_OBD_MAP_UP_EINH | string |  |
| STAT_CMD_TYPE_WERT | real | Gearbox oil temperature |
| STAT_CMD_TYPE_EINH | string |  |
| STAT_OBD_TIA_WERT | real | Inlet air temperature |
| STAT_OBD_TIA_EINH | string |  |
| STAT_DIST_FAIL_WERT | real | Covered distance when the failure occured |
| STAT_DIST_FAIL_EINH | string |  |
| STAT_STATE_LS1_WERT | real | Status of Fuel system 1 |
| STAT_STATE_LS1_EINH | string |  |
| STAT_LOAD_CLC_WERT | real | Calculated load |
| STAT_LOAD_CLC_EINH | string |  |
| STAT_OBD_TCO_WERT | real | Engine coolant temperature |
| STAT_OBD_TCO_EINH | string |  |
| STAT_TI_LAM_1_WERT | real | Short term fuel trim bank 1 |
| STAT_TI_LAM_1_EINH | string |  |
| STAT_FUEL_AD_MMV_REL_1_WERT | real | Long term fuel trim bank 1 |
| STAT_FUEL_AD_MMV_REL_1_EINH | string |  |
| STAT_OBD_MAP_WERT | real | Intake manifold absolute pressure |
| STAT_OBD_MAP_EINH | string |  |
| STAT_N_WERT | real | Engine speed |
| STAT_N_EINH | string |  |
| STAT_VS_WERT | real | Vehicle speed |
| STAT_VS_EINH | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-fs-lesen"></a>
### FS_LESEN

Read all faults

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_HEX_CODE | binary | Hexdump des Fehlersatzes Raw fault data from the ECU |
| F_ORT_NR | int | Fehlercode des SG als Index Fault number as an integer |
| F_ORT_TEXT | string | Fehlercode des SG als Text Fault description |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers Frequency counter |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers Count of Environment Data Items per fault |
| F_ART_ANZ | int | Anzahl der Fehlerarten des SG Count of additional fault status information |
| F_ART1_NR | int | Fehlerart 1 Index Fault status 1 |
| F_ART1_TEXT | string | Fehlerart 1 Text Fault status text 1 |
| F_ART2_NR | int | Fehlerart 2 Index Fault status 2 |
| F_ART2_TEXT | string | Fehlerart 2 Text Fault status text 2 |
| F_ART3_NR | int | Fehlerart 3 Index Fault status 3 |
| F_ART3_TEXT | string | Fehlerart 3 Text Fault status text 3 |
| F_ART4_NR | int | Fehlerart 4 Index Fault status 4 |
| F_ART4_TEXT | string | Fehlerart 4 Text Fault status text 4 |
| F_ART5_NR | int | Fehlerart 5 Index Fault status 5 |
| F_ART5_TEXT | string | Fehlerart 5 Text Fault status text 5 |
| F_ART6_NR | int | Fehlerart 6 Index Fault status 6 |
| F_ART6_TEXT | string | Fehlerart 6 Text Fault status text 6 |
| F_ART7_NR | int | Fehlerart 7 Index Fault status 7 |
| F_ART7_TEXT | string | Fehlerart 7 Text Fault status text 7 |
| F_ART8_NR | int | Fehlerart 8 Index Fault status 8 |
| F_ART8_TEXT | string | Fehlerart 8 Text Fault status text 8 |
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
| F_UW5_NR | int | Umweltbedingung 5 Index Fifth Environment Result Index |
| F_UW5_TEXT | string | Umweltbedingung 5 Text Fifth Environment Result Description |
| F_UW5_WERT | real | Umweltbedingung 5 Wert Fifth Environment Result Value |
| F_UW5_EINH | string | Umweltbedingung 5 Einheit Fifth Environment Result Units |
| F_LZ1 | int | Anti bounce counter |
| F_LZ2 | int | Warmreihezaehler Warm up cycle counter |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read quick fault memory response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read full fault memory response |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG Read freezeframe response |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Clears All Faults

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORTB | binary | Hex-Antwort von SG ECU response packet - last response Only received if first ECU response was "response pending" |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-read-memory"></a>
### READ_MEMORY

Read ECU Memory by Address Speicher lesen mit Adresse

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MEM_ADDRESS | long | 24 bit ECU memory address addresse speicher SG 0xF600 -&gt; 0xFDFF (IRAM) 0xE000 -&gt; 0xE7FF (XRAM) 0x4000 -&gt; 0x7FFF (EEPROM) 0xC000 -&gt; 0xDFFF (EXRAM) 0x70000 -&gt; 0xEFFFF (FLASH) |
| MEM_LENGTH | int | Length of memory to be read (1 - 254) Umfang speicher lesen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MEM_DATA | binary | ECU memory which is read SG speicher data |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-write-memory"></a>
### WRITE_MEMORY

Write data to a specified memory address Speicher schreiben mit Adresse

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADDRESS | long | 24 bit ECU memory address addresse speicher SG 0xF600 -&gt; 0xFDFF (IRAM) 0xE000 -&gt; 0xE7FF (XRAM) 0xC000 -&gt; 0xDFFF (EXRAM) |
| LENGTH | int | Length of memory to write (1 -&gt; 250) Umfang speicher schreiben |
| MEMDATA | string | Data to write Data format hex: 0xXX 0xXX ... 0xXX Data format decimal: d d ... d Data format binary: 0ybbbbbbbb 0ybbbbbbbb ... 0ybbbbbbbb |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORTB | binary | Hex-Antwort von SG ECU response packet - last response Only received if first ECU response was "response pending" |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-access-timing-parameters"></a>
### ACCESS_TIMING_PARAMETERS

Read the comms timing parameters Kommunikationsparameter lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| P2_MIN | unsigned int | Minimum time between tester request and ECU response Timeout-Zeit minimum |
| P2_MAX | unsigned int | Maximum time between tester request and ECU response Timeout-Zeit maximum |
| P3_MIN | unsigned int | Minimum time between ECU response and tester request Regenerations-Zeit minimum |
| P3_MAX | unsigned int | Maximum time between ECU response and tester request Regenerations-Zeit maximum |
| P4_MIN | unsigned int | Minimum inter byte time for tester request Byte-Zwischenzeit minumum |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-change-timing-parameters"></a>
### CHANGE_TIMING_PARAMETERS

Set timing parameters for standard or programming mode Diagnosetimeout aendern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | Set timing parameters mode 0 = set timing parameters to standard mode 1 = set timing parameters to programming mode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORTB | binary | Hex-Antwort von SG ECU response packet - last response Only received if first ECU response was "response pending" |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-code-loeschen"></a>
### CODE_LOESCHEN

Erase the software code and calibration data within flash Das kalibrabrierung daten und software schluessel in flash loeshen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORTB | binary | Hex-Antwort von SG ECU response packet - last response Only received if first ECU response was "response pending" |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-data-loeschen"></a>
### DATA_LOESCHEN

Erase the calibration data within flash Das kalibrabrierung daten in flash loeshen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORTB | binary | Hex-Antwort von SG ECU response packet - last response Only received if first ECU response was "response pending" |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-check-reprog-depending"></a>
### CHECK_REPROG_DEPENDING

Calculate the checksum and check the coherence system

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-report-reprog-status"></a>
### REPORT_REPROG_STATUS

Get the status of reprogramming after a mistake Programmieren status nach fehler auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| REPROG_STATUS | unsigned int | Reprogramming status Bit0: reference error boot software - if error than flag = TRUE Bit1: reference error ECU software - if error than flag = TRUE Bit2: reference calibration data - if error than flag = TRUE Bit3: ECU software does not fit to boot software - if error than flag = TRUE Bit4: calibration data does not fit to ECU software - if error than flag = TRUE Bit5: system references fit together - if OK then flag = TRUE Bit6: ECU locked (seed_key procedure is missing) - if ECU locked then flag = TRUE Bit7: ECU configuration is OK - if OK then flag = TRUE Bit8: ECU software is OK - if OK then flag = TRUE Bit9: ECU software security key is OK - if OK then flag = TRUE Bit10: ECU software security key is not written - if error then flag = TRUE Bit11: checksum ECU software is OK - if OK then flag = TRUE Bit12: calibration data is OK - if OK then flag = TRUE Bit13: calibration data security key is OK - if OK then flag = TRUE Bit14: calibration data security key is not written - if not written then flag = TRUE Bit15: checksum calibration data is OK - if OK then flag = TRUE |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-learn-imob-seed"></a>
### LEARN_IMOB_SEED

The ECM learns the immobolisation seed

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORTB | binary | Hex-Antwort von SG ECU response packet - last response Only received if first ECU response was "response pending" |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-resync-imob-seed"></a>
### RESYNC_IMOB_SEED

The ECM resynchronises the immobolisation seed

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORTB | binary | Hex-Antwort von SG ECU response packet - last response Only received if first ECU response was "response pending" |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

Stop the power latch phase

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JUNK | unsigned char | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-start-man-test"></a>
### START_MAN_TEST

Start the end of line test Hersteller test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-start-cat-test"></a>
### START_CAT_TEST

Start catalyst test Katalysator test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-gib-self-test"></a>
### GIB_SELF_TEST

Run the Gearbox Interface Box self test routine Getriebe Interface test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ldp-test"></a>
### LDP_TEST

Run the Leak Detection Pump test Leckdiagnosepumpen test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-execute-ram-routine"></a>
### EXECUTE_RAM_ROUTINE

Start a routine which is stored within RAM (MTOS)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORTB | binary | Hex-Antwort von SG ECU response packet - last response Only received if first ECU response was "response pending" |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-switch-to-boot"></a>
### SWITCH_TO_BOOT

Allow activation of the boot software mode Needed for programming

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORTB | binary | Hex-Antwort von SG ECU response packet - last response Only received if first ECU response was "response pending" |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-swnr-schreiben"></a>
### SWNR_SCHREIBEN

Write the Software number

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SWNR | string | Software number - 8 characters |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write Software number telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write Software number response |
| _TEL_ANTWORT1B | binary | Hex-Antwort von SG Write Software number last response Only received if first ECU response was "response pending" |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read Software number response |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-tune-nr-schreiben"></a>
### TUNE_NR_SCHREIBEN

Write the tune part number

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TUNE_NR | string | Tune part number - 8 characters |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write tune telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write tune response |
| _TEL_ANTWORT1B | binary | Hex-Antwort von SG Write tune last response Only received if first ECU response was "response pending" |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read tune response |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-flash-schreiben-adresse"></a>
### FLASH_SCHREIBEN_ADRESSE

Request download

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | long | 24 bit ECU memory address Addresse speicher SG 0x108000 -&gt; 0x13FFFF (FLASH) |
| SIZE | long | Uncompressed memory size 0x000000 -&gt; 0xFFFFFF Speicher umfang |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Transfer data to the ECU

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATA | binary | Data to transfer to the ECU (250 bytes) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| _TEL_ANTWORTB | binary | Hex-Antwort von SG ECU response packet - last response Only received if first ECU response was "response pending" |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Exit data transfer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

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
| AIF_SW_NR | string | Softwarenummer |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_ZB_NR | string | Zusammenbaunummer |
| AIF_PROGG_NR | string | Seriennummer |
| AIF_WERKSCODE | string | Haendlernummer |
| AIF_KM_STAND | string | Kilometerstand |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |

<a id="job-aif-schreiben"></a>
### AIF_SCHREIBEN

Write the AIF record

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Fahrgestellnummer VIN - 17 or 18 characters - if 18 the last character is ignored |
| AIF_DATUM | string | Fertigungsdatum Programming date - 6 characters |
| AIF_ZB_NR | string | Zusbaunummer Assembly number - 14 characters |
| AIF_BEHOERDEN_NR | long | Behoerdennummer Homologation test number |
| AIF_PROGG_NR | string | Programming unit serial number - 12 characters |
| AIF_WERKSCODE | string | Plant / Workshop number (Dealer number) - 6 characters |
| AIF_KM_STAND | long | km-Stand (0 -&gt; 655350) |
| AIF_PROG_STATUS | string | Program Status - 8 characters |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write AIF telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write AIF response |
| _TEL_ANTWORT1B | binary | Hex-Antwort von SG Write AIF last response Only received if first ECU response was "response pending" |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read AIF response |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen der Fahrgestellnummer aus dem Anwenderinfofeld Read the VIN from the current AIF record

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer VIN |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Schreiben der 17-stelligen Fahrgestellnummer in dem Anwenderinfofeld Write the VIN into the AIF record

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer VIN Either 17 or 18 characters - if 18 the last character is ignored |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read existing AIF response |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write new AIF Telegram to ECU |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Write new AIF response |
| _TEL_ANTWORT2B | binary | Hex-Antwort von SG Write new AIF last response Only received if first ECU response was "response pending" |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG Read new AIF response |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-zcs-lesen"></a>
### C_ZCS_LESEN

Read the ZCS record

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos + 1 ASCII c/sum) Basic features |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos + 1 ASCII c/sum) Particular equipment |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos + 1 ASCII c/sum) Version information |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-zcs-auftrag"></a>
### C_ZCS_AUFTRAG

Write and verify the Central code

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos + 1 ASCII c/sum) Basic features |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos + 1 ASCII c/sum) Particular equipment |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos + 1 ASCII c/sum) Version information |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write ZCS telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write ZCS response |
| _TEL_ANTWORT1B | binary | Hex-Antwort von SG Write ZCS last response Only received if first ECU response was "response pending" |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read ZCS response |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-azcs-lesen"></a>
### C_AZCS_LESEN

Read the auxiliary ZCS record

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos + 1 ASCII c/sum) Basic features |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos + 1 ASCII c/sum) Particular equipment |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos + 1 ASCII c/sum) Version information |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-azcs-auftrag"></a>
### C_AZCS_AUFTRAG

Write and verify the Auxiliary Central code

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GM | string | Zentralcode C1 - Grundmerkmal (8 ASCII nos + 1 ASCII c/sum) |
| SA | string | Zentralcode C2 - Sonderausstattung (16 ASCII nos + 1 ASCII c/sum) |
| VN | string | Zentralcode C3 - Versionsmerkmal (10 ASCII nos + 1 ASCII c/sum) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write AZCS telegram sent to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write AZCS response |
| _TEL_ANTWORT1B | binary | Hex-Antwort von SG Write AZCS last response Only received if first ECU response was "response pending" |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read AZCS response |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Byte 0:               01=Daten 02=Maskenbyte (nicht unterstuetzt) Byte 1:               Wortbreite (0:Byte, 2:Word, 3:DW Byte 2:               Byteordnung (0:LSB zuerst, 1 MSB Byte 3:               Adressierung (0: freie Adressier Byte 4:               Byteparameter 1 Byte 5,6:             WordParameter 1 (low/high) Byte 7,8:             WordParameter 2 (low/high) Byte 9,10,11,12:      Maske (linksbuendig) Byte 13,14:           Anzahl Bytedaten (low/high) Byte 15,16:           Anzahl Wortdaten (low/high) Byte 17:              Byteadresse im Block Byte 18,19,20:        Blockadresse (low, middle, high) Byte 21,....:         Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren Write and verify coding data

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Byte 0:               01=Daten 02=Maskenbyte (nicht unterstuetzt) Byte 1:               Wortbreite (0:Byte, 2:Word, 3:DW Byte 2:               Byteordnung (0:LSB zuerst, 1 MSB Byte 3:               Adressierung (0: freie Adressier Byte 4:               Byteparameter 1 Byte 5,6:             WordParameter 1 (low/high) Byte 7,8:             WordParameter 2 (low/high) Byte 9,10,11,12:      Maske (linksbuendig) Byte 13,14:           Anzahl Bytedaten (low/high) Byte 15,16:           Anzahl Wortdaten (low/high) Byte 17:              Byteadresse im Block Byte 18,19,20:        Blockadresse (low, middle, high) Byte 21,....:         Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write coding data telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write coding data response |
| _TEL_ANTWORT1B | binary | Hex-Antwort von SG Write coding data last response Only received if first ECU response was "response pending" |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read coding data response |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-c-checksum"></a>
### C_CHECKSUM

Berechnung und Speicherung der Checksumme

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CHECKSUM | unsigned char | berechnete Checksumme calculated checksum |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-config-bytes-lesen"></a>
### CONFIG_BYTES_LESEN

Read the Configuraton Bytes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG Read config response |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| MARKET_CONFIG | int | Market Configuration EU4 = 00, LEV = 01, Japan = 10, EU3 = 11 |
| LEADED_FUEL | int | Leaded fuel Unleaded = 0, Leaded = 1 |
| CRUISE | int | Cruise control Not fitted = 0, Fitted = 1 |
| AIRCON | int | Air Conditioning Not fitted = 0, Fitted = 1 |
| AIRCON_DISABLE_PVS | int | Aircon disable based on PVS Enabled = 0, Disabled = 1 |
| COOLING_FAN_CONFIG | int | Cooling Fan Configuration 1 fan speed = 00, 2 fan speeds = 01, 3 fan speeds = 10 |
| ENGINE_TYPE | int | Engine type 68kw = 00, 85kw = 01, 115kw = 10 |
| TRANSMISSION | int | Transmission R65 = 00, Getrag = 01, CVT = 10, CVT with steptronic = 11 |
| MIL_ACTIVATION | int | MIL Activation MIL active = 0, No MIL active = 1 Only applicable when diagnostic index &gt; 0x31 |
| ASR_MSR_DSC | int | TCS configuration For diagnostic index &lt;= 0x31 ABS only = 0, ASR/MSR = 3 For diagnostic index &gt; 0x31 ABS only = 0, ASR/MSR = 1 |
| CVT_HYBRID_MODE | int | CVT Hybrid Mode Normal CVT mode = 0, Hybrid mode = 1 |
| ALTERNATOR_TYPE | int | Alternator type Denso 105A = 0, Valeo 120A = 1 Only applicable when diagnostic index &gt; 0x31 |
| CVT_SHIFT_INTERLOCK | int | Const velocity transmission shift interlock Shift interlock not fitted = 0, Shift interlock fitted = 1 Only applicable when diagnostic index &lt;= 0x31 |
| CHECKSUM | int | Checksum configuration |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Pruefcode-Daten in Hex auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| PRUEFCODE | binary | Daten in Hex-Format |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read Ident response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read AIF response |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG Read Quick Faults response |

<a id="job-steuern-actuator"></a>
### STEUERN_ACTUATOR

Actuator test

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAME | string | Name of the Actuator test to perform From the "NAME" column of the table "Actuator_test" MAIN_RELAY FUEL_PUMP AC_COMPRESSOR FAN_RELAY_HIGH FAN_RELAY_MED FAN_RELAY_LOW CANISTER_PURGE THROTTLE_ACT LEAK_DETECTION PRIME_FUEL CVT_SHIFT_LOCK INJECTOR_1 INJECTOR_2 INJECTOR_3 INJECTOR_4 UPSTR_O2_HEAT DWSTR_O2_HEAT DISABLE_ACTS |
| CONTROL | int | Control option 0=return control to ECU, 1=report current status, 7=short term adjustments |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| CURRENT_STATUS | int | Control state 0=Activating done, 255=Activating in progress |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-application-correction"></a>
### STEUERN_APPLICATION_CORRECTION

Application correction. Non volatile adjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAME | string | Name of the Application correction to make From the "NAME" column of the table "Applic_Correction" IDLE_CO_TRIM IDLE_TEMP_CORR IDLE_DUR_CORR |
| CONTROL | int | Control option 0=return control to ECU, 1=report current status 7=short term adjustments, 8=long term adjustments |
| STATE | int | only used when control option is short term adjustments 0=decrease short term adjustment, 1=increase short term adjustments |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TI_AD_ADD_MMV_0_WERT | real | Long term additive fuel trim |
| STAT_TI_AD_ADD_MMV_0_EINH | string |  |
| STAT_N_SP_IS_WERT | real | Idle speed at set point |
| STAT_N_SP_IS_EINH | string |  |
| STAT_N_SP_ADD_KWP_LTA_WERT | real | Long term additive fuel trim value used in setting idle speed |
| STAT_N_SP_ADD_KWP_LTA_EINH | string |  |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-adaptive-values"></a>
### STEUERN_ADAPTIVE_VALUES

Reset adaptive values

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAME | string | Name of the Adaptive value to reset From the "NAME" column of the table "Adaptive_Values" ALL_VALUES MAP KNOCK_CONTROL ECT_THROTTLE CVT LAMBDA MISFIRING IDLE_SPEED DYNAMIC_TRIM KNOCK_SPARK_ADV CVT_DIST |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Telegram sent to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet table JobResult STATUS_TEXT |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-ana-wheel-speed"></a>
### STATUS_ANA_WHEEL_SPEED

Read Analogue Input and Output States for LID 02 Read Anti Slip Control 2 analogue information (wheel speeds)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_VRD_LV_ASC_WERT | real | Left front wheel speed |
| STAT_CAN_VRD_LV_ASC_EINH | string |  |
| STAT_CAN_VRD_RV_ASC_WERT | real | Right front wheel speed |
| STAT_CAN_VRD_RV_ASC_EINH | string |  |

<a id="job-status-ana-can-asc4"></a>
### STATUS_ANA_CAN_ASC4

Read Analogue Input and Output States for LID 04 Read Anti Slip Control 4 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_RR_WERT | real | Wheel acceleration signal |
| STAT_CAN_RR_EINH | string |  |
| STAT_CAN_TQI_TW_ASR_WERT | real | Absolute torque at wheels decrease request |
| STAT_CAN_TQI_TW_ASR_EINH | string |  |
| STAT_CAN_TQI_TW_MSR_WERT | real | Absolute torque at wheels increase request |
| STAT_CAN_TQI_TW_MSR_EINH | string |  |

<a id="job-status-ana-can-dme1"></a>
### STATUS_ANA_CAN_DME1

Read Analogue Input and Output States for LID 05 Read Digital Motor Electronics 1 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_N_WERT | real | Engine speed |
| STAT_CAN_N_EINH | string |  |

<a id="job-status-ana-can-dme2"></a>
### STATUS_ANA_CAN_DME2

Read Analogue Input and Output States for LID 06 Read Digital Motor Electronics 2 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_MUL_INFO_WERT | real | Multiplexed information |
| STAT_CAN_MUL_INFO_EINH | string |  |
| STAT_CAN_MUL_COD_WERT | real | Identifier for multiplexed information |
| STAT_CAN_MUL_COD_EINH | string |  |
| STAT_CAN_TCO_WERT | real | Coolant temperature |
| STAT_CAN_TCO_EINH | string |  |
| STAT_CAN_PV_AV_WERT | real | Demand driver |
| STAT_CAN_PV_AV_EINH | string |  |
| STAT_CAN_CRU_SET_LAMP_WERT | real | Cruise control set lamp |
| STAT_CAN_CRU_SET_LAMP_EINH | string |  |

<a id="job-status-ana-fuel-cons"></a>
### STATUS_ANA_FUEL_CONS

Read Analogue Input and Output States for LID 07 Read Digital Motor Electronics 4 analogue information - Fuel Consumption

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_TI_SUM_FCO_WERT | real | Fuel consumption |
| STAT_TI_SUM_FCO_EINH | string |  |

<a id="job-status-ana-can-dme5"></a>
### STATUS_ANA_CAN_DME5

Read Analogue Input and Output States for LID 08 Read Digital Motor Electronics 5 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_DES_AIM_POSITION_WERT | real | Desired motor position |
| STAT_CAN_DES_AIM_POSITION_EINH | string |  |
| STAT_CAN_DES_CMD_TYPE_WERT | real | Motor special codes |
| STAT_CAN_DES_CMD_TYPE_EINH | string |  |
| STAT_CAN_DES_AIM_SPEED_WERT | real | Desired motor speed |
| STAT_CAN_DES_AIM_SPEED_EINH | string |  |
| STAT_CAN_DES_CLU_SOL_DR_WERT | real | Target clutch duty ratio |
| STAT_CAN_DES_CLU_SOL_DR_EINH | string |  |
| STAT_CAN_CLUTCH_CODES_WERT | real | Clutch special codes |
| STAT_CAN_CLUTCH_CODES_EINH | string |  |
| STAT_CAN_DES_SDRY_PRES_DR_WERT | real | Target secondary pressure duty ratio |
| STAT_CAN_DES_SDRY_PRES_DR_EINH | string |  |
| STAT_CAN_SDRY_PRES_CODES_WERT | real | Secondary pressure duty codes |
| STAT_CAN_SDRY_PRES_CODES_EINH | string |  |
| STAT_CAN_MAP_WERT | real | Manifold gauge pressure |
| STAT_CAN_MAP_EINH | string |  |

<a id="job-status-ana-wheel-torque"></a>
### STATUS_ANA_WHEEL_TORQUE

Read Analogue Input and Output States for LID 09 Read Digital Motor Electronics 6 analogue information (wheel torques)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_TQ_AT_WHEELS_WOUT_LOSS_WERT | real | Indicated actual torque at wheels |
| STAT_CAN_TQ_AT_WHEELS_WOUT_LOSS_EINH | string |  |
| STAT_CAN_TW_NORM_WERT | real | Maximum absolute torque at wheels |
| STAT_CAN_TW_NORM_EINH | string |  |
| STAT_CAN_TW_TQ_LOSS_WERT | real | Torque losses at wheels |
| STAT_CAN_TW_TQ_LOSS_EINH | string |  |
| STAT_CAN_TW_TQI_REQ_TRA_WERT | real | Torque requested at wheels |
| STAT_CAN_TW_TQI_REQ_TRA_EINH | string |  |

<a id="job-status-ana-can-egs1"></a>
### STATUS_ANA_CAN_EGS1

Read Analogue Input and Output States for LID 0B Read Electonic Gear Selector 1 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_GR_AT_WERT | real | Current gear |
| STAT_CAN_GR_AT_EINH | string |  |
| STAT_CAN_L_GS_WERT | real | Emergency programt status |
| STAT_CAN_L_GS_EINH | string |  |
| STAT_CAN_GR_AT_SEL_WERT | real | Gear selector position |
| STAT_CAN_GR_AT_SEL_EINH | string |  |
| STAT_CAN_GR_MOD_WERT | real | Gear shift mode |
| STAT_CAN_GR_MOD_EINH | string |  |

<a id="job-status-ana-cvt1"></a>
### STATUS_ANA_CVT1

Read Analogue Input and Output States for LID 0C Read Constant Velocity Transmission 1 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_CURRENT_POSITION_WERT | real | Actual motor position |
| STAT_CAN_CURRENT_POSITION_EINH | string |  |
| STAT_CAN_MOTOR_CDN_COD_WERT | real | Motor condition codes |
| STAT_CAN_MOTOR_CDN_COD_EINH | string |  |
| STAT_CAN_DRIV_LED_STATUS_WERT | real | PRNDM LED drives status |
| STAT_CAN_DRIV_LED_STATUS_EINH | string |  |
| STAT_CAN_CLU_AV_DR_WERT | real | Actual clutch duty ratio |
| STAT_CAN_CLU_AV_DR_EINH | string |  |
| STAT_CAN_CLU_CDN_COD_WERT | real | Clutch condition codes |
| STAT_CAN_CLU_CDN_COD_EINH | string |  |
| STAT_CAN_DRIV_LED_ERR_WERT | real | PRNDM LED fault status |
| STAT_CAN_DRIV_LED_ERR_EINH | string |  |
| STAT_CAN_SDRY_PRS_AV_DR_WERT | real | Actual secondary pressure duty ratio |
| STAT_CAN_SDRY_PRS_AV_DR_EINH | string |  |
| STAT_CAN_SDRY_PRS_CDN_COD_WERT | real | Secondary pressure condition codes |
| STAT_CAN_SDRY_PRS_CDN_COD_EINH | string |  |
| STAT_CAN_GIB_SW_NR_WERT | real | Software number |
| STAT_CAN_GIB_SW_NR_EINH | string |  |

<a id="job-status-ana-can-instr2"></a>
### STATUS_ANA_CAN_INSTR2

Read Analogue Input and Output States for LID 0D Read Instruments 2 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_DIST_WERT | real | Distance |
| STAT_CAN_DIST_EINH | string |  |
| STAT_CAN_FTL_WERT | real | Fuel tank level |
| STAT_CAN_FTL_EINH | string |  |

<a id="job-status-ana-ac-evap"></a>
### STATUS_ANA_AC_EVAP

Read Analogue Input and Output States for LID 0F Read Instruments 2 analogue information - Air Conditioner Evaporator temperature

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_AC_TEMP_WERT | real | A/C Evaporator temperature |
| STAT_CAN_AC_TEMP_EINH | string |  |

<a id="job-status-ana-engine2"></a>
### STATUS_ANA_ENGINE2

Read Analogue Input and Output States for LID 11 Read Engine 2 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_STATE_CP_WERT | real | State variable for canister purge |
| STAT_STATE_CP_EINH | string |  |
| STAT_ALTER_WERT | real | Alternator load |
| STAT_ALTER_EINH | string |  |

<a id="job-status-ana-engine3"></a>
### STATUS_ANA_ENGINE3

Read Analogue Input and Output States for LID 12 Read Engine 3 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_TCO_BAS_WERT | real | Raw engine coolant temperature |
| STAT_TCO_BAS_EINH | string |  |
| STAT_TIA_BAS_WERT | real | Raw inlet air temperature voltage |
| STAT_TIA_BAS_EINH | string |  |
| STAT_MAP_BAS_WERT | real | Raw manifold air pressure |
| STAT_MAP_BAS_EINH | string |  |
| STAT_MAP_UP_BAS_WERT | real | Raw upstream manifold air pressure |
| STAT_MAP_UP_BAS_EINH | string |  |
| STAT_TOIL_CVT_BAS_WERT | real | Raw gearbox oil temperature |
| STAT_TOIL_CVT_BAS_EINH | string |  |
| STAT_AC_PRS_BAS_WERT | real | Raw aircon pressure |
| STAT_AC_PRS_BAS_EINH | string |  |
| STAT_TPS_1_BAS_WERT | real | Raw throttle position  voltage 1 |
| STAT_TPS_1_BAS_EINH | string |  |
| STAT_TPS_2_BAS_WERT | real | Raw throttle position  voltage 2 |
| STAT_TPS_2_BAS_EINH | string |  |
| STAT_PVS_1_BAS_WERT | real | Raw driver demand voltage 1 |
| STAT_PVS_1_BAS_EINH | string |  |
| STAT_PVS_2_BAS_WERT | real | Raw driver demand voltage 2 |
| STAT_PVS_2_BAS_EINH | string |  |
| STAT_VLS_UP_1_BAS_WERT | real | Raw upstream oxygen  voltage |
| STAT_VLS_UP_1_BAS_EINH | string |  |
| STAT_VLS_DOWN_1_BAS_WERT | real | Raw downstream oxygen  voltage |
| STAT_VLS_DOWN_1_BAS_EINH | string |  |
| STAT_VBK_BAS_WERT | real | Raw battery voltage after relay |
| STAT_VBK_BAS_EINH | string |  |
| STAT_VBR_BAS_WERT | real | Raw battery voltage after key |
| STAT_VBR_BAS_EINH | string |  |

<a id="job-status-ana-engine4"></a>
### STATUS_ANA_ENGINE4

Read Analogue Input and Output States for LID 13 Read Engine 4 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_TCO_WERT | real | Engine coolant temperature |
| STAT_TCO_EINH | string |  |
| STAT_TIA_WERT | real | Inlet air temperature |
| STAT_TIA_EINH | string |  |
| STAT_MAP_WERT | real | Manifold air pressure |
| STAT_MAP_EINH | string |  |
| STAT_MAP_UP_WERT | real | Upstream Manifold air pressure |
| STAT_MAP_UP_EINH | string |  |
| STAT_TRANS_OIL_TEMP_WERT | real | Gearbox oil temperature |
| STAT_TRANS_OIL_TEMP_EINH | string |  |
| STAT_AC_PRS_WERT | real | Aircon pressure |
| STAT_AC_PRS_EINH | string |  |
| STAT_TPS_MTC_1_WERT | real | Thottle position  1 |
| STAT_TPS_MTC_1_EINH | string |  |
| STAT_TPS_MTC_2_WERT | real | Thottle position  2 |
| STAT_TPS_MTC_2_EINH | string |  |
| STAT_TPS_WERT | real | Thottle opening |
| STAT_TPS_EINH | string |  |
| STAT_PV_AV_1_WERT | real | Driver demand 1 |
| STAT_PV_AV_1_EINH | string |  |
| STAT_PV_AV_2_WERT | real | Driver demand 2 |
| STAT_PV_AV_2_EINH | string |  |
| STAT_PV_AV_WERT | real | Driver demand |
| STAT_PV_AV_EINH | string |  |
| STAT_VLS_UP_1_WERT | real | Upstream oxygen  voltage |
| STAT_VLS_UP_1_EINH | string |  |
| STAT_VLS_DOWN_1_WERT | real | Downstream oxygen  voltage |
| STAT_VLS_DOWN_1_EINH | string |  |
| STAT_VB_RLY_WERT | real | Battery voltage after relay |
| STAT_VB_RLY_EINH | string |  |
| STAT_VB_KEY_WERT | real | Battery voltage after key |
| STAT_VB_KEY_EINH | string |  |

<a id="job-status-ana-engine5"></a>
### STATUS_ANA_ENGINE5

Read Analogue Input and Output States for LID 14 Read Engine 5 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_KNKS_BAS_WERT | real | Knock  voltage |
| STAT_KNKS_BAS_EINH | string |  |
| STAT_IGA_CYL_KNK0_WERT | real | Knock ignition angle cor. |
| STAT_IGA_CYL_KNK0_EINH | string |  |
| STAT_KNKWB_0_WERT | real | Knock window angle beggining |
| STAT_KNKWB_0_EINH | string |  |
| STAT_KNKWD_0_WERT | real | Knock window angle duration |
| STAT_KNKWD_0_EINH | string |  |
| STAT_KNK_EGY_0_WERT | real | Energy of knock window |
| STAT_KNK_EGY_0_EINH | string |  |
| STAT_KNKS_0_WERT | real | Noise level |
| STAT_KNKS_0_EINH | string |  |
| STAT_IGA_IGC_0_WERT | real | Ignition angle cylinder 1 |
| STAT_IGA_IGC_0_EINH | string |  |
| STAT_IGA_IGC_3_WERT | real | Ignition angle cylinder 2 |
| STAT_IGA_IGC_3_EINH | string |  |
| STAT_IGA_IGC_1_WERT | real | Ignition angle cylinder 3 |
| STAT_IGA_IGC_1_EINH | string |  |
| STAT_IGA_IGC_2_WERT | real | Ignition angle cylinder 4 |
| STAT_IGA_IGC_2_EINH | string |  |
| STAT_IGA_SP_WERT | real | Ignition angle set point |
| STAT_IGA_SP_EINH | string |  |

<a id="job-status-ana-o2-heater"></a>
### STATUS_ANA_O2_HEATER

Read Analogue Input and Output States for LID 15 Read Engine 6 analogue infomation - oxygen  heaters

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LSHPWM_UP_1_WERT | real | Upsteam oxygen  heater |
| STAT_LSHPWM_UP_1_EINH | string |  |
| STAT_LSHPWM_DOWN_WERT | real | Downstream oxygen  heater |
| STAT_LSHPWM_DOWN_EINH | string |  |

<a id="job-status-ana-engine7"></a>
### STATUS_ANA_ENGINE7

Read Analogue Input and Output States for LID 16 Read Engine 7 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_MAF_KGH_WERT | real | Mass airflow |
| STAT_MAF_KGH_EINH | string |  |
| STAT_MAP_SP_WERT | real | Manifold pressure setpoint |
| STAT_MAP_SP_EINH | string |  |
| STAT_MAP_UP_SP_WERT | real | Upstream manifold pressure setpoint |
| STAT_MAP_UP_SP_EINH | string |  |
| STAT_TPS_SP_CLC_WERT | real | Thottle position setpoint |
| STAT_TPS_SP_CLC_EINH | string |  |
| STAT_V_TPS_AD_BOL_1_WERT | real | Lower mechanical stop adaptation 1 |
| STAT_V_TPS_AD_BOL_1_EINH | string |  |
| STAT_V_TPS_AD_BOL_2_WERT | real | Lower mechanical stop adaptation 2 |
| STAT_V_TPS_AD_BOL_2_EINH | string |  |
| STAT_V_TPS_AD_EL_BOL_1_WERT | real | Lower electrical stop adaptation 1 |
| STAT_V_TPS_AD_EL_BOL_1_EINH | string |  |
| STAT_V_TPS_AD_EL_BOL_2_WERT | real | Lower electrical stop adaptation 2 |
| STAT_V_TPS_AD_EL_BOL_2_EINH | string |  |
| STAT_V_TPS_AD_LIH_1_WERT | real | Limp home adaptation 1 |
| STAT_V_TPS_AD_LIH_1_EINH | string |  |
| STAT_V_TPS_AD_LIH_2_WERT | real | Limp home adaptation 2 |
| STAT_V_TPS_AD_LIH_2_EINH | string |  |
| STAT_N_SP_IS_WERT | real | Idle speed set point |
| STAT_N_SP_IS_EINH | string |  |
| STAT_TPS_LIH_WERT | real | Limp home throttle position |
| STAT_TPS_LIH_EINH | string |  |

<a id="job-status-ana-fuel-trim"></a>
### STATUS_ANA_FUEL_TRIM

Read Analogue Input and Output States for LID 17 Read Engine 8 analogue information - fuel trim

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_TI_LAM_1_WERT | real | Short term fuel trim |
| STAT_TI_LAM_1_EINH | string |  |
| STAT_LAM_MV_1_WERT | real | Short term fuel trim average |
| STAT_LAM_MV_1_EINH | string |  |
| STAT_TI_AD_ADD_MMV_0_WERT | real | Long term additive fuel trim |
| STAT_TI_AD_ADD_MMV_0_EINH | string |  |
| STAT_TI_AD_ADD_MMV_REL_0_WERT | real | Rel. long term additive fuel trim |
| STAT_TI_AD_ADD_MMV_REL_0_EINH | string |  |
| STAT_TI_AD_FAC_MMV_0_WERT | real | Long term multiplicative fuel trim |
| STAT_TI_AD_FAC_MMV_0_EINH | string |  |
| STAT_TI_AD_FAC_MMV_REL_0_WERT | real | Rel. long term multiplicative fuel trim |
| STAT_TI_AD_FAC_MMV_REL_0_EINH | string |  |

<a id="job-status-ana-engine9"></a>
### STATUS_ANA_ENGINE9

Read Analogue Input and Output States for LID 18 Read Engine 9 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_VB_WERT | real | Battery voltage |
| STAT_VB_EINH | string |  |
| STAT_VS_WERT | real | Vehicle speed |
| STAT_VS_EINH | string |  |
| STAT_N_WERT | real | Engine speed |
| STAT_N_EINH | string |  |
| STAT_VS_CVT_WERT | real | Transmission output shaft speed |
| STAT_VS_CVT_EINH | string |  |
| STAT_GR_MT_WERT | real | Manual tranmission gear ratio |
| STAT_GR_MT_EINH | string |  |
| STAT_GR_AT_WERT | real | Auto tranmission gear ratio |
| STAT_GR_AT_EINH | string |  |
| STAT_CPPWM_WERT | real | Canister purge duty ratio |
| STAT_CPPWM_EINH | string |  |
| STAT_LOAD_CLC_WERT | real | Calculated load |
| STAT_LOAD_CLC_EINH | string |  |

<a id="job-status-ana-inj-time"></a>
### STATUS_ANA_INJ_TIME

Read Analogue Input and Output States for LID 19 Read Engine 10 analogue information - injection times

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_TIPR_WERT | real | Pre-injection time |
| STAT_TIPR_EINH | string |  |
| STAT_TI_V_000_WERT | real | Computed injection time |
| STAT_TI_V_000_EINH | string |  |

<a id="job-status-ana-ews"></a>
### STATUS_ANA_EWS

Read Analogue Input and Output States for LID 20 Read Immobiliser information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CTR_SDR_1_IMOB_WERT | real | Locked engine counter |
| STAT_CTR_SDR_1_IMOB_EINH | string |  |
| STAT_CTR_SDR_2_IMOB_WERT | real | Unsuccesful communication counter |
| STAT_CTR_SDR_2_IMOB_EINH | string |  |
| STAT_CTR_SDR_3_IMOB_WERT | real | Key on counter |
| STAT_CTR_SDR_3_IMOB_EINH | string |  |

<a id="job-status-ana-man-test"></a>
### STATUS_ANA_MAN_TEST

Read Analogue Input and Output States for LID 21 Read Manufacturing Test information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CAN_FTL_WERT | real | Fuel level |
| STAT_CAN_FTL_EINH | string |  |
| STAT_TCO_WERT | real | Coolant temperature |
| STAT_TCO_EINH | string |  |
| STAT_N_WERT | real | Engine speed |
| STAT_N_EINH | string |  |
| STAT_TIA_WERT | real | Air temperature |
| STAT_TIA_EINH | string |  |
| STAT_MAP_WERT | real | Manifold pressure |
| STAT_MAP_EINH | string |  |
| STAT_MAP_UP_WERT | real | Upstream manifold pressure |
| STAT_MAP_UP_EINH | string |  |
| STAT_TPS_1_BAS_WERT | real | Throttle angle 1 |
| STAT_TPS_1_BAS_EINH | string |  |
| STAT_TPS_2_BAS_WERT | real | Throttle angle 2 |
| STAT_TPS_2_BAS_EINH | string |  |
| STAT_PVS_1_BAS_WERT | real | Accelerator pedal  1 |
| STAT_PVS_1_BAS_EINH | string |  |
| STAT_PVS_2_BAS_WERT | real | Accelerator pedal  2 |
| STAT_PVS_2_BAS_EINH | string |  |
| STAT_TOIL_CVT_BAS_WERT | real | Gearbox oil temperature |
| STAT_TOIL_CVT_BAS_EINH | string |  |
| STAT_AC_PRS_BAS_WERT | real | Aircon pressure |
| STAT_AC_PRS_BAS_EINH | string |  |
| STAT_ALTER_WERT | real | Alternator load |
| STAT_ALTER_EINH | string |  |
| STAT_VS_CVT_WERT | real | Gearbox output shaft speed |
| STAT_VS_CVT_EINH | string |  |
| STAT_VS_WERT | real | Road speed |
| STAT_VS_EINH | string |  |
| STAT_LAM_MV_1_WERT | real | Fuelling correction |
| STAT_LAM_MV_1_EINH | string |  |
| STAT_VLS_CYC_MMV_EOL_1_WERT | real | Upstream O2  cycle time (filtered) |
| STAT_VLS_CYC_MMV_EOL_1_EINH | string |  |
| STAT_KNKS_0_WERT | real | Knock noise level |
| STAT_KNKS_0_EINH | string |  |
| STAT_VLSH_UP_1_WERT | real | Upstream oxygen  heater voltage |
| STAT_VLSH_UP_1_EINH | string |  |
| STAT_VLSH_DOWN_1_WERT | real | Downstream oxygen  heater voltage |
| STAT_VLSH_DOWN_1_EINH | string |  |
| STAT_MIS_B0_WERT | real | Misfire count over 1000 revolutions for cylinder 1 |
| STAT_MIS_B0_EINH | string |  |
| STAT_MIS_B3_WERT | real | Misfire count over 1000 revolutions for cylinder 2 |
| STAT_MIS_B3_EINH | string |  |
| STAT_MIS_B1_WERT | real | Misfire count over 1000 revolutions for cylinder 3 |
| STAT_MIS_B1_EINH | string |  |
| STAT_MIS_B2_WERT | real | Misfire count over 1000 revolutions for cylinder 4 |
| STAT_MIS_B2_EINH | string |  |
| STAT_ER_MMV_EOL_000_WERT | real | Raw Engine roughness value for cylinder 1 |
| STAT_ER_MMV_EOL_000_EINH | string |  |
| STAT_ER_MMV_EOL_003_WERT | real | Raw Engine roughness value for cylinder 2 |
| STAT_ER_MMV_EOL_003_EINH | string |  |
| STAT_ER_MMV_EOL_001_WERT | real | Raw Engine roughness value for cylinder 3 |
| STAT_ER_MMV_EOL_001_EINH | string |  |
| STAT_ER_MMV_EOL_002_WERT | real | Raw Engine roughness value for cylinder 4 |
| STAT_ER_MMV_EOL_002_EINH | string |  |
| STAT_ER_THD_000_WERT | real | Engine roughness threshold value for cylinder 1 |
| STAT_ER_THD_000_EINH | string |  |
| STAT_ER_THD_003_WERT | real | Engine roughness threshold value for cylinder 2 |
| STAT_ER_THD_003_EINH | string |  |
| STAT_ER_THD_001_WERT | real | Engine roughness threshold value for cylinder 3 |
| STAT_ER_THD_001_EINH | string |  |
| STAT_ER_THD_002_WERT | real | Engine roughness threshold value for cylinder 4 |
| STAT_ER_THD_002_EINH | string |  |
| STAT_FAIL_TLDP_EOL_WERT | real | Leak detection pump test status |
| STAT_FAIL_TLDP_EOL_EINH | string |  |

<a id="job-status-ana-cvt2"></a>
### STATUS_ANA_CVT2

Read Analogue Input and Output States for LID 23 Read Constant Velocity Transmission 2 analogue information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_CMD_TYPE_WERT | real | CVT command type |
| STAT_CMD_TYPE_EINH | string |  |
| STAT_MODE_CURRENT_WERT | real | CVT mode |
| STAT_MODE_CURRENT_EINH | string |  |
| STAT_ENG_SPD_TARGET_WERT | real | Target engine speed |
| STAT_ENG_SPD_TARGET_EINH | string |  |
| STAT_CVT_DFT_TOT_DIST_WERT | real | Distance travelled in default mode |
| STAT_CVT_DFT_TOT_DIST_EINH | string |  |
| STAT_T_CVT_MODE_NEUTRAL_WERT | real | Cumulated time in neutral mode |
| STAT_T_CVT_MODE_NEUTRAL_EINH | string |  |
| STAT_T_CVT_MODE_DRIVE_WERT | real | Cumulated time in drive mode |
| STAT_T_CVT_MODE_DRIVE_EINH | string |  |
| STAT_T_CVT_MODE_SPORT_WERT | real | Cumulated time in sport mode |
| STAT_T_CVT_MODE_SPORT_EINH | string |  |
| STAT_T_CVT_MODE_MANUAL_WERT | real | Cumulated time in manual mode |
| STAT_T_CVT_MODE_MANUAL_EINH | string |  |
| STAT_T_CVT_ENG_RUN_WERT | real | Cumulated time engine running |
| STAT_T_CVT_ENG_RUN_EINH | string |  |

<a id="job-status-ana-cvt-ratio-adaption"></a>
### STATUS_ANA_CVT_RATIO_ADAPTION

Read Analogue Input and Output States for LID 25 Read CVT ratio adaption information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_TAB_IP_TRAN_CRV_ADJUST_00_WERT | real | CVT ratio control adaptions 00 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_00_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_01_WERT | real | CVT ratio control adaptions 01 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_01_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_02_WERT | real | CVT ratio control adaptions 02 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_02_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_03_WERT | real | CVT ratio control adaptions 03 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_03_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_04_WERT | real | CVT ratio control adaptions 04 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_04_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_05_WERT | real | CVT ratio control adaptions 05 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_05_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_06_WERT | real | CVT ratio control adaptions 06 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_06_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_07_WERT | real | CVT ratio control adaptions 07 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_07_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_08_WERT | real | CVT ratio control adaptions 08 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_08_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_09_WERT | real | CVT ratio control adaptions 09 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_09_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_10_WERT | real | CVT ratio control adaptions 10 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_10_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_11_WERT | real | CVT ratio control adaptions 11 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_11_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_12_WERT | real | CVT ratio control adaptions 12 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_12_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_13_WERT | real | CVT ratio control adaptions 13 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_13_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_14_WERT | real | CVT ratio control adaptions 14 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_14_EINH | string |  |
| STAT_TAB_IP_TRAN_CRV_ADJUST_15_WERT | real | CVT ratio control adaptions 15 |
| STAT_TAB_IP_TRAN_CRV_ADJUST_15_EINH | string |  |
| STAT_FAST_ADAPT_WERT | real | CVT adaption status |
| STAT_FAST_ADAPT_EINH | string |  |

<a id="job-status-ana-cvt-clutch-adaption"></a>
### STATUS_ANA_CVT_CLUTCH_ADAPTION

Read Analogue Input and Output States for LID 26 Read CVT clutch adaption information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_BP_ADAPTION_D_WERT | real | Current bite point adaption in Drive |
| STAT_BP_ADAPTION_D_EINH | string |  |
| STAT_BP_ADAPTION_R_WERT | real | Current bite point adaption in Reverse |
| STAT_BP_ADAPTION_R_EINH | string |  |
| STAT_CLU_BITE_POINT_EOL_D_WERT | real | EOL adaption value in Drive |
| STAT_CLU_BITE_POINT_EOL_D_EINH | string |  |
| STAT_CLU_BITE_POINT_EOL_R_WERT | real | EOL adaption value in Reverse |
| STAT_CLU_BITE_POINT_EOL_R_EINH | string |  |
| STAT_LONG_TERM_ADPT_D_WERT | real | Current long term adaption in Drive |
| STAT_LONG_TERM_ADPT_D_EINH | string |  |
| STAT_LONG_TERM_ADPT_R_WERT | real | Current long term adaption in Reverse |
| STAT_LONG_TERM_ADPT_R_EINH | string |  |
| STAT_CVT_ADAPT_1_WERT | real | CVT clutch adaption information |
| STAT_CVT_ADAPT_1_EINH | string |  |
| STAT_CLU_MOD_ACTIVE_WERT | real | Clutch control mode |
| STAT_CLU_MOD_ACTIVE_EINH | string |  |
| STAT_TQ_AV_WERT | real | Torque delivered to the clutch |
| STAT_TQ_AV_EINH | string |  |

<a id="job-status-ana-base-engine"></a>
### STATUS_ANA_BASE_ENGINE

Read Analogue Input and Output States for LID 27 Read Base Engine information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_TQ_DIF_IS_AD_WERT | real | Torque adaption at idle without drive or A/C |
| STAT_TQ_DIF_IS_AD_EINH | string |  |
| STAT_TQ_DIF_I_IS_WERT | real | Idle speed integrator I part |
| STAT_TQ_DIF_I_IS_EINH | string |  |
| STAT_TQ_DIF_P_D_IS_WERT | real | Idle speed integrator P+D part |
| STAT_TQ_DIF_P_D_IS_EINH | string |  |

<a id="job-status-ana-obd2"></a>
### STATUS_ANA_OBD2

Read Analogue Input and Output States for LID 28 Read OBD 2 information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_DIF_AR_RED_WERT | real | Air path adaption at idle |
| STAT_DIF_AR_RED_EINH | string |  |
| STAT_SLOP_AR_RED_WERT | real | Air path adaption at part load |
| STAT_SLOP_AR_RED_EINH | string |  |
| STAT_DIF_MAF_SCHA_SAV_WERT | real | Air path adaption across supercharger |
| STAT_DIF_MAF_SCHA_SAV_EINH | string |  |
| STAT_DIST_ACT_MIL_WERT | real | Distance MIL on |
| STAT_DIST_ACT_MIL_EINH | string |  |
| STAT_DIST_ACT_WAL_1_WERT | real | Distance DBW on |
| STAT_DIST_ACT_WAL_1_EINH | string |  |
| STAT_DIST_ACT_WAL_2_WERT | real | Distance EP on |
| STAT_DIST_ACT_WAL_2_EINH | string |  |
| STAT_DOWN_DYN_MEM_CAT_WERT | real | Catalyst monitor last result |
| STAT_DOWN_DYN_MEM_CAT_EINH | string |  |
| STAT_VLS_CYC_SUM_MEM_WERT | real | O2 sensor last result |
| STAT_VLS_CYC_SUM_MEM_EINH | string |  |
| STAT_VLS_CYC_MAX_MEM_WERT | real | O2 sensor last result threshold |
| STAT_VLS_CYC_MAX_MEM_EINH | string |  |
| STAT_SEG_AD_MMV_000_WERT | real | Flywheel adaption seg 0 |
| STAT_SEG_AD_MMV_000_EINH | string |  |
| STAT_SEG_AD_MMV_001_WERT | real | Flywheel adaption seg 1 |
| STAT_SEG_AD_MMV_001_EINH | string |  |
| STAT_SEG_AD_MMV_002_WERT | real | Flywheel adaption seg 2 |
| STAT_SEG_AD_MMV_002_EINH | string |  |
| STAT_SEG_AD_MMV_003_WERT | real | Flywheel adaption seg 3 |
| STAT_SEG_AD_MMV_003_EINH | string |  |
| STAT_CTR_CDN_RBM_TLDP_WERT | real | EVAP monitor conditions encountered counts |
| STAT_CTR_CDN_RBM_TLDP_EINH | string |  |
| STAT_CTR_COMP_RBM_TLDP_WERT | real | EVAP monitor completion condition counts |
| STAT_CTR_COMP_RBM_TLDP_EINH | string |  |
| STAT_CTR_CDN_RBM_LS_UP_DIAG_WERT | real | O2 sensor monitor conditions encountered counts Bank 1 |
| STAT_CTR_CDN_RBM_LS_UP_DIAG_EINH | string |  |
| STAT_CTR_COMP_RBM_LS_UP_DIAG_WERT | real | O2 sensor monitor completion condition counts |
| STAT_CTR_COMP_RBM_LS_UP_DIAG_EINH | string |  |
| STAT_CTR_CDN_RBM_CAT_DIAG_WERT | real | Catalyst monitor conditions encountered Bank 1 |
| STAT_CTR_CDN_RBM_CAT_DIAG_EINH | string |  |
| STAT_CTR_COMP_RBM_CAT_DIAG_WERT | real | Catalyst monitor completions condition counts |
| STAT_CTR_COMP_RBM_CAT_DIAG_EINH | string |  |
| STAT_CTR_IGK_CYC_RBM_WERT | real | Ignition counter |
| STAT_CTR_IGK_CYC_RBM_EINH | string |  |
| STAT_CTR_CDN_OBD_RBM_WERT | real | OBD monitoring conditions encountered counts |
| STAT_CTR_CDN_OBD_RBM_EINH | string |  |

<a id="job-status-io-can-asc1"></a>
### STATUS_IO_CAN_ASC1

Read Digital Input States for LID 01 Read Anti Slip Control 1 digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_CAN_TQ_STATE_ACTIVE | int | ABS/ASC override activity status |

<a id="job-status-io-driving-stability"></a>
### STATUS_IO_DRIVING_STABILITY

Read Digital Input States for LID 03 Read Driving Stability control status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_DSC_ACT_ACTIVE | int | Driving stability control status |

<a id="job-status-io-can-asc4"></a>
### STATUS_IO_CAN_ASC4

Read Digital Input States for LID 04 Read Anti Slip Control 4 digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_TW_MSR_REQ_ACTIVE | int | MSR torque increase request active |
| STAT_LV_TW_ASR_REQ_ACTIVE | int | ASC torque decrease request active |

<a id="job-status-adaption-cvi"></a>
### STATUS_ADAPTION_CVI

Read Digital Input States for LID 26 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_CLU_CAL_DONE_D | int |  |
| STAT_LV_CLU_CAL_DONE_R | int |  |
| STAT_LV_CLU_ADAPT_D_MAX_FAULT | int |  |
| STAT_LV_CLU_ADAPT_D_MIN_FAULT | int |  |
| STAT_LV_CLU_ADAPT_R_MAX_FAULT | int |  |
| STAT_LV_CLU_ADAPT_R_MIN_FAULT | int |  |
| STAT_CLU_MOD_ACTIVE | int |  |

<a id="job-status-io-can-dme1"></a>
### STATUS_IO_CAN_DME1

Read Digital Input States for LID 05 Read Digital Motor Electronics 1 digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_KEY_OFF_ACTIVE | int | Ignition switch status 0=Ignition on, 1=Ignition off |
| STAT_LV_CAN_CRK_ERR_ACTIVE | int | Engine speed error status |
| STAT_LV_ACCOUT_RELAY_ACTIVE | int | Air con compressor status |

<a id="job-status-io-can-dme4"></a>
### STATUS_IO_CAN_DME4

Read Digital Input States for LID 07 Read Digital Motor Electronics 4 digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_MIL_ON | int | Engine MIL status |
| STAT_LV_CRU_ON_LAMP_ON | int | Cruise available lamp status |
| STAT_LV_WAL_1_ON | int | Engine warning lamp |

<a id="job-status-io-wheel-torque"></a>
### STATUS_IO_WHEEL_TORQUE

Read Digital Input States for LID 09 Read Digital Motor Electronics 6 digital information - torque

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_CAN_TW_FLT_ACTIVE | int | Torque intervention failure |
| STAT_LV_TCS_TW_ACK_ACTIVE | int | Torque at wheels request acknowledgement |

<a id="job-status-io-shifting"></a>
### STATUS_IO_SHIFTING

Read Digital Input States for LID 0B Read State of Gear Shifting

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_CAN_GS_ACTIVE | int | Shifting active |

<a id="job-status-io-cvt1"></a>
### STATUS_IO_CVT1

Read Digital Input States for LID 0C Read Constant Vehicle Transmission 1 digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response as a hex string |
| STAT_LV_SHIFTER_PARK_ON | int | Park switch status |
| STAT_LV_SHIFTER_REVERSE_ON | int | Reverse switch status |
| STAT_LV_SHIFTER_NEUTRAL_ON | int | Neutral switch status |
| STAT_LV_SHIFTER_DRIVE_ON | int | Drive switch status |
| STAT_LV_SHIFTER_MANUAL_ON | int | Manual switch status |
| STAT_LV_SHIFTER_PLUS_ON | int | Plus switch status |
| STAT_LV_SHIFTER_MINUS_ON | int | Minus switch status |
| STAT_LV_SHIFTER_MODE_ON | int | Mode switch status |
| STAT_LV_WHEEL_PLUS_ON | int | Extra plus switch status |
| STAT_LV_WHEEL_MINUS_ON | int | Extra minus switch status |
| STAT_LV_SPARE_SWI_1_ON | int | Spare switch 1 status |
| STAT_LV_SPARE_SWI_2_ON | int | Spare switch 2 status |
| STAT_LV_GIB_CKS_ERR_DET_ON | int | EE checksum fault in GIB |
| STAT_LV_GIB_CTL_ERR_DET_ON | int | Control impossible |

<a id="job-status-io-instr3"></a>
### STATUS_IO_INSTR3

Read Digital Input States for LID 0E Read Instruments 3 digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_ACCIN_ON | int | Air con compressor state request |
| STAT_LV_ACIN_ON | int | Air con request |

<a id="job-status-io-engine1"></a>
### STATUS_IO_ENGINE1

Read Digital Input States for LID 10 Read Engine 1 digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_TIA_ERR_ACTIVE | int | Error currently present on air temperature |
| STAT_LV_TCO_ERR_ACTIVE | int | Error currently present on coolant temperature |
| STAT_LV_CAM_ERR_ACTIVE | int | Error currently present on camshaft signal |
| STAT_LV_CAM_ERR_LIH_ACTIVE | int | Limp home activation for CAM |
| STAT_LV_CAM_1_LEVEL_ACTIVE | int | Indication of CAM falling edge |
| STAT_LV_CRK_ERR_ACTIVE | int | Error currently present on crankshaft signal |
| STAT_LV_CRK_ERR_LIH_ACTIVE | int | Limp home activation for CRANK |
| STAT_LV_MAP_ERR_ACTIVE | int | Error currently present on MAP |
| STAT_LV_MAP_LIH_ACTIVE | int | Limp home activation for MAP |
| STAT_LV_TPS_ERR_1_ACTIVE | int | Error currently present on throttle position  1 |
| STAT_LV_TPS_ERR_2_ACTIVE | int | Error currently present on throttle position  2 |
| STAT_LV_ERR_IV_0_ACTIVE | int | Error currently present on injector A |
| STAT_LV_ERR_IV_1_ACTIVE | int | Error currently present on injector B |
| STAT_LV_ERR_IV_2_ACTIVE | int | Error currently present on injector C |
| STAT_LV_ERR_IV_3_ACTIVE | int | Error currently present on injector D |
| STAT_LV_PVS_ERR_1_ACTIVE | int | Error currently present on driver demand 1 |
| STAT_LV_PVS_ERR_2_ACTIVE | int | Error currently present on driver demand 2 |
| STAT_LV_MTC_AD_ERR_ACTIVE | int | Error currently present on motorized throttle |
| STAT_LV_MTC_CTL_ERR_ACTIVE | int | Error currently present on motorized throttle controller |
| STAT_LV_AC_PRS_ERR_ACTIVE | int | Error currently present on Aircon pressure tranducer |
| STAT_LV_ERR_PRES_TLDP_EOL_ACTIVE | int | Error currently present on LDP (end of line test only) |
| STAT_LV_MAP_UP_ERR_ACTIVE | int | Error currently present on upstream MAP |
| STAT_LV_ERR_CPS_ACTIVE | int | Error currently present on canister purge solenoid |
| STAT_LV_ERR_EFP_ACTIVE | int | Error currently present on fuel pump relay |
| STAT_LV_ERR_CAN_ASC_ACTIVE | int | Error currently present on incoming CAN ABS frame |
| STAT_LV_ERR_CAN_EGS_ACTIVE | int | Error currently present on incoming CAN EGS frame |
| STAT_LV_ERR_CAN_INSTR_ACTIVE | int | Error currently present on incoming CAN INSTR frame |
| STAT_LV_ERR_BOFF_ACTIVE | int | Error currently present on CAN protocol |
| STAT_LV_EFP_ACTIVE | int | Fuel pump relay activated |
| STAT_LV_AST_ACTIVE | int | Engine after start phase |
| STAT_LV_IS_ACTIVE | int | Idle phase |
| STAT_LV_PL_ACTIVE | int | Engine part load phase |
| STAT_LV_PU_ACTIVE | int | Engine trailing throttle phase |
| STAT_LV_PUC_ACTIVE | int | Engine trailing throttle cut-off phase |
| STAT_LV_FL_ACTIVE | int | Engine full load phase |
| STAT_LV_CT_ACTIVE | int | Closed throttle |
| STAT_LV_MAIN_RLY_ACTIVE | int | Main relay activated |
| STAT_LV_BLS_ACTIVE | int | Brake switch 1 |
| STAT_LV_BTS_ACTIVE | int | Brake switch 2 |
| STAT_LV_CS_CRU_ACTIVE | int | Clutch switch |
| STAT_LV_IN_RS_TLDP_ACTIVE | int | EVAPS pressure switch |
| STAT_LV_PRNDM_FAULT_ACTIVE | int | PRNDM fault flag |
| STAT_LV_VS_CVT_ERR_ACTIVE | int | CVT vehicle speed error |
| STAT_LV_RATIO_PLAUS_ERR_ACTIVE | int | CVT ratio plausibility error |
| STAT_LV_TRANS_OIL_TEMP_ERR_ACTIVE | int | Tranmission oil temperature error |
| STAT_LV_SHIFT_IN_PROGRESS_ACTIVE | int | CVT shift in progress |
| STAT_LV_ASR_AUTH_ACTIVE | int | ASR request authorised |
| STAT_LV_MSR_AUTH_ACTIVE | int | MSR request authorised |
| STAT_LV_CLUTCH_LOCKED_ACTIVE | int | Clutch locked |

<a id="job-status-io-engine2"></a>
### STATUS_IO_ENGINE2

Read Digital Input States for LID 11 Read Engine 2 digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_MIL_ALSO_ACTIVE | int | MIL light |
| STAT_LV_ACCOUT_RLY_ALSO_ACTIVE | int | Air conditioning relay activated |
| STAT_LV_CFA_1_ACTIVE | int | Cooling fan activated at low speed |
| STAT_LV_CFA_2_ACTIVE | int | Cooling fan activated at medium speed |
| STAT_LV_CFA_3_ACTIVE | int | Cooling fan activated at high speed |
| STAT_LV_KEY_ON_ACTIVE | int | Ignition key is on |
| STAT_LV_ACIN_ALSO_ACTIVE | int | Air conditioning request |
| STAT_LV_ACCIN_ALSO_ACTIVE | int | Air conditioning compressor relay |
| STAT_LV_AC_FAN_REQ_1_ACTIVE | int | Air conditionning fan low speed request |
| STAT_LV_AFR_1_ACTIVE | int | Rich mixture detected on upstream oxygen  1 |
| STAT_LV_LSCL_1_ACTIVE | int | Closed loop enable |
| STAT_LV_LS_UP_ACTIVE | int | Upstream oxygen  1 ready for air/fuel regulation |
| STAT_LV_LS_DOWN_ACTIVE | int | Downstream  operability |
| STAT_LV_RUN_ENG_ACTIVE | int | Engine is running |
| STAT_LV_SYN_ENG_ACTIVE | int | Engine is synchronized |
| STAT_LV_ES_ACTIVE | int | Engine is stopped |
| STAT_LV_ST_ACTIVE | int | Engine start phase |
| STAT_LV_MSR_ACT_ACTIVE | int | Torque increase flag |
| STAT_LV_ASR_ACT_ACTIVE | int | Torque reduction flag |
| STAT_LV_TPS_AD_REQ_ACTIVE | int | Throttle adaption successful |

<a id="job-status-io-ews"></a>
### STATUS_IO_EWS

Read Digital Input States for LID 20 Read Immobiliser digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_ERR_IMOB_03_ACTIVE | int | No successful communication flag |
| STAT_LV_ERR_IMOB_04_ACTIVE | int | Wrong message received |
| STAT_LV_SEED_KEY_INI_ACTIVE | int | Rolling code set to start value |
| STAT_LV_NOT_LEARNT_MEM_IMOB_ACTIVE | int | SEED code not learnt |
| STAT_LV_LOCK_IMOB_ACTIVE | int | Immobilization status 0=unlocked, 1=locked |
| STAT_LV_ANS_ERR_IMOB_ACTIVE | int | Erroneous answer received |
| STAT_LV_ANS_ERR_COM_IMOB_ACTIVE | int | Communication error |
| STAT_LV_ANS_NOT_IMOB_ACTIVE | int | No correct answer before end of comm time |

<a id="job-status-io-man-test"></a>
### STATUS_IO_MAN_TEST

Read Digital Input States for LID 21 Read Manufacturing Test digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_SEG_T_AD_ERR_ACTIVE | int | Flywheel adaptation flag error |
| STAT_LV_SEG_AD_STATE_ACTIVE | int | Flywheel adaptation flag done |
| STAT_LV_END_CAT_DIAG_EOL_ACTIVE | int | Manufacturing catalyst test complete flag |
| STAT_LV_AUTH_CAT_DIAG_EOL_ACTIVE | int | Catalyst condition flag |
| STAT_LV_ERR_PRES_LS_DOWN_EOL_ACTIVE | int | Downstream O2  condition flag |
| STAT_LV_END_TLDP_DIAG_EOL_ACTIVE | int | LDP test flag |
| STAT_LV_ERR_PRES_TLDP_EOL_ACTIVE | int | Error present in LDP EOL Test |
| STAT_LV_ERR_PRES_CAT_EOL_ACTIVE | int | Error present in Catalyst condition EOL Test |
| STAT_LV_ERR_PRES_0_TLDP_ACTIVE | int | Reed switch blocked in open position - State 1 detection. |
| STAT_LV_ERR_PRES_1_TLDP_ACTIVE | int | Reed switch blocked in closed position - State 2 detection. |
| STAT_LV_ERR_PRES_2_TLDP_ACTIVE | int | Reed switch blocked in open position - State 3 detection. |
| STAT_LV_ERR_PRES_3_TLDP_ACTIVE | int | Pinched Tube. |
| STAT_LV_ERR_PRES_4_TLDP_ACTIVE | int | Leakage &gt;= 0.5mm. |
| STAT_LV_ERR_PRES_5_TLDP_ACTIVE | int | Leakage &gt;= 1.0mm. |
| STAT_LV_ERR_PRES_6_TLDP_ACTIVE | int | Leakage &gt;&gt; 1.0mm (fuel cap lost). |
| STAT_LV_ERR_PRES_7_TLDP_ACTIVE | int | Cannister purge system blocked. |

<a id="job-status-io-cruise"></a>
### STATUS_IO_CRUISE

Read Digital Input States for LID 22 Read Cruise digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_CRU_CTL_ACT_ACTIVE | int | Cruise active |
| STAT_LV_CRU_CTL_AUTH_ACTIVE | int | Cruise enabled |
| STAT_LV_CRU_SWI_ON_OFF_ACTIVE | int | Cruise signal O/I |
| STAT_LV_CRU_SWI_RES_ACTIVE | int | Cruise signal RES |
| STAT_LV_CRU_SWI_SET_POS_ACTIVE | int | Cruise signal SET+ |
| STAT_LV_CRU_SWI_SET_MINUS_ACTIVE | int | Cruise signal SET- |
| STAT_LV_BLS_1_ACTIVE | int | Cruise suspension byte 1 - brake pedal |
| STAT_LV_CS_CRU_1_ACTIVE | int | Cruise suspension byte 1 - clutch pedal |
| STAT_LV_DRIV_1_ACTIVE | int | Cruise suspension byte 1 - P/N/D engaged or no valid forward ratio |
| STAT_LV_N_CRU_AUTH_1_ACTIVE | int | Cruise suspension byte 1 - engine speed outside of operating range Siemens mnemonic has changed from LV_CRU_N_INH to LV_N_CRU_AUTH |
| STAT_LV_VS_CRU_ON_AUTH_1_ACTIVE | int | Cruise suspension byte 1 - road speed outside of operating range Siemens mnemonic has changed from LV_CRU_VS_INH to LV_VS_CRU_ON_AUTH |
| STAT_LV_ASR_MSR_ACT_1_ACTIVE | int | Cruise suspension byte 1 - traction control active Siemens mnemonic has changed from LV_TCS_AUTH to LV_ASR_MSR_ACT |
| STAT_LV_VS_RATIO_DFT_1_ACTIVE | int | Cruise suspension byte 1 - vehicle speed below 70% of stored speed |
| STAT_LV_CRU_SWI_ON_OFF_1_ACTIVE | int | Cruise suspension byte 1 - O/I switch pressed |

<a id="job-status-io-oil-test-ok"></a>
### STATUS_IO_OIL_TEST_OK

Read Digital Input States for LID 23 Read whether it is OK to measure the oil level

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_OIL_LEVEL_TEST_OK_ACTIVE | int | Gearbox oil temperature is OK to measure oil level |

<a id="job-status-io-ready-code"></a>
### STATUS_IO_READY_CODE

Read Digital Input States for LID 24 Read Readiness code digital information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_READY_EVAP_1_ACTIVE | int | Readiness flag of EVAP 1 1 = not ready, 0 = ready |
| STAT_LV_READY_EVAP_2_ACTIVE | int | Readiness flag of EVAP 2 1 = not ready, 0 = ready |
| STAT_LV_READY_EVAP_3_ACTIVE | int | Readiness flag of EVAP 3 1 = not ready, 0 = ready |
| STAT_LV_READY_EVAP_4_ACTIVE | int | Readiness flag of EVAP 4 1 = not ready, 0 = ready |
| STAT_LV_READY_MIS_A_ACTIVE | int | Readiness flag of misfire A 1 = not ready, 0 = ready |
| STAT_LV_READY_MIS_B1_ACTIVE | int | Readiness flag of misfire B1 1 = not ready, 0 = ready |
| STAT_LV_READY_MIS_B4_ACTIVE | int | Readiness flag of misfire B4 1 = not ready, 0 = ready |
| STAT_LV_READY_FSD_1_ACTIVE | int | Readiness flag of fuel system 1 = not ready, 0 = ready |
| STAT_LV_READY_OBD_ACTIVE | int | Readiness flag for comprehensive component 1 = not ready, 0 = ready |
| STAT_LV_READY_LS_UP_1_ACTIVE | int | Readiness flag of UP O2 1 = not ready, 0 = ready |
| STAT_LV_READY_LS_DOWN_1_ACTIVE | int | Readiness flag of DOWN O2 1 = not ready, 0 = ready |
| STAT_LV_READY_CAT_1_ACTIVE | int | Readiness flag of catalyst 1 = not ready, 0 = ready |

<a id="job-status-io-cvt-clutch-adaption"></a>
### STATUS_IO_CVT_CLUTCH_ADAPTION

Read Digital Input States for LID 26 Read clutch adaption information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |
| STAT_LV_CLU_CAL_DONE_D_ACTIVE | int | CVT EOL Clutch adaption complete in Drive |
| STAT_LV_CLU_CAL_DONE_R_ACTIVE | int | CVT EOL Clutch adaption complete in Reverse |
| STAT_LV_CLU_ADAPT_D_MAX_FAULT_ACTIVE | int | Biting point adaption Maximum in Drive |
| STAT_LV_CLU_ADAPT_D_MIN_FAULT_ACTIVE | int | Biting point adaption Minimum in Drive |
| STAT_LV_CLU_ADAPT_R_MAX_FAULT_ACTIVE | int | Biting point adaption Maximum in Reverse |
| STAT_LV_CLU_ADAPT_R_MIN_FAULT_ACTIVE | int | Biting point adaption Minimum in Reverse |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Motordrehzahl Read the engine speed

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STATUS_MOTORDREHZAHL_WERT | real | Engine speed |
| STAT_MOTORDREHZAHL_WERT | real | Engine speed |
| STAT_MOTORDREHZAHL_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-ll-solldrehzahl"></a>
### STATUS_LL_SOLLDREHZAHL

Solldrehzahl Leerlaufregler auslesen Read the target idle speed

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LL_SOLLDREHZAHL_WERT | real | Ergebnis Solldrehzahl Target idle speed |
| STAT_LL_SOLLDREHZAHL_EINH | string | Einheit Solldrehzahl |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-zuendwinkel"></a>
### STATUS_ZUENDWINKEL

Zuendwinkel Zyl1 Read the spark advance angle

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZUENDWINKEL_WERT | real | Spark advance angle |
| STAT_ZUENDWINKEL_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

Luftmasse Read the air mass

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LMM_MASSE_WERT | real | Mass airflow |
| STAT_LMM_MASSE_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-einspritzzeit"></a>
### STATUS_EINSPRITZZEIT

Einspritzzeit EV1 Read the injection duration

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EINSPRITZZEIT_WERT | real | Computed injection time |
| STAT_EINSPRITZZEIT_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-last"></a>
### STATUS_LAST

Lastsignal auslesen Read the calculated load value

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LAST_WERT | real | Ergebnis Lastsignal WRGL Caculated load value |
| STAT_LAST_EINH | string | Einheit Lastsignal WRGL |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-dkp-winkel"></a>
### STATUS_DKP_WINKEL

DK-Winkel Read the throttle angle

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DKP_WINKEL_WERT | real | Throttle opening |
| STAT_DKP_WINKEL_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-systemcheck-laufunruhe"></a>
### STATUS_SYSTEMCHECK_LAUFUNRUHE

Laufunruhe lesen Read the engine roughness for each cylinder

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL1_WERT | real | Engine roughness cylinder 1 Rundlaufwert Zylinder 1 |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL2_WERT | real | Engine roughness cylinder 2 Rundlaufwert Zylinder 2 |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL3_WERT | real | Engine roughness cylinder 3 Rundlaufwert Zylinder 3 |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL4_WERT | real | Engine roughness cylinder 4 Rundlaufwert Zylinder 4 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-ls-vkat-heizung-tv-1"></a>
### STATUS_LS_VKAT_HEIZUNG_TV_1

norm. Heizleist. L-Sonde vKat1 Read the upstream oxygen  heater

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LS_VKAT_HEIZUNG_TV_1_WERT | real | Upstream oxygen  heater |
| STAT_LS_VKAT_HEIZUNG_TV_1_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-ls-nkat-heizung-tv-1"></a>
### STATUS_LS_NKAT_HEIZUNG_TV_1

norm. Heizleist. L-Sonde hKat1 Read the downstream oxygen  heater

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LS_NKAT_HEIZUNG_TV_1_WERT | real | Downstream oxygen  heater |
| STAT_LS_NKAT_HEIZUNG_TV_1_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-ls-vkat-signal-1"></a>
### STATUS_LS_VKAT_SIGNAL_1

Lambdasondenspannung v Kat Read the voltage of the upstream oxygen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LS_VKAT_SIGNAL_1_WERT | real | Upstream oxygen  voltage |
| STAT_LS_VKAT_SIGNAL_1_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-ls-nkat-signal-1"></a>
### STATUS_LS_NKAT_SIGNAL_1

Lambdasondenspannung n Kat Read the voltage of the downstream oxygen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LS_NKAT_SIGNAL_1_WERT | real | Downstream oxygen  voltage |
| STAT_LS_NKAT_SIGNAL_1_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-lambda-integrator-1"></a>
### STATUS_LAMBDA_INTEGRATOR_1

Lambdaregler1 Read the fuel control bank 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LAMBDA_INTEGRATOR_1_WERT | real | Short term fuel trim bank 1 |
| STAT_LAMBDA_INTEGRATOR_1_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-te-tastverhaeltnis"></a>
### STATUS_TE_TASTVERHAELTNIS

Tastverhaeltnis TEV Read solenoid valve, tank ventillation (purge cannister)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TE_TASTVERHAELTNIS_WERT | real | Canister purge duty ratio |
| STAT_TE_TASTVERHAELTNIS_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-mdk-poti-spannung"></a>
### STATUS_MDK_POTI_SPANNUNG

Potentiometer Motordrosselklappe auslesen Read the throttle potentiometer signals

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MDK_POTI_SPANNUNG_1_WERT | real | Ergebnis Spannung MDK 1 Throttle position  1 |
| STAT_MDK_POTI_SPANNUNG_2_WERT | real | Ergebnis Spannung MDK 1 Throttle position  2 |
| STAT_MDK_POTI_SPANNUNG_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

Fahrerwunsch Read the pedal  signals

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PWG_POTI_SPANNUNG_1_WERT | real | Driver demand 1 |
| STAT_PWG_POTI_SPANNUNG_2_WERT | real | Driver demand 2 |
| STAT_PWG_POTI_SPANNUNG_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-pwg-winkel"></a>
### STATUS_PWG_WINKEL

PWG-Winkel auslesen Read the pedal  angle

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PWG_WINKEL_WERT | real | Ergebnis PWG-Winkel Driver demand |
| STAT_PWG_WINKEL_EINH | string | Einheit PWG-Winkel |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

Ansauglufttemperatur Read the air intake temperature

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Inlet air temperature |
| STATUS_AN_LUFTTEMPERATUR_WERT | real | Inlet air temperature |
| STAT_AN_LUFTTEMPERATUR_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Motortemperatur Read the engine coolant temperature

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOTORTEMPERATUR_WERT | real | Engine coolant temperature |
| STATUS_MOTORTEMPERATUR_WERT | real | Engine coolant temperature |
| STAT_MOTORTEMPERATUR_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Ubatt Read the battery voltage after relay

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_UBATT_WERT | real | Battery voltage after relay |
| STATUS_UBATT_WERT | real | Battery voltage after relay |
| STAT_UBATT_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-geberrad-adaption"></a>
### STATUS_GEBERRAD_ADAPTION

Geberradadaption Read the crank  adaption (engine is synchonized switch)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STATUS_GEBERRAD_ADAPTION_WERT | int | Flywheel adaption flag done |
| STAT_GEBERRAD_ADAPTION_WERT | int | Flywheel adaption flag done |
| STATUS_GEBERRAD_ADAPTION_EINH | string | Einheit inc |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status Schalteingaenge Read switches and I/O states

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FEHLERLAMPE_EIN | int | MIL lamp on 0=No / 1=Yes Fehlerlampe an 0=Nein / 1=Ja |
| STAT_KO_EIN | int | Air Conditioning switch on 0=No / 1=Yes Klima-Anforderung 0=Nein / 1=Ja |
| STAT_AC_EIN | int | Request Air Conditioning compressor 0=No / 1=Yes Anforderung Klimabereitschaft 0=Nein / 1=Ja |
| STAT_EWS_OK | int | Flag for successful communication EWS ok 0=Nein / 1=Ja |
| STAT_LV_EFP | int | Fuel pump active EKP angesteuert |
| STAT_CVT_VORHANDEN | int | Tranmission - automatic gearbox - TRANS_CONF in Siemens configuration data CVT verbaut 0=Nein / 1=Ja |
| STAT_ASC_VORHANDEN | int | Automatic stability control - LV_TCS_CONF in Siemens configuration data ASC verbaut 0=Nein / 1=Ja |
| STAT_KAT_VORHANDEN | int | Catalyst installed - LV_F_CONF in Siemens configuration data 1= vehicle is not in leaded fuel configuration, 0=leaded fuel KAT verbaut 0=Nein / 1=Ja |
| STAT_KLIMA_VORHANDEN | int | Aircon installed - LV_AC_CONF in Siemens configuation data Klima verbaut 0=Nein / 1=Ja |
| STAT_LAMBDAREGELUNG_1_EIN | int | Oxygen monitoring of exhaust fumes active Lambdaregelung 0=Nein / 1=Ja |
| STAT_LL_EIN | int | Engine at idle speed Leerlauf 0=Nein / 1=Ja |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read MIL lamp response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read AirCon response |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG Read EWS response |
| _TEL_ANTWORT4 | binary | Hex-Antwort von SG Read fuel pump response |
| _TEL_ANTWORT5 | binary | Hex-Antwort von SG Read Upstream oxygen sensor 1 response |
| _TEL_ANTWORT6 | binary | Hex-Antwort von SG Read configuration response |

<a id="job-status-lambda-add-1"></a>
### STATUS_LAMBDA_ADD_1

Gemischadaption additiv 1 Read adaption mixture additive bank 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LAMBDA_ADD_1_WERT | real | Rel. long term additive fuel trim |
| STAT_LAMBDA_ADD_1_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-lambda-mul-1"></a>
### STATUS_LAMBDA_MUL_1

Gemischadaption multipl. 1 Read adaption mixture multiplicative bank 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LAMBDA_MUL_1_WERT | real | Rel. long term multiplicative fuel trim |
| STAT_LAMBDA_MUL_1_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG ECU response packet |

<a id="job-status-digital-obdii"></a>
### STATUS_DIGITAL_OBDII

Status Schalteingaenge Read OBD2 Readiness flags

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation - OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MIL | int | MIL Status Ueberwachung MIL Status |
| ANZAHL_MIL | int | Count of ignition cycles during which MIL was on NB: This information is not available so this is always 0 !!! Anzahl von MIL Fehlern, immer 0 |
| STAT_RDY_LS | int | Oxygen monitoring completed Readiness flags of upstream and downstream O2 sensors both 0 Lambdasondenueberwachung |
| STAT_RDY_KKV | int | Catalyst monitoring completed (readiness flag of catalyst is 0) Katalysatorueberwachung |
| STAT_RDY_KVS | int | Fuel system monitoring completed (readiness flag of fuel system is 0) Readiness Kraftstoffsystem |
| STAT_RDY_AUS | int | Misfire monitoring completed (all misfire readiness flags are 0) Readiness Verbrennungsaussetzer |
| STAT_UBW_TES | int | Evaporative system monitoring completed (all EVAP readiness flags are 0) Ueberwachung Tankentlueftungssystem |
| KM_STAND_MIL_AN | long | Kilometers MIL on Kilometerstand MIL an This is the distance covered with the MIL active.  If the MIL is deactivated again (after the appropriate number of drive cycles without a fault), the distance covered when it was active is stored and returned If the MIL is then re-activated, the distance is reset to zero again |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Read MIL response |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG Read readiness flags response |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG Read Kilometers MIL on response |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (22 × 2)
- [LIEFERANTEN](#table-lieferanten) (45 × 2)
- [FREEZEFRAME](#table-freezeframe) (21 × 10)
- [DIGITAL](#table-digital) (195 × 4)
- [ANALOG](#table-analog) (208 × 4)
- [FORTTEXTE](#table-forttexte) (250 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (250 × 7)
- [FARTTEXTE](#table-farttexte) (10 × 2)
- [ACTUATOR_TEST](#table-actuator-test) (19 × 3)
- [APPLIC_CORRECTION](#table-applic-correction) (4 × 3)
- [ADAPTIVE_VALUES](#table-adaptive-values) (12 × 3)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 22 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x11 | DIENST NICHT UNTERSTÜTZT |
| 0x12 | UNTERFUNKTION NICHT UNTERSTÜTZT |
| 0x22 | BEDINGUNG NICHT RICHTIG |
| 0x31 | ABFRAGE AUSSERHALB BEREICH |
| 0x33 | BERECHTIGUNG VERWEIGERT / GEFORDERT |
| 0x35 | UNGÜLTIGE TASTE |
| 0x36 | ANZAHL DER VERSUCHE ÜBERSCHRITTEN |
| 0x37 | GEFORDERTE VERZÖGERUNGSZEIT NICHT ABGELAUFEN |
| 0x40 | HERUNTERLADEN NICHT AKZEPTIERT |
| 0x41 | FALSCHER HERUNTERLADEN-TYP |
| 0x42 | HERUNTERLADEN AUF ANGEGEBENE ADRESSE NICHT MÖGLICH |
| 0x50 | HOCHLADEN NICHT AKZEPTIERT |
| 0x52 | HOCHLADEN VON ANGEGEBENER ADRESSE NICHT MÖGLICH |
| 0x53 | HOCHLADEN DER ANGEFORDERTEN ANZAHL VON BYTES NICHT MÖGLICH |
| 0x78 | ANFORDERUNGRICHTIG EMPFANGEN - ANTWORT IN BEARBEITUNG |
| 0x79 | FALSCHER BYTE-ZÄHLWERT BEI BLOCKÜBERTRAGUNG |
| 0x80 | IN AKTUELLEM DIAGNOSEMODUS NICHT UNTERSTÜTZTER DIENST |
| 0x90 | VORGANG NICHT AUSGEFÜHRT |
| 0x91 | FALSCHES MELDUNGSFORMAT |
| 0xA0 | OKAY |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 45 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |

<a id="table-freezeframe"></a>
### FREEZEFRAME

Dimensions: 21 rows × 10 columns

| NAME | FACT_A | FACT_B | EINH | UWNR | POS | SIZE | MASK | TYPE | UWTEXT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FTL | 1.0 | 0.0 | L | 0x01 | 6 | 1 | 0xFF | 0 | Füllstand Kraftstofftank |
| OBD_TPS | 0.468627450 | 0.0 | Grad DK | 0x02 | 7 | 1 | 0xFF | 0 | Drosselklappenöffnung |
| OBD_PV_AV | 0.392156860 | 0.0 | % | 0x03 | 8 | 1 | 0xFF | 0 | Fahrerwunsch |
| VB_RLY | 0.112941180 | 0.0 | V | 0x04 | 9 | 1 | 0xFF | 0 | Batteriespannung |
| LV_CAN_TQ_STATE | 1.0 | 0.0 |  | 0x05 | 10 | 1 | 0x01 | 0 | Activierungsstatus ABS/ACS |
| LV_VS_ERR | 0.5 | 0.0 |  | 0x06 | 10 | 1 | 0x02 | 0 | Fehlerstatus Fahrgeschwindigkeit |
| LV_ACCOUT_RLY | 1.0 | 0.0 |  | 0x07 | 11 | 1 | 0x01 | 0 | Status Klimaanlage |
| LV_DRI | 1.0 | 0.0 |  | 0x08 | 12 | 1 | 0x01 | 0 | Status Getriebe |
| OBD_MAP_UP | 0.036621653 | 0.0 | hPa | 0x09 | 13 | 2 | 0xFF | 0 | Saugrohrdruck vor DK |
| CMD_TYPE | 1.0 | 0.0 |  | 0x0A | 15 | 1 | 0xFF | 0 | Art CVT-Befehl |
| OBD_TIA | 0.75 | -48.0 | Grad C | 0x0B | 16 | 1 | 0xFF | 0 | Einlasslufttemperatur |
| DIST_FAIL | 0.1 | 0.0 | km | 0x0D | 18 | 4 | 0xFF | 0 | Zurückgelegte Strecke bei Ausfall |
| STATE_LS1 | 1.0 | 0.0 |  | 0x0E | 22 | 1 | 0xFF | 0 | Status Kraftstoffsystem 1 |
| LOAD_CLC | 0.392156860 | 0.0 | % | 0x10 | 24 | 1 | 0xFF | 0 | Berechneter Lastwert |
| OBD_TCO | 0.75 | -48.0 | Grad C | 0x11 | 25 | 1 | 0xFF | 0 | Kühlmitteltemperatur/Motor |
| TI_LAM_1 | 0.001525902 | 0.0 | % | 0x12 | 26 | 2 | 0xFF | 1 | Kurzfristige Kraftstoffkorrektur, Zylinderreihe 1 |
| FUEL_AD_MMV_REL_1 | 0.001525902 | 0.0 | % | 0x13 | 28 | 2 | 0xFF | 1 | Langfristige Kraftstoffkorrektur, Zylinderreihe 1 |
| OBD_MAP | 0.036621653 | 0.0 | hPa | 0x16 | 35 | 2 | 0xFF | 0 | Saugrohr-Absolutdruck |
| N | 1.0 | 0.0 | 1/min | 0x17 | 37 | 2 | 0xFF | 0 | Motordrehzahl |
| VS | 1.0 | 0.0 | km/h | 0x18 | 39 | 1 | 0xFF | 0 | Fahrgeschwindigkeit |
| Unbekannter Gegenstand | 0.0 | 0.0 |  | 0x00 | 0 | 0 | 0xFF | 0 | Unbekannter Gegenstand |

<a id="table-digital"></a>
### DIGITAL

Dimensions: 195 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| LV_ASR_REQ | 6 | 0x01 | 0x01 |
| LV_MSR_REQ | 6 | 0x02 | 0x02 |
| LV_ASC_PAS | 6 | 0x04 | 0x04 |
| LV_GS_INH | 6 | 0x08 | 0x08 |
| LV_CAN_TQ_STATE | 7 | 0x02 | 0x02 |
| LV_VS_CAN_ERR_DET | 7 | 0x04 | 0x04 |
| LV_DSC_ACT | 10 | 0x04 | 0x04 |
| LV_TW_MSR_REQ | 7 | 0x20 | 0x20 |
| LV_TW_ASR_REQ | 7 | 0x40 | 0x40 |
| LV_KEY_OFF | 6 | 0x01 | 0x01 |
| LV_CAN_CRK_ERR | 6 | 0x02 | 0x02 |
| LV_TCS_ACK | 6 | 0x04 | 0x04 |
| LV_ACCOUT_RELAY | 6 | 0x40 | 0x40 |
| LV_MIL | 6 | 0x02 | 0x02 |
| LV_CRU_ON_LAMP | 6 | 0x08 | 0x08 |
| LV_WAL_1 | 6 | 0x10 | 0x10 |
| LV_CAN_TW_FLT | 9 | 0x01 | 0x01 |
| LV_TCS_TW_ACK | 9 | 0x02 | 0x02 |
| LV_CAN_GS | 6 | 0x08 | 0x08 |
| LV_SHIFTER_PARK | 6 | 0x01 | 0x01 |
| LV_SHIFTER_REVERSE | 6 | 0x02 | 0x02 |
| LV_SHIFTER_NEUTRAL | 6 | 0x04 | 0x04 |
| LV_SHIFTER_DRIVE | 6 | 0x08 | 0x08 |
| LV_SHIFTER_MANUAL | 6 | 0x10 | 0x10 |
| LV_SHIFTER_PLUS | 6 | 0x20 | 0x20 |
| LV_SHIFTER_MINUS | 6 | 0x40 | 0x40 |
| LV_SHIFTER_MODE | 6 | 0x80 | 0x80 |
| LV_WHEEL_PLUS | 7 | 0x01 | 0x01 |
| LV_WHEEL_MINUS | 7 | 0x02 | 0x02 |
| LV_SPARE_SWI_1 | 7 | 0x04 | 0x04 |
| LV_SPARE_SWI_2 | 7 | 0x08 | 0x08 |
| LV_GIB_CKS_ERR_DET | 7 | 0x10 | 0x10 |
| LV_GIB_CTL_ERR_DET | 7 | 0x20 | 0x20 |
| LV_ACCIN | 6 | 0x40 | 0x40 |
| LV_ACIN | 6 | 0x80 | 0x80 |
| LV_TIA_ERR | 6 | 0x01 | 0x01 |
| LV_TCO_ERR | 6 | 0x02 | 0x02 |
| LV_CAM_ERR | 6 | 0x04 | 0x04 |
| LV_CAM_ERR_LIH | 6 | 0x08 | 0x08 |
| LV_CAM_1_LEVEL | 6 | 0x10 | 0x10 |
| LV_CRK_ERR | 6 | 0x20 | 0x20 |
| LV_CRK_ERR_LIH | 6 | 0x40 | 0x40 |
| LV_MAP_ERR | 6 | 0x80 | 0x80 |
| LV_MAP_LIH | 7 | 0x01 | 0x01 |
| LV_TPS_ERR_1 | 7 | 0x02 | 0x02 |
| LV_TPS_ERR_2 | 7 | 0x04 | 0x04 |
| LV_ERR_IV_0 | 7 | 0x08 | 0x08 |
| LV_ERR_IV_1 | 7 | 0x10 | 0x10 |
| LV_ERR_IV_2 | 7 | 0x20 | 0x20 |
| LV_ERR_IV_3 | 7 | 0x40 | 0x40 |
| LV_TCO_EX_ERR | 7 | 0x80 | 0x80 |
| LV_PVS_ERR_1 | 8 | 0x01 | 0x01 |
| LV_PVS_ERR_2 | 8 | 0x02 | 0x02 |
| LV_MTC_AD_ERR | 8 | 0x04 | 0x04 |
| LV_MTC_CTL_ERR | 8 | 0x08 | 0x08 |
| LV_AC_PRS_ERR | 8 | 0x10 | 0x10 |
| LV_ERR_PRES_TLDP_EOL | 8 | 0x20 | 0x20 |
| LV_MAP_UP_ERR | 9 | 0x01 | 0x01 |
| LV_ERR_CPS | 9 | 0x02 | 0x02 |
| LV_ERR_EFP | 9 | 0x04 | 0x04 |
| LV_ERR_CAN_ASC | 9 | 0x08 | 0x08 |
| LV_ERR_CAN_EGS | 9 | 0x10 | 0x10 |
| LV_ERR_CAN_INSTR | 9 | 0x20 | 0x20 |
| LV_ERR_BOFF | 10 | 0x01 | 0x01 |
| LV_EFP | 10 | 0x02 | 0x02 |
| LV_AST | 10 | 0x04 | 0x04 |
| LV_IS | 10 | 0x08 | 0x08 |
| LV_PL | 10 | 0x20 | 0x20 |
| LV_PU | 10 | 0x40 | 0x40 |
| LV_PUC | 10 | 0x80 | 0x80 |
| LV_FL | 11 | 0x01 | 0x01 |
| LV_CT | 11 | 0x02 | 0x02 |
| LV_MAIN_RLY | 11 | 0x04 | 0x04 |
| LV_BLS | 11 | 0x08 | 0x08 |
| LV_BTS | 11 | 0x10 | 0x10 |
| LV_CS_CRU | 11 | 0x20 | 0x20 |
| LV_IN_RS_TLDP | 11 | 0x40 | 0x40 |
| LV_PRNDM_FAULT | 12 | 0x01 | 0x01 |
| LV_VS_CVT_ERR | 12 | 0x02 | 0x02 |
| LV_RATIO_PLAUS_ERR | 12 | 0x04 | 0x04 |
| LV_TRANS_OIL_TEMP_ERR | 12 | 0x08 | 0x08 |
| LV_SHIFT_IN_PROGRESS | 12 | 0x10 | 0x10 |
| LV_ASR_AUTH | 12 | 0x20 | 0x20 |
| LV_MSR_AUTH | 12 | 0x40 | 0x40 |
| LV_CLUTCH_LOCKED | 12 | 0x80 | 0x80 |
| LV_MIL_ALSO | 6 | 0x01 | 0x01 |
| LV_ACCOUT_RLY_ALSO | 6 | 0x02 | 0x02 |
| LV_CFA_1 | 6 | 0x04 | 0x04 |
| LV_CFA_2 | 6 | 0x08 | 0x08 |
| LV_CFA_3 | 6 | 0x10 | 0x10 |
| LV_KEY_ON | 7 | 0x01 | 0x01 |
| LV_ACIN_ALSO | 7 | 0x04 | 0x04 |
| LV_ACCIN_ALSO | 7 | 0x08 | 0x08 |
| LV_AC_FAN_REQ_1 | 7 | 0x10 | 0x10 |
| LV_AFR_1 | 8 | 0x01 | 0x01 |
| LV_LSCL_1 | 8 | 0x02 | 0x02 |
| LV_LS_UP | 8 | 0x04 | 0x04 |
| LV_LS_DOWN | 8 | 0x08 | 0x08 |
| LV_RUN_ENG | 9 | 0x01 | 0x01 |
| LV_SYN_ENG | 9 | 0x02 | 0x02 |
| LV_ES | 9 | 0x04 | 0x04 |
| LV_ST | 9 | 0x08 | 0x08 |
| LV_MSR_ACT | 9 | 0x10 | 0x10 |
| LV_ASR_ACT | 9 | 0x20 | 0x20 |
| LV_TPS_AD_REQ | 9 | 0x40 | 0x40 |
| LV_ERR_IMOB_03 | 6 | 0x01 | 0x01 |
| LV_ERR_IMOB_04 | 6 | 0x02 | 0x02 |
| LV_SEED_KEY_INI | 6 | 0x04 | 0x04 |
| LV_NOT_LEARNT_MEM_IMOB | 6 | 0x08 | 0x08 |
| LV_LOCK_IMOB | 6 | 0x10 | 0x10 |
| LV_ANS_ERR_IMOB | 6 | 0x20 | 0x20 |
| LV_ANS_ERR_COM_IMOB | 6 | 0x40 | 0x40 |
| LV_ANS_NOT_IMOB | 7 | 0x01 | 0x01 |
| LV_SEG_T_AD_ERR | 37 | 0x01 | 0x01 |
| LV_SEG_AD_STATE | 37 | 0x02 | 0x02 |
| LV_END_CAT_DIAG_EOL | 37 | 0x04 | 0x04 |
| LV_AUTH_CAT_DIAG_EOL | 37 | 0x08 | 0x08 |
| LV_ERR_PRES_LS_DOWN_EOL | 37 | 0x10 | 0x10 |
| LV_END_TLDP_DIAG_EOL | 37 | 0x20 | 0x20 |
| LV_ERR_PRES_TLDP_EOL_ONE | 37 | 0x40 | 0x40 |
| LV_ERR_PRES_CAT_EOL | 37 | 0x80 | 0x80 |
| LV_ERR_PRES_0_TLDP | 65 | 0x01 | 0x01 |
| LV_ERR_PRES_1_TLDP | 65 | 0x02 | 0x02 |
| LV_ERR_PRES_2_TLDP | 65 | 0x04 | 0x04 |
| LV_ERR_PRES_3_TLDP | 65 | 0x08 | 0x08 |
| LV_ERR_PRES_4_TLDP | 65 | 0x10 | 0x10 |
| LV_ERR_PRES_5_TLDP | 65 | 0x20 | 0x20 |
| LV_ERR_PRES_6_TLDP | 65 | 0x40 | 0x40 |
| LV_ERR_PRES_7_TLDP | 65 | 0x80 | 0x80 |
| LV_CRU_CTL_ACT | 6 | 0x01 | 0x01 |
| LV_CRU_CTL_AUTH | 6 | 0x02 | 0x02 |
| LV_CRU_SWI_ON_OFF | 6 | 0x04 | 0x04 |
| LV_CRU_SWI_RES | 6 | 0x08 | 0x08 |
| LV_CRU_SWI_SET_POS | 6 | 0x10 | 0x10 |
| LV_CRU_SWI_SET_MINUS | 6 | 0x20 | 0x20 |
| LV_BLS_1 | 7 | 0x01 | 0x01 |
| LV_CS_CRU_1 | 7 | 0x02 | 0x02 |
| LV_DRIV_1 | 7 | 0x04 | 0x04 |
| LV_N_CRU_AUTH_1 | 7 | 0x08 | 0x08 |
| LV_VS_CRU_ON_AUTH_1 | 7 | 0x10 | 0x10 |
| LV_ASR_MSR_ACT_1 | 7 | 0x20 | 0x20 |
| LV_VS_RATIO_DFT_1 | 7 | 0x40 | 0x40 |
| LV_CRU_SWI_ON_OFF_1 | 7 | 0x80 | 0x80 |
| LV_BLS_2 | 8 | 0x01 | 0x01 |
| LV_CS_CRU_2 | 8 | 0x02 | 0x02 |
| LV_DRIV_2 | 8 | 0x04 | 0x04 |
| LV_N_CRU_AUTH_2 | 8 | 0x08 | 0x08 |
| LV_VS_CRU_ON_AUTH_2 | 8 | 0x10 | 0x10 |
| LV_ASR_MSR_ACT_2 | 8 | 0x20 | 0x20 |
| LV_VS_RATIO_DFT_2 | 8 | 0x40 | 0x40 |
| LV_CRU_SWI_ON_OFF_2 | 8 | 0x80 | 0x80 |
| LV_BLS_3 | 9 | 0x01 | 0x01 |
| LV_CS_CRU_3 | 9 | 0x02 | 0x02 |
| LV_DRIV_3 | 9 | 0x04 | 0x04 |
| LV_N_CRU_AUTH_3 | 9 | 0x08 | 0x08 |
| LV_VS_CRU_ON_AUTH_3 | 9 | 0x10 | 0x10 |
| LV_ASR_MSR_ACT_3 | 9 | 0x20 | 0x20 |
| LV_VS_RATIO_DFT_3 | 9 | 0x40 | 0x40 |
| LV_CRU_SWI_ON_OFF_3 | 9 | 0x80 | 0x80 |
| LV_BLS_4 | 10 | 0x01 | 0x01 |
| LV_CS_CRU_4 | 10 | 0x02 | 0x02 |
| LV_DRIV_4 | 10 | 0x04 | 0x04 |
| LV_N_CRU_AUTH_4 | 10 | 0x08 | 0x08 |
| LV_VS_CRU_ON_AUTH_4 | 10 | 0x10 | 0x10 |
| LV_ASR_MSR_ACT_4 | 10 | 0x20 | 0x20 |
| LV_VS_RATIO_DFT_4 | 10 | 0x40 | 0x40 |
| LV_CRU_SWI_ON_OFF_4 | 10 | 0x80 | 0x80 |
| LV_BLS_5 | 11 | 0x01 | 0x01 |
| LV_CS_CRU_5 | 11 | 0x02 | 0x02 |
| LV_DRIV_5 | 11 | 0x04 | 0x04 |
| LV_N_CRU_AUTH_5 | 11 | 0x08 | 0x08 |
| LV_VS_CRU_ON_AUTH_5 | 11 | 0x10 | 0x10 |
| LV_ASR_MSR_ACT_5 | 11 | 0x20 | 0x20 |
| LV_VS_RATIO_DFT_5 | 11 | 0x40 | 0x40 |
| LV_CRU_SWI_ON_OFF_5 | 11 | 0x80 | 0x80 |
| LV_OIL_LEVEL_TEST_OK | 6 | 0x40 | 0x40 |
| LV_READY_EVAP_1 | 6 | 0x10 | 0x10 |
| LV_READY_EVAP_2 | 6 | 0x20 | 0x20 |
| LV_READY_EVAP_3 | 6 | 0x40 | 0x40 |
| LV_READY_EVAP_4 | 6 | 0x80 | 0x80 |
| LV_READY_MIS_A | 8 | 0x04 | 0x04 |
| LV_READY_MIS_B1 | 8 | 0x08 | 0x08 |
| LV_READY_MIS_B4 | 8 | 0x10 | 0x10 |
| LV_READY_FSD_1 | 8 | 0x20 | 0x20 |
| LV_READY_OBD | 8 | 0x80 | 0x80 |
| LV_READY_LS_UP_1 | 9 | 0x01 | 0x01 |
| LV_READY_LS_DOWN_1 | 9 | 0x04 | 0x04 |
| LV_READY_CAT_1 | 9 | 0x10 | 0x10 |
| LV_CLU_CAL_DONE_D | 16 | 0x01 | 0x01 |
| LV_CLU_CAL_DONE_R | 16 | 0x02 | 0x02 |
| LV_CLU_ADAPT_D_MAX_FAULT | 16 | 0x04 | 0x04 |
| LV_CLU_ADAPT_D_MIN_FAULT | 16 | 0x08 | 0x08 |
| LV_CLU_ADAPT_R_MAX_FAULT | 16 | 0x10 | 0x10 |
| LV_CLU_ADAPT_R_MIN_FAULT | 16 | 0x20 | 0x20 |
| ?? | FF | 0x00 | 0xFF |

<a id="table-analog"></a>
### ANALOG

Dimensions: 208 rows × 4 columns

| NAME | FACT_A | FACT_B | EINH |
| --- | --- | --- | --- |
| CAN_VS_BAS | 0.06258 | 0.0 | km/h |
| CAN_TQI_ASR | 0.3906525 | 0.0 | % |
| CAN_TQI_MSR | 0.3906525 | 0.0 | % |
| CAN_VRD_LV_ASC | 0.06258 | 0.0 | km/h |
| CAN_VRD_RV_ASC | 0.06258 | 0.0 | km/h |
| CAN_VRD_LH_ASC | 0.06258 | 0.0 | km/h |
| CAN_VRD_RH_ASC | 0.06258 | 0.0 | km/h |
| CAN_RR | 0.08 | 0.0 | G |
| CAN_TQI_TW_ASR | 0.001525902 | 0.0 | % |
| CAN_TQI_TW_MSR | 0.001525902 | 0.0 | % |
| TQ_COR_STATE | 1.0 | 0.0 |  |
| CAN_TQI_AV | 0.3906525 | 0.0 | % |
| CAN_N | 1.0 | 0.0 | 1/min |
| CAN_TQI_BAS | 0.3906525 | 0.0 | % |
| CAN_TQI_LOSS | 0.3906525 | 0.0 | % |
| CAN_MUL_INFO | 1.0 | 0.0 |  |
| CAN_MUL_COD | 1.0 | 0.0 |  |
| CAN_TCO | 0.75 | -48.0 | Grad C |
| CAN_CRU_SET_LAMP | 1.0 | 0.0 |  |
| CAN_PV_AV | 0.392156860 | 0.0 | % |
| TI_SUM_FCO | 1.0 | 0.0 | Microliter |
| CAN_DES_AIM_POSITION | 0.5 | 0.0 | Schritte |
| CAN_DES_CMD_TYPE | 1.0 | 0.0 |  |
| CAN_DES_AIM_SPEED | 1.0 | 0.0 |  |
| CAN_DES_CLU_SOL_DR | 0.195694720 | 0.0 | % |
| CAN_CLUTCH_CODES | 1.0 | 0.0 |  |
| CAN_DES_SDRY_PRES_DR | 0.195694720 | 0.0 | % |
| CAN_SDRY_PRES_CODES | 1.0 | 0.0 |  |
| CAN_MAP | 1.0 | -100.0 | kPa |
| CAN_TQ_AT_WHEELS_WOUT_LOSS | 0.03125 | 0.0 | Nm |
| CAN_TW_NORM | 20.0 | 0.0 | Nm |
| CAN_TW_TQ_LOSS | 0.03125 | 0.0 | Nm |
| CAN_TW_TQI_REQ_TRA | 0.0015259 | 0.0 | % |
| CAN_GR_AT | 1.0 | 0.0 |  |
| CAN_L_GS | 1.0 | 0.0 |  |
| CAN_GR_AT_SEL | 1.0 | 0.0 |  |
| CAN_GR_MOD | 1.0 | 0.0 |  |
| CAN_CURRENT_POSITION | 0.5 | 0.0 | Schritte |
| CAN_MOTOR_CDN_COD | 1.0 | 0.0 |  |
| CAN_DRIV_LED_STATUS | 1.0 | 0.0 |  |
| CAN_CLU_AV_DR | 0.195694720 | 0.0 | % |
| CAN_CLU_CDN_COD | 1.0 | 0.0 |  |
| CAN_DRIV_LED_ERR | 1.0 | 0.0 |  |
| CAN_SDRY_PRS_AV_DR | 0.195694720 | 0.0 | % |
| CAN_SDRY_PRS_CDN_COD | 1.0 | 0.0 |  |
| CAN_GIB_SW_NR | 1.0 | 0.0 |  |
| CAN_DIST | 10.0 | 0.0 | km |
| CAN_FTL | 1.0 | 0.0 | L |
| CAN_AC_TEMP | 0.364 | -30.0 | Grad C |
| STATE_CP | 1.0 | 0.0 |  |
| ALTER | 0.001525902 | 0.0 | % |
| TCO_BAS | 0.004887586 | 0.0 | V |
| TIA_BAS | 0.004887586 | 0.0 | V |
| MAP_BAS | 0.004887586 | 0.0 | V |
| MAP_UP_BAS | 0.004887586 | 0.0 | V |
| TCO_EX_BAS | 0.004887586 | 0.0 | V |
| TOIL_CVT_BAS | 0.004887586 | 0.0 | V |
| AC_PRS_BAS | 0.004887586 | 0.0 | V |
| TPS_1_BAS | 0.004887586 | 0.0 | V |
| TPS_2_BAS | 0.004887586 | 0.0 | V |
| PVS_1_BAS | 0.004887586 | 0.0 | V |
| PVS_2_BAS | 0.004887586 | 0.0 | V |
| VLS_UP_1_BAS | 0.004887586 | 0.0 | V |
| VLS_DOWN_1_BAS | 0.004887586 | 0.0 | V |
| VBK_BAS | 0.028152492 | 0.0 | V |
| VBR_BAS | 0.028152492 | 0.0 | V |
| TCO | 0.75 | -48.0 | Grad C |
| TIA | 0.75 | -48.0 | Grad C |
| MAP | 0.036621653 | 0.0 | hPa |
| MAP_UP | 0.036621653 | 0.0 | hPa |
| TCO_EX | 0.75 | -48.0 | Grad C |
| TRANS_OIL_TEMP | 1.0 | -50.0 | Grad C |
| AC_PRS | 0.156862750 | 0.0 | bar |
| TPS_MTC_1 | 0.001823 | 0.0 | Grad DK |
| TPS_MTC_2 | 0.001823 | 0.0 | Grad DK |
| TPS | 0.468627450 | 0.0 | Grad DK |
| PV_AV_1 | 0.392156860 | 0.0 | % |
| PV_AV_2 | 0.392156860 | 0.0 | % |
| PV_AV | 0.392156860 | 0.0 | % |
| VLS_UP_1 | 0.004887586 | 0.0 | V |
| VLS_DOWN_1 | 0.004887586 | 0.0 | V |
| VB_RLY | 0.112941180 | 0.0 | V |
| VB_KEY | 0.112941180 | 0.0 | V |
| KNKS_BAS | 0.00489 | 0.0 | V |
| IGA_CYL_KNK0 | 0.001459144 | 0.0 | Grad KW |
| KNKWB_0 | 1.0 | 0.0 | Grad KW |
| KNKWD_0 | 1.0 | 0.0 | Grad KW |
| KNK_EGY_0 | 1.0 | 0.0 |  |
| KNKS_0 | 1.0 | 0.0 |  |
| IGA_IGC_0 | -0.375 | 72.0 | Grad KW |
| IGA_IGC_1 | -0.375 | 72.0 | Grad KW |
| IGA_IGC_2 | -0.375 | 72.0 | Grad KW |
| IGA_IGC_3 | -0.375 | 72.0 | Grad KW |
| IGA_SP | 0.375 | -23.625 | Grad KW |
| LSHPWM_UP_1 | 0.001525902 | 0.0 | % |
| LSHPWM_DOWN | 0.001525902 | 0.0 | % |
| MAF_KGH | 0.25 | 0.0 | kg/h |
| MAP_SP | 0.036621653 | 0.0 | hPa |
| MAP_UP_SP | 0.036621653 | 0.0 | hPa |
| TPS_SP_CLC | 0.001823 | 0.0 | Grad DK |
| V_TPS_AD_BOL_1 | 0.004887586 | 0.0 | V |
| V_TPS_AD_BOL_2 | 0.004887586 | 0.0 | V |
| V_TPS_AD_EL_BOL_1 | 0.004887586 | 0.0 | V |
| V_TPS_AD_EL_BOL_2 | 0.004887586 | 0.0 | V |
| V_TPS_AD_LIH_1 | 0.004887586 | 0.0 | V |
| V_TPS_AD_LIH_2 | 0.004887586 | 0.0 | V |
| N_SP_IS | 1.0 | 0.0 | 1/min |
| TPS_LIH | 0.001823 | 0.0 | Grad DK |
| TI_LAM_1 | 0.001525902 | 0.0 | % |
| LAM_MV_1 | 0.001525902 | 0.0 | % |
| TI_AD_ADD_MMV_0 | 0.004 | 0.0 | ms |
| TI_AD_ADD_MMV_REL_0 | 0.004 | 0.0 | ms |
| TI_AD_FAC_MMV_0 | 0.001525902 | 0.0 | % |
| TI_AD_FAC_MMV_REL_0 | 0.001525902 | 0.0 | % |
| VB | 0.112941180 | 0.0 | V |
| VS | 1.0 | 0.0 | km/h |
| N | 1.0 | 0.0 | 1/min |
| VS_CVT | 0.1 | 0.0 | km/h |
| GR_MT | 1.0 | 0.0 |  |
| GR_AT | 1.0 | 0.0 |  |
| CPPWM | 0.392156860 | 0.0 | % |
| LOAD_CLC | 0.392156860 | 0.0 | % |
| TIPR | 0.016 | 0.0 | ms |
| TI_V_000 | 0.0039999542 | 0.0 | ms |
| CTR_SDR_1_IMOB | 1.0 | 0.0 |  |
| CTR_SDR_2_IMOB | 1.0 | 0.0 |  |
| CTR_SDR_3_IMOB | 1.0 | 0.0 |  |
| VLS_CYC_MMV_EOL_1 | 0.01 | 0.0 | s |
| VLSH_UP_1 | 0.004887586 | 0.0 | V |
| VLSH_DOWN_1 | 0.004887586 | 0.0 | V |
| MIS_B0 | 1.0 | 0.0 |  |
| MIS_B1 | 1.0 | 0.0 |  |
| MIS_B2 | 1.0 | 0.0 |  |
| MIS_B3 | 1.0 | 0.0 |  |
| ER_000 | 1.0 | 0.0 | Mikrosekunde |
| ER_001 | 1.0 | 0.0 | Mikrosekunde |
| ER_002 | 1.0 | 0.0 | Mikrosekunde |
| ER_003 | 1.0 | 0.0 | Mikrosekunde |
| ER_MMV_EOL_000 | 0.00122 | 0.0 | Mikrosekunde |
| ER_MMV_EOL_001 | 0.00122 | 0.0 | Mikrosekunde |
| ER_MMV_EOL_002 | 0.00122 | 0.0 | Mikrosekunde |
| ER_MMV_EOL_003 | 0.00122 | 0.0 | Mikrosekunde |
| ER_THD_000 | 1.0 | 0.0 | Mikrosekunde |
| ER_THD_001 | 1.0 | 0.0 | Mikrosekunde |
| ER_THD_002 | 1.0 | 0.0 | Mikrosekunde |
| ER_THD_003 | 1.0 | 0.0 | Mikrosekunde |
| FAIL_TLDP_EOL | 1.0 | 0.0 |  |
| CMD_TYPE | 1.0 | 0.0 |  |
| MODE_CURRENT | 1.0 | 0.0 |  |
| ENG_SPD_TARGET | 1.0 | 0.0 | 1/min |
| CVT_DFT_TOT_DIST | 0.1 | 0.0 | km |
| T_CVT_MODE_NEUTRAL | 1.0 | 0.0 | s |
| T_CVT_MODE_DRIVE | 1.0 | 0.0 | s |
| T_CVT_MODE_SPORT | 1.0 | 0.0 | s |
| T_CVT_MODE_MANUAL | 1.0 | 0.0 | s |
| T_CVT_ENG_RUN | 1.0 | 0.0 | s |
| TAB_IP_TRAN_CRV_ADJUST_00 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_01 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_02 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_03 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_04 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_05 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_06 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_07 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_08 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_09 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_10 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_11 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_12 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_13 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_14 | 0.5 | -255.0 | Schritte |
| TAB_IP_TRAN_CRV_ADJUST_15 | 0.5 | -255.0 | Schritte |
| FAST_ADAPT | 1.0 | 0.0 |  |
| BP_ADAPTION_D | 0.1956 | 0.0 | % |
| BP_ADAPTION_R | 0.1956 | 0.0 | % |
| CLU_BITE_POINT_EOL_D | 0.1956 | 0.0 | % |
| CLU_BITE_POINT_EOL_R | 0.1956 | 0.0 | % |
| LONG_TERM_ADPT_D | 0.1956 | 0.0 | % |
| LONG_TERM_ADPT_R | 0.1956 | 0.0 | % |
| CVT_ADAPT_1 | 1.0 | 0.0 |  |
| CLU_MOD_ACTIVE | 1.0 | 0.0 |  |
| TQ_AV | 0.03125 | 0.0 | Nm |
| TQ_DIF_IS_AD | 0.03125 | 0.0 | Nm |
| TQ_DIF_I_IS | 0.03125 | 0.0 | Nm |
| TQ_DIF_P_D_IS | 0.03125 | 0.0 | Nm |
| DIF_AR_RED | 0.000976563 | 0.0 | cm2 |
| SLOP_AR_RED | 0.001525902 | 0.0 | % |
| DIF_MAF_SCHA_SAV | 0.25 | 0.0 | kg/h |
| DIST_ACT_MIL | 0.1 | 0.0 | km |
| DIST_ACT_WAL_1 | 0.1 | 0.0 | km |
| DIST_ACT_WAL_2 | 0.1 | 0.0 | km |
| DOWN_DYN_MEM_CAT | 0.003891051 | 0.0 |  |
| VLS_CYC_SUM_MEM | 0.01 | 0.0 | s |
| VLS_CYC_MAX_MEM | 0.01 | 0.0 | s |
| SEG_AD_MMV_000 | 0.061035156 | 0.0 | % |
| SEG_AD_MMV_001 | 0.061035156 | 0.0 | % |
| SEG_AD_MMV_002 | 0.061035156 | 0.0 | % |
| SEG_AD_MMV_003 | 0.061035156 | 0.0 | % |
| CTR_CDN_RBM_TLDP | 1.0 | 0.0 |  |
| CTR_COMP_RBM_TLDP | 1.0 | 0.0 |  |
| CTR_CDN_RBM_LS_UP_DIAG | 1.0 | 0.0 |  |
| CTR_COMP_RBM_LS_UP_DIAG | 1.0 | 0.0 |  |
| CTR_CDN_RBM_CAT_DIAG | 1.0 | 0.0 |  |
| CTR_COMP_RBM_CAT_DIAG | 1.0 | 0.0 |  |
| CTR_IGK_CYC_RBM | 1.0 | 0.0 |  |
| CTR_CDN_OBD_RBM | 1.0 | 0.0 |  |
| N_SP_ADD_KWP_LTA | 1.0 | 0.0 |  |
| Unbekannter Gegenstand | 0.0 | 0 |  |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 250 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0071 | Ambient Lufteinlass Temperatursensor Range/Performance ungültiger Wert |
| 0x113C | Lufteinlass Temperatur TIA haengender Wert |
| 0x113D | Temperatur Lufteinlass ungültige Werte |
| 0x316B | Temperatursignal Motorlüfter haengt unter Einschalttemperatur |
| 0x316A | Temperatursignal Motorlüfter zu hoch |
| 0x0700 | AISIN TCU OBD relevanter Fehler |
| 0x101F | Temperatur Lufteinlass und ungültige Werte der Aussentemperatur-Sensoren |
| 0x0070 | Fehlfunktion Aussentemperatur-Sensor oder Stromkreis unterbrochen |
| 0x0113 | Intake Air Temperature Circuit High Input |
| 0x0112 | Intake Air Temperature Circuit Low Input |
| 0x0114 | Stromkreis Ansauglufttemperatur, zeitw. unterbr. |
| 0x0108 | Stromkreis Saugrohr-Absolutdruck/Atmosphärendruck, Eingang hoch |
| 0x0107 | Stromkreis Saugrohr-Absolutdruck/Atmosphärendruck, Eingang niedrig |
| 0x0109 | Stromkreis Saugrohr-Absolutdruck/Atmosphärendruck, zeitw. unterbr. |
| 0x1106 | Saugrohrdrucksensor zu niedrig bei Motorstillstand |
| 0x1107 | Saugrohrdrucksensor zu niedrig im Leerlauf |
| 0x1108 | Saugrohrdrucksensor zu niedrig bei Vollast für niedrige Motordrehzahl |
| 0x1109 | Saugrohrdruck zu hoch im Schiebebetrieb |
| 0x1238 | Sekundär-Saugrohrdrucksensor vor DK, Eingang hoch |
| 0x1237 | Sekundär-Saugrohrdrucksensor vor DK, Eingang niedrig |
| 0x1235 | Sekundär-Saugrohrdrucksensor vor DK, Stromkreis zeitw. unterbr. |
| 0x1239 | Sekundär-Saugrohrdrucksensor vor DK zu niedrig bei Motorstillstand |
| 0x1240 | Sekundär-Saugrohrdrucksensor vor DK zu niedrig im Leerlauf |
| 0x1241 | Sekundär-Saugrohrdrucksensor vor DK zu niedrig bei Vollast für niedrige Motordrehzahl |
| 0x1242 | Sekundär-Saugrohrdrucksensor vor DK zu hoch im Schiebebetrieb |
| 0x1499 | Ansaugluftfilter undicht |
| 0x1497 | Luftundichtigkeit nach DK |
| 0x1498 | Luftundichtigkeit nach Lader |
| 0x0118 | Engine Coolant Temperature Circuit High Input |
| 0x0117 | Engine Coolant Temperature Circuit Low Input |
| 0x0116 | Engine Coolant Temperature Circuit Circuit Range/ Performance Problem |
| 0x0125 | Kühlmitteltemperatur nicht ausreichend für Lambaregelung |
| 0x0128 | Kühlmittelthermostat (Kühlmitteltemperatur unter Thermostat-Regeltemperatur) |
| 0x0119 | Kühlmitteltemperatur/Motor, Stromkreis zeitw. unterbr. |
| 0x0234 | Overboost (Ladedrucküberschreitung) |
| 0x1112 | Kühlmitteltemperatur/Motor, Sensor Kühlerauslauf, Eingang hoch |
| 0x1111 | Kühlmitteltemperatur/Motor, Sensor Kühlerauslauf, Eingang niedrig |
| 0x1113 | Kühlmitteltemperatur/Motor, Sensor Kühlerauslauf, zeitw. unterbr. |
| 0x0132 | Stromkreis Lambasonde, Spannung hoch (Reihe1 Sensor1) |
| 0x0131 | Stromkreis Lambasonde, Spannung niedrig (Reihe1 Sensor1) |
| 0x0130 | Stromkreis Lambasonde (Reihe1 Sensor1) |
| 0x0032 | Steuerstromkreis Sondenheizung hoch (Reihe1 Sensor1) |
| 0x0031 | Steuerstromkreis Sondenheizung niedrig (Reihe1 Sensor1) |
| 0x0030 | Steuerstromkreis Sondenheizung (Reihe1 Sensor1) |
| 0x0135 | Stromkreis Sondenheizung (Reihe1 Sensor1) |
| 0x0053 | HO2S Heizwiderstand (Bank1 Sensor1) |
| 0x0138 | Stromkreis Lambasonde, Spannung hoch (Reihe1 Sensor2) |
| 0x0137 | Stromkreis Lambasonde, Spannung niedrig (Reihe1 Sensor2) |
| 0x0136 | Funktionsstörung Stromkreis Lambasonde (Reihe1 Sensor2) |
| 0x0038 | Steuerstromkreis Sondenheizung hoch (Reihe1 Sensor2) |
| 0x0037 | Steuerstromkreis Sondenheizung niedrig (Reihe1 Sensor2) |
| 0x0036 | Steuerstromkreis Sondenheizung (Reihe1 Sensor2) |
| 0x0141 | Stromkreis Sondenheizung (Reihe1 Sensor2) |
| 0x0054 | HO2S Heizwiderstand (Bank1 Sensor2) |
| 0x0262 | Stromkreis Einspritzventil Zylinder 1 hoch |
| 0x0261 | Stromkreis Einspritzventil Zylinder 1 niedrig |
| 0x0201 | Stromkreis Einspritzventil - Zylinder 1 |
| 0x0265 | Stromkreis Einspritzventil Zylinder 2 hoch |
| 0x0264 | Stromkreis Einspritzventil Zylinder 2 niedrig |
| 0x0202 | Stromkreis Einspritzventil - Zylinder 2 |
| 0x0268 | Stromkreis Einspritzventil Zylinder 3 hoch |
| 0x0267 | Stromkreis Einspritzventil Zylinder 3 niedrig |
| 0x0203 | Stromkreis Einspritzventil - Zylinder 3 |
| 0x0271 | Stromkreis Einspritzventil Zylinder 4 hoch |
| 0x0270 | Stromkreis Einspritzventil Zylinder 4 niedrig |
| 0x0204 | Stromkreis Einspritzventil - Zylinder 4 |
| 0x1236 | Primärkreis Relais/Kraftstoffpumpe hoch |
| 0x1234 | Primärkreis Relais/Kraftstoffpumpe niedrig |
| 0x0171 | System zu mager (Reihe1) |
| 0x0172 | System zu fett (Reihe1) |
| 0x0133 | Stromkreis Lambasonde, Reaktion zu langsam (Reihe1 Sensor1) |
| 0x0139 | Stromkreis Lambasonde, Reaktion zu langsam (Reihe1 Sensor2) |
| 0x1143 | Prüfsignal Sondenaktivität zu hoch (Reihe1 Sensor 2) |
| 0x1144 | Prüfsignal Sondenaktivität zu niedrig (Reihe1 Sensor 2) |
| 0x2271 | Lambdasondensignal bei fett haengend (Bank 1 Sensor 2) |
| 0x2270 | Lambdasondensignal bei mager haengend (Bank 1 Sensor 2) |
| 0x2096 | Kraftstoffkorrektursystem nach Kat zu mager, Reihe1 |
| 0x2097 | Kraftstoffkorrektursystem nach Kat zu fett, Reihe1 |
| 0x0340 | Stromkreis Nockenwinkelsensor A (Reihe1 oder Einzelsensor) |
| 0x0341 | Stromkreis Nockenwinkelsensor A, Bereich/Betriebsgüte (Reihe1 oder Einzelsensor) |
| 0x0351 | Zündspule A, Primär-/Sekundärkreis |
| 0x1366 | Zündspule A, Primär-/Sekundärkreis niedrig |
| 0x0352 | Zündspule B, Primär-/Sekundärkreis |
| 0x1367 | Zündspule B, Primär-/Sekundärkreis niedrig |
| 0x2301 | Zündspule A, Primärsteuerkreis hoch |
| 0x2300 | Zündspule A, Primärsteuerkreis niedrig |
| 0x2304 | Zündspule B, Primärsteuerkreis niedrig |
| 0x2303 | Zündspule B, Primärsteuerkreis hoch |
| 0x0326 | Stromkreis Klopfsensor 1, Bereich/Betriebsgüte (Reihe1 oder Einzelsensor) |
| 0x0324 | Fehler in Klopfregelung |
| 0x1340 | Fehlzündg. beim Start, Mehrfachfehler |
| 0x0300 | Fehlzündg. erkannt, stochastisch/mehrere Zyl. |
| 0x1341 | Kat-schäd. Fehlzündg., Mehrfachfehler |
| 0x1342 | Fehlzündg. beim Start, Zylinder 1 |
| 0x0301 | Fehlzündg. Zylinder 1 erkannt |
| 0x1343 |   |
| 0x1344 | Fehlzündg. beim Start, Zylinder 2 |
| 0x0302 | Fehlzündg. Zylinder 2 erkannt |
| 0x1345 | Kat-schäd. Fehlzündg. Zylinder 2 |
| 0x1346 | Fehlzündg. beim Start Zylinder 3 |
| 0x0303 | Fehlzündg. Zylinder 3 erkannt |
| 0x1347 | Kat-schäd. Fehlzündg. Zylinder 3 |
| 0x1348 | Fehlzündg. beim Start Zylinder 4 |
| 0x0304 | Fehlzündg. Zylinder 4 erkannt |
| 0x1349 | Kat-schäd. Fehlzündg. Zylinder 4 |
| 0x0313 | Fehlzündg. bei Kraftstoffmangel erkannt |
| 0x1320 | Schwungradanpassung für Bereich Fehlzündungserkennung |
| 0x1321 | Schwungradanpassung für Betriebsgüte Fehlzündungserkennung |
| 0x0420 | Katalysatorwirkungsgrad unter Schwelle (Reihe 1) |
| 0x0443 | AKF-System, Stromkreis Regenerierventil |
| 0x0444 | AKF-System, Stromkreis Regenerierventil unterbr. |
| 0x0445 | AKF-System, Stromkreis Regenerierventil kurzgeschl. |
| 0x1443 | Leckdiagnosepumpe, Signal hoch |
| 0x1442 | Leckdiagnosepumpe, Signal niedrig |
| 0x1436 | Leckdiagnosepumpe, Unterbrechung |
| 0x2402 | AKF-System, Leckdiagnosepumpe, Steuerkreis hoch |
| 0x2401 | AKF-System, Leckdiagnosepumpe, Steuerkreis niedrig |
| 0x2400 | AKF-System, Leckdiagnosepumpe, Kanal offen |
| 0x1475 | Reed-Schalter schliesst nicht |
| 0x1477 | Reed-Schalter öffnet nicht |
| 0x1437 | Bereich/Betriebsgüte Leckdiagnosepumpe |
| 0x2404 | AKF-System, Leckdiagnosepumpe, Sensorkanal Bereich/Betriebsgüte |
| 0x0441 | AKF-System, Regenerierluftstrom n.i.O. |
| 0x1476 | Leckdiagnosepumpe, Leitung eingeklemmt |
| 0x0455 | AKF-System, Leck erkannt (grosses Leck) |
| 0x0442 | AKF-System, Leck erkannt (kleines Leck) |
| 0x0456 | AKF-System, Leck erkannt (sehr kleines Leck) |
| 0x0123 | Stromkreis DK-Sensor/Pedalwegsensor/Schalter A, Eingang hoch |
| 0x0122 | Stromkreis DK-Sensor/Pedalwegsensor/Schalter A, Eingang niedrig |
| 0x0223 | Stromkreis DK-Sensor/Pedalwegsensor/Schalter B, Eingang hoch |
| 0x0222 | Stromkreis DK-Sensor/Pedalwegsensor/Schalter B, Eingang niedrig |
| 0x1125 | DK-Sensor A und B, Bereich/Betriebsgüte, geringer Fehler |
| 0x1126 | DK-Sensor A und B, Bereich/Betriebsgüte, enormer Fehler |
| 0x1229 | Drosselklappensensor, Anpassungsfehler |
| 0x1226 | Funktionsstörung Drosselklappe (Klappe defekt) |
| 0x1123 | Pedalwegsensor 1, Eingang hoch |
| 0x1122 | Pedalwegsensor 1, Eingang niedrig |
| 0x1223 | Pedalwegsensor 2, Eingang hoch |
| 0x1222 | Pedalwegsensor 2, Eingang niedrig |
| 0x1224 | Pedalwegsensor 1 und 2, Bereich/Betriebsgüte n.i.O. |
| 0x0638 | Drosselklappensteller Bereich/Betriebsgüte |
| 0x2123 | DK/PWG Position Sensor/Schalter D Kanal High Input |
| 0x2122 | DK/PWG Position Sensor/Schalter D Kanal Low Input |
| 0x2128 | DK/PWG Position Sensor/Schalter E Kanal High Input |
| 0x2127 | DK/PWG Position Sensor/Schalter E Kanal Low Input |
| 0x2138 | DK/PWG Position Sensor/Schalter D/E Spannungswechselbeziehung |
| 0x1617 | Elektr. Steuergerät, Regler H-Brücke |
| 0x1679 | E-Gas, Überwachungsebene 2/3, Berechnung Drehmomentverlust |
| 0x1680 | E-Gas, Überwachungsebene 2/3, Fehler ADK-Prozessor |
| 0x1681 | E-Gas, Überwachungsebene 2/3, Berechnungsfehler Motordrehzahl |
| 0x1682 | E-Gas, Überwachungsebene 2/3, Berechnungsfehler Leerlaufdrehzahl A |
| 0x1683 | E-Gas, Überwachungsebene 2/3, Berechnungsfehler Leerlaufdrehzahl B |
| 0x1685 | E-Gas, Überwachungsebene 2/3, max. Fehler Kupplungsdrehmoment |
| 0x1684 | E-Gas, Überwachungsebene 2/3, min. Fehler Kupplungsdrehmoment |
| 0x1686 | E-Gas, Überwachungsebene 2/3, Diagnosefehler Pedalwegsensor |
| 0x1687 | E-Gas, Überwachungsebene 2/3 Diagnosefehler DK-Sensor |
| 0x1688 | E-Gas, Überwachungsebene 2/3, Berechnung Luftmassenstrom |
| 0x1689 | E-Gas, Überwachungsebene 2/3, Fehler Drehmomentberechnung |
| 0x1691 | E-Gas, Überwachungsebene 2/3, Fehler Drehzahlbegrenzung, elektromot. Drosselklappensteller |
| 0x1692 | E-Gas, Überwachungsebene 2/3, elektromot. Drosselklappensteller und Kraftstoffabschaltung 'A' |
| 0x1693 | E-Gas, Überwachungsebene 2/3, elektromot. Drosselklappensteller und Kraftstoffabschaltung 'B' |
| 0x0533 | Stromkreis Kältemitteldrucksensor, Eingang hoch |
| 0x0532 | Stromkreis Kältemitteldrucksensor, Eingang niedrig |
| 0x0500 | Fahrgeschwindigkeitssensor |
| 0x0335 | Stromkreis Kurbelwinkelsensor A |
| 0x0336 | Stromkreis Kurbelwinkelsensor A, Bereich/Betriebsgüte |
| 0x0647 | Relais/Kompressorkupplung, Steuerstromkreis hoch |
| 0x0646 | Relais/Kompressorkupplung, Steuerstromkreis niedrig |
| 0x1482 | Relais/Motorkühlerlüfter 1, Eingang hoch |
| 0x1481 | Relais/Motorkühlerlüfter 1, Eingang niedrig |
| 0x1485 | Relais/Motorkühlerlüfter 2, Eingang hoch |
| 0x1484 | Relais/Motorkühlerlüfter 2, Eingang niedrig |
| 0x1488 | Relais/Motorkühlerlüfter 3, Eingang hoch |
| 0x1487 | Relais/Motorkühlerlüfter 3, Eingang niedrig |
| 0x0692 | Luefter 1 Steuerkreis hoch |
| 0x0691 | Luefter 1 Steuerkreis niedrig |
| 0x0694 | Luefter 2 Steuerkreis hoch |
| 0x0693 | Luefter 2 Steuerkreis niedrig |
| 0x0696 | Luefter 3 Steuerkreis hoch |
| 0x0695 | Luefter 3 Steuerkreis niedrig |
| 0x0704 | Funktionsstörung Eingangsstromkreis Kupplungsschalter |
| 0x0571 | Stromkreis Geschwindigkeitsregelung / Bremsschalter A |
| 0x0568 | Einstellsignal Geschwindigkeitsregelung |
| 0x0575 | Eingangsstromkreis Geschwindigkeitsregelung |
| 0x1627 | Systemspannung, Lastsensor hoch |
| 0x1626 | Systemspannung, Lastsensor niedrig |
| 0x0506 | Leerlaufregelsystem, Drehzahl niedriger als erwartet |
| 0x0507 | Leerlaufregelsystem, Drehzahl höher als erwartet |
| 0x0218 | Getriebeflüssigkeit, Übertemperaturzustand |
| 0x0713 | Stromkreis Temperatursensor Getriebeflüssigkeit, Eingang hoch |
| 0x0712 | Stromkreis Temperatursensor Getriebeflüssigkeit, Eingang niedrig |
| 0x0714 | Temperatursensor Getriebeflüssigkeit, Stromkreis zeitw. unterbr. |
| 0x0721 | Stromkreis Abtriebsdrehzahlsensor, Bereich/Betriebsgüte |
| 0x0705 | Funktionsstörung Stromkreis Getriebepositionssensor (PRNDL-Eingang) |
| 0x0816 | Stromkreis Herunterschaltkontakt |
| 0x0815 | Stromkreis Hochschaltkontakt |
| 0x1816 | Fehler Lenkrad-Minusschalter, Eingang niedrig |
| 0x1815 | Fehler Lenkrad-Plusschalter, Eingang niedrig |
| 0x0790 | Stromkreis, Normal/Sport-Schalter |
| 0x1698 | Steuerungsfehler Getriebesteuergerät |
| 0x1699 | Prüfsummenfehler Getriebesteuergerät |
| 0x1705 | Unterbrechung LED-Ausgang Getriebesteuergerät |
| 0x1706 | Kurzschluss LED-Ausgang Getriebesteuergerät |
| 0x1786 | Stromkreis Stellantrieb Getriebeübersetzung, Bereich/Betriebsgüte |
| 0x1788 | Kurzschluss Stellantrieb Getriebeübersetzung |
| 0x1787 | Unterbrechung Stellantrieb Getriebeübersetzung |
| 0x1785 | Funktionsstörung Stromkreis Stellantrieb Getriebeübersetzung |
| 0x1789 | Kommunikationsfehler Stellantrieb Getriebeübersetzung |
| 0x1825 | Funktionsstörung Wählhebelsperre |
| 0x1826 | Relais Wählhebelsperrmagnet (CVT), Eingang niedrig |
| 0x1827 | Relais Wählhebelsperrmagnet (CVT), Eingang hoch |
| 0x1739 | Kupplungsmagnetventil, Kommunikationsfehler |
| 0x1740 | Stromkreis Kupplungsmagnetventil, Bereich/Betriebsgüte |
| 0x1741 | Unterbrechung Kupplungsmagnetventil |
| 0x1742 | Kurzschluss Kupplungsmagnetventil |
| 0x1749 | Sekundärdruck-Magnetventil, Kommunikationsfehler |
| 0x1750 | Stromkreis Sekundärdruck-Magnetventil, Bereich/Betriebsgüte |
| 0x1751 | Sekundärdruck-Magnetventil, Unterbrechung |
| 0x1752 | Sekundärdruck-Magnetventil, Kurzschluss |
| 0x1661 | Zeitüberschreitung EWS-Telegramm |
| 0x1656 | EWS, falscher Code |
| 0x0604 | Steuergerät, interner RAM-Speicher, Fehler |
| 0x0603 | Steuergerät, interner KAM-Speicher, Fehler |
| 0x0601 | Steuergerät, interner Speicher, Prüfsummenfehler |
| 0x1615 | Elektr. Steuergerät, Prozessor, Ausfall SPI-Bus |
| 0x1600 | Steuergerät, externer RAM-Speicher, Fehler |
| 0x1616 | Elektr. Steuergerät, Codierspeicher, Prüfsummenfehler |
| 0x0563 | Systemspannung hoch |
| 0x0562 | Systemspannung niedrig |
| 0x1571 | Elektr. Steuergerät, Sensorspeisung A, Ausgang hoch |
| 0x1570 | Elektr. Steuergerät, Sensorspeisung A, Ausgang niedrig |
| 0x1572 | Elektr. Steuergerät, Sensorspeisung A, unsauberes Signal |
| 0x1574 | Elektr. Steuergerät, Sensorspeisung B, Ausgang hoch |
| 0x1573 | Elektr. Steuergerät, Sensorspeisung B, Ausgang niedrig |
| 0x1575 | Elektr. Steuergerät, Sensorspeisung B, unsauberes Signal |
| 0x1696 | Steuerstromkreis Hauptrelais, Eingang niedrig |
| 0x1697 | Steuerstromkreis Hauptrelais, Eingang hoch |
| 0x0643 | Sensor Referenzspannung A Kanal Hoch |
| 0x0642 | Sensor Referenzspannung A Kanal niedrig |
| 0x0653 | Sensor Referenzspannung B Kanal Hoch |
| 0x0652 | Sensor Referenzspannung B Kanal niedrig |
| 0x0686 | ECM/PCM Hauptrelais Steuerkreis niedrig |
| 0x0687 | ECM/PCM Hauptrelais Steuerkreis hoch |
| 0x1613 | Serielle Kommunikationsverbindung ASC |
| 0x1612 | Serielle Kommunikationsverbindung Kombiinstrument |
| 0x1611 | Serielle Kommunikationsverbindung Getriebesteuergerät |
| 0x1607 | CAN-Status |
| 0x1712 | Getriebeflüssigkeit, Temperatur zu hoch |
| 0x2299 | Gaspedal Position/Bremse Plausibilitaetsfehler |
| 0xFFFF | Unbekannter Fehler |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 250 rows × 7 columns

| ORT | UW_ANZ | UW_SATZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 0x0071 | 4 | 1 | 0x17 | 0x11 | 0x02 | 0x0B |
| 0x113C | 4 | 1 | 0x17 | 0x11 | 0x16 | 0x0B |
| 0x113D | 4 | 1 | 0x17 | 0x11 | 0x16 | 0x0B |
| 0x316B | 4 | 1 | 0x17 | 0x11 | 0x16 | 0x0B |
| 0x316A | 4 | 1 | 0x17 | 0x11 | 0x16 | 0x0B |
| 0x0700 | 4 | 1 | 0x17 | 0x18 | 0x08 | 0x0D |
| 0x101F | 4 | 1 | 0x17 | 0x11 | 0x02 | 0x0B |
| 0x0070 | 4 | 1 | 0x17 | 0x11 | 0x16 | 0x0B |
| 0x0113 | 4 | 1 | 0x17 | 0x11 | 0x16 | 0x0B |
| 0x0112 | 4 | 1 | 0x17 | 0x11 | 0x16 | 0x0B |
| 0x0114 | 4 | 1 | 0x17 | 0x11 | 0x16 | 0x0B |
| 0x0108 | 4 | 1 | 0x17 | 0x02 | 0x16 | 0x0B |
| 0x0107 | 4 | 1 | 0x17 | 0x02 | 0x16 | 0x0B |
| 0x0109 | 4 | 1 | 0x17 | 0x02 | 0x16 | 0x0B |
| 0x1106 | 4 | 1 | 0x17 | 0x02 | 0x16 | 0x0B |
| 0x1107 | 4 | 1 | 0x17 | 0x02 | 0x16 | 0x0B |
| 0x1108 | 4 | 1 | 0x17 | 0x02 | 0x16 | 0x0B |
| 0x1109 | 4 | 1 | 0x17 | 0x02 | 0x16 | 0x0B |
| 0x1238 | 4 | 1 | 0x17 | 0x02 | 0x09 | 0x16 |
| 0x1237 | 4 | 1 | 0x17 | 0x02 | 0x09 | 0x16 |
| 0x1235 | 4 | 1 | 0x17 | 0x02 | 0x09 | 0x16 |
| 0x1239 | 4 | 1 | 0x17 | 0x02 | 0x09 | 0x16 |
| 0x1240 | 4 | 1 | 0x17 | 0x02 | 0x09 | 0x16 |
| 0x1241 | 4 | 1 | 0x17 | 0x02 | 0x09 | 0x16 |
| 0x1242 | 4 | 1 | 0x17 | 0x02 | 0x09 | 0x16 |
| 0x1499 | 4 | 1 | 0x17 | 0x0E | 0x11 | 0x16 |
| 0x1497 | 4 | 1 | 0x17 | 0x0E | 0x11 | 0x16 |
| 0x1498 | 4 | 1 | 0x17 | 0x0E | 0x11 | 0x16 |
| 0x0118 | 4 | 1 | 0x17 | 0x16 | 0x11 | 0x0B |
| 0x0117 | 4 | 1 | 0x17 | 0x16 | 0x11 | 0x0B |
| 0x0116 | 4 | 1 | 0x17 | 0x16 | 0x11 | 0x0B |
| 0x0125 | 4 | 1 | 0x17 | 0x16 | 0x11 | 0x0B |
| 0x0128 | 4 | 1 | 0x17 | 0x16 | 0x11 | 0x0B |
| 0x0119 | 4 | 1 | 0x17 | 0x16 | 0x11 | 0x0B |
| 0x0234 | 4 | 1 | 0x17 | 0x16 | 0x11 | 0x09 |
| 0x1112 | 4 | 1 | 0x17 | 0x16 | 0x0B | 0x00 |
| 0x1111 | 4 | 1 | 0x17 | 0x16 | 0x0B | 0x00 |
| 0x1113 | 4 | 1 | 0x17 | 0x16 | 0x0B | 0x00 |
| 0x0132 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0131 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0130 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0032 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0031 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0030 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0135 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0053 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0138 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0137 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0136 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0038 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0037 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0036 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0141 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0054 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0262 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0261 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0201 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0265 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0264 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0202 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0268 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0267 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0203 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0271 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0270 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0204 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x1236 | 4 | 1 | 0x17 | 0x0E | 0x01 | 0x16 |
| 0x1234 | 4 | 1 | 0x17 | 0x0E | 0x01 | 0x16 |
| 0x0171 | 4 | 1 | 0x17 | 0x0E | 0x13 | 0x16 |
| 0x0172 | 4 | 1 | 0x17 | 0x0E | 0x13 | 0x16 |
| 0x0133 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0139 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x1143 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x1144 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x2271 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x2270 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x2096 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x2097 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0340 | 4 | 1 | 0x17 | 0x04 | 0x06 | 0x16 |
| 0x0341 | 4 | 1 | 0x17 | 0x04 | 0x06 | 0x16 |
| 0x0351 | 4 | 1 | 0x17 | 0x04 | 0x11 | 0x16 |
| 0x1366 | 4 | 1 | 0x17 | 0x04 | 0x11 | 0x16 |
| 0x0352 | 4 | 1 | 0x17 | 0x04 | 0x11 | 0x16 |
| 0x1367 | 4 | 1 | 0x17 | 0x04 | 0x11 | 0x16 |
| 0x2301 | 4 | 1 | 0x17 | 0x04 | 0x11 | 0x16 |
| 0x2300 | 4 | 1 | 0x17 | 0x04 | 0x11 | 0x16 |
| 0x2304 | 4 | 1 | 0x17 | 0x04 | 0x11 | 0x16 |
| 0x2303 | 4 | 1 | 0x17 | 0x04 | 0x11 | 0x16 |
| 0x0326 | 4 | 1 | 0x17 | 0x0E | 0x11 | 0x16 |
| 0x0324 | 4 | 1 | 0x17 | 0x0E | 0x11 | 0x16 |
| 0x1340 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x0300 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x1341 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x1342 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x0301 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x1343 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x1344 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x0302 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x1345 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x1346 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x0303 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x1347 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x1348 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x0304 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x1349 | 4 | 1 | 0x17 | 0x0B | 0x11 | 0x16 |
| 0x0313 | 4 | 1 | 0x17 | 0x01 | 0x11 | 0x16 |
| 0x1320 | 4 | 1 | 0x17 | 0x04 | 0x06 | 0x16 |
| 0x1321 | 4 | 1 | 0x17 | 0x04 | 0x06 | 0x16 |
| 0x0420 | 4 | 1 | 0x17 | 0x0E | 0x13 | 0x16 |
| 0x0443 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0444 | 4 | 1 | 0x17 | 0x04 | 0x0E | 0x16 |
| 0x0445 | 4 | 1 | 0x17 | 0x0B | 0x0E | 0x16 |
| 0x1443 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x1442 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x1436 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x2402 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x2401 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x2400 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x1475 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x1477 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x1437 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x2404 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0441 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x1476 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0455 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0442 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0456 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x0123 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x0122 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x0223 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x0222 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1125 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1126 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1229 | 4 | 1 | 0x17 | 0x02 | 0x11 | 0x16 |
| 0x1226 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1123 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1122 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1223 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1222 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1224 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x0638 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x2123 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x2122 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x2128 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x2127 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x2138 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1617 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1679 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x1680 | 4 | 1 | 0x17 | 0x10 | 0x04 | 0x16 |
| 0x1681 | 4 | 1 | 0x17 | 0x18 | 0x06 | 0x16 |
| 0x1682 | 4 | 1 | 0x17 | 0x07 | 0x11 | 0x16 |
| 0x1683 | 4 | 1 | 0x17 | 0x07 | 0x11 | 0x16 |
| 0x1684 | 4 | 1 | 0x17 | 0x10 | 0x05 | 0x16 |
| 0x1685 | 4 | 1 | 0x17 | 0x10 | 0x05 | 0x16 |
| 0x1686 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1687 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0x1688 | 4 | 1 | 0x17 | 0x13 | 0x0E | 0x16 |
| 0x1689 | 4 | 1 | 0x17 | 0x10 | 0x05 | 0x16 |
| 0x1691 | 4 | 1 | 0x17 | 0x18 | 0x06 | 0x16 |
| 0x1692 | 4 | 1 | 0x17 | 0x02 | 0x10 | 0x16 |
| 0x1693 | 4 | 1 | 0x17 | 0x02 | 0x10 | 0x16 |
| 0x0533 | 4 | 1 | 0x17 | 0x07 | 0x11 | 0x16 |
| 0x0532 | 4 | 1 | 0x17 | 0x07 | 0x11 | 0x16 |
| 0x0500 | 4 | 1 | 0x17 | 0x18 | 0x06 | 0x16 |
| 0x0335 | 4 | 1 | 0x17 | 0x04 | 0x06 | 0x16 |
| 0x0336 | 4 | 1 | 0x17 | 0x04 | 0x06 | 0x16 |
| 0x0647 | 4 | 1 | 0x17 | 0x07 | 0x11 | 0x16 |
| 0x0646 | 4 | 1 | 0x17 | 0x07 | 0x11 | 0x16 |
| 0x1482 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x1481 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x1485 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x1484 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x1488 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x1487 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x0692 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x0691 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x0694 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x0693 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x0696 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x0695 | 4 | 1 | 0x17 | 0x10 | 0x11 | 0x16 |
| 0x0704 | 4 | 1 | 0x17 | 0x18 | 0x04 | 0x16 |
| 0x0571 | 4 | 1 | 0x17 | 0x18 | 0x04 | 0x16 |
| 0x1825 | 4 | 1 | 0x17 | 0x0A | 0x08 | 0x16 |
| 0x0575 | 4 | 1 | 0x17 | 0x18 | 0x08 | 0x16 |
| 0x0568 | 4 | 1 | 0x17 | 0x18 | 0x08 | 0x16 |
| 0x1627 | 4 | 1 | 0x17 | 0x04 | 0x10 | 0x16 |
| 0x1626 | 4 | 1 | 0x17 | 0x04 | 0x10 | 0x16 |
| 0x0506 | 4 | 1 | 0x17 | 0x16 | 0x02 | 0x11 |
| 0x0507 | 4 | 1 | 0x17 | 0x16 | 0x02 | 0x11 |
| 0x0218 | 4 | 1 | 0x17 | 0x08 | 0x11 | 0x16 |
| 0x1712 | 4 | 1 | 0x17 | 0x08 | 0x11 | 0x16 |
| 0x0713 | 4 | 1 | 0x17 | 0x08 | 0x11 | 0x16 |
| 0x0712 | 4 | 1 | 0x17 | 0x08 | 0x11 | 0x16 |
| 0x0714 | 4 | 1 | 0x17 | 0x08 | 0x11 | 0x16 |
| 0x0721 | 4 | 1 | 0x17 | 0x08 | 0x11 | 0x16 |
| 0x0705 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x0816 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x0815 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1816 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1815 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x0790 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1698 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1699 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1705 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1706 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1786 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1788 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1787 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1785 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1789 | 4 | 1 | 0x17 | 0x08 | 0x04 | 0x16 |
| 0x1826 | 4 | 1 | 0x04 | 0x18 | 0x0A | 0x08 |
| 0x1827 | 4 | 1 | 0x04 | 0x18 | 0x0A | 0x08 |
| 0x1739 | 4 | 1 | 0x04 | 0x17 | 0x11 | 0x08 |
| 0x1740 | 4 | 1 | 0x04 | 0x17 | 0x11 | 0x08 |
| 0x1741 | 4 | 1 | 0x04 | 0x17 | 0x11 | 0x08 |
| 0x1742 | 4 | 1 | 0x04 | 0x17 | 0x11 | 0x08 |
| 0x1749 | 4 | 1 | 0x04 | 0x17 | 0x11 | 0x08 |
| 0x1750 | 4 | 1 | 0x04 | 0x17 | 0x11 | 0x08 |
| 0x1751 | 4 | 1 | 0x04 | 0x17 | 0x11 | 0x08 |
| 0x1752 | 4 | 1 | 0x04 | 0x17 | 0x11 | 0x08 |
| 0x1661 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1656 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x0604 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x0603 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x0601 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1615 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1600 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x0563 | 4 | 1 | 0x17 | 0x10 | 0x04 | 0x0D |
| 0x0562 | 4 | 1 | 0x17 | 0x10 | 0x04 | 0x0D |
| 0x1571 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1570 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1572 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1574 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1573 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1575 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1697 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x10 |
| 0x1696 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x10 |
| 0x0643 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x0642 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x0653 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x0652 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x0687 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x10 |
| 0x0686 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x10 |
| 0x1613 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x10 |
| 0x1612 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1611 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1607 | 4 | 1 | 0x17 | 0x0D | 0x04 | 0x16 |
| 0x1616 | 4 | 1 | 0x17 | 0xOD | 0x04 | 0x16 |
| 0x2299 | 4 | 1 | 0x17 | 0x02 | 0x03 | 0x16 |
| 0xFFFF | 0 | 0 | 0x00 | 0x00 | 0x00 | 0x00 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss mit V batt |
| 0x02 | Kurzschluss mit Masse |
| 0x03 | Kein Signal erkannt |
| 0x04 | Signal ausserhalb Bereich |
| 0x05 | Test abgeschlossen |
| 0x06 | Sporadischer Fehler |
| 0x07 | Fehler vorhanden |
| 0x08 | Warnleuchtenstatus |
| 0xFF | Unbekannter Status |

<a id="table-actuator-test"></a>
### ACTUATOR_TEST

Dimensions: 19 rows × 3 columns

| NAME | LID | ACTION |
| --- | --- | --- |
| MAIN_RELAY | 0x11 | Hauptrelais |
| FUEL_PUMP | 0x12 | Kraftstoffpumpe |
| AC_COMPRESSOR | 0x13 | Klimakompressor |
| FAN_RELAY_HIGH | 0x1B | Kühlerlüfterrelais (hoch) |
| FAN_RELAY_MED | 0x1A | Kühlerlüfterrelais (mittel) |
| FAN_RELAY_LOW | 0x19 | Kühlerlüfterrelais (niedrig) |
| CANISTER_PURGE | 0x20 | AKF-Regenerierung |
| THROTTLE_ACT | 0x23 | Drosselklappensteller |
| LEAK_DETECTION | 0x24 | Leckdiagnosepumpe |
| PRIME_FUEL | 0x34 | Anlasskraftstoffleitung |
| CVT_SHIFT_LOCK | 0x37 | Stufenloses Getriebe Wählhebelsperre |
| INJECTOR_1 | 0x39 | Einspritzventil 1 |
| INJECTOR_2 | 0x3A | Einspritzventil 2 |
| INJECTOR_3 | 0x3B | Einspritzventil 3 |
| INJECTOR_4 | 0x3C | Einspritzventil 4 |
| UPSTR_O2_HEAT | 0x3D | Heizung Lambasonde vor Kat |
| DWSTR_O2_HEAT | 0x3E | Heizung Lambasonde nach Kat |
| DISABLE_ACTS | 0x3F | Alle Stellantriebe deaktivieren |
|  | 0xFF |  |

<a id="table-applic-correction"></a>
### APPLIC_CORRECTION

Dimensions: 4 rows × 3 columns

| NAME | LID | ACTION |
| --- | --- | --- |
| IDLE_CO_TRIM | 0x90 | Leerlaufdrehzahl CO-Korrektur |
| IDLE_TEMP_CORR | 0x91 | Leerlaufdrehzahl Vorübergehende Korrektur |
| IDLE_DUR_CORR | 0x92 | Leerlaufdrehzahl Dauerhafte Korrektur |
|  | 0xFF |  |

<a id="table-adaptive-values"></a>
### ADAPTIVE_VALUES

Dimensions: 12 rows × 3 columns

| NAME | LID | ACTION |
| --- | --- | --- |
| ALL_VALUES | 0x50 | Rücksetzen Alle Adaptivwerte |
| MAP | 0x51 | Rücksetzen Korrektur Saugrohrdruck |
| KNOCK_CONTROL | 0x52 | Rücksetzen Klopfregelung Adaptivwert |
| ECT_THROTTLE | 0x53 | Rücksetzen Anpassung E-Gas |
| CVT | 0x54 | Rücksetzen Stufenloses Getriebe |
| LAMBDA | 0x56 | Rücksetzen Lambda Adaptivwert |
| MISFIRING | 0x57 | Rücksetzen Fehlzündungen Adaptivwert |
| IDLE_SPEED | 0x58 | Rücksetzen Leerlaufdrehzahl Adaptivwert |
| DYNAMIC_TRIM | 0x59 | Rücksetzen Dynamische Korrektur |
| KNOCK_SPARK_ADV | 0x5A | Rücksetzen Klopffrühverstellung, Langsamkorrektur |
| CVT_DIST | 0x5B | Rücksetzen CVT Weg im Notprogramm zurueckgelegt |
|  | 0xFF |  |
