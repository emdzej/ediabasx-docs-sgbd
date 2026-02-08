# CCCA60.prg

- Jobs: [94](#jobs)
- Tables: [38](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | CCC Application |
| ORIGIN | BMW EE-40 Dieter Vollmerhaus |
| REVISION | 4.020 |
| AUTHOR | BMW EE-40 Dieter Vollmerhaus, Siemens-VDO HEM-SWF Joerg Keller |
| COMMENT | N/A |
| PACKAGE | 1.24 |
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
- [SELBSTTEST_STARTEN](#job-selbsttest-starten) - Starten des Selbsttests KWP2000: $31 StartRoutineByLocalIdentifier $04 Selftest
- [SELBSTTEST_STOPPEN](#job-selbsttest-stoppen) - Abbrechen des Selbsttests KWP2000: $32 StopRoutineByLocalIdentifier $04 Selftest
- [SELBSTTEST_ABFRAGEN](#job-selbsttest-abfragen) - Abfragen des Systemtests KWP2000: $33 RequestRoutineResultsByLocalIdentifier $04 Selftest
- [SYSTEMTEST_STARTEN](#job-systemtest-starten) - Starten des Systemtests KWP2000: $31 StartRoutineByLocalIdentifier $FA OEM-spezifisch: Systemtest
- [SYSTEMTEST_STOPPEN](#job-systemtest-stoppen) - Abbrechen des Systemtests KWP2000: $32 StopRoutineByLocalIdentifier $FA OEM-spezifisch: Systemtest
- [SYSTEMTEST_ABFRAGEN](#job-systemtest-abfragen) - Abfragen des Systemtests KWP2000: $33 RequestRoutineResultsByLocalIdentifier $FA OEM-spezifisch: Systemtest
- [READ_CURRENT_UIF](#job-read-current-uif) - currentUIFDataTable KWP2000: $1A ReadECUIdentification Modus  : Default
- [READ_BMW_SACH_NR](#job-read-bmw-sach-nr) - SystemSupplierECUHardwareNumber KWP2000: $1A ReadECUIdentification Modus  : Default
- [READ_BMW_HW_VERSION](#job-read-bmw-hw-version) - vehicleManufactureECUHardwareVersionNumber KWP2000: $1A ReadECUIdentification Modus  : Default
- [PROGRAM_REFERENZ_LESEN](#job-program-referenz-lesen) - vehicleManufECUSoftwareLayerVersionNumber KWP2000: $1A ReadECUIdentification Modus  : Default
- [REQUEST_REMOTE_DATA_SOURCES](#job-request-remote-data-sources) - Anstossen der Programmiereung mit Daten von externer Datenquelle und Abfragen des Status Extended Flashjob KWP2000: $40 Modus  : Default
- [REQUEST_REMOTE_DOWNLOAD](#job-request-remote-download) - start der Programmierung mit Daten von externer Datenquelle und Abfragen des Status Extended Flashjob KWP2000: $41 Modus  : Default
- [REMOTE_TRANSFER_DATA](#job-remote-transfer-data) - start der Programmierung mit Daten von externer Datenquelle und Abfragen des Status Extended Flashjob KWP2000: $42 Modus  : Default
- [REQUEST_REMOTE_TRANSFER_EXIT](#job-request-remote-transfer-exit) - Beendigung oder Abbruch der Remote Programmierung Extended Flashjob KWP2000: $43 Modus  : Default
- [SET_ENDE_CODIERUNG](#job-set-ende-codierung) - Codierdaten flashen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
- [SCHREIBEN_TELEFONNUMMER_SDARS](#job-schreiben-telefonnummer-sdars) - Schreiben der Telefonnummer für SDARS KWP2000: $3B writeDataByLocalIdentifier $A3 recordLocalIdentifier Modus  : Default
- [LESEN_TELEFONNUMMER_SDARS](#job-lesen-telefonnummer-sdars) - Auslesen der im CCC gespeicherten Telefonnummer für - SDARS KWP2000: $21 readDataByLocalIdentifier $A3 recordLocalIdentifier Modus  : Default
- [LESEN_TELEFONNUMMERN](#job-lesen-telefonnummern) - Auslesen der im CCC gespeicherten Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline KWP2000: $21 readDataByLocalIdentifier $A2 recordLocalIdentifier Modus  : Default
- [SCHREIBEN_TELEFONNUMMERN](#job-schreiben-telefonnummern) - Schreiben der Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline KWP2000: $3B writeDataByLocalIdentifier $A2 recordLocalIdentifier Modus  : Default
- [STATUS_HIP_SW_VERSION](#job-status-hip-sw-version) - Aktuelle HIP SW-Version wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_HIP_HW_VERSION](#job-status-hip-hw-version) - Aktuelle HIP HW-Version wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_GPS_TRACKING](#job-status-gps-tracking) - Status des GPS wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_GPS_ANTENNA](#job-status-gps-antenna) - Status der GPS Antenne wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_GPS_POSITION](#job-status-gps-position) - GPS Position wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_DR_POSITION](#job-status-dr-position) - GPS Position abgeglichen mit speed, gyro wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_GPS_DOP](#job-status-gps-dop) - GPS Auflösung wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_GPS_TIME](#job-status-gps-time) - GPS Datum und Uhrzeit wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_GPS_SATINFO](#job-status-gps-satinfo) - GPS SatInfo wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_DIR_SWITCH](#job-status-dir-switch) - Status der Gangwahl wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_TACHOPULSE](#job-status-tachopulse) - Status der Tachopulse wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_GYRO](#job-status-gyro) - Status der GYRO-Spannung wird ausgegeben (wird ab NAVI01-SW 6.3.0 unterstützt) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_HIP_SW_LOADING](#job-status-hip-sw-loading) - Der aktuelle HIP SWL-Status wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [START_HIP_SW_LOADING](#job-start-hip-sw-loading) - HIP Software Laden wird gestartet KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_AUDIO](#job-status-audio) - Detektiert den Status der Audio-Applikation KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_MIXER](#job-status-mixer) - Gibt die aktive Audio Ausgabe Einheit an KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_AKTIVE_APPLIKATION](#job-status-aktive-applikation) - Liefert den Namen der zur Zeit aktiven Applikation KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STEUERN_START_TUNER](#job-steuern-start-tuner) - ? KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
- [STATUS_SPEECH_RECOG](#job-status-speech-recog) - Status der Spracherkennung KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_AUDIO_MGR](#job-status-audio-mgr) - Status des universellen Sprachausgabe Managers KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_LAST_CONNECTION](#job-status-last-connection) - URL der letzen Verbindung wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STEUERN_TESTBILD_FARBFLAECHE](#job-steuern-testbild-farbflaeche) - ? KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
- [STEUERN_TESTBILD_SPEZIAL](#job-steuern-testbild-spezial) - ? KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
- [STATUS_LESEN_SYSTEM_AUDIO](#job-status-lesen-system-audio) - Auslesen des codierten Audio-Systems KWP2000: $22 ReadDataByCommonIdentifier
- [STEUERN_INTERNAL_RESET](#job-steuern-internal-reset) - Seuergeraete reset ausloesen KWP2000: $11 ECUReset $FA RequestInternalReset Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig 
- [STEUERN_VOLUMEAUDIO](#job-steuern-volumeaudio) - Einstellen der Audio-Lautstaerke KWP2000: $22 WriteDataByCommonIdentifier - set volume Modus  : Default
- [STEUERN_NEXT_ENTSOURCE](#job-steuern-next-entsource) - Weiterschaltung der Entertainment-Quelle per Diagnose KWP2000: $22 WriteDataByCommonIdentifier - set volume $F902 set naechste Entertainment Quelle

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

_No arguments._

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

<a id="job-selbsttest-starten"></a>
### SELBSTTEST_STARTEN

Starten des Selbsttests KWP2000: $31 StartRoutineByLocalIdentifier $04 Selftest

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEST_NR | int | gewaehltes Testscript 0 - standard tests, &gt; 0 nur für Entwicklung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-selbsttest-stoppen"></a>
### SELBSTTEST_STOPPEN

Abbrechen des Selbsttests KWP2000: $32 StopRoutineByLocalIdentifier $04 Selftest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-selbsttest-abfragen"></a>
### SELBSTTEST_ABFRAGEN

Abfragen des Systemtests KWP2000: $33 RequestRoutineResultsByLocalIdentifier $04 Selftest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_TESTERG_NR | unsigned int | Status des Tests 0x00: 	Test nicht gestartet 0x01: 	Test laeuft 0x7F: 	Test abgebrochen 0x81: 	Test beendet mit Fehler 0xFF: 	Test beendet ohne Fehler |
| ID_TESTERG_TEXT | string | Teststatus-Text table Testergebnisse TESTERG_TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-systemtest-starten"></a>
### SYSTEMTEST_STARTEN

Starten des Systemtests KWP2000: $31 StartRoutineByLocalIdentifier $FA OEM-spezifisch: Systemtest

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEST_NR | unsigned int | gewaehltes Testscript 0 - standard tests, &gt; 0 nur für Entwicklung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-systemtest-stoppen"></a>
### SYSTEMTEST_STOPPEN

Abbrechen des Systemtests KWP2000: $32 StopRoutineByLocalIdentifier $FA OEM-spezifisch: Systemtest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-systemtest-abfragen"></a>
### SYSTEMTEST_ABFRAGEN

Abfragen des Systemtests KWP2000: $33 RequestRoutineResultsByLocalIdentifier $FA OEM-spezifisch: Systemtest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_TESTERG_NR | unsigned int | Status des Tests 0x00: 	Test nicht gestartet 0x01: 	Test laeuft 0x7F: 	Test abgebrochen 0x81: 	Test beendet mit Fehler 0xFF: 	Test beendet ohne Fehler |
| ID_TESTERG_TEXT | string | Teststatus-Text table Testergebnisse TESTERG_TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-current-uif"></a>
### READ_CURRENT_UIF

currentUIFDataTable KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| UIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| UIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| UIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| UIF_OFFSET | int | Anzahl Programmiervorgaenge |
| UIF_GROESSE | int | Groesse des UIF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-bmw-sach-nr"></a>
### READ_BMW_SACH_NR

SystemSupplierECUHardwareNumber KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_HW_NR | string | BMW-Hardwarenummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-bmw-hw-version"></a>
### READ_BMW_HW_VERSION

vehicleManufactureECUHardwareVersionNumber KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_HW_NR | string | BMW-HardwareVersion |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-program-referenz-lesen"></a>
### PROGRAM_REFERENZ_LESEN

vehicleManufECUSoftwareLayerVersionNumber KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PROGRAMM_REFERENZ | string | PRGREF ProgrammReferenz letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-request-remote-data-sources"></a>
### REQUEST_REMOTE_DATA_SOURCES

Anstossen der Programmiereung mit Daten von externer Datenquelle und Abfragen des Status Extended Flashjob KWP2000: $40 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_MEDIUM | string | Daten medium "CD-ROM", "DVD-ROM", "IP-SERVER" |
| DATA_LABEL | string | Label des Datenmediums |
| DATEI_NAME | string | Name der Datenquelle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MEDIUM_STATUS | string | JA / NEIN |
| DATEI_STATUS | string | JA / NEIN 0x07 - alles OK |
| RESULT | unsigned char | result value 0x0F - alles OK |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-request-remote-download"></a>
### REQUEST_REMOTE_DOWNLOAD

start der Programmierung mit Daten von externer Datenquelle und Abfragen des Status Extended Flashjob KWP2000: $41 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | string | table SpeicherSegment SEG_NAME SEG_TEXT |
| DATEN_KOMPRESSION | unsigned char | Kennung fuer Datenkompression ung Verschluesselung |
| DATEN_MEDIUM | string | Daten medium "CD-ROM", "DVD-ROM", "IP-SERVER" |
| DATA_LABEL | string | Label des Datenmediums |
| DATEI_NAME | string | Erreichter Prozentsatz der Programmierung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MEDIUM_STATUS | string | JA / NEIN |
| DATEI_STATUS | string | JA / NEIN 0x07 - alles OK |
| RESULT | unsigned char | result value 0x0F - alles OK |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-remote-transfer-data"></a>
### REMOTE_TRANSFER_DATA

start der Programmierung mit Daten von externer Datenquelle und Abfragen des Status Extended Flashjob KWP2000: $42 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NUM_PROG_AKTIVE | unsigned char | Anzahl der zur Zeit aktiven Programmierprozesse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROGRAMMIER_STATUS | unsigned char | Prozentsatz der erreichten Programmierung |
| CD_STATUS | string | OK / not OK |
| SPEICHER_STATUS | string | OK / not OK |
| KOMMUNIKATIONS_STATUS | string | OK / not OK |
| RESULT | unsigned char | result value 0x0F - alles OK |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-request-remote-transfer-exit"></a>
### REQUEST_REMOTE_TRANSFER_EXIT

Beendigung oder Abbruch der Remote Programmierung Extended Flashjob KWP2000: $43 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DUMMY | string | wird eigentlich nichtbenoetigt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-ende-codierung"></a>
### SET_ENDE_CODIERUNG

Codierdaten flashen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-telefonnummer-sdars"></a>
### SCHREIBEN_TELEFONNUMMER_SDARS

Schreiben der Telefonnummer für SDARS KWP2000: $3B writeDataByLocalIdentifier $A3 recordLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NR_SDARS | string | Nummer des Bereitschaftsdienstes Stringlänge max. 35 Zeichen (ohne Endezeichen \0) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-telefonnummer-sdars"></a>
### LESEN_TELEFONNUMMER_SDARS

Auslesen der im CCC gespeicherten Telefonnummer für - SDARS KWP2000: $21 readDataByLocalIdentifier $A3 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| NR_SDARS | string | Nummer des Bereitschaftsdienstes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-telefonnummern"></a>
### LESEN_TELEFONNUMMERN

Auslesen der im CCC gespeicherten Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline KWP2000: $21 readDataByLocalIdentifier $A2 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| NR_BEREITSCHAFTSDIENST | string | Nummer des Bereitschaftsdienstes |
| NR_HEIMATHAENDLER | string | Nummer des Heimathändlers |
| NR_PASSO | string | Nummer Passo |
| NR_HOTLINE | string | Nummer der Hotline |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-telefonnummern"></a>
### SCHREIBEN_TELEFONNUMMERN

Schreiben der Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline KWP2000: $3B writeDataByLocalIdentifier $A2 recordLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NR_BEREITSCHAFTSDIENST | string | Nummer des Bereitschaftsdienstes Stringlänge max. 50 Zeichen + Stringende-Zeichen (\0) |
| NR_HEIMATHAENDLER | string | Nummer des Heimathändlers Stringlänge max. 50 Zeichen + Stringende-Zeichen (\0) |
| NR_PASSO | string | Nummer Passo Stringlänge max. 50 Zeichen + Stringende-Zeichen (\0) |
| NR_HOTLINE | string | Nummer der Hotline Stringlänge max. 50 Zeichen + Stringende-Zeichen (\0) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hip-sw-version"></a>
### STATUS_HIP_SW_VERSION

Aktuelle HIP SW-Version wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_HIP_SW_VERSION | string | HIP SW-version |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hip-hw-version"></a>
### STATUS_HIP_HW_VERSION

Aktuelle HIP HW-Version wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_HIP_HW_VERSION | string | HIP HW-version |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gps-tracking"></a>
### STATUS_GPS_TRACKING

Status des GPS wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_GPS_TEXT | string | GPS-status als Textausgabe table TrackingState ANZEIGE_TEXT |
| STAT_GPS | int | GPS status |
| STAT_ALMANACH_TEXT | string | ALMANACH-status als Textausgabe table AlmanachState ANZEIGE_TEXT |
| STAT_ALMANACH | int | GPS-status |

<a id="job-status-gps-antenna"></a>
### STATUS_GPS_ANTENNA

Status der GPS Antenne wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_ANTENNA | int | GPS-status als Nummer table GpsAntennaState WERT |
| STAT_ANTENNA_TEXT | string | GPS-status als Textausgabe table GpsAntennaState ANZEIGE_TEXT |

<a id="job-status-gps-position"></a>
### STATUS_GPS_POSITION

GPS Position wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_GPS_POSITION_BREITE | string | Es wird die aktuelle GPS Position Breite zurueckgeliefert |
| STAT_GPS_POSITION_LAENGE | string | Es wird die aktuelle GPS Position Laenge zurueckgeliefert |
| STAT_GPS_POSITION_HOEHE | string | Es wird die aktuelle GPS Position Hoehe zurueckgeliefert |

<a id="job-status-dr-position"></a>
### STATUS_DR_POSITION

GPS Position abgeglichen mit speed, gyro wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_POSITION | string | OK oder Ungueltig |
| STAT_GPS_POSITION_BREITE | string | Es wird die aktuelle GPS Position Breite zurückgeliefert |
| STAT_GPS_POSITION_LAENGE | string | Es wird die aktuelle GPS Position Laenge zurückgeliefert |
| STAT_GPS_POSITION_HOEHE | string | Es wird die aktuelle GPS Position Hoehe zurückgeliefert |
| STAT_SPEED | string | OK oder Ungueltig |
| STAT_SPEED_VAL | string | aktuelle Geschwindigkeit |
| STAT_HEADING | string | OK oder Ungueltig |
| STAT_HEADING_VAL | string | aktuelle Richtung |

<a id="job-status-gps-dop"></a>
### STATUS_GPS_DOP

GPS Auflösung wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_POSITION_AUFLOES | string | Positions Unsicherheit |
| STAT_HORIZONTALE_AUFLOES | string | Horizontale Unsicherheit |
| STAT_VERTICALE_AUFLOES | string | Vertikale Unsicherheit |

<a id="job-status-gps-time"></a>
### STATUS_GPS_TIME

GPS Datum und Uhrzeit wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_TIME_DATE_VAL | string | Datum und Uhrzeit |
| STAT_TIME | string | Gueltigkeit und Zeitbasis |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gps-satinfo"></a>
### STATUS_GPS_SATINFO

GPS SatInfo wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_VISI_SATS | int | Anzahl der sichtbaren Satelliten |
| STAT_TRACKED_SATS | int | Anzahl der verfolgbaren Satelliten |
| STAT_SAT_ID | int | ID des Satelliten |
| STAT_SIG_TO_NOISE | int | Signal Qualitaet des Satelliten |
| STAT_AZIMUTH | string | Azimuth des Satelliten |
| STAT_ELEVATION | string | Elevation des Satelliten |
| STAT_EPHEMERIS | string | Ephemeris des Satelliten |
| STAT_SATELLITE | string | Ephemeris des Satelliten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dir-switch"></a>
### STATUS_DIR_SWITCH

Status der Gangwahl wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_GANGWAHL_TEXT | string | Gangwahl-status als Textausgabe |
| STAT_GANGWAHL | int | Gangwahl-status als Nummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tachopulse"></a>
### STATUS_TACHOPULSE

Status der Tachopulse wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_TACHOPULSE | int | Tachopulse Hex-Zahl entspricht der Anzahl der Tachoimpulse |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gyro"></a>
### STATUS_GYRO

Status der GYRO-Spannung wird ausgegeben (wird ab NAVI01-SW 6.3.0 unterstützt) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIP_DRIVER_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP_DRIVER | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_GYRO_VOLTAGE_WERT | string | Es wird die aktuelle GYRO-Spannung zurückgeliefert |
| STAT_GYRO_TEXT | string | GYRO Status Es wird ein Text zu fehlerhaften Datenwerten angezeigt |
| STAT_GYRO_VOLTAGE_EINH | string | GYRO-Spannung Einheit: V |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hip-sw-loading"></a>
### STATUS_HIP_SW_LOADING

Der aktuelle HIP SWL-Status wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIP_TEXT | string | HIP-Treiber Status als Textausgabe table HipDriverStateTable ANZEIGE_TEXT |
| STAT_HIP | int | HIP-Treiber Status als Nummer table HipDriverStateTable WERT |
| STAT_SWL_HIP | int | HIP SW-Loading status |
| STAT_SWL_HIP_TEXT | string | table HipSwlTABLE ANZEIGE_TEXT HIP SW-Loading status |
| STAT_SWL_ERROR | string | HIP SW-Loading Error table HipSwlErrorTABLE ANZEIGE_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-hip-sw-loading"></a>
### START_HIP_SW_LOADING

HIP Software Laden wird gestartet KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HIP_SWL_SOURCE | string | Quelldatei inclusive Pfad Max. Laenge: 48 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-audio"></a>
### STATUS_AUDIO

Detektiert den Status der Audio-Applikation KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AUDIO | unsigned char | 1 wenn der Audio Service laeuft, sonst 0 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mixer"></a>
### STATUS_MIXER

Gibt die aktive Audio Ausgabe Einheit an KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MIXER | unsigned char | aktive Audio Ausgabe Einheit |
| STAT_MIXER_TEXT | string | aktive Audio Ausgabe Einheit Werte der Tabelle AudioSourceTable |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktive-applikation"></a>
### STATUS_AKTIVE_APPLIKATION

Liefert den Namen der zur Zeit aktiven Applikation KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AKTIVE_APPLIKATION | string | aktive Applikation |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-start-tuner"></a>
### STEUERN_START_TUNER

? KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-speech-recog"></a>
### STATUS_SPEECH_RECOG

Status der Spracherkennung KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPEECH_RECOG | unsigned char | 1: Spracherkennung laeuft, 0: Spracherkennung nicht aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-audio-mgr"></a>
### STATUS_AUDIO_MGR

Status des universellen Sprachausgabe Managers KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AUDIO_MGR | unsigned char | 1: Sprachausgabe ist aktiv, 0: Sprachausgabe ist nicht aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-last-connection"></a>
### STATUS_LAST_CONNECTION

URL der letzen Verbindung wird ausgegeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ONLINE_TEXT | string | Online Status als Textausgabe table OnlineStateTable ANZEIGE_TEXT |
| STAT_ONLINE | int | Online Status als Wert table OnlineStateTable WERT |
| STAT_CONNECTION_ATTEMPS | int | Anzahl der Verbindungsversuche |
| STAT_START_TIME_DATE | string | Start der Sitzung |
| STAT_END_TIME_DATE | string | Ende der Sitzung |
| STAT_BYTES_RECEIVED | long | Bytes received within last session (download) |
| STAT_BYTES_SENT | long | Bytes sent within last session (upload) |
| STAT_PHONE_NO | string | Telephone number of the RAS server |
| STAT_MODE | int | Digital, analogues or other dial-in |
| STAT_SIM_MNC | string | MNC (mobile network code) of SIM |
| STAT_SIM_MCC | string | MCC (mobile country code) of SIM |
| STAT_NET_MNC | string | MNC of net |
| STAT_NET_MCC | string | MCC of net |
| STAT_IP_NO | string | IP-number of the last connection. The IP-number will be provided by the PPP- RAS server |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-testbild-farbflaeche"></a>
### STEUERN_TESTBILD_FARBFLAECHE

? KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ROT_WERT | long | OKAY, wenn fehlerfrei |
| GRUEN_WERT | long | OKAY, wenn fehlerfrei |
| BLAU_WERT | long | OKAY, wenn fehlerfrei |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-testbild-spezial"></a>
### STEUERN_TESTBILD_SPEZIAL

? KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTBILD_ID | int | OKAY, wenn fehlerfrei |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-system-audio"></a>
### STATUS_LESEN_SYSTEM_AUDIO

Auslesen des codierten Audio-Systems KWP2000: $22 ReadDataByCommonIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AUDIO_SYSTEM | int | Codiertes Audio-System table AudioSystemTable WERT |
| STAT_AUDIO_SYSTEM_TEXT | string | Codiertes Audio-System table AudioSystemTable ANZEIGE_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-internal-reset"></a>
### STEUERN_INTERNAL_RESET

Seuergeraete reset ausloesen KWP2000: $11 ECUReset $FA RequestInternalReset Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-volumeaudio"></a>
### STEUERN_VOLUMEAUDIO

Einstellen der Audio-Lautstaerke KWP2000: $22 WriteDataByCommonIdentifier - set volume Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VOLUME | string | Ausgewaehlte Audio-Lautstaerke  table TAudioVolume WERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| LAUTSTAERKE | string | eingestellte Lautstaerke |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-next-entsource"></a>
### STEUERN_NEXT_ENTSOURCE

Weiterschaltung der Entertainment-Quelle per Diagnose KWP2000: $22 WriteDataByCommonIdentifier - set volume $F902 set naechste Entertainment Quelle

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ENTSOURCE | string | Einzustellende Entertainmentquelle table TEntSource TEXT Wenn weggelassen, dann weiterschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENTSOURCE | int | Neue Entertainmentquelle als Nummer table TEntSource MASKE |
| STAT_ENTSOURCE_TEXT | string | Neue Entertainmentquelle als Textausgabe table TEntSource TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (72 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (43 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (1 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (43 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (2 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (80 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (56 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (2 × 9)
- [IARTTEXTEERWEITERT](#table-iarttexteerweitert) (1 × 3)
- [TESTERGEBNISSE](#table-testergebnisse) (5 × 2)
- [PROTVERSIONTABLE](#table-protversiontable) (3 × 2)
- [HIPDRIVERSTATETABLE](#table-hipdriverstatetable) (3 × 2)
- [ONLINESTATETABLE](#table-onlinestatetable) (3 × 2)
- [HIPSWLERRORTABLE](#table-hipswlerrortable) (6 × 2)
- [HIPSWLTABLE](#table-hipswltable) (5 × 2)
- [HIPRESETTABLE](#table-hipresettable) (3 × 2)
- [TRACKINGSTATE](#table-trackingstate) (5 × 2)
- [ALMANACHSTATE](#table-almanachstate) (3 × 2)
- [GPSANTENNASTATE](#table-gpsantennastate) (4 × 2)
- [GANGWAHL](#table-gangwahl) (3 × 2)
- [AUDIOSYSTEMTABLE](#table-audiosystemtable) (4 × 2)
- [AUDIOSOURCETABLE](#table-audiosourcetable) (11 × 2)
- [TAUDIOVOLUME](#table-taudiovolume) (28 × 2)
- [TENTSOURCE](#table-tentsource) (16 × 2)

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

Dimensions: 72 rows × 2 columns

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

Dimensions: 43 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA048 | Kein Zusaetzliches Memory verfuegbar |
| 0xA04A | Root Zertifikat im Browser ist ungueltig |
| 0xA04B | Das angeforderte Security Level ist beim WAP Gateway nicht verfuegbar |
| 0xA04C | Das OU-Feld des geladenen WAP Zertifikat ist ungueltig |
| 0xA04D | Das aktuelle Netz wird nicht unterstuetzt |
| 0xA04E | Gyro Ausgaben ausserhalb der Spezifikation |
| 0xA04F | Kein Tacho Signal waehrend GPS Bewegung erkennt |
| 0xA050 | Zu grosse Tachodaten |
| 0xA051 | Rueckwertsgang Signal in Widerspruch zu GPS |
| 0xA052 | Grosse oder haeufige Positionsspruenge (obsolete) |
| 0xA053 | Oszillatorwerte ausserhalb Grosse der Spezifikation |
| 0xA054 | Offener GPS-Antennenanschluss |
| 0xA055 | Kurzschluss des GPS-Antennenanschluss |
| 0xA056 | Keine Verbindung zu GPS DSP |
| 0xA057 | RealTimeClock inkonsistent mit GPS-Zeit |
| 0xA058 | Gyro Fehler bei Selbsttest |
| 0xA059 | Gyro AD-Wandler Fehler bei Selbsttest |
| 0xA05A | Gyro gibt permanent 3.3 V |
| 0xA05B | Generischer Gyro Fehler |
| 0xA05C | Nicht spezifizierter Gyro Fehler |
| 0xA05D | Nicht spezifizierter Tacho Fehler |
| 0xA05E | Unbekanntes Soft Event |
| 0xA05F | Illegale hardware-Interrupts |
| 0xA060 | HIP: RAM-Fehler bei Selbsttest |
| 0xA061 | HIP: Checksum Fehler bei ROM test |
| 0xA062 | Keine UART-Verbindung zum HIP Modul |
| 0xA063 | HIP: interner SW-Fehler |
| 0xA064 | HIP: Fehler bei der Freigabe einer Semaphore |
| 0xA065 | HIP: Fehler beim Loeschen einer Message Queue |
| 0xA066 | HIP: Fehler beim Loeschen einer Task |
| 0xA067 | HIP: Fehler beim Suspendieren einer Task |
| 0xA6E8 | HIP: Fehler beim Resume einer Task |
| 0xA6E9 | HIP: Fehler beim Erstellen einer Semaphore |
| 0xA6EA | HIP: Fehler beim Verbinden zu einer IO-Zelle |
| 0xA6EB | HIP: Fehler beim Erstellen einer Task |
| 0xA6EC | HIP: Fehler beim Speicher allocieren |
| 0xA6ED | HIP: eine Message Queue ist voll |
| 0xA6EE | HIP: Fehler beim Oeffnen des seriellen Ports |
| 0xA6EF | HIP: COCOM event, kein recovery |
| 0xA6F0 | HIP: Fehler in Navigations library |
| 0xA6F1 | HIP: Serieller Port nicht gefunden |
| 0xA6F2 | HIP: Fehler beim Zugriff auf den seriellen Port |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 00000000 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 1 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxxx | 0 | - |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 43 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xA048 | 20 | 21 | - | - |
| 0xA04A | 20 | 21 | - | - |
| 0xA04B | 20 | 21 | - | - |
| 0xA04C | 20 | 21 | - | - |
| 0xA04D | 20 | 21 | - | - |
| 0xA04E | 20 | 21 | - | - |
| 0xA04F | 20 | 21 | - | - |
| 0xA050 | 20 | 21 | - | - |
| 0xA051 | 20 | 21 | - | - |
| 0xA052 | 20 | 21 | - | - |
| 0xA053 | 20 | 21 | - | - |
| 0xA054 | 20 | 21 | - | - |
| 0xA055 | 20 | 21 | - | - |
| 0xA056 | 20 | 21 | - | - |
| 0xA057 | 20 | 21 | - | - |
| 0xA058 | 20 | 21 | - | - |
| 0xA059 | 20 | 21 | - | - |
| 0xA05A | 20 | 21 | - | - |
| 0xA05B | 20 | 21 | - | - |
| 0xA05C | 20 | 21 | - | - |
| 0xA05D | 20 | 21 | - | - |
| 0xA05E | 20 | 21 | - | - |
| 0xA05F | 20 | 21 | - | - |
| 0xA060 | 20 | 21 | - | - |
| 0xA061 | 20 | 21 | - | - |
| 0xA062 | 20 | 21 | - | - |
| 0xA063 | 20 | 21 | - | - |
| 0xA064 | 20 | 21 | - | - |
| 0xA065 | 20 | 21 | - | - |
| 0xA066 | 20 | 21 | - | - |
| 0xA067 | 20 | 21 | - | - |
| 0xA6E8 | 20 | 21 | - | - |
| 0xA6E9 | 20 | 21 | - | - |
| 0xA6EA | 20 | 21 | - | - |
| 0xA6EB | 20 | 21 | - | - |
| 0xA6EC | 20 | 21 | - | - |
| 0xA6ED | 20 | 21 | - | - |
| 0xA6EE | 20 | 21 | - | - |
| 0xA6EF | 20 | 21 | - | - |
| 0xA6F0 | 20 | 21 | - | - |
| 0xA6F1 | 20 | 21 | - | - |
| 0xA6F2 | 20 | 21 | - | - |
| default | 20 | 21 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 2 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20 | VDO-Error | Hex | - | unsigned long | - | 1 | 1 | 0 |
| 21 | Datenlaenge | Hex | - | unsigned char | - | 1 | 1 | 0 |

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

Dimensions: 80 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9508 | Online: Browser kann nicht gestartet werden |
| 0x9509 | Online: Dateien koennen nicht geschrieben oder gelesen werden |
| 0x950A | Online: Initiale Timer koennen nicht gestartet werden |
| 0x950B | Online: Einwahl in RAS-Server konnte fehlgeschlagen |
| 0x950D | Online: Telefon nicht verfuegbar |
| 0x950E | Online: Kein zusaetzlicher Speicher verfuegbar |
| 0x9520 | Viva: Fehler in der Spracherkennungs-SW |
| 0x9521 | Viva: Audioverbindung konnte nicht aufgebaut werden |
| 0x9522 | Viva: MultiMedia Registry nicht verfuegbar |
| 0x9523 | Viva: Mikrophon Registry nicht verfuegbar |
| 0x9524 | Viva: Grammatik-Datei nicht verfuegbar |
| 0x9525 | Viva: nicht alle benoetigten Resourcen konnten allokiert werden |
| 0x9526 | Viva: SprachSynthesiser nicht verfuegbar |
| 0x9527 | Viva: Verbindung zum SprachSynthesiser nicht verfuegbar |
| 0x9528 | Viva: MPEG4 file player nicht verfuegbar |
| 0x9529 | Viva: Fehler bei der Spracherkennung |
| 0x952A | Viva: Fehler bei der Spracherzeugung |
| 0x952B | Viva: Fehler beim Erzeugen des SampleRate Converters |
| 0x952C | Viva: Fehler bei der Spracherverarbeitung |
| 0x952D | Viva: Fehler in der Synthesiser Engine |
| 0x952E | Viva: Fehler beim allocieren des Synthesisers |
| 0x952F | Viva: Fehler beim freigeben des Synthesisers |
| 0x9530 | Viva: Fehler mit Java MultiMedia Framework |
| 0x9531 | Viva: Fehler mit dem Sprach-Synthesiser |
| 0x9532 | Viva: Nativer MPEG4-Decoder kann nicht angesprochen werden |
| 0x9533 | Viva: Nativer MPEG4-Encoder kann nicht angesprochen werden |
| 0x9534 | Viva: Nativer MPEG4-AudioMultiplexer kann nicht angesprochen werden |
| 0x9535 | Viva: Nativer MPEG4-Coder kann keinen Speicher allocieren |
| 0x9536 | Viva: Nativer MPEG4-Coder hat Korrupte Eingabedaten empfangen |
| 0x9540 | Kein VoiceMemo service Recorder gefunden. |
| 0x9541 | Registry setting konnten nicht gelesen werden. |
| 0x9542 | Fehler 0x9542 |
| 0x9543 | Datenbank konnte nicht gespeichert werden |
| 0x9544 | Kein Speicher Service Verfuegbar |
| 0x9545 | Audio Manager Error |
| 0x9546 | Exception der AudioMgrFactory abgefangen |
| 0x9547 | Initialisierung des MPEG4-Encoders fehlgeschlagen |
| 0x9561 | SAM: Verbindung zur Sprachvorverarbeitung konnte nicht erstellt werden |
| 0x9562 | SAM: Generischer Dialog Manager konnte nicht geladen werden |
| 0x9563 | SAM: Das PrompterFile konnte nicht geleden werden |
| 0x9564 | SAM: keine Verbindung zum Adressbuch |
| 0x9565 | SAM: Verbindung zur Spracherkennung konnte nicht erstellt werden |
| 0x9566 | SAM: die Spracherkennung konnte nicht gestartet werden |
| 0x9567 | SAM: Verbindung zum SALSA Adressbuch konnte nicht erstellt werden |
| 0x9568 | SAM: Fehler Adressbuch Modul |
| 0x9569 | SAM: Daten koennen nicht im Flash gespeichert werden |
| 0x956A | SAM: Fehler in der Spracherkennung |
| 0x956B | SAM: Fehler im Prompter Modul |
| 0x956C | SAM: Fehler im Generischen Dialog Manager (GDM) |
| 0x956D | SAM: Der Sprach-Application Manager (SAM) konnte nicht gestartet werden |
| 0x956E | SAM: Der Sprachservice konnte nicht registriert werden |
| 0x956F | SAM: Verbindung zum MPEG4 Coder konnte nicht erstellt werden |
| 0x9570 | SAM: Fehler im der Texterkennung |
| 0x9580 | HIP: Beim Startup ungueliges BBRAM gefunden |
| 0x9581 | HIP: Checksum Fehler bei ROM test (obsolete) |
| 0x9582 | HIP: Fehler beim Senden einer Nachricht |
| 0x9583 | HIP: Fehler beim Empfang einer Nachricht |
| 0x9584 | HIP: unbekanntes Fatal Event Fehler empfangen |
| 0x9585 | HIP: unangeforderte Nachricht erhalten |
| 0x9586 | HIP: Programmier Fehler HIP-Treiber |
| 0x9587 | HIP: Grosse oder haeufige Positionsspruenge |
| 0x9588 | HIP: Ein Thread konte nicht gestartet werden |
| 0x9589 | Fehler 0x9589 |
| 0x958A | HIP Treiber: Fehler beim Zugriff auf den seriellen Port |
| 0x958B | HIP Treiber: Versuch zum Wiederaufbau der Verb. zu seriellem Port |
| 0x958C | HIP Treiber: Fehler beim Zugriff auf java Ptimer |
| 0x958D | HIP Treiber: Keine serielle Verbindung zu HIP-Modul |
| 0x958E | HIP Treiber: Interner Zustandswechsel |
| 0x958F | Fehler 0x958F |
| 0x9590 | HIP Treiber: Keine Antwort auf Anforderung zur Baudraten Reduzierung |
| 0x9591 | HIP Module antwortet nicht auf Statusanfrage |
| 0x9592 | HIP Module antwortet mit Fehler Code |
| 0x9593 | HIP Treiber: Weder ACK noch NACK als Antwort empfangen |
| 0x9594 | HIP Treiber: Unerwartete Antwort auf Status Anfrage: +toName(result) |
| 0x9595 | HIP Module Kommuniziert in keinem bekannten Protokoll |
| 0x9596 | Keine Verbindung zu HIP Module fuer mehr als 10 sec |
| 0x9597 | HardwareId des HIP Moduls hat unbekanntes Format |
| 0x9598 | Die neu installierte HIP-Firmware can nicht auf dem FileSystem geloescht werden |
| 0x9599 | HIP: Unbekanntes Event empfangen |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 00000000 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 56 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9508 | 20 | 21 | - | - |
| 0x9509 | 20 | 21 | - | - |
| 0x950A | 20 | 21 | - | - |
| 0x950B | 20 | 21 | - | - |
| 0x950D | 20 | 21 | - | - |
| 0x950E | 20 | 21 | - | - |
| 0x9520 | 20 | 21 | - | - |
| 0x9521 | 20 | 21 | - | - |
| 0x9522 | 20 | 21 | - | - |
| 0x9523 | 20 | 21 | - | - |
| 0x9524 | 20 | 21 | - | - |
| 0x9525 | 20 | 21 | - | - |
| 0x9526 | 20 | 21 | - | - |
| 0x9527 | 20 | 21 | - | - |
| 0x9528 | 20 | 21 | - | - |
| 0x9529 | 20 | 21 | - | - |
| 0x952A | 20 | 21 | - | - |
| 0x952B | 20 | 21 | - | - |
| 0x952C | 20 | 21 | - | - |
| 0x952D | 20 | 21 | - | - |
| 0x952E | 20 | 21 | - | - |
| 0x952F | 20 | 21 | - | - |
| 0x9540 | 20 | 21 | - | - |
| 0x9541 | 20 | 21 | - | - |
| 0x9542 | 20 | 21 | - | - |
| 0x9543 | 20 | 21 | - | - |
| 0x9544 | 20 | 21 | - | - |
| 0x9545 | 20 | 21 | - | - |
| 0x9546 | 20 | 21 | - | - |
| 0x9547 | 20 | 21 | - | - |
| 0x9580 | 20 | 21 | - | - |
| 0x9581 | 20 | 21 | - | - |
| 0x9582 | 20 | 21 | - | - |
| 0x9583 | 20 | 21 | - | - |
| 0x9584 | 20 | 21 | - | - |
| 0x9585 | 20 | 21 | - | - |
| 0x9586 | 20 | 21 | - | - |
| 0x9587 | 20 | 21 | - | - |
| 0x9588 | 20 | 21 | - | - |
| 0x9589 | 20 | 21 | - | - |
| 0x958A | 20 | 21 | - | - |
| 0x958B | 20 | 21 | - | - |
| 0x958C | 20 | 21 | - | - |
| 0x958D | 20 | 21 | - | - |
| 0x958E | 20 | 21 | - | - |
| 0x958F | 20 | 21 | - | - |
| 0x9590 | 20 | 21 | - | - |
| 0x9591 | 20 | 21 | - | - |
| 0x9592 | 20 | 21 | - | - |
| 0x9593 | 20 | 21 | - | - |
| 0x9594 | 20 | 21 | - | - |
| 0x9595 | 20 | 21 | - | - |
| 0x9596 | 20 | 21 | - | - |
| 0x9597 | 20 | 21 | - | - |
| 0x9598 | 20 | 21 | - | - |
| default | 20 | 21 | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 2 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20 | VDO-Error | Hex | - | unsigned long | - | 1 | 1 | 0 |
| 21 | Datenlaenge | Hex | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iarttexteerweitert"></a>
### IARTTEXTEERWEITERT

Dimensions: 1 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxxx | 0 | -- |

<a id="table-testergebnisse"></a>
### TESTERGEBNISSE

Dimensions: 5 rows × 2 columns

| TESTERG_NR | TESTERG_TEXT |
| --- | --- |
| 0x00 | Test nicht gestartet |
| 0x01 | Test läuft - Nummer  |
| 0x7F | Test abgebrochen |
| 0x81 | Test beendet mit Fehler  |
| 0xFF | Test beendet |

<a id="table-protversiontable"></a>
### PROTVERSIONTABLE

Dimensions: 3 rows × 2 columns

| WERT | PROT_VERSION |
| --- | --- |
| 0x00FA | Standard |
| 0x037A | XXL |
| 0xXY | unknown |

<a id="table-hipdriverstatetable"></a>
### HIPDRIVERSTATETABLE

Dimensions: 3 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | HIP-Treiber: OK |
| 0x01 | HIP-Treiber: Daten nicht abrufbar |
| 0xXY | nicht definiert |

<a id="table-onlinestatetable"></a>
### ONLINESTATETABLE

Dimensions: 3 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Online-Status OK |
| 0x01 | Daten nicht abrufbar |
| 0xXY | nicht definiert |

<a id="table-hipswlerrortable"></a>
### HIPSWLERRORTABLE

Dimensions: 6 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x04158010 | keine Verbindung zu HIP Modul |
| 0x0415801B | Die zu ladende Datei konnte nicht geoeffnet werden oder existiert nicht |
| 0x0415801C | Exception beim SWL aber kein Fehler gespeichert |
| 0x04158002 | Beim Laden der SW trat ein Fehler auf |
| 0x04158017 | Die Software ist nicht kompatibel zum HIP-Modul |
| 0xXY | nicht definiert |

<a id="table-hipswltable"></a>
### HIPSWLTABLE

Dimensions: 5 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | nicht aktiv |
| 0x01 | HIP SW-Laden laeuft |
| 0x02 | HIP SW-Laden erfolgreich beendet |
| 0x03 | HIP SW-Laden fehlgeschlagen |
| 0xXY | nicht definiert |

<a id="table-hipresettable"></a>
### HIPRESETTABLE

Dimensions: 3 rows × 2 columns

| WERT | RESET_MODE |
| --- | --- |
| 0x07 | ResetClear |
| 0x09 | ResetSave |
| 0xXY | nicht definiert |

<a id="table-trackingstate"></a>
### TRACKINGSTATE

Dimensions: 5 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Search the Sky |
| 0x01 | Tracking |
| 0x02 | 2D Positionierung |
| 0x03 | 3D Positionierung |
| 0xXY | nicht definiert |

<a id="table-almanachstate"></a>
### ALMANACHSTATE

Dimensions: 3 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Kein Almanach |
| 0x01 | Almanach OK |
| 0xXY | nicht definiert |

<a id="table-gpsantennastate"></a>
### GPSANTENNASTATE

Dimensions: 4 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Verbunden |
| 0x01 | Nicht verbunden |
| 0x02 | Kurzschluss |
| 0xXY | nicht definiert |

<a id="table-gangwahl"></a>
### GANGWAHL

Dimensions: 3 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Rueckwaertsgang |
| 0x01 | Vorwaertsgang oder Leerlauf |
| 0xXY | nicht definiert |

<a id="table-audiosystemtable"></a>
### AUDIOSYSTEMTABLE

Dimensions: 4 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | STEREO |
| 0x01 | HIFI |
| 0x02 | TOP-HIFI |
| 0xXY | nicht definiert |

<a id="table-audiosourcetable"></a>
### AUDIOSOURCETABLE

Dimensions: 11 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x03 | AUX |
| 0x04 | CDPlayer |
| 0x05 | CDC |
| 0x06 | Radio |
| 0x07 | MDPlayer |
| 0x08 | SDARS |
| 0x09 | TV |
| 0x0A | DVDPlayer |
| 0x0B | RadioTP |
| 0x0C | MP3 |
| 0xXY | nicht definiert |

<a id="table-taudiovolume"></a>
### TAUDIOVOLUME

Dimensions: 28 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Mute |
| 0x0F | Inkrement 15 |
| 0x10 | Inkrement 16 |
| 0x12 | Inkrement 18 |
| 0x14 | Inkrement 20 |
| 0x16 | Inkrement 22 |
| 0x18 | Inkrement 24 |
| 0x1A | Inkrement 26 |
| 0x1C | Inkrement 28 |
| 0x1E | Inkrement 30 |
| 0x20 | Inkrement 32 |
| 0x22 | Inkrement 34 |
| 0x24 | Inkrement 36 |
| 0x26 | Inkrement 38 |
| 0x28 | Inkrement 40 |
| 0x2A | Inkrement 42 |
| 0x2C | Inkrement 44 |
| 0x2E | Inkrement 46 |
| 0x30 | Inkrement 48 |
| 0x32 | Inkrement 50 |
| 0x34 | Inkrement 52 |
| 0x36 | Inkrement 54 |
| 0x38 | Inkrement 56 |
| 0x3A | Inkrement 58 |
| 0x3C | Inkrement 60 |
| 0x3E | Inkrement 62 |
| 0x3F | Maximal |
| 0xXY | Nicht definiert |

<a id="table-tentsource"></a>
### TENTSOURCE

Dimensions: 16 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | next |
| 0x01 | FM |
| 0x02 | AM |
| 0x03 | SCD |
| 0x04 | CDC |
| 0x05 | MD |
| 0x06 | WB |
| 0x07 | SDARS |
| 0x08 | IBOC |
| 0x09 | AUX |
| 0x0A | DVD |
| 0x0B | TV |
| 0x0C | VIDEOTXT |
| 0x0D | AV-AUX |
| 0x0E | DAB |
| 0xFF | Entertainmentsource not available |
