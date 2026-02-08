# mrkomb18.prg

- Jobs: [102](#jobs)
- Tables: [34](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | K18-K19 |
| ORIGIN | BMW_Motorrad UX_EE_2 Reiner_Pfeifer |
| REVISION | 1.057 |
| AUTHOR | MTA Research_and_Development Ferrigno_Roberto, BMW UX-EE-1 Stef |
| COMMENT | N/A |
| PACKAGE | 1.57 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [C_CI_LESEN](#job-c-ci-lesen) - Codierindex lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9B Vehicle Manufacturer Coding Index oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_AEI_LESEN](#job-c-aei-lesen) - Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_SCHREIBEN](#job-c-aei-schreiben) - Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_AUFTRAG](#job-c-aei-auftrag) - Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_LESEN](#job-zif-lesen) - Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_BACKUP_LESEN](#job-zif-backup-lesen) - Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [PHYSIKALISCHE_HW_NR_LESEN](#job-physikalische-hw-nr-lesen) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [HARDWARE_REFERENZ_LESEN](#job-hardware-referenz-lesen) - Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [DATEN_REFERENZ_LESEN](#job-daten-referenz-lesen) - Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default
- [FLASH_ZEITEN_LESEN](#job-flash-zeiten-lesen) - Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default
- [FLASH_BLOCKLAENGE_LESEN](#job-flash-blocklaenge-lesen) - Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default
- [AUTHENTISIERUNG_ZUFALLSZAHL_LESEN](#job-authentisierung-zufallszahl-lesen) - Authentisierung Zufallszahl des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $07 RequestForAuthentication Modus  : Default
- [AUTHENTISIERUNG_START](#job-authentisierung-start) - Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default
- [FLASH_PROGRAMMIER_STATUS_LESEN](#job-flash-programmier-status-lesen) - Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default
- [FLASH_SIGNATUR_PRUEFEN](#job-flash-signatur-pruefen) - Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [DIAGNOSE_MODE_GATEWAY](#job-diagnose-mode-gateway) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [BAUDRATE_115200_GATEWAY](#job-baudrate-115200-gateway) - Umschaltung auf 115200 Baud (und BMW-FAST wg. Fast-Initialisation)
- [FLASH_SCHREIBEN_XXL](#job-flash-schreiben-xxl) - Flash Daten schreiben XXL-Format Standard Flashjob KWP2000: $36 TransferData Modus  : Default
- [NG_FLASH_LOESCHEN](#job-ng-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [STEUERN_EWS4](#job-steuern-ews4) - "EWS4-data" schreiben KWP 2000: $2E WriteDataByCommonIdentifier CommonIdentifier=0xC001
- [STATUS_DIGITAL](#job-status-digital) - Read the status of the digital inputs KWP2000: 	$31 StartRoutineByLocalIdentifier $FB Read Status (System Supplier Specific) $0F Digital Port(s)
- [STEUERN_LED_CONTROL](#job-steuern-led-control) - LEDs individuell ansteuern KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED
- [WRITE_EE_DATA](#job-write-ee-data) - Write the data in EEPROM KWP2000: $2E	WriteDataByCommonIdentifier $AAAA	Write data in EEPROM
- [NG_SIGNATUR_PRUEFEN](#job-ng-signatur-pruefen) - Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default
- [NG_AUTHENTISIERUNG_START](#job-ng-authentisierung-start) - Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default
- [STATUS_EWS4_SK](#job-status-ews4-sk) - KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier = 0xC002 Lesen des SecretKey des Server sowie Client für EWS4
- [READ_EE_DATA](#job-read-ee-data) - Read the data in EEPROM KWP2000: $22 ReadDataByCommonIdentifier $BBBB	Read data in EEPROM
- [STATUS_EWS](#job-status-ews) - KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier = 0xC000 Read the current status of the EWS SecretKeys
- [STATUS_SCHLUESSELDATEN](#job-status-schluesseldaten) - Read the transponder table key data Service 	$31 	(Service routine control) Sub-ID 	$01 	(Start routine) RID 		0xAC5A 	(For reading out the key data from the transponder table)
- [STEUERN_SCHLUESSELDATEN](#job-steuern-schluesseldaten) - Writing in the KOMBI of the KEY_IDs only if the EWS4_TRSP_SK is unlocked Service: $2E WriteDataByIdentifier SubService: 0xDC80 STEUERN_SCHLUESSELDATEN
- [STEUERN_FAHRGESTELLNUMMER](#job-steuern-fahrgestellnummer) - Writing of VIN JobHeaderFormat Service $2E: WiteDataByIdentifier SubService $F190: DID for writing the VIN (17 digits)
- [STATUS_FAHRGESTELLNUMMER](#job-status-fahrgestellnummer) - Read the Vehicle Identification Number JobHeaderFormat Service: $22 -&gt; ReadDataByIdentifier SubService: $F190 -&gt; DID to read the VIN (17 digits)
- [STEUERN_CAS_INIT_LOC_DATE](#job-steuern-cas-init-loc-date) - Write the key init data in the KOMBI JobHeaderFormat Service: $2E (WriteDataByIdentifier) SubService: $DC7B (DID for writing the time stamp, location and station data of the key init in the KOMBI)
- [STATUS_CAS_INIT_LOC_DATE](#job-status-cas-init-loc-date) - Read the key init data stored in the KOMBI JobHeaderFormat Service $22 (ReadDataByIdentifier) SubService $DC7B (DID for reading out the time stamp, location and station data of the key init in the KOMBI)
- [STEUERN_CAS_ANLIEFERZUSTAND](#job-steuern-cas-anlieferzustand) - Put the KOMBI in delivery condition If the conditions to put the KOMBI in delivery status are wrong, return 'ERROR_ECU_CONDITIONS_NOT_CORRECT' After the data reset, all the lock flags shall be also reset JobHeaderFormat Service $31 -&gt; Service routine control SubID $01 -&gt; Sub-ID for start routine RID $AC50 -&gt; RID for resetting the KOMBI into delivery condition
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F0A Fahrzeugauftrag Modus  : Default
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F7F Fahrzeugauftrag Modus  : Default
- [C_FA_SCHREIBEN](#job-c-fa-schreiben) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F0A Fahrzeugauftrag Modus  : Default
- [STEUERN_SCHLUESSEL_INIT](#job-steuern-schluessel-init) - Start key initialisation. Service: $31 StartRoutineByLocalIdentifier Sub-ID: 0x01 for start routine RID: 0xAC52 for starting the key
- [STATUS_SCHLUESSEL_TRSP](#job-status-schluessel-trsp) - Read the status of the last transponder found Service 	$22 	(Read data) DID 		0xDC7E 	(For reading out the key status)
- [STATUS_CAS_ANLIEFERZUSTAND](#job-status-cas-anlieferzustand) - Indicate the current progress of the reset after STEUERN_CAS_ANLIEFERZUSTAND JobHeaderFormat Service $22 (ReadDataByIdentifier) SubService 0xDC7D (DID for return the progress of the EWS4 parameter reset)
- [STEUERN](#job-steuern) - Write the HO INFO in the KOMBI JobHeaderFormat Service $2E: WiteDataByIdentifier SubService $DC54: DID for write the HO INFO (9 bytes)
- [STEUERN_PRODUCTION_MODE](#job-steuern-production-mode) - Set or reset the Production Mode coding flag in the KOMBI JobHeaderFormat $2E: WiteDataByIdentifier $DC55: DID for write the Production Mode coding flag (1 bit)
- [STATUS_GWSZ_ANZEIGE](#job-status-gwsz-anzeige) - Kilometers reading KWP2000: $21 ReadDataByLocalIdentifier $01 SubService ID to read the Odometer value KWP2000: $22 ReadDataByCommonIdentifier $3007 SubService ID to read the Odometer unit (Miles or KM)
- [STEUERN_GWSZ_ANZEIGE_SCHREIBEN](#job-steuern-gwsz-anzeige-schreiben) - Odometer writing KWP2000: $3B WriteDataByLocalIdentifier $01 SubService ID to write the Odometer value
- [STEUERN_START_KALIBRIERUNG_WINDSCHILD](#job-steuern-start-kalibrierung-windschild) - Start der Kalibrierung des Windschildes KWP2000: $31 StartRoutineByLocalId $21 Windshield $01 Start Reference Run
- [STATUS_KALIBRIERUNG_WINDSCHILD](#job-status-kalibrierung-windschild) - Status Kalibrierung Windschild KWP2000: $31 StartRoutineByLocalId $21 Windshield $03 Status of Reference Run
- [STATUS_SERVICE_DATE](#job-status-service-date) - Job to read the Service Date KWP2000: $21 ApplDiagReadDataByLocalIdentifier $11 Read Service_Date
- [STEUERN_SERVICE_DATE](#job-steuern-service-date) - Service Date writing KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $11 Set Service_Date
- [STATUS_SERVICE_RESTWEG](#job-status-service-restweg) - Remaining service distance reading KWP2000:  $22 ApplDiagReadDataByCommonIdentifier $3007 Coding block for odometer unit setting $21 ApplDiagReadDataByLocalIdentifier $12 Read Actual_Service_Mileage_Range in [km]
- [STEUERN_SERVICE_RESTWEG](#job-steuern-service-restweg) - Service distance interval writing KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $12 Set actual service mileage range in [km]
- [STEUERN_SELF_TEST_ON](#job-steuern-self-test-on) - Kombi Selbsttest KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $18 self test
- [STEUERN_SELF_TEST_OFF](#job-steuern-self-test-off) - Kombi Self Test KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $18 self test
- [STATUS_WINDSCHILD](#job-status-windschild) - Status des Windschilds KWP2000: $30 InputOutputByLocalId $05 Windshield $01 Status
- [STEUERN_WINDSCHILD](#job-steuern-windschild) - Windschild ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $05 Windshield $07 ShortTermAdjustment $XX Windshield Parameter
- [STEUERN_BLINKER_RECHTS](#job-steuern-blinker-rechts) - Control the Right Blinkers directly KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED
- [STEUERN_BLINKER_LINKS](#job-steuern-blinker-links) - Control the Left Blinkers directly KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED
- [STEUERN_STANDLICHT](#job-steuern-standlicht) - Position lights controlled directly Pre-requirement: Execution of the Job STEUERN_VORBEREITEN KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED $10 Position Light
- [STEUERN_ABBLENDLICHT](#job-steuern-abblendlicht) - Control the Low Beam directly KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED
- [STEUERN_RUECKLICHT](#job-steuern-ruecklicht) - Control the Tail lights Pre-requirement: execute the job STEUERN_VORBEREITEN KWP2000: $31 InputOutputControlByLocalIdentifier $FA System Supplier Specific $15 pwm output $01 Tail Light
- [STATUS_RUECKLICHT](#job-status-ruecklicht) - Read the tail light pwm value Pre-requirement: execute the job STEUERN_VORBEREITEN KWP2000: $31 StartRoutineByLocalIdentifier $FB Read Status (System Supplier Specific) $15 pwm output $01 Tail Light
- [STATUS_ANALOG_BLINKER](#job-status-analog-blinker) - Read the Blinkers analog values KWP2000: $31 StartRoutineByLocalIdentifier $FB Read Status (system supplier specific) $1A read ADC inputs
- [STEUERN_PWM_CONTROL](#job-steuern-pwm-control) - Control the PWM outputs KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $15 PWM control
- [STATUS_PWM_CONTROL](#job-status-pwm-control) - Read the PWM output values KWP2000: $31 StartRoutineByLocalIdentifier $FB Read Status (system supplier specific) $15 pwm output
- [STATUS_ANALOG_EINGANG](#job-status-analog-eingang) - Read the input analog values KWP2000: $31 StartRoutineByLocalIdentifier $FB system supplier specific $1A read ADC $01 read ADC inputs
- [STEUERN_LCD_CONTROL](#job-steuern-lcd-control) - Control the LCD KWP2000: $31 StartRoutineByLocalIdentifier $FA System supplier specific $17 control LCD
- [STEUERN_DATE_TIME](#job-steuern-date-time) - Set the clock date and time KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $10 Set Date/Time
- [STATUS_DATE_TIME](#job-status-date-time) - Read the clock date and time KWP2000: $21 ApplDiagReadDataByLocalIdentifier $10 Read Date/Time
- [STATUS_ANALOG_AUSGANG](#job-status-analog-ausgang) - Read the current sense values KWP2000: $31 StartRoutineByLocalIdentifier $FB system supplier specific $1A read ADC inputs $02 read ADC current sense
- [STEUERN_ZEIGERINSTRUMENT](#job-steuern-zeigerinstrument) - Control the pointer of the speedometer gauge KWP2000: $31 StartRoutineByLocalIdentifier $FA Set Status $0D Gauge Position
- [STEUERN_FERNLICHT](#job-steuern-fernlicht) - Control the High Beam directly KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED $12 High Beam
- [STEUERN_SCHLUESSEL_SPERRE](#job-steuern-schluessel-sperre) - Job used to enable or disable a key The job works only if a valid key is currently in the transponder coil The key in the transponder coil cannot be disabled or enabled 0x2E WriteDataByIndentifier 0xDC73 STEUERN_SCHLUESSEL_SPERRE
- [STEUERN_HUPE](#job-steuern-hupe) - Control the horn directly KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED $13 Horn
- [STEUERN_GWSZ_OFFSET](#job-steuern-gwsz-offset) - Job to wtite the odometer offset KWP2000: $22 ReadDataByCommonIdentifier $D10D SubService ID to read the absolute odometer value KWP2000: $2E WriteDataByCommonIdentifier $D114 SubService ID to write the odometer offset value
- [STATUS_GWSZ_OFFSET_LESEN](#job-status-gwsz-offset-lesen) - Job to read the odometer offset [km] KWP2000: $22 ReadDataByCommonIdentifier $D114 SubService ID to read the odometer offset value
- [STATUS_GWSZ_ABSOLUT](#job-status-gwsz-absolut) - Job to read the absolute odometer value [km] KWP2000: $22 ReadDataByCommonIdentifier $D10D SubService ID to read the absolute odometer value

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

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardware-Versionsindex |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_VAR_INDEX | int | Varianten-Index |
| ID_DATUM_JAHR | int | Herstelldatum (Jahr) |
| ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| ID_DATUM_TAG | int | Herstelldatum (Tag) |
| ID_DATUM | string | Herstelldatum (TT.MM.JJJJ) |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) |
| ID_SG_ADR | long | Steuergeraeteadresse bzw. LIN Master Steuergeraeteadresse |
| ID_LIN_SLAVE_ADR | long | LIN Slave Steuergeraeteadresse |
| ID_EWS_SS | int | Identifikation EWS-Schnittstelle Nur fuer DS2-Bordnetz benoetigt Fuer EWS-DME/DDE Abgleich |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-detail"></a>
### FS_LESEN_DETAIL

Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Fehlercode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_PCODE | unsigned int | optional / Pflicht fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_PCODE7 | unsigned int | optional / fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE7_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE7_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_LZ | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_ART_ANZ | int | Anzahl der zusaetzlichen Fehlerarten Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_ARTi_NR   Index der i. Fehlerart (string) F_ARTi_TEXT Text  zur i. Fehlerart |
| F_UW_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | 0x????: Angabe eines einzelnen Fehlers 0xFFFB: alle Antriebsfehler 0xFFFC: alle Fahrwerkfehler 0xFFFD: alle Karosseriefehler 0xFFFE: alle Netzwerkfehler Default: 0xFFFF: alle Fehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-normaler-datenverkehr"></a>
### NORMALER_DATENVERKEHR

Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREIGEBEN | string | "ja"   -&gt; normalen Datenverkehr freigeben "nein" -&gt; normalen Datenverkehr sperren table DigitalArgument TEXT |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |
| FUNKTIONAL | string | "ja"   -&gt; Funktionale Adresse 0xEF wird benutzt nur in Verbindung mit SG_ANTWORT="nein" "nein" -&gt; SG Adresse wird benutzt table DigitalArgument TEXT Default:  SG Adresse wird benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |
| FUNKTIONAL | string | "ja"   -&gt; Funktionale Adresse 0xEF wird benutzt nur in Verbindung mit SG_ANTWORT="nein" "nein" -&gt; SG Adresse wird benutzt table DigitalArgument TEXT Default:  SG Adresse wird benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-mode"></a>
### DIAGNOSE_MODE

SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |
| BAUDRATE | string | optionaler Parameter fuer die gewuenschte Baudrate table BaudRate BAUD |
| SPEZIFISCHE_BAUDRATE_WERT | long | Parameter nur fuer BAUDRATE = 'SB' ( spezifische Baudrate ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-ci-lesen"></a>
### C_CI_LESEN

Codierindex lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9B Vehicle Manufacturer Coding Index oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_COD_INDEX | int | Codier-Index |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-schreiben"></a>
### C_FG_SCHREIBEN

Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-aei-lesen"></a>
### C_AEI_LESEN

Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-schreiben"></a>
### C_AEI_SCHREIBEN

Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-auftrag"></a>
### C_AEI_AUFTRAG

Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-schreiben"></a>
### C_C_SCHREIBEN

Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-seriennummer-lesen"></a>
### SERIENNUMMER_LESEN

Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SERIENNUMMER | string | Seriennummer des Steuergeraets |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-zif-lesen"></a>
### ZIF_LESEN

Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_PROGRAMM_REFERENZ | string | PRGREF ProgrammReferenz letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| ZIF_SG_KENNUNG | string | ZZZ |
| ZIF_PROJEKT | string | PPPxV |
| ZIF_PROGRAMM_STAND | string | BBxh |
| ZIF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| ZIF_BMW_HW | string | VMECUH*N vehicleManufacturerECUHardware*Number BMW Hardware Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |

<a id="job-zif-backup-lesen"></a>
### ZIF_BACKUP_LESEN

Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_BACKUP_PROGRAMM_REFERENZ | string | PRGREFB ProgrammReferenzBackup letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| ZIF_BACKUP_SG_KENNUNG | string | ZZZ |
| ZIF_BACKUP_PROJEKT | string | PPPxV |
| ZIF_BACKUP_PROGRAMM_STAND | string | BBxh |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| ZIF_BACKUP_BMW_HW | string | VMECUH*NB vehicleManufECUHW*NumberBackup BMW Hardware* Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-physikalische-hw-nr-lesen"></a>
### PHYSIKALISCHE_HW_NR_LESEN

Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PHYSIKALISCHE_HW_NR | string | Physikalische Hardware-Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-hardware-referenz-lesen"></a>
### HARDWARE_REFERENZ_LESEN

Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HARDWARE_REFERENZ | string | Hardware Referenz Format: ZZZPPPx 7 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware |
| HW_REF_SG_KENNUNG | string | ZZZ |
| HW_REF_PROJEKT | string | PPPx |
| HW_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-daten-referenz-lesen"></a>
### DATEN_REFERENZ_LESEN

Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATEN_REFERENZ | string | Daten Referenz Format: ZZZPPPxVBBxhdxxxx 17 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller d     : Datenstandersteller xxxx  : frei aber eindeutig belegt |
| DATEN_REF_SG_KENNUNG | string | ZZZ |
| DATEN_REF_PROJEKT | string | PPPxV |
| DATEN_REF_PROGRAMM_STAND | string | BBxh |
| DATEN_REF_DATENSATZ | string | dxxxx |
| DATEN_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-zeiten-lesen"></a>
### FLASH_ZEITEN_LESEN

Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_LOESCHZEIT | int | Flash Loeschzeit in Sekunden |
| FLASH_SIGNATURTESTZEIT | int | Flash Signaturtestzeit in Sekunden |
| FLASH_RESETZEIT | int | Flash Resetzeit in Sekunden |
| FLASH_AUTHENTISIERZEIT | int | Flash Authentisierberechnungszeit in Sekunden |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-blocklaenge-lesen"></a>
### FLASH_BLOCKLAENGE_LESEN

Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_BLOCKLAENGE_GESAMT | unsigned int | Flash Blocklaenge inclusive SID |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-authentisierung-zufallszahl-lesen"></a>
### AUTHENTISIERUNG_ZUFALLSZAHL_LESEN

Authentisierung Zufallszahl des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $07 RequestForAuthentication Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LEVEL | int |  |
| USER_ID | long | optional |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ZUFALLSZAHL | binary | Zufallszahl |
| AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTHG_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-authentisierung-start"></a>
### AUTHENTISIERUNG_START

Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Authentisierungszeit in Sekunden Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Schluesseldaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-programmier-status-lesen"></a>
### FLASH_PROGRAMMIER_STATUS_LESEN

Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_PROGRAMMIER_STATUS_TEXT | string | table ProgrammierStatus STATUS_TEXT |
| FLASH_PROGRAMMIER_STATUS | int | ProgrammierStatus 0 - 255 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-signatur-pruefen"></a>
### FLASH_SIGNATUR_PRUEFEN

Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BEREICH | string | 'Programm' 'Daten' |
| SIGNATURTESTZEIT | int | Zeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-loeschen"></a>
### FLASH_LOESCHEN

Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Loeschzeit in Sekunden (Byteparameter 1) Byte 5,6            : Loeschzeit in Sekunden (WordParameter 1 (low/high)) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN_STATUS | int | Loeschstatus 1 = Speicher geloescht 2 = Speicher nicht geloescht 5 = Signaturpruefung PAF nicht durchgefuehrt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-adresse"></a>
### FLASH_SCHREIBEN_ADRESSE

Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge ohne Telegramm-Overhead |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_ANZAHL | unsigned int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
| FLASH_SCHREIBEN_STATUS | int | Programmierstatus 1 = Programmierung in Ordnung 2 = Programmierung nicht in Ordnung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_NUMMER | int | ==0 : aktuelles AIF &gt; 0 : Nummer des zu lesenden AIF default = 0 : aktuelles AIF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_ADRESSE_HIGH | int | AIF Adresse des AIF, High-Word |
| AIF_ADRESSE_LOW | int | AIF Adresse des AIF, Low-Word |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | long | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |
| AIF_ANZ_DATEN | int | Groesse des AIF-Eintrags |
| AIF_GROESSE | int | Groesse des AIF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-aif-schreiben"></a>
### AIF_SCHREIBEN

Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig oder 17-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ oder TTMMJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | long | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| AIF_NUMMER | int | Nummer des geschreibenen AIF |
| AIF_DATEN | binary | AIF Hex-Daten |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG AIF lesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG AIF lesen |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG AIF schreiben |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG AIF schreiben |

<a id="job-diagnose-mode-gateway"></a>
### DIAGNOSE_MODE_GATEWAY

SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |
| BAUDRATE | string | optionaler Parameter fuer die gewuenschte Baudrate table BaudRate BAUD |
| SPEZIFISCHE_BAUDRATE_WERT | long | Parameter nur fuer BAUDRATE = 'SB' ( spezifische Baudrate ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-baudrate-115200-gateway"></a>
### BAUDRATE_115200_GATEWAY

Umschaltung auf 115200 Baud (und BMW-FAST wg. Fast-Initialisation)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-flash-schreiben-xxl"></a>
### FLASH_SCHREIBEN_XXL

Flash Daten schreiben XXL-Format Standard Flashjob KWP2000: $36 TransferData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_ANZAHL | unsigned int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
| FLASH_SCHREIBEN_STATUS | int | Programmierstatus 1 = Programmierung in Ordnung 2 = Programmierung nicht in Ordnung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ng-flash-loeschen"></a>
### NG_FLASH_LOESCHEN

Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Loeschzeit in Sekunden (Byteparameter 1) Byte 5,6            : Loeschzeit in Sekunden (WordParameter 1 (low/high)) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN_STATUS | int | Loeschstatus 1 = Speicher geloescht 2 = Speicher nicht geloescht 5 = Signaturpruefung PAF nicht durchgefuehrt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-steuern-ews4"></a>
### STEUERN_EWS4

"EWS4-data" schreiben KWP 2000: $2E WriteDataByCommonIdentifier CommonIdentifier=0xC001

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | table Steuern_EWS4_Mode WRITE_DMEDDE_SK LOCK_DMEDDE_SK WRITE_TRSP_SK LOCK_TRSP_SK LOCK_EWS4 UNLOCK_DMEDDE_SK UNLOCK_TRSP_SK UNLOCK_DEL_DMEDDE_SK UNLOCK_DEL_TRSP_SK |
| DATA | string | Byte1...16 16 Byte Data (SecretKey or Authentication Key) MODE = WRITE_DMEDDE_SK/WRITE_TRSP_SK/UNLOCK_DMEDDE_SK/UNLOCK_TRSP_SK/UNLOCK_DEL_DMEDDE_SK/UNLOCK_DEL_TRSP_SK, "0x01,0x02,.." MODE = LOCK_TRSP_SK/LOCK_DMEDDE_SK/LOCK_EWS4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Read the status of the digital inputs KWP2000: 	$31 StartRoutineByLocalIdentifier $FB Read Status (System Supplier Specific) $0F Digital Port(s)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TRIP | int | Trip Input PK.00 Trip |
| STAT_BLINKER_RIGHT | int | Right Blinker Input PK.01 Right Blinker on/off |
| STAT_BLINKER_RESET | int | Reset Blinker Input PK.02 Reset Blinker |
| STAT_WINDS_DOWN | int | WindShield Down Input PK.03 WindShield Down setting |
| STAT_DRL | int | DRL Input PK.04 DRL on/off |
| STAT_WAKE | int | Wake Input PH.00 Wake Up Line |
| STAT_HAZARD | int | Hazard Input PH.01 Left and right blinker on/off |
| STAT_BLINKER_LEFT | int | Left Blinker Input PH.02 Left Blinker on/off |
| STAT_HIGH_BEAM | int | High Beam Input PH.03 High beam on/off |
| STAT_INFO | int | Info Input PA.05 Info |
| STAT_WINDS_UP | int | WindShield Up Input PA.06 WindShield Up setting |
| STAT_HSEATR | int | Heated Seat Rider Input PA.07 Heated Seat Rider |
| STAT_HSEATP1 | int | Heated Seat Pilion Low Input PS.02 Heated Seat Pilion Low |
| STAT_HGRIPS | int | Heated Grips Input PS.03 Heated Grips |
| STAT_HSEATP2 | int | Heated Seat Pilion High Input PJ.00 Heated Seat Pilion High |
| STAT_HORN | int | Horn Input PE.02 Horn |
| STAT_LUGGAGE_BOX | int | Luggage Box Input PE.04 Luggage Box |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-led-control"></a>
### STEUERN_LED_CONTROL

LEDs individuell ansteuern KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LED_TYPE | string | table Steuern_Led_Type 0x01 Left_Blinker 0x02 Right_Blinker 0x03 ABS 0x04 General Warning (RED) 0x05 High_Beam 0x06 DRL 0x07 Fuel_Reserve 0x08 MIL 0x09 DWA 0x0A General Warning (YELLOW) 0x0B All_Leds |
| LED_OPTION | string | table Steuern_Led_Option 0x00 led_off 0x01 led_on 0x02 led_flashing (1 Hz) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-ee-data"></a>
### WRITE_EE_DATA

Write the data in EEPROM KWP2000: $2E	WriteDataByCommonIdentifier $AAAA	Write data in EEPROM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| START_ADDRESS | string | Initial EE address (16 bit) |
| NUM_BYTES | string | Number of bytes to write (max 16) |
| DATA_BYTES | string | Data to write |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ng-signatur-pruefen"></a>
### NG_SIGNATUR_PRUEFEN

Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BEREICH | string | 'Programm' 'Daten' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ng-authentisierung-start"></a>
### NG_AUTHENTISIERUNG_START

Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Authentisierungszeit in Sekunden Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Schluesseldaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ews4-sk"></a>
### STATUS_EWS4_SK

KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier = 0xC002 Lesen des SecretKey des Server sowie Client für EWS4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS4_DMEDDE_SK | binary | SecretKey Server (16 byte) |
| STAT_EWS4_TRSP_SK | binary | SecretKey Client (16 byte) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-ee-data"></a>
### READ_EE_DATA

Read the data in EEPROM KWP2000: $22 ReadDataByCommonIdentifier $BBBB	Read data in EEPROM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| START_ADDRESS | string | Initial EE address (16 bit) |
| NUM_BYTES | string | Number of bytes to read (max 16) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EE_DATA_BYTES | binary | Data bytes (max 16) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ews"></a>
### STATUS_EWS

KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier = 0xC000 Read the current status of the EWS SecretKeys

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TRSP_SK_LOCKED | unsigned char | TRSP_SK (1 = Locked / 0 = Unlocked) |
| STAT_DMEDDE_SK_LOCKED | unsigned char | DMEDDE_SK (1 = Locked / 0 = Unlocked) |
| STAT_VERSION | unsigned char | Version of the EWS4 interface 1 = SecretKey written directly |
| JOB_STATUS | string | "OKAY", if no errors |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schluesseldaten"></a>
### STATUS_SCHLUESSELDATEN

Read the transponder table key data Service 	$31 	(Service routine control) Sub-ID 	$01 	(Start routine) RID 		0xAC5A 	(For reading out the key data from the transponder table)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TAB_INDEX | unsigned char | Position of the key data to read Setting performed according to the table TAB_CAS_SCHLUESSEL_POSITION |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEY_DISABLED | unsigned char | Key status (enabled/disabled) Setting performed according to the table TAB_CAS_SCHLUESSELSPERRE |
| STAT_KEY_DISABLED_TEXT | string | Key status (enabled/disabled) Setting performed according to the table TAB_CAS_SCHLUESSELSPERRE |
| STAT_INIT_DONE | unsigned char | Key initialization status Setting performed according to the table TAB_CAS_TRSP_INITSTATUS 1 = valid key 255 = Free key position |
| STAT_INIT_DONE_TEXT | string | Key initialization status Setting performed according to the table TAB_CAS_TRSP_INITSTATUS 1 = valid key 255 = Free key position |
| STAT_KEY_ID_WERT | binary | Key Identifier 4 Byte hex All the values are valid, except 'FF FF FF FF' (unknown) |
| STAT_KEY_ID_EINH | string | Key Identifier unit |
| STAT_KEY_TYPE | unsigned char | Key type Setting performed according to the table TAB_CAS_KEYTYPE |
| STAT_KEY_TYPE_TEXT | string | Key type Setting performed according to the table TAB_CAS_KEYTYPE |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-schluesseldaten"></a>
### STEUERN_SCHLUESSELDATEN

Writing in the KOMBI of the KEY_IDs only if the EWS4_TRSP_SK is unlocked Service: $2E WriteDataByIdentifier SubService: 0xDC80 STEUERN_SCHLUESSELDATEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TAB_INDEX | unsigned char | Position of the key in the transponder table Setting performed according to the table TAB_CAS_SCHLUESSEL_POSITION |
| KEY_ID | string | Identifier of the key to write (4 Byte hex value) All values are accepted, except 'FF FF FF FF' Format: '01 23 45 67' or '0x01,0x23,0x45,0x67' |
| KEY_TYPE | unsigned char | Type of the key to write Setting performed according to the table TAB_CAS_KEYTYPE |
| KEY_DISABLED | unsigned char | Key enabled/disabled Setting performed according to the table TAB_CAS_SCHLUESSELSPERRE Only the values 0 and 1 are allowed |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-fahrgestellnummer"></a>
### STEUERN_FAHRGESTELLNUMMER

Writing of VIN JobHeaderFormat Service $2E: WiteDataByIdentifier SubService $F190: DID for writing the VIN (17 digits)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FGNR17 | string | VIN (17 digits) Only the values '0..9' and 'A..Z' are valid If the argument is set to '00000000000000000', it is converted in the SGBD to '0xFF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF' before sending to the KOMBI |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-fahrgestellnummer"></a>
### STATUS_FAHRGESTELLNUMMER

Read the Vehicle Identification Number JobHeaderFormat Service: $22 -&gt; ReadDataByIdentifier SubService: $F190 -&gt; DID to read the VIN (17 digits)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FGNR17_WERT | string | VIN (17 digits) VIN = '00000000000000000' if the unit is virgin If the response of the KOMBI is 'FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF', the string '00000000000000000' is returned |
| STAT_FGNR17_EINH | string | Unit of VIN |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-cas-init-loc-date"></a>
### STEUERN_CAS_INIT_LOC_DATE

Write the key init data in the KOMBI JobHeaderFormat Service: $2E (WriteDataByIdentifier) SubService: $DC7B (DID for writing the time stamp, location and station data of the key init in the KOMBI)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INIT_DAY | unsigned char | Day of the key initialization Valid range [1..31] |
| INIT_MONTH | unsigned char | Month of the key initialization Valid range [1..12] |
| INIT_YEAR | unsigned int | Year of the key initialization Valid range [2000..9999] |
| INIT_LOCATION | string | Location of the key initialization Format -&gt; 4 ASCII characters |
| INIT_STATION | string | BMW specific designation of the learning station Format -&gt; 4 ASCII characters Examples DC22, DA21, DN01, ... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cas-init-loc-date"></a>
### STATUS_CAS_INIT_LOC_DATE

Read the key init data stored in the KOMBI JobHeaderFormat Service $22 (ReadDataByIdentifier) SubService $DC7B (DID for reading out the time stamp, location and station data of the key init in the KOMBI)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INIT_DAY_WERT | unsigned char | Day of the key initialization Valid range [1..31] |
| STAT_INIT_DAY_EINH | string | Day unit |
| STAT_INIT_MONTH_WERT | unsigned char | Month of the key initialization Valid range [1..12] |
| STAT_INIT_MONTH_EINH | string | Month unit |
| STAT_INIT_YEAR_WERT | unsigned int | Year of the key initialization Valid range [2000..9999] |
| STAT_INIT_YEAR_EINH | string | Year unit |
| STAT_INIT_LOCATION_WERT | string | Location of the key initialization Format -&gt; 4 ASCII characters |
| STAT_INIT_LOCATION_EINH | string | Location unit |
| STAT_INIT_STATION_WERT | string | BMW specific designation of the learning station Format -&gt; 4 ASCII characters Examples DC22, DA21, DN01, ... |
| STAT_INIT_STATION_EINH | string | Station unit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-cas-anlieferzustand"></a>
### STEUERN_CAS_ANLIEFERZUSTAND

Put the KOMBI in delivery condition If the conditions to put the KOMBI in delivery status are wrong, return 'ERROR_ECU_CONDITIONS_NOT_CORRECT' After the data reset, all the lock flags shall be also reset JobHeaderFormat Service $31 -&gt; Service routine control SubID $01 -&gt; Sub-ID for start routine RID $AC50 -&gt; RID for resetting the KOMBI into delivery condition

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EWS4_TRSP_SK | string | If the TRSP_SK in the KOMBI isn't locked, this parameter isn't needed 16-Byte hex in the format '0x01,0x02,0x03' or '01 02 03' or '0x01 0x02 0x03' or '01,02,03' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-c-fa-auftrag"></a>
### C_FA_AUFTRAG

Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F0A Fahrzeugauftrag Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-lesen"></a>
### C_FA_LESEN

Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F7F Fahrzeugauftrag Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | Daten des Fahrzeugauftrages |
| SPEICHER_STATUS | string | BELEGT bzw. UNBELEGT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-schreiben"></a>
### C_FA_SCHREIBEN

Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F0A Fahrzeugauftrag Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schluessel-init"></a>
### STEUERN_SCHLUESSEL_INIT

Start key initialisation. Service: $31 StartRoutineByLocalIdentifier Sub-ID: 0x01 for start routine RID: 0xAC52 for starting the key

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TAB_INDEX | unsigned char | Position of the key in the transponder table Setting performed according to the table TAB_CAS_SCHLUESSEL_POSITION |
| KEY_ID | string | Identifier of the key to write (4 Byte hex value) All values are accepted, except 'FF FF FF FF' Format: '01 23 45 67' or '0x01,0x23,0x45,0x67' |
| KEY_TYPE | unsigned char | Type of the key to write Setting performed according to the table TAB_CAS_KEYTYPE |
| INIT_MODE | unsigned char | Learning Mode (optional) Only the values 0 and 1 are allowed 0 = Key isn't locked 1 = Learn Normally and lock transponder memory (default) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-schluessel-trsp"></a>
### STATUS_SCHLUESSEL_TRSP

Read the status of the last transponder found Service 	$22 	(Read data) DID 		0xDC7E 	(For reading out the key status)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEY_ID_WERT | binary | Key Identifier 4 Byte hex All the values are valid, except 'FF FF FF FF' (key reading) or '00 00 00 00' (key unknown) |
| STAT_KEY_ID_EINH | string | Key Identifier unit |
| STAT_KEY_TYPE | unsigned char | Key type Setting performed according to the table TAB_CAS_KEYTYPE |
| STAT_KEY_TYPE_TEXT | string | Key type Setting performed according to the table TAB_CAS_KEYTYPE |
| STAT_KEY_FREQ | unsigned char | Key frequency Setting performed according to the table TAB_CAS_FREQ |
| STAT_KEY_FREQ_TEXT | string | Key frequency Setting performed according to the table TAB_CAS_FREQ |
| STAT_KEY_TRSP_TYPE | unsigned char | type of transponder Setting performed according to the table TAB_CAS_TRSP_TYPE |
| STAT_KEY_TRSP_TYPE_TEXT | string | type of transponder Setting performed according to the table TAB_CAS_TRSP_TYPE |
| STAT_KEY_MECHCODE_WERT | string | mechanical lock code 10 characters e.g. 'HF000xxxxx', where x is an hex digit The ECU returns only 5 bytes, the first 4 bytes are the MLC and the 5th byte is the checksum 5 characters are added by SGBD If the ECU returns 0xFF, 0xFF, 0xFF, 0xFF, 0xFF, no MLC is written in the transponder. In this case, the SGBD has to return 'K000000000' |
| STAT_KEY_MECHCODE_EINH | string | mechanical lock code |
| STAT_FBD_BATTERIE_ZUSTAND | unsigned char | value for the quantised battery voltage of the transmitting key Setting performed according to the table TAB_CAS_FBD_BATTERIEZUSTAND |
| STAT_FBD_BATTERIE_ZUSTAND_TEXT | string | value for the quantised battery voltage of the transmitting key Setting performed according to the table TAB_CAS_FBD_BATTERIEZUSTAND |
| STAT_KEY_VIN17_WERT | binary | VIN 17 Byte hex 17 bytes VIN in the key |
| STAT_KEY_VIN17_EINH | string | 17 bytes VIN in the key |
| STAT_TAB_INDEX | unsigned char | key position in transponder table Setting performed according to the table TAB_CAS_SCHLUESSEL_POSITION |
| STAT_TAB_INDEX_TEXT | string | key position in transponder table Setting performed according to the table TAB_CAS_SCHLUESSEL_POSITION |
| STAT_KEY_VALID | unsigned char | status whether the current key is valid |
| STAT_KEY_ID_KNOWN | unsigned char | status whether the key is known in the CAS |
| STAT_KEY_DISABLED | unsigned char | Key status (enabled/disabled) Setting performed according to the table TAB_CAS_SCHLUESSELSPERRE |
| STAT_KEY_DISABLED_TEXT | string | Key status (enabled/disabled) Setting performed according to the table TAB_CAS_SCHLUESSELSPERRE |
| STAT_INIT_DONE | unsigned char | Key initialization status Setting performed according to the table TAB_CAS_TRSP_INITSTATUS 1 = valid key 255 = Free key position |
| STAT_INIT_DONE_TEXT | string | Key initialization status Setting performed according to the table TAB_CAS_TRSP_INITSTATUS 1 = valid key 255 = Free key position |
| STAT_TRSP_ERROR | unsigned char | the result indicates whether communication errors and learning errors have occurred Setting performed according to the table TAB_CAS_TRSP_ERROR |
| STAT_TRSP_ERROR_TEXT | string | the result indicates whether communication errors and learning errors have occurred Setting performed according to the table TAB_CAS_TRSP_ERROR |
| STAT_KEY_LOCKED | unsigned char | locking status of the AES transponder Setting performed according to the table TAB_CAS_TRSP_VERRIEGELUNGSSTATUS |
| STAT_KEY_LOCKED_TEXT | string | locking status of the AES transponder Setting performed according to the table TAB_CAS_TRSP_VERRIEGELUNGSSTATUS |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cas-anlieferzustand"></a>
### STATUS_CAS_ANLIEFERZUSTAND

Indicate the current progress of the reset after STEUERN_CAS_ANLIEFERZUSTAND JobHeaderFormat Service $22 (ReadDataByIdentifier) SubService 0xDC7D (DID for return the progress of the EWS4 parameter reset)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EEBLOCKS_TODO | int | Number of blocks still to be deleted in the CAS 0 -&gt; Deletion complete 255 -&gt; No deletion in this alive cycle 0 &lt; Value &lt; 255 -&gt; Number of blocks still to be deleted |
| STAT_EEBLOCKS_TODO_TEXT | string | Number of blocks still to be deleted in the CAS 0 -&gt; Deletion complete 255 -&gt; No deletion in this alive cycle 0 &lt; Value &lt; 255 -&gt; Number of blocks still to be deleted |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern"></a>
### STEUERN

Write the HO INFO in the KOMBI JobHeaderFormat Service $2E: WiteDataByIdentifier SubService $DC54: DID for write the HO INFO (9 bytes)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAM | string | Should be "ARG" |
| PARAM_NAME | string | Should be "HO_INFO" |
| DEALER_NR | string | Dealer number (5 digits) Numeric code '0..9' |
| REG_DAY | unsigned char | Day of the registration Valid range [1..31] |
| REG_MONTH | unsigned char | Month of the registration Valid range [1..12] |
| REG_YEAR | unsigned int | Year of the registration Valid range [2000..9999] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-production-mode"></a>
### STEUERN_PRODUCTION_MODE

Set or reset the Production Mode coding flag in the KOMBI JobHeaderFormat $2E: WiteDataByIdentifier $DC55: DID for write the Production Mode coding flag (1 bit)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRODUCTION_MODE | unsigned char | 1 -&gt; ON 0 -&gt; OFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-gwsz-anzeige"></a>
### STATUS_GWSZ_ANZEIGE

Kilometers reading KWP2000: $21 ReadDataByLocalIdentifier $01 SubService ID to read the Odometer value KWP2000: $22 ReadDataByCommonIdentifier $3007 SubService ID to read the Odometer unit (Miles or KM)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GWSZ_ANZEIGE_WERT | real | Kilometers Valid range: 0 to 429496729.4 Not valid value (EEPROM reading error): -1 |
| STAT_GWSZ_ANZEIGE_EINH | string | km or miles |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-gwsz-anzeige-schreiben"></a>
### STEUERN_GWSZ_ANZEIGE_SCHREIBEN

Odometer writing KWP2000: $3B WriteDataByLocalIdentifier $01 SubService ID to write the Odometer value

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GWSZ_WERT | real | Odometer (KM or Miles) Valid range: 0 to 999999 In order to display the new value, trigger the Reset!! |
| GWSZ_ANZEIGE_EINH | string | km or miles |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-start-kalibrierung-windschild"></a>
### STEUERN_START_KALIBRIERUNG_WINDSCHILD

Start der Kalibrierung des Windschildes KWP2000: $31 StartRoutineByLocalId $21 Windshield $01 Start Reference Run

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIBRIERUNG_TEXT | string | table Tab_Kalibrierung_Windschild STATUS_TEXT |
| STAT_KALIBRIERUNG_WERT | char | table Tab_Kalibrierung_Windschild STATUS_NUMMER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kalibrierung-windschild"></a>
### STATUS_KALIBRIERUNG_WINDSCHILD

Status Kalibrierung Windschild KWP2000: $31 StartRoutineByLocalId $21 Windshield $03 Status of Reference Run

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIBRIERUNG_TEXT | string | table Tab_Kalibrierung_Windschild STATUS_TEXT |
| STAT_KALIBRIERUNG_WERT | char | table Tab_Kalibrierung_Windschild STATUS_NUMMER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-service-date"></a>
### STATUS_SERVICE_DATE

Job to read the Service Date KWP2000: $21 ApplDiagReadDataByLocalIdentifier $11 Read Service_Date

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERV_DATE_DD | int | Service Date: day |
| STAT_SERV_DATE_MM | int | Service Date: Month |
| STAT_SERV_DATE_YYYY | int | Service Date: Year |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-steuern-service-date"></a>
### STEUERN_SERVICE_DATE

Service Date writing KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $11 Set Service_Date

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERV_DATE_DD | int | Service Date -&gt; day (DD = 1..28,29,30,31) |
| SERV_DATE_MM | int | Service Date -&gt; month (MM = 1..12) |
| SERV_DATE_YYYY | int | Service Date -&gt; Year (YYYY = 2011..2099) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-service-restweg"></a>
### STATUS_SERVICE_RESTWEG

Remaining service distance reading KWP2000:  $22 ApplDiagReadDataByCommonIdentifier $3007 Coding block for odometer unit setting $21 ApplDiagReadDataByLocalIdentifier $12 Read Actual_Service_Mileage_Range in [km]

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERV_WEG_WERT | real | Remaining service distance [km] |
| STAT_SERV_WEG_EINHEIT | string | km or miles |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag1 an SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag2 an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort1 von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort2 von SG |

<a id="job-steuern-service-restweg"></a>
### STEUERN_SERVICE_RESTWEG

Service distance interval writing KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $12 Set actual service mileage range in [km]

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERV_WEG_WERT | real | new value of service distance interval in km or miles max value &lt;= 65535 |
| SERV_WEG_EINHEIT | string | km or miles |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-self-test-on"></a>
### STEUERN_SELF_TEST_ON

Kombi Selbsttest KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $18 self test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-self-test-off"></a>
### STEUERN_SELF_TEST_OFF

Kombi Self Test KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $18 self test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-windschild"></a>
### STATUS_WINDSCHILD

Status des Windschilds KWP2000: $30 InputOutputByLocalId $05 Windshield $01 Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HIGH_POS | int | WindShield upper position (Hall sensor pulses) |
| STAT_POS_COUNT | int | WindShield current position (Hall sensor pulses) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-windschild"></a>
### STEUERN_WINDSCHILD

Windschild ansteuern KWP2000: $30 InputOutputControlByLocalIdentifier $05 Windshield $07 ShortTermAdjustment $XX Windshield Parameter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WS_OPTION | string | Windschild ansteuern Werte: table Steuern_Windshield_Arg WINDSHIELD_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-blinker-rechts"></a>
### STEUERN_BLINKER_RECHTS

Control the Right Blinkers directly KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Turn ON/OFF the right blinkers Values: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-blinker-links"></a>
### STEUERN_BLINKER_LINKS

Control the Left Blinkers directly KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Turn ON/OFF the left blinkers Values: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-standlicht"></a>
### STEUERN_STANDLICHT

Position lights controlled directly Pre-requirement: Execution of the Job STEUERN_VORBEREITEN KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED $10 Position Light

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Turn ON/OFF the position lights Values: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-abblendlicht"></a>
### STEUERN_ABBLENDLICHT

Control the Low Beam directly KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Turn ON/OFF the Low Beam Values: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ruecklicht"></a>
### STEUERN_RUECKLICHT

Control the Tail lights Pre-requirement: execute the job STEUERN_VORBEREITEN KWP2000: $31 InputOutputControlByLocalIdentifier $FA System Supplier Specific $15 pwm output $01 Tail Light

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | int | Tail light PWM value Range from 0 to 100 [%] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ruecklicht"></a>
### STATUS_RUECKLICHT

Read the tail light pwm value Pre-requirement: execute the job STEUERN_VORBEREITEN KWP2000: $31 StartRoutineByLocalIdentifier $FB Read Status (System Supplier Specific) $15 pwm output $01 Tail Light

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RUECKLICHT | int | Tail light PWM value Range from 0 to 100 [%] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-blinker"></a>
### STATUS_ANALOG_BLINKER

Read the Blinkers analog values KWP2000: $31 StartRoutineByLocalIdentifier $FB Read Status (system supplier specific) $1A read ADC inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LEFT_WERT | real | Left Blinker sense value |
| STAT_LEFT_EINH | string | A |
| STAT_RIGHT_WERT | real | Right blinker sense value |
| STAT_RIGHT_EINH | string | A |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm-control"></a>
### STEUERN_PWM_CONTROL

Control the PWM outputs KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $15 PWM control

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PWM | string | table pwm PWM_TEXT |
| VALUE | int | PWM value Range from 0 to 100 [%] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pwm-control"></a>
### STATUS_PWM_CONTROL

Read the PWM output values KWP2000: $31 StartRoutineByLocalIdentifier $FB Read Status (system supplier specific) $15 pwm output

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TAIL_LIGHT_WERT | int | Tail light PWM value Range from 0 to 100 [%] |
| STAT_TAIL_LIGHT_EINH | string | % |
| STAT_POSITION_LIGHT_WERT | int | Position light PWM value Range from 0 to 100 [%] |
| STAT_POSITION_LIGHT_EINH | string | % |
| STAT_BRAKE_LIGHT_WERT | int | Brake light PWM value Range from 0 to 100 [%] |
| STAT_BRAKE_LIGHT_EINH | string | % |
| STAT_HEATED_GRIPS_WERT | int | Heated Grips PWM value Range from 0 to 100 [%] |
| STAT_HEATED_GRIPS_EINH | string | % |
| STAT_RIDER_HEATED_SEAT_WERT | int | Rider Heated Seat PWM value Range from 0 to 100 [%] |
| STAT_RIDER_HEATED_SEAT_EINH | string | % |
| STAT_PILLOW_HEATED_SEAT_WERT | int | Pillow Heated Seat PWM value Range from 0 to 100 [%] |
| STAT_PILLOW_HEATED_SEAT_EINH | string | % |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG4 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT4 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG5 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT5 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG6 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT6 | binary | Hex-Antwort von SG |

<a id="job-status-analog-eingang"></a>
### STATUS_ANALOG_EINGANG

Read the input analog values KWP2000: $31 StartRoutineByLocalIdentifier $FB system supplier specific $1A read ADC $01 read ADC inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VKEY_WERT | real | Key voltage Range from 0 to 16 Volt |
| STAT_VKEY_EINH | string | V |
| STAT_FUEL_LEVEL_WERT | real | Fuel level voltage Range from 0 to 5 Volt |
| STAT_FUEL_LEVEL_EINH | string | V |
| STAT_VDD_WERT | real | VDD voltage Range from 0 to 5 Volt |
| STAT_VDD_EINH | string | V |
| STAT_TEMP_WERT | real | PCB temperature |
| STAT_TEMP_EINH | string | °C |
| STAT_TAIR_WERT | real | Air Temperature voltage |
| STAT_TAIR_EINH | string | V |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lcd-control"></a>
### STEUERN_LCD_CONTROL

Control the LCD KWP2000: $31 StartRoutineByLocalIdentifier $FA System supplier specific $17 control LCD

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LCD_OPTION | string | table lcd_option LCD_OPTION 1 lcd_positive 2 lcd_negative |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-date-time"></a>
### STEUERN_DATE_TIME

Set the clock date and time KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $10 Set Date/Time

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TIME_HH | unsigned int | Time -&gt; Hour (HH) = 0..23 No argument (computer time) |
| TIME_MM | unsigned int | Time -&gt; Minutes (MM) = 0..59 No argument (computer time) |
| TIME_SS | unsigned int | Time -&gt; Seconds (SS) = 0..59 No argument (computer time) |
| DATE_DD | unsigned int | Date -&gt; Day (DD) = 1..28,29,30,31 No argument (computer date) |
| DATE_MM | unsigned int | Date -&gt; Month (MM) = 1..12 No argument (computer date) |
| DATE_YYYY | unsigned int | Date -&gt; Year (YYYY) = 2011..2099 No argument (computer date) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-date-time"></a>
### STATUS_DATE_TIME

Read the clock date and time KWP2000: $21 ApplDiagReadDataByLocalIdentifier $10 Read Date/Time

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME_HH | unsigned int | Time -&gt; Hour |
| STAT_TIME_MM | unsigned int | Time -&gt; Minutes |
| STAT_TIME_SS | unsigned int | Time -&gt; Seconds |
| STAT_DATE_DD | unsigned int | Date -&gt; Day |
| STAT_DATE_MM | unsigned int | Date -&gt; Month |
| STAT_DATE_YYYY | unsigned int | Date -&gt; Year |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-analog-ausgang"></a>
### STATUS_ANALOG_AUSGANG

Read the current sense values KWP2000: $31 StartRoutineByLocalIdentifier $FB system supplier specific $1A read ADC inputs $02 read ADC current sense

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LEFT_BLINKER_WERT | real | Left Blinker current sense |
| STAT_LEFT_BLINKER_EINH | string | A |
| STAT_RIGHT_BLINKER_WERT | real | Right Blinker current sense |
| STAT_RIGHT_BLINKER_EINH | string | A |
| STAT_POSITION_LIGHT_WERT | real | Position Light current sense |
| STAT_POSITION_LIGHT_EINH | string | A |
| STAT_TAIL_LIGHT_WERT | real | Tail Light current sense |
| STAT_TAIL_LIGHT_EINH | string | A |
| STAT_HSEATR_WERT | real | Rider Heated Seat current sense |
| STAT_HSEATR_EINH | string | A |
| STAT_HSEATP_WERT | real | Passenger Heated Seat current sense |
| STAT_HSEATP_EINH | string | A |
| STAT_HBEAM_WERT | real | High Beam current sense |
| STAT_HBEAM_EINH | string | A |
| STAT_LBEAM_WERT | real | Low Beam current sense |
| STAT_LBEAM_EINH | string | A |
| STAT_HGRIPS_WERT | real | Heated Grips current sense |
| STAT_HGRIPS_EINH | string | A |
| STAT_HORN_WERT | real | Horn current sense |
| STAT_HORN_EINH | string | A |
| STAT_BLIGHT_WERT | real | Brake Lights current sense |
| STAT_BLIGHT_EINH | string | A |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zeigerinstrument"></a>
### STEUERN_ZEIGERINSTRUMENT

Control the pointer of the speedometer gauge KWP2000: $31 StartRoutineByLocalIdentifier $FA Set Status $0D Gauge Position

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPEEDO_VALUE | string | Speedometer control value [km/h] Range from 0 to 180 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fernlicht"></a>
### STEUERN_FERNLICHT

Control the High Beam directly KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED $12 High Beam

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Turn ON/OFF the High Beam Values: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schluessel-sperre"></a>
### STEUERN_SCHLUESSEL_SPERRE

Job used to enable or disable a key The job works only if a valid key is currently in the transponder coil The key in the transponder coil cannot be disabled or enabled 0x2E WriteDataByIndentifier 0xDC73 STEUERN_SCHLUESSEL_SPERRE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TAB_INDEX | unsigned char | Key selection in the transponder table See the table TAB_CAS_SCHLUESSEL_POSITION Valid values 0-9 |
| SCHL_SPERRE | unsigned char | Enable or disable a key See the table TAB_CAS_SCHLUESSELSPERRE Valid values 0 or 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hupe"></a>
### STEUERN_HUPE

Control the horn directly KWP2000: $31 StartRoutineByLocalIdentifier $FA system supplier specific $13 control LED $13 Horn

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Turn ON/OFF the Horn Values: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-gwsz-offset"></a>
### STEUERN_GWSZ_OFFSET

Job to wtite the odometer offset KWP2000: $22 ReadDataByCommonIdentifier $D10D SubService ID to read the absolute odometer value KWP2000: $2E WriteDataByCommonIdentifier $D114 SubService ID to write the odometer offset value

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GWSZ_OFFSET_STEUERN | string | if GWSZ_Absolut &lt; 255 km, then OFFSET = GWSZ_Absolut if 255 km &lt;= GWSZ_Absolut &lt; 0x00188F7D km, then OFFSET = 255 km if GWSZ_Absolut &gt;= 0x00188F7D km, then do not write the ODO OFFSET in the cluster |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gwsz-offset-lesen"></a>
### STATUS_GWSZ_OFFSET_LESEN

Job to read the odometer offset [km] KWP2000: $22 ReadDataByCommonIdentifier $D114 SubService ID to read the odometer offset value

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GWSZ_OFFSET_WERT | unsigned char | Odometer offset value Range [0, 255] |
| STAT_GWSZ_OFFSET_EINH | string | Odometer offset unit [km] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gwsz-absolut"></a>
### STATUS_GWSZ_ABSOLUT

Job to read the absolute odometer value [km] KWP2000: $22 ReadDataByCommonIdentifier $D10D SubService ID to read the absolute odometer value

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ABSOLUT_GWSZ_WERT | unsigned long | Absolute odometer value Range [0, 1609597] |
| STAT_ABSOLUT_GWSZ_EINH | string | Absolute odometer unit [km] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (71 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (2 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (128 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [STEUERN_EWS4_MODE](#table-steuern-ews4-mode) (9 × 3)
- [STEUERN_LED_TYPE](#table-steuern-led-type) (11 × 3)
- [STEUERN_LED_OPTION](#table-steuern-led-option) (3 × 3)
- [TAB_CAS_SCHLUESSEL_POSITION](#table-tab-cas-schluessel-position) (14 × 2)
- [TAB_CAS_KEYTYPE](#table-tab-cas-keytype) (7 × 2)
- [TAB_CAS_SCHLUESSELSPERRE](#table-tab-cas-schluesselsperre) (2 × 2)
- [TAB_CAS_TRSP_INITSTATUS](#table-tab-cas-trsp-initstatus) (6 × 2)
- [TAB_CAS_FBD_BATTERIEZUSTAND](#table-tab-cas-fbd-batteriezustand) (10 × 2)
- [TAB_CAS_FREQ](#table-tab-cas-freq) (6 × 2)
- [TAB_CAS_TRSP_ERROR](#table-tab-cas-trsp-error) (1 × 2)
- [TAB_CAS_TRSP_INITSTATUS2](#table-tab-cas-trsp-initstatus2) (29 × 2)
- [TAB_CAS_TRSP_VERRIEGELUNGSSTATUS](#table-tab-cas-trsp-verriegelungsstatus) (4 × 2)
- [TAB_CAS_TRSP_TYPE](#table-tab-cas-trsp-type) (5 × 2)
- [TAB_KALIBRIERUNG_WINDSCHILD](#table-tab-kalibrierung-windschild) (8 × 3)
- [STEUERN_WINDSHIELD_ARG](#table-steuern-windshield-arg) (9 × 2)
- [PWM](#table-pwm) (6 × 2)
- [LCD_OPTION](#table-lcd-option) (2 × 2)

<a id="table-diagmode"></a>
### DIAGMODE

Dimensions: 14 rows × 3 columns

| NR | MODE | MODE_TEXT |
| --- | --- | --- |
| 0x81 | DEFAULT | DefaultMode |
| 0x82 | PT | PeriodicTransmissions |
| 0x84 | EOLSSM | EndOfLineSystemSupplierMode |
| 0x85 | ECUPM | ECUProgrammingMode |
| 0x86 | ECUDM | ECUDevelopmentMode |
| 0x87 | ECUAM | ECUAdjustmentMode |
| 0x88 | ECUVCM | ECUVariantCodingMode |
| 0x89 | ECUSM | ECUSafetyMode |
| 0xFA | SSS_A | SystemSupplierSpecific (A) |
| 0xFB | SSS_B | SystemSupplierSpecific (B) |
| 0xFC | SSS_C | SystemSupplierSpecific (C) |
| 0xFD | SSS_D | SystemSupplierSpecific (D) |
| 0xFE | SSS_E | SystemSupplierSpecific (E) |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-baudrate"></a>
### BAUDRATE

Dimensions: 7 rows × 3 columns

| NR | BAUD | BAUD_TEXT |
| --- | --- | --- |
| 0x01 | PC9600 | Baudrate 9.6 kBaud |
| 0x02 | PC19200 | Baudrate 19.2 kBaud |
| 0x03 | PC38400 | Baudrate 38.4 kBaud |
| 0x04 | PC57600 | Baudrate 57.6 kBaud |
| 0x05 | PC115200 | Baudrate 115.2 kBaud |
| 0x06 | SB | Specific Baudrate |
| 0xXY | -- | unbekannte Baudrate |

<a id="table-programmierstatus"></a>
### PROGRAMMIERSTATUS

Dimensions: 19 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Anlieferzustand |
| 0x01 | Normalbetrieb |
| 0x02 | nicht benutzt |
| 0x03 | Speicher gelöscht |
| 0x04 | nicht benutzt |
| 0x05 | Signaturprüfung PAF nicht durchgeführt |
| 0x06 | Signaturprüfung DAF nicht durchgeführt |
| 0x07 | Programmprogrammiersitzung aktiv |
| 0x08 | Datenprogrammiersitzung aktiv |
| 0x09 | Hardwarereferenzeintrag fehlerhaft |
| 0x0A | Programmreferenzeintrag fehlerhaft |
| 0x0B | Referenzierungsfehler Hardware -&gt; Programm |
| 0x0C | Programm nicht vorhanden oder nicht vollständig |
| 0x0D | Datenreferenzeintrag fehlerhaft |
| 0x0E | Referenzierungsfehler Programm -&gt; Daten |
| 0x0F | Daten nicht vorhanden oder nicht vollständig |
| 0x10 | Reserviert fuer BMW |
| 0x80 | Reserviert fuer Zulieferer |
| 0xXY | unbekannter Programmierstatus |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| - | BMW-FAST |
| - | KWP2000* |
| 1 | KWP2000 |
| 2 | D-CAN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 71 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9308 | No answare from the transponder |
| 0x9309 | Unknown key |
| 0x930A | Key disabled |
| 0x930B | Invalid Key |
| 0x930C | EWS4 Fault |
| 0x930D | High Beam open load or short circuit to UBatt |
| 0x930E | High Beam cc to GND |
| 0x930F | Low Beam open load or short circuit to UBatt |
| 0x9310 | Low Beam cc to GND |
| 0x9311 | Tail Light open load or short circuit to UBatt |
| 0x9312 | Tail Light cc to GND |
| 0x9313 | Position Light / DRL open load or short circuit to UBatt |
| 0x9314 | Position Light / DRL cc to GND |
| 0x9315 | Left Blink failure: one or two lamps open load or short circuit to Ubatt |
| 0x9316 | Left Blink cc to GND |
| 0x9317 | Right Blink failure: one or two lamps open load or short circuit to Ubatt |
| 0x9318 | Right Blink cc to GND |
| 0x9319 | Brake Light open load or short circuit to UBatt |
| 0x931A | Brake Light cc to GND |
| 0x931B | Windshield overcurrent |
| 0x931C | Windshield eeprom error |
| 0x931D | Windshield encoder fault |
| 0x931E | Fuel Sensor open load or short circuit to UBatt |
| 0x931F | Fuel Sensor cc GND |
| 0x9320 | Temp Sensor open load or short circuit to UBatt |
| 0x9321 | Temp Sensor cc GND |
| 0x9322 | Hardware error |
| 0x9323 | PCB High voltage |
| 0x9324 | PCB Low voltage |
| 0x9325 | Heated Seat Rider open load or short circuit to UBatt |
| 0x9326 | Heated Seat Rider cc GND |
| 0x9327 | Heated Seat Passenger open load or short circuit to UBatt |
| 0x9328 | Heated Seat Passenger cc GND |
| 0x9329 | Heated Grip open load or short circuit to UBatt |
| 0x932A | Heated Grip cc GND |
| 0x932B | HORN open load or short circuit to UBatt |
| 0x932C | HORN cc GND |
| 0x932D | SPARE HSD open load or short circuit to UBatt |
| 0x932E | SPARE HSD cc GND |
| 0x932F | INFO Button cc GND |
| 0x9330 | TRIP Button cc GND |
| 0x9331 | DRL Button cc GND |
| 0x9332 | RESET BLINKER Button cc GND |
| 0x9333 | LEFT BLINKER Button cc GND |
| 0x9334 | RIGHT BLINKER Button cc GND |
| 0x9335 | Left and Right Blinker buttons closed together |
| 0x9336 | HAZARD Button cc GND |
| 0x9337 | WINDSHIELD UP Button cc GND |
| 0x9338 | WINDSHIELD DOWN Button cc GND |
| 0x9339 | WindShield UP and DOWN buttons closed together |
| 0x933A | Heated Seat Rider Button cc GND |
| 0x933B | Heated Grip Button cc GND |
| 0x933C | Heated Seat Passenger 1 and 2 buttons closed together |
| 0x933D | Wake up line cc GND |
| 0x933E | Wake up line short circuit to UBatt |
| 0x933F | WindShield Overtemperature |
| 0x9340 | Production Mode active |
| 0x9341 | Odometer Compare Failure |
| 0x9342 | Error DMEDDE_SK |
| 0x9343 | Error TRSP_SK |
| 0x9344 | Odometer Fault |
| 0xE504 | ABS_1_MOTBK message missing |
| 0xE505 | SPEED_MOTBK message missing |
| 0xE506 | ENGINE_1_MOTBK message missing |
| 0xE507 | ENGINE_2_MOTBK message missing |
| 0xE508 | MILEAGE_REDUNDANT_MOTBK message missing |
| 0xE509 | ZFE_2_MOTBK message missing |
| 0xE50A | DWA_MOTBK message missing |
| 0xE50B | RDC_MOTBK message missing |
| 0xE50C | CAN Bus OFF |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xFFFF | 0x01 | 0x02 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 2 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Time second counter | sec | high | signed long | - | 1 | 1 | 0 |
| 0x02 | Battery Voltage | Volt | - | unsigned char | - | 1 | 10 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

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

Dimensions: 128 rows × 2 columns

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
| 0xAA | ArvinMeritor |
| 0xAB | Kongsberg Automotive GmbH |
| 0xAC | SMR Automotive Mirrors |
| 0xAD | So.Ge.Mi. |
| 0xAE | MTA |
| 0xAF | Alfmeier |
| 0xB0 | ELTEK VALERE DEUTSCHLAND GMBH |
| 0xB1 | Omron Automotive Electronics Europe Group |
| 0xB2 | ASK |
| 0xB3 | CML Innovative Technologies GmbH & Co. KG |
| 0xB4 | APAG Elektronik AG |
| 0xB5 | Nexteer Automotive World Headquarters |
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

<a id="table-authentisierung"></a>
### AUTHENTISIERUNG

Dimensions: 4 rows × 2 columns

| AUTH_NR | AUTH_TEXT |
| --- | --- |
| 0x01 | Simple |
| 0x02 | Symetrisch |
| 0x03 | Asymetrisch |
| 0xFF | Keine |

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 5 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x10 | D-CAN |
| 0x0F | BMW-FAST |
| 0x0D | KWP2000* |
| 0x0C | KWP2000 |
| 0x06 | DS2 |

<a id="table-steuern-ews4-mode"></a>
### STEUERN_EWS4_MODE

Dimensions: 9 rows × 3 columns

| NR | MODE | MODE_TEXT |
| --- | --- | --- |
| 0x02 | WRITE_DMEDDE_SK | Server_SK_Written |
| 0x04 | LOCK_DMEDDE_SK | Server_SK_Locked |
| 0x03 | WRITE_TRSP_SK | Client_SK_Written |
| 0x05 | LOCK_TRSP_SK | Client_SK_Locked |
| 0x01 | LOCK_EWS4 | ClientServer_SK_Locked |
| 0x06 | UNLOCK_DMEDDE_SK | Server_SK_Unlocked |
| 0x07 | UNLOCK_TRSP_SK | Client_SK_Unlocked |
| 0x10 | UNLOCK_DEL_DMEDDE_SK | Server_SK_Unlocked_and_Deleted |
| 0x11 | UNLOCK_DEL_TRSP_SK | Client_SK_Unlocked_and_Deleted |

<a id="table-steuern-led-type"></a>
### STEUERN_LED_TYPE

Dimensions: 11 rows × 3 columns

| NR | LED_TYPE | LED_TYPE_TEXT |
| --- | --- | --- |
| 0x01 | LEFT_BLINK | Left Blinker |
| 0x02 | RIGHT_BLINK | Right Blinker |
| 0x03 | ABS | ABS |
| 0x04 | RED ALARM | RED General Warning |
| 0x05 | HBEAM | High Beam |
| 0x06 | DRL | DRL |
| 0x07 | RESERVE | Fuel Reserve |
| 0x08 | MIL | MIL |
| 0x09 | DWA | DWA |
| 0x0A | YELLOW ALARM | YELLOW General Warning |
| 0x0B | ALL | All LED |

<a id="table-steuern-led-option"></a>
### STEUERN_LED_OPTION

Dimensions: 3 rows × 3 columns

| NR | LED_OPTION | LED_OPTION_TEXT |
| --- | --- | --- |
| 0x00 | LED_OFF | Led_turned_OFF |
| 0x01 | LED_ON | Led_turned_ON |
| 0x02 | LED_FLASHING | Led_flashing_1_HZ |

<a id="table-tab-cas-schluessel-position"></a>
### TAB_CAS_SCHLUESSEL_POSITION

Dimensions: 14 rows × 2 columns

| VALUE | TEXT |
| --- | --- |
| 0 | KEY 0 |
| 1 | KEY 1 |
| 2 | KEY 2 |
| 3 | KEY 3 |
| 4 | KEY 4 |
| 5 | KEY 5 |
| 6 | KEY 6 |
| 7 | KEY 7 |
| 8 | KEY 8 |
| 9 | KEY 9 |
| 252 | EMC test mode, LF ON |
| 253 | EMC test mode, LF OFF |
| 254 | Avoid ECU sleep |
| 255 | Invalid/Unknown |

<a id="table-tab-cas-keytype"></a>
### TAB_CAS_KEYTYPE

Dimensions: 7 rows × 2 columns

| VALUE | TEXT |
| --- | --- |
| 0 | Circulating key |
| 2 | Wallet key |
| 3 | Driver's key |
| 4 | Remote key |
| 5 | Transmitter ID |
| 15 | Future Spare key |
| 255 | Invalid/Unknown |

<a id="table-tab-cas-schluesselsperre"></a>
### TAB_CAS_SCHLUESSELSPERRE

Dimensions: 2 rows × 2 columns

| VALUE | TEXT |
| --- | --- |
| 0 | Key enabled |
| 1 | Key disabled |

<a id="table-tab-cas-trsp-initstatus"></a>
### TAB_CAS_TRSP_INITSTATUS

Dimensions: 6 rows × 2 columns

| VALUE | TEXT |
| --- | --- |
| 0 | Invalid status |
| 1 | Key valid |
| 2 | KEY_TYPE written, KEY_DISABLED has to be written |
| 3 | KEY_ID written, KEY_TYPE has to be written |
| 4 | KEY_ID has to be written |
| 255 | Free key position |

<a id="table-tab-cas-fbd-batteriezustand"></a>
### TAB_CAS_FBD_BATTERIEZUSTAND

Dimensions: 10 rows × 2 columns

| VALUE | TEXT |
| --- | --- |
| 0x00 | Very bad |
| 0x01 | Bad |
| 0x02 | Bad to fair |
| 0x03 | Fair |
| 0x04 | Fair to good |
| 0x05 | Good |
| 0x06 | Very good |
| 0x0A | Battery status weak |
| 0x0B | Battery status Good |
| 0xFF | Invalid or irrilevant |

<a id="table-tab-cas-freq"></a>
### TAB_CAS_FREQ

Dimensions: 6 rows × 2 columns

| VALUE | TEXT |
| --- | --- |
| 0x00 | UNKNOWN |
| 0x03 | 315 MHZ Low Power (Japan/Korea) |
| 0x04 | 315 MHZ |
| 0x05 | 433 MHZ |
| 0x06 | 868 MHZ |
| 0xFF | INVALID |

<a id="table-tab-cas-trsp-error"></a>
### TAB_CAS_TRSP_ERROR

Dimensions: 1 rows × 2 columns

| VALUE | TEXT |
| --- | --- |
| 0xFF | Unknown error |

<a id="table-tab-cas-trsp-initstatus2"></a>
### TAB_CAS_TRSP_INITSTATUS2

Dimensions: 29 rows × 2 columns

| VALUE | TEXT |
| --- | --- |
| 0x00 | Invalid status |
| 0x01 | Key completely learned |
| 0x14 | Verify seg. 5, block 0, page 0 |
| 0x18 | Write CAS-Init = 1 to the key (seg. 5,block 0, page 0 |
| 0x1C | Key authentication with the new crypto-data |
| 0x28 | Key isn't correctly configured, transponder reset |
| 0x2C | Verify key configuration |
| 0x30 | Read key configuration from transponder |
| 0x34 | Check the key configuration (locked and configured ?) |
| 0x38 | Write and lock the new configuration |
| 0x3C | Check the key configuration |
| 0x40 | Restart in the event of CFG writing cancellation |
| 0x54 | Verify Secret Key |
| 0x58 | Generation and writing of Secret Key |
| 0x5C | Select segment 0 |
| 0x70 | Generation and writing of password (page 3) to the key |
| 0x74 | Generation and writing of secret key high to the key |
| 0x78 | Generation and writing of secret key low to the key |
| 0x7C | Authentication with default SecretKeys |
| 0x88 | Initialisation of driving cycle counter |
| 0x8C | Initialisation of FBD and CA sequence counter |
| 0x9C | Initialisation of FBD data in the key |
| 0xD8 | Writing of BMW EOL data, block 1 to the key |
| 0xDC | Writing of BMW EOL data , block 0 to the key |
| 0xF0 | Key data are prepared, transponder reset |
| 0xF4 | Preparation of initialised position in the CAS: Deletion of CAM No,PIA No,BLOCKED |
| 0xF8 | Check the key data: frequency,type |
| 0xFC | Check the key configuration |
| 0xFF | Default value or wallet key |

<a id="table-tab-cas-trsp-verriegelungsstatus"></a>
### TAB_CAS_TRSP_VERRIEGELUNGSSTATUS

Dimensions: 4 rows × 2 columns

| VALUE | TEXT |
| --- | --- |
| 0x00 | Key not yet locked |
| 0x01 | Key completely locked |
| 0x03 | Erroneous configuration;initialisation impossible |
| 0xFF | Unknown transponder type |

<a id="table-tab-cas-trsp-type"></a>
### TAB_CAS_TRSP_TYPE

Dimensions: 5 rows × 2 columns

| VALUE | TEXT |
| --- | --- |
| 0x01 | Hitag2,old L2 |
| 0x02 | HitagPro,new L6 |
| 0x03 | TI DST80 |
| 0x04 | TI CRAID |
| 0xFF | UNKNOWN |

<a id="table-tab-kalibrierung-windschild"></a>
### TAB_KALIBRIERUNG_WINDSCHILD

Dimensions: 8 rows × 3 columns

| STATUS_ID | STATUS_NUMMER | STATUS_TEXT |
| --- | --- | --- |
| 0xFD | 1 | Calibrating Bottom position |
| 0xFE | 2 | Calibrating Top position |
| 0x00 | 3 | Calibration performed with success |
| 0xFF | 4 | Calibration error |
| 0x07 | 5 | Calibration cannot be performed |
| 0x01 | 6 | Calibration started |
| 0x02 | 7 | Calibration already performed |
| 0x03 | 8 | Calibration not performed |

<a id="table-steuern-windshield-arg"></a>
### STEUERN_WINDSHIELD_ARG

Dimensions: 9 rows × 2 columns

| WINDSHIELD_TEXT | WINDSHIELD_WERT |
| --- | --- |
| auf | 0x01 |
| ab | 0x02 |
| stopp | 0x00 |
| up | 0x01 |
| down | 0x02 |
| stop | 0x00 |
| 1 | 0x01 |
| 2 | 0x02 |
| 0 | 0x00 |

<a id="table-pwm"></a>
### PWM

Dimensions: 6 rows × 2 columns

| PWM | PWM_TEXT |
| --- | --- |
| 0x01 | TAIL_LIGHTS |
| 0x02 | POSITION_LIGHTS |
| 0x03 | BRAKE_LIGHTS |
| 0x04 | HEATED_GRIPS |
| 0x05 | HSEAT_RIDER |
| 0x06 | HSEAT_PILLOW |

<a id="table-lcd-option"></a>
### LCD_OPTION

Dimensions: 2 rows × 2 columns

| LCD_OPT_NUMBER | LCD_OPTION |
| --- | --- |
| 0x01 | lcd_positive |
| 0x02 | lcd_negative |
