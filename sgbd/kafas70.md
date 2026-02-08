# kafas70.prg

- Jobs: [84](#jobs)
- Tables: [55](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | KAFAS |
| ORIGIN | BMW EI-612 André Schwald |
| REVISION | 2.000 |
| AUTHOR | ADC_Automotive_Distance_Control_Systems_GmbH C/PSAD/AD Robert_A |
| COMMENT | N/A |
| PACKAGE | 1.50 |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default
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
- [STATUS_AUSSTATTUNG](#job-status-ausstattung) - KafasConfiguration KWP2000: $21 ReadDataByLocalIdentifier $23 STATUS_AUSSTATTUNG KafasConfiguration
- [STATUS_ERGEBNS_SLI](#job-status-ergebns-sli) - Gibt das Ergebnis der Verkeherzeichenerkennung aus. KWP2000: $21 ReadDataByLocalIdentifier $27 ERGEBNIS_SLI
- [STATUS_FLA_FERNLICHT_SCHALTEN](#job-status-fla-fernlicht-schalten) - Gibt aus, ob die Funktion Fernlichtassistent das Fernlicht ein- oder ausschaltet. KWP2000: $21 ReadDataByLocalIdentifier $2B STATUS_FLA_FERNLICHT_SCHALTEN
- [STATUS_FLA_GRUND_FL_ABSCHALTUNG](#job-status-fla-grund-fl-abschaltung) - Gibt die Parameter zur Funktion FLA aus. KWP2000: $21 ReadDataByLocalIdentifier $2A STATUS_FLA_GRUND_FL_ABSCHALTUNG
- [STATUS_INITIALISIERUNG](#job-status-initialisierung) - KWP2000: $21 ReadDataByLocalIdentifier $24 STATUS_INITIALISIERUNG
- [STATUS_KAFAS_KAM_SN_LESEN](#job-status-kafas-kam-sn-lesen) - Gibt die Seriennummer aus der Kamera aus. KWP2000: $21 ReadDataByLocalIdentifier $29 STATUS_KAFAS_KAM_SN_LESEN
- [STATUS_KAFAS_VINS_LESEN](#job-status-kafas-vins-lesen) - Gibt die VINs aus der Kamera und ECU aus. KWP2000: $21 ReadDataByLocalIdentifier $28 STATUS_KAFAS_VINS_LESEN
- [STATUS_KALIBRIERWERTE_KAFAS](#job-status-kalibrierwerte-kafas) - This service reads the camera calibration data from the camera's EEPROM KWP2000: $21 ReadDataByLocalIdentifier $2C STATUS_KALIBRIERWERTE_KAFAS
- [STATUS_KAMERAVERBINDUNG](#job-status-kameraverbindung) - Kann ermitteln, ob eine Kamera am TLC-Steuergerät angeschlossen ist KWP2000: $21 ReadDataByLocalIdentifier $22 STATUS_KAMERAVERBINDUNG
- [STATUS_KAMERAVERSORGUNG](#job-status-kameraversorgung) - Gibt die aktuellen Werte der Kamera aus KWP2000: $21 ReadDataByLocalIdentifier $21 STATUS_KAMERAVERSORGUNG
- [STATUS_KLEMMEN](#job-status-klemmen) - Job zum Auslesen der Klemmensteuerung am Steuergerät KWP2000: $21 ReadDataByLocalIdentifier $20 STATUS_KLEMMEN
- [STATUS_SPANNUNGEN](#job-status-spannungen) - KWP2000: $21 ReadDataByLocalIdentifier $25 STATUS_SPANNUNGEN
- [STEUERN_AKTUATOR](#job-steuern-aktuator) - Ansteuerung Demo Mode KWP2000: $2E WriteDataByCommonIdentifier .        $F195 STEUERN_AKTUATOR
- [STEUERN_ANZEIGE_KOMBI_SLI](#job-steuern-anzeige-kombi-sli) - Steuert die Ausgabe der Verkehrzeichenerkennung im Kombi an. KWP2000: $2E WriteDataByCommonIdentifier .        $F191 STEUERN_ANZEIGE_KOMBI_SLI
- [STEUERN_ANZEIGE_KOMBI_TLC](#job-steuern-anzeige-kombi-tlc) - Steuert die Anzeige im Kombi an. KWP2000: $2E WriteDataByCommonIdentifier .        $F190 STEUERN_ANZEIGE_KOMBI_TLC
- [STEUERN_BUS_NACHRICHT](#job-steuern-bus-nachricht) - Ansteuerung zum Senden einer ausgehenden Busnachricht mit vorgegebenen Werten. KWP2000: $2E WriteDataByCommonIdentifier .        $F193 STEUERN_BUS_NACHRICHT
- [STEUERN_DEMO_MODE_FLA](#job-steuern-demo-mode-fla) - Ansteuerung Demo Mode KWP2000: $2E WriteDataByCommonIdentifier .        $F194 STEUERN_DEMO_MODE_FLA
- [STEUERN_KALIBRIERUNG_MONTAGE](#job-steuern-kalibrierung-montage) - Startet die Kalibrierung der Kameras im Werk KWP2000: $31 StartRoutineByLocalIdentifier .      	 $20 KALIBRIERUNG_KAFAS_MONTAGE (TAC)
- [STATUS_STEUERN_KALIBRIERUNG_MONTAGE](#job-status-steuern-kalibrierung-montage) - Status Kalibrierung der Kameras im Werk KWP2000: $33 RequestRoutineResultsByLocalIdentifier .        $20 KALIBRIERUNG_KAFAS_MONTAGE (TAC)
- [STEUERN_KALIBRIERUNG_SERVICE_START](#job-steuern-kalibrierung-service-start) - Start calibration SPC KWP2000: $31 StartRoutineByLocalIdentifier .        $21 CalibrationSPC
- [STEUERN_KALIBRIERUNG_SERVICE_STOP](#job-steuern-kalibrierung-service-stop) - Stop calibration SPC KWP2000: $32 StopRoutineByLocalIdentifier .        $21 CalibrationSPC
- [STATUS_STEUERN_KALIBRIERUNG_SERVICE](#job-status-steuern-kalibrierung-service) - Get Status of calibration SPC KWP2000: $33 RequestRoutineResultsByLocalIdentifier .        $21 CalibrationSPC
- [STEUERN_METHODE_SLI](#job-steuern-methode-sli) - Gibt vor, welche Methode bei der Verkehrszeichenerkennung abgewendet werden soll. KWP2000: $2E WriteDataByCommonIdentifier .        $F192 STEUERN_METHODE_SLI
- [C_CHECKSUMME](#job-c-checksumme) - Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob
- [_HARDWARE_REVISION_LESEN](#job-hardware-revision-lesen) - Gibt aus, ob die Funktion Fernlichtassistent das Fernlicht ein- oder ausschaltet. KWP2000: $1A ReadECUIdentification $8A HardwareRevision
- [_STATUS_ECU_IDENT_LESEN](#job-status-ecu-ident-lesen) - Gibt die VIN aus. KWP2000: $22 ReadDataByCommonIdentifier .        $F18C STATUS_ECU_IDENT
- [_STEUERN_DIAGNOSE_MESSAGES_START](#job-steuern-diagnose-messages-start) - Control Diagnostic Messages KWP2000: $31 StartRoutineByLocalIdentifier .        $23 ControlDiagnosticMessages
- [_STEUERN_DIAGNOSE_MESSAGES_STOP](#job-steuern-diagnose-messages-stop) - Control Diagnostic Messages KWP2000: $32 StopRoutineByLocalIdentifier .        $23 ControlDiagnosticMessages
- [_STEUERN_KALIBRIERUNG_RESET](#job-steuern-kalibrierung-reset) - This service reset the camera calibration data from the camera's EEPROM KWP2000: $2E WriteDataByCommonIdentifier .        $F011 STEUERN_KALIBRIERUNG_RESET
- [_STEUERN_KALIBRIERWERTE_KAFAS](#job-steuern-kalibrierwerte-kafas) - This service updates the camera calibration data from the camera's EEPROM KWP2000: $2E WriteDataByCommonIdentifier .        $F010 STEUERN_KALIBRIERWERTE_KAFAS
- [_STEUERN_TEST_FUNKTIONAL_TLC_START](#job-steuern-test-funktional-tlc-start) - This control enables TLC performance tests KWP2000: $31 StartRoutineByLocalIdentifier .        $22 STEUERN_TEST_FUNKTIONAL_TLC
- [_STEUERN_TEST_FUNKTIONAL_TLC_STOP](#job-steuern-test-funktional-tlc-stop) - This control disables TLC performance tests KWP2000: $32 StopRoutineByLocalIdentifier .        $22 STEUERN_TEST_FUNKTIONAL_TLC
- [_STATUS_STEUERN_TEST_FUNKTIONAL_TLC](#job-status-steuern-test-funktional-tlc) - Get Status of TLC performance tests KWP2000: $33 RequestRoutineResultsByLocalIdentifier .        $22 STEUERN_TEST_FUNKTIONAL_TLC

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

<a id="job-status-ausstattung"></a>
### STATUS_AUSSTATTUNG

KafasConfiguration KWP2000: $21 ReadDataByLocalIdentifier $23 STATUS_AUSSTATTUNG KafasConfiguration

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VORHANDEN_TLC | int | Gibt an, ob die Funktion Time-to-Line Crossing vorhanden ist: 0= nicht vorhanden  1= vorhanden |
| STAT_VORHANDEN_TLC_TEXT | string | Gibt an, ob die Funktion Time-to-Line Crossing vorhanden ist: 0= nicht vorhanden  1= vorhanden |
| STAT_VORHANDEN_FLA | int | Gibt an, ob die Funktion Fernlichtassistent vorhanden ist: 0= nicht vorhanden  1= vorhanden |
| STAT_VORHANDEN_FLA_TEXT | string | Gibt an, ob die Funktion Fernlichtassistent vorhanden ist: 0= nicht vorhanden  1= vorhanden |
| STAT_VORHANDEN_SLI | int | Gibt an, ob die Funktion Speed-Limit-Info vorhanden ist: 0= nicht vorhanden  1= vorhanden |
| STAT_VORHANDEN_SLI_TEXT | string | Gibt an, ob die Funktion Speed-Limit-Info vorhanden ist: 0= nicht vorhanden  1= vorhanden |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ergebns-sli"></a>
### STATUS_ERGEBNS_SLI

Gibt das Ergebnis der Verkeherzeichenerkennung aus. KWP2000: $21 ReadDataByLocalIdentifier $27 ERGEBNIS_SLI

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KAMERA_ZEICHEN_NR | int | Gibt aus, welches Zeichen von der Kamera erkannt wurde: Results siehe TAB_ZEICHEN_KAMERA |
| STAT_KAMERA_ZEICHEN_NR_TEXT | string | Gibt aus, welches Zeichen von der Kamera erkannt wurde: Results siehe TAB_ZEICHEN_KAMERA |
| STAT_KAMERA_GESCHWINDIGKEIT_WERT | int | Gibt aus, welche Geschwindigkeit in den Zeichen erkannt wurde: 0 = Aufhebung alles, 5 bis 150 in 5-er Schritten. |
| STAT_KAMERA_GESCHWINDIGKEIT_EINH | string | KM/H |
| STAT_KAMERA_GESCHWINDIGKEIT_TEXT | string | Gibt aus, welche Geschwindigkeit in den Zeichen erkannt wurde: 0 = Aufhebung alles, 5 bis 150 in 5-er Schritten. |
| STAT_KARTE_ZEICHEN_NR | int | Gibt aus, welches Zeichen aus der Karte gelesen wurde: Results siehe TAB_ZEICHEN_KARTE |
| STAT_KARTE_ZEICHEN_NR_TEXT | string | Gibt aus, welches Zeichen aus der Karte gelesen wurde: Results siehe TAB_ZEICHEN_KARTE |
| STAT_KARTE_GESCHWINDIGKEIT_WERT | int | Gibt aus, welche Geschwindigkeit aus der Karte gelesen wurde: 0 = Aufhebung alles, 5 bis 150 in 5-er Schritten. |
| STAT_KARTE_GESCHWINDIGKEIT_EINH | string | KM/H |
| STAT_KARTE_GESCHWINDIGKEIT_TEXT | string | Gibt aus, welche Geschwindigkeit aus der Karte gelesen wurde: 0 = Aufhebung alles, 5 bis 150 in 5-er Schritten. |
| STAT_FUSIONIERT_ZEICHEN_NR | int | Gibt aus, welches Zeichen aus den fusioniertem Erkennungsergebnis ausgegeben wird: Results siehe TAB_ZEICHEN_FUSIONIERT |
| STAT_FUSIONIERT_ZEICHEN_NR_TEXT | string | Gibt aus, welches Zeichen aus den fusioniertem Erkennungsergebnis ausgegeben wird: Results siehe TAB_ZEICHEN_FUSIONIERT |
| STAT_FUSIONIERT_GESCHWINDIGKEIT_WERT | int | Gibt aus, welche Geschwindigkeit aus dem fusionierten Erkennungsergebnis ausgegeben wird: 0 = Aufhebung alles, 5 bis 150 in 5-er Schritten |
| STAT_FUSIONIERT_GESCHWINDIGKEIT_EINH | string | KM/H |
| STAT_FUSIONIERT_GESCHWINDIGKEIT_TEXT | string | Gibt aus, welche Geschwindigkeit aus dem fusionierten Erkennungsergebnis ausgegeben wird: 0 = Aufhebung alles, 5 bis 150 in 5-er Schritten |
| STAT_GUETE_KAM_SLI_GESCHW_WERT | int | Gibt aus, mit welcher Güte das Beschränkungs- und Aufhebungszeichen für Geschwindigkeiten mit der Kamera erkannt wurde: 0 - 100 |
| STAT_GUETE_KAM_SLI_GESCHW_EINH | string | KM/H |
| STAT_GUETE_KAM_SLI_GESCHW_TEXT | string | Gibt aus, mit welcher Güte das Beschränkungs- und Aufhebungszeichen für Geschwindigkeiten mit der Kamera erkannt wurde: 0 - 100 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fla-fernlicht-schalten"></a>
### STATUS_FLA_FERNLICHT_SCHALTEN

Gibt aus, ob die Funktion Fernlichtassistent das Fernlicht ein- oder ausschaltet. KWP2000: $21 ReadDataByLocalIdentifier $2B STATUS_FLA_FERNLICHT_SCHALTEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FLA_FERNLICHT_SCHALTEN | int | Gibt aus, ob das Fernlicht durch den Fernlichtassistenten aus- oder eingeschaltet wird: 0 = Keine Empfehlung (Defekt erkannt, Sichtfeld verdreckt), 1 = Fernlicht AUS, 2 = Fernlicht EIN |
| STAT_FLA_FERNLICHT_SCHALTEN_TEXT | string | Gibt aus, ob das Fernlicht durch den Fernlichtassistenten aus- oder eingeschaltet wird: 0 = Keine Empfehlung (Defekt erkannt, Sichtfeld verdreckt), 1 = Fernlicht AUS, 2 = Fernlicht EIN |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fla-grund-fl-abschaltung"></a>
### STATUS_FLA_GRUND_FL_ABSCHALTUNG

Gibt die Parameter zur Funktion FLA aus. KWP2000: $21 ReadDataByLocalIdentifier $2A STATUS_FLA_GRUND_FL_ABSCHALTUNG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FLA_AUSREICHENDE_BELEUCHTUNG | int | Gibt aus, ob eine ausreichende Beleuchtung erkannt worden ist: 0 = keine ausreichende Beleuchtung erkannt, 1 = ausreichende Beleuchtung erkannt |
| STAT_FLA_AUSREICHENDE_BELEUCHTUNG_TEXT | string | Gibt aus, ob eine ausreichende Beleuchtung erkannt worden ist: 0 = keine ausreichende Beleuchtung erkannt, 1 = ausreichende Beleuchtung erkannt |
| STAT_FLA_VORAUSFAHRENDES_FAHRZEUG | int | Gibt aus, ob ein vorausfahrendes Fahrzeug erkannt worden ist: 0 = kein Fahrzeug erkannt, 1 = Fahrzeug erkannt |
| STAT_FLA_VORAUSFAHRENDES_FAHRZEUG_TEXT | string | Gibt aus, ob ein vorausfahrendes Fahrzeug erkannt worden ist: 0 = kein Fahrzeug erkannt, 1 = Fahrzeug erkannt |
| STAT_FLA_ENTGEGENKOMMENDES_FAHRZEUG | int | Gibt aus, ob ein entgegenkommendes Fahrzeug erkannt worden ist: 0 = kein Fahrzeug erkannt, 1 = Fahrzeug erkannt |
| STAT_FLA_ENTGEGENKOMMENDES_FAHRZEUG_TEXT | string | Gibt aus, ob ein entgegenkommendes Fahrzeug erkannt worden ist: 0 = kein Fahrzeug erkannt, 1 = Fahrzeug erkannt |
| STAT_FLA_TAGERKENNUNG | int | Gibt aus, ob Umgebungshelligkeit (Tag) erkannt worden ist: 0 = kein Helligkeit (Nacht) erkannt, 1 = Helligkeit (Tag) erkannt |
| STAT_FLA_TAGERKENNUNG_TEXT | string | Gibt aus, ob Umgebungshelligkeit (Tag) erkannt worden ist: 0 = kein Helligkeit (Nacht) erkannt, 1 = Helligkeit (Tag) erkannt |
| STAT_FLA_GESCHWINDIGKEIT | int | Gibt aus, ob die Geschwindigkeit unterhalb der Grenze erkannt worden ist: 0 = Geschwindigkeit überhalb der Grenze, 1 = Geschwindigkeit unterhalb der Grenze |
| STAT_FLA_GESCHWINDIGKEIT_TEXT | string | Gibt aus, ob die Geschwindigkeit unterhalb der Grenze erkannt worden ist: 0 = Geschwindigkeit überhalb der Grenze, 1 = Geschwindigkeit unterhalb der Grenze |
| STAT_FLA_VERZOEGERUNG | int | Gibt aus, ob wegen einer Zeiterzögerung das Fernlicht nicht eingeschaltet wird: 0 = keine Zeitverzögerung, 1 = Zeitverzögerung |
| STAT_FLA_VERZOEGERUNG_TEXT | string | Gibt aus, ob wegen einer Zeiterzögerung das Fernlicht nicht eingeschaltet wird: 0 = keine Zeitverzögerung, 1 = Zeitverzögerung |
| STAT_FLA_SENSORTEMPERATUR | int | Gibt aus, ob Temperatur des Sensors das Einschalten des Fernlicht verhindert: 0 = Temperatur außerhalb des Arbeitsbereiches, 1 = Temperatur zulässig |
| STAT_FLA_SENSORTEMPERATUR_TEXT | string | Gibt aus, ob Temperatur des Sensors das Einschalten des Fernlicht verhindert: 0 = Temperatur außerhalb des Arbeitsbereiches, 1 = Temperatur zulässig |
| STAT_FLA_NEBELERKENNUNG | int | Gibt aus, ob Nebel erkannt worden ist: 0 = kein Nebel, 1 = Nebel erkannt |
| STAT_FLA_NEBELERKENNUNG_TEXT | string | Gibt aus, ob Nebel erkannt worden ist: 0 = kein Nebel, 1 = Nebel erkannt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-initialisierung"></a>
### STATUS_INITIALISIERUNG

KWP2000: $21 ReadDataByLocalIdentifier $24 STATUS_INITIALISIERUNG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KALIBRIERUNG_KAFAS_INIT_NR | int | Ausgabe des aktuellen Zustands der Initialisierung (Kalibrierung) der Kamera: 0 (0x00) = nicht initialisiert 1 (0x01) = Initialisierung in Ordnung 255 (0xFF) = Initialisierung nicht in Ordnung |
| STAT_KALIBRIERUNG_KAFAS_INIT_NR_TEXT | string | Status of the camera calibration: 0x00 - KAFAS nicht initialisiert 0x01 - KAFAS initialisiert 0x02 - Information noch nicht verfügbar 0xFF - KAFAS calibration not correct |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kafas-kam-sn-lesen"></a>
### STATUS_KAFAS_KAM_SN_LESEN

Gibt die Seriennummer aus der Kamera aus. KWP2000: $21 ReadDataByLocalIdentifier $29 STATUS_KAFAS_KAM_SN_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KAFAS_KAM_SN_WERT | string | Ausgabe der Seriennummer der Kamera. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kafas-vins-lesen"></a>
### STATUS_KAFAS_VINS_LESEN

Gibt die VINs aus der Kamera und ECU aus. KWP2000: $21 ReadDataByLocalIdentifier $28 STATUS_KAFAS_VINS_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KAFAS_KAM_VIN_WERT | string | Ausgabe der 7-stelligen Fahrgestellnummer aus der Kamera. |
| STAT_KAFAS_ECU_VIN_WERT | string | Ausgabe der 7-stelligen Fahrgestellnummer aus dem Steuergerät. |
| STAT_KAFAS_VIN_STATUS_NR | int | Gibt aus, ob die Zuordnung Kamera zu Steuergerät übereinstimmt: 0x00: KEINE UEBEREINSTIMMUNG, 0x01 UEBEREINSTIMMUNG |
| STAT_KAFAS_VIN_STATUS_NR_TEXT | string | Gibt aus, ob die Zuordnung Kamera zu Steuergerät übereinstimmt: 0x00: KEINE UEBEREINSTIMMUNG, 0x01 UEBEREINSTIMMUNG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kalibrierwerte-kafas"></a>
### STATUS_KALIBRIERWERTE_KAFAS

This service reads the camera calibration data from the camera's EEPROM KWP2000: $21 ReadDataByLocalIdentifier $2C STATUS_KALIBRIERWERTE_KAFAS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFFLINE_YAW_WERT | int | Offline Yaw-Winkel |
| STAT_OFFLINE_YAW_WERT_TEXT | string | Offline Yaw-Winkel |
| STAT_OFFLINE_HORIZON_WERT | int | Offline Horizon-Winkel |
| STAT_OFFLINE_HORIZON_WERT_TEXT | string | Offline Horizon-Winkel |
| STAT_OFFLINE_ROLL_WERT | int | Offline Roll-Winkel |
| STAT_OFFLINE_ROLL_WERT_TEXT | string | Offline Roll-Winkel |
| STAT_ONLINE_YAW_WERT | int | Online Yaw-Winkel |
| STAT_ONLINE_YAW_WERT_TEXT | string | Online Yaw-Winkel |
| STAT_ONLINE_HORIZON_WERT | int | Online Horizon-Winkel |
| STAT_ONLINE_HORIZON_WERT_TEXT | string | Online Horizon-Winkel |
| STAT_ONLINE_ROLL_WERT | int | Online Roll-Winkel |
| STAT_ONLINE_ROLL_WERT_TEXT | string | Online Roll-Winkel |
| STAT_KAM_HOEHE_WERT | unsigned int | Kamera-Verbauhöhe |
| STAT_KAM_HOEHE_WERT_TEXT | string | Kamera-Verbauhöhe |
| STAT_BRENNWEITE_WERT | unsigned int | Brennweite |
| STAT_BRENNWEITE_WERT_TEXT | string | Brennweite |
| STAT_GRABBING_SHIFT_WERT | unsigned int | Grabbing-Shift |
| STAT_GRABBING_SHIFT_WERT_TEXT | string | Grabbing-Shift |
| STAT_FAHRGESTELLNR_WERT | string | Fahrgestellnummer in der Kamera |
| STAT_FAHRGESTELLNR_WERT_TEXT | string | Fahrgestellnummer in der Kamera |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kameraverbindung"></a>
### STATUS_KAMERAVERBINDUNG

Kann ermitteln, ob eine Kamera am TLC-Steuergerät angeschlossen ist KWP2000: $21 ReadDataByLocalIdentifier $22 STATUS_KAMERAVERBINDUNG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KAFAS_VERBINDUNG_KAM_NR | int | 0x01 = Kameraverbindung in Ordnung 0x02 = Fehler nur an Videoleitungen 0x04 = Fehler nur an Dataleitungen 0x08 = LVDS Leitungsfehler 0x10 = Fehler nur an Versorgungsleitungen 0xFF = Information nicht verfügbar, Anfrage wiederholen |
| STAT_KAFAS_VERBINDUNG_KAM_NR_TEXT | string | See above |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kameraversorgung"></a>
### STATUS_KAMERAVERSORGUNG

Gibt die aktuellen Werte der Kamera aus KWP2000: $21 ReadDataByLocalIdentifier $21 STATUS_KAMERAVERSORGUNG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KAFAS_SPANNUNG_KAM_WERT | int | Spannungswert an der Kamera 1mV resolution |
| STAT_KAFAS_SPANNUNG_KAM_EINH | string | Spannungswert an der Kamera resolution |
| STAT_KAFAS_STROM_KAM_WERT | int | Stromaufnahme der Kamera 1mA resolution |
| STAT_KAFAS_STROM_KAM_EINH | string | Stromaufnahme der Kamera resolution |
| STAT_KAFAS_SPANNUNG_KAM_NR | int | 0x01 - unterhalb des Limits 0x02 - normal 0x03 - oberhalb des Limits 0xff - invalid |
| STAT_KAFAS_SPANNUNG_KAM_NR_TEXT | string | Siehe STAT_KAFAS_SPANNUNG_KAM_NR |
| STAT_KAFAS_STROM_KAM_NR | int | 0x01 - unterhalb des Limits 0x02 - normal 0x03 - oberhalb des Limits 0xff - invalid |
| STAT_KAFAS_STROM_KAM_NR_TEXT | string | Siehe STAT_KAFAS_STROM_KAM_NR |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klemmen"></a>
### STATUS_KLEMMEN

Job zum Auslesen der Klemmensteuerung am Steuergerät KWP2000: $21 ReadDataByLocalIdentifier $20 STATUS_KLEMMEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_KLEMME_15_WERT | real | Spannungswert am Steuergerät an Klemme 15 (auf eine Nachkommastelle genau) |
| STAT_SPANNUNG_KLEMME_15_EINH | string | Spannungswert am Steuergerät an Klemme 15 (auf eine Nachkommastelle genau) |
| STAT_SPANNUNG_KLEMME_15_TEXT | string | Spannungswert am Steuergerät an Klemme 15 (auf eine Nachkommastelle genau) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spannungen"></a>
### STATUS_SPANNUNGEN

KWP2000: $21 ReadDataByLocalIdentifier $25 STATUS_SPANNUNGEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KAFAS_ECU_SPG_1_8V_WERT | int | Spannungen des Netzteils in der ECU Netzteil  (1,8V) - 1mV resolution |
| STAT_KAFAS_ECU_SPG_1_8V_EINH | string | See Above |
| STAT_KAFAS_ECU_SPG_1_8V_NR | int | 0x01: unterhalb des Limits 0x02: normal 0x03: überhalb des Limits 0x04: ungültig 0xFF: ungültig |
| STAT_KAFAS_ECU_SPG_1_8V_NR_TEXT | string | 0x01: unterhalb des Limits 0x02: normal 0x03: überhalb des Limits 0xFF - invalid |
| STAT_KAFAS_ECU_SPG_3_3V_WERT | int | Spannungen des Netzteils in der ECU Netzteil (3,3V) |
| STAT_KAFAS_ECU_SPG_3_3V_EINH | string | See Above |
| STAT_KAFAS_ECU_SPG_3_3V_NR | int | 0x01: unterhalb des Limits 0x02: normal 0x03: überhalb des Limits 0x04: ungültig 0xFF: ungültig |
| STAT_KAFAS_ECU_SPG_3_3V_NR_TEXT | string | See Above |
| STAT_KAFAS_ECU_SPG_5V_WERT | int | Spannungen des Netzteils in der ECU Netzteil (5V) |
| STAT_KAFAS_ECU_SPG_5V_EINH | string | See Above |
| STAT_KAFAS_ECU_SPG_5V_NR | int | 0x01: unterhalb des Limits 0x02: normal 0x03: überhalb des Limits 0x04: ungültig 0xFF: ungültig |
| STAT_KAFAS_ECU_SPG_5V_NR_TEXT | string | See Above |
| STAT_KAFAS_ECU_SPG_BORDNETZ_WERT | int | Spannungen des Bordnetzes |
| STAT_KAFAS_ECU_SPG_BORDNETZ_EINH | string | See Above |
| STAT_KAFAS_ECU_SPG_BORDNETZ_NR | int | 0x01: unterhalb des Limits 0x02: normal 0x03: überhalb des Limits 0x04: ungültig 0xFF: ungültig |
| STAT_KAFAS_ECU_SPG_BORDNETZ_NR_TEXT | string | See Above |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-aktuator"></a>
### STEUERN_AKTUATOR

Ansteuerung Demo Mode KWP2000: $2E WriteDataByCommonIdentifier .        $F195 STEUERN_AKTUATOR

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DAUER | int | Ansteuerdauer in Sekunden 1-250 : 0.1-25.0 Sekunden 0 = Ansteuerung AUS |
| ANLAUFRAMPE | int | Werte von 0, 1 und 2 sind möglich "0" entspricht steilster Rampe, "2" entspricht der flachsten Rampe Der genaue Signalverlaufen der Rampe ist in der Lenkradelektronik festgelegt. |
| STOPRAMPE | int | Werte von 0, 1 und 2 sind möglich "0" entspricht steilster Rampe, "2" entspricht der flachsten Rampe Der genaue Signalverlaufen der Rampe ist in der Lenkradelektronik festgelegt. |
| AMPLITUDE | int | Vibrationsstärke  es sind Amplituden von 0-14 (dezimal) möglich. |
| FREQUENZ | int | Frequenz der Vibration, Frequenzstufen von 0-14 (dezimal) sind möglich. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-anzeige-kombi-sli"></a>
### STEUERN_ANZEIGE_KOMBI_SLI

Steuert die Ausgabe der Verkehrzeichenerkennung im Kombi an. KWP2000: $2E WriteDataByCommonIdentifier .        $F191 STEUERN_ANZEIGE_KOMBI_SLI

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTUELLES_SEGMENT_ZEICHEN | int | Gibt an, welches Zeichen angezeigt werden soll: Argumente siehe TAB_ART_ZEICHEN 0x00 - set PRES_WDR_LIM_V to "kein Zeichen verfügbar" 0x01 - set PRES_WDR_LIM_V to "Beschränkungszeichen" 0x02 - set PRES_WDR_LIM_V to "Aufhebungszeichen" 0x03 - set PRES_WDR_LIM_V to "ungueltig" |
| AKTUELLES_SEGMENT_GESCHWINDIGKEIT | int | Gibt an, welche Geschwindigkeit für die Zeichen angezeigt werden soll: 0 = Aufhebungszeichen alles, 5 bis 150 in 5-er Schritten. 0x00 - set PRES_CLAS_LIM_V to "general end of restriction" 5 to 150 (only multiples of 5 allowed) - set PRES_CLAS_LIM_V to input value divided by 5 0xfe - set PRES_CLAS_LIM_V to "nicht verfuegbar" 0xff - set PRES_CLAS_LIM_V to "ungueltig" |
| KOMMENDES_SEGMENT_ZEICHEN | int | Gibt an, welches Zeichen angezeigt werden soll: Argument siehe TAB_ART_ZEICHEN 0x00 - set NXT_WDR_LIM_V to "kein Zeichen verfügbar" 0x01 - set NXT_WDR_LIM_V to "Beschränkungszeichen" 0x02 - set NXT_WDR_LIM_V to "Aufhebungszeichen" 0x03 - set NXT_WDR_LIM_V to "ungueltig" |
| KOMMENDES_SEGMENT_GESCHWINDIGKEIT | int | Gibt an, welche Geschwindigkeit für die Zeichen angezeigt werden soll: 0 = Aufhebung alles, 5 bis 150 in 5-er Schritten. 0x00 - set NXT_CLAS_LIM_V to "general end of restriction" 5 to 150 (only multiples of 5 allowed) - set NXT_CLAS_LIM_V to input value divided by 5 0xfe -  set NXT_CLAS_LIM_V to "nicht verfuegbar" 0xff -  set NXT_CLAS_LIM_V to "ungueltig" |
| ANZEIGE_UEBERHOLVERBOTSZEICHEN | int | Gibt an, welches Überholverbotszeichen angezeigt werden soll: Argumente siehe TAB_ART_UEBERHOL_ZEICHEN 0x00 - kein Überholverbot 0x01 - Überholverbot PKW 0x02 - Aufhebung Überholverbot PKW 0x03 - Überholverbot PKW mit Anhänger 0x04 - Aufhebung Überholverbot PKW mit Anhänger 0x05 - Überholverbot LKW 0x06 - Aufhebung Überholverbot LKW 0x07 - andere Überholverbote |
| LAENDERKODIERUNG_VERKEHRSZEICHEN | int | Angabe der Länderkodierung der Verkehrszeichen, Argumente siehe TAB_ART_LAENDERKODIERUNG 0x00 = EU weiss 0x01 = EU gelb 0x02 = US weiss 0x03 = US gelb 0x04 = generisch 0x05...0x0D = reserved 0x0E = nicht verfuegbar 0x0F = ungueltig |
| ANZEIGE_TEXT_MELDUNG | int | Gibt an, welche Textmeldung angezeigt werden soll: Argumente siehe TAB_ART_MELDUNG 0x00 = keine Textmeldung 0x01 = nur mit Navigations - DVD 0x02 = in diesem Land nicht verfuegbar 0x03 = Navigationsdaten nicht verfuegbar 0x07 = ungueltig |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-anzeige-kombi-tlc"></a>
### STEUERN_ANZEIGE_KOMBI_TLC

Steuert die Anzeige im Kombi an. KWP2000: $2E WriteDataByCommonIdentifier .        $F190 STEUERN_ANZEIGE_KOMBI_TLC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | int | 00h  Alle Anzeigen im Kombi ausgeschaltet 01h  Set ST_TLC aktiv, 02h  Balken rechts anzeigen, 04h  Balken links anzeigen, 07h  Balken rechts und links anzeigen 08h  Aktivierungsanzeige = Verfügbarkeitsschwelle anzeigen 10h  Verfügbarkeit rechts 20h  Verfügbarkeit links FFh  Ungültig |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AKTION_TEXT | string | Action to perform: 00h  Alle Anzeigen im Kombi ausgeschaltet 01h  Set ST_TLC aktiv, 02h  Balken rechts anzeigen, 04h  Balken links anzeigen, 07h  Balken rechts und links anzeigen 08h  Aktivierungsanzeige = Verfügbarkeitsschwelle anzeigen 10h  Verfügbarkeit rechts 20h  Verfügbarkeit links FFh  Invalid |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bus-nachricht"></a>
### STEUERN_BUS_NACHRICHT

Ansteuerung zum Senden einer ausgehenden Busnachricht mit vorgegebenen Werten. KWP2000: $2E WriteDataByCommonIdentifier .        $F193 STEUERN_BUS_NACHRICHT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | int | Gibt an, ob das Fernlicht über BUS aus- oder eingeschaltet werden soll: 0 = AUS, 1 = EIN, 2 = Keine Empfehlung 3 = Zurück zum Normalmodus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AKTION_TEXT | string | Action to perform: 00h - Set CTR_MAB to "off" 01h - Set CTR_MAB to "on" 02h - Set CTR_MAB to "no recomendation" 03h - Return to normal operation immediately |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-demo-mode-fla"></a>
### STEUERN_DEMO_MODE_FLA

Ansteuerung Demo Mode KWP2000: $2E WriteDataByCommonIdentifier .        $F194 STEUERN_DEMO_MODE_FLA

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | int | 0 = Demo-Mode Ausschalten, 1 = Demo-Mode Einschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AKTION_TEXT | string | Action to perform: 0 = Demo-Mode Ausschalten, 1 = Demo-Mode Einschalten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kalibrierung-montage"></a>
### STEUERN_KALIBRIERUNG_MONTAGE

Startet die Kalibrierung der Kameras im Werk KWP2000: $31 StartRoutineByLocalIdentifier .      	 $20 KALIBRIERUNG_KAFAS_MONTAGE (TAC)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TARGET_POSITION | int | Gibt an, welche Seite mit dem Target kalibriert werden soll: 0x01 = LINKS, 0x02 = RECHTS |
| ENTFERNUNG_X | int | Angabe der Entfernung zwischen Vorderachse des Fahrzeugs und Gerüst. |
| ENTFERNUNG_Y | int | Angabe der Entfernung in y-Richtung von der Fahrzeugmitte zur gedachten Mittellinie zwischen den beiden Targetpositionen, wobei eine Verschiebung nach links in Fahrtrichtung einem positiven Wert entspricht. |
| HOEHE_TARGET_OBEN | int | Angabe der Höhe vom Boden bis zur Mitte des oberen Targets. |
| HOEHE_TARGET_UNTEN | int | Angabe der Höhe vom Boden bis zur Mitte des unteren Targets. |
| HOEHE_KAMERA | int | Angabe der tatsächlichen, am Kalibrierstand gemessenen Verbauhöhe der Kamera. |
| ENTFERNUNG_TARGETS | int | Gibt an, wie weit die einzelnen Targetpositionen auseinander liegen. Gemessen wird von der linken Außenkante des Targets in der linken Position bis zur linken Außenkante des Targets in der rechten Position. |
| QUADRAT_GROESSE | int | Angabe der Größe der Quadrate des Schachbrettmusters der Targets. Diese Parameter sind notwendig, um TLC auch an geänderten Kalibrierständen kalibrieren zu können. Alle Parameter sind als 2Byte Signed Integer mit einen Auflösung von 1 mm definiert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TAC_STATUS | unsigned int | status byte of calibration as integer |
| TAC_TEXT | string | status byte of calibration as text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-steuern-kalibrierung-montage"></a>
### STATUS_STEUERN_KALIBRIERUNG_MONTAGE

Status Kalibrierung der Kameras im Werk KWP2000: $33 RequestRoutineResultsByLocalIdentifier .        $20 KALIBRIERUNG_KAFAS_MONTAGE (TAC)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KALIB_KAFAS_MONTAGE_NR_WERT | int | Ausgabe des Status der Kalibierung: 0x00 - TAC in progress 0x01 - calibratiion sucessfully completed 0x02 - Success -&gt; continue calibrating 0x03 - insufficient image quality 0x04 - no target located 0x05 - targets out of range 0x06 - inconsistency between left and right target  (for instance wrong pitch angle) 0x07 - TAC parameters out of range 0x08 - calibration values out of range (Note: limits are codable in  EEPROM) 0x09 - TAC undefined error |
| STAT_KALIB_KAFAS_MONTAGE_NR_TEXT | string | Ausgabe des Status der Kalibierung: 0x00 Kalibrierung laeuft gerade, 0x01 Kalibrierung erfolgreich abgeschlossen, 0x02 Erfolg - fortfahren mit der Kalibrierung, 0x03 Unzureichende Bildqualität, 0x04 kein Target gefunden, 0x05 Targets befinden sich außerhalb des Bereichs, 0x06 Inkonsistenz zwischen linkem und rechtem Target  z.B. falscher Nickwinkel, 0x07 empfangene Parameter außerhalb der Limits, 0x08 empfangene Parameter außerhalb der Limits (Parameter codierbar in EEPROM) 0x09 TAC undefined error |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kalibrierung-service-start"></a>
### STEUERN_KALIBRIERUNG_SERVICE_START

Start calibration SPC KWP2000: $31 StartRoutineByLocalIdentifier .        $21 CalibrationSPC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-kalibrierung-service-stop"></a>
### STEUERN_KALIBRIERUNG_SERVICE_STOP

Stop calibration SPC KWP2000: $32 StopRoutineByLocalIdentifier .        $21 CalibrationSPC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-steuern-kalibrierung-service"></a>
### STATUS_STEUERN_KALIBRIERUNG_SERVICE

Get Status of calibration SPC KWP2000: $33 RequestRoutineResultsByLocalIdentifier .        $21 CalibrationSPC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KALIB_KAFAS_SERVICE_NR_WERT | int | 0x00 Blockagetest nicht gestartet, SPC (Service Point Calibration) nicht gestartet, 0x01 Blockagetest aktiv, SPC nicht gestartet, 0x02 Blockagetest erfolgreich beendet, SPC aktiv, 0x03 Blockagetest erfolgreich beendet, SPC erfolgreich abgeschlossen |
| STAT_KALIB_KAFAS_SERVICE_NR_TEXT | string | 0x00 Blockagetest nicht gestartet, SPC (Service Point Calibration) nicht gestartet, 0x01 Blockagetest aktiv, SPC nicht gestartet, 0x02 Blockagetest erfolgreich beendet, SPC aktiv, 0x03 Blockagetest erfolgreich beendet, SPC erfolgreich abgeschlossen |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-methode-sli"></a>
### STEUERN_METHODE_SLI

Gibt vor, welche Methode bei der Verkehrszeichenerkennung abgewendet werden soll. KWP2000: $2E WriteDataByCommonIdentifier .        $F192 STEUERN_METHODE_SLI

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| METHODE_SLI | int | Argumente siehe TAB_METHODE_SLI |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| METHODE_SLI_TEXT | string | Argumente siehe TAB_METHODE_SLI 00h - activate camera-based recognition only 01h - acivate map-based recognition only 02h - activate consolidated recognition FFh - reset to standard configuration coded in EEPROM |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-checksumme"></a>
### C_CHECKSUMME

Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte  21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| OUT_BUFFER | binary | Als Result wird der gefuellte Binaerbuffer zurueckgegeben Der Binaerbuffer hat den Aufbau von BINAER_BUFFER |

<a id="job-hardware-revision-lesen"></a>
### _HARDWARE_REVISION_LESEN

Gibt aus, ob die Funktion Fernlichtassistent das Fernlicht ein- oder ausschaltet. KWP2000: $1A ReadECUIdentification $8A HardwareRevision

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HARDWARE_REVISION_LESEN | int | Ausgabe der Hardware Revision. table JobResult HW_REVISION_TAB |
| HARDWARE_REVISION_LESEN_TEXT | string | Ausgabe der Hardware Revision. table JobResult HW_REVISION_TAB |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ecu-ident-lesen"></a>
### _STATUS_ECU_IDENT_LESEN

Gibt die VIN aus. KWP2000: $22 ReadDataByCommonIdentifier .        $F18C STATUS_ECU_IDENT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ECU_IDENT | string | Ausgabe der ECU IDENT. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnose-messages-start"></a>
### _STEUERN_DIAGNOSE_MESSAGES_START

Control Diagnostic Messages KWP2000: $31 StartRoutineByLocalIdentifier .        $23 ControlDiagnosticMessages

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-diagnose-messages-stop"></a>
### _STEUERN_DIAGNOSE_MESSAGES_STOP

Control Diagnostic Messages KWP2000: $32 StopRoutineByLocalIdentifier .        $23 ControlDiagnosticMessages

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-kalibrierung-reset"></a>
### _STEUERN_KALIBRIERUNG_RESET

This service reset the camera calibration data from the camera's EEPROM KWP2000: $2E WriteDataByCommonIdentifier .        $F011 STEUERN_KALIBRIERUNG_RESET

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kalibrierwerte-kafas"></a>
### _STEUERN_KALIBRIERWERTE_KAFAS

This service updates the camera calibration data from the camera's EEPROM KWP2000: $2E WriteDataByCommonIdentifier .        $F010 STEUERN_KALIBRIERWERTE_KAFAS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OFFLINE_YAW | int | Offline Yaw-Winkel |
| OFFLINE_HORIZON | int | Offline Horizon-Winkel |
| OFFLINE_ROLL | int | Offline Roll-Winkel |
| ONLINE_YAW | int | Online Yaw-Winkel |
| ONLINE_HORIZON | int | Online Horizon-Winkel |
| ONLINE_ROLL | int | Online Roll-Winkel |
| KAM_HOEHE | unsigned int | Kamera-Verbauhöhe |
| BRENNWEITE | unsigned int | Brennweite |
| GRABBING_SHIFT | unsigned int | Grabbing-Shift |
| FAHRGESTELLNR | string | Fahrgestellnummer(VIN) in der Kamera |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag zu SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-test-funktional-tlc-start"></a>
### _STEUERN_TEST_FUNKTIONAL_TLC_START

This control enables TLC performance tests KWP2000: $31 StartRoutineByLocalIdentifier .        $22 STEUERN_TEST_FUNKTIONAL_TLC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GESCHWINDIGKEIT | int | Geschwindigkeit |
| YAW | int | Yaw-Winkel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-steuern-test-funktional-tlc-stop"></a>
### _STEUERN_TEST_FUNKTIONAL_TLC_STOP

This control disables TLC performance tests KWP2000: $32 StopRoutineByLocalIdentifier .        $22 STEUERN_TEST_FUNKTIONAL_TLC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

<a id="job-status-steuern-test-funktional-tlc"></a>
### _STATUS_STEUERN_TEST_FUNKTIONAL_TLC

Get Status of TLC performance tests KWP2000: $33 RequestRoutineResultsByLocalIdentifier .        $22 STEUERN_TEST_FUNKTIONAL_TLC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STEUERN_TEST_FUNKTIONAL_TLC | int | 0x00 - Service not running (yaw and speed values from vehicle CAN) 0x01 - Service running (yaw and speed values from diagnostic job) |
| STAT_STEUERN_TEST_FUNKTIONAL_TLC_TEXT | string | 0x00 - Service not running (yaw and speed values from vehicle CAN) 0x01 - Service running (yaw and speed values from diagnostic job) |
| JOB_STATUS | string | OKAY, if error-free table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | request to ECU |
| _TEL_ANTWORT | binary | ECU response |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (118 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (125 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (5 × 2)
- [FORTTEXTE](#table-forttexte) (50 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (49 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (14 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (13 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (4 × 9)
- [TAC_TEXT](#table-tac-text) (11 × 2)
- [SPANNUNGEN_TEXT](#table-spannungen-text) (5 × 2)
- [VORHANDEN_TEXT](#table-vorhanden-text) (3 × 2)
- [ZEICHEN_NR_TEXT](#table-zeichen-nr-text) (5 × 2)
- [GESCHWINDIGKEIT_TEXT](#table-geschwindigkeit-text) (4 × 2)
- [GUETE_TEXT](#table-guete-text) (3 × 2)
- [BELEUCHTUNG_TEXT](#table-beleuchtung-text) (4 × 2)
- [V_FAHRZEUG_TEXT](#table-v-fahrzeug-text) (4 × 2)
- [E_FAHRZEUG_TEXT](#table-e-fahrzeug-text) (4 × 2)
- [FLA_TAGERKENNUNG_TEXT](#table-fla-tagerkennung-text) (4 × 2)
- [FLA_GESCHWINDIGKEIT_TEXT](#table-fla-geschwindigkeit-text) (4 × 2)
- [FLA_VERZOEGERUNG_TEXT](#table-fla-verzoegerung-text) (4 × 2)
- [FLA_SENSORTEMPERATUR_TEXT](#table-fla-sensortemperatur-text) (3 × 2)
- [FLA_NEBELERKENNUNG_TEXT](#table-fla-nebelerkennung-text) (4 × 2)
- [VERBINDUNG_KAM_NR_TEXT](#table-verbindung-kam-nr-text) (8 × 2)
- [KAFAS_INIT_TEXT](#table-kafas-init-text) (5 × 2)
- [VIN_STATUS_TEXT](#table-vin-status-text) (4 × 2)
- [SPANNUNG_STROM_KAM_TEXT](#table-spannung-strom-kam-text) (5 × 2)
- [SAK_AKTION_TEXT](#table-sak-aktion-text) (10 × 2)
- [SBN_AKTION_TEXT](#table-sbn-aktion-text) (5 × 2)
- [SDMF_AKTION_TEXT](#table-sdmf-aktion-text) (3 × 2)
- [KALIB_SERVICE_TEXT](#table-kalib-service-text) (5 × 2)
- [TEST_FUNKTIONAL_TLC_TEXT](#table-test-funktional-tlc-text) (3 × 2)
- [SLI_METHODE_TEXT](#table-sli-methode-text) (5 × 2)
- [PIXEL_TEXT](#table-pixel-text) (2 × 2)
- [DEGREE_TEXT](#table-degree-text) (2 × 2)
- [KAM_HOHE_TEXT](#table-kam-hohe-text) (2 × 2)
- [SUPLEMENTAL_TEXT](#table-suplemental-text) (6 × 2)
- [FLA_FERNLICHT_SCHALTEN_TEXT](#table-fla-fernlicht-schalten-text) (5 × 2)
- [HW_REVISION_TAB](#table-hw-revision-tab) (10 × 2)

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

Dimensions: 118 rows × 2 columns

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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 125 rows × 3 columns

| ORT | ORTTEXT | LIN_2_FORMAT |
| --- | --- | --- |
| 0x0100 | Batteriesensor BSD | - |
| 0x0150 | Ölqualitätsensor BSD | - |
| 0x0200 | Elektrische Wasserpumpe BSD | - |
| 0x0250 | Elektrische Kraftstoffpumpe BSD | - |
| 0x0300 | Generator 1 | - |
| 0x0350 | Generator 2 | - |
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
| 0x1000 | Topview Kamera Außenspiegel links | 1 |
| 0x1100 | Topview Kamera Außenspiegel rechts | 1 |
| 0x1200 | Sideview Kamera Stoßfänger vorne links | 1 |
| 0x1300 | Sideview Kamera Stoßfänger vorne rechts | 1 |
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
| 0x3E00 | PCU(DCDC) | 1 |
| 0x3F00 | Startergenerator | 1 |
| 0x3F80 | Generator | 1 |
| 0x4000 | Sitzverstellschalter Fahrer | 1 |
| 0x4100 | Sitzverstellschalter Beifahrer | 1 |
| 0x4200 | Sitzverstellschalter Fahrer hinten | 1 |
| 0x4300 | Sitzverstellschalter Beifahrer hinten | 1 |
| 0x4400 | Gepäckraumschalter links | 1 |
| 0x4500 | Gepäckraumschalter rechts | 1 |
| 0x4A00 | Fond-Klimaanlage | 1 |
| 0x4B00 | Elektrischer Klimakompressor | 1 |
| 0x4C00 | Klimabedienteil | 1 |
| 0x4D00 | Gebläseregler | 1 |
| 0x4E00 | Klappenmotor | 0 |
| 0x4F00 | Elektrischer Kältemittelverdichter eKMV | 1 |
| 0x4F80 | Elektrischer Zuheizer PTC | 1 |
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
| 0x5780 | Fussgängerschutz Sensorband | 0 |
| 0x5788 | Satellit C-Säule links Y | 0 |
| 0x5790 | Satellit C-Säule rechts Y | 0 |
| 0x5798 | Satellit Zentrale Körperschall | 0 |
| 0x57A0 | Kapazitive Insassen- Sensorik CIS | 1 |
| 0x57A8 | Sitzbelegungserkennung Beifahrer SBR | 1 |
| 0x5800 | HUD | 1 |
| 0x5900 | Audio-Bedienteil | 1 |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 5 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| 2 | D-CAN |
| 1 | BMW-FAST |
| 3 | KWP2000* |
| 4 | KWP2000 |
| 5 | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 50 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA928 | Kamera Strommessung ausserhalb Bereich |
| 0xA929 | Kamera Spannungsmessung ausserhalb Bereich |
| 0xA92B | Steuergeraet: Interner Fehler |
| 0xA92C | Kamera EEPROM Kommunikationsfehler |
| 0xA92D | Kamera: nicht kalibriert |
| 0xA92F | Aktuator Lenkrad defekt |
| 0xA931 | Kamera Empfindlichkeitsänderung |
| 0xA932 | CAM: SPC failed |
| 0xA933 | ECU: VIN_INCORRECT |
| 0xA934 | Steuergerät Checksummenfehler |
| 0xA936 | Steuergeraet: Klemmenspannung ausserhalb Bereich |
| 0xA937 | Kamera: Gierwinkel ausserhalb Bereich |
| 0xA938 | Kamera: Nickwinkel ausserhalb Bereich |
| 0xA939 | Kamera: Rollwinkel ausserhalb Bereich |
| 0xA93A | Steuergeraet: Interne Spannungen ausserhalb Bereich |
| 0xA93B | Kamera: Imager Defekt |
| 0xA93C | LVDS Kommunikationsfehler |
| 0xA93D | Kamera EEPROM Checksummenfehler |
| 0xA93E | Energiesparmode aktiv |
| 0xE047 | PT-CAN BUS OFF |
| 0xE054 | Nachrichtenfehler(130h, Klemmenstatus) |
| 0xE055 | Nachrichtenfehler(19Eh, Status DSC)) |
| 0xE056 | Nachrichtenfehler(1A0h, Geschwindigkeit) |
| 0xE057 | Nachrichtenfehler(1B4h, Status Kombi) |
| 0xE058 | Nachrichtenfehler(1D6h, Bedienung Taster Audio/Telefon) |
| 0xE059 | Nachrichtenfehler(1EEh, Bedienung Lenkstock) |
| 0xE05A | Nachrichtenfehler(1F6h, Blinken) |
| 0xE05B | Nachrichtenfehler (C8h, Lenkradwinkel oben) |
| 0xE05C | Nachrichtenfehler(21Ah, Lampenzustand) |
| 0xE05D | Nachrichtenfehler(226h, Regensensor Wischergeschwindigkeit) |
| 0xE05E | Nachrichtenfehler(252h, Wischerstatus) |
| 0xE05F | Nachrichtenfehler(278h, Navigationsgraph) |
| 0xE060 | Nachrichtenfehler(27Ah, Synchronisation Navigationsgraph) |
| 0xE061 | Nachrichtenfehler(2A6h, Bedienung Wischertaster) |
| 0xE062 | Nachrichtenfehler(2E4h, Status Anhaenger) |
| 0xE063 | Nachrichtenfehler(2F8h, Uhrzeit / Datum) |
| 0xE064 | Nachrichtenfehler(310h, Aussentemperatur / Relativzeit) |
| 0xE065 | Nachrichtenfehler(314h, Status Fahrlicht) |
| 0xE066 | Nachrichtenfehler(330h, Kilometerstand / Reichweite) |
| 0xE067 | Nachrichtenfehler(347h, Status Koordination Vibration Lenkrad) |
| 0xE068 | Nachrichtenfehler(348h, Uebereinstimmung Navigationsgraph) |
| 0xE069 | Nachrichtenfehler(34Ch, Navigation GPS2) |
| 0xE06A | Nachrichtenfehler(34Eh, Navigation System Information) |
| 0xE06B | Nachrichtenfehler(380h, Fahrgestellnummer) |
| 0xE06C | Nachrichtenfehler(36Ah, Status Fernlicht Assistenz) |
| 0xE06D | Nachrichtenfehler(3B0h, Status Gang Rueckwaerts) |
| 0xE06E | Nachrichtenfehler(3CCh, Navigationsgraph Geschwindigkeit) |
| 0xE06F | Nachrichtenfehler(3F7h, Navigationsgraph Fahrspur) |
| 0xE070 | Nachrichtenfehler(2F7h, Einheiten) |
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
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 49 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xA928 | 2 | 3 | 4 | - |
| 0xA929 | 2 | 3 | 4 | - |
| 0xA92B | 2 | 3 | 4 | - |
| 0xA92C | 2 | 3 | 4 | - |
| 0xA92D | 2 | 3 | 4 | - |
| 0xA92F | 2 | 3 | 4 | - |
| 0xA931 | 2 | 3 | 4 | - |
| 0xA932 | 2 | 3 | 4 | - |
| 0xA933 | 2 | 3 | 4 | - |
| 0xA934 | 2 | 3 | 4 | - |
| 0xA936 | 2 | 3 | 4 | - |
| 0xA937 | 2 | 3 | 4 | - |
| 0xA938 | 2 | 3 | 4 | - |
| 0xA939 | 2 | 3 | 4 | - |
| 0xA93A | 2 | 3 | 4 | - |
| 0xA93B | 2 | 3 | 4 | - |
| 0xA93C | 2 | 3 | 4 | - |
| 0xA93D | 2 | 3 | 4 | - |
| 0xA93E | 2 | 3 | 4 | - |
| 0xE047 | 2 | 3 | 4 | - |
| 0xE054 | 2 | 3 | 4 | - |
| 0xE055 | 2 | 3 | 4 | - |
| 0xE056 | 2 | 3 | 4 | - |
| 0xE057 | 2 | 3 | 4 | - |
| 0xE058 | 2 | 3 | 4 | - |
| 0xE059 | 2 | 3 | 4 | - |
| 0xE05A | 2 | 3 | 4 | - |
| 0xE05B | 2 | 3 | 4 | - |
| 0xE05C | 2 | 3 | 4 | - |
| 0xE05D | 2 | 3 | 4 | - |
| 0xE05E | 2 | 3 | 4 | - |
| 0xE05F | 2 | 3 | 4 | - |
| 0xE060 | 2 | 3 | 4 | - |
| 0xE061 | 2 | 3 | 4 | - |
| 0xE062 | 2 | 3 | 4 | - |
| 0xE063 | 2 | 3 | 4 | - |
| 0xE064 | 2 | 3 | 4 | - |
| 0xE065 | 2 | 3 | 4 | - |
| 0xE066 | 2 | 3 | 4 | - |
| 0xE067 | 2 | 3 | 4 | - |
| 0xE068 | 2 | 3 | 4 | - |
| 0xE069 | 2 | 3 | 4 | - |
| 0xE06A | 2 | 3 | 4 | - |
| 0xE06B | 2 | 3 | 4 | - |
| 0xE06C | 2 | 3 | 4 | - |
| 0xE06D | 2 | 3 | 4 | - |
| 0xE06E | 2 | 3 | 4 | - |
| 0xE06F | 2 | 3 | 4 | - |
| 0xE070 | 2 | 3 | 4 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Kilometerstand | km | high | unsigned int | - | 1 | 1 | 0 |
| 2 | Relativzeit | s | high | signed long | - | 1 | 1 | 0 |
| 3 | Aussentemperatur | °C | high | signed char | - | 1 | 1 | 0 |
| 4 | Batteriespannung | V | high | unsigned int | - | 1 | 1000 | 0 |

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
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9340 | EyeQ: Interner Fehler |
| 0x9341 | EyeQ: Verlust der Kommunikation |
| 0x9342 | Kamerasensor ueberhitzt |
| 0x9343 | nvm_e_write_failed |
| 0x9344 | nvm_e_read_failed |
| 0x9345 | nvm_e_control_failed |
| 0x9346 | nvm_e_erase_failed |
| 0x9347 | nvm_e_write_all_failed |
| 0x9348 | nvm_e_read_all_failed |
| 0x9349 | nvm_e_wrong_config_id |
| 0x934A | CBT Failure |
| 0x934B | TLC Actuator ueberhitzt |
| 0x934C | Coding Failed |
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
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 13 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9340 | 2 | 3 | 4 | - |
| 0x9341 | 2 | 3 | 4 | - |
| 0x9342 | 2 | 3 | 4 | - |
| 0x9343 | 2 | 3 | 4 | - |
| 0x9344 | 2 | 3 | 4 | - |
| 0x9345 | 2 | 3 | 4 | - |
| 0x9346 | 2 | 3 | 4 | - |
| 0x9347 | 2 | 3 | 4 | - |
| 0x9348 | 2 | 3 | 4 | - |
| 0x9349 | 2 | 3 | 4 | - |
| 0x934A | 2 | 3 | 4 | - |
| 0x934B | 2 | 3 | 4 | - |
| 0x934C | 2 | 3 | 4 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Kilometerstand | km | high | unsigned int | - | 1 | 1 | 0 |
| 2 | Relativzeit | s | high | signed long | - | 1 | 1 | 0 |
| 3 | Aussentemperatur | °C | high | signed char | - | 1 | 1 | 0 |
| 4 | Batteriespannung | V | high | unsigned int | - | 1 | 1000 | 0 |

<a id="table-tac-text"></a>
### TAC_TEXT

Dimensions: 11 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | TAC in progress |
| 0x01 | Calibration successfully completed |
| 0x02 | Success -&gt; continue calibration |
| 0x03 | Insufficient image quality |
| 0x04 | No target located |
| 0x05 | Targets out of range |
| 0x06 | Inconsistency between left and right target (for instance wrong pitch angle) |
| 0x07 | TAC parameters out of range |
| 0x08 | Calibration values out of range (Note: limits are codable in EEPROM) |
| 0x09 | TAC undefined error |
| 0xXY | Invalid status received |

<a id="table-spannungen-text"></a>
### SPANNUNGEN_TEXT

Dimensions: 5 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x01 | Unterhalb Limit |
| 0x02 | Normal |
| 0x03 | Oberhalb Limit |
| 0xFF | Ungueltig |
| 0xXY | Invalid status received |

<a id="table-vorhanden-text"></a>
### VORHANDEN_TEXT

Dimensions: 3 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Nicht Vorhanden |
| 0x01 | Vorhanden |
| 0xXY | Invalid status received |

<a id="table-zeichen-nr-text"></a>
### ZEICHEN_NR_TEXT

Dimensions: 5 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Kein Zeichen erkannt |
| 0x01 | Beschraenkungszeichen |
| 0x02 | Aufhebungszeichen |
| 0xFF | Ungueltige Kamerainformation |
| 0xXY | Invalid status received |

<a id="table-geschwindigkeit-text"></a>
### GESCHWINDIGKEIT_TEXT

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Aufhebung alles |
| 0x01 | Erkannte Geschwindigkeit (Aufloesung 5km/h) |
| 0x02 | Ungueltig |
| 0xXY | Invalid status received |

<a id="table-guete-text"></a>
### GUETE_TEXT

Dimensions: 3 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Erkennungsqualitaet in Prozent |
| 0x01 | Ungueltig |
| 0xXY | Invalid status received |

<a id="table-beleuchtung-text"></a>
### BELEUCHTUNG_TEXT

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Keine ausreichende Beleuchtung erkannt |
| 0x01 | Ausreichende Beleuchtung erkannt |
| 0xFF | Ungueltig |
| 0xXY | Invalid status received |

<a id="table-v-fahrzeug-text"></a>
### V_FAHRZEUG_TEXT

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Kein vorausfahrendes Fahrzeug erkannt |
| 0x01 | Vorausfahrendes Fahrzeug erkannt |
| 0xFF | Ungueltig |
| 0xXY | Invalid status received |

<a id="table-e-fahrzeug-text"></a>
### E_FAHRZEUG_TEXT

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Kein entgegenkommendes Fahrzeug erkannt |
| 0x01 | Entgegenkommendes Fahrzeug erkannt |
| 0xFF | Ungueltig |
| 0xXY | Invalid status received |

<a id="table-fla-tagerkennung-text"></a>
### FLA_TAGERKENNUNG_TEXT

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Keine Helligkeit (Nacht) erkannt |
| 0x01 | Helligkeit (Nacht) erkannt |
| 0xFF | Ungueltig |
| 0xXY | Invalid status received |

<a id="table-fla-geschwindigkeit-text"></a>
### FLA_GESCHWINDIGKEIT_TEXT

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Geschwindigkeit über Limit |
| 0x01 | Geschwindigkeit unter Limit |
| 0xFF | Ungueltig |
| 0xXY | Invalid status received |

<a id="table-fla-verzoegerung-text"></a>
### FLA_VERZOEGERUNG_TEXT

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Keine Verzoegerung |
| 0x01 | Verzoegerung |
| 0xFF | Ungueltig |
| 0xXY | Invalid status received |

<a id="table-fla-sensortemperatur-text"></a>
### FLA_SENSORTEMPERATUR_TEXT

Dimensions: 3 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Temperatur außerhalb des Arbeitsbereiches |
| 0x01 | Temperatur zulässig |
| 0xXY | Invalid request |

<a id="table-fla-nebelerkennung-text"></a>
### FLA_NEBELERKENNUNG_TEXT

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Kein Nebel erkannt |
| 0x01 | Nebel erkannt |
| 0xFF | Ungueltig |
| 0xXY | Invalid status received |

<a id="table-verbindung-kam-nr-text"></a>
### VERBINDUNG_KAM_NR_TEXT

Dimensions: 8 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x01 | Information nicht verfügbar, Anfrage wiederholen |
| 0x02 | Kameraverbindung in Ordnung |
| 0x03 | Videoleitungen: |
| 0x04 | Dataleitungen: |
| 0x05 | LVDS Leitungs: |
| 0x06 | Versorgungsleitungen: |
| 0x07 | Fehler |
| 0xXY | Invalid status received |

<a id="table-kafas-init-text"></a>
### KAFAS_INIT_TEXT

Dimensions: 5 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | KAFAS nicht initialisiert |
| 0x01 | KAFAS initialisiert |
| 0x02 | Information noch nicht verfuegbar |
| 0xFF | KAFAS Initialisierung fehlerhaft |
| 0xXY | Invalid status received |

<a id="table-vin-status-text"></a>
### VIN_STATUS_TEXT

Dimensions: 4 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Keine Uebereinstimmung |
| 0x01 | Uebereinstimmung |
| 0x02 | Kein Zugriff auf VINs, Anfrage wiederholen |
| 0xXY | Invalid status received |

<a id="table-spannung-strom-kam-text"></a>
### SPANNUNG_STROM_KAM_TEXT

Dimensions: 5 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x01 | Unterhalb des Limits |
| 0x02 | Normal |
| 0x03 | Oberhalb des Limits |
| 0xFF | Ungueltig |
| 0xXY | Invalid status received |

<a id="table-sak-aktion-text"></a>
### SAK_AKTION_TEXT

Dimensions: 10 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Alle Anzeigen im Kombi ausgeschaltet |
| 0x01 | Set ST_TLC aktiv |
| 0x02 | Balken rechts anzeigen |
| 0x04 | Balken links anzeigen |
| 0x07 | Balken rechts und links anzeigen |
| 0x08 | Aktivierungsanzeige = Verfügbarkeitsschwelle anzeigen |
| 0x10 | Verfügbarkeit rechts |
| 0x20 | Verfügbarkeit links |
| 0xFF | Ungueltig |
| 0xXY | Invalid request |

<a id="table-sbn-aktion-text"></a>
### SBN_AKTION_TEXT

Dimensions: 5 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |
| 0x02 | Keine Empfehlung |
| 0x03 | Zurück zum Normalmodus |
| 0xXY | Invalid request |

<a id="table-sdmf-aktion-text"></a>
### SDMF_AKTION_TEXT

Dimensions: 3 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Demo-Mode Ausschalten |
| 0x01 | Demo-Mode Einschalten |
| 0xXY | Invalid request |

<a id="table-kalib-service-text"></a>
### KALIB_SERVICE_TEXT

Dimensions: 5 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Blockagetest nicht gestartet, SPC nicht gestartet |
| 0x01 | Blockagetest aktiv, SPC nicht gestartet |
| 0x02 | Blockagetest erfolgreich beendet, SPC aktiv |
| 0x03 | Blockagetest erfolgreich beendet, SPC erfolgreich abgeschlossen |
| 0xXY | Invalid status received |

<a id="table-test-funktional-tlc-text"></a>
### TEST_FUNKTIONAL_TLC_TEXT

Dimensions: 3 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Service not running (yaw and speed values from vehicle CAN) |
| 0x01 | Service running (yaw and speed values from diagnostic job) |
| 0xXY | Invalid status received |

<a id="table-sli-methode-text"></a>
### SLI_METHODE_TEXT

Dimensions: 5 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Activate camera-based recognition only |
| 0x01 | Activate map-based recognition only |
| 0x02 | Activate consolidated recognition |
| 0xFF | Reset to standard configuration coded in EEPROM |
| 0xXY | Invalid request |

<a id="table-pixel-text"></a>
### PIXEL_TEXT

Dimensions: 2 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0xFFFF | Invalid value |
| 0xXY | Pixel |

<a id="table-degree-text"></a>
### DEGREE_TEXT

Dimensions: 2 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0xFFFF | Invalid value |
| 0xXY | 0.01 * degree |

<a id="table-kam-hohe-text"></a>
### KAM_HOHE_TEXT

Dimensions: 2 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0xFFFF | Invalid value |
| 0xXY | mm, Height of camera above ground |

<a id="table-suplemental-text"></a>
### SUPLEMENTAL_TEXT

Dimensions: 6 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Km/h |
| 0x01 | % (percent) |
| 0x02 | 1V resolution |
| 0x03 | 1mV resolution |
| 0x04 | 1mA resolution |
| 0xXY | Invalid entry |

<a id="table-fla-fernlicht-schalten-text"></a>
### FLA_FERNLICHT_SCHALTEN_TEXT

Dimensions: 5 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x00 | Keine Empfehlung (Defekt erkannt, Sichtfeld verdreckt) |
| 0x01 | Fernlicht AUS |
| 0x02 | Fernlicht EIN |
| 0xFF | Ungueltig |
| 0xXY | Invalid request |

<a id="table-hw-revision-tab"></a>
### HW_REVISION_TAB

Dimensions: 10 rows × 2 columns

| WERT | DESCRIPTION |
| --- | --- |
| 0x02 | B2 |
| 0x78 | B2_1 |
| 0xC9 | C0 Labor V02 |
| 0xCA | C0 BMW V01 |
| 0xD3 | C0 BMW V02 |
| 0xD4 | C1 BMW V02 |
| 0xD6 | C2 BMW V01 |
| 0xD7 | C3 BMW V01 |
| 0xD8 | C4 BMW V01 |
| 0xXY | Undefined Revision |
