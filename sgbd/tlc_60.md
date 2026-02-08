# tlc_60.prg

- Jobs: [99](#jobs)
- Tables: [53](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Spurverlassenswarnsystem |
| ORIGIN | BMW EI-42 Ramboeck Josef |
| REVISION | 6.000 |
| AUTHOR | BMW EI-42 Ramboeck, BMW EI-42 Ender, SAGÖ PSEPROSRT4 Kloiber |
| COMMENT | N/A |
| PACKAGE | 1.36 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
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
- [_READ_UIF_DATA_TABLE](#job-read-uif-data-table) - reads the user info field KWP2000: $1A ReadECUIdentification .        $86 CurrentUIFDataTable
- [_READ_SYS_NAME](#job-read-sys-name) - reads the system name KWP2000: $1A ReadECUIdentification .        $97 SystemName
- [_READ_VMECUHWVNM](#job-read-vmecuhwvnm) - reads the VehicleManufacturerECUHWVersionNumber KWP2000: $1A ReadECUIdentification .        $9A HW Index
- [_READ_VM_DIAG_INDEX](#job-read-vm-diag-index) - read diagnostic index KWP2000: $1A ReadECUIdentification .        $9C VMDiagnosticIndex
- [_READ_DATE_ECU_MANUFACTURING](#job-read-date-ecu-manufacturing) - read date of ECU manufacturing KWP2000: $1A ReadECUIdentification .        $9D DateOfECUManufacturing
- [_READ_SYS_SUPP_INDEX](#job-read-sys-supp-index) - read system supplier index KWP2000: $1A ReadECUIdentification .        $9E SupplierIndex
- [_READ_VM_ECU_SWLAYER_VNR](#job-read-vm-ecu-swlayer-vnr) - read MCV-nr, SW-nr, SC-nr KWP2000: $1A ReadECUIdentification .        $9F VMECUSoftwareLayerVersionNumber
- [READ_DATE_LAST_CODING](#job-read-date-last-coding) - read date of the last coding KWP2000: $21 ReadDataByLocalIdentifier .        $08 date of the last coding
- [STATUS_KAMERA_VERSORGUNG](#job-status-kamera-versorgung) - reports the status of the camera supply KWP2000: $21 ReadDataByLocalIdentifier .        $22 status of camera supply
- [STATUS_FPN](#job-status-fpn) - reports status of the fixes pattern noise evaluation KWP2000: $21 ReadDataByLocalIdentifier .        $24 status of fixes pattern noise evaluation
- [STATUS_KAMERA_EEPROM](#job-status-kamera-eeprom) - reports communication status with the camera eeprom KWP2000: $21 ReadDataByLocalIdentifier .        $26 status of camera eeprom communication
- [STATUS_KAMERASERIENNUMMER](#job-status-kameraseriennummer) - reads camera serial number from eeprom KWP2000: $21 ReadDataByLocalIdentifier .        $28 camera serial number
- [STATUS_BORDNETZ_SPANNUNG](#job-status-bordnetz-spannung) - reports status of the voltage of the vehicle electrical system KWP2000: $21 ReadDataByLocalIdentifier .        $30 status of vehicle electrical system
- [STATUS_TEMPERATUR](#job-status-temperatur) - reports status of the ECU temperature KWP2000: $21 ReadDataByLocalIdentifier .        $31 status of ecu temperature
- [STATUS_WECKLEITUNG](#job-status-weckleitung) - reports status of wake line KWP2000: $21 ReadDataByLocalIdentifier .        $32 status of wake line
- [STATUS_ECU_SPANNUNGEN](#job-status-ecu-spannungen) - reports status of the voltages of the ECU power supply units KWP2000: $21 ReadDataByLocalIdentifier .        $33 status of power supply units
- [STATUS_PPC](#job-status-ppc) - reports status of the power PC KWP2000: $21 ReadDataByLocalIdentifier .        $34 status of power pc
- [STATUS_AKTUATOR](#job-status-aktuator) - reports status of the vibration actuators current consumption KWP2000: $21 ReadDataByLocalIdentifier .        $35 status of vibration actuator
- [STATUS_FETRAWE_MODE](#job-status-fetrawe-mode) - reports status of the FeTraWe-Mode KWP2000: $22 ReadDataByCommonIdentifier .        $10 read fetrawe mode .        $0A
- [_READ_EEPROM_BLOCK](#job-read-eeprom-block) - reports status of the FeTraWe-Mode KWP2000: $22 ReadDataByCommonIdentifier
- [_SET_EEPROM_STATE_OF_DELIVERY](#job-set-eeprom-state-of-delivery) - write and read the  EEPROM state of delivery KWP2000: $2E WriteDataByCommonIdentifier .        $22 ReadDataByCommonIdentifier
- [STEUERN_PPC](#job-steuern-ppc) - de/activation of ppc KWP2000: $30 InputOutputControlByLocalIdentifier .        $95 activate .        $96 deactivate
- [STEUERN_AKTUATOR_PWM](#job-steuern-aktuator-pwm) - activation of actuator with certain duty cycle and time period KWP2000: $30 InputOutputControlByLocalIdentifier .        $90 pwm-output for actuator
- [STEUERN_CHECK_CONTROL](#job-steuern-check-control) - activates display of check-contol message KWP2000: $30 InputOutputControlByLocalIdentifier .        $93 activate display of check-control message
- [STEUERN_AKTUATOR](#job-steuern-aktuator) - motor activation when linear regulator mouted in steering wheel de/activate voltage when warning KWP2000: $30 InputOutputControlByLocalIdentifier .        $94 de/activate voltage when warning
- [WRITE_DATE_LAST_CODING](#job-write-date-last-coding) - write date of the last coding KWP2000: $3B WriteDataByLocalIdentifier .        $08 write date of the last coding
- [_SET_CAMINTRINSIC](#job-set-camintrinsic) - setting of intrinsic camera parameters and camera serial number KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress
- [_SET_CAMCALIBRATION](#job-set-camcalibration) - setting of calibration results and camera VIN KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress
- [_SET_VEHICLEGEOMETRY](#job-set-vehiclegeometry) - setting of extrinsic camera parameters , the coding valid bit and ECU VIN KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress
- [_COPY_CAMERAMIRROR](#job-copy-cameramirror) - copy of camera parameters to ECU KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress
- [_SET_DBGMSG](#job-set-dbgmsg) - de/activates debug messages KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress
- [_MEMORY_WRITE_FLOAT](#job-memory-write-float) - writes a real value to EEPROM KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress
- [_MEMORY_WRITE_LONG](#job-memory-write-long) - writes a long value to EEPROM KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress
- [_SET_SPEED_TABLE](#job-set-speed-table) - coding values for pwm settings of vibration KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress
- [_FPNR_COUNTER_CLEAR](#job-fpnr-counter-clear) - sets the FPNR counter to 0xFF KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress
- [_FPNR_COUNTER_READ](#job-fpnr-counter-read) - reads the FPNR counter KWP2000: $23 ReadMemoryByAddress
- [C_CHECKSUMME](#job-c-checksumme) - Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob
- [STEUERN_KALIBRIERUNG_LINKS](#job-steuern-kalibrierung-links) - TAC (target auto calibration), if target is in left position (driver's view) KWP2000: $31 StartRoutineByLocalIdentifier .        $20 StartCalibrationLeft
- [STEUERN_KALIBRIERUNG_RECHTS](#job-steuern-kalibrierung-rechts) - TAC (target auto calibration), if target is in right position (driver's view) KWP2000: $31 StartRoutineByLocalIdentifier .        $21 StartCalibrationRight
- [STEUERN_KALIBRIERUNG_HO](#job-steuern-kalibrierung-ho) - start SPC (service point calibration) KWP2000: $31 StartRoutineByLocalIdentifier .        $22 StartCalibrationInService
- [STEUERN_STOP_KALIBRIERUNG_HO](#job-steuern-stop-kalibrierung-ho) - stop SPC (service point calibration) KWP2000: $31 StartRoutineByLocalIdentifier .        $23 StopCalibrationInService
- [STATUS_KALIBRIERMODUS_HO](#job-status-kalibriermodus-ho) - status of SPC (service point calibration) KWP2000: $31 StartRoutineByLocalIdentifier .        $24 StatusCalibrationInService
- [_GET_CAMINTRINSIC](#job-get-camintrinsic) - reads intrinsic camera parameters and camera serial number KWP2000: $23 ReadMemoryByAddress
- [_GET_CAMCALIBRATION](#job-get-camcalibration) - reads calibration results and camera VIN KWP2000: $23 ReadMemoryByAddress
- [_GET_VEHICLEGEOMETRY](#job-get-vehiclegeometry) - reads extrinsic camera parameters , the coding valid bit and ECU VIN KWP2000: $23 ReadMemoryByAddress
- [_MEMORY_READ_FLOAT](#job-memory-read-float) - reads a real value from EEPROM KWP2000: $23 ReadMemoryByAddress
- [_MEMORY_READ_LONG](#job-memory-read-long) - reads a long value from EEPROM KWP2000: $23 ReadMemoryByAddress
- [STATUS_LVDS](#job-status-lvds) - reports status of the LVDS data stream KWP2000: $21 ReadDataByLocalIdentifier .        $23 status of LVDS data stream
- [_READ_VNR](#job-read-vnr) - read original and current SW versionnumbers KWP2000: $21 ReadDataByLocalIdentifier .        $36 versionnumbers
- [_STEUERN_TEST_FUNKTIONAL_TLC](#job-steuern-test-funktional-tlc) - activates extended TLC-Check at FAS KWP2000: $31 StartRoutineByLocalIdentifier .        $26 extended TLC-Check
- [_UNIVERSAL_JOB](#job-universal-job) - transmits an individual diagnostic request to the ECU

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

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default

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

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | string | table SpeicherSegment SEG_NAME SEG_TEXT |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| ANZAHL | int | 1 - n ( 254 ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | string | table SpeicherSegment SEG_NAME SEG_TEXT |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| ANZAHL | int | 1 - n ( max. 249 ) |
| DATEN | string | zu schreibende Daten (Anzahl siehe oben) z.B. 1,2,03,0x04,0x05... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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

<a id="job-read-uif-data-table"></a>
### _READ_UIF_DATA_TABLE

reads the user info field KWP2000: $1A ReadECUIdentification .        $86 CurrentUIFDataTable

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ADDRESS_OFFSET | string | adress offset |
| VIN | string | VehicleIdeniticationNumber |
| PROGRAMMING_DATE | string |  |
| BMW_ASSEMBLY_NUMBER | string |  |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-read-sys-name"></a>
### _READ_SYS_NAME

reads the system name KWP2000: $1A ReadECUIdentification .        $97 SystemName

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VAR_INDEX | unsigned int | variant index |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-read-vmecuhwvnm"></a>
### _READ_VMECUHWVNM

reads the VehicleManufacturerECUHWVersionNumber KWP2000: $1A ReadECUIdentification .        $9A HW Index

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HW_INDEX | string | Vehicle manufacturer ECU HW version number |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-read-vm-diag-index"></a>
### _READ_VM_DIAG_INDEX

read diagnostic index KWP2000: $1A ReadECUIdentification .        $9C VMDiagnosticIndex

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_INDEX | string | diagnostic index |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-read-date-ecu-manufacturing"></a>
### _READ_DATE_ECU_MANUFACTURING

read date of ECU manufacturing KWP2000: $1A ReadECUIdentification .        $9D DateOfECUManufacturing

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATE | string | date of ECU manufacturing |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-read-sys-supp-index"></a>
### _READ_SYS_SUPP_INDEX

read system supplier index KWP2000: $1A ReadECUIdentification .        $9E SupplierIndex

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SUPP_INDEX | string | supplier index as hex number |
| SUPP_INDEX_TEXT | string | supplier index as text |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-read-vm-ecu-swlayer-vnr"></a>
### _READ_VM_ECU_SWLAYER_VNR

read MCV-nr, SW-nr, SC-nr KWP2000: $1A ReadECUIdentification .        $9F VMECUSoftwareLayerVersionNumber

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_SW_NR_MCV | string |  |
| ID_SW_NR_FSV | string |  |
| ID_SW_NR_OSV | string |  |
| ID_SW_NR_RES | string |  |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-read-date-last-coding"></a>
### READ_DATE_LAST_CODING

read date of the last coding KWP2000: $21 ReadDataByLocalIdentifier .        $08 date of the last coding

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATE | string | date of last coding |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-kamera-versorgung"></a>
### STATUS_KAMERA_VERSORGUNG

reports the status of the camera supply KWP2000: $21 ReadDataByLocalIdentifier .        $22 status of camera supply

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_STATUS | unsigned int | status byte as integer |
| STAT_SPANNUNG_TEXT | string | status byte as text table LIMIT_DESCRIPTION DESCRIPTION |
| STAT_SPANNUNG_WERT | real | measurement as floating point value |
| STAT_SPANNUNG_EINH | string | physical unit: V |
| STAT_STROM_STATUS | unsigned int | status byte as integer |
| STAT_STROM_TEXT | string | status byte as text table LIMIT_DESCRIPTION DESCRIPTION |
| STAT_STROM_WERT | real | measurement as floating point value |
| STAT_STROM_EINH | string | physical unit: A |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-fpn"></a>
### STATUS_FPN

reports status of the fixes pattern noise evaluation KWP2000: $21 ReadDataByLocalIdentifier .        $24 status of fixes pattern noise evaluation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FPN_STATUS | unsigned int | status byte als integer |
| STAT_FPN_TEXT | string | status byte as text table FPN_DESCRIPTION DESCRIPTION |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-kamera-eeprom"></a>
### STATUS_KAMERA_EEPROM

reports communication status with the camera eeprom KWP2000: $21 ReadDataByLocalIdentifier .        $26 status of camera eeprom communication

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EEPROM_STATUS | unsigned int | status byte as integer |
| STAT_EEPROM_TEXT | string | status byte as text table EEPROM_COMM_DESCRIPTION DESCRIPTION |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-kameraseriennummer"></a>
### STATUS_KAMERASERIENNUMMER

reads camera serial number from eeprom KWP2000: $21 ReadDataByLocalIdentifier .        $28 camera serial number

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KAMERASERIENNUMMER_TEXT | string | camera serial number |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-bordnetz-spannung"></a>
### STATUS_BORDNETZ_SPANNUNG

reports status of the voltage of the vehicle electrical system KWP2000: $21 ReadDataByLocalIdentifier .        $30 status of vehicle electrical system

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BORDNETZ_STATUS | unsigned int | status byte as integer |
| STAT_BORDNETZ_TEXT | string | status byte as text table LIMIT_DESCRIPTION DESCRIPTION |
| STAT_BORDNETZ_WERT | real | measurement as floating point value |
| STAT_BORDNETZ_EINH | string | physical unit: V |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-temperatur"></a>
### STATUS_TEMPERATUR

reports status of the ECU temperature KWP2000: $21 ReadDataByLocalIdentifier .        $31 status of ecu temperature

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPERATUR_WERT | char | pos./neg. ecu temperature |
| STAT_TEMPERATUR_EINH | string | physical unit: °C |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-weckleitung"></a>
### STATUS_WECKLEITUNG

reports status of wake line KWP2000: $21 ReadDataByLocalIdentifier .        $32 status of wake line

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WECKLEITUNG_STATUS | unsigned int | status byte as integer |
| STAT_WECKLEITUNG_TEXT | string | status byte as text table WAKE_LINE_DESCRIPTION DESCRIPTION |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-ecu-spannungen"></a>
### STATUS_ECU_SPANNUNGEN

reports status of the voltages of the ECU power supply units KWP2000: $21 ReadDataByLocalIdentifier .        $33 status of power supply units

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_1_5V_STATUS | unsigned int | status byte als integer |
| STAT_3_3V_STATUS | unsigned int | status byte as integer |
| STAT_5V_STATUS | unsigned int | status byte as integer |
| STAT_1_5V_TEXT | string | status byte as text table LIMIT_DESCRIPTION DESCRIPTION |
| STAT_3_3V_TEXT | string | status byte as text table LIMIT_DESCRIPTION DESCRIPTION |
| STAT_5V_TEXT | string | status byte as text table LIMIT_DESCRIPTION DESCRIPTION |
| STAT_1_5_V_WERT | real | measurement as floating point value |
| STAT_3_3_V_WERT | real | measurement as floating point value |
| STAT_5_V_WERT | real | measurement as floating point value |
| STAT_1_5V_EINH | string | physical unit: V |
| STAT_3_3V_EINH | string | physical unit: V |
| STAT_5V_EINH | string | physical unit: V |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-ppc"></a>
### STATUS_PPC

reports status of the power PC KWP2000: $21 ReadDataByLocalIdentifier .        $34 status of power pc

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PPC_STATUS | unsigned int | status byte as integer |
| STAT_PPC_TEXT | string | status byte as text table PPC_DESCRIPTION DESCRIPTION |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-aktuator"></a>
### STATUS_AKTUATOR

reports status of the vibration actuators current consumption KWP2000: $21 ReadDataByLocalIdentifier .        $35 status of vibration actuator

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AKTUATORSTROM_STATUS | unsigned int | status byte as integer |
| STAT_AKTUATORSTROM_TEXT | string | status byte as text table LIMIT_DESCRIPTION DESCRIPTION |
| STAT_AKTUATORSTROM_WERT | real | measurement as floating point value |
| STAT_AKTUATORSTROM_EINH | string | physical unit: A |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-fetrawe-mode"></a>
### STATUS_FETRAWE_MODE

reports status of the FeTraWe-Mode KWP2000: $22 ReadDataByCommonIdentifier .        $10 read fetrawe mode .        $0A

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FETRAWE_MODE_STATUS | string | status of fetrawe mode table FETRAWE_MODE_DESCRIPTION DESCRIPTION |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-read-eeprom-block"></a>
### _READ_EEPROM_BLOCK

reports status of the FeTraWe-Mode KWP2000: $22 ReadDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | int | EEPROM-Block e.g. 0x3000 - 0x3E09 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CONTENT | binary | block data content |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | ECU response |
| _TEL_AUFTRAG | binary | request to ECU |

<a id="job-set-eeprom-state-of-delivery"></a>
### _SET_EEPROM_STATE_OF_DELIVERY

write and read the  EEPROM state of delivery KWP2000: $2E WriteDataByCommonIdentifier .        $22 ReadDataByCommonIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |

<a id="job-steuern-ppc"></a>
### STEUERN_PPC

de/activation of ppc KWP2000: $30 InputOutputControlByLocalIdentifier .        $95 activate .        $96 deactivate

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_PPC | string | "ein/1" - activate "aus/0" - deactivate |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-aktuator-pwm"></a>
### STEUERN_AKTUATOR_PWM

activation of actuator with certain duty cycle and time period KWP2000: $30 InputOutputControlByLocalIdentifier .        $90 pwm-output for actuator

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PWM_PROZENT | int | PWM in %, range of values to max. 100% (100 = 100%) |
| PWM_TIME | int | PWM output time in 100ms steps (max. 10 sec) -&gt; e.g. 1 = 100 ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-check-control"></a>
### STEUERN_CHECK_CONTROL

activates display of check-contol message KWP2000: $30 InputOutputControlByLocalIdentifier .        $93 activate display of check-control message

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-aktuator"></a>
### STEUERN_AKTUATOR

motor activation when linear regulator mouted in steering wheel de/activate voltage when warning KWP2000: $30 InputOutputControlByLocalIdentifier .        $94 de/activate voltage when warning

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WARNING_TIME | int | time duration of warning output in 100 ms steps (max 10 sec.) 0 = warning output off |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-write-date-last-coding"></a>
### WRITE_DATE_LAST_CODING

write date of the last coding KWP2000: $3B WriteDataByLocalIdentifier .        $08 write date of the last coding

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DAY | int | day of last coding - DD bcd coded |
| MONTH | int | month of last coding - MM bcd coded |
| YEAR | int | year of last coding - YY bcd coded |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATE | string | date of last coding |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-set-camintrinsic"></a>
### _SET_CAMINTRINSIC

setting of intrinsic camera parameters and camera serial number KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERIAL | string | camera serial number written to 0x3E0900 - max. 8 digits |
| K1 | real | written to 0x3E0204 |
| K2 | real | written to 0x3E0208 |
| OPTIK_VERSATZ_X | long | written to 0x3E020C |
| OPTIK_VERSATZ_Y | long | written to 0x3E0210 |
| FOCAL_LENGTH | long | camera's focal length written to 0x3E0214 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_BLOCK_3E02 | string | consistency of camera parameters in eeprom block 3E02 |
| EEPROM_BLOCK_3E09 | string | consistency of camera parameters in eeprom block 3E09 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |
| _TEL_ANTWORT_2 | binary | ECU response |
| _TEL_AUFTRAG_2 | binary | request to ECU |
| _TEL_AUFTRAG_3 | binary | request to ECU |
| _TEL_ANTWORT_3 | binary | ECU response |
| _TEL_ANTWORT_4 | binary | ECU response |
| _TEL_AUFTRAG_4 | binary | request to ECU |

<a id="job-set-camcalibration"></a>
### _SET_CAMCALIBRATION

setting of calibration results and camera VIN KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VIN_CAM | string | camera VehicleIdentificationNunmber written to 0x3E0601 - 7 digits |
| ORIGINAL_YAW_CAMERA | long | yaw angle(vertical axis) written to 0x3E0801 |
| ORIGINAL_ROLL_CAMERA | real | roll angle(longitudinal axis) written to 0x3E0805 |
| ORIGINAL_PITCH_CAMERA | long | pitch angle (horizontal axis) written to 0x3E0809 |
| ORIGINAL_HEIGHT_CAMERA | real | camera height written to 0x3E080D |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_BLOCK_3E06 | string | consistency of camera parameters in eeprom block 3E06 |
| EEPROM_BLOCK_3E08 | string | consistency of camera parameters in eeprom block 3E08 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |
| _TEL_ANTWORT_2 | binary | ECU response |
| _TEL_AUFTRAG_2 | binary | request to ECU |
| _TEL_AUFTRAG_3 | binary | request to ECU |
| _TEL_ANTWORT_3 | binary | ECU response |
| _TEL_ANTWORT_4 | binary | ECU response |
| _TEL_AUFTRAG_4 | binary | request to ECU |

<a id="job-set-vehiclegeometry"></a>
### _SET_VEHICLEGEOMETRY

setting of extrinsic camera parameters , the coding valid bit and ECU VIN KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VIN_ECU | string | ECU VehicleIdentificationNunmber written to 0x3800 - 7 digits |
| INITIAL_HEIGHT | real | written to 0x320001 |
| Y_DISTANCE_LEFT | real | written to 0x320005 |
| Y_DISTANCE_RIGHT | real | written to 0x320009 |
| X_DIST_CAM_TO_FRONT_AXLE | real | written to 0x32000D |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_BLOCK_3800 | string | consistency of camera parameters in eeprom block 3800 |
| EEPROM_BLOCK_3200 | string | consistency of camera parameters in eeprom block 3200 |
| EEPROM_BLOCK_3701 | string | consistency of camera parameters in eeprom block 3701 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |
| _TEL_ANTWORT_2 | binary | ECU response |
| _TEL_AUFTRAG_2 | binary | request to ECU |
| _TEL_AUFTRAG_3 | binary | request to ECU |
| _TEL_ANTWORT_3 | binary | ECU response |
| _TEL_ANTWORT_4 | binary | ECU response |
| _TEL_AUFTRAG_4 | binary | request to ECU |
| _TEL_AUFTRAG_5 | binary | request to ECU |
| _TEL_ANTWORT_5 | binary | ECU response |
| _TEL_ANTWORT_6 | binary | ECU response |
| _TEL_AUFTRAG_6 | binary | request to ECU |

<a id="job-copy-cameramirror"></a>
### _COPY_CAMERAMIRROR

copy of camera parameters to ECU KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| INTRINSIC | string | status of the intrinsic camera parameters copies 20 bytes from 0x3E0204 to 0x310004 |
| VIN | string | status of the VehicleIdentificationNumber copies 7 bytes from 0x3E0601 to 0x380001 |
| S_N | string | status of the SerialNumber copies 4 bytes from 0x3E0900 to 0x380200 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | request to ECU |
| _TEL_AUFTRAG | binary | ECU response |
| _TEL_ANTWORT_2 | binary | ECU response |
| _TEL_AUFTRAG_2 | binary | request to ECU |
| _TEL_ANTWORT_3 | binary | ECU response |
| _TEL_AUFTRAG_3 | binary | request to ECU |
| _TEL_ANTWORT_4 | binary | request to ECU |
| _TEL_AUFTRAG_4 | binary | ECU response |
| _TEL_ANTWORT_5 | binary | ECU response |
| _TEL_AUFTRAG_5 | binary | request to ECU |
| _TEL_ANTWORT_6 | binary | ECU response |
| _TEL_AUFTRAG_6 | binary | request to ECU |
| _TEL_ANTWORT_7 | binary | request to ECU |
| _TEL_AUFTRAG_7 | binary | ECU response |
| _TEL_ANTWORT_8 | binary | request to ECU |
| _TEL_AUFTRAG_8 | binary | request to ECU |
| _TEL_ANTWORT_9 | binary | request to ECU |
| _TEL_AUFTRAG_9 | binary | request to ECU |

<a id="job-set-dbgmsg"></a>
### _SET_DBGMSG

de/activates debug messages KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DBGMSG | string | "on" - activates debug message "off" - deactivates debug message |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_BLOCK_3000 | string | consistency of Debug-Message Byte in eeprom block 3000 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-memory-write-float"></a>
### _MEMORY_WRITE_FLOAT

writes a real value to EEPROM KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADR | unsigned long | address to be written e.g. "0x320002" |
| PARAMETER | real | parameter to be written |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-memory-write-long"></a>
### _MEMORY_WRITE_LONG

writes a long value to EEPROM KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADR | unsigned long | address to be read from e.g. "0x320002" |
| PARAMETER | long | parameter to be written |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-set-speed-table"></a>
### _SET_SPEED_TABLE

coding values for pwm settings of vibration KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | mode of operation: default-mode, 100%-mode "default" - sets speed table to 60\|65\|70\|80\|85\|90\|95\|98 "100%" - sets speed table to 100\|100\|100\|100\|100\|100\|100\|100 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_SPEED_TABLE_DATA | string | consistency of parameters in block adress 300107 - 300116 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |
| _TEL_AUFTRAG_2 | binary | request to ECU |
| _TEL_ANTWORT_2 | binary | ECU response |

<a id="job-fpnr-counter-clear"></a>
### _FPNR_COUNTER_CLEAR

sets the FPNR counter to 0xFF KWP2000: $3D WriteMemoryByAddress KWP2000: $23 ReadMemoryByAddress

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_FPNR_COUNTER | string | status of FPNR counter in block adress 3B0400 counter cleared / not cleared |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |
| _TEL_AUFTRAG_2 | binary | request to ECU |
| _TEL_ANTWORT_2 | binary | ECU response |

<a id="job-fpnr-counter-read"></a>
### _FPNR_COUNTER_READ

reads the FPNR counter KWP2000: $23 ReadMemoryByAddress

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FPNR_COUNTER | string | content of FPNR counter |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-c-checksumme"></a>
### C_CHECKSUMME

Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte  21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| OUT_BUFFER | binary | Als Result wird der gefuellte Binaerbuffer zurueckgegeben Der Binaerbuffer hat den Aufbau von BINAER_BUFFER |

<a id="job-steuern-kalibrierung-links"></a>
### STEUERN_KALIBRIERUNG_LINKS

TAC (target auto calibration), if target is in left position (driver's view) KWP2000: $31 StartRoutineByLocalIdentifier .        $20 StartCalibrationLeft

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENTF_X | int | distance between front axle (vehicle) and gantry range: -32768 -&gt; 32767 resolution: 1 mm |
| ENTF_Y | int | distance between the vehicle's middle axle and the fictional middle axle between the 2 target positions a shift to the right means a positive value range: -32768 -&gt; 32767 resolution: 1 mm |
| ENTF_Z_O | int | distance between the ground and the middle of the upper target range: -32768 -&gt; 32767 resolution: 1 mm |
| ENTF_Z_U | int | distance between the ground and the middle of the lower target range: -32768 -&gt; 32767 resolution: 1 mm |
| KAMERA_HOEHE | int | mounting height of the camera range: -32768 -&gt; 32767 resolution: 1 mm |
| TARGET_POS_ENTF | int | distance between the outer left edge of the left target to the outer left edge of the right target range: -32768 -&gt; 32767 resolution: 1 mm |
| QUADRAT_GROESSE | int | size of the checker's squares (Schachbrettmuster) of the targets range: -32768 -&gt; 32767 resolution: 1 mm |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_KALIBRIERUNG_LINKS_STATUS | unsigned int | status byte of calibration as integer |
| STATUS_KALIBRIERUNG_LINKS_TEXT | string | status byte of calibration as text table CALIBRATION_DESCRIPTION DESCRIPTION |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-kalibrierung-rechts"></a>
### STEUERN_KALIBRIERUNG_RECHTS

TAC (target auto calibration), if target is in right position (driver's view) KWP2000: $31 StartRoutineByLocalIdentifier .        $21 StartCalibrationRight

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENTF_X | int | distance between front axle (vehicle) and gantry range: -32768 -&gt; 32767 resolution: 1 mm |
| ENTF_Y | int | distance between the vehicle's middle axle and the fictional middle axle between the 2 target positions a shift to the right means a positive value range: -32768 -&gt; 32767 resolution: 1 mm |
| ENTF_Z_O | int | distance between the ground and the middle of the upper target range: -32768 -&gt; 32767 resolution: 1 mm |
| ENTF_Z_U | int | distance between the ground and the middle of the lower target range: -32768 -&gt; 32767 resolution: 1 mm |
| KAMERA_HOEHE | int | mounting height of the camera range: -32768 -&gt; 32767 resolution: 1 mm |
| TARGET_POS_ENTF | int | distance between the outer left edge of the left target to the outer left edge of the right target range: -32768 -&gt; 32767 resolution: 1 mm |
| QUADRAT_GROESSE | int | size of the checker's squares (Schachbrettmuster) of the targets range: -32768 -&gt; 32767 resolution: 1 mm |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_KALIBRIERUNG_RECHTS_STATUS | unsigned int | status byte of calibration as integer |
| STATUS_KALIBRIERUNG_RECHTS_TEXT | string | status byte of calibration as text table CALIBRATION_DESCRIPTION DESCRIPTION |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-kalibrierung-ho"></a>
### STEUERN_KALIBRIERUNG_HO

start SPC (service point calibration) KWP2000: $31 StartRoutineByLocalIdentifier .        $22 StartCalibrationInService

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-stop-kalibrierung-ho"></a>
### STEUERN_STOP_KALIBRIERUNG_HO

stop SPC (service point calibration) KWP2000: $31 StartRoutineByLocalIdentifier .        $23 StopCalibrationInService

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-kalibriermodus-ho"></a>
### STATUS_KALIBRIERMODUS_HO

status of SPC (service point calibration) KWP2000: $31 StartRoutineByLocalIdentifier .        $24 StatusCalibrationInService

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KALIBRIERUNG_HO_STATUS | unsigned int | status byte of calibration as integer |
| STAT_KALIBRIERUNG_HO_TEXT | string | status byte of calibration as text table STAT_CAL_DESCRIPTION DESCRIPTION |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-get-camintrinsic"></a>
### _GET_CAMINTRINSIC

reads intrinsic camera parameters and camera serial number KWP2000: $23 ReadMemoryByAddress

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SERIAL | string | camera serial number read from 0x3E0900 - 4 bytes BCD |
| K1 | real | read from 0x3E0204 |
| K2 | real | read from 0x3E0208 |
| OPTIK_VERSATZ_X | long | read from 0x3E020C |
| OPTIK_VERSATZ_Y | long | read from 0x3E0210 |
| FOCAL_LENGTH | long | camera's focal length read from 0x3E0214 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |
| _TEL_AUFTRAG_2 | binary | request to ECU |
| _TEL_ANTWORT_2 | binary | ECU response |

<a id="job-get-camcalibration"></a>
### _GET_CAMCALIBRATION

reads calibration results and camera VIN KWP2000: $23 ReadMemoryByAddress

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VIN_CAM | string | camera vehicle identification number read from 0x3E0601 - 7 digits |
| ORIGINAL_YAW_CAMERA | long | yaw angle(vertical axis) read from 0x3E0801 |
| ORIGINAL_ROLL_CAMERA | real | roll angle(longitudinal axis) read from 0x3E0805 |
| ORIGINAL_PITCH_CAMERA | long | pitch angle (horizontal axis) read from 0x3E0809 |
| ORIGINAL_HEIGHT_CAMERA | real | camera height read from 0x3E080D |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |
| _TEL_AUFTRAG_2 | binary | request to ECU |
| _TEL_ANTWORT_2 | binary | ECU response |

<a id="job-get-vehiclegeometry"></a>
### _GET_VEHICLEGEOMETRY

reads extrinsic camera parameters , the coding valid bit and ECU VIN KWP2000: $23 ReadMemoryByAddress

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VIN_ECU | string | ECU VehicleIdentificationNunmber read from 0x380001 - 7 digits |
| INITIAL_HEIGHT | real | read from 0x320001 |
| Y_DISTANCE_LEFT | real | read from 0x320005 |
| Y_DISTANCE_RIGHT | real | read from 0x320009 |
| X_DIST_CAM_TO_FRONT_AXLE | real | read from 0x32000D |
| CODING_VALID_BIT | string | bit is set or cleared read from 0x370101 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |
| _TEL_AUFTRAG_2 | binary | request to ECU |
| _TEL_ANTWORT_2 | binary | ECU response |
| _TEL_AUFTRAG_3 | binary | request to ECU |
| _TEL_ANTWORT_3 | binary | ECU response |

<a id="job-memory-read-float"></a>
### _MEMORY_READ_FLOAT

reads a real value from EEPROM KWP2000: $23 ReadMemoryByAddress

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADR | unsigned long | address to be read from e.g. "0x320002" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | real | parameter to be read |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-memory-read-long"></a>
### _MEMORY_READ_LONG

reads a long value from EEPROM KWP2000: $23 ReadMemoryByAddress

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADR | unsigned long | address to be read from e.g. "0x320002" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | long | parameter to be read |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-lvds"></a>
### STATUS_LVDS

reports status of the LVDS data stream KWP2000: $21 ReadDataByLocalIdentifier .        $23 status of LVDS data stream

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LVDS_STATUS | unsigned int | status byte as integer |
| STAT_LVDS_TEXT | string | status byte as text table LVDS_DESCRIPTION DESCRIPTION |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-read-vnr"></a>
### _READ_VNR

read original and current SW versionnumbers KWP2000: $21 ReadDataByLocalIdentifier .        $36 versionnumbers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ORIG_SW_MUC | string | original MUC version number |
| ORIG_SW_SUC | string | original SUC version number |
| ORIG_SW_CPLD | string | original CPLD version number |
| TLC_ALGO | string | Algo version number |
| ECU_Version | string | ECU version number |
| CURRENT_SW_MUC | string | current MUC version number |
| CURRENT_SW_SUC | string | current SUC version number |
| CURRENT_SW_CPLD | string | current MUC version number |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-test-funktional-tlc"></a>
### _STEUERN_TEST_FUNKTIONAL_TLC

activates extended TLC-Check at FAS KWP2000: $31 StartRoutineByLocalIdentifier .        $26 extended TLC-Check

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACTIVATION | unsigned int | de/activates the extended TLC-Check 0 - deactivation 1 - activation |
| SPEED | real | vehicle speed range: 0.0 -&gt; 400.0 resolution: 1 kmh |
| YAW | real | yaw angle range: -100.0 -&gt; 100.0 resolution: 1 °/s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-universal-job"></a>
### _UNIVERSAL_JOB

transmits an individual diagnostic request to the ECU

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REQUEST | string | holds the testers request in hex, e.g. speicher_lesen e.g. SID = 23 - ReadMemoryByAddress e.g. address_high = 30 e.g. address_middle = 01 e.g. address_low = 01 e.g. segement = 03 - NVRAM e.g. amount = 30 - 48 databytes input is the 233001010330 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (97 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (33 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (30 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (2 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [ERRORTYPE](#table-errortype) (5 × 2)
- [LIMIT_DESCRIPTION](#table-limit-description) (5 × 2)
- [CAMCONN_DESCRIPTION](#table-camconn-description) (4 × 2)
- [LVDS_DESCRIPTION](#table-lvds-description) (4 × 2)
- [FPN_DESCRIPTION](#table-fpn-description) (4 × 2)
- [EEPROM_COMM_DESCRIPTION](#table-eeprom-comm-description) (4 × 2)
- [VIDEO_DATA_DESCRIPTION](#table-video-data-description) (4 × 2)
- [WAKE_LINE_DESCRIPTION](#table-wake-line-description) (4 × 2)
- [MEM_CONSISTENT_DESCRIPTION](#table-mem-consistent-description) (4 × 2)
- [PPC_DESCRIPTION](#table-ppc-description) (4 × 2)
- [FETRAWE_MODE_DESCRIPTION](#table-fetrawe-mode-description) (4 × 2)
- [EEPROM_BLOCK_3000](#table-eeprom-block-3000) (32 × 2)
- [EEPROM_BLOCK_3001](#table-eeprom-block-3001) (32 × 2)
- [EEPROM_BLOCK_3002](#table-eeprom-block-3002) (17 × 2)
- [EEPROM_BLOCK_3203](#table-eeprom-block-3203) (11 × 2)
- [EEPROM_BLOCK_3400](#table-eeprom-block-3400) (5 × 2)
- [EEPROM_BLOCK_3500](#table-eeprom-block-3500) (128 × 2)
- [EEPROM_BLOCK_3501](#table-eeprom-block-3501) (16 × 2)
- [EEPROM_BLOCK_3600](#table-eeprom-block-3600) (3 × 2)
- [EEPROM_BLOCK_3601](#table-eeprom-block-3601) (4 × 2)
- [EEPROM_BLOCK_3700](#table-eeprom-block-3700) (5 × 2)
- [EEPROM_BLOCK_3701](#table-eeprom-block-3701) (4 × 2)
- [EEPROM_BLOCK_3800](#table-eeprom-block-3800) (32 × 2)
- [EEPROM_BLOCK_3802](#table-eeprom-block-3802) (4 × 2)
- [EEPROM_BLOCK_3B02](#table-eeprom-block-3b02) (96 × 2)
- [EEPROM_BLOCK_3B03](#table-eeprom-block-3b03) (25 × 2)
- [EEPROM_BLOCK_3B04](#table-eeprom-block-3b04) (7 × 2)
- [EEPROM_BLOCK_3B06](#table-eeprom-block-3b06) (32 × 2)
- [EEPROM_BLOCK_3B07](#table-eeprom-block-3b07) (32 × 2)
- [EEPROM_BLOCK_3B08](#table-eeprom-block-3b08) (32 × 2)
- [EEPROM_BLOCK_3B09](#table-eeprom-block-3b09) (32 × 2)
- [EEPROM_BLOCK_3B0A](#table-eeprom-block-3b0a) (32 × 2)
- [CALIBRATION_DESCRIPTION](#table-calibration-description) (56 × 2)
- [STAT_CAL_DESCRIPTION](#table-stat-cal-description) (6 × 2)
- [VNR_DESCRIPTION](#table-vnr-description) (9 × 2)

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

Dimensions: 97 rows × 2 columns

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

<a id="table-speichersegment"></a>
### SPEICHERSEGMENT

Dimensions: 12 rows × 3 columns

| SEG_BYTE | SEG_NAME | SEG_TEXT |
| --- | --- | --- |
| 0x00 | LAR | linearAdressRange |
| 0x01 | ROMI | ROM / EPROM, internal |
| 0x02 | ROMX | ROM / EPROM, external |
| 0x03 | NVRAM | NV-RAM (characteristic zones, DTC memory |
| 0x04 | RAMIS | RAM, internal (short MOV) |
| 0x05 | RAMXX | RAM, external (x data MOV) |
| 0x06 | FLASH | Flash EPROM, internal |
| 0x07 | UIFM | User Info Field Memory |
| 0x08 | VODM | Vehicle Order Data Memory |
| 0x09 | FLASHX | Flash EPROM, external |
| 0x0B | RAMIL | RAM, internal (long MOV / Register) |
| 0xFF | ??? | unbekanntes Speichersegment |

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

Dimensions: 33 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA928 | Spannungsversorgung Kamera |
| 0xA929 | Power PC Watchdog |
| 0xA92A | Verbindung Imager-ECU unterbrochen |
| 0xA92B | Kamera-Kalibrierung |
| 0xA92C | Kalibrierung Out of Range |
| 0xA92E | EEPROM Kommunikation |
| 0xA92F | Spannungsversorgung (Klemme 30) |
| 0xA930 | interne Spannungsversorgung (Netzteil 1-3) |
| 0xA931 | Aktuator |
| 0xA932 | Timeout CAN ID 1A0h (Geschwindigkeit) |
| 0xA933 | Timeot CAN ID C8h (Lenkradwinkel oben) |
| 0xA934 | Timeout CAN ID C4h (Lenkradwinkel unten) |
| 0xA935 | Timeout CAN ID 21Ah (Lampenzustand) |
| 0xA936 | Timeout CAN ID 314h (Status Fahrlicht) |
| 0xA937 | Timeout CAN ID 2A6h (Bedienung Wischer) |
| 0xA938 | Timeout CAN ID 226h (Wischergeschwindigkeit) |
| 0xA939 | PPC nicht funktionsfähig |
| 0xA93A | Timeout  CAN ID 1B4h (Status Kombi) |
| 0xA93B | Timeout CAN ID 1EEh (operation steering rod) |
| 0xA93D | Timeout CAN ID 130h (Klemmenstatus) |
| 0xA941 | Timeout CAN ID 330h (Kilometerstand) |
| 0xA942 | Timeout CAN ID 1D6h (Bedienung Audio Telefon) |
| 0xA943 | Timeout CAN ID 19Eh (STAT_DSC) |
| 0xA944 | Timeout CAN ID 1D0h (Engine_1, Status Motor) |
| 0xA946 | Checksummenfehler ECU EEPROM |
| 0xA947 | Checksummenfehler Kamera EEPROM |
| 0xA948 | ECU nicht korrekt kodiert |
| 0xA949 | Algorithm parameter out of range |
| 0xA94A | CPLD error |
| 0xA94B | EEPROM communication ECU |
| 0xE047 | Bus Off, Fehler Nr. 3h |
| 0xA92D | Energiesparmode aktiv |
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

Dimensions: 30 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xA928 | 0x01 | 0x0A | - | - |
| 0xA929 | 0x01 | 0x0A | - | - |
| 0xA92A | 0x01 | 0x0A | - | - |
| 0xA92B | 0x01 | 0x0A | - | - |
| 0xA92C | 0x01 | 0x0A | - | - |
| 0xA92D | 0x01 | 0x0A | - | - |
| 0xA92E | 0x01 | 0x0A | - | - |
| 0xA92F | 0x01 | 0x0A | - | - |
| 0xA930 | 0x01 | 0x0A | - | - |
| 0xA931 | 0x01 | 0x0A | - | - |
| 0xA932 | 0x01 | 0x0A | - | - |
| 0xA933 | 0x01 | 0x0A | - | - |
| 0xA934 | 0x01 | 0x0A | - | - |
| 0xA935 | 0x01 | 0x0A | - | - |
| 0xA936 | 0x01 | 0x0A | - | - |
| 0xA937 | 0x01 | 0x0A | - | - |
| 0xA938 | 0x01 | 0x0A | - | - |
| 0xA939 | 0x01 | 0x0A | - | - |
| 0xA93A | 0x01 | 0x0A | - | - |
| 0xA93C | 0x01 | 0x0A | - | - |
| 0xA93D | 0x01 | 0x0A | - | - |
| 0xA941 | 0x01 | 0x0A | - | - |
| 0xA942 | 0x01 | 0x0A | - | - |
| 0xA943 | 0x01 | 0x0A | - | - |
| 0xA944 | 0x01 | 0x0A | - | - |
| 0xA946 | 0x01 | 0x0A | - | - |
| 0xA947 | 0x01 | 0x0A | - | - |
| 0xA948 | 0x01 | 0x0A | - | - |
| 0xE047 | 0x01 | 0x0A | - | - |
| 0xFFFF | 0x01 | 0x0A | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 2 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Bordspannung | VOLT | - | unsigned char | - | 1 | 10 | 0 |
| 0x0A | Botschaftenfehler | 0-n | - | 0xFF | ERRORTYPE | 1 | 1 | 0 |

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

<a id="table-errortype"></a>
### ERRORTYPE

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Timeout |
| 0x02 | Alive |
| 0x04 | Checksum |
| 0x08 | Application |
| xy | unplausibler Wert |

<a id="table-limit-description"></a>
### LIMIT_DESCRIPTION

Dimensions: 5 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x01 | unterhalb des Limits |
| 0x02 | innerhalb der Limits |
| 0x03 | überhalb der Limits |
| 0xFF | ungültig |
| xy | unplausibler Wert |

<a id="table-camconn-description"></a>
### CAMCONN_DESCRIPTION

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | nein |
| 0x01 | ja |
| 0xFF | ungültig |
| xy | unplausibler Wert |

<a id="table-lvds-description"></a>
### LVDS_DESCRIPTION

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x01 | Datenstrom ok |
| 0x02 | Datenstrom fehlerhaft |
| 0xFF | ungültig |
| xy | unplausibler Wert |

<a id="table-fpn-description"></a>
### FPN_DESCRIPTION

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | nein |
| 0x01 | ja |
| 0xFF | ungültig |
| xy | unplausibler Wert |

<a id="table-eeprom-comm-description"></a>
### EEPROM_COMM_DESCRIPTION

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | keine Kommunikation |
| 0x01 | Kommunikation möglich |
| 0xFF | ungültig |
| xy | unplausibler Wert |

<a id="table-video-data-description"></a>
### VIDEO_DATA_DESCRIPTION

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Videodaten in Ordnung |
| 0x01 | Videodaten nicht in Ordnung |
| 0xFF | ungültig |
| xy | unplausibler Wert |

<a id="table-wake-line-description"></a>
### WAKE_LINE_DESCRIPTION

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x01 | Weckleitung aktiv |
| 0x02 | Weckleitung nicht aktiv |
| 0xFF | ungültig |
| xy | unplausibler Wert |

<a id="table-mem-consistent-description"></a>
### MEM_CONSISTENT_DESCRIPTION

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Speichertyp konsistent |
| 0x01 | Speichertyp nicht konsistent |
| 0xFF | ungültig |
| xy | unplausibler Wert |

<a id="table-ppc-description"></a>
### PPC_DESCRIPTION

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | PowerPC nicht aktiv |
| 0x01 | PowerPC aktiv |
| 0xFF | ungültig |
| xy | unplausibler Wert |

<a id="table-fetrawe-mode-description"></a>
### FETRAWE_MODE_DESCRIPTION

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Fetrawe-Modus aktiv |
| 0x01 | Fetrawe-Modus nicht aktiv |
| 0xFF | ungültig |
| xy | unplausibler Wert |

<a id="table-eeprom-block-3000"></a>
### EEPROM_BLOCK_3000

Dimensions: 32 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | 01 |
| 0x02 | 01 |
| 0x03 | 00 |
| 0x04 | 46 |
| 0x05 | 41 |
| 0x06 | 01 |
| 0x07 | 03 |
| 0x08 | 96 |
| 0x09 | 14 |
| 0x0A | 01 |
| 0x0B | FF |
| 0x0C | FF |
| 0x0D | FF |
| 0x0E | FF |
| 0x0F | FF |
| 0x10 | FF |
| 0x11 | FF |
| 0x12 | FF |
| 0x13 | FF |
| 0x14 | FF |
| 0x15 | FF |
| 0x16 | FF |
| 0x17 | FF |
| 0x18 | FF |
| 0x19 | FF |
| 0x1A | FF |
| 0x1B | FF |
| 0x1C | FF |
| 0x1D | FF |
| 0x1E | FF |
| 0x1F | FF |

<a id="table-eeprom-block-3001"></a>
### EEPROM_BLOCK_3001

Dimensions: 32 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | 01 |
| 0x02 | 04 |
| 0x03 | 05 |
| 0x04 | 7D |
| 0x05 | 09 |
| 0x06 | 09 |
| 0x07 | 8C |
| 0x08 | 1E |
| 0x09 | 28 |
| 0x0A | 32 |
| 0x0B | 3C |
| 0x0C | 46 |
| 0x0D | 50 |
| 0x0E | 5A |
| 0x0F | 64 |
| 0x10 | 3C |
| 0x11 | 41 |
| 0x12 | 46 |
| 0x13 | 4B |
| 0x14 | 50 |
| 0x15 | 55 |
| 0x16 | 5F |
| 0x17 | 62 |
| 0x18 | 7D |
| 0x19 | FF |
| 0x1A | FF |
| 0x1B | FF |
| 0x1C | FF |
| 0x1D | 01 |
| 0x1E | 05 |
| 0x1F | 19 |

<a id="table-eeprom-block-3002"></a>
### EEPROM_BLOCK_3002

Dimensions: 17 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | 00 |
| 0x02 | 04 |
| 0x03 | 00 |
| 0x04 | 18 |
| 0x05 | 00 |
| 0x06 | C8 |
| 0x07 | 00 |
| 0x08 | 18 |
| 0x09 | 19 |
| 0x0A | 0F |
| 0x0B | 01 |
| 0x0C | FF |
| 0x0D | FF |
| 0x0E | FF |
| 0x0F | FF |
| 0x10 | FF |

<a id="table-eeprom-block-3203"></a>
### EEPROM_BLOCK_3203

Dimensions: 11 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | FF |
| 0x02 | FF |
| 0x03 | FF |
| 0x04 | FF |
| 0x05 | FF |
| 0x06 | FF |
| 0x07 | FF |
| 0x08 | FF |
| 0x09 | FF |
| 0x0A | FF |

<a id="table-eeprom-block-3400"></a>
### EEPROM_BLOCK_3400

Dimensions: 5 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 05 |
| 0x01 | 00 |
| 0x02 | 00 |
| 0x03 | 00 |
| 0x04 | 00 |

<a id="table-eeprom-block-3500"></a>
### EEPROM_BLOCK_3500

Dimensions: 128 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | 00 |
| 0x02 | 00 |
| 0x03 | 00 |
| 0x04 | 00 |
| 0x05 | 00 |
| 0x06 | 00 |
| 0x07 | 00 |
| 0x08 | 00 |
| 0x09 | 00 |
| 0x0A | 00 |
| 0x0B | 00 |
| 0x0C | 00 |
| 0x0D | 00 |
| 0x0E | 00 |
| 0x0F | 00 |
| 0x10 | 00 |
| 0x11 | 00 |
| 0x12 | 00 |
| 0x13 | 00 |
| 0x14 | 00 |
| 0x15 | 00 |
| 0x16 | 00 |
| 0x17 | 00 |
| 0x18 | 00 |
| 0x19 | 00 |
| 0x1A | 00 |
| 0x1B | 00 |
| 0x1C | 00 |
| 0x1D | 00 |
| 0x1E | 00 |
| 0x1F | 00 |
| 0x20 | 00 |
| 0x21 | 00 |
| 0x22 | 00 |
| 0x23 | 00 |
| 0x24 | 00 |
| 0x25 | 00 |
| 0x26 | 00 |
| 0x27 | 00 |
| 0x28 | 00 |
| 0x29 | 00 |
| 0x2A | 00 |
| 0x2B | 00 |
| 0x2C | 00 |
| 0x2D | 00 |
| 0x2E | 00 |
| 0x2F | 00 |
| 0x30 | 00 |
| 0x31 | 00 |
| 0x32 | 00 |
| 0x33 | 00 |
| 0x34 | 00 |
| 0x35 | 00 |
| 0x36 | 00 |
| 0x37 | 00 |
| 0x38 | 00 |
| 0x39 | 00 |
| 0x3A | 00 |
| 0x3B | 00 |
| 0x3C | 00 |
| 0x3D | 00 |
| 0x3E | 00 |
| 0x3F | 00 |
| 0x40 | 00 |
| 0x41 | 00 |
| 0x42 | 00 |
| 0x43 | 00 |
| 0x44 | 00 |
| 0x45 | 00 |
| 0x46 | 00 |
| 0x47 | 00 |
| 0x48 | 00 |
| 0x49 | 00 |
| 0x4A | 00 |
| 0x4B | 00 |
| 0x4C | 00 |
| 0x4D | 00 |
| 0x4E | 00 |
| 0x4F | 00 |
| 0x50 | 00 |
| 0x51 | 00 |
| 0x52 | 00 |
| 0x53 | 00 |
| 0x54 | 00 |
| 0x55 | 00 |
| 0x56 | 00 |
| 0x57 | 00 |
| 0x58 | 00 |
| 0x59 | 00 |
| 0x5A | 00 |
| 0x5B | 00 |
| 0x5C | 00 |
| 0x5D | 00 |
| 0x5E | 00 |
| 0x5F | 00 |
| 0x60 | 00 |
| 0x61 | FF |
| 0x62 | FF |
| 0x63 | FF |
| 0x64 | FF |
| 0x65 | FF |
| 0x66 | FF |
| 0x67 | FF |
| 0x68 | FF |
| 0x69 | FF |
| 0x6A | FF |
| 0x6B | FF |
| 0x6C | FF |
| 0x6D | FF |
| 0x6E | FF |
| 0x6F | FF |
| 0x70 | FF |
| 0x71 | FF |
| 0x72 | FF |
| 0x73 | FF |
| 0x74 | FF |
| 0x75 | FF |
| 0x76 | FF |
| 0x77 | FF |
| 0x78 | FF |
| 0x79 | FF |
| 0x7A | FF |
| 0x7B | FF |
| 0x7C | FF |
| 0x7D | FF |
| 0x7E | FF |
| 0x7F | FF |

<a id="table-eeprom-block-3501"></a>
### EEPROM_BLOCK_3501

Dimensions: 16 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | 00 |
| 0x02 | 00 |
| 0x03 | 00 |
| 0x04 | 00 |
| 0x05 | 00 |
| 0x06 | 00 |
| 0x07 | 00 |
| 0x08 | 00 |
| 0x09 | 00 |
| 0x0A | 00 |
| 0x0B | 00 |
| 0x0C | 00 |
| 0x0D | 00 |
| 0x0E | 00 |
| 0x0F | 00 |

<a id="table-eeprom-block-3600"></a>
### EEPROM_BLOCK_3600

Dimensions: 3 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | 01 |
| 0x02 | FF |

<a id="table-eeprom-block-3601"></a>
### EEPROM_BLOCK_3601

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | FF |
| 0x01 | FF |
| 0x02 | FF |
| 0x03 | FF |

<a id="table-eeprom-block-3700"></a>
### EEPROM_BLOCK_3700

Dimensions: 5 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | FF |
| 0x02 | FF |
| 0x03 | FF |
| 0x04 | FF |

<a id="table-eeprom-block-3701"></a>
### EEPROM_BLOCK_3701

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | 00 |
| 0x02 | 00 |
| 0x03 | 00 |

<a id="table-eeprom-block-3800"></a>
### EEPROM_BLOCK_3800

Dimensions: 32 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | FF |
| 0x02 | FF |
| 0x03 | FF |
| 0x04 | FF |
| 0x05 | FF |
| 0x06 | FF |
| 0x07 | FF |
| 0x08 | FF |
| 0x09 | FF |
| 0x0A | FF |
| 0x0B | FF |
| 0x0C | FF |
| 0x0D | FF |
| 0x0E | FF |
| 0x0F | FF |
| 0x10 | FF |
| 0x11 | FF |
| 0x12 | FF |
| 0x13 | FF |
| 0x14 | FF |
| 0x15 | FF |
| 0x16 | FF |
| 0x17 | FF |
| 0x18 | FF |
| 0x19 | FF |
| 0x1A | FF |
| 0x1B | FF |
| 0x1C | FF |
| 0x1D | FF |
| 0x1E | FF |
| 0x1F | FF |

<a id="table-eeprom-block-3802"></a>
### EEPROM_BLOCK_3802

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | FF |
| 0x01 | FF |
| 0x02 | FF |
| 0x03 | FF |

<a id="table-eeprom-block-3b02"></a>
### EEPROM_BLOCK_3B02

Dimensions: 96 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | FF |
| 0x01 | FF |
| 0x02 | FF |
| 0x03 | FF |
| 0x04 | FF |
| 0x05 | FF |
| 0x06 | FF |
| 0x07 | FF |
| 0x08 | FF |
| 0x09 | FF |
| 0x0A | FF |
| 0x0B | FF |
| 0x0C | FF |
| 0x0D | FF |
| 0x0E | FF |
| 0x0F | FF |
| 0x10 | FF |
| 0x11 | FF |
| 0x12 | FF |
| 0x13 | FF |
| 0x14 | FF |
| 0x15 | FF |
| 0x16 | FF |
| 0x17 | FF |
| 0x18 | FF |
| 0x19 | FF |
| 0x1A | FF |
| 0x1B | FF |
| 0x1C | FF |
| 0x1D | FF |
| 0x1E | FF |
| 0x1F | FF |
| 0x20 | FF |
| 0x21 | FF |
| 0x22 | FF |
| 0x23 | FF |
| 0x24 | FF |
| 0x25 | FF |
| 0x26 | FF |
| 0x27 | FF |
| 0x28 | FF |
| 0x29 | FF |
| 0x2A | FF |
| 0x2B | FF |
| 0x2C | FF |
| 0x2D | FF |
| 0x2E | FF |
| 0x2F | FF |
| 0x30 | FF |
| 0x31 | FF |
| 0x32 | FF |
| 0x33 | FF |
| 0x34 | FF |
| 0x35 | FF |
| 0x36 | FF |
| 0x37 | FF |
| 0x38 | FF |
| 0x39 | FF |
| 0x3A | FF |
| 0x3B | FF |
| 0x3C | FF |
| 0x3D | FF |
| 0x3E | FF |
| 0x3F | FF |
| 0x40 | FF |
| 0x41 | FF |
| 0x42 | FF |
| 0x43 | FF |
| 0x44 | FF |
| 0x45 | FF |
| 0x46 | FF |
| 0x47 | FF |
| 0x48 | FF |
| 0x49 | FF |
| 0x4A | FF |
| 0x4B | FF |
| 0x4C | FF |
| 0x4D | FF |
| 0x4E | FF |
| 0x4F | FF |
| 0x50 | FF |
| 0x51 | FF |
| 0x52 | FF |
| 0x53 | FF |
| 0x54 | FF |
| 0x55 | FF |
| 0x56 | FF |
| 0x57 | FF |
| 0x58 | FF |
| 0x59 | FF |
| 0x5A | FF |
| 0x5B | FF |
| 0x5C | FF |
| 0x5D | FF |
| 0x5E | FF |
| 0x5F | FF |

<a id="table-eeprom-block-3b03"></a>
### EEPROM_BLOCK_3B03

Dimensions: 25 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | FF |
| 0x01 | 5F |
| 0x02 | 00 |
| 0x03 | 00 |
| 0x04 | 00 |
| 0x05 | F1 |
| 0x06 | FF |
| 0x07 | FF |
| 0x08 | FF |
| 0x09 | 73 |
| 0x0A | 00 |
| 0x0B | 00 |
| 0x0C | 00 |
| 0x0D | 39 |
| 0x0E | B4 |
| 0x0F | 48 |
| 0x10 | 3D |
| 0x11 | 1E |
| 0x12 | 00 |
| 0x13 | 00 |
| 0x14 | 00 |
| 0x15 | 14 |
| 0x16 | 00 |
| 0x17 | 00 |
| 0x18 | 00 |

<a id="table-eeprom-block-3b04"></a>
### EEPROM_BLOCK_3B04

Dimensions: 7 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | FF |
| 0x01 | 00 |
| 0x02 | FF |
| 0x03 | 82 |
| 0x04 | 1A |
| 0x05 | FF |
| 0x06 | FF |

<a id="table-eeprom-block-3b06"></a>
### EEPROM_BLOCK_3B06

Dimensions: 32 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | 00 |
| 0x02 | 00 |
| 0x03 | 00 |
| 0x04 | 00 |
| 0x05 | 33 |
| 0x06 | 33 |
| 0x07 | 33 |
| 0x08 | 3F |
| 0x09 | 9A |
| 0x0A | 99 |
| 0x0B | 99 |
| 0x0C | 3E |
| 0x0D | 33 |
| 0x0E | 33 |
| 0x0F | 33 |
| 0x10 | 3F |
| 0x11 | CD |
| 0x12 | CC |
| 0x13 | CC |
| 0x14 | 3D |
| 0x15 | FF |
| 0x16 | FF |
| 0x17 | FF |
| 0x18 | FF |
| 0x19 | FF |
| 0x1A | FF |
| 0x1B | FF |
| 0x1C | FF |
| 0x1D | FF |
| 0x1E | FF |
| 0x1F | FF |

<a id="table-eeprom-block-3b07"></a>
### EEPROM_BLOCK_3B07

Dimensions: 32 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | 0A |
| 0x02 | D7 |
| 0x03 | A3 |
| 0x04 | 3C |
| 0x05 | CD |
| 0x06 | CC |
| 0x07 | CC |
| 0x08 | 3D |
| 0x09 | 00 |
| 0x0A | 00 |
| 0x0B | 00 |
| 0x0C | 00 |
| 0x0D | 00 |
| 0x0E | 00 |
| 0x0F | 20 |
| 0x10 | 40 |
| 0x11 | 00 |
| 0x12 | 00 |
| 0x13 | 40 |
| 0x14 | 40 |
| 0x15 | FF |
| 0x16 | FF |
| 0x17 | FF |
| 0x18 | FF |
| 0x19 | FF |
| 0x1A | FF |
| 0x1B | FF |
| 0x1C | FF |
| 0x1D | FF |
| 0x1E | FF |
| 0x1F | FF |

<a id="table-eeprom-block-3b08"></a>
### EEPROM_BLOCK_3B08

Dimensions: 32 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | 00 |
| 0x02 | 00 |
| 0x03 | 00 |
| 0x04 | 00 |
| 0x05 | CD |
| 0x06 | CC |
| 0x07 | 4C |
| 0x08 | 3E |
| 0x09 | 6F |
| 0x0A | 12 |
| 0x0B | 03 |
| 0x0C | 3A |
| 0x0D | 9A |
| 0x0E | 99 |
| 0x0F | 99 |
| 0x10 | 3E |
| 0x11 | 00 |
| 0x12 | 00 |
| 0x13 | 00 |
| 0x14 | 40 |
| 0x15 | FF |
| 0x16 | FF |
| 0x17 | FF |
| 0x18 | FF |
| 0x19 | FF |
| 0x1A | FF |
| 0x1B | FF |
| 0x1C | FF |
| 0x1D | FF |
| 0x1E | FF |
| 0x1F | FF |

<a id="table-eeprom-block-3b09"></a>
### EEPROM_BLOCK_3B09

Dimensions: 32 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | 00 |
| 0x02 | 00 |
| 0x03 | 00 |
| 0x04 | 3F |
| 0x05 | 00 |
| 0x06 | 00 |
| 0x07 | 80 |
| 0x08 | 3F |
| 0x09 | 00 |
| 0x0A | 24 |
| 0x0B | F4 |
| 0x0C | 49 |
| 0x0D | 00 |
| 0x0E | 00 |
| 0x0F | 80 |
| 0x10 | 40 |
| 0x11 | 39 |
| 0x12 | 8E |
| 0x13 | 9B |
| 0x14 | 41 |
| 0x15 | FF |
| 0x16 | FF |
| 0x17 | FF |
| 0x18 | FF |
| 0x19 | FF |
| 0x1A | FF |
| 0x1B | FF |
| 0x1C | FF |
| 0x1D | FF |
| 0x1E | FF |
| 0x1F | FF |

<a id="table-eeprom-block-3b0a"></a>
### EEPROM_BLOCK_3B0A

Dimensions: 32 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | 00 |
| 0x01 | C7 |
| 0x02 | 71 |
| 0x03 | 90 |
| 0x04 | 41 |
| 0x05 | 00 |
| 0x06 | 00 |
| 0x07 | 20 |
| 0x08 | 40 |
| 0x09 | 0A |
| 0x0A | D7 |
| 0x0B | 23 |
| 0x0C | 3B |
| 0x0D | 00 |
| 0x0E | 00 |
| 0x0F | 40 |
| 0x10 | 40 |
| 0x11 | FF |
| 0x12 | FF |
| 0x13 | FF |
| 0x14 | FF |
| 0x15 | FF |
| 0x16 | FF |
| 0x17 | FF |
| 0x18 | FF |
| 0x19 | FF |
| 0x1A | FF |
| 0x1B | FF |
| 0x1C | FF |
| 0x1D | FF |
| 0x1E | FF |
| 0x1F | FF |

<a id="table-calibration-description"></a>
### CALIBRATION_DESCRIPTION

Dimensions: 56 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x01 | TAC_COMPLETE_OK |
| 0x02 | TAC_OK |
| 0x03 | TAC_IMAGE |
| 0x04 | TAC_NO_TARGET |
| 0x05 | TAC_TARGET_OOR |
| 0x06 | TAC_INCONSISTENCY |
| 0x07 | TAC_PARAM_LIMIT |
| 0x08 | TAC_INTERNAL_ERROR |
| 0x09 | TAC_FINISH_OK |
| 0x0A | TAC_FINISH_ONGOING |
| 0x0B | TAC_FINISH_ERROR |
| 0x0C | TAC_INPUT_IMAGE_POINTER_IS_NULL |
| 0x0D | TAC_INPUT_FPNI_POINTER_IS_NULL |
| 0x0E | TAC_INPUT_FPNI_LOOKUP_TABLE_IS_NULL |
| 0x0F | TAC_INPUT_DISTANCE_VEHICLE_CENTER_LINE_OUT_OF_RANGE |
| 0x11 | TAC_INPUT_TARGET_WIDTH_OUT_OF_RANGE |
| 0x12 | TAC_INPUT_TARGET_FRONT_AXE_OUT_OF_RANGE |
| 0x13 | TAC_INPUT_UPPER_TARGETS_HEIGHT_OUT_OF_RANGE |
| 0x14 | TAC_INPUT_LOWER_TARGETS_HEIGHT_OUT_OF_RANGE |
| 0x15 | TAC_INPUT_SQUARE_SIZE_OUT_OF_RANGE |
| 0x16 | TAC_INPUT_DISTANCE_CAMERA_TO_TARGET_OUT_OF_RANGE |
| 0x17 | TAC_INPUT_CAMERA_CENTERLINE_OUT_OF_RANGE |
| 0x18 | TAC_RUN_ILLEGAL_CALL_SEQUENCE |
| 0x19 | TAC_RUN_RESULT_ROLL_ANGLE_TOO_LARGE |
| 0x1A | TAC_RUN_WRONG_DISTANCE |
| 0x1B | TAC_RUN_WRONG_HORIZONTAL_BOTTOM_TARGET_LOCATION |
| 0x1C | TAC_RUN_WRONG_VERTICAL_BOTTOM_TARGET_LOCATION |
| 0x1D | TAC_RUN_ROLL_ANGLE_DIFFERENTIAL_BETWEEN_FRAMES_TOO_LARGE |
| 0x1E | TAC_RUN_DISTANCE_OF_BOTTOM_IMAGES_DIFFERENT_THAN_DISTANCE_OF_TOP_IMAGES |
| 0x1F | TAC_RUN_RESULT_YAW_ANGLE_TOO_LARGE |
| 0x21 | TAC_RUN_RESULT_HORIZON_ANGLE_TOO_LARGE |
| 0x22 | TAC_PARAM_CAMERA_LEFT_WHEEL_DISTANCE_NOT_IN_RANGE |
| 0x23 | TAC_PARAM_CAMERA_RIGHT_WHEEL_DISTANCE_NOT_IN_RANGE |
| 0x24 | TAC_PARAM_CAMERA_HEIGHT_NOT_IN_RANGE |
| 0x25 | TAC_PARAM_CAMERA_CAR_FRONT_DISTANCE_NOT_IN_RANGE |
| 0x26 | TAC_PARAM_CAMERA_FOCAL_LENGTH_NOT_IN_RANGE |
| 0x27 | TAC_PARAM_WIDTH_CAMERA_IMAGE_ORIGINAL_NOT_IN_RANGE |
| 0x28 | TAC_PARAM_HEIGHT_CAMERA_IMAGE_ORIGINAL_NOT_IN_RANGE |
| 0x29 | TAC_PARAM_MAX_YAW_CALIBRATION_OUT_OF_RANGE |
| 0x2A | TAC_PARAM_MIN_HORIZON_CALIBRATION_OUT_OF_RANGE |
| 0x2B | TAC_PARAM_MAX_HORIZON_CALIBRATION_OUT_OF_RANGE |
| 0x2C | TAC_PARAM_MAX_ROLL_CALIBRATION_OUT_OF_RANGE |
| 0x2D | TAC_PARAM_FPNI_HEIGHT_NOT_IN_RANGE |
| 0x2E | TAC_PARAM_FPNI_WIDTH_NOT_IN_RANGE |
| 0x2F | TAC_PARAM_K1_DISTORTION_NOT_IN_RANGE |
| 0x31 | TAC_PARAM_K2_DISTORTION_NOT_IN_RANGE |
| 0x32 | TAC_PARAM_MAIN_POINT_X_DEVIATION_NOT_IN_RANGE |
| 0x33 | TAC_PARAM_MAIN_POINT_Y_DEVIATION_NOT_IN_RANGE |
| 0x34 | TAC_INIT_ILLEGAL_CALL_SEQUENCE |
| 0xE1 | TAC_NOT_AVAILABLE_(NOT INITIALIZED) |
| 0xE2 | ECU_NOT_CODED |
| 0xE3 | TAC_BUSY_(ALREADY_RUNNING) |
| 0xE4 | SPC_RUNNING |
| 0xE5 | EEPROM_ACCESS_FAILED |
| 0xE6 | uC_COMMUNICATION_FAILURE |
| xy | unplausibler Wert |

<a id="table-stat-cal-description"></a>
### STAT_CAL_DESCRIPTION

Dimensions: 6 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Blockagetest nicht gestartet, SPC(Service Point Calibration) nicht gestartet |
| 0x01 | Blockagetest aktiv, SPC nicht gestartet |
| 0x02 | Blockagetest erfolgreich beendet, SPC aktiv |
| 0x03 | Blockagetest erfolgreich beendet, SPC erfolgreich abgeschlossen |
| 0xFF | ungültig |
| xy | unplausibler Wert |

<a id="table-vnr-description"></a>
### VNR_DESCRIPTION

Dimensions: 9 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | B0 |
| 0x01 | C1 |
| 0x02 | C2 |
| 0x03 | C2_1 |
| 0x04 | C3 Labor |
| 0x06 | C3 default |
| 0x0A | C3 BMW |
| 0x0B | C4 BMW |
| xy | unplausibler Wert |
