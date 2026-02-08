# 01MRZFE.prg

- Jobs: [94](#jobs)
- Tables: [30](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MRZFEH |
| ORIGIN | Bertrandt UX-EE-2 Goetz |
| REVISION | 1.000 |
| AUTHOR | BMW_AG UX-EE-1 Stoffregen, ESG UX-EE-1 Sergl, BMW_AG UX-EE-1 Kr |
| COMMENT | SGBD nur zum Programmieren der ZFEB und ZFEH |
| PACKAGE | 1.71 |
| SPRACHE | deutsch |

## Jobs

### Index

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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
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
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F0A Fahrzeugauftrag Modus  : Default
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F7F Fahrzeugauftrag Modus  : Default
- [C_FA_SCHREIBEN](#job-c-fa-schreiben) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F0A Fahrzeugauftrag Modus  : Default
- [STATUS_CODIERUNG](#job-status-codierung) - Lesen der Konfigurationsparameter der ZFE KWP2000:      $22 ReadDataByCommonIdentifier $300F DataGroup CodingDone (EEPROM) Modus:        Default
- [STATUS_KONFIGURATION](#job-status-konfiguration) - Lesen der Konfigurationsparameter der ZFE KWP2000:      $22 ReadDataByCommonIdentifier $300B (C07) bzw. $300A (C08) DataGroup Configuration Parameter (EEPROM) Modus:        Default
- [STATUS_DIGITAL](#job-status-digital) - Lesen digitaler Stati der Ausgaenge ZFE KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Only Digital Output Signals (siehe ControlState.xls) $01 ReportCurrentState Modus:        Default
- [STATUS_ANALOG_AUSGANG](#job-status-analog-ausgang) - Lesen der PWM Ausgaenge ZFE und der Geschwindigkeit KWP2000:      $30 InputOutputControlByLocalIdentifier $04 Only Analog Output Signals (siehe ControlState.xls) $01 ReportCurrentState Modus:        Default
- [STATUS_ANALOG_EINGANG](#job-status-analog-eingang) - Lesen analoger Eingaenge der ZFE KWP2000:      $30 InputOutputControlByLocalIdentifier $03 Analog Input Signals (siehe ControlState.xls) $01 ReportCurrentState KWP2000:      $22 ReadDataByCommonIdentifier $300B DataGroup Configuration Parameter (EEPROM) Modus:        Default
- [STATUS_SCHALTER](#job-status-schalter) - Lesen der Stati der Eingaenge der ZFE KWP2000:      $30 InputOutputControlByLocalIdentifier $01 Digital Inputs (siehe ControlState.xls) $01 ReportCurrentState Modus:        Default
- [STATUS_ESA](#job-status-esa) - Lesen der aktuellen ESA-Position KWP2000:      $30 InputOutputByLocalIdentifier $06 ESA $01 ReportCurrentState Modus:        Default
- [STATUS_WINDSCHILD](#job-status-windschild) - Status des Windschilds KWP2000:      $30 InputOutputByLocalId $05 Windshield $01 Status Modus:        Default
- [STEUERN_VORBEREITEN](#job-steuern-vorbereiten) - Kontrolle von ZFE an Diagnosesystem uebergeben KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Outputs (siehe ControlState.xls) $05 FreezeCurrentState $04 Analog Outputs (siehe ControlState.xls) Modus:        Default
- [STEUERN_ABBLENDLICHT](#job-steuern-abblendlicht) - Abblendlicht direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $03 c_KL56b1_soft $0A c_KL56b2_soft Modus:        Default
- [STEUERN_FERNLICHT](#job-steuern-fernlicht) - Fernlicht direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $04 c_KL56a Modus:        Default
- [STEUERN_STANDLICHT](#job-steuern-standlicht) - Standlicht direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $06 c_KL58_front_soft Modus:        Default
- [STEUERN_KENNZEICHENLEUCHTE](#job-steuern-kennzeichenleuchte) - Kennzeichenleuchte direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $10 c_licence_plate Modus:        Default
- [STEUERN_BREMSLICHT](#job-steuern-bremslicht) - Bremslicht direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $04 Analog Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $00 c_KL54 Modus:        Default
- [STEUERN_RUECKLICHT](#job-steuern-ruecklicht) - Ruecklicht/Zusatzscheinwerfer K7x_MUE direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $04 Analog Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $01 c_KL58_rear Modus:        Default
- [STEUERN_BLINKER_LINKS](#job-steuern-blinker-links) - Linken Blinker direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $0E c_KLbl Modus:        Default
- [STEUERN_BLINKER_RECHTS](#job-steuern-blinker-rechts) - Rechten Blinker direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $0D c_KLbr Modus:        Default
- [STEUERN_GRIFFHEIZUNG](#job-steuern-griffheizung) - Griffheizung ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $07 c_handlerheat Modus:        Default
- [STEUERN_SITZHEIZUNG_FAHRER](#job-steuern-sitzheizung-fahrer) - Sitzheizung Fahrer ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $09 seat_heating_drv Modus:        Default
- [STEUERN_SITZHEIZUNG_SOZIUS](#job-steuern-sitzheizung-sozius) - Sitzheizung Sozius ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $08 seat_heating_pas Modus:        Default
- [STEUERN_HUPE](#job-steuern-hupe) - Hupe direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $05 horn Modus:        Default
- [STEUERN_BEENDEN](#job-steuern-beenden) - Kontrolle an ZFE zurueckgeben KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Outputs (siehe ControlState.xls) $00 ReturnControlToEcu $04 Analog Outputs (siehe ControlState.xls) Modus:        Default
- [STEUERN_ESA](#job-steuern-esa) - ESA ansteuern KWP2000:      $30 InputOutputControlByLocalIdentifier $06 ESA $07 ShortTermAdjustment $XX $YY ESA Parameter Modus:        Default
- [STEUERN_WINDSCHILD](#job-steuern-windschild) - Windschild ansteuern KWP2000:      $30 InputOutputControlByLocalIdentifier $05 Windshield $07 ShortTermAdjustment $XX Windshield Parameter Modus:        Default
- [STEUERN_START_ESA_KALIBRIERUNG](#job-steuern-start-esa-kalibrierung) - Start der ESA-Kalibrierung KWP2000:      $31 StartRoutineByLocalId $22 ESA $01 Rear ESA: Start Reference Run in SO Postion $04 Rear ESA: Start Reference Run in every Postion $05 Front ESA: Start Reference Run in SO Postion $08 Front ESA: Start Reference Run in every Postion $09 Both ESA: Start Reference Run in SO Postion $0C Both ESA: Start Reference Run in every Postion Modus:        Default
- [STEUERN_START_KALIBRIERUNG_FOLIENGEBER](#job-steuern-start-kalibrierung-foliengeber) - Start der Kalibrierung des Foliengebers KWP2000:      $31 StartRoutineByLocalId $20 Thermocouples $01 Start Calibration Modus:        Default
- [STEUERN_START_KALIBRIERUNG_WINDSCHILD](#job-steuern-start-kalibrierung-windschild) - Start der Kalibrierung des Windschildes KWP2000:      $31 StartRoutineByLocalId $21 Windshield $01 Start Reference Run Modus:        Default
- [STEUERN_BBVA_INIT](#job-steuern-bbva-init) - Initialisieren der Bremsbelagsverschleißanzeige Mit diesem Job kann die Bremsbelagsverschleißanzeige nach dem Verbauen neuer Bremsbeläge neu initialisiert werden KWP2000:      $31 StartRoutineByLocalId $23 Brake Pad $01 Reset BrakePadWornOutFront or $02 Reset BrakePadWornOutRear or $03 Reset BrakePadWornOutFront & BrakePadWornOutRear Modus:        Default
- [STATUS_KALIBRIERUNG_ESA](#job-status-kalibrierung-esa) - Auslesen Status Kalibrierung ESA KWP2000:      $31 StartRoutineByLocalId $22 ESA $03 Status Reference Run Modus:        Default
- [STATUS_KALIBRIERUNG_FOLIENGEBER](#job-status-kalibrierung-foliengeber) - Status Kalibrierung des Foliengebers KWP2000:      $31 StartRoutineByLocalId $20 Thermocouples $03 Status Calibration Modus:        Default
- [STATUS_KALIBRIERUNG_WINDSCHILD](#job-status-kalibrierung-windschild) - Status Kalibrierung Windschild KWP2000:      $31 StartRoutineByLocalId $21 Windshield $03 Status of Reference Run Modus:        Default
- [STATUS_BBVA](#job-status-bbva) - Auslesen Status Bremsbelagsverschleißanzeige KWP2000:      $31 StartRoutineByLocalId $23 Brake Pad $04 Ask for status of BrakePadWear Modus:        Default
- [STATUS_WS_KALIBRIERSTROM](#job-status-ws-kalibrierstrom) - Kalibrierstrom Windschild KWP2000:      $23 ReadMemoryByAddress $03 $AC Adresse $03 NVRAM $02 Länge 2 Byte Modus:        Default
- [STATUS_SG_VARIANTE](#job-status-sg-variante) - Status Bestueckungsvariante der ZFEB Damit wird die (Bestueckungs-)Variante der ZFE(High Full Version, no ESA, ESA only,  Low,  Basic Low,Mid,High) zurueckgegeben KWP2000: $1A Ident $80 Ident  $23 ReadMemoryByAddress $00 High Byte $03 Mid Byte $8E Low Byte for ZFEBasic $E8 Low Byte for ZFEHigh
- [STATUS_ESA_HALL_POSITION](#job-status-esa-hall-position) - Lesen der aktuellen ESA-Hall-Position KWP2000:      $31 StartRoutineByLocalIdentifier $24 ESA Hall $01 Report max number of pulses rear, $02 Report acutal position rear $03 Number of pulses front, $03 Actual position front Modus:        Default
- [STATUS_SPEED_SENSOR_DF11I](#job-status-speed-sensor-df11i) - Status Information (Zusatzinfo) beim DF11i KWP2000:      $30 InputOutputByLocalId $07 Speed Sensor DF11i Modus:        Default
- [STEUERN_EMERGENCY_SOFTWARE](#job-steuern-emergency-software) - Starten/Beenden der Emergency Software KWP2000:      $31 StartRoutineByLocalId $25 Emergency Software $01 Enable Emergency Software $02 Disable Emergency Software Modus:        Default
- [_STATUS_FOLIENGEBER](#job-status-foliengeber) - Lesen analoger Eingaenge der ZFE KWP2000:      $30 InputOutputControlByLocalIdentifier $03 Analog Input Signals (siehe ControlState.xls) $01 ReportCurrentState KWP2000:      $22 ReadDataByCommonIdentifier $300B DataGroup Configuration Parameter (EEPROM) KWP2000:      $30 InputOutputControlByLocalIdentifier $04 Only Analog Output Signals (siehe ControlState.xls) $01 ReportCurrentState KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Only Digital Output Signals (siehe ControlState.xls) $01 ReportCurrentState Modus:        Default
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [FLASH_PARAMETER_LESEN](#job-flash-parameter-lesen) - Gibt die SG-spezifischen Flash-Parameter zurück
- [FLASH_PARAMETER_SETZEN](#job-flash-parameter-setzen) - Setzt die SG-spezifischen Flash-Parameter
- [INTERFACETYPE](#job-interfacetype) - Interface-Typ bestimmen und ausgeben Es wird der Name des Interfaces übergeben Wichtig für Baudratenumschaltung weil bei ADS, EADS und OBD sind nur 115200 Baud möglich, bei EDIC nur 125000 Baud möglich
- [NG_AUTHENTISIERUNG_START](#job-ng-authentisierung-start) - Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default
- [NG_FLASH_LOESCHEN](#job-ng-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [NG_SIGNATUR_PRUEFEN](#job-ng-signatur-pruefen) - Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default

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

<a id="job-status-codierung"></a>
### STATUS_CODIERUNG

Lesen der Konfigurationsparameter der ZFE KWP2000:      $22 ReadDataByCommonIdentifier $300F DataGroup CodingDone (EEPROM) Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CODIERUNG_WERT | unsigned char | 255   .. Codierdaten wurden nicht übernommen -&gt; Defaultdaten aus ROM werden herangezogen 0-254 .. Codierdaten wurden übernommen |
| STAT_CODIERUNG_TEXT | string | Text zum Ausgabewert |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-konfiguration"></a>
### STATUS_KONFIGURATION

Lesen der Konfigurationsparameter der ZFE KWP2000:      $22 ReadDataByCommonIdentifier $300B (C07) bzw. $300A (C08) DataGroup Configuration Parameter (EEPROM) Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_C_ABS | int | 0.. mit ABS 1.. ohne ABS Basic&High |
| STAT_C_REAR_BULB_SUBSTITUTION | int | 0.. nicht aktiv 1.. aktiv Basic&High |
| STAT_C_THERMOCOUPLES_FLS | int | 0.. Hebelgeber (Potentiometer) 1.. Foliengeber (Thermocouples) Basic&High |
| STAT_C_LICENSE_PLATE_BULB | int | 0.. mit Kennzeichenleuchte, von Software nicht ausgewertet 1.. ohne Kennzeichenleuchte, von Software nicht ausgewertet nur High C07, wird aber nicht von der Software benutzt |
| STAT_C_HANDLERHEAT_PRESENT | int | 0.. mit Griffheizung 1.. ohne Griffheizung Basic&High |
| STAT_C_KL56B1_OFF_56A_ON | int | 0.. aktiv 1.. nicht aktiv Basic&High |
| STAT_C_KL56B2_OFF_56A_ON | int | 0.. aktiv 1.. nicht aktiv nur High |
| STAT_C_NTC_TEMP_SENSOR_PRESENT | int | 0.. aktiv 1.. nicht aktiv Basic&High |
| STAT_C_SEAT_HEAT_DRV_PRESENT | int | 0.. aktiv 1.. nicht aktiv nur High |
| STAT_C_SEAT_HEAT_PAS_PRESENT | int | 0.. aktiv 1.. nicht aktiv nur High |
| STAT_C_ESA_ZSVO_PRESENT | int | 0.. aktiv 1.. nicht aktiv nur High |
| STAT_C_ESA_FBHI_PRESENT | int | 0.. aktiv 1.. nicht aktiv nur High |
| STAT_C_ESA_ZSHI_PRESENT | int | 0.. aktiv 1.. nicht aktiv nur High |
| STAT_C_ESA_DSHI_PRESENT | int | 0.. aktiv 1.. nicht aktiv nur High |
| STAT_C_WINDSCREEN_PRESENT | int | 0.. aktiv 1.. nicht aktiv nur High |
| STAT_C_DWA_PRESENT | int | 0.. aktiv 1.. nicht aktiv Basic&High |
| STAT_C_LED_KL54_OUTPUT | int | 0.. aktiv 1.. nicht aktiv Basic&High |
| STAT_C_LED_KL58R_OUTPUT | int | 0.. aktiv 1.. nicht aktiv Basic&High |
| STAT_C_LOW_BEAM_BY_HAND_OFF | int | 0.. aktiv 1.. nicht aktiv Basic&High |
| STAT_C_BRAKE_PAD_PRESENT | int | 0.. aktiv 1.. nicht aktiv nur High |
| STAT_C_SENSOR_TYPE | int | 0.. Bosch 1.. Beru Basic&High |
| STAT_C_DF11_TYPE | int | 0.. df11i 1.. df11 Basic&High |
| STAT_C_USAGE_KL58_REAR | int | Verwendung der Kl58_Rear als Versorgung (z.B. für Radio) od. als PWM-Rücklicht 0.. Radio.. Versorgung (dauernd ON und Diagnose Leitungsunterbrechung deaktiviert!) 1.. PWM-Rücklicht nur High |
| STAT_C_SW_MOVE_ONLY_IF_RPM | int | 0.. Windschild auch bei Motorstillstand verstellbar 1.. Windschild ist nur bei Motordrehzahl verstellbar nur High |
| STAT_C_AUTHORITY_LIGHTS | int | 0.. jedes Licht kann ueber Behoerdenschalter deaktiviert werden 1.. Beleuchtung nicht vom Behoerdenschalter betroffen nur High |
| STAT_C_AUTHORITY_FOG_LAMP | int | 0.. KL58_REAR fuer Nebellicht 1.. nicht aktiv nur High |
| STAT_C_AUTHORITY_MAIN_RELAY | int | 0.. Ausgang Sitzheizung_Beifahrer fuer Behoerdenrelais 1.. nicht aktiv nur High |
| STAT_C_WKS_CONFIGURED | int | 0.. Warnkontaktschalter fuer Reserver 1.. Hebel- oder Foliengeber fuer Tankanzeige Basic&High |
| STAT_C_ESA_WITH_HALL_SENSOR | int | 0.. ESA mit Hall, ab PU 06 nur High |
| STAT_C_DOUBLE_POWER_KL56B | int | 0.. aktiv 1.. nicht aktiv Basic&High |
| STAT_C_HAZARD_WARNING_PRESENT | int | 0.. Warnblinker nur ueber Warnblinktaster 1.. Warnblinker auch ueber beide Blinkertaster Basic&High wird von aktueller Software nicht unterstuetzt |
| STAT_C_BRAKE_STATUS_VIA_CAN | int | 0.. Bremslichtansteuerung ueber CAN, CT-ABS 1.. Bremslichtansteuerung ueber Schalter Basic&High |
| STAT_C_TEMP_WHEN_ENGINE_WARM | int | 0.. gespeicherte Temperatur wird bei warmen Motor ausgegeben 1.. gemessene Temperatur Basic&High |
| STAT_C_LAPTIMER_CONFIGURED | int | 0.. Warnblinkschalter als MFSW2-Signal fuer Laptimer 1.. Warnblinkschalter fuer Warnblinkfunktion Basic&High |
| STAT_C_KL56A_PWM_DRIVEN | int | 0.. KL56A ueber PWM gesteuert 1.. KL56A digital nur High |
| STAT_C_OPENLOAD_HORN_DISABLED | int | 0.. OpenLoad Hupe deaktiviert 1.. OpenLoad Hupe aktiv nur High |
| STAT_C_CRUISE_CONTROL_PRESENT | int | 0.. OpenLoad Enable_Pin Tempomat aktiviert 1.. OpenLoad Enable_Pin Tempomat deaktiviert nur High |
| STAT_C_DIAG_SPEED_OUTPUT_ENABLED | int | 0.. OpenLoad Geschwindigkeitsausgang aktiviert 1.. OpenLoad Geschwindigkeitsausgang deaktiviert nur High |
| STAT_C_KL15_BOOST_PRESENT | int | 0.. aktiv 1.. nicht aktiv nur Basic |
| STAT_C_KL56A_KL56B_CROSSFADE | int | 0.. Ausgleich bei Ausfall aktiv 1.. nicht aktiv nur Basic |
| STAT_C_DOUBLE_POWER_KL56A | int | 0.. doppelte Leistung aktiv 1.. nicht aktiv nur Basic |
| STAT_C_FRONT_FBVO_PRESENT | int | 0.. Federbein vorne verbaut 1.. kein Federbein vorne nur High |
| STAT_C_CROSSCOUNTRY_MODE | int | 0.. Geländemodus aktiv 1.. Geländemodus nicht aktiv nur High |
| STAT_C_POSITION_ERROR_NOTIFICATION | int | 0.. enabled 1.. disabled nur High |
| STAT_C_DTC_POSITION_NOT_REACHED | int | 0.. DTC 1.. no DTC nur High |
| STAT_C_ESA_INFINITE_RETRIES | int | 0.. Begrenzung der Wiederholungen nicht aktiv 1.. maximale Anzahl der Wiederholungen in esa_retries_within_KL15 codiert nur High |
| STAT_C_CC_AUTHORITY_BIKE | int | 0.. Ausgang Cruise_Control ist aktiv 1.. Ausgang Cruise_Control ist nicht aktiv nur High |
| STAT_C_ACTIVATE_ESA2_FUNCTIONS | int | 0.. aktiv 1.. nicht aktiv nur High |
| STAT_C_DEACTIVATE_ESAMENUE_BLINIKNG | int | 0.. aktiv 1.. nicht aktiv nur High |
| STAT_C_HEAT_PUSH_BUTTON | int | 0.. Steuerung Sitz- und Griffheizung durch Taster 1.. Steuerung Sitz- und Griffheizung durch Schalter Basci&High |
| STAT_C_FREEZE_FLS_BY_SIDESTAND | int | 0.. aktiv 1.. nicht aktiv |
| STAT_C_TCPL_READ_INJECTED_FUEL | int | 0.. aktiv 1.. nicht aktiv |
| STAT_C_INDUCTIVE_FUEL_SENSOR | int | 0.. aktiv 1.. nicht aktiv |
| STAT_C_NEW_FLS_ALGORITHM | int | 0.. aktiv 1.. nicht aktiv |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Lesen digitaler Stati der Ausgaenge ZFE KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Only Digital Output Signals (siehe ControlState.xls) $01 ReportCurrentState Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_C_KL56B1_SOFT | int | 1. Mosfet Abblendlicht |
| STAT_C_KL56B2_SOFT | int | 2. Mosfet Abblendlicht |
| STAT_C_KL56A | int | Fernlicht |
| STAT_C_HORN | int | Hupe |
| STAT_C_KL58_FRONT_SOFT | int | Standlicht vorne |
| STAT_C_HANDLERHEAT | int | Heizgriffe |
| STAT_SEAT_HEATING_PAS | int | Sitzheizung Sozius |
| STAT_SEAT_HEATING_DRV | int | Sitzheizung Fahrer |
| STAT_C_LICENCE_PLATE | int | Kennzeichenbeleuchtung bzw. KL15 |
| STAT_C_KLBR | int | Blinker rechts |
| STAT_C_KLBL | int | Blinker links |
| STAT_C_ESA_DCMOTOR_OUT1 | int | 1.Ausgang ESA |
| STAT_C_ESA_DCMOTOR_OUT2 | int | 2.Ausgang ESA |
| STAT_C_WIND_SCREEN_OUT1 | int | 1.Ausgang Windschild |
| STAT_C_WIND_SCREEN_OUT2 | int | 2.Ausgang Windschild |
| STAT_C_AUX_FET | int | FET Steckdose |
| STAT_WAKE_UP_LINE | int | WakeUp-Line |
| STAT_CRUISE_CONTROL | int | Tempomat Spannungsversorgung |
| STAT_LOW_SIDE_CRUISE_CONTROL | int | Tempomat SoftOff digitaler Ausgang der Bremslichtschalter ueber CAN Achtung - 1 heisst hier Tempomat aktiv 0 heisst hier Tempomat wegen Bremsen deaktiviert |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-ausgang"></a>
### STATUS_ANALOG_AUSGANG

Lesen der PWM Ausgaenge ZFE und der Geschwindigkeit KWP2000:      $30 InputOutputControlByLocalIdentifier $04 Only Analog Output Signals (siehe ControlState.xls) $01 ReportCurrentState Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PWM_KL54_WERT | real | PWM-Wert Bremslicht Bereich: 0 bis 100 [%] |
| STAT_PWM_KL58_REAR_WERT | real | PWM-Wert Ruecklicht/Zusatzscheinwerfer K7x_MUE Bereich: 0 bis 100 [%] |
| STAT_PWM_FUEL_HEATER_CTL_WERT | real | PWM-Wert Heizung Foliengeber Bereich: 0 bis 100 [%] |
| STAT_PWM_EINH | string | % |
| STAT_SPEED_WERT | real | Tacho-A Signal Periodendauer in ms des SpeedOutput-Signals (2ms High und der Rest der Zeit auf Low) Bereich: 0 bis 128 [ms] |
| STAT_SPEED_EINH | string | ms |
| STAT_STEPPER_ZSVO_WERT | binary | Verstellung Zugstufe vorne Bereich: mögliche Polaritätswerte 0x3F,0x1A,0x12,0x13,0x1B |
| STAT_STEPPER_ZSHI_WERT | binary | Verstellung Zugstufe hinten Bereich: mögliche Polaritätswerte 0x3F,0x1A,0x12,0x13,0x1B |
| STAT_STEPPER_DSHI_WERT | binary | Verstellung Druckstufe hinten Bereich: mögliche Polaritätswerte 0x3F,0x1A,0x12,0x13,0x1B |
| STAT_STEPPER_EINH | string | Einheit Druck- und Zugstufen - |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-eingang"></a>
### STATUS_ANALOG_EINGANG

Lesen analoger Eingaenge der ZFE KWP2000:      $30 InputOutputControlByLocalIdentifier $03 Analog Input Signals (siehe ControlState.xls) $01 ReportCurrentState KWP2000:      $22 ReadDataByCommonIdentifier $300B DataGroup Configuration Parameter (EEPROM) Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_NTC_TEMP_SENSE_WERT | real | Interne Temperatur im Treiberbaustein für die Steckdose Bereich: -20 bis 125 [°C] |
| STAT_NTC_TEMP_SENSE_EINH | string | °C |
| STAT_KL_61_SENSE_WERT | real | Generatorspannung Bereich: 0 bis 16 [Volt] |
| STAT_VBAT_SENSE_WERT | real | Batteriespannung Bereich: 0 bis 16 [Volt] |
| STAT_FRONT_BRAKE_TRIG_WERT | real | Schalter Handbremse Bereich: 0 bis 16  [Volt] Bremse betätigt -&gt; ca. 3 Volt Bremse nicht betätigt -&gt; ca. 7 Volt |
| STAT_REAR_BRAKE_TRIG_WERT | real | Schalter Fussbremse Bereich: 0 bis 16  [Volt] Bremse betätigt -&gt; ca. 3 Volt Bremse nicht betätigt -&gt; ca. 7 Volt |
| STAT_FLS_WERT | real | Tankgeberspannung Bereich: 0 bis 16 [Volt] |
| STAT_FLS_TYP | int | Tankgeberart: 0.. Potentiometer 1.. Foliengeber |
| STAT_U_FUEL_HEATER_WERT | real | Heizspannung Heizdraht (nur bei Foliengeber) Bereich: 0 bis 1 [Volt] |
| STAT_SPANNUNG_EINH | string | Spannung Einheit V |
| STAT_I_FUEL_HEATER_WERT | real | Heizstrom Foliengeber Bereich: 0 bis 300 [mA] |
| STAT_I_FUEL_HEATER_EINH | string | mA |
| STAT_SPEED_WERT | real | Sensorimpulse pro Sekunde (Geschwindigkeitssensor Hinterrad) Geschwindigkeit [km/h] = Radumfang[m]/Zähnezahl*3.6*STAT_SPEED_WERT Bereich: 0 bis 655350 [1/s] |
| STAT_SPEED_EINH | string | Impulse/s |
| STAT_DC_MOTOR_POS2_WERT | real | Potentiometer DC-Motor Pos2 Bereich: 0 bis 5 [Volt] |
| STAT_DC_MOTOR_POS_WERT | real | Potentiometer DC-Motor Pos Bereich: 0 bis 5 [Volt] |
| STAT_DC_MOTOR_POS_DIFF | real | Differenzspannung: Pos-Pos2 Bereich: 0 bis 5 [Volt] |
| STAT_DC_MOTOR_EINH | string | DC-Motor Spannung Einheit V |
| STAT_DC_MOTOR_POS_DIFF_PR_WERT | real | Differenzspannung (Pos-Pos2) als Prozentwert -&gt; 100% = 5Volt Bereich: 0 bis 100 [%] |
| STAT_DC_MOTOR_POS_DIFF_PR_EINH | string | % |
| STAT_EXTERIOR_NTC_TEMP_WERT | real | NTC-Spannung des Außentemperaturfühlers Bereich: 0 bis 5 [Volt] |
| STAT_EXTERIOR_NTC_TEMP_EINH | string | V |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schalter"></a>
### STATUS_SCHALTER

Lesen der Stati der Eingaenge der ZFE KWP2000:      $30 InputOutputControlByLocalIdentifier $01 Digital Inputs (siehe ControlState.xls) $01 ReportCurrentState Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_I_HAND_HEAT_STEP1 | int | Heizgriffe Stufe 1 |
| STAT_I_HAND_HEAT_STEP2 | int | Heizgriffe Stufe 2 |
| STAT_I_HORN | int | Knopf Hupe |
| STAT_I_KLB_OFF | int | Blinkerrueckstellung |
| STAT_I_KL56A | int | Schalter Fernlicht |
| STAT_I_WARNING | int | Knopf Warnblinklicht bzw BC2 Taster |
| STAT_I_KLBL | int | Blinktaster links |
| STAT_I_KLBR | int | Blinktaster rechts |
| STAT_I_ASC | int | Knopf ASC |
| STAT_I_BC | int | Knopf Bordcomputer |
| STAT_I_WIND_SCREEN_SENSOR | int | Windschild Hall-Sensor Eingang |
| STAT_I_WIND_SCREEN_DOWN | int | Taster Windschild runter |
| STAT_I_CRUISE_CONTROL | int | Knopf Tempomat |
| STAT_I_SEAT_HT_DRV_STEP1 | int | Sitzheizung Fahrer Stufe 1 |
| STAT_I_SEAT_HT_DRV_STEP2 | int | Sitzheizung Fahrer Stufe 2 |
| STAT_I_SEAT_HT_PAS_STEP1 | int | Sitzheizung Sozius Stufe 1 |
| STAT_I_SEAT_HT_PAS_STEP2 | int | Sitzheizung Sozius Stufe 2 |
| STAT_I_ESA | int | Knopf ESA |
| STAT_I_WIND_SCREEN_UP | int | Taster Windschild rauf |
| STAT_I_BRAKE_PAD_REAR | int | Eingang Bremsverschleiss hinten |
| STAT_I_REVERSE | int | Eingang ? |
| STAT_I_BRAKE_PAD_FRONT | int | Eingang Bremsverschleiss vorne |
| STAT_I_AUTHORITY_FOG_LAMP | int | Eingang Nebelschlussleuchte für Behörde |
| STAT_I_AUTHORITY_LIGHTS | int | Eingang Lichtabschaltung für Behörde |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-esa"></a>
### STATUS_ESA

Lesen der aktuellen ESA-Position KWP2000:      $30 InputOutputByLocalIdentifier $06 ESA $01 ReportCurrentState Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ESA_BELADUNG | string | Federbasiseinstellung |
| STAT_ESA_DAEMPFER | string | Dämpfereinstellung |
| STAT_AKT_ESA_TEXT | string | Text zum aktuellen Zustand table Status_ESA_Arg3 ESA_TEXT |
| STAT_AKT_ESA_WERT | unsigned char | aktueller Zustand table Status_ESA_Arg3 ESA_WERT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-windschild"></a>
### STATUS_WINDSCHILD

Status des Windschilds KWP2000:      $30 InputOutputByLocalId $05 Windshield $01 Status Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HIGH_POS | int | Obere Position Windschild (Impulse Hallgeber) |
| STAT_POS_COUNT | int | Aktuelle Position Windschild (Impulse Hallgeber) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vorbereiten"></a>
### STEUERN_VORBEREITEN

Kontrolle von ZFE an Diagnosesystem uebergeben KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Outputs (siehe ControlState.xls) $05 FreezeCurrentState $04 Analog Outputs (siehe ControlState.xls) Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag an SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-steuern-abblendlicht"></a>
### STEUERN_ABBLENDLICHT

Abblendlicht direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $03 c_KL56b1_soft $0A c_KL56b2_soft Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Aus- u. Einschalten des Abblendlichts Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag1 an SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag2 an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort2 von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort2 von SG |

<a id="job-steuern-fernlicht"></a>
### STEUERN_FERNLICHT

Fernlicht direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $04 c_KL56a Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Aus- u. Einschalten des Fernlichts Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-standlicht"></a>
### STEUERN_STANDLICHT

Standlicht direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $06 c_KL58_front_soft Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Aus- u. Einschalten des Standlichts Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kennzeichenleuchte"></a>
### STEUERN_KENNZEICHENLEUCHTE

Kennzeichenleuchte direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $10 c_licence_plate Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Aus- u. Einschalten der Kennzeichenleuchte Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bremslicht"></a>
### STEUERN_BREMSLICHT

Bremslicht direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $04 Analog Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $00 c_KL54 Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | int | PWM-Analogwert für Bremslicht Bereich: 0 bis 100 [%] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ruecklicht"></a>
### STEUERN_RUECKLICHT

Ruecklicht/Zusatzscheinwerfer K7x_MUE direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $04 Analog Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $01 c_KL58_rear Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | int | PWM-Analogwert für Rücklicht/Zusatzscheinwerfer Bereich: 0 bis 100 [%] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-blinker-links"></a>
### STEUERN_BLINKER_LINKS

Linken Blinker direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $0E c_KLbl Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Aus- u. Einschalten des linken Blinkers Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-blinker-rechts"></a>
### STEUERN_BLINKER_RECHTS

Rechten Blinker direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $0D c_KLbr Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Aus- u. Einschalten des rechten Blinkers Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-griffheizung"></a>
### STEUERN_GRIFFHEIZUNG

Griffheizung ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $07 c_handlerheat Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Aus- u. Einschalten der Griffheizung Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sitzheizung-fahrer"></a>
### STEUERN_SITZHEIZUNG_FAHRER

Sitzheizung Fahrer ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $09 seat_heating_drv Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Aus- u. Einschalten der Sitzheizung Fahrer Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sitzheizung-sozius"></a>
### STEUERN_SITZHEIZUNG_SOZIUS

Sitzheizung Sozius ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls $07 ShortTermAdjustment $08 seat_heating_pas Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Aus- u. Einschalten der Sitzheizung Sozius Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hupe"></a>
### STEUERN_HUPE

Hupe direkt ansteuern Vorbedingung: Ausführung des Jobs STEUERN_VORBEREITEN KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Output Signals (siehe ControlState.xls) $07 ShortTermAdjustment $05 horn Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Aus- u. Einschalten der Hupe Werte: 0, 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-beenden"></a>
### STEUERN_BEENDEN

Kontrolle an ZFE zurueckgeben KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Digital Outputs (siehe ControlState.xls) $00 ReturnControlToEcu $04 Analog Outputs (siehe ControlState.xls) Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag an SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwor2 von SG |

<a id="job-steuern-esa"></a>
### STEUERN_ESA

ESA ansteuern KWP2000:      $30 InputOutputControlByLocalIdentifier $06 ESA $07 ShortTermAdjustment $XX $YY ESA Parameter Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ESA_BELADUNG | string | Federbasisparameter Werte:E,EB,SO,HU,BE table Steuern_ESA_Arg1 ESA_TEXT |
| ESA_DAEMPFUNG | string | Federdämpfungsparameter Werte:C / soft, N / normal, S / hard table Steuern_ESA_Arg2 ESA_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-windschild"></a>
### STEUERN_WINDSCHILD

Windschild ansteuern KWP2000:      $30 InputOutputControlByLocalIdentifier $05 Windshield $07 ShortTermAdjustment $XX Windshield Parameter Modus:        Default

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

<a id="job-steuern-start-esa-kalibrierung"></a>
### STEUERN_START_ESA_KALIBRIERUNG

Start der ESA-Kalibrierung KWP2000:      $31 StartRoutineByLocalId $22 ESA $01 Rear ESA: Start Reference Run in SO Postion $04 Rear ESA: Start Reference Run in every Postion $05 Front ESA: Start Reference Run in SO Postion $08 Front ESA: Start Reference Run in every Postion $09 Both ESA: Start Reference Run in SO Postion $0C Both ESA: Start Reference Run in every Postion Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAL_TYPE | char | Werte: kein Argument od. 1.. Kalibrierung Hinten aus jeder Federbeinposition 2.. Kalibrierung Hinten mit max. vorgespanntem Federbein 3.. Kalibrierung Vorne aus jeder Federbeinposition 4.. Kalibrierung Vorne mit max. vorgespanntem Federbein 5.. Kalibrierung Vorne und Hinten aus jeder Federbeinposition 6.. Kalibrierung Vorne und Hinten mit max. vorgespanntem Federbein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIBRIERUNG_TEXT | string | table Tab_Kalibrierung_ESA STATUS_TEXT |
| STAT_KALIBRIERUNG_WERT | char | table Tab_Kalibrierung_ESA STATUS_NUMMER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-start-kalibrierung-foliengeber"></a>
### STEUERN_START_KALIBRIERUNG_FOLIENGEBER

Start der Kalibrierung des Foliengebers KWP2000:      $31 StartRoutineByLocalId $20 Thermocouples $01 Start Calibration Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIBRIERUNG_TEXT | string | table Tab_Kalibrierung_Foliengeber STATUS_TEXT |
| STAT_KALIBRIERUNG_WERT | char | table Tab_Kalibrierung_Foliengeber STATUS_NUMMER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-start-kalibrierung-windschild"></a>
### STEUERN_START_KALIBRIERUNG_WINDSCHILD

Start der Kalibrierung des Windschildes KWP2000:      $31 StartRoutineByLocalId $21 Windshield $01 Start Reference Run Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIBRIERUNG_TEXT | string | table Tab_Kalibrierung_Windschild STATUS_TEXT |
| STAT_KALIBRIERUNG_WERT | char | table Tab_Kalibrierung_Windschild STATUS_NUMMER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bbva-init"></a>
### STEUERN_BBVA_INIT

Initialisieren der Bremsbelagsverschleißanzeige Mit diesem Job kann die Bremsbelagsverschleißanzeige nach dem Verbauen neuer Bremsbeläge neu initialisiert werden KWP2000:      $31 StartRoutineByLocalId $23 Brake Pad $01 Reset BrakePadWornOutFront or $02 Reset BrakePadWornOutRear or $03 Reset BrakePadWornOutFront & BrakePadWornOutRear Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POSITION | unsigned char | Werte: 1.. vorne 2.. hinten 3.. vorne und hinten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BBVA_TEXT | string | table Tab_BBVA STATUS_TEXT |
| STAT_BBVA_WERT | char | table Tab_BBVA STATUS_NUMMER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kalibrierung-esa"></a>
### STATUS_KALIBRIERUNG_ESA

Auslesen Status Kalibrierung ESA KWP2000:      $31 StartRoutineByLocalId $22 ESA $03 Status Reference Run Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIBRIERUNG_TEXT | string | table Tab_Kalibrierung_ESA STATUS_TEXT |
| STAT_KALIBRIERUNG_WERT | char | table Tab_Kalibrierung_ESA STATUS_NUMMER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kalibrierung-foliengeber"></a>
### STATUS_KALIBRIERUNG_FOLIENGEBER

Status Kalibrierung des Foliengebers KWP2000:      $31 StartRoutineByLocalId $20 Thermocouples $03 Status Calibration Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIBRIERUNG_TEXT | string | table Tab_Kalibrierung_Foliengeber STATUS_TEXT |
| STAT_KALIBRIERUNG_WERT | char | table Tab_Kalibrierung_Foliengeber STATUS_NUMMER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kalibrierung-windschild"></a>
### STATUS_KALIBRIERUNG_WINDSCHILD

Status Kalibrierung Windschild KWP2000:      $31 StartRoutineByLocalId $21 Windshield $03 Status of Reference Run Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIBRIERUNG_TEXT | string | table Tab_Kalibrierung_Windschild STATUS_TEXT |
| STAT_KALIBRIERUNG_WERT | char | table Tab_Kalibrierung_Windschild STATUS_NUMMER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bbva"></a>
### STATUS_BBVA

Auslesen Status Bremsbelagsverschleißanzeige KWP2000:      $31 StartRoutineByLocalId $23 Brake Pad $04 Ask for status of BrakePadWear Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BBVA_TEXT | string | table Tab_BBVA STATUS_TEXT |
| STAT_BBVA_WERT | char | table Tab_BBVA STATUS_NUMMER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ws-kalibrierstrom"></a>
### STATUS_WS_KALIBRIERSTROM

Kalibrierstrom Windschild KWP2000:      $23 ReadMemoryByAddress $03 $AC Adresse $03 NVRAM $02 Länge 2 Byte Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FEHLERZAEHLER | unsigned char | Windschild Fehlerzähler |
| STAT_STROM | real | Kalibrierstrom wenn Kalibrierung i.O. durchgeführt wurde |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sg-variante"></a>
### STATUS_SG_VARIANTE

Status Bestueckungsvariante der ZFEB Damit wird die (Bestueckungs-)Variante der ZFE(High Full Version, no ESA, ESA only,  Low,  Basic Low,Mid,High) zurueckgegeben KWP2000: $1A Ident $80 Ident  $23 ReadMemoryByAddress $00 High Byte $03 Mid Byte $8E Low Byte for ZFEBasic $E8 Low Byte for ZFEHigh

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SG_VARIANTE_TEXT | string | table TAB_ZFE_Variante TEXT |
| STAT_SG_VARIANTE_WERT | char | table TAB_ZFE_Variante WERT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-status-esa-hall-position"></a>
### STATUS_ESA_HALL_POSITION

Lesen der aktuellen ESA-Hall-Position KWP2000:      $31 StartRoutineByLocalIdentifier $24 ESA Hall $01 Report max number of pulses rear, $02 Report acutal position rear $03 Number of pulses front, $03 Actual position front Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ESA_HALL_HINTEN_MAX | int | Maximaler Verstellweg ESA Hinten Einheit PULSE |
| STAT_ESA_HALL_HINTEN_POS | int | Aktuelle Position ESA Hinten Einheit PULSE |
| STAT_ESA_HALL_VORNE_MAX | int | Maximaler Verstellweg ESA Vorne Einheit PULSE |
| STAT_ESA_HALL_VORNE_POS | int | Aktuelle Position ESA Vorne Einheit PULSE |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-speed-sensor-df11i"></a>
### STATUS_SPEED_SENSOR_DF11I

Status Information (Zusatzinfo) beim DF11i KWP2000:      $30 InputOutputByLocalId $07 Speed Sensor DF11i Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DF11I_TEXT | string | table Tab_Sensor_DF11i STATUS_TEXT |
| STAT_DF11I_WERT | char | table Tab_Sensor_DF11i STATUS_NUMMER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-emergency-software"></a>
### STEUERN_EMERGENCY_SOFTWARE

Starten/Beenden der Emergency Software KWP2000:      $31 StartRoutineByLocalId $25 Emergency Software $01 Enable Emergency Software $02 Disable Emergency Software Modus:        Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IO_VALUE | string | Emergency-SW ein- bzw. ausschalten Werte: 0 aus, 1 ein table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EMERGENCY_TEXT | string | Emergency_SW STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-foliengeber"></a>
### _STATUS_FOLIENGEBER

Lesen analoger Eingaenge der ZFE KWP2000:      $30 InputOutputControlByLocalIdentifier $03 Analog Input Signals (siehe ControlState.xls) $01 ReportCurrentState KWP2000:      $22 ReadDataByCommonIdentifier $300B DataGroup Configuration Parameter (EEPROM) KWP2000:      $30 InputOutputControlByLocalIdentifier $04 Only Analog Output Signals (siehe ControlState.xls) $01 ReportCurrentState KWP2000:      $30 InputOutputControlByLocalIdentifier $02 Only Digital Output Signals (siehe ControlState.xls) $01 ReportCurrentState Modus:        Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VBAT_SENSE_WERT | real | Batteriespannung Bereich: 0 bis 16 [Volt] |
| STAT_FLS_WERT | real | Tankgeberspannung Bereich: 0 bis 5   [Volt] (bei Hebelgeber) Bereich: 0 bis 0.5 [Volt] (bei Foliengeber) |
| STAT_FLS_TYP | int | Tankgeberart: 0.. Potentiometer 1.. Foliengeber |
| STAT_U_FUEL_HEATER_WERT | real | Heizspannung Heizdraht (nur bei Foliengeber) Bereich: 0 bis 0.5 [Volt] |
| STAT_SPANNUNG_EINH | string | Spannung Einheit V |
| STAT_I_FUEL_HEATER_WERT | real | Heizstrom Foliengeber Bereich: 0 bis 300 [mA] |
| STAT_I_FUEL_HEATER_EINH | string | mA |
| STAT_PWM_FUEL_HEATER_CTL_WERT | real | PWM-Wert Heizung Foliengeber Bereich: 0 bis 100 [%] |
| STAT_PWM_EINH | string | % |
| STAT_FUEL_HEATER_CTL_DIG | int | Heizung Foliengeber ein/aus |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG4 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT4 | binary | Hex-Antwort von SG |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-flash-parameter-lesen"></a>
### FLASH_PARAMETER_LESEN

Gibt die SG-spezifischen Flash-Parameter zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_DIAG_PROT oder ERROR_SG_AUTHENTISIERUNG |
| SG_ADRESSE | int | Steuergeräteadresse |
| SG_MAXANZAHL_AIF | int | Anzahl der Anwender-Infofelder |
| SG_GROESSE_AIF | int | Grösse des Anwender-Infofeldes |
| SG_ENDEKENNUNG_AIF | int | Offset für letztes Anwender-Infofeld |
| SG_AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTH_TEXT |
| DIAG_PROT_IST | string | Gibt das aktuelle gewählte Protokoll aus table KONZEPT_TABELLE KONZEPT_TEXT |

<a id="job-flash-parameter-setzen"></a>
### FLASH_PARAMETER_SETZEN

Setzt die SG-spezifischen Flash-Parameter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ADRESSE | int | Steuergeräteadresse |
| SG_MAXANZAHL_AIF | int | Anzahl der Anwender-Infofelder 0x00  Nicht zulässig sonst Anzahl der AIF |
| SG_GROESSE_AIF | int | Grösse des Anwender-Infofeldes 0x12  18 dez kleines AIF 0x33  51 dez grosses AIF 0x40  64 dez grosses AIF ( gilt nur für Power-Pc ) sonst Nicht zulässig |
| SG_ENDEKENNUNG_AIF | int | Offset für letztes Anwender-Infofeld 0xFE  Letztes AIF nicht überschreibbar 0x01  Letztes AIF ist überschreibbar sonst Nicht zulässig |
| SG_AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTH_TEXT |
| DIAG_PROT | string | optionaler Parameter Diagnoseprotokoll table KONZEPT_TABELLE KONZEPT_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

<a id="job-interfacetype"></a>
### INTERFACETYPE

Interface-Typ bestimmen und ausgeben Es wird der Name des Interfaces übergeben Wichtig für Baudratenumschaltung weil bei ADS, EADS und OBD sind nur 115200 Baud möglich, bei EDIC nur 125000 Baud möglich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| INTERFACE_TYP | string | Rueckmeldung des Interface-Typs |

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

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (140 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (81 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 9)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (5 × 2)
- [STATUS_ESA_ARG3](#table-status-esa-arg3) (5 × 2)
- [STEUERN_ESA_ARG1](#table-steuern-esa-arg1) (6 × 3)
- [STEUERN_ESA_ARG2](#table-steuern-esa-arg2) (4 × 3)
- [STEUERN_WINDSHIELD_ARG](#table-steuern-windshield-arg) (9 × 2)
- [TAB_ZFE_VARIANTE](#table-tab-zfe-variante) (8 × 2)
- [TAB_BBVA](#table-tab-bbva) (6 × 3)
- [TAB_KALIBRIERUNG_ESA](#table-tab-kalibrierung-esa) (20 × 3)
- [TAB_KALIBRIERUNG_FOLIENGEBER](#table-tab-kalibrierung-foliengeber) (5 × 3)
- [TAB_KALIBRIERUNG_WINDSCHILD](#table-tab-kalibrierung-windschild) (5 × 3)
- [TAB_SENSOR_DF11I](#table-tab-sensor-df11i) (7 × 3)

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

Dimensions: 140 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
| 0x02 | Leopold Kostal GmbH & Co. KG |
| 0x03 | Hella Fahrzeugkomponenten GmbH |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako GmbH |
| 0x08 | Robert Bosch GmbH |
| 0x09 | Lear Corporation |
| 0x10 | VDO |
| 0x11 | Valeo GmbH |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine Electronics GmbH |
| 0x18 | Continental Teves AG & Co. OHG |
| 0x19 | Elektromatik Südafrika |
| 0x20 | Harman Becker Automotive Systems |
| 0x21 | Preh GmbH |
| 0x22 | Alps Electric Co. Ltd. |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto SE |
| 0x26 | MotoMeter |
| 0x27 | Delphi Automotive PLC |
| 0x28 | DODUCO (Beru) |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer Corporation |
| 0x33 | Jatco |
| 0x34 | FUBA Automotive GmbH & Co. KG |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0x38 | Sachs |
| 0x39 | ITT |
| 0x40 | FTE (Fahrzeugtechnik Ebern) |
| 0x41 | Megamos |
| 0x42 | TRW Automotive GmbH |
| 0x43 | WABCO Fahrzeugsysteme GmbH |
| 0x44 | ISAD Electronic Systems |
| 0x45 | HEC Hella Electronics Corporation |
| 0x46 | Gemel |
| 0x47 | ZF Friedrichshafen AG |
| 0x48 | GMPT |
| 0x49 | Harman Becker Automotive Systems GmbH |
| 0x50 | Remes GmbH |
| 0x51 | ZF Lenksysteme GmbH |
| 0x52 | Magneti Marelli S.p.A. |
| 0x53 | Johnson Controls Inc. |
| 0x54 | GETRAG Getriebe- und Zahnradf. Hermann Hagenmeyer GmbH & Co. KG |
| 0x55 | Behr-Hella Thermocontrol GmbH |
| 0x56 | Siemens VDO Automotive |
| 0x57 | Visteon Innovation & Technology GmbH |
| 0x58 | Autoliv AB |
| 0x59 | Haberl Electronic GmbH & Co. KG |
| 0x60 | Magna International Inc. |
| 0x61 | Marquardt GmbH |
| 0x62 | AB Elektronik GmbH |
| 0x63 | SDVO/BORG |
| 0x64 | Hirschmann Car Communication GmbH |
| 0x65 | hoerbiger-electronics |
| 0x66 | Thyssen Krupp Automotive |
| 0x67 | Gentex Corporation |
| 0x68 | Atena GmbH |
| 0x69 | Magna-Donelly |
| 0x70 | Koyo Steeting Europe |
| 0x71 | NSI Beheer B.V. |
| 0x72 | Aisin AW Co. Ltd. |
| 0x73 | Schorlock |
| 0x74 | Schrader Electronics Ltd. |
| 0x75 | Huf-Electronics Bretten GmbH |
| 0x76 | CEL |
| 0x77 | AUDIO MOBIL Elektronik GmbH |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia-Automotive GmbH |
| 0x81 | Tyco Electronics |
| 0x82 | Paragon AG |
| 0x83 | IEE S.A. |
| 0x84 | TEMIC AUTOMOTIVE of NA |
| 0x85 | Sonceboz S.A. |
| 0x86 | Meta System S.p.A. |
| 0x87 | Huf Hülsbeck & Fürst GmbH & Co. KG |
| 0x88 | MANN+HUMMEL GmbH |
| 0x89 | Brose Fahrzeugteile GmbH & Co. |
| 0x90 | Keihin |
| 0x91 | Vimercati S.p.a |
| 0x92 | CRH |
| 0x93 | TPO Display Corp |
| 0x94 | Küster Automotive GmbH |
| 0x95 | Hitachi Automotive |
| 0x96 | Continental AG |
| 0x97 | TI-Automotive |
| 0x98 | Hydro |
| 0x99 | Johnson Controls Inc. |
| 0x9A | Takata-Petri |
| 0x9B | Mitsubishi Electric B.V. (Melco) |
| 0x9C | Autokabel |
| 0x9D | GKN Plc |
| 0x9E | Zollner Elektronik AG |
| 0x9F | peiker acustic GmbH & Co. KG |
| 0xA0 | Bosal-Oris |
| 0xA1 | Cobasys |
| 0xA2 | Automotive Lighting Reutlingen GmbH |
| 0xA3 | CONTI VDO |
| 0xA4 | A.D.C. Automotive Distance Control Systems GmbH |
| 0xA5 | Novero Dabendorf GmbH |
| 0xA6 | LAMES S.p.a. |
| 0xA7 | Magna/Closures |
| 0xA8 | Harbin Wan Yu Technology Co |
| 0xA9 | ThyssenKrupp Presta AG |
| 0xAA | ArvinMeritor |
| 0xAB | Kongsberg Automotive GmbH |
| 0xAC | SMR Automotive Mirrors Stuttgart GmbH |
| 0xAD | So.Ge.Mi. |
| 0xAE | MTA S.p.A. |
| 0xAF | Alfmeier Präzision AG |
| 0xB0 | Eltek Deutechland GmbH |
| 0xB1 | OMRON Automotive Electronics Europe GmbH |
| 0xB2 | ASK Industries GmbH |
| 0xB3 | CML Innovative Technologies GmbH & Co. KG |
| 0xB4 | APAG Elektronik AG |
| 0xB5 | Nexteer Automotive |
| 0xB6 | Hans Widmaier Fernmelde- und Feinwerktechnik |
| 0xB7 | Robert Bosch Battery Systems GmbH |
| 0xB8 | Kyocera Display Europe GmbH |
| 0xB9 | Magna Powertrain AG & Co. KG |
| 0xBA | BorgWarner Beru Systems GmbH |
| 0xBB | BMW AG |
| 0xBC | Benteler Duncan Plant |
| 0xBD | U-Shin Deutschland Zugangssysteme GmbH |
| 0xBE | Schaeffler Technologies AG & Co. KG |
| 0xBF | JTEKT Corporation |
| 0xC0 | VLF |
| 0xC1 | Flextronics |
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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 81 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA2E8 | Kl30 Unterspannung |
| 0xA2E9 | Tankgeber |
| 0xA2EA | Handbremsschalter Kurzschluß nach Masse |
| 0xA2EB | Handbremsschalter Kurzschluß nach Plus |
| 0xA2EC | Handbremsschalter Leitungsunterbrechung |
| 0xA2ED | Fussbremsschalter Kurzschluß nach Masse |
| 0xA2EE | Fussbremsschalter Kurzschluß nach Plus |
| 0xA2EF | Fussbremsschalter Leitungsunterbrechung |
| 0xA2F1 | Geschwindigkeitssensor |
| 0xA2F2 | Taster Hupe |
| 0xA2F3 | Taster Warnblinkschalter |
| 0xA2F4 | Taster Blinker links |
| 0xA2F5 | Taster Blinker rechts |
| 0xA2F6 | Taster Blinkerrückstellung |
| 0xA2F7 | Rücklicht/Radio/NSL/Zusatzscheinwerfer Kurzschluß |
| 0xA2F8 | Rücklicht/NSL/Zusatzscheinwerfer Leitungsunterbrechung |
| 0xA2F9 | Standlicht Kurzschluß |
| 0xA2FA | Standlicht Leitungsunterbrechung |
| 0xA2FB | Fernlicht Kurzschluß |
| 0xA2FC | Fernlicht Leitungsunterbrechung |
| 0xA2FD | Abblendlicht 1 Kurzschluß |
| 0xA2FE | Abblendlicht 1 Leitungsunterbrechung |
| 0xA2FF | Abblendlicht 2 Kurzschluß |
| 0xA301 | Abblendlicht 2 Leitungsunterbrechung |
| 0xA302 | Bremslicht Kurzschluß |
| 0xA303 | Bremslicht Leitungsunterbrechung |
| 0xA306 | Blinker links Kurzschluß |
| 0xA307 | Blinker links Leitungsunterbrechung |
| 0xA308 | Blinker rechts Kurzschluß |
| 0xA309 | Blinker rechts Leitungsunterbrechung |
| 0xA30A | Hupe Kurzschluß |
| 0xA30B | Hupe Leitungsunterbrechung |
| 0xA30C | Heizgriffe Kurzschluß |
| 0xA30D | Heizgriffe Leitungsunterbrechung |
| 0xA30F | Bordsteckdose Kurzschluß |
| 0xA311 | CAN Time Out DWA |
| 0xA319 | CAN Bus Off |
| 0xA31A | CAN Time Out BMS-K |
| 0xA31B | CAN Time Out ABS |
| 0xA31C | CAN Time Out I-Kombi |
| 0xA31D | EEPROM Fehler |
| 0xA31E | Kl30 Überspannung |
| 0xA320 | Sitzheizung Fahrer Kurzschluß |
| 0xA321 | Sitzheizung Fahrer Leitungsunterbrechung |
| 0xA322 | Sitzheizung Beifahrer Kurzschluß |
| 0xA323 | Sitzheizung Beifahrer Leitungsunterbrechung |
| 0xA324 | Windschildverstellung/Federbeinverstellung vorne Kurzschluß |
| 0xA325 | Windschildverstellung/Federbeinverstellung vorne Leitungsunterbrechung |
| 0xA326 | Federbeinverstellung hinten Kurzschluß |
| 0xA327 | Federbeinverstellung hinten Leitungsunterbrechung/Kurzschluß |
| 0xA328 | Sensorsignal ESA hinten |
| 0xA329 | Sensorsignal Windschild / ESA vorne |
| 0xA32A | Federbeinverstellung hinten Position nicht erreicht |
| 0xA32B | Federbeinverstellung vorne Position nicht erreicht |
| 0xA32C | Druckstufenverstellung hinten Kurzschluß |
| 0xA32D | Druckstufenverstellung hinten Leitungsunterbrechung |
| 0xA32E | Zugstufenverstellung hinten Kurzschluß |
| 0xA32F | Zugstufenverstellung hinten Leitungsunterbrechung |
| 0xA330 | Zugstufenverstellung vorne Kurzschluß |
| 0xA331 | Zugstufenverstellung vorne Leitungsunterbrechung |
| 0xA332 | Heizdraht Tanksensor |
| 0xA333 | Taster Windschildverstellung auf |
| 0xA334 | Taster Windschildverstellung ab |
| 0xA335 | Taster ESA |
| 0xA336 | Energiesparmode aktiv |
| 0xA337 | Taster BC |
| 0xA33E | Tempomat Versorgung Kurzschluß nach Masse |
| 0xA33F | Externer Temperatursensor: Leitungsunterbrechung/Kurzschluss nach Plus |
| 0xA340 | Weckleitung Kurzschluß |
| 0xA341 | Fehler Kalibrierparameter Foliengeber |
| 0xA342 | Fehler Kalibrierparameter Windschild/ESA vorne |
| 0xA343 | Fehler Kalibrierparameter ESA |
| 0xA34D | Externer Temperatursensor: Kurzschluss nach Masse |
| 0xA352 | Tempomat Ansteuerung Kurzschluß nach Masse/Leitungsunterbrechung |
| 0xA355 | Geschwindigkeitssignal Ausgang Leitungsunterbrechung/Kurzschluß nach Masse |
| 0xA356 | Taster Griffheizung |
| 0xA357 | Taster Sitzheizung vorne |
| 0xA358 | Versorgung Hall-Sensor Federbein vorne Leitungsunterbrechung |
| 0xA359 | Versorgung Hall-Sensor Federbein hinten Leitungsunterbrechung |
| 0xA35A | Thermische Ueberlast Federbeinverstellung hinten |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xA2E8 | 0x01 | 0x02 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | - | unsigned char | -- | 185 | 2560 | 0 |
| 0x02 | Geschwindigkeit | km/h | high | unsigned int | -- | 1 | 16 | 0 |
| 0xFF | unbekannte Umweltbedingung | 1 | - | unsigned char | -- | 1 | 1 | 0 |
| 0xXYXY | UWB_UNKNOWN | - | - | - | - | - | - | - |

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
| F_UWB_ERW | nein |

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
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 5 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| - | BMW-FAST |
| - | KWP2000* |
| 1 | KWP2000 |
| - | DS2 |
| 2 | D-CAN |

<a id="table-status-esa-arg3"></a>
### STATUS_ESA_ARG3

Dimensions: 5 rows × 2 columns

| ESA_TEXT | ESA_WERT |
| --- | --- |
| ESA noch in alter Position | 0x00 |
| ESA-Verstellung läuft | 0x01 |
| ESA-Endposition erfolgreich erreicht | 0x02 |
| ESA-Fehler bei Ansteuerung | 0x03 |
| nicht gültig | 0xXY |

<a id="table-steuern-esa-arg1"></a>
### STEUERN_ESA_ARG1

Dimensions: 6 rows × 3 columns

| ESA_TEXT | ESA_WERT | ESA_INFO |
| --- | --- | --- |
| E | 0x01 | Einzel |
| EB | 0x02 | Einzel Beladung |
| SO | 0x03 | Sozius |
| HU | 0x04 | Huegel |
| BE | 0x05 | Berg |
| nicht gültig | 0xXY | - |

<a id="table-steuern-esa-arg2"></a>
### STEUERN_ESA_ARG2

Dimensions: 4 rows × 3 columns

| ESA_TEXT | ESA_WERT | ESA_INFO |
| --- | --- | --- |
| N | 0x01 | normal |
| C | 0x02 | comfort |
| S | 0x03 | sport |
| nicht gültig | 0xXY | - |

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

<a id="table-tab-zfe-variante"></a>
### TAB_ZFE_VARIANTE

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ZFEBasic_Low |
| 0x01 | ZFEBasic_Mid |
| 0x02 | ZFEBasic_High |
| 0x10 | ZFELow |
| 0x20 | ZFEHigh Full Version |
| 0x21 | ZFEHigh no ESA |
| 0x22 | ZFEHigh ESA only |
| 0xff | Keine_gueltige_Variante |

<a id="table-tab-bbva"></a>
### TAB_BBVA

Dimensions: 6 rows × 3 columns

| STATUS_ID | STATUS_NUMMER | STATUS_TEXT |
| --- | --- | --- |
| 0x00 | 0 | Status OK - Bremsbeläge i.O. |
| 0x01 | 1 | Bremsbelag vorne verschlissen |
| 0x02 | 2 | Bremsbelag hinten verschlissen |
| 0x03 | 3 | Bremsbelag vorne und hinten verschlissen |
| 0xFD | 4 | Steuergerätereset wird abgewartet |
| 0xXY | -1 | nicht gültig |

<a id="table-tab-kalibrierung-esa"></a>
### TAB_KALIBRIERUNG_ESA

Dimensions: 20 rows × 3 columns

| STATUS_ID | STATUS_NUMMER | STATUS_TEXT |
| --- | --- | --- |
| 0xFD | 1 | Kalibrierung aktiviert, läuft aber noch nicht |
| 0xFE | 2 | Kalibrierung wird durchgeführt |
| 0x00 | 3 | Kalibrierung erfolgreich abgeschlossen |
| 0x01 | 5 | Fehler ESA Sensor Hinten |
| 0x02 | 4 | Kalibrierung Hinten durch Anwender gestoppt |
| 0x03 | 5 | Fehler ESA Sensor Vorne |
| 0x04 | 4 | Kalibrierung Vorne durch Anwender gestoppt |
| 0x05 | 6 | Kalibrierung Hinten erfolgreich abgeschlossen, Kalibrierung Vorne wird durchgeführt |
| 0x06 | 7 | Kalibrierung Vorne erfolgreich abgeschlossen, Kalibrierung Hinten wird durchgeführt |
| 0x07 | 8 | Kalibrierung Hinten erfolgreich abgeschlossen, ESA Vorne fehlerhaft |
| 0x08 | 9 |  Kalibrierung Vorne erfolgreich abgeschlossen, ESA hinten fehlerhaft |
| 0x09 | 10 |  ESA Hinten fehlerhaft, Kalibrierung Vorne wird durchgeführt |
| 0x0A | 11 |  ESA Vorne fehlerhaft, Kalibrierung Hinten wird durchgeführt |
| 0x0B | 4 | Kalibrierung ESA Vorne und Hinten durch Anwender gestoppt |
| 0x0C | 12 | Minimale Pulsanzahl beider ESA nicht erreicht |
| 0x0D | 12 | Nach Kalibrierung beider ESAs minimale Pulszahl hinten nicht erreicht |
| 0x0E | 12 | Nach Kalibrierung beider ESAs minimale Pulszahl vorne nicht erreicht |
| 0x0F | 12 | Minimale Pulszahl hinten nicht erreicht |
| 0xFF | -1 | nicht gültig |
| 0xXY | 4 | Fehler bei Kalibrierung |

<a id="table-tab-kalibrierung-foliengeber"></a>
### TAB_KALIBRIERUNG_FOLIENGEBER

Dimensions: 5 rows × 3 columns

| STATUS_ID | STATUS_NUMMER | STATUS_TEXT |
| --- | --- | --- |
| 0xFD | 1 | Kalibrierung aktiviert, läuft aber noch nicht |
| 0xFE | 2 | Kalibrierung wird durchgeführt |
| 0x00 | 3 | Kalibrierung erfolgreich abgeschlossen |
| 0xFF | -1 | nicht gültig |
| 0xXY | 4 | Fehler bei Kalibrierung |

<a id="table-tab-kalibrierung-windschild"></a>
### TAB_KALIBRIERUNG_WINDSCHILD

Dimensions: 5 rows × 3 columns

| STATUS_ID | STATUS_NUMMER | STATUS_TEXT |
| --- | --- | --- |
| 0xFD | 1 | Kalibrierung wird durchgeführt |
| 0xFE | 2 | Kalibrierung wird durchgeführt |
| 0x00 | 3 | Kalibrierung erfolgreich abgeschlossen |
| 0xFF | -1 | nicht gültig |
| 0xXY | 4 | Fehler bei Kalibrierung |

<a id="table-tab-sensor-df11i"></a>
### TAB_SENSOR_DF11I

Dimensions: 7 rows × 3 columns

| STATUS_ID | STATUS_NUMMER | STATUS_TEXT |
| --- | --- | --- |
| 0x00 | 0 | STOP (Standstill) |
| 0x01 | 1 | LR |
| 0x02 | 2 | DR-L |
| 0x03 | 3 | DR-R |
| 0x04 | 4 | DR-L/EL |
| 0x05 | 5 | DR-R/EL |
| 0xXY | 255 | unbekannter Status |
