# AFS_70.prg

- Jobs: [90](#jobs)
- Tables: [47](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Active Front Steering für E70 |
| ORIGIN | BMW EF-61 Manuel Singer |
| REVISION | 3.000 |
| AUTHOR | BMW EF-61 Manuel Singer, Software & Systems EF-61 Joachim Schindlbeck |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
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
- [STATUS_VERSORGUNGEN](#job-status-versorgungen) - Auslesen der aktuellen Spanungspegel KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $01 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [STATUS_AFS_OS](#job-status-afs-os) - Auslesen verschiedener Betriebssystem (OS, SG) Stati KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $02 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_PHASENSTROEME](#job-status-phasenstroeme) - Auslesen der Phasenstrome I1,I2,I3 am Stellmotor, Stator KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $04 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_TEMPERATUREN](#job-status-temperaturen) - Auslesen der Steuergeraetetemperatur KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $05 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_SZL](#job-status-szl) - Auslesen verschiedener vom SZL gesendeter Werte ueber F-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $06 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_SENSORCLUSTER](#job-status-sensorcluster) - Auslesen verschiedener Stati des Sensorclsuter ueber F-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $07 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_SUMMENLENKWINKEL](#job-status-summenlenkwinkel) - Auslesen des im SG errechneten Summenlenkwinkels KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $08 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_MOTORLAGEWINKEL](#job-status-motorlagewinkel) - Auslesen verschiedener Motorlagewinkel KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $09 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_FAHRERLENKWINKEL](#job-status-fahrerlenkwinkel) - Auslesen des Fahrerlenkwinkels vom SZL KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0A InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [STATUS_GESCHWINDIGKEITEN](#job-status-geschwindigkeiten) - Auslesen verschiedener Geschwindigkeiten KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0B InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [STATUS_BESCHLEUNIGUNG](#job-status-beschleunigung) - Auslesen der Quer- und Laengsbeschleunigungswerte KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0C InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [STATUS_GIERRATEN](#job-status-gierraten) - Auslesen der Gierratenwerte KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0D InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [STATUS_DSC_INFO](#job-status-dsc-info) - Auslesen aktueller DSC Stati ueber PT-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0E InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [STATUS_WINKELWERTE](#job-status-winkelwerte) - Auslesen verschiedener Winkelwerte, wie Fahrerlenkwinkel, Summenlenkwinkel, Motorlagewinkel KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0F InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [STATUS_PHASENSPANNUNGEN](#job-status-phasenspannungen) - Auslesen der Phasenspanngen U1,U2,U3 am Stellmotor, Stator KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $10 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_ALIVE_INFO](#job-status-alive-info) - Auslesen verschiedener ALIVE Zaehler KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $13 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_SENSORCLUSTER_INFO](#job-status-sensorcluster-info) - Status und Diagnoseinfos ueber den Sensorclsuter KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $15 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [STATUS_CAS_INFO](#job-status-cas-info) - Auslesen der vom CAS gesendeten Fahrgestellnummer ueber PT-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $16 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [STATUS_ECO_SERVO](#job-status-eco-servo) - Auslesen des aktuell anliegenden Stromes am ECO Ventil und dessen Status KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $17 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_ECO_VENTIL](#job-status-eco-ventil) - Auslesen des aktuell anliegenden Stromes am ECO Ventil und dessen Status KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $18 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_SERVO_VENTIL](#job-status-servo-ventil) - Auslesen des aktuell anliegenden Stromes am SERVO Ventil und dessen Status KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $19 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_PTCAN_SIGNAL_FEHLER](#job-status-ptcan-signal-fehler) - diverse vom AFS eingelesene PTCAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $1B InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_FCAN_SIGNAL_FEHLER](#job-status-fcan-signal-fehler) - diverse vom AFS eingelesene FCAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $1C InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [START_LWM_RUECKSETZEN](#job-start-lwm-ruecksetzen) - Motorlagewinkel wird ungueltig gesetzt KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $21 Motorlagewinkel ungueltig setzen,ueber ZFLS Fkt mit anschl. SG-RESET Modus  : Default KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $50 Gueltigkeit Motorlagewinkel abfragen Modus  : Default
- [START_LWM_INIT](#job-start-lwm-init) - KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $22 Inbetriebnahme Resultat abfragen Modus  : Default
- [START_ADAPTIVDATEN_ABGLEICH](#job-start-adaptivdaten-abgleich) - KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $51 Abgleich der Adaptivdaten wird gestartet Modus  : Default
- [START_ADAPTIVDATEN_RUECKSETZEN](#job-start-adaptivdaten-ruecksetzen) - KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $53 Adaptivdaten im EEPROM werden DEFAULT werten beschrieben Modus  : Default
- [STATUS_LWM_INIT](#job-status-lwm-init) - Gueltigkeit des Motorlagewinkels auslesen KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $50 Inbetriebnahme Resultat abfragen Modus  : Default
- [STATUS_ADAPTIVDATEN_ABGLEICH](#job-status-adaptivdaten-abgleich) - aktueller Zustand des Adaptivdatenabgleichs KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $51 alle aktuelle Abgleichstati abfragen Modus  : Default
- [STATUS_ADAPTIVDATEN_RUECKSETZEN](#job-status-adaptivdaten-ruecksetzen) - aktueller Zustand des Ruecksetzens der Adaptivdaten KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $53 Adaptivdaten werden mit DEFAULT Werten belegt Modus  : Default
- [STEUERN_MOTORLAGEWINKEL_OFFSET](#job-steuern-motorlagewinkel-offset) - Schreiben des Motorlagewinkeloffsets ins EEPROM KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $22 InputOutputLocalIdentifier(IOLI) SubID  : $07 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_EEPROM_SERIENNUMMER_SZL](#job-status-eeprom-seriennummer-szl) - Auslesen der im AFS EEPROM abgelegten Seriennummer des SZL AFS wird / bleibt inaktiv falls SZL getauscht wird KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $01 InputOutputLocalIdentifier(IOLI) SubID  : $08 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_EEPROM_OFFSET_SZL](#job-status-eeprom-offset-szl) - Auslesen des im AFS EEPROM abgelegten Fahrerlenkwinkeloffsets vom SZL KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $02 InputOutputLocalIdentifier(IOLI) SubID  : $08 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_MOTORLAGEWINKEL_OFFSET](#job-status-motorlagewinkel-offset) - Auslesen des Motorlagewinkeloffsets aus dem EEPROM und des Maximalwerts KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $03 InputOutputLocalIdentifier(IOLI) SubID  : $08 InputOutputControlParameter(IOCP) Modus  : Default
- [ZF_FACTORY_DATEN_LESEN](#job-zf-factory-daten-lesen) - hier werden 12 Byte aus dem EEPROM Werksdatenbereich ausgelesen, ab Adresse 0x0FCA KWP2000: $23 readMemoryByAddress SubID  : $02 MemoryTypeIdentifier (ROMX), MT = 2 Modus  : Default
- [IDENT_AIF_LESEN](#job-ident-aif-lesen) - aktuelles AIF Feld auslesen KWP2000: $1A ReadECUIdentification SubID  : $86 CurrentUIFDataTable Modus  : Default
- [IDENT_ISTUFE_LESEN](#job-ident-istufe-lesen) - Auslesen der aktuellen Integrationsstufe KWP2000: $1A ReadECUIdentification SubID  : $82 reserved by Document Modus  : Default
- [IDENT_DIVCALC_LESEN](#job-ident-divcalc-lesen) - Auslesen der aktuellen Kennung des diversitaeren Rechnens auf dem NEC, SG darf NICHT im DRIVE Modus sein KWP2000: $1A ReadECUIdentification SubID  : $83 reserved by Document Modus  : Default
- [IDENT_DCM_LESEN](#job-ident-dcm-lesen) - Auslesen der aktuellen Kennung des DCM Datenstandes KWP2000: $1A ReadECUIdentification SubID  : $84 reserved by Document Modus  : Default
- [IDENT_SSECUSON_LESEN](#job-ident-ssecuson-lesen) - ZFLD Softwarenummern auf MPC Seite KWP2000: $1A ReadECUIdentification SubID  : $94 systemSupplierECUSoftwareNumber Modus  : Default
- [IDENT_SSECUSVN_LESEN](#job-ident-ssecusvn-lesen) - Auslesen der NEC Logistik, PAF-DAF und Bootblockkennung, SG darf NICHT im DRIVE Modus sein KWP2000: $1A ReadECUIdentification SubID  : $95 SystemSupplierECUSoftwareVersionNumber Modus  : Default

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

<a id="job-status-versorgungen"></a>
### STATUS_VERSORGUNGEN

Auslesen der aktuellen Spanungspegel KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $01 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLEMME30_WERT | real | Spannungswert an Klemme 30 Quantisierung: ( 25.5V -&gt; 1023 digit, 0.02492 V/digit ) Skalierungsfaktor: ( 1000 ) Wertebereich: ( 0..20 ) Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SENSOR_VERSORGUNG_WERT | real | Spannungswert des Sensors Quantisierung: ( 25.5V -&gt; 1023 digit, 0.02492 V/digit ) Skalierungsfaktor: ( 1000 ) Wertebereich: ( 0...8 ) Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SPANNUNG_RELAIS_WERT | real | Spannungswert des Relais Quantisierung: ( 25.5V -&gt; 1023 digit, 0.02492 V/digit ) Skalierungsfaktor: ( 1000 ) Wertebereich: ( 0...20 ) Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SPANNUNGSUEBERWACHUNG_5V_WERT | real | Spannungsueberwachung 5 Volt Quantisierung: ( 25.5V -&gt; 1023 digit, 0.02492 V/digit ) Skalierungsfaktor: ( 1000 ) Wertebereich: ( 0...5 ) Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SPANNUNGSUEBERWACHUNG_3K3V_WERT | real | Spannungsueberwachung 3,3 Volt Quantisierung: ( 5V -&gt; 1023 digit, 0.00489 V/digit ) Skalierungsfaktor: ( 1000 ) Wertebereich: ( 0...3 ) Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SPANNUNGSUEBERWACHUNG_2K6V_WERT | real | Spannungsueberwachung 2,6 Volt Quantisierung: ( 5V -&gt; 1023 digit, 0.00489 V/digit ) Skalierungsfaktor: ( 1000 ) Wertebereich: ( 0...3 ) Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SPANNUNGSUEBERWACHUNG_1K5V_WERT | real | Spannungsueberwachung 1,5 Volt Quantisierung: ( 5V -&gt; 1023 digit, 0.00489 V/digit ) Skalierungsfaktor: ( 1000 ) Wertebereich: ( 0...3 ) Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SPANNUNG_EINH | string | Einheit der Spannung Einheit: ( Volt ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-afs-os"></a>
### STATUS_AFS_OS

Auslesen verschiedener Betriebssystem (OS, SG) Stati KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $02 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BETRIEBSSYSTEM_MODE_WERT | int | OP Status von ERCOSEK Wertebereich: ( 0,1,2,3,4,5 ) moegliche Zustaende: ( 0 -- &gt; OPM_OFF ) moegliche Zustaende: ( 1 -- &gt; OPM_PREDRIVE ) moegliche Zustaende: ( 2 -- &gt; OPM_POSTRUN ) moegliche Zustaende: ( 3 -- &gt; OPM_DRIVE ) moegliche Zustaende: ( 4 -- &gt; OPM_ERROR ) moegliche Zustaende: ( 5 -- &gt; OPM_INIT ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_BETRIEBSSYSTEM_MODE_TEXT | string | Wertebereich: ( 0,1,2,3,4,5 ) moegliche Zustaende: ( 0 -- &gt; OPM_OFF ) moegliche Zustaende: ( 1 -- &gt; OPM_PREDRIVE ) moegliche Zustaende: ( 2 -- &gt; OPM_POSTRUN ) moegliche Zustaende: ( 3 -- &gt; OPM_DRIVE ) moegliche Zustaende: ( 4 -- &gt; OPM_ERROR ) moegliche Zustaende: ( 5 -- &gt; OPM_INIT ) Textausgabe ueber Tabelle: ( ErcosekModi ) |
| STAT_HL_UEBERGAENGE_WERT | int | interne Uebergaenge Wertebereich: ( 0,1,2,3,4,5,6,7 ) moegliche Zustaende: ( 0 -- &gt; HighLevel_Off ) moegliche Zustaende: ( 1 -- &gt; HighLevel_Init ) moegliche Zustaende: ( 2 -- &gt; HighLevel_Angle_Init ) moegliche Zustaende: ( 3 -- &gt; HighLevel_Ready ) moegliche Zustaende: ( 4 -- &gt; HighLevel_Drive ) moegliche Zustaende: ( 5 -- &gt; HighLevel_Down ) moegliche Zustaende: ( 6 -- &gt; HighLevel_Error ) moegliche Zustaende: ( 7 -- &gt; HighLevel_Pause ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_HL_UEBERGAENGE_TEXT | string | interne Uebergaenge Wertebereich: ( 0,1,2,3,4,5,6,7 ) moegliche Zustaende: ( 0 -- &gt; HighLevel_Off ) moegliche Zustaende: ( 1 -- &gt; HighLevel_Init ) moegliche Zustaende: ( 2 -- &gt; HighLevel_Angle_Init ) moegliche Zustaende: ( 3 -- &gt; HighLevel_Ready ) moegliche Zustaende: ( 4 -- &gt; HighLevel_Drive ) moegliche Zustaende: ( 5 -- &gt; HighLevel_Down ) moegliche Zustaende: ( 6 -- &gt; HighLevel_Error ) moegliche Zustaende: ( 7 -- &gt; HighLevel_Pause ) Textausgabe ueber Tabelle: ( StatusmaschineEingaenge ) |
| STAT_SYSTEMZUSTAND_MPC_WERT | int | stellt den Systemzustand des MPC dar Wertebereich: ( 0,.........,31 ) moegliche Zustaende: ( 0  -- &gt; NOSTATE ) moegliche Zustaende: ( 8  -- &gt; MSGREST ) moegliche Zustaende: ( 9  -- &gt; PREINIT ) moegliche Zustaende: ( 10 -- &gt; HWINIT ) moegliche Zustaende: ( 11 -- &gt; SWINIT ) moegliche Zustaende: ( 12 -- &gt; ANGLEINIT ) moegliche Zustaende: ( 13 -- &gt; DRIVEREADY ) moegliche Zustaende: ( 14 -- &gt; DRIVEUP ) moegliche Zustaende: ( 15 -- &gt; DRIVE ) moegliche Zustaende: ( 16 -- &gt; DRIVEDOWN ) moegliche Zustaende: ( 17 -- &gt; POWERDOWN ) moegliche Zustaende: ( 18 -- &gt; SLEEPIND ) moegliche Zustaende: ( 19 -- &gt; OFF ) moegliche Zustaende: ( 20 -- &gt; RESTART ) moegliche Zustaende: ( 21 -- &gt; GOPAUSE ) moegliche Zustaende: ( 22 -- &gt; PAUSE ) moegliche Zustaende: ( 23 -- &gt; GODRIVE ) moegliche Zustaende: ( 31 -- &gt; ERROR ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SYSTEMZUSTAND_MPC_TEXT | string | stellt den Systemzustand des MPC dar Wertebereich: ( 0,.........,31 ) moegliche Zustaende: ( 0  -- &gt; NOSTATE ) moegliche Zustaende: ( 8  -- &gt; MSGREST ) moegliche Zustaende: ( 9  -- &gt; PREINIT ) moegliche Zustaende: ( 10 -- &gt; HWINIT ) moegliche Zustaende: ( 11 -- &gt; SWINIT ) moegliche Zustaende: ( 12 -- &gt; ANGLEINIT ) moegliche Zustaende: ( 13 -- &gt; DRIVEREADY ) moegliche Zustaende: ( 14 -- &gt; DRIVEUP ) moegliche Zustaende: ( 15 -- &gt; DRIVE ) moegliche Zustaende: ( 16 -- &gt; DRIVEDOWN ) moegliche Zustaende: ( 17 -- &gt; POWERDOWN ) moegliche Zustaende: ( 18 -- &gt; SLEEPIND ) moegliche Zustaende: ( 19 -- &gt; OFF ) moegliche Zustaende: ( 20 -- &gt; RESTART ) moegliche Zustaende: ( 21 -- &gt; GOPAUSE ) moegliche Zustaende: ( 22 -- &gt; PAUSE ) moegliche Zustaende: ( 23 -- &gt; GODRIVE ) moegliche Zustaende: ( 31 -- &gt; ERROR ) Textausgabe ueber Tabelle: ( StatusmaschineZustaende ) |
| STAT_SYSTEMZUSTAND_NEC_WERT | int | stellt den Systemzustand des NEC dar, wie er vom MPC uebertragen wird Wertebereich: ( 0,.........,31 ) moegliche Zustaende: ( 0  -- &gt; NOSTATE ) moegliche Zustaende: ( 8  -- &gt; MSGREST ) moegliche Zustaende: ( 9  -- &gt; PREINIT ) moegliche Zustaende: ( 10 -- &gt; HWINIT ) moegliche Zustaende: ( 11 -- &gt; SWINIT ) moegliche Zustaende: ( 12 -- &gt; ANGLEINIT ) moegliche Zustaende: ( 13 -- &gt; DRIVEREADY ) moegliche Zustaende: ( 14 -- &gt; DRIVEUP ) moegliche Zustaende: ( 15 -- &gt; DRIVE ) moegliche Zustaende: ( 16 -- &gt; DRIVEDOWN ) moegliche Zustaende: ( 17 -- &gt; POWERDOWN ) moegliche Zustaende: ( 18 -- &gt; SLEEPIND ) moegliche Zustaende: ( 19 -- &gt; OFF ) moegliche Zustaende: ( 20 -- &gt; RESTART ) moegliche Zustaende: ( 21 -- &gt; GOPAUSE ) moegliche Zustaende: ( 22 -- &gt; PAUSE ) moegliche Zustaende: ( 23 -- &gt; GODRIVE ) moegliche Zustaende: ( 31 -- &gt; ERROR ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SYSTEMZUSTAND_NEC_TEXT | string | stellt den Systemzustand des NEC dar, wie er vom MPC uebertragen wird Wertebereich: ( 0,.........,31 ) moegliche Zustaende: ( 0  -- &gt; NOSTATE ) moegliche Zustaende: ( 8  -- &gt; MSGREST ) moegliche Zustaende: ( 9  -- &gt; PREINIT ) moegliche Zustaende: ( 10 -- &gt; HWINIT ) moegliche Zustaende: ( 11 -- &gt; SWINIT ) moegliche Zustaende: ( 12 -- &gt; ANGLEINIT ) moegliche Zustaende: ( 13 -- &gt; DRIVEREADY ) moegliche Zustaende: ( 14 -- &gt; DRIVEUP ) moegliche Zustaende: ( 15 -- &gt; DRIVE ) moegliche Zustaende: ( 16 -- &gt; DRIVEDOWN ) moegliche Zustaende: ( 17 -- &gt; POWERDOWN ) moegliche Zustaende: ( 18 -- &gt; SLEEPIND ) moegliche Zustaende: ( 19 -- &gt; OFF ) moegliche Zustaende: ( 20 -- &gt; RESTART ) moegliche Zustaende: ( 21 -- &gt; GOPAUSE ) moegliche Zustaende: ( 22 -- &gt; PAUSE ) moegliche Zustaende: ( 23 -- &gt; GODRIVE ) moegliche Zustaende: ( 31 -- &gt; ERROR ) Textausgabe ueber Tabelle: ( StatusmaschineZustaende ) |
| STAT_SYSTEMZUSTAND_SOLL_NEC_WERT | int | zeigt den Status an, der vom MPC als 'Befehl' zum NEC uebertragen wird Wertebereich: ( 0,.........,31 ) moegliche Zustaende: ( 0  -- &gt; NOSTATE ) moegliche Zustaende: ( 8  -- &gt; MSGREST ) moegliche Zustaende: ( 9  -- &gt; PREINIT ) moegliche Zustaende: ( 10 -- &gt; HWINIT ) moegliche Zustaende: ( 11 -- &gt; SWINIT ) moegliche Zustaende: ( 12 -- &gt; ANGLEINIT ) moegliche Zustaende: ( 13 -- &gt; DRIVEREADY ) moegliche Zustaende: ( 14 -- &gt; DRIVEUP ) moegliche Zustaende: ( 15 -- &gt; DRIVE ) moegliche Zustaende: ( 16 -- &gt; DRIVEDOWN ) moegliche Zustaende: ( 17 -- &gt; POWERDOWN ) moegliche Zustaende: ( 18 -- &gt; SLEEPIND ) moegliche Zustaende: ( 19 -- &gt; OFF ) moegliche Zustaende: ( 20 -- &gt; RESTART ) moegliche Zustaende: ( 21 -- &gt; GOPAUSE ) moegliche Zustaende: ( 22 -- &gt; PAUSE ) moegliche Zustaende: ( 23 -- &gt; GODRIVE ) moegliche Zustaende: ( 31 -- &gt; ERROR ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SYSTEMZUSTAND_SOLL_NEC_TEXT | string | zeigt den Status an, der vom MPC als 'Befehl' zum NEC uebertragen wird Wertebereich: ( 0,.........,31 ) moegliche Zustaende: ( 0  -- &gt; NOSTATE ) moegliche Zustaende: ( 8  -- &gt; MSGREST ) moegliche Zustaende: ( 9  -- &gt; PREINIT ) moegliche Zustaende: ( 10 -- &gt; HWINIT ) moegliche Zustaende: ( 11 -- &gt; SWINIT ) moegliche Zustaende: ( 12 -- &gt; ANGLEINIT ) moegliche Zustaende: ( 13 -- &gt; DRIVEREADY ) moegliche Zustaende: ( 14 -- &gt; DRIVEUP ) moegliche Zustaende: ( 15 -- &gt; DRIVE ) moegliche Zustaende: ( 16 -- &gt; DRIVEDOWN ) moegliche Zustaende: ( 17 -- &gt; POWERDOWN ) moegliche Zustaende: ( 18 -- &gt; SLEEPIND ) moegliche Zustaende: ( 19 -- &gt; OFF ) moegliche Zustaende: ( 20 -- &gt; RESTART ) moegliche Zustaende: ( 21 -- &gt; GOPAUSE ) moegliche Zustaende: ( 22 -- &gt; PAUSE ) moegliche Zustaende: ( 23 -- &gt; GODRIVE ) moegliche Zustaende: ( 31 -- &gt; ERROR ) Textausgabe ueber Tabelle: ( StatusmaschineZustaende ) |
| STAT_NEC_FERTIG_WERT | int | zeigt an ob der NEC die Aufgaben zum aktuellen Zustand abgeschlossen hat Wertebereich: ( 0,1 ) Telegrammlaenge KWP: ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-phasenstroeme"></a>
### STATUS_PHASENSTROEME

Auslesen der Phasenstrome I1,I2,I3 am Stellmotor, Stator KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $04 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHASENSTROM_I1_WERT | real | Phasenstrom I1 am Stator des Stellmotors Quantisierung: ( 0.03125 ) Wertebereich: ( -70A..+70A ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSTROM_I2_WERT | real | Phasenstrom I2 am Stator des Stellmotors Quantisierung: ( 0.03125 ) Wertebereich: ( -70A..+70A ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSTROM_I3_WERT | real | Phasenstrom I3 am Stator des Stellmotors Quantisierung: ( 0.03125 ) Wertebereich: ( -70A..+70A ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSTROM_EINH | string | Einheit des Stroms Einheit: ( Ampere ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-temperaturen"></a>
### STATUS_TEMPERATUREN

Auslesen der Steuergeraetetemperatur KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $05 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ECU_TEMPERATUR_WERT | real | SG-Innentemperatur an Endstufe auf der Platine gemessen Skalierungsfaktor: ( 1 ) Wertebereich: ( -70..+185 ) Einheit: ( Grad Celsius ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_TEMPERATUR_EINH | string | Einheit der Temperatur Einheit: ( Grad Celsius ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-szl"></a>
### STATUS_SZL

Auslesen verschiedener vom SZL gesendeter Werte ueber F-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $06 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SZL_SERIENNUMMER | string | gesendete Seriennummer des SZL CAN-ID: (201 / 0x0C9) Wertebereich: ( 0...99999999 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_SZL_FAHRERLENKWINKEL_OFFSET | real | gesendeter Offsetwert des Fahrerlenkwinkels der beim Abgleich des SZL ermittelt wurde CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [° / s] ) Skalierungsfaktor: ( (PH) = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -180...180 ) Einheit: ( Grad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_SZL_MUX_WERT | int | MUX Alive Zaehler Wertebereich: ( 0..14 ) moegliche Zustaende: ( 0 -- &gt; LWS Seriennummer Teil1 LSB ) moegliche Zustaende: ( 1 -- &gt; LWS Seriennummer Teil2 LSB ) moegliche Zustaende: ( 2 -- &gt; Fehleruebermittlung ) moegliche Zustaende: ( 3 -- &gt; Fehlercode ) moegliche Zustaende: ( 4 -- &gt; Fehlerart ) moegliche Zustaende: ( 5 -- &gt; Submessage ) moegliche Zustaende: ( 6 -- &gt; SZL interne Messgroessen1 ) moegliche Zustaende: ( 7 -- &gt; SZL interne Messgroessen2 ) moegliche Zustaende: ( 8 -- &gt; SZL Teilenummer1 ) moegliche Zustaende: ( 9 -- &gt; SZL Teilenummer2 ) moegliche Zustaende: (10 -- &gt; SZL Teilenummer3 ) moegliche Zustaende: (11 -- &gt; Lenkradgeschw. oben ) moegliche Zustaende: (12 -- &gt; Kodierung Fahrzeug ) moegliche Zustaende: (13 -- &gt; Submessage ) moegliche Zustaende: (14 -- &gt; SZL Offsetwert ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SZL_INFO_WERT | int | SZL Prozessor Info, Ein / Zwei Prozessorsystem Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SZL_INFO_TEXT | string | SZL Prozessor Info, Ein / Zwei Prozessorsystem Textausgabe ueber Tabelle: ( SZLProzInfo ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-sensorcluster"></a>
### STATUS_SENSORCLUSTER

Auslesen verschiedener Stati des Sensorclsuter ueber F-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $07 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GIERRATE_1_STATUS_WERT | int | gesendeter Status der Gierrate 1 CAN-ID: (216 / 0x0D8) Wertebereich: ( 00,01,10,21,20 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GIERRATE_2_STATUS_WERT | int | gesendeter Status der Gierrate 2 CAN-ID: (244 / 0x0F4) Wertebereich: ( 00,01,10,21,20 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_QUERBESCHLEUNIGUNG_1_STATUS_WERT | int | gesendeter Status der Querbeschleunigung 1 CAN-ID: (216 / 0x0D8) Wertebereich: ( 00,01,10,21,20 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_QUERBESCHLEUNIGUNG_2_STATUS_WERT | int | gesendeter Status der Querbeschleunigung 2 CAN-ID: (244 / 0x0F4) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_LAENGSBESCHLEUNIGUNG_STATUS_WERT | int | gesendeter Status der Laengsbeschleunigung CAN-ID: (227 / 0x0E3) Wertebereich: ( 00,01,10,21,20 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MSG_ZAEHLER_1_WERT | int | Botschafts Alive Zaehler 1 CAN-ID: (216 / 0x0D8) Wertebereich: ( 0..14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MSG_ZAEHLER_2_WERT | int | Botschafts Alive Zaehler 2 CAN-ID: (227 / 0x0E3) Wertebereich: ( 0..14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MSG_ZAEHLER_3_WERT | int | Botschafts Alive Zaehler 3 CAN-ID: (244 / 0x0F4) Wertebereich: ( 0..14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-summenlenkwinkel"></a>
### STATUS_SUMMENLENKWINKEL

Auslesen des im SG errechneten Summenlenkwinkels KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $08 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SUMMENLENKWINKEL_WERT | real | SG intern berrechneter Summenlenkwinkel, virtueller Wert da KEIN Sensor vorhanden ist Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Wertebereich: ( -670...+670 ) Einheit: ( Grad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_SUMMENLENKWINKEL_VIRT_WERT | real | SG intern berrechneter Summenlenkwinkel, virtueller Wert da KEIN Sensor vorhanden ist Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Wertebereich: ( -670...+670 ) Einheit: ( Grad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_SUMMENLENKWINKEL_EINH | string | Einheit des Summenwinkels Einheit: ( Grad ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-motorlagewinkel"></a>
### STATUS_MOTORLAGEWINKEL

Auslesen verschiedener Motorlagewinkel KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $09 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_MPC | real | Motorlagewinkel Absoultwert in Grad eingelesen vom MPC Wertebereich: ( -50000...+50000 ) Skalierungsfaktor: ( 1 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_NEC | real | Motorlagewinkel Absoultwert in Grad eingelesen vom NEC Wertebereich: ( -50000...+50000 ) Skalierungsfaktor: ( 1 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MOTORLAGEWINKEL_ABSOLUT_SOLLWERT | real | Motorlagewinkel Absoultwert in Grad, ineterne Groesse von ASCET Wertebereich: ( -50000...+50000 ) Skalierungsfaktor: ( 1 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MOTORLAGEWINKEL_EINH | string | Einheit des Motorwinkels Einheit: ( Grad Motorwinkel ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-fahrerlenkwinkel"></a>
### STATUS_FAHRERLENKWINKEL

Auslesen des Fahrerlenkwinkels vom SZL KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0A InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAHRER_LENKWINKEL_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [grad] ) Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -1439.95Grad...1439.95Grad ) Einheit: ( Grad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_FAHRER_LENKWINKEL_1_ALIVECOUNTER_WERT | int | Alivezaehler des Fahrerlenkwinkels vom SZL ueber F-CAN CAN-ID: (201 / 0x0C9) Ungueltigkeitsbezeichnung: ( 15 ) Wertebereich: ( 0...14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_FAHRERLENKWINKEL_WERT | int | Gueltigkeit des Fahrerlenkwinkels vom SZL moegliche Zustaende: ( 00 -- &gt; in Ordnung ) moegliche Zustaende: ( 01 -- &gt; Radlenkwinkelverifizierung ) moegliche Zustaende: ( 10 -- &gt; Signal fehlerhaft ) Wertebereich: ( 0,1,2 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_FAHRERLENKWINKEL_TEXT | string | Gueltigkeit des Fahrerlenkwinkels vom SZL moegliche Zustaende: ( 00 -- &gt; in Ordnung ) moegliche Zustaende: ( 01 -- &gt; Radlenkwinkelverifizierung ) moegliche Zustaende: ( 10 -- &gt; Signal fehlerhaft ) Wertebereich: ( 0,1,2 ) Textausgabe ueber Tabelle: ( GueLwD ) |
| STAT_FAHRER_LENKWINKEL_REDUNDANT_WERT | real | Fahrerlenkwinkel mit Absicherungszaehler vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [grad] ) Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -1439.95Grad...1439.95Grad ) Einheit: ( Grad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_FAHRER_LENKWINKEL_2_ALIVECOUNTER_WERT | int | Alivezaehler des Fahrerlenkwinkels vom SZL ueber F-CAN CAN-ID: (201 / 0x0C9) Ungueltigkeitsbezeichnung: ( 15 ) Wertebereich: ( 0...14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_FAHRER_LENKWINKEL_EINH | string | Einheit des Fahrerlenkwinkels Einheit: ( Grad Fahrerlenkwinkel ) |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_WERT | real | Fahrerlenkwinkelgeshwindikkeit vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [° / s] ) Skalierungsfaktor: ( (PH)[grad/s] = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -1439.95Grad/s...1439.95Grad/s ) Einheit: ( Grad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_EINH | string | Einheit der Fahrerlenkwinkelgeschwindigkeit Einheit: ( Grad/s ) |
| STAT_LENKRADWINKELSCHIEFSTAND_WERT | real | Lenkradwinkelschiefstand als interne ASCET Var. Wertebereich: ( ???...??? ) Einheit: ( Grad Fahrerlenkwinkel ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_LENKRADWINKELSCHIEFSTAND_EINH | string | Einheit des Lenkradschiefstandes bezogen auf den Fahrerlenkwinkel Einheit: ( Grad Fahrerlenkwinkel ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-geschwindigkeiten"></a>
### STATUS_GESCHWINDIGKEITEN

Auslesen verschiedener Geschwindigkeiten KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0B InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RAD_GESCHWINDIGKEIT_VL_WERT | real | Radgeschwindigkeit vorne links ueber F-CAN CAN-ID: (206 / 0x0CE) Quantisierung: ( (PH) = 0,0625 * (HEX) [ km/h] ) Skalierungsfaktor: ( (PH)[m/s] = 3.6 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -320km/h...320km/h ) Einheit: ( km/h ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_RAD_GESCHWINDIGKEIT_VR_WERT | real | Radgeschwindigkeit vorne links ueber F-CAN CAN-ID: (206 / 0x0CE) Quantisierung: ( (PH) = 0,0625 * (HEX) [ km/h] ) Skalierungsfaktor: ( (PH)[m/s] = 3.6 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -320km/h...320km/h ) Einheit: ( km/h ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_RAD_GESCHWINDIGKEIT_HL_WERT | real | Radgeschwindigkeit vorne links ueber F-CAN CAN-ID: (206 / 0x0CE) Quantisierung: ( (PH) = 0,0625 * (HEX) [ km/h] ) Skalierungsfaktor: ( (PH)[m/s] = 3.6 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -320km/h...320km/h ) Einheit: ( km/h ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_RAD_GESCHWINDIGKEIT_HR_WERT | real | Radgeschwindigkeit vorne links ueber F-CAN CAN-ID: (206 / 0x0CE) Quantisierung: ( (PH) = 0,0625 * (HEX) [ km/h] ) Skalierungsfaktor: ( (PH)[m/s] = 3.6 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -320km/h...320km/h ) Einheit: ( km/h ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_REF_GESCHWINDIGKEIT_WERT | real | Fahrzeuggeschwindigkeit ueber PT-CAN CAN-ID: (416 / 0x1A0) Quantisierung: ( (PH) = 0,1 * (HEX) [ km/h] ) Skalierungsfaktor: ( (PH)[m/s] = 3.6 * (HEX) ) Ungueltigkeitsbezeichnung: ( FFF hex) Wertebereich: ( 0km/h...320km/h ) Einheit: ( km/h ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_RAD_GESCHWINDIGKEIT_EINH | string | Einheit der Radgeschwindigkeiten, vorne links, vorne recht, hinten links, hinten rechts Einheit: ( km/h ) |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_WERT | real | Fahrerlenkwinkelgeshwindikkeit vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [° / s] ) Skalierungsfaktor: ( (PH)[grad/s] = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -1439.95Grad/s...1439.95Grad/s ) Einheit: ( Grad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_FAHRER_LENKWINKEL_GESCHWINDIGKEIT_EINH | string | Einheit der Fahrerlenkwinkelgeschwindigkeit Einheit: ( Grad/s ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-beschleunigung"></a>
### STATUS_BESCHLEUNIGUNG

Auslesen der Quer- und Laengsbeschleunigungswerte KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0C InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QUERBESCHLEUNIGUNG_1_WERT | real | Querbeschleunigung 1 ueber F-CAN CAN-ID: (216 / 0x0D8) Quantisierung: ( (PH) = 0,0001275 * (HEX) - 4.17688[g] ) Skalierungsfaktor: ( (PH)[m/s2] = 1/9.81 * (HEX) ) Ungueltigkeitsbezeichnung: ( FFFF hex) Wertebereich: ( -4.1768g...4.1765g ) Einheit: ( g ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_QUERBESCHLEUNIGUNG_2_WERT | real | Querbeschleunigung 2 ueber F-CAN CAN-ID: (244 / 0x0F4) Quantisierung: ( (PH) = 0,0001275 * (HEX) - 4.17688[g] ) Skalierungsfaktor: ( (PH)[m/s2] = ??? * (HEX) ) Ungueltigkeitsbezeichnung: ( FFFF hex) Wertebereich: ( -4.1768g...4.1765g ) Einheit: ( g ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_LAENGSBESCHLEUNIGUNG_WERT | real | Laengsbeschleunigung 2 ueber F-CAN CAN-ID: (227 / 0x0E3) Quantisierung: ( (PH) = 0,0001275 * (HEX) - 4.17688[g] ) Skalierungsfaktor: ( (PH)[m/s2] = ??? * (HEX) ) Ungueltigkeitsbezeichnung: ( FFFF hex) Wertebereich: ( -4.1768g...4.1765g ) Einheit: ( g ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_BESCHLEUNIGUNG_EINH | string | Einheit der Beschleunigungswert Einheit: ( g ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-gierraten"></a>
### STATUS_GIERRATEN

Auslesen der Gierratenwerte KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0D InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GIERRATE_1_WERT | real | Gierrate 1 ueber F-CAN CAN-ID: (216 / 0x0D8) Quantisierung: ( (PH) = 0,0005 * (HEX) - 163.84[grad/s] ) Skalierungsfaktor: ( (PH)[m/s] = ??? * (HEX) ) Ungueltigkeitsbezeichnung: ( FFFF hex) Wertebereich: ( -163.84grad/s...163.83grad/s ) Einheit: ( grad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_GIERRATE_2_WERT | real | Gierrate 1 ueber F-CAN CAN-ID: (244 / 0x0F4) Quantisierung: ( (PH) = 0,0005 * (HEX) - 163.84[grad/s] ) Skalierungsfaktor: ( (PH)[m/s] = ??? * (HEX) ) Ungueltigkeitsbezeichnung: ( FFFF hex) Wertebereich: ( -163.84grad/s...163.83grad/s ) Einheit: ( grad/s ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_GIERRATE_EINH | string | Einheit der Gierraten 1,2 Einheit: ( Grad/s ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-dsc-info"></a>
### STATUS_DSC_INFO

Auslesen aktueller DSC Stati ueber PT-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0E InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DSC_ALIVECOUNTER_WERT | int | Alivezaehler DSC ueber PT-CAN CAN-ID: (414 / 0x19E) Ungueltigkeitsbezeichnung: ( 15 ) Wertebereich: ( 0...14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_DSC_STATUS_WERT | int | aktueller Status des DSC als Wert ueber PT-CAN CAN-ID: (414 / 0x19E) Wertebereich: ( 0,1,2,3,4,5,6,7 ) moegliche Zustaende: ( 0 -- &gt; in Ordnung, DSC initialisiert ) moegliche Zustaende: ( 1 -- &gt; passiv ) moegliche Zustaende: ( 2 -- &gt; defekt ) moegliche Zustaende: ( 3 -- &gt; LW Verifizierung aktiv ) moegliche Zustaende: ( 4 -- &gt; Traktionsmodus ) moegliche Zustaende: ( 5 -- &gt; reserviert ) moegliche Zustaende: ( 6 -- &gt; Unterspannung DSC ) moegliche Zustaende: ( 7 -- &gt; Signal ungueltig ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_DSC_STATUS_TEXT | string | aktueller Status des DSC als Textausgabe CAN-ID: (414 / 0x19E) Wertebereich: ( 0,1,2,3,4,5,6,7 ) moegliche Zustaende: ( 0 -- &gt; in Ordnung, DSC initialisiert ) moegliche Zustaende: ( 1 -- &gt; passiv ) moegliche Zustaende: ( 2 -- &gt; defekt ) moegliche Zustaende: ( 3 -- &gt; LW Verifizierung aktiv ) moegliche Zustaende: ( 4 -- &gt; Traktionsmodus ) moegliche Zustaende: ( 5 -- &gt; reserviert ) moegliche Zustaende: ( 6 -- &gt; Unterspannung DSC ) moegliche Zustaende: ( 7 -- &gt; Signal ungueltig ) Textausgabe ueber Tabelle: ( GueDSC ) |
| STAT_DSC_REGELUNG_WERT | int | aktueller Status der DSC Regelung als Wert ueber PT-CAN CAN-ID: (414 / 0x19E) Wertebereich: ( 0,1,2,4,8,16,32,64 ) moegliche Zustaende: ( 0 -- &gt; keine DSC Regelung ) moegliche Zustaende: ( 1 -- &gt; ABS Regelung ) moegliche Zustaende: ( 2 -- &gt; ASC Regelung ) moegliche Zustaende: ( 4 -- &gt; DSC Regelung ) moegliche Zustaende: ( 8 -- &gt; HBA Regelung ) moegliche Zustaende: ( 16 -- &gt; MSR Regelung ) moegliche Zustaende: ( 32 -- &gt; EBV Regelung ) moegliche Zustaende: ( 64 -- &gt; FLR Regelung ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_DSC_REGELUNG_TEXT | string | aktueller Status der DSC Regelung als Textausgabe CAN-ID: (414 / 0x19E) Wertebereich: ( 0,1,2,4,8,16,32,64 ) moegliche Zustaende: ( 0 -- &gt; keine DSC Regelung ) moegliche Zustaende: ( 1 -- &gt; ABS Regelung ) moegliche Zustaende: ( 2 -- &gt; ASC Regelung ) moegliche Zustaende: ( 4 -- &gt; DSC Regelung ) moegliche Zustaende: ( 8 -- &gt; HBA Regelung ) moegliche Zustaende: ( 16 -- &gt; MSR Regelung ) moegliche Zustaende: ( 32 -- &gt; EBV Regelung ) moegliche Zustaende: ( 64 -- &gt; FLR Regelung ) Textausgabe ueber Tabelle: ( RegelDSC ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-winkelwerte"></a>
### STATUS_WINKELWERTE

Auslesen verschiedener Winkelwerte, wie Fahrerlenkwinkel, Summenlenkwinkel, Motorlagewinkel KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $0F InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAHRER_LENKWINKEL_WERT | real | Fahrerlenkwinkel vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -1439.95Grad...1439.95Grad ) Einheit: ( Grad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_FAHRER_LENKWINKEL_REDUNDANT_WERT | real | Fahrerlenkwinkel mit Absicherungszaehler vom SZL gesendet ueber F-CAN CAN-ID: (201 / 0x0C9) Quantisierung: ( (PH) = 0,04395 * (HEX) [rad] ) Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Ungueltigkeitsbezeichnung: ( 8000 hex) Wertebereich: ( -1439.95Grad...1439.95Grad ) Einheit: ( Grad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_FAHRER_LENKWINKEL_EINH | string | Einheit des Fahrerlenkwinkels Einheit: ( Grad ) |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_MPC | real | Motorlagewinkel Absoultwert in Grad eingelesen vom MPC Wertebereich: ( -50000...+50000 ) Skalierungsfaktor: ( 1 ) Einheit: ( Grad Motorwinkel ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MOTORLAGEWINKEL_ABSOLUT_ISTWERT_NEC | real | Motorlagewinkel Absoultwert in Grad eingelesen vom NEC Wertebereich: ( -50000...+50000 ) Skalierungsfaktor: ( 1 ) Einheit: ( Grad Motorwinkel ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MOTORLAGEWINKEL_ABSOLUT_SOLLWERT | real | Motorlagewinkel Absoultwert in Grad, interne Groesse von ASCET Wertebereich: ( -50000...+50000 ) Skalierungsfaktor: ( 1 ) Einheit: ( Grad Motorwinkel ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MOTORLAGEWINKEL_EINH | string | Einheit des Motorlagewinkels Einheit: ( Grad Motorwinkel ) |
| STAT_SUMMENLENKWINKEL_ABSOLUT_WERT | real | SG intern berrechneter Summenlenkwinkel, virtueller Wert da KEIN Sensor vorhanden ist Skalierungsfaktor: ( (PH)[grad] = 180 / 3.141592 * (HEX) ) Wertebereich: ( -670...+670 ) Einheit: ( Grad ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_SUMMENLENKWINKEL_EINH | string | Einheit des Summenlenkwinkels Einheit: ( Grad ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-phasenspannungen"></a>
### STATUS_PHASENSPANNUNGEN

Auslesen der Phasenspanngen U1,U2,U3 am Stellmotor, Stator KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $10 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHASENSPANNUNG_U1_WERT | real | Sapnnung U1 am Stator des Stellmotors Quantisierung: ( 0.02492 ) Wertebereich: ( 0..25.5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSPANNUNG_U2_WERT | real | Sapnnung U2 am Stator des Stellmotors Quantisierung: ( 0.02492 ) Wertebereich: ( 0..25.5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSPANNUNG_U3_WERT | real | Sapnnung U3 am Stator des Stellmotors Quantisierung: ( 0.02492 ) Wertebereich: ( 0..25.5 ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSPANNUNG_EINH | string | Einheit der Spannung Einheit: ( Volt ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-alive-info"></a>
### STATUS_ALIVE_INFO

Auslesen verschiedener ALIVE Zaehler KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $13 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AFS_ALIVE | int | Alivezaehler vom AFS Wertebereich: ( 0..14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AFS_SPI_ALIVE_WERT | int | SG interne Alivezaehler, SPI Wertebereich: ( 0..255 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AFS_SPI_MOTORLAGEWINKEL_NEC_ALIVE_WERT | int | SG interne Alivezaehler, SPI Wertebereich: ( 0..255 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_FAHRER_LENKWINKEL_1_ALIVECOUNTER_WERT | int | Alivezaehler des Fahrerlenkwinkels vom SZL ueber F-CAN CAN-ID: (201 / 0x0C9) Ungueltigkeitsbezeichnung: ( 15 ) Wertebereich: ( 0...14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_FAHRER_LENKWINKEL_2_ALIVECOUNTER_WERT | int | Alivezaehler des Fahrerlenkwinkels vom SZL ueber F-CAN CAN-ID: (201 / 0x0C9) Ungueltigkeitsbezeichnung: ( 15 ) Wertebereich: ( 0...14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SENSORCLUSTER_1_ALIVECOUNTER_WERT | int | Botschafts Alive Zaehler 1 CAN-ID: (216 / 0x0D8) Wertebereich: ( 0..14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SENSORCLUSTER_2_ALIVECOUNTER_WERT | int | Botschafts Alive Zaehler 2 CAN-ID: (227 / 0x0E3) Wertebereich: ( 0..14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SENSORCLUSTER_3_ALIVECOUNTER_WERT | int | Botschafts Alive Zaehler 3 CAN-ID: (244 / 0x0F4) Wertebereich: ( 0..14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_DSC_ALIVECOUNTER_WERT | int | Alivezaehler des DSC Wertebereich: ( 0..14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-sensorcluster-info"></a>
### STATUS_SENSORCLUSTER_INFO

Status und Diagnoseinfos ueber den Sensorclsuter KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $15 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSORCLUSTER_TYP_WERT | int | Typ des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0,1,2,3,4,5,8,9,10,11,13,14 ) moegliche Zustaende: ( 0x00 -- &gt; Sensorcluster 3.6 ) moegliche Zustaende: ( 0x01 -- &gt; Sensorcluster 3.7 ) moegliche Zustaende: ( 0x02 -- &gt; Sensorcluster 3.8 ) moegliche Zustaende: ( 0x03 -- &gt; Sensorcluster 3.9 ) moegliche Zustaende: ( 0x04 -- &gt; Sensorcluster 3.10 ) moegliche Zustaende: ( 0x05 -- &gt; Sensorcluster 3.11 ) moegliche Zustaende: ( 0x08 -- &gt; Sensorcluster 3.0 ) moegliche Zustaende: ( 0x09 -- &gt; Sensorcluster 3.1 ) moegliche Zustaende: ( 0x0A -- &gt; Sensorcluster 3.2 ) moegliche Zustaende: ( 0x0B -- &gt; Sensorcluster 3.3 ) moegliche Zustaende: ( 0x0D -- &gt; TRW_YAW/LAT ) moegliche Zustaende: ( 0x0E -- &gt; TRW_YAW/LAT/LONG ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SENSORCLUSTER_TYP_TEXT | string | Typ des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0,1,2,3,4,5,8,9,10,11,13,14 ) moegliche Zustaende: ( 0x00 -- &gt; Sensorcluster 3.6 ) moegliche Zustaende: ( 0x01 -- &gt; Sensorcluster 3.7 ) moegliche Zustaende: ( 0x02 -- &gt; Sensorcluster 3.8 ) moegliche Zustaende: ( 0x03 -- &gt; Sensorcluster 3.9 ) moegliche Zustaende: ( 0x04 -- &gt; Sensorcluster 3.10 ) moegliche Zustaende: ( 0x05 -- &gt; Sensorcluster 3.11 ) moegliche Zustaende: ( 0x08 -- &gt; Sensorcluster 3.0 ) moegliche Zustaende: ( 0x09 -- &gt; Sensorcluster 3.1 ) moegliche Zustaende: ( 0x0A -- &gt; Sensorcluster 3.2 ) moegliche Zustaende: ( 0x0B -- &gt; Sensorcluster 3.3 ) moegliche Zustaende: ( 0x0D -- &gt; TRW_YAW/LAT ) moegliche Zustaende: ( 0x0E -- &gt; TRW_YAW/LAT/LONG ) Textausgabe ueber Tabelle: ( SensorClusterTyp ) |
| STAT_SENSORCLUSTER_DIAG_WERT | int | Diagnosedaten des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0...255 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SENSORCLUSTER_1_WERT | int | Status 1 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; CRC Fehler ) moegliche Zustaende: ( 0x02 -- &gt; Ueberspannnung ) moegliche Zustaende: ( 0x04 -- &gt; Unterspannung ) moegliche Zustaende: ( 0x08 -- &gt; Sensor-interner Fehler ) moegliche Zustaende: ( 0x10 -- &gt; Synchronisationsfehler ) moegliche Zustaende: ( 0x20 -- &gt; Synchronisation Underflow ) moegliche Zustaende: ( 0x40 -- &gt; Synchronisation Overflow ) moegliche Zustaende: ( 0x80 -- &gt; Bus-Off Fehler ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SENSORCLUSTER_1_BIT0_TEXT | string | Status 1 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; CRC Fehler ) Textausgabe ueber Tabelle: ( SensorClusterStatus1 ) |
| STAT_SENSORCLUSTER_1_BIT1_TEXT | string | Status 1 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Ueberspannnung ) Textausgabe ueber Tabelle: ( SensorClusterStatus1 ) |
| STAT_SENSORCLUSTER_1_BIT2_TEXT | string | Status 1 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Unterspannung ) Textausgabe ueber Tabelle: ( SensorClusterStatus1 ) |
| STAT_SENSORCLUSTER_1_BIT3_TEXT | string | Status 1 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Sensor-interner Fehler ) Textausgabe ueber Tabelle: ( SensorClusterStatus1 ) |
| STAT_SENSORCLUSTER_1_BIT4_TEXT | string | Status 1 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Synchronisationsfehler ) Textausgabe ueber Tabelle: ( SensorClusterStatus1 ) |
| STAT_SENSORCLUSTER_1_BIT5_TEXT | string | Status 1 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Synchronisation Underflow ) Textausgabe ueber Tabelle: ( SensorClusterStatus1 ) |
| STAT_SENSORCLUSTER_1_BIT6_TEXT | string | Status 1 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Synchronisation Overflow ) Textausgabe ueber Tabelle: ( SensorClusterStatus1 ) |
| STAT_SENSORCLUSTER_1_BIT7_TEXT | string | Status 1 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Bus-Off Fehler ) Textausgabe ueber Tabelle: ( SensorClusterStatus1 ) |
| STAT_SENSORCLUSTER_2_WERT | int | Status 2 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Fehler Gierrate 1 ) moegliche Zustaende: ( 0x02 -- &gt; Fehler Querbeschleunigung 1 ) moegliche Zustaende: ( 0x04 -- &gt; Fehler Gierbeschleunigung ) moegliche Zustaende: ( 0x08 -- &gt; Fehler Laengsbeschleunigung ) moegliche Zustaende: ( 0x10 -- &gt; Fehler Gierrate 2 ) moegliche Zustaende: ( 0x20 -- &gt; Fehler Querbeschleunigung 2 ) moegliche Zustaende: ( 0x40 -- &gt; reserviert ) moegliche Zustaende: ( 0x80 -- &gt; reserviert ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SENSORCLUSTER_2_BIT0_TEXT | string | Status 2 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Fehler Gierrate 1 ) Textausgabe ueber Tabelle: ( SensorClusterStatus2 ) |
| STAT_SENSORCLUSTER_2_BIT1_TEXT | string | Status 2 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Fehler Querbeschleunigung 1 ) Textausgabe ueber Tabelle: ( SensorClusterStatus2 ) |
| STAT_SENSORCLUSTER_2_BIT2_TEXT | string | Status 2 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Fehler Gierbeschleunigung ) Textausgabe ueber Tabelle: ( SensorClusterStatus2 ) |
| STAT_SENSORCLUSTER_2_BIT3_TEXT | string | Status 2 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Fehler Laengsbeschleunigung ) Textausgabe ueber Tabelle: ( SensorClusterStatus2 ) |
| STAT_SENSORCLUSTER_2_BIT4_TEXT | string | Status 2 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Fehler Gierrate 2 ) Textausgabe ueber Tabelle: ( SensorClusterStatus2 ) |
| STAT_SENSORCLUSTER_2_BIT5_TEXT | string | Status 2 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Fehler Querbeschleunigung 2 ) Textausgabe ueber Tabelle: ( SensorClusterStatus2 ) |
| STAT_SENSORCLUSTER_2_BIT6_TEXT | string | Status 2 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x40 -- &gt; reserviert ) Textausgabe ueber Tabelle: ( SensorClusterStatus2 ) |
| STAT_SENSORCLUSTER_2_BIT7_TEXT | string | Status 2 des Sensorclusters ueber F-CAN CAN-ID: (357 / 0x165) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x80 -- &gt; reserviert ) Textausgabe ueber Tabelle: ( SensorClusterStatus2 ) |
| STAT_GIERRATE_1_WERT | int | Status 1 des Sensorclusters ueber F-CAN CAN-ID: (216 / 0xD8) Wertebereich: ( 00,01,10,21,20 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GIERRATE_1_BIT01_TEXT | string | Status Gierrate 1 ueber F-CAN CAN-ID: (216 / 0xD8) Wertebereich: ( 0, 1, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| STAT_GIERRATE_1_BIT2_TEXT | string | Status Gierrate 1 ueber F-CAN CAN-ID: (216 / 0xD8) Wertebereich: ( 0x20, 0x21 ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| STAT_QUERBESCHLEUNIGUNG_1_WERT | int | Status Querbeschleunigung 1 des Sensorclusters ueber F-CAN CAN-ID: (216 / 0xD8) Wertebereich: ( 00,01,10,21,20 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_QUERBESCHLEUNIGUNG_1_BIT01_TEXT | string | Status Querbeschleunigung 1 ueber F-CAN CAN-ID: (216 / 0xD8) Wertebereich: ( 0, 1, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| STAT_QUERBESCHLEUNIGUNG_1_BIT2_TEXT | string | Status Querbeschleunigung 1 ueber F-CAN CAN-ID: (216 / 0xD8) Wertebereich: ( 0x20, 0x21 ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| STAT_GIERWINKEL_BESCHLEUNIGUNG_WERT | int | Status Gierwinkelbeschleunigung ueber F-CAN CAN-ID: (227 / 0xE3) Wertebereich: ( 00,01,10,21,20 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GIERWINKEL_BESCHLEUNIGUNG_BIT01_TEXT | string | Status Gierwinkelbeschleunigung ueber F-CAN CAN-ID: (227 / 0xE3) Wertebereich: ( 0, 1, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| STAT_GIERWINKEL_BESCHLEUNIGUNG_BIT2_TEXT | string | Status Gierwinkelbeschleunigung ueber F-CAN CAN-ID: (227 / 0xE3) Wertebereich: ( 0x20, 0x21 ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| STAT_LAENGSBESCHLEUNIGUNG_WERT | int | Status Laengsbeschleunigung ueber F-CAN CAN-ID: (227 / 0xE3) Wertebereich: ( 00,01,10,21,20 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_LAENGSBESCHLEUNIGUNG_BIT01_TEXT | string | Status Laengsbeschleunigung ueber F-CAN CAN-ID: (227 / 0xE3) Wertebereich: ( 0, 1, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| STAT_LAENGSBESCHLEUNIGUNG_BIT2_TEXT | string | Status Laengsbeschleunigung ueber F-CAN CAN-ID: (227 / 0xE3) Wertebereich: ( 0x20, 0x21 ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| STAT_GIERRATE_2_WERT | int | Status 1 des Sensorclusters ueber F-CAN CAN-ID: (244 / 0xF4) Wertebereich: ( 00,01,10,21,20 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GIERRATE_2_BIT01_TEXT | string | Status Gierrate 2 ueber F-CAN CAN-ID: (244 / 0xF4) Wertebereich: ( 0, 1, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| STAT_GIERRATE_2_BIT2_TEXT | string | Status Gierrate 2 ueber F-CAN CAN-ID: (244 / 0xF4) Wertebereich: ( 0x20, 0x21 ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| STAT_QUERBESCHLEUNIGUNG_2_WERT | int | Status Querbeschleunigung 2 des Sensorclusters ueber F-CAN CAN-ID: (244 / 0xF4) Wertebereich: ( 00,01,10,21,20 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_QUERBESCHLEUNIGUNG_2_BIT01_TEXT | string | Status Querbeschleunigung 2 ueber F-CAN CAN-ID: (244 / 0xF4) Wertebereich: ( 0, 1, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Signal wie spezifiziert ) moegliche Zustaende: ( 0x01 -- &gt; Sensor nicht verfuegbar ) moegliche Zustaende: ( 0x10 -- &gt; Signalfehler ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| STAT_QUERBESCHLEUNIGUNG_2_BIT2_TEXT | string | Status Querbeschleunigung 2 ueber F-CAN CAN-ID: (244 / 0xF4) Wertebereich: ( 0x20, 0x21 ) moegliche Zustaende: ( 0x21 -- &gt; Initialisierung laeuft ) moegliche Zustaende: ( 0x20 -- &gt; Initialisierung beendet ) Textausgabe ueber Tabelle: ( SensClusterSignalStatus ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-cas-info"></a>
### STATUS_CAS_INFO

Auslesen der vom CAS gesendeten Fahrgestellnummer ueber PT-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $16 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CAS_FAHRGESTELLNR_WERT | string | vom AFS eingelesene Fahrgestellnummer ueber PT-CAN CAN-ID: (896 / 0x380) Telegrammlaenge KWP: ( 8 Byte ) |
| STAT_GUELTIGKEIT_CAS_FAHRGESTELLNR_WERT | int | Gueltigkeit der Fahrgestellnummer CAN Botschaft vom CAS ueber PT-CAN CAN-ID: (896 / 0x380) Wertebereich: ( 00,02,04,08,10,20,40,80 ) moegliche Zustaende: ( 0x00 -- &gt; Botschaft i.o. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) moegliche Zustaende: ( 0x08 -- &gt; Timeout - Botschaft faellt fuer 1 Abtastzyklus Zyklus aus ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) moegliche Zustaende: ( 0x80 -- &gt; Fehler von CRC Alive Fehlerwert Botschaft nie empfangen ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_CAS_FAHRGESTELLNR_TEXT | string | Gueltigkeit der Fahrgestellnummer CAN Botschaft vom CAS ueber PT-CAN CAN-ID: (896 / 0x380) Wertebereich: ( 00,02,04,08,10,20,40,80 ) moegliche Zustaende: ( 0x00 -- &gt; Botschaft i.o. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) moegliche Zustaende: ( 0x08 -- &gt; Timeout - Botschaft faellt fuer 1 Abtastzyklus Zyklus aus ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) moegliche Zustaende: ( 0x80 -- &gt; Fehler von CRC Alive Fehlerwert Botschaft nie empfangen ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-eco-servo"></a>
### STATUS_ECO_SERVO

Auslesen des aktuell anliegenden Stromes am ECO Ventil und dessen Status KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $17 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ECO_AKTUELL_WERT | int | aktueller Status des ECO Ventils Wertebereich: ( 0,1,2,3,5,7,26,87 ) moegliche Zustaende: ( 0 -- &gt;  'KFA_GEN'  , i.O. Ventile regeln den Strom korrekt ein ) moegliche Zustaende: ( 1 -- &gt;  'KFA_SCP'  , Kurzschluss einer Ventilleitung nach U_Bat ) moegliche Zustaende: ( 2 -- &gt;  'KFA_SCM'  , Kurzschluss einer Ventilleitung nach GND ) moegliche Zustaende: ( 3 -- &gt;  'KFA_OC'   , offene Leitung / Unterbrechung eines Stromkreises ) moegliche Zustaende: ( 5 -- &gt;  'KFA_SCMOC', Kurzschluss nach GND oder Unterbrechung der Leitung ) moegliche Zustaende: ( 7 -- &gt;  'KFA_TLOW' , Strom kann nicht eingestellt werden, Ventilstrom zu niedrig ) moegliche Zustaende: ( 26 -- &gt; 'KFA_SC'   , Kurzschluss zwischen den Ventilleitungen ) moegliche Zustaende: ( 87 -- &gt; 'KFA_GEN'  , Uebertemperatur Endstufe CG207 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ECO_AKTUELL_TEXT | string | aktueller Status des ECO Ventils Wertebereich: ( 0,1,2,3,5,7,26,87 ) moegliche Zustaende: ( 0 -- &gt;  'KFA_GEN'  , i.O. Ventile regeln den Strom korrekt ein ) moegliche Zustaende: ( 1 -- &gt;  'KFA_SCP'  , Kurzschluss einer Ventilleitung nach U_Bat ) moegliche Zustaende: ( 2 -- &gt;  'KFA_SCM'  , Kurzschluss einer Ventilleitung nach GND ) moegliche Zustaende: ( 3 -- &gt;  'KFA_OC'   , offene Leitung / Unterbrechung eines Stromkreises ) moegliche Zustaende: ( 5 -- &gt;  'KFA_SCMOC', Kurzschluss nach GND oder Unterbrechung der Leitung ) moegliche Zustaende: ( 7 -- &gt;  'KFA_TLOW' , Strom kann nicht eingestellt werden, Ventilstrom zu niedrig ) moegliche Zustaende: ( 26 -- &gt; 'KFA_SC'   , Kurzschluss zwischen den Ventilleitungen ) moegliche Zustaende: ( 87 -- &gt; 'KFA_GEN'  , Uebertemperatur Endstufe CG207 ) Textausgabe ueber Tabelle: ( ECOSERVO ) |
| STAT_SERVO_AKTUELL_WERT | int | aktueller Status des SERVO Ventils Wertebereich: ( 0,1,2,3,5,7,26,87 ) moegliche Zustaende: ( 0 -- &gt;  'KFA_GEN'  , i.O. Ventile regeln den Strom korrekt ein ) moegliche Zustaende: ( 1 -- &gt;  'KFA_SCP'  , Kurzschluss einer Ventilleitung nach U_Bat ) moegliche Zustaende: ( 2 -- &gt;  'KFA_SCM'  , Kurzschluss einer Ventilleitung nach GND ) moegliche Zustaende: ( 3 -- &gt;  'KFA_OC'   , offene Leitung / Unterbrechung eines Stromkreises ) moegliche Zustaende: ( 5 -- &gt;  'KFA_SCMOC', Kurzschluss nach GND oder Unterbrechung der Leitung ) moegliche Zustaende: ( 7 -- &gt;  'KFA_TLOW' , Strom kann nicht eingestellt werden, Ventilstrom zu niedrig ) moegliche Zustaende: ( 26 -- &gt; 'KFA_SC'   , Kurzschluss zwischen den Ventilleitungen ) moegliche Zustaende: ( 87 -- &gt; 'KFA_GEN'  , Uebertemperatur Endstufe CG207 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SERVO_AKTUELL_TEXT | string | aktueller Status des SERVO Ventils Wertebereich: ( 0,1,2,3,5,7,26,87 ) moegliche Zustaende: ( 0 -- &gt;  'KFA_GEN'  , i.O. Ventile regeln den Strom korrekt ein ) moegliche Zustaende: ( 1 -- &gt;  'KFA_SCP'  , Kurzschluss einer Ventilleitung nach U_Bat ) moegliche Zustaende: ( 2 -- &gt;  'KFA_SCM'  , Kurzschluss einer Ventilleitung nach GND ) moegliche Zustaende: ( 3 -- &gt;  'KFA_OC'   , offene Leitung / Unterbrechung eines Stromkreises ) moegliche Zustaende: ( 5 -- &gt;  'KFA_SCMOC', Kurzschluss nach GND oder Unterbrechung der Leitung ) moegliche Zustaende: ( 7 -- &gt;  'KFA_TLOW' , Strom kann nicht eingestellt werden, Ventilstrom zu niedrig ) moegliche Zustaende: ( 26 -- &gt; 'KFA_SC'   , Kurzschluss zwischen den Ventilleitungen ) moegliche Zustaende: ( 87 -- &gt; 'KFA_GEN'  , Uebertemperatur Endstufe CG207 ) Textausgabe ueber Tabelle: ( ECOSERVO ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-eco-ventil"></a>
### STATUS_ECO_VENTIL

Auslesen des aktuell anliegenden Stromes am ECO Ventil und dessen Status KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $18 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ECO_STROM_WERT | real | aktuell gestellter Strom am ECO Ventil Skalierungsfaktor: ( 1000 ) Wertebereich: ( 0...1000 ) Einheit: ( mA ) Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_ECO_STROM_EINH | string | Einheit des Stromes Einheit: ( mA ) |
| STAT_ECO_AKTUELL_WERT | int | aktueller Status des ECO Ventils Wertebereich: ( 0,1,2,3,5,7,26,87 ) moegliche Zustaende: ( 0 -- &gt;  'KFA_GEN'  , i.O. Ventile regeln den Strom korrekt ein ) moegliche Zustaende: ( 1 -- &gt;  'KFA_SCP'  , Kurzschluss einer Ventilleitung nach U_Bat ) moegliche Zustaende: ( 2 -- &gt;  'KFA_SCM'  , Kurzschluss einer Ventilleitung nach GND ) moegliche Zustaende: ( 3 -- &gt;  'KFA_OC'   , offene Leitung / Unterbrechung eines Stromkreises ) moegliche Zustaende: ( 5 -- &gt;  'KFA_SCMOC', Kurzschluss nach GND oder Unterbrechung der Leitung ) moegliche Zustaende: ( 7 -- &gt;  'KFA_TLOW' , Strom kann nicht eingestellt werden, Ventilstrom zu niedrig ) moegliche Zustaende: ( 26 -- &gt; 'KFA_SC'   , Kurzschluss zwischen den Ventilleitungen ) moegliche Zustaende: ( 87 -- &gt; 'KFA_GEN'  , Uebertemperatur Endstufe CG207 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ECO_AKTUELL_TEXT | string | aktueller Status des ECO Ventils Wertebereich: ( 0,1,2,3,5,7,26,87 ) moegliche Zustaende: ( 0 -- &gt;  'KFA_GEN'  , i.O. Ventile regeln den Strom korrekt ein ) moegliche Zustaende: ( 1 -- &gt;  'KFA_SCP'  , Kurzschluss einer Ventilleitung nach U_Bat ) moegliche Zustaende: ( 2 -- &gt;  'KFA_SCM'  , Kurzschluss einer Ventilleitung nach GND ) moegliche Zustaende: ( 3 -- &gt;  'KFA_OC'   , offene Leitung / Unterbrechung eines Stromkreises ) moegliche Zustaende: ( 5 -- &gt;  'KFA_SCMOC', Kurzschluss nach GND oder Unterbrechung der Leitung ) moegliche Zustaende: ( 7 -- &gt;  'KFA_TLOW' , Strom kann nicht eingestellt werden, Ventilstrom zu niedrig ) moegliche Zustaende: ( 26 -- &gt; 'KFA_SC'   , Kurzschluss zwischen den Ventilleitungen ) moegliche Zustaende: ( 87 -- &gt; 'KFA_GEN'  , Uebertemperatur Endstufe CG207 ) Textausgabe ueber Tabelle: ( ECOSERVO ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-servo-ventil"></a>
### STATUS_SERVO_VENTIL

Auslesen des aktuell anliegenden Stromes am SERVO Ventil und dessen Status KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $19 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERVO_STROM_WERT | real | aktuell gestellter Strom am SERVO Ventil Skalierungsfaktor: ( 1000 ) Wertebereich: ( 0...1000 ) Einheit: ( mA ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SERVO_STROM_EINH | string | Einheit des Stromes Einheit: ( mAmpere ) |
| STAT_SERVO_AKTUELL_WERT | int | aktueller Status des SERVO Ventils Wertebereich: ( 0,1,2,3,5,7,26,87 ) moegliche Zustaende: ( 0 -- &gt;  'KFA_GEN'  , i.O. Ventile regeln den Strom korrekt ein ) moegliche Zustaende: ( 1 -- &gt;  'KFA_SCP'  , Kurzschluss einer Ventilleitung nach U_Bat ) moegliche Zustaende: ( 2 -- &gt;  'KFA_SCM'  , Kurzschluss einer Ventilleitung nach GND ) moegliche Zustaende: ( 3 -- &gt;  'KFA_OC'   , offene Leitung / Unterbrechung eines Stromkreises ) moegliche Zustaende: ( 5 -- &gt;  'KFA_SCMOC', Kurzschluss nach GND oder Unterbrechung der Leitung ) moegliche Zustaende: ( 7 -- &gt;  'KFA_TLOW' , Strom kann nicht eingestellt werden, Ventilstrom zu niedrig ) moegliche Zustaende: ( 26 -- &gt; 'KFA_SC'   , Kurzschluss zwischen den Ventilleitungen ) moegliche Zustaende: ( 87 -- &gt; 'KFA_GEN'  , Uebertemperatur Endstufe CG207 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SERVO_AKTUELL_TEXT | string | aktueller Status des SERVO Ventils Wertebereich: ( 0,1,2,3,5,7,26,87 ) moegliche Zustaende: ( 0 -- &gt;  'KFA_GEN'  , i.O. Ventile regeln den Strom korrekt ein ) moegliche Zustaende: ( 1 -- &gt;  'KFA_SCP'  , Kurzschluss einer Ventilleitung nach U_Bat ) moegliche Zustaende: ( 2 -- &gt;  'KFA_SCM'  , Kurzschluss einer Ventilleitung nach GND ) moegliche Zustaende: ( 3 -- &gt;  'KFA_OC'   , offene Leitung / Unterbrechung eines Stromkreises ) moegliche Zustaende: ( 5 -- &gt;  'KFA_SCMOC', Kurzschluss nach GND oder Unterbrechung der Leitung ) moegliche Zustaende: ( 7 -- &gt;  'KFA_TLOW' , Strom kann nicht eingestellt werden, Ventilstrom zu niedrig ) moegliche Zustaende: ( 26 -- &gt; 'KFA_SC'   , Kurzschluss zwischen den Ventilleitungen ) moegliche Zustaende: ( 87 -- &gt; 'KFA_GEN'  , Uebertemperatur Endstufe CG207 ) Textausgabe ueber Tabelle: ( ECOSERVO ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-ptcan-signal-fehler"></a>
### STATUS_PTCAN_SIGNAL_FEHLER

diverse vom AFS eingelesene PTCAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $1B InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DSC_STATUS_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (414 / 0x19E) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_DSC_STATUS_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (414 / 0x19E) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_DSC_STATUS_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (414 / 0x19E) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_DSC_STATUS_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (414 / 0x19E) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_DSC_STATUS_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (414 / 0x19E) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_DSC_STATUS_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (414 / 0x19E) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_DSC_STATUS_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (414 / 0x19E) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_DSC_STATUS_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (414 / 0x19E) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_DSC_STATUS_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (414 / 0x19E) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GESCHWINDIKHEITEN_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (416 / 0x1A0) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GESCHWINDIKHEITEN_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (416 / 0x1A0) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GESCHWINDIKHEITEN_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (416 / 0x1A0) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GESCHWINDIKHEITEN_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (416 / 0x1A0) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GESCHWINDIKHEITEN_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (416 / 0x1A0) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GESCHWINDIKHEITEN_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (416 / 0x1A0) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GESCHWINDIKHEITEN_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (416 / 0x1A0) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GESCHWINDIKHEITEN_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (416 / 0x1A0) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GESCHWINDIKHEITEN_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (416 / 0x1A0) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT1_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (168 / 0x0A8) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MOTORMOMENT1_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (168 / 0x0A8) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT1_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (168 / 0x0A8) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT1_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (168 / 0x0A8) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT1_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (168 / 0x0A8) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT1_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (168 / 0x0A8) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT1_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (168 / 0x0A8) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT1_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (168 / 0x0A8) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT1_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (168 / 0x0A8) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT3_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (170 / 0x0AA) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MOTORMOMENT3_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (170 / 0x0AA) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT3_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (170 / 0x0AA) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT3_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (170 / 0x0AA) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT3_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (170 / 0x0AA) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT3_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (170 / 0x0AA) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT3_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (170 / 0x0AA) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT3_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (170 / 0x0AA) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORMOMENT3_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (170 / 0x0AA) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORDATEN_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (464 / 0x1D0) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MOTORDATEN_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (464 / 0x1D0) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORDATEN_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (464 / 0x1D0) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORDATEN_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (464 / 0x1D0) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORDATEN_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (464 / 0x1D0) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORDATEN_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (464 / 0x1D0) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORDATEN_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (464 / 0x1D0) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORDATEN_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (464 / 0x1D0) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_MOTORDATEN_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (464 / 0x1D0) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GETRIEBEDATEN_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (186 / 0x0BA) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GETRIEBEDATEN_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (186 / 0x0BA) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GETRIEBEDATEN_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (186 / 0x0BA) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GETRIEBEDATEN_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (186 / 0x0BA) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GETRIEBEDATEN_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (186 / 0x0BA) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GETRIEBEDATEN_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (186 / 0x0BA) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GETRIEBEDATEN_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (186 / 0x0BA) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GETRIEBEDATEN_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (186 / 0x0BA) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_GETRIEBEDATEN_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (186 / 0x0BA) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KUPPLUNGSDATEN_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (188 / 0x0BC) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_KUPPLUNGSDATEN_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (188 / 0x0BC) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KUPPLUNGSDATEN_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (188 / 0x0BC) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KUPPLUNGSDATEN_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (188 / 0x0BC) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KUPPLUNGSDATEN_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (188 / 0x0BC) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KUPPLUNGSDATEN_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (188 / 0x0BC) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KUPPLUNGSDATEN_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (188 / 0x0BC) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KUPPLUNGSDATEN_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (188 / 0x0BC) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KUPPLUNGSDATEN_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (188 / 0x0BC) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ANHAENGERDATEN_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (740 / 0x2E4) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ANHAENGERDATEN_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (740 / 0x2E4) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ANHAENGERDATEN_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (740 / 0x2E4) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ANHAENGERDATEN_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (740 / 0x2E4) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ANHAENGERDATEN_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (740 / 0x2E4) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ANHAENGERDATEN_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (740 / 0x2E4) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ANHAENGERDATEN_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (740 / 0x2E4) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ANHAENGERDATEN_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (740 / 0x2E4) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ANHAENGERDATEN_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (740 / 0x2E4) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KLEMMEMSTATUS_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_KLEMMEMSTATUS_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KLEMMEMSTATUS_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KLEMMEMSTATUS_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KLEMMEMSTATUS_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KLEMMEMSTATUS_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KLEMMEMSTATUS_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KLEMMEMSTATUS_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_KLEMMEMSTATUS_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_FGNR_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_FGNR_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_AFS_STATUS_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (508 / 0x1FC) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AFS_STATUS_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (508 / 0x1FC) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_AFS_STATUS_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (508 / 0x1FC) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_AFS_STATUS_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (508 / 0x1FC) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_AFS_STATUS_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (508 / 0x1FC) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_AFS_STATUS_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (508 / 0x1FC) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_AFS_STATUS_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (508 / 0x1FC) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_AFS_STATUS_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (508 / 0x1FC) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_AFS_STATUS_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (508 / 0x1FC) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ARS_STATUS_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (428 / 0x1AC) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ARS_STATUS_CAN_FEHLER_BIT0_TEXT | string | PTCAN Signalfehler CAN-ID: (428 / 0x1AC) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ARS_STATUS_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (428 / 0x1AC) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ARS_STATUS_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (428 / 0x1AC) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ARS_STATUS_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (428 / 0x1AC) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ARS_STATUS_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (428 / 0x1AC) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ARS_STATUS_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (428 / 0x1AC) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ARS_STATUS_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (428 / 0x1AC) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_ARS_STATUS_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (428 / 0x1AC) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-fcan-signal-fehler"></a>
### STATUS_FCAN_SIGNAL_FEHLER

diverse vom AFS eingelesene FCAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $1C InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CLU1_CAN_FEHLER_WERT | int | FCAN Signalfehler CAN-ID: (216 / 0x0D8) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_CLU1_CAN_FEHLER_BIT0_TEXT | string | FCAN Signalfehler CAN-ID: (216 / 0x0D8) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 0 i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU1_CAN_FEHLER_BIT1_TEXT | string | FCAN Signalfehler CAN-ID: (216 / 0x0D8) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU1_CAN_FEHLER_BIT2_TEXT | string | FCAN Signalfehler CAN-ID: (216 / 0x0D8) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU1_CAN_FEHLER_BIT3_TEXT | string | FCAN Signalfehler CAN-ID: (216 / 0x0D8) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU1_CAN_FEHLER_BIT4_TEXT | string | FCAN Signalfehler CAN-ID: (216 / 0x0D8) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU1_CAN_FEHLER_BIT5_TEXT | string | FCAN Signalfehler CAN-ID: (216 / 0x0D8) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU1_CAN_FEHLER_BIT6_TEXT | string | FCAN Signalfehler CAN-ID: (216 / 0x0D8) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU1_CAN_FEHLER_BIT7_TEXT | string | FCAN Signalfehler CAN-ID: (216 / 0x0D8) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU2_CAN_FEHLER_WERT | int | FCAN Signalfehler CAN-ID: (227 / 0x0E3) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_CLU2_CAN_FEHLER_BIT0_TEXT | string | FCAN Signalfehler CAN-ID: (227 / 0x0E3) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU2_CAN_FEHLER_BIT1_TEXT | string | FCAN Signalfehler CAN-ID: (227 / 0x0E3) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU2_CAN_FEHLER_BIT2_TEXT | string | FCAN Signalfehler CAN-ID: (227 / 0x0E3) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU2_CAN_FEHLER_BIT3_TEXT | string | FCAN Signalfehler CAN-ID: (227 / 0x0E3) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU2_CAN_FEHLER_BIT4_TEXT | string | FCAN Signalfehler CAN-ID: (227 / 0x0E3) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU2_CAN_FEHLER_BIT5_TEXT | string | FCAN Signalfehler CAN-ID: (227 / 0x0E3) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU2_CAN_FEHLER_BIT6_TEXT | string | FCAN Signalfehler CAN-ID: (227 / 0x0E3) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU2_CAN_FEHLER_BIT7_TEXT | string | FCAN Signalfehler CAN-ID: (227 / 0x0E3) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU3_CAN_FEHLER_WERT | int | FCAN Signalfehler CAN-ID: (244 / 0x0F4) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_CLU3_CAN_FEHLER_BIT0_TEXT | string | FCAN Signalfehler CAN-ID: (244 / 0x0F4) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU3_CAN_FEHLER_BIT1_TEXT | string | FCAN Signalfehler CAN-ID: (244 / 0x0F4) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU3_CAN_FEHLER_BIT2_TEXT | string | FCAN Signalfehler CAN-ID: (244 / 0x0F4) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU3_CAN_FEHLER_BIT3_TEXT | string | FCAN Signalfehler CAN-ID: (244 / 0x0F4) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU3_CAN_FEHLER_BIT4_TEXT | string | FCAN Signalfehler CAN-ID: (244 / 0x0F4) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU3_CAN_FEHLER_BIT5_TEXT | string | FCAN Signalfehler CAN-ID: (244 / 0x0F4) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU3_CAN_FEHLER_BIT6_TEXT | string | FCAN Signalfehler CAN-ID: (244 / 0x0F4) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU3_CAN_FEHLER_BIT7_TEXT | string | FCAN Signalfehler CAN-ID: (244 / 0x0F4) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU_STATUS_CAN_FEHLER_WERT | int | FCAN Signalfehler CAN-ID: (357 / 0x165) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_CLU_STATUS_CAN_FEHLER_BIT0_TEXT | string | FCAN Signalfehler CAN-ID: (357 / 0x165) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU_STATUS_CAN_FEHLER_BIT1_TEXT | string | FCAN Signalfehler CAN-ID: (357 / 0x165) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU_STATUS_CAN_FEHLER_BIT2_TEXT | string | FCAN Signalfehler CAN-ID: (357 / 0x165) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU_STATUS_CAN_FEHLER_BIT3_TEXT | string | FCAN Signalfehler CAN-ID: (357 / 0x165) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU_STATUS_CAN_FEHLER_BIT4_TEXT | string | FCAN Signalfehler CAN-ID: (357 / 0x165) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU_STATUS_CAN_FEHLER_BIT5_TEXT | string | FCAN Signalfehler CAN-ID: (357 / 0x165) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU_STATUS_CAN_FEHLER_BIT6_TEXT | string | FCAN Signalfehler CAN-ID: (357 / 0x165) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_CLU_STATUS_CAN_FEHLER_BIT7_TEXT | string | FCAN Signalfehler CAN-ID: (357 / 0x165) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_RAD_GESCHW_CAN_FEHLER_WERT | int | FCAN Signalfehler CAN-ID: (206 / 0x0CE) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_RAD_GESCHW_CAN_FEHLER_BIT0_TEXT | string | FCAN Signalfehler CAN-ID: (206 / 0x0CE) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_RAD_GESCHW_CAN_FEHLER_BIT1_TEXT | string | FCAN Signalfehler CAN-ID: (206 / 0x0CE) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_RAD_GESCHW_CAN_FEHLER_BIT2_TEXT | string | FCAN Signalfehler CAN-ID: (206 / 0x0CE) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_RAD_GESCHW_CAN_FEHLER_BIT3_TEXT | string | FCAN Signalfehler CAN-ID: (206 / 0x0CE) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_RAD_GESCHW_CAN_FEHLER_BIT4_TEXT | string | FCAN Signalfehler CAN-ID: (206 / 0x0CE) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_RAD_GESCHW_CAN_FEHLER_BIT5_TEXT | string | FCAN Signalfehler CAN-ID: (206 / 0x0CE) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_RAD_GESCHW_CAN_FEHLER_BIT6_TEXT | string | FCAN Signalfehler CAN-ID: (206 / 0x0CE) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_RAD_GESCHW_CAN_FEHLER_BIT7_TEXT | string | FCAN Signalfehler CAN-ID: (206 / 0x0CE) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_REGELEINGRIFFE_DSC_AFS_CAN_FEHLER_WERT | int | FCAN Signalfehler CAN-ID: (286 / 0x11E) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_REGELEINGRIFFE_DSC_AFS_CAN_FEHLER_BIT0_TEXT | string | FCAN Signalfehler CAN-ID: (286 / 0x11E) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_REGELEINGRIFFE_DSC_AFS_CAN_FEHLER_BIT1_TEXT | string | FCAN Signalfehler CAN-ID: (286 / 0x11E) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_REGELEINGRIFFE_DSC_AFS_CAN_FEHLER_BIT2_TEXT | string | FCAN Signalfehler CAN-ID: (286 / 0x11E) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_REGELEINGRIFFE_DSC_AFS_CAN_FEHLER_BIT3_TEXT | string | FCAN Signalfehler CAN-ID: (286 / 0x11E) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_REGELEINGRIFFE_DSC_AFS_CAN_FEHLER_BIT4_TEXT | string | FCAN Signalfehler CAN-ID: (286 / 0x11E) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_REGELEINGRIFFE_DSC_AFS_CAN_FEHLER_BIT5_TEXT | string | FCAN Signalfehler CAN-ID: (286 / 0x11E) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_REGELEINGRIFFE_DSC_AFS_CAN_FEHLER_BIT6_TEXT | string | FCAN Signalfehler CAN-ID: (286 / 0x11E) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_REGELEINGRIFFE_DSC_AFS_CAN_FEHLER_BIT7_TEXT | string | FCAN Signalfehler CAN-ID: (286 / 0x11E) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_LENKRADWINKEL_OBEN_CAN_FEHLER_WERT | int | FCAN Signalfehler CAN-ID: (201 / 0x0C9) Wertebereich: ( 0,1,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_LENKRADWINKEL_OBEN_CAN_FEHLER_BIT0_TEXT | string | FCAN Signalfehler CAN-ID: (201 / 0x0C9) Wertebereich: ( 0, 1 ) moegliche Zustaende: ( 0x00 -- &gt; i.O. ) moegliche Zustaende: ( 0x01 -- &gt; Checksumme Falsch ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_LENKRADWINKEL_OBEN_CAN_FEHLER_BIT1_TEXT | string | FCAN Signalfehler CAN-ID: (201 / 0x0C9) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Alive-Zähler der Nachricht wurde mehr als um 1 erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_LENKRADWINKEL_OBEN_CAN_FEHLER_BIT2_TEXT | string | FCAN Signalfehler CAN-ID: (201 / 0x0C9) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Alive-Zähler der Nachricht wurde nicht erhöht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_LENKRADWINKEL_OBEN_CAN_FEHLER_BIT3_TEXT | string | FCAN Signalfehler CAN-ID: (201 / 0x0C9) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Alive-Zähler der Nachricht stimmt nicht ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_LENKRADWINKEL_OBEN_CAN_FEHLER_BIT4_TEXT | string | FCAN Signalfehler CAN-ID: (201 / 0x0C9) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Die Nachricht selbst ist nicht korrekt ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_LENKRADWINKEL_OBEN_CAN_FEHLER_BIT5_TEXT | string | FCAN Signalfehler CAN-ID: (201 / 0x0C9) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_LENKRADWINKEL_OBEN_CAN_FEHLER_BIT6_TEXT | string | FCAN Signalfehler CAN-ID: (201 / 0x0C9) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Dieseist aber nicht empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| STAT_LENKRADWINKEL_OBEN_CAN_FEHLER_BIT7_TEXT | string | FCAN Signalfehler CAN-ID: (201 / 0x0C9) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; Eine Nachricht ist mehr als einmal vom System empfangen worden ) Textausgabe ueber Tabelle: ( CANSignalFehler ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-start-lwm-ruecksetzen"></a>
### START_LWM_RUECKSETZEN

Motorlagewinkel wird ungueltig gesetzt KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $21 Motorlagewinkel ungueltig setzen,ueber ZFLS Fkt mit anschl. SG-RESET Modus  : Default KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $50 Gueltigkeit Motorlagewinkel abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GUELTIGKEIT_LWM_WERT | int | Wertebereich: ( 0,1,2 ) moegliche Zustaende: ( 0 -- &gt; NICHT gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; nicht definiert ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_LWM_TEXT | string | moegliche Zustaende: ( 0 -- &gt; NICHT gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; nicht definiert ) Textausgabe ueber Tabelle: ( GueRotor ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG_1 | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT_1 | binary | Hex - Antwort von SG |
| _TEL_DATEN_1 | binary | Hex - Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex - Antwort von SG |
| _TEL_DATEN_2 | binary | Hex - Antwort von SG |

<a id="job-start-lwm-init"></a>
### START_LWM_INIT

KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $22 Inbetriebnahme Resultat abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-start-adaptivdaten-abgleich"></a>
### START_ADAPTIVDATEN_ABGLEICH

KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $51 Abgleich der Adaptivdaten wird gestartet Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-start-adaptivdaten-ruecksetzen"></a>
### START_ADAPTIVDATEN_RUECKSETZEN

KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $53 Adaptivdaten im EEPROM werden DEFAULT werten beschrieben Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-lwm-init"></a>
### STATUS_LWM_INIT

Gueltigkeit des Motorlagewinkels auslesen KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $50 Inbetriebnahme Resultat abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GUELTIGKEIT_LWM_WERT | int | aktueller Zustand des Motorlagewinkels Wertebereich: ( 0,1,2 ) moegliche Zustaende: ( 0 -- &gt; NICHT gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; nicht definiert ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_LWM_TEXT | string | aktueller Zustand des Motorlagewinkels moegliche Zustaende: ( 0 -- &gt; NICHT gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; nicht definiert ) Textausgabe ueber Tabelle: ( GueRotor ) |
| STAT_INBETRIEBNAHME_LWG_FERTIG | int | aktueller Status der Inbetriebnahme moegliche Zustaende: ( 0 -- &gt; NICHT gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; nicht definiert ) Textausgabe ueber Tabelle: ( GueRotor ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-adaptivdaten-abgleich"></a>
### STATUS_ADAPTIVDATEN_ABGLEICH

aktueller Zustand des Adaptivdatenabgleichs KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $51 alle aktuelle Abgleichstati abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADAPTIVDATEN_ABGLEICH_WERT | int | aktueller Status des Adaptivdatenabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Abgleich aktiv ) moegliche Zustaende: ( 1 -- &gt; Abgleich NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ADAPTIVDATEN_ABGLEICH_TEXT | string | aktueller Status des Adaptivdatenabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Abgleich aktiv ) moegliche Zustaende: ( 1 -- &gt; Abgleich NICHT aktiv ) Textausgabe ueber Tabelle: ( AbgleichAktiv ) |
| STAT_LANGZEITABGLEICH_WERT | int | aktueller Status des Adaptivdatenabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; LangzeitAbgleich NICHT aktiv ) moegliche Zustaende: ( 1 -- &gt; LangzeitAbgleich aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_LANGZEITABGLEICH_TEXT | string | aktueller Status des Adaptivdatenabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; LangzeitAbgleich NICHT aktiv ) moegliche Zustaende: ( 1 -- &gt; LangzeitAbgleich aktiv ) Textausgabe ueber Tabelle: ( LangzeitAbgleich ) |
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
| STAT_RTA_ABGLEICH_TEXT | string | aktueller Status des Reifentoleranzabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Textausgabe ueber Tabelle: ( BasisAktiv ) |
| STAT_YR_ABGLEICH_WERT | int | aktueller Status des Gierratenabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_YR_ABGLEICH_TEXT | string | aktueller Status des Gierratenabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Textausgabe ueber Tabelle: ( BasisAktiv ) |
| STAT_AY_ABGLEICH_WERT | int | aktueller Status des Querbeschleunigungsabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AY_ABGLEICH_TEXT | string | aktueller Status des Querbeschleunigungsabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Textausgabe ueber Tabelle: ( BasisAktiv ) |
| STAT_SLW_ABGLEICH_WERT | int | aktueller Status des Summenlenkwinkelabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SLW_ABGLEICH_TEXT | string | aktueller Status des Summenlenkwinkelabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Textausgabe ueber Tabelle: ( BasisAktiv ) |
| STAT_AX_ABGLEICH_WERT | int | aktueller Status des Laengsbeschleunigungsabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_AX_ABGLEICH_TEXT | string | aktueller Status des Laengsbeschleunigungsabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Textausgabe ueber Tabelle: ( BasisAktiv ) |
| STAT_VCH_ABGLEICH_WERT | int | aktueller Status der charakter. Geschwindigkeitsabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_VCH_ABGLEICH_TEXT | string | aktueller Status der charakter. Geschwindigkeitsabgleichs Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; Basiswerte aktiv ) moegliche Zustaende: ( 1 -- &gt; Basiswerte NICHT aktiv ) Textausgabe ueber Tabelle: ( BasisAktiv ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-steuern-motorlagewinkel-offset"></a>
### STEUERN_MOTORLAGEWINKEL_OFFSET

Schreiben des Motorlagewinkeloffsets ins EEPROM KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $22 InputOutputLocalIdentifier(IOLI) SubID  : $07 InputOutputControlParameter(IOCP) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTORLAGEWINKEL_OFFSET_SOLL_WERT | real | Motorlagewinkeloffset ins EEPROM für Lenkradkorrektur, erlaubt im PREDRIVE/DRIVE Skalierungsfaktor: ( 100 ) Wertebereich: ( -10..+10 ) Einheit: ( Grad Fahrerlenkwinkel ) Telegrammlaenge KWP: ( 2 Byte ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORLAGEWINKEL_OFFSET_EINH | string | Einheit des Motorlagewinkeloffsets Einheit: ( Grad Fahrerlenkwinkel ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-eeprom-seriennummer-szl"></a>
### STATUS_EEPROM_SERIENNUMMER_SZL

Auslesen der im AFS EEPROM abgelegten Seriennummer des SZL AFS wird / bleibt inaktiv falls SZL getauscht wird KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $01 InputOutputLocalIdentifier(IOLI) SubID  : $08 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EEPROM_SERIENNUMMER_SZL_WERT | string | 8 stellige SZL Seriennummer beim AFS im EEPROM abgelegt Wertebereich: ( 0...99999999 ) Telegrammlaenge KWP: ( 4 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-eeprom-offset-szl"></a>
### STATUS_EEPROM_OFFSET_SZL

Auslesen des im AFS EEPROM abgelegten Fahrerlenkwinkeloffsets vom SZL KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $02 InputOutputLocalIdentifier(IOLI) SubID  : $08 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EEPROM_FAHRER_LENKWINKEL_OFFSET_SZL_WERT | real | FLWOffset vom SZL beim AFS im EEPROM abgelegt Quantisierung: ( (PH) = 0,04395 * (HEX) [grad] ) Skalierungsfaktor: ( 1000 ) Wertebereich: ( -1439.95Grad...1439.95Grad ) Einheit: ( Grad Fahrerlenkwinkel ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_FAHRER_LENKWINKEL_EINH | string | Einheit des Fahrerlenkwinkels Einheit: ( Grad Fahrerlenkwinkel ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-motorlagewinkel-offset"></a>
### STATUS_MOTORLAGEWINKEL_OFFSET

Auslesen des Motorlagewinkeloffsets aus dem EEPROM und des Maximalwerts KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $03 InputOutputLocalIdentifier(IOLI) SubID  : $08 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORLAGEWINKEL_OFFSET_WERT | real | Motorlagewinkel-Offset aus EEPROM für Lenkradkorrektur Skalierungsfaktor: ( 100 ) Wertebereich: ( -10..+10 ) Einheit: ( Grad Fahrerlenkwinkel ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_MOTORLAGEWINKEL_OFFSET_MAX_WERT | real | Motorlagewinkel Offset Maximalwert für Lenkradkorrektur Skalierungsfaktor: ( 1 ) Wertebereich: ( -10, +10 ) Einheit: ( Grad Fahrerlenkwinkel ) |
| STAT_MOTORLAGEWINKEL_OFFSET_EINH | string | Einheit des Motorlagewinkeloffsets Einheit: ( Grad Fahrerlenkwinkel ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-zf-factory-daten-lesen"></a>
### ZF_FACTORY_DATEN_LESEN

hier werden 12 Byte aus dem EEPROM Werksdatenbereich ausgelesen, ab Adresse 0x0FCA KWP2000: $23 readMemoryByAddress SubID  : $02 MemoryTypeIdentifier (ROMX), MT = 2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ZF_FACTORY_MPC_EEPROM_DATEN | binary | Daten die aus dem EEPROM gelesen werden, ohne 3 Byte Adress Adresseinfo Telegrammlaenge KWP: ( 12 Byte ) |
| ZF_FACTORY_WERK | string | Bosch / ZF Werkskennzahl, z.B. auf SG Label( 0078 ) Telegrammlaenge KWP: ( 2 Byte ) |
| ZF_FACTORY_PAM | string | Bosch / ZF Knotenkennzahl, z.B. auf SG Label( 7441 ) Telegrammlaenge KWP: ( 2 Byte ) |
| ZF_FACTORY_SERIENNUMMER | string | Bosch / ZF Seriennummer, z.B. auf SG Label( 0248 ) Telegrammlaenge KWP: ( 2 Byte ) |
| ZF_FACTORY_DATUM | string | Bosch / ZF SG Herstelldatum, z.B. auf SG Label( 240703 ) Telegrammlaenge KWP: ( 3 Byte ) |
| ZF_FACTORY_UHRZEIT | string | Bosch / ZF Uhrzeit, ( 17: 08: 03 ) Telegrammlaenge KWP: ( 3 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-ident-aif-lesen"></a>
### IDENT_AIF_LESEN

aktuelles AIF Feld auslesen KWP2000: $1A ReadECUIdentification SubID  : $86 CurrentUIFDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BELEGT | int | wurde AIF schon beschrieben Wertebereich: ( 0,1 ) moegliche Zustaende: ( 0 -- &gt; gesammtes AIF Feld ist nicht frei ) moegliche Zustaende: ( 1 -- &gt; mindestens ein Byte enthaelt einen Wert ungleich 0xFF ) |
| AIF_ANZ_DATEN_HEX | string | Verweis auf naechstes AIF Feld Telegrammwert in HEX |
| AIF_ANZ_DATEN | int | AIF Feld Typ Groesse des jeweiligen Eintrages ist aus dem Adressofset ersichtlich 0x40_hex ( 64_dez ) Power PC 0x33_hex ( 51_dez ) fuer alle anderen Anwender des grossen AIF Feldes 0x12_hex ( 18_dez ) letztmoeglicher Blockeintrag 0xFE_hex ( 254_dez ) letztmöglicher Eintrag 0x01_hex ( 64_dez ) nur ein Eintrag der aber ueberschreibbar ist 0xFF_hex ( 255_dez ) freier Speicherplatz 0x00_hex ( 00_dez ) freier Speicherplatz |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7 - stellig Wertebereich: ( ASCII Zeichen ) Telegrammlaenge KWP: ( 7 Byte ) |
| AIF_FAHRGESTELL_NR_HEX | string | Telegrammdarstellung im KWP |
| AIF_PROGRAMMIER_DATUM | string | Programmierdatum in yyyy.mm.tt Wertebereich: ( Zahlen 0..9 ) Telegrammlaenge KWP: ( 4 Byte ) |
| AIF_PROGRAMMIER_DATUM_HEX | string | Telegrammdarstellung im KWP |
| AIF_ZUSAMMENBAU_NR | string | Zusammenbaunummer die beim Flashen ueber Winkfp eingetragen wird Wertebereich: ( Zahlen 0..9 ) Telegrammlaenge KWP: ( 6 Byte ) |
| AIF_ZUSAMMENBAU_NR_HEX | string | Telegrammdarstellung im KWP |
| AIF_SOFTWARENUMMER_NR | string | Datensatznummer, eigene Teilenummer fuer gesonderten DAF Stand Wertebereich: ( ASCII Zeichen ) Telegrammlaenge KWP: ( 6 Byte ) |
| AIF_SOFTWARENUMMER_NR_HEX | string | Telegrammdarstellung im KWP |
| AIF_BEHOERDEN_NR | string | Behoerdennummer Telegrammlaenge KWP: ( 6 Byte ) |
| AIF_BEHOERDEN_NR_HEX | string | Telegrammdarstellung im KWP |
| AIF_HAENDLER_NR | string | Haendlernummer Telegrammlaenge KWP: ( 3 Byte ) |
| AIF_HAENDLER_NR_HEX | string | Telegrammdarstellung im KWP |
| AIF_TESTER_NR | string | Haendlernummer Telegrammlaenge KWP: ( 5 Byte ) |
| AIF_TESTER_NR_HEX | string | Telegrammdarstellung im KWP |
| AIF_KM_STAND | string | Kilometerstand bei der Programmierung Telegrammlaenge KWP: ( 1 Byte ) |
| AIF_KM_STAND_HEX | string | Telegrammdarstellung im KWP |
| AIF_PROGRAMM_STAND | string | Programmstand als Programmreferenz Telegrammlaenge KWP: ( 12 Byte ) |
| AIF_PROGRAMM_STAND_HEX | string | Telegrammdarstellung im KWP |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 10 - stellig falls vorhanden, sonst 7 - stellig zusammen mit Fahrgestellnummer kurz ('AIF_FAHRGESTELL_NR') 10 + 7 Byte 17 - stellig Telegrammlaenge KWP: ( 17 Byte ) |
| AIF_FG_NR_LANG_HEX | string | Fahrgestellnummer 17 - stellig falls vorhanden, sonst 7 - stellig Telegrammdarstellung im KWP |
| AIF_RESERVE | string | Reserve fuer SG spez. Eintraege Telegrammlaenge KWP: ( 3 Byte ) |
| AIF_RESERVE_HEX | string | Telegrammdarstellung im KWP |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-ident-istufe-lesen"></a>
### IDENT_ISTUFE_LESEN

Auslesen der aktuellen Integrationsstufe KWP2000: $1A ReadECUIdentification SubID  : $82 reserved by Document Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_INTEGRATIONS_STUFE_TEXT | string | aktuelle Interationssufe z.B. 'E070-06-10-310' Telegrammlaenge KWP: ( 14 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-ident-divcalc-lesen"></a>
### IDENT_DIVCALC_LESEN

Auslesen der aktuellen Kennung des diversitaeren Rechnens auf dem NEC, SG darf NICHT im DRIVE Modus sein KWP2000: $1A ReadECUIdentification SubID  : $83 reserved by Document Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_NEC_DIVCALC_TEXT | string | aktuelles Label vom diversitaeren Rechnen Telegrammlaenge KWP: ( 20 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-ident-dcm-lesen"></a>
### IDENT_DCM_LESEN

Auslesen der aktuellen Kennung des DCM Datenstandes KWP2000: $1A ReadECUIdentification SubID  : $84 reserved by Document Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_DCM_MPCDAF_TEXT | string | DCM Dateiname vom MPC DAF Bereich Telegrammlaenge KWP: ( 64 Byte ) |
| ID_DCM_NECDAF_TEXT | string | DCM Dateiname vom NEC DAF Bereich Telegrammlaenge KWP: ( 64 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-ident-ssecuson-lesen"></a>
### IDENT_SSECUSON_LESEN

ZFLD Softwarenummern auf MPC Seite KWP2000: $1A ReadECUIdentification SubID  : $94 systemSupplierECUSoftwareNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_ZFLSLIB_MPC_DRIVE_TEXT | string | aktuelle ZFLS Lib Fahrprogrammversion auf MPC Seite Telegrammlaenge KWP: ( 20 Byte ) |
| ID_ZFLSLIB_MPC_BOOT_TEXT | string | aktuelle ZFLS Lib Bootversion auf MPC Seite Telegrammlaenge KWP: ( 20 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-ident-ssecusvn-lesen"></a>
### IDENT_SSECUSVN_LESEN

Auslesen der NEC Logistik, PAF-DAF und Bootblockkennung, SG darf NICHT im DRIVE Modus sein KWP2000: $1A ReadECUIdentification SubID  : $95 SystemSupplierECUSoftwareVersionNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_NEC_BOOT_TEXT | string | aktuelles NEC Label der Bootversion Telegrammlaenge KWP: ( 20 Byte ) |
| ID_NEC_BOOT_TIMELABEL_TEXT | string | aktuelles NEC Zeitlabel der Bootversion Telegrammlaenge KWP: ( 40 Byte ) |
| ID_NEC_PAF_TEXT | string | aktuelles NEC PAF Label Telegrammlaenge KWP: ( 20 Byte ) |
| ID_NEC_PAF_TIMELABEL_TEXT | string | aktuelles NEC PAF Zeitlabel Telegrammlaenge KWP: ( 40 Byte ) |
| ID_NEC_DAF_TEXT | string | aktuelles NEC DAF Label Telegrammlaenge KWP: ( 20 Byte ) |
| ID_NEC_DAF_TIMELABEL_TEXT | string | aktuelles NEC DAF Zeitlabel Telegrammlaenge KWP: ( 40 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

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
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (11 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (58 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (10 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (151 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (23 × 9)
- [IARTTEXTEERWEITERT](#table-iarttexteerweitert) (4 × 3)
- [ZFFEHLERCODEUNDART](#table-zffehlercodeundart) (1 × 7)
- [ERCOSEKMODI](#table-ercosekmodi) (7 × 2)
- [GUEROTOR](#table-guerotor) (4 × 2)
- [STATUSCANFEHLER](#table-statuscanfehler) (9 × 2)
- [GUELWD](#table-guelwd) (4 × 2)
- [GUEDSC](#table-guedsc) (8 × 2)
- [REGELDSC](#table-regeldsc) (9 × 2)
- [SZLPROZINFO](#table-szlprozinfo) (3 × 2)
- [STATUSMASCHINEEINGAENGE](#table-statusmaschineeingaenge) (9 × 2)
- [STATUSMASCHINEZUSTAENDE](#table-statusmaschinezustaende) (33 × 2)
- [INFOUMWELTZF](#table-infoumweltzf) (1 × 9)
- [INFOUMWELTBMW](#table-infoumweltbmw) (1 × 4)
- [INFOFAHRZEUGSTATI](#table-infofahrzeugstati) (1 × 7)
- [INFOALLGEMEIN](#table-infoallgemein) (1 × 5)
- [ECOSERVO](#table-ecoservo) (9 × 2)
- [SENSORCLUSTERTYP](#table-sensorclustertyp) (13 × 2)
- [SENSORCLUSTERSTATUS1](#table-sensorclusterstatus1) (10 × 2)
- [CANSIGNALFEHLER](#table-cansignalfehler) (10 × 2)
- [SENSORCLUSTERSTATUS2](#table-sensorclusterstatus2) (10 × 2)
- [SENSCLUSTERSIGNALSTATUS](#table-sensclustersignalstatus) (6 × 2)
- [ABGLEICHAKTIV](#table-abgleichaktiv) (3 × 2)
- [BASISAKTIV](#table-basisaktiv) (3 × 2)
- [LANGZEITABGLEICH](#table-langzeitabgleich) (3 × 2)

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

Dimensions: 11 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED__INVALID_FORMAT |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0x23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x35 | ERROR_ECU_INVALID_KEY |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x80 | ERROR_FAILED_DELETE_MPC |
| 0x81 | ERROR_FAILED_DELETE_NEC |
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

Dimensions: 58 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x612C | Hardwarefehler Steuergerät |
| 0x612D | Gierratenregelung Plus |
| 0x612E | Fahrgestellnummernvergleich |
| 0x612F | Codierdatenfehler |
| 0x6130 | Boot- oder Flashfehler MPC |
| 0x6131 | Flashvorgang oder fehler NEC |
| 0x6133 | Motorspannung |
| 0x6134 | Motorstrom |
| 0x6135 | SZL neu verbaut oder AFS neu abgleichen |
| 0x6137 | Motorlagesensorversorgung,-position,-kommunikation |
| 0x6139 | Fzg Ref. Geschw. oder Fahrtrichtung unsicher oder nicht verfuegbar |
| 0x613A | Unterspannung Klemme. 30 (&lt; 9 Volt) |
| 0x613D | elektrischer Sperrenfehler |
| 0x613E | mechanischer Sperrenfehler |
| 0x6140 | Fahrerlenkwinkelplausibilitaet |
| 0x6142 | ECO-Ventil |
| 0x6143 | SERVO-Ventil |
| 0x6144 | Selbsthemmungsueberwachung |
| 0x6145 | diversitaeres Rechnen |
| 0x6146 | Steuergeraet kann nicht in den aktiven Modus wechseln |
| 0x6147 | Motorblockade |
| 0x6148 | Ueberspannung Klemme 30 (&gt; 17 Volt) |
| 0x6149 | kombinierte Lage- Drehzahlueberwachung |
| 0x614A | Motorlagewinkel nicht initialisiert |
| 0x614B | Betriebssystem |
| 0xCE84 | nicht benutzt |
| 0xCE85 | nicht benutzt |
| 0xCE86 | nicht benutzt |
| 0xCE87 | F-CAN Kommunikationsfehler |
| 0xCE88 | nicht benutzt |
| 0xCE89 | nicht benutzt |
| 0xCE8A | nicht benutzt |
| 0xCE8B | PT-CAN Kommunikationsfehler |
| 0xCE8C | nicht benutzt |
| 0xCE8D | nicht benutzt |
| 0xCE8E | nicht benutzt |
| 0xCE8F | nicht benutzt |
| 0xCE90 | nicht benutzt |
| 0xCE91 | nicht benutzt |
| 0xCE92 | Botschaft (Sensorcluster 3, ID=0F4) von F-CAN |
| 0xCE93 | Botschaft (Lenkradwinkel oben, ID=0C9) Initialisierungsphase |
| 0xCE94 | Botschaft (Sensorcluster 1, ID=0D8) von F-CAN |
| 0xCE95 | Botschaft (Sensorcluster 2, ID=0E3) von F-CAN |
| 0xCE96 | Botschaft (Radgeschwindigkeiten, ID=0CE) von DSC F-CAN |
| 0xCE97 | Botschaft (Sensorcluster Status, ID=165) von F-CAN |
| 0xCE98 | Botschaft (Regeleingriffe DSC, ID=11E) von DSC F-CAN |
| 0xCE99 | Botschaft (Lenkradwinkel oben, ID=0C9) von SZL F-CAN |
| 0xCE9A | Botschaft (Anhaengerdaten, ID=2E4) von PT-CAN |
| 0xCE9B | Botschaft (Status DXC Kupplung, ID=BC) von PT-CAN |
| 0xCE9C | Botschaft (Status DSC, ID=19E) von DSC PT-CAN |
| 0xCE9D | Botschaft (Motormoment 1, ID=0A8) von DME PT-CAN |
| 0xCE9E | Botschaft (Motormoment 3, ID=0AA) von DME PT-CAN |
| 0xCE9F | Botschaft (Motordaten, ID=1D0) von DME PT-CAN |
| 0xCEA0 | Botschaft (Getriebedaten 1, ID=BA) von EGS PT-CAN |
| 0xCEA1 | Botschaft (Klemmenstatus, ID=130) von CAS PT-CAN |
| 0xCEA2 | Botschaft (Status ARS, ID=1AC) von ARS PT-CAN |
| 0xCEA3 | Botschaft (Kilometerstand, ID=330) von KI PT-CAN |
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

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | ZfFehlerCodeUndArt | 0x08 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 10 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Anzahl der zu diesem Fehler gefundenen KFCs | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x02 | ZFLS Fehlercode | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x03 | ZFLS Fehlerart | -- | high | unsigned int | -- | 1 | 1 | 0 |
| 0x04 | ZFLS Fehlercode 1 | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x05 | ZFLS Fehlerart 1 | -- | high | unsigned int | -- | 1 | 1 | 0 |
| 0x06 | ZFLS Fehlercode 2 | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x07 | ZFLS Fehlerart 2 | -- | high | unsigned int | -- | 1 | 1 | 0 |
| 0x08 | FSV Nummer | -- | - | signed long | -- | 1 | 1 | 0 |
| 0xFF | ohne Bedeutung | 1 | -- | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

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

Dimensions: 151 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x7001 | KFC_NEC_ERR_1 |
| 0x7002 | KFC_NEC_ERR_2 |
| 0x7003 | KFC_NEC_ERR_3 |
| 0x7004 | KFC_NEC_ERR_4 |
| 0x7005 | KFC_NEC_ERR_5 |
| 0x7006 | KFC_NEC_ERR_6 |
| 0x7007 | KFC_NEC_ERR_7 |
| 0x7008 | KFC_NEC_ERR_8 |
| 0x7009 | KFC_PROG |
| 0x700A | KFC_COMM |
| 0x700B | KFC_EEPROMNR |
| 0x700C | KFC_EEPROMHR |
| 0x700D | KFC_KLD |
| 0x700E | KFC_ROM |
| 0x700F | KFC_RAM |
| 0x7010 | KFC_CORE |
| 0x7011 | KFC_RESERVED17 |
| 0x7012 | KFC_OS |
| 0x7013 | KFC_MLW_INVALID |
| 0x7014 | KFC_VX_REF |
| 0x7015 | KFC_DPSI1 |
| 0x7016 | KFC_RESERVED22 |
| 0x7017 | KFC_DPSI2 |
| 0x7018 | KFC_RESERVED24 |
| 0x7019 | KFC_AY1 |
| 0x701A | KFC_RESERVED26 |
| 0x701B | KFC_AY2 |
| 0x701C | KFC_RESERVED28 |
| 0x701D | KFC_DEH |
| 0x701E | KFC_RESERVED30 |
| 0x701F | KFC_RESERVED31 |
| 0x7020 | KFC_LWS |
| 0x7021 | KFC_MPC_POSCTRL_ERR |
| 0x7022 | KFC_VINCOMP |
| 0x7023 | KFC_CONFIG |
| 0x7024 | KFC_MPC_BOOT_FLASH |
| 0x7025 | KFC_NEC_UPDATE |
| 0x7026 | KFC_RESERVED38 |
| 0x7027 | KFC_INV_SER_SLZ |
| 0x7028 | KFC_GEST_REDUNDANT |
| 0x7029 | KFC_RESERVED41 |
| 0x702A | KFC_RESERVED42 |
| 0x702B | KFC_LOW_VOLTAGE |
| 0x702C | KFC_RESERVED44 |
| 0x702D | KFC_RESERVED45 |
| 0x702E | KFC_SENSOR_DRIVE |
| 0x702F | KFC_CANA |
| 0x7030 | KFC_CANB |
| 0x7031 | KFC_CANA_Y1 |
| 0x7032 | KFC_CANA_Y2 |
| 0x7033 | KFC_CANA_DSC_VWHL |
| 0x7034 | KFC_RESERVED52 |
| 0x7035 | KFC_CANA_DSC_REGULATION |
| 0x7036 | KFC_CANA_SZL_LWDS |
| 0x7037 | KFC_RESERVED55 |
| 0x7038 | KFC_RESERVED56 |
| 0x7039 | KFC_CANB_DSC_STAT |
| 0x703A | KFC_CANB_DME_TORQ1 |
| 0x703B | KFC_CANB_DME_TORQ3 |
| 0x703C | KFC_CANB_DME_MOTORDAT |
| 0x703D | KFC_GMK |
| 0x703E | KFC_CANB_CAS_KLEMMEN |
| 0x703F | KFC_RESERVED63 |
| 0x7040 | KFC_CANB_KI_KM |
| 0x7041 | KFC_RESERVED65 |
| 0x7042 | KFC_CANA_SZL_LWDS_INIT |
| 0x7043 | KFC_RSCAN |
| 0x7044 | KFC_RESERVED68 |
| 0x7045 | KFC_RESERVED69 |
| 0x7046 | KFC_DIV_CALC_MPC |
| 0x7047 | KFC_SPI |
| 0x7048 | KFC_CANA_AX |
| 0x7049 | KFC_CANB_EGS_GETRIEBEDATEN_1 |
| 0x704A | KFC_TBD74 |
| 0x704B | KFC_SMCOM |
| 0x704C | KFC_US |
| 0x704D | KFC_HIGH_VOLTAGE |
| 0x704E | KFC_GESTOERT_LWSYNC |
| 0x704F | KFC_GESTOERT_ABWUERG |
| 0x7050 | KFC_GESTOERT_ROLLEN |
| 0x7051 | KFC_CANA_CLU_STATUS |
| 0x7052 | KFC_AX |
| 0x7053 | KFC_LWMOTOR_MAX |
| 0x7054 | KFC_CANB_DXC_KUPPLUNG |
| 0x7055 | KFC_CANB_ANHAENGER |
| 0x7056 | KFC_ALIVE_MONITOR |
| 0x7057 | KFC_MOTORBLOCKADE |
| 0x7058 | KFC_CANB_STAT_ARS |
| 0x7059 | KFC_NECQUAL |
| 0x705A | KFC_DRIVE_TRANSITION |
| 0x705B | KFC_TBD91 |
| 0x705C | KFC_TBD92 |
| 0x705D | KFC_TBD93 |
| 0x705E | KFC_TBD94 |
| 0x705F | KFC_TBD95 |
| 0x7060 | KFC_TBD96 |
| 0x7061 | KFC_TBD97 |
| 0x7062 | KFC_TBD98 |
| 0x7101 | NKFC_CAN |
| 0x7102 | NKFC_CCU |
| 0x7103 | NKFC_EEPROMNR |
| 0x7104 | NKFC_US |
| 0x7105 | NKFC_EPROM |
| 0x7106 | NKFC_IWD |
| 0x7107 | NKFC_COMP |
| 0x7108 | NKFC_RAM |
| 0x7109 | NKFC_RELAIS |
| 0x710A | NKFC_SMCURR |
| 0x710B | NKFC_SMPOS |
| 0x710C | NKFC_SMVOLT |
| 0x710D | NKFC_PROG |
| 0x710E | NKFC_EEPROMHR |
| 0x710F | NKFC_MOD_MC |
| 0x7110 | NKFC_BRAKE |
| 0x7111 | NKFC_COMM |
| 0x7113 | NKFC_LWSSUPP |
| 0x7114 | NKFC_DPOS |
| 0x7115 | NKFC_MPC |
| 0x7116 | NKFC_MPC_SUBS_1 |
| 0x7117 | NKFC_MPC_SUBS_2 |
| 0x7118 | NKFC_MPC_SUBS_3 |
| 0x7119 | NKFC_MPC_SUBS_4 |
| 0x711A | NKFC_MPC_SUBS_5 |
| 0x711B | NKFC_MPC_SUBS_6 |
| 0x711C | NKFC_MPC_SUBS_7 |
| 0x711D | NKFC_MPC_SUBS_8 |
| 0x711E | NKFC_MPC_SUBS_9 |
| 0x7120 | NKFC_EN_CHOKE |
| 0x7121 | NKFC_ST |
| 0x7122 | NKFC_ECO |
| 0x7123 | NKFC_COMP_CAN |
| 0x7124 | NKFC_RESERVED36 |
| 0x7125 | NKFC_RESERVED37 |
| 0x7126 | NKFC_CANA_WHEELSPEED |
| 0x7127 | NKFC_LOWVOLT |
| 0x7128 | NKFC_ADC |
| 0x7129 | NKFC_SMCOM |
| 0x712A | NKFC_SPI |
| 0x712B | NKFC_OS |
| 0x712C | NKFC_ALIVE_MONITOR |
| 0x712D | NKFC_SAS_TRIALS |
| 0x712E | NKFC_SAS_FAILS |
| 0x712F | NKFC_SELFLOCK |
| 0x7130 | NKFC_HIGHVOLT |
| 0x7131 | NKFC_TBD49 |
| 0x7132 | NKFC_TBD50 |
| 0x7133 | NKFC_TBD51 |
| 0x7134 | NKFC_TBD52 |
| 0x7135 | NKFC_TBD53 |
| 0x7136 | NKFC_TBD54 |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 00000011 |
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
| default | InfoAllgemein | InfoFahrzeugStati | InfoUmweltBMW | InfoUmweltZF |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 23 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | FSV Nummer | -- | - | signed long | -- | 1 | 1 | 0 |
| 0x02 | ZFLS Fehlercode | -- | high | unsigned int | -- | 1 | 1 | 0 |
| 0x03 | ZFLS Fehlerart | -- | high | unsigned int | -- | 1 | 1 | 0 |
| 0x04 | ZFLS Statuswort | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x10 | Fahrzeuggeschwindigkeit | km/h | -- | signed char | -- | 1.8 | 1 | 0 |
| 0x11 | Querbeschleunigung | m/(s*s) | -- | signed char | -- | 1 | 7 | 0 |
| 0x12 | Gierrate | rad/s | -- | signed char | -- | 1 | 70 | 0 |
| 0x13 | Summenlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x14 | Fahrerlenkwinkel | Grad | -- | signed char | -- | 12 | 1 | 0 |
| 0x15 | Versorgungsspannung | Volt | -- | unsigned char | -- | 1 | 12.75 | 0 |
| 0x20 | OS Status | -- | high | unsigned int | -- | 1 | 1 | 0 |
| 0x21 | Ersatzmassnahme | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x22 | Qualifier | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x30 | Gewichtung charakteristische Geschwindigkeit | -- | -- | unsigned char | -- | 1 | 64 | 0 |
| 0x31 | charakteristische Geschwindigkeit | m/s | high | unsigned int | -- | 20 | 1024 | 20 |
| 0x32 | Zeitstempel Zuendungszyklus Zaehler | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x33 | Zeitstempel des sychronen 10 ms Zaehler | -- | - | signed long | -- | 1 | 1 | 0 |
| 0x34 | SG Temperatur | -- | -- | signed char | -- | 1 | 1 | -70 |
| 0x35 | Weckleitung | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x36 | SG-Stati | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0x37 | Sperrenstatus | -- | -- | unsigned char | -- | 1 | 1 | 0 |
| 0xFF | ohne Bedeutung | 1 | -- | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-iarttexteerweitert"></a>
### IARTTEXTEERWEITERT

Dimensions: 4 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxx00 | 100 | Allgemeiner Fehler |
| xxxxxx01 | 101 | AFS ausgefallen |
| xxxxxx10 | 110 | AFS gestoert |
| xxxxxx11 | 111 | Allgemeiner Fehler |

<a id="table-zffehlercodeundart"></a>
### ZFFEHLERCODEUNDART

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 |

<a id="table-ercosekmodi"></a>
### ERCOSEKMODI

Dimensions: 7 rows × 2 columns

| COPM_STATI_NR | COPM_STATI_TEXT |
| --- | --- |
| 0x00 | OPM_OFF |
| 0x01 | OPM_PREDRIVE |
| 0x02 | OPM_POSTRUN |
| 0x03 | OPM_DRIVE |
| 0x04 | OPM_ERROR |
| 0x05 | OPM_INIT |
| 0xFF | unbekannter Betriebssystemstatus |

<a id="table-guerotor"></a>
### GUEROTOR

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NICHT gueltig |
| 0x01 | gueltig |
| 0x02 | nicht definiert |
| 0xFF | unbekannter Status |

<a id="table-statuscanfehler"></a>
### STATUSCANFEHLER

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Botschaft i.O. |
| 0x02 | Botschaft wurde nie empfangen |
| 0x04 | Mehrere Botschaften pro Abtastzyklus |
| 0x08 | Timeout - Botschaft faellt fuer 1 Abtastzyklus Zyklus aus |
| 0x10 | Fehlerwert laut Nachrichtenkatalog |
| 0x20 | Alive-Fehler |
| 0x40 | Checksummen-Fehler |
| 0x80 | Fehler von CRC Alive Fehlerwert Botschaft nie empfangen |
| 0xFF | unbekannter CAN Fehler Status |

<a id="table-guelwd"></a>
### GUELWD

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | gueltig |
| 0x01 | NICHT gueltig |
| 0x02 | Fehler |
| 0xFF | unbekannter Status |

<a id="table-guedsc"></a>
### GUEDSC

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | i.O. |
| 0x01 | passiv |
| 0x02 | defekt |
| 0x03 | LW Verifizierung aktiv |
| 0x04 | Traktionsmodus |
| 0x06 | Unterspannung DSC |
| 0x07 | Signal ungueltig |
| 0xFF | unbekannter Status |

<a id="table-regeldsc"></a>
### REGELDSC

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Regelung |
| 0x01 | ABS Regelung |
| 0x02 | ASC Regelung |
| 0x04 | DSC Regelung |
| 0x08 | HBA Regelung |
| 0x10 | MSR Regelung |
| 0x20 | EBV Regelung |
| 0x40 | FLR Regelung |
| 0xFF | Signal ungueltig |

<a id="table-szlprozinfo"></a>
### SZLPROZINFO

Dimensions: 3 rows × 2 columns

| SZL_PROZ_NR | SZL_PROZ_TEXT |
| --- | --- |
| 0x00 | SZL Ein-Prozessor; kein AFS |
| 0xA0 | SZL Zwei-Prozessor; AFS |
| 0xFF | unbekannter Status |

<a id="table-statusmaschineeingaenge"></a>
### STATUSMASCHINEEINGAENGE

Dimensions: 9 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | HL_OFF |
| 0x01 | HL_INIT |
| 0x02 | HL_ANGLE_INIT |
| 0x03 | HL_READY |
| 0x04 | HL_DRIVE |
| 0x05 | HL_DOWN |
| 0x06 | HL_ERROR |
| 0x07 | HL_PAUSE |
| 0xFF | unbekannt |

<a id="table-statusmaschinezustaende"></a>
### STATUSMASCHINEZUSTAENDE

Dimensions: 33 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | ccNOSTATE |
| 0x01 | unbekannt 1 |
| 0x02 | unbekannt 2 |
| 0x03 | unbekannt 3 |
| 0x04 | unbekannt 4 |
| 0x05 | unbekannt 5 |
| 0x06 | unbekannt 6 |
| 0x07 | unbekannt 7 |
| 0x08 | ccMSGREST |
| 0x09 | ccPREINIT |
| 0x0A | ccHWINIT |
| 0x0B | ccSWINIT |
| 0x0C | ccANGLEINIT |
| 0x0D | ccDRIVEREADY |
| 0x0E | ccDRIVEUP |
| 0x0F | ccDRIVE |
| 0x10 | ccDRIVEDOWN |
| 0x11 | ccPOWERDOWN |
| 0x12 | ccSLEEPIND |
| 0x13 | ccOFF |
| 0x14 | ccRESTART |
| 0x15 | ccGOPAUSE |
| 0x16 | ccPAUSE |
| 0x17 | ccGODRIVE |
| 0x18 | unbekannt 24 |
| 0x19 | unbekannt 25 |
| 0x1A | unbekannt 26 |
| 0x1B | unbekannt 27 |
| 0x1C | unbekannt 28 |
| 0x1D | unbekannt 29 |
| 0x1E | unbekannt 30 |
| 0x1F | ccERROR |
| 0xFF | unbekannt |

<a id="table-infoumweltzf"></a>
### INFOUMWELTZF

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x30 | 0x31 | 0x32 | 0x33 | 0x34 | 0x35 | 0x36 | 0x37 |

<a id="table-infoumweltbmw"></a>
### INFOUMWELTBMW

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x20 | 0x21 | 0x22 |

<a id="table-infofahrzeugstati"></a>
### INFOFAHRZEUGSTATI

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 |

<a id="table-infoallgemein"></a>
### INFOALLGEMEIN

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x01 | 0x02 | 0x03 | 0x04 |

<a id="table-ecoservo"></a>
### ECOSERVO

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | i.O., Ventile regeln den Strom korrekt ein |
| 0x01 | Kurzschluss einer Ventilleitung nach U Bat |
| 0x02 | Kurzschluss einer Ventilleitung nach GND |
| 0x03 | offene Leitung / Unterbrechung eines Stromkreises |
| 0x05 | Kurzschluss nach GND oder Unterbrechung der Leitung |
| 0x07 | Strom kann nicht eingestellt werden; Ventilstrom zu niedrig |
| 0x1A | Kurzschluss zwischen den Ventilleitungen |
| 0x57 | Uebertemperatur Endstufe CG207 |
| 0xFF | unbekannter Fehler |

<a id="table-sensorclustertyp"></a>
### SENSORCLUSTERTYP

Dimensions: 13 rows × 2 columns

| SCTYP_WERT | SCTYP_TEXT |
| --- | --- |
| 0x00 | Sensorcluster 3.6 |
| 0x01 | Sensorcluster 3.7 |
| 0x02 | Sensorcluster 3.8 |
| 0x03 | Sensorcluster 3.9 |
| 0x04 | Sensorcluster 3.10 |
| 0x05 | Sensorcluster 3.11 |
| 0x08 | Sensorcluster 3.0 |
| 0x09 | Sensorcluster 3.1 |
| 0x0A | Sensorcluster 3.2 |
| 0x0B | Sensorcluster 3.3 |
| 0x0D | TRW_YAW/LAT; |
| 0x0E | TRW_YAW/LAT/LONG |
| 0xFF | Signal ungueltig |

<a id="table-sensorclusterstatus1"></a>
### SENSORCLUSTERSTATUS1

Dimensions: 10 rows × 2 columns

| SCSTATUS1_WERT | SCSTATUS1_TEXT |
| --- | --- |
| 0x00 | i.O. |
| 0x01 | CRC Fehler |
| 0x02 | Ueberspannnung |
| 0x04 | Unterspannung |
| 0x08 | Sensor-interner Fehler |
| 0x10 | Synchronisationsfehler |
| 0x20 | Synchronisation Underflow |
| 0x40 | Synchronisation Overflow |
| 0x80 | Bus-Off Fehler |
| 0xFF | unbekannter Status |

<a id="table-cansignalfehler"></a>
### CANSIGNALFEHLER

Dimensions: 10 rows × 2 columns

| CANFEHLER_WERT | CANFEHLER_TEXT |
| --- | --- |
| 0x00 | i.O. |
| 0x01 | Checksumme Falsch |
| 0x02 | Alive-Zähler der Nachricht wurde mehr als um 1 erhöht |
| 0x04 | Alive-Zähler der Nachricht wurde nicht erhöht |
| 0x08 | Alive-Zähler der Nachricht stimmt nicht |
| 0x10 | Die Nachricht selbst ist nicht korrekt |
| 0x20 | Es ist ein Fehler in mindestens einen der Signale innerhalb einer Nachricht aufgetreten |
| 0x40 | Das System erwartet eine Nachricht innerhalb einer bestimmten Zeit. Diese ist aber nicht empfangen worden |
| 0x80 | Eine Nachricht ist mehr als einmal vom System empfangen worden |
| 0xFF | unbeaknnter Signal Fehler |

<a id="table-sensorclusterstatus2"></a>
### SENSORCLUSTERSTATUS2

Dimensions: 10 rows × 2 columns

| SCSTATUS2_WERT | SCSTATUS2_TEXT |
| --- | --- |
| 0x00 | i.O. |
| 0x01 | Fehler Gierrate 1 |
| 0x02 | Fehler Querbeschleunigung 1 |
| 0x04 | Fehler Gierbeschleunigung |
| 0x08 | Fehler Laengsbeschleunigung |
| 0x10 | Fehler Gierrate |
| 0x20 | Fehler Querbeschleunigung 2 |
| 0x40 | reserviert |
| 0x80 | reserviert |
| 0xFF | unbekannter Status |

<a id="table-sensclustersignalstatus"></a>
### SENSCLUSTERSIGNALSTATUS

Dimensions: 6 rows × 2 columns

| SCSIGNALSTATUS_WERT | SCSIGNALSTATUS_TEXT |
| --- | --- |
| 0x00 | Signal wie spezifiziert |
| 0x01 | Sensor nicht verfuegbar |
| 0x10 | Signalfehler |
| 0x21 | Initialisierung laeuft |
| 0x20 | Initialisierung beendet |
| 0xFF | unbekannter Status |

<a id="table-abgleichaktiv"></a>
### ABGLEICHAKTIV

Dimensions: 3 rows × 2 columns

| ABGLEICHAKTIV_WERT | ABGLEICHAKTIV_TEXT |
| --- | --- |
| 0x00 | Abgleich aktiv |
| 0x01 | Abgleich NICHT aktiv |
| 0xFF | unbekannter Status |

<a id="table-basisaktiv"></a>
### BASISAKTIV

Dimensions: 3 rows × 2 columns

| BASISAKTIV_WERT | BASISAKTIV_TEXT |
| --- | --- |
| 0x00 | Basiswert uebernehmen |
| 0x01 | Basiswert NICHT uebernehmen |
| 0xFF | unbekannter Status |

<a id="table-langzeitabgleich"></a>
### LANGZEITABGLEICH

Dimensions: 3 rows × 2 columns

| LANGZEITABGLEICH_WERT | LANGZEITABGLEICH_TEXT |
| --- | --- |
| 0x00 | Langzeitabgleich NICHT aktiv |
| 0x01 | Langzeitabgleich aktiv |
| 0xFF | unbekannter Status |
