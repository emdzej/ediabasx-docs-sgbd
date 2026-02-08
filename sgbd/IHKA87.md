# IHKA87.prg

- Jobs: [141](#jobs)
- Tables: [39](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | IHKA |
| ORIGIN | BMW EI-63 Peter Bauer |
| REVISION | 008.000 |
| AUTHOR | SiemensVDO I IP HVAC TA SW HMD, SiemensVDO I IP HVAC TA SW UDS, SiemensVDO I IP HVAC TA SW PaH |
| COMMENT | Muster-SGBD fuer PL2 |
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
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 4) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 4) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)
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
- [STATUS_TASTEN](#job-status-tasten) - Aktueller Zustand der ECU-Tasten (reportCurrentState). 1 = Taste gedrückt KWP2000: $30 InputOutputControlByLocalIdentifier $01 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) ECU-Tasten $01 ReportCurrentState Modus  : Default
- [STATUS_SZM_TASTEN](#job-status-szm-tasten) - Aktueller Zustand der SZM-Tasten (reportCurrentState). 1 = Taste gedrückt KWP2000: $30 InputOutputControlByLocalIdentifier $04 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) SZM-Tasten $01 ReportCurrentState Modus  : Default
- [STATUS_ANALOG_PORT](#job-status-analog-port) - Aktueller Zustand des Analog-Ports (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier (ANALOG_PORT_ARGUMENT) $01 reportCurrentState Modus  : Default
- [STATUS_POTI_ANALOG_PORT](#job-status-poti-analog-port) - Auslesen des Poti-Analog-Ausgangsports (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $10 InputOutputLocalIdetifier $01 reportCurrentState Modus  : Default
- [STATUS_SZM_ANALOG_PORT](#job-status-szm-analog-port) - Auslesen des SZM-Analog-Ausgangsports (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $11 InputOutputLocalIdetifier $01 reportCurrentState Modus  : Default
- [STATUS_SPANNUNGEN_ANALOG_PORT](#job-status-spannungen-analog-port) - Auslesen der Spannung des 12V-Ausgangs (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $12 InputOutputLocalIdetifier $01 reportCurrentState Modus  : Default
- [STATUS_SENSOREN_ANALOG_PORT](#job-status-sensoren-analog-port) - Auslesen der Sensoren (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $13 InputOutputLocalIdetifier $01 reportCurrentState Modus  : Default
- [STATUS_INNENFUEHLERGEBLAESE_ANALOG_PORT](#job-status-innenfuehlergeblaese-analog-port) - Auslesen der Innenfühlergebläsefrequenz (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $17 InputOutputLocalIdetifier $01 reportCurrentState Modus  : Default
- [STATUS_IHX_WERTE](#job-status-ihx-werte) - Lesen von IHX relevanten Daten KWP2000: $30 InputOutputControlByLocalIdentifier $16 InputOutputLocalIdetifier (IHX relevante Werte) $01 reportCurrentState Modus  : Default
- [STATUS_SZM_VARIANTE](#job-status-szm-variante) - Auslesen der SZM-Variante (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $05 InputOutputLocalIdetifier IOLI_VARIANTE_SZM $01 ReportCurrentState Modus  : Default
- [STATUS_TIMER_EINLAUFSCHUTZ](#job-status-timer-einlaufschutz) - Lesen des Status des Kompressor-Einlaufschutzes KWP2000: $21 ReadDataByLocalIdentifier $02 Timer Kompressor Einlaufschutz (recordLocalIdentifier) Modus  : Default
- [STATUS_ERROR_FLAGS](#job-status-error-flags) - Aktueller Zustand der Error-Flags (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $06 InputOutputLocalIdetifier (Error-Flags) $01 reportCurrentState Modus  : Default
- [STATUS_MOTOR_IDENT](#job-status-motor-ident) - Liefert die Identdaten des jeweiligen LIN-Bus-Schrittmotors (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier LIN-Bus-Teilnehmer $01 ReportCurrentState Modus  : Default
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - Lesen aller Soll- und Ist-Klappenpositionen in % 255 = Fehlerwert, Komponente nicht vorhanden KWP2000: $21 ReadDataByLocalIdentifier $04 Motor Klappenposition (recordLocalIdentifier) Modus  : Default
- [STATUS_MOTOR_FEHLER](#job-status-motor-fehler) - Liefert  interne Zähler für Motorfehler (reportCurrentState) KWP2000: $21 ReadDataByLocalIdentifier $06 InputOutputLocalIdetifier LIN-Bus-Teilnehmer (recordLocalIdentifier) Modus  : Default
- [STATUS_KLIMASYSTEM](#job-status-klimasystem) - Lesen aller ansprechbaren Adressen des LIN-Bus-Systems KWP2000: $21 ReadDataByLocalIdentifier $05 Status Klimasystem (recordLocalIdentifier) Modus  : Default
- [STATUS_FASTA_BLOCK](#job-status-fasta-block) - Aktueller Wert des FASTA-Blocks (je 16 Bit) KWP2000: $23 recordCommonIdentifier (High-Byte) $xx recordCommonIdentifier (Low-Byte) (FASTA-Block) Modus  : Default
- [STATUS_PTC_IDENT](#job-status-ptc-ident) - Liefert die Identdaten des PTC (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $26 InputOutputLocalIdetifier PTC $01 ReportCurrentState Modus  : Default
- [STEUERN_MOTOREN_EICHLAUF](#job-steuern-motoren-eichlauf) - Löst Klappeneichlauf aus und kalibriert die Schrittzahlen neu KWP2000: $31 StartRoutineByLocalIdetifier $20 routineLocalIdentifier Klappenmotoreneichlauf Modus  : Default
- [STATUS_MOTOR_EICHLAUF](#job-status-motor-eichlauf) - Lesen des aktuellen Status des Motoren-Eichlaufs KWP2000: $21 ReadDataByLocalIdentifier $10 Status Motor-Eichlauf (recordLocalIdentifier) Modus  : Default
- [FERTIGUNGSDATEN_LESEN](#job-fertigungsdaten-lesen) - Lesen der zuliefererspezifischen Fertigungsdaten KWP2000: $21 ReadDataByLocalIdentifier $07-$14,$FA-$FB systemSupplierSpecific Modus  : Default
- [STEUERN_KOMPRESSOR_EINLAUFSCHUTZ](#job-steuern-kompressor-einlaufschutz) - Setzen/Löschen des Kompressor Einlaufschutzes KWP2000: $3B WriteDataByLocalIdentifier $01 Kompressor Einlaufschutz (recordLocalIdentifier) $0x Ein/Aus (recordValue#1) Modus  : Default
- [FERTIGUNGSDATEN_SCHREIBEN](#job-fertigungsdaten-schreiben) - Schreiben der zuliefererspezifischen Fertigungsdaten KWP2000: $3B WriteDataByLocalIdentifier $07-$14, $FA-$FB systemSupplierSpecific Modus  : Default
- [STEUERN_DIAGNOSEBIT_SETZEN](#job-steuern-diagnosebit-setzen) - Setzen der I/O-Port-Diagnosebits (executeControlOption) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) $06 executeControlOption Modus  : Default
- [STEUERN_DIAGNOSEBIT_LOESCHEN](#job-steuern-diagnosebit-loeschen) - Rücksetzen der I/O-Port-Diagnosebits (returnControlToECU) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) $00 returnControlToECU Modus  : Default
- [STEUERN_SOLLWERTE_IHKA](#job-steuern-sollwerte-ihka) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $40 InputOutputLocalIdetifier (Sollwerte) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_TASTEN](#job-steuern-tasten) - Setzen von der ECU-Tasten (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $01 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT)Tastatur $07 ShortTermAdjustment Modus  : Default
- [STEUERN_SZM_TASTEN](#job-steuern-szm-tasten) - Setzen der SZM-Tasten (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $04 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) Tastatur-SZM $06 executeControlOption Modus  : Default
- [STEUERN_OUTPUTPORT](#job-steuern-outputport) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_12V_AUSGANG](#job-steuern-12v-ausgang) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $07 InputOutputLocalIdetifier (12V-Ausgang) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_5V_AUSGANG](#job-steuern-5v-ausgang) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $08 InputOutputLocalIdetifier (5V-Ausgang) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_INNENFUEHLERGEBLAESE](#job-steuern-innenfuehlergeblaese) - Setzen des Innenfühlergebläseausgangs (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $17 InputOutputLocalIdetifier (Innenfühlergebläse) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_SZM_AUSGAENGE](#job-steuern-szm-ausgaenge) - Setzen der PWM der Funktionsbeleuchtung des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $09 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) SZM-Ausgänge $07 ShortTermAdjustment Modus  : Default
- [STEUERN_DISPLAY](#job-steuern-display) - Setzen von Bitmustern des LCDs (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $0A InputOutputLocalIdentifier (I_O_PORT_ARGUMENT) LCD $07 ShortTermAdjustment Modus  : Default
- [STEUERN_FUNKTIONSBELEUCHTUNG](#job-steuern-funktionsbeleuchtung) - Setzen der Funktions-LEDs (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $02 InputOutputLocalIdentifier (I_O_PORT_ARGUMENT) LED-Port $07 ShortTermAdjustment Modus  : Default
- [STEUERN_SZM_FUNKTIONSBELEUCHTUNG](#job-steuern-szm-funktionsbeleuchtung) - Setzen der Funktions-SZM-LEDs (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $03 InputOutputLocalIdentifier (I_O_PORT_ARGUMENT) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_PWM_FUNKTIONSBELEUCHTUNG](#job-steuern-pwm-funktionsbeleuchtung) - Setzen der PWM der Funktionsbeleuchtung des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $30 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM Funktionsbeleuchtung ECU $07 ShortTermAdjustment Modus  : Default
- [STEUERN_PWM_RINGBELEUCHTUNG](#job-steuern-pwm-ringbeleuchtung) - Setzen der PWM der Ringsuchbeleuchtung des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $31 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM Ringsuchbeleuchtung ECU $07 ShortTermAdjustment Modus  : Default
- [STEUERN_PWM_TASTENBELEUCHTUNG](#job-steuern-pwm-tastenbeleuchtung) - Setzen der PWM der Tastensuchbeleuchtung des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $32 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM Tastensuchbeleuchtung ECU $07 ShortTermAdjustment Modus  : Default
- [STEUERN_PWM_DISPLAYBELEUCHTUNG](#job-steuern-pwm-displaybeleuchtung) - Setzen der PWM der Dispalybeleuchtung des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $33 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM Dispalybeleuchtung ECU $07 ShortTermAdjustment Modus  : Default
- [STEUERN_PWM_DISPLAYKONTRAST](#job-steuern-pwm-displaykontrast) - Setzen der PWM des Dispalykontrasts des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $34 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM Displaykontrast ECU $07 ShortTermAdjustment Modus  : Default
- [STEUERN_PWM_SZM_FUNKTIONSBELEUCHTUNG](#job-steuern-pwm-szm-funktionsbeleuchtung) - Setzen der PWM der ECU-Suchbeleuchtung (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $35 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM ECU-Suchbeleuchtung $07 ShortTermAdjustment Modus  : Default
- [STEUERN_PWM_SZM_SUCHBELEUCHTUNG](#job-steuern-pwm-szm-suchbeleuchtung) - Setzen der PWM der SZM-Suchbeleuchtung (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $36 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM SZM-Suchbeleuchtung $07 ShortTermAdjustment Modus  : Default
- [STEUERN_GEBLAESE](#job-steuern-geblaese) - Setzen der Gebläseleistung (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $15 InputOutputLocalIdetifier (Gebläse) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_BELEUCHTUNG](#job-steuern-beleuchtung) - Setzen aller Beleuchtungen der ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $37 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) Beleuchtung ECU $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_UMLUFT](#job-steuern-klappe-umluft) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $20 InputOutputLocalIdetifier (Frischluft/Umluft/Staudruckklappe) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_MISCHLUFT_LINKS](#job-steuern-klappe-mischluft-links) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $21 InputOutputLocalIdetifier (Mischluftklappe links) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_MISCHLUFT_RECHTS](#job-steuern-klappe-mischluft-rechts) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $22 InputOutputLocalIdetifier (Mischluftklappe rechts) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_BELUEFTUNG](#job-steuern-klappe-belueftung) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $23 InputOutputLocalIdetifier (Belüftung) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FUSSRAUM](#job-steuern-klappe-fussraum) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $24 InputOutputLocalIdetifier (Fußraum) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_DEFROST](#job-steuern-klappe-defrost) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $25 InputOutputLocalIdetifier (Defrost) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FOND](#job-steuern-klappe-fond) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $27 InputOutputLocalIdetifier (Fondbelüftung nur E9X) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_SCHICHTUNG](#job-steuern-klappe-schichtung) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $28 InputOutputLocalIdetifier (Schichtung nur E9X) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_PTC](#job-steuern-ptc) - Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $26 InputOutputLocalIdetifier (Zuheizer) $07 ShortTermAdjustment Modus  : Default
- [STEUERN_AUTOADRESSIERUNG](#job-steuern-autoadressierung) - Startet die LIN-Bus Autoadressierung KWP2000: $31 StartRoutineByLocalIdetifier $22 routineLocalIdentifier LIN-Bus Autoadressierung Modus  : Default
- [STEUERN_MOTOR_FEHLER_LOESCHEN](#job-steuern-motor-fehler-loeschen) - Löscht Zähler für Motorfehler KWP2000: $31 StartRoutineByLocalIdetifier $24 routineLocalIdentifier LIN-Bus Motorfehler löschen Modus  : Default
- [STEUERN_EINZELADRESSIERUNG](#job-steuern-einzeladressierung) - Startet die LIN-Bus Einzeladressierung KWP2000: $31 StartRoutineByLocalIdetifier $23 routineLocalIdentifier LIN-Bus Einzeladressierung Modus  : Default
- [STEUERN_DIAGNOSETESTBETRIEB_PERMANENT](#job-steuern-diagnosetestbetrieb-permanent) - Dauerhaftes Setzen oder Löschen des Diagosetestbetriebs KWP2000: $3B WriteDataByLocalIdentifier $03 Diagnosetestbetrieb permanent(recordLocalIdentifier) $0x Ein/Aus (recordValue#1) Modus  : Default
- [STEUERN_RESET_LIN](#job-steuern-reset-lin) - Löst Rücksetzen des LIN-Bus aus KWP2000: $31 StartRoutineByLocalIdetifier $25 routineLocalIdentifier Reset LIN-Bus Modus  : Default
- [STEUERN_DREHMOMENT_MESSUNG](#job-steuern-drehmoment-messung) - Start der AD-Wert-Aufnahme während der Drehmomentmessung in diversen Rastpunkten KWP2000: $31 StartRoutineByLocalIdetifier $26 routineLocalIdentifier Drehmomentmessung Modus  : Default
- [C_C_LOESCHEN](#job-c-c-loeschen) - KWP2000: $31 StartRoutineByLocalIdetifier $21 routineLocalIdentifier Löschen Codierdatensatz Modus  : Default
- [STATUS_SHZH_IDENT](#job-status-shzh-ident) - BMW Zusammenbaunummer auslesen
- [STATUS_SHZH_BMW_ZUSAMMENBAUNUMMER](#job-status-shzh-bmw-zusammenbaunummer) - BMW Zusammenbaunummer auslesen
- [STATUS_SHZH_BMW_HARDWARENUMMER](#job-status-shzh-bmw-hardwarenummer) - BMW Hardwarenummer auslesen
- [STATUS_SHZH_BMW_HARDWARESTERNNUMMER](#job-status-shzh-bmw-hardwaresternnummer) - BMW Hardwaresternnummer auslesen
- [STATUS_SHZH_VERSIONIERUNG](#job-status-shzh-versionierung) - Versionsdaten auslesen
- [STEUERN_SHZH_KALTBEFEUERUNG](#job-steuern-shzh-kaltbefeuerung) - Kaltbefeuerung aktivieren/deaktivieren
- [STATUS_SHZH_TESTLAUF](#job-status-shzh-testlauf) - Testlauf (vom Prüfbetrieb) auslesen
- [STATUS_SHZH_BETRIEBSDATEN](#job-status-shzh-betriebsdaten) - Betriebsdaten (Betriebsdauer, Brenndauer und Einschaltzähler) auslesen
- [STATUS_SHZH_IO](#job-status-shzh-io) - I/O Messwerte (Betriebsspannung, Funktionszustand, I/O Status, Glüelementwiederstand) auslesen
- [STATUS_SHZH](#job-status-shzh) - Der Job fasst den Job I/O Messwerte  (Betriebsspannung, Funktionszustand, I/O Status, Glüelementwiederstand) auslesen und den Job Status Applaktionsnachricht
- [SHZH_FEHLERSPEICHER_LOESCHEN](#job-shzh-fehlerspeicher-loeschen) - Lieferantenfehlerspeicher loeschen
- [SHZH_FEHLERSPEICHER_LESEN](#job-shzh-fehlerspeicher-lesen) - Lieferantenfehlerspeicher lesen
- [STATUS_SHZH_KONFIGURATION_LESEN](#job-status-shzh-konfiguration-lesen) - Konfiguration lesen
- [SHZH_KONFIGURATION_SCHREIBEN](#job-shzh-konfiguration-schreiben) - Konfiguration lesen
- [SHZH_STEUERGERAET_RESET](#job-shzh-steuergeraet-reset) - Reset des Steuergerätes
- [SHZH_BAUDRATE_KONFIGURIEREN](#job-shzh-baudrate-konfigurieren) - Baudrate konfigurieren
- [STEUERN_SHZH_KOMPONENTEN](#job-steuern-shzh-komponenten) - Komponententest
- [STEUERN_SHZH_UMWAELZPUMPE](#job-steuern-shzh-umwaelzpumpe) - sTEUERN UMWAELZPUMPE
- [STEUERN_SHZH_UMSCHALTVENTIL](#job-steuern-shzh-umschaltventil) - Steuern Umschaltventil Ventil steht auf SH Kreislauf=bestromt=100%
- [STEUERN_SHZH](#job-steuern-shzh) - Steuern SHZH BITTE BEACHTEN: Das Gerät schaltet sich nach Erreichen des Volllast automatisch ab!
- [STEUERN_SHZH_EXPERT](#job-steuern-shzh-expert) - Prüfbetrieb Expert BITTE BEACHTEN: Prüfbetrieb 1 : Das Gerät schaltet sich nach Erreichen des Volllast automatisch ab! Prüfbetrieb 2: Das Gerät schaltet sich nach 10min automatisch ab!
- [STEUERN_SHZH_HGV_RESET](#job-steuern-shzh-hgv-reset) - Heizgeräteverriegelung reset
- [STEUERN_SHZH_TESTABBRUCH](#job-steuern-shzh-testabbruch) - Testabbruch
- [STEUERN_SHZH_LEITUNGSBEFUELLUNG](#job-steuern-shzh-leitungsbefuellung) - Leitungsbefuellung
- [STATUS_SHZH_SERIENNUMMER](#job-status-shzh-seriennummer) - Heizgerätenummer auslesen
- [STATUS_SHZH_LIN_PRODUCT_ID](#job-status-shzh-lin-product-id) - LIN Product Identification auslesen
- [STATUS_SHZH_UEBER_APP_NACHRICHT](#job-status-shzh-ueber-app-nachricht) - Statusinformation über Applikationsnachricht auslesen
- [STATUS_KLAPPEN_VERSTELLBEREICH](#job-status-klappen-verstellbereich) - Lesen des aktuellen Status der Verstellbereiche alle Motoren ermittelt über den Eichlauf. 65535 = Fehlerwert, Komponente nicht vorhanden KWP2000: $21 ReadDataByLocalIdentifier $15 Klappen Verstellbereich (recordLocalIdentifier) Modus  : Default

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

<a id="job-cbs-info"></a>
### CBS_INFO

Ausgabe der CBS-Version

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ECU_NAME | string | Steuergeraetename |
| CBS_VERSION_TEXT | string | CBS Version im Klartext |
| CBS_VERSION_HEX | string | CBS Version als Wert |

<a id="job-cbs-daten-lesen"></a>
### CBS_DATEN_LESEN

CBS Daten auslesen (fuer CBS-Version 4) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Hex-String |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| ANZ_CBS | int | Anzahl der CBS - Umfaenge im Steuergeraet |
| ID_FN_CBS_MESS_WERT | int | CBS-Kennung als Zahl |
| ID_FN_CBS_MESS_HEX | string | CBS-Kennung als Hex-String |
| ID_FN_CBS_MESS_TEXT | string | table CbsKennung CBS_K CBS_K_TEXT CBS-Kennung im Klartext |
| RMMI_CBS_WERT | int | Restlaufleistung |
| RMMI_CBS_EINH | string | Information zur Restlaufleistung |
| ST_UN_CBS_WERT | int | Einheit Restlaufleistung als Zahl |
| ST_UN_CBS_HEX | string | Einheit Restlaufleistung als Hex-String |
| ST_UN_CBS_TEXT | string | Einheit Restlaufleistung im Klartext |
| COU_RSTG_CBS_MESS_WERT | int | Servicezaehler |
| COU_RSTG_CBS_MESS_EINH | string | Zaehler |
| AVAI_CBS_WERT | int | Verfuegbarkeit in % |
| AVAI_CBS_EINH | string | % |
| AVAI_CBS_WERT_OEL | int | Verfuegbarkeit OEL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_CSF | int | Verfuegbarkeit CSF in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BATT | int | Verfügbarkeit BATT in %, für Prüfablauf Bandende |
| AVAI_CBS_WERT_VTG | int | Verfügbarkeit VTG in %, für Prüfablauf Bandende |
| AVAI_CBS_WERT_FILT | int | Verfuegbarkeit FILT in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_V | int | Verfuegbarkeit BR_V in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_H | int | Verfuegbarkeit BR_H in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BRFL | int | Verfuegbarkeit BRFL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_ZKRZ | int | Verfuegbarkeit ZKRZ in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_SIC | int | Verfuegbarkeit SIC in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_KFL | int | Verfuegbarkeit KFL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_UEB | int | Verfuegbarkeit UEB in %, fuer Pruefablauf Bandende |
| ZIEL_MM_WERT | int | Ziel-Monat |
| ZIEL_MM_EINH | string | Monat |
| ZIEL_YY_WERT | int | Ziel-Jahr |
| ZIEL_YY_EINH | string | Jahr |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall |
| FRC_INTM_WAY_CBS_EINH | string | Information zur Prognose Wegintervall |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall |
| MANIP_CBS | int | Manipulationsbyte |
| MANIP_CBS_TEXT | string | Manipulationsbyte im Klartext |
| Res_Byte | int | Reserve Byte (noch unbenutzt) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbs-reset"></a>
### CBS_RESET

CBS Daten Zuruecksetzen (fuer CBS-Version 4) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, ZKrz, Sic, Kfl, TUV, AU, Ueb Werte externe Umfaenge: Oel, Br_v, Br_h, Filt, CSF, Batt, VTG Defaultwert: 0x00 (ungueltig) |
| CBS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, keine Aenderung: 255 Defaultwert: 100 |
| CBS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, Erhoehung der Anzahl um +1: 31 Defaultwert: 31 |
| CBS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter, keine Aenderung: 255 Defaultwert: 255 |
| CBS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter, keine Aenderung: 255 Defaultwert: 255 |
| RMM_CBS_WERT | int | Restlaufleistung in km oder % (siehe Argument Einheit) Schalter, keine Aenderung: 8000h Defaultwert: 8000h |
| ST_UN_CBS_RSTG | int | Einheit Restlaufleistung 0hex -&gt; % 1hex -&gt; km*10 Fhex -&gt; d.c. Defaultwert: Fh |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall Umrechnung 1-254*1000km Schalter, setzt auf Defaultwert zurueck: 0h Schalter, keine Aenderung: FFh Defaultwert: FFh |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall 0-254 Monate Schalter, keine Aenderung: FFh Defaultwert: FFh |
| Res_Byte | int | Reserve Byte (noch unbenutzt) Defaultwert: 00h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
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

<a id="job-status-tasten"></a>
### STATUS_TASTEN

Aktueller Zustand der ECU-Tasten (reportCurrentState). 1 = Taste gedrückt KWP2000: $30 InputOutputControlByLocalIdentifier $01 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) ECU-Tasten $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_REST | unsigned char | Aktueller Zustand der Restwärme-Taste |
| STAT_DEF | unsigned char | Aktueller Zustand der Defroster-Taste |
| STAT_AC_MAX | unsigned char | Aktueller Zustand der AC-Max-Taste |
| STAT_AUTO | unsigned char | Aktueller Zustand der Automatik-Taste |
| STAT_LV_OBEN | unsigned char | Aktueller Zustand der Luftverteilung-Oben-Taste |
| STAT_LV_MITTE | unsigned char | Aktueller Zustand der Luftverteilung-Mitte-Taste |
| STAT_LV_UNTEN | unsigned char | Aktueller Zustand der Luftverteilung-Unten-Taste |
| STAT_AC | unsigned char | Aktueller Zustand der Klimakompressor-Ein-Taste |
| STAT_AUC | unsigned char | Aktueller Zustand der Automatische-Umluft-Taste |
| STAT_GBL_PLUS | unsigned char | Aktueller Zustand der Gebläse-Plus-Taste |
| STAT_GBL_MINUS | unsigned char | Aktueller Zustand der Gebläse-Minus-Taste |
| STAT_HHS | unsigned char | Aktueller Zustand der Heckscheibenheizung-Taste |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-szm-tasten"></a>
### STATUS_SZM_TASTEN

Aktueller Zustand der SZM-Tasten (reportCurrentState). 1 = Taste gedrückt KWP2000: $30 InputOutputControlByLocalIdentifier $04 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) SZM-Tasten $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HDC | unsigned char | Aktueller Zustand der Hill Decent control Taste |
| STAT_SITZHEIZUNG_LINKS | unsigned char | Aktueller Zustand der Sitzheizung links Taste |
| STAT_PDC | unsigned char | Aktueller Zustand der PDC-Taste |
| STAT_SITZHEIZUNG_RECHTS | unsigned char | Aktueller Zustand der Sitzheizung rechts |
| STAT_SONNENROLLO | unsigned char | Aktueller Zustand der Sonnenrollo-Taste |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-port"></a>
### STATUS_ANALOG_PORT

Aktueller Zustand des Analog-Ports (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier (ANALOG_PORT_ARGUMENT) $01 reportCurrentState Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANALOG_PORT_ARGUMENT | unsigned char | Nummer des Analog-Ports table IOPortTab Portnumber,Portname Wenn keine Eingabe: default = 0x10 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANALOG_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| STAT_ANALOG_PORT_EINH | string | je 8 Bit Hex-Rohwerte der AD-Wandler Hex |
| STAT_SOLLWERT_RECHTS_PU_WERT | unsigned char | Poti Temperatursollwert rechts mit geschaltetem Pull-Up Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_RECHTS_PD_WERT | unsigned char | Poti Temperatursollwert rechts mit geschaltetem Pull-Down Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_RECHTS_IN_TOT_WERT | unsigned char | Poti Temperatursollwert rechts im Totbereich Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_LINKS_PU_WERT | unsigned char | Poti Temperatursollwert links mit geschaltetem Pull-Up Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_LINKS_PD_WERT | unsigned char | Poti Temperatursollwert links mit geschaltetem Pull-Down Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_LINKS_IN_TOT_WERT | unsigned char | Poti Temperatursollwert links im Totbereich Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_MAX_WERT | unsigned char | Poti Temperatursollwert max Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_MIN_WERT | unsigned char | Poti Temperatursollwert min Bereich: 0x00 bis 0xFF |
| STAT_SCHICHTUNG_WERT | unsigned char | Poti Schichtung Bereich: 0x00 bis 0xFF |
| STAT_SZM_TAST4_WERT | unsigned char | Schaltzentrum-Mitte Taste 4 Bereich: 0x00 bis 0xFF |
| STAT_SZM_TAST3_WERT | unsigned char | Schaltzentrum-Mitte Taste 3 Bereich: 0x00 bis 0xFF |
| STAT_SZM_STROM_5V_WERT | unsigned char | Schaltzentrum-Mitte Strom 5V-Ausgang Bereich: 0x00 bis 0xFF |
| STAT_SZM_CODIER1_WERT | unsigned char | Schaltzentrum-Mitte Codierspannung1 Bereich: 0x00 bis 0xFF |
| STAT_SZM_CODIER2_WERT | unsigned char | Schaltzentrum-Mitte Codierspannung2 Bereich: 0x00 bis 0xFF |
| STAT_12V_AUSGANG_WERT | unsigned char | Spannung der Klemme 30 Bereich: 0x00 bis 0xFF |
| STAT_TEMP_ML_RECHTS_WERT | unsigned char | Temperatur Mischluftklappe rechts Bereich: 0x00 bis 0xFF |
| STAT_TEMP_ML_LINKS_WERT | unsigned char | Temperatur Mischluftklappe links Bereich: 0x00 bis 0xFF |
| STAT_TEMP_FUSSR_RECHTS_WERT | unsigned char | Temperatur Fußraum rechts Bereich: 0x00 bis 0xFF |
| STAT_TEMP_FUSSR_LINKS_WERT | unsigned char | Temperatur Fußraum links Bereich: 0x00 bis 0xFF |
| STAT_TEMP_VERDAMPFER_WERT | unsigned char | Temperatur Verdampfer Bereich: 0x00 bis 0xFF |
| STAT_TEMP_INNEN_WERT | unsigned char | Temperatur Innenraum Bereich: 0x00 bis 0xFF |
| STAT_SOLARSENSOR_WERT | unsigned char | Solarsensor Bereich: 0x00 bis 0xFF |
| STAT_TEMP_DISPLAY_WERT | unsigned char | Temperatur Display Bereich: 0x00 bis 0xFF |
| STAT_GEBL_DIAGNOSE_WERT | unsigned char | Gebläsediagnoszähler Bereich: 0x00 bis 0xFF |
| STAT_INFL_GEBL_DIAGNOSE_WERT | unsigned char | Innenfühlergebläsefrequenz [Hz] Bereich: 0x00 bis 0xFF |
| STAT_Y_WERT | char | Aktueller Y Wert in Prozent (Auflösung 1 Prozent)[-128 bis +127] |
| STAT_Y_EINH | string | % |
| STAT_AUC_WERT | unsigned char | Aktuelle AUC-Stufe (Auflösung je 1 Stufe) [0-6] |
| STAT_AUC_EINH | string | Stufe |
| STAT_DRUCK_KAELTEMITTEL_WERT | unsigned char | Aktueller Kältemitteldruck in bar (Auflösung 1 bar) [0-127] (gemäß CAN-Datenbasis 4.1.0) |
| STAT_DRUCK_KAELTEMITTEL_EINH | string | bar |
| STAT_KLEMME_30_WERT | unsigned char | Aktuelle IHX-Versorgungsspannung in Volt (Auflösung 1 V) [0-25] |
| STAT_KLEMME_30_EINH | string | Volt |
| STAT_SOLAR_WERT | char | Aktueller Wert des Solarsensors in W/qm (Auflösung 1 W/qm) [-127 bis + 128] |
| STAT_SOLAR_EINH | string | W/qm |
| STAT_T_AUSSEN_WERT | char | Aktuelle Aussentemperatur in Grad Celsius (Auflösung 1 bar) [-40 bis +85](gemäß CAN-Datenbasis 4.1.0) |
| STAT_T_AUSSEN_EINH | string | Grad Celsius |
| STAT_T_INNEN_WERT | char | Aktuelle Temperaur des Innenraumfühlers in Grad Celsius (Auflösung 1 Grad Celsius) [-127 bis + 128] |
| STAT_T_INNEN_EINH | string | Grad Celsius |
| STAT_T_VERDAMPFER_WERT | char | Aktuelle Verdampfertemperatur in Grad Celsius (Auflösung 1 Grad Celsius) [-127 bis + 128] |
| STAT_T_VERDAMPFER_EINH | string | Grad Celsius |
| STAT_T_BELUEFTUNG_WERT | char | Aktueller Wert der Ausblastemperatur der Belüftungsebene in Grad Celsius (Auflösung 1 Grad Celsius) [-127 bis + 128] |
| STAT_T_BELUEFTUNG_EINH | string | Grad Celsius |
| STAT_T_FUSSRAUM_WERT | char | Aktueller Wert der Ausblastemperatur der Fussraumebene in Grad Celsius (Auflösung 1 Grad Celsius) [-127 bis + 128] |
| STAT_T_FUSSRAUM_EINH | string | Grad Celsius |
| STAT_EC_LUEFTER_STUFE_WERT | unsigned char | Aktuell gesetzte Stufe des EC-Luefters (Auflösung je 1 Stufe, gemäß CAN-Datenbasis 4.1.0) |
| STAT_EC_LUEFTER_STUFE_EINH | string | Stufe |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-poti-analog-port"></a>
### STATUS_POTI_ANALOG_PORT

Auslesen des Poti-Analog-Ausgangsports (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $10 InputOutputLocalIdetifier $01 reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANALOG_PORT_EINH | string | je 8 Bit Hex-Rohwerte der AD-Wandler) Hex |
| STAT_ANALOG_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| STAT_SOLLWERT_RECHTS_PU_WERT | unsigned char | Poti Temperatursollwert rechts mit geschaltetem Pull-Up (je 8 Bit Hex-Rohwerte der AD-Wandler) Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_RECHTS_PD_WERT | unsigned char | Poti Temperatursollwert rechts mit geschaltetem Pull-Down Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_RECHTS_IN_TOT_WERT | unsigned char | Poti Temperatursollwert rechts im Totbereich Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_LINKS_PU_WERT | unsigned char | Poti Temperatursollwert links mit geschaltetem Pull-Up Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_LINKS_PD_WERT | unsigned char | Poti Temperatursollwert links mit geschaltetem Pull-Down Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_LINKS_IN_TOT_WERT | unsigned char | Poti Temperatursollwert links im Totbereich Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_MAX_WERT | unsigned char | Poti Temperatursollwert max Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_MIN_WERT | unsigned char | Poti Temperatursollwert min Bereich: 0x00 bis 0xFF |
| STAT_SCHICHTUNG_WERT | unsigned char | Poti Schichtung Bereich: 0x00 bis 0xFF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-szm-analog-port"></a>
### STATUS_SZM_ANALOG_PORT

Auslesen des SZM-Analog-Ausgangsports (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $11 InputOutputLocalIdetifier $01 reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANALOG_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| STAT_ANALOG_PORT_EINH | string | je 8 Bit Hex-Rohwerte der AD-Wandler) Hex |
| STAT_SZM_TAST4_WERT | unsigned char | Schaltzentrum-Mitte Taste 4 Bereich: 0x00 bis 0xFF |
| STAT_SZM_TAST3_WERT | unsigned char | Schaltzentrum-Mitte Taste 3 Bereich: 0x00 bis 0xFF |
| STAT_SZM_STROM_5V_WERT | unsigned char | Schaltzentrum-Mitte Strom 5V-Ausgang Bereich: 0x00 bis 0xFF |
| STAT_SZM_CODIER1_WERT | unsigned char | Schaltzentrum-Mitte Codierspannung1 Bereich: 0x00 bis 0xFF |
| STAT_SZM_CODIER2_WERT | unsigned char | Schaltzentrum-Mitte Codierspannung2 Bereich: 0x00 bis 0xFF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spannungen-analog-port"></a>
### STATUS_SPANNUNGEN_ANALOG_PORT

Auslesen der Spannung des 12V-Ausgangs (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $12 InputOutputLocalIdetifier $01 reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANALOG_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| STAT_ANALOG_PORT_EINH | string | je 8 Bit Hex-Rohwerte der AD-Wandler) Hex |
| STAT_12V_AUSGANG_WERT | unsigned char | Spannung der Klemme 30 Bereich: 0x00 bis 0xFF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sensoren-analog-port"></a>
### STATUS_SENSOREN_ANALOG_PORT

Auslesen der Sensoren (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $13 InputOutputLocalIdetifier $01 reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANALOG_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| STAT_ANALOG_PORT_EINH | string | je 8 Bit Hex-Rohwerte der AD-Wandler) Hex |
| STAT_TEMP_ML_RECHTS_WERT | unsigned char | Temperatur Mischluftklappe rechts Bereich: 0x00 bis 0xFF |
| STAT_TEMP_ML_LINKS_WERT | unsigned char | Temperatur Mischluftklappe links Bereich: 0x00 bis 0xFF |
| STAT_TEMP_FUSSR_RECHTS_WERT | unsigned char | Temperatur Fußraum rechts Bereich: 0x00 bis 0xFF |
| STAT_TEMP_FUSSR_LINKS_WERT | unsigned char | Temperatur Fußraum links Bereich: 0x00 bis 0xFF |
| STAT_TEMP_VERDAMPFER_WERT | unsigned char | Temperatur Verdampfer Bereich: 0x00 bis 0xFF |
| STAT_TEMP_INNEN_WERT | unsigned char | Temperatur Innenraum Bereich: 0x00 bis 0xFF |
| STAT_SOLARSENSOR_WERT | unsigned char | Solarsensor Bereich: 0x00 bis 0xFF |
| STAT_TEMP_DISPLAY_WERT | unsigned char | Temperatur Display Bereich: 0x00 bis 0xFF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-innenfuehlergeblaese-analog-port"></a>
### STATUS_INNENFUEHLERGEBLAESE_ANALOG_PORT

Auslesen der Innenfühlergebläsefrequenz (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $17 InputOutputLocalIdetifier $01 reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANALOG_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| STAT_ANALOG_PORT_EINH | string | je 8 Bit Hex-Rohwerte der AD-Wandler) Hex |
| STAT_GEBL_DIAGNOSE_WERT | unsigned char | Gebläsediagnoszähler Bereich: 0x00 bis 0xFF |
| STAT_INFL_GEBL_DIAGNOSE_WERT | unsigned char | Innenfühlergebläsefrequenz [Hz] Bereich: 0x00 bis 0xFF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ihx-werte"></a>
### STATUS_IHX_WERTE

Lesen von IHX relevanten Daten KWP2000: $30 InputOutputControlByLocalIdentifier $16 InputOutputLocalIdetifier (IHX relevante Werte) $01 reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANALOG_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| STAT_Y_WERT | char | Aktueller Y Wert in Prozent (Auflösung 1 Prozent)[-128 bis +127] |
| STAT_Y_EINH | string | % |
| STAT_AUC_WERT | unsigned char | Aktuelle AUC-Stufe (Auflösung je 1 Stufe) [0-6] |
| STAT_AUC_EINH | string | Stufe |
| STAT_DRUCK_KAELTEMITTEL_WERT | real | Aktueller Kältemitteldruck in bar (Auflösung 1 bar) [0-127] (gemäß CAN-Datenbasis 4.1.0) |
| STAT_DRUCK_KAELTEMITTEL_EINH | string | bar |
| STAT_KLEMME_30_WERT | real | Aktuelle IHX-Versorgungsspannung in Volt (Auflösung 1 V) [0-25] |
| STAT_KLEMME_30_EINH | string | Volt |
| STAT_SOLAR_WERT | real | Aktueller Wert des Solarsensors in W/qm (Auflösung 1 W/qm) [0 bis 1200] |
| STAT_SOLAR_EINH | string | W/qm |
| STAT_T_AUSSEN_WERT | real | Aktuelle Aussentemperatur in Grad Celsius (Auflösung 1 bar) [-40 bis +85](gemäß CAN-Datenbasis 4.1.0) |
| STAT_T_AUSSEN_EINH | string | Grad Celsius |
| STAT_T_INNEN_WERT | char | Aktuelle Temperaur des Innenraumfühlers in Grad Celsius (Auflösung 1 Grad Celsius) [-127 bis + 128] |
| STAT_T_INNEN_EINH | string | Grad Celsius |
| STAT_T_VERDAMPFER_WERT | char | Aktuelle Verdampfertemperatur in Grad Celsius (Auflösung 1 Grad Celsius) [-127 bis + 128] |
| STAT_T_VERDAMPFER_EINH | string | Grad Celsius |
| STAT_T_BELUEFTUNG_WERT | char | Aktueller Wert der Ausblastemperatur der Belüftungsebene in Grad Celsius (Auflösung 1 Grad Celsius) [-127 bis + 128] |
| STAT_T_BELUEFTUNG_EINH | string | Grad Celsius |
| STAT_T_FUSSRAUM_WERT | char | Aktueller Wert der Ausblastemperatur der Fussraumebene in Grad Celsius (Auflösung 1 Grad Celsius) [-127 bis + 128] |
| STAT_T_FUSSRAUM_EINH | string | Grad Celsius |
| STAT_EC_LUEFTER_STUFE_WERT | unsigned char | Aktuell gesetzte Stufe des EC-Luefters (Auflösung je 1 Stufe, gemäß CAN-Datenbasis 4.1.0) |
| STAT_EC_LUEFTER_STUFE_EINH | string | Stufe |
| STAT_T_SOLLWERT_FA_EINH | string | Grad Celsius |
| STAT_T_SOLLWERT_FA_WERT | real | Aktueller Temperatursollwert in Grad Celsius (Auflösung 0,5 Grad Celsius) [0 bis 127,5] |
| STAT_T_SOLLWERT_BF_EINH | string | Grad Celsius |
| STAT_T_SOLLWERT_BF_WERT | real | Aktueller Temperatursollwert in Grad Celsius (Auflösung 0,5 Grad Celsius) [0 bis 127,5] |
| STAT_KLIMAKOMPRESSOR_EIN_WERT | char | Aktueller Status der Klimafunktion [0=AUS, 1=EIN, -1=Wert nicht verfügbar (altes SG)] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-szm-variante"></a>
### STATUS_SZM_VARIANTE

Auslesen der SZM-Variante (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $05 InputOutputLocalIdetifier IOLI_VARIANTE_SZM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SZM_VARIANTE | unsigned char | Aktuelle SZM-Variante (1-39) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-timer-einlaufschutz"></a>
### STATUS_TIMER_EINLAUFSCHUTZ

Lesen des Status des Kompressor-Einlaufschutzes KWP2000: $21 ReadDataByLocalIdentifier $02 Timer Kompressor Einlaufschutz (recordLocalIdentifier) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TIMER_EINH | string | Sekunden |
| STAT_TIMER_WERT | unsigned char | Aktuelle Restzeit des Einlaufschutzzählers in Sekunden (0=abgelaufen) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-error-flags"></a>
### STATUS_ERROR_FLAGS

Aktueller Zustand der Error-Flags (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $06 InputOutputLocalIdetifier (Error-Flags) $01 reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_NO_CAN_ERROR | unsigned char | Aktueller Zustand des Error-Flags des CAN-Transceiver |
| STAT_UEBERSTROM_12V_AUSGANG | unsigned char | Aktueller Zustand der Überstromerkennung des 12V-Ausgangs |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-ident"></a>
### STATUS_MOTOR_IDENT

Liefert die Identdaten des jeweiligen LIN-Bus-Schrittmotors (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier LIN-Bus-Teilnehmer $01 ReportCurrentState Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LIN_DEVICE_ARGUMENT | unsigned char | LIN-Bus-Teilnehmer table IOPortTab Portnumber,Portname Wenn keine Eingabe: default = 0x20 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_REFERENCE | unsigned char | Aktuelle Referenznummer |
| STAT_SUPPLIER | unsigned char | Aktuelle Suppliernummer |
| STAT_ASIC_NR | unsigned char | Aktuelle ASIC-Nummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-klappenposition"></a>
### STATUS_MOTOR_KLAPPENPOSITION

Lesen aller Soll- und Ist-Klappenpositionen in % 255 = Fehlerwert, Komponente nicht vorhanden KWP2000: $21 ReadDataByLocalIdentifier $04 Motor Klappenposition (recordLocalIdentifier) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTOR_DATEN | binary | Soll-Klappenpositionen in % Byte0=PTC Byte1=DEF Byte2=FL/UML/SD Byte3=Mischluft rechts Byte4=Fußraum Byte5=Belüftung Byte6=Mischluft links Byte7=Fond (nur E9X) Byte8=Schichtung (nur E9X) Ist-Klappenpositionen in % Byte9=PTC Byte10=DEF Byte11=FL/UML/SD Byte12=Mischluft rechts Byte13=Fußraum Byte14=Belüftung Byte15=Mischluft links Byte16=Fond (nur E9X) Byte17=Schichtung (nur E9X) Bei SG für SGBD-Version vor 3.200 wird für die Ist-Position die Soll-Position ausgegeben! |
| STAT_MOTOR_EINH | string | % alle Motoreinheiten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PTC_WERT | unsigned char | Aktueller Soll-Heizanforderung an den elektrischen Zuheizer PTC |
| STAT_DEFROST_WERT | unsigned char | Aktuelle Soll-Klappenposition des Defrostmotors |
| STAT_FRISCHLUFT_UMLUFT_WERT | unsigned char | Aktuelle Soll-Klappenposition des Frischluft- /Umluftmotors |
| STAT_MISCHLUFT_RECHTS_WERT | unsigned char | Aktuelle Soll-Klappenposition des Mischluftmotors rechts |
| STAT_FUSSRAUM_WERT | unsigned char | Aktuelle Soll-Klappenposition des Fussraummotors |
| STAT_BELUEFTUNG_WERT | unsigned char | Aktuelle Soll-Klappenposition des Belüftungsmotors |
| STAT_MISCHLUFT_LINKS_WERT | unsigned char | Aktuelle Soll-Klappenposition des Mischluftmotors links |
| STAT_FOND_WERT | unsigned char | Aktuelle Soll-Klappenposition des Fondschichtungsmotors |
| STAT_FRONT_SCHICHTUNG_WERT | unsigned char | Aktuelle Soll-Klappenposition des Frontschichtungsmotors |
| STAT_PTC_IST_WERT | unsigned char | Aktueller Ist-Heizanforderung an den elektrischen Zuheizer PTC |
| STAT_DEFROST_IST_WERT | unsigned char | Aktuelle Ist-Klappenposition des Defrostmotors |
| STAT_FRISCHLUFT_UMLUFT_IST_WERT | unsigned char | Aktuelle Ist-Klappenposition des Frischluft- /Umluftmotors |
| STAT_MISCHLUFT_RECHTS_IST_WERT | unsigned char | Aktuelle Ist-Klappenposition des Mischluftmotors rechts |
| STAT_FUSSRAUM_IST_WERT | unsigned char | Aktuelle Ist-Klappenposition des Fussraummotors |
| STAT_BELUEFTUNG_IST_WERT | unsigned char | Aktuelle Ist-Klappenposition des Belüftungsmotors |
| STAT_MISCHLUFT_LINKS_IST_WERT | unsigned char | Aktuelle Ist-Klappenposition des Mischluftmotors links |
| STAT_FOND_IST_WERT | unsigned char | Aktuelle Ist-Klappenposition des Fondschichtungsmotors |
| STAT_FRONT_SCHICHTUNG_IST_WERT | unsigned char | Aktuelle Ist-Klappenposition des Frontschichtungsmotors |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-fehler"></a>
### STATUS_MOTOR_FEHLER

Liefert  interne Zähler für Motorfehler (reportCurrentState) KWP2000: $21 ReadDataByLocalIdentifier $06 InputOutputLocalIdetifier LIN-Bus-Teilnehmer (recordLocalIdentifier) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BLOCKIERUNG | unsigned char | Häufigkeitszähler Blockierung |
| STAT_FEHLENDE_ANTWORT | unsigned char | Häufigkeitszähler fehlende Antwort |
| STAT_INTERNER_FEHLER | unsigned char | Häufigkeitszähler interner Fehler |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klimasystem"></a>
### STATUS_KLIMASYSTEM

Lesen aller ansprechbaren Adressen des LIN-Bus-Systems KWP2000: $21 ReadDataByLocalIdentifier $05 Status Klimasystem (recordLocalIdentifier) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLIMASYSTEM | binary | Adresse des jeweiligen LIN-Slaves 0xFF = Nicht verbaut oder antwortet nicht Byte0=PTC Byte1=DEF Byte2=FL/UML/SD Byte3=Mischluft rechts Byte4=Fußraum Byte5=Belüftung Byte6=Mischluft links Byte7=Fond (nur E9X) Byte8=Schichtung (nur E9X) Byte9=Fehlerstatus Beschreibung Fehlerstatus: 0x00=kein Fehler 0x01=PTC-Fehler 0x02=falsch Codiert 0x03=falscher Klimakasten 0xFF=unbekannter Fehler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta-block"></a>
### STATUS_FASTA_BLOCK

Aktueller Wert des FASTA-Blocks (je 16 Bit) KWP2000: $23 recordCommonIdentifier (High-Byte) $xx recordCommonIdentifier (Low-Byte) (FASTA-Block) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FASTA_BLOCK_ARGUMENT | unsigned char | Nummer des FASTA-Blocks (0-FF) table FastaBlockTab Blocknumber,Blockname Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FASTA_BLOCK_NAME_WERT | string | Ausgabe des FASTA-Blocksnamens |
| STAT_FASTA_BLOCK_EINH | string | Einheit des FASTA-Blocks Stunden oder Zählerstand |
| STAT_FASTA_BLOCK_WERT | real | Wert des FASTA-Blocks |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ptc-ident"></a>
### STATUS_PTC_IDENT

Liefert die Identdaten des PTC (reportCurrentState) KWP2000: $30 InputOutputControlByLocalIdentifier $26 InputOutputLocalIdetifier PTC $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_REFERENCE | unsigned char | Aktuelle Referenznummer |
| STAT_SUPPLIER | unsigned char | Aktuelle Suppliernummer |
| STAT_ASIC_NR | unsigned char | Aktuelle ASIC-Nummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motoren-eichlauf"></a>
### STEUERN_MOTOREN_EICHLAUF

Löst Klappeneichlauf aus und kalibriert die Schrittzahlen neu KWP2000: $31 StartRoutineByLocalIdetifier $20 routineLocalIdentifier Klappenmotoreneichlauf Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-eichlauf"></a>
### STATUS_MOTOR_EICHLAUF

Lesen des aktuellen Status des Motoren-Eichlaufs KWP2000: $21 ReadDataByLocalIdentifier $10 Status Motor-Eichlauf (recordLocalIdentifier) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTOR_EICHLAUF_DATEN | binary | Byte0=Eichlaufstatus Byte1=Status DEF Byte2=Status FL/UML/SD Byte3=Status Mischluft rechts Byte4=Status Fußraum Byte5=Status Belüftung Byte6=Status Mischluft links Byte7=Status Fond (nur E9X) Byte8=Status Schichtung (nur E9X) |
| STAT_EICHLAUF_WERT | unsigned char | 0x?0 = in diesem Klemmenzyklus (auch Klemme 30 Reset) noch nicht gestartet 0x?1 = Eichlauf läuft gerade 0x?2 = Eichlauf abgeschlossen IO 0x?3 = Eichlauf abgeschlossen NIO 0x0? = keine gültigen Schrittweiten vorhanden 0x1? = gültige Schrittweiten vorhanden |
| STAT_EICHLAUF_TEXT | string | Repräsentation von STAT_EICHLAUF_WERT (aktuelle Eichlaufinformation) |
| STAT_EICHLAUF_HISTORY | string | Repräsentation von STAT_EICHLAUF_WERT (History) |
| STAT_KLAPPE_DEFROST_WERT | unsigned char | 0 = NIO 1 = IO 2 = Klappe nicht verbaut / nicht relevant (z.B. Klappe Fond bei IHKA E87) |
| STAT_KLAPPE_UMLUFT_WERT | unsigned char | 0 = NIO 1 = IO 2 = Klappe nicht verbaut / nicht relevant (z.B. Klappe Fond bei IHKA E87) |
| STAT_KLAPPE_MISCHLUFT_RE_WERT | unsigned char | 0 = NIO 1 = IO 2 = Klappe nicht verbaut / nicht relevant (z.B. Klappe Fond bei IHKA E87) |
| STAT_KLAPPE_FUSSRAUM_WERT | unsigned char | 0 = NIO 1 = IO 2 = Klappe nicht verbaut / nicht relevant (z.B. Klappe Fond bei IHKA E87) |
| STAT_KLAPPE_BELUEFTUNG_WERT | unsigned char | 0 = NIO 1 = IO 2 = Klappe nicht verbaut / nicht relevant (z.B. Klappe Fond bei IHKA E87) |
| STAT_KLAPPE_MISCHLUFT_LI_WERT | unsigned char | 0 = NIO 1 = IO 2 = Klappe nicht verbaut / nicht relevant (z.B. Klappe Fond bei IHKA E87) |
| STAT_KLAPPE_FOND_WERT | unsigned char | 0 = NIO 1 = IO 2 = Klappe nicht verbaut / nicht relevant (z.B. Klappe Fond bei IHKA E87) |
| STAT_KLAPPE_SCHICHTUNG_WERT | unsigned char | 0 = NIO 1 = IO 2 = Klappe nicht verbaut / nicht relevant (z.B. Klappe Fond bei IHKA E87) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fertigungsdaten-lesen"></a>
### FERTIGUNGSDATEN_LESEN

Lesen der zuliefererspezifischen Fertigungsdaten KWP2000: $21 ReadDataByLocalIdentifier $07-$14,$FA-$FB systemSupplierSpecific Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SSS_ARGUMENT | unsigned char | Adresse des Datenfeldes = systemSupplierSpecific local identifier (SSS) $07-$13,$FA-$FB Wenn keine Eingabe: default = 0xFA (erstes systemSupplierSpecific Datenfeld) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FERTIGUNGSDATEN | binary | Als Antwort wird ein Datenpuffer empfangen Der Datenpuffer hat folgenden Aufbau Byte 0              : Adresse des Datenfeldes = systemSupplierSpecific local identifier (SSS) $07-$11,$FA-$FB Byte 1...           : Zeigt die fertigungsspezifischen Datenfelder Der Inhalt und die jeweils maximale Anzahl der Daten sind der Fertigungsdokumentation zu entnehmen |
| STAT_FUNKTIONSBELEUCHTUNG_WERT | unsigned char | Kalibrierwert der Funktionsbeleuchtung [0-255] |
| STAT_RINGBELEUCHTUNG_WERT | unsigned char | Kalibrierwert der Ringbeleuchtung [0-255] |
| STAT_TASTENBELEUCHTUNG_WERT | unsigned char | Kalibrierwert der Tastenbeleuchtung [0-255] |
| STAT_DISPLAYBELEUCHTUNG_WERT | unsigned char | Kalibrierwert der Displaybeleuchtung [0-255] |
| STAT_ASIC_STROM_WERT | unsigned char | Kalibrierwert des ASIC-Stroms [0-255] |
| STAT_POTI_RECHTS_0_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 0 Grad Position [0-255] |
| STAT_POTI_RECHTS_25_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 25 Grad Position [0-255] |
| STAT_POTI_RECHTS_50_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 50 Grad Position [0-255] |
| STAT_POTI_RECHTS_75_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 75 Grad Position [0-255] |
| STAT_POTI_RECHTS_100_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 100 Grad Position [0-255] |
| STAT_POTI_RECHTS_125_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 125 Grad Position [0-255] |
| STAT_POTI_RECHTS_150_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 150 Grad Position [0-255] |
| STAT_POTI_RECHTS_175_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 175 Grad Position [0-255] |
| STAT_POTI_RECHTS_200_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 200 Grad Position [0-255] |
| STAT_POTI_RECHTS_225_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 225 Grad Position [0-255] |
| STAT_POTI_RECHTS_250_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 250 Grad Position [0-255] |
| STAT_POTI_RECHTS_275_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 275 Grad Position [0-255] |
| STAT_POTI_RECHTS_300_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 300 Grad Position [0-255] |
| STAT_POTI_RECHTS_325_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 325 Grad Position [0-255] |
| STAT_POTI_RECHTS_360_GRAD_WERT | unsigned char | Kalibrierwert des Poti rechts 360 Grad Position [0-255] |
| STAT_POTI_LINKS_0_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 0 Grad Position [0-255] |
| STAT_POTI_LINKS_25_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 25 Grad Position [0-255] |
| STAT_POTI_LINKS_50_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 50 Grad Position [0-255] |
| STAT_POTI_LINKS_75_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 75 Grad Position [0-255] |
| STAT_POTI_LINKS_100_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 100 Grad Position [0-255] |
| STAT_POTI_LINKS_125_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 125 Grad Position [0-255] |
| STAT_POTI_LINKS_150_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 150 Grad Position [0-255] |
| STAT_POTI_LINKS_175_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 175 Grad Position [0-255] |
| STAT_POTI_LINKS_200_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 200 Grad Position [0-255] |
| STAT_POTI_LINKS_225_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 225 Grad Position [0-255] |
| STAT_POTI_LINKS_250_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 250 Grad Position [0-255] |
| STAT_POTI_LINKS_275_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 275 Grad Position [0-255] |
| STAT_POTI_LINKS_300_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 300 Grad Position [0-255] |
| STAT_POTI_LINKS_325_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 325 Grad Position [0-255] |
| STAT_POTI_LINKS_360_GRAD_WERT | unsigned char | Kalibrierwert des Poti links 360 Grad Position [0-255] |
| STAT_DISPLAY_KONTRAST_OBEN_WERT | unsigned char | Displaykontrast Einbaulage oben [0-255] |
| STAT_DISPLAY_KONTRAST_UNTEN_WERT | unsigned char | Displaykontrast Einbaulage unten [0-255] |
| STAT_FAKTOR_EINBAULAGE_FUNKTIONSBELEUCHTUNG | unsigned char | Einbaulagenfaktor der Funktionsbeleuchtung E9X oder E8X [0-255] |
| STAT_DISPLAY_BELEUCHTUNGSFAKTOR_OBEN_WERT | unsigned char | Displaybeleuchtungsfaktor Einbaulage oben [0-255] |
| STAT_DISPLAY_BELEUCHTUNGSFAKTOR_UNTEN_WERT | unsigned char | Displaybeleuchtungsfaktor Einbaulage unten [0-255] |
| STAT_LEITERPLATTE_GENRAD_WERT | unsigned char | Genrad Byte in Hex [0-99] |
| STAT_PROZESS_NUMMER_PCB_WERT | unsigned int | Prozeßnummer in BCD [0-9999] |
| STAT_TYP_NUMMER_WERT | unsigned int | Typnummer in Hex [0-9999] |
| STAT_LAUFENDE_NUMMER_WERT | unsigned long | Laufende Nummer in BCD [0-99999999] |
| STAT_PRUEFDATUM_KW_WERT | unsigned char | Prüfdatum Kalenderwoche in BCD [0-52] |
| STAT_PRUEFDATUM_JAHR_WERT | unsigned char | Prüfdatum Jahr in BCD [0-99] |
| STAT_PRUEFINDEX_WERT | unsigned char | Prüfindex Jahr in BCD [0-99] |
| STAT_PRUEFZAEHLER_PCB_WERT | unsigned char | Prüfzähler in BCD [0-99] |
| STAT_TIMER_BESTROMUNG_WERT | unsigned char | Prüfindex Jahr in Hex [0-3C] |
| STAT_HW_PCB_WERT | unsigned int | Hardware PCB in ASCII [0-9,A-Z] |
| STAT_PRUEFSTATUS_WERT | unsigned char | Prüfstatus in BCD [0-99] |
| STAT_PROZESS_NUMMER_EOL_WERT | unsigned char | Prozeßnummer in BCD [0-99] |
| STAT_PRODIS_TYP_NUMMER_WERT | unsigned long | Prodis-Typnummer in BCD [0-99999999] |
| STAT_PRODIS_SERIEN_NUMMER_WERT | unsigned long | Prodis-Seriennummer in BCD [0-99999999] |
| STAT_PRUEFZAEHLER_EOL_WERT | unsigned char | Prüfzähler in BCD [0-99] |
| STAT_HPI_WERT | unsigned char | Hardwareprogramierindex in ASCII [0-9,A-Z] |
| STAT_VDO_INDEX_WERT | unsigned int | VDO-Index in BCD [0-9999] |
| STAT_BMW_AI_WERT | unsigned char | BMW-Änderungsindex in BCD [] |
| STAT_AD_WERTE_IN_RASTPUNKTEN | unsigned char | Ausgabe von AD-Werten die während der Drehmomentmessung in diversen Rastpunkten gemessen werden Der Inhalt und die jeweils Bedeutung der Daten sind der Fertigungsdokumentation zu entnehmen |
| STAT_AKTIVIERUNG_POTI_NACHKALIBRIERUNG | unsigned int | Ausgabe Aktivierung der Poti-Nachkalibrierung Highbyte Checksum [= Aktivstatus invertiert] Low-Byte Aktivstatus [1=aktiv, 0=inaktiv] |
| STAT_VARIANTE_IHKA_TEXT | string | Repräsentation von STAT_VARIANTE_IHKA |
| STAT_VARIANTE_IHKA | unsigned char | IHKA-Variante (Drehsteller) 0 = schwarz 1 = Perlglanz Chrom 2 = chrome pearlgray |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kompressor-einlaufschutz"></a>
### STEUERN_KOMPRESSOR_EINLAUFSCHUTZ

Setzen/Löschen des Kompressor Einlaufschutzes KWP2000: $3B WriteDataByLocalIdentifier $01 Kompressor Einlaufschutz (recordLocalIdentifier) $0x Ein/Aus (recordValue#1) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EIN_AUS | string | "ein" -&gt; Kompressoreinlaufschutz ein "aus" -&gt; Kompressoreinlaufschutz aus table DigitalArgument TEXT Wenn keine Eingabe: Default = "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fertigungsdaten-schreiben"></a>
### FERTIGUNGSDATEN_SCHREIBEN

Schreiben der zuliefererspezifischen Fertigungsdaten KWP2000: $3B WriteDataByLocalIdentifier $07-$14, $FA-$FB systemSupplierSpecific Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Adresse des Datenfeldes = systemSupplierSpecific local identifier (SSS) $07-$11, $FA-$FE Byte 1...           : Beschreibt direkt die fertigungsspezifischen Datenfelder im EEPROM Die Inhalt und die jeweils maximale Anzahl der Daten ist der Fertigungsdukumentation zu entnehmen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnosebit-setzen"></a>
### STEUERN_DIAGNOSEBIT_SETZEN

Setzen der I/O-Port-Diagnosebits (executeControlOption) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) $06 executeControlOption Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_ARGUMENT | unsigned char | Nummer des anzusteuernden Ports table IOPortTab Portnumber,Portname Wenn keine Eingabe: default = 0x01 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnosebit-loeschen"></a>
### STEUERN_DIAGNOSEBIT_LOESCHEN

Rücksetzen der I/O-Port-Diagnosebits (returnControlToECU) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) $00 returnControlToECU Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_ARGUMENT | unsigned char | Nummer des I/O-Ports table IOPortTab Portnumber,Portname Wenn keine Eingabe: default = 0x01 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sollwerte-ihka"></a>
### STEUERN_SOLLWERTE_IHKA

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $40 InputOutputLocalIdetifier (Sollwerte) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_SOLLWERT_FA | unsigned char | Sollwert Fahrer 16°C-28°C in 0,5° Schritten Wenn keine Eingabe: default = 22°C |
| SET_SOLLWERT_BF | unsigned char | Sollwert Beifahrer 16°C-28°C in 0,5° Schritten Wenn keine Eingabe: default = 22°C |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tasten"></a>
### STEUERN_TASTEN

Setzen von der ECU-Tasten (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $01 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT)Tastatur $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_TASTEN_BITMUSTER | unsigned int | Bitmuster der anzusteuernden Tasten 1 = Taste wird über Diagnose gesteuert 0 = Kontrolle zurück an ECU BIT 0: REST BIT 1: GBL PLUS BIT 2: DEF BIT 3: AUTO BIT 4: AC BIT 5: LVT MITTE BIT 6: frei BIT 7: frei BIT 8: GBL_MINUS BIT 9: HHS BIT 10: AC MAX BIT 11: AUC BIT 12: LVT UNTEN BIT 13: LVT OBEN BIT 14: frei BIT 15: frei Wenn keine Eingabe: default = 0x0000 |
| SET_TASTEN_BITMUSTER | unsigned int | Bitmuster der ein/auszuschaltenden Tasten 1 = Taste gedrückt 0 = Taste nicht gedrückt BIT 0: REST BIT 1: GBL PLUS BIT 2: DEF BIT 3: AUTO BIT 4: AC BIT 5: LVT MITTE BIT 6: frei BIT 7: frei BIT 8: GBL_MINUS BIT 9: HHS BIT 10: AC MAX BIT 11: AUC BIT 12: LVT UNTEN BIT 13: LVT OBEN BIT 14: frei BIT 15: frei Wenn keine Eingabe: default = 0x0000 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-szm-tasten"></a>
### STEUERN_SZM_TASTEN

Setzen der SZM-Tasten (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $04 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) Tastatur-SZM $06 executeControlOption Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_SZM_TASTEN_BITMUSTER | unsigned char | Bitmuster der anzusteuernden Tasten des 1. Tastenports 1 = Taste wird über Diagnose gesteuert 0 = Kontrolle zurück an ECU BIT 0: Hill decent control BIT 1: Sitzheizung links BIT 2: frei BIT 3: Park distance control BIT 4: Sitzheizung rechts BIT 5: frei BIT 6: Sonnenrollo BIT 7: frei Wenn keine Eingabe: default = 0x00 |
| SET_SZM_TASTEN_BITMUSTER | unsigned char | Bitmuster der ein/auszuschaltenden Tasten des 1. Tastenports 1 = Taste gedrückt 0 = Taste nicht gedrückt BIT 0: Hill decent control BIT 1: Sitzheizung links BIT 2: frei BIT 3: Park distance control BIT 4: Sitzheizung rechts BIT 5: frei BIT 6: Sonnenrollo BIT 7: frei Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-outputport"></a>
### STEUERN_OUTPUTPORT

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $xx InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_ARGUMENT | unsigned char | Nummer des I/O-Ports table IOPortTab Portnumber,Portname Wenn keine Eingabe: default = 0x20 |
| SET_PORT_VALUE | unsigned char | Ausgangswert des anzusteuernden Ports Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-12v-ausgang"></a>
### STEUERN_12V_AUSGANG

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $07 InputOutputLocalIdetifier (12V-Ausgang) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PORT_STATUS | string | "ein"   -&gt; 12V-Ausgang einschalten "aus"   -&gt; 12V-Ausgang ausschalten table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-5v-ausgang"></a>
### STEUERN_5V_AUSGANG

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $08 InputOutputLocalIdetifier (5V-Ausgang) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PORT_STATUS | string | "ein"   -&gt; 5V-Ausgang einschalten "aus"   -&gt; 5V-Ausgang ausschalten table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-innenfuehlergeblaese"></a>
### STEUERN_INNENFUEHLERGEBLAESE

Setzen des Innenfühlergebläseausgangs (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $17 InputOutputLocalIdetifier (Innenfühlergebläse) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PORT_STATUS | string | "ein"   -&gt; Innenfühlergebläse einschalten "aus"   -&gt; Innenfühlergebläse ausschalten table DigitalArgument TEXT Default:  Innenfühlergebläse ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-szm-ausgaenge"></a>
### STEUERN_SZM_AUSGAENGE

Setzen der PWM der Funktionsbeleuchtung des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $09 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) SZM-Ausgänge $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Rohwerte der drei SZM-Ausgänge (1=Port gesetzt) Bit0 =   Data Bit1 =   Clock Bit2 =   Strobe Bit3-7 = frei Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-display"></a>
### STEUERN_DISPLAY

Setzen von Bitmustern des LCDs (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $0A InputOutputLocalIdentifier (I_O_PORT_ARGUMENT) LCD $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer beschreibt direkt das Datenfeld zum Displaycontroller Byte 0...19 : Displaymuster gemäß Displayspzifikation Bsp. Muster1: $3C3C33C3C34BC3443CBCCCBCB43C3C33C3C343CB Bsp. Muster2: $C3C3CC3C3CB43433C34333434BC3C3CC3C3C3C34 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-funktionsbeleuchtung"></a>
### STEUERN_FUNKTIONSBELEUCHTUNG

Setzen der Funktions-LEDs (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $02 InputOutputLocalIdentifier (I_O_PORT_ARGUMENT) LED-Port $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_LED_BITMUSTER | unsigned int | Bitmuster der LEDs, die über Diagnose angesteuert werden sollen 1 = LED wird über Diagnose gesteuert 0 = Kontrolle zurück an ECU BIT 15: frei  (MSB) BIT 14: frei BIT 13: frei BIT 12: frei BIT 11: LV oben BIT 10: LV mitte BIT 9:  LV unten BIT 8:  UML BIT 7:  AUC BIT 6:  AUTO BIT 5:  AC BIT 4:  AC-MAX BIT 3:  REST BIT 2:  HHS BIT 1:  DEF BIT 0:  frei  (LSB) Wenn keine Eingabe: default = 0x0000 |
| SET_LED_BITMUSTER | unsigned int | Bitmuster der LEDs, die gesetzt oder gelöscht werden sollen 1 = LED an 0 = LED aus BIT 15: frei  (MSB) BIT 14: frei BIT 13: frei BIT 12: frei BIT 11: LV oben BIT 10: LV mitte BIT 9:  LV unten BIT 8:  UML BIT 7:  AUC BIT 6:  AUTO BIT 5:  AC BIT 4:  AC-MAX BIT 3:  REST BIT 2:  HHS BIT 1:  DEF BIT 0:  frei  (LSB) Wenn keine Eingabe: default = 0x0000 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-szm-funktionsbeleuchtung"></a>
### STEUERN_SZM_FUNKTIONSBELEUCHTUNG

Setzen der Funktions-SZM-LEDs (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $03 InputOutputLocalIdentifier (I_O_PORT_ARGUMENT) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_LED_BITMUSTER | unsigned int | Bitmuster der LEDs, die über Diagnose angesteuert werden sollen 1 = LED wird über Diagnose gesteuert 0 = Kontrolle zurück an ECU BIT 15: Sitzheizung links LED außen  (MSB) BIT 14: Sitzheizung links LED außen & mitte BIT 13: Sitzheizung links LED außen & mitte & innen BIT 12: Park Distance Control (PDC) BIT 11: Hill decent Control (HDC) BIT 10: Sitzheizung rechts LED außen BIT 9:  Sitzheizung rechts LED außen & mitte BIT 8:  Sitzheizung rechts LED außen & mitte & innen BIT 7:  frei BIT 6:  frei BIT 5:  frei BIT 4:  frei BIT 3:  frei BIT 2:  frei BIT 1:  frei BIT 0:  frei   (LSB) Wenn keine Eingabe: default = 0x0000 |
| SET_LED_BITMUSTER | unsigned int | Bitmuster der LEDs, die gesetzt oder gelöscht werden sollen 1 = LED an 0 = LED aus BIT 15: Sitzheizung links LED außen  (MSB) BIT 14: Sitzheizung links LED außen & mitte BIT 13: Sitzheizung links LED außen & mitte & innen BIT 12: Park Distance Control (PDC) BIT 11: Hill decent Control (HDC) BIT 10: Sitzheizung rechts LED außen BIT 9:  Sitzheizung rechts LED außen & mitte BIT 8:  Sitzheizung rechts LED außen & mitte & innen BIT 7:  frei BIT 6:  frei BIT 5:  frei BIT 4:  frei BIT 3:  frei BIT 2:  frei BIT 1:  frei BIT 0:  frei   (LSB) Wenn keine Eingabe: default = 0x0000 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm-funktionsbeleuchtung"></a>
### STEUERN_PWM_FUNKTIONSBELEUCHTUNG

Setzen der PWM der Funktionsbeleuchtung des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $30 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM Funktionsbeleuchtung ECU $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Rohwerte der PWM 0-255 (= 0-100%) Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm-ringbeleuchtung"></a>
### STEUERN_PWM_RINGBELEUCHTUNG

Setzen der PWM der Ringsuchbeleuchtung des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $31 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM Ringsuchbeleuchtung ECU $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Rohwerte der PWM 0-255 (= 0-100%) Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm-tastenbeleuchtung"></a>
### STEUERN_PWM_TASTENBELEUCHTUNG

Setzen der PWM der Tastensuchbeleuchtung des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $32 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM Tastensuchbeleuchtung ECU $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Rohwerte der PWM 0-255 (= 0-100%) Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm-displaybeleuchtung"></a>
### STEUERN_PWM_DISPLAYBELEUCHTUNG

Setzen der PWM der Dispalybeleuchtung des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $33 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM Dispalybeleuchtung ECU $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Rohwerte der PWM 0-255 (= 0-100%) Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm-displaykontrast"></a>
### STEUERN_PWM_DISPLAYKONTRAST

Setzen der PWM des Dispalykontrasts des ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $34 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM Displaykontrast ECU $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Rohwerte der PWM 0-255 (= 0-100%) Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm-szm-funktionsbeleuchtung"></a>
### STEUERN_PWM_SZM_FUNKTIONSBELEUCHTUNG

Setzen der PWM der ECU-Suchbeleuchtung (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $35 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM ECU-Suchbeleuchtung $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Rohwerte der PWM 0-255 (= 0-100%) Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm-szm-suchbeleuchtung"></a>
### STEUERN_PWM_SZM_SUCHBELEUCHTUNG

Setzen der PWM der SZM-Suchbeleuchtung (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $36 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) PWM SZM-Suchbeleuchtung $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Rohwerte der PWM 0-255 (= 0-100%) Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-geblaese"></a>
### STEUERN_GEBLAESE

Setzen der Gebläseleistung (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $15 InputOutputLocalIdetifier (Gebläse) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PWM_VALUE | unsigned char | Gebläseleistung 0%-100% in 1% Schritten Wenn keine Eingabe: default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-beleuchtung"></a>
### STEUERN_BELEUCHTUNG

Setzen aller Beleuchtungen der ECU (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $37 InputOutputLocalIdetifier (I_O_PORT_ARGUMENT) Beleuchtung ECU $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PWM_VALUE | unsigned char | Wert der PWM 0-100% Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-umluft"></a>
### STEUERN_KLAPPE_UMLUFT

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $20 InputOutputLocalIdetifier (Frischluft/Umluft/Staudruckklappe) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Klappenstellung 0%-100% in 1% Schritten Wenn keine Eingabe: default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-mischluft-links"></a>
### STEUERN_KLAPPE_MISCHLUFT_LINKS

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $21 InputOutputLocalIdetifier (Mischluftklappe links) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Klappenstellung 0%-100% in 1% Schritten Wenn keine Eingabe: default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-mischluft-rechts"></a>
### STEUERN_KLAPPE_MISCHLUFT_RECHTS

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $22 InputOutputLocalIdetifier (Mischluftklappe rechts) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Klappenstellung 0%-100% in 1% Schritten Wenn keine Eingabe: default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-belueftung"></a>
### STEUERN_KLAPPE_BELUEFTUNG

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $23 InputOutputLocalIdetifier (Belüftung) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Klappenstellung 0%-100% in 1% Schritten Wenn keine Eingabe: default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fussraum"></a>
### STEUERN_KLAPPE_FUSSRAUM

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $24 InputOutputLocalIdetifier (Fußraum) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Klappenstellung 0%-100% in 1% Schritten Wenn keine Eingabe: default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-defrost"></a>
### STEUERN_KLAPPE_DEFROST

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $25 InputOutputLocalIdetifier (Defrost) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Klappenstellung 0%-100% in 1% Schritten Wenn keine Eingabe: default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fond"></a>
### STEUERN_KLAPPE_FOND

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $27 InputOutputLocalIdetifier (Fondbelüftung nur E9X) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Klappenstellung 0%-100% in 1% Schritten Wenn keine Eingabe: default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-schichtung"></a>
### STEUERN_KLAPPE_SCHICHTUNG

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $28 InputOutputLocalIdetifier (Schichtung nur E9X) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Klappenstellung 0%-100% in 1% Schritten Wenn keine Eingabe: default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ptc"></a>
### STEUERN_PTC

Setzen von Ausgangsports (shortTermAdjustment) KWP2000: $30 InputOutputControlByLocalIdentifier $26 InputOutputLocalIdetifier (Zuheizer) $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_PORT_VALUE | unsigned char | Zuheizer-Ansteuerung 0%-100% in 1% Schritten Wenn keine Eingabe: default = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_O_PORT_NAME_WERT | string | Ausgabe des I/O_Portnamens |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-autoadressierung"></a>
### STEUERN_AUTOADRESSIERUNG

Startet die LIN-Bus Autoadressierung KWP2000: $31 StartRoutineByLocalIdetifier $22 routineLocalIdentifier LIN-Bus Autoadressierung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motor-fehler-loeschen"></a>
### STEUERN_MOTOR_FEHLER_LOESCHEN

Löscht Zähler für Motorfehler KWP2000: $31 StartRoutineByLocalIdetifier $24 routineLocalIdentifier LIN-Bus Motorfehler löschen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-einzeladressierung"></a>
### STEUERN_EINZELADRESSIERUNG

Startet die LIN-Bus Einzeladressierung KWP2000: $31 StartRoutineByLocalIdetifier $23 routineLocalIdentifier LIN-Bus Einzeladressierung Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CURRENT_STEPPER_ADDESS | unsigned char | Aktuelle Adresse des zu programmierenden Motors Wenn keine Eingabe: default = 0x3F |
| NEW_STEPPER_ADDRESS | unsigned char | Neue Adresse des zu programmierenden Motors Wenn keine Eingabe: default = 0x3F |
| DIRECTION | unsigned char | Laufrichtung des zu programmierenden Motors 0x00=Laufrichtung im Uhrzeigersinn für steigende Schrittzahlen 0x01=Laufrichtung gegen den Uhrzeigersinn für steigende Schrittzahlen 0xFF=Laufrichtung wie aktuelle Motorprogrammierung Wenn keine Eingabe: default = 0xFF |
| SAFETY_ENABLE | unsigned char | Notlaufaktivierung des zu programmierenden Motors 0x00=Notauf aktiviert 0x01=Notauf deaktiviert 0xFF=Notauf wie aktuelle Motorprogrammierung Wenn keine Eingabe: default = 0xFF |
| SAFETY_DIRECTION | unsigned char | Notlaufendposition des zu programmierenden Motors 0x00=Zu niedrigen Schrittzahlen 0x01=Zu hohen Schrittzahlen 0xFF=Notlaufendposition wie aktuelle Motorprogrammierung Wenn keine Eingabe: default = 0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnosetestbetrieb-permanent"></a>
### STEUERN_DIAGNOSETESTBETRIEB_PERMANENT

Dauerhaftes Setzen oder Löschen des Diagosetestbetriebs KWP2000: $3B WriteDataByLocalIdentifier $03 Diagnosetestbetrieb permanent(recordLocalIdentifier) $0x Ein/Aus (recordValue#1) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EIN_AUS | string | "ein" -&gt; Diagnosetestbetrieb permanent ein "aus" -&gt; Diagnosetestbetrieb aus table DigitalArgument TEXT Wenn keine Eingabe: Default = "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-reset-lin"></a>
### STEUERN_RESET_LIN

Löst Rücksetzen des LIN-Bus aus KWP2000: $31 StartRoutineByLocalIdetifier $25 routineLocalIdentifier Reset LIN-Bus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-drehmoment-messung"></a>
### STEUERN_DREHMOMENT_MESSUNG

Start der AD-Wert-Aufnahme während der Drehmomentmessung in diversen Rastpunkten KWP2000: $31 StartRoutineByLocalIdetifier $26 routineLocalIdentifier Drehmomentmessung Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_AUSWAHL_LINKS_RECHTS | unsigned char | Auswahl der Seite (links=2, rechts=1, aus=0) Wenn keine Eingabe: default = 0 (aus) |
| SET_ABLAUFSTEUERUNG | unsigned char | Ablaufsteuerung (Werte 0-255) Wenn keine Eingabe: default = 0 Die Beschreibung des Inhalts ist der Fertigungsdokumentation zu entnehmen |
| SET_DREHGESCHWINDIGKEIT | unsigned char | Drehgeschwindigkeit (0-255) Wenn keine Eingabe: default = 120 Die Beschreibung des Inhalts ist der Fertigungsdokumentation zu entnehmen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOLLWERT_RECHTS_IN_TOT_WERT | unsigned char | Poti Temperatursollwert rechts im Totbereich Bereich: 0x00 bis 0xFF |
| STAT_SOLLWERT_LINKS_IN_TOT_WERT | unsigned char | Poti Temperatursollwert links im Totbereich Bereich: 0x00 bis 0xFF |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-loeschen"></a>
### C_C_LOESCHEN

KWP2000: $31 StartRoutineByLocalIdetifier $21 routineLocalIdentifier Löschen Codierdatensatz Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-shzh-ident"></a>
### STATUS_SHZH_IDENT

BMW Zusammenbaunummer auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BMW_ZUSAMMENBAUNUMMER | string | BMW Zusammenbaunummer |
| STAT_BMW_HARDWARENUMMER | string | BMW Hardwarenummer |
| STAT_HARDWARE_VERSION | string | Hardware Version |
| STAT_SOFTWARE_VERSION | string | Software Version |
| STAT_SH_VARIANTE_WERT | int | SH Variante 1-&gt;Benzin 2-&gt;Diesel 4-&gt;RME 255-&gt;ungueltig |
| STAT_SH_VARIANTE | string | SH Variante |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG_SATZ1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ3 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ4 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ4 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-shzh-bmw-zusammenbaunummer"></a>
### STATUS_SHZH_BMW_ZUSAMMENBAUNUMMER

BMW Zusammenbaunummer auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BMW_ZUSAMMENBAUNUMMER | string | BMW Zusammenbaunummer |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG_SATZ1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ2 | binary | Hex-Antwort von SG |

<a id="job-status-shzh-bmw-hardwarenummer"></a>
### STATUS_SHZH_BMW_HARDWARENUMMER

BMW Hardwarenummer auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BMW_HARDWARENUMMER | string | BMW Hardwarenummer |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG_SATZ1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ2 | binary | Hex-Antwort von SG |

<a id="job-status-shzh-bmw-hardwaresternnummer"></a>
### STATUS_SHZH_BMW_HARDWARESTERNNUMMER

BMW Hardwaresternnummer auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BMW_HARDWARESTERNNUMMER | string | BMW Hardwaresternnummer |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG_SATZ1 | binary | Hex-Auaftrag an SG |
| _TEL_ANTWORT_SATZ1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ2 | binary | Hex-Antwort von SG |

<a id="job-status-shzh-versionierung"></a>
### STATUS_SHZH_VERSIONIERUNG

Versionsdaten auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HARDWARE_VERSION | string | Hardware Version |
| STAT_SOFTWARE_VERSION | string | Software Version |
| STAT_SH_VARIANTE_WERT | int | SH Variante 1-&gt;Benzin 2-&gt;Diesel 4-&gt;RME 255-&gt;ungueltig |
| STAT_SH_VARIANTE | string | SH Variante |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shzh-kaltbefeuerung"></a>
### STEUERN_SHZH_KALTBEFEUERUNG

Kaltbefeuerung aktivieren/deaktivieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PASSWORT | int | Dieser Job ist mit Passwort geschützt |
| KALTBEFEUERUNG_MODUS | int | Kaltbefeuerungmodus 0x00 -&gt; deaktiviert 0x01 -&gt; aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-shzh-testlauf"></a>
### STATUS_SHZH_TESTLAUF

Testlauf (vom Prüfbetrieb) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TESTLAUF_WERT | int | Testlauf 0-&gt;Testlauf niO 1-&gt;Testlauf iO 255-&gt;ungueltig |
| STAT_TESTLAUF | string | Testlauf |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-shzh-betriebsdaten"></a>
### STATUS_SHZH_BETRIEBSDATEN

Betriebsdaten (Betriebsdauer, Brenndauer und Einschaltzähler) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BETRIEBSDAUER_MINUTEN | int | Betriebsdauer Minuten |
| STAT_BETRIEBSDAUER_STUNDEN | int | Betriebsdauer Stunden |
| STAT_BRENNDAUER_MINUTEN | int | Brenndauer Minuten |
| STAT_BRENNDAUER_STUNDEN | int | Brenndauer Stunden |
| STAT_EINSCHALTZAEHLER | int | Einschaltzaehler |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG_BETRIEBSDAUER | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_BETRIEBSDAUER | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_BRENNDAUER | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_BRENNDAUER | binary | Hex-Antwort von SG |

<a id="job-status-shzh-io"></a>
### STATUS_SHZH_IO

I/O Messwerte (Betriebsspannung, Funktionszustand, I/O Status, Glüelementwiederstand) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BETRIEBSSPANNUNG_WERT | int | Betriebsspannung |
| STAT_BETRIEBSSPANNUNG_EINHEIT | string | Betriebsspannungseinheit [mV] |
| STAT_FUNKTIONSZUSTAND_WERT | int | Funktionszustand |
| STAT_FUNKTIONSZUSTAND_TEXT | string | Funktionszustand |
| STAT_FLAMME_WERT | int | IO Status |
| STAT_FLAMME_ERKANNT | string | IO Status |
| STAT_GLUEHELEMENTWIDERSTAND_WERT | int | Gluehelementwiderstand |
| STAT_GLUEHELEMENTWIDERSTAND_EINHEIT | string | Gluehelementwiderstandseinheit [mOhm] |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG_SATZ1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ2 | binary | Hex-Antwort von SG |

<a id="job-status-shzh"></a>
### STATUS_SHZH

Der Job fasst den Job I/O Messwerte  (Betriebsspannung, Funktionszustand, I/O Status, Glüelementwiederstand) auslesen und den Job Status Applaktionsnachricht

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BETRIEBSSPANNUNG_WERT | int | Betriebsspannung |
| STAT_BETRIEBSSPANNUNG_EINHEIT | string | Betriebsspannungseinheit [mV] |
| STAT_FUNKTIONSZUSTAND_WERT | int | Funktionszustand |
| STAT_FUNKTIONSZUSTAND_TEXT | string | Funktionszustand |
| STAT_FLAMME_WERT | int | IO Status |
| STAT_FLAMME_ERKANNT | string | IO Status |
| STAT_GLUEHELEMENTWIDERSTAND_WERT | int | Gluehelementwiderstand |
| STAT_GLUEHELEMENTWIDERSTAND_EINHEIT | string | Gluehelementwiderstandseinheit [mOhm] |
| _TEL_AUFTRAG_SATZ1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ2 | binary | Hex-Antwort von SG |
| STAT_SHZH_WERT | int | Wert des Status der Standheizung / Zuheizung |
| STAT_SHZH_NAME | string | Name des Status der Standheizung / Zuheizung |
| STAT_SHZH_BESCHREIBUNG | string | Beschreibung des Status der Standheizung / Zuheizung |
| STAT_BETRIEBSMODUS_WERT | int | Status Betriebsmodus Wert |
| STAT_BETRIEBSMODUS_NAME | string | Status Betriebsmodus Name |
| STAT_BETRIEBSMODUS_BESCHREIBUNG | string | Status Betriebsmodus Beschreibung |
| STAT_WASSERPUMPE_WERT | int | Status Wasserpumpe Wert |
| STAT_WASSERPUMPE | string | Status Wasserpumpe |
| STAT_KRAFTSTOFFVORWAERMUNG_WERT | int | Status Kraftstoffvorwärmung Wert |
| STAT_KRAFTSTOFFVORWAERMUNG | string | Status Kraftstoffvorwärmung |
| STAT_DOSIERPUMPE_WERT | int | Status Dosierpumpe Wert |
| STAT_DOSIERPUMPE | string | Status Dosierpumpe |
| STAT_BRENNLUFTGEBLAESE_WERT | int | Status Brennluftgebläse Wert |
| STAT_BRENNLUFTGEBLAESE | string | Status Brennluftgebläse |
| STAT_GLUESTIFT_WERT | int | Status Glühstift Wert |
| STAT_GLUESTIFT | string | Status Glühstift |
| STAT_UMSCHALTVENTIL_WERT | int | Status Umschlatventil Wert |
| STAT_UMSCHALTVENTIL | string | Status Umschlatventil |
| STAT_TESTBETRIEB_WERT | int | Status Testbetrieb Wert |
| STAT_TESTBETRIEB | string | Status Testbetrieb |
| STAT_FEHLER_WERT | int | Status Fehler Wert |
| STAT_FEHLER | string | Status Fehler |
| STAT_COM_ERROR_WERT | int | Status Kommunikationsfehler Wert |
| STAT_COM_ERROR | string | Status Kommunikationsfehler |
| STAT_PWM_BRENNLUFTGEBLAESE_PROZENT | int | Status PWM Brennluftgebläse in Prozent |
| STAT_PWM_GLUEHSTIFT_PROZENT | int | Status PWM Glühstift in Prozent |
| STAT_PWM_KRAFTSTOFFVORWAERMUNG_PROZENT | int | Status PWM Kraftstoffvorwärmung in Prozent |
| STAT_WASSERTEMPERATUR_CELSIUS | int | Status Wassertemperatur in Grad Celsius |
| STAT_DOSIERPUMPENFREQUENZ_PERIODENDAUER_HERZ | int | Status Dosierpumpenfrequenz / Periodendauer in Herz |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-shzh-fehlerspeicher-loeschen"></a>
### SHZH_FEHLERSPEICHER_LOESCHEN

Lieferantenfehlerspeicher loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PASSWORT | int | Dieser Job ist mit Passwort geschützt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-shzh-fehlerspeicher-lesen"></a>
### SHZH_FEHLERSPEICHER_LESEN

Lieferantenfehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SHZH_FEHLERCODE1 | int | Fehlercode1 |
| STAT_SHZH_FEHLERART1 | string | Fehlerart1 |
| STAT_FUNKTIONSZUSTANDSTEXT_FEHLER1 | string | Funktionszustand |
| STAT_WASSERTEMPERATUR_FEHLER1_CELSIUS | int | Wassertemperatur |
| STAT_BETRIEBSSPANNUNG_FEHLER1_MILLIVOLT | int | Betriebsspannung |
| STAT_BETRIEBSDAUER_FEHLER1_MINUTEN | int | Betriebsdauer |
| STAT_BETRIEBSDAUER_FEHLER1_STUNDEN | int | Betriebsdauer |
| STAT_FEHLERSTATUS_FEHLER1_GESPEICHERT | string | Fehlerstatus |
| STAT_FEHLERSTATUS_FEHLER1_AKTUELL | string | Fehlerstatus |
| STAT_SHZH_FEHLERCODE2 | int | Fehlercode2 |
| STAT_SHZH_FEHLERART2 | string | Fehlerart2 |
| STAT_FUNKTIONSZUSTANDSTEXT_FEHLER2 | string | Funktionszustand |
| STAT_WASSERTEMPERATUR_FEHLER2_CELSIUS | int | Wassertemperatur |
| STAT_BETRIEBSSPANNUNG_FEHLER2_MILLIVOLT | int | Betriebsspannung |
| STAT_BETRIEBSDAUER_FEHLER2_MINUTEN | int | Betriebsdauer |
| STAT_BETRIEBSDAUER_FEHLER2_STUNDEN | int | Betriebsdauer |
| STAT_FEHLERSTATUS_FEHLER2_GESPEICHERT | string | Fehlerstatus |
| STAT_FEHLERSTATUS_FEHLER2_AKTUELL | string | Fehlerstatus |
| STAT_SHZH_FEHLERCODE3 | int | Fehlercode3 |
| STAT_SHZH_FEHLERART3 | string | Fehlerart3 |
| STAT_FUNKTIONSZUSTANDSTEXT_FEHLER3 | string | Funktionszustand |
| STAT_WASSERTEMPERATUR_FEHLER3_CELSIUS | int | Wassertemperatur |
| STAT_BETRIEBSSPANNUNG_FEHLER3_MILLIVOLT | int | Betriebsspannung |
| STAT_BETRIEBSDAUER_FEHLER3_MINUTEN | int | Betriebsdauer |
| STAT_BETRIEBSDAUER_FEHLER3_STUNDEN | int | Betriebsdauer |
| STAT_FEHLERSTATUS_FEHLER3_GESPEICHERT | string | Fehlerstatus |
| STAT_FEHLERSTATUS_FEHLER3_AKTUELL | string | Fehlerstatus |
| STAT_SHZH_FEHLERCODE4 | int | Fehlercode4 |
| STAT_SHZH_FEHLERART4 | string | Fehlerart4 |
| STAT_FUNKTIONSZUSTANDSTEXT_FEHLER4 | string | Funktionszustand |
| STAT_WASSERTEMPERATUR_FEHLER4_CELSIUS | int | Wassertemperatur |
| STAT_BETRIEBSSPANNUNG_FEHLER4_MILLIVOLT | int | Betriebsspannung |
| STAT_BETRIEBSDAUER_FEHLER4_MINUTEN | int | Betriebsdauer |
| STAT_BETRIEBSDAUER_FEHLER4_STUNDEN | int | Betriebsdauer |
| STAT_FEHLERSTATUS_FEHLER4_GESPEICHERT | string | Fehlerstatus |
| STAT_FEHLERSTATUS_FEHLER4_AKTUELL | string | Fehlerstatus |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG_SATZ1_TEL1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ1_TEL1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ1_TEL2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ1_TEL2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ2_TEL1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ2_TEL1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ2_TEL2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ2_TEL2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ3_TEL1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ3_TEL1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ3_TEL2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ3_TEL2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ4_TEL1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ4_TEL1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ4_TEL2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ4_TEL2 | binary | Hex-Antwort von SG |

<a id="job-status-shzh-konfiguration-lesen"></a>
### STATUS_SHZH_KONFIGURATION_LESEN

Konfiguration lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SH_KOMMUNIKATIONSUEBERWACHUNG_WERT | int | SH Kommunikationsüberwachung 0x00-&gt;Nicht aktiv 0x01-&gt;Aktiv |
| STAT_SH_KOMMUNIKATIONSUEBERWACHUNG | string | SH Kommunikationsüberwachung |
| STAT_WASSERPUMPE_ANSTEUERUNG_WERT | int | Status SH Wasserpumpeansteuerung 0x00-&gt;WP-Ansteuerung überexterne Komponenten 0x01-&gt;WP-Ansteuerung direkt über Stand-/Zuheizer |
| STAT_WASSERPUMPE_ANSTEUERUNG | string | Status SH Wasserpumpeansteuerung |
| STAT_UMSCHALTVENTIL_ANSTEUERUNG_WERT | int | Status SH Umschaltventilansteuerung 0x00-&gt;USV-Ansteuerung über externe Komponenten 0x01-&gt;USV-Ansteuerung direkt über Stand-/Zuheizer |
| STAT_UMSCHALTVENTIL_ANSTEUERUNG | string | Status SH Umschaltventilansteuerung |
| STAT_SHZH_HEIZZEIT_MINUTEN | int | Status Heizzeit (Sicherheitsfunktion) |
| STAT_UEBERWACHUNG_UNGUELTIGKEITSSIGNATUR_SEKUNDEN | int | Status Überwachung Ungültigkeitssignatur |
| STAT_UNTERSPANNUNGSABSCHALTSCHWELLE_MILLIVOLT | int | Status Unterspannungsabschaltschwelle |
| STAT_ZEITKRITERIUM_UNTERSPANNUNG_SEKUNDEN | int | Status Zeitkriterium für Unterspannung |
| STAT_CO2_WARMEINSTELLUNG | int | Status CO2 Warmeinstellung |
| STAT_UEBERSPANNUNGSABSCHALTSCHWELLE_MILLIVOLT | int | Status Überspannungsabschaltschwelle |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG_SATZ1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ2 | binary | Hex-Antwort von SG |

<a id="job-shzh-konfiguration-schreiben"></a>
### SHZH_KONFIGURATION_SCHREIBEN

Konfiguration lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PASSWORT | int | Dieser Job ist mit Passwort geschützt |
| STAT_SH_KOMMUNIKATIONSUEBERWACHUNG | int | SH Kommunikationsüberwachung 0x00-&gt;Nicht aktiv 0x01-&gt;Aktiv |
| STAT_WASSERPUMPE_ANSTEUERUNG | int | Status SH Wasserpumpeansteuerung 0x00-&gt;WP-Ansteuerung überexterne Komponenten 0x01-&gt;WP-Ansteuerung direkt über Stand-/Zuheizer |
| STAT_UMSCHALTVENTIL_ANSTEUERUNG | int | Status SH Umschaltventilansteuerung 0x00-&gt;USV-Ansteuerung über externe Komponenten 0x01-&gt;USV-Ansteuerung direkt über Stand-/Zuheizer |
| STAT_SHZH_HEIZZEIT | int | Status Heizzeit (Sicherheitsfunktion) Heizzeit [nx10min] eingeben MIN: 10min MAX: 60min |
| STAT_UEBERWACHUNG_UNGUELTIGKEITSSIGNATUR_SEKUNDEN | int | Status Überwachung Ungültigkeitssignatur Nutzbereich: 0...14sec 15-&gt;Deaktivierung |
| STAT_UNTERSPANNUNGSABSCHALTSCHWELLE_MILLIVOLT | int | Status Unterspannungsabschaltschwelle in [mV] |
| STAT_ZEITKRITERIUM_UNTERSPANNUNG_SEKUNDEN | int | Status Zeitkriterium in [s] für Unterspannung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG_SATZ1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ2 | binary | Hex-Antwort von SG |

<a id="job-shzh-steuergeraet-reset"></a>
### SHZH_STEUERGERAET_RESET

Reset des Steuergerätes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-shzh-baudrate-konfigurieren"></a>
### SHZH_BAUDRATE_KONFIGURIEREN

Baudrate konfigurieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PASSWORT | int | Dieser Job ist mit Passwort geschützt |
| BAUDRATEN_KENNUNG | int | BAUDRATEN 0x01 -&gt; reserviert 0x02 -&gt; reserviert 0x04 -&gt; 9600 Baud 0x08 -&gt; reserviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shzh-komponenten"></a>
### STEUERN_SHZH_KOMPONENTEN

Komponententest

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SHZH_KOMPONENTENTEST_UP | int | Status Umwälzpumpe 0 -&gt; Nicht aktiv 1 -&gt; Aktiv max. Zeitangabe: 254s |
| SHZH_KOMPONENTENTEST_KV | int | Status Kraftstoffvorwärmung 0-&gt;KV nicht aktiv 1-&gt;KV aktiv max. Zeitangabe: 10s |
| SHZH_KOMPONENTENTEST_DP | int | Status Dosierpumpe 0-&gt;DP nicht aktiv 1-&gt;DP aktiv max. Zeitangabe: 10s |
| SHZH_KOMPONENTENTEST_BLG | int | Status Brennluftgebläse 0-&gt;BLG nicht aktiv 1-&gt;BLG aktiv max. Zeitangabe: 60s |
| SHZH_KOMPONENTENTEST_GS | int | Status Glühstift 0-&gt;GS nicht aktiv 1-&gt;GS aktiv max. Zeitangabe: 60s |
| SHZH_KOMPONENTENTEST_USV | int | 0  -&gt; AUS 1  -&gt; 10% Taktung 2  -&gt; 20% Taktung 3  -&gt; 30% Taktung 4  -&gt; 40% Taktung 5  -&gt; 50% Taktung 6  -&gt; 60% Taktung 7  -&gt; 70% Taktung 8  -&gt; 80% Taktung 9  -&gt; 90% Taktung 10 -&gt; 100% Taktung max. Zeitangabe: 254s |
| SHZH_KOMPONENTENTEST_TESTZEIT | int | UP  max.254s KV  max.10s DP  max.10s BLG max.60s GS  max.60s USV max.254s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shzh-umwaelzpumpe"></a>
### STEUERN_SHZH_UMWAELZPUMPE

sTEUERN UMWAELZPUMPE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SHZH_KOMPONENTENTEST_TESTZEIT | int | max. Zeitangabe: 254s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shzh-umschaltventil"></a>
### STEUERN_SHZH_UMSCHALTVENTIL

Steuern Umschaltventil Ventil steht auf SH Kreislauf=bestromt=100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SHZH_KOMPONENTENTEST_TESTZEIT | int | max. Zeitangabe: 254s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shzh"></a>
### STEUERN_SHZH

Steuern SHZH BITTE BEACHTEN: Das Gerät schaltet sich nach Erreichen des Volllast automatisch ab!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SHZH_CTRL | int | 1-&gt;EIN 0-&gt;AUS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shzh-expert"></a>
### STEUERN_SHZH_EXPERT

Prüfbetrieb Expert BITTE BEACHTEN: Prüfbetrieb 1 : Das Gerät schaltet sich nach Erreichen des Volllast automatisch ab! Prüfbetrieb 2: Das Gerät schaltet sich nach 10min automatisch ab!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PASSWORT | int | Dieser Job ist mit Passwort geschützt |
| STAT_UMWAELZPUMPE | int | Status Umwälzpumpe 0 -&gt; Nicht aktiv 1 -&gt; Aktiv |
| STAT_UMSCHALTVENTIL | int | Status Umschaltventil |
| SHZG_PRUEFBETRIEB | int | Prüfbetrieb 1/2 PB1-&gt;5 PB2-&gt;9 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shzh-hgv-reset"></a>
### STEUERN_SHZH_HGV_RESET

Heizgeräteverriegelung reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shzh-testabbruch"></a>
### STEUERN_SHZH_TESTABBRUCH

Testabbruch

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shzh-leitungsbefuellung"></a>
### STEUERN_SHZH_LEITUNGSBEFUELLUNG

Leitungsbefuellung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SHZH_DAUER_LEITUNGSBEFUELLUNG | int | Dauer Leitungsbefüllung max 120Sec |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-shzh-seriennummer"></a>
### STATUS_SHZH_SERIENNUMMER

Heizgerätenummer auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERIENNUMMER | string | Heizgerätenummer |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG_SATZ1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_SATZ2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SATZ2 | binary | Hex-Antwort von SG |

<a id="job-status-shzh-lin-product-id"></a>
### STATUS_SHZH_LIN_PRODUCT_ID

LIN Product Identification auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LIN_PRODUCT_ID | string | LIN Product ID |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-shzh-ueber-app-nachricht"></a>
### STATUS_SHZH_UEBER_APP_NACHRICHT

Statusinformation über Applikationsnachricht auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SHZH_NAME | string | Name des Status der Standheizung / Zuheizung |
| STAT_SHZH_BESCHREIBUNG | string | Beschreibung des Status der Standheizung / Zuheizung |
| STAT_BETRIEBSMODUS_NAME | string | Status Betriebsmodus Name |
| STAT_BETRIEBSMODUS_BESCHREIBUNG | string | Status Betriebsmodus Beschreibung |
| STAT_WASSERPUMPE | string | Status Wasserpumpe |
| STAT_KRAFTSTOFFVORWAERMUNG | string | Status Kraftstoffvorwärmung |
| STAT_DOSIERPUMPE | string | Status Dosierpumpe |
| STAT_BRENNLUFTGEBLAESE | string | Status Brennluftgebläse |
| STAT_GLUESTIFT | string | Status Glühstift |
| STAT_UMSCHALTVENTIL | string | Status Umschlatventil |
| STAT_TESTBETRIEB | string | Status Testbetrieb |
| STAT_FEHLER | string | Status Fehler |
| STAT_COM_ERROR | string | Status Kommunikationsfehler |
| STAT_PWM_BRENNLUFTGEBLAESE_PROZENT | int | Status PWM Brennluftgebläse in Prozent |
| STAT_PWM_GLUEHSTIFT_PROZENT | int | Status PWM Glühstift in Prozent |
| STAT_PWM_KRAFTSTOFFVORWAERMUNG_PROZENT | int | Status PWM Kraftstoffvorwärmung in Prozent |
| STAT_WASSERTEMPERATUR_CELSIUS | int | Status Wassertemperatur in Grad Celsius |
| STAT_DOSIERPUMPENFREQUENZ_PERIODENDAUER_HERZ | int | Status Dosierpumpenfrequenz / Periodendauer in Herz |
| JOB_STATUS | string | OK, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klappen-verstellbereich"></a>
### STATUS_KLAPPEN_VERSTELLBEREICH

Lesen des aktuellen Status der Verstellbereiche alle Motoren ermittelt über den Eichlauf. 65535 = Fehlerwert, Komponente nicht vorhanden KWP2000: $21 ReadDataByLocalIdentifier $15 Klappen Verstellbereich (recordLocalIdentifier) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERSTELLBEREICH_DATEN | binary | Angabe des Verstellbereichs in Inkrementen Byte0=Status Eichlauf Byte1,2=DEF Byte3,4=FL/UML/SD Byte5,6=Mischluft rechts Byte7,8=Fußraum Byte9,10=Belüftung Byte11,12=Mischluft links Byte13,14=Fond (nur E9X) Byte15,16=Schichtung (nur E9X) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VERSTELLBEREICH_STATUS | unsigned char | 0x00 = keine gültigen Schrittweiten für Klappenmotoren vorhanden 0x01 = gültigen Schrittweiten für Klappenmotoren vorhanden |
| STAT_VERSTELLBEREICH_TEXT | string | Repräsentation von STAT_VERSTELLBEREICH_STATUS |
| STAT_VERSTELLBEREICH_DEFROST_WERT | unsigned int | Verstellbereich des Defrostmotors |
| STAT_VERSTELLBEREICH_FRISCHLUFT_UMLUFT_WERT | unsigned int | Verstellbereich des Frischluft- /Umluftmotors  in Inkrementen |
| STAT_VERSTELLBEREICH_MISCHLUFT_RECHTS_WERT | unsigned int | Verstellbereich des Mischluftmotors rechts |
| STAT_VERSTELLBEREICH_FUSSRAUM_WERT | unsigned int | Verstellbereich des Fussraummotors |
| STAT_VERSTELLBEREICH_BELUEFTUNG_WERT | unsigned int | Verstellbereich des Belüftungsmotors |
| STAT_VERSTELLBEREICH_MISCHLUFT_LINKS_WERT | unsigned int | Verstellbereich des Mischluftmotors links |
| STAT_VERSTELLBEREICH_FOND_WERT | unsigned int | Verstellbereich des Fondschichtungsmotors |
| STAT_VERSTELLBEREICH_FRONT_SCHICHTUNG_WERT | unsigned int | Verstellbereich des Frontschichtungsmotors |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [CBSKENNUNG](#table-cbskennung) (16 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (70 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 9)
- [FARTTYP](#table-farttyp) (70 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (51 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [IOPORTTAB](#table-ioporttab) (35 × 2)
- [FASTABLOCKTAB](#table-fastablocktab) (29 × 2)
- [ZUSTANDTEXTE](#table-zustandtexte) (99 × 3)
- [VARIANTEN](#table-varianten) (4 × 2)
- [TESTLAUF](#table-testlauf) (3 × 2)
- [IOSTATUSTAB](#table-iostatustab) (3 × 2)
- [FEHLERCODETABELLE](#table-fehlercodetabelle) (37 × 3)
- [STATUS_SHZH](#table-status-shzh) (11 × 3)
- [STATUS_WASSERPUMPE](#table-status-wasserpumpe) (4 × 3)
- [STATUS_BETRIEBSMODUS](#table-status-betriebsmodus) (4 × 3)
- [STATUS_KRAFTSTOFFVORWAERMUNG](#table-status-kraftstoffvorwaermung) (3 × 3)
- [STATUS_DOSIERPUMPE](#table-status-dosierpumpe) (3 × 3)
- [STATUS_BRENNLUFTGEBLAESE](#table-status-brennluftgeblaese) (3 × 3)
- [STATUS_GLUEHSTIFT](#table-status-gluehstift) (3 × 3)
- [STATUS_UMSCHALTVENTIL](#table-status-umschaltventil) (13 × 3)
- [STATUS_TESTBETRIEB](#table-status-testbetrieb) (3 × 3)
- [STATUS_FEHLER](#table-status-fehler) (4 × 3)
- [STATUS_COMERROR](#table-status-comerror) (2 × 3)

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

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 16 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x04 | Filt | Mikrofilter |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x07 | CSF | Dieselpartikelfilter |
| 0x08 | Batt | Batterie |
| 0x09 | VTG | Verteilergetriebeoel |
| 0x10 | ZKrz | Zuendkerzen |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x12 | Kfl | Kuehlfluessigkeit |
| 0x13 | H2 | H2-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x16 | DAD | Additiv fuer Partikelfilter |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |

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

Dimensions: 70 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9C48 | Mischluftklappe links (LIN) |
| 0x9C49 | Mischluftklappe rechts (LIN) |
| 0x9C4A | Frischluft/Umluft/Staudruckklappe (LIN) |
| 0x9C4B | Defrostklappe (LIN) |
| 0x9C4C | Fußraumklappe (LIN) |
| 0x9C4D | Zentralantrieb (LIN) |
| 0x9C4E | Schichtungsklappe (LIN) |
| 0x9C50 | Fondbelüftungsklappe (LIN) |
| 0x9C52 | Belüftungsklappe (LIN) |
| 0x9C53 | PTC (LIN) |
| 0x9C54 | Autoadressierung (LIN) |
| 0x9C56 | Temperaturfühler Fußraum |
| 0x9C58 | Temperaturfühler Innenraum |
| 0x9C5F | Temperaturfühler Belüftung |
| 0x9C61 | 5V-Ausgang Peripherie |
| 0x9C62 | Temperarturfühler Verdampfer |
| 0x9C63 | Schalter Kulissenscheibe |
| 0x9C6C | 12V-Ausgang Peripherie |
| 0x9C6E | Sonnensensor |
| 0x9C75 | Unter-/Überspannung |
| 0x9C7B | Innenraumfühlergebläse |
| 0x9C90 | Steuergerät defekt |
| 0x9C97 | Schichtungspoti |
| 0x9CA7 | Energiesparmode aktiv |
| 0x9CA8 | Standheizung systembedingte Abschaltung |
| 0x9CA9 | Standheizung Kommunikation |
| 0x9CB0 | Standheizung Glühstift |
| 0x9CB1 | Standheizung Brennluftgebläse |
| 0x9CB2 | Standheizung Wasserpumpe |
| 0x9CB3 | Standheizung Magnetventil |
| 0x9CB4 | Standheizung Dosierpumpe |
| 0x9CB5 | Standheizung Temperatursensor |
| 0x9CB6 | Standheizung Über/Unterspannung |
| 0x9CB7 | Standheizung Gerät |
| 0x9CB8 | Standheizung Überhitzungssensor |
| 0x9CB9 | Standheizung Flamme Start |
| 0x9CBA | Standheizung Kraftstoff Vorwärmung |
| 0x9CBB | Standheizung LIN-Kommunikation |
| 0x9CBC | Standheizung System |
| 0x9CBD | Standheizung Absperrventil |
| 0xE704 | CAN-BUS. Physikalischer Busfehler |
| 0xE707 | Can-Bus off |
| 0xE714 | Can-Botschaft Klemmenstatus |
| 0xE715 | Can-Botschaft Außentemperatur |
| 0xE716 | Can-Botschaft Dimmung |
| 0xE717 | Can-Botschaft Motordaten |
| 0xE718 | Can-Botschaft Status Druck Kältekreislauf |
| 0xE719 | Can-Botschaft Kilometerstand/Reichweite |
| 0xE71A | Can-Botschaft Drehmoment 3 |
| 0xE71B | Can-Botschaft Wärmestrom Motor |
| 0xE71C | Can-Botschaft Geschwindigkeit |
| 0xE71D | Can-Botschaft Status PDC |
| 0xE71E | Can-Botschaft Status BFS |
| 0xE71F | Can-Botschaft Status FAS |
| 0xE720 | Can-Botschaft Powermanagement Verbrauchersteuerung |
| 0xE721 | Can-Botschaft Status Sensor AUC |
| 0xE722 | Can-Botschaft Status Funkschlüssel |
| 0xE723 | CAN-Botschaft Status Beschlag Scheibe vorn |
| 0xE724 | CAN-Botschaft Status Schichtung Fond |
| 0xE725 | CAN-Botschaft Fahrgestellnummer |
| 0xE726 | CAN-Botschaft Einheiten |
| 0xE727 | CAN-Botschaft LCD-Leuchtdichte |
| 0xE728 | CAN-Botschaft Relativzeit |
| 0xE729 | CAN-Botschaft Status HDC |
| 0xE72A | CAN-Botschaft Status Wasserventil |
| 0xE72B | CAN-Botschaft Status Zusatzwasserpumpe |
| 0xE72C | CAN-Botschaft Crash |
| 0xE72D | CAN-Botschaft Status Ventil Klimakompressor |
| 0xE72E | CAN-Botschaft Status MSA |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | 0x03 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Aussentemperatur | Grad C | - | unsigned char | - | 1 | 2 | -40 |
| 0x02 | Kuehlmitteltemperatur | Grad C | - | unsigned char | - | 1 | 1 | -48 |
| 0x03 | Batteriespannung | Volt | - | unsigned char | - | 1 | 10 | 0 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 70 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x9C48 | 0x001C | 0x000B | 0x000A | 0x0009 |
| 0x9C49 | 0x001C | 0x000B | 0x000A | 0x0009 |
| 0x9C4A | 0x001C | 0x000B | 0x000A | 0x0009 |
| 0x9C4B | 0x001C | 0x000B | 0x000A | 0x0009 |
| 0x9C4C | 0x001C | 0x000B | 0x000A | 0x0009 |
| 0x9C4D | 0x001C | 0x000B | 0x000A | 0x0009 |
| 0x9C4E | 0x001C | 0x000B | 0x000A | 0x0009 |
| 0x9C50 | 0x001C | 0x000B | 0x000A | 0x0009 |
| 0x9C52 | 0x001C | 0x000B | 0x000A | 0x0009 |
| 0x9C53 | 0x000F | 0x000E | 0x000D | 0x000C |
| 0x9C54 | 0x0018 | 0x001D | 0x0018 | 0x0018 |
| 0x9C56 | 0x0018 | 0x0018 | 0x0019 | 0x001A |
| 0x9C58 | 0x0018 | 0x0018 | 0x0019 | 0x001A |
| 0x9C5F | 0x0018 | 0x0018 | 0x0019 | 0x001A |
| 0x9C61 | 0x0018 | 0x0018 | 0x0018 | 0x0010 |
| 0x9C62 | 0x0018 | 0x0018 | 0x0019 | 0x001A |
| 0x9C63 | 0x0018 | 0x0011 | 0x0019 | 0x0018 |
| 0x9C6C | 0x0013 | 0x0018 | 0x0019 | 0x0012 |
| 0x9C6E | 0x0018 | 0x0018 | 0x0019 | 0x001A |
| 0x9C75 | 0x0014 | 0x0018 | 0x0018 | 0x0018 |
| 0x9C7B | 0x0018 | 0x0018 | 0x000A | 0x0018 |
| 0x9C90 | 0x0018 | 0x0018 | 0x0018 | 0x0015 |
| 0x9C97 | 0x0018 | 0x0018 | 0x001B | 0x001A |
| 0x9CA7 | 0x0018 | 0x0018 | 0x0018 | 0x0018 |
| 0x9CA8 | 0x0037 | 0x0038 | 0x0039 | 0x003a |
| 0x9CA9 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0x9CB0 | 0x001E | 0x001F | 0x0019 | 0x001A |
| 0x9CB1 | 0x0020 | 0x000A | 0x0019 | 0x001A |
| 0x9CB2 | 0x0018 | 0x0018 | 0x0019 | 0x001A |
| 0x9CB3 | 0x0018 | 0x0018 | 0x0019 | 0x001A |
| 0x9CB4 | 0x0018 | 0x0018 | 0x0019 | 0x001A |
| 0x9CB5 | 0x0008 | 0x0018 | 0x0019 | 0x001A |
| 0x9CB6 | 0x0018 | 0x0018 | 0x0021 | 0x0035 |
| 0x9CB7 | 0x0022 | 0x0023 | 0x0024 | 0x0036 |
| 0x9CB8 | 0x0018 | 0x0018 | 0x0018 | 0x001A |
| 0x9CB9 | 0x0027 | 0x0026 | 0x0028 | 0x0029 |
| 0x9CBA | 0x0018 | 0x0018 | 0x0019 | 0x001A |
| 0x9CBB | 0x0030 | 0x0031 | 0x003b | 0x0032 |
| 0x9CBC | 0x0018 | 0x0018 | 0x0033 | 0x0034 |
| 0x9CBD | 0x0018 | 0x0018 | 0x0019 | 0x001A |
| 0xE704 | 0x0018 | 0x0018 | 0x0018 | 0x0018 |
| 0xE707 | 0x0018 | 0x0018 | 0x0018 | 0x0016 |
| 0xE714 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE715 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE716 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE717 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE718 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE719 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE71A | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE71B | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE71C | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE71D | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE71E | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE71F | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE720 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE721 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE722 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE723 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE724 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE725 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE726 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE727 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE728 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE729 | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE72A | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE72B | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE72C | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE72D | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| 0xE72E | 0x0018 | 0x0017 | 0x0018 | 0x0018 |
| default | 0x0008 | 0x0004 | 0x0002 | 0x0001 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 51 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0004 | kein Signal oder Wert |
| 0x0008 | unplausibles Signal oder Wert |
| 0x0009 | Interner Fehler Stellmotor |
| 0x000A | Blockierung |
| 0x000B | Motor antwortet nicht |
| 0x000C | Übertemperatur |
| 0x000D | Kurzschluß, fehlerhafter Heizerstrang |
| 0x000E | Keine Antwort |
| 0x000F | PWM fehlt |
| 0x0010 | Überstrom |
| 0x0011 | Kein Signal/Wert |
| 0x0012 | Unterspannung |
| 0x0013 | Überspannung |
| 0x0014 | Unter- oder Überspannung erkannt |
| 0x0015 | Interner Fehler |
| 0x0016 | Error Passiv |
| 0x0017 | Timeout |
| 0x0018 | Nicht verwendet |
| 0x0019 | Kurzschluß gegen Masse |
| 0x001A | Kurzschluß gegen Ubatt oder Leitungsunterbrechung |
| 0x001B | Kurzschluß gegen Masse oder Ausfall 5V-Versorgung Peripherie |
| 0x001C | Fehlerhafte Schrittweite |
| 0x001D | Autoadressierung fehlerhaft |
| 0x001E | Fremdlicht (Wendel defekt/unterbrochen) od. Glühstift defekt |
| 0x001F | Referenzwiderstand nicht erreicht |
| 0x0020 | Schwergängigkeit |
| 0x0021 | Unterspannung (intern) |
| 0x0022 | EOL-Checksumfehler |
| 0x0023 | Steuergerät defekt |
| 0x0024 | Heizgerät verriegelt |
| 0x0025 | Sicherung defekt |
| 0x0026 | Kein Start: keine Flamme im Normalbetrieb |
| 0x0027 | Kein Start: keine Flamme im Testbetrieb |
| 0x0028 | Flammabbruch: wiederholter Abbruch im Heizzyklus |
| 0x0029 | Flammabbruch |
| 0x0030 | Signal mit Ungültigkeitssignatur |
| 0x0031 | LIN-Timeout (-&gt;Notlauf: Abschaltung) |
| 0x0032 | Bit-Error |
| 0x0033 | Not aus wurde angefordet, qualmen möglich |
| 0x0034 | Überschreitung Heizvorgabe |
| 0x0035 | Überspannung (intern) |
| 0x0036 | Überhitzung |
| 0x0037 | Powermodulabschaltung |
| 0x0038 | Unterschreiten der Restreichweite |
| 0x0039 | Abschaltung durch Fehler ZWP |
| 0x003a | Abschaltung durch Fehler USV |
| 0x003b | Baudratedetection fehlgeschlagen |
| 0xFFFF | unbekannte Fehlerart |

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

<a id="table-ioporttab"></a>
### IOPORTTAB

Dimensions: 35 rows × 2 columns

| PORTNUMBER | PORTNAME |
| --- | --- |
| 0x01 | ECU-Tasten |
| 0x02 | ECU-Funktionsbeleuchtung |
| 0x03 | SZM-Funktionsbeleuchtung |
| 0x04 | SZM-Tasten |
| 0x05 | SZM-Variante |
| 0x06 | Error-Flags |
| 0x07 | 12V-Ausgang |
| 0x08 | 5V-Ausgang |
| 0x09 | Ausgänge SZM |
| 0x0A | Display |
| 0x10 | Drehsteller-Sollwerte |
| 0x11 | SZM |
| 0x12 | Spannung 12V-Ausgang |
| 0x13 | Analog-Sensoren |
| 0x15 | Gebläse |
| 0x16 | IHX-Daten |
| 0x17 | Innenfühlergebläse |
| 0x20 | LinFrischluftUml |
| 0x21 | LinMischluftLi |
| 0x22 | LinMischluftRe |
| 0x23 | LinBelueftung |
| 0x24 | LinFussraum |
| 0x25 | LinDefrost |
| 0x26 | LinPTC |
| 0x27 | LinFond |
| 0x28 | LinSchichtung |
| 0x30 | PWM-Funktionsbeleuchtung |
| 0x31 | PWM-Ringsuchbeleuchtung |
| 0x32 | PWM-Tastensuchbeleuchtung |
| 0x33 | PWM-Displaybeleuchtung |
| 0x34 | PWM-Displaykontrast |
| 0x35 | PWM-SZM-Funktionsbeleuchtung |
| 0x36 | PWM-SZM-Suchbeleuchtung |
| 0x37 | PWM-Beleuchtung |
| 0x40 | Sollwerte |

<a id="table-fastablocktab"></a>
### FASTABLOCKTAB

Dimensions: 29 rows × 2 columns

| BLOCKNUMBER | BLOCKNAME |
| --- | --- |
| 0x00 | Gesamtbetriebsstunden |
| 0x01 | Anzahl der Resets |
| 0x02 | Richtungswechsel Mischluft links |
| 0x03 | Richtungswechsel Mischluft rechts |
| 0x04 | Richtungswechsel Frischluft/Umluft |
| 0x05 | Richtungswechsel Defrost |
| 0x06 | Richtungswechsel Belüftung |
| 0x07 | Richtungswechsel Fußraum |
| 0x08 | Richtungswechsel Schichtung front |
| 0x09 | Richtungswechsel Schichtung fond |
| 0x0B | Blockierungen Mischluft links |
| 0x0C | Blockierungen Mischluft rechts |
| 0x0D | Blockierungen Frischluft/Umluft |
| 0x0E | Blockierungen Defrost |
| 0x0F | Blockierungen Belüftung |
| 0x10 | Blockierungen Fußraum |
| 0x11 | Blockierungen Schichtung front |
| 0x12 | Blockierungen Schichtung fond |
| 0x14 | Betriebsstunden Klappenautomatik |
| 0x15 | Betriebsstunden Gebläseautomatik |
| 0x16 | Deaktivierungen Klappenautomatik |
| 0x17 | Deaktivierungen Gebläseautomatik |
| 0x18 | Betriebsstunden Klimabetrieb |
| 0x19 | Betriebsstunden AUC-Betrieb |
| 0x1A | Deaktivierungen der AUC-Funktion |
| 0x1B | Aktivierungen der REST-Funktion |
| 0x1C | Betriebsstunden OFF-Funktion |
| 0x1D | Aktivierungen der OFF-Funktion |
| 0x1E | Aktivierungen der Defrost aus Vollautomatik |

<a id="table-zustandtexte"></a>
### ZUSTANDTEXTE

Dimensions: 99 rows × 3 columns

| NUMMER | ABKUERZUNG | TEXT |
| --- | --- | --- |
| 0x00 | ABR | Ausbrennen |
| 0x01 | ABSCH | Abschaltung |
| 0x02 | ABT | Ausbrennen TRS |
| 0x03 | AKÜ | Ausbrennrampe |
| 0x04 | AUS | Auszustand |
| 0x05 | BBTL | Brennbetrieb Teillast |
| 0x06 | BBVL | Brennbetrieb Volllast |
| 0x07 | BFÖ | Brennstofffördern |
| 0x08 | BMS | Brennermotorstart (Losreissen) |
| 0x09 | BU | Brennstoffunterbr |
| 0x0A | DIAG | Diagnosezustand |
| 0x0B | DPU | Dosierpumpenunterbrechung |
| 0x0C | EMK | EMK-Messung |
| 0x0D | EPR | Entprellen |
| 0x0E | EXIT | EXIT |
| 0x0F | FLA | Flammwächterabfrage |
| 0x10 | FLK | Flammwächterkühlung |
| 0x11 | FLM | Flammwächter Messphase |
| 0x12 | FLZ | Flammabfrage bei ZUE |
| 0x13 | GA | Gebläseanlauf |
| 0x14 | GSR | Glühstiftrampe |
| 0x15 | HGV | Heizgeräteverriegelung |
| 0x16 | INIT | Initialisierung |
| 0x17 | KBÜ | Kraftstoffblasenüberbrückung |
| 0x18 | KGA | Kaltgebläseanlauf |
| 0x19 | KSA | Kaltstartanreicherung |
| 0x1A | KÜG | Kühlung |
| 0x1B | LTV | Lastwechsel Teil- / Volllast |
| 0x1C | LÜE | Lüften |
| 0x1D | LVT | Lastwechsel Voll- / Teillast |
| 0x1E | Neu INIT | Neue Initialisierung |
| 0x1F | RB | Regelbetrieb |
| 0x20 | RP | Regelpause |
| 0x21 | SAN | Sanftanlauf |
| 0x22 | SIZ | Sicherheitszeit |
| 0x23 | SPÜ | Spülen |
| 0x24 | STA | Start |
| 0x25 | STAB | Stabilisierung |
| 0x26 | STR | Startrampe |
| 0x27 | Stromlos | Stromlos |
| 0x28 | STV | Störverriegelung |
| 0x29 | STV_TRS | Störverriegelung TRS |
| 0x2A | STZ | Stabilisierungszeit |
| 0x2B | ÜRB | Übergang Regelbetrieb |
| 0x2C | USA | Entscheidungsknoten |
| 0x2D | VFÖ | Vorfördern |
| 0x2E | VGL | Vorglühen |
| 0x2F | VGLP | Vorglühen Leistungsregelung |
| 0x30 | VZG | Verzögerung vor Abregeln |
| 0x31 | ZGA | Zähgebläseanlauf |
| 0x32 | ZGL | Zuglühen |
| 0x33 | ZP | Zündpause |
| 0x34 | ZUE | Zündung |
| 0x35 | ZWGL | Zwischenglühen |
| 0x36 | APP | Applikationsüberwachung |
| 0x37 | HGA | Heizgeräteverriegelungsabspeicherung |
| 0x38 | HGE | Heizgeräteentriegelung |
| 0x39 | HLR | Heizleistungsregelung |
| 0x3A | UPR | Umwälzpumpenregelung |
| 0x3B | µP-\| | Initialisierung µP |
| 0x3C | FL | Fremdlichtabfrage |
| 0x3D | VL | Vorlauf |
| 0x3E | VZ | Vorzündung |
| 0x3F | FZ | Flammzündung |
| 0x40 | FS | Flammstabilisierung |
| 0x41 | BBS | Brennbetrieb Standheizen |
| 0x42 | BBZ | Brennbetrieb Zuheizen |
| 0x43 | BSS | Brennstörung Standheizen |
| 0x44 | BSZ | Brennstörung Zuheizen |
| 0x45 | AN | Aus Nachlauf |
| 0x46 | RPN | Regelpause Nachlauf |
| 0x47 | SN | Störnachlauf |
| 0x48 | ZSN | Zeitlicher Störnachlauf |
| 0x49 | STVU | Störverriegelung Umwälzpumpe |
| 0x4A | RPS | Regelpause Standheizen |
| 0x4B | RPZ | Regelpause Zuheizen |
| 0x4C | RPZU | Regelpause Zuheizen mit Umwälzpumpe |
| 0x4D | UP | Umwälzpumpe ohne Heizfunktion |
| 0x4E | WSUE | Warteschleife Überspannung |
| 0x4F | FSA | Fehlerspeicher aktualisieren |
| 0x50 | WS | Warteschleife |
| 0x51 | KOMP | Komponententest |
| 0x52 | BOOST | Boostbetrieb |
| 0x53 | ABK | Abkühlen |
| 0x54 | HGVP | Heizgeräteverriegelung permanent |
| 0x55 | GBU | Gebläseunterbrechung |
| 0x56 | LOS | Brennermotor losreissen |
| 0x57 | TA | Temperaturabfrage |
| 0x58 | VUS | Vorlauf Unterspannung |
| 0x59 | UNF | Unfallabfrage |
| 0x5A | SNMV | Störnachlauf Magnetventil |
| 0x5B | FSAMV | Fehlerspeicher aktualisieren Magnetventil |
| 0x5C | ZSNMV | Zeitlicher Störnachlauf Magnetventil |
| 0x5D | SV | Startversuch |
| 0x5E | VLV | Vorlaufverlängerung |
| 0x5F | BB | Brennbetrieb |
| 0x60 | ZSNUS | zeitlicher Störnachlauf bei Unterspannung |
| 0x61 | FSAA | Fehlerspeicher aktualisieren beim Ausschalten |
| 0x62 | RAVL | Rampe Vollast |

<a id="table-varianten"></a>
### VARIANTEN

Dimensions: 4 rows × 2 columns

| VARIANTE | TEXT |
| --- | --- |
| 0x01 | Benzin |
| 0x02 | Diesel |
| 0x04 | RME |
| 0xFF | ungültig |

<a id="table-testlauf"></a>
### TESTLAUF

Dimensions: 3 rows × 2 columns

| TESTLAUFCODE | TEXT |
| --- | --- |
| 0x00 | Testlauf niO |
| 0x01 | Testlauf iO |
| 0xFF | ungültig |

<a id="table-iostatustab"></a>
### IOSTATUSTAB

Dimensions: 3 rows × 2 columns

| IOSTATUS | TEXT |
| --- | --- |
| 0x00 | NEIN |
| 0x01 | JA |
| 0x03 | ungültig (aktiver Fehler) |

<a id="table-fehlercodetabelle"></a>
### FEHLERCODETABELLE

Dimensions: 37 rows × 3 columns

| FEHLERCODE | FEHLERORT | FEHLERART |
| --- | --- | --- |
| 0x8A | SHZH Glühstift | SHZH Glühstift Unterbrechung / Kurzschluss nach Plus |
| 0x0A | SHZH Glühstift | SHZH Glühstift Kurzschluß nach Masse |
| 0x22 | SHZH Glühstift | SHZH Glühstift Referenzwiderstand nicht erreicht |
| 0x99 | SHZH Glühstift | SHZH Glühstift defekt |
| 0x05 | SHZH Glühstift | SHZH Glühstift hat als Brennraumsensor vor dem Brennbetrieb eine Flamme erkannt Fremdlicht (Wendel defekt/unterbrochen) |
| 0x89 | SHZH Brennluftgebläse | SHZH Brennluftgebläse Unterbrechung / Kurzschluss nach Plus |
| 0x09 | SHZH Brennluftgebläse | SHZH Brennluftgebläse Unterbrechung / Kurzschluss nach Masse |
| 0x15 | SHZH Brennluftgebläse | SHZH Brennluftgebläse Blockierschutz hat angesprochen (EMK) |
| 0x95 | SHZH Brennluftgebläse | SHZH Brennluftgebläse Schwergängigkeitserkennung hat angesprochen (EMK) |
| 0x8B | SHZH Wasserpumpe | SHZH Wasserpumpe Unterbrechung / Kurzschluss nach Plus |
| 0x0B | SHZH Wasserpumpe | SHZH Wasserpumpe Kurzschluß nach Masse |
| 0x90 | SHZH Umschaltventil | SHZH Umschaltventil Unterbrechung / Kurzschluss nach Plus |
| 0x10 | SHZH Umschaltventil | SHZH Umschaltventil Kurzschluß nach Masse |
| 0x88 | SHZH Dosierpumpe | SHZH Dosierpumpe Unterbrechung / Kurzschluss nach Plus |
| 0x08 | SHZH Dosierpumpe | SHZH Dosierpumpe Kurzschluß nach Masse |
| 0x94 | SHZH Wassertemperatursensor | SHZH Wassertemperatursensor Unterbrechung / Kurzschluss nach Plus |
| 0x14 | SHZH Wassertemperatursensor | SHZH Wassertemperatursensor Kurzschluß nach Masse |
| 0x04 | SHZH Unter-/Überspannung | SHZH Unter-/Überspannung Die Spannung war länger als die eingestellte Maximalzeit in Überspannung |
| 0x84 | SHZH Unter-/Überspannung | SHZH Unter-/Überspannung Die Spannung war länger als die eingestellte Maximalzeit in. Unterspannung |
| 0x06 | SHZH Gerät | SHZH Gerät Überhitzung ist aufgetreten |
| 0x07 | SHZH Gerät | SHZH Gerät Heizgerät verriegelt |
| 0x01 | SHZH Gerät | SHZH Gerät Steuergerät defekt (RAM,ROM,SW) |
| 0x81 | SHZH Gerät | SHZH Gerät EOL-Checksummenfehler |
| 0xAB | SHZH Überhitzungssensor | SHZH Überhitzungssensor Unterbrechung / Kurzschluss nach Plus |
| 0x03 | SHZH Flamme-Start | SHZH Flamme-Start Flammabbruch |
| 0x83 | SHZH Flamme-Start | SHZH Flamme-Start Flammabbruch: wiederholter Abbruch im Heizzyklus |
| 0x02 | SHZH Flamme-Start | SHZH Flamme-Start Kein Start: keine Flamme im Normalbetrieb |
| 0x82 | SHZH Flamme-Start | SHZH Flamme-Start Kein Start: keine Flamme im Testbetrieb |
| 0xA5 | SHZH Kraftstoffvorwärmung | SHZH Kraftstoffvorwärmung Unterbrechung / Kurzschluss nach Plus |
| 0x25 | SHZH Kraftstoffvorwärmung | SHZH Kraftstoffvorwärmung Kurzschluß nach Masse |
| 0x60 | SHZH LIN-Kommunikationsfehler | SHZH LIN-Kommunikationsfehler Bit Error bzw. falsche Checksumme |
| 0x61 | SHZH LIN-Kommunikationsfehler | SHZH LIN-Kommunikationsfehler Bauratedetection fehlgeschlagen |
| 0x62 | SHZH LIN-Kommunikationsfehler | SHZH LIN-Kommunikationsfehler LIN-Timeout (-&gt; Notlauf: Abschaltung) |
| 0x63 | SHZH LIN-Kommunikationsfehler | SHZH LIN-Kommunikationsfehler Signal mit Ungültigkeitssignatur, ungültiger Wertebereich oder Nachricht mit ungültigen Signalkombinationen hat bis zum Ungültigkeits-Timeout angestanden |
| 0x70 | SHZH System-Fehler | SHZH System-Fehler Überschreitung der Heizzeitvorgabe |
| 0x71 | SHZH System-Fehler | SHZH System-Fehler Notaus (ohne Nachlauf) wurde angefordert, qualmen möglich |
| 0x29 | SHZH System-Fehler | SHZH System-Fehler Leitungsbefüllung nicht erfolgt |

<a id="table-status-shzh"></a>
### STATUS_SHZH

Dimensions: 11 rows × 3 columns

| CODE | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | AUS-Bereit | Heizgerät AUS und in Bereitschaft |
| 0x01 | AUS-Nachlauf | Heizgerät befindet sich im Nachlauf (Wasserpumpe ist anzusteuern). |
| 0x02 | AUS – Störungsnachlauf-Gemeldet | Heizgerät hat sich aufgrund eines Fehlers oder wegen Notaus abgeschaltet. Im Heizgerät findet ein Störungsnachlauf statt; Wasser-pumpe ist deshalb von der IHKA anzusteuern. Störung muß von der IHKA mittels AUS-Kommando quittiert werden. |
| 0x03 | AUS-Störungsnachlauf_Quittiert | Folgezustand zu &gt;&gt;AUS-Störungsnachlauf-Gemeldet&lt;&lt; nach erfolgter Quittung durch die IHKA. Störungsnachlauf findet weiterhin statt; Wasserpumpe ist deshalb von der IHKA anzusteuern. Nach Ende des Störungsnachlaufs geht das Heizgerät selbständig in den Zu-stand &gt;&gt;AUS – Bereit&lt;&lt; |
| 0x04 | EIN - Start | Heizgerät aktiv |
| 0x05 | EIN - Regelpause | Regelpause |
| 0x06 | EIN - Teillast | Teillastbetrieb |
| 0x07 | EIN - Vollast | Vollastbetrieb |
| 0x08 | AUS - Heizgeräteverriege-lung | Heizgerät ist verriegelt, Entriegelung notwendig. |
| 0x09 | Nachlauf - Regelpause | Nachlauf der in den Zustand Regelpause führt. |
| 0x0F | Signal ungültig | Ungültigkeitssignatur |

<a id="table-status-wasserpumpe"></a>
### STATUS_WASSERPUMPE

Dimensions: 4 rows × 3 columns

| CODE | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | AUS |  |
| 0x01 | EIN |  |
| 0x02 | Nicht verbaut |  |
| 0x03 | Signal ungültig | Ungültigkeitssignatur |

<a id="table-status-betriebsmodus"></a>
### STATUS_BETRIEBSMODUS

Dimensions: 4 rows × 3 columns

| CODE | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | Keine Auswahl | Keine Betriebsart ausgewählt, SHZH schaltet nicht ein. |
| 0x01 | Standheizen | Heizgerät arbeitet als Standheizer;Heizzeitvorgabe wird berücksichtigt |
| 0x02 | Zuheizen/Pseudozuheizen | Heizgerät arbeitet als Zuheizer (auch Pseudozuheizer); die Heiz-zeitvorgabe wird nicht berücksichtigt. |
| 0x03 | Signal ungültig | Ungültigkeitssignatur |

<a id="table-status-kraftstoffvorwaermung"></a>
### STATUS_KRAFTSTOFFVORWAERMUNG

Dimensions: 3 rows × 3 columns

| CODE | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | AUS | Kraftstoffvorwaermung ist aus |
| 0x01 | EIN | Kraftstoffvorwaermung ist aktiv |
| 0x03 | Signal ungültig | Ungültigkeitssignatur |

<a id="table-status-dosierpumpe"></a>
### STATUS_DOSIERPUMPE

Dimensions: 3 rows × 3 columns

| CODE | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | AUS | Dosierpumpe ist aus |
| 0x01 | EIN | Dosierpumpe wird angesteuert |
| 0x03 | Signal ungültig | Ungültigkeitssignatur |

<a id="table-status-brennluftgeblaese"></a>
### STATUS_BRENNLUFTGEBLAESE

Dimensions: 3 rows × 3 columns

| CODE | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | AUS | Brennluftgeblaese ist aus |
| 0x01 | EIN | Brennluftgeblaese wird angesteuert |
| 0x03 | Signal ungültig | Ungültigkeitssignatur |

<a id="table-status-gluehstift"></a>
### STATUS_GLUEHSTIFT

Dimensions: 3 rows × 3 columns

| CODE | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | AUS | Gluehstift ist aus |
| 0x01 | EIN | Gluehstift wird angesteuert |
| 0x03 | Signal ungültig | Ungültigkeitssignatur |

<a id="table-status-umschaltventil"></a>
### STATUS_UMSCHALTVENTIL

Dimensions: 13 rows × 3 columns

| CODE | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | AUS | Grosser Kries (Motor) =unbestromt=0% |
| 0x01 | 10% Taktung |  |
| 0x02 | 20% Taktung |  |
| 0x03 | 30% Taktung |  |
| 0x04 | 40% Taktung |  |
| 0x05 | 50% Taktung |  |
| 0x06 | 60% Taktung |  |
| 0x07 | 70% Taktung |  |
| 0x08 | 80% Taktung |  |
| 0x09 | 90% Taktung | 90% auf SH Kreislauf, Rest Motorkreislauf |
| 0x0A | USV EIN | Ventil steht auf SH Kreislauf=bestromt=100% |
| 0x0B | Nicht verbaut |  |
| 0x0F | Signal ungueltig | Ungültigkeitssignatur |

<a id="table-status-testbetrieb"></a>
### STATUS_TESTBETRIEB

Dimensions: 3 rows × 3 columns

| CODE | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | AUS | Testbetrieb nicht aktiv |
| 0x01 | EIN | Testbetrieb aktiv |
| 0x03 | Signal ungültig | Ungültigkeitssignatur |

<a id="table-status-fehler"></a>
### STATUS_FEHLER

Dimensions: 4 rows × 3 columns

| CODE | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | kein Fehler |  |
| 0x01 | Fehler aktiv |  |
| 0x02 | Fehler Statusänderung |  |
| 0x03 | Signal ungültig | Ungültigkeitssignatur |

<a id="table-status-comerror"></a>
### STATUS_COMERROR

Dimensions: 2 rows × 3 columns

| CODE | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 |  | Die Kommunikation verläuft fehlerfrei |
| 0x01 |  | In der vorherigen Nachricht wurde ein Fehler festgestellt |
