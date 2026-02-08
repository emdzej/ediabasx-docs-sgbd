# LM_AHL_2.PRG

- Jobs: [150](#jobs)
- Tables: [35](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | LM-AHL 2 |
| ORIGIN | BMW EI-63 Tom Willmann |
| REVISION | 1.000 |
| AUTHOR | LEAR DCS Ahrens |
| COMMENT | N/A |
| PACKAGE | 1.30 |
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
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
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
- [STATUS_DIGITAL_INPUTS](#job-status-digital-inputs) - Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $01 Digitale Inputs
- [STATUS_ANALOG_INPUTS](#job-status-analog-inputs) - Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 Analoge Inputs
- [STATUS_DIMMWERT](#job-status-dimmwert) - KWP2000: $30-&gt;IOCBLI $08-&gt;Auslesen der analogen Stati (%) aller Lampen $01-&gt;RCS
- [STATUS_LAMPEN_DIGITAL](#job-status-lampen-digital) - KWP2000: $30-&gt;IOCBLI $08-&gt;Auslesen der digitalen Stati (EIN/AUS) aller Lampen $01-&gt;RCS
- [STATUS_SENSE_LESEN](#job-status-sense-lesen) - Senseausgang fuer ausgewaehlte Lampe lesen, FRMFA KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $17 Sensewerte lesen Modus  : Default
- [STATUS_LAMPEN_DEFEKTE](#job-status-lampen-defekte) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $27 Lampenfehler auslesen Status Defektbits (explizit) von LM-II lesen
- [STATUS_FLC_FLA_AHL](#job-status-flc-fla-ahl) - Auslesen spezieller Stati KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $28 Stati fuer FLC, FLA und AHL
- [STATUS_FAHRZEUGNEIGUNG](#job-status-fahrzeugneigung) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2A STATUS_FAHRZEUGNEIGUNG
- [_STATUS_LAMPE_EIN_SENSE_LESEN_LEAR](#job-status-lampe-ein-sense-lesen-lear) - Senseausgang fuer ausgewaehlte Lampe lesen, FRMFA KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2D Lampe ein Sensewerte lesen Modus  : Default
- [STEUERN_LAMPEN_DIGITAL](#job-steuern-lampen-digital) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Dimmwert an PWM-Port Status von LM-II schreiben Ausgewaehlte Lampe voll ein bzw. ausschalten
- [STEUERN_LAMPEN_PWM](#job-steuern-lampen-pwm) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Dimmwert an PWM-Port Status von LM-II schreiben Lampe mit Prozentwert ein- bzw. ausschalten
- [STEUERN_AL_EINSCHALTEN](#job-steuern-al-einschalten) - Abblendlicht ueber Diagnose ein- bzw. ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0F Abblendlicht ein- bzw. ausschalten Status von LM-II schreiben
- [STEUERN_LAMPEN_FUNKTIONEN_EINSCHALTEN](#job-steuern-lampen-funktionen-einschalten) - Lampenfunktionen ueber Diagnose ein- bzw. ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $29 Lampenfunktionen ein- bzw. ausschalten Status von LM-II schreiben
- [STEUERN_BFD_STUFE](#job-steuern-bfd-stufe) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $24 BFD-Stufe ein-/ausschalten Status von LM II schreiben Ausgewaehlte BFD-Stufe ein bzw. ausschalten
- [STEUERN_POSITION_LWR](#job-steuern-position-lwr) - bestimmte Position der LWR anfahren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $09 Position der LWR anfahren Status von LM II schreiben
- [START_LAMPEN_PRE_DRIVE_CHECK](#job-start-lampen-pre-drive-check) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $2B Start des Pre-Drive-Checks der Lampen Status von LM2 schreiben
- [_STEUERN_SLEEPMODE_FERTIGUNG_LEAR](#job-steuern-sleepmode-fertigung-lear) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $2C Sleepmode Fertigung Status von LM-II schreiben sofortiger Sleepmode
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default
- [C_FA_SCHREIBEN](#job-c-fa-schreiben) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default
- [READ_FVIN](#job-read-fvin) - liest die lange Fahrgestellnummer KWP 2000: $22 ReadDataByCommonIdentifier $1010 FVIN
- [WRITE_FVIN](#job-write-fvin) - schreibt die lange Fahrgestellnummer KWP 2000: $2E WriteDataByCommonIdentifier $1010 FVIN
- [FVIN_AUFTRAG](#job-fvin-auftrag) - lange Fahrgestellnummer schreiben und ruecklesen KWP 2000: $2E WriteDataByCommonIdentifier $1010 FVIN KWP 2000: $22 ReadDataByCommonIdentifier $1010 FVIN
- [_CODIERDATEN_BLOCK_LESEN_LEAR](#job-codierdaten-block-lesen-lear) - KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default
- [_CODIERDATEN_BLOCK_SCHREIBEN_LEAR](#job-codierdaten-block-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $xxxx Codierdaten Modus  : Codieren je nach Block
- [_CODIERDATEN_3400_LESEN_KOMPLETT_LEAR](#job-codierdaten-3400-lesen-komplett-lear) - Auslesen der kompletten Codierdaten im 3400-Bereich Auslesen der LM2-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [_CODIERDATEN_3000_LESEN_KOMPLETT_LEAR](#job-codierdaten-3000-lesen-komplett-lear) - Auslesen der kompletten Codierdaten im 3000-Bereich Auslesen der ALC-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [_CODIERDATEN_3400_SCHREIBEN_AUS_DATEI_LEAR](#job-codierdaten-3400-schreiben-aus-datei-lear) - Beschreiben der Default-Codierdaten Beschreiben der LM2-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $34xx Codierdaten, Default Modus  : Default
- [_CODIERDATEN_KOMPLETT_SCHREIBEN_LEAR](#job-codierdaten-komplett-schreiben-lear) - Beschreiben der Default-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten AHL schreiben $31xx Codierdaten Code schreiben $32xx Codierdaten SMC_L schreiben $33xx Codierdaten SMC_R schreiben $34xx Codierdaten LM2 schreiben Modus  : Default
- [_READ_LINK_DATE_TIME_LEAR](#job-read-link-date-time-lear) - Auslesen der Linkdate und -time KWP2000: $21 ReadDataByLocalIdentifier $01 Linkdate und -time
- [_READ_EMERGENCY_FALLBACK_COUNTER_LEAR](#job-read-emergency-fallback-counter-lear) - Auslesen der Fallback Counter KWP2000: $21 ReadDataByLocalIdentifier $02 Fallback Counter
- [_CLR_EMERGENCY_FALLBACK_COUNTER_LEAR](#job-clr-emergency-fallback-counter-lear) - KWP2000: $3B WriteDataByLocalIdentifier $02 NOTLAUF_FALLBACK_COUNTER Modus  : Default
- [_READ_ABS_TIMER_LEAR](#job-read-abs-timer-lear) - Auslesen der Fallback Counter KWP2000: $21 ReadDataByLocalIdentifier $09 ABS_TIMER
- [_CLR_ABS_TIMER_LEAR](#job-clr-abs-timer-lear) - KWP2000: $3B WriteDataByLocalIdentifier $09 ABS_TIMER Modus  : Default
- [_HERSTELLER_DATEN_LESEN_LEAR](#job-hersteller-daten-lesen-lear) - Auslesen der Herstellerdaten KWP2000: $21 ReadDataByLocalIdentifier $04 Herstellerdaten
- [_HERSTELLER_DATEN_SCHREIBEN_LEAR](#job-hersteller-daten-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $3B WriteDataByLocalIdentifier $04 Herstellerdaten
- [STATUS_LWR_LESEN](#job-status-lwr-lesen) - Unterscheidung zwischen dynamischer, automatischer und manueller LWR KWP2000: $21 ReadDataByLocalIdentifier $05 LWR lesen
- [_READ_ENERGY_SAVING_MODE_LEAR](#job-read-energy-saving-mode-lear) - Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode
- [_CBD_ZEICHN_INDEX_LESEN_LEAR](#job-cbd-zeichn-index-lesen-lear) - Auslesen des Aenderungsindex aus den Codierdaten KWP2000: $21 ReadDataByLocalIdentifier $06 CBD_ZEICHN_INDEX lesen
- [STATUS_SENSE_INPUTS](#job-status-sense-inputs) - Auslesen der Sensewerte der einzelnen Lampen KWP2000: $21 ReadDataByLocalIdentifier $08 Sensewerte lesen
- [STATUS_PIA_DATEN](#job-status-pia-daten) - Auslesen der momentan aktuellen Piadaten KWP2000: $21 ReadDataByLocalIdentifier $0A Piadaten
- [_BRIF_SCHREIBEN_LEAR](#job-brif-schreiben-lear) - Writting the BRIF in EEPROM All the arguments should be supplied KWP2000: $2E WriteDataByCommonIdentifier $34Fx BRIF Modus  : Default
- [_BRIF_FILE_LEAR](#job-brif-file-lear) - Writting the BRIF in EEPROM All the arguments should be supplied KWP2000: $2E WriteDataByCommonIdentifier $34Fx BRIF Modus  : Default
- [STATUS_BETR_H_FUNKTIONEN](#job-status-betr-h-funktionen) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $06 Betriebsstunden fuer alle Funktionen Status von LM2 lesen Lesen der Betriebsstunden der einzelnen Lampenfunktionen des LM2
- [STEUERN_BETR_H_LM2_LOESCHEN](#job-steuern-betr-h-lm2-loeschen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Betriebsstunden Status von LM2 schreiben Loeschen aller Betriebsstunden des FRM2
- [STATUS_LWR_POSITION](#job-status-lwr-position) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $09 STATUS_LWR_POSITION
- [STATUS_XENON_AL_EINSCHALTVERSUCHE](#job-status-xenon-al-einschaltversuche) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $14 Xenon-AL-Einschaltversuche Auslesen wie oft das Abblendlicht eingeschaltet wurde
- [STEUERN_XENON_AL_EINSCHALTVERSUCHE_LOESCHEN](#job-steuern-xenon-al-einschaltversuche-loeschen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $14 Xenon-AL-Einschaltversuche Loeschen der AL-Einschaltversuche
- [_WARTEZEIT_LEAR](#job-wartezeit-lear) - Wartezeit
- [_RESET_KURZSCHLUSS_SPERRE](#job-reset-kurzschluss-sperre) - Kurzschlusssperre ueber Diagnose ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1F Kurzschlusssperre ausschalten Status von LM2 schreiben
- [STATUS_LAMPEN_KURZSCHLUSS](#job-status-lampen-kurzschluss) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $20 Lampenkurzschluss auslesen Status Lampenkurzschluesse (explizit) vom LM2 lesen
- [STATUS_LAMPEN_KURZSCHLUSS_WIEDERHOL_COUNTER](#job-status-lampen-kurzschluss-wiederhol-counter) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $21 Lampenkurzschluss Wiederholzaehler auslesen Status Lampenkurzschlusswiederholzaehler (explizit) vom LM2 lesen
- [STATUS_LAMPEN_KURZSCHLUSS_COUNTER](#job-status-lampen-kurzschluss-counter) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $22 Lampenkurzschluss Zaehler auslesen Status Lampenkurzschlusszaehler (explizit) von LM lesen
- [STATUS_LAMPEN_KURZSCHLUSS_COUNTER_MAX](#job-status-lampen-kurzschluss-counter-max) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $23 Lampenkurzschluss Zaehler Maxwert auslesen Status des max. Wertes des Lampenkurzschlusszaehlers (explizit) vom LM2 lesen
- [STEUERN_SMC_BESTROMEN](#job-steuern-smc-bestromen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1A SMC bestromen Status von LM-II schreiben Bestromung der SMCs einschalten
- [STEUERN_REFERENZLAUF_ALC_SYSTEM](#job-steuern-referenzlauf-alc-system) - Referenzlauf der SMCs starten KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $42 Referenzlauf starten
- [STATUS_REFERENZLAUF_ALC_SYSTEM](#job-status-referenzlauf-alc-system) - Pruefung, ob ALC-System referenziert ist KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht $41 Pos LWR
- [_CODIERDATEN_SMC_BLOCK_SCHREIBEN_LEAR](#job-codierdaten-smc-block-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier $xxxx Codierdaten schreiben Modus  : Codieren je nach Block
- [_CODIERDATEN_SMC_SCHREIBEN_LEAR](#job-codierdaten-smc-schreiben-lear) - Beschreiben der Default-Codierdaten KWP 2000:$A6 LINGateway $2E WriteDataByCommonIdentifier $32xx Codierdaten SMC links schreiben $33xx Codierdaten SMC rechts schreiben Modus  : Default
- [_CODIERDATEN_SMC_BLOCK_LESEN_LEAR](#job-codierdaten-smc-block-lesen-lear) - Auslesen der Codierdaten fuer einen Block KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x32xx Codierdaten SMC links schreiben $0x33xx Codierdaten SMC rechts schreiben Modus  : Default
- [_CODIERDATEN_SMC_LINKS_LESEN_KOMPLETT_LEAR](#job-codierdaten-smc-links-lesen-komplett-lear) - Auslesen der kompletten Codierdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $32xx Codierdaten SMC links lesen Modus  : Default
- [_CODIERDATEN_SMC_RECHTS_LESEN_KOMPLETT_LEAR](#job-codierdaten-smc-rechts-lesen-komplett-lear) - Auslesen der kompletten Codierdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $33xx Codierdaten SMC rechts lesen Modus  : Default
- [VIN_SMC_LINKS_SCHREIBEN_LEAR](#job-vin-smc-links-schreiben-lear) - Schreiben der VIN in die linke SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN Schreiben der Fahrgestellnummer in die linke SMC
- [VIN_SMC_RECHTS_SCHREIBEN_LEAR](#job-vin-smc-rechts-schreiben-lear) - Schreiben der VIN in die rechte SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN Schreiben der Fahrgestellnummer in die rechte SMC
- [VIN_SMC_LESEN](#job-vin-smc-lesen) - Fahrgestellnummer fuer SMC links und rechts lesen Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [ID_SMC_LESEN](#job-id-smc-lesen) - ID-SMC lesen Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-SMC Modus  : Default Auslesen der Identdaten der SMCs
- [STEUERN_REFERENZLAUF_SMC](#job-steuern-referenzlauf-smc) - Referenzlauf der SMC starten KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $42 Referenzlauf starten
- [STATUS_POSITION_SMC](#job-status-position-smc) - IST-Position der SMC auslesen KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht $41 Pos LWR
- [STEUERN_POSITION_SMC](#job-steuern-position-smc) - bestimmte Position der SMC anfahren KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht starten $41 Pos LWR starten
- [SMC_SPEICHER_LESEN_LEAR](#job-smc-speicher-lesen-lear) - Speicher lesen KWP 2000: $A6 LINGateway $23 ReadMemoryByAddress Modus  : Default
- [SMC_SPEICHER_SCHREIBEN_LEAR](#job-smc-speicher-schreiben-lear) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Start-Adresse Datenbyte KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [_HERSTELLERDATEN_SMC_LEAR_SCHREIBEN](#job-herstellerdaten-smc-lear-schreiben) - Beschreiben der LEAR-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [_HERSTELLERDATEN_SMC_LEAR_LESEN](#job-herstellerdaten-smc-lear-lesen) - Auslesen der LEAR-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3280 Herstellerdaten SMC links lesen $0x3380 HErstellerdaten SMC rechts lesen Modus  : Default
- [HERSTELLERDATEN_SMC_SCHEINWERFER_SCHREIBEN](#job-herstellerdaten-smc-scheinwerfer-schreiben) - Beschreiben der Scheinwerfer-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [HERSTELLERDATEN_SMC_SCHEINWERFER_LESEN](#job-herstellerdaten-smc-scheinwerfer-lesen) - Auslesen der Scheinwerfer-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Herstellerdaten SMC links lesen $0x3381 HErstellerdaten SMC rechts lesen Modus  : Default
- [IS_LESEN_SMC_L_LEAR](#job-is-lesen-smc-l-lear) - Infospeicher von SMC links lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_SMC_R_LEAR](#job-is-lesen-smc-r-lear) - Infospeicher von SMC rechts lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL_SMC_L_LEAR](#job-is-lesen-detail-smc-l-lear) - Infospeicher Details von SMC links lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [IS_LESEN_DETAIL_SMC_R_LEAR](#job-is-lesen-detail-smc-r-lear) - Infospeicher Details von SMC rechts lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [IS_LOESCHEN_SMC_L_LEAR](#job-is-loeschen-smc-l-lear) - Infospeicher der SMC links loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [IS_LOESCHEN_SMC_R_LEAR](#job-is-loeschen-smc-r-lear) - Infospeicher der SMC rechts loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [STATUS_BETR_H_SMC](#job-status-betr-h-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $51 Betriebsstunden Betriebsstunden von ausgewaehlter SMC lesen
- [STEUERN_BETR_H_SMC_LOESCHEN](#job-steuern-betr-h-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $51 Betriebsstunden alle Betriebszeiten der ausgewaehlten SMC loeschen
- [STATUS_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC](#job-status-verteilung-winkel-ansteuerung-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $50 Verteilung der Winkelansteuerung Verteilung der Winkelansteuerung von ausgewaehlter SMC lesen
- [STEUERN_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC_LOESCHEN](#job-steuern-verteilung-winkel-ansteuerung-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $50 Verteilung der Winkelansteuerung Loeschen der Verteilung der Winkelansteuerung der ausgewaehlten SMC
- [STATUS_TEMPERATURVERTEILUNG_SMC](#job-status-temperaturverteilung-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $52 Temperaturverteilung Temperaturverteilung von der ausgewaehlten SMC lesen
- [STEUERN_TEMPERATURVERTEILUNG_SMC_LOESCHEN](#job-steuern-temperaturverteilung-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $52 Temperaturverteilung Loeschen der Temperaturverteilung der ausgewaehlten SMC
- [STATUS_SCHRITTVERLUSTE_SMC](#job-status-schrittverluste-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $53 Schrittverluste Schrittverluste von der ausgewaehlten SMC lesen
- [STEUERN_SCHRITTVERLUSTE_SMC_LOESCHEN](#job-steuern-schrittverluste-smc-loeschen) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $53 Schrittverluste Loeschen der Schrittverluste der ausgewaehlten SMC
- [STATUS_HW_EINGANGE_SMC](#job-status-hw-eingange-smc) - KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $54 HW_Eingaenge HW_Eingaenge von der ausgewaehlten SMC lesen
- [_HERSTELLERTEST_SMC_LEAR](#job-herstellertest-smc-lear) - Herstellertest KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $04 Herstellertest Modus  : Default
- [SCHEINWERFERHERSTELLERDATEN_SCHREIBEN](#job-scheinwerferherstellerdaten-schreiben) - Beschreiben der Scheinwerfer-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [SCHEINWERFERHERSTELLERDATEN_LESEN](#job-scheinwerferherstellerdaten-lesen) - Auslesen der Scheinwerfer-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Herstellerdaten SMC links lesen $0x3381 HErstellerdaten SMC rechts lesen Modus  : Default
- [PRUEFSTEMPEL_SCHEINWERFER_SCHREIBEN](#job-pruefstempel-scheinwerfer-schreiben) - Beschreiben des Scheinwerfer-Pruefstempel KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [PRUEFSTEMPEL_SCHEINWERFER_LESEN](#job-pruefstempel-scheinwerfer-lesen) - Auslesen der Scheinwerfer-Pruefstempel KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Scheinwerfer-Pruefstempel SMC links lesen $0x3381 Scheinwerfer-Pruefstempel SMC rechts lesen Modus  : Default
- [_READ_DIAG_RINGSPEICHER_LEAR](#job-read-diag-ringspeicher-lear) - KWP 2000: $21 ReadDataByLocalIdentifier $0B DIAG_RINGSPEICHER Modus   : Default
- [_CLR_DIAG_RINGSPEICHER_LEAR](#job-clr-diag-ringspeicher-lear) - KWP2000: $3B WriteDataByLocalIdentifier $0B DIAG_RINGSPEICHER Modus  : Default

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

<a id="job-status-digital-inputs"></a>
### STATUS_DIGITAL_INPUTS

Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $01 Digitale Inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHALTER_LICHT_2_RED_EIN | int | Lichtschalterstellung 2 Redundant ein |
| STAT_EINGANG_R_GANG_EIN | int | Rueckwaertsgang ein |
| STAT_EINGANG_BLS_EIN | int | Bremslichtschalter ein |
| STAT_SCHALTER_FLC_EIN | int | Schalter Fahrlichtkontrolle ein |
| STAT_KLEMME_15_EIN | int | Klemme 15 ein |
| STAT_TASTER_WBL_EIN | int | Taster Warnblinklicht betaetigt |
| STAT_SZL_BLK_R_EIN | int | SZL BLK-Rechts ein |
| STAT_SZL_BLK_L_EIN | int | SZL BLK-Links ein |
| STAT_SZL_LH_EIN | int | SZL LH ein |
| STAT_SCHALTER_FRA_RECHTS_DAUER_EIN | int | Dauer-Schalter Fahrtrichtungsanzeiger rechts ein |
| STAT_SCHALTER_FRA_RECHTS_TIPP_EIN | int | Tipp-Schalter Fahrtrichtungsanzeiger rechts ein |
| STAT_SCHALTER_FRA_LINKS_DAUER_EIN | int | Dauer-Schalter Fahrtrichtungsanzeiger links ein |
| STAT_SCHALTER_FRA_LINKS_TIPP_EIN | int | Tipp-Schalter Fahrtrichtungsanzeiger links ein |
| STAT_SCHALTER_FL_EIN | int | Schalter Fernlicht ein |
| STAT_SCHALTER_LH_EIN | int | Taster Lichthupe ein |
| STAT_TASTER_NSW_EIN | int | Taster Nebelscheinwerfer betaetigt |
| STAT_TASTER_NSL_EIN | int | Taster Nebelschlussleuchte betaetigt |
| STAT_SCHALTER_SL_EIN | int | Schalter Standlicht ein |
| STAT_SCHALTER_AL_EIN | int | Schalter Abblendlicht ein |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-inputs"></a>
### STATUS_ANALOG_INPUTS

Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 Analoge Inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPANNUNG_KLEMME_30A_WERT | real | Spannung Klemme 30A Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_KLEMME_30B_WERT | real | Spannung Klemme 30B Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_TASTER_NSW_WERT | real | Spannung Taster NSW Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_BELADUNGSSENSOR_HINTEN_WERT | real | Spannung Hoehenstandssensor hinten Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_TASTER_NSL_WERT | real | Spannung Taster NSL Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_BELADUNGSSENSOR_VORN_WERT | real | Spannung Hoehenstandssensor vorne Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_LICHT_1_WERT | real | Spannung Lichtschalterstellung 1 (Standlicht) Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_RESERVE_1_WERT | real | Reserve Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_SCHALTER_LICHT_2_WERT | real | Spannung Lichtschalterstellung 2 (Abblendlicht) Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_SZL_WERT | real | Spannung Schalter SZL links Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_LWR_POTI_WERT | real | Spannung LWR-Poti Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_DIMMER_POTI_WERT | real | Spannung Dimmer-Poti Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dimmwert"></a>
### STATUS_DIMMWERT

KWP2000: $30-&gt;IOCBLI $08-&gt;Auslesen der analogen Stati (%) aller Lampen $01-&gt;RCS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSGANG_FL_LINKS_WERT | real | Fernlicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FL_RECHTS_WERT | real | Fernlicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_AL_LINKS_WERT | real | Abblendlicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_AL_RECHTS_WERT | real | Abblendlicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BEGRL_LINKS_WERT | real | Begrenzungslicht links (E60, E65), aussen (E60-Halogen) Zusatzfahrtrichtungsanzeiger links (E63, E64 ab 09/07) Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BEGRL_RECHTS_WERT | real | Begrenzungslicht rechts (E60, E65), aussen (E60-Halogen) Zusatzfahrtrichtungsanzeiger rechts (E63, E64 ab 09/07) Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_NSW_LINKS_WERT | real | Nebelscheinwerfer links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_NSW_RECHTS_WERT | real | Nebelscheinwerfer rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FRA_LINKS_VORN_WERT | real | Fahrtrichtungsanzeiger links vorne Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FRA_RECHTS_VORN_WERT | real | Fahrtrichtungsanzeiger rechts vorne Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FRA_LINKS_HINTEN_WERT | real | Fahrtrichtungsanzeiger links hinten Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FRA_RECHTS_HINTEN_WERT | real | Fahrtrichtungsanzeiger rechts hinten Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BREMSLICHT_LINKS_WERT | real | Bremslicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BREMSLICHT_MITTE_WERT | real | Bremslicht mitte Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BREMSLICHT_RECHTS_WERT | real | Bremslicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_SL_BL_LINKS_1_WERT | real | Schlusslicht links 1 Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_SL_BL_RECHTS_1_WERT | real | Schlusslicht rechts 1 Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_SL_BL_LINKS_2_WERT | real | Schlusslicht links 2 Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_SL_BL_RECHTS_2_WERT | real | Schlusslicht rechts 2 Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_KZL_L_WERT | real | Kennzeichenlicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_KZL_R_WERT | real | Kennzeichenlicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_NSL_LINKS_WERT | real | Nebelschlusslicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_NSL_RECHTS_WERT | real | Nebelschlusslicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_RFL_LINKS_WERT | real | Rueckfahrlicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_RFL_RECHTS_WERT | real | Rueckfahrlicht rechts Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FRA_LINKS_VORN_2_WERT | real | Fahrtrichtungsanzeiger links vorne 2 Schlusslicht/Bremslicht links 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FRA_RECHTS_VORN_2_WERT | real | Fahrtrichtungsanzeiger rechts vorne 2 Schlusslicht/Bremslicht rechts 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_DRL_LINKS_WERT | real | Tagfahrlicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_DRL_RECHTS_WERT | real | Tagfahrlicht links Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_KL_58G_WERT | real | KL_58G Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_SML_WERT | real | Seitenmarkierungsleuchte Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_BIX_WERT | real | Bixenonklappe Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_FLC_LED_WERT | real | FLC_LED Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_WBL_WERT | real | Warnblinktasterbeleuchtung Bereich von 0 [%] bis 100 [%] |
| STAT_AUSGANG_DIMMWERT_EINH | string | Einheit fuer Dimmwert |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-digital"></a>
### STATUS_LAMPEN_DIGITAL

KWP2000: $30-&gt;IOCBLI $08-&gt;Auslesen der digitalen Stati (EIN/AUS) aller Lampen $01-&gt;RCS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSGANG_FL_LINKS_EIN | int | Fernlicht links |
| STAT_AUSGANG_FL_RECHTS_EIN | int | Fernlicht rechts |
| STAT_AUSGANG_AL_LINKS_EIN | int | Abblendlicht links |
| STAT_AUSGANG_AL_RECHTS_EIN | int | Abblendlicht rechts |
| STAT_AUSGANG_BEGRL_LINKS_EIN | int | Begrenzungslicht links (E60, E65), aussen (E60-Halogen) Zusatzfahrtrichtungsanzeiger links (E63, E64 ab 09/07) |
| STAT_AUSGANG_BEGRL_RECHTS_EIN | int | Begrenzungslicht rechts (E60, E65), aussen (E60-Halogen) Zusatzfahrtrichtungsanzeiger rechts (E63, E64 ab 09/07) |
| STAT_AUSGANG_NSW_LINKS_EIN | int | Nebelscheinwerfer links |
| STAT_AUSGANG_NSW_RECHTS_EIN | int | Nebelscheinwerfer rechts |
| STAT_AUSGANG_FRA_LINKS_VORN_EIN | int | Fahrtrichtungsanzeiger links vorne |
| STAT_AUSGANG_FRA_RECHTS_VORN_EIN | int | Fahrtrichtungsanzeiger rechts vorne |
| STAT_AUSGANG_FRA_LINKS_HINTEN_EIN | int | Fahrtrichtungsanzeiger links hinten |
| STAT_AUSGANG_FRA_RECHTS_HINTEN_EIN | int | Fahrtrichtungsanzeiger rechts hinten |
| STAT_AUSGANG_BREMSLICHT_LINKS_EIN | int | Bremslicht links |
| STAT_AUSGANG_BREMSLICHT_MITTE_EIN | int | Bremslicht mitte |
| STAT_AUSGANG_BREMSLICHT_RECHTS_EIN | int | Bremslicht rechts |
| STAT_AUSGANG_SL_BL_LINKS_1_EIN | int | Schlusslicht links 1 |
| STAT_AUSGANG_SL_BL_RECHTS_1_EIN | int | Schlusslicht rechts 1 |
| STAT_AUSGANG_SL_BL_LINKS_2_EIN | int | Schlusslicht links 2 |
| STAT_AUSGANG_SL_BL_RECHTS_2_EIN | int | Schlusslicht rechts 2 |
| STAT_AUSGANG_KZL_L_EIN | int | Kennzeichenlicht links |
| STAT_AUSGANG_KZL_R_EIN | int | Kennzeichenlicht rechts |
| STAT_AUSGANG_NSL_LINKS_EIN | int | Nebelschlusslicht links |
| STAT_AUSGANG_NSL_RECHTS_EIN | int | Nebelschlusslicht rechts |
| STAT_AUSGANG_RFL_LINKS_EIN | int | Rueckfahrlicht links |
| STAT_AUSGANG_RFL_RECHTS_EIN | int | Rueckfahrlicht rechts |
| STAT_AUSGANG_FRA_LINKS_VORN_2_EIN | int | Fahrtrichtungsanzeiger links vorne 2 Schlusslicht/Bremslicht links 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) |
| STAT_AUSGANG_FRA_RECHTS_VORN_2_EIN | int | Fahrtrichtungsanzeiger rechts vorne 2 Schlusslicht/Bremslicht rechts 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) |
| STAT_AUSGANG_DRL_LINKS_EIN | int | Tagfahrlicht links |
| STAT_AUSGANG_DRL_RECHTS_EIN | int | Tagfahrlicht rechts |
| STAT_AUSGANG_KL_58G_EIN | int | KL_58G |
| STAT_AUSGANG_SML_EIN | int | Seitenmarkierungsleuchte |
| STAT_AUSGANG_BIX_EIN | int | Bixenonklappe |
| STAT_AUSGANG_FLC_LED_EIN | int | FLC_LED |
| STAT_AUSGANG_WBL_EIN | int | Warnblinktasterbeleuchtung |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sense-lesen"></a>
### STATUS_SENSE_LESEN

Senseausgang fuer ausgewaehlte Lampe lesen, FRMFA KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $17 Sensewerte lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table LampNrTexte NAME TEXT Auswahl, welche Lampe geprueft werden soll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAMPE | string | ausgewaehlte Lampe |
| STAT_SENSE_WERT_EIN_1 | unsigned char | Sensewert bei eingeschalteter Lampe |
| STAT_SENSE_WERT_EIN_2 | unsigned char | Sensewert bei eingeschalteter Lampe |
| STAT_SENSE_WERT_EIN_3 | unsigned char | Sensewert bei eingeschalteter Lampe |
| STAT_SENSE_WERT_AUS_1 | unsigned char | Sensewert bei ausgeschalteter Lampe |
| STAT_SENSE_WERT_AUS_2 | unsigned char | Sensewert bei ausgeschalteter Lampe |
| STAT_SENSE_WERT_AUS_3 | unsigned char | Sensewert bei ausgeschalteter Lampe |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-defekte"></a>
### STATUS_LAMPEN_DEFEKTE

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $27 Lampenfehler auslesen Status Defektbits (explizit) von LM-II lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSGANG_FL_LINKS_DEFEKTE | int | Fernlicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FL_RECHTS_DEFEKTE | int | Fernlicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_AL_LINKS_DEFEKTE | int | Abblendlicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_AL_RECHTS_DEFEKTE | int | Abblendlicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BEGRL_LINKS_DEFEKTE | int | Begrenzungslicht links (E60, E65), aussen (E60-Halogen) Zusatzfahrtrichtungsanzeiger links (E63, E64 ab 09/07) table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BEGRL_RECHTS_DEFEKTE | int | Begrenzungslicht rechts (E60, E65), aussen (E60-Halogen) Zusatzfahrtrichtungsanzeiger rechts (E63, E64 ab 09/07) table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_NSW_LINKS_DEFEKTE | int | Nebelscheinwerfer links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_NSW_RECHTS_DEFEKTE | int | Nebelscheinwerfer rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FRA_LINKS_VORN_DEFEKTE | int | Fahrtrichtungsanzeiger links vorne table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FRA_RECHTS_VORN_DEFEKTE | int | Fahrtrichtungsanzeiger rechts vorne table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FRA_LINKS_HINTEN_DEFEKTE | int | Fahrtrichtungsanzeiger links hinten table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FRA_RECHTS_HINTEN_DEFEKTE | int | Fahrtrichtungsanzeiger rechts hinten table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BREMSLICHT_LINKS_DEFEKTE | int | Bremslicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BREMSLICHT_MITTE_DEFEKTE | int | Bremslicht mitte table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_BREMSLICHT_RECHTS_DEFEKTE | int | Bremslicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_SL_BL_LINKS_1_DEFEKTE | int | Schlusslicht links 1 table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_SL_BL_RECHTS_1_DEFEKTE | int | Schlusslicht rechts 1 table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_SL_BL_LINKS_2_DEFEKTE | int | Schlusslicht links 2 table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_SL_BL_RECHTS_2_DEFEKTE | int | Schlusslicht rechts 2 table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_KZL_L_DEFEKTE | int | Kennzeichenlicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_KZL_R_DEFEKTE | int | Kennzeichenlicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_NSL_LINKS_DEFEKTE | int | Nebelschlusslicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_NSL_RECHTS_DEFEKTE | int | Nebelschlusslicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_RFL_LINKS_DEFEKTE | int | Rueckfahrlicht links table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_RFL_RECHTS_DEFEKTE | int | Rueckfahrlicht rechts table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FRA_LINKS_VORN_2_DEFEKTE | int | Fahrtrichtungsanzeiger links vorne 2 Schlusslicht/Bremslicht links 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_FRA_RECHTS_VORN_2_DEFEKTE | int | Fahrtrichtungsanzeiger rechts vorne 2 Schlusslicht/Bremslicht rechts 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_DRL_LINKS_DEFEKTE | int | Beleuchtung WBL-Taster table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_DRL_RECHTS_DEFEKTE | int | LED Fahrtlichtkontrolle table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_KL58G_DEFEKTE | int | Klemme 58G table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| STAT_AUSGANG_SML_DEFEKTE | int | Seitenmarkierungsleuchte table STATUS_LAMPEN_DEFEKTE STATUS_DEFEKTE_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-flc-fla-ahl"></a>
### STATUS_FLC_FLA_AHL

Auslesen spezieller Stati KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $28 Stati fuer FLC, FLA und AHL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FLC_AKTIV | int | Licht ist ueber Status Fahrlicht eingeschaltet |
| STAT_FLA_AKTIV | int | Fernlichtassistent ist aktiv |
| STAT_FL_WEGEN_FLA_AKTIV | int | Fernlicht (BiXenon) aufgrund von Fernlichtassistent ist aktiv |
| STAT_AHL_AKTIV | int | AHL ist aktiv, d.h. Auswirkung von Lenkwinkel und Gierrate |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrzeugneigung"></a>
### STATUS_FAHRZEUGNEIGUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2A STATUS_FAHRZEUGNEIGUNG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FAHRZEUGNEIGUNG | real | Fahrzeugneigung auslesen |
| STAT_FAHRZEUGNEIGUNG_EINH | string | Einheit fuer Fahrzeugneigung [Grad] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampe-ein-sense-lesen-lear"></a>
### _STATUS_LAMPE_EIN_SENSE_LESEN_LEAR

Senseausgang fuer ausgewaehlte Lampe lesen, FRMFA KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $2D Lampe ein Sensewerte lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table LampNrTexte NAME TEXT Auswahl, welche Lampe geprueft werden soll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAMPE | string | ausgewaehlte Lampe |
| STAT_SENSE_WERT | unsigned char | Sensewert bei eingeschalteter Lampe |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lampen-digital"></a>
### STEUERN_LAMPEN_DIGITAL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Dimmwert an PWM-Port Status von LM-II schreiben Ausgewaehlte Lampe voll ein bzw. ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table LampNrTexte NAME TEXT Lampe aus Tabelle auswaehlen |
| AUSGANG_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lampen-pwm"></a>
### STEUERN_LAMPEN_PWM

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Dimmwert an PWM-Port Status von LM-II schreiben Lampe mit Prozentwert ein- bzw. ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table LampNrTexte NAME TEXT Lampe aus Tabelle auswaehlen |
| PWM_WERT | int | 0 bis 100 Prozent Einschaltdauer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-al-einschalten"></a>
### STEUERN_AL_EINSCHALTEN

Abblendlicht ueber Diagnose ein- bzw. ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0F Abblendlicht ein- bzw. ausschalten Status von LM-II schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AL_EIN_AUS | string | Werte: ein, aus table DigitalArgument TEXT |
| AL_ZEIT | int | Werte: 0 bis 254 Einheit: secons Optional argument, by default is 15 sec. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lampen-funktionen-einschalten"></a>
### STEUERN_LAMPEN_FUNKTIONEN_EINSCHALTEN

Lampenfunktionen ueber Diagnose ein- bzw. ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $29 Lampenfunktionen ein- bzw. ausschalten Status von LM-II schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_LAMPEN_FUNKTION | string | Werte: ein, aus table Lampenfunktion TEXT |
| LAMPEN_EIN_AUS | string | Werte: ein, aus table DigitalArgument TEXT |
| EINSCHALT_ZEIT | int | Werte: 0 bis 254 Einheit: secons Optional argument, by default is 15 sec. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bfd-stufe"></a>
### STEUERN_BFD_STUFE

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $24 BFD-Stufe ein-/ausschalten Status von LM II schreiben Ausgewaehlte BFD-Stufe ein bzw. ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table BFDStufeTexte NAME TEXT BFD-Stufe aus Tabelle auswaehlen |
| AUSGANG_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-position-lwr"></a>
### STEUERN_POSITION_LWR

bestimmte Position der LWR anfahren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $09 Position der LWR anfahren Status von LM II schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POS_LWR | long | Winkel fuer LWR Einstellung in 1/100 Grad max. bzw. min. kann mit STATUS_LWR_LESEN ausgelesen werden |
| AUSGANG_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-lampen-pre-drive-check"></a>
### START_LAMPEN_PRE_DRIVE_CHECK

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $2B Start des Pre-Drive-Checks der Lampen Status von LM2 schreiben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sleepmode-fertigung-lear"></a>
### _STEUERN_SLEEPMODE_FERTIGUNG_LEAR

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $2C Sleepmode Fertigung Status von LM-II schreiben sofortiger Sleepmode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-lesen"></a>
### C_FA_LESEN

Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | Daten des Fahrzeugauftrages |
| SPEICHER_STATUS | string | BELEGT bzw. UNBELEGT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-schreiben"></a>
### C_FA_SCHREIBEN

Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-auftrag"></a>
### C_FA_AUFTRAG

Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-fvin"></a>
### READ_FVIN

liest die lange Fahrgestellnummer KWP 2000: $22 ReadDataByCommonIdentifier $1010 FVIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FVIN | string | lange Fahrgestellnummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-fvin"></a>
### WRITE_FVIN

schreibt die lange Fahrgestellnummer KWP 2000: $2E WriteDataByCommonIdentifier $1010 FVIN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FVIN | string | lange Fahrgestellnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fvin-auftrag"></a>
### FVIN_AUFTRAG

lange Fahrgestellnummer schreiben und ruecklesen KWP 2000: $2E WriteDataByCommonIdentifier $1010 FVIN KWP 2000: $22 ReadDataByCommonIdentifier $1010 FVIN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FVIN | string | lange Fahrgestellnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-codierdaten-block-lesen-lear"></a>
### _CODIERDATEN_BLOCK_LESEN_LEAR

KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | string | Bereich: 0x30xx bis 0x34xx |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | binary | Codierdaten fuer angegebenen Block |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-block-schreiben-lear"></a>
### _CODIERDATEN_BLOCK_SCHREIBEN_LEAR

Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $xxxx Codierdaten Modus  : Codieren je nach Block

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | string | Block+Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3400-lesen-komplett-lear"></a>
### _CODIERDATEN_3400_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten im 3400-Bereich Auslesen der LM2-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_FRMFA | string | die kompletten Codierdaten im 3400-Bereich (LM2) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3000-lesen-komplett-lear"></a>
### _CODIERDATEN_3000_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten im 3000-Bereich Auslesen der ALC-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_ALC | string | die kompletten Codierdaten im 3000-Bereich (ALC) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3400-schreiben-aus-datei-lear"></a>
### _CODIERDATEN_3400_SCHREIBEN_AUS_DATEI_LEAR

Beschreiben der Default-Codierdaten Beschreiben der LM2-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $34xx Codierdaten, Default Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit Default-Codierdaten fuer 3400-Bereich Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |
| WARTEZEIT_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-komplett-schreiben-lear"></a>
### _CODIERDATEN_KOMPLETT_SCHREIBEN_LEAR

Beschreiben der Default-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten AHL schreiben $31xx Codierdaten Code schreiben $32xx Codierdaten SMC_L schreiben $33xx Codierdaten SMC_R schreiben $34xx Codierdaten LM2 schreiben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit Default-Codierdaten Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |
| WARTEZEIT_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-link-date-time-lear"></a>
### _READ_LINK_DATE_TIME_LEAR

Auslesen der Linkdate und -time KWP2000: $21 ReadDataByLocalIdentifier $01 Linkdate und -time

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_LINK_DATE_APP | string | Linkdatum fuer Applikation |
| SW_LINK_DATE_BOOT | string | Linkdatum fuer Bootloader |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-emergency-fallback-counter-lear"></a>
### _READ_EMERGENCY_FALLBACK_COUNTER_LEAR

Auslesen der Fallback Counter KWP2000: $21 ReadDataByLocalIdentifier $02 Fallback Counter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CME_COUNTER | int | gibt an wie oft der CME als Notlauf-Fallback zugeschlagen hat |
| CRG_PLL_LOCK_COUNTER | int | gibt an wie oft der CRG_PLL_LOCK als Notlauf-Fallback zugeschlagen hat |
| SCME_COUNTER | int | gibt an wie oft der SCME als Notlauf-Fallback zugeschlagen hat |
| ILLEGAL_OPCODE_COUNTER | int | gibt an wie oft der ILLEGAL_OPCODE als Notlauf-Fallback zugeschlagen hat |
| SWI_COUNTER | int | gibt an wie oft der SWI als Notlauf-Fallback zugeschlagen hat |
| XIRQ_COUNTER | int | gibt an wie oft der XIRQ als Notlauf-Fallback zugeschlagen hat |
| XGATE_COUNTER | int | Fehlerzaehler fuer das X-Gate |
| STACK_COUNTER | int | Fehlerzaehler fuer das Stack |
| LVI_COUNTER | int | Fehlerzaehler fuer das low voltage interrupt |
| COP_COUNTER | int | Fehlerzaehler fuer das watchdog |
| ADDR_ILLEGAL_COUNTER | int | Fehlerzaehler fuer das illegal address violation |
| SPURIOUS_COUNTER | int | Fehlerzaehler fuer das spurious interrupt |
| INVALID_INT_COUNTER | int | Fehlerzaehler fuer das invalid interrupt |
| RESET_COUNTER | int | Reset Counter |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-clr-emergency-fallback-counter-lear"></a>
### _CLR_EMERGENCY_FALLBACK_COUNTER_LEAR

KWP2000: $3B WriteDataByLocalIdentifier $02 NOTLAUF_FALLBACK_COUNTER Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-abs-timer-lear"></a>
### _READ_ABS_TIMER_LEAR

Auslesen der Fallback Counter KWP2000: $21 ReadDataByLocalIdentifier $09 ABS_TIMER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ABS_TIMER | long | gibt den absoluten Laufzeittimer in Sekunden an |
| STAT_ABS_TIMER_EINH | string | Einheit fuer ABS_TIMER: Sekunden |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-clr-abs-timer-lear"></a>
### _CLR_ABS_TIMER_LEAR

KWP2000: $3B WriteDataByLocalIdentifier $09 ABS_TIMER Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hersteller-daten-lesen-lear"></a>
### _HERSTELLER_DATEN_LESEN_LEAR

Auslesen der Herstellerdaten KWP2000: $21 ReadDataByLocalIdentifier $04 Herstellerdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HERSTELLERDATEN | binary | Herstellerdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hersteller-daten-schreiben-lear"></a>
### _HERSTELLER_DATEN_SCHREIBEN_LEAR

Beschreiben der Codierdaten je nach Block KWP2000: $3B WriteDataByLocalIdentifier $04 Herstellerdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HERSTELLERDATEN | string | Herstellerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lwr-lesen"></a>
### STATUS_LWR_LESEN

Unterscheidung zwischen dynamischer, automatischer und manueller LWR KWP2000: $21 ReadDataByLocalIdentifier $05 LWR lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEINE_LWR | unsigned char | 0 oder 1, ob LWR aktiv bei Kurvenlicht immer 1 |
| STAT_DYN_LWR | unsigned char | 0 oder 1, ob dynamisch LWR aktiv |
| STAT_AUT_LWR | unsigned char | 0 oder 1, ob automatische LWR aktiv |
| STAT_MAN_LWR | unsigned char | 0 oder 1, ob manuelle LWR aktiv |
| STAT_LWR_MIN | int | Kleinste Schrittmotorposition |
| STAT_LWR_MAX | int | Groesste Schrittmotorposition |
| STAT_LWR_SCHRITTE_REF_LAUF | int | Schrittanzahl fuer den Referenzlauf |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-energy-saving-mode-lear"></a>
### _READ_ENERGY_SAVING_MODE_LEAR

Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ENERGY_SAVING_MODE | string | Ausgabe des Engery-Saving-Modes table EnergySaving NAME TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbd-zeichn-index-lesen-lear"></a>
### _CBD_ZEICHN_INDEX_LESEN_LEAR

Auslesen des Aenderungsindex aus den Codierdaten KWP2000: $21 ReadDataByLocalIdentifier $06 CBD_ZEICHN_INDEX lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CBD_ZEICHN_INDEX | string | Aenderungsindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sense-inputs"></a>
### STATUS_SENSE_INPUTS

Auslesen der Sensewerte der einzelnen Lampen KWP2000: $21 ReadDataByLocalIdentifier $08 Sensewerte lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SENSE_BERGL_L_WERT | real | Spannung Sensor Begrenzungslicht links (E60, E65), aussen (E60-Halogen) Spannung Sensor Zusatzfahrtrichtungsanzeiger links (E63, E64 ab 09/07) Bereich: 0 V bis 5 V |
| STAT_SENSE_BERGL_R_WERT | real | Spannung Sensor Begrenzungslicht rechts (E60, E65), aussen (E60-Halogen) Spannung Sensor Zusatzfahrtrichtungsanzeiger rechts (E63, E64 ab 09/07) Bereich: 0 V bis 5 V |
| STAT_SENSE_AL_L_WERT | real | Spannung Sensor Abblendlicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_AL_R_WERT | real | Spannung Sensor Abblendlicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_FL_L_WERT | real | Spannung Sensor Fernlicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_FL_R_WERT | real | Spannung Sensor Fernlicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_NSW_L_WERT | real | Spannung Sensor Nebelscheinwerfer links Bereich: 0 V bis 5 V |
| STAT_SENSE_NSW_R_WERT | real | Spannung Sensor Nebelscheinwerfer rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_1_SL_L_WERT | real | Spannung Sensor Standlicht 1 links Bereich: 0 V bis 5 V |
| STAT_SENSE_1_SL_R_WERT | real | Spannung Sensor Standlicht 1 rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_2_SL_L_WERT | real | Spannung Sensor Standlicht 2 links Bereich: 0 V bis 5 V |
| STAT_SENSE_2_SL_R_WERT | real | Spannung Sensor Standlicht 2 rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_RFL_L_WERT | real | Spannung Sensor Rueckfahrscheinwerfer links Bereich: 0 V bis 5 V |
| STAT_SENSE_RFL_R_WERT | real | Spannung Sensor Rueckfahrscheinwerfer rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_NSL_L_WERT | real | Spannung Sensor Nebelschlusslicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_NSL_R_WERT | real | Spannung Sensor Nebelschlusslicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_VL_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger vorne links Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_VR_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger vorne rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_HL_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger hinten links Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_HR_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger hinten rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_BL_L_WERT | real | Spannung Sensor Bremslicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_BL_R_WERT | real | Spannung Sensor Bremslicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_KZL_L_WERT | real | Spannung Sensor Kennzeichenlicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_KZL_R_WERT | real | Spannung Sensor Kennzeichenlicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_BL_M_WERT | real | Spannung Sensor Bremslicht mitte Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_VL_2_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger vorne links 2 Spannung Sensor Schlusslicht/Bremslicht links 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_VR_2_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger vorne rechts 2 Spannung Sensor Schlusslicht/Bremslicht rechts 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) Bereich: 0 V bis 5 V |
| STAT_SENSE_SML_WERT | real | Spannung Sensor Seitenmarkierungsleuchte Bereich: 0 V bis 5 V |
| STAT_SENSE_DRL_L_WERT | real | Spannung Sensor Tagfahrlicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_DRL_R_WERT | real | Spannung Sensor Tagfahrlicht rechts Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pia-daten"></a>
### STATUS_PIA_DATEN

Auslesen der momentan aktuellen Piadaten KWP2000: $21 ReadDataByLocalIdentifier $0A Piadaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FOLLOW_ME_HOME_ZEIT | int | momentan eingestellte Zeit fuer Follow Me Home |
| STAT_QUITT_BLINK_ENTRIEGELN_EIN | int | Quittierungsblinken bei Entriegeln momentan |
| STAT_QUITT_BLINK_SICHERN_EIN | int | Quittierungsblinken bei Sichern momentan |
| STAT_MIND_ANZAHL_BLINKZYKLEN_BEI_TIPP | int | Mind.-Anzahl Blinkzyklen bei Tippblinken momentan |
| STAT_TAGFAHRLICHT_EIN | int | Tagfahrlicht momentan |
| STAT_ABBIEGELICHT_EIN | int | Abbiegelicht momentan |
| STAT_WELCOMELIGHT_EIN | int | Welcomelight momentan |
| STAT_FLA_EIN | int | Fernlichtassistent momentan |
| STAT_AHL_MODE | string | momentan ausgewaehlter AHL-Mode |
| STAT_FUNKSCHLUESSEL_PROFIL | int | momentan ausgewaehltes Funkschluessel-Profil |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-brif-schreiben-lear"></a>
### _BRIF_SCHREIBEN_LEAR

Writting the BRIF in EEPROM All the arguments should be supplied KWP2000: $2E WriteDataByCommonIdentifier $34Fx BRIF Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HWREF | string | Hardware Reference Length is 7 Default value is '009FRM0' |
| PECUHN | string | Physical ECU Hardware Number Format is XX XX XX XX XX XX (6 bytes length) Default value is '00 00 01 23 45 67' |
| DOECUM | string | Date of ECU Manufacturing Format either DD.MM.YYYY or YYMMDD Default value is 15.10.2004 |
| SSI | unsigned char | System Supplier Index Range is 0x00-0xFE Default value is 09 |
| SSECUSN | string | System Supplier ECU Serial Number Length is 9 Default value is '000000001' |
| ERT | unsigned char | Erase Time Range is 0x00-0xFE Default value is 0x10 |
| SIGT | unsigned char | Signature Time Range is 0x00-0xFE Default value is 0x20 |
| RST | unsigned char | Reset Time Range is 0x00-0xFE Default value is 0x02 |
| MXBL | unsigned char | Max block length Range is 0x00-0xFE Default value is 0xF1 |
| VMECUHVN | unsigned char | Vehicle Manufacturer ECU Version Number Range is 0x00-0xFE Default value is 0x01 |
| SNOET | string | System Name Or Engine Type Format is XX XX Default value is '41 4F' |
| ZB_NR | string | ZusBau Number Format is XX XX XX XX XX XX (6 bytes length) Default value is '00 00 01 23 45 67' |
| VAR_NR | unsigned char | Variant Number Range is 0x00-0xFE Default value is 0x01 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-brif-file-lear"></a>
### _BRIF_FILE_LEAR

Writting the BRIF in EEPROM All the arguments should be supplied KWP2000: $2E WriteDataByCommonIdentifier $34Fx BRIF Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FILE_TEXT | string | Format: [Drive]:[Path]\[File].[Ext] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HWREF | string | Written Value |
| PECUHN | string | Written Value |
| DOECUM | string | Written Value |
| SSI | string | Written Value |
| SSECUSN | string | Written Value |
| ERT | string | Written Value |
| SIGT | string | Written Value |
| RST | string | Written Value |
| MXBL | string | Written Value |
| VMECUHVN | string | Written Value |
| SNOET | string | Written Value |
| UIF_ZB_NR | string | Written Value |
| VARIANT | string | Written Value |
| JOB_STATUS | string | From JobResult Table |

<a id="job-status-betr-h-funktionen"></a>
### STATUS_BETR_H_FUNKTIONEN

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $06 Betriebsstunden fuer alle Funktionen Status von LM2 lesen Lesen der Betriebsstunden der einzelnen Lampenfunktionen des LM2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSZEIT_LM2_WERT | real | Betriebsstunden FRMFA auslesen |
| STAT_BETRIEBSZEIT_FL_WERT | unsigned long | Betr_h Fernlicht |
| STAT_BETRIEBSZEIT_AL_WERT | unsigned long | Betr_h Abblendlicht |
| STAT_BETRIEBSZEIT_SL_WERT | unsigned long | Betr_h Standlicht |
| STAT_BETRIEBSZEIT_NSW_WERT | unsigned long | Betr_h Nebelscheinwerfer |
| STAT_BETRIEBSZEIT_FRA_LINKS_WERT | unsigned long | Betr_h Fahrtrichtungsanzeiger links |
| STAT_BETRIEBSZEIT_FRA_RECHTS_WERT | unsigned long | Betr_h Fahrtrichtungsanzeiger rechts |
| STAT_BETRIEBSZEIT_BL_WERT | unsigned long | Betr_h Bremslicht |
| STAT_BETRIEBSZEIT_BFD_WERT | unsigned long | Betr_h Break-Force-Display |
| STAT_BETRIEBSZEIT_NSL_WERT | unsigned long | Betr_h Nebelschlusslicht |
| STAT_BETRIEBSZEIT_RFL_WERT | unsigned long | Betr_h Rueckfahrlicht |
| STAT_BETRIEBSZEIT_PL_WERT | unsigned long | Betr_h Parklicht |
| STAT_BETRIEBSZEIT_EINH | string | Einheit fuer Betriebsstunden |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-betr-h-lm2-loeschen"></a>
### STEUERN_BETR_H_LM2_LOESCHEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $06 Betriebsstunden Status von LM2 schreiben Loeschen aller Betriebsstunden des FRM2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lwr-position"></a>
### STATUS_LWR_POSITION

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $09 STATUS_LWR_POSITION

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LWR_POSITION | int | Position der Schrittmotoren auslesen je nach Scheinwerfer max. von 0 bis 1000 Halbschritte der Arbeitspunkt haengt von Fahrzeugtyp und Scheinwerfer ab und ist kodierbar |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-xenon-al-einschaltversuche"></a>
### STATUS_XENON_AL_EINSCHALTVERSUCHE

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $14 Xenon-AL-Einschaltversuche Auslesen wie oft das Abblendlicht eingeschaltet wurde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_XENON_AL_EINSCHALTVERSUCHE | int | Xenon-AL-Einschaltversuche auslesen |
| STAT_XENON_AL_L_RESTART_VERSUCHE | int | Xenon-AL-Einschaltrestartversuche links auslesen |
| STAT_XENON_AL_R_RESTART_VERSUCHE | int | Xenon-AL-Einschaltrestartversuche rechts auslesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-xenon-al-einschaltversuche-loeschen"></a>
### STEUERN_XENON_AL_EINSCHALTVERSUCHE_LOESCHEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $14 Xenon-AL-Einschaltversuche Loeschen der AL-Einschaltversuche

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-wartezeit-lear"></a>
### _WARTEZEIT_LEAR

Wartezeit

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WARTEZEIT | unsigned char | Wartezeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-reset-kurzschluss-sperre"></a>
### _RESET_KURZSCHLUSS_SPERRE

Kurzschlusssperre ueber Diagnose ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1F Kurzschlusssperre ausschalten Status von LM2 schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LAMP_NR | unsigned int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-kurzschluss"></a>
### STATUS_LAMPEN_KURZSCHLUSS

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $20 Lampenkurzschluss auslesen Status Lampenkurzschluesse (explizit) vom LM2 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT | int | Fernlicht links SHORT_CIRCUIT ja/nein |
| STAT_FL_RECHTS_SHORT_CIRCUIT | int | Fernlicht rechts SHORT_CIRCUIT ja/nein |
| STAT_AL_LINKS_SHORT_CIRCUIT | int | Abblendlicht links SHORT_CIRCUIT ja/nein |
| STAT_AL_RECHTS_SHORT_CIRCUIT | int | Abblendlicht rechts SHORT_CIRCUIT ja/nein |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT | int | Begrenzungslicht links (E60, E65), aussen (E60-Halogen) SHORT_CIRCUIT ja/nein Zusatzfahrtrichtungsanzeiger links (E63, E64 ab 09/07) SHORT_CIRCUIT ja/nein |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT | int | Begrenzungslicht rechts (E60, E65), aussen (E60-Halogen) SHORT_CIRCUIT ja/nein Zusatzfahrtrichtungsanzeiger rechts (E63, E64 ab 09/07) SHORT_CIRCUIT ja/nein |
| STAT_NSW_LINKS_SHORT_CIRCUIT | int | Nebelscheinwerfer links SHORT_CIRCUIT ja/nein |
| STAT_NSW_RECHTS_SHORT_CIRCUIT | int | Nebelscheinwerfer rechts SHORT_CIRCUIT ja/nein |
| STAT_FRA_LINKS_VORN_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT ja/nein |
| STAT_FRA_RECHTS_VORN_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT ja/nein |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT ja/nein |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT ja/nein |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT | int | Bremslicht links SHORT_CIRCUIT ja/nein |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT | int | Bremslicht rechts SHORT_CIRCUIT ja/nein |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT | int | Bremslicht mitte SHORT_CIRCUIT ja/nein |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT | int | Schlusslicht 1 links SHORT_CIRCUIT ja/nein |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT | int | Schlusslicht 1 rechts SHORT_CIRCUIT ja/nein |
| STAT_SL_BL_LINKS_2_SHORT_CIRCUIT | int | Schlusslicht 2 links SHORT_CIRCUIT ja/nein |
| STAT_SL_BL_RECHTS_2_SHORT_CIRCUIT | int | Schlusslicht 2 rechts SHORT_CIRCUIT ja/nein |
| STAT_KZL_L_SHORT_CIRCUIT | int | Kennzeichenlicht links SHORT_CIRCUIT ja/nein |
| STAT_KZL_R_SHORT_CIRCUIT | int | Kennzeichenlicht rechts SHORT_CIRCUIT ja/nein |
| STAT_NSL_LINKS_SHORT_CIRCUIT | int | Nebelschlusslicht links SHORT_CIRCUIT ja/nein |
| STAT_NSL_RECHTS_SHORT_CIRCUIT | int | Nebelschlusslicht rechts SHORT_CIRCUIT ja/nein |
| STAT_RFL_LINKS_SHORT_CIRCUIT | int | Rueckfahrlicht links SHORT_CIRCUIT ja/nein |
| STAT_RFL_RECHTS_SHORT_CIRCUIT | int | Rueckfahrlicht rechts SHORT_CIRCUIT ja/nein |
| STAT_FRA_LINKS_VORN_2_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger links vorne 2 SHORT_CIRCUIT ja/nein Schlusslicht/Bremslicht links 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) SHORT_CIRCUIT ja/nein |
| STAT_FRA_RECHTS_VORN_2_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger rechts vorne 2 SHORT_CIRCUIT ja/nein Schlusslicht/Bremslicht rechts 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) SHORT_CIRCUIT ja/nein |
| STAT_DRL_LINKS_SHORT_CIRCUIT | int | DRL_LINKS SHORT_CIRCUIT ja/nein |
| STAT_DRL_RECHTS_SHORT_CIRCUIT | int | DRL_RECHTS SHORT_CIRCUIT ja/nein |
| STAT_SML_SHORT_CIRCUIT | int | Seitenmarkierungsleuchte SHORT_CIRCUIT ja/nein |
| STAT_KLEMME_58G_SHORT_CIRCUIT | int | Klemme 58g SHORT_CIRCUIT ja/nein |
| STAT_BIX_SHORT_CIRCUIT | int | Bi-Xenonklappe SHORT_CIRCUIT ja/nein |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-kurzschluss-wiederhol-counter"></a>
### STATUS_LAMPEN_KURZSCHLUSS_WIEDERHOL_COUNTER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $21 Lampenkurzschluss Wiederholzaehler auslesen Status Lampenkurzschlusswiederholzaehler (explizit) vom LM2 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Fernlicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_FL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Fernlicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_AL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Abblendlicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_AL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Abblendlicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Begrenzungslicht links (E60, E65), aussen (E60-Halogen) SHORT_CIRCUIT_WIEDERHOL Zusatzfahrtrichtungsanzeiger links (E63, E64 ab 09/07) SHORT_CIRCUIT_WIEDERHOL |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Begrenzungslicht rechts (E60, E65), aussen (E60-Halogen) SHORT_CIRCUIT_WIEDERHOL Zusatzfahrtrichtungsanzeiger rechts (E63, E64 ab 09/07) SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSW_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelscheinwerfer links SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSW_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelscheinwerfer rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_LINKS_VORN_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_RECHTS_VORN_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT_WIEDERHOL |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Bremslicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Bremslicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT_WIEDERHOL | int | Bremslicht mitte SHORT_CIRCUIT_WIEDERHOL |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT_WIEDERHOL | int | Schlusslicht 1 links SHORT_CIRCUIT_WIEDERHOL |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT_WIEDERHOL | int | Schlusslicht 1 rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_SL_BL_LINKS_2_SHORT_CIRCUIT_WIEDERHOL | int | Schlusslicht links 2 SHORT_CIRCUIT_WIEDERHOL |
| STAT_SL_BL_RECHTS_2_SHORT_CIRCUIT_WIEDERHOL | int | Schlusslicht rechts 2 SHORT_CIRCUIT_WIEDERHOL |
| STAT_KZL_L_SHORT_CIRCUIT_WIEDERHOL | int | Kennzeichenlicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_KZL_R_SHORT_CIRCUIT_WIEDERHOL | int | Kennzeichenlicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelschlusslicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelschlusslicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_RFL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Rueckfahrlicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_RFL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Rueckfahrlicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_LINKS_VORN_2_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger links vorne 2 SHORT_CIRCUIT_WIEDERHOL Schlusslicht/Bremslicht links 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_RECHTS_VORN_2_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger rechts vorne 2 SHORT_CIRCUIT_WIEDERHOL Schlusslicht/Bremslicht rechts 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) SHORT_CIRCUIT_WIEDERHOL |
| STAT_DRL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | DRL_LINKS SHORT_CIRCUIT_WIEDERHOL |
| STAT_DRL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | DRL_RECHTS SHORT_CIRCUIT_WIEDERHOL |
| STAT_SML_SHORT_CIRCUIT_WIEDERHOL | int | Seitenmarkierungsleuchte SHORT_CIRCUIT_WIEDERHOL |
| STAT_KLEMME_58G_SHORT_CIRCUIT_WIEDERHOL | int | Klemme 58g SHORT_CIRCUIT_WIEDERHOL |
| STAT_BIX_SHORT_CIRCUIT_WIEDERHOL | int | Bi-Xenonklappe SHORT_CIRCUIT_WIEDERHOL |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-kurzschluss-counter"></a>
### STATUS_LAMPEN_KURZSCHLUSS_COUNTER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $22 Lampenkurzschluss Zaehler auslesen Status Lampenkurzschlusszaehler (explizit) von LM lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT_COUNTER | int | Fernlicht links SHORT_CIRCUIT_COUNTER |
| STAT_FL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Fernlicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_AL_LINKS_SHORT_CIRCUIT_COUNTER | int | Abblendlicht links SHORT_CIRCUIT_COUNTER |
| STAT_AL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Abblendlicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT_COUNTER | int | Begrenzungslicht links (E60, E65), aussen (E60-Halogen) SHORT_CIRCUIT_COUNTER Zusatzfahrtrichtungsanzeiger links (E63, E64 ab 09/07) SHORT_CIRCUIT_COUNTER |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Begrenzungslicht rechts (E60, E65), aussen (E60-Halogen) SHORT_CIRCUIT_COUNTER Zusatzfahrtrichtungsanzeiger rechts (E63, E64 ab 09/07) SHORT_CIRCUIT_COUNTER |
| STAT_NSW_LINKS_SHORT_CIRCUIT_COUNTER | int | Nebelscheinwerfer links SHORT_CIRCUIT_COUNTER |
| STAT_NSW_RECHTS_SHORT_CIRCUIT_COUNTER | int | Nebelscheinwerfer rechts SHORT_CIRCUIT_COUNTER |
| STAT_FRA_LINKS_VORN_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT_COUNTER |
| STAT_FRA_RECHTS_VORN_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT_COUNTER |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT_COUNTER |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT_COUNTER |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT_COUNTER | int | Bremslicht links SHORT_CIRCUIT_COUNTER |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT_COUNTER | int | Bremslicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT_COUNTER | int | Bremslicht mitte SHORT_CIRCUIT_COUNTER |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT_COUNTER | int | Schlusslicht links 1 SHORT_CIRCUIT_COUNTER |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT_COUNTER | int | Schlusslicht rechts 1 SHORT_CIRCUIT_COUNTER |
| STAT_SL_BL_LINKS_2_SHORT_CIRCUIT_COUNTER | int | Schlusslicht links 2 SHORT_CIRCUIT_COUNTER |
| STAT_SL_BL_RECHTS_2_SHORT_CIRCUIT_COUNTER | int | Schlusslicht rechts 2 SHORT_CIRCUIT_COUNTER |
| STAT_KZL_L_SHORT_CIRCUIT_COUNTER | int | Kennzeichenlicht links SHORT_CIRCUIT_COUNTER |
| STAT_KZL_R_SHORT_CIRCUIT_COUNTER | int | Kennzeichenlicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_NSL_LINKS_SHORT_CIRCUIT_COUNTER | int | Nebelschlusslicht links SHORT_CIRCUIT_COUNTER |
| STAT_NSL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Nebelschlusslicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_RFL_LINKS_SHORT_CIRCUIT_COUNTER | int | Rueckfahrlicht links SHORT_CIRCUIT_COUNTER |
| STAT_RFL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Rueckfahrlicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_FRA_LINKS_VORN_2_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger links vorne 2 SHORT_CIRCUIT_COUNTER Schlusslicht/Bremslicht links 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) SHORT_CIRCUIT_COUNTER |
| STAT_FRA_RECHTS_VORN_2_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger rechts vorne 2 SHORT_CIRCUIT_COUNTER Schlusslicht/Bremslicht rechts 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) SHORT_CIRCUIT_COUNTER |
| STAT_DRL_LINKS_SHORT_CIRCUIT_COUNTER | int | DRL_LINKS SHORT_CIRCUIT_COUNTER |
| STAT_DRL_RECHTS_SHORT_CIRCUIT_COUNTER | int | DRL_RECHTS SHORT_CIRCUIT_COUNTER |
| STAT_SML_SHORT_CIRCUIT_COUNTER | int | Seitenmarkierungsleuchte SHORT_CIRCUIT_COUNTER |
| STAT_KLEMME_58G_SHORT_CIRCUIT_COUNTER | int | Klemme 58g SHORT_CIRCUIT_COUNTER |
| STAT_BIX_SHORT_CIRCUIT_COUNTER | int | Bi-Xenonklappe SHORT_CIRCUIT_COUNTER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-kurzschluss-counter-max"></a>
### STATUS_LAMPEN_KURZSCHLUSS_COUNTER_MAX

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $23 Lampenkurzschluss Zaehler Maxwert auslesen Status des max. Wertes des Lampenkurzschlusszaehlers (explizit) vom LM2 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Fernlicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Fernlicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_AL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Abblendlicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_AL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Abblendlicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Begrenzungslicht links (E60, E65), aussen (E60-Halogen) SHORT_CIRCUIT_COUNTER_MAX Zusatzfahrtrichtungsanzeiger links (E63, E64 ab 09/07) SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Begrenzungslicht rechts (E60, E65), aussen (E60-Halogen) SHORT_CIRCUIT_COUNTER_MAX Zusatzfahrtrichtungsanzeiger rechts (E63, E64 ab 09/07) SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSW_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelscheinwerfer links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSW_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelscheinwerfer rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_LINKS_VORN_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_RECHTS_VORN_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Bremslicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Bremslicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT_COUNTER_MAX | int | Bremslicht mitte SHORT_CIRCUIT_COUNTER_MAX |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT_COUNTER_MAX | int | Schlusslicht links 1 SHORT_CIRCUIT_COUNTER_MAX |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT_COUNTER_MAX | int | Schlusslicht rechts 1 SHORT_CIRCUIT_COUNTER_MAX |
| STAT_SL_BL_LINKS_2_SHORT_CIRCUIT_COUNTER_MAX | int | Schlusslicht links 2 SHORT_CIRCUIT_COUNTER_MAX |
| STAT_SL_BL_RECHTS_2_SHORT_CIRCUIT_COUNTER_MAX | int | Schlusslicht rechts 2 SHORT_CIRCUIT_COUNTER_MAX |
| STAT_KZL_L_SHORT_CIRCUIT_COUNTER_MAX | int | Kennzeichenlicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_KZL_R_SHORT_CIRCUIT_COUNTER_MAX | int | Kennzeichenlicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelschlusslicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelschlusslicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_RFL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Rueckfahrlicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_RFL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Rueckfahrlicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_LINKS_VORN_2_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger links vorne 2 SHORT_CIRCUIT_COUNTER_MAX Schlusslicht/Bremslicht links 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_RECHTS_VORN_2_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger rechts vorne 2 SHORT_CIRCUIT_COUNTER_MAX Schlusslicht/Bremslicht rechts 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) SHORT_CIRCUIT_COUNTER_MAX |
| STAT_DRL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | DRL_LINKS SHORT_CIRCUIT_COUNTER_MAX |
| STAT_DRL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | DRL_RECHTS SHORT_CIRCUIT_COUNTER_MAX |
| STAT_SML_SHORT_CIRCUIT_COUNTER_MAX | int | Seitenmarkierungsleuchte SHORT_CIRCUIT_COUNTER_MAX |
| STAT_KLEMME_58G_SHORT_CIRCUIT_COUNTER_MAX | int | Klemme 58g SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BIX_SHORT_CIRCUIT_COUNTER_MAX | int | Bi-Xenonklappe SHORT_CIRCUIT_COUNTER_MAX |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-smc-bestromen"></a>
### STEUERN_SMC_BESTROMEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1A SMC bestromen Status von LM-II schreiben Bestromung der SMCs einschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BESTROMEN_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-referenzlauf-alc-system"></a>
### STEUERN_REFERENZLAUF_ALC_SYSTEM

Referenzlauf der SMCs starten KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $42 Referenzlauf starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REFERENZLAUF | string | Referenzlauf fuer Kurvenlicht auswaehlen falls keiner ausgewaehlt dann wird mit Sensor ausgewaehlt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-referenzlauf-alc-system"></a>
### STATUS_REFERENZLAUF_ALC_SYSTEM

Pruefung, ob ALC-System referenziert ist KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht $41 Pos LWR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ALC_SYSTEM_REFERENZIERT_EIN | int | gibt an ob ALC-System fertig referenziert hat |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-block-schreiben-lear"></a>
### _CODIERDATEN_SMC_BLOCK_SCHREIBEN_LEAR

Beschreiben der Codierdaten je nach Block KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier $xxxx Codierdaten schreiben Modus  : Codieren je nach Block

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | string | Block+Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-schreiben-lear"></a>
### _CODIERDATEN_SMC_SCHREIBEN_LEAR

Beschreiben der Default-Codierdaten KWP 2000:$A6 LINGateway $2E WriteDataByCommonIdentifier $32xx Codierdaten SMC links schreiben $33xx Codierdaten SMC rechts schreiben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit Default-Codierdaten Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-block-lesen-lear"></a>
### _CODIERDATEN_SMC_BLOCK_LESEN_LEAR

Auslesen der Codierdaten fuer einen Block KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x32xx Codierdaten SMC links schreiben $0x33xx Codierdaten SMC rechts schreiben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | string | Bereich: 30xx und 31xx |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | string | Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-links-lesen-komplett-lear"></a>
### _CODIERDATEN_SMC_LINKS_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $32xx Codierdaten SMC links lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_1 | string | Teil 1 der kompletten Codierdaten |
| CODIERDATEN_2 | string | Teil 2 der kompletten Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-rechts-lesen-komplett-lear"></a>
### _CODIERDATEN_SMC_RECHTS_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $33xx Codierdaten SMC rechts lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_1 | string | Teil 1 der kompletten Codierdaten |
| CODIERDATEN_2 | string | Teil 2 der kompletten Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-vin-smc-links-schreiben-lear"></a>
### VIN_SMC_LINKS_SCHREIBEN_LEAR

Schreiben der VIN in die linke SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN Schreiben der Fahrgestellnummer in die linke SMC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VINDATEN | string | 7stellige Fahrgestellnummern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-vin-smc-rechts-schreiben-lear"></a>
### VIN_SMC_RECHTS_SCHREIBEN_LEAR

Schreiben der VIN in die rechte SMC KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN Schreiben der Fahrgestellnummer in die rechte SMC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VINDATEN | string | 7stellige Fahrgestellnummern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-vin-smc-lesen"></a>
### VIN_SMC_LESEN

Fahrgestellnummer fuer SMC links und rechts lesen Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| VIN_SMC_LINKS | string | Fahrgestellnummer 7-stellig fuer SMC links |
| VIN_SMC_LINKS_KONFIG | int | Konfigbyte Fahrgestellnummer fuer SMC links |
| VIN_SMC_RECHTS | string | Fahrgestellnummer 7-stellig fuer SMC rechts |
| VIN_SMC_RECHTS_KONFIG | int | Konfigbyte Fahrgestellnummer fuer SMC rechts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-id-smc-lesen"></a>
### ID_SMC_LESEN

ID-SMC lesen Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-SMC Modus  : Default Auslesen der Identdaten der SMCs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_VERSION_SMC_LINKS | string | SW-Version fuer SMC links |
| HW_VERSION_SMC_LINKS | string | HW-Version fuer SMC links |
| CODING_INDEX_SMC_LINKS | string | Codierindex fuer SMC links |
| MCV_VERSION_SMC_LINKS | string | MCV-Version fuer SMC links |
| SW_VERSION_SMC_RECHTS | string | SW-Version fuer SMC rechts |
| HW_VERSION_SMC_RECHTS | string | HW-Version fuer SMC rechts |
| CODING_INDEX_SMC_RECHTS | string | Codierindex fuer SMC rechts |
| MCV_VERSION_SMC_RECHTS | string | MCV-Version fuer SMC rechts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-referenzlauf-smc"></a>
### STEUERN_REFERENZLAUF_SMC

Referenzlauf der SMC starten KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $42 Referenzlauf starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| REFERENZLAUF | string | Referenzlauf auswaehlen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-position-smc"></a>
### STATUS_POSITION_SMC

IST-Position der SMC auslesen KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht $41 Pos LWR

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POS_KURVENLICHT | long | Winkel fuer Kurvenlicht je nach Scheinwerfer max. von -170 bis 170 entspricht -17Grad bis 17Grad |
| STAT_POS_LWR | long | Winkel fuer LWR je nach Scheinwerfer max. von 0 bis 1000 entspricht 0Grad bis 10Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-position-smc"></a>
### STEUERN_POSITION_SMC

bestimmte Position der SMC anfahren KWP2000: $A6 LINGateway $30 InputOutputByLocalIdentifier $40 Pos Kurvenlicht starten $41 Pos LWR starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| POS_KURVENLICHT | long | Winkel fuer Kurvenlicht je nach Scheinwerfer max. von -170 bis 170 entspricht -17Grad bis 17Grad |
| GESCHW_KURVENLICHT | unsigned char | Geschwindigkeit fuer Kurvenlicht je nach Scheinwerfer max. von 0 bis 31 |
| POS_LWR | long | Winkel fuer LWR je nach Scheinwerfer max. von 0 bis 1000 entspricht 0Grad bis 10Grad |
| GESCHW_LWR | unsigned char | Geschwindigkeit fuer LWR je nach Scheinwerfer max. von 0 bis 7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-smc-speicher-lesen-lear"></a>
### SMC_SPEICHER_LESEN_LEAR

Speicher lesen KWP 2000: $A6 LINGateway $23 ReadMemoryByAddress Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| ADRESSE | long | zu lesende Adresse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-smc-speicher-schreiben-lear"></a>
### SMC_SPEICHER_SCHREIBEN_LEAR

Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Start-Adresse Datenbyte KWP2000: $3D WriteMemoryByAddress Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| DATEN | string | zu schreibende Daten (immer 1 Byte) z.B. 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-smc-lear-schreiben"></a>
### _HERSTELLERDATEN_SMC_LEAR_SCHREIBEN

Beschreiben der LEAR-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| HERSTELLERDATEN | string | Herstellerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-smc-lear-lesen"></a>
### _HERSTELLERDATEN_SMC_LEAR_LESEN

Auslesen der LEAR-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3280 Herstellerdaten SMC links lesen $0x3380 HErstellerdaten SMC rechts lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HERSTELLERDATEN | string | Herstellerdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-smc-scheinwerfer-schreiben"></a>
### HERSTELLERDATEN_SMC_SCHEINWERFER_SCHREIBEN

Beschreiben der Scheinwerfer-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| HERSTELLERDATEN | string | Herstellerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-smc-scheinwerfer-lesen"></a>
### HERSTELLERDATEN_SMC_SCHEINWERFER_LESEN

Auslesen der Scheinwerfer-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Herstellerdaten SMC links lesen $0x3381 HErstellerdaten SMC rechts lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HERSTELLERDATEN | string | Herstellerdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen-smc-l-lear"></a>
### IS_LESEN_SMC_L_LEAR

Infospeicher von SMC links lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory

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

<a id="job-is-lesen-smc-r-lear"></a>
### IS_LESEN_SMC_R_LEAR

Infospeicher von SMC rechts lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory

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

<a id="job-is-lesen-detail-smc-l-lear"></a>
### IS_LESEN_DETAIL_SMC_L_LEAR

Infospeicher Details von SMC links lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Infocode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt Es darf dann nicht argument F_POS angegeben werden |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen-detail-smc-r-lear"></a>
### IS_LESEN_DETAIL_SMC_R_LEAR

Infospeicher Details von SMC rechts lesen (alle Info-Meldungen / Ort und Art) KWP2000: $A6 LINGateway KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Infocode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt Es darf dann nicht argument F_POS angegeben werden |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen-smc-l-lear"></a>
### IS_LOESCHEN_SMC_L_LEAR

Infospeicher der SMC links loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen-smc-r-lear"></a>
### IS_LOESCHEN_SMC_R_LEAR

Infospeicher der SMC rechts loeschen KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betr-h-smc"></a>
### STATUS_BETR_H_SMC

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $51 Betriebsstunden Betriebsstunden von ausgewaehlter SMC lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSZEIT_SMC_WERT | unsigned long | Betr_h SMC |
| STAT_RESETCOUNTER_WERT | unsigned long | Anzahl Resets |
| STAT_ANZ_HS_KURVENLICHT_WERT | unsigned long | Anzahl Halbschritte Kurvenlicht |
| STAT_ANZ_HS_LWR_WERT | unsigned long | Anzahl Halbschritte LWR |
| STAT_ACHSEN_VERFAHRZEIT_KURVENLICHT_WERT | unsigned long | Achsenverfahrzeit fuer Kurvenlicht |
| STAT_ACHSEN_VERFAHRZEIT_LWR_WERT | unsigned long | Achsenverfahrzeit fur LWR |
| STAT_BETRIEBSZEIT_EINH | string | Einheit fuer Betriebsstunden |
| STAT_VERFAHRZEIT_EINH | string | Einheit fuer Achsenverfahrzeit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-betr-h-smc-loeschen"></a>
### STEUERN_BETR_H_SMC_LOESCHEN

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $51 Betriebsstunden alle Betriebszeiten der ausgewaehlten SMC loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-verteilung-winkel-ansteuerung-smc"></a>
### STATUS_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $50 Verteilung der Winkelansteuerung Verteilung der Winkelansteuerung von ausgewaehlter SMC lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WINKEL_0_2_WERT | unsigned int | WINKEL zwischen 0° und 2° |
| STAT_WINKEL_2_4_WERT | unsigned int | WINKEL zwischen 2° und 4° |
| STAT_WINKEL_4_6_WERT | unsigned int | WINKEL zwischen 4° und 6° |
| STAT_WINKEL_6_8_WERT | unsigned int | WINKEL zwischen 6° und 8° |
| STAT_WINKEL_8_10_WERT | unsigned int | WINKEL zwischen 8° und 10° |
| STAT_WINKEL_10_12_WERT | unsigned int | WINKEL zwischen 10° und 12° |
| STAT_WINKEL_12_14_WERT | unsigned int | WINKEL zwischen 12° und 14° |
| STAT_WINKEL_14_16_WERT | unsigned int | WINKEL zwischen 14° und 16° |
| STAT_WINKEL_MINUS_0_2_WERT | unsigned int | WINKEL zwischen 0° und -2° |
| STAT_WINKEL_MINUS_2_4_WERT | unsigned int | WINKEL zwischen -2° und -4° |
| STAT_WINKEL_MINUS_4_6_WERT | unsigned int | WINKEL zwischen -4° und -6° |
| STAT_WINKEL_MINUS_6_8_WERT | unsigned int | WINKEL zwischen -6° und -8° |
| STAT_WINKEL_MINUS_8_10_WERT | unsigned int | WINKEL zwischen -8° und -10° |
| STAT_WINKEL_MINUS_10_12_WERT | unsigned int | WINKEL zwischen -10° und -12° |
| STAT_WINKEL_MINUS_12_14_WERT | unsigned int | WINKEL zwischen -12° und -14° |
| STAT_WINKEL_MINUS_14_16_WERT | unsigned int | WINKEL zwischen -14° und -16° |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-verteilung-winkel-ansteuerung-smc-loeschen"></a>
### STEUERN_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC_LOESCHEN

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $50 Verteilung der Winkelansteuerung Loeschen der Verteilung der Winkelansteuerung der ausgewaehlten SMC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temperaturverteilung-smc"></a>
### STATUS_TEMPERATURVERTEILUNG_SMC

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $52 Temperaturverteilung Temperaturverteilung von der ausgewaehlten SMC lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_10_PROZENT_ABSCHALTUNG_WERT | unsigned int | 10% werden nicht mehr angefahren |
| STAT_20_PROZENT_ABSCHALTUNG_WERT | unsigned int | 20% werden nicht mehr angefahren |
| STAT_30_PROZENT_ABSCHALTUNG_WERT | unsigned int | 30% werden nicht mehr angefahren |
| STAT_40_PROZENT_ABSCHALTUNG_WERT | unsigned int | 40% werden nicht mehr angefahren |
| STAT_50_PROZENT_ABSCHALTUNG_WERT | unsigned int | 50% werden nicht mehr angefahren |
| STAT_60_PROZENT_ABSCHALTUNG_WERT | unsigned int | 60% werden nicht mehr angefahren |
| STAT_70_PROZENT_ABSCHALTUNG_WERT | unsigned int | 70% werden nicht mehr angefahren |
| STAT_80_PROZENT_ABSCHALTUNG_WERT | unsigned int | 80% werden nicht mehr angefahren |
| STAT_90_PROZENT_ABSCHALTUNG_WERT | unsigned int | 90% werden nicht mehr angefahren |
| STAT_100_PROZENT_ABSCHALTUNG_WERT | unsigned int | 100% werden nicht mehr angefahren |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-temperaturverteilung-smc-loeschen"></a>
### STEUERN_TEMPERATURVERTEILUNG_SMC_LOESCHEN

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $52 Temperaturverteilung Loeschen der Temperaturverteilung der ausgewaehlten SMC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schrittverluste-smc"></a>
### STATUS_SCHRITTVERLUSTE_SMC

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $53 Schrittverluste Schrittverluste von der ausgewaehlten SMC lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHRITTVERLUSTGRENZE_1_WERT | unsigned int | Schrittverluste in Bereich 1 |
| STAT_SCHRITTVERLUSTGRENZE_2_WERT | unsigned int | Schrittverluste in Bereich 2 |
| STAT_SCHRITTVERLUSTGRENZE_3_WERT | unsigned int | Schrittverluste in Bereich 3 |
| STAT_SCHRITTVERLUSTGRENZE_4_WERT | unsigned int | Schrittverluste in Bereich 4 |
| STAT_SCHRITTVERLUSTGRENZE_5_WERT | unsigned int | Schrittverluste in Bereich 5 |
| STAT_SCHRITTVERLUSTGRENZE_6_WERT | unsigned int | Schrittverluste in Bereich 6 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schrittverluste-smc-loeschen"></a>
### STEUERN_SCHRITTVERLUSTE_SMC_LOESCHEN

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $53 Schrittverluste Loeschen der Schrittverluste der ausgewaehlten SMC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hw-eingange-smc"></a>
### STATUS_HW_EINGANGE_SMC

KWP2000: $A6 LINGateway KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $54 HW_Eingaenge HW_Eingaenge von der ausgewaehlten SMC lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_U_BATT_WERT | unsigned int | Batteriespannung |
| STAT_SPANNUNG_BATT_WERT | real | Batteriespannung Bereich: 0 .. 18 Volt |
| STAT_U_KOD_WERT | unsigned int | Kodierspannung: kleiner 128: SMC_L, groesser 128: SMC_R |
| STAT_U_SENSE_WERT | unsigned int | Sensespannung |
| STAT_SPANNUNG_SENSE_WERT | real | Sensespannung Bereich: 0 .. 5 Volt |
| STAT_COD_1_EIN | unsigned int | Hardwarekodierungseingang 1 |
| STAT_COD_2_EIN | unsigned int | Hardwarekodierungseingang 2 |
| STAT_COD_3_EIN | unsigned int | Hardwarekodierungseingang 3 |
| STAT_SENSE_UP_DOWN_EIN | unsigned int | Zustand von Sensor-Pullup |
| STAT_U_SENSE_EIN | unsigned int | Sensorspannung ein |
| STAT_KONTROLL_WERT | unsigned long | Sensor Kontrollwert: Anzahl HS der letzten Schrittverluste |
| STAT_SENSOR_WERT | unsigned long | Sensorwert PWM-Verhaeltnis |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellertest-smc-lear"></a>
### _HERSTELLERTEST_SMC_LEAR

Herstellertest KWP2000: $A6 LINGateway KWP2000: $31 StartRoutineByLocalIdentifier $04 Herstellertest Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| UBAT_HIGH | unsigned char | Grenzwert Batteriespannung Highwert |
| UBAT_LOW | unsigned char | Grenzwert Batteriespannung Lowwert |
| USEN_HIGH | unsigned char | Grenzwert Sensespannung Highwert |
| USEN_LOW | unsigned char | Grenzwert Sensespannung Lowwert |
| DIGITAL_MASK_1 | unsigned char | Musterbyte fuer Digitalstatus 1 |
| DIGITAL_MASK_2 | unsigned char | Musterbyte fuer Digitalstatus 2 |
| DIGITAL_MASK_3 | unsigned char | Musterbyte fuer Digitalstatus 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS | string | Statusbyte |
| UBAT_1 | real | Batteriespannung 1 |
| UBAT_2 | real | Batteriespannung 2 |
| UBAT_3 | real | Batteriespannung 3 |
| USEN_1 | real | Sensespannung 1 |
| USEN_2 | real | Sensespannung 2 |
| USEN_3 | real | Sensespannung 3 |
| DIGITAL_1 | string | Digitalwerte Satz 1 |
| DIGITAL_2 | string | Digitalwerte Satz 2 |
| DIGITAL_3 | string | Digitalwerte Satz 3 |
| HERSTELLERTEST | string | Daten Herstellertest |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-scheinwerferherstellerdaten-schreiben"></a>
### SCHEINWERFERHERSTELLERDATEN_SCHREIBEN

Beschreiben der Scheinwerfer-Herstellerdaten KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| SCHEINWERFER_HERSTELLERDATEN | string | Herstellerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-scheinwerferherstellerdaten-lesen"></a>
### SCHEINWERFERHERSTELLERDATEN_LESEN

Auslesen der Scheinwerfer-Herstellerdaten KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Herstellerdaten SMC links lesen $0x3381 HErstellerdaten SMC rechts lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SCHEINWERFER_HERSTELLERDATEN | string | Herstellerdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-scheinwerfer-schreiben"></a>
### PRUEFSTEMPEL_SCHEINWERFER_SCHREIBEN

Beschreiben des Scheinwerfer-Pruefstempel KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| SCHEINWERFER_PRUEFSTEMPEL | string | Scheinwerfer-Pruefstempel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-scheinwerfer-lesen"></a>
### PRUEFSTEMPEL_SCHEINWERFER_LESEN

Auslesen der Scheinwerfer-Pruefstempel KWP 2000: $A6 LINGateway $22 ReadDataByCommonIdentifier $0x3281 Scheinwerfer-Pruefstempel SMC links lesen $0x3381 Scheinwerfer-Pruefstempel SMC rechts lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SCHEINWERFER_PRUEFSTEMPEL | string | Herstellerdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-diag-ringspeicher-lear"></a>
### _READ_DIAG_RINGSPEICHER_LEAR

KWP 2000: $21 ReadDataByLocalIdentifier $0B DIAG_RINGSPEICHER Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| POS_RINGSPEICHER | int | aktuelle POSITION im RINGSPEICHER |
| SCHALTER_LICHT_1 | int | Lichtschalterstellung 1 (Standlicht) Lichtschalterstellung 1 + 2 (Abblendlicht) |
| SCHALTER_LICHT_2 | int | Lichtschalterstellung 2 (FLC) Lichtschalterstellung 1 + 2 (Abblendlicht) |
| KL_15_HW | int | Klemme 15 HW-Eingang |
| KL_15_CAN | int | Klemme 15 ueber CAN |
| ANF_AL | int | Anforderung AL SW-seitig |
| AL_EINGANG_RED | int | redundanter Abblendlichteingang |
| RESET_COUNTER | int | RESET_COUNTER |
| BORDNETZ_SPG | real | BORDNETZ_SPG |
| GESCHWINDIGKEIT | int | GESCHWINDIGKEIT |
| KM_STAND | long | KM_STAND |
| TEL_STATUS_FAHRLICHT | long | TELEGRAMM STATUS_FAHRLICHT |
| ABS_TIMER | long | Absoluttimer im Steuergeraet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-clr-diag-ringspeicher-lear"></a>
### _CLR_DIAG_RINGSPEICHER_LEAR

KWP2000: $3B WriteDataByLocalIdentifier $0B DIAG_RINGSPEICHER Modus  : Default

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
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
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
- [FORTTEXTE](#table-forttexte) (75 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (87 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (13 × 9)
- [HORTTEXTE](#table-horttexte) (81 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HUMWELTMATRIX](#table-humweltmatrix) (80 × 5)
- [HUMWELTTEXTE](#table-humwelttexte) (12 × 9)
- [IORTTEXTE](#table-iorttexte) (13 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (3 × 9)
- [LAMPNRTEXTE](#table-lampnrtexte) (35 × 3)
- [SMCS](#table-smcs) (3 × 3)
- [REF_SMCS](#table-ref-smcs) (4 × 3)
- [BFDSTUFETEXTE](#table-bfdstufetexte) (9 × 3)
- [STAT_LAMPEN_DEFEKTE](#table-stat-lampen-defekte) (4 × 3)
- [LAMPFUNKTEXTE](#table-lampfunktexte) (10 × 3)
- [NOTL](#table-notl) (1 × 7)
- [ENERGYSAVING](#table-energysaving) (5 × 3)
- [TIEFENTL](#table-tiefentl) (1 × 8)

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

Dimensions: 75 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9CA8 | interner Fehler LM-II |
| 0x9CA9 | Klemme 30A Anschluss fehlerhaft |
| 0x9CAA | Klemme 30B Anschluss fehlerhaft |
| 0x9CAB | eine Klemme 15 fehlt |
| 0x9CAC | Bremslichtschalter defekt |
| 0x9CAD | LWR-Poti defekt |
| 0x9CAE | Bedienteilfehler |
| 0x9CAF | Lichtschalterstellung 1 defekt |
| 0x9CB0 | Lichtschalterstellung 2 defekt |
| 0x9CB1 | Dimmer-Poti defekt |
| 0x9CB2 | Sensor Hoehenstand vorne defekt |
| 0x9CB3 | Sensor Hoehenstand hinten defekt |
| 0x9CB4 | Energiesparmode aktiv |
| 0x9CB5 | Unkonsistenz: Softwareversion und Codierindex |
| 0x9CB6 | LWR-Spulenabriss |
| 0x9CB7 | LWR-Treiberfehler |
| 0x9CB8 | Kurzschlussfehler |
| 0x9CB9 | Batterie tiefentladen |
| 0x9CBA | Tiefentladungsschutz der Batterie: Abschaltung Standlicht |
| 0x9CBB | Tiefentladungsschutz der Batterie: Abschaltung Parklicht |
| 0x9CBC | Kommunikation mit StepperMoterBox links gestoert |
| 0x9CBD | Kommunikation mit StepperMoterBox rechts gestoert |
| 0x9CBE | Achtung: Elektronik am linken Scheinwerfer (SMC) meldet Fehler |
| 0x9CBF | Achtung: Elektronik am rechten Scheinwerfer (SMC) meldet Fehler |
| 0x9CC0 | Vergleich Fahrgestellnummer ALC mit SMC links unterschiedlich |
| 0x9CC1 | Vergleich Fahrgestellnummer ALC mit SMC rechts unterschiedlich |
| 0x9CC2 | Hardwareleitung zu SZL fehlt |
| 0x9CC3 | RLS: LinPhysicalBusError |
| 0x9CC4 | RLS: LinProtocolError |
| 0x9CC5 | RLS: NoResponse |
| 0xA8A8 | Fernlicht links defekt |
| 0xA8A9 | Fernlicht rechts defekt |
| 0xA8AA | Abblendlicht links defekt |
| 0xA8AB | Abblendlicht rechts defekt |
| 0xA8AC | Begrenzungslicht links (E60, E65), aussen (E60-Halogen), Zusatzfahrtrichtungsanzeiger links (E63, E64 ab 09/07) defekt |
| 0xA8AD | Begrenzungslicht rechts (E60, E65), aussen (E60-Halogen), Zusatzfahrtrichtungsanzeiger rechts (E63, E64 ab 09/07) defekt |
| 0xA8AE | Nebelscheinwerfer links defekt |
| 0xA8AF | Nebelscheinwerfer rechts defekt |
| 0xA8B0 | Fahrtrichtungsanzeiger links vorne 1 defekt |
| 0xA8B1 | Fahrtrichtungsanzeiger rechts vorne 1 defekt |
| 0xA8B2 | Fahrtrichtungsanzeiger links hinten defekt |
| 0xA8B3 | Fahrtrichtungsanzeiger rechts hinten defekt |
| 0xA8B4 | Seitenmarkierungslicht defekt |
| 0xA8B5 | Bremslicht links defekt |
| 0xA8B6 | Bremslicht rechts defekt |
| 0xA8B7 | Bremslicht mitte defekt |
| 0xA8B8 | Schlusslicht/Bremslicht links defekt |
| 0xA8B9 | Schlusslicht/Bremslicht rechts defekt |
| 0xA8BA | Schlusslicht (E65), Begrenzungslicht (E60-Halogen), links innen defekt |
| 0xA8BB | Schlusslicht (E65), Begrenzungslicht (E60-Halogen), rechts innen defekt |
| 0xA8BC | Kennzeichenlicht links defekt |
| 0xA8BD | Kennzeichenlicht rechts defekt |
| 0xA8BE | Nebelschlusslicht links defekt |
| 0xA8BF | Nebelschlusslicht rechts defekt |
| 0xA8C0 | Rueckfahrlicht links defekt |
| 0xA8C1 | Rueckfahrlicht rechts defekt |
| 0xA8C2 | Fahrtrichtungsanzeiger links vorne 2, Schlusslicht/Bremslicht links 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) defekt |
| 0xA8C3 | Fahrtrichtungsanzeiger rechts vorne 2, Schlusslicht/Bremslicht rechts 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) defekt |
| 0xA8C4 | Tagfahrlicht links defekt |
| 0xA8C5 | Tagfahrlicht rechts defekt |
| 0xA8C6 | Klemme 58g defekt |
| 0xA8C7 | Bi-Xenonklappe defekt |
| 0xE504 | Bus Leitungsfehler K-CAN |
| 0xE507 | Bus Kommunikationsfehler K-CAN |
| 0xE50B | Bus Kommunikationsfehler PT-CAN |
| 0xE514 | Telegramm Lenkwinkel Timeout |
| 0xE515 | Telegramm Status-AHM Timeout |
| 0xE516 | Telegramm Bedienung Lenkstock Timeout |
| 0xE517 | Telegramm Status DSC Timeout |
| 0xE518 | Telegramm Status Fahrlicht Timeout |
| 0xE519 | Telegramm Geschwindigkeit Timeout |
| 0xE51A | Telegramm Gierrate Timeout |
| 0xE51B | Telegramm Klemmenstatus Timeout |
| 0xE51C | Telegramm Fernlichtassistent Timeout |
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

Dimensions: 87 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9CA8 | 0x01 | 0x02 | - | - |
| 0x9CA9 | 0x01 | 0x02 | - | - |
| 0x9CAA | 0x01 | 0x02 | - | - |
| 0x9CAB | 0x01 | 0x02 | - | - |
| 0x9CAC | 0x01 | 0x02 | - | - |
| 0x9CAD | 0x01 | 0x02 | - | - |
| 0x9CAE | 0x01 | 0x02 | - | - |
| 0x9CAF | 0x01 | 0x02 | - | - |
| 0x9CB0 | 0x01 | 0x02 | - | - |
| 0x9CB1 | 0x01 | 0x02 | - | - |
| 0x9CB2 | 0x01 | 0x02 | - | - |
| 0x9CB3 | 0x01 | 0x02 | - | - |
| 0x9CB4 | 0x01 | 0x02 | - | - |
| 0x9CB5 | 0x01 | 0x02 | - | - |
| 0x9CB6 | 0x01 | 0x02 | - | - |
| 0x9CB7 | 0x20 | 0x21 | - | - |
| 0x9CB8 | 0x01 | 0x02 | - | - |
| 0x9CB9 | 0x01 | TIEFENTL | - | - |
| 0x9CBA | 0x01 | 0x02 | - | - |
| 0x9CBB | 0x01 | 0x02 | - | - |
| 0x9CBC | 0x01 | 0x02 | - | - |
| 0x9CBD | 0x01 | 0x02 | - | - |
| 0x9CBE | 0x01 | 0x02 | - | - |
| 0x9CBF | 0x01 | 0x02 | - | - |
| 0x9CC0 | 0x01 | 0x02 | - | - |
| 0x9CC1 | 0x01 | 0x02 | - | - |
| 0x9CC2 | 0x01 | 0x02 | - | - |
| 0x9CC3 | 0x01 | 0x02 | - | - |
| 0x9CC4 | 0x01 | 0x02 | - | - |
| 0x9CC5 | 0x01 | 0x02 | - | - |
| 0x9CC6 | 0x01 | 0x02 | - | - |
| 0x9CC7 | 0x01 | 0x02 | - | - |
| 0x9CC8 | 0x01 | 0x02 | - | - |
| 0x9CC9 | 0x01 | 0x02 | - | - |
| 0x9CCA | 0x01 | 0x02 | - | - |
| 0x9CCB | 0x01 | 0x02 | - | - |
| 0x9CCC | 0x01 | 0x02 | - | - |
| 0x9CCD | 0x01 | 0x02 | - | - |
| 0x9CCE | 0x01 | 0x02 | - | - |
| 0x9CCF | 0x01 | 0x02 | - | - |
| 0x9CD0 | 0x01 | 0x02 | - | - |
| 0x9CD1 | 0x01 | 0x02 | - | - |
| 0x9CD2 | 0x01 | 0x02 | - | - |
| 0xA8A8 | 0x01 | 0x03 | - | - |
| 0xA8A9 | 0x01 | 0x03 | - | - |
| 0xA8AA | 0x01 | 0x03 | - | - |
| 0xA8AB | 0x01 | 0x03 | - | - |
| 0xA8AC | 0x01 | 0x03 | - | - |
| 0xA8AD | 0x01 | 0x03 | - | - |
| 0xA8AE | 0x01 | 0x03 | - | - |
| 0xA8AF | 0x01 | 0x03 | - | - |
| 0xA8B0 | 0x01 | 0x03 | - | - |
| 0xA8B1 | 0x01 | 0x03 | - | - |
| 0xA8B2 | 0x01 | 0x03 | - | - |
| 0xA8B3 | 0x01 | 0x03 | - | - |
| 0xA8B4 | 0x01 | 0x03 | - | - |
| 0xA8B5 | 0x01 | 0x03 | - | - |
| 0xA8B6 | 0x01 | 0x03 | - | - |
| 0xA8B7 | 0x01 | 0x03 | - | - |
| 0xA8B8 | 0x01 | 0x03 | - | - |
| 0xA8B9 | 0x01 | 0x03 | - | - |
| 0xA8BA | 0x01 | 0x03 | - | - |
| 0xA8BB | 0x01 | 0x03 | - | - |
| 0xA8BC | 0x01 | 0x03 | - | - |
| 0xA8BD | 0x01 | 0x03 | - | - |
| 0xA8BE | 0x01 | 0x03 | - | - |
| 0xA8BF | 0x01 | 0x03 | - | - |
| 0xA8C0 | 0x01 | 0x03 | - | - |
| 0xA8C1 | 0x01 | 0x03 | - | - |
| 0xA8C2 | 0x01 | 0x03 | - | - |
| 0xA8C3 | 0x01 | 0x03 | - | - |
| 0xA8C4 | 0x01 | 0x03 | - | - |
| 0xA8C5 | 0x01 | 0x03 | - | - |
| 0xA8C6 | 0x01 | 0x03 | - | - |
| 0xA8C7 | 0x01 | 0x03 | - | - |
| 0xE504 | 0x01 | 0x02 | - | - |
| 0xE507 | 0x01 | 0x02 | - | - |
| 0xE50B | 0x01 | 0x02 | - | - |
| 0xE514 | 0x01 | 0x02 | - | - |
| 0xE515 | 0x01 | 0x02 | - | - |
| 0xE516 | 0x01 | 0x02 | - | - |
| 0xE517 | 0x01 | 0x02 | - | - |
| 0xE518 | 0x01 | 0x02 | - | - |
| 0xE519 | 0x01 | 0x02 | - | - |
| 0xE51A | 0x01 | 0x02 | - | - |
| 0xE51B | 0x01 | 0x02 | - | - |
| 0xE51C | 0x01 | 0x02 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 13 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | - | unsigned char | - | 18 | 255 | 0 |
| 0x02 | Sensorspannung | Volt | - | unsigned char | - | 5 | 255 | 0 |
| 0x03 | Betriebsstunden | h | - | unsigned char | - | 2 | 1 | 0 |
| 0x10 | Klemme 15 | 0/1 | high | 0x80 | - | - | - | - |
| 0x11 | Klemme R | 0/1 | high | 0x40 | - | - | - | - |
| 0x12 | Standlicht | 0/1 | high | 0x20 | - | - | - | - |
| 0x13 | Parklicht links | 0/1 | high | 0x10 | - | - | - | - |
| 0x14 | Parklicht rechts | 0/1 | high | 0x08 | - | - | - | - |
| 0x15 | Warnblinklicht | 0/1 | high | 0x04 | - | - | - | - |
| 0x16 | Follow me home | 0/1 | high | 0x02 | - | - | - | - |
| 0x20 | LWR-Treiberfehlerbyte 1 | 1 | - | unsigned char | - | - | - | - |
| 0x21 | LWR-Treiberfehlerbyte 2 | 1 | - | unsigned char | - | - | - | - |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 81 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9308 | EEPROM SMC links defekt |
| 0x9309 | Motor Kurvenlicht SMC links defekt |
| 0x930A | Motor LWR SMC links defekt |
| 0x930B | Treiber Kurvenlicht SMC links defekt |
| 0x930C | Spannungsversorgung Sensor SMC links defekt |
| 0x930D | Signal Sensor SMC links defekt |
| 0x930E | Flanke Sensor SMC links defekt |
| 0x930F | LIN SMC links defekt |
| 0x9310 | Schrittverlust Grenze 1 SMC links |
| 0x9311 | Schrittverlust Grenze 2 SMC links |
| 0x9312 | Schrittverlust Grenze 3 SMC links |
| 0x9313 | Schrittverlust Grenze 4 SMC links |
| 0x9314 | Schrittverlust Grenze 5 SMC links |
| 0x9315 | Schrittverlust Grenze 6 SMC links |
| 0x9316 | Spike auf Sensor SMS links |
| 0x9317 | Notlauf aktiv SMC links |
| 0x9318 | unbekannter Fehler 2 SMC links |
| 0x9319 | unbekannter Fehler 3 SMC links |
| 0x931A | unbekannter Fehler 4 SMC links |
| 0x931B | unbekannter Fehler 5 SMC links |
| 0x931C | EEPROM SMC rechts defekt |
| 0x931D | Motor Kurvenlicht SMC rechts defekt |
| 0x931E | Motor LWR SMC rechts defekt |
| 0x931F | Treiber Kurvenlicht SMC rechts defekt |
| 0x9320 | Spannungsversorgung Sensor SMC rechts defekt |
| 0x9321 | Signal Sensor SMC rechts defekt |
| 0x9322 | Flanke Sensor SMC rechts defekt |
| 0x9323 | LIN SMC rechts defekt |
| 0x9324 | Schrittverlust Grenze 1 SMC rechts |
| 0x9325 | Schrittverlust Grenze 2 SMC rechts |
| 0x9326 | Schrittverlust Grenze 3 SMC rechts |
| 0x9327 | Schrittverlust Grenze 4 SMC rechts |
| 0x9328 | Schrittverlust Grenze 5 SMC rechts |
| 0x9329 | Schrittverlust Grenze 6 SMC rechts |
| 0x932A | Spike auf Sensor SMS rechts |
| 0x932B | Notlauf aktiv SMC rechts |
| 0x932C | unbekannter Fehler 2 SMC rechts |
| 0x932D | unbekannter Fehler 3 SMC rechts |
| 0x932E | unbekannter Fehler 4 SMC rechts |
| 0x932F | unbekannter Fehler 5 SMC rechts |
| 0x9400 | EEPROM SMC links defekt |
| 0x9401 | Motor Kurvenlicht SMC links defekt |
| 0x9402 | Motor LWR SMC links defekt |
| 0x9403 | Treiber Kurvenlicht SMC links defekt |
| 0x9404 | Spannungsversorgung Sensor SMC links defekt |
| 0x9405 | Signal Sensor SMC links defekt |
| 0x9406 | Flanke Sensor SMC links defekt |
| 0x9407 | LIN SMC links defekt |
| 0x9408 | Schrittverlust Grenze 1 SMC links |
| 0x9409 | Schrittverlust Grenze 2 SMC links |
| 0x940A | Schrittverlust Grenze 3 SMC links |
| 0x940B | Schrittverlust Grenze 4 SMC links |
| 0x940C | Schrittverlust Grenze 5 SMC links |
| 0x940D | Schrittverlust Grenze 6 SMC links |
| 0x940E | Spike auf Sensor SMS links |
| 0x940F | Notlauf aktiv SMC links |
| 0x9410 | unbekannter Fehler 2 SMC links |
| 0x9411 | unbekannter Fehler 3 SMC links |
| 0x9412 | unbekannter Fehler 4 SMC links |
| 0x9413 | unbekannter Fehler 5 SMC links |
| 0x9420 | EEPROM SMC rechts defekt |
| 0x9421 | Motor Kurvenlicht SMC rechts defekt |
| 0x9422 | Motor LWR SMC rechts defekt |
| 0x9423 | Treiber Kurvenlicht SMC rechts defekt |
| 0x9424 | Spannungsversorgung Sensor SMC rechts defekt |
| 0x9425 | Signal Sensor SMC rechts defekt |
| 0x9426 | Flanke Sensor SMC rechts defekt |
| 0x9427 | LIN SMC rechts defekt |
| 0x9428 | Schrittverlust Grenze 1 SMC rechts |
| 0x9429 | Schrittverlust Grenze 2 SMC rechts |
| 0x942A | Schrittverlust Grenze 3 SMC rechts |
| 0x942B | Schrittverlust Grenze 4 SMC rechts |
| 0x942C | Schrittverlust Grenze 5 SMC rechts |
| 0x942D | Schrittverlust Grenze 6 SMC rechts |
| 0x942E | Spike auf Sensor SMS rechts |
| 0x942F | Notlauf aktiv SMC rechts |
| 0x9430 | unbekannter Fehler 2 SMC rechts |
| 0x9431 | unbekannter Fehler 3 SMC rechts |
| 0x9432 | unbekannter Fehler 4 SMC rechts |
| 0x9433 | unbekannter Fehler 5 SMC rechts |
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
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 80 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9308 | 0x04 | -- | -- | -- |
| 0x9309 | 0x01 | -- | -- | -- |
| 0x930A | 0x01 | -- | -- | -- |
| 0x930B | 0x01 | -- | -- | -- |
| 0x930C | 0x03 | -- | -- | -- |
| 0x930D | 0x01 | -- | -- | -- |
| 0x930E | 0x01 | -- | -- | -- |
| 0x930F | 0x01 | -- | -- | -- |
| 0x9310 | 0x01 | -- | -- | -- |
| 0x9311 | 0x01 | -- | -- | -- |
| 0x9312 | 0x01 | -- | -- | -- |
| 0x9313 | 0x01 | -- | -- | -- |
| 0x9314 | 0x01 | -- | -- | -- |
| 0x9315 | 0x01 | -- | -- | -- |
| 0x9316 | 0x03 | -- | -- | -- |
| 0x9317 | NOTL | -- | -- | -- |
| 0x9318 | -- | -- | -- | -- |
| 0x9319 | -- | -- | -- | -- |
| 0x931A | -- | -- | -- | -- |
| 0x931B | -- | -- | -- | -- |
| 0x931C | 0x04 | -- | -- | -- |
| 0x931D | 0x01 | -- | -- | -- |
| 0x931E | 0x01 | -- | -- | -- |
| 0x931F | 0x01 | -- | -- | -- |
| 0x9320 | 0x03 | -- | -- | -- |
| 0x9321 | 0x01 | -- | -- | -- |
| 0x9322 | 0x01 | -- | -- | -- |
| 0x9323 | 0x01 | -- | -- | -- |
| 0x9324 | 0x01 | -- | -- | -- |
| 0x9325 | 0x01 | -- | -- | -- |
| 0x9326 | 0x01 | -- | -- | -- |
| 0x9327 | 0x01 | -- | -- | -- |
| 0x9328 | 0x01 | -- | -- | -- |
| 0x9329 | 0x01 | -- | -- | -- |
| 0x932A | 0x03 | -- | -- | -- |
| 0x932B | NOTL | -- | -- | -- |
| 0x932C | -- | -- | -- | -- |
| 0x932D | -- | -- | -- | -- |
| 0x932E | -- | -- | -- | -- |
| 0x932F | -- | -- | -- | -- |
| 0x9400 | 0x04 | -- | -- | -- |
| 0x9401 | 0x01 | -- | -- | -- |
| 0x9402 | 0x01 | -- | -- | -- |
| 0x9403 | 0x01 | -- | -- | -- |
| 0x9404 | 0x03 | -- | -- | -- |
| 0x9405 | 0x01 | -- | -- | -- |
| 0x9406 | 0x01 | -- | -- | -- |
| 0x9407 | 0x01 | -- | -- | -- |
| 0x9408 | 0x01 | -- | -- | -- |
| 0x9409 | 0x01 | -- | -- | -- |
| 0x940A | 0x01 | -- | -- | -- |
| 0x940B | 0x01 | -- | -- | -- |
| 0x940C | 0x01 | -- | -- | -- |
| 0x940D | 0x01 | -- | -- | -- |
| 0x940E | 0x03 | -- | -- | -- |
| 0x940F | NOTL | -- | -- | -- |
| 0x9410 | -- | -- | -- | -- |
| 0x9411 | -- | -- | -- | -- |
| 0x9412 | -- | -- | -- | -- |
| 0x9413 | -- | -- | -- | -- |
| 0x9420 | 0x04 | -- | -- | -- |
| 0x9421 | 0x01 | -- | -- | -- |
| 0x9422 | 0x01 | -- | -- | -- |
| 0x9423 | 0x01 | -- | -- | -- |
| 0x9424 | 0x03 | -- | -- | -- |
| 0x9425 | 0x01 | -- | -- | -- |
| 0x9426 | 0x01 | -- | -- | -- |
| 0x9427 | 0x01 | -- | -- | -- |
| 0x9428 | 0x01 | -- | -- | -- |
| 0x9429 | 0x01 | -- | -- | -- |
| 0x942A | 0x01 | -- | -- | -- |
| 0x942B | 0x01 | -- | -- | -- |
| 0x942C | 0x01 | -- | -- | -- |
| 0x942D | 0x01 | -- | -- | -- |
| 0x942E | 0x03 | -- | -- | -- |
| 0x942F | NOTL | -- | -- | -- |
| 0x9430 | -- | -- | -- | -- |
| 0x9431 | -- | -- | -- | -- |
| 0x9432 | -- | -- | -- | -- |
| 0x9433 | -- | -- | -- | -- |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 12 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | -- | unsigned char | -- | 18 | 255 | 0 |
| 0x02 | Betriebsstunden | min | -- | unsigned int | -- | 3 | 1 | 0 |
| 0x03 | Sensorspannung | Volt | -- | unsigned char | -- | 5 | 255 | 0 |
| 0x04 | Motortemperatur | °C | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x05 | Bordnetzspannung | Volt | -- | unsigned char | -- | 18 | 255 | 0 |
| 0x10 | NOT_SENS_DEFEKT | 0/1 | high | 0x01 | - | - | - | - |
| 0x11 | NOT_SENS_NOK | 0/1 | high | 0x02 | - | - | - | - |
| 0x12 | NOT_SCHR_VER_NOK | 0/1 | high | 0x04 | - | - | - | - |
| 0x13 | NOT_USENS_NOK | 0/1 | high | 0x08 | - | - | - | - |
| 0x14 | NOT_MOTOR_DEF | 0/1 | high | 0x10 | - | - | - | - |
| 0x15 | NOT_MOTOR_LWR_DEF | 0/1 | high | 0x20 | - | - | - | - |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 13 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9308 | LoadDump aktiviert |
| 0x9309 | Signal vom Regenlichtsensor unplausibel |
| 0x930A | Lichtnotlauf mit Kl.15 aktiv |
| 0x930B | Lichtnotlauf mit Geschwindigkeit aktiv |
| 0x930C | ALC-System defekt |
| 0x930D | ALC-System: AL links abgeschaltet |
| 0x930E | ALC-System: AL rechts abgeschaltet |
| 0x930F | RLS Grund: Dunkelheit aber Abblendlicht aus |
| 0x9310 | Taster Nebelscheinwerfer defekt |
| 0x9311 | Taster Nebelschlusslicht defekt |
| 0x9312 | Taster Warnblinklicht defekt |
| 0x9313 | Schalter Rueckfahrscheinwerfer defekt |
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

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | - | unsigned char | - | 18 | 255 | 0 |
| 0x02 | Sensorspannung | Volt | - | unsigned char | - | 5 | 255 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-lampnrtexte"></a>
### LAMPNRTEXTE

Dimensions: 35 rows × 3 columns

| LAMPNR | NAME | TEXT |
| --- | --- | --- |
| 0x00 | AUSGANG_FL_LINKS | Fernlicht links |
| 0x01 | AUSGANG_FL_RECHTS | Fernlicht rechts |
| 0x02 | AUSGANG_AL_LINKS | Abblendlicht links |
| 0x03 | AUSGANG_AL_RECHTS | Abblendlicht rechts |
| 0x04 | AUSGANG_BEGRL_LINKS | Begrenzungslicht links (E60, E65), aussen (E60-Halogen), Zusatzfahrtrichtungsanzeiger links (E63, E64 ab 09/07) |
| 0x05 | AUSGANG_BEGRL_RECHTS | Begrenzungslicht rechts (E60, E65), aussen (E60-Halogen), Zusatzfahrtrichtungsanzeiger rechts (E63, E64 ab 09/07) |
| 0x06 | AUSGANG_NSW_LINKS | Nebelscheinwerfer links |
| 0x07 | AUSGANG_NSW_RECHTS | Nebelscheinwerfer rechts |
| 0x08 | AUSGANG_FRA_LINKS_VORN | Fahrtrichtungsanzeiger links vorne |
| 0x09 | AUSGANG_FRA_RECHTS_VORN | Fahrtrichtungsanzeiger rechts vorne |
| 0x0A | AUSGANG_FRA_LINKS_HINTEN | Fahrtrichtungsanzeiger links hinten |
| 0x0B | AUSGANG_FRA_RECHTS_HINTEN | Fahrtrichtungsanzeiger rechts hinten |
| 0x0C | AUSGANG_SML | Seitenmarkierungsleuchte |
| 0x0D | AUSGANG_BREMSLICHT_LINKS | Bremslicht links |
| 0x0E | AUSGANG_BREMSLICHT_RECHTS | Bremslicht rechts |
| 0x0F | AUSGANG_BREMSLICHT_MITTE | Bremslicht mitte |
| 0x10 | AUSGANG_SL_BL_LINKS_1 | Schlusslicht/Bremslicht links 1 |
| 0x11 | AUSGANG_SL_BL_RECHTS_1 | Schlusslicht/Bremslicht rechts 1 |
| 0x12 | AUSGANG_SL_BL_LINKS_2 | Schlusslicht/Bremslicht links 2 |
| 0x13 | AUSGANG_SL_BL_RECHTS_2 | Schlusslicht/Bremslicht rechts 2 |
| 0x14 | AUSGANG_KZL_L | Kennzeichenlicht links |
| 0x15 | AUSGANG_KZL_R | Kennzeichenlicht rechts |
| 0x16 | AUSGANG_NSL_LINKS | Nebelschlusslicht links |
| 0x17 | AUSGANG_NSL_RECHTS | Nebelschlusslicht rechts |
| 0x18 | AUSGANG_RFL_LINKS | Rueckfahrlicht links |
| 0x19 | AUSGANG_RFL_RECHTS | Rueckfahrlicht rechts |
| 0x1A | AUSGANG_FRA_LINKS_VORN_2 | Fahrtrichtungsanzeiger links vorne 2, Schlusslicht/Bremslicht links 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) |
| 0x1B | AUSGANG_FRA_RECHTS_VORN_2 | Fahrtrichtungsanzeiger rechts vorne 2, Schlusslicht/Bremslicht rechts 2 (E60, E61 ab 03/07, E63, E64 ab 09/07) |
| 0x1C | AUSGANG_DRL_LINKS | Tagfahrlicht links |
| 0x1D | AUSGANG_DRL_RECHTS | Tagfahrlicht rechts |
| 0x1E | AUSGANG_KL_58G | Klemme 58g |
| 0x1F | AUSGANG_BIX | Bixenon-Klappe |
| 0x20 | AUSGANG_FLC_LED | FLC-LED |
| 0x21 | AUSGANG_WBL | Warnblinktasterbeleuchtung |
| 0xFF | UNKNOWN | unbekannte Lampe |

<a id="table-smcs"></a>
### SMCS

Dimensions: 3 rows × 3 columns

| SMC | NAME | TEXT |
| --- | --- | --- |
| 0x89 | SMC_L | SMC links |
| 0x8A | SMC_R | SMC rechts |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-ref-smcs"></a>
### REF_SMCS

Dimensions: 4 rows × 3 columns

| REF | NAME | TEXT |
| --- | --- | --- |
| 0x00 | REF_ALC_MIT | Referenzlauf Kurvenlicht mit Sensor |
| 0x01 | REF_ALC_OHNE | Referenzlauf Kurvenlicht ohne Sensor |
| 0x02 | REF_LWR | Referenzlauf LWR |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-bfdstufetexte"></a>
### BFDSTUFETEXTE

Dimensions: 9 rows × 3 columns

| BFD_STUFE | NAME | TEXT |
| --- | --- | --- |
| 0x00 | KEINE_BFD | keine BFD-Stufe |
| 0x01 | BFD_0 | Bremslicht |
| 0x02 | BFD_1 | BFD-Stufe 1 |
| 0x04 | BFD_2 | BFD-Stufe 2 |
| 0x03 | BFD_0_1 | Bremslicht und BFD-Stufe 1 |
| 0x05 | BFD_0_2 | Bremslicht und BFD-Stufe 2 |
| 0x06 | BFD_1_2 | BFD-Stufe 1 und BFD-Stufe 2 |
| 0x07 | BFD_0_1_2 | Bremslicht und BFD-Stufe 1 und BFD-Stufe 2 |
| 0xff | ERROR | falsche Eingabe |

<a id="table-stat-lampen-defekte"></a>
### STAT_LAMPEN_DEFEKTE

Dimensions: 4 rows × 3 columns

| WERT | VSWERT | STATUS_TEXT |
| --- | --- | --- |
| 0x00 | 2 | Nicht Ueberwacht |
| 0x01 | 1 | Fehler |
| 0x02 | 0 | Ok |
| 0x03 | 1 | Fehler |

<a id="table-lampfunktexte"></a>
### LAMPFUNKTEXTE

Dimensions: 10 rows × 3 columns

| LAMPFUNK | NAME | TEXT |
| --- | --- | --- |
| 0x01 | AL | Abblendlicht |
| 0x02 | NSW | Nebelscheinwerfer |
| 0x03 | FL | Fernlicht |
| 0x04 | FRA | Fahrtrichtungsanzeiger |
| 0x05 | BL | Bremslicht |
| 0x06 | BFD_1 | BFD Stufe 1 |
| 0x07 | BFD_2 | BFD Stufe 2 |
| 0x08 | RFL | Rueckfahrlicht |
| 0x09 | TFL | Tagfahrlicht |
| 0x0A | NSL | Nebelschlusslicht |

<a id="table-notl"></a>
### NOTL

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 |

<a id="table-energysaving"></a>
### ENERGYSAVING

Dimensions: 5 rows × 3 columns

| E_MODE | NAME | TEXT |
| --- | --- | --- |
| 0x00 | ENERGY_MODE_AUS | Energysaving aus |
| 0x01 | ENERGY_MODE_PRODUCTION | Energysaving Produktion |
| 0x02 | ENERGY_MODE_SHIPMENT | Energysaving Shipment |
| 0x04 | ENERGY_MODE_REPAIR_SHOP | Energysaving Repair-Shop |
| 0x08 | ERROR | falscher Eingabewert |

<a id="table-tiefentl"></a>
### TIEFENTL

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 | 0x16 |
