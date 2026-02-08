# ARS_70.prg

- Jobs: [130](#jobs)
- Tables: [83](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Aktive Rollstabilisierung E70 |
| ORIGIN | BMW EF-63 Bernhard Schmidt |
| REVISION | 4.000 |
| AUTHOR | ContiTemic PC-FES Anders, BMW TI-432 Helmich |
| COMMENT | Stand zur Integrationsstufe E070-06-10-450 und Anpassungen |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
- [HS_LESEN_DETAIL](#job-hs-lesen-detail) - Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default
- [HS_LOESCHEN](#job-hs-loeschen) - Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
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
- [STATUS_VERSORGUNGEN](#job-status-versorgungen) - Auslesen der Stati von Spanungspegel KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $F020 Entry Status Modus  : Default
- [STATUS_ARS_SENSOREN](#job-status-ars-sensoren) - Auslesen der Stati von ARS Sensoren KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $0F C0 00 00 00 FF 80 Entry Status Modus  : Default
- [STATUS_PROPORTIONAL_VENTILE](#job-status-proportional-ventile) - Auslesen der Stati von Proportional Ventilen KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 0C 0C CC Entry Status Modus  : Default
- [STATUS_SCHALTVENTILE](#job-status-schaltventile) - Auslesen der Stati von Schaltventilen KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 03 03 33 Entry Status Modus  : Default
- [STATUS_CAN_SIGNALE_ARS](#job-status-can-signale-ars) - Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 00 00 00 00 F0 30 Entry Status Modus  : Default
- [STATUS_CAN_GESCHWINDIGKEIT_ARS](#job-status-can-geschwindigkeit-ars) - Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 00 00 00 C0 Entry Status Modus  : Default
- [STATUS_CAN_DREHZAHL_ARS](#job-status-can-drehzahl-ars) - Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 00 00 0F Entry Status Modus  : Default
- [STATUS_CAN_BESCHLEUNIGUNG_ARS](#job-status-can-beschleunigung-ars) - Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 40 00 00 3C Entry Status Modus  : Default
- [STATUS_CAN_TEMP_ARS](#job-status-can-temp-ars) - Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 00 00 30 00 00 C0 Entry Status Modus  : Default
- [STATUS_CAN_DIVERSES_ARS](#job-status-can-diverses-ars) - Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 40 00 00 03 0F 00 Entry Status Modus  : Default
- [STATUS_CAN_ROTOR_POSITION](#job-status-can-rotor-position) - Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 F0 00 00 00 40 Entry Status Modus  : Default
- [STATUS_CAN_ALIVE_ARS](#job-status-can-alive-ars) - Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 00 00 C0 Entry Status Modus  : Default
- [START_INBETRIEBNAHME](#job-start-inbetriebnahme) - alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x00 und 0xFF KWP2000: $31 StartRoutineByLocalIdentifier $30 Inbetriebnahme starten Modus  : Default
- [START_DRUCKRAMPE](#job-start-druckrampe) - alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x00 und 0xFF KWP2000: $31 StartRoutineByLocalIdentifier $35 Rampe Strom Druck lernen Modus  : Default
- [START_OFFSET_WERTE_VA](#job-start-offset-werte-va) - alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x7 (Signal Ungueltig) KWP2000: $31 StartRoutineByLocalIdentifier $36 Nullpunkt Druck VA lernen Modus  : Default
- [START_OFFSET_WERTE_HA](#job-start-offset-werte-ha) - alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x7 (Signal Ungueltig) KWP2000: $31 StartRoutineByLocalIdentifier $37 Nullpunkt Druck HA lernen Modus  : Default
- [START_OFFSET_QUERBESCH](#job-start-offset-querbesch) - alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x7 (Signal Ungueltig) KWP2000: $31 StartRoutineByLocalIdentifier $38 Nullpunkt Aquer Sensor lernen Modus  : Default
- [START_OFFSET_WERTE_HGLV](#job-start-offset-werte-hglv) - alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x7 (Signal Ungueltig) KWP2000: $31 StartRoutineByLocalIdentifier $51, $52, $53, $54 Nullpunkt Hoehenstandssensor lernen Modus  : Default
- [START_LERNEN_NEUE_SENSOR_WERTE_VA](#job-start-lernen-neue-sensor-werte-va) - KWP2000: $31 StartRoutineByLocalIdentifier $40 Sensor Paramenter fuer neuen Drucksensor VA lernen. Parameter laut Sensordatenblatt Modus  : Default
- [START_LERNEN_NEUE_SENSOR_WERTE_HA](#job-start-lernen-neue-sensor-werte-ha) - KWP2000: $31 StartRoutineByLocalIdentifier $41 Sensor Paramenter fuer neuen Drucksensor HA lernen. Parameter laut Sensordatenblatt Modus  : Default
- [START_LERNEN_NEUE_WERTE_QUERBESCH](#job-start-lernen-neue-werte-querbesch) - KWP2000: $31 StartRoutineByLocalIdentifier $42 Sensor Paramenter fuer neuen A Quer Sensor lernen. Parameter laut Sensordatenblatt Modus  : Default
- [START_LERNEN_NEUE_SENSOR_WERTE_HGLV](#job-start-lernen-neue-sensor-werte-hglv) - KWP2000: $31 StartRoutineByLocalIdentifier $55, $56, $57, $58 Sensor Paramenter fuer neuen Hoehenstandssensor lernen. Parameter laut Sensordatenblatt Modus  : Default
- [START_LOESCHEN_LEWI](#job-start-loeschen-lewi) - alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x00 und 0xFF KWP2000: $31 StartRoutineByLocalIdentifier $50 Zuruecksetzen des gelernten Lenkwinkeloffsets Modus  : Default
- [STOP_INBETRIEBNAHME](#job-stop-inbetriebnahme) - KWP2000: $32 StopRoutineByLocalIdentifier $30 Inbetriebnahme stoppen Modus  : Default
- [STOP_DRUCKRAMPE](#job-stop-druckrampe) - KWP2000: $32 StopRoutineByLocalIdentifier $35 Nullpunkt Druck HA lernen Modus  : Default
- [STATUS_INBETRIEBNAHME_ABFRAGEN](#job-status-inbetriebnahme-abfragen) - KWP2000: $33 RequestRoutineResultsByLocalIdentifier $30 Inbetriebnahme Resultat abfragen Modus  : Default
- [STATUS_DRUCKRAMPE_ABFRAGEN](#job-status-druckrampe-abfragen) - KWP2000: $33 RequestRoutineResultsByLocalIdentifier $35 Rampe Strom Druck lernen Resultat abfragen Modus  : Default
- [STATUS_OFFSET_WERTE_VA](#job-status-offset-werte-va) - KWP2000: $33 RequestRoutineresultsByLocalIdentifier $36 Nullpunkt Druck VA gelernter Offset holen Modus  : Default
- [STATUS_OFFSET_WERTE_HA](#job-status-offset-werte-ha) - KWP2000: $33 RequestRoutineresultsByLocalIdentifier $37 Nullpunkt Druck HA gelernter Offset holen Modus  : Default
- [STATUS_OFFSET_QUERBESCH](#job-status-offset-querbesch) - KWP2000: $33 RequestRoutineresultsByLocalIdentifier $38 Nullpunkt BeschleunigungsSensor Offset holen Modus  : Default
- [STATUS_NEUE_SENSOR_WERTE_VA](#job-status-neue-sensor-werte-va) - KWP2000: $33 RequestRoutineresultsByLocalIdentifier $40 Sensor Paramenter fuer neuen Drucksensor VA auslesen. Parameter laut Sensordatenblatt Modus  : Default
- [STATUS_NEUE_SENSOR_WERTE_HA](#job-status-neue-sensor-werte-ha) - KWP2000: $33 RequestRoutineresultsByLocalIdentifier $41 Sensor Paramenter fuer neuen Drucksensor HA auslesen. Parameter laut Sensordatenblatt Modus  : Default
- [STATUS_NEUE_WERTE_QUERBESCH](#job-status-neue-werte-querbesch) - KWP2000: $33 RequestRoutineresultsByLocalIdentifier $42 Sensor Paramenter fuer neuen Querbesch.sensor auslesen. Parameter laut Sensordatenblatt Modus  : Default
- [STATUS_OFFSET_LENKWINKEL](#job-status-offset-lenkwinkel) - KWP2000: $33 RequestRoutineresultsByLocalIdentifier $50 Lenkwinkel Offset holen Modus  : Default
- [STATUS_NEUE_SENSOR_WERTE_HGLV](#job-status-neue-sensor-werte-hglv) - KWP2000: $33 RequestRoutineresultsByLocalIdentifier $55, $56, $57, $58  Sensor Paramenter fuer Hoehenstandssensor auslesen. Parameter laut Sensordatenblatt Modus  : Default
- [STATUS_OFFSET_WERTE_HGLV](#job-status-offset-werte-hglv) - KWP2000: $33 RequestRoutineresultsByLocalIdentifier $51, $52, $53, $54 Für alle Hoehenstandssensoren gelernter Offset holen Modus  : Default
- [STATUS_SG_TEMP](#job-status-sg-temp) - Auslesen der ECU Innentemperatur KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 10 Entry Status Modus  : Default
- [STEUERN_SV_PWM_MIT_FP](#job-steuern-sv-pwm-mit-fp) - KWP2000: $30 InputOutputControlByLocalIdentifier $31 Sicherheitsventil Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe mit Fehlerpruefung
- [STEUERN_SV_PWM_OHNE_FP](#job-steuern-sv-pwm-ohne-fp) - KWP2000: $30 InputOutputControlByLocalIdentifier $31 Sicherheitsventil Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe ohne Fehlerpruefung
- [STEUERN_SV_HOCHLAUFPRUEFUNG](#job-steuern-sv-hochlaufpruefung) - KWP2000: $30 InputOutputControlByLocalIdentifier $31 Sicherheitsventil Modus  : $07 IOCP Nummer Modus  : Hochlaufpruefung (Pruefimpuls)
- [STEUERN_SV_PUSHHOLD](#job-steuern-sv-pushhold) - KWP2000: $30 InputOutputControlByLocalIdentifier $31 Sicherheitsventil Modus  : $07 IOCP Nummer Modus  : Push Hold Ansteuerung
- [STEUERN_RV_PWM_MIT_FP](#job-steuern-rv-pwm-mit-fp) - KWP2000: $30 InputOutputControlByLocalIdentifier $32 Richtungsventil Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe mit Fehlerpruefung
- [STEUERN_RV_PWM_OHNE_FP](#job-steuern-rv-pwm-ohne-fp) - KWP2000: $30 InputOutputControlByLocalIdentifier $32 Richtungsventil Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe ohne Fehlerpruefung
- [STEUERN_RV_HOCHLAUFPRUEFUNG](#job-steuern-rv-hochlaufpruefung) - KWP2000: $30 InputOutputControlByLocalIdentifier $32 Richtungsventil Modus  : $07 IOCP Nummer Modus  : Hochlaufpruefung (Pruefimpuls)
- [STEUERN_RV_PUSHHOLD](#job-steuern-rv-pushhold) - KWP2000: $30 InputOutputControlByLocalIdentifier $32 Richtungsventil Modus  : $07 IOCP Nummer Modus  : Push Hold Ansteuerung
- [STEUERN_PVVA_PWM_MIT_FP](#job-steuern-pvva-pwm-mit-fp) - KWP2000: $30 InputOutputControlByLocalIdentifier $33 Proportionalventil VA Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe mit Fehlerpruefung
- [STEUERN_PVVA_PWM_OHNE_FP](#job-steuern-pvva-pwm-ohne-fp) - KWP2000: $30 InputOutputControlByLocalIdentifier $33 Proportionalventil VA Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe ohne Fehlerpruefung
- [STEUERN_PVVA_HOCHLAUFPRUEFUNG](#job-steuern-pvva-hochlaufpruefung) - KWP2000: $30 InputOutputControlByLocalIdentifier $33 Proportionalventil VA Modus  : $07 IOCP Nummer Modus  : Hochlaufpruefung (Pruefimpuls)
- [STEUERN_PVHA_PWM_MIT_FP](#job-steuern-pvha-pwm-mit-fp) - KWP2000: $30 InputOutputControlByLocalIdentifier $34 Proportionalventil HA Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe mit Fehlerpruefung
- [STEUERN_PVHA_PWM_OHNE_FP](#job-steuern-pvha-pwm-ohne-fp) - KWP2000: $30 InputOutputControlByLocalIdentifier $34 Proportionalventil HA Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe ohne Fehlerpruefung
- [STEUERN_PVHA_HOCHLAUFPRUEFUNG](#job-steuern-pvha-hochlaufpruefung) - KWP2000: $30 InputOutputControlByLocalIdentifier $34 Proportionalventil HA Modus  : $07 IOCP Nummer Modus  : Hochlaufpruefung (Pruefimpuls)
- [STEUERN_PVSD_PWM_MIT_FP](#job-steuern-pvsd-pwm-mit-fp) - KWP2000: $30 InputOutputControlByLocalIdentifier $36 Proportionalventil SD Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe mit Fehlerpruefung
- [STEUERN_PVSD_PWM_OHNE_FP](#job-steuern-pvsd-pwm-ohne-fp) - KWP2000: $30 InputOutputControlByLocalIdentifier $36 Proportionalventil SD Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe ohne Fehlerpruefung
- [STEUERN_PVSD_HOCHLAUFPRUEFUNG](#job-steuern-pvsd-hochlaufpruefung) - KWP2000: $30 InputOutputControlByLocalIdentifier $36 Proportionalventil VA Modus  : $07 IOCP Nummer Modus  : Hochlaufpruefung (Pruefimpuls)
- [STEUERN_ARS_CHECKCONTROL](#job-steuern-ars-checkcontrol) - KWP2000: $30 InputOutputControlByLocalIdentifier $35 Modus  : Default
- [STEUERN_RAMPE_DIAGSTAT_SETZEN](#job-steuern-rampe-diagstat-setzen) - KWP2000: $31 StartRoutineByLocalIdentifier $31 Diagnose Status setzen Modus  : Default
- [STEUERN_RAMPE_PARAMETER](#job-steuern-rampe-parameter) - KWP2000: $31 StartRoutineByLocalIdentifier $32 Rampe setzen Modus  : Default
- [STEUERN_RAMPE_VA](#job-steuern-rampe-va) - KWP2000: $31 StartRoutineByLocalIdentifier $32 Rampe setzen, $31 Diagnose Status setzen Modus  : Default
- [STEUERN_RAMPE_HA](#job-steuern-rampe-ha) - KWP2000: $31 StartRoutineByLocalIdentifier $32 Rampe setzen, $31 Diagnose Status setzen Modus  : Default
- [C_CHECKSUMME](#job-c-checksumme) - Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob
- [IDENT_PD_LESEN](#job-ident-pd-lesen) - letztes Programmierdatum lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $99 ProgrammingDate Modus  : Default
- [IDENT_HWNR_PHYS_LESEN](#job-ident-hwnr-phys-lesen) - Physikalische Hardware Nummer lesen, PECUHN Standard Codierjob KWP2000: $1A ReadECUIdentification $87 PECUHN Index Modus  : Default
- [IDENT_VMECUHVN_LESEN](#job-ident-vmecuhvn-lesen) - HardwareNummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9A vehicleManufacturerECUHardwareVersionNumber Modus  : Default
- [PROGRAMM_REFERENZ_LESEN](#job-programm-referenz-lesen) - Auslesen der Programm Referenz KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz Modus  : Default
- [AIF_AKTUELL_LESEN](#job-aif-aktuell-lesen) - CUIFDT Standard Codierjob KWP2000: $1A ReadECUIdentification $86 CurrentUIFDataTable Modus  : Default
- [AIF_TABELLE_LESEN](#job-aif-tabelle-lesen) - AIF/UIF Datenblock auslesen KWP2000: $23   ReadMemoryByAddress $AdrHigh AdrMid AdrLow UIFM UIFBlockLaenge $00      00     00     07   40 Modus  : Default
- [HARDWARE_REFERENZ_LESEN_PAF_DAF](#job-hardware-referenz-lesen-paf-daf) - Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HardwareReferenz Modus  : Default
- [PROGRAMM_REFERENZ_LESEN_PAF_DAF](#job-programm-referenz-lesen-paf-daf) - Auslesen der Programm Referenz KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz Modus  : Default
- [DATEN_REFERENZ_LESEN_PAF_DAF](#job-daten-referenz-lesen-paf-daf) - Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DatenReferenz Modus  : Default
- [COD_C_LESEN](#job-cod-c-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_C_SCHREIBEN](#job-cod-c-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_N_LESEN](#job-cod-n-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_N_SCHREIBEN](#job-cod-n-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_LESEN](#job-cod-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [COD_SCHREIBEN](#job-cod-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [DATENSATZ_COD_DATUM](#job-datensatz-cod-datum) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [_STEUERN_ERROR_INJECTION](#job-steuern-error-injection) - KWP2000: $31 StartRoutineByLocalIdentifier $34 Error Injection, $31 Diagnose Status setzen Modus  : Default

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

<a id="job-hs-lesen-detail"></a>
### HS_LESEN_DETAIL

Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Historycode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

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

<a id="job-hs-loeschen"></a>
### HS_LOESCHEN

Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default

_No arguments._

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

<a id="job-status-versorgungen"></a>
### STATUS_VERSORGUNGEN

Auslesen der Stati von Spanungspegel KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $F020 Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERSORGUNG_QUERBESCHL_WERT | real | Versorgung Querbeschleunigungssensor Bereich:0 bis 20V |
| STAT_VERSORGUNG_QUERBESCHL_EINH | string | Volt |
| STAT_VERSORGUNG_SCHALTSEN_WERT | real | Versorgung Schaltstellungssensor Bereich:0 bis 20V |
| STAT_VERSORGUNG_SCHALTSEN_EINH | string | Volt |
| STAT_VERSORGUNG_HA_WERT | real | Spannungspegel Bereich:0 bis 20V |
| STAT_VERSORGUNG_HA_EINH | string | Volt |
| STAT_VERSORGUNG_VA_WERT | real | Spannungspegel Bereich: 0 bis 20V |
| STAT_VERSORGUNG_VA_EINH | string | Volt |
| STAT_KLEMME30_WERT | real | Spanung Klemme 30 Bereich: 0 bis 20V |
| STAT_KLEMME30_EINH | string | Volt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-ars-sensoren"></a>
### STATUS_ARS_SENSOREN

Auslesen der Stati von ARS Sensoren KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $0F C0 00 00 00 FF 80 Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QUERBESCHL_HW_WERT | real | gelesener Sensorwert Querbeschl. |
| STAT_QUERBESCHL_HW_EINH | string | Volt |
| STAT_POSITION_HW_WERT | real | gelesener Sensorwert RV |
| STAT_POSITION_HW_EINH | string | Volt |
| STAT_DRUCK_HA_HW_WERT | real | gelesener Sensorwert HA |
| STAT_DRUCK_HA_HW_EINH | string | Volt |
| STAT_DRUCK_VA_HW_WERT | real | gelesener Sensorwert VA |
| STAT_DRUCK_VA_HW_EINH | string | Volt |
| STAT_WECKLEITUNG_HW_WERT | string | Pegel |
| STAT_WECKLEITUNG_HW_EINH | string | Pegel |
| STAT_OELSTAND_HW_WERT | real | gelesener Sensorwert Oelstand |
| STAT_OELSTAND_HW_EINH | string | Volt |
| STAT_QUERBESCHLSEN_WERT | string | Telegrammwert (hex) |
| STAT_QUERBESCHLSEN_TEXT | string | Sensor Zustand, siehe Tabelle --&gt; StatusQuerSens |
| STAT_POSITION_WERT | string | Telegrammwert (hex) |
| STAT_POSITION_TEXT | string | Sensor Zustand, siehe Tabelle --&gt; StatusSchaltSens |
| STAT_DRUCK_HA_WERT | string | Telegrammwert (hex) |
| STAT_DRUCK_HA_TEXT | string | Sensor Zustand, siehe Tabelle --&gt; StatusDruckSens |
| STAT_DRUCK_VA_WERT | string | Telegrammwert (hex) |
| STAT_DRUCK_VA_TEXT | string | Sensor Zustand, siehe Tabelle --&gt; StatusDruckSens |
| STAT_QUERBESCHL_SW_WERT | real | G-Wert Bereich: -50 bis 50m/s*s |
| STAT_QUERBESCHL_SW_EINH | string | m/s*s |
| STAT_POSITION_SW_WERT | real | Zustand |
| STAT_POSITION_SW_EINH | string | Zustand |
| STAT_DRUCK_HA_SW_WERT | real | Druckwert Bereich: 0 bis 300Bar |
| STAT_DRUCK_HA_SW_EINH | string | Bar |
| STAT_DRUCK_VA_SW_WERT | real | Druckwert Bereich: 0 bis 300Bar |
| STAT_DRUCK_VA_SW_EINH | string | Bar |
| STAT_OELSTAND_SW_WERT | string | Pegel |
| STAT_OELSTAND_SW_EINH | string | Pegel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-proportional-ventile"></a>
### STATUS_PROPORTIONAL_VENTILE

Auslesen der Stati von Proportional Ventilen KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 0C 0C CC Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STEUERSTROM_HA_WERT | real | Stromwert Bereich: 0 bis 4A |
| STAT_STEUERSTROM_HA_EINH | string | Ampere |
| STAT_STEUERSTROM_VA_WERT | real | Stromwert Bereich: 0 bis 4A |
| STAT_STEUERSTROM_VA_EINH | string | Ampere |
| STAT_SOLLSTROM_HA_WERT | real | Stromwert Bereich: 0 bis 4A |
| STAT_SOLLSTROM_HA_EINH | string | Ampere |
| STAT_SOLLSTROM_VA_WERT | real | Stromwert Bereich: 0 bis 4A |
| STAT_SOLLSTROM_VA_EINH | string | Ampere |
| STAT_VENTIL_HA_WERT | string | Telegrammwert (Hex) |
| STAT_VENTIL_HA_TEXT | string | Fehlercodes zugeordnet zu den Ventilen |
| STAT_VENTIL_VA_WERT | string | Telegrammwert (Hex) |
| STAT_VENTIL_VA_TEXT | string | Fehlercodes zugeordnet zu den Ventilen |
| STAT_PWM_HA_WERT | real | Reglerwert Bereich: 0 bis 100% |
| STAT_PWM_HA_EINH | string | % |
| STAT_PWM_VA_WERT | real | Reglerwert Bereich: 0 bis 100% |
| STAT_PWM_VA_EINH | string | % |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-schaltventile"></a>
### STATUS_SCHALTVENTILE

Auslesen der Stati von Schaltventilen KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 03 03 33 Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STROM_SICHVENT_WERT | real | Stromwert Bereich: 0 bis 4A |
| STAT_STROM_SICHVENT_EINH | string | Ampere |
| STAT_STROM_RICHTVENT_WERT | real | Stromwert Bereich: 0 bis 4A |
| STAT_STROM_RICHTVENT_EINH | string | Ampere |
| STAT_SOLLSTROM_SICHVENT_WERT | real | Stromwert Bereich: 0 bis 4A |
| STAT_SOLLSTROM_SICHVENT_EINH | string | Ampere |
| STAT_SOLLSTROM_RICHTVENT_WERT | real | Stromwert Bereich: 0 bis 4A |
| STAT_SOLLSTROM_RICHTVENT_EINH | string | Ampere |
| STAT_SICHERHEITSVENTIL_WERT | string | Telegrammwert (Hex) |
| STAT_SICHERHEITSVENTIL_TEXT | string | Fehlercodes |
| STAT_RICHTUNGSVENTIL_WERT | string | Telegrammwert (Hex) |
| STAT_RICHTUNGSVENTIL_TEXT | string | Fehlercodes |
| STAT_PWM_SICHVENT_WERT | real | Reglerwert Bereich: 0 bis 100% |
| STAT_PWM_SICHVENT_EINH | string | % |
| STAT_PWM_RICHTVENT_WERT | real | Reglerwert Bereich: 0 bis 100% |
| STAT_PWM_RICHTVENT_EINH | string | % |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-can-signale-ars"></a>
### STATUS_CAN_SIGNALE_ARS

Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 00 00 00 00 F0 30 Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FEHLER_KL50_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_KL50_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_KL50_NR_WERT | int | 0=0x00, 1=0x01, 2=0x03 |
| STAT_KL50_TEXT | string | Status der KL50 als Text table StatKL50 KL10_TEXT |
| STAT_FEHLER_KL15_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_KL15_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_KL15_NR_WERT | int | 0=0x00, 1=0x01, 2=0x03 |
| STAT_KL15_TEXT | string | Status der KL15 als Text |
| STAT_FEHLER_DSC_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_DSC_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_DSC_WERT | int | Zustand |
| STAT_DSC_EINH | string | Zustand |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-can-geschwindigkeit-ars"></a>
### STATUS_CAN_GESCHWINDIGKEIT_ARS

Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 00 00 00 C0 Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FEHLER_GESCHWINDIGKEIT_FZG_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_GESCHWINDIGKEIT_FZG_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_GESCHWINDIGKEIT_FZG_WERT | real | Fahrzeuggeschwindigkeit Bereich:0.1 bis 350km/h |
| STAT_GESCHWINDIGKEIT_FZG_EINH | string | km/h |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-can-drehzahl-ars"></a>
### STATUS_CAN_DREHZAHL_ARS

Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 00 00 0F Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FEHLER_DREHZAHL_MOTOR_FEHLER_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_DREHZAHL_MOTOR_FEHLER_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_DREHZAHL_MOTOR_FEHLER_WERT | int | Zustand |
| STAT_DREHZAHL_MOTOR_FEHLER_EINH | string | Zustand |
| STAT_FEHLER_DREHZAHL_MOTOR_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_DREHZAHL_MOTOR_TEXT | string | STAT_CAN Fehler in Tabelleneintrag |
| STAT_DREHZAHL_MOTOR_WERT | real | 1/min |
| STAT_DREHZAHL_MOTOR_EINH | string | 1/mín |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-can-beschleunigung-ars"></a>
### STATUS_CAN_BESCHLEUNIGUNG_ARS

Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 40 00 00 3C Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FEHLER_WINKELGESCHW_DSC_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_WINKELGESCHW_DSC_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_WINKELGESCHW_DSC_WERT | real | Gier-Wert Bereich:-100 bis 100 Grad/s |
| STAT_WINKELGESCHW_DSC_EINH | string | Grad/s |
| STAT_FEHLER_QUERBESCHL_DSC_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_QUERBESCHL_DSC_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_QUERBESCHL_DSC_WERT | real | Beschleunigung in m/s*s Bereich: -50 bis 50m/s*s |
| STAT_QUERBESCHL_DSC_EINH | string | m/s*s |
| STAT_CODSTR2_WERT | int | Codierdatenbyte |
| STAT_CODSTR2_TEXT | string | Auswertung des F-CAN enable Bits |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-can-temp-ars"></a>
### STATUS_CAN_TEMP_ARS

Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 00 00 30 00 00 C0 Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FEHLER_AUSSENTEMPERATUR_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_AUSSENTEMPERATUR_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_AUSSENTEMPERATUR_WERT | real | Skalierung 0,01 Grad Celcius |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad Celcius |
| STAT_FEHLER_MOTORTEMPERATUR_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_MOTORTEMPERATUR_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_MOTORTEMPERATUR_WERT | real | Skalierung 0,01 Grad Celcius |
| STAT_MOTORTEMPERATUR_EINH | string | Grad Celcius |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-can-diverses-ars"></a>
### STATUS_CAN_DIVERSES_ARS

Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 40 00 00 03 0F 00 Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FEHLER_KILOMETERSTAND_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_KILOMETERSTAND_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_KILOMETERSTAND_WERT | real | Wegstrecke Bereich:0 bis 16777214km |
| STAT_KILOMETERSTAND_EINH | string | km |
| STAT_FEHLER_LENKRADWINKEL_FEHLER_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_LENKRADWINKEL_FEHLER_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_LENKRADWINKEL_FEHLER_NR | int | LENKWINKF_NR |
| STAT_LENKRADWINKEL_FEHLER_TEXT | string | Status des Lenkradwinkels als Text table StatLenkwinkF LENKWINKF_TEXT |
| STAT_FEHLER_LENKRADWINKEL_WERT | string | Telegrammwert (Hex) des CAN Fehlers |
| STAT_FEHLER_LENKRADWINKEL_TEXT | string | CAN Fehler in Tabelleneintrag |
| STAT_LENKRADWINKEL_WERT | real | Winkel in Grad Bereich: -1433.60Grad bis 1433.60Grad |
| STAT_LENKRADWINKEL_EINH | string | Grad |
| STAT_CODSTR2_WERT | int | Codierdatenbyte |
| STAT_CODSTR2_TEXT | string | Auswertung des F-CAN enable Bits |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-can-rotor-position"></a>
### STATUS_CAN_ROTOR_POSITION

Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 F0 00 00 00 40 Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FEHLER_ROTOR_POSITION_STAT_WERT | string | Errorstatus CAN fuer ST_RTR_PO (Rotor Position), Hexwert |
| STAT_FEHLER_ROTOR_POSITION_STAT_TEXT | string | Errorstatus CAN fuer ST_RTR_PO (Rotor Position), Tabelleneintrag |
| STAT_ROTOR_POSITION_STAT_AFS_WERT | int | ST_RTR_PO - Rotorlagewinkel-Status AFS |
| STAT_ROTOR_POSITION_STAT_AFS_TEXT | string | ST_RTR_PO - Rotorlagewinkel-Status AFS |
| STAT_FEHLER_ROTOR_POSITION_ACTUAL_VALUE_WERT | string | Errorstatus CAN fuer RTR_PO_AVL (Rotor Position, tatsaechlicher Wert), Hexwert |
| STAT_FEHLER_ROTOR_POSITION_ACTUAL_VALUE_TEXT | string | Errorstatus CAN fuer RTR_PO_AVL (tatsaechlicher Wert), Tabelleneintrag |
| STAT_ROTOR_POSITION_ACTUAL_VALUE_WERT | real | RTR_PO_AVL - Rotorlage-Ist-Winkel bezogen aufs Lenkrad Winkel in Grad - Bereich: -1439.95Grad bis 1439.95Grad |
| STAT_ROTOR_POSITION_ACTUAL_VALUE_EINH | string | RTR_PO_AVL - Einheit in 0.1 Grad |
| STAT_CODSTR2_WERT | int | Codierdatenbyte |
| STAT_CODSTR2_TEXT | string | Auswertung des F-CAN enable Bits |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-can-alive-ars"></a>
### STATUS_CAN_ALIVE_ARS

Auslesen der Stati von CAN-Signale-ARS KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 00 00 C0 Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ARS_WERT | int | Status ARS |
| STAT_ARS_INB_TEXT | string | Status ARS ist in Ordnung Ueberwachung eingeschraenkt eingeschraenkter Regelkomfort Fail Safe Oelverlust Fail Safe temporaer |
| STAT_ARS_TEXT | string | Bit x gesetzt |
| STAT_ALIVE_ZAEHLER_WERT | int | zaehlt von 0-14 |
| STAT_ALIVE_ZAEHLER_TEXT | string | Code mit 4 Bit table StatZaehler ZAEHLERTEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-inbetriebnahme"></a>
### START_INBETRIEBNAHME

alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x00 und 0xFF KWP2000: $31 StartRoutineByLocalIdentifier $30 Inbetriebnahme starten Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-druckrampe"></a>
### START_DRUCKRAMPE

alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x00 und 0xFF KWP2000: $31 StartRoutineByLocalIdentifier $35 Rampe Strom Druck lernen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-offset-werte-va"></a>
### START_OFFSET_WERTE_VA

alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x7 (Signal Ungueltig) KWP2000: $31 StartRoutineByLocalIdentifier $36 Nullpunkt Druck VA lernen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-offset-werte-ha"></a>
### START_OFFSET_WERTE_HA

alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x7 (Signal Ungueltig) KWP2000: $31 StartRoutineByLocalIdentifier $37 Nullpunkt Druck HA lernen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-offset-querbesch"></a>
### START_OFFSET_QUERBESCH

alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x7 (Signal Ungueltig) KWP2000: $31 StartRoutineByLocalIdentifier $38 Nullpunkt Aquer Sensor lernen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-offset-werte-hglv"></a>
### START_OFFSET_WERTE_HGLV

alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x7 (Signal Ungueltig) KWP2000: $31 StartRoutineByLocalIdentifier $51, $52, $53, $54 Nullpunkt Hoehenstandssensor lernen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_RADPOS_HGLV | int | Gibt an um welches Rad es sich handelt: 1 - Vorne Links   (FL) 2 - Vorne Rechts  (FR) 3 - Hinten Links  (RL) 4 - Hinten Rechts (RR) |
| SENSOR_OFFSET_HGLV | int | mm-Abweichung von Nullpunktlage (ausgefedert ist immer positiv) in [mm] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-lernen-neue-sensor-werte-va"></a>
### START_LERNEN_NEUE_SENSOR_WERTE_VA

KWP2000: $31 StartRoutineByLocalIdentifier $40 Sensor Paramenter fuer neuen Drucksensor VA lernen. Parameter laut Sensordatenblatt Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_NULLPKT_VA | int | SensorNullpunkt in [mV] |
| SENSOR_STEIGUNG_VA | int | Steigung in [mue Volt/bar] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-lernen-neue-sensor-werte-ha"></a>
### START_LERNEN_NEUE_SENSOR_WERTE_HA

KWP2000: $31 StartRoutineByLocalIdentifier $41 Sensor Paramenter fuer neuen Drucksensor HA lernen. Parameter laut Sensordatenblatt Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_NULLPKT_HA | int | SensorNullpunkt in [mV] |
| SENSOR_STEIGUNG_HA | int | Steigung in [mue Volt/bar] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-lernen-neue-werte-querbesch"></a>
### START_LERNEN_NEUE_WERTE_QUERBESCH

KWP2000: $31 StartRoutineByLocalIdentifier $42 Sensor Paramenter fuer neuen A Quer Sensor lernen. Parameter laut Sensordatenblatt Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_NULLPKT_AQUER | int | SensorNullpunkt in [mV] |
| SENSOR_STEIGUNG_AQUER | int | Steigung in [mVolt/g] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-lernen-neue-sensor-werte-hglv"></a>
### START_LERNEN_NEUE_SENSOR_WERTE_HGLV

KWP2000: $31 StartRoutineByLocalIdentifier $55, $56, $57, $58 Sensor Paramenter fuer neuen Hoehenstandssensor lernen. Parameter laut Sensordatenblatt Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_RADPOS_HGLV | int | Gibt an um welches Rad es sich handelt: 1 - Vorne Links   (FL) 2 - Vorne Rechts  (FR) 3 - Hinten Links  (RL) 4 - Hinten Rechts (RR) |
| SENSOR_NULLPKT_HGLV | int | SensorNullpunkt in [mV] |
| SENSOR_STEIGUNG_HGLV | int | Steigung in [mV/m] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-start-loeschen-lewi"></a>
### START_LOESCHEN_LEWI

alle 4 Radgeschwindigkeiten kleiner 4 km/h DSC Status ungleich 0x00 und 0xFF KWP2000: $31 StartRoutineByLocalIdentifier $50 Zuruecksetzen des gelernten Lenkwinkeloffsets Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-stop-inbetriebnahme"></a>
### STOP_INBETRIEBNAHME

KWP2000: $32 StopRoutineByLocalIdentifier $30 Inbetriebnahme stoppen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| NORMAL_EXIT_WITH_RESULTS_AVAILABLE | int | normales Ende mit Ergebnis  |
| NORMAL_EXIT_WITHOUT_RESULTS_AVAILABLE | int | normales Ende ohne Ergebnis  |
| ABNORMAL_EXIT_WITH_RESULTS_AVAILABLE | int | fehlerhaftes Ende mit Ergebnis  |
| ABNORMAL_EXIT_WITHOUT_RESULTS_AVAILABLE | int | fehlerhaftes Ende ohne Ergebnis  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-stop-druckrampe"></a>
### STOP_DRUCKRAMPE

KWP2000: $32 StopRoutineByLocalIdentifier $35 Nullpunkt Druck HA lernen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| NORMAL_EXIT_WITH_RESULTS_AVAILABLE | int | normales Ende mit Ergebnis  |
| NORMAL_EXIT_WITHOUT_RESULTS_AVAILABLE | int | normales Ende ohne Ergebnis  |
| ABNORMAL_EXIT_WITH_RESULTS_AVAILABLE | int | fehlerhaftes Ende mit Ergebnis  |
| ABNORMAL_EXIT_WITHOUT_RESULTS_AVAILABLE | int | fehlerhaftes Ende ohne Ergebnis  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-inbetriebnahme-abfragen"></a>
### STATUS_INBETRIEBNAHME_ABFRAGEN

KWP2000: $33 RequestRoutineResultsByLocalIdentifier $30 Inbetriebnahme Resultat abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FA_CODE_WERT | int | gewaehlter Fehlercode |
| STAT_FA_CODE | string | gewaehlter Fehlercode |
| STAT_WA_CODE_HEX | string | gefilterte Warnungen ueber &lt;0xC0&gt; |
| STAT_FA_CODE_HEX | string | gefilterte Fehler ueber &lt;0x3F&gt; |
| STAT_ZUSTAND | int | gewaehlter Fehlercode |
| STAT_INBETRIEBNAHME | string | IO, wenn fehlerfrei NIO, wenn fehlerhaft |
| STAT_INBETRIEBNAHME_FEHLER_TEXT | string | IO, wenn fehlerfrei NIO, wenn fehlerhaft |
| STAT_INBETRIEBNAHME_WARNUNG_TEXT | string | IO, wenn fehlerfrei NIO, wenn fehlerhaft |
| STAT_FA_CODE_ERWEITERT_HEX | string | gefilterte Fehler ueber &lt;0x0F&gt; |
| STAT_ANZ_ZUSATZINFOS | int | Anzahl der gefundenen Zusatzinfos |
| STAT_INBETRIEBNAHME_ZUSATZINFO_TEXT | string | Enthaelt die erste Zusatzinfo als Text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-druckrampe-abfragen"></a>
### STATUS_DRUCKRAMPE_ABFRAGEN

KWP2000: $33 RequestRoutineResultsByLocalIdentifier $35 Rampe Strom Druck lernen Resultat abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-offset-werte-va"></a>
### STATUS_OFFSET_WERTE_VA

KWP2000: $33 RequestRoutineresultsByLocalIdentifier $36 Nullpunkt Druck VA gelernter Offset holen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NULLPUNKT_OFFSET_DRUCK_VA_WERT | int | gelernter Nullpunkt Offset VA auslesen |
| STAT_NULLPUNKT_OFFSET_DRUCK_VA_EINH | string | mV |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-offset-werte-ha"></a>
### STATUS_OFFSET_WERTE_HA

KWP2000: $33 RequestRoutineresultsByLocalIdentifier $37 Nullpunkt Druck HA gelernter Offset holen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NULLPUNKT_OFFSET_DRUCK_HA_WERT | int | gelernter Nullpunkt Offset HA auslesen |
| STAT_NULLPUNKT_OFFSET_DRUCK_HA_EINH | string | mV |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-offset-querbesch"></a>
### STATUS_OFFSET_QUERBESCH

KWP2000: $33 RequestRoutineresultsByLocalIdentifier $38 Nullpunkt BeschleunigungsSensor Offset holen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NULLPUNKT_OFFSET_QUERBESCH_WERT | int | gelernter Nullpunkt Offset Querbeschleunigungssenosr auslesen |
| STAT_NULLPUNKT_OFFSET_QUERBESCH_EINH | string | mV |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-neue-sensor-werte-va"></a>
### STATUS_NEUE_SENSOR_WERTE_VA

KWP2000: $33 RequestRoutineresultsByLocalIdentifier $40 Sensor Paramenter fuer neuen Drucksensor VA auslesen. Parameter laut Sensordatenblatt Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSOR_NULLPKT_VA_WERT | int | gelernter SensorNullpunkt in [mV] |
| STAT_SENSOR_NULLPKT_VA_EINH | string | mV |
| STAT_SENSOR_STEIGUNG_VA_WERT | int | gelernte Steigung in [mue Volt/bar] |
| STAT_SENSOR_STEIGUNG_VA_EINH | string | mueV/bar |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-neue-sensor-werte-ha"></a>
### STATUS_NEUE_SENSOR_WERTE_HA

KWP2000: $33 RequestRoutineresultsByLocalIdentifier $41 Sensor Paramenter fuer neuen Drucksensor HA auslesen. Parameter laut Sensordatenblatt Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSOR_NULLPKT_HA_WERT | int | gelernter SensorNullpunkt in [mV] |
| STAT_SENSOR_NULLPKT_HA_EINH | string | mV |
| STAT_SENSOR_STEIGUNG_HA_WERT | int | gelernte Steigung in [mue Volt/bar] |
| STAT_SENSOR_STEIGUNG_HA_EINH | string | mueV/bar |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-neue-werte-querbesch"></a>
### STATUS_NEUE_WERTE_QUERBESCH

KWP2000: $33 RequestRoutineresultsByLocalIdentifier $42 Sensor Paramenter fuer neuen Querbesch.sensor auslesen. Parameter laut Sensordatenblatt Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSOR_NULLPKT_AQUER_WERT | int | gelernter SensorNullpunkt in [mV] |
| STAT_SENSOR_NULLPKT_AQUER_EINH | string | mV |
| STAT_SENSOR_STEIGUNG_AQUER_WERT | int | gelernte Steigung in [mVolt/g] |
| STAT_SENSOR_STEIGUNG_AQUER_EINH | string | mV/g |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-offset-lenkwinkel"></a>
### STATUS_OFFSET_LENKWINKEL

KWP2000: $33 RequestRoutineresultsByLocalIdentifier $50 Lenkwinkel Offset holen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFFSET_LENKWINKEL_WERT | int | gelernter Lenkwinkel Offset auslesen |
| STAT_OFFSET_LENKWINKEL_EINH | string | Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-neue-sensor-werte-hglv"></a>
### STATUS_NEUE_SENSOR_WERTE_HGLV

KWP2000: $33 RequestRoutineresultsByLocalIdentifier $55, $56, $57, $58  Sensor Paramenter fuer Hoehenstandssensor auslesen. Parameter laut Sensordatenblatt Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_RADPOS_HGLV | int | Gibt an um welches Rad es sich handelt: 1 - Vorne Links   (FL) 2 - Vorne Rechts  (FR) 3 - Hinten Links  (RL) 4 - Hinten Rechts (RR) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSOR_NULLPKT_HGLV_WERT | int | gelernter SensorNullpunkt in [mV] |
| STAT_SENSOR_NULLPKT_HGLV_EINH | string | mV |
| STAT_SENSOR_STEIGUNG_HGLV_WERT | int | gelernte Steigung in [Volt/m] bzw. [mV/mm] |
| STAT_SENSOR_STEIGUNG_HGLV_EINH | string | mV/m |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-offset-werte-hglv"></a>
### STATUS_OFFSET_WERTE_HGLV

KWP2000: $33 RequestRoutineresultsByLocalIdentifier $51, $52, $53, $54 Für alle Hoehenstandssensoren gelernter Offset holen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NULLPUNKT_OFFSET_DRUCK_HGLV_FLH_WERT | int | gelernter Nullpunkt Offset Hoehenstand auslesen |
| STAT_NULLPUNKT_OFFSET_DRUCK_HGLV_FRH_WERT | int | gelernter Nullpunkt Offset Hoehenstand auslesen |
| STAT_NULLPUNKT_OFFSET_DRUCK_HGLV_RLH_WERT | int | gelernter Nullpunkt Offset Hoehenstand auslesen |
| STAT_NULLPUNKT_OFFSET_DRUCK_HGLV_RRH_WERT | int | gelernter Nullpunkt Offset Hoehenstand auslesen |
| STAT_NULLPUNKT_OFFSET_DRUCK_HGLV_EINH | string | mV |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-status-sg-temp"></a>
### STATUS_SG_TEMP

Auslesen der ECU Innentemperatur KWP2000: $30 InputOutputControlByLocalIdentifier $01 IOLI $01 IOCP $00 00 00 00 00 00 10 Entry Status Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SG_TEMP_WERT | real | Versorgung Aussentemperatursensor Bereich:-40 bis 120 Grad Celsius |
| STAT_SG_TEMP_EINH | string | Grad Celsius |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-steuern-sv-pwm-mit-fp"></a>
### STEUERN_SV_PWM_MIT_FP

KWP2000: $30 InputOutputControlByLocalIdentifier $31 Sicherheitsventil Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe mit Fehlerpruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STROM_MA_SV | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Strom in mA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-sv-pwm-ohne-fp"></a>
### STEUERN_SV_PWM_OHNE_FP

KWP2000: $30 InputOutputControlByLocalIdentifier $31 Sicherheitsventil Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe ohne Fehlerpruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STROM_MA_SV | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Strom in mA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-sv-hochlaufpruefung"></a>
### STEUERN_SV_HOCHLAUFPRUEFUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $31 Sicherheitsventil Modus  : $07 IOCP Nummer Modus  : Hochlaufpruefung (Pruefimpuls)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-sv-pushhold"></a>
### STEUERN_SV_PUSHHOLD

KWP2000: $30 InputOutputControlByLocalIdentifier $31 Sicherheitsventil Modus  : $07 IOCP Nummer Modus  : Push Hold Ansteuerung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-rv-pwm-mit-fp"></a>
### STEUERN_RV_PWM_MIT_FP

KWP2000: $30 InputOutputControlByLocalIdentifier $32 Richtungsventil Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe mit Fehlerpruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STROM_MA_RV | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Strom in mA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-rv-pwm-ohne-fp"></a>
### STEUERN_RV_PWM_OHNE_FP

KWP2000: $30 InputOutputControlByLocalIdentifier $32 Richtungsventil Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe ohne Fehlerpruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STROM_MA_RV | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Strom in mA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-rv-hochlaufpruefung"></a>
### STEUERN_RV_HOCHLAUFPRUEFUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $32 Richtungsventil Modus  : $07 IOCP Nummer Modus  : Hochlaufpruefung (Pruefimpuls)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-rv-pushhold"></a>
### STEUERN_RV_PUSHHOLD

KWP2000: $30 InputOutputControlByLocalIdentifier $32 Richtungsventil Modus  : $07 IOCP Nummer Modus  : Push Hold Ansteuerung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-pvva-pwm-mit-fp"></a>
### STEUERN_PVVA_PWM_MIT_FP

KWP2000: $30 InputOutputControlByLocalIdentifier $33 Proportionalventil VA Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe mit Fehlerpruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STROM_MA_PVVA | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Strom in mA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-pvva-pwm-ohne-fp"></a>
### STEUERN_PVVA_PWM_OHNE_FP

KWP2000: $30 InputOutputControlByLocalIdentifier $33 Proportionalventil VA Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe ohne Fehlerpruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STROM_MA_PVVA | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Strom in mA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-pvva-hochlaufpruefung"></a>
### STEUERN_PVVA_HOCHLAUFPRUEFUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $33 Proportionalventil VA Modus  : $07 IOCP Nummer Modus  : Hochlaufpruefung (Pruefimpuls)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-pvha-pwm-mit-fp"></a>
### STEUERN_PVHA_PWM_MIT_FP

KWP2000: $30 InputOutputControlByLocalIdentifier $34 Proportionalventil HA Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe mit Fehlerpruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STROM_MA_PVHA | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Strom in mA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-pvha-pwm-ohne-fp"></a>
### STEUERN_PVHA_PWM_OHNE_FP

KWP2000: $30 InputOutputControlByLocalIdentifier $34 Proportionalventil HA Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe ohne Fehlerpruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STROM_MA_PVHA | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Strom in mA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-pvha-hochlaufpruefung"></a>
### STEUERN_PVHA_HOCHLAUFPRUEFUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $34 Proportionalventil HA Modus  : $07 IOCP Nummer Modus  : Hochlaufpruefung (Pruefimpuls)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-pvsd-pwm-mit-fp"></a>
### STEUERN_PVSD_PWM_MIT_FP

KWP2000: $30 InputOutputControlByLocalIdentifier $36 Proportionalventil SD Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe mit Fehlerpruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STROM_MA_PVSD | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Strom in mA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-pvsd-pwm-ohne-fp"></a>
### STEUERN_PVSD_PWM_OHNE_FP

KWP2000: $30 InputOutputControlByLocalIdentifier $36 Proportionalventil SD Modus  : $07 IOCP Nummer Modus  : PWM Ausgabe ohne Fehlerpruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STROM_MA_PVSD | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Strom in mA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-pvsd-hochlaufpruefung"></a>
### STEUERN_PVSD_HOCHLAUFPRUEFUNG

KWP2000: $30 InputOutputControlByLocalIdentifier $36 Proportionalventil VA Modus  : $07 IOCP Nummer Modus  : Hochlaufpruefung (Pruefimpuls)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-ars-checkcontrol"></a>
### STEUERN_ARS_CHECKCONTROL

KWP2000: $30 InputOutputControlByLocalIdentifier $35 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| UNTERSERVICE | int | Hex-Auftrag an SG |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CHECK_CONTROL_MELDUNG_WERT | int | Telegramm Wert |
| CHECK_CONTROL_MELDUNG_TEXT | string | Check Control Meldungen, siehe Tabelle CheckConrtol |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-rampe-diagstat-setzen"></a>
### STEUERN_RAMPE_DIAGSTAT_SETZEN

KWP2000: $31 StartRoutineByLocalIdentifier $31 Diagnose Status setzen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_WORT | int | 16Bit Bit1-2  - Bit3    Modus Inbetriebnahme Bit4    Rampmode active Bit5    diag pSynt Bit6    diag iSynt Bit7    diag sSynt Bit8    - Bit9    FehlerSimMode Bit10-16 - |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-rampe-parameter"></a>
### STEUERN_RAMPE_PARAMETER

KWP2000: $31 StartRoutineByLocalIdentifier $32 Rampe setzen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_RAMP_CTRL_STATUS | int | 16Bit Bit1    Rampe HA Halt Bit2    Rampe HA Ab Bit3    Rampe HA Auf Bit4    Rampe VA Halt Bit5    Rampe VA Ab Bit6    Rampe VA Auf Bit7    Rampe zusammen (bits 4-6 auf bits 1-3 spiegeln) Bit8-16 - |
| DIAG_RAMP_TIME_VA | int | Quantisierung 0,001s Dauer der Rampe VA in ms |
| DIAG_RAMP_TIME_HA | int | Quantisierung 0,001s Dauer der Rampe HA in ms |
| DIAG_RAMP_HIGHLIMIT_VA | int | Quantisierung 0,001A oder 0.1bar oder 0.1% Maxwert der Rampe VA |
| DIAG_RAMP_HIGHLIMIT_HA | int | Quantisierung 0,001A oder 0.1bar oder 0.1% Maxwert der Rampe HA |
| DIAG_RAMP_RV_FS_STATUS | int | 16Bit Bit1-2  - Bit3    (MI fails) Modus Failsafe Bit4    - Bit5    (MI reli) Modus Richtungsventilvorgabe Bit6-16 - |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-rampe-va"></a>
### STEUERN_RAMPE_VA

KWP2000: $31 StartRoutineByLocalIdentifier $32 Rampe setzen, $31 Diagnose Status setzen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_RAMP_CTRL_STATUS | int | 16Bit Bit1-3  nur bei Rampe HA Bit4    Rampe VA Halt Bit5    Rampe VA Ab Bit6    Rampe VA Auf Bit7    nur fuer Doppelrampe Bit8-16 - nur Bits 4-6 zulaessig |
| DIAG_RAMP_TIME | int | Quantisierung 0,001s Dauer der Rampe VA in ms |
| DIAG_RAMP_HIGHLIMIT | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Maxwert der Rampe VA |
| DIAG_RAMP_RV_FS_STATUS | int | 16Bit Bit1-2  - Bit3    (MI fails) Modus Failsafe Bit4    - Bit5    (MI reli) Modus Richtungsventilvorgabe Bit6-16 - |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-steuern-rampe-ha"></a>
### STEUERN_RAMPE_HA

KWP2000: $31 StartRoutineByLocalIdentifier $32 Rampe setzen, $31 Diagnose Status setzen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_RAMP_CTRL_STATUS | int | 16Bit Bit1    Rampe HA Halt Bit2    Rampe HA Ab Bit3    Rampe HA Auf Bit4-7  nur Rampe HA oder zusammen Bit8-16 - nur Bits 1-3 zulaessig |
| DIAG_RAMP_TIME | int | Quantisierung 0,001s Dauer der Rampe HA in ms |
| DIAG_RAMP_HIGHLIMIT | int | Quantisierung 0,001A Bereich 0 mA - 3000 mA Maxwert der Rampe HA |
| DIAG_RAMP_RV_FS_STATUS | int | 16Bit Bit1-2  - Bit3    (MI fails) Modus Failsafe Bit4    - Bit5    (MI reli) Modus Richtungsventilvorgabe Bit6-16 - |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

<a id="job-c-checksumme"></a>
### C_CHECKSUMME

Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| OUT_BUFFER | binary | Als Result wird der gefuellte Binaerbuffer zurueckgegeben Der Binaerbuffer hat den Aufbau von BINAER_BUFFER |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ident-pd-lesen"></a>
### IDENT_PD_LESEN

letztes Programmierdatum lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $99 ProgrammingDate Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| ID_DATUM | string | TT.MM.JJJJ |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-hwnr-phys-lesen"></a>
### IDENT_HWNR_PHYS_LESEN

Physikalische Hardware Nummer lesen, PECUHN Standard Codierjob KWP2000: $1A ReadECUIdentification $87 PECUHN Index Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HWNR_PHYS | string | physikalische Hardwarenummer |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-vmecuhvn-lesen"></a>
### IDENT_VMECUHVN_LESEN

HardwareNummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9A vehicleManufacturerECUHardwareVersionNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_HW_NR | string | BMW-Hardwarenummer |
| IDENT_DATEN | binary | Hex-Daten an Cotool |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-programm-referenz-lesen"></a>
### PROGRAMM_REFERENZ_LESEN

Auslesen der Programm Referenz KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROGRAMM_REFERENZ | string | Herstellerkennung & Projektnummer & Projektindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aif-aktuell-lesen"></a>
### AIF_AKTUELL_LESEN

CUIFDT Standard Codierjob KWP2000: $1A ReadECUIdentification $86 CurrentUIFDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BELEGT | int | 0 --&gt; gesmmtes AIF Feld ist nich frei, 1--&gt; mindestens ein Byte enthaelt einen Wert ungleich 0xFF |
| AIF_ANZ_DATEN_HEX | string | Telegrammwert in HEX Verweis auf naechstes AIF Feld |
| AIF_ANZ_DATEN | int | AIF Feld Typ Groesse des jeweiligen Eintrages ist aus dem Adressofset ersichtlich 0x40_hex ( 64_dez ) Power PC 0x33_hex ( 51_dez ) fuer alle anderen Anwender des grossen AIF Feldes 0x12_hex ( 18_dez ) letztmoeglicher Blockeintrag 0xFE_hex ( 254_dez ) letztmöglicher Eintrag 0x01_hex ( 64_dez ) nur ein Eintrag der aber ueberschreibbar ist 0xFF_hex ( 255_dez ) freier Speicherplatz 0x00_hex ( 00_dez ) freier Speicherplatz |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FAHRGESTELL_NR_HEX | string | Telegrammdarstellung Fahrgestellnummer (7 Byte) |
| AIF_PROGRAMMIER_DATUM | string | Programmierdatum in yyyy.mm.tt |
| AIF_PROGRAMMIER_DATUM_HEX | string | Speicherdarstellung/Telegrammdarstellung (4 Byte) |
| AIF_ZUSAMMENBAU_NR | string | Zusammenbaunummer |
| AIF_ZUSAMMENBAU_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_DATENSATZ_NR | string | Datensatznummer |
| AIF_DATENSATZ_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_BEHOERDEN_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_HAENDLER_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (3 Byte) |
| AIF_TESTER_NR | string | Haendlernummer |
| AIF_TESTER_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (5 Byte) |
| AIF_KM_STAND | string | Kilometerstand bei der Programmierung |
| AIF_KM_STAND_HEX | string | Speicherdarstellung/Telegrammdarstellung (1 Byte) |
| AIF_PROGRAMM_STAND | string | Programmstand als Programmreferenz |
| AIF_PROGRAMM_STAND_HEX | string | Speicherdarstellung/Telegrammdarstellung (12 Byte) |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 10-stellig falls vorhanden, sonst 7-stellig zusammen mit Fahrgestellnummer kurz ('AIF_FAHRGESTELL_NR') 10 + 7 Byte    17-stellig |
| AIF_FG_NR_LANG_HEX | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig zusammen mit Fahrgestellnummer kurz ('AIF_FAHRGESTELL_NR') 10 + 7 Byte    17-stellig Speicherdarstellung/Telegrammdarstellung (10 Byte) |
| AIF_RESERVE | string | Reserve fuer MPC555 |
| AIF_RESERVE_HEX | string | Speicherdarstellung/Telegrammdarstellung (13 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Daten von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aif-tabelle-lesen"></a>
### AIF_TABELLE_LESEN

AIF/UIF Datenblock auslesen KWP2000: $23   ReadMemoryByAddress $AdrHigh AdrMid AdrLow UIFM UIFBlockLaenge $00      00     00     07   40 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_NR | int | == 0 : aktuelles AIF &gt; 0 : Nummer des zu lesenden AIF default = 0 : aktuelles AIF AIF Blocknummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_ANZ_DATEN_HEX | string | Telegrammwert in HEX Verweis auf naechstes AIF Feld |
| AIF_ANZ_DATEN | int | AIF Feld Typ Groesse des jeweiligen Eintrages ist aus dem Adressofset ersichtlich 0x40_hex ( 64_dez ) Power PC 0x33_hex ( 51_dez ) fuer alle anderen Anwender des grossen AIF Feldes 0x12_hex ( 18_dez ) letztmoeglicher Blockeintrag 0xFE_hex ( 254_dez ) letztmöglicher Eintrag 0x01_hex ( 64_dez ) nur ein Eintrag der aber ueberschreibbar ist 0xFF_hex ( 255_dez ) freier Speicherplatz 0x00_hex ( 00_dez ) freier Speicherplatz |
| BELEGT | int | 0 --&gt; gesmmtes AIF Feld ist nich frei, 1--&gt; mindestens ein Byte enthaelt einen Wert ungleich 0xFF |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ADRESSE | long | logische Adresse des AIF Feldes |
| AIF_ADRESSE_PHYSIKALISCH | long | physikalische Adresse des AIF Feldes |
| LOGISCHE_ADRESSE | string | Telegrammwert in HEX logische Adresse des AIF Feldes |
| PHYSIKALISCHE_ADRESSE | string | Telegrammwert in HEX physikalische Adresse des AIF Feldes |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FAHRGESTELL_NR_HEX | string | Telegrammdarstellung Fahrgestellnummer (7 Byte) |
| AIF_PROGRAMMIER_DATUM | string | Programmierdatum in yyyy.mm.tt |
| AIF_PROGRAMMIER_DATUM_HEX | string | Speicherdarstellung/Telegrammdarstellung (4 Byte) |
| AIF_ZUSAMMENBAU_NR | string | Zusammenbaunummer |
| AIF_ZUSAMMENBAU_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_DATENSATZ_NR | string | Datensatznummer |
| AIF_DATENSATZ_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_BEHOERDEN_NR | string | Behoerdennummer |
| AIF_BEHOERDEN_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (6 Byte) |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_HAENDLER_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (3 Byte) |
| AIF_TESTER_NR | string | Haendlernummer |
| AIF_TESTER_NR_HEX | string | Speicherdarstellung/Telegrammdarstellung (5 Byte) |
| AIF_KM_STAND | string | Kilometerstand bei der Programmierung |
| AIF_KM_STAND_HEX | string | Speicherdarstellung/Telegrammdarstellung (1 Byte) |
| AIF_PROGRAMM_STAND | string | Programmstand als Programmreferenz |
| AIF_PROGRAMM_STAND_HEX | string | Speicherdarstellung/Telegrammdarstellung (12 Byte) |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 10-stellig falls vorhanden, sonst 7-stellig zusammen mit Fahrgestellnummer kurz ('AIF_FAHRGESTELL_NR') 10 + 7 Byte    17-stellig |
| AIF_FG_NR_LANG_HEX | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig zusammen mit Fahrgestellnummer kurz ('AIF_FAHRGESTELL_NR') 10 + 7 Byte    17-stellig Speicherdarstellung/Telegrammdarstellung (10 Byte) |
| AIF_RESERVE | string | Reserve fuer MPC555 |
| AIF_RESERVE_HEX | string | Speicherdarstellung/Telegrammdarstellung (13 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Auftrag an SG |

<a id="job-hardware-referenz-lesen-paf-daf"></a>
### HARDWARE_REFERENZ_LESEN_PAF_DAF

Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HardwareReferenz Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HARDWARE_REFERENZ | string | Hardware Referenz |
| HARDWARE_ZZZ | string | Hardware Referenz ZZZ Nummer |
| HARDWARE_PPP | string | Hardware Referenz PPP Nummer |
| HARDWARE_X | string | Hardware Referenz X Nummer |
| TEMP1 | binary | erster Telegrammteil |
| TEMP2 | binary | zweiter Telegrammteil |
| TEMP3 | binary | dritter Telegrammteil |
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Auftrag an SG |

<a id="job-programm-referenz-lesen-paf-daf"></a>
### PROGRAMM_REFERENZ_LESEN_PAF_DAF

Auslesen der Programm Referenz KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROGRAMM_REFERENZ | string | Herstellerkennung & Projektnummer & Projektindex |
| HARDWARE_REFERENZ | string | Herstellerkennung & Projektnummer & Projektindex |
| HARDWARE_ZZZ | string | Hardware Referenz ZZZ Nummer |
| HARDWARE_PPP | string | Hardware Referenz PPP Nummer |
| HARDWARE_X | string | Hardware Referenz X Nummer |
| PROGRAMM_V | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_BB | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_X | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_H | string | Herstellerkennung & Projektnummer & Projektindex |
| TEMP1 | binary | erster Telegrammteil |
| TEMP2 | binary | zweiter Telegrammteil |
| TEMP3 | binary | dritter Telegrammteil |
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Auftrag an SG |

<a id="job-daten-referenz-lesen-paf-daf"></a>
### DATEN_REFERENZ_LESEN_PAF_DAF

Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DatenReferenz Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_REFERENZ | string | Daten Referenz |
| PROGRAMM_REFERENZ | string | Herstellerkennung & Projektnummer & Projektindex |
| HARDWARE_REFERENZ | string | Herstellerkennung & Projektnummer & Projektindex |
| HARDWARE_ZZZ | string | Hardware Referenz ZZZ Nummer |
| HARDWARE_PPP | string | Hardware Referenz PPP Nummer |
| HARDWARE_X | string | Hardware Referenz X Nummer |
| PROGRAMM_V | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_BB | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_X | string | Herstellerkennung & Projektnummer & Projektindex |
| PROGRAMM_H | string | Herstellerkennung & Projektnummer & Projektindex |
| DATEN_D | string | Daten Referenz |
| DATEN_XXXX | string | Daten Referenz |
| TEMP1 | binary | erster Telegrammteil |
| TEMP2 | binary | zweiter Telegrammteil |
| TEMP3 | binary | dritter Telegrammteil |
| JOB_STATUS_1 | string | 3-fache Telegrammlaenge nicht vorhanden |
| JOB_STATUS_2 | string | Vergleich der Inhalte in den Telegrammen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Auftrag an SG |

<a id="job-cod-c-lesen"></a>
### COD_C_LESEN

Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-cod-c-schreiben"></a>
### COD_C_SCHREIBEN

Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-cod-n-lesen"></a>
### COD_N_LESEN

Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-cod-n-schreiben"></a>
### COD_N_SCHREIBEN

Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-cod-lesen"></a>
### COD_LESEN

Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-cod-schreiben"></a>
### COD_SCHREIBEN

Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CODIER_DATEN | binary | Codierdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-datensatz-cod-datum"></a>
### DATENSATZ_COD_DATUM

Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATENSATZ_DATUM_TAG | int | Herstelldatum (Tag) |
| DATENSATZ_DATUM_MONAT | int | Herstelldatum (Monat) |
| DATENSATZ_DATUM_JAHR | int | Herstelldatum (Jahr) |
| DATENSATZ_CODIER_DATUM | binary | Codierdaten |
| COD_DATUM_TAG | int | Herstelldatum (Tag) |
| COD_DATUM_MONAT | int | Herstelldatum (Monat) |
| COD_DATUM_JAHR | int | Herstelldatum (Jahr) |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BIN_BUFFER | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_DATEN | binary | Hex-Antwort von SG |

<a id="job-steuern-error-injection"></a>
### _STEUERN_ERROR_INJECTION

KWP2000: $31 StartRoutineByLocalIdentifier $34 Error Injection, $31 Diagnose Status setzen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_ERR_SIM_ACTIVE | int | 8Bit 0 --&gt; off, groesser 0 --&gt; on/aktiv |
| DIAG_ERR_SIM_LL_FORCE | int | Fehler erzeugen/ erzwingen Bit1    aqARS Bit2    p_VA Bit3    p_HA Bit4    i_VA Bit5    i_HA Bit6    i_RV Bit7    i_FS Bit8    i_SD Bit9    u_bat Bit10   - Bit11   - Bit12   n_mot Bit13   psipkt Bit14   v_fzg Bit15   aqDSC Bit16   - |
| DIAG_ERR_SIM_LL_DISABLE | int | Fehlererkennung fuer bestimmte Fehler deaktivieren Bits: siehe DIAG_ERR_SIM_LL_FORCE |
| DIAG_ERR_SIM_HL_FORCE | int | Fehler erzeugen/ erzwingen Bit1    aqARS Grd Bit2    aqARS Kons Bit3    aqDSC Grd Bit4    aqDSC Kons Bit5    lewi Grd Bit6    lewi Kons Bit7    Wankrate Grd Bit8    Wankrate Kons Bit9-16 - |
| DIAG_ERR_SIM_HL_DISABLE | int | Fehlererkennung fuer bestimmte Fehler deaktivieren Bits: siehe DIAG_ERR_SIM_HL_FORCE |
| DIAG_ERR_SIM_RV_FS_STATUS | int | Vorgaben fuer Richtungs- und Sicherheitsventil (16Bit) Bit1    RV invertieren Bit2    RV rechts Bit3    RV links Bit4    (MI fails) Failsafevorgabe im FehlerSimModus Bit5-16 - |
| DIAG_ERR_SIM_PWM_STATUS | int | PWM, optionen muessen einzeln gesetzt werden koennen (16Bit) Bit1    VA PWM Sprung Bit2    VA PWM Halten Bit3    HA PWM Sprung Bit4    HA PWM Halten Bit5-16 - |
| DIAG_ERR_SIM_PWM_VALUE_VA | int | in Prozent [%] |
| DIAG_ERR_SIM_PWM_VALUE_HA | int | in Prozent [%] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_DATEN | binary | Hex-Daten von SG |

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
- [HARTTEXTE](#table-harttexte) (14 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (2 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (82 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (82 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (44 × 9)
- [FARTTYP](#table-farttyp) (82 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (58 × 2)
- [HORTTEXTE](#table-horttexte) (82 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HUMWELTMATRIX](#table-humweltmatrix) (82 × 5)
- [HUMWELTTEXTE](#table-humwelttexte) (44 × 9)
- [HARTTYP](#table-harttyp) (82 × 5)
- [HARTTEXTEINDIVIDUELL](#table-harttexteindividuell) (58 × 2)
- [IORTTEXTE](#table-iorttexte) (24 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (24 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (7 × 9)
- [IARTTYP](#table-iarttyp) (24 × 5)
- [IARTTEXTEINDIVIDUELL](#table-iarttexteindividuell) (16 × 2)
- [BUS_TYPEN](#table-bus-typen) (7 × 2)
- [DIGITAL](#table-digital) (1 × 3)
- [EE_ECU](#table-ee-ecu) (1 × 17)
- [EEECU_10](#table-eeecu-10) (3 × 2)
- [EEECU_F](#table-eeecu-f) (3 × 2)
- [EEECU_E](#table-eeecu-e) (3 × 2)
- [EEECU_D](#table-eeecu-d) (3 × 2)
- [EEECU_C](#table-eeecu-c) (3 × 2)
- [EEECU_B](#table-eeecu-b) (3 × 2)
- [EEECU_A](#table-eeecu-a) (3 × 2)
- [EEECU_9](#table-eeecu-9) (3 × 2)
- [EEECU_8](#table-eeecu-8) (3 × 2)
- [EEECU_7](#table-eeecu-7) (3 × 2)
- [EEECU_6](#table-eeecu-6) (3 × 2)
- [EEECU_5](#table-eeecu-5) (3 × 2)
- [EEECU_4](#table-eeecu-4) (3 × 2)
- [EEECU_3](#table-eeecu-3) (3 × 2)
- [EEECU_2](#table-eeecu-2) (3 × 2)
- [EEECU_1](#table-eeecu-1) (3 × 2)
- [INWA](#table-inwa) (5 × 2)
- [INFH](#table-infh) (38 × 2)
- [INFH_ERW](#table-infh-erw) (5 × 2)
- [STATKL15](#table-statkl15) (4 × 2)
- [STATKL50](#table-statkl50) (4 × 2)
- [STATLENKWINKF](#table-statlenkwinkf) (9 × 2)
- [STATLENKWINKT](#table-statlenkwinkt) (4 × 2)
- [STATZAEHLER](#table-statzaehler) (16 × 2)
- [STATMOTORDREH](#table-statmotordreh) (4 × 2)
- [CHECKCONRTOL](#table-checkconrtol) (7 × 2)
- [STATUSSCHALTVENTILE](#table-statusschaltventile) (10 × 2)
- [STATUSPROPVENTILE](#table-statuspropventile) (10 × 2)
- [STATUSDRUCKSENS](#table-statusdrucksens) (6 × 2)
- [STATUSSCHALTSENS](#table-statusschaltsens) (6 × 2)
- [STATUSQUERSENS](#table-statusquersens) (6 × 2)
- [STATUSWECKSENS](#table-statuswecksens) (3 × 2)
- [STATUSOELSTANDSENS](#table-statusoelstandsens) (3 × 2)
- [PTCANSIGNALE](#table-ptcansignale) (5 × 2)
- [STATUSDSC](#table-statusdsc) (6 × 2)
- [PRE_DRIVE](#table-pre-drive) (1 × 5)
- [PRE_DRIVE_1](#table-pre-drive-1) (3 × 2)
- [PRE_DRIVE_2](#table-pre-drive-2) (3 × 2)
- [PRE_DRIVE_3](#table-pre-drive-3) (3 × 2)
- [PRE_DRIVE_4](#table-pre-drive-4) (3 × 2)
- [INBETR](#table-inbetr) (1 × 8)
- [INBETR_1](#table-inbetr-1) (3 × 2)
- [INBETR_2](#table-inbetr-2) (3 × 2)
- [INBETR_3](#table-inbetr-3) (3 × 2)
- [INBETR_4](#table-inbetr-4) (3 × 2)
- [INBETR_5](#table-inbetr-5) (3 × 2)
- [INBETR_6](#table-inbetr-6) (3 × 2)
- [INBETR_7](#table-inbetr-7) (3 × 2)

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

Dimensions: 2 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | ERROR_... |
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

Dimensions: 82 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5D4C | Sicherheitsventil |
| 0x5D4D | Richtungsventil |
| 0x5D4E | Proportionalventil VA |
| 0x5D4F | Proportionalventil HA |
| 0x5D50 | Versorgung Drucksensor VA |
| 0x5D51 | Versorgung Drucksensor HA |
| 0x5D52 | Versorgung Schaltstellungssensor |
| 0x5D53 | Versorgung Querbeschleunigungssensor |
| 0x5D54 | Lernen Drucksensor VA |
| 0x5D55 | Lernen Drucksensor HA |
| 0x5D56 | Lernen Hoehenstandssensor |
| 0x5D57 | Lernen Querbeschleunigungssensor |
| 0x5D5A | Konsistenz LWS |
| 0x5D5B | Konsistenz Druck VA |
| 0x5D5C | Konsistenz Druck HA |
| 0x5D5E | Konsistenz Strommessung Propventile |
| 0x5D5F | Konsistenz Strommessung Schaltventile |
| 0x5D60 | Oelstandssensor |
| 0x5D61 | KL30 ARS-SG |
| 0x5D62 | ECU intern |
| 0x5D64 | Codierdatenfehler |
| 0x5D65 | Status Richtungsventil |
| 0x5D67 | Konsistenz Fahrgestellnummer |
| 0x5D69 | Fehlerspeicher defekt |
| 0x5D6A | VDM Wankratenüberwachung |
| 0x5D6B | Oelstandssensorelektronik |
| 0x5D6C | Inbetriebnahme: RV bestromt |
| 0x5D6D | Inbetriebnahme: RV unbestromt |
| 0x5D6E | Inbetriebnahme: FS und VA-Ventil unbestr. zu od. Sensor p_VA defekt |
| 0x5D6F | Inbetriebnahme: Sensor p_HA defekt |
| 0x5D70 | Inbetriebnahme: Tankruecklauf zu oder (FS und HA-Ventil unbestromt zu) |
| 0x5D71 | Inbetriebnahme: FS unbestr. zu u. (Ventilblock dicht od. Tankrueckl. zu od. HA unbestr. zu) |
| 0x5D72 | Inbetriebnahme: FS unbestr. zu |
| 0x5D73 | Inbetriebnahme: FS u. VA-Ventil unbestr. zu |
| 0x5D74 | Inbetriebnahme: Schwenkmotor VA fest |
| 0x5D75 | Inbetriebnahme: FS-Drossel oder VA-Ventil haengt offen od. beide DS od. Rueckschl.-ventil links defekt |
| 0x5D76 | Inbetriebnahme: Drucksensoren vertauscht |
| 0x5D77 | Inbetriebnahme: Druckaufbau VA zu langsam oder Kennlinie VA (VBL Problem) od. Sensor pVA defekt |
| 0x5D78 | Inbetriebnahme: VA-Ventil haengt geschlossen |
| 0x5D79 | Inbetriebnahme: Summen Leck VA oder Sensor pVA defekt |
| 0x5D7A | Inbetriebnahme: Kennline VA oder Sensor pVA defekt |
| 0x5D7D | Inbetriebnahme: Schwenkmotor HA fest |
| 0x5D7E | Inbetriebnahme: Sensor pVA oder Sensor pHA defekt |
| 0x5D7F | Inbetriebnahme: HA_Ventil haengt geschlossen |
| 0x5D80 | Inbetriebnahme: Druckaufbau HA zu langsam oder Kennlinie HA (VBL Problem) |
| 0x5D81 | Inbetriebnahme: HA-Ventil haengt offen od. Rueckschl.-ventil links defekt |
| 0x5D82 | Inbetriebnahme: HA-Ventil haengt offen od. Rueckschl.-ventil rechts defekt |
| 0x5D83 | Inbetriebnahme: Dynamikfehler VA/HA |
| 0x5D84 | Inbetriebnahme: Druckaufbau (VA und HA) zu langsam |
| 0x5D85 | Inbetriebnahme: Kennline HA |
| 0x5D8A | Inbetriebnahme: Kennlinienfehler VA |
| 0x5D8B | Inbetriebnahme: Kennlinienfehler HA |
| 0x626C | Konsistenz Querbeschleunigung Can Signal |
| 0x626D | Konsistenz Querbeschleunigung ARS Sensor |
| 0x6271 | Predrive Check: FS und VA-Ventil unbestromt zu oder Sensor P_VA defekt |
| 0x6272 | Predrive Check: FS und HA-Ventil unbestromt zu |
| 0x6273 | Predrive Check: FS Okay, VA- und HA-Ventil bestromt offen |
| 0x6274 | Predrive Check: FS unbestromt zu und VA Okay |
| 0x6275 | Predrive Check: FS unbestromt zu und VA-Ventil offen, HA-Ventil Okay |
| 0x6276 | Predrive Check: VA-Ventil bestromt offen |
| 0x6277 | Predrive Check: FS oder HA oder VA-Ventilstrom zu hoch |
| 0x6278 | Predrive Check: Umlaufdruck temporaer zu hoch (evtl. Oel zu kalt) |
| 0x6279 | Predrive Check: Umlaufdruck dauerhaft zu hoch |
| 0x627A | Predrive Check: Motor in Fahrt gestoppt |
| 0x627B | Predrive Check: Zuschalten nach Reset waehrend der Fahrt |
| 0x6288 | Inbetriebnahme: aQuer Analogsensor defekt |
| 0x6289 | Inbetriebnahme: aQuer Analogsensor Vorzeichenfehler |
| 0x628A | Inbetriebnahme: LL- oder Predrive Fehler verhindert Inbetriebnahme Start |
| 0x628B | Inbetriebnahme: Inbetriebnahme durch Tester abgebrochen |
| 0xD1C7 | PT-CAN Bus Off |
| 0xD1C8 | F-CAN Bus Off |
| 0xD1DD | CAN Beschleunigung Fahrzeug Quer DSC |
| 0xD1DF | CAN Geschwindigkeit Fahrzeug |
| 0xD1E4 | CAN Lenkradwinkel |
| 0xD1E8 | CAN Gradient Lenkradwinkel |
| 0xD1E9 | Fahrgestellnummer |
| 0xD1F1 | CAN Botschaft Geschwindigkeit |
| 0xD1F5 | F-CAN STWA_TOP |
| 0xD1F6 | F-CAN RTR_PO_AVL |
| 0xD1F8 | F-CAN RATE_ANG_VDC_EST |
| 0xD1FD | F-CAN ACLN_ACRO_1 |
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

Dimensions: 82 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x5D4C | 0x0B | - | - | - |
| 0x5D4D | 0x0B | - | - | - |
| 0x5D4E | 0x0B | - | - | - |
| 0x5D4F | 0x0B | - | - | - |
| 0x5D50 | 0x05 | - | - | - |
| 0x5D51 | 0x05 | - | - | - |
| 0x5D52 | 0x05 | - | - | - |
| 0x5D53 | 0x05 | - | - | - |
| 0x5D54 | 0x06 | - | - | - |
| 0x5D55 | 0x06 | - | - | - |
| 0x5D56 | 0x0D | - | - | - |
| 0x5D57 | 0x06 | - | - | - |
| 0x5D5A | 0x01 | - | - | - |
| 0x5D5B | 0x07 | - | - | - |
| 0x5D5C | 0x0E | - | - | - |
| 0x5D5E | 0x09 | - | - | - |
| 0x5D5F | 0x09 | - | - | - |
| 0x5D60 | 0x0A | - | - | - |
| 0x5D61 | 0x0B | - | - | - |
| 0x5D62 | EE_ECU | - | - | - |
| 0x5D64 | 0x0C | - | - | - |
| 0x5D65 | 0x02 | - | - | - |
| 0x5D67 | 0x02 | - | - | - |
| 0x5D69 | 0x0F | - | - | - |
| 0x5D6A | 0x08 | - | - | - |
| 0x5D6B | 0x05 | - | - | - |
| 0x5D6C | INBETR | - | - | - |
| 0x5D6D | INBETR | - | - | - |
| 0x5D6E | INBETR | - | - | - |
| 0x5D6F | INBETR | - | - | - |
| 0x5D70 | INBETR | - | - | - |
| 0x5D71 | INBETR | - | - | - |
| 0x5D72 | INBETR | - | - | - |
| 0x5D73 | INBETR | - | - | - |
| 0x5D74 | INBETR | - | - | - |
| 0x5D75 | INBETR | - | - | - |
| 0x5D76 | INBETR | - | - | - |
| 0x5D77 | INBETR | - | - | - |
| 0x5D78 | INBETR | - | - | - |
| 0x5D79 | INBETR | - | - | - |
| 0x5D7A | INBETR | - | - | - |
| 0x5D7D | INBETR | - | - | - |
| 0x5D7E | INBETR | - | - | - |
| 0x5D7F | INBETR | - | - | - |
| 0x5D80 | INBETR | - | - | - |
| 0x5D81 | INBETR | - | - | - |
| 0x5D82 | INBETR | - | - | - |
| 0x5D83 | INBETR | - | - | - |
| 0x5D84 | INBETR | - | - | - |
| 0x5D85 | INBETR | - | - | - |
| 0x5D8A | INBETR | - | - | - |
| 0x5D8B | INBETR | - | - | - |
| 0x626C | 0x08 | - | - | - |
| 0x626D | 0x08 | - | - | - |
| 0x6271 | PRE_DRIVE | - | - | - |
| 0x6272 | PRE_DRIVE | - | - | - |
| 0x6273 | PRE_DRIVE | - | - | - |
| 0x6274 | PRE_DRIVE | - | - | - |
| 0x6275 | PRE_DRIVE | - | - | - |
| 0x6276 | PRE_DRIVE | - | - | - |
| 0x6277 | PRE_DRIVE | - | - | - |
| 0x6278 | PRE_DRIVE | - | - | - |
| 0x6279 | PRE_DRIVE | - | - | - |
| 0x627A | PRE_DRIVE | - | - | - |
| 0x627B | PRE_DRIVE | - | - | - |
| 0x6288 | INBETR | - | - | - |
| 0x6289 | INBETR | - | - | - |
| 0x628A | INBETR | - | - | - |
| 0x628B | INBETR | - | - | - |
| 0xD1C7 | 0x0B | - | - | - |
| 0xD1C8 | 0x0B | - | - | - |
| 0xD1DD | 0x0B | - | - | - |
| 0xD1DF | 0x0B | - | - | - |
| 0xD1E4 | 0x0B | - | - | - |
| 0xD1E8 | 0x0B | - | - | - |
| 0xD1E9 | 0x0B | - | - | - |
| 0xD1F1 | 0x0B | - | - | - |
| 0xD1F5 | 0x0B | - | - | - |
| 0xD1F6 | 0x0B | - | - | - |
| 0xD1F8 | 0x0B | - | - | - |
| 0xD1FD | 0x0B | - | - | - |
| default | - | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 44 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Drehzahl | 1/min | - | unsigned int | - | 1 | 1 | 0 |
| 0x02 | Aussentemperatur | Grad C | high | signed int | - | 1 | 100 | 0 |
| 0x03 | ECU Temperatur | Grad C | high | signed int | - | 1 | 100 | 0 |
| 0x05 | Sensorversorgungsspannung | mV | high | unsigned int | - | 1 | 1 | 0 |
| 0x06 | korrigierte Sensorspannung | mV | high | unsigned int | - | 1 | 1 | 0 |
| 0x07 | Ist-Druck VA | bar | high | unsigned int | - | 1 | 10 | 0 |
| 0x08 | aQ-Sensor | m/s^2 | high | signed int | - | 1 | 100 | 0 |
| 0x09 | Ist-Strom | mA | high | unsigned int | - | 1 | 1 | 0 |
| 0x0A | Sensorspannung | mV | high | unsigned int | - | 1 | 1 | 0 |
| 0x0B | Spannung KL30 | mV | high | unsigned int | - | 1 | 1 | 0 |
| 0x0C | Codierdatum | @@ | high | unsigned int | - | 1 | 1 | 0 |
| 0x0D | CAN-Sensorspannung | mV | high | unsigned int | - | 1 | 1 | 0 |
| 0x0E | Ist-Druck HA | bar | high | unsigned int | - | 1 | 10 | 0 |
| 0x0F | Bitcodierter Wert | @@ | high | unsigned int | - | 1 | 1 | 0 |
| 0xC0 | Inbetriebnahme Warnung | 0-n | - | 0xC0 | InWa | - | - | - |
| 0x3F | Inbetriebnahme Fehler | 0-n | - | 0x3F | InFh | - | - | - |
| 0x80 | EEProm ECU | 0-n | high | 0x0001 | EEECU_1 | - | - | - |
| 0x81 | EEProm ECU | 0-n | high | 0x0002 | EEECU_2 | - | - | - |
| 0x82 | EEProm ECU | 0-n | high | 0x0004 | EEECU_3 | - | - | - |
| 0x83 | EEProm ECU | 0-n | high | 0x0008 | EEECU_4 | - | - | - |
| 0x84 | EEProm ECU | 0-n | high | 0x0010 | EEECU_5 | - | - | - |
| 0x85 | EEProm ECU | 0-n | high | 0x0020 | EEECU_6 | - | - | - |
| 0x86 | EEProm ECU | 0-n | high | 0x0040 | EEECU_7 | - | - | - |
| 0x87 | EEProm ECU | 0-n | high | 0x0080 | EEECU_8 | - | - | - |
| 0x88 | EEProm ECU | 0-n | high | 0x0100 | EEECU_9 | - | - | - |
| 0x89 | EEProm ECU | 0-n | high | 0x0200 | EEECU_A | - | - | - |
| 0x8A | EEProm ECU | 0-n | high | 0x0400 | EEECU_B | - | - | - |
| 0x8B | EEProm ECU | 0-n | high | 0x0800 | EEECU_C | - | - | - |
| 0x8C | EEProm ECU | 0-n | high | 0x1000 | EEECU_D | - | - | - |
| 0x8D | EEProm ECU | 0-n | high | 0x2000 | EEECU_E | - | - | - |
| 0x8E | EEProm ECU | 0-n | high | 0x4000 | EEECU_F | - | - | - |
| 0x8F | EEProm ECU | 0-n | high | 0x8000 | EEECU_10 | - | - | - |
| 0x90 | Predrive Fehler | 0-n | high | 0x0001 | PRE_DRIVE_1 | - | - | - |
| 0x91 | Predrive Fehler | 0-n | high | 0x0002 | PRE_DRIVE_2 | - | - | - |
| 0x92 | Predrive Fehler | 0-n | high | 0x0004 | PRE_DRIVE_3 | - | - | - |
| 0x93 | Predrive Fehler | 0-n | high | 0x0008 | PRE_DRIVE_4 | - | - | - |
| 0xA0 | Inbetriebnahme Fehler | 0-n | high | 0x0001 | INBETR_1 | - | - | - |
| 0xA1 | Inbetriebnahme Fehler | 0-n | high | 0x0002 | INBETR_2 | - | - | - |
| 0xA2 | Inbetriebnahme Fehler | 0-n | high | 0x0004 | INBETR_3 | - | - | - |
| 0xA3 | Inbetriebnahme Fehler | 0-n | high | 0x0008 | INBETR_4 | - | - | - |
| 0xA4 | Inbetriebnahme Fehler | 0-n | high | 0x0010 | INBETR_5 | - | - | - |
| 0xA5 | Inbetriebnahme Fehler | 0-n | high | 0x0020 | INBETR_6 | - | - | - |
| 0xA6 | Inbetriebnahme Fehler | 0-n | high | 0x0040 | INBETR_7 | - | - | - |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 82 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x5D4C | 0x0101 | 0x0102 | 0x0103 | 0x0104 |
| 0x5D4D | 0x0101 | 0x0102 | 0x0103 | 0x0104 |
| 0x5D4E | 0x0101 | 0x0102 | 0x0103 | 0x0104 |
| 0x5D4F | 0x0101 | 0x0102 | 0x0103 | 0x0104 |
| 0x5D50 | 0x0105 | 0x0106 | 0x0107 | 0x0108 |
| 0x5D51 | 0x0105 | 0x0106 | 0x0107 | 0x0108 |
| 0x5D52 | 0x0105 | 0x0106 | 0x0107 | 0x0108 |
| 0x5D53 | 0x0105 | 0x0106 | 0x0107 | 0x0108 |
| 0x5D54 | 0x01EE | 0x0109 | 0x0110 | 0x0111 |
| 0x5D55 | 0x01EE | 0x0109 | 0x0110 | 0x0111 |
| 0x5D56 | 0x011A | 0x011B | 0x011C | 0x011D |
| 0x5D57 | 0x01EE | 0x0109 | 0x0110 | 0x0111 |
| 0x5D5A | 0x0112 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D5B | 0x01EE | 0x01EE | 0x0113 | 0x0114 |
| 0x5D5C | 0x01EE | 0x01EE | 0x0113 | 0x0114 |
| 0x5D5E | 0x0117 | 0x0118 | 0x0119 | 0x0120 |
| 0x5D5F | 0x0121 | 0x0122 | 0x0123 | 0x0124 |
| 0x5D60 | 0x01EE | 0x0125 | 0x01EE | 0x01EE |
| 0x5D61 | 0x012B | 0x012A | 0x0126 | 0x0127 |
| 0x5D62 | 0x0128 | 0x0129 | 0x0130 | 0x0131 |
| 0x5D64 | 0x013B | 0x0132 | 0x01EE | 0x01EE |
| 0x5D65 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D67 | 0x0133 | 0x01EE | 0x0134 | 0x01EE |
| 0x5D69 | 0x013A | 0x0135 | 0x01EE | 0x0139 |
| 0x5D6A | 0x0152 | 0x0143 | 0x0151 | 0x0150 |
| 0x5D6B | 0x0105 | 0x0106 | 0x010B | 0x010A |
| 0x5D6C | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D6D | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D6E | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D6F | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D70 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D71 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D72 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D73 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D74 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D75 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D76 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D77 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D78 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D79 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D7A | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D7D | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D7E | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D7F | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D80 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D81 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D82 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D83 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D84 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D85 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D8A | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D8B | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x626C | 0x0116 | 0x01EE | 0x01EE | 0x01EE |
| 0x626D | 0x0115 | 0x01EE | 0x01EE | 0x01EE |
| 0x6271 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6272 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6273 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6274 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6275 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6276 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6277 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6278 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6279 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x627A | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x627B | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6288 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x6289 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x628A | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x628B | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0xD1C7 | 0x01EE | 0x0137 | 0x01EE | 0x01EE |
| 0xD1C8 | 0x01EE | 0x0137 | 0x01EE | 0x01EE |
| 0xD1DD | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1DF | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1E4 | 0x0140 | 0x0141 | 0x0134 | 0x0144 |
| 0xD1E8 | 0x01EE | 0x01EE | 0x01EE | 0x0143 |
| 0xD1E9 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1F1 | 0x01EE | 0x0141 | 0x0134 | 0x01EE |
| 0xD1F5 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1F6 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1F8 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1FD | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| default | 0x01EE | 0x01EE | 0x01EE | 0x01EE |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 58 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0101 | KS Ventil |
| 0x0102 | offene Leitung |
| 0x0103 | KS KL31 |
| 0x0104 | KS KL30 |
| 0x0105 | Abriss Sensorground |
| 0x0106 | Abriss Sensorversorgung |
| 0x0107 | Unterspannung Sensorversorgung |
| 0x0108 | Ueberspannung Sensorversorgung |
| 0x0109 | Nullpunkt Lernen Fehler |
| 0x010A | Ueberspannung Sensorsignal |
| 0x010B | Unterspannung Sensorsignal |
| 0x0110 | Sensorparameter fehlen |
| 0x0111 | nicht kalibriert |
| 0x0112 | Lenkwinkel unplausibel |
| 0x0113 | Druck zu hoch |
| 0x0114 | Druck zu niedrig |
| 0x0115 | aQ-Sensor Kons. Error |
| 0x0116 | aQ-CAN Kons. Error |
| 0x0117 | Propventil VA Strommessung |
| 0x0118 | Propventil HA Strommessung |
| 0x0119 | P_VA Endstufe nicht kalibriert |
| 0x011A | Sensorparameter fehlen hinten rechts |
| 0x011B | Sensorparameter fehlen hinten links |
| 0x011C | Sensorparameter fehlen vorne rechts |
| 0x011D | Sensorparameter fehlen vorne links |
| 0x0120 | P_HA Endstufe nicht kalibriert |
| 0x0121 | RV Strommessung |
| 0x0122 | SV Strommessung |
| 0x0123 | RV Endstufe nicht kalibriert |
| 0x0124 | SV Endstufe nicht kalibriert |
| 0x0125 | kein Signal |
| 0x0126 | Unterspannung KL30 &lt; 9V |
| 0x0127 | Ueberspannung KL30 &gt; 17V |
| 0x0128 | CPU Fehler |
| 0x0129 | HW Fehler |
| 0x012A | CAN-Fehler bei Ueberspannung KL30 &gt; 16V |
| 0x012B | CAN-Fehler bei Niedrigspannung KL30 &lt; 10VL |
| 0x0130 | BS Fehler |
| 0x0131 | EEProm Fehler |
| 0x0132 | falscher Codierdatenstand |
| 0x0133 | unplausibles Signal |
| 0x0134 | Init |
| 0x0135 | einzelner Fehler zurueckgesetzt Umweltbed. Bits: 0-3 Status ARS, Bit 4 Prim./Shadow Default, Bit 5 History Default, Bit 6 Prim./Shadow EEP Zellen defekt, Bit 7 History EEP Zellen defekt, Bit 8-11 Fahrzeuggeschw., Bit 12-15 a_quer |
| 0x0136 | Inbetriebnahme Fehler |
| 0x0137 | Can Bus Off |
| 0x0139 | CC-Meldung ohne FSP Umweltbed. Bits: 0-3 Status ARS, Bit 4 Prim./Shadow Default, Bit 5 History Default, Bit 6 Prim./Shadow EEP Zellen defekt, Bit 7 History EEP Zellen defekt, Bit 8-11 Fahrzeuggeschw., Bit 12-15 a_quer |
| 0x013A | unplausible Daten EEProm defekt Umweltbed. Bits: 0-3 Status ARS, Bit 4 Prim./Shadow Default, Bit 5 History Default, Bit 6 Prim./Shadow EEP Zellen defekt, Bit 7 History EEP Zellen defekt, Bit 8-11 Fahrzeuggeschw., Bit 12-15 a_quer |
| 0x013B | unplausible Daten EEProm |
| 0x0140 | Wert ungueltig |
| 0x0141 | Timeout |
| 0x0142 | Msg error |
| 0x0143 | Gradientenfehler |
| 0x0144 | Verifikation |
| 0x0150 | ARD Sollmoment überschritten |
| 0x0151 | Bereich überschritten |
| 0x0152 | Höhenstands Konsistenz Fehler |
| 0x01EE | im Steuergerät nicht verwendet |
| 0x00XY | mehrere Symptome oder Fehlerursache unbekannt |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 82 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5D4C | Sicherheitsventil |
| 0x5D4D | Richtungsventil |
| 0x5D4E | Proportionalventil VA |
| 0x5D4F | Proportionalventil HA |
| 0x5D50 | Versorgung Drucksensor VA |
| 0x5D51 | Versorgung Drucksensor HA |
| 0x5D52 | Versorgung Schaltstellungssensor |
| 0x5D53 | Versorgung Querbeschleunigungssensor |
| 0x5D54 | Lernen Drucksensor VA |
| 0x5D55 | Lernen Drucksensor HA |
| 0x5D56 | Lernen Hoehenstandssensor |
| 0x5D57 | Lernen Querbeschleunigungssensor |
| 0x5D5A | Konsistenz LWS |
| 0x5D5B | Konsistenz Druck VA |
| 0x5D5C | Konsistenz Druck HA |
| 0x5D5E | Konsistenz Strommessung Propventile |
| 0x5D5F | Konsistenz Strommessung Schaltventile |
| 0x5D60 | Oelstandssensor |
| 0x5D61 | KL30 ARS-SG |
| 0x5D62 | ECU intern |
| 0x5D64 | Codierdatenfehler |
| 0x5D65 | Status Richtungsventil |
| 0x5D67 | Konsistenz Fahrgestellnummer |
| 0x5D69 | Fehlerspeicher defekt |
| 0x5D6A | VDM Wankratenüberwachung |
| 0x5D6B | Oelstandssensorelektronik |
| 0x5D6C | Inbetriebnahme: RV bestromt |
| 0x5D6D | Inbetriebnahme: RV unbestromt |
| 0x5D6E | Inbetriebnahme: FS und VA-Ventil unbestr. zu od. Sensor p_VA defekt |
| 0x5D6F | Inbetriebnahme: Sensor p_HA defekt |
| 0x5D70 | Inbetriebnahme: Tankruecklauf zu oder (FS und HA-Ventil unbestromt zu) |
| 0x5D71 | Inbetriebnahme: FS unbestr. zu u. (Ventilblock dicht od. Tankrueckl. zu od. HA unbestr. zu) |
| 0x5D72 | Inbetriebnahme: FS unbestr. zu |
| 0x5D73 | Inbetriebnahme: FS u. VA-Ventil unbestr. zu |
| 0x5D74 | Inbetriebnahme: Schwenkmotor VA fest |
| 0x5D75 | Inbetriebnahme: FS-Drossel oder VA-Ventil haengt offen od. beide DS od. Rueckschl.-ventil links defekt |
| 0x5D76 | Inbetriebnahme: Drucksensoren vertauscht |
| 0x5D77 | Inbetriebnahme: Druckaufbau VA zu langsam oder Kennlinie VA (VBL Problem) od. Sensor pVA defekt |
| 0x5D78 | Inbetriebnahme: VA-Ventil haengt geschlossen |
| 0x5D79 | Inbetriebnahme: Summen Leck VA oder Sensor pVA defekt |
| 0x5D7A | Inbetriebnahme: Kennline VA oder Sensor pVA defekt |
| 0x5D7D | Inbetriebnahme: Schwenkmotor HA fest |
| 0x5D7E | Inbetriebnahme: Sensor pVA oder Sensor pHA defekt |
| 0x5D7F | Inbetriebnahme: HA_Ventil haengt geschlossen |
| 0x5D80 | Inbetriebnahme: Druckaufbau HA zu langsam oder Kennlinie HA (VBL Problem) |
| 0x5D81 | Inbetriebnahme: HA-Ventil haengt offen od. Rueckschl.-ventil links defekt |
| 0x5D82 | Inbetriebnahme: HA-Ventil haengt offen od. Rueckschl.-ventil rechts defekt |
| 0x5D83 | Inbetriebnahme: Dynamikfehler VA/HA |
| 0x5D84 | Inbetriebnahme: Druckaufbau (VA und HA) zu langsam |
| 0x5D85 | Inbetriebnahme: Kennline HA |
| 0x5D8A | Inbetriebnahme: Kennlinienfehler VA |
| 0x5D8B | Inbetriebnahme: Kennlinienfehler HA |
| 0x626C | Konsistenz Querbeschleunigung Can Signal |
| 0x626D | Konsistenz Querbeschleunigung ARS Sensor |
| 0x6271 | Predrive Check: FS und VA-Ventil unbestromt zu oder Sensor P_VA defekt |
| 0x6272 | Predrive Check: FS und HA-Ventil unbestromt zu |
| 0x6273 | Predrive Check: FS Okay, VA- und HA-Ventil bestromt offen |
| 0x6274 | Predrive Check: FS unbestromt zu und VA Okay |
| 0x6275 | Predrive Check: FS unbestromt zu und VA-Ventil offen, HA-Ventil Okay |
| 0x6276 | Predrive Check: VA-Ventil bestromt offen |
| 0x6277 | Predrive Check: FS oder HA oder VA-Ventilstrom zu hoch |
| 0x6278 | Predrive Check: Umlaufdruck temporaer zu hoch (evtl. Oel zu kalt) |
| 0x6279 | Predrive Check: Umlaufdruck dauerhaft zu hoch |
| 0x627A | Predrive Check: Motor in Fahrt gestoppt |
| 0x627B | Predrive Check: Zuschalten nach Reset waehrend der Fahrt |
| 0x6288 | Inbetriebnahme: aQuer Analogsensor defekt |
| 0x6289 | Inbetriebnahme: aQuer Analogsensor Vorzeichenfehler |
| 0x628A | Inbetriebnahme: LL- oder Predrive Fehler verhindert Inbetriebnahme Start |
| 0x628B | Inbetriebnahme: Inbetriebnahme durch Tester abgebrochen |
| 0xD1C7 | PT-CAN Bus Off |
| 0xD1C8 | F-CAN Bus Off |
| 0xD1DD | CAN Beschleunigung Fahrzeug Quer DSC |
| 0xD1DF | CAN Geschwindigkeit Fahrzeug |
| 0xD1E4 | CAN Lenkradwinkel |
| 0xD1E8 | CAN Gradient Lenkradwinkel |
| 0xD1E9 | Fahrgestellnummer |
| 0xD1F1 | CAN Botschaft Geschwindigkeit |
| 0xD1F5 | F-CAN STWA_TOP |
| 0xD1F6 | F-CAN RTR_PO_AVL |
| 0xD1F8 | F-CAN RATE_ANG_VDC_EST |
| 0xD1FD | F-CAN ACLN_ACRO_1 |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

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

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 82 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x5D4C | 0x0B | - | - | - |
| 0x5D4D | 0x0B | - | - | - |
| 0x5D4E | 0x0B | - | - | - |
| 0x5D4F | 0x0B | - | - | - |
| 0x5D50 | 0x05 | - | - | - |
| 0x5D51 | 0x05 | - | - | - |
| 0x5D52 | 0x05 | - | - | - |
| 0x5D53 | 0x05 | - | - | - |
| 0x5D54 | 0x06 | - | - | - |
| 0x5D55 | 0x06 | - | - | - |
| 0x5D56 | 0x0D | - | - | - |
| 0x5D57 | 0x06 | - | - | - |
| 0x5D5A | 0x01 | - | - | - |
| 0x5D5B | 0x07 | - | - | - |
| 0x5D5C | 0x0E | - | - | - |
| 0x5D5E | 0x09 | - | - | - |
| 0x5D5F | 0x09 | - | - | - |
| 0x5D60 | 0x0A | - | - | - |
| 0x5D61 | 0x0B | - | - | - |
| 0x5D62 | EE_ECU | - | - | - |
| 0x5D64 | 0x0C | - | - | - |
| 0x5D65 | 0x02 | - | - | - |
| 0x5D67 | 0x02 | - | - | - |
| 0x5D69 | 0x0F | - | - | - |
| 0x5D6A | 0x08 | - | - | - |
| 0x5D6B | 0x05 | - | - | - |
| 0x5D6C | INBETR | - | - | - |
| 0x5D6D | INBETR | - | - | - |
| 0x5D6E | INBETR | - | - | - |
| 0x5D6F | INBETR | - | - | - |
| 0x5D70 | INBETR | - | - | - |
| 0x5D71 | INBETR | - | - | - |
| 0x5D72 | INBETR | - | - | - |
| 0x5D73 | INBETR | - | - | - |
| 0x5D74 | INBETR | - | - | - |
| 0x5D75 | INBETR | - | - | - |
| 0x5D76 | INBETR | - | - | - |
| 0x5D77 | INBETR | - | - | - |
| 0x5D78 | INBETR | - | - | - |
| 0x5D79 | INBETR | - | - | - |
| 0x5D7A | INBETR | - | - | - |
| 0x5D7D | INBETR | - | - | - |
| 0x5D7E | INBETR | - | - | - |
| 0x5D7F | INBETR | - | - | - |
| 0x5D80 | INBETR | - | - | - |
| 0x5D81 | INBETR | - | - | - |
| 0x5D82 | INBETR | - | - | - |
| 0x5D83 | INBETR | - | - | - |
| 0x5D84 | INBETR | - | - | - |
| 0x5D85 | INBETR | - | - | - |
| 0x5D8A | INBETR | - | - | - |
| 0x5D8B | INBETR | - | - | - |
| 0x626C | 0x08 | - | - | - |
| 0x626D | 0x08 | - | - | - |
| 0x6271 | PRE_DRIVE | - | - | - |
| 0x6272 | PRE_DRIVE | - | - | - |
| 0x6273 | PRE_DRIVE | - | - | - |
| 0x6274 | PRE_DRIVE | - | - | - |
| 0x6275 | PRE_DRIVE | - | - | - |
| 0x6276 | PRE_DRIVE | - | - | - |
| 0x6277 | PRE_DRIVE | - | - | - |
| 0x6278 | PRE_DRIVE | - | - | - |
| 0x6279 | PRE_DRIVE | - | - | - |
| 0x627A | PRE_DRIVE | - | - | - |
| 0x627B | PRE_DRIVE | - | - | - |
| 0x6288 | INBETR | - | - | - |
| 0x6289 | INBETR | - | - | - |
| 0x628A | INBETR | - | - | - |
| 0x628B | INBETR | - | - | - |
| 0xD1C7 | 0x0B | - | - | - |
| 0xD1C8 | 0x0B | - | - | - |
| 0xD1DD | 0x0B | - | - | - |
| 0xD1DF | 0x0B | - | - | - |
| 0xD1E4 | 0x0B | - | - | - |
| 0xD1E8 | 0x0B | - | - | - |
| 0xD1E9 | 0x0B | - | - | - |
| 0xD1F1 | 0x0B | - | - | - |
| 0xD1F5 | 0x0B | - | - | - |
| 0xD1F6 | 0x0B | - | - | - |
| 0xD1F8 | 0x0B | - | - | - |
| 0xD1FD | 0x0B | - | - | - |
| default | - | - | - | - |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 44 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Drehzahl | 1/min | - | unsigned int | - | 1 | 1 | 0 |
| 0x02 | Aussentemperatur | Grad C | high | signed int | - | 1 | 100 | 0 |
| 0x03 | ECU Temperatur | Grad C | high | signed int | - | 1 | 100 | 0 |
| 0x05 | Sensorversorgungsspannung | mV | high | unsigned int | - | 1 | 1 | 0 |
| 0x06 | korrigierte Sensorspannung | mV | high | unsigned int | - | 1 | 1 | 0 |
| 0x07 | Ist-Druck VA | bar | high | unsigned int | - | 1 | 10 | 0 |
| 0x08 | aQ-Sensor | m/s^2 | high | signed int | - | 1 | 100 | 0 |
| 0x09 | Ist-Strom | mA | high | unsigned int | - | 1 | 1 | 0 |
| 0x0A | Sensorspannung | mV | high | unsigned int | - | 1 | 1 | 0 |
| 0x0B | Spannung KL30 | mV | high | unsigned int | - | 1 | 1 | 0 |
| 0x0C | Codierdatum | @@ | high | unsigned int | - | 1 | 1 | 0 |
| 0x0D | CAN-Sensorspannung | mV | high | unsigned int | - | 1 | 1 | 0 |
| 0x0E | Ist-Druck HA | bar | high | unsigned int | - | 1 | 10 | 0 |
| 0x0F | Bitcodierter Wert | @@ | high | unsigned int | - | 1 | 1 | 0 |
| 0xC0 | Inbetriebnahme Warnung | 0-n | - | 0xC0 | InWa | - | - | - |
| 0x3F | Inbetriebnahme Fehler | 0-n | - | 0x3F | InFh | - | - | - |
| 0x80 | EEProm ECU | 0-n | high | 0x0001 | EEECU_1 | - | - | - |
| 0x81 | EEProm ECU | 0-n | high | 0x0002 | EEECU_2 | - | - | - |
| 0x82 | EEProm ECU | 0-n | high | 0x0004 | EEECU_3 | - | - | - |
| 0x83 | EEProm ECU | 0-n | high | 0x0008 | EEECU_4 | - | - | - |
| 0x84 | EEProm ECU | 0-n | high | 0x0010 | EEECU_5 | - | - | - |
| 0x85 | EEProm ECU | 0-n | high | 0x0020 | EEECU_6 | - | - | - |
| 0x86 | EEProm ECU | 0-n | high | 0x0040 | EEECU_7 | - | - | - |
| 0x87 | EEProm ECU | 0-n | high | 0x0080 | EEECU_8 | - | - | - |
| 0x88 | EEProm ECU | 0-n | high | 0x0100 | EEECU_9 | - | - | - |
| 0x89 | EEProm ECU | 0-n | high | 0x0200 | EEECU_A | - | - | - |
| 0x8A | EEProm ECU | 0-n | high | 0x0400 | EEECU_B | - | - | - |
| 0x8B | EEProm ECU | 0-n | high | 0x0800 | EEECU_C | - | - | - |
| 0x8C | EEProm ECU | 0-n | high | 0x1000 | EEECU_D | - | - | - |
| 0x8D | EEProm ECU | 0-n | high | 0x2000 | EEECU_E | - | - | - |
| 0x8E | EEProm ECU | 0-n | high | 0x4000 | EEECU_F | - | - | - |
| 0x8F | EEProm ECU | 0-n | high | 0x8000 | EEECU_10 | - | - | - |
| 0x90 | Predrive Fehler | 0-n | high | 0x0001 | PRE_DRIVE_1 | - | - | - |
| 0x91 | Predrive Fehler | 0-n | high | 0x0002 | PRE_DRIVE_2 | - | - | - |
| 0x92 | Predrive Fehler | 0-n | high | 0x0004 | PRE_DRIVE_3 | - | - | - |
| 0x93 | Predrive Fehler | 0-n | high | 0x0008 | PRE_DRIVE_4 | - | - | - |
| 0xA0 | Inbetriebnahme Fehler | 0-n | high | 0x0001 | INBETR_1 | - | - | - |
| 0xA1 | Inbetriebnahme Fehler | 0-n | high | 0x0002 | INBETR_2 | - | - | - |
| 0xA2 | Inbetriebnahme Fehler | 0-n | high | 0x0004 | INBETR_3 | - | - | - |
| 0xA3 | Inbetriebnahme Fehler | 0-n | high | 0x0008 | INBETR_4 | - | - | - |
| 0xA4 | Inbetriebnahme Fehler | 0-n | high | 0x0010 | INBETR_5 | - | - | - |
| 0xA5 | Inbetriebnahme Fehler | 0-n | high | 0x0020 | INBETR_6 | - | - | - |
| 0xA6 | Inbetriebnahme Fehler | 0-n | high | 0x0040 | INBETR_7 | - | - | - |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-harttyp"></a>
### HARTTYP

Dimensions: 82 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x5D4C | 0x0101 | 0x0102 | 0x0103 | 0x0104 |
| 0x5D4D | 0x0101 | 0x0102 | 0x0103 | 0x0104 |
| 0x5D4E | 0x0101 | 0x0102 | 0x0103 | 0x0104 |
| 0x5D4F | 0x0101 | 0x0102 | 0x0103 | 0x0104 |
| 0x5D50 | 0x0105 | 0x0106 | 0x0107 | 0x0108 |
| 0x5D51 | 0x0105 | 0x0106 | 0x0107 | 0x0108 |
| 0x5D52 | 0x0105 | 0x0106 | 0x0107 | 0x0108 |
| 0x5D53 | 0x0105 | 0x0106 | 0x0107 | 0x0108 |
| 0x5D54 | 0x01EE | 0x0109 | 0x0110 | 0x0111 |
| 0x5D55 | 0x01EE | 0x0109 | 0x0110 | 0x0111 |
| 0x5D56 | 0x011A | 0x011B | 0x011C | 0x011D |
| 0x5D57 | 0x01EE | 0x0109 | 0x0110 | 0x0111 |
| 0x5D5A | 0x0112 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D5B | 0x01EE | 0x01EE | 0x0113 | 0x0114 |
| 0x5D5C | 0x01EE | 0x01EE | 0x0113 | 0x0114 |
| 0x5D5E | 0x0117 | 0x0118 | 0x0119 | 0x0120 |
| 0x5D5F | 0x0121 | 0x0122 | 0x0123 | 0x0124 |
| 0x5D60 | 0x01EE | 0x0125 | 0x01EE | 0x01EE |
| 0x5D61 | 0x012B | 0x012A | 0x0126 | 0x0127 |
| 0x5D62 | 0x0128 | 0x0129 | 0x0130 | 0x0131 |
| 0x5D64 | 0x013B | 0x0132 | 0x01EE | 0x01EE |
| 0x5D65 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D67 | 0x0133 | 0x01EE | 0x0134 | 0x01EE |
| 0x5D69 | 0x013A | 0x0135 | 0x01EE | 0x0139 |
| 0x5D6A | 0x0152 | 0x0143 | 0x0151 | 0x0150 |
| 0x5D6B | 0x0105 | 0x0106 | 0x010B | 0x010A |
| 0x5D6C | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D6D | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D6E | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D6F | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D70 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D71 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D72 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D73 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D74 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D75 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D76 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D77 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D78 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D79 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D7A | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D7D | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D7E | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D7F | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D80 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D81 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D82 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D83 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D84 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D85 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D8A | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x5D8B | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x626C | 0x0116 | 0x01EE | 0x01EE | 0x01EE |
| 0x626D | 0x0115 | 0x01EE | 0x01EE | 0x01EE |
| 0x6271 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6272 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6273 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6274 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6275 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6276 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6277 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6278 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6279 | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x627A | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x627B | 0x0133 | 0x01EE | 0x01EE | 0x01EE |
| 0x6288 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x6289 | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x628A | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0x628B | 0x0136 | 0x01EE | 0x01EE | 0x01EE |
| 0xD1C7 | 0x01EE | 0x0137 | 0x01EE | 0x01EE |
| 0xD1C8 | 0x01EE | 0x0137 | 0x01EE | 0x01EE |
| 0xD1DD | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1DF | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1E4 | 0x0140 | 0x0141 | 0x0134 | 0x0144 |
| 0xD1E8 | 0x01EE | 0x01EE | 0x01EE | 0x0143 |
| 0xD1E9 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1F1 | 0x01EE | 0x0141 | 0x0134 | 0x01EE |
| 0xD1F5 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1F6 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1F8 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xD1FD | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| default | 0x01EE | 0x01EE | 0x01EE | 0x01EE |

<a id="table-harttexteindividuell"></a>
### HARTTEXTEINDIVIDUELL

Dimensions: 58 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0101 | KS Ventil |
| 0x0102 | offene Leitung |
| 0x0103 | KS KL31 |
| 0x0104 | KS KL30 |
| 0x0105 | Abriss Sensorground |
| 0x0106 | Abriss Sensorversorgung |
| 0x0107 | Unterspannung Sensorversorgung |
| 0x0108 | Ueberspannung Sensorversorgung |
| 0x0109 | Nullpunkt Lernen Fehler |
| 0x010A | Ueberspannung Sensorsignal |
| 0x010B | Unterspannung Sensorsignal |
| 0x0110 | Sensorparameter fehlen |
| 0x0111 | nicht kalibriert |
| 0x0112 | Lenkwinkel unplausibel |
| 0x0113 | Druck zu hoch |
| 0x0114 | Druck zu niedrig |
| 0x0115 | aQ-Sensor Kons. Error |
| 0x0116 | aQ-CAN Kons. Error |
| 0x0117 | Propventil VA Strommessung |
| 0x0118 | Propventil HA Strommessung |
| 0x0119 | P_VA Endstufe nicht kalibriert |
| 0x011A | Sensorparameter fehlen hinten rechts |
| 0x011B | Sensorparameter fehlen hinten links |
| 0x011C | Sensorparameter fehlen vorne rechts |
| 0x011D | Sensorparameter fehlen vorne links |
| 0x0120 | P_HA Endstufe nicht kalibriert |
| 0x0121 | RV Strommessung |
| 0x0122 | SV Strommessung |
| 0x0123 | RV Endstufe nicht kalibriert |
| 0x0124 | SV Endstufe nicht kalibriert |
| 0x0125 | kein Signal |
| 0x0126 | Unterspannung KL30 &lt; 9V |
| 0x0127 | Ueberspannung KL30 &gt; 17V |
| 0x0128 | CPU Fehler |
| 0x0129 | HW Fehler |
| 0x012A | CAN-Fehler bei Ueberspannung &gt; 16V |
| 0x012B | CAN-Fehler bei Niedrigspannung &lt; 10V |
| 0x0130 | BS Fehler |
| 0x0131 | EEProm Fehler |
| 0x0132 | falscher Codierdatenstand |
| 0x0133 | unplausibles Signal |
| 0x0134 | Init |
| 0x0135 | einzelner Fehler zurueckgesetzt Umweltbed. Bits: 0-3 Status ARS, Bit 4 Prim./Shadow Default, Bit 5 History Default, Bit 6 Prim./Shadow EEP Zellen defekt, Bit 7 History EEP Zellen defekt, Bit 8-11 Fahrzeuggeschw., Bit 12-15 a_quer |
| 0x0136 | Inbetriebnahme Fehler |
| 0x0137 | Can Bus Off |
| 0x0139 | CC-Meldung ohne FSP Umweltbed. Bits: 0-3 Status ARS, Bit 4 Prim./Shadow Default, Bit 5 History Default, Bit 6 Prim./Shadow EEP Zellen defekt, Bit 7 History EEP Zellen defekt, Bit 8-11 Fahrzeuggeschw., Bit 12-15 a_quer |
| 0x013A | unplausible Daten EEProm defekt Umweltbed. Bits: 0-3 Status ARS, Bit 4 Prim./Shadow Default, Bit 5 History Default, Bit 6 Prim./Shadow EEP Zellen defekt, Bit 7 History EEP Zellen defekt, Bit 8-11 Fahrzeuggeschw., Bit 12-15 a_quer |
| 0x013B | unplausible Daten EEProm |
| 0x0140 | Wert ungueltig |
| 0x0141 | Timeout |
| 0x0142 | Msg error |
| 0x0143 | Gradientenfehler |
| 0x0144 | Verifikation |
| 0x0150 | ARD Sollmoment überschritten |
| 0x0151 | Bereich überschritten |
| 0x0152 | Höhenstands Konsistenz Fehler |
| 0x01EE | im Steuergerät nicht verwendet |
| 0x00XY | mehrere Symptome oder Fehlerursache unbekannt |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 24 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x7D5A | Konsistenz LWS |
| 0x7D62 | ECU intern |
| 0x7D63 | ECU intern Software |
| 0x7D69 | Fehlerspeicher defekt |
| 0x826C | Konsistenz Querbeschleunigung Can Signal |
| 0xF1DD | CAN Beschleunigung Fahrzeug Quer DSC |
| 0xF1DE | CAN Winkelgeschwindigkeit Gier DSC |
| 0xF1E0 | CAN Aussentemperatur |
| 0xF1E1 | CAN Temperatur Motor |
| 0xF1E2 | CAN Status Klemme 15 |
| 0xF1E3 | CAN Status Klemme 50 Zuendschlossstellung Anlasser |
| 0xF1E4 | CAN Lenkradwinkel |
| 0xF1E5 | CAN Drehzahl Motor |
| 0xF1EB | CAN Kilometerstand |
| 0xF1F2 | CAN Botschaft Klemmenstatus |
| 0xF1F5 | F-CAN STWA_TOP |
| 0xF1F6 | F-CAN RTR_PO_AVL |
| 0xF1F8 | F-CAN RATE_ANG_VDC_EST |
| 0xF1F9 | F-CAN HGLV_FLH |
| 0xF1FA | F-CAN HGLV_FRH |
| 0xF1FB | F-CAN HGLV_RLH |
| 0xF1FC | F-CAN HGLV_RRH |
| 0xF1FD | F-CAN ACLN_ACRO_1 |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

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

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 24 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x7D5A | 0x01 | - | - | - |
| 0x7D62 | 0x03 | - | - | - |
| 0x7D63 | 0x10 | - | - | - |
| 0x7D69 | 0x0F | - | - | - |
| 0x826C | 0x08 | - | - | - |
| 0xF1DD | 0x0B | - | - | - |
| 0xF1DE | 0x0B | - | - | - |
| 0xF1E0 | 0x0B | - | - | - |
| 0xF1E1 | 0x0B | - | - | - |
| 0xF1E2 | 0x0B | - | - | - |
| 0xF1E3 | 0x0B | - | - | - |
| 0xF1E4 | 0x0B | - | - | - |
| 0xF1E5 | 0x0B | - | - | - |
| 0xF1EB | 0x0B | - | - | - |
| 0xF1F2 | 0x0B | - | - | - |
| 0xF1F5 | 0x0B | - | - | - |
| 0xF1F6 | 0x0B | - | - | - |
| 0xF1F8 | 0x0B | - | - | - |
| 0xF1F9 | 0x0B | - | - | - |
| 0xF1FA | 0x0B | - | - | - |
| 0xF1FB | 0x0B | - | - | - |
| 0xF1FC | 0x0B | - | - | - |
| 0xF1FD | 0x0B | - | - | - |
| default | - | - | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Drehzahl | 1/min | - | unsigned int | - | 1 | 1 | 0 |
| 0x03 | ECU Temperatur | Grad C | high | signed int | - | 1 | 100 | 0 |
| 0x08 | aQ-Sensor | m/s^2 | high | signed int | - | 1 | 100 | 0 |
| 0x0B | Spannung KL30 | mV | high | unsigned int | - | 1 | 1 | 0 |
| 0x0F | Bitcodierter Wert | @@ | high | unsigned int | - | 1 | 1 | 0 |
| 0x10 | Exception Code | @@ | high | unsigned int | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iarttyp"></a>
### IARTTYP

Dimensions: 24 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x7D5A | 0x0112 | 0x01EE | 0x01EE | 0x01EE |
| 0x7D62 | 0x0128 | 0x0129 | 0x0130 | 0x0131 |
| 0x7D63 | 0x01EE | 0x01EE | 0x01EE | 0x012A |
| 0x7D69 | 0x013A | 0x0135 | 0x01EE | 0x01EE |
| 0x826C | 0x0116 | 0x01EE | 0x01EE | 0x01EE |
| 0xF1DD | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1DE | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1E0 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1E1 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1E2 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1E3 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1E4 | 0x0140 | 0x0141 | 0x0134 | 0x0144 |
| 0xF1E5 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1EB | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1F2 | 0x01EE | 0x0141 | 0x0134 | 0x01EE |
| 0xF1F5 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1F6 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1F8 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1F9 | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1FA | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1FB | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1FC | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| 0xF1FD | 0x0140 | 0x0141 | 0x0134 | 0x01EE |
| default | 0x01EE | 0x01EE | 0x01EE | 0x01EE |

<a id="table-iarttexteindividuell"></a>
### IARTTEXTEINDIVIDUELL

Dimensions: 16 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0112 | Lenkwinkel unplausibel |
| 0x0116 | aQ-CAN Kons. Error |
| 0x0128 | CPU Fehler |
| 0x0129 | HW Fehler |
| 0x012A | Exception aufgetreten |
| 0x0130 | BS Fehler |
| 0x0131 | EEProm Fehler |
| 0x0134 | Init |
| 0x0135 | einzelner Fehler zurueckgesetzt Umweltbed. Bits: 0-3 Status ARS, Bit 4 Prim./Shadow Default, Bit 5 History Default, Bit 6 Prim./Shadow EEP Zellen defekt, Bit 7 History EEP Zellen defekt, Bit 8-11 Fahrzeuggeschw., Bit 12-15 a_quer |
| 0x013A | unplausible Daten EEProm defekt Umweltbed. Bits: 0-3 Status ARS, Bit 4 Prim./Shadow Default, Bit 5 History Default, Bit 6 Prim./Shadow EEP Zellen defekt, Bit 7 History EEP Zellen defekt, Bit 8-11 Fahrzeuggeschw., Bit 12-15 a_quer |
| 0x0140 | Wert ungueltig |
| 0x0141 | Timeout |
| 0x0142 | Msg error |
| 0x0144 | Verifikation |
| 0x01EE | im Steuergerät nicht verwendet |
| 0x00XY | mehrere Symptome oder Fehlerursache unbekannt |

<a id="table-bus-typen"></a>
### BUS_TYPEN

Dimensions: 7 rows × 2 columns

| BUS_NR | BUS_TEXT |
| --- | --- |
| 0x00 | PT-CAN |
| 0x01 | I/K-Bus |
| 0x02 | K-CAN System |
| 0x03 | K-CAN Peripherie |
| 0x04 | SI-Bus |
| 0x05 | MOST-Bus |
| 0xFF | unbekannter Bus |

<a id="table-digital"></a>
### DIGITAL

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0xC0 | 0x3F |

<a id="table-ee-ecu"></a>
### EE_ECU

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x80 | 0x81 | 0x82 | 0x83 | 0x84 | 0x85 | 0x86 | 0x87 | 0x88 | 0x89 | 0x8A | 0x8B | 0x8C | 0x8D | 0x8E | 0x8F |

<a id="table-eeecu-10"></a>
### EEECU_10

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x8000 | FPU Check sys error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-f"></a>
### EEECU_F

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x4000 | ALU Check sys error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-e"></a>
### EEECU_E

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x2000 | RAM Check sys error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-d"></a>
### EEECU_D

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x1000 | ROM Check sys error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-c"></a>
### EEECU_C

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0800 | KL30 Inkonsistenz |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-b"></a>
### EEECU_B

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0400 | Shutdown Timeout error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-a"></a>
### EEECU_A

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0200 | Ext. Watchdog sys error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-9"></a>
### EEECU_9

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0100 | VCCL 2V6 sys error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-8"></a>
### EEECU_8

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0080 | Taskcheck sys error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-7"></a>
### EEECU_7

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0040 | Stack Check sys error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-6"></a>
### EEECU_6

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0020 | Tasktime sys error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-5"></a>
### EEECU_5

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0010 | BMW Data Tab error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-4"></a>
### EEECU_4

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0008 | Temic Data Tab error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-3"></a>
### EEECU_3

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0004 | LW Para Tab error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-2"></a>
### EEECU_2

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0002 | Sensorik Tab error |
| 0xFFFF | unbekannter Fehler |

<a id="table-eeecu-1"></a>
### EEECU_1

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0001 | Aktor Tab Error |
| 0xFFFF | unbekannter Fehler |

<a id="table-inwa"></a>
### INWA

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | keine Warnung |
| 0x40 | Luft im VA-System |
| 0x80 | Dynamikproblem VA Luft |
| 0xC0 | Dynamikproblem HA/VA Luft |
| 0xFF | unbekannte Warnung |

<a id="table-infh"></a>
### INFH

Dimensions: 38 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | RV bestromt |
| 0x02 | RV unbestromt |
| 0x03 | FS und VA-Ventil unbestromt zu oder Sensor p_VA defekt |
| 0x04 | Sensor p_HA defekt |
| 0x05 | Tankruecklauf zu oder (FS und HA-Ventil unbestromt zu) |
| 0x06 | FS unbestromt zu und (Ventilblock dicht od. Tankrueckl. zu od. HA unbestr. zu) |
| 0x07 | FS unbestromt zu |
| 0x08 | FS u. VA-Ventil unbestromt zu |
| 0x09 | Schwenkmotor VA fest |
| 0x0A | FS-Ventil od. FS-Drossel oder VA-Ventil haengt offen od. beide DS od. Rueckschl.-ventil links defekt |
| 0x0B | Drucksensoren vertauscht |
| 0x0C | Summen Leck VA oder Kennlinie VA pVA(l) (VBL Problem) od. Sensor pVA defekt |
| 0x0D | VA-Ventil haengt geschlossen |
| 0x0E | Druckaufbau_VA zu langsam oder Sensor pVA defekt |
| 0x0F | Kennline VA oder Sensor pVA defekt |
| 0x10 | frei |
| 0x11 | frei |
| 0x12 | Schwenkmotor HA fest |
| 0x13 | Sensor pVA oder Sensor pHA defekt |
| 0x14 | HA_Ventil haengt geschlossen |
| 0x15 | Druckaufbau_HA zu langsam oder Kennlinie HA pHA(l) (VBL Problem) |
| 0x16 | HA-Ventil haengt offen od. Rueckschl.-ventil links defekt |
| 0x17 | HA-Ventil haengt offen od. Rueckschl.-ventil rechts defekt |
| 0x18 | Dynamikfehler HA/VA |
| 0x19 | Druckaufbau (VA und HA) zu langsam |
| 0x1A | Kennline HA |
| 0x1B | frei |
| 0x1C | frei |
| 0x1D | frei |
| 0x1E | frei |
| 0x1F | Kennlinienfehler VA |
| 0x20 | Kennlinienfehler HA |
| 0x3C | aQuer Analogsensor defekt |
| 0x3D | aQuer Analogsensor Vorzeichenfehler |
| 0x3E | LL Fehler oder Predrive Fehler verhindert Inbetriebnahme starten |
| 0x3F | Inbetriebnahme abgebrochen |
| 0xFF | unbekannter Fehler |

<a id="table-infh-erw"></a>
### INFH_ERW

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | keine Zusatzinfo bei Inbetriebnahme |
| 0x01 | Zusatzinfo: Motordrehzahl oberhalb Schwelle |
| 0x02 | Zusatzinfo: Motordrehzahl unterhalb Schwelle |
| 0x08 | Zusatzinfo: Plausibilitaet |
| 0xFF | unbekannte Zusatzinfo bei Inbetriebnahme |

<a id="table-statkl15"></a>
### STATKL15

Dimensions: 4 rows × 2 columns

| KL15NR | KL15TEXT |
| --- | --- |
| 0x00 | Klemme 15 AUS |
| 0x01 | Klemme 15 EIN |
| 0x03 | Signal ungueltig |
| 0x?? | unbekannt |

<a id="table-statkl50"></a>
### STATKL50

Dimensions: 4 rows × 2 columns

| KL50NR | KL50TEXT |
| --- | --- |
| 0x00 | Klemme 50 AUS |
| 0x01 | Klemme 50 EIN |
| 0x03 | Signal ungueltig |
| 0x?? | unbekannt |

<a id="table-statlenkwinkf"></a>
### STATLENKWINKF

Dimensions: 9 rows × 2 columns

| LENKWINKF_NR | LENKWINKF_TEXT |
| --- | --- |
| 0x00 | Lenkradwinkelsignal absolut und verifiziert |
| 0x01 | Lenkradwinkelsignal absolut |
| 0x02 | Lenkradwinkelsignal relativ |
| 0x03 | Lenkradwinkelsignal waehrend Diagnose |
| 0x04 | Lenkradwinkelsignal aus Radgeschwindigkeiten |
| 0x05 | Sensorfehler-&gt; kein Lenkradwinkelsignal |
| 0x06 | Elektronikfehler-&gt; kein Lenkradwinkelsignal |
| 0x07 | Signal Lenkradwinkel_Fehler fehlerhaft |
| 0x?? | unbekannt |

<a id="table-statlenkwinkt"></a>
### STATLENKWINKT

Dimensions: 4 rows × 2 columns

| LENKWINKT_NR | LENKWINKT_TEXT |
| --- | --- |
| 0x01 | Lenkradwinkelsignal waehrend Fehlertoleranzphase |
| 0x03 | Signal Lenkradwinkel_Toleranzphase fehlerhaft |
| 0x00 | Lenkradwinkelsignal ausserhalb Fehlertoleranzphase |
| 0x?? | unbekannt |

<a id="table-statzaehler"></a>
### STATZAEHLER

Dimensions: 16 rows × 2 columns

| STATZAEHLERNR | STATZAEHLERTEXT |
| --- | --- |
| 0x00 | Zaehlerstand 0 |
| 0x01 | Zaehlerstand 1 |
| 0x02 | Zaehlerstand 2 |
| 0x03 | Zaehlerstand 3 |
| 0x04 | Zaehlerstand 4 |
| 0x05 | Zaehlerstand 5 |
| 0x06 | Zaehlerstand 6 |
| 0x07 | Zaehlerstand 7 |
| 0x08 | Zaehlerstand 8 |
| 0x09 | Zaehlerstand 9 |
| 0x0A | Zaehlerstand 10 |
| 0x0B | Zaehlerstand 11 |
| 0x0C | Zaehlerstand 12 |
| 0x0D | Zaehlerstand 13 |
| 0x0E | Zaehlerstand 14 |
| 0x0F | Signal ungueltig |

<a id="table-statmotordreh"></a>
### STATMOTORDREH

Dimensions: 4 rows × 2 columns

| DREHZAHL_MOTOR_NR | DREHZAHL_MOTOR_TEXT |
| --- | --- |
| 0x00 | Signal Drehzahl_Motor ist in Ordnung |
| 0x01 | Drehzahlgeber defekt |
| 0x03 | Signal Drehzahl Motor Fehler fehlerhaft |
| 0x?? | unbekannt |

<a id="table-checkconrtol"></a>
### CHECKCONRTOL

Dimensions: 7 rows × 2 columns

| CHKCRTL_WERT | CHKCRTL_TEXT |
| --- | --- |
| 0x01 | Ueberwachung eingeschraenkt |
| 0x02 | eingeschraenkter Regelkomfort |
| 0x03 | Fail Safe |
| 0x04 | Oelverlust |
| 0x05 | Fail Safe temporaer |
| 0x06 | Signal ungueltig |
| 0xFF | unbekannte Anfrage |

<a id="table-statusschaltventile"></a>
### STATUSSCHALTVENTILE

Dimensions: 10 rows × 2 columns

| STATUS_SCHALT_VENTILE_WERT | STATUS_SCHALT_VENTILE_TEXT |
| --- | --- |
| 0x0000 | kein Fehler |
| 0x8001 | Kurzschluss nach Plus |
| 0x8002 | Kurzschluss nach Masse |
| 0x8004 | Leitungsunterbrechung |
| 0x8008 | Ventilkurzschluss |
| 0x8010 | keine Endstufen freigabe ueber Watchdog |
| 0x8020 | Ventilendstufe nicht kalibiriert |
| 0x8040 | Maximale Soll-Stromgrenze durch Ansteuer Fehler ueberschritten |
| 0x8080 | Strommesswert unplausibel |
| 0xFFFF | unbekannter Schaltventilfehler |

<a id="table-statuspropventile"></a>
### STATUSPROPVENTILE

Dimensions: 10 rows × 2 columns

| STATUS_PROP_VENTILE_WERT | STATUS_PROP_VENTILE_TEXT |
| --- | --- |
| 0x0000 | kein Fehler |
| 0x8001 | Kurzschluss nach Plus |
| 0x8002 | Kurzschluss nach Masse |
| 0x8004 | Leitungsunterbrechung |
| 0x8008 | Ventilkurzschluss |
| 0x8010 | keine Endstufen freigabe ueber Watchdog |
| 0x8020 | Ventilendstufe nicht kalibiriert |
| 0x8040 | Maximale Soll-Stromgrenze durch Ansteuer Fehler ueberschritten |
| 0x8080 | Strommesswert unplausibel |
| 0xFFFF | unbekannter Propventilfehler |

<a id="table-statusdrucksens"></a>
### STATUSDRUCKSENS

Dimensions: 6 rows × 2 columns

| STAT_DR_SENS_WERT | STAT_DR_SENS_TEXT |
| --- | --- |
| 0x0000 | kein Fehler |
| 0x8001 | Versorungsspannung zu hoch |
| 0x8002 | Versorgungsspannung zu tief oder ausgeschaltet |
| 0x8004 | Leitungsbruch bei Versorgung oder Abgriff |
| 0x8008 | Leitungsbruch Sensormasse |
| 0xFFFF | unbekannter Sensorfehler |

<a id="table-statusschaltsens"></a>
### STATUSSCHALTSENS

Dimensions: 6 rows × 2 columns

| STAT_SCHALT_SENS_WERT | STAT_SCHALT_SENS_TEXT |
| --- | --- |
| 0x0000 | kein Fehler |
| 0x8001 | Versorungsspannung zu hoch |
| 0x8002 | Versorgungsspannung zu tief |
| 0x8004 | Leitungsbruch bei Versorgung oder Abgriff |
| 0x8008 | Leitungsbruch Sensormasse |
| 0xFFFF | unbekannter Sensorfehler |

<a id="table-statusquersens"></a>
### STATUSQUERSENS

Dimensions: 6 rows × 2 columns

| STAT_QUER_SENS_WERT | STAT_QUER_SENS_TEXT |
| --- | --- |
| 0x0000 | kein Fehler |
| 0x8001 | Versorungsspannung zu hoch |
| 0x8002 | Versorgungsspannung zu tief |
| 0x8004 | Leitungsbruch bei Versorgung oder Abgriff |
| 0x8008 | Leitungsbruch Sensormasse |
| 0xFFFF | unbekannter Sensorfehler |

<a id="table-statuswecksens"></a>
### STATUSWECKSENS

Dimensions: 3 rows × 2 columns

| STAT_WECK_SENS_WERT | STAT_WECK_SENS_TEXT |
| --- | --- |
| 0x0000 | Weckleitung ist aus |
| 0x0001 | Weckleitung ist ein |
| 0xFFFF | Weckleitungszustand unbekannt |

<a id="table-statusoelstandsens"></a>
### STATUSOELSTANDSENS

Dimensions: 3 rows × 2 columns

| STAT_OELSTAND_SENS_WERT | STAT_OELSTAND_SENS_TEXT |
| --- | --- |
| 0x0000 | Oelstandsschalter aus |
| 0x0001 | Oelstandsschalter ein |
| 0xFFFF | Oelstandsschalter unbekannt |

<a id="table-ptcansignale"></a>
### PTCANSIGNALE

Dimensions: 5 rows × 2 columns

| PTCAN_FEHLER_WERT | PTCAN_FEHLER_TEXT |
| --- | --- |
| 0x0000 | kein Fehler |
| 0x8002 | Init Fehler |
| 0x8004 | Timeout Fehler |
| 0x8008 | Fehlerwert |
| 0xFFFF | unbekannter CAN Fehler |

<a id="table-statusdsc"></a>
### STATUSDSC

Dimensions: 6 rows × 2 columns

| STATUS_PTCAN_DSC_WERT | STATUS_PTCAN_DSC_TEXT |
| --- | --- |
| 0x00 | in Ordnung |
| 0x01 | passiv |
| 0x02 | defekt |
| 0x04 | Traktionsmodus |
| 0x07 | Signal ungueltig |
| 0xFF | unbekannter Status |

<a id="table-pre-drive"></a>
### PRE_DRIVE

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x90 | 0x91 | 0x92 | 0x93 |

<a id="table-pre-drive-1"></a>
### PRE_DRIVE_1

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0001 | Umlaufdruck temp. zu hoch o. Oel zu kalt |
| 0xFFFF | unbekannter Fehler |

<a id="table-pre-drive-2"></a>
### PRE_DRIVE_2

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0002 | Umlaufdruck dauerhaft zu hoch |
| 0xFFFF | unbekannter Fehler |

<a id="table-pre-drive-3"></a>
### PRE_DRIVE_3

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0004 | Motor in Fahrt gestoppt |
| 0xFFFF | unbekannter Fehler |

<a id="table-pre-drive-4"></a>
### PRE_DRIVE_4

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0008 | Zuschalten nach Reset waehrend Fahrt |
| 0xFFFF | unbekannter Fehler |

<a id="table-inbetr"></a>
### INBETR

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0xA0 | 0xA1 | 0xA2 | 0xA3 | 0xA4 | 0xA5 | 0xA6 |

<a id="table-inbetr-1"></a>
### INBETR_1

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0001 | 001 LowLevel oder PreDrive Fehler |
| 0xFFFF | unbekannter Fehler |

<a id="table-inbetr-2"></a>
### INBETR_2

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0002 | 002 Abbruch durch Tester |
| 0xFFFF | unbekannter Fehler |

<a id="table-inbetr-3"></a>
### INBETR_3

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0004 | 004 Motordrehzahl zu hoch |
| 0xFFFF | unbekannter Fehler |

<a id="table-inbetr-4"></a>
### INBETR_4

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0008 | 008 Motordrehzahl zu niedrig |
| 0xFFFF | unbekannter Fehler |

<a id="table-inbetr-5"></a>
### INBETR_5

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0010 | 016 Warnung Luft VA |
| 0xFFFF | unbekannter Fehler |

<a id="table-inbetr-6"></a>
### INBETR_6

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0020 | 032 Dynamik Fehler VA |
| 0xFFFF | unbekannter Fehler |

<a id="table-inbetr-7"></a>
### INBETR_7

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | IO |
| 0x0040 | 064 Dynamik Fehler VA/HA |
| 0xFFFF | unbekannter Fehler |
