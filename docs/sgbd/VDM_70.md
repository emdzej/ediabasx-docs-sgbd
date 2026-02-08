# VDM_70.prg

- Jobs: [83](#jobs)
- Tables: [35](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Vertikal Dynamik Management |
| ORIGIN | BMW EF-63 Tobias Schmid |
| REVISION | 4.020 |
| AUTHOR | Conti-Temic CC-Elektronik Braun, Conti-Temic CC-Elektronik Schwarz, Conti-Temic CC-Elektronik Geweniger, Conti-Temic PC-FES Schuster |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
- [HS_LESEN_DETAIL](#job-hs-lesen-detail) - Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default
- [HS_LOESCHEN](#job-hs-loeschen) - Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
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
- [STATUS_VDM](#job-status-vdm) - Liest den aktuellen Status des VDM-SG's KWP 2000: $21 ReadDataByLocalIdentifier $23 Status VDM lesen
- [STATUS_PIA](#job-status-pia) - Liest die im VDM gespeicherten PIA-Daten aller Schlüssel KWP 2000: $21 ReadDataByLocalIdentifier $24 PIA-Daten auslesen
- [STEUERN_PIA](#job-steuern-pia) - Schreibt die Einstellungen für alle Schlüssel KWP 2000: $3B WriteDataByLocalIdentifier $24 PIA-Daten schreiben
- [STEUERN_PIA_KEY](#job-steuern-pia-key) - Schreibt die Einstellungen für einen Schlüssel KWP 2000: $3B WriteDataByLocalIdentifier $25 PIA-Daten schreiben
- [STATUS_ANALOG_EINGAENGE](#job-status-analog-eingaenge) - Lesen der Abgleichdaten für den Höhenstand KWP 2000: $21 ReadDataByLocalIdentifier $22 Analoge Eingaenge lesen
- [STEUERN_ABGLEICH_HOEHENSTAND](#job-steuern-abgleich-hoehenstand) - Schreiben der Abgleichdaten für den Höhenstand KWP 2000: $3B WriteDataByLocalIdentifier $21 HS-Abgleich
- [STATUS_ABGLEICH_HOEHENSTAND](#job-status-abgleich-hoehenstand) - Lesen der Abgleichdaten für den Höhenstand KWP 2000: $21 ReadDataByLocalIdentifier $21 HS-Abgleich
- [STATUS_FAHRZEUGHOEHE](#job-status-fahrzeughoehe) - Lesen der Abgleichdaten für den Höhenstand KWP 2000: $21 ReadDataByLocalIdentifier $21 HS-Abgleich
- [STATUS_BUS_DIAGNOSE_MODUL](#job-status-bus-diagnose-modul) - Liest die Bus-Diagnose-Daten des FlexRays KWP 2000: $21 ReadDataByLocalIdentifier $31 FR-Status auslesen
- [STEUERN_RESET_BUS_DIAGNOSE_MODUL](#job-steuern-reset-bus-diagnose-modul) - Setzt die Daten des FlexRay Busstatusmodul zurück KWP 2000: $3B ReadDataByLocalIdentifier $31 FR-Status schreiben
- [STATUS_WCET_LESEN](#job-status-wcet-lesen) - Liest die im VDM gespeicherten max. Laufzeiten aller Tasks KWP 2000: $21 ReadDataByLocalIdentifier $51 WCET auslesen
- [STEUERN_RESET_WCET](#job-steuern-reset-wcet) - Setzt die maximal erkannten Tasklaufzeiten zurück KWP 2000: $3B ReadDataByLocalIdentifier $51 WCET zurücksetzen
- [STATUS_COMPILER_BOOTLOADER](#job-status-compiler-bootloader) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des MPC-Bootloader KWP 2000: $21 ReadDataByLocalIdentifier $A0 status_compiler_bootloader
- [STATUS_COMPILER_APPLIKATION](#job-status-compiler-applikation) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der Applikation KWP 2000: $21 ReadDataByLocalIdentifier $A1 status_compiler_applikation
- [STATUS_COMPILER_DAF](#job-status-compiler-daf) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des DAF KWP 2000: $21 ReadDataByLocalIdentifier $A3 status_compiler_daf
- [_STATUS_READ_LL_ERROR](#job-status-read-ll-error) - Liest die momentanen Stati der LL-Fehlerpruefung KWP 2000: $21 ReadDataByLocalIdentifier $20 interne Fehlerstati lesen interner TEMIC-Job
- [_STEUERN_LENKWINKEL_RESET](#job-steuern-lenkwinkel-reset) - Setzt die Lernwerte für den Lenkwinkel zurück KWP 2000: $3B ReadDataByLocalIdentifier $40 Lenkwinkel zurücksetzen
- [_STATUS_TJA](#job-status-tja) - Liest die Busstatistik des FlexRays KWP 2000: $31 ReadDataByLocalIdentifier $AF TJA-Status auslesen
- [_STEUERN_ERROR_INJEKTION](#job-steuern-error-injektion) - Zur Vorgabe von Fehlern KWP2000: $3B WriteDataByLocalIdentifier $30 Fehlerinjektion interner TEMIC-Job Modus  : Default
- [_STATUS_ERRCODE](#job-status-errcode) - Gibt den Errorcode und die Umwelt- bedingungen eines kritischen Fehlers zurück KWP 2000: $21 ReadDataByLocalIdentifier $35 Errorcode auslesen
- [_STEUERN_RESET_ERRCODE](#job-steuern-reset-errcode) - Setzt den Errorcode und die Umweltbedingungen zurück KWP 2000: $3B ReadDataByLocalIdentifier $35 Errorcode und UBs schreiben
- [_STATUS_ANALOG_EINGAENGE](#job-status-analog-eingaenge) - Lesen der Abgleichdaten für den Höhenstand KWP 2000: $21 ReadDataByLocalIdentifier $22 Analoge Eingaenge lesen
- [_STEUERN_XCP_FR](#job-steuern-xcp-fr) - Freigabe oder Sperren der XCP-Schnittstelle über FlexRay KWP 2000: $3B WriteDataByLocalIdentifier $26 XCP freigeben/sperren
- [_STATUS_XCP_FR](#job-status-xcp-fr) - Liest den aktuellen Freigabestatus der XCP-Schnittstelle aus KWP 2000: $21 ReadDataByLocalIdentifier $26 Status XCP-Schnittstelle interner TEMIC-Job
- [_STATUS_TRACENUMMER](#job-status-tracenummer) - Liest die Temic Tracenummer KWP 2000: $21 ReadDataByLocalIdentifier $70 Temic Tracenummer lesen interner TEMIC-Job
- [_STATUS_AD_REF](#job-status-ad-ref) - Liest die AD-Referenzspannung zurück KWP 2000: $21 ReadDataByLocalIdentifier $72 Temic AD-Referenzspannung lesen interner TEMIC-Job
- [_STATUS_ENDTEST_INTERN](#job-status-endtest-intern) - Gibt den Status vom ROM-, RAM-, ALU- und ADC-Check sowie die Reset-Zeit bei einem vorangegangenen Watchdog-Fehler zurück KWP 2000: $21 ReadDataByLocalIdentifier $34 interner Status
- [_STATUS_ENDTEST_FR](#job-status-endtest-fr) - Gibt den Bus- und Nachrichtentransfer- Status auf dem FlexRay zurück Meßdauer 1 Sekunde KWP 2000: $21 ReadDataByLocalIdentifier $33 FR-Status auslesen
- [_STATUS_ENDTEST_ANALOGWERTE](#job-status-endtest-analogwerte) - Liest die Minimal- und Maximalwerte aller Analogeingänge über die Meßdauer von 1 Sekunde KWP 2000: $21 ReadDataByLocalIdentifier $32 analoge Min-/Maxwerte auslesen
- [_STEUERN_ENDTEST](#job-steuern-endtest) - Einstellungen für den Endtest KWP 2000: $3B ReadDataByLocalIdentifier $32 Einstellungen für den Endtest schreiben
- [_DUMMY](#job-dummy) - Zur Definition eines beliebigen Jobs Freie Auswahl eines Single Frames interner TEMIC-Job
- [_DUMMY_LONG](#job-dummy-long) - Zur Definition eines beliebigen Jobs interner TEMIC-Job

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

<a id="job-status-vdm"></a>
### STATUS_VDM

Liest den aktuellen Status des VDM-SG's KWP 2000: $21 ReadDataByLocalIdentifier $23 Status VDM lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODING_WERT | unsigned char | Status der Codierdaten |
| STAT_CODING_TEXT | string | Status der Codierdaten |
| STAT_CALIBRATION_WERT | unsigned char | Status des Höhenstandsabgleichs |
| STAT_CALIBRATION_TEXT | string | Status des Höhenstandsabgleichs |
| STAT_HSENSOR_FL_WERT | unsigned char | Status des Höhenstandssensor VL |
| STAT_HSENSOR_FL_TEXT | string | Status des Höhenstandssensor VL |
| STAT_SUPPLY_HSENSOR_FL_WERT | unsigned char | Status der Versorgungsspannung des Höhenstandssensor VL |
| STAT_SUPPLY_HSENSOR_FL_TEXT | string | Status der Versorgungsspannung des Höhenstandssensor VL |
| STAT_HSENSOR_FR_WERT | unsigned char | Status des Höhenstandssensor VR |
| STAT_HSENSOR_FR_TEXT | string | Status des Höhenstandssensor VR |
| STAT_SUPPLY_HSENSOR_FR_WERT | unsigned char | Status der Versorgungsspannung des Höhenstandssensor VR |
| STAT_SUPPLY_HSENSOR_FR_TEXT | string | Status der Versorgungsspannung des Höhenstandssensor VR |
| STAT_HSENSOR_RL_WERT | unsigned char | Status des Höhenstandssensor HL |
| STAT_HSENSOR_RL_TEXT | string | Status des Höhenstandssensor HL |
| STAT_SUPPLY_HSENSOR_RL_WERT | unsigned char | Status der Versorgungsspannung des Höhenstandssensor HL |
| STAT_SUPPLY_HSENSOR_RL_TEXT | string | Status der Versorgungsspannung des Höhenstandssensor HL |
| STAT_HSENSOR_RR_WERT | unsigned char | Status des Höhenstandssensor HR |
| STAT_HSENSOR_RR_TEXT | string | Status des Höhenstandssensor HR |
| STAT_SUPPLY_HSENSOR_RR_WERT | unsigned char | Status der Versorgungsspannung des Höhenstandssensor HR |
| STAT_SUPPLY_HSENSOR_RR_TEXT | string | Status der Versorgungsspannung des Höhenstandssensor HR |
| STAT_ECU_MODE_WERT | unsigned char | Status der Low-Level-Software |
| STAT_ECU_MODE_TEXT | string | Status der Low-Level-Software |
| STAT_KL30_WERT | unsigned char | Status der KL30-Spannung |
| STAT_KL30_TEXT | string | Status der KL30-Spannung |
| STAT_WAKE_WERT | unsigned char | Status der Weckleitung |
| STAT_WAKE_TEXT | string | Status der Weckleitung |
| STAT_PRG_CFSP_WERT | unsigned char | Status Dämpferprogramm |
| STAT_PRG_CFSP_TEXT | string | Status Dämpferprogramm |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pia"></a>
### STATUS_PIA

Liest die im VDM gespeicherten PIA-Daten aller Schlüssel KWP 2000: $21 ReadDataByLocalIdentifier $24 PIA-Daten auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEY_1_WERT | unsigned int | Einstellung Schlüssel 1 |
| STAT_KEY_1_TEXT | string | Einstellung Schlüssel 1 |
| STAT_KEY_2_WERT | unsigned int | Einstellung Schlüssel 2 |
| STAT_KEY_2_TEXT | string | Einstellung Schlüssel 2 |
| STAT_KEY_3_WERT | unsigned int | Einstellung Schlüssel 3 |
| STAT_KEY_3_TEXT | string | Einstellung Schlüssel 3 |
| STAT_KEY_4_WERT | unsigned int | Einstellung Schlüssel 4 |
| STAT_KEY_4_TEXT | string | Einstellung Schlüssel 4 |
| STAT_KEY_5_WERT | unsigned int | Einstellung Schlüssel 5 |
| STAT_KEY_5_TEXT | string | Einstellung Schlüssel 5 |
| STAT_LAST_FUNCTION_WERT | unsigned int | zuletzt verwendete Einstellung |
| STAT_LAST_FUNCTION_TEXT | string | zuletzt verwendete Einstellung |
| STAT_DEFAULT_WERT | unsigned int | Default-Einstellung |
| STAT_DEFAULT_TEXT | string | Default-Einstellung |
| STAT_UNPERSONALISED_WERT | unsigned int | Einstellung für Unpersonalisiert / Werkstattmode |
| STAT_UNPERSONALISED_TEXT | string | Einstellung für Unpersonalisiert / Werkstattmode |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pia"></a>
### STEUERN_PIA

Schreibt die Einstellungen für alle Schlüssel KWP 2000: $3B WriteDataByLocalIdentifier $24 PIA-Daten schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE_KEY_1 | unsigned int | Einstellung Schlüssel 1 0 -&gt; Komfort 1 -&gt; Sport 2 -&gt; Komfort mit Ersatzwerten 3 -&gt; Sport mit Ersatzwerten 4 -&gt; Festbestromung 5 -&gt; Nullbestromung |
| VALUE_KEY_2 | unsigned int | Einstellung Schlüssel 2 0 -&gt; Komfort 1 -&gt; Sport 2 -&gt; Komfort mit Ersatzwerten 3 -&gt; Sport mit Ersatzwerten 4 -&gt; Festbestromung 5 -&gt; Nullbestromung |
| VALUE_KEY_3 | unsigned int | Einstellung Schlüssel 3 0 -&gt; Komfort 1 -&gt; Sport 2 -&gt; Komfort mit Ersatzwerten 3 -&gt; Sport mit Ersatzwerten 4 -&gt; Festbestromung 5 -&gt; Nullbestromung |
| VALUE_KEY_4 | unsigned int | Einstellung Schlüssel 4 0 -&gt; Komfort 1 -&gt; Sport 2 -&gt; Komfort mit Ersatzwerten 3 -&gt; Sport mit Ersatzwerten 4 -&gt; Festbestromung 5 -&gt; Nullbestromung |
| VALUE_KEY_5 | unsigned int | Einstellung Schlüssel 5 0 -&gt; Komfort 1 -&gt; Sport 2 -&gt; Komfort mit Ersatzwerten 3 -&gt; Sport mit Ersatzwerten 4 -&gt; Festbestromung 5 -&gt; Nullbestromung |
| VALUE_LAST_FUNCTION | unsigned int | zuletzt verwendete Einstellung 0 -&gt; Komfort 1 -&gt; Sport 2 -&gt; Komfort mit Ersatzwerten 3 -&gt; Sport mit Ersatzwerten 4 -&gt; Festbestromung 5 -&gt; Nullbestromung |
| VALUE_DEFAULT | unsigned int | Default-Einstellung 0 -&gt; Komfort 1 -&gt; Sport 2 -&gt; Komfort mit Ersatzwerten 3 -&gt; Sport mit Ersatzwerten 4 -&gt; Festbestromung 5 -&gt; Nullbestromung |
| VALUE_UNPERSONALISED | unsigned int | Einstellung Unpersonalisert / Werkstattmode 0 -&gt; Komfort 1 -&gt; Sport 2 -&gt; Komfort mit Ersatzwerten 3 -&gt; Sport mit Ersatzwerten 4 -&gt; Festbestromung 5 -&gt; Nullbestromung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pia-key"></a>
### STEUERN_PIA_KEY

Schreibt die Einstellungen für einen Schlüssel KWP 2000: $3B WriteDataByLocalIdentifier $25 PIA-Daten schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NO_KEY | unsigned char | Nummer des Schlüssels, der gespeichert werden soll 0 -&gt; Schlüssel 1 1 -&gt; Schlüssel 2 2 -&gt; Schlüssel 3 3 -&gt; Schlüssel 4 4 -&gt; Schlüssel 5 5 -&gt; Default 6 -&gt; Default 7 -&gt; Default 8 -&gt; Default 9 -&gt; Default 10-&gt; Unpersonalisiert / Werkstattmode 11-&gt; Default 12-&gt; Default 13-&gt; Default 14-&gt; Default 15-&gt; Unpersonalisiert / Werkstattmode 16-&gt; Last Function |
| VALUE_KEY | unsigned int | Einstellung Schlüssel 1 0 -&gt; Komfort 1 -&gt; Sport 2 -&gt; Komfort mit Ersatzwerten 3 -&gt; Sport mit Ersatzwerten 4 -&gt; Festbestromung 5 -&gt; Nullbestromung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-eingaenge"></a>
### STATUS_ANALOG_EINGAENGE

Lesen der Abgleichdaten für den Höhenstand KWP 2000: $21 ReadDataByLocalIdentifier $22 Analoge Eingaenge lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_U_KL30_WERT | real | Spannung KL30 |
| STAT_U_KL30_EINH | string | Einheit Spannung KL30 (V) |
| STAT_U_KL30_FEHLER_WERT | unsigned char | Fehlerstatus der KL30 |
| STAT_U_KL30_FEHLER_TEXT | string | Fehlerstatus der KL30 |
| STAT_WECKLEITUNG | unsigned char | Status der Weckleitung |
| STAT_WECKLEITUNG_TEXT | string | Status der Weckleitung |
| STAT_U_HS_VL_WERT | real | Spannung des Höhenstandssensors VL |
| STAT_U_HS_VL_EINH | string | Einheit der Spannung des Höhenstandssensors VL |
| STAT_HS_VL_FEHLER_WERT | unsigned char | Fehlerstatus des Höhenstandssensors VL |
| STAT_HS_VL_FEHLER_TEXT | string | Fehlerstatus des Höhenstandssensors VL |
| STAT_U_HS_VR_WERT | real | Spannung des Höhenstandssensors VR |
| STAT_U_HS_VR_EINH | string | Einheit der Spannung des Höhenstandssensors VR |
| STAT_HS_VR_FEHLER_WERT | unsigned char | Fehlerstatus des Höhenstandssensors VR |
| STAT_HS_VR_FEHLER_TEXT | string | Fehlerstatus des Höhenstandssensors VR |
| STAT_U_HS_HL_WERT | real | Spannung des Höhenstandssensors HL |
| STAT_U_HS_HL_EINH | string | Einheit der Spannung des Höhenstandssensors HL |
| STAT_HS_HL_FEHLER_WERT | unsigned char | Fehlerstatus des Höhenstandssensors HL |
| STAT_HS_HL_FEHLER_TEXT | string | Fehlerstatus des Höhenstandssensors HL |
| STAT_U_HS_HR_WERT | real | Spannung des Höhenstandssensors HR |
| STAT_U_HS_HR_EINH | string | Einheit der Spannung des Höhenstandssensors HR |
| STAT_HS_HR_FEHLER_WERT | unsigned char | Fehlerstatus des Höhenstandssensors HR |
| STAT_HS_HR_FEHLER_TEXT | string | Fehlerstatus des Höhenstandssensors HR |
| STAT_VERSORGUNG_HS_VL_WERT | real | Spannung der Versorgungsspannung des Höhenstandssensors VL |
| STAT_VERSORGUNG_HS_VL_EINH | string | Einheit der Versorgungsspannung  des Höhenstandssensors VL |
| STAT_VERSORGUNG_VL_FEHLER_WERT | unsigned char | Fehlerstatus der Versorgungsspannung VL |
| STAT_VERSORGUNG_VL_FEHLER_TEXT | string | Fehlerstatus der Versorgungsspannung VL |
| STAT_VERSORGUNG_HS_VR_WERT | real | Spannung der Versorgungsspannung des Höhenstandssensors VR |
| STAT_VERSORGUNG_HS_VR_EINH | string | Einheit der Versorgungsspannung  des Höhenstandssensors VR |
| STAT_VERSORGUNG_VR_FEHLER_WERT | unsigned char | Fehlerstatus der Versorgungsspannung VR |
| STAT_VERSORGUNG_VR_FEHLER_TEXT | string | Fehlerstatus der Versorgungsspannung VR |
| STAT_VERSORGUNG_HS_HL_WERT | real | Spannung der Versorgungsspannung des Höhenstandssensors HL |
| STAT_VERSORGUNG_HS_HL_EINH | string | Einheit der Versorgungsspannung  des Höhenstandssensors HL |
| STAT_VERSORGUNG_HL_FEHLER_WERT | unsigned char | Fehlerstatus der Versorgungsspannung HL |
| STAT_VERSORGUNG_HL_FEHLER_TEXT | string | Fehlerstatus der Versorgungsspannung HL |
| STAT_VERSORGUNG_HS_HR_WERT | real | Spannung der Versorgungsspannung des Höhenstandssensors HR |
| STAT_VERSORGUNG_HS_HR_EINH | string | Einheit der Versorgungsspannung  des Höhenstandssensors HR |
| STAT_VERSORGUNG_HR_FEHLER_WERT | unsigned char | Fehlerstatus der Versorgungsspannung HR |
| STAT_VERSORGUNG_HR_FEHLER_TEXT | string | Fehlerstatus der Versorgungsspannung HR |
| STAT_U_ENABLE_L_WERT | real | Spannung des Enableausgang Links |
| STAT_U_ENABLE_L_EINH | string | Einheit der Spannung des Enableausgang Links |
| STAT_ENABLE_L_FEHLER_WERT | unsigned char | Fehlerstatus des Enableausgangs Links |
| STAT_ENABLE_L_FEHLER_TEXT | string | Fehlerstatus des Enableausgangs Links |
| STAT_U_ENABLE_R_WERT | real | Spannung des Enableausgang Rechts |
| STAT_U_ENABLE_R_EINH | string | Einheit der Spannung des Enableausgang Rechts |
| STAT_ENABLE_R_FEHLER_WERT | unsigned char | Fehlerstatus des Enableausgangs Rechts |
| STAT_ENABLE_R_FEHLER_TEXT | string | Fehlerstatus des Enableausgangs Rechts |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-abgleich-hoehenstand"></a>
### STEUERN_ABGLEICH_HOEHENSTAND

Schreiben der Abgleichdaten für den Höhenstand KWP 2000: $3B WriteDataByLocalIdentifier $21 HS-Abgleich

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DELTA_HOEHE_VL | char | Abweichung der Fahrzeughöhe vorne links vom Sollnullpunkt in mm (-125..125) |
| DELTA_HOEHE_VR | char | Abweichung der Fahrzeughöhe vorne rechts vom Sollnullpunkt in mm (-125..125) |
| DELTA_HOEHE_HL | char | Abweichung der Fahrzeughöhe hinten links vom Sollnullpunkt in mm (-125..125) |
| DELTA_HOEHE_HR | char | Abweichung der Fahrzeughöhe hinten rechts vom Sollnullpunkt in mm (-125..125) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSOR_VL_WERT | unsigned int | aktueller Sensorwert (in Digits) |
| STAT_SENSOR_VL_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_VERSORGUNG_VL_WERT | unsigned int | aktuelle Versorgungsspannung (in Digits) |
| STAT_VERSORGUNG_VL_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_AD_0_VL_WERT | unsigned int | AD-Wert zum Sollnullpunkt (in Digits) |
| STAT_AD_0_VL_EINH | string | Einheit des AD-Wertes (Digits) |
| STAT_STEIGUNG_VL_WERT | int | Steigung des Sensors VL (in Digits/mm) |
| STAT_STEIGUNG_VL_EINH | string | Einheit der Sensorsteigung (Digits/mm) |
| STAT_HOEHE_VL_WERT | long | Abweichung der Fahrzeughöhe vorne links vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_VL_EINH | string | Einheit der Fahrzeughöhe (mm) |
| STAT_SENSOR_VR_WERT | unsigned int | aktueller Sensorwert (in Digits) |
| STAT_SENSOR_VR_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_VERSORGUNG_VR_WERT | unsigned int | aktuelle Versorgungsspannung (in Digits) |
| STAT_VERSORGUNG_VR_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_AD_0_VR_WERT | unsigned int | AD-Wert zum Sollnullpunkt (in Digits) |
| STAT_AD_0_VR_EINH | string | Einheit des AD-Wertes (Digits) |
| STAT_STEIGUNG_VR_WERT | int | Steigung des Sensors VR (in Digits/mm) |
| STAT_STEIGUNG_VR_EINH | string | Einheit der Sensorsteigung (Digits/mm) |
| STAT_HOEHE_VR_WERT | long | Abweichung der Fahrzeughöhe vorne links vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_VR_EINH | string | Einheit der Fahrzeughöhe (mm) |
| STAT_SENSOR_HL_WERT | unsigned int | aktueller Sensorwert (in Digits) |
| STAT_SENSOR_HL_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_VERSORGUNG_HL_WERT | unsigned int | aktuelle Versorgungsspannung (in Digits) |
| STAT_VERSORGUNG_HL_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_AD_0_HL_WERT | unsigned int | AD-Wert zum Sollnullpunkt (in Digits) |
| STAT_AD_0_HL_EINH | string | Einheit des AD-Wertes (Digits) |
| STAT_STEIGUNG_HL_WERT | int | Steigung des Sensors HL (in Digits/mm) |
| STAT_STEIGUNG_HL_EINH | string | Einheit der Sensorsteigung (Digits/mm) |
| STAT_HOEHE_HL_WERT | long | Abweichung der Fahrzeughöhe hinten links vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_HL_EINH | string | Einheit der Fahrzeughöhe (mm) |
| STAT_SENSOR_HR_WERT | unsigned int | aktueller Sensorwert (in Digits) |
| STAT_SENSOR_HR_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_VERSORGUNG_HR_WERT | unsigned int | aktuelle Versorgungsspannung (in Digits) |
| STAT_VERSORGUNG_HR_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_AD_0_HR_WERT | unsigned int | AD-Wert zum Sollnullpunkt (in Digits) |
| STAT_AD_0_HR_EINH | string | Einheit des AD-Wertes (Digits) |
| STAT_STEIGUNG_HR_WERT | int | Steigung des Sensors HR (in Digits/mm) |
| STAT_STEIGUNG_HR_EINH | string | Einheit der Sensorsteigung (Digits/mm) |
| STAT_HOEHE_HR_WERT | long | Abweichung der Fahrzeughöhe hinten rechts vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_HR_EINH | string | Einheit der Fahrzeughöhe (mm) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-abgleich-hoehenstand"></a>
### STATUS_ABGLEICH_HOEHENSTAND

Lesen der Abgleichdaten für den Höhenstand KWP 2000: $21 ReadDataByLocalIdentifier $21 HS-Abgleich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSOR_VL_WERT | unsigned int | aktueller Sensorwert (in Digits) |
| STAT_SENSOR_VL_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_VERSORGUNG_VL_WERT | unsigned int | aktuelle Versorgungsspannung (in Digits) |
| STAT_VERSORGUNG_VL_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_AD_0_VL_WERT | unsigned int | AD-Wert zum Sollnullpunkt (in Digits) |
| STAT_AD_0_VL_EINH | string | Einheit des AD-Wertes (Digits) |
| STAT_STEIGUNG_VL_WERT | int | Steigung des Sensors VL (in Digits/m) |
| STAT_STEIGUNG_VL_EINH | string | Einheit der Sensorsteigung (Digits/m) |
| STAT_HOEHE_VL_WERT | long | Abweichung der Fahrzeughöhe vorne links vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_VL_EINH | string | Einheit der Fahrzeughöhe (mm) |
| STAT_SENSOR_VR_WERT | unsigned int | aktueller Sensorwert (in Digits) |
| STAT_SENSOR_VR_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_VERSORGUNG_VR_WERT | unsigned int | aktuelle Versorgungsspannung (in Digits) |
| STAT_VERSORGUNG_VR_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_AD_0_VR_WERT | unsigned int | AD-Wert zum Sollnullpunkt (in Digits) |
| STAT_AD_0_VR_EINH | string | Einheit des AD-Wertes (Digits) |
| STAT_STEIGUNG_VR_WERT | int | Steigung des Sensors VR (in Digits/m) |
| STAT_STEIGUNG_VR_EINH | string | Einheit der Sensorsteigung (Digits/m) |
| STAT_HOEHE_VR_WERT | long | Abweichung der Fahrzeughöhe vorne rechts vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_VR_EINH | string | Einheit der Fahrzeughöhe (mm) |
| STAT_SENSOR_HL_WERT | unsigned int | aktueller Sensorwert (in Digits) |
| STAT_SENSOR_HL_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_VERSORGUNG_HL_WERT | unsigned int | aktuelle Versorgungsspannung (in Digits) |
| STAT_VERSORGUNG_HL_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_AD_0_HL_WERT | unsigned int | AD-Wert zum Sollnullpunkt (in Digits) |
| STAT_AD_0_HL_EINH | string | Einheit des AD-Wertes (Digits) |
| STAT_STEIGUNG_HL_WERT | int | Steigung des Sensors HL (in Digits/m) |
| STAT_STEIGUNG_HL_EINH | string | Einheit der Sensorsteigung (Digits/m) |
| STAT_HOEHE_HL_WERT | long | Abweichung der Fahrzeughöhe hinten links vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_HL_EINH | string | Einheit der Fahrzeughöhe (mm) |
| STAT_SENSOR_HR_WERT | unsigned int | aktueller Sensorwert (in Digits) |
| STAT_SENSOR_HR_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_VERSORGUNG_HR_WERT | unsigned int | aktuelle Versorgungsspannung (in Digits) |
| STAT_VERSORGUNG_HR_EINH | string | Einheit des Sensorwertes (Digits) |
| STAT_AD_0_HR_WERT | unsigned int | AD-Wert zum Sollnullpunkt (in Digits) |
| STAT_AD_0_HR_EINH | string | Einheit des AD-Wertes (Digits) |
| STAT_STEIGUNG_HR_WERT | int | Steigung des Sensors HR (in Digits/m) |
| STAT_STEIGUNG_HR_EINH | string | Einheit der Sensorsteigung (Digits/m) |
| STAT_HOEHE_HR_WERT | long | Abweichung der Fahrzeughöhe hinten rechts vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_HR_EINH | string | Einheit der Fahrzeughöhe (mm) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrzeughoehe"></a>
### STATUS_FAHRZEUGHOEHE

Lesen der Abgleichdaten für den Höhenstand KWP 2000: $21 ReadDataByLocalIdentifier $21 HS-Abgleich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HOEHE_VL_WERT | long | Abweichung der Fahrzeughöhe vorne links vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_VL_EINH | string | Einheit der Fahrzeughöhe (mm) |
| STAT_HOEHE_VR_WERT | long | Abweichung der Fahrzeughöhe vorne rechts vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_VR_EINH | string | Einheit der Fahrzeughöhe (mm) |
| STAT_HOEHE_HL_WERT | long | Abweichung der Fahrzeughöhe hinten links vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_HL_EINH | string | Einheit der Fahrzeughöhe (mm) |
| STAT_HOEHE_HR_WERT | long | Abweichung der Fahrzeughöhe hinten rechts vom Sollnullpunkt in mm (-125..125) |
| STAT_HOEHE_HR_EINH | string | Einheit der Fahrzeughöhe (mm) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bus-diagnose-modul"></a>
### STATUS_BUS_DIAGNOSE_MODUL

Liest die Bus-Diagnose-Daten des FlexRays KWP 2000: $21 ReadDataByLocalIdentifier $31 FR-Status auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BDM_VERSION | unsigned char | Versionsnummer des Bus-Diagnose-Moduls |
| STAT_OS_SYNC_WERT | unsigned char | Status, ob das OS synchron zum FlexRay ist |
| STAT_OS_SYNC_TEXT | string | Status, ob das OS synchron zum FlexRay ist |
| STAT_KM_ANFANG_WERT | unsigned long | Kilometerstand bei Beginn der Aufzeichnung |
| STAT_KM_ANFANG_EINH | string | Einheit des Kilometerstandes (Anfangswert) |
| STAT_KM_AKTUELL_WERT | unsigned long | aktueller Kilometerstand |
| STAT_KM_AKTUELL_EINH | string | Einheit des Kilometerstandes (Endewert) |
| STAT_WEGSTRECKE_WERT | unsigned long | zurückgelegte Wegstrecke in km seit Beginn der Aufzeichnung |
| STAT_WEGSTRECKE_EINH | string | Einheit der zurückgelegten Wegstrecke seit Beginn der Aufzeichnung |
| STAT_BETRIEBSZEIT_WERT | unsigned long | Betriebszeit des BDM (in Sekunden) |
| STAT_BETRIEBSZEIT_EINH | string | Einheit der Betriebszeit des BDM (Sekunden) |
| STAT_BETRIEBSZEIT_TEXT | string | Betriebszeit des BDM (in hh:mm:ss) |
| STAT_CSEC0R | unsigned int | globaler Fehlerzähler |
| STAT_CSEC0R_KL_1 | unsigned int | Klasse 1: 0ms &lt; t &lt;= 5ms |
| STAT_CSEC0R_KL_2 | unsigned int | Klasse 2: 5ms &lt; t &lt;= 320ms |
| STAT_CSEC0R_KL_3 | unsigned int | Klasse 3: 320ms &lt; t &lt;= 10s |
| STAT_CSEC0R_KL_4 | unsigned int | Klasse 4: 10s &lt; t &lt;= 5min |
| STAT_CSEC0R_KL_5 | unsigned int | Klasse 5: t &gt; 5min |
| STAT_BOUNDARY_VIOLATION | unsigned int | Frame geht über Slotgrenze hinaus |
| STAT_CONTENT_ERROR | unsigned int | z.B. HeaderCRC- oder FrameCRC-Fehler |
| STAT_SYNTAX_ERROR | unsigned int | z.B. Dekodierungsfehler |
| STAT_FRAME_ERROR_1 | unsigned int | Fehlerzähler für jeden empfangenen Frame |
| STAT_FRAME_ERROR_2 | unsigned int | Fehlerzähler für jeden empfangenen Frame |
| STAT_FRAME_ERROR_3 | unsigned int | Fehlerzähler für jeden empfangenen Frame |
| STAT_FRAME_ERROR_4 | unsigned int | Fehlerzähler für jeden empfangenen Frame |
| STAT_FRAME_ERROR_5 | unsigned int | Fehlerzähler für jeden empfangenen Frame |
| STAT_FRAME_ERROR_6 | unsigned int | Fehlerzähler für jeden empfangenen Frame |
| STAT_FRAME_ERROR_7 | unsigned int | Fehlerzähler für jeden empfangenen Frame |
| STAT_FRAME_ERROR_8 | unsigned int | Fehlerzähler für jeden empfangenen Frame |
| STAT_SYNC_LOST | unsigned int | Zähler für SYNC_LOST |
| STAT_STARTUP_TIME_KL_1 | unsigned int | Klasse 1: 0ms &lt; t_up &lt;= 50ms |
| STAT_STARTUP_TIME_KL_2 | unsigned int | Klasse 2: 50ms &lt; t_up &lt;= 65ms |
| STAT_STARTUP_TIME_KL_3 | unsigned int | Klasse 3: 65ms &lt; t_up &lt;= 100ms |
| STAT_STARTUP_TIME_KL_4 | unsigned int | Klasse 4: t_up &gt; 100ms |
| STAT_BUSERROR_BD_R | unsigned int | Busdriver 1: Physikalischer Busfehler, Kurzschluß, Unterbrechung |
| STAT_UNDERVOLTAGE_BD_R | unsigned int | Busdriver 1: UVVBAT, UVVCC und UVVIO |
| STAT_OVERTEMP_BD_R | unsigned int | Busdriver 1: Überhitzung, Überstrom |
| STAT_BUSERROR_BD_L | unsigned int | Busdriver 2: Physikalischer Busfehler, Kurzschluß, Unterbrechung |
| STAT_UNDERVOLTAGE_BD_L | unsigned int | Busdriver 2: UVVBAT, UVVCC und UVVIO |
| STAT_OVERTEMP_BD_L | unsigned int | Busdriver 2: Überhitzung, Überstrom |
| STAT_BUSERROR | unsigned int | Summe Buserror von Busdriver 1 und 2 |
| STAT_UNDERVOLTAGE | unsigned int | Summe der Unterspannungsfehler von Busdriver 1 und 2 |
| STAT_OVERTEMP | unsigned int | Summe der Fehler für Überhitzung/Überstrom von Busdriver 1 und 2 |
| STAT_FREEZE_FLAG | unsigned char | Status der FlexRay-Statistik Zähler eingefroren oder aktiv |
| STAT_EEPROM_ERROR_FLAG | unsigned char | zeigt an, ob die EEProm-Daten zwischenzeitlich zerstört waren |
| STAT_SYNC_FAILED | unsigned int | Anzahl der gescheiterten Synchronisationsversuche nach dem Aufstarten |
| STAT_SYNC_NOISE | unsigned int | Anzahl Synchronisationsversuche mit Rauschen auf dem Bus |
| STAT_SYNC_NOISE_CYCLE | unsigned int | Anzahl Synchronisationsversuche mit Rauschen auf dem Bus in diesem Wachzyklus |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-reset-bus-diagnose-modul"></a>
### STEUERN_RESET_BUS_DIAGNOSE_MODUL

Setzt die Daten des FlexRay Busstatusmodul zurück KWP 2000: $3B ReadDataByLocalIdentifier $31 FR-Status schreiben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wcet-lesen"></a>
### STATUS_WCET_LESEN

Liest die im VDM gespeicherten max. Laufzeiten aller Tasks KWP 2000: $21 ReadDataByLocalIdentifier $51 WCET auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WCET_TASK_0_WERT | unsigned int | WCET für die Task-ID 0 |
| STAT_WCET_TASK_1_WERT | unsigned int | WCET für die Task-ID 1 |
| STAT_WCET_TASK_2_WERT | unsigned int | WCET für die Task-ID 2 |
| STAT_WCET_TASK_3_WERT | unsigned int | WCET für die Task-ID 3 |
| STAT_WCET_TASK_4_WERT | unsigned int | WCET für die Task-ID 4 |
| STAT_WCET_TASK_5_WERT | unsigned int | WCET für die Task-ID 5 |
| STAT_WCET_TASK_6_WERT | unsigned int | WCET für die Task-ID 6 |
| STAT_WCET_TASK_7_WERT | unsigned int | WCET für die Task-ID 7 |
| STAT_WCET_TASK_8_WERT | unsigned int | WCET für die Task-ID 8 |
| STAT_WCET_TASK_9_WERT | unsigned int | WCET für die Task-ID 9 |
| STAT_WCET_TASK_10_WERT | unsigned int | WCET für die Task-ID 10 |
| STAT_WCET_TASK_11_WERT | unsigned int | WCET für die Task-ID 11 |
| STAT_WCET_TASK_12_WERT | unsigned int | WCET für die Task-ID 12 |
| STAT_WCET_TASK_13_WERT | unsigned int | WCET für die Task-ID 13 |
| STAT_WCET_EINH | string | Einheit für die WCET |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-reset-wcet"></a>
### STEUERN_RESET_WCET

Setzt die maximal erkannten Tasklaufzeiten zurück KWP 2000: $3B ReadDataByLocalIdentifier $51 WCET zurücksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-compiler-bootloader"></a>
### STATUS_COMPILER_BOOTLOADER

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des MPC-Bootloader KWP 2000: $21 ReadDataByLocalIdentifier $A0 status_compiler_bootloader

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSSYSTEM | string | Betriebssystem der Workstation |
| STAT_USER | string | Bearbeiter |
| STAT_PC | string | Name der Workstation, dort wurde der Stand uebersetzt |
| STAT_DATUM | string | Compilerdatum, an diesem Tag wurde der Stand uebersetzt |
| STAT_ZEIT | string | Compilerzeit, zu dieser Zeit wurde der Stand uebersetzt |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-compiler-applikation"></a>
### STATUS_COMPILER_APPLIKATION

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der Applikation KWP 2000: $21 ReadDataByLocalIdentifier $A1 status_compiler_applikation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSSYSTEM | string | Betriebssystem der Workstation |
| STAT_USER | string | Bearbeiter |
| STAT_PC | string | Name der Workstation, dort wurde der Stand uebersetzt |
| STAT_DATUM | string | Compilerdatum, an diesem Tag wurde der Stand uebersetzt |
| STAT_ZEIT | string | Compilerzeit, zu dieser Zeit wurde der Stand uebersetzt |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-compiler-daf"></a>
### STATUS_COMPILER_DAF

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des DAF KWP 2000: $21 ReadDataByLocalIdentifier $A3 status_compiler_daf

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSSYSTEM | string | Betriebssystem der Workstation |
| STAT_USER | string | Bearbeiter |
| STAT_PC | string | Name der Workstation, dort wurde der Stand uebersetzt |
| STAT_DATUM | string | Compilerdatum, an diesem Tag wurde der Stand uebersetzt |
| STAT_ZEIT | string | Compilerzeit, zu dieser Zeit wurde der Stand uebersetzt |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-read-ll-error"></a>
### _STATUS_READ_LL_ERROR

Liest die momentanen Stati der LL-Fehlerpruefung KWP 2000: $21 ReadDataByLocalIdentifier $20 interne Fehlerstati lesen interner TEMIC-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LLSW | unsigned char | Status der LL-SW |
| STAT_KL30 | unsigned char | Status der Spannung an KL30 |
| STAT_TASTER_KS | unsigned char | Status des Taster Komfort/Sport |
| STAT_ENABLE_LI | unsigned char | Status der Enableleitung Links |
| STAT_ENABLE_RE | unsigned char | Status der Enableleitung Rechts |
| STAT_HSENSOR_VL | unsigned char | Status des Hoehenstandssensor VL |
| STAT_SPG_HSENSOR_VL | unsigned char | Status der Versorgung des Hoehenstandssensor VL |
| STAT_HSENSOR_VR | unsigned char | Status des Hoehenstandssensor VR |
| STAT_SPG_HSENSOR_VR | unsigned char | Status der Versorgung des Hoehenstandssensor VR |
| STAT_HSENSOR_HL | unsigned char | Status des Hoehenstandssensor HL |
| STAT_SPG_HSENSOR_HL | unsigned char | Status der Versorgung des Hoehenstandssensor HL |
| STAT_HSENSOR_HR | unsigned char | Status des Hoehenstandssensor HR |
| STAT_SPG_HSENSOR_HR | unsigned char | Status der Versorgung des Hoehenstandssensor HR |
| STAT_EEPROM | unsigned long | Fehler der EEProm-Daten |
| STAT_PTC_BEDIENUNG_VD | unsigned char | Status der PT-Can Nachricht Bedienung VDM |
| STAT_PTC_MOTORDATEN | unsigned char | Status der PT-Can Nachricht Motordaten |
| STAT_PTC_STAT_ARS | unsigned char | Status der PT-Can Nachricht Status ARS |
| STAT_PTC_STAT_DSC | unsigned char | Status der PT-Can Nachricht Status DSC |
| STAT_PTC_GETRIEBEDATEN | unsigned char | Status der PT-Can Nachricht Getriebedaten |
| STAT_PTC_DREHMOMENT3 | unsigned char | Status der PT-Can Nachricht Drehmoment 3 |
| STAT_PTC_STAT_FUNKSCHLUESSEL | unsigned char | Status der PT-Can Nachricht Status Funkschluessel |
| STAT_PTC_KLEMMENSTATUS | unsigned char | Status der PT-Can Nachricht Klemmenstatus |
| STAT_PTC_GESCHWINDIGKEIT | unsigned char | Status der PT-Can Nachricht Geschwindigkeit |
| STAT_PTC_AUSSENTEMPERATUR | unsigned char | Status der PT-Can Nachricht Aussentemperatur / Relativzeit |
| STAT_PTC_KILOMETERSTAND | unsigned char | Status der PT-Can Nachricht Kilometerstand |
| STAT_FC_ENDTEST_RXD | unsigned char | Status der F-Can Nachricht Endtest RxD |
| STAT_FC_SENSOR_DATA_ROSE | unsigned char | Status der F-Can Nachricht Sensor Daten ROSE |
| STAT_FC_EXCH_AFS_DSC | unsigned char | Status der F-Can Nachricht Austausch AFS - DSC |
| STAT_FC_RADGESCHWINDIGKEIT | unsigned char | Status der F-Can Nachricht Geschwindigkeit Rad |
| STAT_FC_CLU2_VDA | unsigned char | Status der F-Can Nachricht CLU2 VDA |
| STAT_FC_LENKRADWINKEL2 | unsigned char | Status der F-Can Nachricht Lenkradwinkel Oben 2 |
| STAT_FC_QDYN_ARS_VDM | unsigned char | Status der F-Can Nachricht Querdynamik ARS-VDM |
| STAT_FC_CLU1_VDA | unsigned char | Status der F-Can Nachricht CLU1 VDA |
| STAT_FC_CLU_ST_VDA | unsigned char | Status der F-Can Nachricht CLU Status VDA |
| STAT_FR_ST_EDCS_VL | unsigned char | Status der FlexRay Nachricht Status EDCS VL |
| STAT_FR_ST_EDCS_VR | unsigned char | Status der FlexRay Nachricht Status EDCS VR |
| STAT_FR_ST_EDCS_HL | unsigned char | Status der FlexRay Nachricht Status EDCS HL |
| STAT_FR_ST_EDCS_HR | unsigned char | Status der FlexRay Nachricht Status EDCS HR |
| STAT_POR_FLAG | unsigned int | Aktueller Wert des POR-Flag |
| STAT_POR_COUNTER | unsigned int | Aktueller Wert des POR-Zähler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lenkwinkel-reset"></a>
### _STEUERN_LENKWINKEL_RESET

Setzt die Lernwerte für den Lenkwinkel zurück KWP 2000: $3B ReadDataByLocalIdentifier $40 Lenkwinkel zurücksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tja"></a>
### _STATUS_TJA

Liest die Busstatistik des FlexRays KWP 2000: $31 ReadDataByLocalIdentifier $AF TJA-Status auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_S0_WAKEUP_R | unsigned int | Wake Flag |
| STAT_S1_WAKEUP_SOURCE_R | unsigned int | Wakeup Source Flag |
| STAT_S2_STAR_CONFIG_R | unsigned int | Star Configuration Flag |
| STAT_S3_PWON_R | unsigned int |  |
| STAT_S4_BUS_ERROR_R | unsigned int |  |
| STAT_S5_TEMP_HIGH_R | unsigned int |  |
| STAT_S6_TEMP_MEDIUM_R | unsigned int |  |
| STAT_S7_TXEN_BGE_CLAMPED_R | unsigned int |  |
| STAT_S8_UVVBAT_R | unsigned int |  |
| STAT_S9_UVVCC_R | unsigned int |  |
| STAT_S10_UVVIO_R | unsigned int |  |
| STAT_S11_STAR_LOCKED_R | unsigned int |  |
| STAT_S12_TRXD_COLLISION_R | unsigned int |  |
| STAT_S0_WAKEUP_L | unsigned int | Wake Flag |
| STAT_S1_WAKEUP_SOURCE_L | unsigned int | Wakeup Source Flag |
| STAT_S2_STAR_CONFIG_L | unsigned int | Star Configuration Flag |
| STAT_S3_PWON_L | unsigned int |  |
| STAT_S4_BUS_ERROR_L | unsigned int |  |
| STAT_S5_TEMP_HIGH_L | unsigned int |  |
| STAT_S6_TEMP_MEDIUM_L | unsigned int |  |
| STAT_S7_TXEN_BGE_CLAMPED_L | unsigned int |  |
| STAT_S8_UVVBAT_L | unsigned int |  |
| STAT_S9_UVVCC_L | unsigned int |  |
| STAT_S10_UVVIO_L | unsigned int |  |
| STAT_S11_STAR_LOCKED_L | unsigned int |  |
| STAT_S12_TRXD_COLLISION_L | unsigned int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-error-injektion"></a>
### _STEUERN_ERROR_INJEKTION

Zur Vorgabe von Fehlern KWP2000: $3B WriteDataByLocalIdentifier $30 Fehlerinjektion interner TEMIC-Job Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLERNUMMER | unsigned char | Dieser Fehler wird vorgegeben Auswahl über VDM-LH Teil 3 |
| RESET_ZAEHLER | unsigned char | So viele Zyklen wird der Fehler vorgegeben |
| PARAMETER | unsigned int | dieser Parameter wird job-spezifisch verwendet siehe VDM-LH Teil 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-errcode"></a>
### _STATUS_ERRCODE

Gibt den Errorcode und die Umwelt- bedingungen eines kritischen Fehlers zurück KWP 2000: $21 ReadDataByLocalIdentifier $35 Errorcode auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ERR_CODE | unsigned long | Fehlercode des kritischen Fehlers |
| STAT_ERR_COND1 | unsigned long | 1. Umweltbedingung |
| STAT_ERR_COND2 | unsigned long | 2. Umweltbedingung |
| STAT_EXCEPT_ADDR | unsigned long | Adresse der Exception |
| STAT_EXCEPT_STAT | unsigned long | Status der Exception |
| STAT_POR_FLAG1 | unsigned long | Power-On-Reset-Flag 1 |
| STAT_POR_FLAG2 | unsigned long | Power-On-Reset-Flag 2 |
| STAT_OS_SHTDWN | unsigned int | OS-Shutdown |
| STAT_DISP1 | unsigned char |  |
| STAT_DISP2 | unsigned char |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-reset-errcode"></a>
### _STEUERN_RESET_ERRCODE

Setzt den Errorcode und die Umweltbedingungen zurück KWP 2000: $3B ReadDataByLocalIdentifier $35 Errorcode und UBs schreiben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-eingaenge"></a>
### _STATUS_ANALOG_EINGAENGE

Lesen der Abgleichdaten für den Höhenstand KWP 2000: $21 ReadDataByLocalIdentifier $22 Analoge Eingaenge lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_U_KL30_WERT | unsigned int | Spannung KL30 |
| STAT_U_KL30_EINH | string | Einheit Spannung KL30 (mV) |
| STAT_U_KL30_FEHLER_WERT | unsigned char | Fehlerstatus der KL30 |
| STAT_U_KL30_FEHLER_TEXT | string | Fehlerstatus der KL30 |
| STAT_WECKLEITUNG | unsigned char | Status der Weckleitung |
| STAT_WECKLEITUNG_TEXT | string | Status der Weckleitung |
| STAT_U_HS_VL_WERT | unsigned int | Spannung des Höhenstandssensors VL |
| STAT_U_HS_VL_EINH | string | Einheit der Spannung des Höhenstandssensors VL |
| STAT_HS_VL_FEHLER_WERT | unsigned char | Fehlerstatus des Höhenstandssensors VL |
| STAT_HS_VL_FEHLER_TEXT | string | Fehlerstatus des Höhenstandssensors VL |
| STAT_U_HS_VR_WERT | unsigned int | Spannung des Höhenstandssensors VR |
| STAT_U_HS_VR_EINH | string | Einheit der Spannung des Höhenstandssensors VR |
| STAT_HS_VR_FEHLER_WERT | unsigned char | Fehlerstatus des Höhenstandssensors VR |
| STAT_HS_VR_FEHLER_TEXT | string | Fehlerstatus des Höhenstandssensors VR |
| STAT_U_HS_HL_WERT | unsigned int | Spannung des Höhenstandssensors HL |
| STAT_U_HS_HL_EINH | string | Einheit der Spannung des Höhenstandssensors HL |
| STAT_HS_HL_FEHLER_WERT | unsigned char | Fehlerstatus des Höhenstandssensors HL |
| STAT_HS_HL_FEHLER_TEXT | string | Fehlerstatus des Höhenstandssensors HL |
| STAT_U_HS_HR_WERT | unsigned int | Spannung des Höhenstandssensors HR |
| STAT_U_HS_HR_EINH | string | Einheit der Spannung des Höhenstandssensors HR |
| STAT_HS_HR_FEHLER_WERT | unsigned char | Fehlerstatus des Höhenstandssensors HR |
| STAT_HS_HR_FEHLER_TEXT | string | Fehlerstatus des Höhenstandssensors HR |
| STAT_VERSORGUNG_HS_VL_WERT | unsigned int | Spannung der Versorgungsspannung des Höhenstandssensors VL |
| STAT_VERSORGUNG_HS_VL_EINH | string | Einheit der Versorgungsspannung  des Höhenstandssensors VL |
| STAT_VERSORGUNG_VL_FEHLER_WERT | unsigned char | Fehlerstatus der Versorgungsspannung VL |
| STAT_VERSORGUNG_VL_FEHLER_TEXT | string | Fehlerstatus der Versorgungsspannung VL |
| STAT_VERSORGUNG_HS_VR_WERT | unsigned int | Spannung der Versorgungsspannung des Höhenstandssensors VR |
| STAT_VERSORGUNG_HS_VR_EINH | string | Einheit der Versorgungsspannung  des Höhenstandssensors VR |
| STAT_VERSORGUNG_VR_FEHLER_WERT | unsigned char | Fehlerstatus der Versorgungsspannung VR |
| STAT_VERSORGUNG_VR_FEHLER_TEXT | string | Fehlerstatus der Versorgungsspannung VR |
| STAT_VERSORGUNG_HS_HL_WERT | unsigned int | Spannung der Versorgungsspannung des Höhenstandssensors HL |
| STAT_VERSORGUNG_HS_HL_EINH | string | Einheit der Versorgungsspannung  des Höhenstandssensors HL |
| STAT_VERSORGUNG_HL_FEHLER_WERT | unsigned char | Fehlerstatus der Versorgungsspannung HL |
| STAT_VERSORGUNG_HL_FEHLER_TEXT | string | Fehlerstatus der Versorgungsspannung HL |
| STAT_VERSORGUNG_HS_HR_WERT | unsigned int | Spannung der Versorgungsspannung des Höhenstandssensors HR |
| STAT_VERSORGUNG_HS_HR_EINH | string | Einheit der Versorgungsspannung  des Höhenstandssensors HR |
| STAT_VERSORGUNG_HR_FEHLER_WERT | unsigned char | Fehlerstatus der Versorgungsspannung HR |
| STAT_VERSORGUNG_HR_FEHLER_TEXT | string | Fehlerstatus der Versorgungsspannung HR |
| STAT_U_ENABLE_L_WERT | unsigned int | Spannung des Enableausgang Links |
| STAT_U_ENABLE_L_EINH | string | Einheit der Spannung des Enableausgang Links |
| STAT_ENABLE_L_FEHLER_WERT | unsigned char | Fehlerstatus des Enableausgangs Links |
| STAT_ENABLE_L_FEHLER_TEXT | string | Fehlerstatus des Enableausgangs Links |
| STAT_U_ENABLE_R_WERT | unsigned int | Spannung des Enableausgang Rechts |
| STAT_U_ENABLE_R_EINH | string | Einheit der Spannung des Enableausgang Rechts |
| STAT_ENABLE_R_FEHLER_WERT | unsigned char | Fehlerstatus des Enableausgangs Rechts |
| STAT_ENABLE_R_FEHLER_TEXT | string | Fehlerstatus des Enableausgangs Rechts |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-xcp-fr"></a>
### _STEUERN_XCP_FR

Freigabe oder Sperren der XCP-Schnittstelle über FlexRay KWP 2000: $3B WriteDataByLocalIdentifier $26 XCP freigeben/sperren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| XCP | char | Freigabewert für die XCP-Schnittstelle 0x01: Freigabe (Authentisierung erforderlich) 0x00: Sperren  (keine Authentiserung erforderlich) sonstige Werte: ebenfalls sperren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-xcp-fr"></a>
### _STATUS_XCP_FR

Liest den aktuellen Freigabestatus der XCP-Schnittstelle aus KWP 2000: $21 ReadDataByLocalIdentifier $26 Status XCP-Schnittstelle interner TEMIC-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_XCP_FR_WERT | unsigned char | Status der XCP-Schnittstelle |
| STAT_XCP_FR_TEXT | string | Status der XCP-Schnittstelle |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tracenummer"></a>
### _STATUS_TRACENUMMER

Liest die Temic Tracenummer KWP 2000: $21 ReadDataByLocalIdentifier $70 Temic Tracenummer lesen interner TEMIC-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TRACENUMMER_HEX | string | Status der LL-SW |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ad-ref"></a>
### _STATUS_AD_REF

Liest die AD-Referenzspannung zurück KWP 2000: $21 ReadDataByLocalIdentifier $72 Temic AD-Referenzspannung lesen interner TEMIC-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AD_REF_WERT | int | Status der LL-SW |
| STAT_AD_REF_EINH | string | Einheit der Referenzspannung (mV) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-endtest-intern"></a>
### _STATUS_ENDTEST_INTERN

Gibt den Status vom ROM-, RAM-, ALU- und ADC-Check sowie die Reset-Zeit bei einem vorangegangenen Watchdog-Fehler zurück KWP 2000: $21 ReadDataByLocalIdentifier $34 interner Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INT_RAM | unsigned char | Status des RAM-Checks |
| STAT_INT_RAM_TEXT | string |  |
| STAT_INT_ROM | unsigned char | Status des ROM-Checks |
| STAT_INT_ROM_TEXT | string |  |
| STAT_INT_ALU | unsigned char | Status des ALU-Checks |
| STAT_INT_ALU_TEXT | string |  |
| STAT_INT_ADC | unsigned char | Status des ADC-Checks |
| STAT_INT_ADC_TEXT | string |  |
| STAT_INT_WDG_RESET_ZYKLEN | unsigned char | Dauer des letzten Watchdog-Resets |
| STAT_INT_WDG_RESET_ZEIT | string | Dauer des letzten Watchdog-Resets |
| STAT_INT_WDG_RESET_ZEIT_EINH | string | Einheit Resetdauer (ms) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-endtest-fr"></a>
### _STATUS_ENDTEST_FR

Gibt den Bus- und Nachrichtentransfer- Status auf dem FlexRay zurück Meßdauer 1 Sekunde KWP 2000: $21 ReadDataByLocalIdentifier $33 FR-Status auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FR_UNSY_R | unsigned char | Zeitdauer, die rechter FR-Strang unsymmetrisch war (Auflösung: 100ms) |
| STAT_FR_UNSY_L | unsigned char | Zeitdauer, die linker FR-Strang unsymmetrisch war (Auflösung: 100ms) |
| STAT_FR_WRONG_R | unsigned char | Anzahl Nachrichten mit falschem Inhalt auf dem rechten FR-Strang |
| STAT_FR_WRONG_L | unsigned char | Anzahl Nachrichten mit falschem Inhalt auf dem linken FR-Strang |
| STAT_FR_NE_R | unsigned char | Anzahl nicht empfangener Nachrichen auf dem rechten FR-Strang |
| STAT_FR_NE_L | unsigned char | Anzahl nicht empfangener Nachrichen auf dem linken FR-Strang |
| STAT_FR_BUSERR_R | unsigned char | Anzahl TJA-Fehlermeldungen für Buserror auf dem rechten FR-Strang |
| STAT_FR_BUSERR_L | unsigned char | Anzahl TJA-Fehlermeldungen für Buserror auf dem linken FR-Strang |
| STAT_FR_OTEMP_R | unsigned char | Anzahl TJA-Fehlermeldungen für Übertemperatur auf dem rechten FR-Strang |
| STAT_FR_OTEMP_L | unsigned char | Anzahl TJA-Fehlermeldungen für Übertemperatur auf dem linken FR-Strang |
| STAT_FR_LOWVOLT_R | unsigned char | Anzahl TJA-Fehlermeldungen für Unterspannung auf dem rechten FR-Strang |
| STAT_FR_LOWVOLT_L | unsigned char | Anzahl TJA-Fehlermeldungen für Unterspannung auf dem linken FR-Strang |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-endtest-analogwerte"></a>
### _STATUS_ENDTEST_ANALOGWERTE

Liest die Minimal- und Maximalwerte aller Analogeingänge über die Meßdauer von 1 Sekunde KWP 2000: $21 ReadDataByLocalIdentifier $32 analoge Min-/Maxwerte auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_U_2V6_MIN | unsigned int | Minimalwert der Prozessorspannung |
| STAT_U_2V6_MIN_EINH | string | Einheit der minimalen Prozessorspannung (Digits) |
| STAT_U_2V6_MAX | unsigned int | Maximalwert der Prozessorspannung |
| STAT_U_2V6_MAX_EINH | string | Einheit der maximalen Prozessorspannung (Digits) |
| STAT_U_3V3_MIN | unsigned int | Minimalwert der FR-Controllerspannung |
| STAT_U_3V3_MIN_EINH | string | Einheit der minimalen FR-Controllerspannung (Digits) |
| STAT_U_3V3_MAX | unsigned int | Maximalwert der FR-Controllerspannung |
| STAT_U_3V3_MAX_EINH | string | Einheit der maximalen FR-Controllerspannung (Digits) |
| STAT_U_KL30_MIN | unsigned int | Minimalwert der KL30-Spannung |
| STAT_U_KL30_MIN_EINH | string | Einheit der minimalen Klemme 30 Spannung (Digits) |
| STAT_U_KL30_MAX | unsigned int | Maximalwert der KL30-Spannung |
| STAT_U_KL30_MAX_EINH | string | Einheit der maximalen Klemme 30 Spannung (Digits) |
| STAT_SIGN_VL_MIN | unsigned int | Minimalwert der Sensorsignalspannung vorne links |
| STAT_SIGN_VL_MIN_EINH | string | Einheit der minimalen Sensor-Signalspannung VL (Digits) |
| STAT_SIGN_VL_MAX | unsigned int | Maximalwert der Sensorsignalspannung vorne links |
| STAT_SIGN_VL_MAX_EINH | string | Einheit der maximalen Sensor-Signalspannung VL (Digits) |
| STAT_SIGN_VR_MIN | unsigned int | Minimalwert der Sensorsignalspannung vorne rechts |
| STAT_SIGN_VR_MIN_EINH | string | Einheit der minimalen Sensor-Signalspannung VR (Digits) |
| STAT_SIGN_VR_MAX | unsigned int | Maximalwert der Sensorsignalspannung vorne rechts |
| STAT_SIGN_VR_MAX_EINH | string | Einheit der maximalen Sensor-Signalspannung VR (Digits) |
| STAT_SIGN_HL_MIN | unsigned int | Minimalwert der Sensorsignalspannung hinten links |
| STAT_SIGN_HL_MIN_EINH | string | Einheit der minimalen Sensor-Signalspannung HL (Digits) |
| STAT_SIGN_HL_MAX | unsigned int | Maximalwert der Sensorsignalspannung hinten links |
| STAT_SIGN_HL_MAX_EINH | string | Einheit der maximalen Sensor-Signalspannung HL (Digits) |
| STAT_SIGN_HR_MIN | unsigned int | Minimalwert der Sensorsignalspannung hinten rechts |
| STAT_SIGN_HR_MIN_EINH | string | Einheit der minimalen Sensor-Signalspannung HR (Digits) |
| STAT_SIGN_HR_MAX | unsigned int | Maximalwert der Sensorsignalspannung hinten rechts |
| STAT_SIGN_HR_MAX_EINH | string | Einheit der maximalen Sensor-Signalspannung HR (Digits) |
| STAT_VERS_VL_MIN | unsigned int | Minimalwert der Sensorversorgungsspannung vorne links |
| STAT_VERS_VL_MIN_EINH | string | Einheit der minimalen Sensor-Versorgungsspannung VL (Digits) |
| STAT_VERS_VL_MAX | unsigned int | Maximalwert der Sensorversorgungsspannung vorne links |
| STAT_VERS_VL_MAX_EINH | string | Einheit der maximalen Sensor-Versorgungsspannung VL (Digits) |
| STAT_VERS_VR_MIN | unsigned int | Minimalwert der Sensorversorgungsspannung vorne rechts |
| STAT_VERS_VR_MIN_EINH | string | Einheit der minimalen Sensor-Versorgungsspannung VR (Digits) |
| STAT_VERS_VR_MAX | unsigned int | Maximalwert der Sensorversorgungsspannung vorne rechts |
| STAT_VERS_VR_MAX_EINH | string | Einheit der maximalen Sensor-Versorgungsspannung VR (Digits) |
| STAT_VERS_HL_MIN | unsigned int | Minimalwert der Sensorversorgungsspannung hinten links |
| STAT_VERS_HL_MIN_EINH | string | Einheit der minimalen Sensor-Versorgungsspannung HL (Digits) |
| STAT_VERS_HL_MAX | unsigned int | Maximalwert der Sensorversorgungsspannung hinten links |
| STAT_VERS_HL_MAX_EINH | string | Einheit der maximalen Sensor-Versorgungsspannung HL (Digits) |
| STAT_VERS_HR_MIN | unsigned int | Minimalwert der Sensorversorgungsspannung hinten rechts |
| STAT_VERS_HR_MIN_EINH | string | Einheit der minimalen Sensor-Versorgungsspannung HR (Digits) |
| STAT_VERS_HR_MAX | unsigned int | Maximalwert der Sensorversorgungsspannung hinten rechts |
| STAT_VERS_HR_MAX_EINH | string | Einheit der maximalen Sensor-Versorgungsspannung HR (Digits) |
| STAT_EDCS_L_MIN | unsigned int | Minimalwert der EDCS-Spannung am linken Strang |
| STAT_EDCS_L_MIN_EINH | string | Einheit der minimalen EDCS-Spannung links (Digits) |
| STAT_EDCS_L_MAX | unsigned int | Maximalwert der EDCS-Spannung am linken Strang |
| STAT_EDCS_L_MAX_EINH | string | Einheit der maximalen EDCS-Spannung links (Digits) |
| STAT_EDCS_R_MIN | unsigned int | Minimalwert der EDCS-Spannung am rechten Strang |
| STAT_EDCS_R_MIN_EINH | string | Einheit der minimalen EDCS-Spannung rechts (Digits) |
| STAT_EDCS_R_MAX | unsigned int | Maximalwert der EDCS-Spannung am rechten Strang |
| STAT_EDCS_R_MAX_EINH | string | Einheit der maximalen EDCS-Spannung rechts (Digits) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-endtest"></a>
### _STEUERN_ENDTEST

Einstellungen für den Endtest KWP 2000: $3B ReadDataByLocalIdentifier $32 Einstellungen für den Endtest schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KOMP | unsigned char | Komponente Zur Unterscheidung der unterschiedlichen Komponenten, die verändert werden sollen 0x00 Voltage Tracker 0x01 EDCS-Leitungen 0x02 Fensterwatchdog im Spannungsregler TLE6368 0x03 Externer Watchdog 0x04 EEPROM-Check |
| PARAM | unsigned char | Parameter Parameter zur Einstellung der ausgewählten Komponente Komponente: Voltage Tracker 0x00 alle Tracker (VL, VR, HL, HR) OFF Bit 0: VL ON Bit 1: VR ON Bit 2: HL ON Bit 3: HR ON Komponente: EDCS-Leitungen 0x00 EDCS_R und EDCS_L disable 0x01 EDCS_L enable 0x02 EDCS_R enable 0x03 EDCS_L und EDCS_R enable Komponente: Fensterwatchdoch kein weiterer Parameter nötig Komponente: externer Watchdog 0x00 korrekte Triggerung des Watchdogs 0x01 Fehltriggerung durch /C_LOW_TRIG 0x02 Fehltriggerung durch C_HIGH_TRIG 0x03 Fehltriggerung durch /C_LOW_TRIG und C_HIGH_TRIG |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dummy"></a>
### _DUMMY

Zur Definition eines beliebigen Jobs Freie Auswahl eines Single Frames interner TEMIC-Job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| JOB_LAENGE | char | soll: Anzahl der Parameter + 1 kann frei gewählt werden (0...21) |
| SG_ADRESSE | char | soll: Adresse des Ziel-SG (VDM: 0x39) |
| TESTER_ADRESSE | char | soll: Adresse des Testers (normal: 0xF1) |
| JOB_NR | char | soll: Job nach KWP2000 |
| PARAMETER_1 | char | Freie Wahl |
| PARAMETER_2 | char | Freie Wahl |
| PARAMETER_3 | char | Freie Wahl |
| PARAMETER_4 | char | Freie Wahl |
| PARAMETER_5 | char | Freie Wahl |
| PARAMETER_6 | char | Freie Wahl |
| PARAMETER_7 | char | Freie Wahl |
| PARAMETER_8 | char | Freie Wahl |
| PARAMETER_9 | char | Freie Wahl |
| PARAMETER_10 | char | Freie Wahl |
| PARAMETER_11 | char | Freie Wahl |
| PARAMETER_12 | char | Freie Wahl |
| PARAMETER_13 | char | Freie Wahl |
| PARAMETER_14 | char | Freie Wahl |
| PARAMETER_15 | char | Freie Wahl |
| PARAMETER_16 | char | Freie Wahl |
| PARAMETER_17 | char | Freie Wahl |
| PARAMETER_18 | char | Freie Wahl |
| PARAMETER_19 | char | Freie Wahl |
| PARAMETER_20 | char | Freie Wahl |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dummy-long"></a>
### _DUMMY_LONG

Zur Definition eines beliebigen Jobs interner TEMIC-Job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Job-Länge (SID + Daten) Byte 1              : SG-Adresse Byte 2              : Tester-Adresse Byte 3              : SID Byte 4..Byte x      : Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
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
- [HARTTEXTE](#table-harttexte) (14 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (52 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (52 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (21 × 9)
- [FARTTYP](#table-farttyp) (42 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (16 × 2)
- [HORTTEXTE](#table-horttexte) (52 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HUMWELTMATRIX](#table-humweltmatrix) (52 × 5)
- [HUMWELTTEXTE](#table-humwelttexte) (21 × 9)
- [HARTTYP](#table-harttyp) (42 × 5)
- [HARTTEXTEINDIVIDUELL](#table-harttexteindividuell) (16 × 2)
- [IORTTEXTE](#table-iorttexte) (25 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (25 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (9 × 9)
- [IARTTYP](#table-iarttyp) (25 × 5)
- [IARTTEXTEINDIVIDUELL](#table-iarttexteindividuell) (16 × 2)
- [UMWELT_ALLG](#table-umwelt-allg) (1 × 5)
- [UMWELT_VERSCHRAENKUNG](#table-umwelt-verschraenkung) (1 × 7)
- [ABGLEICH_HOEHENSTAND](#table-abgleich-hoehenstand) (6 × 2)
- [DAEMPFERPROGRAMM](#table-daempferprogramm) (7 × 2)

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

Dimensions: 52 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x630C | Steuergerät interner Fehler |
| 0x630D | Steuergerät nicht codiert |
| 0x630E | Steuergerät nicht abgeglichen |
| 0x630F | HSensor Signal VL |
| 0x6310 | HSensor Signal VR |
| 0x6311 | HSensor Signal HL |
| 0x6312 | HSensor Signal HR |
| 0x6313 | HSensor Versorgung VL |
| 0x6314 | HSensor Versorgung VR |
| 0x6315 | HSensor Versorgung HL |
| 0x6316 | HSensor Versorgung HR |
| 0x6317 | Verschränkungsplausibilität |
| 0x6318 | Enable Links |
| 0x6319 | Enable Rechts |
| 0x631A | Fehler Satellit VL |
| 0x631B | Fehler Satellit VR |
| 0x631C | Fehler Satellit HL |
| 0x631D | Fehler Satellit HR |
| 0x631E | Spannungsversorgung |
| 0xD747 | PT-CAN Kommunikationsfehler |
| 0xD74B | F-CAN Kommunikationsfehler |
| 0xD74C | FlexRay Bus Error Transceiver |
| 0xD74F | FlexRay Synchronisation (Controller) |
| 0xD754 | Botschaft (Kilometerstand/Reichweite, 0x330) |
| 0xD755 | Botschaft (Außentemperatur/Relativzeit, 0x310) |
| 0xD756 | Botschaft (Geschwindigkeit PT-CAN, 0x1A0) |
| 0xD757 | Botschaft (Status DSC PT-CAN, 0x19E) |
| 0xD758 | Botschaft (Bedienung Taster Vertikaldynamik, 0x28C) |
| 0xD759 | Botschaft (Motordaten, 0x1D0) |
| 0xD75A | Botschaft (Klemmenstatus, 0x130) |
| 0xD75B | Botschaft (Drehmoment 3 PT-CAN, 0x0AA) |
| 0xD75C | Botschaft (Getriebedaten, 0x0BA) |
| 0xD75D | Botschaft (Status ARS-Modul, 0x1AC) |
| 0xD75E | Botschaft (Status Funkschlüssel, 0x23A) |
| 0xD75F | Botschaft (Netzwerkmanagement PT-CAN, 0x4B9) |
| 0xD760 | Botschaft (Lenkradwinkel oben 2 F-CAN, 0x0C9) |
| 0xD761 | Botschaft (Querdynamik ARS VDM, 0x0F7) |
| 0xD762 | Botschaft (Austausch AFS DSC, 0x118) |
| 0xD763 | Botschaft (Lenkradwinkel oben F-CAN, 0x0C8) |
| 0xD764 | Botschaft (Radgeschwindigkeit F-CAN, 0x0CE) |
| 0xD765 | Botschaft (CLU Status VDA, 0x165) |
| 0xD766 | Botschaft (CLU1 VDA, 0x0D8) |
| 0xD767 | Botschaft (CLU2 VDA, 0x0E3) |
| 0xD768 | Botschaft (Status EDCS VL) |
| 0xD769 | Botschaft (Status EDCS VR) |
| 0xD76A | Botschaft (Status EDCS HL) |
| 0xD76B | Botschaft (Status EDCS HR) |
| 0xD76C | Botschaft (Netzwerkmanagement FlexRay) |
| 0xD76D | Botschaft (Sensor Daten ROSE, 0x12A) |
| 0xD76E | Botschaft (Lenkradwinkel Oben 2 F-CAN, 0x0C9) |
| 0xD76F | Botschaft (Geschwindigkeit PT-CAN, 0x1A0) |
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

Dimensions: 52 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x630C | 0x02 | 0x01 | 0x13 | 0x06 |
| 0x630D | Umwelt_allg | 0x05 | 0x14 | - |
| 0x630E | Umwelt_allg | 0x05 | 0x14 | - |
| 0x630F | Umwelt_allg | 0x07 | 0x14 | - |
| 0x6310 | Umwelt_allg | 0x07 | 0x14 | - |
| 0x6311 | Umwelt_allg | 0x07 | 0x14 | - |
| 0x6312 | Umwelt_allg | 0x07 | 0x14 | - |
| 0x6313 | Umwelt_allg | 0x08 | 0x14 | - |
| 0x6314 | Umwelt_allg | 0x08 | 0x14 | - |
| 0x6315 | Umwelt_allg | 0x08 | 0x14 | - |
| 0x6316 | Umwelt_allg | 0x08 | 0x14 | - |
| 0x6317 | 0x01 | 0x04 | 0x03 | Umwelt_Verschraenkung |
| 0x6318 | Umwelt_allg | 0x0e | 0x14 | - |
| 0x6319 | Umwelt_allg | 0x0e | 0x14 | - |
| 0x631A | Umwelt_allg | 0x0f | 0x14 | - |
| 0x631B | Umwelt_allg | 0x10 | 0x14 | - |
| 0x631C | Umwelt_allg | 0x11 | 0x14 | - |
| 0x631D | Umwelt_allg | 0x12 | 0x14 | - |
| 0x631E | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD747 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD74B | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD74C | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD74F | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD754 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD755 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD756 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD757 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD758 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD759 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75A | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75B | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75C | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75D | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75E | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75F | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD760 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD761 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD762 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD763 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD764 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD765 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD766 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD767 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD768 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD769 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76A | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76B | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76C | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76D | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76E | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76F | Umwelt_allg | 0x05 | 0x14 | - |
| 0xFFFF | - | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 21 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | uKL30g | V | - | unsigned char | - | 0.1 | 1 | - |
| 0x02 | Relativzeit | - | high | signed long | - | 1 | 1 | - |
| 0x03 | Aussentemperatur | °C | - | unsigned char | - | 0.5 | 1 | -40 |
| 0x04 | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1 | 1 | - |
| 0x05 | Motorstatus | - | - | unsigned char | - | 1 | 1 | - |
| 0x06 | Fehlerdetail | - | high | signed long | - | 1 | 1 | - |
| 0x07 | Sensorsignal | mm/s | - | unsigned char | - | 2 | 1 | -256 |
| 0x08 | Sensorspannung | V | - | unsigned char | - | 0.1 | 1 | - |
| 0x09 | Lenkradwinkel | - | - | unsigned char | - | 1 | 1 | - |
| 0x0a | Sensorsignal_VL | mm/s | - | unsigned char | - | 2 | 1 | -256 |
| 0x0b | Sensorsignal_VR | mm/s | - | unsigned char | - | 2 | 1 | -256 |
| 0x0c | Sensorsignal_HL | mm/s | - | unsigned char | - | 2 | 1 | -256 |
| 0x0d | Sensorsignal_HR | mm/s | - | unsigned char | - | 2 | 1 | -256 |
| 0x0e | Spannung_Enable | V | - | unsigned char | - | 0.1 | 1 | - |
| 0x0f | FehlerEDCS_VL | - | - | unsigned char | - | 1 | 1 | - |
| 0x10 | FehlerEDCS_VR | - | - | unsigned char | - | 1 | 1 | - |
| 0x11 | FehlerEDCS_HL | - | - | unsigned char | - | 1 | 1 | - |
| 0x12 | FehlerEDCS_HR | - | - | unsigned char | - | 1 | 1 | - |
| 0x13 | unused_byte | - | - | unsigned char | - | 1 | 1 | - |
| 0x14 | unused_word | - | high | unsigned int | - | 1 | 1 | - |
| 0xFF | unbekannte Umweltbedingung | - | - | unsigned char | - | 1 | 1 | - |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 42 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x630C | 0xFFFF | 0xFFFF | 0x0011 | 0x0012 |
| 0x630D | 0x0008 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x630E | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x6318 | 0x0008 | 0xFFFF | 0x0002 | 0x0001 |
| 0x6319 | 0x0008 | 0xFFFF | 0x0002 | 0x0001 |
| 0x631A | 0x0008 | 0x0004 | 0x0014 | 0xFFFF |
| 0x631B | 0x0008 | 0x0004 | 0x0014 | 0xFFFF |
| 0x631C | 0x0008 | 0x0004 | 0x0014 | 0xFFFF |
| 0x631D | 0x0008 | 0x0004 | 0x0014 | 0xFFFF |
| 0xD747 | 0xFFFF | 0x0004 | 0xFFFF | 0xFFFF |
| 0xD74B | 0xFFFF | 0x0004 | 0xFFFF | 0xFFFF |
| 0xD74C | 0xFFFF | 0xFFFF | 0x001A | 0x0019 |
| 0xD74F | 0xFFFF | 0x001B | 0xFFFF | 0xFFFF |
| 0xD754 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD755 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD756 | 0x0018 | 0x0017 | 0x0016 | 0xFFFF |
| 0xD757 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD758 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD759 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75A | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75B | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75C | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75D | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75E | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75F | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD760 | 0x0018 | 0x0017 | 0x0016 | 0xFFFF |
| 0xD761 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD762 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD763 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD764 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD765 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD766 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD767 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD768 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD769 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD76A | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD76B | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD76C | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD76D | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD76E | 0xFFFF | 0xFFFF | 0xFFFF | 0x0015 |
| 0xD76F | 0xFFFF | 0xFFFF | 0xFFFF | 0x0015 |
| default | 0x0008 | 0x0004 | 0x0002 | 0x0001 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 16 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0004 | kein Signal oder Wert |
| 0x0008 | unplausibles Signal |
| 0x0011 | kritischer Fehler |
| 0x0012 | EEPROM |
| 0x0014 | Störung Satellit |
| 0x0015 | Signal oder Wert nicht belegt |
| 0x0016 | Fehler Alive Zähler |
| 0x0017 | Timeout |
| 0x0018 | Checksummenfehler |
| 0x0019 | Transceiver links |
| 0x001A | Transceiver rechts |
| 0x001B | rot |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 52 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x630C | Steuergerät interner Fehler |
| 0x630D | Steuergerät nicht codiert |
| 0x630E | Steuergerät nicht abgeglichen |
| 0x630F | HSensor Signal VL |
| 0x6310 | HSensor Signal VR |
| 0x6311 | HSensor Signal HL |
| 0x6312 | HSensor Signal HR |
| 0x6313 | HSensor Versorgung VL |
| 0x6314 | HSensor Versorgung VR |
| 0x6315 | HSensor Versorgung HL |
| 0x6316 | HSensor Versorgung HR |
| 0x6317 | Verschränkungsplausibilität |
| 0x6318 | Enable Links |
| 0x6319 | Enable Rechts |
| 0x631A | Fehler Satellit VL |
| 0x631B | Fehler Satellit VR |
| 0x631C | Fehler Satellit HL |
| 0x631D | Fehler Satellit HR |
| 0x631E | Spannungsversorgung |
| 0xD747 | PT-CAN Kommunikationsfehler |
| 0xD74B | F-CAN Kommunikationsfehler |
| 0xD74C | FlexRay Bus Error Transceiver |
| 0xD74F | FlexRay Synchronisation (Controller) |
| 0xD754 | Botschaft (Kilometerstand/Reichweite, 0x330) |
| 0xD755 | Botschaft (Außentemperatur/Relativzeit, 0x310) |
| 0xD756 | Botschaft (Geschwindigkeit PT-CAN, 0x1A0) |
| 0xD757 | Botschaft (Status DSC PT-CAN, 0x19E) |
| 0xD758 | Botschaft (Bedienung Taster Vertikaldynamik, 0x28C) |
| 0xD759 | Botschaft (Motordaten, 0x1D0) |
| 0xD75A | Botschaft (Klemmenstatus, 0x130) |
| 0xD75B | Botschaft (Drehmoment 3 PT-CAN, 0x0AA) |
| 0xD75C | Botschaft (Getriebedaten, 0x0BA) |
| 0xD75D | Botschaft (Status ARS-Modul, 0x1AC) |
| 0xD75E | Botschaft (Status Funkschlüssel, 0x23A) |
| 0xD75F | Botschaft (Netzwerkmanagement PT-CAN, 0x4B9) |
| 0xD760 | Botschaft (Lenkradwinkel oben 2 F-CAN, 0x0C9) |
| 0xD761 | Botschaft (Querdynamik ARS VDM, 0x0F7) |
| 0xD762 | Botschaft (Austausch AFS DSC, 0x118) |
| 0xD763 | Botschaft (Lenkradwinkel oben F-CAN, 0x0C8) |
| 0xD764 | Botschaft (Radgeschwindigkeit F-CAN, 0x0CE) |
| 0xD765 | Botschaft (CLU Status VDA, 0x165) |
| 0xD766 | Botschaft (CLU1 VDA, 0x0D8) |
| 0xD767 | Botschaft (CLU2 VDA, 0x0E3) |
| 0xD768 | Botschaft (Status EDCS VL) |
| 0xD769 | Botschaft (Status EDCS VR) |
| 0xD76A | Botschaft (Status EDCS HL) |
| 0xD76B | Botschaft (Status EDCS HR) |
| 0xD76C | Botschaft (Netzwerkmanagement FlexRay) |
| 0xD76D | Botschaft (Sensor Daten ROSE, 0x12A) |
| 0xD76E | Botschaft (Lenkradwinkel Oben 2 F-CAN, 0x0C9) |
| 0xD76F | Botschaft (Geschwindigkeit PT-CAN, 0x1A0) |
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
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 52 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x630C | 0x02 | 0x01 | 0x13 | 0x06 |
| 0x630D | Umwelt_allg | 0x05 | 0x14 | - |
| 0x630E | Umwelt_allg | 0x05 | 0x14 | - |
| 0x630F | Umwelt_allg | 0x07 | 0x14 | - |
| 0x6310 | Umwelt_allg | 0x07 | 0x14 | - |
| 0x6311 | Umwelt_allg | 0x07 | 0x14 | - |
| 0x6312 | Umwelt_allg | 0x07 | 0x14 | - |
| 0x6313 | Umwelt_allg | 0x08 | 0x14 | - |
| 0x6314 | Umwelt_allg | 0x08 | 0x14 | - |
| 0x6315 | Umwelt_allg | 0x08 | 0x14 | - |
| 0x6316 | Umwelt_allg | 0x08 | 0x14 | - |
| 0x6317 | 0x01 | 0x04 | 0x03 | Umwelt_Verschraenkung |
| 0x6318 | Umwelt_allg | 0x0e | 0x14 | - |
| 0x6319 | Umwelt_allg | 0x0e | 0x14 | - |
| 0x631A | Umwelt_allg | 0x0f | 0x14 | - |
| 0x631B | Umwelt_allg | 0x10 | 0x14 | - |
| 0x631C | Umwelt_allg | 0x11 | 0x14 | - |
| 0x631D | Umwelt_allg | 0x12 | 0x14 | - |
| 0x631E | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD747 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD74B | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD74C | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD74F | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD754 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD755 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD756 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD757 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD758 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD759 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75A | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75B | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75C | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75D | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75E | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD75F | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD760 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD761 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD762 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD763 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD764 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD765 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD766 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD767 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD768 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD769 | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76A | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76B | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76C | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76D | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76E | Umwelt_allg | 0x05 | 0x14 | - |
| 0xD76F | Umwelt_allg | 0x05 | 0x14 | - |
| 0xFFFF | - | - | - | - |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 21 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | uKL30g | V | - | unsigned char | - | 0.1 | 1 | - |
| 0x02 | Relativzeit | - | high | signed long | - | 1 | 1 | - |
| 0x03 | Aussentemperatur | °C | - | unsigned char | - | 0.5 | 1 | -40 |
| 0x04 | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1 | 1 | - |
| 0x05 | Motorstatus | - | - | unsigned char | - | 1 | 1 | - |
| 0x06 | Fehlerdetail | - | high | signed long | - | 1 | 1 | - |
| 0x07 | Sensorsignal | mm/s | - | unsigned char | - | 2 | 1 | -256 |
| 0x08 | Sensorspannung | V | - | unsigned char | - | 0.1 | 1 | - |
| 0x09 | Lenkradwinkel | - | - | unsigned char | - | 1 | 1 | - |
| 0x0a | Sensorsignal_VL | mm/s | - | unsigned char | - | 2 | 1 | -256 |
| 0x0b | Sensorsignal_VR | mm/s | - | unsigned char | - | 2 | 1 | -256 |
| 0x0c | Sensorsignal_HL | mm/s | - | unsigned char | - | 2 | 1 | -256 |
| 0x0d | Sensorsignal_HR | mm/s | - | unsigned char | - | 2 | 1 | -256 |
| 0x0e | Spannung_Enable | V | - | unsigned char | - | 0.1 | 1 | - |
| 0x0f | FehlerEDCS_VL | - | - | unsigned char | - | 1 | 1 | - |
| 0x10 | FehlerEDCS_VR | - | - | unsigned char | - | 1 | 1 | - |
| 0x11 | FehlerEDCS_HL | - | - | unsigned char | - | 1 | 1 | - |
| 0x12 | FehlerEDCS_HR | - | - | unsigned char | - | 1 | 1 | - |
| 0x13 | unused_byte | - | - | unsigned char | - | 1 | 1 | - |
| 0x14 | unused_word | - | high | unsigned int | - | 1 | 1 | - |
| 0xFF | unbekannte Umweltbedingung | - | - | unsigned char | - | 1 | 1 | - |

<a id="table-harttyp"></a>
### HARTTYP

Dimensions: 42 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x630C | 0xFFFF | 0xFFFF | 0x0011 | 0x0012 |
| 0x630D | 0x0008 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x630E | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x6318 | 0x0008 | 0xFFFF | 0x0002 | 0x0001 |
| 0x6319 | 0x0008 | 0xFFFF | 0x0002 | 0x0001 |
| 0x631A | 0x0008 | 0x0004 | 0x0014 | 0xFFFF |
| 0x631B | 0x0008 | 0x0004 | 0x0014 | 0xFFFF |
| 0x631C | 0x0008 | 0x0004 | 0x0014 | 0xFFFF |
| 0x631D | 0x0008 | 0x0004 | 0x0014 | 0xFFFF |
| 0xD747 | 0xFFFF | 0x0004 | 0xFFFF | 0xFFFF |
| 0xD74B | 0xFFFF | 0x0004 | 0xFFFF | 0xFFFF |
| 0xD74C | 0xFFFF | 0xFFFF | 0x001A | 0x0019 |
| 0xD74F | 0xFFFF | 0x001B | 0xFFFF | 0xFFFF |
| 0xD754 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD755 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD756 | 0x0018 | 0x0017 | 0x0016 | 0xFFFF |
| 0xD757 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD758 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD759 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75A | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75B | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75C | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75D | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75E | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD75F | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD760 | 0x0018 | 0x0017 | 0x0016 | 0xFFFF |
| 0xD761 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD762 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD763 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD764 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD765 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD766 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD767 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD768 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD769 | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD76A | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD76B | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD76C | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD76D | 0x0018 | 0x0017 | 0x0016 | 0x0015 |
| 0xD76E | 0xFFFF | 0xFFFF | 0xFFFF | 0x0015 |
| 0xD76F | 0xFFFF | 0xFFFF | 0xFFFF | 0x0015 |
| default | 0x0008 | 0x0004 | 0x0002 | 0x0001 |

<a id="table-harttexteindividuell"></a>
### HARTTEXTEINDIVIDUELL

Dimensions: 16 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0004 | kein Signal oder Wert |
| 0x0008 | unplausibles Signal |
| 0x0011 | kritischer Fehler |
| 0x0012 | EEPROM |
| 0x0014 | Störung Satellit |
| 0x0015 | Signal oder Wert nicht belegt |
| 0x0016 | Fehler Alive Zähler |
| 0x0017 | Timeout |
| 0x0018 | Checksummenfehler |
| 0x0019 | Transceiver links |
| 0x001A | Transceiver rechts |
| 0x001B | rot |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 25 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5D0C | Unterspannung / Überspannung |
| 0x5D0D | interner Fehler |
| 0x5D0E | FlexRay Controller |
| 0x5D0F | FlexRay |
| 0x5D10 | EEPROM |
| 0x5D11 | PT-CAN Geschwindigkeit |
| 0x5D12 | PT-CAN Drehmoment 3 |
| 0x5D13 | PT-CAN Getriebedaten |
| 0x5D14 | PT-CAN Status DSC |
| 0x5D15 | F-CAN Austausch AFS DSC |
| 0x5D16 | F-CAN Lenkradwinkel oben 2 |
| 0x5D17 | F-CAN CLU1 VDA |
| 0x5D18 | F-CAN CLU2 VDA |
| 0x5D19 | F-CAN Querdynamik ARS VDM |
| 0x5D1A | F-CAN Sensor Daten ROSE |
| 0x5D20 | Eckplausibilisierung VL |
| 0x5D21 | Eckplausibilisierung VR |
| 0x5D22 | Eckplausibilisierung HL |
| 0x5D23 | Eckplausibilisierung HR |
| 0x5D24 | Achsplausi. Höhenstand links |
| 0x5D25 | Achsplausi. Höhenstand rechts |
| 0x5D26 | Achsplausi. Radbeschl. links |
| 0x5D27 | Achsplausi. Radbeschl. rechts |
| 0x5D28 | CLU Status VDA |
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

Dimensions: 25 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x5D0C | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D0D | 0x02 | 0x01 | 0x07 | 0x06 |
| 0x5D0E | 0x02 | 0x01 | 0x07 | 0x06 |
| 0x5D0F | 0x02 | 0x01 | 0x07 | 0x06 |
| 0x5D10 | 0x02 | 0x01 | 0x07 | 0x06 |
| 0x5D11 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D12 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D13 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D14 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D15 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D16 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D17 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D18 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D19 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D1A | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D20 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D21 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D22 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D23 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D24 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D25 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D26 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D27 | Umwelt_allg | 0x05 | 0x08 | - |
| 0x5D28 | Umwelt_allg | 0x05 | 0x08 | - |
| 0xFFFF | - | - | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 9 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | uKL30g | V | - | unsigned char | - | 0.1 | 1 | - |
| 0x02 | Relativzeit | - | high | signed long | - | 1 | 1 | - |
| 0x03 | Aussentemperatur | °C | - | unsigned char | - | 0.5 | 1 | -40 |
| 0x04 | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1 | 1 | - |
| 0x05 | Motorstatus | - | - | unsigned char | - | 1 | 1 | - |
| 0x06 | Fehlerdetail | - | high | signed long | - | 1 | 1 | - |
| 0x07 | unused_byte | - | - | unsigned char | - | 1 | 1 | - |
| 0x08 | unused_word | - | high | unsigned int | - | 1 | 1 | - |
| 0xff | unbekannte Umwelt | - | - | unsigned char | - | 1 | 1 | - |

<a id="table-iarttyp"></a>
### IARTTYP

Dimensions: 25 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x5D0C | 0xFFFF | 0xFFFF | 0x0006 | 0x0005 |
| 0x5D0D | 0xFFFF | 0xFFFF | 0xFFFF | 0x0007 |
| 0x5D0E | 0xFFFF | 0xFFFF | 0xFFFF | 0x0008 |
| 0x5D0F | 0xFFFF | 0xFFFF | 0xFFFF | 0x0007 |
| 0x5D10 | 0xFFFF | 0xFFFF | 0xFFFF | 0x0007 |
| 0x5D11 | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x5D12 | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x5D13 | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x5D14 | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x5D15 | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x5D16 | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x5D17 | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x5D18 | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x5D19 | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x5D1A | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0x5D20 | 0x0004 | 0xFFFF | 0x000E | 0x000D |
| 0x5D21 | 0x0004 | 0xFFFF | 0x000E | 0x000D |
| 0x5D22 | 0x0004 | 0xFFFF | 0x000E | 0x000D |
| 0x5D23 | 0x0004 | 0xFFFF | 0x000E | 0x000D |
| 0x5D24 | 0x0004 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5D25 | 0x0004 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5D26 | 0x0004 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5D27 | 0x0004 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5D28 | 0x000C | 0x000B | 0x000A | 0x0009 |
| 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |

<a id="table-iarttexteindividuell"></a>
### IARTTEXTEINDIVIDUELL

Dimensions: 16 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0003 | kein Signal oder Wert |
| 0x0004 | unplausibles Signal |
| 0x0005 | Überspannung |
| 0x0006 | Unterspannung |
| 0x0007 | Fehler |
| 0x0008 | gelb |
| 0x0009 | Signal oder Wert nicht belegt |
| 0x000A | Fehler Alive Zähler |
| 0x000B | Timeout |
| 0x000C | Checksummenfehler |
| 0x000D | Schwelle PhiP |
| 0x000E | Schwelle Plausibilität |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-umwelt-allg"></a>
### UMWELT_ALLG

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x02 | 0x01 | 0x04 | 0x03 |

<a id="table-umwelt-verschraenkung"></a>
### UMWELT_VERSCHRAENKUNG

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d | 0x14 |

<a id="table-abgleich-hoehenstand"></a>
### ABGLEICH_HOEHENSTAND

Dimensions: 6 rows × 2 columns

| BIT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Kurzschluss KL30 |
| 0x02 | Kurzschluss KL31 / offene Leitung |
| 0x10 | Spannung Sensorversorgung zu hoch |
| 0x20 | Spannung Sensorversorgung zu niedrig |
| 0xXY | unbekannter Fehler |

<a id="table-daempferprogramm"></a>
### DAEMPFERPROGRAMM

Dimensions: 7 rows × 2 columns

| BIT | TEXT |
| --- | --- |
| 0x00 | Komfort |
| 0x01 | Sport |
| 0x02 | Komfort mit Ersatzwerten |
| 0x03 | Sport mit Ersatzwerten |
| 0x04 | Festbestromung |
| 0x05 | Nullbestromung |
| 0xXY | unbekanntes Dämpferprogramm |
