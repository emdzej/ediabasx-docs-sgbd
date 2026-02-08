# IHKARR.prg

- Jobs: [168](#jobs)
- Tables: [17](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Klimasteuergeraet IHKA RR |
| ORIGIN | BMW L5-W-3 Holzner |
| REVISION | 3.00 |
| AUTHOR | Preh 1713 Fuchs, Voll |
| COMMENT | SGBD IHKA RR Stand KW47/05 |
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
- [STATUS_ANALOGEINGAENGE](#job-status-analogeingaenge) - Auslesen der 44 A/D-Werte + 2 CAN-Signale KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_REGLERGROESSEN](#job-status-reglergroessen) - Auslesen der 28 Byte Reglerinformationene KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_BEDIENTEIL](#job-status-bedienteil) - Auslesen der 8 Ports KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_IO](#job-status-io) - Auslesen der Controller-Ports KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - Auslesen der 14 (mit Fondklima: 18) Klappenpositionen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_TRANSPORTMODE](#job-status-transportmode) - Auslesen der 2 Bytes Transportmode KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_FZE](#job-status-fze) - Auslesen der Stati der Filterzustandserkennung(FZE) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_SICHERHEITSFAHRZEUG](#job-status-sicherheitsfahrzeug) - Auslesen des Stauts Sicherheitsfahrzeug KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_ZUSATZLUEFTER_STUFE](#job-status-zusatzluefter-stufe) - Auslesen der Stufe des Zusatzluefters KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_BOOT_SW_VERSION](#job-status-boot-sw-version) - Auslesen der Boot-SW-Version KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_AUC_SENSOR](#job-status-auc-sensor) - Auslesen der AUC-Sensor-Version KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_MOTOR_FEHLER](#job-status-motor-fehler) - Auslesen der Schrittmotoren-Fehler KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_CAR_GEBL_OFFSET](#job-status-car-gebl-offset) - Auslesen des Geblaese-Offsets Car-Memory KWP2000: $21 ReadDataByLocalIdentifier $02 Status Geblaese-Offset Modus  : Default
- [STEUERN_CAR_GEBLAESE_OFFSET](#job-steuern-car-geblaese-offset) - Setzen des Geblaese-Offsets KWP2000: $3B WriteDataByLocalIdentifier $02 Geblaese-Offset Modus  : Default
- [STATUS_CAR_TEMP_OFFSET](#job-status-car-temp-offset) - Auslesen des Temperatur-Offsets Car-Memory KWP2000: $21 ReadDataByLocalIdentifier $03 Status Temperatur-Offset Modus  : Default
- [STEUERN_CAR_TEMPERATUR_OFFSET](#job-steuern-car-temperatur-offset) - Setzen des Temperatur-Offsets KWP2000: $3B WriteDataByLocalIdentifier $03 Temperatur-Offset Modus  : Default
- [STATUS_CAR_DEFAULT_KEY](#job-status-car-default-key) - Auslesen, ob der Default-Key gesetzt ist KWP2000: $21 InputOutputControlByLocalIdentifier $04 ReportCurrentState Modus  : Default
- [STEUERN_CAR_DEFAULT_KEY](#job-steuern-car-default-key) - KWP2000: $3B WriteDataByLocalIdentifier $04 Default-Key setzen Modus  : Default
- [STATUS_KEY_FAHRER](#job-status-key-fahrer) - Auslesen des Fahrers Key-Memory KWP2000: $21 ReadDataByLocalIdentifier $01 Aktuell eingestellten Fahrer auslesen Modus  : Default
- [STATUS_KEY_AUTO_NEUSTART](#job-status-key-auto-neustart) - Auslesen, ob Auto-Funktion immer EIN nach Reset KWP2000: $22 ReadDataByCommonIdentifier $24 + Argument Fahrer Modus  : Default
- [STEUERN_KEY_AUTO_NEUSTART](#job-steuern-key-auto-neustart) - KWP2000: $2E WriteDataByCommonIdentifier $24 + Argument Fahrer Modus  : Default
- [STATUS_KEY_KLIMA_NEUSTART](#job-status-key-klima-neustart) - Auslesen, ob Klima-Funktion immer EIN nach Reset KWP2000: $22 ReadDataByCommonIdentifier $24 + Argument Fahrer Modus  : Default
- [STEUERN_KEY_KLIMA_NEUSTART](#job-steuern-key-klima-neustart) - KWP2000: $2E WriteDataByCommonIdentifier $24 + Argument Fahrer Modus  : Default
- [DIAGNOSE_TESTBIT](#job-diagnose-testbit) - Ansteuern des Diagnosetest-Bits Das Bit kann ein- bzw. ausgeschaltet werden.
- [STEUERN_WASSERPUMPE](#job-steuern-wasserpumpe) - Ansteuern der Wasserpumpe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_WISCHERABLAGENHEIZUNG](#job-steuern-wischerablagenheizung) - Ansteuern der Wischerablagenheizung im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_WASSERVENTIL_LINKS](#job-steuern-wasserventil-links) - Ansteuern des linken Wasserventils im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_WASSERVENTIL_RECHTS](#job-steuern-wasserventil-rechts) - Ansteuern des rechten Wasserventils im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KAELTEMITTELVERDICHTER](#job-steuern-kaeltemittelverdichter) - Ansteuern des Kaeltemittelverdichters im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_GEBLAESE](#job-steuern-geblaese) - Ansteuern des Geblaeses im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_ZUSATZLUEFTER](#job-steuern-zusatzluefter) - Ansteuern des Zusatzluefters im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_WARMLUFT_LINKS](#job-steuern-klappe-warmluft-links) - Ansteuern der Warmluftklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_WARMLUFT_RECHTS](#job-steuern-klappe-warmluft-rechts) - Ansteuern der Warmluftklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_UMLUFT](#job-steuern-klappe-umluft) - Ansteuern der Umluftklappe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_ENTFROSTUNG](#job-steuern-klappe-entfrostung) - Ansteuern der Entfrostungsklappe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FUSSRAUM_LINKS](#job-steuern-klappe-fussraum-links) - Ansteuern der Fussraumklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FUSSRAUM_RECHTS](#job-steuern-klappe-fussraum-rechts) - Ansteuern der Fussraumklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_KALTLUFT_LINKS](#job-steuern-klappe-kaltluft-links) - Ansteuern der Kaltluftklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_KALTLUFT_RECHTS](#job-steuern-klappe-kaltluft-rechts) - Ansteuern der Kaltluftklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FONDRAUM_LINKS](#job-steuern-klappe-fondraum-links) - Ansteuern der Fondraumklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FONDRAUM_RECHTS](#job-steuern-klappe-fondraum-rechts) - Ansteuern der Fondraumklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FRISCHLUFT](#job-steuern-klappe-frischluft) - Ansteuern der Frischluftklappe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_REGLERGROESSE_Y_LINKS](#job-steuern-reglergroesse-y-links) - Steuern der Reglergroesse links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_REGLERGROESSE_Y_RECHTS](#job-steuern-reglergroesse-y-rechts) - Steuern der Reglergroesse rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KOMPRESSOR_EINLAUFSCHUTZ](#job-steuern-kompressor-einlaufschutz) - Steuern des Kompressoreinlaufschutzes KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_TRANSPORTMODE](#job-steuern-transportmode) - Steuern des Transportmodes im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_MOTOREN_EICHLAUF](#job-steuern-motoren-eichlauf) - Motoren-Eichlauf aktivieren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STATUS_HKZ_AGGREGATE_ABSCHALTUNG_PM](#job-status-hkz-aggregate-abschaltung-pm) - Auslesen der Zaehler fuer Abschaltung HHS, WABL, Geblaese wg. Priostufe KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_HKZ_MOTOR_ANTWORTET_NICHT](#job-status-hkz-motor-antwortet-nicht) - Auslesen des Haefigkeitszaehlers Motor antwortet nicht KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_HKZ_MOTOR_BLOCKIERUNG](#job-status-hkz-motor-blockierung) - Auslesen des Haefigkeitszaehlers Motor-Blockierung KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_HKZ_MOTOR_INTERNER_FEHLER](#job-status-hkz-motor-interner-fehler) - Auslesen des Haefigkeitszaehlers Motor-Blockierung KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_HKZ_GEBLAESE_ANTWORTET_NICHT](#job-status-hkz-geblaese-antwortet-nicht) - Auslesen des Haefigkeitszaehlers Motor antwortet nicht KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_USPG_STANDHEIZEN_ZAEHLER](#job-status-uspg-standheizen-zaehler) - Auslesen des Unterspannungszaehlers SH KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_MOTOR_SUMME_SCHRITTANZAHL](#job-status-motor-summe-schrittanzahl) - Auslesen der kumulierten Motor-Schrittzahlen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_BS_TEMPERATUR_SENSOREN](#job-status-bs-temperatur-sensoren) - Auslesen der Betriebsstunden Temperatursensoren KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_WASSERVENTILE_LASTWECHSEL](#job-status-wasserventile-lastwechsel) - Auslesen der Zaehler fuer Wasserventil-Lastwechsel KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_BS_WASSERPUMPE](#job-status-bs-wasserpumpe) - Auslesen der Betriebsstunden Wasserpumpe KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_BS_KOMPRESSORVENTIL](#job-status-bs-kompressorventil) - Auslesen der Betriebsstunden Kompressorventil KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_BS_GEBLREGLER_LASTPROFIL](#job-status-bs-geblregler-lastprofil) - Auslesen der Status Geblaeseregler-Lastprofil KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_BS_DRUCKSENSOR](#job-status-bs-drucksensor) - Auslesen der Status Betriebsstunden Drucksensor KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_TINNEN_LUEFTER](#job-status-tinnen-luefter) - Auslesen der Status Innentemperatursensor Luefter KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_DRUCKSENSOR_MAX](#job-status-drucksensor-max) - Auslesen der Status Drucksensor Max-Druck KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_BS_PRIOSTUFEN](#job-status-bs-priostufen) - Auslesen der Status Stundenzaehler Priostufen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_INDIVIDUALISIERUNG](#job-status-individualisierung) - Auslesen der Status Individualisierung KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STEUERN_MOTOR_ANTWORTET_NICHT_LOESCHEN](#job-steuern-motor-antwortet-nicht-loeschen) - Zaehler fuer Motor antwortet nicht loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_MOTOR_BLOCKIERUNG_LOESCHEN](#job-steuern-motor-blockierung-loeschen) - Zaehler fuer Motor-Blockierung loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_MOTOR_INTERNER_FEHLER_LOESCHEN](#job-steuern-motor-interner-fehler-loeschen) - Zaehler fuer interne Motorfehler loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_GEBLAESE_ANTWORTET_NICHT_LOESCHEN](#job-steuern-geblaese-antwortet-nicht-loeschen) - Zaehler fuer Geblaese antwortet nicht loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_USPG_STANDHEIZEN_ZAEHLER_LOESCHEN](#job-steuern-uspg-standheizen-zaehler-loeschen) - Zaehler fuer Uspg Standheizen loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_MOTOR_SUMME_SCHRITTZAHLEN_LOESCHEN](#job-steuern-motor-summe-schrittzahlen-loeschen) - Zaehler fuer kumulierte Motorschrittzahlen loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_BS_TEMPERATUR_SENSOREN_LOESCHEN](#job-steuern-bs-temperatur-sensoren-loeschen) - BS Temperatursensoren loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_WASSERVENTILE_LASTWECHSEL_LOESCHEN](#job-steuern-wasserventile-lastwechsel-loeschen) - Zaehler fuer WV-Lastwechsel loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_BS_WASSERPUMPE_LOESCHEN](#job-steuern-bs-wasserpumpe-loeschen) - Zaehler fuer Wasserpumpe loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_BS_KOMPRESSORVENTIL_LOESCHEN](#job-steuern-bs-kompressorventil-loeschen) - Zaehler fuer Kompressorventil loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_GEBLREGLER_LASTPROFIL_LOESCHEN](#job-steuern-geblregler-lastprofil-loeschen) - Zaehler fuer Geblaeseregler-Lastprofil loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_BS_DRUCKSENSOR_LOESCHEN](#job-steuern-bs-drucksensor-loeschen) - Zaehler fuer Drucksensor loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_TINNEN_LUEFTER_LOESCHEN](#job-steuern-tinnen-luefter-loeschen) - Zaehler fuer Innenfuehlerluefter loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_DRUCKSENSOR_MAX_LOESCHEN](#job-steuern-drucksensor-max-loeschen) - Zaehler fuer max. Drucksensorwert loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_BS_PRIOSTUFEN_LOESCHEN](#job-steuern-bs-priostufen-loeschen) - Zaehler fuer Priostufen (PowerModul) loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_MUX4_KOMMUNIKATION](#job-steuern-mux4-kommunikation) - Sperren der MUX4-Kommunikation Die Sperre kann aktiviert( EIN )bzw. deaktiviert (AUS) werden
- [STEUERN_MOTOR_PROGRAMMIEREN](#job-steuern-motor-programmieren) - Programmieren von Schrittmotoren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_BEDIENTEIL_TASTEN](#job-steuern-bedienteil-tasten) - Simulieren von Tastenbetaetigungen am Bedienteil KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [ZWP_AKTIVIEREN](#job-zwp-aktivieren) - Aktivieren der Zusatzwasserpumpe (Setzen des Codierbits) KWP 2000: $23 ReadMemoryByAddress KWP 2000: $31 StartRoutineByLocalIdentifier KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [ZWP_DEAKTIVIEREN](#job-zwp-deaktivieren) - Deaktivieren der Zusatzwasserpumpe (Loeschen des Codierbits) KWP 2000: $23 ReadMemoryByAddress KWP 2000: $31 StartRoutineByLocalIdentifier KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [BOS_DATEN_LESEN](#job-bos-daten-lesen) - BOS Daten auslesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [BOS_RESET](#job-bos-reset) - BOS Daten Zurücksetzen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
- [STEUERN_POTI_KALIBRIERUNG_RR](#job-steuern-poti-kalibrierung-rr) - Starten der Kalibrierung fuer die 6 bei RR einzulernenden Potentiometer Vorgehen: 1. Kalibrierung starten (durch Aufruf dieses Jobs) (die 3 Funktions-LEDs beginnen zu blinken) 2. IHKA Geblaesesteller und alle Bedienelemente des Heckbedienteiles auf MIN stellen 3. UMLUFT-Taste der IHKA (linke Taste) druecken (die linke LED hoert auf zu blinken, wenn Linksanschlaege erfolgreich gelernt wurden) 4. IHKA Geblaesesteller und alle Bedienelemente des Heckbedienteiles auf MAX stellen 5. AC_OFF-Taste der IHKA (rechte Taste) betaetigen - FERTIG (die beiden rechten LEDs hoeren bei Erfolg nun auch auf zu blinken) gab es ein Problem beim Lernen, blinken die LEDs weiter 60sec nach Aktivierung des Jobs bzw. nach dem ersten Tastendruck wird das Lernen abgebrochen, wenn bis dahin nicht erfolgreich gelernt wurde. KWP2000: $30 InputOutputControlByLocalIdentifier $01 Modus  : Default Dieser Job lernt folgende Potis ein: (Namen aus dem Job STATUS_ANALOGAEINGAENGE) STAT_POTI_GEBL_LI_WERT         Geblaesedrehsteller vorne links STAT_POTI_GEBL_RE_WERT         Geblaesedrehsteller vorne rechts STAT_POTI_GEBL_FOND_LI_WERT    Geblaesedrehsteller hinten links STAT_POTI_GEBL_FOND_RE_WERT    Geblaesedrehsteller hinten rechts STAT_POTI_TEMP_FOND_LI_WERT    Temperaturraendel hinten links STAT_POTI_TEMP_FOND_RE_WERT    Temperaturraendel hinten rechts
- [STEUERN_POTI_KALIBRIERUNG_PREH](#job-steuern-poti-kalibrierung-preh) - Starten der Kalibrierung fuer die 5 IHKA Raendelraeder (Temp. und GBL Frontscheibe) Vorgehen: 1. Kalibrierung starten (mit diesem Job) (die drei Funktions-LEDs am Bedienteil beginnen zu blinken) 2. IHKA Raendelraeder in den Linksanschlag drehen 3. UMLUFT-Taste der IHKA betaetigen (linke Taste) (die linke LED hoert auf zu blinken, wenn die Linksanschlaege erfolgreich gelernt wurden.) 4. IHKA Raendelraeder in den Rechtsanschlag drehen 5. AC_OFF-Taste (auf der rechten Seite) betaetigen - FERTIG (die beiden rechten LEDs hoeren bei Erfolg nun auch auf zu blinken) gab es ein Problem beim Lernen, blinken die LEDs weiter 60sec nach Aktivierung des Jobs bzw. nach dem ersten Tastendruck wird das Lernen abgebrochen, wenn bis dahin nicht erfolgreich gelernt wurde. KWP2000: $30 InputOutputControlByLocalIdentifier $01 Modus  : Default Dieser Job lernt folgende Potis ein: (Namen aus dem Job STATUS_ANALOGAEINGAENGE) STAT_POTI_TEMP_LI_OBEN_WERT      Temperaturraendel links oben STAT_POTI_TEMP_LI_UNTEN_WERT     Temperaturraendel links unten STAT_POTI_SCHEIBENLUFT_WERT      Frontscheibenluftraendel STAT_POTI_TEMP_RE_OBEN_WERT      Temperaturraendel rechts oben STAT_POTI_TEMP_RE_UNTEN_WERT     Temperaturraendel rechts unten
- [STATUS_POTI_KALIBRIERUNG_RR](#job-status-poti-kalibrierung-rr) - Auslesen des Status der Kalibrierung der bei RR zu lernenden Potis Gibt nur beim ersten Lesen nach erfolgter Kalibrierung den Status zurueck, sonst Null KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_POTI_KALIBRIERUNG_PREH](#job-status-poti-kalibrierung-preh) - Auslesen des Status der Kalibrierung der bei Preh einzulernenden Potis Gibt nur beim ersten Lesen nach erfolgter Kalibrierung den Status zurueck, sonst Null KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STEUERN_KLAPPE_KUGELAUS_LINKS_AUSSEN](#job-steuern-klappe-kugelaus-links-aussen) - Ansteuern des Kugelausstroemers links aussen im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_KUGELAUS_LINKS_MITTE](#job-steuern-klappe-kugelaus-links-mitte) - Ansteuern des Kugelausstroemers links mitte im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_KNIEAUS_LINKS](#job-steuern-klappe-knieaus-links) - Ansteuern des Knieausstroemers links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_INDIREKTERAUS_LINKS](#job-steuern-klappe-indirekteraus-links) - Ansteuern des indirekten Ausstroemers links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_KUGELAUS_RECHTS_MITTE](#job-steuern-klappe-kugelaus-rechts-mitte) - Ansteuern des Kugelausstroemers rechts mitte im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_KUGELAUS_RECHTS_AUSSEN](#job-steuern-klappe-kugelaus-rechts-aussen) - Ansteuern des Kugelausstroemers rechts aussen im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_KNIEAUS_RECHTS](#job-steuern-klappe-knieaus-rechts) - Ansteuern des Knieausstroemers rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_INDIREKTERAUS_RECHTS](#job-steuern-klappe-indirekteraus-rechts) - Ansteuern des indirekten Ausstroemers rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_A_SAEULE_LINKS](#job-steuern-klappe-a-saeule-links) - Ansteuern des Ausstroemers an der A-Saeule links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_A_SAEULE_RECHTS](#job-steuern-klappe-a-saeule-rechts) - Ansteuern des Ausstroemers an der A-Saeule rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_B_SAEULE_LINKS](#job-steuern-klappe-b-saeule-links) - Ansteuern des Ausstroemers an der B-Saeule links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_MITTELKON_LINKS](#job-steuern-klappe-mittelkon-links) - Ansteuern des Ausstroemers an der Mittelkonsole links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_B_SAEULE_RECHTS](#job-steuern-klappe-b-saeule-rechts) - Ansteuern des Ausstroemers an der B-Saeule rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_MITTELKON_RECHTS](#job-steuern-klappe-mittelkon-rechts) - Ansteuern des Ausstroemers an der Mittelkonsole rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_FONDGEBLAESE_LINKS](#job-steuern-fondgeblaese-links) - Ansteuern des Fondgeblaese links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_FONDGEBLAESE_RECHTS](#job-steuern-fondgeblaese-rechts) - Ansteuern des Fondgeblaese rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_SEITENSCHEIBENHEIZUNG](#job-steuern-seitenscheibenheizung) - Ansteuern der Seitenscheibenheizung im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FOKL_B_LI](#job-steuern-klappe-fokl-b-li) - Ansteuern des Fondklima Klappenmoduls B-Saeule links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FOKL_MI_LI](#job-steuern-klappe-fokl-mi-li) - Ansteuern des Fondklima Klappenmoduls Mittelkonsole links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FOKL_B_RE](#job-steuern-klappe-fokl-b-re) - Ansteuern des Fondklima Klappenmoduls B-Saeule rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_KLAPPE_FOKL_MI_RE](#job-steuern-klappe-fokl-mi-re) - Ansteuern des Fondklima Klappenmoduls Mittelkonsole rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_FONDKLIMA_LI](#job-steuern-fondklima-li) - Ansteuern des Fondklimaausganges Links im Diagnosemode (Nur erlaubt, wenn Fondgeblaese nicht auf 0!) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_FONDKLIMA_RE](#job-steuern-fondklima-re) - Ansteuern des Fondklimaausganges Rechts im Diagnosemode (Nur erlaubt, wenn Fondgeblaese nicht auf 0!) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STATUS_BESCHLAG_SENSOR](#job-status-beschlag-sensor) - Auslesen des Status des Beschlagsensors KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_GERUCHSSTARTVERRIEGELUNG](#job-status-geruchsstartverriegelung) - Auslesen der Geruchsstartverriegelungsparameter KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STEUERN_GERUCHSSTARTVERRIEGELUNG](#job-steuern-geruchsstartverriegelung) - Parameter der Geruchsstartverriegelung setzen KWP2000: $30 InputOutputControlByLocalIdentifier $08 LongTermAdjustment Modus  : Default

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

Auslesen der 44 A/D-Werte + 2 CAN-Signale KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TINNEN_WERT | real | Innentemperaturfuehler |
| STAT_TINNEN_EINH | string | Grad Celsius |
| STAT_KMV_SENSE_WERT | int | Stromsense KMV |
| STAT_KMV_SENSE_EINH | string | Inkremente |
| STAT_WP_SENSE_WERT | int | Stromsense Wasserpumpe |
| STAT_WP_SENSE_EINH | string | Inkremente |
| STAT_DRUCK_UB_WERT | real | Versorgungsspannung Drucksensor |
| STAT_DRUCK_UB_EINH | string | Volt |
| STAT_UB_VOR_AUC_WERT | int | Versorgungsspannung vor AUC |
| STAT_UB_VOR_AUC_EINH | string | Volt |
| STAT_TREIBER_UB_SENSE_WERT | real | Stromsense Treiberversorgung |
| STAT_TREIBER_UB_SENSE_EINH | string | Volt |
| STAT_TEMP_FOND_LINKS_WERT | real | Fondtemperaturfuehler links |
| STAT_TEMP_FOND_LINKS_EINH | string | Grad Celsius |
| STAT_AUSSTROEM_POTI_5_WERT | real | Vorgabepoti Nr. 5 fuer Ausstroemerklappen |
| STAT_AUSSTROEM_POTI_5_EINH | string | Volt |
| STAT_TEMP_FOND_RECHTS_WERT | real | Fondtemperaturfuehler rechts |
| STAT_TEMP_FOND_RECHTS_EINH | string | Grad Celsius |
| STAT_AUSSTROEM_POTI_6_WERT | real | Vorgabepoti Nr. 6 fuer Ausstroemerklappen |
| STAT_AUSSTROEM_POTI_6_EINH | string | Volt |
| STAT_AUSSTROEM_HALLSENS_1_WERT | real | Hallsensor Nr. 1 fuer Ausstroemerklappen |
| STAT_AUSSTROEM_HALLSENS_1_EINH | string | Volt |
| STAT_AUSSTROEM_HALLSENS_2_WERT | real | Hallsensor Nr. 2 fuer Ausstroemerklappen |
| STAT_AUSSTROEM_HALLSENS_2_EINH | string | Volt |
| STAT_AUSSTROEM_POTI_3_WERT | real | Vorgabepoti Nr. 3 fuer Ausstroemerklappen |
| STAT_AUSSTROEM_POTI_3_EINH | string | Volt |
| STAT_AUSSTROEM_POTI_4_WERT | real | Vorgabepoti Nr. 4 fuer Ausstroemerklappen |
| STAT_AUSSTROEM_POTI_4_EINH | string | Volt |
| STAT_WT_RE_WERT | real | Waermetauscherfuehler rechts |
| STAT_WT_RE_EINH | string | Grad Celsius |
| STAT_WT_LI_WERT | real | Waermetauscherfuehler links |
| STAT_WT_LI_EINH | string | Grad Celsius |
| STAT_AUSSTROEM_POTI_8_WERT | real | Vorgabepoti Nr. 8 fuer Ausstroemerklappen |
| STAT_AUSSTROEM_POTI_8_EINH | string | Volt |
| STAT_TEMP_VERDAMFER_WERT | real | Verdampfertemperaturfuehler |
| STAT_TEMP_VERDAMFER_EINH | string | Grad Celsius |
| STAT_SCHICHTUNG_LI_WERT | real | Schichtungstemperatur links |
| STAT_SCHICHTUNG_LI_EINH | string | Grad Celsius |
| STAT_AUC_SENSOR_WERT | real | AUC-Sensor |
| STAT_AUC_SENSOR_EINH | string | Volt |
| STAT_SCHICHTUNG_RE_WERT | real | Schichtungstemperatur rechts |
| STAT_SCHICHTUNG_RE_EINH | string | Grad Celsius |
| STAT_MONI_SOL_BESCHL_UB_WERT | real | Monitor Sonnen-/Beschlagsensor-Versorgung |
| STAT_MONI_SOL_BESCHL_UB_EINH | string | Volt |
| STAT_POTI_TEMP_LI_UNTEN_WERT | real | Poti Temperatur links unten |
| STAT_POTI_TEMP_LI_UNTEN_EINH | string | Prozent |
| STAT_POTI_TEMP_LI_OBEN_WERT | real | Poti Temperatur links oben |
| STAT_POTI_TEMP_LI_OBEN_EINH | string | Prozent |
| STAT_POTI_GEBL_LI_WERT | int | Poti Geblaese links vorne |
| STAT_POTI_GEBL_LI_EINH | string | Stufe |
| STAT_POTI_GEBL_RE_WERT | int | Poti Geblaese rechts vorne |
| STAT_POTI_GEBL_RE_EINH | string | Stufe |
| STAT_MONI_AUC_UB_WERT | real | Monitor AUC-Versorgung |
| STAT_MONI_AUC_UB_EINH | string | Volt |
| STAT_LP_CODE_WERT | int | Leiterplattencode |
| STAT_LP_CODE_EINH | string | Inkremente |
| STAT_FONDRAUM_VERSORGUNG_WERT | real | 12V Spannungsversorgung fuer Fond |
| STAT_FONDRAUM_VERSORGUNG_EINH | string | Volt |
| STAT_POTI_TEMP_RE_UNTEN_WERT | real | Poti Temperatur rechts unten |
| STAT_POTI_TEMP_RE_UNTEN_EINH | string | Prozent |
| STAT_AUSSTROEM_POTI_7_WERT | real | Vorgabepoti Nr. 7 fuer Ausstroemerklappen |
| STAT_AUSSTROEM_POTI_7_EINH | string | Volt |
| STAT_MONI_USTEUER_FONDGBL_LI_WERT | real | Monitor Steuerspannung Fond-Geblaese links |
| STAT_MONI_USTEUER_FONDGBL_LI_EINH | string | Volt |
| STAT_POTI_TEMP_RE_OBEN_WERT | real | Poti Temperatur rechts oben |
| STAT_POTI_TEMP_RE_OBEN_EINH | string | Prozent |
| STAT_MONI_USTEUER_FONDGBL_RE_WERT | real | Monitor Steuerspannung Fond-Geblaese rechts |
| STAT_MONI_USTEUER_FONDGBL_RE_EINH | string | Volt |
| STAT_POTI_SCHEIBENLUFT_WERT | int | Poti Frontscheibenluft |
| STAT_POTI_SCHEIBENLUFT_EINH | string | Stufe |
| STAT_DRUCKSENSOR_WERT | real | Drucksensor |
| STAT_DRUCKSENSOR_EINH | string | bar |
| STAT_AUSSTROEM_POTI_2_WERT | real | Vorgabepoti Nr. 2 fuer Ausstroemerklappen |
| STAT_AUSSTROEM_POTI_2_EINH | string | Volt |
| STAT_SOLARSENSOR_LI_WERT | real | Solarsensor links |
| STAT_SOLARSENSOR_LI_EINH | string | W/m2 |
| STAT_AUSSTROEM_POTI_1_WERT | real | Vorgabepoti Nr. 1 fuer Ausstroemerklappen |
| STAT_AUSSTROEM_POTI_1_EINH | string | Volt |
| STAT_SOLARSENSOR_RE_WERT | real | Solarsensor |
| STAT_SOLARSENSOR_RE_EINH | string | W/m2 |
| STAT_POTI_GEBL_FOND_LI_WERT | real | Geblaesepoti Fondraum links |
| STAT_POTI_GEBL_FOND_LI_EINH | string | Volt |
| STAT_POTI_TEMP_FOND_LI_WERT | int | Fondraum Temperaturpoti links |
| STAT_POTI_TEMP_FOND_LI_EINH | string | Volt |
| STAT_POTI_GEBL_FOND_RE_WERT | real | Geblaesepoti Fondraum rechts |
| STAT_POTI_GEBL_FOND_RE_EINH | string | Volt |
| STAT_POTI_TEMP_FOND_RE_WERT | int | Fondraum Temperaturpoti rechts |
| STAT_POTI_TEMP_FOND_RE_EINH | string | Volt |
| STAT_TAUSSEN_WERT | real | Aussentemperatur |
| STAT_TAUSSEN_EINH | string | Grad Celsius |
| STAT_TKUEHLERWASSER_WERT | int | Kuehlwassertemperatur |
| STAT_TKUEHLERWASSER_EINH | string | Grad Celsius |
| STAT_STUFE_GEBL_FOND_LI_WERT | int | Sollansteuerung Geblaese Fondraum links |
| STAT_STUFE_GEBL_FOND_LI_EINH | string | Inkremente |
| STAT_STUFE_GEBL_FOND_RE_WERT | int | Sollansteuerung Geblaese Fondraum links |
| STAT_STUFE_GEBL_FOND_RE_EINH | string | Inkremente |
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
| STAT_FUEHR_LI_WERT | int |  |
| STAT_FUEHR_LI_EINH | string | % |
| STAT_FUEHR_RE_WERT | int |  |
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

Auslesen der 8 Ports KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_POTI_TEMP_LI_WERT | real |  |
| STAT_POTI_TEMP_LI_EINH | string | Grad Celsius |
| STAT_POTI_TEMP_RE_WERT | real |  |
| STAT_POTI_TEMP_RE_EINH | string | Grad Celsius |
| STAT_POTI_GEBL_LI_WERT | int |  |
| STAT_POTI_GEBL_LI_EINH | string | Stufen |
| STAT_POTI_GEBL_RE_WERT | int |  |
| STAT_POTI_GEBL_RE_EINH | string | Stufen |
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
| STAT_KLAPPEN_AUTO_FA_EIN | int |  |
| STAT_GEBLAESE_AUTO_FA_EIN | int |  |
| STAT_INDIVIDUAL_FA_EIN | int |  |
| STAT_KEIN_PRG_FA_EIN | int |  |
| STAT_OBEN_HEAT_FA_EIN | int |  |
| STAT_MITTE_VENT_FA_EIN | int |  |
| STAT_UNTEN_FLOOR_FA_EIN | int |  |
| STAT_BILEVEL_FA_EIN | int |  |
| STAT_KLAPPEN_AUTO_BF_EIN | int |  |
| STAT_GEBLAESE_AUTO_BF_EIN | int |  |
| STAT_INDIVIDUAL_BF_EIN | int |  |
| STAT_KEIN_PRG_BF_EIN | int |  |
| STAT_OBEN_HEAT_BF_EIN | int |  |
| STAT_MITTE_VENT_BF_EIN | int |  |
| STAT_UNTEN_FLOOR_BF_EIN | int |  |
| STAT_BILEVEL_BF_EIN | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-io"></a>
### STATUS_IO

Auslesen der Controller-Ports KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WASSERVENTIL_LI_EIN | int |  |
| STAT_WASSERVENTIL_RE_EIN | int |  |
| STAT_ZUSATZWASSERPUMPE_EIN | int |  |
| STAT_SEITENSCHEIBENHEIZUNG_EIN | int |  |
| STAT_SH_LED_BLINKEN_EIN | int |  |
| STAT_AUC_HZG_VERSORGUNG_EIN | int |  |
| STAT_SELBSTHALTUNG_SLEEP_EIN | int |  |
| STAT_TREIBERVERSORGUNG_BUSSE_EIN | int |  |
| STAT_WISCHERABLAGENHEIZUNG_EIN | int |  |
| STAT_AUC_PARAGON_PWM_EIN | int |  |
| STAT_SH_LED_OFF_EIN | int |  |
| STAT_ANSTEUERUNG_KMV_WERT | int | Ansteuerung KMV-PWM |
| STAT_ANSTEUERUNG_KMV_EINH | string | % |
| STAT_12V_VERSORGUNG_FOND_EIN | int |  |
| STAT_TASTE_UML_NICHT_GEDRUECKT | int |  |
| STAT_TASTE_HHS_NICHT_GEDRUECKT | int |  |
| STAT_TASTE_ACOFF_NICHT_GEDRUECKT | int |  |
| STAT_VERSORGUNG_MUX4BC_EIN | int |  |
| STAT_ANSTEUERUNG_FONDKLIMA_LINKS_EIN | int |  |
| STAT_ANSTEUERUNG_FONDKLIMA_RECHTS_EIN | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-klappenposition"></a>
### STATUS_MOTOR_KLAPPENPOSITION

Auslesen der 14 (mit Fondklima: 18) Klappenpositionen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WARMLUFT_LI_WERT | int |  |
| STAT_WARMLUFT_LI_EINH | string | % Klappenposition in % |
| STAT_WARMLUFT_RE_WERT | int |  |
| STAT_WARMLUFT_RE_EINH | string | % Klappenposition in % |
| STAT_UMLUFT_WERT | int |  |
| STAT_UMLUFT_EINH | string | % Klappenposition in % |
| STAT_ENTFROSTUNG_WERT | int |  |
| STAT_ENTFROSTUNG_EINH | string | % Klappenposition in % |
| STAT_FUSSRAUM_LI_WERT | int |  |
| STAT_FUSSRAUM_LI_EINH | string | % Klappenposition in % |
| STAT_FUSSRAUM_RE_WERT | int |  |
| STAT_FUSSRAUM_RE_EINH | string | % Klappenposition in % |
| STAT_KALTLUFT_LI_WERT | int |  |
| STAT_KALTLUFT_LI_EINH | string | % Klappenposition in % |
| STAT_KALTLUFT_RE_WERT | int |  |
| STAT_KALTLUFT_RE_EINH | string | % Klappenposition in % |
| STAT_FONDRAUM_LI_WERT | int |  |
| STAT_FONDRAUM_LI_EINH | string | % Klappenposition in % |
| STAT_FONDRAUM_RE_WERT | int |  |
| STAT_FONDRAUM_RE_EINH | string | % Klappenposition in % |
| STAT_VIRTUELL_LI_WERT | int |  |
| STAT_VIRTUELL_LI_EINH | string | % Klappenposition in % |
| STAT_VIRTUELL_RE_WERT | int |  |
| STAT_VIRTUELL_RE_EINH | string | % Klappenposition in % |
| STAT_FRISCHLUFT_WERT | int |  |
| STAT_FRISCHLUFT_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_KUGELAUS_LINKS_AUSSEN_WERT | int |  |
| STAT_KLAPPE_KUGELAUS_LINKS_AUSSEN_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_KUGELAUS_LINKS_MITTE_WERT | int |  |
| STAT_KLAPPE_KUGELAUS_LINKS_MITTE_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_KNIEAUS_LINKS_WERT | int |  |
| STAT_KLAPPE_KNIEAUS_LINKS_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_INDIREKTERAUS_LINKS_WERT | int |  |
| STAT_KLAPPE_INDIREKTERAUS_LINKS_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_KUGELAUS_RECHTS_MITTE_WERT | int |  |
| STAT_KLAPPE_KUGELAUS_RECHTS_MITTE_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_KUGELAUS_RECHTS_AUSSEN_WERT | int |  |
| STAT_KLAPPE_KUGELAUS_RECHTS_AUSSEN_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_KNIEAUS_RECHTS_WERT | int |  |
| STAT_KLAPPE_KNIEAUS_RECHTS_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_INDIREKTERAUS_RECHTS_WERT | int |  |
| STAT_KLAPPE_INDIREKTERAUS_RECHTS_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_A_SAEULE_LINKS_WERT | int |  |
| STAT_KLAPPE_A_SAEULE_LINKS_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_A_SAEULE_RECHTS_WERT | int |  |
| STAT_KLAPPE_A_SAEULE_RECHTS_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_B_SAEULE_LINKS_WERT | int |  |
| STAT_KLAPPE_B_SAEULE_LINKS_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_MITTELKON_LINKS_WERT | int |  |
| STAT_KLAPPE_MITTELKON_LINKS_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_B_SAEULE_RECHTS_WERT | int |  |
| STAT_KLAPPE_B_SAEULE_RECHTS_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_MITTELKON_RECHTS_WERT | int |  |
| STAT_KLAPPE_MITTELKON_RECHTS_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_FOKL_B_LI_WERT | int |  |
| STAT_KLAPPE_FOKL_B_LI_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_FOKL_MI_LI_WERT | int |  |
| STAT_KLAPPE_FOKL_MI_LI_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_FOKL_B_RE_WERT | int |  |
| STAT_KLAPPE_FOKL_B_RE_EINH | string | % Klappenposition in % |
| STAT_KLAPPE_FOKL_MI_RE_WERT | int |  |
| STAT_KLAPPE_FOKL_MI_RE_EINH | string | % Klappenposition in % |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-transportmode"></a>
### STATUS_TRANSPORTMODE

Auslesen der 2 Bytes Transportmode KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TRANSPORTMODE_BYTE1_WERT | int |  |
| STAT_TRANSPORTMODE_BYTE1_EINH | string | Wert |
| STAT_TRANSPORTMODE_BYTE2_WERT | int |  |
| STAT_TRANSPORTMODE_BYTE2_EINH | string | Wert |
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

<a id="job-status-sicherheitsfahrzeug"></a>
### STATUS_SICHERHEITSFAHRZEUG

Auslesen des Stauts Sicherheitsfahrzeug KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SICHERHEITS_FZG | int |  |
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

<a id="job-status-auc-sensor"></a>
### STATUS_AUC_SENSOR

Auslesen der AUC-Sensor-Version KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MELDUNG | string | Meldung bei falscher SW-Nr. |
| STAT_AUC_SENSOR_WERT | int | 0 = noch kein Sensor erkannt, 1 = AUC-SensorI erkannt, 2 = AUC-SensorII erkannt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-fehler"></a>
### STATUS_MOTOR_FEHLER

Auslesen der Schrittmotoren-Fehler KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANTWORT_FEHLT_WERT | int |  |
| STAT_INTERNER_FEHLER_WERT | int |  |
| STAT_BLOCKIERUNG_WERT | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-car-gebl-offset"></a>
### STATUS_CAR_GEBL_OFFSET

Auslesen des Geblaese-Offsets Car-Memory KWP2000: $21 ReadDataByLocalIdentifier $02 Status Geblaese-Offset Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT 0 = kein Offset, 1 = Geblaese-Offset 10%, 3 = Geblaese-Offset -10% |
| STAT_CAR_GEBLAESE_OFFSET_WERT | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-car-geblaese-offset"></a>
### STEUERN_CAR_GEBLAESE_OFFSET

Setzen des Geblaese-Offsets KWP2000: $3B WriteDataByLocalIdentifier $02 Geblaese-Offset Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GEBLAESE_OFFSET_WERT | int | Geblaese-Offset: 0 = Kein Offset, 1 = +10 % Offset, 3 = -10% Offset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-car-temp-offset"></a>
### STATUS_CAR_TEMP_OFFSET

Auslesen des Temperatur-Offsets Car-Memory KWP2000: $21 ReadDataByLocalIdentifier $03 Status Temperatur-Offset Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPERATUR_OFFSET_WERT | int | Temperatur-Offset: 0 = Kein Offset Temperatur-Offset: 1 = Plus 1 Kelvin, 2 = Plus 2 Kelvin, 3 = Plus 3 Kelvin Temperatur-Offset: 5 = Minus 1 Kelvin, 6 = Minus 2 Kelvin, 7 = Minus 3 Kelvin |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-car-temperatur-offset"></a>
### STEUERN_CAR_TEMPERATUR_OFFSET

Setzen des Temperatur-Offsets KWP2000: $3B WriteDataByLocalIdentifier $03 Temperatur-Offset Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPERATUR_OFFSET_WERT | int | Temperatur-Offset: 0 = Kein Offset Temperatur-Offset: 1 = Plus 1 Kelvin, 2 = Plus 2 Kelvin, 3 = Plus 3 Kelvin Temperatur-Offset: 5 = Minus 1 Kelvin, 6 = Minus 2 Kelvin, 7 = Minus 3 Kelvin |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-car-default-key"></a>
### STATUS_CAR_DEFAULT_KEY

Auslesen, ob der Default-Key gesetzt ist KWP2000: $21 InputOutputControlByLocalIdentifier $04 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CAR_DEFAULT_KEY | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-car-default-key"></a>
### STEUERN_CAR_DEFAULT_KEY

KWP2000: $3B WriteDataByLocalIdentifier $04 Default-Key setzen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DEFAULT_KEY | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-key-fahrer"></a>
### STATUS_KEY_FAHRER

Auslesen des Fahrers Key-Memory KWP2000: $21 ReadDataByLocalIdentifier $01 Aktuell eingestellten Fahrer auslesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KEY_FAHRER_WERT | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-key-auto-neustart"></a>
### STATUS_KEY_AUTO_NEUSTART

Auslesen, ob Auto-Funktion immer EIN nach Reset KWP2000: $22 ReadDataByCommonIdentifier $24 + Argument Fahrer Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEY_FAHRER | int | Fahrerwahl 0x00 = Fahrer 1, 0x10 = Fahrer 2, 0x20 = Fahrer 3, 0x40 = Fahrer 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KEY_AUTO_NEUSTART | int | 1 = Auto nach Neustart aktiv, 0 = Auto nach Neustart nicht aktiv |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-key-auto-neustart"></a>
### STEUERN_KEY_AUTO_NEUSTART

KWP2000: $2E WriteDataByCommonIdentifier $24 + Argument Fahrer Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUTO_KEY | string | 'EIN','AUS' table DigitalArgument TEXT |
| FAHRER | int | Fahrerwahl 0x00 = Fahrer 1, 0x10 = Fahrer 2, 0x20 = Fahrer 3, 0x40 = Fahrer 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-key-klima-neustart"></a>
### STATUS_KEY_KLIMA_NEUSTART

Auslesen, ob Klima-Funktion immer EIN nach Reset KWP2000: $22 ReadDataByCommonIdentifier $24 + Argument Fahrer Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEY_FAHRER | int | Fahrerwahl 0x00 = Fahrer 1, 0x10 = Fahrer 2, 0x20 = Fahrer 3, 0x40 = Fahrer 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KEY_KLIMA_NEUSTART | int | 1 = Klima nach Neustart aktiv, 0 = Klima nach Neustart nicht aktiv |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-key-klima-neustart"></a>
### STEUERN_KEY_KLIMA_NEUSTART

KWP2000: $2E WriteDataByCommonIdentifier $24 + Argument Fahrer Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLIMA_KEY | string | 'EIN','AUS' table DigitalArgument TEXT |
| FAHRER | int | Fahrerwahl 0x00 = Fahrer 1, 0x10 = Fahrer 2, 0x20 = Fahrer 3, 0x40 = Fahrer 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

<a id="job-steuern-wischerablagenheizung"></a>
### STEUERN_WISCHERABLAGENHEIZUNG

Ansteuern der Wischerablagenheizung im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WISCHERABLAGE | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wasserventil-links"></a>
### STEUERN_WASSERVENTIL_LINKS

Ansteuern des linken Wasserventils im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

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

<a id="job-steuern-klappe-warmluft-links"></a>
### STEUERN_KLAPPE_WARMLUFT_LINKS

Ansteuern der Warmluftklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_WARMLUFT_LINKS | int | Klappenansteuerung KLAPPE_WARMLUFT_LINKS in Prozentschritten 0-100 % Motoradresse 0x11 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-warmluft-rechts"></a>
### STEUERN_KLAPPE_WARMLUFT_RECHTS

Ansteuern der Warmluftklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_WARMLUFT_RECHTS | int | Klappenansteuerung KLAPPE_WARMLUFT_RECHTS in Prozentschritten 0-100 % Motoradresse 0x12 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-umluft"></a>
### STEUERN_KLAPPE_UMLUFT

Ansteuern der Umluftklappe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_UMLUFT | int | Klappenansteuerung KLAPPE_UMLUFT in Prozentschritten 0-100 % Motoradresse 0x13 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-entfrostung"></a>
### STEUERN_KLAPPE_ENTFROSTUNG

Ansteuern der Entfrostungsklappe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_ENTFROSTUNG | int | Klappenansteuerung KLAPPE_ENTFROSTUNG in Prozentschritten 0-100 % Motoradresse 0x14 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fussraum-links"></a>
### STEUERN_KLAPPE_FUSSRAUM_LINKS

Ansteuern der Fussraumklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FUSSRAUM_LINKS | int | Klappenansteuerung KLAPPE_FUSSRAUM_LINKS in Prozentschritten 0-100 % Motoradresse 0x15 |

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
| KLAPPE_FUSSRAUM_RECHTS | int | Klappenansteuerung KLAPPE_FUSSRAUM_RECHTS in Prozentschritten 0-100 % Motoradresse 0x16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-kaltluft-links"></a>
### STEUERN_KLAPPE_KALTLUFT_LINKS

Ansteuern der Kaltluftklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_KALTLUFT_LINKS | int | Klappenansteuerung KLAPPE_KALTLUFT_LINKS in Prozentschritten 0-100 % Motoradresse 0x17 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-kaltluft-rechts"></a>
### STEUERN_KLAPPE_KALTLUFT_RECHTS

Ansteuern der Kaltluftklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_KALTLUFT_RECHTS | int | Klappenansteuerung KLAPPE_KALTLUFT_RECHTS in Prozentschritten 0-100 % Motoradresse 0x18 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fondraum-links"></a>
### STEUERN_KLAPPE_FONDRAUM_LINKS

Ansteuern der Fondraumklappe links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FONDRAUM_LINKS | int | Klappenansteuerung KLAPPE_FONDRAUM_LINKS in Prozentschritten 0-100 % Motoradresse 0x19 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fondraum-rechts"></a>
### STEUERN_KLAPPE_FONDRAUM_RECHTS

Ansteuern der Fondraumklappe rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FONDRAUM_RECHTS | int | Klappenansteuerung KLAPPE_FONDRAUM_RECHTS in Prozentschritten 0-100 % Motoradresse 0x1A |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-frischluft"></a>
### STEUERN_KLAPPE_FRISCHLUFT

Ansteuern der Frischluftklappe im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FRISCHLUFT | int | Klappenansteuerung KLAPPE_FRISCHLUFT in Prozentschritten 0-100 % |

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

<a id="job-steuern-transportmode"></a>
### STEUERN_TRANSPORTMODE

Steuern des Transportmodes im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |

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

<a id="job-status-hkz-aggregate-abschaltung-pm"></a>
### STATUS_HKZ_AGGREGATE_ABSCHALTUNG_PM

Auslesen der Zaehler fuer Abschaltung HHS, WABL, Geblaese wg. Priostufe KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HHS_ABSCHALTUNG_PM_WERT | unsigned char |  |
| STAT_HHS_ABSCHALTUNG_PM_EINH | string | Inkremente |
| STAT_WABL_ABSCHALTUNG_PM_WERT | unsigned char |  |
| STAT_WABL_ABSCHALTUNG_PM_EINH | string | Inkremente |
| STAT_GEBL_ABSCHALTUNG_PM_WERT | unsigned char |  |
| STAT_GEBL_ABSCHALTUNG_PM_EINH | string | Inkremente |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hkz-motor-antwortet-nicht"></a>
### STATUS_HKZ_MOTOR_ANTWORTET_NICHT

Auslesen des Haefigkeitszaehlers Motor antwortet nicht KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZAEHLER_MOTOR_ANTWORTET_NICHT_WERT | int |  |
| STAT_ZAEHLER_MOTOR_ANTWORTET_NICHT_EINH | string | Inkremente |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hkz-motor-blockierung"></a>
### STATUS_HKZ_MOTOR_BLOCKIERUNG

Auslesen des Haefigkeitszaehlers Motor-Blockierung KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZAEHLER_WARMLUFT_MOTOR_LI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_WARMLUFT_MOTOR_LI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_WARMLUFT_MOTOR_RE_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_WARMLUFT_MOTOR_RE_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_UMLUFT_MOTOR_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_UMLUFT_MOTOR_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_ENTFROSTUNG_MOTOR_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_ENTFROSTUNG_MOTOR_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_FUSSRAUM_MOTOR_LI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_FUSSRAUM_MOTOR_LI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_FUSSRAUM_MOTOR_RE_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_FUSSRAUM_MOTOR_RE_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_KALTLUFT_MOTOR_LI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_KALTLUFT_MOTOR_LI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_KALTLUFT_MOTOR_RE_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_KALTLUFT_MOTOR_RE_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_FONDBEL_MOTOR_LI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_FONDBEL_MOTOR_LI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_FONDBEL_MOTOR_RE_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_FONDBEL_MOTOR_RE_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_KUGELAUS_MOTOR_LI_AU_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_KUGELAUS_MOTOR_LI_AU_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_KUGELAUS_MOTOR_LI_MI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_KUGELAUS_MOTOR_LI_MI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_KNIEAUS_MOTOR_LI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_KNIEAUS_MOTOR_LI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_INDAUS_MOTOR_LI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_INDAUS_MOTOR_LI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_KUGELAUS_MOTOR_RE_MI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_KUGELAUS_MOTOR_RE_MI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_KUGELAUS_MOTOR_RE_AU_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_KUGELAUS_MOTOR_RE_AU_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_KNIEAUS_MOTOR_RE_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_KNIEAUS_MOTOR_RE_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_INDAUS_MOTOR_RE_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_INDAUS_MOTOR_RE_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_A_SAEULE_MOTOR_LI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_A_SAEULE_MOTOR_LI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_A_SAEULE_MOTOR_RE_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_A_SAEULE_MOTOR_RE_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_B_SAEULE_MOTOR_LI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_B_SAEULE_MOTOR_LI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_MIKON_MOTOR_LI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_MIKON_MOTOR_LI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_B_SAEULE_MOTOR_RE_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_B_SAEULE_MOTOR_RE_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_MIKON_MOTOR_RE_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_MIKON_MOTOR_RE_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_FOKL_B_LI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_FOKL_B_LI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_FOKL_MI_LI_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_FOKL_MI_LI_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_FOKL_B_RE_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_FOKL_B_RE_BLOCKIERUNG_EINH | string | Inkremente |
| STAT_ZAEHLER_FOKL_MI_RE_BLOCKIERUNG_WERT | int |  |
| STAT_ZAEHLER_FOKL_MI_RE_BLOCKIERUNG_EINH | string | Inkremente |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hkz-motor-interner-fehler"></a>
### STATUS_HKZ_MOTOR_INTERNER_FEHLER

Auslesen des Haefigkeitszaehlers Motor-Blockierung KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZAEHLER_MOTOR_INTERNER_FEHLER_WERT | int |  |
| STAT_ZAEHLER_MOTOR_INTERNER_FEHLER_EINH | string | Inkremente |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hkz-geblaese-antwortet-nicht"></a>
### STATUS_HKZ_GEBLAESE_ANTWORTET_NICHT

Auslesen des Haefigkeitszaehlers Motor antwortet nicht KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZAEHLER_GEBLAESE_ANTWORTET_NICHT_WERT | int |  |
| STAT_ZAEHLER_GEBLAESE_ANTWORTET_NICHT_EINH | string | Inkremente |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-uspg-standheizen-zaehler"></a>
### STATUS_USPG_STANDHEIZEN_ZAEHLER

Auslesen des Unterspannungszaehlers SH KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZAEHLER_USPG_SH_WERT | int |  |
| STAT_ZAEHLER_USPG_SH_EINH | string | Inkremente |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-summe-schrittanzahl"></a>
### STATUS_MOTOR_SUMME_SCHRITTANZAHL

Auslesen der kumulierten Motor-Schrittzahlen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHRITTZAHL_WARMLUFT_MOTOR_LI_WERT | unsigned long |  |
| STAT_SCHRITTZAHL_WARMLUFT_MOTOR_LI_EINH | string | 1000 Inkremente |
| STAT_SCHRITTZAHL_WARMLUFT_MOTOR_RE_WERT | unsigned long |  |
| STAT_SCHRITTZAHL_WARMLUFT_MOTOR_RE_EINH | string | 1000 Inkremente |
| STAT_SCHRITTZAHL_KALTLUFT_MOTOR_LI_WERT | unsigned long |  |
| STAT_SCHRITTZAHL_KALTLUFT_MOTOR_LI_EINH | string | 1000 Inkremente |
| STAT_SCHRITTZAHL_KALTLUFT_MOTOR_RE_WERT | unsigned long |  |
| STAT_SCHRITTZAHL_KALTLUFT_MOTOR_RE_EINH | string | 1000 Inkremente |
| STAT_SCHRITTZAHL_FRISCHLUFT_MOTOR_WERT | unsigned long |  |
| STAT_SCHRITTZAHL_FRISCHLUFT_MOTOR_EINH | string | 1000 Inkremente |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bs-temperatur-sensoren"></a>
### STATUS_BS_TEMPERATUR_SENSOREN

Auslesen der Betriebsstunden Temperatursensoren KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WT_LI_BEREICH_A_WERT | unsigned long |  |
| STAT_WT_LI_BEREICH_A_EINH | string | min |
| STAT_WT_LI_BEREICH_B_WERT | unsigned long |  |
| STAT_WT_LI_BEREICH_B_EINH | string | min |
| STAT_WT_LI_BEREICH_C_WERT | unsigned long |  |
| STAT_WT_LI_BEREICH_C_EINH | string | min |
| STAT_WT_RE_BEREICH_A_WERT | unsigned long |  |
| STAT_WT_RE_BEREICH_A_EINH | string | min |
| STAT_WT_RE_BEREICH_B_WERT | unsigned long |  |
| STAT_WT_RE_BEREICH_B_EINH | string | min |
| STAT_WT_RE_BEREICH_C_WERT | unsigned long |  |
| STAT_WT_RE_BEREICH_C_EINH | string | min |
| STAT_VERDAMPFER_BEREICH_A_WERT | unsigned long |  |
| STAT_VERDAMPFER_BEREICH_A_EINH | string | min |
| STAT_VERDAMPFER_BEREICH_B_WERT | unsigned long |  |
| STAT_VERDAMPFER_BEREICH_B_EINH | string | min |
| STAT_VERDAMPFER_BEREICH_C_WERT | unsigned long |  |
| STAT_VERDAMPFER_BEREICH_C_EINH | string | min |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wasserventile-lastwechsel"></a>
### STATUS_WASSERVENTILE_LASTWECHSEL

Auslesen der Zaehler fuer Wasserventil-Lastwechsel KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WV_LI_LASTWECHSEL_WERT | unsigned long |  |
| STAT_WV_LI_LASTWECHSEL_EINH | string | Anzahl |
| STAT_WV_RE_LASTWECHSEL_WERT | unsigned long |  |
| STAT_WV_RE_LASTWECHSEL_EINH | string | Anzahl |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bs-wasserpumpe"></a>
### STATUS_BS_WASSERPUMPE

Auslesen der Betriebsstunden Wasserpumpe KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BS_WASSERPUMPE_WERT | unsigned long |  |
| STAT_BS_WASSERPUMPE_EINH | string | min |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bs-kompressorventil"></a>
### STATUS_BS_KOMPRESSORVENTIL

Auslesen der Betriebsstunden Kompressorventil KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BS_KOMPRESSORVENTIL_WERT | unsigned long |  |
| STAT_BS_KOMPRESSORVENTIL_EINH | string | min |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bs-geblregler-lastprofil"></a>
### STATUS_BS_GEBLREGLER_LASTPROFIL

Auslesen der Status Geblaeseregler-Lastprofil KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BS_GEBLREGLER_BEREICH_A_WERT | unsigned long |  |
| STAT_BS_GEBLREGLER_BEREICH_A_EINH | string | min |
| STAT_BS_GEBLREGLER_BEREICH_B_WERT | unsigned long |  |
| STAT_BS_GEBLREGLER_BEREICH_B_EINH | string | min |
| STAT_BS_GEBLREGLER_BEREICH_C_WERT | unsigned long |  |
| STAT_BS_GEBLREGLER_BEREICH_C_EINH | string | min |
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

<a id="job-status-bs-priostufen"></a>
### STATUS_BS_PRIOSTUFEN

Auslesen der Status Stundenzaehler Priostufen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZAEHLER_PRIOSTUFE_1_WERT | unsigned long |  |
| STAT_ZAEHLER_PRIOSTUFE_1_EINH | string | min |
| STAT_ZAEHLER_PRIOSTUFE_4_WERT | unsigned long |  |
| STAT_ZAEHLER_PRIOSTUFE_4_EINH | string | min |
| STAT_ZAEHLER_PRIOSTUFE_5_WERT | unsigned long |  |
| STAT_ZAEHLER_PRIOSTUFE_5_EINH | string | min |
| STAT_ZAEHLER_PRIOSTUFE_6_WERT | unsigned long |  |
| STAT_ZAEHLER_PRIOSTUFE_6_EINH | string | min |
| STAT_ZAEHLER_STANDVERBRAUCHER_WERT | unsigned long |  |
| STAT_ZAEHLER_STANDVERBRAUCHER_EINH | string | min |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-individualisierung"></a>
### STATUS_INDIVIDUALISIERUNG

Auslesen der Status Individualisierung KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KLAPPE_LINKS_OBEN_WERT | unsigned long |  |
| STAT_KLAPPE_LINKS_OBEN_EINH | string | % |
| STAT_KLAPPE_LINKS_MITTE_WERT | unsigned long |  |
| STAT_KLAPPE_LINKS_MITTE_EINH | string | % |
| STAT_KLAPPE_LINKS_UNTEN_WERT | unsigned long |  |
| STAT_KLAPPE_LINKS_UNTEN_EINH | string | % |
| STAT_KLAPPE_RECHTS_OBEN_WERT | unsigned long |  |
| STAT_KLAPPE_RECHTS_OBEN_EINH | string | % |
| STAT_KLAPPE_RECHTS_MITTE_WERT | unsigned long |  |
| STAT_KLAPPE_RECHTS_MITTE_EINH | string | % |
| STAT_KLAPPE_RECHTS_UNTEN_WERT | unsigned long |  |
| STAT_KLAPPE_RECHTS_UNTEN_EINH | string | % |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motor-antwortet-nicht-loeschen"></a>
### STEUERN_MOTOR_ANTWORTET_NICHT_LOESCHEN

Zaehler fuer Motor antwortet nicht loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motor-blockierung-loeschen"></a>
### STEUERN_MOTOR_BLOCKIERUNG_LOESCHEN

Zaehler fuer Motor-Blockierung loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTOR | int | Motorangabe 0=WL-LI,1=WL-RE,2=UL,3=DFR,4=FUSS_LI,5=FUSS_RE,6=KL-LI,7=KL-RE,8=FOND-LI,9=FOND-RE 10=FOKL-B-LI,11=FOKL-MI-LI, 15=KUG-LI-AU,16=KUG-LI-MI,17=KNIE-LI,18=INDIR-LI,19=KUG-RE-MI 20=KUG-RE-AU,21=KNIE-RE,22=INDIR-RE,23=A-SAEU-LI,24=A-SAEU-RE,25=B-SAEU-LI 26=MITKON-LI,27=B-SAEU-RE,28=MITKON-RE,29=FOKL-B-RE,30=FOKL-MI-RE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motor-interner-fehler-loeschen"></a>
### STEUERN_MOTOR_INTERNER_FEHLER_LOESCHEN

Zaehler fuer interne Motorfehler loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-geblaese-antwortet-nicht-loeschen"></a>
### STEUERN_GEBLAESE_ANTWORTET_NICHT_LOESCHEN

Zaehler fuer Geblaese antwortet nicht loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-uspg-standheizen-zaehler-loeschen"></a>
### STEUERN_USPG_STANDHEIZEN_ZAEHLER_LOESCHEN

Zaehler fuer Uspg Standheizen loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motor-summe-schrittzahlen-loeschen"></a>
### STEUERN_MOTOR_SUMME_SCHRITTZAHLEN_LOESCHEN

Zaehler fuer kumulierte Motorschrittzahlen loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTOR | int | Motorangabe 0=WL-LI,1=WL-RE,2=KL-LI,3=KL-RE,4=FL |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bs-temperatur-sensoren-loeschen"></a>
### STEUERN_BS_TEMPERATUR_SENSOREN_LOESCHEN

BS Temperatursensoren loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR | int | Sensorangabe 0=WAERMETAUSCHER-LI,1=WAERMETAUSCHER-RE,2=VERDAMPFER |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wasserventile-lastwechsel-loeschen"></a>
### STEUERN_WASSERVENTILE_LASTWECHSEL_LOESCHEN

Zaehler fuer WV-Lastwechsel loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WASSERVENTIL | int | Wasserventil 0=LINKS,1=RECHTS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bs-wasserpumpe-loeschen"></a>
### STEUERN_BS_WASSERPUMPE_LOESCHEN

Zaehler fuer Wasserpumpe loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bs-kompressorventil-loeschen"></a>
### STEUERN_BS_KOMPRESSORVENTIL_LOESCHEN

Zaehler fuer Kompressorventil loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-geblregler-lastprofil-loeschen"></a>
### STEUERN_GEBLREGLER_LASTPROFIL_LOESCHEN

Zaehler fuer Geblaeseregler-Lastprofil loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

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

<a id="job-steuern-bs-priostufen-loeschen"></a>
### STEUERN_BS_PRIOSTUFEN_LOESCHEN

Zaehler fuer Priostufen (PowerModul) loeschen KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mux4-kommunikation"></a>
### STEUERN_MUX4_KOMMUNIKATION

Sperren der MUX4-Kommunikation Die Sperre kann aktiviert( EIN )bzw. deaktiviert (AUS) werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERRE | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motor-programmieren"></a>
### STEUERN_MOTOR_PROGRAMMIEREN

Programmieren von Schrittmotoren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE_SCHRITTMOTOREN | int | Schrittmotoradresse im Bereich von 0x11..0x1C und 0x20..0x2F zulaessig |

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
| TASTEN_NUMMER | int | Tastennummern im Bereich von 0 bis 2 zulaessig 0 = HHS, 1 = UML, 2 = AC_OFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-zwp-aktivieren"></a>
### ZWP_AKTIVIEREN

Aktivieren der Zusatzwasserpumpe (Setzen des Codierbits) KWP 2000: $23 ReadMemoryByAddress KWP 2000: $31 StartRoutineByLocalIdentifier KWP 2000: $23 ReadMemoryByAddress Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MELDUNG | string | Zustand nach dem Job: WP aktiv/nicht aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-zwp-deaktivieren"></a>
### ZWP_DEAKTIVIEREN

Deaktivieren der Zusatzwasserpumpe (Loeschen des Codierbits) KWP 2000: $23 ReadMemoryByAddress KWP 2000: $31 StartRoutineByLocalIdentifier KWP 2000: $23 ReadMemoryByAddress Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MELDUNG | string | Zustand nach dem Job: WP aktiv/nicht aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bos-daten-lesen"></a>
### BOS_DATEN_LESEN

BOS Daten auslesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ECU_ADR_WERT | string | Steuergeräteadresse als Hex-String |
| STAT_ECU_ADR_EINH | string | Adresse |
| STAT_ID_FN_BOS_MESS_WERT | string | BOS-Kennung |
| STAT_ID_FN_BOS_MESS_EINH | string | Kennung |
| STAT_RMMI_BOS_WERT | string | Restlaufleistung |
| STAT_RMMI_BOS_EINH | string | km |
| STAT_ST_UN_BOS_WERT | string | Einheit Restlaufleistung |
| STAT_ST_UN_BOS_EINH | string | km |
| STAT_COU_RSTG_BOS_MESS_WERT | string | Servicezähler |
| STAT_COU_RSTG_BOS_MESS_EINH | string | km |
| STAT_AVAI_BOS_WERT | string | Verfügbarkeit in % |
| STAT_AVAI_BOS_EINH | string | % |
| STAT_ZIEL_MM_WERT | string | Ziel-Monat (HU/AU) |
| STAT_ZIEL_MM_EINH | string | Monat |
| STAT_ZIEL_YY_WERT | string | Ziel-Jahr (HU/AU) |
| STAT_ZIEL_YY_EINH | string | Jahr |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bos-reset"></a>
### BOS_RESET

BOS Daten Zurücksetzen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BOS_KENNUNG_WERT | string | gewünschte BOS-Kennung table BosKennung BOS_K BOS_K_TEXT Werte: Oel, Br_v, Brfl, Filt, Batt, Br_h, ZKrz, Sic, Kfl, TUV, AU Defaultwert: Oel |
| STAT_BOS_VERFUEGBARKEIT_WERT | string | gewünschte Verfügbarkeit in Prozent: 0-200 Schalter, kein Rückstellen: 255 Defaultwert: 100 |
| STAT_BOS_ANZAHL_SERVICE_WERT | string | Anzahl der durchgeführten Services: 0-30 Schalter, keine Änderung: 31 Defaultwert: 31 |
| STAT_BOS_ZIEL_MONAT_WERT | string | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter für Monat und Jahr, keine Änderung: 255 Defaultwert: 255 |
| STAT_BOS_ZIEL_JAHR_WERT | string | Ziel-Jahr (HU/AU) 2000-2239: 0-239 d.c.: 255 Defaultwert: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BOS_KENNUNG_EINH | string | Kennung |
| STAT_BOS_VERFUEGBARKEIT_EINH | string | % |
| STAT_BOS_ANZAHL_SERVICE_EINH | string | Anzahl |
| STAT_BOS_ZIEL_MONAT_EINH | string | Monat |
| STAT_BOS_ZIEL_JAHR_EINH | string | Jahr |
| STAT_ECU_ADR_WERT | string | Steuergeräteadresse als Hex-String |
| STAT_ECU_ADR_EINH | string | Adresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-poti-kalibrierung-rr"></a>
### STEUERN_POTI_KALIBRIERUNG_RR

Starten der Kalibrierung fuer die 6 bei RR einzulernenden Potentiometer Vorgehen: 1. Kalibrierung starten (durch Aufruf dieses Jobs) (die 3 Funktions-LEDs beginnen zu blinken) 2. IHKA Geblaesesteller und alle Bedienelemente des Heckbedienteiles auf MIN stellen 3. UMLUFT-Taste der IHKA (linke Taste) druecken (die linke LED hoert auf zu blinken, wenn Linksanschlaege erfolgreich gelernt wurden) 4. IHKA Geblaesesteller und alle Bedienelemente des Heckbedienteiles auf MAX stellen 5. AC_OFF-Taste der IHKA (rechte Taste) betaetigen - FERTIG (die beiden rechten LEDs hoeren bei Erfolg nun auch auf zu blinken) gab es ein Problem beim Lernen, blinken die LEDs weiter 60sec nach Aktivierung des Jobs bzw. nach dem ersten Tastendruck wird das Lernen abgebrochen, wenn bis dahin nicht erfolgreich gelernt wurde. KWP2000: $30 InputOutputControlByLocalIdentifier $01 Modus  : Default Dieser Job lernt folgende Potis ein: (Namen aus dem Job STATUS_ANALOGAEINGAENGE) STAT_POTI_GEBL_LI_WERT         Geblaesedrehsteller vorne links STAT_POTI_GEBL_RE_WERT         Geblaesedrehsteller vorne rechts STAT_POTI_GEBL_FOND_LI_WERT    Geblaesedrehsteller hinten links STAT_POTI_GEBL_FOND_RE_WERT    Geblaesedrehsteller hinten rechts STAT_POTI_TEMP_FOND_LI_WERT    Temperaturraendel hinten links STAT_POTI_TEMP_FOND_RE_WERT    Temperaturraendel hinten rechts

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-poti-kalibrierung-preh"></a>
### STEUERN_POTI_KALIBRIERUNG_PREH

Starten der Kalibrierung fuer die 5 IHKA Raendelraeder (Temp. und GBL Frontscheibe) Vorgehen: 1. Kalibrierung starten (mit diesem Job) (die drei Funktions-LEDs am Bedienteil beginnen zu blinken) 2. IHKA Raendelraeder in den Linksanschlag drehen 3. UMLUFT-Taste der IHKA betaetigen (linke Taste) (die linke LED hoert auf zu blinken, wenn die Linksanschlaege erfolgreich gelernt wurden.) 4. IHKA Raendelraeder in den Rechtsanschlag drehen 5. AC_OFF-Taste (auf der rechten Seite) betaetigen - FERTIG (die beiden rechten LEDs hoeren bei Erfolg nun auch auf zu blinken) gab es ein Problem beim Lernen, blinken die LEDs weiter 60sec nach Aktivierung des Jobs bzw. nach dem ersten Tastendruck wird das Lernen abgebrochen, wenn bis dahin nicht erfolgreich gelernt wurde. KWP2000: $30 InputOutputControlByLocalIdentifier $01 Modus  : Default Dieser Job lernt folgende Potis ein: (Namen aus dem Job STATUS_ANALOGAEINGAENGE) STAT_POTI_TEMP_LI_OBEN_WERT      Temperaturraendel links oben STAT_POTI_TEMP_LI_UNTEN_WERT     Temperaturraendel links unten STAT_POTI_SCHEIBENLUFT_WERT      Frontscheibenluftraendel STAT_POTI_TEMP_RE_OBEN_WERT      Temperaturraendel rechts oben STAT_POTI_TEMP_RE_UNTEN_WERT     Temperaturraendel rechts unten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-poti-kalibrierung-rr"></a>
### STATUS_POTI_KALIBRIERUNG_RR

Auslesen des Status der Kalibrierung der bei RR zu lernenden Potis Gibt nur beim ersten Lesen nach erfolgter Kalibrierung den Status zurueck, sonst Null KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIBRIERUNG_RR | int | 0=nicht eingelernt  1=eingelernt |
| STAT_KALIBRIERUNG_RR_TEXT | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-poti-kalibrierung-preh"></a>
### STATUS_POTI_KALIBRIERUNG_PREH

Auslesen des Status der Kalibrierung der bei Preh einzulernenden Potis Gibt nur beim ersten Lesen nach erfolgter Kalibrierung den Status zurueck, sonst Null KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIBRIERUNG_PREH_TEXT | string |  |
| STAT_KALIBRIERUNG_PREH | int | 0=nicht eingelernt  1=eingelernt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-kugelaus-links-aussen"></a>
### STEUERN_KLAPPE_KUGELAUS_LINKS_AUSSEN

Ansteuern des Kugelausstroemers links aussen im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_KUGELAUS_LINKS_AUSSEN | int | Klappenansteuerung KLAPPE_KUGELAUS_LINKS_AUSSEN in Prozentschritten 0-100 % Motoradresse 0x20 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-kugelaus-links-mitte"></a>
### STEUERN_KLAPPE_KUGELAUS_LINKS_MITTE

Ansteuern des Kugelausstroemers links mitte im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_KUGELAUS_LINKS_MITTE | int | Klappenansteuerung KLAPPE_KUGELAUS_LINKS_MITTE in Prozentschritten 0-100 % Motoradresse 0x21 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-knieaus-links"></a>
### STEUERN_KLAPPE_KNIEAUS_LINKS

Ansteuern des Knieausstroemers links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_KNIEAUS_LINKS | int | Klappenansteuerung KLAPPE_KNIEAUS_LINKS in Prozentschritten 0-100 % Motoradresse 0x22 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-indirekteraus-links"></a>
### STEUERN_KLAPPE_INDIREKTERAUS_LINKS

Ansteuern des indirekten Ausstroemers links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_INDIREKTERAUS_LINKS | int | Klappenansteuerung KLAPPE_INDIREKTERAUS_LINKS in Prozentschritten 0-100 % Motoradresse 0x23 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-kugelaus-rechts-mitte"></a>
### STEUERN_KLAPPE_KUGELAUS_RECHTS_MITTE

Ansteuern des Kugelausstroemers rechts mitte im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_KUGELAUS_RECHTS_MITTE | int | Klappenansteuerung KLAPPE_KUGELAUS_RECHTS_MITTE in Prozentschritten 0-100 % Motoradresse 0x24 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-kugelaus-rechts-aussen"></a>
### STEUERN_KLAPPE_KUGELAUS_RECHTS_AUSSEN

Ansteuern des Kugelausstroemers rechts aussen im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_KUGELAUS_RECHTS_AUSSEN | int | Klappenansteuerung KLAPPE_KUGELAUS_RECHTS_AUSSEN in Prozentschritten 0-100 % Motoradresse 0x25 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-knieaus-rechts"></a>
### STEUERN_KLAPPE_KNIEAUS_RECHTS

Ansteuern des Knieausstroemers rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_KNIEAUS_RECHTS | int | Klappenansteuerung KLAPPE_KNIEAUS_RECHTS in Prozentschritten 0-100 % Motoradresse 0x26 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-indirekteraus-rechts"></a>
### STEUERN_KLAPPE_INDIREKTERAUS_RECHTS

Ansteuern des indirekten Ausstroemers rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_INDIREKTERAUS_RECHTS | int | Klappenansteuerung KLAPPE_INDIREKTERAUS_RECHTS in Prozentschritten 0-100 % Motoradresse 0x27 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-a-saeule-links"></a>
### STEUERN_KLAPPE_A_SAEULE_LINKS

Ansteuern des Ausstroemers an der A-Saeule links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_A_SAEULE_LINKS | int | Klappenansteuerung KLAPPE_A_SAEULE_LINKS in Prozentschritten 0-100 % Motoradresse 0x28 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-a-saeule-rechts"></a>
### STEUERN_KLAPPE_A_SAEULE_RECHTS

Ansteuern des Ausstroemers an der A-Saeule rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_A_SAEULE_RECHTS | int | Klappenansteuerung KLAPPE_A_SAEULE_RECHTS in Prozentschritten 0-100 % Motoradresse 0x29 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-b-saeule-links"></a>
### STEUERN_KLAPPE_B_SAEULE_LINKS

Ansteuern des Ausstroemers an der B-Saeule links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_B_SAEULE_LINKS | int | Klappenansteuerung KLAPPE_B_SAEULE_LINKS in Prozentschritten 0-100 % Motoradresse 0x2A |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-mittelkon-links"></a>
### STEUERN_KLAPPE_MITTELKON_LINKS

Ansteuern des Ausstroemers an der Mittelkonsole links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_MITTELKON_LINKS | int | Klappenansteuerung KLAPPE_MITTELKON_LINKS in Prozentschritten 0-100 % Motoradresse 0x2B |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-b-saeule-rechts"></a>
### STEUERN_KLAPPE_B_SAEULE_RECHTS

Ansteuern des Ausstroemers an der B-Saeule rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_B_SAEULE_RECHTS | int | Klappenansteuerung KLAPPE_B_SAEULE_RECHTS in Prozentschritten 0-100 % Motoradresse 0x2C |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-mittelkon-rechts"></a>
### STEUERN_KLAPPE_MITTELKON_RECHTS

Ansteuern des Ausstroemers an der Mittelkonsole rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_MITTELKON_RECHTS | int | Klappenansteuerung KLAPPE_MITTELKON_RECHTS in Prozentschritten 0-100 % Motoradresse 0x2D |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fondgeblaese-links"></a>
### STEUERN_FONDGEBLAESE_LINKS

Ansteuern des Fondgeblaese links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FONDGEBLAESE_LINKS | int | Ansteuerung FONDGEBLAESE_LINKS in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fondgeblaese-rechts"></a>
### STEUERN_FONDGEBLAESE_RECHTS

Ansteuern des Fondgeblaese rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FONDGEBLAESE_RECHTS | int | Ansteuerung FONDGEBLAESE_LINKS in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-seitenscheibenheizung"></a>
### STEUERN_SEITENSCHEIBENHEIZUNG

Ansteuern der Seitenscheibenheizung im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEITENSCHEIBENHEIZUNG | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fokl-b-li"></a>
### STEUERN_KLAPPE_FOKL_B_LI

Ansteuern des Fondklima Klappenmoduls B-Saeule links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FOKL_B_LI | int | Klappenansteuerung KLAPPE_FOKL_B_LI in Prozentschritten 0-100 % Motoradresse 0x1B |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fokl-mi-li"></a>
### STEUERN_KLAPPE_FOKL_MI_LI

Ansteuern des Fondklima Klappenmoduls Mittelkonsole links im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FOKL_MI_LI | int | Klappenansteuerung KLAPPE_FOKL_MI_LI in Prozentschritten 0-100 % Motoradresse 0x1C |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fokl-b-re"></a>
### STEUERN_KLAPPE_FOKL_B_RE

Ansteuern des Fondklima Klappenmoduls B-Saeule rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FOKL_B_RE | int | Klappenansteuerung KLAPPE_FOKL_B_RE in Prozentschritten 0-100 % Motoradresse 0x2E |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klappe-fokl-mi-re"></a>
### STEUERN_KLAPPE_FOKL_MI_RE

Ansteuern des Fondklima Klappenmoduls Mittelkonsole rechts im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPE_FOKL_MI_RE | int | Klappenansteuerung KLAPPE_FOKL_MI_RE in Prozentschritten 0-100 % Motoradresse 0x2F |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fondklima-li"></a>
### STEUERN_FONDKLIMA_LI

Ansteuern des Fondklimaausganges Links im Diagnosemode (Nur erlaubt, wenn Fondgeblaese nicht auf 0!) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FONDKLIMA_LI | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fondklima-re"></a>
### STEUERN_FONDKLIMA_RE

Ansteuern des Fondklimaausganges Rechts im Diagnosemode (Nur erlaubt, wenn Fondgeblaese nicht auf 0!) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FONDKLIMA_RE | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-beschlag-sensor"></a>
### STATUS_BESCHLAG_SENSOR

Auslesen des Status des Beschlagsensors KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BESCHLAGSENSOR_WERT | real | Beschlagsensorfrequenz |
| STAT_BESCHLAGSENSOR_EINH | string | Hz |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geruchsstartverriegelung"></a>
### STATUS_GERUCHSSTARTVERRIEGELUNG

Auslesen der Geruchsstartverriegelungsparameter KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSSENTEMP_WERT | int | Wert der Aussentemperaturschwelle in Grad |
| STAT_AUSSENTEMP_EINH | string | Grad Celsius |
| STAT_GEBLAESELEISTUNG_WERT | int | Wert der Geblaeseleistung in % |
| STAT_GEBLAESELEISTUNG_EINH | string | Prozent |
| STAT_VERZOEGERUNGSZEIT_WERT | int | Codierung der Verzoegerungszeit 0 ==&gt;  0 Sek --&gt; GSV AUS 1 ==&gt;  8 Sek 2 ==&gt; 10 Sek 3 ==&gt; 12 Sek 4 ==&gt; 15 Sek |
| STAT_VERZOEGERUNGSZEIT_EINH | string | Inkremente |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-geruchsstartverriegelung"></a>
### STEUERN_GERUCHSSTARTVERRIEGELUNG

Parameter der Geruchsstartverriegelung setzen KWP2000: $30 InputOutputControlByLocalIdentifier $08 LongTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSSENTEMP_WERT | int | Aussentemperaturschwelle in Grad |
| GEBLAESELEISTUNG_WERT | int | Geblaeseleistung in % |
| VERZOEGERUNGSZEIT_WERT | int | Codierung der Verzoegerungszeit 0 ==&gt;  0 Sek --&gt; GSV AUS 1 ==&gt;  8 Sek 2 ==&gt; 10 Sek 3 ==&gt; 12 Sek 4 ==&gt; 15 Sek |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
- [JOBRESULTEXTENDED](#table-jobresultextended) (2 × 2)
- [FORTTEXTE](#table-forttexte) (113 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (5 × 9)
- [BOSKENNUNG](#table-boskennung) (11 × 3)
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

Dimensions: 2 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x01 | ERROR_SOFTWARENUMMER |
| 0xXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 113 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9C48 | Warmluftklappenmotor links Motoradresse 11hex |
| 0x9C49 | Warmluftklappenmotor rechts Motoradresse 12hex |
| 0x9C4A | Umluftklappenmotor Motoradresse 13hex |
| 0x9C4B | Entfrostungsklappenmotor Motoradresse 14hex |
| 0x9C4C | Fussraumklappenmotor links Fond Motoradresse 15hex |
| 0x9C4D | Fussraumklappenmotor rechts Fond Motoradresse 16hex |
| 0x9C4E | Kaltluftklappenmotor links Motoradresse 17hex |
| 0x9C4F | Kaltluftklappenmotor rechts Motoradresse 18hex |
| 0x9C50 | Fondbelueftungsklappenmotor links Motoradresse 19hex |
| 0x9C51 | Fondbelueftungsklappenmotor rechts Motoradresse 1Ahex |
| 0x9C52 | Fondklimaklappenmotor B-Saeule links Motoradresse 1Bhex |
| 0x9C53 | Fondklimaklappenmotor Mittelkonsole links Motoradresse 1Chex |
| 0x9C54 | Reserve 1 |
| 0x9C55 | Frischluftklappenmotor |
| 0x9C56 | Umluft als Schnelllaeufer (vorgehalten) |
| 0x9C57 | Kugelausstroemer Stellmotor links Aussen Motoradresse 20hex |
| 0x9C58 | Kugelausstroemer Stellmotor links Mitte Motoradresse 21hex |
| 0x9C59 | Knieausstroemer Stellmotor links Motoradresse 22hex |
| 0x9C5A | Ausstroemer Stellmotor Indirekt links Motoradresse 23hex |
| 0x9C5B | Kugelausstroemer Stellmotor rechts Mitte Motoradresse 24hex |
| 0x9C5C | Kugelausstroemer Stellmotor rechts Aussen Motoradresse 25hex |
| 0x9C5D | Knieausstroemer Stellmotor rechts Motoradresse 26hex |
| 0x9C5E | Ausstroemer Stellmotor Indirekt rechts Motoradresse 27hex |
| 0x9C5F | Mischklappenmotor A-Saeule links Motoradresse 28hex |
| 0x9C60 | Mischklappenmotor A-Saeule rechts Motoradresse 29hex |
| 0x9C61 | Kugelausstroemer Stellmotor B-Saeule links Motoradresse 2Ahex |
| 0x9C62 | Kugelausstroemer Stellmotor Mittelkonsole links Motoradresse 2Bhex |
| 0x9C63 | Kugelausstroemer Stellmotor B-Saeule rechts Motoradresse 2Chex |
| 0x9C64 | Kugelausstroemer Stellmotor Mittelkonsole rechts Motoradresse 2Dhex |
| 0x9C65 | Fondklimaklappenmotor B-Saeule rechts Motoradresse 2Ehex |
| 0x9C66 | Fondklimaklappenmotor Mittelkonsole rechts Motoradresse 2Fhex |
| 0x9C67 | Geblaeseendstufe IHKA |
| 0x9C68 | Innenraumtemperaturfuehler |
| 0x9C69 | Stromsense fuer Kaeltemittelverdichter |
| 0x9C6A | Stromsense fuer Zusatzwasserpumpe |
| 0x9C6B | Monitor Drucksensor Versorgung |
| 0x9C6C | Stromsense fuer AUC Versorgung/Heizung |
| 0x9C6D | Stromsense fuer Treiberversorgung |
| 0x9C6E | Temperatur Sensor Fond links |
| 0x9C6F | Potentiometer Nr. 5 fuer Kugelausstroemer Stellmotor B-Saeule links |
| 0x9C70 | Temperatur Sensor Fond rechts |
| 0x9C71 | Potentiometer Nr. 6 fuer Kugelausstroemer Stellmotor Mittelkonsole links |
| 0x9C72 | Hall-Sensor Nr. 1 fuer Knieausstroemer Stellmotor links |
| 0x9C73 | Hall-Sensor Nr. 2 fuer Knieausstroemer Stellmotor rechts |
| 0x9C74 | Potentiometer Nr. 3 fuer Kugelausstroemer Stellmotor rechts Mitte |
| 0x9C75 | Potentiometer Nr. 4 fuer Kugelausstroemer Stellmotor rechts Aussen |
| 0x9C76 | Temperatur Sensor Waermetauscher rechts |
| 0x9C77 | Temperatur Sensor Waermetauscher links |
| 0x9C78 | Potentiometer Nr. 8 fuer Kugelausstroemer Stellmotor Mittelkonsole rechts |
| 0x9C79 | Verdampfertemperaturfuehler |
| 0x9C7A | Belueftungstemperaturfuehler links |
| 0x9C7B | AUC-Sensor |
| 0x9C7C | Belueftungstemperaturfuehler rechts |
| 0x9C7D | 5V Sammelversorgung: Sonnen-/Beschlagsensor, Ausstroemer-, Fond-, Geblaese-Potis |
| 0x9C7E | Potentiometer Temperatur links unten |
| 0x9C7F | Potentiometer Temperatur links oben |
| 0x9C80 | Potentiometer Geblaese IHKA links |
| 0x9C81 | Potentiometer Geblaese IHKA rechts |
| 0x9C82 | Monitor AUC Versorgung/Heizung |
| 0x9C83 | Leiterplatten-Code |
| 0x9C84 | Monitor 12V Versorgung Fond |
| 0x9C85 | Potentiometer Temperatur rechts unten |
| 0x9C86 | Potentiometer Nr. 7 fuer Kugelausstroemer Stellmotor B-Saeule rechts |
| 0x9C87 | Monitor Steuerspannung Fondgeblaese links |
| 0x9C88 | Potentiometer Temperatur rechts oben |
| 0x9C89 | Monitor Steuerspannung Fondgeblaese rechts |
| 0x9C8A | Potentiometer Frontscheibenluft |
| 0x9C8B | Drucksensor |
| 0x9C8C | Potentiometer Nr. 2 fuer Kugelausstroemer Stellmotor links Mitte |
| 0x9C8D | Solarsensor links |
| 0x9C8E | Potentiometer Nr. 1 fuer Kugelausstroemer Stellmotor links Aussen |
| 0x9C8F | Solarsensor rechts |
| 0x9C90 | Potentiometer Fondgeblaese links |
| 0x9C91 | Potentiometer Fond Temperatur links |
| 0x9C92 | Potentiometer Fondgeblaese rechts |
| 0x9C93 | Potentiometer Fond Temperatur rechts |
| 0x9C94 | Zusatzwasserpumpe |
| 0x9C95 | Kaeltemittelverdichter |
| 0x9C96 | Wischerablagenheizung |
| 0x9C97 | Wasserventil links |
| 0x9C98 | Wasserventil rechts |
| 0x9C99 | Innenfuehlergeblaese |
| 0x9C9A | Kaeltemittelverdichter Sperrventil |
| 0x9C9B | Seitenscheibenheizung |
| 0x9C9C | Beschlagsensor |
| 0x9C9D | Treiber Reserve 1 |
| 0x9C9E | Treiber Reserve 2 |
| 0x9C9F | KCAN: Waermestrom Motor ( DME1 ) |
| 0x9CA0 | Fondgeblaese links |
| 0x9CA1 | Fondgeblaese rechts |
| 0x9CA2 | 12V Versorgung MUX4-Bus Blau |
| 0x9CA3 | 12V Versorgung MUX4-Bus Weiss |
| 0x9CA4 | SH/SK nicht EIN wegen Reichweite |
| 0x9CA5 | Checksumme EEPROM |
| 0x9CA6 | KCAN: Kilometerstand ( KOMBI ) |
| 0x9CA7 | KCAN: Klemmenstatus ( CAS ) |
| 0xA608 | Heizbare Heckscheibe |
| 0xA609 | Zusatzluefter |
| 0xA60A | KCAN: Relativzeit ( KOMBI ) |
| 0xA612 | KCAN: Motor laeuft ( DME1 ) |
| 0xA614 | KCAN: Aussentemperatur ( KOMBI ) |
| 0xA615 | KCAN: Fahrzeuggeschwindigkeit ( DSC ) |
| 0xA616 | KCAN: Kuehlmitteltemperatur ( DME1 ) |
| 0xA617 | KCAN: Motordrehzahl ( DME1 ) |
| 0xA618 | KCAN: Dimmung ( LSZ ) |
| 0xA619 | KCAN: Powermanagement Batteriespannung ( PM ) |
| 0xA61A | KCAN: Stand/Zuheizer ( SH/ZH ) |
| 0xA647 | Energiesparmode aktiv |
| 0xE704 | CAN-Low, Physikalischer Busfehler |
| 0xE705 | Netzwerkmanagementfehler |
| 0xE706 | MUX4-Bus Fehler |
| 0xE707 | Controller, Bus Off |
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
