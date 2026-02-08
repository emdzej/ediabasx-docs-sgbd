# emf_89.prg

- Jobs: [72](#jobs)
- Tables: [53](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EMF |
| ORIGIN | BMW EF-513 Martin Berndaner |
| REVISION | 5.002 |
| AUTHOR | Helbling T1211 F_Malaun, BMW EF-513 Martin_Berndaner, TRW EPB-P |
| COMMENT | N/A |
| PACKAGE | 1.52 |
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
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
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
- [SS_SOFTWARE_NR](#job-ss-software-nr) - Identdaten System Supplier Software Nummer KWP2000: $1A 94 System Supplier Software Number Modus  : Default
- [_STEUERN_EEPROM_RESET](#job-steuern-eeprom-reset) - Rücksetzen von Lernparametern, wie z.B. MAX_RECLAMP_COUNTER KWP2000: $31 StartRoutineByLocalIdentifier $25 EEPROM Reset  Vorbedingungen: keine Modus  : Default
- [STEUERN_MONTAGEMODE_AKTIVIEREN](#job-steuern-montagemode-aktivieren) - Montagemodus aktivieren KWP2000: $31 StartRoutineByLocalIdentifier $26 ActivateAssemblyMode  Vorbedingungen: - Bremse nicht geschlossen - Funktion "Feststellen" und "Lösen" verfügbar  Modus  : Default
- [STEUERN_MONTAGEMODE_DEAKTIVIEREN](#job-steuern-montagemode-deaktivieren) - Montagemodus deaktivieren KWP2000: $31 StartRoutineByLocalIdentifier $27 DeactivateAssemblyMode  Vorbedingungen: - Bremse geöffnet  Modus  : Default
- [STEUERN_MONTAGEPOSITON_ANFAHREN](#job-steuern-montagepositon-anfahren) - Montagepsotion anfahren KWP2000: $31 StartRoutineByLocalIdentifier $28 EnterMaintenancePosition  Vorbedingungen: - Bremse geöffnet - Funktion "Feststellen" und "Lösen" verfügbar  Modus  : Default
- [STEUERN_ANLEGEMODUS_CHECK](#job-steuern-anlegemodus-check) - Anlegemoduscheck aktivieren KWP2000: $31 StartRoutineByLocalIdentifier $2A ApplyingCheck  Vorbedingungen: - Bremse geöffnet - Funktion "Feststellen" und "Lösen" verfügbar  Modus  : Default
- [_STEUERN_AUSGABE_ENTWICKLERBOTSCHAFTEN](#job-steuern-ausgabe-entwicklerbotschaften) - Ausgabe von Entwicklerbotschaften aus-/einschalten KWP2000: $31 StartRoutineByLocalIdentifier $40 SendDevelopMessages  Vorbedingungen: keine  Modus  : Default
- [STEUERN_FUNKTIONSERGEBNISSE_LESSEN](#job-steuern-funktionsergebnisse-lessen) - Auslesen der Funktionsergebisse einer zuvor gestarteten Bremsenansteuerung KWP2000: $33 RequestRoutineResultByLocalIdentifier $28 EnterMaintenancePosition $2A ApplyingCheck  Vorbedingungen: keine  Modus  : Default
- [STATUS_SYSTEM_KONFIGURATION](#job-status-system-konfiguration) - Auslesen der Systemkonfiguration KWP2000: $21 ReadDataByLocalIdentifier $01 ReadSystemConfiguration Modus  : Default
- [STATUS_VERSORGUNGSSPANNUNGEN](#job-status-versorgungsspannungen) - Auslesen der Versgungsspannungen KWP2000: $21 ReadDataByLocalIdentifier $02 ReadSupplyVoltages Modus  : Default
- [STATUS_FAHRZEUGGESCHWINDIGKEITEN](#job-status-fahrzeuggeschwindigkeiten) - Auslesen der Fahrzeuggeschwindigkeiten KWP2000: $21 ReadDataByLocalIdentifier $03 ReadVehilceSpeed Modus  : Default
- [STATUS_EINGANGSSIGNALE](#job-status-eingangssignale) - Auslesen der (CAN-)Eingangssignale KWP2000: $21 ReadDataByLocalIdentifier $04 ReadInputSignals Modus  : Default
- [STATUS_ANALOGE_SCHALTER_SIGNALE](#job-status-analoge-schalter-signale) - Auslesen der Schalterspannungen KWP2000: $21 ReadDataByLocalIdentifier $05 ReadAnalogSwitchSignals Modus  : Default
- [STATUS_BREMSEN_SYSTEMSTATUS](#job-status-bremsen-systemstatus) - Auslesen des Bremsen und Systemstatus KWP2000: $21 ReadDataByLocalIdentifier $06 ReadBrakeAndSystemState Modus  : Default
- [STATUS_RADMOMENTEN_SIGNALE](#job-status-radmomenten-signale) - Auslesen der Radmomente KWP2000: $21 ReadDataByLocalIdentifier $07 ReadTorqueInterface Modus  : Default
- [STATUS_BREMSEN_TEMPERATUR](#job-status-bremsen-temperatur) - Auslesen der Bremsentemperatur KWP2000: $21 ReadDataByLocalIdentifier $08 ReadBrakeTemperature Modus  : Default
- [STATUS_CAN_NETZWERK](#job-status-can-netzwerk) - Auslesen des Status vom CAN Netzwerkmanagement KWP2000: $21 ReadDataByLocalIdentifier $09 ReadCANNetworkState Modus  : Default
- [STATUS_FESTSTELL_BETAETIGUNGEN](#job-status-feststell-betaetigungen) - Auslesen der Feststellbetätigungszähler KWP2000: $21 ReadDataByLocalIdentifier $0A ReadBrakeApplyActivity Modus  : Default
- [STATUS_NACHSPANN_BETAETIGUNGEN](#job-status-nachspann-betaetigungen) - Auslesen der Nachspannbetätigungszähler KWP2000: $21 ReadDataByLocalIdentifier $0B ReadReclampingActivity Modus  : Default
- [STATUS_CC_BOTSCHAFTEN](#job-status-cc-botschaften) - Auslesen der Stati der CC Botschaften KWP2000: $21 ReadDataByLocalIdentifier $0C ReadDashboardRequests Modus  : Default
- [STATUS_BEDIENELEMENT_BETAETIGUNGEN](#job-status-bedienelement-betaetigungen) - Auslesen der Bedienelementbetätigungszähler KWP2000: $21 ReadDataByLocalIdentifier $0D ReadSwitchApplyActivity Modus  : Default
- [STATUS_MOTOR_TEMP_SIGNALE](#job-status-motor-temp-signale) - Auslesen der NTC-Sensortemperatur KWP2000: $21 ReadDataByLocalIdentifier $0E ReadNTCSensorTemperature Modus  : Default
- [STATUS_SPANNKRAFT](#job-status-spannkraft) - Auslesen der erreichten Spannkraft der Aktuatoren KWP2000: $21 ReadDataByLocalIdentifier $0F ReadAchivedClampForce Modus  : Default
- [_STEUERN_STEUERGERAET_CODIEREN](#job-steuern-steuergeraet-codieren) - Dieser Job bietet die Moeglichkeit an, die EMF zu Codieren KWP2000: $2E WriteDataByIdentifier $3000 EMFCodingBlock Modus  : Default
- [_STATUS_CODIERUNG](#job-status-codierung) - Auslesen der EMF Codierung KWP2000: $22 ReadDataByCommonIdentifier $3000 EMFCodingBlock Modus  : Default

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

<a id="job-ss-software-nr"></a>
### SS_SOFTWARE_NR

Identdaten System Supplier Software Nummer KWP2000: $1A 94 System Supplier Software Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SS_SW_NR1 | string | SS_Software Nummer1 |
| SS_SW_NR2 | string | SS_Software Nummer2 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eeprom-reset"></a>
### _STEUERN_EEPROM_RESET

Rücksetzen von Lernparametern, wie z.B. MAX_RECLAMP_COUNTER KWP2000: $31 StartRoutineByLocalIdentifier $25 EEPROM Reset  Vorbedingungen: keine Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-montagemode-aktivieren"></a>
### STEUERN_MONTAGEMODE_AKTIVIEREN

Montagemodus aktivieren KWP2000: $31 StartRoutineByLocalIdentifier $26 ActivateAssemblyMode  Vorbedingungen: - Bremse nicht geschlossen - Funktion "Feststellen" und "Lösen" verfügbar  Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ASSEMBLYMODE | string | Montagemode |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-montagemode-deaktivieren"></a>
### STEUERN_MONTAGEMODE_DEAKTIVIEREN

Montagemodus deaktivieren KWP2000: $31 StartRoutineByLocalIdentifier $27 DeactivateAssemblyMode  Vorbedingungen: - Bremse geöffnet  Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ASSEMBLYMODE | string | Montagemode |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-montagepositon-anfahren"></a>
### STEUERN_MONTAGEPOSITON_ANFAHREN

Montagepsotion anfahren KWP2000: $31 StartRoutineByLocalIdentifier $28 EnterMaintenancePosition  Vorbedingungen: - Bremse geöffnet - Funktion "Feststellen" und "Lösen" verfügbar  Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ASSEMBLYMODE | string | Montagemode |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-anlegemodus-check"></a>
### STEUERN_ANLEGEMODUS_CHECK

Anlegemoduscheck aktivieren KWP2000: $31 StartRoutineByLocalIdentifier $2A ApplyingCheck  Vorbedingungen: - Bremse geöffnet - Funktion "Feststellen" und "Lösen" verfügbar  Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ausgabe-entwicklerbotschaften"></a>
### _STEUERN_AUSGABE_ENTWICKLERBOTSCHAFTEN

Ausgabe von Entwicklerbotschaften aus-/einschalten KWP2000: $31 StartRoutineByLocalIdentifier $40 SendDevelopMessages  Vorbedingungen: keine  Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENDEN | int | Ausgabe von Entwicklerbotschaften Werte: 1 = ein, 0 = aus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DEVELOP_MESSAGES | string | Ausgabe von Entwicklerbotschaften Werte: 1 = aktiviert, 0 = deaktiviert table DevelopMessages TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-funktionsergebnisse-lessen"></a>
### STEUERN_FUNKTIONSERGEBNISSE_LESSEN

Auslesen der Funktionsergebisse einer zuvor gestarteten Bremsenansteuerung KWP2000: $33 RequestRoutineResultByLocalIdentifier $28 EnterMaintenancePosition $2A ApplyingCheck  Vorbedingungen: keine  Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ROUTINEID | int | Routine ID |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SERVICE | string | Diagnose Service table Service TEXT |
| STAT_SERVICE_STATUS | string | Status des Diagnose Service table ServiceStatus TEXT |
| STAT_CUT_OFF_CURRENT_L_WERT | int | Erreichter Abschaltstrom links Bereich: 0 bis 25,4 [Ampere] Auflösung: 0,1 A/Bit |
| STAT_CUT_OFF_CURRENT_L_EINH | string | Ampere |
| STAT_CUT_OFF_CURRENT_R_WERT | int | Erreichter Abschaltstrom rechts Bereich: 0 bis 25,4 [Ampere] Auflösung: 0,1 A/Bit |
| STAT_CUT_OFF_CURRENT_R_EINH | string | Ampere |
| STAT_BRAKE_STATE_HL | string | Bremsen Status hinten links table BremsenStatus TEXT |
| STAT_BRAKE_STATE_HR | string | Bremsen Status hinten rechts table BremsenStatus TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-system-konfiguration"></a>
### STATUS_SYSTEM_KONFIGURATION

Auslesen der Systemkonfiguration KWP2000: $21 ReadDataByLocalIdentifier $01 ReadSystemConfiguration Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ASSEMBLY_CHECK | string | AssemblyCheck table AssemblyCheck TEXT |
| STAT_HU_FUNCTION | string | HU Funktion table Aktiv TEXT |
| STAT_ASSEMBLY_MODE | string | Montagemodus table Aktiv TEXT |
| STAT_TRANSMISSION_TYPE | string | Getriebeart table Getriebeart TEXT |
| STAT_FAIL_STATE_L | string | Fehlerstatus Aktuator links table Fehlerstatus TEXT |
| STAT_FAIL_STATE_R | string | Fehlerstatus Aktuator rechts table Fehlerstatus TEXT |
| STAT_NVM_CONFIG_ID | int | Version der NVM Konfiguration |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-versorgungsspannungen"></a>
### STATUS_VERSORGUNGSSPANNUNGEN

Auslesen der Versgungsspannungen KWP2000: $21 ReadDataByLocalIdentifier $02 ReadSupplyVoltages Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ECU_SUPPLY_VOLTAGE_WERT | int | ECU Versorgungsspannung Bereich: 0 bis 25,5 [Volt] Auflösung: 0,1 V/Bit |
| STAT_ECU_SUPPLY_VOLTAGE_EINH | string | Volt |
| STAT_WAKEUP_VOLTAGE_WERT | int | Wakeup Spannung Bereich: 0 bis 25,5 [Volt] Auflösung: 0,1 V/Bit |
| STAT_WAKEUP_VOLTAGE_EINH | string | Volt |
| STAT_MOTOR_SUPPLY_VOLTAGE_L_WERT | int | Motor Versorgungsspannung links Bereich: 0 bis 25,5 [Volt] Auflösung: 0,1 V/Bit |
| STAT_MOTOR_SUPPLY_VOLTAGE_L_EINH | string | Volt |
| STAT_MOTOR_SUPPLY_VOLTAGE_R_WERT | int | Motor Versorgungsspannung rechts Bereich: 0 bis 25,5 [Volt] Auflösung: 0,1 V/Bit |
| STAT_MOTOR_SUPPLY_VOLTAGE_R_EINH | string | Volt |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrzeuggeschwindigkeiten"></a>
### STATUS_FAHRZEUGGESCHWINDIGKEITEN

Auslesen der Fahrzeuggeschwindigkeiten KWP2000: $21 ReadDataByLocalIdentifier $03 ReadVehilceSpeed Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VEHICLE_SPEED_WERT | int | Fahrzeuggeschwindikeit Bereich: 0 bis 320,0 [km/h] Auflösung: 0,1 km/h / Bit |
| STAT_VEHICLE_SPEED_EINH | string | km/h |
| STAT_DFA_EMF_FREQUENZ | string | Frequenz des DFA_EMF Signals vom DSC 500 Hz (unplausible Geschwindigkeit) 250 Hz (0,0 ... 0,5 km/h) 125 Hz (0,5 ... 3,0 km/h) 62,5 Hz (3,0 ... 10,0 km/h) 31,25 Hz (10,0 ... 20,0 km/h) 15,625 Hz (20,0 km/h ... Vmax) |
| STAT_DFA_LOWER_THRES_WERT | int | Untere Geschwindigkeitsschwelle des DFA_EMF Signals Bereich: 0 bis 320,0 [km/h] Auflösung: 0,1 km/h / Bit |
| STAT_DFA_LOWER_THRES_EINH | string | km/h |
| STAT_DFA_UPPER_THRES_WERT | int | Untere Geschwindigkeitsschwelle des DFA_EMF Signals Bereich: 0 bis 320,0 [km/h] Auflösung: 0,1 km/h / Bit |
| STAT_DFA_UPPER_THRES_EINH | string | km/h |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eingangssignale"></a>
### STATUS_EINGANGSSIGNALE

Auslesen der (CAN-)Eingangssignale KWP2000: $21 ReadDataByLocalIdentifier $04 ReadInputSignals Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EMF_SWITCH | string | Status EMF Schalter table StatusEMFSchalter TEXT |
| STAT_EMF_SWITCH_FEHLER | string | Status Fehlerzustand EMF Schalter table StatusEMFSchalterfehler TEXT |
| STAT_BLS | string | Status Bremslicht Schalter table BLSStatus TEXT |
| STAT_ANGLE_THROTTLE_PEDAL_WERT | int | Winkel Fahrpedal Bereich: 0 bis 100 [%] Auflösung: 0,5 %/Bit |
| STAT_ANGLE_THROTTLE_PEDAL_EINH | string | Prozent |
| STAT_BRAKE_PRES_WERT | int | Bremsdruck Bereich: 0 bis 254 [bar] Auflösung: 1 bar/Bit |
| STAT_BRAKE_PRES_EINH | string | bar |
| STAT_KL15 | string | Status Klemme 15 table KL15Status TEXT |
| STAT_KL50 | string | Status Klemme 50 table KL50Status TEXT |
| STAT_KLR | string | Status Klemme Radio table KLRStatus TEXT |
| STAT_ZAS | string | Status ZAS table ZASStatus TEXT |
| STAT_GEAR | string | Status Gang Getriebe table GangStatus TEXT |
| STAT_CLUTCH | string | Status Kupplung table KupplungStatus TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analoge-schalter-signale"></a>
### STATUS_ANALOGE_SCHALTER_SIGNALE

Auslesen der Schalterspannungen KWP2000: $21 ReadDataByLocalIdentifier $05 ReadAnalogSwitchSignals Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ASS1_WERT | int | Schaltersignal 1 Bereich: 0 bis 25,5 [Volt] Auflösung: 0,1 V/Bit |
| STAT_ASS1_EINH | string | Volt |
| STAT_ASS2_WERT | int | Schaltersignal 2 Bereich: 0 bis 25,5 [Volt] Auflösung: 0,1 V/Bit |
| STAT_ASS2_EINH | string | Volt |
| STAT_ASS3_WERT | int | Schaltersignal 3 Bereich: 0 bis 25,5 [Volt] Auflösung: 0,1 V/Bit |
| STAT_ASS3_EINH | string | Volt |
| STAT_ASS4_WERT | int | Schaltersignal 4 Bereich: 0 bis 25,5 [Volt] Auflösung: 0,1 V/Bit |
| STAT_ASS4_EINH | string | Volt |
| STAT_ASS5_WERT | int | Schaltersignal 5 Bereich: 0 bis 25,5 [Volt] Auflösung: 0,1 V/Bit |
| STAT_ASS5_EINH | string | Volt |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bremsen-systemstatus"></a>
### STATUS_BREMSEN_SYSTEMSTATUS

Auslesen des Bremsen und Systemstatus KWP2000: $21 ReadDataByLocalIdentifier $06 ReadBrakeAndSystemState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BRAKE_STATE_HL | string | Bremsen Status hinten links table BremsenStatus TEXT |
| STAT_BRAKE_STATE_HR | string | Bremsen Status hinten rechts table BremsenStatus TEXT |
| STAT_MODE_CONTROLLER_STATE | string | Modecontroller Status table ModecontrollerStatus TEXT |
| STAT_SHUTDOWN_MODE | string | Stillegungs Status table EPBStillegungsStatus TEXT |
| STAT_CUT_OFF_CURRENT_L_WERT | int | Erreichter Abschaltstrom links Bereich: 0 bis 25,4 [Ampere] Auflösung: 0,1 A/Bit |
| STAT_CUT_OFF_CURRENT_L_EINH | string | Ampere |
| STAT_CUT_OFF_CURRENT_R_WERT | int | Erreichter Abschaltstrom rechts Bereich: 0 bis 25,4 [Ampere] Auflösung: 0,1 A/Bit |
| STAT_CUT_OFF_CURRENT_R_EINH | string | Ampere |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-radmomenten-signale"></a>
### STATUS_RADMOMENTEN_SIGNALE

Auslesen der Radmomente KWP2000: $21 ReadDataByLocalIdentifier $07 ReadTorqueInterface Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_REQ_TORQUE_STATE | string | Status Sollwertanforderung table SollwertAnforderungStatus TEXT |
| STAT_REQ_TORQUE_WERT | int | Angefordertes Radmoment Bereich: -32000 bis 32000 [Nm] Auflösung: 1 Nm/Bit |
| STAT_REQ_TORQUE_EINH | string | Nm |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bremsen-temperatur"></a>
### STATUS_BREMSEN_TEMPERATUR

Auslesen der Bremsentemperatur KWP2000: $21 ReadDataByLocalIdentifier $08 ReadBrakeTemperature Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BRAKE_TEMP_RL_WERT | int | Bremsentemperatur hinten links Bereich: 0 bis 3727 [°C] Auflösung: 1 °C/Bit |
| STAT_BRAKE_TEMP_RL_EINH | string | °C |
| STAT_BRAKE_TEMP_RR_WERT | int | Bremsentemperatur hinten rechts Bereich: 0 bis 3727 [°C] Auflösung: 1 °C/Bit |
| STAT_BRAKE_TEMP_RR_EINH | string | °C |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-netzwerk"></a>
### STATUS_CAN_NETZWERK

Auslesen des Status vom CAN Netzwerkmanagement KWP2000: $21 ReadDataByLocalIdentifier $09 ReadCANNetworkState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_OSEK_NM | string | Status vom OSEK Netzwerkmanagement table CANNetworkStatus TEXT |
| STAT_INTERNAL_NM | string | Interner Netzwerkstatus table InternerNetworkStatus TEXT |
| STAT_SHUTDOWN_MODE | string | EPB Stillegungsstufe table EPBStillegungsStatus TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-feststell-betaetigungen"></a>
### STATUS_FESTSTELL_BETAETIGUNGEN

Auslesen der Feststellbetätigungszähler KWP2000: $21 ReadDataByLocalIdentifier $0A ReadBrakeApplyActivity Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_APPLY_COUNTER_L | unsigned int | Betätigungszähler links |
| STAT_APPLY_COUNTER_R | unsigned int | Betätigungszähler rechts |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-nachspann-betaetigungen"></a>
### STATUS_NACHSPANN_BETAETIGUNGEN

Auslesen der Nachspannbetätigungszähler KWP2000: $21 ReadDataByLocalIdentifier $0B ReadReclampingActivity Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RECLAMPING_COUNTER | unsigned int | Gesamtzahl der Nachspannzähler absolut |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cc-botschaften"></a>
### STATUS_CC_BOTSCHAFTEN

Auslesen der Stati der CC Botschaften KWP2000: $21 ReadDataByLocalIdentifier $0C ReadDashboardRequests Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CC_1E2 | string | CC Meldung 1E2: Gesamtstillegung table CCMeldungen TEXT |
| STAT_CC_1E1 | string | CC Meldung 1E1: Elektromechanischer Modus table CCMeldungen TEXT |
| STAT_CC_1E0 | string | CC Meldung 1E0: Eingeschränkter hydraulischer Modus table CCMeldungen TEXT |
| STAT_CC_19A | string | CC Meldung 19A: Leitungsfehler table CCMeldungen TEXT |
| STAT_CC_30 | string | CC Meldung 30: Tasterfehler table CCMeldungen TEXT |
| STAT_CC_38 | string | CC Meldung 38: Festgestellt table CCMeldungen TEXT |
| STAT_CC_192 | string | CC Meldung 192: Bremse treten zum Lösen table CCMeldungen TEXT |
| STAT_CC_2C1 | string | CC Meldung 2C1: Zusätzlich P einlegen table CCMeldungen TEXT |
| STAT_CC_2C2 | string | CC Meldung 2C2: Fußbremse oder Kupplung treten table CCMeldungen TEXT |
| STAT_CC_37 | string | CC Meldung 37: Bremse lösen zum Anfahren table CCMeldungen TEXT |
| STAT_CC_FD | string | CC Meldung FD: Montagemode table CCMeldungen TEXT |
| STAT_ILLUMINATION | int | Dimmwert für Hinterleuchtung der Schalter Bereich: 0 (Poti Min) bis 253 (Poti Max) 254: Lichtschalter aus 255: Signal ungültig |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bedienelement-betaetigungen"></a>
### STATUS_BEDIENELEMENT_BETAETIGUNGEN

Auslesen der Bedienelementbetätigungszähler KWP2000: $21 ReadDataByLocalIdentifier $0D ReadSwitchApplyActivity Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SWITCH_APPLY_COUNTER | unsigned int | Betätigungszähler Schliessen |
| STAT_SWITCH_RELEASE_COUNTER | unsigned int | Betätigungszähler Öffnen |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motor-temp-signale"></a>
### STATUS_MOTOR_TEMP_SIGNALE

Auslesen der NTC-Sensortemperatur KWP2000: $21 ReadDataByLocalIdentifier $0E ReadNTCSensorTemperature Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AKT_TEMP_L_WERT | int | NTC-Sensortemperatur hinten links Bereich: -40 bis 200 [°C] Auflösung: 1 °C/Bit |
| STAT_AKT_TEMP_L_EINH | string | °C |
| STAT_AKT_TEMP_R_WERT | int | NTC-Sensortemperatur hinten rechts Bereich: -40 bis 200 [°C] Auflösung: 1 °C/Bit |
| STAT_AKT_TEMP_R_EINH | string | °C |
| STAT_K_FACTOR_L_WERT | int | Korrektur Faktor links Bereich: -127 bis +127 |
| STAT_K_FACTOR_R_WERT | int | Korrektur Faktor rechts Bereich: -127 bis +127 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spannkraft"></a>
### STATUS_SPANNKRAFT

Auslesen der erreichten Spannkraft der Aktuatoren KWP2000: $21 ReadDataByLocalIdentifier $0F ReadAchivedClampForce Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ACHIVED_CLAMP_L_WERT | int | Erreichte Spannkraft links Bereich: 0 bis 25,4 [kN] Auflösung: 0,1 A/Bit |
| STAT_ACHIVED_CLAMP_L_EINH | string | kN |
| STAT_ACHIVED_CLAMP_R_WERT | int | Erreichte Spannkraft rechts Bereich: 0 bis 25,4 [kN] Auflösung: 0,1 A/Bit |
| STAT_ACHIVED_CLAMP_R_EINH | string | kN |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-steuergeraet-codieren"></a>
### _STEUERN_STEUERGERAET_CODIEREN

Dieser Job bietet die Moeglichkeit an, die EMF zu Codieren KWP2000: $2E WriteDataByIdentifier $3000 EMFCodingBlock Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TRANSMISSION_TYPE | int | Getriebeart Werte: 0 = Automatik, 1 = Manuell Default: 0 = Automatik |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung"></a>
### _STATUS_CODIERUNG

Auslesen der EMF Codierung KWP2000: $22 ReadDataByCommonIdentifier $3000 EMFCodingBlock Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TRANSMISSION_TYPE | string | Getriebeart table Getriebeart TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (121 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (130 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (8 × 9)
- [FARTTYP](#table-farttyp) (2 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (13 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (37 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (8 × 9)
- [IARTTYP](#table-iarttyp) (1 × 5)
- [IARTTEXTEINDIVIDUELL](#table-iarttexteindividuell) (6 × 2)
- [BETRIEBSMODUS_BYTE1](#table-betriebsmodus-byte1) (9 × 2)
- [BETRIEBSMODUS_BYTE2](#table-betriebsmodus-byte2) (9 × 2)
- [BETRIEBSMODUS_BYTE3](#table-betriebsmodus-byte3) (9 × 2)
- [UW1_TABELLE](#table-uw1-tabelle) (1 × 4)
- [UW2_TABELLE](#table-uw2-tabelle) (1 × 5)
- [DEVELOPMESSAGES](#table-developmessages) (2 × 2)
- [BREMSENSTATUS](#table-bremsenstatus) (9 × 2)
- [MODECONTROLLERSTATUS](#table-modecontrollerstatus) (9 × 2)
- [EPBSTILLEGUNGSSTATUS](#table-epbstillegungsstatus) (4 × 2)
- [CANNETWORKSTATUS](#table-cannetworkstatus) (5 × 2)
- [INTERNERNETWORKSTATUS](#table-internernetworkstatus) (3 × 2)
- [CCMELDUNGEN](#table-ccmeldungen) (12 × 2)
- [STATUSEMFSCHALTER](#table-statusemfschalter) (9 × 2)
- [STATUSEMFSCHALTERFEHLER](#table-statusemfschalterfehler) (6 × 2)
- [BLSSTATUS](#table-blsstatus) (4 × 2)
- [SOLLWERTANFORDERUNGSTATUS](#table-sollwertanforderungstatus) (5 × 2)
- [KL15STATUS](#table-kl15status) (4 × 2)
- [KL50STATUS](#table-kl50status) (4 × 2)
- [KLRSTATUS](#table-klrstatus) (4 × 2)
- [ZASSTATUS](#table-zasstatus) (4 × 2)
- [GANGSTATUS](#table-gangstatus) (16 × 2)
- [KUPPLUNGSTATUS](#table-kupplungstatus) (4 × 2)
- [GETRIEBEART](#table-getriebeart) (2 × 2)
- [FEHLERSTATUS](#table-fehlerstatus) (2 × 2)
- [ASSEMBLYCHECK](#table-assemblycheck) (2 × 2)
- [AKTIV](#table-aktiv) (2 × 2)
- [EOLRESET](#table-eolreset) (2 × 2)
- [SERVICESTATUS](#table-servicestatus) (3 × 2)
- [SERVICE](#table-service) (2 × 2)
- [DFA_EMF](#table-dfa-emf) (7 × 2)

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

Dimensions: 121 rows × 2 columns

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
| 0xAC | SMR Automotive Mirrors |
| 0xAD | So.Ge.Mi. |
| 0xAE | MTA |
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

Dimensions: 130 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x600C | Bremsscheibe hinten links nicht erreicht |
| 0x600D | Bremsscheibe hinten rechts nicht erreicht |
| 0x600E | Feststellmotor links Spannkraft nicht erreicht |
| 0x600F | Feststellmotor rechts Spannkraft nicht erreicht |
| 0x6010 | Feststellmotor links mechanischer Fehler |
| 0x6011 | Feststellmotor rechts mechanischer Fehler |
| 0x6012 | Feststellmotor links mechanische Reibung zu gross oder mechanischer Fehler |
| 0x6013 | Feststellmotor rechts mechanische Reibung zu gross oder mechanischer Fehler |
| 0x6015 | Steuergerät nicht codiert |
| 0x6016 | Interner Steuergerätefehler - Systemfunktionstest |
| 0x6017 | Rollüberwachungslimit wurde erreicht |
| 0x6018 | Bedienelement Leitung 1 - Kurzschluss gegen U-Batt |
| 0x6019 | Bedienelement Leitung 1 - Leitungsunterbrechung oder Kurzschluss gegen Masse |
| 0x601A | Bedienelement Leitung 1 - Leitungsunterbrechung |
| 0x601B | Bedienelement Leitung 2 - Kurzschluss gegen U-Batt |
| 0x601C | Bedienelement Leitung 2 - Kurzschluss gegen Masse |
| 0x601D | Bedienelement Leitung 2 - Leitungsunterbrechung |
| 0x601E | Bedienelement Leitung 3 - Kurzschluss gegen U-Batt |
| 0x601F | Bedienelement Leitung 3 - Kurzschluss gegen Masse |
| 0x6020 | Bedienelement Leitung 3 - Leitungsunterbrechung |
| 0x6021 | Bedienelement Leitung 4 - Kurzschluss gegen U-Batt |
| 0x6022 | Bedienelement Leitung 4 - Kurzschluss gegen Masse |
| 0x6023 | Bedienelement Leitung 4 - Leitungsunterbrechung |
| 0x6024 | Bedienelement Leitung 5 - Kurzschluss gegen U-Batt |
| 0x6025 | Bedienelement Leitung 5 - Kurzschluss gegen Masse |
| 0x6026 | Bedienelement Leitung 5 - Leitungsunterbrechung |
| 0x6027 | Bedienelement für elektrische Feststellbremse - mehr als ein Leitungssignal nicht gültig |
| 0x6028 | Bedienelement für elektrische Feststellbremse - unstabiler Zustand |
| 0x6029 | Bedienelement für elektrische Feststellbremse - permanent betätigt |
| 0x602A | Bedienelement für elektrische Feststellbremse - nicht vorhanden |
| 0x602B | Bedienelement für elektrische Feststellbremse - unplausibles Signal |
| 0x602C | Weckleitung - Kurzschluss gegen Masse |
| 0x602D | Weckleitung unplausibel |
| 0x602E | Funktionsbeleuchtung Bedienelement - Kurzschluss gegen U-Batt |
| 0x602F | Funktionsbeleuchtung Bedienelement - Kurzschluss gegen Masse |
| 0x6030 | Versorgungsspannung - Unterspannung erkannt |
| 0x6031 | Versorgungsspannung - Überspannung erkannt |
| 0x6032 | Versorgungsspannung - Leitungsunterbrechung |
| 0x6033 | Funktionseinschränkung durch Unterspannung |
| 0x6034 | Funktionseinschränkung durch Überspannung |
| 0x6035 | Feststellmotor links Spannungsversorgung - Signal oder Wert oberhalb der Schwelle |
| 0x6036 | Feststellmotor rechts Spannungsversorgung - Signal oder Wert oberhalb der Schwelle |
| 0x6037 | Feststellmotor links Spannungsversorgung - Leitungsunterbrechnung |
| 0x6038 | Feststellmotor rechts Spannungsversorgung - Leitungsunterbrechnung |
| 0x6039 | Feststellmotor links Spannungsversorgung - Kein Signal oder Wert |
| 0x603A | Feststellmotor rechts Spannungsversorgung - Kein Signal oder Wert |
| 0x603B | Feststellmotor links Spannungsversorgung - unplausibles Signal oder Wert |
| 0x603C | Feststellmotor rechts Spannungsversorgung - unplausibles Signal oder Wert |
| 0x603D | Steuergerät linker Kanal - Leitungsunterbrechnung oder Kurzschluss gegen Masse |
| 0x603E | Steuergerät rechter Kanal - Leitungsunterbrechnung oder Kurzschluss gegen Masse |
| 0x603F | Steuergerät linker Kanal - Kein Signal oder Wert |
| 0x6040 | Steuergerät rechter Kanal - Kein Signal oder Wert |
| 0x6041 | Feststellmotor links schwergängig |
| 0x6042 | Feststellmotor rechts schwergängig |
| 0x6043 | Temperatursensor Feststellmotor links - Kurzschluss gegen Masse |
| 0x6044 | Temperatursensor Feststellmotor rechts - Kurzschluss gegen Masse |
| 0x6045 | Temperatursensor Feststellmotor links - Kurzschluss gegen Masse, Leitungsunterbrechung oder Sensorfehler |
| 0x6046 | Temperatursensor Feststellmotor rechts - Kurzschluss gegen Masse, Leitungsunterbrechung oder Sensorfehler |
| 0x6047 | Temperatursensor Feststellmotor - Abweichung zu groß |
| 0x6048 | Feststellmotor links - Stromkalibierfehler |
| 0x6049 | Feststellmotor rechts - Stromkalibierfehler |
| 0x604A | Feststellmotor links Versorgungsleitung - Kurzschluss gegen U-Batt |
| 0x604B | Feststellmotor rechts Versorgungsleitung - Kurzschluss gegen U-Batt |
| 0x656C | Feststellmotor links Versorgungsleitung - Kurzschluss gegen Masse |
| 0x656D | Feststellmotor rechts Versorgungsleitung - Kurzschluss gegen Masse |
| 0x656E | Motor Zuleitung B+ links - Leitungsunterbrechung |
| 0x656F | Motor Zuleitung B+ rechts - Leitungsunterbrechung |
| 0x6570 | Stillegungsstufe 1E1 - Elektromechanischer Modus - Schnittstelle zum DSC defekt |
| 0x6571 | Stillegungsstufe 1E1 - Elektromechanischer Modus - DSC setzt dynamische Abbremsung nicht um |
| 0x6572 | Stillegungsstufe 1E1 - Elektromechanischer Modus - DSC meldet dynamische Abbremsung ohne Anforderung von EMF |
| 0x6573 | Stillegungsstufe 1E0 - Eingeschränkter hydraulischer Modus - DSC sendet ungültige DFA_EMF Frequenz |
| 0x6574 | Stillegungsstufe 1E0 - Eingeschränkter hydraulischer Modus - DSC sendet nicht erlaubte DFA_EMF Frequenz |
| 0x6575 | Stillegungsstufe 1E0 - Eingeschränkter hydraulischer Modus - Fahrzeuggeschwindigkeit (CAN) und DFA_EMF Frequenz nicht plausibel |
| 0x6576 | Stillegungsstufe 1E2 - Gesamtstilllegung - Fahrzeuggeschwindigkeit ungültig |
| 0x6577 | Interner Steuergerätefehler - Steuergeräte-Kalibrierdaten ungültig |
| 0x6578 | Interner Steuergerätefehler - Freigabeleitung des Relais nicht gesetzt |
| 0x6579 | Interner Steuergerätefehler - Main Micro Checksumme fehlerhaft |
| 0x657A | Interner Steuergerätefehler - Main Micro Update Counter fehlerhaft |
| 0x657B | Interner Steuergerätefehler - Failsafe Micro Update Counter fehlerhaft |
| 0x657C | Interner Steuergerätefehler - Failsafe Micro Checksumme fehlerhaft |
| 0x657D | Interner Steuergerätefehler - Spannung im Failsafe Micro außerhalb dem spez. Wertebereich |
| 0x657E | Interner Steuergerätefehler - Referenzspannung ungültig |
| 0x657F | Interner Steuergerätefehler - Bedienelement für elektrische Feststellbremse vom Failsafe Micro |
| 0x6580 | Funktionsbeleuchtung Bedienelement - Leitungsunterbrechung |
| 0x6581 | Bremsenstatus ungleich |
| 0x6582 | Fahrzeug rollt trotz Nachspannen |
| 0x6583 | Taster Richtung Ziehen Defekt |
| 0x6584 | Taster Richtung Drücken Defekt |
| 0x6585 | TRW Dummy DTC 10 |
| 0x6586 | TRW Dummy DTC 11 |
| 0x6587 | TRW Dummy DTC 12 |
| 0x6588 | TRW Dummy DTC 13 |
| 0xD387 | CAN Bus |
| 0xD395 | Botschaft TORQUE_1 (ID:0xA8) - Fehler in Alive-Zähler |
| 0xD396 | Botschaft TORQUE_1 (ID:0xA8) - Timeout |
| 0xD397 | Botschaft TORQUE_1 (ID:0xA8) - Fehler in Checksumme oder DLC |
| 0xD398 | Botschaft TORQUE_3 (ID:0xAA) - Fehler in Alive-Zähler |
| 0xD399 | Botschaft TORQUE_3 (ID:0xAA) - Timeout |
| 0xD39A | Botschaft TORQUE_3 (ID:0xAA) - Fehler in Checksumme oder DLC |
| 0xD39B | Botschaft GESCHWINDIGKEIT (ID:0x1A0) - Fehler in Alive-Zähler |
| 0xD39C | Botschaft GESCHWINDIGKEIT (ID:0x1A0) - Timeout |
| 0xD39D | Botschaft GESCHWINDIGKEIT (ID:0x1A0) - Fehler in Checksumme oder DLC |
| 0xD39E | Botschaft GETRIEBEDATEN (ID:0xBA) - Fehler in Alive-Zähler |
| 0xD39F | Botschaft GETRIEBEDATEN (ID:0xBA) - Timeout |
| 0xD3A0 | Botschaft GETRIEBEDATEN (ID:0xBA) - Fehler in Checksumme oder DLC |
| 0xD3A1 | Botschaft KLEMMENSTATUS (ID:0x130) - Fehler in Alive-Zähler |
| 0xD3A2 | Botschaft KLEMMENSTATUS (ID:0x130) - Timeout |
| 0xD3A3 | Botschaft KLEMMENSTATUS (ID:0x130) - Fehler in Checksumme oder DLC |
| 0xD3A4 | Botschaft ENGINE_1 (ID:0x1D0) - Fehler in Alive-Zähler |
| 0xD3A5 | Botschaft ENGINE_1 (ID:0x1D0) - Timeout |
| 0xD3A6 | Botschaft ENGINE_1 (ID:0x1D0) - Fehler in Checksumme oder DLC |
| 0xD3A7 | Botschaft STAT_DSC (ID:0x19E) - Fehler in Alive-Zähler |
| 0xD3A8 | Botschaft STAT_DSC (ID:0x19E) - Timeout |
| 0xD3A9 | Botschaft STAT_DSC (ID:0x19E) - Fehler in Checksumme oder DLC |
| 0xD3AA | Botschaft TEMP_BREMSE (ID:0x37E) - Fehler in Alive-Zähler |
| 0xD3AB | Botschaft TEMP_BREMSE (ID:0x37E) - Timeout |
| 0xD3AC | Botschaft TEMP_BREMSE (ID:0x37E) - Fehler in Checksumme oder DLC |
| 0xD3AD | Botschaft A_TEMP_RELATIVZEIT (ID:0x310) - Timeout |
| 0xD3AE | Botschaft A_TEMP_RELATIVZEIT (ID:0x310) - Fehler in DLC |
| 0xD3AF | Botschaft BREMSDRUCK_RAD (ID:0x2B2) - Timeout |
| 0xD3B0 | Botschaft BREMSDRUCK_RAD (ID:0x2B2) - Fehler in DLC |
| 0xD3B1 | Botschaft DIMMUNG (ID: 0x202) - Timeout |
| 0xD3B2 | Botschaft DIMMUNG (ID: 0x202) - Fehler in DLC |
| 0xD3B3 | Botschaft FLLUPT_GPWSUP (ID:0x3BE) - Timeout |
| 0xD3B4 | Botschaft FLLUPT_GPWSUP (ID:0x3BE) - Fehler in DLC |
| 0xD3B5 | Botschaft GESCHWINDIGKEIT_RAD (ID:0xCE) - Timeout |
| 0xD3B6 | Botschaft GESCHWINDIGKEIT_RAD (ID:0xCE) - Fehler in DLC |
| 0xD3B7 | Botschaft KILOMETERSTAND (ID:0x330) - Timeout |
| 0xD3B8 | Botschaft KILOMETERSTAND (ID:0x330) - Fehler in DLC |
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
| default | 0x01 | UW1_Tabelle | UW2_Tabelle | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 8 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Relativzeit | s | high | unsigned int | - | 1 | 1 | 0 |
| 0x02 | Geschwindigkeit | km/h | high | unsigned int | - | 1 | 100 | 0 |
| 0x03 | Spannung KL15 | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x04 | Spannung KL30 | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x05 | Systemzustand | HEX | - | unsigned char | - | - | - | - |
| 0x06 | Bremsenzustand hinten links | HEX | - | unsigned char | - | - | - | - |
| 0x07 | Bremsenzustand hinten rechts | HEX | - | unsigned char | - | - | - | - |
| 0x08 | Interner Fehlercode | HEX | - | unsigned char | - | - | - | - |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 2 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0xD387 | 0x9007 | 0x9006 | 0xFFFF | 0x9005 |
| 0xFFFF | 0x0000 | 0x0000 | 0x0000 | 0x0000 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 13 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb der Schwelle |
| 0x0002 | Signal oder Wert unterhalb der Schwelle |
| 0x0004 | kein Signal oder Wert |
| 0x0008 | unplausibles Signal oder Wert |
| 0x0010 | nicht belegt |
| 0x0020 | Fehler in Alive Zähler |
| 0x0040 | Timeout |
| 0x0080 | unplausibles Signal oder Fehler in Checksumme |
| 0x9005 | Übertragungsfehler |
| 0x9006 | BusOff |
| 0x9007 | Empfangsfehler |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 37 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x606C | ERD Leitungsunterbrechung oder Treiberfehler |
| 0x606D | Failsafe Micro nicht kommunikationsbereit |
| 0x606E | Main Micro Header ID fehlerhaft |
| 0x606F | Main Micro IPC Länge fehlerhaft |
| 0x6070 | Main Micro Zykluszeit fehlerhaft |
| 0x6073 | Programmablauf im Main Micro fehlerhaft |
| 0x6074 | Failsafe Micro Stack fehlerhaft |
| 0x6075 | Failsafe Micro Header ID fehlerhaft |
| 0x6078 | Failsafe Micro IPC Länge fehlerhaft |
| 0x6079 | Failsafe Micro Zykluszeit fehlerhaft |
| 0x607A | Failsafe Micro Motor Spannungsversorgung links fehlerhaft |
| 0x607B | Failsafe Micro Motor Spannungsversorgung rechts fehlerhaft |
| 0x607D | RAM Test im Failsafe Micro fehlerhaft |
| 0x607E | ROM Test im Failsafe Micro fehlerhaft |
| 0x607F | Programmablauf im Main Mirco fehlerhaft |
| 0x6083 | State Machine Fehler |
| 0x6084 | Interruptfehler |
| 0x6085 | RAM / ROM Test im Main Micro fehlerhaft |
| 0x6086 | Kommunikation mit ZENON ASIC fehlerhaft |
| 0x6087 | Programmablauf im Failsafe Micro fehlerhaft |
| 0x6089 | EEPROM schreiben fehlerhaft (ein Block) |
| 0x608A | EEPROM schreiben fehlerhaft (alle Blöcke) |
| 0x608B | EEPROM löschen fehlerhaft |
| 0x608C | EEPROM lesen fehlerhaft (ein Block) |
| 0x608D | EEPROM lesen fehlerhaft (alle Blöcke) |
| 0x608E | EEPROM Verarbeitungsfehler |
| 0x608F | EEPROM Config ID ungültig |
| 0x6090 | Fehler beim Codiervorgang |
| 0x6091 | Signaturprüfung der Codierung fehlerhaft |
| 0x6092 | Falsches Fahrzeug codiert |
| 0x6093 | Codierdaten ungültig |
| 0x6094 | Stack Check Fehler |
| 0x6095 | Interner Datenfehler im RAM |
| 0x6096 | TRW Dummy DTC 6 |
| 0x6097 | TRW Dummy DTC 7 |
| 0x6098 | TRW Dummy DTC 8 |
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

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | UW1_Tabelle | UW2_Tabelle | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 8 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Relativzeit | S | high | unsigned int | - | 1 | 1 | 0 |
| 0x02 | Geschwindigkeit | km/h | high | unsigned int | - | 1 | 100 | 0 |
| 0x03 | Spannung KL15 | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x04 | Spannung KL30 | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x05 | Systemzustand | Hex | - | unsigned char | - | - | - | - |
| 0x06 | Bremsenzustand hinten links | Hex | - | unsigned char | - | - | - | - |
| 0x07 | Bremsenzustand hinten rechts | Hex | - | unsigned char | - | - | - | - |
| 0x08 | Interner Fehlercode | Hex | - | unsigned char | - | - | - | - |

<a id="table-iarttyp"></a>
### IARTTYP

Dimensions: 1 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |

<a id="table-iarttexteindividuell"></a>
### IARTTEXTEINDIVIDUELL

Dimensions: 6 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb der Schwelle |
| 0x0002 | Signal oder Wert unterhalb der Schwelle |
| 0x0004 | kein Signal oder Wert |
| 0x0008 | unplausibles Signal oder Wert |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-betriebsmodus-byte1"></a>
### BETRIEBSMODUS_BYTE1

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Limphome State |
| 0x02 | Dynamic State |
| 0x04 | Release inhibit |
| 0x08 | Schalter Bremse öffnen Anforderung |
| 0x10 | Schalter Bremse schliessen Anforderung |
| 0x20 | Dynamische Abbremsung |
| 0x40 | Montagemodus |
| 0x80 | HU Mode |
| 0xFF | ungültig |

<a id="table-betriebsmodus-byte2"></a>
### BETRIEBSMODUS_BYTE2

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Bremse hl geöffnet |
| 0x02 | Bremse hl wird geöffnet |
| 0x04 | Bremse hl fehlerhaft |
| 0x08 | Bremse hl wird geschlossen |
| 0x10 | Bremse hl geschlossen |
| 0x20 | Bremse hl Unterspannung |
| 0x40 | Bremse hl geschlossen mit Einbremskraft |
| 0x80 | Bremse hl notentriegelt |
| 0xFF | ungültig |

<a id="table-betriebsmodus-byte3"></a>
### BETRIEBSMODUS_BYTE3

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Bremse hr geöffnet |
| 0x02 | Bremse hr wird geöffnet |
| 0x04 | Bremse hr fehlerhaft |
| 0x08 | Bremse hr wird geschlossen |
| 0x10 | Bremse hr geschlossen |
| 0x20 | Bremse hr Unterspannung |
| 0x40 | Bremse hr geschlossen mit Einbremskraft |
| 0x80 | Bremse hr notentriegelt |
| 0xFF | ungültig |

<a id="table-uw1-tabelle"></a>
### UW1_TABELLE

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x02 | 0x03 | 0x04 |

<a id="table-uw2-tabelle"></a>
### UW2_TABELLE

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x05 | 0x06 | 0x07 | 0x08 |

<a id="table-developmessages"></a>
### DEVELOPMESSAGES

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | deaktiviert |
| 0x01 | aktiviert |

<a id="table-bremsenstatus"></a>
### BREMSENSTATUS

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Bremse geöffnet |
| 0x01 | Bremse angelegt |
| 0x02 | Bremse wird geöffnet |
| 0x04 | Bremse fehlerhaft |
| 0x08 | Bremse wird geschlossen |
| 0x10 | Bremse geschlossen |
| 0x20 | Bremse Unterspannung |
| 0x40 | Bremse geschlossen mit Einbremskraft |
| 0x80 | Bremse notentriegelt |

<a id="table-modecontrollerstatus"></a>
### MODECONTROLLERSTATUS

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Release Inhibit |
| 0x01 | Statisch |
| 0x02 | Dynamisch |
| 0x04 | Limphome |
| 0x08 | Schalter Bremse öffnen |
| 0x10 | Schalter Bremse schliessen |
| 0x20 | Dynamische Abremsung |
| 0x40 | Montagemodus |
| 0x80 | HU Modus |

<a id="table-epbstillegungsstatus"></a>
### EPBSTILLEGUNGSSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Normalfunktion |
| 0x01 | Eingeschränkter hydraulischer Modus |
| 0x02 | Elektromechanischer Modus |
| 0x04 | Gesamtstilllegung |

<a id="table-cannetworkstatus"></a>
### CANNETWORKSTATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NM Reset |
| 0x01 | Normal |
| 0x02 | Sleep Indication |
| 0x04 | Wait for sleep |
| 0x08 | Bus sleep |

<a id="table-internernetworkstatus"></a>
### INTERNERNETWORKSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Sleep |
| 0x01 | Goto sleep |
| 0x02 | Active |

<a id="table-ccmeldungen"></a>
### CCMELDUNGEN

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | keine Anzeige |
| 0x0001 | Gesamtstillegung |
| 0x0002 | Elektromechanischer Modus |
| 0x0004 | Eingeschränkter hydraulischer Modus |
| 0x0008 | Festgestellt |
| 0x0010 | Montagemodus |
| 0x0020 | Tasterfehler |
| 0x0040 | Bremse treten zum Lösen |
| 0x0080 | Redundanter Tasterfehler |
| 0x0100 | Bremse lösen zum Anfahren |
| 0x0200 | Zusätzlich Getriebe P einlegen |
| 0x0400 | Fußbremse oder Kupplung treten |

<a id="table-statusemfschalter"></a>
### STATUSEMFSCHALTER

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht betätigt |
| 0x01 | nicht betätigt |
| 0x02 | Taster gezogen |
| 0x03 | Taster gezogen |
| 0x04 | Taster gedrückt |
| 0x05 | Taster gedrückt |
| 0x06 | Signal ungültig |
| 0x07 | Signal ungültig |
| 0x08 | Signal ungültig |

<a id="table-statusemfschalterfehler"></a>
### STATUSEMFSCHALTERFEHLER

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Redundanter Tasterfehler |
| 0x02 | Fehler in Richtung Ziehen |
| 0x03 | Fehler in Richtung Drücken |
| 0x04 | Komplett defekt |
| 0x05 | Signal ungültig |

<a id="table-blsstatus"></a>
### BLSSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Bremslichtschalter offen |
| 0x01 | Bremslichtschalter geschlossen |
| 0x02 | Bremslichtschalter Zustand nicht bekannt |
| 0x03 | Bremslichtschalter Fehler |

<a id="table-sollwertanforderungstatus"></a>
### SOLLWERTANFORDERUNGSTATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Initialisierung |
| 0x02 | Sollwert umsetzen |
| 0x04 | Sollwert nicht umsetzen (Standby) |
| 0x08 | Sollwert nicht umsetzen (Fehler) |
| 0xFF | Signal ungültig |

<a id="table-kl15status"></a>
### KL15STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Klemme 15 AUS |
| 0x01 | Klemme 15 EIN |
| 0x02 | unbekannt |
| 0x03 | Signal ungültig |

<a id="table-kl50status"></a>
### KL50STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Klemme 50 AUS |
| 0x01 | Klemme 50 EIN |
| 0x02 | Anlasserstart-Wunsch |
| 0x03 | Signal ungültig |

<a id="table-klrstatus"></a>
### KLRSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Klemme R AUS |
| 0x01 | Klemme R EIN |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig |

<a id="table-zasstatus"></a>
### ZASSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Schlüssel im ZAS |
| 0x01 | Schlüssel steckt im ZAS |
| 0x02 | Signal unplausibel |
| 0x03 | Signal ungültig |

<a id="table-gangstatus"></a>
### GANGSTATUS

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | N Kein Kraftschluß |
| 0x01 | R Rückwärtsgang |
| 0x02 | P Kein Kraftschluß |
| 0x03 | D Drive |
| 0x04 | Reserviert |
| 0x05 | Reserviert |
| 0x06 | Reserviert |
| 0x07 | Reserviert |
| 0x08 | Reserviert |
| 0x09 | Reserviert |
| 0x0A | Reserviert |
| 0x0B | Reserviert |
| 0x0C | Reserviert |
| 0x0D | Reserviert |
| 0x0E | Reserviert |
| 0x0F | Signal ungültig / Automatikgetriebe nicht vorhanden |

<a id="table-kupplungstatus"></a>
### KUPPLUNGSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kupplung nicht betätigt |
| 0x01 | Kupplung betätigt |
| 0x02 | Reserviert |
| 0x03 | Signal ungültig / Kupplung nicht vorhanden |

<a id="table-getriebeart"></a>
### GETRIEBEART

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Automatik |
| 0x01 | Manuell |

<a id="table-fehlerstatus"></a>
### FEHLERSTATUS

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler vorhanden |
| 0x01 | mindestens ein Fehler vorhanden |

<a id="table-assemblycheck"></a>
### ASSEMBLYCHECK

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NOT DONE |
| 0x01 | DONE |

<a id="table-aktiv"></a>
### AKTIV

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Inaktiv |
| 0x01 | Aktiv |

<a id="table-eolreset"></a>
### EOLRESET

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | EOL rücksetzen erfolgreich |
| 0xFF | EOL rücksetzen nicht erfolgreich |

<a id="table-servicestatus"></a>
### SERVICESTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | erfolgreich beendet |
| 0x02 | fehlerhaft beendet |
| 0x03 | Initialisierung (wurde noch nicht gestartet) |

<a id="table-service"></a>
### SERVICE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x28 | Montagemodus anfahren |
| 0x2A | Anlegemodus Check |

<a id="table-dfa-emf"></a>
### DFA_EMF

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 500 Hz |
| 0x01 | 250 Hz |
| 0x02 | 125 Hz |
| 0x03 | 62,5 Hz |
| 0x04 | 31,25 Hz |
| 0x05 | 15,625 Hz |
| 0x06 | ungültiger Frequenzbereich |
