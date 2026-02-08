# icm_71.prg

- Jobs: [99](#jobs)
- Tables: [73](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integrated Chassis Management für E71 |
| ORIGIN | BMW EF-610 Rüdiger Magdon |
| REVISION | 5.034 |
| AUTHOR | BMW EF-610 Rüdiger_Magdon, GTImbH EF-610 Peter_Gross-Grueber |
| COMMENT | N/A |
| PACKAGE | 1.43 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
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
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
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
- [C_CHECKSUMME](#job-c-checksumme) - Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob
- [STATUS_SZL](#job-status-szl) - Auslesen verschiedener vom SZL gesendeter Werte ueber F-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $06 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_SUMMENLENKWINKEL](#job-status-summenlenkwinkel) - Auslesen des im SG errechneten Summenlenkwinkelsrohwertes KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $23 Zustand des Werksmodus KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $08 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_FAHRERLENKWINKEL](#job-status-fahrerlenkwinkel) - Auslesen des Fahrerlenkwinkels vom SZL KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0A InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [STATUS_SG_STATE](#job-status-sg-state) - ICM_lt Steuergeraetestatus (diverse Zustandsgroessen) KWP2000: $22 ReadDataByCommonIdentifier SubID  : $0F recordCommonIdentifier(RCI_) SubID  : $FF recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_SG_WERK](#job-status-sg-werk) - ICM_lt Werksstatus KWP2000: $22 ReadDataByCommonIdentifier SubID  : $0F recordCommonIdentifier(RCI_) SubID  : $FF recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_QMVH_ZFM_FS_I](#job-status-qmvh-zfm-fs-i) - Kommunikation QSG ICM KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier(RCI_) SubID  : $01 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_QMVH_ZFM_ANTEUERUNG](#job-status-qmvh-zfm-anteuerung) - QSG Ansteuerung KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier(RCI_) SubID  : $02 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_QMVH_ZFM_ZAKT](#job-status-qmvh-zfm-zakt) - Zustände Aktuatoren KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier(RCI_) SubID  : $03 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_QMVH_ZFM_SOLL_IST_MOMENT](#job-status-qmvh-zfm-soll-ist-moment) - Soll Ist Moment KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier(RCI_) SubID  : $04 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_QES_FS_I](#job-status-zfm-qes-fs-i) - Qualität Eingangssignale ZFM KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $01 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_QES_AB_QMV](#job-status-zfm-qes-ab-qmv) - Qualität Eingangssignale ZFM KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $02 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_ZAKT_ABLEN](#job-status-zfm-zakt-ablen) - Zustände Aktuatoren KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $03 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_ZEF_FS](#job-status-zfm-zef-fs) - Zustände Externe Funktionen KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $04 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_ZIF_DK_VQ](#job-status-zfm-zif-dk-vq) - Zustände Interne Funktionalität KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $05 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_ZIF_DK_FQ](#job-status-zfm-zif-dk-fq) - Zustände Interne Funktionalität KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $06 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_ZIF_DK_RL](#job-status-zfm-zif-dk-rl) - Zustände Interne Funktionalität, Regelung-Laengs KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $07 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_ZIF_DK_SQ](#job-status-zfm-zif-dk-sq) - Zustände Interne Funktionalität KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $08 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_ZIF_DK_RQ](#job-status-zfm-zif-dk-rq) - Zustände Interne Funktionalität KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $09 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_QIS_DK_VQ](#job-status-zfm-qis-dk-vq) - Qualität Interne Signale KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $0A recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_QIS_DK_FQ](#job-status-zfm-qis-dk-fq) - Qualität Interne Signale KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $0B recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_QIS_DK_SQ](#job-status-zfm-qis-dk-sq) - Qualität Interne Signale KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $0C recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ZFM_QIS_DK_RQ](#job-status-zfm-qis-dk-rq) - Qualität Interne Signale KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $0D recordCommonIdentifier(RCI_) Modus  : Default
- [START_AL_LW_CODIERUNG_INIT](#job-start-al-lw-codierung-init) - AL Codierueberwachung zuruecksetzen [STEUERN_ADAPTIVDATEN_SETZEN(31,0)] KWP2000: $2E WriteDataByLocalIdentifer SubID  : $00 SubID  : $04 KWP2000: $11 ECUReset SubID  : $01 PowerOn Modus  : Default
- [START_ADAPTIVDATEN_ABGLEICH](#job-start-adaptivdaten-abgleich) - Aktiviert für einen Klemmenzyklus die Sensorabgleiche falls sie auskodiert sind KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $51 Abgleich der Adaptivdaten wird gestartet Modus  : Default
- [START_ADAPTIVDATEN_WERKSMODUS](#job-start-adaptivdaten-werksmodus) - Adaptivdaten im Werk vorbelegen KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $52 Toleranzbaender,Empfindlichleiten in den Adaptivdaten werden gesetzt Modus  : Default
- [START_ADAPTIVDATEN_RUECKSETZEN](#job-start-adaptivdaten-ruecksetzen) - Adaptivdaten werden auf DEFAULT Werte gesetzt, aus EEPROM oder ROM KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $53 Adaptivdaten im EEPROM werden auf DEFAULT Werte gesetzt Modus  : Default
- [START_ADAPTIVDATEN_OFFSET_LERNEN](#job-start-adaptivdaten-offset-lernen) - Schnellabgleich der Ax und Ay Werte Randbedingungen, Fahrzeugstillstand auf ebener Fläche KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $24 Lernen der Offsetwerte KWP2000: $11 ECUReset SubID  : $01 PowerOn Modus  : Default
- [STATUS_ADAPTIVDATEN_ABGLEICH](#job-status-adaptivdaten-abgleich) - aktueller Zustand des Adaptivdatenabgleichs Aktiviert für einen Klemmenzyklus die Sensorabgleiche falls sie auskodiert sind KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $51 alle aktuelle Abgleichstati abfragen Modus  : Default
- [STATUS_ADAPTIVDATEN_WERKSMODUS](#job-status-adaptivdaten-werksmodus) - aktueller Zustand des Ruecksetzens der Adaptivdaten KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $52 Toleranzbaender,Empfindlichleiten in den Adaptivdaten werden gesetzt Modus  : Default
- [STATUS_ADAPTIVDATEN_RUECKSETZEN](#job-status-adaptivdaten-ruecksetzen) - aktueller Zustand des Ruecksetzens der Adaptivdaten KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $53 Adaptivdaten werden mit DEFAULT Werten belegt Modus  : Default
- [STEUERN_ADAPTIVDATEN_SETZEN](#job-steuern-adaptivdaten-setzen) - Adaptivdaten setzen KWP2000: $2E WriteDataByLocalIdentifer SubID  : $00 SubID  : $04 KWP2000: $11 ECUReset SubID  : $01 PowerOn Modus  : Default
- [STATUS_ADAPTIVDATEN_LESEN](#job-status-adaptivdaten-lesen) - Adaptivdaten lesen KWP2000: $22 ReadDataByCommonIdentifier SubID  : $00 recordCommonIdentifier(RCI_) SubID  : $03 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_ADAPTIVDATEN_PU_LESEN](#job-status-adaptivdaten-pu-lesen) - Adaptivdaten lesen KWP2000: $22 ReadDataByCommonIdentifier SubID  : $00 recordCommonIdentifier(RCI_) SubID  : $05 recordCommonIdentifier(RCI_) Modus  : Default
- [STEUERN_ECO_VENTIL](#job-steuern-eco-ventil) - Bestromumg des ECO Ventils KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $20 InputOutputLocalIdentifier(IOLI) SubID  : $07 InputOutputControlParameter(IOCP) Modus  : Default
- [STEUERN_SERVO_VENTIL](#job-steuern-servo-ventil) - Bestromumg des SERVO Ventils KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $21 InputOutputLocalIdentifier(IOLI) SubID  : $07 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_ECO_VENTIL](#job-status-eco-ventil) - aktueller Zustand und Bestromung des ECO Ventils KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier SubID  : $05 recordCommonIdentifier Modus  : Default
- [STATUS_SERVO_VENTIL](#job-status-servo-ventil) - aktueller Zustand und Bestromung des SERVO Ventils KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier SubID  : $06 recordCommonIdentifier Modus  : Default
- [STATUS_AL_WINKELWERTE](#job-status-al-winkelwerte) - Auslesen verschiedener Winkelwerte, wie Fahrerlenkwinkel, Summenlenkwinkel, Motorlagewinkel KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $23 Zustand des Werksmodus KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0F InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [START_AL_MLW_RUECKSETZEN](#job-start-al-mlw-ruecksetzen) - Motorlagewinkel wird ungueltig gesetzt KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $21 Motorlagewinkel ungueltig setzen Modus  : Default
- [START_AL_MLWOFFSET_SETZEN](#job-start-al-mlwoffset-setzen) - intern berechneter Motorlagewinkeloffset wird gesepeichert KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $22 Speicherung des Motorlagewinkeloffset Modus  : Default
- [STEUERN_AL_INITMODE](#job-steuern-al-initmode) - AktivLenkung wird in den Werksmodus versetzt KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $23 Speicherung des Motorlagewinkeloffset Modus  : Default
- [STATUS_AL_INITMODE](#job-status-al-initmode) - aktueller Zustand ob AL im Werksmodus ist KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $23 Zustand des Werksmodus Modus  : Default
- [STATUS_AL_MLW_INIT](#job-status-al-mlw-init) - Gueltigkeit des Motorlagewinkels AL auslesen KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $20 Inbetriebnahme Resultat abfragen Modus  : Default
- [STATUS_AL_MLWOFFSET_SETZEN](#job-status-al-mlwoffset-setzen) - Status AL MLW Offset KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $22 Gueltigkeit AL Motorlagewinkeloffset Modus  : Default
- [STATUS_AL_ICM_VERBUND](#job-status-al-icm-verbund) - Status AktivLenkung beim ICM KWP2000: $22 ReadDataByCommonIdentifier SubID  : $00 recordCommonIdentifier(RCI_) SubID  : $01 recordCommonIdentifier(RCI_) Modus  : Default
- [STATUS_AL_CHECKCONTROL](#job-status-al-checkcontrol) - Checkcontrol Meldungen der Aktivlenkung KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $11 recordCommonIdentifier(RCI_) Modus  : Default
- [STEUERN_AL_SPANNUNGSVERSORGUNG](#job-steuern-al-spannungsversorgung) - AL Spannungsversorgung ein/ausschalten KWP2000: $2E WriteDataByCommonIdentifier SubID  : $F0 recordCommonIdentifier SubID  : $15 recordCommonIdentifier Modus  : Default
- [STATUS_FN_AL](#job-status-fn-al) - STATUS_FN_AL KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $56 Funktion AL analysieren Modus  : Default
- [START_MODUS_ROLLENPRUEFSTAND](#job-start-modus-rollenpruefstand) - versetzt das ICM Steuergerät in einen Rollenprüfstandsmodus Geschwindigkeit entspricht HA-Geschwindigkeit, Regler passiv KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $54 routineLocalIdentifier Modus  : Default
- [STOP_MODUS_ROLLENPRUEFSTAND](#job-stop-modus-rollenpruefstand) - dieser Job beendet den Rollenpruefstandsmodus des ICM-Steuergeraets KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $55 routineLocalIdentifier Modus  : Default
- [STATUS_ROLLENPRUEFSTAND](#job-status-rollenpruefstand) - dieser Job liefert den Status des Rollenprüfstandsmodus KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $54 routineLocalIdentifier Modus  : Default

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

<a id="job-c-checksumme"></a>
### C_CHECKSUMME

Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0 : Datentyp (1: Daten, 2: Maskendaten) Byte 1 : (unbenutzt) Wortbreite (1: Byte, 2: Word, 3: DWord) Byte 2 : (unbenutzt) Byteordnung (0: LSB zuerst, 1 MSB zuerst) Byte 3 : Adressierung (0: freie Adressierung, 1: Blockadressierung) Byte 4 : (unbenutzt) Byteparameter 1 Byte 5, 6 : (unbenutzt) WordParameter 1 (low / high) Byte 7, 8 : (unbenutzt) WordParameter 2 (low / high) Byte 9, 10, 11, 12 : (unbenutzt) Maske (linksbuendig) Byte 13, 14 : Anzahl Bytedaten (low / high) Byte 15, 16 : (unbenutzt) Anzahl Wortdaten (low / high) Byte 17, 18, 19, 20 : Wortadresse (low / highbyte, low / highword) Byte 21, .... : Codierdaten Byte 21 + Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| OUT_BUFFER | binary | Als Result wird der gefuellte Binaerbuffer zurueckgegeben Der Binaerbuffer hat den Aufbau von BINAER_BUFFER |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-szl"></a>
### STATUS_SZL

Auslesen verschiedener vom SZL gesendeter Werte ueber F-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $06 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SZL_SERIENNUMMER | string | gesendete Seriennummer des SZL CAN-ID: (201 / 0x0C9) Wertebereich: ( 0...99999999 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_SZL_FAHRERLENKWINKEL_OFFSET_GRAD_WERT | real | gesendeter Offsetwert des Fahrerlenkwinkels in Grad der beim Abgleich des SZL ermittelt wurde CAN-ID: (201 / 0x0C9) Skalierungsfaktor: ( (PH) = 0,04395 * (HEX) [°] ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -180...180 ) Einheit: ( Grad ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SZL_FAHRERLENKWINKEL_OFFSET_GRAD_EINH | string | Einheit des Fahrerlenkwinkels Einheit: ( Grad ) |
| STAT_SZL_FAHRERLENKWINKEL_OFFSET_RAD_WERT | real | gesendeter Offsetwert des Fahrerlenkwinkels in RAD der beim Abgleich des SZL ermittelt wurde CAN-ID: (201 / 0x0C9) Skalierungsfaktor: ( (PH) = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -180...180 ) Einheit: ( rad ) |
| STAT_SZL_FAHRERLENKWINKEL_OFFSET_RAD_EINH | string | Einheit des Fahrerlenkwinkels Einheit: ( rad ) |
| STAT_SZL_INFO_WERT | int | SZL Prozessor Info, Ein / Zwei Prozessorsystem CAN-ID: (201 / 0x0C9) Wertebereich: ( 0x00, 0xA0 ) moegliche Zustaende: ( 0x00 -- &gt; SZL Ein-Prozessor, kein AFS ) moegliche Zustaende: ( 0xA0 -- &gt; SZL Zwei-Prozessor, AFS ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SZL_INFO_EINH | string | Einheit: ( hex ) |
| STAT_SZL_INFO_TEXT | string | SZL Prozessor Info, Ein / Zwei Prozessorsystem CAN-ID: (201 / 0x0C9) Wertebereich: ( 0x00, 0xA0 ) moegliche Zustaende: ( 0x00 -- &gt; SZL Ein-Prozessor, kein AFS ) moegliche Zustaende: ( 0xA0 -- &gt; SZL Zwei-Prozessor, AFS ) Textausgabe ueber Tabelle: ( SZLProzInfo ) |
| STAT_SZL_ABGLEICH_WERT | int | gesendeter SZL Abgleich status CAN-ID: (201 / 0x0C9) Wertebereich: ( 00,01,10,11 ) moegliche Zustaende: ( 00 -- &gt; kein Abgleich ) moegliche Zustaende: ( 01 -- &gt; Abgleich ) moegliche Zustaende: ( 10 -- &gt; Coding ) moegliche Zustaende: ( 11 -- &gt; Signal ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SZL_ABGLEICH_EINH | string | Einheit: ( hex ) |
| STAT_SZL_ABGLEICH_TEXT | string | gesendeter SZL Abgleich status CAN-ID: (201 / 0x0C9) Wertebereich: ( 00,01,10,11 ) moegliche Zustaende: ( 00 -- &gt; kein Abgleich ) moegliche Zustaende: ( 01 -- &gt; Abgleich ) moegliche Zustaende: ( 10 -- &gt; Coding ) moegliche Zustaende: ( 11 -- &gt; Signal ungueltig ) Textausgabe ueber Tabelle: ( SZLAbgleichInfo ) |
| STAT_SZL_GUELTIGKEIT_FAHRER_LENKWINKEL_ROH_WERT | int | SZL Status des Fahrerlenkwinkels als Rohwert vom CAN Bus CAN-ID: (201 / 0x0C9) Wertebereich: ( 00,01,10,11 ) moegliche Zustaende: ( 00 -- &gt; absolut ) moegliche Zustaende: ( 01 -- &gt; relativ ) moegliche Zustaende: ( 10 -- &gt; Fehler ) moegliche Zustaende: ( 11 -- &gt; Signal ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SZL_GUELTIGKEIT_FAHRER_LENKWINKEL_ROH_EINH | string | Einheit: ( hex ) |
| STAT_SZL_GUELTIGKEIT_FAHRER_LENKWINKEL_ROH_TEXT | string | gesendeter SZL Abgleich status CAN-ID: (201 / 0x0C9) Wertebereich: ( 00,01,10,11 ) moegliche Zustaende: ( 00 -- &gt; absolut ) moegliche Zustaende: ( 01 -- &gt; relativ ) moegliche Zustaende: ( 10 -- &gt; Fehler ) moegliche Zustaende: ( 11 -- &gt; Signal ungueltig ) Textausgabe ueber Tabelle: ( SZLGueFLWRoh ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-summenlenkwinkel"></a>
### STATUS_SUMMENLENKWINKEL

Auslesen des im SG errechneten Summenlenkwinkelsrohwertes KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $23 Zustand des Werksmodus KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $08 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AL_INITMODE_WERT | int | aktueller Zustand der AL Initialisierung Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Werksmodus AL aus ) moegliche Zustaende: ( 1 -- &gt; Werksmodus AL ein ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AL_INITMODE_EINH | string | Einheit des aktueller Zustand der AL Initialisierung Einheit: ( hex ) |
| STAT_AL_INITMODE_TEXT | string | aktueller Zustand der AL Initialisierung moegliche Zustaende: ( 0 -- &gt; Werksmodus AL aus ) moegliche Zustaende: ( 1 -- &gt; Werksmodus AL ein ) Textausgabe ueber Tabelle: ( DigitalArgument ) |
| STAT_SUMMENLENKWINKELROH_RAD_WERT | real | SG intern berrechneter Summenlenkwinkelrohwert, virtueller Wert da KEIN Sensor vorhanden ist Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Wertebereich: ( -12,2173...+12,2173 ) Ungueltigkeitsbezeichnung: ( 8000 hex, -25,1327 rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_SUMMENLENKWINKELROH_RAD_EINH | string | Einheit des SG intern berrechneter Summenlenkwinkelrohwert Einheit: ( Grad ) |
| STAT_SUMMENLENKWINKELROH_GRAD_WERT | real | SG intern berrechneter Summenlenkwinkelrohwert, virtueller Wert da KEIN Sensor vorhanden ist Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Wertebereich: ( -700...+700 ) Ungueltigkeitsbezeichnung: ( 8000 hex, -1440 Grad ) Einheit: ( Grad ) |
| STAT_SUMMENLENKWINKELROH_GRAD_EINH | string | Einheit des SG intern berrechneter Summenlenkwinkelrohwert Einheit: ( Grad ) |
| STAT_GUELTIGKEIT_SUMMENLENKWINKELROH_WERT | int | SG intern berrechneter Summenlenkwinkelrohwert, virtueller Wert da KEIN Sensor vorhanden ist, Filter 0x07 Gueltigkeit des Fahrerlenkwinkels vom SZL moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; nicht definiert ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_GUELTIGKEIT_SUMMENLENKWINKELROH_EINH | string | Einheit: ( ohne ) |
| STAT_GUELTIGKEIT_SUMMENLENKWINKELROH_TEXT | string | SG intern berrechneter Summenlenkwinkelrohwert, virtueller Wert da KEIN Sensor vorhanden ist, Filter 0x07 Gueltigkeit des Fahrerlenkwinkels vom SZL moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; nicht definiert ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Textausgabe ueber Tabelle: ( GueSLWroh ) |
| STAT_SUMMENLENKWINKEL_RAD_EINH | string | Einheit des Summenwinkels bezogen auf Ritzel Einheit: ( rad Ritzel ) |
| STAT_SUMMENLENKWINKEL_GRAD_EINH | string | Einheit des Summenwinkels bezogen auf Ritzel Einheit: ( Grad Ritzel ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG_1 | binary | Hex Auftrag an SG |
| _TEL_ANTWORT_1 | binary | Hex - Antwort von SG |
| _TEL_DATEN_1 | binary | Hex - Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex - Antwort von SG |
| _TEL_DATEN_2 | binary | Hex - Antwort von SG |

<a id="job-status-fahrerlenkwinkel"></a>
### STATUS_FAHRERLENKWINKEL

Auslesen des Fahrerlenkwinkels vom SZL KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0A InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAHRER_LENKWINKEL_RAD_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -25.132232 rad...25.132232 rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_FAHRER_LENKWINKEL_GRAD_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -1439.95Grad...1439.95Grad ) Einheit: ( Grad ) |
| STAT_FAHRER_LENKWINKEL_1_ALIVECOUNTER_WERT | int | Alivezaehler des Fahrerlenkwinkels vom SZL ueber F-CAN CAN-ID: (201 / 0x0C9) Ungueltigkeitsbezeichnung: ( 15 ) Wertebereich: ( 0...14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_FAHRER_LENKWINKEL_1_ALIVECOUNTER_EINH | string | Einheit des Alivezaehler des Fahrerlenkwinkels vom SZL ueber F-CAN Einheit: ( hex ) |
| STAT_GUELTIGKEIT_FAHRER_LENKWINKEL_WERT | int | Gueltigkeit des Fahrerlenkwinkels vom SZL, Filter 0x07 moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; nicht definiert ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_FAHRER_LENKWINKEL_EINH | string | Einheit der Gueltigkeit des Fahrerlenkwinkels vom SZL, Filter 0x07 Einheit: ( hex ) |
| STAT_GUELTIGKEIT_FAHRERLENKWINKEL_TEXT | string | Gueltigkeit des Fahrerlenkwinkels vom SZL moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; nicht definiert ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Textausgabe ueber Tabelle: ( GueFLW ) |
| STAT_FAHRER_LENKWINKEL_REDUNDANT_RAD_WERT | real | Fahrerlenkwinkel mit Absicherungszaehler vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [grad] ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -25.132232 rad...25.132232 rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_FAHRER_LENKWINKEL_REDUNDANT_RAD_EINH | string | Einheit des Fahrerlenkwinkel mit Absicherungszaehlers vom SZL gesendet ueber F-CAN Einheit: ( rad ) |
| STAT_FAHRER_LENKWINKEL_REDUNDANT_GRAD_WERT | real | Fahrerlenkwinkel mit Absicherungszaehler vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [grad] ) Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -1439.95Grad...1439.95Grad ) Einheit: ( Grad ) |
| STAT_FAHRER_LENKWINKEL_REDUNDANT_GRAD_EINH | string | Einheit des Fahrerlenkwinkel mit Absicherungszaehlers vom SZL gesendet ueber F-CAN Einheit: ( Grad ) |
| STAT_FAHRER_LENKWINKEL_2_ALIVECOUNTER_WERT | int | Alivezaehler des Fahrerlenkwinkels vom SZL ueber F-CAN CAN-ID: (201 / 0x0C9) Ungueltigkeitsbezeichnung: ( 0 ) Wertebereich: ( 1...3 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_FAHRER_LENKWINKEL_2_ALIVECOUNTER_EINH | string | Einheit des Alivezaehler des Fahrerlenkwinkels vom SZL ueber F-CAN Einheit: ( hex ) |
| STAT_FAHRER_LENKWINKEL_RAD_EINH | string | Einheit des Fahrerlenkwinkels Einheit: ( rad ) |
| STAT_FAHRER_LENKWINKEL_GRAD_EINH | string | Einheit des Fahrerlenkwinkels Einheit: ( Grad ) |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_RAD_WERT | real | Fahrerlenkwinkelgeshwindikkeit vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [° / s] ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -25.132232 rad/s...25.132232 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_GRAD_WERT | real | Fahrerlenkwinkelgeshwindikkeit vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [° / s] ) Skalierungsfaktor: ( (PH)[grad/s] = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -1439.95Grad/s...1439.95Grad/s ) Einheit: ( Grad/s ) |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_RAD_EINH | string | Einheit der Fahrerlenkwinkelgeschwindigkeit Einheit: ( rad/s ) |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_GRAD_EINH | string | Einheit der Fahrerlenkwinkelgeschwindigkeit Einheit: ( Grad/s ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-sg-state"></a>
### STATUS_SG_STATE

ICM_lt Steuergeraetestatus (diverse Zustandsgroessen) KWP2000: $22 ReadDataByCommonIdentifier SubID  : $0F recordCommonIdentifier(RCI_) SubID  : $FF recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AKTIVER_FEHLER_WERT | string | bitweiser Error-Status Wertebereich: ( 0...(2**32)-1 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_AKTIVER_FEHLER_EINH | string | Einheit des bitweisen Error-Status Einheit: ( string ) |
| STAT_ZUSTAND_AKTUELL | string | Steuergeraetezustand Wertebereich: ( 0...255 ) moegliche Zustaende: ( 0x00 -- &gt; SG_STATE_BOOT_INIT ) moegliche Zustaende: ( 0x11 -- &gt; SG_STATE_BOOT_ACTIVE ) moegliche Zustaende: ( 0x22 -- &gt; SG_STATE_BOOT_ERROR ) moegliche Zustaende: ( 0x33 -- &gt; SG_STATE_BOOT_SAVE ) moegliche Zustaende: ( 0x44 -- &gt; SG_STATE_APPL_INIT ) moegliche Zustaende: ( 0x55 -- &gt; SG_STATE_APPL_ACTIVE ) moegliche Zustaende: ( 0x66 -- &gt; SG_STATE_APPL_ERROR ) moegliche Zustaende: ( 0x77 -- &gt; SG_STATE_APPL_SAVE ) moegliche Zustaende: ( 0x88 -- &gt; SG_STATE_APPL_ERROR_2 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZUSTAND_AKTUELL_TEXT | string | Steuergeraetezustand Wertebereich: ( 0...255 ) moegliche Zustaende: ( 0x00 -- &gt; SG_STATE_BOOT_INIT ) moegliche Zustaende: ( 0x11 -- &gt; SG_STATE_BOOT_ACTIVE ) moegliche Zustaende: ( 0x22 -- &gt; SG_STATE_BOOT_ERROR ) moegliche Zustaende: ( 0x33 -- &gt; SG_STATE_BOOT_SAVE ) moegliche Zustaende: ( 0x44 -- &gt; SG_STATE_APPL_INIT ) moegliche Zustaende: ( 0x55 -- &gt; SG_STATE_APPL_ACTIVE ) moegliche Zustaende: ( 0x66 -- &gt; SG_STATE_APPL_ERROR ) moegliche Zustaende: ( 0x77 -- &gt; SG_STATE_APPL_SAVE ) moegliche Zustaende: ( 0x88 -- &gt; SG_STATE_APPL_ERROR_2 ) Textausgabe ueber Tabelle: ( SGStati ) |
| STAT_ZUSTAND_MERKER | string | Steuergeraetezustand Wertebereich: ( 0...255 ) moegliche Zustaende: ( 0x00 -- &gt; SG_STATE_BOOT_INIT ) moegliche Zustaende: ( 0x11 -- &gt; SG_STATE_BOOT_ACTIVE ) moegliche Zustaende: ( 0x22 -- &gt; SG_STATE_BOOT_ERROR ) moegliche Zustaende: ( 0x33 -- &gt; SG_STATE_BOOT_SAVE ) moegliche Zustaende: ( 0x44 -- &gt; SG_STATE_APPL_INIT ) moegliche Zustaende: ( 0x55 -- &gt; SG_STATE_APPL_ACTIVE ) moegliche Zustaende: ( 0x66 -- &gt; SG_STATE_APPL_ERROR ) moegliche Zustaende: ( 0x77 -- &gt; SG_STATE_APPL_SAVE ) moegliche Zustaende: ( 0x88 -- &gt; SG_STATE_APPL_ERROR_2 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZUSTAND_MERKER_TEXT | string | Steuergeraetezustand Wertebereich: ( 0...255 ) moegliche Zustaende: ( 0x00 -- &gt; SG_STATE_BOOT_INIT ) moegliche Zustaende: ( 0x11 -- &gt; SG_STATE_BOOT_ACTIVE ) moegliche Zustaende: ( 0x22 -- &gt; SG_STATE_BOOT_ERROR ) moegliche Zustaende: ( 0x33 -- &gt; SG_STATE_BOOT_SAVE ) moegliche Zustaende: ( 0x44 -- &gt; SG_STATE_APPL_INIT ) moegliche Zustaende: ( 0x55 -- &gt; SG_STATE_APPL_ACTIVE ) moegliche Zustaende: ( 0x66 -- &gt; SG_STATE_APPL_ERROR ) moegliche Zustaende: ( 0x77 -- &gt; SG_STATE_APPL_SAVE ) moegliche Zustaende: ( 0x88 -- &gt; SG_STATE_APPL_ERROR_2 ) Textausgabe ueber Tabelle: ( SGStati ) |
| STAT_DIVCALC_ERROR | string | Error-Flags DivCalc Wertebereich: ( 0...(2**16)-1 ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_TIMESTAMP | unsigned long | Betriebszeit / Zeitstempel Wertebereich: ( 0..2^32-1 ) Einheit: ( ms ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_KLEMME30_WERT | real | Spannungswert an Klemme 30 Wertebereich: ( 0..20 ) Skalierungsfaktor: ( 1000 ) Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_KLEMME30_EINH | string | Einheit der Spannung Einheit: ( Volt ) |
| STAT_SPANNUNG_EINH | string | Einheit der Spannung Einheit: ( Volt ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-sg-werk"></a>
### STATUS_SG_WERK

ICM_lt Werksstatus KWP2000: $22 ReadDataByCommonIdentifier SubID  : $0F recordCommonIdentifier(RCI_) SubID  : $FF recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STEUERGERAET_WERT | int | Interpretation aus Byte(7) Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Steuergeraet n.i.O. ) moegliche Zustaende: ( 1 -- &gt; Steuergeraet i.O. ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_STEUERGERAET_EINH | string | Einheit des Stg-Zustands Einheit: ( hex ) |
| STAT_STEUERGERAET_TEXT | string | Interpretation aus Byte(7) Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Steuergeraet n.i.O. ) moegliche Zustaende: ( 1 -- &gt; Steuergeraet i.O. ) Textausgabe ueber Tabelle: ( SGStatus ) |
| STAT_FAHRGESTELLNR_WERT | int | Interpretation aus Byte(3-6) und Byte(7) Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Fahrgestellnummner ungueltig ) moegliche Zustaende: ( 1 -- &gt; Fahrgestellnummner gueltig ) Telegrammlaenge KWP: ( 4 + 1 Byte ) |
| STAT_FAHRGESTELLNR_EINH | string | Einheit des FGST-Zustands Einheit: ( hex ) |
| STAT_FAHRGESTELLNR_TEXT | string | Interpretation aus Byte(3-6) und Byte(7) Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Fahrgestellnummner ungueltig ) moegliche Zustaende: ( 1 -- &gt; Fahrgestellnummner gueltig ) Textausgabe ueber Tabelle: ( FahrgestellNrStatus ) |
| STAT_DIVCALC_WERT | int | Interpretation aus Byte(9,10) Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; diversitaeres Rechnen n.i.O. ) moegliche Zustaende: ( 1 -- &gt; diversitaeres Rechnen i.O. ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_DIVCALC_EINH | string | Einheit des DIVALC-Zustands Einheit: ( hex ) |
| STAT_DIVCALC_TEXT | string | Interpretation aus Byte(3-6) und Byte(7) Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; diversitaeres Rechnen n.i.O. ) moegliche Zustaende: ( 1 -- &gt; diversitaeres Rechnen i.O. ) Textausgabe ueber Tabelle: ( DivCalcStatus ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-qmvh-zfm-fs-i"></a>
### STATUS_QMVH_ZFM_FS_I

Kommunikation QSG ICM KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier(RCI_) SubID  : $01 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMFS_I_QMVH_SQ_WERT | int | Kommunikation QSG ICM Wertebereich: ( 0...255 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_QMVH_SQ_EINH | string | Einheit der Kommunikation QSG ICM Einheit: ( hex ) |
| STAT_ZFMFS_I_QMVH_SQ_FSQUAL_WERT | int | Kommunikation FSQUAL QSG ICM Wertebereich: ( 0...255 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_QMVH_SQ_FSQUAL_EINH | string | Einheit der FSQUAL Kommunikation QSG ICM Einheit: ( hex ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-qmvh-zfm-anteuerung"></a>
### STATUS_QMVH_ZFM_ANTEUERUNG

QSG Ansteuerung KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier(RCI_) SubID  : $02 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMKAQMV_I_M_DIFF_HA_STAT_WERT | int | QSG Ansteuerung Wertebereich: ( 0...255 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMKAQMV_I_M_DIFF_HA_STAT_EINH | string | Einheit der QSG Ansteuerung Einheit: ( hex ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-qmvh-zfm-zakt"></a>
### STATUS_QMVH_ZFM_ZAKT

Zustände Aktuatoren KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier(RCI_) SubID  : $03 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMABQMV_I_QMVH_AKT_ZST_WERT | int | Zustände Aktuatoren Wertebereich: ( 0...255 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMABQMV_I_QMVH_AKT_ZST_EINH | string | Einheit Zustände Aktuatoren Einheit: ( hex ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-qmvh-zfm-soll-ist-moment"></a>
### STATUS_QMVH_ZFM_SOLL_IST_MOMENT

Soll Ist Moment KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier(RCI_) SubID  : $04 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMKAQMV_R_M_DIFF_HA_WERT | real | Soll Ist Moment Wertebereich: ( tbd. ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_ZFMKAQMV_R_M_DIFF_HA_EINH | string | Einheit des Soll Ist Moment Einheit: ( hex ) |
| STAT_ZFMWRE_R_MQMVH_WERT | real | Soll Ist Moment Wertebereich: ( tbd. ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_ZFMWRE_R_MQMVH_EINH | string | Einheit des Soll Ist Moment Einheit: ( hex ) |
| STAT_ZFMFS_I_DSC_ROM_FKT_ZST_WERT | int | Soll Ist Moment Wertebereich: ( 0...255 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_DSC_ROM_FKT_ZST_EINH | string | Einheit des Soll Ist Moment Einheit: ( hex ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-qes-fs-i"></a>
### STATUS_ZFM_QES_FS_I

Qualität Eingangssignale ZFM KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $01 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMFS_I_V_FSQUAL_UNBEHANDELT_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_V_FSQUAL_UNBEHANDELT_EINH | string | Einheit derQualität Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_V_FSQUAL_UNBEHANDELT_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_VX_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_VX_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_VX_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_LWFAHRER_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_LWFAHRER_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_LWFAHRER_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_LW_VA_IST_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_LW_VA_IST_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_LW_VA_IST_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_LW_VA_RITZEL_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_LW_VA_RITZEL_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_LW_VA_RITZEL_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_PSIP_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_PSIP_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_PSIP_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_AY_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_AY_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_AY_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_AY_SN_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_AY_SN_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_AY_SN_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_AX_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_AX_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_AX_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_AX_LS_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_AX_LS_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_AX_LS_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_VCH_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_VCH_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_VCH_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_SX_DIFF_HA_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_SX_DIFF_HA_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_SX_DIFF_HA_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_LMV_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_LMV_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_LMV_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_LW_VA_EFF_OFFSET_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_LW_VA_EFF_OFFSET_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_LW_VA_EFF_OFFSET_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_LW_VA_EFF_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_LW_VA_EFF_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_LW_VA_EFF_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_LWVA_AKT_IST_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_LWVA_AKT_IST_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_LWVA_AKT_IST_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_LWHA_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_LWHA_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_LWHA_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_OMEGAMOTOR_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_OMEGAMOTOR_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_OMEGAMOTOR_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_ENGINE_RUN_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_ENGINE_RUN_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_ENGINE_RUN_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_GMV_SQ_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_GMV_SQ_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_GMV_SQ_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_ASA_SQ_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_ASA_SQ_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_ASA_SQ_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_QMVH_SQ_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_QMVH_SQ_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_QMVH_SQ_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_MRAD_BREMS_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_MRAD_BREMS_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_MRAD_BREMS_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_DSC_ABS_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_DSC_ABS_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_DSC_ABS_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_ANHAENGER_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_ANHAENGER_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_ANHAENGER_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_OMEGARAD_HL_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_OMEGARAD_HL_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_OMEGARAD_HL_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_OMEGARAD_HR_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_OMEGARAD_HR_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_OMEGARAD_HR_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_KL_DSC_QMVH_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_KL_DSC_QMVH_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_KL_DSC_QMVH_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_KR_DSC_QMVH_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_KR_DSC_QMVH_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_KR_DSC_QMVH_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_VB_QMVH_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_VB_QMVH_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_VB_QMVH_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_MRAD_ANTRIEB_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_MRAD_ANTRIEB_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_MRAD_ANTRIEB_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_MRAD_ANTRIEB_FW_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_MRAD_ANTRIEB_FW_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_MRAD_ANTRIEB_FW_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_BLS_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_BLS_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_BLS_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_LWVA_AKT_MAX_DYN_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_LWVA_AKT_MAX_DYN_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_LWVA_AKT_MAX_DYN_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_KLEMME15_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_KLEMME15_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_KLEMME15_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_VX_REG_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_VX_REG_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_VX_REG_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| STAT_ZFMFS_I_PWG_FSQUAL_WERT | int | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_PWG_FSQUAL_EINH | string | Einheit des Eingangssignale ZFM FS Qualifier Einheit: ( hex ) |
| STAT_ZFMFS_I_PWG_FSQUAL_TEXT | string | Qualität Eingangssignale ZFM FS Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-qes-ab-qmv"></a>
### STATUS_ZFM_QES_AB_QMV

Qualität Eingangssignale ZFM KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $02 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMABQMV_I_KKIN_ABQUAL_WERT | int | Qualität Eingangssignale ZFM AB Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMABQMV_I_KKIN_ABQUAL_EINH | string | Einheit der Qualität der Eingangssignale ZFM AB Qualifier Einheit: ( hex ) |
| STAT_ZFMABQMV_I_KKIN_ABQUAL_TEXT | string | Qualität Eingangssignale ZFM AB Qualifier Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QES_fsqual ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-zakt-ablen"></a>
### STATUS_ZFM_ZAKT_ABLEN

Zustände Aktuatoren KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $03 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMABLEN_AFS_AKT_ZST_WERT | int | Zustände Aktuatoren im ZFM Wertebereich: ( 1,2,4,8,16 ) moegliche Zustaende: ( 0x01 -- &gt; Aktuator Fehler ) moegliche Zustaende: ( 0x02 -- &gt; Aktuator nicht verbaut ) moegliche Zustaende: ( 0x04 -- &gt; Aktuator eingeschraenkt verfuegbar ) moegliche Zustaende: ( 0x08 -- &gt; Aktuator nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Aktuator will Sollwert ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMABLEN_AFS_AKT_ZST_EINH | string | Einheit der Zustände der Aktuatoren im ZFM Einheit: ( hex ) |
| STAT_ZFMABLEN_AFS_AKT_ZST_TEXT | string | Zustände Aktuatoren im ZFM Wertebereich: ( 1,2,4,8,16 ) moegliche Zustaende: ( 0x01 -- &gt; Aktuator Fehler ) moegliche Zustaende: ( 0x02 -- &gt; Aktuator nicht verbaut ) moegliche Zustaende: ( 0x04 -- &gt; Aktuator eingeschraenkt verfuegbar ) moegliche Zustaende: ( 0x08 -- &gt; Aktuator nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Aktuator will Sollwert ) Textausgabe ueber Tabelle: ( ZFM_AKT_zst ) |
| STAT_ZFMABLEN_GMVH_AKT_ZST_WERT | int | Zustände Aktuatoren im ZFM Wertebereich: ( 1,2,4,8,16 ) moegliche Zustaende: ( 0x01 -- &gt; Aktuator Fehler ) moegliche Zustaende: ( 0x02 -- &gt; Aktuator nicht verbaut ) moegliche Zustaende: ( 0x04 -- &gt; Aktuator eingeschraenkt verfuegbar ) moegliche Zustaende: ( 0x08 -- &gt; Aktuator nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Aktuator will Sollwert ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMABLEN_GMVH_AKT_ZST_EINH | string | Einheit der Zustände der Aktuatoren im ZFM Einheit: ( hex ) |
| STAT_ZFMABLEN_GMVH_AKT_ZST_TEXT | string | Zustände Aktuatoren im ZFM Wertebereich: ( 1,2,4,8,16 ) moegliche Zustaende: ( 0x01 -- &gt; Aktuator Fehler ) moegliche Zustaende: ( 0x02 -- &gt; Aktuator nicht verbaut ) moegliche Zustaende: ( 0x04 -- &gt; Aktuator eingeschraenkt verfuegbar ) moegliche Zustaende: ( 0x08 -- &gt; Aktuator nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Aktuator will Sollwert ) Textausgabe ueber Tabelle: ( ZFM_AKT_zst ) |
| STAT_ZFMABLEN_QMVH_AKT_ZST_WERT | int | Zustände Aktuatoren im ZFM Wertebereich: ( 1,2,4,8,16 ) moegliche Zustaende: ( 0x01 -- &gt; Aktuator Fehler ) moegliche Zustaende: ( 0x02 -- &gt; Aktuator nicht verbaut ) moegliche Zustaende: ( 0x04 -- &gt; Aktuator eingeschraenkt verfuegbar ) moegliche Zustaende: ( 0x08 -- &gt; Aktuator nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Aktuator will Sollwert ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMABLEN_QMVH_AKT_ZST_EINH | string | Einheit der Zustände der Aktuatoren im ZFM Einheit: ( hex ) |
| STAT_ZFMABLEN_QMVH_AKT_ZST_TEXT | string | Zustände Aktuatoren im ZFM Wertebereich: ( 1,2,4,8,16 ) moegliche Zustaende: ( 0x01 -- &gt; Aktuator Fehler ) moegliche Zustaende: ( 0x02 -- &gt; Aktuator nicht verbaut ) moegliche Zustaende: ( 0x04 -- &gt; Aktuator eingeschraenkt verfuegbar ) moegliche Zustaende: ( 0x08 -- &gt; Aktuator nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Aktuator will Sollwert ) Textausgabe ueber Tabelle: ( ZFM_AKT_zst ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-zef-fs"></a>
### STATUS_ZFM_ZEF_FS

Zustände Externe Funktionen KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $04 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMFS_I_DSC_ABS_FKT_ZST_WERT | int | Zustände Externe Funktionen Wertebereich: ( 0...4 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit ) moegliche Zustaende: ( 0x02 -- &gt; aktiv ) moegliche Zustaende: ( 0x03 -- &gt; fehler ) moegliche Zustaende: ( 0x04 -- &gt; in abschaltung ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_DSC_ABS_FKT_ZST_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMFS_I_DSC_ABS_FKT_ZST_TEXT | string | Zustände Externe Funktionen Wertebereich: ( 0...4 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit ) moegliche Zustaende: ( 0x02 -- &gt; aktiv ) moegliche Zustaende: ( 0x03 -- &gt; fehler ) moegliche Zustaende: ( 0x04 -- &gt; in abschaltung ) Textausgabe ueber Tabelle: ( ZFM_ZEF_zst ) |
| STAT_ZFMFS_I_DSC_FZR_FKT_ZST_WERT | int | Zustände Externe Funktionen Wertebereich: ( 0...4 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit ) moegliche Zustaende: ( 0x02 -- &gt; aktiv ) moegliche Zustaende: ( 0x03 -- &gt; fehler ) moegliche Zustaende: ( 0x04 -- &gt; in abschaltung ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_DSC_FZR_FKT_ZST_EINH | string | Einheit der Zustände der Externen Funktionen Einheit: ( hex ) |
| STAT_ZFMFS_I_DSC_FZR_FKT_ZST_TEXT | string | Zustände Externe Funktionen Wertebereich: ( 0...4 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit ) moegliche Zustaende: ( 0x02 -- &gt; aktiv ) moegliche Zustaende: ( 0x03 -- &gt; fehler ) moegliche Zustaende: ( 0x04 -- &gt; in abschaltung ) Textausgabe ueber Tabelle: ( ZFM_ZEF_zst ) |
| STAT_ZFMFS_I_DSC_ROM_FKT_ZST_WERT | int | Zustände Externe Funktionen Wertebereich: ( 0...4 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit ) moegliche Zustaende: ( 0x02 -- &gt; aktiv ) moegliche Zustaende: ( 0x03 -- &gt; fehler ) moegliche Zustaende: ( 0x04 -- &gt; in abschaltung ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMFS_I_DSC_ROM_FKT_ZST_EINH | string | Einheit der Zustands der Externen Funktionen Einheit: ( hex ) |
| STAT_ZFMFS_I_DSC_ROM_FKT_ZST_TEXT | string | Zustände Externe Funktionen Wertebereich: ( 0...4 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit ) moegliche Zustaende: ( 0x02 -- &gt; aktiv ) moegliche Zustaende: ( 0x03 -- &gt; fehler ) moegliche Zustaende: ( 0x04 -- &gt; in abschaltung ) Textausgabe ueber Tabelle: ( ZFM_ZEF_zst ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-zif-dk-vq"></a>
### STATUS_ZFM_ZIF_DK_VQ

Zustände Interne Funktionalität KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $05 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMDKVQ_I_ZS_VX_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_ZS_VX_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_ZS_VX_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKVQ_I_ZS_AFSSVSOLL_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_ZS_AFSSVSOLL_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_ZS_AFSSVSOLL_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKVQ_I_ZS_ECO_SOLL_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_ZS_ECO_SOLL_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_ZS_ECO_SOLL_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKVQ_I_ZS_SERVO_SOLL_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_ZS_SERVO_SOLL_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_ZS_SERVO_SOLL_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKVQ_I_ZS_AFSDVSOLL_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_ZS_AFSDVSOLL_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_ZS_AFSDVSOLL_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKVQ_I_ZS_GMVHSVSOLL_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_ZS_GMVHSVSOLL_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_ZS_GMVHSVSOLL_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKVQ_I_ZS_QMVHSVSOLL_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_ZS_QMVHSVSOLL_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_ZS_QMVHSVSOLL_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKVQ_I_ZS_QMVHDVSOLL_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_ZS_QMVHDVSOLL_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_ZS_QMVHDVSOLL_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKVQ_I_ZS_LWVA_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_ZS_LWVA_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_ZS_LWVA_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKVQ_I_ZS_VSRHSRADD_SOLL_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_ZS_VSRHSRADD_SOLL_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_ZS_VSRHSRADD_SOLL_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-zif-dk-fq"></a>
### STATUS_ZFM_ZIF_DK_FQ

Zustände Interne Funktionalität KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $06 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMDKFQ_I_ZS_FQ_PSIP_ACK_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKFQ_I_ZS_FQ_PSIP_ACK_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKFQ_I_ZS_FQ_PSIP_ACK_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKFQ_I_ZS_FQ_GRRPLUS_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKFQ_I_ZS_FQ_GRRPLUS_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKFQ_I_ZS_FQ_GRRPLUS_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-zif-dk-rl"></a>
### STATUS_ZFM_ZIF_DK_RL

Zustände Interne Funktionalität, Regelung-Laengs KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $07 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMDKRL_I_ZS_RL_QMVH_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKRL_I_ZS_RL_QMVH_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKRL_I_ZS_RL_QMVH_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKRL_I_ZS_RL_QMVH_QDBEG_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKRL_I_ZS_RL_QMVH_QDBEG_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKRL_I_ZS_RL_QMVH_QDBEG_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-zif-dk-sq"></a>
### STATUS_ZFM_ZIF_DK_SQ

Zustände Interne Funktionalität KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $08 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMDKSQ_I_ZS_SQ_QMVH_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKSQ_I_ZS_SQ_QMVH_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKSQ_I_ZS_SQ_QMVH_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKSQ_I_ZS_SQ_AFS_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKSQ_I_ZS_SQ_AFS_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKSQ_I_ZS_SQ_AFS_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKSQ_I_ZS_SQ_GMVH_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKSQ_I_ZS_SQ_GMVH_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKSQ_I_ZS_SQ_GMVH_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-zif-dk-rq"></a>
### STATUS_ZFM_ZIF_DK_RQ

Zustände Interne Funktionalität KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $09 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMDKRQ_I_ZS_RQ_QMVH_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKRQ_I_ZS_RQ_QMVH_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKRQ_I_ZS_RQ_QMVH_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKRQ_I_ZS_RQ_AFS_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKRQ_I_ZS_RQ_AFS_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKRQ_I_ZS_RQ_AFS_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| STAT_ZFMDKRQ_I_ZS_RQ_GMVH_WERT | int | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKRQ_I_ZS_RQ_GMVH_EINH | string | Einheit der Zustände der Internen Funktionalität Einheit: ( hex ) |
| STAT_ZFMDKRQ_I_ZS_RQ_GMVH_TEXT | string | Zustände Interne Funktionalität Wertebereich: ( 0...3 ) moegliche Zustaende: ( 0x00 -- &gt; passiv ) moegliche Zustaende: ( 0x01 -- &gt; bereit passiv ) moegliche Zustaende: ( 0x02 -- &gt; bereit aktiv ) moegliche Zustaende: ( 0x03 -- &gt; aktiv ) Textausgabe ueber Tabelle: ( ZFM_ZIF_zs ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-qis-dk-vq"></a>
### STATUS_ZFM_QIS_DK_VQ

Qualität Interne Signale KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $0A recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMDKVQ_I_LWVA_STG_NSQ_WERT | int | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_LWVA_STG_NSQ_EINH | string | Einheit der Qualität der Internen Signale Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_LWVA_STG_NSQ_TEXT | string | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QIS_nsq ) |
| STAT_ZFMDKVQ_I_LWVA_STELL_NSQ_WERT | int | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKVQ_I_LWVA_STELL_NSQ_EINH | string | Einheit der Qualität der Internen Signale Einheit: ( hex ) |
| STAT_ZFMDKVQ_I_LWVA_STELL_NSQ_TEXT | string | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QIS_nsq ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-qis-dk-fq"></a>
### STATUS_ZFM_QIS_DK_FQ

Qualität Interne Signale KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $0B recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMDKFQ_I_FQ_PSIP_ACK_NSQ_WERT | int | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKFQ_I_FQ_PSIP_ACK_NSQ_EINH | string | Einheit der Qualität der Internen Signale Einheit: ( hex ) |
| STAT_ZFMDKFQ_I_FQ_PSIP_ACK_NSQ_TEXT | string | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QIS_nsq ) |
| STAT_ZFMDKFQ_I_FQ_ESM_NSQ_WERT | int | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKFQ_I_FQ_ESM_NSQ_EINH | string | Einheit der Qualität der Internen Signale Einheit: ( hex ) |
| STAT_ZFMDKFQ_I_FQ_ESM_NSQ_TEXT | string | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QIS_nsq ) |
| STAT_ZFMDKFQ_I_FQ_AY_NSQ_WERT | int | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKFQ_I_FQ_AY_NSQ_EINH | string | Einheit der Qualität der Internen Signale Einheit: ( hex ) |
| STAT_ZFMDKFQ_I_FQ_AY_NSQ_TEXT | string | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QIS_nsq ) |
| STAT_ZFMDKFQ_I_FQ_IND_NSQ_WERT | int | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKFQ_I_FQ_IND_NSQ_EINH | string | Einheit der Qualität der Internen Signale Einheit: ( hex ) |
| STAT_ZFMDKFQ_I_FQ_IND_NSQ_TEXT | string | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QIS_nsq ) |
| STAT_ZFMDKFQ_I_FQ_MUESPLIT_NSQ_WERT | int | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKFQ_I_FQ_MUESPLIT_NSQ_EINH | string | Einheit der Qualität der Internen Signale Einheit: ( hex ) |
| STAT_ZFMDKFQ_I_FQ_MUESPLIT_NSQ_TEXT | string | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QIS_nsq ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-qis-dk-sq"></a>
### STATUS_ZFM_QIS_DK_SQ

Qualität Interne Signale KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $0C recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMDKSQ_I_SQ_AX_NSQ_WERT | int | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKSQ_I_SQ_AX_NSQ_EINH | string | Einheit der Qualität der Internen Signale Einheit: ( hex ) |
| STAT_ZFMDKSQ_I_SQ_AX_NSQ_TEXT | string | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QIS_nsq ) |
| STAT_ZFMDKSQ_I_SQ_BA_NSQ_WERT | int | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKSQ_I_SQ_BA_NSQ_EINH | string | Einheit der Qualität der Internen Signale Einheit: ( hex ) |
| STAT_ZFMDKSQ_I_SQ_BA_NSQ_TEXT | string | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QIS_nsq ) |
| STAT_ZFMDKSQ_I_SQ_GRRPLUS_NSQ_WERT | int | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKSQ_I_SQ_GRRPLUS_NSQ_EINH | string | Einheit der Qualität der Internen Signale Einheit: ( hex ) |
| STAT_ZFMDKSQ_I_SQ_GRRPLUS_NSQ_TEXT | string | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QIS_nsq ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfm-qis-dk-rq"></a>
### STATUS_ZFM_QIS_DK_RQ

Qualität Interne Signale KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $0D recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFMDKSQ_I_RQ_GRRPLUS_NSQ_WERT | int | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ZFMDKSQ_I_RQ_GRRPLUS_NSQ_EINH | string | Einheit der Qualität der Internen Signale Einheit: ( hex ) |
| STAT_ZFMDKSQ_I_RQ_GRRPLUS_NSQ_TEXT | string | Qualität Interne Signale Wertebereich: ( 0...7 ) moegliche Zustaende: ( 0x00 -- &gt; Initialisierung ) moegliche Zustaende: ( 0x01 -- &gt; Gueltig und abgesichert ) moegliche Zustaende: ( 0x02 -- &gt; Gueltig ) moegliche Zustaende: ( 0x03 -- &gt; Nicht vertrauenswuerdig ) moegliche Zustaende: ( 0x04 -- &gt; Ersatzwert ) moegliche Zustaende: ( 0x05 -- &gt; Kommunikationsfehler ) moegliche Zustaende: ( 0x06 -- &gt; Ungueltig ) moegliche Zustaende: ( 0x07 -- &gt; Ungueltig ) Textausgabe ueber Tabelle: ( ZFM_QIS_nsq ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-start-al-lw-codierung-init"></a>
### START_AL_LW_CODIERUNG_INIT

AL Codierueberwachung zuruecksetzen [STEUERN_ADAPTIVDATEN_SETZEN(31,0)] KWP2000: $2E WriteDataByLocalIdentifer SubID  : $00 SubID  : $04 KWP2000: $11 ECUReset SubID  : $01 PowerOn Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex - Auftrag fuer StgReset an SG |
| _TEL_ANTWORT_2 | binary | Hex - Antwort auf StgReset von SG |
| _TEL_DATEN_2 | binary | Hex - Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |

<a id="job-start-adaptivdaten-abgleich"></a>
### START_ADAPTIVDATEN_ABGLEICH

Aktiviert für einen Klemmenzyklus die Sensorabgleiche falls sie auskodiert sind KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $51 Abgleich der Adaptivdaten wird gestartet Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADAPTIVDATEN_ABGLEICH_WERT | char | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ADAPTIVDATEN_ABGLEICH_EINH | string | Einheit des Zustands Abgleich Einheit: ( hex ) |
| STAT_ADAPTIVDATEN_ABGLEICH_TEXT | string | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Textausgabe ueber Tabelle: ( JobInterpretation ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-start-adaptivdaten-werksmodus"></a>
### START_ADAPTIVDATEN_WERKSMODUS

Adaptivdaten im Werk vorbelegen KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $52 Toleranzbaender,Empfindlichleiten in den Adaptivdaten werden gesetzt Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADAPTIVDATEN_WERKSMODUS_WERT | char | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ADAPTIVDATEN_WERKSMODUS_EINH | string | Einheit des Zustands Abgleich Einheit: ( hex ) |
| STAT_ADAPTIVDATEN_WERKSMODUS_TEXT | string | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Textausgabe ueber Tabelle: ( JobInterpretation ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-start-adaptivdaten-ruecksetzen"></a>
### START_ADAPTIVDATEN_RUECKSETZEN

Adaptivdaten werden auf DEFAULT Werte gesetzt, aus EEPROM oder ROM KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $53 Adaptivdaten im EEPROM werden auf DEFAULT Werte gesetzt Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADAPTIVDATEN_RUECKSETZEN_WERT | char | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ADAPTIVDATEN_RUECKSETZEN_EINH | string | Einheit des Zustands Abgleich Einheit: ( hex ) |
| STAT_ADAPTIVDATEN_RUECKSETZEN_TEXT | string | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Textausgabe ueber Tabelle: ( JobInterpretation ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-start-adaptivdaten-offset-lernen"></a>
### START_ADAPTIVDATEN_OFFSET_LERNEN

Schnellabgleich der Ax und Ay Werte Randbedingungen, Fahrzeugstillstand auf ebener Fläche KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $24 Lernen der Offsetwerte KWP2000: $11 ECUReset SubID  : $01 PowerOn Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADAPTIVDATEN_OFFSET_LERNEN_WERT | char | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ADAPTIVDATEN_OFFSET_LERNEN_EINH | string | Einheit des Zustands Abgleich Einheit: ( hex ) |
| STAT_ADAPTIVDATEN_OFFSET_LERNEN_TEXT | string | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Textausgabe ueber Tabelle: ( JobInterpretation ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex - Auftrag StgReset an SG |
| _TEL_ANTWORT_2 | binary | Hex - Antwort auf RESET von SG |
| _TEL_DATEN_2 | binary | Hex - Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |

<a id="job-status-adaptivdaten-abgleich"></a>
### STATUS_ADAPTIVDATEN_ABGLEICH

aktueller Zustand des Adaptivdatenabgleichs Aktiviert für einen Klemmenzyklus die Sensorabgleiche falls sie auskodiert sind KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $51 alle aktuelle Abgleichstati abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADAPTIVDATEN_ABGLEICH_WERT | int | aktueller Status des Adaptivdatenabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Abgleich aktiv ) moegliche Zustaende: ( 1 -- &gt; Abgleich NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ADAPTIVDATEN_ABGLEICH_EINH | string | Einheit des aktuellen Status des Adaptivdatenabgleichs Einheit: ( hex ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-adaptivdaten-werksmodus"></a>
### STATUS_ADAPTIVDATEN_WERKSMODUS

aktueller Zustand des Ruecksetzens der Adaptivdaten KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $52 Toleranzbaender,Empfindlichleiten in den Adaptivdaten werden gesetzt Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADAPTIVDATEN_WERKSMODUS_WERT | int | aktueller Status des Adaptivdatenwerksmodus Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; aus ) moegliche Zustaende: ( 1 -- &gt; ein ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ADAPTIVDATEN_WERKSMODUS_EINH | string | Einheit des aktuellen Status des Adaptivdatenwerksmodus Einheit: ( hex ) |
| STAT_ADAPTIVDATEN_WERKSMODUS_TEXT | string | aktueller Status des Reifentoleranzabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; aus ) moegliche Zustaende: ( 1 -- &gt; ein ) Textausgabe ueber Tabelle: ( DigitalArgument ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-adaptivdaten-ruecksetzen"></a>
### STATUS_ADAPTIVDATEN_RUECKSETZEN

aktueller Zustand des Ruecksetzens der Adaptivdaten KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $53 Adaptivdaten werden mit DEFAULT Werten belegt Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RTA_ABGLEICH_WERT | int | aktueller Status des Reifentoleranzabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_RTA_ABGLEICH_EINH | string | Einheit des aktuellen Status des Reifentoleranzabgleichs Einheit: ( hex ) |
| STAT_YR_ABGLEICH_WERT | int | aktueller Status des Gierratenabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_YR_ABGLEICH_EINH | string | Einheit des aktuellen Status des Gierratenabgleichs Einheit: ( hex ) |
| STAT_AY_ABGLEICH_WERT | int | aktueller Status des Querbeschleunigungsabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AY_ABGLEICH_EINH | string | Einheit des aktuellen Status des Querbeschleunigungsabgleichs Einheit: ( hex ) |
| STAT_SLW_ABGLEICH_WERT | int | aktueller Status des Summenlenkwinkelabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SLW_ABGLEICH_EINH | string | Einheit des aktuellen Status des Summenlenkwinkelabgleichs Einheit: ( hex ) |
| STAT_AX_ABGLEICH_WERT | int | aktueller Status des Laengsbeschleunigungsabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AX_ABGLEICH_EINH | string | Einheit des aktuellen Status des Laengsbeschleunigungsabgleichs Einheit: ( hex ) |
| STAT_VCH_ABGLEICH_WERT | int | aktueller Status der charakter. Geschwindigkeitsabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_VCH_ABGLEICH_EINH | string | Einheit des aktuellen Status des charakter. Geschwindigkeitsabgleichs Einheit: ( hex ) |
| STAT_RLLL_ABGLEICH_WERT | int | aktueller Status RechtsLinkslenker Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_RLLL_ABGLEICH_EINH | string | Einheit des aktuellen Status des RechtsLinkslenkers Einheit: ( hex ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-steuern-adaptivdaten-setzen"></a>
### STEUERN_ADAPTIVDATEN_SETZEN

Adaptivdaten setzen KWP2000: $2E WriteDataByLocalIdentifer SubID  : $00 SubID  : $04 KWP2000: $11 ECUReset SubID  : $01 PowerOn Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADAPTIV_INDEX_WERT | int | Wertebereich: ( 0...65565 ) moegliche Zustaende: (  0 -- &gt; VCH Lernwerttoleranz (beide Kurven) ) moegliche Zustaende: (  1 -- &gt; VCH Lernwerttoleranz (links Kurven) ) moegliche Zustaende: (  2 -- &gt; VCH Lernwerttoleranz (rechts Kurven) ) moegliche Zustaende: (  3 -- &gt; VCH Lernwert (beide Kurven) ) moegliche Zustaende: (  4 -- &gt; VCH Lernwert (links Kurven) ) moegliche Zustaende: (  5 -- &gt; VCH Lernwert (rechts Kurven) ) moegliche Zustaende: (  6 -- &gt; Korrekturfaktor für die Rollrate zur Kompensation des Gierratenübersprechens ) moegliche Zustaende: (  7 -- &gt; Offsetwert des Längsbeschleunigungssensors 1 ) moegliche Zustaende: (  8 -- &gt; Signaltoleranz des Längsbeschleunigungsnutzsignals 1 ) moegliche Zustaende: (  9 -- &gt; Offsetwert des Querbeschleunigungssensors 1 ) moegliche Zustaende: ( 10 -- &gt; Signaltoleranz des Querbeschleunigungsnutzsignals 1 ) moegliche Zustaende: ( 11 -- &gt; Offsetwert des Querbeschleunigungssensors 2 ) moegliche Zustaende: ( 12 -- &gt; Signaltoleranz des Querbeschleunigungsnutzsignals 2 ) moegliche Zustaende: ( 13 -- &gt; Offsetwert des Ritzelwinkels ) moegliche Zustaende: ( 14 -- &gt; Signaltoleranz des Ritzelwinkelnutzsignals ) moegliche Zustaende: ( 15 -- &gt; Offsetwert des Rollratensensors 1 ) moegliche Zustaende: ( 16 -- &gt; Signaltoleranz des Rollratennutzsignals 1 ) moegliche Zustaende: ( 17 -- &gt; Offsetwert des Gierratensensors 1 aus Fahrtabgleich ) moegliche Zustaende: ( 18 -- &gt; Offsetwert des Gierratensensors 1 aus Stillstandsabgleich ) moegliche Zustaende: ( 19 -- &gt; Signaltoleranz des Gierratennutzsignals 1 ) moegliche Zustaende: ( 20 -- &gt; Offsetwert des Gierratensensors 2 aus Fahrtabgleich ) moegliche Zustaende: ( 21 -- &gt; Offsetwert des Gierratensensors 2 aus Stillstandsabgleich ) moegliche Zustaende: ( 22 -- &gt; Signaltoleranz des Gierratennutzsignals 2 ) moegliche Zustaende: ( 23 -- &gt; Empfindlichkeit des Längsbeschleunigungssensors 1 ) moegliche Zustaende: ( 24 -- &gt; Radtoleranz hinten links ) moegliche Zustaende: ( 25 -- &gt; Radtoleranz hinten rechts ) moegliche Zustaende: ( 26 -- &gt; Radtoleranz vorne links ) moegliche Zustaende: ( 27 -- &gt; Radtoleranz vorne rechts ) moegliche Zustaende: ( 28 -- &gt; Empfindlichkeit Rollratensensor 1 ) moegliche Zustaende: ( 29 -- &gt; Empfindlichkeit Gierratensensor 1 ) moegliche Zustaende: ( 30 -- &gt; Empfindlichkeit Gierratensensor 2 ) moegliche Zustaende: ( 31 -- &gt; Lernwert für die Lenkwinkelkodierüberwachung ) moegliche Zustaende: ( 32 -- &gt; Lernwert für die Vorzeichenüberwachung Querbeschleunigung 1 ) moegliche Zustaende: ( 33 -- &gt; Lernwert für die Vorzeichenüberwachung Querbeschleunigung 2 ) moegliche Zustaende: ( 34 -- &gt; Lernwert für die Vorzeichenüberwachung Gierrate 1 ) moegliche Zustaende: ( 35 -- &gt; Lernwert für die Vorzeichenüberwachung Gierrate 2 ) moegliche Zustaende: ( 36 -- &gt; Lernwert für die Vorzeichenüberwachung Gierrate aus Radgeschwindigkeiten ) moegliche Zustaende: ( 37 -- &gt; Lernwert für Offset des Lernwerts ax aus Antriebsmoment ) moegliche Zustaende: ( 38 -- &gt; Lernwert für Offset des Lernwerts ofs_deYR ) Telegrammlaenge KWP: ( 4 Byte ) |
| ADAPTIV_WERT | real | zu schreibender Adaptivwert Wertebereich: ( 0...????? ) Telegrammlaenge KWP: ( 4 Byte ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex - Auftrag fuer StgReset an SG |
| _TEL_ANTWORT_2 | binary | Hex - Antwort auf StgReset von SG |
| _TEL_DATEN_2 | binary | Hex - Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |

<a id="job-status-adaptivdaten-lesen"></a>
### STATUS_ADAPTIVDATEN_LESEN

Adaptivdaten lesen KWP2000: $22 ReadDataByCommonIdentifier SubID  : $00 recordCommonIdentifier(RCI_) SubID  : $03 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SBS_2EV_R_VCH_INTRO_B | real | VCH Lernwerttoleranz (beide Kurven) Wertebereich: ( 0...5 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_2EV_R_VCH_INTRO_L | real | VCH Lernwerttoleranz (links Kurven) Wertebereich: ( 0...5 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_SBS_2EV_R_VCH_INTRO_R | real | VCH Lernwerttoleranz (rechts Kurven) Wertebereich: ( 0...5 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_2EV_R_VCH_WERT0_B | real | VCH Lernwert (beide Kurven) Wertebereich: ( 20...40 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_2EV_R_VCH_WERT0_L | real | VCH Lernwert (links Kurven) Wertebereich: ( 20...40 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_2EV_R_VCH_WERT0_R | real | VCH Lernwert (rechts Kurven) Wertebereich: ( 20...40 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_KYR_XR1 | real | Korrekturfaktor für die Rollrate zur Kompensation des Gierratenübersprechens Wertebereich: ( -1...1 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AX1 | real | Offsetwert des Längsbeschleunigungssensors 1 Wertebereich: ( -4...4 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AX1_TOL | real | Signaltoleranz des Längsbeschleunigungsnutzsignals 1 Wertebereich: ( 0....5 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AY1 | real | Offsetwert des Querbeschleunigungssensors 1 Wertebereich: ( -4...4 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AY1_TOL | real | Signaltoleranz des Querbeschleunigungsnutzsignals 1 Wertebereich: ( 0....5 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AY2 | real | Offsetwert des Querbeschleunigungssensors 2 Wertebereich: ( -4...4 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AY2_TOL | real | Signaltoleranz des Querbeschleunigungsnutzsignals 2 Wertebereich: ( 0....5 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_DE | real | Offsetwert des Ritzelwinkels Wertebereich: ( -0,45....0,45 rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_DE_TOL | real | Signaltoleranz des Ritzelwinkelnutzsignals Wertebereich: ( 0...0,5 rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_XR1 | real | Offsetwert des Rollratensensors 1 Wertebereich: ( -0,2....0,2 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_XR1_TOL | real | Signaltoleranz des Rollratennutzsignals 1 Wertebereich: (  0...0,2 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR1_DRV | real | Offsetwert des Gierratensensors 1 aus Fahrtabgleich Wertebereich: ( -0,3....0,3 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR1_STST | real | Offsetwert des Gierratensensors 1 aus Stillstandsabgleich Wertebereich: ( -0,3....0,3 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR1_TOL | real | Signaltoleranz des Gierratennutzsignals 1 Wertebereich: ( -0,2....0,2 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR2_DRV | real | Offsetwert des Gierratensensors 2 aus Fahrtabgleich Wertebereich: ( -0,3....0,3 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR2_STST | real | Offsetwert des Gierratensensors 2 aus Stillstandsabgleich Wertebereich: ( -0,3....0,3 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR2_TOL | real | Signaltoleranz des Gierratennutzsignals 2 Wertebereich: (  0...0,2 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_AX1 | real | Empfindlichkeit des Längsbeschleunigungssensors 1 Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_VWHL_HL | real | Radtoleranz hinten links Wertebereich: ( -0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_VWHL_HR | real | Radtoleranz hinten rechts Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_VWHL_VL | real | Radtoleranz vorne links Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_VWHL_VR | real | Radtoleranz vorne rechts Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_XR1 | real | Empfindlichkeit Rollratensensor 1 Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_YR1 | real | Empfindlichkeit Gierratensensor 1 Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_YR2 | real | Empfindlichkeit Gierratensensor 2 Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_SBS_3DE_IDE_CODE | real | Lernwert für die Lenkwinkelkodierüberwachung Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_AY1_SGN | real | Lernwert für die Vorzeichenüberwachung Querbeschleunigung 1 Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_AY2_SGN | real | Lernwert für die Vorzeichenüberwachung Querbeschleunigung 2 Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_YR1_SGN | real | Lernwert für die Vorzeichenüberwachung Gierrate 1 Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_YR2_SGN | real | Lernwert für die Vorzeichenüberwachung Gierrate 2 Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_YR_WH_SGN | real | Lernwert für die Vorzeichenüberwachung Gierrate aus Radgeschwindigkeiten Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_ZFMFS_OFS_AXM_WERT | real | Lernwert für Offset des Lernwerts ax aus Antriebsmoment Wertebereich: ( 0....5 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_ZFMFS_OFS_AXM_EINH | string | Einheit des Offset des Lernwerts ax aus Antriebsmoment Einheit: ( m/s**2 ) |
| STAT_COMP_OFS_DEYR_WERT | real | Comparatorempfindlichkeit Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_DEYR_EINH | string | Einheit der Comparatorempfindlichkeit Einheit: ( ohne ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-adaptivdaten-pu-lesen"></a>
### STATUS_ADAPTIVDATEN_PU_LESEN

Adaptivdaten lesen KWP2000: $22 ReadDataByCommonIdentifier SubID  : $00 recordCommonIdentifier(RCI_) SubID  : $05 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SBS_2EV_R_VCH_INTRO_B | real | VCH Lernwerttoleranz (beide Kurven) Wertebereich: ( 0...5 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_2EV_R_VCH_INTRO_L | real | VCH Lernwerttoleranz (links Kurven) Wertebereich: ( 0...5 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_SBS_2EV_R_VCH_INTRO_R | real | VCH Lernwerttoleranz (rechts Kurven) Wertebereich: ( 0...5 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_2EV_R_VCH_WERT0_B | real | VCH Lernwert (beide Kurven) Wertebereich: ( 20...40 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_2EV_R_VCH_WERT0_L | real | VCH Lernwert (links Kurven) Wertebereich: ( 20...40 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_2EV_R_VCH_WERT0_R | real | VCH Lernwert (rechts Kurven) Wertebereich: ( 20...40 m/s ) Einheit: ( m/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_KYR_XR1 | real | Korrekturfaktor für die Rollrate zur Kompensation des Gierratenübersprechens Wertebereich: ( -1...1 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AX1 | real | Offsetwert des Längsbeschleunigungssensors 1 Wertebereich: ( -4...4 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AX1_TOL | real | Signaltoleranz des Längsbeschleunigungsnutzsignals 1 Wertebereich: ( 0....5 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AY1 | real | Offsetwert des Querbeschleunigungssensors 1 Wertebereich: ( -4...4 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AY1_TOL | real | Signaltoleranz des Querbeschleunigungsnutzsignals 1 Wertebereich: ( 0....5 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AY2 | real | Offsetwert des Querbeschleunigungssensors 2 Wertebereich: ( -4...4 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_AY2_TOL | real | Signaltoleranz des Querbeschleunigungsnutzsignals 2 Wertebereich: ( 0....5 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_DE | real | Offsetwert des Ritzelwinkels Wertebereich: ( -0,45....0,45 rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_DE_TOL | real | Signaltoleranz des Ritzelwinkelnutzsignals Wertebereich: ( 0...0,5 rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_XR1 | real | Offsetwert des Rollratensensors 1 Wertebereich: ( -0,2....0,2 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_XR1_TOL | real | Signaltoleranz des Rollratennutzsignals 1 Wertebereich: (  0...0,2 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR1_DRV | real | Offsetwert des Gierratensensors 1 aus Fahrtabgleich Wertebereich: ( -0,3....0,3 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR1_STST | real | Offsetwert des Gierratensensors 1 aus Stillstandsabgleich Wertebereich: ( -0,3....0,3 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR1_TOL | real | Signaltoleranz des Gierratennutzsignals 1 Wertebereich: ( -0,2....0,2 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR2_DRV | real | Offsetwert des Gierratensensors 2 aus Fahrtabgleich Wertebereich: ( -0,3....0,3 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR2_STST | real | Offsetwert des Gierratensensors 2 aus Stillstandsabgleich Wertebereich: ( -0,3....0,3 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_YR2_TOL | real | Signaltoleranz des Gierratennutzsignals 2 Wertebereich: (  0...0,2 rad/s ) Einheit: ( rad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_AX1 | real | Empfindlichkeit des Längsbeschleunigungssensors 1 Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_VWHL_HL | real | Radtoleranz hinten links Wertebereich: ( -0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_VWHL_HR | real | Radtoleranz hinten rechts Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_VWHL_VL | real | Radtoleranz vorne links Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_VWHL_VR | real | Radtoleranz vorne rechts Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_XR1 | real | Empfindlichkeit Rollratensensor 1 Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_YR1 | real | Empfindlichkeit Gierratensensor 1 Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_SENS_YR2 | real | Empfindlichkeit Gierratensensor 2 Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_SBS_3DE_IDE_CODE | real | Lernwert für die Lenkwinkelkodierüberwachung Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_AY1_SGN | real | Lernwert für die Vorzeichenüberwachung Querbeschleunigung 1 Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_AY2_SGN | real | Lernwert für die Vorzeichenüberwachung Querbeschleunigung 2 Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_YR1_SGN | real | Lernwert für die Vorzeichenüberwachung Gierrate 1 Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_YR2_SGN | real | Lernwert für die Vorzeichenüberwachung Gierrate 2 Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_I_YR_WH_SGN | real | Lernwert für die Vorzeichenüberwachung Gierrate aus Radgeschwindigkeiten Wertebereich: ( -125....125 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_ZFMFS_OFS_AXM_WERT | real | Lernwert für Offset des Lernwerts ax aus Antriebsmoment Wertebereich: ( 0....5 m/s2 ) Einheit: ( m/s2 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_ZFMFS_OFS_AXM_EINH | string | Einheit des Offset des Lernwerts ax aus Antriebsmoment Einheit: ( m/s**2 ) |
| STAT_COMP_OFS_DEYR_WERT | real | Comparatorempfindlichkeit Wertebereich: ( 0,5....1,5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_COMP_OFS_DEYR_EINH | string | Einheit der Comparatorempfindlichkeit Einheit: ( ohne ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-steuern-eco-ventil"></a>
### STEUERN_ECO_VENTIL

Bestromumg des ECO Ventils KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $20 InputOutputLocalIdentifier(IOLI) SubID  : $07 InputOutputControlParameter(IOCP) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ECO_VENTIL_STROM_SOLL_WERT | real | zu stellender Strom fuer das Servo Ventil Wertebereich: ( 0...1000 mA ) Telegrammlaenge KWP: ( 4 Byte ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ECO_VENTIL_STEUERUNG_WERT | int | Zustand ECO Ventil moegliche Zustaende: ( 1 -- &gt; Bestromung i.O. ) moegliche Zustaende: ( 8x -- &gt; Anfrage konnte nicht ausgefuehrt werden ) Wertebereich: ( 1, 129...143 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ECO_VENTIL_STEUERUNG_EINH | string | Einheit des Zustands ECO Ventil Einheit: ( ohne ) |
| STAT_ECO_VENTIL_STEUERUNG_BIT0_TEXT | string | Zustand ECO Ventil moegliche Zustaende: ( Bit0 = '0' -- &gt; vx kleiner/gleich als 3m/s ) moegliche Zustaende: ( Bit0 = '1' -- &gt; vx groesser als 3m/s ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusECOVentil ) |
| STAT_ECO_VENTIL_STEUERUNG_BIT1_TEXT | string | Zustand ECO Ventil moegliche Zustaende: ( Bit1 = '0' -- &gt; Qualifier gueltig ) moegliche Zustaende: ( Bit1 = '1' -- &gt; Qualifier ungueltig ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusECOVentil ) |
| STAT_ECO_VENTIL_STEUERUNG_BIT2_TEXT | string | Zustand ECO Ventil moegliche Zustaende: ( Bit2 = '0' -- &gt; Motor an ) moegliche Zustaende: ( Bit2 = '1' -- &gt; Motor aus ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusECOVentil ) |
| STAT_ECO_VENTIL_STEUERUNG_BIT3_TEXT | string | Zustand ECO Ventil moegliche Zustaende: ( Bit3 = '0' -- &gt; ECO in Ordnung ) moegliche Zustaende: ( Bit3 = '1' -- &gt; ECO im Selbsttest oder defekt ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusECOVentil ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-steuern-servo-ventil"></a>
### STEUERN_SERVO_VENTIL

Bestromumg des SERVO Ventils KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $21 InputOutputLocalIdentifier(IOLI) SubID  : $07 InputOutputControlParameter(IOCP) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERVO_VENTIL_STROM_SOLL_WERT | real | zu stellender Strom fuer das Servo Ventil Wertebereich: ( 0...1000 mA ) Telegrammlaenge KWP: ( 4 Byte ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERVO_VENTIL_STEUERUNG_WERT | int | Zustand SERVO Ventil moegliche Zustaende: ( 1 -- &gt; Bestromung i.O. ) moegliche Zustaende: ( 8x -- &gt; Anfrage konnte nicht ausgefuehrt werden ) Wertebereich: ( 1, 129...143 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SERVO_VENTIL_STEUERUNG_EINH | string | Einheit der Comparatorempfindlichkeit Einheit: ( ohne ) |
| STAT_SERVO_VENTIL_STEUERUNG_BIT0_TEXT | string | Zustand ECO Ventil moegliche Zustaende: ( Bit0 = '0' -- &gt; vx kleiner/gleich als 3m/s ) moegliche Zustaende: ( Bit0 = '1' -- &gt; vx groesser als 3m/s ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusSERVOVentil ) |
| STAT_SERVO_VENTIL_STEUERUNG_BIT1_TEXT | string | Zustand ECO Ventil moegliche Zustaende: ( Bit1 = '0' -- &gt; Qualifier gueltig ) moegliche Zustaende: ( Bit1 = '1' -- &gt; Qualifier ungueltig ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusSERVOVentil ) |
| STAT_SERVO_VENTIL_STEUERUNG_BIT2_TEXT | string | Zustand ECO Ventil moegliche Zustaende: ( Bit2 = '0' -- &gt; Motor an ) moegliche Zustaende: ( Bit2 = '1' -- &gt; Motor aus ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusSERVOVentil ) |
| STAT_SERVO_VENTIL_STEUERUNG_BIT3_TEXT | string | Zustand ECO Ventil moegliche Zustaende: ( Bit3 = '0' -- &gt; SVT in Ordnung ) moegliche Zustaende: ( Bit3 = '1' -- &gt; SVT im Selbsttest oder defekt ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusSERVOVentil ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-eco-ventil"></a>
### STATUS_ECO_VENTIL

aktueller Zustand und Bestromung des ECO Ventils KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier SubID  : $05 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ECO_VENTIL_ZUSTAND_WERT | int | akteuller ECO Ventil Zustand Wertebereich: ( 0..15 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ECO_VENTIL_ZUSTAND_EINH | string | Einheit des Zustands ECO Ventil Einheit: ( ohne ) |
| STAT_ECO_VENTIL_ZUSTAND_BIT0_TEXT | string | akteuller ECO Ventil Zustand moegliche Zustaende: ( Bit0 = '0' -- &gt; ECO Ventil in Ordnung ) moegliche Zustaende: ( Bit0 = '1' -- &gt; ECO Ventil fehlerhaft ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusECOVentil_Bit0 ) |
| STAT_ECO_VENTIL_ZUSTAND_BIT1_TEXT | string | akteuller ECO Ventil Zustand moegliche Zustaende: ( Bit1 = '0' -- &gt; ECO Venitl verbaut ) moegliche Zustaende: ( Bit1 = '1' -- &gt; ECO Ventil nicht verbaut ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusECOVentil_Bit1 ) |
| STAT_ECO_VENTIL_ZUSTAND_BIT3_TEXT | string | akteuller ECO Ventil Zustand moegliche Zustaende: ( Bit3 = '0' -- &gt; ECO Ventil verfuegbar ) moegliche Zustaende: ( Bit3 = '1' -- &gt; ECO Ventil nicht verfuegbar ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusECOVentil_Bit3 ) |
| STAT_ECO_VENTIL_STROM_SOLL_WERT | real | gestellter Strom am Servo Ventil Wertebereich: ( 0...1000 mA ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_ECO_VENTIL_STROM_SOLL_EINH | string | Einheit des Stromes Einheit: ( mA ) |
| STAT_ECO_VENTIL_STROM_EINH | string | Einheit des Stromes Einheit: ( mA ) |
| STAT_ECO_VENTIL_STEUERUNG_WERT | int | gibt an ob Strom fuer das ECO Ventil ueber Diagnose oder Modell gestellt wird Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0 -- &gt; nein, Modell ) moegliche Zustaende: ( 1 -- &gt; ja, Diagnose ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ECO_VENTIL_STEUERUNG_EINH | string | Einheit des Zustands ECO Ventil Einheit: ( ohne ) |
| STAT_ECO_VENTIL_STEUERUNG_TEXT | string | gibt an ob Strom fuer das SERVO Ventil ueber Diagnose oder ASCET gestellt wird Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0 -- &gt; nein, Modell ) moegliche Zustaende: ( 1 -- &gt; ja, Diagnose ) Textausgabe ueber Tabelle: ( DigitalArgument ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-servo-ventil"></a>
### STATUS_SERVO_VENTIL

aktueller Zustand und Bestromung des SERVO Ventils KWP2000: $22 ReadDataByCommonIdentifier SubID  : $02 recordCommonIdentifier SubID  : $06 recordCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERVO_VENTIL_ZUSTAND_WERT | int | akteuller ECO Ventil Zustand Wertebereich: ( 0..15 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SERVO_VENTIL_ZUSTAND_EINH | string | Einheit des akteullen ECO Ventil Zustands Einheit: ( ohne ) |
| STAT_SERVO_VENTIL_ZUSTAND_BIT0_TEXT | string | akteuller ECO Ventil Zustand moegliche Zustaende: ( Bit0 = '0' -- &gt; ECO Ventil in Ordnung ) moegliche Zustaende: ( Bit0 = '1' -- &gt; ECO Ventil fehlerhaft ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusECOVentil_Bit0 ) |
| STAT_SERVO_VENTIL_ZUSTAND_BIT1_TEXT | string | akteuller ECO Ventil Zustand moegliche Zustaende: ( Bit1 = '0' -- &gt; ECO Venitl verbaut ) moegliche Zustaende: ( Bit1 = '1' -- &gt; ECO Ventil nicht verbaut ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusECOVentil_Bit1 ) |
| STAT_SERVO_VENTIL_ZUSTAND_BIT3_TEXT | string | akteuller ECO Ventil Zustand moegliche Zustaende: ( Bit3 = '0' -- &gt; ECO Ventil verfuegbar ) moegliche Zustaende: ( Bit3 = '1' -- &gt; ECO Ventil nicht verfuegbar ) Wertebereich: ( 0, 1 ) Textausgabe ueber Tabelle: ( StatusECOVentil_Bit3 ) |
| STAT_SERVO_VENTIL_STROM_SOLL_WERT | real | gestellter Strom am Servo Ventil Wertebereich: ( 0...1000 mA ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_SERVO_VENTIL_STROM_SOLL_EINH | string | Einheit des Stromes Einheit: ( mA ) |
| STAT_SERVO_VENTIL_STROM_EINH | string | Einheit des Stromes Einheit: ( mA ) |
| STAT_SERVO_VENTIL_STEUERUNG_WERT | int | gibt an ob Strom fuer das ECO Ventil ueber Diagnose oder Modell gestellt wird Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0 -- &gt; nein, Modell ) moegliche Zustaende: ( 1 -- &gt; ja, Diagnose ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SERVO_VENTIL_STEUERUNG_EINH | string | Einheit der Strom-Vorgabe fuer das ECO-Ventil Einheit: ( ohne ) |
| STAT_SERVO_VENTIL_STEUERUNG_TEXT | string | gibt an ob Strom fuer das SERVO Ventil ueber Diagnose oder ASCET gestellt wird Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0 -- &gt; nein, Modell ) moegliche Zustaende: ( 1 -- &gt; ja, Diagnose ) Textausgabe ueber Tabelle: ( DigitalArgument ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-al-winkelwerte"></a>
### STATUS_AL_WINKELWERTE

Auslesen verschiedener Winkelwerte, wie Fahrerlenkwinkel, Summenlenkwinkel, Motorlagewinkel KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $23 Zustand des Werksmodus KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0F InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AL_INITMODE_WERT | int | aktueller Zustand der AL Initialisierung Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Werksmodus AL aus ) moegliche Zustaende: ( 1 -- &gt; Werksmodus AL ein ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AL_INITMODE_EINH | string | Einheit des aktueller Zustand der AL Initialisierung Einheit: ( hex ) |
| STAT_AL_INITMODE_TEXT | string | aktueller Zustand der AL Initialisierung moegliche Zustaende: ( 0 -- &gt; Werksmodus AL aus ) moegliche Zustaende: ( 1 -- &gt; Werksmodus AL ein ) Textausgabe ueber Tabelle: ( DigitalArgument ) |
| STAT_FAHRER_LENKWINKEL_RAD_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -25.132232 rad...25.132232 rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_FAHRER_LENKWINKEL_GRAD_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -1439.95Grad...1439.95Grad ) Einheit: ( Grad ) |
| STAT_GUELTIGKEIT_FAHRER_LENKWINKEL_WERT | int | Gueltigkeit des Fahrerlenkwinkels vom SZL, Filter 0x07 moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; nicht definiert ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_FAHRER_LENKWINKEL_EINH | string | Einheit der Comparatorempfindlichkeit Einheit: ( ohne ) |
| STAT_GUELTIGKEIT_FAHRER_LENKWINKEL_TEXT | string | Gueltigkeit des Fahrerlenkwinkels vom SZL, Filter 0x07 moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; nicht definiert ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Textausgabe ueber Tabelle: ( GueFLW ) |
| STAT_FAHRER_LENKWINKEL_GRAD_EINH | string | Einheit des Fahrerlenkwinkels Einheit: ( Grad ) |
| STAT_FAHRER_LENKWINKEL_RAD_EINH | string | Einheit des Fahrerlenkwinkels Einheit: ( rad ) |
| STAT_MOTORLAGEWINKEL_ABSOLUT_AL_RAD_ISTWERT | real | Motorlagewinkel Absoultistwert in Grad Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Wertebereich: ( ???? rad...???? rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MOTORLAGEWINKEL_ABSOLUT_AL_GRAD_ISTWERT | real | Motorlagewinkel Absoultistwert in Grad Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Wertebereich: ( ???? rad...???? rad ) Einheit: ( Grad ) |
| STAT_GUELTIGKEIT_MOTORLAGEWINKEL_ABSOLUT_AL_ISTWERT | int | Gueltigkeit Motorlagewinkel Absoultistwert moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 5 -- &gt; Timeout ) moegliche Zustaende: ( 6 -- &gt; ungueltig ) Wertebereich: ( 0,1,5,6 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_MOTORLAGEWINKEL_ABSOLUT_AL_ISTWERT_TEXT | string | Gueltigkeit Motorlagewinkel Absoultistwert moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 5 -- &gt; Timeout ) moegliche Zustaende: ( 6 -- &gt; ungueltig ) Wertebereich: ( 0,1,5,6 ) Textausgabe ueber Tabelle: ( GueALIstMLW ) |
| STAT_MOTORLAGEWINKEL_ABSOLUT_RAD_SOLLWERT | real | Motorlagewinkel Absoultsollwert in Grad Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( ???? rad...???? rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MOTORLAGEWINKEL_ABSOLUT_GRAD_SOLLWERT | real | Motorlagewinkel Absoultsollwert in Grad Wertebereich: ( ???? rad...???? rad ) Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Einheit: ( Grad ) |
| STAT_GUELTIGKEIT_MOTORLAGEWINKEL_ABSOLUT_SOLLWERT | int | Motorlagewinkel Absoultsollwert in Grad moegliche Zustaende: ( 32 -- &gt; Sollwert umsetzen ) moegliche Zustaende: ( 224 -- &gt; Sollwert nicht umsetzen ) moegliche Zustaende: ( 225 -- &gt; Rotorlage im AL gueltig setzen ) moegliche Zustaende: ( 226 -- &gt; Rotorlage im AL ungueltig setzen ) Wertebereich: ( 32,224,225,226 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_MOTORLAGEWINKEL_ABSOLUT_SOLLWERT_TEXT | string | Motorlagewinkel Absoultwert in Grad moegliche Zustaende: ( 32 -- &gt; Sollwert umsetzen ) moegliche Zustaende: ( 224 -- &gt; Sollwert nicht umsetzen ) moegliche Zustaende: ( 225 -- &gt; Rotorlage im AL gueltig setzen ) moegliche Zustaende: ( 226 -- &gt; Rotorlage im AL ungueltig setzen ) Wertebereich: ( 32,224,225,226 ) Textausgabe ueber Tabelle: ( GueALSollMLW ) |
| STAT_MOTORLAGEWINKEL_RAD_EINH | string | Einheit des Motorlagewinkels bezogen auf Grad Lenkrad Einheit: ( rad ) |
| STAT_MOTORLAGEWINKEL_GRAD_EINH | string | Einheit des Motorlagewinkels bezogen auf Grad Lenkrad Einheit: ( Grad ) |
| STAT_SUMMENLENKWINKELROH_RAD_WERT | real | SG intern berrechneter Summenlenkwinkelrohwert, virtueller Wert da KEIN Sensor vorhanden ist Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Wertebereich: ( -12,2173...+12,2173 ) Ungueltigkeitsbezeichnung: ( 8000 hex, -25,1327 rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_SUMMENLENKWINKELROH_GRAD_WERT | real | SG intern berrechneter Summenlenkwinkelrohwert, virtueller Wert da KEIN Sensor vorhanden ist Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Wertebereich: ( -700...+700 ) Ungueltigkeitsbezeichnung: ( 8000 hex, -1440 Grad ) Einheit: ( Grad ) |
| STAT_GUELTIGKEIT_SUMMENLENKWINKELROH_WERT | int | SG intern berrechneter Summenlenkwinkelrohwert, virtueller Wert da KEIN Sensor vorhanden ist, Filter 0x07 Gueltigkeit des Fahrerlenkwinkels vom SZL moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; nicht definiert ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_SUMMENLENKWINKELROH_EINH | string | Einheit: ( ohne ) |
| STAT_GUELTIGKEIT_SUMMENLENKWINKELROH_TEXT | string | SG intern berrechneter Summenlenkwinkelrohwert, virtueller Wert da KEIN Sensor vorhanden ist, Filter 0x07 Gueltigkeit des Fahrerlenkwinkels vom SZL moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; nicht definiert ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Textausgabe ueber Tabelle: ( GueSLWroh ) |
| STAT_SUMMENLENKWINKELROH_RAD_EINH | string | Einheit des Summenlenkwinkels bezogen auf Ritzel Einheit: ( rad Ritzel ) |
| STAT_SUMMENLENKWINKELROH_GRAD_EINH | string | Einheit des Summenlenkwinkels bezogen auf Ritzel Einheit: ( Grad Ritzel ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG_1 | binary | Hex Auftrag an SG |
| _TEL_ANTWORT_1 | binary | Hex - Antwort von SG |
| _TEL_DATEN_1 | binary | Hex - Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex - Antwort von SG |
| _TEL_DATEN_2 | binary | Hex - Antwort von SG |

<a id="job-start-al-mlw-ruecksetzen"></a>
### START_AL_MLW_RUECKSETZEN

Motorlagewinkel wird ungueltig gesetzt KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $21 Motorlagewinkel ungueltig setzen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AL_GUELTIGKEIT_MLW_WERT | int | Zustand der Gueltigkeit des AL Motorlagewinkels moegliche Zustaende: ( 1 -- &gt; MLW ruecksetzen erfolgreich ) moegliche Zustaende: ( 8x -- &gt; Anfrage konnte nicht ausgefuehrt werden ) Wertebereich: ( 1,129 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AL_GUELTIGKEIT_MLW_EINH | string | Einheit des aktuellen Zustands des Motorlagewinkels Einheit: ( ohne ) |
| STAT_AL_GUELTIGKEIT_MLW_BIT0_TEXT | string | Zustand der Gueltigkeit des AL Motorlagewinkels moegliche Zustaende: ( Bit0 = '0' -- &gt; MLW AL gueltig ) moegliche Zustaende: ( Bit0 = '1' -- &gt; MLW AL nicht gueltig ) Wertebereich: ( 0,1 ) Textausgabe ueber Tabelle: ( GueALMLW ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-start-al-mlwoffset-setzen"></a>
### START_AL_MLWOFFSET_SETZEN

intern berechneter Motorlagewinkeloffset wird gesepeichert KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $22 Speicherung des Motorlagewinkeloffset Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GUELTIGKEIT_AL_MLWOFFSET_WERT | int | Zustand der Gueltigkeit des AL Motorlagewinkels moegliche Zustaende: ( 1 -- &gt; MLW setzen erfolgreich ) moegliche Zustaende: ( 8x -- &gt; Anfrage konnte nicht ausgefuehrt werden ) Wertebereich: ( 1,129,130,131 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_AL_MLWOFFSET_EINH | string | Einheit des Zustand der Gueltigkeit des AL Motorlagewinkels Einheit: ( ohne ) |
| STAT_GUELTIGKEIT_AL_MLWOFFSET_BIT0_TEXT | string | Zustand der Gueltigkeit des AL Motorlagewinkels moegliche Zustaende: ( Bit0 = '0' -- &gt; im Werksmodus ) moegliche Zustaende: ( Bit0 = '1' -- &gt; nicht im Werksmodus ) Wertebereich: ( 0,1 ) Textausgabe ueber Tabelle: ( GueALMLWOffset ) |
| STAT_GUELTIGKEIT_AL_MLWOFFSET_BIT1_TEXT | string | Zustand der Gueltigkeit des AL Motorlagewinkels moegliche Zustaende: ( Bit1 = '0' -- &gt; MLW AL nicht gueltig ) moegliche Zustaende: ( Bit1 = '1' -- &gt; MLW AL gueltig ) Wertebereich: ( 0,1 ) Textausgabe ueber Tabelle: ( GueALMLWOffset ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-steuern-al-initmode"></a>
### STEUERN_AL_INITMODE

AktivLenkung wird in den Werksmodus versetzt KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $23 Speicherung des Motorlagewinkeloffset Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AL_INITMODE_WERT | int | zu setzender Werksmodus moegliche Zustaende: ( 0 -- &gt; Werksmodus AL aus ) moegliche Zustaende: ( 1 -- &gt; Werksmodus AL ein ) Wertebereich: ( 0..1 ) Telegrammlaenge KWP: ( 1 Byte ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-al-initmode"></a>
### STATUS_AL_INITMODE

aktueller Zustand ob AL im Werksmodus ist KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $23 Zustand des Werksmodus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AL_INITMODE_WERT | int | aktueller Zustand der AL Initialisierung Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Werksmodus AL aus ) moegliche Zustaende: ( 1 -- &gt; Werksmodus AL ein ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AL_INITMODE_EINH | string | Einheit des aktueller Zustand der AL Initialisierung Einheit: ( hex ) |
| STAT_AL_INITMODE_TEXT | string | aktueller Zustand der AL Initialisierung moegliche Zustaende: ( 0 -- &gt; Werksmodus AL aus ) moegliche Zustaende: ( 1 -- &gt; Werksmodus AL ein ) Textausgabe ueber Tabelle: ( DigitalArgument ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-al-mlw-init"></a>
### STATUS_AL_MLW_INIT

Gueltigkeit des Motorlagewinkels AL auslesen KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $20 Inbetriebnahme Resultat abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AL_GUELTIGKEIT_MLW_WERT | int | aktueller Zustand des Motorlagewinkels moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 5 -- &gt; Timeout ) moegliche Zustaende: ( 6 -- &gt; ungueltig ) Wertebereich: ( 0,1,5,6 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AL_GUELTIGKEIT_MLW_EINH | string | Einheit des aktuellen Zustands des Motorlagewinkels Einheit: ( ohne ) |
| STAT_AL_GUELTIGKEIT_MLW_TEXT | string | aktueller Zustand des Motorlagewinkels moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 5 -- &gt; Timeout ) moegliche Zustaende: ( 6 -- &gt; ungueltig ) Wertebereich: ( 0,1,5,6 ) Textausgabe ueber Tabelle: ( GueALMLWZustand ) |
| STAT_AL_GUELTIGKEIT_MLW_INITMODE_WERT | int | aktueller Zustand des Motorlagewinkels moegliche Zustaende: ( 0 -- &gt; nicht gelernt ) moegliche Zustaende: ( 1 -- &gt; gelernt ) Wertebereich: ( 0,1 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AL_GUELTIGKEIT_MLW_INITMODE_EINH | string | Einheit des aktuellen Zustands des Motorlagewinkels Einheit: ( ohne ) |
| STAT_AL_GUELTIGKEIT_MLW_INITMODE_TEXT | string | aktueller Zustand des Motorlagewinkels moegliche Zustaende: ( 0 -- &gt; nicht gelernt ) moegliche Zustaende: ( 1 -- &gt; gelernt ) Wertebereich: ( 0,1 ) Textausgabe ueber Tabelle: ( GueALMLWInit ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-al-mlwoffset-setzen"></a>
### STATUS_AL_MLWOFFSET_SETZEN

Status AL MLW Offset KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $22 Gueltigkeit AL Motorlagewinkeloffset Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MLW_ANSCH_ANSCH_WERT | real | aktueller Status des Motorlagewinkeloffset Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Wertebereich: ( -700...700 ) Einheit: ( Grad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MLW_ANSCH_ANSCH_EINH | string | Einheit des aktuellen Status des Motorlagewinkeloffset Einheit: ( ohne ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-al-icm-verbund"></a>
### STATUS_AL_ICM_VERBUND

Status AktivLenkung beim ICM KWP2000: $22 ReadDataByCommonIdentifier SubID  : $00 recordCommonIdentifier(RCI_) SubID  : $01 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORLAGEWINKEL_ISTWERT_AL_RAD_WERT | real | Motorlagewinkel Absoultistwert in rad Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Wertebereich: ( -25.132232 rad...25.132232 rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MOTORLAGEWINKEL_ISTWERT_AL_RAD_EINH | string | Einheit des Motorlagewinkel Absoultistwert in rad Einheit: ( rad ) |
| STAT_MOTORLAGEWINKEL_ISTWERT_AL_GRAD_WERT | real | Motorlagewinkel Absoultistwert in Grad Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Wertebereich: ( -1440 grad...+1440 grad ) Einheit: ( Grad ) |
| STAT_MOTORLAGEWINKEL_ISTWERT_AL_GRAD_EINH | string | Einheit des Motorlagewinkel Absoultistwert in Grad Einheit: ( rad ) |
| STAT_MOTORLAGEWINKEL_ISTWERT_AL_QUALIFIER_WERT | int | Qualifier MLW Istwert moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; Signal zu oft entprellt ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MOTORLAGEWINKEL_ISTWERT_AL_QUALIFIER_EINH | string | Einheit des Qualifier MLW Istwert Einheit: ( ohne ) |
| STAT_MOTORLAGEWINKEL_ISTWERT_AL_QUALIFIER_TEXT | string | Qualifier MLW Istwert moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; Signal zu oft entprellt ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Textausgabe ueber Tabelle: ( ALMLWIstQualifier ) |
| STAT_AL_SERVICEQUALIFIER_WERT | int | Servivequalifier AL moegliche Zustaende: ( 128 -- &gt; Initialisierung ) moegliche Zustaende: ( 33 -- &gt; Drive Standby ) moegliche Zustaende: ( 34 -- &gt; Drive ) moegliche Zustaende: ( 49 -- &gt; Drive Standby, USW1  ) moegliche Zustaende: ( 53 -- &gt; Drive Standby, USW2  ) moegliche Zustaende: ( 57 -- &gt; Drive Standby, USW3  ) moegliche Zustaende: ( 54 -- &gt; Drive, USW1  ) moegliche Zustaende: ( 50 -- &gt; Drive, USW2  ) moegliche Zustaende: ( 58 -- &gt; Drive, USW3  ) moegliche Zustaende: ( 224 -- &gt; Postrun ) moegliche Zustaende: ( 225 -- &gt; ReadyforDrive ) moegliche Zustaende: ( 227 -- &gt; Drive_RampZero ) moegliche Zustaende: ( 228 -- &gt; WaitForRLWSet ) moegliche Zustaende: ( 233 -- &gt; ReadyForDrive Unterspannung ) moegliche Zustaende: ( 235 -- &gt; Drive_RampZero Unterspannung ) moegliche Zustaende: ( 104 -- &gt; Error ) moegliche Zustaende: ( 255 -- &gt; Invalid ) Wertebereich: ( 128,33,44,49,53,57,54,50,58,224,225,227,228,233,235,104,255 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AL_SERVICEQUALIFIER_EINH | string | Einheit des Servivequalifier AL Einheit: ( ohne ) |
| STAT_AL_SERVICEQUALIFIER_TEXT | string | Servivequalifier AL moegliche Zustaende: ( 128 -- &gt; Initialisierung ) moegliche Zustaende: ( 33 -- &gt; Drive Standby ) moegliche Zustaende: ( 34 -- &gt; Drive ) moegliche Zustaende: ( 49 -- &gt; Drive Standby, USW1  ) moegliche Zustaende: ( 53 -- &gt; Drive Standby, USW2  ) moegliche Zustaende: ( 57 -- &gt; Drive Standby, USW3  ) moegliche Zustaende: ( 54 -- &gt; Drive, USW1  ) moegliche Zustaende: ( 50 -- &gt; Drive, USW2  ) moegliche Zustaende: ( 58 -- &gt; Drive, USW3  ) moegliche Zustaende: ( 224 -- &gt; Postrun ) moegliche Zustaende: ( 225 -- &gt; ReadyforDrive ) moegliche Zustaende: ( 227 -- &gt; Drive_RampZero ) moegliche Zustaende: ( 228 -- &gt; WaitForRLWSet ) moegliche Zustaende: ( 233 -- &gt; ReadyForDrive Unterspannung ) moegliche Zustaende: ( 235 -- &gt; Drive_RampZero Unterspannung ) moegliche Zustaende: ( 104 -- &gt; Error ) moegliche Zustaende: ( 255 -- &gt; Invalid ) Wertebereich: ( 128,33,44,49,53,57,54,50,58,224,225,227,228,233,235,104,255 ) Textausgabe ueber Tabelle: ( ALMLWServiceQualifier ) |
| STAT_AL_SERVICEQUALIFIER_QUALIFIER_WERT | int | Qualifier MLW Istwert moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; Signal zu oft entprellt ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AL_SERVICEQUALIFIER_QUALIFIER_EINH | string | Einheit des Qualifier MLW Istwert Einheit: ( ohne ) |
| STAT_AL_SERVICEQUALIFIER_QUALIFIER_TEXT | string | Qualifier MLW Istwert moegliche Zustaende: ( 0 -- &gt; Initialisierung ) moegliche Zustaende: ( 1 -- &gt; Signalwert ist gueltig und abgesichert ) moegliche Zustaende: ( 2 -- &gt; Signal ist gueltig ) moegliche Zustaende: ( 3 -- &gt; Signal ist nicht vertrauenswuerdig ) moegliche Zustaende: ( 4 -- &gt; Ersatzwert ist im Nutzsignal gesetzt ) moegliche Zustaende: ( 5 -- &gt; Signal zu oft entprellt ) moegliche Zustaende: ( 6 -- &gt; Signalwert ist ungueltig ) moegliche Zustaende: ( 7 -- &gt; Sensor nicht vorhanden oder Signal ungueltig ) Wertebereich: ( 0,1,2,3,4,5,6,7 ) Textausgabe ueber Tabelle: ( ALMLWIstQualifier ) |
| STAT_MOTORLAGEWINKEL_SOLLWERT_AL_RAD_WERT | real | Motorlagewinkel Absoultistwert in rad Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Wertebereich: ( -25.132232 rad...25.132232 rad ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MOTORLAGEWINKEL_SOLLWERT_AL_RAD_EINH | string | Einheit des Motorlagewinkel Absoultistwert in rad Einheit: ( rad ) |
| STAT_MOTORLAGEWINKEL_SOLLWERT_AL_GRAD_WERT | real | Motorlagewinkel Absoultistwert in Grad Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Wertebereich: ( -1440 grad...+1440 grad ) Einheit: ( Grad ) |
| STAT_MOTORLAGEWINKEL_SOLLWERT_AL_GRAD_EINH | string | Einheit des Motorlagewinkel Absoultistwert in Grad Einheit: ( Grad ) |
| STAT_AL_SOLLWERTQUALIFIER_WERT | int | Qualifier MLW Istwert moegliche Zustaende: ( 128 -- &gt; Initialisierung ) moegliche Zustaende: ( 32 -- &gt; Sollwert umsetzen ) moegliche Zustaende: ( 224 -- &gt; Sollwert nicht umsetzen ) moegliche Zustaende: ( 225 -- &gt; Set RLW valid ) moegliche Zustaende: ( 226 -- &gt; Set RLW invalid ) moegliche Zustaende: ( 96 -- &gt; Fehler ) moegliche Zustaende: ( 112 -- &gt; Sollwert nicht vorhanden ) moegliche Zustaende: ( 255 -- &gt; Signal ungueltig ) Wertebereich: ( 128,32,224,225,96,112,255 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AL_SOLLWERTQUALIFIER_EINH | string | Einheit des Qualifier MLW Istwert Einheit: ( ohne ) |
| STAT_AL_SOLLWERTQUALIFIER_TEXT | string | Qualifier MLW Istwert moegliche Zustaende: ( 128 -- &gt; Initialisierung ) moegliche Zustaende: ( 32 -- &gt; Sollwert umsetzen ) moegliche Zustaende: ( 224 -- &gt; Sollwert nicht umsetzen ) moegliche Zustaende: ( 225 -- &gt; Set RLW valid ) moegliche Zustaende: ( 226 -- &gt; Set RLW invalid ) moegliche Zustaende: ( 96 -- &gt; Fehler ) moegliche Zustaende: ( 112 -- &gt; Sollwert nicht vorhanden ) moegliche Zustaende: ( 255 -- &gt; Signal ungueltig ) Wertebereich: ( 128,32,224,225,96,112,255 ) Textausgabe ueber Tabelle: ( ALMLWSollQualifier ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-al-checkcontrol"></a>
### STATUS_AL_CHECKCONTROL

Checkcontrol Meldungen der Aktivlenkung KWP2000: $22 ReadDataByCommonIdentifier SubID  : $01 recordCommonIdentifier(RCI_) SubID  : $11 recordCommonIdentifier(RCI_) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AL_CCMELDUNG_WERT | int | Checkcontrol Meldung von AL moegliche Zustaende: ( 0 -- &gt; Aktivlenkung i.O. ) moegliche Zustaende: ( 1 -- &gt; Aktivlenkung ausgefallen ) moegliche Zustaende: ( 2 -- &gt; Aktivlenkung gestoert ) Wertebereich: ( 0,1,2 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AL_CCMELDUNG_EINH | string | Einheit des Status der Checkcontrol Meldung von AL Einheit: ( ohne ) |
| STAT_AL_CCMELDUNG_TEXT | string | Checkcontrol Meldung von AL moegliche Zustaende: ( 0 -- &gt; Aktivlenkung i.O. ) moegliche Zustaende: ( 1 -- &gt; Aktivlenkung ausgefallen ) moegliche Zustaende: ( 2 -- &gt; Aktivlenkung gestoert ) Wertebereich: ( 0,1,2 ) Textausgabe ueber Tabelle: ( ALCCMeldung ) |
| STAT_AL_ERROR_WERT | int | Fehlernummer AL Wertebereich: ( 0,....17 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_AL_ERROR_EINH | string | Einheit der Fehlernummer AL Einheit: ( ohne ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-steuern-al-spannungsversorgung"></a>
### STEUERN_AL_SPANNUNGSVERSORGUNG

AL Spannungsversorgung ein/ausschalten KWP2000: $2E WriteDataByCommonIdentifier SubID  : $F0 recordCommonIdentifier SubID  : $15 recordCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AL_SPANNUNGSVERSORGUNG_WERT | int | Wertebereich: ( 0..1 ) moegliche Zustaende: (  0 -- &gt; aus ) moegliche Zustaende: (  1 -- &gt; ein ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AL_SPANNUNGSVERSORGUNG_WERT | int | Wertebereich: ( 0..1 ) moegliche Zustaende: (  0 -- &gt; aus ) moegliche Zustaende: (  1 -- &gt; ein ) |
| STAT_AL_SPANNUNGSVERSORGUNG_EINH | string | Einheit des Status der Spannungsversorgung Einheit: ( ohne ) |
| STAT_AL_SPANNUNGSVERSORGUNG_TEXT | string | Wertebereich: ( 0..1 ) moegliche Zustaende: (  0 -- &gt; aus ) moegliche Zustaende: (  1 -- &gt; ein ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-fn-al"></a>
### STATUS_FN_AL

STATUS_FN_AL KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $56 Funktion AL analysieren Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VORSTEUERANTEIL_ASA | real | Vorsteueranteil in RAD Wertebereich: ( -??...?? ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_REGLERANTEIL_ASA | real | Regleranteil in RAD Wertebereich: ( -??...?? ) Einheit: ( rad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_UMSETZUNG_VORSTEUERWERT_FAMPDYN_TEXT | string | Umsetzung des Vorsteuerwerts Wertebereich: ( 0..1 ) moegliche Zustaende: (  0 -- &gt; Vorsteuerwert wird nicht umgesetzt) moegliche Zustaende: (  1 -- &gt; Vorsteuerwert wird umgesetzt) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_UMSETZUNG_VORSTEUERWERT_DYN_TEXT | string | Umsetzung des Vorsteuerwerts Wertebereich: ( 0..1 ) moegliche Zustaende: (  0 -- &gt; Vorsteuerwert wird nicht umgesetzt) moegliche Zustaende: (  1 -- &gt; Vorsteuerwert wird umgesetzt) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_VORSTEUERUNG_ASA_TEXT | string | ASA Vorsteuerstatus Wertebereich: ( 0..3 ) moegliche Zustaende: (  0 -- &gt; Vorsteuerung ist passiv) moegliche Zustaende: (  1 -- &gt; Vorsteuerung ist bereit passiv) moegliche Zustaende: (  2 -- &gt; Vorsteuerung ist bereit aktiv) moegliche Zustaende: (  3 -- &gt; Vorsteuerung ist aktiv) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_REGLER_ASA_TEXT | string | ASA Reglerstatus Wertebereich: ( 0..3 ) moegliche Zustaende: (  0 -- &gt; Regler-ASA ist passiv) moegliche Zustaende: (  1 -- &gt; Regler-ASA ist bereit passiv) moegliche Zustaende: (  2 -- &gt; Regler-ASA ist bereit aktiv) moegliche Zustaende: (  3 -- &gt; Regler-ASA ist aktiv) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GRRPLUS_ASA_TEXT | string | Umsetzung des Vorsteuerwerts Wertebereich: ( 0..3 ) moegliche Zustaende: (  0 -- &gt; Regler-GRRplus-ASA ist passiv) moegliche Zustaende: (  1 -- &gt; Regler-GRRplus-ASA ist bereit passiv) moegliche Zustaende: (  2 -- &gt; Regler-GRRplus-ASA ist bereit aktiv) moegliche Zustaende: (  3 -- &gt; Regler-GRRplus-ASA ist aktiv) Telegrammlaenge KWP: ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-start-modus-rollenpruefstand"></a>
### START_MODUS_ROLLENPRUEFSTAND

versetzt das ICM Steuergerät in einen Rollenprüfstandsmodus Geschwindigkeit entspricht HA-Geschwindigkeit, Regler passiv KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $54 routineLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MODUS_ROLLENPRUEFSTAND_WERT | char | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MODUS_ROLLENPRUEFSTAND_EINH | string | Einheit des Zustands des Rollenpruefstandswerts Einheit: ( ohne ) |
| STAT_MODUS_ROLLENPRUEFSTAND_TEXT | string | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Textausgabe ueber Tabelle: ( JobInterpretation ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-stop-modus-rollenpruefstand"></a>
### STOP_MODUS_ROLLENPRUEFSTAND

dieser Job beendet den Rollenpruefstandsmodus des ICM-Steuergeraets KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $55 routineLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MODUS_ROLLENPRUEFSTAND_WERT | char | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MODUS_ROLLENPRUEFSTAND_EINH | string | Einheit des Zustands des Rollenpruefstandswerts Einheit: ( ohne ) |
| STAT_MODUS_ROLLENPRUEFSTAND_TEXT | string | Zustand Abgleich moegliche Zustaende: ( 0 -- &gt; Job noch nicht gelaufen oder nicht abgeschlossen ) moegliche Zustaende: ( 1 -- &gt; Jobergebnis i.O. ) moegliche Zustaende: ( -1 -- &gt; Jobergebnis fehlerhaft ) Wertebereich: ( -1, 0, 1 ) Textausgabe ueber Tabelle: ( JobInterpretation ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-rollenpruefstand"></a>
### STATUS_ROLLENPRUEFSTAND

dieser Job liefert den Status des Rollenprüfstandsmodus KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $54 routineLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MODUS_ROLLENPRUEFSTAND_WERT | int | Startergebnis Wertebereich: ( 0,1 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MODUS_ROLLENPRUEFSTAND_EINH | string | Einheit des Zustands des Rollenpruefstandswerts Einheit: ( ohne ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (111 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (116 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (38 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (62 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (129 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (78 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (62 × 9)
- [GUEALMLW](#table-guealmlw) (3 × 2)
- [SZLPROZINFO](#table-szlprozinfo) (3 × 2)
- [SZLABGLEICHINFO](#table-szlabgleichinfo) (5 × 2)
- [GUEFLW](#table-gueflw) (9 × 2)
- [GUEALISTMLW](#table-guealistmlw) (5 × 2)
- [GUEALSOLLMLW](#table-guealsollmlw) (5 × 2)
- [GUESLWROH](#table-gueslwroh) (9 × 2)
- [GUEALMLWZUSTAND](#table-guealmlwzustand) (5 × 2)
- [GUEALMLWINIT](#table-guealmlwinit) (3 × 2)
- [ZFM_QES_FSQUAL](#table-zfm-qes-fsqual) (9 × 2)
- [ZFM_QIS_NSQ](#table-zfm-qis-nsq) (9 × 2)
- [ZFM_ZEF_ZST](#table-zfm-zef-zst) (6 × 2)
- [ZFM_ZIF_ZS](#table-zfm-zif-zs) (5 × 2)
- [ZFM_AKT_ZST](#table-zfm-akt-zst) (6 × 2)
- [STATUSECOVENTIL](#table-statusecoventil) (9 × 2)
- [STATUSSERVOVENTIL](#table-statusservoventil) (9 × 2)
- [ALMLWISTQUALIFIER](#table-almlwistqualifier) (9 × 2)
- [ALMLWSERVICEQUALIFIER](#table-almlwservicequalifier) (17 × 2)
- [ALMLWSOLLQUALIFIER](#table-almlwsollqualifier) (8 × 2)
- [SGSTATI](#table-sgstati) (10 × 2)
- [GUEALMLWOFFSET](#table-guealmlwoffset) (5 × 2)
- [JOBINTERPRETATION](#table-jobinterpretation) (4 × 2)
- [SGSTATUS](#table-sgstatus) (3 × 2)
- [FAHRGESTELLNRSTATUS](#table-fahrgestellnrstatus) (4 × 2)
- [DIVCALCSTATUS](#table-divcalcstatus) (3 × 2)
- [STATUSECOVENTIL_BIT0](#table-statusecoventil-bit0) (3 × 2)
- [STATUSECOVENTIL_BIT1](#table-statusecoventil-bit1) (3 × 2)
- [STATUSECOVENTIL_BIT3](#table-statusecoventil-bit3) (3 × 2)
- [STATUSSERVOVENTIL_BIT0](#table-statusservoventil-bit0) (3 × 2)
- [STATUSSERVOVENTIL_BIT1](#table-statusservoventil-bit1) (3 × 2)
- [STATUSSERVOVENTIL_BIT3](#table-statusservoventil-bit3) (3 × 2)
- [ALCCMELDUNG](#table-alccmeldung) (4 × 2)
- [SZLGUEFLWROH](#table-szlgueflwroh) (5 × 2)
- [ALVSTDYN](#table-alvstdyn) (3 × 2)
- [ALVSTSTAT](#table-alvststat) (5 × 2)
- [ALREGLERSTAT](#table-alreglerstat) (5 × 2)
- [ALREGLERGRRPLUSSTAT](#table-alreglergrrplusstat) (5 × 2)
- [UWB_A](#table-uwb-a) (1 × 9)
- [UWB_B](#table-uwb-b) (1 × 4)
- [UWB_C](#table-uwb-c) (1 × 7)
- [UWB_D](#table-uwb-d) (1 × 12)
- [UWB_E](#table-uwb-e) (1 × 7)
- [UWB_F](#table-uwb-f) (1 × 7)
- [UWB_G](#table-uwb-g) (1 × 7)
- [UWB_H](#table-uwb-h) (1 × 7)
- [UWB_I](#table-uwb-i) (1 × 5)
- [UWB_J](#table-uwb-j) (1 × 7)
- [UWB_K](#table-uwb-k) (1 × 7)
- [UWB_L](#table-uwb-l) (1 × 6)
- [UWB_M](#table-uwb-m) (1 × 13)
- [UWB_N](#table-uwb-n) (1 × 13)

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

Dimensions: 111 rows × 2 columns

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

Dimensions: 116 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x640C | allgemeiner Steuergeräte Hardware Fehler |
| 0x640D | Fahrgestellnummer Vergleich |
| 0x640E | Codierdaten Fehler |
| 0x640F | Boot oder Flash Fehler |
| 0x6410 | Leitung AL Kurzschluss oder Unterbrechung |
| 0x6411 | Sicherheitsabschaltung Diversitaeres Rechnen |
| 0x6412 | Betriebssystem Eigen-Diagnose |
| 0x6413 | EVV sporadischer Fehler |
| 0x6414 | Servo sporadischer Fehler |
| 0x6415 | Werksmodus AL ist aktiv |
| 0x6416 | allgemeiner Steuergeräte Softwareware Fehler |
| 0x6417 | Modus fuer Rollenprüfstand aktiv |
| 0x641A | Unterspannung Klemme 30 (&lt; 9 Volt) |
| 0x641B | Ueberspannung Klemme 30 (&gt;16 Volt) |
| 0x641C | Diversitaeres Rechnen CRC-Fehler |
| 0x641D | Sensor-Abgleiche nicht durchgeführt |
| 0x6421 | Signalsammelfehler Sender AL |
| 0x6422 | Signalfehler in der Botschaft (ST_LTRQD_BAX_ACT, ID=13E) von QSG ICM-CAN |
| 0x6423 | Signalsammelfehler Sensorcluster |
| 0x6424 | Signalfehler in der Botschaft (Lenkradwinkel Oben 2, ID=C9) von SZL F-CAN |
| 0x6425 | Signalsammelfehler Sender DME |
| 0x6426 | Signalfehler in der Botschaft (Status Anhaenger, ID=2E4) von AHM PT-CAN |
| 0x6427 | Signalsammelfehler Sender CAS |
| 0x6428 | Signalfehler in der Botschaft (Status Sollmomentumsetzung, ID=BC) von VGSG PT-CAN |
| 0x6429 | Signalfehler in der Botschaft (Drehmoment 1, ID=0A8) von DME PT-CAN |
| 0x642A | Signalfehler in der Botschaft (Drehmoment 3, ID=0AA) von DME PT-CAN |
| 0x642B | Signalfehler in der Botschaft (Motordaten, ID=1D0) von DME PT-CAN |
| 0x642C | Signalfehler in der Botschaft (Status DSC PT-CAN, ID=19E) von EHB3 PT-CAN |
| 0x642D | Signalfehler in der Botschaft (Raddruecke PT-CAN, ID=2B2) von EHB3 PT-CAN |
| 0x642E | Signalfehler in der Botschaft (Klemmenstatus, ID=130) von CAS PT-CAN |
| 0x642F | Sensorcluster Typ unbekannt |
| 0x6430 | Signalfehler in der Botschaft (Fahrgestellnummer, ID=380) von CAS PT-CAN |
| 0x6431 | Signalfehler in der Botschaft (Status Lenkung Vorderachse Stellglied, ID=13D) von ASA ICM-CAN |
| 0x6432 | Signalfehler in der Botschaft (Status Lenkung Vorderachse Stellglied Erweitert, ID=13F) von ASA ICM-CAN |
| 0x6433 | Signalfehler in der Botschaft (Radgeschwindigkeiten, ID=0CE) von EHB3 F-CAN |
| 0x6434 | Signalfehler in der Botschaft (Regeleingriffe DSC, ID=11E) von EHB3 F-CAN |
| 0x6435 | Signalfehler in der Botschaft (Austausch DSC, ID=12D) von EHB3 F-CAN |
| 0x6436 | Signalfehler in der Botschaft (CLU1 VDA, ID=0D8) von SC_VDA F-CAN |
| 0x6437 | Signalfehler in der Botschaft (CLU2 VDA, ID=0E3) von SC_VDA F-CAN |
| 0x6438 | Signalfehler in der Botschaft (CLU3 VDA, ID=0F4) von SC_VDA F-CAN |
| 0x6439 | Signalfehler in der Botschaft (CLU Status VDA, ID=165) von SC_VDA F-CAN |
| 0x643A | Signalfehler in der Botschaft (Status ARS Modul, ID=1AC) von ARS PT-CAN |
| 0x643B | EVV Unterbrechung Schaltkreis |
| 0x643C | EVV Kurzschluss Masse gegen Low Side |
| 0x643D | EVV Kurzschluss Klemme 30 gegen Low Side |
| 0x643E | EVV Kurzschluss Masse gegen High Side |
| 0x6440 | EVV Kurzschluss Klemme 30 gegen High Side |
| 0x6441 | EVV Kurzschluss Spulenwindung |
| 0x6442 | EVV nicht lokalisierbarer Kurzschluss gegen Masse |
| 0x6443 | EVV nicht lokalisierbarer Kurzschluss gegen Klemme 30 |
| 0x6444 | Servo Unterbrechung Schaltkreis |
| 0x6445 | Servo Kurzschluss Masse gegen Low Side |
| 0x6446 | Servo Kurzschluss Klemme 30 gegen Low Side |
| 0x6447 | Servo Kurzschluss Masse gegen High Side |
| 0x6448 | Servo Kurzschluss Klemme 30 gegen High Side |
| 0x6449 | Servo Kurzschluss Spulenwindung |
| 0x644A | Servo nicht lokalisierbarer Kurzschluss gegen Masse |
| 0x644B | Servo nicht lokalisierbarer Kurzschluss gegen Klemme 30 |
| 0x644C | Motorlagewinkel AL ungueltig |
| 0x644D | AL inaktiv und Fahrzeug rollt |
| 0x644E | AL im Pausemodus und Fahrzeug rollt (Motor abgewuergt, Unterspannung, …) |
| 0x644F | AL im Errormodus |
| 0x6450 | AL im undefinierten Statemaschine Zustand (haengt im Init, Postrun fest) |
| 0x6451 | AL im Werksmodus |
| 0x6452 | SZL neu abgeglichen |
| 0x6453 | SZL neu verbaut |
| 0x6454 | AL gestoert: schnelle Lenkwinkelsynchronisation |
| 0x6455 | AL gestoert: langsame Lenkwinkelsynchronisation |
| 0x6456 | AL gestoert: AGB (verfuegbare Dynamik zu gering, Fehleramplitude zu gross) |
| 0x6457 | Signal ZfmFs_r_vx nicht nutzbar (fsqual nicht in Ordnung) |
| 0x6458 | Signal ZfmFs_i_engine_run nicht nutzbar (fsqual nicht in Ordnung) |
| 0x6459 | Signal ZfmFs_i_ASA_sq nicht nutzbar (fsqual nicht in Ordnung) |
| 0x645A | Signal ZfmFs_r_lwVA_akt_max_dyn nicht nutzbar (fsqual nicht in Ordnung) |
| 0x645B | AL kann nicht in aktiven Modus wechseln |
| 0x645C | Signalfehler in der Botschaft (Sensor Daten ROSE, ID=12A) von ACSM_ROSE F-CAN |
| 0x645D | Codierdaten Checksummenfehler |
| 0x645E | falsch codierte AL |
| 0x645F | AL Grenze fuer Lenkwinkelendanschlag ueberschritten |
| 0x6460 | SZL in Initialisierungsphase |
| 0x6461 | Signalueberwachung der Sensorclustersignale hat angeschlagen |
| 0x6462 | Signalueberwachung der Lenkwinkelsignale hat angeschlagen |
| 0x6463 | Fehler in Codierdaten. System im Errormode |
| 0x6464 | AY-Check Threshold war oder ist aktiv |
| 0xD007 | F-CAN Kommunikationsfehler |
| 0xD008 | F-CAN physikalisch gestoert |
| 0xD00B | PT-CAN Kommunikationsfehler |
| 0xD00C | PT-CAN physikalisch gestoert |
| 0xD00E | ICM-CAN physikalisch gestoert |
| 0xD00F | ICM-CAN Kommunikationsfehler |
| 0xD010 | Botschaft (Lenkradwinkel oben, ID=0C9) von SZL F-CAN |
| 0xD011 | Botschaft (Radgeschwindigkeiten, ID=0CE) von EHB3 F-CAN |
| 0xD012 | Botschaft (CLU1 VDA, ID=0D8) von SC_VDA F-CAN |
| 0xD013 | Botschaft (CLU2 VDA, ID=0E3) von SC_VDA F-CAN |
| 0xD014 | Botschaft (CLU3 VDA, ID=0F4) von SC_VDA F-CAN |
| 0xD015 | Botschaft (Regeleingriffe DSC AFS, ID=11E) von EHB3 F-CAN |
| 0xD016 | Botschaft (Austausch DSC ICM, ID=12D) von EHB3 F-CAN |
| 0xD017 | Botschaft (Klemmenstatus, ID=130) von CAS F-CAN |
| 0xD018 | Botschaft (CLU Status VDA, ID=165) von SC_VDA F-CAN |
| 0xD019 | Botschaft (Sensor Daten ROSE, ID=12A) von ACSM_ROSE F-CAN |
| 0xD020 | Botschaft (Drehmoment 1, ID=0A8) von DME PT-CAN |
| 0xD021 | Botschaft (Drehmoment 3, ID=0AA) von DME PT-CAN |
| 0xD022 | Botschaft (Getriebedaten, ID=0BA) von EGS_EL PT-CAN |
| 0xD023 | Botschaft (Status Sollmomentumsetzung, ID=0BC) von VGSG PT-CAN |
| 0xD024 | Botschaft (Klemmenstatus, ID=130) von CAS PT-CAN |
| 0xD025 | Botschaft (Status DSC PT-CAN, ID=19E) von EHB3 PT-CAN |
| 0xD026 | Botschaft (Status ARS Modul ID=1AC) von ARS PT-CAN |
| 0xD027 | Botschaft (Motordaten, ID=1D0) von DME PT-CAN |
| 0xD028 | Botschaft (Raddruecke PT-CAN, ID=2B2) von EHB3 PT-CAN |
| 0xD029 | Botschaft (Status Anhaenger, ID=2E4) von AHM PT-CAN |
| 0xD02A | Botschaft (Kilometerstand, ID=330) von Kombi PT-CAN |
| 0xD02B | Botschaft (Fahrgestellnummer, ID=380) von CAS PT-CAN |
| 0xD030 | Botschaft (Status Lenkung Vorderachse Stellglied, ID=13D) von ASA ICM-CAN |
| 0xD031 | Botschaft (Status Quermomentenverteilung Hinterachse Stellglied, ID=13E) von QSG PT-CAN |
| 0xD032 | Botschaft (Status Lenkung Vorderachse Stellglied Erweitert, ID=13F) von ASA PT-CAN |
| 0xD033 | Botschaft (Entwicklungsdaten ID=7C8) von QSG ICM-CAN |
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

Dimensions: 38 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x640C | UWB_C | - | - | - |
| 0x640D | UWB_B | - | - | - |
| 0x640E | UWB_B | - | - | - |
| 0x640F | UWB_C | - | - | - |
| 0x6410 | UWB_B | - | - | - |
| 0x6411 | UWB_C | - | - | - |
| 0x6412 | UWB_D | - | - | - |
| 0x6413 | UWB_B | - | - | - |
| 0x6414 | UWB_B | - | - | - |
| 0x6416 | UWB_C | - | - | - |
| 0x641A | UWB_B | - | - | - |
| 0x641B | UWB_B | - | - | - |
| 0x641C | UWB_B | - | - | - |
| 0x641D | UWB_B | - | - | - |
| 0x642F | UWB_B | - | - | - |
| 0x643B | UWB_B | - | - | - |
| 0x643C | UWB_B | - | - | - |
| 0x643D | UWB_B | - | - | - |
| 0x643E | UWB_B | - | - | - |
| 0x6440 | UWB_B | - | - | - |
| 0x6441 | UWB_B | - | - | - |
| 0x6442 | UWB_B | - | - | - |
| 0x6443 | UWB_B | - | - | - |
| 0x6444 | UWB_B | - | - | - |
| 0x6445 | UWB_B | - | - | - |
| 0x6446 | UWB_B | - | - | - |
| 0x6447 | UWB_B | - | - | - |
| 0x6448 | UWB_B | - | - | - |
| 0x6449 | UWB_B | - | - | - |
| 0x644A | UWB_B | - | - | - |
| 0x644B | UWB_B | - | - | - |
| 0x645D | UWB_B | - | - | - |
| 0x645E | UWB_B | - | - | - |
| 0x645F | UWB_B | - | - | - |
| 0x6460 | UWB_B | - | - | - |
| 0x6463 | UWB_B | - | - | - |
| 0x6464 | UWB_B | - | - | - |
| default | UWB_A | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 62 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Zeitstempel, absolute Zeit in ms | ms | - | signed long | - | 10 | 1 | 0 |
| 0x02 | Fehler Detail, zuletzt gemeldet | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x03 | Abschaltvektor ZFM 1 | hex | high | signed long | - | 1 | 1 | 0 |
| 0x04 | Abschaltvektor ZFM 2 | hex | high | signed long | - | 1 | 1 | 0 |
| 0x05 | Abschaltvektor DSC | hex | high | unsigned char | - | 1 | 1 | 0 |
| 0x06 | Abschaltvektor QMV | hex | high | unsigned char | - | 1 | 1 | 0 |
| 0x07 | Abschaltvektor AL | hex | high | signed long | - | 1 | 1 | 0 |
| 0x08 | Abschaltvektor MRAD | hex | high | signed long | - | 1 | 1 | 0 |
| 0x09 | Abschaltvektor ERRMGR | hex | high | signed long | - | 1 | 1 | 0 |
| 0x0A | Abschaltvektor SBS_FS_AX | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x0B | Abschaltvektor SBS_FS_AY | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x0C | Abschaltvektor SBS_FS_PSIP | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x0D | Abschaltvektor SBS_LW_VA effektiv | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x0E | Abschaltvektor SBS_LW_VA aktuell | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x0F | Abschaltvektor SBS_LW Fahrer | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x10 | Versorgungsspannung | Volt | - | unsigned char | - | 0.125 | 1 | 0 |
| 0x11 | Service Qualifier Aktivlenkung | hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x20 | Fahrzeuggeschwindigkeit | m/s | - | unsigned char | - | 0.5 | 1 | -14 |
| 0x21 | Querbeschleunigung | m/s² | - | signed char | - | 0.12 | 1 | 0 |
| 0x22 | Gierrate | rad/s | - | signed char | - | 0.01375 | 1 | 0 |
| 0x23 | Summenlenkwinkel Rohwert | rad | - | signed int | - | 0.0175 | 1 | 0 |
| 0x24 | Fahrerlenkwinkel rad | rad | - | signed int | - | 0.0175 | 1 | 0 |
| 0x25 | Laengsbeschleunigung | m/s² | - | signed char | - | 0.08 | 1 | 0 |
| 0x26 | Lenkwinkel VA effektiv | rad | - | signed char | - | 0.006 | 1 | 0 |
| 0x27 | Fahrerlenkwinkel rad | rad | - | signed char | - | 0.08 | 1 | 0 |
| 0x28 | generische Geschwindigkeit | m/s | - | signed char | - | 0.5 | 1 | -23 |
| 0x29 | Fehleramplitude SBS AX | m/s | - | signed char | - | 0.05 | 1 | -1.2 |
| 0x2A | Fehleramplitude SBS AY | m/s | - | signed char | - | 0.05 | 1 | -1.2 |
| 0x2B | Fehleramplitude SBS PSIP | rad/s | - | signed char | - | 0.009 | 1 | -0.2 |
| 0x2C | Fehleramplitude SBS Lenkwinkel | rad | - | signed char | - | 0.005 | 1 | -0.15 |
| 0x40 | Access Violation | hex | high | signed long | - | 1 | 1 | 0 |
| 0x41 | Code Failure | hex | high | signed long | - | 1 | 1 | 0 |
| 0x42 | SPEFSCR Saved | hex | high | signed long | - | 1 | 1 | 0 |
| 0x50 | CPU 1 Block Status | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x51 | Laufzeit TASK Nr. 1 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x52 | Laufzeit TASK Nr. 2 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x53 | Laufzeit TASK Nr. 3 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x54 | Laufzeit TASK Nr. 4 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x55 | Laufzeit TASK Nr. 5 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x56 | Laufzeit TASK Nr. 6 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x57 | Laufzeit TASK Nr. 7 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x58 | Laufzeit TASK Nr. 8 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x60 | CPU1_H_xxx | hex | high | signed long | - | 1 | 1 | 0 |
| 0x61 | CPU1_L_xxx | hex | high | signed long | - | 1 | 1 | 0 |
| 0x62 | CPU2_H_xxx | hex | high | signed long | - | 1 | 1 | 0 |
| 0x63 | CPU2_L_xxx | hex | high | signed long | - | 1 | 1 | 0 |
| 0x70 | CPU1_0x13B high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x71 | CPU1_0x13B low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x72 | CPU2_0x13B high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x73 | CPU2_0x13B low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x74 | CPU1_0x13C high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x75 | CPU1_0x13C low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x76 | CPU2_0x13C high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x77 | CPU2_0x13C low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x78 | CPU1_0x136 high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x79 | CPU1_0x136 low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7A | CPU2_0x136 high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7B | CPU2_0x136 low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7C | CPU1_0x12E high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7D | CPU1_0x12E low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7E | CPU2_0x12E_high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7F | CPU2_0x12E low | hex | high | signed long | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
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
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 129 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x7000 | Diversitaeres Rechnen ODM-Analysedaten |
| 0x7001 | Diversitaeres Rechnen Fehler High Level Software |
| 0x7002 | Diversitaeres Rechnen 13B |
| 0x7003 | Diversitaeres Rechnen 13C |
| 0x7004 | Diversitaeres Rechnen 136 |
| 0x7005 | Diversitaeres Rechnen 12E |
| 0x7006 | temperaturbedingte Verfuegbarkeit QMVH unter Schwellwert |
| 0x7007 | Steuergeräte Reset |
| 0x7008 | Funktionsabschaltung aufgrund von Fehlertoleranz auf dem Signal ax |
| 0x7009 | Funktionsabschaltung aufgrund von Fehlertoleranz auf dem Signal ay |
| 0x700A | Funktionsabschaltung aufgrund von Fehlertoleranz auf dem Signal psiP |
| 0x700B | Funktionsabschaltung aufgrund von Fehlertoleranz auf dem Signal Istlenkwinkel Vorderachse lwVA_ist |
| 0x7010 | Signalueberwachung Laengsbeschleunigung ax1 hat zugeschlagen |
| 0x7011 | Signalueberwachung Querbeschleunigung ay1 hat zugeschlagen |
| 0x7012 | Signalueberwachung Querbeschleunigung ay2 hat zugeschlagen |
| 0x7013 | Signalueberwachung Gierrate psiP1 Fehler hat zugeschlagen |
| 0x7014 | Signalueberwachung Gierrate psiP2 Fehler hat zugeschlagen |
| 0x7015 | Signalueberwachung des Lenkwinkels der Aktivlenkung hat zugeschlagen |
| 0x7016 | Signalueberwachung des Fahrerlenkwinkels hat zugeschlagen |
| 0x701A | Ackermanngierrate ungueltig weil Fahrgeschwindigkeit ungueltig |
| 0x701B | Ackermanngierrate ungueltig weil Fahrgeschwindigkeit unzureichende Guete |
| 0x701C | Ackermanngierrate ungueltig weil Fahrerlenkwinkel ungueltig |
| 0x701D | Ackermanngierrate ungueltig weil Fahrzeug IST-Lenkwinkel unzureichende Guete |
| 0x7020 | CCM  Aktivlenkung gestoert  angefordert (ID 321) |
| 0x7021 | CCM  Aktivlenkung ausgefallen  angefordert (ID 273) |
| 0x7022 | CCM  QMV nicht verfuegbar erste ID  angefordert (ID 707) |
| 0x7023 | CCM  QMV nicht verfuegbar zweite ID  angefordert (ID 707) |
| 0x7024 | CCM  Servotronic ausgefallen  angefordert (ID 70) |
| 0x7422 | Signalfehler in der Botschaft (ST_LTRQD_BAX_ACT, ID=13E) von QSG ICM-CAN |
| 0x7424 | Signalfehler in der Botschaft (Lenkradwinkel Oben 2, ID=C9) von SZL F-CAN |
| 0x7426 | Signalfehler in der Botschaft (Status Anhaenger, ID=2E4) von AHM PT-CAN |
| 0x7428 | Signalfehler in der Botschaft (Status Sollmomentumsetzung, ID=BC) von VGSG PT-CAN |
| 0x7429 | Signalfehler in der Botschaft (Drehmoment 1, ID=0A8) von DME PT-CAN |
| 0x742A | Signalfehler in der Botschaft (Drehmoment 3, ID=0AA) von DME PT-CAN |
| 0x742B | Signalfehler in der Botschaft (Motordaten, ID=1D0) von DME PT-CAN |
| 0x742C | Signalfehler in der Botschaft (Status DSC PT-CAN, ID=19E) von EHB3 PT-CAN |
| 0x742D | Signalfehler in der Botschaft (Raddruecke PT-CAN, ID=2B2) von EHB3 PT-CAN |
| 0x742E | Signalfehler in der Botschaft (Klemmenstatus, ID=130) von CAS PT-CAN |
| 0x7430 | Signalfehler in der Botschaft (Fahrgestellnummer, ID=380) von CAS PT-CAN |
| 0x7431 | Signalfehler in der Botschaft (Status Lenkung Vorderachse Stellglied, ID=13D) von ASA ICM-CAN |
| 0x7432 | Signalfehler in der Botschaft (Status Lenkung Vorderachse Stellglied Erweitert, ID=13F) von ASA ICM-CAN |
| 0x7433 | Signalfehler in der Botschaft (Radgeschwindigkeiten, ID=0CE) von EHB3 F-CAN |
| 0x7434 | Signalfehler in der Botschaft (Regeleingriffe DSC, ID=11E) von EHB3 F-CAN |
| 0x7435 | Signalfehler in der Botschaft (Austausch DSC, ID=12D) von EHB3 F-CAN |
| 0x7436 | Signalfehler in der Botschaft (CLU1_VDA, ID=0D8) von SC_VDA F-CAN |
| 0x7437 | Signalfehler in der Botschaft (CLU2_VDA, ID=0E3) von SC_VDA F-CAN |
| 0x7438 | Signalfehler in der Botschaft (CLU3_VDA, ID=0F4) von SC_VDA F-CAN |
| 0x7439 | Signalfehler in der Botschaft (CLU Status VDA, ID=165) von SC_VDA F-CAN |
| 0x743A | Signalfehler in der Botschaft (Status ARS Modul ID=1AC) von ARS PT-CAN |
| 0x745C | Signalfehler in der Botschaft (Sensor Daten ROSE, ID=12A) von ACSM_ROSE F-CAN |
| 0x8010 | Botschaft (Lenkradwinkel oben, ID=0C9) von SZL F-CAN |
| 0x8011 | Botschaft (Radgeschwindigkeiten, ID=0CE) von EHB3 F-CAN |
| 0x8012 | Botschaft (CLU1_VDA, ID=0D8) von SC_VDA F-CAN |
| 0x8013 | Botschaft (CLU2_VDA, ID=0E3) von SC_VDA F-CAN |
| 0x8014 | Botschaft (CLU3_VDA, ID=0F4) von SC_VDA F-CAN |
| 0x8015 | Botschaft (Regeleingriffe DSC, ID=11E)  von EHB3 F-CAN |
| 0x8016 | Botschaft (Austausch DSC, ID=12D)  von EHB3 F-CAN |
| 0x8017 | Botschaft (Klemmenstatus, ID=130) von CAS F-CAN |
| 0x8018 | Botschaft (Status DSC-Sensor, ID=165) von EHB3 F-CAN |
| 0x8019 | Botschaft (Sensor Daten ROSE, ID=12A) von ACSM_ROSE F-CAN |
| 0x8020 | Botschaft (Drehmoment 1, ID=0A8) von DME PT-CAN |
| 0x8021 | Botschaft (Drehmoment 3, ID=0AA) von DME PT-CAN |
| 0x8022 | Botschaft (Getriebedaten, ID=0BA) von EGS_EL PT-CAN |
| 0x8023 | Botschaft (Status Sollmomentumsetzung, ID=0BC) von VGSG PT-CAN |
| 0x8024 | Botschaft (Klemmenstatus, ID=130) von CAS PT-CAN |
| 0x8025 | Botschaft (Status DSC PT-CAN, ID=19E) von EHB3 PT-CAN |
| 0x8026 | Botschaft (Status ARS Modul ID=1AC) von ARS PT-CAN |
| 0x8027 | Botschaft (Motordaten, ID=1D0) von DME PT-CAN |
| 0x8028 | Botschaft (Raddruecke PT-CAN, ID=2B2) von EHB3 PT-CAN |
| 0x8029 | Botschaft (Anhaengerdaten, ID=2E4) von AHM PT-CAN |
| 0x802A | Botschaft (Kilometerstand, ID=330) von Kombi PT-CAN |
| 0x802B | Botschaft (Fahrgestellnummer, ID=380) von CAS PT-CAN |
| 0x8030 | Botschaft (Status Lenkung Vorderachse Stellglied, ID=13D) von ASA ICM-CAN |
| 0x8031 | Botschaft (Status Quermomentenverteilung Hinterachse Stellglied, ID=13E) von QSG ICM-CAN |
| 0x8032 | Botschaft (Status Lenkung Vorderachse Stellglied Erweitert, ID=13F) von ASA ICM-CAN |
| 0x8033 | Botschaft (Entwicklungsdaten, ID=7C8) von QSG ICM-CAN |
| 0x9008 | Funktionsabschaltung aufgrund von Fehlertoleranz auf dem Signal ax |
| 0x9009 | Funktionsabschaltung aufgrund von Fehlertoleranz auf dem Signal ay |
| 0x900A | Funktionsabschaltung aufgrund von Fehlertoleranz auf dem Signal psiP |
| 0x900B | Funktionsabschaltung aufgrund von Fehlertoleranz auf dem Signal Ist-Lenkwinkel-Vorderachse lwVA_ist |
| 0x9010 | Signalueberwachung Laengsbeschleunigung ax1 hat zugeschlagen |
| 0x9011 | Signalueberwachung Querbeschleunigung ay1 hat zugeschlagen |
| 0x9012 | Signalueberwachung Querbeschleunigung ay2 hat zugeschlagen |
| 0x9013 | Signalueberwachung Gierrate psiP1 Fehler hat zugeschlagen |
| 0x9014 | Signalueberwachung Gierrate psiP2 Fehler hat zugeschlagen |
| 0x9015 | Signalueberwachung des Lenkwinkels der Aktivlenkung hat zugeschlagen |
| 0x9016 | Signalueberwachung des Fahrerlenkwinkels hat zugeschlagen |
| 0x941D | Sensor-Abgleiche nicht durchgeführt |
| 0x9422 | Signalfehler in der Botschaft (ST_LTRQD_BAX_ACT, ID=13E) von QSG ICM-CAN |
| 0x9424 | Signalfehler in der Botschaft (Lenkradwinkel Oben 2, ID=C9) von SZL F-CAN |
| 0x9429 | Signalfehler in der Botschaft (Drehmoment 1, ID=0A8) von DME PT-CAN |
| 0x942A | Signalfehler in der Botschaft (Drehmoment 3, ID=0AA) von DME PT-CAN |
| 0x942D | Signalfehler in der Botschaft (Raddruecke PT-CAN, ID=2B2) von EHB3 PT-CAN |
| 0x9430 | Signalfehler in der Botschaft (Fahrgestellnummer, ID=380) von CAS PT-CAN |
| 0x9431 | Signalfehler in der Botschaft (Status Lenkung Vorderachse Stellglied, ID=13D) von ASA ICM-CAN |
| 0x9432 | Signalfehler in der Botschaft (Status Lenkung Vorderachse Stellglied Erweitert, ID=13F) von ASA ICM-CAN |
| 0x9433 | Signalfehler in der Botschaft (Radgeschwindigkeiten, ID=0CE) von EHB3 F-CAN |
| 0x9435 | Signalfehler in der Botschaft (Austausch DSC, ID=12D) von EHB3 F-CAN |
| 0x9436 | Signalfehler in der Botschaft (CLU1_VDA, ID=0D8) von SC_VDA F-CAN |
| 0x9437 | Signalfehler in der Botschaft (CLU2_VDA, ID=0E3) von SC_VDA F-CAN |
| 0x9438 | Signalfehler in der Botschaft (CLU3_VDA, ID=0F4) von SC_VDA F-CAN |
| 0x9439 | Signalfehler in der Botschaft (CLU Status VDA, ID=165) von SC_VDA F-CAN |
| 0x944C | Motorlagewinkel AL ungueltig |
| 0x944D | AL inaktiv und Fahrzeug rollt |
| 0x944E | AL im Pausemodus und Fahrzeug rollt (Motor abgewuergt, Untersannung) |
| 0x944F | AL im Errormodus |
| 0x9450 | AL in undefinitrtem Statemaschine Zustand (haengt im Intit, Postrun) |
| 0x9452 | SZL neu abgeglichen |
| 0x9453 | SZL neu verbaut |
| 0x9454 | AL gestoert: schnelle Lenkwinkelsynchronisation |
| 0x9455 | AL gestoert: langsame Lenkwinkelsynchronisation |
| 0x9456 | AL gestoert: AGB (verfuegbare Dynamik zu gering, Fehleramplitude zu gross) |
| 0x945B | AL kann nicht in aktiven Modus wechseln |
| 0x9461 | Signalüberwachung der Sensorclustersignale hat angeschlagen |
| 0x9462 | Signalüberwachung der Lenkwinkelsignale hat angeschlagen |
| 0xA010 | Botschaft (Lenkradwinkel oben, ID=0C9) von SZL F-CAN |
| 0xA011 | Botschaft (Radgeschwindigkeiten, ID=0CE) von EHB3 F-CAN |
| 0xA012 | Botschaft (CLU1_VDA, ID=0D8) von SC_VDA F-CAN |
| 0xA013 | Botschaft (CLU2_VDA, ID=0E3) von SC_VDA F-CAN |
| 0xA014 | Botschaft (CLU3_VDA, ID=0F4) von SC_VDA F-CAN |
| 0xA016 | Botschaft (Austausch DSC, ID=12D)  von EHB3 F-CAN |
| 0xA018 | Botschaft (Status DSC-Sensor, ID=165) von EHB3 F-CAN |
| 0xA020 | Botschaft (Drehmoment 1, ID=0A8) von DME PT-CAN |
| 0xA021 | Botschaft (Drehmoment 3, ID=0AA) von DME PT-CAN |
| 0xA028 | Botschaft (Raddruecke PT-CAN, ID=2B2) von DXC PT-CAN |
| 0xA030 | Botschaft (Status Lenkung Vorderachse Stellglied, ID=13D) von ASA ICM-CAN |
| 0xA031 | Botschaft (Status Quermomentenverteilung Hinterachse Stellglied, ID=13E) von QSG ICM-CAN |
| 0xA032 | Botschaft (Status Lenkung Vorderachse Stellglied Erweitert, ID=13F) von ASA ICM-CAN |
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

Dimensions: 78 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x7000 | UWB_D | - | - | - |
| 0x7001 | UWB_A | - | - | - |
| 0x7002 | UWB_E | - | - | - |
| 0x7003 | UWB_F | - | - | - |
| 0x7004 | UWB_G | - | - | - |
| 0x7005 | UWB_H | - | - | - |
| 0x7006 | UWB_A | - | - | - |
| 0x7007 | UWB_D | - | - | - |
| 0x7008 | UWB_A | - | - | - |
| 0x7009 | UWB_A | - | - | - |
| 0x700A | UWB_A | - | - | - |
| 0x700B | UWB_A | - | - | - |
| 0x7010 | UWB_B | - | - | - |
| 0x7011 | UWB_B | - | - | - |
| 0x7012 | UWB_B | - | - | - |
| 0x7013 | UWB_B | - | - | - |
| 0x7014 | UWB_B | - | - | - |
| 0x7015 | UWB_B | - | - | - |
| 0x7016 | UWB_B | - | - | - |
| 0x701A | UWB_B | - | - | - |
| 0x701B | UWB_B | - | - | - |
| 0x701C | UWB_B | - | - | - |
| 0x701D | UWB_B | - | - | - |
| 0x7020 | UWB_B | - | - | - |
| 0x7021 | UWB_B | - | - | - |
| 0x7022 | UWB_B | - | - | - |
| 0x7023 | UWB_B | - | - | - |
| 0x7024 | UWB_B | - | - | - |
| 0x9008 | UWB_M | - | - | - |
| 0x9009 | UWB_M | - | - | - |
| 0x900A | UWB_M | - | - | - |
| 0x900B | UWB_N | - | - | - |
| 0x9010 | UWB_M | - | - | - |
| 0x9011 | UWB_M | - | - | - |
| 0x9012 | UWB_M | - | - | - |
| 0x9013 | UWB_M | - | - | - |
| 0x9014 | UWB_M | - | - | - |
| 0x9015 | UWB_N | - | - | - |
| 0x9016 | UWB_N | - | - | - |
| 0x941D | UWB_M | - | - | - |
| 0x9422 | UWB_J | - | - | - |
| 0x9424 | UWB_K | - | - | - |
| 0x9429 | UWB_L | - | - | - |
| 0x942A | UWB_L | - | - | - |
| 0x9431 | UWB_K | - | - | - |
| 0x9432 | UWB_K | - | - | - |
| 0x9433 | UWB_J | - | - | - |
| 0x9435 | UWB_J | - | - | - |
| 0x9436 | UWB_J | - | - | - |
| 0x9437 | UWB_J | - | - | - |
| 0x9438 | UWB_J | - | - | - |
| 0x9439 | UWB_J | - | - | - |
| 0x944C | UWB_K | - | - | - |
| 0x944D | UWB_K | - | - | - |
| 0x944E | UWB_K | - | - | - |
| 0x944F | UWB_K | - | - | - |
| 0x9450 | UWB_K | - | - | - |
| 0x9452 | UWB_K | - | - | - |
| 0x9453 | UWB_K | - | - | - |
| 0x9454 | UWB_K | - | - | - |
| 0x9455 | UWB_K | - | - | - |
| 0x9456 | UWB_K | - | - | - |
| 0x945B | UWB_K | - | - | - |
| 0x9461 | UWB_M | - | - | - |
| 0x9462 | UWB_N | - | - | - |
| 0xA010 | UWB_K | - | - | - |
| 0xA011 | UWB_J | - | - | - |
| 0xA012 | UWB_J | - | - | - |
| 0xA013 | UWB_J | - | - | - |
| 0xA014 | UWB_J | - | - | - |
| 0xA016 | UWB_J | - | - | - |
| 0xA018 | UWB_J | - | - | - |
| 0xA020 | UWB_L | - | - | - |
| 0xA021 | UWB_L | - | - | - |
| 0xA030 | UWB_K | - | - | - |
| 0xA031 | UWB_J | - | - | - |
| 0xA032 | UWB_K | - | - | - |
| default | UWB_I | - | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 62 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Zeitstempel, absolute Zeit in ms | ms | - | signed long | - | 10 | 1 | 0 |
| 0x02 | Fehler Detail, zuletzt gemeldet | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x03 | Abschaltvektor ZFM 1 | hex | high | signed long | - | 1 | 1 | 0 |
| 0x04 | Abschaltvektor ZFM 2 | hex | high | signed long | - | 1 | 1 | 0 |
| 0x05 | Abschaltvektor DSC | hex | high | unsigned char | - | 1 | 1 | 0 |
| 0x06 | Abschaltvektor QMV | hex | high | unsigned char | - | 1 | 1 | 0 |
| 0x07 | Abschaltvektor AL | hex | high | signed long | - | 1 | 1 | 0 |
| 0x08 | Abschaltvektor MRAD | hex | high | signed long | - | 1 | 1 | 0 |
| 0x09 | Abschaltvektor ERRMGR | hex | high | signed long | - | 1 | 1 | 0 |
| 0x0A | Abschaltvektor SBS_FS_AX | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x0B | Abschaltvektor SBS_FS_AY | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x0C | Abschaltvektor SBS_FS_PSIP | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x0D | Abschaltvektor SBS_LW_VA effektiv | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x0E | Abschaltvektor SBS_LW_VA aktuell | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x0F | Abschaltvektor SBS_LW Fahrer | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x10 | Versorgungsspannung | Volt | - | unsigned char | - | 0.125 | 1 | 0 |
| 0x11 | Service Qualifier Aktivlenkung | hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x20 | Fahrzeuggeschwindigkeit | m/s | - | unsigned char | - | 0.5 | 1 | -14 |
| 0x21 | Querbeschleunigung | m/s² | - | signed char | - | 0.12 | 1 | 0 |
| 0x22 | Gierrate | rad/s | - | signed char | - | 0.01375 | 1 | 0 |
| 0x23 | Summenlenkwinkel Rohwert | rad | - | signed int | - | 0.0175 | 1 | 0 |
| 0x24 | Fahrerlenkwinkel rad | rad | - | signed int | - | 0.0175 | 1 | 0 |
| 0x25 | Laengsbeschleunigung | m/s² | - | signed char | - | 0.08 | 1 | 0 |
| 0x26 | Lenkwinkel VA effektiv | rad | - | signed char | - | 0.006 | 1 | 0 |
| 0x27 | Fahrerlenkwinkel rad | rad | - | signed char | - | 0.08 | 1 | 0 |
| 0x28 | generische Geschwindigkeit | m/s | - | signed char | - | 0.5 | 1 | -23 |
| 0x29 | Fehleramplitude SBS AX | m/s | - | signed char | - | 0.05 | 1 | -1.2 |
| 0x2A | Fehleramplitude SBS AY | m/s | - | signed char | - | 0.05 | 1 | -1.2 |
| 0x2B | Fehleramplitude SBS PSIP | rad/s | - | signed char | - | 0.009 | 1 | -0.2 |
| 0x2C | Fehleramplitude SBS Lenkwinkel | rad | - | signed char | - | 0.005 | 1 | -0.15 |
| 0x40 | Access Violation | hex | high | signed long | - | 1 | 1 | 0 |
| 0x41 | Code Failure | hex | high | signed long | - | 1 | 1 | 0 |
| 0x42 | SPEFSCR Saved | hex | high | signed long | - | 1 | 1 | 0 |
| 0x50 | CPU 1 Block Status | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x51 | Laufzeit TASK Nr. 1 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x52 | Laufzeit TASK Nr. 2 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x53 | Laufzeit TASK Nr. 3 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x54 | Laufzeit TASK Nr. 4 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x55 | Laufzeit TASK Nr. 5 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x56 | Laufzeit TASK Nr. 6 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x57 | Laufzeit TASK Nr. 7 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x58 | Laufzeit TASK Nr. 8 | µs | - | unsigned int | - | 1 | 1 | 0 |
| 0x60 | CPU1_H_xxx | hex | high | signed long | - | 1 | 1 | 0 |
| 0x61 | CPU1_L_xxx | hex | high | signed long | - | 1 | 1 | 0 |
| 0x62 | CPU2_H_xxx | hex | high | signed long | - | 1 | 1 | 0 |
| 0x63 | CPU2_L_xxx | hex | high | signed long | - | 1 | 1 | 0 |
| 0x70 | CPU1_0x13B high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x71 | CPU1_0x13B low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x72 | CPU2_0x13B high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x73 | CPU2_0x13B low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x74 | CPU1_0x13C high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x75 | CPU1_0x13C low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x76 | CPU2_0x13C high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x77 | CPU2_0x13C low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x78 | CPU1_0x136 high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x79 | CPU1_0x136 low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7A | CPU2_0x136 high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7B | CPU2_0x136 low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7C | CPU1_0x12E high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7D | CPU1_0x12E low | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7E | CPU2_0x12E_high | hex | high | signed long | - | 1 | 1 | 0 |
| 0x7F | CPU2_0x12E low | hex | high | signed long | - | 1 | 1 | 0 |

<a id="table-guealmlw"></a>
### GUEALMLW

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | MLW AL gueltig |
| 0x01 | MLW AL nicht gueltig |
| 0xFF | unbekannter Status |

<a id="table-szlprozinfo"></a>
### SZLPROZINFO

Dimensions: 3 rows × 2 columns

| SZL_PROZ_NR | SZL_PROZ_TEXT |
| --- | --- |
| 0x00 | SZL Ein-Prozessor; kein AFS |
| 0xA0 | SZL Zwei-Prozessor; AFS |
| 0xFF | unbekannter Status |

<a id="table-szlabgleichinfo"></a>
### SZLABGLEICHINFO

Dimensions: 5 rows × 2 columns

| SZL_ABGLEICH_NR | SZL_ABGLEICH_TEXT |
| --- | --- |
| 0x00 | kein Abgleich |
| 0x01 | Abgleich laeuft |
| 0x02 | Coding |
| 0x03 | Signal ungueltig |
| 0xFF | unbekannter Status |

<a id="table-gueflw"></a>
### GUEFLW

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Initialisierung |
| 0x01 | Signalwert ist gueltig und abgesichert |
| 0x02 | Signal ist gueltig |
| 0x03 | Signal ist nicht vertrauenswuerdig |
| 0x04 | Ersatzwert ist im Nutzsignal gesetzt |
| 0x05 | nicht definiert |
| 0x06 | Signalwert ist ungueltig |
| 0x07 | Sensor nicht vorhanden oder Signal ungueltig |
| 0xFF | unbekannter Status |

<a id="table-guealistmlw"></a>
### GUEALISTMLW

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Initialisierung |
| 0x01 | gueltig |
| 0x05 | Timeout |
| 0x06 | ungueltig |
| 0xFF | unbekannter Status |

<a id="table-guealsollmlw"></a>
### GUEALSOLLMLW

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x20 | Sollwert umsetzen |
| 0xE0 | Sollwert nicht umsetzen |
| 0xE1 | Rotorlage im ASA gueltig setzen |
| 0xE2 | Rotorlage im ASA ungueltig setzen |
| 0xFF | unbekannter Status |

<a id="table-gueslwroh"></a>
### GUESLWROH

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Initialisierung |
| 0x01 | Signalwert ist gueltig und abgesichert |
| 0x02 | Signal ist gueltig |
| 0x03 | Signal ist nicht vertrauenswuerdig |
| 0x04 | Ersatzwert ist im Nutzsignal gesetzt |
| 0x05 | nicht definiert |
| 0x06 | Signalwert ist ungueltig |
| 0x07 | Sensor nicht vorhanden oder Signal ungueltig |
| 0xFF | unbekannter Status |

<a id="table-guealmlwzustand"></a>
### GUEALMLWZUSTAND

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Initialisierung |
| 0x01 | gueltig |
| 0x05 | Timeout |
| 0x06 | ungueltig |
| 0xFF | unbekannter Status |

<a id="table-guealmlwinit"></a>
### GUEALMLWINIT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht gelernt |
| 0x01 | gelernt |
| 0xFF | unbekannter Status |

<a id="table-zfm-qes-fsqual"></a>
### ZFM_QES_FSQUAL

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Initialisierung |
| 0x01 | Gueltig und abgesichert |
| 0x02 | Gueltig |
| 0x03 | Nicht vertrauenswuerdig |
| 0x04 | Ersatzwert |
| 0x05 | Kommunikationsfehler |
| 0x06 | Ungueltig |
| 0x07 | Ungueltig |
| 0xFF | unbekannter Status |

<a id="table-zfm-qis-nsq"></a>
### ZFM_QIS_NSQ

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Initialisierung |
| 0x01 | Gueltig und abgesichert |
| 0x02 | Gueltig |
| 0x03 | Nicht vertrauenswuerdig |
| 0x04 | Ersatzwert |
| 0x05 | Kommunikationsfehler |
| 0x06 | Ungueltig |
| 0x07 | Ungueltig |
| 0xFF | unbekannter Status |

<a id="table-zfm-zef-zst"></a>
### ZFM_ZEF_ZST

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | passiv |
| 0x01 | bereit |
| 0x02 | aktiv |
| 0x03 | fehler |
| 0x04 | in abschaltung |
| 0xFF | unbekannter Status |

<a id="table-zfm-zif-zs"></a>
### ZFM_ZIF_ZS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | passiv |
| 0x01 | bereit passiv |
| 0x02 | bereit aktiv |
| 0x03 | aktiv |
| 0xFF | unbekannter Status |

<a id="table-zfm-akt-zst"></a>
### ZFM_AKT_ZST

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Aktuator Fehler |
| 0x02 | Aktuator nicht verbaut |
| 0x04 | Aktuator eingeschraenkt verfuegbar |
| 0x08 | Aktuator nicht verfuegbar |
| 0x10 | Aktuator will Sollwert |
| 0xFF | unbekannter Status |

<a id="table-statusecoventil"></a>
### STATUSECOVENTIL

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Vx kleiner/gleich als 3 m/s |
| 0x01 | Vx groesser als 3 m/s |
| 0x10 | Qualifier gueltig |
| 0x11 | Qualifier ungueltig |
| 0x20 | Motor an |
| 0x21 | Motor aus |
| 0x30 | ECO in Ordnung |
| 0x31 | ECO im Selbsttest oder defekt |
| 0xFF | unbekannter Status |

<a id="table-statusservoventil"></a>
### STATUSSERVOVENTIL

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Vx kleiner/gleich als 3 m/s |
| 0x01 | Vx groesser als 3 m/s |
| 0x10 | Qualifier gueltig |
| 0x11 | Qualifier ungueltig |
| 0x20 | Motor an |
| 0x21 | Motor aus |
| 0x30 | SVT in Ordnung |
| 0x31 | SVT im Selbsttest oder defekt |
| 0xFF | unbekannter Status |

<a id="table-almlwistqualifier"></a>
### ALMLWISTQUALIFIER

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Initialisierung |
| 0x01 | Signalwert ist gueltig und abgesichert |
| 0x02 | Signal ist gueltig |
| 0x03 | Signal ist nicht vertrauenswuerdig |
| 0x04 | Ersatzwert ist im Nutzsignal gesetzt |
| 0x05 | Signal zu oft entprellt |
| 0x06 | Signalwert ist ungueltig |
| 0x07 | Sensor nicht vorhanden oder Signal ungueltig |
| 0xFF | unbekannter Status |

<a id="table-almlwservicequalifier"></a>
### ALMLWSERVICEQUALIFIER

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x80 | Initialisierung |
| 0x21 | Drive Standby |
| 0x22 | Drive |
| 0x31 | Drive Standby, USW1 |
| 0x35 | Drive Standby, USW2 |
| 0x39 | Drive Standby, USW3 |
| 0x36 | Drive, USW1 |
| 0x32 | Drive, USW2 |
| 0x3A | Drive, USW3 |
| 0xE0 | Postrun |
| 0xE1 | ReadyforDrive |
| 0xE3 | Drive_RampZero |
| 0xE4 | WaitForRLWSet |
| 0xE9 | ReadyForDrive Unterspannung |
| 0xEB | Drive_RampZero Unterspannung |
| 0x68 | Error |
| 0xFF | Invalid |

<a id="table-almlwsollqualifier"></a>
### ALMLWSOLLQUALIFIER

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x80 | Initialisierung |
| 0x20 | Sollwert umsetzen |
| 0xE0 | Sollwert nicht umsetzen |
| 0xE1 | Set RLW valid |
| 0xE2 | Set RLW invalid |
| 0x60 | Fehler |
| 0x70 | Sollwert nicht vorhanden |
| 0xFF | Signal ungueltig |

<a id="table-sgstati"></a>
### SGSTATI

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | SG_STATE_BOOT_INIT |
| 0x11 | SG_STATE_BOOT_ACTIVE |
| 0x22 | SG_STATE_BOOT_ERROR |
| 0x33 | SG_STATE_BOOT_SAVE |
| 0x44 | SG_STATE_APPL_INIT |
| 0x55 | SG_STATE_APPL_ACTIVE |
| 0x66 | SG_STATE_APPL_ERROR |
| 0x77 | SG_STATE_APPL_SAVE |
| 0x88 | SG_STATE_APPL_ERROR_2 |
| 0xFF | unbekannter Status |

<a id="table-guealmlwoffset"></a>
### GUEALMLWOFFSET

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | im Werksmode |
| 0x01 | nicht im Werksmode |
| 0x10 | MLW AL nicht gueltig |
| 0x11 | MLW AL gueltig |
| 0xFF | unbekannter Status |

<a id="table-jobinterpretation"></a>
### JOBINTERPRETATION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Jobergebnis fehlerhaft |
| 0x01 | Job noch nicht gelaufen oder nicht abgeschlossen |
| 0x02 | Jobergebnis i.O. |
| 0xFF | unbekannter Status |

<a id="table-sgstatus"></a>
### SGSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Steuergeraet n.i.O. |
| 0x01 | Steuergeraet i.O. |
| 0xFF | unbekannter Status |

<a id="table-fahrgestellnrstatus"></a>
### FAHRGESTELLNRSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Fahrgestellnummner unterschiedlich |
| 0x01 | Fahrgestellnummner gueltig |
| 0x02 | Fahrgestellnummner nicht empfangen bzw ungueltig |
| 0xFF | unbekannter Status |

<a id="table-divcalcstatus"></a>
### DIVCALCSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | diversitaeres Rechnen n.i.O. |
| 0x01 | diversitaeres Rechnen i.O. |
| 0xFF | unbekannter Status |

<a id="table-statusecoventil-bit0"></a>
### STATUSECOVENTIL_BIT0

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ECO Ventil i.O. |
| 0x01 | ECO Ventil nicht i.O. |
| 0xFF | unbekannter Status |

<a id="table-statusecoventil-bit1"></a>
### STATUSECOVENTIL_BIT1

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ECO Ventil verbaut |
| 0x01 | ECO Ventil nicht verbaut |
| 0xFF | unbekannter Status |

<a id="table-statusecoventil-bit3"></a>
### STATUSECOVENTIL_BIT3

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ECO Ventil verfuegbar |
| 0x01 | ECO Ventil nicht verfuegbar |
| 0xFF | unbekannter Status |

<a id="table-statusservoventil-bit0"></a>
### STATUSSERVOVENTIL_BIT0

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | SERVO Ventil i.O. |
| 0x01 | SERVO Ventil nicht i.O. |
| 0xFF | unbekannter Status |

<a id="table-statusservoventil-bit1"></a>
### STATUSSERVOVENTIL_BIT1

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | SERVO Ventil verbaut |
| 0x01 | SERVO Ventil nicht verbaut |
| 0xFF | unbekannter Status |

<a id="table-statusservoventil-bit3"></a>
### STATUSSERVOVENTIL_BIT3

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | SERVO Ventil verfuegbar |
| 0x01 | SERVO Ventil nicht verfuegbar |
| 0xFF | unbekannter Status |

<a id="table-alccmeldung"></a>
### ALCCMELDUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine CC-Meldung |
| 0x01 | Aktivlenkung ausgefallen |
| 0x02 | Aktivlenkung gestoert |
| 0xFF | unbekannter Status |

<a id="table-szlgueflwroh"></a>
### SZLGUEFLWROH

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | absolut |
| 0x01 | relativ |
| 0x02 | Fehler |
| 0x03 | Signal ungueltig |
| 0xFF | unbekannter Status |

<a id="table-alvstdyn"></a>
### ALVSTDYN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Vorsteuerwert wird nicht umgesetzt |
| 0x01 | Vorsteuerwert wird umgesetzt |
| 0xFF | unbekannter Wert |

<a id="table-alvststat"></a>
### ALVSTSTAT

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Vorsteuerung ist passiv |
| 0x01 | Vorsteuerung ist bereit passiv |
| 0x02 | Vorsteuerung ist bereit aktiv |
| 0x03 | Vorsteuerung ist aktiv |
| 0xFF | ungueltiger Wert |

<a id="table-alreglerstat"></a>
### ALREGLERSTAT

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Regler ASA ist passiv |
| 0x01 | Regler ASA ist bereit-passiv |
| 0x02 | Regler ASA ist bereit-aktiv |
| 0x023 | Regler ASA ist aktiv |
| 0xFF | ungueltiger Wert |

<a id="table-alreglergrrplusstat"></a>
### ALREGLERGRRPLUSSTAT

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Regler ASA GRRplus ist passiv |
| 0x01 | Regler ASA GRRplus ist bereit-passiv |
| 0x02 | Regler ASA GRRplus ist bereit-aktiv |
| 0x03 | Regler ASA GRRplus ist aktiv |
| 0xFF | ungueltiger Wert |

<a id="table-uwb-a"></a>
### UWB_A

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x01 | 0x02 | 0x10 | 0x20 | 0x21 | 0x22 | 0x23 | 0x24 |

<a id="table-uwb-b"></a>
### UWB_B

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x01 | 0x02 | 0x10 |

<a id="table-uwb-c"></a>
### UWB_C

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x01 | 0x02 | 0x10 | 0x40 | 0x41 | 0x42 |

<a id="table-uwb-d"></a>
### UWB_D

Dimensions: 1 rows × 12 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 11 | 0x01 | 0x02 | 0x50 | 0x51 | 0x52 | 0x53 | 0x54 | 0x55 | 0x56 | 0x57 | 0x58 |

<a id="table-uwb-e"></a>
### UWB_E

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x01 | 0x02 | 0x70 | 0x71 | 0x72 | 0x73 |

<a id="table-uwb-f"></a>
### UWB_F

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x01 | 0x02 | 0x74 | 0x75 | 0x76 | 0x77 |

<a id="table-uwb-g"></a>
### UWB_G

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x01 | 0x02 | 0x78 | 0x79 | 0x7A | 0x7B |

<a id="table-uwb-h"></a>
### UWB_H

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x01 | 0x02 | 0x7C | 0x7D | 0x7E | 0x7F |

<a id="table-uwb-i"></a>
### UWB_I

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x01 | 0x02 | 0x03 | 0x04 |

<a id="table-uwb-j"></a>
### UWB_J

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 |

<a id="table-uwb-k"></a>
### UWB_K

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x01 | 0x02 | 0x03 | 0x04 | 0x07 | 0x11 |

<a id="table-uwb-l"></a>
### UWB_L

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x01 | 0x02 | 0x03 | 0x04 | 0x08 |

<a id="table-uwb-m"></a>
### UWB_M

Dimensions: 1 rows × 13 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 12 | 0x01 | 0x02 | 0x09 | 0x0A | 0x0B | 0x0C | 0x21 | 0x22 | 0x25 | 0x29 | 0x2A | 0x2B |

<a id="table-uwb-n"></a>
### UWB_N

Dimensions: 1 rows × 13 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 12 | 0x01 | 0x02 | 0x09 | 0x0D | 0x0E | 0x0F | 0x11 | 0x23 | 0x24 | 0x26 | 0x27 | 0x2C |
