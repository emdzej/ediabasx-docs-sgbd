# ulf2_hi.prg

- Jobs: [87](#jobs)
- Tables: [26](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ULF2_HI |
| ORIGIN | BMW EI-43 Peter Schramm |
| REVISION | 5.005 |
| AUTHOR | Temic EDSB Aufrecht |
| COMMENT | N/A |
| PACKAGE | 1.47 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [DIAGNOSEPROTOKOLL_LESEN](#job-diagnoseprotokoll-lesen) - Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück
- [DIAGNOSEPROTOKOLL_SETZEN](#job-diagnoseprotokoll-setzen) - Wählt ein Diagnoseprotokoll aus
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [MOST_VERSION_LESEN](#job-most-version-lesen) - Auslesen von Most Version KWP2000: $21 ReadDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $A0 MOSTVersion MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_MOST_3DB](#job-status-most-3db) - Auslesen des Status der Lichtleistungsabsenkung KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STEUERN_MOST_3DB](#job-steuern-most-3db) - Lichtleistungsabsenkung einschalten KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch $00 S1 geoeffnet = 3dB Absenkung MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_WAKE_UP_STATUS](#job-status-wake-up-status) - Auslesen des Status WakeupStatus KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_ABILITY_TO_WAKE](#job-status-ability-to-wake) - Auslesen des Status AbilityToWake KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STEUERN_ABILITY_TO_WAKE](#job-steuern-ability-to-wake) - AbilityToWake einstellen KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD AbilityToWake $00 of, $01 on, $02 critical MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
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
- [DIAGNOSTIC_MODE_ECUVM](#job-diagnostic-mode-ecuvm) - KWP2000: $10 StartDiagnosticsSession $88 ECUVariantCodingMode
- [BATTERY_VOLTAGE](#job-battery-voltage) - KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $06 Get Battery Voltage
- [BT_GERAETESUCHE](#job-bt-geraetesuche) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $04 BluetoothInquiry
- [BT_GERAETESUCHE_ERG_LESEN](#job-bt-geraetesuche-erg-lesen) - KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $03 Get Device List
- [BT_GERAETEADRESSE_LESEN](#job-bt-geraeteadresse-lesen) - KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $07 Get BT device address
- [BT_GERAETEADRESSE_SCHREIBEN](#job-bt-geraeteadresse-schreiben) - KWP2000: $31 StartRoutineByLocalIdentifier $FC RecordLocalIdentifier $07 Set BT Device Address
- [STATUS_BT](#job-status-bt) - KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $11 Get Bluetooth On / Off Status
- [BT_EIN](#job-bt-ein) - KWP2000: $3B WriteDataByLocalIdentifier $FC RecordLocalIdentifier $0D $01 ON
- [BT_AUS](#job-bt-aus) - KWP2000: $3B WriteDataByLocalIdentifier $FC RecordLocalIdentifier $0D $00 Off
- [BT_ANTENNENTEST](#job-bt-antennentest) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $07 Get Bluetooth Antenna Test Result
- [BT_PASSKEY_LESEN](#job-bt-passkey-lesen) - KWP2000: $21 readDataByLocalIdentifier $FB RecordLocalIdentifier $06 Get Current BT Passkey
- [BT_PASSKEY_SCHREIBEN](#job-bt-passkey-schreiben) - KWP2000: $3B WriteDataByLocalIdentifier $FC RecordLocalIdentifier $02 Set BT Passkey
- [BT_ERKENNUNGSMODUS](#job-bt-erkennungsmodus) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $06 Bluetooth Discoverable Mode
- [STATUS_BT_ERKENNUNGSMODUS](#job-status-bt-erkennungsmodus) - KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $12 Get Bluetooth Discoverablemode Status
- [BT_GEKOPPELT_LESEN](#job-bt-gekoppelt-lesen) - KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $04 Get Paired Device List
- [BT_VERBINDUNGSTEST](#job-bt-verbindungstest) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $08 Start BT Link Quality Test
- [BT_VERBINDUNGSTEST_ERG_LESEN](#job-bt-verbindungstest-erg-lesen) - KWP2000: $21 readDataByLocalIdentifier $FB RecordLocalIdentifier $0B Get Bluetooth Link Quality Test Result
- [STATUS_IO_LESEN](#job-status-io-lesen) - KWP2000: $21 readDataByLocalIdentifier $FB RecordLocalIdentifier $02 Get IO Status
- [RESET_AUSLIEFERSTAND](#job-reset-auslieferstand) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $03 Reset to basic state
- [NUMMER_WAEHLEN](#job-nummer-waehlen) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $11 Dial Number
- [MICRO_TEST](#job-micro-test) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $0A Start MicroTest
- [MICRO_TEST_OHNE_12_VOLT](#job-micro-test-ohne-12-volt) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $0B Start MicroTest without voltage check
- [TELEFONBUCH_DOWNLOAD_STOP](#job-telefonbuch-download-stop) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $12 Stop phonebook download
- [EIGENDIAGNOSE](#job-eigendiagnose) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $20 Start Selftest
- [BT_GERAETENAME_LESEN](#job-bt-geraetename-lesen) - KWP2000: $21 readDataByLocalIdentifier $FB RecordLocalIdentifier $08 Get BT User Friendly Name
- [BT_READ_PHONE_ID](#job-bt-read-phone-id) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $21 ReadDataByLocalIdentifier $FB SUBFNID_21H_READ_ULF_PARAM_REO $15 GetAllPiInfo Modus  : Default
- [DELETE_ALL_PHONE_ID](#job-delete-all-phone-id) - Infospeicher loeschen KWP2000: $3B WriteDataByLocalIdentifier $FC SUBFNID_3BH_WRITE_ULF $15 ClearAllPiInfo Modus  : Default
- [STEUERN_USB_TEST](#job-steuern-usb-test) - KWP2000: $31 StartRoutineByLocalIdentifier $A0 RecordLocalIdentifier $0C Test
- [STATUS_USB_TEST](#job-status-usb-test) - KWP2000: $31 StartRoutineByLocalIdentifier $A0 RecordLocalIdentifier $0C Test
- [READ_USB_IDENT](#job-read-usb-ident) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $30 Test
- [USB_STACK_INFO_FOR_DEVICE](#job-usb-stack-info-for-device) - KWP2000: $21 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $25 Read USB-Info
- [USB_HUB_TEST](#job-usb-hub-test) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $31 Start USB HUB Test
- [RESET_API_DATENBANK](#job-reset-api-datenbank) - KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $13 Reset API Database

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

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table IOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen-detail"></a>
### IS_LESEN_DETAIL

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Infocode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table IOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
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

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

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

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x0E) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x05) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-most-version-lesen"></a>
### MOST_VERSION_LESEN

Auslesen von Most Version KWP2000: $21 ReadDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $A0 MOSTVersion MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| TRANSCEIVER_VERSION | string | Version des MOST Transceivers |
| NETSERVICES_VERSION | string | Version der Oasis NetServices |
| NETSERVICES_REVISION | string | Revision der Oasis NetServices |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-most-3db"></a>
### STATUS_MOST_3DB

Auslesen des Status der Lichtleistungsabsenkung KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOST_3DB | int | Status der Lichtleistungsabsenkung 0 = Lichtleistung abgesenkt 1 = Volle Lichtleistung 5s nach Absenkung wird die volle Lichtleistung wieder aktiv |
| STAT_MOST_3DB_TEXT | string | Status der Lichtleistungsabsenkung als Text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-3db"></a>
### STEUERN_MOST_3DB

Lichtleistungsabsenkung einschalten KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch $00 S1 geoeffnet = 3dB Absenkung MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT Nach 5s wieder volle Lichtleistung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wake-up-status"></a>
### STATUS_WAKE_UP_STATUS

Auslesen des Status WakeupStatus KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WAKE_UP_STATUS | int | Status ob Device geweckt hat oder geweckt wurde 0 = nicht initialisiert 1 = SG hat geweckt 2 = SG wurde geweckt |
| STAT_WAKE_UP_STATUS_TEXT | string | Status ob Device geweckt hat oder geweckt wurde als Text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ability-to-wake"></a>
### STATUS_ABILITY_TO_WAKE

Auslesen des Status AbilityToWake KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ABILITY_TO_WAKE | int | Status ob Device wecken darf 0 = off 1 = on 2 = critical |
| STAT_ABILITY_TO_WAKE_TEXT | string | Status ob Device wecken darf als Text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ability-to-wake"></a>
### STEUERN_ABILITY_TO_WAKE

AbilityToWake einstellen KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD AbilityToWake $00 of, $01 on, $02 critical MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter AbilityToWake Modus table  AbilityToWake Status Defaultwert: DEFAULT 00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

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

<a id="job-diagnostic-mode-ecuvm"></a>
### DIAGNOSTIC_MODE_ECUVM

KWP2000: $10 StartDiagnosticsSession $88 ECUVariantCodingMode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-battery-voltage"></a>
### BATTERY_VOLTAGE

KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $06 Get Battery Voltage

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| BATTERY_VOLTAGE | string | Batterie Voltage |
| BATTERY_VOLTAGE_UNIT | string | Batterie Voltage Unit |

<a id="job-bt-geraetesuche"></a>
### BT_GERAETESUCHE

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $04 BluetoothInquiry

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-bt-geraetesuche-erg-lesen"></a>
### BT_GERAETESUCHE_ERG_LESEN

KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $03 Get Device List

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| BT_GERAETESUCHE_ERG | string | Ergebnis der Geraetesuche |
| DEVICE_1 | string | Ergebnis des Dev1 |
| DEVICE_2 | string | Ergebnis des Dev2 |
| DEVICE_3 | string | Ergebnis des Dev3 |
| DEVICE_4 | string | Ergebnis des Dev4 |
| DEVICE_5 | string | Ergebnis des Dev5 |

<a id="job-bt-geraeteadresse-lesen"></a>
### BT_GERAETEADRESSE_LESEN

KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $07 Get BT device address

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| BT_ADRESSE | string | Hex-respone from ECU |

<a id="job-bt-geraeteadresse-schreiben"></a>
### BT_GERAETEADRESSE_SCHREIBEN

KWP2000: $31 StartRoutineByLocalIdentifier $FC RecordLocalIdentifier $07 Set BT Device Address

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1TO6 | string | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-bt"></a>
### STATUS_BT

KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $11 Get Bluetooth On / Off Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_BT_ON | unsigned char | Status whether BT is on or off |
| STAT_COMMENT | string | Hex-request to ECU |

<a id="job-bt-ein"></a>
### BT_EIN

KWP2000: $3B WriteDataByLocalIdentifier $FC RecordLocalIdentifier $0D $01 ON

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-bt-aus"></a>
### BT_AUS

KWP2000: $3B WriteDataByLocalIdentifier $FC RecordLocalIdentifier $0D $00 Off

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-bt-antennentest"></a>
### BT_ANTENNENTEST

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $07 Get Bluetooth Antenna Test Result

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_COMMENT | string | ausgelesene Daten |
| STAT_BT_ANTENNA_STATUS | unsigned char | ausgelesene Daten |

<a id="job-bt-passkey-lesen"></a>
### BT_PASSKEY_LESEN

KWP2000: $21 readDataByLocalIdentifier $FB RecordLocalIdentifier $06 Get Current BT Passkey

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| BT_PASSKEY | string | ausgelesene Daten |

<a id="job-bt-passkey-schreiben"></a>
### BT_PASSKEY_SCHREIBEN

KWP2000: $3B WriteDataByLocalIdentifier $FC RecordLocalIdentifier $02 Set BT Passkey

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1TO8 | string | Bereich: 0-255 bzw. 0x00-0xFF Eingabe z.B. 1234 Eingabe darf nicht länger seine als 8 Ziffer Es sind nur Ziffern als Eingabe erlaubt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-bt-erkennungsmodus"></a>
### BT_ERKENNUNGSMODUS

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $06 Bluetooth Discoverable Mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_BT_ERKENNUNGSMODUS | unsigned char | Blutooth Discoverablemode on or off |
| STAT_COMMENT | string | Kommentar |

<a id="job-status-bt-erkennungsmodus"></a>
### STATUS_BT_ERKENNUNGSMODUS

KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $12 Get Bluetooth Discoverablemode Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_BT_ERKENNUNGSMODUS | unsigned char | Discoverable mode on or off |
| STAT_COMMENT | string | JobResult STATUS_TEXT |

<a id="job-bt-gekoppelt-lesen"></a>
### BT_GEKOPPELT_LESEN

KWP2000: $21 ReadDataByLocalIdentifier $FB RecordLocalIdentifier $04 Get Paired Device List

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| DEVICE_1 | string | Ergebnis Dev1 |
| DEVICE_2 | string | Ergebnis Dev2 |
| DEVICE_3 | string | Ergebnis Dev3 |
| DEVICE_4 | string | Ergebnis Dev4 |

<a id="job-bt-verbindungstest"></a>
### BT_VERBINDUNGSTEST

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $08 Start BT Link Quality Test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| BLUETOOTH_MODE | string | OKAY, if without errors table JobResult STATUS_TEXT |
| BLUETOOTH_FAILURE | string | OKAY, if without errors table JobResult STATUS_TEXT |

<a id="job-bt-verbindungstest-erg-lesen"></a>
### BT_VERBINDUNGSTEST_ERG_LESEN

KWP2000: $21 readDataByLocalIdentifier $FB RecordLocalIdentifier $0B Get Bluetooth Link Quality Test Result

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LINK_QUALITY | unsigned char | OKAY, if without errors |
| STAT_LINK_QUALITY_VALUE | unsigned char | OKAY, if without errors |
| STAT_HVX_SCO_PACKETS | string | OKAY, if without errors |
| STAT_DMX_ACL_PACKETS | string | OKAY, if without errors |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

KWP2000: $21 readDataByLocalIdentifier $FB RecordLocalIdentifier $02 Get IO Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_CRADLE_KEY_INPUT | unsigned char | Hex-request to ECU |
| STAT_CRADLE_ENABLE_OUTPUT | unsigned char | Hex-request to ECU |
| STAT_TELEPHONE_ON_OUTPUT | unsigned char | Hex-request to ECU |
| STAT_COMMENT | string | Hex-request to ECU |

<a id="job-reset-auslieferstand"></a>
### RESET_AUSLIEFERSTAND

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $03 Reset to basic state

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_RESET | unsigned char | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_RESET_OKAY | string | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_BLUETOOTH_FAILURE | string | OKAY, if without errors table JobResult STATUS_TEXT |

<a id="job-nummer-waehlen"></a>
### NUMMER_WAEHLEN

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $11 Dial Number

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STRING_BUFFER | string | Als Argument wird ein vorgefuellter Stringbuffer uebergeben Der Stringbuffer enthält die Telefonnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-micro-test"></a>
### MICRO_TEST

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $0A Start MicroTest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_MIC_TEST | string | Ergebnis Test |
| STAT_MIC | string | Ergebnis Test Mikro |
| STAT_MIC_2 | string | Ergebnis Test Mikro_2 |
| STAT_COMMENT | string | Hex-request to ECU |
| STAT_MIC_DETAIL_1 | int | Ergebnis Test Mikro 1 - detailliert -1 - Keine Diagnose durchfuehrbar 0 - Alles OK 1 - Nicht angeschlossen 2 - Kurzschluss UBatt 3 - Kurzschluss Masse 4 - Keine eindeutige Diagnose möglich 5 - Keine Micro codiert |
| STAT_MIC_DETAIL_2 | int | Ergebnis Test Mikro 2 - detailliert -1 - Keine Diagnose durchfuehrbar 0 - Alles OK 1 - Nicht angeschlossen 2 - Kurzschluss UBatt 3 - Kurzschluss Masse 4 - Keine eindeutige Diagnose möglich 5 - Keine Micro codiert |

<a id="job-micro-test-ohne-12-volt"></a>
### MICRO_TEST_OHNE_12_VOLT

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $0B Start MicroTest without voltage check

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_MIC_TEST_LOW | string | Ergebnis Test |
| STAT_MIC | string | Ergebnis Test Mikro |
| STAT_MIC_2 | string | Ergebnis Test Mikro_2 |
| STAT_COMMENT | string | Hex-request to ECU |

<a id="job-telefonbuch-download-stop"></a>
### TELEFONBUCH_DOWNLOAD_STOP

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $12 Stop phonebook download

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TB_CODE | string | TB Download Code |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-eigendiagnose"></a>
### EIGENDIAGNOSE

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $20 Start Selftest

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_CODE | string | Test Code |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIAG_STATUS | string | Status der Eigendiagnose |
| STAT_COMMENT | string | Hex-request to ECU |

<a id="job-bt-geraetename-lesen"></a>
### BT_GERAETENAME_LESEN

KWP2000: $21 readDataByLocalIdentifier $FB RecordLocalIdentifier $08 Get BT User Friendly Name

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| BT_UFN | string | ausgelesene Daten |

<a id="job-bt-read-phone-id"></a>
### BT_READ_PHONE_ID

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $21 ReadDataByLocalIdentifier $FB SUBFNID_21H_READ_ULF_PARAM_REO $15 GetAllPiInfo Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PHONE_ID1 | string | Phone ID 1 |
| P1_KM_READING_AT_LAST_RECONNECT | long | Phone1 KM reading at last reconnect |
| P1_NO_OF_RECONNECTS | int | Phone1 no of reconnects |
| P1_PHONE_MODEL_RAWDATA_TRUNC | string | Phone1 phone model raw data |
| P1_PHONE_MODEL | string | Phone1 phone model understandable format |
| P1_PHONE_SOFTWARE_RAWDATA_TRUNC | string | Phone1 phone software raw data |
| P1_PHONE_SOFTWARE | string | Phone1 phone software understandable format |
| P1_KNOWN_PHONE_MODEL | int | Phone1 phone model readyness flag |
| P1_KNOWN_PHONE_SOFTWARE | int | Phone1 phone software readyness flag |
| PHONE_ID2 | string | Phone ID 2 |
| P2_KM_READING_AT_LAST_RECONNECT | long | Phone2 KM reading at last reconnect |
| P2_NO_OF_RECONNECTS | int | Phone2 no of reconnects |
| P2_PHONE_MODEL_RAWDATA_TRUNC | string | Phone2 phone model raw data |
| P2_PHONE_MODEL | string | Phone2 phone model understandable format |
| P2_PHONE_SOFTWARE_RAWDATA_TRUNC | string | Phone2 phone software raw data |
| P2_PHONE_SOFTWARE | string | Phone2 phone software understandable format |
| P2_KNOWN_PHONE_MODEL | int | Phone2 phone model readyness flag |
| P2_KNOWN_PHONE_SOFTWARE | int | Phone2 phone software readyness flag |
| PHONE_ID3 | string | Phone ID 3 |
| P3_KM_READING_AT_LAST_RECONNECT | long | Phone3 KM reading at last reconnect |
| P3_NO_OF_RECONNECTS | int | Phone3 no of reconnects |
| P3_PHONE_MODEL_RAWDATA_TRUNC | string | Phone3 phone model raw data |
| P3_PHONE_MODEL | string | Phone3 phone model understandable format |
| P3_PHONE_SOFTWARE_RAWDATA_TRUNC | string | Phone3 phone software raw data |
| P3_PHONE_SOFTWARE | string | Phone3 phone software understandable format |
| P3_KNOWN_PHONE_MODEL | int | Phone3 phone model readyness flag |
| P3_KNOWN_PHONE_SOFTWARE | int | Phone3 phone software readyness flag |
| PHONE_ID4 | string | Phone ID 4 |
| P4_KM_READING_AT_LAST_RECONNECT | long | Phone4 KM reading at last reconnect |
| P4_NO_OF_RECONNECTS | int | Phone4 no of reconnects |
| P4_PHONE_MODEL_RAWDATA_TRUNC | string | Phone4 phone model raw data |
| P4_PHONE_MODEL | string | Phone4 phone model understandable format |
| P4_PHONE_SOFTWARE_RAWDATA_TRUNC | string | Phone4 phone software raw data |
| P4_PHONE_SOFTWARE | string | Phone4 phone software understandable format |
| P4_KNOWN_PHONE_MODEL | int | Phone4 phone model readyness flag |
| P4_KNOWN_PHONE_SOFTWARE | int | Phone4 phone software readyness flag |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-delete-all-phone-id"></a>
### DELETE_ALL_PHONE_ID

Infospeicher loeschen KWP2000: $3B WriteDataByLocalIdentifier $FC SUBFNID_3BH_WRITE_ULF $15 ClearAllPiInfo Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY NO ERRORS FOUND, wenn fehlerfrei ERROR_DELETE_ALL_PHONE_ID,in case of error table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-usb-test"></a>
### STEUERN_USB_TEST

KWP2000: $31 StartRoutineByLocalIdentifier $A0 RecordLocalIdentifier $0C Test

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_VENDORID | string | Parameter VendorID (2Byte) |
| ARG_PRODUCTID | string | Parameter ProductID (2Byte) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |

<a id="job-status-usb-test"></a>
### STATUS_USB_TEST

KWP2000: $31 StartRoutineByLocalIdentifier $A0 RecordLocalIdentifier $0C Test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_USB_TEST | int | USB Status |
| STAT_USB_TEST_TEXT | string | Klartext des USB Status |
| STAT_VENDORID_REC | string | Erkannte Vendor ID des device |
| STAT_PRODUCTID_REC | string | Erkannte Product ID des device |
| STAT_VENDORID_INT | string | Als Parameter übergebene Vendor ID |
| STAT_PRODUCTID_INT | string | Als Parameter übergebene Product ID |
| STAT_PARTITION_REC | string | Erkannte partition des device |
| STAT_SERIAL_REC | string | Erkannte serial string des device |
| STAT_PORT_INFO | string | Gelesene Port Information |
| STAT_PORT_INFO_STRING | string | Port Information als Klartext |

<a id="job-read-usb-ident"></a>
### READ_USB_IDENT

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $30 Test

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_VENDORID | string | Zu erwartende VendorID (2Byte) |
| ARG_PRODUCTID | string | Zu erwartende ProductID (2Byte) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_VENDORID_INT | string | Gelesene Vendor ID |
| STAT_PRODUCTID_INT | string | Gelesene Product ID |
| STAT_VENDOR_STRING_INT | string | Gelesener Vendor String |
| STAT_SNR_STRING_INT | string | Gelesener Seriennummer String |
| STAT_USB_IDENT_RESULT | string | Gelesener Seriennummer String |
| STAT_PORT_INFO | string | Gelesene Port Information |
| STAT_PORT_INFO_STRING | string | Port Information als Klartext |

<a id="job-usb-stack-info-for-device"></a>
### USB_STACK_INFO_FOR_DEVICE

KWP2000: $21 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $25 Read USB-Info

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-response from ECU |
| USB1_STAT_VENDORID | string | Vendor ID von USB Stick 1 |
| USB1_STAT_PRODUCTID | string | Product ID von USB Stick 1 |
| USB1_STAT_CLASSID | string | Vendor ID von USB Stick 1 |
| USB1_STAT_SUBCLASSID | string | Product ID von USB Stick 1 |
| USB1_STAT_PORT_INFO | string | Port Info von USB Stick 1 |
| USB1_STAT_PORT_INFO_STRING | string | Port Info String von USB Stick 1 |
| USB1_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von USB Stick 1 |
| USB1_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von USB Stick 1 |
| USB1_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von USB Stick 1 |
| USB1_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von USB Stick 1 |
| USB1_STAT_CONNECTIONS | string | Anzahl der Connections von USB Stick 1 |
| USB1_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von USB Stick 1 |
| USB2_STAT_VENDORID | string | Vendor ID von USB Stick 2 |
| USB2_STAT_PRODUCTID | string | Product ID von USB Stick 2 |
| USB2_STAT_CLASSID | string | Vendor ID von USB Stick 2 |
| USB2_STAT_SUBCLASSID | string | Product ID von USB Stick 2 |
| USB2_STAT_PORT_INFO | string | Port Info von USB Stick 2 |
| USB2_STAT_PORT_INFO_STRING | string | Port Info String von USB Stick 2 |
| USB2_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von USB Stick 2 |
| USB2_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von USB Stick 2 |
| USB2_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von USB Stick 2 |
| USB2_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von USB Stick 2 |
| USB2_STAT_CONNECTIONS | string | Anzahl der Connections von USB Stick 2 |
| USB2_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von USB Stick 2 |
| USB3_STAT_VENDORID | string | Vendor ID von USB Stick 3 |
| USB3_STAT_PRODUCTID | string | Product ID von USB Stick 3 |
| USB3_STAT_CLASSID | string | Vendor ID von USB Stick 3 |
| USB3_STAT_SUBCLASSID | string | Product ID von USB Stick 3 |
| USB3_STAT_PORT_INFO | string | Port Info von USB Stick 3 |
| USB3_STAT_PORT_INFO_STRING | string | Port Info String von USB Stick 3 |
| USB3_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von USB Stick 3 |
| USB3_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von USB Stick 3 |
| USB3_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von USB Stick 3 |
| USB3_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von USB Stick 3 |
| USB3_STAT_CONNECTIONS | string | Anzahl der Connections von USB Stick 3 |
| USB3_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von USB Stick 3 |
| USB4_STAT_VENDORID | string | Vendor ID von USB Stick 4 |
| USB4_STAT_PRODUCTID | string | Product ID von USB Stick 4 |
| USB4_STAT_CLASSID | string | Vendor ID von USB Stick 4 |
| USB4_STAT_SUBCLASSID | string | Product ID von USB Stick 4 |
| USB4_STAT_PORT_INFO | string | Port Info von USB Stick 4 |
| USB4_STAT_PORT_INFO_STRING | string | Port Info String von USB Stick 4 |
| USB4_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von USB Stick 4 |
| USB4_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von USB Stick 4 |
| USB4_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von USB Stick 4 |
| USB4_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von USB Stick 4 |
| USB4_STAT_CONNECTIONS | string | Anzahl der Connections von USB Stick 4 |
| USB4_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von USB Stick 4 |
| IPOD1_STAT_SWVERSION | string | SW Version von Ipod 1 |
| IPOD1_STAT_TYPE | string | Type von Ipod 1 |
| IPOD1_STAT_PORT_INFO | string | Port Info von Ipod 1 |
| IPOD1_STAT_PORT_INFO_STRING | string | Port Info String von Ipod 1 |
| IPOD1_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Ipod 1 |
| IPOD1_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Ipod 1 |
| IPOD1_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Ipod 1 |
| IPOD1_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Ipod 1 |
| IPOD1_STAT_CONNECTIONS | string | Anzahl der Connections von Ipod 1 |
| IPOD1_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Ipod 1 |
| IPOD2_STAT_SWVERSION | string | SW Version von Ipod 2 |
| IPOD2_STAT_TYPE | string | Type von Ipod 2 |
| IPOD2_STAT_PORT_INFO | string | Port Info von Ipod 2 |
| IPOD2_STAT_PORT_INFO_STRING | string | Port Info String von Ipod 2 |
| IPOD2_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Ipod 2 |
| IPOD2_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Ipod 2 |
| IPOD2_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Ipod 2 |
| IPOD2_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Ipod 2 |
| IPOD2_STAT_CONNECTIONS | string | Anzahl der Connections von Ipod 2 |
| IPOD2_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Ipod 2 |
| IPOD3_STAT_SWVERSION | string | SW Version von Ipod 3 |
| IPOD3_STAT_TYPE | string | Typ von Ipod 3 |
| IPOD3_STAT_PORT_INFO | string | Port Info von Ipod 3 |
| IPOD3_STAT_PORT_INFO_STRING | string | Port Info String von Ipod 3 |
| IPOD3_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Ipod 3 |
| IPOD3_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Ipod 3 |
| IPOD3_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Ipod 3 |
| IPOD3_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Ipod 3 |
| IPOD3_STAT_CONNECTIONS | string | Anzahl der Connections von Ipod 3 |
| IPOD3_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Ipod 3 |
| IPOD4_STAT_SWVERSION | string | SW Version von Ipod 4 |
| IPOD4_STAT_TYPE | string | Typ von Ipod 4 |
| IPOD4_STAT_PORT_INFO | string | Port Info von Ipod 4 |
| IPOD4_STAT_PORT_INFO_STRING | string | Port Info String von Ipod 4 |
| IPOD4_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Ipod 4 |
| IPOD4_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Ipod 4 |
| IPOD4_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Ipod 4 |
| IPOD4_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Ipod 4 |
| IPOD4_STAT_CONNECTIONS | string | Anzahl der Connections von Ipod 4 |
| IPOD4_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Ipod 4 |
| MTP1_STAT_VENDORID | string | Vendor ID von Mtp 1 |
| MTP1_STAT_PRODUCTID | string | Product ID von Mtp 1 |
| MTP1_STAT_CLASSID | string | Vendor ID von Mtp 1 |
| MTP1_STAT_SUBCLASSID | string | Product ID von Mtp 1 |
| MTP1_STAT_PORT_INFO | string | Port Info von Mtp 1 |
| MTP1_STAT_PORT_INFO_STRING | string | Port Info String von Mtp 1 |
| MTP1_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Mtp 1 |
| MTP1_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Mtp 1 |
| MTP1_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Mtp 1 |
| MTP1_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Mtp 1 |
| MTP1_STAT_CONNECTIONS | string | Anzahl der Connections von Mtp 1 |
| MTP1_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Mtp 1 |
| MTP2_STAT_VENDORID | string | Vendor ID von Mtp 2 |
| MTP2_STAT_PRODUCTID | string | Product ID von Mtp 2 |
| MTP2_STAT_CLASSID | string | Vendor ID von Mtp 2 |
| MTP2_STAT_SUBCLASSID | string | Product ID von Mtp 2 |
| MTP2_STAT_PORT_INFO | string | Port Info von Mtp 2 |
| MTP2_STAT_PORT_INFO_STRING | string | Port Info String von Mtp 2 |
| MTP2_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Mtp 2 |
| MTP2_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Mtp 2 |
| MTP2_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Mtp 2 |
| MTP2_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Mtp 2 |
| MTP2_STAT_CONNECTIONS | string | Anzahl der Connections von Mtp 2 |
| MTP2_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Mtp 2 |
| MTP3_STAT_VENDORID | string | Vendor ID von Mtp 3 |
| MTP3_STAT_PRODUCTID | string | Product ID von Mtp 3 |
| MTP3_STAT_CLASSID | string | Vendor ID von Mtp 3 |
| MTP3_STAT_SUBCLASSID | string | Product ID von Mtp 3 |
| MTP3_STAT_PORT_INFO_STRING | string | Port Info String von Mtp 3 |
| MTP3_STAT_PORT_INFO | string | Port Info von Mtp 3 |
| MTP3_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Mtp 3 |
| MTP3_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Mtp 3 |
| MTP3_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Mtp 3 |
| MTP3_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Mtp 3 |
| MTP3_STAT_CONNECTIONS | string | Anzahl der Connections von Mtp 3 |
| MTP3_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Mtp 3 |
| MTP4_STAT_VENDORID | string | Vendor ID von Mtp 4 |
| MTP4_STAT_PRODUCTID | string | Product ID von Mtp 4 |
| MTP4_STAT_CLASSID | string | Vendor ID von Mtp 4 |
| MTP4_STAT_SUBCLASSID | string | Product ID von Mtp 4 |
| MTP4_STAT_PORT_INFO | string | Port Info von Mtp 4 |
| MTP4_STAT_PORT_INFO_STRING | string | Port Info String von Mtp 4 |
| MTP4_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Mtp 4 |
| MTP4_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Mtp 4 |
| MTP4_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Mtp 4 |
| MTP4_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Mtp 4 |
| MTP4_STAT_CONNECTIONS | string | Anzahl der Connections von Mtp 4 |
| MTP4_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Mtp 4 |
| UNKNOWN1_STAT_VENDORID | string | Vendor ID von Unknown device 1 |
| UNKNOWN1_STAT_PRODUCTID | string | Product ID von Unknown device 1 |
| UNKNOWN1_STAT_CLASSID | string | Vendor ID von Unknown device 1 |
| UNKNOWN1_STAT_SUBCLASSID | string | Product ID von Unknown device 1 |
| UNKNOWN1_STAT_PORT_INFO | string | Port Info von Unknown device 1 |
| UNKNOWN1_STAT_PORT_INFO_STRING | string | Port Info String von Unknown device 1 |
| UNKNOWN1_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Unknown device 1 |
| UNKNOWN1_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Unknown device 1 |
| UNKNOWN1_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Unknown device 1 |
| UNKNOWN1_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Unknown device 1 |
| UNKNOWN1_STAT_CONNECTIONS | string | Anzahl der Connections von Unknown device 1 |
| UNKNOWN1_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Unknown device 1 |
| UNKNOWN2_STAT_VENDORID | string | Vendor ID von Unknown device 2 |
| UNKNOWN2_STAT_PRODUCTID | string | Product ID von Unknown device 2 |
| UNKNOWN2_STAT_CLASSID | string | Vendor ID von Unknown device 2 |
| UNKNOWN2_STAT_SUBCLASSID | string | Product ID von Unknown device 2 |
| UNKNOWN2_STAT_PORT_INFO | string | Port Info von Unknown device 2 |
| UNKNOWN2_STAT_PORT_INFO_STRING | string | Port Info String von Unknown device 2 |
| UNKNOWN2_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Unknown device 2 |
| UNKNOWN2_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Unknown device 2 |
| UNKNOWN2_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Unknown device 2 |
| UNKNOWN2_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Unknown device 2 |
| UNKNOWN2_STAT_CONNECTIONS | string | Anzahl der Connections von Unknown device 2 |
| UNKNOWN2_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Unknown device 2 |
| UNKNOWN3_STAT_VENDORID | string | Vendor ID von Unknown device 3 |
| UNKNOWN3_STAT_PRODUCTID | string | Product ID von Unknown device 3 |
| UNKNOWN3_STAT_CLASSID | string | Vendor ID von Unknown device 3 |
| UNKNOWN3_STAT_SUBCLASSID | string | Product ID von Unknown device 3 |
| UNKNOWN3_STAT_PORT_INFO | string | Port Info von Unknown device 3 |
| UNKNOWN3_STAT_PORT_INFO_STRING | string | Port Info String von Unknown device 3 |
| UNKNOWN3_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Unknown device 3 |
| UNKNOWN3_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Unknown device 3 |
| UNKNOWN3_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Unknown device 3 |
| UNKNOWN3_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Unknown device 3 |
| UNKNOWN3_STAT_CONNECTIONS | string | Anzahl der Connections von Unknown device 3 |
| UNKNOWN3_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Unknown device 3 |
| UNKNOWN4_STAT_VENDORID | string | Vendor ID von Unknown device 4 |
| UNKNOWN4_STAT_PRODUCTID | string | Product ID von Unknown device 4 |
| UNKNOWN4_STAT_CLASSID | string | Vendor ID von Unknown device 4 |
| UNKNOWN4_STAT_SUBCLASSID | string | Product ID von Unknown device 4 |
| UNKNOWN4_STAT_PORT_INFO | string | Port Info von Unknown device 4 |
| UNKNOWN4_STAT_PORT_INFO_STRING | string | Port Info String von Unknown device 4 |
| UNKNOWN4_STAT_KM_FIRST_CONNECT | string | km Stand beim ersten Connect von Unknown device 4 |
| UNKNOWN4_STAT_KM_FIRST_DISCONNECT | string | km Stand beim ersten Disconnect von Unknown device 4 |
| UNKNOWN4_STAT_KM_LAST_CONNECT | string | km Stand beim letzten Connect von Unknown device 4 |
| UNKNOWN4_STAT_KM_LAST_DISCONNECT | string | km Stand beim letzten Disconnect von Unknown device 4 |
| UNKNOWN4_STAT_CONNECTIONS | string | Anzahl der Connections von Unknown device 4 |
| UNKNOWN4_STAT_CONNECT_STATE | string | Aktueller Zustand der Connection von Unknown device 4 |
| STAT_USB_STACK_STATE | string | Aktuelle Belegung des USB Stacks |
| STAT_IPOD_STACK_STATE | string | Aktuelle Belegung des IPOD Stacks |
| STAT_MTP_STACK_STATE | string | Aktuelle Belegung des MTP Stacks |
| STAT_UNKNOWN_STACK_STATE | string | Aktuelle Belegung des UNKNOWN Stacks |

<a id="job-usb-hub-test"></a>
### USB_HUB_TEST

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $31 Start USB HUB Test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_COMMENT | string | ausgelesene Daten |
| STAT_HUB_TEST | unsigned char | ausgelesene Daten |

<a id="job-reset-api-datenbank"></a>
### RESET_API_DATENBANK

KWP2000: $31 StartRoutineByLocalIdentifier $FB RecordLocalIdentifier $13 Reset API Database

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_RESET | unsigned char | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_RESET_API_OKAY | string | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_RESET_API_FAILURE | string | OKAY, if without errors table JobResult STATUS_TEXT |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (115 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [ABILITY_TO_WAKE](#table-ability-to-wake) (4 × 2)
- [MOST_3DB](#table-most-3db) (3 × 2)
- [WAKE_UP_STATUS](#table-wake-up-status) (4 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (14 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (2 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (7 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (13 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (3 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (5 × 9)
- [REFERENCE_TABLE_PHONE_MODEL](#table-reference-table-phone-model) (71 × 4)
- [REFERENCE_TABLE_PHONE_SOFTWARE](#table-reference-table-phone-software) (91 × 5)

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

Dimensions: 115 rows × 2 columns

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

<a id="table-ability-to-wake"></a>
### ABILITY_TO_WAKE

Dimensions: 4 rows × 2 columns

| ABILITY_TO_WAKE_NR | ABILITY_TO_WAKE_MODE |
| --- | --- |
| 0x00 | off |
| 0x01 | on |
| 0x02 | critical |
| 0xXY | unbekannter Mode |

<a id="table-most-3db"></a>
### MOST_3DB

Dimensions: 3 rows × 2 columns

| MOST_3DB_NR | MOST_3DB_MODE |
| --- | --- |
| 0x00 | Lichtleistung abgesenkt |
| 0x01 | Volle Lichtleistung |
| 0xXY | unbekannter Mode |

<a id="table-wake-up-status"></a>
### WAKE_UP_STATUS

Dimensions: 4 rows × 2 columns

| WAKE_UP_STATUS_NR | WAKE_UP_STATUS_MODE |
| --- | --- |
| 0x00 | nicht initialisiert |
| 0x01 | SG hat geweckt |
| 0x02 | SG wurde geweckt |
| 0xXY | unbekannter Mode |

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
| 1 | BMW-FAST |
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA9A8 | Interner Speicherfehler (Error_Memory_Failure). |
| 0xA9A9 | Cradle Key blockiert (Error_Stuck_Cradle_Key). |
| 0xA9AA | Fehler beim initialisieren von Bluetooth (Error_Bluetooth_Failure). |
| 0xA9AB | Bluetooth-Antenne nicht angeschlossen oder defekt (Error_Bluetooth_Antenna_Fault). |
| 0xA9AC | Überspannung am Steuergerät gemessen ( Error_Battey_Voltage_Fault). |
| 0xA9AD | Übertemeratur am FOT aufgetretten (Error_FOT_Temperature_Fault). |
| 0xA9AE | Selbsttest während Startup fehlgeschlagen (Error_Failed_Power_On_Self_Test). |
| 0xA9AF | Prozessor defekt (Error_DSP_Failure). |
| 0xDE4D | MOST Bus konnte nicht geweckt werden (Error_Wakeup_Failed) |
| 0xDE4E | Obwohl Shutdown (Execute) geschickt wurde, ging das Licht nicht aus (Error_Light_Not_Off) |
| 0xDE50 | Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |
| 0xDE51 | Lange und/oder haeufige Unlocks (Error_Unlock_Long) |
| 0xDE52 | Ein Device hat sich wegen Uebertemperatur abgeschaltet (Error_Temp_Shutdown) |
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
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 2 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xDE50 | 0x06 | -- | -- | -- |
| default | -- | -- | -- | -- |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Logische-Knotenadresse | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x02 | FBlockID | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x03 | InstID | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x04 | FktID | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x05 | Diagnoseadresse | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x06 | NPR | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0xFF | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 13 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9301 | Phone_ID_1 |
| 0x9302 | Phone_ID_2 |
| 0x9303 | Phone_ID_3 |
| 0x9304 | Phone_ID_4 |
| 0x9308 | Device bekam Reset (Error_Reset). |
| 0x930A | Device ist im Zustand Normal Operation und das Licht am Eingang geht ohne Vorankuendigung aus (Error_Sudden_light_off). |
| 0x930B | Anfragendes Device bekommt keine Antwort obwohl Partner vorhanden ist (Error_Device_No_Answer). |
| 0x930C | Kurze Unlocks (Error_Unlock_Short). |
| 0x930D | Kein Broadcast Configuration(Status) vom Networkmaster erhalten (Error_t_CfgStatus). |
| 0x930F | Ein Device hat im laufenden Betrieb seinen Bypass All geschlossen (Error_NCE). |
| 0x9310 | Empfaenger hat eine Nachricht nicht abgenommen (Error_NAK). |
| 0x9311 | Device bekam Bluetooth Reset (Error_Bluetooth_Watchdog). |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 3 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x930B | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x9310 | 0x01 | 0x02 | 0x03 | 0x04 |
| default | -- | -- | -- | -- |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Zieladresse | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x02 | FBlockID | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x03 | InstID | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x04 | FktID | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-reference-table-phone-model"></a>
### REFERENCE_TABLE_PHONE_MODEL

Dimensions: 71 rows × 4 columns

| - | INPUT_COLUMN | OUTPUT_COLUMN | CODE_NUMBER |
| --- | --- | --- | --- |
| Variable | Phone_model_rawdata_trunc | Phone_model | - |
| Format of variable | String[47] | String[50] | - |
| 1.1 | AAB-1021011-BV | SonyEricsson T610 | 6 |
| 1.2 | AAB-1021012-BV | SonyEricsson T630 | 6 |
| 1.3 | AAB-1021041-BV | SonyEricsson K700i | 99 |
| 1.4 | AAB-1022011-BV | SonyEricsson K750i | 7 |
| 1.5 | AAD-3021021-BV | SonyEricsson K600i | 99 |
| 1.6 | AAB-1022013-BV | SonyEricsson W800i | 99 |
| 1.7 | AAB-1022012-BV | SonyEricsson D750i | 99 |
| 1.8 | AAF-1022011-BV | SonyEricsson K790i | 99 |
| 1.9 | AAD-3022031-BV | SonyEricsson K800i | 7 |
| 1.10 | AAD-3022041-BV | SonyEricsson K610i | 99 |
| 1.11 | AAF-1052051-BV | SonyEricsson W810i | 99 |
| 1.12 | AAB-1022014-BV | SonyEricsson W700i | 99 |
| 1.13 | AAD-3022021-BV | SonyEricsson W850i | 99 |
| 1.14 | FAD-3022012-BV | SonyEricsson M600 | 99 |
| 1.15 | AAD-3022061-BV | SonyEricsson K810 | 99 |
| 1.16 | AAC-1052022-BV | SonyEricsson W610i | 99 |
| 1.17 | AAC-1052021-BV | SonyEricsson K550i | 99 |
| 2.1 | GSM900","GSM1800","GSM1900","GSM850","MODEL=V3" | Motorala V3 | 99 |
| 2.2 | M900","GSM1800","GSM1900","GSM850","MODEL=V600" | Motorola V600 | 0 |
| 2.3 | M900","GSM1800","GSM1900","GSM850","MODEL=V620" | Motorola V620 | 99 |
| 2.4 | M900","GSM1800","GSM1900","GSM850","MODEL=V635" | Motorola V635 | 0 |
| 2.5 | 0","GSM1800","GSM1900","GSM850","MODEL=PEBL U6" | Motorola PEBL U6 | 99 |
| 2.6 | SM900","GSM1800","GSM1900","GSM850","MODEL=V3i" | Motorola V3i | 99 |
| 2.7 | GSM900","GSM1800","GSM1900","GSM850","MODEL=L7" | Motorola L7 | 99 |
| 2.8 | GSM900","GSM1800","GSM1900","GSM850","MODEL=K1" | Motorola K1 | 0 |
| 2.9 | "GSM900","GSM1800","GSM1900","WCDMA","MODEL=K3" | Motorola K3 | 99 |
| 2.10 | 00","GSM1800","GSM1900","WCDMA","MODEL=RAZRV6v" | Motorola RAZR V3xx | 99 |
| 3.1 | Nokia 6310i | Nokia 6310i | 6 |
| 3.2 | Nokia 6230 | Nokia 6230 | 99 |
| 3.3 | Nokia 6230i | Nokia 6230i | 7 |
| 3.4 | Nokia 6021 | Nokia 6021 | 99 |
| 3.5 | Nokia 6822 | Nokia 6822 | 99 |
| 3.6 | Nokia 6233 | Nokia 6233 | 7 |
| 3.7 | Nokia 6234 | Nokia 6234 | 99 |
| 3.8 | Nokia 6151 | Nokia 6151 | 99 |
| 3.9 | Nokia 6131 | Nokia 6131 | 99 |
| 3.10 | Nokia 5200 | Nokia 5200 | 99 |
| 3.11 | Nokia 5300 | Nokia 5300 | 99 |
| 3.12 | Nokia 6300 | Nokia 6300 | 7 |
| 3.13 | Nokia 6288 | Nokia 6288 | 99 |
| 3.14 | Nokia 6120 | Nokia 6120 | 99 |
| 3.15 | Nokia N73 | Nokia N73 | 99 |
| 4.1 | S55 | Siemens S55 | 2 |
| 4.2 | S65 | Siemens S65 | 2 |
| 4.3 | SP65 | Siemens SP65 | 99 |
| 4.4 | S75 | Siemens S75 | 2 |
| 4.5 | SK65 | Siemens SK65 | 99 |
| 4.6 | SL75 | Siemens SL75 | 99 |
| 5.1 | BlackBerry 8700 | BlackBerry 8700 | 99 |
| 5.2 | BlackBerry 8707 | BlackBerry 8707 | 99 |
| 5.3 | BlackBerry 7290 | BlackBerry 7290 | 99 |
| 5.4 | BlackBerry 7130 | BlackBerry 7130 | 99 |
| 5.5 | BlackBerry 8100 | BlackBerry 8100 | 99 |
| 5.6 | BlackBerry 8300 | BlackBerry 8300 | 99 |
| 5.7 | BlackBerry 8800 | BlackBerry 8800 | 99 |
| 6.1 | EF81 | BenQ EF81 | 99 |
| 6.2 | S68 | BenQ S68 | 99 |
| 6.3 | EL71 | BenQ EL71 | 99 |
| 6.4 | M81 | BenQ M81 | 99 |
| 6.5 | E71 | BenQ E71 | 99 |
| 7.1 | SAMSUNG SGH-E780 | Samsung SGH-E780 | 99 |
| 7.2 | SGH-X830 | Samsung SGH-X830 | 99 |
| 7.3 | SAMSUNG SGH-D900 | Samsung SGH-D900 | 99 |
| 7.4 | SAMSUNG SGH-E250 | Samsung SGH-E250 | 99 |
| 7.5 | SAMSUNG SGH-E830 | Samsung SGH-E830 | 99 |
| 7.6 | SAMSUNG SGH-E590 | Samsung SGH-E590 | 99 |
| 7.7 | SAMSUNG SGH-E740 | Samsung SGH-E740 | 99 |
| 7.8 | SGH-U600 | Samsung SGH-U600 | 99 |
| 8.1 | KG800 | LG Chocolate | 99 |

<a id="table-reference-table-phone-software"></a>
### REFERENCE_TABLE_PHONE_SOFTWARE

Dimensions: 91 rows × 5 columns

| INDEX | - | HELP_COLUMN | COMPARE_COLUMN | OUTPUT_COLUMN |
| --- | --- | --- | --- | --- |
| - | Variable | - | - | Phone_software |
| - | Description of Variable | - | - | Understandible phone software |
| - | Format of variable | - | - | String[50] |
| 01 | 1.1 | Motorola V600 | +CGMR: "TRIPLETS_G_0B.08.A2R_VA" | 0B.08.A2R_VA |
| 02 | 1.2 | Motorola V600 | +CGMR: "TRIPLETS_G_0B.09.1DR_A" | 0B.09.1DR_A |
| 03 | 1.3 | Motorola V600 | +CGMR: "TRIPLETS_G_0B.09.1FR_A" | 0B.09.1FR_A |
| 04 | 1.4 | Motorola V600 | +CGMR: "TRIPLETS_G_0B.09.37R" | 0B.09.37R |
| 05 | 1.5 | Motorola V600 | +CGMR: "TRIPLETS_G_0B.09.38R" | 0B.09.38R |
| 06 | 1.6 | Motorola V600 | +CGMR: "TRIPLETS_G_0B.09.56R" | 0B.09.56R |
| 07 | 1.7 | Motorola V600 | +CGMR: "TRIPLETS_G_0B.09.1FR_AV" | 0B.09.1FR_AV |
| 08 | 1.8 | Motorola V600 | +CGMR: "TRIPLETS_G_0B.09.4ER" | 0B.09.4ER |
| 09 | 1.9 | Motorola V600 | +CGMR: "TRIPLETS_G_0B.08.9FR" | 0B.08.9FR |
| 10 | - | - | END | - |
| 11 | 2.1 | Motorola V635 | +CGMR: "R474_G_08.48.24R_A" | 08.48.24R_A |
| 12 | 2.2 | Motorola V635 | +CGMR: "R474_G_08.48.6DR" | 08.48.6DR |
| 13 | 2.3 | Motorola V635 | +CGMR: "R474_G_08.48.6FR" | 08.48.6FR |
| 14 | - | - | END | - |
| 15 | 3.1 | Nokia 6310i | V 5.22 | 5.22 |
| 16 | 3.2 | Nokia 6310i | V 5.51 | 5.51 |
| 17 | 3.3 | Nokia 6310i | V 5.52 | 5.52 |
| 18 | 3.4 | Nokia 6310i | V 5.50 | 5.50 |
| 19 | 3.5 | Nokia 6310i | V 5.60 | 5.60 |
| 20 | 3.6 | Nokia 6310i | V 7.00 | 7.00 |
| 21 | - | - | END | - |
| 22 | 4.1 | Nokia 6230i | V 03.40 | 3.40 |
| 23 | 4.2 | Nokia 6230i | V 03.50 | 3.50 |
| 24 | 4.3 | Nokia 6230i | V 03.25 | 3.25 |
| 25 | 4.4 | Nokia 6230i | V 03.30 | 3.30 |
| 26 | 4.5 | Nokia 6230i | V 03.62 | 3.62 |
| 27 | 4.6 | Nokia 6230i | V 03.70 | 3.70 |
| 28 | 4.7 | Nokia 6230i | V 03.80 | 3.80 |
| 29 | 4.8 | Nokia 6230i | V 03.81 | 3.81 |
| 30 | 4.9 | Nokia 6230i | V 03.88 | 3.88 |
| 31 | - | - | END | - |
| 32 | 5.1 | Siemens S55 | 16 | 16 |
| 33 | 5.2 | Siemens S55 | 10 | 10 |
| 34 | 5.3 | Siemens S55 | 12 | 12 |
| 35 | 5.4 | Siemens S55 | 20 | 20 |
| 36 | 5.5 | Siemens S55 | 91 | 91 |
| 37 | - | - | END | - |
| 38 | 6.1 | Siemens S65 | 12 | 12 |
| 39 | 6.2 | Siemens S65 | 16 | 16 |
| 40 | 6.3 | Siemens S65 | 25 | 25 |
| 41 | 6.4 | Siemens S65 | 43 | 43 |
| 42 | 6.5 | Siemens S65 | 50 | 50 |
| 43 | - | - | END | - |
| 44 | 7.1 | SonyEricsson T610 | R4C003 | R4C003 |
| 45 | 7.2 | SonyEricsson T610 | R6C005 | R6C005 |
| 46 | 7.3 | SonyEricsson T610 | R1A081 | R1A081 |
| 47 | 7.4 | SonyEricsson T610 | R1L013 | R1L013 |
| 48 | - | - | END | - |
| 49 | 8.1 | SonyEricsson T630 | R4C003 | R4C003 |
| 50 | 8.2 | SonyEricsson T630 | R6C005 | R6C005 |
| 51 | 8.3 | SonyEricsson T630 | R4E002 | R4E002 |
| 52 | 8.4 | SonyEricsson T630 | R7A011 | R7A011 |
| 53 | - | - | END | - |
| 54 | 9.1 | SonyEricsson K750i | R1A040 | R1A040 |
| 55 | 9.2 | SonyEricsson K750i | R1J002 | R1J002 |
| 56 | 9.3 | SonyEricsson K750i | R1L002 | R1L002 |
| 57 | 9.4 | SonyEricsson K750i | R1N035 | R1N035 |
| 58 | 9.5 | SonyEricsson K750i | R1S005 | R1S005 |
| 59 | 9.6 | SonyEricsson K750i | R1AA008 | R1AA008 |
| 60 | 9.7 | SonyEricsson K750i | R1CA021 | R1CA021 |
| 61 | 9.8 | SonyEricsson K750i | R1BC002 | R1BC002 |
| 62 | 9.9 | SonyEricsson K750i | R1CA021 | R1CA021 |
| 63 | 9.10 | SonyEricsson K750i | R1DB001 | R1DB001 |
| 64 | - | - | END | - |
| 65 | 10.1 | Siemens S75 | 10 | 10 |
| 66 | 10.2 | Siemens S75 | 20 | 20 |
| 67 | 10.3 | Siemens S75 | 22 | 22 |
| 68 | 10.4 | Siemens S75 | 24 | 24 |
| 69 | 10.5 | Siemens S75 | 26 | 26 |
| 70 | 10.6 | Siemens S75 | 31 | 31 |
| 71 | 10.7 | Siemens S75 | 40 | 40 |
| 72 | - | - | END | - |
| 73 | 11.1 | Nokia 6233 | V 03.70 | 3.70 |
| 74 | 11.2 | Nokia 6233 | V 04.52 | 4.52 |
| 75 | 11.3 | Nokia 6233 | V 04.91 | 4.91 |
| 76 | 11.4 | Nokia 6233 | V 05.10 | 5.10 |
| 77 | - | - | END | - |
| 78 | 12.1 | SonyEricsson K800i | R1EA007 | R1EA007 |
| 79 | 12.2 | SonyEricsson K800i | R1ED001 | R1ED001 |
| 80 | 12.3 | SonyEricsson K800i | R1GB001 | R1GB001 |
| 81 | 12.4 | SonyEricsson K800i | R1JC002 | R1JC002 |
| 82 | 12.5 | SonyEricsson K800i | R1KG001 | R1KG001 |
| 83 | - | - | END | - |
| 84 | 13.1 | Motorola K1 | +CGMR: "R4527_G_08.22.07R" | R4527_G_08.22.07R |
| 85 | 13.2 | Motorola K1 | +CGMR: "R452F_G_08.03.08R" | R452F_G_08.03.08R |
| 86 | - | END | END | - |
| 87 | 14.1 | Nokia 6300 | V 04.70 | 4.70 |
| 88 | - | END | END | - |
