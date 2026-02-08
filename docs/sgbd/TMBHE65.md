# TMBHE65.prg

- Jobs: [74](#jobs)
- Tables: [22](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Tuermodul Beifahrertuer hinten E65 |
| ORIGIN | BMW TI-430 Gerd Huber |
| REVISION | 3.010 |
| AUTHOR | LEAR EE K. Fuchs, BMW TI-430 R. Gall, LEAR EE C. Stagl, LEAR EE S. C: Schmidt |
| COMMENT | N/A |
| PACKAGE | 1.26 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
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
- [C_C_PROG](#job-c-c-prog) - Codierdaten schreiben fuer TM KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [READ_SHADOW](#job-read-shadow) - Lese kompletten Shadow-Speicher aus KWP2000: $22    ReadDataByCommonIdentifier $2000  dtcShadowMemory Modus  : Default
- [CODIERDATEN_MODUL_LESEN](#job-codierdaten-modul-lesen) - Auslesen der Codierdaten Modul !!! nur fuer Tuermodule !!! KWP2000: $22 ReadDataByCommonIdentifier $3100 Codierdaten Modul Modus  : Default
- [STATUS_INPUTS](#job-status-inputs) - Auslesen der Stati aller Hall-Eingaenge KWP2000: $30 InputOutputControlByLocalIdentifier $07 all digital inputs $01 ReportCurrentState Modus  : Default
- [STATUS_DIAG](#job-status-diag) - Auslesen der Stati aller Diagnose Eingaenge (Treiber zu Prozessor) KWP2000: $30 InputOutputControlByLocalIdentifier $02 all diagnostic inputs $01 ReportCurrentState Modus  : Default
- [STATUS_OUTPUT](#job-status-output) - Auslesen der Stati aller Ausgaenge (Prozessor zu Treiber) KWP2000: $30 InputOutputControlByLocalIdentifier $03 all outputs $01 ReportCurrentState Modus  : Default
- [STATUS_SWITCH_BLOCK](#job-status-switch-block) - Auslesen der Stati aller Schalterblock Signale (K-Bus) KWP2000: $30 InputOutputControlByLocalIdentifier $05 all K-Bus inputs $01 ReportCurrentState Modus  : Default
- [STATUS_FLAGS](#job-status-flags) - Auslesen der internen Software-Flags KWP2000: $30 InputOutputControlByLocalIdentifier $06 all internal flags $01 ReportCurrentState Modus  : Default
- [STATUS_DIGITAL](#job-status-digital) - Auslesen der Stati aller digitaler Signale KWP2000: $30 InputOutputControlByLocalIdentifier $01 all digital signals $01 ReportCurrentState Modus  : Default
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern von jedem digitalen Signal KWP2000: $30 InputOutputControlByLocalIdentifier $01 digital signals $07 ShortTermAdjustment Modus  : Default
- [STEUERN_ANALOG](#job-steuern-analog) - Ansteuern von jedem digitalen Signal KWP2000: $30 InputOutputControlByLocalIdentifier $10 digital signals $07 ShortTermAdjustment Modus  : Default
- [STEUERN_ENDE](#job-steuern-ende) - Ansteuern von jedem digitalen Signal KWP2000: $30 InputOutputControlByLocalIdentifier $01 digital signals $00 returnControlToECU Modus  : Default
- [C_CHECKSUMME](#job-c-checksumme) - Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob
- [STATUS_CFL](#job-status-cfl) - Auslesen der Stati von CFL KWP2000: $31 startRoutineByLocalIdentifier Modus  : Default
- [STEUERN_CFL](#job-steuern-cfl) - Steuern der CFL-modul KWP2000: $31 startRoutineByLocalIdentifier Modus  : Default
- [STEUERN_ER](#job-steuern-er) - Tuermodul ZV Entriegeln !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $21 DiagZVER Modus  : Default
- [STEUERN_VR](#job-steuern-vr) - Tuermodul ZV Verriegeln !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $22 DiagZVVR Modus  : Default
- [STEUERN_ZS](#job-steuern-zs) - Tuermodul ZV Sichern !!! ab i6.121 !!! Achtung: bei Diagnose-Ende nach Timeout bleibt TM gesichert!! Diagnose ist dann nicht mehr möglich (Security-Access denied) Diagnose muß bis Entriegeln aufrechterhalten werden!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $23 DiagZVZS Modus  : Default
- [STATUS_ANALOG](#job-status-analog) - Auslesen aller analoge Werte KWP2000: $30 InputOutputControlByLocalIdentifier $10 all analog values $01 ReportCurrentState Modus  : Default
- [STEUERN_COSI_EIN](#job-steuern-cosi-ein) - Coach-Door Sicherung einlegen !!! ab i6.121 mit Rolls Royce Kodierung !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $01 DiagCoSiOn Modus  : Default
- [STEUERN_COSI_AUS](#job-steuern-cosi-aus) - Coach-Door Sicherung auslegen !!! ab i6.121 mit Rolls Royce Kodierung !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $02 DiagCoSiOff Modus  : Default
- [STEUERN_EMF](#job-steuern-emf) - Steuern der EMF Ausgaenge fuer ZEIT mal 10ms !!! ab i6.121 mit Rolls Royce Kodierung !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $03 DiagEMF $xx EMF Aktivierung fuer $xx * 10ms Modus  : Default
- [STEUERN_SR1_UP](#job-steuern-sr1-up) - Sonnenrollo 1 rauf fuer ZEIT mal 10ms oder bis Anschlag !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $11 DiagSR1Up $xx SR1 Aktivierung fuer $xx * 10ms Modus  : Default
- [STEUERN_SR1_DOWN](#job-steuern-sr1-down) - Sonnenrollo 1 runter fuer ZEIT mal 10ms oder bis Anschlag !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $12 DiagSR1Down $xx SR1 Aktivierung fuer $xx * 10ms Modus  : Default
- [STEUERN_SR2_UP](#job-steuern-sr2-up) - Sonnenrollo 2 rauf fuer ZEIT mal 10ms oder bis Anschlag !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $13 DiagSR2Up $xx SR2 Aktivierung fuer $xx * 10ms Modus  : Default
- [STEUERN_SR2_DOWN](#job-steuern-sr2-down) - Sonnenrollo 1 runter fuer ZEIT mal 10ms oder bis Anschlag !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $14 DiagSR2Down $xx SR2 Aktivierung fuer $xx * 10ms Modus  : Default

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

<a id="job-c-c-prog"></a>
### C_C_PROG

Codierdaten schreiben fuer TM KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-shadow"></a>
### READ_SHADOW

Lese kompletten Shadow-Speicher aus KWP2000: $22    ReadDataByCommonIdentifier $2000  dtcShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Der Binaerbuffer hat folgenden Aufbau Byte 0              : Anzahl Info Eintraege Byte 1,usw          : Infoeintraege Rohformat |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-modul-lesen"></a>
### CODIERDATEN_MODUL_LESEN

Auslesen der Codierdaten Modul !!! nur fuer Tuermodule !!! KWP2000: $22 ReadDataByCommonIdentifier $3100 Codierdaten Modul Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PLANT_MODE | int | Modul im Fertigungsmode, Bereich: 0-1 |
| TRANSPORT_MODE | int | Modul im Transportmode, Bereich: 0-1 |
| SERVICE_MODE | int | Modul im Werkstattmode, Bereich: 0-1 |
| GENERIC | int | Generische Idents fuer CAN, Bereich: 0-1 |
| HW_TEST | int | Hardware Test Mode (nur LEAR!), Bereich: 0-1 |
| EEPROM | int | vorgehalten - wird nicht verwendet EEPROM Wert wird genommen, Bereich: 0-1 |
| ROM | int | vorgehalten - wird nicht verwendet ROM Default Wert wird genommen, Bereich: 0-1 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-inputs"></a>
### STATUS_INPUTS

Auslesen der Stati aller Hall-Eingaenge KWP2000: $30 InputOutputControlByLocalIdentifier $07 all digital inputs $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_S_SZ_VR | int | SNU2, Hallsensor Entriegeln im Schliesszylinder Fuer gueltiges Verriegeln muss auch SNU1 nach 10-1000ms gesetzt sein RR01: Signal S_COSI_VR = Status CoSi eingelegt |
| STAT_S_ZV_ER | int | Hallsensor Schloss verriegelt oder gesichert |
| STAT_S_SZ_ER | int | SNU1, Hallsensor Verriegeln im Schliesszylinder Fuer gueltiges Entriegeln muss auch SNU2 nach 10-1000ms gesetzt sein RR01: Signal S_COSI_TK = Status 2. Tuerkontakt |
| STAT_S_ZV_TK | int | Tuerkontakt |
| STAT_S_SCA_SPK | int | SCA-Sperrklinke = Vorrastsensor Schloss |
| STAT_S_ZV_TAG | int | Tueraussengriff gezogen RR: Signal S_ZV_TIG = Tuerinnengriff gezogen |
| STAT_S_FH_ZU | int | Lokaler Taster Fensterheber zu (nach oben) |
| STAT_S_FH_AUF | int | Lokaler Taster Fensterheber auf (nach unten) |
| STAT_S_SPARE_1 | int | Reserveeingang 1 |
| STAT_S_PE_BEREIT | int | Hallsensor EO-Antrieb in Bereitposition |
| STAT_S_SCA_BEREIT | int | Hallsensor SCA-Antrieb in Bereitposition |
| STAT_S_ZV_KISI | int | Hallsensor elektr. Kindersicherung eingelegt (unbenutzt) RR01 benutzt fuer diese Funktion Signal STAT_S_SZ_VR |
| STAT_S_SPARE_2 | int | Reserveeingang 2 |
| STAT_S_SPARE_3 | int | Reserveeingang 3 |
| STAT_S_SPARE_4 | int | Reserveeingang 4 |
| STAT_S_SPARE_5 | int | Reserveeingang 5 |
| STAT_S_FH_GESAMT | int | Kombinierter Status lokaler Taster Fensterheber 0 = aus, 1 = zu, 2 = auf, 3 = tipp |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-diag"></a>
### STATUS_DIAG

Auslesen der Stati aller Diagnose Eingaenge (Treiber zu Prozessor) KWP2000: $30 InputOutputControlByLocalIdentifier $02 all diagnostic inputs $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DIAG_SCASTS | int | Diag-Status SCA-Treiber |
| STAT_DIAG_PETOSTS | int | Diag-Status EO-Treiber |
| STAT_DIAG_MFOLDSTS | int | Diag-Status ASP Beiklappen |
| STAT_DIAG_VFSTS | int | Diag-Status FH Enable |
| STAT_DIAG_CMNSTS | int | Diag-Status ZV Common (ER/KISI) |
| STAT_DIAG_LOCKSTS | int | Diag-Status ZV (VR/ZS) |
| STAT_DIAG_ASP_COMLO | int | Diag-Status ASP Common low |
| STAT_DIAG_ASP_COMHI | int | Diag-Status ASP Common high |
| STAT_DIAG_LTSTS1 | int | Diag-Status Light Status 1 (SB_KL30/EST) |
| STAT_DIAG_FHENOUTPUT | int | Diag-Status FH-Enable Ausgang |
| STAT_DIAG_ASP_OVERLOAD | int | Diag-Status ASP Overload |
| STAT_DIAG_ASP_OPENLOAD | int | Diag-Status ASP Open Load |
| STAT_DIAG_ASP_POWER | int | Diag-Status ASP power line |
| STAT_DIAG_LTSTS2 | int | Diag-Status Lights 2 (ARV/AMB Light) |
| STAT_DIAG_PEST | int | Diag-Status not used |
| STAT_DIAG_ASP_TEMP | int | Diag-Status ASP Over Temperature |
| STAT_DIAG_ASP_HORLO | int | Diag-Status ASP Horizontal low |
| STAT_DIAG_ASP_HORHI | int | Diag-Status ASP Horizontal high |
| STAT_DIAG_ASP_VERLO | int | Diag-Status ASP Vertical low |
| STAT_DIAG_ASP_VERHI | int | Diag-Status ASP Vertical high |
| STAT_S_FH_HALL1 | int | Status Fensterheber Positions-Hallsensor 1 |
| STAT_S_FH_HALL2 | int | Status Fensterheber Positions-Hallsensor 2 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-output"></a>
### STATUS_OUTPUT

Auslesen der Stati aller Ausgaenge (Prozessor zu Treiber) KWP2000: $30 InputOutputControlByLocalIdentifier $03 all outputs $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_OUT_SB_KL30DISC | int | Schalterblock Kl. 30 |
| STAT_OUT_SBR_KL30DISC | int | Schalterblock hinten Kl. 30 (ab i6.121) |
| STAT_OUT_LMP_FRDISC | int | Tuerwarnleuchte/Einstiegshi |
| STAT_OUT_SCA_MOTDISC | int | ZV Motor SCA High-Side |
| STAT_OUT_SCA_MOTBRKDISC | int | ZV Motor SCA Low-Side |
| STAT_OUT_PE_MOTURZUDISC | int | ZV Motor EO High-Side |
| STAT_OUT_PE_MOTURZUBRKDISC | int | ZV Motor EO Low-Side |
| STAT_OUT_ZV_MOTCOMHIDISC | int | ZV Motor Enriegeln (COM) High-Side |
| STAT_OUT_ZV_MOTCOMLODISC | int | ZV Motor Entriegeln (COM) Low-Side |
| STAT_OUT_ZV_VRHIDISC | int | ZV Motor Verriegeln High-Side |
| STAT_OUT_ZV_VRLODISC | int | ZV Motor Verriegeln Low-Side |
| STAT_OUT_ZV_ZSHIDISC | int | ZV Motor Sichern High-Side |
| STAT_OUT_ZV_ZSLODISC | int | ZV Motor Sichern Low-Side |
| STAT_OUT_ZV_KISIHIDISC | int | ZV Motor KiSi High-Side |
| STAT_OUT_ZV_KISILODISC | int | ZV Motor KiSi Low-Side |
| STAT_OUT_WKUP_TIMER | int | Wake-Up-Timer Enable (bis i6.103) |
| STAT_OUT_PE_KL30DISC | int | Versorgung PE Kl. 30 (unbenutzt) |
| STAT_OUT_SR1_MOTAUFHIDISC | int | Sonnenrollo 1 Auf High-Side |
| STAT_OUT_SR1_MOTAUFLODISC | int | Sonnenrollo 1 Auf Low-Side |
| STAT_OUT_SR1_MOTZUHIDISC | int | Sonnenrollo 1 Zu High-Side |
| STAT_OUT_SR1_MOTZULODISC | int | Sonnenrollo 1 Zu Low-Side |
| STAT_OUT_SR2_MOTAUFHIDISC | int | Sonnenrollo 2 Auf High-Side |
| STAT_OUT_SR2_MOTAUFLODISC | int | Sonnenrollo 2 Auf Low-Side |
| STAT_OUT_SR2_MOTZUHIDISC | int | Sonnenrollo 2 Zu High-Side |
| STAT_OUT_SR2_MOTZULODISC | int | Sonnenrollo 2 Zu Low-Side |
| STAT_OUT_ASP_5VPOT | int | 5V fuer ASP-Potentiometer (Spiegelposition) |
| STAT_OUT_ASP_HZGDISC | int | ASP Heizung |
| STAT_OUT_ASP_MOTCOMHIDISC | int | SPI: ASP Common High-Side |
| STAT_OUT_ASP_MOTCOMLODISC | int | SPI: ASP Common Low-Side |
| STAT_OUT_ASP_MOTHORHIDISC | int | SPI: ASP Horz. High-Side |
| STAT_OUT_ASP_MOTHORLODISC | int | SPI: ASP Horz. Low-Side |
| STAT_OUT_ASP_MOTVERHIDISC | int | SPI: ASP Vert. High-Side |
| STAT_OUT_ASP_MOTVERLODISC | int | SPI: ASP Vert. Low-Side |
| STAT_OUT_ASP_DRIVER | int | Enable ASP-Treiber TLE6208 (INH) |
| STAT_OUT_ASP_MOT_CS | int | ASP-Treiber TLE6208 Chip select (für SPI) |
| STAT_OUT_ASPKLP_AUS_HS | int | ASP Beiklappen Ausgang 2 High-Side |
| STAT_OUT_ASPKLP_AUS_LS | int | ASP Beiklappen Ausgang 2 Low-Side |
| STAT_OUT_ASPKLP_EIN_HS | int | ASP Beiklappen Ausgang 1 High-Side |
| STAT_OUT_ASPKLP_EIN_LS | int | ASP Beiklappen Ausgang 1 Low-Side |
| STAT_OUT_ASP_ISENSE | int | Enable Strommessung ASP Beiklappen (ab i6.121) |
| STAT_OUT_FH_EN | int | Fensterheber Enable Ausgang |
| STAT_OUT_EN1 | int | Elmos 1 enable (ab i6.121) |
| STAT_OUT_EN2 | int | Elmos 2 enable (ab i6.121) |
| STAT_OUT_FLASHEN | int | Enable FLASH Ladungspumpe (bis i6.103) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-switch-block"></a>
### STATUS_SWITCH_BLOCK

Auslesen der Stati aller Schalterblock Signale (K-Bus) KWP2000: $30 InputOutputControlByLocalIdentifier $05 all K-Bus inputs $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_S_FH_SBFT_GESAMT | int | Status Taster Fensterheber Fahrertuer vorne 0 = aus, 1 = auf, 2 = zu, 5 = tipp-auf, 10 = tipp-zu |
| STAT_S_FH_SBFTAUFDISC | int | Fahrertuer vorne Fensterheber auf |
| STAT_S_FH_SBFTZUDISC | int | Fahrertuer vorne Fensterheber zu |
| STAT_S_FH_SBFTTAUFDISC | int | Fahrertuer vorne Fensterheber tipp-auf |
| STAT_S_FH_SBFTTZUDISC | int | Fahrertuer vorne Fensterheber tipp-zu |
| STAT_S_FH_SBFTH_GESAMT | int | Status Taster Fensterheber Fahrertuer hinten 0 = aus, 1 = auf, 2 = zu, 5 = tipp-auf, 10 = tipp-zu |
| STAT_S_FH_SBFTHAUFDISC | int | Fahrertuer hinten Fensterheber auf |
| STAT_S_FH_SBFTHZUDISC | int | Fahrertuer hinten Fensterheber zu |
| STAT_S_FH_SBFTHTAUFDISC | int | Fahrertuer hinten Fensterheber tipp-auf |
| STAT_S_FH_SBFTHTZUDISC | int | Fahrertuer hinten Fensterheber tipp-zu |
| STAT_S_FH_SBBT_GESAMT | int | Status Taster Fensterheber Beifahrertuer vorne 0 = aus, 1 = auf, 2 = zu, 5 = tipp-auf, 10 = tipp-zu |
| STAT_S_FH_SBBFTAUFDISC | int | Beifahrertuer vorne Fensterheber auf |
| STAT_S_FH_SBBFTZUDISC | int | Beifahrertuer vorne Fensterheber zu |
| STAT_S_FH_SBBFTTAUFDISC | int | Beifahrertuer vorne Fensterheber tipp-auf |
| STAT_S_FH_SBBFTTZUDISC | int | Beifahrertuer vorne Fensterheber tipp-zu |
| STAT_S_FH_SBBTH_GESAMT | int | Status Taster Fensterheber Beifahrertuer hinten 0 = aus, 1 = auf, 2 = zu, 5 = tipp-auf, 10 = tipp-zu |
| STAT_S_FH_SBBFTHAUFDISC | int | Beifahrertuer hinten Fensterheber auf |
| STAT_S_FH_SBBFTHZUDISC | int | Beifahrertuer hinten Fensterheber zu |
| STAT_S_FH_SBBFTHTAUFDISC | int | Beifahrertuer hinten Fensterheber tipp-auf |
| STAT_S_FH_SBBFTHTZUDISC | int | Beifahrertuer hinten Fensterheber tipp-zu |
| STAT_S_ASP_GESAMT | int | Status Taster Spiegelverstellung 0 = aus, 1 = rechts, 2 = links, 4 = oben, 8 = unten |
| STAT_S_ASP_RECHTSDISC | int | Spiegelverstellung rechts |
| STAT_S_ASP_LINKSDISC | int | Spiegelverstellung links |
| STAT_S_ASP_OBENDISC | int | Spiegelverstellung oben |
| STAT_S_ASP_UNTENDISC | int | Spiegelverstellung unten |
| STAT_S_ASP_FTBFTDISC | int | Wechselschalter Spiegelverstellung Fahrer-/Beifahrertuer 0 = Fahrertuer, 1 = Beifahrertuer |
| STAT_S_ASP_BKLPDISC | int | Taster Spiegelbeiklappen |
| STAT_S_KISI_DISC | int | Taster Kindersicherung |
| STAT_S_SRR_SBDISC | int | Taster Heckrollo Schalterblock vorne |
| STAT_S_FH_LOC_GESAMT | int | Status Taster lokaler Fensterheber hinten 0 = aus, 1 = auf, 2 = zu, 5 = tipp-auf, 10 = tipp-zu |
| STAT_S_FH_SBLOCAUFDISC | int | Lokaler Fensterheber hinten auf |
| STAT_S_FH_SBLOCZUDISC | int | Lokaler Fensterheber hinten zu |
| STAT_S_FH_SBLOCTAUFDISC | int | Lokaler Fensterheber hinten tipp-auf |
| STAT_S_FH_SBLOCTZUDISC | int | Lokaler Fensterheber hinten tipp-zu |
| STAT_S_SR1_DISC | int | Taster Sonnenrollo 1 (Rechtecksrollo) |
| STAT_S_SR2_DISC | int | Taster Sonnenrollo 2 (Dreiecksrollo) |
| STAT_S_SRR_DISC | int | Taster Heckrollo Schalterblock hinten |
| STAT_S_SR_RLDISC | int | Wechselschalter Sonnenrollo remote/lokal 0 = Rollo andere Seite, 1 = Rollo selbe Seite |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-flags"></a>
### STATUS_FLAGS

Auslesen der internen Software-Flags KWP2000: $30 InputOutputControlByLocalIdentifier $06 all internal flags $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_Z_ZV_RUN | int | ZV aktiv |
| STAT_Z_ZV_ER | int | ZV Enriegelt |
| STAT_Z_ZV_VR | int | ZV Verriegelt |
| STAT_Z_ZV_KISI | int | ZV Kindersicherung aktiv (nicht Fensterheber) |
| STAT_Z_ZV_ZS | int | ZV Gesichert |
| STAT_Z_EO_RETURN | int | EO Rücklauf eingeleitet |
| STAT_Z_SCA_CATCH | int | SCA benötigt vollen Lauf zur Synchronisation |
| STAT_Z_ZV_ZSDELAY | int | Motorverzögerung bei ZV Sichern aktiv |
| STAT_Z_ZV_CRASH | int | Crash Modus aktiv |
| STAT_Z_EO_RUN | int | Electric Open aktiv |
| STAT_Z_SCA_READY | int | SCA in Bereit Position |
| STAT_Z_SZ_VR | int | Schliesszylinder Verriegeln aktiv |
| STAT_Z_SZ_ER | int | Schliesszylinder Entriegeln aktiv |
| STAT_Z_SZ_VRVALID | int | Gültige ER-Hall Flanke nach VR-Flanke |
| STAT_Z_SZ_ERVALID | int | Gültige VR-Hall Flanke nach ER-Flanke |
| STAT_Z_ZV_WDHSPERRE | int | lokale Wiederholsperre ZV aktiv |
| STAT_Z_ZV_TKALT | int | verzögerter (100ms) Türkontakt für SCA |
| STAT_Z_EO_BREAK | int | EO-Antrieb hat Bremsposition erreicht |
| STAT_Z_EO_UNDEF | int | EO-Antrieb in undefinierter Position |
| STAT_S_ZV_PEER | int | Anforderung Entriegeln nach EO an das CAS |
| STAT_Z_EBA_MODE | int | EBA-Modus aktiv (nicht mehr benutzt) |
| STAT_Z_SCA_ZU | int | SCA geschlossen (Parkposition) |
| STAT_Z_KISI | int | Kindersicherung (Fensterheber und Sonnenrollo) aktiv |
| STAT_Z_SCA_UNDEF | int | SCA in undefinierter Position |
| STAT_Z_ASP_PAUSE | int | Aussenspiegelverstellung pausiert nach Timeout (10s) |
| STAT_Z_MEMAKT | int | Aussenspiegel Memoryposition wird angefahren |
| STAT_Z_MEM_VER | int | Aussenspiegel Memoryposition Verstellung vertikal |
| STAT_Z_MEM_HOR | int | Aussenspiegel Memoryposition Verstellung horizontal |
| STAT_Z_ASP_USPG | int | Aussenspiegel Unterspannung detektiert |
| STAT_Z_SPGKLAPP | int | Aussenspiegel beigeklappt |
| STAT_Z_ASP_KERB | int | Auusenspiegel in abgeklappter Bordsteinposition |
| STAT_Z_ASP_SPERRE | int | Spiegelbeiklappen gesperrt für 3min nach Timeout |
| STAT_Z_SR1_BLOCK | int | Sonnenrollo 1 hat Block erreicht |
| STAT_Z_SR2_BLOCK | int | Sonnenrollo 2 hat Block erreicht |
| STAT_Z_SR1_REVERSE | int | Sonnenrollo 1 dreht Laufrichtung um |
| STAT_Z_SR2_REVERSE | int | Sonnenrollo 2 dreht Laufrichtung um |
| STAT_Z_SR1_DELAY | int | Strommessung Sonnenrollo 1 verzögert nach Start |
| STAT_Z_SR2_DELAY | int | Strommessung Sonnenrollo 2 verzögert nach Start |
| STAT_Z_SR_VLOW | int | Unterspannung Sonnenrollos detektiert |
| STAT_Z_SR1_ERROR | int | Sonnenrollo 1 im Fehlerbetrieb bei offener Scheibe |
| STAT_Z_SR1_DRIVE | int | Motor Sonnenrollo 1 aktiv |
| STAT_Z_SR2_DRIVE | int | Motor Sonnenrollo 2 aktiv |
| STAT_Z_SR1_UP | int | Sonnenrollo 1 oben oder fährt nach oben |
| STAT_Z_SR2_UP | int | Sonnenrollo 2 oben oder fährt nach oben |
| STAT_Z_SRR_LONG | int | Heckrollo-Langdruck aktiviert |
| STAT_Z_SR1_REPEAT | int | Sonnenrollo 1 in Wiederholsperre |
| STAT_Z_SR2_REPEAT | int | Sonnenrollo 2 in Wiederholsperre |
| STAT_Z_ASP_DRIVE | int | Motor Spiegelbeiklappen aktiv |
| STAT_Z_ASP_DELAY | int | Strommessung Spiegelbeiklappen verzögert nach Start |
| STAT_Z_ASP_BSDELAY | int | Wartezeit (1s) vor Bordsteinautomatik aktiv |
| STAT_Z_ASP_VLOW | int | Unterspannung Aussenspiegel detektiert |
| STAT_Z_FH_SEND | int | Fensterheber sendet neue Scheibenposition (ab i6.121) |
| STAT_Z_FH_OPEN | int | 0 = Fenster geschlossen, 1 = Fenster halb offen (ab i6.121) |
| STAT_Z_FH_OPENED | int | 0 = Fenster halb offen oder geschlossen, 1 = Fenster ganz offen (ab i6.121) |
| STAT_Z_LOW_VOLTAGE | int | Unterspannung (&lt;9V) an Klemme 30 detektiert (ab i6.121) |
| STAT_Z_OVR_VOLTAGE | int | Überspannung (&gt;16V) an Klemme 30 detektiert (ab i6.121) |
| STAT_Z_KBUS_ACTIVE | int | K-Bus aktiv (ab i6.121) |
| STAT_Z_RHD | int | Rechtslenkerfahrzeug eingestellt (ab i6.121, kodiert) |
| STAT_Z_LOWVOLT_LOG | int | Fehlerspeichereintrag Unterspannung aktiv (ab i6.121) |
| STAT_DIAG_SR | int | Diagnoseansteuerung Sonnenrollo aktiv (ab i6.121) |
| STAT_DIAG_ASPHZGOFF | int | Spiegelheizung abgeschaltet durch Diagnose (ab i6.121) |
| STAT_DIAG_EMF | int | Diagnoseansteuerung EMF aktiv (ab i6.121) |
| STAT_DIAG_RESERVE3 | int | vorgehalten (ab i6.121) |
| STAT_DIAG_RESERVE4 | int | vorgehalten (ab i6.121) |
| STAT_DIAG_RESERVE5 | int | vorgehalten (ab i6.121) |
| STAT_DIAG_RESERVE6 | int | vorgehalten (ab i6.121) |
| STAT_DIAG_RESERVE7 | int | vorgehalten (ab i6.121) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Auslesen der Stati aller digitaler Signale KWP2000: $30 InputOutputControlByLocalIdentifier $01 all digital signals $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SIGNALS | binary | Alle Signale in Hex |
| STAT_Z_FH_OPEN | int | 0 = Fenster geschlossen, 1 = Fenster (halb) offen |
| STAT_Z_FH_OPENED | int | 0 = Fenster halb offen oder geschlossen, 1 = Fenster ganz offen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern von jedem digitalen Signal KWP2000: $30 InputOutputControlByLocalIdentifier $01 digital signals $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SIGNAL_NAME | string | Werte: Alle Namen aus Signaltabelle E65  : table DigitalIOSignal E65rd: table DigitalIOSignalRd table DigitalIOSignal__ TEXT |
| DIGITALWERT | string | logical value Werte: true, false table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-analog"></a>
### STEUERN_ANALOG

Ansteuern von jedem digitalen Signal KWP2000: $30 InputOutputControlByLocalIdentifier $10 digital signals $07 ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SIGNAL_NAME | string | Werte: Alle Namen aus Analogtabelle table AnalogSignal TEXT |
| ANALOGWERT | int | Werte: 0...255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende"></a>
### STEUERN_ENDE

Ansteuern von jedem digitalen Signal KWP2000: $30 InputOutputControlByLocalIdentifier $01 digital signals $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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

<a id="job-status-cfl"></a>
### STATUS_CFL

Auslesen der Stati von CFL KWP2000: $31 startRoutineByLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GERAET | string | gewuenschte Komponente table Geraet NAME_GERAET TEXT |
| FUNKTION | string | gewuenschte Funktion table Funktion_CFL CFL_FUNKTION TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| WERT | int | Auslesen von Funktionswert |
| STOP_REASON | string | Auslesen von Stop_Reason |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cfl"></a>
### STEUERN_CFL

Steuern der CFL-modul KWP2000: $31 startRoutineByLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GERAET | string | gewuenschte Komponente table Geraet NAME_GERAET TEXT |
| FUNKTION | string | gewuenschte Funktion table Funktion_CFL CFL_FUNKTION TEXT |
| WERT | string | Funktionswert Werte in dezimal |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-er"></a>
### STEUERN_ER

Tuermodul ZV Entriegeln !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $21 DiagZVER Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vr"></a>
### STEUERN_VR

Tuermodul ZV Verriegeln !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $22 DiagZVVR Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zs"></a>
### STEUERN_ZS

Tuermodul ZV Sichern !!! ab i6.121 !!! Achtung: bei Diagnose-Ende nach Timeout bleibt TM gesichert!! Diagnose ist dann nicht mehr möglich (Security-Access denied) Diagnose muß bis Entriegeln aufrechterhalten werden!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $23 DiagZVZS Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Auslesen aller analoge Werte KWP2000: $30 InputOutputControlByLocalIdentifier $10 all analog values $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_U_BATT | int | (Klemme 30) Spannung am Steuergerät (digits) |
| STAT_U_BATT_WERT | int | (Klemme 30) Spannung am Steuergerät (gerundet) |
| STAT_UBATT_WERT | real | (Klemme 30) Spannung am Steuergerät in Volt Auflösung 0.11 V/Bit |
| STAT_U_BATT_EINH | string | Volt |
| STAT_SR1_CURRENT | int | Sonnenrollo 1 Laufstrom (digits) |
| STAT_SR1_CURRENT_WERT | int | Sonnenrollo 1 Laufstrom (gerundet) |
| STAT_SR1_CURRENT_REAL_WERT | real | Sonnenrollo 1 Laufstrom in Ampere Auflösung 0.0565 A/Bit |
| STAT_SR1_CURRMAX | int | Sonnenrollo 1 Anlaufstrom (digits) |
| STAT_SR1_CURRMAX_WERT | int | Sonnenrollo 1 Anlaufstrom (gerundet) |
| STAT_SR1_CURRMAX_REAL_WERT | real | Sonnenrollo 1 Anlaufstrom in Ampere Auflösung 0.0565 A/Bit Wert bleibt bis nächsten Start stehen Kann durch STEUERGERAETE_RESET zurückgesetzt werden |
| STAT_SR1_CURR_EINH | string | Ampere |
| STAT_SR2_CURRENT | int | Sonnenrollo 2 Laufstrom (digits) |
| STAT_SR2_CURRENT_WERT | int | Sonnenrollo 2 Laufstrom (gerundet) |
| STAT_SR2_CURRENT_REAL_WERT | real | Sonnenrollo 2 Laufstrom in Ampere Auflösung 0.0565 A/Bit |
| STAT_SR2_CURRMAX | int | Sonnenrollo 2 Anlaufstrom (digits) |
| STAT_SR2_CURRMAX_WERT | int | Sonnenrollo 2 Anlaufstrom (gerundet) |
| STAT_SR2_CURRMAX_REAL_WERT | real | Sonnenrollo 2 Anlaufstrom in Ampere Auflösung 0.0565 A/Bit Wert bleibt bis nächsten Start stehen Kann durch STEUERGERAETE_RESET zurückgesetzt werden |
| STAT_SR2_CURR_EINH | string | Ampere |
| STAT_FH_VMOT1 | int | Fensterheber Kontrollspannung 1 (digits) |
| STAT_FH_VMOT1_WERT | int | Fensterheber Kontrollspannung 1 (gerundet) |
| STAT_FH_VMOT1_REAL_WERT | real | Fensterheber Kontrollspannung 1 in Volt Auflösung 0.1 V/Bit |
| STAT_FH_VMOT1_EINH | string | Volt |
| STAT_FH_VMOT2 | int | Fensterheber Kontrollspannung 2 (digits) |
| STAT_FH_VMOT2_WERT | int | Fensterheber Kontrollspannung 2 (gerundet) |
| STAT_FH_VMOT2_REAL_WERT | real | Fensterheber Kontrollspannung 2 in Volt Auflösung 0.1 V/Bit |
| STAT_FH_VMOT2_EINH | string | Volt |
| STAT_FH_PWM1 | int | PWM-Wert für Fensterheber-Treiber 1 iO-Bereich bis i6.103: 0...200 = 0...100% iO-Bereich ab  i6.121: 0...250 = 0...100% |
| STAT_FH_PWM2 | int | PWM-Wert für Fensterheber-Treiber 2 iO-Bereich bis i6.103: 0...200 = 0...100% iO-Bereich ab  i6.121: 0...250 = 0...100% |
| STAT_FH_POS | int | Position der Seitenscheibe (digits) |
| STAT_FH_POS_WERT | int | Position der Seitenscheibe (gerundet) |
| STAT_FH_POS_REAL_WERT | int | Position der Seitenscheibe in cm |
| STAT_FH_POS_EINH | string | cm |
| STAT_OUT_SB_LCHTLED | int | output value of LED illumination switch block |
| STAT_LMP_VFB | int | PWM value of arrival lamp |
| STAT_LMP_AMB | int | PWM value of ambient illumination |
| STAT_CTR_ILMUMN_SW | int | Kl58g (ilumination value, received from CAN) |
| STAT_V_FZG | int | Fahrzeuggeschwindigkeit (CAN-Empfang) |
| STAT_TEMP_FZG_AUSSEN | int | Aussentemperatur (CAN-Empfang) |
| STAT_TEMP_FZG_AUSSEN_WERT | int | Aussentemperatur (gerundet) |
| STAT_TEMP_FZG_AUSSEN_REAL_WERT | int | Aussentemperatur in Grad C |
| STAT_TEMP_INTERN | int | Fahrzeuginnentemperatur (CAN-Empfang) |
| STAT_TEMP_BOARD | int | Leiterplattentemperatur (digits) |
| STAT_TEMP_BOARD_WERT | int | Leiterplattentemperatur (gerundet) |
| STAT_TEMP_BOARD_REAL_WERT | int | Leiterplattentemperatur in Grad C |
| STAT_TEMP_EINH | string | Grad Celcius |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cosi-ein"></a>
### STEUERN_COSI_EIN

Coach-Door Sicherung einlegen !!! ab i6.121 mit Rolls Royce Kodierung !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $01 DiagCoSiOn Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cosi-aus"></a>
### STEUERN_COSI_AUS

Coach-Door Sicherung auslegen !!! ab i6.121 mit Rolls Royce Kodierung !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $02 DiagCoSiOff Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-emf"></a>
### STEUERN_EMF

Steuern der EMF Ausgaenge fuer ZEIT mal 10ms !!! ab i6.121 mit Rolls Royce Kodierung !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $03 DiagEMF $xx EMF Aktivierung fuer $xx * 10ms Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | int | Zeit der Aktivierung Werte: 0...255 Werte: 0  = EMF ausschalten Werte: &gt;0 = EMF 0,01s - 2,55s ein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sr1-up"></a>
### STEUERN_SR1_UP

Sonnenrollo 1 rauf fuer ZEIT mal 10ms oder bis Anschlag !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $11 DiagSR1Up $xx SR1 Aktivierung fuer $xx * 10ms Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | int | Zeit der Aktivierung Werte: 0...255 Werte: 0  = Fahrt bis Block Werte: &gt;0 = 0,01s - 2,55s Fahrt nach oben und Stop |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sr1-down"></a>
### STEUERN_SR1_DOWN

Sonnenrollo 1 runter fuer ZEIT mal 10ms oder bis Anschlag !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $12 DiagSR1Down $xx SR1 Aktivierung fuer $xx * 10ms Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | int | Zeit der Aktivierung Werte: 0...255 Werte: 0  = Fahrt bis Block Werte: &gt;0 = 0,01s - 2,55s Fahrt nach unten und Stop |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sr2-up"></a>
### STEUERN_SR2_UP

Sonnenrollo 2 rauf fuer ZEIT mal 10ms oder bis Anschlag !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $13 DiagSR2Up $xx SR2 Aktivierung fuer $xx * 10ms Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | int | Zeit der Aktivierung Werte: 0...255 Werte: 0  = Fahrt bis Block Werte: &gt;0 = 0,01s - 2,55s Fahrt nach oben und Stop |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sr2-down"></a>
### STEUERN_SR2_DOWN

Sonnenrollo 1 runter fuer ZEIT mal 10ms oder bis Anschlag !!! ab i6.121 !!! KWP2000: $31 StartRoutineByLocalIdentifier $FC Application diagnostics routines $14 DiagSR2Down $xx SR2 Aktivierung fuer $xx * 10ms Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | int | Zeit der Aktivierung Werte: 0...255 Werte: 0  = Fahrt bis Block Werte: &gt;0 = 0,01s - 2,55s Fahrt nach unten und Stop |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (41 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [DIGITALIOSIGNALRD](#table-digitaliosignalrd) (247 × 2)
- [DIGITALIOSIGNAL](#table-digitaliosignal) (215 × 2)
- [ANALOGSIGNAL](#table-analogsignal) (22 × 2)
- [GERAET](#table-geraet) (2 × 3)
- [STOP_REASON](#table-stop-reason) (31 × 3)
- [FUNKTION_CFL](#table-funktion-cfl) (61 × 3)

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

Dimensions: 76 rows × 2 columns

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

Dimensions: 41 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xDCC4 | CAN_Low, Physikalischer Fehler |
| 0xDCC7 | Controller, Bus Off |
| 0x9C08 | Prozessor defekt |
| 0x9C09 | Schalterblock defekt |
| 0x9C0A | Dauerhafte Unterspannung |
| 0x9C0B | Energiesparmode aktiv |
| 0x9C0E | CAN_Low, Physikalischer Fehler |
| 0x9C0F | Controller, Bus Off |
| 0x9C10 | ZV Motor ER defekt |
| 0x9C11 | ZV Motor COM defekt |
| 0x9C12 | ZV Motor VR/ZS defekt |
| 0x9C13 | Elektrisch Oeffnen Motor defekt |
| 0x9C14 | SCA Motor defekt |
| 0x9C15 | KISI Sensor defekt |
| 0x9C16 | ZV ER Sensor defekt |
| 0x9C17 | SCA Sensor defekt |
| 0x9C18 | Elektrisch Oeffnen Sensor defekt |
| 0x9C19 | Elektrisch Oeffnen Freigabe ohne TAG |
| 0x9C1A | Fussraumleuchte defekt |
| 0x9C1B | Tuerwarnleuchte defekt |
| 0x9C1C | Ambiente Beleuchtung defekt |
| 0x9C1D | Vorfeldbeleuchtung defekt |
| 0x9C20 | FH Defekt vorgehalten |
| 0x9C21 | FH Defekt vorgehalten |
| 0x9C22 | Fensterhebermechanik schwergaengig |
| 0x9C23 | Hallsensor defekt |
| 0x9C24 | Transistorbruecke defekt |
| 0x9C25 | Motorklemmenspannung unplausibel |
| 0x9C26 | Fensterposition ungueltig |
| 0x9C27 | Kennlinie ungueltig |
| 0x9C28 | Temperaturwert unplausibel |
| 0x9C29 | Magnetrad Polbreiten ungueltig |
| 0x9C2F | Einklemmschutz defekt |
| 0x9C30 | Spiegel Motor Horizontal defekt |
| 0x9C31 | Spiegel Motor Vertikal defekt |
| 0x9C32 | Beiklappmotor defekt |
| 0x9C33 | Spiegelheizung defekt |
| 0x9C34 | Spiegelheizung Kurzschluss |
| 0x9C35 | Spiegelposition Potentiometer vertikal defekt |
| 0x9C36 | Spiegelposition Potentiometer horizontal defekt |
| 0x???? | unbekannter Fehlerort |

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
| F_UWB_ERW | nein |

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

<a id="table-digitaliosignalrd"></a>
### DIGITALIOSIGNALRD

Dimensions: 247 rows × 2 columns

| TEXT | NR |
| --- | --- |
| S_SZ_VR | 0 |
| S_COSI_VR | 0 |
| S_ZV_ER | 1 |
| S_SZ_ER | 2 |
| S_COSI_TK | 2 |
| S_ZV_TK | 3 |
| S_SCA_SPK | 4 |
| S_ZV_TAG | 5 |
| S_ZV_TIG | 5 |
| S_FH_ZU | 6 |
| S_FH_AUF | 7 |
| S_SPARE_1 | 8 |
| S_PE_BEREIT | 9 |
| S_SCA_BEREIT | 10 |
| S_ZV_KISI | 11 |
| S_ASP_RAST | 12 |
| S_ZV_TAG2 | 13 |
| S_KS_AUF | 14 |
| S_KS_AB | 15 |
| DIAG_MFOLDSTS | 16 |
| RESERVED_1 | 17 |
| DIAG_SCASTS | 18 |
| DIAG_ASP_COMLO | 19 |
| DIAG_ASP_COMHI | 20 |
| DIAG_ASP_POWER | 21 |
| DIAG_CMNSTS | 22 |
| DIAG_LOCKSTS | 23 |
| DIAG_PETOSTS | 24 |
| RESERVED_2 | 25 |
| S_FH_HALL2 | 26 |
| S_FH_HALL1 | 27 |
| DIAG_PEST | 28 |
| DIAG_ASP_OVERLOAD | 29 |
| DIAG_ASP_OPENLOAD | 30 |
| DIAG_VFSTS | 31 |
| DIAG_LTSTS2 | 32 |
| RESERVED_3 | 33 |
| DIAG_LTSTS1 | 34 |
| RESERVED_4 | 35 |
| DIAG_ASP_HORLO | 36 |
| DIAG_ASP_HORHI | 37 |
| DIAG_ASP_VERLO | 38 |
| DIAG_ASP_VERHI | 39 |
| OUT_SB_KL30DISC | 40 |
| OUT_ASP_MOTBKLPAUSHIDISC | 41 |
| OUT_ASP_ISENSE | 42 |
| OUT_ASP_MOTBKLPEINHIDISC | 43 |
| OUT_ASP_MOT_INH | 44 |
| OUT_ASP_MOT_CS | 45 |
| OUT_ASP_MOTBKLPAUSLODISC | 46 |
| OUT_ASP_MOTBKLPEINLODISC | 47 |
| OUT_SBR_KL30DISC | 48 |
| OUT_SR2_MOTZULODISC | 49 |
| OUT_SR2_MOTAUFLODISC | 50 |
| OUT_SR2_MOTAUFHIDISC | 51 |
| OUT_SR1_MOTAUFLODISC | 52 |
| OUT_SR1_MOTZUHIDISC | 53 |
| OUT_SR1_MOTZULODISC | 54 |
| OUT_SR1_MOTAUFHIDISC | 55 |
| OUT_ASP_MOTHORLODISC | 56 |
| OUT_ASP_MOTHORHIDISC | 57 |
| OUT_ASP_MOTVERLODISC | 58 |
| OUT_ASP_MOTVERHIDISC | 59 |
| OUT_ZV_VRLODISC | 60 |
| OUT_ZV_ZSLODISC | 61 |
| OUT_ZV_VRHIDISC | 62 |
| OUT_ZV_ZSHIDISC | 63 |
| OUT_EN1 | 64 |
| OUT_EN2 | 65 |
| OUT_ZV_KISILODISC | 66 |
| OUT_ZV_MOTCOMLODISC | 67 |
| OUT_ZV_KISIHIDISC | 68 |
| OUT_ASP_5VPOT | 69 |
| RESERVED_5 | 70 |
| OUT_ZV_MOTCOMHIDISC | 71 |
| OUT_SR2_MOTZUHIDISC | 72 |
| RESERVED_6 | 73 |
| OUT_LMP_FRDISC | 74 |
| OUT_ASP_HZGDISC | 75 |
| RESERVED_7 | 76 |
| OUT_SCA_MOTDISC | 77 |
| OUT_FH_EN | 78 |
| RESERVED_8 | 79 |
| RESERVED_9 | 80 |
| RESERVED_10 | 81 |
| RESERVE_11 | 82 |
| OUT_ASP_MOTCOMLODISC | 83 |
| OUT_ASP_MOTCOMHIDISC | 84 |
| OUT_PE_MOTURZUBRKDISC | 85 |
| OUT_SCA_MOTBRKDISC | 86 |
| OUT_PE_MOTURZUDISC | 87 |
| S_KLR_CBOT | 88 |
| S_KL15_CBOT | 89 |
| S_KL50_CBOT | 90 |
| S_TRAILER_CBOT | 91 |
| S_RFS_CBOT | 92 |
| CTR_DIM_PFIECBOT | 93 |
| CTR_PFIE_CBOT | 94 |
| S_FH_PANICCBOT | 95 |
| S_EO_CBOT | 96 |
| S_ER_CBOT | 97 |
| S_VR_CBOT | 98 |
| S_SICHERN_CBOT | 99 |
| S_ZV_PEER | 100 |
| Z_CRASH_CBOT | 101 |
| S_ZV_ZSINHIBIT | 102 |
| S_ZV_WDHSPERRE | 103 |
| S_FH_AUFCBOT | 104 |
| S_FH_ZUCBOT | 105 |
| S_FH_TCBOT | 106 |
| S_FH_FZGSTEHTCBOT | 107 |
| S_FHCAS_AUFCBOT | 108 |
| S_FHCAS_ZUCBOT | 109 |
| S_FHCAS_TCBOT | 110 |
| S_FHCAS_ENBCBOT | 111 |
| S_MEM_ABRUFCBOT | 112 |
| S_MEM_SPEICHCBOT | 113 |
| S_SR1_CBOT | 114 |
| S_SR2_CBOT | 115 |
| S_SR_UPCBOT | 116 |
| S_SR_DOWNCBOT | 117 |
| S_COMFORT_AUFCBOT | 118 |
| S_COMFORT_ZUCBOT | 119 |
| CAN_COSI_SAFE | 120 |
| CAN_COSI_ALWD | 121 |
| CAN_COSI_EMF | 122 |
| CAN_COSI_SEND | 123 |
| RESERVED_12 | 124 |
| RESERVED_13 | 125 |
| RESERVED_14 | 126 |
| RESERVED_15 | 127 |
| RESERVED_16 | 128 |
| RESERVED_17 | 129 |
| RESERVED_18 | 130 |
| RESERVED_19 | 131 |
| S_POWER_VACBOT | 132 |
| S_POWER_DOWNCBOT | 133 |
| S_WISCHER_STSCBOT | 134 |
| S_SH_EINCBOT | 135 |
| S_FH_SBFTAUFDISC | 136 |
| S_FH_SBFTZUDISC | 137 |
| S_FH_SBFTTAUFDISC | 138 |
| S_FH_SBFTTZUDISC | 139 |
| S_FH_SBFTHAUFDISC | 140 |
| S_FH_SBFTHZUDISC | 141 |
| S_FH_SBFTHTAUFDISC | 142 |
| S_FH_SBFTHTZUDISC | 143 |
| S_FH_SBBFTAUFDISC | 144 |
| S_FH_SBBFTZUDISC | 145 |
| S_FH_SBBFTTAUFDISC | 146 |
| S_FH_SBBFTTZUDISC | 147 |
| S_FH_SBBFTHAUFDISC | 148 |
| S_FH_SBBFTHZUDISC | 149 |
| S_FH_SBBFTHTAUFDISC | 150 |
| S_FH_SBBFTHTZUDISC | 151 |
| S_ASP_RECHTSDISC | 152 |
| S_ASP_LINKSDISC | 153 |
| S_ASP_OBENDISC | 154 |
| S_ASP_UNTENDISC | 155 |
| S_ASP_FTBFTDISC | 156 |
| S_ASP_BKLPDISC | 157 |
| S_KISI_DISC | 158 |
| S_SRR_SBDISC | 159 |
| S_FH_SBLOCAUFDISC | 160 |
| S_FH_SBLOCZUDISC | 161 |
| S_FH_SBLOCTAUFDISC | 162 |
| S_FH_SBLOCTZUDISC | 163 |
| S_SR1_DISC | 164 |
| S_SR2_DISC | 165 |
| S_SRR_DISC | 166 |
| S_SR_RLDISC | 167 |
| Z_ZV_RUN | 168 |
| Z_ZV_ER | 169 |
| Z_ZV_VR | 170 |
| Z_ZV_ZS | 171 |
| Z_ZV_KISI | 172 |
| Z_ZV_CRASH | 173 |
| Z_ZV_WDHSPERRE | 174 |
| Z_ZV_ZSDELAY | 175 |
| Z_EO_RUN | 176 |
| Z_EO_BREAK | 177 |
| Z_EO_UNDEF | 178 |
| Z_EO_RETURN | 179 |
| Z_SZ_VR | 180 |
| Z_SZ_ER | 181 |
| Z_SZ_VRVALID | 182 |
| Z_SZ_ERVALID | 183 |
| Z_SCA_READY | 184 |
| Z_SCA_CATCH | 185 |
| Z_SCA_ZU | 186 |
| Z_SCA_UNDEF | 187 |
| Z_PEER | 188 |
| Z_ZV_TKALT | 189 |
| Z_KISI | 190 |
| RESERVED_20 | 191 |
| Z_ASP_PAUSE | 192 |
| Z_MEMAKT | 193 |
| Z_MEM_VER | 194 |
| Z_MEM_HOR | 195 |
| Z_ASP_USPG | 196 |
| Z_SPGKLAPP | 197 |
| Z_ASP_KERB | 198 |
| Z_ASP_SPERRE | 199 |
| Z_ASP_DRIVE | 200 |
| Z_ASP_DELAY | 201 |
| Z_ASP_BSDELAY | 202 |
| Z_ASP_VLOW | 203 |
| RESERVED_21 | 204 |
| RESERVED_22 | 205 |
| RESERVED_23 | 206 |
| RESERVED_24 | 207 |
| Z_SR1_BLOCK | 208 |
| Z_SR2_BLOCK | 209 |
| Z_SR1_REVERSE | 210 |
| Z_SR2_REVERSE | 211 |
| Z_SR1_DELAY | 212 |
| Z_SR2_DELAY | 213 |
| Z_SR_VLOW | 214 |
| Z_SR1_ERROR | 215 |
| Z_SR1_DRIVE | 216 |
| Z_SR2_DRIVE | 217 |
| Z_SR1_UP | 218 |
| Z_SR2_UP | 219 |
| Z_SRR_LONG | 220 |
| RESERVED_25 | 221 |
| Z_SR1_REPEAT | 222 |
| Z_SR2_REPEAT | 223 |
| Z_FH_SEND | 224 |
| Z_FH_OPEN | 225 |
| Z_FH_OPENED | 226 |
| Z_LOW_VOLTAGE | 227 |
| Z_OVR_VOLTAGE | 228 |
| Z_KBUS_ACTIVE | 229 |
| Z_RHD | 230 |
| Z_LOWVOLT_LOG | 231 |
| DIAG_ASP_TEMP | 999 |
| DIAG_FHENOUTPUT | 999 |
| OUT_FLASHEN | 999 |
| OUT_PE_KL30DISC | 999 |
| OUT_WKUP_TIMER | 999 |
| S_FH_SBHAUFCBOT | 999 |
| S_FH_SBHTCBOT | 999 |
| S_FH_SBHZUCBOT | 999 |
| S_KISI_CBOT | 999 |
| Z_EBA_MODE | 999 |
| Z_ZV_INIT | 999 |
| Z_ZV_MOTORKURZ | 999 |

<a id="table-digitaliosignal"></a>
### DIGITALIOSIGNAL

Dimensions: 215 rows × 2 columns

| TEXT | NR |
| --- | --- |
| S_SZ_VR | 0 |
| S_ZV_ER | 1 |
| S_SZ_ER | 2 |
| S_ZV_TK | 3 |
| S_SCA_SPK | 4 |
| S_ZV_TAG | 5 |
| S_FH_ZU | 6 |
| S_FH_AUF | 7 |
| S_SPARE_1 | 8 |
| S_PE_BEREIT | 9 |
| S_SCA_BEREIT | 10 |
| S_ZV_KISI | 11 |
| S_ASP_RAST | 12 |
| S_ZV_TAG2 | 13 |
| S_KS_AUF | 14 |
| S_KS_AB | 15 |
| RESERVED_1 | 16 |
| DIAG_SCASTS | 17 |
| DIAG_PETOSTS | 18 |
| DIAG_MFOLDSTS | 19 |
| DIAG_VFSTS | 20 |
| DIAG_CMNSTS | 21 |
| DIAG_LOCKSTS | 22 |
| RESERVED_2 | 23 |
| DIAG_ASP_COMLO | 24 |
| DIAG_ASP_COMHI | 25 |
| DIAG_LTSTS1 | 26 |
| DIAG_FHENOUTPUT | 27 |
| DIAG_ASP_OVERLOAD | 28 |
| DIAG_ASP_OPENLOAD | 29 |
| DIAG_ASP_POWER | 30 |
| DIAG_LTSTS2 | 31 |
| DIAG_PEST | 32 |
| S_FH_HALL1 | 33 |
| S_FH_HALL2 | 34 |
| DIAG_ASP_TEMP | 35 |
| DIAG_ASP_HORLO | 36 |
| DIAG_ASP_HORHI | 37 |
| DIAG_ASP_VERLO | 38 |
| DIAG_ASP_VERHI | 39 |
| RESERVED_3 | 40 |
| RESERVED_4 | 41 |
| OUT_ZV_KISILODISC | 42 |
| OUT_ZV_MOTCOMLODISC | 43 |
| OUT_ZV_KISIHIDISC | 44 |
| OUT_ASP_5VPOT | 45 |
| OUT_FLASHEN | 46 |
| OUT_ZV_MOTCOMHIDISC | 47 |
| OUT_SB_KL30DISC | 48 |
| OUT_WKUP_TIMER | 49 |
| OUT_PE_KL30DISC | 50 |
| OUT_SR2_MOTAUFHIDISC | 51 |
| OUT_ASP_MOTBKLPAUSHIDISC | 51 |
| OUT_SR1_MOTZULODISC | 52 |
| OUT_ASP_MOT_INH | 52 |
| OUT_SR1_MOTZUHIDISC | 53 |
| OUT_ASP_MOT_CS | 53 |
| OUT_SR1_MOTAUFLODISC | 54 |
| OUT_ASP_MOTBKLPAUSLODISC | 54 |
| OUT_SR1_MOTAUFHIDISC | 55 |
| OUT_ASP_MOTBKLPEINLODISC | 55 |
| OUT_ASP_MOTHORLODISC | 56 |
| OUT_ASP_MOTHORHIDISC | 57 |
| OUT_LMP_FRDISC | 58 |
| OUT_ASP_HZGDISC | 59 |
| RESERVED_5 | 60 |
| RESERVED_6 | 61 |
| OUT_FH_EN | 62 |
| OUT_SR2_MOTZULODISC | 63 |
| OUT_ASP_MOTBKLPEINHIDISC | 63 |
| RESERVED_7 | 64 |
| OUT_SR2_MOTAUFLODISC | 65 |
| RESERVED_8 | 66 |
| OUT_SCA_MOTDISC | 67 |
| OUT_PE_MOTURZUDISC | 68 |
| OUT_SCA_MOTBRKDISC | 69 |
| OUT_PE_MOTURZUBRKDISC | 70 |
| OUT_SR2_MOTZUHIDISC | 71 |
| OUT_ASP_MOTVERLODISC | 72 |
| OUT_ASP_MOTVERHIDISC | 73 |
| OUT_ASP_MOTCOMLODISC | 74 |
| OUT_ASP_MOTCOMHIDISC | 75 |
| OUT_ZV_VRLODISC | 76 |
| OUT_ZV_ZSLODISC | 77 |
| OUT_ZV_VRHIDISC | 78 |
| OUT_ZV_ZSHIDISC | 79 |
| S_KLR_CBOT | 80 |
| S_KL15_CBOT | 81 |
| S_KL50_CBOT | 82 |
| S_TRAILER_CBOT | 83 |
| S_RFS_CBOT | 84 |
| CTR_DIM_PFIECBOT | 85 |
| CTR_PFIE_CBOT | 86 |
| Z_CRASH_CBOT | 87 |
| S_EO_CBOT | 88 |
| S_ER_CBOT | 89 |
| S_VR_CBOT | 90 |
| S_SICHERN_CBOT | 91 |
| S_KISI_CBOT | 92 |
| RESERVED_10 | 93 |
| S_ZV_ZSINHIBIT | 94 |
| S_ZV_WDHSPERRE | 95 |
| S_FH_AUFCBOT | 96 |
| S_FH_ZUCBOT | 97 |
| S_FH_TCBOT | 98 |
| S_FH_FZGSTEHTCBOT | 99 |
| S_FHCAS_AUFCBOT | 100 |
| S_FHCAS_ZUCBOT | 101 |
| S_FHCAS_TCBOT | 102 |
| S_FHCAS_ENBCBOT | 103 |
| S_MEM_ABRUFCBOT | 104 |
| S_MEM_SPEICHCBOT | 105 |
| S_SR1_CBOT | 106 |
| S_SR2_CBOT | 107 |
| S_SR_UPCBOT | 108 |
| S_SR_DOWNCBOT | 109 |
| S_COMFORT_AUFCBOT | 110 |
| S_COMFORT_ZUCBOT | 111 |
| S_FH_SBHAUFCBOT | 112 |
| S_FH_SBHZUCBOT | 113 |
| S_FH_SBHTCBOT | 114 |
| S_FH_PANICCBOT | 115 |
| S_POWER_VACBOT | 116 |
| S_POWER_DOWNCBOT | 117 |
| S_WISCHER_STSCBOT | 118 |
| S_SH_EINCBOT | 119 |
| S_FH_SBFTAUFDISC | 120 |
| S_FH_SBFTZUDISC | 121 |
| S_FH_SBFTTAUFDISC | 122 |
| S_FH_SBFTTZUDISC | 123 |
| S_FH_SBFTHAUFDISC | 124 |
| S_FH_SBFTHZUDISC | 125 |
| S_FH_SBFTHTAUFDISC | 126 |
| S_FH_SBFTHTZUDISC | 127 |
| S_FH_SBBFTAUFDISC | 128 |
| S_FH_SBBFTZUDISC | 129 |
| S_FH_SBBFTTAUFDISC | 130 |
| S_FH_SBBFTTZUDISC | 131 |
| S_FH_SBBFTHAUFDISC | 132 |
| S_FH_SBBFTHZUDISC | 133 |
| S_FH_SBBFTHTAUFDISC | 134 |
| S_FH_SBBFTHTZUDISC | 135 |
| S_ASP_RECHTSDISC | 136 |
| S_ASP_LINKSDISC | 137 |
| S_ASP_OBENDISC | 138 |
| S_ASP_UNTENDISC | 139 |
| S_ASP_FTBFTDISC | 140 |
| S_ASP_BKLPDISC | 141 |
| S_KISI_DISC | 142 |
| S_SRR_SBDISC | 143 |
| S_FH_SBLOCAUFDISC | 144 |
| S_FH_SBLOCZUDISC | 145 |
| S_FH_SBLOCTAUFDISC | 146 |
| S_FH_SBLOCTZUDISC | 147 |
| S_SR1_DISC | 148 |
| S_SR2_DISC | 149 |
| S_SRR_DISC | 150 |
| S_SR_RLDISC | 151 |
| Z_ZV_RUN | 152 |
| Z_ZV_ER | 153 |
| Z_ZV_VR | 154 |
| Z_ZV_KISI | 155 |
| Z_ZV_ZS | 156 |
| Z_ZV_INIT | 157 |
| Z_SCA_CATCH | 158 |
| Z_ZV_ZSDELAY | 159 |
| Z_ZV_CRASH | 160 |
| Z_ZV_MOTORKURZ | 161 |
| Z_SCA_READY | 162 |
| Z_SZ_VR | 163 |
| Z_SZ_ER | 164 |
| Z_SZ_VRVALID | 165 |
| Z_SZ_ERVALID | 166 |
| Z_ZV_WDHSPERRE | 167 |
| Z_ZV_TKALT | 168 |
| Z_EO_BREAK | 169 |
| RESERVE_11 | 170 |
| S_ZV_PEER | 171 |
| Z_EBA_MODE | 172 |
| Z_SCA_ZU | 173 |
| Z_KISI | 174 |
| Z_SCA_UNDEF | 175 |
| Z_ASP_PAUSE | 176 |
| Z_MEMAKT | 177 |
| Z_MEM_VER | 178 |
| Z_MEM_HOR | 179 |
| Z_ASP_USPG | 180 |
| Z_SPGKLAPP | 181 |
| Z_ASP_KERB | 182 |
| Z_ASP_SPERRE | 183 |
| Z_SR1_BLOCK | 176 |
| Z_SR2_BLOCK | 177 |
| Z_SR1_REVERSE | 178 |
| Z_SR2_REVERSE | 179 |
| Z_SR1_DELAY | 180 |
| Z_SR2_DELAY | 181 |
| Z_SR_VLOW | 182 |
| Z_SR1_ERROR | 183 |
| Z_ASP_DRIVE | 184 |
| Z_ASP_DELAY | 185 |
| Z_ASP_BSDELAY | 186 |
| Z_ASP_VLOW | 187 |
| Z_SRR_LONG | 188 |
| Z_SR1_DRIVE | 184 |
| Z_SR2_DRIVE | 185 |
| Z_SR1_UP | 186 |
| Z_SR2_UP | 187 |
| Z_FH_SEND | 192 |
| Z_FH_OPEN | 193 |
| Z_FH_OPENED | 194 |
| Z_LOW_VOLTAGE | 195 |
| Z_OVR_VOLTAGE | 196 |
| Z_KBUS_ACTIVE | 197 |
| Z_RHD | 198 |
| Z_LOWVOLT_LOG | 199 |

<a id="table-analogsignal"></a>
### ANALOGSIGNAL

Dimensions: 22 rows × 2 columns

| TEXT | NR |
| --- | --- |
| U_BATT_DISC | 0 |
| S8_ASP_POTI_VOLTAGE | 1 |
| S8_ASP_POSVERTDISC | 2 |
| S8_ASP_POSHORDIC | 3 |
| S8_SR1_CURRENT_SENSE | 4 |
| S8_SR2_CURRENT_SENSE | 5 |
| S8_FH_VMOT1 | 6 |
| S8_FH_VMOT2 | 7 |
| OUT_LCHT_SBLED | 8 |
| S8_SR1_CURRENT_MAX | 9 |
| S8_SR2_CURRENT_MAX | 10 |
| S8_LMP_VFBDISC | 11 |
| S8_LMP_AMBDISC | 12 |
| S8_FH_PWM1 | 13 |
| S8_FH_PWM2 | 14 |
| S8_FH_POSCBOT | 15 |
| S8_MEM_POSCBOT | 16 |
| TEMP_FZG_AUSSENCBOT | 17 |
| CTR_ILMUMN_SWCBOT | 18 |
| V_FZG_CBOT | 19 |
| TEMP_INTERNCBOT | 20 |
| TEMP_BOARD | 21 |

<a id="table-geraet"></a>
### GERAET

Dimensions: 2 rows × 3 columns

| IOLI | NAME_GERAET | TEXT |
| --- | --- | --- |
| 0xFA | ECU | Steuergeraet |
| 0xFB | TSG | Fensterheber |

<a id="table-stop-reason"></a>
### STOP_REASON

Dimensions: 31 rows × 3 columns

| STOP_REASON_NR | STOP_REASON_TEXT | TEXT |
| --- | --- | --- |
| 0 | NOT_STOPPED | Motor laeuft |
| 1 | POSITION_REACHED | Position erreicht |
| 2 | STOP_MOVE | Bewegung abgebrochen |
| 3 | STOP_MOVE_INSTANTLY | Bewegung abgebrochen |
| 4 | NORM | Normiert |
| 5 | RENORM | Renormiert |
| 6 | PINCHING | Einklemmen erkannt |
| 7 | BLOCKING | Blockieren erkannt |
| 8 | DOUBLE_BLOCK | doppeltes Blockieren erkannt |
| 9 | NO_MOVE | keine Bewegung |
| 10 | EXCEPTION | Ausnahme |
| 11 | SAFETY_TIMER | Sicherheitszeitueberlauf |
| 12 | OPPOSITE_DIRECTION | verkehrte Drehrichtung |
| 13 | INVALID_TARGET_POS | falsche Zielposition |
| 14 | INVALID_ACTUAL_POS_LOW | falsche Zielposition (zu niedrig) |
| 15 | INVALID_ACTUAL_POS_HIGH | falsche Zielposition (zu hoch) |
| 16 | WRONG_DIR_LIMPHOME | falsche Drehrichtung fuer Notlauf |
| 17 | WRONG_NR_VALUES | flasche Anzahl Elemente |
| 18 | FINALIZE_CANT_WRITE | Schreibzugriff verweigert |
| 19 | FIFO_OVERRUN | FIFO Ueberlauf |
| 20 | CFL_NUMERICAL_OV | Numerischer Ueberlauf |
| 21 | CANT_TILT | ungueltige Hebenaufforderung |
| 22 | POS_OPEN_LEARNED | Fensterlaenge gelernt |
| 23 | STOP_MOVE_HIGH_TEMP | Motorabschaltung durch Thermomonitor |
| 24 | DRIVER_BAD | Motoransteuerung defekt |
| 25 | MOTOR_SHORT | Motorkurzschluss erkannt |
| 26 | STARTUP_FAILED | Bewegungsstart abgebrochen |
| 27 | RESET | State Machine Initialisierung |
| 28 | UNEXPECTED_STOP | unerwarteter Motorstop |
| 29 | HARDWARE_DOWN | Motoransteuerung inaktiv |
| 30 | RE_INIT | Re-Initialisierung |

<a id="table-funktion-cfl"></a>
### FUNKTION_CFL

Dimensions: 61 rows × 3 columns

| IOLI | CFL_FUNKTION | TEXT                                                                                    |
| --- | --- | --- |
|  |  | status_cfl                                             / steuern_cfl                    |
|  |  | DIAGNOSE-CMD's ECU                                                                      |
| 0x0000 | AUTOINIT_VORMONTAGE | Autoinit Vormontage starten (starten mit 0)                                             |
| 0x0001 | AUTOINIT_ENDMONTAGE | Autoinit Endmontage starten (starten mit 0), alle vier Fenster werden initialisiert     |
| 0x0002 | AUTOINIT_NACHBEARB. | Autoinit Nachbearbeitung starten (starten mit 0)                                        |
| 0x01FF | ECU_RESET | ECU Reset                                                                               |
|  |  | DIAGNOSE-CMD's TSG                                                                      |
| 0x01FE | CLEAR_EEPROM | EEPROM loeschen                                                                         |
| 0x0202 | NORMED | Status Normierung abfragen                             / Normierung loeschen            |
| 0x0203 | RF_VALID | Status Kennlinie abfragen                              / Kennlinie loeschen             |
| 0x0205 | STOP_REASON | Abbruchkriterium abfragen                                                               |
| 0x0206 | CFL_AVAILABLE | Status CFL verfuegbar abfragen                                                          |
| 0x0301 | POS_OPEN | Position Offen abfragen                                / setzen                         |
| 0x0304 | POS_XMM | Reversierweg abfragen                                  / setzen                         |
| 0x0307 | QUARTER_TURN | Reversierweg bei Emergency Close abfragen              / setzen                         |
| 0x0308 | TOLERANCE | Mechanisches Spiel abfragen                            / setzen                         |
| 0x0309 | CATCH_RANGE_CI | Fangfenster oben/innen abfragen                        / setzen                         |
| 0x030B | SPEED_SEAL | Geschwindigkeit im Dichtungsbereich abfragen           / setzen                         |
| 0x030D | SOFT_STOP_OFFSET | SoftStop Offset (Beginn der Bremsrampe) abfragen       / setzen                         |
| 0x030E | POS_SEAL | Beginn des Dichtungsbereiches abfragen                 / setzen                         |
| 0x030F | ENDMONTAGE_OK | Status Endmontage abfragen                                                              |
| 0x0311 | RF_DISTANCE | Abstand der Kennlinie von Position 0 abfragen          / setzen                         |
| 0x0313 | RF_LENGTH | Laenge der Kennlinie abfragen                          / setzen                         |
| 0x0314 | RF_LENGTH_65N | Kennlinie65N-Laenge abfragen                           / setzen                         |
| 0x0316 | SPEED_20N | Geschwindigkeit im 20N-Bereich abfragen                / setzen                         |
| 0x0317 | SPEED_65N | Geschwindigkeit im 65N-Bereich abfragen                / setzen                         |
| 0x0318 | FORCE_OFFSET_START | zusaetzlicher Ausloese-Offset beim Startvorgang(aus gleicher Richtung) abf. / setzen    |
| 0x0319 | FORCE_OFFSET_RESTART | zusaetzlicher Ausloese-Offset beim Startvorgang abf.   / setzen                         |
| 0x031A | FORCE_THRESH | Ausloese-Offset abfragen                               / setzen                         |
| 0x031D | TRACK_LIMIT | Startwert Tracking abfragen                            / setzen                         |
| 0x031E | TRACK_LIMIT_MIN | Endwert Tracking abfragen                              / setzen                         |
| 0x0331 | ACTPOS | aktuelle Position auslesen                             / setzen                         |
| 0x0332 | AMBIENT_TEMP | Umgebungstemperatur abfragen                                                            |
| 0x0333 | CAS_ALLOWED | Status CAS Freigabe abfragen                           / setzen                         |
| 0x0339 | SHOCK_OFFSET_MAX | Max. Ausloese-Offset bei RRD abfragen                  / setzen                         |
| 0x033A | CAL_VOLT | Kalibrierwert der Batteriespannung abfragen            / setzen                         |
| 0x033D | SOFT_START_RISE | SoftStart Rampe abfragen                               / setzen                         |
| 0x0340 | VBAT | Batteriespannung abfragen                                                               |
| 0x0348 | CAL_TEMP | Kalibrierwert der Umgebungstemperatur abfragen         / setzen                         |
| 0x034D | SPEED_OPEN | Geschwindigkeit beim Oeffnen abfragen                  / setzen                         |
| 0x034E | SEG_CAL_CLOSE_VALID | Status Polbreiten gelernt abfragen                     / setzen                         |
| 0x0351 | FORCE_EXT_MAX_DEC | RRD: Max. Kraft Dekrement abfragen                     / setzen                         |
| 0x0352 | FORCE_EXT_MIN_DEC | RRD: Min. Kraft Dekrement abfragen                     / setzen                         |
| 0x0354 | CATCH_RANGE_OI | Fangfenster unten/innen abfragen                       / setzen                         |
| 0x0355 | CATCH_RANGE_OO | Fangfenster unten/aussen abfragen                      / setzen                         |
| 0x0357 | CATCH_RANGE_CO | Fangfenster oben/aussen abfragen                       / setzen                         |
| 0x035D | FORCE_THRESH_20N | Ausloese-Offset im 20N-Bereich abfragen                / setzen                         |
| 0x035E | FORCE_THRESH_65N | Ausloese-Offset im 65N-Bereich abfragen                / setzen                         |
| 0x035F | FORCE_THRESH_SEAL | zusaetzlicher Ausloese-Offset im Dichtungsbereich abfragen                  / setzen    |
| 0x036C | VMAX_PRESS_POSOPEN | Max. Spannung beim Nachdruecken im unteren mechan. Anschlag abfragen        / setzen    |
| 0x0378 | TEMP_COIL | Motorwicklungstemperatur abfragen                      / setzen                         |
| 0x03CA | PosOpen150N | Offen Position fuer PseudoNorm                         / setzen                         |
| 0x03CB | Pos150Nstart | Position bei der 150N beginnt                          / setzen                         |
| 0x03CC | Pos150Nend | Position bei der 150N endet                            / setzen                         |
| 0x03CD | TRACK_LIMIT_150N | 150N Bereich Tracking abfragen                         / setzen                         |
| 0x03CE | FORCE_THRESH_150N | Ausloese-Offset im 150N-Bereich abfragen               / setzen                         |
| 0x03CF | Pos150Nneeded | Position ab der 150N benoetigt wird                    / setzen                         |
| 0x0501 | ACTU_ALLOWED | Kennlinie aktualisieren erlaubt abfragen               / setzen                         |
| 0x0503 | RRD_ALLOWED | Ruettelerkennung erlaubt abfragen                      / setzen                         |
| 0x050A | CFL150N_ALLOWED | cfl 150N waehrend autoinit erlaubt                     / setzen                         |
| 0x050C | LEARN_POS_OPEN_ALLOWED | Lernen des Fensterweges erlaubt abfragen               / setzen                         |
