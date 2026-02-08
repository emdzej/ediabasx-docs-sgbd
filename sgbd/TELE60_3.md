# TELE60_3.PRG

- Jobs: [136](#jobs)
- Tables: [28](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | TCU 1.5 (Telematic Control Unit) |
| ORIGIN | BMW_Group EI-43 Dr. Gengenbach |
| REVISION | 1.312 |
| AUTHOR | Motorola Inc. ? M.Manns, BMW Group EI-43 T.Kiefer |
| COMMENT | N/A |
| PACKAGE | 1.31 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
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
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
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
- [TCU_TYPE_LESEN](#job-tcu-type-lesen) - Reads the TCU Type KWP2000: $22 ReadDataByCommonIdentifier $A009 recordCommonIdentifier Modus  : Default
- [NVM_INIT](#job-nvm-init) - Initialise NVM Data KWP2000: $31 StartRoutineByLocalId $FB NVM Initialise Modus  : Default
- [US_SID_NID_SCHREIBEN](#job-us-sid-nid-schreiben) - Writes multiple SID & NID values into NAD (ONLY US!) KWP2000: $2E WriteDataByCommonId $A118 SID/NID Modus  : Default
- [US_SID_NID_LESEN](#job-us-sid-nid-lesen) - Reads SID & NID (16 Bytes (including NULL)) KWP2000: $22 ReadDataByCommonIdentifier $A118 recordCommonIdentifier Modus  : Default
- [US_CDMA_PRIMARY_CH_A_SCHREIBEN](#job-us-cdma-primary-ch-a-schreiben) - Reads CDMA Primary Channel A (Only US!) KWP2000: $2E WriteDataByCommonId $A119 CDMA Primary Channel A Modus  : Default
- [US_CDMA_PRIMARY_CH_A_LESEN](#job-us-cdma-primary-ch-a-lesen) - Reads CDMA Primary Channel A (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A119 recordCommonIdentifier Modus  : Default
- [US_CDMA_SECONDARY_CH_A_SCHREIBEN](#job-us-cdma-secondary-ch-a-schreiben) - CM-42 ESN CDMA Secondary Channel A KWP2000: $2E WriteDataByCommonId $A11A CDMA Secondary Channel A Modus  : Default
- [US_CDMA_SECONDARY_CH_A_LESEN](#job-us-cdma-secondary-ch-a-lesen) - Reads CDMA Secondary Channel A (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A11A recordCommonIdentifier Modus  : Default
- [US_CDMA_PRIMARY_CH_B_SCHREIBEN](#job-us-cdma-primary-ch-b-schreiben) - Writes CDMA Primary Channel B into NAD (Only US!) KWP2000: $2E WriteDataByCommonId $A11B CDMA Primary Channel B Modus  : Default
- [US_CDMA_PRIMARY_CH_B_LESEN](#job-us-cdma-primary-ch-b-lesen) - Reads CDMA Primary Channel B (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A11B recordCommonIdentifier Modus  : Default
- [US_CDMA_SECONDARY_CH_B_SCHREIBEN](#job-us-cdma-secondary-ch-b-schreiben) - Writes CDMA Secondary Channel B (Only US!) KWP2000: $2E WriteDataByCommonId $A11C CDMA Secondary Channel B Modus  : Default
- [US_CDMA_SECONDARY_CH_B_LESEN](#job-us-cdma-secondary-ch-b-lesen) - Reads CDMA Secondary Channel B (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A11C recordCommonIdentifier Modus  : Default
- [US_AMPS_SID_SCHREIBEN](#job-us-amps-sid-schreiben) - Writes AMPS Home SID (Only US!) KWP2000: $2E WriteDataByCommonId $A11D AMPS Home SID Modus  : Default
- [US_AMPS_SID_LESEN](#job-us-amps-sid-lesen) - Reads AMPS SID (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A11D recordCommonIdentifier Modus  : Default
- [US_AMPS_PAGING_CH_SCHREIBEN](#job-us-amps-paging-ch-schreiben) - Writes AMPS Paging Channel KWP2000: $2E WriteDataByCommonId $A11E AMPS Paging Channel Modus  : Default
- [US_AMPS_PAGING_CH_LESEN](#job-us-amps-paging-ch-lesen) - Reads AMPS Paging Channel (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A11E recordCommonIdentifier Modus  : Default
- [US_A_B_SIDE_SCHREIBEN](#job-us-a-b-side-schreiben) - Sets channel A or B (Only US!) KWP2000: $2E WriteDataByCommonId $A11F RecordCommonId Modus  : Default
- [STATUS_GPS](#job-status-gps) - Status des GPS wird ausgegeben KWP2000:$21 ReadDataByLocalIdentifier $02 recordLocalIdentifier Modus  : Default
- [ECALL_DISABLE](#job-ecall-disable) - Disables eCall possibility KWP2000: $2E WriteDataByCommonId $A124 recordCommonIdentifier Modus  : Default
- [ECALL_ENABLE](#job-ecall-enable) - Enables eCall possibility KWP2000: $2E WriteDataByCommonId $A124 recordCommonIdentifier Modus  : Default
- [STATUS_ECALL](#job-status-ecall) - Reads out ecall status KWP2000: $22 ReadDataByCommonIdentifier $A124 recordCommonIdentifier Modus  : Default
- [HW_SELBSTTEST](#job-hw-selbsttest) - Starts HW selftest of ECU Tested modules: BT module GPS module NAD Flash ROM SDRAM KWP2000: $31 startRoutineByLocalIdentifier $04 routineLocalIdentifier (selfTest) Modus  : Default
- [STATUS_HW_SELBSTTEST](#job-status-hw-selbsttest) - Reads the result of the hardware selftest KWP2000: $22 ReadDataByCommonIdentifier $A013 recordCommonIdentifier Modus  : Default
- [STATUS_ECU_CONNECTIONS](#job-status-ecu-connections) - Test of eCall button+LED, Backup Antenna, Main Antenna, Microphone 1+2 and Backup-Loudspeaker KWP2000: $2E WriteDataByCommonId $A013 RecordCommonId Modus  : Default
- [NAD_INFORMATION](#job-nad-information) - Get information about the current NAD Activity KWP2000: $22 ReadDataByCommonIdentifier $A032 recordCommonIdentifier Modus  : Default
- [US_STATUS_HOME_ONLY](#job-us-status-home-only) - Reads "Home Only" Status KWP2000: $22 ReadDataByCommonIdentifier $A11F recordCommonIdentifier Modus  : Default
- [US_HOME_ONLY_DISABLE](#job-us-home-only-disable) - Disables "Home Only" and enables Roaming KWP2000: $2E WriteDataByCommonId $A11F recordCommonIdentifier Modus  : Default
- [US_HOME_ONLY_ENABLE](#job-us-home-only-enable) - Enables "Home Only" and disables Roaming KWP2000: $2E WriteDataByCommonId $A11F recordCommonIdentifier Modus  : Default
- [US_STATUS_CAR_PHONE](#job-us-status-car-phone) - Reads out status of internal car phone KWP2000: $22 ReadDataByCommonIdentifier $A106 recordCommonIdentifier Modus  : Default
- [US_DISABLE_CAR_PHONE](#job-us-disable-car-phone) - Disables Car Phone KWP2000: $2E WriteDataByCommonId $A106 recordCommonIdentifier Modus  : Default
- [US_ENABLE_CAR_PHONE](#job-us-enable-car-phone) - Enables Car Phone KWP2000: $2E WriteDataByCommonId $A106 recordCommonIdentifier Modus  : Default
- [EMERG_NO_LESEN](#job-emerg-no-lesen) - Reads Backup Emergency Number KWP2000: $22 ReadDataByCommonIdentifier $A108 recordCommonIdentifier Modus  : Default
- [EMERG_NO_SCHREIBEN](#job-emerg-no-schreiben) - Writes Emergency Number KWP2000: $2E writeDataByCommonIdentifier $A108 recordCommonIdentifier Modus  : Default
- [HOTLINE_NO_LESEN](#job-hotline-no-lesen) - Reads Hotline Number KWP2000: $22 ReadDataByCommonIdentifier $A123 recordCommonIdentifier Modus  : Default
- [HOTLINE_NO_SCHREIBEN](#job-hotline-no-schreiben) - Writes Hotline Number KWP2000: $2E writeDataByCommonIdentifier $A123 recordCommonIdentifier Modus  : Default
- [BREAKDOWN_NO_LESEN](#job-breakdown-no-lesen) - Reads Breakdown Number KWP2000: $22 ReadDataByCommonIdentifier $A122 recordCommonIdentifier Modus  : Default
- [BREAKDOWN_NO_SCHREIBEN](#job-breakdown-no-schreiben) - Writes BMW Breakdown Number KWP2000: $2E writeDataByCommonIdentifier $A122 recordCommonIdentifier Modus  : Default
- [DEALER_NO_LESEN](#job-dealer-no-lesen) - Reads BMW Home Dealer Number KWP2000: $22 ReadDataByCommonIdentifier $A121 recordCommonIdentifier Modus  : Default
- [DEALER_NO_SCHREIBEN](#job-dealer-no-schreiben) - Writes BMW HOME Dealer Number KWP2000: $2E writeDataByCommonIdentifier $A121 recordCommonIdentifier Modus  : Default
- [GATS_SMSC_NO_LESEN](#job-gats-smsc-no-lesen) - Reads GATS SMSC Number KWP2000: $22 ReadDataByCommonIdentifier $A109 recordCommonIdentifier Modus  : Default
- [GATS_SMSC_NO_SCHREIBEN](#job-gats-smsc-no-schreiben) - Writes GATS SMCS Number KWP2000: $2E writeDataByCommonIdentifier $A109 recordCommonIdentifier Modus  : Default
- [GATS_PROVIDER_NO_LESEN](#job-gats-provider-no-lesen) - Reads GATS Provider Nuber KWP2000: $22 ReadDataByCommonIdentifier $A10A recordCommonIdentifier Modus  : Default
- [GATS_PROVIDER_NO_SCHREIBEN](#job-gats-provider-no-schreiben) - Writes GATS Provider No KWP2000: $2E writeDataByCommonIdentifier $A10A recordCommonIdentifier Modus  : Default
- [STATUS_NON_TELEMATIC_ECALL](#job-status-non-telematic-ecall) - Reads status of non-telematic eCall (Coding Bit) KWP2000: $22 ReadDataByCommonIdentifier $A104 recordCommonIdentifier Modus  : Default
- [STATUS_TELEMATICS_SERVICES](#job-status-telematics-services) - Reads status of telematic coding bit KWP2000: $22 ReadDataByCommonIdentifier $A103 recordCommonIdentifier Modus  : Default
- [STATUS_IO_PORT_PINS](#job-status-io-port-pins) - TCU I/O Port Pins KWP2000: $22 ReadDataByCommonIdentifier $A010 RecordCommonId Modus  : Default
- [ECE_SPRACHKONFIGURATION](#job-ece-sprachkonfiguration) - starts language configuration (Argument = 0xFF) KWP2000: $2E WriteDataByCommonId $A10B recordCommonIdentifier Modus  : Default
- [ECE_STATUS_SIM_CARD_READER](#job-ece-status-sim-card-reader) - Status of Sim Card Reader KWP2000: $22 ReadDataByCommonIdentifier $A00A RecordCommonId Modus  : Default
- [ECE_CHECK_IMEI](#job-ece-check-imei) - Reads IMEI (International Mobile Equipment Identity) KWP2000: $22 ReadDataByCommonIdentifier $A008 recordCommonIdentifier Modus  : Default
- [ECE_CHECK_ICC_ID](#job-ece-check-icc-id) - Read out ICC ID(10 Bytes BCD) KWP2000: $22 ReadDataByCommonIdentifier $A007 recordCommonIdentifier Modus  : Default
- [US_ESN_MIN_LESEN](#job-us-esn-min-lesen) - Reads ESN (Electronic Serial Number) and MIN (Mobile Identification Number) of internal NAD KWP2000: $22 ReadDataByCommonIdentifier $A006 recordCommonIdentifier and $A110 recordCommonIdentifier Modus  : Default
- [US_SET_MIN_TO_ZERO](#job-us-set-min-to-zero) - Sets CDMA module to MIN=0000000000 KWP2000: $2E WriteDataByCommonId $A110 GMIN Modus  : Default
- [US_MIN_SCHREIBEN](#job-us-min-schreiben) - Writes MIN into internal NAD KWP2000: $2E WriteDataByCommonId $A110 GMIN Modus  : Default
- [US_MDN_LESEN](#job-us-mdn-lesen) - Reads CDMA Mobile Directory Number (MDN) KWP2000: $22 ReadDataByCommonIdentifier $A117 recordCommonIdentifier Modus  : Default
- [US_MDN_SCHREIBEN](#job-us-mdn-schreiben) - Writes CDMA Mobile Directory Number (MDN) KWP2000: $2E WriteDataByCommonId $A117 recordCommonIdentifier Modus  : Default
- [BT_AUS](#job-bt-aus) - Sets BT Module to "always-off" KWP2000: $2E WriteDataByCommonId $A100 recordCommonIdentifier Modus  : Default
- [BT_EIN](#job-bt-ein) - Sets BT module to "on" KWP2000: $2E WriteDataByCommonId $A100 recordCommonIdentifier Modus  : Default
- [STATUS_BLUETOOTH](#job-status-bluetooth) - Reads status of BT module KWP2000: $22 ReadDataByCommonIdentifier $A100 recordCommonIdentifier Modus  : Default
- [BT_ANTENNENTEST](#job-bt-antennentest) - Checks, if BT antenna is connected properly KWP2000: $2E WriteDataByCommonIdentifier $A014 recordCommonIdentifier Modus  : Default
- [BT_GERAETEADRESSE_LESEN](#job-bt-geraeteadresse-lesen) - Reads the Bluetooth Device Address KWP2000: $22 ReadDataByCommonIdentifier $A001 recordCommonIdentifier Modus  : Default
- [BT_PASSKEY_LESEN](#job-bt-passkey-lesen) - Reads BT Fix Passkey of TCU (only for 7series & RR) KWP2000: $22 ReadDataByCommonIdentifier $A002 recordCommonIdentifier Modus  : Default
- [BT_PASSKEY_SCHREIBEN](#job-bt-passkey-schreiben) - Writes BT Fix Passkey into TCU (only 7series & RR) (16 bytes hex) KWP2000: $2E writeDataByCommonIdentifier $A000 recordCommonIdentifier Modus  : Default
- [BT_ERKENNUNGSMODUS](#job-bt-erkennungsmodus) - Sets the BT Module to Discoverable Mode KWP2000: $31 StartRoutineByLocalId $21 Delete BT Paired Device List Modus  : Default
- [BT_KOPPLUNG_STARTEN_1234](#job-bt-kopplung-starten-1234) - Starts the Bluetooth Pairing Process KWP2000: $31 StartRoutineByLocalId $19 BT pairing Modus  : Default
- [STATUS_BT_KOPPLUNG](#job-status-bt-kopplung) - Read Bluetooth Pairing Result KWP2000: $22 ReadDataByCommonIdentifier $A005 recordCommonIdentifier Modus  : Default
- [BT_GEKOPPELT_ANZAHL_LESEN](#job-bt-gekoppelt-anzahl-lesen) - Read Bluetooth paired devices KWP2000: $22 ReadDataByCommonIdentifier $A003 recordCommonIdentifier Modus  : Default
- [BT_GEKOPPELT_LOESCHEN](#job-bt-gekoppelt-loeschen) - Delete Bluetooth paired devices list KWP2000: $31 StartRoutineByLocalId $20 Delete Bt Paired Device List Modus  : Default
- [BT_GERAETENAME_LESEN](#job-bt-geraetename-lesen) - Reads the Bluetooth User Friendly Name KWP2000: $22 ReadDataByCommonIdentifier $A002 recordCommonIdentifier Modus  : Default
- [BT_GERAETENAME_SCHREIBEN](#job-bt-geraetename-schreiben) - Writes Bluetooth User Friendly Name KWP2000: $2E writeDataByCommonIdentifier $A002 recordCommonIdentifier Modus  : Default
- [FGNR_ALS_BMW_GERAETENAME_SCHREIBEN](#job-fgnr-als-bmw-geraetename-schreiben) - Writes "BMW" + "space" + last 5 digits of the VIN as BT devicename KWP2000: $2E writeDataByCommonIdentifier $A002 recordCommonIdentifier Modus  : Default
- [FGNR_ALS_RR_GERAETENAME_SCHREIBEN](#job-fgnr-als-rr-geraetename-schreiben) - Writes "RR" + "2xspace" + last 5 digits of the VIN as BT Devicename (only for RR!) KWP2000: $2E writeDataByCommonIdentifier $A002 recordCommonIdentifier Modus  : Default
- [STATUS_SPRACHE](#job-status-sprache) - Read out the Language Variant of Voice Recognition (VR) KWP2000: $22 ReadDataByCommonIdentifier $A10B recordCommonIdentifier Modus  : Default
- [LOESCHE_CODIERBIT_INTERNAL_NAD](#job-loesche-codierbit-internal-nad) - Disables NAD (sets coding bit to "0")
- [SETZE_CODIERBIT_INTERNAL_NAD](#job-setze-codierbit-internal-nad) - Enables NAD (sets coding bit to "1")
- [STATUS_CODIERBIT_INTERNAL_NAD](#job-status-codierbit-internal-nad) - Reads status of "NAD_equipped" coding bit
- [LESEN_PHONE_ID1](#job-lesen-phone-id1) - Reads Phone_ID1 (40 Bytes ASCII) KWP2000: $22 ReadDataByCommonIdentifier $20 recordCommonIdentifier Modus  : Default
- [LESEN_PHONE_ID2](#job-lesen-phone-id2) - Reads Phone_ID2 (40 Bytes ASCII) KWP2000: $22 ReadDataByCommonIdentifier $20 recordCommonIdentifier Modus  : Default
- [LESEN_PHONE_ID3](#job-lesen-phone-id3) - Reads Phone_ID3 (40 Bytes ASCII) KWP2000: $22 ReadDataByCommonIdentifier $20 recordCommonIdentifier Modus  : Default
- [LESEN_PHONE_ID4](#job-lesen-phone-id4) - Reads Phone_ID4 (40 Bytes ASCII) KWP2000: $22 ReadDataByCommonIdentifier $20 recordCommonIdentifier Modus  : Default

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

<a id="job-tcu-type-lesen"></a>
### TCU_TYPE_LESEN

Reads the TCU Type KWP2000: $22 ReadDataByCommonIdentifier $A009 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| TCU_TYPE | int | Hardwarevariante der TCU ECE         /0x00h/ECE variant US          /0x01h/US variant SUPERTHIN   /0x02h/TCU without GPS module and NAD module |
| TCU_TYPE_TEXT | string | Hardwarevariante der TCU, Klartext |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-nvm-init"></a>
### NVM_INIT

Initialise NVM Data KWP2000: $31 StartRoutineByLocalId $FB NVM Initialise Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-sid-nid-schreiben"></a>
### US_SID_NID_SCHREIBEN

Writes multiple SID & NID values into NAD (ONLY US!) KWP2000: $2E WriteDataByCommonId $A118 SID/NID Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INDEX | string | INDEX (Listenplatz) (0-19) |
| SID | string | Home SID (0-32176) |
| NID | string | Home NID (0-65535) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-sid-nid-lesen"></a>
### US_SID_NID_LESEN

Reads SID & NID (16 Bytes (including NULL)) KWP2000: $22 ReadDataByCommonIdentifier $A118 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| INDEX | string | INDEX (Listenplatz) |
| SID | string | SID |
| NID | string | NID |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-cdma-primary-ch-a-schreiben"></a>
### US_CDMA_PRIMARY_CH_A_SCHREIBEN

Reads CDMA Primary Channel A (Only US!) KWP2000: $2E WriteDataByCommonId $A119 CDMA Primary Channel A Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CDMA_PA | string | CDMA Primary Channel A |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-cdma-primary-ch-a-lesen"></a>
### US_CDMA_PRIMARY_CH_A_LESEN

Reads CDMA Primary Channel A (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A119 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CDMA_PA | string | CDMA Primary Channel A 5 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-cdma-secondary-ch-a-schreiben"></a>
### US_CDMA_SECONDARY_CH_A_SCHREIBEN

CM-42 ESN CDMA Secondary Channel A KWP2000: $2E WriteDataByCommonId $A11A CDMA Secondary Channel A Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CDMA_SA | string | CDMA Secondary Channel A |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-cdma-secondary-ch-a-lesen"></a>
### US_CDMA_SECONDARY_CH_A_LESEN

Reads CDMA Secondary Channel A (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A11A recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CDMA_SA | string | CDMA Secondary Channel A 5 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-cdma-primary-ch-b-schreiben"></a>
### US_CDMA_PRIMARY_CH_B_SCHREIBEN

Writes CDMA Primary Channel B into NAD (Only US!) KWP2000: $2E WriteDataByCommonId $A11B CDMA Primary Channel B Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CDMA_PB | string | CDMA Primary Channel B |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-cdma-primary-ch-b-lesen"></a>
### US_CDMA_PRIMARY_CH_B_LESEN

Reads CDMA Primary Channel B (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A11B recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CDMA_PB | string | CDMA Primary Channel B 5 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-cdma-secondary-ch-b-schreiben"></a>
### US_CDMA_SECONDARY_CH_B_SCHREIBEN

Writes CDMA Secondary Channel B (Only US!) KWP2000: $2E WriteDataByCommonId $A11C CDMA Secondary Channel B Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CDMA_SB | string | CDMA Secondary Channel B |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-cdma-secondary-ch-b-lesen"></a>
### US_CDMA_SECONDARY_CH_B_LESEN

Reads CDMA Secondary Channel B (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A11C recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CDMA_SB | string | CDMA Secondary Channel B 5 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-amps-sid-schreiben"></a>
### US_AMPS_SID_SCHREIBEN

Writes AMPS Home SID (Only US!) KWP2000: $2E WriteDataByCommonId $A11D AMPS Home SID Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AMPS_SID | string | Amps SID |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-amps-sid-lesen"></a>
### US_AMPS_SID_LESEN

Reads AMPS SID (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A11D recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| AMPS_SID | string | Amps SID 6 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-amps-paging-ch-schreiben"></a>
### US_AMPS_PAGING_CH_SCHREIBEN

Writes AMPS Paging Channel KWP2000: $2E WriteDataByCommonId $A11E AMPS Paging Channel Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AMPS_PAG | string | Amps Paging Channel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-amps-paging-ch-lesen"></a>
### US_AMPS_PAGING_CH_LESEN

Reads AMPS Paging Channel (Only US!) KWP2000: $22 ReadDataByCommonIdentifier $A11E recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| AMPS_PAG | string | Amps Paging Channel 5 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-a-b-side-schreiben"></a>
### US_A_B_SIDE_SCHREIBEN

Sets channel A or B (Only US!) KWP2000: $2E WriteDataByCommonId $A11F RecordCommonId Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Channel Modus 0x00 = Home Only Disable 0x01 = Home Only Enable 0x02 = Side A Scanning 0x03 = Side B Scanning |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gps"></a>
### STATUS_GPS

Status des GPS wird ausgegeben KWP2000:$21 ReadDataByLocalIdentifier $02 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GPS | int | GPS Status 0x00 = Not supported: No GPS 0x01 = Not supported: Communication error 0x02 = Receiver error 0x03 = No almanac 0x04 = Searching satellites 0x05 = Tracking 1 satellite 0x06 = Tracking 2 satellites 0x07 = Tracking 3 satellites 0x08 = Tracking 4 satellites 0x09 = Tracking 5 satellites 0x0A = Tracking 6 satellites 0x0B = 2D positioning 0x0C = 3D positioning |
| STAT_GPS_TEXT | string | GPS-Status als Textausgabe |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecall-disable"></a>
### ECALL_DISABLE

Disables eCall possibility KWP2000: $2E WriteDataByCommonId $A124 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecall-enable"></a>
### ECALL_ENABLE

Enables eCall possibility KWP2000: $2E WriteDataByCommonId $A124 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ecall"></a>
### STATUS_ECALL

Reads out ecall status KWP2000: $22 ReadDataByCommonIdentifier $A124 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ECALL | int | eCall status (1 Byte) 0x00 eCall possibility not activated 0x01 eCall possibility activated |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hw-selbsttest"></a>
### HW_SELBSTTEST

Starts HW selftest of ECU Tested modules: BT module GPS module NAD Flash ROM SDRAM KWP2000: $31 startRoutineByLocalIdentifier $04 routineLocalIdentifier (selfTest) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT table JobResultExtended STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hw-selbsttest"></a>
### STATUS_HW_SELBSTTEST

Reads the result of the hardware selftest KWP2000: $22 ReadDataByCommonIdentifier $A013 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BYTE_HW_TEST | int | Result of hardware selftest Possible results: 0x00 All tests passed 0x01 SDRAM test failed 0x02 Flash RAM test failed 0x04 GPS module test failed 0x08 BT module test failed 0x10 NAD module test failed |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ecu-connections"></a>
### STATUS_ECU_CONNECTIONS

Test of eCall button+LED, Backup Antenna, Main Antenna, Microphone 1+2 and Backup-Loudspeaker KWP2000: $2E WriteDataByCommonId $A013 RecordCommonId Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TEST | int | Test Resultat (1 Byte) 0x00 Tests nicht bestanden (Bitte FS_LESEN aufrufen, um das Resultat einzusehen) 0x01 alle Tests bestanden |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-nad-information"></a>
### NAD_INFORMATION

Get information about the current NAD Activity KWP2000: $22 ReadDataByCommonIdentifier $A032 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| NAD_REGISTERSTATE | int | Einbuchungsstatus des NAD 0x00 NAD momentan nicht eingebucht 0x01 NAD momentan eingebucht |
| NAD_REGISTERSTATE_TEXT | string | NAD_RegisterState als Textausgabe externe Tabelle |
| NAD_SIGNALSTRENGTH | int | Signalstaerke (0-31) 0xFF (unknown) |
| NAD_SIGNALBARS | int | Signalstaerke (1-5) 0x00 (0 bars) 0x01 (1 bar) 0x02 (2 bars) 0x03 (3 bars) 0x04 (4 bars) 0x05 (5 bars) 0xFF (unknown) |
| NAD_ROAMING_STATUS | int | Roamingstatus des NAD 0x00 Roaming momentan nicht aktiviert 0x01 Roaming momentan aktiviert 0x02 Roeming off network (US only) |
| NAD_CURRENT_SID | string | System ID, in welcher das NAD gerade eingebucht ist (Only US!) 5 Bytes in ECE: immer "00000" |
| NAD_CURRENT_NID | string | Network ID, in welcher das NAD gerade eingebucht ist (Only US!) 5 Bytes in ECE: immer "00000" |
| NAD_CURRENT_MCC | string | Mobile Country Code (MCC), in welchem das NAD gerade eingebucht ist (Only US!) 3 Bytes in ECE: immer "000" |
| NAD_CURRENT_MNC | string | Mobile Network Code (MNC), in welchem das NAD gerade eingebucht ist (Only US!) 2 Bytes in ECE: immer "00" |
| NAD_PRL_ID | string | ID der Preferred Roaming List (PRL) (Only US!) 5 Bytes in ECE: immer "00000" |
| GPS_DATE | string | Momentanes GPS Datum 10 Bytes |
| GPS_TIME | string | Momentane GPS Zeit 8 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-status-home-only"></a>
### US_STATUS_HOME_ONLY

Reads "Home Only" Status KWP2000: $22 ReadDataByCommonIdentifier $A11F recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HOME_ONLY | int | "Home Only" Status 1 Byte 0x00 "Home Only" nicht aktiviert 0x01 "Home Only" aktiviert (kein Roaming erlaubt) 0x02 Side A scanning 0x03 Side B scanning |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-home-only-disable"></a>
### US_HOME_ONLY_DISABLE

Disables "Home Only" and enables Roaming KWP2000: $2E WriteDataByCommonId $A11F recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-home-only-enable"></a>
### US_HOME_ONLY_ENABLE

Enables "Home Only" and disables Roaming KWP2000: $2E WriteDataByCommonId $A11F recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-status-car-phone"></a>
### US_STATUS_CAR_PHONE

Reads out status of internal car phone KWP2000: $22 ReadDataByCommonIdentifier $A106 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CAR_PHONE | int | Status des Car Phones 1 Byte 0x00 Car Phone ist nicht aktiviert 0x01 Car Phone ist aktiviert |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-disable-car-phone"></a>
### US_DISABLE_CAR_PHONE

Disables Car Phone KWP2000: $2E WriteDataByCommonId $A106 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-enable-car-phone"></a>
### US_ENABLE_CAR_PHONE

Enables Car Phone KWP2000: $2E WriteDataByCommonId $A106 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-emerg-no-lesen"></a>
### EMERG_NO_LESEN

Reads Backup Emergency Number KWP2000: $22 ReadDataByCommonIdentifier $A108 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| EMERGENCY_NUM | string | Notfall Nummer 20 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-emerg-no-schreiben"></a>
### EMERG_NO_SCHREIBEN

Writes Emergency Number KWP2000: $2E writeDataByCommonIdentifier $A108 recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EMERGENCY_NUM | string | Notfall Nummer 20 Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hotline-no-lesen"></a>
### HOTLINE_NO_LESEN

Reads Hotline Number KWP2000: $22 ReadDataByCommonIdentifier $A123 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HOTLINE_NUM | string | Hotline Nummer 20 bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hotline-no-schreiben"></a>
### HOTLINE_NO_SCHREIBEN

Writes Hotline Number KWP2000: $2E writeDataByCommonIdentifier $A123 recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HOTLINE_NUM | string | Hotline Nummer 20 Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-breakdown-no-lesen"></a>
### BREAKDOWN_NO_LESEN

Reads Breakdown Number KWP2000: $22 ReadDataByCommonIdentifier $A122 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BREAKDOWN_NO | string | BMW Pannenservice-Nummer 20 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-breakdown-no-schreiben"></a>
### BREAKDOWN_NO_SCHREIBEN

Writes BMW Breakdown Number KWP2000: $2E writeDataByCommonIdentifier $A122 recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BREAKDOWN_NUM | string | BMW Pannenservice-Nummer 20 bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dealer-no-lesen"></a>
### DEALER_NO_LESEN

Reads BMW Home Dealer Number KWP2000: $22 ReadDataByCommonIdentifier $A121 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DEALER_NUM | string | Eigene BMW Haendler Nummer 20 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dealer-no-schreiben"></a>
### DEALER_NO_SCHREIBEN

Writes BMW HOME Dealer Number KWP2000: $2E writeDataByCommonIdentifier $A121 recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DEALER_NUM | string | Eigene BMW Handler Nummer 20 Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-gats-smsc-no-lesen"></a>
### GATS_SMSC_NO_LESEN

Reads GATS SMSC Number KWP2000: $22 ReadDataByCommonIdentifier $A109 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| GATS_SMSC_NUM | string | GATS SMSC (Short Message Service Center) Nummer 20 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-gats-smsc-no-schreiben"></a>
### GATS_SMSC_NO_SCHREIBEN

Writes GATS SMCS Number KWP2000: $2E writeDataByCommonIdentifier $A109 recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GATS_SMSC_NUM | string | GATS SMSC (Short Message Service Center) Nummer 20 Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-gats-provider-no-lesen"></a>
### GATS_PROVIDER_NO_LESEN

Reads GATS Provider Nuber KWP2000: $22 ReadDataByCommonIdentifier $A10A recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PROVIDER_NUM | string | GATS Provider Nummer 20 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-gats-provider-no-schreiben"></a>
### GATS_PROVIDER_NO_SCHREIBEN

Writes GATS Provider No KWP2000: $2E writeDataByCommonIdentifier $A10A recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PROVIDER_NUM | string | GATS Provider Nummer 20 Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-non-telematic-ecall"></a>
### STATUS_NON_TELEMATIC_ECALL

Reads status of non-telematic eCall (Coding Bit) KWP2000: $22 ReadDataByCommonIdentifier $A104 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_NT_ECALL | int | Status des Non-Telematik eCalls 1 Byte 0x00 Non telematic eCall nicht erlaubt 0x01 Non telematic eCall erlaubt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-telematics-services"></a>
### STATUS_TELEMATICS_SERVICES

Reads status of telematic coding bit KWP2000: $22 ReadDataByCommonIdentifier $A103 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TELEMATICS_SRVC | int | Status des Telematik Codierbis 1 Byte 0x00 Telematik Services nicht aktiviert 0x01 Telematik Services aktiviert |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-io-port-pins"></a>
### STATUS_IO_PORT_PINS

TCU I/O Port Pins KWP2000: $22 ReadDataByCommonIdentifier $A010 RecordCommonId Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BYTE1 | int | Port Pins Byte 1 |
| STAT_BYTE2 | int | Port Pins Byte 2 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ece-sprachkonfiguration"></a>
### ECE_SPRACHKONFIGURATION

starts language configuration (Argument = 0xFF) KWP2000: $2E WriteDataByCommonId $A10B recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ece-status-sim-card-reader"></a>
### ECE_STATUS_SIM_CARD_READER

Status of Sim Card Reader KWP2000: $22 ReadDataByCommonIdentifier $A00A RecordCommonId Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CARD_READER | int | Status of Sim Card Reader SIM_CARD = 0 No SIM card in Telematics SIM card reader readable SIM_CARD = 1 SIM card in Telematics SIM card reader readable SIM_CARD = 2 SIM card in external front SIM card reader readable SIM_CARD = 4 SIM card in external rear SIM card reader readable SIM_CARD = 6 SIM card in external front and rear SIM card reader readable |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ece-check-imei"></a>
### ECE_CHECK_IMEI

Reads IMEI (International Mobile Equipment Identity) KWP2000: $22 ReadDataByCommonIdentifier $A008 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| IMEI | string | IMEI des internen Telefonmoduls 15 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ece-check-icc-id"></a>
### ECE_CHECK_ICC_ID

Read out ICC ID(10 Bytes BCD) KWP2000: $22 ReadDataByCommonIdentifier $A007 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ICC_ID | string | ICC-ID des internen Telefonmoduls |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-esn-min-lesen"></a>
### US_ESN_MIN_LESEN

Reads ESN (Electronic Serial Number) and MIN (Mobile Identification Number) of internal NAD KWP2000: $22 ReadDataByCommonIdentifier $A006 recordCommonIdentifier and $A110 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| US_ESN | string | Electronic Serial Number 12 Bytes |
| US_MIN | string | Mobile Identification Number 10 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-us-set-min-to-zero"></a>
### US_SET_MIN_TO_ZERO

Sets CDMA module to MIN=0000000000 KWP2000: $2E WriteDataByCommonId $A110 GMIN Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-min-schreiben"></a>
### US_MIN_SCHREIBEN

Writes MIN into internal NAD KWP2000: $2E WriteDataByCommonId $A110 GMIN Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| US_MIN | string | MIN 10 Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-mdn-lesen"></a>
### US_MDN_LESEN

Reads CDMA Mobile Directory Number (MDN) KWP2000: $22 ReadDataByCommonIdentifier $A117 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| US_MDN | string | Mobile Directory Number (MDN) 15 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-us-mdn-schreiben"></a>
### US_MDN_SCHREIBEN

Writes CDMA Mobile Directory Number (MDN) KWP2000: $2E WriteDataByCommonId $A117 recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| US_MDN | string | Mobile Directory Number 10 Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-aus"></a>
### BT_AUS

Sets BT Module to "always-off" KWP2000: $2E WriteDataByCommonId $A100 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-ein"></a>
### BT_EIN

Sets BT module to "on" KWP2000: $2E WriteDataByCommonId $A100 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bluetooth"></a>
### STATUS_BLUETOOTH

Reads status of BT module KWP2000: $22 ReadDataByCommonIdentifier $A100 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BLUETOOTH | int | Status des Bluetooth Moduls 0x00 BT Modul ist aus 0x01 BT Modul ist an |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-antennentest"></a>
### BT_ANTENNENTEST

Checks, if BT antenna is connected properly KWP2000: $2E WriteDataByCommonIdentifier $A014 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BT_RESULT_BYTE | int | Result byte of antenna test |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-geraeteadresse-lesen"></a>
### BT_GERAETEADRESSE_LESEN

Reads the Bluetooth Device Address KWP2000: $22 ReadDataByCommonIdentifier $A001 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DEV_ADR | binary | Bluetooth Device Adresse von TCU 6 Bytes, hex |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-passkey-lesen"></a>
### BT_PASSKEY_LESEN

Reads BT Fix Passkey of TCU (only for 7series & RR) KWP2000: $22 ReadDataByCommonIdentifier $A002 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BT_FIX_PASSKEY | string | Fix Passkey der TCU 18 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-passkey-schreiben"></a>
### BT_PASSKEY_SCHREIBEN

Writes BT Fix Passkey into TCU (only 7series & RR) (16 bytes hex) KWP2000: $2E writeDataByCommonIdentifier $A000 recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FIX_PASSKEY | string | Fix Passkey der TCU |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-erkennungsmodus"></a>
### BT_ERKENNUNGSMODUS

Sets the BT Module to Discoverable Mode KWP2000: $31 StartRoutineByLocalId $21 Delete BT Paired Device List Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-kopplung-starten-1234"></a>
### BT_KOPPLUNG_STARTEN_1234

Starts the Bluetooth Pairing Process KWP2000: $31 StartRoutineByLocalId $19 BT pairing Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bt-kopplung"></a>
### STATUS_BT_KOPPLUNG

Read Bluetooth Pairing Result KWP2000: $22 ReadDataByCommonIdentifier $A005 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PAIRING | int | Pairing Result 0x00 erfolgreich 0x01 Fehler 0x02 wartend 0x99 unbekannt |
| STAT_PAIRING_TEXT | string | Pairing Status |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-gekoppelt-anzahl-lesen"></a>
### BT_GEKOPPELT_ANZAHL_LESEN

Read Bluetooth paired devices KWP2000: $22 ReadDataByCommonIdentifier $A003 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| NUM_PAIRED_DEVICES | int | Anzahl der paired Devices in TCU |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-gekoppelt-loeschen"></a>
### BT_GEKOPPELT_LOESCHEN

Delete Bluetooth paired devices list KWP2000: $31 StartRoutineByLocalId $20 Delete Bt Paired Device List Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-geraetename-lesen"></a>
### BT_GERAETENAME_LESEN

Reads the Bluetooth User Friendly Name KWP2000: $22 ReadDataByCommonIdentifier $A002 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FRIENDLY_NAME | string | Bluetooth Geraetename 18 Bytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bt-geraetename-schreiben"></a>
### BT_GERAETENAME_SCHREIBEN

Writes Bluetooth User Friendly Name KWP2000: $2E writeDataByCommonIdentifier $A002 recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| USER_FRIENDLY_NAME | string | Bluetooth Geraetenamen 18 Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fgnr-als-bmw-geraetename-schreiben"></a>
### FGNR_ALS_BMW_GERAETENAME_SCHREIBEN

Writes "BMW" + "space" + last 5 digits of the VIN as BT devicename KWP2000: $2E writeDataByCommonIdentifier $A002 recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer 18 Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fgnr-als-rr-geraetename-schreiben"></a>
### FGNR_ALS_RR_GERAETENAME_SCHREIBEN

Writes "RR" + "2xspace" + last 5 digits of the VIN as BT Devicename (only for RR!) KWP2000: $2E writeDataByCommonIdentifier $A002 recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer 18 Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sprache"></a>
### STATUS_SPRACHE

Read out the Language Variant of Voice Recognition (VR) KWP2000: $22 ReadDataByCommonIdentifier $A10B recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LANGUAGE | int | Language Variant (1 Byte) 0x00 deutsch 0x01 us 0x02 englisch (auch in NL/RUS/CHI/KOR) 0x03 italienisch 0x04 franzoesisch 0x05 spanisch 0x06 japanisch (nicht aktivierbar) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-loesche-codierbit-internal-nad"></a>
### LOESCHE_CODIERBIT_INTERNAL_NAD

Disables NAD (sets coding bit to "0")

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if job works properly |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-setze-codierbit-internal-nad"></a>
### SETZE_CODIERBIT_INTERNAL_NAD

Enables NAD (sets coding bit to "1")

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY if job works properly |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierbit-internal-nad"></a>
### STATUS_CODIERBIT_INTERNAL_NAD

Reads status of "NAD_equipped" coding bit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY if job works properly |
| STAT_NAD | int | Codierbit INTERNAL_NAD 0x00 NAD ausgeschaltet 0x01 NAD eingeschaltet |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-phone-id1"></a>
### LESEN_PHONE_ID1

Reads Phone_ID1 (40 Bytes ASCII) KWP2000: $22 ReadDataByCommonIdentifier $20 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HAEUFIGKEIT | int | Haeufigkeitszaehler |
| LAUFLEISTUNG1 | unsigned long | km-Stand des ersten Connects |
| LAUFLEISTUNG2 | unsigned long | km-Stand des ersten Reconnects |
| LAUFLEISTUNG3 | unsigned long | km-Stand des letzten Reconnects |
| PHONE_MODEL1 | string | Model des Mobiltelefons 1 |
| PHONE_SW1 | string | Software des Mobiltelefons 1 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-phone-id2"></a>
### LESEN_PHONE_ID2

Reads Phone_ID2 (40 Bytes ASCII) KWP2000: $22 ReadDataByCommonIdentifier $20 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HAEUFIGKEIT | int | Haeufigkeitszaehler |
| LAUFLEISTUNG1 | unsigned long | km-Stand des ersten Connects |
| LAUFLEISTUNG2 | unsigned long | km-Stand des ersten Reconnects |
| LAUFLEISTUNG3 | unsigned long | km-Stand des letzten Reconnects |
| PHONE_MODEL2 | string | Model des Mobiltelefons 2 |
| PHONE_SW2 | string | Software des Mobiltelefons 2 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-phone-id3"></a>
### LESEN_PHONE_ID3

Reads Phone_ID3 (40 Bytes ASCII) KWP2000: $22 ReadDataByCommonIdentifier $20 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HAEUFIGKEIT | int | Haeufigkeitszaehler |
| LAUFLEISTUNG1 | unsigned long | km-Stand des ersten Connects |
| LAUFLEISTUNG2 | unsigned long | km-Stand des ersten Reconnects |
| LAUFLEISTUNG3 | unsigned long | km-Stand des letzten Reconnects |
| PHONE_MODEL3 | string | Model des Mobiltelefons 3 |
| PHONE_SW3 | string | Software des Mobiltelefons 3 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-phone-id4"></a>
### LESEN_PHONE_ID4

Reads Phone_ID4 (40 Bytes ASCII) KWP2000: $22 ReadDataByCommonIdentifier $20 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HAEUFIGKEIT | int | Haeufigkeitszaehler |
| LAUFLEISTUNG1 | unsigned long | km-Stand des ersten Connects |
| LAUFLEISTUNG2 | unsigned long | km-Stand des ersten Reconnects |
| LAUFLEISTUNG3 | unsigned long | km-Stand des letzten Reconnects |
| PHONE_MODEL4 | string | Model des Mobiltelefons 4 |
| PHONE_SW4 | string | Software des Mobiltelefons 4 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [ABILITY_TO_WAKE](#table-ability-to-wake) (4 × 2)
- [MOST_3DB](#table-most-3db) (3 × 2)
- [WAKE_UP_STATUS](#table-wake-up-status) (4 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (36 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (2 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (7 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (18 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (3 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (6 × 9)
- [TCUTYPE_STATUS](#table-tcutype-status) (4 × 2)
- [TGPSSTATUS](#table-tgpsstatus) (14 × 2)
- [TABNADSTATUS](#table-tabnadstatus) (3 × 2)

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
| ?81? | ERROR_VIHICLE_IDENTFICATON_NR |
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

Dimensions: 77 rows × 2 columns

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

Dimensions: 36 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xD68D | Weckendes Device hat drei Mal erfolglos versucht, das Netzwerk zu wecken (Error_WAKEUP_Failed) |
| 0xD68E | Obwohl Shutdown (Execute) geschickt wurde, ging das Licht nicht aus (Error_Light_Not_Off) |
| 0xD690 | Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |
| 0xD691 | Lange und/oder haeufige Unlocks (Error_Unlock_Long) |
| 0xD692 | Ein Device hat sich wegen Uebertemperatur abgeschaltet (Error_Temp_Shutdown) |
| 0xA368 | Kurzschluss in der GPS-Antenne (Error_HW_GPS_ANTENNA_SHORT) |
| 0xA369 | GPS-Antenne nicht angeschlossen (Error_HW_GPS_ANTENNA_OPEN) |
| 0xA36A | Fehler im GPS-Modul (Error_HW_GPS_HW) |
| 0xA36B | Kommunikation zwischen GPS-Modul und MOST gestoert (Error_HW_GPS_COMM_FAIL) |
| 0xA36C | Fehler im internen Telefon Modul (ERROR_NAD) |
| 0xA36D | Notruftaster fehlerhaft oder nicht angeschlossen (Error_HW_MAYDAY_SWITCH_DISCONNECTED) |
| 0xA36E | Notruf-LED ist ohne Funktion (Error_HW_MAYDAY_LED_NOK) |
| 0xA36F | Kommunikation mit Airbag SG gestoert (ERROR_COM_AIRBAG_ECU) |
| 0xA370 | Kurzschluss gegen 12V im Notruftaster (Error_HW_MAYDAY_SWITCH_SHORT) |
| 0xA372 | Kommunikation mit Airbag SG gestoert (ERROR_COM_AIRBAG_ECU) |
| 0xA373 | Speicherfehler (Error NVM_NOK) |
| 0xA374 | Kurzschluss gegen Masse im Notruftaster (Error_HW_MAYDAY_SWITCH_STUCK) |
| 0xA375 | Kommunikation mit Airbag-SG gestoert (Error_IBUS_CONNECTION_FAIL) |
| 0xA376 | Kommunikation mit PhoneBoard gestoert (Error_CAN_TELECOMMANDER_FAIL) |
| 0xA377 | Fehler im PhoneBoard (Error_TELCOMMANDER_KEYPAD_FAIL) |
| 0xA378 | Kommunikation mit Airbag SG gestoert (ERROR_COM_AIRBAG_ECU) |
| 0xA379 | Fehler im Bluetooth-Interface (Error_BT_INTERFACE) |
| 0xA37A | Energiesparmode aktiv (Error_MTS_MODE_ACTIVE) |
| 0xA37B | Fehler mit Backup Antenne (ERROR_BACKUP_ANTENNA) |
| 0xA37C | Fehler mit Haupt TCU Antenne (ERROR_TCU_MAIN_ANTENNA) |
| 0xA37D | Fehler mit Backup Lautsprecher (ERROR_BACKUP_LOUDSPEAKER) |
| 0xA37E | Fehler mit BT Cradle Button (ERROR_BT_CRADLE_BUTTON) |
| 0xA382 | Fehler mit Mikrofon 1 (ERROR_MIC_1) |
| 0xA383 | Fehler mit Mikrofon 2 (ERROR_MIC_2) |
| 0xA384 | Prefit SIM physikalisch nicht erreichbar (ERROR_PSIM_NOT_REACHABLE) |
| 0xA385 | Prefit SIM Lesefehler (ERROR_PSIM_NOT_READABLE) |
| 0xA386 | Prefit SIM PIN gesperrt (ERROR_PSIM_PIN_LOCKED) |
| 0xA387 | Fehler mit Bluetooth Antenne (ERROR_BT_ANTENNA) |
| 0xA8E8 | Fehler in Wheel Speed Sensor (ERROR_WHEEL_SPEED_SENSOR) |
| 0xA8E9 | Fehlerhafte Codierdaten (ERROR_CODING_DATA) |
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
| 0xD690 | 0x06 | -- | -- | -- |
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
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 18 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9301 | Phone_ID_1 |
| 0x9302 | Phone_ID_2 |
| 0x9303 | Phone_ID_3 |
| 0x9304 | Phone_ID_4 |
| 0x9308 | Watchdog Reset |
| 0x9309 | HW NS Init Timeout |
| 0x930A | Device ist im Zustand Normal Operation und das Licht am Eingang geht ohne Vorankuendigung aus (Error_Sudden_light_off) |
| 0x930B | Anfragendes Device bekommt keine Antwort obwohl Partner vorhanden ist (Error_Device_No_Answer) |
| 0x930C | Kurze Unlocks (Error_Unlock_Short) |
| 0x930D | Kein Broadcast Configuration(Status) vom Networkmaster erhalten (Error_t_CfgStatus) |
| 0x9310 | Empfaenger hat eine Nachricht nicht abgenommen (Error_NAK) |
| 0x9312 | Niedrige Feldstaerke waehrend aktiver Verbindung über das interne NAD (Error_LOW_RF) |
| 0x9313 | Behebbarer Fehler im NVM (Error_NVM_CORRUPTION) |
| 0x931A | Prefit SIM nicht angeschlossen; PSIM jedoch momentan nicht aktiviert (ERROR_PSIM_NOT_REACHABLE) |
| 0x931B | Fehler beim Lesen der Prefit SIM; PSIM jedoch momentan nicht aktiviert (ERROR_PSIM_NOT_READABLE) |
| 0x931C | Prefit SIM PIN gesperrt; PSIM jedoch momentan nicht aktiviert (ERROR_PSIM_PIN_LOCKED) |
| 0x931D | Prefit SIM von Provider nicht freigeschaltet (ERROR_PSIM_DENIED_IN_THE_NETWORK) |
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

Dimensions: 6 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Logische-Knotenadresse | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x02 | FBlockID | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x03 | InstID | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x04 | FktID | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x05 | Diagnoseadresse | Hex | -- | unsigned char | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-tcutype-status"></a>
### TCUTYPE_STATUS

Dimensions: 4 rows × 2 columns

| TCU_TYPE | TCU_TYPE_TEXT |
| --- | --- |
| 0x00 | ECE |
| 0x01 | US |
| 0x02 | SUPERTHIN |
| 0xXY | unbekannte TCU |

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

<a id="table-tabnadstatus"></a>
### TABNADSTATUS

Dimensions: 3 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | not registered |
| 0x01 | registered |
| 0xXY | nicht definiert |
