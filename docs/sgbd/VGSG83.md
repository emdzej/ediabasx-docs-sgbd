# VGSG83.prg

- Jobs: [77](#jobs)
- Tables: [41](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Verteilergetriebe Steuergerät ATC400/500 |
| ORIGIN | BMW EA-71 Jochen Schröder |
| REVISION | 1.04 |
| AUTHOR | MAGNA SFT EEE-S Bohlen Robert, Podpecan Mirko |
| COMMENT | SGBD Für E83 & E53Mü, kompatiabel ab SW 3.57 |
| PACKAGE | 1.14 |
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
- [STATUS_STATUSINFORMATIONEN](#job-status-statusinformationen) - dxc Status und Fehlerinformation KWP2000: $21 ReadDataByLocalIdentifier LID01 Modus  : Default
- [STATUS_AKTUATOR_STROM](#job-status-aktuator-strom) - Aktuator_Strom KWP2000: $21 ReadDataByLocalIdentifier LID02 Modus  : Default
- [STATUS_PHISMSPERRE](#job-status-phismsperre) - KWP2000: $21 ReadDataByLocalIdentifier LID03 Modus  : Default
- [STATUS_T_E_MOT](#job-status-t-e-mot) - Thermische Belastung des Aktuator Stellmotor KWP2000: $21 ReadDataByLocalIdentifier LID04 Modus  : Default
- [STATUS_THR_STRS_E_MOT](#job-status-thr-strs-e-mot) - Thermische Belastung des Aktuator Stellmotor KWP2000: $21 ReadDataByLocalIdentifier LID05 Modus  : Default
- [STATUS_T_OEL_DXC](#job-status-t-oel-dxc) - Oel Temperatur VGSG KWP2000: $21 ReadDataByLocalIdentifier LID06 Modus  : Default
- [STATUS_THR_STRS_CLT](#job-status-thr-strs-clt) - Thermische Belastung der Kupplung KWP2000: $21 ReadDataByLocalIdentifier LID07 Modus  : Default
- [STATUS_MK_SOLL](#job-status-mk-soll) - MK_Soll KWP2000: $21 ReadDataByLocalIdentifier LID08 Modus  : Default
- [STATUS_MK_IST](#job-status-mk-ist) - MK_Ist KWP2000: $21 ReadDataByLocalIdentifier LID09 Modus  : Default
- [STATUS_CODIERSTATUS](#job-status-codierstatus) - Codierung KWP2000: $21 ReadDataByLocalIdentifier LID0A Modus  : Default
- [STATUS_V_FZG](#job-status-v-fzg) - KWP2000: $21 ReadDataByLocalIdentifier LID0B Modus  : Default
- [STATUS_N_MOT](#job-status-n-mot) - Motordrehzahl KWP2000: $21 ReadDataByLocalIdentifier LID0C Modus  : Default
- [STATUS_KLEMMENSPANNUNG](#job-status-klemmenspannung) - Klemmenspannung am Verteilergetriebe KWP2000: $21 ReadDataByLocalIdentifier LID0D Modus  : Default
- [STATUS_GETRIEBE_INTEGRATOREN](#job-status-getriebe-integratoren) - Getriebe Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID0E Modus  : Default
- [STATUS_LAMELLEN_INTEGRATOREN](#job-status-lamellen-integratoren) - Lamellen Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID0F Modus  : Default
- [STATUS_KLASSIERSPEICHER](#job-status-klassierspeicher) - Wiederstandsklassierung des Getriebe KWP2000: $21 ReadDataByLocalIdentifier LID11 Modus  : Default
- [STATUS_CODIERDATEN](#job-status-codierdaten) - dxc Status und Fehlerinformation KWP2000: $21 ReadDataByLocalIdentifier LID1A Modus  : Default
- [STATUS_LT_GETRIEBE_INTEGRATOREN](#job-status-lt-getriebe-integratoren) - Life Time Getriebe Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1E Modus  : Default
- [STATUS_LT_LAMELLEN_INTEGRATOREN](#job-status-lt-lamellen-integratoren) - Life Time Lamellen Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1F Modus  : Default
- [STATUS_KALIBRIERUNG](#job-status-kalibrierung) - dxc Status und Fehlerinformation KWP2000: $21 ReadDataByLocalIdentifier LID21 Modus  : Default
- [WRITE_MK_SOLL](#job-write-mk-soll) - Sollmomentvorgabe per Diagnose KWP2000: $3B WriteDataByLocalIdentifier Modus: Default
- [WRITE_GETRIEBE_INTEGRATOREN](#job-write-getriebe-integratoren) - Getriebe Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier Modus: Default
- [WRITE_LAMELLEN_INTEGRATOREN](#job-write-lamellen-integratoren) - Lamellen Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier Modus: Default
- [STEUERN_KLASSIERSPEICHER_RUECKSETZEN](#job-steuern-klassierspeicher-ruecksetzen) - Widerstandsklasse des Getriebe neu setzen KWP2000: $3B WriteDataByLocalIdentifier LID11 Modus: Default
- [WRITE_LT_GETRIEBE_INTEGRATOREN](#job-write-lt-getriebe-integratoren) - Lifetime Getriebe Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier Modus: Default
- [WRITE_LT_LAMELLEN_INTEGRATOREN](#job-write-lt-lamellen-integratoren) - Lifetime Lamellen Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier Modus: Default
- [STEUERN_KUPP_FUNKTIONSPRUEFUNG](#job-steuern-kupp-funktionspruefung) - KWP2000: $31 StartRoutineByLocalIdentifier $30 Funktionspruefung Kupplung Modus  : Default
- [STEUERN_HO_INTEGRATOREN_LOESCHEN](#job-steuern-ho-integratoren-loeschen) - KWP2000: $31 StartRoutineByLocalIdentifier $31 Funktionspruefung Kupplung Modus  : Default
- [STEUERN_KALIBRIERUNG_LOESCHEN](#job-steuern-kalibrierung-loeschen) - KWP2000: $31 StartRoutineByLocalIdentifier $32 Funktionspruefung Kupplung Modus  : Default
- [STEUERN_LT_INTEGRATOREN_LOESCHEN](#job-steuern-lt-integratoren-loeschen) - KWP2000: $31 StartRoutineByLocalIdentifier $33 Funktionspruefung Kupplung Modus  : Default
- [STEUERN_FUNKTIONSPRUEFUNG](#job-steuern-funktionspruefung) - KWP2000: $31 StartRoutineByLocalIdentifier $32 Kalibrierung loeschen KWP2000: $11 ECUReset $01 PowerOn KWP2000: $31 StartRoutineByLocalIdentifier $30 Funktionspruefung Kupplung Modus  : Default
- [STATUS_AKTUELLES_AIF_LESEN](#job-status-aktuelles-aif-lesen) - Auslesen des Anwender Informations Feldes KWP 2000: $1A ReadEcuIdentification LID86 Modus   : Default
- [VGSG_DIAGNOSE_TESTJOB](#job-vgsg-diagnose-testjob) - Job fuer VGSG Diagnosetest KWP2000*: Modus  : Default

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

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default

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

<a id="job-status-statusinformationen"></a>
### STATUS_STATUSINFORMATIONEN

dxc Status und Fehlerinformation KWP2000: $21 ReadDataByLocalIdentifier LID01 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ERR_INFO_DXC_TEXT | string |  |
| STAT_ERR_INFO_DXC_WERT | int |  |
| STAT_STATUS_INFO_DXC_TEXT | string |  |
| STAT_STATUS_INFO_DXC_WERT | int |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktuator-strom"></a>
### STATUS_AKTUATOR_STROM

Aktuator_Strom KWP2000: $21 ReadDataByLocalIdentifier LID02 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AKTUATOR_STROM_WERT | real | Bit0 - Bit15: Aktuator_Strom |
| STAT_AKTUATOR_STROM_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-phismsperre"></a>
### STATUS_PHISMSPERRE

KWP2000: $21 ReadDataByLocalIdentifier LID03 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PHISMSPERRE_WERT | real | Istmoment das auf den CAN ausgegeben wird |
| STAT_PHISMSPERRE_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-t-e-mot"></a>
### STATUS_T_E_MOT

Thermische Belastung des Aktuator Stellmotor KWP2000: $21 ReadDataByLocalIdentifier LID04 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_T_E_MOT_WERT | int | Belastungsgrad des Stellmotores, THR_STRS_E_MOT |
| STAT_T_E_MOT_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-thr-strs-e-mot"></a>
### STATUS_THR_STRS_E_MOT

Thermische Belastung des Aktuator Stellmotor KWP2000: $21 ReadDataByLocalIdentifier LID05 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_THERMISCHE_BELASTUNG_E_MOTOR_WERT | int | Belastungsgrad des Stellmotores, THR_STRS_E_MOT |
| STAT_THERMISCHE_BELASTUNG_E_MOTOR_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-t-oel-dxc"></a>
### STATUS_T_OEL_DXC

Oel Temperatur VGSG KWP2000: $21 ReadDataByLocalIdentifier LID06 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_T_OEL_DXC_WERT | int |  |
| STAT_T_OEL_DXC_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-thr-strs-clt"></a>
### STATUS_THR_STRS_CLT

Thermische Belastung der Kupplung KWP2000: $21 ReadDataByLocalIdentifier LID07 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_THERMISCHE_BELASTUNG_KUPPLUNG_WERT | int | Belastungsgrad des Stellmotores, THR_STRS_E_MOT |
| STAT_THERMISCHE_BELASTUNG_KUPPLUNG_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mk-soll"></a>
### STATUS_MK_SOLL

MK_Soll KWP2000: $21 ReadDataByLocalIdentifier LID08 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MK_SOLL_WERT | int | Sollmoment, das am CAN anliegt |
| STAT_MK_SOLL_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mk-ist"></a>
### STATUS_MK_IST

MK_Ist KWP2000: $21 ReadDataByLocalIdentifier LID09 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MK_IST_WERT | int | Istmoment das auf den CAN ausgegeben wird |
| STAT_MK_IST_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierstatus"></a>
### STATUS_CODIERSTATUS

Codierung KWP2000: $21 ReadDataByLocalIdentifier LID0A Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CODIERUNG_TEXT | string |  |
| STAT_CODIERUNG_WERT | int |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-v-fzg"></a>
### STATUS_V_FZG

KWP2000: $21 ReadDataByLocalIdentifier LID0B Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STATUS_V_FZG_WERT | real | Istmoment das auf den CAN ausgegeben wird |
| STATUS_V_FZG_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-n-mot"></a>
### STATUS_N_MOT

Motordrehzahl KWP2000: $21 ReadDataByLocalIdentifier LID0C Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_N_MOT_WERT | int | Motordrehzahl |
| STAT_N_MOT_EINHEIT | string | physikalische Einheit der Motordrehzahl |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klemmenspannung"></a>
### STATUS_KLEMMENSPANNUNG

Klemmenspannung am Verteilergetriebe KWP2000: $21 ReadDataByLocalIdentifier LID0D Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KLEMMENSPANNUNG_VG_WERT | real | Klemmenspannung am Verteilergetriebe |
| STAT_KLEMMENSPANNUNG_VG_EINHEIT | string | physikalische Einheit der Klemmenspannung |
| STAT_KLEMME_15_TEXT | string | Klemme 15 Ein oder Aus |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-getriebe-integratoren"></a>
### STATUS_GETRIEBE_INTEGRATOREN

Getriebe Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID0E Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GETRIEBE_1_WERT | real | Integrator Getriebe |
| STAT_GETRIEBE_1_EINHEIT | string |  |
| STAT_GETRIEBE_2_WERT | real | Integrator Getriebe |
| STAT_GETRIEBE_2_EINHEIT | string |  |
| STAT_INTEGRATOR_KM_WERT | real | Integrator Getriebe |
| STAT_INTEGRATOR_KM_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lamellen-integratoren"></a>
### STATUS_LAMELLEN_INTEGRATOREN

Lamellen Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID0F Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LAMELLE_1_WERT | real | Integrator Lamellen |
| STAT_LAMELLE_1_EINHEIT | string |  |
| STAT_LAMELLE_2_WERT | real | Integrator Lamellen |
| STAT_LAMELLE_2_EINHEIT | string |  |
| STAT_LAMELLE_3_WERT | real | Integrator Lamellen |
| STAT_LAMELLE_3_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klassierspeicher"></a>
### STATUS_KLASSIERSPEICHER

Wiederstandsklassierung des Getriebe KWP2000: $21 ReadDataByLocalIdentifier LID11 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RESISTOR_KLASS_AKTUAL_TEXT | string |  |
| STAT_RESISTOR_KLASS_AKTUAL_WERT | int |  |
| STAT_RESISTOR_KLASS_EEPROM_TEXT | string |  |
| STAT_RESISTOR_KLASS_EEPROM_WERT | int |  |
| STAT_RESISTOR_KLASS_ADC_TEXT | string |  |
| STAT_RESISTOR_KLASS_ADC_WERT | int |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierdaten"></a>
### STATUS_CODIERDATEN

dxc Status und Fehlerinformation KWP2000: $21 ReadDataByLocalIdentifier LID1A Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BAUREIHE_TEXT | string | Baureihe 2-bit |
| STAT_NOTLAUFREGLER_TEXT | string | Notlaufrgeler 1-bit |
| STAT_GETRIEBEVARIANTE_TEXT | string | CAN-Datensatz fuer Getriebevariante 1-Byte |
| STAT_REIFENRADIUS_WERT | real | Dynamischer Reifenradius 2-Byte |
| STAT_REIFENRADIUS_EINHEIT | string | Dynamischer Reifenradius 2-Byte |
| STAT_GETRIEBE_US_SS1_WERT | real | Getriebe-Uebersetzung 1. Stuetzstelle 2-Byte |
| STAT_GETRIEBE_US_SS2_WERT | real | Getriebe-Uebersetzung 2. Stuetzstelle 2-Byte |
| STAT_GETRIEBE_US_SS3_WERT | real | Getriebe-Uebersetzung 3. Stuetzstelle 2-Byte |
| STAT_GETRIEBE_US_SS4_WERT | real | Getriebe-Uebersetzung 4. Stuetzstelle 2-Byte |
| STAT_GETRIEBE_US_SS5_WERT | real | Getriebe-Uebersetzung 5. Stuetzstelle 2-Byte |
| STAT_GETRIEBE_US_SS6_WERT | real | Getriebe-Uebersetzung 6. Stuetzstelle 2-Byte |
| STAT_GETRIEBE_US_SS7_WERT | real | Getriebe-Uebersetzung 7. Stuetzstelle 2-Byte |
| STAT_ACHS_US_WERT | real | Achs-Uebersetzung 2-Byte |
| STAT_KUPPLUNG_MK_SS1_WERT | real | Momentenkennlinie der Allradkupplung 1. Stuetzstelle 2-Byte |
| STAT_KUPPLUNG_MK_SS2_WERT | real | Momentenkennlinie der Allradkupplung 2. Stuetzstelle 2-Byte |
| STAT_KUPPLUNG_MK_SS3_WERT | real | Momentenkennlinie der Allradkupplung 3. Stuetzstelle 2-Byte |
| STAT_KUPPLUNG_MK_SS4_WERT | real | Momentenkennlinie der Allradkupplung 4. Stuetzstelle 2-Byte |
| STAT_KUPPLUNG_MK_SS5_WERT | real | Momentenkennlinie der Allradkupplung 5. Stuetzstelle 2-Byte |
| STAT_KUPPLUNG_MK_SS6_WERT | real | Momentenkennlinie der Allradkupplung 6. Stuetzstelle 2-Byte |
| STAT_KUPPLUNG_MK_SS7_WERT | real | Momentenkennlinie der Allradkupplung 7. Stuetzstelle 2-Byte |
| STAT_KUPPLUNG_MK_SS8_WERT | real | Momentenkennlinie der Allradkupplung 8. Stuetzstelle 2-Byte |
| STAT_KUPPLUNG_MK_SS9_WERT | real | Momentenkennlinie der Allradkupplung 9. Stuetzstelle 2-Byte |
| STAT_KUPPLUNG_MK_SS10_WERT | real | Momentenkennlinie der Allradkupplung 10. Stuetzstelle 2-Byte |
| STAT_KUPPLUNG_MK_EINHEIT | string | Momentenkennlinie der Allradkupplung 2-Byte |
| STAT_KUPPLUNG_KALIB_WERT | real | Momentenkonstante fuer Kupplungskalibrierung 1-Byte |
| STAT_KUPPLUNG_KALIB_EINHEIT | string | Momentenkonstante fuer Kupplungskalibrierung 1-Byte |
| STAT_KUPPLUNG_REG_WERT | real | Momentenkonstante fuer Kupplungsregelung 1-Byte |
| STAT_KUPPLUNG_REG_EINHEIT | string | Momentenkonstante fuer Kupplungsregelung 1-Byte |
| STAT_GRENZARBEIT_OEL_WERT | real | Grenzarbeit Ölschädigung 1-Byte |
| STAT_GRENZARBEIT_OEL_EINHEIT | string | Grenzarbeit Ölschädigung 1-Byte |
| STAT_SERVICE_WERT | real | Service-Interval 1-Byte |
| STAT_SERVICE_EINHEIT | string | Service-Interval 1-Byte |
| STAT_LAMELLEN_ARBEIT_1_WERT | real | Normierungsfaktor Ölschädigung 1-Byte |
| STAT_LAMELLEN_ARBEIT_2_WERT | real | Normierungsfaktor Ölschädigung 1-Byte |
| STAT_LAMELLEN_ARBEIT_3_WERT | real | Normierungsfaktor Ölschädigung 1-Byte |
| STAT_GETRIEBE_ARBEIT_1_WERT | real | Normierungsfaktor Ölschädigung 1-Byte |
| STAT_GETRIEBE_ARBEIT_2_WERT | real | Normierungsfaktor Ölschädigung 1-Byte |
| STAT_DIAG_SCH_00_TEXT | string | Diagnose Schalter 0 2-bit |
| STAT_DIAG_SCH_01_TEXT | string | Diagnose Schalter 1 2-bit |
| STAT_DIAG_SCH_02_TEXT | string | Diagnose Schalter 2 2-bit |
| STAT_DIAG_SCH_03_TEXT | string | Diagnose Schalter 3 2-bit |
| STAT_DIAG_SCH_04_TEXT | string | Diagnose Schalter 4 2-bit |
| STAT_DIAG_SCH_05_TEXT | string | Diagnose Schalter 5 2-bit |
| STAT_DIAG_SCH_06_TEXT | string | Diagnose Schalter 6 2-bit |
| STAT_DIAG_SCH_07_TEXT | string | Diagnose Schalter 7 2-bit |
| STAT_DIAG_SCH_08_TEXT | string | Diagnose Schalter 8 2-bit |
| STAT_DIAG_SCH_09_TEXT | string | Diagnose Schalter 9 2-bit |
| STAT_DIAG_SCH_10_TEXT | string | Diagnose Schalter 10 2-bit |
| STAT_DIAG_SCH_11_TEXT | string | Diagnose Schalter 11 2-bit |
| STAT_DIAG_SCH_12_TEXT | string | Diagnose Schalter 12 2-bit |
| STAT_DIAG_SCH_13_TEXT | string | Diagnose Schalter 13 2-bit |
| STAT_DIAG_SCH_14_TEXT | string | Diagnose Schalter 14 2-bit |
| STAT_DIAG_SCH_15_TEXT | string | Diagnose Schalter 15 2-bit |
| STAT_DIAG_SCH_16_TEXT | string | Diagnose Schalter 16 2-bit |
| STAT_DIAG_SCH_17_TEXT | string | Diagnose Schalter 17 2-bit |
| STAT_DIAG_SCH_18_TEXT | string | Diagnose Schalter 18 2-bit |
| STAT_DIAG_SCH_19_TEXT | string | Diagnose Schalter 19 2-bit |
| STAT_DIAG_SCH_20_TEXT | string | Diagnose Schalter 20 2-bit |
| STAT_DIAG_SCH_21_TEXT | string | Diagnose Schalter 21 2-bit |
| STAT_DIAG_SCH_22_TEXT | string | Diagnose Schalter 22 2-bit |
| STAT_DIAG_SCH_23_TEXT | string | Diagnose Schalter 23 2-bit |
| STAT_DIAG_SCH_24_TEXT | string | Diagnose Schalter 24 2-bit |
| STAT_DIAG_SCH_25_TEXT | string | Diagnose Schalter 25 2-bit |
| STAT_DIAG_SCH_26_TEXT | string | Diagnose Schalter 26 2-bit |
| STAT_DIAG_SCH_27_TEXT | string | Diagnose Schalter 27 2-bit |
| STAT_DIAG_SCH_28_TEXT | string | Diagnose Schalter 28 2-bit |
| STAT_DIAG_SCH_29_TEXT | string | Diagnose Schalter 29 2-bit |
| STAT_DIAG_SCH_30_TEXT | string | Diagnose Schalter 30 2-bit |
| STAT_DIAG_SCH_31_TEXT | string | Diagnose Schalter 31 2-bit |
| STAT_DIAG_SCH_32_TEXT | string | Diagnose Schalter 32 2-bit |
| STAT_DIAG_SCH_33_TEXT | string | Diagnose Schalter 33 2-bit |
| STAT_DIAG_SCH_34_TEXT | string | Diagnose Schalter 34 2-bit |
| STAT_DIAG_SCH_35_TEXT | string | Diagnose Schalter 35 2-bit |
| STAT_DIAG_SCH_36_TEXT | string | Diagnose Schalter 36 2-bit |
| STAT_DIAG_SCH_37_TEXT | string | Diagnose Schalter 37 2-bit |
| STAT_DIAG_SCH_38_TEXT | string | Diagnose Schalter 38 2-bit |
| STAT_DIAG_SCH_39_TEXT | string | Diagnose Schalter 39 2-bit |
| STAT_DIAG_SCH_40_TEXT | string | Diagnose Schalter 40 2-bit |
| STAT_DIAG_SCH_41_TEXT | string | Diagnose Schalter 41 2-bit |
| STAT_DIAG_SCH_42_TEXT | string | Diagnose Schalter 42 2-bit |
| STAT_DIAG_SCH_43_TEXT | string | Diagnose Schalter 43 2-bit |
| STAT_DIAG_SCH_44_TEXT | string | Diagnose Schalter 44 2-bit |
| STAT_DIAG_SCH_45_TEXT | string | Diagnose Schalter 45 2-bit |
| STAT_DIAG_SCH_46_TEXT | string | Diagnose Schalter 46 2-bit |
| STAT_DIAG_SCH_47_TEXT | string | Diagnose Schalter 47 2-bit |
| STAT_DIAG_SCH_48_TEXT | string | Diagnose Schalter 48 2-bit |
| STAT_DIAG_SCH_49_TEXT | string | Diagnose Schalter 49 2-bit |
| STAT_DIAG_SCH_50_TEXT | string | Diagnose Schalter 50 2-bit |
| STAT_DIAG_SCH_51_TEXT | string | Diagnose Schalter 51 2-bit |
| STAT_DIAG_SCH_52_TEXT | string | Diagnose Schalter 52 2-bit |
| STAT_DIAG_SCH_53_TEXT | string | Diagnose Schalter 53 2-bit |
| STAT_DIAG_SCH_54_TEXT | string | Diagnose Schalter 54 2-bit |
| STAT_DIAG_SCH_55_TEXT | string | Diagnose Schalter 55 2-bit |
| STAT_DIAG_SCH_56_TEXT | string | Diagnose Schalter 56 2-bit |
| STAT_DIAG_SCH_57_TEXT | string | Diagnose Schalter 57 2-bit |
| STAT_DIAG_SCH_58_TEXT | string | Diagnose Schalter 58 2-bit |
| STAT_DIAG_SCH_59_TEXT | string | Diagnose Schalter 59 2-bit |
| STAT_DIAG_SCH_60_TEXT | string | Diagnose Schalter 60 2-bit |
| STAT_DIAG_SCH_61_TEXT | string | Diagnose Schalter 61 2-bit |
| STAT_DIAG_SCH_62_TEXT | string | Diagnose Schalter 62 2-bit |
| STAT_DIAG_SCH_63_TEXT | string | Diagnose Schalter 63 2-bit |
| STAT_OFFSETKORREKTUR_0_WERT | real | Offset-Korrektur fuer Klassierwiderstand A |
| STAT_OFFSETKORREKTUR_1_WERT | real | Offset-Korrektur fuer Klassierwiderstand B |
| STAT_OFFSETKORREKTUR_2_WERT | real | Offset-Korrektur fuer Klassierwiderstand C |
| STAT_OFFSETKORREKTUR_3_WERT | real | Offset-Korrektur fuer Klassierwiderstand D |
| STAT_OFFSETKORREKTUR_4_WERT | real | Offset-Korrektur fuer Klassierwiderstand E |
| STAT_OFFSETKORREKTUR_5_WERT | real | Offset-Korrektur fuer Klassierwiderstand F |
| STAT_OFFSETKORREKTUR_6_WERT | real | Offset-Korrektur fuer Klassierwiderstand G |
| STAT_OFFSETKORREKTUR_7_WERT | real | Offset-Korrektur fuer Klassierwiderstand H |
| STAT_OFFSETKORREKTUR_8_WERT | real | Offset-Korrektur fuer Klassierwiderstand J |
| STAT_OFFSETKORREKTUR_9_WERT | real | Offset-Korrektur fuer Klassierwiderstand K |
| STAT_OFFSETKORREKTUR_10_WERT | real | Offset-Korrektur fuer Klassierwiderstand L |
| STAT_OFFSETKORREKTUR_11_WERT | real | Offset-Korrektur fuer Klassierwiderstand M |
| STAT_OFFSETKORREKTUR_12_WERT | real | Offset-Korrektur fuer Klassierwiderstand N |
| STAT_OFFSETKORREKTUR_13_WERT | real | Offset-Korrektur fuer Klassierwiderstand P |
| STAT_OFFSETKORREKTUR_14_WERT | real | Offset-Korrektur fuer Klassierwiderstand Q |
| STAT_OFFSETKORREKTUR_EINHEIT | string | Offset-Korrektur fuer Klassierwiderstand |
| STAT_STEIGUNGSKORREKTUR_0_WERT | real | Steigungs-Korrektur |
| STAT_STEIGUNGSKORREKTUR_1_WERT | real | Steigungs-Korrektur |
| STAT_STEIGUNGSKORREKTUR_2_WERT | real | Steigungs-Korrektur |
| STAT_STEIGUNGSKORREKTUR_3_WERT | real | Steigungs-Korrektur |
| STAT_STEIGUNGSKORREKTUR_4_WERT | real | Steigungs-Korrektur |
| STAT_STEIGUNGSKORREKTUR_EINHEIT | string | Steigungs-Korrektur |
| STAT_MSPERRMAX_WERT | real | Maximalmoment, dass von der Kupplung eingestellt wird |
| STAT_MSPERRMAX_EINHEIT | string | Maximalmoment, dass von der Kupplung eingestellt wird |
| STAT_SMKAL_WERT | real | Maximalmoment, dass von der Kupplung eingestellt wird |
| STAT_SMKAL_EINHEIT | string | Maximalmoment, dass von der Kupplung eingestellt wird |
| STAT_PHISTART_1_WERT | real | Startwinkel fuer Energiebetrachtung |
| STAT_PHISTART_EINHEIT | string | Startwinkel fuer Energiebetrachtung |
| STAT_BREITE_1_WERT | real | Breite des 1 Bereichs in der Rueckstellfeder |
| STAT_PHISTART_2_WERT | real | Startwinkel fuer Energiebetrachtung |
| STAT_BREITE_2_WERT | real | Breite des 2 Bereichs in der Rueckstellfeder |
| STAT_PHISTART_3_WERT | real | Breite des Sperrenbereichs in der letzten KalPhase |
| STAT_BREITE_3_WERT | real | Maximalmoment, dass von der Kupplung eingestellt wird |
| STAT_BREITE_EINHEIT | string | Breite der Bereiche in der Rueckstellfeder |
| STAT_KALSTART_WERT | real | Mindestenergie fuer Sperre, vor Start des letzten Kalbereichs |
| STAT_KALSTOP_WERT | real | Sperrenenergie, fuer Beendigung des Kalibriervorganges |
| STAT_KAL_EINHEIT | string | Sperrenenergie, fuer Beendigung des Kalibriervorganges |
| STAT_PHIDIFFMAX_WERT | real | Maximalwert delta fuer Vorwaerts/Rueckwaerts –kalibrierung |
| STAT_PHIDIFFMAX_EINHEIT | string | Maximalwert delta fuer Vorwaerts/Rueckwaerts –kalibrierung |
| STAT_OFFSETMAX_WERT | real | Maximale Korrektur zum Kalibrierergebnis ueber km-Stand |
| STAT_OFFSETMAX_EINHEIT | string | Maximale Korrektur zum Kalibrierergebnis ueber km-Stand |
| STAT_OFFSETFAKTOR_WERT | real | Maximale Korrekturfaktor zum Kalibrierergebnis ueber km-Stand |
| STAT_OFFSETFAKTOR_EINHEIT | string | Maximale Korrekturfaktor zum Kalibrierergebnis ueber km-Stand |
| STAT_OEL_FS_LOGIK | string | Oel-Fuellung Lifetime 1-bit |
| STAT_CS_TEXT | string | Checksumme der gesamten CBD |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lt-getriebe-integratoren"></a>
### STATUS_LT_GETRIEBE_INTEGRATOREN

Life Time Getriebe Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1E Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LT_GETRIEBE_1_WERT | real | Integrator Getriebe |
| STAT_LT_GETRIEBE_1_EINHEIT | string |  |
| STAT_LT_GETRIEBE_2_WERT | real | Integrator Getriebe |
| STAT_LT_GETRIEBE_2_EINHEIT | string |  |
| STAT_LT_INTEGRATOR_KM_WERT | real | Integrator Getriebe |
| STAT_LT_INTEGRATOR_KM_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lt-lamellen-integratoren"></a>
### STATUS_LT_LAMELLEN_INTEGRATOREN

Life Time Lamellen Integratoren KWP2000: $21 ReadDataByLocalIdentifier LID1F Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LT_LAMELLE_1_WERT | real | Integrator Lamellen |
| STAT_LT_LAMELLE_1_EINHEIT | string |  |
| STAT_LT_LAMELLE_2_WERT | real | Integrator Lamellen |
| STAT_LT_LAMELLE_2_EINHEIT | string |  |
| STAT_LT_LAMELLE_3_WERT | real | Integrator Lamellen |
| STAT_LT_LAMELLE_3_EINHEIT | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kalibrierung"></a>
### STATUS_KALIBRIERUNG

dxc Status und Fehlerinformation KWP2000: $21 ReadDataByLocalIdentifier LID21 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIB_INFO_TEXT | string |  |
| STAT_KALIB_INFO_WERT | int |  |
| STAT_PHISPERREKAL_WERT | real | Istmoment das auf den CAN ausgegeben wird |
| STAT_PHISPERREKAL_EINHEIT | string |  |
| STAT_DELTAPHI_WERT | real | Differenz zum Erst-Kalibrierwinkel deltaPhi = Erst-Kalibrierwinkel - Aktueller-Kalibrierwinkel |
| STAT_DELTAPHI_EINHEIT | string |  |
| STAT_ZYKLEN_BIS_ZWANGSKALIB | int |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-mk-soll"></a>
### WRITE_MK_SOLL

Sollmomentvorgabe per Diagnose KWP2000: $3B WriteDataByLocalIdentifier Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_1 | string | Daten Sollmoment |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-getriebe-integratoren"></a>
### WRITE_GETRIEBE_INTEGRATOREN

Getriebe Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_1 | string | Daten GetriebeArbeit1 |
| DATEN_2 | string | Daten GetriebeArbeit2 |
| DATEN_3 | string | Daten KM Stand Integrator |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-lamellen-integratoren"></a>
### WRITE_LAMELLEN_INTEGRATOREN

Lamellen Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_1 | string | Daten Lamelle1 |
| DATEN_2 | string | Daten Lamelle2 |
| DATEN_3 | string | Daten Lamelle3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klassierspeicher-ruecksetzen"></a>
### STEUERN_KLASSIERSPEICHER_RUECKSETZEN

Widerstandsklasse des Getriebe neu setzen KWP2000: $3B WriteDataByLocalIdentifier LID11 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-lt-getriebe-integratoren"></a>
### WRITE_LT_GETRIEBE_INTEGRATOREN

Lifetime Getriebe Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_1 | string | Daten GetriebeArbeit1 |
| DATEN_2 | string | Daten GetriebeArbeit2 |
| DATEN_3 | string | Daten KM Stand Integrator |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-lt-lamellen-integratoren"></a>
### WRITE_LT_LAMELLEN_INTEGRATOREN

Lifetime Lamellen Integratoren ins EEPROM schreiben KWP2000: $3B WriteDataByLocalIdentifier Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_1 | string | Daten Lamelle1 |
| DATEN_2 | string | Daten Lamelle2 |
| DATEN_3 | string | Daten Lamelle3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kupp-funktionspruefung"></a>
### STEUERN_KUPP_FUNKTIONSPRUEFUNG

KWP2000: $31 StartRoutineByLocalIdentifier $30 Funktionspruefung Kupplung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ho-integratoren-loeschen"></a>
### STEUERN_HO_INTEGRATOREN_LOESCHEN

KWP2000: $31 StartRoutineByLocalIdentifier $31 Funktionspruefung Kupplung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kalibrierung-loeschen"></a>
### STEUERN_KALIBRIERUNG_LOESCHEN

KWP2000: $31 StartRoutineByLocalIdentifier $32 Funktionspruefung Kupplung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lt-integratoren-loeschen"></a>
### STEUERN_LT_INTEGRATOREN_LOESCHEN

KWP2000: $31 StartRoutineByLocalIdentifier $33 Funktionspruefung Kupplung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-funktionspruefung"></a>
### STEUERN_FUNKTIONSPRUEFUNG

KWP2000: $31 StartRoutineByLocalIdentifier $32 Kalibrierung loeschen KWP2000: $11 ECUReset $01 PowerOn KWP2000: $31 StartRoutineByLocalIdentifier $30 Funktionspruefung Kupplung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG_1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |

<a id="job-status-aktuelles-aif-lesen"></a>
### STATUS_AKTUELLES_AIF_LESEN

Auslesen des Anwender Informations Feldes KWP 2000: $1A ReadEcuIdentification LID86 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AIF_AKTUELL_FG_NR_TEXT | string | Fahrgestellnummer 7-stellig |
| STAT_AIF_AKTUELL_FG_NR_LANG_TEXT | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| STAT_AIF_AKTUELL_DATUM_TEXT | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| STAT_AIF_AKTUELL_ZB_NR_TEXT | string | BMW/Rover Zusammenbaunummer |
| STAT_AIF_AKTUELL_SW_NR_TEXT | string | BMW/Rover Datensatznummer - Softwarenummer |
| STAT_AIF_AKTUELL_BEHOERDEN_NR_TEXT | string | BMW/Rover Behoerdennummer |
| STAT_AIF_AKTUELL_HAENDLER_NR_TEXT | string | Haendlernummer |
| STAT_AIF_AKTUELL_SERIEN_NR_TEXT | string | Tester Seriennummer |
| STAT_AIF_AKTUELL_KM_TEXT | long | km-Stand bei der Programmierung |
| STAT_AIF_AKTUELL_PROG_NR_TEXT | string | Programmstandsnummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-vgsg-diagnose-testjob"></a>
### VGSG_DIAGNOSE_TESTJOB

Job fuer VGSG Diagnosetest KWP2000*: Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL_DATEN | int | Anzahl Datenbytes |
| DATEN_1 | int | Daten Byte 1 |
| DATEN_2 | int | Daten Byte 2 |
| DATEN_3 | int | Daten Byte 3 |
| DATEN_4 | int | Daten Byte 4 |
| DATEN_5 | int | Daten Byte 5 |
| DATEN_6 | int | Daten Byte 6 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VGSG_OUT | binary | Antwort von VGSG  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (72 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (53 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (7 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (30 × 5)
- [FF_X_0](#table-ff-x-0) (1 × 4)
- [FF_X_A](#table-ff-x-a) (1 × 5)
- [FF_0_B](#table-ff-0-b) (1 × 7)
- [FF_1_B](#table-ff-1-b) (1 × 5)
- [FF_2_B](#table-ff-2-b) (1 × 6)
- [FF_2_C](#table-ff-2-c) (1 × 6)
- [FF_3_B](#table-ff-3-b) (1 × 7)
- [FF_4_B](#table-ff-4-b) (1 × 6)
- [FF_5_B](#table-ff-5-b) (1 × 7)
- [FF_6_B](#table-ff-6-b) (1 × 7)
- [FF_7_B](#table-ff-7-b) (1 × 6)
- [FF_8_B](#table-ff-8-b) (1 × 7)
- [FF_9_B](#table-ff-9-b) (1 × 7)
- [FF_A_B](#table-ff-a-b) (1 × 7)
- [FF_B_B](#table-ff-b-b) (1 × 8)
- [KL15CAN](#table-kl15can) (3 × 2)
- [KL15](#table-kl15) (2 × 2)
- [NMOT](#table-nmot) (4 × 2)
- [RQ](#table-rq) (8 × 2)
- [DSC1](#table-dsc1) (6 × 2)
- [DME1](#table-dme1) (6 × 2)
- [ASC2](#table-asc2) (5 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (35 × 9)
- [MESSDATENTEXTE](#table-messdatentexte) (8 × 9)
- [IORTTEXTE](#table-iorttexte) (7 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (4 × 9)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0D | KWP2000* |
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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 53 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5208 | 5208 Stellmotor Verkabelung |
| 0x52D0 | 52D0 Inkrementalgeber DIR - Leitung |
| 0x52D1 | 52D1 Inkrementalgeber Versorgung |
| 0x52D2 | 52D2 Inkrementalgeber IMP - Leitung |
| 0x52D4 | 52D4 Inkrementalgeber unplausibel |
| 0x5398 | 5398 Prüfsummenfehler Programmcode |
| 0x5399 | 5399 Prüfsummenfehler EEPROM |
| 0x539A | 539A Watchdog Fehlfunktion |
| 0x539B | 539B Prüffehler  RAM |
| 0x539D | 539D Steuergerät interner Fehler |
| 0x53A0 | 53A0 Verteilergetriebe Steuergerät - Codierung |
| 0x53FB | 53FB FEHLENDE_VERSORGUNG |
| 0x53FC | 53FC KL30 Versorgungsspannung |
| 0x53FE | 53FE Unerwarteter Reset |
| 0x53FF | 53FF Kl15 Plausibilität |
| 0x5460 | 5460 Motorstrommessung Plausibilität |
| 0x5461 | 5461 Fehler Stellmotoransteuerung |
| 0x5462 | 5462 Fehler Stellmotor oder erhöhter Kraftbedarf Kupplung |
| 0x5463 | 5463 Bruch Mechanik |
| 0x54C4 | 54C4 Erstkalibrierung fehlerhaft |
| 0x54C5 | 54C5 Motorstrommessung Offset Strommessung |
| 0x54C6 | 54C6 Ölverschleiss |
| 0x55C0 | 55C0 Notlaufregler Abbruch |
| 0x55C4 | 55C4 CAN_MESSAGE_DSC1 |
| 0x55C5 | 55C5 CAN_MESSAGE_DME1 |
| 0x55C6 | 55C6 CAN_MESSAGE_DME2 |
| 0x55C8 | 55C8 CAN_MESSAGE_ASC2 |
| 0x55C9 | 55C9 CAN_MESSAGE_ASC4 |
| 0x55CA | 55CA CAN_MESSAGE_INSTR2 |
| 0x55CB | 55CB CAN_MESSAGE_INSTR3 |
| 0x55CC | 55CC CAN_MESSAGE_ASC1 |
| 0x55CD | 55CD CAN_MESSAGE_ASC3 |
| 0x55CE | 55CE CAN_MESSAGE_EGS1_SMG1 |
| 0x55CF | 55CF CAN_MESSAGE_EGS2 |
| 0x55D0 | 55D0 CAN_MESSAGE_LWS1 |
| 0xD607 | D607 CAN Bus Off |
| 0xD614 | D614 CAN_TIMEOUT_DSC1 |
| 0xD615 | D615 CAN_TIMEOUT_DME1 |
| 0xD616 | D616 CAN_TIMEOUT_DME2 |
| 0xD618 | D618 CAN_TIMEOUT_ASC2 |
| 0xD619 | D619 CAN_TIMEOUT_ASC4 |
| 0xD61A | D61A CAN_TIMEOUT_INSTR2 |
| 0xD61B | D61B CAN_TIMEOUT_INSTR3 |
| 0xD61C | D61C CAN_TIMEOUT_ASC1 |
| 0xD61D | D61D CAN_TIMEOUT_ASC3 |
| 0xD61E | D61E CAN_TIMEOUT_EGS1_SMG1 |
| 0xD61F | D61F CAN_TIMEOUT_EGS2 |
| 0xD620 | D620 CAN_TIMEOUT_LWS1 |
| 0x55C1 | 55C1 ALLRADVERLUST |
| 0x54C7 | 54C7 INC_MODEL_UNPLAUSIBEL |
| 0x54C8 | 54C8 Klassierwiderstand am Stellmotor |
| 0x539E | 539E Funktionsfehler VTG Gesamtsystem |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 7 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxx00xx | 20 | Text a |
| xxxx01xx | 21 | Text b |
| xxxx10xx | 22 | Text c |
| xxxx11xx | 23 | Text d |
| xxxxxx01 | 11 | Text x |
| xxxxxx10 | 12 | Text y |
| xxxxxxxx | 0 | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 30 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x5208 | 0x01 | FF_x_a | FF_3_b | - |
| 0x54C8 | 0x01 | FF_x_a | FF_3_b | - |
| 0x52D0 | 0x01 | FF_x_a | FF_2_b | FF_2_c |
| 0x52D1 | 0x01 | FF_x_a | FF_2_b | FF_2_c |
| 0x52D2 | 0x01 | FF_x_a | FF_2_b | FF_2_c |
| 0x52D4 | 0x01 | FF_x_a | FF_2_b | FF_2_c |
| 0x5398 | 0x01 | FF_x_a | FF_7_b | - |
| 0x5399 | 0x01 | FF_x_a | FF_7_b | - |
| 0x539A | 0x01 | FF_x_a | FF_4_b | - |
| 0x539B | 0x01 | FF_x_a | FF_4_b | - |
| 0x539D | 0x01 | FF_x_a | FF_4_b | - |
| 0x53A0 | 0x01 | FF_x_a | FF_4_b | - |
| 0x53FB | 0x01 | FF_x_a | FF_1_b | 0x0F |
| 0x53FC | 0x01 | FF_x_a | FF_2_b | FF_2_c |
| 0x53FE | 0x01 | FF_x_a | FF_1_b | 0x0F |
| 0x53FF | 0x01 | FF_x_a | FF_0_b | - |
| 0x5460 | 0x01 | FF_x_a | FF_6_b | - |
| 0x5461 | 0x01 | FF_x_a | FF_6_b | - |
| 0x5462 | 0x01 | FF_x_a | FF_6_b | - |
| 0x5463 | 0x01 | FF_x_a | FF_6_b | - |
| 0x54C4 | 0x01 | FF_x_a | FF_6_b | - |
| 0x54C5 | 0x01 | FF_x_a | FF_6_b | - |
| 0x54C6 | 0x01 | FF_x_a | FF_0_b | - |
| 0x54C7 | 0x01 | FF_x_a | FF_6_b | - |
| 0x539E | 0x01 | FF_x_a | FF_6_b | - |
| 0x55C4 | 0x01 | FF_x_a | FF_8_b | - |
| 0x55C5 | 0x01 | FF_x_a | FF_9_b | - |
| 0x55C8 | 0x01 | FF_x_a | FF_A_b | - |
| 0x55C1 | 0x01 | FF_x_a | FF_B_b | - |
| default | 0x01 | FF_x_a | FF_5_b | - |

<a id="table-ff-x-0"></a>
### FF_X_0

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x02 | 0x03 | 0x04 |

<a id="table-ff-x-a"></a>
### FF_X_A

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x02 | 0x03 | 0x04 | 0x05 |

<a id="table-ff-0-b"></a>
### FF_0_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B |

<a id="table-ff-1-b"></a>
### FF_1_B

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x06 | 0x0B | 0x12 | 0x13 |

<a id="table-ff-2-b"></a>
### FF_2_B

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x0E | 0x07 | 0x08 | 0x09 | 0x0B |

<a id="table-ff-2-c"></a>
### FF_2_C

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x15 | 0x16 | 0x17 | 0x18 | 0x19 |

<a id="table-ff-3-b"></a>
### FF_3_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x09 | 0x0B | 0x13 | 0x0E |

<a id="table-ff-4-b"></a>
### FF_4_B

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x0E | 0x0B | 0x1A | 0x12 | 0x13 |

<a id="table-ff-5-b"></a>
### FF_5_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x14 |

<a id="table-ff-6-b"></a>
### FF_6_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x0E | 0x07 | 0x10 | 0x09 | 0x0B | 0x11 |

<a id="table-ff-7-b"></a>
### FF_7_B

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x1B | 0x1C | 0x1A | 0x12 | 0x13 |

<a id="table-ff-8-b"></a>
### FF_8_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x1D |

<a id="table-ff-9-b"></a>
### FF_9_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x1E |

<a id="table-ff-a-b"></a>
### FF_A_B

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0B | 0x1F |

<a id="table-ff-b-b"></a>
### FF_B_B

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x20 | 0x21 | 0x0B | 0x09 | 0x22 | 0x23 | 0x24 |

<a id="table-kl15can"></a>
### KL15CAN

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | CAN Signal OK -- KL15 aus |
| 0x01 | CAN Signal OK -- KL15 ein |
| 0xXY | CAN Signal Timeout -- KL15 unbekannt |

<a id="table-kl15"></a>
### KL15

Dimensions: 2 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | KL15. aus |
| 0x04 | KL15. ein |

<a id="table-nmot"></a>
### NMOT

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | CAN Signal OK -- VKM aus |
| 0x08 | CAN Signal OK -- VKM ein |
| 0x10 | Ersatzwert -- VKM aus |
| 0x18 | Ersatzwert -- VKM ein |

<a id="table-rq"></a>
### RQ

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | UNKOWN_SOURCE |
| 0x20 | EE_RST_MARKER |
| 0x40 | OSEK_SHUTDOWN |
| 0x60 | BASIS_DRIVER_ERROR |
| 0x80 | UNDER_VOLTAGE |
| 0xA0 | INTERNAL_WATCHDOG |
| 0xC0 | EXTERN_WATCHDOG |
| 0xE0 | NO RESET |

<a id="table-dsc1"></a>
### DSC1

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | DSC1_MK_SOLL |
| 0x02 | DSC1_S_OEFFNEN |
| 0x04 | DSC1_DYN_MK_SOLL |
| 0x08 | DSC1_FKT_TEST |
| 0x10 | DSC1_NL_OEFFNEN  |
| 0xXY | multiple Signals |

<a id="table-dme1"></a>
### DME1

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | DME1_DDE1_N_MOT |
| 0x02 | DME1_DDE1_MD_IND_NE |
| 0x04 | DME1_DDE1_MD_IND |
| 0x08 | DME1_DDE1_MD_REIB |
| 0x10 | DME1_DDE1_S_KL15 |
| 0xXY | multiple Signals |

<a id="table-asc2"></a>
### ASC2

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | ASC2_VRD_RV_ASC |
| 0x02 | ASC2_VRD_LV_ASC |
| 0x04 | ASC2_VRD_RH_ASC |
| 0x08 | ASC2_VRD_LH_ASC |
| 0xXY | multiple Signals |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 35 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Eingangsspannung KL30 | Volt | - | unsigned char | - |  1 |  8 | 0 |
| 0x02 | KL15 Status CAN | 0-n | - | 0x03 | KL15CAN |  1 |  1 | 0 |
| 0x03 | KL15 Intern | 0-n | - | 0x04 | KL15 |  1 |  1 | 0 |
| 0x04 | Motordrehzahl | 0-n | - | 0x18 | NMOT |  1 |  1 | 0 |
| 0x05 | Reset-Quelle | 0-n | - | 0xE0 | RQ |  1 |  1 | 0 |
| 0x06 | MKSOLL | Nm | - | unsigned char | - | 10 |  1 | 0 |
| 0x07 | MSperrIstPosLim | Nm | - | unsigned char | - |  8 |  1 | 0 |
| 0x08 | deltaPhiSperreCal | Grad | - | unsigned char | - | -1 |  1 | 0 |
| 0x09 | SperreError | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0x0A | SperreState | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0x0B | SperreMainState | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0x0E | iSM | Ampere | - | signed char | - |  1 |  2 | 0 |
| 0x0F | ResetWhileEngineOn | 0/1 | - | 0x01 | - |  1 |  1 | 0 |
| 0x10 | Fehlerzähler Kalibrierversuche | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0x11 | Fehlerzähler Zeitüberschreitung | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0x12 | SwErrNr | HEX | - | unsigned int | H |  1 |  1 | 0 |
| 0x13 | SGTemp | Grad C | - | signed char | - |  2 |  1 | 0 |
| 0x14 | CAN_Fehlersignale | 1 | - | unsigned char | _ |  1 |  1 | 0 |
| 0x15 | uSM_IE_VCC_ST | 0/1 | - | 0x01 | - |  1 |  1 | 0 |
| 0x16 | Plausib_Ink_Gradient | 0/1 | - | 0x02 | - |  1 |  1 | 0 |
| 0x17 | Plausib_Ink_Frequenz | 0/1 | - | 0x04 | - |  1 |  1 | 0 |
| 0x18 | Plausib_MotorModell | 0/1 | - | 0x08 | - |  1 |  1 | 0 |
| 0x19 | Plausib_Ink_Wackler | 0/1 | - | 0x10 | - |  1 |  1 | 0 |
| 0x1A | Page Number | HEX | - | unsigned char | - |  1 |  1 | 0 |
| 0x1B | Info | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0x1C | Status | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0x1D | DSC1_Fehlersignale | 0-n | - | 0x1F | DSC1 |  1 |  1 | 0 |
| 0x1E | DME1_Fehlersignale | 0-n | - | 0x1F | DME1 |  1 |  1 | 0 |
| 0x1F | ASC2_Fehlersignale | 0-n | - | 0x0F | ASC2 |  1 |  1 | 0 |
| 0x20 | SperreNotlauf | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0x21 | EP_Sperre | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0x22 | ExeptionHandlingKUPPSTAT | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0x23 | ExeptionHandlingKUPPSTATERR | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0x24 | ErrorKUPPSTAT | 1 | - | unsigned char | - |  1 |  1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - |  1 |  1 | 0 |

<a id="table-messdatentexte"></a>
### MESSDATENTEXTE

Dimensions: 8 rows × 9 columns

| MDNR | MDTEXT | MD_EINH | L/H | MDTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Status Kupplung | - | -- | unsigned char | -- |  1 |  1 | 0 |
| 0x02 | Aktuator Strom | Amp | -- | signed int | -- | 12 | 77 | 0 |
| 0x04 | Motortemperatur | Grad C | -- | signed int | -- |  1 | 128 | 0 |
| 0x05 | Motorbelastungsgrad | Prozent | -- | unsigned char | -- |  1 |  1 | 0 |
| 0x0C | Motordrehzahl | 1/min | -- | unsigned int | -- | 12 | 77 | 0 |
| 0x0D | Batteriespannung | Volt | -- | unsigned char | -- |  1 |  8 | 0 |
| 0x10 | Aktuatorposition | Grad | -- | signed int | -- |  1 | 16 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | low | unsigned char | -- |  1 |  1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 7 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5398 | Prüfsummenfehler Programmcode |
| 0x5399 | Prüfsummenfehler EEPROM |
| 0x539B | Prüffehler  RAM |
| 0x1004 | Fehler d |
| 0x1005 | Fehler e |
| 0x1006 | Fehler f |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 5 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_HFK | nein |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | -- | -- |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | -- | unsigned char | -- | 1 | 22 | 0 |
| 0x02 | Aussentemperatur | Grad C | -- | signed char | -- | 1 | 1 | 0 |
| 0x03 | Motordrehzahl | 1/min | low | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |
