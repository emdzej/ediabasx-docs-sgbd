# FRM_87.prg

- Jobs: [208](#jobs)
- Tables: [33](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | FRM_87 |
| ORIGIN | BMW EI-63 Kober |
| REVISION | 3.09 |
| AUTHOR | Lear Entwicklung Ahrens, Brose Gerstner |
| COMMENT | SGBD fuer FRMFA-E87 |
| PACKAGE | 1.33 |
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
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [I_STUFE_LESEN](#job-i-stufe-lesen) - Auslesen der I-Stufe KWP2000: $22 ReadDataByCommonIdentifier $100B I-Step Modus  : Default
- [I_STUFE_SCHREIBEN](#job-i-stufe-schreiben) - Beschreiben der I-Stufe Es muessen immer alle drei Argumente im Bereich von 0-65535 bzw. 0x0000-0xFFFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $100B I-Step Modus  : Default
- [READ_CODIER_INDEX](#job-read-codier-index) - KWP 2000: $21 ReadDataByLocalIdentifier $05 READ_CODING_INDEX Modus   : Default Auslesen der drei Codierindexe: AHL, FH, FRMFA Funktioniert nur bis FSV 4.4.1
- [READ_VARIANTE](#job-read-variante) - KWP 2000: $21 ReadDataByLocalIdentifier $06 VARIANTE Modus   : Default Auslesen der Variante des Steuergeraetes
- [STATUS_BETR_H_FRMFA](#job-status-betr-h-frmfa) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Betriebsstunden fuer FRMFA Status von PL2-FRMFA lesen Betriebsstunden des FRMFA lesen
- [STEUERN_BETR_H_FRMFA_LOESCHEN](#job-steuern-betr-h-frmfa-loeschen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Betriebsstunden fuer FRMFA Status von FRMFA schreiben Loeschen der Betriebsstunden des FRMFA
- [STATUS_BETR_H_FUNKTIONEN](#job-status-betr-h-funktionen) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $04 Betriebsstunden fuer alle Funktionen Status von FRMFA lesen Lesen der Betriebsstunden der einzelnen Lampenfunktionen des FRMFA
- [STEUERN_BETR_H_FUNKTIONEN_LOESCHEN](#job-steuern-betr-h-funktionen-loeschen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $04 Betriebsstunden fuer alle Funktionen Status von FRMFA schreiben Loeschen der Betriebsstunden aller Lampenfunktionen des FRMFA
- [STATUS_BETR_H_AMPERE](#job-status-betr-h-ampere) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $08 Betriebsstunden mit Ampereunterteilung Status von FRMFA lesen Lesen der bisherigen Stromverteilung des FRMFA
- [STEUERN_BETR_H_AMPERE](#job-steuern-betr-h-ampere) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $08 Betriebsstunden mit Ampereunterteilung Status von FRMFA schreiben Loeschen der bisherigen Stromverteilung des FRMFA
- [STATUS_DIGITAL_INPUTS](#job-status-digital-inputs) - Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $06 Digitale Inputs
- [STATUS_ANALOG_INPUTS](#job-status-analog-inputs) - Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $07 Analoge Inputs
- [STATUS_LAMPEN_DIGITAL](#job-status-lampen-digital) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 alle Dimmwerte an PWM-Ports Status von FRMFA lesen Auslesen der digitalen Stati (EIN/AUS) aller Lampen des FRMFA
- [STATUS_SCHLOSSNUESSE](#job-status-schlossnuesse) - Auslesen der Stati von den Schlossnuessen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $23 Schlossnuesse
- [STATUS_LWR_POSITION](#job-status-lwr-position) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $25 STATUS_LWR_POSITION
- [STEUERN_LAMPEN_DIGITAL](#job-steuern-lampen-digital) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $01 Dimmwert an PWM-Port Status von FRMFA schreiben Ausgewaehlte Lampe voll ein bzw. ausschalten
- [STEUERN_LAMPEN_PWM](#job-steuern-lampen-pwm) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $01 Dimmwert an PWM-Port Status von FRMFA schreiben Lampe mit PWM- bzw. Spannungswert ein- bzw. ausschalten
- [STATUS_DIMMWERT](#job-status-dimmwert) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 alle Dimmwerte an PWM-Ports Status von FRMFA lesen Dimmwerte aller Lampen auslesen
- [STATUS_SENSE_INPUTS](#job-status-sense-inputs) - Auslesen der Sensewerte der einzelnen Lampen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $05 Sense Inputs
- [STATUS_FENSTERHEBER](#job-status-fensterheber) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0E Stati der Fensterheber fuer FRMFA Status von PL2-FRMFA lesen Stati der einzelnen FH-Funktionen auslesen
- [STEUERN_FENSTERHEBER](#job-steuern-fensterheber) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0E Ansteuern FH Status von FRMFA schreiben Verfahren der Fensterheber, Fahrer, Beifahrer, beide
- [STEUERN_FENSTERHEBER_EINLERNEN](#job-steuern-fensterheber-einlernen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0E Ansteuern FH Status von FRMFA schreiben Dauer max. 7sec Einlernen der Fensterheber
- [STEUERN_FENSTERHEBER_MIT_EKS_EINLERNEN](#job-steuern-fensterheber-mit-eks-einlernen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1F Hublaenge zum Einlernen uebergeben und Einlernen starten Status von FRMFA schreiben Dauer ca. 14 sec Einlernen der Fensterheber
- [STEUERN_FENSTERHEBER_EINLERNEN_AUS_CODIERUNG](#job-steuern-fensterheber-einlernen-aus-codierung) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1F Hublaenge zum Einlernen aus Codierdaten lesen und Einlernen starten Status von FRMFA schreiben Dauer ca. 14 sec Einlernen der Fensterheber
- [STEUERN_FENSTERHEBER_DENORMIEREN](#job-steuern-fensterheber-denormieren) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $12 FH denormieren Status von FRMFA schreiben Denormieren der Fensterheber, ja nach Auswahl, Fahrer, Beifahrer, beide
- [STATUS_WIEDERHOLZAEHLER](#job-status-wiederholzaehler) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $20 Wiederholzaehler fuer FRMFA Status von PL2-FRMFA lesen Wiederholzaehler des FRMFA lesen
- [STEUERN_AL_EINSCHALTEN](#job-steuern-al-einschalten) - Abblendlicht ueber Diagnose ein- bzw. ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $22 Abblendlicht ein- bzw. ausschalten Status von FRMFA schreiben
- [STATUS_VERBAU_SPIEGEL](#job-status-verbau-spiegel) - KWP2000: $22 ReadDataByCommonIdentifier $3414 GM-Kodierdatenblock Kodierdaten von FRMFA lesen
- [STATUS_POSITION_SPIEGEL](#job-status-position-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $10 Position Spiegel fuer FRMFA Status von PL2-FRMFA lesen Abfrage der Position der beiden Aussenspiegel
- [STATUS_MEMORY_POSITION_SPIEGEL](#job-status-memory-position-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $1E Position Spiegel fuer FRMFA Status von PL2-FRMFA lesen Abfrage der MemoryPosition der beiden Aussenspiegel
- [STEUERN_MEMORY_POSITION_SPIEGEL](#job-steuern-memory-position-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $1E Position Spiegel fuer FRMFA Status von PL2-FRMFA schreiben Schreiben der MemoryPosition der beiden Aussenspiegel
- [STATUS_SPIEGEL_TASTER](#job-status-spiegel-taster) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0F Spiegelschalter fuer FRMFA Status von PL2-FRMFA lesen Auslesen der einzelnen Tasten der Spiegelschalters
- [STEUERN_POSITION_SPIEGEL](#job-steuern-position-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $10 Position Spiegel fuer FRMFA Status von FRMFA schreiben ausgewaehlten Spiegel in angegebene Position fahren
- [STEUERN_POSITION_DIREKT_SPIEGEL](#job-steuern-position-direkt-spiegel) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1D Position Spiegel fuer FRMFA Status von FRMFA schreiben ausgewaehlten Spiegel in angegebene Position fahren
- [STATUS_GURTBRINGER](#job-status-gurtbringer) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $27 Stati von Gurtbringer fuer FRMFA Status von PL2-FRMFA lesen
- [STEUERN_GURTBRINGER_INITIALISIERUNG](#job-steuern-gurtbringer-initialisierung) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $27 Stati von Gurtbringer fuer FRMFA Status von PL2-FRMFA schreiben
- [STEUERN_GURTBRINGER_POSITION](#job-steuern-gurtbringer-position) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $27 Stati von Gurtbringer fuer FRMFA Status von PL2-FRMFA schreiben
- [STEUERN_GURTBRINGER_RICHTUNG](#job-steuern-gurtbringer-richtung) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $27 Stati von Gurtbringer fuer FRMFA Status von PL2-FRMFA schreiben
- [STATUS_WARNBLINKEN](#job-status-warnblinken) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 Warnblinken Status von PL2-FRMFA lesen Status ob Warnblinken aktiv ist auslesen
- [STATUS_KINDERSICHERUNG](#job-status-kindersicherung) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 Kindersicherung Status von PL2-FRMFA lesen Status der Kindersicherung auslesen
- [STEUERN_KINDERSICHERUNG](#job-steuern-kindersicherung) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $13 Kindersicherung Status von FRMFA schreiben Betaetigung des Kindersicherungstasters simulieren
- [STATUS_SPIEGELHEIZUNG](#job-status-spiegelheizung) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $19 Spiegelheizung Status von PL2-FRMFA lesen Wert der Spiegelheizung auslesen
- [STEUERN_SPIEGELHEIZUNG](#job-steuern-spiegelheizung) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $19 Spiegelheizung Status von FRMFA schreiben Spiegelheizung mit speziellen Werten eischalten
- [STATUS_SPIEGEL_ABBLENDEN](#job-status-spiegel-abblenden) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $1A SPIEGEL_ABBLENDEN Status von PL2-FRMFA lesen Auslesen des Wertes, wie der Spiegel abgeblendet ist
- [STEUERN_SPIEGEL_ABBLENDEN](#job-steuern-spiegel-abblenden) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1A SPIEGEL_ABBLENDEN Status von FRMFA schreiben Abblenden der Aussenspiegel
- [STATUS_XENON_AL_EINSCHALTVERSUCHE](#job-status-xenon-al-einschaltversuche) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $1B Xenon-AL-Einschaltversuche Auslesen wie oft das Abblendlicht eingeschaltet wurde
- [STEUERN_XENON_AL_EINSCHALTVERSUCHE_LOESCHEN](#job-steuern-xenon-al-einschaltversuche-loeschen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1B Xenon-AL-Einschaltversuche Loeschen der AL-Einschaltversuche
- [STATUS_INNENBELEUCHTUNG_DAUERAUS](#job-status-innenbeleuchtung-daueraus) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $26 Xenon-AL-Einschaltversuche Auslesen, ob Innenlicht daueraus geschaltet wurde
- [STEUERN_INNENBELEUCHTUNG_DAUERAUS](#job-steuern-innenbeleuchtung-daueraus) - KWP2000: $30 InputOutputControlByLocalIdentifier $08 LongTermAdjustment $26 Innenbeleuchtung Dauerausschalten Innenbeleuchtung Dauerausschalten
- [STATUS_SENSE_LESEN](#job-status-sense-lesen) - Senseausgang fuer ausgewaehlte Lampe lesen, FRMFA KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $1C Senseausgang lesen Modus  : Default
- [STATUS_FH_SCHALTER](#job-status-fh-schalter) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $24 FH-Schalter fuer FRMFA Status von PL2-FRMFA lesen Auslesen der einzelnen Tasten der FH
- [STATUS_EE_FH_LOG_DATA](#job-status-ee-fh-log-data) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $21 EE_FH_LOG_DATA Lesen von EE_FH_LOG_DATA
- [STEUERN_EE_FH_LOG_DATA](#job-steuern-ee-fh-log-data) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 EE_FH_LOG_DATA Status von FRMFA schreiben Loeschen von EE_FH_LOG_DATA des FRMFA
- [_CODIERDATEN_BLOCK_LESEN_LEAR](#job-codierdaten-block-lesen-lear) - KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default
- [_CODIERDATEN_BLOCK_SCHREIBEN_LEAR](#job-codierdaten-block-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $xxxx Codierdaten Modus  : Codieren je nach Block
- [_CODIERDATEN_3000_LESEN_KOMPLETT_LEAR](#job-codierdaten-3000-lesen-komplett-lear) - Auslesen der kompletten Codierdaten im 3000-Bereich Auslesen der ALC-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [_CODIERDATEN_3400_LESEN_KOMPLETT_LEAR](#job-codierdaten-3400-lesen-komplett-lear) - Auslesen der kompletten Codierdaten im 3400-Bereich Auslesen der FRMFA-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [_CODIERDATEN_3100_LESEN_KOMPLETT_LESEN_LEAR](#job-codierdaten-3100-lesen-komplett-lesen-lear) - Auslesen der kompletten Codierdaten im 3100-Bereich KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [_CODIERDATEN_3500_LESEN_KOMPLETT_LEAR](#job-codierdaten-3500-lesen-komplett-lear) - Auslesen der kompletten Codierdaten im 3500-Bereich (FH) KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [_CODIERDATEN_3400_SCHREIBEN_AUS_DATEI_LEAR](#job-codierdaten-3400-schreiben-aus-datei-lear) - Beschreiben der Default-Codierdaten Beschreiben der FRMFA-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $34xx Codierdaten, Default Modus  : Default
- [_CODIERDATEN_3000_SCHREIBEN_AUS_DATEI_LEAR](#job-codierdaten-3000-schreiben-aus-datei-lear) - Beschreiben der Default-Codierdaten Beschreiben der ALC-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten, Default Modus  : Default
- [_CODIERDATEN_3100_SCHREIBEN_AUS_DATEI_LEAR](#job-codierdaten-3100-schreiben-aus-datei-lear) - Beschreiben der Default-Codierdaten fuer 3100-Bereich KWP2000: $2E WriteDataByCommonIdentifier $31xx Code in EEPROM Modus  : Default
- [_CODIERDATEN_KOMPLETT_SCHREIBEN_LEAR](#job-codierdaten-komplett-schreiben-lear) - Beschreiben der Default-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten ALC schreiben $31xx Code in EEPROM schreiben $34xx Codierdaten FRMFA schreiben $35xx Codierdaten FH schreiben Modus  : Default
- [_READ_IDENT_94_SSECUSON_LEAR](#job-read-ident-94-ssecuson-lear) - SystemSupplierECUSoftwareNumber KWP2000: $1A ReadECUIdentification Modus  : $94 SystemSupplierECUSoftwareNumber
- [_WRITE_CI_AHL_FH_LEAR](#job-write-ci-ahl-fh-lear) - Beschreiben der CI fuer AHL und FH KWP2000: $2E WriteDataByLocalIdentifier $05 CI Modus  : Default
- [READ_IDENT_PARAM](#job-read-ident-param) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : mit Angabe der ID_OPTION zum spezifischen ID_LESEN
- [WRITE_IDENT_93_SSECUHVN](#job-write-ident-93-ssecuhvn) - Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $3B WriteDataByLocalIdentifier $93 SystemSupplierECUHardwareVersionNumber Modus  : Default
- [READ_FVIN](#job-read-fvin) - liest die lange Fahrgestellnummer KWP 2000: $22 ReadDataByCommonIdentifier $1010 FVIN
- [WRITE_FVIN](#job-write-fvin) - schreibt die lange Fahrgestellnummer KWP 2000: $2E WriteDataByCommonIdentifier $1010 FVIN
- [FVIN_AUFTRAG](#job-fvin-auftrag) - lange Fahrgestellnummer schreiben und ruecklesen KWP 2000: $2E WriteDataByCommonIdentifier $1010 FVIN KWP 2000: $22 ReadDataByCommonIdentifier $1010 FVIN
- [STATUS_LWR_LESEN](#job-status-lwr-lesen) - Lesen eines Codierdatensatzes zur Unterscheidung zwischen dynamischer, automatischer und manueller LWR KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet
- [READ_ENERGY_SAVING_MODE](#job-read-energy-saving-mode) - Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode
- [_HERSTELLER_DATEN_LESEN_LEAR](#job-hersteller-daten-lesen-lear) - Auslesen der Herstellerdaten KWP2000: $22 ReadDataByCommonIdentifier $0004 Herstellerdaten
- [CBD_ZEICHN_INDEX_LESEN_LEAR](#job-cbd-zeichn-index-lesen-lear) - Auslesen des Aenderungsindex aus den Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier $3404 Aenderungs-Index Modus  : Default
- [_HERSTELLER_DATEN_SCHREIBEN_LEAR](#job-hersteller-daten-schreiben-lear) - Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $0004 Herstellerdaten
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F7F Fahrzeugauftrag Modus  : Default
- [C_FA_SCHREIBEN](#job-c-fa-schreiben) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F13 Fahrzeugauftrag Modus  : Default
- [_FLASH_PROG_STATUS_SCHREIBEN_LEAR](#job-flash-prog-status-schreiben-lear) - Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $02 FlashProgrammierstatus auf 1 setzen Modus  : Default
- [_STEUERN_DIAGNOSE_BROSE_FH_1](#job-steuern-diagnose-brose-fh-1) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $09 Diagnose job 1 fuer BROSE-FH Status von FRMFA schreiben
- [_STEUERN_DIAGNOSE_BROSE_FH_2](#job-steuern-diagnose-brose-fh-2) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0A Diagnose job 2 fuer BROSE-FH Status von FRMFA schreiben
- [_STEUERN_DIAGNOSE_BROSE_FH_3](#job-steuern-diagnose-brose-fh-3) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0B Diagnose job 3 fuer BROSE-FH Status von FRMFA schreiben
- [_STEUERN_DIAGNOSE_BROSE_FH_4](#job-steuern-diagnose-brose-fh-4) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0C Diagnose job 4 fuer BROSE-FH Status von FRMFA schreiben
- [_STEUERN_DIAGNOSE_BROSE_FH_5](#job-steuern-diagnose-brose-fh-5) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0D Diagnose job 5 fuer BROSE-FH Status von FRMFA schreiben
- [_READ_CAN_BUS_ERROR_LEAR](#job-read-can-bus-error-lear) - KWP 2000: $21 ReadDataByLocalIdentifier $03 CAN_BUS_ERROR Modus   : Default
- [_CLR_CAN_BUS_ERROR_LEAR](#job-clr-can-bus-error-lear) - KWP2000: $3B WriteDataByLocalIdentifier $03 CAN_BUS_ERROR Modus  : Default
- [_READ_REGISTER_U435_LEAR](#job-read-register-u435-lear) - KWP 2000: $21 ReadDataByLocalIdentifier $03 READ_REGISTER_U435 Modus   : Default
- [_WRITE_REGISTER_U435_LEAR](#job-write-register-u435-lear) - KWP2000: $3B WriteDataByLocalIdentifier $03 WRITE_REGISTER_U435 Modus  : Default
- [_RESET_KURZSCHLUSS_SPERRE](#job-reset-kurzschluss-sperre) - Kurzschlusssperre ueber Diagnose ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $18 Kurzschlusssperre ausschalten Status von FRMFA schreiben
- [STATUS_LAMPEN_KURZSCHLUSS](#job-status-lampen-kurzschluss) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $14 Lampenkurzschluss auslesen Status Lampenkurzschluesse (explizit) von FRMFA lesen
- [STATUS_LAMPEN_KURZSCHLUSS_WIEDERHOL_COUNTER](#job-status-lampen-kurzschluss-wiederhol-counter) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $15 Lampenkurzschluss Wiederholzaehler auslesen Status Lampenkurzschlusswiederholzaehler (explizit) von FRMFA lesen
- [STATUS_LAMPEN_KURZSCHLUSS_COUNTER](#job-status-lampen-kurzschluss-counter) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $16 Lampenkurzschluss Zaehler auslesen Status Lampenkurzschlusszaehler (explizit) von FRMFA lesen
- [STATUS_LAMPEN_KURZSCHLUSS_COUNTER_MAX](#job-status-lampen-kurzschluss-counter-max) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $17 Lampenkurzschluss Zaehler Maxwert auslesen Status des max. Wertes des Lampenkurzschlusszaehlers (explizit) von FRMFA lesen
- [STEUERN_SMC_BESTROMEN](#job-steuern-smc-bestromen) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $11 SMC bestromen Status von FRMFA schreiben Bestromung der SMCs einschalten
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
- [_WARTEZEIT_LEAR](#job-wartezeit-lear) - Wartezeit
- [STATUS_LAMPENAUSGANG_ENTPRELLT_LESEN](#job-status-lampenausgang-entprellt-lesen) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 alle Dimmwerte an PWM-Ports Status von FRMFA lesen entprellte Dimmwerte aller Lampen auslesen Modus  : Default
- [FG_NR_SMC_DEFAULT](#job-fg-nr-smc-default) - Beschreiben der VIN mit 0xff KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN Beschreiben der Fahrgestellnummer in beide SMC mit 0xff
- [READ_GURTBRINGER_FA_IDENT](#job-read-gurtbringer-fa-ident) - ident lesen des LIN-Slave GURTBRINGER_FA Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-GURTBRINGER Modus  : Default Auslesen der Identdaten der GURTBRINGER_FA
- [READ_GURTBRINGER_BF_IDENT](#job-read-gurtbringer-bf-ident) - ident lesen des LIN-Slave GURTBRINGER_BF Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-GURTBRINGER Modus  : Default Auslesen der Identdaten der GURTBRINGER_BF
- [C_FG_SCHREIBEN_GURTBRINGER_FA](#job-c-fg-schreiben-gurtbringer-fa) - Schreiben der FG-Nr. in den GURTBRINGER_FA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [C_FG_LESEN_GURTBRINGER_FA](#job-c-fg-lesen-gurtbringer-fa) - Lesen der FG-Nr. aus dem GURTBRINGER_FA KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier
- [C_FG_AUFTRAG_GURTBRINGER_FA](#job-c-fg-auftrag-gurtbringer-fa) - Schreiben und Lesen der FG-Nr. GURTBRINGER_FA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [C_FG_SCHREIBEN_GURTBRINGER_BF](#job-c-fg-schreiben-gurtbringer-bf) - Schreiben der FG-Nr. in den GURTBRINGER_BF KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [C_FG_LESEN_GURTBRINGER_BF](#job-c-fg-lesen-gurtbringer-bf) - Lesen der FG-Nr. aus dem GURTBRINGER_BF KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier
- [C_FG_AUFTRAG_GURTBRINGER_BF](#job-c-fg-auftrag-gurtbringer-bf) - Schreiben und Lesen der FG-Nr. GURTBRINGER_BF KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [C_AEI_SCHREIBEN_GURTBRINGER_FA](#job-c-aei-schreiben-gurtbringer-fa) - Schreiben des Aenderungsindex in den GURTBRINGER_FA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [C_AEI_LESEN_GURTBRINGER_FA](#job-c-aei-lesen-gurtbringer-fa) - Lesen des Aenderungsindex aus dem GURTBRINGER_FA KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier
- [C_AEI_AUFTRAG_GURTBRINGER_FA](#job-c-aei-auftrag-gurtbringer-fa) - Schreiben und Lesen des Aenderungsindex GURTBRINGER_FA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [C_AEI_SCHREIBEN_GURTBRINGER_BF](#job-c-aei-schreiben-gurtbringer-bf) - Schreiben des Aenderungsindex in den GURTBRINGER_BF KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [C_AEI_LESEN_GURTBRINGER_BF](#job-c-aei-lesen-gurtbringer-bf) - Lesen des Aenderungsindex aus dem GURTBRINGER_BF KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier
- [C_AEI_AUFTRAG_GURTBRINGER_BF](#job-c-aei-auftrag-gurtbringer-bf) - Schreiben und Lesen des Aenderungsindex GURTBRINGER_BF KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier
- [RESET_GURTBRINGER_FA](#job-reset-gurtbringer-fa) - Reset GURTBRINGER_FA KWP2000: $A6 LINGateway $11 Reset
- [RESET_GURTBRINGER_BF](#job-reset-gurtbringer-bf) - Reset GURTBRINGER_BF KWP2000: $A6 LINGateway $11 Reset
- [STEUERN_KURZHUB_DEAKTIVIEREN](#job-steuern-kurzhub-deaktivieren) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $28 Kurzhub Deaktivieren
- [STATUS_QUALITAET_FENSTERHEBERLAUF](#job-status-qualitaet-fensterheberlauf) - Qualitaetsbewertung Fensterheber
- [_STATUS_FH_ADAPTIONSSPEICHER_LESEN](#job-status-fh-adaptionsspeicher-lesen) - Adaptionsdaten Fensterheber KWP2000: $30 InputOutputControlByLocalIdentifier $18 ECHTZEITDATEN_BROSE_LESEN $01 ReportCurrentState

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

<a id="job-i-stufe-lesen"></a>
### I_STUFE_LESEN

Auslesen der I-Stufe KWP2000: $22 ReadDataByCommonIdentifier $100B I-Step Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| I_STEP_1 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |
| I_STEP_2 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |
| I_STEP_3 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-i-stufe-schreiben"></a>
### I_STUFE_SCHREIBEN

Beschreiben der I-Stufe Es muessen immer alle drei Argumente im Bereich von 0-65535 bzw. 0x0000-0xFFFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $100B I-Step Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_STEP_1 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |
| I_STEP_2 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |
| I_STEP_3 | unsigned int | Bereich: 0-65535 bzw. 0x0000-0xFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-codier-index"></a>
### READ_CODIER_INDEX

KWP 2000: $21 ReadDataByLocalIdentifier $05 READ_CODING_INDEX Modus   : Default Auslesen der drei Codierindexe: AHL, FH, FRMFA Funktioniert nur bis FSV 4.4.1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_INDEX_FRMFA | int | Codierindex der FRMFA-Codierdaten |
| CODIER_INDEX_ALC | int | Codierindex der ALC-Codierdaten |
| CODIER_INDEX_FH | int | Codierindex der FH-Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-variante"></a>
### READ_VARIANTE

KWP 2000: $21 ReadDataByLocalIdentifier $06 VARIANTE Modus   : Default Auslesen der Variante des Steuergeraetes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VARIANTE_WERT | int | Variante als Wert |
| VARIANTEN_BEZEICHNUNG | string | Bezeichnung der Variante des Steuergeraetes |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betr-h-frmfa"></a>
### STATUS_BETR_H_FRMFA

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Betriebsstunden fuer FRMFA Status von PL2-FRMFA lesen Betriebsstunden des FRMFA lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSZEIT_FRMFA_WERT | real | Betriebsstunden FRMFA auslesen |
| STAT_BETRIEBSZEIT_EINH | string | Einheit fuer Betriebszeit [min] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-betr-h-frmfa-loeschen"></a>
### STEUERN_BETR_H_FRMFA_LOESCHEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Betriebsstunden fuer FRMFA Status von FRMFA schreiben Loeschen der Betriebsstunden des FRMFA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betr-h-funktionen"></a>
### STATUS_BETR_H_FUNKTIONEN

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $04 Betriebsstunden fuer alle Funktionen Status von FRMFA lesen Lesen der Betriebsstunden der einzelnen Lampenfunktionen des FRMFA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSZEIT_FL_WERT | unsigned long | Betr_h Fernlicht, E92/E93: Abbiegelicht |
| STAT_BETRIEBSZEIT_AL_WERT | unsigned long | Betr_h Abblendlicht |
| STAT_BETRIEBSZEIT_SL_WERT | unsigned long | Betr_h Standlicht |
| STAT_BETRIEBSZEIT_NSW_WERT | unsigned long | Betr_h Nebelscheinwerfer |
| STAT_BETRIEBSZEIT_FRA_LINKS_WERT | unsigned long | Betr_h Fahrtrichtungsanzeiger links |
| STAT_BETRIEBSZEIT_FRA_RECHTS_WERT | unsigned long | Betr_h Fahrtrichtungsanzeiger rechts |
| STAT_BETRIEBSZEIT_BREMSLICHT_STUFE_1_WERT | unsigned long | Betr_h Bremslicht Stufe 1 |
| STAT_BETRIEBSZEIT_BREMSLICHT_STUFE_2_WERT | unsigned long | Betr_h Bremslicht Stufe 2 |
| STAT_BETRIEBSZEIT_NSL_WERT | unsigned long | Betr_h Nebelschlusslicht |
| STAT_BETRIEBSZEIT_RFL_WERT | unsigned long | Betr_h Rueckfahrlicht |
| STAT_BETRIEBSZEIT_EINH | string | Einheit fuer Betriebsstunden |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-betr-h-funktionen-loeschen"></a>
### STEUERN_BETR_H_FUNKTIONEN_LOESCHEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $04 Betriebsstunden fuer alle Funktionen Status von FRMFA schreiben Loeschen der Betriebsstunden aller Lampenfunktionen des FRMFA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betr-h-ampere"></a>
### STATUS_BETR_H_AMPERE

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $08 Betriebsstunden mit Ampereunterteilung Status von FRMFA lesen Lesen der bisherigen Stromverteilung des FRMFA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSZEIT_15A_20A_WERT | unsigned long | Betriebszeit mit 15A bis 20A |
| STAT_BETRIEBSZEIT_20A_25A_WERT | unsigned long | Betriebszeit mit 20A bis 25A |
| STAT_BETRIEBSZEIT_25A_28A_WERT | unsigned long | Betriebszeit mit 25A bis 28A |
| STAT_BETRIEBSZEIT_28A_31A_WERT | unsigned long | Betriebszeit mit 28A bis 31A |
| STAT_BETRIEBSZEIT_31A_34A_WERT | unsigned long | Betriebszeit mit 31A bis 34A |
| STAT_BETRIEBSZEIT_34A_37A_WERT | unsigned long | Betriebszeit mit 34A bis 37A |
| STAT_BETRIEBSZEIT_37A_40A_WERT | unsigned long | Betriebszeit mit 37A bis 40A |
| STAT_BETRIEBSZEIT_40A_WERT | unsigned long | Betriebszeit mit &gt; 40A |
| STAT_BETRIEBSZEIT_EINH | string | Einheit fuer Betriebsstunden |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-betr-h-ampere"></a>
### STEUERN_BETR_H_AMPERE

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $08 Betriebsstunden mit Ampereunterteilung Status von FRMFA schreiben Loeschen der bisherigen Stromverteilung des FRMFA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-inputs"></a>
### STATUS_DIGITAL_INPUTS

Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $06 Digitale Inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHALTER_LICHT_1_EIN | int | Lichtschalterstellung 1 (Standlicht) Lichtschalterstellung 1 + 2 (Abblendlicht) |
| STAT_SCHALTER_LICHT_2_EIN | int | Lichtschalterstellung 2 (FLC) Lichtschalterstellung 1 + 2 (Abblendlicht) |
| STAT_KLEMME_15_EIN | int | Klemme 15 ein |
| STAT_TASTER_WBL_EIN | int | Taster Warnblinklicht betaetigt |
| STAT_TASTER_NSW_EIN | int | Taster Nebelscheinwerfer betaetigt |
| STAT_TASTER_NSL_EIN | int | Taster Nebelschlussleuchte betaetigt |
| STAT_EINGANG_BLS_EIN | int | Bremslichtschalter ein |
| STAT_TASTER_FH_FA_EIN | int | Taster Fensterheber Fahrertuer ein |
| STAT_TASTER_FH_BF_EIN | int | Taster Fensterheber Fahrertuer ein |
| STAT_EINGANG_R_GANG_EIN | int | Rueckwaertsgang ein |
| STAT_TASTER_IB_EIN | int | Taster Innenbeleuchtung ein |
| STAT_SCHALTER_SL_EIN | int | Schalter Standlicht ein |
| STAT_SCHALTER_AL_EIN | int | Schalter Abblendlicht ein |
| STAT_SCHALTER_FLC_EIN | int | Schalter Fahrlichtkontrolle ein |
| STAT_SCHALTER_FRA_LINKS_TIPP_EIN | int | Tipp-Schalter Fahrtrichtungsanzeiger links ein |
| STAT_SCHALTER_FRA_LINKS_DAUER_EIN | int | Dauer-Schalter Fahrtrichtungsanzeiger links ein |
| STAT_SCHALTER_FRA_RECHTS_TIPP_EIN | int | Tipp-Schalter Fahrtrichtungsanzeiger rechts ein |
| STAT_SCHALTER_FRA_RECHTS_DAUER_EIN | int | Dauer-Schalter Fahrtrichtungsanzeiger rechts ein |
| STAT_TASTER_FH_FA_TIPP_EIN | int | Tipp-Taster Fensterheber Fahrertuer ein |
| STAT_TASTER_FH_FA_DAUER_EIN | int | Dauer-Taster Fensterheber Fahrertuer ein |
| STAT_TASTER_FH_BF_TIPP_EIN | int | Tipp-Taster Fensterheber Beifahrertuer ein |
| STAT_TASTER_FH_BF_DAUER_EIN | int | Dauer-Taster Fensterheber Beifahrertuer ein |
| STAT_SCHALTER_FL_EIN | int | Schalter Fernlicht ein |
| STAT_SCHALTER_LH_EIN | int | Taster Lichthupe ein |
| STAT_EINGANG_TK_VL_EIN | int | Tuerkontakt vorne links ein bitte result: STAT_EINGANG_TK_FAT_EIN verwenden |
| STAT_EINGANG_TK_VR_EIN | int | Tuerkontakt vorne rechts ein bitte result: STAT_EINGANG_TK_BFT_EIN verwenden |
| STAT_EINGANG_TK_HL_EIN | int | Tuerkontakt hinten links ein bitte result: STAT_EINGANG_TK_FATH_EIN verwenden |
| STAT_EINGANG_TK_HR_EIN | int | Tuerkontakt hinten rechts ein bitte result: STAT_EINGANG_TK_BFTH_EIN verwenden |
| STAT_EINGANG_TK_FAT_EIN | int | Tuerkontakt Fahrertuer ein |
| STAT_EINGANG_TK_BFT_EIN | int | Tuerkontakt Beifahrertuer ein |
| STAT_EINGANG_TK_FATH_EIN | int | Tuerkontakt Fahrertuer hinten ein |
| STAT_EINGANG_TK_BFTH_EIN | int | Tuerkontakt Beifahrertuer hinten ein |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-inputs"></a>
### STATUS_ANALOG_INPUTS

Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $07 Analoge Inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPANNUNG_SCHALTER_LICHT_1_WERT | real | Spannung Lichtschalterstellung 1 (Standlicht) Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_LICHT_2_WERT | real | Spannung Lichtschalterstellung 2 (Abblendlicht) Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_TASTER_NSW_NSL_WERT | real | Spannung Taster Nebelscheinwerfer/-schlusslicht Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_LWR_POTI_WERT | real | Spannung Poti LWR Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_BELADUNGSSENSOR_VORN_WERT | real | Spannung Sensor Hoehenstandsmesser vorne Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_BELADUNGSSENSOR_HINTEN_WERT | real | Spannung Sensor Hoehenstandsmesser hinten Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_KLEMME_30A_WERT | real | Spannung Klemme 30A Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_KLEMME_30B_WERT | real | Spannung Klemme 30B Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_SCHALTER_FRA_LINKS_WERT | real | Spannung Schalter Blinker links Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_FRA_RECHTS_WERT | real | Spannung Schalter Blinker rechts Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_MOTOR_FH_LINKS_WERT | real | Spannung Motor Fensterheber links Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_MOTOR_FH_RECHTS_WERT | real | Spannung Motor Fensterheber rechts Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_SCHALTER_FL_LH_WERT | real | Spannung Schalter Fernlicht / Lichthupe Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_FH_FA_WERT | real | Spannung Schalter Fensterheber Fahrerseite Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_FH_BF_WERT | real | Spannung Schalter Fensterheber Beifahrerseite Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SCHALTER_RFS_WERT | real | Spannung Schalter Rueckfahrscheinwerfer Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_KLEMME_15_WERT | real | Spannung Klemme 15 Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SENSOR_LWR_WERT | real | Spannungswert zur Diagnose fuer Spulenabriss Spannung Sensor LWR Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_BEHOERDEN_FZG_WERT | real | Spannung Eingang Behoerdenfahrzeug Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_SPIEGELHEIZUNG_WERT | real | Spannung Spiegelheizung Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_FH_FA_WERT | real | Spannung FH FA Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_FH_BF_WERT | real | Spannung FH BF Bereich: 0 V bis 18 V |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-digital"></a>
### STATUS_LAMPEN_DIGITAL

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 alle Dimmwerte an PWM-Ports Status von FRMFA lesen Auslesen der digitalen Stati (EIN/AUS) aller Lampen des FRMFA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSGANG_FL_LINKS_EIN | int | Fernlicht links, E92/E93: Abbiegelicht links |
| STAT_AUSGANG_FL_RECHTS_EIN | int | Fernlicht rechts, E92/E93: Abbiegelicht rechts |
| STAT_AUSGANG_AL_LINKS_EIN | int | Abblendlicht links |
| STAT_AUSGANG_AL_RECHTS_EIN | int | Abblendlicht rechts |
| STAT_AUSGANG_BEGRL_LINKS_EIN | int | Begrenzungslicht links |
| STAT_AUSGANG_BEGRL_RECHTS_EIN | int | Begrenzungslicht rechts |
| STAT_AUSGANG_NSW_LINKS_EIN | int | Nebelscheinwerfer links |
| STAT_AUSGANG_NSW_RECHTS_EIN | int | Nebelscheinwerfer rechts |
| STAT_AUSGANG_FRA_LINKS_VORN_EIN | int | Fahrtrichtungsanzeiger links vorne |
| STAT_AUSGANG_FRA_RECHTS_VORN_EIN | int | Fahrtrichtungsanzeiger rechts vorne |
| STAT_AUSGANG_FRA_LINKS_HINTEN_EIN | int | Fahrtrichtungsanzeiger links hinten |
| STAT_AUSGANG_FRA_RECHTS_HINTEN_EIN | int | Fahrtrichtungsanzeiger rechts hinten |
| STAT_AUSGANG_BREMSLICHT_LINKS_EIN | int | Bremslicht links |
| STAT_AUSGANG_BREMSLICHT_MITTE_EIN | int | Bremslicht rechts |
| STAT_AUSGANG_BREMSLICHT_RECHTS_EIN | int | Bremslicht mitte |
| STAT_AUSGANG_SL_BL_LINKS_1_EIN | int | Schlusslicht links 1, E92/E93: Tagfahrlicht links |
| STAT_AUSGANG_SL_BL_RECHTS_1_EIN | int | Schlusslicht rechts 1, E92/E93: Tagfahrlicht rechts |
| STAT_AUSGANG_SL_BL_LINKS_2_EIN | int | Schlusslicht links 2 |
| STAT_AUSGANG_SL_BL_RECHTS_2_EIN | int | Schlusslicht rechts 2 |
| STAT_AUSGANG_KZL_EIN | int | Kennzeichenlicht |
| STAT_AUSGANG_IBL_EIN | int | Innenbeleuchtung rechts |
| STAT_AUSGANG_NSL_LINKS_EIN | int | Nebelschlusslicht links |
| STAT_AUSGANG_NSL_RECHTS_EIN | int | Nebelschlusslicht rechts |
| STAT_AUSGANG_RFL_LINKS_EIN | int | Rueckfahrlicht links |
| STAT_AUSGANG_RFL_RECHTS_EIN | int | Rueckfahrlicht rechts |
| STAT_AUSGANG_BFD_LINKS_EIN | int | Break-Force-Display links |
| STAT_AUSGANG_BFD_RECHTS_EIN | int | Break-Force-Display rechts |
| STAT_AUSGANG_BEL_WBL_TASTE_EIN | int | Beleuchtung WBL-Taster |
| STAT_AUSGANG_FLC_LED_EIN | int | LED Fahrtlichtkontrolle |
| STAT_AUSGANG_VORFELD_BEL_EIN | int | LED Vorfeldbeleuchtung |
| STAT_AUSGANG_KL58G_EIN | int | Klemme 58G |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schlossnuesse"></a>
### STATUS_SCHLOSSNUESSE

Auslesen der Stati von den Schlossnuessen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $23 Schlossnuesse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHALTNUSS_STELLUNG_NULL_EIN | int | Schaltnuesse in Stellung Neutral |
| STAT_SCHALTNUSS_STELLUNG_ENTRIEGELN_EIN | int | Schaltnuesse in Stellung Entriegeln |
| STAT_SCHALTNUSS_STELLUNG_SICHERN_EIN | int | Schaltnuesse in Stellung Sichern |
| STAT_SCHALTNUSS_STELLUNG_UNGUELTIG_EIN | int | Schaltnuesse in Stellung Ungueltig |
| STAT_SCHALTNUSS_STELLUNG_1_EIN | int | Schaltnuesse in Stellung 1 |
| STAT_SCHALTNUSS_STELLUNG_2_EIN | int | Schaltnuesse in Stellung 2 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lwr-position"></a>
### STATUS_LWR_POSITION

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $25 STATUS_LWR_POSITION

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_STATUS_LWR_POSITION | int | Position der Schrittmotoren auslesen je nach Scheinwerfer max. von 0 bis 1000 Halbschritte der Arbeitspunkt haengt von Fahrzeugtyp und Scheinwerfer ab und ist kodierbar |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lampen-digital"></a>
### STEUERN_LAMPEN_DIGITAL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $01 Dimmwert an PWM-Port Status von FRMFA schreiben Ausgewaehlte Lampe voll ein bzw. ausschalten

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

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $01 Dimmwert an PWM-Port Status von FRMFA schreiben Lampe mit PWM- bzw. Spannungswert ein- bzw. ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table LampNrTexte NAME TEXT Lampe aus Tabelle auswaehlen |
| PWM_WERT | int | je nach Auswahl mit 0x 0000 UUUU UUUU UUUU = Spannungsnachregelung 0001 PPPP PPPP PPPP = Prozent Einschaltdauer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dimmwert"></a>
### STATUS_DIMMWERT

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 alle Dimmwerte an PWM-Ports Status von FRMFA lesen Dimmwerte aller Lampen auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUSGANG_FL_LINKS_WERT | int | Dimmwert Fernlicht links, E92/E93: Abbiegelicht links |
| STAT_AUSGANG_FL_RECHTS_WERT | int | Dimmwert Fernlicht rechts, E92/E93: Abbiegelicht rechts |
| STAT_AUSGANG_AL_LINKS_WERT | int | Dimmwert Abblendlicht links |
| STAT_AUSGANG_AL_RECHTS_WERT | int | Dimmwert Abblendlicht rechts |
| STAT_AUSGANG_BEGRL_LINKS_WERT | int | Dimmwert Begrenzungslicht links |
| STAT_AUSGANG_BEGRL_RECHTS_WERT | int | Dimmwert Begrenzungslicht rechts |
| STAT_AUSGANG_NSW_LINKS_WERT | int | Dimmwert Nebelscheinwerfer links |
| STAT_AUSGANG_NSW_RECHTS_WERT | int | Dimmwert Nebelscheinwerfer rechts |
| STAT_AUSGANG_FRA_LINKS_VORN_WERT | int | Dimmwert Fahrtrichtungsanzeiger links vorne |
| STAT_AUSGANG_FRA_RECHTS_VORN_WERT | int | Dimmwert Fahrtrichtungsanzeiger rechts vorne |
| STAT_AUSGANG_FRA_LINKS_HINTEN_WERT | int | Dimmwert Fahrtrichtungsanzeiger links hinten |
| STAT_AUSGANG_FRA_RECHTS_HINTEN_WERT | int | Dimmwert Fahrtrichtungsanzeiger rechts hinten |
| STAT_AUSGANG_BREMSLICHT_LINKS_WERT | int | Dimmwert Bremslicht links |
| STAT_AUSGANG_BREMSLICHT_MITTE_WERT | int | Dimmwert Bremslicht rechts |
| STAT_AUSGANG_BREMSLICHT_RECHTS_WERT | int | Dimmwert Bremslicht mitte |
| STAT_AUSGANG_SL_BL_LINKS_1_WERT | int | Dimmwert Schlusslicht links 1, E92/E93: Tagfahrlicht links |
| STAT_AUSGANG_SL_BL_RECHTS_1_WERT | int | Dimmwert Schlusslicht rechts 1, E92/E93: Tagfahrlicht rechts |
| STAT_AUSGANG_SL_BL_LINKS_2_WERT | int | Dimmwert Schlusslicht links 2 |
| STAT_AUSGANG_SL_BL_RECHTS_2_WERT | int | Dimmwert Schlusslicht rechts 2 |
| STAT_AUSGANG_KZL_WERT | int | Dimmwert Kennzeichenlicht |
| STAT_AUSGANG_IBL_WERT | int | Dimmwert Innenbeleuchtung rechts |
| STAT_AUSGANG_NSL_LINKS_WERT | int | Dimmwert Nebelschlusslicht links |
| STAT_AUSGANG_NSL_RECHTS_WERT | int | Dimmwert Nebelschlusslicht rechts |
| STAT_AUSGANG_RFL_LINKS_WERT | int | Dimmwert Rueckfahrlicht links |
| STAT_AUSGANG_RFL_RECHTS_WERT | int | Dimmwert Rueckfahrlicht rechts |
| STAT_AUSGANG_BFD_LINKS_WERT | int | Dimmwert Break-Force-Display links |
| STAT_AUSGANG_BFD_RECHTS_WERT | int | Dimmwert Break-Force-Display rechts |
| STAT_AUSGANG_BEL_WBL_TASTE_WERT | int | Dimmwert Beleuchtung WBL-Taster |
| STAT_AUSGANG_FLC_LED_WERT | int | Dimmwert LED Fahrtlichtkontrolle |
| STAT_AUSGANG_VORFELD_BEL_WERT | int | Dimmwert LED Vorfeldbeleuchtung |
| STAT_AUSGANG_KL58G_WERT | int | Dimmwert Klemme 58G |
| STAT_AUSGANG_DIMMWERT_EINH | string | Einheit fuer Dimmwert |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sense-inputs"></a>
### STATUS_SENSE_INPUTS

Auslesen der Sensewerte der einzelnen Lampen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $05 Sense Inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SENSE_POL_L_WERT | real | Spannung Sensor Positionslicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_POL_R_WERT | real | Spannung Sensor Positionslicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_AL_L_WERT | real | Spannung Sensor Abblendlicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_AL_R_WERT | real | Spannung Sensor Abblendlicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_FL_L_WERT | real | Spannung Sensor Fernlicht links, E92/E93: Abbiegelicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_FL_R_WERT | real | Spannung Sensor Fernlicht rechts, E92/E93: Abbiegelicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_NSW_L_WERT | real | Spannung Sensor Nebelscheinwerfer links Bereich: 0 V bis 5 V |
| STAT_SENSE_NSW_R_WERT | real | Spannung Sensor Nebelscheinwerfer rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_1_SL_L_WERT | real | Spannung Sensor Standlicht 1 links, E92/E93: Tagfahrlicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_1_SL_R_WERT | real | Spannung Sensor Standlicht 1 rechts, E92/E93: Tagfahrlicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_2_SL_L_WERT | real | Spannung Sensor Standlicht 2 links Bereich: 0 V bis 5 V |
| STAT_SENSE_2_SL_R_WERT | real | Spannung Sensor Standlicht 2 rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_RFS_L_WERT | real | Spannung Sensor Rueckfahrscheinwerfer links Bereich: 0 V bis 5 V |
| STAT_SENSE_RFS_R_WERT | real | Spannung Sensor Rueckfahrscheinwerfer rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_NSL_L_WERT | real | Spannung Sensor Nebelschlusslicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_NSL_R_WERT | real | Spannung Sensor Nebelschlusslicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_VL_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger vorne links Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_VR_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger vorne rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_HL_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger hinten links Bereich: 0 V bis 5 V |
| STAT_SENSE_FRA_HR_WERT | real | Spannung Sensor Fahrtrichtungsanzeiger hinten rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_BL_L_WERT | real | Spannung Sensor Bremslicht links Bereich: 0 V bis 5 V |
| STAT_SENSE_BL_R_WERT | real | Spannung Sensor Bremslicht rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_KZL_WERT | real | Spannung Sensor Kennzeichenlicht Bereich: 0 V bis 5 V |
| STAT_SENSE_BL_M_WERT | real | Spannung Sensor Bremslicht mitte Bereich: 0 V bis 5 V |
| STAT_SENSE_BFD_L_WERT | real | Spannung Sensor BFD links Bereich: 0 V bis 5 V |
| STAT_SENSE_BFD_R_WERT | real | Spannung Sensor BFD rechts Bereich: 0 V bis 5 V |
| STAT_SENSE_IB_WERT | real | Spannung Sensor Innenbeleuchtung Bereich: 0 V bis 5 V |
| STAT_SENSE_KL_58G_WERT | real | Spannung Sensor Klemme 58G Bereich: 0 V bis 5 V |
| STAT_SENSE_PWM_1_WERT | real | Spannung Sensor PWM 1 Bereich: 0 V bis 5 V |
| STAT_SENSE_PWM_2_WERT | real | Spannung Sensor PWM 2 Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fensterheber"></a>
### STATUS_FENSTERHEBER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0E Stati der Fensterheber fuer FRMFA Status von PL2-FRMFA lesen Stati der einzelnen FH-Funktionen auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FA_FH_OFFEN_KOMPLETT | int | Fensterheber Fahrer komplett offen |
| STAT_BF_FH_OFFEN_KOMPLETT | int | Fensterheber Beifahrer komplett offen |
| STAT_FA_FH_GESCHLOSSEN | int | Fensterheber Fahrer geschlossen |
| STAT_BF_FH_GESCHLOSSEN | int | Fensterheber Beifahrer geschlossen |
| STAT_FA_FH_FAEHRT_EIN | int | Fensterheber Fahrer faehrt |
| STAT_FA_FH_FAEHRT_AUF_EIN | int | Fensterheber Fahrer faehrt auf |
| STAT_FA_FH_FAEHRT_ZU_EIN | int | Fensterheber Fahrer faehrt zu |
| STAT_BF_FH_FAEHRT_EIN | int | Fensterheber Beifahrer faehrt |
| STAT_BF_FH_FAEHRT_AUF_EIN | int | Fensterheber Beifahrer faehrt auf |
| STAT_BF_FH_FAEHRT_ZU_EIN | int | Fensterheber Beifahrer faehrt zu |
| STAT_FA_FH_EINGELERNT_EIN | int | Fensterheber Fahrer eingelernt |
| STAT_BF_FH_EINGELERNT_EIN | int | Fensterheber Beifahrer eingelernt |
| STAT_FA_FH_POSITION_WERT | int | Position Fensterheber Fahrer, nur bei eingelerntem FH |
| STAT_BF_FH_POSITION_WERT | int | Position Fensterheber Beifahrer, nur bei eingelerntem FH |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber"></a>
### STEUERN_FENSTERHEBER

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0E Ansteuern FH Status von FRMFA schreiben Verfahren der Fensterheber, Fahrer, Beifahrer, beide

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RICHTUNG_FH_FAT | string | table FH_Richtung NAME TEXT Auswahl der Richtung, in der das Fahrertuerfenster verfahren soll |
| ANSTEUER_ZEIT_FAT | int | Zeit in 100ms, die der FH angesteuert werden soll, d.h. 1 = 100ms |
| RICHTUNG_FH_BFT | string | table FH_Richtung NAME TEXT Auswahl der Richtung, in der das Beiahrertuerfenster verfahren soll |
| ANSTEUER_ZEIT_BFT | int | Zeit in 100ms, die der FH angesteuert werden soll, d.h. 1 = 100ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-einlernen"></a>
### STEUERN_FENSTERHEBER_EINLERNEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0E Ansteuern FH Status von FRMFA schreiben Dauer max. 7sec Einlernen der Fensterheber

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FH | string | table Auswahl_Fenster NAME TEXT Auswahl des Fensters, dass eingelernt werden soll, Fahrer, Beifahrer, beide |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-mit-eks-einlernen"></a>
### STEUERN_FENSTERHEBER_MIT_EKS_EINLERNEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1F Hublaenge zum Einlernen uebergeben und Einlernen starten Status von FRMFA schreiben Dauer ca. 14 sec Einlernen der Fensterheber

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HUBLAENGE_FH_FAT | unsigned int | Hublaenge zum Einlernen der FH-Fahrertuer bei 0 wird der FH nicht eingelernt |
| HUBLAENGE_FH_BFT | unsigned int | Hublaenge zum Einlernen der FH-Beifahrertuer bei 0 wird der FH nicht eingelernt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-einlernen-aus-codierung"></a>
### STEUERN_FENSTERHEBER_EINLERNEN_AUS_CODIERUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1F Hublaenge zum Einlernen aus Codierdaten lesen und Einlernen starten Status von FRMFA schreiben Dauer ca. 14 sec Einlernen der Fensterheber

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FH | string | table Auswahl_Fenster NAME TEXT Auswahl des Fensterhebers, der eingelernt werden soll, Fahrer, Beifahrer, beide |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fensterheber-denormieren"></a>
### STEUERN_FENSTERHEBER_DENORMIEREN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $12 FH denormieren Status von FRMFA schreiben Denormieren der Fensterheber, ja nach Auswahl, Fahrer, Beifahrer, beide

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_FH | string | table Auswahl_Fenster NAME TEXT Auswahl des Fensterhebers, der denormiert werden soll, Fahrer, Beifahrer, beide |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wiederholzaehler"></a>
### STATUS_WIEDERHOLZAEHLER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $20 Wiederholzaehler fuer FRMFA Status von PL2-FRMFA lesen Wiederholzaehler des FRMFA lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WIEDERHOLZAEHLER_ASP_BEIKLAPPEN_WERT | int | Wiederholzaehler Aussenspiegel Beiklappen auslesen |
| STAT_WIEDERHOLZAEHLER_VORFELDBELEUCHTUNG_WERT | unsigned int | Wiederholzaehler Vorfeldbeleuchtung auslesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-al-einschalten"></a>
### STEUERN_AL_EINSCHALTEN

Abblendlicht ueber Diagnose ein- bzw. ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $22 Abblendlicht ein- bzw. ausschalten Status von FRMFA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AL_EIN_AUS | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-verbau-spiegel"></a>
### STATUS_VERBAU_SPIEGEL

KWP2000: $22 ReadDataByCommonIdentifier $3414 GM-Kodierdatenblock Kodierdaten von FRMFA lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPIEGEL_LIN | int | LIN-Spiegel kodiert/verbaut |
| STAT_LIN_SCHALTER_BLOCK | int | LIN-Schalterblock kodiert/verbaut |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-position-spiegel"></a>
### STATUS_POSITION_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $10 Position Spiegel fuer FRMFA Status von PL2-FRMFA lesen Abfrage der Position der beiden Aussenspiegel

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_POS_SPIEGEL_FAHRER_HOR_WERT | int | Position Fahrerspiegel horizontal |
| STAT_POS_SPIEGEL_BEIFAHRER_HOR_WERT | int | Position Beifahrerspiegel horizontal |
| STAT_POS_SPIEGEL_FAHRER_VER_WERT | int | Position Fahrerspiegel vertikal |
| STAT_POS_SPIEGEL_BEIFAHRER_VER_WERT | int | Position Beifahrerspiegel vertikal |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-memory-position-spiegel"></a>
### STATUS_MEMORY_POSITION_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $1E Position Spiegel fuer FRMFA Status von PL2-FRMFA lesen Abfrage der MemoryPosition der beiden Aussenspiegel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY | int | 0 bis 3 und 255 welcher Schluessel |
| MEM_POS_SLOT | int | 0 bis 3 welche Memoryposition |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEY_WERT | int | abgefragter Schluessel |
| STAT_MEM_POS_SLOT_WERT | int | abgefragter Memorypositionsslot |
| STAT_MEM_POS_SPIEGEL_FAHRER_HOR_WERT | int | Position Fahrerspiegel horizontal |
| STAT_MEM_POS_SPIEGEL_BEIFAHRER_HOR_WERT | int | Position Beifahrerspiegel horizontal |
| STAT_MEM_POS_SPIEGEL_FAHRER_VER_WERT | int | Position Fahrerspiegel vertikal |
| STAT_MEM_POS_SPIEGEL_BEIFAHRER_VER_WERT | int | Position Beifahrerspiegel vertikal |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-memory-position-spiegel"></a>
### STEUERN_MEMORY_POSITION_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $1E Position Spiegel fuer FRMFA Status von PL2-FRMFA schreiben Schreiben der MemoryPosition der beiden Aussenspiegel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY | int | 0 bis 3 und 255 welcher Schluessel |
| MEM_POS_SLOT | int | 0 bis 3 welche Memoryposition |
| MEM_POS_SPIEGEL_FAHRER_HOR_WERT | int | Position Fahrerspiegel horizontal |
| MEM_POS_SPIEGEL_BEIFAHRER_HOR_WERT | int | Position Beifahrerspiegel horizontal |
| MEM_POS_SPIEGEL_FAHRER_VER_WERT | int | Position Fahrerspiegel vertikal |
| MEM_POS_SPIEGEL_BEIFAHRER_VER_WERT | int | Position Beifahrerspiegel vertikal |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spiegel-taster"></a>
### STATUS_SPIEGEL_TASTER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $0F Spiegelschalter fuer FRMFA Status von PL2-FRMFA lesen Auslesen der einzelnen Tasten der Spiegelschalters

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TASTER_LINKS_EIN | int | Taster nach links betaetigt |
| STAT_TASTER_RECHTS_EIN | int | Taster nach rechts betaetigt |
| STAT_TASTER_OBEN_EIN | int | Taster nach oben betaetigt |
| STAT_TASTER_UNTEN_EIN | int | Taster nach unten betaetigt |
| STAT_SPIEGEL_AUSWAHL_FA_EIN | int | Fahrerspiegel auswaehlen |
| STAT_SPIEGEL_AUSWAHL_BF_EIN | int | Beifahrerspiegel auswaehlen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-position-spiegel"></a>
### STEUERN_POSITION_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $10 Position Spiegel fuer FRMFA Status von FRMFA schreiben ausgewaehlten Spiegel in angegebene Position fahren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_SPIEGEL | string | table Auswahl_Spiegel NAME TEXT Spiegel auswaehlen |
| RICHTUNG_SPIEGEL | string | table Richtung_Spiegel NAME TEXT Auswahl der Richtung in die der Spiegel verfahren werden soll |
| ANSTEUER_ZEIT_SPIEGEL | int | Zeit in 100ms, die der Spiegel angesteuert werden soll, d.h. 1 = 100ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-position-direkt-spiegel"></a>
### STEUERN_POSITION_DIREKT_SPIEGEL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1D Position Spiegel fuer FRMFA Status von FRMFA schreiben ausgewaehlten Spiegel in angegebene Position fahren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_SPIEGEL | string | table Auswahl_Spiegel NAME TEXT Spiegel auswaehlen |
| RICHTUNG_SPIEGEL_HORIZONTAL | int |  |
| RICHTUNG_SPIEGEL_VERTIKAL | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gurtbringer"></a>
### STATUS_GURTBRINGER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $27 Stati von Gurtbringer fuer FRMFA Status von PL2-FRMFA lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_GURTBRINGER | int | Auswahl des Gurtbringer 1 Fahrer, 2 Beifahrer, 3 oder nichts beide |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_POS_GURTBRINGER_FAHRER_WERT | int | Position Gurtbringer Fahrerseite ungueltig: 0xffff bzw. -1 |
| STAT_POS_GURTBRINGER_BEIFAHRER_WERT | int | Position Gurtbringer Beifahrer ungueltig: 0xffff bzw. -1 |
| STAT_GURTBRINGER_FAHRER_ENDLAGE_2_WERT | int | Endlage 2 Gurtbringer Fahrerseite 0 nicht erreicht, 1 erreicht, 3 ungueltig |
| STAT_GURTBRINGER_BEIFAHRER_ENDLAGE_2_WERT | int | Endlage 2 Gurtbringer Beifahrerseite 0 nicht erreicht, 1 erreicht, 3 ungueltig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-gurtbringer-initialisierung"></a>
### STEUERN_GURTBRINGER_INITIALISIERUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $27 Stati von Gurtbringer fuer FRMFA Status von PL2-FRMFA schreiben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-gurtbringer-position"></a>
### STEUERN_GURTBRINGER_POSITION

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $27 Stati von Gurtbringer fuer FRMFA Status von PL2-FRMFA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POSITION_GURTBRINGER_FAHRER | int | Position fuer Gurtbringer Fahrerseite |
| POSITION_GURTBRINGER_BEIFAHRER | int | Position fuer Gurtbringer Beifahrerseite |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-gurtbringer-richtung"></a>
### STEUERN_GURTBRINGER_RICHTUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $27 Stati von Gurtbringer fuer FRMFA Status von PL2-FRMFA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RICHTUNG_GURTBRINGER_FAHRER | int | Richtung fuer Gurtbringer Fahrerseite stop 0x00, rausfahren 0x01, reinfahren 0x02 |
| RICHTUNG_GURTBRINGER_BEIFAHRER | int | Richtung fuer Gurtbringer Beifahrerseite stop 0x00, rausfahren 0x01, reinfahren 0x02 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-warnblinken"></a>
### STATUS_WARNBLINKEN

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 Warnblinken Status von PL2-FRMFA lesen Status ob Warnblinken aktiv ist auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WARNBLINKEN_EIN | string | Warnblinken aktiv |
| STAT_WARNBLINKEN_WERT_EIN | int | Warnblinken aktiv 1 bzw. 0 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kindersicherung"></a>
### STATUS_KINDERSICHERUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $13 Kindersicherung Status von PL2-FRMFA lesen Status der Kindersicherung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TASTER_KINDERSICHERUNG_EIN | int | Taster fuer Kindersicherung betaetigt |
| STAT_KINDERSICHERUNG_AKTIV | int | Kindersicherung ein/aus |
| STAT_KINDERSICHERUNG_EIN | string | Kindersicherung ein/aus |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kindersicherung"></a>
### STEUERN_KINDERSICHERUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $13 Kindersicherung Status von FRMFA schreiben Betaetigung des Kindersicherungstasters simulieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTER_KINDERSICHERUNG | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spiegelheizung"></a>
### STATUS_SPIEGELHEIZUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $19 Spiegelheizung Status von PL2-FRMFA lesen Wert der Spiegelheizung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPIEGELHEIZUNG_TEXT_WERT | string | Wert fuer Spiegelheizung als Text |
| STAT_SPIEGELHEIZUNG_WERT | int | Wert fuer Spiegelheizung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spiegelheizung"></a>
### STEUERN_SPIEGELHEIZUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $19 Spiegelheizung Status von FRMFA schreiben Spiegelheizung mit speziellen Werten eischalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPIEGELHEIZUNG_WERT | string | Wert fuer Spiegelheizung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spiegel-abblenden"></a>
### STATUS_SPIEGEL_ABBLENDEN

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $1A SPIEGEL_ABBLENDEN Status von PL2-FRMFA lesen Auslesen des Wertes, wie der Spiegel abgeblendet ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPIEGEL_ABBLENDEN_WERT | int | Wert fuer Spiegel abblenden in Prozent von 0 bis 100 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spiegel-abblenden"></a>
### STEUERN_SPIEGEL_ABBLENDEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1A SPIEGEL_ABBLENDEN Status von FRMFA schreiben Abblenden der Aussenspiegel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPIEGEL_ABBLENDEN_WERT | int | Wert wie Aussenspiegel abgeblendet werden soll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-xenon-al-einschaltversuche"></a>
### STATUS_XENON_AL_EINSCHALTVERSUCHE

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $1B Xenon-AL-Einschaltversuche Auslesen wie oft das Abblendlicht eingeschaltet wurde

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

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $1B Xenon-AL-Einschaltversuche Loeschen der AL-Einschaltversuche

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-innenbeleuchtung-daueraus"></a>
### STATUS_INNENBELEUCHTUNG_DAUERAUS

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $26 Xenon-AL-Einschaltversuche Auslesen, ob Innenlicht daueraus geschaltet wurde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_INNENBELEUCHTUNG_DAUERAUS | int | Innenlicht daueraus geschaltet |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-innenbeleuchtung-daueraus"></a>
### STEUERN_INNENBELEUCHTUNG_DAUERAUS

KWP2000: $30 InputOutputControlByLocalIdentifier $08 LongTermAdjustment $26 Innenbeleuchtung Dauerausschalten Innenbeleuchtung Dauerausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INNENBELEUCHTUNG_DAUERAUS_EIN | string | Werte: ein, aus table DigitalArgument TEXT Innenbeleuchtung Dauerausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sense-lesen"></a>
### STATUS_SENSE_LESEN

Senseausgang fuer ausgewaehlte Lampe lesen, FRMFA KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $1C Senseausgang lesen Modus  : Default

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

<a id="job-status-fh-schalter"></a>
### STATUS_FH_SCHALTER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $24 FH-Schalter fuer FRMFA Status von PL2-FRMFA lesen Auslesen der einzelnen Tasten der FH

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FH_SCHALTER_FAT_VORNE | int | FH-Schalter FAT vorne 00 = neutral, 01 = Oeffnen manuell 02 = Oeffnen automatik, 03 = Schliessen manuell 04 = Schliessen automatik, 07 = ungueltig Bei Rechtslenker wird hier das Result fuer BFT dargestellt |
| STAT_FH_SCHALTER_FAT_HINTEN | int | FH-Schalter FAT hinten 00 = neutral, 01 = Oeffnen manuell 02 = Oeffnen automatik, 03 = Schliessen manuell 04 = Schliessen automatik, 07 = ungueltig Bei Rechtslenker wird hier das Result fuer BFT dargestellt |
| STAT_FH_SCHALTER_BFT_VORNE | int | FH-Schalter BFT vorne 00 = neutral, 01 = Oeffnen manuell 02 = Oeffnen automatik, 03 = Schliessen manuell 04 = Schliessen automatik, 07 = ungueltig Bei Rechtslenker wird hier das Result fuer FAT dargestellt |
| STAT_FH_SCHALTER_BFT_HINTEN | int | FH-Schalter BFT hinten 00 = neutral, 01 = Oeffnen manuell 02 = Oeffnen automatik, 03 = Schliessen manuell 04 = Schliessen automatik, 07 = ungueltig Bei Rechtslenker wird hier das Result fuer FAT dargestellt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ee-fh-log-data"></a>
### STATUS_EE_FH_LOG_DATA

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $21 EE_FH_LOG_DATA Lesen von EE_FH_LOG_DATA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EE_FH_LOG_DATA | binary | Lesen von EE_FH_LOG_DATA |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ee-fh-log-data"></a>
### STEUERN_EE_FH_LOG_DATA

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 EE_FH_LOG_DATA Status von FRMFA schreiben Loeschen von EE_FH_LOG_DATA des FRMFA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-block-lesen-lear"></a>
### _CODIERDATEN_BLOCK_LESEN_LEAR

KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | string | Bereich: 0x30xx bis 0x35xx |

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

<a id="job-codierdaten-3400-lesen-komplett-lear"></a>
### _CODIERDATEN_3400_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten im 3400-Bereich Auslesen der FRMFA-Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_FRMFA | string | die kompletten Codierdaten im 3400-Bereich (FRMFA) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3100-lesen-komplett-lesen-lear"></a>
### _CODIERDATEN_3100_LESEN_KOMPLETT_LESEN_LEAR

Auslesen der kompletten Codierdaten im 3100-Bereich KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| COD_COD_LEN | int | Laenge der Code-Codierdaten |
| COD_CHECK_SUM | string | Checksumme der Code-Codierdaten |
| LAND | string | Land |
| EXT | string | Extension |
| COD_INDEX | int | Codierindex |
| COD_VARIANTE | int | Codiervariante |
| CODE_DATEN_1 | string | Teil 1 der kompletten Codierdaten im 3100-Bereich |
| CODE_DATEN_2 | string | Teil 2 der kompletten Codierdaten im 3100-Bereich |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3500-lesen-komplett-lear"></a>
### _CODIERDATEN_3500_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten im 3500-Bereich (FH) KWP 2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_FH | string | die kompletten Codierdaten im 3500-Bereich |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3400-schreiben-aus-datei-lear"></a>
### _CODIERDATEN_3400_SCHREIBEN_AUS_DATEI_LEAR

Beschreiben der Default-Codierdaten Beschreiben der FRMFA-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $34xx Codierdaten, Default Modus  : Default

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

<a id="job-codierdaten-3000-schreiben-aus-datei-lear"></a>
### _CODIERDATEN_3000_SCHREIBEN_AUS_DATEI_LEAR

Beschreiben der Default-Codierdaten Beschreiben der ALC-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten, Default Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit Default-Codierdaten fuer 3000-Bereich Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |
| WARTEZEIT_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-3100-schreiben-aus-datei-lear"></a>
### _CODIERDATEN_3100_SCHREIBEN_AUS_DATEI_LEAR

Beschreiben der Default-Codierdaten fuer 3100-Bereich KWP2000: $2E WriteDataByCommonIdentifier $31xx Code in EEPROM Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_DATEI | string | Dateiname mit generiertem Code Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.cod codiert letztes Zeichen muss ein LF sein |
| WARTEZEIT_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-komplett-schreiben-lear"></a>
### _CODIERDATEN_KOMPLETT_SCHREIBEN_LEAR

Beschreiben der Default-Codierdaten KWP2000: $2E WriteDataByCommonIdentifier $30xx Codierdaten ALC schreiben $31xx Code in EEPROM schreiben $34xx Codierdaten FRMFA schreiben $35xx Codierdaten FH schreiben Modus  : Default

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

<a id="job-read-ident-94-ssecuson-lear"></a>
### _READ_IDENT_94_SSECUSON_LEAR

SystemSupplierECUSoftwareNumber KWP2000: $1A ReadECUIdentification Modus  : $94 SystemSupplierECUSoftwareNumber

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_SW_APP | string | SystemSupplierECUSoftwareNumber fuer Applikation |
| ID_SW_BOOT | string | SystemSupplierECUSoftwareNumber fuer Bootloader |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-ci-ahl-fh-lear"></a>
### _WRITE_CI_AHL_FH_LEAR

Beschreiben der CI fuer AHL und FH KWP2000: $2E WriteDataByLocalIdentifier $05 CI Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CI_AHL | unsigned char | Bereich: 0-99 |
| CI_FH | unsigned char | Bereich: 0-99 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-ident-param"></a>
### READ_IDENT_PARAM

Identdaten KWP2000: $1A ReadECUIdentification Modus  : mit Angabe der ID_OPTION zum spezifischen ID_LESEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ID_OPT | int | Bereich: 0x86-0x9F |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR_1 | string | BMW-Teilenummer 1.Eintrag |
| ID_BMW_NR_2 | string | BMW-Teilenummer 2.Eintrag |
| ID_BMW_NR_3 | string | BMW-Teilenummer 3.Eintrag |
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
| ID_CHANGE_INDEX | string | Change-Index |
| ID_SSECUSEN | string | SystenSupplierECUSerialNumber |
| ID_VIN | string | VehicleIdentificationNumber |
| ID_SSECUHN | string | SystemSupplierECUHardwareNumber |
| ID_SSECUHVN | string | SystemSupplierECUHardwareVersionNumber |
| ID_SSECUSON | string | SystemSupplierECUSoftwareNumber |
| ID_SSECUSVN | string | SystemSupplierECUSoftwareVersionNumber |
| ID_PD | string | ProgrammingDate |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-ident-93-ssecuhvn"></a>
### WRITE_IDENT_93_SSECUHVN

Schreiben der SystemSupplierECUHardwareVersionNumber KWP2000: $3B WriteDataByLocalIdentifier $93 SystemSupplierECUHardwareVersionNumber Modus  : Default

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

<a id="job-status-lwr-lesen"></a>
### STATUS_LWR_LESEN

Lesen eines Codierdatensatzes zur Unterscheidung zwischen dynamischer, automatischer und manueller LWR KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEINE_LWR | unsigned char | 0 oder 1, ob LWR aktiv bei Kurvenlicht immer 1 |
| STAT_DYN_LWR | unsigned char | 0 oder 1, ob dynamisch LWR aktiv |
| STAT_AUT_LWR | unsigned char | 0 oder 1, ob automatische LWR aktiv |
| STAT_MAN_LWR | unsigned char | 0 oder 1, ob manuelle LWR aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-energy-saving-mode"></a>
### READ_ENERGY_SAVING_MODE

Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ENERGY_SAVING_MODE | string | Ausgabe des Engery-Saving-Modes table EnergySaving NAME TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hersteller-daten-lesen-lear"></a>
### _HERSTELLER_DATEN_LESEN_LEAR

Auslesen der Herstellerdaten KWP2000: $22 ReadDataByCommonIdentifier $0004 Herstellerdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HERSTELLERDATEN | binary | Herstellerdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbd-zeichn-index-lesen-lear"></a>
### CBD_ZEICHN_INDEX_LESEN_LEAR

Auslesen des Aenderungsindex aus den Codierdaten KWP 2000: $22 ReadDataByCommonIdentifier $3404 Aenderungs-Index Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CBD_ZEICHN_INDEX | string | Aenderungsindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hersteller-daten-schreiben-lear"></a>
### _HERSTELLER_DATEN_SCHREIBEN_LEAR

Beschreiben der Codierdaten je nach Block KWP2000: $2E WriteDataByCommonIdentifier $0004 Herstellerdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HERSTELLERDATEN | string | Block+Codierdaten |

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

<a id="job-flash-prog-status-schreiben-lear"></a>
### _FLASH_PROG_STATUS_SCHREIBEN_LEAR

Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $02 FlashProgrammierstatus auf 1 setzen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnose-brose-fh-1"></a>
### _STEUERN_DIAGNOSE_BROSE_FH_1

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $09 Diagnose job 1 fuer BROSE-FH Status von FRMFA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE_1 | unsigned char |  |
| BYTE_2 | unsigned char |  |
| BYTE_3 | unsigned char |  |
| BYTE_4 | unsigned char |  |
| BYTE_5 | unsigned char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnose-brose-fh-2"></a>
### _STEUERN_DIAGNOSE_BROSE_FH_2

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0A Diagnose job 2 fuer BROSE-FH Status von FRMFA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE_1 | unsigned char |  |
| BYTE_2 | unsigned char |  |
| BYTE_3 | unsigned char |  |
| BYTE_4 | unsigned char |  |
| BYTE_5 | unsigned char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnose-brose-fh-3"></a>
### _STEUERN_DIAGNOSE_BROSE_FH_3

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0B Diagnose job 3 fuer BROSE-FH Status von FRMFA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE_1 | unsigned char |  |
| BYTE_2 | unsigned char |  |
| BYTE_3 | unsigned char |  |
| BYTE_4 | unsigned char |  |
| BYTE_5 | unsigned char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnose-brose-fh-4"></a>
### _STEUERN_DIAGNOSE_BROSE_FH_4

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0C Diagnose job 4 fuer BROSE-FH Status von FRMFA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE_1 | unsigned char |  |
| BYTE_2 | unsigned char |  |
| BYTE_3 | unsigned char |  |
| BYTE_4 | unsigned char |  |
| BYTE_5 | unsigned char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnose-brose-fh-5"></a>
### _STEUERN_DIAGNOSE_BROSE_FH_5

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $0D Diagnose job 5 fuer BROSE-FH Status von FRMFA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE_1 | unsigned char |  |
| BYTE_2 | unsigned char |  |
| BYTE_3 | unsigned char |  |
| BYTE_4 | unsigned char |  |
| BYTE_5 | unsigned char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-can-bus-error-lear"></a>
### _READ_CAN_BUS_ERROR_LEAR

KWP 2000: $21 ReadDataByLocalIdentifier $03 CAN_BUS_ERROR Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CAN_BUS_ERROR | string | gibt an welcher CAN-Fehler vorliegt |
| CAN_BUS_ERROR_OLD | string | gibt an welcher CAN-Fehler vorgelegen hat |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-clr-can-bus-error-lear"></a>
### _CLR_CAN_BUS_ERROR_LEAR

KWP2000: $3B WriteDataByLocalIdentifier $03 CAN_BUS_ERROR Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-register-u435-lear"></a>
### _READ_REGISTER_U435_LEAR

KWP 2000: $21 ReadDataByLocalIdentifier $03 READ_REGISTER_U435 Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REGISTER_U435_ADR | unsigned int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| REGISTER_U435 | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-register-u435-lear"></a>
### _WRITE_REGISTER_U435_LEAR

KWP2000: $3B WriteDataByLocalIdentifier $03 WRITE_REGISTER_U435 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REGISTER_U435 | unsigned int |  |
| WERT_REGISTER_U435 | unsigned char |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-reset-kurzschluss-sperre"></a>
### _RESET_KURZSCHLUSS_SPERRE

Kurzschlusssperre ueber Diagnose ausschalten KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $18 Kurzschlusssperre ausschalten Status von FRMFA schreiben

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

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $14 Lampenkurzschluss auslesen Status Lampenkurzschluesse (explizit) von FRMFA lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT | int | Fernlicht links, E92/E93: Abbiegelicht links SHORT_CIRCUIT ja/nein |
| STAT_FL_RECHTS_SHORT_CIRCUIT | int | Fernlicht rechts, E92/E93: Abbiegelicht rechts SHORT_CIRCUIT ja/nein |
| STAT_AL_LINKS_SHORT_CIRCUIT | int | Abblendlicht links SHORT_CIRCUIT ja/nein |
| STAT_AL_RECHTS_SHORT_CIRCUIT | int | Abblendlicht rechts SHORT_CIRCUIT ja/nein |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT | int | Begrenzungslicht links SHORT_CIRCUIT ja/nein |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT | int | Begrenzungslicht rechts SHORT_CIRCUIT ja/nein |
| STAT_NSW_LINKS_SHORT_CIRCUIT | int | Nebelscheinwerfer links SHORT_CIRCUIT ja/nein |
| STAT_NSW_RECHTS_SHORT_CIRCUIT | int | Nebelscheinwerfer rechts SHORT_CIRCUIT ja/nein |
| STAT_FRA_LINKS_VORN_1_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT ja/nein |
| STAT_FRA_RECHTS_VORN_1_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT ja/nein |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT ja/nein |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT ja/nein |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT | int | Bremslicht links SHORT_CIRCUIT ja/nein |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT | int | Bremslicht rechts SHORT_CIRCUIT ja/nein |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT | int | Bremslicht mitte SHORT_CIRCUIT ja/nein |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT | int | Schlusslicht 1 links, E92/E93: Tagfahrlicht links SHORT_CIRCUIT ja/nein |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT | int | Schlusslicht 1 rechts, E92/E93: Tagfahrlicht rechts SHORT_CIRCUIT ja/nein |
| STAT_SL_BL_LINKS_2_SHORT_CIRCUIT | int | Schlusslicht 2 links SHORT_CIRCUIT ja/nein |
| STAT_SL_BL_RECHTS_2_SHORT_CIRCUIT | int | Schlusslicht 2 rechts SHORT_CIRCUIT ja/nein |
| STAT_KZL_SHORT_CIRCUIT | int | Kennzeichenlicht SHORT_CIRCUIT ja/nein |
| STAT_IB_SHORT_CIRCUIT | int | Innenbeleuchtung SHORT_CIRCUIT ja/nein |
| STAT_NSL_LINKS_SHORT_CIRCUIT | int | Nebelschlusslicht links SHORT_CIRCUIT ja/nein |
| STAT_NSL_RECHTS_SHORT_CIRCUIT | int | Nebelschlusslicht rechts SHORT_CIRCUIT ja/nein |
| STAT_RFL_LINKS_SHORT_CIRCUIT | int | Rueckfahrlicht links SHORT_CIRCUIT ja/nein |
| STAT_RFL_RECHTS_SHORT_CIRCUIT | int | Rueckfahrlicht rechts SHORT_CIRCUIT ja/nein |
| STAT_BFD_LINKS_SHORT_CIRCUIT | int | Brake-Force-Display links SHORT_CIRCUIT ja/nein |
| STAT_BFD_RECHTS_SHORT_CIRCUIT | int | Brake-Force-Display rechts SHORT_CIRCUIT ja/nein |
| STAT_KLEMME_58G_SHORT_CIRCUIT | int | Klemme 58g SHORT_CIRCUIT ja/nein |
| STAT_FLC_LED_SHORT_CIRCUIT | int | FLC LED SHORT_CIRCUIT ja/nein |
| STAT_VFB_SHORT_CIRCUIT | int | Vorfeldbeleuchtung SHORT_CIRCUIT ja/nein |
| STAT_BEL_WBL_SHORT_CIRCUIT | int | Beleuchtung Warnblinktaster SHORT_CIRCUIT ja/nein |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-kurzschluss-wiederhol-counter"></a>
### STATUS_LAMPEN_KURZSCHLUSS_WIEDERHOL_COUNTER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $15 Lampenkurzschluss Wiederholzaehler auslesen Status Lampenkurzschlusswiederholzaehler (explizit) von FRMFA lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Fernlicht links, E92/E93: Abbiegelicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_FL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Fernlicht rechts, E92/E93: Abbiegelicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_AL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Abblendlicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_AL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Abblendlicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Begrenzungslicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Begrenzungslicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSW_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelscheinwerfer links SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSW_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelscheinwerfer rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_LINKS_VORN_1_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_RECHTS_VORN_1_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT_WIEDERHOL |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT_WIEDERHOL | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT_WIEDERHOL |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Bremslicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Bremslicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT_WIEDERHOL | int | Bremslicht mitte SHORT_CIRCUIT_WIEDERHOL |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT_WIEDERHOL | int | Schlusslicht 1 links, E92/E93: Tagfahrlicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT_WIEDERHOL | int | Schlusslicht 1 rechts, E92/E93: Tagfahrlicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_SL_BL_LINKS_2_SHORT_CIRCUIT_WIEDERHOL | int | Schlusslicht links 2 SHORT_CIRCUIT_WIEDERHOL |
| STAT_SL_BL_RECHTS_2_SHORT_CIRCUIT_WIEDERHOL | int | Schlusslicht rechts 2 SHORT_CIRCUIT_WIEDERHOL |
| STAT_KZL_SHORT_CIRCUIT_WIEDERHOL | int | Kennzeichenlicht SHORT_CIRCUIT_WIEDERHOL |
| STAT_IB_SHORT_CIRCUIT_WIEDERHOL | int | Innenbeleuchtung SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelschlusslicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_NSL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Nebelschlusslicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_RFL_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Rueckfahrlicht links SHORT_CIRCUIT_WIEDERHOL |
| STAT_RFL_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Rueckfahrlicht rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_BFD_LINKS_SHORT_CIRCUIT_WIEDERHOL | int | Brake-Force-Display links SHORT_CIRCUIT_WIEDERHOL |
| STAT_BFD_RECHTS_SHORT_CIRCUIT_WIEDERHOL | int | Brake-Force-Display rechts SHORT_CIRCUIT_WIEDERHOL |
| STAT_KLEMME_58G_SHORT_CIRCUIT_WIEDERHOL | int | Klemme 58g SHORT_CIRCUIT_WIEDERHOL |
| STAT_FLC_LED_SHORT_CIRCUIT_WIEDERHOL | int | FLC LED SHORT_CIRCUIT_WIEDERHOL |
| STAT_VFB_SHORT_CIRCUIT_WIEDERHOL | int | Vorfeldbeleuchtung SHORT_CIRCUIT_WIEDERHOL |
| STAT_BEL_WBL_SHORT_CIRCUIT_WIEDERHOL | int | Beleuchtung Warnblinktaster SHORT_CIRCUIT_WIEDERHOL |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-kurzschluss-counter"></a>
### STATUS_LAMPEN_KURZSCHLUSS_COUNTER

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $16 Lampenkurzschluss Zaehler auslesen Status Lampenkurzschlusszaehler (explizit) von FRMFA lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT_COUNTER | int | Fernlicht links, E92/E93: Abbiegelicht links SHORT_CIRCUIT_COUNTER |
| STAT_FL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Fernlicht rechts, E92/E93: Abbiegelicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_AL_LINKS_SHORT_CIRCUIT_COUNTER | int | Abblendlicht links SHORT_CIRCUIT_COUNTER |
| STAT_AL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Abblendlicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT_COUNTER | int | Begrenzungslicht links SHORT_CIRCUIT_COUNTER |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Begrenzungslicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_NSW_LINKS_SHORT_CIRCUIT_COUNTER | int | Nebelscheinwerfer links SHORT_CIRCUIT_COUNTER |
| STAT_NSW_RECHTS_SHORT_CIRCUIT_COUNTER | int | Nebelscheinwerfer rechts SHORT_CIRCUIT_COUNTER |
| STAT_FRA_LINKS_VORN_1_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT_COUNTER |
| STAT_FRA_RECHTS_VORN_1_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT_COUNTER |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT_COUNTER |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT_COUNTER | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT_COUNTER |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT_COUNTER | int | Bremslicht links SHORT_CIRCUIT_COUNTER |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT_COUNTER | int | Bremslicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT_COUNTER | int | Bremslicht mitte SHORT_CIRCUIT_COUNTER |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT_COUNTER | int | Schlusslicht links 1, E92/E93: Tagfahrlicht links SHORT_CIRCUIT_COUNTER |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT_COUNTER | int | Schlusslicht rechts 1, E92/E93: Tagfahrlicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_SL_BL_LINKS_2_SHORT_CIRCUIT_COUNTER | int | Schlusslicht links 2 SHORT_CIRCUIT_COUNTER |
| STAT_SL_BL_RECHTS_2_SHORT_CIRCUIT_COUNTER | int | Schlusslicht rechts 2 SHORT_CIRCUIT_COUNTER |
| STAT_KZL_SHORT_CIRCUIT_COUNTER | int | Kennzeichenlicht SHORT_CIRCUIT_COUNTER |
| STAT_IB_SHORT_CIRCUIT_COUNTER | int | Innenbeleuchtung SHORT_CIRCUIT_COUNTER |
| STAT_NSL_LINKS_SHORT_CIRCUIT_COUNTER | int | Nebelschlusslicht links SHORT_CIRCUIT_COUNTER |
| STAT_NSL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Nebelschlusslicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_RFL_LINKS_SHORT_CIRCUIT_COUNTER | int | Rueckfahrlicht links SHORT_CIRCUIT_COUNTER |
| STAT_RFL_RECHTS_SHORT_CIRCUIT_COUNTER | int | Rueckfahrlicht rechts SHORT_CIRCUIT_COUNTER |
| STAT_BFD_LINKS_SHORT_CIRCUIT_COUNTER | int | Brake-Force-Display links SHORT_CIRCUIT_COUNTER |
| STAT_BFD_RECHTS_SHORT_CIRCUIT_COUNTER | int | Brake-Force-Display rechts SHORT_CIRCUIT_COUNTER |
| STAT_KLEMME_58G_SHORT_CIRCUIT_COUNTER | int | Klemme 58g SHORT_CIRCUIT_COUNTER |
| STAT_FLC_LED_SHORT_CIRCUIT_COUNTER | int | FLC LED SHORT_CIRCUIT_COUNTER |
| STAT_VFB_SHORT_CIRCUIT_COUNTER | int | Vorfeldbeleuchtung SHORT_CIRCUIT_COUNTER |
| STAT_BEL_WBL_SHORT_CIRCUIT_COUNTER | int | Beleuchtung Warnblinktaster SHORT_CIRCUIT_COUNTER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lampen-kurzschluss-counter-max"></a>
### STATUS_LAMPEN_KURZSCHLUSS_COUNTER_MAX

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $17 Lampenkurzschluss Zaehler Maxwert auslesen Status des max. Wertes des Lampenkurzschlusszaehlers (explizit) von FRMFA lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Fernlicht links, E92/E93: Abbiegelicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Fernlicht rechts, E92/E93: Abbiegelicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_AL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Abblendlicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_AL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Abblendlicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BEGRL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Begrenzungslicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BEGRL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Begrenzungslicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSW_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelscheinwerfer links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSW_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelscheinwerfer rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_LINKS_VORN_1_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger links vorne SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_RECHTS_VORN_1_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger rechts vorne SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_LINKS_HINTEN_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger links hinten SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FRA_RECHTS_HINTEN_SHORT_CIRCUIT_COUNTER_MAX | int | Fahrtrichtungsanzeiger rechts hinten SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BREMSLICHT_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Bremslicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BREMSLICHT_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Bremslicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BREMSLICHT_MITTE_SHORT_CIRCUIT_COUNTER_MAX | int | Bremslicht mitte SHORT_CIRCUIT_COUNTER_MAX |
| STAT_SL_BL_LINKS_1_SHORT_CIRCUIT_COUNTER_MAX | int | Schlusslicht links 1, E92/E93: Tagfahrlicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_SL_BL_RECHTS_1_SHORT_CIRCUIT_COUNTER_MAX | int | Schlusslicht rechts 1, E92/E93: Tagfahrlicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_SL_BL_LINKS_2_SHORT_CIRCUIT_COUNTER_MAX | int | Schlusslicht links 2 SHORT_CIRCUIT_COUNTER_MAX |
| STAT_SL_BL_RECHTS_2_SHORT_CIRCUIT_COUNTER_MAX | int | Schlusslicht rechts 2 SHORT_CIRCUIT_COUNTER_MAX |
| STAT_KZL_SHORT_CIRCUIT_COUNTER_MAX | int | Kennzeichenlicht SHORT_CIRCUIT_COUNTER_MAX |
| STAT_IB_SHORT_CIRCUIT_COUNTER_MAX | int | Innenbeleuchtung SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelschlusslicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_NSL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Nebelschlusslicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_RFL_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Rueckfahrlicht links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_RFL_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Rueckfahrlicht rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BFD_LINKS_SHORT_CIRCUIT_COUNTER_MAX | int | Brake-Force-Display links SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BFD_RECHTS_SHORT_CIRCUIT_COUNTER_MAX | int | Brake-Force-Display rechts SHORT_CIRCUIT_COUNTER_MAX |
| STAT_KLEMME_58G_SHORT_CIRCUIT_COUNTER_MAX | int | Klemme 58g SHORT_CIRCUIT_COUNTER_MAX |
| STAT_FLC_LED_SHORT_CIRCUIT_COUNTER_MAX | int | FLC LED SHORT_CIRCUIT_COUNTER_MAX |
| STAT_VFB_SHORT_CIRCUIT_COUNTER_MAX | int | Vorfeldbeleuchtung SHORT_CIRCUIT_COUNTER_MAX |
| STAT_BEL_WBL_SHORT_CIRCUIT_COUNTER_MAX | int | Beleuchtung Warnblinktaster SHORT_CIRCUIT_COUNTER_MAX |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-smc-bestromen"></a>
### STEUERN_SMC_BESTROMEN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $11 SMC bestromen Status von FRMFA schreiben Bestromung der SMCs einschalten

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

<a id="job-status-lampenausgang-entprellt-lesen"></a>
### STATUS_LAMPENAUSGANG_ENTPRELLT_LESEN

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 alle Dimmwerte an PWM-Ports Status von FRMFA lesen entprellte Dimmwerte aller Lampen auslesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | table LampNrTexte NAME TEXT Auswahl, welche Lampe geprueft werden soll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAMPE | string | ausgewaehlte Lampe |
| STAT_AUSGANG_EIN | int | Ein/Aus der ausgewaehlten Lampe |
| STAT_AUSGANG_DIMMWERT | int | Dimmwert der ausgewaehlten Lampe |
| STAT_AUSGANG_DIMMWERT_EINH | string | Einheit fuer Dimmwert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fg-nr-smc-default"></a>
### FG_NR_SMC_DEFAULT

Beschreiben der VIN mit 0xff KWP2000: $A6 LINGateway $3B WriteDataByLocalIdentifier $90 VIN Beschreiben der Fahrgestellnummer in beide SMC mit 0xff

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-gurtbringer-fa-ident"></a>
### READ_GURTBRINGER_FA_IDENT

ident lesen des LIN-Slave GURTBRINGER_FA Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-GURTBRINGER Modus  : Default Auslesen der Identdaten der GURTBRINGER_FA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_VERSION_GURTBRINGER | string | SW-Version fuer GURTBRINGER |
| ID_BMW_NR_GURTBRINGER | string | BMW_Teilenummer fuer das GURTBRINGER |
| CODING_INDEX_GURTBRINGER | string | Codierindex fuer GURTBRINGER |
| MCV_VERSION_GURTBRINGER | string | Nummer Nachrichtenkatalog fuer das GURTBRINGER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-gurtbringer-bf-ident"></a>
### READ_GURTBRINGER_BF_IDENT

ident lesen des LIN-Slave GURTBRINGER_BF Standard Codierjob KWP2000: $A6 LINGateway $1A ReadECUIdentification $8A ID-GURTBRINGER Modus  : Default Auslesen der Identdaten der GURTBRINGER_BF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_VERSION_GURTBRINGER | string | SW-Version fuer GURTBRINGER |
| ID_BMW_NR_GURTBRINGER | string | BMW_Teilenummer fuer das GURTBRINGER |
| CODING_INDEX_GURTBRINGER | string | Codierindex fuer GURTBRINGER |
| MCV_VERSION_GURTBRINGER | string | Nummer Nachrichtenkatalog fuer das GURTBRINGER |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-schreiben-gurtbringer-fa"></a>
### C_FG_SCHREIBEN_GURTBRINGER_FA

Schreiben der FG-Nr. in den GURTBRINGER_FA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR_GURTBRINGER | string | Fahrgestellnummer GURTBRINGER (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen-gurtbringer-fa"></a>
### C_FG_LESEN_GURTBRINGER_FA

Lesen der FG-Nr. aus dem GURTBRINGER_FA KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR_GURTBRINGER | string | Fahrgestellnummer 7-stellig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-auftrag-gurtbringer-fa"></a>
### C_FG_AUFTRAG_GURTBRINGER_FA

Schreiben und Lesen der FG-Nr. GURTBRINGER_FA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR_GURTBRINGER | string | Fahrgestellnummer GURTBRINGER (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-schreiben-gurtbringer-bf"></a>
### C_FG_SCHREIBEN_GURTBRINGER_BF

Schreiben der FG-Nr. in den GURTBRINGER_BF KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR_GURTBRINGER | string | Fahrgestellnummer GURTBRINGER (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen-gurtbringer-bf"></a>
### C_FG_LESEN_GURTBRINGER_BF

Lesen der FG-Nr. aus dem GURTBRINGER_BF KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR_GURTBRINGER | string | Fahrgestellnummer 7-stellig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-auftrag-gurtbringer-bf"></a>
### C_FG_AUFTRAG_GURTBRINGER_BF

Schreiben und Lesen der FG-Nr. GURTBRINGER_BF KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR_GURTBRINGER | string | Fahrgestellnummer GURTBRINGER (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-schreiben-gurtbringer-fa"></a>
### C_AEI_SCHREIBEN_GURTBRINGER_FA

Schreiben des Aenderungsindex in den GURTBRINGER_FA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AEI_GURTBRINGER | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-lesen-gurtbringer-fa"></a>
### C_AEI_LESEN_GURTBRINGER_FA

Lesen des Aenderungsindex aus dem GURTBRINGER_FA KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AEI_GURTBRINGER | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-auftrag-gurtbringer-fa"></a>
### C_AEI_AUFTRAG_GURTBRINGER_FA

Schreiben und Lesen des Aenderungsindex GURTBRINGER_FA KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AEI_GURTBRINGER | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-schreiben-gurtbringer-bf"></a>
### C_AEI_SCHREIBEN_GURTBRINGER_BF

Schreiben des Aenderungsindex in den GURTBRINGER_BF KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AEI_GURTBRINGER | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-lesen-gurtbringer-bf"></a>
### C_AEI_LESEN_GURTBRINGER_BF

Lesen des Aenderungsindex aus dem GURTBRINGER_BF KWP2000: $A6 LINGateway $22 ReadDataByCommonIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AEI_GURTBRINGER | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-auftrag-gurtbringer-bf"></a>
### C_AEI_AUFTRAG_GURTBRINGER_BF

Schreiben und Lesen des Aenderungsindex GURTBRINGER_BF KWP2000: $A6 LINGateway $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AEI_GURTBRINGER | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-reset-gurtbringer-fa"></a>
### RESET_GURTBRINGER_FA

Reset GURTBRINGER_FA KWP2000: $A6 LINGateway $11 Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-reset-gurtbringer-bf"></a>
### RESET_GURTBRINGER_BF

Reset GURTBRINGER_BF KWP2000: $A6 LINGateway $11 Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kurzhub-deaktivieren"></a>
### STEUERN_KURZHUB_DEAKTIVIEREN

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $28 Kurzhub Deaktivieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTIV | int | EIN: Kurzhub deaktivieren AUS: Kurzhub reaktivieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-qualitaet-fensterheberlauf"></a>
### STATUS_QUALITAET_FENSTERHEBERLAUF

Qualitaetsbewertung Fensterheber

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GRENZWERT_1 | int | Optional abweichender Grenzwert 1 |
| GRENZWERT_2 | int | Optional abweichender Grenzwert 2 |
| GRENZWERT_3 | int | Optional abweichender Grenzwert 3 |
| GRENZWERT_4 | int | Optional abweichender Grenzwert 4 |
| GRENZWERT_5 | int | Optional abweichender Grenzwert 5 |
| GRENZWERT_6 | int | Optional abweichender Grenzwert 6 |
| GRENZWERT_7 | int | Optional abweichender Grenzwert 7 |
| GRENZWERT_8 | int | Optional abweichender Grenzwert 8 |
| GRENZWERT_9 | int | Optional abweichender Grenzwert 9 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| STAT_AUSWERTUNG_FAHRER | string | Interpretation Adaptionsdaten Fahrerseite Bei Kategorie 9, 8 und 7 wird die Oeffnungsweite des Fensters an der B-Saeule ausgegeben mit zugehoerigen Adaptionswert |
| STAT_KATEGORIE_FAHRER_WERT | int | Kategorie Fahrerseite als Integer |
| STAT_AUSWERTUNG_BEIFAHRER | string | Interpretation Adaptionsdaten Beifahrerseite Bei Kategorie 9, 8 und 7 wird die Oeffnungsweite des Fensters an der B-Saeule ausgegeben mit zugehoerigen Adaptionswert |
| STAT_KATEGORIE_BEIFAHRER_WERT | int | Kategorie Beifahrerseite als Integer |
| STAT_ADAPTIONSDATEN_FAHRER | binary | ausgelesene Daten Fahrerseite |
| STAT_ADAPTIONSDATEN_BEIFAHRER | binary | ausgelesene Daten Beifahrerseite |
| STAT_INFO_GRENZWERTE | string | verwendete Grenzwerte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fh-adaptionsspeicher-lesen"></a>
### _STATUS_FH_ADAPTIONSSPEICHER_LESEN

Adaptionsdaten Fensterheber KWP2000: $30 InputOutputControlByLocalIdentifier $18 ECHTZEITDATEN_BROSE_LESEN $01 ReportCurrentState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME | string | Date&Time |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ADAPTIONSDATEN_FAHRER | binary | ausgelesene Daten Fahrerseite |
| STAT_ADAPTIONSDATEN_BEIFAHRER | binary | ausgelesene Daten Beifahrerseite |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FORTTEXTE](#table-forttexte) (57 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (6 × 5)
- [TIEFENTL](#table-tiefentl) (1 × 8)
- [FUMWELTTEXTE](#table-fumwelttexte) (9 × 9)
- [ERR_LAMPE](#table-err-lampe) (36 × 2)
- [IORTTEXTE](#table-iorttexte) (103 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (91 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (12 × 9)
- [NOTL](#table-notl) (1 × 7)
- [LAMPNRTEXTE](#table-lampnrtexte) (33 × 3)
- [FUNKTIONNRTEXTE](#table-funktionnrtexte) (13 × 3)
- [ZUSATZOUT](#table-zusatzout) (3 × 3)
- [ENERGYSAVING](#table-energysaving) (5 × 3)
- [SMCS](#table-smcs) (3 × 3)
- [REF_SMCS](#table-ref-smcs) (4 × 3)
- [FH_RICHTUNG](#table-fh-richtung) (4 × 3)
- [AUSWAHL_FENSTER](#table-auswahl-fenster) (7 × 3)
- [AUSWAHL_SPIEGEL](#table-auswahl-spiegel) (3 × 3)
- [RICHTUNG_SPIEGEL](#table-richtung-spiegel) (7 × 3)
- [SPIEGEL_HEIZUNG](#table-spiegel-heizung) (9 × 3)

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

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 57 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9CA8 | interner Fehler |
| 0x9CA9 | Klemme 30A Anschluss fehlerhaft |
| 0x9CAA | Klemme 30B Anschluss fehlerhaft |
| 0x9CAB | eine Klemme 15 fehlt |
| 0x9CAC | Bremslichtschalter defekt |
| 0x9CAD | AHM-Kommunikation gestoert |
| 0x9CAE | Bedienteilfehler |
| 0x9CAF | Lichtschalterstellung 1 defekt |
| 0x9CB0 | Lichtschalterstellung 2 defekt |
| 0x9CB1 | Dimmer-Poti defekt |
| 0x9CB2 | LWR-Poti defekt |
| 0x9CB3 | Sensor Hoehenstand vorne defekt |
| 0x9CB4 | Sensor Hoehenstand hinten defekt |
| 0x9CB5 | Energiesparmode aktiv |
| 0x9CB6 | LWR-Spulenabriss |
| 0x9CB7 | LWR-Treiberfehler |
| 0x9CB8 | SPI (EEPROM, LWR) gestoert |
| 0x9CB9 | Kurzschlussfehler 4 |
| 0x9CBA | Kurzschlussfehler 3 |
| 0x9CBB | Kurzschlussfehler 2 |
| 0x9CBC | Kurzschlussfehler 1 |
| 0x9CBD | Kommunikation mit StepperMotorBox links gestoert |
| 0x9CBE | Kommunikation mit StepperMotorBox rechts gestoert |
| 0x9CBF | SMC links defekt |
| 0x9CC0 | SMC rechts defekt |
| 0x9CC1 | Kommunikation mit Spiegel Fahrerseite gestoert |
| 0x9CC2 | Kommunikation mit Spiegel Beifahrerseite gestoert |
| 0x9CC3 | Spiegelheizung Fahrerseite defekt |
| 0x9CC4 | Spiegelheizung Beifahrerseite defekt |
| 0x9CC5 | Hallsensor FH-Fahrertuer defekt |
| 0x9CC6 | Hallsensor FH-Beifahrertuer defekt |
| 0x9CC7 | Zeitfenster FH-Fahrertuer gestoert |
| 0x9CC8 | Zeitfenster FH-Beifahrertuer gestoert |
| 0x9CC9 | FH-EEPROM gestoert |
| 0x9CCA | Relais FH-Fahrertuer defekt |
| 0x9CCB | Relais FH-Beifahrertuer defekt |
| 0x9CCC | Tiefentladungsschutz der Batterie: Abschaltung Standlicht |
| 0x9CCD | Tiefentladungsschutz der Batterie: Abschaltung Parklicht |
| 0x9CCE | Batterie tiefentladen |
| 0x9CCF | Kommunikation mit LIN-Bedienteil gestoert |
| 0x9CD0 | Antrieb Spiegel Fahrerseite defekt |
| 0x9CD1 | Antrieb Spiegel Beifahrerseite defekt |
| 0x9CD2 | Antrieb Beiklappen Spiegel Fahrerseite defekt |
| 0x9CD3 | Antrieb Beiklappen Spiegel Beifahrerseite defekt |
| 0x9CD4 | Kommunikation mit Gurtbringer Fahrerseite gestoert |
| 0x9CD5 | Kommunikation mit Gurtbringer Beifahrerseite gestoert |
| 0x9CD6 | Motor Gurtbringer Fahrerseite defekt |
| 0x9CD7 | Motor Gurtbringer Beifahrerseite defekt |
| 0x9CD8 | Spannungsversorgung Gurtbringer Fahrerseite defekt |
| 0x9CD9 | Spannungsversorgung Gurtbringer Beifahrerseite defekt |
| 0xE584 | CAN-Low, physikalischer Fehler |
| 0xE585 | CAN-High, Kurzschluss VB |
| 0xE586 | Ground Shift, zu hoch |
| 0xE587 | Controller K-CAN, Bus Off |
| 0xE588 | Controller PT-CAN, Bus Off |
| 0xE58B | Controller PT-CAN, Bus Off |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 6 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9CB9 | 0x01 | - | - | - |
| 0x9CBA | 0x01 | - | - | - |
| 0x9CBB | 0x01 | - | - | - |
| 0x9CBC | 0x01 | - | - | - |
| 0x9CCE | TIEFENTL | - | - | - |
| default | - | - | - | - |

<a id="table-tiefentl"></a>
### TIEFENTL

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 | 0x16 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 9 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | ERR_LAMPE | 0-n | - | 0x7F | Err_Lampe | 1 | 1 | 0 |
| 0x10 | Klemme 15 | 0/1 | high | 0x80 | - | - | - | - |
| 0x11 | Klemme R | 0/1 | high | 0x40 | - | - | - | - |
| 0x12 | Standlicht | 0/1 | high | 0x20 | - | - | - | - |
| 0x13 | Parklicht links | 0/1 | high | 0x10 | - | - | - | - |
| 0x14 | Parklicht rechts | 0/1 | high | 0x08 | - | - | - | - |
| 0x15 | Warnblinklicht | 0/1 | high | 0x04 | - | - | - | - |
| 0x16 | Follow me home | 0/1 | high | 0x02 | - | - | - | - |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-err-lampe"></a>
### ERR_LAMPE

Dimensions: 36 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Fernlicht links, E92/E93: Abbiegelicht links |
| 0x01 | Fernlicht rechts, E92/E93: Abbiegelicht rechts |
| 0x02 | Abblendlicht links |
| 0x03 | Abblendlicht rechts |
| 0x04 | Begrenzungslicht links |
| 0x05 | Begrenzungslicht rechts |
| 0x06 | Nebelscheinwerfer links |
| 0x07 | Nebelscheinwerfer rechts |
| 0x08 | Fahrtrichtungsanzeiger links vorne 1 |
| 0x09 | Fahrtrichtungsanzeiger rechts vorne 1 |
| 0x0A | Fahrtrichtungsanzeiger links hinten |
| 0x0B | Fahrtrichtungsanzeiger rechts hinten |
| 0x0C | unbekannte Lampe 1 |
| 0x0D | Beleuchtung WBL-Taster |
| 0x0E | Bremslicht links |
| 0x0F | Bremslicht rechts |
| 0x10 | Bremslicht mitte |
| 0x11 | Schlusslicht links 1, E92/E93: Tagfahrlicht links |
| 0x12 | Schlusslicht rechts 1, E92/E93: Tagfahrlicht rechts |
| 0x13 | Schlusslicht links 2 |
| 0x14 | Schlusslicht rechts 2 |
| 0x15 | Kennzeichenlicht |
| 0x16 | Innenbeleuchtung |
| 0x17 | Nebelschlusslicht links |
| 0x18 | Nebelschlusslicht rechts |
| 0x19 | Rueckfahrlicht links |
| 0x1A | Rueckfahrlicht rechts |
| 0x1B | Break-Force-Display links |
| 0x1C | Break-Force-Display rechts |
| 0x1D | Klemme 58g |
| 0x1E | LED Fahrtlichtkontrolle |
| 0x1F | LED Vorfeldbeleuchtung |
| 0x20 | unbekannte Lampe 2 |
| 0x21 | unbekannte Lampe 3 |
| 0x22 | unbekannte Lampe 4 |
| 0xFFFF | unbekannte Lampe |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 103 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9308 | Fernlicht links, E92/E93: Abbiegelicht links defekt |
| 0x9309 | Fernlicht rechts, E92/E93: Abbiegelicht rechts defekt |
| 0x930A | Abblendlicht links defekt |
| 0x930B | Abblendlicht rechts defekt |
| 0x930C | Begrenzungslicht links defekt |
| 0x930D | Begrenzungslicht rechts defekt |
| 0x930E | Nebelscheinwerfer links defekt |
| 0x930F | Nebelscheinwerfer rechts defekt |
| 0x9310 | Fahrtrichtungsanzeiger links vorne defekt |
| 0x9311 | Fahrtrichtungsanzeiger rechts vorne defekt |
| 0x9312 | Fahrtrichtungsanzeiger links hinten defekt |
| 0x9313 | Fahrtrichtungsanzeiger rechts hinten defekt |
| 0x9314 | unbekannte Lampe 1 defekt |
| 0x9315 | Beleuchtung WBL-Taster defekt |
| 0x9316 | Bremslicht links defekt |
| 0x9317 | Bremslicht rechts defekt |
| 0x9318 | Bremslicht mitte defekt |
| 0x9319 | Schlusslicht links 1, E92/E93: Tagfahrlicht links defekt |
| 0x931A | Schlusslicht rechts 1, E92/E93: Tagfahrlicht rechts defekt |
| 0x931B | Schlusslicht links 2 defekt |
| 0x931C | Schlusslicht rechts 2 defekt |
| 0x931D | Kennzeichenlicht defekt |
| 0x931E | Innenbeleuchtung defekt |
| 0x931F | Nebelschlusslicht links defekt |
| 0x9320 | Nebelschlusslicht rechts defekt |
| 0x9321 | Rueckfahrlicht links defekt |
| 0x9322 | Rueckfahrlicht rechts defekt |
| 0x9323 | Break-Force-Display links defekt |
| 0x9324 | Break-Force-Display rechts defekt |
| 0x9325 | Klemme 58g defekt |
| 0x9326 | LED Fahrtlichtkontrolle defekt |
| 0x9327 | LED Vorfeldbeleuchtung defekt |
| 0x9328 | LoadDump aktiviert |
| 0x9329 | Bedienteil abgerissen |
| 0x932A | Lichtnotlauf mit Kl.15 aktiv |
| 0x932B | Lichtnotlauf mit Geschwindigkeit aktiv |
| 0x932C | ALC-System defekt |
| 0x932D | ALC-System: AL links abgeschaltet |
| 0x932E | ALC-System: AL rechts abgeschaltet |
| 0x932F | Signal vom Regenlichtsensor unplausibel |
| 0x9330 | Telegramm Geschwindigkeit ungueltig |
| 0x9331 | Telegramm Gierrate Timeout oder ungueltig |
| 0x9332 | Telegramm Lenkwinkel Timeout oder ungueltig |
| 0x9333 | Telegramm Klemmenstatus Timeout oder ungueltig |
| 0x9334 | Telegramm Status-AHM Timeout |
| 0x9335 | Telegramm Status DSC Timeout |
| 0x9336 | Telegramm Status Fahrlicht Timeout |
| 0x9337 | Uebertemperatur FH-Fahrertuer |
| 0x9338 | Uebertemperatur FH-Beifahrertuer |
| 0x9339 | Schliesszylinder defekt |
| 0x933A | Telegramm Fernlichtassistent Timeout |
| 0x933B | Analog-Schalter FH-Fahrertuer defekt |
| 0x933C | Analog-Schalter FH-Beifahrertuer defekt |
| 0x933D | LIN-Schalterblock FH-Fahrertuer defekt |
| 0x933E | LIN-Schalterblock FH-Beifahrertuer defekt |
| 0x933F | LIN-Schalterblock FH-Fahrertuer hinten defekt |
| 0x9340 | LIN-Schalterblock FH-Beifahrertuer hinten defekt |
| 0x9341 | LIN-Schalterblock zentraler FH-Schalter defekt |
| 0x9342 | LIN-Schalterblock Spiegelverstellung horizontal defekt |
| 0x9343 | LIN-Schalterblock Spiegelverstellung vertikal defekt |
| 0x9344 | LIN-Schalterblock Spiegelverstellung beiklappen defekt |
| 0x9345 | LIN-Schalterblock Funktionsschalter 1 defekt |
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

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 91 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9308 | 0x01 | 0x02 | -- | -- |
| 0x9309 | 0x01 | 0x02 | -- | -- |
| 0x930A | 0x01 | 0x02 | -- | -- |
| 0x930B | 0x01 | 0x02 | -- | -- |
| 0x930C | 0x01 | 0x02 | -- | -- |
| 0x930D | 0x01 | 0x02 | -- | -- |
| 0x930E | 0x01 | 0x02 | -- | -- |
| 0x930F | 0x01 | 0x02 | -- | -- |
| 0x9310 | 0x01 | 0x02 | -- | -- |
| 0x9311 | 0x01 | 0x02 | -- | -- |
| 0x9312 | 0x01 | 0x02 | -- | -- |
| 0x9313 | 0x01 | 0x02 | -- | -- |
| 0x9314 | 0x01 | 0x02 | -- | -- |
| 0x9315 | 0x01 | 0x02 | -- | -- |
| 0x9316 | 0x01 | 0x02 | -- | -- |
| 0x9317 | 0x01 | 0x02 | -- | -- |
| 0x9318 | 0x01 | 0x02 | -- | -- |
| 0x9319 | 0x01 | 0x02 | -- | -- |
| 0x931A | 0x01 | 0x02 | -- | -- |
| 0x931B | 0x01 | 0x02 | -- | -- |
| 0x931C | 0x01 | 0x02 | -- | -- |
| 0x931D | 0x01 | 0x02 | -- | -- |
| 0x931E | 0x01 | 0x02 | -- | -- |
| 0x931F | 0x01 | 0x02 | -- | -- |
| 0x9320 | 0x01 | 0x02 | -- | -- |
| 0x9321 | 0x01 | 0x02 | -- | -- |
| 0x9322 | 0x01 | 0x02 | -- | -- |
| 0x9323 | 0x01 | 0x02 | -- | -- |
| 0x9324 | 0x01 | 0x02 | -- | -- |
| 0x9325 | 0x01 | 0x02 | -- | -- |
| 0x9326 | 0x01 | 0x02 | -- | -- |
| 0x9327 | 0x01 | 0x02 | -- | -- |
| 0x9328 | 0x01 | -- | -- | -- |
| 0x9329 | 0x01 | -- | -- | -- |
| 0x932A | 0x01 | -- | -- | -- |
| 0x932B | 0x01 | -- | -- | -- |
| 0x932C | 0x01 | -- | -- | -- |
| 0x932D | 0x01 | -- | -- | -- |
| 0x932E | 0x01 | -- | -- | -- |
| 0x932F | 0x01 | -- | -- | -- |
| 0x9330 | 0x01 | -- | -- | -- |
| 0x9331 | 0x05 | -- | -- | -- |
| 0x9332 | 0x05 | -- | -- | -- |
| 0x9333 | 0x05 | -- | -- | -- |
| 0x9334 | 0x05 | -- | -- | -- |
| 0x9335 | 0x05 | -- | -- | -- |
| 0x9336 | 0x05 | -- | -- | -- |
| 0x9337 | 0x01 | -- | -- | -- |
| 0x9338 | 0x01 | -- | -- | -- |
| 0x9339 | 0x01 | -- | -- | -- |
| 0x933A | 0x01 | -- | -- | -- |
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

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 12 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | -- | unsigned char | -- |  18 | 255 | 0 |
| 0x02 | Betriebsstunden | min | -- | unsigned int | -- | 3 | 1 | 0 |
| 0x03 | Sensorspannung | Volt | -- | unsigned char | -- |  5 | 255 | 0 |
| 0x04 | Motortemperatur | °C | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x05 | Bordnetzspannung | Volt | -- | unsigned char | -- |  18 | 255 | 0 |
| 0x10 | NOT_SENS_DEFEKT | 0/1 | high | 0x01 | - | - | - | - |
| 0x11 | NOT_SENS_NOK | 0/1 | high | 0x02 | - | - | - | - |
| 0x12 | NOT_SCHR_VER_NOK | 0/1 | high | 0x04 | - | - | - | - |
| 0x13 | NOT_USENS_NOK | 0/1 | high | 0x08 | - | - | - | - |
| 0x14 | NOT_MOTOR_DEF | 0/1 | high | 0x10 | - | - | - | - |
| 0x15 | NOT_MOTOR_LWR_DEF | 0/1 | high | 0x20 | - | - | - | - |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-notl"></a>
### NOTL

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 |

<a id="table-lampnrtexte"></a>
### LAMPNRTEXTE

Dimensions: 33 rows × 3 columns

| LAMPNR | NAME | TEXT |
| --- | --- | --- |
| 0x00 | AUSGANG_FL_LINKS | Fernlicht links, E92/E93: Abbiegelicht links |
| 0x01 | AUSGANG_FL_RECHTS | Fernlicht rechts, E92/E93: Abbiegelicht rechts |
| 0x02 | AUSGANG_AL_LINKS | Abblendlicht links |
| 0x03 | AUSGANG_AL_RECHTS | Abblendlicht rechts |
| 0x04 | AUSGANG_BEGRL_LINKS | Begrenzungslicht links |
| 0x05 | AUSGANG_BEGRL_RECHTS | Begrenzungslicht rechts |
| 0x06 | AUSGANG_NSW_LINKS | Nebelscheinwerfer links |
| 0x07 | AUSGANG_NSW_RECHTS | Nebelscheinwerfer rechts |
| 0x08 | AUSGANG_FRA_LINKS_VORN | Fahrtrichtungsanzeiger links vorne |
| 0x09 | AUSGANG_FRA_RECHTS_VORN | Fahrtrichtungsanzeiger rechts vorne |
| 0x0A | AUSGANG_FRA_LINKS_HINTEN | Fahrtrichtungsanzeiger links hinten |
| 0x0B | AUSGANG_FRA_RECHTS_HINTEN | Fahrtrichtungsanzeiger rechts hinten |
| 0x0C | UNBELEGT_1 | unbelegt 1 |
| 0x0D | AUSGANG_BEL_WBL_TASTE | Beleuchtung WBL-Taster |
| 0x0E | AUSGANG_BREMSLICHT_LINKS | Bremslicht links |
| 0x0F | AUSGANG_BREMSLICHT_RECHTS | Bremslicht rechts |
| 0x10 | AUSGANG_BREMSLICHT_MITTE | Bremslicht mitte |
| 0x11 | AUSGANG_SL_BL_LINKS_1 | Schlusslicht/Bremslicht links 1, E92/E93: Tagfahrlicht links |
| 0x12 | AUSGANG_SL_BL_RECHTS_1 | Schlusslicht/Bremslicht rechts 1, E92/E93: Tagfahrlicht rechts |
| 0x13 | AUSGANG_SL_BL_LINKS_2 | Schlusslicht/Bremslicht links 2 |
| 0x14 | AUSGANG_SL_BL_RECHTS_2 | Schlusslicht/Bremslicht rechts 2 |
| 0x15 | AUSGANG_KZL | Kennzeichenlicht |
| 0x16 | AUSGANG_INNENBELEUCHTUNG | Innenbeleuchtung |
| 0x17 | AUSGANG_NSL_LINKS | Nebelschlusslicht links |
| 0x18 | AUSGANG_NSL_RECHTS | Nebelschlusslicht rechts |
| 0x19 | AUSGANG_RFL_LINKS | Rueckfahrlicht links |
| 0x1A | AUSGANG_RFL_RECHTS | Rueckfahrlicht rechts |
| 0x1B | AUSGANG_BFD_LINKS | Break-Force-Display links |
| 0x1C | AUSGANG_BFD_RECHTS | Break-Force-Display rechts |
| 0x1D | AUSGANG_KL_58G | Klemme 58g |
| 0x1E | AUSGANG_FLC_LED | LED Fahrtlichtkontrolle |
| 0x1F | AUSGANG_VORFELD_BEL | LED Vorfeldbeleuchtung |
| 0xFF | UNKNOWN | unbekannte Lampe |

<a id="table-funktionnrtexte"></a>
### FUNKTIONNRTEXTE

Dimensions: 13 rows × 3 columns

| FKTNR | NAME | TEXT |
| --- | --- | --- |
| 0x00 | FKT_FL | Fernlicht, E92/E93: Abbiegelicht |
| 0x01 | FKT_AL | Abblendlicht |
| 0x02 | FKT_SL | Standlicht |
| 0x03 | FKT_NSW | Nebelscheinwerfer |
| 0x04 | FKT_FRA_L | Fahrtrichtungsanzeiger links |
| 0x05 | FKT_FRA_R | Fahrtrichtungsanzeiger rechts |
| 0x06 | FKT_BL_STUFE1 | Bremslichtstufe 1 |
| 0x07 | FKT_BL_STUFE2 | Bremslichtstufe 2 |
| 0x08 | FKT_NSL | Nebelschlusslicht |
| 0x09 | FKT_RFS | Rueckfahrlicht |
| 0x0A | UNKNOWN | unbekannte Funktion |
| 0x0B | UNKNOWN | unbekannte Funktion |
| 0x0C | UNKNOWN | unbekannte Funktion |

<a id="table-zusatzout"></a>
### ZUSATZOUT

Dimensions: 3 rows × 3 columns

| OUTNR | NAME | TEXT |
| --- | --- | --- |
| 0x00 | UNKNOWN | unbekannter Ausgang |
| 0x00 | UNKNOWN | unbekannter Ausgang |
| 0x00 | UNKNOWN | unbekannter Ausgang |

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

<a id="table-fh-richtung"></a>
### FH_RICHTUNG

Dimensions: 4 rows × 3 columns

| FH_R | NAME | TEXT |
| --- | --- | --- |
| 0x00 | NEUTRAL | Fenster nicht bewegen |
| 0x01 | OEFFNEN | Fenster oeffnen |
| 0x03 | SCHLIESSEN | Fenster schliessen |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-auswahl-fenster"></a>
### AUSWAHL_FENSTER

Dimensions: 7 rows × 3 columns

| FH | NAME | TEXT |
| --- | --- | --- |
| 0x01 | 0 | Fensterheber Fahrertuer auswaehlen |
| 0x02 | 1 | Fensterheber Beifahrertuer auswaehlen |
| 0x03 | 2 | beide Fensterheber auswaehlen |
| 0x01 | FH_FAT | Fensterheber Fahrertuer auswaehlen |
| 0x02 | FH_BFT | Fensterheber Beifahrertuer auswaehlen |
| 0x03 | BEIDE_FH | beide Fensterheber auswaehlen |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-auswahl-spiegel"></a>
### AUSWAHL_SPIEGEL

Dimensions: 3 rows × 3 columns

| SPIEGEL | NAME | TEXT |
| --- | --- | --- |
| 0x01 | SPIEGEL_FAT | Spiegel Fahrertuer auswaehlen |
| 0x02 | SPIEGEL_BFT | Spiegel Beifahrertuer auswaehlen |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-richtung-spiegel"></a>
### RICHTUNG_SPIEGEL

Dimensions: 7 rows × 3 columns

| SPIEGEL_R | NAME | TEXT |
| --- | --- | --- |
| 0x00 | NEUTRAL | Spiegel nicht bewegen |
| 0x01 | OBEN | Spiegel nach oben fahren |
| 0x02 | UNTEN | Spiegel nach unten fahren |
| 0x03 | LINKS | Spiegel nach links fahren |
| 0x04 | RECHTS | Spiegel nach rechts fahren |
| 0x05 | BEIKLAPPEN | Spiegel beiklappen |
| 0xFF | ERROR | falscher Eingabewert |

<a id="table-spiegel-heizung"></a>
### SPIEGEL_HEIZUNG

Dimensions: 9 rows × 3 columns

| HEIZUNG | NAME | TEXT |
| --- | --- | --- |
| 0x00 | 0 | Spiegelheizung aus |
| 0x01 | 25 | Spiegelheizung 25% ein |
| 0x02 | 50 | Spiegelheizung 50% ein |
| 0x03 | 75 | Spiegelheizung 75% ein |
| 0x04 | 100 | Spiegelheizung 100% ein |
| 0x05 | 125 | Spiegelheizung 125% ein |
| 0x06 | UNBEGRENZT | Spiegelheizung unbegrenzt ein |
| 0x07 | UNGUELTIG | ungueltig |
| 0xFF | ERROR | falscher Eingabewert |
