# DWA_63.prg

- Jobs: [91](#jobs)
- Tables: [36](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DWA - Innenraumschutz E63-E64, E88, E93  |
| ORIGIN | BMW EI-61 T. Reiter |
| REVISION | 2.000 |
| AUTHOR | Metasystem S.r.l. R&D M. Cattaneo, Bertrandt GmbH - K. Knorr |
| COMMENT | SGBD fuer DWA E63-E64, E88, E93 |
| PACKAGE | 1.29 |
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
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
- [HS_LESEN_DETAIL](#job-hs-lesen-detail) - Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default
- [HS_LOESCHEN](#job-hs-loeschen) - Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default
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
- [_GEMEL_REVISION_INDEX_IDENT_ID](#job-gemel-revision-index-ident-id) - Readout of the Gemel revision index of the part. This ID is written in EEPROM KWP2000: $21 ReadDataByLocalIdentifier $B8 identifier of the Gemel Rev Ind
- [_GEMEL_APPL_SW_IDENT_ID](#job-gemel-appl-sw-ident-id) - Readout of the Gemel application software identifier which is written in the ROM KWP2000: $21 ReadDataByLocalIdentifier $A9 identifier of the Gemel Software
- [_GEMEL_BOOTLOADER_SW_IDENT_ID](#job-gemel-bootloader-sw-ident-id) - Readout of the bootloader software identifier which is written in the ROM KWP2000: $21 ReadDataByLocalIdentifier $AA identifier of the Gemel Software
- [_GEMEL_MUW_SERIENNUMMER_LESEN](#job-gemel-muw-seriennummer-lesen) - Reads the SERIAL NUMBER of the addressed MUW (vr,hr,hl,vl,hi,alle) in EEPROM. The S.N. has 9 ASCII characters bytes: - the last two digits of year (2 bytes) - one char for month id: '1','2','3','4','5' '6','7','8','9','A','B','C' (1 byte) - two digits for the day (2 bytes) - the progressive nr. in hex (4 bytes) If JOB_STATUS is OK: The Serial Number (S.N.) is displayed. In case an internal error occurred, the S.N. is not valid, and the following error codes appear: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $21 ReadDataByLocalIdentifier $B2 identifier of the S.N. of MUW's $MUWID identifier of the MUW's
- [_GEMEL_MUW_CODIERUNG_LESEN](#job-gemel-muw-codierung-lesen) - Reads the CODIERUNG values of all the MUW's In case an internal error occurred, the CODIERUNG values are not valid. KWP2000: $21 ReadDataByLocalIdentifier $B7 identifier of the of MUW's COD.
- [_GEMEL_STEUERN_MUW_DIAG_INIT](#job-gemel-steuern-muw-diag-init) - Init the MUW/s (vr, hr, hl, vl, hi, alle) to the normal (Off) status (from any status). This job can be used during development for removing a MUW deadlock situation (i.e.: MUW not responding) If JOB_STATUS is OK: The MUW/s status is displayed: the datum XX_MUW_STAT has value '0' if the MUW is in status Off (ready). It has values 1,2,3 in case the MUW is responding but is in other status than Off (On, Sleep, Alarm) In case an internal error occurred, the following error codes are indicated by XX_MUW_STAT: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $39 Muw status to Off
- [IDENT_MUW](#job-ident-muw) - Reads the identification data of the addressed MUW (vr,hr,hl,vl,hi,alle) The MUW identification data are: - Developer ID - MUW Message Catalogue Version - MUW Functional SW Version - MUW Hardware Index - MUW Part Number - MUW Address If JOB_STATUS is OK: All the above data are displayed. The datum XX_MUW_FEHLER_STATUS has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error codes are indicated by XX_MUW_FEHLER_STATUS: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $22 ReadDataByCommonIdentifier $40 ident MuW (project specific)
- [STATUS_CAR_KEY_MEMORY](#job-status-car-key-memory) - Readout of the CKM parameters from RAM (currently used by the DWA Cansine) KWP2000: $21 ReadDataByLocalIdentifier $B0
- [STATUS_DWA_KLEMME_30](#job-status-dwa-klemme-30) - Readout of the external battery supply voltage KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $02 external supply voltage
- [STATUS_MUW_KLEMME_30](#job-status-muw-klemme-30) - Readout of the supply voltage of the addressed MUW (vr,hr,hl,vl,hi,alle). The MUW supply voltage has a resolution of 1 Volt If JOB_STATUS is OK: The MUW/s voltage is displayed. The datum STAT_XX_MUW_KLEMME_30_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error codes are indicated by STAT_XX_MUW_KLEMME_30_FEHL: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState
- [STATUS_DWA_TEMPERATUR](#job-status-dwa-temperatur) - Readout of the internal temperature on the DWA PCB of the Cansine - wait ca. 30 seconds after Cansine power on KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $08 parameter DWA temperature
- [STATUS_MUW_TEMPERATUR](#job-status-muw-temperatur) - Readout of the MUW internal temperature of the addressed MUW (vr,hr,hl,vl,hi,alle). Wait at least 2 seconds after Power ON before executing this job. If JOB_STATUS is OK: The MUW/s voltage is displayed. The datum STAT_XX_MUW_TEMP_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error codes are indicated by STAT_XX_MUW_TEMP_FEHL: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $30 InputOutputControlByLocalIdentifier $0A MUW_TEMPERATUR $02 ReportIOconditions $xx identifiers of MUW
- [STATUS_DWA_LED](#job-status-dwa-led) - Readout of the DWA LED status (on=1, off=0) KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $01 status of the DWA LED
- [STATUS_DWA_ALARMTRIGGER](#job-status-dwa-alarmtrigger) - Readout of the alarm trigger status of the DWA For the MUW related alarm trigger, the system must be armed, for other alarm triggers, the system can be armed or disarmed KWP2000: $21 ReadDataByLocalIdentifier $A0 identifier of the ALARM_TRIGGER
- [STATUS_DWA_INTERN](#job-status-dwa-intern) - Readout of the application status of the CANSINE. The following statuses are possible: -  0: dwa disarmed -  1: dwa arming -  2: dwa armed -  3: dwa disarming -  4: dwa alarm -  5: dwa dwa pause after alarm -  6: dwa transport mode -  7: dwa werkstatt mode -  9: dwa armed - MUW & Tilt Sensor deactivated by User - 10: dwa armed - distribution mode - 11: dwa ending energiesparmode - 12: dwa powerdown mode - 13: dwa panik alarm mode - 14: dwa armed - hotelstellung active - 15: dwa armed- MUW & Tilt Sensor not active - 16: dwa armed - MUW not active - 17: dwa armed - Tilt Sensor not active - 18: dwa schnelltest active - 19: dwa armed - MUW & Tilt Sensor referencing - 20: dwa armed - MUW referencing - 21: dwa armed - Tilt Sensor referencing KWP2000: $21 ReadDataByLocalIdentifier $A1 identifier of the DWA_STS
- [STATUS_MUW_INTERN](#job-status-muw-intern) - Readout of the MUW status of the addressed MUW (vr, hr, hl, vl, hi, alle). The following statuses are shown: - MUW communication error status - MUW internal error code - Number of intrusions recorded The Number of Intrusions detected is reset after this job is executed. If JOB_STATUS is OK: The MUW/s voltage is displayed. The datum STAT_XX_MUW_KOMM_FEHLER has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error codes are indicated by STAT_XX_MUW_KOMM_FEHLER: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $21 ReadDataByLocalIdentifier $A3 identifier of the MUW status
- [STATUS_MUW_ALARM_LEVELS](#job-status-muw-alarm-levels) - Readout of the last ten alarms voltage levels of the addressed MUW/s (vr,hr,hl,vl,hi,alle) The MUW alarm level value has a resolution of 5mV for parts with FSV550 or lower, and of 20mV for FSV higher or equal than FSV560 If JOB_STATUS is OK: The 10 MUW/s alarms levels are displayed. The value '0' means 'no alarm stored in this location. STAT_XX_MUW_ALARM_LEVELS_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error code is shown by STAT_XX_MUW_ALARM_LEVELS_FEHL: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $11 status of the MUW alarm levels $xx MUW id
- [STATUS_MUW_FALSE_WAKEUP_LEVELS](#job-status-muw-false-wakeup-levels) - Readout of the last ten false wakeup levels (wakeup not leading to alarm) of the addressed MUW/s (vr,hr,hl,vl,hi,alle). The MUW alarm level value has a resolution of 5mV for parts with FSV550 or lower, and of 20mV for FSV higher or equal than FSV560 If JOB_STATUS is OK: The 10 MUW/s false wakeup levels are displayed. The value '0' means 'no alarm stored in this location. STAT_XX_MUW_F_WAKEUP_LEVELS_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error code is shown by STAT_XX_MUW_F_WAKEUP_LEVELS_FEHL: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $12 status of the MUW F wakeup level $xx MUW id
- [STATUS_MUW_NOISE](#job-status-muw-noise) - Readout of the MUW noise level of the addressed MUW (vr, hr, hl, vl, hi). The local noise measurement takes approx 5s for each MUW. If JOB_STATUS is OK: The MUW/s noise level is displayed in mV. Each MUW returns a value from 0 to 255, in in multiples of 5mV or 20mV The MUW noise level value has a resolution of 5mV for parts with FSV550 or lower, and of 20mV for FSV higher or equal than FSV560 This value is then converted and displayed in mV. STAT_XX_MUW_KOMM_FEHLER has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error codes are indicated by STAT_XX_MUW_KOMM_FEHLER: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState
- [STATUS_NEIGUNG_X_ACHSE](#job-status-neigung-x-achse) - Readout of the current angle value in degrees, given by the inclination sensor of the DWA KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $0E id. of the ADXL X angle
- [STATUS_NEIGUNG_Y_ACHSE](#job-status-neigung-y-achse) - Readout of the current angle value in degrees, given by the inclination sensor of the DWA KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $0F id. of the ADXL Y angle
- [STATUS_INTERNER_BATTERIE_LEVEL](#job-status-interner-batterie-level) - Readout of the current residual level of the internal battery. The possible levels are: - 1: empty - 2: good - 3: new KWP2000: $21 ReadDataByLocalIdentifier $A8 identifier of the internal battery level of charge
- [INTERNER_BATTERIE_WECHSEL](#job-interner-batterie-wechsel) - Set the current consumption status of the internal battery to '3:New'. This operation has to be done with new batteries KWP2000: $3B WriteDataByLocalIdentifier $A8 identifier of the internal battery level of charge
- [STEUERN_DWA_LED](#job-steuern-dwa-led) - Set the status of the DWA LED to 'ein', 'aus' KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment
- [STEUERN_DWA_SCHAERFEN](#job-steuern-dwa-schaerfen) - Set the DWA to the armed ('ein') or disarmed ('aus') status KWP2000: $31 StartRoutineByLocalIdentifier $43 id for Schaerfen/Entschaerfen
- [STEUERN_SIRENE_EIN_AUS](#job-steuern-sirene-ein-aus) - Start ('ein') the siren sound, timeout ca. 30s Stop ('aus') the current sound before timeout KWP2000: $31 StartRoutineByLocalIdentifier $44 Sirene identifier
- [STEUERN_DWA_SELFTEST](#job-steuern-dwa-selftest) - Perform an hardware selftest of the DWA and report the results, for each test performed: - Status DWA Selftest General: -  0: dwa ok (all the following tests ok) -  1: dwa not ok (at least one test not ok) - Status DWA External Voltage Level: -  0: dwa ext V level ok - 15: External Battery voltage &lt; 9V - 19: External Battery voltage &gt; 16V - Status DWA LED: -  0: dwa LED ok - 13: dwa LED failure - Status DWA EEPROM: -  0: dwa EEPROM ok - 60: EEPROM addressing failure - 61: EEPROM access timeout - 62: EEPROM write failure - 63: EEPROM test failure - 64: EEPROM read failure - Status DWA RAM: -  0: dwa RAM ok -  7: dwa RAM hardware failure - Status DWA Internal Battery: -  0: dwa Internal Battery ok - 11: dwa Internal Battery failure - Status DWA Protection Circuit: -  0: dwa Protection Circuit ok - 16: dwa Protection Circuit VS Filter defect - 17: dwa Protection Circuit Sense defect - 18: dwa Protection Circuit external battery_switch off defect - Status DWA ROM: -  0: dwa ROM ok -  6: dwa ROM checksum error - Status DWA Sound Circuit: -  0: dwa Sound Circuit ok -  8: dwa Sound Short Circuit failure -  9: dwa Sound Open Circuit failure - 10: dwa Sound Circuit failure - Status DWA ADXL Circuit: -  0: dwa ADXL ok - 14: dwa ADXL tilt sensor failure - Status DWA Wake Up Circuit: -  0: dwa Wake Up Circuit ok - 20: dwa Wake Up Circuit failure KWP2000: $31 StartRoutineByLocalIdentifier $04 Selftest $09 Cansine
- [STEUERN_DWA_SCHNELLTEST](#job-steuern-dwa-schnelltest) - Activates the 'dwa armed - schnelltest' mode: activates the MUW & ADXL alarm triggers. When the alarm trigger is detected the CANSINE make a siren sound lasting 2s (with normal sound level), then returns to 'dwa disarmed' status The Tilt sensor monitoring starts 5 seconds after sending this command The MUW sensor alarm detectable 10 seconds after sending this command KWP2000: $31 StartRoutineByLocalIdentifier $48 Fast Test $01 normal volume
- [STEUERN_DWA_SCHNELLTEST_LEISE](#job-steuern-dwa-schnelltest-leise) - Activates the 'dwa armed - schnelltest' mode: activates the MUW & ADXL alarm triggers. When the alarm trigger is detected the CANSINE make a siren sound lasting 2s (with lower sound level), then returns to 'dwa disarmed' status The Tilt sensor monitoring starts 5 seconds after sending this command The MUW sensor alarm detectable 10 seconds after sending this command KWP2000: $31 StartRoutineByLocalIdentifier $48 Fast Test $00 low volume
- [STEUERN_MUW_ALARM_LEVELS_RESET](#job-steuern-muw-alarm-levels-reset) - Reset of the last ten alarms voltage levels recorded by the addressed MUW/s (vr,hr,hl,vl,hi,alle). If JOB_STATUS is OK: The 10 MUW/s alarms levels are set to zero. The value '0' means 'no alarm stored in this location. STAT_XX_MUW_ALARM_LEVELS_RESET_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not deleted, and the following error code is shown by STAT_XX_MUW_ALARM_LEVELS_RESET_FEHL - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $49 reset of the MUW alarm levels $xx MUW id
- [STEUERN_MUW_FALSE_WAKEUP_LEVELS_RESET](#job-steuern-muw-false-wakeup-levels-reset) - Reset of the last ten false wakeup levels recorded by the addressed MUW/s (vr,hr,hl,vl,hi,alle). If JOB_STATUS is OK: The 10 MUW/s false wakeup levels are set to 0 The value '0' means 'no level stored in this location. STAT_XX_MUW_F_WK_LEVELS_RESET_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not deleted, and the following error code is shown by STAT_XX_MUW_F_WK_LEVELS_RESET_FEHL - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $50 reset of MUW false wakeup levels $xx MUW id
- [STEUERN_MUW_FUNKTIONSTEST_START](#job-steuern-muw-funktionstest-start) - Set all the configured MUWs into 'Function Test Status' (FTS). When in this status, the MUW will return 'Movement'/'No Movement' detected when queried with job: - STEUERN_MUW_FUNKTIONSTEST After usign this job, wait 15 seconds before using the job STEUERN_MUW_FUNKTIONSTEST MUWs exit this status, upon receipt of any other not related jobs If JOB_STATUS is OK: The MUW/s resulting status is displayed XX_MUW_STAT has value '0' in case no internal error occurred and the MUW is in 'FTS' In case an internal error occurred, the data are not valid, and the following error codes are indicated by XX_MUW_STAT: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $45 MUW funktion test id
- [STEUERN_MUW_FUNKTIONSTEST](#job-steuern-muw-funktionstest) - Queries the addressed (vr, hr, hl, vl, hi, alle) the latched motion detection status. Pre-condition: MUWs has been set to 'Function Test Status' (FTS) with job STEUERN_MUW_FUNKTIONSTEST_START. When in this status, the MUW will return 'Movement'/ 'No Movement'. When the MUW replies, the latched motion is deleted. A warning will advise the user if this job is called for a MUW which is not in FTS If JOB_STATUS is OK: If STAT_MUW has value 0, the MUW's are in FTS and the results are valid. If STAT_MUW has value 1, the MUW's are not in FTS, and the results are not valid: the user must use the job STEUERN_MUW_FUNKTIONSTEST_START The MUW/s resulting status is displayed XX_MUW_STAT has value '0' in case no internal error occurred In case an internal error occurred, the data are not valid, and the following error codes are indicated by XX_MUW_STAT: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $46 MUW funktionstest (project specific $(MUWID)
- [STEUERN_MUW_SELFTEST](#job-steuern-muw-selftest) - Activates a selftest inside the addressed MUW (vr, hr, hl, vl, hi, alle) and report the result. One has to wait at least 10 seconds after MUW Power ON before performing this job. Checked MUW hw: ROM, RAM, EEPROM, RF drive circuit, Address Manager, RF lines. If JOB_STATUS is OK: The MUW/s selftest results  are displayed in XX_MUW_SELFTEST_STAT. The following errors can appear: - 1: ROM check failure - 2: RAM check failure - 3: EEPROM check failure - 4: RF drive failure - 5: Address Manager failure - 6: RF Signal line failure - 7: RF Interference line failure In case an internal error occurred, the data are not valid, and the following error codes are indicated by XX_MUW_SELFTEST_STAT: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $04 Selftest $(MUWID)
- [STEUERN_K_BUS_TEST](#job-steuern-k-bus-test) - Send a test telegram and check the reply from any of the MUW/s (vr, hr, hl, vl, hi, alle) in order to perform a test on the local Dwabus (K-BUS), from the point of view of the connection. If JOB_STATUS is OK: The MUW/s status is displayed: the datum DWABUS_TEST_RESULT has value '0' if no error is present on the local bus. In case an internal error occurred, the following error codes are indicated by DWABUS_TEST_RESULT: - x30: "error DWA BUS PERMANENTLY LOW", i.e. no connection to any of the MUW - x31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - x32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - x33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - x36: "MUW not configured",i.e.: this MUW is not coded on this type of car where x = 1...5 is the ID of the MUW: - 1: VR - 2: HR - 3: HL - 4: VL - 5: HI KWP2000: $31 StartRoutineByLocalIdentifier $40 dwabus id
- [STEUERN_NEIGUNG_X_ZERO](#job-steuern-neigung-x-zero) - Set the zero for the ADXL tilt sensor X axis KWP2000: $31 StartRoutineByLocalIdentifier $41 $0E
- [STEUERN_NEIGUNG_Y_ZERO](#job-steuern-neigung-y-zero) - Set the zero for the ADXL tilt sensor Y axis KWP2000: $31 StartRoutineByLocalIdentifier $41 $0F Modus  : Default

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

<a id="job-hs-lesen"></a>
### HS_LESEN

Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table HOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hs-lesen-detail"></a>
### HS_LESEN_DETAIL

Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Historycode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table HOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
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

<a id="job-hs-loeschen"></a>
### HS_LOESCHEN

Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default

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

<a id="job-gemel-revision-index-ident-id"></a>
### _GEMEL_REVISION_INDEX_IDENT_ID

Readout of the Gemel revision index of the part. This ID is written in EEPROM KWP2000: $21 ReadDataByLocalIdentifier $B8 identifier of the Gemel Rev Ind

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| GEMEL_REVISION_INDEX | unsigned char | identifier of the Gemel Software |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-gemel-appl-sw-ident-id"></a>
### _GEMEL_APPL_SW_IDENT_ID

Readout of the Gemel application software identifier which is written in the ROM KWP2000: $21 ReadDataByLocalIdentifier $A9 identifier of the Gemel Software

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| GEMEL_APPL_SOFTWARE_ID | string | identifier of the Gemel Software |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-gemel-bootloader-sw-ident-id"></a>
### _GEMEL_BOOTLOADER_SW_IDENT_ID

Readout of the bootloader software identifier which is written in the ROM KWP2000: $21 ReadDataByLocalIdentifier $AA identifier of the Gemel Software

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BOOTLOADER_SOFTWARE_ID | string | identifier of the SC version Bootloader Software |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-gemel-muw-seriennummer-lesen"></a>
### _GEMEL_MUW_SERIENNUMMER_LESEN

Reads the SERIAL NUMBER of the addressed MUW (vr,hr,hl,vl,hi,alle) in EEPROM. The S.N. has 9 ASCII characters bytes: - the last two digits of year (2 bytes) - one char for month id: '1','2','3','4','5' '6','7','8','9','A','B','C' (1 byte) - two digits for the day (2 bytes) - the progressive nr. in hex (4 bytes) If JOB_STATUS is OK: The Serial Number (S.N.) is displayed. In case an internal error occurred, the S.N. is not valid, and the following error codes appear: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $21 ReadDataByLocalIdentifier $B2 identifier of the S.N. of MUW's $MUWID identifier of the MUW's

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VR_MUW_SERIENNUMMER_RES | string | MUW SERIENNUMMER by Gemel oder fehler beschreibung |
| HR_MUW_SERIENNUMMER_RES | string | MUW SERIENNUMMER by Gemel oder fehler beschreibung |
| HL_MUW_SERIENNUMMER_RES | string | MUW SERIENNUMMER by Gemel oder fehler beschreibung |
| VL_MUW_SERIENNUMMER_RES | string | MUW SERIENNUMMER by Gemel oder fehler beschreibung |
| HI_MUW_SERIENNUMMER_RES | string | MUW SERIENNUMMER by Gemel oder fehler beschreibung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-gemel-muw-codierung-lesen"></a>
### _GEMEL_MUW_CODIERUNG_LESEN

Reads the CODIERUNG values of all the MUW's In case an internal error occurred, the CODIERUNG values are not valid. KWP2000: $21 ReadDataByLocalIdentifier $B7 identifier of the of MUW's COD.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VR_MUW_CODIERUNG_RES | string | MUW CODIERUNG oder fehler beschreibung |
| HR_MUW_CODIERUNG_RES | string | MUW CODIERUNG oder fehler beschreibung |
| HL_MUW_CODIERUNG_RES | string | MUW CODIERUNG oder fehler beschreibung |
| VL_MUW_CODIERUNG_RES | string | MUW CODIERUNG oder fehler beschreibung |
| HI_MUW_CODIERUNG_RES | string | MUW CODIERUNG oder fehler beschreibung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-gemel-steuern-muw-diag-init"></a>
### _GEMEL_STEUERN_MUW_DIAG_INIT

Init the MUW/s (vr, hr, hl, vl, hi, alle) to the normal (Off) status (from any status). This job can be used during development for removing a MUW deadlock situation (i.e.: MUW not responding) If JOB_STATUS is OK: The MUW/s status is displayed: the datum XX_MUW_STAT has value '0' if the MUW is in status Off (ready). It has values 1,2,3 in case the MUW is responding but is in other status than Off (On, Sleep, Alarm) In case an internal error occurred, the following error codes are indicated by XX_MUW_STAT: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $39 Muw status to Off

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| VR_MUW_STAT | int | muw ready - muw not ready |
| HR_MUW_STAT | int | muw ready - muw not ready |
| HL_MUW_STAT | int | muw ready - muw not ready |
| VL_MUW_STAT | int | muw ready - muw not ready |
| HI_MUW_STAT | int | muw ready - muw not ready |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-muw"></a>
### IDENT_MUW

Reads the identification data of the addressed MUW (vr,hr,hl,vl,hi,alle) The MUW identification data are: - Developer ID - MUW Message Catalogue Version - MUW Functional SW Version - MUW Hardware Index - MUW Part Number - MUW Address If JOB_STATUS is OK: All the above data are displayed. The datum XX_MUW_FEHLER_STATUS has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error codes are indicated by XX_MUW_FEHLER_STATUS: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $22 ReadDataByCommonIdentifier $40 ident MuW (project specific)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, when without errors table JobResult STATUS_TEXT |
| VR_MUW_FEHLER_STATUS | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| VR_MUW_FEHLER_STATUS_TEXT | string | Error text |
| VR_MUW_ENTWICKLER_ID | string | Name der Firme Entwickler MuW |
| VR_MUW_NACHR_KATALOG | int | Version nachrichte kommunikation DWA - MUW |
| VR_MUW_SW_FSV_NUMMER | string | Version software MUW |
| VR_MUW_HARDWARE_NUMM | int | Version hardware MUW |
| VR_MUW_COD_PART_NUMM | string | BMW Part Nummer |
| VR_MUW_ADDRESSE_NUMM | int | Addresse auf der MUW |
| HR_MUW_FEHLER_STATUS | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| HR_MUW_FEHLER_STATUS_TEXT | string | Error text |
| HR_MUW_ENTWICKLER_ID | string | Name der Firme Entwickler MuW |
| HR_MUW_NACHR_KATALOG | int | Version nachrichte kommunikation DWA - MUW |
| HR_MUW_SW_FSV_NUMMER | string | Version software MUW |
| HR_MUW_HARDWARE_NUMM | int | Version hardware MUW |
| HR_MUW_COD_PART_NUMM | string | BMW Part Nummer |
| HR_MUW_ADDRESSE_NUMM | int | Addresse auf der MUW |
| HL_MUW_FEHLER_STATUS | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| HL_MUW_FEHLER_STATUS_TEXT | string | Error text |
| HL_MUW_ENTWICKLER_ID | string | Name der Firme Entwickler MuW |
| HL_MUW_NACHR_KATALOG | int | Version nachrichte kommunikation DWA - MUW |
| HL_MUW_SW_FSV_NUMMER | string | Version software MUW |
| HL_MUW_HARDWARE_NUMM | int | Version hardware MUW |
| HL_MUW_COD_PART_NUMM | string | BMW Part Nummer |
| HL_MUW_ADDRESSE_NUMM | int | Addresse auf der MUW |
| VL_MUW_FEHLER_STATUS | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| VL_MUW_FEHLER_STATUS_TEXT | string | Error text |
| VL_MUW_ENTWICKLER_ID | string | Name der Firme Entwickler MuW |
| VL_MUW_NACHR_KATALOG | int | Version nachrichte kommunikation DWA - MUW |
| VL_MUW_SW_FSV_NUMMER | string | Version software MUW |
| VL_MUW_HARDWARE_NUMM | int | Version hardware MUW |
| VL_MUW_COD_PART_NUMM | string | BMW Part Nummer |
| VL_MUW_ADDRESSE_NUMM | int | Addresse auf der MUW |
| HI_MUW_FEHLER_STATUS | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| HI_MUW_FEHLER_STATUS_TEXT | string | Error text |
| HI_MUW_ENTWICKLER_ID | string | Name der Firme Entwickler MuW |
| HI_MUW_NACHR_KATALOG | int | Version nachrichte kommunikation DWA - MUW |
| HI_MUW_SW_FSV_NUMMER | string | Version software MUW |
| HI_MUW_HARDWARE_NUMM | int | Version hardware MUW |
| HI_MUW_COD_PART_NUMM | string | BMW Part Nummer |
| HI_MUW_ADDRESSE_NUMM | int | Addresse auf der MUW |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-car-key-memory"></a>
### STATUS_CAR_KEY_MEMORY

Readout of the CKM parameters from RAM (currently used by the DWA Cansine) KWP2000: $21 ReadDataByLocalIdentifier $B0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_QUIT_OPTIC_ENTSCHAERFEN | int | 0: inaktiv 1: aktiv |
| STAT_QUIT_OPTIC_SCHAERFEN | int | 0: inaktiv 1: aktiv |
| STAT_QUIT_OPTIC_SCHAERFEN_KLAPPE | int | 0: inaktiv 1: aktiv |
| STAT_QUIT_AKUSTIC_ENTSCHAERFEN | int | 0: inaktiv 1: aktiv |
| STAT_QUIT_AKUSTIC_SCHAERFEN | int | 0: inaktiv 1: aktiv |
| STAT_QUIT_AKUSTIC_SCHAERFEN_KLAPPE | int | 0: inaktiv 1: aktiv |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dwa-klemme-30"></a>
### STATUS_DWA_KLEMME_30

Readout of the external battery supply voltage KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $02 external supply voltage

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DWA_KLEMME_30_WERT | int | Spannung Klemme 30 an der DWA |
| STAT_DWA_KLEMME_30_EINH | string | Einheit Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-muw-klemme-30"></a>
### STATUS_MUW_KLEMME_30

Readout of the supply voltage of the addressed MUW (vr,hr,hl,vl,hi,alle). The MUW supply voltage has a resolution of 1 Volt If JOB_STATUS is OK: The MUW/s voltage is displayed. The datum STAT_XX_MUW_KLEMME_30_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error codes are indicated by STAT_XX_MUW_KLEMME_30_FEHL: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VR_MUW_KLEMME_30_FEHL | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_VR_MUW_KLEMME_30_WERT | int | Spannung Klemme 30 an der DWA |
| STAT_HR_MUW_KLEMME_30_FEHL | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HR_MUW_KLEMME_30_WERT | int | Spannung Klemme 30 an der DWA |
| STAT_HL_MUW_KLEMME_30_FEHL | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HL_MUW_KLEMME_30_WERT | int | Spannung Klemme 30 an der DWA |
| STAT_VL_MUW_KLEMME_30_FEHL | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_VL_MUW_KLEMME_30_WERT | int | Spannung Klemme 30 an der DWA |
| STAT_HI_MUW_KLEMME_30_FEHL | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HI_MUW_KLEMME_30_WERT | int | Spannung Klemme 30 an der DWA |
| STAT_VR_MUW_KLEMME_30_FEHL_TEXT | string | Error text |
| STAT_HR_MUW_KLEMME_30_FEHL_TEXT | string | Error text |
| STAT_HL_MUW_KLEMME_30_FEHL_TEXT | string | Error text |
| STAT_VL_MUW_KLEMME_30_FEHL_TEXT | string | Error text |
| STAT_HI_MUW_KLEMME_30_FEHL_TEXT | string | Error text |
| STAT_EINHEIT_MUW_KLEMME_30 | string | Einheit Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dwa-temperatur"></a>
### STATUS_DWA_TEMPERATUR

Readout of the internal temperature on the DWA PCB of the Cansine - wait ca. 30 seconds after Cansine power on KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $08 parameter DWA temperature

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DWA_INTERN_TEMP_WERT | char | Wert Temperatur an der DWA |
| STAT_DWA_INTERN_TEMP_EINH | string | Einheit Grad C |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-muw-temperatur"></a>
### STATUS_MUW_TEMPERATUR

Readout of the MUW internal temperature of the addressed MUW (vr,hr,hl,vl,hi,alle). Wait at least 2 seconds after Power ON before executing this job. If JOB_STATUS is OK: The MUW/s voltage is displayed. The datum STAT_XX_MUW_TEMP_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error codes are indicated by STAT_XX_MUW_TEMP_FEHL: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $30 InputOutputControlByLocalIdentifier $0A MUW_TEMPERATUR $02 ReportIOconditions $xx identifiers of MUW

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VR_MUW_TEMP_FEHL | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_VR_MUW_TEMP_WERT | char | Wert Temperatur an der DWA |
| STAT_HR_MUW_TEMP_FEHL | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HR_MUW_TEMP_WERT | char | Wert Temperatur an der DWA |
| STAT_HL_MUW_TEMP_FEHL | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HL_MUW_TEMP_WERT | char | Wert Temperatur an der DWA |
| STAT_VL_MUW_TEMP_FEHL | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_VL_MUW_TEMP_WERT | char | Wert Temperatur an der DWA |
| STAT_HI_MUW_TEMP_FEHL | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HI_MUW_TEMP_WERT | char | Wert Temperatur an der DWA |
| STAT_MUW_TEMP_EINH | string | Einheit Grad C |
| STAT_VR_MUW_TEMP_FEHL_TEXT | string | Error text |
| STAT_HR_MUW_TEMP_FEHL_TEXT | string | Error text |
| STAT_HL_MUW_TEMP_FEHL_TEXT | string | Error text |
| STAT_VL_MUW_TEMP_FEHL_TEXT | string | Error text |
| STAT_HI_MUW_TEMP_FEHL_TEXT | string | Error text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dwa-led"></a>
### STATUS_DWA_LED

Readout of the DWA LED status (on=1, off=0) KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $01 status of the DWA LED

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DWA_LED | int | ein - aus |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dwa-alarmtrigger"></a>
### STATUS_DWA_ALARMTRIGGER

Readout of the alarm trigger status of the DWA For the MUW related alarm trigger, the system must be armed, for other alarm triggers, the system can be armed or disarmed KWP2000: $21 ReadDataByLocalIdentifier $A0 identifier of the ALARM_TRIGGER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FAT_AUSGEL | int | tuer offenen |
| STAT_BFT_AUSGEL | int | tuer offenen |
| STAT_FATH_AUSGEL | int | tuer offenen |
| STAT_BFTH_AUSGEL | int | tuer offenen |
| STAT_HK_AUSGEL | int | tuer offenen |
| STAT_MH_AUSGEL | int | tuer offenen |
| STAT_NG_AUSGEL | int | neigungsgeber alarm |
| STAT_MUW_AUSGEL | int | muw alarm |
| STAT_KBUS_AUSGEL | int | Kbus manipulation |
| STAT_DISTRIBUTION_AUSGEL | int | distribution alarm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dwa-intern"></a>
### STATUS_DWA_INTERN

Readout of the application status of the CANSINE. The following statuses are possible: -  0: dwa disarmed -  1: dwa arming -  2: dwa armed -  3: dwa disarming -  4: dwa alarm -  5: dwa dwa pause after alarm -  6: dwa transport mode -  7: dwa werkstatt mode -  9: dwa armed - MUW & Tilt Sensor deactivated by User - 10: dwa armed - distribution mode - 11: dwa ending energiesparmode - 12: dwa powerdown mode - 13: dwa panik alarm mode - 14: dwa armed - hotelstellung active - 15: dwa armed- MUW & Tilt Sensor not active - 16: dwa armed - MUW not active - 17: dwa armed - Tilt Sensor not active - 18: dwa schnelltest active - 19: dwa armed - MUW & Tilt Sensor referencing - 20: dwa armed - MUW referencing - 21: dwa armed - Tilt Sensor referencing KWP2000: $21 ReadDataByLocalIdentifier $A1 identifier of the DWA_STS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DWA_INTERN | int | dwa application status |
| STAT_DWA_INTERN_TEXT | string | dwa application status |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-muw-intern"></a>
### STATUS_MUW_INTERN

Readout of the MUW status of the addressed MUW (vr, hr, hl, vl, hi, alle). The following statuses are shown: - MUW communication error status - MUW internal error code - Number of intrusions recorded The Number of Intrusions detected is reset after this job is executed. If JOB_STATUS is OK: The MUW/s voltage is displayed. The datum STAT_XX_MUW_KOMM_FEHLER has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error codes are indicated by STAT_XX_MUW_KOMM_FEHLER: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $21 ReadDataByLocalIdentifier $A3 identifier of the MUW status

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VR_MUW_KOMM_FEHLER | int | 0 : MUW ok 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_VR_MUW_INTERN_FEHL | int | 0=OK - weitere coden bei GEMEL |
| STAT_VR_MUW_ALARM_ZAEHL | unsigned int | nummer abfragung von letzte STATUS_MUW_INTERN - MUW EIN sequenz |
| STAT_HR_MUW_KOMM_FEHLER | int | 0 : MUW ok 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HR_MUW_INTERN_FEHL | int | 0=OK - weitere coden bei GEMEL |
| STAT_HR_MUW_ALARM_ZAEHL | unsigned int | nummer abfragung von letzte STATUS_MUW_INTERN - MUW EIN sequenz |
| STAT_HL_MUW_KOMM_FEHLER | int | 0 : MUW ok 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HL_MUW_INTERN_FEHL | int | 0=OK - weitere coden bei GEMEL |
| STAT_HL_MUW_ALARM_ZAEHL | unsigned int | nummer abfragung von letzte STATUS_MUW_INTERN - MUW EIN sequenz |
| STAT_VL_MUW_KOMM_FEHLER | int | 0 : MUW ok 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_VL_MUW_INTERN_FEHL | int | 0=OK - weitere coden bei GEMEL |
| STAT_VL_MUW_ALARM_ZAEHL | unsigned int | nummer abfragung von letzte STATUS_MUW_INTERN - MUW EIN sequenz |
| STAT_HI_MUW_KOMM_FEHLER | int | 0 : MUW ok 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HI_MUW_INTERN_FEHL | int | 0=OK - weitere coden bei GEMEL |
| STAT_HI_MUW_ALARM_ZAEHL | unsigned int | nummer abfragung von letzte STATUS_MUW_INTERN - MUW EIN sequenz |
| STAT_VR_MUW_KOMM_FEHLER_TEXT | string | Error text |
| STAT_HR_MUW_KOMM_FEHLER_TEXT | string | Error text |
| STAT_HL_MUW_KOMM_FEHLER_TEXT | string | Error text |
| STAT_VL_MUW_KOMM_FEHLER_TEXT | string | Error text |
| STAT_HI_MUW_KOMM_FEHLER_TEXT | string | Error text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-muw-alarm-levels"></a>
### STATUS_MUW_ALARM_LEVELS

Readout of the last ten alarms voltage levels of the addressed MUW/s (vr,hr,hl,vl,hi,alle) The MUW alarm level value has a resolution of 5mV for parts with FSV550 or lower, and of 20mV for FSV higher or equal than FSV560 If JOB_STATUS is OK: The 10 MUW/s alarms levels are displayed. The value '0' means 'no alarm stored in this location. STAT_XX_MUW_ALARM_LEVELS_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error code is shown by STAT_XX_MUW_ALARM_LEVELS_FEHL: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $11 status of the MUW alarm levels $xx MUW id

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VR_MUW_ALARM_LEVELS_FEHL | int | MUW fehler |
| STAT_VR_MUW_ALARM_LEVEL_1_WERT | int | Alarm level an der MUW VR |
| STAT_VR_MUW_ALARM_LEVEL_2_WERT | int | Alarm level an der MUW VR |
| STAT_VR_MUW_ALARM_LEVEL_3_WERT | int | Alarm level an der MUW VR |
| STAT_VR_MUW_ALARM_LEVEL_4_WERT | int | Alarm level an der MUW VR |
| STAT_VR_MUW_ALARM_LEVEL_5_WERT | int | Alarm level an der MUW VR |
| STAT_VR_MUW_ALARM_LEVEL_6_WERT | int | Alarm level an der MUW VR |
| STAT_VR_MUW_ALARM_LEVEL_7_WERT | int | Alarm level an der MUW VR |
| STAT_VR_MUW_ALARM_LEVEL_8_WERT | int | Alarm level an der MUW VR |
| STAT_VR_MUW_ALARM_LEVEL_9_WERT | int | Alarm level an der MUW VR |
| STAT_VR_MUW_ALARM_LEVEL_10_WERT | int | Alarm level an der MUW VR |
| STAT_HR_MUW_ALARM_LEVELS_FEHL | int | MUW fehler |
| STAT_HR_MUW_ALARM_LEVEL_1_WERT | int | Alarm level an der MUW HR |
| STAT_HR_MUW_ALARM_LEVEL_2_WERT | int | Alarm level an der MUW HR |
| STAT_HR_MUW_ALARM_LEVEL_3_WERT | int | Alarm level an der MUW HR |
| STAT_HR_MUW_ALARM_LEVEL_4_WERT | int | Alarm level an der MUW HR |
| STAT_HR_MUW_ALARM_LEVEL_5_WERT | int | Alarm level an der MUW HR |
| STAT_HR_MUW_ALARM_LEVEL_6_WERT | int | Alarm level an der MUW HR |
| STAT_HR_MUW_ALARM_LEVEL_7_WERT | int | Alarm level an der MUW HR |
| STAT_HR_MUW_ALARM_LEVEL_8_WERT | int | Alarm level an der MUW HR |
| STAT_HR_MUW_ALARM_LEVEL_9_WERT | int | Alarm level an der MUW HR |
| STAT_HR_MUW_ALARM_LEVEL_10_WERT | int | Alarm level an der MUW HR |
| STAT_HL_MUW_ALARM_LEVELS_FEHL | int | MUW fehler |
| STAT_HL_MUW_ALARM_LEVEL_1_WERT | int | Alarm level an der MUW HL |
| STAT_HL_MUW_ALARM_LEVEL_2_WERT | int | Alarm level an der MUW HL |
| STAT_HL_MUW_ALARM_LEVEL_3_WERT | int | Alarm level an der MUW HL |
| STAT_HL_MUW_ALARM_LEVEL_4_WERT | int | Alarm level an der MUW HL |
| STAT_HL_MUW_ALARM_LEVEL_5_WERT | int | Alarm level an der MUW HL |
| STAT_HL_MUW_ALARM_LEVEL_6_WERT | int | Alarm level an der MUW HL |
| STAT_HL_MUW_ALARM_LEVEL_7_WERT | int | Alarm level an der MUW HL |
| STAT_HL_MUW_ALARM_LEVEL_8_WERT | int | Alarm level an der MUW HL |
| STAT_HL_MUW_ALARM_LEVEL_9_WERT | int | Alarm level an der MUW HL |
| STAT_HL_MUW_ALARM_LEVEL_10_WERT | int | Alarm level an der MUW HL |
| STAT_VL_MUW_ALARM_LEVELS_FEHL | int | MUW fehler |
| STAT_VL_MUW_ALARM_LEVEL_1_WERT | int | Alarm level an der MUW VL |
| STAT_VL_MUW_ALARM_LEVEL_2_WERT | int | Alarm level an der MUW VL |
| STAT_VL_MUW_ALARM_LEVEL_3_WERT | int | Alarm level an der MUW VL |
| STAT_VL_MUW_ALARM_LEVEL_4_WERT | int | Alarm level an der MUW VL |
| STAT_VL_MUW_ALARM_LEVEL_5_WERT | int | Alarm level an der MUW VL |
| STAT_VL_MUW_ALARM_LEVEL_6_WERT | int | Alarm level an der MUW VL |
| STAT_VL_MUW_ALARM_LEVEL_7_WERT | int | Alarm level an der MUW VL |
| STAT_VL_MUW_ALARM_LEVEL_8_WERT | int | Alarm level an der MUW VL |
| STAT_VL_MUW_ALARM_LEVEL_9_WERT | int | Alarm level an der MUW VL |
| STAT_VL_MUW_ALARM_LEVEL_10_WERT | int | Alarm level an der MUW VL |
| STAT_HI_MUW_ALARM_LEVELS_FEHL | int | MUW fehler |
| STAT_HI_MUW_ALARM_LEVEL_1_WERT | int | Alarm level an der MUW HI |
| STAT_HI_MUW_ALARM_LEVEL_2_WERT | int | Alarm level an der MUW HI |
| STAT_HI_MUW_ALARM_LEVEL_3_WERT | int | Alarm level an der MUW HI |
| STAT_HI_MUW_ALARM_LEVEL_4_WERT | int | Alarm level an der MUW HI |
| STAT_HI_MUW_ALARM_LEVEL_5_WERT | int | Alarm level an der MUW HI |
| STAT_HI_MUW_ALARM_LEVEL_6_WERT | int | Alarm level an der MUW HI |
| STAT_HI_MUW_ALARM_LEVEL_7_WERT | int | Alarm level an der MUW HI |
| STAT_HI_MUW_ALARM_LEVEL_8_WERT | int | Alarm level an der MUW HI |
| STAT_HI_MUW_ALARM_LEVEL_9_WERT | int | Alarm level an der MUW HI |
| STAT_HI_MUW_ALARM_LEVEL_10_WERT | int | Alarm level an der MUW HI |
| STAT_EINHEIT_MUW_ALARM_LEVELS | string | Einheit milliVolts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-muw-false-wakeup-levels"></a>
### STATUS_MUW_FALSE_WAKEUP_LEVELS

Readout of the last ten false wakeup levels (wakeup not leading to alarm) of the addressed MUW/s (vr,hr,hl,vl,hi,alle). The MUW alarm level value has a resolution of 5mV for parts with FSV550 or lower, and of 20mV for FSV higher or equal than FSV560 If JOB_STATUS is OK: The 10 MUW/s false wakeup levels are displayed. The value '0' means 'no alarm stored in this location. STAT_XX_MUW_F_WAKEUP_LEVELS_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error code is shown by STAT_XX_MUW_F_WAKEUP_LEVELS_FEHL: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $12 status of the MUW F wakeup level $xx MUW id

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VR_MUW_F_WAKEUP_LEVELS_FEHL | int | MUW fehler |
| STAT_VR_MUW_F_WAKEUP_LEVEL_1_WERT | int | False wakeup level an der MUW VR |
| STAT_VR_MUW_F_WAKEUP_LEVEL_2_WERT | int | False wakeup level an der MUW VR |
| STAT_VR_MUW_F_WAKEUP_LEVEL_3_WERT | int | False wakeup level an der MUW VR |
| STAT_VR_MUW_F_WAKEUP_LEVEL_4_WERT | int | False wakeup level an der MUW VR |
| STAT_VR_MUW_F_WAKEUP_LEVEL_5_WERT | int | False wakeup level an der MUW VR |
| STAT_VR_MUW_F_WAKEUP_LEVEL_6_WERT | int | False wakeup level an der MUW VR |
| STAT_VR_MUW_F_WAKEUP_LEVEL_7_WERT | int | False wakeup level an der MUW VR |
| STAT_VR_MUW_F_WAKEUP_LEVEL_8_WERT | int | False wakeup level an der MUW VR |
| STAT_VR_MUW_F_WAKEUP_LEVEL_9_WERT | int | False wakeup level an der MUW VR |
| STAT_VR_MUW_F_WAKEUP_LEVEL_10_WERT | int | False wakeup level an der MUW VR |
| STAT_HR_MUW_F_WAKEUP_LEVELS_FEHL | int | MUW fehler |
| STAT_HR_MUW_F_WAKEUP_LEVEL_1_WERT | int | False wakeup level an der MUW HR |
| STAT_HR_MUW_F_WAKEUP_LEVEL_2_WERT | int | False wakeup level an der MUW HR |
| STAT_HR_MUW_F_WAKEUP_LEVEL_3_WERT | int | False wakeup level an der MUW HR |
| STAT_HR_MUW_F_WAKEUP_LEVEL_4_WERT | int | False wakeup level an der MUW HR |
| STAT_HR_MUW_F_WAKEUP_LEVEL_5_WERT | int | False wakeup level an der MUW HR |
| STAT_HR_MUW_F_WAKEUP_LEVEL_6_WERT | int | False wakeup level an der MUW HR |
| STAT_HR_MUW_F_WAKEUP_LEVEL_7_WERT | int | False wakeup level an der MUW HR |
| STAT_HR_MUW_F_WAKEUP_LEVEL_8_WERT | int | False wakeup level an der MUW HR |
| STAT_HR_MUW_F_WAKEUP_LEVEL_9_WERT | int | False wakeup level an der MUW HR |
| STAT_HR_MUW_F_WAKEUP_LEVEL_10_WERT | int | False wakeup level an der MUW HR |
| STAT_HL_MUW_F_WAKEUP_LEVELS_FEHL | int | MUW fehler |
| STAT_HL_MUW_F_WAKEUP_LEVEL_1_WERT | int | False wakeup level an der MUW HL |
| STAT_HL_MUW_F_WAKEUP_LEVEL_2_WERT | int | False wakeup level an der MUW HL |
| STAT_HL_MUW_F_WAKEUP_LEVEL_3_WERT | int | False wakeup level an der MUW HL |
| STAT_HL_MUW_F_WAKEUP_LEVEL_4_WERT | int | False wakeup level an der MUW HL |
| STAT_HL_MUW_F_WAKEUP_LEVEL_5_WERT | int | False wakeup level an der MUW HL |
| STAT_HL_MUW_F_WAKEUP_LEVEL_6_WERT | int | False wakeup level an der MUW HL |
| STAT_HL_MUW_F_WAKEUP_LEVEL_7_WERT | int | False wakeup level an der MUW HL |
| STAT_HL_MUW_F_WAKEUP_LEVEL_8_WERT | int | False wakeup level an der MUW HL |
| STAT_HL_MUW_F_WAKEUP_LEVEL_9_WERT | int | False wakeup level an der MUW HL |
| STAT_HL_MUW_F_WAKEUP_LEVEL_10_WERT | int | False wakeup level an der MUW HL |
| STAT_VL_MUW_F_WAKEUP_LEVELS_FEHL | int | MUW fehler |
| STAT_VL_MUW_F_WAKEUP_LEVEL_1_WERT | int | False wakeup level an der MUW VL |
| STAT_VL_MUW_F_WAKEUP_LEVEL_2_WERT | int | False wakeup level an der MUW VL |
| STAT_VL_MUW_F_WAKEUP_LEVEL_3_WERT | int | False wakeup level an der MUW VL |
| STAT_VL_MUW_F_WAKEUP_LEVEL_4_WERT | int | False wakeup level an der MUW VL |
| STAT_VL_MUW_F_WAKEUP_LEVEL_5_WERT | int | False wakeup level an der MUW VL |
| STAT_VL_MUW_F_WAKEUP_LEVEL_6_WERT | int | False wakeup level an der MUW VL |
| STAT_VL_MUW_F_WAKEUP_LEVEL_7_WERT | int | False wakeup level an der MUW VL |
| STAT_VL_MUW_F_WAKEUP_LEVEL_8_WERT | int | False wakeup level an der MUW VL |
| STAT_VL_MUW_F_WAKEUP_LEVEL_9_WERT | int | False wakeup level an der MUW VL |
| STAT_VL_MUW_F_WAKEUP_LEVEL_10_WERT | int | False wakeup level an der MUW VL |
| STAT_HI_MUW_F_WAKEUP_LEVELS_FEHL | int | MUW fehler |
| STAT_HI_MUW_F_WAKEUP_LEVEL_1_WERT | int | False wakeup level an der MUW HI |
| STAT_HI_MUW_F_WAKEUP_LEVEL_2_WERT | int | False wakeup level an der MUW HI |
| STAT_HI_MUW_F_WAKEUP_LEVEL_3_WERT | int | False wakeup level an der MUW HI |
| STAT_HI_MUW_F_WAKEUP_LEVEL_4_WERT | int | False wakeup level an der MUW HI |
| STAT_HI_MUW_F_WAKEUP_LEVEL_5_WERT | int | False wakeup level an der MUW HI |
| STAT_HI_MUW_F_WAKEUP_LEVEL_6_WERT | int | False wakeup level an der MUW HI |
| STAT_HI_MUW_F_WAKEUP_LEVEL_7_WERT | int | False wakeup level an der MUW HI |
| STAT_HI_MUW_F_WAKEUP_LEVEL_8_WERT | int | False wakeup level an der MUW HI |
| STAT_HI_MUW_F_WAKEUP_LEVEL_9_WERT | int | False wakeup level an der MUW HI |
| STAT_HI_MUW_F_WAKEUP_LEVEL_10_WERT | int | False wakeup level an der MUW HI |
| STAT_EINHEIT_MUW_F_WAKEUP_LEVELS | string | Einheit milliVolts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-muw-noise"></a>
### STATUS_MUW_NOISE

Readout of the MUW noise level of the addressed MUW (vr, hr, hl, vl, hi). The local noise measurement takes approx 5s for each MUW. If JOB_STATUS is OK: The MUW/s noise level is displayed in mV. Each MUW returns a value from 0 to 255, in in multiples of 5mV or 20mV The MUW noise level value has a resolution of 5mV for parts with FSV550 or lower, and of 20mV for FSV higher or equal than FSV560 This value is then converted and displayed in mV. STAT_XX_MUW_KOMM_FEHLER has value '0' in case no internal error occurred. In case an internal error occurred, the data are not valid, and the following error codes are indicated by STAT_XX_MUW_KOMM_FEHLER: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VR_MUW_KOMM_FEHLER | int | MUW ok - MUW nicht i.O. |
| STAT_VR_MUW_NOISE_LEVEL | int | 0=OK - weitere coden bei GEMEL |
| STAT_HR_MUW_KOMM_FEHLER | int | MUW ok - MUW nicht i.O. |
| STAT_HR_MUW_NOISE_LEVEL | int | 0=OK - weitere coden bei GEMEL |
| STAT_HL_MUW_KOMM_FEHLER | int | MUW ok - MUW nicht i.O. |
| STAT_HL_MUW_NOISE_LEVEL | int | 0=OK - weitere coden bei GEMEL |
| STAT_VL_MUW_KOMM_FEHLER | int | MUW ok - MUW nicht i.O. |
| STAT_VL_MUW_NOISE_LEVEL | int | 0=OK - weitere coden bei GEMEL |
| STAT_HI_MUW_KOMM_FEHLER | int | MUW ok - MUW nicht i.O. |
| STAT_HI_MUW_NOISE_LEVEL | int | 0=OK - weitere coden bei GEMEL |
| STAT_EINH_MUW_NOISE_LEVEL | string | Einheit milliVolts (peak to peak) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-neigung-x-achse"></a>
### STATUS_NEIGUNG_X_ACHSE

Readout of the current angle value in degrees, given by the inclination sensor of the DWA KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $0E id. of the ADXL X angle

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_NEIGUNG_X_ACHSE_ANGLE_WERT | real | Wert X 'Angle' neigungsensor an der DWA |
| STAT_NEIGUNG_X_ACHSE_EINH | string | degree of angle |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-neigung-y-achse"></a>
### STATUS_NEIGUNG_Y_ACHSE

Readout of the current angle value in degrees, given by the inclination sensor of the DWA KWP2000: $30 InputOutputControlByLocalIdentifier $02 ReportIOconditions $0F id. of the ADXL Y angle

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_NEIGUNG_Y_ACHSE_ANGLE_WERT | real | Wert X 'Angle' neigungsensor an der DWA |
| STAT_NEIGUNG_Y_ACHSE_EINH | string | degree |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-interner-batterie-level"></a>
### STATUS_INTERNER_BATTERIE_LEVEL

Readout of the current residual level of the internal battery. The possible levels are: - 1: empty - 2: good - 3: new KWP2000: $21 ReadDataByLocalIdentifier $A8 identifier of the internal battery level of charge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_INT_BATTERY_LEVEL_WERT | int | 1: empty 2: good 3: new |
| STAT_INT_BATTERY_LEVEL_TEXT | string | Level text |
| STAT_N_OF_SELF_SUPPLIED_CYCLES | int | number of self supplied alarms |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-interner-batterie-wechsel"></a>
### INTERNER_BATTERIE_WECHSEL

Set the current consumption status of the internal battery to '3:New'. This operation has to be done with new batteries KWP2000: $3B WriteDataByLocalIdentifier $A8 identifier of the internal battery level of charge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_INT_BATTERY_LEVEL_WERT | int | 1: empty 2: good 3: new |
| STAT_INT_BATTERY_LEVEL_TEXT | string | Level Text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-led"></a>
### STEUERN_DWA_LED

Set the status of the DWA LED to 'ein', 'aus' KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIGITALWERT | string | Erklaerung Werte: true, false table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-schaerfen"></a>
### STEUERN_DWA_SCHAERFEN

Set the DWA to the armed ('ein') or disarmed ('aus') status KWP2000: $31 StartRoutineByLocalIdentifier $43 id for Schaerfen/Entschaerfen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIGITALWERT | string | Werte: ein(1), aus(0) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sirene-ein-aus"></a>
### STEUERN_SIRENE_EIN_AUS

Start ('ein') the siren sound, timeout ca. 30s Stop ('aus') the current sound before timeout KWP2000: $31 StartRoutineByLocalIdentifier $44 Sirene identifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIGITALWERT | string | Werte: ein(1), aus(0) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-selftest"></a>
### STEUERN_DWA_SELFTEST

Perform an hardware selftest of the DWA and report the results, for each test performed: - Status DWA Selftest General: -  0: dwa ok (all the following tests ok) -  1: dwa not ok (at least one test not ok) - Status DWA External Voltage Level: -  0: dwa ext V level ok - 15: External Battery voltage &lt; 9V - 19: External Battery voltage &gt; 16V - Status DWA LED: -  0: dwa LED ok - 13: dwa LED failure - Status DWA EEPROM: -  0: dwa EEPROM ok - 60: EEPROM addressing failure - 61: EEPROM access timeout - 62: EEPROM write failure - 63: EEPROM test failure - 64: EEPROM read failure - Status DWA RAM: -  0: dwa RAM ok -  7: dwa RAM hardware failure - Status DWA Internal Battery: -  0: dwa Internal Battery ok - 11: dwa Internal Battery failure - Status DWA Protection Circuit: -  0: dwa Protection Circuit ok - 16: dwa Protection Circuit VS Filter defect - 17: dwa Protection Circuit Sense defect - 18: dwa Protection Circuit external battery_switch off defect - Status DWA ROM: -  0: dwa ROM ok -  6: dwa ROM checksum error - Status DWA Sound Circuit: -  0: dwa Sound Circuit ok -  8: dwa Sound Short Circuit failure -  9: dwa Sound Open Circuit failure - 10: dwa Sound Circuit failure - Status DWA ADXL Circuit: -  0: dwa ADXL ok - 14: dwa ADXL tilt sensor failure - Status DWA Wake Up Circuit: -  0: dwa Wake Up Circuit ok - 20: dwa Wake Up Circuit failure KWP2000: $31 StartRoutineByLocalIdentifier $04 Selftest $09 Cansine

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DWA_SELFTEST_GENERAL | int | 0: dwa ok (all the following tests ok) 1: dwa not ok (at least one test not ok) |
| STAT_DWA_EXT_V_LEV | int | 0:  Dwa ext V level ok 15: External Battery voltage &lt; 9V 19: External Battery voltage &gt; 16V |
| STAT_DWA_LED | int | 0:  dwa LED ok 13: dwa LED failure |
| STAT_DWA_EEPROM | int | 0:  dwa EEPROM ok 60: EEPROM addressing failure 61: EEPROM access timeout 62: EEPROM write failure 63: EEPROM test failure 64: EEPROM read failure |
| STAT_DWA_RAM | int | 0: dwa RAM ok 7: dwa RAM hardware failure |
| STAT_DWA_INTERNAL_BATTERY | int | 0:  dwa Internal Battery ok 11: dwa Internal Battery failure |
| STAT_DWA_PROTECTION_CIRCUIT | int | 0:  dwa Protection Circuit ok 16: dwa Protection Circuit VS Filter defect 17: dwa Protection Circuit Sense defect 18: dwa Protection Circuit external battery_switch off defect |
| STAT_DWA_ROM | int | 0: dwa ROM ok 6: dwa ROM checksum error |
| STAT_DWA_SOUND_CIRCUIT | int | 0:  dwa Sound Circuit ok 8:  dwa Sound Short Circuit failure 9:  dwa Sound Open Circuit failure 10: dwa Sound Circuit failure |
| STAT_DWA_ADXL_CIRCUIT | int | 0:  dwa ADXL ok 14: dwa ADXL tilt sensor failure |
| STAT_DWA_WAKEUP_CIRCUIT | int | 0:  dwa Wake Up Circuit ok 20: dwa Wake Up Circuit failure |
| STAT_DWA_SELFTEST_GENERAL_TEXT | string | dwa ok - dwa not ok |
| STAT_DWA_EXT_V_LEV_TEXT | string | dwa ext V level ok - External Battery voltage &lt; 9V - External Battery voltage &gt; 16V |
| STAT_DWA_LED_TEXT | string | dwa LED ok - dwa LED failure |
| STAT_DWA_EEPROM_TEXT | string | dwa EEPROM ok - EEPROM addressing failure - EEPROM access timeout - EEPROM write failure - EEPROM test failure - EEPROM read failure |
| STAT_DWA_RAM_TEXT | string | dwa RAM ok - dwa RAM hardware failure |
| STAT_DWA_INTERNAL_BATTERY_TEXT | string | dwa Internal Battery ok - dwa Internal Battery failure |
| STAT_DWA_PROTECTION_CIRCUIT_TEXT | string | dwa Protection Circuit ok - dwa Protection Circuit VS Filter defect - dwa Protection Circuit Sense defect - dwa Protection Circuit external battery switch off defect |
| STAT_DWA_ROM_TEXT | string | dwa ROM ok - dwa ROM checksum error |
| STAT_DWA_SOUND_CIRCUIT_TEXT | string | dwa Sound Circuit ok - dwa Sound Short Circuit failure - dwa Sound Open Circuit failure - dwa Sound Circuit failure |
| STAT_DWA_ADXL_CIRCUIT_TEXT | string | dwa ADXL ok - dwa ADXL tilt sensor failure |
| STAT_DWA_WAKEUP_CIRCUIT_TEXT | string | dwa Wake Up Circuit ok - dwa Wake Up Circuit failure |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-schnelltest"></a>
### STEUERN_DWA_SCHNELLTEST

Activates the 'dwa armed - schnelltest' mode: activates the MUW & ADXL alarm triggers. When the alarm trigger is detected the CANSINE make a siren sound lasting 2s (with normal sound level), then returns to 'dwa disarmed' status The Tilt sensor monitoring starts 5 seconds after sending this command The MUW sensor alarm detectable 10 seconds after sending this command KWP2000: $31 StartRoutineByLocalIdentifier $48 Fast Test $01 normal volume

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-schnelltest-leise"></a>
### STEUERN_DWA_SCHNELLTEST_LEISE

Activates the 'dwa armed - schnelltest' mode: activates the MUW & ADXL alarm triggers. When the alarm trigger is detected the CANSINE make a siren sound lasting 2s (with lower sound level), then returns to 'dwa disarmed' status The Tilt sensor monitoring starts 5 seconds after sending this command The MUW sensor alarm detectable 10 seconds after sending this command KWP2000: $31 StartRoutineByLocalIdentifier $48 Fast Test $00 low volume

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-muw-alarm-levels-reset"></a>
### STEUERN_MUW_ALARM_LEVELS_RESET

Reset of the last ten alarms voltage levels recorded by the addressed MUW/s (vr,hr,hl,vl,hi,alle). If JOB_STATUS is OK: The 10 MUW/s alarms levels are set to zero. The value '0' means 'no alarm stored in this location. STAT_XX_MUW_ALARM_LEVELS_RESET_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not deleted, and the following error code is shown by STAT_XX_MUW_ALARM_LEVELS_RESET_FEHL - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $49 reset of the MUW alarm levels $xx MUW id

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VR_MUW_ALARM_LEVELS_RESET_FEHL | int | MUW ok - MUW not ok code |
| STAT_HR_MUW_ALARM_LEVELS_RESET_FEHL | int | MUW ok - MUW not ok code |
| STAT_HL_MUW_ALARM_LEVELS_RESET_FEHL | int | MUW ok - MUW not ok code |
| STAT_VL_MUW_ALARM_LEVELS_RESET_FEHL | int | MUW ok - MUW not ok code |
| STAT_HI_MUW_ALARM_LEVELS_RESET_FEHL | int | MUW ok - MUW not ok code |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-muw-false-wakeup-levels-reset"></a>
### STEUERN_MUW_FALSE_WAKEUP_LEVELS_RESET

Reset of the last ten false wakeup levels recorded by the addressed MUW/s (vr,hr,hl,vl,hi,alle). If JOB_STATUS is OK: The 10 MUW/s false wakeup levels are set to 0 The value '0' means 'no level stored in this location. STAT_XX_MUW_F_WK_LEVELS_RESET_FEHL has value '0' in case no internal error occurred. In case an internal error occurred, the data are not deleted, and the following error code is shown by STAT_XX_MUW_F_WK_LEVELS_RESET_FEHL - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $50 reset of MUW false wakeup levels $xx MUW id

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VR_MUW_F_WK_LEVELS_RESET_FEHL | int | MUW ok - MUW not ok code |
| STAT_HR_MUW_F_WK_LEVELS_RESET_FEHL | int | MUW ok - MUW not ok code |
| STAT_HL_MUW_F_WK_LEVELS_RESET_FEHL | int | MUW ok - MUW not ok code |
| STAT_VL_MUW_F_WK_LEVELS_RESET_FEHL | int | MUW ok - MUW not ok code |
| STAT_HI_MUW_F_WK_LEVELS_RESET_FEHL | int | MUW ok - MUW not ok code |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-muw-funktionstest-start"></a>
### STEUERN_MUW_FUNKTIONSTEST_START

Set all the configured MUWs into 'Function Test Status' (FTS). When in this status, the MUW will return 'Movement'/'No Movement' detected when queried with job: - STEUERN_MUW_FUNKTIONSTEST After usign this job, wait 15 seconds before using the job STEUERN_MUW_FUNKTIONSTEST MUWs exit this status, upon receipt of any other not related jobs If JOB_STATUS is OK: The MUW/s resulting status is displayed XX_MUW_STAT has value '0' in case no internal error occurred and the MUW is in 'FTS' In case an internal error occurred, the data are not valid, and the following error codes are indicated by XX_MUW_STAT: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $45 MUW funktion test id

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VR_MUW_STAT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| HR_MUW_STAT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| HL_MUW_STAT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| VL_MUW_STAT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| HI_MUW_STAT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| VR_MUW_STAT_TEXT | string | muw on - muw nicht i.O. code |
| HR_MUW_STAT_TEXT | string | muw on - muw nicht i.O. code |
| HL_MUW_STAT_TEXT | string | muw on - muw nicht i.O. code |
| VL_MUW_STAT_TEXT | string | muw on - muw nicht i.O. code |
| HI_MUW_STAT_TEXT | string | muw on - muw nicht i.O. code |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-muw-funktionstest"></a>
### STEUERN_MUW_FUNKTIONSTEST

Queries the addressed (vr, hr, hl, vl, hi, alle) the latched motion detection status. Pre-condition: MUWs has been set to 'Function Test Status' (FTS) with job STEUERN_MUW_FUNKTIONSTEST_START. When in this status, the MUW will return 'Movement'/ 'No Movement'. When the MUW replies, the latched motion is deleted. A warning will advise the user if this job is called for a MUW which is not in FTS If JOB_STATUS is OK: If STAT_MUW has value 0, the MUW's are in FTS and the results are valid. If STAT_MUW has value 1, the MUW's are not in FTS, and the results are not valid: the user must use the job STEUERN_MUW_FUNKTIONSTEST_START The MUW/s resulting status is displayed XX_MUW_STAT has value '0' in case no internal error occurred In case an internal error occurred, the data are not valid, and the following error codes are indicated by XX_MUW_STAT: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $46 MUW funktionstest (project specific $(MUWID)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VR_MUW_WERT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HR_MUW_WERT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HL_MUW_WERT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_VL_MUW_WERT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HI_MUW_WERT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_MUW | int | set if funktionstest has not been activated before |
| STAT_VR_MUW_TEXT | string | Error Text |
| STAT_HR_MUW_TEXT | string | Error Text |
| STAT_HL_MUW_TEXT | string | Error Text |
| STAT_VL_MUW_TEXT | string | Error Text |
| STAT_HI_MUW_TEXT | string | Error Text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-muw-selftest"></a>
### STEUERN_MUW_SELFTEST

Activates a selftest inside the addressed MUW (vr, hr, hl, vl, hi, alle) and report the result. One has to wait at least 10 seconds after MUW Power ON before performing this job. Checked MUW hw: ROM, RAM, EEPROM, RF drive circuit, Address Manager, RF lines. If JOB_STATUS is OK: The MUW/s selftest results  are displayed in XX_MUW_SELFTEST_STAT. The following errors can appear: - 1: ROM check failure - 2: RAM check failure - 3: EEPROM check failure - 4: RF drive failure - 5: Address Manager failure - 6: RF Signal line failure - 7: RF Interference line failure In case an internal error occurred, the data are not valid, and the following error codes are indicated by XX_MUW_SELFTEST_STAT: - 30: "error DWA BUS PERMANENTLY LOW", i.e.: no connection to any of the MUW - 31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - 32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - 33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - 36: "MUW not configured",i.e.: this MUW is not coded on this type of car KWP2000: $31 StartRoutineByLocalIdentifier $04 Selftest $(MUWID)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle, vr, hr, hl, vl, hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VR_MUW_SELFTEST_WERT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HR_MUW_SELFTEST_WERT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HL_MUW_SELFTEST_WERT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_VL_MUW_SELFTEST_WERT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_HI_MUW_SELFTEST_WERT | int | 0 : no error 30: error DWA BUS PERMANENTLY LOW 31: error MUW TIMEOUT 32: error REPLY FROM WRONG MUW 33: error WRONG MUW REPLY CHECKSUM 36: MUW not configured |
| STAT_VR_MUW_SELFTEST_TEXT | string | Error text |
| STAT_HR_MUW_SELFTEST_TEXT | string | Error text |
| STAT_HL_MUW_SELFTEST_TEXT | string | Error text |
| STAT_VL_MUW_SELFTEST_TEXT | string | Error text |
| STAT_HI_MUW_SELFTEST_TEXT | string | Error text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-k-bus-test"></a>
### STEUERN_K_BUS_TEST

Send a test telegram and check the reply from any of the MUW/s (vr, hr, hl, vl, hi, alle) in order to perform a test on the local Dwabus (K-BUS), from the point of view of the connection. If JOB_STATUS is OK: The MUW/s status is displayed: the datum DWABUS_TEST_RESULT has value '0' if no error is present on the local bus. In case an internal error occurred, the following error codes are indicated by DWABUS_TEST_RESULT: - x30: "error DWA BUS PERMANENTLY LOW", i.e. no connection to any of the MUW - x31: "error MUW TIMEOUT", i.e.: the target MUW/s does not reply - x32: "error REPLY FROM WRONG MUW", i.e. an internal protocol error has occurred - x33: "error WRONG MUW REPLY CHECKSUM",i.e.: an internal comm. error has occurred - x36: "MUW not configured",i.e.: this MUW is not coded on this type of car where x = 1...5 is the ID of the MUW: - 1: VR - 2: HR - 3: HL - 4: VL - 5: HI KWP2000: $31 StartRoutineByLocalIdentifier $40 dwabus id

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MUWID | string | alle vr hr hl vl hi |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DWABUS_TEST_RESULT | int | dwabus ok - dwabus nicht i.O. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-neigung-x-zero"></a>
### STEUERN_NEIGUNG_X_ZERO

Set the zero for the ADXL tilt sensor X axis KWP2000: $31 StartRoutineByLocalIdentifier $41 $0E

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-neigung-y-zero"></a>
### STEUERN_NEIGUNG_Y_ZERO

Set the zero for the ADXL tilt sensor Y axis KWP2000: $31 StartRoutineByLocalIdentifier $41 $0F Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [HARTTEXTE](#table-harttexte) (14 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (22 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (17 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (7 × 9)
- [HORTTEXTE](#table-horttexte) (25 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HUMWELTMATRIX](#table-humweltmatrix) (14 × 5)
- [HUMWELTTEXTE](#table-humwelttexte) (7 × 9)
- [IORTTEXTE](#table-iorttexte) (5 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (4 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (12 × 9)
- [MUWINPUTPARS](#table-muwinputpars) (6 × 2)
- [ENVDATASETCOND](#table-envdatasetcond) (1 × 6)
- [MONTHS](#table-months) (13 × 2)
- [DAYS](#table-days) (32 × 2)
- [HOURS](#table-hours) (25 × 2)
- [WINDOW](#table-window) (2 × 2)
- [KLIMA](#table-klima) (2 × 2)
- [MINUTES](#table-minutes) (60 × 2)
- [DATUM](#table-datum) (1 × 5)
- [ENVPARS1](#table-envpars1) (1 × 4)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 4 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
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

Dimensions: 76 rows × 2 columns

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

<a id="table-harttexte"></a>
### HARTTEXTE

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

Dimensions: 22 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9CE8 | Fault in RAM Memory |
| 0x9CE9 | Fault in Flash Memory |
| 0x9CEA | Fault in EEPROM |
| 0x9CEB | 'Energiesparmode' active |
| 0x9CF9 | Fault in LED |
| 0x9D00 | Fault in DWABUS |
| 0x9D12 | Fault in Internal Battery |
| 0x9D14 | Fault in Protection Circuit |
| 0x9D15 | Fault in Wakeup Circuit |
| 0x9D16 | Fault in Sound Circuit |
| 0x9D1F | Fault in Tilt Sensor Circuit |
| 0xD944 | CAN physical error: single wire |
| 0xD947 | CAN physical error: bus off |
| 0x9D17 | Max Operating Temperature Exceeded |
| 0x9D01 | MUW implausible |
| 0x9D18 | General default data use |
| 0x9D19 | Application default data use |
| 0x9D1A | SIREN default data use |
| 0x9D1B | TILTSENSOR default data use |
| 0x9D1C | Min Operating Temperature Exceeded |
| 0x9D1D | MUW default data use |
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

Dimensions: 17 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9CE8 | 0x01 | - | - | - |
| 0x9CE9 | 0x01 | - | - | - |
| 0x9CEA | 0x01 | - | - | - |
| 0x9CEB | 0x01 | - | - | - |
| 0x9CF9 | 0x01 | - | - | - |
| 0x9D00 | 0x01 | - | - | - |
| 0x9D12 | 0x01 | - | - | - |
| 0x9D14 | 0x01 | - | - | - |
| 0x9D15 | 0x01 | - | - | - |
| 0x9D16 | 0x01 | - | - | - |
| 0x9D1F | 0x01 | - | - | - |
| 0xD124 | 0x01 | - | - | - |
| 0xD127 | 0x01 | - | - | - |
| 0x9D17 | 0x01 | - | - | - |
| 0x9D01 | 0x01 | - | - | - |
| 0x9D1D | 0x01 | - | - | - |
| default | 0x01 | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | PCB Temperature | [-40°C / 85°C] | - | signed char | - | 1 | 1 | 0 |
| 0x02 | Minutes | 0...59 | - | unsigned char | - | 1 | 1 | 0 |
| 0x03 | Hours | 00...23 | - | unsigned char | - | 1 | 1 | 0 |
| 0x04 | Day | 1...31 | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | Month | 1...12 | - | unsigned char | - | 1 | 1 | 0 |
| 0x06 | Year | 2002... | - | unsigned short | - | 1 | 1 | 0 |
| 0x07 | Special Error Code | 0...n | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 25 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9315 | Alarm MUW Intrusion |
| 0x9317 | Alarm Bonnet Contacts |
| 0x9318 | Alarm Trunk Contacts |
| 0x9319 | Alarm Driver Door Front |
| 0x931A | Alarm Passenger Door Front |
| 0x931B | Alarm Driver Door Rear |
| 0x931C | Alarm Passenger Door Rear |
| 0x931E | Alarm MUW DWABUS Cut Wire |
| 0x9321 | Alarm Distribution |
| 0x9328 | Alarm Inclination X-axis |
| 0x9329 | Alarm Inclination Y-axis |
| 0x932A | Alarm Inclination X/Y-axis |
| 0x932B | Alarm power supply cut wire |
| 0x931F | Alarm CAS Authentication |
| 0x932C | Alarm MUW VR Intrusion |
| 0x932D | Alarm MUW HR Intrusion |
| 0x932E | Alarm MUW HL Intrusion |
| 0x932F | Alarm MUW VL Intrusion |
| 0x9322 | Alarm MUW VR Cut Wire |
| 0x9323 | Alarm MUW HR Cut Wire |
| 0x9324 | Alarm MUW HL Cut Wire |
| 0x9325 | Alarm MUW VL Cut Wire |
| 0x9320 | Alarm MUW HI Cut Wire |
| 0x931D | Alarm MUW HI Intrusion |
| 0xFFFF | unbekannter Fehlerort |

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
| F_UWB_ERW | ja |

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 14 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9315 | DATUM | ENVPARS1 | - | - |
| 0x9317 | DATUM | ENVPARS1 | - | - |
| 0x9318 | DATUM | ENVPARS1 | - | - |
| 0x9319 | DATUM | ENVPARS1 | - | - |
| 0x931A | DATUM | ENVPARS1 | - | - |
| 0x931B | DATUM | ENVPARS1 | - | - |
| 0x931C | DATUM | ENVPARS1 | - | - |
| 0x931E | DATUM | ENVPARS1 | - | - |
| 0x9321 | DATUM | ENVPARS1 | - | - |
| 0x9328 | DATUM | ENVPARS1 | - | - |
| 0x9329 | DATUM | ENVPARS1 | - | - |
| 0x932A | DATUM | ENVPARS1 | - | - |
| 0x932B | DATUM | ENVPARS1 | - | - |
| default | DATUM | ENVPARS1 | - | - |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | PCB TEMPERATURE | [-40°C / +85°C] | - | signed char | - | 1 | 1 | 0 |
| 0x02 | MINUTE | 0...59 | - | unsigned char | - | 1 | 1 | 0 |
| 0x03 | HOUR | 0...23 | - | unsigned char | - | 1 | 1 | 0 |
| 0x04 | DAY | 1...31 | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | MONTH | 1...12 | - | unsigned char | - | 1 | 1 | 0 |
| 0x06 | CAR APERTURE STS | 0 or 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x07 | KLIMA STS | 0 or 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 5 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x930A | Error Door Contact |
| 0x9314 | Sensor Inactivated |
| 0x9339 | Polarity Inversion Detected |
| 0x9D13 | External battery voltage out of range |
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
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 4 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x930A | 0x05 | 0x04 | 0x03 | 0x02 |
| 0x9314 | 0x05 | 0x04 | 0x03 | 0x02 |
| 0x9339 | 0x08 | 0x09 | 0x0A | 0x0B |
| default | 0x05 | 0x04 | 0x03 | 0x02 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 12 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | PCB Temperature | [-40°C / 85°C] | - | unsigned char | - | 1 | 1 | 0 |
| 0x02 | Minutes | 0...59 | - | unsigned char | - | 1 | 1 | 0 |
| 0x03 | Hours | 0...23 | - | unsigned char | - | 1 | 1 | 0 |
| 0x04 | Day | 1...31 | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | Month | 1...12 | - | unsigned char | - | 1 | 1 | 0 |
| 0x06 | Year | 2002... | - | unsigned short | - | 1 | 1 | 0 |
| 0x07 | Special Error Code | 0...n | - | unsigned char | - | 1 | 1 | 0 |
| 0x08 | Maximum Reverse Voltage Read | Volts | - | signed char | - | -1 | 26 | 4.6 |
| 0x09 | Time at less than -1V | seconds | - | unsigned char | - | 1 | 1 | 0 |
| 0x0A | Time at less than -2V | seconds | - | unsigned char | - | 1 | 1 | 0 |
| 0x0B | Time at less than -3V | seconds | - | unsigned char | - | 1 | 1 | 0 |
| 0x0C | Time at less than 4V | seconds | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-muwinputpars"></a>
### MUWINPUTPARS

Dimensions: 6 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| alle | 2 |
| vr | 3 |
| hr | 4 |
| hl | 5 |
| vl | 6 |
| hi | 7 |

<a id="table-envdatasetcond"></a>
### ENVDATASETCOND

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x06 | 0x07 | 0x05 | 0x04 | 0x03 |

<a id="table-months"></a>
### MONTHS

Dimensions: 13 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0400 | 1 |
| 0x0800 | 2 |
| 0x0C00 | 3 |
| 0x1000 | 4 |
| 0x1400 | 5 |
| 0x1800 | 6 |
| 0x1C00 | 7 |
| 0x2000 | 8 |
| 0x2400 | 9 |
| 0x2800 | 10 |
| 0x2C00 | 11 |
| 0x3000 | 12 |
| default | Invalid |

<a id="table-days"></a>
### DAYS

Dimensions: 32 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0020 | 1 |
| 0x0040 | 2 |
| 0x0060 | 3 |
| 0x0080 | 4 |
| 0x00A0 | 5 |
| 0x00C0 | 6 |
| 0x00E0 | 7 |
| 0x0100 | 8 |
| 0x0120 | 9 |
| 0x0140 | 10 |
| 0x0160 | 11 |
| 0x0180 | 12 |
| 0x01A0 | 13 |
| 0x01C0 | 14 |
| 0x01E0 | 15 |
| 0x0200 | 16 |
| 0x0220 | 17 |
| 0x0240 | 18 |
| 0x0260 | 19 |
| 0x0280 | 20 |
| 0x02A0 | 21 |
| 0x02C0 | 22 |
| 0x02E0 | 23 |
| 0x0300 | 24 |
| 0x0320 | 25 |
| 0x0340 | 26 |
| 0x0360 | 27 |
| 0x0380 | 28 |
| 0x03A0 | 29 |
| 0x03C0 | 30 |
| 0x03E0 | 31 |
| default | Invalid |

<a id="table-hours"></a>
### HOURS

Dimensions: 25 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0001 | 1 |
| 0x0002 | 2 |
| 0x0003 | 3 |
| 0x0004 | 4 |
| 0x0005 | 5 |
| 0x0006 | 6 |
| 0x0007 | 7 |
| 0x0008 | 8 |
| 0x0009 | 9 |
| 0x000A | 10 |
| 0x000B | 11 |
| 0x000C | 12 |
| 0x000D | 13 |
| 0x000E | 14 |
| 0x000F | 15 |
| 0x0010 | 16 |
| 0x0011 | 17 |
| 0x0012 | 18 |
| 0x0013 | 19 |
| 0x0014 | 20 |
| 0x0015 | 21 |
| 0x0016 | 22 |
| 0x0017 | 23 |
| 0x0018 | 0 |
| default | Invalid |

<a id="table-window"></a>
### WINDOW

Dimensions: 2 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x8000 | Open |
| default | Closed |

<a id="table-klima"></a>
### KLIMA

Dimensions: 2 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x4000 | On |
| default | Off |

<a id="table-minutes"></a>
### MINUTES

Dimensions: 60 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0 | 0 |
| 0x1 | 1 |
| 0x2 | 2 |
| 0x3 | 3 |
| 0x4 | 4 |
| 0x5 | 5 |
| 0x6 | 6 |
| 0x7 | 7 |
| 0x8 | 8 |
| 0x9 | 9 |
| 0xA | 10 |
| 0xB | 11 |
| 0xC | 12 |
| 0xD | 13 |
| 0xE | 14 |
| 0xF | 15 |
| 0x10 | 16 |
| 0x11 | 17 |
| 0x12 | 18 |
| 0x13 | 19 |
| 0x14 | 20 |
| 0x15 | 21 |
| 0x16 | 22 |
| 0x17 | 23 |
| 0x18 | 24 |
| 0x19 | 25 |
| 0x1A | 26 |
| 0x1B | 27 |
| 0x1C | 28 |
| 0x1D | 29 |
| 0x1E | 30 |
| 0x1F | 31 |
| 0x20 | 32 |
| 0x21 | 33 |
| 0x22 | 34 |
| 0x23 | 35 |
| 0x24 | 36 |
| 0x25 | 37 |
| 0x26 | 38 |
| 0x27 | 39 |
| 0x28 | 40 |
| 0x29 | 41 |
| 0x2A | 42 |
| 0x2B | 43 |
| 0x2C | 44 |
| 0x2D | 45 |
| 0x2E | 46 |
| 0x2F | 47 |
| 0x30 | 48 |
| 0x31 | 49 |
| 0x32 | 50 |
| 0x33 | 51 |
| 0x34 | 52 |
| 0x35 | 53 |
| 0x36 | 54 |
| 0x37 | 55 |
| 0x38 | 56 |
| 0x39 | 57 |
| 0x3A | 58 |
| default | Invalid |

<a id="table-datum"></a>
### DATUM

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x05 | 0x04 | 0x03 | 0x02 |

<a id="table-envpars1"></a>
### ENVPARS1

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x06 | 0x07 | 0x01 |
