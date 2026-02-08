# mevd17kw.prg

- Jobs: [270](#jobs)
- Tables: [132](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MEVD172 mit KWP Protokoll  |
| ORIGIN | BMW EA-740 Lorch |
| REVISION | 5.050 |
| AUTHOR | P&Z EA-740 Berger, P&Z EA-740 Hadersdorfer |
| COMMENT | SGBD für MEVD172 KWP zur Software 7982780B |
| PACKAGE | 1.66 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default
- [STATUS_MESSWERTBLOCK_LESEN](#job-status-messwertblock-lesen) - Lesen eines Messwertblockes Es muss immer das BlockSchreibenFlag und mindestens ein MESSWERT uebergeben werden. KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $04 ClearDynamicallyDefinedLocalIdentifier KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $02 DefineByCommonIdentifier KWP2000: $21 ReadDataByLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier Modus  : Default
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 4) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 4) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)
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
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [MESSWERTBLOCK_LESEN](#job-messwertblock-lesen) - 0x2CF0 MESSWERTBLOCK_LESEN DDLI Messwerte auf Basis Übergabestring aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1 es können 40 Messwerte in einem Block zusammengefasst werden
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [IS_LESEN](#job-is-lesen) - 0x222000 IS_LESEN Infospeicher lesen (alle Info-Meldungen / Ort und Art) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [STATUS_BETRIEBSSTUNDENZAEHLER](#job-status-betriebsstundenzaehler) - 0x2CF0 5AB4 STATUS_BETRIEBSSTUNDENZAEHLER Betriebsstundenzaehler auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [IDENT_AIF](#job-ident-aif) - 0x1A80 und 0x23 IDENT_AIF Identdaten und Anwender Informations Felder Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [ABGLEICHWERTE_SCHREIBEN](#job-abgleichwerte-schreiben) - 0x2E5F90 ABGLEICHWERTE_SCHREIBEN Abgleichwerte Injektoren programmieren für CASCADE mit Übernahme Daten aus COD-Datei Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - 0x225F90 ABGLEICHWERTE_LESEN Abgleichwerte Injektoren auslesen für CASCADE für Vergleich mit Daten aus COD-Datei Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EWS](#job-status-ews) - KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC000 Zurücklesen verschiedener interner Stati für EWS
- [STATUS_EWS4_SK](#job-status-ews4-sk) - KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC002 Lesen des SecretKey des Server sowie Client für EWS4
- [STEUERN_EWS4_SK](#job-steuern-ews4-sk) - 17 "EWS4-data" schreiben KWP 2000: $2E WriteDataByCommonIdentifier CommonIdentifier=0xC001
- [FLASH_SCHREIBEN_XXL](#job-flash-schreiben-xxl) - 0x36 FLASH_SCHREIBEN_XXL Flash Daten schreiben XXL-Format, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [FLASH_SCHREIBEN_ADRESSE_4BYTE](#job-flash-schreiben-adresse-4byte) - 0x34 FLASH_SCHREIBEN_ADRESSE_4BYTE Flash Daten schreiben, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [FLASH_LOESCHEN_4BYTE](#job-flash-loeschen-4byte) - 0x3102 FLASH_LOESCHEN_4BYTE Flash löschen, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [FLASH_SCHREIBEN_ENDE_4BYTE](#job-flash-schreiben-ende-4byte) - 0x37 FLASH_SCHREIBEN_ENDE_4BYTE Flashprogrammierung abschliessen, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [START_SYSTEMCHECK_IGR_AUS](#job-start-systemcheck-igr-aus) - 0x31F7 START_SYSTEMCHECK_IGR_AUS Ansteuerung Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_IGR_AUS](#job-stop-systemcheck-igr-aus) - 0x32F7 STOP_SYSTEMCHECK_IGR_AUS Ansteuerung Intelligente Generatorregelung deaktivieren beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_IGR_AUS](#job-status-systemcheck-igr-aus) - 0x33F7 STATUS_SYSTEMCHECK_IGR_AUS Auslesen Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_IGRINFO](#job-status-igrinfo) - 0x224016 STATUS_IGRINFO Infospeicher Intelligente Generator Regelung (IGR) auslesen
- [STATUS_LEMINFO](#job-status-leminfo) - 0x224017 STATUS_LEMINFO Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen
- [STATUS_SYSTEMCHECK_PM_INFO_1](#job-status-systemcheck-pm-info-1) - $22 40 22 Bytefeld 1 Batterie Powermanagement lesen
- [STATUS_SYSTEMCHECK_PM_INFO_2](#job-status-systemcheck-pm-info-2) - $22 40 23 Bytefeld 2 Batterie Powermanagement lesen
- [STEUERN_PM_HISTOGRAM_RESET](#job-steuern-pm-histogram-reset) - $30 F5 04 Loeschen von pminfo1 index 23-30
- [ADAP_SELEKTIV_LOESCHEN](#job-adap-selektiv-loeschen) - Löschen von Adaptionen und gelernte Varianten KWP 2000 $31 30 xx xx xx Loeschen der Adaptionswerte
- [STEUERN_BATTERIETAUSCH_REGISTRIEREN](#job-steuern-batterietausch-registrieren) - KWP 2000 $31 30 00 10 00 Bit setzen Batterietausch registrieren
- [START_SYSTEMCHECK_PM_MESSEMODE](#job-start-systemcheck-pm-messemode) - $31 F6 Systemdiagnose BatterieSensor reset
- [STOP_SYSTEMCHECK_PM_MESSEMODE](#job-stop-systemcheck-pm-messemode) - $32 F6 Systemdiagnose BatterieSensor reset beenden
- [LESEN_INDIVIDUALDATA_LISTE](#job-lesen-individualdata-liste) - Lesen eines Listeneintrags der Individualisierungsdaten KWP2000: $21 ReadDataByLocalIdentifier (not used) $01 recordLocalIdentifier (not used)
- [LESE_INDIVIDUALDATA](#job-lese-individualdata) - Lesen von Individualisierungsdaten Modus   : Default
- [SCHREIBEN_INDIVIDUALDATA](#job-schreiben-individualdata) - Schreiben von Individualisierungsdaten Modus   : Default
- [_STATUS_EISYUGD](#job-status-eisyugd) - 0x31E0 & 0x33E0 _STATUS_EISYUGD Ansteuern und Auslesen Eisy-Adaptionswerte (ungedrosselt) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_EISYGD](#job-status-eisygd) - 0x31E1 & 0x33E1 _STATUS_EISYGD Ansteuern und Auslesen Eisy-Adaptionswerte (gedrosselt) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_KRANN](#job-status-krann) - 0x31E3 & 0x33E3 _STATUS_KRANN Ansteuern und Auslesen Krann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_KLANN](#job-status-klann) - 0x31E4 & 0x33E4 _STATUS_KLANN Ansteuern und Auslesen Klann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [START_SYSTEMCHECK_TEV](#job-start-systemcheck-tev) - Ansteuern Diagnosefunktion Tankentlueftungsventil SYSTEMCHECK_TEV (0x22)
- [STATUS_SYSTEMCHECK_TEV](#job-status-systemcheck-tev) - Auslesen Diagnosefunktion Tankentlueftungsventil SYSTEMCHECK_TEV (0x22)
- [STOP_SYSTEMCHECK_TEV](#job-stop-systemcheck-tev) - Diagnosefunktion Tankentlueftungsventil beenden SYSTEMCHECK_TEV (0x22)
- [START_SYSTEMCHECK_EVAUSBL](#job-start-systemcheck-evausbl) - Ansteuern Diagnosefunktion Einspritzventilausblendung SYSTEMCHECK_EVAUSBL (0x25)
- [STATUS_SYSTEMCHECK_EVAUSBL](#job-status-systemcheck-evausbl) - Auslesen Diagnosefunktion EinspritzVentile EV-Ausblendung SYSTEMCHECK_EVAUSBL (0x25)
- [STOP_SYSTEMCHECK_EVAUSBL](#job-stop-systemcheck-evausbl) - Ende Diagnosefunktion EinspritzVentile EV-Ausblendung SYSTEMCHECK_EVAUSBL (0x25)
- [START_SYSTEMCHECK_VVT_ANSCHLAG](#job-start-systemcheck-vvt-anschlag) - Ansteuern Diagnosefunktion VVT-Anschlag lernen SYSTEMCHECK_VVT_ANSCHLAG (0x27)
- [STATUS_SYSTEMCHECK_VVT_ANSCHLAG](#job-status-systemcheck-vvt-anschlag) - Auslesen VVT Anschlag lernen SYSTEMCHECK_VVT_ANSCHLAG (0x27)
- [STOP_SYSTEMCHECK_VVT_ANSCHLAG](#job-stop-systemcheck-vvt-anschlag) - Diagnosefunktion VVT Anschlag lernen beenden SYSTEMCHECK_VVT_ANSCHLAG (0x27)
- [START_SYSTEMCHECK_GEN](#job-start-systemcheck-gen) - Diagnosefunktion Generatortest SYSTEMCHECK_GEN (0x2A)
- [STATUS_SYSTEMCHECK_GEN](#job-status-systemcheck-gen) - Auslesen Diagnosefunktion Generatortest SYSTEMCHECK_GEN (0x2A)
- [STOP_SYSTEMCHECK_GEN](#job-stop-systemcheck-gen) - Diagnosefunktion Generatortest beenden SYSTEMCHECK_GEN (0x2A)
- [START_SYSTEMCHECK_ODR](#job-start-systemcheck-odr) - Diagnosefunktion Oeldruckregelung SYSTEMCHECK_ODR (0x2C)
- [STATUS_SYSTEMCHECK_ODR](#job-status-systemcheck-odr) - Auslesen Diagnosefunktion Oeldruckregelung SYSTEMCHECK_ODR (0x2C)
- [STOP_SYSTEMCHECK_ODR](#job-stop-systemcheck-odr) - Diagnosefunktion Oeldruckregelung beenden SYSTEMCHECK_ODR (0x2C)
- [ADAP2_SELEKTIV_LOESCHEN](#job-adap2-selektiv-loeschen) - Ansteuern Adaptionen 2 selektiv loeschen ADAP2_SELEKTIV_LOESCHEN (0x31)
- [START_ZSZ](#job-start-zsz) - Ansteuern des Systemtestes Zuendkerze freibrennen (Kalttestspezifisch) (Anforderung aus CP21228) ZSZ (0x36)
- [STATUS_ZSZ](#job-status-zsz) - Auslesen des Systemtestes Zuendkerze freibrennen (Kalttestspezifisch) (Anforderung aus CP21228) ZSZ (0x36)
- [STOP_ZSZ](#job-stop-zsz) - Ende des Systemtestes Zuendkerze freibrennen (Kalttestspezifisch) (Anforderung aus CP21228) ZSZ (0x36)
- [START_ZSZW](#job-start-zszw) - Ansteuern des Systemtests betriebspunktunabhaengiger (Winkelsynchroner) Zuendspulentest (Kalttestspezifisch) ZSZW (0x37)
- [STATUS_ZSZW](#job-status-zszw) - Auslesen des Systemtests betriebspunktunabhaengiger (Winkelsynchroner) Zuenspulentest (Kalttestspezifisch) ZSZW (0x37)
- [STOP_ZSZW](#job-stop-zszw) - Ende des Systemtests betriebspunktunabhaengiger (Winkelsynchroner) Zuenspulentest (Kalttestspezifisch) ZSZW (0x37)
- [START_EVZ](#job-start-evz) - Ansteuern des Systemtestes Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) (Anforderung aus CP21228) EVZ (0x38)
- [STATUS_EVZ](#job-status-evz) - Auslesen des Systemtestes Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) (Anforderung aus CP21228) EVZ (0x38)
- [STOP_EVZ](#job-stop-evz) - Ende des Systemtestes Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) (Anforderung aus CP21228) EVZ (0x38)
- [START_ZSZZ](#job-start-zszz) - Zeitbasierte Zuendsequenz (Kalttestspezifisch) ZSZZ (0x39)
- [STATUS_ZSZZ](#job-status-zszz) - Zeitbasierte Zuendsequenz (Kalttestspezifisch) ZSZZ (0x39)
- [STOP_ZSZZ](#job-stop-zszz) - Zeitbasierte Zuendsequenz (Kalttestspezifisch) ZSZZ (0x39)
- [START_ZWDIAG](#job-start-zwdiag) - CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Start-Routine ZWDIAG (0x3A)
- [STATUS_ZWDIAG](#job-status-zwdiag) - CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Status-Routine ZWDIAG (0x3A)
- [STOP_ZWDIAG](#job-stop-zwdiag) - CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Stop-Routine ZWDIAG (0x3A)
- [START_VANOSSPUELEN](#job-start-vanosspuelen) - VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0x42)
- [STATUS_VANOSSPUELEN](#job-status-vanosspuelen) - VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0x42)
- [STOP_VANOSSPUELEN](#job-stop-vanosspuelen) - VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0x42)
- [START_SYSTEMCHECK_ATL](#job-start-systemcheck-atl) - Diagnosefunktion Abgasturbolader starten SYSTEMCHECK_ATL (0xD0)
- [STATUS_SYSTEMCHECK_ATL](#job-status-systemcheck-atl) - Diagnosefunktion Abgasturbolader auslesen SYSTEMCHECK_ATL (0xD0)
- [STOP_SYSTEMCHECK_ATL](#job-stop-systemcheck-atl) - Diagnosefunktion Abgasturbolader beenden SYSTEMCHECK_ATL (0xD0)
- [START_SYSTEMCHECK_GLF](#job-start-systemcheck-glf) - Ansteuern Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xD5)
- [STATUS_SYSTEMCHECK_GLF](#job-status-systemcheck-glf) - Auslesen Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xD5)
- [STOP_SYSTEMCHECK_GLF](#job-stop-systemcheck-glf) - Ende Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xD5)
- [START_SYSTEMCHECK_L_REGELUNG_AUS](#job-start-systemcheck-l-regelung-aus) - Ansteuerung Lambdaregelung deaktivieren SYSTEMCHECK_L_REGELUNG_AUS (0xD9)
- [STATUS_SYSTEMCHECK_L_REGELUNG_AUS](#job-status-systemcheck-l-regelung-aus) - Auslesen Lambdaregelung ausschalten SYSTEMCHECK_L_REGELUNG_AUS (0xD9)
- [STOP_SYSTEMCHECK_L_REGELUNG_AUS](#job-stop-systemcheck-l-regelung-aus) - Ende Lambdaregelung ausschalten SYSTEMCHECK_L_REGELUNG_AUS (0xD9)
- [START_SYSTEMCHECK_DMTL](#job-start-systemcheck-dmtl) - Ansteuern Diagnosefunktion DMTL SYSTEMCHECK_DMTL (0xDA)
- [STATUS_SYSTEMCHECK_DMTL](#job-status-systemcheck-dmtl) - Auslesen Diagnosefunktion DMTL SYSTEMCHECK_DMTL (0xDA)
- [STOP_SYSTEMCHECK_DMTL](#job-stop-systemcheck-dmtl) - Diagnosefunktion DMTL beenden SYSTEMCHECK_DMTL (0xDA)
- [START_EISYUGD](#job-start-eisyugd) - Ansteuern Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403) EISYUGD (0xE0)
- [STATUS_EISYUGD](#job-status-eisyugd) - Auslesen Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403) EISYUGD (0xE0)
- [START_EISYGD](#job-start-eisygd) - Ansteuern Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403) EISYGD (0xE1)
- [STATUS_EISYGD](#job-status-eisygd) - Auslesen Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403) EISYGD (0xE1)
- [START_KRANN](#job-start-krann) - Ansteuern Krann-Adaptionswerte (Anforderung aus CP5404) KRANN (0xE3)
- [STATUS_KRANN](#job-status-krann) - Auslesen Krann-Adaptionswerte (Anforderung aus CP5404) KRANN (0xE3)
- [START_KLANN](#job-start-klann) - Ansteuern Klann-Adaptionswerte (Anforderung aus CP10798) KLANN (0xE4)
- [STATUS_KLANN](#job-status-klann) - Auslesen Klann-Adaptionswerte (Anforderung aus CP10798) KLANN (0xE4)
- [START_SYSTEMCHECK_DDLSHK](#job-start-systemcheck-ddlshk) - Ansteuern Dynamik Diagnose Lamdasonden hinter Hauptkat SYSTEMCHECK_DDLSHK (0xE7)
- [STATUS_SYSTEMCHECK_DDLSHK](#job-status-systemcheck-ddlshk) - Auslesen Dynamik Diagnose Lamdasonden hinter Hauptkat SYSTEMCHECK_DDLSHK (0xE7)
- [STOP_SYSTEMCHECK_DDLSHK](#job-stop-systemcheck-ddlshk) - Ende Dynamik Diagnose Lamdasonden hinter Hauptkat SYSTEMCHECK_DDLSHK (0xE7)
- [START_CRAM](#job-start-cram) - Ansteuern RAM-Backup-Werte loeschen CRAM (0xE9)
- [STATUS_CRAM](#job-status-cram) - Auslesen RAM-Backup-Werte loeschen CRAM (0xE9)
- [START_SYSTEMCHECK_DKAT](#job-start-systemcheck-dkat) - Ansteuern Kurztest Kat SYSTEMCHECK_DKAT (0xEB)
- [STATUS_SYSTEMCHECK_DKAT](#job-status-systemcheck-dkat) - Auslesen Kurztest Kat SYSTEMCHECK_DKAT (0xEB)
- [STOP_SYSTEMCHECK_DKAT](#job-stop-systemcheck-dkat) - Ende Kurztest Kat SYSTEMCHECK_DKAT (0xEB)
- [STATUS_SYSTEMCHECK_PM_MESSEMODE](#job-status-systemcheck-pm-messemode) - Auslesen Messemode SYSTEMCHECK_PM_MESSEMODE (0xF6)
- [STEUERN_ENDE_DK](#job-steuern-ende-dk) - Drosselklappe Ansteuerung beenden DK (0x2A00)
- [STEUERN_DK](#job-steuern-dk) - Drosselklappe ansteuern DK (0x2A07)
- [STEUERN_ENDE_UGEN](#job-steuern-ende-ugen) - Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden UGEN (0x3200)
- [STEUERN_UGEN](#job-steuern-ugen) - Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) ansteuern UGEN (0x3207)
- [STATUS_MESSWERTE](#job-status-messwerte) - Messwerte auslesen MESSWERTE (0x4000)
- [STATUS_DFMONITOR](#job-status-dfmonitor) - Batterieladezustand auslesen DFMONITOR (0x4001)
- [STATUS_DIGITAL_1](#job-status-digital-1) - Status Schaltzustaende 1 DIGITAL_1 (0x4002)
- [STATUS_NOCKENWELLE_ADAPTION](#job-status-nockenwelle-adaption) - Nockenwellenadationswerte auslesen NOCKENWELLE_ADAPTION (0x4006)
- [STATUS_DIGITAL_0](#job-status-digital-0) - Status Schaltzustaende 0 DIGITAL_0 (0x4007)
- [STATUS_ADAPTION_DK](#job-status-adaption-dk) - Drosselklappenadaptionswerte auslesen ADAPTION_DK (0x4008)
- [STATUS_ADAPTION_GEMISCH](#job-status-adaption-gemisch) - Gemischadaptionswerte auslesen ADAPTION_GEMISCH (0x400A)
- [STATUS_MESSWERTE_VVT](#job-status-messwerte-vvt) - VVT Messwerte auslesen MESSWERTE_VVT (0x400B)
- [FASTA10](#job-fasta10) - FASTA-Messwertblock 10 lesen FASTA10 (0x4015)
- [STATUS_BZEINFO](#job-status-bzeinfo) - Infospeicher Batterie Zustands Erkennung (BZE) auslesen BZEINFO (0x401A)
- [STATUS_GENINFO](#job-status-geninfo) - Infospeicher Generatordiagnose erweitert auslesen GENINFO (0x401B)
- [STATUS_VERBREDINFO](#job-status-verbredinfo) - Verbraucherreduzierungsspeicher auslesen VERBREDINFO (0x401D)
- [STATUS_DMEREF](#job-status-dmeref) - BMW Programmstands-Bezeichnung auslesen DMEREF (0x401F)
- [STATUS_MESSWERTE_EWAP](#job-status-messwerte-ewap) - elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) Messwerte auslesen MESSWERTE_EWAP (0x4024)
- [STATUS_MESSWERTE_VAD](#job-status-messwerte-vad) - Variantenadaptionen auslesen MESSWERTE_VAD (0x4025)
- [STATUS_RBMMODE9](#job-status-rbmmode9) - Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9) RBMMODE9 (0x4026)
- [STATUS_RBMME1](#job-status-rbmme1) - Rate Based Monitoring Motorsteuerung ME... Block 1 auslesen (Vorhalt) RBMME1 (0x4029)
- [STATUS_RBMME2](#job-status-rbmme2) - Rate Based Monitoring Motorsteuerung ME... Block 2 auslesen (Vorhalt) RBMME2 (0x402A)
- [STATUS_MESSWERTE_IBS](#job-status-messwerte-ibs) - Messwerte IBS auslesen MESSWERTE_IBS (0x402B)
- [STATUS_MESSWERTE_LRP](#job-status-messwerte-lrp) - Messwerte Laufruhepruefung auslesen MESSWERTE_LRP (0x402D)
- [STATUS_KQE](#job-status-kqe) - Messwerte zur Kraftstoffqualitaet auslesen KQE (0x4035)
- [STATUS_INJAD](#job-status-injad) - Injektor Adaptionswerte lesen INJAD (Kleinstmengen-Adaption RB-Umfaenge) INJAD (0x403F)
- [STATUS_ATLDIAG](#job-status-atldiag) - Turboladerstatus auslesen ATLDIAG (0x4044)
- [STATUS_KLANNADAP](#job-status-klannadap) - KLANN Adaptionen auslesen KLANNADAP (0x4046)
- [STATUS_INTEGRITAETDME](#job-status-integritaetdme) - Integritaet DME und Codierzaehler Leistungsklasse, Vmax und maximale V_VEH INTEGRITAETDME (0x4048)
- [STATUS_ZDKSHDP](#job-status-zdkshdp) - Zeitanteile der erreichten Druckbereiche (beim Tausch der Kraftstoffhochdruckpumpe) auslesen. ZDKSHDP (0x404C)
- [STATUS_READINESS](#job-status-readiness) - Monitorfunktionen und Readinessflags aus DME auslesen READINESS (0x4105)
- [STATUS_WRUECKDREHWINKEL](#job-status-wrueckdrehwinkel) - VVT: Mehrfaches Rueckdrehen (Wiederholter Rueckdrehwinkel) lesen. WRUECKDREHWINKEL (0x5F75)
- [STEUERN_WRUECKDREHWINKEL](#job-steuern-wrueckdrehwinkel) - VVT: Mehrfaches Rueckdrehen (Wiederholter Rueckdrehwinkel). Wenn B_favvtexwinksrev gesetzt ist, dann wird der Wert vom Tester (vvt_exwinksrev_count) auf den Zaehler (vvt_exwinksrev) kopiert. WRUECKDREHWINKEL (0x5F75)
- [STEUERN_VVTHIGHCURRENT](#job-steuern-vvthighcurrent) - Anzahl erkannter VVT Lageregelungsfehlerwarnungen irrreversible (VVT-Schwergaengigkeit) vorgeben. VVTHIGHCURRENT (0x5F7A)
- [STATUS_VVTSCHWERGAENGIGKEIT](#job-status-vvtschwergaengigkeit) - Anzahl erkannter VVT Lageregelungsfehler, Anzahl erkannter VVT Lageregelungsfehlerwarnungen irrreversible und Anzahl erkannter VVT Lageregelungsfehlerwarnungen reversible (VVT-Schwergaengigkeit) lesen. VVTSCHWERGAENGIGKEIT (0x5F7B)
- [STEUERN_VVTDEVIATION](#job-steuern-vvtdeviation) - Anzahl erkannter VVT Lageregelungsfehler vorgeben. VVTDEVIATION (0x5F7B)
- [STEUERN_ZDKSHDPRESET](#job-steuern-zdkshdpreset) - Zeitanteile der erreichten Druckbereiche (beim Tausch der Kraftstoffhochdruckpumpe) zuruecksetzen. Beim Aufruf dieses Services soll das Bit B_prail_mon_clr gesetzt werden. ZDKSHDPRESET (0x5F7F)
- [STATUS_GVOBD](#job-status-gvobd) - Gemischvertrimmung fuer OBD-Demo und PVE auslesen. GVOBD (0x5F80)
- [STEUERN_GVOBD](#job-steuern-gvobd) - Gemischvertrimmung fuer OBD-Demo und PVE vorgeben. Der Korrekturfaktor soll bei Klemmenwechsel auf den Standardwert 1 zurueckgesetzt werden. STEUERN_GVOBD (0x5F80)
- [STEUERN_PROGRAMM_GVOBD](#job-steuern-programm-gvobd) - Gemischvertrimmung fuer OBD-Demo und PVE programmieren. STEUERN_PROGRAMM_GVOBD (0x5F80)
- [STATUS_HUBKORR](#job-status-hubkorr) - Hubkorrektur auslesen HUBKORR (0x5F8C)
- [STEUERN_HUBKORR_PROGRAMMIEREN](#job-steuern-hubkorr-programmieren) - Hubkorrektur programmieren STEUERN_HUBKORR_PROGRAMMIEREN (0x5F8C)
- [STEUERN_HUBKORR_RESET](#job-steuern-hubkorr-reset) - Hubkorrektur loeschen STEUERN_HUBKORR_RESET (0x5F8C)
- [STEUERN_HUBKORR_VERSTELLEN](#job-steuern-hubkorr-verstellen) - Hubkorrektur vorgeben STEUERN_HUBKORR_VERSTELLEN (0x5F8C)
- [STATUS_IMAALLE](#job-status-imaalle) - Abgleichwerte Injektoren auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. IMAALLE (0x5F90)
- [STEUERN_IMAALLE](#job-steuern-imaalle) - Abgleichwerte Injektoren programmieren IMAALLE (0x5F90)
- [STEUERN_IMA_ZYL_1](#job-steuern-ima-zyl-1) - Abgleichwert Injektor 01 (phys) programmieren IMA_ZYL_1 (0x5F91)
- [STEUERN_IMA_ZYL_2](#job-steuern-ima-zyl-2) - Abgleichwert Injektor 02 (phys) programmieren IMA_ZYL_2 (0x5F92)
- [STEUERN_IMA_ZYL_3](#job-steuern-ima-zyl-3) - Abgleichwert Injektor 03 (phys) programmieren IMA_ZYL_3 (0x5F93)
- [STEUERN_IMA_ZYL_4](#job-steuern-ima-zyl-4) - Abgleichwert Injektor 04 (phys) programmieren IMA_ZYL_4 (0x5F94)
- [STEUERN_IMA_ZYL_5](#job-steuern-ima-zyl-5) - Abgleichwert Injektor 05 (phys) programmieren IMA_ZYL_5 (0x5F95)
- [STEUERN_IMA_ZYL_6](#job-steuern-ima-zyl-6) - Abgleichwert Injektor 06 (phys) programmieren IMA_ZYL_6 (0x5F96)
- [STEUERN_KVA](#job-steuern-kva) - KraftstoffVerbrauchsAnzeige - Korrekturfaktor schreiben KVA (0x5FC1)
- [STATUS_LL_ABGLEICH](#job-status-ll-abgleich) - Abgleichwert LL (Leerlauf) auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. LL_ABGLEICH (0x5FF0)
- [STEUERN_ENDE_ABLL](#job-steuern-ende-abll) - Abgleichwert LL (Leerlauf) Vorgeben beenden ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. STEUERN_ENDE_ABLL (0x5FF0)
- [STEUERN_LLABG_PROG](#job-steuern-llabg-prog) - Abgleichwert LL (Leerlauf) programmieren ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. STEUERN_LLABG_PROG (0x5FF0)
- [STEUERN_LL_ABGLEICH](#job-steuern-ll-abgleich) - Abgleichwert LL (Leerlauf) vorgeben ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. STEUERN_LL_ABGLEICH (0x5FF0)
- [ECU_CONFIG](#job-ecu-config) - Variante auslesen ECU_CONFIG (0x5FF2)
- [ECU_CONFIG_RESET](#job-ecu-config-reset) - Variante loeschen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. ECU_CONFIG_RESET (0x5FF2)
- [STEUERN_ENDE_GLF2](#job-steuern-ende-glf2) - Gesteuerte Luftfuehrung Klappe 2 Ansteuerung beenden GLF2 (0xA400)
- [STEUERN_GLF2](#job-steuern-glf2) - Gesteuerte Luftfuehrung Klappe 2 ansteuern GLF2 (0xA407)
- [STEUERN_ENDE_ODR](#job-steuern-ende-odr) - Oel Druck Regelung (Geregeltes Oeldrucksystem) Ansteuerung beenden ODR (0xAB00)
- [STEUERN_ODR](#job-steuern-odr) - Oel Druck Regelung (Geregeltes Oeldrucksystem) ansteuern ODR (0xAB07)
- [STEUERN_ENDE_ODV](#job-steuern-ende-odv) - Oeldruckventil (Geregeltes Oeldrucksystem) Ansteuerung beenden ODV (0xAC00)
- [STEUERN_ODV](#job-steuern-odv) - Oeldruckventil (Geregeltes Oeldrucksystem) ansteuern ODV (0xAC07)
- [STEUERN_ENDE_MLS](#job-steuern-ende-mls) - Motorlagersteuerung Ansteuerung beenden MLS (0xB200)
- [STEUERN_MLS](#job-steuern-mls) - Motorlagersteuerung ansteuern MLS (0xB207)
- [STEUERN_ENDE_ULV](#job-steuern-ende-ulv) - Umluftventil Ansteuerung beenden ULV (0xB500)
- [STEUERN_ULV](#job-steuern-ulv) - Umluftventil ansteuern ULV (0xB507)
- [STEUERN_ENDE_LDS1](#job-steuern-ende-lds1) - Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) Ansteuerung beenden LDS1 (0xB600)
- [STEUERN_LDS1](#job-steuern-lds1) - Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) ansteuern LDS1 (0xB607)
- [STEUERN_ENDE_MSV](#job-steuern-ende-msv) - Mengensteuerventil Ansteuerung beenden MSV (0xBD00)
- [STEUERN_MSV](#job-steuern-msv) - Mengensteuerventil ansteuern MSV (0xBD07)
- [STEUERN_ENDE_EWAP](#job-steuern-ende-ewap) - elektr. Wasserpumpe Ansteuerung beenden EWAP (0xBF00)
- [STEUERN_EWAP](#job-steuern-ewap) - elektr. Wasserpumpe (Bit Serielle Datenschnittstelle) ansteuern EWAP (0xBF07)
- [STEUERN_ENDE_AGK](#job-steuern-ende-agk) - Abgasklappe Ansteuerung beenden AGK (0xC100)
- [STEUERN_AGK](#job-steuern-agk) - Abgasklappe ansteuern AGK (0xC107)
- [STEUERN_ENDE_GLF](#job-steuern-ende-glf) - Gesteuerte Luftfuehrung (Klappe 1) Ansteuerung beenden GLF (0xC300)
- [STEUERN_GLF](#job-steuern-glf) - Gesteuerte Luftfuehrung (Klappe 1) ansteuern GLF (0xC307)
- [STEUERN_ENDE_KFT](#job-steuern-ende-kft) - Kennfeldthermostat Ansteuerung beenden KFT (0xC900)
- [STEUERN_KFT](#job-steuern-kft) - Kennfeldthermostat ansteuern KFT (0xC907)
- [STEUERN_ENDE_DMTL_P](#job-steuern-ende-dmtl-p) - Diagnosemodul-Tank Leckage Pumpe Ansteuerung beenden DMTL_P (0xCC00)
- [STEUERN_DMTL_P](#job-steuern-dmtl-p) - Diagnosemodul-Tank Leckage Pumpe ansteuern DMTL_P (0xCC07)
- [STEUERN_ENDE_DMTL_V](#job-steuern-ende-dmtl-v) - Diagnosemodul-Tank Leckage Ventil Ansteuerung beenden DMTL_V (0xCD00)
- [STEUERN_DMTL_V](#job-steuern-dmtl-v) - Diagnosemodul-Tank Leckage Ventil ansteuern DMTL_V (0xCD07)
- [STEUERN_ENDE_DMTL_HEIZUNG](#job-steuern-ende-dmtl-heizung) - Diagnosemodul-Tank Leckage Heizung Ansteuerung beenden DMTL_HEIZUNG (0xCE00)
- [STEUERN_DMTL_HEIZUNG](#job-steuern-dmtl-heizung) - Diagnosemodul-Tank Leckage Heizung ansteuern DMTL_HEIZUNG (0xCE07)
- [STEUERN_ENDE_TEV](#job-steuern-ende-tev) - Tankentlueftungsventil Ansteuerung beenden TEV (0xCF00)
- [STEUERN_TEV](#job-steuern-tev) - Tankentlueftungsventil ansteuern TEV (0xCF07)
- [STEUERN_ENDE_LSH1](#job-steuern-ende-lsh1) - Lambdasondenheizung vor Kat Bank1 Ansteuerung beenden LSH1 (0xD000)
- [STEUERN_LSH1](#job-steuern-lsh1) - Lambdasondenheizung vor Kat Bank1 ansteuern LSH1 (0xD007)
- [STEUERN_ENDE_LSH2](#job-steuern-ende-lsh2) - Lambdasondenheizung hinter Kat Bank1 Ansteuerung beenden LSH2 (0xD100)
- [STEUERN_LSH2](#job-steuern-lsh2) - Lambdasondenheizung hinter Kat Bank1 ansteuern LSH2 (0xD107)
- [STEUERN_ENDE_MIL](#job-steuern-ende-mil) - MIL (Malfunction Indicator Lamp) Ansteuerung beenden MIL (0xD400)
- [STEUERN_MIL](#job-steuern-mil) - MIL (Malfunction Indicator Lamp) ansteuern MIL (0xD407)
- [STEUERN_ENDE_EML](#job-steuern-ende-eml) - EML (Engine Malfunction Lamp) Ansteuerung beenden EML (0xD600)
- [STEUERN_EML](#job-steuern-eml) - EML (Engine Malfunction Lamp) ansteuern EML (0xD607)
- [STEUERN_ENDE_EKP](#job-steuern-ende-ekp) - Elektrische Kraftstoffpumpe 1 Ansteuerung beenden Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben EKP (0xD800)
- [STEUERN_EKP](#job-steuern-ekp) - Elektrische Kraftstoffpumpe 1 ansteuern Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben EKP (0xD807)
- [STEUERN_ENDE_E_LUEFTER](#job-steuern-ende-e-luefter) - E-Luefter Ansteuerung beenden E_LUEFTER (0xDA00)
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - E-Luefter ansteuern E_LUEFTER (0xDA07)
- [STEUERN_ENDE_VVT](#job-steuern-ende-vvt) - VVT Ansteuerung beenden VVT (0xDD00)
- [STEUERN_VVT](#job-steuern-vvt) - VVT ansteuern VVT (0xDD07)
- [STEUERN_ENDE_EV1](#job-steuern-ende-ev1) - Einspritzventil 1 (physikalisch) Ansteuerung beenden EV1 (0xE100)
- [STEUERN_EV1](#job-steuern-ev1) - Einspritzventil 1 (physikalisch) ansteuern EV1 (0xE107)
- [STEUERN_ENDE_EV2](#job-steuern-ende-ev2) - Einspritzventil 2 (physikalisch) Ansteuerung beenden EV2 (0xE200)
- [STEUERN_EV2](#job-steuern-ev2) - Einspritzventil 2 (physikalisch) ansteuern EV2 (0xE207)
- [STEUERN_ENDE_EV3](#job-steuern-ende-ev3) - Einspritzventil 3 (physikalisch) Ansteuerung beenden EV3 (0xE300)
- [STEUERN_EV3](#job-steuern-ev3) - Einspritzventil 3 (physikalisch) ansteuern EV3 (0xE307)
- [STEUERN_ENDE_EV4](#job-steuern-ende-ev4) - Einspritzventil 4 (physikalisch) Ansteuerung beenden EV4 (0xE400)
- [STEUERN_EV4](#job-steuern-ev4) - Einspritzventil 4 (physikalisch) ansteuern EV4 (0xE407)
- [STEUERN_ENDE_EV5](#job-steuern-ende-ev5) - Einspritzventil 5 (physikalisch) Ansteuerung beenden EV5 (0xE500)
- [STEUERN_EV5](#job-steuern-ev5) - Einspritzventil 5 (physikalisch) ansteuern EV5 (0xE507)
- [STEUERN_ENDE_EV6](#job-steuern-ende-ev6) - Einspritzventil 6 Ansteuerung (physikalisch) beenden EV6 (0xE600)
- [STEUERN_EV6](#job-steuern-ev6) - Einspritzventil 6 (physikalisch) ansteuern EV6 (0xE607)
- [STEUERN_ENDE_ENWS](#job-steuern-ende-enws) - Vanos Einlass Ventil Ansteuerung beenden ENWS (0xED00)
- [STEUERN_ENWS](#job-steuern-enws) - Vanos Einlass Ventil ansteuern ENWS (0xED07)
- [STEUERN_ENDE_ANWS](#job-steuern-ende-anws) - Vanos Auslass Ventil Ansteuerung beenden ANWS (0xEE00)
- [STEUERN_ANWS](#job-steuern-anws) - Vanos Auslass Ventil ansteuern ANWS (0xEE07)
- [STEUERN_ENDE_TEAV](#job-steuern-ende-teav) - Absperrventil Tankentlueftung (Steuern-Ende) TEAV (0xFC00)
- [STEUERN_TEAV](#job-steuern-teav) - Absperrventil Tankentlueftung Ansteuerung TEAV (0xFC07)
- [STATUS_RUHESTROMMESSUNG](#job-status-ruhestrommessung) - Auslesen Ruhestrompruefung mit IBS RUHESTROMMESSUNG (0x2B)
- [STEUERN_RUHESTROMMESSUNG](#job-steuern-ruhestrommessung) - Ansteuern Ruhestrompruefung mit IBS RUHESTROMMESSUNG (0x2B) Aktivierung: Klemme 15 = EIN
- [START_SYSTEMCHECK_LLERH](#job-start-systemcheck-llerh) - Ansteuern Diagnosefunktion Leerlauf-Erhoehung SYSTEMCHECK_LLERH (0x26)
- [STOP_SYSTEMCHECK_LLERH](#job-stop-systemcheck-llerh) - Diagnosefunktion Leerlauf-Erhoehung beenden SYSTEMCHECK_LLERH (0x26)
- [STATUS_SYSTEMCHECK_LLERH](#job-status-systemcheck-llerh) - Auslesen Diagnosefunktion Leerlauf-Erhoehung SYSTEMCHECK_LLERH (0x26)
- [IDENT_IBS](#job-ident-ibs) - $22 40 21 BMW Nr, Seriennummer, SW/HW Index

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

<a id="job-sensoren-anzahl-lesen"></a>
### SENSOREN_ANZAHL_LESEN

Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_ANZAHL | long | Anzahl der intelligenten Subbussensoren |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sensoren-ident-lesen"></a>
### SENSOREN_IDENT_LESEN

Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_NR | long | optionales Argument gewuenschter Sensor xx (0x01 - 0xFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_VERBAUORT | string | Verbauort des Sensors table VerbauortTabelle ORTTEXT |
| SENSOR_BMW_NR | string | BMW-Teilenummer des Sensors |
| SENSOR_PART_NR | string | Teilenummer des Sensors optional wenn SENSOR_BMW_NR gueltig wenn vom Teilenummer vom Sensor nicht verfuegbar dann '--' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-status-messwertblock-lesen"></a>
### STATUS_MESSWERTBLOCK_LESEN

Lesen eines Messwertblockes Es muss immer das BlockSchreibenFlag und mindestens ein MESSWERT uebergeben werden. KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $04 ClearDynamicallyDefinedLocalIdentifier KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $02 DefineByCommonIdentifier KWP2000: $21 ReadDataByLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Wenn 'JA' wird der Messwertblock im SG gelöscht neu ins SG geschrieben und dann gelesen Wenn 'NEIN' wird der Messwertblock im SG nicht gelöscht Es wird der im SG gespeicherte Messwertblock gelesen table MesswerteMode TEXT KOMMENTAR |
| MESSWERT | string | Dynamische Argumente Es können bis zu 42 Argumente übergeben werden Es muss mindestens ein Argument übergeben werden Er wird das zugehörige Result table MesswerteTab ARG RESULTNAME erzeugt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |

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
| AVAI_CBS_WERT_DAD | int | Verfuegbarkeit DAD in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_ZKRZ_A | int | Verfuegbarkeit ZKRZ_A in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_H2 | int | Verfuegbarkeit H2 in %, fuer Pruefablauf Bandende |
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
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, ZKrz, Sic, Kfl, TUV, AU, Ueb, H2 Werte externe Umfaenge: Oel, Br_v, Br_h, Filt, CSF, Batt, VTG, ZKrz_a, DAD Defaultwert: 0x00 (ungueltig) |
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

<a id="job-messwertblock-lesen"></a>
### MESSWERTBLOCK_LESEN

0x2CF0 MESSWERTBLOCK_LESEN DDLI Messwerte auf Basis Übergabestring aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1 es können 40 Messwerte in einem Block zusammengefasst werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STRING_IN | string | Werte aus DDLI Liste Format 0x58XX,0x42YY,0x43ZZ,... |
| TRENNZEICHEN | string | Werte aus DDLI Liste Format 0x58XX,0x42YY,0x43ZZ,... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL_WERTE | int | Anzahl Messwerte 0 bis n dezimal ansteigend |
| STAT_MESSWERT0_WERT | real | real Wert |
| STAT_MESSWERT0_STRING | string | String mit 10 signifikanten Stellen |
| STAT_MESSWERT0_TEXT | string | Text der Variablen aus INFO |
| STAT_MESSWERT0_EINH | string | Einheit der Variablen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an  SG Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG Block löschen |
| _TEL_AUFTRAG | binary | Hex-Auftrag an  SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an  SG Block lesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG Block lesen |

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

<a id="job-is-lesen"></a>
### IS_LESEN

0x222000 IS_LESEN Infospeicher lesen (alle Info-Meldungen / Ort und Art) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text aus Tabelle FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen-detail"></a>
### IS_LESEN_DETAIL

Infospeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default

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

<a id="job-status-betriebsstundenzaehler"></a>
### STATUS_BETRIEBSSTUNDENZAEHLER

0x2CF0 5AB4 STATUS_BETRIEBSSTUNDENZAEHLER Betriebsstundenzaehler auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BSZ_WERT | unsigned long | Auswertung Betriebsstundenzaehler TRT_FLAG |
| STAT_BSZ_TEXT | string | Status Betriebsstundenzaehler |
| STAT_TRT_WERT | real | Betriebsstundenzaehler TRT |
| STAT_TRT_EINH | string | h |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-aif"></a>
### IDENT_AIF

0x1A80 und 0x23 IDENT_AIF Identdaten und Anwender Informations Felder Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
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
| ID_LIEF_TEXT | string | Lieferanten-Text nach Tabelle Lieferanten |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) |
| AIF_ADRESSE | long | AIF Adresse |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| AIF_PROGRAMMIER_DATUM | string | Datum der SG-Programmierung in der Form JJJJ.MM.TT |
| AIF_ZUSAMMENBAU_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_DATENSATZ_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_TESTER_NR | string | Tester Seriennummer |
| AIF_KM_STAND | long | km-Stand bei der Programmierung |
| AIF_PROGRAMM_STAND | string | Programmstandsnummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZ_DATEN | int | Groesse des AIF-Eintrags |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleichwerte-schreiben"></a>
### ABGLEICHWERTE_SCHREIBEN

0x2E5F90 ABGLEICHWERTE_SCHREIBEN Abgleichwerte Injektoren programmieren für CASCADE mit Übernahme Daten aus COD-Datei Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_DATEN | string | Abgleichdaten für alle Injektoren aus COD-Datei |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_ABGLEICHDATEN | string | Abgleichdaten zum Steuergeraet |
| ABGLEICHWERTE_SCHREIBEN_PRUEFZEICHEN | string | das im Job berechnete Pruefzeichen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleichwerte-lesen"></a>
### ABGLEICHWERTE_LESEN

0x225F90 ABGLEICHWERTE_LESEN Abgleichwerte Injektoren auslesen für CASCADE für Vergleich mit Daten aus COD-Datei Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_DATEN | string | Abgleichdaten für alle Injektoren aus COD-Datei |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_LESEN_DATEN | string | Abgleichdaten für alle Injektoren aus COD-Datei nach Anwendung Umrechnungsmethoden |
| ABGLEICHWERTE_LESEN_ABGLEICHDATEN | string | Abgleichdaten für alle Injektoren aus Steuergeraet |
| ABGLEICHWERTE_LESEN_VERGLEICHSBIT_WERT | int | das im Job berechnete Vergleichsergebnis für Übereinstimmung zwischen COD- und DME-Werten |
| ABGLEICHWERTE_LESEN_VERGLEICHSBIT_TEXT | string | das im Job berechnete Vergleichsergebnis für Übereinstimmung zwischen COD- und DME-Werten als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ews"></a>
### STATUS_EWS

KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC000 Zurücklesen verschiedener interner Stati für EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS3_CAPABLE | int | 0 Das SG beherrscht kein EWS3 1 Das SG beherrscht EWS3 |
| STAT_EWS4_CAPABLE | int | 0 Das SG beherrscht kein EWS4 1 Das SG beherrscht EWS4 |
| STAT_EWS3_ACTIVE | int | 0 EWS3 ist nicht (mehr) aktiv 1 EWS3 ist aktiv (oder lässt sich aktivieren) |
| STAT_EWS4_ACTIVE | int | 0 EWS4 ist nicht aktiv 1 EWS4 ist aktiv |
| STAT_EWS4_SERVER_SK_LOCKED | int | 0 SecretKey server lässt sich noch direkt schreiben 1 SecretKey server lässt sich nicht mehr schreiben/lesen |
| STAT_EWS4_CLIENT_SK_LOCKED | int | 0 SecretKey client lässt sich noch direkt schreiben 1 SecretKey client lässt sich nicht mehr schreiben/lesen |
| STAT_CLIENT_AUTHENTICATED | int | 0 Freigabe von Zuendung und Einspritzung (noch) nicht erteilt (noch nicht versucht oder Kommunikation gestört, Motorlauf gesperrt) 1 Freigabe von Zuendung und Einspritzung erteilt (Challenge-Response erfolgreich) 2 Freigabe von Zuendung und Einspritzung abgelehnt (Challenge-Response fehlgeschlagen, falsche Response, Kommunikation i.O.) 3 nicht definiert |
| STAT_CLIENT_AUTHENTICATED_TXT | string | Text zu Status Wert |
| STAT_FREE_SK0 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK0_TXT | string | Freie Plaetze |
| STAT_FREE_SK1 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK1_TXT | string | Freie Plaetze |
| STAT_VERSION | int | 0x01 Direktschreiben des SecretKey 0x02 Direktschreiben des SecretKey und DH-Abgleich |
| _STAT_VERSION_TXT | string | Version |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ews4-sk"></a>
### STATUS_EWS4_SK

KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC002 Lesen des SecretKey des Server sowie Client für EWS4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS4_SERVER_SK | binary | SecretKey Server |
| STAT_EWS4_CLIENT_SK | binary | SecretKey Client |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ews4-sk"></a>
### STEUERN_EWS4_SK

17 "EWS4-data" schreiben KWP 2000: $2E WriteDataByCommonIdentifier CommonIdentifier=0xC001

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Byte0 LOCK_SERVER_SK LOCK_CLIENT_SK WRITE_SERVER_SK WRITE_CLIENT_SK UNLOCK_CLIENT_SK |
| DATA | string | Byte1...16 16 Byte Daten (SecretKey), falls MODE = WRITE_SERVER_SK/WRITE_CLIENT_SK, "0x01,0x02,.." KEINE Daten nötig, falls MODE = LOCK_SERVER_SK/LOCK_CLIENT_SK |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-xxl"></a>
### FLASH_SCHREIBEN_XXL

0x36 FLASH_SCHREIBEN_XXL Flash Daten schreiben XXL-Format, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_ANZAHL | unsigned int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
| FLASH_SCHREIBEN_STATUS | int | Programmierstatus 1 = Programmierung in Ordnung 2 = Programmierung nicht in Ordnung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-adresse-4byte"></a>
### FLASH_SCHREIBEN_ADRESSE_4BYTE

0x34 FLASH_SCHREIBEN_ADRESSE_4BYTE Flash Daten schreiben, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge ohne Telegramm-Overhead |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-loeschen-4byte"></a>
### FLASH_LOESCHEN_4BYTE

0x3102 FLASH_LOESCHEN_4BYTE Flash löschen, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Loeschzeit in Sekunden (Byteparameter 1) Byte 5,6            : Loeschzeit in Sekunden (WordParameter 1 (low/high)) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN_STATUS | int | Loeschstatus 1 = Speicher geloescht 2 = Speicher nicht geloescht 5 = Signaturpruefung PAF nicht durchgefuehrt |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-ende-4byte"></a>
### FLASH_SCHREIBEN_ENDE_4BYTE

0x37 FLASH_SCHREIBEN_ENDE_4BYTE Flashprogrammierung abschliessen, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-igr-aus"></a>
### START_SYSTEMCHECK_IGR_AUS

0x31F7 START_SYSTEMCHECK_IGR_AUS Ansteuerung Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-igr-aus"></a>
### STOP_SYSTEMCHECK_IGR_AUS

0x32F7 STOP_SYSTEMCHECK_IGR_AUS Ansteuerung Intelligente Generatorregelung deaktivieren beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-igr-aus"></a>
### STATUS_SYSTEMCHECK_IGR_AUS

0x33F7 STATUS_SYSTEMCHECK_IGR_AUS Auslesen Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_IGR_TEXT | string | Funktionsstatus Intelligente Generatorregelung B_DIAGIGR |
| STAT_SYSTEMCHECK_IGR_WERT | int | Funktionsstatus Intelligente Generatorregelung B_DIAGIGR |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-igrinfo"></a>
### STATUS_IGRINFO

0x224016 STATUS_IGRINFO Infospeicher Intelligente Generator Regelung (IGR) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IGR1_BITS7 | unsigned long | Begrenzung 2 1BIT IDENTICAL |
| STAT_IGR1_BITS6 | unsigned long | Begrenzung 1 1BIT IDENTICAL |
| STAT_IGR1_BITS5 | unsigned long | Regeneration 1BIT IDENTICAL |
| STAT_IGR1_BITS4 | unsigned long | IGR-Medium 1BIT IDENTICAL |
| STAT_IGR1_BITS3 | unsigned long | IGR-High 1BIT IDENTICAL |
| STAT_IGR1_BITS2 | unsigned long | IGR-Low 1BIT IDENTICAL |
| STAT_IGR1_BITS1 | unsigned long | Diagnosejob gesetzt 1BIT IDENTICAL |
| STAT_IGR1_BITS0 | unsigned long | IGR codiert 1BIT IDENTICAL |
| STAT_IGR2_BITS7 | unsigned long | Zyklisierung MSA 1BIT IDENTICAL |
| STAT_IGR2_BITS6 | unsigned long | Begrenzung DS 1BIT IDENTICAL |
| STAT_IGR2_BITS5 | unsigned long | Begrenzung TS 1BIT IDENTICAL |
| STAT_IGR2_BITS4 | unsigned long | Begrenzung TB 1BIT IDENTICAL |
| STAT_IGR2_BITS3 | unsigned long | Begrenzung M 1BIT IDENTICAL |
| STAT_IGR2_BITS2 | unsigned long | Begrenzung G 1BIT IDENTICAL |
| STAT_IGR2_BITS1 | unsigned long | Begrenzung W 1BIT IDENTICAL |
| STAT_IGR2_BITS0 | unsigned long | Begrenzung L 1BIT IDENTICAL |
| STAT_IGR3_BITS7 | unsigned long | IGR Res2 1BIT IDENTICAL |
| STAT_IGR3_BITS6 | unsigned long | IGR Res1 1BIT IDENTICAL |
| STAT_IGR3_BITS5 | unsigned long | IGR-Hi Aktiv 1BIT IDENTICAL |
| STAT_IGR3_BITS4 | unsigned long | IGR-Med Aktiv 1BIT IDENTICAL |
| STAT_IGR3_BITS3 | unsigned long | IGR-Low Aktiv 1BIT IDENTICAL |
| STAT_IGR3_BITS2 | unsigned long | IGR-Hi Enabled 1BIT IDENTICAL |
| STAT_IGR3_BITS1 | unsigned long | IGR-Med Enabled 1BIT IDENTICAL |
| STAT_IGR3_BITS0 | unsigned long | IGR-Low Enabled 1BIT IDENTICAL |
| STAT_IGR_PR1 | unsigned long | Level BN Soll 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_PR2 | unsigned long | Level Soll 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_ANTL_WERT | real | Anteil Low 2BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.9969482421875 |
| STAT_IGR_ANTL_EINH | string | percent |
| STAT_IGR_ANTM_WERT | real | Anteil Medium 2BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.9969482421875 |
| STAT_IGR_ANTM_EINH | string | percent |
| STAT_IGR_ANTH_WERT | real | Anteil High 2BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.9969482421875 |
| STAT_IGR_ANTH_EINH | string | percent |
| STAT_IGR_11 | unsigned long | Anteil 11 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_12 | unsigned long | Anteil 12 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_M_AGO_WERT | unsigned long | Abstand zu letzter Mediumphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_M_AGO_EINH | string | Minute |
| STAT_IGR_H_AGO_WERT | unsigned long | Abstand zu letzter Highphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_H_AGO_EINH | string | Minute |
| STAT_IGR_BSA1 | unsigned long | Zaehler Low 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_IGR_QLAD_WERT | real | Bilanz Low 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_QLAD_EINH | string | Ah |
| STAT_IGR_QLAD_M_WERT | long | Bilanz Medium IGRINFO_1BYTE_in_minus128bis127Ah   Einheit: Ah   Min: -128 Max: 127 |
| STAT_IGR_QLAD_M_EINH | string | Ah |
| STAT_IGR_QELAD_WERT | real | Bilanz High 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_QELAD_EINH | string | Ah |
| STAT_IGR_TMED_WERT | unsigned long | Dauer letzte Mediumphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_TMED_EINH | string | Minute |
| STAT_IGR_THIGH_WERT | unsigned long | Dauer letzte Highphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_THIGH_EINH | string | Minute |
| STAT_IGR_TCODE | unsigned long | Dauer iGR-Codiert 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_IGR_HIGH | unsigned long | Zaehler High 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_REG_ZR | unsigned long | Einfachzaehler 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_REG_SEIT_WERT | unsigned long | Zeit seit letzter R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_SEIT_EINH | string | h |
| STAT_REG_DAUER_WERT | unsigned long | Dauer letzte R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_DAUER_EINH | string | h |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-leminfo"></a>
### STATUS_LEMINFO

0x224017 STATUS_LEMINFO Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZR_USTAT_A | unsigned long | Haeufigkeitszaehler Zr_ustat_A 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_B | unsigned long | Haeufigkeitszaehler Zr_ustat_B 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_C | unsigned long | Haeufigkeitszaehler Zr_ustat_C 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_D | unsigned long | Haeufigkeitszaehler Zr_ustat_D 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_E | unsigned long | Haeufigkeitszaehler Zr_ustat_E 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_F | unsigned long | Haeufigkeitszaehler Zr_ustat_F 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_G | unsigned long | Haeufigkeitszaehler Zr_ustat_G 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_UBSTUFE_L | unsigned long | Haeufigkeitszaehler Zr_ubstufe_L 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UBSTUFE_H | unsigned long | Haeufigkeitszaehler Zr_ubstufe_H 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UQUALI_A | unsigned long | Haeufigkeitszaehler Zr_uquali_A 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UQUALI_B | unsigned long | Haeufigkeitszaehler Zr_uquali_B 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UQUALI_C | unsigned long | Haeufigkeitszaehler Zr_uquali_C 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_IERRLLRED | unsigned long | Haeufigkeitszaehler Zr_ierrllred 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_TM_IERRLLRED_WERT | unsigned long | Mittelwert Tm_ierrllred 1BYTE_in_0bis255s   Einheit: s   Min: 0 Max: 255 |
| STAT_TM_IERRLLRED_EINH | string | second |
| STAT_ZR_IERRTRED | unsigned long | Haeufigkeitszaehler Zr_ierrtred 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_TM_IERRTRED_WERT | unsigned long | Mittelwert Tm_ierrtred 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |
| STAT_TM_IERRTRED_EINH | string | second |
| STAT_TM_ENTLFUNK_WERT | unsigned long | Mittelwert Tm_entlfunk 1BYTE_in_0bis255s   Einheit: s   Min: 0 Max: 255 |
| STAT_TM_ENTLFUNK_EINH | string | second |
| STAT_ZR_ENTLFUNK | unsigned long | Haeufigkeitszaehler Zr_entlfunk 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_ENTLFUNKVOLL | unsigned long | Haeufigkeitszaehler Zr_entlfunkvoll 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_ENTLFUNKNIX | unsigned long | Haeufigkeitszaehler Zr_entlfunknix 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_ENTLFUNKTEIL | unsigned long | Haeufigkeitszaehler Zr_entlfunkteil 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_TM_ENTLSICH_WERT | unsigned long | Mittelwert Tm_entlsich 1BYTE_in_0bis255s   Einheit: s   Min: 0 Max: 255 |
| STAT_TM_ENTLSICH_EINH | string | second |
| STAT_ZR_ENTLSICH | unsigned long | Haeufigkeitszaehler Zr_entelsich 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_ENTLSICHVOLL | unsigned long | Haeufigkeitszaehler Zr_entelsichvoll 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-pm-info-1"></a>
### STATUS_SYSTEMCHECK_PM_INFO_1

$22 40 22 Bytefeld 1 Batterie Powermanagement lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_RUHESTROMANALYSE_MODE_WERT | int | Modus der Ruhestromanalyse (1 = als Histogramm (nicht Layer), 2 = Bitcodiert für 32 Zyklen (Layer)) |
| STAT_RUHESTROMANALYSE_MODE_TEXT | string | Modus der Ruhestromanalyse (1 = als Histogramm (nicht Layer), 2 = Bitcodiert für 32 Zyklen (Layer)) |
| STAT_BATTERIELADUNG_BILANZ_WERT | real | Differenz LADUNG - ENTLADUNG in Ah 0 - 19088 |
| STAT_BATTERIELADUNG_BILANZ_EINH | string | Einheit |
| STAT_BATTERIELADUNG_GESAMT_WERT | real | Batterie Ladungen in Ah 0 - 19088 |
| STAT_BATTERIELADUNG_GESAMT_EINH | string | Einheit |
| STAT_BATTERIEENTLADUNG_GESAMT_WERT | real | Batterie Ladungen in Ah 0 - 19088 |
| STAT_BATTERIEENTLADUNG_GESAMT_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_0_20_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_0_20_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_20_40_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_20_40_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_40_60_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_40_60_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_60_80_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_60_80_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_80_100_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_80_100_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_0_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_0_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_0_20_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_0_20_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_20_40_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_20_40_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_40_60_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_40_60_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_AB_60_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_AB_60_EINH | string | Einheit |
| STAT_KM_STAND_AKTUELL_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_AKTUELL_EINH | string | Einheit |
| STAT_KM_STAND_VOR_1_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_1_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_2_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_2_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_3_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_3_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_4_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_4_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_5_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_5_TAG_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_LETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_LETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_DRITTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_DRITTLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_VIERTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_VIERTLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_FUENFTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_FUENFTLETZTER_EINH | string | Einheit |
| STAT_BATTENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_WERT | real | 0 - 19088 Ah |
| STAT_BATTENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_EINH | string | Einheit Ah |
| STAT_RUHESTROM_AKTUELL | string |  |
| STAT_RUHESTROM_VOR_1_ZYKLUS | string |  |
| STAT_RUHESTROM_VOR_2_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_3_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_4_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_5_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_6_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_7_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_8_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_9_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_10_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_11_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_12_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_13_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_14_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_15_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_16_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_17_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_18_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_19_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_20_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_21_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_22_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_23_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_24_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_25_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_26_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_27_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_28_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_29_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_30_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_31_ZYKLEN | string |  |
| STAT_IBS_FEHLERZAEHLER_BSD_PARITY_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_BSD_PARITY_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_WATCHDOG_RESET_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_WATCHDOG_RESET_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_POWER_ON_RESET_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_POWER_ON_RESET_EINH | string | Einheit |
| STAT_KTBS_FEHLERZAEHLER_BSD_ERWEITERT_WERT | real | Anzahl 0 - 65535 |
| STAT_KTBS_FEHLERZAEHLER_BSD_ERWEITERT_EINH | string | Einheit |
| STAT_KTIBS_FEHLERZAEHLER_BSD_WERT | real | Anzahl 0 - 65535 |
| STAT_KTIBS_FEHLERZAEHLER_BSD_EINH | string | Einheit |
| STAT_KTIBS_FEHLERZAEHLER_EBSD_CHECKSUMME_WERT | real | Anzahl 0 - 65535 |
| STAT_KTIBS_FEHLERZAEHLER_EBSD_CHECKSUMME_EINH | string | Einheit |

<a id="job-status-systemcheck-pm-info-2"></a>
### STATUS_SYSTEMCHECK_PM_INFO_2

$22 40 23 Bytefeld 2 Batterie Powermanagement lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_BATTERIE_KAPAZITAET_WERT | real | Batterie Kapazitaet in Ah 0 - 255 |
| STAT_BATTERIE_KAPAZITAET_EINH | string | Einheit |
| STAT_SOH_WERT | real | Bereich -50% - 49,6% |
| STAT_SOH_EINH | string | Einheit |
| STAT_SOC_FIT_WERT | real | Bereich 0-100% |
| STAT_SOC_FIT_EINH | string | Einheit |
| STAT_TEMP_SAISON_WERT | real | Bereich -128C - 127C |
| STAT_TEMP_SAISON_EINH | string | Einheit C |
| STAT_KALIBRIER_EVENT_CNT_WERT | real | Kalibrieranzahl 0 - 255 |
| STAT_KALIBRIER_EVENT_CNT_EINH | string | Einheit |
| STAT_Q_SOC_AKTUELL_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_AKTUELL_EINH | string | Einheit |
| STAT_Q_SOC_VOR_1_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_1_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_2_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_2_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_3_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_3_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_4_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_4_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_5_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_5_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_AKTUELL_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_AKTUELL_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_DOWNLOAD_CHECKSUMME_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_DOWNLOAD_CHECKSUMME_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_EEPROM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_EEPROM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_RAM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_RAM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_PROM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_PROM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_I2C_NAC_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_I2C_NAC_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_I2C_BUS_COLLISION_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_I2C_BUS_COLLISION_EINH | string | Einheit |

<a id="job-steuern-pm-histogram-reset"></a>
### STEUERN_PM_HISTOGRAM_RESET

$30 F5 04 Loeschen von pminfo1 index 23-30

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adap-selektiv-loeschen"></a>
### ADAP_SELEKTIV_LOESCHEN

Löschen von Adaptionen und gelernte Varianten KWP 2000 $31 30 xx xx xx Loeschen der Adaptionswerte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_2 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_3 | int | Bit=1 löscht Bit=0 behält alten Wert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-batterietausch-registrieren"></a>
### STEUERN_BATTERIETAUSCH_REGISTRIEREN

KWP 2000 $31 30 00 10 00 Bit setzen Batterietausch registrieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-pm-messemode"></a>
### START_SYSTEMCHECK_PM_MESSEMODE

$31 F6 Systemdiagnose BatterieSensor reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-pm-messemode"></a>
### STOP_SYSTEMCHECK_PM_MESSEMODE

$32 F6 Systemdiagnose BatterieSensor reset beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-individualdata-liste"></a>
### LESEN_INDIVIDUALDATA_LISTE

Lesen eines Listeneintrags der Individualisierungsdaten KWP2000: $21 ReadDataByLocalIdentifier (not used) $01 recordLocalIdentifier (not used)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LISTENTRY | unsigned int | Nummer des angeforderten Listenelements (0,1,2,...) 0x0000 = Anforderung, das 1. Listelement zu senden 0x0001 = Anforderung, das 2. Listelement zu senden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_ENTRYNR | unsigned int | Nummer des zurückgegebenen Listenelements (0,1,2,...) |
| RET_STATUS | unsigned char | Information ob aktuelles Listenelement das Letzte ist 0xFF	letztes Listenelement 0xFE	Listenelement nicht gefunden 0x00 	nicht letztes Listenelement |
| RET_FROMWHERE | unsigned char | Strategienummer 0x01	via 22 5F 8B |
| RET_DATA | binary | Listentry zur Individualdaten-Abfrage 1.Byte, Diagnoseadresse (for future use), diese gibt Auskunft von welchem SG die Individualdaten verwaltet werden. z.B. 0x63  2.Byte:	Sind die Daten Car- oder Key- Memory relevant? 0x01	CarMemory relevant 0x02	KeyMemory relevant 0x03	CarMemory relevant und KeyMemory relevant  3.Byte:	 Strategienummer 0x01	via 22 5F 8B  4.Byte und Folgende siehe Spec Datenrettung  |
| RET_COMMENT | string | Kommentarspalte des Entries |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-lese-individualdata"></a>
### LESE_INDIVIDUALDATA

Lesen von Individualisierungsdaten Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KEYID | unsigned char | 0x00       CarMemory 0x01..0x04 Schlüsselnummer dem der RET_DATA zugeordnet ist 0xFF	   Aktuell gesteckter Schlüssel ist RET_DATA zugeordnet (not used) |
| ARG_BLOCKNR | unsigned long | Zu übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 (4 Bytes) falls nicht verwendet als Dummy mitschleifen |
| ARG_FROMWHERE | unsigned char | Strategienummer 0x01	= PM Recovery 0x02	= AD Recovery |
| ARG_INQY_LEN | unsigned char | Länge des folgenden Anfragedatenstreams (not used) z.B. 0x02 für 2 Byte |
| ARG_INQY_DATA | string | ASCII-codiert Anfrage Individualdatenstream (not used) |
| ARG_RESP_LEN | unsigned char | Länge der folgenden Information wie die Antwort erhalten wird. Also ein Antwortfilter bzw. -hinweis (not used) |
| ARG_RESP_DATA | string | ASCII-codiert Information wie die Antwort erhalten wird: Also ein Antwortfilter bzw. -hinweis (not used) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | 0xFF letztes oder einziges element des Datenstreams 0x00 es folgen weitere Datenstreamstücke |
| RET_BLOCKNR | unsigned long | Übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 falls nicht verwendet als Dummy mitschleifen |
| RET_LEN | int | Länge des Individualisierungs Datenstream oder -streamstücks |
| RET_DATA | binary | Individualisierungs Datenstream |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-individualdata"></a>
### SCHREIBEN_INDIVIDUALDATA

Schreiben von Individualisierungsdaten Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KEYID | unsigned char | 0x00       CarMemory 0x01..0x04 Schlüsselnummer dem der ARG_DATA zugeordnet ist 0xFF	   Aktuell gesteckter Schlüssel ist ARG_DATA zugeordnet (not used) |
| ARG_BLOCKNR | unsigned long | Zu übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 (4 Bytes) falls nicht verwendet als Dummy mitschleifen |
| ARG_FROMWHERE | unsigned char | Strategienummer 0x01	= PM Recovery 0x02	= AD Recovery |
| ARG_STATUS | unsigned char | 0xFF letztes oder einziges element des Datenstreams 0x00 es folgen weitere Datenstreamstücke |
| ARG_WRITE_LEN | unsigned char | Länge des folgenden Schreibauftrags z.B. 0x02 für 2 Byte |
| ARG_WRITE_DATA | string | ASCII-codiert Schreibauftrag für Individualdatenstream (not used) |
| ARG_W_RESP_LEN | unsigned char | Optional, Laenge des folgenden Antwortfilters  (not used) z.B. 0x02 für 2 Byte |
| ARG_W_RESP_DATA | string | ASCII-codiert, Optional, Antwortfilter des Schreibauftrags (not used) |
| ARG_LEN | int | Länge des Individualisierungs Datenstream oder -streamstücks |
| ARG_DATA | string | ASCII-codiert Datenstream |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Rückmeldungen, Fehlercodes z.B. OK 0x00 oder NOTOK 0x01 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eisyugd"></a>
### _STATUS_EISYUGD

0x31E0 & 0x33E0 _STATUS_EISYUGD Ansteuern und Auslesen Eisy-Adaptionswerte (ungedrosselt) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSLESEMODE | string | Werte aus Tabelle _AUSLESEMODE  |
| STUETZSTELLE_NR | unsigned char | Nummer der auszulesenden Stützstellenkombination  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STUETZSTELLE_ANZAHL | unsigned char | Anzahl der auszulesenden Adaptionswerte  |
| STAT_NKW_0_WERT | long | Drehzahl NKW |
| STAT_NKW_EINH | string | rpm |
| STAT_VSE_SPRI_0_WERT | real | Istwert Einlassspreizung variable NWS VSE_SPRI |
| STAT_VSE_SPRI_EINH | string | degree CRK |
| STAT_VSA_SPRI_0_WERT | real | Istwert Auslassspreizung variable NWS VSA_SPRI |
| STAT_VSA_SPRI_EINH | string | degree CRK |
| STAT_HUBEV_IST_0_WERT | real | Istwert Einlassventilhub HUBEV_IST |
| STAT_HUBEV_IST_EINH | string | mm |
| STAT_PS_0_WERT | real | Ladedruck |
| STAT_PS_EINH | string | hpa |
| STAT_FS_EISYUGD_TEXT | string | Adaption Massenstromregler auf DK erstmalig erfolgt B_MAREGHUB_AD |
| STAT_FS_EISYUGD_WERT | int |  |
| STAT_MRNN_TEST_VVT_0_WERT | real | Massenstromregler-Adaptionswert NN im UGD - Betrieb ueber Test gelesen MRNN_TEST_VVT |
| STAT_MRNN_TEST_VVT_EINH | string | - |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eisygd"></a>
### _STATUS_EISYGD

0x31E1 & 0x33E1 _STATUS_EISYGD Ansteuern und Auslesen Eisy-Adaptionswerte (gedrosselt) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSLESEMODE | string | Werte aus Tabelle _AUSLESEMODE  |
| STUETZSTELLE_NR | unsigned char | Nummer der auszulesenden Stützstellenkombination  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STUETZSTELLE_ANZAHL | unsigned char | Anzahl der auszulesenden Adaptionswerte  |
| STAT_NKW_0_WERT | long | Drehzahl NKW |
| STAT_NKW_EINH | string | rpm |
| STAT_VSE_SPRI_0_WERT | real | Istwert Einlassspreizung variable NWS VSE_SPRI |
| STAT_VSE_SPRI_EINH | string | degree CRK |
| STAT_VSA_SPRI_0_WERT | real | Istwert Auslassspreizung variable NWS VSA_SPRI |
| STAT_VSA_SPRI_EINH | string | degree CRK |
| STAT_WDK_IST_0_WERT | real | Aktueller Drosselklappenwinkel WDK_IST |
| STAT_WDK_IST_EINH | string | percent |
| STAT_FS_EISYGD_TEXT | string | Adaption Massenstromregler auf DK erstmalig erfolgt B_MAREGDK_AD |
| STAT_FS_EISYGD_WERT | int |  |
| STAT_MRNN_TEST_DK_0_WERT | real | Massenstromregler-Adaptionswert NN im GD - Betrieb ueber Test gelesen MRNN_TEST_DK |
| STAT_MRNN_TEST_DK_EINH | string |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-krann"></a>
### _STATUS_KRANN

0x31E3 & 0x33E3 _STATUS_KRANN Ansteuern und Auslesen Krann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSLESEMODE | string | Werte aus Tabelle _AUSLESEMODE  |
| STUETZSTELLE_NR | unsigned char | Nummer der auszulesenden Stützstellenkombination  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STUETZSTELLE_ANZAHL | unsigned char | Anzahl der auszulesenden Adaptionswerte  |
| STAT_NKW_0_WERT | long | Drehzahl NKW |
| STAT_NKW_EINH | string | rpm |
| STAT_RF_0_WERT | real | Relative Luftfuellung RF |
| STAT_RF_EINH | string | percent |
| STAT_TANS_0_WERT | real | Ansauglufttemperatur TANS |
| STAT_TANS_EINH | string | degree |
| STAT_TMOT_WERT | real | Kuehlwassertemperatur TMOT |
| STAT_TMOT_EINH | string | degree |
| STAT_BA_IST_WERT | string | Istbetriebsart BA_IST |
| STAT_BA_IST_EINH | string | - |
| STAT_KRNN_TEST_0_WERT | real | Zuendwinkelaenderung aus Adaption Klopfregelung fuer Testerabfrage KRNN_TEST |
| STAT_KRNN_TEST_EINH | string | degree |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klann"></a>
### _STATUS_KLANN

0x31E4 & 0x33E4 _STATUS_KLANN Ansteuern und Auslesen Klann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSLESEMODE | string | Werte aus Tabelle _AUSLESEMODE  |
| STUETZSTELLE_NR | unsigned char | Nummer der auszulesenden Stützstellenkombination  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STUETZSTELLE_ANZAHL | unsigned char | Anzahl der auszulesenden Adaptionswerte  |
| STAT_NKW_LOC_0_WERT | long | Drehzahl NKW_LOC |
| STAT_NKW_LOC_EINH | string | rpm |
| STAT_RK_LOC_0_WERT | real | Relative Kraftstoffmasse RK_LOC |
| STAT_RK_LOC_EINH | string | percent |
| STAT_TMOT_LOC_0_WERT | real | Kuehlwassertemperatur TMOT_LOC |
| STAT_TMOT_LOC_EINH | string | degree |
| STAT_KLANN_TEST1_0_WERT | real | Faktor aus Adaption Lambdaregelung Bank 1 fuer Testerabfrage KLANN_TEST1 |
| STAT_KLANN_TEST1_EINH | string |  |
| STAT_KLANN_TEST2_0_WERT | real | Faktor aus Adaption Lambdaregelung Bank 2 fuer Testerabfrage KLANN_TEST2 |
| STAT_KLANN_TEST2_EINH | string |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-tev"></a>
### START_SYSTEMCHECK_TEV

Ansteuern Diagnosefunktion Tankentlueftungsventil SYSTEMCHECK_TEV (0x22)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-tev"></a>
### STATUS_SYSTEMCHECK_TEV

Auslesen Diagnosefunktion Tankentlueftungsventil SYSTEMCHECK_TEV (0x22)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFTE | unsigned char | FUNKTIONSSTATUS DFTE |
| STAT_FS_DFTE_TEXT | string | FUNKTIONSSTATUS DFTE |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-tev"></a>
### STOP_SYSTEMCHECK_TEV

Diagnosefunktion Tankentlueftungsventil beenden SYSTEMCHECK_TEV (0x22)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-evausbl"></a>
### START_SYSTEMCHECK_EVAUSBL

Ansteuern Diagnosefunktion Einspritzventilausblendung SYSTEMCHECK_EVAUSBL (0x25)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DEVOFF | unsigned char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-evausbl"></a>
### STATUS_SYSTEMCHECK_EVAUSBL

Auslesen Diagnosefunktion EinspritzVentile EV-Ausblendung SYSTEMCHECK_EVAUSBL (0x25)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFEV_WERT | unsigned char | FUNKTIONSSTATUS DFEV |
| STAT_EV1_AUSBL | unsigned char | Status ausgeblendetes Ventil 1 |
| STAT_EV2_AUSBL | unsigned char | Status ausgeblendetes Ventil 2 |
| STAT_EV3_AUSBL | unsigned char | Status ausgeblendetes Ventil 3 |
| STAT_EV4_AUSBL | unsigned char | Status ausgeblendetes Ventil 4 |
| STAT_EV5_AUSBL | unsigned char | Status ausgeblendetes Ventil 5 |
| STAT_EV6_AUSBL | unsigned char | Status ausgeblendetes Ventil 6 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-evausbl"></a>
### STOP_SYSTEMCHECK_EVAUSBL

Ende Diagnosefunktion EinspritzVentile EV-Ausblendung SYSTEMCHECK_EVAUSBL (0x25)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-vvt-anschlag"></a>
### START_SYSTEMCHECK_VVT_ANSCHLAG

Ansteuern Diagnosefunktion VVT-Anschlag lernen SYSTEMCHECK_VVT_ANSCHLAG (0x27)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-vvt-anschlag"></a>
### STATUS_SYSTEMCHECK_VVT_ANSCHLAG

Auslesen VVT Anschlag lernen SYSTEMCHECK_VVT_ANSCHLAG (0x27)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_VVTL | unsigned char | FUNKTIONSSTATUS VVTL |
| STAT_FS_VVTL_TEXT | string | FUNKTIONSSTATUS VVTL |
| STAT_VVTL_BIT0 | unsigned char | Auswertung Bit 0 Fehler unterer Anschlag nicht gefunden |
| STAT_VVTL_BIT0_TEXT | string | Auswertung Bit 0 Fehler unterer Anschlag nicht gefunden |
| STAT_VVTL_BIT1 | unsigned char | Auswertung Bit 1 Fehler oberer Anschlag nicht gefunden |
| STAT_VVTL_BIT1_TEXT | string | Auswertung Bit 1 Fehler oberer Anschlag nicht gefunden |
| STAT_VVTL_BIT2 | unsigned char | Auswertung Bit 2 Fehler Verstellbereich Fuehrungssensor unplausibel |
| STAT_VVTL_BIT2_TEXT | string | Auswertung Bit 2 Fehler Verstellbereich Fuehrungssensor unplausibel |
| STAT_VVTL_BIT3 | unsigned char | Auswertung Bit 3 Fehler Verstellbereich Referenzsensor unplausibel |
| STAT_VVTL_BIT3_TEXT | string | Auswertung Bit 3 Fehler Verstellbereich Referenzsensor unplausibel |
| STAT_VVTL_BIT4 | unsigned char | Auswertung Bit 4 Fehler zulaessige Hoechstzeit Anschlaglernvorgang ueberschritten |
| STAT_VVTL_BIT4_TEXT | string | Auswertung Bit 4 Fehler zulaessige Hoechstzeit Anschlaglernvorgang ueberschritten |
| STAT_VVTL_BIT5 | unsigned char | Auswertung Bit 5 Fehler Spannungsversorgung |
| STAT_VVTL_BIT5_TEXT | string | Auswertung Bit 5 Fehler Spannungsversorgung |
| STAT_VVTL_BIT6 | unsigned char | Auswertung Bit 6 Fehler VVT-Sensor, Leistungsversorgung oder Stellglied |
| STAT_VVTL_BIT6_TEXT | string | Auswertung Bit 6 Fehler VVT-Sensor, Leistungsversorgung oder Stellglied |
| STAT_VVTL_BIT7 | unsigned char | Auswertung Bit 7 Ruecknahme Lernanforderung |
| STAT_VVTL_BIT7_TEXT | string | Auswertung Bit 7 Ruecknahme Lernanforderung |
| STAT_F_VVTL_WERT | unsigned int | Fuehrungssensorrohwert |
| STAT_F_VVTL_EINH | string | "°" |
| STAT_R_VVTL_WERT | real | Referenzsensorrohwert |
| STAT_R_VVTL_EINH | string | "Grad" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-vvt-anschlag"></a>
### STOP_SYSTEMCHECK_VVT_ANSCHLAG

Diagnosefunktion VVT Anschlag lernen beenden SYSTEMCHECK_VVT_ANSCHLAG (0x27)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-gen"></a>
### START_SYSTEMCHECK_GEN

Diagnosefunktion Generatortest SYSTEMCHECK_GEN (0x2A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-gen"></a>
### STATUS_SYSTEMCHECK_GEN

Auslesen Diagnosefunktion Generatortest SYSTEMCHECK_GEN (0x2A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1 | unsigned char | Stati fuer Diagnosefunktion Generatortest |
| STAT_DIAGNOSE_1_TEXT | string | Stati fuer Diagnosefunktion Generatortest |
| STAT_GENIUTEST_ERR_WERT | unsigned char | GENIUTEST Fehler |
| STAT_GENIUTEST_AB_WERT | unsigned char | GENIUTEST_AB Abbruchbedingungen |
| STAT_GENITEST_TOL_WERT | real | Toleranzbereich fuer Abweichung vom Sollwert Strom (GENITEST_TOL) |
| STAT_GENITEST_TOL_EINH | string | "%" |
| STAT_GENUTEST_TOL_WERT | real | Toleranzbereich fuer Abweichung vom Sollwert Spannung (GENUTEST_TOL) |
| STAT_GENUTEST_TOL_EINH | string | "%" |
| STAT_I_GENTEST_WERT | unsigned char | Modellierter Generatorstrom |
| STAT_I_GENTEST_EINH | string | "A" |
| STAT_U_GENTEST_WERT | real | Generatorsollspannung |
| STAT_U_GENTEST_EINH | string | "V" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-gen"></a>
### STOP_SYSTEMCHECK_GEN

Diagnosefunktion Generatortest beenden SYSTEMCHECK_GEN (0x2A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-odr"></a>
### START_SYSTEMCHECK_ODR

Diagnosefunktion Oeldruckregelung SYSTEMCHECK_ODR (0x2C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-odr"></a>
### STATUS_SYSTEMCHECK_ODR

Auslesen Diagnosefunktion Oeldruckregelung SYSTEMCHECK_ODR (0x2C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1 | unsigned char | Stati fuer Diagnosefunktion Oeldruckregelung |
| STAT_DIAGNOSE_1_TEXT | string | Stati fuer Diagnosefunktion Oeldruckregelung |
| STAT_DIAGNOSE_2 | unsigned char | Erweiterte Stati fuer Diagnosefunktion Oeldruckregelung |
| STAT_DIAGNOSE_2_TEXT | string | Erweiterte Stati fuer Diagnosefunktion Oeldruckregelung |
| STAT_TOEL_WERT | real | Ausgabewert Motoroeltemperatur fuer LoCAN |
| STAT_TOEL_EINH | string | "Grad C" |
| STAT_P_OEL_SOLL_WERT | real | Sollwert Oeldruck |
| STAT_P_OEL_SOLL_EINH | string | "kPa" |
| STAT_P_OEL_IST_WERT | int | Istwert Oeldruck |
| STAT_P_OEL_IST_EINH | string | "hPa" |
| STAT_NKW_SOLL_WERT | int | Sollwertanforderung Drehzahl aus Funktion Oeldruckregelung |
| STAT_NKW_SOLL_EINH | string | "1/min" |
| STAT_NKW_WERT | real | Istwert Drehzahl Kurbelwelle |
| STAT_NKW_EINH | string | "rpm" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-odr"></a>
### STOP_SYSTEMCHECK_ODR

Diagnosefunktion Oeldruckregelung beenden SYSTEMCHECK_ODR (0x2C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adap2-selektiv-loeschen"></a>
### ADAP2_SELEKTIV_LOESCHEN

Ansteuern Adaptionen 2 selektiv loeschen ADAP2_SELEKTIV_LOESCHEN (0x31)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADAV2_AUSWAHLBYTE_1 | unsigned char | ADAV2_AUSWAHLBYTE_1_BIT_7 -- &gt; Kleinstmengenadaption ADAV2_AUSWAHLBYTE_1_BIT_6 --&gt; NOT USED ADAV2_AUSWAHLBYTE_1_BIT_5 --&gt; NOT USED ADAV2_AUSWAHLBYTE_1_BIT_4 --&gt; NOT USED ADAV2_AUSWAHLBYTE_1_BIT_3 --&gt; Adaption elektrische Kraftstoffpumpe ADAV2_AUSWAHLBYTE_1_BIT_2 --&gt; Adaption Langzeit fuer Injektoralterung Bank 2(NOT USED) ADAV2_AUSWAHLBYTE_1_BIT_1 --&gt; Adaption Langzeit fuer Injektoralterung Bank 1(NOT USED) ADAV2_AUSWAHLBYTE_1_BIT_0 --&gt; Adaption Nullgangsensor (Achtung: Mit diesem Bit darf die Adaption des Nullgangsensors nicht mehr geloescht werden! Bei Austausch des Nullgangsensors soll die Adaption mit dem dafuer vorgesehenen Dienst durch |
| ADAV2_AUSWAHLBYTE_2 | unsigned char | ADAV2_AUSWAHLBYTE_2_BIT_7 --&gt; NOT USED ADAV2_AUSWAHLBYTE_2_BIT_6 --&gt; Verlustmomentadaption Reset ADAV2_AUSWAHLBYTE_2_BIT_5 --&gt; Adaption NOx-Katalysator (NOT USED) ADAV2_AUSWAHLBYTE_2_BIT_4 --&gt; Bereichserkennung Benzin im Oel (B_clradbo) ADAV2_AUSWAHLBYTE_2_BIT_3 --&gt; NOT USED ADAV2_AUSWAHLBYTE_2_BIT_2 --&gt; NOT USED ADAV2_AUSWAHLBYTE_2_BIT_1 --&gt; NOT USED ADAV2_AUSWAHLBYTE_2_BIT_0 --&gt; NOT USED |
| ADAV2_AUSWAHLBYTE_3 | unsigned char | ADAV2_AUSWAHLBYTE_3_BIT_7 --&gt; Zuruecksetzen der Hubkorrekturstatistik per Tester (Bit-Name = B_vbr_stat_reset_ext und Basisvariable = St_vbr_stat) ADAV2_AUSWAHLBYTE_3_BIT_6 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_5 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_4 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_3 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_2 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_1 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_0 --&gt; NOT USED |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-zsz"></a>
### START_ZSZ

Ansteuern des Systemtestes Zuendkerze freibrennen (Kalttestspezifisch) (Anforderung aus CP21228) ZSZ (0x36)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZUENDFREQUENZ | unsigned char | Zuendfrequenz zum Freibrennen der Zuendkerzen |
| FREIBRENNDAUER | real | Freibrenndauer |
| LADEDAUER | real | Ladedauer fuer alle Kalttest-Zuendungstests (Freibrennen, zeitgesteuerte Ablauf-sequenz, winkelsynchroner Test) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zsz"></a>
### STATUS_ZSZ

Auslesen des Systemtestes Zuendkerze freibrennen (Kalttestspezifisch) (Anforderung aus CP21228) ZSZ (0x36)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_ZSZ | unsigned char | FUNKTIONSSTATUS ZSZ |
| STAT_FS_ZSZ_TEXT | string | FUNKTIONSSTATUS ZSZ |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-zsz"></a>
### STOP_ZSZ

Ende des Systemtestes Zuendkerze freibrennen (Kalttestspezifisch) (Anforderung aus CP21228) ZSZ (0x36)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-zszw"></a>
### START_ZSZW

Ansteuern des Systemtests betriebspunktunabhaengiger (Winkelsynchroner) Zuendspulentest (Kalttestspezifisch) ZSZW (0x37)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LADEDAUER | real | Ladedauer fuer alle Kalttest-Zuendungstests (Freibrennen, zeitgesteuerte Ablauf-sequenz, winkelsynchroner Test) |
| ZUENDWINKEL | real | Zuendwinkel fuer winkelsynchronen Zuendungstest |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zszw"></a>
### STATUS_ZSZW

Auslesen des Systemtests betriebspunktunabhaengiger (Winkelsynchroner) Zuenspulentest (Kalttestspezifisch) ZSZW (0x37)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_ZSZW | unsigned char | FUNKTIONSSTATUS ZSZW |
| STAT_FS_ZSZW_TEXT | string | FUNKTIONSSTATUS ZSZW |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-zszw"></a>
### STOP_ZSZW

Ende des Systemtests betriebspunktunabhaengiger (Winkelsynchroner) Zuenspulentest (Kalttestspezifisch) ZSZW (0x37)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-evz"></a>
### START_EVZ

Ansteuern des Systemtestes Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) (Anforderung aus CP21228) EVZ (0x38)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANSTEUERDAUER | real | Ansteuerdauer pro Einspritzimpuls vom Testermodul |
| PERIONDENDAUER | real | Periodendauer fuer Einspritzimpuls vom Testermodul |
| PAUSENDAUER | real | Pausendauer zwischen der Ansteuerung der Injektoren bei Ansteuersequenz vom Testermodul |
| ANZAHL_DER_TESTIMPULSE | unsigned char | Anzahl der Testimpulse pro Injektor vom Testermodul |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-evz"></a>
### STATUS_EVZ

Auslesen des Systemtestes Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) (Anforderung aus CP21228) EVZ (0x38)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EVZ | unsigned char | FUNKTIONSSTATUS EVZ |
| STAT_FS_EVZ_TEXT | string | FUNKTIONSSTATUS EVZ |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-evz"></a>
### STOP_EVZ

Ende des Systemtestes Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) (Anforderung aus CP21228) EVZ (0x38)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-zszz"></a>
### START_ZSZZ

Zeitbasierte Zuendsequenz (Kalttestspezifisch) ZSZZ (0x39)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PAUSENDAUER | real | Pausendauer zwischen der Ansteuerung der Zuendkerzen bei Ansteuersequenz vom Testermodul |
| LADEDAUER | real | Ladedauer fuer alle Kalttest-Zuendungstests (Freibrennen, zeitgesteuerte Ablauf- sequenz, winkelsynchroner Test |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zszz"></a>
### STATUS_ZSZZ

Zeitbasierte Zuendsequenz (Kalttestspezifisch) ZSZZ (0x39)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_ZSZZ | unsigned char | FUNKTIONSSTATUS ZSZZ |
| STAT_FS_ZSZZ_TEXT | string | FUNKTIONSSTATUS ZSZZ |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-zszz"></a>
### STOP_ZSZZ

Zeitbasierte Zuendsequenz (Kalttestspezifisch) ZSZZ (0x39)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-zwdiag"></a>
### START_ZWDIAG

CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Start-Routine ZWDIAG (0x3A)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAC_CH_DIAG_EXT_ADJ_IS | real | Manipulation factor of CH torque reserve for ignition angle efficiency monitoring - demo-mode IS |
| FAC_CH_DIAG_EXT_ADJ_PL | real | Manipulation factor of CH torque reserve for ignition angle efficiency monitoring - demo-mode PL |
| LV_CH_DIAG_EXT_REQ | unsigned char | External request for ignition angle efficiency monitoring - demo- mode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zwdiag"></a>
### STATUS_ZWDIAG

CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Status-Routine ZWDIAG (0x3A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_ZWDIAG | unsigned char | FUNKTIONSSTATUS ZWDIAG |
| STAT_FS_ZWDIAG_TEXT | string | FUNKTIONSSTATUS ZWDIAG |
| STAT_LV_DIAG_CST_ACT | unsigned char | Condition for cold start diagnosis active |
| STAT_LV_DIAG_CST_ACT_TEXT | string | Condition for cold start diagnosis active |
| STAT_LV_INH_DIAG_EFF_IGA_CST | unsigned char | Flag for inhibitation of the Ignition angle efficiency Diagnosis |
| STAT_LV_INH_DIAG_EFF_IGA_CST_TEXT | string | Flag for inhibitation of the Ignition angle efficiency Diagnosis |
| STAT_STATE_CH | unsigned char | state of catalyst heating (A2L-Name: state_ch) |
| STAT_STATE_CH_TEXT | string | state of catalyst heating (A2L-Name: state_ch) |
| STAT_T_AST_WERT | real | Time after start (A2L-Name: t_ast) |
| STAT_T_AST_EINH | string | "s" |
| STAT_TCO_ST_WERT | real | coolant temperature at start (A2L-Name: tco_st) |
| STAT_TCO_ST_EINH | string | "Grad C" |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_IS | unsigned char | Diagnosis conditions fulfilled Ignition angle efficiency at coldstart - idle speed |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_IS_TEXT | string | Diagnosis conditions fulfilled Ignition angle efficiency at coldstart - idle speed |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_PL | unsigned char | Diagnosis conditions fulfilled Ignition angle efficiency at coldstart - part load |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_PL_TEXT | string | Diagnosis conditions fulfilled Ignition angle efficiency at coldstart - part load |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-zwdiag"></a>
### STOP_ZWDIAG

CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Stop-Routine ZWDIAG (0x3A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-vanosspuelen"></a>
### START_VANOSSPUELEN

VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0x42)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VANOSSPL_M_MODUS | unsigned char | 1=gleichzeitiges Verstellen von Ein- und Auslass-Vanos. und 2=erst Verstellen Einlass, dann Verstellen Auslass. Default-Wert = 1. (A2L-Name: modenwstcl) Min: 1.0 Max: 2.0 |
| VANOSSPL_N_AZLVERSTL | unsigned char | Anzahl Verstellungen. Default-Wert = 10 Dez. (A2L-Name: anztvtcl) Min: 1.0 Max: 50.0 |
| VANOSSPL_T_HLTZVERSTL | real | Haltezeit Verstellung (0 bis 5 s). Default-Wert = 2.0 s. Gesamtzeit Vanosspuelen = N * 2 * T * m. (A2L-Name: takttcl) Min: 0.0 Max: 5.0 |
| VANOSSPL_N1_UDZLGRNZ | unsigned long | Untere Drehzahlgrenze (500 bis 2000 U/min) ca 100 U/min unter LL-Solldrehzahl . Default-Wert = 1000. (A2L-Name: nmotmintcl) Min: 500.0 Max: 2000.0 |
| VANOSSPL_N2_ODZLGRNZ | unsigned long | Obere Drehzahlgrenze (500 bis 2000 U/min) ca 100 U/min ueber LL-Solldrehzahl . Default-Wert = 1200. (A2L-Name: nmotmaxtcl) Min: 500.0 Max: 2000.0 |
| VANOSSPL_V_MAX | unsigned char | Max. Fahrzeuggeschwindigkeit (0 bis 100 km/h). Default-Wert = 0 (A2L-Name: vfzgmxtcl) Min: 0.0 Max: 100.0 |
| VANOSSPL_T2_ZUBRZ | real | Zulaessige Unterbrechungszeit (0 bis 20 s). Default-Wert = 5s. (A2L-Name: taktumxtcl) Min: 0.0 Max: 20.0 |
| VANOSSPL_DVSE1_VO1EV | real | Verstelloffset 1 Einlass-Vanos (von -102,4 bis 101,6°KW). Default-Wert=5.6°Grad. (A2L-Name: ofstclnwe1) Min: -102.4 Max: 101.60000000000001 |
| VANOSSPL_DVSE2_VO2EV | real | Verstelloffset 2 Einlass-Vanos (von -102,4 bis 101,6°KW). Default-Wert=-5.6°Grad. (A2L-Name: ofstclnwe2) Min: -102.4 Max: 101.60000000000001 |
| VANOSSPL_DVSA1_VO1AV | real | Verstelloffset 1 Auslas-Vanos (von -102,4 bis 101,6°KW). Default-Wert=-5.6°Grad. (A2L-Name: ofstclnwa1) Min: -102.4 Max: 101.60000000000001 |
| VANOSSPL_DVSA2_VO1AV | real | Verstelloffset 2 Auslas-Vanos (von -102,4 bis 101,6°KW). Default-Wert=5.6°Grad. (A2L-Name: ofstclnwa2) Min: -102.4 Max: 101.60000000000001 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vanosspuelen"></a>
### STATUS_VANOSSPUELEN

VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0x42)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_VANOSSPUELEN_WERT | unsigned char | FUNKTIONSSTATUS VANOSSPUELEN (statnwtscl) |
| STAT_FS_VANOSSPUELEN_WERT_TEXT | string | FUNKTIONSSTATUS VANOSSPUELEN (statnwtscl) |
| STAT_NMOT_W_WERT | real | Motordrehzahl soll zws. der unteren Drehzahlgrenze (ca. 100 rpm unter LL-Solldrehzahl. Default= 1000 rpm) und der oberen Drehzahlgrenze (ca. 100 rpm ueber LL-Solldrehzahl. Default = 1200 rpm) sein. (A2L-Name: nmot_w) Einheit: 1/min Min: 0.0 Max: 10000.0 |
| STAT_NMOT_W_EINH | string | "1/min" |
| STAT_V_WERT | real | Fahrzeuggeschwindigkeit soll zws. 0 und 100 Km/h liegen. Default = 0 (A2L-Name: vfzg_w) Einheit: km/h Min: 0.0 Max: 511.9921875 |
| STAT_V_EINH | string | "km/h" |
| STAT_ST_LL | unsigned char | Status Leerlauf (A2L-Name: B_ll) Min: 0.0 Max: 255.0 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-vanosspuelen"></a>
### STOP_VANOSSPUELEN

VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0x42)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-atl"></a>
### START_SYSTEMCHECK_ATL

Diagnosefunktion Abgasturbolader starten SYSTEMCHECK_ATL (0xD0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-atl"></a>
### STATUS_SYSTEMCHECK_ATL

Diagnosefunktion Abgasturbolader auslesen SYSTEMCHECK_ATL (0xD0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1 | unsigned char | Status waehrend der ATL-Diagnose (A2L-Name: Statlsvc) |
| STAT_DIAGNOSE_1_TEXT | string | Status waehrend der ATL-Diagnose (A2L-Name: Statlsvc) |
| STAT_DIAGNOSE_2 | unsigned char | Ergebnis der ATL-Diagnosefunktion (A2L-Name: statlsvcpvdk) |
| STAT_DIAGNOSE_2_TEXT | string | Ergebnis der ATL-Diagnosefunktion (A2L-Name: statlsvcpvdk) |
| STAT_AMP_WERT | real | Ambient pressure (measured or adapted) (A2L-Name: pur_w) |
| STAT_AMP_EINH | string | "hPa" |
| STAT_TAM_WERT | real | Ambient temperature (A2L-Name: tumg) |
| STAT_TAM_EINH | string | "Grad C" |
| STAT_TIA_WERT | real | Intake air temperature (A2L-Name: tans) |
| STAT_TIA_EINH | string | "Grad C" |
| STAT_ATLSVC_DPVDK1_WERT | real | Differenzdruck vor DK beider Turbolader (A2L-Name: Atlsvcdpvdk1_w) |
| STAT_ATLSVC_DPVDK1_EINH | string | "hPa" |
| STAT_ATLSVC_DPVDK2_WERT | real | Differenzdruck vor DK mit Turbolader 1 (A2L-Name: Atlsvcdpvdk2_w) |
| STAT_ATLSVC_DPVDK2_EINH | string | "hPa" |
| STAT_ATLSVC_DPVDK3_WERT | real | Differenzdruck vor DK mit Turbolader 2 (A2L-Name: Atlsvcdpvdk3_w) |
| STAT_ATLSVC_DPVDK3_EINH | string | "hPa" |
| STAT_PWG_IST_WERT | real | Pedalwert Fahrerwunsch in % (A2L-Name: wped_w) |
| STAT_PWG_IST_EINH | string | "%PED" |
| STAT_TN_ABSTELL_WERT | unsigned int | Abstellzeit (A2L-Name: Tabst_w) |
| STAT_TN_ABSTELL_EINH | string | "s" |
| STAT_B_KUPP | unsigned char | Bedingung Kupplungsbetätigung über Schalter oder Modell (A2L-Name: B_kuppl) |
| STAT_B_KUPP_TEXT | string | Bedingung Kupplungsbetätigung über Schalter oder Modell (A2L-Name: B_kuppl) |
| STAT_GANGI_WERT | unsigned char | Aktueller Gang intern (A2L-Name: Gangi) |
| STAT_V_WERT | real | Fahrzeuggeschwindigkeit (A2L-Name: Vfzg_w) |
| STAT_V_EINH | string | "km/h" |
| STAT_TMOT_WERT | real | Kuehlwassertemperatur (A2L-Name: Tmot) |
| STAT_TMOT_EINH | string | "Grad C" |
| STAT_PU_WERT | real | Umgebungsdruck (A2L-Name: Pu_w) |
| STAT_PU_EINH | string | "hPa" |
| STAT_LV_ERR_PUT_EL_WERT | unsigned char | electrical PUT sensor error detected (A2L-Name: DFC_PVDEmax \|\| DFC_PVDEmin) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-atl"></a>
### STOP_SYSTEMCHECK_ATL

Diagnosefunktion Abgasturbolader beenden SYSTEMCHECK_ATL (0xD0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-glf"></a>
### START_SYSTEMCHECK_GLF

Ansteuern Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xD5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-glf"></a>
### STATUS_SYSTEMCHECK_GLF

Auslesen Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xD5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_GLF_WERT | unsigned char | FUNKTIONSSTATUS GLFS |
| STAT_SYSTEMCHECK_GLF_WERT_TEXT | string | FUNKTIONSSTATUS GLFS |
| STAT_GLF_15_WERT | unsigned char | Fehlerstatus gesteuerte Luftfuehrung |
| STAT_GLF_15_WERT_TEXT | string | Fehlerstatus gesteuerte Luftfuehrung |
| STAT_GLF_14_WERT | unsigned char | Kommunikationsstatus gesteuerte Luftfuehrung |
| STAT_GLF_14_WERT_TEXT | string | Kommunikationsstatus gesteuerte Luftfuehrung |
| STAT_GLF_13_WERT | unsigned char | Status Testeransteuerung obere Luftklappe |
| STAT_GLF_13_WERT_TEXT | string | Status Testeransteuerung obere Luftklappe |
| STAT_GLF_12_WERT | unsigned char | Status Testeransteuerung untere Luftklappe |
| STAT_GLF_12_WERT_TEXT | string | Status Testeransteuerung untere Luftklappe |
| STAT_GLF_11_WERT | unsigned char | Status Eigendiagnose untere Luftklappe |
| STAT_GLF_11_WERT_TEXT | string | Status Eigendiagnose untere Luftklappe |
| STAT_GLF_10_WERT | unsigned char | Status Eigendiagnose obere Luftklappe |
| STAT_GLF_10_WERT_TEXT | string | Status Eigendiagnose obere Luftklappe |
| STAT_GLF_9_WERT | unsigned char | Status elektrische Diagnose gesteuerte Luftfuehrung |
| STAT_GLF_9_WERT_TEXT | string | Status elektrische Diagnose gesteuerte Luftfuehrung |
| STAT_GLF_8_WERT | unsigned char | Status Systemtest durchgefuehrt |
| STAT_GLF_8_WERT_TEXT | string | Status Systemtest durchgefuehrt |
| STAT_GLF_7_WERT | unsigned char | Status Systemtest aktiv |
| STAT_GLF_7_WERT_TEXT | string | Status Systemtest aktiv |
| STAT_GLF_6_WERT | unsigned char | Fehlerstatus aus Eigendiagnose untere Luftklappe |
| STAT_GLF_6_WERT_TEXT | string | Fehlerstatus aus Eigendiagnose untere Luftklappe |
| STAT_GLF_5_WERT | unsigned char | Fehlerstatus aus Eigendiagnose obere Luftklappe |
| STAT_GLF_5_WERT_TEXT | string | Fehlerstatus aus Eigendiagnose obere Luftklappe |
| STAT_GLF_4_WERT | unsigned char | Status elektrischer Fehler |
| STAT_GLF_4_WERT_TEXT | string | Status elektrischer Fehler |
| STAT_GLF_3_WERT | unsigned char | Status Fehlerabfrage |
| STAT_GLF_3_WERT_TEXT | string | Status Fehlerabfrage |
| STAT_GLF_2_WERT | unsigned char | Status gelernte Variante untere Luftklappe |
| STAT_GLF_2_WERT_TEXT | string | Status gelernte Variante untere Luftklappe |
| STAT_GLF_1_WERT | unsigned char | Status gelernte Variante obere Luftklappe |
| STAT_GLF_1_WERT_TEXT | string | Status gelernte Variante obere Luftklappe |
| STAT_GLF_0_WERT | unsigned char | Status Variantenerkennung |
| STAT_GLF_0_WERT_TEXT | string | Status Variantenerkennung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-glf"></a>
### STOP_SYSTEMCHECK_GLF

Ende Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xD5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-l-regelung-aus"></a>
### START_SYSTEMCHECK_L_REGELUNG_AUS

Ansteuerung Lambdaregelung deaktivieren SYSTEMCHECK_L_REGELUNG_AUS (0xD9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-l-regelung-aus"></a>
### STATUS_SYSTEMCHECK_L_REGELUNG_AUS

Auslesen Lambdaregelung ausschalten SYSTEMCHECK_L_REGELUNG_AUS (0xD9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFL0 | unsigned char | FUNKTIONSSTATUS DFL0 |
| STAT_FS_DFL0_TEXT | string | FUNKTIONSSTATUS DFL0 |
| STAT_LR_AUS_BIT0 | unsigned char | Auswertung Bit 0 Open Loop - Start-/Ansteuerbedingung für Regelung nicht erfüllt |
| STAT_LR_AUS_BIT0_TEXT | string | Auswertung Bit 0 Open Loop - Start-/Ansteuerbedingung für Regelung nicht erfüllt |
| STAT_LR_AUS_BIT1 | unsigned char | Auswertung Bit 1 Closed Loop - Lambdaregelung-Diagnose |
| STAT_LR_AUS_BIT1_TEXT | string | Auswertung Bit 1 Closed Loop - Lambdaregelung-Diagnose |
| STAT_LR_AUS_BIT2 | unsigned char | Auswertung Bit 2 Open Loop - Keine Regelung durch Fahrzustand. Gemisch zu fett/mager |
| STAT_LR_AUS_BIT2_TEXT | string | Auswertung Bit 2 Open Loop - Keine Regelung durch Fahrzustand. Gemisch zu fett/mager |
| STAT_LR_AUS_BIT3 | unsigned char | Auswertung Bit 3 Open Loop - Fehler erkannt |
| STAT_LR_AUS_BIT3_TEXT | string | Auswertung Bit 3 Open Loop - Fehler erkannt |
| STAT_LR_AUS_BIT4 | unsigned char | Auswertung Bit 4 Closed Loop - Min. eine Lambdasonde fehlerhaft. U.u. in Einzelbetrieb |
| STAT_LR_AUS_BIT4_TEXT | string | Auswertung Bit 4 Closed Loop - Min. eine Lambdasonde fehlerhaft. U.u. in Einzelbetrieb |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-l-regelung-aus"></a>
### STOP_SYSTEMCHECK_L_REGELUNG_AUS

Ende Lambdaregelung ausschalten SYSTEMCHECK_L_REGELUNG_AUS (0xD9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-dmtl"></a>
### START_SYSTEMCHECK_DMTL

Ansteuern Diagnosefunktion DMTL SYSTEMCHECK_DMTL (0xDA)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-dmtl"></a>
### STATUS_SYSTEMCHECK_DMTL

Auslesen Diagnosefunktion DMTL SYSTEMCHECK_DMTL (0xDA)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1 | unsigned char | Aktionsstatus DMTL. |
| STAT_DIAGNOSE_1_TEXT | string | Aktionsstatus DMTL. |
| STAT_DIAGNOSE_2 | unsigned char | Funktionsstatus DMTL. |
| STAT_DIAGNOSE_2_TEXT | string | Funktionsstatus DMTL. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-dmtl"></a>
### STOP_SYSTEMCHECK_DMTL

Diagnosefunktion DMTL beenden SYSTEMCHECK_DMTL (0xDA)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-eisyugd"></a>
### START_EISYUGD

Ansteuern Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403) EISYUGD (0xE0)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW | int | Drehzahl |
| VSE_SPRI | real | Istwert Einlassspreizung variable NWS |
| VSA_SPRI | real | Istwert Auslassspreizung variable NWS |
| HUBEV_IST | real | Istwert Einlassventilhub |
| PS | real | Absolut Druck im Saugrohr (A2L-Name: Ps) (Istwert Umgebungsdruck) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eisyugd"></a>
### STATUS_EISYUGD

Auslesen Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403) EISYUGD (0xE0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EISYUGD | unsigned char | FUNKTIONSSTATUS EISYUGD |
| STAT_FS_EISYUGD_TEXT | string | FUNKTIONSSTATUS EISYUGD |
| STAT_MRNN_TEST_VVT_WERT | real | Massenstromregler-Adaptionswert im VVT Betrieb ueber Test gelesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-eisygd"></a>
### START_EISYGD

Ansteuern Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403) EISYGD (0xE1)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW | int | Drehzahl |
| VSE_SPRI | real | Istwert Einlassspreizung variable NWS |
| VSA_SPRI | real | Istwert Auslassspreizung variable NWS |
| WDK_IST | real | Aktueller Drosselklappenwinkel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eisygd"></a>
### STATUS_EISYGD

Auslesen Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403) EISYGD (0xE1)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EISYGD | unsigned char | FUNKTIONSSTATUS EISYGD |
| STAT_FS_EISYGD_TEXT | string | FUNKTIONSSTATUS EISYGD |
| STAT_MRNN_TEST_DK_WERT | real | Massenstromregler-Adaptionswert im GD - Betrieb ueber Test gelesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-krann"></a>
### START_KRANN

Ansteuern Krann-Adaptionswerte (Anforderung aus CP5404) KRANN (0xE3)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_LOC | int | Drehzahl |
| RK_LOC | real | Relative Kraftstoffmasse |
| TANS_LOC | real | Ansauglufttemperatur |
| TMOT_LOC | real | Kuehlwassertemperatur |
| BA_IST_LOC | string | Istbetriebsart Werttabelle 0/ = Keine 1/ = Schicht 2/ = Homogen 3/ = Homogen_Schicht 8/ = Notlauf |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-krann"></a>
### STATUS_KRANN

Auslesen Krann-Adaptionswerte (Anforderung aus CP5404) KRANN (0xE3)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KRNN_TEST_WERT | real | Zuendwinkelaenderung aus Adaption Klopfregelung fuer Testerabfrage |
| STAT_KRNN_TEST_EINH | string | "Grad" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-klann"></a>
### START_KLANN

Ansteuern Klann-Adaptionswerte (Anforderung aus CP10798) KLANN (0xE4)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_LOC | int | Drehzahl |
| RK_LOC | real | Relative Kraftstoffmasse |
| TMOT_LOC | real | Kuehlwassertemperatur |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klann"></a>
### STATUS_KLANN

Auslesen Klann-Adaptionswerte (Anforderung aus CP10798) KLANN (0xE4)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLNN_TEST_WERT | real | Lambdaadaptionswert für Tester Bank1 |
| STAT_KLNN_TEST_EINH | string | "%" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-ddlshk"></a>
### START_SYSTEMCHECK_DDLSHK

Ansteuern Dynamik Diagnose Lamdasonden hinter Hauptkat SYSTEMCHECK_DDLSHK (0xE7)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-ddlshk"></a>
### STATUS_SYSTEMCHECK_DDLSHK

Auslesen Dynamik Diagnose Lamdasonden hinter Hauptkat SYSTEMCHECK_DDLSHK (0xE7)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DDLSHK | unsigned char | Dynamik Diagnose LS hinter Hauptkat freigegeben |
| STAT_FS_DDLSHK_TEXT | string | Dynamik Diagnose LS hinter Hauptkat freigegeben |
| STAT_TAHSO_WERT | real | Abgastemperatur an Sonde hinter Kat |
| STAT_TAHSO_EINH | string | "Grad C" |
| STAT_TRLRS2_WERT | real | Ereignisfilterwert für Transient Zeit Sonde hinter KAT LR |
| STAT_TRLRS2_EINH | string | "s" |
| STAT_TRRLS2_WERT | real | Ereignisfilterwert für Transient Zeit Sonde hinter KAT Bank 2 |
| STAT_TRRLS2_EINH | string | "s" |
| STAT_DTLRFS2_WERT | real | Ereignisfilterwert für Response Zeit Sonde hinter KAT LR |
| STAT_DTLRFS2_EINH | string | "s" |
| STAT_DTRLFS2_WERT | real | Ereignisfilterwert für Response Zeit Sonde hinter KAT RL |
| STAT_DTRLFS2_EINH | string | "s" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-ddlshk"></a>
### STOP_SYSTEMCHECK_DDLSHK

Ende Dynamik Diagnose Lamdasonden hinter Hauptkat SYSTEMCHECK_DDLSHK (0xE7)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-cram"></a>
### START_CRAM

Ansteuern RAM-Backup-Werte loeschen CRAM (0xE9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cram"></a>
### STATUS_CRAM

Auslesen RAM-Backup-Werte loeschen CRAM (0xE9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_CRAM | unsigned char | FUNKTIONSSTATUS CRAM |
| STAT_FS_CRAM_TEXT | string | FUNKTIONSSTATUS CRAM |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-dkat"></a>
### START_SYSTEMCHECK_DKAT

Ansteuern Kurztest Kat SYSTEMCHECK_DKAT (0xEB)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-dkat"></a>
### STATUS_SYSTEMCHECK_DKAT

Auslesen Kurztest Kat SYSTEMCHECK_DKAT (0xEB)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DKAT | unsigned char | FUNKTIONSSTATUS DKAT |
| STAT_FS_DKAT_TEXT | string | FUNKTIONSSTATUS DKAT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-dkat"></a>
### STOP_SYSTEMCHECK_DKAT

Ende Kurztest Kat SYSTEMCHECK_DKAT (0xEB)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-pm-messemode"></a>
### STATUS_SYSTEMCHECK_PM_MESSEMODE

Auslesen Messemode SYSTEMCHECK_PM_MESSEMODE (0xF6)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_PM_MESSEMODE | unsigned char | Funktionsstatus Powermanagement Messemode |
| STAT_SYSTEMCHECK_PM_MESSEMODE_TEXT | string | Funktionsstatus Powermanagement Messemode |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dk"></a>
### STEUERN_ENDE_DK

Drosselklappe Ansteuerung beenden DK (0x2A00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dk"></a>
### STEUERN_DK

Drosselklappe ansteuern DK (0x2A07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DK | real | Tastverhaeltniss Drosselklappe |
| SW_TO_DK | unsigned long | Timeout Drosselklappe |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ugen"></a>
### STEUERN_ENDE_UGEN

Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden UGEN (0x3200)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ugen"></a>
### STEUERN_UGEN

Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) ansteuern UGEN (0x3207)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PHY_UGEN | real | Spannung Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) |
| SW_TO_UGEN | unsigned long | Timeout Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte"></a>
### STATUS_MESSWERTE

Messwerte auslesen MESSWERTE (0x4000)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LR1_MW_WERT | real | Lambdaregler 1 |
| STAT_VFZG_MW_WERT | real | Fahrzeuggeschwindigkeit |
| STAT_VFZG_MW_EINH | string | "km/h" |
| STAT_NMOT_W_MW_WERT | real | Motordrehzahl hoch aufgeloest |
| STAT_NMOT_W_MW_EINH | string | "1/min" |
| STAT_NSOL_MW_WERT | real | Leerlauf-Solldrehzahl |
| STAT_NSOL_MW_EINH | string | "1/min" |
| STAT_CAM_IN_WERT | real | Istwert Einlassnockenwellensteller |
| STAT_CAM_IN_EINH | string | "Grad KW" |
| STAT_CAM_EX_WERT | real | Istwert Auslassnockenwellensteller |
| STAT_CAM_EX_EINH | string | "Grad KW" |
| STAT_TIA_WERT | real | Ansauglufttemperatur |
| STAT_TIA_EINH | string | "Grad C" |
| STAT_TCO_MES_WERT | real | Kühlmitteltemperatur Rohwert |
| STAT_TCO_MES_EINH | string | "Grad C" |
| STAT_IGA_IGC_WERT | real | Zuendwinkel Zylinder 1 |
| STAT_IGA_IGC_EINH | string | "Grad KW" |
| STAT_TPS_AV_1_WERT | real | Drosselklappenwinkel Potentiometer 1 |
| STAT_TPS_AV_1_EINH | string | "%DK" |
| STAT_MAF_KGH_MES_BAS_WERT | real | Gemessene Luftmasse Rohwert |
| STAT_MAF_KGH_MES_BAS_EINH | string | "kg/h" |
| STAT_TQI_AV_WERT | real | Aktuelle Drehmomentanforderung |
| STAT_TQI_AV_EINH | string | "Nm" |
| STAT_VB_WERT | real | Batteriespannung |
| STAT_VB_EINH | string | "V" |
| STAT_V_PVS_1_WERT | real | Pedalwertgeber 1 Rohwert |
| STAT_V_PVS_1_EINH | string | "V" |
| STAT_TCO_2_MES_WERT | real | Kuehlmittelauslasstemperatur Rohwert |
| STAT_TCO_2_MES_EINH | string | "Grad C" |
| STAT_NL_0_WERT | real | Spannung Klopfwerte Zylinder 1 (phys) |
| STAT_NL_0_EINH | string | "V" |
| STAT_NL_1_WERT | real | Spannung Klopfwerte Zylinder 5 (phys) |
| STAT_NL_1_EINH | string | "V" |
| STAT_NL_2_WERT | real | Spannung Klopfwerte Zylinder 3 (phys) |
| STAT_NL_2_EINH | string | "V" |
| STAT_NL_3_WERT | real | Spannung Klopfwerte Zylinder 6 (phys) |
| STAT_NL_3_EINH | string | "V" |
| STAT_NL_4_WERT | real | Spannung Klopfwerte Zylinder 2 (phys) |
| STAT_NL_4_EINH | string | "V" |
| STAT_NL_5_WERT | real | Spannung Klopfwerte Zylinder 4 (phys) |
| STAT_NL_5_EINH | string | "V" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dfmonitor"></a>
### STATUS_DFMONITOR

Batterieladezustand auslesen DFMONITOR (0x4001)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AUSGANG_WERT | real | Umrechnung:0x00 bis 0xFF in 0 bis 99.609375%oder Zuordnung:0x00-0x7F = AUS0x80-0xFF = EIN |
| STAT_AUSGANG_EINH | string | "%" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-1"></a>
### STATUS_DIGITAL_1

Status Schaltzustaende 1 DIGITAL_1 (0x4002)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AC_EIN | unsigned char | Status Klimabereitschaft, a2l: B_ko |
| STAT_AC_EIN_TEXT | string | Status Klimabereitschaft, a2l: B_ko |
| STAT_BTS_EIN | unsigned char | Status Bremslichtschalter-Kanal 2, a2l: B_br |
| STAT_BTS_EIN_TEXT | string | Status Bremslichtschalter-Kanal 2, a2l: B_br |
| STAT_BLS_EIN | unsigned char | Status Bremslichtschalter-Kanal 1, a2l: B_bl |
| STAT_BLS_EIN_TEXT | string | Status Bremslichtschalter-Kanal 1, a2l: B_bl |
| STAT_KUPPL_EIN | unsigned char | Status Kupplungsschalter, a2l: B_kuppl |
| STAT_KUPPL_EIN_TEXT | string | Status Kupplungsschalter, a2l: B_kuppl |
| STAT_MOTOR_EIN | unsigned char | Status Motorzustand, a2l: B_nmot |
| STAT_MOTOR_EIN_TEXT | string | Status Motorzustand, a2l: B_nmot |
| STAT_KL15_EIN | unsigned char | Status Klemme-15, a2l: B_kl15 |
| STAT_KL15_EIN_TEXT | string | Status Klemme-15, a2l: B_kl15 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-nockenwelle-adaption"></a>
### STATUS_NOCKENWELLE_ADAPTION

Nockenwellenadationswerte auslesen NOCKENWELLE_ADAPTION (0x4006)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PSN_EDGE_AD_CAM_IN_1_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_1_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_IN_2_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_2_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_IN_3_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_3_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_IN_4_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_4_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_IN_5_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_5_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_IN_6_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_6_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_1_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_1_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_2_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_2_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_3_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_3_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_4_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_4_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_5_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_5_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_6_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_6_EINH | string | "deg CrS" |
| STAT_WINKELVERSATZ_ZYL_1_WERT | real | Nullpunktverschiebung fuer die Winkelversatz Diagnose |
| STAT_WINKELVERSATZ_ZYL_1_EINH | string | "deg CrS" |
| STAT_WINKELVERSATZ_ZYL_5_WERT | real | Nullpunktverschiebung fuer die Winkelversatz Diagnose |
| STAT_WINKELVERSATZ_ZYL_5_EINH | string | "deg CrS" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-0"></a>
### STATUS_DIGITAL_0

Status Schaltzustaende 0 DIGITAL_0 (0x4007)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LS1_REGELUNG | unsigned char | Status Regelkreis Bank 1 |
| STAT_LS1_REGELUNG_TEXT | string | Status Regelkreis Bank 1 |
| STAT_LS2_REGELUNG | unsigned char | Status Regelkreis Bank 2 |
| STAT_LS2_REGELUNG_TEXT | string | Status Regelkreis Bank 2 |
| STAT_LSVK1 | unsigned char | Status Lambdaregelung vor Katalysator Bank 1 |
| STAT_LSVK1_TEXT | string | Status Lambdaregelung vor Katalysator Bank 1 |
| STAT_LSVK2 | unsigned char | Status Lambdaregelung vor Katalysator Bank 2 |
| STAT_LSVK2_TEXT | string | Status Lambdaregelung vor Katalysator Bank 2 |
| STAT_LSHK1 | unsigned char | Status Lambdaregelung hinter Katalysator Bank 1 |
| STAT_LSHK1_TEXT | string | Status Lambdaregelung hinter Katalysator Bank 1 |
| STAT_LSHK2 | unsigned char | Status Lambdaregelung hinter Katalysator Bank 2 |
| STAT_LSHK2_TEXT | string | Status Lambdaregelung hinter Katalysator Bank 2 |
| STAT_VL | unsigned char | Status Vollast |
| STAT_VL_TEXT | string | Status Vollast |
| STAT_LL | unsigned char | Status Leerlauf |
| STAT_LL_TEXT | string | Status Leerlauf |
| STAT_DK_ABGLEICH | unsigned char | Status Drosselklappen-Neuabgleich |
| STAT_DK_ABGLEICH_TEXT | string | Status Drosselklappen-Neuabgleich |
| STAT_SCHUBAB | unsigned char | Status Schubabschaltung |
| STAT_SCHUBAB_TEXT | string | Status Schubabschaltung |
| STAT_FAHRSTUFE | unsigned char | Status Fahrstufe |
| STAT_FAHRSTUFE_TEXT | string | Status Fahrstufe |
| STAT_KICKDOWN | unsigned char | Status Kickdownerkennung |
| STAT_KICKDOWN_TEXT | string | Status Kickdownerkennung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-adaption-dk"></a>
### STATUS_ADAPTION_DK

Drosselklappenadaptionswerte auslesen ADAPTION_DK (0x4008)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EV_ADD_WERT | long | Adaption Einstritzventil Offset |
| STAT_EV_ADD_EINH | string | "kg/h" |
| STAT_EV_FAC_WERT | real | Adaption Einspritzventil Faktor |
| STAT_DK_ADD_WERT | long | Adaption Drosselkappe Offset |
| STAT_DK_ADD_EINH | string | "kg/h" |
| STAT_DK_FAC_WERT | real | Adaption Drosselklappe Faktor |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-adaption-gemisch"></a>
### STATUS_ADAPTION_GEMISCH

Gemischadaptionswerte auslesen ADAPTION_GEMISCH (0x400A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAC_1_WERT | real | Lambda adaption carried out by customer (multiplicative share). |
| STAT_FAC_2_WERT | real | Lambda adaption carried out by customer Bank 2 (multiplicative share). |
| STAT_PWM_UP_1_WERT | real | Heater driver PWM duty cycle acquired also by BSW. |
| STAT_PWM_UP_2_WERT | real | Heater driver PWM duty cycle Bank 2 acquired also by BSW. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-vvt"></a>
### STATUS_MESSWERTE_VVT

VVT Messwerte auslesen MESSWERTE_VVT (0x400B)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOLLW_VVT_WERT | real | VVT Exzenterwinkel Sollwert |
| STAT_SOLLW_VVT_EINH | string | "Grad" |
| STAT_ISTW_VVT_WERT | real | VVT Exzenterwinkel Istwert |
| STAT_ISTW_VVT_EINH | string | "Grad" |
| STAT_I_VVT_WERT | real | VVT Stellmotorstrom, Vorzeichen kennzeichnet Bewegungsrichtung |
| STAT_I_VVT_EINH | string | "A" |
| STAT_ULB_VVT_WERT | real | VVT-Spannung Leistungsversorgung (LB) |
| STAT_SRF_VVT_WERT | real | VVT-Sensor Rohwert Führungssensor. |
| STAT_SRF_VVT_EINH | string | "°" |
| STAT_NOTL_VVT | unsigned char | Notlaufzustand VVT |
| STAT_NOTL_VVT_TEXT | string | Notlaufzustand VVT |
| STAT_SUEL_VVT_WERT | unsigned char | Systemueberlastzustand VVT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fasta10"></a>
### FASTA10

FASTA-Messwertblock 10 lesen FASTA10 (0x4015)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BSZSIFNP_WERT | unsigned long | Serviceintervall Betriebsstundenzaehler (bszsifnp_l) |
| STAT_BSZSIFNP_EINH | string | "s" |
| STAT_NMDSFNP_0_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_1_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_2_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_3_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_4_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_5_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_6_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_7_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_8_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_9_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_10_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_11_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_12_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_13_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_14_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_15_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_16_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_17_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_18_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_19_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_20_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_21_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_22_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_23_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_24_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_25_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_26_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_27_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_28_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_29_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_30_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_31_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_32_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_33_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_34_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_35_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_36_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_37_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_38_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_39_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_40_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_41_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_42_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_43_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_44_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_45_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_46_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| STAT_NMDSFNP_47_WERT | unsigned char | Sekundäres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzprofilen. |
| DFDSPROFLE_0_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_1_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_2_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_3_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_4_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_5_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_6_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_7_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_8_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_9_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_10_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_11_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_12_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_13_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_14_WERT | unsigned char | Generatorauslastungsprofil |
| DFDSPROFLE_15_WERT | unsigned char | Generatorauslastungsprofil |
| STAT_IGENKFNP_WERT | real | Generatorstrom kumuliert |
| STAT_TMOTB1_WERT | real | Kühlmitteltemperatur innerhalb Bereich 1 |
| STAT_TMOTB1_EINH | string | "%" |
| STAT_TMOTB2_WERT | real | Kühlmitteltemperatur innerhalb Bereich 2 |
| STAT_TMOTB2_EINH | string | "%" |
| STAT_TMOTB3_WERT | real | Kühlmitteltemperatur innerhalb Bereich 3 |
| STAT_TMOTB3_EINH | string | "%" |
| STAT_TMOTB4_WERT | real | Kühlmitteltemperatur innerhalb Bereich 4 |
| STAT_TMOTB4_EINH | string | "%" |
| STAT_TMOTB5_WERT | real | Kühlmitteltemperatur innerhalb Bereich 5 |
| STAT_TMOTB5_EINH | string | "%" |
| STAT_TOELB1_WERT | real | Motoröltemperatur innerhalb Bereich 1 |
| STAT_TOELB1_EINH | string | "%" |
| STAT_TOELB2_WERT | real | Motoröltemperatur innerhalb Bereich 2 |
| STAT_TOELB2_EINH | string | "%" |
| STAT_TOELB3_WERT | real | Motoröltemperatur innerhalb Bereich 3 |
| STAT_TOELB3_EINH | string | "%" |
| STAT_TOELB4_WERT | real | Motoröltemperatur innerhalb Bereich 4 |
| STAT_TOELB4_EINH | string | "%" |
| STAT_TOELB5_WERT | real | Motoröltemperatur innerhalb Bereich 5 |
| STAT_TOELB5_EINH | string | "%" |
| STAT_TGETB1_WERT | real | Getriebeöltemperatur innerhalb Bereich 1 |
| STAT_TGETB1_EINH | string | "%" |
| STAT_TGETB2_WERT | real | Getriebeöltemperatur innerhalb Bereich 2 |
| STAT_TGETB2_EINH | string | "%" |
| STAT_TGETB3_WERT | real | Getriebeöltemperatur innerhalb Bereich 3 |
| STAT_TGETB3_EINH | string | "%" |
| STAT_TGETB4_WERT | real | Getriebeöltemperatur innerhalb Bereich 4 |
| STAT_TGETB4_EINH | string | "%" |
| STAT_TGETB5_WERT | real | Getriebeöltemperatur innerhalb Bereich 5 |
| STAT_TGETB5_EINH | string | "%" |
| STAT_TUMGB1_WERT | real | Umgebungstemperatur innerhalb Bereich 1 |
| STAT_TUMGB1_EINH | string | "%" |
| STAT_TUMGB2_WERT | real | Umgebungstemperatur innerhalb Bereich 2 |
| STAT_TUMGB2_EINH | string | "%" |
| STAT_TUMGB3_WERT | real | Umgebungstemperatur innerhalb Bereich 3 |
| STAT_TUMGB3_EINH | string | "%" |
| STAT_TUMGB4_WERT | real | Umgebungstemperatur innerhalb Bereich 4 |
| STAT_TUMGB4_EINH | string | "%" |
| STAT_TUMGB5_WERT | real | Umgebungstemperatur innerhalb Bereich 5 |
| STAT_TUMGB5_EINH | string | "%" |
| STAT_N_STET_WERT | unsigned long | 4Byte Zähler Anzahl Statistikkennfeld |
| STAT_TECU_1_1_WERT | unsigned int | 1.1 Statistikkennfeld |
| STAT_TECU_1_2_WERT | unsigned int | 1.2 Statistikkennfeld |
| STAT_TECU_1_3_WERT | unsigned int | 1.3 Statistikkennfeld |
| STAT_TECU_1_4_WERT | unsigned int | 1.4 Statistikkennfeld |
| STAT_TECU_1_5_WERT | unsigned int | 1.5 Statistikkennfeld |
| STAT_TECU_2_1_WERT | unsigned int | 2.1 Statistikkennfeld |
| STAT_TECU_2_2_WERT | unsigned int | 2.2 Statistikkennfeld |
| STAT_TECU_2_3_WERT | unsigned int | 2.3 Statistikkennfeld |
| STAT_TECU_2_4_WERT | unsigned int | 2.4 Statistikkennfeld |
| STAT_TECU_2_5_WERT | unsigned int | 2.5 Statistikkennfeld |
| STAT_TECU_3_1_WERT | unsigned int | 3.1 Statistikkennfeld |
| STAT_TECU_3_2_WERT | unsigned int | 3.2 Statistikkennfeld |
| STAT_TECU_3_3_WERT | unsigned int | 3.3 Statistikkennfeld |
| STAT_TECU_3_4_WERT | unsigned int | 3.4 Statistikkennfeld |
| STAT_TECU_3_5_WERT | unsigned int | 3.5 Statistikkennfeld |
| STAT_TECU_4_1_WERT | unsigned int | 4.1 Statistikkennfeld |
| STAT_TECU_4_2_WERT | unsigned int | 4.2 Statistikkennfeld |
| STAT_TECU_4_3_WERT | unsigned int | 4.3 Statistikkennfeld |
| STAT_TECU_4_4_WERT | unsigned int | 4.4 Statistikkennfeld |
| STAT_TECU_4_5_WERT | unsigned int | 4.5 Statistikkennfeld |
| STAT_TECU_5_1_WERT | unsigned int | 5.1 Statistikkennfeld |
| STAT_TECU_5_2_WERT | unsigned int | 5.2 Statistikkennfeld |
| STAT_TECU_5_3_WERT | unsigned int | 5.3 Statistikkennfeld |
| STAT_TECU_5_4_WERT | unsigned int | 5.4 Statistikkennfeld |
| STAT_TECU_5_5_WERT | unsigned int | 5.5 Statistikkennfeld |
| STAT_SSV_NMOT_1_WERT | unsigned char | Stützstellenverteilung nmot-1 SG-Temperaturhistogramm |
| STAT_SSV_NMOT_2_WERT | unsigned char | Stützstellenverteilung nmot-2 SG-Temperaturhistogramm |
| STAT_SSV_NMOT_3_WERT | unsigned char | Stützstellenverteilung nmot-3 SG-Temperaturhistogramm |
| STAT_SSV_NMOT_4_WERT | unsigned char | Stützstellenverteilung nmot-4 SG-Temperaturhistogramm |
| STAT_SSV_NMOT_5_WERT | unsigned char | Stützstellenverteilung nmot-5 SG-Temperaturhistogramm |
| STAT_SSV_TSG_1_WERT | unsigned char | Stützstellenverteilung tsg 1 SG-Temperaturhistogramm |
| STAT_SSV_TSG_2_WERT | unsigned char | Stützstellenverteilung tsg 2 SG-Temperaturhistogramm |
| STAT_SSV_TSG_3_WERT | unsigned char | Stützstellenverteilung tsg 3 SG-Temperaturhistogramm |
| STAT_SSV_TSG_4_WERT | unsigned char | Stützstellenverteilung tsg 4 SG-Temperaturhistogramm |
| STAT_SSV_TSG_5_WERT | unsigned char | Stützstellenverteilung tsg 5 SG-Temperaturhistogramm |
| STAT_TINT_SGTH_WERT | unsigned char | Zeitintervall für Erfassung SG-Temperatur-Histogramm |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bzeinfo"></a>
### STATUS_BZEINFO

Infospeicher Batterie Zustands Erkennung (BZE) auslesen BZEINFO (0x401A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QV_OUT_M_WERT | real | Gueltiger gemittelter Kapazitaetsverlust (A2L-Name: Qv_out_m) |
| STAT_QV_OUT_M_EINH | string | "%" |
| STAT_QV_QUALI_M_WERT | real | Qualitaetsindex fuer gemittelten Qv-Wert (A2L-Name: Qv_quali_m) |
| STAT_QV_QUALI_M_EINH | string | "%" |
| STAT_QV_STATUS_WERT | char | Prozessstatus / Trend fuer gemittelten Qv-Wert (A2L-Name: Qv_status) |
| STAT_QV_OUT_1_WERT | char | Kapazitaetsverlust letzter Start (A2L-Name: Qv_out_1) |
| STAT_QV_OUT_1_EINH | string | "Ah" |
| STAT_QV_OUT_2_WERT | char | Kapazitaetsverlust 2. letzter Start (A2L-Name: Qv_out_2) |
| STAT_QV_OUT_2_EINH | string | "Ah" |
| STAT_QV_OUT_3_WERT | char | Kapazitaetsverlust 3. letzter Start (A2L-Name: Qv_out_3) |
| STAT_QV_OUT_3_EINH | string | "Ah" |
| STAT_QV_OUT_4_WERT | char | Kapazitaetsverlust 4. letzter Start (A2L-Name: Qv_out_4) |
| STAT_QV_OUT_4_EINH | string | "Ah" |
| STAT_QV_OUT_5_WERT | char | Kapazitaetsverlust 5. letzter Start (A2L-Name: Qv_out_5) |
| STAT_QV_OUT_5_EINH | string | "Ah" |
| STAT_QV_QUALI_1_WERT | real | Qualitaetsindex letzter Qv-Wert (A2L-Name: Qv_quali_1) |
| STAT_QV_QUALI_1_EINH | string | "%" |
| STAT_QV_QUALI_2_WERT | real | Qualitaetsindex 2. letzter Qv-Wert (A2L-Name: Qv_quali_2) |
| STAT_QV_QUALI_2_EINH | string | "%" |
| STAT_QV_QUALI_3_WERT | real | Qualitaetsindex 3. letzter Qv-Wert (A2L-Name: Qv_quali_3) |
| STAT_QV_QUALI_3_EINH | string | "%" |
| STAT_QV_QUALI_4_WERT | real | Qualitaetsindex 4. letzter Qv-Wert (A2L-Name: Qv_quali_4) |
| STAT_QV_QUALI_4_EINH | string | "%" |
| STAT_QV_QUALI_5_WERT | real | Qualitaetsindex 5. letzter Qv-Wert (A2L-Name: Qv_quali_5) |
| STAT_QV_QUALI_5_EINH | string | "%" |
| STAT_QV_TD1_WERT | unsigned int | Zeit seit Qv_out_1 Berechnung (A2L-Name: Qv_td1) |
| STAT_QV_TD1_EINH | string | "h" |
| STAT_QV_TD2_WERT | unsigned int | Zeit zwischen Qv_out_1 und Qv_out_2 (A2L-Name: Qv_td2) |
| STAT_QV_TD2_EINH | string | "h" |
| STAT_QV_TD3_WERT | unsigned int | Zeit zwischen Qv_out_2 und Qv_out_3 (A2L-Name: Qv_td3) |
| STAT_QV_TD3_EINH | string | "h" |
| STAT_QV_TD4_WERT | unsigned int | Zeit zwischen Qv_out_3 und Qv_out_4 (A2L-Name: Qv_td4) |
| STAT_QV_TD4_EINH | string | "h" |
| STAT_QV_TD5_WERT | unsigned int | Zeit zwischen Qv_out_4 und Qv_out_5 (A2L-Name: Qv_td5) |
| STAT_QV_TD5_EINH | string | "h" |
| STAT_QVC_STATUS_1_WERT | real | Ausgang für Schluesselgroeße 1 (A2L-Name: Qvc_status_1) |
| STAT_QVC_STATUS_1_EINH | string | "%" |
| STAT_QVC_STATUS_2_WERT | real | Ausgang für Schluesselgroeße 2 (A2L-Name: Qvc_status_2) |
| STAT_QVC_STATUS_2_EINH | string | "%" |
| STAT_QVC_STATUS_3_WERT | unsigned char | Ausgang für Schluesselgroeße 3 (A2L-Name: Qvc_status_3) |
| STAT_QVC_STATUS_3_EINH | string | "Ah" |
| STAT_QVC_STATUS_4_WERT | char | Ausgang für Schluesselgroeße 4 (A2L-Name: Qvc_status_4) |
| STAT_QV_NV_ZH_WERT | unsigned long | Anzahl der Hystereseauswertungen (A2L-Name: Qv_nv_zh) |
| STAT_QV_NV_EZM_WERT | real | Mittlerer Fehler fuer gesamte Hystereseberechnung (A2L-Name: Qv_nv_ezm) |
| STAT_QV_H2O_WERT | real | Bisheriger Wasserverlust Batterie (A2L-Name: Qv_h2o) |
| STAT_QV_H2OQUALI_WERT | real | Qualitaetswert fuer Wasserverlust Batterie (A2L-Name: Qv_h2oquali) |
| STAT_QV_H2OQUALI_EINH | string | "%" |
| STAT_ST_QVC1_WERT | unsigned char | Statuswort (A2L-Name: St_qvc1) Bedeutung: - 0: Wasserverlust O.K. - 1: Wasserverlust zu hoch |
| STAT_QV_H2OSTATUS_WERT | unsigned char | Status fuer Entwicklung Wasserverlust (A2L-Name: Qv_h2ostatus) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geninfo"></a>
### STATUS_GENINFO

Infospeicher Generatordiagnose erweitert auslesen GENINFO (0x401B)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DGENUB1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) |
| STAT_DGENUB1_EINH | string | "V" |
| STAT_DGENUB2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) |
| STAT_DGENUB2_EINH | string | "V" |
| STAT_DGENUBNZ_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) |
| STAT_DGENUBNZ_EINH | string | "V" |
| STAT_DGENUBERR_WERT | unsigned char | Fehlerstati zur Batteriespannung |
| STAT_DGENUGEN1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) |
| STAT_DGENUGEN1_EINH | string | "V" |
| STAT_DGENUGEN2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) |
| STAT_DGENUGEN2_EINH | string | "V" |
| STAT_DGENUGENNZ_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) |
| STAT_DGENUGENNZ_EINH | string | "V" |
| STAT_DGENUGENERR_WERT | unsigned char | Fehlerstati zur Generatorsollspannung |
| STAT_DGENGRENZ1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) |
| STAT_DGENGRENZ1_EINH | string | "A" |
| STAT_DGENGRENZ2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) |
| STAT_DGENGRENZ2_EINH | string | "A" |
| STAT_DGENGRENZNZ_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) |
| STAT_DGENGRENZNZ_EINH | string | "A" |
| STAT_DGENGRENZERR_WERT | unsigned char | Fehlerstati zur Erregerstrombegrenzung |
| STAT_DGENUB1_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz |
| STAT_DGENUB1_MD1_EINH | string | "V" |
| STAT_DGENUB2_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz |
| STAT_DGENUB2_MD1_EINH | string | "V" |
| STAT_DGENUBNZ_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz |
| STAT_DGENUBNZ_MD1_EINH | string | "V" |
| STAT_DGENUBERR_MD1_WERT | unsigned char | Fehlerstati zur Batteriespannung zu 1. Messdatensatz |
| STAT_DGENUGEN1_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz |
| STAT_DGENUGEN1_MD1_EINH | string | "V" |
| STAT_DGENUGEN2_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz |
| STAT_DGENUGEN2_MD1_EINH | string | "V" |
| STAT_DGENUGENNZ_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz |
| STAT_DGENUGENNZ_MD1_EINH | string | "V" |
| STAT_DGENUGENERR_MD1_WERT | unsigned char | Fehlerstati zur Generatorsollspannung zu 1. Messdatensatz |
| STAT_DGENGRENZ1_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz |
| STAT_DGENGRENZ1_MD1_EINH | string | "A" |
| STAT_DGENGRENZ2_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz |
| STAT_DGENGRENZ2_MD1_EINH | string | "A" |
| STAT_DGENGRENZNZ_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz |
| STAT_DGENGRENZNZ_MD1_EINH | string | "A" |
| STAT_DGENGRENZERR_MD1_WERT | unsigned char | Fehlerstati zur Erregerstrombegrenzung zu 1. Messdatensatz |
| STAT_DGENUB1_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz |
| STAT_DGENUB1_MD2_EINH | string | "V" |
| STAT_DGENUB2_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz |
| STAT_DGENUB2_MD2_EINH | string | "V" |
| STAT_DGENUBNZ_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz |
| STAT_DGENUBNZ_MD2_EINH | string | "V" |
| STAT_DGENUBERR_MD2_WERT | unsigned char | Fehlerstati zur Batteriespannung zu 2. Messdatensatz |
| STAT_DGENUGEN1_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz |
| STAT_DGENUGEN1_MD2_EINH | string | "V" |
| STAT_DGENUGEN2_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz |
| STAT_DGENUGEN2_MD2_EINH | string | "V" |
| STAT_DGENUGENNZ_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz |
| STAT_DGENUGENNZ_MD2_EINH | string | "V" |
| STAT_DGENUGENERR_MD2_WERT | unsigned char | Fehlerstati zur Generatorsollspannung zu 2. Messdatensatz |
| STAT_DGENGRENZ1_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz |
| STAT_DGENGRENZ1_MD2_EINH | string | "A" |
| STAT_DGENGRENZ2_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz |
| STAT_DGENGRENZ2_MD2_EINH | string | "A" |
| STAT_DGENGRENZNZ_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz |
| STAT_DGENGRENZNZ_MD2_EINH | string | "A" |
| STAT_DGENGRENZERR_MD2_WERT | unsigned char | Fehlerstati zur Erregerstrombegrenzung zu 2. Messdatensatz |
| STAT_DGENERRST_MD1_WERT | unsigned int | Trigger zur Statuswortablage zu 1. Messdatensatz |
| STAT_DGENERRST_MD2_WERT | unsigned int | Trigger zur Statuswortablage zu 2. Messdatensatz |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-verbredinfo"></a>
### STATUS_VERBREDINFO

Verbraucherreduzierungsspeicher auslesen VERBREDINFO (0x401D)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERBREDUCINF_0_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_1_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_2_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_3_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_4_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_5_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_6_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_7_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_8_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_9_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_10_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_11_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_12_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_13_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_14_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_15_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_16_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_17_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_18_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_19_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_20_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_21_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_22_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_23_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_24_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_25_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_26_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_27_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_28_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_29_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_30_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| STAT_VERBREDUCINF_31_WERT | unsigned char | Ringspeicher Verbraucherreduktion |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dmeref"></a>
### STATUS_DMEREF

BMW Programmstands-Bezeichnung auslesen DMEREF (0x401F)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DMEREF_WERT | string | Logistikbereich |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-ewap"></a>
### STATUS_MESSWERTE_EWAP

elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) Messwerte auslesen MESSWERTE_EWAP (0x4024)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_U_EWAP_WERT | real | Pumpenspannung elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) |
| STAT_U_EWAP_EINH | string | "V" |
| STAT_T_EWAP_WERT | real | Pumpentemperatur elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) |
| STAT_I_EWAP_WERT | real | Pumpenstrom elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) |
| STAT_I_EWAP_EINH | string | "%" |
| STAT_ERR_BIT7_EWAP | unsigned char | Error Status Deblockierung aktiv |
| STAT_ERR_BIT6_EWAP | unsigned char | Error Status falsche Versorgungsspannung |
| STAT_ERR_BIT5_EWAP | unsigned char | Error Status Trockenlauf |
| STAT_ERR_BIT4_EWAP | unsigned char | Error Status Ueberstrom |
| STAT_ERR_BIT3_EWAP | unsigned char | Error Status Uebertemperatur |
| STAT_ERR_BIT2_EWAP | unsigned char | Error Status Sperrung-Deblockierung |
| STAT_ERR_BIT1_EWAP | unsigned char | Error Status Keine Drehzahlueberwachung |
| STAT_ERR_BIT0_EWAP | unsigned char | Error Status Sperrung-Sollwert |
| STAT_TMOT_WERT | real | Motortemperatur TCO/TMOT |
| STAT_TMOT_EINH | string | "Grad C" |
| STAT_UBAT_WERT | real | Batteriespannung |
| STAT_UBAT_EINH | string | "V" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-vad"></a>
### STATUS_MESSWERTE_VAD

Variantenadaptionen auslesen MESSWERTE_VAD (0x4025)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_I_HA_WERT | real | Hinterachseuebersetzung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmmode9"></a>
### STATUS_RBMMODE9

Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9) RBMMODE9 (0x4026)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OBDCOND_WERT | unsigned int | OBD Monitoring Conditions Encountered Counts (general denominator) |
| STAT_IGNCNTR_WERT | unsigned int | Ignition Counter |
| STAT_CATCOMP1_WERT | unsigned int | Catalyst Monitor Completion Counts Bank 1 (numerator) |
| STAT_CATCOND1_WERT | unsigned int | Catalyst Monitor Conditions Encountered Counts Bank 1 (denominator) |
| STAT_CATCOMP2_WERT | unsigned int | Catalyst Monitor Completion Counts Bank 2 (numerator) |
| STAT_CATCOND2_WERT | unsigned int | Catalyst Monitor Conditions Encountered Counts Bank 2 (denominator) |
| STAT_O2SCOMP1_WERT | unsigned int | O2 Sensor Monitor Completion Counts Bank 1 (numerator) |
| STAT_O2SCOND1_WERT | unsigned int | O2 Sensor Monitor Conditions Encountered Counts Bank 1 (denominator) |
| STAT_O2SCOMP2_WERT | unsigned int | O2 Sensor Monitor Completion Counts Bank 2 (numerator) |
| STAT_O2SCOND2_WERT | unsigned int | O2 Sensor Monitor Conditions Encountered Counts Bank 2 (denominator) |
| STAT_EGRCOMP_WERT | unsigned int | EGR Monitor Completion Condition Counts (numerator) |
| STAT_EGRCOND_WERT | unsigned int | EGR Monitor Conditions Encountered Counts (denominator) |
| STAT_AIRCOMP1_WERT | unsigned int | AIR Monitor Completion Condition Counts Bank 1 (Secondary Air) (numerator) |
| STAT_AIRCOND1_WERT | unsigned int | AIR Monitor Conditions Encountered Counts Bank 1 (Secondary Air) (denominator) |
| STAT_EVAPCOMP_WERT | unsigned int | EVAP Monitor Completion Condition Counts (numerator) |
| STAT_EVAPCOND_WERT | unsigned int | EVAP Monitor Conditions Encountered Counts (denominator) |
| STAT_SO2COMP1_WERT | unsigned int | SO2 Sensor Monitor Completion Condition Counts Bank 1 (Numerator) |
| STAT_SO2COND1_WERT | unsigned int | SO2 Sensor Monitor Conditions Encountered Counts Bank 1 (Denominator) |
| STAT_SO2COMP2_WERT | unsigned int | SO2 Sensor Monitor Completion Condition Counts Bank 2 (Numerator) |
| STAT_SO2COND2_WERT | unsigned int | SO2 Sensor Monitor Conditions Encountered Counts Bank 2 (Denominator) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmme1"></a>
### STATUS_RBMME1

Rate Based Monitoring Motorsteuerung ME... Block 1 auslesen (Vorhalt) RBMME1 (0x4029)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NUM_FID_BHKT_WERT | unsigned int | Katalysator Bank1-Numerator |
| STAT_DEN_FID_BHKT_WERT | unsigned int | Katalysator Bank1-Denumerator |
| STAT_NUM_FID_CDLSU_WERT | unsigned int | LSU dynamisch zu langsam Bank1 Numerator |
| STAT_DEN_FID_CDLSU_WERT | unsigned int | LSU dynamisch zu langsam Bank1-Denumerator |
| STAT_NUM_FID_CULSU_WERT | unsigned int | Spannungsüberwachung LSU Bank1-Numerator |
| STAT_DEN_FID_CULSU_WERT | unsigned int | Spannungsüberwachung LSU Bank1-Denumerator |
| STAT_NUM_FID_CPLSU_WERT | unsigned int | Plausibilität der LSU Bank1-Numerator |
| STAT_DEN_FID_CPLSU_WERT | unsigned int | Plausibilität der LSU Bank1-Denumerator |
| STAT_NUM_FID_ATEVTLD_WERT | unsigned int | TEV-Check mit Tankleckagediagnose aktiv Numerator |
| STAT_DEN_FID_ATEVTLD_WERT | unsigned int | TEV-Check mit Tankleckage aktiv Denumerator |
| STAT_NUM_FID_CTESG_WERT | unsigned int | Tankdiagnose, Grobleck-Numerator |
| STAT_DEN_FID_CTESG_WERT | unsigned int | Tankdiagnose, Grobleck-Denumerator |
| STAT_NUM_FID_CDMTK_WERT | unsigned int | Tankdiagnose, Feinstleck-Numerator |
| STAT_DEN_FID_CDMTK_WERT | unsigned int | Tankdiagnose, Feinstleck-Denumerator |
| STAT_NUM_FID_CDMTL_WERT | unsigned int | Tankdiagnose, Modulfehler-Numerator |
| STAT_DEN_FID_CDMTL_WERT | unsigned int | Tankdiagnose, Modulfehler-Denumerator |
| STAT_NUM_FID_CENWS_WERT | unsigned int | Nockenwellensteuerung Einlass Bank 1-Numerator |
| STAT_DEN_FID_CENWS_WERT | unsigned int | Nockenwellensteuerung Einlass Bank1-Denumerator |
| STAT_NUM_FID_CANWS_WERT | unsigned int | Nockenwellensteuerung Auslass Bank1-Numerator |
| STAT_DEN_FID_CANWS_WERT | unsigned int | Nockenwellensteuerung Auslass Bank 1-Denumerator |
| STAT_NUM_FID_CNWVE_WERT | unsigned int | Nockenwellenverriegelungsdiagnose Einlass Bank1-Numerator |
| STAT_DEN_FID_CNWVE_WERT | unsigned int | Nockenwellenverriegelungsdiagnose Einlass Bank1-Denumerator |
| STAT_NUM_FID_CNWVA_WERT | unsigned int | Nockenwellenverriegelungsdiagnose Auslass Bank1-Numerator |
| STAT_DEN_FID_CNWVA_WERT | unsigned int | Nockenwellenverriegelungsdiagnose Ausass Bank1-Denumerator |
| STAT_NUM_FID_EPMCASOFSERRCASI1_WERT | unsigned int | Zuordnung Einlassnockenwelle zu Kurbelwelle-Numerator |
| STAT_DEN_FID_EPMCASOFSERRCASI1_WERT | unsigned int | Zuordnung Einlassnockenwelle zu Kurbelwelle-Denumerator |
| STAT_NUM_FID_EPMCASOFSERRCASO1_WERT | unsigned int | Zuordnung Auslassnockenwelle zu Kurbelwelle-Numerator |
| STAT_DEN_FID_EPMCASOFSERRCASO1_WERT | unsigned int | Zuordnung Auslassnockenwelle zu Kurbelwelle Numerator |
| STAT_NUM_FID_BLASH_WERT | unsigned int | Lambdasondenalterung hinter KAT-Numerator |
| STAT_DEN_FID_BLASH_WERT | unsigned int | Lambdasondenalterung hinter KAT-Denumerator |
| STAT_NUM_FID_BHDYRE_WERT | unsigned int | Diagnose Delay time für O2 Sensor nach Hauptkatalysator-Numerator |
| STAT_DEN_FID_BHDYRE_WERT | unsigned int | Diagnose Delay time für O2 Sensor nach Hauptkatalysator-Denumerator |
| STAT_NUM_FID_ADSLS_WERT | unsigned int | Sekundärluftsystem-Numerator |
| STAT_DEN_FID_ADSLS_WERT | unsigned int | Sekundärluftsystem-Denumerator |
| STAT_NUM_FID_CSLSU_WERT | unsigned int | Überwachung des Schubadaptionsfaktors LSU-Numerator |
| STAT_DEN_FID_CSLSU_WERT | unsigned int | Überwachung des Schubadaptionsfaktors LSU-Denumerator |
| STAT_NUM_FID_CTRSH_WERT | unsigned int | Diagnose Transition Time für O2Sensor nach Hauptkat-Numerator |
| STAT_DEN_FID_CTRSH_WERT | unsigned int | Diagnose Transition Time für O2Sensor nach Hauptkat-Denumerator |
| STAT_NUM_FID_DVVTLRUWRN_WERT | unsigned int | Diagnose Ventilhubverstellung Stellgliedfehler aus Lagereglerüberwachung- Numerator |
| STAT_DEN_FID_DVVTLRUWRN_WERT | unsigned int | Diagnose Ventilhubverstellung Warnschwelle Regelabweichung aus Lagereglerüberwachung- Denominator |
| STAT_NUM_FID_DVVTLRUERR_WERT | unsigned int | Diagnose Ventilhubverstellung Stellgliedfehler aus Lagereglerüberwachung- Numerator |
| STAT_DEN_FID_DVVTLRUERR_WERT | unsigned int | Diagnose Ventilhubverstellung Stellgliedfehler aus Lagereglerüberwachung- Denominator |
| STAT_NUM_FID_ATEVSPL_WERT | unsigned int | Diagnose TEV zweite Einleitstelle mit DMTL zweite Einleitstelle während Fahrt Numerator |
| STAT_DEN_FID_ATEVSPL_WERT | unsigned int | Diagnose TEV zweite Einleitstelle mit DMTL zweite Einleitstelle während Fahrt Denominator |
| STAT_NUM_FID_CTEVSPLB_WERT | unsigned int | Diagnose TEV zweite Einleitstelle mit DMTL Prüfung auf Blockade im Nachlauf Numerator |
| STAT_DEN_FID_CTEVSPLB_WERT | unsigned int | Diagnose TEV zweite Einleitstelle mit DMTL Prüfung auf Blockade im Nachlauf Denominator |
| STAT_NUM_FID_BDLSU_WERT | unsigned int | DDYLSU Adaption Numerator |
| STAT_DEN_FID_BDLSU_WERT | unsigned int | DDYLSU Adaption Denominator |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmme2"></a>
### STATUS_RBMME2

Rate Based Monitoring Motorsteuerung ME... Block 2 auslesen (Vorhalt) RBMME2 (0x402A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NUM_FID_CCUHR_WERT | unsigned int | CAN relativer Zeitgeber-Numerator |
| STAT_DEN_FID_CCUHR_WERT | unsigned int | CAN relativer Zeitgeber-Denumerator |
| STAT_NUM_FID_CHSHK_WERT | unsigned int | Heizung Lambdasonde hinter KAT-Numerator |
| STAT_DEN_FID_CHSHK_WERT | unsigned int | Heizung Lambdasonde hinter KAT-Denumerator |
| STAT_NUM_FID_CHSV_WERT | unsigned int | Heizung Lamdbasonde vor KAT-Numerator |
| STAT_DEN_FID_CHSV_WERT | unsigned int | Heizung Lambdasonde vor KAT-Denumerator |
| STAT_NUM_FID_BLLRH_WERT | unsigned int | Leerlaufregelung-Numerator |
| STAT_DEN_FID_BLLRH_WERT | unsigned int | Leerlaufregelung-Denumerator |
| STAT_NUM_FID_BLLRKH_WERT | unsigned int | Leerlaufregelung während KAT-Heizen-Numerator |
| STAT_DEN_FID_BLLRKH_WERT | unsigned int | Leerlaufregelung während KAT-Heizen-Denumerator |
| STAT_NUM_FID_CPUR_WERT | unsigned int | Umgebungsdrucksensor Range Check-Numerator |
| STAT_DEN_FID_CPUR_WERT | unsigned int | Umgebungsdrucksensor Range Check-Denumerator |
| STAT_NUM_FID_CTAVDC_WERT | unsigned int | Kaltstartdiagnose Ansauglufttemperatursensor vor DK-Numerator |
| STAT_DEN_FID_CTAVDC_WERT | unsigned int | Kaltstartdiagnose Ansauglufttemperatursensor vor DK-Denumerator |
| STAT_NUM_FID_CTAVDR_WERT | unsigned int | Diagnose Ansauglufttemperatursensor VDK-Denumerator |
| STAT_DEN_FID_CTAVDR_WERT | unsigned int | Diagnose Ansauglufttemperatursensor VDK-Denumerator |
| STAT_NUM_FID_CTANLC_WERT | unsigned int | Kaltstartdiagnose Ansauglufttemperatursensor nach Luftfilter-Numerator |
| STAT_DEN_FID_CTANLC_WERT | unsigned int | Kaltstartdiagnose Ansauglufttemperatursensor nach Luftfilter-Denumerator |
| STAT_NUM_FID_CTANLR_WERT | unsigned int | Diagnsoe Ansauglufttemperatursensor nach Luftfilter-Numerator |
| STAT_DEN_FID_CTANLR_WERT | unsigned int | Diagnose Ansauglufttemperatursensor nach Luftfilter-Denumerator |
| STAT_NUM_FID_CTM_WERT | unsigned int | Motortemperatur TMOT-Numerator |
| STAT_DEN_FID_CTM_WERT | unsigned int | Motortemperatur TMOT-Denumerator |
| STAT_NUM_FID_CTMCS_WERT | unsigned int | Motortemperatur TMOT-Sensor bei Kaltstart-Numerator |
| STAT_DEN_FID_CTMCS_WERT | unsigned int | Motortemperatur TMOT-Sensor bei Kaltstart-Denumerator |
| STAT_NUM_FID_CTUM_WERT | unsigned int | Umgebungstemperatur TUM-Numerator |
| STAT_DEN_FID_CTUM_WERT | unsigned int | Umgebungstemperatur TUM-Denumerator |
| STAT_NUM_FID_CVFZ_WERT | unsigned int | Geschwindigkeitssignal-Numerator |
| STAT_DEN_FID_CVFZ_WERT | unsigned int | Geschwindigkeitssignal-Denumerator |
| STAT_NUM_FID_CDVEF_WERT | unsigned int | DV-E Fehler bei Federprüfung-Numerator |
| STAT_DEN_FID_CDVEF_WERT | unsigned int | V-E Fehler bei Federprüfung-Denumerator |
| STAT_NUM_FID_CDVEL_WERT | unsigned int | DV-E Lageabweichung-Numerator |
| STAT_DEN_FID_CDVEL_WERT | unsigned int | DV-E Lageabweichung-Denumerator |
| STAT_NUM_FID_CDVER_WERT | unsigned int | DV-E Regelbereich-Numerator |
| STAT_DEN_FID_CDVER_WERT | unsigned int | DV-E Regelbereich-Denumerator |
| STAT_NUM_FID_BMW_HFMPL_WERT | unsigned int | Plausibilisierung Luftmassenmesser-Numerator |
| STAT_DEN_FID_BMW_HFMPL_WERT | unsigned int | Plausibilisierung Luftmassenmesser-Denumerator |
| STAT_NUM_FID_BMW_DKPSRPL_WERT | unsigned int | Plausibilisierung Drucksensor Saugrohr-Numerator |
| STAT_DEN_FID_BMW_DKPSRPL_WERT | unsigned int | Plausiblisierung Drucksensor Saugrohr-Denumerator |
| STAT_NUM_FID_CDK_WERT | unsigned int | DK-Potentiometer-Numerator |
| STAT_DEN_FID_CDK_WERT | unsigned int | DK-Potentiometer-Denumerator |
| STAT_NUM_FID_CDK1P_WERT | unsigned int | Drosselklappenpotentiometer 1-Numerator |
| STAT_DEN_FID_CDK1P_WERT | unsigned int | Drosselklappenpotentiometer 1-Denumerator |
| STAT_NUM_FID_CDK2P_WERT | unsigned int | Drosselklappenpotentiometer 2-Numerator |
| STAT_DEN_FID_CDK2P_WERT | unsigned int | Drosselklappenpotentiometer 2-Denumerator |
| STAT_NUM_FID_CKUP_WERT | unsigned int | Pedalwertgeber Kupplung-Numerator |
| STAT_DEN_FID_CKUP_WERT | unsigned int | Pedalwertgeber Kupplung-Denumerator |
| STAT_NUM_FID_CPVDR_WERT | unsigned int | Drucksensor vor Drosselklappe Plausibel Diagnose-Numerator |
| STAT_DEN_FID_CPVDR_WERT | unsigned int | Drucksensor vor Drosselklappe Plausibel Diagnose-Denumerator |
| STAT_NUM_FID_CDSKVR_WERT | unsigned int | Diagnose Hochdrucksensor plausibel-Numerator |
| STAT_DEN_FID_CDSKVR_WERT | unsigned int | Diagnose Hochdrucksensor plausibel-Denumerator |
| STAT_NUM_FID_BMW_DMDKH_WERT | unsigned int | Md-Überwachung bei Katheizen-Numerator |
| STAT_DEN_FID_BMW_DMDKH_WERT | unsigned int | Md-Überwachung bei Katheizen-Denumerator |
| STAT_NUM_FID_CENCS_WERT | unsigned int | Funktion NW Stellerdiagnose-Einlass CERS-Numerator |
| STAT_DEN_FID_CENCS_WERT | unsigned int | Funktion NW Stellerdiagnose-Einlass CERS-Denumerator |
| STAT_NUM_FID_CANCS_WERT | unsigned int | Funktion NW Stellerdiagnose-Auslass CERS-Numerator |
| STAT_DEN_FID_CANCS_WERT | unsigned int | Funktion NW Stellerdiagnose-Auslass CERS-Denumerator |
| STAT_NUM_FID_CHDRKH_WERT | unsigned int | Raildruckregelung während KAT-Heizen CERS-Numerator |
| STAT_DEN_FID_CHDRKH_WERT | unsigned int | Raildruckregelung während KAT-Heizen CERS Denumerator |
| STAT_NUM_FID_CETKHL_WERT | unsigned int | Zündwinkelwirkungsgraddiagnose bei Katheizen(im Leerlauf) CERS-Numerator |
| STAT_DEN_FID_CETKHL_WERT | unsigned int | Zündwinkelwirkungsgraddiagnose bei Katheizen (im Leerlauf) CERS-Denumerator |
| STAT_NUM_FID_CTEOEH_WERT | unsigned int | Diagnose CAN-Uhr ist zu schnell-Numerator |
| STAT_DEN_FID_CTEOEH_WERT | unsigned int | Diagnose CAN-Uhr ist zu schnell-Denumerator |
| STAT_NUM_FID_CTEOEL_WERT | unsigned int | Diagnose CAN-Uhr ist zu langsam-Numerator |
| STAT_DEN_FID_CTEOEL_WERT | unsigned int | Diagnose CAN-Uhr ist zu langsam-Denumerator |
| STAT_NUM_FID_CTEOES_WERT | unsigned int | Diagnose Einseitiger Fehler der CAN-Uhr-Numerator |
| STAT_DEN_FID_CTEOES_WERT | unsigned int | Diagnose Einseitiger Fehler der CAN-Uhr-Denumerator |
| STAT_NUM_FID_CTEOET_WERT | unsigned int | Diagnose Fehler der CAN-Uhr (beidseitiger Check)-Numerator |
| STAT_DEN_FID_CTEOET_WERT | unsigned int | Diagnose Fehler der CAN-Uhr (beidseitiger Check)-Denumerator |
| STAT_NUM_FID_CETKHT_WERT | unsigned int | Zündwinkelwirkungsgraddiagnose bei Katheizen (im Teillastbereich) CERS-Numerator |
| STAT_DEN_FID_CETKHT_WERT | unsigned int | Zündwinkelwirkungsgraddiagnose bei Katheizen (im Teillastbereich) CERS-Denumerator |
| STAT_NUM_FID_BMW_ATLDIAG_WERT | unsigned int | Diagnose Ladedruck-Numerator |
| STAT_DEN_FID_BMW_ATLDIAG_WERT | unsigned int | Diagnose Ladedruck-Denumerator |
| STAT_NUM_FID_CHFMR_WERT | unsigned int | HFM-Rationality-Diagnose-Numerator |
| STAT_DEN_FID_CHFMR_WERT | unsigned int | HFM-Rationality-Diagnose-Denominator |
| STAT_NUM_FID_CAFIMD_WERT | unsigned int | Cylinder-Imbalance Diagnose-Numerator |
| STAT_DEN_FID_CAFIMD_WERT | unsigned int | Cylinder-Imbalance Diagnose-Denominator |
| STAT_NUM_FID_CIP_WERT | unsigned int | IP Lambdasondenleitung Diagnose-Numerator |
| STAT_DEN_FID_CIP_WERT | unsigned int | IP Lambdasondenleitung Diagnose-Denominator |
| STAT_NUM_FID_CTH_WERT | unsigned int | Thermostat Diagnose-Numerator |
| STAT_DEN_FID_CTH_WERT | unsigned int | Thermostat Diagnose-Denominator |
| STAT_NUM_FID_BMW_DOR_WERT | unsigned int | Aktivierung Premair-Diagnose-Numerator |
| STAT_DEN_FID_BMW_DOR_WERT | unsigned int | Aktivierung Premair-Diagnose-Denominator |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-ibs"></a>
### STATUS_MESSWERTE_IBS

Messwerte IBS auslesen MESSWERTE_IBS (0x402B)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_T_BATT_WERT | real | Batterietemperatur |
| STAT_T_BATT_EINH | string | "Grad C" |
| STAT_I_BATT_WERT | real | Batteriestrom von IBS gemessen |
| STAT_I_BATT_EINH | string | "A" |
| STAT_U_BATT_WERT | real | Batteriespannung von IBS gemessen |
| STAT_U_BATT_EINH | string | "V" |
| STAT_IBSINFO_0_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_1_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_2_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_3_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_4_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_5_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_6_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_7_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_8_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_9_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_10_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_11_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_12_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_13_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_14_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_15_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_16_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_17_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_18_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_19_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_20_WERT | unsigned char | IBS Fastadaten |
| STAT_IBSINFO_21_WERT | unsigned char | IBS Fastadaten |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-lrp"></a>
### STATUS_MESSWERTE_LRP

Messwerte Laufruhepruefung auslesen MESSWERTE_LRP (0x402D)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ST_VBRVS_AUS_WERT | unsigned int | Statuswort Verbrennungsregelung fuer Service |
| STAT_ST_VBRVS_EIN_WERT | unsigned char | Statuswort Verbrennungsregelung vom Tester |
| STAT_ST_VBRVS_EINNV_WERT | unsigned char | Statuswort Verbrennungsregelung vom Tester nichtfluechtig |
| STAT_AMO_05_WERT | real | Gesamte DFT 0,5 Motorordnung |
| STAT_AMO_10_WERT | real | Gesamte DFT 1,0 Motorordnung |
| STAT_AMO_15_WERT | real | Gesamte DFT 1,5 Motorordnung |
| STAT_AMO_20_WERT | real | Gesamte DFT 2,0 Motorordnung |
| STAT_EXWINKKOR_WERT | real | Korrekturwinkel Excenterwelle zur Hubkorrektur |
| STAT_EXWINKKOR_EINH | string | "°" |
| STAT_ZYLHUBKOR_WERT | unsigned char | Fuer Hubkorrektur ausgewaehlter Zylinder |
| STAT_MINHUB_WERT | real | Tatsaechlich wirksamer Minhub (nach Ein-/Ausblendungsfakoren) |
| STAT_MINHUB_EINH | string | "mm" |
| STAT_F_MINHUB_WERT | real | Faktor Ein-/Ausblendung Minhub ueber Tmot und Nkw |
| STAT_MINHUB_ROH_WERT | real | Minhubrohwert aus Adaption |
| STAT_MINHUB_ROH_EINH | string | "mm" |
| STAT_MINHUBVS_WERT | real | Vorgabe Minhub ueber Tester |
| STAT_MINHUBVS_EINH | string | "mm" |
| STAT_MINHUBVS_IST_WERT | real | Tatsaechlich wirksamer Minhub aus Verstelleingriff (vor Ein-/Ausblendungsfaktoren) |
| STAT_MINHUBVS_IST_EINH | string | "mm" |
| STAT_MINHUBVSNV_WERT | real | Dauerhaft fest programmierter Minhub |
| STAT_MINHUBVSNV_EINH | string | "mm" |
| STAT_S_VSMNHB | unsigned char | Schalter fuer Testereingriff |
| STAT_S_VSMNHB_TEXT | string | Schalter fuer Testereingriff |
| STAT_S_VSMNHBNV_WERT | unsigned char | Schalter fuer Testereingriff |
| STAT_LURABS_F_0_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (pysikalischer Zylinder 1) |
| STAT_LURDIF_F_0_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (pysikalischer Zylinder 1) |
| STAT_LURABS_F_1_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) (pysikalischer Zylinder 5) |
| STAT_LURDIF_F_1_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (pysikalischer Zylinder 5) |
| STAT_LURABS_F_2_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (pysikalischer Zylinder 3) |
| STAT_LURDIF_F_2_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) (pysikalischer Zylinder 3) |
| STAT_LURABS_F_3_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (pysikalischer Zylinder 6) |
| STAT_LURDIF_F_3_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) (pysikalischer Zylinder 6) |
| STAT_LURABS_F_4_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (pysikalischer Zylinder 2) |
| STAT_LURDIF_F_4_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (pysikalischer Zylinder 2) |
| STAT_LURABS_F_5_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (pysikalischer Zylinder 4) |
| STAT_LURDIF_F_5_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (pysikalischer Zylinder 4) |
| STAT_AMO_30_WERT | real | Gesamte DFT 3,0 Motorordnung |
| STAT_EXWINKKOR_2_WERT | real | Korrekturwinkel Excenterwelle zur Hubkorrektur |
| STAT_EXWINKKOR_2_EINH | string | "°" |
| STAT_ZYLHUBKOR_2_WERT | unsigned char | Fuer Hubkorrektur ausgewaehlter Zylinder |
| STAT_HUBKORSTAT_WERT | real | Hubkorrektur Status |
| STAT_HUBKORSTAT_2_WERT | real | Hubkorrektur Status |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kqe"></a>
### STATUS_KQE

Messwerte zur Kraftstoffqualitaet auslesen KQE (0x4035)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QB1_WERT | unsigned int | Qualitaetsbereich 1 (Niedrig) |
| STAT_QB2_WERT | unsigned int | Qualitaetsbereich 2 (Mittel) |
| STAT_QB3_WERT | unsigned int | Qualitaetsbereich 3 (Hoch) |
| STAT_KM1_WERT | unsigned long | Kilometerstand 1 |
| STAT_KM1_EINH | string | "km" |
| STAT_KM1QB_WERT | unsigned char | Qualitaetsbereich bei Kilometerstand 1 |
| STAT_KM2_WERT | unsigned long | Kilometerstand 2 |
| STAT_KM2_EINH | string | "km" |
| STAT_KM2QB_WERT | unsigned char | Qualitaetsbereich bei Kilometerstand 2 |
| STAT_KM3_WERT | unsigned long | Kilometerstand 3 |
| STAT_KM3_EINH | string | "km" |
| STAT_KM3QB_WERT | unsigned char | Qualitaetsbereich bei Kilometerstand 3 |
| STAT_KM4_WERT | unsigned long | Kilometerstand 4 |
| STAT_KM4_EINH | string | "km" |
| STAT_KM4QB_WERT | unsigned char | Qualitaetsbereich bei Kilometerstand 4 |
| STAT_KM5_WERT | unsigned long | Kilometerstand 5 |
| STAT_KM5_EINH | string | "km" |
| STAT_KM5QB_WERT | unsigned char | Qualitaetsbereich bei Kilometerstand 5 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-injad"></a>
### STATUS_INJAD

Injektor Adaptionswerte lesen INJAD (Kleinstmengen-Adaption RB-Umfaenge) INJAD (0x403F)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_F_INJAD_XZYL_YMOD_00_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[0]) |
| STAT_F_INJAD_XYZL_YMOD_01_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[1]) |
| STAT_F_INJAD_XZYL_YMOD_02_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[2]) |
| STAT_F_INJAD_XZYL_YMOD_03_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[3]) |
| STAT_F_INJAD_XZYL_YMOD_04_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[4]) |
| STAT_F_INJAD_XZYL_YMOD_05_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[5]) |
| STAT_F_INJAD_XZYL_YMOD_06_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[6]) |
| STAT_F_INJAD_XZYL_YMOD_07_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[7]) |
| STAT_F_INJAD_XZYL_YMOD_08_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[8]) |
| STAT_F_INJAD_XZYL_YMOD_09_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[9]) |
| STAT_F_INJAD_XZYL_YMOD_10_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[10]) |
| STAT_F_INJAD_XZYL_YMOD_11_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: fakkorteadp_w[11]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_00_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[0]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_00_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_01_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[1]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_01_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_02_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[2]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_02_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_03_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[3]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_03_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_04_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[4]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_04_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_05_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[5]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_05_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_06_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[6]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_06_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_07_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[7]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_07_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_08_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[8]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_08_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_09_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[9]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_09_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_10_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[10]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_10_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_11_WERT | real | zylinderindividueller Korrekturoffset für die Injektorkennlinie (A2L-Name: tiofsinjad_w[11]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_11_EINH | string | "ms" |
| STAT_KMSTLASTINJAD_WERT | real | Kilometerstand der letzten vollständigen Injektoradaption. |
| STAT_STATINJADYSEQ_0_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_STATINJADYSEQ_1_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_STATINJADYSEQ_2_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_STATINJADYSEQ_3_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_STATINJADYSEQ_4_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_STATINJADYSEQ_5_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_STATINJADYSEQ_6_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_STATINJADYSEQ_7_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_STATINJADYSEQ_8_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_STATINJADYSEQ_9_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_STATINJADYSEQ_10_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_STATINJADYSEQ_11_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_0_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_1_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_2_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_3_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_4_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_5_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_6_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_7_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_8_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_9_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_10_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADAUSSXY_W_11_WERT | unsigned int | Zähler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_0_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_1_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_2_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_3_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_4_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_5_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_6_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_7_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_8_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_9_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_10_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADTIBOUNDXY_11_WERT | unsigned char | Zähler Verletzung zulässiger Ti-Bereich (bankweise / Ablaufsequenz) |
| STAT_ZRINJADCOMPL_WERT | unsigned char | Status Injektoradaption. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-atldiag"></a>
### STATUS_ATLDIAG

Turboladerstatus auslesen ATLDIAG (0x4044)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ATLDIAG_AKTIV | unsigned char | Ladedruckdiagnose aktiv |
| STAT_ATLDIAG_BANK1 | unsigned char | Ladedruckdiagnose fuer Bank 1 durchgelaufen |
| STAT_ATLDIAG_BANK2 | unsigned char | Ladedruckdiagnose fuer Bank 2 durchgelaufen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klannadap"></a>
### STATUS_KLANNADAP

KLANN Adaptionen auslesen KLANNADAP (0x4046)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_F_LRADAP1_WERT | real | Faktor aus Lambdaregelungsadaption fuer Bank 1 (A2L-Name: F_lradap1) |
| STAT_DLATRMO_WERT | real | Delta Sondenoffset Fuehrungsregelung (A2L-Name: dlatrmo_w) |
| STAT_FLRADAP1C_W_0_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_1_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_2_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_3_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_4_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_5_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_6_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_7_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_8_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_9_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_10_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_11_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_12_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_13_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_FLRADAP1C_W_14_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 |
| STAT_F_LRLZA1_WERT | real | Langzeitadaptions-Faktor aus KLANN Bank1 (NV-Ram) (A2L-Name: F_lrlza1) |
| STAT_FLRADAPSTXAB_W_0_WERT | real |  |
| STAT_FLRADAPSTXAB_W_1_WERT | real |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-integritaetdme"></a>
### STATUS_INTEGRITAETDME

Integritaet DME und Codierzaehler Leistungsklasse, Vmax und maximale V_VEH INTEGRITAETDME (0x4048)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERSIONSKENNUNG_WERT | unsigned char | Versionskennung |
| STAT_KENNUNGSWE1_1_WERT | unsigned long | Kennung SWE 1.1 |
| STAT_KENNUNGSWE1_2_WERT | unsigned long | Kennung SWE 1.2 |
| STAT_PRUEFERGEBNIS1_WERT | unsigned char | Pruefergebniss 1 |
| STAT_KENNUNGSWE2_1_WERT | unsigned long | Kennung SWE 2.1 |
| STAT_KENNUNGSWE2_2_WERT | unsigned long | Kennung SWE 2.2 |
| STAT_PRUEFERGEBNIS2_WERT | unsigned char | Pruefergebniss 2 |
| STAT_KENNUNGSWE3_1_WERT | unsigned long | Kennung SWE 3.1 |
| STAT_KENNUNGSWE3_2_WERT | unsigned long | Kennung SWE 3.2 |
| STAT_PRUEFERGEBNIS3_WERT | unsigned char | Pruefergebniss 3 |
| STAT_KENNUNGSWE4_1_WERT | unsigned long | Kennung SWE 4.1 |
| STAT_KENNUNGSWE4_2_WERT | unsigned long | Kennung SWE 4.2 |
| STAT_PRUEFERGEBNIS4_WERT | unsigned char | Pruefergebniss 4 |
| STAT_KENNUNGSWE5_1_WERT | unsigned long | Kennung SWE 5.1 |
| STAT_KENNUNGSWE5_2_WERT | unsigned long | Kennung SWE 5.2 |
| STAT_PRUEFERGEBNIS5_WERT | unsigned char | Pruefergebniss 5 |
| STAT_ANZAHLCODLK_WERT | unsigned char | Anzahl Codierungen Leistungsklasse |
| STAT_ANZAHLCODVMAX_WERT | unsigned char | Anzahl Codierungen Vmax (FF ist ein ungueltigkeitwert) |
| STAT_MAXIMALEVVEH_WERT | unsigned int | maximale V_VEH |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zdkshdp"></a>
### STATUS_ZDKSHDP

Zeitanteile der erreichten Druckbereiche (beim Tausch der Kraftstoffhochdruckpumpe) auslesen. ZDKSHDP (0x404C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_T_PRAIL_MON_XB_YPB_0_0_WERT | real | Raildruckmonitor: aufintegrierte Zeit des Raildrucks Prail_ist_xpb von Rail ix zwischen Schwellen iy. Umrechnung = 0,01 |
| STAT_T_PRAIL_MON_XB_YPB_0_0_EINH | string | "s" |
| STAT_T_PRAIL_MON_XB_YPB_1_0_WERT | real | Raildruckmonitor: aufintegrierte Zeit des Raildrucks Prail_ist_xpb von Rail ix zwischen Schwellen iy. Umrechnung = 0,01 |
| STAT_T_PRAIL_MON_XB_YPB_1_0_EINH | string | "s" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-readiness"></a>
### STATUS_READINESS

Monitorfunktionen und Readinessflags aus DME auslesen READINESS (0x4105)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_COMPREHENSIVE | unsigned char | Ueberwachung der uebrigen Komponenten Test abgeschlossen oder nicht anwendbar = 0 test nicht abgeschlossen = 1 |
| STAT_COMPREHENSIVE_TEXT | string | Ueberwachung der uebrigen Komponenten Test abgeschlossen oder nicht anwendbar = 0 test nicht abgeschlossen = 1 |
| STAT_FUELSYSTEM | unsigned char | Ueberwachung Kraftstoffsystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_FUELSYSTEM_TEXT | string | Ueberwachung Kraftstoffsystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_MISSFIRE | unsigned char | Ueberwachung Verbrennungsaussetzer Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_MISSFIRE_TEXT | string | Ueberwachung Verbrennungsaussetzer Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_COMPREHENSIVE_MONITOR | unsigned char | Ueberwachung der uebrigen Komponenten Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_COMPREHENSIVE_MONITOR_TEXT | string | Ueberwachung der uebrigen Komponenten Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_FUELSYSTEM_MONITOR | unsigned char | Ueberwachung Kraftstoffsystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_FUELSYSTEM_MONITOR_TEXT | string | Ueberwachung Kraftstoffsystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_MISSFIRE_MONITOR | unsigned char | Ueberwachung Verbrennungsaussetzer Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_MISSFIRE_MONITOR_TEXT | string | Ueberwachung Verbrennungsaussetzer Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_AGRRDY_EIN | unsigned char | Ueberwachung Abgasrueckfuehrung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_AGRRDY_EIN_TEXT | string | Ueberwachung Abgasrueckfuehrung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_HSRDY_EIN | unsigned char | Ueberwachung Lambdasondenheizung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_HSRDY_EIN_TEXT | string | Ueberwachung Lambdasondenheizung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_LSRDY_EIN | unsigned char | Ueberwachung Lambdasonde Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_LSRDY_EIN_TEXT | string | Ueberwachung Lambdasonde Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_KLIMARDY_EIN | unsigned char | Ueberwachung Klimaanlage Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_KLIMARDY_EIN_TEXT | string | Ueberwachung Klimaanlage Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_SLSRDY_EIN | unsigned char | Ueberwachung Sekundaerluftsystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_SLSRDY_EIN_TEXT | string | Ueberwachung Sekundaerluftsystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_TESRDY_EIN | unsigned char | Ueberwachung Tankentlueftungssystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_TESRDY_EIN_TEXT | string | Ueberwachung Tankentlueftungssystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_HKATRDY_EIN | unsigned char | Ueberwachung Katalysatorheizung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_HKATRDY_EIN_TEXT | string | Ueberwachung Katalysatorheizung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_KATRDY_EIN | unsigned char | Ueberwachung Katalysator Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_KATRDY_EIN_TEXT | string | Ueberwachung Katalysator Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_AGRMON_EIN | unsigned char | Ueberwachung Abgasrueckfuehrung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_AGRMON_EIN_TEXT | string | Ueberwachung Abgasrueckfuehrung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_HSMON_EIN | unsigned char | Ueberwachung Lambdasondenheizung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_HSMON_EIN_TEXT | string | Ueberwachung Lambdasondenheizung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_LSMON_EIN | unsigned char | Ueberwachung Lambdasonde Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_LSMON_EIN_TEXT | string | Ueberwachung Lambdasonde Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_KLIMAMON_EIN | unsigned char | Ueberwachung Klimaanlage Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_KLIMAMON_EIN_TEXT | string | Ueberwachung Klimaanlage Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_SLSMON_EIN | unsigned char | Ueberwachung Sekundaerluftsystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_SLSMON_EIN_TEXT | string | Ueberwachung Sekundaerluftsystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_TESMON_EIN | unsigned char | Ueberwachung Tankentlueftungssystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_TESMON_EIN_TEXT | string | Ueberwachung Tankentlueftungssystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_HKATMON_EIN | unsigned char | Ueberwachung Katalysatorheizung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_HKATMON_EIN_TEXT | string | Ueberwachung Katalysatorheizung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_KATMON_EIN | unsigned char | Ueberwachung Katalysator Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_KATMON_EIN_TEXT | string | Ueberwachung Katalysator Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wrueckdrehwinkel"></a>
### STATUS_WRUECKDREHWINKEL

VVT: Mehrfaches Rueckdrehen (Wiederholter Rueckdrehwinkel) lesen. WRUECKDREHWINKEL (0x5F75)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VVT_EXWINKSREV_WERT | unsigned int | Sollwert Zaehler Rueckdrehereignisse aufgrund von Lagereglerabweichung VVT-Steller |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-wrueckdrehwinkel"></a>
### STEUERN_WRUECKDREHWINKEL

VVT: Mehrfaches Rueckdrehen (Wiederholter Rueckdrehwinkel). Wenn B_favvtexwinksrev gesetzt ist, dann wird der Wert vom Tester (vvt_exwinksrev_count) auf den Zaehler (vvt_exwinksrev) kopiert. WRUECKDREHWINKEL (0x5F75)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_VVT_EXWINKSREV | unsigned int | Sollwert Zaehler Rueckdrehereignisse aufgrund von Lagereglerabweichung VVT-Steller |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvthighcurrent"></a>
### STEUERN_VVTHIGHCURRENT

Anzahl erkannter VVT Lageregelungsfehlerwarnungen irrreversible (VVT-Schwergaengigkeit) vorgeben. VVTHIGHCURRENT (0x5F7A)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_VVTHIGHCURRENT | unsigned int | Anzahl erkannter VVT Lageregelungsfehlerwarnungen irrreversible |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vvtschwergaengigkeit"></a>
### STATUS_VVTSCHWERGAENGIGKEIT

Anzahl erkannter VVT Lageregelungsfehler, Anzahl erkannter VVT Lageregelungsfehlerwarnungen irrreversible und Anzahl erkannter VVT Lageregelungsfehlerwarnungen reversible (VVT-Schwergaengigkeit) lesen. VVTSCHWERGAENGIGKEIT (0x5F7B)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VVTDEVIATION_WERT | unsigned int | Anzahl erkannter VVT Lageregelungsfehler |
| STAT_VVTHIGHCURRENT_WERT | unsigned int | Anzahl erkannter VVT Lageregelungsfehlerwarnungen irrreversible |
| STAT_VVT_HIGHCURRENT_REV_WERT | unsigned int | Anzahl erkannter VVT Lageregelungsfehlerwarnungen reversible. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvtdeviation"></a>
### STEUERN_VVTDEVIATION

Anzahl erkannter VVT Lageregelungsfehler vorgeben. VVTDEVIATION (0x5F7B)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_VVTDEVIATION | unsigned int | Anzahl erkannter VVT Lageregelungsfehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zdkshdpreset"></a>
### STEUERN_ZDKSHDPRESET

Zeitanteile der erreichten Druckbereiche (beim Tausch der Kraftstoffhochdruckpumpe) zuruecksetzen. Beim Aufruf dieses Services soll das Bit B_prail_mon_clr gesetzt werden. ZDKSHDPRESET (0x5F7F)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gvobd"></a>
### STATUS_GVOBD

Gemischvertrimmung fuer OBD-Demo und PVE auslesen. GVOBD (0x5F80)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SW_F_MK_KORR_EXT_XZYL_1_WERT | real | Faktor auf Einspritzung Zylinder 1 (Physikalische Reihenfolge) |
| STAT_SW_F_MK_KORR_EXT_XZYL_5_WERT | real | Faktor auf Einspritzung Zylinder 5 (Physikalische Reihenfolge) |
| STAT_SW_F_MK_KORR_EXT_XZYL_3_WERT | real | Faktor auf Einspritzung Zylinder 3 (Physikalische Reihenfolge) |
| STAT_SW_F_MK_KORR_EXT_XZYL_6_WERT | real | Faktor auf Einspritzung Zylinder 6 (Physikalische Reihenfolge) |
| STAT_SW_F_MK_KORR_EXT_XZYL_2_WERT | real | Faktor auf Einspritzung Zylinder 2 (Physikalische Reihenfolge) |
| STAT_SW_F_MK_KORR_EXT_XZYL_4_WERT | real | Faktor auf Einspritzung Zylinder 4 (Physikalische Reihenfolge) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-gvobd"></a>
### STEUERN_GVOBD

Gemischvertrimmung fuer OBD-Demo und PVE vorgeben. Der Korrekturfaktor soll bei Klemmenwechsel auf den Standardwert 1 zurueckgesetzt werden. STEUERN_GVOBD (0x5F80)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_F_MK_KORR_EXT_XZYL_1 | real | Faktor auf Einspritzung Zylinder 1 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_5 | real | Faktor auf Einspritzung Zylinder 5 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_3 | real | Faktor auf Einspritzung Zylinder 3 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_6 | real | Faktor auf Einspritzung Zylinder 6 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_2 | real | Faktor auf Einspritzung Zylinder 2 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_4 | real | Faktor auf Einspritzung Zylinder 4 (Physikalische Reihenfolge) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-gvobd"></a>
### STEUERN_PROGRAMM_GVOBD

Gemischvertrimmung fuer OBD-Demo und PVE programmieren. STEUERN_PROGRAMM_GVOBD (0x5F80)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_F_MK_KORR_EXT_XZYL_1 | real | Faktor auf Einspritzung Zylinder 1 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_5 | real | Faktor auf Einspritzung Zylinder 5 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_3 | real | Faktor auf Einspritzung Zylinder 3 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_6 | real | Faktor auf Einspritzung Zylinder 6 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_2 | real | Faktor auf Einspritzung Zylinder 2 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_4 | real | Faktor auf Einspritzung Zylinder 4 (Physikalische Reihenfolge) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hubkorr"></a>
### STATUS_HUBKORR

Hubkorrektur auslesen HUBKORR (0x5F8C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STVBRVSIN_WERT | unsigned char | Statuswort Verbrennungsregelung vom Tester nichtflüchtig. |
| STAT_STVBRVSNNV_WERT | unsigned char | Statuswort Verbrennungsregelung vom Tester. |
| STAT_STVBRVSO_WERT | unsigned int | Statuswort Verbrennungsregelung für Service. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hubkorr-programmieren"></a>
### STEUERN_HUBKORR_PROGRAMMIEREN

Hubkorrektur programmieren STEUERN_HUBKORR_PROGRAMMIEREN (0x5F8C)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_STVBRVSNNV | unsigned char | Codierdaten Hub Korrektur |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hubkorr-reset"></a>
### STEUERN_HUBKORR_RESET

Hubkorrektur loeschen STEUERN_HUBKORR_RESET (0x5F8C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hubkorr-verstellen"></a>
### STEUERN_HUBKORR_VERSTELLEN

Hubkorrektur vorgeben STEUERN_HUBKORR_VERSTELLEN (0x5F8C)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_STVBRVSIN | unsigned char | Codierdaten Hub Korrektur |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-imaalle"></a>
### STATUS_IMAALLE

Abgleichwerte Injektoren auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. IMAALLE (0x5F90)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_1_WERT | real | Abgleichwert Injektor 01 (Durchfluss) |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_1_EINH | string | "mg/Hub" |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_2_WERT | real | Abgleichwert Injektor 02 (Durchfluss) |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_2_EINH | string | "mg/Hub" |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_3_WERT | real | Abgleichwert Injektor 03 (Durchfluss) |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_3_EINH | string | "mg/Hub" |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_4_WERT | real | Abgleichwert Injektor 04 (Durchfluss) |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_4_EINH | string | "mg/Hub" |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_5_WERT | real | Abgleichwert Injektor 05 (Durchfluss) |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_5_EINH | string | "mg/Hub" |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_6_WERT | real | Abgleichwert Injektor 06 (Durchfluss) |
| STAT_SW_DURCHFLUSSABGLEICH_ZYL_6_EINH | string | "mg/Hub" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-imaalle"></a>
### STEUERN_IMAALLE

Abgleichwerte Injektoren programmieren IMAALLE (0x5F90)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_1 | real | Abgleichwert Injektor 01 (Durchfluss) |
| SW_DURCHFLUSSABGLEICH_ZYL_2 | real | Abgleichwert Injektor 02 (Durchfluss) |
| SW_DURCHFLUSSABGLEICH_ZYL_3 | real | Abgleichwert Injektor 03 (Durchfluss) |
| SW_DURCHFLUSSABGLEICH_ZYL_4 | real | Abgleichwert Injektor 04 (Durchfluss) |
| SW_DURCHFLUSSABGLEICH_ZYL_5 | real | Abgleichwert Injektor 05 (Durchfluss) |
| SW_DURCHFLUSSABGLEICH_ZYL_6 | real | Abgleichwert Injektor 06 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-1"></a>
### STEUERN_IMA_ZYL_1

Abgleichwert Injektor 01 (phys) programmieren IMA_ZYL_1 (0x5F91)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_1 | real | Abgleichwert Injektor 01 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-2"></a>
### STEUERN_IMA_ZYL_2

Abgleichwert Injektor 02 (phys) programmieren IMA_ZYL_2 (0x5F92)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_2 | real | Abgleichwert Injektor 02 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-3"></a>
### STEUERN_IMA_ZYL_3

Abgleichwert Injektor 03 (phys) programmieren IMA_ZYL_3 (0x5F93)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_3 | real | Abgleichwert Injektor 03 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-4"></a>
### STEUERN_IMA_ZYL_4

Abgleichwert Injektor 04 (phys) programmieren IMA_ZYL_4 (0x5F94)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_4 | real | Abgleichwert Injektor 04 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-5"></a>
### STEUERN_IMA_ZYL_5

Abgleichwert Injektor 05 (phys) programmieren IMA_ZYL_5 (0x5F95)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_5 | real | Abgleichwert Injektor 05 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-6"></a>
### STEUERN_IMA_ZYL_6

Abgleichwert Injektor 06 (phys) programmieren IMA_ZYL_6 (0x5F96)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_6 | real | Abgleichwert Injektor 06 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kva"></a>
### STEUERN_KVA

KraftstoffVerbrauchsAnzeige - Korrekturfaktor schreiben KVA (0x5FC1)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KVA | real | KraftstoffVerbrauchsAnzeige - Korrekturfaktor |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ll-abgleich"></a>
### STATUS_LL_ABGLEICH

Abgleichwert LL (Leerlauf) auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. LL_ABGLEICH (0x5FF0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_ABLL1_WERT | long | Drehzahlanhebung im Leerlauf |
| STAT_PHY_ABLL1_EINH | string | "1/min" |
| STAT_PHY_ABLL2_WERT | long | Drehzahlanhebung im Leerlauf mit Klimaanlage ein |
| STAT_PHY_ABLL2_EINH | string | "1/min" |
| STAT_PHY_ABLL3_WERT | long | Drehzahlanhebung im Leerlauf mit Fahrstufe |
| STAT_PHY_ABLL3_EINH | string | "1/min" |
| STAT_PHY_ABLL4_WERT | long | Drehzahlanhebung im Leerlauf mit Fahrstufe und Klimaanlage ein |
| STAT_PHY_ABLL4_EINH | string | "1/min" |
| STAT_PHY_ABLL5_WERT | long | Drehzahlanhebung im Leerlauf zum Batterie laden |
| STAT_PHY_ABLL5_EINH | string | "1/min" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-abll"></a>
### STEUERN_ENDE_ABLL

Abgleichwert LL (Leerlauf) Vorgeben beenden ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. STEUERN_ENDE_ABLL (0x5FF0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-llabg-prog"></a>
### STEUERN_LLABG_PROG

Abgleichwert LL (Leerlauf) programmieren ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. STEUERN_LLABG_PROG (0x5FF0)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ABLL1 | long | Drehzahlanhebung im Leerlauf |
| SW_ABLL2 | long | Drehzahlanhebung im Leerlauf mit Klimaanlage ein |
| SW_ABLL3 | long | Drehzahlanhebung im Leerlauf mit Fahrstufe |
| SW_ABLL4 | long | Drehzahlanhebung im Leerlauf mit Fahrstufe und Klimaanlage ein |
| SW_ABLL5 | long | Drehzahlanhebung im Leerlauf zum Batterie laden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ll-abgleich"></a>
### STEUERN_LL_ABGLEICH

Abgleichwert LL (Leerlauf) vorgeben ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. STEUERN_LL_ABGLEICH (0x5FF0)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ABLL1 | long | Drehzahlanhebung im Leerlauf |
| SW_ABLL2 | long | Drehzahlanhebung im Leerlauf mit Klimaanlage ein |
| SW_ABLL3 | long | Drehzahlanhebung im Leerlauf mit Fahrstufe |
| SW_ABLL4 | long | Drehzahlanhebung im Leerlauf mit Fahrstufe und Klimaanlage ein |
| SW_ABLL5 | long | Drehzahlanhebung im Leerlauf zum Batterie laden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecu-config"></a>
### ECU_CONFIG

Variante auslesen ECU_CONFIG (0x5FF2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DISA_WERT | unsigned char | DISA geschaltet vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_DISA_LM_WERT | unsigned char | DISA geregelt mit Lagerueckmeldung. 0=nicht vorhanden / 1=vorhanden |
| STAT_ANSK_WERT | unsigned char | Ansaugluftklappe vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_TURBO_WERT | unsigned char | Turbo mit Wastegate vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_TURBO_VTG_WERT | unsigned char | Turbo mit variabler Turbinengeometrie vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGR_WERT | unsigned char | Abgasrueckfuehrung vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGK_MONO_WERT | unsigned char | Abgaskonzept Mono vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGK_Y_WERT | unsigned char | Abgaskonzept Y vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGK_STEREO_WERT | unsigned char | Abgaskonzept Stereo vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGK_KAT_WERT | unsigned char | Abgaskonzept ohne KAT vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_LLSVK_WERT | unsigned char | Lineare Lambdasonden vor KAT vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_BLSVK_WERT | unsigned char | Binaere Lambdasonden vor KAT vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_SLP_WERT | unsigned char | Sekundaerluftpumpe vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_SLV_WERT | unsigned char | Sekundaerluftventil vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGK_WERT | unsigned char | Abgasklappe vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_SOK_WERT | unsigned char | Soundklappe vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_KLJ_WERT | unsigned char | Kuehler Jalousie vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_ELUE_400_WERT | unsigned char | E-Luefter 400W vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_ELUE_600_WERT | unsigned char | E-Luefter 600W vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_EBL_WERT | unsigned char | E-Box-Luefter. 0=nicht vorhanden / 1=vorhanden |
| STAT_MFL_WERT | unsigned char | Multifunktionslenkrad. 0=nicht vorhanden / 1=vorhanden |
| STAT_SPT_WERT | unsigned char | Sport-Taster. 0=nicht vorhanden / 1=vorhanden |
| STAT_TOZNIV_WERT | unsigned char | Thermischer Oelniveausensor vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AKKS_BN2000_WERT | unsigned char | Aktive Kuehlluftklappe (oben). 0=nicht vorhanden / 1=vorhanden |
| STAT_PKKS_BN2000_WERT | unsigned char | Passive Kuehlluftklappe (unten). 0=nicht vorhanden / 1=vorhanden |
| STAT_HS_WERT | unsigned char | Handschalter vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_EGS_WERT | unsigned char | EGS vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_DKG_WERT | unsigned char | DKG vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_ASC_WERT | unsigned char | Automatic Stability Control vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_ARS_WERT | unsigned char | Anti Roll Stabilisierung vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AFS_WERT | unsigned char | Active Front Steering vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_RKK_WERT | unsigned char | Relais Klimakompressor vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_MSA_WERT | unsigned char | Start-Stop-Automatik. 0=nicht vorhanden / 1=vorhanden |
| STAT_AOEL_WERT | unsigned char | Oelabscheiderheizung vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_EMF_WERT | unsigned char | Elektromechanische Feststellbremse vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_SAT_WERT | unsigned char | Sportautomat. 0=nicht vorhanden / 1=vorhanden |
| STAT_ELUE_850_WERT | unsigned char | E-Luefter 850W vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_IBS_WERT | unsigned char | Vorhalt (bisher: intelligenter Batteriesensor an BSD vorhanden) 0=nicht vorhanden / 1=vorhanden |
| STAT_ELUE_1000_WERT | unsigned char | E-Luefter 1000W vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_KLIMA_WERT | unsigned char | Klimaanlage verbaut. 0=nicht vorhanden / 1=vorhanden |
| STAT_BN2000_WERT | unsigned char | Bordnetz 2000. 0=nicht vorhanden / 1=vorhanden |
| STAT_TEMP_CAN_WERT | unsigned char | Tempomat ueber CAN. 0=nicht vorhanden / 1=vorhanden |
| STAT_KOMBI_WERT | unsigned char | Kombi ueber CAN. 0=nicht vorhanden / 1=vorhanden |
| STAT_LDM_WERT | unsigned char | Laengsdynamik-Management. 0=nicht vorhanden / 1=vorhanden |
| STAT_LMM_WERT | unsigned char | Luftmassenmesser. 0=nicht vorhanden / 1=vorhanden |
| STAT_PST_AFS_WERT | unsigned char | Powersteering: AFS1-Botschaft Variante. 0=nicht vorhanden / 1=vorhanden |
| STAT_PST_STE_WERT | unsigned char | Powersteering: STE1-Botschaft Variante. 0=nicht vorhanden / 1=vorhanden |
| STAT_FSTCAN_WERT | unsigned char | Fuellstandsinformation ueber CAN. 0=nicht vorhanden / 1=vorhanden |
| STAT_ICM_WERT | unsigned char | Bedingung ICM verbaut. 0=nicht vorhanden / 1=vorhanden |
| STAT_IBS_BSD_WERT | unsigned char | Batteriesensor am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_ZWP_BSD_WERT | unsigned char | El. Zusatzwasserpumpe fuer Elektronik am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_EWAP_BSD_WERT | unsigned char | El. Wasserpumpe am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_OZS_BSD_WERT | unsigned char | Oelzustandssensor am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_GEN_2_BSD_WERT | unsigned char | Generator 2 am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_GEN_1_BSD_WERT | unsigned char | Generator 1 am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_AFS_BN2020_WERT | unsigned char | Elektrische Lenkung L6 erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_IBS_LIN_WERT | unsigned char | Batteriesensor an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_AKKS_LIN_WERT | unsigned char | Aktive Kuehlklappensteuerung an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_BCU_LIN_WERT | unsigned char | Broadcastunit an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_SGR_LIN_WERT | unsigned char | Startergenerator an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_OELSENS_WERT | unsigned char | Variante Oelsensor. 0=nicht vorhanden / 1=vorhanden |
| STAT_WAP_LIN_WERT | unsigned char | Wasserpumpe an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_GEN_LIN_WERT | unsigned char | Generator an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_ZWAP_LIN_WERT | unsigned char | Zusatzwasserpumpe an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_KSNDS_WERT | unsigned char | Kraftstoff-Niederdrucksensor. 0=nicht vorhanden / 1=vorhanden |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecu-config-reset"></a>
### ECU_CONFIG_RESET

Variante loeschen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. ECU_CONFIG_RESET (0x5FF2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-glf2"></a>
### STEUERN_ENDE_GLF2

Gesteuerte Luftfuehrung Klappe 2 Ansteuerung beenden GLF2 (0xA400)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-glf2"></a>
### STEUERN_GLF2

Gesteuerte Luftfuehrung Klappe 2 ansteuern GLF2 (0xA407)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_GLF2 | unsigned char | Komponentenansteuerung: Gesteuerte Luftfuehrung Klappe 2 1 = Ansteuern 0 = Aussteuern (default) |
| SW_TO_GLF2 | unsigned long | Timeout Gesteuerte Luftfuehrung Klappe 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-odr"></a>
### STEUERN_ENDE_ODR

Oel Druck Regelung (Geregeltes Oeldrucksystem) Ansteuerung beenden ODR (0xAB00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-odr"></a>
### STEUERN_ODR

Oel Druck Regelung (Geregeltes Oeldrucksystem) ansteuern ODR (0xAB07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_P_OELSOL_TST | unsigned long | Oeldruck Sollwert durch Testereingriff |
| SW_TO_ODR | unsigned long | Timeout Oel Druck Regelung (Geregeltes Oeldrucksystem) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-odv"></a>
### STEUERN_ENDE_ODV

Oeldruckventil (Geregeltes Oeldrucksystem) Ansteuerung beenden ODV (0xAC00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-odv"></a>
### STEUERN_ODV

Oeldruckventil (Geregeltes Oeldrucksystem) ansteuern ODV (0xAC07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ODV | real | Tastverhaeltniss Oeldruckventil (Geregeltes Oeldrucksystem) |
| SW_TO_ODV | unsigned long | Timeout Oeldruckventil (Geregeltes Oeldrucksystem) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-mls"></a>
### STEUERN_ENDE_MLS

Motorlagersteuerung Ansteuerung beenden MLS (0xB200)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mls"></a>
### STEUERN_MLS

Motorlagersteuerung ansteuern MLS (0xB207)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MLS | unsigned char | Komponentenansteuerung: Motorlagersteuerung 1 = Ansteuern 0 = Aussteuern (default) |
| SW_TO_MLS | unsigned long | Timeout Motorlagersteuerung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ulv"></a>
### STEUERN_ENDE_ULV

Umluftventil Ansteuerung beenden ULV (0xB500)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ulv"></a>
### STEUERN_ULV

Umluftventil ansteuern ULV (0xB507)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ULV | real | Tastverhaeltniss Umluftventil |
| SW_TO_ULV | unsigned long | Timeout Umluftventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lds1"></a>
### STEUERN_ENDE_LDS1

Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) Ansteuerung beenden LDS1 (0xB600)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lds1"></a>
### STEUERN_LDS1

Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) ansteuern LDS1 (0xB607)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LDS1 | real | Tastverhaeltniss Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) |
| SW_TO_LDS1 | unsigned long | Timeout Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-msv"></a>
### STEUERN_ENDE_MSV

Mengensteuerventil Ansteuerung beenden MSV (0xBD00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-msv"></a>
### STEUERN_MSV

Mengensteuerventil ansteuern MSV (0xBD07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MSV | real | Tastverhaeltniss Mengensteuerventil |
| SW_TO_MSV | unsigned long | Timeout Mengensteuerventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ewap"></a>
### STEUERN_ENDE_EWAP

elektr. Wasserpumpe Ansteuerung beenden EWAP (0xBF00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ewap"></a>
### STEUERN_EWAP

elektr. Wasserpumpe (Bit Serielle Datenschnittstelle) ansteuern EWAP (0xBF07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EWAP | unsigned char | Sollwert elektr. Wasserpumpe (0 bis 255 Upm) |
| SW_TO_EWAP | unsigned long | Timeout elektr. Wasserpumpe |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-agk"></a>
### STEUERN_ENDE_AGK

Abgasklappe Ansteuerung beenden AGK (0xC100)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agk"></a>
### STEUERN_AGK

Abgasklappe ansteuern AGK (0xC107)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_AGK | unsigned char | Komponentenansteuerung: Abgasklappe 1 = Ansteuern 0 = Aussteuern (default) |
| SW_TO_AGK | unsigned long | Timeout 0 bis 508s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-glf"></a>
### STEUERN_ENDE_GLF

Gesteuerte Luftfuehrung (Klappe 1) Ansteuerung beenden GLF (0xC300)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-glf"></a>
### STEUERN_GLF

Gesteuerte Luftfuehrung (Klappe 1) ansteuern GLF (0xC307)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_GLF | unsigned char | Komponentenansteuerung: Gesteuerte Luftfuehrung 1 = Ansteuern 0 = Aussteuern (default) |
| SW_TO_GLF | unsigned long | Timeout Gesteuerte Luftfuehrung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-kft"></a>
### STEUERN_ENDE_KFT

Kennfeldthermostat Ansteuerung beenden KFT (0xC900)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kft"></a>
### STEUERN_KFT

Kennfeldthermostat ansteuern KFT (0xC907)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_KFT | unsigned char | Komponentenansteuerung: Kennfeldthermostat 1 = Ansteuern 0 = Aussteuern (default) |
| SW_TO_KFT | unsigned long | Timeout Kennfeldthermostat |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-p"></a>
### STEUERN_ENDE_DMTL_P

Diagnosemodul-Tank Leckage Pumpe Ansteuerung beenden DMTL_P (0xCC00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-p"></a>
### STEUERN_DMTL_P

Diagnosemodul-Tank Leckage Pumpe ansteuern DMTL_P (0xCC07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTL_P | unsigned char | Komponentenansteuerung: Diagnosemodul-Tank Leckage Pumpe 1 = Ansteuern 0 = Aussteuern (default) |
| SW_TO_DMTL_P | unsigned long | Timeout Diagnosemodul-Tank Leckage Pumpe |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-v"></a>
### STEUERN_ENDE_DMTL_V

Diagnosemodul-Tank Leckage Ventil Ansteuerung beenden DMTL_V (0xCD00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-v"></a>
### STEUERN_DMTL_V

Diagnosemodul-Tank Leckage Ventil ansteuern DMTL_V (0xCD07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTL_V | unsigned char | Komponentenansteuerung: Diagnosemodul-Tank Leckage Ventil 1 = Ansteuern 0 = Aussteuern (default) |
| SW_TO_DMTL_V | unsigned long | Timeout Diagnosemodul-Tank Leckage Ventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-heizung"></a>
### STEUERN_ENDE_DMTL_HEIZUNG

Diagnosemodul-Tank Leckage Heizung Ansteuerung beenden DMTL_HEIZUNG (0xCE00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-heizung"></a>
### STEUERN_DMTL_HEIZUNG

Diagnosemodul-Tank Leckage Heizung ansteuern DMTL_HEIZUNG (0xCE07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTLH | unsigned char | Komponentenansteuerung: Diagnosemodul-Tank Leckage Heizung 1 = Ansteuern 0 = Aussteuern (default) |
| SW_TO_DMTLH | unsigned long | Timeout Diagnosemodul-Tank Leckage Heizung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-tev"></a>
### STEUERN_ENDE_TEV

Tankentlueftungsventil Ansteuerung beenden TEV (0xCF00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

Tankentlueftungsventil ansteuern TEV (0xCF07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_TEV | real | Tastverhaeltniss Tankentlueftungsventil |
| SW_TO_TEV | unsigned long | Timeout Tankentlueftungsventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh1"></a>
### STEUERN_ENDE_LSH1

Lambdasondenheizung vor Kat Bank1 Ansteuerung beenden LSH1 (0xD000)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh1"></a>
### STEUERN_LSH1

Lambdasondenheizung vor Kat Bank1 ansteuern LSH1 (0xD007)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH1 | real | Tastverhaeltniss Lambdasondenheizung vor Kat Bank1 |
| SW_TO_LSH1 | unsigned long | Timeout Lambdasondenheizung vor Kat Bank1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh2"></a>
### STEUERN_ENDE_LSH2

Lambdasondenheizung hinter Kat Bank1 Ansteuerung beenden LSH2 (0xD100)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh2"></a>
### STEUERN_LSH2

Lambdasondenheizung hinter Kat Bank1 ansteuern LSH2 (0xD107)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH2 | real | Tastverhaeltniss Lambdasondenheizung hinter Kat Bank1 |
| SW_TO_LSH2 | unsigned long | Timeout Lambdasondenheizung hinter Kat Bank1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-mil"></a>
### STEUERN_ENDE_MIL

MIL (Malfunction Indicator Lamp) Ansteuerung beenden MIL (0xD400)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mil"></a>
### STEUERN_MIL

MIL (Malfunction Indicator Lamp) ansteuern MIL (0xD407)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MIL | unsigned long | Tastverhaeltniss MIL (Malfunction Indicator Lamp) |
| SW_TO_MIL | unsigned long | Timeout MIL (Malfunction Indicator Lamp) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-eml"></a>
### STEUERN_ENDE_EML

EML (Engine Malfunction Lamp) Ansteuerung beenden EML (0xD600)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eml"></a>
### STEUERN_EML

EML (Engine Malfunction Lamp) ansteuern EML (0xD607)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EML | unsigned long | Tastverhaeltniss EML (Engine Malfunction Lamp) |
| SW_TO_EML | unsigned long | Timeout EML (Engine Malfunction Lamp) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ekp"></a>
### STEUERN_ENDE_EKP

Elektrische Kraftstoffpumpe 1 Ansteuerung beenden Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben EKP (0xD800)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

Elektrische Kraftstoffpumpe 1 ansteuern Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben EKP (0xD807)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EKP1 | unsigned char | Komponentenansteuerung: Elektrische Kraftstoffpumpe 1 1 = Ansteuern 0 = Aussteuern (default) |
| SW_TO_EKP1 | unsigned long | Timeout Elektrische Kraftstoffpumpe 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-e-luefter"></a>
### STEUERN_ENDE_E_LUEFTER

E-Luefter Ansteuerung beenden E_LUEFTER (0xDA00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

E-Luefter ansteuern E_LUEFTER (0xDA07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ELUE | real | Tastverhaeltniss E-Luefter |
| SW_TO_ELUE | unsigned long | Timeout E-Luefter |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-vvt"></a>
### STEUERN_ENDE_VVT

VVT Ansteuerung beenden VVT (0xDD00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt"></a>
### STEUERN_VVT

VVT ansteuern VVT (0xDD07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PHY_VVT | real | Stellbereich VVT |
| SW_TO_VVT | unsigned long | Timeout VVT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev1"></a>
### STEUERN_ENDE_EV1

Einspritzventil 1 (physikalisch) Ansteuerung beenden EV1 (0xE100)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev1"></a>
### STEUERN_EV1

Einspritzventil 1 (physikalisch) ansteuern EV1 (0xE107)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV1 | unsigned long | Periodendauer Einspritzventil 1 |
| SW_TV_EV1 | real | Tastverhaeltniss Einspritzventil 1 |
| SW_TO_EV1 | unsigned long | Timeout Einspritzventil 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev2"></a>
### STEUERN_ENDE_EV2

Einspritzventil 2 (physikalisch) Ansteuerung beenden EV2 (0xE200)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev2"></a>
### STEUERN_EV2

Einspritzventil 2 (physikalisch) ansteuern EV2 (0xE207)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV2 | unsigned long | Periodendauer Einspritzventil 2 |
| SW_TV_EV2 | real | Tastverhaeltniss Einspritzventil 2 |
| SW_TO_EV2 | unsigned long | Timeout Einspritzventil 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev3"></a>
### STEUERN_ENDE_EV3

Einspritzventil 3 (physikalisch) Ansteuerung beenden EV3 (0xE300)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev3"></a>
### STEUERN_EV3

Einspritzventil 3 (physikalisch) ansteuern EV3 (0xE307)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV3 | unsigned long | Periodendauer Einspritzventil 3 |
| SW_TV_EV3 | real | Tastverhaeltniss Einspritzventil 3 |
| SW_TO_EV3 | unsigned long | Timeout Einspritzventil 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev4"></a>
### STEUERN_ENDE_EV4

Einspritzventil 4 (physikalisch) Ansteuerung beenden EV4 (0xE400)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev4"></a>
### STEUERN_EV4

Einspritzventil 4 (physikalisch) ansteuern EV4 (0xE407)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV4 | unsigned long | Periodendauer Einspritzventil 4 |
| SW_TV_EV4 | real | Tastverhaeltniss Einspritzventil 4 |
| SW_TO_EV4 | unsigned long | Timeout Einspritzventil 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev5"></a>
### STEUERN_ENDE_EV5

Einspritzventil 5 (physikalisch) Ansteuerung beenden EV5 (0xE500)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev5"></a>
### STEUERN_EV5

Einspritzventil 5 (physikalisch) ansteuern EV5 (0xE507)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV5 | unsigned long | Periodendauer Einspritzventil 5 |
| SW_TV_EV5 | real | Tastverhaeltniss Einspritzventil 5 |
| SW_TO_EV5 | unsigned long | Timeout Einspritzventil 5 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev6"></a>
### STEUERN_ENDE_EV6

Einspritzventil 6 Ansteuerung (physikalisch) beenden EV6 (0xE600)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev6"></a>
### STEUERN_EV6

Einspritzventil 6 (physikalisch) ansteuern EV6 (0xE607)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV6 | unsigned long | Periodendauer Einspritzventil 6 |
| SW_TV_EV6 | real | Tastverhaeltniss Einspritzventil 6 |
| SW_TO_EV6 | unsigned long | Timeout Einspritzventil 6 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-enws"></a>
### STEUERN_ENDE_ENWS

Vanos Einlass Ventil Ansteuerung beenden ENWS (0xED00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-enws"></a>
### STEUERN_ENWS

Vanos Einlass Ventil ansteuern ENWS (0xED07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ENWS | real | Tastverhältnis Vanos_E Ventil |
| SW_TO_ENWS | unsigned long | Timeout Vanos_E Ventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-anws"></a>
### STEUERN_ENDE_ANWS

Vanos Auslass Ventil Ansteuerung beenden ANWS (0xEE00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-anws"></a>
### STEUERN_ANWS

Vanos Auslass Ventil ansteuern ANWS (0xEE07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ANWS | real | Tastverhältnis Vanos_A Ventil |
| SW_TO_ANWS | unsigned long | Timeout Vanos_A Ventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-teav"></a>
### STEUERN_ENDE_TEAV

Absperrventil Tankentlueftung (Steuern-Ende) TEAV (0xFC00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-teav"></a>
### STEUERN_TEAV

Absperrventil Tankentlueftung Ansteuerung TEAV (0xFC07)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_TEAV | unsigned char | Komponentenansteuerung: Absperrventil Tankentlueftung 1 = Ansteuern 0 = Aussteuern (default) |
| SW_TO_TEAV | unsigned long | Timeout Absperrventil Tankentlueftung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ruhestrommessung"></a>
### STATUS_RUHESTROMMESSUNG

Auslesen Ruhestrompruefung mit IBS RUHESTROMMESSUNG (0x2B)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_RUHESTROM_WERT | unsigned char | Funktionsstatus RUHESTROM |
| STAT_FS_RUHESTROM_TEXT | string | Funktionsstatus RUHESTROM |
| STAT_STAT_RUHESTROM_WERT | real | Ruhestrom |
| STAT_STAT_RUHESTROM_EINH | string | "A" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ruhestrommessung"></a>
### STEUERN_RUHESTROMMESSUNG

Ansteuern Ruhestrompruefung mit IBS RUHESTROMMESSUNG (0x2B) Aktivierung: Klemme 15 = EIN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_MAX_WERT | real | Max. Ruhestromschwelle (Eco_max_i) Einheit: A Min: 0 Max: 0.3178 default: 0.08 |
| MSB_WERT | real | Ecos Messtartbedingung (Eco_msb) Einheit: s Min: 0 Max: 12.75 default: 0.05 |
| MZ_WERT | real | Dauer Mittelwertmessung (Eco_mz) Einheit: s Min: 0 Max: 12.75 default: 0.05 |
| TO_WERT | unsigned char | Ecos Messung Timeout (Eco_timo) Einheit: s Min: 0 Max: 255 default: 30 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-llerh"></a>
### START_SYSTEMCHECK_LLERH

Ansteuern Diagnosefunktion Leerlauf-Erhoehung SYSTEMCHECK_LLERH (0x26)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL | unsigned long | Drehzahlaenderung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-llerh"></a>
### STOP_SYSTEMCHECK_LLERH

Diagnosefunktion Leerlauf-Erhoehung beenden SYSTEMCHECK_LLERH (0x26)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-llerh"></a>
### STATUS_SYSTEMCHECK_LLERH

Auslesen Diagnosefunktion Leerlauf-Erhoehung SYSTEMCHECK_LLERH (0x26)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE | unsigned char | Funktionsstatus Diagnosefunktion LL-Erhoehung |
| STAT_DIAGNOSE_TEXT | string | Funktionsstatus Diagnosefunktion LL-Erhoehung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-ibs"></a>
### IDENT_IBS

$22 40 21 BMW Nr, Seriennummer, SW/HW Index

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ID_BMW_NR | string | BMW-Teilenummer 7 stellig |
| SERIENNUMMER | unsigned long | BMW-Seriennummer |
| ZIF_PROGRAMMSTAND | int | Programm referenz |
| ZIF_STATUS | int | Programm Revision |
| HW_REF | int | Hardware Referenz |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (137 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (210 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [MESSWERTEMODE](#table-messwertemode) (14 × 3)
- [CBSKENNUNG](#table-cbskennung) (20 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (761 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (750 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (444 × 9)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (761 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (750 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (444 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (15 × 2)
- [MESSWERTETAB](#table-messwertetab) (429 × 12)
- [RESET_GRPID](#table-reset-grpid) (33 × 2)
- [RESET_ID](#table-reset-id) (145 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [BA_VCV_STATE_TEXT](#table-ba-vcv-state-text) (8 × 2)
- [_MSD80N43_CNV_S_2_DEF_BIT_UB_741_CM](#table-msd80n43-cnv-s-2-def-bit-ub-741-cm) (2 × 2)
- [STAT_RUHESTROM](#table-stat-ruhestrom) (17 × 2)
- [TINDIVIDUALDATALISTE](#table-tindividualdataliste) (1 × 17)
- [STATCLIENTAUTHTXT](#table-statclientauthtxt) (4 × 2)
- [STATFREESKTXT](#table-statfreesktxt) (3 × 2)
- [STATEWSVERTXT](#table-statewsvertxt) (3 × 2)
- [SWTFEHLER_TAB](#table-swtfehler-tab) (51 × 2)
- [_AUSLESEMODE](#table-auslesemode) (5 × 2)
- [_EISYUGD_INPA](#table-eisyugd-inpa) (9 × 6)
- [_EISYUGD_FASTA](#table-eisyugd-fasta) (6 × 6)
- [_EISYGD_INPA](#table-eisygd-inpa) (6 × 5)
- [_KRANN_INPA](#table-krann-inpa) (145 × 4)
- [_KLANN_INPA](#table-klann-inpa) (228 × 4)
- [_EISYGD_FASTA](#table-eisygd-fasta) (5 × 5)
- [_KRANN_FASTA](#table-krann-fasta) (7 × 4)
- [_KLANN_FASTA](#table-klann-fasta) (12 × 4)
- [T_BA_IST_NN](#table-t-ba-ist-nn) (5 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (13 × 3)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT4_DOP](#table-t-1bit-switch-position-high-byte-bit4-dop) (2 × 2)
- [T_1BIT_FS_ERW_LR_AUS_BIT3_DOP](#table-t-1bit-fs-erw-lr-aus-bit3-dop) (2 × 2)
- [T_ST_ATLSVC_PVDK_DOP](#table-t-st-atlsvc-pvdk-dop) (6 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT2_DOP](#table-t-1bit-state-ready-obd-2-bit2-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT2_DOP](#table-t-1bit-switch-position-low-byte-bit2-dop) (2 × 2)
- [T_1BIT_FS_ERW_LR_AUS_BIT4_DOP](#table-t-1bit-fs-erw-lr-aus-bit4-dop) (2 × 2)
- [T_1BIT_GLF_HIGH_BYTE_BIT0_DOP](#table-t-1bit-glf-high-byte-bit0-dop) (2 × 2)
- [T_1BIT_GLF_LOW_BYTE_BIT2_DOP](#table-t-1bit-glf-low-byte-bit2-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT6_DOP](#table-t-1bit-state-ready-obd-1-bit6-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_BIT2_DOP](#table-t-1bit-switch-position-bit2-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT0_DOP](#table-t-1bit-state-ready-obd-1-bit0-dop) (2 × 2)
- [T_1BIT_GLF_LOW_BYTE_BIT7_DOP](#table-t-1bit-glf-low-byte-bit7-dop) (2 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT2_DOP](#table-t-1bit-c-state-ready-obd-2-bit2-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT4_DOP](#table-t-1bit-fs-erw-vvtl-bit4-dop) (2 × 2)
- [T_1BIT_FS_ERW_LR_AUS_BIT2_DOP](#table-t-1bit-fs-erw-lr-aus-bit2-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT4_DOP](#table-t-1bit-state-ready-obd-1-bit4-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT5_DOP](#table-t-1bit-fs-erw-vvtl-bit5-dop) (2 × 2)
- [T_1BIT_GLF_HIGH_BYTE_BIT4_DOP](#table-t-1bit-glf-high-byte-bit4-dop) (2 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT6_DOP](#table-t-1bit-c-state-ready-obd-2-bit6-dop) (2 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT4_DOP](#table-t-1bit-c-state-ready-obd-2-bit4-dop) (2 × 2)
- [T_STATE_DMTL_DOP](#table-t-state-dmtl-dop) (21 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT7_DOP](#table-t-1bit-state-ready-obd-2-bit7-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_BIT0_DOP](#table-t-1bit-switch-position-bit0-dop) (2 × 2)
- [T_ST_ATLSVC_DOP](#table-t-st-atlsvc-dop) (9 × 2)
- [T_1BIT_SWITCH_POSITION_BIT3_DOP](#table-t-1bit-switch-position-bit3-dop) (2 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT7_DOP](#table-t-1bit-c-state-ready-obd-2-bit7-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT6_DOP](#table-t-1bit-switch-position-high-byte-bit6-dop) (2 × 2)
- [T_B_VVTNOTL_DOP](#table-t-b-vvtnotl-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT7_DOP](#table-t-1bit-switch-position-high-byte-bit7-dop) (2 × 2)
- [T_B_MSRDKAD_DOP](#table-t-b-msrdkad-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT0_DOP](#table-t-1bit-switch-position-high-byte-bit0-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT7_DOP](#table-t-1bit-switch-position-low-byte-bit7-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT7_DOP](#table-t-1bit-fs-erw-vvtl-bit7-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT4_DOP](#table-t-1bit-state-ready-obd-2-bit4-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT3_DOP](#table-t-1bit-fs-erw-vvtl-bit3-dop) (2 × 2)
- [T_1BIT_GLF_LOW_BYTE_BIT5_DOP](#table-t-1bit-glf-low-byte-bit5-dop) (2 × 2)
- [T_1BIT_GLF_LOW_BYTE_BIT4_DOP](#table-t-1bit-glf-low-byte-bit4-dop) (2 × 2)
- [T_B_KUPPL_DOP](#table-t-b-kuppl-dop) (2 × 2)
- [T_EOL_RAM_1__DOP](#table-t-eol-ram-1-dop) (10 × 2)
- [T_1BIT_SWITCH_POSITION_BIT4_DOP](#table-t-1bit-switch-position-bit4-dop) (2 × 2)
- [T_1BIT_GLF_LOW_BYTE_BIT0_DOP](#table-t-1bit-glf-low-byte-bit0-dop) (2 × 2)
- [T_ST_TESTPOELSYS2_DOP](#table-t-st-testpoelsys2-dop) (11 × 2)
- [T_1BIT_GLF_HIGH_BYTE_BIT6_DOP](#table-t-1bit-glf-high-byte-bit6-dop) (2 × 2)
- [T_VVTCHKSF1_FS_DOP](#table-t-vvtchksf1-fs-dop) (10 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT3_DOP](#table-t-1bit-state-ready-obd-2-bit3-dop) (2 × 2)
- [T_1BIT_GLF_HIGH_BYTE_BIT5_DOP](#table-t-1bit-glf-high-byte-bit5-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT6_DOP](#table-t-1bit-fs-erw-vvtl-bit6-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT1_DOP](#table-t-1bit-fs-erw-vvtl-bit1-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT1_DOP](#table-t-1bit-state-ready-obd-2-bit1-dop) (2 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT1_DOP](#table-t-1bit-c-state-ready-obd-2-bit1-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT2_DOP](#table-t-1bit-state-ready-obd-1-bit2-dop) (2 × 2)
- [T_1BIT_FS_ERW_LR_AUS_BIT0_DOP](#table-t-1bit-fs-erw-lr-aus-bit0-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT5_DOP](#table-t-1bit-state-ready-obd-2-bit5-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_BIT1_DOP](#table-t-1bit-switch-position-bit1-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT6_DOP](#table-t-1bit-state-ready-obd-2-bit6-dop) (2 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT3_DOP](#table-t-1bit-c-state-ready-obd-2-bit3-dop) (2 × 2)
- [T_1BYTE_FS_GLF_DOP](#table-t-1byte-fs-glf-dop) (11 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT5_DOP](#table-t-1bit-c-state-ready-obd-2-bit5-dop) (2 × 2)
- [T_B_STANDARD_1BYTE_LESEN_0_1](#table-t-b-standard-1byte-lesen-0-1) (3 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT0_DOP](#table-t-1bit-c-state-ready-obd-2-bit0-dop) (2 × 2)
- [T_1BYTE_FS_DOP](#table-t-1byte-fs-dop) (11 × 2)
- [T_B_MSRHUBAD_DOP](#table-t-b-msrhubad-dop) (2 × 2)
- [T_1BIT_GLF_HIGH_BYTE_BIT7_DOP](#table-t-1bit-glf-high-byte-bit7-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT3_DOP](#table-t-1bit-switch-position-low-byte-bit3-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT1_DOP](#table-t-1bit-state-ready-obd-1-bit1-dop) (2 × 2)
- [T_1BIT_GLF_HIGH_BYTE_BIT1_DOP](#table-t-1bit-glf-high-byte-bit1-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT5_DOP](#table-t-1bit-state-ready-obd-1-bit5-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT0_DOP](#table-t-1bit-fs-erw-vvtl-bit0-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT3_DOP](#table-t-1bit-switch-position-high-byte-bit3-dop) (2 × 2)
- [T_1BIT_FS_ERW_LR_AUS_BIT1_DOP](#table-t-1bit-fs-erw-lr-aus-bit1-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_BIT7_DOP](#table-t-1bit-switch-position-bit7-dop) (2 × 2)
- [T_S_VSMNHB_DOP](#table-t-s-vsmnhb-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT2_DOP](#table-t-1bit-fs-erw-vvtl-bit2-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT6_DOP](#table-t-1bit-switch-position-low-byte-bit6-dop) (2 × 2)
- [T_1BIT_GLF_LOW_BYTE_BIT3_DOP](#table-t-1bit-glf-low-byte-bit3-dop) (2 × 2)
- [T_1BIT_GLF_HIGH_BYTE_BIT3_DOP](#table-t-1bit-glf-high-byte-bit3-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT1_DOP](#table-t-1bit-switch-position-high-byte-bit1-dop) (2 × 2)
- [T_1BIT_GLF_HIGH_BYTE_BIT2_DOP](#table-t-1bit-glf-high-byte-bit2-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT0_DOP](#table-t-1bit-state-ready-obd-2-bit0-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT5_DOP](#table-t-1bit-switch-position-high-byte-bit5-dop) (2 × 2)
- [T_ST_TESTPOELSYS_DOP](#table-t-st-testpoelsys-dop) (8 × 2)
- [T_1BIT_GLF_LOW_BYTE_BIT1_DOP](#table-t-1bit-glf-low-byte-bit1-dop) (2 × 2)
- [T_BA_IST_DOP](#table-t-ba-ist-dop) (5 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT2_DOP](#table-t-1bit-switch-position-high-byte-bit2-dop) (2 × 2)
- [T_1BIT_GLF_LOW_BYTE_BIT6_DOP](#table-t-1bit-glf-low-byte-bit6-dop) (2 × 2)

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

Dimensions: 137 rows × 2 columns

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
| 0xAF | Alfmeier |
| 0xB0 | ELTEK VALERE DEUTSCHLAND GMBH |
| 0xB1 | Omron Automotive Electronics Europe Group |
| 0xB2 | ASK |
| 0xB3 | CML Innovative Technologies GmbH & Co. KG |
| 0xB4 | APAG Elektronik AG |
| 0xB5 | Nexteer Automotive World Headquarters |
| 0xB6 | Hans Widmaier |
| 0xB7 | Robert Bosch Battery Systems GmbH |
| 0xB8 | KYOCERA Display Corporation |
| 0xB9 | MAGNA Powertrain AG & Co KG |
| 0xBA | BorgWarner |
| 0xBB | BMW - Fahrzeugsimulator |
| 0xBC | Benteler Duncan Plant |
| 0xBD | U-Shin |
| 0xBE | Schaeffler Technologies |
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
| 0x20 | Fehler momentan nicht vorhanden, nicht OBD-entprellt |
| 0x21 | Fehler momentan nicht vorhanden, OBD-entprellt |
| 0x22 | Fehler momentan vorhanden, noch nicht OBD-entprellt |
| 0x23 | Fehler momentan vorhanden, OBD-entprellt |
| 0x30 | Fehler verursacht kein Aufleuchten der Warnlampe (MIL) |
| 0x31 | Fehler wuerde das Aufleuchten der Warnlampe (MIL) verursachen |
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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 210 rows × 3 columns

| ORT | ORTTEXT | LIN_2_FORMAT |
| --- | --- | --- |
| 0x0100 | Batteriesensor BSD | - |
| 0x0150 | Ölqualitätsensor BSD | - |
| 0x0200 | Elektrische Wasserpumpe BSD | - |
| 0x0250 | Elektrische Kraftstoffpumpe BSD | - |
| 0x0300 | Generator 1 | - |
| 0x0350 | Generator 2 | - |
| 0x03A0 | Druck- Temperatursensor Tank | 1 |
| 0x03C0 | EAC-Sensor | - |
| 0x0400 | Schaltzentrum Lenksäule | - |
| 0x0500 | DSC Sensor-Cluster | - |
| 0x0600 | Nahbereichsradarsensor links | - |
| 0x0700 | Nahbereichsradarsensor rechts | - |
| 0x0800 | Funkempfänger | - |
| 0x0900 | Elektrische Lenksäulenverriegelung | - |
| 0x0A00 | Regen- Lichtsensor | - |
| 0x290A00 | DSC Hydraulikblock | - |
| 0x0B00 | Nightvision Kamera | - |
| 0x0C00 | TLC Kamera | - |
| 0x0D00 | Spurwechselradarsensor hinten links | - |
| 0x0E00 | Heckklima Bedienteil rechts | 1 |
| 0x0F00 | Rearview Kamera hinten | 1 |
| 0x0F80 | Frontview Kamera vorne | 1 |
| 0x1000 | Topview Kamera Außenspiegel links | 1 |
| 0x1100 | Topview Kamera Außenspiegel rechts | 1 |
| 0x1200 | Sideview Kamera Stoßfänger vorne links | 1 |
| 0x1210 | Sideview Kamera Kotflügel vorne links | 1 |
| 0x1300 | Sideview Kamera Stoßfänger vorne rechts | 1 |
| 0x1310 | Sideview Kamera Kotflügel vorne rechts | 1 |
| 0x1400 | Wischermotor | 1 |
| 0x1500 | Regen- Lichtsensor | 1 |
| 0x1600 | Innenspiegel | 1 |
| 0x1700 | Garagentoröffner | 1 |
| 0x1800 | AUC-Sensor | 1 |
| 0x1900 | Druck- Temperatursensor | 1 |
| 0x1A20 | Schalterblock Sitzheizung hinten links | 1 |
| 0x1A40 | Schalterblock Sitzheizung hinten rechts | 1 |
| 0x1A60 | Sitzheizung Fahrer | 1 |
| 0x1A80 | Sitzheizung Beifahrer | 1 |
| 0x1AA0 | Sitzheizung Fahrer hinten | 1 |
| 0x1AC0 | Sitzheizung Beifahrer hinten | 1 |
| 0x1B00 | Schalterblock Sitzmemory/-massage Fahrer | 1 |
| 0x1C00 | Schalterblock Sitzmemory/-massage Beifahrer | 1 |
| 0x1C80 | Sitzverstellschalter Beifahrer über Fond | 1 |
| 0x1D00 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x1E00 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x1E40 | Heckklappenemblem | 1 |
| 0x1F00 | KAFAS Kamera | 1 |
| 0x2000 | Automatische Anhängevorrichtung | 1 |
| 0x2100 | SINE | 1 |
| 0x2110 | DWA Mikrowellensensor vorne rechts | 1 |
| 0x2120 | DWA Mikrowellensensor hinten rechts | 1 |
| 0x2130 | DWA Mikrowellensensor hinten links | 1 |
| 0x2140 | DWA Mikrowellensensor vorne links | 1 |
| 0x2150 | DWA Mikrowellensensor hinten | 1 |
| 0x2180 | DWA Ultraschallsensor | 1 |
| 0x2200 | Aussenspiegel Fahrer | - |
| 0x2300 | Aussenspiegel Beifahrer | - |
| 0x2400 | Schaltzentrum Tür | 1 |
| 0x2500 | Schalterblock Sitz Fahrer | 1 |
| 0x2600 | Schalterblock Sitz Beifahrer | 1 |
| 0x2700 | Gurtbringer Fahrer | 1 |
| 0x2800 | Gurtbringer Beifahrer | 1 |
| 0x2900 | Treibermodul Scheinwerfer links | 1 |
| 0x2A00 | Treibermodul Scheinwerfer rechts | 1 |
| 0x2B00 | Bedieneinheit Fahrerassistenzsysteme | 1 |
| 0x2C00 | Bedieneinheit Licht | 1 |
| 0x2D00 | Smart Opener | 1 |
| 0x2E00 | LED-Hauptlicht-Modul links | 1 |
| 0x2F00 | LED-Hauptlicht-Modul rechts | 1 |
| 0x0910 | Elektrische Lenksäulenverriegelung | 1 |
| 0x3200 | Funkempfänger | 1 |
| 0x3300 | Funkempfänger 2 | 1 |
| 0x3400 | Türgriffelektronik Fahrer | - |
| 0x3500 | Türgriffelektronik Beifahrer | - |
| 0x3600 | Türgriffelektronik Fahrer hinten | - |
| 0x3700 | Türgriffelektronik Beifahrer hinten | - |
| 0x3800 | Telestart-Handsender 1 | - |
| 0x3900 | Telestart-Handsender 2 | - |
| 0x3A00 | Fond-Fernbedienung | - |
| 0x3B00 | Elektrische Wasserpumpe | 1 |
| 0x3B10 | Elektrische Wasserpumpe 1 | 1 |
| 0x3B20 | Elektrische Wasserpumpe 2 | 1 |
| 0x3B80 | Elektrische Zusatzwasserpumpe | 1 |
| 0x3C00 | Batteriesensor LIN | - |
| 0x3D00 | Aktives Kühlklappensystem | 1 |
| 0x3D80 | Lüfter | 1 |
| 0x3D88 | Lüfter 2 | 1 |
| 0x3E00 | PCU(DCDC) | 1 |
| 0x3E80 | DCDC Versorgung Zustartbatterie | 1 |
| 0x3F00 | Startergenerator | 1 |
| 0x3F80 | Generator | 1 |
| 0x4000 | Sitzverstellschalter Fahrer | 1 |
| 0x4100 | Sitzverstellschalter Beifahrer | 1 |
| 0x4200 | Sitzverstellschalter Fahrer hinten | 1 |
| 0x4300 | Sitzverstellschalter Beifahrer hinten | 1 |
| 0x4400 | Gepäckraumschalter links | 1 |
| 0x4500 | Gepäckraumschalter rechts | 1 |
| 0x4600 | Nackenwärmer | 1 |
| 0x4700 | Nackenwärmer Bedienschalter | 1 |
| 0x4A00 | Fond-Klimaanlage | 1 |
| 0x4B00 | Elektrischer Klimakompressor | 1 |
| 0x4C00 | Klimabedienteil | 1 |
| 0x4D00 | Gebläseregler | 1 |
| 0x4E00 | Klappenmotor | 0 |
| 0x4F00 | Elektrischer Kältemittelverdichter eKMV | 1 |
| 0x4F80 | Elektrischer Zuheizer PTC | 1 |
| 0x4FC0 | Elektrischer Zuheizer 3. Sitzreihe | 1 |
| 0x6000 | Standheizung | 1 |
| 0x6100 | Wärmepumpe | 1 |
| 0x6200 | elektrischer Durchlaufheizer | 1 |
| 0x6300 | Ionisator | 1 |
| 0x6400 | Bedufter | 1 |
| 0x6500 | Sense-Touch-Modul links | 1 |
| 0x6600 | Sense-Touch-Modul rechts | 1 |
| 0x5000 | PMA Sensor links | 1 |
| 0x5100 | PMA Sensor rechts | 1 |
| 0x5200 | CID-Klappe | - |
| 0x5300 | Schaltzentrum Lenksäule | 1 |
| 0x5400 | Multifunktionslenkrad | 1 |
| 0x5500 | Lenkradelektronik | 1 |
| 0x5600 | CID | - |
| 0x5700 | Satellit Upfront links | 0 |
| 0x5708 | Satellit Upfront rechts | 0 |
| 0x5710 | Satellit Tür links | 0 |
| 0x5718 | Satellit Tür rechts | 0 |
| 0x5720 | Satellit B-Säule links X | 0 |
| 0x5728 | Satellit B-Säule rechts X | 0 |
| 0x5730 | Satellit B-Säule links Y | 0 |
| 0x5738 | Satellit B-Säule rechts Y | 0 |
| 0x5740 | Satellit Zentralsensor X | 0 |
| 0x5748 | Satellit Zentralsensor Y | 0 |
| 0x5750 | Satellit Zentralsensor Low g Y | 0 |
| 0x5758 | Satellit Zentralsensor Low g Z | 0 |
| 0x5760 | Satellit Zentralsensor Roll Achse | 0 |
| 0x5768 | Fussgängerschutz Sensor links | 0 |
| 0x5770 | Fussgängerschutz Sensor rechts | 0 |
| 0x5778 | Fussgängerschutz Sensor mitte | 0 |
| 0x5780 | Fussgängerschutzsensor statisch | 0 |
| 0x5788 | Satellit C-Säule links Y | 0 |
| 0x5790 | Satellit C-Säule rechts Y | 0 |
| 0x5798 | Satellit Zentrale Körperschall | 0 |
| 0x57A0 | Kapazitive Insassen- Sensorik CIS | 1 |
| 0x57A8 | Sitzbelegungserkennung Beifahrer SBR | 1 |
| 0x57B0 | Fussgängerschutzsensor dynamisch 1 | 0 |
| 0x57B8 | Fussgängerschutzsensor dynamisch 2 | 0 |
| 0x5800 | HUD | 1 |
| 0x5900 | Audio-Bedienteil | 1 |
| 0x5A00 | Innenlichtelektronik | 1 |
| 0x5A20 | Innenlichteinheit 2 | 1 |
| 0x5A30 | Innenlichteinheit 3 | 1 |
| 0x5B00 | Zentralinstrument | 1 |
| 0x5B40 | CID | 1 |
| 0x5B80 | Fondmonitor links | 1 |
| 0x5BC0 | Fondmonitor rechts | 1 |
| 0x5C00 | Elektrische Lenksäulenverstellung ELSV | 1 |
| 0x5D00 | Hands-Off Detection HOD | 1 |
| 0x5E01 | Innenbeleuchtung Fußraum Fahrer vorne | 1 |
| 0x5E02 | Innenbeleuchtung Fußraum Fahrer hinten | 1 |
| 0x5E03 | Innenbeleuchtung Fußraum Beifahrer vorne | 1 |
| 0x5E04 | Innenbeleuchtung Fußraum Beifahrer hinten | 1 |
| 0x5E05 | Innenbeleuchtung Fahrertür vorne oben | 1 |
| 0x5E06 | Innenbeleuchtung Fahrertür vorne Mitte | 1 |
| 0x5E07 | Innenbeleuchtung Fahrertür vorne unten | 1 |
| 0x5E08 | Innenbeleuchtung Fahrertür vorne Kartentasche | 1 |
| 0x5E09 | Innenbeleuchtung Fahrertür hinten oben | 1 |
| 0x5E0A | Innenbeleuchtung Fahrertür hinten unten | 1 |
| 0x5E0B | Innenbeleuchtung Fahrertür hinten Kartentasche | 1 |
| 0x5E0C | Innenbeleuchtung Beifahrertür vorne oben | 1 |
| 0x5E0D | Innenbeleuchtung Beifahrertür vorne Mitte | 1 |
| 0x5E0E | Innenbeleuchtung Beifahrertür vorne unten | 1 |
| 0x5E0F | Innenbeleuchtung Beifahrertür vorne Kartentasche | 1 |
| 0x5E10 | Innenbeleuchtung Beifahrertür hinten oben | 1 |
| 0x5E11 | Innenbeleuchtung Beifahrertür hinten unten | 1 |
| 0x5E12 | Innenbeleuchtung Beifahrertür hinten Kartentasche | 1 |
| 0x5E13 | Innenbeleuchtung I-Tafel Fahrer oben | 1 |
| 0x5E14 | Innenbeleuchtung I-Tafel Fahrer unten | 1 |
| 0x5E15 | Innenbeleuchtung I-Tafel oben Mitte | 1 |
| 0x5E16 | Innenbeleuchtung I-Tafel unten Mitte | 1 |
| 0x5E17 | Innenbeleuchtung I-Tafel oben Beifahrer | 1 |
| 0x5E18 | Innenbeleuchtung I-Tafel unten Beifahrer | 1 |
| 0x5E19 | Innenbeleuchtung B-Säule Fahrer | 1 |
| 0x5E1A | Innenbeleuchtung B-Säule Beifahrer | 1 |
| 0x5E1B | Innenbeleuchtung Lehne Fahrersitz | 1 |
| 0x5E1C | Innenbeleuchtung Lehne Beifahrersitz | 1 |
| 0x5E1D | Innenbeleuchtung Centerstack | 1 |
| 0x5E1E | Innenbeleuchtung Mittelkonsole Ablagefach | 1 |
| 0x5E1F | Innenbeleuchtung Gangwahlschalter links | 1 |
| 0x5E20 | Innenbeleuchtung Gangwahlschalter rechts | 1 |
| 0x5E80 | Stromverteiler hinten | 1 |
| 0x5EA0 | Wireless Charging Ablage | - |
| 0x5F00 | Integrierte Fensterheber Elektronik Fahrer | 1 |
| 0x5F10 | Integrierte Fensterheber Elektronik Beifahrer | 1 |
| 0x5F20 | Integrierte Fensterheber Elektronik Fahrer hinten | 1 |
| 0x5F30 | Integrierte Fensterheber Elektronik Beifahrer hinten | 1 |
| 0x5F40 | Schalterblock Sitzmemory Fahrer | 1 |
| 0x5F50 | Schalterblock Sitzmemory Beifahrer | 1 |
| 0x5F60 | Schalterblock Sitzmemory Fahrer hinten | 1 |
| 0x5F70 | Schalterblock Sitzmemory Beifahrer hinten | 1 |
| 0x5F80 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x5F90 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x5FA0 | Bedieneinheit Mittelkonsole | 1 |
| 0x5FB0 | WB und SARAH Schalter | 1 |
| 0x7000 | Abschattungs-Elektronik-Dach | 1 |
| 0x7040 | Frontwischermotor | 1 |
| 0x7100 | NFC Leser Innenraum vorne | 1 |
| 0x7200 | Spurwechselradarsensor vorne rechts | 1 |
| 0x7208 | Spurwechselradarsensor vorne links | 1 |
| 0x7210 | Spurwechselradarsensor hinten rechts (Master) | 1 |
| 0x7218 | Spurwechselradarsensor hinten links | 1 |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-messwertemode"></a>
### MESSWERTEMODE

Dimensions: 14 rows × 3 columns

| TEXT | WERT | KOMMENTAR |
| --- | --- | --- |
| ein | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| aus | 0 | Argument ARG.   Messwertblock nur lesen |
| ja | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| nein | 0 | Argument ARG.   Messwertblock nur lesen |
| yes | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| no | 0 | Argument ARG.   Messwertblock nur lesen |
| on | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| off | 0 | Argument ARG.   Messwertblock nur lesen |
| 1 | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| 0 | 0 | Argument ARG.   Messwertblock nur lesen |
| 3 | 3 | Argument ID.    Messwertblock im SG löschen, neu schreiben und lesen |
| 2 | 2 | Argument ID.    Messwertblock nur lesen |
| 5 | 5 | Argument LABEL. Messwertblock im SG löschen, neu schreiben und lesen |
| 4 | 4 | Argument LABEL. Messwertblock nur lesen |

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 20 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x04 | Filt | Mikrofilter |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x07 | CSF | Dieselpartikelfilter |
| 0x08 | Batt | Batterie |
| 0x09 | QMV | QMV-H-Oel |
| 0x10 | ZKrz | Zuendkerzen |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x12 | Kfl | Kuehlfluessigkeit |
| 0x13 | H2 | H2-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x15 | Efk | Einfahrkontrolle |
| 0x16 | DAD | Additiv fuer Partikelfilter |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |
| 0x23 | DKG | DK-Getriebeoel |
| 0x0A | ZKrz_a | Zuendkerzen adaptiv |
| 0x0D | NOx_a | NOx-Additiv |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 00654321 |
| F_PCODE | ja |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 761 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x2710 | 0x2710 Drosselklappe, Funktion: klemmt dauerhaft |
| 0x2711 | 0x2711 Drosselklappe, Funktion: klemmt kurzzeitig |
| 0x2714 | 0x2714 Drosselklappe, Funktion: schwergängig, zu langsam |
| 0x2774 | 0x2774 Luftmasse, Plausibilität: Luftmasse zu hoch |
| 0x2775 | 0x2775 Luftmasse, Plausibilität: Luftmasse zu niedrig |
| 0x2778 | 0x2778 Luftmassenmesser, Arbeitsbereich: Periodendauer zu niedrig, Luftmasse zu hoch |
| 0x2779 | 0x2779 Luftmassenmesser, Arbeitsbereich: Periodendauer zu groß, Luftmasse zu niedrig |
| 0x277A | 0x277A Luftmassenmesser, Signal: elektrischer Fehler |
| 0x277B | 0x277B Luftmassenmesser, Arbeitsbereich: Periodendauer zu groß, Luftmasse zu hoch |
| 0x277C | 0x277C Luftmassenmesser, Arbeitsbereich: Periodendauer zu niedrig, Luftmasse zu niedrig |
| 0x27D9 | 0x27D9 Fahrpedalmodul, Pedalwertgeber 1, elektrisch: Kurzschluss nach Plus |
| 0x27DA | 0x27DA Fahrpedalmodul, Pedalwertgeber 1, elektrisch: Kurzschluss nach Masse |
| 0x27DB | 0x27DB Fahrpedalmodul, Pedalwertgeber 2, elektrisch: Kurzschluss nach Plus |
| 0x27DC | 0x27DC Fahrpedalmodul, Pedalwertgeber 2, elektrisch: Kurzschluss nach Masse |
| 0x27E4 | 0x27E4 Fahrpedalmodul, Pedalwertgeber: Sammelfehler |
| 0x27E8 | 0x27E8 Fahrpedalmodul, Pedalwertgeber, Plausibilität: Gleichlauffehler zwischen Pedalwertgeber 1 und Pedalwertgeber 2 |
| 0x280E | 0x280E Absolutdrucksensor, Saugrohr, Plausibilität, Nachlauf: Druck zu hoch |
| 0x280F | 0x280F Absolutdrucksensor, Saugrohr, Plausibilität, Nachlauf: Druck zu niedrig |
| 0x281A | 0x281A Absolutdrucksensor, Saugrohr, elektrisch: Kurzschluss nach Plus |
| 0x281B | 0x281B Absolutdrucksensor, Saugrohr, elektrisch: Kurzschluss nach Masse |
| 0x2820 | 0x2820 Absolutdrucksensor, Saugrohr: Sammelfehler |
| 0x283C | 0x283C DME: interner Fehler [Umgebungsdrucksensor: Kurzschluss nach Plus] |
| 0x283D | 0x283D DME: interner Fehler [Umgebungsdrucksensor: Kurzschluss nach Masse] |
| 0x2841 | 0x2841 DME: interner Fehler [Umgebungsdrucksensor, Plausibilität: Druck zu hoch im Nachlauf] |
| 0x2842 | 0x2842 DME: interner Fehler [Umgebungsdrucksensor, Plausibilität: Druck zu niedrig im Nachlauf] |
| 0x2848 | 0x2848 DME: interner Fehler [Umgebungsdrucksensor: Sammelfehler] |
| 0x284C | 0x284C DME: interner Fehler [Umgebungsdrucksensor, Arbeitsbereich: Druck zu hoch] |
| 0x284D | 0x284D DME: interner Fehler [Umgebungsdrucksensor, Arbeitsbereich: Druck zu niedrig] |
| 0x284E | 0x284E DME: interner Fehler [Umgebungsdrucksensor, Plausibilität: Druck unplausibel] |
| 0x284F | 0x284F DME: interner Fehler [Umgebungsdrucksensor, Plausibilität: Druck unplausibel] |
| 0x28A0 | 0x28A0 Drosselklappenwinkel - Absolutdruck Saugrohr, Vergleich: Druck zu hoch |
| 0x28A1 | 0x28A1 Drosselklappenwinkel - Absolutdruck Saugrohr, Vergleich: Druck zu niedrig |
| 0x28A4 | 0x28A4 Drosselklappe, Drosselklappenpotenziometer 1, elektrisch: Kurzschluss nach Plus |
| 0x28A5 | 0x28A5 Drosselklappe, Drosselklappenpotenziometer 1, elektrisch: Kurzschluss nach Masse |
| 0x28A6 | 0x28A6 Drosselklappe, Drosselklappenpotenziometer 1: Signal unplausibel zur Luftmasse |
| 0x28A8 | 0x28A8 Drosselklappe, Drosselklappenpotenziometer 2, elektrisch: Kurzschluss nach Plus |
| 0x28A9 | 0x28A9 Drosselklappe, Drosselklappenpotenziometer 2, elektrisch: Kurzschluss nach Masse |
| 0x28AA | 0x28AA Drosselklappe, Drosselklappenpotenziometer 2: Signal unplausibel zur Luftmasse |
| 0x28AC | 0x28AC Drosselklappe, Drosselklappenpotenziometer 1 und 2: Doppelfehler |
| 0x28B0 | 0x28B0 Drosselklappe: Notlauf aktiv |
| 0x28B4 | 0x28B4 Drosselklappe, Drosselklappenpotenziometer, Plausibilität: Gleichlauffehler zwischen Potentiometer 1 und 2 |
| 0x28B8 | 0x28B8 Drosselklappe, Ansteuerung: Kurzschluss |
| 0x28B9 | 0x28B9 Drosselklappe, Ansteuerung: Übertemperatur oder Strom zu hoch |
| 0x28BA | 0x28BA DME, interner Fehler, Ansteuerung Drosselklappe: interner Kommunikationsfehler |
| 0x28BB | 0x28BB Drosselklappe, Ansteuerung: Leitungsunterbrechung |
| 0x28BC | 0x28BC Drosselklappe, schliessende Federprüfung: Abbruch Prüfung, Feder schliesst nicht |
| 0x28BD | 0x28BD Drosselklappe, schliessende Federprüfung: Fehlfunktion |
| 0x28C0 | 0x28C0 Drosselklappe, öffnende Federprüfung: Abbruch Prüfung, Feder öffnet nicht |
| 0x28C1 | 0x28C1 Drosselklappe, öffnende Federprüfung: Fehlfunktion |
| 0x28C4 | 0x28C4 Drosselklappe, Adaption: Notluftposition nicht adaptiert |
| 0x28CC | 0x28CC Drosselklappe, Adaption: Randbedingungen nicht erfüllt |
| 0x28CD | 0x28CD Drosselklappe, Adaption: Randbedingungen nicht erfüllt, Batteriespannung zu niedrig |
| 0x28D0 | 0x28D0 Drosselklappe, Adaption: Erstadaption, unterer Anschlag nicht gelernt |
| 0x28D4 | 0x28D4 Drosselklappe, Adaption: Wiederlernen, unterer Anschlag nicht gelernt |
| 0x28D8 | 0x28D8 Drosselklappensteller, Verstärkerabgleich: Fehlfunktion |
| 0x28D9 | 0x28D9 Tuningschutz: Luftmasse zu hoch |
| 0x2904 | 0x2904 Ladelufttemperatursensor: Sammelfehler |
| 0x2906 | 0x2906 Ansaugluftsystem: Verdacht auf Undichtigkeit zwischen Turbolader und Einlassventilen |
| 0x2908 | 0x2908 Ladelufttemperatursensor: Sammelfehler |
| 0x290A | 0x290A Ansauglufttemperatursensor: Sammelfehler |
| 0x2936 | 0x2936 Kühlmitteltemperatursensor, elektrisch: Kurzschluss nach Masse |
| 0x2937 | 0x2937 Kühlmitteltemperatursensor, elektrisch: Kurzschluss nach Plus |
| 0x293A | 0x293A Kühlmitteltemperatursensor, Plausibilität, Kaltstart: Temperatur zu hoch |
| 0x293B | 0x293B Kühlmitteltemperatursensor, Plausibilität, Kaltstart: Temperatur zu niedrig |
| 0x293E | 0x293E Kühlmitteltemperatursensor: Sammelfehler |
| 0x2942 | 0x2942 Kühlmitteltemperatursensor, elektrisch: Signal fehlt |
| 0x2943 | 0x2943 Kühlmitteltemperatursensor, Signaländerung: zu schnell |
| 0x2946 | 0x2946 Kühlmitteltemperatursensor, Plausibilität: Motortemperatur gegenüber Modell unplausibel zu hoch |
| 0x2947 | 0x2947 Kühlmitteltemperatursensor, Signal: festliegend auf niedrig |
| 0x2948 | 0x2948 Kühlmitteltemperatursensor, Signal: festliegend |
| 0x299A | 0x299A Außentemperatursensor, Signal: Oberen Schwellwert überschritten |
| 0x299B | 0x299B Außentemperatursensor, Signal: Unteren Schwellwert unterschritten |
| 0x299C | 0x299C Außentemperatursensor, Signal: CAN-Botschaft fehlerhaft |
| 0x299E | 0x299E Außentemperatursensor, Sammelfehler: elektrisch und Plausibilität |
| 0x29A2 | 0x29A2 Außentemperatursensor, Plausibilität: Umgebungstemperatur größer als Modelltemperatur |
| 0x29A3 | 0x29A3 Außentemperatursensor, Plausibilität: Umgebungstemperatur kleiner als Modelltemperatur |
| 0x29CC | 0x29CC Ansauglufttemperatursensor, Plausibilität, Kaltstart: Temperatur zu hoch |
| 0x29CD | 0x29CD Ansauglufttemperatursensor, Plausibilität, Kaltstart: Temperatur zu niedrig |
| 0x29D0 | 0x29D0 Ansauglufttemperatursensor, elektrisch: Kurzschluss nach Plus |
| 0x29D1 | 0x29D1 Ansauglufttemperatursensor, elektrisch: Kurzschluss nach Masse |
| 0x29D2 | 0x29D2 Ansauglufttemperatursensor, Signaländerung: zu schnell |
| 0x29D8 | 0x29D8 Ansauglufttemperatur - Ladelufttemperatur, Vergleich: Ansauglufttemperatur zu hoch |
| 0x29D9 | 0x29D9 Ansauglufttemperatur - Ladelufttemperatur, Vergleich: Ansauglufttemperatur zu niedrig |
| 0x29DC | 0x29DC Ladelufttemperatursensor, Plausibilität, Kaltstart: Temperatur zu hoch |
| 0x29DD | 0x29DD Ladelufttemperatursensor, Plausibilität, Kaltstart: Temperatur zu niedrig |
| 0x29E0 | 0x29E0 Ladelufttemperatursensor, elektrisch: Kurzschluss nach Plus |
| 0x29E1 | 0x29E1 Ladelufttemperatursensor, elektrisch: Kurzschluss nach Masse |
| 0x29E2 | 0x29E2 Ladelufttemperatursensor, Spannungsänderung: zu schnell |
| 0x29E4 | 0x29E4 Ladelufttemperatur, Plausibilität: Temperatur zu hoch |
| 0x29E5 | 0x29E5 Ladelufttemperatur, Signal: festliegend |
| 0x29E6 | 0x29E6 Ladelufttemperatursensor, Kaltstart: Sammelfehler |
| 0x29E7 | 0x29E7 Ladelufttemperatursensor: Sammelfehler |
| 0x29E8 | 0x29E8 Ladelufttemperatursensor, Signaländerung: zu schnell |
| 0x29FE | 0x29FE Injektor Zylinder 1, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x29FF | 0x29FF Injektor Zylinder 1, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A00 | 0x2A00 Injektor Zylinder 1, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A01 | 0x2A01 Injektor Zylinder 1, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A02 | 0x2A02 Injektor Zylinder 2, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x2A03 | 0x2A03 Injektor Zylinder 2, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A04 | 0x2A04 Injektor Zylinder 2, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A05 | 0x2A05 Injektor Zylinder 2, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A06 | 0x2A06 Injektor Zylinder 3, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x2A07 | 0x2A07 Injektor Zylinder 3, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A08 | 0x2A08 Injektor Zylinder 3, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A09 | 0x2A09 Injektor Zylinder 3, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A0A | 0x2A0A Injektor Zylinder 4, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x2A0B | 0x2A0B Injektor Zylinder 4, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A0C | 0x2A0C Injektor Zylinder 4, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A0D | 0x2A0D Injektor Zylinder 4, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A0E | 0x2A0E Injektor Zylinder 5, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x2A0F | 0x2A0F Injektor Zylinder 5, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A10 | 0x2A10 Injektor Zylinder 5, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A11 | 0x2A11 Injektor Zylinder 5, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A12 | 0x2A12 Injektor Zylinder 6, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x2A13 | 0x2A13 Injektor Zylinder 6, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A14 | 0x2A14 Injektor Zylinder 6, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A15 | 0x2A15 Injektor Zylinder 6, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A30 | 0x2A30 Injektor Zylinder 1, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A31 | 0x2A31 Injektor Zylinder 2, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A32 | 0x2A32 Injektor Zylinder 3, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A33 | 0x2A33 Injektor Zylinder 4, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A34 | 0x2A34 Injektor Zylinder 5, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A35 | 0x2A35 Injektor Zylinder 6, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A40 | 0x2A40 Injektor Zylinder 1, Stromanstieg: zu langsam |
| 0x2A41 | 0x2A41 Injektor Zylinder 2, Stromanstieg: zu langsam |
| 0x2A42 | 0x2A42 Injektor Zylinder 3, Stromanstieg: zu langsam |
| 0x2A43 | 0x2A43 Injektor Zylinder 4, Stromanstieg: zu langsam |
| 0x2A44 | 0x2A44 Injektor Zylinder 5, Stromanstieg: zu langsam |
| 0x2A45 | 0x2A45 Injektor Zylinder 6, Stromanstieg: zu langsam |
| 0x2A4C | 0x2A4C Injektor Zylinder 1, Ansteuerung: Leitungsunterbrechung |
| 0x2A4D | 0x2A4D Injektor Zylinder 2, Ansteuerung: Leitungsunterbrechung |
| 0x2A4E | 0x2A4E Injektor Zylinder 3, Ansteuerung: Leitungsunterbrechung |
| 0x2A4F | 0x2A4F Injektor Zylinder 4, Ansteuerung: Leitungsunterbrechung |
| 0x2A50 | 0x2A50 Injektor Zylinder 5, Ansteuerung: Leitungsunterbrechung |
| 0x2A51 | 0x2A51 Injektor Zylinder 6, Ansteuerung: Leitungsunterbrechung |
| 0x2A5F | 0x2A5F Relais Zündung und Injektoren, Versorgungsspannung Einspritzung: Kurzschluss nach Plus |
| 0x2A60 | 0x2A60 Relais Zündung und Injektoren, Versorgungsspannung Einspritzung: Kurzschluss nach Masse |
| 0x2A61 | 0x2A61 Relais Zündung und Injektoren, Versorgungsspannung Einspritzung: Leitungsunterbrechung |
| 0x2A70 | 0x2A70 DME, interner Fehler, HDEV-Endstufen-Baustein 1: SPI-Kommunikation fehlerhaft |
| 0x2A71 | 0x2A71 DME, interner Fehler, HDEV-Endstufen-Baustein 2: SPI-Kommunikation fehlerhaft |
| 0x2A72 | 0x2A72 DME, interner Fehler, HDEV-Endstufen-Baustein 1: SPI-Kommunikation unplausibel |
| 0x2A73 | 0x2A73 DME, interner Fehler, HDEV-Endstufen-Baustein 2: SPI-Kommunikation unplausibel |
| 0x2A74 | 0x2A74 DME, interner Fehler, HDEV-Endstufen-Baustein 1: SPI-Kommunikation gestört |
| 0x2A75 | 0x2A75 DME, interner Fehler, HDEV-Endstufen-Baustein 2: SPI-Kommunikation gestört |
| 0x2BC0 | 0x2BC0 Gemischregelung: Gemisch zu mager |
| 0x2BC1 | 0x2BC1 Gemischregelung: Gemisch zu fett |
| 0x2BC2 | 0x2BC2 Gemischadaption, Leerlauf: Gemisch zu mager |
| 0x2BC3 | 0x2BC3 Gemischadaption, Leerlauf: Gemisch zu fett |
| 0x2BC5 | 0x2BC5 Gemischadaption, Injektor-Alterung: Zylinderseite 1: langfristige Adaption zu hoch |
| 0x2BCA | 0x2BCA Lambdasonde vor Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu fett |
| 0x2BCB | 0x2BCB Lambdasonde vor Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu mager |
| 0x2BD9 | 0x2BD9 Raildrucksensor, elektrisch: Kurzschluss nach Plus |
| 0x2BDA | 0x2BDA Raildrucksensor, elektrisch: Kurzschluss nach Masse |
| 0x2BDB | 0x2BDB Kraftstoffhochdruck, Plausibilität: Druck zu hoch, Notlauf mit Niederdruck |
| 0x2BDC | 0x2BDC Kraftstoffversorgungssystem: Druck zu hoch, Notlauf mit Einspritzabschaltung |
| 0x2BDD | 0x2BDD Kraftstoffhochdruck: Druck kurzzeitig zu hoch, Drehzahl- und Lastbegrenzung |
| 0x2BDE | 0x2BDE Kraftstoffhochdruck bei Freigabe der Einspritzung: Druck zu niedrig |
| 0x2BDF | 0x2BDF Kraftstoffniederdrucksystem, Plausibilität: Leistung elektrische Kraftstoffpumpe für Istdruck zu hoch |
| 0x2BE0 | 0x2BE0 Kraftstoffniederdrucksystem: Leistung elektrische Kraftstoffpumpe für Istdruck zu niedrig |
| 0x2BE1 | 0x2BE1 Kraftstoffniederdrucksystem, Plausibilität: Förderleistung zu niedrig |
| 0x2BE2 | 0x2BE2 Kraftstoffniederdrucksystem, Plausibilität: Spannung elektrische Kraftstoffpumpe unplausibel |
| 0x2BE3 | 0x2BE3 Kraftstoffniederdruck, Arbeitsbereich: Druck zu niedrig |
| 0x2BE4 | 0x2BE4 Kraftstoffniederdruck, Arbeitsbereich: Druck zu hoch |
| 0x2BE5 | 0x2BE5 Kraftstoffhochdrucksystem, Plausibilität: Regelabweichung des Mengensteuerventils zu groß |
| 0x2BE6 | 0x2BE6 Kraftstoffhochdrucksystem, Plausibilität: Regelabweichung des Mengensteuerventils zu klein |
| 0x2BE9 | 0x2BE9 Zylindereinspritzabschaltung: Druck zu niedrig im Hochdrucksystem |
| 0x2BEA | 0x2BEA Gemischregelung: Gemisch zu mager, große Abweichung |
| 0x2BEB | 0x2BEB Gemischregelung: Gemisch zu fett, große Abweichung |
| 0x2BEC | 0x2BEC Kraftstoffhochdruck nach Motorstopp: Druck zu hoch |
| 0x2BED | 0x2BED Kraftstoffhochdruck, Plausibilität, Kaltstart: Druck zu hoch |
| 0x2BEE | 0x2BEE Kraftstoffhochdruck, Plausibilität, Kaltstart: Druck zu niedrig |
| 0x2BEF | 0x2BEF Kraftstoffhochdruck nach Freigabe der Einspritzung: Druck zu niedrig |
| 0x2BF0 | 0x2BF0 Kraftstoffhochdruck bei oder nach Freigabe der Einspritzung (2. Umweltbedingungssatz nach Zeitverzögerung): Druck zu niedrig |
| 0x2BF2 | 0x2BF2 Raildrucksensor, Arbeitsbereich: Druck zu hoch |
| 0x2BF3 | 0x2BF3 Raildrucksensor, Arbeitsbereich: Druck zu niedrig |
| 0x2BF4 | 0x2BF4 Raildrucksensor, Plausibilität: Druck zu hoch vor Motorstart |
| 0x2BF5 | 0x2BF5 Raildrucksensor, Plausibilität: Druck zu niedrig vor Motorstart |
| 0x2BF6 | 0x2BF6 Kraftstoffniederdrucksensor, elektrisch: Kurzschluss nach Plus |
| 0x2BF7 | 0x2BF7 Kraftstoffniederdrucksensor, elektrisch: Kurzschluss nach Masse |
| 0x2BF8 | 0x2BF8 Raildrucksensor, Signal: festliegend |
| 0x2C00 | 0x2C00 Kraftstoffhochdruck, Plausibilität: Druck zu hoch |
| 0x2C01 | 0x2C01 Kraftstoffhochdruck, Plausibilität: Druck zu niedrig |
| 0x2C3D | 0x2C3D Mengensteuerventil, Ansteuerung: Kurzschluss nach Plus |
| 0x2C3E | 0x2C3E Mengensteuerventil, Ansteuerung: Kurzschluss nach Masse |
| 0x2C3F | 0x2C3F Mengensteuerventil, Ansteuerung: Leitungsunterbrechung |
| 0x2C42 | 0x2C42 Gemischregelung: Sammelfehler |
| 0x2C56 | 0x2C56 Ladedruckregelung, Plausibilität: Druck zu hoch |
| 0x2C57 | 0x2C57 Ladedruckregelung, Plausibilität: Druck zu niedrig |
| 0x2C58 | 0x2C58 Ladedruckregelung: Abschaltung als Folgereaktion |
| 0x2C6F | 0x2C6F Ladedrucksensor, elektrisch: Kurzschluss nach Plus |
| 0x2C70 | 0x2C70 Ladedrucksensor, elektrisch: Kurzschluss nach Masse |
| 0x2C71 | 0x2C71 Ladedrucksensor, Plausibilität, Nachlauf: Druck zu hoch |
| 0x2C72 | 0x2C72 Ladedrucksensor, Plausibilität, Nachlauf: Druck zu niedrig |
| 0x2C7F | 0x2C7F Ladedrucksensor: Sammelfehler |
| 0x2C83 | 0x2C83 Ladedruck, Plausibilität: Druck zu hoch |
| 0x2C84 | 0x2C84 Ladedruck, Arbeitsbereich: Druck zu niedrig |
| 0x2C85 | 0x2C85 Ladedruck - Umgebungsdruck, Vergleich: Ladedruck zu hoch |
| 0x2C86 | 0x2C86 Ladedruck - Umgebungsdruck, Vergleich: Ladedruck zu niedrig |
| 0x2C88 | 0x2C88 Schubumluftventil, Ansteuerung: Kurzschluss nach Plus |
| 0x2C89 | 0x2C89 Schubumluftventil, Ansteuerung: Kurzschluss nach Masse |
| 0x2C8A | 0x2C8A Schubumluftventil, Ansteuerung: Leitungsunterbrechung |
| 0x2C90 | 0x2C90 Schubumluftventil: klemmt geschlossen |
| 0x2C91 | 0x2C91 Schubumluftventil, Mechanik: Verdacht auf offen klemmendes Schubumluftventil |
| 0x2CA1 | 0x2CA1 Wastegate, Ansteuerung: Kurzschluss nach Plus |
| 0x2CA2 | 0x2CA2 Wastegate, Ansteuerung: Kurzschluss nach Masse |
| 0x2CA3 | 0x2CA3 Wastegate, Ansteuerung: Leitungsunterbrechung |
| 0x2CB3 | 0x2CB3 Wastegate, Ansteuerung: Verdacht auf Fehler in der Wastegateansteuerung |
| 0x2CED | 0x2CED Lambdasonde nach Katalysator, Dynamik, von Fett nach Mager: langsame Reaktion |
| 0x2CEE | 0x2CEE Lambdasondenbeheizung vor Katalysator, Funktion: Heizelement fehlerhaft |
| 0x2CF4 | 0x2CF4 Lambdasonde vor Katalysator, Dynamik: langsame Reaktion |
| 0x2CF8 | 0x2CF8 Lambdasonde vor Katalysator: Falschluft erkannt |
| 0x2CFA | 0x2CFA Lambdasonde vor Katalysator, elektrisch: Unterbrechung Nernstleitung |
| 0x2CFE | 0x2CFE Lambdasonde vor Katalysator, Leitungsfehler: Unterbrechung Abgleichleitung |
| 0x2CFF | 0x2CFF Lambdasonde vor Katalysator, Signalleitungen: Kurzschluss nach Plus |
| 0x2D00 | 0x2D00 Lambdasonde vor Katalysator, Signalleitungen: Kurzschluss nach Masse |
| 0x2D03 | 0x2D03 DME, interner Fehler, Lambdasonde vor Katalysator: Lambdasondenbaustein, Signalkreisadaptionswerte zu hoch |
| 0x2D04 | 0x2D04 DME, interner Fehler, Lambdasonde vor Katalysator: Lambdasondenbaustein, Unterspannung |
| 0x2D05 | 0x2D05 DME, interner Fehler, Lambdasonde vor Katalysator: Initialisierungsfehler |
| 0x2D06 | 0x2D06 DME, interner Fehler, Lambdasonde vor Katalysator: Kommunikationsfehler |
| 0x2D0B | 0x2D0B Lambdasondenbeheizung vor Katalysator, Ansteuerung: Kurzschluss nach Plus |
| 0x2D0C | 0x2D0C Lambdasondenbeheizung vor Katalysator, Ansteuerung: Kurzschluss nach Masse |
| 0x2D0D | 0x2D0D Lambdasondenbeheizung vor Katalysator, Ansteuerung: Leitungsunterbrechung |
| 0x2D0F | 0x2D0F Lambdasondenbeheizung nach Katalysator, Ansteuerung: Kurzschluss nach Plus |
| 0x2D10 | 0x2D10 Lambdasondenbeheizung nach Katalysator, Ansteuerung: Kurzschluss nach Masse |
| 0x2D11 | 0x2D11 Lambdasondenbeheizung nach Katalysator, Ansteuerung: Leitungsunterbrechung |
| 0x2D13 | 0x2D13 Lambdasondenbeheizung nach Katalysator, Funktion: Innenwiderstand zu hoch |
| 0x2D15 | 0x2D15 Lambdasonde nach Katalysator, im Schub, von Fett nach Mager: verzögerte Reaktion |
| 0x2D17 | 0x2D17 Lambdasondenbeheizung vor Katalysator, Funktion: Betriebstemperatur nicht erreicht |
| 0x2D18 | 0x2D18 Lambdasondenbeheizung vor Katalysator, Funktion: Mangelnde Signalbereitschaft |
| 0x2D19 | 0x2D19 Lambdasondenbeheizung vor Katalysator, Funktion: Innenwiderstand des Signalkreises zu hochohmig |
| 0x2D1B | 0x2D1B Lambdasonde nach Katalysator, Systemprüfung: Signal festliegend auf Mager |
| 0x2D1C | 0x2D1C Lambdasonde nach Katalysator, Systemprüfung: Signal festliegend auf Fett |
| 0x2D1E | 0x2D1E Lambdasonde nach Katalysator, Alterung: Schubspannungsschwelle nicht erreicht |
| 0x2D1F | 0x2D1F Lambdasonde nach Katalysator, elektrisch: Kurzschluss nach Plus |
| 0x2D20 | 0x2D20 Lambdasonde nach Katalysator, elektrisch: Kurzschluss nach Masse |
| 0x2D22 | 0x2D22 Lambdasonde nach Katalysator, elektrisch: Leitungsunterbrechung |
| 0x2D23 | 0x2D23 Lambdasonde vor Katalysator, elektrisch: Unterbrechung Pumpstromleitung |
| 0x2D24 | 0x2D24 Lambdasonde vor Katalysator, im Schub: Signal außerhalb Grenzwert |
| 0x2D25 | 0x2D25 Lambdasonde vor Katalysator, elektrisch: Unterbrechung Pumpstromleitung |
| 0x2D27 | 0x2D27 Lambdasonde vor Katalysator, elektrisch: Unterbrechung virtuelle Masse |
| 0x2D2B | 0x2D2B Lambdasonde vor Katalysator, elektrisch: Nernstzellenwiderstand oder Keramiktemperatur unplausibel, Leitungs- oder Heizungsfehler |
| 0x2D2F | 0x2D2F Lambdasonde vor Katalysator: Sammelfehler |
| 0x2D33 | 0x2D33 Lambdasonde vor Katalysator, Systemprüfung: Signal festliegend auf Mager |
| 0x2D34 | 0x2D34 Lambdasonde vor Katalysator, Systemprüfung: Signal festliegend auf Fett |
| 0x2D35 | 0x2D35 Lambdasonde vor Katalysator, Systemprüfung: Signal festliegend auf Mager |
| 0x2D36 | 0x2D36 Lambdasonde vor Katalysator, Systemprüfung: Signal festliegend auf Fett |
| 0x2D41 | 0x2D41 Valvetronic, Verstellbereich: Urlernen ausserhalb Toleranzen |
| 0x2D42 | 0x2D42 Valvetronic, Verstellbereich: Anschlag nicht gelernt |
| 0x2D43 | 0x2D43 Valvetronic, Verstellbereich: Fehler Bereichsüberprüfung |
| 0x2D44 | 0x2D44 Valvetronic, Verstellbereich: Bereichsüberprüfung Abweichung zu Urlernen |
| 0x2D45 | 0x2D45 Valvetronic, Verstellbereich: Anschlag nicht gelernt wegen Umweltbedingungen |
| 0x2D51 | 0x2D51 VANOS-Magnetventil Einlass, Ansteuerung: Kurzschluss nach Plus |
| 0x2D52 | 0x2D52 VANOS-Magnetventil Einlass, Ansteuerung: Kurzschluss nach Masse |
| 0x2D53 | 0x2D53 VANOS-Magnetventil Einlass, Ansteuerung: Leitungsunterbrechung |
| 0x2D54 | 0x2D54 VANOS, Auslass, Kaltstart: nicht regelbar |
| 0x2D55 | 0x2D55 VANOS, Einlass, Kaltstart: nicht regelbar |
| 0x2D5A | 0x2D5A VANOS, Einlass: Regelfehler, Nockenwelle klemmt |
| 0x2D5B | 0x2D5B VANOS, Einlass: Regelfehler, Position nicht erreicht |
| 0x2D60 | 0x2D60 VANOS, Auslass: Regelfehler, Nockenwelle klemmt |
| 0x2D61 | 0x2D61 VANOS, Auslass: Regelfehler, Position nicht erreicht |
| 0x2D9B | 0x2D9B VANOS-Magnetventil Auslass, Ansteuerung: Kurzschluss nach Plus |
| 0x2D9C | 0x2D9C VANOS-Magnetventil Auslass, Ansteuerung: Kurzschluss nach Masse |
| 0x2D9D | 0x2D9D VANOS-Magnetventil Auslass, Ansteuerung: Leitungsunterbrechung |
| 0x2D9F | 0x2D9F Einlassnockenwellensensor, Plausibilität: Signal unplausibel |
| 0x2DA0 | 0x2DA0 Einlassnockenwelle: Winkelversatz zur Kurbelwelle außerhalb Toleranz |
| 0x2DA1 | 0x2DA1 Auslassnockenwellensensor, Plausibilität: Signal unplausibel |
| 0x2DA2 | 0x2DA2 Auslassnockenwelle: Winkelversatz zur Kurbelwelle außerhalb Toleranz |
| 0x2DAD | 0x2DAD VANOS, Auslass: Sammelfehler |
| 0x2DAE | 0x2DAE VANOS, Einlass: Sammelfehler |
| 0x2DAF | 0x2DAF VANOS: Sammelfehler |
| 0x2DB0 | 0x2DB0 VANOS, Auslass: Nockenwelle beim Start nicht in Verriegelungsposition |
| 0x2DB1 | 0x2DB1 VANOS, Einlass: Nockenwelle beim Start nicht in Verriegelungsposition |
| 0x2DB4 | 0x2DB4 Valvetronic-Relais, Ansteuerung: Kurzschluss nach Plus |
| 0x2DB5 | 0x2DB5 Valvetronic-Relais, Ansteuerung: Kurzschluss nach Masse |
| 0x2DB6 | 0x2DB6 Valvetronic-Relais, Ansteuerung: Leitungsunterbrechung |
| 0x2DBA | 0x2DBA Valvetronic: Bauteileschutz, Abschaltung System |
| 0x2DBB | 0x2DBB Valvetronic-Stellmotor: Bauteileschutz, Abschaltung System |
| 0x2DBC | 0x2DBC Valvetronic, Exzenterwellenadaption: unterer Anschlag erreicht |
| 0x2DBD | 0x2DBD Valvetronic-Stellmotor, Positionssensoren: Exzenterwinkel falsch |
| 0x2DBF | 0x2DBF Valvetronic-Stellmotor, Ansteuerung: Kurzschluss nach Plus |
| 0x2DC0 | 0x2DC0 Valvetronic-Stellmotor, Ansteuerung: Kurzschluss nach Masse |
| 0x2DC3 | 0x2DC3 Valvetronic-Stellmotor, Ansteuerung: Leitungsunterbrechung |
| 0x2DC4 | 0x2DC4 Valvetronic-Stellmotor, Ansteuerung: Abschaltung im Fahrbetrieb |
| 0x2DCA | 0x2DCA Valvetronic: Endstufe überlastet |
| 0x2DCB | 0x2DCB Valvetronic-Stellmotor: Überlastung |
| 0x2DCC | 0x2DCC Valvetronic: Warnschwelle Überlastschutz überschritten |
| 0x2DCD | 0x2DCD Valvetronic-Stellmotor: Warnschwelle Überlastschutz überschritten |
| 0x2DCE | 0x2DCE Valvetronic System: keine Verstellung möglich |
| 0x2DCF | 0x2DCF Valvetronic System: keine Bewegung erkannt |
| 0x2DD0 | 0x2DD0 Valvetronic System: Warnschwelle Regelabweichung überschritten |
| 0x2DD6 | 0x2DD6 Valvetronic-Stellmotor, Positionssensoren: Kurzschluss oder Leitungsunterbrechung |
| 0x2DD7 | 0x2DD7 Valvetronic-Stellmotor, Positionssensoren: Versorgungsspannung fehlerhaft |
| 0x2DD8 | 0x2DD8 Valvetronic-Stellmotor, Positionssensoren: Signal unplausibel |
| 0x2DE1 | 0x2DE1 Valvetronic-Stellmotor, Positionssensoren, Plausibilität: Feinhallsignale zueinander unplausibel |
| 0x2DE2 | 0x2DE2 Valvetronic-Stellmotor, Ansteuerung Phase U: Leitungsunterbrechung |
| 0x2DE3 | 0x2DE3 Valvetronic-Stellmotor, Ansteuerung Phase V: Leitungsunterbrechung |
| 0x2DE4 | 0x2DE4 Valvetronic-Stellmotor, Ansteuerung Phase W: Leitungsunterbrechung |
| 0x2DE5 | 0x2DE5 Valvetronic-Stellmotor: Überlastung |
| 0x2DE6 | 0x2DE6 Valvetronic: Warnschwelle Überlastschutz überschritten |
| 0x2DE7 | 0x2DE7 Valvetronic-Stellmotor: Warnschwelle Überlastschutz überschritten |
| 0x2DE8 | 0x2DE8 Valvetronic: Bauteileschutz, Abschaltung System |
| 0x2DE9 | 0x2DE9 Valvetronic-Stellmotor: Bauteileschutz, Abschaltung System |
| 0x2DEA | 0x2DEA Valvetronic: Endstufe überlastet |
| 0x2E0A | 0x2E0A Valvetronic-Stellmotor, Ansteuerung Phase U: Leitungsunterbrechung |
| 0x2E0B | 0x2E0B Valvetronic-Stellmotor, Ansteuerung Phase V: Leitungsunterbrechung |
| 0x2E0C | 0x2E0C Valvetronic-Stellmotor, Ansteuerung Phase W: Leitungsunterbrechung |
| 0x2E0D | 0x2E0D Valvetronic-Stellmotor, Positionssensoren: Fehler erkannt |
| 0x2E0E | 0x2E0E Valvetronic-Stellmotor, Positionssensoren: Signale unplausibel |
| 0x2E0F | 0x2E0F Valvetronic System: deaktiviert, zu häufiger Verstellfehler |
| 0x2E10 | 0x2E10 Valvetronic System: deaktiviert, Warnschwelle Regelabweichung zu oft überschritten |
| 0x2E11 | 0x2E11 Valvetronic System: unterer Anschlag gelernt |
| 0x2E12 | 0x2E12 Valvetronic System: keine Verstellung möglich |
| 0x2E13 | 0x2E13 Valvetronic System: Warnschwelle Regelabweichung überschritten |
| 0x2E4A | 0x2E4A Abgasklappe, Ansteuerung: Kurzschluss nach Plus |
| 0x2E4B | 0x2E4B Abgasklappe, Ansteuerung: Kurzschluss nach Masse |
| 0x2E4C | 0x2E4C Abgasklappe, Ansteuerung: Leitungsunterbrechung |
| 0x2E7C | 0x2E7C Kühlerjalousie, oben, Eigendiagnose: Hardwaredefekt |
| 0x2E7D | 0x2E7D Kühlerjalousie, oben, Eigendiagnose: mechanischer Fehler |
| 0x2E7E | 0x2E7E Kühlerjalousie, oben, Eigendiagnose: Kommunikationsfehler |
| 0x2E80 | 0x2E80 Kühlerjalousie, Ansteuerung: Kurzschluss nach Plus |
| 0x2E81 | 0x2E81 Kühlerjalousie, Ansteuerung: Kurzschluss nach Masse |
| 0x2E82 | 0x2E82 Kühlerjalousie, Ansteuerung: Leitungsunterbrechung |
| 0x2E84 | 0x2E84 Kühlerjalousie, unten, Eigendiagnose, elektrisch: Fehlfunktion |
| 0x2EE0 | 0x2EE0 Verbrennungsaussetzer, mehrere Zylinder: Einspritzabschaltung |
| 0x2EE1 | 0x2EE1 Verbrennungsaussetzer, mehrere Zylinder: abgasschädigend |
| 0x2EE2 | 0x2EE2 Verbrennungsaussetzer, mehrere Zylinder: abgasschädigend nach Startvorgang |
| 0x2EE4 | 0x2EE4 Verbrennungsaussetzer, Zylinder 1: Einspritzabschaltung |
| 0x2EE5 | 0x2EE5 Verbrennungsaussetzer, Zylinder 1: abgasschädigend |
| 0x2EE6 | 0x2EE6 Verbrennungsaussetzer, Zylinder 1: abgasschädigend nach Startvorgang |
| 0x2EE7 | 0x2EE7 Verbrennungsaussetzer, Zylinder 2: Einspritzabschaltung |
| 0x2EE8 | 0x2EE8 Verbrennungsaussetzer, Zylinder 2: abgasschädigend |
| 0x2EE9 | 0x2EE9 Verbrennungsaussetzer, Zylinder 2: abgasschädigend nach Startvorgang |
| 0x2EEA | 0x2EEA Verbrennungsaussetzer, Zylinder 3: Einspritzabschaltung |
| 0x2EEB | 0x2EEB Verbrennungsaussetzer, Zylinder 3: abgasschädigend |
| 0x2EEC | 0x2EEC Verbrennungsaussetzer, Zylinder 3: abgasschädigend nach Startvorgang |
| 0x2EED | 0x2EED Verbrennungsaussetzer, Zylinder 4: Einspritzabschaltung |
| 0x2EEF | 0x2EEF Verbrennungsaussetzer, Zylinder 4: abgasschädigend |
| 0x2EF0 | 0x2EF0 Verbrennungsaussetzer, Zylinder 4: abgasschädigend nach Startvorgang |
| 0x2EF1 | 0x2EF1 Verbrennungsaussetzer, Zylinder 5: Einspritzabschaltung |
| 0x2EF2 | 0x2EF2 Verbrennungsaussetzer, Zylinder 5: abgasschädigend |
| 0x2EF3 | 0x2EF3 Verbrennungsaussetzer, Zylinder 5: abgasschädigend nach Startvorgang |
| 0x2EF4 | 0x2EF4 Verbrennungsaussetzer, Zylinder 6: Einspritzabschaltung |
| 0x2EF5 | 0x2EF5 Verbrennungsaussetzer, Zylinder 6: abgasschädigend |
| 0x2EF6 | 0x2EF6 Verbrennungsaussetzer, Zylinder 6: abgasschädigend nach Startvorgang |
| 0x2EFE | 0x2EFE Verbrennungsaussetzer, mehrere Zylinder: katalysator- oder abgasschädigend |
| 0x2EFF | 0x2EFF Verbrennungsaussetzer, Zylinder 1: katalysator- oder abgasschädigend |
| 0x2F00 | 0x2F00 Verbrennungsaussetzer, Zylinder 2: katalysator- oder abgasschädigend |
| 0x2F01 | 0x2F01 Verbrennungsaussetzer, Zylinder 3: katalysator- oder abgasschädigend |
| 0x2F02 | 0x2F02 Verbrennungsaussetzer, Zylinder 4: katalysator- oder abgasschädigend |
| 0x2F03 | 0x2F03 Verbrennungsaussetzer, Zylinder 5: katalysator- oder abgasschädigend |
| 0x2F04 | 0x2F04 Verbrennungsaussetzer, Zylinder 6: katalysator- oder abgasschädigend |
| 0x2F44 | 0x2F44 Zündkreis, Versorgungsspannung: Bankausfall oder Motorausfall |
| 0x2F45 | 0x2F45 Laufunruhe, Füllung Einzelzylinder: Momentenbeitrag zu niedrig |
| 0x2F76 | 0x2F76 Superklopfen Zylinder 1: Einspritzungsabschaltung |
| 0x2F77 | 0x2F77 Superklopfen Zylinder 2: Einspritzungsabschaltung |
| 0x2F78 | 0x2F78 Superklopfen Zylinder 3: Einspritzungsabschaltung |
| 0x2F79 | 0x2F79 Superklopfen Zylinder 4: Einspritzungsabschaltung |
| 0x2F7A | 0x2F7A Superklopfen Zylinder 5: Einspritzungsabschaltung |
| 0x2F7B | 0x2F7B Superklopfen Zylinder 6: Einspritzungsabschaltung |
| 0x2F7C | 0x2F7C Superklopfen: Einspritzungsabschaltung |
| 0x2F83 | 0x2F83 Zündwinkelverstellung im Leerlauf, Kaltstart: Zündwinkel zu früh |
| 0x2F84 | 0x2F84 Zündwinkelverstellung in Teillast, Kaltstart: Zündwinkel zu früh |
| 0x2F8A | 0x2F8A Relais Zündung und Injektoren, Versorgungsspannung Zündung: Kurzschluss nach Plus |
| 0x2F8B | 0x2F8B Relais Zündung und Injektoren, Versorgungsspannung Zündung: Kurzschluss nach Masse |
| 0x2FA8 | 0x2FA8 Zündung, Zylinder 1: Brenndauer zu kurz |
| 0x2FA9 | 0x2FA9 Zündung, Zylinder 2: Brenndauer zu kurz |
| 0x2FAA | 0x2FAA Zündung, Zylinder 3: Brenndauer zu kurz |
| 0x2FAB | 0x2FAB Zündung, Zylinder 4: Brenndauer zu kurz |
| 0x2FAC | 0x2FAC Zündung, Zylinder 5: Brenndauer zu kurz |
| 0x2FAD | 0x2FAD Zündung, Zylinder 6: Brenndauer zu kurz |
| 0x2FDA | 0x2FDA Kurbelwellensensor, Signal: fehlt |
| 0x2FDB | 0x2FDB Kurbelwellensensor, Signal: unplausibel |
| 0x2FDD | 0x2FDD Kurbelwellensensor, Plausibilität: Drehrichtung unplausibel |
| 0x300C | 0x300C Einlassnockenwellensensor, elektrisch: Kurzschluss nach Plus |
| 0x300D | 0x300D Einlassnockenwellensensor, elektrisch: Kurzschluss nach Masse |
| 0x300E | 0x300E Auslassnockenwellensensor, elektrisch: Kurzschluss nach Plus |
| 0x300F | 0x300F Ausassnockenwellensensor, elektrisch: Kurzschluss nach Masse |
| 0x3011 | 0x3011 Einlassnockenwelle: Montage fehlerhaft |
| 0x3012 | 0x3012 Auslassnockenwelle: Montage fehlerhaft |
| 0x303E | 0x303E Klopfregelung: Systemfehler |
| 0x303F | 0x303F Klopfsensor, elektrisch: Signal-Eingang A, Kurzschluss nach Plus |
| 0x3040 | 0x3040 Klopfsensor, elektrisch: Signal-Eingang A, Kurzschluss nach Masse |
| 0x3041 | 0x3041 Klopfsensor, elektrisch: Signal-Eingang B, Kurzschluss nach Plus |
| 0x3042 | 0x3042 Klopfsensor, elektrisch: Signal-Eingang B, Kurzschluss nach Masse |
| 0x3043 | 0x3043 Klopfsensor 2, elektrisch: Signal-Eingang A, Kurzschluss nach Plus |
| 0x3044 | 0x3044 Klopfsensor 2, elektrisch: Signal-Eingang A, Kurzschluss nach Masse |
| 0x3045 | 0x3045 Klopfsensor 2, elektrisch: Signal-Eingang B, Kurzschluss nach Plus |
| 0x3046 | 0x3046 Klopfsensor 2, elektrisch: Signal-Eingang B, Kurzschluss nach Masse |
| 0x3048 | 0x3048 Klopfsensor 1, Signal: Motorgeräusch über Grenzwert |
| 0x3049 | 0x3049 Klopfsensor 1, Signal: Motorgeräusch unter Grenzwert oder Leitungsunterbrechung |
| 0x304C | 0x304C Klopfsensor 2, Signal: Motorgeräusch über Grenzwert |
| 0x304D | 0x304D Klopfsensor 2, Signal: Motorgeräusch unter Grenzwert oder Leitungsunterbrechung |
| 0x3106 | 0x3106 Katalysator: Wirkungsgrad unterhalb Grenzwert |
| 0x3139 | 0x3139 DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Plus |
| 0x313A | 0x313A DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Masse |
| 0x313B | 0x313B DMTL-Magnetventil, Ansteuerung: Leitungsunterbrechung |
| 0x3140 | 0x3140 Tankentlüftungs- und Spülluftsystem, Feinleck: Leckage größer 1, 0 mm |
| 0x3141 | 0x3141 Tankentlüftungs- und Spülluftsystem, Feinstleck: Leckage größer 0, 5 mm |
| 0x3142 | 0x3142 DMTL, Systemfehler: Pumpenstrom zu groß bei Referenzmessung |
| 0x3143 | 0x3143 DMTL, Systemfehler: Pumpenstrom zu klein bei Referenzmessung |
| 0x3144 | 0x3144 DMTL, Systemfehler: Abbruch wegen Stromschwankungen bei Referenzmessung |
| 0x3145 | 0x3145 DMTL, Systemfehler: Pumpenstrom bei Ventilprüfung erreicht Grenzwert |
| 0x3146 | 0x3146 DMTL, Heizung, Ansteuerung: Kurzschluss nach Plus |
| 0x3147 | 0x3147 DMTL, Heizung, Ansteuerung: Kurzschluss nach Masse |
| 0x3148 | 0x3148 DMTL, Heizung, Ansteuerung: Leitungsunterbrechung |
| 0x314A | 0x314A DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Plus |
| 0x314B | 0x314B DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Masse |
| 0x314C | 0x314C DMTL-Leckdiagnosepumpe, Ansteuerung: Leitungsunterbrechung |
| 0x3155 | 0x3155 Tankentlüftungsventil, Ansteuerung: Kurzschluss nach Plus |
| 0x3156 | 0x3156 Tankentlüftungsventil, Ansteuerung: Kurzschluss nach Masse |
| 0x3157 | 0x3157 Tankentlüftungsventil, Ansteuerung: Leitungsunterbrechung |
| 0x3159 | 0x3159 Tankentlüftungsventil: klemmt geschlossen |
| 0x315A | 0x315A Tankentlüftungsventil: klemmt offen |
| 0x3160 | 0x3160 Tankentlüftungssystem Absperrventil, Ansteuerung: Kurzschluss nach Plus |
| 0x3161 | 0x3161 Tankentlüftungssystem Absperrventil, Ansteuerung: Kurzschluss nach Masse |
| 0x3162 | 0x3162 Tankentlüftungssystem Absperrventil, Ansteuerung: Leitungsunterbrechung |
| 0x3163 | 0x3163 Tankentlüftungssystem Absperrventil: klemmt offen |
| 0x3164 | 0x3164 Tankentlüftungssystem, 2. Einleitestelle: Fehlfunktion |
| 0x3165 | 0x3165 Tankentlüftungssystem, Nachlauf: Fehlfunktion |
| 0x3166 | 0x3166 Tankentlüftungssystem: Fehlfunktion |
| 0x316A | 0x316A Tankdeckel: nicht korrekt geschlossen |
| 0x316B | 0x316B Tankdeckel: offen im Nachlauf |
| 0x3183 | 0x3183 Tankfüllstandssensor, rechts, Signal: Kurzschluss nach Plus |
| 0x3184 | 0x3184 Tankfüllstandssensor, rechts, Signal: Kurzschluss nach Masse |
| 0x3185 | 0x3185 Tankfüllstandssensor, rechts, Signal: CAN Wert unplausibel |
| 0x3187 | 0x3187 Tankfüllstandssensor, links, Signal: Kurzschluss nach Plus |
| 0x3188 | 0x3188 Tankfüllstandssensor, links, Signal: Kurzschluss nach Masse |
| 0x3189 | 0x3189 Tankfüllstandssensor, links, Signal: Tankfüllstandsignal unplausibel zu hoch |
| 0x318A | 0x318A Tankfüllstandssensor, links, Signal: CAN Wert unplausibel |
| 0x318B | 0x318B Tankfüllstandssensor: Signal unplausibel wegen festhängendem Tankfüllstandsgeber |
| 0x318C | 0x318C Tankfüllstandssensor: Tankfüllstand größer als Tankvolumen |
| 0x318D | 0x318D Tankfüllstandssensor: Abweichung zwischen Verbrauch und Füllstandsänderung |
| 0x318F | 0x318F Tankfüllstand, Sammelfehler: Signal und elektrisch |
| 0x31E7 | 0x31E7 Elektrolüfter, Ansteuerungleitung: Kurzschluss nach Plus |
| 0x31E8 | 0x31E8 Elektrolüfter, Ansteuerungleitung: Kurzschluss nach Masse |
| 0x31E9 | 0x31E9 Elektrolüfter, Ansteuerungleitung: Leitungsunterbrechung |
| 0x31EA | 0x31EA Elektrolüfter, Eigendiagnose: Mechanischer- oder Hardwaredefekt |
| 0x3219 | 0x3219 DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Plus |
| 0x321A | 0x321A DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Masse |
| 0x321B | 0x321B DMTL-Magnetventil, Ansteuerung: Leitungsunterbrechung |
| 0x321C | 0x321C Tankentlüftungs- und Spülluftsystem, Feinleck: Leckage größer 1,0 mm |
| 0x321D | 0x321D Tankentlüftungs- und Spülluftsystem, Feinstleck: Leckage größer 0,5 mm |
| 0x321E | 0x321E DMTL, Systemfehler: Pumpenstrom zu groß bei Referenzmessung |
| 0x321F | 0x321F DMTL, Systemfehler: Pumpenstrom zu klein bei Referenzmessung |
| 0x3220 | 0x3220 DMTL, Systemfehler: Abbruch wegen Stromschwankungen bei Referenzmessung |
| 0x3221 | 0x3221 DMTL, Systemfehler: Pumpenstrom bei Ventilprüfung erreicht Grenzwert |
| 0x3222 | 0x3222 DMTL, Heizung, Ansteuerung: Kurzschluss nach Plus |
| 0x3223 | 0x3223 DMTL, Heizung, Ansteuerung: Kurzschluss nach Masse |
| 0x3224 | 0x3224 DMTL, Heizung, Ansteuerung: Leitungsunterbrechung |
| 0x3225 | 0x3225 DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Plus |
| 0x3226 | 0x3226 DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Masse |
| 0x3227 | 0x3227 DMTL-Leckdiagnosepumpe, Ansteuerung: Leitungsunterbrechung |
| 0x3228 | 0x3228 Tankentlüftungssystem, 2. Einleitestelle, Nachlauf: Fehlfunktion |
| 0x32AB | 0x32AB FA-CAN, Botschaft (EWS Dienst DME1/DDE1, 0x5C0): Framefehler |
| 0x32C8 | 0x32C8 Schlechtwegstreckenerkennung: Radgeschwindigkeit zu hoch |
| 0x32C9 | 0x32C9 Schlechtwegstreckenerkennung: Kein Raddrehzahlsignal erhalten |
| 0x32CC | 0x32CC Fahrzeuggeschwindigkeit, Plausibilität: Kombi hat Ungültigkeitssignal gesendet |
| 0x32CD | 0x32CD Fahrzeuggeschwindigkeit, Plausibilität: DSC-Signal unplausibel gegenüber Kombi-Anzeige |
| 0x32D0 | 0x32D0 Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeit zu hoch |
| 0x32D4 | 0x32D4 Fahrzeuggeschwindigkeit: Sammelfehler |
| 0x32D8 | 0x32D8 Fahrzeuggeschwindigkeit, Plausibilität: Mindestgeschwindigkeit unter Last unplausibel |
| 0x32D9 | 0x32D9 Fahrzeuggeschwindigkeit, Plausibilität: Mindestgeschwindigkeit im Schub unplausibel |
| 0x32DA | 0x32DA Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeitssignal unplausibel |
| 0x32DC | 0x32DC Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, Signaländerung: unplausibel |
| 0x32DD | 0x32DD Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, Signaländerung: unplausibel |
| 0x32DE | 0x32DE Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, Signaländerung: unplausibel |
| 0x32DF | 0x32DF Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, Signaländerung: unplausibel |
| 0x32E1 | 0x32E1 EWS Manipulationsschutz: kein Startwert programmiert |
| 0x32E2 | 0x32E2 EWS Manipulationsschutz: Antwort unplausibel |
| 0x32E3 | 0x32E3 Schnittstelle EWS-DME: Hardwarefehler |
| 0x32E4 | 0x32E4 Schnittstelle EWS-DME: Framefehler |
| 0x32E5 | 0x32E5 Schnittstelle EWS-DME: Zeitüberschreitung |
| 0x32E6 | 0x32E6 Schnittstelle EWS-DME: Empfangsfehler CAS Schnittstelle |
| 0x32E7 | 0x32E7 DME, interner Fehler, EWS-Daten: keine verfügbare Speichermöglichkeit |
| 0x32E8 | 0x32E8 DME, interner Fehler, EWS-Daten: Fehlerfreischaltcodeablage |
| 0x32E9 | 0x32E9 DME, interner Fehler, EWS-Daten: Prüfsummenfehler |
| 0x32EA | 0x32EA DME, interner Fehler, EWS-Daten: Schreibfehler Secret Key |
| 0x32EC | 0x32EC FA-CAN, Botschaft (EWS Dienst DME1/DDE1, 0x5C0): fehlt |
| 0x3325 | 0x3325 Bremslichtschalter, Plausibilität: Signal unplausibel |
| 0x332C | 0x332C Klemme 15_3, Leitung vom CAS, elektrisch: Kurzschluss nach Masse |
| 0x332D | 0x332D Klemme 15_3, Leitung vom CAS, elektrisch: Kurzschluss nach Plus |
| 0x332E | 0x332E Klemme 87_1: keine Spannung |
| 0x332F | 0x332F Klemme 87_2: keine Spannung |
| 0x3330 | 0x3330 Klemme 87_3: keine Spannung |
| 0x335B | 0x335B Bremsunterdrucksensor, Plausibilität: Differenzdruck zu niedrig |
| 0x335C | 0x335C Bremsunterdrucksensor, elektrisch: Kurzschluss nach Plus |
| 0x335D | 0x335D Bremsunterdrucksensor, elektrisch: Kurzschluss nach Masse |
| 0x3392 | 0x3392 Motorabstellzeit, Plausibilität: Zeit zu kurz in Korrelation zu Motorkühlmittel-Abkühlung |
| 0x3393 | 0x3393 Motorabstellzeit, Plausibilität: Zeit zu lang in Korrelation zu Motorkühlmittel-Abkühlung |
| 0x3394 | 0x3394 Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi zu hoch im Motorlauf |
| 0x3395 | 0x3395 Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi zu niedrig im Motorlauf |
| 0x3396 | 0x3396 Motorabstellzeit, Signal: fehlt |
| 0x3398 | 0x3398 Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi zu hoch im Nachlauf |
| 0x3399 | 0x3399 Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi zu niedrig im Nachlauf |
| 0x33DB | 0x33DB Nullgangsensor, Adaption: nicht gelernt (MSA deaktiviert) |
| 0x33DC | 0x33DC Nullgangsensor, Plausibilität: Signal unplausibel |
| 0x33DD | 0x33DD Nullgangsensor, Signal: Tastverhältnis zu hoch |
| 0x33DE | 0x33DE Nullgangsensor, Signal: Tastverhältnis zu niedrig |
| 0x33DF | 0x33DF Nullgangsensor, elektrisch: Kurzschluss nach Plus oder Leitungsunterbrechung |
| 0x33E0 | 0x33E0 Nullgangsensor, elektrisch: Kurzschluss nach Masse |
| 0x33E1 | 0x33E1 Nullgangsensor, Plausibilität: Periodendauer außerhalb gültigem Bereich |
| 0x33FC | 0x33FC Motoröldruckregelung, Plausibilität: Druckschwankungen |
| 0x33FD | 0x33FD Motoröldruckregelung, Plausibilität, statisch: Druck zu hoch |
| 0x33FE | 0x33FE Motoröldruckregelung, Plausibilität, statisch: Druck zu niedrig |
| 0x33FF | 0x33FF Motoröldruckregelventil, Ansteuerung: Kurzschluss nach Plus |
| 0x3400 | 0x3400 Motoröldruckregelventil, Ansteuerung: Kurzschluss nach Masse |
| 0x3401 | 0x3401 Motoröldruckregelventil, Ansteuerung: Leitungsunterbrechung |
| 0x3404 | 0x3404 Motoröldruckregelung: instabil |
| 0x3405 | 0x3405 Motorölpumpe: Druck zu hoch |
| 0x3406 | 0x3406 Motorölpumpe: Druck zu niedrig |
| 0x3408 | 0x3408 Motoröldruckregelventil: klemmt in voll bestromter Stellung (minimaler Öldruck) |
| 0x3409 | 0x3409 Motoröldruckregelventil: klemmt in unbestromter Stellung (maximaler Öldruck) |
| 0x3426 | 0x3426 Motoröldrucksensor, elektrisch: Kurzschluss nach Plus |
| 0x3427 | 0x3427 Motoröldrucksensor, elektrisch: Kurzschluss nach Masse |
| 0x3429 | 0x3429 Motoröldrucksensor, Plausibilität: Druck vor Motorstart zu hoch |
| 0x342A | 0x342A Motoröldrucksensor, Plausibilität: Druck vor Motorstart zu niedrig |
| 0x342B | 0x342B Motoröldrucksensor, Signal: festliegend |
| 0x343F | 0x343F Ölzustand, Status Niveau: Fehlfunktion |
| 0x3440 | 0x3440 Ölzustandssensor, Status Temperatur: Fehlfunktion |
| 0x3441 | 0x3441 Ölzustandssensor, elektrisch: Permittivität Fehlfunktion |
| 0x3442 | 0x3442 Ölzustandssensor, Plausibilität: Niveau unplausibel |
| 0x3443 | 0x3443 Ölzustandssensor, Plausibilität: Temperatur unplausibel |
| 0x3444 | 0x3444 Ölzustandssensor, Plausibilität: Permittivität unplausibel |
| 0x3446 | 0x3446 BSD, Kommunikation (Ölzustandssensor): fehlt |
| 0x3447 | 0x3447 Motorölniveau: zu niedrig |
| 0x3449 | 0x3449 Ölzustandssensor: Fehlfunktion |
| 0x344A | 0x344A Ölzustandssensor, Plausibilität: Niveau unplausibel |
| 0x344B | 0x344B Ölzustandssensor, Plausibilität: Temperatur unplausibel |
| 0x344C | 0x344C Motoröltemperatursensor, elektrisch: Fehlfunktion |
| 0x344D | 0x344D Motoröltemperatursensor, Plausibilität: Temperatur unplausibel |
| 0x344E | 0x344E Ölzustandssensor: Signal fehlt |
| 0x344F | 0x344F Ölzustandssensor: Signal unplausibel |
| 0x348A | 0x348A Kennfeldthermostat: klemmt offen |
| 0x348E | 0x348E Kennfeldthermostat, Ansteuerung: Kurzschluss nach Plus |
| 0x348F | 0x348F Kennfeldthermostat, Ansteuerung: Kurzschluss nach Masse |
| 0x3490 | 0x3490 Kennfeldthermostat, Ansteuerung: Leitungsunterbrechung |
| 0x34A3 | 0x34A3 Kupplungsschalter, Plausibilität: Signal unplausibel |
| 0x34A5 | 0x34A5 Kupplungsschalter: Positionen zueinander unplausibel |
| 0x34A8 | 0x34A8 Kupplungstemperatur: Warnschwellenwert 1 ohne Schädigung überschritten |
| 0x34A9 | 0x34A9 Kupplungstemperatur: Warnschwellenwert 2 ohne Schädigung überschritten |
| 0x34AD | 0x34AD Kupplung, Plausibilität: Übertragbares Moment zu niedrig, Kupplung leicht geschädigt |
| 0x34AE | 0x34AE Kupplung, Plausibilität: Übertragbares Moment zu niedrig, Kupplung geschädigt |
| 0x34AF | 0x34AF Kupplung, Plausibilität: Übertragbares Moment zu niedrig, Kupplung stark geschädigt |
| 0x3520 | 0x3520 Leerlaufregelung: Drehzahl zu hoch |
| 0x3521 | 0x3521 Leerlaufregelung: Drehzahl zu niedrig |
| 0x3524 | 0x3524 Leerlaufregelung, Kaltstart: Drehzahl zu hoch |
| 0x3525 | 0x3525 Leerlaufregelung, Kaltstart: Drehzahl zu niedrig |
| 0x3528 | 0x3528 Antrieb, Sicherheitsfunktion: Leistungsreduzierung durch Sicherheitskonzept |
| 0x3529 | 0x3529 Drehzahlbegrenzung bei stehendem Fahrzeug: Leerlaufdrehzahl zu lange zu hoch |
| 0x352A | 0x352A Manipulationsschutz: Motorleistung zu hoch |
| 0x3584 | 0x3584 DME, interner Fehler, Innentemperatursensor: Wert zu hoch |
| 0x3585 | 0x3585 DME, interner Fehler, Innentemperatursensor: Wert zu niedrig |
| 0x3586 | 0x3586 DME Temperatur: Übertemperatur |
| 0x36B0 | 0x36B0 DME, interner Fehler, Ansteuerung Valvetronic: Fehlfunktion |
| 0x36B1 | 0x36B1 DME, interner Fehler, Überwachung 5V-Versorgung 2: Überspannung erkannt |
| 0x36B2 | 0x36B2 DME, interner Fehler, Überwachung 5V-Versorgung 2: Unterspannung erkannt |
| 0x36B4 | 0x36B4 DME, interner Fehler: Überwachung SPI-Kommunikation |
| 0x36B5 | 0x36B5 DME, interner Fehler: Löschen EEPROM fehlerhaft |
| 0x36B6 | 0x36B6 DME, interner Fehler: Lesen EEPROM fehlerhaft |
| 0x36B7 | 0x36B7 DME, interner Fehler: Schreiben EEPROM fehlerhaft |
| 0x36B8 | 0x36B8 DME, interner Fehler: Überwachungsmodulfehler |
| 0x36B9 | 0x36B9 DME, interner Fehler, Überwachung 5V-Versorgung: Überspannung erkannt |
| 0x36BA | 0x36BA DME, interner Fehler, Überwachung 5V-Versorgung: Unterspannung erkannt |
| 0x36BB | 0x36BB DME, interner Fehler, Watchdog-Ausgang: Fehlfunktion |
| 0x36BC | 0x36BC DME, interner Fehler, Watchdog-Ausgang: fehlerhafte Frage-/Antwort-Kommunikation |
| 0x36BD | 0x36BD DME, interner Fehler, Watchdog-Ausgang: Überspannungserkennung |
| 0x36BE | 0x36BE DME, Kodierung: fehlt oder Fahrgestellnummer falsch |
| 0x36BF | 0x36BF DME, interner Fehler, MSA-Überwachung: fehlerhafte Berechnung |
| 0x36C0 | 0x36C0 Antrieb, Sicherheitsfunktion: AD-Wandler Leerlauftestimpulsprüfung |
| 0x36C1 | 0x36C1 Antrieb, Sicherheitsfunktion: AD-Wandler Testspannungsprüfung |
| 0x36C2 | 0x36C2 DME, interner Fehler, Sicherheitsfunktion: Luftmengenabgleich |
| 0x36C3 | 0x36C3 Antrieb, Sicherheitsfunktion: Fahrpedalmodul oder Pedalwertgeber unplausibel |
| 0x36C4 | 0x36C4 Antrieb, Sicherheitsfunktion: Drehzahlgeber unplausibel |
| 0x36C5 | 0x36C5 DME, interner Fehler, Sicherheitsfunktion: Plausibilisierung der Gemischkorrekturfaktoren |
| 0x36C6 | 0x36C6 DME, interner Fehler, Sicherheitsfunktion: Einspritzmengenbegrenzung Ebene 1 |
| 0x36C7 | 0x36C7 Antrieb, Sicherheitsfunktion: Sicherheitsabschaltung Einspritzung |
| 0x36C8 | 0x36C8 DME, interner Fehler, Sicherheitsfunktion: Lambda-Sollwert |
| 0x36C9 | 0x36C9 DME, interner Fehler, Sicherheitsfunktion: Plausibilisierung relative Kraftstoffmasse |
| 0x36CA | 0x36CA DME, interner Fehler, Sicherheitsfunktion: Momentenvergleich |
| 0x36CB | 0x36CB DME, interner Fehler, Sicherheitsfunktion: Antriebstrangübersetzungsverhältnis unplausibel |
| 0x36CC | 0x36CC Antrieb, Sicherheitsfunktion: Getriebevariante unplausibel |
| 0x36CD | 0x36CD DME, interner Fehler, Sicherheitsfunktion: Zündwinkelüberwachung |
| 0x36CE | 0x36CE Antrieb, Sicherheitsfunktion: Abschaltpfad-Test negativ |
| 0x36CF | 0x36CF DME, interner Fehler, Sicherheitsfunktion: Plausiblisierung Kraftstoffmasse |
| 0x36D0 | 0x36D0 DME, interner Fehler, Überwachung MSC-Kommunikation: Fehlfunktion an Baustein R2S2/1 |
| 0x36D2 | 0x36D2 DME, interner Fehler, Überwachung MSC-Kommunikation: Fehlfunktion an Baustein R2S2/2 |
| 0x36D4 | 0x36D4 DME, interner Fehler, Ansteuerung Valvetronic: Fehlfunktion |
| 0x36E2 | 0x36E2 Überwachung 5V Sensor-Versorgung: Spannung außerhalb gültigem Bereich |
| 0x36E3 | 0x36E3 Überwachung 5V Sensor-Versorgung 2: Spannung außerhalb gültigem Bereich |
| 0x36E4 | 0x36E4 Überwachung 5V Sensor-Versorgung 3: Spannung außerhalb gültigem Bereich |
| 0x36E5 | 0x36E5 DME, interner Fehler: Software-Reset |
| 0x36E6 | 0x36E6 DME, interner Fehler: Software-Reset |
| 0x36E7 | 0x36E7 DME, interner Fehler: Software-Reset |
| 0x36FA | 0x36FA Startaggregat Ritzelstarter, Ansteuerung: Kurzschluss nach Plus |
| 0x36FB | 0x36FB Startaggregat Ritzelstarter, Ansteuerung: Kurzschluss nach Masse |
| 0x36FC | 0x36FC Startaggregat Ritzelstarter, Ansteuerung: Leitungsunterbrechung |
| 0x36FD | 0x36FD DME-Hauptrelais, Plausibilität: vorzeitig abgefallen |
| 0x36FE | 0x36FE DME-Hauptrelais, Ansteuerung: Kurzschluss nach Masse |
| 0x36FF | 0x36FF DME-Hauptrelais: nicht abgefallen |
| 0x3714 | 0x3714 Bordnetzspannung, DME-Hauptrelais, Arbeitsbereich: Spannung zu hoch |
| 0x3719 | 0x3719 Valvetronic, Versorgungsspannung: Kurzschluss nach Masse |
| 0x371A | 0x371A Valvetronic, Versorgungsspannung: Leitungsunterbrechung |
| 0x371B | 0x371B Relais Zündung und Injektoren, Ansteuerung: Kurzschluss nach Masse |
| 0x371C | 0x371C Relais Zündung und Injektoren, Ansteuerung: Kurzschluss nach Plus |
| 0x371E | 0x371E Relais Zündung und Injektoren, Ansteuerung: Leitungsunterbrechung |
| 0x375A | 0x375A CBS-Client: Ausgabe von Ersatzwert |
| 0x375B | 0x375B CBS-Client: Verfügbarkeitssprung |
| 0x375C | 0x375C DME, Manipulationsschutz: Programm oder Datenmanipulation erkannt |
| 0x375F | 0x375F DME, falscher Datensatz: FA-CAN, Botschaft (Fahrzeugtyp, 0x388): fehlt |
| 0x3760 | 0x3760 DME, falscher Datensatz: Variantenüberwachung |
| 0x3761 | 0x3761 Funktionsfreischaltung, Leistungserhöhung: nicht erfolgt |
| 0x3778 | 0x3778 Motor-Kühlsystem: Abschaltung Kühlmittelpumpe wegen Übertemperatur |
| 0x3779 | 0x3779 Motor-Kühlsystem: Abschaltung Kühlmittelpumpe wegen Überspannung |
| 0x377A | 0x377A Motor-Kühlsystem: Abschaltung Kühlmittelpumpe wegen Blockierung |
| 0x377B | 0x377B Motor-Kühlsystem, leistungsreduzierter Betrieb: Kühlmittelverlust durch Kühlmittelpumpe erkannt |
| 0x377C | 0x377C Motor-Kühlsystem, leistungsreduzierter Betrieb: Versorgungsspannung Kühlmittelpumpe zu niedrig |
| 0x377D | 0x377D Motor-Kühlsystem, leistungsreduzierter Betrieb: Kühlmittelpumpe Temperaturschwelle 1 überschritten |
| 0x377E | 0x377E Motor-Kühlsystem, leistungsreduzierter Betrieb: Kühlmittelpumpe Temperaturschwelle 2 überschritten |
| 0x378F | 0x378F BSD, Kommunikation (Motor-Kühlmittelpumpe): fehlt |
| 0x3791 | 0x3791 Motor-Kühlsystem: kein Notlaufsignal an Kühlmittelpumpe |
| 0x3792 | 0x3792 Motor-Kühlsystem: Drehzahl Kühlmittelpumpe außerhalb der Toleranz |
| 0x3796 | 0x3796 Kupplungsschalter, Signal: fehlt |
| 0x3840 | 0x3840 Generator, elektrisch: Fehlfunktion |
| 0x3841 | 0x3841 Generator, elektrisch: Fehlfunktion |
| 0x3842 | 0x3842 Generator, Plausibilität, elektrisch: berechnet |
| 0x3843 | 0x3843 Generator, Temperatur: Übertemperatur |
| 0x3844 | 0x3844 Generator, Plausibilität, elektrisch: berechnet |
| 0x3845 | 0x3845 Generator, mechanisch: Fehlfunktion |
| 0x3846 | 0x3846 Generator: Typ falsch |
| 0x3848 | 0x3848 Generator, Temperatur: Übertemperatur |
| 0x384C | 0x384C Generator, Plausibilität, Temperatur: Übertemperatur berechnet |
| 0x3850 | 0x3850 Generator, mechanisch: Fehlfunktion |
| 0x3854 | 0x3854 Generator, Regler: Typ falsch |
| 0x3858 | 0x3858 Generator: Typ falsch |
| 0x385B | 0x385B Generator/Startergenerator: Kodierung oder Programmstand falsch |
| 0x385C | 0x385C Generator, Kommunikation: keine Kommunikation |
| 0x385D | 0x385D Generator, Kommunikation: Bus-Fehler |
| 0x385F | 0x385F Generator/Startergenerator: Kodierung fehlt |
| 0x3865 | 0x3865 BSD-Bus: Kommunikationsfehler |
| 0x3866 | 0x3866 BSD, Botschaft (Intelligenter Batteriesensor): fehlt |
| 0x3871 | 0x3871 Startergenerator: Typ falsch |
| 0x3872 | 0x3872 Powermanagement, Batteriezustandserkennung: Batteriedefekt |
| 0x3873 | 0x3873 Powermanagement, Batteriezustandserkennung: Tiefentladung |
| 0x3875 | 0x3875 Powermanagement, Überspannung: Überspannung erkannt |
| 0x3876 | 0x3876 Powermanagement, Unterspannung: Unterspannung erkannt |
| 0x3877 | 0x3877 Powermanagement: zentrale Überspannung |
| 0x3878 | 0x3878 Powermanagement: zentrale Unterspannung |
| 0x3879 | 0x3879 Powermanagement: Batterieloser Betrieb |
| 0x387C | 0x387C Powermanagement: Batterie Tiefentladung |
| 0x387D | 0x387D Powermanagement: Transportüberwachung Ladezustand Batterie tiefentladen |
| 0x387F | 0x387F Powermanagement: Ruhestromverletzung |
| 0x3886 | 0x3886 Bordnetzspannung, Arbeitsbereich: Spannung zu hoch |
| 0x3887 | 0x3887 Bordnetzspannung, Arbeitsbereich: Spannung zu niedrig |
| 0x3888 | 0x3888 Bordnetzspannung: Analog-Digital-Wandler defekt |
| 0x38A4 | 0x38A4 Erweiterte Kommunikation, Intelligenter Batteriesensor: Fehlfunktion |
| 0x38A7 | 0x38A7 Intelligenter Batteriesensor, Kompatibilität: Version nicht plausibel |
| 0x38A8 | 0x38A8 Intelligenter Batteriesensor, Eigendiagnose: Systemfehler |
| 0x38A9 | 0x38A9 Intelligenter Batteriesensor, Plausibilität: Temperatur unplausibel |
| 0x38AA | 0x38AA Intelligenter Batteriesensor, Plausibilität: Spannung unplausibel |
| 0x38AB | 0x38AB Intelligenter Batteriesensor, Plausibilität: Strom unplausibel |
| 0x38AC | 0x38AC Intelligenter Batteriesensor, Wake-up-Leitung, elektrisch: Kurzschluss nach Plus oder Masse |
| 0x38B2 | 0x38B2 Intelligenter Batteriesensor, Wake-up-Leitung, elektrisch: Leitungsunterbrechung |
| 0x38B4 | 0x38B4 BSD, Kommunikation (Intelligenter Batteriesensor): fehlt |
| 0x38D6 | 0x38D6 Aktives Motorlager, elektrisch: Kurzschluss nach Plus |
| 0x38D7 | 0x38D7 Aktives Motorlager, elektrisch: Kurzschluss nach Masse |
| 0x38D8 | 0x38D8 Aktives Motorlager, elektrisch: Leitungsunterbrechung |
| 0x38EF | 0x38EF Freigabeleitung, MSA, Ansteuerung: Kurzschluss nach Plus |
| 0x38F0 | 0x38F0 Freigabeleitung, MSA, Ansteuerung: Kurzschluss nach Masse |
| 0x38F1 | 0x38F1 Freigabeleitung, MSA, Ansteuerung: Leitungsunterbrechung |
| 0x38F2 | 0x38F2 MSA, Überwachung: Motorstart zu langsam |
| 0x38F3 | 0x38F3 MSA, Überwachung: Aufbau Motordrehzahl zu langsam |
| 0x3908 | 0x3908 Batterieladeeinheit: Interner Fehler |
| 0x3909 | 0x3909 Batterieladeeinheit, Leitungsüberwachung: Fehlfunktion |
| 0x390A | 0x390A Batterieladeeinheit: Zusatzbatterie defekt |
| 0x390B | 0x390B Batterieladeeinheit: Fehler im Trennrelais oder Kabelbaum oder Zusatzbatterie tiefentladen |
| 0x390C | 0x390C Startspannungswandler, Ansteuerung: Kurzschluss nach Plus |
| 0x390D | 0x390D Startspannungswandler, Ansteuerung: Kurzschluss nach Masse |
| 0x390E | 0x390E Startspannungswandler, Ansteuerung: Leitungsunterbrechung |
| 0x393A | 0x393A Motordrehmomentbegrenzung: infolge Notlaufanforderung vom EME-Notlaufmanager |
| 0x393B | 0x393B Motordrehzahlbegrenzung, Stufe 1: infolge Notlaufanforderung vom EME-Notlaufmanager |
| 0x393C | 0x393C Motordrehzahlbegrenzung, Stufe 2: infolge Notlaufanforderung vom EME-Notlaufmanager |
| 0x393D | 0x393D Motordrehzahlbegrenzung, Stufe 3: infolge Notlaufanforderung vom EME-Notlaufmanager |
| 0x3B94 | 0x3B94 LIN, Botschaft (Batterieladeeinheit, Status Energieerzeugung Bordnetz 2, 0x5): fehlt |
| 0x3B97 | 0x3B97 LIN Bus, Kommunikation: Signal fehlt |
| 0x3B99 | 0x3B99 Motor-Kühlsystem: Kommunikation mit Kühlmittelpumpe fehlt |
| 0x3B9A | 0x3B9A Motor-Kühlsystem: Kommunikation mit Kühlmittelpumpe fehlerhaft |
| 0x3B9B | 0x3B9B LIN, Botschaft (Status Generator LIN, 0x15). fehlt |
| 0x3B9C | 0x3B9C LIN, Botschaft (Status_Wasserpumpe_LIN, 0x25): fehlt |
| 0x3B9D | 0x3B9D LIN Knoten Generator, Kommunikation: Fehlfunktion |
| 0x3BC4 | 0x3BC4 PT-CAN, Botschaft (Status ARS-Modul, 0x1AC): Aliveprüfung |
| 0x3BC5 | 0x3BC5 PT-CAN, Botschaft (Status ARS-Modul, 0x1AC): fehlt |
| 0x3BC6 | 0x3BC6 PT-CAN, Botschaft (Status ARS-Modul, 0x1AC): Prüfsumme falsch |
| 0x3BC7 | 0x3BC7 PT-CAN, Botschaft (Klemmenstatus, 0x130): fehlt |
| 0x3BC8 | 0x3BC8 PT-CAN, Botschaft (Klemmenstatus, 0x130): Prüfsumme falsch/Aliveprüfung |
| 0x3BCC | 0x3BCC PT-CAN, Botschaft (Wärmestrom/Lastmoment Klima, 0x1B5): fehlt |
| 0x3BCD | 0x3BCD PT-CAN, Botschaft (Status Kombi, 0x1B4): Aliveprüfung |
| 0x3BCE | 0x3BCE PT-CAN, Botschaft (Status Kombi, 0x1B4): fehlt |
| 0x3BCF | 0x3BCF PT-CAN, Botschaft (Status Kombi, 0x1B4): MIL-Ansteuerung unplausibel |
| 0x3BD0 | 0x3BD0 PT-CAN, Botschaft (Anforderung Drehmoment DSC, 0x0B6): Prüfsumme falsch/Aliveprüfung |
| 0x3BD1 | 0x3BD1 PT-CAN, Botschaft (Anforderung Drehmoment DSC, 0x0B6): fehlt |
| 0x3BD2 | 0x3BD2 PT-CAN, Botschaft (Radgeschwindigkeit, 0xCE): fehlt |
| 0x3BD3 | 0x3BD3 PT-CAN, Botschaft (Getriebedaten 4, 0x10A): Prüfsumme falsch/Aliveprüfung |
| 0x3BD4 | 0x3BD4 PT-CAN, Botschaft (Getriebedaten 4, 0x10A): fehlt |
| 0x3BD5 | 0x3BD5 PT-CAN, Botschaft (Status DSC, 0x19E): fehlt |
| 0x3BD6 | 0x3BD6 PT-CAN, Botschaft (Geschwindigkeit, 0x1A0): Prüfsumme falsch/Aliveprüfung |
| 0x3BD7 | 0x3BD7 PT-CAN, Botschaft (Geschwindigkeit, 0x1A0): fehlt |
| 0x3BD8 | 0x3BD8 PT-CAN, Botschaft (Getriebedaten 2, 0x1A2): fehlt |
| 0x3BD9 | 0x3BD9 PT-CAN, Botschaft (Status DKG, 0x37D): fehlt |
| 0x3BDA | 0x3BDA PT-CAN, Botschaft (Getriebedaten 3, 0x3B1): Prüfsumme falsch/Aliveprüfung |
| 0x3BDB | 0x3BDB PT-CAN, Botschaft (Getriebedaten 3, 0x3B1): fehlt |
| 0x3BDC | 0x3BDC PT-CAN, Botschaft (Anforderung Drehmoment EGS, 0xB5): Prüfsumme falsch/Aliveprüfung |
| 0x3BDD | 0x3BDD PT-CAN, Botschaft (Anforderung Drehmoment EGS, 0xB5): fehlt |
| 0x3BDE | 0x3BDE PT-CAN, Botschaft (Anforderung Drehmoment DKG, 0xB8): Prüfsumme falsch/Aliveprüfung |
| 0x3BDF | 0x3BDF PT-CAN, Botschaft (Anforderung Drehmoment DKG, 0xB8): fehlt |
| 0x3BE0 | 0x3BE0 PT-CAN, Botschaft (Getriebedaten, 0xBA): Prüfsumme falsch/Aliveprüfung |
| 0x3BE1 | 0x3BE1 PT-CAN, Botschaft (Getriebedaten, 0xBA): fehlt |
| 0x3BE2 | 0x3BE2 PT-CAN, Botschaft (DKG Drehzahlregelung, 0xB8): Überwachungseingriff |
| 0x3BE7 | 0x3BE7 PT-CAN, Botschaft (Bedienung Taster MSA, 0x195): fehlt |
| 0x3BEC | 0x3BEC PT-CAN, Botschaft (Bedienung Tempomat, 0x194): Prüfsumme falsch/Aliveprüfung |
| 0x3BED | 0x3BED PT-CAN, Botschaft (Bedienung Tempomat, 0x194): fehlt |
| 0x3BF0 | 0x3BF0 PT-CAN, Botschaft (Status Fahrererkennung, 0x2F1): Prüfsumme falsch |
| 0x3BF1 | 0x3BF1 PT-CAN, Botschaft (Status Fahrererkennung, 0x2F1): fehlt |
| 0x3BF4 | 0x3BF4 PT-CAN, Botschaft (ZV und Klappenzustand, 0x2FC): fehlt |
| 0xCD83 | 0xCD83 Energiesparmodus: aktiv |
| 0xCD85 | 0xCD85 PT-CAN, Botschaft (Klemmenstatus, 0x130): Prüfsumme falsch |
| 0xCD86 | 0xCD86 PT-CAN, Botschaft (Klemmenstatus, 0x130): fehlt |
| 0xCD87 | 0xCD87 PT-CAN Kommunikationsfehler: CAN-Bus Off oder CAN-Bus defekt |
| 0xCD89 | 0xCD89 PT-CAN, Botschaft (Status Crashabschaltung elektrische Kraftstoffpumpe, 0x135): fehlt |
| 0xCD8B | 0xCD8B PT-CAN, Botschaft (Stellanforderung EMF, 0x1A7): Prüfsumme falsch |
| 0xCD8C | 0xCD8C PT-CAN, Botschaft (Stellanforderung EMF, 0x1A7): fehlt |
| 0xCD8F | 0xCD8F PT-CAN, Botschaft (Anzeige Getriebedaten, 0x1D2): fehlt |
| 0xCD91 | 0xCD91 PT-CAN, Botschaft (Status EMF, 0x201): Prüfsumme falsch |
| 0xCD92 | 0xCD92 PT-CAN, Botschaft (Status EMF, 0x201): fehlt |
| 0xCD95 | 0xCD95 PT-CAN, Botschaft (Lampenzustand, 0x21A): fehlt |
| 0xCD98 | 0xCD98 PT-CAN, Botschaft (Status Anhänger, 0x2E4): fehlt |
| 0xCD9B | 0xCD9B PT-CAN, Botschaft (Uhrzeit/Datum, 0x2F8): fehlt |
| 0xCD9D | 0xCD9D PT-CAN, Botschaft (Fahrzeugmodus, 0x315): Prüfsumme falsch |
| 0xCD9E | 0xCD9E PT-CAN, Botschaft (Fahrzeugmodus, 0x315): fehlt |
| 0xCDA1 | 0xCDA1 PT-CAN, Botschaft (Powermanagement Ladespannung, 0x334): fehlt |
| 0xCDA2 | 0xCDA2 PT-CAN, Botschaft (Status Verdeck Cabrio, 0x27E): fehlt |
| 0xCDA4 | 0xCDA4 PT-CAN, Botschaft (Status Gang Rückwärts, 0x3B0): fehlt |
| 0xCDA5 | 0xCDA5 PT-CAN, Botschaft (Drehmomentanforderung Lenkung, 0xB1): AFS/STE disabled oder Lenkmoment ungültig |
| 0xCDA6 | 0xCDA6 PT-CAN, Botschaft (Drehmomentanforderung Lenkung, 0xB1): Prüfsumme falsch |
| 0xCDA7 | 0xCDA7 PT-CAN, Botschaft (Drehmomentanforderung Lenkung, 0xB1): fehlt |
| 0xCDA8 | 0xCDA8 PT-CAN, Botschaft (Drehmomentanforderung AFS, 0xB9): AFS/STE disabled oder Lenkmoment ungültig |
| 0xCDA9 | 0xCDA9 PT-CAN, Botschaft (Drehmomentanforderung AFS, 0xB9): Prüfsumme falsch |
| 0xCDAA | 0xCDAA PT-CAN, Botschaft (Drehmomentanforderung AFS, 0xB9): fehlt |
| 0xCDAB | 0xCDAB PT-CAN, Botschaft (Anforderung Radmoment Antriebstrang, 0xBF): Aliveprüfung |
| 0xCDAC | 0xCDAC PT-CAN, Botschaft (Anforderung Radmoment Antriebstrang, 0xBF): Prüfsumme falsch |
| 0xCDAD | 0xCDAD PT-CAN, Botschaft (Anforderung Radmoment Antriebstrang, 0xBF): fehlt |
| 0xCDB0 | 0xCDB0 PT-CAN, Botschaft (Lenkradwinkel, 0xC4): fehlt |
| 0xCDB1 | 0xCDB1 PT-CAN Kommunikationsfehler: DPRAM CAN Baustein defekt |
| 0xCDB2 | 0xCDB2 PT-CAN, Botschaft (Sollmomentanforderung, 0xBB): fehlt |
| 0xCDB3 | 0xCDB3 PT-CAN, Botschaft (Drehmomentanforderung AFS, 0xB9): Verlustmoment zu gross |
| 0xCDB4 | 0xCDB4 PT-CAN, Botschaft (OBD Sensor Diagnosestatus, 0x5E0): fehlt, Sender Kombi |
| 0xCDB6 | 0xCDB6 PT-CAN, Botschaft (Drehmomentanforderung Lenkung, 0xB1): Verlustmoment zu gross |
| 0xCDB7 | 0xCDB7 PT-CAN, Botschaft (Status Elektrische Kraftstoffpumpe, 0x335): fehlt |
| 0xCDB8 | 0xCDB8 PT-CAN, Botschaft (Status Klemmenanforderung, 0x365): fehlt |
| 0xCDB9 | 0xCDB9 PT-CAN, Botschaft (Status Türsensoren abgesichert BN2000, 0x1E1): Prüfsumme falsch |
| 0xCDBA | 0xCDBA PT-CAN, Botschaft (Status Türsensoren abgesichert BN2000, 0x1E1): fehlt |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 750 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x2710 | 0x583F | 0x584E | 0x584C | 0x5858 |
| 0x2711 | 0x583F | 0x584E | 0x584C | 0x5858 |
| 0x2714 | 0x583F | 0x584E | 0x584C | 0x5858 |
| 0x2774 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2775 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2778 | 0x580C | 0x5818 | 0x5812 | 0x58AE |
| 0x2779 | 0x580C | 0x5818 | 0x5812 | 0x58AE |
| 0x277A | 0x580C | 0x5818 | 0x5812 | 0x58AE |
| 0x277B | 0x580C | 0x5818 | 0x5812 | 0x58AE |
| 0x277C | 0x580C | 0x5818 | 0x5812 | 0x58AE |
| 0x27D9 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x27DA | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x27DB | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x27DC | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x27E4 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x27E8 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x280E | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x280F | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x281A | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x281B | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x2820 | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x283C | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x283D | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x2841 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2842 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2848 | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x284C | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x284D | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x284E | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x284F | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x28A0 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x28A1 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x28A4 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28A5 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28A6 | 0x5813 | 0x584E | 0x584C | 0x5858 |
| 0x28A8 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28A9 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28AA | 0x5813 | 0x584E | 0x584C | 0x5858 |
| 0x28AC | 0x583F | 0x584E | 0x584C | 0x5858 |
| 0x28B0 | 0x5813 | 0x584E | 0x584C | 0x5858 |
| 0x28B4 | 0x583F | 0x584E | 0x584C | 0x5858 |
| 0x28B8 | 0x5815 | 0x584E | 0x584C | 0x5821 |
| 0x28B9 | 0x5815 | 0x584E | 0x584C | 0x5821 |
| 0x28BA | 0x5815 | 0x584E | 0x584C | 0x5821 |
| 0x28BB | 0x5815 | 0x584E | 0x584C | 0x5821 |
| 0x28BC | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28BD | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28C0 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28C1 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28C4 | 0x58B0 | 0x584E | 0x584C | 0x5858 |
| 0x28CC | 0x58B0 | 0x584E | 0x584C | 0x5858 |
| 0x28CD | 0x58B0 | 0x584E | 0x584C | 0x5858 |
| 0x28D0 | 0x58B0 | 0x584E | 0x584C | 0x5858 |
| 0x28D4 | 0x58B0 | 0x584E | 0x584C | 0x5858 |
| 0x28D8 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28D9 | 0x580C | 0x5812 | 0x5814 | 0x580B |
| 0x2904 | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x2906 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2908 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x290A | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x2936 | 0x580C | 0x5850 | 0x580F | 0x5817 |
| 0x2937 | 0x580C | 0x5850 | 0x580F | 0x5817 |
| 0x293A | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x293B | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x293E | 0x5817 | 0x5850 | 0x58EA | 0x580F |
| 0x2942 | 0x5817 | 0x5850 | 0x5836 | 0x5815 |
| 0x2943 | 0x5817 | 0x5850 | 0x5836 | 0x5815 |
| 0x2946 | 0x5817 | 0x5850 | 0x58EA | 0x580F |
| 0x2947 | 0x5817 | 0x5850 | 0x58EA | 0x580F |
| 0x2948 | 0x5817 | 0x5850 | 0x58EA | 0x580F |
| 0x299A | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x299B | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x299C | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x299E | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x29A2 | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x29A3 | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x29CC | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x29CD | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x29D0 | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x29D1 | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x29D2 | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x29D8 | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x29D9 | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x29DC | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x29DD | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x29E0 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x29E1 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x29E2 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x29E4 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x29E5 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x29E6 | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x29E7 | 0x580C | 0x5814 | 0x5817 | 0x580F |
| 0x29E8 | 0x580C | 0x5814 | 0x5817 | 0x580F |
| 0x29FE | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x29FF | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A00 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A01 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A02 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A03 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A04 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A05 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A06 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A07 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A08 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A09 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0A | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0B | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0C | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0D | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0E | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0F | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A10 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A11 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A12 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A13 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A14 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A15 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A30 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A31 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A32 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A33 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A34 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A35 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A40 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A41 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A42 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A43 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A44 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A45 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A4C | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A4D | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A4E | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A4F | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A50 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A51 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A5F | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A60 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A61 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A70 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A71 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A72 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A73 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A74 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A75 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2BC0 | 0x580C | 0x5813 | 0x5807 | 0x5806 |
| 0x2BC1 | 0x580C | 0x5813 | 0x5807 | 0x5806 |
| 0x2BC2 | 0x580C | 0x5813 | 0x5807 | 0x5806 |
| 0x2BC5 | 0x580C | 0x5855 | 0x5807 | 0x5804 |
| 0x2BC3 | 0x580C | 0x5813 | 0x5807 | 0x5806 |
| 0x2BCA | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2BCB | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2BD9 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BDA | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BDB | 0x580C | 0x5813 | 0x58EF | 0x5855 |
| 0x2BDC | 0x580C | 0x5813 | 0x58EF | 0x5855 |
| 0x2BDD | 0x580C | 0x5813 | 0x58EF | 0x5855 |
| 0x2BDE | 0x58EF | 0x58F3 | 0x5882 | 0x5815 |
| 0x2BDF | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE0 | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE1 | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE2 | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE3 | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE4 | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE5 | 0x580C | 0x58EF | 0x5837 | 0x5805 |
| 0x2BE6 | 0x580C | 0x58EF | 0x5837 | 0x5805 |
| 0x2BE9 | 0x580C | 0x58EF | 0x583B | 0x5805 |
| 0x2BEA | 0x580C | 0x5855 | 0x5807 | 0x5804 |
| 0x2BEB | 0x580C | 0x5855 | 0x5807 | 0x5804 |
| 0x2BEC | 0x58F0 | 0x58F2 | 0x5805 | 0x5815 |
| 0x2BED | 0x580C | 0x58EF | 0x5837 | 0x5805 |
| 0x2BEE | 0x580C | 0x58EF | 0x5837 | 0x5805 |
| 0x2BEF | 0x58EF | 0x580C | 0x5882 | 0x5823 |
| 0x2BF0 | 0x58EF | 0x580C | 0x5817 | 0x5823 |
| 0x2BF2 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF3 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF4 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF5 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF6 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF7 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF8 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2C00 | 0x580C | 0x58EF | 0x5837 | 0x5855 |
| 0x2C01 | 0x580C | 0x58EF | 0x5837 | 0x5855 |
| 0x2C3D | 0x58F2 | 0x580D | 0x580C | 0x586A |
| 0x2C3E | 0x58F2 | 0x580D | 0x580C | 0x586A |
| 0x2C3F | 0x58F2 | 0x580D | 0x580C | 0x586A |
| 0x2C42 | 0x580C | 0x5813 | 0x5807 | 0x5806 |
| 0x2C56 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2C57 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2C58 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2C6F | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C70 | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C71 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2C72 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2C7F | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C83 | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C84 | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C85 | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C86 | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C88 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2C89 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2C8A | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2C90 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2C91 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2CA1 | 0x58DD | 0x580C | 0x5821 | 0x586A |
| 0x2CA2 | 0x58DD | 0x580C | 0x5821 | 0x586A |
| 0x2CA3 | 0x58DD | 0x580C | 0x5821 | 0x586A |
| 0x2CB3 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2CED | 0x5806 | 0x5815 | 0x5849 | 0x585C |
| 0x2CEE | 0x5827 | 0x588C | 0x5860 | 0x5863 |
| 0x2CF4 | 0x580C | 0x5855 | 0x5807 | 0x5804 |
| 0x2CF8 | 0x588C | 0x5800 | 0x5845 | 0x5849 |
| 0x2CFA | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2CFE | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2CFF | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D00 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D03 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D04 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D05 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D06 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D0B | 0x588C | 0x5800 | 0x5845 | 0x5815 |
| 0x2D0C | 0x588C | 0x5800 | 0x5845 | 0x5815 |
| 0x2D0D | 0x588C | 0x5800 | 0x5845 | 0x5815 |
| 0x2D0F | 0x5800 | 0x5815 | 0x5849 | 0x585C |
| 0x2D10 | 0x5800 | 0x5815 | 0x5849 | 0x585C |
| 0x2D11 | 0x5800 | 0x5815 | 0x5849 | 0x585C |
| 0x2D13 | 0x5849 | 0x5818 | 0x588B | 0x582F |
| 0x2D15 | 0x5806 | 0x5815 | 0x5849 | 0x585C |
| 0x2D17 | 0x5827 | 0x588C | 0x5860 | 0x5863 |
| 0x2D18 | 0x5827 | 0x588C | 0x5860 | 0x5863 |
| 0x2D19 | 0x5827 | 0x588C | 0x5860 | 0x5863 |
| 0x2D1B | 0x5849 | 0x5818 | 0x588B | 0x582F |
| 0x2D1C | 0x5849 | 0x5818 | 0x588B | 0x582F |
| 0x2D1E | 0x5849 | 0x5818 | 0x588B | 0x582F |
| 0x2D1F | 0x5806 | 0x5815 | 0x5849 | 0x585C |
| 0x2D20 | 0x5806 | 0x5815 | 0x5849 | 0x585C |
| 0x2D22 | 0x5806 | 0x5815 | 0x5849 | 0x585C |
| 0x2D23 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D24 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D25 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D27 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D2B | 0x5827 | 0x588C | 0x5860 | 0x5863 |
| 0x2D2F | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D33 | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2D34 | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2D35 | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2D36 | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2D41 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2D42 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2D43 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2D44 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2D45 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2D51 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D52 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D53 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D54 | 0x580C | 0x5813 | 0x581C | 0x581D |
| 0x2D55 | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2D5A | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2D5B | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2D60 | 0x580C | 0x5813 | 0x581C | 0x581D |
| 0x2D61 | 0x580C | 0x5813 | 0x581C | 0x581D |
| 0x2D9B | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D9C | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D9D | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D9F | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2DA0 | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2DA1 | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2DA2 | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2DAD | 0x580C | 0x5813 | 0x581C | 0x581D |
| 0x2DAE | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2DAF | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2DB0 | 0x580C | 0x5813 | 0x581C | 0x581D |
| 0x2DB1 | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2DB4 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DB5 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DB6 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DBA | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DBB | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DBC | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2DBD | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2DBF | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DC0 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DC3 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DC4 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCA | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCB | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCC | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCD | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCE | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCF | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2DD0 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DD6 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DD7 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DD8 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DE1 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DE2 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DE3 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DE4 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DE5 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2DE6 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2DE7 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2DE8 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2DE9 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2DEA | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2E0A | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2E0B | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2E0C | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2E0D | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2E0E | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2E0F | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2E10 | 0x580C | 0x58E6 | 0x5822 | 0x58A2 |
| 0x2E11 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2E12 | 0x580C | 0x58E6 | 0x5822 | 0x58A2 |
| 0x2E13 | 0x589E | 0x58E5 | 0x58BB | 0x58A2 |
| 0x2E4A | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2E4B | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2E4C | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2E7C | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E7D | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E7E | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E80 | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E81 | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E82 | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E84 | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2EE0 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE1 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE2 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE4 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE5 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE6 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE7 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE8 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE9 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EEA | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EEB | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EEC | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EED | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EEF | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF0 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF1 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF2 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF3 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF4 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF5 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF6 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EFE | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EFF | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F00 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F01 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F02 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F03 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F04 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F44 | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2F45 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2F76 | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F77 | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F78 | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F79 | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F7A | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F7B | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F7C | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F83 | 0x580C | 0x5813 | 0x580E | 0x58CA |
| 0x2F84 | 0x580C | 0x5813 | 0x580E | 0x58CA |
| 0x2F8A | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2F8B | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2FA8 | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FA9 | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FAA | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FAB | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FAC | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FAD | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FDA | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2FDB | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2FDD | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x300C | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x300D | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x300E | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x300F | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x3011 | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x3012 | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x303E | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x303F | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x3040 | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x3041 | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x3042 | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x3043 | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x3044 | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x3045 | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x3046 | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x3048 | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x3049 | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x304C | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x304D | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x3106 | 0x580C | 0x5805 | 0x58AD | 0x5818 |
| 0x3139 | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x313A | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x313B | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x3140 | 0x580C | 0x583B | 0x588E | 0x5859 |
| 0x3141 | 0x580C | 0x583B | 0x588E | 0x585B |
| 0x3142 | 0x580C | 0x583B | 0x5859 | 0x5815 |
| 0x3143 | 0x580C | 0x583B | 0x5859 | 0x5815 |
| 0x3144 | 0x580C | 0x583B | 0x5859 | 0x5815 |
| 0x3145 | 0x580C | 0x583B | 0x588E | 0x5859 |
| 0x3146 | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x3147 | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x3148 | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x314A | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x314B | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x314C | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x3155 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3156 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3157 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3159 | 0x580C | 0x583B | 0x58FA | 0x586A |
| 0x315A | 0x580C | 0x583B | 0x58FA | 0x586A |
| 0x3160 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3161 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3162 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3163 | 0x580C | 0x583B | 0x58FA | 0x586A |
| 0x3164 | 0x580C | 0x583B | 0x58FA | 0x586A |
| 0x3165 | 0x580C | 0x583B | 0x5859 | 0x5815 |
| 0x3166 | 0x580C | 0x583B | 0x58FA | 0x586A |
| 0x316A | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x316B | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x3183 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x3184 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x3185 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x3187 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x3188 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x3189 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x318A | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x318B | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x318C | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x318D | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x318F | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x31E7 | 0x5805 | 0x587F | 0x580D | 0x5815 |
| 0x31E8 | 0x5805 | 0x587F | 0x580D | 0x5815 |
| 0x31E9 | 0x5805 | 0x587F | 0x580D | 0x5815 |
| 0x31EA | 0x5805 | 0x587F | 0x580D | 0x5815 |
| 0x3219 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x321A | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x321B | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x321C | 0x583B | 0x5859 | 0x585A | 0x588D |
| 0x321D | 0x583B | 0x5859 | 0x585A | 0x588D |
| 0x321E | 0x580C | 0x583B | 0x5859 | 0x585A |
| 0x321F | 0x580C | 0x583B | 0x5859 | 0x585A |
| 0x3220 | 0x580C | 0x583B | 0x5859 | 0x585A |
| 0x3221 | 0x580C | 0x583B | 0x5859 | 0x585A |
| 0x3222 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3223 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3224 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3225 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3226 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3227 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3228 | 0x580C | 0x583B | 0x5859 | 0x585A |
| 0x32AB | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32C8 | 0x580C | 0x586A | 0x580D | 0x5881 |
| 0x32C9 | 0x580C | 0x586A | 0x580D | 0x5881 |
| 0x32CC | 0x580C | 0x5813 | 0x580D | 0x5814 |
| 0x32CD | 0x580C | 0x5813 | 0x580D | 0x5814 |
| 0x32D0 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32D4 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32D8 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32D9 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32DA | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32DC | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32DD | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32DE | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32DF | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32E1 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E2 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E3 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E4 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E5 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E6 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E7 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E8 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E9 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32EA | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32EC | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x3325 | 0x58B7 | 0x5821 | 0x580D | 0x5815 |
| 0x332C | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x332D | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x332E | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x332F | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x3330 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x335B | 0x58B7 | 0x5821 | 0x580D | 0x5815 |
| 0x335C | 0x58B7 | 0x5821 | 0x580D | 0x5815 |
| 0x335D | 0x58B7 | 0x5821 | 0x580D | 0x5815 |
| 0x3392 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3393 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3394 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3395 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3396 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3398 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3399 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x33DB | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x33FC | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x33FD | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x33FE | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x33FF | 0x580C | 0x586F | 0x5866 | 0x586A |
| 0x3400 | 0x580C | 0x586F | 0x5866 | 0x586A |
| 0x3401 | 0x580C | 0x586F | 0x5866 | 0x586A |
| 0x3404 | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x3405 | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x3406 | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x3408 | 0x580C | 0x5822 | 0x586F | 0x586A |
| 0x3409 | 0x580C | 0x5822 | 0x586F | 0x586A |
| 0x3426 | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x3427 | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x3429 | 0x580C | 0x5822 | 0x586F | 0x5801 |
| 0x342A | 0x580C | 0x5822 | 0x586F | 0x5801 |
| 0x342B | 0x580C | 0x5822 | 0x586F | 0x5801 |
| 0x343F | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3440 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3441 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3442 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3443 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3444 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3446 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3447 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3449 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344A | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344B | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344C | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344D | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344E | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344F | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x348A | 0x580C | 0x5805 | 0x5882 | 0x5817 |
| 0x348E | 0x580C | 0x5805 | 0x5882 | 0x5817 |
| 0x348F | 0x580C | 0x5805 | 0x5882 | 0x5817 |
| 0x3490 | 0x580C | 0x5805 | 0x5882 | 0x5817 |
| 0x34A5 | 0x580C | 0x586A | 0x580D | 0x5881 |
| 0x34A8 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x34A9 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x34AD | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x34AE | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x34AF | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x3520 | 0x580C | 0x5813 | 0x580D | 0x5881 |
| 0x3521 | 0x580C | 0x5813 | 0x580D | 0x5881 |
| 0x3524 | 0x580C | 0x5813 | 0x580D | 0x5881 |
| 0x3525 | 0x580C | 0x5813 | 0x580D | 0x5881 |
| 0x3528 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x3529 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x352A | 0x580C | 0x5812 | 0x5814 | 0x580B |
| 0x3584 | 0x5841 | 0x5805 | 0x5821 | 0x586A |
| 0x3585 | 0x5841 | 0x5805 | 0x5821 | 0x586A |
| 0x3586 | 0x580C | 0x5805 | 0x580F | 0x5821 |
| 0x36B0 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x36B1 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36B2 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36B4 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36B5 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36B6 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36B7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36B8 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x36B9 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36BA | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36BB | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36BC | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36BD | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36BE | 0x5832 | 0x583D | 0x58FC | 0x5815 |
| 0x36BF | 0x580C | 0x5813 | 0x580D | 0x5814 |
| 0x36C0 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x36C1 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x36C2 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36C3 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x36C4 | 0x58B8 | 0x5814 | 0x58CF | 0x58D0 |
| 0x36C5 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36C6 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36C7 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36C8 | 0x58B8 | 0x5816 | 0x5889 | 0x58D0 |
| 0x36C9 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36CA | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36CB | 0x58B8 | 0x5881 | 0x580D | 0x58D0 |
| 0x36CC | 0x58B8 | 0x5814 | 0x58CF | 0x58D0 |
| 0x36CD | 0x58B8 | 0x58BC | 0x58BA | 0x580E |
| 0x36CE | 0x58B8 | 0x5858 | 0x583F | 0x5815 |
| 0x36CF | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36D0 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36D2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36D4 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x36E2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36E3 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36E4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36E5 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36E6 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36E7 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36FA | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36FB | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36FC | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36FD | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x36FE | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x36FF | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x3714 | 0x580C | 0x583C | 0x5898 | 0x586A |
| 0x3719 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x371A | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x371B | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x371C | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x371E | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x375A | 0x580C | 0x586F | 0x5866 | 0x586A |
| 0x375B | 0x580C | 0x586F | 0x5866 | 0x586A |
| 0x375C | 0x5832 | 0x583D | 0x58FC | 0x5815 |
| 0x375F | 0x5832 | 0x583D | 0x58FC | 0x5815 |
| 0x3760 | 0x5832 | 0x583D | 0x58FC | 0x5815 |
| 0x3761 | 0x5832 | 0x583D | 0x58FC | 0x5815 |
| 0x3778 | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x3779 | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x377A | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x377B | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x377C | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x377D | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x377E | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x378F | 0x580C | 0x5805 | 0x58EA | 0x5815 |
| 0x3791 | 0x580C | 0x5805 | 0x58EA | 0x5815 |
| 0x3792 | 0x580C | 0x5805 | 0x58EA | 0x5815 |
| 0x3796 | 0x580C | 0x586A | 0x580D | 0x5881 |
| 0x3840 | 0x5857 | 0x5887 | 0x5898 | 0x5815 |
| 0x3841 | 0x5872 | 0x5835 | 0x5842 | 0x5815 |
| 0x3842 | 0x5872 | 0x5835 | 0x5842 | 0x5815 |
| 0x3843 | 0x5857 | 0x5887 | 0x5844 | 0x5815 |
| 0x3844 | 0x5857 | 0x5887 | 0x5898 | 0x5815 |
| 0x3845 | 0x5872 | 0x5835 | 0x5842 | 0x5815 |
| 0x3848 | 0x5857 | 0x5887 | 0x5844 | 0x5815 |
| 0x384C | 0x5857 | 0x5887 | 0x5844 | 0x5815 |
| 0x3850 | 0x5857 | 0x5887 | 0x5898 | 0x5815 |
| 0x3854 | 0x5872 | 0x5835 | 0x5842 | 0x5815 |
| 0x3858 | 0x5872 | 0x5835 | 0x5842 | 0x5815 |
| 0x385C | 0x588B | 0x5835 | 0x5842 | 0x5815 |
| 0x385D | 0x5857 | 0x5887 | 0x5898 | 0x5815 |
| 0x3865 | 0x580C | 0x5852 | 0x5854 | 0x5817 |
| 0x3866 | 0x580C | 0x5852 | 0x5854 | 0x5817 |
| 0x3872 | 0x5868 | 0x5869 | 0x5823 | 0x586A |
| 0x3873 | 0x5868 | 0x5869 | 0x5823 | 0x586A |
| 0x3875 | 0x586A | 0x5898 | 0x58A5 | 0x58A4 |
| 0x3876 | 0x586A | 0x5898 | 0x58A5 | 0x58A4 |
| 0x3877 | 0x586A | 0x5898 | 0x58A5 | 0x58A4 |
| 0x3878 | 0x586A | 0x5898 | 0x58A5 | 0x58A4 |
| 0x3879 | 0x580C | 0x586A | 0x5898 | 0x584F |
| 0x387C | 0x580C | 0x586A | 0x5823 | 0x5869 |
| 0x387D | 0x589F | 0x5868 | 0x5869 | 0x5898 |
| 0x387F | 0x586B | 0x586C | 0x586E | 0x58A0 |
| 0x3886 | 0x580C | 0x583C | 0x5898 | 0x586A |
| 0x3887 | 0x580C | 0x583C | 0x5898 | 0x586A |
| 0x3888 | 0x580C | 0x583C | 0x5898 | 0x586A |
| 0x38A4 | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38A7 | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38A8 | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38A9 | 0x580C | 0x5852 | 0x5854 | 0x5817 |
| 0x38AA | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38AB | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38AC | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38B2 | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38B4 | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38D6 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38D7 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38D8 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38EF | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38F0 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38F1 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38F2 | 0x580C | 0x58EF | 0x583B | 0x5805 |
| 0x38F3 | 0x580C | 0x58EF | 0x583B | 0x5805 |
| 0x3908 | 0x5825 | 0x586A | 0x5817 | 0x5820 |
| 0x3909 | 0x5825 | 0x586A | 0x5817 | 0x5820 |
| 0x390A | 0x5825 | 0x586A | 0x5817 | 0x5820 |
| 0x390B | 0x5825 | 0x586A | 0x5817 | 0x5820 |
| 0x390C | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x390D | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x390E | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x393A | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x393B | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x393C | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x393D | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3B94 | 0x5825 | 0x586A | 0x5817 | 0x5820 |
| 0x3B97 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3B99 | 0x580C | 0x5805 | 0x58EA | 0x5815 |
| 0x3B9A | 0x580C | 0x5805 | 0x58EA | 0x5815 |
| 0x3B9B | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3B9C | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3B9D | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BC4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BC5 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BC6 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BC7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BC8 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BCC | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BCD | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BCE | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BCF | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD0 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD1 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD3 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD5 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD6 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD8 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD9 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDA | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDB | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDC | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDD | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDE | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDF | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BE0 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BE1 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BE2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BE7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BEC | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BED | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BF0 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BF1 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BF4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD83 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0xCD85 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD86 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD87 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD89 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD8B | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD8C | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD8F | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD91 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD92 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD95 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD98 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD9B | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD9D | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD9E | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA1 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA5 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA6 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA8 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA9 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDAA | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDAB | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDAC | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDAD | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB0 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB1 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB3 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB6 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB8 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB9 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDBA | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xFFFF | 0x58FF | 0x58FF | 0x58FF | 0x58FF |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 444 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4200 | Ansaugluft-Temperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4201 | Umgebungsdruck | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x4202 | Saugrohr-Absolutdruck | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x4203 | Massenstrom HFM | kg/h | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4204 | Umgebungstemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4205 | Druck vor Drosselklappe | hPa | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| 0x4300 | Motor-Temperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4303 | empf. Temperatur von BSS-Wasserpumpe | Grad C | - | unsigned char | - | 1,0 | 1 | -50,0 |
| 0x4304 | empf. Strom von BSS-Wasserpumpe | % | - | unsigned char | - | 0,5 | 1 | 0,0 |
| 0x4305 | empf. Istdrehzahl von BSS-Wasserpumpe | 1/min | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4306 | Quittung  Solldrehzahl von BSS-Wasserpumpe | 1/min | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4307 | empf. Status von BSS-Wasserpumpe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4400 | Langzeit-Ölniveau-Mittelwert für den DIS-Tester | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x4401 | Relativer Füllstand des Motoröls | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4402 | Oeltemperatur nach Filter | Grad C | - | unsigned integer | - | 0,75 | 1 | -48,0 |
| 0x4403 | Kraftstoffverbrauch seit letztem Ölwechsel | - | - | unsigned long | - | 1,220703125E-4 | 1 | 0,0 |
| 0x4404 | Ölkilometer | km | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| 0x4405 | Sensorrohwert Ölniveau | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4406 | Sensorrohwert Permittivität | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4407 | Sensorrohwert Öltemperatur | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4408 | Öltemperatur ungefiltert | Grad C | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4409 | Ölniveau ungefiltert in [mm] | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x440A | Permitivität für den Tester | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x440B | CodingDataSet-ÖL-Länderfaktor1- EEPROM | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440C | CodingDataSet-ÖL-Länderfaktor2- EEPROM | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440D | Länderfaktor 1 | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440E | Länderfaktor 2 | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440F | Kurzzeit-Ölniveau-Mittelwert für den DIS-Tester | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x4411 | Restweg aus Kraftstoffverbrauch abgeleitet | - | - | signed integer | - | 10,0 | 1 | 0,0 |
| 0x4412 | Öllaufzeit | month | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4418 | Status Ölzustandssensor | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4501 | VVT Excenterwellenadaptionswert | mm | - | signed integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x4505 | Sollwinkel vom BMW Layer (Einlass-VANOS) | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x4506 | Nockenwellenposition Einlass | Grad KW | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4507 | Nockenwellenposition Auslass | Grad KW | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4508 | Winkel Einlassventil oeffnet bezogen auf LWOT | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x4509 | Winkel Auslassventil schließt bezogen auf LWOT | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x450C | Adaption Kurbel/Einlassnockenwelle erfolgt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x450D | Adaption Kurbel/Auslassnockenwelle erfolgt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x450E | [0] Nullpunktverschiebung in Grad KW für die Winkelversatz Diag, bedingt d. Toleranzen d. Einbaulage | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x4510 | Bedingung VVT-Lagereglerüberwachung hat bleibende Regelabweichung erkannt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4511 | Bedingung VVT-Lageregler schwingt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4512 | Bedingung: VVT Motor Überlast Warnschwelle | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4513 | Bedingung VVT-Überlastung (klemmender Steller) | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4514 | Bedingung VVT-Adaption möglich | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4515 | Anforderung VVT-Anschlaglernen (intern) | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4516 | Status VVT-Anschlaglernen (intern) | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4517 | [0] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 0 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x4518 | [1] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 1 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x4519 | [2] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 2 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451A | [3] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 3 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451B | [4] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 4 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451C | [5] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 5 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451D | Gesamtzeit VVT-Performancetest | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x451E | Stromsumme VVT-Performancetest | A | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4600 | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | - | signed integer | - | 0,0244140625 | 1 | 0,0 |
| 0x4601 | Sollwert Drosselklappenwinkel, bezogen auf (unteren) Anschlag | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4602 | phys. Wert Generatorsollspannung (Volt) für Komponententreiber Generator | V | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| 0x4603 | Chiptemperatur Generator 1 | Grad C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x4604 | Generatorstrom | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4605 | Chipversion Generator 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4606 | Reglerversion on Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4607 | Kennung Generator Hersteller | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4608 | Kennung Generatortyp | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x460A | momentane Batteriespannung | V | - | unsigned integer | - | 0,014999999664723873 | 1 | 0,0 |
| 0x460B | aktuelle Batteriespannung | V | - | unsigned integer | - | 2,500000118743628E-4 | 1 | 6,0 |
| 0x460C | Batteriespannung; vom AD-Wandler erfaßter Wert  | V | - | unsigned integer | - | 0,02355000004172325 | 1 | 0,0 |
| 0x460D | Korrekturwert Abschaltung | % | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 |
| 0x460E | Abstand zur Startfähigkeit | % | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 |
| 0x460F | DF-Monitor für Batterie-Ladezustand in % | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4611 | Tastverhältnis E-Lüfter | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4612 | Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x4613 | vom Generator empfangene Generatorsollspannung (Kopie gesendeter Wert) | V | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| 0x4614 | Auslastungsgrad Generator 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4615 | Kopie begrenzter Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x4616 | vom Generator empfangene Load response Zeit (Kopie gesendeter Wert) | s | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4617 | gefiltertes Generatormoment absolut | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4618 | Drehzahlschwelle für LR-Funktion Generator 1 aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4619 | Bedingung BSD Protokollinhalt für BSD2 Regler | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x461A | Nominalspannung Regler Generator 1 | V | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| 0x4680 | Leerlaufdrehzahl gelernt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4681 | Getriebe ist bereit die Neutralposition anzulernen | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4700 | Bedingung Sonde betriebsbereit vor Kat | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4701 | Bedingung Sonde betriebsbereit vor Kat, Bank 2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4702 | Offset korrigierte Sondenspannung vor Kat einer Breitbandlambdasonde | V | - | unsigned integer | - | 4,8828125E-4 | 1 | 0,0 |
| 0x4703 | Offset korrigierte Sondenspannung vor Kat einerBreitbandlambdasonde Bank 2 | V | - | unsigned integer | - | 4,8828125E-4 | 1 | 0,0 |
| 0x4704 | Lambdasoll Begrenzung (word) | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x4705 | Lambdasoll Begrenzung (word) Bank2 | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x4800 | Bedingung Kupplungspedal betätigt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4801 | Schalter Kupplung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4802 | Bedingung umschalten auf KFPEDS | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4803 | Bedingung für Kompressoreinschalten | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4805 | Schalter Klemme 50 von CAN | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4806 | Steuergerätetemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4807 | Motordrehzahl | 1/min | - | unsigned integer | - | 0,25 | 1 | 0,0 |
| 0x4808 | Leerlaufsolldrehzahl | 1/min | - | unsigned integer | - | 0,25 | 1 | 0,0 |
| 0x4809 | Bedingung Leerlaufregelung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x480A | Wegstrecke_km auf 1km genau | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x480B | normierter Fahrpedalwinkel | %PED | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| 0x4880 | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Leerlauf bez. auf Schwellwert | % | - | unsigned char | - | 0,78125 | 1 | 0,0 |
| 0x4881 | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Teillast bez. auf Schwellwert | % | - | unsigned char | - | 0,78125 | 1 | 0,0 |
| 0x4890 | Tprot-Status auslesen | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5800 | Zeitzähler ab Startende (16bit) | s | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5801 | Umgebungsdruck | hPa | - | unsigned char | - | 5,0 | 1 | 0,0 |
| 0x5802 | CARB FREEZE FRAME Byte, Bank 1, für LR | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5804 | relative Luftmasse (calc. load value) nach SAE J1979 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5805 | Motortemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5806 | Lambda-Regler-Ausgang (Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5807 | Faktor aus Lambdaregelungsadaption für Bank 1 | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x580B | Saugrohr-Absolutdruck (Word) | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x580C | Motordrehzahl | 1/min | - | unsigned char | - | 40,0 | 1 | 0,0 |
| 0x580D | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1,25 | 1 | 0,0 |
| 0x580E | Zündwinkel Zylinder 1 | Grad KW | - | signed char | - | 0,75 | 1 | 0,0 |
| 0x580F | Ansaugluft-Temperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5810 | relative Luftmasse (calc. load value) nach SAE J1979 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5812 | Massenstrom HFM 16-Bit Größe | kg/h | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5813 | relative Luftfüllung | % | - | unsigned char | - | 0,75 | 1 | 0,0 |
| 0x5814 | Normierter Fahrpedalwinkel | %PED | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5815 | Batteriespannung | V | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| 0x5816 | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5817 | Umgebungstemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5818 | Luftmassenfluß | kg/h | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x5819 | Motordrehzahl [1/min] | rpm | - | signed integer | - | 0,5 | 1 | 0,0 |
| 0x581A | Winkel Einlassventil oeffnet bezogen auf LWOT | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581B | Sollwinkel Nockenwelle Einlass öffnet | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581C | Winkel Auslassventil schließt bezogen auf LWOT | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581D | Sollwinkel Nockenwelle Auslass schließt | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581E | Ansauglufttemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x581F | Motortemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5820 | Status Klemme 15 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5821 | Steuergerätetemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5822 | Öltemperatur | Grad C | - | unsigned char | - | 1,0 | 1 | -60,0 |
| 0x5823 | Abstellzeit | s | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5825 | Spannung BCU LIN | V | - | signed integer | - | 0,009999999776482582 | 1 | 0,0 |
| 0x5826 | Drosselklappenwinkel aus Poti 1 | %DK | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5827 | Tastverhältnis für Lambdasondenheizung | % | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x5829 | normierte Heizleistung der Lambdasonde hinter Kat | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x582B | Drehmomentaufnahme des Wandlers über CAN | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x582C | Lambdasondenistwert, korrigiert um Zusatzamplitude | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x582D | Korrekturwert der LSU-Spannung vor Kat | V | - | signed integer | - | 4,8828125E-4 | 1 | 0,0 |
| 0x582F | Abgastemperatur nach Katalysator aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x5830 | Dynamikwert der LSU | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5832 | Zustand Motor-Koordinator | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5834 | Umgebungsdruck von Sensor | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x5835 | Kennung Generator Hersteller | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5836 | gefilterter Drehzahlgradient | 1/min/s | - | signed char | - | 100,0 | 1 | 0,0 |
| 0x5837 | Solldruck Hochdrucksystem | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x5838 | Relatives Moment für Aussetzererkennung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5839 | Bedingung Sicherheitskraftstoffabschaltung (SKA) | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x583A | Ansaugluft-Temperatur bei Start | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x583B | Fuellstand Kraftstofftank | L | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x583C | Batteriespannung; vom AD-Wandler erfasster Wert | V | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| 0x583D | Betriebsstundenzaehler | min | - | unsigned integer | - | 6,0 | 1 | 0,0 |
| 0x583E | Dauer-RAM: Sollwert DK-Winkel in NLP-Stellung, bez. auf UMA | %DK | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| 0x583F | Sollwert DK-Winkel, bezogen auf unteren Anschlag | %DK | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5840 | DK-Winkel der Notluftposition | %DK | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| 0x5841 | Wert Temperatur Steuergerät | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5842 | Kennung Generatortyp | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5844 | Chiptemperatur Generator 1 | Grad C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x5845 | Sondenspannung vor Kat einer Breitbandlambdasonde (ADC-Wert) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5846 | Spannung PWG-Poti 1 (Word) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5847 | Spannung PWG-Poti 2 (Word) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5849 | ADC-Spannung Lambdasonde hinter Katalysator (Word) | V | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| 0x584C | Spannung DK-Poti 2 | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x584D | Massenstrom Tankentlüftung in das Saugrohr | kg/h | - | unsigned integer | - | 3,906250058207661E-4 | 1 | 0,0 |
| 0x584E | Spannung DK-Poti 1 | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x584F | Erkennung Bordnetzinstabilität | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5850 | Signalspannung des Kühlmitteltemperatursensors | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5851 | Spannungswert des Ansauglufttemperatursensors tfa2 (SY_TFAKON &gt; 0) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5852 | Batteriestrom von IBS | A | - | unsigned integer | - | 0,019999999552965164 | 1 | -200,0 |
| 0x5853 | Batt Spannung von IBS | V | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x5854 | BattTemp von IBS | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5855 | schneller Mittelwert des Lambdaregelfaktors (Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5857 | Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x5858 | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5859 | Pumpenstrom Referenzleck | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x585A | min. Pumpenstrom bei Grobleckmessung | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x585B | Pumpenstrom am Ende der Feinstleckmessung | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x585C | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | - | unsigned char | - | 512,0 | 1 | 0,0 |
| 0x585E | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | - | unsigned char | - | 2,0 | 1 | 0,0 |
| 0x5860 | Innenwiderstand der Nernstzelle der LSU | Ohm | - | unsigned char | - | 10,0 | 1 | 0,0 |
| 0x5862 | Sollwert Öldruck | kPa | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5863 | Innenwiderstand der Nernstzelle der LSU | Ohm | - | unsigned char | - | 0,0390625 | 1 | 0,0 |
| 0x5865 | Langzeit-Ölniveau-Mittelwert für den DIS-Tester | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x5866 | Relativer Füllstand des Motoröls | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5867 | Fahrstrecke des Fahrzeugs als Information über CAN | km | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| 0x5868 | Status Standverbraucher registriert Teil 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5869 | Status Standverbraucher registriert Teil 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x586A | aktuelle Batteriespannung | V | - | unsigned integer | - | 2,500000118743628E-4 | 1 | 6,0 |
| 0x586B | Zeit, indem der Ruhestrom bei 80..200mA liegt | min | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| 0x586C | Zeit, indem der Ruhestrom bei 200..1000mA liegt | min | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| 0x586E | Zeit, indem der Ruhestrom größer als 1000mA liegt | min | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| 0x586F | Öldruck | hPa | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5870 | Spannung Umgebungsdrucksensor (word 10-Bit von ADC) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5871 | Zähler Prüfzustand für VVT Endstufenprüfung | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5872 | Reglerversion on Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5874 | ADC-Spannung Pumpenstrom Tankdiagnose | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x5875 | Indiziertes Soll-Motormoment MSR | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5876 | Schnittstelle für Scan Tool Mode $01/$02 Raildruck Rohwert PID$23 | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x5878 | I-Anteil der stetigen LRSHK Variante kontinuierlich | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x587B | Anzahl erkannter VVT Lageregelungsfehlerwarnungen irreversibel | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x587E | Anzahl erkannter VVT Lageregelungsfehlerwarnungen reversibel | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x587F | Tastverhältnis E-Lüfter | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5880 | Tastverhältnis GLF System | % | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5881 | Ist-Gang | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5882 | Motorstarttemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5883 | [0] Spannung Klopfwerte Zylinder 1 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5884 | Kopie begrenzter Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x5885 | [2] Referenzpegel Klopfregelung, 16bit | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5886 | [3] Referenzpegel Klopfregelung, 16bit | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5887 | Auslastungsgrad Generator 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5888 | [5] Spannung Klopfwerte Zylinder 4 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5889 | Lambda-Istwert | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x588B | Zeit nach Startende | s | - | unsigned integer | - | 0,009999999776482582 | 1 | 0,0 |
| 0x588C | Keramiktemperatur der LSU | Grad C | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| 0x588D | aktuelle Zeit Leckmessung | s | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x588E | Pumpenstrom Tankdiagnose | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x5891 | Kupplungsmotormoment Istwert | Nm | - | signed integer | - | 0,5 | 1 | 0,0 |
| 0x5893 | Indiziertes Soll-Motormoment GS für schnellen Eingriff | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5894 | [4] Spannung Klopfwerte Zylinder 2 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5895 | [1] Spannung Klopfwerte Zylinder 5 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5896 | Abgastemperatur hinter Hauptkat aus Modell | Grad C | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| 0x5898 | phys. Wert Generatorsollspannung (Volt) für Komponententreiber Generator | V | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| 0x5899 | Bedingung Anforderung Motorrelais einschalten | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x589B | Bedingung unzulässig hoher Motorstrom bei Kurzschluss erkannt | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x589C | Bedingung Freigabe VVT-Endstufe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x589D | Anzahl erkannter VVT Lageregelungsfehler | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x589E | Sollwert Exzenterwinkel VVT | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x589F | Batterietemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x58A0 | Entladung während Ruhestromverletzung | Ah | - | unsigned integer | - | 0,018204445019364357 | 1 | 0,0 |
| 0x58A1 | Umweltbedingung Kilometerstand für Fehlerspeichereintrag | km | - | unsigned integer | - | 8,0 | 1 | 0,0 |
| 0x58A2 | Istwert Exzenterwinkel VVT | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A3 | rel. Exzenterwinkel am oberen mech. Anschlag | Grad | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A4 | Generatorstatus | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58A5 | Vom Generator empfangenes Lastsignal | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58A6 | Relativer Exzenterwinkel | Grad | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A7 | Abstellzeit aus relativem Minutenzähler bis Motorstart | min | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58A8 | rel. Exzenterwinkel am unteren mech. Anschlag | Grad | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A9 | VVT Verstellbereich aus Urlernvorgang | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AA | Verstellbereich des Exzenterwinkels | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AB | DLR für DV-E: Summe der PID-Anteile | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x58AD | Sauerstoffspeichervermögen des Katalysators, temperatur- und luftmassenstrombezogen | mg | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AE | Peridendauer für Massenstrom aus HFM | us | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AF | EKP-Sollvolumenstrom | l | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B0 | Zähler für Lerndauer eines Lernsteps | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B1 | [0] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 1 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B2 | [1] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 5 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B3 | [2] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 3 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B4 | [3] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 6 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B5 | [4] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 2 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B6 | [5] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 4 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B7 | aktueller Bremsdruck | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B8 | Motordrehzahl in der Funktionsüberwachung | 1/min | - | unsigned char | - | 40,0 | 1 | 0,0 |
| 0x58B9 | Pedalsollwert (8 Bit) in der Funktionsüberwachung | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x58BA | Bank mittel eingespritzte effektive relative Krafftstoffmasse (inkl. Reduzierstufe) | % | - | unsigned integer | - | 0,046875 | 1 | 0,0 |
| 0x58BB | Strom für VVT-Motor | A | - | signed integer | - | 0,006103515625 | 1 | 0,0 |
| 0x58BC | relative Luftfüllung in der Funktionsüberwachung | % | - | unsigned char | - | 0,75 | 1 | 0,0 |
| 0x58BD | Status Fehler Überlast VVT1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58BE | DV-E-Adaption: Status Prüfbedingungen | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C0 | VVT-Endstufentemperatur aus Modell | Grad C | - | unsigned integer | - | 0,75 | 1 | -48,0 |
| 0x58C8 | geforderte Drehmomentänderung von der LLR (I-Anteil) | % | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x58C9 | Ansteuerungsmodus für den VVT Motor | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58CA | geforderte MD-Änderung von der LLR (PD-Zündungsanteil) | % | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x58CB | Aufsummierte thermische Belastung VVT | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58CC | Tastverhältnis zur Ansteuerung des VVT-Stellmotors | % | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x58CD | Spannung hinter VVT-Relais | V | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58CE | Carrierbyte Schalterstati | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58CF | Momentenanforderung vom Getriebe in der Funktionsüberwachung | Nm | - | signed integer | - | 0,0625 | 1 | 0,0 |
| 0x58D0 | Berechnetes Ist-Moment in der Funktionsüberwachung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58D2 | Status Luftklappensystem High Byte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58D3 | Status Luftklappensystem Low Byte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58D4 | Startbedingung Kraftschluss erfüllt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x58D5 | physikalischer Temperaturwert, der sich bei Wandlung der elektrischen Sensorspannung wtfa1_w ergibt | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x58D7 | Spannungswert des Ansauglufttemperatursensors tfa1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x58D8 | Differenz-DK-Winkel Sollwert - Istwert (wdkdlr_w - wdkba_w) | %DK | - | signed integer | - | 0,0244140625 | 1 | 0,0 |
| 0x58D9 | Schrittzähler DK-Rückstellfeder-Prüfung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58DA | koordiniertes Moment für Füllung | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x58DB | Fehlerzähler Summe, zählt abgasrelevante Aussetzer über alle Zylinder | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58DC | Intervallzähler für abgasrelevante Aussetzer | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58DD | Druck vor Drosselklappe Rohwert | hPa | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| 0x58DE | Spannung Drucksensor vor Drosselklappe | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x58E0 | Abgleich DK-Modell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58E1 | Abgleich DK-Modell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58E2 | Abgleich EV-Modell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58E3 | Abgleich EV-Modell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58E4 | Ist-Betriebsart | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58E5 | Rotorposition VVT-Motor | ° | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58E6 | Soll-Bestromung VVT-Motor | A | - | signed integer | - | 0,006103515625 | 1 | 0,0 |
| 0x58E9 | empf. Spannung von BSS-Wasserpumpe | V | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58EA | empf. Istdrehzahl von BSS-Wasserpumpe | 1/min | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58EC | empf. Temperatur von BSS-Wasserpumpe | Grad C | - | unsigned char | - | 1,0 | 1 | -50,0 |
| 0x58ED | empf. Strom von BSS-Wasserpumpe | % | - | unsigned char | - | 0,5 | 1 | 0,0 |
| 0x58EF | Gefilterter Raildruck-Istwert (Absolutdruck) | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x58F0 | ungefilterter Raildruck Istwert (abs.) | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x58F2 | PWM signal for the VCV | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x58F3 | Ungefilterter Niederdruck Rohwert | kPa | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58F4 | Spannung Kraftstoffniederdrucksensor im 1 ms Raster | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x58F5 | Spannung Diagnose-Port VVT-Ansteuerung (3V ADC) | V | - | unsigned char | - | 0,012890624813735485 | 1 | 0,0 |
| 0x58F6 | Sollspannung des VVT Lagereglers | V | - | signed integer | - | 7,812500116415322E-4 | 1 | 0,0 |
| 0x58F7 | Statusbyte Strommessung plausibel | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58FA | gefilterter Faktor Tankentlüftungs-Adaption | - | - | signed char | - | 0,5 | 1 | 0,0 |
| 0x58FC | Fertigungs-Werkstatt-,Transportmodus | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58FF | Umweltbedingung unbekannt | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x5A02 | ATL-Leckagediagnose läuft | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A04 | Spannung PWG-Poti 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A05 | Spannung PWG-Poti 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A06 | Spannung DK-Poti 1 | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x5A07 | Spannung DK-Poti 2 | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x5A08 | Spannungswert des Ansauglufttemperatursensors tfa1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A09 | Signalspannung des Kühlmitteltemperatursensor | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A0B | Spannung Umgebungsdrucksensor (word 10-Bit von ADC) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A0C | Spannungswert des Ansauglufttemperatursensors tfa2 (SY_TFAKON &gt; 0) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A0E | Wert Temperatur Steuergerät | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5A11 | Spannung Lambdasonde vor Katalysator | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A13 | Spannung Lambdasonde hinter Katalysator | V | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| 0x5A14 | Spannung Lambdasonde (4.88mV/LSB) hinter Katalysator 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| 0x5A17 | Spannung Pumpenstrom Tankdiagnose | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A1B | Elektrische Kraftstoffpumpe | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A1D | Spannung Bremsenunterdruck | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A1E | Differenz zwischen Umgebungsdruck und Bremskraftverstärkerdruck von Drucksensor (Rohwert) | hPa | - | signed integer | - | 0,0390625 | 1 | 0,0 |
| 0x5A20 | Peridendauer für Massenstrom aus HFM | us | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5A21 | Kühlmitteltemperatur (Sensorwert) nach Tiefpassfilterung | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5A23 | Sollwert Öldruck | kPa | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5A24 | Sollwert Drosselklappenwinkel, bezogen auf (unteren) Anschlag | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A25 | Öldruck | hPa | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A29 | normierter Fahrpedalwinkel | %PED | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| 0x5A2B | physikalischer Temperaturwert, ergibt sich bei Wandlung der tiefpassgefilterten Sensorspg. wtfa1f_w | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5A2D | Saugrohr-Absolutdruck gemessen | hPa | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| 0x5A2E | Ungefilterter Niederdruck Rohwert | kPa | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5A2F | Gefilterter Raildruck-Istwert (Absolutdruck) | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x5A30 | [0] Laufunruhe Zylinder 1 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A31 | [4] Laufunruhe Zylinder 2 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A32 | [2] Laufunruhe Zylinder 3 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A33 | [5] Laufunruhe Zylinder 4 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A34 | [1] Laufunruhe Zylinder 5 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A35 | [3] Laufunruhe Zylinder 6 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A36 | Bedingung für erkannte Klopfer | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A37 | [0] normierter Referenzpegel Klopfregelung Zylinder 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A38 | [4] normierter Referenzpegel Klopfregelung Zylinder 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A39 | [2] normierter Referenzpegel Klopfregelung Zylinder 3 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A3A | [5] normierter Referenzpegel Klopfregelung Zylinder 4 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A3B | [1] normierter Referenzpegel Klopfregelung Zylinder 5 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A3C | [3] normierter Referenzpegel Klopfregelung Zylinder 6 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A49 | [0] Ausgegebener Zündwinkel | Grad KW | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5A4B | relative Luftmasse (calc. load value) nach SAE J1979 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A50 | Lambda-Istwert | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5A51 | Lambda-Istwert Bank2 | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5A52 | Bedingung Sonde betriebsbereit hinter Kat | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A53 | Bedingung Sonde betriebsbereit hinter Kat Bank2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A54 | Bedingung Sonde hinter Kat ausreichend beheizt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A55 | Bedingung Sonde 2 hinter Kat ausreichend beheizt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A56 | Bedingung: Heizerstatus A liegt vor, Sonde ist ausreichend aufgeheizt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A57 | Bedingung: Heizerstatus A liegt vor, Sonde ist ausreichend aufgeheizt, Bank2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A58 | Tastverhältnis für Lambdasondenheizung | % | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x5A59 | normierte Heizleistung der Lambdasonde hinter Kat | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x5A5A | Tastverhältnis für Lambdasondenheizung, Bank 2 | % | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x5A60 | Bedingung Bremslichtschalter betätigt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A61 | Bedingung Bremstestschalter betätigt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A65 | Bedingung Abgasklappe mit Resonator | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A66 | Bedingung DMTL-Pumpenmotor an | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A67 | Bedingung DMTL-Magnetventil an | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A68 | Bedingung Heizung DMTL Portansteuerung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A69 | MIL-Ansteuerung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6A | Lampe FGR Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6B | Bedingung für Ansteuerung EGAS-Fehlerlampe | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6C | Korrekturfaktor für die Kraftstoffmenge | % | - | signed char | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x5A74 | Tastverhältnis Kennfeldthermostat | - | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5A77 | ausgegebenes Tastverhältnis für Tankentlüftungsventil (16 Bit) | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A78 | Bedingung Abgasklappe mit Resonator | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A7A | Tastverhältnis Einlaßnockenwellenregelung Ansteuerung Endstufe(word) | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A7B | Tastverhältnis Auslaßnockenwellenregelung Ansteuerung Endstufe(word) | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A81 | Lambda-Regler-Ausgang (Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5A85 | multiplikative Gemischkorrektur der Gemischadaption (Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5A91 | Amplitudenverhältnis laafh/laafv gefiltert | - | - | unsigned char | - | 0,00390625 | 1 | 0,0 |
| 0x5A93 | Fehlerzähler für Lernen Nullgang | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5A94 | gespeicherter Nockenwellensollwinkel Auslaß | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x5A95 | [0] Adaptionswert Nockenwelle Auslass Bank 1 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x5A96 | [0] Adaptionswert Nockenwelle Einlass Bank 1 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x5A97 | Bedi. Vanos Einlass im Anschlag | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A99 | Status der fuel-off Adaption im aktuellen Betriebsbereich | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5A9D | multiplikative Gemischkorrektur der Gemischadaption | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5AA1 | Zyklusflag: Tankentlüftungsventil Endstufe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AA2 | Funktionsstatus-Zähler DM-TL für Testerausgabe aus letztem Fahrzyklus | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AA4 | Funktionsstatus LLRNS bei Anforderung Systemcheck | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AA9 | Tastverhältnis GLF System | % | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AAA | Tastverhältnis PWM Ansteuerung Öldruck | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AAB | Tastverhältnis an Endstufe des Ladedruckstellers | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AAC | Tastverhältnis an Endstufe des Ladedruckstellers, Bank 2 | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AB0 | Ladedruck- Sollwert | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x5AB1 | Fahrzeuggeschwindigkeit | km/h | - | unsigned integer | - | 0,0078125 | 1 | 0,0 |
| 0x5AB3 | Zähler für gefahrene Kilometer mit MIL EIN | km | - | unsigned long | - | 0,009999999776482582 | 1 | 0,0 |
| 0x5AB4 | sekundengenauer Betribsstundenzähler als 32 Bitwert | s | - | unsigned long | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5AB6 | Ansauglufttemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5AB7 | Motortemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5AB8 | Spannung Drucksensor Saugrohrdruck (word) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5ABC | Luftmassenfluss gefiltert (Word) | kg/h | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5ABD | Bedingung automatischer Start | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5ABE | I-Regler Mengenregelung Kraftstoffsystem | mg | - | signed integer | - | 0,0211944580078125 | 1 | 0,0 |
| 0x5ABF | Verbrauch ohne Regler | l/h | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 |
| 0x5AC0 | Verbrauch mit Regler | l/h | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 |
| 0x5AC2 | Reset Information  | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AC4 | Raildruck Kraftstoffsystem Sollwert | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x5AC5 | Tastverhältnis Mengensteuerventil | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AC6 | Modus Kraftstoffsystem (Druck-, Mengen-, Max-Regelung) | 0-n | - | 0xFF | ba_vcv_state_text | 1 | 1 | 0 |
| 0x5AD5 | Kraftstofftemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5AD6 | Bedingung Schubabschalten | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5AE2 | Reset Information - Reset-group-ID of the last reset reason | 0-n | - | 0xFF | Reset_GrpID | 1 | 1 | 0 |
| 0x5AE3 | Reset Information - Reset-ID of the last reset | 0-n | - | 0xFFFF | Reset_ID | 1 | 1 | 0 |
| 0x5AE4 | Reset Information - User defined value of the last reset reason | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AEB | Kühlmitteltemperatur &lt; 98°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEC | 98°C =&lt; Kühlmitteltemperatur =&lt; 112°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AED | 113°C =&lt; Kühlmitteltemperatur =&lt; 120°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEE | 121°C =&lt; Kühlmitteltemperatur =&lt; 125°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEF | Kühlmitteltemperatur &gt; 125°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF0 | Motoröltemperatur &lt; 80°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF1 | 80°C =&lt; Motoröltemperatur =&lt; 110°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF2 | 110°C =&lt; Motoröltemperatur =&lt; 135°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF3 | 135°C =&lt; Motoröltemperatur =&lt; 150°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF4 | Motoröltemperatur &gt; 150°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF5 | Getriebeöltemperatur &lt; 80°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF6 | 80°C =&lt; Getriebeöltemperatur =&lt; 109°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF7 | 110°C =&lt; Getriebeöltemperatur =&lt; 124°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF8 | 125°C =&lt; Getriebeöltemperatur =&lt; 129°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF9 | Getriebeöltemperatur &gt; 129°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFA | Umgebungstemperatur &lt; 3°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFB | 3°C =&lt; Umgebungstemperatur =&lt; 19°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFC | 20°C =&lt; Umgebungstemperatur =&lt; 29°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFD | 30°C =&lt; Umgebungstemperatur =&lt; 39°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFE | Umgebungstemperatur &gt; 39°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5B10 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B11 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B12 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B13 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B14 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B15 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B20 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B21 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B22 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B23 | [0] Aussetzerzähler im Abgasintervall Zyl. 1 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B24 | [4] Aussetzerzähler im Abgasintervall Zyl. 2 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B25 | [2] Aussetzerzähler im Abgasintervall Zyl. 3 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B30 | [5] Aussetzerzähler im Abgasintervall Zyl. 4 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B31 | [1] Aussetzerzähler im Abgasintervall Zyl. 5 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B32 | [3] Aussetzerzähler im Abgasintervall Zyl. 6 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |

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
| F_PCODE | ja |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 761 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x2710 | 0x2710 Drosselklappe, Funktion: klemmt dauerhaft |
| 0x2711 | 0x2711 Drosselklappe, Funktion: klemmt kurzzeitig |
| 0x2714 | 0x2714 Drosselklappe, Funktion: schwergängig, zu langsam |
| 0x2774 | 0x2774 Luftmasse, Plausibilität: Luftmasse zu hoch |
| 0x2775 | 0x2775 Luftmasse, Plausibilität: Luftmasse zu niedrig |
| 0x2778 | 0x2778 Luftmassenmesser, Arbeitsbereich: Periodendauer zu niedrig, Luftmasse zu hoch |
| 0x2779 | 0x2779 Luftmassenmesser, Arbeitsbereich: Periodendauer zu groß, Luftmasse zu niedrig |
| 0x277A | 0x277A Luftmassenmesser, Signal: elektrischer Fehler |
| 0x277B | 0x277B Luftmassenmesser, Arbeitsbereich: Periodendauer zu groß, Luftmasse zu hoch |
| 0x277C | 0x277C Luftmassenmesser, Arbeitsbereich: Periodendauer zu niedrig, Luftmasse zu niedrig |
| 0x27D9 | 0x27D9 Fahrpedalmodul, Pedalwertgeber 1, elektrisch: Kurzschluss nach Plus |
| 0x27DA | 0x27DA Fahrpedalmodul, Pedalwertgeber 1, elektrisch: Kurzschluss nach Masse |
| 0x27DB | 0x27DB Fahrpedalmodul, Pedalwertgeber 2, elektrisch: Kurzschluss nach Plus |
| 0x27DC | 0x27DC Fahrpedalmodul, Pedalwertgeber 2, elektrisch: Kurzschluss nach Masse |
| 0x27E4 | 0x27E4 Fahrpedalmodul, Pedalwertgeber: Sammelfehler |
| 0x27E8 | 0x27E8 Fahrpedalmodul, Pedalwertgeber, Plausibilität: Gleichlauffehler zwischen Pedalwertgeber 1 und Pedalwertgeber 2 |
| 0x280E | 0x280E Absolutdrucksensor, Saugrohr, Plausibilität, Nachlauf: Druck zu hoch |
| 0x280F | 0x280F Absolutdrucksensor, Saugrohr, Plausibilität, Nachlauf: Druck zu niedrig |
| 0x281A | 0x281A Absolutdrucksensor, Saugrohr, elektrisch: Kurzschluss nach Plus |
| 0x281B | 0x281B Absolutdrucksensor, Saugrohr, elektrisch: Kurzschluss nach Masse |
| 0x2820 | 0x2820 Absolutdrucksensor, Saugrohr: Sammelfehler |
| 0x283C | 0x283C DME: interner Fehler [Umgebungsdrucksensor: Kurzschluss nach Plus] |
| 0x283D | 0x283D DME: interner Fehler [Umgebungsdrucksensor: Kurzschluss nach Masse] |
| 0x2841 | 0x2841 DME: interner Fehler [Umgebungsdrucksensor, Plausibilität: Druck zu hoch im Nachlauf] |
| 0x2842 | 0x2842 DME: interner Fehler [Umgebungsdrucksensor, Plausibilität: Druck zu niedrig im Nachlauf] |
| 0x2848 | 0x2848 DME: interner Fehler [Umgebungsdrucksensor: Sammelfehler] |
| 0x284C | 0x284C DME: interner Fehler [Umgebungsdrucksensor, Arbeitsbereich: Druck zu hoch] |
| 0x284D | 0x284D DME: interner Fehler [Umgebungsdrucksensor, Arbeitsbereich: Druck zu niedrig] |
| 0x284E | 0x284E DME: interner Fehler [Umgebungsdrucksensor, Plausibilität: Druck unplausibel] |
| 0x284F | 0x284F DME: interner Fehler [Umgebungsdrucksensor, Plausibilität: Druck unplausibel] |
| 0x28A0 | 0x28A0 Drosselklappenwinkel - Absolutdruck Saugrohr, Vergleich: Druck zu hoch |
| 0x28A1 | 0x28A1 Drosselklappenwinkel - Absolutdruck Saugrohr, Vergleich: Druck zu niedrig |
| 0x28A4 | 0x28A4 Drosselklappe, Drosselklappenpotenziometer 1, elektrisch: Kurzschluss nach Plus |
| 0x28A5 | 0x28A5 Drosselklappe, Drosselklappenpotenziometer 1, elektrisch: Kurzschluss nach Masse |
| 0x28A6 | 0x28A6 Drosselklappe, Drosselklappenpotenziometer 1: Signal unplausibel zur Luftmasse |
| 0x28A8 | 0x28A8 Drosselklappe, Drosselklappenpotenziometer 2, elektrisch: Kurzschluss nach Plus |
| 0x28A9 | 0x28A9 Drosselklappe, Drosselklappenpotenziometer 2, elektrisch: Kurzschluss nach Masse |
| 0x28AA | 0x28AA Drosselklappe, Drosselklappenpotenziometer 2: Signal unplausibel zur Luftmasse |
| 0x28AC | 0x28AC Drosselklappe, Drosselklappenpotenziometer 1 und 2: Doppelfehler |
| 0x28B0 | 0x28B0 Drosselklappe: Notlauf aktiv |
| 0x28B4 | 0x28B4 Drosselklappe, Drosselklappenpotenziometer, Plausibilität: Gleichlauffehler zwischen Potentiometer 1 und 2 |
| 0x28B8 | 0x28B8 Drosselklappe, Ansteuerung: Kurzschluss |
| 0x28B9 | 0x28B9 Drosselklappe, Ansteuerung: Übertemperatur oder Strom zu hoch |
| 0x28BA | 0x28BA DME, interner Fehler, Ansteuerung Drosselklappe: interner Kommunikationsfehler |
| 0x28BB | 0x28BB Drosselklappe, Ansteuerung: Leitungsunterbrechung |
| 0x28BC | 0x28BC Drosselklappe, schliessende Federprüfung: Abbruch Prüfung, Feder schliesst nicht |
| 0x28BD | 0x28BD Drosselklappe, schliessende Federprüfung: Fehlfunktion |
| 0x28C0 | 0x28C0 Drosselklappe, öffnende Federprüfung: Abbruch Prüfung, Feder öffnet nicht |
| 0x28C1 | 0x28C1 Drosselklappe, öffnende Federprüfung: Fehlfunktion |
| 0x28C4 | 0x28C4 Drosselklappe, Adaption: Notluftposition nicht adaptiert |
| 0x28CC | 0x28CC Drosselklappe, Adaption: Randbedingungen nicht erfüllt |
| 0x28CD | 0x28CD Drosselklappe, Adaption: Randbedingungen nicht erfüllt, Batteriespannung zu niedrig |
| 0x28D0 | 0x28D0 Drosselklappe, Adaption: Erstadaption, unterer Anschlag nicht gelernt |
| 0x28D4 | 0x28D4 Drosselklappe, Adaption: Wiederlernen, unterer Anschlag nicht gelernt |
| 0x28D8 | 0x28D8 Drosselklappensteller, Verstärkerabgleich: Fehlfunktion |
| 0x28D9 | 0x28D9 Tuningschutz: Luftmasse zu hoch |
| 0x2904 | 0x2904 Ladelufttemperatursensor: Sammelfehler |
| 0x2906 | 0x2906 Ansaugluftsystem: Verdacht auf Undichtigkeit zwischen Turbolader und Einlassventilen |
| 0x2908 | 0x2908 Ladelufttemperatursensor: Sammelfehler |
| 0x290A | 0x290A Ansauglufttemperatursensor: Sammelfehler |
| 0x2936 | 0x2936 Kühlmitteltemperatursensor, elektrisch: Kurzschluss nach Masse |
| 0x2937 | 0x2937 Kühlmitteltemperatursensor, elektrisch: Kurzschluss nach Plus |
| 0x293A | 0x293A Kühlmitteltemperatursensor, Plausibilität, Kaltstart: Temperatur zu hoch |
| 0x293B | 0x293B Kühlmitteltemperatursensor, Plausibilität, Kaltstart: Temperatur zu niedrig |
| 0x293E | 0x293E Kühlmitteltemperatursensor: Sammelfehler |
| 0x2942 | 0x2942 Kühlmitteltemperatursensor, elektrisch: Signal fehlt |
| 0x2943 | 0x2943 Kühlmitteltemperatursensor, Signaländerung: zu schnell |
| 0x2946 | 0x2946 Kühlmitteltemperatursensor, Plausibilität: Motortemperatur gegenüber Modell unplausibel zu hoch |
| 0x2947 | 0x2947 Kühlmitteltemperatursensor, Signal: festliegend auf niedrig |
| 0x2948 | 0x2948 Kühlmitteltemperatursensor, Signal: festliegend |
| 0x299A | 0x299A Außentemperatursensor, Signal: Oberen Schwellwert überschritten |
| 0x299B | 0x299B Außentemperatursensor, Signal: Unteren Schwellwert unterschritten |
| 0x299C | 0x299C Außentemperatursensor, Signal: CAN-Botschaft fehlerhaft |
| 0x299E | 0x299E Außentemperatursensor, Sammelfehler: elektrisch und Plausibilität |
| 0x29A2 | 0x29A2 Außentemperatursensor, Plausibilität: Umgebungstemperatur größer als Modelltemperatur |
| 0x29A3 | 0x29A3 Außentemperatursensor, Plausibilität: Umgebungstemperatur kleiner als Modelltemperatur |
| 0x29CC | 0x29CC Ansauglufttemperatursensor, Plausibilität, Kaltstart: Temperatur zu hoch |
| 0x29CD | 0x29CD Ansauglufttemperatursensor, Plausibilität, Kaltstart: Temperatur zu niedrig |
| 0x29D0 | 0x29D0 Ansauglufttemperatursensor, elektrisch: Kurzschluss nach Plus |
| 0x29D1 | 0x29D1 Ansauglufttemperatursensor, elektrisch: Kurzschluss nach Masse |
| 0x29D2 | 0x29D2 Ansauglufttemperatursensor, Signaländerung: zu schnell |
| 0x29D8 | 0x29D8 Ansauglufttemperatur - Ladelufttemperatur, Vergleich: Ansauglufttemperatur zu hoch |
| 0x29D9 | 0x29D9 Ansauglufttemperatur - Ladelufttemperatur, Vergleich: Ansauglufttemperatur zu niedrig |
| 0x29DC | 0x29DC Ladelufttemperatursensor, Plausibilität, Kaltstart: Temperatur zu hoch |
| 0x29DD | 0x29DD Ladelufttemperatursensor, Plausibilität, Kaltstart: Temperatur zu niedrig |
| 0x29E0 | 0x29E0 Ladelufttemperatursensor, elektrisch: Kurzschluss nach Plus |
| 0x29E1 | 0x29E1 Ladelufttemperatursensor, elektrisch: Kurzschluss nach Masse |
| 0x29E2 | 0x29E2 Ladelufttemperatursensor, Spannungsänderung: zu schnell |
| 0x29E4 | 0x29E4 Ladelufttemperatur, Plausibilität: Temperatur zu hoch |
| 0x29E5 | 0x29E5 Ladelufttemperatur, Signal: festliegend |
| 0x29E6 | 0x29E6 Ladelufttemperatursensor, Kaltstart: Sammelfehler |
| 0x29E7 | 0x29E7 Ladelufttemperatursensor: Sammelfehler |
| 0x29E8 | 0x29E8 Ladelufttemperatursensor, Signaländerung: zu schnell |
| 0x29FE | 0x29FE Injektor Zylinder 1, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x29FF | 0x29FF Injektor Zylinder 1, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A00 | 0x2A00 Injektor Zylinder 1, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A01 | 0x2A01 Injektor Zylinder 1, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A02 | 0x2A02 Injektor Zylinder 2, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x2A03 | 0x2A03 Injektor Zylinder 2, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A04 | 0x2A04 Injektor Zylinder 2, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A05 | 0x2A05 Injektor Zylinder 2, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A06 | 0x2A06 Injektor Zylinder 3, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x2A07 | 0x2A07 Injektor Zylinder 3, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A08 | 0x2A08 Injektor Zylinder 3, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A09 | 0x2A09 Injektor Zylinder 3, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A0A | 0x2A0A Injektor Zylinder 4, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x2A0B | 0x2A0B Injektor Zylinder 4, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A0C | 0x2A0C Injektor Zylinder 4, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A0D | 0x2A0D Injektor Zylinder 4, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A0E | 0x2A0E Injektor Zylinder 5, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x2A0F | 0x2A0F Injektor Zylinder 5, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A10 | 0x2A10 Injektor Zylinder 5, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A11 | 0x2A11 Injektor Zylinder 5, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A12 | 0x2A12 Injektor Zylinder 6, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse |
| 0x2A13 | 0x2A13 Injektor Zylinder 6, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus |
| 0x2A14 | 0x2A14 Injektor Zylinder 6, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus |
| 0x2A15 | 0x2A15 Injektor Zylinder 6, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse |
| 0x2A30 | 0x2A30 Injektor Zylinder 1, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A31 | 0x2A31 Injektor Zylinder 2, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A32 | 0x2A32 Injektor Zylinder 3, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A33 | 0x2A33 Injektor Zylinder 4, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A34 | 0x2A34 Injektor Zylinder 5, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A35 | 0x2A35 Injektor Zylinder 6, Ansteuerung: Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x2A40 | 0x2A40 Injektor Zylinder 1, Stromanstieg: zu langsam |
| 0x2A41 | 0x2A41 Injektor Zylinder 2, Stromanstieg: zu langsam |
| 0x2A42 | 0x2A42 Injektor Zylinder 3, Stromanstieg: zu langsam |
| 0x2A43 | 0x2A43 Injektor Zylinder 4, Stromanstieg: zu langsam |
| 0x2A44 | 0x2A44 Injektor Zylinder 5, Stromanstieg: zu langsam |
| 0x2A45 | 0x2A45 Injektor Zylinder 6, Stromanstieg: zu langsam |
| 0x2A4C | 0x2A4C Injektor Zylinder 1, Ansteuerung: Leitungsunterbrechung |
| 0x2A4D | 0x2A4D Injektor Zylinder 2, Ansteuerung: Leitungsunterbrechung |
| 0x2A4E | 0x2A4E Injektor Zylinder 3, Ansteuerung: Leitungsunterbrechung |
| 0x2A4F | 0x2A4F Injektor Zylinder 4, Ansteuerung: Leitungsunterbrechung |
| 0x2A50 | 0x2A50 Injektor Zylinder 5, Ansteuerung: Leitungsunterbrechung |
| 0x2A51 | 0x2A51 Injektor Zylinder 6, Ansteuerung: Leitungsunterbrechung |
| 0x2A5F | 0x2A5F Relais Zündung und Injektoren, Versorgungsspannung Einspritzung: Kurzschluss nach Plus |
| 0x2A60 | 0x2A60 Relais Zündung und Injektoren, Versorgungsspannung Einspritzung: Kurzschluss nach Masse |
| 0x2A61 | 0x2A61 Relais Zündung und Injektoren, Versorgungsspannung Einspritzung: Leitungsunterbrechung |
| 0x2A70 | 0x2A70 DME, interner Fehler, HDEV-Endstufen-Baustein 1: SPI-Kommunikation fehlerhaft |
| 0x2A71 | 0x2A71 DME, interner Fehler, HDEV-Endstufen-Baustein 2: SPI-Kommunikation fehlerhaft |
| 0x2A72 | 0x2A72 DME, interner Fehler, HDEV-Endstufen-Baustein 1: SPI-Kommunikation unplausibel |
| 0x2A73 | 0x2A73 DME, interner Fehler, HDEV-Endstufen-Baustein 2: SPI-Kommunikation unplausibel |
| 0x2A74 | 0x2A74 DME, interner Fehler, HDEV-Endstufen-Baustein 1: SPI-Kommunikation gestört |
| 0x2A75 | 0x2A75 DME, interner Fehler, HDEV-Endstufen-Baustein 2: SPI-Kommunikation gestört |
| 0x2BC0 | 0x2BC0 Gemischregelung: Gemisch zu mager |
| 0x2BC1 | 0x2BC1 Gemischregelung: Gemisch zu fett |
| 0x2BC2 | 0x2BC2 Gemischadaption, Leerlauf: Gemisch zu mager |
| 0x2BC3 | 0x2BC3 Gemischadaption, Leerlauf: Gemisch zu fett |
| 0x2BC5 | 0x2BC5 Gemischadaption, Injektor-Alterung: Zylinderseite 1: langfristige Adaption zu hoch |
| 0x2BCA | 0x2BCA Lambdasonde vor Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu fett |
| 0x2BCB | 0x2BCB Lambdasonde vor Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu mager |
| 0x2BD9 | 0x2BD9 Raildrucksensor, elektrisch: Kurzschluss nach Plus |
| 0x2BDA | 0x2BDA Raildrucksensor, elektrisch: Kurzschluss nach Masse |
| 0x2BDB | 0x2BDB Kraftstoffhochdruck, Plausibilität: Druck zu hoch, Notlauf mit Niederdruck |
| 0x2BDC | 0x2BDC Kraftstoffversorgungssystem: Druck zu hoch, Notlauf mit Einspritzabschaltung |
| 0x2BDD | 0x2BDD Kraftstoffhochdruck: Druck kurzzeitig zu hoch, Drehzahl- und Lastbegrenzung |
| 0x2BDE | 0x2BDE Kraftstoffhochdruck bei Freigabe der Einspritzung: Druck zu niedrig |
| 0x2BDF | 0x2BDF Kraftstoffniederdrucksystem, Plausibilität: Leistung elektrische Kraftstoffpumpe für Istdruck zu hoch |
| 0x2BE0 | 0x2BE0 Kraftstoffniederdrucksystem: Leistung elektrische Kraftstoffpumpe für Istdruck zu niedrig |
| 0x2BE1 | 0x2BE1 Kraftstoffniederdrucksystem, Plausibilität: Förderleistung zu niedrig |
| 0x2BE2 | 0x2BE2 Kraftstoffniederdrucksystem, Plausibilität: Spannung elektrische Kraftstoffpumpe unplausibel |
| 0x2BE3 | 0x2BE3 Kraftstoffniederdruck, Arbeitsbereich: Druck zu niedrig |
| 0x2BE4 | 0x2BE4 Kraftstoffniederdruck, Arbeitsbereich: Druck zu hoch |
| 0x2BE5 | 0x2BE5 Kraftstoffhochdrucksystem, Plausibilität: Regelabweichung des Mengensteuerventils zu groß |
| 0x2BE6 | 0x2BE6 Kraftstoffhochdrucksystem, Plausibilität: Regelabweichung des Mengensteuerventils zu klein |
| 0x2BE9 | 0x2BE9 Zylindereinspritzabschaltung: Druck zu niedrig im Hochdrucksystem |
| 0x2BEA | 0x2BEA Gemischregelung: Gemisch zu mager, große Abweichung |
| 0x2BEB | 0x2BEB Gemischregelung: Gemisch zu fett, große Abweichung |
| 0x2BEC | 0x2BEC Kraftstoffhochdruck nach Motorstopp: Druck zu hoch |
| 0x2BED | 0x2BED Kraftstoffhochdruck, Plausibilität, Kaltstart: Druck zu hoch |
| 0x2BEE | 0x2BEE Kraftstoffhochdruck, Plausibilität, Kaltstart: Druck zu niedrig |
| 0x2BEF | 0x2BEF Kraftstoffhochdruck nach Freigabe der Einspritzung: Druck zu niedrig |
| 0x2BF0 | 0x2BF0 Kraftstoffhochdruck bei oder nach Freigabe der Einspritzung (2. Umweltbedingungssatz nach Zeitverzögerung): Druck zu niedrig |
| 0x2BF2 | 0x2BF2 Raildrucksensor, Arbeitsbereich: Druck zu hoch |
| 0x2BF3 | 0x2BF3 Raildrucksensor, Arbeitsbereich: Druck zu niedrig |
| 0x2BF4 | 0x2BF4 Raildrucksensor, Plausibilität: Druck zu hoch vor Motorstart |
| 0x2BF5 | 0x2BF5 Raildrucksensor, Plausibilität: Druck zu niedrig vor Motorstart |
| 0x2BF6 | 0x2BF6 Kraftstoffniederdrucksensor, elektrisch: Kurzschluss nach Plus |
| 0x2BF7 | 0x2BF7 Kraftstoffniederdrucksensor, elektrisch: Kurzschluss nach Masse |
| 0x2BF8 | 0x2BF8 Raildrucksensor, Signal: festliegend |
| 0x2C00 | 0x2C00 Kraftstoffhochdruck, Plausibilität: Druck zu hoch |
| 0x2C01 | 0x2C01 Kraftstoffhochdruck, Plausibilität: Druck zu niedrig |
| 0x2C3D | 0x2C3D Mengensteuerventil, Ansteuerung: Kurzschluss nach Plus |
| 0x2C3E | 0x2C3E Mengensteuerventil, Ansteuerung: Kurzschluss nach Masse |
| 0x2C3F | 0x2C3F Mengensteuerventil, Ansteuerung: Leitungsunterbrechung |
| 0x2C42 | 0x2C42 Gemischregelung: Sammelfehler |
| 0x2C56 | 0x2C56 Ladedruckregelung, Plausibilität: Druck zu hoch |
| 0x2C57 | 0x2C57 Ladedruckregelung, Plausibilität: Druck zu niedrig |
| 0x2C58 | 0x2C58 Ladedruckregelung: Abschaltung als Folgereaktion |
| 0x2C6F | 0x2C6F Ladedrucksensor, elektrisch: Kurzschluss nach Plus |
| 0x2C70 | 0x2C70 Ladedrucksensor, elektrisch: Kurzschluss nach Masse |
| 0x2C71 | 0x2C71 Ladedrucksensor, Plausibilität, Nachlauf: Druck zu hoch |
| 0x2C72 | 0x2C72 Ladedrucksensor, Plausibilität, Nachlauf: Druck zu niedrig |
| 0x2C7F | 0x2C7F Ladedrucksensor: Sammelfehler |
| 0x2C83 | 0x2C83 Ladedruck, Plausibilität: Druck zu hoch |
| 0x2C84 | 0x2C84 Ladedruck, Arbeitsbereich: Druck zu niedrig |
| 0x2C85 | 0x2C85 Ladedruck - Umgebungsdruck, Vergleich: Ladedruck zu hoch |
| 0x2C86 | 0x2C86 Ladedruck - Umgebungsdruck, Vergleich: Ladedruck zu niedrig |
| 0x2C88 | 0x2C88 Schubumluftventil, Ansteuerung: Kurzschluss nach Plus |
| 0x2C89 | 0x2C89 Schubumluftventil, Ansteuerung: Kurzschluss nach Masse |
| 0x2C8A | 0x2C8A Schubumluftventil, Ansteuerung: Leitungsunterbrechung |
| 0x2C90 | 0x2C90 Schubumluftventil: klemmt geschlossen |
| 0x2C91 | 0x2C91 Schubumluftventil, Mechanik: Verdacht auf offen klemmendes Schubumluftventil |
| 0x2CA1 | 0x2CA1 Wastegate, Ansteuerung: Kurzschluss nach Plus |
| 0x2CA2 | 0x2CA2 Wastegate, Ansteuerung: Kurzschluss nach Masse |
| 0x2CA3 | 0x2CA3 Wastegate, Ansteuerung: Leitungsunterbrechung |
| 0x2CB3 | 0x2CB3 Wastegate, Ansteuerung: Verdacht auf Fehler in der Wastegateansteuerung |
| 0x2CED | 0x2CED Lambdasonde nach Katalysator, Dynamik, von Fett nach Mager: langsame Reaktion |
| 0x2CEE | 0x2CEE Lambdasondenbeheizung vor Katalysator, Funktion: Heizelement fehlerhaft |
| 0x2CF4 | 0x2CF4 Lambdasonde vor Katalysator, Dynamik: langsame Reaktion |
| 0x2CF8 | 0x2CF8 Lambdasonde vor Katalysator: Falschluft erkannt |
| 0x2CFA | 0x2CFA Lambdasonde vor Katalysator, elektrisch: Unterbrechung Nernstleitung |
| 0x2CFE | 0x2CFE Lambdasonde vor Katalysator, Leitungsfehler: Unterbrechung Abgleichleitung |
| 0x2CFF | 0x2CFF Lambdasonde vor Katalysator, Signalleitungen: Kurzschluss nach Plus |
| 0x2D00 | 0x2D00 Lambdasonde vor Katalysator, Signalleitungen: Kurzschluss nach Masse |
| 0x2D03 | 0x2D03 DME, interner Fehler, Lambdasonde vor Katalysator: Lambdasondenbaustein, Signalkreisadaptionswerte zu hoch |
| 0x2D04 | 0x2D04 DME, interner Fehler, Lambdasonde vor Katalysator: Lambdasondenbaustein, Unterspannung |
| 0x2D05 | 0x2D05 DME, interner Fehler, Lambdasonde vor Katalysator: Initialisierungsfehler |
| 0x2D06 | 0x2D06 DME, interner Fehler, Lambdasonde vor Katalysator: Kommunikationsfehler |
| 0x2D0B | 0x2D0B Lambdasondenbeheizung vor Katalysator, Ansteuerung: Kurzschluss nach Plus |
| 0x2D0C | 0x2D0C Lambdasondenbeheizung vor Katalysator, Ansteuerung: Kurzschluss nach Masse |
| 0x2D0D | 0x2D0D Lambdasondenbeheizung vor Katalysator, Ansteuerung: Leitungsunterbrechung |
| 0x2D0F | 0x2D0F Lambdasondenbeheizung nach Katalysator, Ansteuerung: Kurzschluss nach Plus |
| 0x2D10 | 0x2D10 Lambdasondenbeheizung nach Katalysator, Ansteuerung: Kurzschluss nach Masse |
| 0x2D11 | 0x2D11 Lambdasondenbeheizung nach Katalysator, Ansteuerung: Leitungsunterbrechung |
| 0x2D13 | 0x2D13 Lambdasondenbeheizung nach Katalysator, Funktion: Innenwiderstand zu hoch |
| 0x2D15 | 0x2D15 Lambdasonde nach Katalysator, im Schub, von Fett nach Mager: verzögerte Reaktion |
| 0x2D17 | 0x2D17 Lambdasondenbeheizung vor Katalysator, Funktion: Betriebstemperatur nicht erreicht |
| 0x2D18 | 0x2D18 Lambdasondenbeheizung vor Katalysator, Funktion: Mangelnde Signalbereitschaft |
| 0x2D19 | 0x2D19 Lambdasondenbeheizung vor Katalysator, Funktion: Innenwiderstand des Signalkreises zu hochohmig |
| 0x2D1B | 0x2D1B Lambdasonde nach Katalysator, Systemprüfung: Signal festliegend auf Mager |
| 0x2D1C | 0x2D1C Lambdasonde nach Katalysator, Systemprüfung: Signal festliegend auf Fett |
| 0x2D1E | 0x2D1E Lambdasonde nach Katalysator, Alterung: Schubspannungsschwelle nicht erreicht |
| 0x2D1F | 0x2D1F Lambdasonde nach Katalysator, elektrisch: Kurzschluss nach Plus |
| 0x2D20 | 0x2D20 Lambdasonde nach Katalysator, elektrisch: Kurzschluss nach Masse |
| 0x2D22 | 0x2D22 Lambdasonde nach Katalysator, elektrisch: Leitungsunterbrechung |
| 0x2D23 | 0x2D23 Lambdasonde vor Katalysator, elektrisch: Unterbrechung Pumpstromleitung |
| 0x2D24 | 0x2D24 Lambdasonde vor Katalysator, im Schub: Signal außerhalb Grenzwert |
| 0x2D25 | 0x2D25 Lambdasonde vor Katalysator, elektrisch: Unterbrechung Pumpstromleitung |
| 0x2D27 | 0x2D27 Lambdasonde vor Katalysator, elektrisch: Unterbrechung virtuelle Masse |
| 0x2D2B | 0x2D2B Lambdasonde vor Katalysator, elektrisch: Nernstzellenwiderstand oder Keramiktemperatur unplausibel, Leitungs- oder Heizungsfehler |
| 0x2D2F | 0x2D2F Lambdasonde vor Katalysator: Sammelfehler |
| 0x2D33 | 0x2D33 Lambdasonde vor Katalysator, Systemprüfung: Signal festliegend auf Mager |
| 0x2D34 | 0x2D34 Lambdasonde vor Katalysator, Systemprüfung: Signal festliegend auf Fett |
| 0x2D35 | 0x2D35 Lambdasonde vor Katalysator, Systemprüfung: Signal festliegend auf Mager |
| 0x2D36 | 0x2D36 Lambdasonde vor Katalysator, Systemprüfung: Signal festliegend auf Fett |
| 0x2D41 | 0x2D41 Valvetronic, Verstellbereich: Urlernen ausserhalb Toleranzen |
| 0x2D42 | 0x2D42 Valvetronic, Verstellbereich: Anschlag nicht gelernt |
| 0x2D43 | 0x2D43 Valvetronic, Verstellbereich: Fehler Bereichsüberprüfung |
| 0x2D44 | 0x2D44 Valvetronic, Verstellbereich: Bereichsüberprüfung Abweichung zu Urlernen |
| 0x2D45 | 0x2D45 Valvetronic, Verstellbereich: Anschlag nicht gelernt wegen Umweltbedingungen |
| 0x2D51 | 0x2D51 VANOS-Magnetventil Einlass, Ansteuerung: Kurzschluss nach Plus |
| 0x2D52 | 0x2D52 VANOS-Magnetventil Einlass, Ansteuerung: Kurzschluss nach Masse |
| 0x2D53 | 0x2D53 VANOS-Magnetventil Einlass, Ansteuerung: Leitungsunterbrechung |
| 0x2D54 | 0x2D54 VANOS, Auslass, Kaltstart: nicht regelbar |
| 0x2D55 | 0x2D55 VANOS, Einlass, Kaltstart: nicht regelbar |
| 0x2D5A | 0x2D5A VANOS, Einlass: Regelfehler, Nockenwelle klemmt |
| 0x2D5B | 0x2D5B VANOS, Einlass: Regelfehler, Position nicht erreicht |
| 0x2D60 | 0x2D60 VANOS, Auslass: Regelfehler, Nockenwelle klemmt |
| 0x2D61 | 0x2D61 VANOS, Auslass: Regelfehler, Position nicht erreicht |
| 0x2D9B | 0x2D9B VANOS-Magnetventil Auslass, Ansteuerung: Kurzschluss nach Plus |
| 0x2D9C | 0x2D9C VANOS-Magnetventil Auslass, Ansteuerung: Kurzschluss nach Masse |
| 0x2D9D | 0x2D9D VANOS-Magnetventil Auslass, Ansteuerung: Leitungsunterbrechung |
| 0x2D9F | 0x2D9F Einlassnockenwellensensor, Plausibilität: Signal unplausibel |
| 0x2DA0 | 0x2DA0 Einlassnockenwelle: Winkelversatz zur Kurbelwelle außerhalb Toleranz |
| 0x2DA1 | 0x2DA1 Auslassnockenwellensensor, Plausibilität: Signal unplausibel |
| 0x2DA2 | 0x2DA2 Auslassnockenwelle: Winkelversatz zur Kurbelwelle außerhalb Toleranz |
| 0x2DAD | 0x2DAD VANOS, Auslass: Sammelfehler |
| 0x2DAE | 0x2DAE VANOS, Einlass: Sammelfehler |
| 0x2DAF | 0x2DAF VANOS: Sammelfehler |
| 0x2DB0 | 0x2DB0 VANOS, Auslass: Nockenwelle beim Start nicht in Verriegelungsposition |
| 0x2DB1 | 0x2DB1 VANOS, Einlass: Nockenwelle beim Start nicht in Verriegelungsposition |
| 0x2DB4 | 0x2DB4 Valvetronic-Relais, Ansteuerung: Kurzschluss nach Plus |
| 0x2DB5 | 0x2DB5 Valvetronic-Relais, Ansteuerung: Kurzschluss nach Masse |
| 0x2DB6 | 0x2DB6 Valvetronic-Relais, Ansteuerung: Leitungsunterbrechung |
| 0x2DBA | 0x2DBA Valvetronic: Bauteileschutz, Abschaltung System |
| 0x2DBB | 0x2DBB Valvetronic-Stellmotor: Bauteileschutz, Abschaltung System |
| 0x2DBC | 0x2DBC Valvetronic, Exzenterwellenadaption: unterer Anschlag erreicht |
| 0x2DBD | 0x2DBD Valvetronic-Stellmotor, Positionssensoren: Exzenterwinkel falsch |
| 0x2DBF | 0x2DBF Valvetronic-Stellmotor, Ansteuerung: Kurzschluss nach Plus |
| 0x2DC0 | 0x2DC0 Valvetronic-Stellmotor, Ansteuerung: Kurzschluss nach Masse |
| 0x2DC3 | 0x2DC3 Valvetronic-Stellmotor, Ansteuerung: Leitungsunterbrechung |
| 0x2DC4 | 0x2DC4 Valvetronic-Stellmotor, Ansteuerung: Abschaltung im Fahrbetrieb |
| 0x2DCA | 0x2DCA Valvetronic: Endstufe überlastet |
| 0x2DCB | 0x2DCB Valvetronic-Stellmotor: Überlastung |
| 0x2DCC | 0x2DCC Valvetronic: Warnschwelle Überlastschutz überschritten |
| 0x2DCD | 0x2DCD Valvetronic-Stellmotor: Warnschwelle Überlastschutz überschritten |
| 0x2DCE | 0x2DCE Valvetronic System: keine Verstellung möglich |
| 0x2DCF | 0x2DCF Valvetronic System: keine Bewegung erkannt |
| 0x2DD0 | 0x2DD0 Valvetronic System: Warnschwelle Regelabweichung überschritten |
| 0x2DD6 | 0x2DD6 Valvetronic-Stellmotor, Positionssensoren: Kurzschluss oder Leitungsunterbrechung |
| 0x2DD7 | 0x2DD7 Valvetronic-Stellmotor, Positionssensoren: Versorgungsspannung fehlerhaft |
| 0x2DD8 | 0x2DD8 Valvetronic-Stellmotor, Positionssensoren: Signal unplausibel |
| 0x2DE1 | 0x2DE1 Valvetronic-Stellmotor, Positionssensoren, Plausibilität: Feinhallsignale zueinander unplausibel |
| 0x2DE2 | 0x2DE2 Valvetronic-Stellmotor, Ansteuerung Phase U: Leitungsunterbrechung |
| 0x2DE3 | 0x2DE3 Valvetronic-Stellmotor, Ansteuerung Phase V: Leitungsunterbrechung |
| 0x2DE4 | 0x2DE4 Valvetronic-Stellmotor, Ansteuerung Phase W: Leitungsunterbrechung |
| 0x2DE5 | 0x2DE5 Valvetronic-Stellmotor: Überlastung |
| 0x2DE6 | 0x2DE6 Valvetronic: Warnschwelle Überlastschutz überschritten |
| 0x2DE7 | 0x2DE7 Valvetronic-Stellmotor: Warnschwelle Überlastschutz überschritten |
| 0x2DE8 | 0x2DE8 Valvetronic: Bauteileschutz, Abschaltung System |
| 0x2DE9 | 0x2DE9 Valvetronic-Stellmotor: Bauteileschutz, Abschaltung System |
| 0x2DEA | 0x2DEA Valvetronic: Endstufe überlastet |
| 0x2E0A | 0x2E0A Valvetronic-Stellmotor, Ansteuerung Phase U: Leitungsunterbrechung |
| 0x2E0B | 0x2E0B Valvetronic-Stellmotor, Ansteuerung Phase V: Leitungsunterbrechung |
| 0x2E0C | 0x2E0C Valvetronic-Stellmotor, Ansteuerung Phase W: Leitungsunterbrechung |
| 0x2E0D | 0x2E0D Valvetronic-Stellmotor, Positionssensoren: Fehler erkannt |
| 0x2E0E | 0x2E0E Valvetronic-Stellmotor, Positionssensoren: Signale unplausibel |
| 0x2E0F | 0x2E0F Valvetronic System: deaktiviert, zu häufiger Verstellfehler |
| 0x2E10 | 0x2E10 Valvetronic System: deaktiviert, Warnschwelle Regelabweichung zu oft überschritten |
| 0x2E11 | 0x2E11 Valvetronic System: unterer Anschlag gelernt |
| 0x2E12 | 0x2E12 Valvetronic System: keine Verstellung möglich |
| 0x2E13 | 0x2E13 Valvetronic System: Warnschwelle Regelabweichung überschritten |
| 0x2E4A | 0x2E4A Abgasklappe, Ansteuerung: Kurzschluss nach Plus |
| 0x2E4B | 0x2E4B Abgasklappe, Ansteuerung: Kurzschluss nach Masse |
| 0x2E4C | 0x2E4C Abgasklappe, Ansteuerung: Leitungsunterbrechung |
| 0x2E7C | 0x2E7C Kühlerjalousie, oben, Eigendiagnose: Hardwaredefekt |
| 0x2E7D | 0x2E7D Kühlerjalousie, oben, Eigendiagnose: mechanischer Fehler |
| 0x2E7E | 0x2E7E Kühlerjalousie, oben, Eigendiagnose: Kommunikationsfehler |
| 0x2E80 | 0x2E80 Kühlerjalousie, Ansteuerung: Kurzschluss nach Plus |
| 0x2E81 | 0x2E81 Kühlerjalousie, Ansteuerung: Kurzschluss nach Masse |
| 0x2E82 | 0x2E82 Kühlerjalousie, Ansteuerung: Leitungsunterbrechung |
| 0x2E84 | 0x2E84 Kühlerjalousie, unten, Eigendiagnose, elektrisch: Fehlfunktion |
| 0x2EE0 | 0x2EE0 Verbrennungsaussetzer, mehrere Zylinder: Einspritzabschaltung |
| 0x2EE1 | 0x2EE1 Verbrennungsaussetzer, mehrere Zylinder: abgasschädigend |
| 0x2EE2 | 0x2EE2 Verbrennungsaussetzer, mehrere Zylinder: abgasschädigend nach Startvorgang |
| 0x2EE4 | 0x2EE4 Verbrennungsaussetzer, Zylinder 1: Einspritzabschaltung |
| 0x2EE5 | 0x2EE5 Verbrennungsaussetzer, Zylinder 1: abgasschädigend |
| 0x2EE6 | 0x2EE6 Verbrennungsaussetzer, Zylinder 1: abgasschädigend nach Startvorgang |
| 0x2EE7 | 0x2EE7 Verbrennungsaussetzer, Zylinder 2: Einspritzabschaltung |
| 0x2EE8 | 0x2EE8 Verbrennungsaussetzer, Zylinder 2: abgasschädigend |
| 0x2EE9 | 0x2EE9 Verbrennungsaussetzer, Zylinder 2: abgasschädigend nach Startvorgang |
| 0x2EEA | 0x2EEA Verbrennungsaussetzer, Zylinder 3: Einspritzabschaltung |
| 0x2EEB | 0x2EEB Verbrennungsaussetzer, Zylinder 3: abgasschädigend |
| 0x2EEC | 0x2EEC Verbrennungsaussetzer, Zylinder 3: abgasschädigend nach Startvorgang |
| 0x2EED | 0x2EED Verbrennungsaussetzer, Zylinder 4: Einspritzabschaltung |
| 0x2EEF | 0x2EEF Verbrennungsaussetzer, Zylinder 4: abgasschädigend |
| 0x2EF0 | 0x2EF0 Verbrennungsaussetzer, Zylinder 4: abgasschädigend nach Startvorgang |
| 0x2EF1 | 0x2EF1 Verbrennungsaussetzer, Zylinder 5: Einspritzabschaltung |
| 0x2EF2 | 0x2EF2 Verbrennungsaussetzer, Zylinder 5: abgasschädigend |
| 0x2EF3 | 0x2EF3 Verbrennungsaussetzer, Zylinder 5: abgasschädigend nach Startvorgang |
| 0x2EF4 | 0x2EF4 Verbrennungsaussetzer, Zylinder 6: Einspritzabschaltung |
| 0x2EF5 | 0x2EF5 Verbrennungsaussetzer, Zylinder 6: abgasschädigend |
| 0x2EF6 | 0x2EF6 Verbrennungsaussetzer, Zylinder 6: abgasschädigend nach Startvorgang |
| 0x2EFE | 0x2EFE Verbrennungsaussetzer, mehrere Zylinder: katalysator- oder abgasschädigend |
| 0x2EFF | 0x2EFF Verbrennungsaussetzer, Zylinder 1: katalysator- oder abgasschädigend |
| 0x2F00 | 0x2F00 Verbrennungsaussetzer, Zylinder 2: katalysator- oder abgasschädigend |
| 0x2F01 | 0x2F01 Verbrennungsaussetzer, Zylinder 3: katalysator- oder abgasschädigend |
| 0x2F02 | 0x2F02 Verbrennungsaussetzer, Zylinder 4: katalysator- oder abgasschädigend |
| 0x2F03 | 0x2F03 Verbrennungsaussetzer, Zylinder 5: katalysator- oder abgasschädigend |
| 0x2F04 | 0x2F04 Verbrennungsaussetzer, Zylinder 6: katalysator- oder abgasschädigend |
| 0x2F44 | 0x2F44 Zündkreis, Versorgungsspannung: Bankausfall oder Motorausfall |
| 0x2F45 | 0x2F45 Laufunruhe, Füllung Einzelzylinder: Momentenbeitrag zu niedrig |
| 0x2F76 | 0x2F76 Superklopfen Zylinder 1: Einspritzungsabschaltung |
| 0x2F77 | 0x2F77 Superklopfen Zylinder 2: Einspritzungsabschaltung |
| 0x2F78 | 0x2F78 Superklopfen Zylinder 3: Einspritzungsabschaltung |
| 0x2F79 | 0x2F79 Superklopfen Zylinder 4: Einspritzungsabschaltung |
| 0x2F7A | 0x2F7A Superklopfen Zylinder 5: Einspritzungsabschaltung |
| 0x2F7B | 0x2F7B Superklopfen Zylinder 6: Einspritzungsabschaltung |
| 0x2F7C | 0x2F7C Superklopfen: Einspritzungsabschaltung |
| 0x2F83 | 0x2F83 Zündwinkelverstellung im Leerlauf, Kaltstart: Zündwinkel zu früh |
| 0x2F84 | 0x2F84 Zündwinkelverstellung in Teillast, Kaltstart: Zündwinkel zu früh |
| 0x2F8A | 0x2F8A Relais Zündung und Injektoren, Versorgungsspannung Zündung: Kurzschluss nach Plus |
| 0x2F8B | 0x2F8B Relais Zündung und Injektoren, Versorgungsspannung Zündung: Kurzschluss nach Masse |
| 0x2FA8 | 0x2FA8 Zündung, Zylinder 1: Brenndauer zu kurz |
| 0x2FA9 | 0x2FA9 Zündung, Zylinder 2: Brenndauer zu kurz |
| 0x2FAA | 0x2FAA Zündung, Zylinder 3: Brenndauer zu kurz |
| 0x2FAB | 0x2FAB Zündung, Zylinder 4: Brenndauer zu kurz |
| 0x2FAC | 0x2FAC Zündung, Zylinder 5: Brenndauer zu kurz |
| 0x2FAD | 0x2FAD Zündung, Zylinder 6: Brenndauer zu kurz |
| 0x2FDA | 0x2FDA Kurbelwellensensor, Signal: fehlt |
| 0x2FDB | 0x2FDB Kurbelwellensensor, Signal: unplausibel |
| 0x2FDD | 0x2FDD Kurbelwellensensor, Plausibilität: Drehrichtung unplausibel |
| 0x300C | 0x300C Einlassnockenwellensensor, elektrisch: Kurzschluss nach Plus |
| 0x300D | 0x300D Einlassnockenwellensensor, elektrisch: Kurzschluss nach Masse |
| 0x300E | 0x300E Auslassnockenwellensensor, elektrisch: Kurzschluss nach Plus |
| 0x300F | 0x300F Ausassnockenwellensensor, elektrisch: Kurzschluss nach Masse |
| 0x3011 | 0x3011 Einlassnockenwelle: Montage fehlerhaft |
| 0x3012 | 0x3012 Auslassnockenwelle: Montage fehlerhaft |
| 0x303E | 0x303E Klopfregelung: Systemfehler |
| 0x303F | 0x303F Klopfsensor, elektrisch: Signal-Eingang A, Kurzschluss nach Plus |
| 0x3040 | 0x3040 Klopfsensor, elektrisch: Signal-Eingang A, Kurzschluss nach Masse |
| 0x3041 | 0x3041 Klopfsensor, elektrisch: Signal-Eingang B, Kurzschluss nach Plus |
| 0x3042 | 0x3042 Klopfsensor, elektrisch: Signal-Eingang B, Kurzschluss nach Masse |
| 0x3043 | 0x3043 Klopfsensor 2, elektrisch: Signal-Eingang A, Kurzschluss nach Plus |
| 0x3044 | 0x3044 Klopfsensor 2, elektrisch: Signal-Eingang A, Kurzschluss nach Masse |
| 0x3045 | 0x3045 Klopfsensor 2, elektrisch: Signal-Eingang B, Kurzschluss nach Plus |
| 0x3046 | 0x3046 Klopfsensor 2, elektrisch: Signal-Eingang B, Kurzschluss nach Masse |
| 0x3048 | 0x3048 Klopfsensor 1, Signal: Motorgeräusch über Grenzwert |
| 0x3049 | 0x3049 Klopfsensor 1, Signal: Motorgeräusch unter Grenzwert oder Leitungsunterbrechung |
| 0x304C | 0x304C Klopfsensor 2, Signal: Motorgeräusch über Grenzwert |
| 0x304D | 0x304D Klopfsensor 2, Signal: Motorgeräusch unter Grenzwert oder Leitungsunterbrechung |
| 0x3106 | 0x3106 Katalysator: Wirkungsgrad unterhalb Grenzwert |
| 0x3139 | 0x3139 DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Plus |
| 0x313A | 0x313A DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Masse |
| 0x313B | 0x313B DMTL-Magnetventil, Ansteuerung: Leitungsunterbrechung |
| 0x3140 | 0x3140 Tankentlüftungs- und Spülluftsystem, Feinleck: Leckage größer 1, 0 mm |
| 0x3141 | 0x3141 Tankentlüftungs- und Spülluftsystem, Feinstleck: Leckage größer 0, 5 mm |
| 0x3142 | 0x3142 DMTL, Systemfehler: Pumpenstrom zu groß bei Referenzmessung |
| 0x3143 | 0x3143 DMTL, Systemfehler: Pumpenstrom zu klein bei Referenzmessung |
| 0x3144 | 0x3144 DMTL, Systemfehler: Abbruch wegen Stromschwankungen bei Referenzmessung |
| 0x3145 | 0x3145 DMTL, Systemfehler: Pumpenstrom bei Ventilprüfung erreicht Grenzwert |
| 0x3146 | 0x3146 DMTL, Heizung, Ansteuerung: Kurzschluss nach Plus |
| 0x3147 | 0x3147 DMTL, Heizung, Ansteuerung: Kurzschluss nach Masse |
| 0x3148 | 0x3148 DMTL, Heizung, Ansteuerung: Leitungsunterbrechung |
| 0x314A | 0x314A DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Plus |
| 0x314B | 0x314B DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Masse |
| 0x314C | 0x314C DMTL-Leckdiagnosepumpe, Ansteuerung: Leitungsunterbrechung |
| 0x3155 | 0x3155 Tankentlüftungsventil, Ansteuerung: Kurzschluss nach Plus |
| 0x3156 | 0x3156 Tankentlüftungsventil, Ansteuerung: Kurzschluss nach Masse |
| 0x3157 | 0x3157 Tankentlüftungsventil, Ansteuerung: Leitungsunterbrechung |
| 0x3159 | 0x3159 Tankentlüftungsventil: klemmt geschlossen |
| 0x315A | 0x315A Tankentlüftungsventil: klemmt offen |
| 0x3160 | 0x3160 Tankentlüftungssystem Absperrventil, Ansteuerung: Kurzschluss nach Plus |
| 0x3161 | 0x3161 Tankentlüftungssystem Absperrventil, Ansteuerung: Kurzschluss nach Masse |
| 0x3162 | 0x3162 Tankentlüftungssystem Absperrventil, Ansteuerung: Leitungsunterbrechung |
| 0x3163 | 0x3163 Tankentlüftungssystem Absperrventil: klemmt offen |
| 0x3164 | 0x3164 Tankentlüftungssystem, 2. Einleitestelle: Fehlfunktion |
| 0x3165 | 0x3165 Tankentlüftungssystem, Nachlauf: Fehlfunktion |
| 0x3166 | 0x3166 Tankentlüftungssystem: Fehlfunktion |
| 0x316A | 0x316A Tankdeckel: nicht korrekt geschlossen |
| 0x316B | 0x316B Tankdeckel: offen im Nachlauf |
| 0x3183 | 0x3183 Tankfüllstandssensor, rechts, Signal: Kurzschluss nach Plus |
| 0x3184 | 0x3184 Tankfüllstandssensor, rechts, Signal: Kurzschluss nach Masse |
| 0x3185 | 0x3185 Tankfüllstandssensor, rechts, Signal: CAN Wert unplausibel |
| 0x3187 | 0x3187 Tankfüllstandssensor, links, Signal: Kurzschluss nach Plus |
| 0x3188 | 0x3188 Tankfüllstandssensor, links, Signal: Kurzschluss nach Masse |
| 0x3189 | 0x3189 Tankfüllstandssensor, links, Signal: Tankfüllstandsignal unplausibel zu hoch |
| 0x318A | 0x318A Tankfüllstandssensor, links, Signal: CAN Wert unplausibel |
| 0x318B | 0x318B Tankfüllstandssensor: Signal unplausibel wegen festhängendem Tankfüllstandsgeber |
| 0x318C | 0x318C Tankfüllstandssensor: Tankfüllstand größer als Tankvolumen |
| 0x318D | 0x318D Tankfüllstandssensor: Abweichung zwischen Verbrauch und Füllstandsänderung |
| 0x318F | 0x318F Tankfüllstand, Sammelfehler: Signal und elektrisch |
| 0x31E7 | 0x31E7 Elektrolüfter, Ansteuerungleitung: Kurzschluss nach Plus |
| 0x31E8 | 0x31E8 Elektrolüfter, Ansteuerungleitung: Kurzschluss nach Masse |
| 0x31E9 | 0x31E9 Elektrolüfter, Ansteuerungleitung: Leitungsunterbrechung |
| 0x31EA | 0x31EA Elektrolüfter, Eigendiagnose: Mechanischer- oder Hardwaredefekt |
| 0x3219 | 0x3219 DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Plus |
| 0x321A | 0x321A DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Masse |
| 0x321B | 0x321B DMTL-Magnetventil, Ansteuerung: Leitungsunterbrechung |
| 0x321C | 0x321C Tankentlüftungs- und Spülluftsystem, Feinleck: Leckage größer 1,0 mm |
| 0x321D | 0x321D Tankentlüftungs- und Spülluftsystem, Feinstleck: Leckage größer 0,5 mm |
| 0x321E | 0x321E DMTL, Systemfehler: Pumpenstrom zu groß bei Referenzmessung |
| 0x321F | 0x321F DMTL, Systemfehler: Pumpenstrom zu klein bei Referenzmessung |
| 0x3220 | 0x3220 DMTL, Systemfehler: Abbruch wegen Stromschwankungen bei Referenzmessung |
| 0x3221 | 0x3221 DMTL, Systemfehler: Pumpenstrom bei Ventilprüfung erreicht Grenzwert |
| 0x3222 | 0x3222 DMTL, Heizung, Ansteuerung: Kurzschluss nach Plus |
| 0x3223 | 0x3223 DMTL, Heizung, Ansteuerung: Kurzschluss nach Masse |
| 0x3224 | 0x3224 DMTL, Heizung, Ansteuerung: Leitungsunterbrechung |
| 0x3225 | 0x3225 DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Plus |
| 0x3226 | 0x3226 DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Masse |
| 0x3227 | 0x3227 DMTL-Leckdiagnosepumpe, Ansteuerung: Leitungsunterbrechung |
| 0x3228 | 0x3228 Tankentlüftungssystem, 2. Einleitestelle, Nachlauf: Fehlfunktion |
| 0x32AB | 0x32AB FA-CAN, Botschaft (EWS Dienst DME1/DDE1, 0x5C0): Framefehler |
| 0x32C8 | 0x32C8 Schlechtwegstreckenerkennung: Radgeschwindigkeit zu hoch |
| 0x32C9 | 0x32C9 Schlechtwegstreckenerkennung: Kein Raddrehzahlsignal erhalten |
| 0x32CC | 0x32CC Fahrzeuggeschwindigkeit, Plausibilität: Kombi hat Ungültigkeitssignal gesendet |
| 0x32CD | 0x32CD Fahrzeuggeschwindigkeit, Plausibilität: DSC-Signal unplausibel gegenüber Kombi-Anzeige |
| 0x32D0 | 0x32D0 Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeit zu hoch |
| 0x32D4 | 0x32D4 Fahrzeuggeschwindigkeit: Sammelfehler |
| 0x32D8 | 0x32D8 Fahrzeuggeschwindigkeit, Plausibilität: Mindestgeschwindigkeit unter Last unplausibel |
| 0x32D9 | 0x32D9 Fahrzeuggeschwindigkeit, Plausibilität: Mindestgeschwindigkeit im Schub unplausibel |
| 0x32DA | 0x32DA Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeitssignal unplausibel |
| 0x32DC | 0x32DC Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, Signaländerung: unplausibel |
| 0x32DD | 0x32DD Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, Signaländerung: unplausibel |
| 0x32DE | 0x32DE Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, Signaländerung: unplausibel |
| 0x32DF | 0x32DF Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, Signaländerung: unplausibel |
| 0x32E1 | 0x32E1 EWS Manipulationsschutz: kein Startwert programmiert |
| 0x32E2 | 0x32E2 EWS Manipulationsschutz: Antwort unplausibel |
| 0x32E3 | 0x32E3 Schnittstelle EWS-DME: Hardwarefehler |
| 0x32E4 | 0x32E4 Schnittstelle EWS-DME: Framefehler |
| 0x32E5 | 0x32E5 Schnittstelle EWS-DME: Zeitüberschreitung |
| 0x32E6 | 0x32E6 Schnittstelle EWS-DME: Empfangsfehler CAS Schnittstelle |
| 0x32E7 | 0x32E7 DME, interner Fehler, EWS-Daten: keine verfügbare Speichermöglichkeit |
| 0x32E8 | 0x32E8 DME, interner Fehler, EWS-Daten: Fehlerfreischaltcodeablage |
| 0x32E9 | 0x32E9 DME, interner Fehler, EWS-Daten: Prüfsummenfehler |
| 0x32EA | 0x32EA DME, interner Fehler, EWS-Daten: Schreibfehler Secret Key |
| 0x32EC | 0x32EC FA-CAN, Botschaft (EWS Dienst DME1/DDE1, 0x5C0): fehlt |
| 0x3325 | 0x3325 Bremslichtschalter, Plausibilität: Signal unplausibel |
| 0x332C | 0x332C Klemme 15_3, Leitung vom CAS, elektrisch: Kurzschluss nach Masse |
| 0x332D | 0x332D Klemme 15_3, Leitung vom CAS, elektrisch: Kurzschluss nach Plus |
| 0x332E | 0x332E Klemme 87_1: keine Spannung |
| 0x332F | 0x332F Klemme 87_2: keine Spannung |
| 0x3330 | 0x3330 Klemme 87_3: keine Spannung |
| 0x335B | 0x335B Bremsunterdrucksensor, Plausibilität: Differenzdruck zu niedrig |
| 0x335C | 0x335C Bremsunterdrucksensor, elektrisch: Kurzschluss nach Plus |
| 0x335D | 0x335D Bremsunterdrucksensor, elektrisch: Kurzschluss nach Masse |
| 0x3392 | 0x3392 Motorabstellzeit, Plausibilität: Zeit zu kurz in Korrelation zu Motorkühlmittel-Abkühlung |
| 0x3393 | 0x3393 Motorabstellzeit, Plausibilität: Zeit zu lang in Korrelation zu Motorkühlmittel-Abkühlung |
| 0x3394 | 0x3394 Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi zu hoch im Motorlauf |
| 0x3395 | 0x3395 Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi zu niedrig im Motorlauf |
| 0x3396 | 0x3396 Motorabstellzeit, Signal: fehlt |
| 0x3398 | 0x3398 Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi zu hoch im Nachlauf |
| 0x3399 | 0x3399 Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi zu niedrig im Nachlauf |
| 0x33DB | 0x33DB Nullgangsensor, Adaption: nicht gelernt (MSA deaktiviert) |
| 0x33DC | 0x33DC Nullgangsensor, Plausibilität: Signal unplausibel |
| 0x33DD | 0x33DD Nullgangsensor, Signal: Tastverhältnis zu hoch |
| 0x33DE | 0x33DE Nullgangsensor, Signal: Tastverhältnis zu niedrig |
| 0x33DF | 0x33DF Nullgangsensor, elektrisch: Kurzschluss nach Plus oder Leitungsunterbrechung |
| 0x33E0 | 0x33E0 Nullgangsensor, elektrisch: Kurzschluss nach Masse |
| 0x33E1 | 0x33E1 Nullgangsensor, Plausibilität: Periodendauer außerhalb gültigem Bereich |
| 0x33FC | 0x33FC Motoröldruckregelung, Plausibilität: Druckschwankungen |
| 0x33FD | 0x33FD Motoröldruckregelung, Plausibilität, statisch: Druck zu hoch |
| 0x33FE | 0x33FE Motoröldruckregelung, Plausibilität, statisch: Druck zu niedrig |
| 0x33FF | 0x33FF Motoröldruckregelventil, Ansteuerung: Kurzschluss nach Plus |
| 0x3400 | 0x3400 Motoröldruckregelventil, Ansteuerung: Kurzschluss nach Masse |
| 0x3401 | 0x3401 Motoröldruckregelventil, Ansteuerung: Leitungsunterbrechung |
| 0x3404 | 0x3404 Motoröldruckregelung: instabil |
| 0x3405 | 0x3405 Motorölpumpe: Druck zu hoch |
| 0x3406 | 0x3406 Motorölpumpe: Druck zu niedrig |
| 0x3408 | 0x3408 Motoröldruckregelventil: klemmt in voll bestromter Stellung (minimaler Öldruck) |
| 0x3409 | 0x3409 Motoröldruckregelventil: klemmt in unbestromter Stellung (maximaler Öldruck) |
| 0x3426 | 0x3426 Motoröldrucksensor, elektrisch: Kurzschluss nach Plus |
| 0x3427 | 0x3427 Motoröldrucksensor, elektrisch: Kurzschluss nach Masse |
| 0x3429 | 0x3429 Motoröldrucksensor, Plausibilität: Druck vor Motorstart zu hoch |
| 0x342A | 0x342A Motoröldrucksensor, Plausibilität: Druck vor Motorstart zu niedrig |
| 0x342B | 0x342B Motoröldrucksensor, Signal: festliegend |
| 0x343F | 0x343F Ölzustand, Status Niveau: Fehlfunktion |
| 0x3440 | 0x3440 Ölzustandssensor, Status Temperatur: Fehlfunktion |
| 0x3441 | 0x3441 Ölzustandssensor, elektrisch: Permittivität Fehlfunktion |
| 0x3442 | 0x3442 Ölzustandssensor, Plausibilität: Niveau unplausibel |
| 0x3443 | 0x3443 Ölzustandssensor, Plausibilität: Temperatur unplausibel |
| 0x3444 | 0x3444 Ölzustandssensor, Plausibilität: Permittivität unplausibel |
| 0x3446 | 0x3446 BSD, Kommunikation (Ölzustandssensor): fehlt |
| 0x3447 | 0x3447 Motorölniveau: zu niedrig |
| 0x3449 | 0x3449 Ölzustandssensor: Fehlfunktion |
| 0x344A | 0x344A Ölzustandssensor, Plausibilität: Niveau unplausibel |
| 0x344B | 0x344B Ölzustandssensor, Plausibilität: Temperatur unplausibel |
| 0x344C | 0x344C Motoröltemperatursensor, elektrisch: Fehlfunktion |
| 0x344D | 0x344D Motoröltemperatursensor, Plausibilität: Temperatur unplausibel |
| 0x344E | 0x344E Ölzustandssensor: Signal fehlt |
| 0x344F | 0x344F Ölzustandssensor: Signal unplausibel |
| 0x348A | 0x348A Kennfeldthermostat: klemmt offen |
| 0x348E | 0x348E Kennfeldthermostat, Ansteuerung: Kurzschluss nach Plus |
| 0x348F | 0x348F Kennfeldthermostat, Ansteuerung: Kurzschluss nach Masse |
| 0x3490 | 0x3490 Kennfeldthermostat, Ansteuerung: Leitungsunterbrechung |
| 0x34A3 | 0x34A3 Kupplungsschalter, Plausibilität: Signal unplausibel |
| 0x34A5 | 0x34A5 Kupplungsschalter: Positionen zueinander unplausibel |
| 0x34A8 | 0x34A8 Kupplungstemperatur: Warnschwellenwert 1 ohne Schädigung überschritten |
| 0x34A9 | 0x34A9 Kupplungstemperatur: Warnschwellenwert 2 ohne Schädigung überschritten |
| 0x34AD | 0x34AD Kupplung, Plausibilität: Übertragbares Moment zu niedrig, Kupplung leicht geschädigt |
| 0x34AE | 0x34AE Kupplung, Plausibilität: Übertragbares Moment zu niedrig, Kupplung geschädigt |
| 0x34AF | 0x34AF Kupplung, Plausibilität: Übertragbares Moment zu niedrig, Kupplung stark geschädigt |
| 0x3520 | 0x3520 Leerlaufregelung: Drehzahl zu hoch |
| 0x3521 | 0x3521 Leerlaufregelung: Drehzahl zu niedrig |
| 0x3524 | 0x3524 Leerlaufregelung, Kaltstart: Drehzahl zu hoch |
| 0x3525 | 0x3525 Leerlaufregelung, Kaltstart: Drehzahl zu niedrig |
| 0x3528 | 0x3528 Antrieb, Sicherheitsfunktion: Leistungsreduzierung durch Sicherheitskonzept |
| 0x3529 | 0x3529 Drehzahlbegrenzung bei stehendem Fahrzeug: Leerlaufdrehzahl zu lange zu hoch |
| 0x352A | 0x352A Manipulationsschutz: Motorleistung zu hoch |
| 0x3584 | 0x3584 DME, interner Fehler, Innentemperatursensor: Wert zu hoch |
| 0x3585 | 0x3585 DME, interner Fehler, Innentemperatursensor: Wert zu niedrig |
| 0x3586 | 0x3586 DME Temperatur: Übertemperatur |
| 0x36B0 | 0x36B0 DME, interner Fehler, Ansteuerung Valvetronic: Fehlfunktion |
| 0x36B1 | 0x36B1 DME, interner Fehler, Überwachung 5V-Versorgung 2: Überspannung erkannt |
| 0x36B2 | 0x36B2 DME, interner Fehler, Überwachung 5V-Versorgung 2: Unterspannung erkannt |
| 0x36B4 | 0x36B4 DME, interner Fehler: Überwachung SPI-Kommunikation |
| 0x36B5 | 0x36B5 DME, interner Fehler: Löschen EEPROM fehlerhaft |
| 0x36B6 | 0x36B6 DME, interner Fehler: Lesen EEPROM fehlerhaft |
| 0x36B7 | 0x36B7 DME, interner Fehler: Schreiben EEPROM fehlerhaft |
| 0x36B8 | 0x36B8 DME, interner Fehler: Überwachungsmodulfehler |
| 0x36B9 | 0x36B9 DME, interner Fehler, Überwachung 5V-Versorgung: Überspannung erkannt |
| 0x36BA | 0x36BA DME, interner Fehler, Überwachung 5V-Versorgung: Unterspannung erkannt |
| 0x36BB | 0x36BB DME, interner Fehler, Watchdog-Ausgang: Fehlfunktion |
| 0x36BC | 0x36BC DME, interner Fehler, Watchdog-Ausgang: fehlerhafte Frage-/Antwort-Kommunikation |
| 0x36BD | 0x36BD DME, interner Fehler, Watchdog-Ausgang: Überspannungserkennung |
| 0x36BE | 0x36BE DME, Kodierung: fehlt oder Fahrgestellnummer falsch |
| 0x36BF | 0x36BF DME, interner Fehler, MSA-Überwachung: fehlerhafte Berechnung |
| 0x36C0 | 0x36C0 Antrieb, Sicherheitsfunktion: AD-Wandler Leerlauftestimpulsprüfung |
| 0x36C1 | 0x36C1 Antrieb, Sicherheitsfunktion: AD-Wandler Testspannungsprüfung |
| 0x36C2 | 0x36C2 DME, interner Fehler, Sicherheitsfunktion: Luftmengenabgleich |
| 0x36C3 | 0x36C3 Antrieb, Sicherheitsfunktion: Fahrpedalmodul oder Pedalwertgeber unplausibel |
| 0x36C4 | 0x36C4 Antrieb, Sicherheitsfunktion: Drehzahlgeber unplausibel |
| 0x36C5 | 0x36C5 DME, interner Fehler, Sicherheitsfunktion: Plausibilisierung der Gemischkorrekturfaktoren |
| 0x36C6 | 0x36C6 DME, interner Fehler, Sicherheitsfunktion: Einspritzmengenbegrenzung Ebene 1 |
| 0x36C7 | 0x36C7 Antrieb, Sicherheitsfunktion: Sicherheitsabschaltung Einspritzung |
| 0x36C8 | 0x36C8 DME, interner Fehler, Sicherheitsfunktion: Lambda-Sollwert |
| 0x36C9 | 0x36C9 DME, interner Fehler, Sicherheitsfunktion: Plausibilisierung relative Kraftstoffmasse |
| 0x36CA | 0x36CA DME, interner Fehler, Sicherheitsfunktion: Momentenvergleich |
| 0x36CB | 0x36CB DME, interner Fehler, Sicherheitsfunktion: Antriebstrangübersetzungsverhältnis unplausibel |
| 0x36CC | 0x36CC Antrieb, Sicherheitsfunktion: Getriebevariante unplausibel |
| 0x36CD | 0x36CD DME, interner Fehler, Sicherheitsfunktion: Zündwinkelüberwachung |
| 0x36CE | 0x36CE Antrieb, Sicherheitsfunktion: Abschaltpfad-Test negativ |
| 0x36CF | 0x36CF DME, interner Fehler, Sicherheitsfunktion: Plausiblisierung Kraftstoffmasse |
| 0x36D0 | 0x36D0 DME, interner Fehler, Überwachung MSC-Kommunikation: Fehlfunktion an Baustein R2S2/1 |
| 0x36D2 | 0x36D2 DME, interner Fehler, Überwachung MSC-Kommunikation: Fehlfunktion an Baustein R2S2/2 |
| 0x36D4 | 0x36D4 DME, interner Fehler, Ansteuerung Valvetronic: Fehlfunktion |
| 0x36E2 | 0x36E2 Überwachung 5V Sensor-Versorgung: Spannung außerhalb gültigem Bereich |
| 0x36E3 | 0x36E3 Überwachung 5V Sensor-Versorgung 2: Spannung außerhalb gültigem Bereich |
| 0x36E4 | 0x36E4 Überwachung 5V Sensor-Versorgung 3: Spannung außerhalb gültigem Bereich |
| 0x36E5 | 0x36E5 DME, interner Fehler: Software-Reset |
| 0x36E6 | 0x36E6 DME, interner Fehler: Software-Reset |
| 0x36E7 | 0x36E7 DME, interner Fehler: Software-Reset |
| 0x36FA | 0x36FA Startaggregat Ritzelstarter, Ansteuerung: Kurzschluss nach Plus |
| 0x36FB | 0x36FB Startaggregat Ritzelstarter, Ansteuerung: Kurzschluss nach Masse |
| 0x36FC | 0x36FC Startaggregat Ritzelstarter, Ansteuerung: Leitungsunterbrechung |
| 0x36FD | 0x36FD DME-Hauptrelais, Plausibilität: vorzeitig abgefallen |
| 0x36FE | 0x36FE DME-Hauptrelais, Ansteuerung: Kurzschluss nach Masse |
| 0x36FF | 0x36FF DME-Hauptrelais: nicht abgefallen |
| 0x3714 | 0x3714 Bordnetzspannung, DME-Hauptrelais, Arbeitsbereich: Spannung zu hoch |
| 0x3719 | 0x3719 Valvetronic, Versorgungsspannung: Kurzschluss nach Masse |
| 0x371A | 0x371A Valvetronic, Versorgungsspannung: Leitungsunterbrechung |
| 0x371B | 0x371B Relais Zündung und Injektoren, Ansteuerung: Kurzschluss nach Masse |
| 0x371C | 0x371C Relais Zündung und Injektoren, Ansteuerung: Kurzschluss nach Plus |
| 0x371E | 0x371E Relais Zündung und Injektoren, Ansteuerung: Leitungsunterbrechung |
| 0x375A | 0x375A CBS-Client: Ausgabe von Ersatzwert |
| 0x375B | 0x375B CBS-Client: Verfügbarkeitssprung |
| 0x375C | 0x375C DME, Manipulationsschutz: Programm oder Datenmanipulation erkannt |
| 0x375F | 0x375F DME, falscher Datensatz: FA-CAN, Botschaft (Fahrzeugtyp, 0x388): fehlt |
| 0x3760 | 0x3760 DME, falscher Datensatz: Variantenüberwachung |
| 0x3761 | 0x3761 Funktionsfreischaltung, Leistungserhöhung: nicht erfolgt |
| 0x3778 | 0x3778 Motor-Kühlsystem: Abschaltung Kühlmittelpumpe wegen Übertemperatur |
| 0x3779 | 0x3779 Motor-Kühlsystem: Abschaltung Kühlmittelpumpe wegen Überspannung |
| 0x377A | 0x377A Motor-Kühlsystem: Abschaltung Kühlmittelpumpe wegen Blockierung |
| 0x377B | 0x377B Motor-Kühlsystem, leistungsreduzierter Betrieb: Kühlmittelverlust durch Kühlmittelpumpe erkannt |
| 0x377C | 0x377C Motor-Kühlsystem, leistungsreduzierter Betrieb: Versorgungsspannung Kühlmittelpumpe zu niedrig |
| 0x377D | 0x377D Motor-Kühlsystem, leistungsreduzierter Betrieb: Kühlmittelpumpe Temperaturschwelle 1 überschritten |
| 0x377E | 0x377E Motor-Kühlsystem, leistungsreduzierter Betrieb: Kühlmittelpumpe Temperaturschwelle 2 überschritten |
| 0x378F | 0x378F BSD, Kommunikation (Motor-Kühlmittelpumpe): fehlt |
| 0x3791 | 0x3791 Motor-Kühlsystem: kein Notlaufsignal an Kühlmittelpumpe |
| 0x3792 | 0x3792 Motor-Kühlsystem: Drehzahl Kühlmittelpumpe außerhalb der Toleranz |
| 0x3796 | 0x3796 Kupplungsschalter, Signal: fehlt |
| 0x3840 | 0x3840 Generator, elektrisch: Fehlfunktion |
| 0x3841 | 0x3841 Generator, elektrisch: Fehlfunktion |
| 0x3842 | 0x3842 Generator, Plausibilität, elektrisch: berechnet |
| 0x3843 | 0x3843 Generator, Temperatur: Übertemperatur |
| 0x3844 | 0x3844 Generator, Plausibilität, elektrisch: berechnet |
| 0x3845 | 0x3845 Generator, mechanisch: Fehlfunktion |
| 0x3846 | 0x3846 Generator: Typ falsch |
| 0x3848 | 0x3848 Generator, Temperatur: Übertemperatur |
| 0x384C | 0x384C Generator, Plausibilität, Temperatur: Übertemperatur berechnet |
| 0x3850 | 0x3850 Generator, mechanisch: Fehlfunktion |
| 0x3854 | 0x3854 Generator, Regler: Typ falsch |
| 0x3858 | 0x3858 Generator: Typ falsch |
| 0x385B | 0x385B Generator/Startergenerator: Kodierung oder Programmstand falsch |
| 0x385C | 0x385C Generator, Kommunikation: keine Kommunikation |
| 0x385D | 0x385D Generator, Kommunikation: Bus-Fehler |
| 0x385F | 0x385F Generator/Startergenerator: Kodierung fehlt |
| 0x3865 | 0x3865 BSD-Bus: Kommunikationsfehler |
| 0x3866 | 0x3866 BSD, Botschaft (Intelligenter Batteriesensor): fehlt |
| 0x3871 | 0x3871 Startergenerator: Typ falsch |
| 0x3872 | 0x3872 Powermanagement, Batteriezustandserkennung: Batteriedefekt |
| 0x3873 | 0x3873 Powermanagement, Batteriezustandserkennung: Tiefentladung |
| 0x3875 | 0x3875 Powermanagement, Überspannung: Überspannung erkannt |
| 0x3876 | 0x3876 Powermanagement, Unterspannung: Unterspannung erkannt |
| 0x3877 | 0x3877 Powermanagement: zentrale Überspannung |
| 0x3878 | 0x3878 Powermanagement: zentrale Unterspannung |
| 0x3879 | 0x3879 Powermanagement: Batterieloser Betrieb |
| 0x387C | 0x387C Powermanagement: Batterie Tiefentladung |
| 0x387D | 0x387D Powermanagement: Transportüberwachung Ladezustand Batterie tiefentladen |
| 0x387F | 0x387F Powermanagement: Ruhestromverletzung |
| 0x3886 | 0x3886 Bordnetzspannung, Arbeitsbereich: Spannung zu hoch |
| 0x3887 | 0x3887 Bordnetzspannung, Arbeitsbereich: Spannung zu niedrig |
| 0x3888 | 0x3888 Bordnetzspannung: Analog-Digital-Wandler defekt |
| 0x38A4 | 0x38A4 Erweiterte Kommunikation, Intelligenter Batteriesensor: Fehlfunktion |
| 0x38A7 | 0x38A7 Intelligenter Batteriesensor, Kompatibilität: Version nicht plausibel |
| 0x38A8 | 0x38A8 Intelligenter Batteriesensor, Eigendiagnose: Systemfehler |
| 0x38A9 | 0x38A9 Intelligenter Batteriesensor, Plausibilität: Temperatur unplausibel |
| 0x38AA | 0x38AA Intelligenter Batteriesensor, Plausibilität: Spannung unplausibel |
| 0x38AB | 0x38AB Intelligenter Batteriesensor, Plausibilität: Strom unplausibel |
| 0x38AC | 0x38AC Intelligenter Batteriesensor, Wake-up-Leitung, elektrisch: Kurzschluss nach Plus oder Masse |
| 0x38B2 | 0x38B2 Intelligenter Batteriesensor, Wake-up-Leitung, elektrisch: Leitungsunterbrechung |
| 0x38B4 | 0x38B4 BSD, Kommunikation (Intelligenter Batteriesensor): fehlt |
| 0x38D6 | 0x38D6 Aktives Motorlager, elektrisch: Kurzschluss nach Plus |
| 0x38D7 | 0x38D7 Aktives Motorlager, elektrisch: Kurzschluss nach Masse |
| 0x38D8 | 0x38D8 Aktives Motorlager, elektrisch: Leitungsunterbrechung |
| 0x38EF | 0x38EF Freigabeleitung, MSA, Ansteuerung: Kurzschluss nach Plus |
| 0x38F0 | 0x38F0 Freigabeleitung, MSA, Ansteuerung: Kurzschluss nach Masse |
| 0x38F1 | 0x38F1 Freigabeleitung, MSA, Ansteuerung: Leitungsunterbrechung |
| 0x38F2 | 0x38F2 MSA, Überwachung: Motorstart zu langsam |
| 0x38F3 | 0x38F3 MSA, Überwachung: Aufbau Motordrehzahl zu langsam |
| 0x3908 | 0x3908 Batterieladeeinheit: Interner Fehler |
| 0x3909 | 0x3909 Batterieladeeinheit, Leitungsüberwachung: Fehlfunktion |
| 0x390A | 0x390A Batterieladeeinheit: Zusatzbatterie defekt |
| 0x390B | 0x390B Batterieladeeinheit: Fehler im Trennrelais oder Kabelbaum oder Zusatzbatterie tiefentladen |
| 0x390C | 0x390C Startspannungswandler, Ansteuerung: Kurzschluss nach Plus |
| 0x390D | 0x390D Startspannungswandler, Ansteuerung: Kurzschluss nach Masse |
| 0x390E | 0x390E Startspannungswandler, Ansteuerung: Leitungsunterbrechung |
| 0x393A | 0x393A Motordrehmomentbegrenzung: infolge Notlaufanforderung vom EME-Notlaufmanager |
| 0x393B | 0x393B Motordrehzahlbegrenzung, Stufe 1: infolge Notlaufanforderung vom EME-Notlaufmanager |
| 0x393C | 0x393C Motordrehzahlbegrenzung, Stufe 2: infolge Notlaufanforderung vom EME-Notlaufmanager |
| 0x393D | 0x393D Motordrehzahlbegrenzung, Stufe 3: infolge Notlaufanforderung vom EME-Notlaufmanager |
| 0x3B94 | 0x3B94 LIN, Botschaft (Batterieladeeinheit, Status Energieerzeugung Bordnetz 2, 0x5): fehlt |
| 0x3B97 | 0x3B97 LIN Bus, Kommunikation: Signal fehlt |
| 0x3B99 | 0x3B99 Motor-Kühlsystem: Kommunikation mit Kühlmittelpumpe fehlt |
| 0x3B9A | 0x3B9A Motor-Kühlsystem: Kommunikation mit Kühlmittelpumpe fehlerhaft |
| 0x3B9B | 0x3B9B LIN, Botschaft (Status Generator LIN, 0x15). fehlt |
| 0x3B9C | 0x3B9C LIN, Botschaft (Status_Wasserpumpe_LIN, 0x25): fehlt |
| 0x3B9D | 0x3B9D LIN Knoten Generator, Kommunikation: Fehlfunktion |
| 0x3BC4 | 0x3BC4 PT-CAN, Botschaft (Status ARS-Modul, 0x1AC): Aliveprüfung |
| 0x3BC5 | 0x3BC5 PT-CAN, Botschaft (Status ARS-Modul, 0x1AC): fehlt |
| 0x3BC6 | 0x3BC6 PT-CAN, Botschaft (Status ARS-Modul, 0x1AC): Prüfsumme falsch |
| 0x3BC7 | 0x3BC7 PT-CAN, Botschaft (Klemmenstatus, 0x130): fehlt |
| 0x3BC8 | 0x3BC8 PT-CAN, Botschaft (Klemmenstatus, 0x130): Prüfsumme falsch/Aliveprüfung |
| 0x3BCC | 0x3BCC PT-CAN, Botschaft (Wärmestrom/Lastmoment Klima, 0x1B5): fehlt |
| 0x3BCD | 0x3BCD PT-CAN, Botschaft (Status Kombi, 0x1B4): Aliveprüfung |
| 0x3BCE | 0x3BCE PT-CAN, Botschaft (Status Kombi, 0x1B4): fehlt |
| 0x3BCF | 0x3BCF PT-CAN, Botschaft (Status Kombi, 0x1B4): MIL-Ansteuerung unplausibel |
| 0x3BD0 | 0x3BD0 PT-CAN, Botschaft (Anforderung Drehmoment DSC, 0x0B6): Prüfsumme falsch/Aliveprüfung |
| 0x3BD1 | 0x3BD1 PT-CAN, Botschaft (Anforderung Drehmoment DSC, 0x0B6): fehlt |
| 0x3BD2 | 0x3BD2 PT-CAN, Botschaft (Radgeschwindigkeit, 0xCE): fehlt |
| 0x3BD3 | 0x3BD3 PT-CAN, Botschaft (Getriebedaten 4, 0x10A): Prüfsumme falsch/Aliveprüfung |
| 0x3BD4 | 0x3BD4 PT-CAN, Botschaft (Getriebedaten 4, 0x10A): fehlt |
| 0x3BD5 | 0x3BD5 PT-CAN, Botschaft (Status DSC, 0x19E): fehlt |
| 0x3BD6 | 0x3BD6 PT-CAN, Botschaft (Geschwindigkeit, 0x1A0): Prüfsumme falsch/Aliveprüfung |
| 0x3BD7 | 0x3BD7 PT-CAN, Botschaft (Geschwindigkeit, 0x1A0): fehlt |
| 0x3BD8 | 0x3BD8 PT-CAN, Botschaft (Getriebedaten 2, 0x1A2): fehlt |
| 0x3BD9 | 0x3BD9 PT-CAN, Botschaft (Status DKG, 0x37D): fehlt |
| 0x3BDA | 0x3BDA PT-CAN, Botschaft (Getriebedaten 3, 0x3B1): Prüfsumme falsch/Aliveprüfung |
| 0x3BDB | 0x3BDB PT-CAN, Botschaft (Getriebedaten 3, 0x3B1): fehlt |
| 0x3BDC | 0x3BDC PT-CAN, Botschaft (Anforderung Drehmoment EGS, 0xB5): Prüfsumme falsch/Aliveprüfung |
| 0x3BDD | 0x3BDD PT-CAN, Botschaft (Anforderung Drehmoment EGS, 0xB5): fehlt |
| 0x3BDE | 0x3BDE PT-CAN, Botschaft (Anforderung Drehmoment DKG, 0xB8): Prüfsumme falsch/Aliveprüfung |
| 0x3BDF | 0x3BDF PT-CAN, Botschaft (Anforderung Drehmoment DKG, 0xB8): fehlt |
| 0x3BE0 | 0x3BE0 PT-CAN, Botschaft (Getriebedaten, 0xBA): Prüfsumme falsch/Aliveprüfung |
| 0x3BE1 | 0x3BE1 PT-CAN, Botschaft (Getriebedaten, 0xBA): fehlt |
| 0x3BE2 | 0x3BE2 PT-CAN, Botschaft (DKG Drehzahlregelung, 0xB8): Überwachungseingriff |
| 0x3BE7 | 0x3BE7 PT-CAN, Botschaft (Bedienung Taster MSA, 0x195): fehlt |
| 0x3BEC | 0x3BEC PT-CAN, Botschaft (Bedienung Tempomat, 0x194): Prüfsumme falsch/Aliveprüfung |
| 0x3BED | 0x3BED PT-CAN, Botschaft (Bedienung Tempomat, 0x194): fehlt |
| 0x3BF0 | 0x3BF0 PT-CAN, Botschaft (Status Fahrererkennung, 0x2F1): Prüfsumme falsch |
| 0x3BF1 | 0x3BF1 PT-CAN, Botschaft (Status Fahrererkennung, 0x2F1): fehlt |
| 0x3BF4 | 0x3BF4 PT-CAN, Botschaft (ZV und Klappenzustand, 0x2FC): fehlt |
| 0xCD83 | 0xCD83 Energiesparmodus: aktiv |
| 0xCD85 | 0xCD85 PT-CAN, Botschaft (Klemmenstatus, 0x130): Prüfsumme falsch |
| 0xCD86 | 0xCD86 PT-CAN, Botschaft (Klemmenstatus, 0x130): fehlt |
| 0xCD87 | 0xCD87 PT-CAN Kommunikationsfehler: CAN-Bus Off oder CAN-Bus defekt |
| 0xCD89 | 0xCD89 PT-CAN, Botschaft (Status Crashabschaltung elektrische Kraftstoffpumpe, 0x135): fehlt |
| 0xCD8B | 0xCD8B PT-CAN, Botschaft (Stellanforderung EMF, 0x1A7): Prüfsumme falsch |
| 0xCD8C | 0xCD8C PT-CAN, Botschaft (Stellanforderung EMF, 0x1A7): fehlt |
| 0xCD8F | 0xCD8F PT-CAN, Botschaft (Anzeige Getriebedaten, 0x1D2): fehlt |
| 0xCD91 | 0xCD91 PT-CAN, Botschaft (Status EMF, 0x201): Prüfsumme falsch |
| 0xCD92 | 0xCD92 PT-CAN, Botschaft (Status EMF, 0x201): fehlt |
| 0xCD95 | 0xCD95 PT-CAN, Botschaft (Lampenzustand, 0x21A): fehlt |
| 0xCD98 | 0xCD98 PT-CAN, Botschaft (Status Anhänger, 0x2E4): fehlt |
| 0xCD9B | 0xCD9B PT-CAN, Botschaft (Uhrzeit/Datum, 0x2F8): fehlt |
| 0xCD9D | 0xCD9D PT-CAN, Botschaft (Fahrzeugmodus, 0x315): Prüfsumme falsch |
| 0xCD9E | 0xCD9E PT-CAN, Botschaft (Fahrzeugmodus, 0x315): fehlt |
| 0xCDA1 | 0xCDA1 PT-CAN, Botschaft (Powermanagement Ladespannung, 0x334): fehlt |
| 0xCDA2 | 0xCDA2 PT-CAN, Botschaft (Status Verdeck Cabrio, 0x27E): fehlt |
| 0xCDA4 | 0xCDA4 PT-CAN, Botschaft (Status Gang Rückwärts, 0x3B0): fehlt |
| 0xCDA5 | 0xCDA5 PT-CAN, Botschaft (Drehmomentanforderung Lenkung, 0xB1): AFS/STE disabled oder Lenkmoment ungültig |
| 0xCDA6 | 0xCDA6 PT-CAN, Botschaft (Drehmomentanforderung Lenkung, 0xB1): Prüfsumme falsch |
| 0xCDA7 | 0xCDA7 PT-CAN, Botschaft (Drehmomentanforderung Lenkung, 0xB1): fehlt |
| 0xCDA8 | 0xCDA8 PT-CAN, Botschaft (Drehmomentanforderung AFS, 0xB9): AFS/STE disabled oder Lenkmoment ungültig |
| 0xCDA9 | 0xCDA9 PT-CAN, Botschaft (Drehmomentanforderung AFS, 0xB9): Prüfsumme falsch |
| 0xCDAA | 0xCDAA PT-CAN, Botschaft (Drehmomentanforderung AFS, 0xB9): fehlt |
| 0xCDAB | 0xCDAB PT-CAN, Botschaft (Anforderung Radmoment Antriebstrang, 0xBF): Aliveprüfung |
| 0xCDAC | 0xCDAC PT-CAN, Botschaft (Anforderung Radmoment Antriebstrang, 0xBF): Prüfsumme falsch |
| 0xCDAD | 0xCDAD PT-CAN, Botschaft (Anforderung Radmoment Antriebstrang, 0xBF): fehlt |
| 0xCDB0 | 0xCDB0 PT-CAN, Botschaft (Lenkradwinkel, 0xC4): fehlt |
| 0xCDB1 | 0xCDB1 PT-CAN Kommunikationsfehler: DPRAM CAN Baustein defekt |
| 0xCDB2 | 0xCDB2 PT-CAN, Botschaft (Sollmomentanforderung, 0xBB): fehlt |
| 0xCDB3 | 0xCDB3 PT-CAN, Botschaft (Drehmomentanforderung AFS, 0xB9): Verlustmoment zu gross |
| 0xCDB4 | 0xCDB4 PT-CAN, Botschaft (OBD Sensor Diagnosestatus, 0x5E0): fehlt, Sender Kombi |
| 0xCDB6 | 0xCDB6 PT-CAN, Botschaft (Drehmomentanforderung Lenkung, 0xB1): Verlustmoment zu gross |
| 0xCDB7 | 0xCDB7 PT-CAN, Botschaft (Status Elektrische Kraftstoffpumpe, 0x335): fehlt |
| 0xCDB8 | 0xCDB8 PT-CAN, Botschaft (Status Klemmenanforderung, 0x365): fehlt |
| 0xCDB9 | 0xCDB9 PT-CAN, Botschaft (Status Türsensoren abgesichert BN2000, 0x1E1): Prüfsumme falsch |
| 0xCDBA | 0xCDBA PT-CAN, Botschaft (Status Türsensoren abgesichert BN2000, 0x1E1): fehlt |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 750 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x2710 | 0x583F | 0x584E | 0x584C | 0x5858 |
| 0x2711 | 0x583F | 0x584E | 0x584C | 0x5858 |
| 0x2714 | 0x583F | 0x584E | 0x584C | 0x5858 |
| 0x2774 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2775 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2778 | 0x580C | 0x5818 | 0x5812 | 0x58AE |
| 0x2779 | 0x580C | 0x5818 | 0x5812 | 0x58AE |
| 0x277A | 0x580C | 0x5818 | 0x5812 | 0x58AE |
| 0x277B | 0x580C | 0x5818 | 0x5812 | 0x58AE |
| 0x277C | 0x580C | 0x5818 | 0x5812 | 0x58AE |
| 0x27D9 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x27DA | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x27DB | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x27DC | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x27E4 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x27E8 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x280E | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x280F | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x281A | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x281B | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x2820 | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x283C | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x283D | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x2841 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2842 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2848 | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x284C | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x284D | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x284E | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x284F | 0x58DD | 0x580B | 0x5821 | 0x5801 |
| 0x28A0 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x28A1 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x28A4 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28A5 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28A6 | 0x5813 | 0x584E | 0x584C | 0x5858 |
| 0x28A8 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28A9 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28AA | 0x5813 | 0x584E | 0x584C | 0x5858 |
| 0x28AC | 0x583F | 0x584E | 0x584C | 0x5858 |
| 0x28B0 | 0x5813 | 0x584E | 0x584C | 0x5858 |
| 0x28B4 | 0x583F | 0x584E | 0x584C | 0x5858 |
| 0x28B8 | 0x5815 | 0x584E | 0x584C | 0x5821 |
| 0x28B9 | 0x5815 | 0x584E | 0x584C | 0x5821 |
| 0x28BA | 0x5815 | 0x584E | 0x584C | 0x5821 |
| 0x28BB | 0x5815 | 0x584E | 0x584C | 0x5821 |
| 0x28BC | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28BD | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28C0 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28C1 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28C4 | 0x58B0 | 0x584E | 0x584C | 0x5858 |
| 0x28CC | 0x58B0 | 0x584E | 0x584C | 0x5858 |
| 0x28CD | 0x58B0 | 0x584E | 0x584C | 0x5858 |
| 0x28D0 | 0x58B0 | 0x584E | 0x584C | 0x5858 |
| 0x28D4 | 0x58B0 | 0x584E | 0x584C | 0x5858 |
| 0x28D8 | 0x586A | 0x584E | 0x584C | 0x5858 |
| 0x28D9 | 0x580C | 0x5812 | 0x5814 | 0x580B |
| 0x2904 | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x2906 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2908 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x290A | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x2936 | 0x580C | 0x5850 | 0x580F | 0x5817 |
| 0x2937 | 0x580C | 0x5850 | 0x580F | 0x5817 |
| 0x293A | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x293B | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x293E | 0x5817 | 0x5850 | 0x58EA | 0x580F |
| 0x2942 | 0x5817 | 0x5850 | 0x5836 | 0x5815 |
| 0x2943 | 0x5817 | 0x5850 | 0x5836 | 0x5815 |
| 0x2946 | 0x5817 | 0x5850 | 0x58EA | 0x580F |
| 0x2947 | 0x5817 | 0x5850 | 0x58EA | 0x580F |
| 0x2948 | 0x5817 | 0x5850 | 0x58EA | 0x580F |
| 0x299A | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x299B | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x299C | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x299E | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x29A2 | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x29A3 | 0x580F | 0x5818 | 0x5805 | 0x5817 |
| 0x29CC | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x29CD | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x29D0 | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x29D1 | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x29D2 | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x29D8 | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x29D9 | 0x580F | 0x5805 | 0x5817 | 0x5851 |
| 0x29DC | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x29DD | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x29E0 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x29E1 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x29E2 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x29E4 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x29E5 | 0x5805 | 0x58D7 | 0x5817 | 0x5818 |
| 0x29E6 | 0x5882 | 0x5817 | 0x583A | 0x58A7 |
| 0x29E7 | 0x580C | 0x5814 | 0x5817 | 0x580F |
| 0x29E8 | 0x580C | 0x5814 | 0x5817 | 0x580F |
| 0x29FE | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x29FF | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A00 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A01 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A02 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A03 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A04 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A05 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A06 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A07 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A08 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A09 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0A | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0B | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0C | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0D | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0E | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A0F | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A10 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A11 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A12 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A13 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A14 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A15 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A30 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A31 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A32 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A33 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A34 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A35 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A40 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A41 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A42 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A43 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A44 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A45 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A4C | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A4D | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A4E | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A4F | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A50 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A51 | 0x580C | 0x58EF | 0x5805 | 0x5815 |
| 0x2A5F | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A60 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A61 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A70 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A71 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A72 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A73 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A74 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2A75 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2BC0 | 0x580C | 0x5813 | 0x5807 | 0x5806 |
| 0x2BC1 | 0x580C | 0x5813 | 0x5807 | 0x5806 |
| 0x2BC2 | 0x580C | 0x5813 | 0x5807 | 0x5806 |
| 0x2BC5 | 0x580C | 0x5855 | 0x5807 | 0x5804 |
| 0x2BC3 | 0x580C | 0x5813 | 0x5807 | 0x5806 |
| 0x2BCA | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2BCB | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2BD9 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BDA | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BDB | 0x580C | 0x5813 | 0x58EF | 0x5855 |
| 0x2BDC | 0x580C | 0x5813 | 0x58EF | 0x5855 |
| 0x2BDD | 0x580C | 0x5813 | 0x58EF | 0x5855 |
| 0x2BDE | 0x58EF | 0x58F3 | 0x5882 | 0x5815 |
| 0x2BDF | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE0 | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE1 | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE2 | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE3 | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE4 | 0x580C | 0x58F3 | 0x583B | 0x58BA |
| 0x2BE5 | 0x580C | 0x58EF | 0x5837 | 0x5805 |
| 0x2BE6 | 0x580C | 0x58EF | 0x5837 | 0x5805 |
| 0x2BE9 | 0x580C | 0x58EF | 0x583B | 0x5805 |
| 0x2BEA | 0x580C | 0x5855 | 0x5807 | 0x5804 |
| 0x2BEB | 0x580C | 0x5855 | 0x5807 | 0x5804 |
| 0x2BEC | 0x58F0 | 0x58F2 | 0x5805 | 0x5815 |
| 0x2BED | 0x580C | 0x58EF | 0x5837 | 0x5805 |
| 0x2BEE | 0x580C | 0x58EF | 0x5837 | 0x5805 |
| 0x2BEF | 0x58EF | 0x580C | 0x5882 | 0x5823 |
| 0x2BF0 | 0x58EF | 0x580C | 0x5817 | 0x5823 |
| 0x2BF2 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF3 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF4 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF5 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF6 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF7 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2BF8 | 0x580C | 0x58F4 | 0x58F0 | 0x583B |
| 0x2C00 | 0x580C | 0x58EF | 0x5837 | 0x5855 |
| 0x2C01 | 0x580C | 0x58EF | 0x5837 | 0x5855 |
| 0x2C3D | 0x58F2 | 0x580D | 0x580C | 0x586A |
| 0x2C3E | 0x58F2 | 0x580D | 0x580C | 0x586A |
| 0x2C3F | 0x58F2 | 0x580D | 0x580C | 0x586A |
| 0x2C42 | 0x580C | 0x5813 | 0x5807 | 0x5806 |
| 0x2C56 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2C57 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2C58 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2C6F | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C70 | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C71 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2C72 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2C7F | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C83 | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C84 | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C85 | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C86 | 0x580C | 0x58DD | 0x58DE | 0x5801 |
| 0x2C88 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2C89 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2C8A | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2C90 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2C91 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2CA1 | 0x58DD | 0x580C | 0x5821 | 0x586A |
| 0x2CA2 | 0x58DD | 0x580C | 0x5821 | 0x586A |
| 0x2CA3 | 0x58DD | 0x580C | 0x5821 | 0x586A |
| 0x2CB3 | 0x580C | 0x5801 | 0x5817 | 0x5813 |
| 0x2CED | 0x5806 | 0x5815 | 0x5849 | 0x585C |
| 0x2CEE | 0x5827 | 0x588C | 0x5860 | 0x5863 |
| 0x2CF4 | 0x580C | 0x5855 | 0x5807 | 0x5804 |
| 0x2CF8 | 0x588C | 0x5800 | 0x5845 | 0x5849 |
| 0x2CFA | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2CFE | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2CFF | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D00 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D03 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D04 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D05 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D06 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D0B | 0x588C | 0x5800 | 0x5845 | 0x5815 |
| 0x2D0C | 0x588C | 0x5800 | 0x5845 | 0x5815 |
| 0x2D0D | 0x588C | 0x5800 | 0x5845 | 0x5815 |
| 0x2D0F | 0x5800 | 0x5815 | 0x5849 | 0x585C |
| 0x2D10 | 0x5800 | 0x5815 | 0x5849 | 0x585C |
| 0x2D11 | 0x5800 | 0x5815 | 0x5849 | 0x585C |
| 0x2D13 | 0x5849 | 0x5818 | 0x588B | 0x582F |
| 0x2D15 | 0x5806 | 0x5815 | 0x5849 | 0x585C |
| 0x2D17 | 0x5827 | 0x588C | 0x5860 | 0x5863 |
| 0x2D18 | 0x5827 | 0x588C | 0x5860 | 0x5863 |
| 0x2D19 | 0x5827 | 0x588C | 0x5860 | 0x5863 |
| 0x2D1B | 0x5849 | 0x5818 | 0x588B | 0x582F |
| 0x2D1C | 0x5849 | 0x5818 | 0x588B | 0x582F |
| 0x2D1E | 0x5849 | 0x5818 | 0x588B | 0x582F |
| 0x2D1F | 0x5806 | 0x5815 | 0x5849 | 0x585C |
| 0x2D20 | 0x5806 | 0x5815 | 0x5849 | 0x585C |
| 0x2D22 | 0x5806 | 0x5815 | 0x5849 | 0x585C |
| 0x2D23 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D24 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D25 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D27 | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D2B | 0x5827 | 0x588C | 0x5860 | 0x5863 |
| 0x2D2F | 0x588C | 0x5815 | 0x5845 | 0x5860 |
| 0x2D33 | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2D34 | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2D35 | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2D36 | 0x5878 | 0x5817 | 0x588B | 0x5801 |
| 0x2D41 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2D42 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2D43 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2D44 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2D45 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2D51 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D52 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D53 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D54 | 0x580C | 0x5813 | 0x581C | 0x581D |
| 0x2D55 | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2D5A | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2D5B | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2D60 | 0x580C | 0x5813 | 0x581C | 0x581D |
| 0x2D61 | 0x580C | 0x5813 | 0x581C | 0x581D |
| 0x2D9B | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D9C | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D9D | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2D9F | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2DA0 | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2DA1 | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2DA2 | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2DAD | 0x580C | 0x5813 | 0x581C | 0x581D |
| 0x2DAE | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2DAF | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2DB0 | 0x580C | 0x5813 | 0x581C | 0x581D |
| 0x2DB1 | 0x580C | 0x5813 | 0x581A | 0x581B |
| 0x2DB4 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DB5 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DB6 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DBA | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DBB | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DBC | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2DBD | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2DBF | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DC0 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DC3 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DC4 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCA | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCB | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCC | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCD | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCE | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DCF | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2DD0 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DD6 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DD7 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DD8 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DE1 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DE2 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DE3 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DE4 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2DE5 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2DE6 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2DE7 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2DE8 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2DE9 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2DEA | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2E0A | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2E0B | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2E0C | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2E0D | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2E0E | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x2E0F | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2E10 | 0x580C | 0x58E6 | 0x5822 | 0x58A2 |
| 0x2E11 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x2E12 | 0x580C | 0x58E6 | 0x5822 | 0x58A2 |
| 0x2E13 | 0x589E | 0x58E5 | 0x58BB | 0x58A2 |
| 0x2E4A | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2E4B | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2E4C | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2E7C | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E7D | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E7E | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E80 | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E81 | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E82 | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2E84 | 0x5817 | 0x580D | 0x58D3 | 0x58D2 |
| 0x2EE0 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE1 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE2 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE4 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE5 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE6 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE7 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE8 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EE9 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EEA | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EEB | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EEC | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EED | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EEF | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF0 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF1 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF2 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF3 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF4 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF5 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EF6 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EFE | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2EFF | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F00 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F01 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F02 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F03 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F04 | 0x580C | 0x5805 | 0x583B | 0x5838 |
| 0x2F44 | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2F45 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x2F76 | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F77 | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F78 | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F79 | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F7A | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F7B | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F7C | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x2F83 | 0x580C | 0x5813 | 0x580E | 0x58CA |
| 0x2F84 | 0x580C | 0x5813 | 0x580E | 0x58CA |
| 0x2F8A | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2F8B | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x2FA8 | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FA9 | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FAA | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FAB | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FAC | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FAD | 0x580C | 0x5813 | 0x5805 | 0x5815 |
| 0x2FDA | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2FDB | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x2FDD | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x300C | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x300D | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x300E | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x300F | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x3011 | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x3012 | 0x580C | 0x5805 | 0x5817 | 0x5815 |
| 0x303E | 0x580C | 0x5813 | 0x5805 | 0x580F |
| 0x303F | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x3040 | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x3041 | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x3042 | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x3043 | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x3044 | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x3045 | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x3046 | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x3048 | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x3049 | 0x580C | 0x5883 | 0x5894 | 0x5885 |
| 0x304C | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x304D | 0x580C | 0x5888 | 0x5895 | 0x5886 |
| 0x3106 | 0x580C | 0x5805 | 0x58AD | 0x5818 |
| 0x3139 | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x313A | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x313B | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x3140 | 0x580C | 0x583B | 0x588E | 0x5859 |
| 0x3141 | 0x580C | 0x583B | 0x588E | 0x585B |
| 0x3142 | 0x580C | 0x583B | 0x5859 | 0x5815 |
| 0x3143 | 0x580C | 0x583B | 0x5859 | 0x5815 |
| 0x3144 | 0x580C | 0x583B | 0x5859 | 0x5815 |
| 0x3145 | 0x580C | 0x583B | 0x588E | 0x5859 |
| 0x3146 | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x3147 | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x3148 | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x314A | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x314B | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x314C | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x3155 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3156 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3157 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3159 | 0x580C | 0x583B | 0x58FA | 0x586A |
| 0x315A | 0x580C | 0x583B | 0x58FA | 0x586A |
| 0x3160 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3161 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3162 | 0x5821 | 0x583B | 0x580D | 0x586A |
| 0x3163 | 0x580C | 0x583B | 0x58FA | 0x586A |
| 0x3164 | 0x580C | 0x583B | 0x58FA | 0x586A |
| 0x3165 | 0x580C | 0x583B | 0x5859 | 0x5815 |
| 0x3166 | 0x580C | 0x583B | 0x58FA | 0x586A |
| 0x316A | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x316B | 0x580C | 0x583B | 0x5874 | 0x5815 |
| 0x3183 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x3184 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x3185 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x3187 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x3188 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x3189 | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x318A | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x318B | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x318C | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x318D | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x318F | 0x580C | 0x583B | 0x580D | 0x586A |
| 0x31E7 | 0x5805 | 0x587F | 0x580D | 0x5815 |
| 0x31E8 | 0x5805 | 0x587F | 0x580D | 0x5815 |
| 0x31E9 | 0x5805 | 0x587F | 0x580D | 0x5815 |
| 0x31EA | 0x5805 | 0x587F | 0x580D | 0x5815 |
| 0x3219 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x321A | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x321B | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x321C | 0x583B | 0x5859 | 0x585A | 0x588D |
| 0x321D | 0x583B | 0x5859 | 0x585A | 0x588D |
| 0x321E | 0x580C | 0x583B | 0x5859 | 0x585A |
| 0x321F | 0x580C | 0x583B | 0x5859 | 0x585A |
| 0x3220 | 0x580C | 0x583B | 0x5859 | 0x585A |
| 0x3221 | 0x580C | 0x583B | 0x5859 | 0x585A |
| 0x3222 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3223 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3224 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3225 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3226 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3227 | 0x5815 | 0x5874 | 0x5820 | 0x5823 |
| 0x3228 | 0x580C | 0x583B | 0x5859 | 0x585A |
| 0x32AB | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32C8 | 0x580C | 0x586A | 0x580D | 0x5881 |
| 0x32C9 | 0x580C | 0x586A | 0x580D | 0x5881 |
| 0x32CC | 0x580C | 0x5813 | 0x580D | 0x5814 |
| 0x32CD | 0x580C | 0x5813 | 0x580D | 0x5814 |
| 0x32D0 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32D4 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32D8 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32D9 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32DA | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32DC | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32DD | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32DE | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32DF | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x32E1 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E2 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E3 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E4 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E5 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E6 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E7 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E8 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32E9 | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32EA | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x32EC | 0x580C | 0x5821 | 0x5805 | 0x5815 |
| 0x3325 | 0x58B7 | 0x5821 | 0x580D | 0x5815 |
| 0x332C | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x332D | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x332E | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x332F | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x3330 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x335B | 0x58B7 | 0x5821 | 0x580D | 0x5815 |
| 0x335C | 0x58B7 | 0x5821 | 0x580D | 0x5815 |
| 0x335D | 0x58B7 | 0x5821 | 0x580D | 0x5815 |
| 0x3392 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3393 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3394 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3395 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3396 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3398 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x3399 | 0x580C | 0x5817 | 0x5882 | 0x5823 |
| 0x33DB | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x33FC | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x33FD | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x33FE | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x33FF | 0x580C | 0x586F | 0x5866 | 0x586A |
| 0x3400 | 0x580C | 0x586F | 0x5866 | 0x586A |
| 0x3401 | 0x580C | 0x586F | 0x5866 | 0x586A |
| 0x3404 | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x3405 | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x3406 | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x3408 | 0x580C | 0x5822 | 0x586F | 0x586A |
| 0x3409 | 0x580C | 0x5822 | 0x586F | 0x586A |
| 0x3426 | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x3427 | 0x580C | 0x5822 | 0x586F | 0x5862 |
| 0x3429 | 0x580C | 0x5822 | 0x586F | 0x5801 |
| 0x342A | 0x580C | 0x5822 | 0x586F | 0x5801 |
| 0x342B | 0x580C | 0x5822 | 0x586F | 0x5801 |
| 0x343F | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3440 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3441 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3442 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3443 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3444 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3446 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3447 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x3449 | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344A | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344B | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344C | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344D | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344E | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x344F | 0x580C | 0x5822 | 0x588B | 0x5865 |
| 0x348A | 0x580C | 0x5805 | 0x5882 | 0x5817 |
| 0x348E | 0x580C | 0x5805 | 0x5882 | 0x5817 |
| 0x348F | 0x580C | 0x5805 | 0x5882 | 0x5817 |
| 0x3490 | 0x580C | 0x5805 | 0x5882 | 0x5817 |
| 0x34A5 | 0x580C | 0x586A | 0x580D | 0x5881 |
| 0x34A8 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x34A9 | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x34AD | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x34AE | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x34AF | 0x580C | 0x5891 | 0x5881 | 0x588B |
| 0x3520 | 0x580C | 0x5813 | 0x580D | 0x5881 |
| 0x3521 | 0x580C | 0x5813 | 0x580D | 0x5881 |
| 0x3524 | 0x580C | 0x5813 | 0x580D | 0x5881 |
| 0x3525 | 0x580C | 0x5813 | 0x580D | 0x5881 |
| 0x3528 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x3529 | 0x580C | 0x58A2 | 0x5858 | 0x580B |
| 0x352A | 0x580C | 0x5812 | 0x5814 | 0x580B |
| 0x3584 | 0x5841 | 0x5805 | 0x5821 | 0x586A |
| 0x3585 | 0x5841 | 0x5805 | 0x5821 | 0x586A |
| 0x3586 | 0x580C | 0x5805 | 0x580F | 0x5821 |
| 0x36B0 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x36B1 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36B2 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36B4 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36B5 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36B6 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36B7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36B8 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x36B9 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36BA | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36BB | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36BC | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36BD | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36BE | 0x5832 | 0x583D | 0x58FC | 0x5815 |
| 0x36BF | 0x580C | 0x5813 | 0x580D | 0x5814 |
| 0x36C0 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x36C1 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x36C2 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36C3 | 0x580C | 0x5846 | 0x5847 | 0x5815 |
| 0x36C4 | 0x58B8 | 0x5814 | 0x58CF | 0x58D0 |
| 0x36C5 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36C6 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36C7 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36C8 | 0x58B8 | 0x5816 | 0x5889 | 0x58D0 |
| 0x36C9 | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36CA | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36CB | 0x58B8 | 0x5881 | 0x580D | 0x58D0 |
| 0x36CC | 0x58B8 | 0x5814 | 0x58CF | 0x58D0 |
| 0x36CD | 0x58B8 | 0x58BC | 0x58BA | 0x580E |
| 0x36CE | 0x58B8 | 0x5858 | 0x583F | 0x5815 |
| 0x36CF | 0x58B8 | 0x58BA | 0x58CF | 0x58D0 |
| 0x36D0 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36D2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36D4 | 0x58BB | 0x58CD | 0x5822 | 0x58AA |
| 0x36E2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36E3 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36E4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x36E5 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36E6 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36E7 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36FA | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36FB | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36FC | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x36FD | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x36FE | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x36FF | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x3714 | 0x580C | 0x583C | 0x5898 | 0x586A |
| 0x3719 | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x371A | 0x580C | 0x58CD | 0x5822 | 0x58A2 |
| 0x371B | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x371C | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x371E | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x375A | 0x580C | 0x586F | 0x5866 | 0x586A |
| 0x375B | 0x580C | 0x586F | 0x5866 | 0x586A |
| 0x375C | 0x5832 | 0x583D | 0x58FC | 0x5815 |
| 0x375F | 0x5832 | 0x583D | 0x58FC | 0x5815 |
| 0x3760 | 0x5832 | 0x583D | 0x58FC | 0x5815 |
| 0x3761 | 0x5832 | 0x583D | 0x58FC | 0x5815 |
| 0x3778 | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x3779 | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x377A | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x377B | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x377C | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x377D | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x377E | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x378F | 0x580C | 0x5805 | 0x58EA | 0x5815 |
| 0x3791 | 0x580C | 0x5805 | 0x58EA | 0x5815 |
| 0x3792 | 0x580C | 0x5805 | 0x58EA | 0x5815 |
| 0x3796 | 0x580C | 0x586A | 0x580D | 0x5881 |
| 0x3840 | 0x5857 | 0x5887 | 0x5898 | 0x5815 |
| 0x3841 | 0x5872 | 0x5835 | 0x5842 | 0x5815 |
| 0x3842 | 0x5872 | 0x5835 | 0x5842 | 0x5815 |
| 0x3843 | 0x5857 | 0x5887 | 0x5844 | 0x5815 |
| 0x3844 | 0x5857 | 0x5887 | 0x5898 | 0x5815 |
| 0x3845 | 0x5872 | 0x5835 | 0x5842 | 0x5815 |
| 0x3848 | 0x5857 | 0x5887 | 0x5844 | 0x5815 |
| 0x384C | 0x5857 | 0x5887 | 0x5844 | 0x5815 |
| 0x3850 | 0x5857 | 0x5887 | 0x5898 | 0x5815 |
| 0x3854 | 0x5872 | 0x5835 | 0x5842 | 0x5815 |
| 0x3858 | 0x5872 | 0x5835 | 0x5842 | 0x5815 |
| 0x385C | 0x588B | 0x5835 | 0x5842 | 0x5815 |
| 0x385D | 0x5857 | 0x5887 | 0x5898 | 0x5815 |
| 0x3865 | 0x580C | 0x5852 | 0x5854 | 0x5817 |
| 0x3866 | 0x580C | 0x5852 | 0x5854 | 0x5817 |
| 0x3872 | 0x5868 | 0x5869 | 0x5823 | 0x586A |
| 0x3873 | 0x5868 | 0x5869 | 0x5823 | 0x586A |
| 0x3875 | 0x586A | 0x5898 | 0x58A5 | 0x58A4 |
| 0x3876 | 0x586A | 0x5898 | 0x58A5 | 0x58A4 |
| 0x3877 | 0x586A | 0x5898 | 0x58A5 | 0x58A4 |
| 0x3878 | 0x586A | 0x5898 | 0x58A5 | 0x58A4 |
| 0x3879 | 0x580C | 0x586A | 0x5898 | 0x584F |
| 0x387C | 0x580C | 0x586A | 0x5823 | 0x5869 |
| 0x387D | 0x589F | 0x5868 | 0x5869 | 0x5898 |
| 0x387F | 0x586B | 0x586C | 0x586E | 0x58A0 |
| 0x3886 | 0x580C | 0x583C | 0x5898 | 0x586A |
| 0x3887 | 0x580C | 0x583C | 0x5898 | 0x586A |
| 0x3888 | 0x580C | 0x583C | 0x5898 | 0x586A |
| 0x38A4 | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38A7 | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38A8 | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38A9 | 0x580C | 0x5852 | 0x5854 | 0x5817 |
| 0x38AA | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38AB | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38AC | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38B2 | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38B4 | 0x580C | 0x5852 | 0x5853 | 0x5815 |
| 0x38D6 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38D7 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38D8 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38EF | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38F0 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38F1 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0x38F2 | 0x580C | 0x58EF | 0x583B | 0x5805 |
| 0x38F3 | 0x580C | 0x58EF | 0x583B | 0x5805 |
| 0x3908 | 0x5825 | 0x586A | 0x5817 | 0x5820 |
| 0x3909 | 0x5825 | 0x586A | 0x5817 | 0x5820 |
| 0x390A | 0x5825 | 0x586A | 0x5817 | 0x5820 |
| 0x390B | 0x5825 | 0x586A | 0x5817 | 0x5820 |
| 0x390C | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x390D | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x390E | 0x580C | 0x5823 | 0x5821 | 0x586A |
| 0x393A | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x393B | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x393C | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x393D | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3B94 | 0x5825 | 0x586A | 0x5817 | 0x5820 |
| 0x3B97 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3B99 | 0x580C | 0x5805 | 0x58EA | 0x5815 |
| 0x3B9A | 0x580C | 0x5805 | 0x58EA | 0x5815 |
| 0x3B9B | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3B9C | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3B9D | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BC4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BC5 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BC6 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BC7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BC8 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BCC | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BCD | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BCE | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BCF | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD0 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD1 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD3 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD5 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD6 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD8 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BD9 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDA | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDB | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDC | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDD | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDE | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BDF | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BE0 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BE1 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BE2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BE7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BEC | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BED | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BF0 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BF1 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0x3BF4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD83 | 0x580C | 0x5821 | 0x580D | 0x5815 |
| 0xCD85 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD86 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD87 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD89 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD8B | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD8C | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD8F | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD91 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD92 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD95 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD98 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD9B | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD9D | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCD9E | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA1 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA5 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA6 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA8 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDA9 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDAA | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDAB | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDAC | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDAD | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB0 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB1 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB2 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB3 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB4 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB6 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB7 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB8 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDB9 | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xCDBA | 0x580C | 0x5821 | 0x586A | 0x588B |
| 0xFFFF | 0x58FF | 0x58FF | 0x58FF | 0x58FF |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 444 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4200 | Ansaugluft-Temperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4201 | Umgebungsdruck | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x4202 | Saugrohr-Absolutdruck | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x4203 | Massenstrom HFM | kg/h | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4204 | Umgebungstemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4205 | Druck vor Drosselklappe | hPa | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| 0x4300 | Motor-Temperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4303 | empf. Temperatur von BSS-Wasserpumpe | Grad C | - | unsigned char | - | 1,0 | 1 | -50,0 |
| 0x4304 | empf. Strom von BSS-Wasserpumpe | % | - | unsigned char | - | 0,5 | 1 | 0,0 |
| 0x4305 | empf. Istdrehzahl von BSS-Wasserpumpe | 1/min | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4306 | Quittung  Solldrehzahl von BSS-Wasserpumpe | 1/min | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4307 | empf. Status von BSS-Wasserpumpe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4400 | Langzeit-Ölniveau-Mittelwert für den DIS-Tester | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x4401 | Relativer Füllstand des Motoröls | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4402 | Oeltemperatur nach Filter | Grad C | - | unsigned integer | - | 0,75 | 1 | -48,0 |
| 0x4403 | Kraftstoffverbrauch seit letztem Ölwechsel | - | - | unsigned long | - | 1,220703125E-4 | 1 | 0,0 |
| 0x4404 | Ölkilometer | km | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| 0x4405 | Sensorrohwert Ölniveau | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4406 | Sensorrohwert Permittivität | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4407 | Sensorrohwert Öltemperatur | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4408 | Öltemperatur ungefiltert | Grad C | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4409 | Ölniveau ungefiltert in [mm] | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x440A | Permitivität für den Tester | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x440B | CodingDataSet-ÖL-Länderfaktor1- EEPROM | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440C | CodingDataSet-ÖL-Länderfaktor2- EEPROM | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440D | Länderfaktor 1 | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440E | Länderfaktor 2 | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440F | Kurzzeit-Ölniveau-Mittelwert für den DIS-Tester | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x4411 | Restweg aus Kraftstoffverbrauch abgeleitet | - | - | signed integer | - | 10,0 | 1 | 0,0 |
| 0x4412 | Öllaufzeit | month | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4418 | Status Ölzustandssensor | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4501 | VVT Excenterwellenadaptionswert | mm | - | signed integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x4505 | Sollwinkel vom BMW Layer (Einlass-VANOS) | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x4506 | Nockenwellenposition Einlass | Grad KW | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4507 | Nockenwellenposition Auslass | Grad KW | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4508 | Winkel Einlassventil oeffnet bezogen auf LWOT | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x4509 | Winkel Auslassventil schließt bezogen auf LWOT | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x450C | Adaption Kurbel/Einlassnockenwelle erfolgt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x450D | Adaption Kurbel/Auslassnockenwelle erfolgt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x450E | [0] Nullpunktverschiebung in Grad KW für die Winkelversatz Diag, bedingt d. Toleranzen d. Einbaulage | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x4510 | Bedingung VVT-Lagereglerüberwachung hat bleibende Regelabweichung erkannt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4511 | Bedingung VVT-Lageregler schwingt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4512 | Bedingung: VVT Motor Überlast Warnschwelle | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4513 | Bedingung VVT-Überlastung (klemmender Steller) | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4514 | Bedingung VVT-Adaption möglich | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4515 | Anforderung VVT-Anschlaglernen (intern) | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4516 | Status VVT-Anschlaglernen (intern) | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4517 | [0] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 0 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x4518 | [1] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 1 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x4519 | [2] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 2 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451A | [3] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 3 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451B | [4] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 4 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451C | [5] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 5 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451D | Gesamtzeit VVT-Performancetest | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x451E | Stromsumme VVT-Performancetest | A | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4600 | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | - | signed integer | - | 0,0244140625 | 1 | 0,0 |
| 0x4601 | Sollwert Drosselklappenwinkel, bezogen auf (unteren) Anschlag | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4602 | phys. Wert Generatorsollspannung (Volt) für Komponententreiber Generator | V | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| 0x4603 | Chiptemperatur Generator 1 | Grad C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x4604 | Generatorstrom | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4605 | Chipversion Generator 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4606 | Reglerversion on Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4607 | Kennung Generator Hersteller | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4608 | Kennung Generatortyp | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x460A | momentane Batteriespannung | V | - | unsigned integer | - | 0,014999999664723873 | 1 | 0,0 |
| 0x460B | aktuelle Batteriespannung | V | - | unsigned integer | - | 2,500000118743628E-4 | 1 | 6,0 |
| 0x460C | Batteriespannung; vom AD-Wandler erfaßter Wert  | V | - | unsigned integer | - | 0,02355000004172325 | 1 | 0,0 |
| 0x460D | Korrekturwert Abschaltung | % | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 |
| 0x460E | Abstand zur Startfähigkeit | % | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 |
| 0x460F | DF-Monitor für Batterie-Ladezustand in % | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4611 | Tastverhältnis E-Lüfter | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4612 | Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x4613 | vom Generator empfangene Generatorsollspannung (Kopie gesendeter Wert) | V | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| 0x4614 | Auslastungsgrad Generator 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4615 | Kopie begrenzter Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x4616 | vom Generator empfangene Load response Zeit (Kopie gesendeter Wert) | s | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4617 | gefiltertes Generatormoment absolut | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4618 | Drehzahlschwelle für LR-Funktion Generator 1 aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4619 | Bedingung BSD Protokollinhalt für BSD2 Regler | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x461A | Nominalspannung Regler Generator 1 | V | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| 0x4680 | Leerlaufdrehzahl gelernt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4681 | Getriebe ist bereit die Neutralposition anzulernen | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4700 | Bedingung Sonde betriebsbereit vor Kat | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4701 | Bedingung Sonde betriebsbereit vor Kat, Bank 2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4702 | Offset korrigierte Sondenspannung vor Kat einer Breitbandlambdasonde | V | - | unsigned integer | - | 4,8828125E-4 | 1 | 0,0 |
| 0x4703 | Offset korrigierte Sondenspannung vor Kat einerBreitbandlambdasonde Bank 2 | V | - | unsigned integer | - | 4,8828125E-4 | 1 | 0,0 |
| 0x4704 | Lambdasoll Begrenzung (word) | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x4705 | Lambdasoll Begrenzung (word) Bank2 | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x4800 | Bedingung Kupplungspedal betätigt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4801 | Schalter Kupplung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4802 | Bedingung umschalten auf KFPEDS | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4803 | Bedingung für Kompressoreinschalten | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4805 | Schalter Klemme 50 von CAN | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4806 | Steuergerätetemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4807 | Motordrehzahl | 1/min | - | unsigned integer | - | 0,25 | 1 | 0,0 |
| 0x4808 | Leerlaufsolldrehzahl | 1/min | - | unsigned integer | - | 0,25 | 1 | 0,0 |
| 0x4809 | Bedingung Leerlaufregelung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x480A | Wegstrecke_km auf 1km genau | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x480B | normierter Fahrpedalwinkel | %PED | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| 0x4880 | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Leerlauf bez. auf Schwellwert | % | - | unsigned char | - | 0,78125 | 1 | 0,0 |
| 0x4881 | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Teillast bez. auf Schwellwert | % | - | unsigned char | - | 0,78125 | 1 | 0,0 |
| 0x4890 | Tprot-Status auslesen | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5800 | Zeitzähler ab Startende (16bit) | s | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5801 | Umgebungsdruck | hPa | - | unsigned char | - | 5,0 | 1 | 0,0 |
| 0x5802 | CARB FREEZE FRAME Byte, Bank 1, für LR | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5804 | relative Luftmasse (calc. load value) nach SAE J1979 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5805 | Motortemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5806 | Lambda-Regler-Ausgang (Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5807 | Faktor aus Lambdaregelungsadaption für Bank 1 | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x580B | Saugrohr-Absolutdruck (Word) | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x580C | Motordrehzahl | 1/min | - | unsigned char | - | 40,0 | 1 | 0,0 |
| 0x580D | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1,25 | 1 | 0,0 |
| 0x580E | Zündwinkel Zylinder 1 | Grad KW | - | signed char | - | 0,75 | 1 | 0,0 |
| 0x580F | Ansaugluft-Temperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5810 | relative Luftmasse (calc. load value) nach SAE J1979 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5812 | Massenstrom HFM 16-Bit Größe | kg/h | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5813 | relative Luftfüllung | % | - | unsigned char | - | 0,75 | 1 | 0,0 |
| 0x5814 | Normierter Fahrpedalwinkel | %PED | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5815 | Batteriespannung | V | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| 0x5816 | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5817 | Umgebungstemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5818 | Luftmassenfluß | kg/h | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x5819 | Motordrehzahl [1/min] | rpm | - | signed integer | - | 0,5 | 1 | 0,0 |
| 0x581A | Winkel Einlassventil oeffnet bezogen auf LWOT | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581B | Sollwinkel Nockenwelle Einlass öffnet | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581C | Winkel Auslassventil schließt bezogen auf LWOT | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581D | Sollwinkel Nockenwelle Auslass schließt | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581E | Ansauglufttemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x581F | Motortemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5820 | Status Klemme 15 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5821 | Steuergerätetemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5822 | Öltemperatur | Grad C | - | unsigned char | - | 1,0 | 1 | -60,0 |
| 0x5823 | Abstellzeit | s | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5825 | Spannung BCU LIN | V | - | signed integer | - | 0,009999999776482582 | 1 | 0,0 |
| 0x5826 | Drosselklappenwinkel aus Poti 1 | %DK | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5827 | Tastverhältnis für Lambdasondenheizung | % | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x5829 | normierte Heizleistung der Lambdasonde hinter Kat | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x582B | Drehmomentaufnahme des Wandlers über CAN | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x582C | Lambdasondenistwert, korrigiert um Zusatzamplitude | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x582D | Korrekturwert der LSU-Spannung vor Kat | V | - | signed integer | - | 4,8828125E-4 | 1 | 0,0 |
| 0x582F | Abgastemperatur nach Katalysator aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x5830 | Dynamikwert der LSU | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5832 | Zustand Motor-Koordinator | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5834 | Umgebungsdruck von Sensor | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x5835 | Kennung Generator Hersteller | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5836 | gefilterter Drehzahlgradient | 1/min/s | - | signed char | - | 100,0 | 1 | 0,0 |
| 0x5837 | Solldruck Hochdrucksystem | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x5838 | Relatives Moment für Aussetzererkennung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5839 | Bedingung Sicherheitskraftstoffabschaltung (SKA) | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x583A | Ansaugluft-Temperatur bei Start | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x583B | Fuellstand Kraftstofftank | L | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x583C | Batteriespannung; vom AD-Wandler erfasster Wert | V | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| 0x583D | Betriebsstundenzaehler | min | - | unsigned integer | - | 6,0 | 1 | 0,0 |
| 0x583E | Dauer-RAM: Sollwert DK-Winkel in NLP-Stellung, bez. auf UMA | %DK | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| 0x583F | Sollwert DK-Winkel, bezogen auf unteren Anschlag | %DK | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5840 | DK-Winkel der Notluftposition | %DK | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| 0x5841 | Wert Temperatur Steuergerät | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5842 | Kennung Generatortyp | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5844 | Chiptemperatur Generator 1 | Grad C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x5845 | Sondenspannung vor Kat einer Breitbandlambdasonde (ADC-Wert) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5846 | Spannung PWG-Poti 1 (Word) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5847 | Spannung PWG-Poti 2 (Word) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5849 | ADC-Spannung Lambdasonde hinter Katalysator (Word) | V | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| 0x584C | Spannung DK-Poti 2 | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x584D | Massenstrom Tankentlüftung in das Saugrohr | kg/h | - | unsigned integer | - | 3,906250058207661E-4 | 1 | 0,0 |
| 0x584E | Spannung DK-Poti 1 | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x584F | Erkennung Bordnetzinstabilität | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5850 | Signalspannung des Kühlmitteltemperatursensors | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5851 | Spannungswert des Ansauglufttemperatursensors tfa2 (SY_TFAKON &gt; 0) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5852 | Batteriestrom von IBS | A | - | unsigned integer | - | 0,019999999552965164 | 1 | -200,0 |
| 0x5853 | Batt Spannung von IBS | V | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x5854 | BattTemp von IBS | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5855 | schneller Mittelwert des Lambdaregelfaktors (Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5857 | Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x5858 | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5859 | Pumpenstrom Referenzleck | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x585A | min. Pumpenstrom bei Grobleckmessung | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x585B | Pumpenstrom am Ende der Feinstleckmessung | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x585C | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | - | unsigned char | - | 512,0 | 1 | 0,0 |
| 0x585E | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | - | unsigned char | - | 2,0 | 1 | 0,0 |
| 0x5860 | Innenwiderstand der Nernstzelle der LSU | Ohm | - | unsigned char | - | 10,0 | 1 | 0,0 |
| 0x5862 | Sollwert Öldruck | kPa | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5863 | Innenwiderstand der Nernstzelle der LSU | Ohm | - | unsigned char | - | 0,0390625 | 1 | 0,0 |
| 0x5865 | Langzeit-Ölniveau-Mittelwert für den DIS-Tester | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x5866 | Relativer Füllstand des Motoröls | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5867 | Fahrstrecke des Fahrzeugs als Information über CAN | km | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| 0x5868 | Status Standverbraucher registriert Teil 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5869 | Status Standverbraucher registriert Teil 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x586A | aktuelle Batteriespannung | V | - | unsigned integer | - | 2,500000118743628E-4 | 1 | 6,0 |
| 0x586B | Zeit, indem der Ruhestrom bei 80..200mA liegt | min | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| 0x586C | Zeit, indem der Ruhestrom bei 200..1000mA liegt | min | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| 0x586E | Zeit, indem der Ruhestrom größer als 1000mA liegt | min | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| 0x586F | Öldruck | hPa | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5870 | Spannung Umgebungsdrucksensor (word 10-Bit von ADC) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5871 | Zähler Prüfzustand für VVT Endstufenprüfung | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5872 | Reglerversion on Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5874 | ADC-Spannung Pumpenstrom Tankdiagnose | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x5875 | Indiziertes Soll-Motormoment MSR | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5876 | Schnittstelle für Scan Tool Mode $01/$02 Raildruck Rohwert PID$23 | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x5878 | I-Anteil der stetigen LRSHK Variante kontinuierlich | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x587B | Anzahl erkannter VVT Lageregelungsfehlerwarnungen irreversibel | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x587E | Anzahl erkannter VVT Lageregelungsfehlerwarnungen reversibel | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x587F | Tastverhältnis E-Lüfter | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5880 | Tastverhältnis GLF System | % | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5881 | Ist-Gang | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5882 | Motorstarttemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5883 | [0] Spannung Klopfwerte Zylinder 1 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5884 | Kopie begrenzter Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x5885 | [2] Referenzpegel Klopfregelung, 16bit | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5886 | [3] Referenzpegel Klopfregelung, 16bit | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5887 | Auslastungsgrad Generator 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5888 | [5] Spannung Klopfwerte Zylinder 4 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5889 | Lambda-Istwert | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x588B | Zeit nach Startende | s | - | unsigned integer | - | 0,009999999776482582 | 1 | 0,0 |
| 0x588C | Keramiktemperatur der LSU | Grad C | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| 0x588D | aktuelle Zeit Leckmessung | s | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x588E | Pumpenstrom Tankdiagnose | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x5891 | Kupplungsmotormoment Istwert | Nm | - | signed integer | - | 0,5 | 1 | 0,0 |
| 0x5893 | Indiziertes Soll-Motormoment GS für schnellen Eingriff | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5894 | [4] Spannung Klopfwerte Zylinder 2 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5895 | [1] Spannung Klopfwerte Zylinder 5 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5896 | Abgastemperatur hinter Hauptkat aus Modell | Grad C | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| 0x5898 | phys. Wert Generatorsollspannung (Volt) für Komponententreiber Generator | V | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| 0x5899 | Bedingung Anforderung Motorrelais einschalten | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x589B | Bedingung unzulässig hoher Motorstrom bei Kurzschluss erkannt | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x589C | Bedingung Freigabe VVT-Endstufe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x589D | Anzahl erkannter VVT Lageregelungsfehler | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x589E | Sollwert Exzenterwinkel VVT | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x589F | Batterietemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x58A0 | Entladung während Ruhestromverletzung | Ah | - | unsigned integer | - | 0,018204445019364357 | 1 | 0,0 |
| 0x58A1 | Umweltbedingung Kilometerstand für Fehlerspeichereintrag | km | - | unsigned integer | - | 8,0 | 1 | 0,0 |
| 0x58A2 | Istwert Exzenterwinkel VVT | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A3 | rel. Exzenterwinkel am oberen mech. Anschlag | Grad | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A4 | Generatorstatus | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58A5 | Vom Generator empfangenes Lastsignal | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58A6 | Relativer Exzenterwinkel | Grad | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A7 | Abstellzeit aus relativem Minutenzähler bis Motorstart | min | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58A8 | rel. Exzenterwinkel am unteren mech. Anschlag | Grad | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A9 | VVT Verstellbereich aus Urlernvorgang | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AA | Verstellbereich des Exzenterwinkels | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AB | DLR für DV-E: Summe der PID-Anteile | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x58AD | Sauerstoffspeichervermögen des Katalysators, temperatur- und luftmassenstrombezogen | mg | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AE | Peridendauer für Massenstrom aus HFM | us | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AF | EKP-Sollvolumenstrom | l | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B0 | Zähler für Lerndauer eines Lernsteps | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B1 | [0] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 1 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B2 | [1] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 5 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B3 | [2] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 3 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B4 | [3] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 6 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B5 | [4] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 2 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B6 | [5] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 4 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B7 | aktueller Bremsdruck | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B8 | Motordrehzahl in der Funktionsüberwachung | 1/min | - | unsigned char | - | 40,0 | 1 | 0,0 |
| 0x58B9 | Pedalsollwert (8 Bit) in der Funktionsüberwachung | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x58BA | Bank mittel eingespritzte effektive relative Krafftstoffmasse (inkl. Reduzierstufe) | % | - | unsigned integer | - | 0,046875 | 1 | 0,0 |
| 0x58BB | Strom für VVT-Motor | A | - | signed integer | - | 0,006103515625 | 1 | 0,0 |
| 0x58BC | relative Luftfüllung in der Funktionsüberwachung | % | - | unsigned char | - | 0,75 | 1 | 0,0 |
| 0x58BD | Status Fehler Überlast VVT1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58BE | DV-E-Adaption: Status Prüfbedingungen | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C0 | VVT-Endstufentemperatur aus Modell | Grad C | - | unsigned integer | - | 0,75 | 1 | -48,0 |
| 0x58C8 | geforderte Drehmomentänderung von der LLR (I-Anteil) | % | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x58C9 | Ansteuerungsmodus für den VVT Motor | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58CA | geforderte MD-Änderung von der LLR (PD-Zündungsanteil) | % | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x58CB | Aufsummierte thermische Belastung VVT | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58CC | Tastverhältnis zur Ansteuerung des VVT-Stellmotors | % | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x58CD | Spannung hinter VVT-Relais | V | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58CE | Carrierbyte Schalterstati | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58CF | Momentenanforderung vom Getriebe in der Funktionsüberwachung | Nm | - | signed integer | - | 0,0625 | 1 | 0,0 |
| 0x58D0 | Berechnetes Ist-Moment in der Funktionsüberwachung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58D2 | Status Luftklappensystem High Byte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58D3 | Status Luftklappensystem Low Byte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58D4 | Startbedingung Kraftschluss erfüllt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x58D5 | physikalischer Temperaturwert, der sich bei Wandlung der elektrischen Sensorspannung wtfa1_w ergibt | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x58D7 | Spannungswert des Ansauglufttemperatursensors tfa1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x58D8 | Differenz-DK-Winkel Sollwert - Istwert (wdkdlr_w - wdkba_w) | %DK | - | signed integer | - | 0,0244140625 | 1 | 0,0 |
| 0x58D9 | Schrittzähler DK-Rückstellfeder-Prüfung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58DA | koordiniertes Moment für Füllung | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x58DB | Fehlerzähler Summe, zählt abgasrelevante Aussetzer über alle Zylinder | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58DC | Intervallzähler für abgasrelevante Aussetzer | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58DD | Druck vor Drosselklappe Rohwert | hPa | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| 0x58DE | Spannung Drucksensor vor Drosselklappe | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x58E0 | Abgleich DK-Modell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58E1 | Abgleich DK-Modell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58E2 | Abgleich EV-Modell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58E3 | Abgleich EV-Modell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58E4 | Ist-Betriebsart | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58E5 | Rotorposition VVT-Motor | ° | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58E6 | Soll-Bestromung VVT-Motor | A | - | signed integer | - | 0,006103515625 | 1 | 0,0 |
| 0x58E9 | empf. Spannung von BSS-Wasserpumpe | V | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58EA | empf. Istdrehzahl von BSS-Wasserpumpe | 1/min | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58EC | empf. Temperatur von BSS-Wasserpumpe | Grad C | - | unsigned char | - | 1,0 | 1 | -50,0 |
| 0x58ED | empf. Strom von BSS-Wasserpumpe | % | - | unsigned char | - | 0,5 | 1 | 0,0 |
| 0x58EF | Gefilterter Raildruck-Istwert (Absolutdruck) | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x58F0 | ungefilterter Raildruck Istwert (abs.) | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x58F2 | PWM signal for the VCV | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x58F3 | Ungefilterter Niederdruck Rohwert | kPa | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58F4 | Spannung Kraftstoffniederdrucksensor im 1 ms Raster | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x58F5 | Spannung Diagnose-Port VVT-Ansteuerung (3V ADC) | V | - | unsigned char | - | 0,012890624813735485 | 1 | 0,0 |
| 0x58F6 | Sollspannung des VVT Lagereglers | V | - | signed integer | - | 7,812500116415322E-4 | 1 | 0,0 |
| 0x58F7 | Statusbyte Strommessung plausibel | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58FA | gefilterter Faktor Tankentlüftungs-Adaption | - | - | signed char | - | 0,5 | 1 | 0,0 |
| 0x58FC | Fertigungs-Werkstatt-,Transportmodus | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58FF | Umweltbedingung unbekannt | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x5A02 | ATL-Leckagediagnose läuft | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A04 | Spannung PWG-Poti 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A05 | Spannung PWG-Poti 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A06 | Spannung DK-Poti 1 | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x5A07 | Spannung DK-Poti 2 | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x5A08 | Spannungswert des Ansauglufttemperatursensors tfa1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A09 | Signalspannung des Kühlmitteltemperatursensor | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A0B | Spannung Umgebungsdrucksensor (word 10-Bit von ADC) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A0C | Spannungswert des Ansauglufttemperatursensors tfa2 (SY_TFAKON &gt; 0) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A0E | Wert Temperatur Steuergerät | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5A11 | Spannung Lambdasonde vor Katalysator | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A13 | Spannung Lambdasonde hinter Katalysator | V | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| 0x5A14 | Spannung Lambdasonde (4.88mV/LSB) hinter Katalysator 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| 0x5A17 | Spannung Pumpenstrom Tankdiagnose | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A1B | Elektrische Kraftstoffpumpe | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A1D | Spannung Bremsenunterdruck | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A1E | Differenz zwischen Umgebungsdruck und Bremskraftverstärkerdruck von Drucksensor (Rohwert) | hPa | - | signed integer | - | 0,0390625 | 1 | 0,0 |
| 0x5A20 | Peridendauer für Massenstrom aus HFM | us | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5A21 | Kühlmitteltemperatur (Sensorwert) nach Tiefpassfilterung | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5A23 | Sollwert Öldruck | kPa | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5A24 | Sollwert Drosselklappenwinkel, bezogen auf (unteren) Anschlag | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A25 | Öldruck | hPa | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A29 | normierter Fahrpedalwinkel | %PED | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| 0x5A2B | physikalischer Temperaturwert, ergibt sich bei Wandlung der tiefpassgefilterten Sensorspg. wtfa1f_w | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5A2D | Saugrohr-Absolutdruck gemessen | hPa | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| 0x5A2E | Ungefilterter Niederdruck Rohwert | kPa | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5A2F | Gefilterter Raildruck-Istwert (Absolutdruck) | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x5A30 | [0] Laufunruhe Zylinder 1 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A31 | [4] Laufunruhe Zylinder 2 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A32 | [2] Laufunruhe Zylinder 3 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A33 | [5] Laufunruhe Zylinder 4 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A34 | [1] Laufunruhe Zylinder 5 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A35 | [3] Laufunruhe Zylinder 6 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x5A36 | Bedingung für erkannte Klopfer | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A37 | [0] normierter Referenzpegel Klopfregelung Zylinder 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A38 | [4] normierter Referenzpegel Klopfregelung Zylinder 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A39 | [2] normierter Referenzpegel Klopfregelung Zylinder 3 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A3A | [5] normierter Referenzpegel Klopfregelung Zylinder 4 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A3B | [1] normierter Referenzpegel Klopfregelung Zylinder 5 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A3C | [3] normierter Referenzpegel Klopfregelung Zylinder 6 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A49 | [0] Ausgegebener Zündwinkel | Grad KW | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5A4B | relative Luftmasse (calc. load value) nach SAE J1979 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A50 | Lambda-Istwert | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5A51 | Lambda-Istwert Bank2 | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5A52 | Bedingung Sonde betriebsbereit hinter Kat | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A53 | Bedingung Sonde betriebsbereit hinter Kat Bank2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A54 | Bedingung Sonde hinter Kat ausreichend beheizt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A55 | Bedingung Sonde 2 hinter Kat ausreichend beheizt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A56 | Bedingung: Heizerstatus A liegt vor, Sonde ist ausreichend aufgeheizt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A57 | Bedingung: Heizerstatus A liegt vor, Sonde ist ausreichend aufgeheizt, Bank2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A58 | Tastverhältnis für Lambdasondenheizung | % | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x5A59 | normierte Heizleistung der Lambdasonde hinter Kat | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x5A5A | Tastverhältnis für Lambdasondenheizung, Bank 2 | % | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x5A60 | Bedingung Bremslichtschalter betätigt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A61 | Bedingung Bremstestschalter betätigt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A65 | Bedingung Abgasklappe mit Resonator | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A66 | Bedingung DMTL-Pumpenmotor an | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A67 | Bedingung DMTL-Magnetventil an | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A68 | Bedingung Heizung DMTL Portansteuerung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A69 | MIL-Ansteuerung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6A | Lampe FGR Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6B | Bedingung für Ansteuerung EGAS-Fehlerlampe | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6C | Korrekturfaktor für die Kraftstoffmenge | % | - | signed char | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x5A74 | Tastverhältnis Kennfeldthermostat | - | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5A77 | ausgegebenes Tastverhältnis für Tankentlüftungsventil (16 Bit) | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A78 | Bedingung Abgasklappe mit Resonator | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A7A | Tastverhältnis Einlaßnockenwellenregelung Ansteuerung Endstufe(word) | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A7B | Tastverhältnis Auslaßnockenwellenregelung Ansteuerung Endstufe(word) | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A81 | Lambda-Regler-Ausgang (Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5A85 | multiplikative Gemischkorrektur der Gemischadaption (Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5A91 | Amplitudenverhältnis laafh/laafv gefiltert | - | - | unsigned char | - | 0,00390625 | 1 | 0,0 |
| 0x5A93 | Fehlerzähler für Lernen Nullgang | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5A94 | gespeicherter Nockenwellensollwinkel Auslaß | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x5A95 | [0] Adaptionswert Nockenwelle Auslass Bank 1 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x5A96 | [0] Adaptionswert Nockenwelle Einlass Bank 1 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x5A97 | Bedi. Vanos Einlass im Anschlag | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A99 | Status der fuel-off Adaption im aktuellen Betriebsbereich | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5A9D | multiplikative Gemischkorrektur der Gemischadaption | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5AA1 | Zyklusflag: Tankentlüftungsventil Endstufe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AA2 | Funktionsstatus-Zähler DM-TL für Testerausgabe aus letztem Fahrzyklus | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AA4 | Funktionsstatus LLRNS bei Anforderung Systemcheck | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AA9 | Tastverhältnis GLF System | % | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AAA | Tastverhältnis PWM Ansteuerung Öldruck | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AAB | Tastverhältnis an Endstufe des Ladedruckstellers | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AAC | Tastverhältnis an Endstufe des Ladedruckstellers, Bank 2 | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AB0 | Ladedruck- Sollwert | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x5AB1 | Fahrzeuggeschwindigkeit | km/h | - | unsigned integer | - | 0,0078125 | 1 | 0,0 |
| 0x5AB3 | Zähler für gefahrene Kilometer mit MIL EIN | km | - | unsigned long | - | 0,009999999776482582 | 1 | 0,0 |
| 0x5AB4 | sekundengenauer Betribsstundenzähler als 32 Bitwert | s | - | unsigned long | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5AB6 | Ansauglufttemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5AB7 | Motortemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5AB8 | Spannung Drucksensor Saugrohrdruck (word) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5ABC | Luftmassenfluss gefiltert (Word) | kg/h | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5ABD | Bedingung automatischer Start | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5ABE | I-Regler Mengenregelung Kraftstoffsystem | mg | - | signed integer | - | 0,0211944580078125 | 1 | 0,0 |
| 0x5ABF | Verbrauch ohne Regler | l/h | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 |
| 0x5AC0 | Verbrauch mit Regler | l/h | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 |
| 0x5AC2 | Reset Information  | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AC4 | Raildruck Kraftstoffsystem Sollwert | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x5AC5 | Tastverhältnis Mengensteuerventil | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AC6 | Modus Kraftstoffsystem (Druck-, Mengen-, Max-Regelung) | 0-n | - | 0xFF | ba_vcv_state_text | 1 | 1 | 0 |
| 0x5AD5 | Kraftstofftemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5AD6 | Bedingung Schubabschalten | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5AE2 | Reset Information - Reset-group-ID of the last reset reason | 0-n | - | 0xFF | Reset_GrpID | 1 | 1 | 0 |
| 0x5AE3 | Reset Information - Reset-ID of the last reset | 0-n | - | 0xFFFF | Reset_ID | 1 | 1 | 0 |
| 0x5AE4 | Reset Information - User defined value of the last reset reason | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AEB | Kühlmitteltemperatur &lt; 98°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEC | 98°C =&lt; Kühlmitteltemperatur =&lt; 112°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AED | 113°C =&lt; Kühlmitteltemperatur =&lt; 120°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEE | 121°C =&lt; Kühlmitteltemperatur =&lt; 125°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEF | Kühlmitteltemperatur &gt; 125°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF0 | Motoröltemperatur &lt; 80°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF1 | 80°C =&lt; Motoröltemperatur =&lt; 110°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF2 | 110°C =&lt; Motoröltemperatur =&lt; 135°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF3 | 135°C =&lt; Motoröltemperatur =&lt; 150°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF4 | Motoröltemperatur &gt; 150°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF5 | Getriebeöltemperatur &lt; 80°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF6 | 80°C =&lt; Getriebeöltemperatur =&lt; 109°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF7 | 110°C =&lt; Getriebeöltemperatur =&lt; 124°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF8 | 125°C =&lt; Getriebeöltemperatur =&lt; 129°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF9 | Getriebeöltemperatur &gt; 129°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFA | Umgebungstemperatur &lt; 3°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFB | 3°C =&lt; Umgebungstemperatur =&lt; 19°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFC | 20°C =&lt; Umgebungstemperatur =&lt; 29°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFD | 30°C =&lt; Umgebungstemperatur =&lt; 39°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFE | Umgebungstemperatur &gt; 39°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5B10 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B11 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B12 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B13 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B14 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B15 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B20 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B21 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B22 | Superklopfen | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B23 | [0] Aussetzerzähler im Abgasintervall Zyl. 1 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B24 | [4] Aussetzerzähler im Abgasintervall Zyl. 2 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B25 | [2] Aussetzerzähler im Abgasintervall Zyl. 3 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B30 | [5] Aussetzerzähler im Abgasintervall Zyl. 4 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B31 | [1] Aussetzerzähler im Abgasintervall Zyl. 5 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5B32 | [3] Aussetzerzähler im Abgasintervall Zyl. 6 | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 15 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x1001 | Fehler Laenge Argument Ungueltig |
| 0x1002 | Fehler Argument in Tabelle nicht vorhanden |
| 0x1003 | Fehler Argument nicht vorhanden |
| 0x1004 | Fehler 1004 |
| 0x1005 | Fehler Resultwert ausserhalb gueltigem Bereich |
| 0x1006 | Fehler 1006 |
| 0x1007 | Fehler Rueckgabe Job fehlerhaft |
| 0x1008 | Fehler Rueckgabe Service fehlerhaft |
| 0x1009 | Fehler physikalischer Wert ausserhalb gueltigem Bereich |
| 0x100A | Fehler 100A |
| 0x100B | Fehler Unterlauf Fehler |
| 0x100C | Fehler Joblaenge falsch |
| 0x100E | Fehler 100E |
| 0x100F | Fehler Argument Wert im negativ Bereich |
| 0xXY | ERROR_UNKNOWN |

<a id="table-messwertetab"></a>
### MESSWERTETAB

Dimensions: 429 rows × 12 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ITANS | 0x4200 | STAT_ANSAUGLUFTTEMPERATUR_WERT | Ansaugluft-Temperatur | Grad C | tans | - | unsigned char | - | 0,75 | 1 | -48,0 |
| IPUMG | 0x4201 | STAT_UMGEBUNGSDRUCK_WERT | Umgebungsdruck | hPa | pu_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| IPSAU | 0x4202 | STAT_SAUGROHRDRUCK_WERT | Saugrohr-Absolutdruck | hPa | ps_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| ILMKG | 0x4203 | STAT_LUFTMASSE_WERT | Massenstrom HFM | kg/h | mshfm_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| ITUMG | 0x4204 | STAT_UMGEBUNGSTEMPERATUR_WERT | Umgebungstemperatur | Grad C | tumg | - | unsigned char | - | 0,75 | 1 | -48,0 |
| IPLAD | 0x4205 | STAT_LADEDRUCK_WERT | Druck vor Drosselklappe | hPa | pvd_w | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| ITKUM | 0x4300 | STAT_KUEHLMITTELTEMPERATUR_WERT | Motor-Temperatur | Grad C | tmot | - | unsigned char | - | 0,75 | 1 | -48,0 |
| ITWAE | 0x4303 | STAT_WASSERPUMPE_ELEKTRONIK_TEMPERATUR_WERT | empf. Temperatur von BSS-Wasserpumpe | Grad C | wmt | - | unsigned char | - | 1,0 | 1 | -50,0 |
| IIWAP | 0x4304 | STAT_WASSERPUMPE_STROM_WERT | empf. Strom von BSS-Wasserpumpe | % | wmi | - | unsigned char | - | 0,5 | 1 | 0,0 |
| INWAP | 0x4305 | STAT_WASSERPUMPE_DREHZAHL_WERT | empf. Istdrehzahl von BSS-Wasserpumpe | 1/min | wmpdzi | - | unsigned char | - | 1,0 | 1 | 0,0 |
| SNWAP | 0x4306 | STAT_WASSERPUMPE_DREHZAHL_SOLL_WERT | Quittung  Solldrehzahl von BSS-Wasserpumpe | 1/min | wmpdzst | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4307_WERT | 0x4307 | STAT_0x4307_WERT | empf. Status von BSS-Wasserpumpe | - | wmstat | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IMLOE | 0x4400 | STAT_OELSTAND_LANGZEIT_MITTEL_WERT | Langzeit-Ölniveau-Mittelwert für den DIS-Tester | - | oznivlangt | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| IFSOE | 0x4401 | STAT_FUELLSTAND_MOTOROEL_WERT | Relativer Füllstand des Motoröls | - | oelstandr | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ITOEL | 0x4402 | STAT_OELTEMPERATUR_WERT | Oeltemperatur nach Filter | Grad C | toel_w | - | unsigned integer | - | 0,75 | 1 | -48,0 |
| IKVLS | 0x4403 | STAT_KRAFTSTOFFVERBRAUCH_SEIT_SERVICE_WERT | Kraftstoffverbrauch seit letztem Ölwechsel | - | ozkvbsm_ul | - | unsigned long | - | 1,220703125E-4 | 1 | 0,0 |
| IKMLS | 0x4404 | STAT_WEG_SEIT_SERVICE_WERT | Ölkilometer | km | ozoelkm | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| RNIOE | 0x4405 | STAT_OELSENSOR_NIVEAU_ROH_WERT | Sensorrohwert Ölniveau | - | oznivr | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| RQUOE | 0x4406 | STAT_OELSENSOR_QUALITAET_ROH_WERT | Sensorrohwert Permittivität | - | ozpermr_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| RTOEL | 0x4407 | STAT_OELSENSOR_TEMPERATUR_ROH_WERT | Sensorrohwert Öltemperatur | - | oztempr | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| ITSOE | 0x4408 | STAT_OELSENSOR_TEMPERATUR_WERT | Öltemperatur ungefiltert | Grad C | oztemp_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| INIOE | 0x4409 | STAT_OELSENSOR_NIVEAU_WERT | Ölniveau ungefiltert in [mm] | - | ozniv | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| IQOEL | 0x440A | STAT_OELSENSOR_QUALITAET_WERT | Permitivität für den Tester | - | ozpermakt | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| STAT_0x440B_WERT | 0x440B | STAT_0x440B_WERT | CodingDataSet-ÖL-Länderfaktor1- EEPROM | - | ozlf1c_eep | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| STAT_0x440C_WERT | 0x440C | STAT_0x440C_WERT | CodingDataSet-ÖL-Länderfaktor2- EEPROM | - | ozlf2c_eep | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| STAT_0x440D_WERT | 0x440D | STAT_0x440D_WERT | Länderfaktor 1 | - | ozlf1t | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| STAT_0x440E_WERT | 0x440E | STAT_0x440E_WERT | Länderfaktor 2 | - | ozlf2t | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| STAT_0x440F_WERT | 0x440F | STAT_0x440F_WERT | Kurzzeit-Ölniveau-Mittelwert für den DIS-Tester | - | oznivkrzt | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| STAT_0x4411_WERT | 0x4411 | STAT_0x4411_WERT | Restweg aus Kraftstoffverbrauch abgeleitet | - | ozrwkvb | - | signed integer | - | 10,0 | 1 | 0,0 |
| STAT_0x4412_WERT | 0x4412 | STAT_0x4412_WERT | Öllaufzeit | month | ozoelzeit | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x4418_WERT | 0x4418 | STAT_0x4418_WERT | Status Ölzustandssensor | - | ozstatus | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| IAVEX | 0x4501 | STAT_VVT_EXCENTER_ADAPTION_WERT | VVT Excenterwellenadaptionswert | mm | hubadmrofs_w | - | signed integer | - | 0,0010000000474974513 | 1 | 0,0 |
| SSPEI | 0x4505 | STAT_NW_EINLASSSPREIZUNG_SOLL_WERT | Sollwinkel vom BMW Layer (Einlass-VANOS) | Grad KW | wnwsaeb_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| STAT_0x4506_WERT | 0x4506 | STAT_0x4506_WERT | Nockenwellenposition Einlass | Grad KW | wnwkwe_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x4507_WERT | 0x4507 | STAT_0x4507_WERT | Nockenwellenposition Auslass | Grad KW | wnwkwa_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| ISNWE | 0x4508 | STAT_NW_EINLASSSPREIZUNG_WERT | Winkel Einlassventil oeffnet bezogen auf LWOT | Grad KW | wnwe_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| ISNWA | 0x4509 | STAT_NW_AUSLASSSPREIZUNG_WERT | Winkel Auslassventil schließt bezogen auf LWOT | Grad KW | wnwa_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| STAT_0x450C_WERT | 0x450C | STAT_0x450C_WERT | Adaption Kurbel/Einlassnockenwelle erfolgt | 0/1 | B_phade | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x450D_WERT | 0x450D | STAT_0x450D_WERT | Adaption Kurbel/Auslassnockenwelle erfolgt | 0/1 | B_phada | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x450E_WERT | 0x450E | STAT_0x450E_WERT | [0] Nullpunktverschiebung in Grad KW für die Winkelversatz Diag, bedingt d. Toleranzen d. Einbaulage | deg CrS | EpmCaS_phiDiffAvrgLim | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x4510_WERT | 0x4510 | STAT_0x4510_WERT | Bedingung VVT-Lagereglerüberwachung hat bleibende Regelabweichung erkannt | 0/1 | B_dvvtregelabweichung | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4511_WERT | 0x4511 | STAT_0x4511_WERT | Bedingung VVT-Lageregler schwingt | 0/1 | B_dvvtschwingung | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4512_WERT | 0x4512 | STAT_0x4512_WERT | Bedingung: VVT Motor Überlast Warnschwelle | 0/1 | B_vvttempovl_wrn | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4513_WERT | 0x4513 | STAT_0x4513_WERT | Bedingung VVT-Überlastung (klemmender Steller) | 0/1 | B_vvttempovl | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4514_WERT | 0x4514 | STAT_0x4514_WERT | Bedingung VVT-Adaption möglich | 0/1 | B_enadpvvt | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4515_WERT | 0x4515 | STAT_0x4515_WERT | Anforderung VVT-Anschlaglernen (intern) | - | vvtlrnaf | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4516_WERT | 0x4516 | STAT_0x4516_WERT | Status VVT-Anschlaglernen (intern) | - | vvtlrnst | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4517_WERT | 0x4517 | STAT_0x4517_WERT | [0] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 0 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x4518_WERT | 0x4518 | STAT_0x4518_WERT | [1] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 1 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x4519_WERT | 0x4519 | STAT_0x4519_WERT | [2] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 2 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x451A_WERT | 0x451A | STAT_0x451A_WERT | [3] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 3 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x451B_WERT | 0x451B | STAT_0x451B_WERT | [4] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 4 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x451C_WERT | 0x451C | STAT_0x451C_WERT | [5] Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle Wert 5 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x451D_WERT | 0x451D | STAT_0x451D_WERT | Gesamtzeit VVT-Performancetest | - | vvtdtperf_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x451E_WERT | 0x451E | STAT_0x451E_WERT | Stromsumme VVT-Performancetest | A | ivvtsumperf_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| IWDKL | 0x4600 | STAT_DROSSELKLAPPENWINKEL_WERT | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | wdkba_w | - | signed integer | - | 0,0244140625 | 1 | 0,0 |
| SWDKL | 0x4601 | STAT_DROSSELKLAPPENWINKEL_SOLL_WERT | Sollwert Drosselklappenwinkel, bezogen auf (unteren) Anschlag | % | wdks_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| SUGEB | 0x4602 | STAT_GENERATOR_SPANNUNG_BSD_SOLL_WERT | phys. Wert Generatorsollspannung (Volt) für Komponententreiber Generator | V | ugen | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| ITGEE | 0x4603 | STAT_GENERATOR_ELEKTRONIKTEMPERATUR_WERT | Chiptemperatur Generator 1 | Grad C | tchip | - | unsigned char | - | 1,0 | 1 | -40,0 |
| IIGEN | 0x4604 | STAT_GENERATOR_STROM_WERT | Generatorstrom | - | st_i_gen | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGENE | 0x4605 | STAT_GENERATOR_CHIPVERSION_WERT | Chipversion Generator 2 | - | bsdgencv | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGENR | 0x4606 | STAT_GENERATOR_REGLERVERSION_WERT | Reglerversion on Generator 1 | - | bsdgenregv | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGENH | 0x4607 | STAT_GENERATOR_HERSTELLERCODE_WERT | Kennung Generator Hersteller | - | genmanufak | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGTYP | 0x4608 | STAT_GENERATOR_TYP_WERT | Kennung Generatortyp | - | gentypkenn | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IUBAT | 0x460A | STAT_UBATT_WERT | momentane Batteriespannung | V | ubt | - | unsigned integer | - | 0,014999999664723873 | 1 | 0,0 |
| IUIBS | 0x460B | STAT_UBATT_IBS_WERT | aktuelle Batteriespannung | V | ubatt_w | - | unsigned integer | - | 2,500000118743628E-4 | 1 | 6,0 |
| IUADW | 0x460C | STAT_UBATT_AD_WANDLER_WERT | Batteriespannung; vom AD-Wandler erfaßter Wert  | V | wub_w | - | unsigned integer | - | 0,02355000004172325 | 1 | 0,0 |
| STAT_0x460D_WERT | 0x460D | STAT_0x460D_WERT | Korrekturwert Abschaltung | % | abschkor_w | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 |
| STAT_0x460E_WERT | 0x460E | STAT_0x460E_WERT | Abstand zur Startfähigkeit | % | dsoc_w | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 |
| ILBAT | 0x460F | STAT_BATTERIELAST_WERT | DF-Monitor für Batterie-Ladezustand in % | % | dfmonitor | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STELU | 0x4611 | STAT_E_LUEFTER_PWM_SOLL_WERT | Tastverhältnis E-Lüfter | % | taml | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x4612_WERT | 0x4612 | STAT_0x4612_WERT | Erregerstrom Generator 1 | A | ierr | - | unsigned char | - | 0,125 | 1 | 0,0 |
| STAT_0x4613_WERT | 0x4613 | STAT_0x4613_WERT | vom Generator empfangene Generatorsollspannung (Kopie gesendeter Wert) | V | ufgen | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| STAT_0x4614_WERT | 0x4614 | STAT_0x4614_WERT | Auslastungsgrad Generator 1 | % | dfsiggen | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x4615_WERT | 0x4615 | STAT_0x4615_WERT | Kopie begrenzter Erregerstrom Generator 1 | A | ierrfgrenz | - | unsigned char | - | 0,125 | 1 | 0,0 |
| STAT_0x4616_WERT | 0x4616 | STAT_0x4616_WERT | vom Generator empfangene Load response Zeit (Kopie gesendeter Wert) | s | tlrfgen | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x4617_WERT | 0x4617 | STAT_0x4617_WERT | gefiltertes Generatormoment absolut | % | mdgenvf_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x4618_WERT | 0x4618 | STAT_0x4618_WERT | Drehzahlschwelle für LR-Funktion Generator 1 aktiv | 0/1 | B_lrfoff | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4619_WERT | 0x4619 | STAT_0x4619_WERT | Bedingung BSD Protokollinhalt für BSD2 Regler | 0/1 | B_bsdprot2 | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x461A_WERT | 0x461A | STAT_0x461A_WERT | Nominalspannung Regler Generator 1 | V | uregnom | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| ISBV1 | 0x4700 | STAT_SONDENBEREITSCHAFT_VORKAT_BANK1 | Bedingung Sonde betriebsbereit vor Kat | 0/1 | B_sbbvk | - | unsigned char | - | 1 | 1 | 0 |
| IUSO1 | 0x4702 | STAT_SONDENSPANNUNG_VORKAT_BANK1_MIT_OFFSET_WERT | Offset korrigierte Sondenspannung vor Kat einer Breitbandlambdasonde | V | ua10mo_w | - | unsigned integer | - | 4,8828125E-4 | 1 | 0,0 |
| SINT1 | 0x4704 | STAT_LAMBDA_BANK1_SOLL_WERT | Lambdasoll Begrenzung (word) | - | lamsbg_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| ISKUB | 0x4800 | STAT_KUPPLUNGSSCHALTER_BETAETIGT_WERT | Bedingung Kupplungspedal betätigt | 0/1 | B_kuppl | - | unsigned char | - | 1 | 1 | 0 |
| ISKUV | 0x4801 | STAT_KUPPLUNGSSCHALTER_VORHANDEN_WERT | Schalter Kupplung | 0/1 | S_kupp | - | unsigned char | - | 1 | 1 | 0 |
| ISSPO | 0x4802 | STAT_SPORTTASTER_BETAETIGT_WERT | Bedingung umschalten auf KFPEDS | 0/1 | B_pedsport | - | unsigned char | - | 1 | 1 | 0 |
| ISKLI | 0x4803 | STAT_KLIMA_EIN | Bedingung für Kompressoreinschalten | 0/1 | B_koe | - | unsigned char | - | 1 | 1 | 0 |
| ISSRC | 0x4805 | STAT_STARTRELAIS_UEBER_CAN_WERT | Schalter Klemme 50 von CAN | 0/1 | S_ckl50 | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4806_WERT | 0x4806 | STAT_0x4806_WERT | Steuergerätetemperatur | Grad C | tsg | - | unsigned char | - | 0,75 | 1 | -48,0 |
| INMOT | 0x4807 | STAT_MOTORDREHZAHL_WERT | Motordrehzahl | 1/min | nmot_w | - | unsigned integer | - | 0,25 | 1 | 0,0 |
| SNLLD | 0x4808 | STAT_LEERLAUFDREHZAHL_SOLL_WERT | Leerlaufsolldrehzahl | 1/min | nsol_w | - | unsigned integer | - | 0,25 | 1 | 0,0 |
| ISLLA | 0x4809 | STAT_LEERLAUF_AKTIV | Bedingung Leerlaufregelung | 0/1 | B_llr | - | unsigned char | - | 1 | 1 | 0 |
| ISKME | 0x480A | STAT_KILOMETERSTAND_WERT | Wegstrecke_km auf 1km genau | - | kmstand_l | - | unsigned long | - | 1,0 | 1 | 0,0 |
| IFPWG | 0x480B | STAT_FAHRERWUNSCH_PEDAL_WERT | normierter Fahrpedalwinkel | %PED | wped_w | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| STAT_0x4880_WERT | 0x4880 | STAT_0x4880_WERT | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Leerlauf bez. auf Schwellwert | % | etkhlmx | - | unsigned char | - | 0,78125 | 1 | 0,0 |
| STAT_0x4881_WERT | 0x4881 | STAT_0x4881_WERT | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Teillast bez. auf Schwellwert | % | etkhtmx | - | unsigned char | - | 0,78125 | 1 | 0,0 |
| STAT_0x4890_WERT | 0x4890 | STAT_0x4890_WERT | Tprot-Status auslesen | 0/1 | B_demsi | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x5800_WERT | 0x5800 | STAT_0x5800_WERT | Zeitzähler ab Startende (16bit) | s | tnse_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x5801_WERT | 0x5801 | STAT_0x5801_WERT | Umgebungsdruck | hPa | pu | - | unsigned char | - | 5,0 | 1 | 0,0 |
| ICLR1 | 0x5802 | STAT_LAMBDAREGELUNG_ZUSTAND_BANK1_WERT | CARB FREEZE FRAME Byte, Bank 1, für LR | - | flglrs | - | unsigned char | - | 1,0 | 1 | 0,0 |
| SLAST | 0x5804 | STAT_LASTWERT_BERECHNET_WERT | relative Luftmasse (calc. load value) nach SAE J1979 | % | rml | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x5805_WERT | 0x5805 | STAT_0x5805_WERT | Motortemperatur, linearisiert und umgerechnet | Grad C | tmotlin | - | unsigned char | - | 0,75 | 1 | -48,0 |
| ILIN1 | 0x5806 | STAT_LAMBDA_INTEGRATOR_GRUPPE1_WERT | Lambda-Regler-Ausgang (Word) | - | fr_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| ILAM1 | 0x5807 | STAT_LAMBDA_ADAPTION_MULTIPLIKATIV_GRUPPE1_WERT | Faktor aus Lambdaregelungsadaption für Bank 1 | - | frann_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| IPSA2 | 0x580B | STAT_SAUGROHRDRUCK_2_WERT | Saugrohr-Absolutdruck (Word) | hPa | ps_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| INAUF | 0x580C | STAT_N_AUFLOESUNG_WERT | Motordrehzahl | 1/min | nmot | - | unsigned char | - | 40,0 | 1 | 0,0 |
| IVKM2 | 0x580D | STAT_GESCHWINDIGKEIT_2_WERT | Fahrzeuggeschwindigkeit | km/h | vfzg | - | unsigned char | - | 1,25 | 1 | 0,0 |
| IZZY1 | 0x580E | STAT_ZUENDZEITPUNKT_ZYL1_WERT | Zündwinkel Zylinder 1 | Grad KW | zwzyl1 | - | signed char | - | 0,75 | 1 | 0,0 |
| ITANL | 0x580F | STAT_ANSAUGLUFTTEMPERATUR_LAW_WERT | Ansaugluft-Temperatur | Grad C | tans | - | unsigned char | - | 0,75 | 1 | -48,0 |
| ILMGS | 0x5810 | STAT_LUFTMASSE_GRAMM_PRO_SEKUNDE_WERT | relative Luftmasse (calc. load value) nach SAE J1979 | % | rml | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x5812_WERT | 0x5812 | STAT_0x5812_WERT | Massenstrom HFM 16-Bit Größe | kg/h | mshfm_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| ILREL | 0x5813 | STAT_LASTWERT_RELATIV_WERT | relative Luftfüllung | % | rl | - | unsigned char | - | 0,75 | 1 | 0,0 |
| STAT_0x5814_WERT | 0x5814 | STAT_0x5814_WERT | Normierter Fahrpedalwinkel | %PED | wped | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| IUK87 | 0x5815 | STAT_KL87_SPANNUNG_WERT | Batteriespannung | V | ub | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| STAT_0x5816_WERT | 0x5816 | STAT_0x5816_WERT | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor | - | lamsons_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| STAT_0x5817_WERT | 0x5817 | STAT_0x5817_WERT | Umgebungstemperatur | Grad C | tumg | - | unsigned char | - | 0,75 | 1 | -48,0 |
| ILMMG | 0x5818 | STAT_LUFTMASSE_PRO_HUB_WERT | Luftmassenfluß | kg/h | ml | - | unsigned char | - | 4,0 | 1 | 0,0 |
| STAT_0x5819_WERT | 0x5819 | STAT_0x5819_WERT | Motordrehzahl [1/min] | rpm | Epm_nEng | - | signed integer | - | 0,5 | 1 | 0,0 |
| STAT_0x581A_WERT | 0x581A | STAT_0x581A_WERT | Winkel Einlassventil oeffnet bezogen auf LWOT | Grad KW | wnwe_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| STAT_0x581B_WERT | 0x581B | STAT_0x581B_WERT | Sollwinkel Nockenwelle Einlass öffnet | Grad KW | wnwse_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| STAT_0x581C_WERT | 0x581C | STAT_0x581C_WERT | Winkel Auslassventil schließt bezogen auf LWOT | Grad KW | wnwa_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| STAT_0x581D_WERT | 0x581D | STAT_0x581D_WERT | Sollwinkel Nockenwelle Auslass schließt | Grad KW | wnwsa_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| STAT_0x581E_WERT | 0x581E | STAT_0x581E_WERT | Ansauglufttemperatur, linearisiert und umgerechnet | Grad C | tanslin | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x581F_WERT | 0x581F | STAT_0x581F_WERT | Motortemperatur, linearisiert und umgerechnet | Grad C | tmotlin | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x5820_WERT | 0x5820 | STAT_0x5820_WERT | Status Klemme 15 | - | B_kl15_byte | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5821_WERT | 0x5821 | STAT_0x5821_WERT | Steuergerätetemperatur | Grad C | tsg | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x5822_WERT | 0x5822 | STAT_0x5822_WERT | Öltemperatur | Grad C | toel | - | unsigned char | - | 1,0 | 1 | -60,0 |
| IZMOS | 0x5823 | STAT_ZEIT_MOTOR_STEHT_WERT | Abstellzeit | s | tabst_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5825_WERT | 0x5825 | STAT_0x5825_WERT | Spannung BCU LIN | V | BcuEcu_u | - | signed integer | - | 0,009999999776482582 | 1 | 0,0 |
| IDKS1 | 0x5826 | STAT_DROSSELKLAPPE_SENSOR1_WERT | Drosselklappenwinkel aus Poti 1 | %DK | wdk1 | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| STAT_0x5827_WERT | 0x5827 | STAT_0x5827_WERT | Tastverhältnis für Lambdasondenheizung | % | tahrlsu_w | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| STAT_0x5829_WERT | 0x5829 | STAT_0x5829_WERT | normierte Heizleistung der Lambdasonde hinter Kat | - | phlsnh | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| IDRCA | 0x582B | STAT_DREHMOMENTEINGRIFF_CAN_WERT | Drehmomentaufnahme des Wandlers über CAN | % | mdwancan_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x582C_WERT | 0x582C | STAT_0x582C_WERT | Lambdasondenistwert, korrigiert um Zusatzamplitude | - | lamzak_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| STAT_0x582D_WERT | 0x582D | STAT_0x582D_WERT | Korrekturwert der LSU-Spannung vor Kat | V | kusvk_w | - | signed integer | - | 4,8828125E-4 | 1 | 0,0 |
| STAT_0x582F_WERT | 0x582F | STAT_0x582F_WERT | Abgastemperatur nach Katalysator aus Modell | Grad C | tkatm | - | unsigned char | - | 5,0 | 1 | -50,0 |
| STAT_0x5830_WERT | 0x5830 | STAT_0x5830_WERT | Dynamikwert der LSU | - | dynlsu_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| IMOST | 0x5832 | STAT_MOTOR_STATUS_WERT | Zustand Motor-Koordinator | - | CoEng_st | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5834_WERT | 0x5834 | STAT_0x5834_WERT | Umgebungsdruck von Sensor | hPa | pur_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| STAT_0x5835_WERT | 0x5835 | STAT_0x5835_WERT | Kennung Generator Hersteller | - | genmanufak | - | unsigned char | - | 1,0 | 1 | 0,0 |
| INGRD | 0x5836 | STAT_DREHZAHLGRADIENT_WERT | gefilterter Drehzahlgradient | 1/min/s | ngfil | - | signed char | - | 100,0 | 1 | 0,0 |
| STAT_0x5837_WERT | 0x5837 | STAT_0x5837_WERT | Solldruck Hochdrucksystem | MPa | prsoll_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| STAT_0x5838_WERT | 0x5838 | STAT_0x5838_WERT | Relatives Moment für Aussetzererkennung | % | midmd | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| ISDKN | 0x5839 | STAT_DROSSELKLAPPE_NOTLAUF_WERT | Bedingung Sicherheitskraftstoffabschaltung (SKA) | 0/1 | B_dkpu | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x583A_WERT | 0x583A | STAT_0x583A_WERT | Ansaugluft-Temperatur bei Start | Grad C | tansst | - | unsigned char | - | 0,75 | 1 | -48,0 |
| IKTFS | 0x583B | STAT_KRAFTSTOFFTANK_FUELLSTAND_WERT | Fuellstand Kraftstofftank | L | fstt | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x583C_WERT | 0x583C | STAT_0x583C_WERT | Batteriespannung; vom AD-Wandler erfasster Wert | V | wub | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| STAT_0x583D_WERT | 0x583D | STAT_0x583D_WERT | Betriebsstundenzaehler | min | top_w | - | unsigned integer | - | 6,0 | 1 | 0,0 |
| STAT_0x583E_WERT | 0x583E | STAT_0x583E_WERT | Dauer-RAM: Sollwert DK-Winkel in NLP-Stellung, bez. auf UMA | %DK | wdknlpr_w | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| STAT_0x583F_WERT | 0x583F | STAT_0x583F_WERT | Sollwert DK-Winkel, bezogen auf unteren Anschlag | %DK | wdks | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| STAT_0x5840_WERT | 0x5840 | STAT_0x5840_WERT | DK-Winkel der Notluftposition | %DK | wdknlp_w | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| RTSGR | 0x5841 | STAT_STEUERGERAETE_INNENTEMPERATUR_ROH_WERT | Wert Temperatur Steuergerät | V | wtsg | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| STAT_0x5842_WERT | 0x5842 | STAT_0x5842_WERT | Kennung Generatortyp | - | gentypkenn | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5844_WERT | 0x5844 | STAT_0x5844_WERT | Chiptemperatur Generator 1 | Grad C | tchip | - | unsigned char | - | 1,0 | 1 | -40,0 |
| STAT_0x5845_WERT | 0x5845 | STAT_0x5845_WERT | Sondenspannung vor Kat einer Breitbandlambdasonde (ADC-Wert) | V | uulsuv_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x5846_WERT | 0x5846 | STAT_0x5846_WERT | Spannung PWG-Poti 1 (Word) | V | upwg1_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x5847_WERT | 0x5847 | STAT_0x5847_WERT | Spannung PWG-Poti 2 (Word) | V | upwg2_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x5849_WERT | 0x5849 | STAT_0x5849_WERT | ADC-Spannung Lambdasonde hinter Katalysator (Word) | V | ushk_w | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| STAT_0x584C_WERT | 0x584C | STAT_0x584C_WERT | Spannung DK-Poti 2 | V | udkp2_w | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| SQTEK | 0x584D | STAT_TANKENTLUEFTUNG_DURCHFLUSS_SOLL_WERT | Massenstrom Tankentlüftung in das Saugrohr | kg/h | mste_w | - | unsigned integer | - | 3,906250058207661E-4 | 1 | 0,0 |
| STAT_0x584E_WERT | 0x584E | STAT_0x584E_WERT | Spannung DK-Poti 1 | V | udkp1_w | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| STAT_0x484F_WERT | 0x584F | STAT_0x484F_WERT | Erkennung Bordnetzinstabilität | - | statbnserr | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5850_WERT | 0x5850 | STAT_0x5850_WERT | Signalspannung des Kühlmitteltemperatursensors | V | utcw_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x5851_WERT | 0x5851 | STAT_0x5851_WERT | Spannungswert des Ansauglufttemperatursensors tfa2 (SY_TFAKON &gt; 0) | V | wtfa2_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x5852_WERT | 0x5852 | STAT_0x5852_WERT | Batteriestrom von IBS | A | iibsl_w | - | unsigned integer | - | 0,019999999552965164 | 1 | -200,0 |
| STAT_0x5853_WERT | 0x5853 | STAT_0x5853_WERT | Batt Spannung von IBS | V | uibsl_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| STAT_0x5854_WERT | 0x5854 | STAT_0x5854_WERT | BattTemp von IBS | Grad C | tibsl | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x5855_WERT | 0x5855 | STAT_0x5855_WERT | schneller Mittelwert des Lambdaregelfaktors (Word) | - | frm_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| STAT_0x5857_WERT | 0x5857 | STAT_0x5857_WERT | Erregerstrom Generator 1 | A | ierr | - | unsigned char | - | 0,125 | 1 | 0,0 |
| STAT_0x5858_WERT | 0x5858 | STAT_0x5858_WERT | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | wdkba | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| STAT_0x5859_WERT | 0x5859 | STAT_0x5859_WERT | Pumpenstrom Referenzleck | mA | iptrefr_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| STAT_0x585A_WERT | 0x585A | STAT_0x585A_WERT | min. Pumpenstrom bei Grobleckmessung | mA | iptglmn_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| STAT_0x585B_WERT | 0x585B | STAT_0x585B_WERT | Pumpenstrom am Ende der Feinstleckmessung | mA | iptkl_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| IRLN1 | 0x585C | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT1_OBERES_BYTE_WERT | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | rinh_w | - | unsigned char | - | 512,0 | 1 | 0,0 |
| IRUN1 | 0x585E | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT1_UNTERES_BYTE_WERT | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | rinh_w | - | unsigned char | - | 2,0 | 1 | 0,0 |
| IRLV1 | 0x5860 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_WERT | Innenwiderstand der Nernstzelle der LSU | Ohm | rinlsu_w | - | unsigned char | - | 10,0 | 1 | 0,0 |
| STAT_0x5862_WERT | 0x5862 | STAT_0x5862_WERT | Sollwert Öldruck | kPa | poels_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| IRUV1 | 0x5863 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_UNTERES_BYTE_WERT | Innenwiderstand der Nernstzelle der LSU | Ohm | rinlsu_w | - | unsigned char | - | 0,0390625 | 1 | 0,0 |
| STAT_0x5865_WERT | 0x5865 | STAT_0x5865_WERT | Langzeit-Ölniveau-Mittelwert für den DIS-Tester | - | oznivlangt | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| STAT_0x5866_WERT | 0x5866 | STAT_0x5866_WERT | Relativer Füllstand des Motoröls | - | oelstandr | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5867_WERT | 0x5867 | STAT_0x5867_WERT | Fahrstrecke des Fahrzeugs als Information über CAN | km | kmstand | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| ISSR1 | 0x5868 | STAT_STANDVERBRAUCHER_REGISTRIERT_TEIL1_WERT | Status Standverbraucher registriert Teil 1 | - | statsvreg1 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ISSR2 | 0x5869 | STAT_STANDVERBRAUCHER_REGISTRIERT_TEIL2_WERT | Status Standverbraucher registriert Teil 2 | - | statsvreg2 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x586A_WERT | 0x586A | STAT_0x586A_WERT | aktuelle Batteriespannung | V | ubatt_w | - | unsigned integer | - | 2,500000118743628E-4 | 1 | 6,0 |
| IZR82 | 0x586B | STAT_ZEIT_MIT_RUHESTROM_80_200_WERT | Zeit, indem der Ruhestrom bei 80..200mA liegt | min | t2hstshort | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| IZR21 | 0x586C | STAT_ZEIT_MIT_RUHESTROM_200_1000_WERT | Zeit, indem der Ruhestrom bei 200..1000mA liegt | min | t3hstshort | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| IZRG1 | 0x586E | STAT_ZEIT_MIT_RUHESTROM_GROESER_1000_WERT | Zeit, indem der Ruhestrom größer als 1000mA liegt | min | t4hstshort | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| STAT_0x586F_WERT | 0x586F | STAT_0x586F_WERT | Öldruck | hPa | poel_w | - | signed integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5870_WERT | 0x5870 | STAT_0x5870_WERT | Spannung Umgebungsdrucksensor (word 10-Bit von ADC) | V | udsu_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x5871_WERT | 0x5871 | STAT_0x5871_WERT | Zähler Prüfzustand für VVT Endstufenprüfung | - | dvestanznmotctr | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5872_WERT | 0x5872 | STAT_0x5872_WERT | Reglerversion on Generator 1 | - | bsdgenregv | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5874_WERT | 0x5874 | STAT_0x5874_WERT | ADC-Spannung Pumpenstrom Tankdiagnose | V | urptes_w | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| STAT_0x5875_WERT | 0x5875 | STAT_0x5875_WERT | Indiziertes Soll-Motormoment MSR | % | mimsr_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5876_WERT | 0x5876 | STAT_0x5876_WERT | Schnittstelle für Scan Tool Mode $01/$02 Raildruck Rohwert PID$23 | MPa | prrohr_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| ILRR1 | 0x5878 | STAT_LAMBDAVERSCHIEBUNG_RUECKFUEHRREGLER1_WERT | I-Anteil der stetigen LRSHK Variante kontinuierlich | - | dlahi_w | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| STAT_0x587B_WERT | 0x587B | STAT_0x587B_WERT | Anzahl erkannter VVT Lageregelungsfehlerwarnungen irreversibel | - | vvt_highcurrent | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x587E_WERT | 0x587E | STAT_0x587E_WERT | Anzahl erkannter VVT Lageregelungsfehlerwarnungen reversibel | - | vvt_highcurrent_rev | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| IELTV | 0x587F | STAT_E_LUEFTER_TASTVERHAELTNIS_WERT | Tastverhältnis E-Lüfter | % | taml | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x5880_WERT | 0x5880 | STAT_0x5880_WERT | Tastverhältnis GLF System | % | glfpwm | - | unsigned char | - | 1,0 | 1 | 0,0 |
| SBEGA | 0x5881 | STAT_BERECHNETER_GANG_WERT | Ist-Gang | - | gangi | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ITMOS | 0x5882 | STAT_MOTORTEMPERATUR_BEIM_START_WERT | Motorstarttemperatur | Grad C | tmst | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x5883_WERT | 0x5883 | STAT_0x5883_WERT | [0] Spannung Klopfwerte Zylinder 1 | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| STAT_0x5884_WERT | 0x5884 | STAT_0x5884_WERT | Kopie begrenzter Erregerstrom Generator 1 | A | ierrfgrenz | - | unsigned char | - | 0,125 | 1 | 0,0 |
| STAT_0x5885_WERT | 0x5885 | STAT_0x5885_WERT | [2] Referenzpegel Klopfregelung, 16bit | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| STAT_0x5886_WERT | 0x5886 | STAT_0x5886_WERT | [3] Referenzpegel Klopfregelung, 16bit | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| STAT_0x5887_WERT | 0x5887 | STAT_0x5887_WERT | Auslastungsgrad Generator 1 | % | dfsiggen | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x5888_WERT | 0x5888 | STAT_0x5888_WERT | [5] Spannung Klopfwerte Zylinder 4 | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| ILAG1 | 0x5889 | STAT_LAMBDA_ISTWERT_GRUPPE1_WERT | Lambda-Istwert | - | lamsoni_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| IZSSE | 0x588B | STAT_ZEIT_SEIT_STARTENDE_WERT | Zeit nach Startende | s | tnst_w | - | unsigned integer | - | 0,009999999776482582 | 1 | 0,0 |
| ITKV1 | 0x588C | STAT_LAMBDASONDE_KERAMIKTEMPERATUR_VORKAT1_WERT | Keramiktemperatur der LSU | Grad C | tkerlsu_w | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| IZDML | 0x588D | STAT_ZEIT_DMTL_LECKMESSUNG_WERT | aktuelle Zeit Leckmessung | s | tdmlka_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| IIDMP | 0x588E | STAT_PUMPENSTROM_BEI_DMTL_PUMPENPRUEFUNG_WERT | Pumpenstrom Tankdiagnose | mA | iptes_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| IMOKU | 0x5891 | STAT_MOMENTANFORDERUNG_KUPPLUNG_WERT | Kupplungsmotormoment Istwert | Nm | mkist_w | - | signed integer | - | 0,5 | 1 | 0,0 |
| IDMGW | 0x5893 | STAT_DREHMOMENTABFALL_BEIM_GANGWECHSEL_WERT | Indiziertes Soll-Motormoment GS für schnellen Eingriff | % | migs_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5894_WERT | 0x5894 | STAT_0x5894_WERT | [4] Spannung Klopfwerte Zylinder 2 | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| STAT_0x5895_WERT | 0x5895 | STAT_0x5895_WERT | [1] Spannung Klopfwerte Zylinder 5 | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| STAT_0x5896_WERT | 0x5896 | STAT_0x5896_WERT | Abgastemperatur hinter Hauptkat aus Modell | Grad C | tanhkm_w | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| SUGEN | 0x5898 | STAT_GENERATOR_SPANNUNG_SOLL_WERT | phys. Wert Generatorsollspannung (Volt) für Komponententreiber Generator | V | ugen | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| STAT_0x5899_WERT | 0x5899 | STAT_0x5899_WERT | Bedingung Anforderung Motorrelais einschalten | - | B_amtr_byte | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x589B_WERT | 0x589B | STAT_0x589B_WERT | Bedingung unzulässig hoher Motorstrom bei Kurzschluss erkannt | - | B_ivvtkse_byte | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x589C_WERT | 0x589C | STAT_0x589C_WERT | Bedingung Freigabe VVT-Endstufe | - | B_vvten_byte | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x589D_WERT | 0x589D | STAT_0x589D_WERT | Anzahl erkannter VVT Lageregelungsfehler | - | vvt_deviation | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x589E_WERT | 0x589E | STAT_0x589E_WERT | Sollwert Exzenterwinkel VVT | Grad | exwinks_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x589F_WERT | 0x589F | STAT_0x589F_WERT | Batterietemperatur | Grad C | tbatt | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x58A0_WERT | 0x58A0 | STAT_0x58A0_WERT | Entladung während Ruhestromverletzung | Ah | qiruhe2_w | - | unsigned integer | - | 0,018204445019364357 | 1 | 0,0 |
| STAT_0x58A1_WERT | 0x58A1 | STAT_0x58A1_WERT | Umweltbedingung Kilometerstand für Fehlerspeichereintrag | km | kmstfsp_w | - | unsigned integer | - | 8,0 | 1 | 0,0 |
| STAT_0x58A2_WERT | 0x58A2 | STAT_0x58A2_WERT | Istwert Exzenterwinkel VVT | Grad | exwnki_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58A3_WERT | 0x58A3 | STAT_0x58A3_WERT | rel. Exzenterwinkel am oberen mech. Anschlag | Grad | exwnkoar_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58A4_WERT | 0x58A4 | STAT_0x58A4_WERT | Generatorstatus | - | st_gen | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58A5_WERT | 0x58A5 | STAT_0x58A5_WERT | Vom Generator empfangenes Lastsignal | % | dffgen | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x58A6_WERT | 0x58A6 | STAT_0x58A6_WERT | Relativer Exzenterwinkel | Grad | exwnkr_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58A7_WERT | 0x58A7 | STAT_0x58A7_WERT | Abstellzeit aus relativem Minutenzähler bis Motorstart | min | tabsmn_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x58A8_WERT | 0x58A8 | STAT_0x58A8_WERT | rel. Exzenterwinkel am unteren mech. Anschlag | Grad | exwnkuar_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58A9_WERT | 0x58A9 | STAT_0x58A9_WERT | VVT Verstellbereich aus Urlernvorgang | Grad | exwnkvb_ur_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58AA_WERT | 0x58AA | STAT_0x58AA_WERT | Verstellbereich des Exzenterwinkels | Grad | exwnkvb_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58AB_WERT | 0x58AB | STAT_0x58AB_WERT | DLR für DV-E: Summe der PID-Anteile | % | dlrspid_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x58AD_WERT | 0x58AD | STAT_0x58AD_WERT | Sauerstoffspeichervermögen des Katalysators, temperatur- und luftmassenstrombezogen | mg | oscdktt_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58AE_WERT | 0x58AE | STAT_0x58AE_WERT | Peridendauer für Massenstrom aus HFM | us | tpmshfm_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| IKRAN | 0x58AF | STAT_KRAFTSTOFF_ANFORDERUNG_AN_PUMPE_WERT | EKP-Sollvolumenstrom | l | vssekp | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IDKAD | 0x58B0 | STAT_DK_ADAPTIONSSCHRITT_WERT | Zähler für Lerndauer eines Lernsteps | - | lrnstep_c | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IZFZ1 | 0x58B1 | STAT_FUNKENBRENNDAUER_ZYL1_WERT | [0] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 1 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IZFZ5 | 0x58B2 | STAT_FUNKENBRENNDAUER_ZYL5_WERT | [1] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 5 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IZFZ3 | 0x58B3 | STAT_FUNKENBRENNDAUER_ZYL3_WERT | [2] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 3 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IZFZ6 | 0x58B4 | STAT_FUNKENBRENNDAUER_ZYL6_WERT | [3] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 6 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IZFZ2 | 0x58B5 | STAT_FUNKENBRENNDAUER_ZYL2_WERT | [4] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 2 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IZFZ4 | 0x58B6 | STAT_FUNKENBRENNDAUER_ZYL4_WERT | [5] Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 4 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IPBRE | 0x58B7 | STAT_BREMSDRUCK_WERT | aktueller Bremsdruck | - | pbrems | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58B8_WERT | 0x58B8 | STAT_0x58B8_WERT | Motordrehzahl in der Funktionsüberwachung | 1/min | MoF_nEng | - | unsigned char | - | 40,0 | 1 | 0,0 |
| STAT_0x58B9_WERT | 0x58B9 | STAT_0x58B9_WERT | Pedalsollwert (8 Bit) in der Funktionsüberwachung | V | MoF_uAPP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| STAT_0x58BA_WERT | 0x58BA | STAT_0x58BA_WERT | Bank mittel eingespritzte effektive relative Krafftstoffmasse (inkl. Reduzierstufe) | % | rkmeeff_w | - | unsigned integer | - | 0,046875 | 1 | 0,0 |
| STAT_0x58BB_WERT | 0x58BB | STAT_0x58BB_WERT | Strom für VVT-Motor | A | ivvtm_w | - | signed integer | - | 0,006103515625 | 1 | 0,0 |
| STAT_0x58BC_WERT | 0x58BC | STAT_0x58BC_WERT | relative Luftfüllung in der Funktionsüberwachung | % | rl_um | - | unsigned char | - | 0,75 | 1 | 0,0 |
| STAT_0x58BD_WERT | 0x58BD | STAT_0x58BD_WERT | Status Fehler Überlast VVT1 | - | stdvovrld | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58BE_WERT | 0x58BE | STAT_0x58BE_WERT | DV-E-Adaption: Status Prüfbedingungen | - | dveadchst | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58C0_WERT | 0x58C0 | STAT_0x58C0_WERT | VVT-Endstufentemperatur aus Modell | Grad C | tvvtes_w | - | unsigned integer | - | 0,75 | 1 | -48,0 |
| STAT_0x58C8_WERT | 0x58C8 | STAT_0x58C8_WERT | geforderte Drehmomentänderung von der LLR (I-Anteil) | % | dmllri_w | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| STAT_0x58C9_WERT | 0x58C9 | STAT_0x58C9_WERT | Ansteuerungsmodus für den VVT Motor | - | vvtmode | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58CA_WERT | 0x58CA | STAT_0x58CA_WERT | geforderte MD-Änderung von der LLR (PD-Zündungsanteil) | % | dmllrz_w | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| STAT_0x58CB_WERT | 0x58CB | STAT_0x58CB_WERT | Aufsummierte thermische Belastung VVT | - | dvvttempovl | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x58CC_WERT | 0x58CC | STAT_0x58CC_WERT | Tastverhältnis zur Ansteuerung des VVT-Stellmotors | % | tvvvtm_w | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| STAT_0x58CD_WERT | 0x58CD | STAT_0x58CD_WERT | Spannung hinter VVT-Relais | V | umtr | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58CE_WERT | 0x58CE | STAT_0x58CE_WERT | Carrierbyte Schalterstati | - | funst_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| SMOMO | 0x58CF | STAT_MOTORMOMENT_SOLL_WERT | Momentenanforderung vom Getriebe in der Funktionsüberwachung | Nm | MoF_trqClthTra16 | - | signed integer | - | 0,0625 | 1 | 0,0 |
| IMOMO | 0x58D0 | STAT_MOTORMOMENT_IST_WERT | Berechnetes Ist-Moment in der Funktionsüberwachung | % | MoF_rTrqInrAct | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x58D2_WERT | 0x58D2 | STAT_0x58D2_WERT | Status Luftklappensystem High Byte | - | state_glf_sys_hb | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58D3_WERT | 0x58D3 | STAT_0x58D3_WERT | Status Luftklappensystem Low Byte | - | state_glf_sys_lb | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58D4_WERT | 0x58D4 | STAT_0x58D4_WERT | Startbedingung Kraftschluss erfüllt | 0/1 | B_kupp1 | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x58D5_WERT | 0x58D5 | STAT_0x58D5_WERT | physikalischer Temperaturwert, der sich bei Wandlung der elektrischen Sensorspannung wtfa1_w ergibt | Grad C | tfa1lin | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x58D7_WERT | 0x58D7 | STAT_0x58D7_WERT | Spannungswert des Ansauglufttemperatursensors tfa1 | V | wtfa1_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x58D8_WERT | 0x58D8 | STAT_0x58D8_WERT | Differenz-DK-Winkel Sollwert - Istwert (wdkdlr_w - wdkba_w) | %DK | dwdkdlr_w | - | signed integer | - | 0,0244140625 | 1 | 0,0 |
| STAT_0x58D9_WERT | 0x58D9 | STAT_0x58D9_WERT | Schrittzähler DK-Rückstellfeder-Prüfung | - | fprstep_c | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58DA_WERT | 0x58DA | STAT_0x58DA_WERT | koordiniertes Moment für Füllung | % | milsol_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x58DB_WERT | 0x58DB | STAT_0x58DB_WERT | Fehlerzähler Summe, zählt abgasrelevante Aussetzer über alle Zylinder | - | fzabgs_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x58DC_WERT | 0x58DC | STAT_0x58DC_WERT | Intervallzähler für abgasrelevante Aussetzer | - | ivzabg_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x58DD_WERT | 0x58DD | STAT_0x58DD_WERT | Druck vor Drosselklappe Rohwert | hPa | pvdr_w | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| STAT_0x58DE_WERT | 0x58DE | STAT_0x58DE_WERT | Spannung Drucksensor vor Drosselklappe | V | udsvd_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x58E0_WERT | 0x58E0 | STAT_0x58E0_WERT | Abgleich DK-Modell (Faktor) | - | eisydkfkaf | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| STAT_0x58E1_WERT | 0x58E1 | STAT_0x58E1_WERT | Abgleich DK-Modell (Offset) | kg/h | eisydkkoff | - | signed char | - | 8,0 | 1 | 0,0 |
| STAT_0x58E2_WERT | 0x58E2 | STAT_0x58E2_WERT | Abgleich EV-Modell (Faktor) | - | eisyevfkaf | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| STAT_0x58E3_WERT | 0x58E3 | STAT_0x58E3_WERT | Abgleich EV-Modell (Offset) | kg/h | eisyevkoff | - | signed char | - | 8,0 | 1 | 0,0 |
| STAT_0x58E4_WERT | 0x58E4 | STAT_0x58E4_WERT | Ist-Betriebsart | - | opmodi | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58E5_WERT | 0x58E5 | STAT_0x58E5_WERT | Rotorposition VVT-Motor | ° | vvtrotwn_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x58E6_WERT | 0x58E6 | STAT_0x58E6_WERT | Soll-Bestromung VVT-Motor | A | ivvtlrs_w | - | signed integer | - | 0,006103515625 | 1 | 0,0 |
| IUWAP | 0x58E9 | STAT_WASSERPUMPE_SPANNUNG_WERT | empf. Spannung von BSS-Wasserpumpe | V | wmu | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58EA_WERT | 0x58EA | STAT_0x58EA_WERT | empf. Istdrehzahl von BSS-Wasserpumpe | 1/min | wmpdzi | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58EC_WERT | 0x58EC | STAT_0x58EC_WERT | empf. Temperatur von BSS-Wasserpumpe | Grad C | wmt | - | unsigned char | - | 1,0 | 1 | -50,0 |
| STAT_0x58ED_WERT | 0x58ED | STAT_0x58ED_WERT | empf. Strom von BSS-Wasserpumpe | % | wmi | - | unsigned char | - | 0,5 | 1 | 0,0 |
| STAT_0x58EF_WERT | 0x58EF | STAT_0x58EF_WERT | Gefilterter Raildruck-Istwert (Absolutdruck) | MPa | prist_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| STAT_0x58F0_WERT | 0x58F0 | STAT_0x58F0_WERT | ungefilterter Raildruck Istwert (abs.) | MPa | prroh_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| STAT_0x58F2_WERT | 0x58F2 | STAT_0x58F2_WERT | PWM signal for the VCV | % | PWM_VCV | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x58F3_WERT | 0x58F3 | STAT_0x58F3_WERT | Ungefilterter Niederdruck Rohwert | kPa | pistndr_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58F4_WERT | 0x58F4 | STAT_0x58F4_WERT | Spannung Kraftstoffniederdrucksensor im 1 ms Raster | V | upnd1ms_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x58F5_WERT | 0x58F5 | STAT_0x58F5_WERT | Spannung Diagnose-Port VVT-Ansteuerung (3V ADC) | V | uvvtdia3V | - | unsigned char | - | 0,012890624813735485 | 1 | 0,0 |
| STAT_0x58F6_WERT | 0x58F6 | STAT_0x58F6_WERT | Sollspannung des VVT Lagereglers | V | uvvtlrs_w | - | signed integer | - | 7,812500116415322E-4 | 1 | 0,0 |
| STAT_0x58F7_WERT | 0x58F7 | STAT_0x58F7_WERT | Statusbyte Strommessung plausibel | - | vvtipl | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58FA_WERT | 0x58FA | STAT_0x58FA_WERT | gefilterter Faktor Tankentlüftungs-Adaption | - | fteadf | - | signed char | - | 0,5 | 1 | 0,0 |
| STAT_58FC_WERT | 0x58FC | STAT_58FC_WERT | Fertigungs-Werkstatt-,Transportmodus | - | fetrawemod | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5A02_WERT | 0x5A02 | STAT_0x5A02_WERT | ATL-Leckagediagnose läuft | 0/1 | B_atlberlek | - | unsigned char | - | 1 | 1 | 0 |
| IUPW1 | 0x5A04 | STAT_PWG1_SPANNUNG_WERT | Spannung PWG-Poti 1 | V | upwg1_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUPW2 | 0x5A05 | STAT_PWG2_SPANNUNG_WERT | Spannung PWG-Poti 2 | V | upwg2_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUDK1 | 0x5A06 | STAT_DK1_SPANNUNG_WERT | Spannung DK-Poti 1 | V | udkp1_w | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| IUDK2 | 0x5A07 | STAT_DK2_SPANNUNG_WERT | Spannung DK-Poti 2 | V | udkp2_w | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| IUANS | 0x5A08 | STAT_ANSAUGLUFTTEMPERATUR_SPANNUNG_WERT | Spannungswert des Ansauglufttemperatursensors tfa1 | V | wtfa1_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKUM | 0x5A09 | STAT_KUEHLMITTELTEMPERATUR_SPANNUNG_WERT | Signalspannung des Kühlmitteltemperatursensor | V | utcw_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUUMG | 0x5A0B | STAT_UMGEBUNGSDRUCK_SPANNUNG_WERT | Spannung Umgebungsdrucksensor (word 10-Bit von ADC) | V | udsu_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IULMM | 0x5A0C | STAT_LUFTMASSE_WERT | Spannungswert des Ansauglufttemperatursensors tfa2 (SY_TFAKON &gt; 0) | V | wtfa2_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSGI | 0x5A0E | STAT_STEUERGERAETE_INNENTEMPERATUR_SPANNUNG_WERT | Wert Temperatur Steuergerät | V | wtsg | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| IUSV1 | 0x5A11 | STAT_SONDENSPANNUNG_VORKAT_WERT | Spannung Lambdasonde vor Katalysator | V | uulsuv_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSN1 | 0x5A13 | STAT_SONDENSPANNUNG_NACHKAT_WERT | Spannung Lambdasonde hinter Katalysator | V | ushk_w | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| IUDMT | 0x5A17 | STAT_DMTL_SPANNUNG_WERT | Spannung Pumpenstrom Tankdiagnose | V | uptes_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x5A1B_WERT | 0x5A1B | STAT_0x5A1B_WERT | Elektrische Kraftstoffpumpe | 0/1 | B_ekp | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x5A20_WERT | 0x5A20 | STAT_0x5A20_WERT | Peridendauer für Massenstrom aus HFM | us | tpmshfm_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| ITKUA | 0x5A21 | STAT_KUEHLERAUSLASSTEMPERATUR_WERT | Kühlmitteltemperatur (Sensorwert) nach Tiefpassfilterung | Grad C | tmotlinf | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x5A23_WERT | 0x5A23 | STAT_0x5A23_WERT | Sollwert Öldruck | kPa | poels_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x5A24_WERT | 0x5A24 | STAT_DK_WINKEL_SOLL_WERT | Sollwert Drosselklappenwinkel, bezogen auf (unteren) Anschlag | % | wdks_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5A25_WERT | 0x5A25 | STAT_0x5A25_WERT | Öldruck | hPa | poel_w | - | signed integer | - | 1,0 | 1 | 0,0 |
| RFPWG | 0x5A29 | STAT_FAHRERWUNSCH_PEDAL_ROH_WERT | normierter Fahrpedalwinkel | %PED | wped_w | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| STAT_0x5A2B_WERT | 0x5A2B | STAT_0x5A2B_WERT | physikalischer Temperaturwert, ergibt sich bei Wandlung der tiefpassgefilterten Sensorspg. wtfa1f_w | Grad C | tfa1linf | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x5A2D_WERT | 0x5A2D | STAT_0x5A2D_WERT | Saugrohr-Absolutdruck gemessen | hPa | psrg_w | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| STAT_0x5A2E_WERT | 0x5A2E | STAT_0x5A2E_WERT | Ungefilterter Niederdruck Rohwert | kPa | pistndr_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x5A2F_WERT | 0x5A2F | STAT_0x5A2F_WERT | Gefilterter Raildruck-Istwert (Absolutdruck) | MPa | prist_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| ILUZ1 | 0x5A30 | STAT_LAUFUNRUHE_ZYL1_WERT | [0] Laufunruhe Zylinder 1 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ILUZ2 | 0x5A31 | STAT_LAUFUNRUHE_ZYL2_WERT | [4] Laufunruhe Zylinder 2 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ILUZ3 | 0x5A32 | STAT_LAUFUNRUHE_ZYL3_WERT | [2] Laufunruhe Zylinder 3 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ILUZ4 | 0x5A33 | STAT_LAUFUNRUHE_ZYL4_WERT | [5] Laufunruhe Zylinder 4 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ILUZ5 | 0x5A34 | STAT_LAUFUNRUHE_ZYL5_WERT | [1] Laufunruhe Zylinder 5 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ILUZ6 | 0x5A35 | STAT_LAUFUNRUHE_ZYL6_WERT | [3] Laufunruhe Zylinder 6 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ISKLO | 0x5A36 | STAT_STATUS_KLOPFEN_WERT | Bedingung für erkannte Klopfer | 0/1 | B_kl | - | unsigned char | - | 1 | 1 | 0 |
| IUKZ1 | 0x5A37 | STAT_KLOPFWERT_ZYL1_SPANNUNG_WERT | [0] normierter Referenzpegel Klopfregelung Zylinder 1 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKZ2 | 0x5A38 | STAT_KLOPFWERT_ZYL2_SPANNUNG_WERT | [4] normierter Referenzpegel Klopfregelung Zylinder 2 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKZ3 | 0x5A39 | STAT_KLOPFWERT_ZYL3_SPANNUNG_WERT | [2] normierter Referenzpegel Klopfregelung Zylinder 3 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKZ4 | 0x5A3A | STAT_KLOPFWERT_ZYL4_SPANNUNG_WERT | [5] normierter Referenzpegel Klopfregelung Zylinder 4 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKZ5 | 0x5A3B | STAT_KLOPFWERT_ZYL5_SPANNUNG_WERT | [1] normierter Referenzpegel Klopfregelung Zylinder 5 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKZ6 | 0x5A3C | STAT_KLOPFWERT_ZYL6_SPANNUNG_WERT | [3] normierter Referenzpegel Klopfregelung Zylinder 6 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IZWZ1 | 0x5A49 | STAT_ZUENDWINKEL_ZYL1_WERT | [0] Ausgegebener Zündwinkel | Grad KW | zwoutzyl_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| ILASB | 0x5A4B | STAT_BERECHNETE_LAST_WERT | relative Luftmasse (calc. load value) nach SAE J1979 | % | rml | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| ILAB1 | 0x5A50 | STAT_LAMBDA_BANK1_WERT | Lambda-Istwert | - | lamsoni_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| IRNK1 | 0x5A52 | STAT_READINESS_SONDE_NACHKAT_BANK1_WERT | Bedingung Sonde betriebsbereit hinter Kat | 0/1 | B_sbbhk | - | unsigned char | - | 1 | 1 | 0 |
| ISHN1 | 0x5A54 | STAT_SONDENHEIZUNG_NACHKAT_BANK1_WERT | Bedingung Sonde hinter Kat ausreichend beheizt | 0/1 | B_hsha | - | unsigned char | - | 1 | 1 | 0 |
| ISHV1 | 0x5A56 | STAT_SONDENHEIZUNG_VORKAT_BANK1_WERT | Bedingung: Heizerstatus A liegt vor, Sonde ist ausreichend aufgeheizt | 0/1 | B_hstlsua | - | unsigned char | - | 1 | 1 | 0 |
| IAHV1 | 0x5A58 | STAT_SONDENHEIZUNG_PWM_VORKAT_BANK1_WERT | Tastverhältnis für Lambdasondenheizung | % | tahrlsu_w | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| IAHN1 | 0x5A59 | STAT_SONDENHEIZUNG_PWM_NACHKAT_BANK1_WERT | normierte Heizleistung der Lambdasonde hinter Kat | - | phlsnh | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| ISBLS | 0x5A60 | STAT_BREMSLICHTSCHALTER_EIN_WERT | Bedingung Bremslichtschalter betätigt | 0/1 | B_bl | - | unsigned char | - | 1 | 1 | 0 |
| ISBLT | 0x5A61 | STAT_BREMSLICHTTESTSCHALTER_EIN_WERT | Bedingung Bremstestschalter betätigt | 0/1 | B_br | - | unsigned char | - | 1 | 1 | 0 |
| ISAGK | 0x5A65 | STAT_ABGASKLAPPE_EIN_WERT | Bedingung Abgasklappe mit Resonator | 0/1 | B_akr | - | unsigned char | - | 1 | 1 | 0 |
| ISDMP | 0x5A66 | STAT_DMTL_PUMPE_EIN_WERT | Bedingung DMTL-Pumpenmotor an | 0/1 | B_admtpm | - | unsigned char | - | 1 | 1 | 0 |
| ISDMV | 0x5A67 | STAT_DMTL_VENTIL_EIN_WERT | Bedingung DMTL-Magnetventil an | 0/1 | B_admtmv | - | unsigned char | - | 1 | 1 | 0 |
| ISDMH | 0x5A68 | STAT_DMTL_HEIZUNG_EIN_WERT | Bedingung Heizung DMTL Portansteuerung | 0/1 | B_hdmtlp | - | unsigned char | - | 1 | 1 | 0 |
| ISMIL | 0x5A69 | STAT_MIL_EIN_WERT | MIL-Ansteuerung | 0/1 | B_mil | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x5A6A_WERT | 0x5A6A | STAT_0x5A6A_WERT | Lampe FGR Ein | 0/1 | B_fgr | - | unsigned char | - | 1 | 1 | 0 |
| ISCEL | 0x5A6B | STAT_CHECK_ENGINE_LAMPE_EIN_WERT | Bedingung für Ansteuerung EGAS-Fehlerlampe | 0/1 | B_epcl | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x5A6C_WERT | 0x5A6C | STAT_0x5A6C_WERT | Korrekturfaktor für die Kraftstoffmenge | % | kva_korr | - | signed char | - | 0,0010000000474974513 | 1 | 0,0 |
| IAKFT | 0x5A74 | STAT_BEHEIZTER_THERMOSTAT_PWM_WERT | Tastverhältnis Kennfeldthermostat | - | tkwpwm | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| IATEV | 0x5A77 | STAT_TEV_PWM_WERT | ausgegebenes Tastverhältnis für Tankentlüftungsventil (16 Bit) | % | tateout_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IAAGK | 0x5A78 | STAT_ABGASKLAPPE_ANSTEUERUNG_WERT | Bedingung Abgasklappe mit Resonator | 0/1 | B_akr | - | unsigned char | - | 1 | 1 | 0 |
| IAVEP | 0x5A7A | STAT_VANOS_EINLASS_PWM_WERT | Tastverhältnis Einlaßnockenwellenregelung Ansteuerung Endstufe(word) | % | tanwree_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IAVAP | 0x5A7B | STAT_VANOS_AUSLASS_PWM_WERT | Tastverhältnis Auslaßnockenwellenregelung Ansteuerung Endstufe(word) | % | tanwraa_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IINT1 | 0x5A81 | STAT_INTEGRATOR_BANK1_WERT | Lambda-Regler-Ausgang (Word) | - | fr_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| IMUL1 | 0x5A85 | STAT_ADAPTION_MULTIPLIKATIV_BANK1_WERT | multiplikative Gemischkorrektur der Gemischadaption (Word) | - | fra_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| STAT_0x5A91_WERT | 0x5A91 | STAT_0x5A91_WERT | Amplitudenverhältnis laafh/laafv gefiltert | - | avkatf | - | unsigned char | - | 0,00390625 | 1 | 0,0 |
| SANWA | 0x5A94 | STAT_NW_AUSLASS_SOLL_WERT | gespeicherter Nockenwellensollwinkel Auslaß | Grad KW | wnwsswa_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| IANWA | 0x5A95 | STAT_NW_ADAPTION_AUSLASS_WERT | [0] Adaptionswert Nockenwelle Auslass Bank 1 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| IANWE | 0x5A96 | STAT_NW_ADAPTION_EINLASS_WERT | [0] Adaptionswert Nockenwelle Einlass Bank 1 | deg CrS | EpmCaS_phiAdapRefPosI1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x5A97_WERT | 0x5A97 | STAT_0x5A97_WERT | Bedi. Vanos Einlass im Anschlag | 0/1 | B_vseansch | - | unsigned char | - | 1 | 1 | 0 |
| IAKWF | 0x5A99 | STAT_KURBELWELLEN_ADAPTION_BEENDET_WERT | Status der fuel-off Adaption im aktuellen Betriebsbereich | - | fofstat | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5A9D_WERT | 0x5A9D | STAT_0x5A9D_WERT | multiplikative Gemischkorrektur der Gemischadaption | - | frai_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| IDSLS | 0x5AA1 | STAT_SLS_DIAGNOSE_WERT | Zyklusflag: Tankentlüftungsventil Endstufe | - | Z_teve_byte | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IDTEV | 0x5AA2 | STAT_TEV_DIAGNOSE_WERT | Funktionsstatus-Zähler DM-TL für Testerausgabe aus letztem Fahrzyklus | - | stpdmtla | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IDLSS | 0x5AA4 | STAT_LS_DIAGNOSE_WERT | Funktionsstatus LLRNS bei Anforderung Systemcheck | - | llsstat | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5AA9_WERT | 0x5AA9 | STAT_0x5AA9_WERT | Tastverhältnis GLF System | % | glfpwm | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5AAA_WERT | 0x5AAA | STAT_0x5AAA_WERT | Tastverhältnis PWM Ansteuerung Öldruck | % | tvpoel_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AAB_WERT | 0x5AAB | STAT_0x5AAB_WERT | Tastverhältnis an Endstufe des Ladedruckstellers | % | tvldste_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AB0_WERT | 0x5AB0 | STAT_0x5AB0_WERT | Ladedruck- Sollwert | hPa | psolldr_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| IVKMH | 0x5AB1 | STAT_GESCHWINDIGKEIT_WERT | Fahrzeuggeschwindigkeit | km/h | vfzg_w | - | unsigned integer | - | 0,0078125 | 1 | 0,0 |
| STAT_0x5AB3_WERT | 0x5AB3 | STAT_0x5AB3_WERT | Zähler für gefahrene Kilometer mit MIL EIN | km | DSMDur_ctPID21h | - | unsigned long | - | 0,009999999776482582 | 1 | 0,0 |
| IZBST | 0x5AB4 | STAT_BETRIEBSSTUNDENZAEHLER_WERT | sekundengenauer Betribsstundenzähler als 32 Bitwert | s | top_l | - | unsigned long | - | 0,10000000149011612 | 1 | 0,0 |
| RTANS | 0x5AB6 | STAT_ANSAUGLUFTTEMPERATUR1_ROH_WERT | Ansauglufttemperatur, linearisiert und umgerechnet | Grad C | tanslin | - | unsigned char | - | 0,75 | 1 | -48,0 |
| RTKWA | 0x5AB7 | STAT_KUEHLWASSERTEMPERATUR_ROH_WERT | Motortemperatur, linearisiert und umgerechnet | Grad C | tmotlin | - | unsigned char | - | 0,75 | 1 | -48,0 |
| IUSAU | 0x5AB8 | STAT_SAUGROHRDRUCK_SPANNUNG_WERT | Spannung Drucksensor Saugrohrdruck (word) | V | udss_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IMLUF | 0x5ABC | STAT_LUFTMASSE_WERT | Luftmassenfluss gefiltert (Word) | kg/h | ml_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| IASRE | 0x5ABD | STAT_STARTRELAIS_AKTIV_WERT | Bedingung automatischer Start | 0/1 | B_sta | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x5ABE_WERT | 0x5ABE | STAT_0x5ABE_WERT | I-Regler Mengenregelung Kraftstoffsystem | mg | FUEL_MASS_REQ_I_CTL_H_RES | - | signed integer | - | 0,0211944580078125 | 1 | 0,0 |
| STAT_0x5ABF_WERT | 0x5ABF | STAT_0x5ABF_WERT | Verbrauch ohne Regler | l/h | VFF_MFF_SP_FUP_CTL | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 |
| STAT_0x5AC0_WERT | 0x5AC0 | STAT_0x5AC0_WERT | Verbrauch mit Regler | l/h | VFF_VCV | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 |
| STAT_0x5AC2_WERT | 0x5AC2 | STAT_0x5AC2_WERT | Reset Information  | - | Reset_Env.adLoc | - | unsigned long | - | 1,0 | 1 | 0,0 |
| STAT_0x5AC4_WERT | 0x5AC4 | STAT_0x5AC4_WERT | Raildruck Kraftstoffsystem Sollwert | MPa | prsoll_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| STAT_0x5AC5_WERT | 0x5AC5 | STAT_0x5AC5_WERT | Tastverhältnis Mengensteuerventil | % | PWM_VCV | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AC6_WERT | 0x5AC6 | STAT_0x5AC6_WERT | Modus Kraftstoffsystem (Druck-, Mengen-, Max-Regelung) | 0-n | STATE_PWM_VCV | - | unsigned char | ba_vcv_state_text | 1 | 1 | 0 |
| STAT_0x5AD5_WERT | 0x5AD5 | STAT_0x5AD5_WERT | Kraftstofftemperatur | Grad C | tkrst | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x5AD6_WERT | 0x5AD6 | STAT_0x5AD6_WERT | Bedingung Schubabschalten | 0/1 | B_sa | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x5AE2_WERT | 0x5AE2 | STAT_0x5AE2_WERT | Reset Information - Reset-group-ID of the last reset reason | 0-n | Reset_Env.xGrp | - | unsigned char | Reset_GrpID | 1 | 1 | 0 |
| STAT_0x5AE3_WERT | 0x5AE3 | STAT_0x5AE3_WERT | Reset Information - Reset-ID of the last reset | 0-n | Reset_Env.xId | - | unsigned integer | Reset_ID | 1 | 1 | 0 |
| STAT_0x5AE4_WERT | 0x5AE4 | STAT_0x5AE4_WERT | Reset Information - User defined value of the last reset reason | - | Reset_Env.xUserValue | - | unsigned long | - | 1,0 | 1 | 0,0 |
| STAT_0x5AEB_WERT | 0x5AEB | STAT_0x5AEB_WERT | Kühlmitteltemperatur &lt; 98°C | % | tmotb1_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AEC_WERT | 0x5AEC | STAT_0x5AEC_WERT | 98°C =&lt; Kühlmitteltemperatur =&lt; 112°C | % | tmotb2_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AED_WERT | 0x5AED | STAT_0x5AED_WERT | 113°C =&lt; Kühlmitteltemperatur =&lt; 120°C | % | tmotb3_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AEE_WERT | 0x5AEE | STAT_0x5AEE_WERT | 121°C =&lt; Kühlmitteltemperatur =&lt; 125°C | % | tmotb4_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AEF_WERT | 0x5AEF | STAT_0x5AEF_WERT | Kühlmitteltemperatur &gt; 125°C | % | tmotb5_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AF0_WERT | 0x5AF0 | STAT_0x5AF0_WERT | Motoröltemperatur &lt; 80°C | % | toelb1_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AF1_WERT | 0x5AF1 | STAT_0x5AF1_WERT | 80°C =&lt; Motoröltemperatur =&lt; 110°C | % | toelb2_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AF2_WERT | 0x5AF2 | STAT_0x5AF2_WERT | 110°C =&lt; Motoröltemperatur =&lt; 135°C | % | toelb3_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AF3_WERT | 0x5AF3 | STAT_0x5AF3_WERT | 135°C =&lt; Motoröltemperatur =&lt; 150°C | % | toelb4_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AF4_WERT | 0x5AF4 | STAT_0x5AF4_WERT | Motoröltemperatur &gt; 150°C | % | toelb5_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AF5_WERT | 0x5AF5 | STAT_0x5AF5_WERT | Getriebeöltemperatur &lt; 80°C | % | tgetb1_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AF6_WERT | 0x5AF6 | STAT_0x5AF6_WERT | 80°C =&lt; Getriebeöltemperatur =&lt; 109°C | % | tgetb2_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AF7_WERT | 0x5AF7 | STAT_0x5AF7_WERT | 110°C =&lt; Getriebeöltemperatur =&lt; 124°C | % | tgetb3_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AF8_WERT | 0x5AF8 | STAT_0x5AF8_WERT | 125°C =&lt; Getriebeöltemperatur =&lt; 129°C | % | tgetb4_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AF9_WERT | 0x5AF9 | STAT_0x5AF9_WERT | Getriebeöltemperatur &gt; 129°C | % | tgetb5_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AFA_WERT | 0x5AFA | STAT_0x5AFA_WERT | Umgebungstemperatur &lt; 3°C | % | tumgb1_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AFB_WERT | 0x5AFB | STAT_0x5AFB_WERT | 3°C =&lt; Umgebungstemperatur =&lt; 19°C | % | tumgb2_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AFC_WERT | 0x5AFC | STAT_0x5AFC_WERT | 20°C =&lt; Umgebungstemperatur =&lt; 29°C | % | tumgb3_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AFD_WERT | 0x5AFD | STAT_0x5AFD_WERT | 30°C =&lt; Umgebungstemperatur =&lt; 39°C | % | tumgb4_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AFE_WERT | 0x5AFE | STAT_0x5AFE_WERT | Umgebungstemperatur &gt; 39°C | % | tumgb5_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5B10_WERT | 0x5B10 | STAT_0x5B10_WERT | Superklopfen | - | iskn1r1_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B11_WERT | 0x5B11 | STAT_0x5B11_WERT | Superklopfen | - | iskn1r2_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B12_WERT | 0x5B12 | STAT_0x5B12_WERT | Superklopfen | - | iskn1r3_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B13_WERT | 0x5B13 | STAT_0x5B13_WERT | Superklopfen | - | iskn2r1_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B14_WERT | 0x5B14 | STAT_0x5B14_WERT | Superklopfen | - | iskn2r2_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B15_WERT | 0x5B15 | STAT_0x5B15_WERT | Superklopfen | - | iskn2r3_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B20_WERT | 0x5B20 | STAT_0x5B20_WERT | Superklopfen | - | iskn3r1_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B21_WERT | 0x5B21 | STAT_0x5B21_WERT | Superklopfen | - | iskn3r2_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B22_WERT | 0x5B22 | STAT_0x5B22_WERT | Superklopfen | - | iskn3r3_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B23_WERT | 0x5B23 | STAT_0x5B23_WERT | [0] Aussetzerzähler im Abgasintervall Zyl. 1 | - | fzabgzyl_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B24_WERT | 0x5B24 | STAT_0x5B24_WERT | [4] Aussetzerzähler im Abgasintervall Zyl. 2 | - | fzabgzyl_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B25_WERT | 0x5B25 | STAT_0x5B25_WERT | [2] Aussetzerzähler im Abgasintervall Zyl. 3 | - | fzabgzyl_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B30_WERT | 0x5B30 | STAT_0x5B30_WERT | [5] Aussetzerzähler im Abgasintervall Zyl. 4 | - | fzabgzyl_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B31_WERT | 0x5B31 | STAT_0x5B31_WERT | [1] Aussetzerzähler im Abgasintervall Zyl. 5 | - | fzabgzyl_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5B32_WERT | 0x5B32 | STAT_0x5B32_WERT | [3] Aussetzerzähler im Abgasintervall Zyl. 6 | - | fzabgzyl_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x58FF | - | Umweltbedingung unbekannt | - | - | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-reset-grpid"></a>
### RESET_GRPID

Dimensions: 33 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | SWRESET_GRP_POWERON_E |
| 0x01 | SWRESET_GRP_HWRESET_E |
| 0x02 | SWRESET_GRP_WDT_E |
| 0x03 | SWRESET_GRP_WAKEUP_E |
| 0x04 | SWRESET_GRP_TRAP_E |
| 0x05 | SWRESET_GRP_SB_E |
| 0x06 | SWRESET_GRP_CB_E |
| 0x07 | SWRESET_SOFTRESETGRP_E |
| 0x08 | SWRESET_GRP_DUMMY_01 |
| 0x09 | SWRESET_GRP_DUMMY_02 |
| 0x0A | SWRESET_GRP_DUMMY_03 |
| 0x0B | RESET_EEP_GRP_E |
| 0x0C | RESET_SWRESET_EPM_E |
| 0x0D | RESET_SWRESET_ESC_E |
| 0x0E | RESET_EXECON_GRP_E |
| 0x0F | RESET_SWRESET_ASW_01 |
| 0x10 | SWRESET_GRP_MO_PREICO |
| 0x11 | RESET_SWRESET_MOC |
| 0x12 | RESET_SWRESET_SOP |
| 0x13 | RESET_SWRESET_MOFICO |
| 0x14 | SWRESET_OCWDA |
| 0x15 | RESET_SWRESET_OS_01 |
| 0x16 | SWRESET_PCP_GRP_E |
| 0x17 | RESET_HWEMONGRP_E |
| 0x18 | RESET_ERRINTRGRP_E |
| 0x19 | SWRESET_SYCGRP_E |
| 0x1A | RESET_SWRESET_TPROT |
| 0x1B | SWRESET_UNSUPPORTED_CPU_E |
| 0x1C | RESET_ADCI_E |
| 0x1D | SWRESET_R2S2_INI_GRP_E |
| 0x1E | RESET_DMA_E |
| 0x1F | RESET_FLASH_E |
| 0xFF | undefiniert |

<a id="table-reset-id"></a>
### RESET_ID

Dimensions: 145 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | SWRESET_POWERON_E |
| 0x0001 | SWRESET_POWERON_WDT_E |
| 0x0002 | SWRESET_POWERON_KL15_E |
| 0x0003 | SWRESET_HW_E |
| 0x0004 | SWRESET_WDT_E |
| 0x1000 | TRAP_MMU_VAF_E |
| 0x1001 | TRAP_MMU_VAP_E |
| 0x1002 | TRAP_INTPROT_PRIV_E |
| 0x1003 | TRAP_INTPROT_MPR_E |
| 0x1004 | TRAP_INTPROT_MPW_E |
| 0x1005 | TRAP_INTPROT_MPX_E |
| 0x1006 | TRAP_INTPROT_MPP_E |
| 0x1007 | TRAP_INTPROT_MPN_E |
| 0x1008 | TRAP_INTPROT_GRWP_E |
| 0x1009 | TRAP_INSTRERR_IOPC_E |
| 0x100A | TRAP_INSTRERR_UOPC_E |
| 0x100B | TRAP_INSTRERR_OPD_E |
| 0x100C | TRAP_INSTRERR_ALN_E |
| 0x100D | TRAP_INSTRERR_MEM_E |
| 0x100E | TRAP_CONTMANA_FCD_E |
| 0x100F | TRAP_CONTMANA_CDO_E |
| 0x1010 | TRAP_CONTMANA_CDU_E |
| 0x1011 | TRAP_CONTMANA_FCU_E |
| 0x1012 | TRAP_CONTMANA_CSU_E |
| 0x1013 | TRAP_CONTMANA_CTYP_E |
| 0x1014 | TRAP_CONTMANA_NEST_E |
| 0x1015 | TRAP_SYSBUSERR_PSE_E |
| 0x1016 | TRAP_SYSBUSERR_DSE_E |
| 0x1017 | TRAP_SYSBUSERR_DAE_E |
| 0x1018 | TRAP_SYSBUSERR_CAE_E |
| 0x1019 | TRAP_SYSBUSERR_PIE_E |
| 0x101A | TRAP_SYSBUSERR_DIE_E |
| 0x101B | TRAP_ASSTRAP_OVF_E |
| 0x101C | TRAP_ASSTRAP_SOVF_E |
| 0x101D | TRAP_SYSCALL_SYS_E |
| 0x101E | TRAP_NMI_ESR0_E |
| 0x101F | TRAP_NMI_ESR1_E |
| 0x1020 | TRAP_NMI_RES0_E |
| 0x1021 | TRAP_NMI_WDT_E |
| 0x1022 | TRAP_NMI_PE_E |
| 0x1023 | TRAP_NMI_OSCLWD_E |
| 0x1024 | TRAP_NMI_OSCHWD_E |
| 0x1025 | TRAP_NMI_OSCSPWD_E |
| 0x1026 | TRAP_NMI_SYSVCOLCK_E |
| 0x1027 | TRAP_NMI_ERAYVCOLCKT |
| 0x1028 | TRAP_NMI_FLOT_E |
| 0x2000 | SWRESET_POWERON_SIMU_E |
| 0x2001 | SWRESET_HRESET_SIMU_E |
| 0x2002 | SWRESET_RB_PROG_E |
| 0x2003 | SWRESET_SOFTRESET_5VUNDERVOLTAGE_E |
| 0x2004 | SWRESET_SOFTRESET_POSTDRV2PREDRV_E |
| 0x2005 | SWRESET_CBPROG_E |
| 0x2006 | SWRESET_CBCPU_E |
| 0x2007 | SWRESET_SBDUMMY_1_E |
| 0x2008 | SWRESET_SBDUMMY_2_E |
| 0x2009 | SWRESET_SBDUMMY_3_E |
| 0x200A | SWRESET_SBDUMMY_4_E |
| 0x200B | SWRESET_SBDUMMY_5_E |
| 0x200C | SWRESET_SBDUMMY_6_E |
| 0x200D | SWRESET_SBDUMMY_7_E |
| 0x200E | SWRESET_SBDUMMY_8_E |
| 0x3000 | SWRST_EEPBANDGAP_E |
| 0x3001 | SWRST_EEPNODEBUGGER_E |
| 0x3002 | SWRST_EEPDELENVRAM_E |
| 0x3003 | SWRST_WRITE_ERRORS_SECTORCHANGE_E |
| 0x3004 | SWRST_EEPACTFIRSTINIT_E |
| 0x3005 | RESET_SWRESET_EPMHCRS_WAIT_PCP_RESET_E |
| 0x3006 | RESET_SWRESET_ESC_SCHED_RESET_E |
| 0x3007 | SWRST_EXECON_FAULTYSTATE_E |
| 0x3008 | RESET_SWRESET_ILLEGAL_OPCODE |
| 0x3009 | RESET_SWRESET_ILLEGAL_RETURN_TO_MAIN |
| 0x300A | SWRESET_MOCADCNTP_PREICO |
| 0x300B | SWRESET_MOCADCTST_PREICO |
| 0x300C | RESET_SWRESET_ILLEGAL_SW_PATH |
| 0x300D | RESET_SWRESET_MOCCOM_SPI_ERROR |
| 0x300E | RESET_SWRESET_MOCCOM_CTSOPTST |
| 0x300F | RESET_SWRESET_MOCCOM_SOPTST |
| 0x3010 | RESET_SWRESET_MOCCOM_CPLCHK_FAILED |
| 0x3011 | RESET_SWRESET_MOCCOM_OS_TIMEOUT_ERROR |
| 0x3012 | RESET_SWRESET_MOCGPTA |
| 0x3013 | RESET_SWRESET_MOCMEM_CPL |
| 0x3014 | RESET_SWRESET_MOCMEM_RAM |
| 0x3015 | RESET_SWRESET_MOCMEM_ROM |
| 0x3016 | RESET_SWRESET_MOCPCP |
| 0x3017 | RESET_SWRESET_MOCRAM_WRI |
| 0x3018 | RESET_SWRESET_MOCRAM_CPL |
| 0x3019 | RESET_SWRESET_MOCRAM_RAMTAB |
| 0x301A | RESET_SWRESET_MOCRAM_RSTPTRRAM |
| 0x301B | RESET_SWRESET_MOCRAM_STACKRAM |
| 0x301C | RESET_SWRESET_MOCRAM_CSARAM |
| 0x301D | RESET_SWRESET_MOCRAM_XRAM |
| 0x301E | RESET_SWRESET_MOCRAM_IRAM |
| 0x301F | RESET_SWRESET_MOCRAM_EXRAM |
| 0x3020 | RESET_SWRESET_MOCRAM_PROTRAM |
| 0x3021 | RESET_SWRESET_MOCRAM_EEPCPL |
| 0x3022 | RESET_SWRESET_MOCRAM_REPEXOK |
| 0x3023 | RESET_SWRESET_MOCROM |
| 0x3024 | RESET_SWRESET_MOCROM_CPL |
| 0x3025 | RESET_SWRESET_MOCROM_INDEX |
| 0x3026 | RESET_SWRESET_MOCROM_WD |
| 0x3027 | RESET_SWRESET_SOPTEST_FAILED |
| 0x3028 | RESET_SWRESET_CPLCHK_FAILED |
| 0x3029 | RESET_SWRESET_MOCSOP_MSC_ERROR |
| 0x302A | RESET_SWRESET_MOCSOP_SPI_ERROR |
| 0x302B | RESET_SWRESET_MOCSOP_OS_TIMEOUT_ERROR |
| 0x302C | RESET_SWRESET_MOCSOP_TIRESPTIME_ERROR |
| 0x302D | SWRESET_MOFAIR_ADJ_PREICO |
| 0x302E | SWRESET_MOFAPP_PREICO |
| 0x302F | SWRESET_MOFESPD_PREICO |
| 0x3030 | SWRESET_MOFGKC_PREICO |
| 0x3031 | SWRESET_MOFRLC_PREICO |
| 0x3032 | RESET_SWRESET_MOFICO_CHK_SYEGAS_FAILED |
| 0x3033 | SWRESET_MOFMODC_PREICO |
| 0x3034 | SWRESET_MOFRKTI_PREICO |
| 0x3035 | SWRESET_MOFTRQCMP_PREICO |
| 0x3036 | SWRESET_MOFTRQRAT_PREICO |
| 0x3037 | SWRESET_MOFVAR_PREICO |
| 0x3038 | SWRESET_MOFZWC_PREICO |
| 0x3039 | SWRESET_OCWDA_WDA_ACTV |
| 0x303A | SWRESET_OCWDA_WDA_MONITOR |
| 0x303B | SWRESET_OCWDA_LOW_VLTG |
| 0x303C | SWRESET_OCWDA_OVR_VLTG |
| 0x303D | RESET_SWRESET_INTERRUPTLOCK_EXPECTED |
| 0x303E | RESET_USERSTACKOVERFLOW_DETECTED |
| 0x303F | SWRESET_PCP_ERROR_E |
| 0x3040 | SWRST_HWEMONDEFAULT_E |
| 0x3041 | RESET_ERRINTR_E |
| 0x3042 | SWRESET_CALWAKEUP_E |
| 0x3043 | SWRESET_DEADLINE1MS_E |
| 0x3044 | SWRESET_DEADLINE10MS_E |
| 0x3045 | SWRESET_DEADLINEBG_E |
| 0x3046 | SWRESET_NMIDISABLED_E |
| 0x3047 | SWRESET_POSTDRIVE_E |
| 0x3048 | SWRESET_SOFTRESET_WAKEUP_E |
| 0x3049 | SWRESET_SOFTRESET_SHUTDOWN_E |
| 0x304A | SWRESET_T15RSTSHUTDOWN_E |
| 0x304B | SWRESET_UNDERVOLTAGE_E |
| 0x304C | SWRESET_T15_PRE_E |
| 0x304D | RESET_SWRESET_SWOVER_DONE |
| 0x304E | SWRESET_CORE_ENV_E |
| 0x304F | SWRST_ADCI_ERROR_E |
| 0x3050 | SWRST_R2S2_INI_ERROR_E |
| 0x3051 | RESET_DMA_ERROR_E |
| 0x3052 | SWRST_FLASHCONFIG_E |
| 0xFFFF | undefiniert |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| 1 | BMW-FAST |
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-ba-vcv-state-text"></a>
### BA_VCV_STATE_TEXT

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | VCV_TEST |
| 0x01 | START |
| 0x02 | MFP_CTL |
| 0x03 | VCV_CLOSE |
| 0x04 | VCV_CRASH |
| 0x05 | MFP_MAX |
| 0x06 | VCV_LIH |
| 0xFF | undefiniert |

<a id="table-msd80n43-cnv-s-2-def-bit-ub-741-cm"></a>
### _MSD80N43_CNV_S_2_DEF_BIT_UB_741_CM

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Falsch |
| 1 | Wahr |

<a id="table-stat-ruhestrom"></a>
### STAT_RUHESTROM

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 0 keine Ruhestromverletzung, keine Standverbraucher aktiv |
| 0x01 | 1 Ruhestrom 80 bis 200mA aktiv, keine Standverbraucher aktiv |
| 0x02 | 2 Ruhestrom 200 bis 1000mA aktiv, keine Standverbraucher aktiv |
| 0x03 | 3 Ruhestrom über 1000mA aktiv, keine Standverbraucher aktiv |
| 0x04 | 4 keine Ruhestromverletzung, Standverbraucher Licht aktiv |
| 0x05 | 5 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Licht aktiv |
| 0x06 | 6 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Licht aktiv |
| 0x07 | 7 Ruhestrom über 1000mA aktiv, Standverbraucher Licht aktiv |
| 0x08 | 8 keine Ruhestromverletzung, Standverbraucher Standheizung aktiv |
| 0x09 | 9 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0A | 10 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0B | 11 Ruhestrom über 1000mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0C | 12 keine Ruhestromverletzung, Standverbraucher Sonstige aktiv |
| 0x0D | 13 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Sonstige aktiv |
| 0x0E | 14 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Sonstige aktiv |
| 0x0F | 15 Ruhestrom über 1000mA aktiv, Standverbraucher Sonstige aktiv |
| 0xFF | 255 Status unbekannt |

<a id="table-tindividualdataliste"></a>
### TINDIVIDUALDATALISTE

Dimensions: 1 rows × 17 columns

| ENTRYNR | ISLAST | FROMWHERE | DIAG | CARORKEY | USECASE | TESTER_ALGO | RESERVED | INQY_LEN | INQY_DATA | RESP_LEN | RESP_DATA | WRITE_LEN | WRITE_DATA | W_RESP_LEN | W_RESP_DATA | COMMENT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0000 | 0xFF | 01 | 12 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 00 |  | 00 |  | PM.Recovery |

<a id="table-statclientauthtxt"></a>
### STATCLIENTAUTHTXT

Dimensions: 4 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0x00 | Freigabe von Zuendung und Einspritzung (noch) nicht erteilt (noch nicht versucht oder Kommunikation gestört, Motorlauf gesperrt) |
| 0x01 | Freigabe von Zuendung und Einspritzung erteilt (Challenge-Response erfolgreich) |
| 0x02 | Freigabe von Zuendung und Einspritzung abgelehnt (Challenge-Response fehlgeschlagen, falsche Response, Kommunikation i.O.) |
| 0x03 | nicht definiert |

<a id="table-statfreesktxt"></a>
### STATFREESKTXT

Dimensions: 3 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0xFE | Ablage unbegrenzt |
| 0xFF | ungültig |
| 0xXY | freie Ablagen |

<a id="table-statewsvertxt"></a>
### STATEWSVERTXT

Dimensions: 3 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0x01 | Direktschreiben des SecretKey |
| 0x02 | Direktschreiben des SecretKey und DH-Abgleich |
| 0xXY | unbekannt |

<a id="table-swtfehler-tab"></a>
### SWTFEHLER_TAB

Dimensions: 51 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x31 | OUT_OF_RANGE |
| 0xCD | KEYFAKTOR_NICHT_VORHANDEN |
| 0xD0 | EXTENSION_CHECK_FEHLERHAFT |
| 0xD1 | FSC_UNGUELTIG |
| 0xD2 | FGN_ZUGRIFF_FEHLERHAFT |
| 0xD3 | KEIN_SPEICHERPLATZ_MEHR_VORHANDEN |
| 0xD4 | FALSCHER_ZERTIFIKATSINHALT_UNBEKANNTES_CRIT-ELEMENT |
| 0xD5 | FALSCHER_FSC_INHALT |
| 0xD6 | FALSCHE_PARAMETERS |
| 0xD7 | FSCS_ZERTIFIKAT_ABGELEHNT |
| 0xD8 | KEINE_DATEN_ZU_ANGEGEBENEM_SG_VORHANDEN |
| 0xD9 | KEINE_AUTHENTISIERUNG |
| 0xDA | FINGER_PRINT_MECHANISMUS_NOT_OK |
| 0xDB | SIGS_ID_UND_ZERTIFIKAT_PASSEN_NICHT_ZUSAMMEN |
| 0xDC | GUELTIGKEITS_PRUEFUNG_SCHLUG_FEHL |
| 0xDD | FAHRGESTELLNUMMER_FEHLERHAFT |
| 0xDE | FGN_PRUEFUNG_SCHLUG_FEHL |
| 0xDF | FLASH_LESEFEHLER |
| 0xE0 | FLASH_SCHREIBFEHLER |
| 0xE1 | FALSCHER_ZERTIFIKATSINHALT_KEY_USAGE |
| 0xE2 | FALSCHER_ZERTIFIKATSINHALT_ISSUER |
| 0xE3 | FALSCHER_ZERTIFIKATSINHALT_VALIDITY |
| 0xE4 | FSCS_ZERTIFIKAT_PRUEFUNG_SCHLUG_FEHL |
| 0xE5 | FSCS_ZERTIFIKAT_UNGUELTIG |
| 0xE6 | FSCS_ZERTIFIKAT_NOCH_NICHT_GEPRUEFT |
| 0xE7 | FSCS_ZERTIFIKAT_NICHT_VORHANDEN |
| 0xE8 | SIGS_ZERTIFIKAT__PRUEFUNG_SCHLUG_FEHL |
| 0xE9 | SIGS_ZERTIFIKAT_UNGUELTIG |
| 0xEA | SIGS_ZERTIFIKAT_NOCH_NICHT_GEPRUEFT |
| 0xEB | SIGS_ZERTIFIKAT_NICHT_VORHANDEN |
| 0xEC | ROOT_ZERTIFIKAT_UNGUELTIG |
| 0xED | ROOT_ZERTIFIKAT_STATUS_ABGELEHNT |
| 0xEE | ROOT_ZERTIFIKAT_FEHLERHAFT |
| 0xEF | ROOT_ZERTIFIKAT_NICHT_LESBAR |
| 0xF0 | ROOT_ZERTIFIKAT_NICHT_VORHANDEN |
| 0xF1 | ZERTIFIKAT_STATUS_ABGELEHNT |
| 0xF2 | ZERTIFIKAT_NICHT_VORHANDEN |
| 0xF3 | FSC_PRUEFUNG_SCHLUG_FEHL |
| 0xF4 | FSC_STORNIERT |
| 0xF5 | FSC_STATUS_ABGELEHNT |
| 0xF6 | FSC_NICHT_VORHANDEN |
| 0xF7 | FALSCHE_FSCS_ID_IM_FSC |
| 0xF8 | UNGUELTIGES_FSC_ERSTELLUNGSDDATUM |
| 0xF9 | SIGNATUR_PRUEFUNG_SCHLUG_FEHL |
| 0xFA | SW_SIGNATURPRUEFUNG_SCHLUG_FEHL |
| 0xFB | SW_SIG_STATUS_ABGELEHNT |
| 0xFC | SW_ID_PRUEFUNG_SCHLUG_FEHL |
| 0xFD | SW_NICHT_AKTIVIERT |
| 0xFE | SW_NICHT_EINGESPIELT |
| 0xFF | UNBEKANNTER_FEHLER |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-auslesemode"></a>
### _AUSLESEMODE

Dimensions: 5 rows × 2 columns

| NR | MODE |
| --- | --- |
| 0x00 | GROESSE |
| 0x01 | INPA |
| 0x02 | SGBD |
| 0x03 | FASTA |
| 0xFF | 0 |

<a id="table-eisyugd-inpa"></a>
### _EISYUGD_INPA

Dimensions: 9 rows × 6 columns

| NR | NKW_WERT | VSE_SPRI_WERT | VSA_SPRI_WERT | HUBEV_IST_WERT | PS_WERT |
| --- | --- | --- | --- | --- | --- |
| 0x00 | 660 | 90 | 105 | 0.4 | 900 |
| 0x01 | 660 | 90 | 105 | 1.5 | 900 |
| 0x02 | 660 | 90 | 105 | 2.0 | 900 |
| 0x03 | 1500 | 60 | 72 | 1.5 | 900 |
| 0x04 | 2000 | 56 | 70 | 2.5 | 900 |
| 0x05 | 3000 | 88 | 98 | 9.7 | 1500 |
| 0x06 | 4000 | 108 | 110 | 9.7 | 1500 |
| 0x07 | 6000 | 108 | 110 | 9.7 | 1500 |
| 0xFF | 0 | 0 | 0 | 0 | 0 |

<a id="table-eisyugd-fasta"></a>
### _EISYUGD_FASTA

Dimensions: 6 rows × 6 columns

| NR | NKW_WERT | VSE_SPRI_WERT | VSA_SPRI_WERT | HUBEV_IST_WERT | PS_WERT |
| --- | --- | --- | --- | --- | --- |
| 0x00 | 660 | 90 | 105 | 0.4 | 900 |
| 0x01 | 1500 | 60 | 72 | 1.5 | 900 |
| 0x02 | 2000 | 56 | 70 | 2.5 | 900 |
| 0x03 | 3000 | 88 | 98 | 9.7 | 1500 |
| 0x04 | 4000 | 108 | 110 | 9.7 | 1500 |
| 0xFF | 0 | 0 | 0 | 0 | 0 |

<a id="table-eisygd-inpa"></a>
### _EISYGD_INPA

Dimensions: 6 rows × 5 columns

| NR | NKW_WERT | VSE_SPRI_WERT | VSA_SPRI_WERT | WDK_IST_WERT |
| --- | --- | --- | --- | --- |
| 0x00 | 660 | 120.0 | 115.0 | 4.00 |
| 0x01 | 2000 | 65.0 | 85.0 | 10.00 |
| 0x02 | 3000 | 90.0 | 100.0 | 15.00 |
| 0x03 | 4000 | 100.0 | 100.0 | 20.00 |
| 0x04 | 5000 | 110.0 | 110.0 | 30.00 |
| 0xFF | 0 | 0 | 0 | 0 |

<a id="table-krann-inpa"></a>
### _KRANN_INPA

Dimensions: 145 rows × 4 columns

| NR | NKW_WERT | RF_WERT | TANS_WERT |
| --- | --- | --- | --- |
| 0x00 | 660 | 15 | 30 |
| 0x01 | 720 | 15 | 30 |
| 0x02 | 900 | 15 | 30 |
| 0x03 | 1200 | 15 | 30 |
| 0x04 | 1500 | 15 | 30 |
| 0x05 | 2000 | 15 | 30 |
| 0x06 | 2500 | 15 | 30 |
| 0x07 | 3000 | 15 | 30 |
| 0x08 | 4000 | 15 | 30 |
| 0x09 | 5000 | 15 | 30 |
| 0x0A | 6000 | 15 | 30 |
| 0x0B | 7000 | 15 | 30 |
| 0x0C | 660 | 20 | 30 |
| 0x0D | 720 | 20 | 30 |
| 0x0E | 900 | 20 | 30 |
| 0x0F | 1200 | 20 | 30 |
| 0x10 | 1500 | 20 | 30 |
| 0x11 | 2000 | 20 | 30 |
| 0x12 | 2500 | 20 | 30 |
| 0x13 | 3000 | 20 | 30 |
| 0x14 | 4000 | 20 | 30 |
| 0x15 | 5000 | 20 | 30 |
| 0x16 | 6000 | 20 | 30 |
| 0x17 | 7000 | 20 | 30 |
| 0x18 | 660 | 25 | 30 |
| 0x19 | 720 | 25 | 30 |
| 0x1A | 900 | 25 | 30 |
| 0x1B | 1200 | 25 | 30 |
| 0x1C | 1500 | 25 | 30 |
| 0x1D | 2000 | 25 | 30 |
| 0x1E | 2500 | 25 | 30 |
| 0x1F | 3000 | 25 | 30 |
| 0x20 | 4000 | 25 | 30 |
| 0x21 | 5000 | 25 | 30 |
| 0x22 | 6000 | 25 | 30 |
| 0x23 | 7000 | 25 | 30 |
| 0x24 | 660 | 30 | 30 |
| 0x25 | 720 | 30 | 30 |
| 0x26 | 900 | 30 | 30 |
| 0x27 | 1200 | 30 | 30 |
| 0x28 | 1500 | 30 | 30 |
| 0x29 | 2000 | 30 | 30 |
| 0x2A | 2500 | 30 | 30 |
| 0x2B | 3000 | 30 | 30 |
| 0x2C | 4000 | 30 | 30 |
| 0x2D | 5000 | 30 | 30 |
| 0x2E | 6000 | 30 | 30 |
| 0x2F | 7000 | 30 | 30 |
| 0x30 | 660 | 35 | 30 |
| 0x31 | 720 | 35 | 30 |
| 0x32 | 900 | 35 | 30 |
| 0x33 | 1200 | 35 | 30 |
| 0x34 | 1500 | 35 | 30 |
| 0x35 | 2000 | 35 | 30 |
| 0x36 | 2500 | 35 | 30 |
| 0x37 | 3000 | 35 | 30 |
| 0x38 | 4000 | 35 | 30 |
| 0x39 | 5000 | 35 | 30 |
| 0x3A | 6000 | 35 | 30 |
| 0x3B | 7000 | 35 | 30 |
| 0x3C | 660 | 40 | 30 |
| 0x3D | 720 | 40 | 30 |
| 0x3E | 900 | 40 | 30 |
| 0x3F | 1200 | 40 | 30 |
| 0x40 | 1500 | 40 | 30 |
| 0x41 | 2000 | 40 | 30 |
| 0x42 | 2500 | 40 | 30 |
| 0x43 | 3000 | 40 | 30 |
| 0x44 | 4000 | 40 | 30 |
| 0x45 | 5000 | 40 | 30 |
| 0x46 | 6000 | 40 | 30 |
| 0x47 | 7000 | 40 | 30 |
| 0x48 | 660 | 50 | 30 |
| 0x49 | 720 | 50 | 30 |
| 0x4A | 900 | 50 | 30 |
| 0x4B | 1200 | 50 | 30 |
| 0x4C | 1500 | 50 | 30 |
| 0x4D | 2000 | 50 | 30 |
| 0x4E | 2500 | 50 | 30 |
| 0x4F | 3000 | 50 | 30 |
| 0x50 | 4000 | 50 | 30 |
| 0x51 | 5000 | 50 | 30 |
| 0x52 | 6000 | 50 | 30 |
| 0x53 | 7000 | 50 | 30 |
| 0x54 | 660 | 60 | 30 |
| 0x55 | 720 | 60 | 30 |
| 0x56 | 900 | 60 | 30 |
| 0x57 | 1200 | 60 | 30 |
| 0x58 | 1500 | 60 | 30 |
| 0x59 | 2000 | 60 | 30 |
| 0x5A | 2500 | 60 | 30 |
| 0x5B | 3000 | 60 | 30 |
| 0x5C | 4000 | 60 | 30 |
| 0x5D | 5000 | 60 | 30 |
| 0x5E | 6000 | 60 | 30 |
| 0x5F | 7000 | 60 | 30 |
| 0x60 | 660 | 70 | 30 |
| 0x61 | 720 | 70 | 30 |
| 0x62 | 900 | 70 | 30 |
| 0x63 | 1200 | 70 | 30 |
| 0x64 | 1500 | 70 | 30 |
| 0x65 | 2000 | 70 | 30 |
| 0x66 | 2500 | 70 | 30 |
| 0x67 | 3000 | 70 | 30 |
| 0x68 | 4000 | 70 | 30 |
| 0x69 | 5000 | 70 | 30 |
| 0x6A | 6000 | 70 | 30 |
| 0x6B | 7000 | 70 | 30 |
| 0x6C | 660 | 80 | 30 |
| 0x6D | 720 | 80 | 30 |
| 0x6E | 900 | 80 | 30 |
| 0x6F | 1200 | 80 | 30 |
| 0x70 | 1500 | 80 | 30 |
| 0x71 | 2000 | 80 | 30 |
| 0x72 | 2500 | 80 | 30 |
| 0x73 | 3000 | 80 | 30 |
| 0x74 | 4000 | 80 | 30 |
| 0x75 | 5000 | 80 | 30 |
| 0x76 | 6000 | 80 | 30 |
| 0x77 | 7000 | 80 | 30 |
| 0x78 | 660 | 120 | 30 |
| 0x79 | 720 | 120 | 30 |
| 0x7A | 900 | 120 | 30 |
| 0x7B | 1200 | 120 | 30 |
| 0x7C | 1500 | 120 | 30 |
| 0x7D | 2000 | 120 | 30 |
| 0x7E | 2500 | 120 | 30 |
| 0x7F | 3000 | 120 | 30 |
| 0x80 | 4000 | 120 | 30 |
| 0x81 | 5000 | 120 | 30 |
| 0x82 | 6000 | 120 | 30 |
| 0x83 | 7000 | 120 | 30 |
| 0x84 | 660 | 150 | 30 |
| 0x85 | 720 | 150 | 30 |
| 0x86 | 900 | 150 | 30 |
| 0x87 | 1200 | 150 | 30 |
| 0x88 | 1500 | 150 | 30 |
| 0x89 | 2000 | 150 | 30 |
| 0x8A | 2500 | 150 | 30 |
| 0x8B | 3000 | 150 | 30 |
| 0x8C | 4000 | 150 | 30 |
| 0x8D | 5000 | 150 | 30 |
| 0x8E | 6000 | 150 | 30 |
| 0x8F | 7000 | 150 | 30 |
| 0xFF | 0 | 0 | 0 |

<a id="table-klann-inpa"></a>
### _KLANN_INPA

Dimensions: 228 rows × 4 columns

| NR | NKW_LOC_WERT | RK_LOC_WERT | TMOT_LOC_WERT |
| --- | --- | --- | --- |
| 0x00 | 700 | 0.12 | 100 |
| 0x01 | 700 | 0.15 | 100 |
| 0x02 | 700 | 0.20 | 100 |
| 0x03 | 700 | 0.30 | 100 |
| 0x04 | 700 | 0.40 | 100 |
| 0x05 | 700 | 0.50 | 100 |
| 0x06 | 700 | 0.70 | 100 |
| 0x07 | 700 | 1.00 | 100 |
| 0x08 | 700 | 1.20 | 100 |
| 0x09 | 700 | 1.40 | 100 |
| 0x0A | 700 | 1.60 | 100 |
| 0x0B | 700 | 1.80 | 100 |
| 0x0C | 1000 | 0.12 | 100 |
| 0x0D | 1000 | 0.15 | 100 |
| 0x0E | 1000 | 0.20 | 100 |
| 0x0F | 1000 | 0.30 | 100 |
| 0x10 | 1000 | 0.40 | 100 |
| 0x11 | 1000 | 0.50 | 100 |
| 0x12 | 1000 | 0.70 | 100 |
| 0x13 | 1000 | 1.00 | 100 |
| 0x14 | 1000 | 1.20 | 100 |
| 0x15 | 1000 | 1.40 | 100 |
| 0x16 | 1000 | 1.60 | 100 |
| 0x17 | 1000 | 1.80 | 100 |
| 0x18 | 1500 | 0.12 | 100 |
| 0x19 | 1500 | 0.15 | 100 |
| 0x1A | 1500 | 0.20 | 100 |
| 0x1B | 1500 | 0.30 | 100 |
| 0x1C | 1500 | 0.40 | 100 |
| 0x1D | 1500 | 0.50 | 100 |
| 0x1E | 1500 | 0.70 | 100 |
| 0x1F | 1500 | 1.00 | 100 |
| 0x20 | 1500 | 1.20 | 100 |
| 0x21 | 1500 | 1.40 | 100 |
| 0x22 | 1500 | 1.60 | 100 |
| 0x23 | 1500 | 1.80 | 100 |
| 0x24 | 2000 | 0.12 | 100 |
| 0x25 | 2000 | 0.15 | 100 |
| 0x26 | 2000 | 0.20 | 100 |
| 0x27 | 2000 | 0.30 | 100 |
| 0x28 | 2000 | 0.40 | 100 |
| 0x29 | 2000 | 0.50 | 100 |
| 0x2A | 2000 | 0.70 | 100 |
| 0x2B | 2000 | 1.00 | 100 |
| 0x2C | 2000 | 1.20 | 100 |
| 0x2D | 2000 | 1.40 | 100 |
| 0x2E | 2000 | 1.60 | 100 |
| 0x2F | 2000 | 1.80 | 100 |
| 0x30 | 2500 | 0.12 | 100 |
| 0x31 | 2500 | 0.15 | 100 |
| 0x32 | 2500 | 0.20 | 100 |
| 0x33 | 2500 | 0.30 | 100 |
| 0x34 | 2500 | 0.40 | 100 |
| 0x35 | 2500 | 0.50 | 100 |
| 0x36 | 2500 | 0.70 | 100 |
| 0x37 | 2500 | 1.00 | 100 |
| 0x38 | 2500 | 1.20 | 100 |
| 0x39 | 2500 | 1.40 | 100 |
| 0x3A | 2500 | 1.60 | 100 |
| 0x3B | 2500 | 1.80 | 100 |
| 0x3C | 3000 | 0.12 | 100 |
| 0x3D | 3000 | 0.15 | 100 |
| 0x3E | 3000 | 0.20 | 100 |
| 0x3F | 3000 | 0.30 | 100 |
| 0x40 | 3000 | 0.40 | 100 |
| 0x41 | 3000 | 0.50 | 100 |
| 0x42 | 3000 | 0.70 | 100 |
| 0x43 | 3000 | 1.00 | 100 |
| 0x44 | 3000 | 1.20 | 100 |
| 0x45 | 3000 | 1.40 | 100 |
| 0x46 | 3000 | 1.60 | 100 |
| 0x47 | 3000 | 1.80 | 100 |
| 0x48 | 4000 | 0.12 | 100 |
| 0x49 | 4000 | 0.15 | 100 |
| 0x4A | 4000 | 0.20 | 100 |
| 0x4B | 4000 | 0.30 | 100 |
| 0x4C | 4000 | 0.40 | 100 |
| 0x4D | 4000 | 0.50 | 100 |
| 0x4E | 4000 | 0.70 | 100 |
| 0x4F | 4000 | 1.00 | 100 |
| 0x50 | 4000 | 1.20 | 100 |
| 0x51 | 4000 | 1.40 | 100 |
| 0x52 | 4000 | 1.60 | 100 |
| 0x53 | 4000 | 1.80 | 100 |
| 0x54 | 5000 | 0.12 | 100 |
| 0x55 | 5000 | 0.15 | 100 |
| 0x56 | 5000 | 0.20 | 100 |
| 0x57 | 5000 | 0.30 | 100 |
| 0x58 | 5000 | 0.40 | 100 |
| 0x59 | 5000 | 0.50 | 100 |
| 0x5A | 5000 | 0.70 | 100 |
| 0x5B | 5000 | 1.00 | 100 |
| 0x5C | 5000 | 1.20 | 100 |
| 0x5D | 5000 | 1.40 | 100 |
| 0x5E | 5000 | 1.60 | 100 |
| 0x5F | 5000 | 1.80 | 100 |
| 0x60 | 6000 | 0.12 | 100 |
| 0x61 | 6000 | 0.15 | 100 |
| 0x62 | 6000 | 0.20 | 100 |
| 0x63 | 6000 | 0.30 | 100 |
| 0x64 | 6000 | 0.40 | 100 |
| 0x65 | 6000 | 0.50 | 100 |
| 0x66 | 6000 | 0.70 | 100 |
| 0x67 | 6000 | 1.00 | 100 |
| 0x68 | 6000 | 1.20 | 100 |
| 0x69 | 6000 | 1.40 | 100 |
| 0x6A | 6000 | 1.60 | 100 |
| 0x6B | 6000 | 1.80 | 100 |
| 0x6C | 700 | 0.12 | 20 |
| 0x6D | 700 | 0.15 | 20 |
| 0x6E | 700 | 0.20 | 20 |
| 0x6F | 700 | 0.30 | 20 |
| 0x70 | 700 | 0.40 | 20 |
| 0x71 | 700 | 0.50 | 20 |
| 0x72 | 700 | 0.70 | 20 |
| 0x73 | 700 | 1.00 | 20 |
| 0x74 | 700 | 1.20 | 20 |
| 0x75 | 700 | 1.40 | 20 |
| 0x76 | 700 | 1.60 | 20 |
| 0x77 | 700 | 1.80 | 20 |
| 0x78 | 1000 | 0.12 | 20 |
| 0x79 | 1000 | 0.15 | 20 |
| 0x7A | 1000 | 0.20 | 20 |
| 0x7B | 1000 | 0.30 | 20 |
| 0x7C | 1000 | 0.40 | 20 |
| 0x7D | 1000 | 0.50 | 20 |
| 0x7E | 1000 | 0.70 | 20 |
| 0x7F | 1000 | 1.00 | 20 |
| 0x80 | 1000 | 1.20 | 20 |
| 0x81 | 1000 | 1.40 | 20 |
| 0x82 | 1000 | 1.60 | 20 |
| 0x83 | 1000 | 1.80 | 20 |
| 0x84 | 1500 | 0.12 | 20 |
| 0x85 | 1500 | 0.15 | 20 |
| 0x86 | 1500 | 0.20 | 20 |
| 0x87 | 1500 | 0.30 | 20 |
| 0x88 | 1500 | 0.40 | 20 |
| 0x89 | 1500 | 0.50 | 20 |
| 0x8A | 1500 | 0.70 | 20 |
| 0x8B | 1500 | 1.00 | 20 |
| 0x8C | 1500 | 1.20 | 20 |
| 0x8D | 1500 | 1.40 | 20 |
| 0x8E | 1500 | 1.60 | 20 |
| 0x8F | 1500 | 1.80 | 20 |
| 0x90 | 2000 | 0.12 | 20 |
| 0x91 | 2000 | 0.15 | 20 |
| 0x92 | 2000 | 0.20 | 20 |
| 0x93 | 2000 | 0.30 | 20 |
| 0x94 | 2000 | 0.40 | 20 |
| 0x95 | 2000 | 0.50 | 20 |
| 0x96 | 2000 | 0.70 | 20 |
| 0x97 | 2000 | 1.00 | 20 |
| 0x98 | 2000 | 1.20 | 20 |
| 0x99 | 2000 | 1.40 | 20 |
| 0x9A | 2000 | 1.60 | 20 |
| 0x9B | 2000 | 1.80 | 20 |
| 0x9C | 3000 | 0.12 | 20 |
| 0x9D | 3000 | 0.15 | 20 |
| 0x9E | 3000 | 0.20 | 20 |
| 0x9F | 3000 | 0.30 | 20 |
| 0xA0 | 3000 | 0.40 | 20 |
| 0xA1 | 3000 | 0.50 | 20 |
| 0xA2 | 3000 | 0.70 | 20 |
| 0xA3 | 3000 | 1.00 | 20 |
| 0xA4 | 3000 | 1.20 | 20 |
| 0xA5 | 3000 | 1.40 | 20 |
| 0xA6 | 3000 | 1.60 | 20 |
| 0xA7 | 3000 | 1.80 | 20 |
| 0xA8 | 4000 | 0.12 | 20 |
| 0xA9 | 4000 | 0.15 | 20 |
| 0xAA | 4000 | 0.20 | 20 |
| 0xAB | 4000 | 0.30 | 20 |
| 0xAC | 4000 | 0.40 | 20 |
| 0xAD | 4000 | 0.50 | 20 |
| 0xAE | 4000 | 0.70 | 20 |
| 0xAF | 4000 | 1.00 | 20 |
| 0xB0 | 4000 | 1.20 | 20 |
| 0xB1 | 4000 | 1.40 | 20 |
| 0xB2 | 4000 | 1.60 | 20 |
| 0xB3 | 4000 | 1.80 | 20 |
| 0xB4 | 700 | 0.12 | 0 |
| 0xB5 | 700 | 0.15 | 0 |
| 0xB6 | 700 | 0.20 | 0 |
| 0xB7 | 700 | 0.30 | 0 |
| 0xB8 | 700 | 0.40 | 0 |
| 0xB9 | 700 | 0.50 | 0 |
| 0xBA | 700 | 0.70 | 0 |
| 0xBB | 700 | 1.00 | 0 |
| 0xBC | 700 | 1.20 | 0 |
| 0xBD | 700 | 1.40 | 0 |
| 0xBE | 700 | 1.60 | 0 |
| 0xBF | 700 | 1.80 | 0 |
| 0xC0 | 1000 | 0.12 | 0 |
| 0xC1 | 1000 | 0.15 | 0 |
| 0xC2 | 1000 | 0.20 | 0 |
| 0xC3 | 1000 | 0.30 | 0 |
| 0xC4 | 1000 | 0.40 | 0 |
| 0xC5 | 1000 | 0.50 | 0 |
| 0xC6 | 1000 | 0.70 | 0 |
| 0xC7 | 1000 | 1.00 | 0 |
| 0xC8 | 1000 | 1.20 | 0 |
| 0xC9 | 1000 | 1.40 | 0 |
| 0xCA | 1000 | 1.60 | 0 |
| 0xCB | 1000 | 1.80 | 0 |
| 0xCC | 2000 | 0.12 | 0 |
| 0xCD | 2000 | 0.15 | 0 |
| 0xCE | 2000 | 0.20 | 0 |
| 0xCF | 2000 | 0.30 | 0 |
| 0xD0 | 2000 | 0.40 | 0 |
| 0xD1 | 2000 | 0.50 | 0 |
| 0xD2 | 2000 | 0.70 | 0 |
| 0xD3 | 2000 | 1.00 | 0 |
| 0xD4 | 2000 | 1.20 | 0 |
| 0xD5 | 2000 | 1.40 | 0 |
| 0xD6 | 2000 | 1.60 | 0 |
| 0xD7 | 2000 | 1.80 | 0 |
| 0xD8 | 3000 | 0.12 | 0 |
| 0xD9 | 3000 | 0.15 | 0 |
| 0xDA | 3000 | 0.20 | 0 |
| 0xDB | 3000 | 0.30 | 0 |
| 0xDC | 3000 | 0.40 | 0 |
| 0xDD | 3000 | 0.50 | 0 |
| 0xDE | 3000 | 0.70 | 0 |
| 0xDF | 3000 | 1.00 | 0 |
| 0xE0 | 3000 | 1.20 | 0 |
| 0xE1 | 3000 | 1.40 | 0 |
| 0xE2 | 3000 | 1.60 | 0 |
| 0xE3 | 3000 | 1.80 | 0 |

<a id="table-eisygd-fasta"></a>
### _EISYGD_FASTA

Dimensions: 5 rows × 5 columns

| NR | NKW_WERT | VSE_SPRI_WERT | VSA_SPRI_WERT | WDK_IST_WERT |
| --- | --- | --- | --- | --- |
| 0x00 | 660 | 120.0 | 115.0 | 3.00 |
| 0x01 | 1000 | 100.0 | 90.00 | 8.00 |
| 0x02 | 1500 | 85.00 | 80.00 | 15.0 |
| 0x03 | 3000 | 90.00 | 100.0 | 30.0 |
| 0xFF | 0 | 0 | 0 | 0 |

<a id="table-krann-fasta"></a>
### _KRANN_FASTA

Dimensions: 7 rows × 4 columns

| NR | NKW_WERT | RF_WERT | TANS_WERT |
| --- | --- | --- | --- |
| 0x00 | 1000 | 60 | 30 |
| 0x01 | 2000 | 85 | 30 |
| 0x02 | 2500 | 40 | 30 |
| 0x03 | 2900 | 85 | 30 |
| 0x04 | 5000 | 80 | 30 |
| 0x05 | 6000 | 80 | 30 |
| 0xFF | 0 | 0 | 0 |

<a id="table-klann-fasta"></a>
### _KLANN_FASTA

Dimensions: 12 rows × 4 columns

| NR | NKW_LOC_WERT | RK_LOC_WERT | TMOT_LOC_WERT |
| --- | --- | --- | --- |
| 0x00 | 700 | 0.10 | 100 |
| 0x01 | 3000 | 0.10 | 100 |
| 0x02 | 3000 | 0.70 | 100 |
| 0x03 | 1500 | 0.70 | 100 |
| 0x04 | 5000 | 1.00 | 100 |
| 0x05 | 5000 | 1.70 | 100 |
| 0x06 | 800 | 0.20 | 20 |
| 0x07 | 1000 | 0.60 | 20 |
| 0x08 | 2000 | 0.80 | 20 |
| 0x09 | 800 | 0.40 | 0 |
| 0x0A | 1500 | 1.00 | 0 |
| 0xFF | 0 | 0 | 0 |

<a id="table-t-ba-ist-nn"></a>
### T_BA_IST_NN

Dimensions: 5 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Keine |
| 1 | Schicht |
| 2 | Homogen |
| 3 | Homogen_Schicht |
| 8 | Notlauf |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 13 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxx0 | 10 | Diagnose läuft nicht |
| xxxxxxx1 | 11 | Diagnose läuft |
| xxxxxx0x | 20 | Diagnose nicht für Fahrzyklus unterbrochen |
| xxxxxx1x | 21 | Diagnose für Fahrzyklus unterbrochen |
| xxxxx0xx | 30 | Zyklus-Flag nicht gesetzt |
| xxxxx1xx | 31 | Zyklus-Flag gesetzt |
| xxxx0xxx | 40 | kein Fehler durch Tester |
| xxxx1xxx | 41 | Fehler durch Tester |
| xxx0xxxx | 50 | MIL aus |
| xxx1xxxx | 51 | MIL ein |
| xx0xxxxx | 60 | Fehler in Entprellphase |
| xx1xxxxx | 61 | Fehler entprellt, keine Scan Tool Ausgabe |
| xxxxxxxx | 0 | -- |

<a id="table-t-1bit-switch-position-high-byte-bit4-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Lambdaregelung vor Katalysator Bank 2 nicht aktiv |
| 1 | Lambdaregelung vor Katalysator Bank 2 aktiv |

<a id="table-t-1bit-fs-erw-lr-aus-bit3-dop"></a>
### T_1BIT_FS_ERW_LR_AUS_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 3 - Open Loop - Fehler erkannt |
| 1 | Bit 3 - Open Loop - Fehler erkannt |

<a id="table-t-st-atlsvc-pvdk-dop"></a>
### T_ST_ATLSVC_PVDK_DOP

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Ladedruckdiagnose ohne Ergebnis |
| 1 | Ladedruck fehlerfrei |
| 2 | Gesamtladedruck zu niedrig |
| 3 | Turbolader 1 mit Ladedruckfehler |
| 4 | Turbolader 2 mit Ladedruckfehler |
| 5 | Gesamtladedruck zu niedrig, Bank nicht identifiziert |

<a id="table-t-1bit-state-ready-obd-2-bit2-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-switch-position-low-byte-bit2-dop"></a>
### T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Kickdown erkannt |
| 1 | Kickdown erkannt |

<a id="table-t-1bit-fs-erw-lr-aus-bit4-dop"></a>
### T_1BIT_FS_ERW_LR_AUS_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 4 - Closed Loop - Min. eine Lambdasonde fehlerhaft. U.u. in Einzelbetrieb |
| 1 | Bit 4 - Closed Loop - Min. eine Lambdasonde fehlerhaft. U.u. in Einzelbetrieb |

<a id="table-t-1bit-glf-high-byte-bit0-dop"></a>
### T_1BIT_GLF_HIGH_BYTE_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Systemtest noch nicht gestartet bzw. noch nicht beendet |
| 1 | gesteuerte Luftfuehrung, Systemtest beendet |

<a id="table-t-1bit-glf-low-byte-bit2-dop"></a>
### T_1BIT_GLF_LOW_BYTE_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, untere Luftklappe nicht verbaut |
| 1 | gesteuerte Luftfuehrung, untere Luftklappe verbaut |

<a id="table-t-1bit-state-ready-obd-1-bit6-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-switch-position-bit2-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kupplung aus |
| 1 | Kupplung ein |

<a id="table-t-1bit-state-ready-obd-1-bit0-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-glf-low-byte-bit7-dop"></a>
### T_1BIT_GLF_LOW_BYTE_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, kein Systemtest aktiv (Normalbetrieb) |
| 1 | gesteuerte Luftfuehrung, Systemtest aktiv |

<a id="table-t-1bit-c-state-ready-obd-2-bit2-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-fs-erw-vvtl-bit4-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 4 - Fehler zulaessige Hoechstzeit Anschlaglernvorgang ueberschritten |
| 1 | Bit 4 - Fehler zulaessige Hoechstzeit Anschlaglernvorgang ueberschritten |

<a id="table-t-1bit-fs-erw-lr-aus-bit2-dop"></a>
### T_1BIT_FS_ERW_LR_AUS_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 2 - Open Loop - Keine Regelung durch Fahrzustand. Gemisch zu fett/mager |
| 1 | Bit 2 - Open Loop - Keine Regelung durch Fahrzustand. Gemisch zu fett/mager |

<a id="table-t-1bit-state-ready-obd-1-bit4-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-fs-erw-vvtl-bit5-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 5 - Fehler Spannungsversorgung |
| 1 | Bit 5 - Fehler Spannungsversorgung |

<a id="table-t-1bit-glf-high-byte-bit4-dop"></a>
### T_1BIT_GLF_HIGH_BYTE_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Testeransteuerung untere Luftklappe nicht aktiv |
| 1 | gesteuerte Luftfuehrung, Testeransteuerung untere Luftklappe aktiv |

<a id="table-t-1bit-c-state-ready-obd-2-bit6-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-c-state-ready-obd-2-bit4-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-state-dmtl-dop"></a>
### T_STATE_DMTL_DOP

Dimensions: 21 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 00 | START |
| 01 | Referenzleck Messung |
| 02 | Grobleck Messung |
| 03 | Feinleck Messung |
| 04 | Zweite Referenzleck Messung |
| 06 | Diagnose beendet |
| 10 | Funktion nicht startbar |
| 11 | Batteriespannnug ausserhalb Bereich |
| 12 | Schwankung vom Referenzstrom zu groß |
| 13 | Elektrischer Fehler vorhanden |
| 14 | Max. Diagnosezeit erreicht |
| 15 | Keine Freigabe TEV aktiv |
| 20 | Funktion wurde abgebrochen |
| 23 | Spannungsschwankung zu groß |
| 24 | Zündung an |
| 30 | Funktion beendet: Tank dicht |
| 31 | Funktion beendet: Feinleck erkannt |
| 32 | Funktion beendet: Grobleck erkannt |
| 33 | Funktion beendet: Modulfehler |
| 34 | Funktion beendet: Kein Grobleck erkannt |
| 255 | Funktion noch nicht gestartet |

<a id="table-t-1bit-state-ready-obd-2-bit7-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-switch-position-bit0-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Klemme-15 aus |
| 1 | Klemme-15 ein |

<a id="table-t-st-atlsvc-dop"></a>
### T_ST_ATLSVC_DOP

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Startbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 5 | Funktionstest laeuft |
| 6 | Funktion beendet |
| 7 | Funktion abgebrochen |
| 8 | Funktion vollstaendig durchlaufen und kein Fehler erkannt |
| 9 | Funktion vollstaendig durchlaufen und Fehler erkannt |

<a id="table-t-1bit-switch-position-bit3-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bremslichtschalter-Kanal 1 aus |
| 1 | Bremslichtschalter-Kanal 1 ein |

<a id="table-t-1bit-c-state-ready-obd-2-bit7-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-switch-position-high-byte-bit6-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Regelkreis Bank 2 nicht geschlossen |
| 1 | Regelkreis Bank 2 geschlossen |

<a id="table-t-b-vvtnotl-dop"></a>
### T_B_VVTNOTL_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | 0 |
| 1 | 1 |

<a id="table-t-1bit-switch-position-high-byte-bit7-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Regelkreis Bank 1 nicht geschlossen |
| 1 | Regelkreis Bank 1 geschlossen |

<a id="table-t-b-msrdkad-dop"></a>
### T_B_MSRDKAD_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Massestromregler auf DK nicht erfolgt |
| 1 | Massestromregler auf DK erstmalig erfolgt |

<a id="table-t-1bit-switch-position-high-byte-bit0-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Leerlauf |
| 1 | Leerlauf |

<a id="table-t-1bit-switch-position-low-byte-bit7-dop"></a>
### T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Drosselklappen-Neuabgleich erforderlich |
| 1 | Drosselklappen-Neuabgleich nicht erforderlich |

<a id="table-t-1bit-fs-erw-vvtl-bit7-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 7 - Ruecknahme Lernanforderung |
| 1 | Bit 7 - Ruecknahme Lernanforderung |

<a id="table-t-1bit-state-ready-obd-2-bit4-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-fs-erw-vvtl-bit3-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 3 - Fehler Verstellbereich Referenzsensor unplausibel |
| 1 | Bit 3 - Fehler Verstellbereich Referenzsensor unplausibel |

<a id="table-t-1bit-glf-low-byte-bit5-dop"></a>
### T_1BIT_GLF_LOW_BYTE_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | obere Luftklappe, kein Fehler durch Eigendiagnose erkannt |
| 1 | obere Luftklappe, Fehler durch Eigendiagnose erkannt |

<a id="table-t-1bit-glf-low-byte-bit4-dop"></a>
### T_1BIT_GLF_LOW_BYTE_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, kein elektrischer Fehler |
| 1 | gesteuerte Luftfuehrung, elektrischer Fehler |

<a id="table-t-b-kuppl-dop"></a>
### T_B_KUPPL_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | 0 |
| 1 | 1 |

<a id="table-t-eol-ram-1-dop"></a>
### T_EOL_RAM_1__DOP

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Startbedingungen nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | Undefinierter Zustand |
| 5 | Funktionstest laeuft |
| 6 | Funktion ergebnislos beendet |
| 7 | Funktion abgebrochen |
| 8 | Funktion durchlaufen und kein Fehler erkannt |
| 9 | Funktion durchlaufen und Fehler erkannt |

<a id="table-t-1bit-switch-position-bit4-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bremslichtschalter-Kanal 2 aus |
| 1 | Bremslichtschalter-Kanal 2 ein |

<a id="table-t-1bit-glf-low-byte-bit0-dop"></a>
### T_1BIT_GLF_LOW_BYTE_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Varianten lernen noch nicht abgeschlossen |
| 1 | Varianten haetten gelernt werden koennen |

<a id="table-t-st-testpoelsys2-dop"></a>
### T_ST_TESTPOELSYS2_DOP

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | -- |
| 1 | Abbruch durch Tester |
| 2 | Warmlauf (Oeltemperatur zu niedrig) |
| 3 | Abbruch aufgrund zu hoher Oeltemperatur |
| 4 | Abbruch aufgrund fehlender Reglerfreigabe |
| 5 | Abbruch der Diagnosefunktion nach Schritt 1 (Fehlerspeicher auslesen) |
| 6 | Abbruch der Diagnosefunktion nach Schritt 2 (Fehlerspeicher auslesen) |
| 7 | Abbruch der Diagnosefunktion nach Schritt 3 (Fehlerspeicher auslesen) |
| 8 | Testfunktion 1 laeuft (konstante Drehzahl, Solldruck-Spruenge) |
| 9 | Testfunktion 2 laeuft (konstante Drehzahl, Solldruck-Rampen) |
| 10 | Testfunktion 3 laeuft (Drehzahl-Rampen, konstanter Solloeldruck) |

<a id="table-t-1bit-glf-high-byte-bit6-dop"></a>
### T_1BIT_GLF_HIGH_BYTE_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Kommunikation noch nicht getestet |
| 1 | gesteuerte Luftfuehrung, Kommunikation in Ordnung |

<a id="table-t-vvtchksf1-fs-dop"></a>
### T_VVTCHKSF1_FS_DOP

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Keine Testeranforderung vorhanden. |
| 1 | Startbedingungen nicht erfüllt (Motorlauf). |
| 2 | nicht belegt |
| 3 | nicht belegt |
| 4 | nicht belegt |
| 5 | Lernvorgang aktiv. |
| 6 | nicht belegt |
| 7 | Abbruch durch Motorlauf, Fehler im VVT-System, Rücknahme Lernanforderung. |
| 8 | Lernvorgang ohne Fehler beendet. |
| 9 | Lernvorgang mit aufgetretenem Fehler beendet. |

<a id="table-t-1bit-state-ready-obd-2-bit3-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-glf-high-byte-bit5-dop"></a>
### T_1BIT_GLF_HIGH_BYTE_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Testeransteuerung obere Luftklappe nicht aktiv |
| 1 | gesteuerte Luftfuehrung, Testeransteuerung obere Luftklappe aktiv |

<a id="table-t-1bit-fs-erw-vvtl-bit6-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 6 - Fehler VVT-Sensor, Leistungsversorgung oder Stellglied |
| 1 | Bit 6 - Fehler VVT-Sensor, Leistungsversorgung oder Stellglied |

<a id="table-t-1bit-fs-erw-vvtl-bit1-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 1 - Fehler oberer Anschlag nicht gefunden |
| 1 | Bit 1 - Fehler oberer Anschlag nicht gefunden |

<a id="table-t-1bit-state-ready-obd-2-bit1-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-c-state-ready-obd-2-bit1-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-state-ready-obd-1-bit2-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-fs-erw-lr-aus-bit0-dop"></a>
### T_1BIT_FS_ERW_LR_AUS_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 0 - Open Loop - Start-/Ansteuerbedingung für Regelung nicht erfüllt |
| 1 | Bit 0 - Open Loop - Start-/Ansteuerbedingung für Regelung nicht erfüllt |

<a id="table-t-1bit-state-ready-obd-2-bit5-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-switch-position-bit1-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Motor steht |
| 1 | Motor laeuft |

<a id="table-t-1bit-state-ready-obd-2-bit6-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-c-state-ready-obd-2-bit3-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1byte-fs-glf-dop"></a>
### T_1BYTE_FS_GLF_DOP

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Funktion laeuft |
| 1 | Start-/Ansteuerbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktion noch nicht gestartet |
| 6 | Funktion beendet (ohne Ergebnis) |
| 7 | Funktion abgebrochen (kein Zyklusflag/Readiness gesetzt) |
| 8 | Funktion vollstaendig durchlaufen (Zyklusflag/Readiness gesetzt) und kein Fehler erkannt |
| 9 | Funktion vollstaendig durchlaufen (Zyklusflag/Readiness gesetzt) und Fehler erkannt |
| 255 | ungueltiger Wert |

<a id="table-t-1bit-c-state-ready-obd-2-bit5-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-b-standard-1byte-lesen-0-1"></a>
### T_B_STANDARD_1BYTE_LESEN_0_1

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | 0 |
| 1 | 1 |
| 2 | Groesser 1 |

<a id="table-t-1bit-c-state-ready-obd-2-bit0-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1byte-fs-dop"></a>
### T_1BYTE_FS_DOP

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Start-/Ansteuerbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktion laeuft |
| 6 | Funktion beendet (ohne Ergebnis) |
| 7 | Funktion abgebrochen (kein Zyklusflag/Readiness gesetzt) |
| 8 | Funktion vollstaendig durchlaufen (Zyklusflag/Readiness gesetzt) und kein Fehler erkannt |
| 9 | Funktion vollstaendig durchlaufen (Zyklusflag/Readiness gesetzt) und Fehler erkannt |
| 255 | ungueltiger Wert |

<a id="table-t-b-msrhubad-dop"></a>
### T_B_MSRHUBAD_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Massestromregler auf Hub nicht erfolgt |
| 1 | Massestromregler auf Hub erstmalig erfolgt |

<a id="table-t-1bit-glf-high-byte-bit7-dop"></a>
### T_1BIT_GLF_HIGH_BYTE_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, kein Fehler erkannt |
| 1 | gesteuerte Luftfuehrung, Fehler erkannt |

<a id="table-t-1bit-switch-position-low-byte-bit3-dop"></a>
### T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Gang nicht eingelegt, Park- oder Neutralstellung |
| 1 | Gang eingelegt, nicht Park- oder Neutralstellung |

<a id="table-t-1bit-state-ready-obd-1-bit1-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-glf-high-byte-bit1-dop"></a>
### T_1BIT_GLF_HIGH_BYTE_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, elektrische Diagnose noch nicht beendet |
| 1 | gesteuerte Luftfuehrung, elektrische Diagnose beendet |

<a id="table-t-1bit-state-ready-obd-1-bit5-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-fs-erw-vvtl-bit0-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 0 - Fehler unterer Anschlag nicht gefunden |
| 1 | Bit 0 - Fehler unterer Anschlag nicht gefunden |

<a id="table-t-1bit-switch-position-high-byte-bit3-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Lambdaregelung hinter Katalysator Bank 2 nicht aktiv |
| 1 | Lambdaregelung hinter Katalysator Bank 2 aktiv |

<a id="table-t-1bit-fs-erw-lr-aus-bit1-dop"></a>
### T_1BIT_FS_ERW_LR_AUS_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 1 - Closed Loop - Lambdaregelung-Diagnose |
| 1 | Bit 1 - Closed Loop - Lambdaregelung-Diagnose |

<a id="table-t-1bit-switch-position-bit7-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Anforderung Klimabereitschaft aus |
| 1 | Anforderung Klimabereitschaft ein |

<a id="table-t-s-vsmnhb-dop"></a>
### T_S_VSMNHB_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | 0 |
| 128 | 1 |

<a id="table-t-1bit-fs-erw-vvtl-bit2-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 2 - Fehler Verstellbereich Fuehrungssensor unplausibel |
| 1 | Bit 2 - Fehler Verstellbereich Fuehrungssensor unplausibel |

<a id="table-t-1bit-switch-position-low-byte-bit6-dop"></a>
### T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Schubabschaltung aktiv |
| 1 | Schubabschaltung aktiv |

<a id="table-t-1bit-glf-low-byte-bit3-dop"></a>
### T_1BIT_GLF_LOW_BYTE_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Fehlerabfrage aktiv, Verstellung moeglich (Normalbetrieb) |
| 1 | Fehlerabfrage aktiv, keine Verstellung moeglich |

<a id="table-t-1bit-glf-high-byte-bit3-dop"></a>
### T_1BIT_GLF_HIGH_BYTE_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Eigendiagnose untere Luftklappe noch nicht beendet |
| 1 | gesteuerte Luftfuehrung, Eigendiagnose untere Luftklappe beendet |

<a id="table-t-1bit-switch-position-high-byte-bit1-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Vollast |
| 1 | Vollast |

<a id="table-t-1bit-glf-high-byte-bit2-dop"></a>
### T_1BIT_GLF_HIGH_BYTE_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Eigendiagnose obere Luftklappe noch nicht beendet |
| 1 | gesteuerte Luftfuehrung, Eigendiagnose obere Luftklappe beendet |

<a id="table-t-1bit-state-ready-obd-2-bit0-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-switch-position-high-byte-bit5-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Lambdaregelung vor Katalysator Bank 1 nicht aktiv |
| 1 | Lambdaregelung vor Katalysator Bank 1 aktiv |

<a id="table-t-st-testpoelsys-dop"></a>
### T_ST_TESTPOELSYS_DOP

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktionstest laeuft |
| 6 | Funktion beendet |
| 7 | Funktion abgebrochen |
| 8 | Funktion vollstaendig durchlaufen und kein Fehler erkannt |
| 9 | Funktion vollstaendig durchlaufen und Fehler erkannt |

<a id="table-t-1bit-glf-low-byte-bit1-dop"></a>
### T_1BIT_GLF_LOW_BYTE_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, obere Luftklappe nicht verbaut |
| 1 | gesteuerte Luftfuehrung, obere Luftklappe verbaut |

<a id="table-t-ba-ist-dop"></a>
### T_BA_IST_DOP

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Keine |
| 1 | Schicht |
| 2 | Homogen |
| 3 | Homogen_Schicht |
| 8 | Notlauf |

<a id="table-t-1bit-switch-position-high-byte-bit2-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Lambdaregelung hinter Katalysator Bank 1 nicht aktiv |
| 1 | Lambdaregelung hinter Katalysator Bank 1 aktiv |

<a id="table-t-1bit-glf-low-byte-bit6-dop"></a>
### T_1BIT_GLF_LOW_BYTE_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | untere Luftklappe, kein Fehler durch Eigendiagnose erkannt |
| 1 | untere Luftklappe, Fehler durch Eigendiagnose erkannt |
