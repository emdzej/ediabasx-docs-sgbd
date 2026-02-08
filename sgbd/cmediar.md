# cmediar.prg

- Jobs: [109](#jobs)
- Tables: [40](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Combox |
| ORIGIN | BMW EI-44 Hr.Mallinson |
| REVISION | 5.020 |
| AUTHOR | Harman/Becker EDSB1 GRichter, HaysAG EI44 Hr.Bubb |
| COMMENT | N/A |
| PACKAGE | 1.52 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [DIAGNOSEPROTOKOLL_LESEN](#job-diagnoseprotokoll-lesen) - Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück
- [DIAGNOSEPROTOKOLL_SETZEN](#job-diagnoseprotokoll-setzen) - Wählt ein Diagnoseprotokoll aus
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
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
- [STEUERN_BT](#job-steuern-bt) - KWP2000: $31   StartRoutineByLocalIdentifier $72   STEUERN_BT
- [STATUS_BT](#job-status-bt) - KWP2000: $33   RoutineResultsByLocalIdentifier $72   STATUS_BT
- [STEUERN_BT_ERKENNUNGSMODUS](#job-steuern-bt-erkennungsmodus) - KWP2000: $31   StartRoutineByLocalIdentifier $73   STEUERN_BT_ERKENNUNGSMODUS
- [STATUS_BT_ERKENNUNGSMODUS](#job-status-bt-erkennungsmodus) - KWP2000: $33   RoutineResultsByLocalIdentifier $73   STATUS_BT_ERKENNUNGSMODUS
- [STEUERN_BT_GERAETEADRESSE](#job-steuern-bt-geraeteadresse) - KWP2000: $3B   WriteDataByLocalIdentifier $79   STEUERN_BT_GERAETEADRESSE
- [STATUS_BT_GERAETEADRESSE](#job-status-bt-geraeteadresse) - KWP2000: $21		ReadDataByLocalIdentifier $79		STATUS_BT_GERAETEADRESSE
- [STEUERN_BT_PASSKEY](#job-steuern-bt-passkey) - KWP2000: $3B   WriteDataByLocalIdentifier $7A   STEUERN_BT_PASSKEY
- [STATUS_BT_PASSKEY](#job-status-bt-passkey) - KWP2000: $21		ReadDataByLocalIdentifier $7A		STATUS_BT_GERAETEADRESSE
- [STEUERN_BT_GERAETENAME](#job-steuern-bt-geraetename) - KWP2000: $3B   WriteDataByLocalIdentifier $7B   STEUERN_BT_GERAETENAME write BT Device Name
- [STATUS_BT_GERAETENAME](#job-status-bt-geraetename) - KWP2000: $21   ReadDataByLocalIdentifier $7B   STATUS_BT_GERAETENAME read BT Device Name
- [STATUS_BT_READ_PHONE_ID](#job-status-bt-read-phone-id) - Returns information about the phone selected as argument
- [STEUERN_BT_DELETE_ALL_PHONE_ID](#job-steuern-bt-delete-all-phone-id) - KWP2000: $31   StartRoutineByLocalIdentifier $74   Delete all Phone ID Delete all Mobile Information stored
- [STEUERN_RESET_TO_BASIC_STATE](#job-steuern-reset-to-basic-state) - KWP2000:$31   StartRoutineByLocalIdentifier $75   STEUERN_RESET_TO_BASIC_STATE Delete Personal information
- [STATUS_RESET_TO_BASIC_STATE](#job-status-reset-to-basic-state) - KWP2000:$33     RoutineResultsByLocalIdentifier $75     STATUS_RESET_TO_BASIC_STATE each byte has to say: 0x00 OK 0x01 Error occured (could not be deleted completelely) 0x02 Not Requested 0x03 Running
- [STATUS_VERSION_ID_LESEN](#job-status-version-id-lesen) - KWP2000: $21   ReadDataByLocalIdentifier $78   Status_Version_ID_Lesen
- [STATUS_SVK_LESEN](#job-status-svk-lesen) - KWP2000: $21   ReadDataByLocalIdentifier $FB   SVK_Lesen
- [STATUS_USB_HUB_TEST](#job-status-usb-hub-test) - KWP:     $21   ReadDataByLocalIdentifier $7E   STATUS_USB_HUB_TEST test if a hub is present on the first and second USB ports
- [STATUS_USB_TEST_TEL](#job-status-usb-test-tel) - KWP2000: $31   StartRoutineByLocalIdentifier $FB   systemSupplierSpecific $03   Layer03 $A06A Status USB Test
- [STEUERN_USB_TEST_TEL](#job-steuern-usb-test-tel) - KWP2000: $31   StartRoutineByLocalIdentifier $FB   systemSupplierSpecific $01   Layer01 $A06A Steuern USB Test
- [STEUERN_TEST_AUXVERBINDUNG](#job-steuern-test-auxverbindung) - KWP2000: $31 StartRoutineByLocalIdentifier $48 STEUERN_TEST_AUXVERBINDUNG
- [STEUERN_TEST_VERBAU_TEL](#job-steuern-test-verbau-tel) - KWP2000: $31 StartRoutineByLocalIdentifier $FB SYSTEM_SUPPLIER_SPECIFIC $01A050 STEUERN_TEST_VERBAU_TEL
- [STATUS_TEST_VERBAU_TEL](#job-status-test-verbau-tel) - KWP2000: $31     StartRoutineByLocalIdentifier $FB     SYSTEM_SUPPLIER_SPECIFIC $03A050 STATUS_TEST_VERBAU_TEL
- [STATUS_SELBSTTEST](#job-status-selbsttest) - KWP2000: $33   RoutineResultsByLocalIdentifie $04   STATUS_SELBSTTEST
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - KWP2000: $31   StartRoutineByLocalIdentifier $04   STATUS_SELBSTTEST
- [LESEN_DAS](#job-lesen-das) - KWP2000: $31       readDataByIdentifier $FB034000 LESEN_DAS Auslesen des Default Access Set (DAS)
- [STEUERN_LAST_CONNECTION_TEL](#job-steuern-last-connection-tel) - KWP2000: $3B   readDataByLocalIdentifier $FD   STEUERN_LAST_CONNECTION_TEL Auslesen des Status (SIM Status und IP Adresse) der letzte Verbindung
- [STATUS_LAST_CONNECTION_TEL](#job-status-last-connection-tel) - KWP2000: $21   readDataByLocalIdentifier $FD   Status_Last_Connection_Tel beschreibt Status der SIM Karte
- [STEUERN_PROVISIONING_TEL](#job-steuern-provisioning-tel) - KWP2000: $31   StartRoutineByLocalIdentifier $39   STEUERN_PROVISIONING_TEL startet einen provisioning request
- [STATUS_PROVISIONING_TEL](#job-status-provisioning-tel) - KWP2000: $33   RoutineResultsByLocalIdentifier $FA   STATUS_PROVISIONING_TEL Status des Provisionierungsprozess und Version von den Provisionierungsdaten
- [LESEN_CONFIG_INIT_VALUES](#job-lesen-config-init-values) - KWP2000: $31       readDataByIdentifier $FB034002 LESEN_CONFIG_INIT_VALUES
- [LESEN_DASVP](#job-lesen-dasvp) - KWP2000: $31                    readDataByIdentifier $FB034003      LESEN_DASVP Auslesen des Default Configuration Vehicle Profile
- [LESEN_CONTROL_LIST_MAINBOARD](#job-lesen-control-list-mainboard) - KWP2000: $22   readDataByIdentifier $F001 LESEN_CONTROL_LIST_MAINBOARD
- [SCHREIBEN_OTA](#job-schreiben-ota) - UDS:     $31   RoutineControl $FB   StatusRoutine $01   StartRoutine $4001 SCHREIBEN_OTA Dieser Job schreibt ein Over The Air (OTA) Datensatz
- [LESEN_OTA](#job-lesen-ota) - KWP2000: $31       readDataByIdentifier $FB034001 LESEN_OTA Auslesen vom Over The Air (OTA) Datensatz
- [LESEN_DPAS](#job-lesen-dpas) - KWP2000: $31       readDataByIdentifier $FB034004 LESEN_DPAS Der Job s liest eine Default Provisioning Access Configuration mit einem spezifizierten Index und schreibt das herunterladene XML File in dem eingegebene Pfad.
- [STEUERN_RESET_TO_DEFAULT_CONFIG](#job-steuern-reset-to-default-config) - KWP:     $31   RoutineControl $FB   UserDefined $01   StartRoutine $A052 STEUERN_RESET_TO_DEFAULT_CONFIG Setzt die standard Telematik Konfigurationswerte zurück und löscht die OTA (Over The Air) Daten
- [STATUS_RESET_TO_DEFAULT_CONFIG](#job-status-reset-to-default-config) - KWP:     $31   RoutineControl $FB   UserDefined $03   ResultRoutine $A052 STEUERN_RESET_TO_DEFAULT_CONFIG Setzt die standard Telematik Konfigurationswerte zurück
- [SCHREIBEN_BMW_ZERTIFIKATE](#job-schreiben-bmw-zertifikate) - KWP:     $31   RoutineControl $FB   SystemSupplierSpecific $01   StatusRoutine $A053 SCHREIBEN_BMW_ZERTIFIKATE
- [SCHREIBEN_BROWSER_ZERTIFIKATE](#job-schreiben-browser-zertifikate) - KWP:     $31   RoutineControl $FB   SystemSupplierSpecific $01   StatusRoutine $A054 SCHREIBEN_BROWSER_ZERTIFIKATE
- [STEUERN_REMOVE_CUSTOMER_UPDATES](#job-steuern-remove-customer-updates) - KWP2000: $31   StartRoutineByLocalIdentifier $78   STEUERN_REMOVE_CUSTOMER_UPDATES
- [STATUS_SWUP_INSTALLED](#job-status-swup-installed) - KWP2000: $21   	ReadDataByLocalIdentifier $76 		STATUS_SWUP_INSTALLED Auslesen des installierten Software Updates. Für jeden Eintrag werden Programmierdatum, Kilometerstand, Werte und Text der Prozessklasse des installierten Updates, SGBM ID und Version und Status des installierten Updates werden gespeichert.
- [STATUS_SWUP_INSTALLATION_HISTORY](#job-status-swup-installation-history) - KWP2000: $21 	ReadDataByLocalIdentifier $77 	STATUS_SWUP_INSTALLATION_HISTORY Auslesen der letzten Software Update Installationen. Für jeden Eintrag werden Zeit, Operationtype, SWIP ID, ECU SW VID und Operationcode gespeichert.
- [STATUS_USB_STACK_INFO_FOR_DEVICE](#job-status-usb-stack-info-for-device) - Reads out logistical information about the four last connected USB devices four last connected IPOD Players, four last connected MTP Players and four last unrecognized USB devices
- [STATUS_TEST_AUXVERBINDUNG](#job-status-test-auxverbindung) - Returns the results of the impedance measurement performed with steuern_test_aux_verbindung
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [STATUS_REMOTE_SERVICES_LOG](#job-status-remote-services-log) - STATUS_REMOTE_SERVICES_LOG KWP2000: $21 ReadDataByLocalIdentifier $75 recordLocalIdentifier Modus   : Default
- [STATUS_POWERMANAGEMENT_SH4](#job-status-powermanagement-sh4) - Auslesen der gespeicherten internen Powermanagement Transitionen 
- [STATUS_BT_GEKOPPELTE_GERAETE_LESEN](#job-status-bt-gekoppelte-geraete-lesen) - Returns the Bluetooth address of the four last connected devices
- [STATUS_TDA_AKTIVIERUNG](#job-status-tda-aktivierung) - Reads out the actual Baureihe of the Gateway table
- [STATUS_USB_STECKZYKLEN](#job-status-usb-steckzyklen) - Returns how many times a USB device has been plugged in the USB interface or in the snap in adapter
- [STEUERN_DELETE_A4A_STRING](#job-steuern-delete-a4a-string) - Reads out the actual Baureihe of the Gateway table
- [STATUS_DELETE_A4A_STRING](#job-status-delete-a4a-string) - This job shall return if the Protocol String com.bmw.a4a is present
- [STEUERN_TEST_ANTENNE_TEL](#job-steuern-test-antenne-tel) - Performs an impedance measurement of one, some or all antennas
- [STATUS_TEST_ANTENNE_TEL](#job-status-test-antenne-tel) - Returns the results of the impedance measurements performed with steuern_test_antenne_tel

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

<a id="job-fs-sperren"></a>
### FS_SPERREN

Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERREN | string | "ja"   -&gt; Fehlerspeicher sperren "nein" -&gt; Fehlerspeicher freigeben table DigitalArgument TEXT |
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

<a id="job-steuern-bt"></a>
### STEUERN_BT

KWP2000: $31   StartRoutineByLocalIdentifier $72   STEUERN_BT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_BT | char | 0x00 BT not activated 0x01 BT activated |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-bt"></a>
### STATUS_BT

KWP2000: $33   RoutineResultsByLocalIdentifier $72   STATUS_BT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BT | int | 0x00 BT not activated 0x01 BT activated |
| STAT_BT_TEXT | string | Bluetooth activation state value from table TBluetoothActivationState |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-steuern-bt-erkennungsmodus"></a>
### STEUERN_BT_ERKENNUNGSMODUS

KWP2000: $31   StartRoutineByLocalIdentifier $73   STEUERN_BT_ERKENNUNGSMODUS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_BT_ERKENNUNGSMODUS | char | 0x00 BT Discovery Mode off 0x01 BT Discovery Mode on |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-bt-erkennungsmodus"></a>
### STATUS_BT_ERKENNUNGSMODUS

KWP2000: $33   RoutineResultsByLocalIdentifier $73   STATUS_BT_ERKENNUNGSMODUS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BT_ERKENNUNGSMODUS | int | 0x00 BT Discovery Mode off 0x01 BT Discovery Mode on |
| STAT_BT_ERKENNUNGSMODUS_TEXT | string | Activation state of the Bluetooth discovery mode value from table TBtDiscoveryModeActivationState |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-steuern-bt-geraeteadresse"></a>
### STEUERN_BT_GERAETEADRESSE

KWP2000: $3B   WriteDataByLocalIdentifier $79   STEUERN_BT_GERAETEADRESSE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_BT_GERAETEADRESSE | string | Bereich: 0-255 bzw 0-0xFF 6 Byte BT Adresse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-bt-geraeteadresse"></a>
### STATUS_BT_GERAETEADRESSE

KWP2000: $21		ReadDataByLocalIdentifier $79		STATUS_BT_GERAETEADRESSE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BT_ADRESSE_WERT | string | Hex-respone from ECU |
| STAT_BT_ADRESSE_EINH | char | Hex-Einheit Ausgabe der 6 Byte Bluetooth (BT) Adresse in Hex |
| STAT_BT_ADRESSE | string | Bluetooth address (example: FE DC BA 98 76 54) |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-steuern-bt-passkey"></a>
### STEUERN_BT_PASSKEY

KWP2000: $3B   WriteDataByLocalIdentifier $7A   STEUERN_BT_PASSKEY

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_BT_PASSKEY | string | Bereich: 0-255 bzw 0-0xFF nullterminierter ASCIIstring_a : Passkey max. 16 digits coded in UTF-8 (max.16bytes) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-bt-passkey"></a>
### STATUS_BT_PASSKEY

KWP2000: $21		ReadDataByLocalIdentifier $7A		STATUS_BT_GERAETEADRESSE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BT_PASSKEY_WERT | string | Hex-respone from ECU |
| STAT_BT_PASSKEY_EINH | char | Hex-Einheit nullterminierter ASCIIstring_a : Passkey max. 16 digits coded in UTF-8 (max.16bytes) |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-steuern-bt-geraetename"></a>
### STEUERN_BT_GERAETENAME

KWP2000: $3B   WriteDataByLocalIdentifier $7B   STEUERN_BT_GERAETENAME write BT Device Name

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_BT_GERAETENAME | string | BT User Friendly Name String up to 18 Bytes nullterminiert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-bt-geraetename"></a>
### STATUS_BT_GERAETENAME

KWP2000: $21   ReadDataByLocalIdentifier $7B   STATUS_BT_GERAETENAME read BT Device Name

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BT_GERAETENAME | string | Bluetooth device name |
| STAT_BT_GERAETENAME_WERT | string | Hex-respone from ECU |
| STAT_BT_GERAETENAME_EINH | char | Hex-Einheit String up to 18 Bytes nullterminiert |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-bt-read-phone-id"></a>
### STATUS_BT_READ_PHONE_ID

Returns information about the phone selected as argument

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_EINTRAG_NR | unsigned char | Phone from which the information must be read out (possible values: 1, 2, 3 and 4) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_P_KM_READING_AT_LAST_RECONNECT | unsigned long | Mileage at the last reconnect of the phone selected as argument |
| STAT_P_NO_OF_RECONNECTS | unsigned int | Number of reconnects of the phone selected as argument |
| STAT_P_PHONE_MODEL_TRUNC_RAWDATA | string | Phone model as raw data |
| STAT_P_PHONE_SOFTWARE_TRUNC_RAWDATA | string | Phone software as raw data |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bt-delete-all-phone-id"></a>
### STEUERN_BT_DELETE_ALL_PHONE_ID

KWP2000: $31   StartRoutineByLocalIdentifier $74   Delete all Phone ID Delete all Mobile Information stored

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-steuern-reset-to-basic-state"></a>
### STEUERN_RESET_TO_BASIC_STATE

KWP2000:$31   StartRoutineByLocalIdentifier $75   STEUERN_RESET_TO_BASIC_STATE Delete Personal information

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DATA_TO_RESET | unsigned long | delete Personal Information as specified 0x00000000 alle 0x00000001 - list of paired devices call lists voice tags (inclusive phonebooks) 0x00000002 - Emails 0x00000004 - SMS 0x00000008 - Music lists 0x00000010 - PIM 0x00000020- …XX (FOR future use) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-reset-to-basic-state"></a>
### STATUS_RESET_TO_BASIC_STATE

KWP2000:$33     RoutineResultsByLocalIdentifier $75     STATUS_RESET_TO_BASIC_STATE each byte has to say: 0x00 OK 0x01 Error occured (could not be deleted completelely) 0x02 Not Requested 0x03 Running

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_JOB_RESULT | unsigned char | Status des kompletten Jobs |
| STAT_PAIRED_DEVICE_DELETED | unsigned char | Status, ob die verbundene Geräte gelöscht wurden |
| STAT_EMAIL_DELETED | unsigned char | Status, ob die Emails gelöscht wurden |
| STAT_SMS_DELETED | unsigned char | Status, ob die SMSs gelöscht wurden |
| STAT_MUSIC_LIST_DELETED | unsigned char | Status, ob die Musik Listen gelöscht wurden |
| STAT_PIM_DELETED | unsigned char | Status, ob PIM gelöscht wurden |

<a id="job-status-version-id-lesen"></a>
### STATUS_VERSION_ID_LESEN

KWP2000: $21   ReadDataByLocalIdentifier $78   Status_Version_ID_Lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_VIN | string | Fahrgestellnummer |
| STAT_HARDWARE_LIEFERUNG | string | ID der Hardwarelieferung |
| STAT_SOFTWARE_LIEFERUNG | string | ID der Softwarelieferung |
| STAT_ECU_SW_VID | string | Ecu Swup ID |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-svk-lesen"></a>
### STATUS_SVK_LESEN

KWP2000: $21   ReadDataByLocalIdentifier $FB   SVK_Lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL_EINHEITEN | int | Anzahl der xWEn |
| STAT_PROZESSKLASSE_WERT | int | dezimale Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_EINH | string | Einheit der dezimalen Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_TEXT | string | Text-Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_KURZTEXT | string | Text-Angabe des Prozessklassenkurztextes |
| STAT_SGBM_IDENTIFIER | string | Angabe SGBM-ID der Prozessklasse |
| STAT_VERSION | string | Angabe der Version der Prozessklasse |
| STAT_SGBM_ID | string | Angabe von Prozessklasse, SGBM-Identifier, Version |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-usb-hub-test"></a>
### STATUS_USB_HUB_TEST

KWP:     $21   ReadDataByLocalIdentifier $7E   STATUS_USB_HUB_TEST test if a hub is present on the first and second USB ports

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_USB_HUB_TEST1 | unsigned char | 0xyy is the result of the test for the first USB port: 0x00 HUB angeschlossen 0x01 HUB nicht angeschlosesen 0x04 HUB auscodiert, keine HUB Prüfung else: Keine Diagnose durchfuehrbar |
| STAT_USB_HUB_TEST2 | unsigned char | 0xzz is the result of the test for the first USB port: 0x00 HUB angeschlossen 0x01 HUB nicht angeschlosesen 0x04 HUB auscodiert, keine HUB Prüfung else: Keine Diagnose durchfuehrbar |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-usb-test-tel"></a>
### STATUS_USB_TEST_TEL

KWP2000: $31   StartRoutineByLocalIdentifier $FB   systemSupplierSpecific $03   Layer03 $A06A Status USB Test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_USB_TEST_TEL_KDZ | unsigned char | Ergebnis des USB Schnittstelle Tests 0x00 Kein Gerät angeschlossen 0x01 Gerät angeschlossen, Erkennung läuft 0x02 Gerät erkannt aber falsche ID 0x03 Gerät angeschlossen und richtige ID 0xFE Gerät angeschlossen aber kein Massenspeicher 0xFF Nicht definiert |
| STAT_VENDORID_INT_TEL_KDZ_WERT | binary | Hier wird die vorgegebene VendorID von STEUERN_USB_TEST_TEL für das Gerät von der USB Schnittstelle ausgegeben ACHTUNG: Rückgabe erfolgt als vierstelliger Hex-String ohne 0x vorangestellt BEISPIEL: A1FB |
| STAT_PRODUCTID_INT_TEL_KDZ_WERT | binary | Hier wird die vorgegebene ProductID von STEUERN_USB_TEST_TEL für das Gerät von der USB Schnittstelle ausgegeben ACHTUNG: Rückgabe erfolgt als vierstelliger Hex-String ohne 0x vorangestellt BEISPIEL: A1FB |
| STAT_VENDORID_REC_TEL_KDZ_WERT | binary | Hier wird die erkannte VendorID des Gerätes von der USB Schnittstelle ausgegeben ACHTUNG: Rückgabe erfolgt als vierstelliger Hex-String ohne 0x vorangestellt BEISPIEL: A1FB |
| STAT_PRODUCTID_REC_TEL_KDZ_WERT | binary | Hier wird die erkannte ProductID des Gerätes von der USB Schnittstelle ausgegeben ACHTUNG: Rückgabe erfolgt als vierstelliger Hex-String ohne 0x vorangestellt BEISPIEL: A1FB |
| STAT_VENDORSTRING_KDZ_REC_WERT | string | Hier wird der erkannte VendorString des Gerätes von der USB Schnittstelle ausgegeben ACHTUNG: Rückgabe erfolgt als String |
| STAT_USB_TEST_TEL_SIA | unsigned char | Ergebnis des Snap In Adpater Tests 0x00 Kein Gerät angeschlossen 0x01 Gerät angeschlossen, Erkennung läuft 0x02 Gerät erkannt aber falsche ID 0x03 Gerät angeschlossen und richtige ID 0xFE Gerät angeschlossen aber kein Massenspeicher 0xFF Nicht definiert |
| STAT_VENDORID_INT_TEL_SIA_WERT | binary | Hier wird die vorgegebene VendorID von STEUERN_USB_TEST_TEL für das Telefon vom Snap In Adapter ausgegeben ACHTUNG: Rückgabe erfolgt als vierstelliger Hex-String ohne 0x vorangestellt BEISPIEL: A1FB |
| STAT_PRODUCTID_INT_TEL_SIA_WERT | binary | Hier wird die vorgegebene ProductID von STEUERN_USB_TEST_TEL für das Telefon vom Snap In Adapter ausgegeben ACHTUNG: Rückgabe erfolgt als vierstelliger Hex-String ohne 0x vorangestellt BEISPIEL: A1FB |
| STAT_VENDORID_REC_TEL_SIA_WERT | binary | Hier wird die erkannte VendorID des Gerätes vom Snap In Adapter ausgegeben ACHTUNG: Rückgabe erfolgt als vierstelliger Hex-String ohne 0x vorangestellt BEISPIEL: A1FB |
| STAT_PRODUCTID_REC_TEL_SIA_WERT | binary | Hier wird die erkannte ProductID des Gerätes vom Snap In Adapter ausgegeben ACHTUNG: Rückgabe erfolgt als vierstelliger Hex-String ohne 0x vorangestellt BEISPIEL: A1FB |
| STAT_VENDORSTRING_SIA_REC_WERT | string | Hier wird der erkannte VendorString für das Gerätes vom Snap In Adapter ausgegeben ACHTUNG: Rückgabe erfolgt als String |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-steuern-usb-test-tel"></a>
### STEUERN_USB_TEST_TEL

KWP2000: $31   StartRoutineByLocalIdentifier $FB   systemSupplierSpecific $01   Layer01 $A06A Steuern USB Test

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_VENDOR_ID_KDZ | string | Vendor ID des USB Device am Kundenzugang z.B. F2E3 |
| ARG_PRODUCT_ID_KDZ | string | Prudukt ID des USB Device am Kundenzugang z.B. A1AB |
| ARG_VENDOR_ID_SIA | string | Vendor ID des USB Device am Snap-In Adapter z.B. F2E3 |
| ARG_PRODUCT_ID_SIA | string | Produkt ID des USB Device am Snap-In Adapter z.B. A1AB |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-steuern-test-auxverbindung"></a>
### STEUERN_TEST_AUXVERBINDUNG

KWP2000: $31 StartRoutineByLocalIdentifier $48 STEUERN_TEST_AUXVERBINDUNG

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_VERBINDUNG | unsigned int | number of connection |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-steuern-test-verbau-tel"></a>
### STEUERN_TEST_VERBAU_TEL

KWP2000: $31 StartRoutineByLocalIdentifier $FB SYSTEM_SUPPLIER_SPECIFIC $01A050 STEUERN_TEST_VERBAU_TEL

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_VERBAU_ROUTINE | unsigned long | tested device number |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-test-verbau-tel"></a>
### STATUS_TEST_VERBAU_TEL

KWP2000: $31     StartRoutineByLocalIdentifier $FB     SYSTEM_SUPPLIER_SPECIFIC $03A050 STATUS_TEST_VERBAU_TEL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERBAU_ROUTINE | unsigned long | kind of device |
| STAT_VERBAU_ROUTINE_TEXT | unsigned char | kind of device |
| STAT_TEST_VERBAU_TEXT | string | result text |
| STAT_TEST_VERBAU | unsigned char | Status of test |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-selbsttest"></a>
### STATUS_SELBSTTEST

KWP2000: $33   RoutineResultsByLocalIdentifie $04   STATUS_SELBSTTEST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_SELBSTTEST_ROUTINE | string | Ergebnis Test |
| STAT_SELBSTTEST | unsigned int | Ergebnis Test |
| STAT_SELBSTTEST_TEXT | string | Ergebnis Test |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

KWP2000: $31   StartRoutineByLocalIdentifier $04   STATUS_SELBSTTEST

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SELBSTTEST_ROUTINE | unsigned long | Testroutin wich will be started 0x00000000 alle Selbstestroutinen 0x00000001 Flash Checksummenpruefung 0x00000002 INIC BuildIn-Test 0x00000004 USB 0x00000008 FPGA 0x00000010 Bluetooth Chip 0x00000020 DRM Chip |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-lesen-das"></a>
### LESEN_DAS

KWP2000: $31       readDataByIdentifier $FB034000 LESEN_DAS Auslesen des Default Access Set (DAS)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SMNC | string | Mobile Network Code von der SIM Karte, z.B: T-Online hat den Code 001 |
| ARG_SMCC | string | Mobile Country Code von der SIM Karte, z.B: Deutschland hat den Code 262 |
| ARG_NMNC | string | Mobile Network Code vom Netz, z.B: T-Online hat den Code 001 |
| ARG_NMCC | string | Mobile Country Code vom Netz, z.B: Deutschland hat den Code 262 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_DAS | binary | liest DAS daten |

<a id="job-steuern-last-connection-tel"></a>
### STEUERN_LAST_CONNECTION_TEL

KWP2000: $3B   readDataByLocalIdentifier $FD   STEUERN_LAST_CONNECTION_TEL Auslesen des Status (SIM Status und IP Adresse) der letzte Verbindung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DEVICE | string | beschreibt welches Gerät für das die letze Verbindung abgefragt wird. 1: Bluetooth Telefon 2: interne NAD Modul |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-last-connection-tel"></a>
### STATUS_LAST_CONNECTION_TEL

KWP2000: $21   readDataByLocalIdentifier $FD   Status_Last_Connection_Tel beschreibt Status der SIM Karte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_SIM_STATUS | int | SIM Status 0x0: not Registered and not searching (nicht eingebucht, sucht kein Netz) 0x1: registered (eingebucht) 0x2: not registered and searching (nicht eingebucht und sucht ein Netz) 0x3: registration denied (einbuchen verweigert) 0x4: registered and roaming (eingebucht und roaming) 0x5: registered and roaming off-net (eingebucht und roaming off-net) |
| STAT_IP_ADRESSE | string | IP Adresse, Bsp: 192.168.0.1 |

<a id="job-steuern-provisioning-tel"></a>
### STEUERN_PROVISIONING_TEL

KWP2000: $31   StartRoutineByLocalIdentifier $39   STEUERN_PROVISIONING_TEL startet einen provisioning request

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-provisioning-tel"></a>
### STATUS_PROVISIONING_TEL

KWP2000: $33   RoutineResultsByLocalIdentifier $FA   STATUS_PROVISIONING_TEL Status des Provisionierungsprozess und Version von den Provisionierungsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_PROVISIONING | int | Provisioning status as integer Integer values from table TProvisioningStatus 0 UNKNOWN - unbekannt 1 ACTIVE – läuft noch 2 SUCCESS – alles OK 3 FAILED – mit Fehler beendet 4 IDLE – wurde nicht gestartet |
| STAT_PROVISIONING_TEXT | string | Provisioning status as text |

<a id="job-lesen-config-init-values"></a>
### LESEN_CONFIG_INIT_VALUES

KWP2000: $31       readDataByIdentifier $FB034002 LESEN_CONFIG_INIT_VALUES

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_CONFIG_INIT_VALUES | binary | Lesen init Values |

<a id="job-lesen-dasvp"></a>
### LESEN_DASVP

KWP2000: $31                    readDataByIdentifier $FB034003      LESEN_DASVP Auslesen des Default Configuration Vehicle Profile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_DASVP | binary | DASVP daten |

<a id="job-lesen-control-list-mainboard"></a>
### LESEN_CONTROL_LIST_MAINBOARD

KWP2000: $22   readDataByIdentifier $F001 LESEN_CONTROL_LIST_MAINBOARD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_CONTROL_LIST_MAINBOARD | binary | LESEN_CONTROL_LIST_MAINBOARD daten |

<a id="job-schreiben-ota"></a>
### SCHREIBEN_OTA

UDS:     $31   RoutineControl $FB   StatusRoutine $01   StartRoutine $4001 SCHREIBEN_OTA Dieser Job schreibt ein Over The Air (OTA) Datensatz

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_PFAD | string | Pfad |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-lesen-ota"></a>
### LESEN_OTA

KWP2000: $31       readDataByIdentifier $FB034001 LESEN_OTA Auslesen vom Over The Air (OTA) Datensatz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_OTA | binary | LESEN_OTA daten |

<a id="job-lesen-dpas"></a>
### LESEN_DPAS

KWP2000: $31       readDataByIdentifier $FB034004 LESEN_DPAS Der Job s liest eine Default Provisioning Access Configuration mit einem spezifizierten Index und schreibt das herunterladene XML File in dem eingegebene Pfad.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_LESEN_DPAS | string | LESEN_DPAS daten |

<a id="job-steuern-reset-to-default-config"></a>
### STEUERN_RESET_TO_DEFAULT_CONFIG

KWP:     $31   RoutineControl $FB   UserDefined $01   StartRoutine $A052 STEUERN_RESET_TO_DEFAULT_CONFIG Setzt die standard Telematik Konfigurationswerte zurück und löscht die OTA (Over The Air) Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-reset-to-default-config"></a>
### STATUS_RESET_TO_DEFAULT_CONFIG

KWP:     $31   RoutineControl $FB   UserDefined $03   ResultRoutine $A052 STEUERN_RESET_TO_DEFAULT_CONFIG Setzt die standard Telematik Konfigurationswerte zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_RESET_TO_DEFAULT_CONFIG | int | Unknown           = 0x00 Active            = 0x01 Success           = 0x02 Failed            = 0x03 Idle              = 0x04 |
| STAT_RESET_TO_DEFAULT_CONFIG_TEXT | string | Ergebniss Test Reset status as text String values from table TResetStatus |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-schreiben-bmw-zertifikate"></a>
### SCHREIBEN_BMW_ZERTIFIKATE

KWP:     $31   RoutineControl $FB   SystemSupplierSpecific $01   StatusRoutine $A053 SCHREIBEN_BMW_ZERTIFIKATE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_PFAD | string | Pfad |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-schreiben-browser-zertifikate"></a>
### SCHREIBEN_BROWSER_ZERTIFIKATE

KWP:     $31   RoutineControl $FB   SystemSupplierSpecific $01   StatusRoutine $A054 SCHREIBEN_BROWSER_ZERTIFIKATE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_PFAD | string | Pfad |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-steuern-remove-customer-updates"></a>
### STEUERN_REMOVE_CUSTOMER_UPDATES

KWP2000: $31   StartRoutineByLocalIdentifier $78   STEUERN_REMOVE_CUSTOMER_UPDATES

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_REMOVE_CUSTOMER_UDPATES | unsigned char | result of the job Removes all customer updates. Restores clean I-Stage |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-swup-installed"></a>
### STATUS_SWUP_INSTALLED

KWP2000: $21   	ReadDataByLocalIdentifier $76 		STATUS_SWUP_INSTALLED Auslesen des installierten Software Updates. Für jeden Eintrag werden Programmierdatum, Kilometerstand, Werte und Text der Prozessklasse des installierten Updates, SGBM ID und Version und Status des installierten Updates werden gespeichert.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_ANZAHL_SWUP | int | Anzahl der SWUP |
| STAT_SWUP_INSTALLED | string | Sind SWUP Pakete installiert |
| STAT_FREI_FLASHSPEICHER | unsigned long | Freier Flashspeicher |
| STAT_FREI_FLASHSPEICHER_EINH | string | Einhiet für Freier Flashspeicher |
| STAT_PROG_DATUM | string | Programmierdatum (DD.MM.YY) |
| STAT_PROG_KM | long | KM-Stand bei Programmierung (10 KM bis 655350 KM) Inkrement sind 10 KM -1: KM-Stand wird nicht unterstuetzt |
| STAT_PROZESSKLASSE_WERT | int | table Prozessklasse WERT dezimale Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_EINH | string | Einheit der dezimale Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_TEXT | string | table Prozessklasse BEZEICHNUNG Text-Angabe der Prozessklasse |
| STAT_SGBM_IDENTIFIER | string | Angabe SGBM-ID der Prozessklasse |
| STAT_VERSION | string | Angabe der Version der Prozessklasse |
| STAT_ACTIVATION_STATUS | char | 0x00: SWUP inaktiv, 0x01: SWUP aktiv |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respones from ECU |

<a id="job-status-swup-installation-history"></a>
### STATUS_SWUP_INSTALLATION_HISTORY

KWP2000: $21 	ReadDataByLocalIdentifier $77 	STATUS_SWUP_INSTALLATION_HISTORY Auslesen der letzten Software Update Installationen. Für jeden Eintrag werden Zeit, Operationtype, SWIP ID, ECU SW VID und Operationcode gespeichert.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| STAT_HISTORY_1_KILOMETER_WERT | unsigned long | Kilometerstand bei der Operation 1. Historyeintrag |
| STAT_HISTORY_1_KILOMETER_EINH | string | Einheit km |
| STAT_HISTORY_2_KILOMETER_WERT | unsigned long | Kilometerstand bei der Operation 2. Historyeintrag |
| STAT_HISTORY_2_KILOMETER_EINH | string | Einheit km |
| STAT_HISTORY_3_KILOMETER_WERT | unsigned long | Kilometerstand bei der Operation 3. Historyeintrag |
| STAT_HISTORY_3_KILOMETER_EINH | string | Einheit km |
| STAT_HISTORY_4_KILOMETER_WERT | unsigned long | Kilometerstand bei der Operation 4. Historyeintrag |
| STAT_HISTORY_4_KILOMETER_EINH | string | Einheit km |
| STAT_HISTORY_5_KILOMETER_WERT | unsigned long | Kilometerstand bei der Operation 5. Historyeintrag |
| STAT_HISTORY_5_KILOMETER_EINH | string | Einheit km |
| STAT_HISTORY_6_KILOMETER_WERT | unsigned long | Kilometerstand bei der Operation 6. Historyeintrag |
| STAT_HISTORY_6_KILOMETER_EINH | string | Einheit km |
| STAT_HISTORY_7_KILOMETER_WERT | unsigned long | Kilometerstand bei der Operation 7. Historyeintrag |
| STAT_HISTORY_7_KILOMETER_EINH | string | Einheit km |
| STAT_HISTORY_8_KILOMETER_WERT | unsigned long | Kilometerstand bei der Operation 8. Historyeintrag |
| STAT_HISTORY_8_KILOMETER_EINH | string | Einheit km |
| STAT_HISTORY_1_ZEIT_WERT | string | Datum und Zeit YYYY-MM-DD_HH:MM 1. Historyeintrag |
| STAT_HISTORY_1_ZEIT_EINH | string | Einheit des Zeiteintrags |
| STAT_HISTORY_2_ZEIT_WERT | string | Datum und Zeit YYYY-MM-DD_HH:MM 2. Historyeintrag |
| STAT_HISTORY_2_ZEIT_EINH | string | Einheit des Zeiteintrags |
| STAT_HISTORY_3_ZEIT_WERT | string | Datum und Zeit YYYY-MM-DD_HH:MM 3. Historyeintrag |
| STAT_HISTORY_3_ZEIT_EINH | string | Einheit des Zeiteintrags |
| STAT_HISTORY_4_ZEIT_WERT | string | Datum und Zeit YYYY-MM-DD_HH:MM 4. Historyeintrag |
| STAT_HISTORY_4_ZEIT_EINH | string | Einheit des Zeiteintrags |
| STAT_HISTORY_5_ZEIT_WERT | string | Datum und Zeit YYYY-MM-DD_HH:MM 5. Historyeintrag |
| STAT_HISTORY_5_ZEIT_EINH | string | Einheit des Zeiteintrags |
| STAT_HISTORY_6_ZEIT_WERT | string | Datum und Zeit YYYY-MM-DD_HH:MM 6. Historyeintrag |
| STAT_HISTORY_6_ZEIT_EINH | string | Einheit des Zeiteintrags |
| STAT_HISTORY_7_ZEIT_WERT | string | Datum und Zeit YYYY-MM-DD_HH:MM 7. Historyeintrag |
| STAT_HISTORY_7_ZEIT_EINH | string | Einheit des Zeiteintrags |
| STAT_HISTORY_8_ZEIT_WERT | string | Datum und Zeit YYYY-MM-DD_HH:MM 8. Historyeintrag |
| STAT_HISTORY_8_ZEIT_EINH | string | Einheit des Zeiteintrags |
| STAT_HISTORY_1_TYP | unsigned char | Typ der Operation 1. Historyeintrag |
| STAT_HISTORY_2_TYP | unsigned char | Typ der Operation 2. Historyeintrag |
| STAT_HISTORY_3_TYP | unsigned char | Typ der Operation 3. Historyeintrag |
| STAT_HISTORY_4_TYP | unsigned char | Typ der Operation 4. Historyeintrag |
| STAT_HISTORY_5_TYP | unsigned char | Typ der Operation 5. Historyeintrag |
| STAT_HISTORY_6_TYP | unsigned char | Typ der Operation 6. Historyeintrag |
| STAT_HISTORY_7_TYP | unsigned char | Typ der Operation 7. Historyeintrag |
| STAT_HISTORY_8_TYP | unsigned char | Typ der Operation 8. Historyeintrag |
| STAT_HISTORY_1_SGBM_IDENTIFIER_WERT | string | Angabe SGBM-ID der Prozessklasse 1. Historyeintrag |
| STAT_HISTORY_1_SGBM_IDENTIFIER_EINH | string | Einheit der Prozessklasse |
| STAT_HISTORY_2_SGBM_IDENTIFIER_WERT | string | Angabe SGBM-ID der Prozessklasse 2. Historyeintrag |
| STAT_HISTORY_2_SGBM_IDENTIFIER_EINH | string | Einheit der Prozessklasse |
| STAT_HISTORY_3_SGBM_IDENTIFIER_WERT | string | Angabe SGBM-ID der Prozessklasse 3. Historyeintrag |
| STAT_HISTORY_3_SGBM_IDENTIFIER_EINH | string | Einheit der Prozessklasse |
| STAT_HISTORY_4_SGBM_IDENTIFIER_WERT | string | Angabe SGBM-ID der Prozessklasse 4. Historyeintrag |
| STAT_HISTORY_4_SGBM_IDENTIFIER_EINH | string | Einheit der Prozessklasse |
| STAT_HISTORY_5_SGBM_IDENTIFIER_WERT | string | Angabe SGBM-ID der Prozessklasse 5. Historyeintrag |
| STAT_HISTORY_5_SGBM_IDENTIFIER_EINH | string | Einheit der Prozessklasse |
| STAT_HISTORY_6_SGBM_IDENTIFIER_WERT | string | Angabe SGBM-ID der Prozessklasse 6. Historyeintrag |
| STAT_HISTORY_6_SGBM_IDENTIFIER_EINH | string | Einheit der Prozessklasse |
| STAT_HISTORY_7_SGBM_IDENTIFIER_WERT | string | Angabe SGBM-ID der Prozessklasse 7. Historyeintrag |
| STAT_HISTORY_7_SGBM_IDENTIFIER_EINH | string | Einheit der Prozessklasse |
| STAT_HISTORY_8_SGBM_IDENTIFIER_WERT | string | Angabe SGBM-ID der Prozessklasse 8. Historyeintrag |
| STAT_HISTORY_8_SGBM_IDENTIFIER_EINH | string | Einheit der Prozessklasse |
| STAT_HISTORY_1_SWIP_VERSION_WERT | string | Angabe der Version der Prozessklasse 1. Historyeintrag |
| STAT_HISTORY_1_SWIP_VERSION_EINH | string | Einheit der Version der Prozessklasse |
| STAT_HISTORY_2_SWIP_VERSION_WERT | string | Angabe der Version der Prozessklasse 2. Historyeintrag |
| STAT_HISTORY_2_SWIP_VERSION_EINH | string | Einheit der Version der Prozessklasse |
| STAT_HISTORY_3_SWIP_VERSION_WERT | string | Angabe der Version der Prozessklasse 3. Historyeintrag |
| STAT_HISTORY_3_SWIP_VERSION_EINH | string | Einheit der Version der Prozessklasse |
| STAT_HISTORY_4_SWIP_VERSION_WERT | string | Angabe der Version der Prozessklasse 4. Historyeintrag |
| STAT_HISTORY_4_SWIP_VERSION_EINH | string | Einheit der Version der Prozessklasse |
| STAT_HISTORY_5_SWIP_VERSION_WERT | string | Angabe der Version der Prozessklasse 5. Historyeintrag |
| STAT_HISTORY_5_SWIP_VERSION_EINH | string | Einheit der Version der Prozessklasse |
| STAT_HISTORY_6_SWIP_VERSION_WERT | string | Angabe der Version der Prozessklasse 6. Historyeintrag |
| STAT_HISTORY_6_SWIP_VERSION_EINH | string | Einheit der Version der Prozessklasse |
| STAT_HISTORY_7_SWIP_VERSION_WERT | string | Angabe der Version der Prozessklasse 7. Historyeintrag |
| STAT_HISTORY_7_SWIP_VERSION_EINH | string | Einheit der Version der Prozessklasse |
| STAT_HISTORY_8_SWIP_VERSION_WERT | string | Angabe der Version der Prozessklasse 8. Historyeintrag |
| STAT_HISTORY_8_SWIP_VERSION_EINH | string | Einheit der Version der Prozessklasse |
| STAT_HISTORY_1_NEW_SW_VID_WERT | string | Neue Steuergeräte Software Version ID 1. Historyeintrag |
| STAT_HISTORY_1_NEW_SW_VID_EINH | string | Einheit der Software Version ID |
| STAT_HISTORY_2_NEW_SW_VID_WERT | string | Neue Steuergeräte Software Version ID 2. Historyeintrag |
| STAT_HISTORY_2_NEW_SW_VID_EINH | string | Einheit der Software Version ID |
| STAT_HISTORY_3_NEW_SW_VID_WERT | string | Neue Steuergeräte Software Version ID 3. Historyeintrag |
| STAT_HISTORY_3_NEW_SW_VID_EINH | string | Einheit der Software Version ID |
| STAT_HISTORY_4_NEW_SW_VID_WERT | string | Neue Steuergeräte Software Version ID 4. Historyeintrag |
| STAT_HISTORY_4_NEW_SW_VID_EINH | string | Einheit der Software Version ID |
| STAT_HISTORY_5_NEW_SW_VID_WERT | string | Neue Steuergeräte Software Version ID 5. Historyeintrag |
| STAT_HISTORY_5_NEW_SW_VID_EINH | string | Einheit der Software Version ID |
| STAT_HISTORY_6_NEW_SW_VID_WERT | string | Neue Steuergeräte Software Version ID 6. Historyeintrag |
| STAT_HISTORY_6_NEW_SW_VID_EINH | string | Einheit der Software Version ID |
| STAT_HISTORY_7_NEW_SW_VID_WERT | string | Neue Steuergeräte Software Version ID 7. Historyeintrag |
| STAT_HISTORY_7_NEW_SW_VID_EINH | string | Einheit der Software Version ID |
| STAT_HISTORY_8_NEW_SW_VID_WERT | string | Neue Steuergeräte Software Version ID 8. Historyeintrag |
| STAT_HISTORY_8_NEW_SW_VID_EINH | string | Einheit der Software Version ID |
| STAT_HISTORY_1_FLASHSPEICHER_WERT | string | Freier Flashspeicher, der nach dem 1. History-Update zur Verfügung steht |
| STAT_HISTORY_1_FLASHSPEICHER_EINH | string | Einheit der Flashspeichers |
| STAT_HISTORY_2_FLASHSPEICHER_WERT | string | Freier Flashspeicher, der nach dem 2. History-Update zur Verfügung steht |
| STAT_HISTORY_2_FLASHSPEICHER_EINH | string | Einheit der Flashspeichers |
| STAT_HISTORY_3_FLASHSPEICHER_WERT | string | Freier Flashspeicher, der nach dem 3. History-Update zur Verfügung steht |
| STAT_HISTORY_3_FLASHSPEICHER_EINH | string | Einheit der Flashspeichers |
| STAT_HISTORY_4_FLASHSPEICHER_WERT | string | Freier Flashspeicher, der nach dem 4. History-Update zur Verfügung steht |
| STAT_HISTORY_4_FLASHSPEICHER_EINH | string | Einheit der Flashspeichers |
| STAT_HISTORY_5_FLASHSPEICHER_WERT | string | Freier Flashspeicher, der nach dem 5. History-Update zur Verfügung steht |
| STAT_HISTORY_5_FLASHSPEICHER_EINH | string | Einheit der Flashspeichers |
| STAT_HISTORY_6_FLASHSPEICHER_WERT | string | Freier Flashspeicher, der nach dem 6. History-Update zur Verfügung steht |
| STAT_HISTORY_6_FLASHSPEICHER_EINH | string | Einheit der Flashspeichers |
| STAT_HISTORY_7_FLASHSPEICHER_WERT | string | Freier Flashspeicher, der nach dem 7. History-Update zur Verfügung steht |
| STAT_HISTORY_7_FLASHSPEICHER_EINH | string | Einheit der Flashspeichers |
| STAT_HISTORY_8_FLASHSPEICHER_WERT | string | Freier Flashspeicher, der nach dem 8. History-Update zur Verfügung steht |
| STAT_HISTORY_8_FLASHSPEICHER_EINH | string | Einheit der Flashspeichers |
| STAT_HISTORY_1_ERROR_CODE | unsigned char | Software Update Fehlercode 1. Historyeintrag |
| STAT_HISTORY_2_ERROR_CODE | unsigned char | Software Update Fehlercode 2. Historyeintrag |
| STAT_HISTORY_3_ERROR_CODE | unsigned char | Software Update Fehlercode 3. Historyeintrag |
| STAT_HISTORY_4_ERROR_CODE | unsigned char | Software Update Fehlercode 4. Historyeintrag |
| STAT_HISTORY_5_ERROR_CODE | unsigned char | Software Update Fehlercode 5. Historyeintrag |
| STAT_HISTORY_6_ERROR_CODE | unsigned char | Software Update Fehlercode 6. Historyeintrag |
| STAT_HISTORY_7_ERROR_CODE | unsigned char | Software Update Fehlercode 7. Historyeintrag |
| STAT_HISTORY_8_ERROR_CODE | unsigned char | Software Update Fehlercode 8. Historyeintrag |
| _TEL_AUFTRAG | binary | Hex-request to ECU |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-usb-stack-info-for-device"></a>
### STATUS_USB_STACK_INFO_FOR_DEVICE

Reads out logistical information about the four last connected USB devices four last connected IPOD Players, four last connected MTP Players and four last unrecognized USB devices

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TYPE | unsigned char | UMS-type of requested Info 0x01 USB Stick 0x02 IPOD 0x03 MTP Player 0x04 UNKNOWN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_1_VENDORID_WERT | string | Vendor ID |
| STAT_1_PRODUCTID_WERT | string | Product ID |
| STAT_1_CLASSID_WERT | string | Class ID |
| STAT_1_SUBCLASSID_WERT | string | Subclass ID |
| STAT_1_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_1_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_1_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_1_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_1_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_1_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_1_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_1_USED_PORT | unsigned char | Port Info |
| STAT_2_VENDORID_WERT | string | Vendor ID |
| STAT_2_PRODUCTID_WERT | string | Product ID |
| STAT_2_CLASSID_WERT | string | Vendor ID |
| STAT_2_SUBCLASSID_WERT | string | Product ID |
| STAT_2_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_2_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_2_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_2_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_2_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_2_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_2_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_2_USED_PORT | unsigned char | Port Info |
| STAT_3_VENDORID_WERT | string | Vendor ID |
| STAT_3_PRODUCTID_WERT | string | Product ID |
| STAT_3_CLASSID_WERT | string | Vendor ID |
| STAT_3_SUBCLASSID_WERT | string | Product ID |
| STAT_3_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_3_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_3_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_3_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_3_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_3_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_3_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_3_USED_PORT | unsigned char | Port Info |
| STAT_4_VENDORID_WERT | string | Vendor ID |
| STAT_4_PRODUCTID_WERT | string | Product ID |
| STAT_4_CLASSID_WERT | string | Vendor ID |
| STAT_4_SUBCLASSID_WERT | string | Product ID |
| STAT_4_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_4_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_4_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_4_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_4_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_4_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_4_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_4_USED_PORT | unsigned char | Port Info |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-daten from ECU |

<a id="job-status-test-auxverbindung"></a>
### STATUS_TEST_AUXVERBINDUNG

Returns the results of the impedance measurement performed with steuern_test_aux_verbindung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERBINDUNG | unsigned int | Aux connection that has been tested Values from table TAuxVerbindung |
| STAT_TEST_AUXVERBINDUNG | unsigned char | Status of the test as integer Integer values from table TTestStatus |
| STAT_TEST_AUXVERBINDUNG_TEXT | string | Status of the test as text Integer values from table TTestStatus |
| STAT_ANZAHL_FEHLERHAFTE_VERBINDUNGEN_WERT | unsigned char | Number of the faulty aux connections |
| STAT_FEHLER_1_VERBINDUNG | unsigned int | Xth faulty connection values from table TAuxVerbindung |
| STAT_FEHLER_1_VERBINDUNG_TEXT | string | Xth faulty connection values from table TAuxVerbindung |
| STAT_FEHLER_1_FEHLERART_VERBINDUNG | unsigned char | Type of error values from table TVerbindungFehlerArt |
| STAT_FEHLER_1_FEHLERART_VERBINDUNG_TEXT | string | Type of error values from table TVerbindungFehlerArt |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
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

<a id="job-status-remote-services-log"></a>
### STATUS_REMOTE_SERVICES_LOG

STATUS_REMOTE_SERVICES_LOG KWP2000: $21 ReadDataByLocalIdentifier $75 recordLocalIdentifier Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_NUMBER_OF_ENTRIES | unsigned int | Number of entries registered in log |
| STAT_APPLICATION_ID | unsigned char | ID of the Remote Service ID stored at position X from the table TRemoteServices |
| STAT_APPLICATION_ID_TEXT | string | ID of the Remote Service ID stored at position X from the table TRemoteServices |
| STAT_SEND_TIME | string | Time when the trigger was received (DD/MM/YYYY hh:mm:ss) |
| STAT_EXEC_TIME | string | Time when the Application Remote Service sent the message on MOST |
| STAT_DOORS_STATUS | unsigned char | Status of the doors (only for Remote Door Services) from the table TDoorsStatus |
| STAT_DOORS_STATUS_TEXT | string | Status of the doors (only for Remote Door Services) from the table TDoorsStatus |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-powermanagement-sh4"></a>
### STATUS_POWERMANAGEMENT_SH4

Auslesen der gespeicherten internen Powermanagement Transitionen 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DATASET | unsigned char | Dataset number requested Index starts with 0x01 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_TEXT | string | values from table TPowerState |
| STAT_EVENT_TEXT | string | values from table TPowerEvent |
| STAT_TIMESTAMP | string | Timestamp as hex string |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-daten from ECU |

<a id="job-status-bt-gekoppelte-geraete-lesen"></a>
### STATUS_BT_GEKOPPELTE_GERAETE_LESEN

Returns the Bluetooth address of the four last connected devices

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BT_ADR_DEV_1 | string | Bluetooth address (example: FE DC BA 98 76 54) |
| STAT_BT_ADR_DEV_2 | string | Bluetooth address (example: FE DC BA 98 76 55) |
| STAT_BT_ADR_DEV_3 | string | Bluetooth address (example: FE DC BA 98 76 56) |
| STAT_BT_ADR_DEV_4 | string | Bluetooth address (example: FE DC BA 98 76 57) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tda-aktivierung"></a>
### STATUS_TDA_AKTIVIERUNG

Reads out the actual Baureihe of the Gateway table

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TDA | unsigned char | Returns the status of activation of BMW services by the user xx values from table TDAActivationState |
| STAT_TDA_TEXT | string | Returns the status of activation of BMW services by the user xx values from table TDAActivationState |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-usb-steckzyklen"></a>
### STATUS_USB_STECKZYKLEN

Returns how many times a USB device has been plugged in the USB interface or in the snap in adapter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_USB_KDZ_WERT | unsigned long | Number of connection over the USB interface |
| STAT_USB_SIA_WERT | unsigned long | Number of connection over the SIA interface |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-delete-a4a-string"></a>
### STEUERN_DELETE_A4A_STRING

Reads out the actual Baureihe of the Gateway table

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-delete-a4a-string"></a>
### STATUS_DELETE_A4A_STRING

This job shall return if the Protocol String com.bmw.a4a is present

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEST | unsigned char | 0x00	String present 0x01	String not present |
| STAT_TEST_TEXT | string | Status of the string is present or not |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-test-antenne-tel"></a>
### STEUERN_TEST_ANTENNE_TEL

Performs an impedance measurement of one, some or all antennas

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ANTENNE | unsigned long | Bitcombination of antennas to be tested values from table TAntenneCMEDIA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-test-antenne-tel"></a>
### STATUS_TEST_ANTENNE_TEL

Returns the results of the impedance measurements performed with steuern_test_antenne_tel

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANTENNE | unsigned long | Antennas that have been tested values from table TAntenneCMEDIA |
| STAT_ANTENNE_TEXT | string | Antenna that have been tested Values from table TAntenneCMEDIA |
| STAT_TEST_ANTENNE | unsigned char | Status of the test values from table TTestStatus |
| STAT_TEST_ANTENNE_TEXT | string | Status of the test values from table TTestStatus |
| STAT_ANZAHL_FEHLERHAFTE_ANTENNEN_WERT | unsigned char | Number of the faulty antennas  In the following you see only first antenna the other results STAT_FEHLER_2-16_... are created dynamically |
| STAT_FEHLER_1_ANTENNE | unsigned long | faulty antenna values from table TAntenneCMEDIA |
| STAT_FEHLER_1_ANTENNE_TEXT | string | faulty antenna values from table TAntenneCMEDIA |
| STAT_FEHLER_1_FEHLERART_ANTENNE | unsigned char | Type of error values from table TAntenneFehlerArt |
| STAT_FEHLER_1_FEHLERART_ANTENNE_TEXT | string | Type of error values from table TAntenneFehlerArt |
| STAT_FEHLER_1_MESSWERT_WIDERSTAND_WERT | unsigned int | impedance value measured 0x0001 = 0.1 kOhm, Max possible value: 0xC350 = 5 MOhm If the exact value cannot be returned, the value 0xFFFF is returned |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (121 × 2)
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
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (3 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (8 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (10 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (10 × 9)
- [FORTTEXTE](#table-forttexte) (32 × 2)
- [IORTTEXTE](#table-iorttexte) (65 × 2)
- [TTESTSTATUS](#table-tteststatus) (6 × 2)
- [TVERBAUROUTINETEL](#table-tverbauroutinetel) (7 × 2)
- [TAUXVERBINDUNG](#table-tauxverbindung) (10 × 2)
- [TANTENNECMEDIA](#table-tantennecmedia) (3 × 2)
- [TANTENNEFEHLERART](#table-tantennefehlerart) (5 × 2)
- [TVERBINDUNGFEHLERART](#table-tverbindungfehlerart) (4 × 2)
- [TREMOTESERVICES](#table-tremoteservices) (4 × 2)
- [TDOORSSTATUS](#table-tdoorsstatus) (3 × 2)
- [TBLUETOOTHACTIVATIONSTATE](#table-tbluetoothactivationstate) (3 × 2)
- [TBTDISCOVERYMODEACTIVATIONSTATE](#table-tbtdiscoverymodeactivationstate) (3 × 2)
- [TPERSONALPHONEDATA](#table-tpersonalphonedata) (6 × 2)
- [THUBCONNECTIONSTATE](#table-thubconnectionstate) (4 × 2)
- [TDAACTIVATIONSTATE](#table-tdaactivationstate) (5 × 2)
- [TA4ASTRINGSTATUS](#table-ta4astringstatus) (3 × 2)
- [TPOWERSTATE](#table-tpowerstate) (7 × 2)
- [TPOWEREVENT](#table-tpowerevent) (23 × 2)

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

Dimensions: 121 rows × 2 columns

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

Dimensions: 3 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xD690 | 0x06 | - | - | - |
| 0xA8FA | 0x170C | - | - | - |
| default | - | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 8 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Logische-Knotenadresse | Hex | high | unsigned int | - | - | - | - |
| 0x02 | FBlockID | Hex | -- | unsigned char | - | - | - | - |
| 0x03 | InstID | Hex | -- | unsigned char | - | - | - | - |
| 0x04 | FktID | Hex | high | unsigned int | - | - | - | - |
| 0x05 | Diagnoseadresse | Hex | -- | unsigned char | - | - | - | - |
| 0x06 | NPR | Hex | -- | unsigned char | - | - | - | - |
| 0x170C | Versorgungsspannung am Eingang des SG | mV | high | unsigned int | - | - | - | - |
| 0xFF | unbekannte Umweltbedingung | 1 | -- | unsigned char | - | - | - | - |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
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

Dimensions: 10 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xA8EA | 0x05 | - | - | - |
| 0xA8FC | 0x06 | - | - | - |
| 0xA8FD | 0x06 | - | - | - |
| 0xA8FF | 0x06 | - | - | - |
| 0x9312 | 0x170C | - | - | - |
| 0x930B | 0x1709 | - | - | - |
| 0xA80D | 0xF003 | - | - | - |
| 0xA80E | 0xF003 | - | - | - |
| 0xA80F | 0xF003 | - | - | - |
| default | - | - | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 10 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Zieladresse | Hex | high | unsigned int | - | - | - | - |
| 0x02 | FBlockID | Hex | -- | unsigned char | - | - | - | - |
| 0x03 | InstID | Hex | -- | unsigned char | - | - | - | - |
| 0x04 | FktID | Hex | high | unsigned int | - | - | - | - |
| 0x05 | Speicheradresse  | Hex | high | signed long | - | - | - | - |
| 0x06 | BT Adresse | text | - | 6 | - | - | - | - |
| 0x170C | Versorgungsspannung am Eingang des SG | mV | high | unsigned int | - | - | - | - |
| 0x1709 | MOST Message Header | text | - | 6 | - | - | - | - |
| 0xF003 | Spannung am Eingang des Mikrophons | mV | high | unsigned int | - | - | - | - |
| 0xFF | unbekannte Umweltbedingung | 1 | -- | unsigned char | - | - | - | - |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 32 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0236 | Energiesparmode aktiv |
| 0xA369 | Flash Speicher Fehler |
| 0xA36A | INIC PCode Fehler |
| 0xA36B | DRM Chip Fehler |
| 0xA36C | USB Chip Fehler |
| 0xA36D | Ethernet Chip Fehler |
| 0xA36E | FPGA Fehler |
| 0xA36F | BlueCore Chip Fehler |
| 0xACC8 | KISU: Speicher oder Filesystem defekt |
| 0xACC9 | KISU: Inkonsistenter System Status |
| 0xACD7 | Unspezifierter Systemdefekt oder inkonsistenter Systemstatus |
| 0xD68E | Obwohl Shutdown (Execute) geschickt wurde, ging das Licht nicht aus |
| 0xD690 | MOST: Ringbruch |
| 0xD691 | Lange und/oder häufige Unlocks |
| 0xD692 | Sender- Empfängerbaustein (FOT): Temperatur übersteigt kritische Schwelle |
| 0xA8F9 | Software Reset: Überwachungsschaltung hat Reset ausgelöst |
| 0xA8EE | Mikrofon 1: Kurzschluss nach Masse |
| 0xA8F6 | AUX-Verbindung rechts: Kurzschluss nach Masse |
| 0xA8F8 | AUX-Verbindung links: Kurzschluss nach Masse |
| 0xA8F7 | AUX-Verbindung links: Kurzschluss nach Plus |
| 0xA8F5 | AUX-Verbindung rechts: Kurzschluss nach Plus |
| 0xA8F3 | Bluetooth-Antenne: Kurzschluss nach Plus |
| 0xA8ED | Mikrofon 1: Kurzschluss nach Plus |
| 0xA8EC | Hardware Reset |
| 0xA8F4 | Bluetooth-Antenne: Unterbrechung |
| 0xA371 | KISU: Deinstallation nach mehrfachem Reset |
| 0xA8EF | Mikrofon 1: Unterbrechung |
| 0xA8FA | Überspannung |
| 0xA8FB | ungültige Bluetoothadresse |
| 0xA900 | USB-Anschluss: Abschaltung wegen Überlastung |
| 0xA901 | Snap-in-Adapter (USB-Anschluss): Abschaltung wegen Überlastung |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 65 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA8E8 | INIC Memory Error |
| 0xA8E9 | Passwort Fehler: Passwort wurde drei mal falsch eingegeben |
| 0xA8EA | HBHK Daten wurden wieder hergestellt |
| 0xA8EB | Filesystem Fehler: Filesystem wurde wieder hergestellt |
| 0xABE9 | Fahrzeug steht nicht |
| 0xABEA | Update Abbruch |
| 0xABEB | MOST Kommunikationsfehler |
| 0xABEC | SWUP Zielplattform antwortet nicht |
| 0xABED | Gerät ausgelastet |
| 0xABF7 | Unspezifizierter Umwelt-Fehler |
| 0xABF8 | Neueste Version schon installiert |
| 0xABF9 | SWUP Package Container veraltet |
| 0xAC07 | Unspezifizierter Versions-Fehler |
| 0xAC08 | Neue I-Stufe nötig |
| 0xAC09 | SWUP - Zielgerät nicht verfügbar |
| 0xAC0A | Abhängigkeiten nicht erfüllt |
| 0xAC0B | Betroffene SWE nicht gefunden |
| 0xAC0C | Pre-Installation Skripte Fehler |
| 0xAC0D | Post-Installation Skripte Fehler |
| 0xAC0E | Fahrgestellnummer stimmt nicht |
| 0xAC17 | Unspezifizierbarer Fehler: Updatekompatibiliät |
| 0xAC18 | SWUP Weiterleitung nicht unterstützt |
| 0xAC19 | Nicht genug RAM |
| 0xAC1A | Nicht genug Flashspeicher |
| 0xAC1B | System überlastet |
| 0xAC1C | SWUP-Paket zu groß |
| 0xAC27 | Unspezifizierbarer Fehler: Ressourcebeschränkungen |
| 0xAC28 | SWIP Signaturverifikation fehlgeschlagen |
| 0xAC29 | SWIP XML-Datei korrupt |
| 0xAC2A | SWUP Hash Value stimmt nicht |
| 0xAC2B | SGBM korrupt oder unerwartetes Format |
| 0xAC2C | SWUP Signaturverifikation fehlgeschlagen |
| 0xAC37 | Unspezifizierter Fehler: Integrität oder Authentisierung |
| 0xAC38 | SWUP Download abgebrochen |
| 0xAC47 | Unspezifizierter Over-The-Air-Fehler |
| 0xAC48 | Keine Deinstallationinformationen verfügbar |
| 0xAC49 | Pre-Deinstallation Skripte Fehler |
| 0xAC4A | Post-Deinstallation Skripte Fehler |
| 0xAC57 | Unspezifierter Deinstallationfehler |
| 0xAC58 | Keine Update-Datei verfügbar |
| 0xAC59 | Update läuft |
| 0xAC5A | USB Gerät nicht angeschlossen |
| 0xAC67 | Unspezifierter Betriebsystemfehler |
| 0xACE7 | Unspezifizierter Fehler |
| 0x930A | MOST: Licht geht unerwartet aus |
| 0x930B | Anfragendes Device bekommt keine Antwort obwohl Partner vorhanden ist |
| 0x930C | Kurze Unlocks |
| 0x930D | Systemzustand Ok nicht fristgerecht erkannt |
| 0x9310 | Empfängerknoten: hat Nachricht nicht abgenommen; Puffer voll |
| 0x9311 | Keine Fahrzeug VIN vom Bus erhalten |
| 0x9312 | Versorgungsspannung: Mindestwert unterschritten |
| 0xA8FC | BT Linkloss |
| 0xA8FD | DisconnectByDeviceDriver |
| 0xA8FE | InvalidBTAddressOfConnectedDevice |
| 0xA8FF | IdleCatching |
| 0xA80D | Mikrofon 1: Kurzschluss nach Plus |
| 0xA80E | Mikrofon 1: Kurzschluss nach Masse |
| 0xA80F | Mikrofon 1: Unterbrechung |
| 0xAC1D | KISU SWUP Paket oder SWIP Datei Weiterleitung fehlgeschlagen. |
| 0xAC1E | KISU Angefordertes SWUP Paket nicht verfügbar. |
| 0xAC39 | KISU Keine Verbindung für Over-The-Air Update. |
| 0xAC68 | KISU Angefordertes SWUP Paket via Teleservice Update nicht verfügbar. |
| 0xAC69 | KISU SWUP Paket oder SWIP Datei zu groß für die Übertragung via Teleservice Update. |
| 0xAC77 | KISU Unspezifizierter Teleservice Fehler. |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-tteststatus"></a>
### TTESTSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test nicht gestartet |
| 0x01 | Test läuft |
| 0x02 | Test beendet ohne Fehler |
| 0x03 | Test beendet mit Fehlern |
| 0x04 | Test unterbrochen |
| 0xFF | Nicht definiert |

<a id="table-tverbauroutinetel"></a>
### TVERBAUROUTINETEL

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Routinen |
| 0x00000001 | Bluetooth |
| 0x00000008 | Ethernet |
| 0x00000010 | AuxIn |
| 0x00000020 | Microphone1 |
| 0x00000040 | Microphone2 |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-tauxverbindung"></a>
### TAUXVERBINDUNG

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Alle Aux Verbindungen |
| 0x0001 | Aux In Audio |
| 0x0100 | Aux In RSE links |
| 0x0200 | Aux In RSE rechts |
| 0x0300 | Aux In RSE links und rechts |
| 0x0400 | Aux In RSE BMW Individual |
| 0x0500 | Aux In RSE links und BMW Individual |
| 0x0600 | Aux In RSE rechts und BMW Individual |
| 0x0700 | Aux In RSE links, rechts und BMW Individual |
| 0xFFFF | Nicht definiert |

<a id="table-tantennecmedia"></a>
### TANTENNECMEDIA

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Antennen |
| 0x00000001 | Bluetooth Antenne |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-tantennefehlerart"></a>
### TANTENNEFEHLERART

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzschluss nach Plus |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Leitungsunterbrechung |
| 0x03 | Falscher Antennfu&#223; oder Diversity |
| 0xFF | Nicht definiert |

<a id="table-tverbindungfehlerart"></a>
### TVERBINDUNGFEHLERART

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzschluss nach Plus |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Leitungsunterbrechung |
| 0xFF | Nicht definiert |

<a id="table-tremoteservices"></a>
### TREMOTESERVICES

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Remote Door (Lock or Unlock) |
| 0x01 | Remote Climate Control |
| 0x02 | Vehicle Finder (incl. Flash Light and / or Horn Blow) |
| 0xFF | Nicht definiert |

<a id="table-tdoorsstatus"></a>
### TDOORSSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | at least one door is not locked |
| 0x01 | all doors inclusive tailgate |
| 0xFF | Nicht definiert |

<a id="table-tbluetoothactivationstate"></a>
### TBLUETOOTHACTIVATIONSTATE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | not activated |
| 0x01 | activated |
| 0xFF | Nicht definiert |

<a id="table-tbtdiscoverymodeactivationstate"></a>
### TBTDISCOVERYMODEACTIVATIONSTATE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | discovery mode off |
| 0x01 | discovery mode on |
| 0xFF | Nicht definiert |

<a id="table-tpersonalphonedata"></a>
### TPERSONALPHONEDATA

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | alle |
| 0x00000001 | list of paired devices (including call lists & voice tags) |
| 0x00000002 | Emails |
| 0x00000004 | SMS |
| 0x00000008 | Music lists (that were built by USB/MTP/iPod audio players) |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-thubconnectionstate"></a>
### THUBCONNECTIONSTATE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | HUB connected |
| 0x01 | HUB not connected |
| 0x04 | HUB not coded |
| 0xFF | Nicht definiert |

<a id="table-tdaactivationstate"></a>
### TDAACTIVATIONSTATE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | idle, not active yet |
| 0x02 | activation in progress |
| 0x03 | activation failed |
| 0x04 | activation successful |
| 0xFF | Nicht definiert |

<a id="table-ta4astringstatus"></a>
### TA4ASTRINGSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | String present |
| 0x01 | String not present |
| 0xFF | Nicht definiert |

<a id="table-tpowerstate"></a>
### TPOWERSTATE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Default; This state should never be logged |
| 0x01 | Sleepmode |
| 0x02 | Bus Active (Normal Operation, light on) |
| 0x03 | Local Active (Normal Operation, light off) |
| 0x04 | Shut-Down |
| 0x05 | Start-Up |
| 0xFF | Nicht definiert |

<a id="table-tpowerevent"></a>
### TPOWEREVENT

Dimensions: 23 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | No change |
| 0x01 | Most Light on |
| 0x02 | Most Light off |
| 0x03 | RST received |
| 0x04 | Sleepmode command received |
| 0x07 | Start-Up OK (First-Switch-To-Power) |
| 0x08 | Timeout |
| 0x09 | Temperature Shut-Down (Over Temperature detected) |
| 0x0A | Under voltage detected |
| 0x0B | Shutdown.Query Received |
| 0x0C | Clamp Off |
| 0x14 | SW Reset |
| 0x15 | Request by Coding (Diagnostic reset) |
| 0x16 | Watchdog Reset |
| 0x28 | Request Subnetwork |
| 0x29 | Telematic active |
| 0x2A | Telematic inactive |
| 0x2B | Phone Call active |
| 0x2C | Phone Call inactive |
| 0x3C | Shut-Down Reclaiming started |
| 0x3D | Shut-Down Reclaiming stopped |
| 0x3E | Shut-Down interrupted (Light On during Shut-Down) |
| 0xFF | Nicht definiert |
