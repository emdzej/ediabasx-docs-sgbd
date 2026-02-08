# IHKA60.prg

- Jobs: [119](#jobs)
- Tables: [21](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | IHKA E60 |
| ORIGIN | BMW EI-63 Wünsche |
| REVISION | 6.08 |
| AUTHOR | Preh 1713 Arnold |
| COMMENT | SGBD IHKA E60 IS05-12-500 |
| PACKAGE | 1.32 |
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
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
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
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS Version 1-3) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS Version 1-3) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
- [STATUS_ANALOGEINGAENGE](#job-status-analogeingaenge) - Auslesen der 30 A/D-Werte (High), bzw. 16 A/D-Werte (Basis) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_DIGITALEINGAENGE](#job-status-digitaleingaenge) - Auslesen der Digitalen-Eingänge (High) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_REGLERGROESSEN](#job-status-reglergroessen) - Auslesen der 28 Byte Reglerinformationene KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_BEDIENTEIL](#job-status-bedienteil) - Auslesen der Bedienteileinstellungen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_IO](#job-status-io) - Auslesen der Ansteuer-Ports für externe Lasten KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - Auslesen der 9 Klappenpositionen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_FZE](#job-status-fze) - Auslesen der Stati der Filterzustandserkennung(FZE) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - Auslesen des aktuell eingestellten Energiesparmodes KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_STEUERORT_ZWP](#job-status-steuerort-zwp) - Auslesen des aktuell codierten Verbauort der ZWP KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_PTC_VERBAUT](#job-status-ptc-verbaut) - Auslesen ob PTC verbaut KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_ZUSATZLUEFTER_STUFE](#job-status-zusatzluefter-stufe) - Auslesen der Stufe des Zusatzluefters KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_BOOT_SW_VERSION](#job-status-boot-sw-version) - Auslesen der Boot-SW-Version KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_MOTOR_FEHLER](#job-status-motor-fehler) - Auslesen der Lin-Motoren-Fehler KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [DIAGNOSE_TESTBIT](#job-diagnose-testbit) - Ansteuern des Diagnosetest-Bits Das Bit kann ein- bzw. ausgeschaltet werden.
- [STEUERN_HECKSCHEIBEN_HEIZUNG](#job-steuern-heckscheiben-heizung) - Ansteuern der Heckscheibenheizugng im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_WASSERPUMPE](#job-steuern-wasserpumpe) - Ansteuern der Wasserpumpe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_SPRITZDUESEN_HEIZUNG](#job-steuern-spritzduesen-heizung) - Ansteuern der Spritzduesenheizung im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_WASSERVENTIL_LINKS](#job-steuern-wasserventil-links) - Ansteuern des linken Wasserventils (BASIS) im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_WASSERVENTIL_RECHTS](#job-steuern-wasserventil-rechts) - Ansteuern des rechten Wasserventils im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KAELTEMITTELVERDICHTER](#job-steuern-kaeltemittelverdichter) - Ansteuern des Kaeltemittelverdichters im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_GEBLAESE](#job-steuern-geblaese) - Ansteuern des Geblaeses im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_ZUSATZLUEFTER](#job-steuern-zusatzluefter) - Ansteuern des Zusatzluefters im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_ATEMP](#job-steuern-atemp) - Ansteuern der Aussentemperatur im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_PTC_DIAG_OL_AUS](#job-steuern-ptc-diag-ol-aus) - Fehlereintrag für Ptc bei Open Load verhindern KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [PTC_WERKSPROZESS](#job-ptc-werksprozess) - Ptc-Werksprozess KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_FRISCHLUFT_UMLUFT_LINKS](#job-steuern-frischluft-umluft-links) - Ansteuern der Frischluft-/Umluftklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_FRISCHLUFT_UMLUFT_RECHTS](#job-steuern-frischluft-umluft-rechts) - Ansteuern der Frischluft/Umluftklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_DEFROST](#job-steuern-klappe-defrost) - Ansteuern der Entfrostungsklappe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_BELUEFTUNG_LINKS](#job-steuern-klappe-belueftung-links) - Ansteuern der Belueftungsklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_BELUEFTUNG_RECHTS](#job-steuern-klappe-belueftung-rechts) - Ansteuern der Belueftungsklappe rechts (BASIS) im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_SCHICHTUNG](#job-steuern-klappe-schichtung) - Ansteuern der Schichtungsklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FUSSRAUM_LINKS](#job-steuern-klappe-fussraum-links) - Ansteuern der Fussraumklappe links (BASIS) im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FUSSRAUM_RECHTS](#job-steuern-klappe-fussraum-rechts) - Ansteuern der Fussraumklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FOND](#job-steuern-klappe-fond) - Ansteuern der Fondraumklappe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_PTC](#job-steuern-ptc) - Ansteuern des PTC im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_REGLERGROESSE_Y_LINKS](#job-steuern-reglergroesse-y-links) - Steuern der Reglergroesse links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_REGLERGROESSE_Y_RECHTS](#job-steuern-reglergroesse-y-rechts) - Steuern der Reglergroesse rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KOMPRESSOR_EINLAUFSCHUTZ](#job-steuern-kompressor-einlaufschutz) - Steuern des Kompressoreinlaufschutzes KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_MOTOREN_EICHLAUF](#job-steuern-motoren-eichlauf) - Motoren-Eichlauf aktivieren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_CAR_KEY_CODIERUNG](#job-steuern-car-key-codierung) - Umschalten der Funktionen - High-Sensity-Programm (Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb) - Low-Sensity-Programm (Belueftungsorientiertes Klappenprogramm) - Temperaturoffset - Geblaeseoffset zwischen CAR-Memory und KEY-Memory DEFAULT-Einstellung: Alle Funktionen sind CAR-Memory
- [STEUERN_OFF_MEMORY_CODIERUNG](#job-steuern-off-memory-codierung) - Aktivieren, deaktivieren der schluesselbezogenen OFF-Memoryeinstellungen
- [STEUERN_UMLUFT_MEMORY_CODIERUNG](#job-steuern-umluft-memory-codierung) - Aktivieren, deaktivieren der Umluftmemoryeinstellung
- [STEUERN_MMI_FUNKTIONEN](#job-steuern-mmi-funktionen) - Einstellen der Funktionen - High-Sensity-Programm (Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb) - Low-Sensity-Programm (Belueftungsorientiertes Klappenprogramm) - Temperaturoffset - Geblaeseoffset zwischen CAR-Memory und KEY-Memory DEFAULT-Einstellung: Alle Funktionen ausgeschaltet
- [STATUS_FUNKSCHLUESSEL_LESEN](#job-status-funkschluessel-lesen) - Auslesen der Nummer des aktuell benutzten Funkschluessels
- [STATUS_CAR_KEY_EINSTELLUNGEN](#job-status-car-key-einstellungen) - Auslesen der fuer einen Funkschluessel eingestellten Werte - High-Sensity-Programm (Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb) - Low-Sensity-Programm (Belueftungsorientiertes Klappenprogramm) - Temperaturoffset - Geblaeseoffset
- [STATUS_CAR_KEY_CODIERUNG](#job-status-car-key-codierung) - Auslesen der Steuerbits fuer CAR/KEY-Umschaltung - High-Sensity-Programm (Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb) - Low-Sensity-Programm (Belueftungsorientiertes Klappenprogramm) - Temperaturoffset - Geblaeseoffset
- [STATUS_CAR_MEMORY_CODIERUNG](#job-status-car-memory-codierung) - Auslesen der aktuellen CAR-Memoryeinstellungen
- [STATUS_OFF_MEMORY_CODIERUNG](#job-status-off-memory-codierung) - Auslesen der aktuellen OFF-Memoryeinstellungen
- [CKM_RESET_WERKSEINSTELLUNG](#job-ckm-reset-werkseinstellung) - Zuruecksetzen der KEY/CAR-Memoryeinstellungen auf Werkseinstellungen
- [STATUS_VERBRAUCHERREDUZIERUNG](#job-status-verbraucherreduzierung) - Auslesen der Status Stundenzaehler Verbraucherreduzierung KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_BS_DRUCKSENSOR](#job-status-bs-drucksensor) - Auslesen der Status Betriebsstunden Drucksensor KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_TINNEN_LUEFTER](#job-status-tinnen-luefter) - Auslesen der Status Innentemperatursensor Luefter KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_DRUCKSENSOR_MAX](#job-status-drucksensor-max) - Auslesen der Status Drucksensor Max-Druck KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STEUERN_ZAEHLER_VERBRAUCHERREDUZIERUNG_LOESCHEN](#job-steuern-zaehler-verbraucherreduzierung-loeschen) - Zaehler fuer Verbraucherreduzierung loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_BS_DRUCKSENSOR_LOESCHEN](#job-steuern-bs-drucksensor-loeschen) - Zaehler fuer Drucksensor loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_TINNEN_LUEFTER_LOESCHEN](#job-steuern-tinnen-luefter-loeschen) - Zaehler fuer Innenfuehlerluefter loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_DRUCKSENSOR_MAX_LOESCHEN](#job-steuern-drucksensor-max-loeschen) - Zaehler fuer max. Drucksensorwert loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_BEDIENTEIL_TASTEN](#job-steuern-bedienteil-tasten) - Simulieren von Tastenbetaetigungen am Bedienteil KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [TASTENSTATUS_LESEN](#job-tastenstatus-lesen) - Auslesen der aktuellen Tastenstellungen
- [KALIBRIERSTATUS_LESEN](#job-kalibrierstatus-lesen) - Auslesen des Kalibrierstatus In jedem Halbbyte des Kalibrierstatus steht die Anzahl der insgesamt durchgefuehrten Kalibrierungen fuer jede Seite. Die Anzahl muss immer gleich sein, da ansonsten eine Kalibrierung fuer die Max-, oder Minanschlaege fehlt. Der Kalibrierstatus wird beim Nachflashen der Software auf Null zurueckgesetzt.
- [POTIANSCHLAEGE_LESEN](#job-potianschlaege-lesen) - Auslesen der aktuellen Anschlagswerte der Potentiometer
- [STEUERN_BEDIENTEIL_POTIS](#job-steuern-bedienteil-potis) - Simulieren von Verstellungen der Potentiometer am Bedienteil KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [SG_VARIANTE_LESEN](#job-sg-variante-lesen) - Auslesen der Steuergeraetevariante BASIS- oder HIGH-Ausfuehrung
- [STEUERN_SELBSTTEST_SCHRITTMOTORE](#job-steuern-selbsttest-schrittmotore) - Alle Stellmotore auf 50 %verfahren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STATUS_SELBSTTEST_SCHRITTMOTORE](#job-status-selbsttest-schrittmotore) - Prüfen Selbsttest der Schrittmotoren KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [VERDAMPF_MIN_ANHEBUNG](#job-verdampf-min-anhebung) - Auslesen der SW-Nummer Dann EEPROM-Kennlinie Verdampfersollwert anheben und Verdampfersoll min mit Standard jobs EEPROM-schreiben Modus  : Default
- [STATUS_VERDAMPF_MIN_ANHEBUNG](#job-status-verdampf-min-anhebung) - Auslesen der SW-Nummer Dann EEPROM-Kennlinie Verdampfersollwert vergleichen und Verdampfersoll min mit Standard jobs EEPROM-schreiben Modus  : Default

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
| ID_HW_NR | string | BMW-Hardwarenummer |
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
| ID_SG_ADR | long | Steuergeraeteadresse |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-blocklaenge-lesen"></a>
### FLASH_BLOCKLAENGE_LESEN

Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_BLOCKLAENGE_GESAMT | int | Flash Blocklaenge inclusive SID |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge |
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
| AUTHENTISIERUNG | string | Authentisierungsart 'Keine'        Keine Authentisierung 'Simple'       Einfache Authentisierung 'Symetrisch'   Symetrische Authentisierung 'Asymetrisch'  Asymetrische Authentisierung |
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
| FLASH_SCHREIBEN_ANZAHL | int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
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
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG AIF schreiben |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG AIF schreiben |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

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

CBS Daten auslesen (fuer CBS Version 1-3) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Hex-String |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| ANZ_CBS | int | Anzahl der CBS - Umfaenge im Steuergerät |
| ID_FN_BOS_MESS_WERT | int | CBS-Kennung als Zahl |
| ID_FN_BOS_MESS_HEX | string | CBS-Kennung als Hex-String |
| ID_FN_BOS_MESS_TEXT | string | table CbsKennung CBS_K CBS_K_TEXT CBS-Kennung im Klartext |
| RMMI_BOS_WERT | int | Restlaufleistung |
| RMMI_BOS_EINH | string | Information zur Restlaufleistung |
| ST_UN_BOS_WERT | int | Einheit Restlaufleistung als Zahl |
| ST_UN_BOS_HEX | string | Einheit Restlaufleistung als Hex-String |
| ST_UN_BOS_TEXT | string | Einheit Restlaufleistung im Klartext |
| COU_RSTG_BOS_MESS_WERT | int | Servicezaehler |
| COU_RSTG_BOS_MESS_EINH | string | Zaehler |
| AVAI_BOS_WERT | int | Verfügbarkeit in % |
| AVAI_BOS_EINH | string | % |
| AVAI_BOS_WERT_OEL | int | Verfügbarkeit OEL in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_CSF | int | Verfügbarkeit CSF in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_BATT | int | Verfügbarkeit BATT in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_VTG | int | Verfügbarkeit VTG in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_FILT | int | Verfügbarkeit FILT in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_BR_V | int | Verfügbarkeit BR_V in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_BR_H | int | Verfügbarkeit BR_H in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_BRFL | int | Verfügbarkeit BRFL in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_ZKRZ | int | Verfügbarkeit ZKRZ in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_SIC | int | Verfügbarkeit SIC in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_KFL | int | Verfügbarkeit KFL in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_UEB | int | Verfügbarkeit UEB in %, für Prüfablauf Bandende |
| ZIEL_MM_WERT | int | Ziel-Monat (HU/AU) |
| ZIEL_MM_EINH | string | Monat |
| ZIEL_YY_WERT | int | Ziel-Jahr (HU/AU) |
| ZIEL_YY_EINH | string | Jahr |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbs-reset"></a>
### CBS_RESET

CBS Daten Zuruecksetzen (fuer CBS Version 1-3) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BOS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, ZKrz, Sic, Kfl, TUV, AU, Ueb Werte externe Umfaenge: Oel, Br_v, Br_h, Filt, CSF, Batt, VTG Defaultwert: 0x00 (ungueltig) |
| BOS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, kein Rueckstellen: 255 Defaultwert: 100 |
| BOS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, keine Aenderung: 31 Defaultwert: 31 |
| BOS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter fuer Monat, keine Aenderung: 255 Defaultwert: 255 |
| BOS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter fuer Jahr, keine Aenderung: 255 Defaultwert: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analogeingaenge"></a>
### STATUS_ANALOGEINGAENGE

Auslesen der 30 A/D-Werte (High), bzw. 16 A/D-Werte (Basis) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_POTI_TEMP_RE_WERT | real | Poti Temperatur rechts |
| STAT_POTI_TEMP_RE_EINH | string | Grad Celsius |
| STAT_POTI_TEMP_WERT | real | Poti Temperatur Basis |
| STAT_POTI_TEMP_EINH | string | Volt |
| STAT_POTI_GEBL_WERT | int | Poti Geblaese |
| STAT_POTI_GEBL_EINH | string | Incremente |
| STAT_POTI_TEMP_LI_WERT | real | Poti Temperatur links |
| STAT_POTI_TEMP_LI_EINH | string | Grad Celsius |
| STAT_POTI_KLAPPEN_WERT | real | Poti Luftverteilung |
| STAT_POTI_KLAPPEN_EINH | string | Incremente |
| STAT_TINNEN_WERT | real | Innentemperaturfuehler |
| STAT_TINNEN_EINH | string | Grad Celsius |
| STAT_TEMP_VERDAMFER_WERT | real | Verdampfertemperaturfuehler |
| STAT_TEMP_VERDAMFER_EINH | string | Grad Celsius |
| STAT_DRUCK_UB_WERT | real | Versorgungsspannung Drucksensor |
| STAT_DRUCK_UB_EINH | string | Volt |
| STAT_DRUCKSENSOR_WERT | real | Drucksensor |
| STAT_DRUCKSENSOR_EINH | string | bar |
| STAT_MONI_HHS_RELAIS_WERT | int | Monitor Heizbare Heckscheibe |
| STAT_MONI_HHS_RELAIS_EINH | string | Volt |
| STAT_WT_LI_WERT | real | Waermetauscherfuehler links |
| STAT_WT_LI_EINH | string | Grad Celsius |
| STAT_MONI_WV_LI_WERT | int | Diagnose Wasserventil links |
| STAT_MONI_WV_LI_EINH | string | Volt |
| STAT_KMV_STROM_WERT | real | Stromsignal KMV |
| STAT_KMV_STROM_EINH | string | mA |
| STAT_MONI_SDH_WERT | int | Diagnose-Eingang Spritzduesenheizung |
| STAT_MONI_SDH_EINH | string | Volt |
| STAT_TREIBER_UB_WERT | real | Stromsense Treiberversorgung |
| STAT_TREIBER_UB_EINH | string | Volt |
| STAT_OPEN_LOAD_UB_SENSE_WERT | real | Stromsense Treiberversorgung |
| STAT_OPEN_LOAD_UB_SENSE_EINH | string | Volt |
| STAT_WT_RE_WERT | real | Waermetauscherfuehler rechts |
| STAT_WT_RE_EINH | string | Grad Celsius |
| STAT_BELUEFTUNG_WERT | real | Belueftungstemperatur |
| STAT_BELUEFTUNG_EINH | string | Grad Celsius |
| STAT_FONDRAUM_WERT | int | Fondraumpoti |
| STAT_FONDRAUM_EINH | string | Volt |
| STAT_SOLARSENSOR_LI_WERT | real | Solarsensor links |
| STAT_SOLARSENSOR_LI_EINH | string | W/m2 |
| STAT_SOLARSENSOR_RE_WERT | real | Solarsensor |
| STAT_SOLARSENSOR_RE_EINH | string | W/m2 |
| STAT_MONI_AUC_UB_WERT | real | Monitor AUC-Versorgung |
| STAT_MONI_AUC_UB_EINH | string | Volt |
| STAT_MONI_SOLAR_UB_WERT | real | Monitor Sonnensensor-Versorgung |
| STAT_MONI_SOLAR_UB_EINH | string | Volt |
| STAT_FONDRAUM_VERSORGUNG_WERT | real | Spannungsversorgung Fondraumpoti |
| STAT_FONDRAUM_VERSORGUNG_EINH | string | Volt |
| STAT_BESCHLAGSENSOR_UB_WERT | real | Spannungsversorgung Beschlagsensor |
| STAT_BESCHLAGSENSOR_UB_EINH | string | Volt |
| STAT_MONI_WV_RE_WERT | int | Diagnose Wasserventil rechts |
| STAT_MONI_WV_RE_EINH | string | Inkremente |
| STAT_WP_SENSE_WERT | int | Stromsense Wasserpumpe |
| STAT_WP_SENSE_EINH | string | Inkremente |
| STAT_WT_WERT | real | Waermetauscherfuehler Basis-Variante |
| STAT_WT_EINH | string | Grad Celsius |
| STAT_MONI_WV_WERT | int | Diagnose Wasserventil Basis-Variante |
| STAT_MONI_WV_EINH | string | Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digitaleingaenge"></a>
### STATUS_DIGITALEINGAENGE

Auslesen der Digitalen-Eingänge (High) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BESCHLAGSENSOR_WERT | real | Beschlagsensorfrequenz |
| STAT_BESCHLAGSENSOR_EINH | string | Hz |
| STAT_AUC_PWM_WERT | real | Auc-Sensor |
| STAT_AUC_PWM_EINH | string | % |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-reglergroessen"></a>
### STATUS_REGLERGROESSEN

Auslesen der 28 Byte Reglerinformationene KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SOLL_LI_WERT | real |  |
| STAT_SOLL_LI_EINH | string | Grad Celsius |
| STAT_SOLL_RE_WERT | real |  |
| STAT_SOLL_RE_EINH | string | Grad Celsius |
| STAT_SOLL_BASIS_WERT | real |  |
| STAT_SOLL_BASIS_EINH | string | Grad Celsius |
| STAT_TINNEN_WERT | real |  |
| STAT_TINNEN_EINH | string | Grad Celsius |
| STAT_TINNEN_VERZOEGERT_WERT | real |  |
| STAT_TINNEN_VERZOEGERT_EINH | string | Grad Celsius |
| STAT_TAUSSEN_WERT | real |  |
| STAT_TAUSSEN_EINH | string | Grad Celsius |
| STAT_LUFTLEISTUNG_WERT | int | Luftleistung |
| STAT_LUFTLEISTUNG_EINH | string | % |
| STAT_WT_LI_WERT | real |  |
| STAT_WT_LI_EINH | string | Grad Celsius |
| STAT_WT_RE_WERT | real |  |
| STAT_WT_RE_EINH | string | Grad Celsius |
| STAT_SOLL_LI_KORRIGIERT_WERT | real |  |
| STAT_SOLL_LI_KORRIGIERT_EINH | string | Grad Celsius |
| STAT_SOLL_RE_KORRIGIERT_WERT | real |  |
| STAT_SOLL_RE_KORRIGIERT_EINH | string | Grad Celsius |
| STAT_WTSOLL_LI_WERT | real |  |
| STAT_WTSOLL_LI_EINH | string | Grad Celsius |
| STAT_WTSOLL_RE_WERT | real |  |
| STAT_WTSOLL_RE_EINH | string | Grad Celsius |
| STAT_DIFFSOLL_WERT | real |  |
| STAT_DIFFSOLL_EINH | string | Grad Celsius |
| STAT_DIFFSOLL_VERZOEGERT_WERT | real |  |
| STAT_DIFFSOLL_VERZOEGERT_EINH | string | Grad Celsius |
| STAT_YWT_LI_WERT | int |  |
| STAT_YWT_LI_EINH | string | % |
| STAT_YWT_RE_WERT | int |  |
| STAT_YWT_RE_EINH | string | % |
| STAT_FUEHR_LI_WERT | real |  |
| STAT_FUEHR_LI_EINH | string | % |
| STAT_FUEHR_RE_WERT | real |  |
| STAT_FUEHR_RE_EINH | string | % |
| STAT_DREHZAHL_WERT | int |  |
| STAT_DREHZAHL_EINH | string | 1/min |
| STAT_SPEED_WERT | int |  |
| STAT_SPEED_EINH | string | km/h |
| STAT_Y_LI_WERT | int |  |
| STAT_Y_LI_EINH | string | % |
| STAT_Y_RE_WERT | int |  |
| STAT_Y_RE_EINH | string | % |
| STAT_WVOEFFNZEIT_LI_WERT | int |  |
| STAT_WVOEFFNZEIT_LI_EINH | string | ms |
| STAT_WVOEFFNZEIT_RE_WERT | int |  |
| STAT_WVOEFFNZEIT_RE_EINH | string | ms |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bedienteil"></a>
### STATUS_BEDIENTEIL

Auslesen der Bedienteileinstellungen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table Job Result STATUS_TEXT |
| STAT_POTI_TEMP_LI_WERT | real | Nur bei HIGH-Ausfuehrung |
| STAT_POTI_TEMP_LI_EINH | string | Grad Celsius Nur bei HIGH-Ausfuehrung |
| STAT_POTI_KLAPPEN_WERT | real | Nur bei BASIS-Ausfuehrung |
| STAT_POTI_KLAPPEN_EINH | string | % Nur bei BASIS-Ausfuehrung |
| STAT_POTI_TEMP_RE_WERT | real |  |
| STAT_POTI_TEMP_RE_EINH | string | Grad Celsius |
| STAT_POTI_GEBLAESE_WERT | int |  |
| STAT_POTI_GEBLAESE_EINH | string | % |
| STAT_KLEMME_58G_WERT | int |  |
| STAT_KLEMME_58G_EINH | string | % |
| STAT_FUNKTION_OFF_EIN | int |  |
| STAT_FUNKTION_DEFROST_EIN | int |  |
| STAT_FUNKTION_MAX_AC_EIN | int |  |
| STAT_FUNKTION_AUC_EIN | int |  |
| STAT_FUNKTION_UMLUFT_EIN | int |  |
| STAT_FUNKTION_HHS_EIN | int |  |
| STAT_FUNKTION_REST_EIN | int |  |
| STAT_FUNKTION_AC_EIN | int |  |
| STAT_KLAPPEN_AUTO_LI_EIN | int |  |
| STAT_KLAPPEN_AUTO_RE_EIN | int |  |
| STAT_KLAPPEN_AUTO_EIN | int |  |
| STAT_GEBLAESE_AUTO_EIN | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-io"></a>
### STATUS_IO

Auslesen der Ansteuer-Ports für externe Lasten KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HHS_EIN | int |  |
| STAT_ZUSATZWASSERPUMPE_EIN | int |  |
| STAT_SPRITZDUESENHEIZUNG_EIN | int |  |
| STAT_WASSERVENTIL_LI_EIN | int |  |
| STAT_WASSERVENTIL_RE_EIN | int |  |
| STAT_WASSERVENTIL_EIN | int |  |
| STAT_INNENFUEHLER_GEBLAESE_EIN | int |  |
| STAT_TREIBERVERSORGUNG_BUSSE_EIN | int |  |
| STAT_PULLUP_TREIBERVERSORGUNG_EIN | int |  |
| STAT_TASTE_HSH_EIN | int |  |
| STAT_TASTE_AC_EIN | int |  |
| STAT_TASTE_AUTO_EIN | int |  |
| STAT_TASTE_UML_EIN | int |  |
| STAT_TASTE_OFF_EIN | int |  |
| STAT_ANSTEUERUNG_KMV_WERT | int | Ansteuerung KMV-PWM |
| STAT_ANSTEUERUNG_KMV_EINH | string | % |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-klappenposition"></a>
### STATUS_MOTOR_KLAPPENPOSITION

Auslesen der 9 Klappenpositionen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOTOR_EINH | string | % alle Motoreinheiten |
| STAT_FRISCHLUFT_UMLUFT_LI_WERT | int |  |
| STAT_FRISCHLUFT_UMLUFT_RE_WERT | int |  |
| STAT_DEFROST_WERT | int |  |
| STAT_BELUEFTUNG_LI_WERT | int |  |
| STAT_BELUEFTUNG_RE_WERT | int |  |
| STAT_BELUEFTUNG_WERT | int |  |
| STAT_KALTLUFT_WERT | int |  |
| STAT_FUSSRAUM_LI_WERT | int |  |
| STAT_FUSSRAUM_RE_WERT | int |  |
| STAT_FUSSRAUM_WERT | int |  |
| STAT_FOND_WERT | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fze"></a>
### STATUS_FZE

Auslesen der Stati der Filterzustandserkennung(FZE) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GESAMT_BELADUNG_WERT | long | gesamte gewichtete Beladungszeit seit dem letztem Filterwechsel (Reset) 0 bis 83886074 Sekunden (83886075 = ungültig) |
| STAT_GESAMT_BELADUNG_EINH | string | Sekunden |
| STAT_GESAMT_FRISCHLUFT_WERT | long | gesamte Frischluftzeit seit dem letztem Filterwechsel (Reset) 0 bis 83886074 Sekunden (83886075 = ungültig) |
| STAT_GESAMT_FRISCHLUFT_EINH | string | Sekunden |
| STAT_GESAMT_MISCHLUFT_WERT | long | gesamte Mischluftzeit seit dem letztem Filterwechsel (Reset) 0 bis 83886074 Sekunden (83886075 = ungültig) |
| STAT_GESAMT_MISCHLUFT_EINH | string | Sekunden |
| STAT_GESAMT_UMLUFT_WERT | long | gesamte Umluftzeit seit dem letztem Filterwechsel (Reset) 0 bis 83886074 Sekunden (83886075 = ungültig) |
| STAT_GESAMT_UMLUFT_EINH | string | Sekunden |
| STAT_BELADUNGSGESCHWINDIGKEIT_FAST_WERT | real | gemittelte Beladungsgeschwindigkeit über 50h reiner Betriebszeit 0 bis 200 Kilometer / gemittelte Beladungsstunde |
| STAT_BELADUNGSGESCHWINDIGKEIT_FAST_EINH | string | km |
| STAT_BELADUNGSGESCHWINDIGKEIT_SLOW_WERT | real | gemittelte Beladungsgeschwindigkeit über 500h reiner Betriebszeit 0 bis 200 Kilometer / gemittelte Beladungsstunde |
| STAT_BELADUNGSGESCHWINDIGKEIT_SLOW_EINH | string | km |
| STAT_KILOMETER_ZAEHLER_WECHSEL_WERT | long | Kilometerstand beim letzten Filterwechsel (Reset) 0 bis 16777200 Kilometer (00FFFFFF = ungültig) |
| STAT_KILOMETER_ZAEHLER_WECHSEL_EINH | string | km |
| STAT_KILOMETER_ZAEHLER_AKTUELL_WERT | long | Kilometerstand vor letzten Zündung aus (Aktuell) 0 bis 16777200 Kilometer (00FFFFFF = ungültig) |
| STAT_KILOMETER_ZAEHLER_AKTUELL_EINH | string | km |
| STAT_TAG_ZAEHLER_WECHSEL_WERT | int | Relativzeittageszähler beim letzten Filterwechsel (Reset) 0 bis 65534 Tage (FFFF = ungültig) |
| STAT_TAG_ZAEHLER_WECHSEL_EINH | string | Tage |
| STAT_TAG_ZAEHLER_AKTUELL_WERT | int | Relativzeittageszähler vor letzten Zündung aus (Aktuell) 0 bis 65534 Tage (FFFF = ungültig) |
| STAT_TAG_ZAEHLER_AKTUELL_EINH | string | Tage |
| STAT_SERVICE_ZAEHLER_WERT | char | Zähler für bishere durchgeführte Filterwechsel (Reset) 0 bis 30 (31 = ungültig) |
| STAT_SERVICE_ZAEHLER_EINH | string | Anzahl |
| STAT_VERFUEGBARKEIT_WERT | char | prozentuale Verfügbarkeit des Filters 0 bis 100 % (0xfe = ungültig) |
| STAT_VERFUEGBARKEIT_EINH | string | % |
| STAT_RESTKILOMETER_WERT | long | vorherberechnete Restlaufleistung des Filters -30000 bis 300000 km |
| STAT_RESTKILOMETER_EINH | string | km |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmode"></a>
### STATUS_ENERGIESPARMODE

Auslesen des aktuell eingestellten Energiesparmodes KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TRANSPORTMODE_WERT | int |  |
| STAT_WERKSTATTMODE_WERT | int |  |
| STAT_FERTIGUNGSMODE_WERT | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-steuerort-zwp"></a>
### STATUS_STEUERORT_ZWP

Auslesen des aktuell codierten Verbauort der ZWP KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VERBAUORT_IHKA_WERT | int |  |
| STAT_VERBAUORT_SH_WERT | int |  |
| STAT_VERBAUORT_DME_WERT | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ptc-verbaut"></a>
### STATUS_PTC_VERBAUT

Auslesen ob PTC verbaut KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PTC_VERBAUT_WERT | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zusatzluefter-stufe"></a>
### STATUS_ZUSATZLUEFTER_STUFE

Auslesen der Stufe des Zusatzluefters KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_STUFE_ZUSATZL_WERT | int |  |
| STAT_STUFE_ZUSATZL_EINH | string | Stufe |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-boot-sw-version"></a>
### STATUS_BOOT_SW_VERSION

Auslesen der Boot-SW-Version KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BOOT_SW_BYTE1_WERT | int |  |
| STAT_BOOT_SW_BYTE2_WERT | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-fehler"></a>
### STATUS_MOTOR_FEHLER

Auslesen der Lin-Motoren-Fehler KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANTWORT_FEHLT_WERT | int |  |
| STAT_INTERNER_FEHLER_WERT | int |  |
| STAT_BLOCKIERUNG_WERT | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-testbit"></a>
### DIAGNOSE_TESTBIT

Ansteuern des Diagnosetest-Bits Das Bit kann ein- bzw. ausgeschaltet werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTBIT | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-heckscheiben-heizung"></a>
### STEUERN_HECKSCHEIBEN_HEIZUNG

Ansteuern der Heckscheibenheizugng im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HECKSCHEIBE | string | 'EIN', 'AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wasserpumpe"></a>
### STEUERN_WASSERPUMPE

Ansteuern der Wasserpumpe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZUSATZWASSERPUMPE | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spritzduesen-heizung"></a>
### STEUERN_SPRITZDUESEN_HEIZUNG

Ansteuern der Spritzduesenheizung im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPRITZDUESEN_HEIZUNG | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wasserventil-links"></a>
### STEUERN_WASSERVENTIL_LINKS

Ansteuern des linken Wasserventils (BASIS) im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WASSERVENTIL_LINKS | int | Einschaltdauer in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wasserventil-rechts"></a>
### STEUERN_WASSERVENTIL_RECHTS

Ansteuern des rechten Wasserventils im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WASSERVENTIL_RECHTS | int | Einschaltdauer in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kaeltemittelverdichter"></a>
### STEUERN_KAELTEMITTELVERDICHTER

Ansteuern des Kaeltemittelverdichters im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KAELTEMITTELVERDICHTER | int | Ansteuerung KMV in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-geblaese"></a>
### STEUERN_GEBLAESE

Ansteuern des Geblaeses im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GEBLAESE | int | Geblaese-Ansteuerung in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zusatzluefter"></a>
### STEUERN_ZUSATZLUEFTER

Ansteuern des Zusatzluefters im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZUSATZLUEFTER | int | Zusatzluefter-Ansteuerung in Stufen 0-14 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-atemp"></a>
### STEUERN_ATEMP

Ansteuern der Aussentemperatur im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSSENTEMP | int | Aussentemperatur von -40°C - 85°C |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ptc-diag-ol-aus"></a>
### STEUERN_PTC_DIAG_OL_AUS

Fehlereintrag für Ptc bei Open Load verhindern KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ptc-werksprozess"></a>
### PTC_WERKSPROZESS

Ptc-Werksprozess KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BATTERIESPANNUNG_WERT | int |  |
| STAT_STROMVERBRAUCH_WERT | int |  |
| STAT_REGLERTEMPERATUR_WERT | int |  |
| STAT_BATTERIESPANNUNG_EINH | string | V |
| STAT_STROMVERBRAUCH_EINH | string | A |
| STAT_REGLERTEMPERATUR_EINH | string | °C |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-frischluft-umluft-links"></a>
### STEUERN_FRISCHLUFT_UMLUFT_LINKS

Ansteuern der Frischluft-/Umluftklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FRISCHLUFT_UMLUFT_LINKS | int | Klappenansteuerung KLAPPE_FRISCHLUFT_UMLUFT_LINKS in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-frischluft-umluft-rechts"></a>
### STEUERN_FRISCHLUFT_UMLUFT_RECHTS

Ansteuern der Frischluft/Umluftklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FRISCHLUFT_UMLUFT_RECHTS | int | Klappenansteuerung KLAPPE_FRISCHLUFT_UMLUFT_RECHTS in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-defrost"></a>
### STEUERN_KLAPPE_DEFROST

Ansteuern der Entfrostungsklappe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_DEFROST | int | Klappenansteuerung KLAPPE_DEFROST in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-belueftung-links"></a>
### STEUERN_KLAPPE_BELUEFTUNG_LINKS

Ansteuern der Belueftungsklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_BELUEFTUNG_LINKS | int | Klappenansteuerung KLAPPE_BELUEFTUNG_LINKS in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-belueftung-rechts"></a>
### STEUERN_KLAPPE_BELUEFTUNG_RECHTS

Ansteuern der Belueftungsklappe rechts (BASIS) im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_BELUEFTUNG_RECHTS | int | Klappenansteuerung KLAPPE_BELUEFTUNG_RECHTS in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-schichtung"></a>
### STEUERN_KLAPPE_SCHICHTUNG

Ansteuern der Schichtungsklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_SCHICHTUNG | int | Klappenansteuerung KLAPPE_SCHICHTUNG in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fussraum-links"></a>
### STEUERN_KLAPPE_FUSSRAUM_LINKS

Ansteuern der Fussraumklappe links (BASIS) im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FUSSRAUM_LINKS | int | Klappenansteuerung KLAPPE_FUSSRAUM_LINKS in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fussraum-rechts"></a>
### STEUERN_KLAPPE_FUSSRAUM_RECHTS

Ansteuern der Fussraumklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FUSSRAUM_RECHTS | int | Klappenansteuerung KLAPPE_FUSSRAUM_RECHTS in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fond"></a>
### STEUERN_KLAPPE_FOND

Ansteuern der Fondraumklappe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FOND | int | Klappenansteuerung KLAPPE_FOND in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ptc"></a>
### STEUERN_PTC

Ansteuern des PTC im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PTC | int | Ansteuerung PTC über Bitmaske von 0y00000000 bis 0y11111111 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-reglergroesse-y-links"></a>
### STEUERN_REGLERGROESSE_Y_LINKS

Steuern der Reglergroesse links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REGLERGROESSE_Y_LINKS | int | Reglergroesse Ylinks -200 - +311 in Prozent |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-reglergroesse-y-rechts"></a>
### STEUERN_REGLERGROESSE_Y_RECHTS

Steuern der Reglergroesse rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REGLERGROESSE_Y_RECHTS | int | Reglergroesse Yrechts -200 - +311 in Prozent |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kompressor-einlaufschutz"></a>
### STEUERN_KOMPRESSOR_EINLAUFSCHUTZ

Steuern des Kompressoreinlaufschutzes KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KOMPRESSOR_EINLAUFSCHUTZ | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motoren-eichlauf"></a>
### STEUERN_MOTOREN_EICHLAUF

Motoren-Eichlauf aktivieren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-car-key-codierung"></a>
### STEUERN_CAR_KEY_CODIERUNG

Umschalten der Funktionen - High-Sensity-Programm (Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb) - Low-Sensity-Programm (Belueftungsorientiertes Klappenprogramm) - Temperaturoffset - Geblaeseoffset zwischen CAR-Memory und KEY-Memory DEFAULT-Einstellung: Alle Funktionen sind CAR-Memory

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HIGH_SENSITY_PRG | string | Programm Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb 'ein' =&gt; Funktion ist KEY-Memory 'aus' =&gt; Funktion ist CAR-Memory |
| LOW_SENSITY_PRG | string | Belueftungsorientiertes Klappenprogramm 'ein' =&gt; Funktion ist KEY-Memory 'aus' =&gt; Funktion ist CAR-Memory |
| TEMPERATUROFFSET | string | Temperaturoffset 'ein' =&gt; Funktion ist KEY-Memory 'aus' =&gt; Funktion ist CAR-Memory |
| GEBLAESEOFFSET | string | Geblaeseoffset 'ein' =&gt; Funktion ist KEY-Memory 'aus' =&gt; Funktion ist CAR-Memory |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-off-memory-codierung"></a>
### STEUERN_OFF_MEMORY_CODIERUNG

Aktivieren, deaktivieren der schluesselbezogenen OFF-Memoryeinstellungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHLUESSEL_1 | string | OFF-Memory fuer Schluessel 1 aktivieren/deaktivieren 'ein' =&gt; OFF-Memory aktivieren 'aus' =&gt; OFF-Memory deaktivieren |
| SCHLUESSEL_2 | string | OFF-Memory fuer Schluessel 2 aktivieren/deaktivieren 'ein' =&gt; OFF-Memory aktivieren 'aus' =&gt; OFF-Memory deaktivieren |
| SCHLUESSEL_3 | string | OFF-Memory fuer Schluessel 3 aktivieren/deaktivieren 'ein' =&gt; OFF-Memory aktivieren 'aus' =&gt; OFF-Memory deaktivieren |
| SCHLUESSEL_4 | string | OFF-Memory fuer Schluessel 4 aktivieren/deaktivieren 'ein' =&gt; OFF-Memory aktivieren 'aus' =&gt; OFF-Memory deaktivieren |
| SCHLUESSEL_DEF | string | OFF-Memory fuer Defaultschluessel aktivieren/deaktivieren 'ein' =&gt; OFF-Memory aktivieren 'aus' =&gt; OFF-Memory deaktivieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-umluft-memory-codierung"></a>
### STEUERN_UMLUFT_MEMORY_CODIERUNG

Aktivieren, deaktivieren der Umluftmemoryeinstellung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_UMLUFT_MEMO | string | UMLUFT-Memory aktivieren/deaktivieren 'ein' =&gt; UMLUFT-Memory aktivieren 'aus' =&gt; UMLUFT-Memory deaktivieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-mmi-funktionen"></a>
### STEUERN_MMI_FUNKTIONEN

Einstellen der Funktionen - High-Sensity-Programm (Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb) - Low-Sensity-Programm (Belueftungsorientiertes Klappenprogramm) - Temperaturoffset - Geblaeseoffset zwischen CAR-Memory und KEY-Memory DEFAULT-Einstellung: Alle Funktionen ausgeschaltet

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HIGH_SENSITY_PRG | string | Programm Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb 'ein' =&gt; Funktion einschalten 'aus' =&gt; Funktion ausschalten |
| LOW_SENSITY_PRG | string | Belueftungsorientiertes Klappenprogramm 'ein' =&gt; Funktion einschalten 'aus' =&gt; Funktion ausschalten |
| TEMPERATUROFFSET | string | Temperaturoffset -3K bis +3K (Default 0K) |
| GEBLAESEOFFSET | string | Geblaeseoffset -10%, 0% oder +10% (Default 0%) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-funkschluessel-lesen"></a>
### STATUS_FUNKSCHLUESSEL_LESEN

Auslesen der Nummer des aktuell benutzten Funkschluessels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NUMMER_FUNKSCHLUESSEL | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-car-key-einstellungen"></a>
### STATUS_CAR_KEY_EINSTELLUNGEN

Auslesen der fuer einen Funkschluessel eingestellten Werte - High-Sensity-Programm (Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb) - Low-Sensity-Programm (Belueftungsorientiertes Klappenprogramm) - Temperaturoffset - Geblaeseoffset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIGH_SENSITY_PRG | string | Programm Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb |
| STAT_LOW_SENSITY_PRG | string | Belueftungsorientiertes Klappenprogramm |
| STAT_KEY_NR | string |  |
| STAT_TEMP_OFFSET_KELVIN | string | Temperaturoffset -3K bis +3K (Default 0K) |
| STAT_GEBL_OFFSET_PROZENT | string | Geblaeseoffset -10%, 0% oder +10% (Default 0%) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-car-key-codierung"></a>
### STATUS_CAR_KEY_CODIERUNG

Auslesen der Steuerbits fuer CAR/KEY-Umschaltung - High-Sensity-Programm (Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb) - Low-Sensity-Programm (Belueftungsorientiertes Klappenprogramm) - Temperaturoffset - Geblaeseoffset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIGH_SENSITY_PRG | string | Programm Defrostklappe und Fussraumklappe ZU im Kuehlbetrieb |
| STAT_LOW_SENSITY_PRG | string | Belueftungsorientiertes Klappenprogramm |
| STAT_TEMPERATUROFFSET | string |  |
| STAT_GEBLAESEOFFSET | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-car-memory-codierung"></a>
### STATUS_CAR_MEMORY_CODIERUNG

Auslesen der aktuellen CAR-Memoryeinstellungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_UMLUFT_MEMORY | string | Umluftfunktion speichern bei Abschaltung |
| STAT_SCHICHTUNGS_RESET | string | Schichtung auf 50% bei Betaetigung AUTO-Taste |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-off-memory-codierung"></a>
### STATUS_OFF_MEMORY_CODIERUNG

Auslesen der aktuellen OFF-Memoryeinstellungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFF_MEMORY_SCHLUESSEL_1 | string | OFF-Funktion fuer Schluessel 1 speichern bei Abschaltung |
| STAT_OFF_MEMORY_SCHLUESSEL_2 | string | OFF-Funktion fuer Schluessel 2 speichern bei Abschaltung |
| STAT_OFF_MEMORY_SCHLUESSEL_3 | string | OFF-Funktion fuer Schluessel 3 speichern bei Abschaltung |
| STAT_OFF_MEMORY_SCHLUESSEL_4 | string | OFF-Funktion fuer Schluessel 44 speichern bei Abschaltung |
| STAT_OFF_MEMORY_SCHLUESSEL_DEF | string | OFF-Funktion fuer Defaultschluessel speichern bei Abschaltung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ckm-reset-werkseinstellung"></a>
### CKM_RESET_WERKSEINSTELLUNG

Zuruecksetzen der KEY/CAR-Memoryeinstellungen auf Werkseinstellungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-verbraucherreduzierung"></a>
### STATUS_VERBRAUCHERREDUZIERUNG

Auslesen der Status Stundenzaehler Verbraucherreduzierung KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZAEHLER_HHS_TAKTUNG_WERT | unsigned long |  |
| STAT_ZAEHLER_HHS_TAKTUNG_EINH | string | min |
| STAT_ZAEHLER_HHS_AUS_WERT | unsigned long |  |
| STAT_ZAEHLER_HHS_AUS_EINH | string | min |
| STAT_ZAEHLER_GEBL_75_PROZ_WERT | unsigned long |  |
| STAT_ZAEHLER_GEBL_75_PROZ_EINH | string | min |
| STAT_ZAEHLER_GEBL_50_PROZ_WERT | unsigned long |  |
| STAT_ZAEHLER_GEBL_50_PROZ_EINH | string | min |
| STAT_ZAEHLER_GEBL_AUS_WERT | unsigned long |  |
| STAT_ZAEHLER_GEBL_AUS_EINH | string | min |
| STAT_ZAEHLER_SH_AUS_BEI_KL15_WERT | unsigned long |  |
| STAT_ZAEHLER_SH_AUS_BEI_KL15_EINH | string | min |
| STAT_ZAEHLER_STANDVERBRAUCHER_WERT | unsigned long |  |
| STAT_ZAEHLER_STANDVERBRAUCHER_EINH | string | min |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bs-drucksensor"></a>
### STATUS_BS_DRUCKSENSOR

Auslesen der Status Betriebsstunden Drucksensor KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BS_DRUCKSENSOR_BEREICH_A_WERT | unsigned long |  |
| STAT_BS_DRUCKSENSOR_BEREICH_A_EINH | string | min |
| STAT_BS_DRUCKSENSOR_BEREICH_B_WERT | unsigned long |  |
| STAT_BS_DRUCKSENSOR_BEREICH_B_EINH | string | min |
| STAT_BS_DRUCKSENSOR_BEREICH_C_WERT | unsigned long |  |
| STAT_BS_DRUCKSENSOR_BEREICH_C_EINH | string | min |
| STAT_BS_DRUCKSENSOR_BEREICH_D_WERT | unsigned long |  |
| STAT_BS_DRUCKSENSOR_BEREICH_D_EINH | string | min |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tinnen-luefter"></a>
### STATUS_TINNEN_LUEFTER

Auslesen der Status Innentemperatursensor Luefter KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_IFG_MIN_DREHZAHL_WERT | unsigned long |  |
| STAT_IFG_MIN_DREHZAHL_EINH | string | U/min |
| STAT_IFG_MIN_TEMP_AUSSEN_WERT | real |  |
| STAT_IFG_MIN_TEMP_AUSSEN_EINH | string | °C |
| STAT_IFG_MIN_U_BATTERIE_WERT | real |  |
| STAT_IFG_MIN_U_BATTERIE_EINH | string | Volt |
| STAT_IFG_MIN_TEMP_INNEN_WERT | real |  |
| STAT_IFG_MIN_TEMP_INNEN_EINH | string | °C |
| STAT_IFG_MAX_DREHZAHL_WERT | unsigned long |  |
| STAT_IFG_MAX_DREHZAHL_EINH | string | U/min |
| STAT_IFG_MAX_TEMP_AUSSEN_WERT | real |  |
| STAT_IFG_MAX_TEMP_AUSSEN_EINH | string | °C |
| STAT_IFG_MAX_U_BATTERIE_WERT | real |  |
| STAT_IFG_MAX_U_BATTERIE_EINH | string | Volt |
| STAT_IFG_MAX_TEMP_INNEN_WERT | real |  |
| STAT_IFG_MAX_TEMP_INNEN_EINH | string | °C |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drucksensor-max"></a>
### STATUS_DRUCKSENSOR_MAX

Auslesen der Status Drucksensor Max-Druck KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DRUCKSENSOR_MAX_DRUCK_WERT | unsigned long |  |
| STAT_DRUCKSENSOR_MAX_DRUCK_EINH | string | bar |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zaehler-verbraucherreduzierung-loeschen"></a>
### STEUERN_ZAEHLER_VERBRAUCHERREDUZIERUNG_LOESCHEN

Zaehler fuer Verbraucherreduzierung loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bs-drucksensor-loeschen"></a>
### STEUERN_BS_DRUCKSENSOR_LOESCHEN

Zaehler fuer Drucksensor loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tinnen-luefter-loeschen"></a>
### STEUERN_TINNEN_LUEFTER_LOESCHEN

Zaehler fuer Innenfuehlerluefter loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-drucksensor-max-loeschen"></a>
### STEUERN_DRUCKSENSOR_MAX_LOESCHEN

Zaehler fuer max. Drucksensorwert loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bedienteil-tasten"></a>
### STEUERN_BEDIENTEIL_TASTEN

Simulieren von Tastenbetaetigungen am Bedienteil KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTEN_NUMMER | int | HIGH-BEDIENTEIL: Tastennummern im Bereich von 0 bis 7 zulaessig 0 = KLIMA,     1 = HHS,      2 = MAX_AC, 3 = OFF 4 = DEFROST,   5 = UML/AUC,  6 = REST,   7 = AUTO Bei MAX-AC muß Aussentemperatur groesser Schwelle sein Bei Restwaerme muss bei Klemme 15 EIN-&gt;AUS die Aussentemperatur kleiner Schwelle und die Motortemperatur groesser Schwelle sein  BASIS-BEDIENTEIL: Tastennummern 0, 1, 3, 5 und 7 zulaessig 0 = KLIMA,  1 = HHS,  3 = OFF,  5 = UMLUFT,  7 = AUTO |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-tastenstatus-lesen"></a>
### TASTENSTATUS_LESEN

Auslesen der aktuellen Tastenstellungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TASTEN_STATUS | int | Nummer der betaetigten Taste |
| TASTEN_STATUS_TEXT | string | Betaetigte Taste im Klartext |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-kalibrierstatus-lesen"></a>
### KALIBRIERSTATUS_LESEN

Auslesen des Kalibrierstatus In jedem Halbbyte des Kalibrierstatus steht die Anzahl der insgesamt durchgefuehrten Kalibrierungen fuer jede Seite. Die Anzahl muss immer gleich sein, da ansonsten eine Kalibrierung fuer die Max-, oder Minanschlaege fehlt. Der Kalibrierstatus wird beim Nachflashen der Software auf Null zurueckgesetzt.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| KALIBRIER_STATUS_LINKS | int |  |
| KALIBRIER_STATUS_RECHTS | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-potianschlaege-lesen"></a>
### POTIANSCHLAEGE_LESEN

Auslesen der aktuellen Anschlagswerte der Potentiometer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| POTI_LINKS_MIN_ANSCHLAG | int |  |
| POTI_LINKS_MAX_ANSCHLAG | int |  |
| POTI_MITTE_MIN_ANSCHLAG | int |  |
| POTI_MITTE_MAX_ANSCHLAG | int |  |
| POTI_RECHTS_MIN_ANSCHLAG | int |  |
| POTI_RECHTS_MAX_ANSCHLAG | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-bedienteil-potis"></a>
### STEUERN_BEDIENTEIL_POTIS

Simulieren von Verstellungen der Potentiometer am Bedienteil KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POTENTIOMETER_LINKS | int | HIGH-BEDIENTEIL: Temperatureinstellung linke Seite Temperatur in Grad Celsius * 2 Gueltige Werte 34 - 54 (entspricht 17 - 27 Grad Celsius in Halbgradschritten)  BASIS-BEDIENTEIL: Verstellung Klappenpotentiometer Klappenverstellung in Anzahl mechanische Rasten Gueltige Werte -18 bis +18 Werte kleiner Null -&gt; links drehen, groesser Null -&gt; rechts drehen, Null -&gt; keine Verstellung |
| POTENTIOMETER_MITTE | int | HIGH-BEDIENTEIL: Verstellung Geblaesestufe Geblaeseverstellung in Anzahl mechanische Rasten Gueltige Werte -9 bis +9 Werte kleiner Null -&gt; links drehen, groesser Null -&gt; rechts drehen, Null -&gt; keine Verstellung  BASIS-BEDIENTEIL: Raststellung Geblaesesteller Geblaeseeinstellung in Stufen Gueltige Werte Raste 1 - 25 (entspricht 0 bis 100 Prozent) |
| POTENTIOMETER_RECHTS | int | HIGH-BEDIENTEIL: Temperatureinstellung rechte Seite Temperatur in Grad Celsius * 2 Gueltige Werte 34 - 54 (entspricht 17 - 27 Grad Celsius in Halbgradschritten)  BASIS-BEDIENTEIL: Temperatureinstellung Temperatur in Grad Celsius * 2 Gueltige Werte 30 - 58 (entspricht 15 - 29 Grad Celsius in Halbgradschritten) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sg-variante-lesen"></a>
### SG_VARIANTE_LESEN

Auslesen der Steuergeraetevariante BASIS- oder HIGH-Ausfuehrung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SG_VARIANTE | int | 0 = BASIS, 1 = HIGH |
| SG_VARIANTE_TEXT | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-selbsttest-schrittmotore"></a>
### STEUERN_SELBSTTEST_SCHRITTMOTORE

Alle Stellmotore auf 50 %verfahren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-selbsttest-schrittmotore"></a>
### STATUS_SELBSTTEST_SCHRITTMOTORE

Prüfen Selbsttest der Schrittmotoren KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SELBSTTEST_SCHRITTMOTORE_WERT | int | Status des Schrittmotorenselbsttests 0 = Test nicht erfolgreich 1 = Test erfolgreich |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-verdampf-min-anhebung"></a>
### VERDAMPF_MIN_ANHEBUNG

Auslesen der SW-Nummer Dann EEPROM-Kennlinie Verdampfersollwert anheben und Verdampfersoll min mit Standard jobs EEPROM-schreiben Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STATUS_TEXT | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-verdampf-min-anhebung"></a>
### STATUS_VERDAMPF_MIN_ANHEBUNG

Auslesen der SW-Nummer Dann EEPROM-Kennlinie Verdampfersollwert vergleichen und Verdampfersoll min mit Standard jobs EEPROM-schreiben Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERDAMPFERSOLLWERT | int | Kennlinie wurde angehoben |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KENNLINIE_TEXT | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (59 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (5 × 9)
- [BOSKENNUNG](#table-boskennung) (11 × 3)
- [INNENTEMPERATUR](#table-innentemperatur) (256 × 3)
- [VERDTEMPERATUR](#table-verdtemperatur) (256 × 3)
- [WTTEMPERATUR](#table-wttemperatur) (256 × 3)
- [SCHICHTTEMPERATUR](#table-schichttemperatur) (256 × 3)
- [CBSKENNUNG](#table-cbskennung) (16 × 3)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 59 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9C48 | Motor Frischluft/Umluft links |
| 0x9C49 | Motor Frischluft/Umluft rechts |
| 0x9C4A | Motor Entfrostung |
| 0x9C4B | Motor Belüftung links |
| 0x9C4C | Motor Belüftung rechts |
| 0x9C4D | Motor Kaltluft |
| 0x9C4E | Motor Fussraum links |
| 0x9C4F | Motor Fussraum rechts |
| 0x9C50 | Motor Belüftung Fond |
| 0x9C53 | PTC-Zuheizer |
| 0x9C54 | AUC-Sensor |
| 0x9C55 | Beschlagsensor |
| 0x9C56 | Standheiz-LED |
| 0x9C57 | Geblaese-Endstufe |
| 0x9C58 | Poti links |
| 0x9C59 | Poti rechts |
| 0x9C5A | Poti mitte |
| 0x9C5B | Innentemperaturfühler |
| 0x9C5C | Verdampfertemperaturfühler |
| 0x9C5D | Monitor Drucksensor-Versorgung |
| 0x9C5E | Drucksensor |
| 0x9C60 | Fühler Wärmetauscher rechts |
| 0x9C65 | Stromsense Treiberversorgung |
| 0x9C66 | Stromsense f. OL-Versorgung |
| 0x9C67 | Fühler Wärmetauscher links |
| 0x9C68 | Belüftungstemperaturfühler |
| 0x9C69 | Schichtung Fondpoti |
| 0x9C6a | Solarsensor links |
| 0x9C6b | Solarsensor rechts |
| 0x9C6c | Monitor AUC-Versorgung |
| 0x9C6d | Monitor Sonnensensor-Versorgung |
| 0x9C6e | Monitor Fondpotiversorgung |
| 0x9C6f | Monitor Beschlagsensor Versorgung |
| 0x9C77 | Zusatzwasserpumpe |
| 0x9C78 | Spritzdüsenheizung |
| 0x9C79 | Wasserventil links |
| 0x9C7A | Wasserventil rechts |
| 0x9C7B | Innenfuehlergeblaese |
| 0x9C7C | KMV-Sperrventil |
| 0x9C7E | Heckscheibenheizung |
| 0x9C7F | Checksumme EEPROM |
| 0x9CA7 | Energiesparmode aktiv |
| 0xE704 | K-Can physikalischer Busfehler |
| 0xE705 | K-CAN Bus High Leitungsfehler |
| 0xE706 | LIN-Busfehler |
| 0xE707 | CAN-Controller, Bus Off |
| 0xE714 | Botschaft(KCAN: Powermanagement Batteriespannung, 3BE) |
| 0xE715 | Botschaft(KCAN: Kilometerstand/Reichweite, 330) |
| 0xE716 | Botschaft(KCAN: Powermanagement Verbrauchersteuerung, 3B3) |
| 0xE717 | Botschaft(KCAN: Relativzeit, 328) |
| 0xE718 | Botschaft(KCAN: Wärmestrom Motor, 1B6) |
| 0xE719 | Botschaft(KCAN: Motordaten, 1D0) |
| 0xE71A | Botschaft(KCAN: Klemmenstatus, 130) |
| 0xE71B | Botschaft(KCAN: Aussentemperatur, 2CA) |
| 0xE71C | Botschaft(KCAN: Geschwindigkeit, 1A0) |
| 0xE71D | Botschaft(KCAN: Status Klima SH/ZH Zusatzwasserpumpe, 2EC) |
| 0xE71E | Botschaft(KCAN: Drehmoment 3, AA) |
| 0xE71F | Botschaft(KCAN: Dimmung, 202) |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | ja |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | 0x03 | 0x04 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Aussentemperatur | Grad C | - | unsigned char | - | 1 | 2 | -40 |
| 0x02 | Kuehlmitteltemperatur | Grad C | - | unsigned char | - | 1 | 1 | -48 |
| 0x03 | Batteriespannung | Volt | - | unsigned char | - | 1 | 10 | 0 |
| 0x04 | Relativzeit | s | high | signed long | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-boskennung"></a>
### BOSKENNUNG

Dimensions: 11 rows × 3 columns

| NR | BOS_K | BOS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Ölqualität |
| 0x02 | Br_v | Bremsbelagverschleiss vorne |
| 0x03 | Brfl | Bremsflüssigkeit |
| 0x04 | Filt | Mikrofilter |
| 0x05 | Batt | Batteriezustand |
| 0x06 | Br_h | Bremsbelagverschleiss hinten |
| 0x10 | ZKrz | Zündkerzen |
| 0x11 | Sic | Sichtprüfung |
| 0x12 | Kfl | Kühlflüssigkeit |
| 0x20 | TUV | TÜV |
| 0x21 | AU | AU |

<a id="table-innentemperatur"></a>
### INNENTEMPERATUR

Dimensions: 256 rows × 3 columns

| WERT | DEZIMALWERT | TEMPERATUR |
| --- | --- | --- |
| 0x00 |   0 |  20.0 |
| 0x01 |   1 |  20.0 |
| 0x02 |   2 |  20.0 |
| 0x03 |   3 |  20.0 |
| 0x04 |   4 |  20.0 |
| 0x05 |   5 |  20.0 |
| 0x06 |   6 |  20.0 |
| 0x07 |   7 |  20.0 |
| 0x08 |   8 |  20.0 |
| 0x09 |   9 |  20.0 |
| 0x0A |  10 |  20.0 |
| 0x0B |  11 |  20.0 |
| 0x0C |  12 |  20.0 |
| 0x0D |  13 |  20.0 |
| 0x0E |  14 |  20.0 |
| 0x0F |  15 |  20.0 |
| 0x10 |  16 |  20.0 |
| 0x11 |  17 |  20.0 |
| 0x12 |  18 |  20.0 |
| 0x13 |  19 |  20.0 |
| 0x14 |  20 |  20.0 |
| 0x15 |  21 |  20.0 |
| 0x16 |  22 |  20.0 |
| 0x17 |  23 |  40.0 |
| 0x18 |  24 |  40.0 |
| 0x19 |  25 |  40.0 |
| 0x1A |  26 |  40.0 |
| 0x1B |  27 |  40.0 |
| 0x1C |  28 |  40.0 |
| 0x1D |  29 |  40.0 |
| 0x1E |  30 |  40.0 |
| 0x1F |  31 |  40.0 |
| 0x20 |  32 |  40.0 |
| 0x21 |  33 |  40.0 |
| 0x22 |  34 |  40.0 |
| 0x23 |  35 |  40.0 |
| 0x24 |  36 |  40.0 |
| 0x25 |  37 |  40.0 |
| 0x26 |  38 |  40.0 |
| 0x27 |  39 |  40.0 |
| 0x28 |  40 |  40.0 |
| 0x29 |  41 |  40.0 |
| 0x2A |  42 |  40.0 |
| 0x2B |  43 |  40.0 |
| 0x2C |  44 |  40.0 |
| 0x2D |  45 |  40.0 |
| 0x2E |  46 |  40.0 |
| 0x2F |  47 |  40.0 |
| 0x30 |  48 |  40.0 |
| 0x31 |  49 |  40.0 |
| 0x32 |  50 |  40.0 |
| 0x33 |  51 |  40.0 |
| 0x34 |  52 |  40.0 |
| 0x35 |  53 |  40.0 |
| 0x36 |  54 |  40.0 |
| 0x37 |  55 |  40.0 |
| 0x38 |  56 |  40.0 |
| 0x39 |  57 |  40.0 |
| 0x3A |  58 |  40.0 |
| 0x3B |  59 |  40.0 |
| 0x3C |  60 |  40.0 |
| 0x3D |  61 |  40.0 |
| 0x3E |  62 |  40.0 |
| 0x3F |  63 |  40.0 |
| 0x40 |  64 |  40.0 |
| 0x41 |  65 |  40.0 |
| 0x42 |  66 |  40.0 |
| 0x43 |  67 |  40.0 |
| 0x44 |  68 |  40.0 |
| 0x45 |  69 |  40.0 |
| 0x46 |  70 |  40.0 |
| 0x47 |  71 |  40.0 |
| 0x48 |  72 |  40.0 |
| 0x49 |  73 |  40.0 |
| 0x4A |  74 |  40.0 |
| 0x4B |  75 |  40.0 |
| 0x4C |  76 |  40.0 |
| 0x4D |  77 |  40.0 |
| 0x4E |  78 |  40.0 |
| 0x4F |  79 |  40.0 |
| 0x50 |  80 |  40.0 |
| 0x51 |  81 |  40.0 |
| 0x52 |  82 |  40.0 |
| 0x53 |  83 |  40.0 |
| 0x54 |  84 |  40.0 |
| 0x55 |  85 |  40.0 |
| 0x56 |  86 |  40.0 |
| 0x57 |  87 |  40.0 |
| 0x58 |  88 |  40.0 |
| 0x59 |  89 |  40.0 |
| 0x5A |  90 |  40.0 |
| 0x5B |  91 |  40.0 |
| 0x5C |  92 |  40.0 |
| 0x5D |  93 |  40.0 |
| 0x5E |  94 |  39.5 |
| 0x5F |  95 |  39.0 |
| 0x60 |  96 |  38.5 |
| 0x61 |  97 |  38.0 |
| 0x62 |  98 |  37.5 |
| 0x63 |  99 |  37.0 |
| 0x64 | 100 |  36.6 |
| 0x65 | 101 |  36.1 |
| 0x66 | 102 |  35.6 |
| 0x67 | 103 |  35.3 |
| 0x68 | 104 |  35.0 |
| 0x69 | 105 |  34.5 |
| 0x6A | 106 |  34.0 |
| 0x6B | 107 |  33.5 |
| 0x6C | 108 |  33.0 |
| 0x6D | 109 |  32.5 |
| 0x6E | 110 |  32.1 |
| 0x6F | 111 |  31.6 |
| 0x70 | 112 |  31.3 |
| 0x71 | 113 |  31.0 |
| 0x72 | 114 |  30.5 |
| 0x73 | 115 |  30.1 |
| 0x74 | 116 |  29.6 |
| 0x75 | 117 |  29.3 |
| 0x76 | 118 |  29.0 |
| 0x77 | 119 |  28.5 |
| 0x78 | 120 |  28.1 |
| 0x79 | 121 |  27.6 |
| 0x7A | 122 |  27.3 |
| 0x7B | 123 |  27.0 |
| 0x7C | 124 |  26.5 |
| 0x7D | 125 |  26.1 |
| 0x7E | 126 |  25.6 |
| 0x7F | 127 |  25.3 |
| 0x80 | 128 |  25.0 |
| 0x81 | 129 |  24.5 |
| 0x82 | 130 |  24.0 |
| 0x83 | 131 |  23.5 |
| 0x84 | 132 |  23.0 |
| 0x85 | 133 |  22.5 |
| 0x86 | 134 |  22.1 |
| 0x87 | 135 |  21.6 |
| 0x88 | 136 |  21.3 |
| 0x89 | 137 |  21.0 |
| 0x8A | 138 |  20.6 |
| 0x8B | 139 |  20.3 |
| 0x8C | 140 |  20.0 |
| 0x8D | 141 |  19.6 |
| 0x8E | 142 |  19.3 |
| 0x8F | 143 |  19.0 |
| 0x90 | 144 |  18.5 |
| 0x91 | 145 |  18.1 |
| 0x92 | 146 |  17.6 |
| 0x93 | 147 |  17.3 |
| 0x94 | 148 |  17.0 |
| 0x95 | 149 |  16.5 |
| 0x96 | 150 |  16.1 |
| 0x97 | 151 |  15.6 |
| 0x98 | 152 |  15.3 |
| 0x99 | 153 |  15.0 |
| 0x9A | 154 |  14.5 |
| 0x9B | 155 |  14.1 |
| 0x9C | 156 |  13.6 |
| 0x9D | 157 |  13.3 |
| 0x9E | 158 |  13.0 |
| 0x9F | 159 |  12.5 |
| 0xA0 | 160 |  12.0 |
| 0xA1 | 161 |  11.6 |
| 0xA2 | 162 |  11.1 |
| 0xA3 | 163 |  10.8 |
| 0xA4 | 164 |  10.3 |
| 0xA5 | 165 |  10.0 |
| 0xA6 | 166 |  10.0 |
| 0xA7 | 167 |  10.0 |
| 0xA8 | 168 |  10.0 |
| 0xA9 | 169 |  10.0 |
| 0xAA | 170 |  10.0 |
| 0xAB | 171 |  10.0 |
| 0xAC | 172 |  10.0 |
| 0xAD | 173 |  10.0 |
| 0xAE | 174 |  10.0 |
| 0xAF | 175 |  10.0 |
| 0xB0 | 176 |  10.0 |
| 0xB1 | 177 |  10.0 |
| 0xB2 | 178 |  10.0 |
| 0xB3 | 179 |  10.0 |
| 0xB4 | 180 |  10.0 |
| 0xB5 | 181 |  10.0 |
| 0xB6 | 182 |  10.0 |
| 0xB7 | 183 |  10.0 |
| 0xB8 | 184 |  10.0 |
| 0xB9 | 185 |  10.0 |
| 0xBA | 186 |  10.0 |
| 0xBB | 187 |  10.0 |
| 0xBC | 188 |  10.0 |
| 0xBD | 189 |  10.0 |
| 0xBE | 190 |  10.0 |
| 0xBF | 191 |  10.0 |
| 0xC0 | 192 |  10.0 |
| 0xC1 | 193 |  10.0 |
| 0xC2 | 194 |  10.0 |
| 0xC3 | 195 |  10.0 |
| 0xC4 | 196 |  10.0 |
| 0xC5 | 197 |  10.0 |
| 0xC6 | 198 |  10.0 |
| 0xC7 | 199 |  10.0 |
| 0xC8 | 200 |  10.0 |
| 0xC9 | 201 |  10.0 |
| 0xCA | 202 |  10.0 |
| 0xCB | 203 |  10.0 |
| 0xCC | 204 |  10.0 |
| 0xCD | 205 |  10.0 |
| 0xCE | 206 |  10.0 |
| 0xCF | 207 |  10.0 |
| 0xD0 | 208 |  10.0 |
| 0xD1 | 209 |  10.0 |
| 0xD2 | 210 |  10.0 |
| 0xD3 | 211 |  10.0 |
| 0xD4 | 212 |  10.0 |
| 0xD5 | 213 |  10.0 |
| 0xD6 | 214 |  10.0 |
| 0xD7 | 215 |  10.0 |
| 0xD8 | 216 |  10.0 |
| 0xD9 | 217 |  10.0 |
| 0xDA | 218 |  10.0 |
| 0xDB | 219 |  10.0 |
| 0xDC | 220 |  10.0 |
| 0xDD | 221 |  10.0 |
| 0xDE | 222 |  10.0 |
| 0xDF | 223 |  10.0 |
| 0xE0 | 224 |  10.0 |
| 0xE1 | 225 |  10.0 |
| 0xE2 | 226 |  10.0 |
| 0xE3 | 227 |  10.0 |
| 0xE4 | 228 |  10.0 |
| 0xE5 | 229 |  10.0 |
| 0xE6 | 230 |  10.0 |
| 0xE7 | 231 |  10.0 |
| 0xE8 | 232 |  10.0 |
| 0xE9 | 233 |  10.0 |
| 0xEA | 234 |  10.0 |
| 0xEB | 235 |  10.0 |
| 0xEC | 236 |  10.0 |
| 0xED | 237 |  10.0 |
| 0xEE | 238 |  10.0 |
| 0xEF | 239 |  10.0 |
| 0xF0 | 240 |  10.0 |
| 0xF1 | 241 |  10.0 |
| 0xF2 | 242 |  10.0 |
| 0xF3 | 243 |  10.0 |
| 0xF4 | 244 |  10.0 |
| 0xF5 | 245 |  10.0 |
| 0xF6 | 246 |  10.0 |
| 0xF7 | 247 |  10.0 |
| 0xF8 | 248 |  10.0 |
| 0xF9 | 249 |  10.0 |
| 0xFA | 250 |  10.0 |
| 0xFB | 251 |  20.0 |
| 0xFC | 252 |  20.0 |
| 0xFD | 253 |  20.0 |
| 0xFE | 254 |  20.0 |
| 0xFF | 255 |  20.0 |

<a id="table-verdtemperatur"></a>
### VERDTEMPERATUR

Dimensions: 256 rows × 3 columns

| WERT | DEZIMALWERT | TEMPERATUR |
| --- | --- | --- |
| 0x00 |   0 |  -2.0 |
| 0x01 |   1 |  -2.0 |
| 0x02 |   2 |  -2.0 |
| 0x03 |   3 |  -2.0 |
| 0x04 |   4 |  -2.0 |
| 0x05 |   5 |  -2.0 |
| 0x06 |   6 |  -2.0 |
| 0x07 |   7 |  -2.0 |
| 0x08 |   8 |  40.0 |
| 0x09 |   9 |  40.0 |
| 0x0A |  10 |  40.0 |
| 0x0B |  11 |  40.0 |
| 0x0C |  12 |  40.0 |
| 0x0D |  13 |  40.0 |
| 0x0E |  14 |  40.0 |
| 0x0F |  15 |  40.0 |
| 0x10 |  16 |  40.0 |
| 0x11 |  17 |  40.0 |
| 0x12 |  18 |  40.0 |
| 0x13 |  19 |  40.0 |
| 0x14 |  20 |  40.0 |
| 0x15 |  21 |  40.0 |
| 0x16 |  22 |  40.0 |
| 0x17 |  23 |  40.0 |
| 0x18 |  24 |  40.0 |
| 0x19 |  25 |  40.0 |
| 0x1A |  26 |  40.0 |
| 0x1B |  27 |  40.0 |
| 0x1C |  28 |  40.0 |
| 0x1D |  29 |  40.0 |
| 0x1E |  30 |  40.0 |
| 0x1F |  31 |  40.0 |
| 0x20 |  32 |  40.0 |
| 0x21 |  33 |  40.0 |
| 0x22 |  34 |  40.0 |
| 0x23 |  35 |  40.0 |
| 0x24 |  36 |  40.0 |
| 0x25 |  37 |  40.0 |
| 0x26 |  38 |  40.0 |
| 0x27 |  39 |  40.0 |
| 0x28 |  40 |  40.0 |
| 0x29 |  41 |  40.0 |
| 0x2A |  42 |  40.0 |
| 0x2B |  43 |  40.0 |
| 0x2C |  44 |  40.0 |
| 0x2D |  45 |  40.0 |
| 0x2E |  46 |  40.0 |
| 0x2F |  47 |  40.0 |
| 0x30 |  48 |  40.0 |
| 0x31 |  49 |  40.0 |
| 0x32 |  50 |  39.2 |
| 0x33 |  51 |  38.6 |
| 0x34 |  52 |  38.0 |
| 0x35 |  53 |  37.4 |
| 0x36 |  54 |  36.8 |
| 0x37 |  55 |  36.2 |
| 0x38 |  56 |  35.6 |
| 0x39 |  57 |  35.0 |
| 0x3A |  58 |  34.4 |
| 0x3B |  59 |  34.0 |
| 0x3C |  60 |  33.4 |
| 0x3D |  61 |  33.0 |
| 0x3E |  62 |  32.4 |
| 0x3F |  63 |  32.0 |
| 0x40 |  64 |  31.4 |
| 0x41 |  65 |  31.0 |
| 0x42 |  66 |  30.4 |
| 0x43 |  67 |  30.0 |
| 0x44 |  68 |  29.4 |
| 0x45 |  69 |  29.0 |
| 0x46 |  70 |  28.6 |
| 0x47 |  71 |  28.0 |
| 0x48 |  72 |  27.6 |
| 0x49 |  73 |  27.2 |
| 0x4A |  74 |  26.8 |
| 0x4B |  75 |  26.2 |
| 0x4C |  76 |  25.8 |
| 0x4D |  77 |  25.4 |
| 0x4E |  78 |  25.0 |
| 0x4F |  79 |  24.6 |
| 0x50 |  80 |  24.2 |
| 0x51 |  81 |  23.8 |
| 0x52 |  82 |  23.4 |
| 0x53 |  83 |  23.0 |
| 0x54 |  84 |  22.6 |
| 0x55 |  85 |  22.2 |
| 0x56 |  86 |  21.8 |
| 0x57 |  87 |  21.4 |
| 0x58 |  88 |  21.0 |
| 0x59 |  89 |  20.6 |
| 0x5A |  90 |  20.2 |
| 0x5B |  91 |  20.0 |
| 0x5C |  92 |  19.6 |
| 0x5D |  93 |  19.2 |
| 0x5E |  94 |  18.8 |
| 0x5F |  95 |  18.6 |
| 0x60 |  96 |  18.2 |
| 0x61 |  97 |  17.8 |
| 0x62 |  98 |  17.4 |
| 0x63 |  99 |  17.0 |
| 0x64 | 100 |  16.6 |
| 0x65 | 101 |  16.4 |
| 0x66 | 102 |  16.0 |
| 0x67 | 103 |  15.6 |
| 0x68 | 104 |  15.2 |
| 0x69 | 105 |  15.0 |
| 0x6A | 106 |  14.6 |
| 0x6B | 107 |  14.2 |
| 0x6C | 108 |  14.0 |
| 0x6D | 109 |  13.6 |
| 0x6E | 110 |  13.2 |
| 0x6F | 111 |  13.0 |
| 0x70 | 112 |  12.6 |
| 0x71 | 113 |  12.2 |
| 0x72 | 114 |  12.0 |
| 0x73 | 115 |  11.6 |
| 0x74 | 116 |  11.2 |
| 0x75 | 117 |  11.0 |
| 0x76 | 118 |  10.6 |
| 0x77 | 119 |  10.2 |
| 0x78 | 120 |  10.0 |
| 0x79 | 121 |   9.6 |
| 0x7A | 122 |   9.2 |
| 0x7B | 123 |   9.0 |
| 0x7C | 124 |   8.6 |
| 0x7D | 125 |   8.2 |
| 0x7E | 126 |   8.0 |
| 0x7F | 127 |   7.6 |
| 0x80 | 128 |   7.2 |
| 0x81 | 129 |   7.0 |
| 0x82 | 130 |   6.6 |
| 0x83 | 131 |   6.2 |
| 0x84 | 132 |   6.0 |
| 0x85 | 133 |   5.6 |
| 0x86 | 134 |   5.2 |
| 0x87 | 135 |   5.0 |
| 0x88 | 136 |   4.6 |
| 0x89 | 137 |   4.2 |
| 0x8A | 138 |   4.0 |
| 0x8B | 139 |   3.6 |
| 0x8C | 140 |   3.4 |
| 0x8D | 141 |   3.0 |
| 0x8E | 142 |   2.8 |
| 0x8F | 143 |   2.4 |
| 0x90 | 144 |   2.0 |
| 0x91 | 145 |   1.8 |
| 0x92 | 146 |   1.4 |
| 0x93 | 147 |   1.2 |
| 0x94 | 148 |   0.8 |
| 0x95 | 149 |   0.6 |
| 0x96 | 150 |   0.1 |
| 0x97 | 151 |   0.0 |
| 0x98 | 152 |  -0.4 |
| 0x99 | 153 |  -0.8 |
| 0x9A | 154 |  -1.0 |
| 0x9B | 155 |  -1.4 |
| 0x9C | 156 |  -1.6 |
| 0x9D | 157 |  -2.0 |
| 0x9E | 158 |  -2.2 |
| 0x9F | 159 |  -2.6 |
| 0xA0 | 160 |  -3.0 |
| 0xA1 | 161 |  -3.2 |
| 0xA2 | 162 |  -3.6 |
| 0xA3 | 163 |  -3.8 |
| 0xA4 | 164 |  -4.2 |
| 0xA5 | 165 |  -4.4 |
| 0xA6 | 166 |  -4.8 |
| 0xA7 | 167 |  -5.0 |
| 0xA8 | 168 |  -5.4 |
| 0xA9 | 169 |  -5.8 |
| 0xAA | 170 |  -6.2 |
| 0xAB | 171 |  -6.6 |
| 0xAC | 172 |  -6.8 |
| 0xAD | 173 |  -7.2 |
| 0xAE | 174 |  -7.6 |
| 0xAF | 175 |  -8.0 |
| 0xB0 | 176 |  -8.4 |
| 0xB1 | 177 |  -8.6 |
| 0xB2 | 178 |  -9.0 |
| 0xB3 | 179 |  -9.4 |
| 0xB4 | 180 |  -9.8 |
| 0xB5 | 181 | -10.0 |
| 0xB6 | 182 | -10.0 |
| 0xB7 | 183 | -10.0 |
| 0xB8 | 184 | -10.0 |
| 0xB9 | 185 | -10.0 |
| 0xBA | 186 | -10.0 |
| 0xBB | 187 | -10.0 |
| 0xBC | 188 | -10.0 |
| 0xBD | 189 | -10.0 |
| 0xBE | 190 | -10.0 |
| 0xBF | 191 | -10.0 |
| 0xC0 | 192 | -10.0 |
| 0xC1 | 193 | -10.0 |
| 0xC2 | 194 | -10.0 |
| 0xC3 | 195 | -10.0 |
| 0xC4 | 196 | -10.0 |
| 0xC5 | 197 | -10.0 |
| 0xC6 | 198 | -10.0 |
| 0xC7 | 199 | -10.0 |
| 0xC8 | 200 | -10.0 |
| 0xC9 | 201 | -10.0 |
| 0xCA | 202 | -10.0 |
| 0xCB | 203 | -10.0 |
| 0xCC | 204 | -10.0 |
| 0xCD | 205 | -10.0 |
| 0xCE | 206 | -10.0 |
| 0xCF | 207 | -10.0 |
| 0xD0 | 208 | -10.0 |
| 0xD1 | 209 | -10.0 |
| 0xD2 | 210 | -10.0 |
| 0xD3 | 211 | -10.0 |
| 0xD4 | 212 | -10.0 |
| 0xD5 | 213 | -10.0 |
| 0xD6 | 214 | -10.0 |
| 0xD7 | 215 | -10.0 |
| 0xD8 | 216 | -10.0 |
| 0xD9 | 217 | -10.0 |
| 0xDA | 218 | -10.0 |
| 0xDB | 219 | -10.0 |
| 0xDC | 220 | -10.0 |
| 0xDD | 221 | -10.0 |
| 0xDE | 222 | -10.0 |
| 0xDF | 223 | -10.0 |
| 0xE0 | 224 | -10.0 |
| 0xE1 | 225 | -10.0 |
| 0xE2 | 226 | -10.0 |
| 0xE3 | 227 | -10.0 |
| 0xE4 | 228 | -10.0 |
| 0xE5 | 229 | -10.0 |
| 0xE6 | 230 | -10.0 |
| 0xE7 | 231 | -10.0 |
| 0xE8 | 232 | -10.0 |
| 0xE9 | 233 | -10.0 |
| 0xEA | 234 | -10.0 |
| 0xEB | 235 | -10.0 |
| 0xEC | 236 | -10.0 |
| 0xED | 237 | -10.0 |
| 0xEE | 238 | -10.0 |
| 0xEF | 239 | -10.0 |
| 0xF0 | 240 |  -2.0 |
| 0xF1 | 241 |  -2.0 |
| 0xF2 | 242 |  -2.0 |
| 0xF3 | 243 |  -2.0 |
| 0xF4 | 244 |  -2.0 |
| 0xF5 | 245 |  -2.0 |
| 0xF6 | 246 |  -2.0 |
| 0xF7 | 247 |  -2.0 |
| 0xF8 | 248 |  -2.0 |
| 0xF9 | 249 |  -2.0 |
| 0xFA | 250 |  -2.0 |
| 0xFB | 251 |  -2.0 |
| 0xFC | 252 |  -2.0 |
| 0xFD | 253 |  -2.0 |
| 0xFE | 254 |  -2.0 |
| 0xFF | 255 |  -2.0 |

<a id="table-wttemperatur"></a>
### WTTEMPERATUR

Dimensions: 256 rows × 3 columns

| WERT | DEZIMALWERT | TEMPERATUR |
| --- | --- | --- |
| 0x00 |   0 |  55.0 |
| 0x01 |   1 |  55.0 |
| 0x02 |   2 |  55.0 |
| 0x03 |   3 |  55.0 |
| 0x04 |   4 |  55.0 |
| 0x05 |   5 |  55.0 |
| 0x06 |   6 |  55.0 |
| 0x07 |   7 |  55.0 |
| 0x08 |   8 |  55.0 |
| 0x09 |   9 |  55.0 |
| 0x0A |  10 |  55.0 |
| 0x0B |  11 |  55.0 |
| 0x0C |  12 |  55.0 |
| 0x0D |  13 |  55.0 |
| 0x0E |  14 |  55.0 |
| 0x0F |  15 |  55.0 |
| 0x10 |  16 |  55.0 |
| 0x11 |  17 |  55.0 |
| 0x12 |  18 |  55.0 |
| 0x13 |  19 |  55.0 |
| 0x14 |  20 |  55.0 |
| 0x15 |  21 |  55.0 |
| 0x16 |  22 | 125.0 |
| 0x17 |  23 | 123.0 |
| 0x18 |  24 | 121.5 |
| 0x19 |  25 | 120.0 |
| 0x1A |  26 | 118.0 |
| 0x1B |  27 | 116.5 |
| 0x1C |  28 | 115.0 |
| 0x1D |  29 | 113.0 |
| 0x1E |  30 | 111.5 |
| 0x1F |  31 | 110.0 |
| 0x20 |  32 | 109.0 |
| 0x21 |  33 | 108.0 |
| 0x22 |  34 | 107.0 |
| 0x23 |  35 | 106.0 |
| 0x24 |  36 | 105.0 |
| 0x25 |  37 | 104.0 |
| 0x26 |  38 | 103.0 |
| 0x27 |  39 | 102.0 |
| 0x28 |  40 | 101.0 |
| 0x29 |  41 | 100.0 |
| 0x2A |  42 |  99.0 |
| 0x2B |  43 |  98.0 |
| 0x2C |  44 |  97.0 |
| 0x2D |  45 |  96.0 |
| 0x2E |  46 |  95.0 |
| 0x2F |  47 |  94.0 |
| 0x30 |  48 |  93.0 |
| 0x31 |  49 |  92.0 |
| 0x32 |  50 |  91.5 |
| 0x33 |  51 |  90.5 |
| 0x34 |  52 |  90.0 |
| 0x35 |  53 |  89.0 |
| 0x36 |  54 |  88.0 |
| 0x37 |  55 |  87.0 |
| 0x38 |  56 |  86.5 |
| 0x39 |  57 |  85.5 |
| 0x3A |  58 |  85.0 |
| 0x3B |  59 |  84.0 |
| 0x3C |  60 |  83.5 |
| 0x3D |  61 |  83.0 |
| 0x3E |  62 |  82.5 |
| 0x3F |  63 |  81.5 |
| 0x40 |  64 |  81.0 |
| 0x41 |  65 |  80.5 |
| 0x42 |  66 |  80.0 |
| 0x43 |  67 |  79.0 |
| 0x44 |  68 |  78.5 |
| 0x45 |  69 |  78.0 |
| 0x46 |  70 |  77.5 |
| 0x47 |  71 |  76.5 |
| 0x48 |  72 |  76.0 |
| 0x49 |  73 |  75.5 |
| 0x4A |  74 |  75.0 |
| 0x4B |  75 |  74.0 |
| 0x4C |  76 |  73.5 |
| 0x4D |  77 |  73.0 |
| 0x4E |  78 |  72.5 |
| 0x4F |  79 |  72.0 |
| 0x50 |  80 |  71.5 |
| 0x51 |  81 |  71.0 |
| 0x52 |  82 |  70.5 |
| 0x53 |  83 |  70.0 |
| 0x54 |  84 |  69.5 |
| 0x55 |  85 |  69.0 |
| 0x56 |  86 |  68.5 |
| 0x57 |  87 |  68.0 |
| 0x58 |  88 |  67.5 |
| 0x59 |  89 |  67.0 |
| 0x5A |  90 |  66.5 |
| 0x5B |  91 |  66.0 |
| 0x5C |  92 |  65.5 |
| 0x5D |  93 |  65.0 |
| 0x5E |  94 |  65.0 |
| 0x5F |  95 |  64.5 |
| 0x60 |  96 |  64.0 |
| 0x61 |  97 |  63.5 |
| 0x62 |  98 |  63.0 |
| 0x63 |  99 |  62.5 |
| 0x64 | 100 |  62.0 |
| 0x65 | 101 |  61.5 |
| 0x66 | 102 |  61.0 |
| 0x67 | 103 |  60.5 |
| 0x68 | 104 |  60.0 |
| 0x69 | 105 |  59.5 |
| 0x6A | 106 |  59.0 |
| 0x6B | 107 |  58.5 |
| 0x6C | 108 |  58.0 |
| 0x6D | 109 |  57.5 |
| 0x6E | 110 |  57.0 |
| 0x6F | 111 |  57.0 |
| 0x70 | 112 |  56.5 |
| 0x71 | 113 |  56.0 |
| 0x72 | 114 |  55.5 |
| 0x73 | 115 |  55.0 |
| 0x74 | 116 |  55.0 |
| 0x75 | 117 |  54.5 |
| 0x76 | 118 |  54.0 |
| 0x77 | 119 |  53.5 |
| 0x78 | 120 |  53.0 |
| 0x79 | 121 |  52.5 |
| 0x7A | 122 |  52.5 |
| 0x7B | 123 |  52.0 |
| 0x7C | 124 |  51.5 |
| 0x7D | 125 |  51.0 |
| 0x7E | 126 |  50.5 |
| 0x7F | 127 |  50.0 |
| 0x80 | 128 |  50.0 |
| 0x81 | 129 |  49.5 |
| 0x82 | 130 |  49.0 |
| 0x83 | 131 |  48.5 |
| 0x84 | 132 |  48.0 |
| 0x85 | 133 |  47.5 |
| 0x86 | 134 |  47.5 |
| 0x87 | 135 |  47.0 |
| 0x88 | 136 |  46.5 |
| 0x89 | 137 |  46.0 |
| 0x8A | 138 |  45.5 |
| 0x8B | 139 |  45.0 |
| 0x8C | 140 |  45.0 |
| 0x8D | 141 |  44.5 |
| 0x8E | 142 |  44.0 |
| 0x8F | 143 |  43.5 |
| 0x90 | 144 |  43.0 |
| 0x91 | 145 |  42.5 |
| 0x92 | 146 |  42.5 |
| 0x93 | 147 |  42.0 |
| 0x94 | 148 |  41.5 |
| 0x95 | 149 |  41.0 |
| 0x96 | 150 |  40.5 |
| 0x97 | 151 |  40.0 |
| 0x98 | 152 |  40.0 |
| 0x99 | 153 |  39.5 |
| 0x9A | 154 |  39.0 |
| 0x9B | 155 |  38.5 |
| 0x9C | 156 |  38.0 |
| 0x9D | 157 |  37.5 |
| 0x9E | 158 |  37.5 |
| 0x9F | 159 |  37.0 |
| 0xA0 | 160 |  36.5 |
| 0xA1 | 161 |  36.0 |
| 0xA2 | 162 |  35.5 |
| 0xA3 | 163 |  35.0 |
| 0xA4 | 164 |  35.0 |
| 0xA5 | 165 |  34.5 |
| 0xA6 | 166 |  34.0 |
| 0xA7 | 167 |  33.5 |
| 0xA8 | 168 |  33.0 |
| 0xA9 | 169 |  32.5 |
| 0xAA | 170 |  32.5 |
| 0xAB | 171 |  32.0 |
| 0xAC | 172 |  31.5 |
| 0xAD | 173 |  31.0 |
| 0xAE | 174 |  30.5 |
| 0xAF | 175 |  30.0 |
| 0xB0 | 176 |  30.0 |
| 0xB1 | 177 |  29.5 |
| 0xB2 | 178 |  29.0 |
| 0xB3 | 179 |  28.5 |
| 0xB4 | 180 |  28.0 |
| 0xB5 | 181 |  27.5 |
| 0xB6 | 182 |  27.5 |
| 0xB7 | 183 |  27.0 |
| 0xB8 | 184 |  26.5 |
| 0xB9 | 185 |  26.0 |
| 0xBA | 186 |  25.5 |
| 0xBB | 187 |  25.0 |
| 0xBC | 188 |  25.0 |
| 0xBD | 189 |  24.5 |
| 0xBE | 190 |  24.0 |
| 0xBF | 191 |  23.5 |
| 0xC0 | 192 |  23.0 |
| 0xC1 | 193 |  22.5 |
| 0xC2 | 194 |  22.0 |
| 0xC3 | 195 |  21.5 |
| 0xC4 | 196 |  21.0 |
| 0xC5 | 197 |  20.5 |
| 0xC6 | 198 |  20.0 |
| 0xC7 | 199 |  19.5 |
| 0xC8 | 200 |  19.0 |
| 0xC9 | 201 |  18.5 |
| 0xCA | 202 |  18.0 |
| 0xCB | 203 |  17.5 |
| 0xCC | 204 |  17.0 |
| 0xCD | 205 |  16.5 |
| 0xCE | 206 |  16.0 |
| 0xCF | 207 |  15.5 |
| 0xD0 | 208 |  15.0 |
| 0xD1 | 209 |  14.0 |
| 0xD2 | 210 |  13.5 |
| 0xD3 | 211 |  13.0 |
| 0xD4 | 212 |  12.5 |
| 0xD5 | 213 |  11.5 |
| 0xD6 | 214 |  11.0 |
| 0xD7 | 215 |  10.5 |
| 0xD8 | 216 |  10.0 |
| 0xD9 | 217 |   9.0 |
| 0xDA | 218 |   8.5 |
| 0xDB | 219 |   7.5 |
| 0xDC | 220 |   7.5 |
| 0xDD | 221 |   6.5 |
| 0xDE | 222 |   6.0 |
| 0xDF | 223 |   5.5 |
| 0xE0 | 224 |   5.0 |
| 0xE1 | 225 |   5.0 |
| 0xE2 | 226 |   5.0 |
| 0xE3 | 227 |   5.0 |
| 0xE4 | 228 |   5.0 |
| 0xE5 | 229 |   5.0 |
| 0xE6 | 230 |   5.0 |
| 0xE7 | 231 |   5.0 |
| 0xE8 | 232 |   5.0 |
| 0xE9 | 233 |   5.0 |
| 0xEA | 234 |   5.0 |
| 0xEB | 235 |   5.0 |
| 0xEC | 236 |   5.0 |
| 0xED | 237 |   5.0 |
| 0xEE | 238 |   5.0 |
| 0xEF | 239 |   5.0 |
| 0xF0 | 240 |   5.0 |
| 0xF1 | 241 |   5.0 |
| 0xF2 | 242 |   5.0 |
| 0xF3 | 243 |   5.0 |
| 0xF4 | 244 |   5.0 |
| 0xF5 | 245 |   5.0 |
| 0xF6 | 246 |   5.0 |
| 0xF7 | 247 |   5.0 |
| 0xF8 | 248 |   5.0 |
| 0xF9 | 249 |   5.0 |
| 0xFA | 250 |   5.0 |
| 0xFB | 251 |   5.0 |
| 0xFC | 252 |   5.0 |
| 0xFD | 253 |  55.0 |
| 0xFE | 254 |  55.0 |
| 0xFF | 255 |  55.0 |

<a id="table-schichttemperatur"></a>
### SCHICHTTEMPERATUR

Dimensions: 256 rows × 3 columns

| WERT | DEZIMALWERT | TEMPERATUR |
| --- | --- | --- |
| 0x00 |   0 |  20.0 |
| 0x01 |   1 |  20.0 |
| 0x02 |   2 |  20.0 |
| 0x03 |   3 |  20.0 |
| 0x04 |   4 |  20.0 |
| 0x05 |   5 |  20.0 |
| 0x06 |   6 |  20.0 |
| 0x07 |   7 |  20.0 |
| 0x08 |   8 |  20.0 |
| 0x09 |   9 |  20.0 |
| 0x0A |  10 |  20.0 |
| 0x0B |  11 |  20.0 |
| 0x0C |  12 |  20.0 |
| 0x0D |  13 |  20.0 |
| 0x0E |  14 |  20.0 |
| 0x0F |  15 |  20.0 |
| 0x10 |  16 |  20.0 |
| 0x11 |  17 |  20.0 |
| 0x12 |  18 |  80.0 |
| 0x13 |  19 |  80.0 |
| 0x14 |  20 |  80.0 |
| 0x15 |  21 |  80.0 |
| 0x16 |  22 |  80.0 |
| 0x17 |  23 |  80.0 |
| 0x18 |  24 |  80.0 |
| 0x19 |  25 |  80.0 |
| 0x1A |  26 |  80.0 |
| 0x1B |  27 |  80.0 |
| 0x1C |  28 |  80.0 |
| 0x1D |  29 |  80.0 |
| 0x1E |  30 |  80.0 |
| 0x1F |  31 |  80.0 |
| 0x20 |  32 |  80.0 |
| 0x21 |  33 |  80.0 |
| 0x22 |  34 |  80.0 |
| 0x23 |  35 |  80.0 |
| 0x24 |  36 |  80.0 |
| 0x25 |  37 |  80.0 |
| 0x26 |  38 |  80.0 |
| 0x27 |  39 |  80.0 |
| 0x28 |  40 |  80.0 |
| 0x29 |  41 |  80.0 |
| 0x2A |  42 |  80.0 |
| 0x2B |  43 |  80.0 |
| 0x2C |  44 |  80.0 |
| 0x2D |  45 |  80.0 |
| 0x2E |  46 |  80.0 |
| 0x2F |  47 |  80.0 |
| 0x30 |  48 |  80.0 |
| 0x31 |  49 |  80.0 |
| 0x32 |  50 |  80.0 |
| 0x33 |  51 |  79.0 |
| 0x34 |  52 |  78.3 |
| 0x35 |  53 |  77.6 |
| 0x36 |  54 |  77.0 |
| 0x37 |  55 |  76.3 |
| 0x38 |  56 |  75.6 |
| 0x39 |  57 |  75.0 |
| 0x3A |  58 |  74.3 |
| 0x3B |  59 |  73.6 |
| 0x3C |  60 |  73.0 |
| 0x3D |  61 |  72.6 |
| 0x3E |  62 |  72.0 |
| 0x3F |  63 |  71.3 |
| 0x40 |  64 |  70.6 |
| 0x41 |  65 |  70.3 |
| 0x42 |  66 |  69.6 |
| 0x43 |  67 |  69.0 |
| 0x44 |  68 |  68.6 |
| 0x45 |  69 |  68.0 |
| 0x46 |  70 |  67.3 |
| 0x47 |  71 |  66.6 |
| 0x48 |  72 |  66.3 |
| 0x49 |  73 |  65.6 |
| 0x4A |  74 |  65.0 |
| 0x4B |  75 |  64.3 |
| 0x4C |  76 |  64.0 |
| 0x4D |  77 |  63.3 |
| 0x4E |  78 |  62.6 |
| 0x4F |  79 |  62.0 |
| 0x50 |  80 |  61.6 |
| 0x51 |  81 |  61.0 |
| 0x52 |  82 |  60.3 |
| 0x53 |  83 |  60.0 |
| 0x54 |  84 |  59.3 |
| 0x55 |  85 |  59.0 |
| 0x56 |  86 |  58.3 |
| 0x57 |  87 |  58.0 |
| 0x58 |  88 |  57.6 |
| 0x59 |  89 |  57.0 |
| 0x5A |  90 |  56.6 |
| 0x5B |  91 |  56.3 |
| 0x5C |  92 |  55.6 |
| 0x5D |  93 |  55.3 |
| 0x5E |  94 |  55.0 |
| 0x5F |  95 |  54.3 |
| 0x60 |  96 |  54.0 |
| 0x61 |  97 |  53.6 |
| 0x62 |  98 |  53.3 |
| 0x63 |  99 |  52.6 |
| 0x64 | 100 |  52.3 |
| 0x65 | 101 |  52.0 |
| 0x66 | 102 |  51.6 |
| 0x67 | 103 |  51.0 |
| 0x68 | 104 |  50.6 |
| 0x69 | 105 |  50.3 |
| 0x6A | 106 |  50.0 |
| 0x6B | 107 |  49.3 |
| 0x6C | 108 |  49.0 |
| 0x6D | 109 |  48.6 |
| 0x6E | 110 |  48.3 |
| 0x6F | 111 |  47.6 |
| 0x70 | 112 |  47.3 |
| 0x71 | 113 |  47.0 |
| 0x72 | 114 |  46.6 |
| 0x73 | 115 |  46.0 |
| 0x74 | 116 |  45.6 |
| 0x75 | 117 |  45.3 |
| 0x76 | 118 |  45.0 |
| 0x77 | 119 |  44.3 |
| 0x78 | 120 |  44.0 |
| 0x79 | 121 |  43.6 |
| 0x7A | 122 |  43.3 |
| 0x7B | 123 |  42.6 |
| 0x7C | 124 |  42.3 |
| 0x7D | 125 |  42.0 |
| 0x7E | 126 |  41.6 |
| 0x7F | 127 |  41.0 |
| 0x80 | 128 |  40.6 |
| 0x81 | 129 |  40.3 |
| 0x82 | 130 |  40.0 |
| 0x83 | 131 |  39.3 |
| 0x84 | 132 |  39.0 |
| 0x85 | 133 |  38.6 |
| 0x86 | 134 |  38.3 |
| 0x87 | 135 |  38.0 |
| 0x88 | 136 |  37.3 |
| 0x89 | 137 |  37.0 |
| 0x8A | 138 |  36.6 |
| 0x8B | 139 |  36.3 |
| 0x8C | 140 |  36.0 |
| 0x8D | 141 |  35.6 |
| 0x8E | 142 |  35.3 |
| 0x8F | 143 |  35.0 |
| 0x90 | 144 |  34.3 |
| 0x91 | 145 |  34.0 |
| 0x92 | 146 |  33.6 |
| 0x93 | 147 |  33.3 |
| 0x94 | 148 |  33.0 |
| 0x95 | 149 |  32.6 |
| 0x96 | 150 |  32.0 |
| 0x97 | 151 |  31.6 |
| 0x98 | 152 |  31.3 |
| 0x99 | 153 |  31.0 |
| 0x9A | 154 |  30.6 |
| 0x9B | 155 |  30.3 |
| 0x9C | 156 |  30.0 |
| 0x9D | 157 |  29.3 |
| 0x9E | 158 |  29.0 |
| 0x9F | 159 |  28.6 |
| 0xA0 | 160 |  28.3 |
| 0xA1 | 161 |  28.0 |
| 0xA2 | 162 |  27.6 |
| 0xA3 | 163 |  27.0 |
| 0xA4 | 164 |  26.6 |
| 0xA5 | 165 |  26.3 |
| 0xA6 | 166 |  26.0 |
| 0xA7 | 167 |  25.6 |
| 0xA8 | 168 |  25.3 |
| 0xA9 | 169 |  25.0 |
| 0xAA | 170 |  24.3 |
| 0xAB | 171 |  24.0 |
| 0xAC | 172 |  23.6 |
| 0xAD | 173 |  23.3 |
| 0xAE | 174 |  22.6 |
| 0xAF | 175 |  22.3 |
| 0xB0 | 176 |  22.0 |
| 0xB1 | 177 |  21.6 |
| 0xB2 | 178 |  21.0 |
| 0xB3 | 179 |  20.6 |
| 0xB4 | 180 |  20.3 |
| 0xB5 | 181 |  20.0 |
| 0xB6 | 182 |  19.3 |
| 0xB7 | 183 |  19.0 |
| 0xB8 | 184 |  18.6 |
| 0xB9 | 185 |  18.3 |
| 0xBA | 186 |  17.6 |
| 0xBB | 187 |  17.3 |
| 0xBC | 188 |  17.0 |
| 0xBD | 189 |  16.6 |
| 0xBE | 190 |  16.0 |
| 0xBF | 191 |  15.6 |
| 0xC0 | 192 |  15.3 |
| 0xC1 | 193 |  15.0 |
| 0xC2 | 194 |  14.3 |
| 0xC3 | 195 |  14.0 |
| 0xC4 | 196 |  13.3 |
| 0xC5 | 197 |  13.0 |
| 0xC6 | 198 |  12.3 |
| 0xC7 | 199 |  12.0 |
| 0xC8 | 200 |  11.3 |
| 0xC9 | 201 |  11.0 |
| 0xCA | 202 |  10.3 |
| 0xCB | 203 |  10.0 |
| 0xCC | 204 |   9.3 |
| 0xCD | 205 |   9.0 |
| 0xCE | 206 |   8.3 |
| 0xCF | 207 |   8.0 |
| 0xD0 | 208 |   7.3 |
| 0xD1 | 209 |   7.0 |
| 0xD2 | 210 |   6.3 |
| 0xD3 | 211 |   6.0 |
| 0xD4 | 212 |   5.3 |
| 0xD5 | 213 |   5.0 |
| 0xD6 | 214 |   4.3 |
| 0xD7 | 215 |   3.6 |
| 0xD8 | 216 |   3.0 |
| 0xD9 | 217 |   2.3 |
| 0xDA | 218 |   1.6 |
| 0xDB | 219 |   1.0 |
| 0xDC | 220 |   0.3 |
| 0xDD | 221 |   0.0 |
| 0xDE | 222 |   0.0 |
| 0xDF | 223 |   0.0 |
| 0xE0 | 224 |   0.0 |
| 0xE1 | 225 |   0.0 |
| 0xE2 | 226 |   0.0 |
| 0xE3 | 227 |   0.0 |
| 0xE4 | 228 |   0.0 |
| 0xE5 | 229 |   0.0 |
| 0xE6 | 230 |   0.0 |
| 0xE7 | 231 |   0.0 |
| 0xE8 | 232 |   0.0 |
| 0xE9 | 233 |   0.0 |
| 0xEA | 234 |   0.0 |
| 0xEB | 235 |   0.0 |
| 0xEC | 236 |   0.0 |
| 0xED | 237 |   0.0 |
| 0xEE | 238 |   0.0 |
| 0xEF | 239 |   0.0 |
| 0xF0 | 240 |   0.0 |
| 0xF1 | 241 |   0.0 |
| 0xF2 | 242 |   0.0 |
| 0xF3 | 243 |   0.0 |
| 0xF4 | 244 |   0.0 |
| 0xF5 | 245 |   0.0 |
| 0xF6 | 246 |   0.0 |
| 0xF7 | 247 |   0.0 |
| 0xF8 | 248 |   0.0 |
| 0xF9 | 249 |   0.0 |
| 0xFA | 250 |   0.0 |
| 0xFB | 251 |   0.0 |
| 0xFC | 252 |  20.0 |
| 0xFD | 253 |  20.0 |
| 0xFE | 254 |  20.0 |
| 0xFF | 255 |  20.0 |

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
