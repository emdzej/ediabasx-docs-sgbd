# IHKA70.prg

- Jobs: [116](#jobs)
- Tables: [39](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | IHKA |
| ORIGIN | BMW EI-63 Adam |
| REVISION | 2.002 |
| AUTHOR | Preh TES Rüdiger Arnold, Preh TES Hatim Merzouki, Preh TES Matthias Leichsenring |
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
- [STEUERN_EINZELADRESSIERUNG](#job-steuern-einzeladressierung) - Startet die LIN-Bus Einzeladressierung KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - Auslesen der Klappenpositionen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - Auslesen des aktuell eingestellten Energiesparmodes KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STEUERN_GEBLAESE](#job-steuern-geblaese) - Ansteuern des Geblaeses im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default Vor dem Ansteuern den Job DIAGNOSE_TESTBIT mit dem Parameter "ein" aufrufen Für die Rückkehr in die geregelte Ansteuerung den Job DIAGNOSE_TESTBIT "aus" aufrufen
- [STEUERN_MOTOREN](#job-steuern-motoren) - Ansteuern der Klappen im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default Vor dem Ansteuern den Job DIAGNOSE_TESTBIT mit dem Parameter "ein" aufrufen Für die Rückkehr in die geregelte Ansteuerung den Job DIAGNOSE_TESTBIT "aus" aufrufen
- [DIAGNOSE_TESTBIT](#job-diagnose-testbit) - Ansteuern des Diagnosetest-Bits Das Bit kann ein- bzw. ausgeschaltet werden. STEUERN-Befehle werden nur bei gesetztem Testbit wirksam die Ansteuerung bleibt so lange erhalten, wie das Testbit gesetzt ist das Testbit wird nur durch einen Steuergerätereset geloescht
- [STEUERN_BEDIENTEIL_POTIS](#job-steuern-bedienteil-potis) - Simulieren von Verstellungen der Potentiometer am Bedienteil KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STATUS_BEDIENTEIL](#job-status-bedienteil) - Auslesen der Bedienteileinstellungen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STEUERN_BEDIENTEIL_TASTEN](#job-steuern-bedienteil-tasten) - Simulieren von Tastenbetaetigungen am Bedienteil KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STATUS_TASTEN_LESEN](#job-status-tasten-lesen) - Auslesen der aktuellen Tastenstellungen
- [STATUS_LEDS_LESEN](#job-status-leds-lesen) - Auslesen der aktuell aktuell angesteuerten LED's am Bedienteil
- [STATUS_SZM](#job-status-szm) - Auslesen aller SZM-Parameter
- [STEUERN_SZM_TASTEN](#job-steuern-szm-tasten) - Simulieren von Tastenbetaetigungen am Bedienteil KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STATUS_ANALOGEINGAENGE](#job-status-analogeingaenge) - Auslesen der 16 A/D-Werte (High/Basis) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_LSV_HAL_INPUT](#job-status-lsv-hal-input) - Auslesen der LSV-Hallsensoren zur Erkennung von Softstops KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState
- [STEUERN_MOTOREN_EICHLAUF](#job-steuern-motoren-eichlauf) - Löst Klappeneichlauf aus und kalibriert die Schrittzahlen neu KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_RESET_LIN](#job-steuern-reset-lin) - Löst Rücksetzen des LIN-Bus (Versorgung) aus KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_MOTOR_FEHLER_LOESCHEN](#job-steuern-motor-fehler-loeschen) - Löscht Zähler für Motorfehler KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STATUS_MOTOR_IDENT](#job-status-motor-ident) - Liefert die Identdaten des jeweiligen LIN-Bus-Schrittmotors KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_KLIMASYSTEM](#job-status-klimasystem) - Lesen aller ansprechbaren Adressen des LIN-Bus-Systems KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STEUERN_SOLLWERT_PTC](#job-steuern-sollwert-ptc) - Ansteuern des Ptc-Sollwertes im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default Vor dem Ansteuern den Job DIAGNOSE_TESTBIT mit dem Parameter "ein" aufrufen Für die Rückkehr in die geregelte Ansteuerung den Job DIAGNOSE_TESTBIT "aus" aufrufen
- [STEUERN_SELBSTTEST_SCHRITTMOTORE](#job-steuern-selbsttest-schrittmotore) - Alle Stellmotore auf 50 % verfahren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STATUS_SELBSTTEST_SCHRITTMOTORE](#job-status-selbsttest-schrittmotore) - Prüfen Selbsttest der Schrittmotoren KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STEUERN_AUTOADRESSIERUNG](#job-steuern-autoadressierung) - Startet die LIN-Bus Autoadressierung KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
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
- [STATUS_MOTOR_FEHLER](#job-status-motor-fehler) - Auslesen der Zähler für Lin-Motoren-Fehler KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STEUERN_KOMPRESSOR_EINLAUFSCHUTZ](#job-steuern-kompressor-einlaufschutz) - Setzen/Löschen des Kompressor Einlaufschutzes KWP2000: $30 InputOutputControlByLocalIdentifier $42 Kompressor Einlaufschutz (recordLocalIdentifier) $0x Ein/Aus (recordValue#1) Modus  : Default
- [STATUS_TIMER_EINLAUFSCHUTZ](#job-status-timer-einlaufschutz) - Lesen des Status des Kompressor-Einlaufschutzes KWP2000: $30 InputOutputControlByLocalIdentifier $43 Timer Kompressor Einlaufschutz Modus  : Default
- [STATUS_FASTA_BLOCK](#job-status-fasta-block) - Aktueller Wert des FASTA-Blocks
- [STEUERN_LHZ_ZUSTAND](#job-steuern-lhz-zustand) - Steuern des Lenkradheizungszustand im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default Vor dem Ansteuern den Job DIAGNOSE_TESTBIT mit dem Parameter "ein" aufrufen Für die Rückkehr in die geregelte Ansteuerung den Job DIAGNOSE_TESTBIT "aus" aufrufen
- [STATUS_ELSV](#job-status-elsv) - Auslesen der Stati der Lenksaeulen-Komponente KWP2000: $30 InputOutputControlByLocalIdentifier $65 ReportCurrentState Modus  : Default
- [STEUERN_ELSV](#job-steuern-elsv) - Steuern der Lenksaeule im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_ELSV_NORMIERUNG](#job-steuern-elsv-normierung) - Steuern des Lenksaeule im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STEUERN_ELSV_MEMORY](#job-steuern-elsv-memory) - Memoryabruf KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [STATUS_ELSV_MEMORY](#job-status-elsv-memory) - Gibt die unter der Memory-Position gespeicherten Werte für Laenge und Neigung zurueck KWP2000: $30 InputOutputControlByLocalIdentifier $69 ReportCurrentState Modus  : Default
- [STATUS_ELSV_STATISTIK](#job-status-elsv-statistik) - Gibt die unter der Memory-Position gespeicherten Werte für Laenge und Neigung zurueck KWP2000: $30 InputOutputControlByLocalIdentifier $6A ReportCurrentState Modus  : Default
- [STATUS_MOTOR_SCHRITTZAHLEN](#job-status-motor-schrittzahlen) - Auslesen der vermessenen Schrittzahlen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STEUERN_FREIGABE_PTC_3SITZR](#job-steuern-freigabe-ptc-3sitzr) - Setzen/Löschen Freigabe Ptc 3. Sitzreihe KWP2000: $30 InputOutputControlByLocalIdentifier $34 Freigabe Ptc 3. Sitzreihe (recordLocalIdentifier) $0x Ein/Aus (recordValue#1) Modus  : Default

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
| AVAI_CBS_WERT_DAD | int | Verfuegbarkeit DAD in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_ZKRZ_A | int | Verfuegbarkeit ZKRZ_A in %, fuer Pruefablauf Bandende |
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
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, ZKrz, Sic, Kfl, TUV, AU, Ueb Werte externe Umfaenge: Oel, Br_v, Br_h, Filt, CSF, Batt, VTG, ZKrz_a, DAD Defaultwert: 0x00 (ungueltig) |
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

<a id="job-steuern-einzeladressierung"></a>
### STEUERN_EINZELADRESSIERUNG

Startet die LIN-Bus Einzeladressierung KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CURRENT_STEPPER_ADDRESS | unsigned char | Aktuelle Adresse des zu programmierenden Motors Wenn keine Eingabe: default = 0x3F |
| NEW_STEPPER_ADDRESS | unsigned char | Neue Adresse des zu programmierenden Motors zwischen 0x21 und 0x2D Wenn keine Eingabe: default = 0x3F |
| DIRECTION | unsigned char | Laufrichtung des zu programmierenden Motors 0x00 = Laufrichtung im Uhrzeigersinn für steigende Schrittzahlen 0x01 = Laufrichtung gegen den Uhrzeigersinn für steigende Schrittzahlen 0xFF = Laufrichtung wie aktuelle Motorprogrammierung Wenn keine Eingabe: default = 0xFF |
| SAFETY_ENABLE | unsigned char | Notlaufaktivierung des zu programmierenden Motors 0x00 = Notlauf aktiviert 0x01 = Notlauf deaktiviert 0xFF = Notlauf wie aktuelle Motorprogrammierung Wenn keine Eingabe: default = 0xFF |
| SAFETY_DIRECTION | unsigned char | Notlaufendposition des zu programmierenden Motors 0x00 = Zu niedrigen Schrittzahlen 0x01 = Zu hohen Schrittzahlen 0xFF = Notlaufendposition wie aktuelle Motorprogrammierung Wenn keine Eingabe: default  = 0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-klappenposition"></a>
### STATUS_MOTOR_KLAPPENPOSITION

Auslesen der Klappenpositionen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOTOR_EINH | string | 0 - 100% wenn verbaut, 255 wenn nicht verbaut alle Motoreinheiten |
| STAT_FRISCHLUFT_UMLUFT_WERT | int | Klappenöffnung FL/Umluft-Klappe |
| STAT_STAUDRUCK_WERT | int | Klappenöffnung Staudruck-Klappe |
| STAT_DEFROST_WERT | int | Klappenöffnung DefrostKlappe |
| STAT_BELUEFTUNG_LI_WERT | int | Klappenöffnung Belüftungsklappe links |
| STAT_BELUEFTUNG_RE_WERT | int | Klappenöffnung Belüftungsklappe rechts |
| STAT_SCHICHTUNG_LI_WERT | int | Klappenöffnung Schichtungsklappe links |
| STAT_SCHICHTUNG_RE_WERT | int | Klappenöffnung Schichtungsklappe rechts |
| STAT_FUSSRAUM_LI_WERT | int | Klappenöffnung Fußraumklappe links |
| STAT_FUSSRAUM_RE_WERT | int | Klappenöffnung Fußraumklappe rechts |
| STAT_FUSS_FOND_LI_WERT | int | Klappenöffnung Fondfußraumklappe links |
| STAT_FUSS_FOND_RE_WERT | int | Klappenöffnung Fondfußraumklappe rechts |
| STAT_SCHICHT_FOND_LI_WERT | int | Klappenöffnung Fondschichtungsklappe links |
| STAT_SCHICHT_FOND_RE_WERT | int | Klappenöffnung Fondschichtungsklappe rechts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmode"></a>
### STATUS_ENERGIESPARMODE

Auslesen des aktuell eingestellten Energiesparmodes KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TRANSPORTMODE_WERT | int | Status Transportmode |
| STAT_WERKSTATTMODE_WERT | int | Status Werkstattmode |
| STAT_FERTIGUNGSMODE_WERT | int | Status Fertigungsmode |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-geblaese"></a>
### STEUERN_GEBLAESE

Ansteuern des Geblaeses im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default Vor dem Ansteuern den Job DIAGNOSE_TESTBIT mit dem Parameter "ein" aufrufen Für die Rückkehr in die geregelte Ansteuerung den Job DIAGNOSE_TESTBIT "aus" aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GEBLAESE | int | Geblaese-Ansteuerung in Prozentschritten 0, 20-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motoren"></a>
### STEUERN_MOTOREN

Ansteuern der Klappen im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default Vor dem Ansteuern den Job DIAGNOSE_TESTBIT mit dem Parameter "ein" aufrufen Für die Rückkehr in die geregelte Ansteuerung den Job DIAGNOSE_TESTBIT "aus" aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLAPPEN_NR | int | HIGH-BEDIENTEIL: Klappennummer im Bereich von 0 bis 13 zulaessig Basis          High 2,5-zonig      High 4-zonig 0 =   Entfrostung    Entfrostung         Entfrostung 1 =   FL/UML         FL/UML              FL/UML 2 =   Staudruck      Staudruck           Staudruck 3 =   Fuss           Fuss rechts         Fuss rechts 4 =   -              Fuss links          Fuss links 5 =   Schichtung     Schichtung links    Schichtung links 6 =   Belueftung     Belueftung links    Belueftung links 7 =   -              Belueftung rechts   Belueftung rechts 8 =                  Schichtung rechts   Schichtung rechts 9 =   -              -                   FondFuss links 10 =   -              -                   FondFuss rechts 11 =   -              Fondschichtung      FondSchichtung links 12 =   -              -                   FondSchichtung rechts |
| KLAPPENOEFFNUNG | int | Klappenansteuerung in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-testbit"></a>
### DIAGNOSE_TESTBIT

Ansteuern des Diagnosetest-Bits Das Bit kann ein- bzw. ausgeschaltet werden. STEUERN-Befehle werden nur bei gesetztem Testbit wirksam die Ansteuerung bleibt so lange erhalten, wie das Testbit gesetzt ist das Testbit wird nur durch einen Steuergerätereset geloescht

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTBIT | string | 'EIN','AUS' table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bedienteil-potis"></a>
### STEUERN_BEDIENTEIL_POTIS

Simulieren von Verstellungen der Potentiometer am Bedienteil KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POTENTIOMETER_LINKS | int | HIGH-BEDIENTEIL: Temperatureinstellung linke Seite Temperatur in Grad Celsius * 2 Gueltige Werte 32 - 56 (entspricht 16 - 28 Grad Celsius in Halbgradschritten)  BASIS-BEDIENTEIL: Geblaeseeinstellung Geblaeseeinstellung in Stufen Gueltige Werte: 0 -&gt; (OFF-Funktion), Stufen 1 - 9 |
| POTENTIOMETER_RECHTS | int | HIGH-BEDIENTEIL: Temperatureinstellung rechte Seite Temperatur in Grad Celsius * 2 Gueltige Werte 32 - 56 (entspricht 16 - 28 Grad Celsius in Halbgradschritten)  BASIS-BEDIENTEIL: Temperatureinstellung Temperatur in Grad Celsius * 2 Gueltige Werte 32 - 56 (entspricht 16 - 28 Grad Celsius in Halbgradschritten) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bedienteil"></a>
### STATUS_BEDIENTEIL

Auslesen der Bedienteileinstellungen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table Job Result STATUS_TEXT |
| STAT_TEMPERATUR_EINH | string | Temperatureinheit in Grad Celsius oder Fahrenheit in Textform |
| STAT_EINHEIT_FAHRENHEIT_AKTIV | int | Temperatureinheit in Grad Celsius oder Fahrenheit als Integer 0 = Grad Celsius, 1 = Grad Fahrenheit |
| STAT_TEMPERATUR_LI_WERT | real | Fuer HIGH-Ausfuehrung: Temperatur links Fuer Basis-Ausfuehrung: Nicht verfuegbar = 255 |
| STAT_TEMPERATUR_RE_WERT | real | Fuer HIGH-Ausfuehrung: Temperatur rechts Fuer Basis-Ausfuehrung: Temperatur |
| STAT_GEBLAESE_WERT | int | Eingestellte Geblaesestufe |
| STAT_GEBLAESE_EINH | string | "Stufe" als Text |
| STAT_PRG_OFF_EIN | int | Status OFF-Programm |
| STAT_PRG_DEFROST_EIN | int | Status DEFROST-Programm |
| STAT_PRG_MAX_AC_EIN | int | Nur bei HIGH-Ausfuehrung 255 = nicht verbaut |
| STAT_PRG_AUC_EIN | int | Nur bei HIGH-Ausfuehrung 255 = nicht verbaut |
| STAT_PRG_UMLUFT_EIN | int | Status UMLUFT-Programm |
| STAT_PRG_HHS_EIN | int | Status HHS-Programm |
| STAT_PRG_REST_EIN | int | Nur bei HIGH-Ausfuehrung 255 = nicht verbaut |
| STAT_PRG_AC_EIN | int | Status AC-Programm |
| STAT_PRG_KLP_AUTO_LI_EIN | int | Fuer HIGH-Ausfuehrung links Fuer Basis nur eine Klappenautomatik |
| STAT_PRG_KLP_AUTO_RE_EIN | int | Nur bei HIGH-Ausfuehrung 255 = nicht verbaut |
| STAT_PRG_GEBL_AUTO_EIN | int | Status Geblaeseautomatik |
| STAT_PRG_LV_LI_TEXT | string | Status Luftverteilungs-Programm links als Text |
| STAT_PRG_LV_LI_NR | int | 1 = "UNTEN", 2 = MITTE",       3 = MITTE_UNTEN",     5 = OBEN_UNTEN" (Nur Fahrer) 8 = AUTO",  32 = INDIVIDUAL", 40 = SONDERPROGRAMM, 255 = "UNGUELTIG" (BASIS) |
| STAT_PRG_LV_RE_TEXT | string | Status Luftverteilungs-Programm rechts als Text |
| STAT_PRG_LV_RE_NR | int | 1 = "UNTEN", 2 = MITTE",       3 = MITTE_UNTEN",     5 = OBEN_UNTEN" (Nur Fahrer) 8 = AUTO",  32 = INDIVIDUAL", 40 = SONDERPROGRAMM, 255 = "UNGUELTIG" (BASIS) |
| STAT_PRG_KLIMASTIL_TEXT | string | Status Klimastil als Text |
| STAT_PRG_KLIMASTIL_NR | int | 1 = "SOFT", 2 = "NORMAL", 3 = "INTENSIV", 255 = "UNGUELTIG" (BASIS) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bedienteil-tasten"></a>
### STEUERN_BEDIENTEIL_TASTEN

Simulieren von Tastenbetaetigungen am Bedienteil KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTEN_NUMMER | int | HIGH-BEDIENTEIL: Tastennummer &gt; 14 und sieben sind zulaessig 0: DEFROST,     1: HHS,          2: AUTO,        3: UMLUFT,            4: KLIMA 5: SH-links,    6: SH-rechts,    8: MAX-AC,      9: Geblaese-Minus,   10: Geblaese-Plus 11: LV-links    12: LV-rechts,   13: SL-links,   14: SL-rechts Bei MAX-AC muß Aussentemperatur groesser Schwelle sein SH und SL muessen codiert sein  BASIS-BEDIENTEIL: Tastennummer &gt; 6 ist unzulaessig 0: DEFROST,   1: HHS,   2: AUTO,   3: UMLUFT,   4: KLIMA,   5: SH-links,   6: SH-rechts SH muss codiert sein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tasten-lesen"></a>
### STATUS_TASTEN_LESEN

Auslesen der aktuellen Tastenstellungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TASTEN_WERT | int | HEX-Wert der betaetigten Taste 0x0001 = "Defrost-Taste",       0x0002 = "HHS-Taste",     0x0004 = "AUTO-Taste" 0x0008 = "UML/(AUC)-Taste",     0x0010 = "Klima-Taste",   0x0020 = "SH-Taste links" 0x0040 = "SH-Taste rechts",     0x0100 = "MAX-AC-Taste",  0x0200 = "Geblaese-Minus-Taste" 0x0400 = "Geblaese-Plus-Taste", 0x0800 = "LV-Taste links, 0x1000 = "LV-Taste rechts" 0x2000 = "SL-Taste links",      0x4000 = "SL-Taste rechts" |
| STAT_TASTEN_TEXT | string | Betaetigte Taste im Klartext |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-leds-lesen"></a>
### STATUS_LEDS_LESEN

Auslesen der aktuell aktuell angesteuerten LED's am Bedienteil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLIMA_LED | int | 0 = LED aus, 1 = LED ein |
| STAT_UMLUFT_LED | int | 0 = LED aus, 1 = LED ein |
| STAT_HHS_LED | int | 0 = LED aus, 1 = LED ein |
| STAT_DEFROST_LED | int | 0 = LED aus, 1 = LED ein |
| STAT_AUTO_LED | int | 0 = LED aus, 1 = LED ein |
| STAT_MAX_AC_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (bei BASIS) |
| STAT_AUC_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (bei BASIS) |
| STAT_LV_RECHTS_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (bei BASIS) |
| STAT_LV_LINKS_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (bei BASIS) |
| STAT_SH_RECHTS_OBEN_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (wenn nicht verbaut/codiert oder SL verbaut/codiert) |
| STAT_SH_RECHTS_MITTE_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (wenn nicht verbaut/codiert oder SL verbaut/codiert) |
| STAT_SH_RECHTS_UNTEN_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (wenn nicht verbaut/codiert) |
| STAT_SH_LINKS_OBEN_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (wenn nicht verbaut/codiert oder SL verbaut/codiert) |
| STAT_SH_LINKS_MITTE_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (wenn nicht verbaut/codiert oder SL verbaut/codiert) |
| STAT_SH_LINKS_UNTEN_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (wenn nicht verbaut/codiert) |
| STAT_SL_RECHTS_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (wenn nicht verbaut/codiert) |
| STAT_SL_LINKS_LED | int | 0 = LED aus, 1 = LED ein, 255 = Ungueltig (wenn nicht verbaut/codiert) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-szm"></a>
### STATUS_SZM

Auslesen aller SZM-Parameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TASTE_AKTIVSITZ_LI_AKTIV | int | 0 = Taste nicht betaetigt, 1 = Taste betaetigt |
| STAT_TASTE_PDC_AKTIV | int | 0 = Taste nicht betaetigt, 1 = Taste betaetigt |
| STAT_TASTE_DSC_OFF_AKTIV | int | 0 = Taste nicht betaetigt, 1 = Taste betaetigt |
| STAT_TASTE_HDC_AKTIV | int | 0 = Taste nicht betaetigt, 1 = Taste betaetigt |
| STAT_TASTE_HKL_AKTIV | int | 0 = Taste nicht betaetigt, 1 = Taste betaetigt |
| STAT_TASTE_JP_CAM_AKTIV | int | 0 = Taste nicht betaetigt, 1 = Taste betaetigt |
| STAT_TASTE_AKTIVSITZ_RE_AKTIV | int | 0 = Taste nicht betaetigt, 1 = Taste betaetigt |
| STAT_LED_AKTIVSITZ_LI_WERT | int | 0 = LED AUS, 1 = LED EIN |
| STAT_LED_PDC_WERT | int | 0 = LED AUS, 1 = LED DAUER-EIN, 2 = LED BLINKT |
| STAT_LED_HDC_WERT | int | 0 = LED AUS, 1 = LED DAUER-EIN, 2 = LED BLINKT |
| STAT_LED_AKTIVSITZ_RE_WERT | int | 0 = LED AUS, 1 = LED EIN |
| STAT_AD_WERT_EINH | string | Volt |
| STAT_AD_WERT_TST_AKTIVSITZ_LI_PDC_WERT | real | Analogwert fuer die Tasten Aktivsitz links und PDC |
| STAT_AD_WERT_TST_AKTIVSITZ_RE_HKL_WERT | real | Analogwert fuer die Tasten Aktivsitz rechts und HKL |
| STAT_AD_WERT_TST_JP_CAM_HDC_WERT | real | Analogwert fuer die Tasten JP-Camera und HDC |
| STAT_AD_WERT_TST_DSC_OFF_WERT | real | Analogwert fuer die Taste DSC-Off |
| STAT_AD_WERT_CODIERLEITUNG_EINS_WERT | real | Analogwert 1 fuer die SZM-Variantencodierung |
| STAT_AD_WERT_CODIERLEITUNG_ZWEI_WERT | real | Analogwert 2 fuer die SZM-Variantencodierung |
| STAT_SZM_VARIANTE_WERT | int | Nummer (1 bis 8) der verbauten SZM-Variante, 0 fuer ungueltig (keine Variante erkannt) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-szm-tasten"></a>
### STEUERN_SZM_TASTEN

Simulieren von Tastenbetaetigungen am Bedienteil KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTEN_NUMMER | int | Tastennummern von links nach rechts 1: Taste Aktivsitz links,    2: Taste PDC     3: Taste DSC Off 4: Taste HDC,                5: Taste HKL,    6: Taste JP-Camera 7: Taste Aktivsitz rechts |
| EIN_AUS | int | 1 = EIN, 0 = AUS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analogeingaenge"></a>
### STATUS_ANALOGEINGAENGE

Auslesen der 16 A/D-Werte (High/Basis) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TINNEN_WERT | real | Innentemperaturfuehler |
| STAT_TINNEN_EINH | string | Grad Celsius |
| STAT_TEMP_VERDAMPFER_WERT | real | Verdampfertemperaturfuehler |
| STAT_TEMP_VERDAMPFER_EINH | string | Grad Celsius |
| STAT_WT_LI_WERT | real | Waermetauscherfuehler links |
| STAT_WT_LI_EINH | string | Grad Celsius |
| STAT_BELUEFTUNG_LINKS_WERT | real | Belueftungsensor links |
| STAT_BELUEFTUNG_LINKS_EINH | string | Grad Celsius |
| STAT_WT_RE_WERT | real | Waermetauscherfuehler rechts (Nur bei HIGH-Ausfuehrung) 255 = nicht verbaut |
| STAT_WT_RE_EINH | string | Grad Celsius (Nur bei HIGH-Ausfuehrung) |
| STAT_BELUEFTUNG_RECHTS_WERT | real | Belueftungstemperatur rechts (Nur bei HIGH-Ausfuehrung) 255 = nicht verbaut |
| STAT_BELUEFTUNG_RECHTS_EINH | string | Grad Celsius (Nur bei HIGH-Ausfuehrung) |
| STAT_LSV_MOTOR_STROM_WERT | real | Stromsense LSV-Motor |
| STAT_LSV_MOTOR_STROM_EINH | string | mA |
| STAT_LSV_JOYSTICK_WERT | real | LSV-Joystick |
| STAT_LSV_JOYSTICK_EINH | string | Volt |
| STAT_SZM_TASTE_1_WERT | real | SZM-Taste-1 |
| STAT_SZM_TASTE_1_EINH | string | Volt |
| STAT_SZM_TASTE_2_WERT | real | SZM-Taste-2 |
| STAT_SZM_TASTE_2_EINH | string | Volt |
| STAT_SZM_TASTE_3_WERT | real | SZM-Taste-3 |
| STAT_SZM_TASTE_3_EINH | string | Volt |
| STAT_SZM_TASTE_4_WERT | real | SZM-Taste-4 |
| STAT_SZM_TASTE_4_EINH | string | Volt |
| STAT_SZM_CODIERUNG_1_WERT | real | SZM-Codierung-1 |
| STAT_SZM_CODIERUNG_1_EINH | string | Volt |
| STAT_SZM_CODIERUNG_2_WERT | real | SZM-Codierung-2 |
| STAT_SZM_CODIERUNG_2_EINH | string | Volt |
| STAT_TREIBER_UB_WERT | real | Treiberversorgung |
| STAT_TREIBER_UB_EINH | string | Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lsv-hal-input"></a>
### STATUS_LSV_HAL_INPUT

Auslesen der LSV-Hallsensoren zur Erkennung von Softstops KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_COUNTER_LENGTH | int | 0: 0-Position, max-Wert: 250, Wert ausserhalb der Verstellbereich = 255 |
| STAT_COUNTER_TILT | int | 0: 0-Position, max-Wert: 250, Wert ausserhalb der Verstellbereich = 255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-motoren-eichlauf"></a>
### STEUERN_MOTOREN_EICHLAUF

Löst Klappeneichlauf aus und kalibriert die Schrittzahlen neu KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-reset-lin"></a>
### STEUERN_RESET_LIN

Löst Rücksetzen des LIN-Bus (Versorgung) aus KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motor-fehler-loeschen"></a>
### STEUERN_MOTOR_FEHLER_LOESCHEN

Löscht Zähler für Motorfehler KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-ident"></a>
### STATUS_MOTOR_IDENT

Liefert die Identdaten des jeweiligen LIN-Bus-Schrittmotors KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LIN_DEVICE_ADDRESS | unsigned char | Adresse des LIN-Bus-Teilnehmers default = 0x20 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_REFERENCE | unsigned char | Aktuelle Referenznummer |
| STAT_SUPPLIER | unsigned char | Aktuelle Suppliernummer |
| STAT_ASIC_NR | unsigned char | Aktuelle ASIC-Nummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klimasystem"></a>
### STATUS_KLIMASYSTEM

Lesen aller ansprechbaren Adressen des LIN-Bus-Systems KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KLIMASYSTEM | binary | Adresse des jeweiligen LIN-Slaves 0xFF = Nicht verbaut oder antwortet nicht Byte0 = PTC Byte1 = Motor1 Byte2 = Motor2 ByteN = MotorN ByteN+1 = Motor mit Adresse 0x3F Beschreibung Fehlerstatus ByteN+2 = Fehlerstatus Beschreibung Fehlerstatus: 0x00 = kein Fehler 0x01 = PTC-Fehler 0x02 = falsch Codiert 0x03 = falscher Klimakasten 0xFF = unbekannter Fehler |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sollwert-ptc"></a>
### STEUERN_SOLLWERT_PTC

Ansteuern des Ptc-Sollwertes im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default Vor dem Ansteuern den Job DIAGNOSE_TESTBIT mit dem Parameter "ein" aufrufen Für die Rückkehr in die geregelte Ansteuerung den Job DIAGNOSE_TESTBIT "aus" aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PTC_SOLLWERT | int | Ptc-Sollwertansteuerung in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selbsttest-schrittmotore"></a>
### STEUERN_SELBSTTEST_SCHRITTMOTORE

Alle Stellmotore auf 50 % verfahren KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

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

<a id="job-steuern-autoadressierung"></a>
### STEUERN_AUTOADRESSIERUNG

Startet die LIN-Bus Autoadressierung KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

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

<a id="job-status-motor-fehler"></a>
### STATUS_MOTOR_FEHLER

Auslesen der Zähler für Lin-Motoren-Fehler KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANTWORT_FEHLT_WERT | int | Status Fehlerzähler Antwort Schrittmotor fehlt |
| STAT_INTERNER_FEHLER_WERT | int | Status Fehlerzähler interner Motorfehler |
| STAT_BLOCKIERUNG_WERT | int | Status Fehlerzähler Blockierung Schrittmotor |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kompressor-einlaufschutz"></a>
### STEUERN_KOMPRESSOR_EINLAUFSCHUTZ

Setzen/Löschen des Kompressor Einlaufschutzes KWP2000: $30 InputOutputControlByLocalIdentifier $42 Kompressor Einlaufschutz (recordLocalIdentifier) $0x Ein/Aus (recordValue#1) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EIN_AUS | string | "ein" -&gt; Kompressoreinlaufschutz beenden "aus" -&gt; Kompressoreinlaufschutz zuruecksetzen table DigitalArgument TEXT Wenn keine Eingabe: Default = "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-timer-einlaufschutz"></a>
### STATUS_TIMER_EINLAUFSCHUTZ

Lesen des Status des Kompressor-Einlaufschutzes KWP2000: $30 InputOutputControlByLocalIdentifier $43 Timer Kompressor Einlaufschutz Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TIMER_EINH | string | Sekunden |
| STAT_TIMER_WERT | unsigned char | Aktuelle Restzeit des Einlaufschutzzählers in Sekunden (0=abgelaufen) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta-block"></a>
### STATUS_FASTA_BLOCK

Aktueller Wert des FASTA-Blocks

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FASTA_BLOCK_ARGUMENT | string | Nummer des FASTA-Blocks (0-FF) table FastaBlockTab Blocknumber,Blockname Wenn keine Eingabe: default = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FASTA_BLOCK_NAME | string | Ausgabe des FASTA-Blocksnamens |
| STAT_FASTA_BLOCK_HEX | int | Status-Fasta-Daten |
| STAT_FASTA_BLOCK_EINH | string | Einheit des FASTA-Blocks Stunden oder Zählerstand |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lhz-zustand"></a>
### STEUERN_LHZ_ZUSTAND

Steuern des Lenkradheizungszustand im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default Vor dem Ansteuern den Job DIAGNOSE_TESTBIT mit dem Parameter "ein" aufrufen Für die Rückkehr in die geregelte Ansteuerung den Job DIAGNOSE_TESTBIT "aus" aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LHZ_ZUSTAND_NR | int | Ansteuerung LHZ-Zustand in den 4 Stufen Zustand 1 = 100 % PWM Zustand 2 = 66 % PWM Zustand 3 = 33 % PWM Zustand 4 = 0 % PWM |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-elsv"></a>
### STATUS_ELSV

Auslesen der Stati der Lenksaeulen-Komponente KWP2000: $30 InputOutputControlByLocalIdentifier $65 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LS_MOTOR | int | 0 = i.O. nicht aktiv, 1 = i.O. aktiv, 2 = Unterbrechung 3 = Kurzschluss, 4 = Überstrom |
| STAT_LS_MOTORSTROM | int | 00,0... 25,0 A 255 = Messung nicht möglich oder sonstige Fehler |
| STAT_HUBMAGNET | char | 0 = i.O nicht aktiv, 1 = i.O. aktiv, 2 = Unterbrechung 3 = Kurzschluss |
| STAT_IO_HAL_LENGTH | char | Softstopp-Sensor Laenge: 0 = nicht aktiv, 1 = aktiv |
| STAT_IO_HAL_TILT | char | Softstopp-Sensor Neigung: 0 = nicht aktiv, 1 = aktiv |
| STAT_ANSCHLAG_OBEN | char | eLSV im Verstellbereichsfenster Softstopp erreicht 0 = kein Softstopp, 1 = softstopp |
| STAT_ANSCHLAG_UNTEN | char | eLSV im Verstellbereichsfenster Softstopp erreicht 0 = kein Softstopp, 1 = softstopp |
| STAT_ANSCHLAG_VORNE | char | eLSV im Verstellbereichsfenster Softstopp erreicht 0 = kein Softstopp, 1 = softstopp |
| STAT_ANSCHLAG_HINTEN | char | eLSV im Verstellbereichsfenster Softstopp erreicht 0 = kein Softstopp, 1 = softstopp |
| STAT_IO_HAL_MOTOR | char | Softstopp-Sensor Neigung: 0 = nicht aktiv, 1 = aktiv 2 = Unterbrechung, 3 = Kurzschluss nach Kl30 |
| STAT_LAENGE_POS_OFFSET | int | aktueller Offset fuer die Laengsachse |
| STAT_LAENGE_POS_RELATIV | int | aktueller Relativwert fuer die Laengsachse |
| STAT_NEIGUNG_POS_OFFSET | int | aktueller Offset fuer die Neigungsachse |
| STAT_NEIGUNG_POS_RELATIV | int | aktueller Relativwert fuer die Neigungsachse |
| STAT_NORMIERUNG_OBEN | char | 0 = nicht normiert, 1 = normiert |
| STAT_NORMIERUNG_UNTEN | char | 0 = nicht normiert, 1 = normiert |
| STAT_NORMIERUNG_VORNE | char | 0 = nicht normiert, 1 = normiert |
| STAT_NORMIERUNG_HINTEN | char | 0 = nicht normiert, 1 = normiert |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-elsv"></a>
### STEUERN_ELSV

Steuern der Lenksaeule im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACHSE | int | 0 = Keine Ansteuerung 1 = Laenge 2 = Neigung |
| RICHTUNG | int | 0 = Keine Richtung 1 = Plus = Zum Fahrer oder nach oben 2 = Minus = Vom Fahrer weg oder nach unten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-elsv-normierung"></a>
### STEUERN_ELSV_NORMIERUNG

Steuern des Lenksaeule im Diagnosemode KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | int | Ansteuerung LSV-Normierung 0 = Eine evtl. laufende Normierung stoppen oder ist keine Normierung am Laufen 1 = Denormieren 2 = Teilnormieren 3 = Vollstaendig normieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-elsv-memory"></a>
### STEUERN_ELSV_MEMORY

Memoryabruf KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MEMORY_POSITION | int | Positionsnummer 0 ... 255 |
| MEMORY_AKTION | int | Memoryabruf 0 = keine Aktion 1 = Memoryposition abrufen 2 = Memoryposotion speichern |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-elsv-memory"></a>
### STATUS_ELSV_MEMORY

Gibt die unter der Memory-Position gespeicherten Werte für Laenge und Neigung zurueck KWP2000: $30 InputOutputControlByLocalIdentifier $69 ReportCurrentState Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LSV_POSITION | int | 0 ... 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LAENGE_POS_OFFSET | int | abgespeicherter Offset |
| STAT_LAENGE_POS_RELATIV | int | abgespeicherter Offset |
| STAT_NEIGUNG_POS_OFFSET | int | abgespeicherter Offset |
| STAT_NEIGUNG_POS_RELATIV | int | abgespeicherter Offset |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-elsv-statistik"></a>
### STATUS_ELSV_STATISTIK

Gibt die unter der Memory-Position gespeicherten Werte für Laenge und Neigung zurueck KWP2000: $30 InputOutputControlByLocalIdentifier $6A ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANZNORMIERUNG | int | Anzahl der Normierungen 0 ... 250 254 = Überlauf 255 = Fehler oder nicht möglich |
| STAT_ANZFAHRTENAUFANSCHLAGVORNE | int | Anzahl der Fahrten auf Anschlag 0 ... 250 254 = Überlauf 255 = Fehler oder nicht möglich |
| STAT_ANZFAHRTENAUFANSCHLAGHINTEN | int | Anzahl der Fahrten auf Anschlag 0 ... 250 254 = Überlauf 255 = Fehler oder nicht möglich |
| STAT_ANZFAHRTENAUFANSCHLAGUNTEN | int | Anzahl der Fahrten auf Anschlag 0 ... 250 254 = Überlauf 255 = Fehler oder nicht möglich |
| STAT_ANZFAHRTENAUFANSCHLAGOBEN | int | Anzahl der Fahrten auf Anschlag 0 ... 250 254 = Überlauf 255 = Fehler oder nicht möglich |
| STAT_ANZFAHRTENAUFSOFTSTOPPVORNE | int | Anzahl der Fahrten auf Softstopp 0 ... 65530 65534 = Überlauf 35535 = Fehler oder nicht möglich |
| STAT_ANZFAHRTENAUFSOFTSTOPPHINTEN | int | Anzahl der Fahrten auf Softstopp 0 ... 250 254 = Überlauf 255 = Fehler oder nicht möglich |
| STAT_ANZFAHRTENAUFSOFTSTOPPUNTEN | int | Anzahl der Fahrten auf Softstopp 0 ... 250 254 = Überlauf 255 = Fehler oder nicht möglich |
| STAT_ANZFAHRTENAUFSOFTSTOPPOBEN | int | Anzahl der Fahrten auf Softstopp 0 ... 65530 65534 = Überlauf 35535 = Fehler oder nicht möglich |
| STAT_ANZFAHRTENINEINSTIEGPOSITION | int | Anzahl der Normierungen 0 ... 65530 65534 = Überlauf 35535 = Fehler oder nicht möglich |
| STAT_MANVERSTELLUNGNEIGUNG | int | Anzahl der Normierungen 0 ... 65530 65534 = Überlauf 35535 = Fehler oder nicht möglich |
| STAT_MANVERSTELLUNGLAENGE | int | Anzahl der Normierungen 0 ... 65530 65534 = Überlauf 35535 = Fehler oder nicht möglich |
| STAT_MEMORYABRUF | int | Anzahl der Normierungen 0 ... 65530 65534 = Überlauf 35535 = Fehler oder nicht möglich |
| STAT_MEMORYSPEICHERN | int | Anzahl der Normierungen 0 ... 65530 65534 = Überlauf 35535 = Fehler oder nicht möglich |
| STAT_BETRIEBSSEKUNDEN | int | Anzahl der Normierungen 0 ... 65530 65534 = Überlauf 35535 = Fehler oder nicht möglich |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-schrittzahlen"></a>
### STATUS_MOTOR_SCHRITTZAHLEN

Auslesen der vermessenen Schrittzahlen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHRITTZAHL_EINH | string | Schritte |
| STAT_FRISCHLUFT_UMLUFT_SCHRITTZAHL_WERT | int | vermessene Schrittzahl FL/Umluft-Klappe 0xFFFF wenn nicht verbaut |
| STAT_STAUDRUCK_SCHRITTZAHL_WERT | int | vermessene Schrittzahl Staudruck-Klappe 0xFFFF wenn nicht verbaut |
| STAT_DEFROST_SCHRITTZAHL_WERT | int | vermessene Schrittzahl DefrostKlappe 0xFFFF wenn nicht verbaut |
| STAT_BELUEFTUNG_LI_SCHRITTZAHL_WERT | int | vermessene Schrittzahl Belüftungsklappe links 0xFFFF wenn nicht verbaut |
| STAT_BELUEFTUNG_RE_SCHRITTZAHL_WERT | int | vermessene Schrittzahl Belüftungsklappe rechts 0xFFFF wenn nicht verbaut |
| STAT_SCHICHTUNG_LI_SCHRITTZAHL_WERT | int | vermessene Schrittzahl Schichtungsklappe links 0xFFFF wenn nicht verbaut |
| STAT_SCHICHTUNG_RE_SCHRITTZAHL_WERT | int | vermessene Schrittzahl Schichtungsklappe rechts 0xFFFF wenn nicht verbaut |
| STAT_FUSSRAUM_LI_SCHRITTZAHL_WERT | int | vermessene Schrittzahl Fußraumklappe links 0xFFFF wenn nicht verbaut |
| STAT_FUSSRAUM_RE_SCHRITTZAHL_WERT | int | vermessene Schrittzahl Fußraumklappe rechts 0xFFFF wenn nicht verbaut |
| STAT_FUSS_FOND_LI_SCHRITTZAHL_WERT | int | vermessene Schrittzahl Fondfußraumklappe links 0xFFFF wenn nicht verbaut |
| STAT_FUSS_FOND_RE_SCHRITTZAHL_WERT | int | vermessene Schrittzahl Fondfußraumklappe rechts 0xFFFF wenn nicht verbaut |
| STAT_SCHICHT_FOND_LI_SCHRITTZAHL_WERT | int | vermessene Schrittzahl Fondschichtungsklappe links 0xFFFF wenn nicht verbaut |
| STAT_SCHICHT_FOND_RE_SCHRITTZAHL_WERT | int | vermessene Schrittzahl Fondschichtungsklappe rechts 0xFFFF wenn nicht verbaut |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-freigabe-ptc-3sitzr"></a>
### STEUERN_FREIGABE_PTC_3SITZR

Setzen/Löschen Freigabe Ptc 3. Sitzreihe KWP2000: $30 InputOutputControlByLocalIdentifier $34 Freigabe Ptc 3. Sitzreihe (recordLocalIdentifier) $0x Ein/Aus (recordValue#1) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EIN_AUS | string | "ein" -&gt; Freigabe Ptc aktivieren "aus" -&gt; Freigabe Ptc deaktivieren table DigitalArgument TEXT Wenn keine Eingabe: Default = "aus" |

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
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [CBSKENNUNG](#table-cbskennung) (17 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (93 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (5 × 9)
- [FARTTYP](#table-farttyp) (93 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (56 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [BOSKENNUNG](#table-boskennung) (11 × 3)
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
- [FASTABLOCKTAB](#table-fastablocktab) (15 × 3)

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

Dimensions: 17 rows × 3 columns

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
| 0x0A | ZKrz_a | Zuendkerzen adaptiv |

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

Dimensions: 93 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9C48 | Motor Entfrostung |
| 0x9C49 | Motor Frischluft/Umluft |
| 0x9C4A | Motor Staudruck |
| 0x9C4B | Motor Fuss rechts |
| 0x9C4C | Motor Fuss links |
| 0x9C4D | Motor Schichtung links |
| 0x9C4E | Motor Belüftung links |
| 0x9C4F | Motor Belüftung rechts |
| 0x9C50 | Motor Schichtung rechts |
| 0x9C51 | Motor Fuss Fond links |
| 0x9C52 | Motor Fuss Fond rechts |
| 0x9C53 | Motor Schichtung Fond links |
| 0x9C54 | Motor Schichtung Fond rechts |
| 0x9C55 | PTC-Zuheizer |
| 0x9C56 | Dritte Sitzreihe |
| 0x9C57 | Geblaese-Endstufe |
| 0x9C58 | Fühler Innentemperatur |
| 0x9C59 | Verdampfertemperaturfühler |
| 0x9C5A | Fühler Wärmetauscher links |
| 0x9C5B | Belüftungstemperaturfühler links |
| 0x9C5C | Fühler Wärmetauscher rechts |
| 0x9C5D | Belüftungstemperaturfühler rechts |
| 0x9C5E | LSV Motorstrom |
| 0x9C5F | LSV-Joystick |
| 0x9C60 | SZM-Taste 1 |
| 0x9C61 | SZM-Taste 2 |
| 0x9C62 | SZM-Taste 3 |
| 0x9C63 | SZM-Taste 4 |
| 0x9C64 | SZM-Variantencodierung 1 |
| 0x9C65 | SZM-Variantencodierung 2 |
| 0x9C66 | Versorgung intern |
| 0x9C68 | Lin-Versorgung |
| 0x9C6A | Innenfuehlergeblaese |
| 0x9C6B | Lenkradheizung |
| 0x9C6C | Lenksaeule Verstellmotor |
| 0x9C6D | Lenksaeule Hubmagnet |
| 0x9C6E | Lenksaeule HallSensor am Motor |
| 0x9C6F | Lenksaeule Versorgung Softstops |
| 0x9C70 | SZM Versorgung |
| 0x9C71 | SZM Suchbeleuchtung |
| 0x9C7A | Autoadressierung |
| 0x9C7B | Dritte Sitzreihe Ptc |
| 0x9C7C | Dritte Sitzreihe Kommunkation |
| 0x9C7D | Dritte Sitzreihe Geblaese |
| 0x9C7E | Standheizung systembedingte Abschaltung |
| 0x9C7F | Standheizung Kommunikation |
| 0x9C80 | Standheizung Gluehstift |
| 0x9C81 | Standheizung Brennluftgeblaese |
| 0x9C82 | Standheizung Wasserpumpe |
| 0x9C83 | Standheizung Magnetventil |
| 0x9C84 | Standheizung Dosierpumpe |
| 0x9C85 | Standheizung Temperatursensor |
| 0x9C86 | Standheizung Unter-/Ueberspannung |
| 0x9C87 | Standheizung Gesamtgeraet |
| 0x9C88 | Standheizung Ueberhitzungssensor |
| 0x9C89 | Standheizung Flamme-Start |
| 0x9C8A | Standheizung Kraftstoffvorwaermung |
| 0x9C8B | Standheizung LIN-Kommunikation |
| 0x9C8C | Standheizung System-Fehler |
| 0x9C8D | Standheizung Absperrventil |
| 0x9CA7 | Energiesparmode aktiv |
| 0xE704 | K-Can physikalischer Busfehler |
| 0xE707 | CAN-Controller, Bus Off |
| 0xE708 | LIN-Busfehler |
| 0xE714 | Botschaft (KCAN: Powermanagement Batteriespannung, 3B4) |
| 0xE715 | Botschaft (KCAN: Kilometerstand/Reichweite, 330) |
| 0xE716 | Botschaft (KCAN: Powermanagement Verbrauchersteuerung, 3B3) |
| 0xE717 | Botschaft (KCAN: Relativzeit, 328) |
| 0xE718 | Botschaft (KCAN: Wärmestrom Motor, 1B6) |
| 0xE719 | Botschaft (KCAN: Motordaten, 1D0) |
| 0xE71A | Botschaft (KCAN: Klemmenstatus, 130) |
| 0xE71B | Botschaft (KCAN: Aussentemperatur, 2CA) |
| 0xE71C | Botschaft (KCAN: Geschwindigkeit, 1A0) |
| 0xE71D | Botschaft (KCAN: Status Klima SH/ZH Zusatzwasserpumpe, 2EC) |
| 0xE71E | Botschaft (KCAN: Drehmoment 3, AA) |
| 0xE71F | Botschaft (KCAN: Dimmung, 202) |
| 0xE720 | Botschaft (KCAN: Lcd-Leuchtdichte, 2C0) |
| 0xE721 | Botschaft (KCAN: Anzeige Hdc, 32D) |
| 0xE722 | Botschaft (KCAN: Crash, 1FE) |
| 0xE723 | Botschaft (KCAN: Status Beschlag Scheibe V, 2D1) |
| 0xE724 | Botschaft (KCAN: Status BFS, 22A) |
| 0xE725 | Botschaft (KCAN: Status FAS, 232) |
| 0xE726 | Botschaft (KCAN: Status Klima Fond, 23E) |
| 0xE727 | Botschaft (KCAN: Status PDC, 24A) |
| 0xE728 | Botschaft (KCAN: Status Schichtung Fond, 2D3) |
| 0xE729 | Botschaft (KCAN: Status Sensor AUC, 2D0) |
| 0xE72A | Botschaft (KCAN: Status Druck Kaeltekreislauf, 2D2) |
| 0xE72B | Botschaft (KCAN: Status Solarsensor, 3D3) |
| 0xE72C | Botschaft (KCAN: Soll Klima Fond, 3FA) |
| 0xE72D | Botschaft (KCAN: Status Ventil Klimakompressor, 2D6) |
| 0xE72E | Botschaft (KCAN: Status Klima Zusatzwasserpumpe, 2CF) |
| 0xE72F | Botschaft (KCAN: Temperatur Ist Fond, 2C2) |
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
| 0x04 | FuellstandTank | l | - | unsigned char | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 93 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x9C48 | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C49 | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C4A | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C4B | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C4C | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C4D | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C4E | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C4F | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C50 | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C51 | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C52 | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C53 | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C54 | 0x0009 | 0x000C | 0x000B | 0x000A |
| 0x9C55 | 0x0010 | 0x000F | 0x000E | 0x0014 |
| 0x9C56 | 0x0037 | 0x0011 | 0x0037 | 0x0037 |
| 0x9C57 | 0x0037 | 0x0037 | 0x0013 | 0x0012 |
| 0x9C58 | 0x0037 | 0x0037 | 0x000D | 0x0014 |
| 0x9C59 | 0x0037 | 0x0037 | 0x000D | 0x0014 |
| 0x9C5A | 0x0037 | 0x0037 | 0x000D | 0x0014 |
| 0x9C5B | 0x0037 | 0x0037 | 0x000D | 0x0014 |
| 0x9C5C | 0x0037 | 0x0037 | 0x000D | 0x0014 |
| 0x9C5D | 0x0037 | 0x0037 | 0x000D | 0x0014 |
| 0x9C5E | 0x0037 | 0x0037 | 0x000D | 0x0014 |
| 0x9C5F | 0x0037 | 0x0037 | 0x000D | 0x0014 |
| 0x9C60 | 0x0038 | 0x0037 | 0x000D | 0x0014 |
| 0x9C61 | 0x0038 | 0x0037 | 0x000D | 0x0014 |
| 0x9C62 | 0x0038 | 0x0037 | 0x000D | 0x0014 |
| 0x9C63 | 0x0038 | 0x0037 | 0x000D | 0x0014 |
| 0x9C64 | 0x0039 | 0x0037 | 0x000D | 0x0014 |
| 0x9C65 | 0x0039 | 0x0037 | 0x000D | 0x0014 |
| 0x9C66 | 0x0037 | 0x0037 | 0x000D | 0x0014 |
| 0x9C68 | 0x0037 | 0x0037 | 0x000D | 0x0037 |
| 0x9C6A | 0x0037 | 0x0037 | 0x000B | 0x0037 |
| 0x9C6B | 0x0037 | 0x0037 | 0x0013 | 0x0012 |
| 0x9C6C | 0x0037 | 0x0016 | 0x000D | 0x0012 |
| 0x9C6D | 0x0037 | 0x0037 | 0x0013 | 0x0012 |
| 0x9C6E | 0x0037 | 0x0017 | 0x0037 | 0x0037 |
| 0x9C6F | 0x0037 | 0x0037 | 0x000D | 0x0037 |
| 0x9C70 | 0x0018 | 0x0016 | 0x000D | 0x0037 |
| 0x9C71 | 0x0037 | 0x0037 | 0x0037 | 0x0012 |
| 0x9C7A | 0x0019 | 0x0037 | 0x0037 | 0x0037 |
| 0x9C7B | 0x001B | 0x001A | 0x000D | 0x0014 |
| 0x9C7C | 0x0008 | 0x002D | 0x0002 | 0x001C |
| 0x9C7D | 0x003A | 0x0008 | 0x001D | 0x0014 |
| 0x9C7E | 0x0036 | 0x0035 | 0x0037 | 0x0037 |
| 0x9C7F | 0x0037 | 0x001F | 0x0037 | 0x0037 |
| 0x9C80 | 0x0021 | 0x0020 | 0x000D | 0x0014 |
| 0x9C81 | 0x001E | 0x000B | 0x000D | 0x0014 |
| 0x9C82 | 0x0008 | 0x0004 | 0x000D | 0x0014 |
| 0x9C83 | 0x0008 | 0x0004 | 0x000D | 0x0014 |
| 0x9C84 | 0x0008 | 0x0004 | 0x000D | 0x0014 |
| 0x9C85 | 0x0008 | 0x0004 | 0x000D | 0x0014 |
| 0x9C86 | 0x0008 | 0x0004 | 0x0023 | 0x0022 |
| 0x9C87 | 0x0026 | 0x0025 | 0x0015 | 0x0024 |
| 0x9C88 | 0x0008 | 0x0027 | 0x0002 | 0x0001 |
| 0x9C89 | 0x002B | 0x002A | 0x0029 | 0x0028 |
| 0x9C8A | 0x0008 | 0x0004 | 0x000D | 0x0014 |
| 0x9C8B | 0x002E | 0x002D | 0x002C | 0x001C |
| 0x9C8C | 0x0008 | 0x0004 | 0x0030 | 0x002F |
| 0x9C8D | 0x0008 | 0x0004 | 0x000D | 0x0014 |
| 0x9CA7 | 0x0037 | 0x0037 | 0x0037 | 0x0037 |
| 0xE704 | 0x0037 | 0x0037 | 0x0037 | 0x0037 |
| 0xE707 | 0x0037 | 0x0032 | 0x0037 | 0x0037 |
| 0xE708 | 0x0037 | 0x0033 | 0x0017 | 0x0037 |
| 0xE714 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE715 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE716 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE717 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE718 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE719 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE71A | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE71B | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE71C | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE71D | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE71E | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE71F | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE720 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE721 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE722 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE723 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE724 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE725 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE726 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE727 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE728 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE729 | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE72A | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE72B | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE72C | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE72D | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE72E | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| 0xE72F | 0x0034 | 0x001F | 0x0037 | 0x0037 |
| default | 0x0037 | 0x0037 | 0x0037 | 0x0037 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 56 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0004 | kein Signal oder Wert |
| 0x0008 | unplausibles Signal oder Wert |
| 0x0009 | Intitialisierungsfehler |
| 0x000A | interner Motorfehler |
| 0x000B | Blockierung |
| 0x000C | Motor antwortet nicht |
| 0x000D | Kurzschluss Masse |
| 0x000E | Übertemperatur |
| 0x000F | Ptc antwortet nicht |
| 0x0010 | Ptc antwortet 5 mal mit Status Reset |
| 0x0011 | Dritte Sitzreihe antwortet nicht |
| 0x0012 | Kurzschluss Plus |
| 0x0013 | Kurzschluss Masse oder Unterbrechung |
| 0x0014 | Kurzschluss Plus oder Unterbrechung |
| 0x0015 | Heizgerät verriegelt |
| 0x0016 | Unterbrechung |
| 0x0017 | Unterbrechung Lin-Bus Aggregat |
| 0x0018 | Keine gültige SZM-Variante erkannt |
| 0x0019 | Autoadressierung fehlerhaft |
| 0x001A | Spannungsfehler |
| 0x001B | Temperaturfehler |
| 0x001C | Bit Error |
| 0x001D | Kurzschluss nach Masse / Blockierung |
| 0x001E | Schwergängigkeit |
| 0x001F | Timeout |
| 0x0020 | Referenzwiderstand nicht erreicht |
| 0x0021 | Fremdlicht (Wendel defekt/unterbrochen) od. Glühstift defekt |
| 0x0022 | Überspannung |
| 0x0023 | Unterspannung |
| 0x0024 | Überhitzung |
| 0x0025 | Steuergerät defekt (RAM,ROM,SW) |
| 0x0026 | EOL-Checksummenfehler |
| 0x0027 | Sicherung defekt |
| 0x0028 | Flammabbruch |
| 0x0029 | Flammabbruch: wiederholter Abbruch im Heizzyklus |
| 0x002A | Kein Start: Keine Flamme im Normalbetrieb |
| 0x002B | Kein Start: Keine Flamme im Testbetrieb |
| 0x002C | Baudratedetection fehlgeschlagen |
| 0x002D | LIN-Time out (-&gt; Notlauf:Abschaltung) |
| 0x002E | Signal mit Ungültigkeitssignatur |
| 0x002F | Überschreitung der Heizzeitvorgabe |
| 0x0030 | Not-Aus wurde angefordert, qualmen möglich |
| 0x0031 | physikalischer Busfehler |
| 0x0032 | Bus Off |
| 0x0033 | Unterbrechung Lin-Bus |
| 0x0034 | Fehler in der Botschaft |
| 0x0035 | Tankinhalt zu gering |
| 0x0036 | Abschaltung durch Verbrauchersteuerung |
| 0x0037 | nicht verwendet |
| 0x0038 | Analogspannung ungültiger Bereich (Spannung kann keiner Taste zugeordnet werden). |
| 0x0039 | Analogspannung ungültiger Bereich (Spannung kann keiner Variante zugeordnet werden). |
| 0x003A | Interner Treiber Funktions-LED defekt |
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

<a id="table-fastablocktab"></a>
### FASTABLOCKTAB

Dimensions: 15 rows × 3 columns

| NR | FASTA_K | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | ges | BETR_STD_GES |
| 0x01 | autoklli | BETR_STD_KLAPPEN_AUTO_LINKS |
| 0x02 | autoklre | BETR_STD_KLAPPEN_AUTO_RECHTS |
| 0x03 | autogebl | BETR_STD_GEBLAESE_AUTO |
| 0x04 | klima | BETR_STD_KLIMA_BETRIEB |
| 0x05 | auc | BETR_STD_AUC_BETRIEB |
| 0x06 | umluft | BETR_STD_ZWANGSUMLUFT_BETRIEB |
| 0x07 | off | BETR_STD_OFF_BETRIEB |
| 0x08 | hhs | BETR_STD_HHS_BETRIEB |
| 0x09 | sh | BETR_STD_STANDHEIZUNG |
| 0x0A | sl | BETR_STD_STANDLUEFTEN |
| 0x0B | anz_res | ANZ_DER_RESETS_UND_SPG_ABRISSE |
| 0x0C | anz_restw | ANZ_DER_AKTIVIERUNGEN_RESTW |
| 0x0D | anz_auto | ANZ_DER_AKTIVIERUNGEN_VOLLAUTOMATIK AUS DEFROST |
| 0xFF | ungültig |  |
