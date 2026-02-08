# trsvc70.prg

- Jobs: [298](#jobs)
- Tables: [19](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | TRSVC  |
| ORIGIN | BMW EI-612 Zeller Armin |
| REVISION | 7.000 |
| AUTHOR | IAV EF-F6 Jevgeni.Boyko.JB, ASL RD Vaclav.Mocek, ASL RD Ravi.Up |
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
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
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
- [ENABLE_FS_REAR_VIEW_MODE](#job-enable-fs-rear-view-mode) - Enable Full Screen Rear View KWP2000: $31 RoutineControl $49 $00 Modus  : Default
- [DISABLE_REAR_VIEW_MODE](#job-disable-rear-view-mode) - Disable Full Screen Rear View KWP2000: $32 RoutineControl $49 $00 Modus  : Default
- [ENABLE_TOP_VIEW_MODE](#job-enable-top-view-mode) - Enable Top View KWP2000: $31 RoutineControl $47 $00 Modus  : Default
- [DISABLE_TOP_VIEW_MODE](#job-disable-top-view-mode) - Disable Top View KWP2000: $32 RoutineControl $47 $00 Modus  : Default
- [ENABLE_SIDE_VIEW_MODE](#job-enable-side-view-mode) - Enable Side View KWP2000: $31 RoutineControl $48 $00 Modus  : Default
- [DISABLE_SIDE_VIEW_MODE](#job-disable-side-view-mode) - Disable Side View KWP2000: $32 RoutineControl $48 $00 Modus  : Default
- [ENABLE_FS_TOP_VIEW_LEFT_OVERLAY_CEL](#job-enable-fs-top-view-left-overlay-cel) - Enable Full Screen TVL Overlay CEL Manf KWP2000: $31 RoutineControl $4B $00 $00 Modus  : Default
- [ENABLE_FS_TOP_VIEW_RIGHT_CEL](#job-enable-fs-top-view-right-cel) - Enable Full Screen TVR CEL Manf KWP2000: $31 RoutineControl $4A $00 $01 Modus  : Default
- [START_AUTOADR_KAM](#job-start-autoadr-kam) - New camera learning KWP2000: $31 RoutineControl $21 $00 $00 Modus  : Default
- [STOP_AUTOADR_KAM](#job-stop-autoadr-kam) - Stop new camera learning KWP2000: $32 RoutineControl $21 $00 $00 Modus  : Default
- [STATUS_AUTOADR_KAM](#job-status-autoadr-kam) - Status of camera learning KWP2000: $33 RoutineControl $21 $00 $00 Modus  : Default
- [ABWEICHUNG_TVL_KAM](#job-abweichung-tvl-kam) - Deviation in mm of mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $7a Modus  : Default
- [ABWEICHUNG_TVR_KAM](#job-abweichung-tvr-kam) - Deviation in mm of the mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $7b Modus  : Default
- [ABWEICHUNG_RV_KAM](#job-abweichung-rv-kam) - Deviation in mm of mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $7D Modus  : Default
- [SET_TV_RIGHT_CAM_POS](#job-set-tv-right-cam-pos) - Set Top view right camera positions KWP2000: $2E $C1 $60 Modus  : Default
- [SET_TV_LEFT_CAM_POS](#job-set-tv-left-cam-pos) - Set Top view left camera positions KWP2000: $2E $C1 $61 Modus  : Default
- [STATUS_TV_RIGHT_CAM_POS](#job-status-tv-right-cam-pos) - Set Top view right camera positions KWP2000: $22 $C1 $60 Modus  : Default
- [STATUS_RV_CAM_POS](#job-status-rv-cam-pos) - Set Rear view cam positions KWP2000: $22 $C1 $62 Modus  : Default
- [STATUS_TV_LEFT_CAM_POS](#job-status-tv-left-cam-pos) - Set Top view left camera positions KWP2000: $22 $C1 $61 Modus  : Default
- [SET_RV_CAM_POS](#job-set-rv-cam-pos) - Set Rear view camera positions KWP2000: $2E $C1 $62 Modus  : Default
- [ENABLE_OUTPUT_VIDEO_TST_PATRN_NTSC](#job-enable-output-video-tst-patrn-ntsc) - Enable NTSC Encoder Colour bar KWP2000: $31 RoutineControl $45 $00 $06 $00 $00 $00 $00 $00 $00 $00 Modus  : Default
- [ENABLE_OUTPUT_VIDEO_TST_PATRN_DSP](#job-enable-output-video-tst-patrn-dsp) - Enable DSP Encoder Colour bar KWP2000: $31 RoutineControl $45 $00 $00 $00 $00 $00 $00 $00 $00 $00 Modus  : Default
- [ENABLE_POWER_TO_DSP_CAM](#job-enable-power-to-dsp-cam) - Enbale POWER for DSP and Cameras KWP2000: $31 RoutineControl $46 $00 $01 Modus  : Default
- [DISABLE_POWER_TO_DSP_CAM](#job-disable-power-to-dsp-cam) - Disbale POWER for DSP and Cameras KWP2000: $31 RoutineControl $46 $00 $00 Modus  : Default
- [ENABLE_FS_TOP_VIEW_RIGHT_OVERLAY_CEL](#job-enable-fs-top-view-right-overlay-cel) - Enable Full Screen TVR Overlay CEL Manf KWP2000: $31 RoutineControl $4A $00 $00 Modus  : Default
- [DISABLE_OUTPUT_TEST_PATTERN](#job-disable-output-test-pattern) - Disable Colour bar KWP2000: $32 RoutineControl $45 $00 Modus  : Default
- [DISABLE_FS_TOP_VIEW_LEFT_CEL](#job-disable-fs-top-view-left-cel) - Disable Full Screen TVL CEL Manf KWP2000: $32 RoutineControl $4B $00 Modus  : Default
- [DISABLE_FS_TOP_VIEW_RIGHT_CEL](#job-disable-fs-top-view-right-cel) - Diable Full Screen TVR CEL Manf KWP2000: $32 RoutineControl $4A $00 Modus  : Default
- [ENABLE_FS_TOP_VIEW_LEFT_CEL](#job-enable-fs-top-view-left-cel) - Enable Full Screen TVL CEL Manf KWP2000: $31 RoutineControl $4B $00 $01 Modus  : Default
- [DSP_APP_SUPPLIER_VER](#job-dsp-app-supplier-ver) - DSP Application Version KWP2000: $22 ReadDataByCommonIdentifier $c1 $02 Modus  : Default
- [DSP_PBL_A_SUPPLIER_VER](#job-dsp-pbl-a-supplier-ver) - DSP PBL A Version KWP2000: $22 ReadDataByCommonIdentifier $c1 $03 Modus  : Default
- [DSP_PBL_B_SUPPLIER_VER](#job-dsp-pbl-b-supplier-ver) - DSP PBL B Version KWP2000: $22 ReadDataByCommonIdentifier $c1 $04 Modus  : Default
- [DSP_PRE_PBL_SUPPLIER_VER](#job-dsp-pre-pbl-supplier-ver) - DSP Pre PBL Version KWP2000: $22 ReadDataByCommonIdentifier $c1 $05 Modus  : Default
- [WINKELVERDREHUNG_TVR_KAM](#job-winkelverdrehung-tvr-kam) - Deviation of the mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $78 Modus  : Default
- [WINKELVERDREHUNG_RV_KAM](#job-winkelverdrehung-rv-kam) - Deviation of the mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $70 Modus  : Default
- [WINKELVERDREHUNG_TVL_KAM](#job-winkelverdrehung-tvl-kam) - Deviation of the mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $79 Modus  : Default
- [HOST_APP_SUPPLIER_VER](#job-host-app-supplier-ver) - HOST Application Version KWP2000: $22 ReadDataByCommonIdentifier $c1 $01 Modus  : Default
- [READ_ECU_VAR](#job-read-ecu-var) - ECU variant KWP2000: $22 ReadDataByCommonIdentifier $c1 $00 Modus  : Default
- [SET_STEUERN_TVC_KALIB_ABWEICH](#job-set-steuern-tvc-kalib-abweich) - Set service calibration deviation KWP2000: $2E $D3 $B2 Modus  : Default
- [SET_STEUERN_TVC_KALIB_VER](#job-set-steuern-tvc-kalib-ver) - Set service calibration rotation KWP2000: $2E $D3 $B3 Modus  : Default
- [STATUS_SRV_RV_VIRT_CAM](#job-status-srv-rv-virt-cam) - Set Rear view right cam positions KWP2000: $22 $C1 $81 Modus  : Default
- [STATUS_SRV_TVR_VIRT_CAM](#job-status-srv-tvr-virt-cam) - Set Rear view right cam positions KWP2000: $22 $C1 $7F Modus  : Default
- [STATUS_SRV_TVL_VIRT_CAM](#job-status-srv-tvl-virt-cam) - Set Rear view right cam positions KWP2000: $22 $C1 $80 Modus  : Default
- [SET_SRV_CALIB_RV_VIRT_CAM](#job-set-srv-calib-rv-virt-cam) - Set service calibration TVL virtual camera KWP2000: $2E $C1 $81 Modus  : Default
- [SET_SRV_CALIB_TVR_VIRT_CAM](#job-set-srv-calib-tvr-virt-cam) - Set service calibration TVR virtual camera KWP2000: $2E $C1 $7F Modus  : Default
- [SET_SRV_CALIB_TVL_VIRT_CAM](#job-set-srv-calib-tvl-virt-cam) - Set service calibration TVL virtual camera KWP2000: $2E $C1 $80 Modus  : Default
- [START_KALIB_MONTAGE](#job-start-kalib-montage) - Start calibration with selected target KWP2000: $31 RoutineControl $20 $00 Modus  : Default
- [STOP_KALIB_MONTAGE](#job-stop-kalib-montage) - Stop calibration with selected target KWP2000: $32 RoutineControl $20 $00 $00 Modus  : Default
- [STATUS_KALIB_MONTAGE](#job-status-kalib-montage) - Status of calibration KWP2000: $33 RoutineControl $20 $00 $00 Modus  : Default
- [ECU_TEMP](#job-ecu-temp) - ECU temerature KWP2000: $22 ReadDataByCommonIdentifier $c1 $06 Modus  : Default
- [TVR_CAM_INFO](#job-tvr-cam-info) - TV right camera information KWP2000: $22 ReadDataByCommonIdentifier $c1 $07 Modus  : Default
- [TVL_CAM_INFO](#job-tvl-cam-info) - TV left camera information KWP2000: $22 ReadDataByCommonIdentifier $c1 $08 Modus  : Default
- [SVR_CAM_INFO](#job-svr-cam-info) - SV right camera information KWP2000: $22 ReadDataByCommonIdentifier $c1 $09 Modus  : Default
- [SVL_CAM_INFO](#job-svl-cam-info) - SV left camera information KWP2000: $22 ReadDataByCommonIdentifier $c1 $0a Modus  : Default
- [RV_CAM_INFO](#job-rv-cam-info) - Rear view camera information KWP2000: $22 ReadDataByCommonIdentifier $c1 $07 Modus  : Default
- [STATUS_TVR_CAM](#job-status-tvr-cam) - TVR cam status KWP2000: $22 ReadDataByCommonIdentifier $c1 $0c Modus  : Default
- [STATUS_TVL_CAM](#job-status-tvl-cam) - TVL cam status KWP2000: $22 ReadDataByCommonIdentifier $c1 $0D Modus  : Default
- [STATUS_SVR_CAM](#job-status-svr-cam) - SVR cam status KWP2000: $22 ReadDataByCommonIdentifier $c1 $0e Modus  : Default
- [STATUS_SVL_CAM](#job-status-svl-cam) - SVL cam status KWP2000: $22 ReadDataByCommonIdentifier $c1 $0f Modus  : Default
- [STATUS_RV_CAM](#job-status-rv-cam) - RV cam status KWP2000: $22 ReadDataByCommonIdentifier $c1 $10 Modus  : Default
- [STATUS_TVR_DISP_CALIB](#job-status-tvr-disp-calib) - Status TV Right display calibration KWP2000: $22 $C1 $28 Modus  : Default
- [STATUS_TVL_DISP_CALIB](#job-status-tvl-disp-calib) - Status TV left display calibration KWP2000: $22 $C1 $29 Modus  : Default
- [STATUS_UV_REAR_DISP_CALIB](#job-status-uv-rear-disp-calib) - Status U view Rear display calibration KWP2000: $22 $C1 $2a Modus  : Default
- [STATUS_FS_REAR_DISP_CALIB](#job-status-fs-rear-disp-calib) - Status FS rear display calibration KWP2000: $22 $C1 $2B Modus  : Default
- [STATUS_BMW_FSR_DISP_CALIB](#job-status-bmw-fsr-disp-calib) - Status BMW production calibration FS rear display calibration KWP2000: $22 $C1 $2C Modus  : Default
- [STATUS_TVR_CAM_CAL_DATA](#job-status-tvr-cam-cal-data) - Read TV right camera clibration data KWP2000: $22 ReadDataByCommonIdentifier $c1 $16 Modus  : Default
- [STATUS_TVL_CAM_CAL_DATA](#job-status-tvl-cam-cal-data) - Read TV left camera clibration data KWP2000: $22 ReadDataByCommonIdentifier $c1 $17 Modus  : Default
- [STATUS_RV_CAM_CAL_DATA](#job-status-rv-cam-cal-data) - Read RV camera clibration data KWP2000: $22 ReadDataByCommonIdentifier $c1 $18 Modus  : Default
- [STATUS_CALIB_OVL_GRID](#job-status-calib-ovl-grid) - Status of calibration overlay gris data KWP2000: $22 ReadDataByCommonIdentifier $c1 $2E Modus  : Default
- [STATUS_BMW_FSR_GRID_LAYOUT](#job-status-bmw-fsr-grid-layout) - Status of BMW assembly calibration FS rear grid layout KWP2000: $22 ReadDataByCommonIdentifier $c1 $68 Modus  : Default
- [STATUS_RV_CAL_TARGET_POS](#job-status-rv-cal-target-pos) - Read RV calibration target position KWP2000: $22 $C1 $71 Modus  : Default
- [STATUS_TVR_CAL_TARGET_POS](#job-status-tvr-cal-target-pos) - Read TV Right calibration target position KWP2000: $22 $C1 $69 Modus  : Default
- [STATUS_TVL_CAL_TARGET_POS](#job-status-tvl-cal-target-pos) - Read TV Left calibration target position KWP2000: $22 $C1 $70 Modus  : Default
- [STATUS_BMW_RV_CAL_SOLV_PARAMS](#job-status-bmw-rv-cal-solv-params) - Read BMW RV assembly calibration solver parameters KWP2000: $22 $C1 $76 Modus  : Default
- [STATUS_MAXIMALEBLOCKLAENGE](#job-status-maximaleblocklaenge) - Status Maximum block length KWP2000: $22 $25 $06 Modus  : Default
- [STATUS_PROGRAMMING_STATE](#job-status-programming-state) - Read programming state KWP2000: $31 $0a Modus  : Default
- [STATUS_BUS_NACHRICHTEN](#job-status-bus-nachrichten) - Status of CAN Speed KWP2000: $22 $D2 $40 Modus  : Default
- [STATUS_BUS_IN_SV_EIN](#job-status-bus-in-sv-ein) - Status of Side view camera active or not KWP2000: $22 $D3 $B5 Modus  : Default
- [STATUS_HECKKLAPPE](#job-status-heckklappe) - Read Boot status KWP2000: $22 $D3 $7c Modus  : Default
- [STATUS_AUSSTATTUNG](#job-status-ausstattung) - Status of RV, TV, SV modes avalibale KWP2000: $22 $D3 $7F Modus  : Default
- [STATUS_STROMAUFNAHME_KAMERA_TSV](#job-status-stromaufnahme-kamera-tsv) - Status of current consumption of TV and SV KWP2000: $22 $D3 $80 Modus  : Default
- [STATUS_INITIALISIERUNG_TV](#job-status-initialisierung-tv) - Status of TVL, TVR camera init KWP2000: $22 $D3 $81 Modus  : Default
- [STATUS_BUS_VORDERTUEREN](#job-status-bus-vordertueren) - Status of front doors KWP2000: $22 $D3 $83 Modus  : Default
- [STATUS_BUS_NACHRICHTEN_D392](#job-status-bus-nachrichten-d392) - Status information about CAN Signal TV, RV requested KWP2000: $22 $D3 $92 Modus  : Default
- [STATUS_BUS_NACHRICHTEN_D395](#job-status-bus-nachrichten-d395) - Status CAN Signals regarding the mirror fold-/unfold status KWP2000: $22 $D3 $95 Modus  : Default
- [STATUS_KALIBRIERUNG_TV](#job-status-kalibrierung-tv) - Top view calibration status KWP2000: $22 $D3 $9C Modus  : Default
- [STATUS_KALIBRIERUNG_RV](#job-status-kalibrierung-rv) - Top view calibration status KWP2000: $22 $D3 $9D Modus  : Default
- [STATUS_STROMAUFNAHME_KAMERA_RV](#job-status-stromaufnahme-kamera-rv) - Rear view camera current consumption KWP2000: $22 $D3 $9E Modus  : Default
- [STATUS_INITIALISIERUNG_RV](#job-status-initialisierung-rv) - Status of RV camera init KWP2000: $22 $D3 $9F Modus  : Default
- [STATUS_KLEMMEN_15N_WERT_DAD2](#job-status-klemmen-15n-wert-dad2) - Status_klemmen (15N wert) KWP2000: $22 $DA $D2 Modus  : Default
- [STATUS_KLEMMEN_15N_EIN](#job-status-klemmen-15n-ein) - Status of KL15N KWP2000: $22 $DA $FE Modus  : Default
- [STATUS_KLEMMEN_15N_WERT_DB2D](#job-status-klemmen-15n-wert-db2d) - CAN signal b_ST_KL_15_b KWP2000: $22 $DB $2D Modus  : Default
- [STATUS_CODING_DATA](#job-status-coding-data) - Read the coding data block KWP2000: $22 RoutineControl $30 $00 Modus  : Default
- [SET_BUS_IN_SV_EIN](#job-set-bus-in-sv-ein) - Enable the SV play mode KWP2000: $2E $D3 $B5 Modus  : Default
- [SET_STEUERN_TESTBILD_KAMERA](#job-set-steuern-testbild-kamera) - Set KWP2000: $2E $D3 $B4 Modus  : Default
- [STATUS_CAMERA_SOILING](#job-status-camera-soiling) - Status of TV,SV,RV camera soiling KWP2000: $22 ReadDataByCommonIdentifier $c1 $30 Modus  : Default
- [STATUS_BMW_TV_CAL_SOLV_PARAMS](#job-status-bmw-tv-cal-solv-params) - Read BMW TV assembly calibration solver parameters KWP2000: $22 $C1 $53 Modus  : Default
- [STATUS_BMW_TVL_GRID_LAYOUT](#job-status-bmw-tvl-grid-layout) - Status of BMW assembly calibration Top view left grid layout KWP2000: $22 ReadDataByCommonIdentifier $c1 $55 Modus  : Default
- [STATUS_BMW_TVR_GRID_LAYOUT](#job-status-bmw-tvr-grid-layout) - Status of BMW assembly calibration Top view right grid layout KWP2000: $22 ReadDataByCommonIdentifier $c1 $57 Modus  : Default
- [STATUS_CALIBRATION_PERFORMED](#job-status-calibration-performed) - Status of calibration performed or not KWP2000: $22 ReadDataByCommonIdentifier $c1 $59 Modus  : Default
- [STATUS_VIDEO_FREEZ_WDT](#job-status-video-freez-wdt) - Video freez watchdog status KWP2000: $22 ReadDataByCommonIdentifier $c1 $67 Modus  : Default
- [START_STEUREN_SIGNALAUSGABE](#job-start-steuren-signalausgabe) - Start test picture and colour bar with time out KWP2000: $31 RoutineControl $22 $00 Modus  : Default
- [STOP_STEUREN_SIGNALAUSGABE](#job-stop-steuren-signalausgabe) - Stop test picture and colour bar KWP2000: $32 RoutineControl $22 $00 Modus  : Default
- [START_TEST_VIDEOAUSGANG](#job-start-test-videoausgang) - Start KWP2000: $31 RoutineControl $23 $00 Modus  : Default
- [STOP_TEST_VIDEOAUSGANG](#job-stop-test-videoausgang) - Stop KWP2000: $32 RoutineControl $23 $00 Modus  : Default
- [STATUS_TEST_VIDEOAUSGANG](#job-status-test-videoausgang) - Status KWP2000: $33 RoutineControl $23 $00 Modus  : Default
- [SET_TVR_CAM_CAL_DATA](#job-set-tvr-cam-cal-data) - Set TV right camera clibration data KWP2000: $2E ReadDataByCommonIdentifier $c1 $16 Modus  : Default
- [SET_TVL_CAM_CAL_DATA](#job-set-tvl-cam-cal-data) - Set TV left camera clibration data KWP2000: $2E ReadDataByCommonIdentifier $c1 $17 Modus  : Default
- [SET_RV_CAM_CAL_DATA](#job-set-rv-cam-cal-data) - Set Rear View camera clibration data KWP2000: $2E ReadDataByCommonIdentifier $c1 $18 Modus  : Default
- [SET_TVR_DISP_CALIB](#job-set-tvr-disp-calib) - Set TV Right display calibration KWP2000: $2E $C1 $28 Modus  : Default
- [SET_TVL_DISP_CALIB](#job-set-tvl-disp-calib) - Set TV left display calibration KWP2000: $2E $C1 $29 Modus  : Default
- [SET_UV_REAR_DISP_CALIB](#job-set-uv-rear-disp-calib) - Set U-view rear display calibration KWP2000: $2E $C1 $2a Modus  : Default
- [SET_FSR_DISP_CALIB](#job-set-fsr-disp-calib) - Status Full screen rear display calibration KWP2000: $2E $C1 $2b Modus  : Default
- [SET_BMW_FSR_DISP_CALIB](#job-set-bmw-fsr-disp-calib) - Status BMW production calibration Full Screen Rear display calibration KWP2000: $2E $C1 $2c Modus  : Default
- [STATUS_ENERGIESPARMODU](#job-status-energiesparmodu) - Status of energy saving mode KWP2000: $22 ReadDataByCommonIdentifier $10 $0A Modus  : Default
- [SET_BUS_NACHRICHTEN_D392](#job-set-bus-nachrichten-d392) - Set CAN Signal TV, RV request KWP2000: $2E $D3 $92 Modus  : Default
- [STATUS_HEIZUNG_RFK](#job-status-heizung-rfk) - status of heating element rv cam KWP2000: $22 $D3 $A0 Modus  : Default
- [SET_HEIZUNG_RFK](#job-set-heizung-rfk) - set of heating element rv cam KWP2000: $2E $D3 $A0 Modus  : Default
- [STATUS_NUM_SUB_BUS_MEMBERS](#job-status-num-sub-bus-members) - status of Number of SubbusMembers and serial numbers KWP2000: $22 $16 $00 Modus  : Default
- [SET_CAMERA_SOILING](#job-set-camera-soiling) - Status of TV,SV,RV camera soiling KWP2000: $2E ReadDataByCommonIdentifier $c1 $30 Modus  : Default
- [STATUS_ECU_DSP_PERFORMNCE](#job-status-ecu-dsp-performnce) - status of ECU DSP processor performance KWP2000: $22 $C1 $32 Modus  : Default
- [STATUS_CEL_SERIAL_NUM](#job-status-cel-serial-num) - Read CEL serial number KWP2000: $22 $C1 $33 Modus  : Default
- [SET_CEL_SERIAL_NUM](#job-set-cel-serial-num) - Set CEL serial number KWP2000: $2E $C1 $33 Modus  : Default
- [STATUS_TEST_PT_LED](#job-status-test-pt-led) - Read Test point LED KWP2000: $22 $C1 $38 Modus  : Default
- [STATUS_LIN_VSYNC](#job-status-lin-vsync) - Read Lin Vsync KWP2000: $22 $C1 $40 Modus  : Default
- [SET_LIN_VSYNC](#job-set-lin-vsync) - Set Lin Vsync KWP2000: $2E $C1 $40 Modus  : Default
- [SET_BMW_TV_CAL_SOLV_PARAMS](#job-set-bmw-tv-cal-solv-params) - Set BMW TV assembly calibration solver parameters KWP2000: $2E $C1 $53 Modus  : Default
- [SET_BMW_TVL_GRID_LAYOUT](#job-set-bmw-tvl-grid-layout) - Set BMW assembly calibration Top view left grid layout KWP2000: $2e ReadDataByCommonIdentifier $c1 $55 Modus  : Default
- [SET_BMW_TVR_GRID_LAYOUT](#job-set-bmw-tvr-grid-layout) - Set BMW assembly calibration Top view right grid layout KWP2000: $2e ReadDataByCommonIdentifier $c1 $57 Modus  : Default
- [SET_BMW_FSR_GRID_LAYOUT](#job-set-bmw-fsr-grid-layout) - Set BMW assembly calibration Full screen rear grid layout KWP2000: $2e ReadDataByCommonIdentifier $c1 $68 Modus  : Default
- [SET_CALIBRATION_PERFORMED](#job-set-calibration-performed) - Set of calibration performed KWP2000: $2E ReadDataByCommonIdentifier $c1 $59 Modus  : Default
- [STATUS_NVM_CFG_INF](#job-status-nvm-cfg-inf) - Read NVM CFG information KWP2000: $22 $C1 $5a Modus  : Default
- [STATUS_CRC_CNT_CHECK](#job-status-crc-cnt-check) - Read CRC & Alive Counter Check on CAN KWP2000: $22 $C1 $66 Modus  : Default
- [SET_CRC_CNT_CHECK](#job-set-crc-cnt-check) - SET CRC & Alive Counter Check on CAN KWP2000: $2E $C1 $66 Modus  : Default
- [SET_TVR_CAL_TRGT_POS](#job-set-tvr-cal-trgt-pos) - Set TV right calibration target position KWP2000: $2E $C1 $69 Modus  : Default
- [SET_TVL_CAL_TRGT_POS](#job-set-tvl-cal-trgt-pos) - Set TV left calibration target position KWP2000: $2E $C1 $70 Modus  : Default
- [SET_REAR_CAL_TRGT_POS](#job-set-rear-cal-trgt-pos) - Set Rear calibration target position KWP2000: $2E $C1 $71 Modus  : Default
- [STATUS_CAL_ERR_POWER](#job-status-cal-err-power) - Read calibration error power KWP2000: $22 $C1 $77 Modus  : Default
- [SET_CAL_ERR_POWER](#job-set-cal-err-power) - SET calibration error power KWP2000: $2E $C1 $77 Modus  : Default
- [SET_BMW_REAR_CAL_SOLV_PARAMS](#job-set-bmw-rear-cal-solv-params) - Set BMW Rear assembly calibration solver parameters KWP2000: $2E $C1 $76 Modus  : Default
- [STATUS_VEH_WEEL_ARCH_HEIGHT](#job-status-veh-weel-arch-height) - Read Vehicle wheel arch heights KWP2000: $22 $C1 $78 Modus  : Default
- [SET_VEH_WEEL_ARCH_HEIGHT](#job-set-veh-weel-arch-height) - Set Vehicle wheel arch heights KWP2000: $2E $C1 $78 Modus  : Default
- [STATUS_DRT_DET_VEH_SPD_THLD](#job-status-drt-det-veh-spd-thld) - Read Dirt detection vehicle speed thresholds KWP2000: $22 $C1 $7a Modus  : Default
- [SET_DRT_DET_VEH_SPD_THLD](#job-set-drt-det-veh-spd-thld) - Set Dirt detection vehicle speed thresholds KWP2000: $2E $C1 $7a Modus  : Default
- [STATUS_CAM_FAILED_PXL_PRCNT](#job-status-cam-failed-pxl-prcnt) - Status of TV,SV,RV Camera failed pixels percentage KWP2000: $22 $c1 $82 Modus  : Default
- [SET_CAM_FAILED_PXL_PRCNT](#job-set-cam-failed-pxl-prcnt) - Set of TV,SV,RV Camera failed pixels percentage KWP2000: $2E $c1 $82 Modus  : Default
- [STATUS_FAIL_PXL_THRESHLD](#job-status-fail-pxl-threshld) - Read Camera failed pixels threshold KWP2000: $22 $C1 $83 Modus  : Default
- [SET_FAIL_PXL_THRESHLD](#job-set-fail-pxl-threshld) - Set Camera failed pixels threshold KWP2000: $2E $C1 $83 Modus  : Default
- [STATUS_IDLE_VDIEO_OP_ENABLE](#job-status-idle-vdieo-op-enable) - Read Idle mode video output enable KWP2000: $22 $C1 $84 Modus  : Default
- [SET_IDLE_VDIEO_OP_ENABLE](#job-set-idle-vdieo-op-enable) - Set Idle mode video output enable KWP2000: $2E $C1 $84 Modus  : Default
- [STATUS_SUB_VARIANT_ID](#job-status-sub-variant-id) - Read Sub variant ID KWP2000: $22 $C1 $85 Modus  : Default
- [STATUS_UV_RIGHT_DISP_CALIB](#job-status-uv-right-disp-calib) - Status U-View Right display calibration KWP2000: $22 $C1 $86 Modus  : Default
- [SET_UV_RIGHT_DISP_CALIB](#job-set-uv-right-disp-calib) - Set U-View Right display calibration KWP2000: $2E $C1 $86 Modus  : Default
- [STATUS_UV_LEFT_DISP_CALIB](#job-status-uv-left-disp-calib) - Status U-View Left display calibration KWP2000: $22 $C1 $87 Modus  : Default
- [SET_UV_LEFT_DISP_CALIB](#job-set-uv-left-disp-calib) - Set U-View Left display calibration KWP2000: $2E $C1 $87 Modus  : Default
- [STATUS_TOW_HITCH_DISP_CALIB](#job-status-tow-hitch-disp-calib) - Status Tow Hitch display calibration KWP2000: $22 $C1 $88 Modus  : Default
- [SET_TOW_HITCH_DISP_CALIB](#job-set-tow-hitch-disp-calib) - Set Tow Hitch Left display calibration KWP2000: $2E $C1 $88 Modus  : Default
- [STATUS_FRM_RATE_REDUC_CNTRL](#job-status-frm-rate-reduc-cntrl) - Read Frame Rate Reduction control KWP2000: $22 $C1 $89 Modus  : Default
- [SET_FRM_RATE_REDUC_CNTRL](#job-set-frm-rate-reduc-cntrl) - Set Frame Rate Reduction control KWP2000: $2E $C1 $89 Modus  : Default
- [SET_FRMRT_RED_MSTR_CNTRL](#job-set-frmrt-red-mstr-cntrl) - Set Framerate Reduction Masterframe KWP2000: $2E $C1 $90 Modus  : Default
- [STATUS_FRMRATE_SLAVE_RESP](#job-status-frmrate-slave-resp) - Read Framerate Reduction Slave responses KWP2000: $22 $C1 $91 Modus  : Default
- [STATUS_OD_TRSHOLDS](#job-status-od-trsholds) - Read Object detection thresholds KWP2000: $22 $C1 $96 Modus  : Default
- [STATUS_OD_PARAMS](#job-status-od-params) - Read Object detection parameters KWP2000: $22 $C1 $97 Modus  : Default
- [STATUS_ONL_CALIB_CNTRL](#job-status-onl-calib-cntrl) - Read Online calibration control KWP2000: $22 $C1 $98 Modus  : Default
- [SET_OD_TRSHOLDS](#job-set-od-trsholds) - Set Object detection thresholds KWP2000: $2E $C1 $96 Modus  : Default
- [SET_OD_PARMS](#job-set-od-parms) - Set Object detection parameters KWP2000: $2E $C1 $97 Modus  : Default
- [SET_ONL_CALIB_CNTRL](#job-set-onl-calib-cntrl) - Set Online calibration control KWP2000: $2E $C1 $98 Modus  : Default
- [SET_ONL_CALIB_CNTRL_DISABLED](#job-set-onl-calib-cntrl-disabled) - Set Online calibration control to be disabled KWP2000: $2E $C1 $98 Modus  : Default
- [STATUS_RV_WRAP_PARAMS](#job-status-rv-wrap-params) - Read Rear view warping parameters KWP2000: $22 $C1 $9b Modus  : Default
- [SET_RV_WRAP_PARAMS](#job-set-rv-wrap-params) - Set Rear view warping parameters KWP2000: $2E $C1 $9B Modus  : Default
- [STATUS_CALIBRATION_ENABLE](#job-status-calibration-enable) - Read development use only - enable / disable calibration KWP2000: $22 $C1 $9c Modus  : Default
- [SET_CALIBRATION_ENABLE](#job-set-calibration-enable) - Set development use only - enable / disable calibration KWP2000: $2E $C1 $9c Modus  : Default
- [STATUS_TOP_VIEW_VEHICLE_POS](#job-status-top-view-vehicle-pos) - Status Enable/disable the Top View Vehicle Position KWP2000: $22 $c1 $9d Modus  : Default
- [SET_TOP_VIEW_VEHICLE_POS](#job-set-top-view-vehicle-pos) - Set Enable/disable the Top View Vehicle Position KWP2000: $2e $c1 $9d Modus  : Default
- [STATUS_UV_ACTIVE_FLAG](#job-status-uv-active-flag) - Status U - View Activation Flag KWP2000: $22 $c1 $9e Modus  : Default
- [SET_UV_ACTIVE_FLAG](#job-set-uv-active-flag) - Set U - View Activation Flag KWP2000: $2e $c1 $9E Modus  : Default
- [STATUS_IDLEMOD_VID_TEST](#job-status-idlemod-vid-test) - Status Idle mode video test index KWP2000: $22 $c1 $9F Modus  : Default
- [STATUS_TV_TEMPORAL_FILT](#job-status-tv-temporal-filt) - Status Topview temporal filtering KWP2000: $22 $c1 $a0 Modus  : Default
- [SET_TV_TEMPORAL_FILT](#job-set-tv-temporal-filt) - Set Topview temporal filtering KWP2000: $2e $c1 $a0 Modus  : Default
- [STATUS_SV_TEMPORAL_FILT](#job-status-sv-temporal-filt) - Status Sideview temporal filtering KWP2000: $22 $c1 $a1 Modus  : Default
- [SET_SV_TEMPORAL_FILT](#job-set-sv-temporal-filt) - Set Sideview temporal filtering KWP2000: $2e $c1 $a1 Modus  : Default
- [STATUS_RV_TEMPORAL_FILT](#job-status-rv-temporal-filt) - Status Rearview temporal filtering KWP2000: $22 $c1 $a2 Modus  : Default
- [SET_RV_TEMPORAL_FILT](#job-set-rv-temporal-filt) - Set Rearview temporal filtering KWP2000: $2e $c1 $a2 Modus  : Default
- [STATUS_INHIBT_ONL_CAL_RES_UPDT](#job-status-inhibt-onl-cal-res-updt) - Read Inhibit Online calibration results update KWP2000: $22 $C1 $A4 Modus  : Default
- [SET_INHIBT_ONL_CAL_RES_UPDT](#job-set-inhibt-onl-cal-res-updt) - Set Inhibit Online calibration results update KWP2000: $2E $C1 $a4 Modus  : Default
- [STATUS_SERVICE_RV_HEATER](#job-status-service-rv-heater) - Read Service Rear View Heater Status KWP2000: $22 $C1 $A5 Modus  : Default
- [SET_SERVICE_RV_HEATER](#job-set-service-rv-heater) - Set Service Rear View Heater Status KWP2000: $2E $C1 $a5 Modus  : Default
- [STATUS_ONL_CAL_DTC_PRESCLRS](#job-status-onl-cal-dtc-presclrs) - Read Online calibration DTC thresholds KWP2000: $22 $C1 $AB Modus  : Default
- [STATUS_TV_INHIBIT](#job-status-tv-inhibit) - Read Inhibit TV status KWP2000: $22 $C1 $A3 Modus  : Default
- [SET_TV_INHIBIT](#job-set-tv-inhibit) - Set Inhibit Top view KWP2000: $2E $C1 $a3 Modus  : Default
- [STATUS_ONL_CAL_RECORD](#job-status-onl-cal-record) - Read the online calibration record data KWP2000: $22 $C1 $AC Modus  : Default
- [STATUS_LIN_NOT_ALIVE](#job-status-lin-not-alive) - Read LIN not alive status KWP2000: $22 $C1 $AD Modus  : Default
- [STATUS_BSDF_ENABLE](#job-status-bsdf-enable) - Read Image quality control parameters KWP2000: $22 $C1 $AE Modus  : Default
- [SET_BSDF_ENABLE](#job-set-bsdf-enable) - Set Image quality control parameters KWP2000: $2E $C1 $ae Modus  : Default
- [STATUS_CAM_LEARN](#job-status-cam-learn) - Read different camera learn status KWP2000: $22 $D3 $A1 Modus  : Default
- [ENABLE_FS_SV_RIGHT_CEL](#job-enable-fs-sv-right-cel) - Enable Full Screen Side view right KWP2000: $31 RoutineControl $58 $00 $00 Modus  : Default
- [DISABLE_FS_SV_RIGHT_CEL](#job-disable-fs-sv-right-cel) - Diaable Full Screen Side view right KWP2000: $32 RoutineControl $58 $00 Modus  : Default
- [ENABLE_FS_SV_LEFT_CEL](#job-enable-fs-sv-left-cel) - Enable Full Screen Side view left KWP2000: $31 RoutineControl $59 $00 $00 Modus  : Default
- [DISABLE_FS_SV_LEFT_CEL](#job-disable-fs-sv-left-cel) - Diable Full Screen Side view  Left KWP2000: $32 RoutineControl $59 $00 Modus  : Default
- [START_BMW_SRV_CAM_LEARN](#job-start-bmw-srv-cam-learn) - Start BMW Service Camera Learn KWP2000: $31 RoutineControl $5C $00 Modus  : Default
- [START_LIN_DISABLE_ALL](#job-start-lin-disable-all) - Start LIN disable all schedules KWP2000: $31 RoutineControl $5D $00 Modus  : Default
- [STOP_LIN_DISABLE_ALL](#job-stop-lin-disable-all) - Stop LIN disable all schedules KWP2000: $32 RoutineControl $5D $00 Modus  : Default
- [START_LVDS_IMAGER](#job-start-lvds-imager) - Start LVDS and Imager state to selectecd input states KWP2000: $31 RoutineControl $5F $00 Modus  : Default
- [STOP_LVDS_IMAGER](#job-stop-lvds-imager) - Set LVDS and Imager state to Default state KWP2000: $32 RoutineControl $5F $00 Modus  : Default
- [START_CLR_CAM_DTC](#job-start-clr-cam-dtc) - Claer camera DTC KWP2000: $31 RoutineControl $60 $00 Modus  : Default
- [START_LIN_HDR](#job-start-lin-hdr) - Enable the HDR functionality KWP2000: $31 RoutineControl $61 $00 Modus  : Default
- [STOP_LIN_HDR](#job-stop-lin-hdr) - Disable the HDR functionality KWP2000: $32 RoutineControl $61 $00 Modus  : Default
- [START_CAM_ERROR_LOG](#job-start-cam-error-log) - Read Camera Error Log KWP2000: $31 RoutineControl $62 $00 Modus  : Default
- [STATUS_CAM_ERROR_LOG](#job-status-cam-error-log) - Read results Camera Error Log KWP2000: $33 RoutineControl $62 $00 Modus  : Default
- [START_VIDEO_FRZ_WATCHDOG](#job-start-video-frz-watchdog) - Start Video freeze watchdog KWP2000: $31 RoutineControl $64 $00 Modus  : Default
- [STOP_VIDEO_FRZ_WATCHDOG](#job-stop-video-frz-watchdog) - Stop Video freeze watchdog KWP2000: $32 RoutineControl $64 $00 Modus  : Default
- [START_CFG_SUPPLIER_DEFAULTS](#job-start-cfg-supplier-defaults) - Set the CFG keep and rebuild structs to default values KWP2000: $31 RoutineControl $65 $00 Modus  : Default
- [START_CAF_DEFAULT_DIDS](#job-start-caf-default-dids) - Set all DIDs to defaults from coding file KWP2000: $31 RoutineControl $66 $00 Modus  : Default
- [START_UPDT_FLASHMEM_CAM](#job-start-updt-flashmem-cam) - Start Trigger Flashmemory Update for cameras KWP2000: $31 RoutineControl $67 $00 Modus  : Default
- [START_UPDT_FLASH_CAM_BL_MODES](#job-start-updt-flash-cam-bl-modes) - Start Trigger Flashmemory Update for cameras from bootloader modes with identical variants KWP2000: $31 RoutineControl $68 $00 Modus  : Default
- [START_CAM_ADC_READINGS](#job-start-cam-adc-readings) - Read camera ADC readings KWP2000: $31 RoutineControl $5E $00 Modus  : Default
- [STOP_CAM_ADC_READINGS](#job-stop-cam-adc-readings) - Stop Reading  camera ADC readings KWP2000: $32 RoutineControl $5E $00 Modus  : Default
- [START_TST_POINT_LEDS](#job-start-tst-point-leds) - start Test Points & LEDs KWP2000: $31 RoutineControl $4E $00 Modus  : Default
- [START_CAM_POWER](#job-start-cam-power) - start Camera Power KWP2000: $31 RoutineControl $52 $00 Modus  : Default
- [STOP_CAM_POWER](#job-stop-cam-power) - stop Camera Power KWP2000: $32 RoutineControl $52 $00 Modus  : Default
- [START_READ_CAM_REG](#job-start-read-cam-reg) - Read Camera Register KWP2000: $31 RoutineControl $40 $00 Modus  : Default
- [STATUS_READ_CAM_REG](#job-status-read-cam-reg) - Stop Read Camera Register KWP2000: $33 RoutineControl $40 $00 Modus  : Default
- [START_WRITE_CAM_REG](#job-start-write-cam-reg) - Start write Camera Register KWP2000: $31 RoutineControl $41 $00 Modus  : Default
- [START_READ_CAM_DATA](#job-start-read-cam-data) - Start Read Camera Data (EEPROM) KWP2000: $31 RoutineControl $42 $00 Modus  : Default
- [STATUS_READ_CAM_DATA](#job-status-read-cam-data) - Status Read Camera Data (EEPROM) KWP2000: $33 RoutineControl $42 $00 Modus  : Default
- [START_WRITE_CAM_DATA](#job-start-write-cam-data) - Status Write Camera Data (EEPROM) KWP2000: $31 RoutineControl $43 $00 Modus  : Default
- [START_CALIB_BMW_ASSEM](#job-start-calib-bmw-assem) - Calibration  for BMW assembly KWP2000: $31 RoutineControl $4C $00 Modus  : Default
- [STATUS_CALIB_RV_MAGNA_SOLV_PARAMS](#job-status-calib-rv-magna-solv-params) - Calibration Rear view Magna target Solver parameters KWP2000: $22 ReadDataByCommonIdentifier $c1 $A6 Modus  : Default
- [SET_CAL_MAGNA_REAR_SOLV_PARAMS](#job-set-cal-magna-rear-solv-params) - Set Calibration Rear view Magna target Solver parameters KWP2000: $2E $C1 $A6 Modus  : Default
- [STATUS_CAL_MAGNA_REAR_GRID_DETAILS](#job-status-cal-magna-rear-grid-details) - Status of Calibration magna Rear grid details KWP2000: $22 ReadDataByCommonIdentifier $c1 $a9 Modus  : Default
- [SET_CAL_MAGNA_REAR_GRID_DETAILS](#job-set-cal-magna-rear-grid-details) - Set Calibration magna Rear grid details KWP2000: $2e ReadDataByCommonIdentifier $c1 $a9 Modus  : Default
- [STATUS_CAL_MAGNA_REAR_DISP](#job-status-cal-magna-rear-disp) - Status Calibration Magana Rear view display KWP2000: $22 $C1 $a7 Modus  : Default
- [SET_CAL_MAGNA_REAR_DISP](#job-set-cal-magna-rear-disp) - Set Calibration Magana Rear view display KWP2000: $2E $C1 $a7 Modus  : Default
- [STATUS_CAL_MAGNA_REAR_GRID_POS](#job-status-cal-magna-rear-grid-pos) - Read Calibration Magna Rear grid positions KWP2000: $22 $C1 $a8 Modus  : Default
- [SET_CAL_MAGNA_REAR_GRID_POS](#job-set-cal-magna-rear-grid-pos) - Set Calibration Magna Rear grid positions KWP2000: $2E $C1 $A8 Modus  : Default
- [READ_DTC_STAT](#job-read-dtc-stat) - Read DTC status KWP2000: $17 Modus  : Default
- [STATUS_USER_BRIGHTNESS](#job-status-user-brightness) - Status of current user brightness(PIA) KWP2000: $22 $C1 $44 Modus  : Default
- [SET_USER_BRIGHTNESS](#job-set-user-brightness) - Set the current user brightness(PIA) KWP2000: $2E $c1 $44 Modus  : Default Set default 0x"D for all cameras 1st byte : Top View brightness 2nd byte : Side View brightness 3rd byte : Rear View brightness
- [STATUS_USER_CONTRAST](#job-status-user-contrast) - Status of current user contrast(PIA) KWP2000: $22 $C1 $45 Modus  : Default
- [SET_USER_CONTRAST](#job-set-user-contrast) - Set the current user contrast(PIA) KWP2000: $2E $c1 $45 Modus  : Default Default set to 0x4B for all cameras 1st byte : Top View contrast 2nd byte : Side View contrast 3rd byte : Rear View contrast
- [STATUS_USER_OVERLAYS](#job-status-user-overlays) - Status of current user overlays enable(PIA) KWP2000: $22 $C1 $65 Modus  : Default
- [SET_USER_OVERLAYS](#job-set-user-overlays) - Set the current user overlays enable(PIA) KWP2000: $2E $c1 $65 Modus  : Default
- [STEUREN_KALIB_RESET](#job-steuren-kalib-reset) - Reset the calibration data of the selected camera KWP2000: $2E $D3 $8E Modus  : Default
- [STATUS_RV_CAM_HEATING_ENABLE](#job-status-rv-cam-heating-enable) - Read statu sof Rear view camera heating enable KWP2000: $22 $C1 $AF Modus  : Default
- [SET_RV_CAM_HEATING_ENABLE](#job-set-rv-cam-heating-enable) - Set Rear view camera heating enable KWP2000: $2E $C1 $AF Modus  : Default
- [STATUS_UPDT_FLASHMEM_CAM](#job-status-updt-flashmem-cam) - Status Trigger Flashmemory Update for cameras KWP2000: $33 RoutineControl $67 $00 Modus  : Default
- [STATUS_UPDT_FLASH_CAM_BL_MODES](#job-status-updt-flash-cam-bl-modes) - Status Trigger Flashmemory Update for cameras from bootloader modes with identical variants KWP2000: $33 RoutineControl $68 $00 Modus  : Default
- [RESET_CALIBRATION_VALUES](#job-reset-calibration-values) - Reset calibration values d38e, CCQ, onl cal record KWP2000: $2E D3 8E $2E C1 A8 $2E C1 Cx Modus  : Default
- [SET_CALIBRATION_DEBUG_OVERLAYS](#job-set-calibration-debug-overlays) - Set development use only - enable / disable calibration overalys KWP2000: $2E $C1 $DB Modus  : Default
- [STATUS_ONL_CALIB](#job-status-onl-calib) - Status of online calibration quality KWP2000: $22 $D3 $CC Modus  : Default
- [STATUS_ONL_CALIB_QUALITY](#job-status-onl-calib-quality) - Status of online calibration quality KWP2000: $22 $D3 $CE Modus  : Default

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

<a id="job-enable-fs-rear-view-mode"></a>
### ENABLE_FS_REAR_VIEW_MODE

Enable Full Screen Rear View KWP2000: $31 RoutineControl $49 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-disable-rear-view-mode"></a>
### DISABLE_REAR_VIEW_MODE

Disable Full Screen Rear View KWP2000: $32 RoutineControl $49 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-top-view-mode"></a>
### ENABLE_TOP_VIEW_MODE

Enable Top View KWP2000: $31 RoutineControl $47 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-disable-top-view-mode"></a>
### DISABLE_TOP_VIEW_MODE

Disable Top View KWP2000: $32 RoutineControl $47 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-side-view-mode"></a>
### ENABLE_SIDE_VIEW_MODE

Enable Side View KWP2000: $31 RoutineControl $48 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-disable-side-view-mode"></a>
### DISABLE_SIDE_VIEW_MODE

Disable Side View KWP2000: $32 RoutineControl $48 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-fs-top-view-left-overlay-cel"></a>
### ENABLE_FS_TOP_VIEW_LEFT_OVERLAY_CEL

Enable Full Screen TVL Overlay CEL Manf KWP2000: $31 RoutineControl $4B $00 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-fs-top-view-right-cel"></a>
### ENABLE_FS_TOP_VIEW_RIGHT_CEL

Enable Full Screen TVR CEL Manf KWP2000: $31 RoutineControl $4A $00 $01 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-autoadr-kam"></a>
### START_AUTOADR_KAM

New camera learning KWP2000: $31 RoutineControl $21 $00 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-autoadr-kam"></a>
### STOP_AUTOADR_KAM

Stop new camera learning KWP2000: $32 RoutineControl $21 $00 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-autoadr-kam"></a>
### STATUS_AUTOADR_KAM

Status of camera learning KWP2000: $33 RoutineControl $21 $00 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TV_LEFT | unsigned char | Refer STAT_RV comments |
| STAT_TV_RIGHT | unsigned char | Refer STAT_RV comments |
| STAT_SV_LEFT | unsigned char | Refer STAT_RV comments |
| STAT_SV_RIGHT | unsigned char | Refer STAT_RV comments |
| STAT_RV | unsigned char | 0x00 Job finalized or not requested 0x01 Job Running (Busy) 0x02 Job Successfully Performed 0x03 CAM/ECU not comptible 0x04 Missing camera 0x05 Wrong Camera detected |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abweichung-tvl-kam"></a>
### ABWEICHUNG_TVL_KAM

Deviation in mm of mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $7a Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| DEV_X_MM | int | Deviation X in mm |
| DEV_Y_MM | int | Deviation Y in mm |
| DEV_Z_MM | int | Deviation Z in mm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abweichung-tvr-kam"></a>
### ABWEICHUNG_TVR_KAM

Deviation in mm of the mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $7b Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| DEV_X_MM | int | Deviation X in mm |
| DEV_Y_MM | int | Deviation Y in mm |
| DEV_Z_MM | int | Deviation Z in mm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abweichung-rv-kam"></a>
### ABWEICHUNG_RV_KAM

Deviation in mm of mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $7D Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| DEV_X_MM | int | Deviation X in mm |
| DEV_Y_MM | int | Deviation z in mm |
| DEV_Z_MM | int | Deviation Z in mm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-tv-right-cam-pos"></a>
### SET_TV_RIGHT_CAM_POS

Set Top view right camera positions KWP2000: $2E $C1 $60 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_POS_DATA | binary | default E70M Cam positions 1byte lsb(rot_x1_deg_64) 2byte msb(rot_x1_deg_64) 3byte lsb(rot_z1_deg_64) 4byte msb(rot_z1_deg_64) 5byte lsb(rot_z2_deg_64) 6byte msb(rot_z2_deg_64) 7byte lsb(point_x_mm) 8byte msb(point_x_mm) 9byte lsb(point_y_mm) 10byte msb(point_y_mm) 11byte lsb(point_z_mm) 12byte msb(point_z_mm) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-tv-left-cam-pos"></a>
### SET_TV_LEFT_CAM_POS

Set Top view left camera positions KWP2000: $2E $C1 $61 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_POS_DATA | binary | 1byte lsb(rot_x1_deg_64) 2byte msb(rot_x1_deg_64) 3byte lsb(rot_z1_deg_64) 4byte msb(rot_z1_deg_64) 5byte lsb(rot_z2_deg_64) 6byte msb(rot_z2_deg_64) 7byte lsb(point_x_mm) 8byte msb(point_x_mm) 9byte lsb(point_y_mm) 10byte msb(point_y_mm) 11byte lsb(point_z_mm) 12byte msb(point_z_mm) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tv-right-cam-pos"></a>
### STATUS_TV_RIGHT_CAM_POS

Set Top view right camera positions KWP2000: $22 $C1 $60 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | Rotation of X in degrees |
| STAT_ROT_Z1_DEG | int | Rotation of z1 in degrees |
| STAT_ROT_Z2_DEG | int | Rotation of z2 in degrees |
| STAT_X_MM | int | X in mm |
| STAT_Y_MM | int | Y in mm |
| STAT_Z_MM | int | Z in mm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rv-cam-pos"></a>
### STATUS_RV_CAM_POS

Set Rear view cam positions KWP2000: $22 $C1 $62 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | Rotation of X in degrees |
| STAT_ROT_Z1_DEG | int | Rotation of Z1 in degrees |
| STAT_ROT_Z2_DEG | int | Rotation of z2 in degrees |
| STAT_X_MM | int | X in mm |
| STAT_Y_MM | int | Y in mm |
| STAT_Z_MM | int | Z in mm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tv-left-cam-pos"></a>
### STATUS_TV_LEFT_CAM_POS

Set Top view left camera positions KWP2000: $22 $C1 $61 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | Rotation of X in degrees |
| STAT_ROT_Z1_DEG | int | Rotation of z1 in degrees |
| STAT_ROT_Z2_DEG | int | Rotation of z2 in degrees |
| STAT_X_MM | int | X in mm |
| STAT_Y_MM | int | Y in mm |
| STAT_Z_MM | int | Z in mm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-rv-cam-pos"></a>
### SET_RV_CAM_POS

Set Rear view camera positions KWP2000: $2E $C1 $62 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_POS_DATA | binary | 1byte lsb(rot_x_deg_64) 2byte msb(rot_x_deg_64) 3byte lsb(rot_y_deg_64) 4byte msb(rot_y_deg_64) 5byte lsb(rot_z_deg_64) 6byte msb(rot_z_deg_64) 7byte lsb(point_x_mm) 8byte msb(point_x_mm) 9byte lsb(point_y_mm) 10byte msb(point_y_mm) 11byte lsb(point_z_mm) 12byte msb(point_z_mm) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-output-video-tst-patrn-ntsc"></a>
### ENABLE_OUTPUT_VIDEO_TST_PATRN_NTSC

Enable NTSC Encoder Colour bar KWP2000: $31 RoutineControl $45 $00 $06 $00 $00 $00 $00 $00 $00 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-output-video-tst-patrn-dsp"></a>
### ENABLE_OUTPUT_VIDEO_TST_PATRN_DSP

Enable DSP Encoder Colour bar KWP2000: $31 RoutineControl $45 $00 $00 $00 $00 $00 $00 $00 $00 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-power-to-dsp-cam"></a>
### ENABLE_POWER_TO_DSP_CAM

Enbale POWER for DSP and Cameras KWP2000: $31 RoutineControl $46 $00 $01 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-disable-power-to-dsp-cam"></a>
### DISABLE_POWER_TO_DSP_CAM

Disbale POWER for DSP and Cameras KWP2000: $31 RoutineControl $46 $00 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-fs-top-view-right-overlay-cel"></a>
### ENABLE_FS_TOP_VIEW_RIGHT_OVERLAY_CEL

Enable Full Screen TVR Overlay CEL Manf KWP2000: $31 RoutineControl $4A $00 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-disable-output-test-pattern"></a>
### DISABLE_OUTPUT_TEST_PATTERN

Disable Colour bar KWP2000: $32 RoutineControl $45 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-disable-fs-top-view-left-cel"></a>
### DISABLE_FS_TOP_VIEW_LEFT_CEL

Disable Full Screen TVL CEL Manf KWP2000: $32 RoutineControl $4B $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-disable-fs-top-view-right-cel"></a>
### DISABLE_FS_TOP_VIEW_RIGHT_CEL

Diable Full Screen TVR CEL Manf KWP2000: $32 RoutineControl $4A $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-fs-top-view-left-cel"></a>
### ENABLE_FS_TOP_VIEW_LEFT_CEL

Enable Full Screen TVL CEL Manf KWP2000: $31 RoutineControl $4B $00 $01 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dsp-app-supplier-ver"></a>
### DSP_APP_SUPPLIER_VER

DSP Application Version KWP2000: $22 ReadDataByCommonIdentifier $c1 $02 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| DSP_APP_VER | string | DSP App version num |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dsp-pbl-a-supplier-ver"></a>
### DSP_PBL_A_SUPPLIER_VER

DSP PBL A Version KWP2000: $22 ReadDataByCommonIdentifier $c1 $03 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| DSP_PBL_A_VER | string | DSP App version num |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dsp-pbl-b-supplier-ver"></a>
### DSP_PBL_B_SUPPLIER_VER

DSP PBL B Version KWP2000: $22 ReadDataByCommonIdentifier $c1 $04 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| DSP_PBL_B_VER | string | DSP PblA version num |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dsp-pre-pbl-supplier-ver"></a>
### DSP_PRE_PBL_SUPPLIER_VER

DSP Pre PBL Version KWP2000: $22 ReadDataByCommonIdentifier $c1 $05 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| DSP_PRE_PBL_VER | string | DSP prePBl version num |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-winkelverdrehung-tvr-kam"></a>
### WINKELVERDREHUNG_TVR_KAM

Deviation of the mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $78 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| ANGLE_DEV_X | int | Deviation X in 10th degrees |
| ANGLE_DEV_Y | int | Deviation Y in 10th degrees |
| ANGLE_DEV_Z | int | Deviation Z in 10th degrees |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-winkelverdrehung-rv-kam"></a>
### WINKELVERDREHUNG_RV_KAM

Deviation of the mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $70 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| ANGLE_DEV_X | int | Deviation X in 10th degrees |
| ANGLE_DEV_Y | int | Deviation Y in 10th degrees |
| ANGLE_DEV_Z | int | Deviation Z in 10th degrees |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-winkelverdrehung-tvl-kam"></a>
### WINKELVERDREHUNG_TVL_KAM

Deviation of the mounting position on the vehicle KWP2000: $22 RoutineControl $d3 $79 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| ANGLE_DEV_X | int | Deviation X in 10th degrees |
| ANGLE_DEV_Y | int | Deviation Y in 10th degrees |
| ANGLE_DEV_Z | int | Deviation Z in 10th degrees |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-host-app-supplier-ver"></a>
### HOST_APP_SUPPLIER_VER

HOST Application Version KWP2000: $22 ReadDataByCommonIdentifier $c1 $01 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| HOST_APP_VER | string | Host app version |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-ecu-var"></a>
### READ_ECU_VAR

ECU variant KWP2000: $22 ReadDataByCommonIdentifier $c1 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| ECU_VAR | int | ECU variant |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-steuern-tvc-kalib-abweich"></a>
### SET_STEUERN_TVC_KALIB_ABWEICH

Set service calibration deviation KWP2000: $2E $D3 $B2 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KAMERA | unsigned int | camera (0=TV_L 1=TV_R 2=RV) |
| REFERENZBILD | unsigned int | 0=Kalibrieren abbrechen ohne Wertspeicherung 1=Kalibrieren starten 2=Kalibrieren beenden und Werte speichern |
| ABWEICHUNG_X | int | abweichung von der X-Achse |
| ABWEICHUNG_Y | int | abweichung von der Y-Achse |
| ABWEICHUNG_Z | int | abweichung von der Z-Achse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-steuern-tvc-kalib-ver"></a>
### SET_STEUERN_TVC_KALIB_VER

Set service calibration rotation KWP2000: $2E $D3 $B3 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KAMERA | unsigned int | camera (0=TV_L 1=TV_R 2=RV) |
| REFERENZBILD | unsigned int | 0=Kalibrieren abbrechen ohne Wertspeicherung 1=Kalibrieren starten 2=Kalibrieren beenden und Werte speichern |
| ROTATION_X | int | Rotation of the X-axis |
| ROTATION_Y | int | Rotation of the Y-axis |
| ROTATION_Z | int | Rotation of the Z-axis |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-srv-rv-virt-cam"></a>
### STATUS_SRV_RV_VIRT_CAM

Set Rear view right cam positions KWP2000: $22 $C1 $81 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_HFOV_DEG | unsigned int | Horizontal field of view in degrees |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | int | 1 flips image in x |
| STAT_FLIP_Y | int | 1 flips image in y |
| STAT_ANTIALIAS | char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | int | Do not use |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-srv-tvr-virt-cam"></a>
### STATUS_SRV_TVR_VIRT_CAM

Set Rear view right cam positions KWP2000: $22 $C1 $7F Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_HFOV_DEG | unsigned int | Horizontal field of view in degrees |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | int | 1 flips image in x |
| STAT_FLIP_Y | int | 1 flips image in y |
| STAT_ANTIALIAS | char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | int | Do not use |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-srv-tvl-virt-cam"></a>
### STATUS_SRV_TVL_VIRT_CAM

Set Rear view right cam positions KWP2000: $22 $C1 $80 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_HFOV_DEG | unsigned int | Horizontal field of view in degrees |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | int | 1 flips image in x |
| STAT_FLIP_Y | int | 1 flips image in y |
| STAT_ANTIALIAS | char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | int | Do not use |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-srv-calib-rv-virt-cam"></a>
### SET_SRV_CALIB_RV_VIRT_CAM

Set service calibration TVL virtual camera KWP2000: $2E $C1 $81 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_VIRT_DATA | binary | default values == 0x00 1byte lsb(rot_x_deg_64) 2byte msb(rot_x_deg_64) 3byte lsb(rot_z1_deg_64) 4byte msb(rot_z1_deg_64) 5byte lsb(rot_z2_deg_64) 6byte msb(rot_z2_deg_64) 7byte lsb(hfov_deg_64) 8byte msb(hfov_deg_64) 9byte lsb(disp_aspect) 10byte msb(disp_aspect) 11byte (flipx) 12byte (flipy) 13byte (antialias) 14byte (auto_bright) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-srv-calib-tvr-virt-cam"></a>
### SET_SRV_CALIB_TVR_VIRT_CAM

Set service calibration TVR virtual camera KWP2000: $2E $C1 $7F Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_VIRT_DATA | binary | default values == 0x00 1byte lsb(rot_x_deg_64) 2byte msb(rot_x_deg_64) 3byte lsb(rot_z1_deg_64) 4byte msb(rot_z1_deg_64) 5byte lsb(rot_z2_deg_64) 6byte msb(rot_z2_deg_64) 7byte lsb(hfov_deg_64) 8byte msb(hfov_deg_64) 9byte lsb(disp_aspect) 10byte msb(disp_aspect) 11byte (flipx) 12byte (flipy) 13byte (antialias) 14byte (auto_bright) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-srv-calib-tvl-virt-cam"></a>
### SET_SRV_CALIB_TVL_VIRT_CAM

Set service calibration TVL virtual camera KWP2000: $2E $C1 $80 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_VIRT_DATA | binary | default values == 0x00 1byte lsb(rot_x_deg_64) 2byte msb(rot_x_deg_64) 3byte lsb(rot_z1_deg_64) 4byte msb(rot_z1_deg_64) 5byte lsb(rot_z2_deg_64) 6byte msb(rot_z2_deg_64) 7byte lsb(hfov_deg_64) 8byte msb(hfov_deg_64) 9byte lsb(disp_aspect) 10byte msb(disp_aspect) 11byte (flipx) 12byte (flipy) 13byte (antialias) 14byte (auto_bright) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-kalib-montage"></a>
### START_KALIB_MONTAGE

Start calibration with selected target KWP2000: $31 RoutineControl $20 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TARGET_TYPE | unsigned char | 0x0 : Valeo RV calibration 0x1 : Magna RV calibration |
| CAMERA_CHOICE | unsigned char | 0x0 : ALL cameras sequentially 0x1 : Left Top View Camera 0x2 : Right Top View Camera 0x3 : Rear View Camera |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-kalib-montage"></a>
### STOP_KALIB_MONTAGE

Stop calibration with selected target KWP2000: $32 RoutineControl $20 $00 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kalib-montage"></a>
### STATUS_KALIB_MONTAGE

Status of calibration KWP2000: $33 RoutineControl $20 $00 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TARGET_TYPE | char | 0x0 : Valeo RV calibration 0x1 : Magna RV calibration |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TARGET_TYPE | unsigned char | Refer STAT_RV comments |
| STAT_TV_LEFT | unsigned char | Refer STAT_RV comments |
| STAT_TV_RIGHT | unsigned char | Refer STAT_RV comments |
| STAT_RV | unsigned char | 0x0 Calibration finalized or not requested 0x1 Calibration runs 0x2 Calibration successfully finished 0x3 Camera not installed 0x4 No traget found 0x5 Targets beyond range 0x6 Not sufficient picture quality 0x7 Calibration aborted |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecu-temp"></a>
### ECU_TEMP

ECU temerature KWP2000: $22 ReadDataByCommonIdentifier $c1 $06 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| ECU_TEMP | char | ECU temperature |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-tvr-cam-info"></a>
### TVR_CAM_INFO

TV right camera information KWP2000: $22 ReadDataByCommonIdentifier $c1 $07 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| LIN_PRESENT | unsigned char | Hex-Antwort von SG |
| SERIAL_NUM | binary | Hex-Antwort von SG |
| CMOS_ID | unsigned int | Hex-Antwort von SG |
| LENS_TYPE | unsigned char | Hex-Antwort von SG |
| VARIANT_ID | unsigned char | Hex-Antwort von SG |
| PARAMS_STORED | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-tvl-cam-info"></a>
### TVL_CAM_INFO

TV left camera information KWP2000: $22 ReadDataByCommonIdentifier $c1 $08 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| LIN_PRESENT | unsigned char | Hex-Antwort von SG |
| SERIAL_NUM | binary | Hex-Antwort von SG |
| CMOS_ID | unsigned int | Hex-Antwort von SG |
| LENS_TYPE | unsigned char | Hex-Antwort von SG |
| VARIANT_ID | unsigned char | Hex-Antwort von SG |
| PARAMS_STORED | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-svr-cam-info"></a>
### SVR_CAM_INFO

SV right camera information KWP2000: $22 ReadDataByCommonIdentifier $c1 $09 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| LIN_PRESENT | unsigned char | Hex-Antwort von SG |
| SERIAL_NUM | binary | Hex-Antwort von SG |
| CMOS_ID | unsigned int | Hex-Antwort von SG |
| LENS_TYPE | unsigned char | Hex-Antwort von SG |
| VARIANT_ID | unsigned char | Hex-Antwort von SG |
| PARAMS_STORED | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-svl-cam-info"></a>
### SVL_CAM_INFO

SV left camera information KWP2000: $22 ReadDataByCommonIdentifier $c1 $0a Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| LIN_PRESENT | unsigned char | Hex-Antwort von SG |
| SERIAL_NUM | binary | Hex-Antwort von SG |
| CMOS_ID | unsigned int | Hex-Antwort von SG |
| LENS_TYPE | unsigned char | Hex-Antwort von SG |
| VARIANT_ID | unsigned char | Hex-Antwort von SG |
| PARAMS_STORED | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-rv-cam-info"></a>
### RV_CAM_INFO

Rear view camera information KWP2000: $22 ReadDataByCommonIdentifier $c1 $07 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| LIN_PRESENT | unsigned char | Hex-Antwort von SG |
| SERIAL_NUM | binary | Hex-Antwort von SG |
| CMOS_ID | unsigned int | Hex-Antwort von SG |
| LENS_TYPE | unsigned char | Hex-Antwort von SG |
| VARIANT_ID | unsigned char | Hex-Antwort von SG |
| PARAMS_STORED | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tvr-cam"></a>
### STATUS_TVR_CAM

TVR cam status KWP2000: $22 ReadDataByCommonIdentifier $c1 $0c Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CAM | int | cam status |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tvl-cam"></a>
### STATUS_TVL_CAM

TVL cam status KWP2000: $22 ReadDataByCommonIdentifier $c1 $0D Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CAM | int | cam status |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-svr-cam"></a>
### STATUS_SVR_CAM

SVR cam status KWP2000: $22 ReadDataByCommonIdentifier $c1 $0e Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CAM | int | cam status |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-svl-cam"></a>
### STATUS_SVL_CAM

SVL cam status KWP2000: $22 ReadDataByCommonIdentifier $c1 $0f Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CAM | int | cam status |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rv-cam"></a>
### STATUS_RV_CAM

RV cam status KWP2000: $22 ReadDataByCommonIdentifier $c1 $10 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CAM | int | cam status |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tvr-disp-calib"></a>
### STATUS_TVR_DISP_CALIB

Status TV Right display calibration KWP2000: $22 $C1 $28 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_CEN_POINT_XMM | int | Area centre point X mm |
| STAT_CEN_POINT_YMM | int | Area centre point Y mm |
| STAT_CEN_POINT_ZMM | int | Area centre point Z mm |
| STAT_AREA_WIDTH_MM | int | Area width mm |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | unsigned char | 1 flips image in x |
| STAT_FLIP_Y | unsigned char | 1 flips image in y |
| STAT_ANTIALIAS | unsigned char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | unsigned char | not used |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tvl-disp-calib"></a>
### STATUS_TVL_DISP_CALIB

Status TV left display calibration KWP2000: $22 $C1 $29 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_CEN_POINT_XMM | int | Area centre point X mm |
| STAT_CEN_POINT_YMM | int | Area centre point Y mm |
| STAT_CEN_POINT_ZMM | int | Area centre point Z mm |
| STAT_AREA_WIDTH_MM | int | Area width mm |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | unsigned char | 1 flips image in x |
| STAT_FLIP_Y | unsigned char | 1 flips image in y |
| STAT_ANTIALIAS | unsigned char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | unsigned char | not used |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-uv-rear-disp-calib"></a>
### STATUS_UV_REAR_DISP_CALIB

Status U view Rear display calibration KWP2000: $22 $C1 $2a Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_CEN_POINT_XMM | int | Area centre point X mm |
| STAT_CEN_POINT_YMM | int | Area centre point Y mm |
| STAT_CEN_POINT_ZMM | int | Area centre point Z mm |
| STAT_AREA_WIDTH_MM | int | Area width mm |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | unsigned char | 1 flips image in x |
| STAT_FLIP_Y | unsigned char | 1 flips image in y |
| STAT_ANTIALIAS | unsigned char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | unsigned char | not used |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fs-rear-disp-calib"></a>
### STATUS_FS_REAR_DISP_CALIB

Status FS rear display calibration KWP2000: $22 $C1 $2B Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_CEN_POINT_XMM | int | Area centre point X mm |
| STAT_CEN_POINT_YMM | int | Area centre point Y mm |
| STAT_CEN_POINT_ZMM | int | Area centre point Z mm |
| STAT_AREA_WIDTH_MM | int | Area width mm |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | unsigned char | 1 flips image in x |
| STAT_FLIP_Y | unsigned char | 1 flips image in y |
| STAT_ANTIALIAS | unsigned char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | unsigned char | not used |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bmw-fsr-disp-calib"></a>
### STATUS_BMW_FSR_DISP_CALIB

Status BMW production calibration FS rear display calibration KWP2000: $22 $C1 $2C Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_CEN_POINT_XMM | int | Area centre point X mm |
| STAT_CEN_POINT_YMM | int | Area centre point Y mm |
| STAT_CEN_POINT_ZMM | int | Area centre point Z mm |
| STAT_AREA_WIDTH_MM | int | Area width mm |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | unsigned char | 1 flips image in x |
| STAT_FLIP_Y | unsigned char | 1 flips image in y |
| STAT_ANTIALIAS | unsigned char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | unsigned char | not used |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tvr-cam-cal-data"></a>
### STATUS_TVR_CAM_CAL_DATA

Read TV right camera clibration data KWP2000: $22 ReadDataByCommonIdentifier $c1 $16 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_FISHEYE_AMT | unsigned char | Hex-Antwort von SG |
| STAT_CXOFFS_PIX_3RDS | char | Hex-Antwort von SG |
| STAT_CYOFFS_PIX_3RDS | char | Hex-Antwort von SG |
| STAT_CAM_ASPECT_OFFS | char | Hex-Antwort von SG |
| STAT_HFOV_DEG_64TH | unsigned int | Hex-Antwort von SG |
| STAT_OPT_AXIS_X_OFFS_PIX | char | Hex-Antwort von SG |
| STAT_OPT_AXIS_Y_OFFS_PIX | char | Hex-Antwort von SG |
| STAT_OPT_AXIS_Z_OFFS_PIX | char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tvl-cam-cal-data"></a>
### STATUS_TVL_CAM_CAL_DATA

Read TV left camera clibration data KWP2000: $22 ReadDataByCommonIdentifier $c1 $17 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_FISHEYE_AMT | unsigned char | Hex-Antwort von SG |
| STAT_CXOFFS_PIX_3RDS | char | Hex-Antwort von SG |
| STAT_CYOFFS_PIX_3RDS | char | Hex-Antwort von SG |
| STAT_CAM_ASPECT_OFFS | char | Hex-Antwort von SG |
| STAT_HFOV_DEG_64TH | unsigned int | Hex-Antwort von SG |
| STAT_OPT_AXIS_X_OFFS_PIX | char | Hex-Antwort von SG |
| STAT_OPT_AXIS_Y_OFFS_PIX | char | Hex-Antwort von SG |
| STAT_OPT_AXIS_Z_OFFS_PIX | char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rv-cam-cal-data"></a>
### STATUS_RV_CAM_CAL_DATA

Read RV camera clibration data KWP2000: $22 ReadDataByCommonIdentifier $c1 $18 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_FISHEYE_AMT | unsigned char | Hex-Antwort von SG |
| STAT_CXOFFS_PIX_3RDS | char | Hex-Antwort von SG |
| STAT_CYOFFS_PIX_3RDS | char | Hex-Antwort von SG |
| STAT_CAM_ASPECT_OFFS | char | Hex-Antwort von SG |
| STAT_HFOV_DEG_64TH | unsigned int | Hex-Antwort von SG |
| STAT_OPT_AXIS_X_OFFS_PIX | char | Hex-Antwort von SG |
| STAT_OPT_AXIS_Y_OFFS_PIX | char | Hex-Antwort von SG |
| STAT_OPT_AXIS_Z_OFFS_PIX | char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-calib-ovl-grid"></a>
### STATUS_CALIB_OVL_GRID

Status of calibration overlay gris data KWP2000: $22 ReadDataByCommonIdentifier $c1 $2E Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ON | unsigned char | Hex-Antwort von SG |
| STAT_HORIZ | unsigned char | Hex-Antwort von SG |
| STAT_VERT | unsigned char | Hex-Antwort von SG |
| STAT_LUM | unsigned char | Hex-Antwort von SG |
| STAT_CR | unsigned char | Hex-Antwort von SG |
| STAT_CB | unsigned char | Hex-Antwort von SG |
| STAT_TRANSP | unsigned char | Hex-Antwort von SG |
| STAT_SPILT | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bmw-fsr-grid-layout"></a>
### STATUS_BMW_FSR_GRID_LAYOUT

Status of BMW assembly calibration FS rear grid layout KWP2000: $22 ReadDataByCommonIdentifier $c1 $68 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_LINE_WIDTH | unsigned char | Hex-Antwort von SG |
| STAT_NUM_H_LINES | unsigned char | Hex-Antwort von SG |
| STAT_NUM_V_LINES | unsigned char | Hex-Antwort von SG |
| STAT_SPLIT_NUM_COLMN | unsigned char | Hex-Antwort von SG |
| STAT_SPLIT_NUM_ROW | unsigned char | Hex-Antwort von SG |
| STAT_LEFT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_RIGHT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_TOP_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_BOTT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_GRID_COLOUR | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rv-cal-target-pos"></a>
### STATUS_RV_CAL_TARGET_POS

Read RV calibration target position KWP2000: $22 $C1 $71 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | Rotation of X in degrees |
| STAT_ROT_Z1_DEG | int | Rotation of Z1 in degrees |
| STAT_ROT_Z2_DEG | int | Rotation of z2 in degrees |
| STAT_X_MM | int | X in mm |
| STAT_Y_MM | int | Y in mm |
| STAT_Z_MM | int | Z in mm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tvr-cal-target-pos"></a>
### STATUS_TVR_CAL_TARGET_POS

Read TV Right calibration target position KWP2000: $22 $C1 $69 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | Rotation of X in degrees |
| STAT_ROT_Z1_DEG | int | Rotation of z1 in degrees |
| STAT_ROT_Z2_DEG | int | Rotation of z2 in degrees |
| STAT_X_MM | int | X in mm |
| STAT_Y_MM | int | Y in mm |
| STAT_Z_MM | int | Z in mm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tvl-cal-target-pos"></a>
### STATUS_TVL_CAL_TARGET_POS

Read TV Left calibration target position KWP2000: $22 $C1 $70 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | Rotation of X in degrees |
| STAT_ROT_Z1_DEG | int | Rotation of z1 in degrees |
| STAT_ROT_Z2_DEG | int | Rotation of z2 in degrees |
| STAT_X_MM | int | X in mm |
| STAT_Y_MM | int | Y in mm |
| STAT_Z_MM | int | Z in mm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bmw-rv-cal-solv-params"></a>
### STATUS_BMW_RV_CAL_SOLV_PARAMS

Read BMW RV assembly calibration solver parameters KWP2000: $22 $C1 $76 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-maximaleblocklaenge"></a>
### STATUS_MAXIMALEBLOCKLAENGE

Status Maximum block length KWP2000: $22 $25 $06 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_MAX_LENGTH | int | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-programming-state"></a>
### STATUS_PROGRAMMING_STATE

Read programming state KWP2000: $31 $0a Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_PROG_STATE | char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bus-nachrichten"></a>
### STATUS_BUS_NACHRICHTEN

Status of CAN Speed KWP2000: $22 $D2 $40 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CAN_SPEED | int | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bus-in-sv-ein"></a>
### STATUS_BUS_IN_SV_EIN

Status of Side view camera active or not KWP2000: $22 $D3 $B5 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_SV_CAMERA | char | 1 - Active 0 - Not Active |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-heckklappe"></a>
### STATUS_HECKKLAPPE

Read Boot status KWP2000: $22 $D3 $7c Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_STUFF_BYTE | unsigned char | Hex-Antwort von SG |
| STAT_BOOT_STATUS | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ausstattung"></a>
### STATUS_AUSSTATTUNG

Status of RV, TV, SV modes avalibale KWP2000: $22 $D3 $7F Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TV_AVAILBLE | unsigned int | 0 - Not Available 1 - Available |
| STAT_SV_AVAILBLE | unsigned int | Hex-Antwort von SG |
| STAT_RV_AVAILBLE | unsigned int | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-stromaufnahme-kamera-tsv"></a>
### STATUS_STROMAUFNAHME_KAMERA_TSV

Status of current consumption of TV and SV KWP2000: $22 $D3 $80 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TVL_CURRENT | unsigned int | Hex-Antwort von SG |
| STAT_TVR_CURRENT | unsigned int | Hex-Antwort von SG |
| STAT_SVL_CURRENT | unsigned int | Hex-Antwort von SG |
| STAT_SVR_CURRENT | unsigned int | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-initialisierung-tv"></a>
### STATUS_INITIALISIERUNG_TV

Status of TVL, TVR camera init KWP2000: $22 $D3 $81 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TVL_INIT | unsigned int | 0x1  - Initialized 0xFF - Not Initialized |
| STAT_TVR_INIT | unsigned int | 0x1  - Initialized 0xFF - Not Initialized |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bus-vordertueren"></a>
### STATUS_BUS_VORDERTUEREN

Status of front doors KWP2000: $22 $D3 $83 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_FRONT_DOOR_LEFT | unsigned char | Hex-Antwort von SG |
| STAT_FRONT_DOOR_RIGHT | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bus-nachrichten-d392"></a>
### STATUS_BUS_NACHRICHTEN_D392

Status information about CAN Signal TV, RV requested KWP2000: $22 $D3 $92 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TV_REQUEST | unsigned char | Hex-Antwort von SG |
| STAT_RV_REQUEST | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bus-nachrichten-d395"></a>
### STATUS_BUS_NACHRICHTEN_D395

Status CAN Signals regarding the mirror fold-/unfold status KWP2000: $22 $D3 $95 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_WING_MIRROR_RIGHT | unsigned char | Hex-Antwort von SG |
| STAT_WING_MIRROR_LEFT | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kalibrierung-tv"></a>
### STATUS_KALIBRIERUNG_TV

Top view calibration status KWP2000: $22 $D3 $9C Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TVL_CALIB | unsigned char | Hex-Antwort von SG |
| STAT_TVR_CALIB | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kalibrierung-rv"></a>
### STATUS_KALIBRIERUNG_RV

Top view calibration status KWP2000: $22 $D3 $9D Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_RV_CALIB | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-stromaufnahme-kamera-rv"></a>
### STATUS_STROMAUFNAHME_KAMERA_RV

Rear view camera current consumption KWP2000: $22 $D3 $9E Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_RV_CURRENT | unsigned int | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-initialisierung-rv"></a>
### STATUS_INITIALISIERUNG_RV

Status of RV camera init KWP2000: $22 $D3 $9F Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_RV_INIT | unsigned int | 0x1  - Initialized 0xFF - Not Initialized |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klemmen-15n-wert-dad2"></a>
### STATUS_KLEMMEN_15N_WERT_DAD2

Status_klemmen (15N wert) KWP2000: $22 $DA $D2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_BATTERY_VOLTAGE | unsigned int | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klemmen-15n-ein"></a>
### STATUS_KLEMMEN_15N_EIN

Status of KL15N KWP2000: $22 $DA $FE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_KL15_ACTIVE_VALUE | unsigned char | 0 - KL15_OFF 1 - KL15_ON |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klemmen-15n-wert-db2d"></a>
### STATUS_KLEMMEN_15N_WERT_DB2D

CAN signal b_ST_KL_15_b KWP2000: $22 $DB $2D Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_KL15N | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-coding-data"></a>
### STATUS_CODING_DATA

Read the coding data block KWP2000: $22 RoutineControl $30 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_ID_MSB | char | 0x30 is valid block_id_msb |
| BLOCK_ID_LSB | char | 0x00,0x01,0x05,0x06,0x07,0x08,0x09 are valid block_id_lsb |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-bus-in-sv-ein"></a>
### SET_BUS_IN_SV_EIN

Enable the SV play mode KWP2000: $2E $D3 $B5 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PLAY_MODE_ACTIVATE | unsigned char | 0x0 : Inactive 0x1 : Activate |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-steuern-testbild-kamera"></a>
### SET_STEUERN_TESTBILD_KAMERA

Set KWP2000: $2E $D3 $B4 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECT | char | Camera selection, TV, SV, RV 0 - TVL 1 - TVR 2 - RV 3 - SVL 4 - SVR |
| OVL_REQUEST | char | 1 - OVL active request 0 - OVL disabled |
| TIME_OUT_OPTION | char | 0x00 - Option OFF, Inactive play mode 0xFF - ON, with out timer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-camera-soiling"></a>
### STATUS_CAMERA_SOILING

Status of TV,SV,RV camera soiling KWP2000: $22 ReadDataByCommonIdentifier $c1 $30 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TVL_PERC_SOILING | unsigned char | Hex-Antwort von SG |
| STAT_TVR_PERC_SOILING | unsigned char | Hex-Antwort von SG |
| STAT_SVL_PERC_SOILING | unsigned char | Hex-Antwort von SG |
| STAT_SVR_PERC_SOILING | unsigned char | Hex-Antwort von SG |
| STAT_RV_PERC_SOILING | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bmw-tv-cal-solv-params"></a>
### STATUS_BMW_TV_CAL_SOLV_PARAMS

Read BMW TV assembly calibration solver parameters KWP2000: $22 $C1 $53 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bmw-tvl-grid-layout"></a>
### STATUS_BMW_TVL_GRID_LAYOUT

Status of BMW assembly calibration Top view left grid layout KWP2000: $22 ReadDataByCommonIdentifier $c1 $55 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_LINE_WIDTH | unsigned char | Hex-Antwort von SG |
| STAT_NUM_H_LINES | unsigned char | Hex-Antwort von SG |
| STAT_NUM_V_LINES | unsigned char | Hex-Antwort von SG |
| STAT_SPLIT_NUM_COLMN | unsigned char | Hex-Antwort von SG |
| STAT_SPLIT_NUM_ROW | unsigned char | Hex-Antwort von SG |
| STAT_LEFT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_RIGHT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_TOP_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_BOTT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_GRID_COLOUR | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bmw-tvr-grid-layout"></a>
### STATUS_BMW_TVR_GRID_LAYOUT

Status of BMW assembly calibration Top view right grid layout KWP2000: $22 ReadDataByCommonIdentifier $c1 $57 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_LINE_WIDTH | unsigned char | Hex-Antwort von SG |
| STAT_NUM_H_LINES | unsigned char | Hex-Antwort von SG |
| STAT_NUM_V_LINES | unsigned char | Hex-Antwort von SG |
| STAT_SPLIT_NUM_COLMN | unsigned char | Hex-Antwort von SG |
| STAT_SPLIT_NUM_ROW | unsigned char | Hex-Antwort von SG |
| STAT_LEFT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_RIGHT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_TOP_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_BOTT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_GRID_COLOUR | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-calibration-performed"></a>
### STATUS_CALIBRATION_PERFORMED

Status of calibration performed or not KWP2000: $22 ReadDataByCommonIdentifier $c1 $59 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TVL_CALIB_PERFMED | unsigned char | Top view left camera status |
| STAT_TVR_CALIB_PERFMED | unsigned char | Top Right camera status |
| STAT_RV_CALIB_PERFMED | unsigned char | Rear view camera status 0 - Not performed 1 - Performed |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-video-freez-wdt"></a>
### STATUS_VIDEO_FREEZ_WDT

Video freez watchdog status KWP2000: $22 ReadDataByCommonIdentifier $c1 $67 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_COUNT_CH1 | unsigned char | Hex-Antwort von SG |
| STAT_DIVIDER_CH1 | unsigned char | Hex-Antwort von SG |
| STAT_MISSED_STARTS_CH1 | unsigned char | Hex-Antwort von SG |
| STAT_MISSED_ENDS_CH1 | unsigned char | Hex-Antwort von SG |
| STAT_COUNT_CH2 | unsigned char | Hex-Antwort von SG |
| STAT_COUNT_CH3 | unsigned char | Hex-Antwort von SG |
| STAT_OVR_FAULT | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-steuren-signalausgabe"></a>
### START_STEUREN_SIGNALAUSGABE

Start test picture and colour bar with time out KWP2000: $31 RoutineControl $22 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_DATA | binary | 1st BYTE - Signal type 0x01 - Real picture 0x02 - Test picture 0x03 - End output 0x04  to 0x09 - Activate Colour bar 2nd BYTE - output_lsb 0x0 3rd BYTE - output_msb 0x00 or 0x01 4th BYTE - time_out less than 0x1E |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-steuren-signalausgabe"></a>
### STOP_STEUREN_SIGNALAUSGABE

Stop test picture and colour bar KWP2000: $32 RoutineControl $22 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-test-videoausgang"></a>
### START_TEST_VIDEOAUSGANG

Start KWP2000: $31 RoutineControl $23 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-test-videoausgang"></a>
### STOP_TEST_VIDEOAUSGANG

Stop KWP2000: $32 RoutineControl $23 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-test-videoausgang"></a>
### STATUS_TEST_VIDEOAUSGANG

Status KWP2000: $33 RoutineControl $23 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_AUS_MSB | unsigned char | Hex-Antwort von SG |
| STAT_AUSGANG | unsigned char | Hex-Antwort von SG |
| STAT_TST_VIDEOAUSGANG | unsigned char | Hex-Antwort von SG |
| STAT_ANZAHL_FEHLER | unsigned char | Hex-Antwort von SG |
| STAT_FEHLER_1_AUSGANG | unsigned char | Hex-Antwort von SG |
| STAT_FEHLERART_AUSGANG | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-tvr-cam-cal-data"></a>
### SET_TVR_CAM_CAL_DATA

Set TV right camera clibration data KWP2000: $2E ReadDataByCommonIdentifier $c1 $16 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1 byte: fisheyeAmt 2 byte: cxoffs_pix_3rds 3 byte: cyoffs_pix_3rds 4 byte: cam_aspect_offs 5 byte: lsb(hfov_deg_64ths) 6 byte: msb(hfov_deg_64ths) 7 byte: opt_axis_x_offs_pix_3rds 8 byte: opt_axis_y_offs_pix_3rds 9 byte: opt_axis_z_rot_deg_64ths |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-tvl-cam-cal-data"></a>
### SET_TVL_CAM_CAL_DATA

Set TV left camera clibration data KWP2000: $2E ReadDataByCommonIdentifier $c1 $17 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1 byte: fisheyeAmt 2 byte: cxoffs_pix_3rds 3 byte: cyoffs_pix_3rds 4 byte: cam_aspect_offs 5 byte: lsb(hfov_deg_64ths) 6 byte: msb(hfov_deg_64ths) 7 byte: opt_axis_x_offs_pix_3rds 8 byte: opt_axis_y_offs_pix_3rds 9 byte: opt_axis_z_rot_deg_64ths |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-rv-cam-cal-data"></a>
### SET_RV_CAM_CAL_DATA

Set Rear View camera clibration data KWP2000: $2E ReadDataByCommonIdentifier $c1 $18 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1 byte: fisheyeAmt 2 byte: cxoffs_pix_3rds 3 byte: cyoffs_pix_3rds 4 byte: cam_aspect_offs 5 byte: lsb(hfov_deg_64ths) 6 byte: msb(hfov_deg_64ths) 7 byte: opt_axis_x_offs_pix_3rds 8 byte: opt_axis_y_offs_pix_3rds 9 byte: opt_axis_z_rot_deg_64ths |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-tvr-disp-calib"></a>
### SET_TVR_DISP_CALIB

Set TV Right display calibration KWP2000: $2E $C1 $28 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1  byte - lsb(disp_area_rot__x_deg_64ths) 2  byte - msb(disp_area_rot__x_deg_64ths) 3  byte - lsb(disp_area_rot_z1_deg_64ths) 4  byte - msb(disp_area_rot_z1_deg_64ths) 5  byte - lsb(disp_area_rot_z2_deg_64ths) 6  byte - msb(disp_area_rot_z2_deg_64ths) 7  byte - lsb(disp_area_centre_pointx_mm) 8  byte - msb(disp_area_centre_pointx_mm) 9  byte - lsb(disp_area_centre_pointy_mm) 10  byte - msb(disp_area_centre_pointy_mm) 11  byte - lsb(disp_area_centre_pointz_mm) 12  byte - msb(disp_area_centre_pointz_mm) 13 byte - lsb(disp_area_width_mm) 14 byte - msb(disp_area_width_mm) 15 byte - lsb(disp_aspect) 16 byte - msb(disp_aspect) 17 byte - flipx 18 byte - flipy 19 byte - antialias 20 byte - auto_bright |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-tvl-disp-calib"></a>
### SET_TVL_DISP_CALIB

Set TV left display calibration KWP2000: $2E $C1 $29 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1  byte - lsb(disp_area_rot__x_deg_64ths) 2  byte - msb(disp_area_rot__x_deg_64ths) 3  byte - lsb(disp_area_rot_z1_deg_64ths) 4  byte - msb(disp_area_rot_z1_deg_64ths) 5  byte - lsb(disp_area_rot_z2_deg_64ths) 6  byte - msb(disp_area_rot_z2_deg_64ths) 7  byte - lsb(disp_area_centre_pointx_mm) 8  byte - msb(disp_area_centre_pointx_mm) 9  byte - lsb(disp_area_centre_pointy_mm) 10  byte - msb(disp_area_centre_pointy_mm) 11  byte - lsb(disp_area_centre_pointz_mm) 12  byte - msb(disp_area_centre_pointz_mm) 13 byte - lsb(disp_area_width_mm) 14 byte - msb(disp_area_width_mm) 15 byte - lsb(disp_aspect) 16 byte - msb(disp_aspect) 17 byte - flipx 18 byte - flipy 19 byte - antialias 20 byte - auto_bright |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-uv-rear-disp-calib"></a>
### SET_UV_REAR_DISP_CALIB

Set U-view rear display calibration KWP2000: $2E $C1 $2a Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1  byte - lsb(disp_area_rot__x_deg_64ths) 2  byte - msb(disp_area_rot__x_deg_64ths) 3  byte - lsb(disp_area_rot_z1_deg_64ths) 4  byte - msb(disp_area_rot_z1_deg_64ths) 5  byte - lsb(disp_area_rot_z2_deg_64ths) 6  byte - msb(disp_area_rot_z2_deg_64ths) 7  byte - lsb(disp_area_centre_pointx_mm) 8  byte - msb(disp_area_centre_pointx_mm) 9  byte - lsb(disp_area_centre_pointy_mm) 10  byte - msb(disp_area_centre_pointy_mm) 11  byte - lsb(disp_area_centre_pointz_mm) 12  byte - msb(disp_area_centre_pointz_mm) 13 byte - lsb(disp_area_width_mm) 14 byte - msb(disp_area_width_mm) 15 byte - lsb(disp_aspect) 16 byte - msb(disp_aspect) 17 byte - flipx 18 byte - flipy 19 byte - antialias 20 byte - auto_bright |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-fsr-disp-calib"></a>
### SET_FSR_DISP_CALIB

Status Full screen rear display calibration KWP2000: $2E $C1 $2b Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1  byte - lsb(disp_area_rot__x_deg_64ths) 2  byte - msb(disp_area_rot__x_deg_64ths) 3  byte - lsb(disp_area_rot_z1_deg_64ths) 4  byte - msb(disp_area_rot_z1_deg_64ths) 5  byte - lsb(disp_area_rot_z2_deg_64ths) 6  byte - msb(disp_area_rot_z2_deg_64ths) 7  byte - lsb(disp_area_centre_pointx_mm) 8  byte - msb(disp_area_centre_pointx_mm) 9  byte - lsb(disp_area_centre_pointy_mm) 10  byte - msb(disp_area_centre_pointy_mm) 11  byte - lsb(disp_area_centre_pointz_mm) 12  byte - msb(disp_area_centre_pointz_mm) 13 byte - lsb(disp_area_width_mm) 14 byte - msb(disp_area_width_mm) 15 byte - lsb(disp_aspect) 16 byte - msb(disp_aspect) 17 byte - flipx 18 byte - flipy 19 byte - antialias 20 byte - auto_bright |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-bmw-fsr-disp-calib"></a>
### SET_BMW_FSR_DISP_CALIB

Status BMW production calibration Full Screen Rear display calibration KWP2000: $2E $C1 $2c Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1  byte - lsb(disp_area_rot__x_deg_64ths) 2  byte - msb(disp_area_rot__x_deg_64ths) 3  byte - lsb(disp_area_rot_z1_deg_64ths) 4  byte - msb(disp_area_rot_z1_deg_64ths) 5  byte - lsb(disp_area_rot_z2_deg_64ths) 6  byte - msb(disp_area_rot_z2_deg_64ths) 7  byte - lsb(disp_area_centre_pointx_mm) 8  byte - msb(disp_area_centre_pointx_mm) 9  byte - lsb(disp_area_centre_pointy_mm) 10  byte - msb(disp_area_centre_pointy_mm) 11  byte - lsb(disp_area_centre_pointz_mm) 12  byte - msb(disp_area_centre_pointz_mm) 13 byte - lsb(disp_area_width_mm) 14 byte - msb(disp_area_width_mm) 15 byte - lsb(disp_aspect) 16 byte - msb(disp_aspect) 17 byte - flipx 18 byte - flipy 19 byte - antialias 20 byte - auto_bright |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmodu"></a>
### STATUS_ENERGIESPARMODU

Status of energy saving mode KWP2000: $22 ReadDataByCommonIdentifier $10 $0A Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ENERGY_SV_MODE | unsigned char | 0 - DEACTIVATED_MODE 1 - PRODUCTION_MODE 2 - SHIPMENT_MODE 3 - REPAIRSHOP_MODE |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-bus-nachrichten-d392"></a>
### SET_BUS_NACHRICHTEN_D392

Set CAN Signal TV, RV request KWP2000: $2E $D3 $92 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SIG_TV_REQUEST | unsigned char | 0 - OFF 1 - ON |
| SIG_RV_REQUEST | unsigned char | 0 - OFF 1 - ON |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-heizung-rfk"></a>
### STATUS_HEIZUNG_RFK

status of heating element rv cam KWP2000: $22 $D3 $A0 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_RVH | char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-heizung-rfk"></a>
### SET_HEIZUNG_RFK

set of heating element rv cam KWP2000: $2E $D3 $A0 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RVH_REQUEST | char | 0 - Off request 1 - ON request |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-num-sub-bus-members"></a>
### STATUS_NUM_SUB_BUS_MEMBERS

status of Number of SubbusMembers and serial numbers KWP2000: $22 $16 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ID | unsigned char | 0x00 : Number of sub bus members 0x01 : Serial number of Rear view camera 0x02 : Serial number of Top view left camera 0x03 : Serial number of Top view right camera 0x04 : Serial number of Side view left camera 0x05 : Serial number of Side view right camera |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_NUM_SBUS_MUMBERS | unsigned char | Only for ID = 0 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-camera-soiling"></a>
### SET_CAMERA_SOILING

Status of TV,SV,RV camera soiling KWP2000: $2E ReadDataByCommonIdentifier $c1 $30 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_PARMERTERS | binary | 1 byte: tvl_percent_soiling 2 byte: tvr_percent_soiling 3 byte: svl_percent_soiling 4 byte: svr_percent_soiling 5 byte: rv_percent_soiling |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ecu-dsp-performnce"></a>
### STATUS_ECU_DSP_PERFORMNCE

status of ECU DSP processor performance KWP2000: $22 $C1 $32 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cel-serial-num"></a>
### STATUS_CEL_SERIAL_NUM

Read CEL serial number KWP2000: $22 $C1 $33 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CEL_SN_NUMBER | binary | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-cel-serial-num"></a>
### SET_CEL_SERIAL_NUM

Set CEL serial number KWP2000: $2E $C1 $33 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CEL_SN_NUMBER | binary | OKAY |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-test-pt-led"></a>
### STATUS_TEST_PT_LED

Read Test point LED KWP2000: $22 $C1 $38 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_LED | int | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lin-vsync"></a>
### STATUS_LIN_VSYNC

Read Lin Vsync KWP2000: $22 $C1 $40 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_LIN_VSYNC | char | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-lin-vsync"></a>
### SET_LIN_VSYNC

Set Lin Vsync KWP2000: $2E $C1 $40 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LIN_VSYNC | char | lin Vsync |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-bmw-tv-cal-solv-params"></a>
### SET_BMW_TV_CAL_SOLV_PARAMS

Set BMW TV assembly calibration solver parameters KWP2000: $2E $C1 $53 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | CFG_CALIB_SOLVER_PARAMS structure(47 bytes) If no input, then it will write default values |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-bmw-tvl-grid-layout"></a>
### SET_BMW_TVL_GRID_LAYOUT

Set BMW assembly calibration Top view left grid layout KWP2000: $2e ReadDataByCommonIdentifier $c1 $55 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | CFG_CALIB_GRID_DETAILS structure(10 bytes) 1 byte: line_width 1 byte: num_hlines 1 byte: num_vlines 1 byte: detect_split_num_cols 1 byte: detect_split_num_rows 1 byte: left_margin 1 byte: right_margin 1 byte: top_margin 1 byte: bot_margin 1 byte: grid_colour |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-bmw-tvr-grid-layout"></a>
### SET_BMW_TVR_GRID_LAYOUT

Set BMW assembly calibration Top view right grid layout KWP2000: $2e ReadDataByCommonIdentifier $c1 $57 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | CFG_CALIB_GRID_DETAILS structure(10 bytes) 1 byte: line_width 1 byte: num_hlines 1 byte: num_vlines 1 byte: detect_split_num_cols 1 byte: detect_split_num_rows 1 byte: left_margin 1 byte: right_margin 1 byte: top_margin 1 byte: bot_margin 1 byte: grid_colour |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-bmw-fsr-grid-layout"></a>
### SET_BMW_FSR_GRID_LAYOUT

Set BMW assembly calibration Full screen rear grid layout KWP2000: $2e ReadDataByCommonIdentifier $c1 $68 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | CFG_CALIB_GRID_DETAILS structure(10 bytes) 1 byte: line_width 1 byte: num_hlines 1 byte: num_vlines 1 byte: detect_split_num_cols 1 byte: detect_split_num_rows 1 byte: left_margin 1 byte: right_margin 1 byte: top_margin 1 byte: bot_margin 1 byte: grid_colour |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-calibration-performed"></a>
### SET_CALIBRATION_PERFORMED

Set of calibration performed KWP2000: $2E ReadDataByCommonIdentifier $c1 $59 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CALIB_PERFMED | unsigned char | set |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-nvm-cfg-inf"></a>
### STATUS_NVM_CFG_INF

Read NVM CFG information KWP2000: $22 $C1 $5a Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_SIK_VER | char | OKAY |
| STAT_SIR_VER | char | OKAY |
| STAT_SIK_SIZE | int | OKAY |
| STAT_SIR_SIZE | int | OKAY |
| STAT_IPG_FLAGS_LOW | int | OKAY |
| STAT_IPG_FLAGS_HIGH | int | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-crc-cnt-check"></a>
### STATUS_CRC_CNT_CHECK

Read CRC & Alive Counter Check on CAN KWP2000: $22 $C1 $66 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_COUNTER | char | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-crc-cnt-check"></a>
### SET_CRC_CNT_CHECK

SET CRC & Alive Counter Check on CAN KWP2000: $2E $C1 $66 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COUNTER_VAL | char | OKAY |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-tvr-cal-trgt-pos"></a>
### SET_TVR_CAL_TRGT_POS

Set TV right calibration target position KWP2000: $2E $C1 $69 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | default E70M Cam positions 1byte lsb(rot_x_deg_64) 2byte msb(rot_x_deg_64) 3byte lsb(rot_z1_deg_64) 4byte msb(rot_z1_deg_64) 5byte lsb(rot_z2_deg_64) 6byte msb(rot_z2_deg_64) 7byte lsb(point_x_mm) 8byte msb(point_x_mm) 9byte lsb(point_y_mm) 10byte msb(point_y_mm) 11byte lsb(point_z_mm) 12byte msb(point_z_mm) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-tvl-cal-trgt-pos"></a>
### SET_TVL_CAL_TRGT_POS

Set TV left calibration target position KWP2000: $2E $C1 $70 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1byte lsb(rot_x_deg_64) 2byte msb(rot_x_deg_64) 3byte lsb(rot_z1_deg_64) 4byte msb(rot_z1_deg_64) 5byte lsb(rot_z2_deg_64) 6byte msb(rot_z2_deg_64) 7byte lsb(point_x_mm) 8byte msb(point_x_mm) 9byte lsb(point_y_mm) 10byte msb(point_y_mm) 11byte lsb(point_z_mm) 12byte msb(point_z_mm) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-rear-cal-trgt-pos"></a>
### SET_REAR_CAL_TRGT_POS

Set Rear calibration target position KWP2000: $2E $C1 $71 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1byte lsb(rot_x_deg_64) 2byte msb(rot_x_deg_64) 3byte lsb(rot_z1_deg_64) 4byte msb(rot_z1_deg_64) 5byte lsb(rot_z2_deg_64) 6byte msb(rot_z2_deg_64) 7byte lsb(point_x_mm) 8byte msb(point_x_mm) 9byte lsb(point_y_mm) 10byte msb(point_y_mm) 11byte lsb(point_z_mm) 12byte msb(point_z_mm) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cal-err-power"></a>
### STATUS_CAL_ERR_POWER

Read calibration error power KWP2000: $22 $C1 $77 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CAL_ERR_PWR | unsigned char | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-cal-err-power"></a>
### SET_CAL_ERR_POWER

SET calibration error power KWP2000: $2E $C1 $77 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CALIB_ERR_PWR | unsigned char | calib error power |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-bmw-rear-cal-solv-params"></a>
### SET_BMW_REAR_CAL_SOLV_PARAMS

Set BMW Rear assembly calibration solver parameters KWP2000: $2E $C1 $76 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | CFG_CALIB_SOLVER_PARAMS structure(47 bytes) If no input, then it will write default values |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-veh-weel-arch-height"></a>
### STATUS_VEH_WEEL_ARCH_HEIGHT

Read Vehicle wheel arch heights KWP2000: $22 $C1 $78 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_FNT_RIGHT_MM | unsigned int | OKAY |
| STAT_FNT_LEFT_MM | unsigned int | OKAY |
| STAT_REAR_RIGHT_MM | unsigned int | OKAY |
| STAT_REAR_LEFT_MM | unsigned int | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-veh-weel-arch-height"></a>
### SET_VEH_WEEL_ARCH_HEIGHT

Set Vehicle wheel arch heights KWP2000: $2E $C1 $78 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1byte lsb(front_right_mm) 2byte msb(front_right_mm) 3byte lsb(front_left_mm) 4byte msb(front_left_mm) 5byte lsb(rear_right_mm) 6byte msb(rear_right_mm) 7byte lsb(rear_left_mm) 8byte msb(rear_left_mm) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drt-det-veh-spd-thld"></a>
### STATUS_DRT_DET_VEH_SPD_THLD

Read Dirt detection vehicle speed thresholds KWP2000: $22 $C1 $7a Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_LOWER_THLD_KMPH | unsigned char | lower_thresh_kmph |
| STAT_UPPER_THLD_KMPH | unsigned char | upper_thresh_kmph |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-drt-det-veh-spd-thld"></a>
### SET_DRT_DET_VEH_SPD_THLD

Set Dirt detection vehicle speed thresholds KWP2000: $2E $C1 $7a Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1byte lower_thresh_kmph 2byte upper_thresh_kmph |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cam-failed-pxl-prcnt"></a>
### STATUS_CAM_FAILED_PXL_PRCNT

Status of TV,SV,RV Camera failed pixels percentage KWP2000: $22 $c1 $82 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TVL_PRCNT_PIXL_FAIL | unsigned char | Hex-Antwort von SG |
| STAT_TVR_PRCNT_PIXL_FAIL | unsigned char | Hex-Antwort von SG |
| STAT_SVL_PRCNT_PIXL_FAIL | unsigned char | Hex-Antwort von SG |
| STAT_SVR_PRCNT_PIXL_FAIL | unsigned char | Hex-Antwort von SG |
| STAT_RV_PRCNT_PIXL_FAIL | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-cam-failed-pxl-prcnt"></a>
### SET_CAM_FAILED_PXL_PRCNT

Set of TV,SV,RV Camera failed pixels percentage KWP2000: $2E $c1 $82 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_PARMERTERS | binary | 1 byte: tvl_percent_pixelf 2 byte: tvr_percent_pixelf 3 byte: svl_percent_pixelf 4 byte: svr_percent_pixelf 5 byte: rv_percent_pixelf |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fail-pxl-threshld"></a>
### STATUS_FAIL_PXL_THRESHLD

Read Camera failed pixels threshold KWP2000: $22 $C1 $83 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_FAILED_PIXEL_TRSHLD | char | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-fail-pxl-threshld"></a>
### SET_FAIL_PXL_THRESHLD

Set Camera failed pixels threshold KWP2000: $2E $C1 $83 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAIL_PXL_TRSHLD | char | Failed pixel threshold |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-idle-vdieo-op-enable"></a>
### STATUS_IDLE_VDIEO_OP_ENABLE

Read Idle mode video output enable KWP2000: $22 $C1 $84 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_IDL_MODE_VIDEO_OP | char | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-idle-vdieo-op-enable"></a>
### SET_IDLE_VDIEO_OP_ENABLE

Set Idle mode video output enable KWP2000: $2E $C1 $84 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VIDEO_OP_ENABLE | char | 0 - Disable 1 - Enable |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sub-variant-id"></a>
### STATUS_SUB_VARIANT_ID

Read Sub variant ID KWP2000: $22 $C1 $85 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_SUB_VAR_ID | char | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-uv-right-disp-calib"></a>
### STATUS_UV_RIGHT_DISP_CALIB

Status U-View Right display calibration KWP2000: $22 $C1 $86 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_CEN_POINT_XMM | int | Area centre point X mm |
| STAT_CEN_POINT_YMM | int | Area centre point Y mm |
| STAT_CEN_POINT_ZMM | int | Area centre point Z mm |
| STAT_AREA_WIDTH_MM | int | Area width mm |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | unsigned char | 1 flips image in x |
| STAT_FLIP_Y | unsigned char | 1 flips image in y |
| STAT_ANTIALIAS | unsigned char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | unsigned char | not used |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-uv-right-disp-calib"></a>
### SET_UV_RIGHT_DISP_CALIB

Set U-View Right display calibration KWP2000: $2E $C1 $86 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1  byte - lsb(disp_area_rot__x_deg_64ths) 2  byte - msb(disp_area_rot__x_deg_64ths) 3  byte - lsb(disp_area_rot_z1_deg_64ths) 4  byte - msb(disp_area_rot_z1_deg_64ths) 5  byte - lsb(disp_area_rot_z2_deg_64ths) 6  byte - msb(disp_area_rot_z2_deg_64ths) 7  byte - lsb(disp_area_centre_pointx_mm) 8  byte - msb(disp_area_centre_pointx_mm) 9  byte - lsb(disp_area_centre_pointy_mm) 10  byte - msb(disp_area_centre_pointy_mm) 11  byte - lsb(disp_area_centre_pointz_mm) 12  byte - msb(disp_area_centre_pointz_mm) 13 byte - lsb(disp_area_width_mm) 14 byte - msb(disp_area_width_mm) 15 byte - lsb(disp_aspect) 16 byte - msb(disp_aspect) 17 byte - flipx 18 byte - flipy 19 byte - antialias 20 byte - auto_bright |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-uv-left-disp-calib"></a>
### STATUS_UV_LEFT_DISP_CALIB

Status U-View Left display calibration KWP2000: $22 $C1 $87 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_CEN_POINT_XMM | int | Area centre point X mm |
| STAT_CEN_POINT_YMM | int | Area centre point Y mm |
| STAT_CEN_POINT_ZMM | int | Area centre point Z mm |
| STAT_AREA_WIDTH_MM | int | Area width mm |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | unsigned char | 1 flips image in x |
| STAT_FLIP_Y | unsigned char | 1 flips image in y |
| STAT_ANTIALIAS | unsigned char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | unsigned char | not used |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-uv-left-disp-calib"></a>
### SET_UV_LEFT_DISP_CALIB

Set U-View Left display calibration KWP2000: $2E $C1 $87 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1  byte - lsb(disp_area_rot__x_deg_64ths) 2  byte - msb(disp_area_rot__x_deg_64ths) 3  byte - lsb(disp_area_rot_z1_deg_64ths) 4  byte - msb(disp_area_rot_z1_deg_64ths) 5  byte - lsb(disp_area_rot_z2_deg_64ths) 6  byte - msb(disp_area_rot_z2_deg_64ths) 7  byte - lsb(disp_area_centre_pointx_mm) 8  byte - msb(disp_area_centre_pointx_mm) 9  byte - lsb(disp_area_centre_pointy_mm) 10  byte - msb(disp_area_centre_pointy_mm) 11  byte - lsb(disp_area_centre_pointz_mm) 12  byte - msb(disp_area_centre_pointz_mm) 13 byte - lsb(disp_area_width_mm) 14 byte - msb(disp_area_width_mm) 15 byte - lsb(disp_aspect) 16 byte - msb(disp_aspect) 17 byte - flipx 18 byte - flipy 19 byte - antialias 20 byte - auto_bright |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tow-hitch-disp-calib"></a>
### STATUS_TOW_HITCH_DISP_CALIB

Status Tow Hitch display calibration KWP2000: $22 $C1 $88 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_CEN_POINT_XMM | int | Area centre point X mm |
| STAT_CEN_POINT_YMM | int | Area centre point Y mm |
| STAT_CEN_POINT_ZMM | int | Area centre point Z mm |
| STAT_AREA_WIDTH_MM | int | Area width mm |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | unsigned char | 1 flips image in x |
| STAT_FLIP_Y | unsigned char | 1 flips image in y |
| STAT_ANTIALIAS | unsigned char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | unsigned char | not used |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-tow-hitch-disp-calib"></a>
### SET_TOW_HITCH_DISP_CALIB

Set Tow Hitch Left display calibration KWP2000: $2E $C1 $88 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1  byte - lsb(disp_area_rot__x_deg_64ths) 2  byte - msb(disp_area_rot__x_deg_64ths) 3  byte - lsb(disp_area_rot_z1_deg_64ths) 4  byte - msb(disp_area_rot_z1_deg_64ths) 5  byte - lsb(disp_area_rot_z2_deg_64ths) 6  byte - msb(disp_area_rot_z2_deg_64ths) 7  byte - lsb(disp_area_centre_pointx_mm) 8  byte - msb(disp_area_centre_pointx_mm) 9  byte - lsb(disp_area_centre_pointy_mm) 10  byte - msb(disp_area_centre_pointy_mm) 11  byte - lsb(disp_area_centre_pointz_mm) 12  byte - msb(disp_area_centre_pointz_mm) 13 byte - lsb(disp_area_width_mm) 14 byte - msb(disp_area_width_mm) 15 byte - lsb(disp_aspect) 16 byte - msb(disp_aspect) 17 byte - flipx 18 byte - flipy 19 byte - antialias 20 byte - auto_bright |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-frm-rate-reduc-cntrl"></a>
### STATUS_FRM_RATE_REDUC_CNTRL

Read Frame Rate Reduction control KWP2000: $22 $C1 $89 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_FRMRATE_RED_CNTL | char | Status of Frame Rate Reduction control |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-frm-rate-reduc-cntrl"></a>
### SET_FRM_RATE_REDUC_CNTRL

Set Frame Rate Reduction control KWP2000: $2E $C1 $89 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FRAMERATE_REDUCTION | char | Frame Rate Reduction control |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-frmrt-red-mstr-cntrl"></a>
### SET_FRMRT_RED_MSTR_CNTRL

Set Framerate Reduction Masterframe KWP2000: $2E $C1 $90 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FRAMERATE_RED_DATA | binary | 1 byte Frame Rate Reduction TVL 2 byte Frame Rate Reduction TVR 3 byte Frame Rate Reduction SVL 4 byte Frame Rate Reduction SVR 5 byte Frame Rate Reduction RV |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-frmrate-slave-resp"></a>
### STATUS_FRMRATE_SLAVE_RESP

Read Framerate Reduction Slave responses KWP2000: $22 $C1 $91 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ACT_FRMRATE_RED_TVL | char | Active frame rate TVL |
| STAT_DES_FRMRATE_RED_TVL | char | Desired frame rate TVL |
| STAT_ACT_FRMRATE_RED_TVR | char | Active frame rate TVR |
| STAT_DES_FRMRATE_RED_TVR | char | Desired frame rate TVR |
| STAT_ACT_FRMRATE_RED_SVL | char | Active frame rate SVL |
| STAT_DES_FRMRATE_RED_SVL | char | Desired frame rate SVL |
| STAT_ACT_FRMRATE_RED_SVR | char | Active frame rate SVR |
| STAT_DES_FRMRATE_RED_SVR | char | Desired frame rate SVR |
| STAT_ACT_FRMRATE_RED_RV | char | Active frame rate RV |
| STAT_DES_FRMRATE_RED_RV | char | Desired frame rate RV |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-od-trsholds"></a>
### STATUS_OD_TRSHOLDS

Read Object detection thresholds KWP2000: $22 $C1 $96 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TV_NEW_TGT_PK_TRSHD | unsigned int | Status of tv_new_target_peak_thresh |
| STAT_TV_CORR_PK_TRSHD | unsigned int | Status of tv_corr_peak_thresh |
| STAT_TV_NEW_TGT_PCE_TRSHD | unsigned char | Status of tv_new_target_pce_thresh |
| STAT_TV_CORR_PCE_TRSHD | unsigned char | Status of tv_corr_pce_thresh |
| STAT_RV_NEW_TGT_PK_TRSHD | unsigned int | Status of rv_new_target_peak_thresh |
| STAT_RV_CORR_PK_TRSHD | unsigned int | Status of rv_corr_peak_thresh |
| STAT_RV_NEW_TGT_PCE_TRSHD | unsigned char | Status of rv_new_target_pce_thresh |
| STAT_RV_CORR_PCE_TRSHD | unsigned char | Status of rv_corr_pce_thresh |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-od-params"></a>
### STATUS_OD_PARAMS

Read Object detection parameters KWP2000: $22 $C1 $97 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CFG_ODT_PARAM_TYPE | binary | Refer CFG_ODT_PARAM_TYPE struct |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-onl-calib-cntrl"></a>
### STATUS_ONL_CALIB_CNTRL

Read Online calibration control KWP2000: $22 $C1 $98 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CFG_ONL_CONTROL_TYPE | binary | Refer CCFG_ONL_CONTROL_TYPE struct |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-od-trsholds"></a>
### SET_OD_TRSHOLDS

Set Object detection thresholds KWP2000: $2E $C1 $96 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | CFG_ODT_THRESH_TYPE structure(12 bytes) 1 byte: lsb(tv_new_target_peak_thresh) 2 byte: msb(tv_new_target_peak_thresh) 3 byte: lsb(tv_corr_peak_thresh) 4 byte: msb(tv_corr_peak_thresh) 5 byte: tv_new_target_pce_thresh 6 byte: tv_new_target_pce_thresh 7 byte: lsb(rv_new_target_peak_thresh) 8 byte: msb(rv_new_target_peak_thresh) 9 byte: lsb(rv_corr_peak_thresh) 10 byte: msb(rv_corr_peak_thresh) 11 byte: rv_new_target_pce_thresh 12 byte: rv_new_target_pce_thresh |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-od-parms"></a>
### SET_OD_PARMS

Set Object detection parameters KWP2000: $2E $C1 $97 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | CFG_ODT_PARAM_TYPE structure(22 bytes) 1 byte: lsb(min_speed_mm_per_s) 2 byte: msb(min_speed_mm_per_s) 3 byte: lsb(max_speed_mm_per_s) 4 byte: msb(max_speed_mm_per_s) 5 byte: lsb(max_speed_delta_mm_per_s) 6 byte: msb(max_speed_delta_mm_per_s) 7 byte: lsb(max_steer_delta_deg_64ths) 8 byte: msb(max_steer_delta_deg_64ths) 9 byte: lsb(min_track_distance_mm) 10 byte: msb(min_track_distance_mm) 11 byte: rv_num_regions 12 byte: tv_num_regions 13 byte: max_lost_count 14 byte: min_track_count 15 byte: max_track_count 16 byte: num_odt_regions 17 byte: restrict_fil 18 byte: overlay_enabled 19 byte: update_time_constant 20 byte: min_on_ground_percent 21 byte: min_turning_percent 22 byte: turning_angle_threshold_degrees |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-onl-calib-cntrl"></a>
### SET_ONL_CALIB_CNTRL

Set Online calibration control KWP2000: $2E $C1 $98 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | CFG_ONL_CONTROL_TYPE structure(23 bytes) 1 byte: onl_enable 2 byte: pass1 3 byte: pass2 4 byte: height_detect 5 byte: max_solves 6 byte: worst_results_count_less 7 byte: worst_less0_amount 8 byte: worst_less1_amount 9 byte: worst_less2_amount 10 byte: worst_amount1_tenths 11 byte: worst_amount2_tenths 12 byte: compensate_steering_mult 13 byte: compensate_steering_offs 14 byte: compensate_speed_mult 15 byte: weight_mean_pos_to_vert 16 byte: new_height_method 17 byte: speedo_method 18 byte: min_multiplier_128ths 19 byte: max_multiplier_128ths 20 byte: speed_multiplier_100ths 21 byte: max_steer_offs_deg_10ths 22 byte: steer_offset_multiplier 23 byte: steer_multiplier_100ths |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-onl-calib-cntrl-disabled"></a>
### SET_ONL_CALIB_CNTRL_DISABLED

Set Online calibration control to be disabled KWP2000: $2E $C1 $98 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rv-wrap-params"></a>
### STATUS_RV_WRAP_PARAMS

Read Rear view warping parameters KWP2000: $22 $C1 $9b Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CFG_WARP_TYPE | binary | Refer CFG_WARP_TYPE struct(13 bytes) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-rv-wrap-params"></a>
### SET_RV_WRAP_PARAMS

Set Rear view warping parameters KWP2000: $2E $C1 $9B Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | CFG_ODT_PARAM_TYPE structure(13 active bytes) 1 byte: lsb(centre_pos_x_px) 2 byte: msb(centre_pos_x_px) 3 byte: lsb(centre_pos_y_px) 4 byte: msb(centre_pos_y_px) 5 byte: lsb(a) 6 byte: msb(a) 7 byte: lsb(b) 8 byte: msb(b) 9 byte: lsb(c) 10 byte: msb(c) 11 byte: lsb(d) 12 byte: msb(d) 13 byte: control |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-calibration-enable"></a>
### STATUS_CALIBRATION_ENABLE

Read development use only - enable / disable calibration KWP2000: $22 $C1 $9c Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CALIBRATION_ENABLE | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-calibration-enable"></a>
### SET_CALIBRATION_ENABLE

Set development use only - enable / disable calibration KWP2000: $2E $C1 $9c Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CALIB_ENABLE | char | enable / disable calibration |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-top-view-vehicle-pos"></a>
### STATUS_TOP_VIEW_VEHICLE_POS

Status Enable/disable the Top View Vehicle Position KWP2000: $22 $c1 $9d Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TV_VEH_POS | char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-top-view-vehicle-pos"></a>
### SET_TOP_VIEW_VEHICLE_POS

Set Enable/disable the Top View Vehicle Position KWP2000: $2e $c1 $9d Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT | char | 0x0 : OFF 0x1 : ON |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-uv-active-flag"></a>
### STATUS_UV_ACTIVE_FLAG

Status U - View Activation Flag KWP2000: $22 $c1 $9e Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_UV_ACT_FLAG | char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-uv-active-flag"></a>
### SET_UV_ACTIVE_FLAG

Set U - View Activation Flag KWP2000: $2e $c1 $9E Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT | char | 0x0 : OFF 0x1 : ON |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-idlemod-vid-test"></a>
### STATUS_IDLEMOD_VID_TEST

Status Idle mode video test index KWP2000: $22 $c1 $9F Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_IDLEMODE_VD_TEST_INDEX | char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tv-temporal-filt"></a>
### STATUS_TV_TEMPORAL_FILT

Status Topview temporal filtering KWP2000: $22 $c1 $a0 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ENB_BITFIELD | char | Enable temporal filtering |
| STAT_THRESHOLD_Y | char | threshold_y |
| STAT_THRESHOLD_CR | char | threshold_cr |
| STAT_THRESHOLD_CB | char | threshold_cb |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-tv-temporal-filt"></a>
### SET_TV_TEMPORAL_FILT

Set Topview temporal filtering KWP2000: $2e $c1 $a0 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT | binary | 1 byte: enable_bitfield 2 byte: threshold_y 3 byte: threshold_cr 4 byte: threshold_cb |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sv-temporal-filt"></a>
### STATUS_SV_TEMPORAL_FILT

Status Sideview temporal filtering KWP2000: $22 $c1 $a1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ENB_BITFIELD | char | Enable temporal filtering |
| STAT_THRESHOLD_Y | char | threshold_y |
| STAT_THRESHOLD_CR | char | threshold_cr |
| STAT_THRESHOLD_CB | char | threshold_cb |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-sv-temporal-filt"></a>
### SET_SV_TEMPORAL_FILT

Set Sideview temporal filtering KWP2000: $2e $c1 $a1 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT | binary | 1 byte: enable_bitfield 2 byte: threshold_y 3 byte: threshold_cr 4 byte: threshold_cb |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rv-temporal-filt"></a>
### STATUS_RV_TEMPORAL_FILT

Status Rearview temporal filtering KWP2000: $22 $c1 $a2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ENB_BITFIELD | char | Enable temporal filtering |
| STAT_THRESHOLD_Y | char | threshold_y |
| STAT_THRESHOLD_CR | char | threshold_cr |
| STAT_THRESHOLD_CB | char | threshold_cb |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-rv-temporal-filt"></a>
### SET_RV_TEMPORAL_FILT

Set Rearview temporal filtering KWP2000: $2e $c1 $a2 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT | binary | 1 byte: enable_bitfield 2 byte: threshold_y 3 byte: threshold_cr 4 byte: threshold_cb |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-inhibt-onl-cal-res-updt"></a>
### STATUS_INHIBT_ONL_CAL_RES_UPDT

Read Inhibit Online calibration results update KWP2000: $22 $C1 $A4 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ONL_CAL_RES_INHIBT | char | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-inhibt-onl-cal-res-updt"></a>
### SET_INHIBT_ONL_CAL_RES_UPDT

Set Inhibit Online calibration results update KWP2000: $2E $C1 $a4 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INHIBT_ONL_RESLT | char | online_cal_results_inhibit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-service-rv-heater"></a>
### STATUS_SERVICE_RV_HEATER

Read Service Rear View Heater Status KWP2000: $22 $C1 $A5 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_RV_HEATER | char | 1 bit(LS bit) : RVH_STATUS_ON 2 bit 	: RVH_DIAGNOSTICS_MODE 3 bit 	: RVH_STATUS_CAN_TIMEOUT 4 bit 	: RVH_STATUS_CURRENT_FAULT 5 bit 	: RVH_STATUS_LIN_FAULT 6 bit 	: RVH_STATUS_CAM_OVER_TEMP 7 bit 	: RVH_STATUS_DE_ICE 8 bit(MS bit) : RVH_STATUS_DE_MIST |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-service-rv-heater"></a>
### SET_SERVICE_RV_HEATER

Set Service Rear View Heater Status KWP2000: $2E $C1 $a5 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RV_HEATER | char | 0 - OFF 1 - ON |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-onl-cal-dtc-presclrs"></a>
### STATUS_ONL_CAL_DTC_PRESCLRS

Read Online calibration DTC thresholds KWP2000: $22 $C1 $AB Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TVL | char | TVL threshold |
| STAT_TVR | char | TVR threshold |
| STAT_RV | char | RV threshold |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tv-inhibit"></a>
### STATUS_TV_INHIBIT

Read Inhibit TV status KWP2000: $22 $C1 $A3 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TV_INHIBIT | unsigned char | Inhibit TV |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-tv-inhibit"></a>
### SET_TV_INHIBIT

Set Inhibit Top view KWP2000: $2E $C1 $a3 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TV_INHIBIT | char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-onl-cal-record"></a>
### STATUS_ONL_CAL_RECORD

Read the online calibration record data KWP2000: $22 $C1 $AC Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ONL_CAL_RECORD | binary | Refer CFG_IVM_RECORD_TYPE structure |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lin-not-alive"></a>
### STATUS_LIN_NOT_ALIVE

Read LIN not alive status KWP2000: $22 $C1 $AD Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_LIN_NOT_ALIVE | char | LIN not alive status |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bsdf-enable"></a>
### STATUS_BSDF_ENABLE

Read Image quality control parameters KWP2000: $22 $C1 $AE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_IQ_CONTROL_TVL | unsigned char | IQ control top view left camera |
| STAT_IQ_CONTROL_TVR | unsigned char | IQ control top view right camera |
| STAT_IQ_CONTROL_SVL | unsigned char | IQ control side view left camera |
| STAT_IQ_CONTROL_SVR | unsigned char | IQ control side view right camera |
| STAT_IQ_CONTROL_RV | unsigned char | IQ control Rear view camera |
| STAT_IQ_CONTROL_OVL | unsigned char | IQ control overlay enable |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-bsdf-enable"></a>
### SET_BSDF_ENABLE

Set Image quality control parameters KWP2000: $2E $C1 $ae Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BSDF_ENABLE | binary | 1byte: IQ_CONTROL_TVL 2byte: IQ_CONTROL_TVR 3byte: IQ_CONTROL_SVL 4byte: IQ_CONTROL_SVR 5byte: IQ_CONTROL_RV 6byte: IQ_CONTROL_Overlay_en 7byte: Unused 8byte: Unused |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cam-learn"></a>
### STATUS_CAM_LEARN

Read different camera learn status KWP2000: $22 $D3 $A1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_TVL | char | 1 - learned |
| STAT_TVR | char | 1 - learned |
| STAT_SVL | char | 1 - learned |
| STAT_SVR | char | 1 - learned |
| STAT_RV | char | 1 - learned |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-fs-sv-right-cel"></a>
### ENABLE_FS_SV_RIGHT_CEL

Enable Full Screen Side view right KWP2000: $31 RoutineControl $58 $00 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-disable-fs-sv-right-cel"></a>
### DISABLE_FS_SV_RIGHT_CEL

Diaable Full Screen Side view right KWP2000: $32 RoutineControl $58 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-fs-sv-left-cel"></a>
### ENABLE_FS_SV_LEFT_CEL

Enable Full Screen Side view left KWP2000: $31 RoutineControl $59 $00 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-disable-fs-sv-left-cel"></a>
### DISABLE_FS_SV_LEFT_CEL

Diable Full Screen Side view  Left KWP2000: $32 RoutineControl $59 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-bmw-srv-cam-learn"></a>
### START_BMW_SRV_CAM_LEARN

Start BMW Service Camera Learn KWP2000: $31 RoutineControl $5C $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-lin-disable-all"></a>
### START_LIN_DISABLE_ALL

Start LIN disable all schedules KWP2000: $31 RoutineControl $5D $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-lin-disable-all"></a>
### STOP_LIN_DISABLE_ALL

Stop LIN disable all schedules KWP2000: $32 RoutineControl $5D $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-lvds-imager"></a>
### START_LVDS_IMAGER

Start LVDS and Imager state to selectecd input states KWP2000: $31 RoutineControl $5F $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LVDS_STATE | char | camera LVDS state |
| IMAGER_STATE | char | camera Imager state |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-lvds-imager"></a>
### STOP_LVDS_IMAGER

Set LVDS and Imager state to Default state KWP2000: $32 RoutineControl $5F $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-clr-cam-dtc"></a>
### START_CLR_CAM_DTC

Claer camera DTC KWP2000: $31 RoutineControl $60 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_VARIANT | char | camera selected |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-lin-hdr"></a>
### START_LIN_HDR

Enable the HDR functionality KWP2000: $31 RoutineControl $61 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECTED | char | camera selected |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-lin-hdr"></a>
### STOP_LIN_HDR

Disable the HDR functionality KWP2000: $32 RoutineControl $61 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECTED | char | camera selected |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-cam-error-log"></a>
### START_CAM_ERROR_LOG

Read Camera Error Log KWP2000: $31 RoutineControl $62 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECTED | char | 0x01 - TVL camera selected 0x02 - TVR camera selected 0x04 - SVL camera selected 0x08 - SVR camera selected 0x10 - RV  camera selected |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cam-error-log"></a>
### STATUS_CAM_ERROR_LOG

Read results Camera Error Log KWP2000: $33 RoutineControl $62 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECTED | char | camera selected |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_RESPONCE | char | 0 - No response received 1 - No response received |
| STAT_RESPONCE_DATA | binary | response data |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-video-frz-watchdog"></a>
### START_VIDEO_FRZ_WATCHDOG

Start Video freeze watchdog KWP2000: $31 RoutineControl $64 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 16bytes input data |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-video-frz-watchdog"></a>
### STOP_VIDEO_FRZ_WATCHDOG

Stop Video freeze watchdog KWP2000: $32 RoutineControl $64 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-cfg-supplier-defaults"></a>
### START_CFG_SUPPLIER_DEFAULTS

Set the CFG keep and rebuild structs to default values KWP2000: $31 RoutineControl $65 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-caf-default-dids"></a>
### START_CAF_DEFAULT_DIDS

Set all DIDs to defaults from coding file KWP2000: $31 RoutineControl $66 $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-updt-flashmem-cam"></a>
### START_UPDT_FLASHMEM_CAM

Start Trigger Flashmemory Update for cameras KWP2000: $31 RoutineControl $67 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECTED | char | 0x01 - TVL camera selected 0x02 - TVR camera selected 0x04 - SVL camera selected 0x08 - SVR camera selected 0x10 - RV camera selected 0x1F - All cameras selected |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-updt-flash-cam-bl-modes"></a>
### START_UPDT_FLASH_CAM_BL_MODES

Start Trigger Flashmemory Update for cameras from bootloader modes with identical variants KWP2000: $31 RoutineControl $68 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECTED | char | 0x01 - TVL camera selected 0x02 - TVR camera selected 0x04 - SVL camera selected 0x08 - SVR camera selected 0x10 - RV  camera selected 0x1F - All cameras selected |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-cam-adc-readings"></a>
### START_CAM_ADC_READINGS

Read camera ADC readings KWP2000: $31 RoutineControl $5E $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECTED | char | 0x01 - TVL camera selected 0x02 - TVR camera selected 0x04 - SVL camera selected 0x08 - SVR camera selected 0x10 - RV  camera selected 0x1F - All cameras selected |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-cam-adc-readings"></a>
### STOP_CAM_ADC_READINGS

Stop Reading  camera ADC readings KWP2000: $32 RoutineControl $5E $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECTED | char | 0x01 - TVL camera selected 0x02 - TVR camera selected 0x04 - SVL camera selected 0x08 - SVR camera selected 0x10 - RV  camera selected 0x1F - All cameras selected |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-tst-point-leds"></a>
### START_TST_POINT_LEDS

start Test Points & LEDs KWP2000: $31 RoutineControl $4E $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1 byte: host_data_byte 2 byte: dsp_data_byte 3 byte: host_mask_byte 3 byte: DSP_mask_byte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-cam-power"></a>
### START_CAM_POWER

start Camera Power KWP2000: $31 RoutineControl $52 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1 byte: data_byte 2 byte: mask_byte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-cam-power"></a>
### STOP_CAM_POWER

stop Camera Power KWP2000: $32 RoutineControl $52 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1 byte: data_byte 2 byte: mask_byte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-read-cam-reg"></a>
### START_READ_CAM_REG

Read Camera Register KWP2000: $31 RoutineControl $40 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1 byte: camera selected 2 byte: Register address |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-read-cam-reg"></a>
### STATUS_READ_CAM_REG

Stop Read Camera Register KWP2000: $33 RoutineControl $40 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1 byte: camera selected 2 byte: Register address |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-write-cam-reg"></a>
### START_WRITE_CAM_REG

Start write Camera Register KWP2000: $31 RoutineControl $41 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1 byte: camera selected 2 byte: Register address 2 byte: Register data |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-read-cam-data"></a>
### START_READ_CAM_DATA

Start Read Camera Data (EEPROM) KWP2000: $31 RoutineControl $42 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1 byte: camera selected 2 byte: lsb Register address 3 byte: msb Register address 4 byte: data type size |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-read-cam-data"></a>
### STATUS_READ_CAM_DATA

Status Read Camera Data (EEPROM) KWP2000: $33 RoutineControl $42 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1 byte: camera selected 2 byte: lsb Register address 3 byte: msb Register address 4 byte: data type size |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-write-cam-data"></a>
### START_WRITE_CAM_DATA

Status Write Camera Data (EEPROM) KWP2000: $31 RoutineControl $43 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1 byte    : camera selected 2 byte    : lsb Register address 3 byte    : msb Register address 4 byte	  : data type size 5 -12 byte: data(8 bytes) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-calib-bmw-assem"></a>
### START_CALIB_BMW_ASSEM

Calibration  for BMW assembly KWP2000: $31 RoutineControl $4C $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1 byte: Camera selected 2 byte: Calibration active 3 byte: Ttarget type |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-calib-rv-magna-solv-params"></a>
### STATUS_CALIB_RV_MAGNA_SOLV_PARAMS

Calibration Rear view Magna target Solver parameters KWP2000: $22 ReadDataByCommonIdentifier $c1 $A6 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-cal-magna-rear-solv-params"></a>
### SET_CAL_MAGNA_REAR_SOLV_PARAMS

Set Calibration Rear view Magna target Solver parameters KWP2000: $2E $C1 $A6 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | CFG_CALIB_SOLVER_PARAMS structure(48 bytes) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cal-magna-rear-grid-details"></a>
### STATUS_CAL_MAGNA_REAR_GRID_DETAILS

Status of Calibration magna Rear grid details KWP2000: $22 ReadDataByCommonIdentifier $c1 $a9 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_LINE_WIDTH | unsigned char | Hex-Antwort von SG |
| STAT_NUM_H_LINES | unsigned char | Hex-Antwort von SG |
| STAT_NUM_V_LINES | unsigned char | Hex-Antwort von SG |
| STAT_SPLIT_NUM_COLMN | unsigned char | Hex-Antwort von SG |
| STAT_SPLIT_NUM_ROW | unsigned char | Hex-Antwort von SG |
| STAT_LEFT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_RIGHT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_TOP_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_BOTT_MARGIN | unsigned char | Hex-Antwort von SG |
| STAT_GRID_COLOUR | unsigned char | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-cal-magna-rear-grid-details"></a>
### SET_CAL_MAGNA_REAR_GRID_DETAILS

Set Calibration magna Rear grid details KWP2000: $2e ReadDataByCommonIdentifier $c1 $a9 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | CFG_CALIB_GRID_DETAILS structure(10 bytes) 1 byte: line_width 1 byte: num_hlines 1 byte: num_vlines 1 byte: detect_split_num_cols 1 byte: detect_split_num_rows 1 byte: left_margin 1 byte: right_margin 1 byte: top_margin 1 byte: bot_margin 1 byte: grid_colour |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cal-magna-rear-disp"></a>
### STATUS_CAL_MAGNA_REAR_DISP

Status Calibration Magana Rear view display KWP2000: $22 $C1 $a7 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | X-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z1_DEG | int | Z1-orientation of the 'vitual camera' in degrees |
| STAT_ROT_Z2_DEG | int | Z2-orientation of the 'vitual camera' in degrees |
| STAT_CEN_POINT_XMM | int | Area centre point X mm |
| STAT_CEN_POINT_YMM | int | Area centre point Y mm |
| STAT_CEN_POINT_ZMM | int | Area centre point Z mm |
| STAT_AREA_WIDTH_MM | int | Area width mm |
| STAT_DISP_ASPECT | unsigned int | Aspect ratio |
| STAT_FLIP_X | unsigned char | 1 flips image in x |
| STAT_FLIP_Y | unsigned char | 1 flips image in y |
| STAT_ANTIALIAS | unsigned char | Anti-alias algorithm:none == 0, bilinear == 1, bicubic == 2 |
| STAT_AUTOBRIGHT | unsigned char | not used |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-cal-magna-rear-disp"></a>
### SET_CAL_MAGNA_REAR_DISP

Set Calibration Magana Rear view display KWP2000: $2E $C1 $a7 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INP_PARAMETERS | binary | 1  byte - lsb(disp_area_rot__x_deg_64ths) 2  byte - msb(disp_area_rot__x_deg_64ths) 3  byte - lsb(disp_area_rot_z1_deg_64ths) 4  byte - msb(disp_area_rot_z1_deg_64ths) 5  byte - lsb(disp_area_rot_z2_deg_64ths) 6  byte - msb(disp_area_rot_z2_deg_64ths) 7  byte - lsb(disp_area_centre_pointx_mm) 8  byte - msb(disp_area_centre_pointx_mm) 9  byte - lsb(disp_area_centre_pointy_mm) 10  byte - msb(disp_area_centre_pointy_mm) 11  byte - lsb(disp_area_centre_pointz_mm) 12  byte - msb(disp_area_centre_pointz_mm) 13 byte - lsb(disp_area_width_mm) 14 byte - msb(disp_area_width_mm) 15 byte - lsb(disp_aspect) 16 byte - msb(disp_aspect) 17 byte - flipx 18 byte - flipy 19 byte - antialias 20 byte - auto_bright |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cal-magna-rear-grid-pos"></a>
### STATUS_CAL_MAGNA_REAR_GRID_POS

Read Calibration Magna Rear grid positions KWP2000: $22 $C1 $a8 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_ROT_X_DEG | int | Rotation of X in degrees |
| STAT_ROT_Z1_DEG | int | Rotation of z1 in degrees |
| STAT_ROT_Z2_DEG | int | Rotation of z2 in degrees |
| STAT_X_MM | int | X in mm |
| STAT_Y_MM | int | Y in mm |
| STAT_Z_MM | int | Z in mm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-cal-magna-rear-grid-pos"></a>
### SET_CAL_MAGNA_REAR_GRID_POS

Set Calibration Magna Rear grid positions KWP2000: $2E $C1 $A8 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GRID_POS_DATA | binary | 1byte lsb(rot_x_deg_64) 2byte msb(rot_x_deg_64) 3byte lsb(rot_z1_deg_64) 4byte msb(rot_z1_deg_64) 5byte lsb(rot_z2_deg_64) 6byte msb(rot_z2_deg_64) 7byte lsb(point_x_mm) 8byte msb(point_x_mm) 9byte lsb(point_y_mm) 10byte msb(point_y_mm) 11byte lsb(point_z_mm) 12byte msb(point_z_mm) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-dtc-stat"></a>
### READ_DTC_STAT

Read DTC status KWP2000: $17 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DTC_ERROR_CODE | int | error code |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| DTC_STAT | char | 1 byte |
| DTC_STAT_STRING | string | 1 byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-user-brightness"></a>
### STATUS_USER_BRIGHTNESS

Status of current user brightness(PIA) KWP2000: $22 $C1 $44 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_BRIGHTNESS_TV | unsigned char | Top view brightness |
| STAT_BRIGHTNESS_SV | unsigned char | Side view brightness |
| STAT_BRIGHTNESS_RV | unsigned char | Rear view brightness |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-user-brightness"></a>
### SET_USER_BRIGHTNESS

Set the current user brightness(PIA) KWP2000: $2E $c1 $44 Modus  : Default Set default 0x"D for all cameras 1st byte : Top View brightness 2nd byte : Side View brightness 3rd byte : Rear View brightness

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-user-contrast"></a>
### STATUS_USER_CONTRAST

Status of current user contrast(PIA) KWP2000: $22 $C1 $45 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CONTRAST_TV | unsigned char | Top view contrast |
| STAT_CONTRAST_SV | unsigned char | Side view contrast |
| STAT_CONTRAST_RV | unsigned char | Rear view contrast |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-user-contrast"></a>
### SET_USER_CONTRAST

Set the current user contrast(PIA) KWP2000: $2E $c1 $45 Modus  : Default Default set to 0x4B for all cameras 1st byte : Top View contrast 2nd byte : Side View contrast 3rd byte : Rear View contrast

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-user-overlays"></a>
### STATUS_USER_OVERLAYS

Status of current user overlays enable(PIA) KWP2000: $22 $C1 $65 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_OVERLAYS_TV | unsigned char | Top view overlay |
| STAT_OVERLAYS_SV | unsigned char | Side view overlay |
| STAT_OVERLAYS_RV | unsigned char | Rear view overlay |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-user-overlays"></a>
### SET_USER_OVERLAYS

Set the current user overlays enable(PIA) KWP2000: $2E $c1 $65 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT_DATA | binary | 1st byte : Top View Overlay 2nd byte : Side View Overlay 3rd byte : Rear View Overlay |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuren-kalib-reset"></a>
### STEUREN_KALIB_RESET

Reset the calibration data of the selected camera KWP2000: $2E $D3 $8E Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SLECTED | unsigned char | 0x0 : Top view left camera(DEFAULT) 0x1 : Top view right camera 0x2 : Rear view camera |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rv-cam-heating-enable"></a>
### STATUS_RV_CAM_HEATING_ENABLE

Read statu sof Rear view camera heating enable KWP2000: $22 $C1 $AF Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_RV_HEATING_ENABLE | char | 0 : disable 1 : enable |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-rv-cam-heating-enable"></a>
### SET_RV_CAM_HEATING_ENABLE

Set Rear view camera heating enable KWP2000: $2E $C1 $AF Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RV_HEATING_ENABLE | char | 0x0 : Disable 0x1 : Enable |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-updt-flashmem-cam"></a>
### STATUS_UPDT_FLASHMEM_CAM

Status Trigger Flashmemory Update for cameras KWP2000: $33 RoutineControl $67 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECTED | char | 0x01 - TVL camera selected 0x02 - TVR camera selected 0x04 - SVL camera selected 0x08 - SVR camera selected 0x10 - RV  camera selected 0x1F - All cameras selected |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TVL_CAM | unsigned char | status of Top view left camera |
| STAT_TVR_CAM | unsigned char | status of Top view right camera |
| STAT_SVL_CAM | unsigned char | status of Side view left camera |
| STAT_SVR_CAM | unsigned char | status of Side view right camera |
| STAT_RV_CAM | unsigned char | status of Rear view camera |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-updt-flash-cam-bl-modes"></a>
### STATUS_UPDT_FLASH_CAM_BL_MODES

Status Trigger Flashmemory Update for cameras from bootloader modes with identical variants KWP2000: $33 RoutineControl $68 $00 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECTED | char | 0x01 - TVL camera selected 0x02 - TVR camera selected 0x04 - SVL camera selected 0x08 - SVR camera selected 0x10 - RV  camera selected 0x1F - All cameras selected |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TVL_CAM | unsigned char | status of Top view left camera |
| STAT_TVR_CAM | unsigned char | status of Top view right camera |
| STAT_SVL_CAM | unsigned char | status of Side view left camera |
| STAT_SVR_CAM | unsigned char | status of Side view right camera |
| STAT_RV_CAM | unsigned char | status of Rear view camera |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-reset-calibration-values"></a>
### RESET_CALIBRATION_VALUES

Reset calibration values d38e, CCQ, onl cal record KWP2000: $2E D3 8E $2E C1 A8 $2E C1 Cx Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAM_SELECTED | unsigned char | 0x00: TVL camera 0x01: TVR camera 0x02: RV camera |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-calibration-debug-overlays"></a>
### SET_CALIBRATION_DEBUG_OVERLAYS

Set development use only - enable / disable calibration overalys KWP2000: $2E $C1 $DB Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OVRLY_ENABLE | char | 1 - Enable  calibration debug overlay 0 - Disable calibration debug overlay |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-onl-calib"></a>
### STATUS_ONL_CALIB

Status of online calibration quality KWP2000: $22 $D3 $CC Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_RV | unsigned char | RV CCQ |
| STAT_TVL | unsigned char | TVL CCQ |
| STAT_TVR | unsigned char | TVR CCQ |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-onl-calib-quality"></a>
### STATUS_ONL_CALIB_QUALITY

Status of online calibration quality KWP2000: $22 $D3 $CE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |
| STAT_CCQ_RV | unsigned char | RV CCQ |
| STAT_CCQ_TVL | unsigned char | TVL CCQ |
| STAT_CCQ_TVR | unsigned char | TVR CCQ |
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
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (79 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (73 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)

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
| 1 | BMW-FAST |
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 79 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xAB71 | Energiesparmode aktiv |
| 0xAB85 | Uebertemperatur TV_R CAM |
| 0xAB84 | Uebertemperatur TV_L CAM |
| 0xAB87 | Uebertemperatur SV_R CAM |
| 0xAB86 | Uebertemperatur SV_L CAM |
| 0xAB88 | Uebertemperatur RV CAM |
| 0xAB97 | Top View rechts Kamera verschmutzt |
| 0xAB98 | Top View links Kamera verschmutzt |
| 0xAB9C | TV_R Kamera nicht angelernt |
| 0xAB9D | TV_L Kamera nicht angelernt |
| 0xAB99 | Side View rechts Kamera verschmutzt |
| 0xAB9A | Side View links Kamera verschmutzt |
| 0xAB7A | Sensor Pixel Fehler, TV_r |
| 0xAB7B | Sensor Pixel Fehler, TV_l |
| 0xAB7C | Sensor Pixel Fehler, SV_r |
| 0xAB7D | Sensor Pixel Fehler, SV_l |
| 0xAB7E | Sensor Pixel Fehler RV |
| 0xAB9B | Rear View Kamera verschmutzt |
| 0xAB72 | Nicht justierte TV_r |
| 0xAB73 | Nicht justierte TV_l |
| 0xAB74 | Nicht justierte RV Cam |
| 0xAB7F | Strom Fehler,TV_r |
| 0xAB80 | Strom Fehler,TV_l |
| 0xAB81 | Strom Fehler,SV_r |
| 0xAB82 | Strom Fehler,SV_l |
| 0xAB83 | Strom Fehler,RV |
| 0xCA94 | Lin-Bus Fehler, TV_r |
| 0xCA95 | Lin-Bus Fehler, TV_L |
| 0xCA96 | Lin-Bus Fehler, SV_r |
| 0xCA97 | Lin-Bus Fehler, SV_l |
| 0xCA98 | Lin-Bus Fehler, RV |
| 0xAB75 | LVDS- Uebertragung TV_r |
| 0xAB76 | LVDS- Uebertragung TV_l |
| 0xAB77 | LVDS- Uebertragung SV_r |
| 0xAB78 | LVDS- Uebertragung SV_l |
| 0xAB79 | LVDS- Uebertragung RV |
| 0xAB92 | Kamera Fehler, TV_R |
| 0xAB93 | Kamera Fehler, TV_L |
| 0xAB94 | Kamera Fehler, SV_R |
| 0xAB95 | Kamera Fehler, SV_L |
| 0xAB96 | Kamera Fehler, RV |
| 0xCAAD | K-Can ID 3B0h Status Gang Rueckwaerts |
| 0xCAAA | K-Can ID 306h Fahrzeugneigung  |
| 0xCAA0 | K-CAN ID C4h (Lenkwinkel K-CAN )  |
| 0xCAA9 | K-CAN ID 3B4h Bordnetz Spannungswert |
| 0xCAAB | K-CAN ID 3AFh Status Aktivierung Funktion Parken |
| 0xCA9D | K-CAN ID 3A0h (Fahrzeugzustand)  |
| 0xCA9F | K-CAN ID 387h (Bedienung Taster SideView) |
| 0xCAAC | K-CAN ID 377h Status Funktion PDC |
| 0xCAA7 | K-CAN ID 36Dh Abstandsmessung PDC |
| 0xCA9B | K-CAN ID 330h (Kilometerstand/Reichweite) |
| 0xCAA3 | K-CAN ID 314h (Status Fahrlicht)  |
| 0xCAA4 | K-CAN ID 304h (Status Gang) |
| 0xCAA6 | K-CAN ID 2FCh (ZV und Klappenzustand) |
| 0xCAA2 | K-CAN ID 2E4h (Status Anhaenger) |
| 0xCAA8 | K-CAN ID 2CAh Aussentemperatur |
| 0xCA9E | K-CAN ID 21Ah (Lampenzustand) |
| 0xCAA5 | K-CAN ID 1A6h (Wegstrecke Fahrzeug) |
| 0xCA9C | K-CAN ID 1A0h (Geschwindigkeit Fahrzeug) |
| 0xCAA1 | K-CAN ID 130h (Klemmen) |
| 0xCA9A | K-CAN ID  328h (Relativzeit) |
| 0xAB89 | TV_R nicht kalibriert |
| 0xAB8A | TV_L nicht kalibriert |
| 0xAB8B | RV nicht kalibriert |
| 0xAB70 | Heizung Rueckfahrkamera |
| 0xAB68 | FBAS-Ausgang Kurzschluss oder offene Leitung |
| 0xAB69 | ECU Spannungsversorgung fehlerhaft |
| 0xAB8E | ECU: Flash Module DSP  passen nicht zusammen |
| 0xAB8C | ECU: DSP SDRAM Defekt |
| 0xAB8D | ECU: DSP Programmierfehler |
| 0xAB90 | ECU Interner Spannung Fehler |
| 0xAB91 | ECU Host Ram Defekt |
| 0xAB8F | ECU  Uebertemperatur |
| 0xCA84 | CAN-Bus Leitungsfehler |
| 0xCA87 | CAN-Bus Kommunikationsfehler |
| 0xAB9E | SV_R Kamera nicht angelernt |
| 0xAB9F | SV_L Kamera nicht angelernt |
| 0xABA0 | RV Kamera nicht angelernt |
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
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 73 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xAB71 | 1 | 2 | 3 | - |
| 0xAB72 | 1 | 2 | 3 | - |
| 0xAB73 | 1 | 2 | 3 | - |
| 0xAB74 | 1 | 2 | 3 | - |
| 0xAB75 | 1 | 2 | 3 | - |
| 0xAB76 | 1 | 2 | 3 | - |
| 0xAB77 | 1 | 2 | 3 | - |
| 0xAB78 | 1 | 2 | 3 | - |
| 0xAB79 | 1 | 2 | 3 | - |
| 0xAB7A | 1 | 2 | 3 | - |
| 0xAB7B | 1 | 2 | 3 | - |
| 0xAB7C | 1 | 2 | 3 | - |
| 0xAB7D | 1 | 2 | 3 | - |
| 0xAB7E | 1 | 2 | 3 | - |
| 0xAB7F | 1 | 2 | 3 | - |
| 0xAB80 | 1 | 2 | 3 | - |
| 0xAB81 | 1 | 2 | 3 | - |
| 0xAB82 | 1 | 2 | 3 | - |
| 0xAB83 | 1 | 2 | 3 | - |
| 0xAB84 | 1 | 2 | 3 | - |
| 0xAB85 | 1 | 2 | 3 | - |
| 0xAB86 | 1 | 2 | 3 | - |
| 0xAB87 | 1 | 2 | 3 | - |
| 0xAB88 | 1 | 2 | 3 | - |
| 0xAB89 | 1 | 2 | 3 | - |
| 0xAB8A | 1 | 2 | 3 | - |
| 0xAB8B | 1 | 2 | 3 | - |
| 0xAB69 | 1 | 2 | 3 | - |
| 0xAB8C | 1 | 2 | 3 | - |
| 0xAB8D | 1 | 2 | 3 | - |
| 0xAB8E | 1 | 2 | 3 | - |
| 0xAB8F | 1 | 2 | 3 | - |
| 0xAB90 | 1 | 2 | 3 | - |
| 0xAB91 | 1 | 2 | 3 | - |
| 0xAB92 | 1 | 2 | 3 | - |
| 0xAB93 | 1 | 2 | 3 | - |
| 0xAB94 | 1 | 2 | 3 | - |
| 0xAB95 | 1 | 2 | 3 | - |
| 0xAB96 | 1 | 2 | 3 | - |
| 0xAB68 | 1 | 2 | 3 | - |
| 0xAB97 | 1 | 2 | 3 | - |
| 0xAB98 | 1 | 2 | 3 | - |
| 0xAB99 | 1 | 2 | 3 | - |
| 0xAB9A | 1 | 2 | 3 | - |
| 0xAB9B | 1 | 2 | 3 | - |
| 0xAB70 | 1 | 2 | 3 | - |
| 0xCA84 | 1 | 2 | 3 | - |
| 0xCA87 | 1 | 2 | 3 | - |
| 0xCA94 | 1 | 2 | 3 | - |
| 0xCA95 | 1 | 2 | 3 | - |
| 0xCA96 | 1 | 2 | 3 | - |
| 0xCA97 | 1 | 2 | 3 | - |
| 0xCA98 | 1 | 2 | 3 | - |
| 0xCA9A | 1 | 2 | 3 | - |
| 0xCA9B | 1 | 2 | 3 | - |
| 0xCA9C | 1 | 2 | 3 | - |
| 0xCA9D | 1 | 2 | 3 | - |
| 0xCA9E | 1 | 2 | 3 | - |
| 0xCA9F | 1 | 2 | 3 | - |
| 0xCAA0 | 1 | 2 | 3 | - |
| 0xCAA1 | 1 | 2 | 3 | - |
| 0xCAA2 | 1 | 2 | 3 | - |
| 0xCAA3 | 1 | 2 | 3 | - |
| 0xCAA4 | 1 | 2 | 3 | - |
| 0xCAA5 | 1 | 2 | 3 | - |
| 0xCAA6 | 1 | 2 | 3 | - |
| 0xCAA7 | 1 | 2 | 3 | - |
| 0xCAA8 | 1 | 2 | 3 | - |
| 0xCAA9 | 1 | 2 | 3 | - |
| 0xCAAA | 1 | 2 | 3 | - |
| 0xCAAB | 1 | 2 | 3 | - |
| 0xCAAC | 1 | 2 | 3 | - |
| 0xCAAD | 1 | 2 | 3 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Ubatt | Volts | - | unsigned char | - | 50 | 1000 | 8 |
| 2 | Temperature | Degrees Celcius | - | signed char | - | 1 | 1 | 0 |
| 3 | Additional Infomation | hex | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | ja |
| F_PCODE | ja |
| F_PCODE7 | ja |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 2 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | kein Betriebsmode gesetzt | kein Betriebsmode |
| 0xFF | ungültiger Betriebsmode | ungültig |
