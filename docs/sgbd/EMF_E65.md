# EMF_E65.prg

- Jobs: [98](#jobs)
- Tables: [60](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EMF_E65 |
| ORIGIN | BMW EE-23, Hoedl, TI-431 Helmich |
| REVISION | 1.02 |
| AUTHOR | SiemensVDO SE CS 41 BRANDL, Funk |
| COMMENT | Elektromechanische Feststellbremse |
| PACKAGE | 1.17 |
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
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
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
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Seuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [STEUERN_SWITCH_TO_APPL_MODE](#job-steuern-switch-to-appl-mode) - Umschalten vom Bootmodus in Applikationmode KWP2000: $31 StartToutineByLocalIdentifier $FD ApllMode Modus  : Default
- [STEUERN_AUSGANG_MAINRELAIS](#job-steuern-ausgang-mainrelais) - Ansteuern von AUSGANG_MAINRELAIS KWP2000: $30 InputOutputControlByLocalIdentifier KWP2000: $FD MOTOR $07 ShortTermAdjustment Modus  : Default
- [STEUERN_EINBREMSEN](#job-steuern-einbremsen) - Feststellbremse fuer Werkstatteinbremsen, kontinuierliches Einbremsen KWP2000: $30 InputOutputControlByLocalIdentifier KWP2000: $01 IOLI = BREMSE $07 ShortTermAdjustment Modus  : Default
- [STEUERN_AUSGANG_MOTORENDSTUFE](#job-steuern-ausgang-motorendstufe) - Ansteuern von AUSGANG_MOTORENDSTUFE KWP2000: $30 InputOutputControlByLocalIdentifier KWP2000: $FA MOTOR $07 ShortTermAdjustment Modus  : Default
- [STEUERN_ECU_RESET](#job-steuern-ecu-reset) - Ansteuern von ECU_RESET KWP2000: $30 InputOutputControlByLocalIdentifier $00 RCTECU Modus  : Default
- [STATUS_DIGITALEINGAENGE](#job-status-digitaleingaenge) - Auslesen der DIGITALEINGAENGE KWP2000: $30 InputOutputControlByLocalIdentifier $18 liefert Digitaleingaenge $01 ReportCurrentState Modus  : Default
- [STATUS_DREHZAHL_EMF_MOTOR](#job-status-drehzahl-emf-motor) - Auslesen der DREHZAHL_EMF_MOTOR KWP2000: $30 InputOutputControlByLocalIdentifier $11 liefert Drehzahl und Richtung $01 ReportCurrentState Modus  : Default
- [STATUS_AD_WERTE_TEMPERATUR](#job-status-ad-werte-temperatur) - Auslesen des AD-Wertes der Temperatur KWP2000: $30 InputOutputControlByLocalIdentifier $23 liefert AD_Wert Temperatur $01 ReportCurrentState Modus  : Default
- [STATUS_AD_WERTE_MOTOR](#job-status-ad-werte-motor) - Auslesen der AD-Werte vom MOTOR KWP2000: $30 InputOutputControlByLocalIdentifier $20 liefert ungefilterte Motorspannungen $01 ReportCurrentState Modus  : Default
- [STATUS_AD_WERTE_TASTER](#job-status-ad-werte-taster) - Auslesen der AD-Werte Tastereingaenge KWP2000: $30 InputOutputControlByLocalIdentifier $22 liefert Tasterspannungen $01 ReportCurrentState Modus  : Default
- [STATUS_AD_Werte_Kl30_KL15W](#job-status-ad-werte-kl30-kl15w) - Auslesen der AD-Werte Kl30/KL15W KWP2000: $30 InputOutputControlByLocalIdentifier $21 liefert Klemmenspannung $01 ReportCurrentState Modus  : Default
- [STATUS_GESCHWINDIGKEIT](#job-status-geschwindigkeit) - Auslesen der Stati von Geschwindigkeit KWP2000: $30 InputOutputControlByLocalIdentifier $10 liefert Rad Geschwindigkeit $01 ReportCurrentState Modus  : Default
- [STATUS_KODIERDATEN](#job-status-kodierdaten) - Auslesen der Kodierdaten vom EMF KWP2000: $22 ReadDataByComonIdentifier $3000 CodingDataSet EMF1 Modus  : Default
- [STATUS_PHY_ECU_HW_NR](#job-status-phy-ecu-hw-nr) - Auslesen physikalischen ECU HW Nummer KWP2000: $1A  ReadECUIdentification $87  PECUHN Modus  : Default
- [STATUS_BMW_TEILE_NR](#job-status-bmw-teile-nr) - Auslesen der BMW_Teilenummer KWP2000: $1A  ReadECUIdentification $91  VMECUHN Modus  : Default
- [STATUS_BMW_CODIER_INDEX](#job-status-bmw-codier-index) - Auslesen des BMW Codierindex aus ZIF KWP2000: $1A  ReadECUIdentification $9B  VMCI Modus  : Default
- [STATUS_BMW_DIAG_INDEX](#job-status-bmw-diag-index) - Auslesen des BMW Diagnoseindex aus ZIF KWP2000: $1A  ReadECUIdentification $9C  VDCI Modus  : Default
- [STATUS_PROGRAMM_DATE](#job-status-programm-date) - Ausgabe des Programming Date aus UIF KWP2000: $1A  ReadECUIdentification $99  PD Modus  : Default
- [STATUS_AIF_LESEN](#job-status-aif-lesen) - Auslesen des Anwender Informations Feldes $1A ReadECUIdentification KWP 2000: $86 CUIFDT Modus   : Default
- [STATUS_ER_FESTELLKRAFT_LESEN](#job-status-er-festellkraft-lesen) - Auslesen der erreichten Festellkraft (N) KWP2000: $22 ReadDataByCommonIdentifier $0001 F_ERREICHT Modus  : Default
- [STATUS_AKT_ISTPOSITION_LESEN](#job-status-akt-istposition-lesen) - Aktuelle Istposition Stelleinheit [1/4 U] KWP2000: $22 ReadDataByCommonIdentifier $000_2 STAT_AKT_ISTPOS Modus  : Default
- [STATUS_LETZTE_LOESEPOS_LESEN](#job-status-letzte-loesepos-lesen) - Letzte Loeseposition [1/4 U] KWP2000: $22 ReadDataByCommonIdentifier $0003 STAT_LET_LOESPOS Modus  : Default
- [STATUS_LETZTE_ANZUGSPOS_LESEN](#job-status-letzte-anzugspos-lesen) - Letzte Anzugsposition [1/4 U] KWP2000: $22 ReadDataByCommonIdentifier $0004 STAT_LET_ANZUGSPOS Modus  : Default
- [STATUS_LETZTEN_KRAFTEIN_LESEN](#job-status-letzten-kraftein-lesen) - Letzter Krafteinsatzpunkt [1/4 U] KWP2000: $22 ReadDataByCommonIdentifier $0005 STAT_LET_KRAFTEIN Modus  : Default
- [STATUS_BETAETIGUNGSZAEHLER_LESEN](#job-status-betaetigungszaehler-lesen) - Betaetigungszaehler (Anzahl Stellvorgaenge) KWP2000: $22 ReadDataByCommonIdentifier $0006 STAT_BET_ZAEHLER Modus  : Default
- [STATUS_EINBREMS_ZAEHLER_LESEN](#job-status-einbrems-zaehler-lesen) - Einbremszaehler (Anzahl Einbremsvorgaenge) KWP2000: $22 ReadDataByCommonIdentifier $0007 STAT_ EINBREMS_ZAEH Modus  : Default
- [STATUS_EINBREMS_STRECKE_LESEN](#job-status-einbrems-strecke-lesen) - Einbremsstrecke [m] KWP2000: $22 ReadDataByCommonIdentifier $0008 STAT_ EINBREMS_STRE Modus  : Default
- [STATUS_SPEZIALMODI](#job-status-spezialmodi) - SPEzialmodi_lesen KWP2000: $22 ReadDataByCommonIdentifier $0012 STAT_ EINBREMS_STRE Modus  : Default
- [STEUERN_KRAFTEINSATZ_SETZEN](#job-steuern-krafteinsatz-setzen) - Stelleinheit Krafteinsatzpunkt setzen KWP2000: $2E WriteDataByCommonIdentifier $0010 RCI = SSS.KEP_SET Modus  : Default
- [STEUERN_KRAFTEINSATZ_UEBERNEHMEN](#job-steuern-krafteinsatz-uebernehmen) - Stelleinheit aktuellen Krafteinsatzpunkt uebernehmen KWP2000: $2E WriteDataByCommonIdentifier $0011 RCI = SSS.KEP_TAKE Modus  : Default
- [STEUERN_SPEZIALMODI](#job-steuern-spezialmodi) - Spezialmodi_einstellen KWP2000: $2E WriteDataByCommonIdentifier $0012 RCI = SPEZIAL_MODIS Modus  : Default
- [STEUERN_FESTSTELLEN](#job-steuern-feststellen) - Feststellkraft nur fuer naechsten Anziehvorgang KWP2000: $3B WriteDataByCommonIdentifier $01 RLI = F_Feststellen Modus  : Default
- [STEUERN_PERSONALISIERUNG](#job-steuern-personalisierung) - Feststellkraft nur fuer naechsten Anziehvorgang KWP2000: $3B WriteDataByCommonIdentifier $02 RLI = PERSONALISIERUNG Modus  : Default
- [STEUERN_KOMFORTFUNKTION](#job-steuern-komfortfunktion) - Feststellkraft nur fuer naechsten Anziehvorgang KWP2000: $3B WriteDataByCommonIdentifier $03 RLI = KOMFORTFUNKTION Modus  : Default
- [STATUS_SLOG1_LESEN](#job-status-slog1-lesen) - Slog_Parameter_Block1 KWP2000: $22 ReadDataByCommonIdentifier $3001 STAT_SLOG1 Modus  : Default
- [STATUS_SLOG2_LESEN](#job-status-slog2-lesen) - Slog_Parameter_Block1 KWP2000: $22 ReadDataByCommonIdentifier $3002 STAT_SLOG2 Modus  : Default
- [STATUS_SLOG3_LESEN](#job-status-slog3-lesen) - Slog_Parameter_Block1 KWP2000: $22 ReadDataByCommonIdentifier $3003 STAT_SLOG3 Modus  : Default
- [STATUS_SEDEC](#job-status-sedec) - Sedec-Status auslesen KWP2000: $22 ReadDataByCommonIdentifier $F1 RCI=SSS.SEDEC_STATUS Modus  : Default
- [STEUERN_SLOG1_SCHREIBEN](#job-steuern-slog1-schreiben) - SLOG-Parameter-Block1 KWP2000: $2E WriteDataByCommonIdentifier $3001 RCI = SLOG_PARA1 Modus  : Default
- [STEUERN_SLOG2_SCHREIBEN](#job-steuern-slog2-schreiben) - SLOG-Parameter-Block2 KWP2000: $2E WriteDataByCommonIdentifier $3002 RCI = SLOG_PARA2 Modus  : Default
- [STEUERN_SLOG3_SCHREIBEN](#job-steuern-slog3-schreiben) - SLOG-Parameter-Block2 KWP2000: $2E WriteDataByCommonIdentifier $3003 RCI = SLOG_PARA3 Modus  : Default
- [FS_LESEN_SAR](#job-fs-lesen-sar) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [STATUS_HISTORY_FS](#job-status-history-fs) - History-Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $22 RDBCI.DTCHM Modus  : Default
- [STEUERN_HISTORY_FS_LOESCHEN](#job-steuern-history-fs-loeschen) - History-Fehlerspeicher loeschen KWP2000: $31 STRBLI.CHM Modus  : Default
- [STEUERN_HISTORY_FS_LOESCHEN_DETAIL](#job-steuern-history-fs-loeschen-detail) - History-Fehlerspeicher loeschen KWP2000: $31 STRBLI.CHM Modus  : Default
- [STATUS_HISTORY_FS_DETAIL](#job-status-history-fs-detail) - History-Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $22 RDBCI.DTCHM Modus: Default

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

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-schreiben"></a>
### C_AEI_SCHREIBEN

Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

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
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

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

Seuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

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

<a id="job-steuern-switch-to-appl-mode"></a>
### STEUERN_SWITCH_TO_APPL_MODE

Umschalten vom Bootmodus in Applikationmode KWP2000: $31 StartToutineByLocalIdentifier $FD ApllMode Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ausgang-mainrelais"></a>
### STEUERN_AUSGANG_MAINRELAIS

Ansteuern von AUSGANG_MAINRELAIS KWP2000: $30 InputOutputControlByLocalIdentifier KWP2000: $FD MOTOR $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MAINRELAIS_FUNKTION | int | AUS, EIN Werte: 0 = AUS, 1 = EIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-einbremsen"></a>
### STEUERN_EINBREMSEN

Feststellbremse fuer Werkstatteinbremsen, kontinuierliches Einbremsen KWP2000: $30 InputOutputControlByLocalIdentifier KWP2000: $01 IOLI = BREMSE $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BREMSFUNKTION | int | AUS, Werkstatt, Kontinuierlich Werte: 0 = AUS, 1 = Werkstatt, 2 = Kontinuierlich |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ausgang-motorendstufe"></a>
### STEUERN_AUSGANG_MOTORENDSTUFE

Ansteuern von AUSGANG_MOTORENDSTUFE KWP2000: $30 InputOutputControlByLocalIdentifier KWP2000: $FA MOTOR $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTOR_FUNKTION | int | AUS, Anziehen, Loesen Werte: 0= AUS,1=anziehen,2=loesen |
| MOTOR_DUTY | int | TASTVERHAELTNISS in % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ecu-reset"></a>
### STEUERN_ECU_RESET

Ansteuern von ECU_RESET KWP2000: $30 InputOutputControlByLocalIdentifier $00 RCTECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digitaleingaenge"></a>
### STATUS_DIGITALEINGAENGE

Auslesen der DIGITALEINGAENGE KWP2000: $30 InputOutputControlByLocalIdentifier $18 liefert Digitaleingaenge $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EMF_TASTE | string | EMF TASTE |
| STAT_DSC_P | string | DSC_P |
| STAT_FREIG_ANZIEHEN | string | Freigabe anziehen |
| STAT_FREIG_LOESEN | string | Freigabe loesen |
| STAT_MOTOR_POSITION_WERT | int | Motorposition |
| STAT_MOTOR_POSITION_EINH | string | 1/4 U |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drehzahl-emf-motor"></a>
### STATUS_DREHZAHL_EMF_MOTOR

Auslesen der DREHZAHL_EMF_MOTOR KWP2000: $30 InputOutputControlByLocalIdentifier $11 liefert Drehzahl und Richtung $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DREHZAHL_EMF_MOTOR_WERT | int | DREHZAHL EMF MOTOR |
| STAT_DREHZAHL_EMF_MOTOR_EINH | string | U/min |
| STAT_DREHRICHTUNG_EMF_MOTOR_WERT | char | DREHRICHTUNG EMF MOTOR |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ad-werte-temperatur"></a>
### STATUS_AD_WERTE_TEMPERATUR

Auslesen des AD-Wertes der Temperatur KWP2000: $30 InputOutputControlByLocalIdentifier $23 liefert AD_Wert Temperatur $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AD_TEMPERATUR_WERT | int | AD-Wert Temperatur |
| STAT_AD_TEMPERATUR_EINH | string | Grad C |
| STAT_AD_TEMPERATUR_4_WERT | char | akt. 8Bit AD-Wert |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ad-werte-motor"></a>
### STATUS_AD_WERTE_MOTOR

Auslesen der AD-Werte vom MOTOR KWP2000: $30 InputOutputControlByLocalIdentifier $20 liefert ungefilterte Motorspannungen $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AD_M1_WERT | int | AD-Wert Klemme M1 |
| STAT_AD_M1_EINH | string | V |
| STAT_AD_M2_WERT | int | AD-Wert Klemme M2 |
| STAT_AD_M2_EINH | string | V |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ad-werte-taster"></a>
### STATUS_AD_WERTE_TASTER

Auslesen der AD-Werte Tastereingaenge KWP2000: $30 InputOutputControlByLocalIdentifier $22 liefert Tasterspannungen $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AD_S1_WERT | int | AD-Wert Tastereingang S1 |
| STAT_AD_S1_EINH | string | V |
| STAT_AD_S2_WERT | int | AD-Wert Tastereingang S2 |
| STAT_AD_S2_EINH | string | V |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ad-werte-kl30-kl15w"></a>
### STATUS_AD_Werte_Kl30_KL15W

Auslesen der AD-Werte Kl30/KL15W KWP2000: $30 InputOutputControlByLocalIdentifier $21 liefert Klemmenspannung $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KL30_WERT | int | AD-Wert KL 30 |
| STAT_KL30_EINH | string | V |
| STAT_KL15W_WERT | int | AD-Wert KL 15W |
| STAT_KL15W_EINH | string | V |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geschwindigkeit"></a>
### STATUS_GESCHWINDIGKEIT

Auslesen der Stati von Geschwindigkeit KWP2000: $30 InputOutputControlByLocalIdentifier $10 liefert Rad Geschwindigkeit $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DREHZAHL_WERT | int | Rad Geschwindigkeit vorne links |
| STAT_DREHZAHL_EINH | string | km/h |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kodierdaten"></a>
### STATUS_KODIERDATEN

Auslesen der Kodierdaten vom EMF KWP2000: $22 ReadDataByComonIdentifier $3000 CodingDataSet EMF1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KODIERDATEN_1 | string | Kodierdaten |
| STAT_KODIERDATEN_2 | string | Kodierdaten |
| STAT_KODIERDATEN_3 | string | Kodierdaten |
| STAT_KODIERDATEN_4 | string | Kodierdaten |
| STAT_KODIERDATEN_5 | string | Kodierdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-phy-ecu-hw-nr"></a>
### STATUS_PHY_ECU_HW_NR

Auslesen physikalischen ECU HW Nummer KWP2000: $1A  ReadECUIdentification $87  PECUHN Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PHY_ECU_HW_NR_1 | string | physikalischen ECU HW Nummer 1 |
| STAT_PHY_ECU_HW_NR_2 | string | physikalischen ECU HW Nummer 2 |
| STAT_PHY_ECU_HW_NR_3 | string | physikalischen ECU HW Nummer 3 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bmw-teile-nr"></a>
### STATUS_BMW_TEILE_NR

Auslesen der BMW_Teilenummer KWP2000: $1A  ReadECUIdentification $91  VMECUHN Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BMW_TEILE_NR_1 | string | BMW_Teilenummer 1 |
| STAT_BMW_TEILE_NR_2 | string | BMW_Teilenummer 2 |
| STAT_BMW_TEILE_NR_3 | string | BMW_Teilenummer 3 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bmw-codier-index"></a>
### STATUS_BMW_CODIER_INDEX

Auslesen des BMW Codierindex aus ZIF KWP2000: $1A  ReadECUIdentification $9B  VMCI Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BMW_CODIER_INX | char | BMW Codierindex aus ZIF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bmw-diag-index"></a>
### STATUS_BMW_DIAG_INDEX

Auslesen des BMW Diagnoseindex aus ZIF KWP2000: $1A  ReadECUIdentification $9C  VDCI Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BMW_DIAG_INX | int | BMW Diagindex aus ZIF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-programm-date"></a>
### STATUS_PROGRAMM_DATE

Ausgabe des Programming Date aus UIF KWP2000: $1A  ReadECUIdentification $99  PD Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PROGRAMM_DATE | string | BMW Diagindex aus ZIF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aif-lesen"></a>
### STATUS_AIF_LESEN

Auslesen des Anwender Informations Feldes $1A ReadECUIdentification KWP 2000: $86 CUIFDT Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_OFFSET | string | AIF Offset |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| AIF_PROGRAMMIER_DATUM | string | Datum der SG-Programmierung in der Form JJJJ.MM.TT |
| AIF_ZUSAMMENBAU_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_DATENSATZ_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_TESTER_NR | string | Tester Seriennummer |
| AIF_KM_STAND | long | km-Stand bei der Programmierung |
| AIF_PROGRAMM_STAND | string | Programmstandsnummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-er-festellkraft-lesen"></a>
### STATUS_ER_FESTELLKRAFT_LESEN

Auslesen der erreichten Festellkraft (N) KWP2000: $22 ReadDataByCommonIdentifier $0001 F_ERREICHT Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_F_ERREICHT_WERT | int | Bereich: 0-65535 |
| STAT_F_ERREICHT_EINH | string | N |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-akt-istposition-lesen"></a>
### STATUS_AKT_ISTPOSITION_LESEN

Aktuelle Istposition Stelleinheit [1/4 U] KWP2000: $22 ReadDataByCommonIdentifier $000_2 STAT_AKT_ISTPOS Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AKT_ISTPOS_WERT | int | Bereich: 0-65535 |
| STAT_AKT_ISTPOS_EINH | string | 1/4 U |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-letzte-loesepos-lesen"></a>
### STATUS_LETZTE_LOESEPOS_LESEN

Letzte Loeseposition [1/4 U] KWP2000: $22 ReadDataByCommonIdentifier $0003 STAT_LET_LOESPOS Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LET_LOESPOS_WERT | int | Bereich: 0-65535 |
| STAT_LET_LOESPOS_EINH | string | 1/4 U |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-letzte-anzugspos-lesen"></a>
### STATUS_LETZTE_ANZUGSPOS_LESEN

Letzte Anzugsposition [1/4 U] KWP2000: $22 ReadDataByCommonIdentifier $0004 STAT_LET_ANZUGSPOS Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LET_ANZUGSPOS_WERT | int | Bereich: 0-65535 |
| STAT_LET_ANZUGSPOS_EINH | string | 1/4 U |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-letzten-kraftein-lesen"></a>
### STATUS_LETZTEN_KRAFTEIN_LESEN

Letzter Krafteinsatzpunkt [1/4 U] KWP2000: $22 ReadDataByCommonIdentifier $0005 STAT_LET_KRAFTEIN Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LET_KRAFTEIN_WERT | int | Bereich: 0-65535 |
| STAT_LET_KRAFTEIN_EINH | string | 1/4 U |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betaetigungszaehler-lesen"></a>
### STATUS_BETAETIGUNGSZAEHLER_LESEN

Betaetigungszaehler (Anzahl Stellvorgaenge) KWP2000: $22 ReadDataByCommonIdentifier $0006 STAT_BET_ZAEHLER Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BET_ZAEHLER_WERT | int | Bereich: 0-65535 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-einbrems-zaehler-lesen"></a>
### STATUS_EINBREMS_ZAEHLER_LESEN

Einbremszaehler (Anzahl Einbremsvorgaenge) KWP2000: $22 ReadDataByCommonIdentifier $0007 STAT_ EINBREMS_ZAEH Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EINBREMS_ZAEH_WERT | int | Bereich: 0-65535 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-einbrems-strecke-lesen"></a>
### STATUS_EINBREMS_STRECKE_LESEN

Einbremsstrecke [m] KWP2000: $22 ReadDataByCommonIdentifier $0008 STAT_ EINBREMS_STRE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EINBREMS_STRE_WERT | int | Bereich: 0-65535 |
| STAT_EINBREMS_STRE_EINH | string | m |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spezialmodi"></a>
### STATUS_SPEZIALMODI

SPEzialmodi_lesen KWP2000: $22 ReadDataByCommonIdentifier $0012 STAT_ EINBREMS_STRE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPEZIALMODI_NR | int | Bereich: 0 - 1 |
| STAT_SPEZIALMODI_TEXT | string | 0=Montagemode_aus, 1=Montagemode_ein |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-krafteinsatz-setzen"></a>
### STEUERN_KRAFTEINSATZ_SETZEN

Stelleinheit Krafteinsatzpunkt setzen KWP2000: $2E WriteDataByCommonIdentifier $0010 RCI = SSS.KEP_SET Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KRAFT_EINS | int | Bereich: 0-65535 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-krafteinsatz-uebernehmen"></a>
### STEUERN_KRAFTEINSATZ_UEBERNEHMEN

Stelleinheit aktuellen Krafteinsatzpunkt uebernehmen KWP2000: $2E WriteDataByCommonIdentifier $0011 RCI = SSS.KEP_TAKE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spezialmodi"></a>
### STEUERN_SPEZIALMODI

Spezialmodi_einstellen KWP2000: $2E WriteDataByCommonIdentifier $0012 RCI = SPEZIAL_MODIS Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPEZIALMODUS | int | Bereich: 0-1, 1 = Montagemode_ein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-feststellen"></a>
### STEUERN_FESTSTELLEN

Feststellkraft nur fuer naechsten Anziehvorgang KWP2000: $3B WriteDataByCommonIdentifier $01 RLI = F_Feststellen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KRAFT | int | Bereich: 0-65535 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-personalisierung"></a>
### STEUERN_PERSONALISIERUNG

Feststellkraft nur fuer naechsten Anziehvorgang KWP2000: $3B WriteDataByCommonIdentifier $02 RLI = PERSONALISIERUNG Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KOMFORTMODUS | int | Bereich: 0-255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-komfortfunktion"></a>
### STEUERN_KOMFORTFUNKTION

Feststellkraft nur fuer naechsten Anziehvorgang KWP2000: $3B WriteDataByCommonIdentifier $03 RLI = KOMFORTFUNKTION Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHALTER | int | als Eingabe nur 1 fuer EIN und 0 fuer AUS moeglich |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-slog1-lesen"></a>
### STATUS_SLOG1_LESEN

Slog_Parameter_Block1 KWP2000: $22 ReadDataByCommonIdentifier $3001 STAT_SLOG1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ST_V1_APP_WERT | real | Bereich: 0-5 km/h |
| STAT_ST_V1_APP_EINH | string | km/h |
| STAT_ST_V2_APP_WERT | real | Bereich: 6-14 km/h |
| STAT_ST_V2_APP_EINH | string | km/h |
| STAT_V_VEH_OFFSET_WERT | real | Bereich: 0-5 km/h |
| STAT_V_VEH_OFFSET_EINH | string | km/h |
| STAT_ST_BSD_APP_WERT | long | Bereich: 2000-4500 N |
| STAT_ST_BSD_APP_EINH | string | Newton |
| STAT_LOESEWEG_WERT | long | Bereich: 200-400 |
| STAT_LOESEWEG_EINH | string | 1/4 U |
| STAT_V_BKLL_APP_WERT | real | Bereich: 0-5 km/h |
| STAT_V_BKLL_APP_EINH | string | km/h |
| STAT_T_ANF_RUECK_APP_WERT | real | Bereich: 0-3 s |
| STAT_T_ANF_RUECK_APP_EINH | string | sec |
| STAT_ANG_ACPD_APP_WERT | real | Bereich: 0-20 % |
| STAT_ANG_ACPD_APP_EINH | string | PROZENT |
| STAT_BRP_FAKTOR_WERT | real | Bereich: 1.0-2.0 |
| STAT_BRP_MIN_APP_WERT | int | Bereich: 0-40 bar |
| STAT_BRP_MIN_APP_EINH | string | Bar |
| STAT_VERSION_WERT | int | 255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-slog2-lesen"></a>
### STATUS_SLOG2_LESEN

Slog_Parameter_Block1 KWP2000: $22 ReadDataByCommonIdentifier $3002 STAT_SLOG2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DCRN_BRP_TAR_EMF_P_WERT | int | Bereich: 0-40 bar |
| STAT_DCRN_BRP_TAR_EMF_P_EINH | string | bar |
| STAT_DCRN_BRP_TAR_EMF_APP_WERT | int | Bereich: 10-50 bar |
| STAT_DCRN_BRP_TAR_EMF_APP_EINH | string | bar |
| STAT_ST_CFFU_EMF_BYTE1_WERT | string | hex eingeben |
| STAT_ST_CFFU_EMF_BYTE2_WERT | string | hex eingeben |
| STAT_T_SEC_COU_REL_APP_WERT | int | Bereich: 27-2500 h |
| STAT_T_SEC_COU_REL_APP_EINH | string | h |
| STAT_MILE_KM_APP_WERT | int | Bereich: 100-10000 km |
| STAT_MILE_KM_APP_EINH | string | km |
| STAT_ST_IBR_BRP_APP_WERT | int | Bereich: 100-1000 N |
| STAT_ST_IBR_BRP_APP_EINH | string | NEWTON |
| STAT_V_IBR_CONT_APP_WERT | real | Bereich: 5-25 km/h |
| STAT_V_IBR_CONT_APP_EINH | string | km/h |
| STAT_T_IBR_APP_WERT | int | Bereich: 0-60 s |
| STAT_T_IBR_APP_EINH | string | sec |
| STAT_VERSION_WERT | int | 255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-slog3-lesen"></a>
### STATUS_SLOG3_LESEN

Slog_Parameter_Block1 KWP2000: $22 ReadDataByCommonIdentifier $3003 STAT_SLOG3 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DCRN_DYN_BRP_APP_ENDTI_WERT | real | Bereich: 0-20 s |
| STAT_DCRN_DYN_BRP_APP_ENDTI_EINH | string | sec |
| STAT_DCRN_DYN_BRP_APP_FITI_WERT | real | Bereich: 0-10 s |
| STAT_DCRN_DYN_BRP_APP_FITI_EINH | string | sec |
| STAT_DCRN_DYN_BRP_APP_FI_WERT | real | Bereich: 1.5-6 m/s^2 |
| STAT_DCRN_DYN_BRP_APP_FI_EINH | string | m/s^2 |
| STAT_DCRN_DYN_BRP_APP_END_WERT | real | Bereich: 1.5-6 m/s^2 |
| STAT_DCRN_DYN_BRP_APP_END_EINH | string | m/s^2 |
| STAT_V_DYN_APP_WERT | real | Bereich: 0-5 km/h |
| STAT_V_DYN_APP_EINH | string | km/h |
| STAT_KEP_AENDERUNG_WERT | int |  |
| STAT_KEP_AENDERUNG_EINH | string | 1/4 U |
| STAT_V_IBR_DIAG_APP_WERT | real | Bereich: 30-60 km/h |
| STAT_V_IBR_DIAG_APP_EINH | string | km/h |
| STAT_AZP_AENDERUNG_WERT | int | Bereich: 30-60 km/h |
| STAT_AZP_AENDERUNG_EINH | string |  |
| STAT_VERSION_WERT | int | 255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sedec"></a>
### STATUS_SEDEC

Sedec-Status auslesen KWP2000: $22 ReadDataByCommonIdentifier $F1 RCI=SSS.SEDEC_STATUS Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEKTOR | int | Bereich: 0-9, keine Eingabe:alle Sektoren werden gelesen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SEDEC_STATUS_BYTE1_WERT | int | o.k. = 00 |
| STAT_SEDEC_STATUS_BYTE2_WERT | int | o.k. = 05 |
| STAT_ANZAHL_REPROGRAMMIERUNGEN_WERT | int |  |
| STAT_SEDEC_VERSION_BYTE1_WERT | int |  |
| STAT_SEDEC_VERSION_BYTE2_WERT | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-slog1-schreiben"></a>
### STEUERN_SLOG1_SCHREIBEN

SLOG-Parameter-Block1 KWP2000: $2E WriteDataByCommonIdentifier $3001 RCI = SLOG_PARA1 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ST_V1_APP | real | Bereich: 0-5 km/h |
| ST_V2_APP | real | Bereich: 6-14 km/h |
| V_VEH_OFFSET | real | Bereich: 0-5 km/h |
| ST_BSD_APP | real | Bereich: 2000-4500 N |
| LOESEWEG | int | Bereich: 200-400 U |
| V_BKLL_APP | real | Bereich: 0-10 km/h |
| T_ANF_RUECK_APP | real | Bereich: 0-5 s |
| ANG_ACPD_APP | real | Bereich: 0-20 % |
| BRP_FAKTOR | real | Bereich: 1.0-2.0 |
| BRP_MIN_APP | int | Bereich: 0-40 bar |
| version | int | 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-slog2-schreiben"></a>
### STEUERN_SLOG2_SCHREIBEN

SLOG-Parameter-Block2 KWP2000: $2E WriteDataByCommonIdentifier $3002 RCI = SLOG_PARA2 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DCRN_BRP_TAR_EMF_P | int | Bereich: 0-40 bar |
| DCRN_BRP_TAR_EMF_APP | int | Bereich: 10-50 bar |
| ST_CFFU_EMF_Byte1 | int | hex eingeben |
| ST_CFFU_EMF_Byte2 | int | hex eingeben |
| T_SEC_COU_REL_APP | int | Bereich: 27-2500 h |
| MILE_KM_APP | int | Bereich: 100-10000 km |
| ST_IBR_BRP_APP | real | Bereich: 100-1000 N |
| V_IBR_CONT_APP | real | Bereich: 5-25 km/h |
| T_IBR_APP | int | Bereich: 0-60 s |
| version | int | 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-slog3-schreiben"></a>
### STEUERN_SLOG3_SCHREIBEN

SLOG-Parameter-Block2 KWP2000: $2E WriteDataByCommonIdentifier $3003 RCI = SLOG_PARA3 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DCRN_DYN_BRP_APP_ENDTI | real | Bereich: 0 - 20 sec |
| DCRN_DYN_BRP_APP_FITI | real | Bereich: 0 - 10 sec |
| DCRN_DYN_BRP_APP_FI | real | Bereich: 1.5 - 6 m*m/sec |
| DCRN_DYN_BRP_APP_END | real | Bereich: 1.5 - 6 m*m/sec |
| V_DYN_APP | real | Bereich: 0 -5 km/h |
| KEP_AENDERUNG | real | Bereich: 0 - 1400 1/4 U |
| V_IBR_DIAG_APP | real | Bereich: 30 - 60 km/h |
| AZP_AENDERUNG | real | Bereich: 0 - 1400 1/4 U |
| version | int | 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-sar"></a>
### FS_LESEN_SAR

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-history-fs"></a>
### STATUS_HISTORY_FS

History-Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $22 RDBCI.DTCHM Modus  : Default

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

<a id="job-steuern-history-fs-loeschen"></a>
### STEUERN_HISTORY_FS_LOESCHEN

History-Fehlerspeicher loeschen KWP2000: $31 STRBLI.CHM Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-history-fs-loeschen-detail"></a>
### STEUERN_HISTORY_FS_LOESCHEN_DETAIL

History-Fehlerspeicher loeschen KWP2000: $31 STRBLI.CHM Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POSITION | int | gewaehlte Position |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-history-fs-detail"></a>
### STATUS_HISTORY_FS_DETAIL

History-Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $22 RDBCI.DTCHM Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POSITION | int | gewaehlte Position |

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
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_LZ | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_ART_ANZ | int | Anzahl der zusaetzlichen Fehlerarten Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_ARTi_NR   Index der i. Fehlerart (string) F_ARTi_TEXT Text  zur i. Fehlerart |
| F_UW_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (87 × 2)
- [LIEFERANTEN](#table-lieferanten) (65 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (31 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (6 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (32 × 5)
- [INPUT_STATIS](#table-input-statis) (1 × 8)
- [KL30_SPANNUNG](#table-kl30-spannung) (1 × 2)
- [EEPROM_FEHLER1](#table-eeprom-fehler1) (1 × 14)
- [EEPROM_FEHLER2](#table-eeprom-fehler2) (1 × 15)
- [FAILSAVE_STATIS](#table-failsave-statis) (1 × 8)
- [FAILSAVE_ANALOG](#table-failsave-analog) (1 × 3)
- [FAILSAVE_FEHLER_BITS](#table-failsave-fehler-bits) (1 × 14)
- [MOTOR_STATIS](#table-motor-statis) (1 × 7)
- [INPUT_MOTOR_SPANNUNGEN](#table-input-motor-spannungen) (1 × 3)
- [OUTPUT_FEHLER_BITS](#table-output-fehler-bits) (1 × 7)
- [INPUT_N_HALL](#table-input-n-hall) (1 × 3)
- [INPUT_MOTOR_POS](#table-input-motor-pos) (1 × 3)
- [INPUT_KLEMMEN_SPANNUNGEN](#table-input-klemmen-spannungen) (1 × 3)
- [MOTOR_TEMPERATUREN](#table-motor-temperaturen) (1 × 3)
- [SLOG_STATIS](#table-slog-statis) (1 × 7)
- [RDZ_W](#table-rdz-w) (1 × 2)
- [MOTOR_POS_ST](#table-motor-pos-st) (1 × 2)
- [COM_CAN_FEHLER_BITS_W](#table-com-can-fehler-bits-w) (1 × 9)
- [COM_CAN_FEHLER_BITS](#table-com-can-fehler-bits) (1 × 9)
- [COM_CAN_SIGNAL_FEHLER](#table-com-can-signal-fehler) (1 × 27)
- [COM_CAN_TIMEOUT_FEHLER](#table-com-can-timeout-fehler) (1 × 17)
- [FAILSAVE_CAN_STATUS_DSC](#table-failsave-can-status-dsc) (1 × 9)
- [RDZ](#table-rdz) (1 × 2)
- [CAN_RPM_GRB_NEGL](#table-can-rpm-grb-negl) (1 × 2)
- [CAN_V_VEH](#table-can-v-veh) (1 × 2)
- [MOTOR_STATIS_W](#table-motor-statis-w) (1 × 7)
- [CAN_T_SEC_COU_REL](#table-can-t-sec-cou-rel) (1 × 2)
- [INPUT_TASTER_SPANNUNGEN](#table-input-taster-spannungen) (1 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (168 × 9)
- [UB_A](#table-ub-a) (5 × 2)
- [UB_B](#table-ub-b) (5 × 2)
- [UB_C1](#table-ub-c1) (5 × 2)
- [UB_C2](#table-ub-c2) (5 × 2)
- [UB_C3](#table-ub-c3) (4 × 2)
- [UB_C4](#table-ub-c4) (4 × 2)
- [UB_C5](#table-ub-c5) (5 × 2)
- [UB_C6](#table-ub-c6) (4 × 2)
- [UB_C7](#table-ub-c7) (4 × 2)
- [UB_C8](#table-ub-c8) (5 × 2)
- [UB_D1](#table-ub-d1) (7 × 2)
- [UB_D2](#table-ub-d2) (7 × 2)
- [UB_E1](#table-ub-e1) (5 × 2)
- [UB_E2](#table-ub-e2) (5 × 2)
- [UB_E3](#table-ub-e3) (8 × 2)
- [UB_E4](#table-ub-e4) (5 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 87 rows × 2 columns

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
| ?A0? | ERROR_DIAG_PROT |
| ?A1? | ERROR_SG_ADRESSE |
| ?A2? | ERROR_SG_MAXANZAHL_AIF |
| ?A3? | ERROR_SG_GROESSE_AIF |
| ?A4? | ERROR_SG_ENDEKENNUNG_AIF |
| ?A5? | ERROR_SG_AUTHENTISIERUNG |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 65 rows × 2 columns

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
| 0x18 | Teves |
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
| 0x10 | Testbedingungen erfuellt |
| 0x11 | Testbedingungen noch nicht erfuellt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler wuerde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler wuerde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 16 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
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
| 0x10 | Testbedingungen erfuellt |
| 0x11 | Testbedingungen noch nicht erfuellt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler wuerde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler wuerde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-programmierstatus"></a>
### PROGRAMMIERSTATUS

Dimensions: 19 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Anlieferzustand |
| 0x01 | Normalbetrieb |
| 0x02 | nicht benutzt |
| 0x03 | Speicher geloescht |
| 0x04 | nicht benutzt |
| 0x05 | Signaturpruefung PAF nicht durchgefuehrt |
| 0x06 | Signaturpruefung DAF nicht durchgefuehrt |
| 0x07 | Programmprogrammiersitzung aktiv |
| 0x08 | Datenprogrammiersitzung aktiv |
| 0x09 | Hardwarereferenzeintrag fehlerhaft |
| 0x0A | Programmreferenzeintrag fehlerhaft |
| 0x0B | Referenzierungsfehler Hardware -&gt; Programm |
| 0x0C | Programm nicht vorhanden oder nicht vollstaendig |
| 0x0D | Datenreferenzeintrag fehlerhaft |
| 0x0E | Referenzierungsfehler Programm -&gt; Daten |
| 0x0F | Daten nicht vorhanden oder nicht vollstaendig |
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

Dimensions: 31 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x600D | ECU EEPROM |
| 0x600E | ECU EEPROM DATEN |
| 0x600F | ECU HW VERRIEGELUNG |
| 0x6010 | ECU ANZIEHEN DEFEKT |
| 0x6011 | ECU HALL |
| 0x6012 | ECU LOESEN DEFEKT |
| 0x6013 | ECU MOT KREIS |
| 0x6014 | ECU MOT ABBRUCH |
| 0x6015 | ECU ANSTEUER VERGLEICH |
| 0x601F | ECU TEMPERATUR |
| 0x6020 | PER EMF TASTE |
| 0x6022 | PER FREIGABE TG |
| 0x6023 | PER RDZ |
| 0x6025 | PER KL30 |
| 0x6026 | PER WAKE |
| 0x6030 | MECH STELLWEG |
| 0x6031 | MECH BLOCKIERT |
| 0x6032 | MECH ROLLERKENNUNG |
| 0x6033 | MECH KEP AZP |
| 0x6034 | MECH UEBERTEMPERATUR |
| 0x6040 | DSC INTF EMF S1 |
| 0x6041 | DSC EMF QUIT |
| 0x6042 | DSC HYDRAULIK |
| 0x6043 | DSC FREIGABE ABBRUCH |
| 0x6044 | DSC INTF EMF S2 |
| 0x6045 | DSC KEINE GESCHW. |
| 0x6046 | DSC FREIGABE |
| 0xD387 | CAN GENERAL |
| 0xD3bd | CAN RX SIGNAL |
| 0xd3be | CAN RX |
| 0xd3c2 | CAN TX |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 6 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxx0000 | 01 | kein passendes Fehlersymptom |
| xxxx0001 | 02 | Signal oder Wert oberhalb Schwelle |
| xxxx0010 | 03 | Signal oder Wert unterhalb Schwelle |
| xxxx0100 | 04 | kein Signal oder Wert  |
| xxxx1000 | 05 | unplausibles Signal oder Wert  |
| xxxxxxxx | 0 | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 32 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x600D | INPUT_STATIS | KL30_SPANNUNG | EEPROM_FEHLER1 | EEPROM_FEHLER2 |
| 0x600E | INPUT_STATIS | KL30_SPANNUNG | EEPROM_FEHLER1 | EEPROM_FEHLER2 |
| 0x600F | INPUT_STATIS | FAILSAVE_STATIS | FAILSAVE_ANALOG | FAILSAVE_FEHLER_BITS |
| 0x6010 | INPUT_STATIS | MOTOR_STATIS | INPUT_MOTOR_SPANNUNGEN | OUTPUT_FEHLER_BITS |
| 0x6012 | INPUT_STATIS | MOTOR_STATIS | INPUT_MOTOR_SPANNUNGEN | OUTPUT_FEHLER_BITS |
| 0x6013 | INPUT_STATIS | MOTOR_STATIS | INPUT_MOTOR_SPANNUNGEN | OUTPUT_FEHLER_BITS |
| 0x6011 | INPUT_STATIS | 0xFF | INPUT_N_HALL | INPUT_MOTOR_POS |
| 0x601F | INPUT_STATIS | FAILSAVE_STATIS | INPUT_KLEMMEN_SPANNUNGEN | MOTOR_TEMPERATUREN |
| 0x6020 | INPUT_STATIS | FAILSAVE_STATIS | INPUT_TASTER_SPANNUNGEN | INPUT_KLEMMEN_SPANNUNGEN |
| 0x6022 | INPUT_STATIS | FAILSAVE_STATIS | FAILSAVE_ANALOG | SLOG_STATIS |
| 0x6043 | INPUT_STATIS | FAILSAVE_STATIS | FAILSAVE_ANALOG | SLOG_STATIS |
| 0x6046 | INPUT_STATIS | FAILSAVE_STATIS | FAILSAVE_ANALOG | SLOG_STATIS |
| 0x6023 | INPUT_STATIS | FAILSAVE_STATIS | INPUT_KLEMMEN_SPANNUNGEN | RDZ_w |
| 0x6025 | INPUT_STATIS | FAILSAVE_STATIS | INPUT_KLEMMEN_SPANNUNGEN | 0xFE |
| 0x6026 | INPUT_STATIS | FAILSAVE_STATIS | INPUT_KLEMMEN_SPANNUNGEN | 0xFE |
| 0x6030 | INPUT_STATIS | MOTOR_STATIS | INPUT_KLEMMEN_SPANNUNGEN | MOTOR_POS_ST |
| 0x6031 | INPUT_STATIS | MOTOR_STATIS | INPUT_KLEMMEN_SPANNUNGEN | MOTOR_POS_ST |
| 0x6032 | INPUT_STATIS | MOTOR_STATIS | INPUT_KLEMMEN_SPANNUNGEN | MOTOR_POS_ST |
| 0x6033 | INPUT_STATIS | MOTOR_STATIS | INPUT_KLEMMEN_SPANNUNGEN | MOTOR_POS_ST |
| 0xD387 | INPUT_STATIS | FAILSAVE_STATIS | COM_CAN_FEHLER_BITS_w | INPUT_KLEMMEN_SPANNUNGEN |
| 0xD3C2 | INPUT_STATIS | FAILSAVE_STATIS | COM_CAN_FEHLER_BITS_w | INPUT_KLEMMEN_SPANNUNGEN |
| 0xD3BD | INPUT_STATIS | COM_CAN_FEHLER_BITS | COM_CAN_SIGNAL_FEHLER | - |
| 0xD3BE | INPUT_STATIS | COM_CAN_FEHLER_BITS | COM_CAN_TIMEOUT_FEHLER | INPUT_KLEMMEN_SPANNUNGEN |
| 0x6040 | INPUT_STATIS | FAILSAVE_STATIS | FAILSAVE_CAN_STATUS_DSC | INPUT_KLEMMEN_SPANNUNGEN |
| 0x6044 | INPUT_STATIS | FAILSAVE_STATIS | FAILSAVE_CAN_STATUS_DSC | INPUT_KLEMMEN_SPANNUNGEN |
| 0x6041 | INPUT_STATIS | FAILSAVE_STATIS | FAILSAVE_CAN_STATUS_DSC | INPUT_KLEMMEN_SPANNUNGEN |
| 0x6042 | INPUT_STATIS | FAILSAVE_STATIS | FAILSAVE_CAN_STATUS_DSC | INPUT_KLEMMEN_SPANNUNGEN |
| 0x6045 | INPUT_STATIS | RDZ | CAN_RPM_GRB_NEGL | CAN_V_VEH |
| 0x6014 | INPUT_STATIS | FAILSAVE_STATIS | MOTOR_STATIS_w | INPUT_KLEMMEN_SPANNUNGEN |
| 0x6015 | INPUT_STATIS | FAILSAVE_STATIS | MOTOR_STATIS_w | SLOG_STATIS |
| 0x6034 | INPUT_STATIS | CAN_T_SEC_COU_REL | MOTOR_STATIS_w | MOTOR_TEMPERATUREN |
| default | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-input-statis"></a>
### INPUT_STATIS

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 |

<a id="table-kl30-spannung"></a>
### KL30_SPANNUNG

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x08 |

<a id="table-eeprom-fehler1"></a>
### EEPROM_FEHLER1

Dimensions: 1 rows × 14 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 13 | 0x09 | 0x0A | 0x0B | 0x0C | 0x0D | 0x0E | 0x0F | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 |

<a id="table-eeprom-fehler2"></a>
### EEPROM_FEHLER2

Dimensions: 1 rows × 15 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 14 | 0x16 | 0x17 | 0x18 | 0x19 | 0x1A | 0x1B | 0x1C | 0x1D | 0x1E | 0x1F | 0x20 | 0x21 | 0x22 | 0x23 |

<a id="table-failsave-statis"></a>
### FAILSAVE_STATIS

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x24 | 0x25 | 0x26 | 0x27 | 0x28 | 0x29 | 0x2A |

<a id="table-failsave-analog"></a>
### FAILSAVE_ANALOG

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x2B | 0x2C |

<a id="table-failsave-fehler-bits"></a>
### FAILSAVE_FEHLER_BITS

Dimensions: 1 rows × 14 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 13 | 0x2D | 0x2E | 0x2F | 0x30 | 0x31 | 0x32 | 0x33 | 0x34 | 0x35 | 0x36 | 0x37 | 0x38 | 0x39 |

<a id="table-motor-statis"></a>
### MOTOR_STATIS

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x3A | 0x3B | 0x3C | 0x3D | 0x3E | 0x3F |

<a id="table-input-motor-spannungen"></a>
### INPUT_MOTOR_SPANNUNGEN

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x40 | 0x41 |

<a id="table-output-fehler-bits"></a>
### OUTPUT_FEHLER_BITS

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x42 | 0x43 | 0x44 | 0x45 | 0x46 | 0x47 |

<a id="table-input-n-hall"></a>
### INPUT_N_HALL

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x48 | 0x49 |

<a id="table-input-motor-pos"></a>
### INPUT_MOTOR_POS

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x4A | 0x4B |

<a id="table-input-klemmen-spannungen"></a>
### INPUT_KLEMMEN_SPANNUNGEN

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x4C | 0x4D |

<a id="table-motor-temperaturen"></a>
### MOTOR_TEMPERATUREN

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x4E | 0x4F |

<a id="table-slog-statis"></a>
### SLOG_STATIS

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x50 | 0x51 | 0x52 | 0x53 | 0x54 | 0x55 |

<a id="table-rdz-w"></a>
### RDZ_W

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x56 |

<a id="table-motor-pos-st"></a>
### MOTOR_POS_ST

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x57 |

<a id="table-com-can-fehler-bits-w"></a>
### COM_CAN_FEHLER_BITS_W

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x58 | 0x59 | 0x5A | 0x5B | 0x5C | 0x5D | 0x5E | 0xB2 |

<a id="table-com-can-fehler-bits"></a>
### COM_CAN_FEHLER_BITS

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x5F | 0x60 | 0x61 | 0x62 | 0x63 | 0x64 | 0x65 | 0xB3 |

<a id="table-com-can-signal-fehler"></a>
### COM_CAN_SIGNAL_FEHLER

Dimensions: 1 rows × 27 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR | UW17_NR | UW18_NR | UW19_NR | UW20_NR | UW21_NR | UW22_NR | UW23_NR | UW24_NR | UW25_NR | UW26_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 26 | 0x66 | 0x67 | 0x68 | 0x69 | 0x6A | 0x6B | 0x6C | 0x6D | 0x6E | 0x6F | 0x70 | 0x71 | 0x72 | 0x73 | 0x74 | 0x75 | 0x76 | 0x77 | 0x78 | 0x79 | 0x7A | 0x7B | 0x9C | 0x9D | 0xA2 | 0xA3 |

<a id="table-com-can-timeout-fehler"></a>
### COM_CAN_TIMEOUT_FEHLER

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x7C | 0x7D | 0x7E | 0x7F | 0x80 | 0x81 | 0x82 | 0x83 | 0x84 | 0x85 | 0x86 | 0x87 | 0x9E | 0x9F | 0xA0 | 0xA1 |

<a id="table-failsave-can-status-dsc"></a>
### FAILSAVE_CAN_STATUS_DSC

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x88 | 0x89 | 0x8A | 0x8B | 0x8C | 0x8D | 0x8E | 0x8F |

<a id="table-rdz"></a>
### RDZ

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x90 |

<a id="table-can-rpm-grb-negl"></a>
### CAN_RPM_GRB_NEGL

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x91 |

<a id="table-can-v-veh"></a>
### CAN_V_VEH

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x92 |

<a id="table-motor-statis-w"></a>
### MOTOR_STATIS_W

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x93 | 0x94 | 0x95 | 0x96 | 0x97 | 0x98 |

<a id="table-can-t-sec-cou-rel"></a>
### CAN_T_SEC_COU_REL

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x99 |

<a id="table-input-taster-spannungen"></a>
### INPUT_TASTER_SPANNUNGEN

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x9A | 0x9B |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 168 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | EMF Taste gedrueckt | 0/1 | - | 0x01 | - | - | - | - |
| 0x02 | HW Freigabe loesen | 0/1 | - | 0x02 | - | - | - | - |
| 0x03 | HW Freigabe anziehen | 0/1 | - | 0x04 | - | - | - | - |
| 0x04 | DSC P anziehen | 0/1 | - | 0x08 | - | - | - | - |
| 0x05 | KLEMME 15 EIN | 0/1 | - | 0x10 | - | - | - | - |
| 0x06 | EMF Unterspannung | 0/1 | - | 0x20 | - | - | - | - |
| 0x07 | Motordrehrichtung | 0-n | - | 0xC0 | ub_A | - | - | - |
| 0x08 | KLEMME 30 Spannung | VOLT | - | unsigned char | - | 1 | 10 | 0 |
| 0x09 | EE BLOCK IDENT EEPROM | 0/1 | low | 0x0001 | - | - | - | - |
| 0x0A | EE ERROR BLOCK KODIER 1 | 0/1 | low | 0x0002 | - | - | - | - |
| 0x0B | EE BLOCK MOTOR PARAMETER | 0/1 | low | 0x0008 | - | - | - | - |
| 0x0C | EE BLOCK MOTOR STATUS | 0/1 | low | 0x0010 | - | - | - | - |
| 0x0D | EE BLOCK SLOG STATUS | 0/1 | low | 0x0020 | - | - | - | - |
| 0x0E | EE BLOCK ABGLEICH PARAMETER | 0/1 | low | 0x0080 | - | - | - | - |
| 0x0F | EE BLOCK MOTOR STATUS 2 | 0/1 | low | 0x0100 | - | - | - | - |
| 0x10 | EE BLOCK FSP 1 | 0/1 | low | 0x0400 | - | - | - | - |
| 0x11 | EE BLOCK FSP 2 | 0/1 | low | 0x0800 | - | - | - | - |
| 0x12 | EE BLOCK FSP 3 | 0/1 | low | 0x1000 | - | - | - | - |
| 0x13 | EE BLOCK FSP 4 | 0/1 | low | 0x2000 | - | - | - | - |
| 0x14 | EE BLOCK FSP 5 | 0/1 | low | 0x4000 | - | - | - | - |
| 0x15 | EE BLOCK FSP 6 | 0/1 | low | 0x8000 | - | - | - | - |
| 0x16 | EE BLOCK FSP 7 | 0/1 | low | 0x0001 | - | - | - | - |
| 0x17 | EE BLOCK FSP 8 | 0/1 | low | 0x0002 | - | - | - | - |
| 0x18 | EE BLOCK FSP 9 | 0/1 | low | 0x0004 | - | - | - | - |
| 0x19 | EE BLOCK FSP 10 | 0/1 | low | 0x0008 | - | - | - | - |
| 0x1A | EE BLOCK FSP 11 | 0/1 | low | 0x0010 | - | - | - | - |
| 0x1B | EE BLOCK FSP 12 | 0/1 | low | 0x0020 | - | - | - | - |
| 0x1C | EE BLOCK FSP 13 | 0/1 | low | 0x0040 | - | - | - | - |
| 0x1D | EE BLOCK FSP 14 | 0/1 | low | 0x0080 | - | - | - | - |
| 0x1E | EE BLOCK FSP 15 | 0/1 | low | 0x0100 | - | - | - | - |
| 0x1F | EE BLOCK SLOG PARAMETER 1 | 0/1 | low | 0x0200 | - | - | - | - |
| 0x20 | EE BLOCK SLOG PARAMETER 2 | 0/1 | low | 0x0400 | - | - | - | - |
| 0x21 | EE BLOCK SLOG PARAMETER 3 | 0/1 | low | 0x0800 | - | - | - | - |
| 0x22 | EE BLOCK ERROR PARAMETER | 0/1 | low | 0x4000 | - | - | - | - |
| 0x23 | EE BLOCK SICHER | 0/1 | low | 0x8000 | - | - | - | - |
| 0x24 | EMF Taste S1 ein | 0/1 | - | 0x01 | - | - | - | - |
| 0x25 | EMF TASTE WURDE GEDRUECKT | 0/1 | - | 0x02 | - | - | - | - |
| 0x26 | V kommt von oben | 0/1 | - | 0x04 | - | - | - | - |
| 0x27 | Anfahren | 0/1 | - | 0x08 | - | - | - | - |
| 0x28 | KL30 Einbruch erkannt | 0/1 | - | 0x10 | - | - | - | - |
| 0x29 | Anfahren erkannt | 0/1 | - | 0x20 | - | - | - | - |
| 0x2A | CAN_ST_WR_RLS | 0-n | - | 0xC0 | ub_B | - | - | - |
| 0x2B | RDZ | km/h | - | unsigned char | - | 1 | 1 | 0 |
| 0x2C | Timer Loese Fenster | s | - | unsigned char | - | 1 | 100 | 0 |
| 0x2D | Freigabe Anziehen, obwohl v &gt; 13 km/h | 0/1 | low | 0x0001 | - | - | - | - |
| 0x2E | Keine Freigabe Loesen obwohl DSC_P = loesen | 0/1 | low | 0x0002 | - | - | - | - |
| 0x2F | Freigabe Anziehen, obwohl v &lt; 13 km/h, gueltig und keine Taste | 0/1 | low | 0x0004 | - | - | - | - |
| 0x30 | Keine Freigabe Anziehen, obwohl  v &lt; 7 km/h, gueltig und Taste | 0/1 | low | 0x0008 | - | - | - | - |
| 0x31 | Keine Freigabe Anziehen obwohl Taste | 0/1 | low | 0x0010 | - | - | - | - |
| 0x32 | Freigabe Loesen obwohl keine Taste | 0/1 | low | 0x0020 | - | - | - | - |
| 0x33 | Keine Freigabe Loesen trotz Taste | 0/1 | low | 0x0040 | - | - | - | - |
| 0x34 | Keine Freigabe Anziehen obwohl v &lt; 7 km/h | 0/1 | low | 0x0080 | - | - | - | - |
| 0x35 | Freigabe Anziehen obwohl keine Taste und Geschw. ungueltig | 0/1 | low | 0x0100 | - | - | - | - |
| 0x36 | Keine Freigabe Loesen obwohl Taste, Geschw. ungueltig | 0/1 | low | 0x0200 | - | - | - | - |
| 0x37 | Freigabe Loesen, obwohl keine Taste und Geschw. ungueltig | 0/1 | low | 0x0400 | - | - | - | - |
| 0x38 | Keine Freigabe Loesen, keine Taste und Geschw. ungueltig | 0/1 | low | 0x0800 | - | - | - | - |
| 0x39 | Freigabe Anziehen obwohl keine Taste und keine defekt Geschw. | 0/1 | low | 0x1000 | - | - | - | - |
| 0x3A | MotorState | 0-n | - | 0x07 | ub_D1 | - | - | - |
| 0x3B | Motor blockiert | 0/1 | - | 0x08 | - | - | - | - |
| 0x3C | Motor Spannungs Einbruch | 0/1 | - | 0x10 | - | - | - | - |
| 0x3D | KEP bestimmen | 0/1 | - | 0x20 | - | - | - | - |
| 0x3E | Hand Verstellung | 0/1 | - | 0x40 | - | - | - | - |
| 0x3F | Kalibriert | 0/1 | - | 0x80 | - | - | - | - |
| 0x40 | Motor Spannung 1 | VOLT | - | unsigned char | - | 1 | 10 | 0 |
| 0x41 | Motor Spannung 2 | VOLT | - | unsigned char | - | 1 | 10 | 0 |
| 0x42 | U Motor kreis defekt, mot kreis defekt | 0/1 | low | 0x0001 | - | - | - | - |
| 0x43 | U Motor bhs oder ahs 0V defekt | 0/1 | low | 0x0004 | - | - | - | - |
| 0x44 | U Motor ahs 12V defekt, loesen defekt | 0/1 | low | 0x0010 | - | - | - | - |
| 0x45 | U Motor ahs 5V defekt, loesen defekt | 0/1 | low | 0x0020 | - | - | - | - |
| 0x46 | U Motor bhs 12V defekt, anziehen defekt | 0/1 | low | 0x0400 | - | - | - | - |
| 0x47 | U Motor bhs 5V defekt, anziehen defekt | 0/1 | low | 0x0800 | - | - | - | - |
| 0x48 | N HALL Sensor 1 Flanken | Impulse | - | unsigned char | - | 1 | 1 | 0 |
| 0x49 | N HALL Sensor 2 Flanken |  Impulse | - | unsigned char | - | 1 | 1 | 0 |
| 0x4A | N HALL Sensor | 1/min | - | unsigned char | - | 64 | 1 | 0 |
| 0x4B | Position | 2 Umdrehungen | - | unsigned char | - | 4 | 1 | 0 |
| 0x4C | KL30 Spannung | VOLT | - | unsigned char | - | 1 | 10 | 0 |
| 0x4D | KL15 Spannung | VOLT | - | unsigned char | - | 1 | 10 | 0 |
| 0x4E | Motor Temperatur | Grad Celsius | - | unsigned char | - | 1 | 1 | 0 |
| 0x4F | Temperatursensor | Grad Celsius | - | unsigned char | - | 1 | 1 | 0 |
| 0x50 | ST EMF LOCA | 0-n | low | 0x0003 | ub_E1 | - | - | - |
| 0x51 | MOTOR ANGEZOGEN | 0/1 | low | 0x0004 | - | - | - | - |
| 0x52 | MOTOR GELOEST | 0/1 | low | 0x0008 | - | - | - | - |
| 0x53 | ST HYD RETA | 0-n | low | 0x0030 | ub_E2 | - | - | - |
| 0x54 | Funktionsmodell, Stillegungsstufen | 0-n | low | 0x01C0 | ub_E3 | - | - | - |
| 0x55 | SLOG_V | 0-n | low | 0x0600 | ub_E4 | - | - | - |
| 0x56 | RDZ | km/h | low | unsigned int | - | 1 | 1 | 0 |
| 0x57 | MOTOR POS STELLEINH | 1/4 Umdrehung | low | unsigned int | - | 1 | 1 | 0 |
| 0x58 | ERROR_NM_BUS_OFF | 0/1 | low | 0x0001 | - | - | - | - |
| 0x59 | ERROR_RX_OVERFLOW | 0/1 | low | 0x0002 | - | - | - | - |
| 0x5A | KL15_W | 0/1 | low | 0x0004 | - | - | - | - |
| 0x5B | Motor Startvorgang | 0/1 | low | 0x0008 | - | - | - | - |
| 0x5C | EMF NM in Normalbetrieb | 0/1 | low | 0x0010 | - | - | - | - |
| 0x5D | ERROR_TRANCEIVER_OFF | 0/1 | low | 0x0040 | - | - | - | - |
| 0x5E | ERROR_DIAG_BUFFER | 0/1 | low | 0x0080 | - | - | - | - |
| 0xB2 | EMF NM zuletzt WaitBussleep | 0/1 | low | 0x0020 | - | - | - | - |
| 0x5F | ERROR_NM_BUS_OFF | 0/1 | - | 0x01 | - | - | - | - |
| 0x60 | ERROR_RX_OVERFLOW | 0/1 | - | 0x02 | - | - | - | - |
| 0x61 | KL15_W | 0/1 | - | 0x04 | - | - | - | - |
| 0x62 | Motor Startvorgang | 0/1 | - | 0x08 | - | - | - | - |
| 0x63 | EMF NM in Normalbetrieb | 0/1 | - | 0x10 | - | - | - | - |
| 0x64 | ERROR_TRANCEIVER_OFF | 0/1 | - | 0x40 | - | - | - | - |
| 0x65 | ERROR_DIAG_BUFFER | 0/1 | - | 0x80 | - | - | - | - |
| 0xB3 | EMF NM zuletzt WaitBussleep | 0/1 | - | 0x20 | - | - | - | - |
| 0x66 | ERROR_T_SEC_COU_REL | 0/1 | low | 0x00000001 | - | - | - | - |
| 0x67 | ERROR_MILE_KM | 0/1 | low | 0x00000002 | - | - | - | - |
| 0x68 | ERROR_ST_CT_BON | 0/1 | low | 0x00000004 | - | - | - | - |
| 0x69 | ERROR_CLAS_WGH_SEAT_DR | 0/1 | low | 0x00000008 | - | - | - | - |
| 0x6A | ERROR_V_VEH | 0/1 | low | 0x00000010 | - | - | - | - |
| 0x6B | ERROR_ST_VEH_DVCO | 0/1 | low | 0x00000020 | - | - | - | - |
| 0x6C | ERROR_ST_CLCTR | 0/1 | low | 0x00000040 | - | - | - | - |
| 0x6D | ERROR_ST_INTF_DSC_EMF | 0/1 | low | 0x00000080 | - | - | - | - |
| 0x6E | ERROR_ST_SHFT_RQ_BRG | 0/1 | low | 0x00000100 | - | - | - | - |
| 0x6F | ERROR_ST_DEAC_CFFU | 0/1 | low | 0x00000200 | - | - | - | - |
| 0x70 | ERROR_ST_DCRN_AVL | 0/1 | low | 0x00000400 | - | - | - | - |
| 0x71 | ERROR_ST_RCPT_DSC_EMF | 0/1 | low | 0x00000800 | - | - | - | - |
| 0x72 | ERROR_ST_CT_BRPD | 0/1 | low | 0x00001000 | - | - | - | - |
| 0x73 | ERROR_BRP | 0/1 | low | 0x00002000 | - | - | - | - |
| 0x74 | ERROR_ST_KL_15 | 0/1 | low | 0x00004000 | - | - | - | - |
| 0x75 | ERROR_ST_KEY_PLGD | 0/1 | low | 0x00008000 | - | - | - | - |
| 0x76 | ERROR_ST_GR_GRB | 0/1 | low | 0x00010000 | - | - | - | - |
| 0x77 | ERROR_CTR_EMF_LOCA | 0/1 | low | 0x00020000 | - | - | - | - |
| 0x78 | ERROR_RPM_GRB_NEGL | 0/1 | low | 0x00040000 | - | - | - | - |
| 0x79 | ERROR_NO_KEY_PRSL_IMME | 0/1 | low | 0x00080000 | - | - | - | - |
| 0x7A | ERROR_ST_ENG_RUN | 0/1 | low | 0x00100000 | - | - | - | - |
| 0x7B | ERROR_ANG_ACPD | 0/1 | low | 0x00200000 | - | - | - | - |
| 0x7C | TIMEOUT_GESCHWINDIGKEIT | 0/1 | low | 0x0004 | - | - | - | - |
| 0x7D | TIMEOUT_GETRIEBEDATEN | 0/1 | low | 0x0008 | - | - | - | - |
| 0x7E | TIMEOUT_KILOMETERSTAND | 0/1 | low | 0x0010 | - | - | - | - |
| 0x7F | TIMEOUT_KLEMMENSTATUS | 0/1 | low | 0x0020 | - | - | - | - |
| 0x80 | TIMEOUT_STAT_DSC | 0/1 | low | 0x0040 | - | - | - | - |
| 0x81 | TIMEOUT_STAT_ZV_KLAPPEN | 0/1 | low | 0x0080 | - | - | - | - |
| 0x82 | TIMEOUT_GESCHWINDIGKEIT_RAD | 0/1 | low | 0x0100 | - | - | - | - |
| 0x83 | TIMEOUT_BEDIENUNG_FAHRWERK | 0/1 | low | 0x0800 | - | - | - | - |
| 0x84 | TIMEOUT_ENGINE_1 | 0/1 | low | 0x1000 | - | - | - | - |
| 0x85 | TIMEOUT_STAT_SITZBELEGUNG_GURT | 0/1 | low | 0x2000 | - | - | - | - |
| 0x86 | TIMEOUT_TORQUE_3 | 0/1 | low | 0x4000 | - | - | - | - |
| 0x87 | TIMEOUT_A_TEMP_RELATIVZEIT | 0/1 | low | 0x8000 | - | - | - | - |
| 0x88 | DSC_ST_INTF_DSC_EMF | 0-n | low | 0x0003 | ub_C1 | - | - | - |
| 0x89 | DSC_ST_RCPT_DSC_EMF | 0-n | low | 0x000C | ub_C2 | - | - | - |
| 0x8A | DSC_ST_SHFT_RQ_BRG | 0-n | low | 0x0030 | ub_C3 | - | - | - |
| 0x8B | EMF_ST_DCRN_BRP_TAR_EMF | 0-n | low | 0x00C0 | ub_C4 | - | - | - |
| 0x8C | DSC_ST_ABS | 0-n | low | 0x0300 | ub_C5 | - | - | - |
| 0x8D | DSC_ST_DEAC_CFFU | 0-n | low | 0x0C00 | ub_C6 | - | - | - |
| 0x8E | DSC_ST_WR_RLS | 0-n | low | 0x3000 | ub_C7 | - | - | - |
| 0x8F | DSC_ST_DCRN_AVL | 0-n | low | 0xC000 | ub_C8 | - | - | - |
| 0x90 | RDZ | km/h | - | unsigned char | - | 1 | 1 | 0 |
| 0x91 | CAN_RPM_GRB_NEGL | 1/min | low | unsigned int | - | 1 | 8 | 0 |
| 0x92 | CAN_V_VEH | km/h | low | unsigned int | - | 1 | 10 | 0 |
| 0x93 | MotorState | 0-n | low | 0x0007 | ub_D2 | - | - | - |
| 0x94 | Motor blockiert | 0/1 | low | 0x0008 | - | - | - | - |
| 0x95 | Motor Spannungs Einbruch | 0/1 | low | 0x0010 | - | - | - | - |
| 0x96 | KEP bestimmen | 0/1 | low | 0x0020 | - | - | - | - |
| 0x97 | Hand Verstellung | 0/1 | low | 0x0040 | - | - | - | - |
| 0x98 | Kalibriert | 0/1 | low | 0x0080 | - | - | - | - |
| 0x99 | CAN_T_SEC_COU_EREL_ungueltig | 0/1 | - | 0x01 | - | - | - | - |
| 0x9A | Taste S1 Spannung | VOLT | - | unsigned char | - | 1 | 10 | 0 |
| 0x9B | Taste S2 Spannung | VOLT | - | unsigned char | - | 1 | 10 | 0 |
| 0x9C | ERROR_ST_CT_BTL | 0/1 | low | 0x00400000 | - | - | - | - |
| 0x9D | ERROR_ST_KL_R | 0/1 | low | 0x00800000 | - | - | - | - |
| 0x9E | CHECKSUM_ALIVE_STAT_DSC | 0/1 | low | 0x0001 | - | - | - | - |
| 0x9F | CHECKSUM_ALIVE_GETRIEBEDATEN | 0/1 | low | 0x0002 | - | - | - | - |
| 0xA0 | CHECKSUM_ALIVE_GESCHWINDIGKEIT | 0/1 | low | 0x0200 | - | - | - | - |
| 0xA1 | CHECKSUM_ALIVE_TORQUE_3 | 0/1 | low | 0x0400 | - | - | - | - |
| 0xA2 | ER_SIGNAL_ERROR_V_WHL_RLH | 0/1 | low | 0x01000000 | - | - | - | - |
| 0xA3 | ER_SIGNAL_ERROR_V_WHL_RRH | 0/1 | low | 0x02000000 | - | - | - | - |
| 0xFE | ohne Bedeutung | - | low | unsigned int | - | 1 | 1 | 0 |
| 0xFF | ohne Bedeutung | - | - | unsigned char | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | - | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-ub-a"></a>
### UB_A

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | ANZIEHEN |
| 0x40 | LOESEN |
| 0x80 | STEHT |
| 0xC0 | ungueltig |
| 0xFF | unbekannter Fehler |

<a id="table-ub-b"></a>
### UB_B

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Anziehen erlaubt |
| 0x40 | Loesen erlaubt |
| 0x80 | falsch |
| 0xC0 | ungueltig |
| 0xFF | unbekannter Fehler |

<a id="table-ub-c1"></a>
### UB_C1

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | In Ordnung |
| 0x0001 | Keine Komfortfuntion moeglich |
| 0x0002 | defekt |
| 0x0003 | ungueltig |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-c2"></a>
### UB_C2

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | In Ordnung |
| 0x0004 | Plausibilitaetsfehler, Aktivitaetsfehler |
| 0x0008 | Timeoutfehler |
| 0x000C | ungueltig |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-c3"></a>
### UB_C3

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Keine_Bremsdruckanforderung |
| 0x0010 | Plausibilitaetsfehler, Aktivitaetsfehler |
| 0x0030 | ungueltig |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-c4"></a>
### UB_C4

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Keine Anforderung |
| 0x0040 | Druck oder Verzoegerungsanforderung |
| 0x00C0 | ungueltig |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-c5"></a>
### UB_C5

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | In Ordnung |
| 0x0100 | Rueckfallebene |
| 0x0200 | defekt |
| 0x0300 | ungueltig |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-c6"></a>
### UB_C6

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Komfortfunktion durchfuehrbar |
| 0x0400 | Komfortfunktion deaktivieren |
| 0x0C00 | ungueltig |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-c7"></a>
### UB_C7

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Anziehen erlaubt Loesen gesperrt |
| 0x1000 | Loesen erlaubt Anziehen gesperrt |
| 0x3000 | ungueltig |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-c8"></a>
### UB_C8

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | keine Anforderung |
| 0x4000 | Anforderung ACC akzeptiert |
| 0x8000 | Anforderung EMF akzeptiert |
| 0xC000 | ungueltig |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-d1"></a>
### UB_D1

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | INIT |
| 0x01 | WARTE STILLSTAND |
| 0x02 | IDLE |
| 0x03 | ANZIEHEN |
| 0x04 | LOESEN |
| 0x05 | NORMIEREN |
| 0xFF | unbekannter Fehler |

<a id="table-ub-d2"></a>
### UB_D2

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | INIT |
| 0x0001 | WARTE STILLSTAND |
| 0x0002 | IDLE |
| 0x0003 | ANZIEHEN |
| 0x0004 | LOESEN |
| 0x0005 | NORMIEREN |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-e1"></a>
### UB_E1

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Zustand unbekannt |
| 0x0001 | Geloest |
| 0x0002 | Halten |
| 0x0003 | ungueltig |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-e2"></a>
### UB_E2

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Zustand unbekannt |
| 0x0010 | Geloest |
| 0x0020 | Halten |
| 0x0030 | ungueltig |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-e3"></a>
### UB_E3

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Start |
| 0x0040 | Normale Funktion |
| 0x0080 | Kein Komfortmodus |
| 0x00C0 | Manueller Notmodus, keine dynamische Abbremsung |
| 0x0100 | Manueller Notmodus, nur dynamische Abbremsung |
| 0x0140 | Gesamtstillegung |
| 0x0180 | Stop |
| 0xFFFF | unbekannter Fehler |

<a id="table-ub-e4"></a>
### UB_E4

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | V 0-3 km/h |
| 0x0200 | V 3-1 0km/h |
| 0x0400 | V 10-250 km/h |
| 0x0600 | V ungueltig |
| 0xFFFF | unbekannter Fehler |
