# him_72.prg

- Jobs: [72](#jobs)
- Tables: [27](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | HIM |
| ORIGIN | BMW EI-642 Bernhard Gasser |
| REVISION | 3.001 |
| AUTHOR | LEAR DCS Ahrens |
| COMMENT | N/A |
| PACKAGE | 1.45 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
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
- [_BRIF_FILE_HIM_LEAR](#job-brif-file-him-lear) - Writting the BRIF in EEPROM All the arguments should be supplied KWP2000: $2E WriteDataByCommonIdentifier $300x BRIF Modus  : Default
- [_READ_LINK_DATE_TIME_LEAR](#job-read-link-date-time-lear) - Auslesen der Linkdate und -time KWP2000: $21 ReadDataByLocalIdentifier $01 Linkdate und -time
- [_READ_ENERGY_SAVING_MODE_LEAR](#job-read-energy-saving-mode-lear) - Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode
- [READ_MAPPING_TABLE_INFO](#job-read-mapping-table-info) - Auslesen der Mappingtable Infos KWP2000: $21 ReadDataByLocalIdentifier $03 Mappingtable Infos
- [STATUS_ANALOG_INPUTS](#job-status-analog-inputs) - Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $01 Analoge Inputs
- [STATUS_DIGITAL_INPUTS](#job-status-digital-inputs) - Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 Digitale Inputs
- [STATUS_VENT_SPERRVENTIL_CHILLER](#job-status-vent-sperrventil-chiller) - Status der Ansteuerung des Kaeltemittelabsperrventils der Hochvolt-Speicherkuehlung abfragen (S_MV+, Pin 25) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge
- [STATUS_VENT_VERDAMPFER](#job-status-vent-verdampfer) - Status der Ansteuerung des Kaeltemittelabsperrventils der Klimaanlage abfragen (S_MVV+, Pin 26) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge
- [STATUS_VENT_BYPASS_WT](#job-status-vent-bypass-wt) - Status der Ansteuerung des Bypassventils Waermetauscher (warm) abfragen (S_BPV1+, Pin 24) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge
- [STATUS_VENT_BYPASS_CHILLER](#job-status-vent-bypass-chiller) - Status der Ansteuerung des Bypassventils Chiller (kalt) abfragen (S_BPV2+, Pin 23) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge
- [STATUS_H_ACCY_WUP](#job-status-h-accy-wup) - Status der Weckleitung H_ACCY_WUP abfragen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge
- [STATUS_HS_COM](#job-status-hs-com) - Status der Weckleitung HS_COM abfragen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge
- [STATUS_APM](#job-status-apm) - Status der Weckleitung APM Wakeup abfragen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge
- [STATUS_VENT_BYPASS_CHILLER_REGLER](#job-status-vent-bypass-chiller-regler) - Aktueller Reglerwert des Bypassventils Chiller (kalt) abfragen (S_BPV2+, Pin 23) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $04 PWM Outputs
- [STATUS_VENT_BYPASS_WT_REGLER](#job-status-vent-bypass-wt-regler) - Aktueller Reglerwert des Bypassventils Waermetauscher (warm) abfragen (S_BPV1+, Pin 24) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $04 PWM Outputs
- [STATUS_TEMPERATURSENSOR](#job-status-temperatursensor) - Auslesen des Status vom TEMPERATURSENSOR der Kühlmitteltemperatur PEB KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $05 TEMPERATURSENSOR
- [_STATUS_LEITERPLATTENTEMPERATUR](#job-status-leiterplattentemperatur) - Auslesen des Status vom LEITERPLATTENTEMPERATUR KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $05 LEITERPLATTENTEMPERATUR
- [STATUS_SCHALTPADDLE](#job-status-schaltpaddle) - Auslesen des Status der SCHALTPADDLE KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $06 SCHALTPADDLE
- [STATUS_TRENNRELAIS](#job-status-trennrelais) - Auslesen des Status der Trennrelais/Batterie KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $07 Trennrelais/Batterie
- [STEUERN_AUSGANG_DIGITAL](#job-steuern-ausgang-digital) - KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern
- [STEUERN_VENT_SPERRVENTIL_CHILLER](#job-steuern-vent-sperrventil-chiller) - Ansteuerung des Kaeltemittelabsperrventils HV-Chiller (S_MV+, Pin 25) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern
- [STEUERN_VENT_VERDAMPFER](#job-steuern-vent-verdampfer) - Ansteuerung des Kaeltemittelabsperrventils Klimaanlage (Verdampfer) (S_MVV+, Pin 26) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern
- [STEUERN_VENT_BYPASS_WT](#job-steuern-vent-bypass-wt) - Ansteuerung des Bypassventils Waermetauscher (warm) (S_BPV1+, Pin 24) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern
- [STEUERN_VENT_BYPASS_CHILLER](#job-steuern-vent-bypass-chiller) - Ansteuerung des Bypassventils Chiller (kalt) (S_BPV2+, Pin 23) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern
- [STEUERN_VENT_BYPASS_WT_REGLER](#job-steuern-vent-bypass-wt-regler) - Ansteuerung des Bypassventils Waermetauscher (warm) mit der Oeffnungszeit des Ventils in 0 bis 3600ms (S_BPV1+, Pin 24) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern
- [STEUERN_VENT_BYPASS_CHILLER_REGLER](#job-steuern-vent-bypass-chiller-regler) - Ansteuerung des Bypassventils Chiller (kalt) mit der Oeffnungszeit des Ventils in 0 bis 3600ms (S_BPV2+, Pin 23) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern
- [STEUERN_TRENNRELAIS_SCHLIESSEN](#job-steuern-trennrelais-schliessen) - Schliessen des Trennrelais KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $07 Trennrelais schliessen
- [_SET_LOGGER_LEVEL](#job-set-logger-level) - Logger Level setzen KWP2000: $3B WriteDataByLocalIdentifier $01 Set Logger Level Modus  : Default
- [_WRITE_DEFAULT_CODING_BYTE](#job-write-default-coding-byte) - Logger Level setzen KWP2000: $3B WriteDataByLocalIdentifier $02 WRITE_DEFAULT_CODING_BYTE Modus  : Default
- [_CODIERDATEN_BLOCK_LESEN_LEAR](#job-codierdaten-block-lesen-lear) - KWP2000: $22 ReadDataByCommonIdentifier $xxxx Codierdaten je nach Block Modus  : Default
- [STATUS_HISTORIENSPEICHER](#job-status-historienspeicher) - Auslesen des Historienspeicher KWP2000: $22 ReadDataByCommonIdentifier $F000 Historienspeicher lesen
- [HISTORIENSPEICHER_LOESCHEN](#job-historienspeicher-loeschen) - Loeschen des Historienspeicher KWP2000: $2E WriteDataByCommonIdentifier $F000 Historienspeicher loeschen

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

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

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

<a id="job-brif-file-him-lear"></a>
### _BRIF_FILE_HIM_LEAR

Writting the BRIF in EEPROM All the arguments should be supplied KWP2000: $2E WriteDataByCommonIdentifier $300x BRIF Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PASSWORT | string | Passwort zum Ausfuehren des jobs |
| FILE_TEXT | string | Format: [Drive]:[Path]\[File].[Ext] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| HWREF | string | Written Value |
| PECUHN | string | Written Value |
| DOECUM | string | Written Value |
| SSI | string | Written Value |
| SSECUSN | string | Written Value |
| ERT | string | Written Value |
| SIGT | string | Written Value |
| RST | string | Written Value |
| MXBL | string | Written Value |
| VMECUHVN | string | Written Value |
| SNOET | string | Written Value |
| UIF_ZB_NR | string | Written Value |
| JOB_STATUS | string | From JobResult Table |

<a id="job-read-link-date-time-lear"></a>
### _READ_LINK_DATE_TIME_LEAR

Auslesen der Linkdate und -time KWP2000: $21 ReadDataByLocalIdentifier $01 Linkdate und -time

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_LINK_DATE_APP | string | Linkdatum fuer Applikation |
| SW_LINK_DATE_BOOT | string | Linkdatum fuer Bootloader |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-energy-saving-mode-lear"></a>
### _READ_ENERGY_SAVING_MODE_LEAR

Energy-Saving-Mode auslesen KWP 2000: $22 ReadDataByCommonIdentifier KWP 2000: $100A EnergySavingMode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ENERGY_SAVING_MODE | string | Ausgabe des Engery-Saving-Modes table EnergySaving NAME TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-mapping-table-info"></a>
### READ_MAPPING_TABLE_INFO

Auslesen der Mappingtable Infos KWP2000: $21 ReadDataByLocalIdentifier $03 Mappingtable Infos

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| MAPPINGTABLE_VERSION | string | MAPPINGTABLE_VERSION |
| MAPPINGTABLE_NAME | string | MAPPINGTABLE_NAME |
| MAPPINGTABLE_DATE | string | MAPPINGTABLE_DATE |
| MAPPINGTABLE_OPERATOR | string | MAPPINGTABLE_OPERATOR |
| MAPPINGTABLE_GENERATOR_TOOL | string | MAPPINGTABLE_GENERATOR_TOOL |
| MAPPINGTABLE_GENERATOR_TOOL_VERSION | string | MAPPINGTABLE_GENERATOR_TOOL_VERSION |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-inputs"></a>
### STATUS_ANALOG_INPUTS

Auslesen der Stati von den analogen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $01 Analoge Inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_IN_AN_H_ACCY_WUP_WERT | real | Spannung AN_H_ACCY_WUP Bereich: 0 V bis 5 V |
| STAT_IN_AN_APM_WUP_WERT | real | Spannung AN_APM_WUP Bereich: 0 V bis 5 V |
| STAT_IN_AN_HS_COM_WERT | real | Spannung AN_HS_COM Bereich: 0 V bis 5 V |
| STAT_IN_AN_HV_WARM_WERT | real | Spannung AN_HV_WARM Bereich: 0 V bis 5 V |
| STAT_IN_AN_HV_KALT_WERT | real | Spannung AN_HV_KALT Bereich: 0 V bis 5 V |
| STAT_IN_AN_S_ML_WERT | real | Spannung AN_S_ML Bereich: 0 V bis 5 V |
| STAT_IN_AN_OPT_WERT | real | Spannung AN_OPT Bereich: 0 V bis 5 V |
| STAT_IN_AN_HV_KLIMA_WERT | real | Spannung AN_HV_KLIMA Bereich: 0 V bis 5 V |
| STAT_IN_AN_HV_KUEHL_WERT | real | Spannung AN_HV_KUEHL Bereich: 0 V bis 5 V |
| STAT_IN_AN_TEMP_MESS_WERT | real | Temperatur AN_TEMP_MESS Bereich: -40°C bis 125°C |
| STAT_IN_AN_PADDLE_WERT | real | Spannung PADDLE Bereich: 0 V bis 5 V |
| STAT_IN_AN_KL30_WERT | real | Spannung AN_KL30 Bereich: 0 V bis 18 V |
| STAT_IN_AN_TEMP_MESS_E_WERT | real | Temperatur AN_TEMP_MESS_E Bereich: -40°C bis 125°C |
| STAT_IN_AN_U3V3_SW_ETH_WERT | real | Spannung AN_U3V3_SW_ETH Bereich: 0 V bis 5 V |
| STAT_IN_AN_HS_H_ACCY_WUP_WERT | real | Spannung AN_HS_H_ACCY_WUP Bereich: 0 V bis 5 V |
| STAT_IN_AN_HS_HS_COM_EN_WERT | real | Spannung AN_HS_HS_COM_EN Bereich: 0 V bis 5 V |
| STAT_IN_AN_HS_S_MVV_PLUS_WERT | real | Spannung AN_HS_S_MVV_PLUS Bereich: 0 V bis 5 V |
| STAT_IN_AN_HS_S_MV_PLUS_WERT | real | Spannung AN_HS_S_MV_PLUS Bereich: 0 V bis 5 V |
| STAT_IN_AN_HS_APM_WUP_WERT | real | Spannung AN_HS_APM_WUP Bereich: 0 V bis 5 V |
| STAT_IN_AN_HS_S_BPV1_PLUS_WERT | real | Spannung AN_HS_S_BPV1_PLUS Bereich: 0 V bis 5 V |
| STAT_IN_AN_HS_S_BPV2_PLUS_WERT | real | Spannung AN_HS_S_BPV2_PLUS Bereich: 0 V bis 5 V |
| STAT_IN_AN_HS_OPT1_WERT | real | Spannung AN_HS_OPT1 Bereich: 0 V bis 5 V |
| STAT_IN_AN_HS_OPT2_WERT | real | Spannung AN_HS_OPT2 Bereich: 0 V bis 5 V |
| STAT_IN_AN_HS_ML_PLUS_WERT | real | Spannung AN_HS_ML_PLUS Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Spannungen: Volt |
| STAT_TEMPERATUR_EINH | string | Einheit fuer alle Temperaturen: °C |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-inputs"></a>
### STATUS_DIGITAL_INPUTS

Auslesen der Stati von den digitalen Eingaengen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $02 Digitale Inputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_IN_PT_CAN_ERR_EIN | int | CAN-Transceiver PT_CAN Fehler |
| STAT_IN_HL_CAN_ERR_EIN | int | CAN-Transceiver HL_CAN Fehler |
| STAT_IN_HS_CAN_ERR_EIN | int | CAN-Transceiver HS_CAN Fehler |
| STAT_IN_D_CAN_ERR_EIN | int | CAN-Transceiver D_CAN Fehler |
| STAT_IN_INT_MPC_EIN | int | IN_INT_MPC ein |
| STAT_IN_CAN_WAKE_EIN | int | IN_CAN_WAKE ein |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vent-sperrventil-chiller"></a>
### STATUS_VENT_SPERRVENTIL_CHILLER

Status der Ansteuerung des Kaeltemittelabsperrventils der Hochvolt-Speicherkuehlung abfragen (S_MV+, Pin 25) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VENT_SPERRVENTIL_CHILLER_WERT | int | SPERRVENTIL_CHILLER geschlossen/offen |
| STAT_VENT_SPERRVENTIL_CHILLER_TEXT | string | SPERRVENTIL_CHILLER geschlossen/offen |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vent-verdampfer"></a>
### STATUS_VENT_VERDAMPFER

Status der Ansteuerung des Kaeltemittelabsperrventils der Klimaanlage abfragen (S_MVV+, Pin 26) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VENT_VERDAMPFER_WERT | int | VERDAMPFER geschlossen/offen |
| STAT_VENT_VERDAMPFER_TEXT | string | VERDAMPFER geschlossen/offen |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vent-bypass-wt"></a>
### STATUS_VENT_BYPASS_WT

Status der Ansteuerung des Bypassventils Waermetauscher (warm) abfragen (S_BPV1+, Pin 24) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VENT_BYPASS_WT_WERT | int | BYPASS_WT geschlossen/offen |
| STAT_VENT_BYPASS_WT_TEXT | string | BYPASS_WT geschlossen/offen |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vent-bypass-chiller"></a>
### STATUS_VENT_BYPASS_CHILLER

Status der Ansteuerung des Bypassventils Chiller (kalt) abfragen (S_BPV2+, Pin 23) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VENT_BYPASS_CHILLER_WERT | int | BYPASS_CHILLER geschlossen/offen |
| STAT_VENT_BYPASS_CHILLER_TEXT | string | BYPASS_CHILLER geschlossen/offen |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-h-accy-wup"></a>
### STATUS_H_ACCY_WUP

Status der Weckleitung H_ACCY_WUP abfragen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_H_ACCY_WUP_EIN | int | H_ACCY_WUP an/aus |
| STAT_H_ACCY_WUP_FEHLER_TEXT | string | Fehler H_ACCY_WUP |
| STAT_H_ACCY_WUP_FEHLER_WERT | int | Fehlerwert H_ACCY_WUP |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-com"></a>
### STATUS_HS_COM

Status der Weckleitung HS_COM abfragen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HS_COM_EIN | int | HS_COM an/aus |
| STAT_HS_COM_FEHLER_TEXT | string | Fehler HS_COM |
| STAT_HS_COM_FEHLER_WERT | int | Fehlerwert HS_COM |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-apm"></a>
### STATUS_APM

Status der Weckleitung APM Wakeup abfragen KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $03 Ausgaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_APM_EIN | int | H_ACCY_WUP an/aus |
| STAT_APM_FEHLER_TEXT | string | Fehler APM |
| STAT_APM_FEHLER_WERT | int | Fehlerwert APM |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vent-bypass-chiller-regler"></a>
### STATUS_VENT_BYPASS_CHILLER_REGLER

Aktueller Reglerwert des Bypassventils Chiller (kalt) abfragen (S_BPV2+, Pin 23) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $04 PWM Outputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VENT_BYPASS_CHILLER_REGLER_WERT | real | Reglerwert des Bypassventils Chiller (kalt) Bereich: 0 bis 3600 |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vent-bypass-wt-regler"></a>
### STATUS_VENT_BYPASS_WT_REGLER

Aktueller Reglerwert des Bypassventils Waermetauscher (warm) abfragen (S_BPV1+, Pin 24) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $04 PWM Outputs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VENT_BYPASS_WT_REGLER_WERT | real | Reglerwert des Bypassventils Waermetauscher (warm) Bereich: 0 bis 3600 |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temperatursensor"></a>
### STATUS_TEMPERATURSENSOR

Auslesen des Status vom TEMPERATURSENSOR der Kühlmitteltemperatur PEB KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $05 TEMPERATURSENSOR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TEMP_MESS_E_WERT | real | Bereich: -40°C bis 150 °C Wert fuer Temperatursensor |
| STAT_TEMP_MESS_E_EINH | string | Einheit: °C |
| STAT_AD_TEMP_MESS_E_WERT | int | Bereich: 0 bis 255 AD-Wert Temperatursensor |
| STAT_TEMP_MESS_E_FEHLER_TEXT | string | Fehler TEMPERATURSENSOR |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-leiterplattentemperatur"></a>
### _STATUS_LEITERPLATTENTEMPERATUR

Auslesen des Status vom LEITERPLATTENTEMPERATUR KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $05 LEITERPLATTENTEMPERATUR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LEITERPLATTENTEMPERATUR_WERT | real | Bereich: -40°C bis 150 °C Wert fuer Temperatursensor |
| STAT_LEITERPLATTENTEMPERATUR_EINH | string | Einheit: °C |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schaltpaddle"></a>
### STATUS_SCHALTPADDLE

Auslesen des Status der SCHALTPADDLE KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $06 SCHALTPADDLE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHALTPADDLE_WERT | int | Wert Schaltpaddle |
| STAT_SCHALTPADDLE_TEXT | string | table Schaltpaddle |
| STAT_AD_SCHALTPADDLE_WERT | int | Bereich: 0 bis 255 AD-Wert Schaltpaddle |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-trennrelais"></a>
### STATUS_TRENNRELAIS

Auslesen des Status der Trennrelais/Batterie KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState $07 Trennrelais/Batterie

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_U_BATT_1_WERT | real | Wert Batterie 1 |
| STAT_U_BATT_2_WERT | real | Wert Batterie 2 |
| STAT_U_BATT_DIFF_WERT | real | Wert Batterie Diff |
| STAT_TRENNRELAIS_EIN | int | Status Trennrelais |
| STAT_AFTER_CLOSE_TRENNRELAIS_WERT | int | Status nach Trennrelais schliessen |
| STAT_AFTER_CLOSE_TRENNRELAIS_TEXT | string | Status nach Trennrelais schliessen |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Spannungen: Volt |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ausgang-digital"></a>
### STEUERN_AUSGANG_DIGITAL

KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG | string | table Ausgaenge NAME TEXT Ausgang aus Tabelle auswaehlen |
| AUSGANG_EIN | string | Werte: ein, aus table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vent-sperrventil-chiller"></a>
### STEUERN_VENT_SPERRVENTIL_CHILLER

Ansteuerung des Kaeltemittelabsperrventils HV-Chiller (S_MV+, Pin 25) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG_EIN | string | Werte: open, close, control table VentilStatus NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vent-verdampfer"></a>
### STEUERN_VENT_VERDAMPFER

Ansteuerung des Kaeltemittelabsperrventils Klimaanlage (Verdampfer) (S_MVV+, Pin 26) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG_EIN | string | Werte: open, close, control table VentilStatus NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vent-bypass-wt"></a>
### STEUERN_VENT_BYPASS_WT

Ansteuerung des Bypassventils Waermetauscher (warm) (S_BPV1+, Pin 24) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG_EIN | string | Werte: open, close, control table VentilStatus NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vent-bypass-chiller"></a>
### STEUERN_VENT_BYPASS_CHILLER

Ansteuerung des Bypassventils Chiller (kalt) (S_BPV2+, Pin 23) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG_EIN | string | Werte: open, close, control table VentilStatus NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vent-bypass-wt-regler"></a>
### STEUERN_VENT_BYPASS_WT_REGLER

Ansteuerung des Bypassventils Waermetauscher (warm) mit der Oeffnungszeit des Ventils in 0 bis 3600ms (S_BPV1+, Pin 24) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG_EIN | string | Werte: ein, aus table DigitalArgument TEXT |
| REGLER_WERT | int | Werte: 0 ... 3600 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vent-bypass-chiller-regler"></a>
### STEUERN_VENT_BYPASS_CHILLER_REGLER

Ansteuerung des Bypassventils Chiller (kalt) mit der Oeffnungszeit des Ventils in 0 bis 3600ms (S_BPV2+, Pin 23) KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $03 Ausgaenge ansteuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG_EIN | string | Werte: ein, aus table DigitalArgument TEXT |
| REGLER_WERT | int | Werte: 0 ... 3600 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-trennrelais-schliessen"></a>
### STEUERN_TRENNRELAIS_SCHLIESSEN

Schliessen des Trennrelais KWP2000: $30 InputOutputControlByLocalIdentifier $07 ShortTermAdjustment $07 Trennrelais schliessen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-logger-level"></a>
### _SET_LOGGER_LEVEL

Logger Level setzen KWP2000: $3B WriteDataByLocalIdentifier $01 Set Logger Level Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KOMPONENT | int | Auswahl der Loggerkomponente, bei 0xff werden alle geaendert |
| LOGGER_LEVEL | int | Auswahl Loggerlevel, bei 0 wird der Logger ausgeschaltet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-default-coding-byte"></a>
### _WRITE_DEFAULT_CODING_BYTE

Logger Level setzen KWP2000: $3B WriteDataByLocalIdentifier $02 WRITE_DEFAULT_CODING_BYTE Modus  : Default

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
| BLOCK | string | Bereich: 0x31xx |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN | binary | Codierdaten fuer angegebenen Block |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-historienspeicher"></a>
### STATUS_HISTORIENSPEICHER

Auslesen des Historienspeicher KWP2000: $22 ReadDataByCommonIdentifier $F000 Historienspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HISTORY_RESET_COUNT_WERT | int | Anzahl von Watchdog-Resets |
| STAT_HISTORY_ANZ_HYB_CAN_MSG_IN_SLEEP_WERT | int | Anzahl empfangener CAN-Frames bei sleep acknowledge |
| STAT_HISTORY_HYB_CAN_MSG_IN_SLEEP_WERT_1 | binary | Empfangene CAN-Frame bei sleep acknowledge Aufbau: CanId: 2Byte, CanPayload: 8Byte, BusIndex: 1Byte, UBatt: 1Byte, kmStand: 2Byte |
| STAT_HISTORY_HYB_CAN_MSG_IN_SLEEP_WERT_2 | binary | Empfangene CAN-Frame bei sleep acknowledge Aufbau: CanId: 2Byte, CanPayload: 8Byte, BusIndex: 1Byte, UBatt: 1Byte, kmStand: 2Byte |
| STAT_HISTORY_HYB_CAN_MSG_IN_SLEEP_WERT_3 | binary | Empfangene CAN-Frame bei sleep acknowledge Aufbau: CanId: 2Byte, CanPayload: 8Byte, BusIndex: 1Byte, UBatt: 1Byte, kmStand: 2Byte |
| STAT_HISTORY_HYB_CAN_MSG_IN_SLEEP_WERT_4 | binary | Empfangene CAN-Frame bei sleep acknowledge Aufbau: CanId: 2Byte, CanPayload: 8Byte, BusIndex: 1Byte, UBatt: 1Byte, kmStand: 2Byte |
| STAT_HISTORY_HYB_CAN_MSG_IN_SLEEP_WERT_5 | binary | Empfangene CAN-Frame bei sleep acknowledge Aufbau: CanId: 2Byte, CanPayload: 8Byte, BusIndex: 1Byte, UBatt: 1Byte, kmStand: 2Byte |
| STAT_HISTORY_HYB_CAN_MSG_IN_SLEEP_WERT_6 | binary | Empfangene CAN-Frame bei sleep acknowledge Aufbau: CanId: 2Byte, CanPayload: 8Byte, BusIndex: 1Byte, UBatt: 1Byte, kmStand: 2Byte |
| STAT_HISTORY_HYB_CAN_MSG_IN_SLEEP_WERT_7 | binary | Empfangene CAN-Frame bei sleep acknowledge Aufbau: CanId: 2Byte, CanPayload: 8Byte, BusIndex: 1Byte, UBatt: 1Byte, kmStand: 2Byte |
| STAT_HISTORY_HYB_CAN_MSG_IN_SLEEP_WERT_8 | binary | Empfangene CAN-Frame bei sleep acknowledge Aufbau: CanId: 2Byte, CanPayload: 8Byte, BusIndex: 1Byte, UBatt: 1Byte, kmStand: 2Byte |
| STAT_HISTORY_HYB_CAN_MSG_IN_SLEEP_WERT_9 | binary | Empfangene CAN-Frame bei sleep acknowledge Aufbau: CanId: 2Byte, CanPayload: 8Byte, BusIndex: 1Byte, UBatt: 1Byte, kmStand: 2Byte |
| STAT_HISTORY_HYB_CAN_MSG_IN_SLEEP_WERT_10 | binary | Empfangene CAN-Frame bei sleep acknowledge Aufbau: CanId: 2Byte, CanPayload: 8Byte, BusIndex: 1Byte, UBatt: 1Byte, kmStand: 2Byte |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-historienspeicher-loeschen"></a>
### HISTORIENSPEICHER_LOESCHEN

Loeschen des Historienspeicher KWP2000: $2E WriteDataByCommonIdentifier $F000 Historienspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
- [FORTTEXTE](#table-forttexte) (29 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (27 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (2 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (2 × 9)
- [ENERGYSAVING](#table-energysaving) (5 × 3)
- [VENTILSTATUS](#table-ventilstatus) (7 × 3)
- [AUSGANGTEXTE](#table-ausgangtexte) (10 × 3)
- [PADDLESTATUS](#table-paddlestatus) (6 × 2)
- [FEHLERSTATUS](#table-fehlerstatus) (4 × 2)
- [TRENNRELAISFEHLERSTATUS](#table-trennrelaisfehlerstatus) (5 × 2)

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

Dimensions: 29 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xAA28 | Energiesparmode aktiv |
| 0xAA29 | Wakeup Leitung: GM_Hybrid_Accessory_Wakeup defekt |
| 0xAA2A | Wakeup Leitung: GM_HighSpeed_Comm_Enable defekt |
| 0xAA2B | Wakeup Leitung: RUN / CRANK defekt |
| 0xAA2C | Wakeup Leitung: APM_Wakeup defekt |
| 0xAA2D | Schaltbares Motorlager defekt |
| 0xAA2E | HV-Speicherkühlung: Vent_Kältemittelventil (Sperrveentil Klimaanlage) defekt |
| 0xAA2F | HV-Speicherkühlung: Vent_HV-Kühlung (Sperrventil Chiller) defekt |
| 0xAA30 | HV-Speicherkühlung: Vent_Bypass warm (Wärmetauscher) defekt |
| 0xAA31 | HV-Speicherkühlung: Vent_Bypass kalt (Chiller) defekt |
| 0xAA32 | Interner Fehler Hardware  |
| 0xAA33 | externer Temperatursensor defekt |
| 0xAA34 | Paddles defekt |
| 0xAA35 | fehlerhafte Dauerbetaetigung |
| 0xAA36 | Fehler 2.Batterie |
| 0xAA37 | Fehler 2.Batterie: U[Batt2] &lt; U[Batt2-Diag] |
| 0xAA38 | Fehler 2.Batterie: Defekte Sicherung |
| 0xCB47 | Bus Kommunikationsfehler (PT-CAN) |
| 0xCB4B | Bus Kommunikationsfehler (HL-CAN) |
| 0xCB4F | Bus Kommunikationsfehler (HS-CAN) |
| 0xCB53 | Bus Kommunikationsfehler (D-CAN) |
| 0xCB54 | Botschaft (Anforderung Klima Hybrid, 299h) |
| 0xCB55 | CTR_CSOV_HVBTC Timeout (HV-Chiller) |
| 0xCB56 | CTR_CSOV_AIC (Klima) |
| 0xCB57 | CTR_VA_BYPA_WARM (Bypass warm) |
| 0xCB58 | CTR_VA_BYPA_COLD (Bypass kalt) |
| 0xCB59 | Botschaft HCP25 (2A5h) Timeout |
| 0xCB5A | Netzwerkaktivitaet bei ausgeschalteten Weckleitungen |
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

Dimensions: 27 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xAA28 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA29 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA2A | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA2B | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA2C | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA2D | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA2E | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA2F | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA30 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA31 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA32 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA33 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA34 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA35 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA36 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA37 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xAA38 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCB47 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCB4B | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCB4F | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCB53 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCB54 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCB55 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCB56 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCB57 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCB58 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0xCB5A | 0x01 | 0x02 | 0x03 | 0x04 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Bordnetzspannung | Volt | - | unsigned int | - | 18 | 255 | 0 |
| 0x02 | Umweltbedingung 2 | Grad | - | unsigned char | - | 1 | 1 | 0 |
| 0x03 | Umweltbedingung 3 | Geschwindigkeit | - | unsigned char | - | 1 | 1 | 0 |
| 0x04 | Umweltbedingung 4 | Ampere | - | signed int | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 2 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xAA61 | Temperatursensor Leiterplatte defekt |
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

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xAA61 | 0x01 | 0x02 | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 2 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Bordnetzspannung | Volt | - | unsigned int | - | 18 | 255 | 0 |
| 0x02 | Temperatur | Grad | - | signed long | - | 1 | 1 | 0 |

<a id="table-energysaving"></a>
### ENERGYSAVING

Dimensions: 5 rows × 3 columns

| E_MODE | NAME | TEXT |
| --- | --- | --- |
| 0x00 | ENERGY_MODE_AUS | Energiesparmode aus |
| 0x01 | ENERGY_MODE_PRODUCTION | Energiesparmode Fertigung |
| 0x02 | ENERGY_MODE_SHIPMENT | Energiesparmode Transport |
| 0x04 | ENERGY_MODE_REPAIR_SHOP | Energiesparmode Werkstatt |
| 0x08 | ERROR | falscher Eingabewert |

<a id="table-ventilstatus"></a>
### VENTILSTATUS

Dimensions: 7 rows × 3 columns

| STATUS | NAME | TEXT |
| --- | --- | --- |
| 0 | CLOSE | geschlossen |
| 1 | OPEN | offen |
| 2 | CONTROL | geregelt |
| 0 | 0 | geschlossen |
| 1 | 1 | offen |
| 2 | 2 | geregelt |
| 4 | ERROR | falscher Eingabewert |

<a id="table-ausgangtexte"></a>
### AUSGANGTEXTE

Dimensions: 10 rows × 3 columns

| OUTPUTNR | NAME | TEXT |
| --- | --- | --- |
| 0x01 | HV_KUEHL | Ventil Sperrventil Chiller |
| 0x02 | HV_KLIMA | Ventil Verdampfer |
| 0x03 | HV_WARM | Ventil Bypass WT |
| 0x04 | HV_KALT | Ventil Bypass Chiller |
| 0x05 | H_ACCY_WUP | Leitung H_ACCY_WUP |
| 0x06 | HS_COM_EN | Leitung HS_COM_EN |
| 0x07 | APM_WUP | Leitung APM_WUP |
| 0x08 | RUN_CRANK | Leitung RUN_CRANK |
| 0x0B | S_BAT2 | Schalter Batterie 2 |
| 0xFF | UNKNOWN | unbekannter Ausgang |

<a id="table-paddlestatus"></a>
### PADDLESTATUS

Dimensions: 6 rows × 2 columns

| STATUS | TEXT |
| --- | --- |
| 0 | Paddle nicht betaetigt, Initialisierung |
| 1 | Tip - betaetigt nicht entprellt |
| 2 | Tip + betaetigt nicht entprellt |
| 3 | Fehler Paddle |
| 5 | Tip - betaetigt und entprellt |
| 6 | Tip + betaetigt und entprellt |

<a id="table-fehlerstatus"></a>
### FEHLERSTATUS

Dimensions: 4 rows × 2 columns

| STATUS | TEXT |
| --- | --- |
| 0 | kein Fehler |
| 1 | Fehler: Kurzschluss UBAT |
| 2 | Fehler: Kurzschluss GND |
| 4 | Fehler: Open Load |

<a id="table-trennrelaisfehlerstatus"></a>
### TRENNRELAISFEHLERSTATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Trennrelais ist nicht angesteuert worden |
| 1 | Fahrbereitschaft ist ein |
| 2 | Ubatt1-IBS ist nicht groesser als Ubatt-DIAG |
| 3 | Udiff ist nicht kleiner gleich Udiff_Schwelle2 |
| 4 | Trennrelais wurde erfolgreich angesteuert |
