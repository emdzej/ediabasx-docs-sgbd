# EMF_70.prg

- Jobs: [74](#jobs)
- Tables: [41](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EMF_70 |
| ORIGIN | BMW EE-24 Mark |
| REVISION | 1.004 |
| AUTHOR | Siemens_VDO_Automotive_AG SV_C_BC_P1_AD_SW Peter, Siemens_VDO_Automotive_AG SV_C_BC_P1_AD_SW Erras, Siemens_VDO_Automotive_AG SV_C_BC_P1_AD_SW Thomas |
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
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
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
- [STATUS_FESTELLKRAFT_LESEN](#job-status-festellkraft-lesen) - Auslesen der erreichten Festellkraft (N) KWP2000: $22 ReadDataByCommonIdentifier $0001 F_ERREICHT Modus  : Default
- [STATUS_PROGRAMM_DATE](#job-status-programm-date) - Ausgabe des Programming Date aus UIF KWP2000: $1A  ReadECUIdentification $99  PD Modus  : Default
- [STATUS_BMW_DIAG_INDEX](#job-status-bmw-diag-index) - Auslesen des BMW Diagnoseindex aus ZIF KWP2000: $1A  ReadECUIdentification $9C  VDCI Modus  : Default
- [STATUS_LETZTE_LOESEKRAFT](#job-status-letzte-loesekraft) - Auslesen der letzten Loesekraft (N) KWP2000: $22 ReadDataByCommonIdentifier $0014 F_LOESE Modus  : Default
- [STATUS_LETZTE_ANZUGSKRAFT](#job-status-letzte-anzugskraft) - Auslesen der letzten Anzugskraft (N) KWP2000: $22 ReadDataByCommonIdentifier $0015 F_ANZ Modus  : Default
- [STATUS_AKTUELLE_ISTKRAFT](#job-status-aktuelle-istkraft) - Auslesen der aktuellen Istkraft(N) KWP2000: $22 ReadDataByCommonIdentifier $0016 F_IST Modus  : Default
- [STATUS_BETAETIGUNGSZAEHLER_ANZ](#job-status-betaetigungszaehler-anz) - Lesen des Betaetigungszaehlers Taster Richtung Anziehen KWP2000: $22 ReadDataByCommonIdentifier $0017 BETAET_ZAEHLER_ANZ Modus  : Default
- [STATUS_BETAETIGUNGSZAEHLER_LOES](#job-status-betaetigungszaehler-loes) - Betaetigungszaehler Taster Richtung Loesen KWP2000: $22 ReadDataByCommonIdentifier $0018 BETAET_ZAEHLER_LOES Modus  : Default
- [STATUS_ANZAHL_FESTSTELLVORGAENGE](#job-status-anzahl-feststellvorgaenge) - Anzahl der Feststellvorgaenge KWP2000: $22 ReadDataByCommonIdentifier $0019 ANZ_FESTSTELL_VORG Modus  : Default
- [STATUS_ANZAHL_NOTENTRIEGELUNGEN](#job-status-anzahl-notentriegelungen) - Anzahl der Notentriegelungen KWP2000: $22 ReadDataByCommonIdentifier $0020 ANZ_NOTENTRIEG Modus  : Default
- [STATUS_ANZAHL_DEGRADED_MODI](#job-status-anzahl-degraded-modi) - Anzahl der Degraded Modi KWP2000: $22 ReadDataByCommonIdentifier $0021 ANZ_DEGRADED_MODE Modus  : Default
- [STATUS_EMF_BUTTON](#job-status-emf-button) - Auslesen des Status der EMF-Taste KWP2000: $30 InputOutputControlByLocalIdentifier $30 STATUS_EMF_BUTTON Modus  : Default
- [STEUERN_MONTAGE_MODE](#job-steuern-montage-mode) - Montagemodus ein/ausschalten KWP2000: $31 StartRoutineByLocalIdentifier $21 MONTAGE_MODE Modus  : Default
- [STEUERN_MONTAGE_POS](#job-steuern-montage-pos) - EMF in Montageposition fahren KWP2000: $31 StartRoutineByLocalIdentifier $20 MONTAGE_POS Modus  : Default
- [STATUS_KRAFTSENSOR](#job-status-kraftsensor) - Auslesen des Kraftsensors KWP2000: $30 InputOutputControlByLocalIdentifier $1901 FORCE Modus  : Default
- [STATUS_AD_MOTOR](#job-status-ad-motor) - Auslesen der AD-Werte des Motors KWP2000: $30 InputOutputControlByLocalIdentifier $2001 AD_MOT Modus  : Default
- [STATUS_AD_KLEMME_30_15](#job-status-ad-klemme-30-15) - Auslesen der AD-Werte von KL30E, KL30P und KL15 KWP2000: $30 InputOutputControlByLocalIdentifier $2101 AD_KL Modus  : Default
- [STATUS_AD_S1_BIS_S4](#job-status-ad-s1-bis-s4) - Auslesen der AD-Werte der Tastereingänge S1 bis S4 KWP2000: $30 InputOutputControlByLocalIdentifier $2201 AD_S Modus  : Default
- [STATUS_AD_TEMP](#job-status-ad-temp) - Auslesen der AD-Werte des PCB Temperatursensors KWP2000: $30 InputOutputControlByLocalIdentifier $2301 AD_TEMP Modus  : Default
- [STATUS_MOTORSTROM](#job-status-motorstrom) - Auslesen Motorstrom KWP2000: $30 InputOutputControlByLocalIdentifier $31 I_MOT $01 RCS Modus  : Default
- [STATUS_BMW_TEILE_NR](#job-status-bmw-teile-nr) - Auslesen der BMW_Teilenummer KWP2000: $1A  ReadECUIdentification $91  VMECUHN Modus  : Default
- [STEUERN_NAECHSTE_FESTSTELLKRAFT](#job-steuern-naechste-feststellkraft) - Feststellkraft fuer naechsten Anziehvorgang KWP2000: $3B WriteDataByLocalIdentifier $FA RLI = F_FESTSTELLEN Modus  : Default
- [STATUS_ANZAHL_NACHZIEHEN_SOLL_IST](#job-status-anzahl-nachziehen-soll-ist) - Anzahl Nachziehvorgaenge mit Soll Ist Vergleich KWP2000: $22 ReadDataByCommonIdentifier $0022 NB_TIGHTENING_CMP Modus  : Default
- [STATUS_ANZAHL_NACHZIEHEN_BOOST_LESEN](#job-status-anzahl-nachziehen-boost-lesen) - Auslesen Anzahl Boost KWP2000: $22 ReadDataByCommonIdentifier $0023 F_ERREICHT Modus  : Default
- [STATUS_SW_VERSION_BOOT_LESEN](#job-status-sw-version-boot-lesen) - Auslesen Software Version BOOT KWP2000: $31 ReadDataByCommonIdentifier $FB F_ERREICHT Modus  : Default
- [STATUS_SW_VERSION_SLAVE_LESEN](#job-status-sw-version-slave-lesen) - Auslesen Software Version SLAVE KWP2000: $31 ReadDataByCommonIdentifier $FB F_ERREICHT Modus  : Default
- [STATUS_GESCHWINDIGKEIT_RDZ](#job-status-geschwindigkeit-rdz) - Auslesen Radgeschwindigkeit KWP2000: $30 InputOutputControlByLocalIdentifier $1001 WS Modus  : Default
- [STATUS_DIGITALEINGAENGE_BUTTON](#job-status-digitaleingaenge-button) - Auslesen der Digitaleingänge KWP2000: $30 InputOutputControlByLocalIdentifier $1801 DIGIN Modus  : Default

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

<a id="job-status-festellkraft-lesen"></a>
### STATUS_FESTELLKRAFT_LESEN

Auslesen der erreichten Festellkraft (N) KWP2000: $22 ReadDataByCommonIdentifier $0001 F_ERREICHT Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_F_ERREICHT_WERT | int | Bereich: 0-65535 |
| STAT_F_ERREICHT_EINH | string | N |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-programm-date"></a>
### STATUS_PROGRAMM_DATE

Ausgabe des Programming Date aus UIF KWP2000: $1A  ReadECUIdentification $99  PD Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PROGRAMM_DATE | string | BMW Diagindex aus ZIF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bmw-diag-index"></a>
### STATUS_BMW_DIAG_INDEX

Auslesen des BMW Diagnoseindex aus ZIF KWP2000: $1A  ReadECUIdentification $9C  VDCI Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BMW_DIAG_INX | int | BMW Diagindex aus ZIF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-letzte-loesekraft"></a>
### STATUS_LETZTE_LOESEKRAFT

Auslesen der letzten Loesekraft (N) KWP2000: $22 ReadDataByCommonIdentifier $0014 F_LOESE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LETZTE_LOESEKRAFT_WERT | int | Bereich: 0-65535 |
| STAT_LETZTE_LOESEKRAFT_EINH | string | N |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-letzte-anzugskraft"></a>
### STATUS_LETZTE_ANZUGSKRAFT

Auslesen der letzten Anzugskraft (N) KWP2000: $22 ReadDataByCommonIdentifier $0015 F_ANZ Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LETZTE_ANZUGSKRAFT_WERT | int | Bereich: 0-65535 |
| STAT_LETZTE_ANZUGSKRAFT_EINH | string | N |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktuelle-istkraft"></a>
### STATUS_AKTUELLE_ISTKRAFT

Auslesen der aktuellen Istkraft(N) KWP2000: $22 ReadDataByCommonIdentifier $0016 F_IST Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AKTUELLE_ISTKRAFT_WERT | int | Bereich: 0-65535 |
| STAT_AKTUELLE_ISTKRAFT_EINH | string | N |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betaetigungszaehler-anz"></a>
### STATUS_BETAETIGUNGSZAEHLER_ANZ

Lesen des Betaetigungszaehlers Taster Richtung Anziehen KWP2000: $22 ReadDataByCommonIdentifier $0017 BETAET_ZAEHLER_ANZ Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETAETIGUNGSZAEHLER_ANZ_WERT | int | Bereich: 0-4294967295 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betaetigungszaehler-loes"></a>
### STATUS_BETAETIGUNGSZAEHLER_LOES

Betaetigungszaehler Taster Richtung Loesen KWP2000: $22 ReadDataByCommonIdentifier $0018 BETAET_ZAEHLER_LOES Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETAETIGUNGSZAEHLER_LOES_WERT | int | Bereich: 0-4294967295 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-anzahl-feststellvorgaenge"></a>
### STATUS_ANZAHL_FESTSTELLVORGAENGE

Anzahl der Feststellvorgaenge KWP2000: $22 ReadDataByCommonIdentifier $0019 ANZ_FESTSTELL_VORG Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANZAHL_FESTSTELLVORGAENGE_WERT | int | Bereich: 0-4294967295 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-anzahl-notentriegelungen"></a>
### STATUS_ANZAHL_NOTENTRIEGELUNGEN

Anzahl der Notentriegelungen KWP2000: $22 ReadDataByCommonIdentifier $0020 ANZ_NOTENTRIEG Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANZAHL_NOTENTRIEGELUNGEN_WERT | int | Bereich: 0-65535 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-anzahl-degraded-modi"></a>
### STATUS_ANZAHL_DEGRADED_MODI

Anzahl der Degraded Modi KWP2000: $22 ReadDataByCommonIdentifier $0021 ANZ_DEGRADED_MODE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANZAHL_DEGRADED_MODI_WERT | int | Bereich: 0-65535 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-emf-button"></a>
### STATUS_EMF_BUTTON

Auslesen des Status der EMF-Taste KWP2000: $30 InputOutputControlByLocalIdentifier $30 STATUS_EMF_BUTTON Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EMF_BUTTON_WERT | int | 0:neutral 1:gezogen 2:gedrueckt 3:sonstiges |
| STAT_EMF_BUTTON_TEXT | string | neutral, gezogen, gedrueckt, sonstiges |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-montage-mode"></a>
### STEUERN_MONTAGE_MODE

Montagemodus ein/ausschalten KWP2000: $31 StartRoutineByLocalIdentifier $21 MONTAGE_MODE Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MONTAGEMODUS | int | Bereich: 0-1, 1 = Montagemode_ein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-montage-pos"></a>
### STEUERN_MONTAGE_POS

EMF in Montageposition fahren KWP2000: $31 StartRoutineByLocalIdentifier $20 MONTAGE_POS Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kraftsensor"></a>
### STATUS_KRAFTSENSOR

Auslesen des Kraftsensors KWP2000: $30 InputOutputControlByLocalIdentifier $1901 FORCE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AD_KRAFTSENSOR_WERT | int | Bereich: 0-65535 |
| STAT_AD_KRAFTSENSOR_EINH | string | mV |
| STAT_KRAFTSENSOR_WERT | int | Bereich: 0-65535 |
| STAT_KRAFTSENSOR_EINH | string | N |
| STAT_AD_ROHDATEN_WERT | int | Bereich: 0-65535 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ad-motor"></a>
### STATUS_AD_MOTOR

Auslesen der AD-Werte des Motors KWP2000: $30 InputOutputControlByLocalIdentifier $2001 AD_MOT Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AD_MON_MOT_WERT | int | Bereich: 0-65535 |
| STAT_AD_MON_MOT_EINH | string | mV |
| STAT_AD_KL30_MOT_WERT | int | Bereich: 0-65535 |
| STAT_AD_KL30_MOT_EINH | string | mV |
| STAT_AD_MON_MOT_RAW_WERT | int | Bereich: 0-65535 |
| STAT_AD_KL30_MOT_RAW_WERT | int | Bereich: 0-65535 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ad-klemme-30-15"></a>
### STATUS_AD_KLEMME_30_15

Auslesen der AD-Werte von KL30E, KL30P und KL15 KWP2000: $30 InputOutputControlByLocalIdentifier $2101 AD_KL Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AD_KL30E_WERT | int | Bereich: 0-65535 |
| STAT_AD_KL30E_EINH | string | mV |
| STAT_AD_KL30P_WERT | int | Bereich: 0-65535 |
| STAT_AD_KL30P_EINH | string | mV |
| STAT_AD_KL15_WERT | int | Bereich: 0-65535 |
| STAT_AD_KL15_EINH | string | mV |
| STAT_AD_KL30E_RAW_WERT | int | Bereich: 0-65535 |
| STAT_AD_KL30P_RAW_WERT | int | Bereich: 0-65535 |
| STAT_AD_KL15_RAW_WERT | int | Bereich: 0-65535 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ad-s1-bis-s4"></a>
### STATUS_AD_S1_BIS_S4

Auslesen der AD-Werte der Tastereingänge S1 bis S4 KWP2000: $30 InputOutputControlByLocalIdentifier $2201 AD_S Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AD_S1_SLAVE_WERT | int | Bereich: 0-65535 |
| STAT_AD_S1_SLAVE_EINH | string | mV |
| STAT_AD_S2_SLAVE_WERT | int | Bereich: 0-65535 |
| STAT_AD_S2_SLAVE_EINH | string | mV |
| STAT_AD_S3_SLAVE_WERT | int | Bereich: 0-65535 |
| STAT_AD_S3_SLAVE_EINH | string | mV |
| STAT_AD_S4_SLAVE_WERT | int | Bereich: 0-65535 |
| STAT_AD_S4_SLAVE_EINH | string | mV |
| STAT_AD_S2_MASTER_WERT | int | Bereich: 0-65535 |
| STAT_AD_S2_MASTER_EINH | string | mV |
| STAT_AD_S1_SLAVE_RAW_WERT | int | Bereich: 0-65535 |
| STAT_AD_S2_SLAVE_RAW_WERT | int | Bereich: 0-65535 |
| STAT_AD_S3_SLAVE_RAW_WERT | int | Bereich: 0-65535 |
| STAT_AD_S4_SLAVE_RAW_WERT | int | Bereich: 0-65535 |
| STAT_AD_S2_MASTER_RAW_WERT | int | Bereich: 0-65535 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ad-temp"></a>
### STATUS_AD_TEMP

Auslesen der AD-Werte des PCB Temperatursensors KWP2000: $30 InputOutputControlByLocalIdentifier $2301 AD_TEMP Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TEMP_PCB_WERT | int | Bereich: 0-65535 |
| STAT_TEMP_PCB_EINH | string | °C |
| STAT_AD_TEMP_PCB_WERT | int | Bereich: 0-65535 |
| STAT_AD_TEMP_PCB_EINH | string | mV |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motorstrom"></a>
### STATUS_MOTORSTROM

Auslesen Motorstrom KWP2000: $30 InputOutputControlByLocalIdentifier $31 I_MOT $01 RCS Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AD_I_MOT_WERT | int | Bereich: 0-65535 |
| STAT_AD_I_MOT_EINH | string | 100mA |
| STAT_AD_I_MOT_RAW_WERT | long | Bereich: 0-65535 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bmw-teile-nr"></a>
### STATUS_BMW_TEILE_NR

Auslesen der BMW_Teilenummer KWP2000: $1A  ReadECUIdentification $91  VMECUHN Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BMW_TEILE_NR_1 | string | BMW_Teilenummer 1 |
| STAT_BMW_TEILE_NR_2 | string | BMW_Teilenummer 2 |
| STAT_BMW_TEILE_NR_3 | string | BMW_Teilenummer 3 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-naechste-feststellkraft"></a>
### STEUERN_NAECHSTE_FESTSTELLKRAFT

Feststellkraft fuer naechsten Anziehvorgang KWP2000: $3B WriteDataByLocalIdentifier $FA RLI = F_FESTSTELLEN Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FESTSTELLKRAFT | int | Bereich: 0-65535 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-anzahl-nachziehen-soll-ist"></a>
### STATUS_ANZAHL_NACHZIEHEN_SOLL_IST

Anzahl Nachziehvorgaenge mit Soll Ist Vergleich KWP2000: $22 ReadDataByCommonIdentifier $0022 NB_TIGHTENING_CMP Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANZAHL_NACHZIEHEN_SOLL_IST_WERT | int | Bereich: 0-65535 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-anzahl-nachziehen-boost-lesen"></a>
### STATUS_ANZAHL_NACHZIEHEN_BOOST_LESEN

Auslesen Anzahl Boost KWP2000: $22 ReadDataByCommonIdentifier $0023 F_ERREICHT Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANZAHL_NACHZIEHEN_BOOST_WERT | int | Bereich: 0-65535 |
| STAT_ANZAHL_NACHZIEHEN_BOOST_EINH | string | n |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sw-version-boot-lesen"></a>
### STATUS_SW_VERSION_BOOT_LESEN

Auslesen Software Version BOOT KWP2000: $31 ReadDataByCommonIdentifier $FB F_ERREICHT Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SW_VERSION_BOOT_X | int | Bereich: 0-255 |
| STAT_SW_VERSION_BOOT_Y | int | Bereich: 0-255 |
| STAT_SW_VERSION_BOOT_Z | int | Bereich: 0-255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sw-version-slave-lesen"></a>
### STATUS_SW_VERSION_SLAVE_LESEN

Auslesen Software Version SLAVE KWP2000: $31 ReadDataByCommonIdentifier $FB F_ERREICHT Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SW_VERSION_SLAVE_X | int | Bereich: 0-255 |
| STAT_SW_VERSION_SLAVE_Y | int | Bereich: 0-255 |
| STAT_SW_VERSION_SLAVE_Z | int | Bereich: 0-255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geschwindigkeit-rdz"></a>
### STATUS_GESCHWINDIGKEIT_RDZ

Auslesen Radgeschwindigkeit KWP2000: $30 InputOutputControlByLocalIdentifier $1001 WS Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GESCHW_RDZ_VALID | char | 0x01 = VALID 0x00 = INVALID |
| STAT_GESCHW_RDZ_WERT | int | Bereich: 0-65535 |
| STAT_GESCHW_RDZ_EINH | string | km/h |
| STAT_PERIOD_GESCHW_RDZ_WERT | long | Bereich: 0-16777216 |
| STAT_PERIOD_GESCHW_RDZ_EINH | string | us |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digitaleingaenge-button"></a>
### STATUS_DIGITALEINGAENGE_BUTTON

Auslesen der Digitaleingänge KWP2000: $30 InputOutputControlByLocalIdentifier $1801 DIGIN Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DIGITALEINGAENGE_BUTTON | char | Bit0: S1_D  Bit1: S2_D  Bit2: S3_D  Bit3: S4_D |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (43 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (127 × 9)
- [FARTTYP](#table-farttyp) (43 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (78 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [ACTUATOR_STATES](#table-actuator-states) (8 × 2)
- [MOTOR_STATES](#table-motor-states) (9 × 2)
- [UMWELTBEDINGUNG_D_1](#table-umweltbedingung-d-1) (1 × 5)
- [UMWELTBEDINGUNG_A_1](#table-umweltbedingung-a-1) (1 × 7)
- [UMWELTBEDINGUNG_D_2](#table-umweltbedingung-d-2) (1 × 21)
- [ACTIVITY_MODE](#table-activity-mode) (6 × 2)
- [LOFO_EMF](#table-lofo-emf) (5 × 2)
- [ENB_STG_ACT](#table-enb-stg-act) (5 × 2)
- [APPLY_PERMISSION](#table-apply-permission) (3 × 2)
- [UMWELTBEDINGUNG_D_3](#table-umweltbedingung-d-3) (1 × 29)
- [TESTCASEMASTERFAILED](#table-testcasemasterfailed) (12 × 2)
- [TESTCASESLAVEFAILED](#table-testcaseslavefailed) (10 × 2)
- [SLAVE_GESCHWINDIGKEIT](#table-slave-geschwindigkeit) (5 × 2)
- [SLAVE_STELLANFORDERUNG](#table-slave-stellanforderung) (5 × 2)
- [SLAVE_GETRIEBEDATEN](#table-slave-getriebedaten) (5 × 2)
- [SLAVE_KLEMMENSTATUS](#table-slave-klemmenstatus) (5 × 2)
- [BLOCKNUMBERDATAERROR](#table-blocknumberdataerror) (36 × 2)
- [BLOCKNUMBERSOFTERROR](#table-blocknumbersofterror) (36 × 2)
- [S1](#table-s1) (4 × 2)
- [S2](#table-s2) (4 × 2)
- [S3](#table-s3) (4 × 2)
- [S4](#table-s4) (4 × 2)

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

Dimensions: 43 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x600B | ECU_EEPROM_SOFT |
| 0x600C | PER_BUTTON_RAW |
| 0x600D | ECU_EEPROM_DATA |
| 0x600E | ECU_RELAY_MOSFET |
| 0x600F | ECU_TEMP_SENSOR |
| 0x6010 | ECU_SCS |
| 0x6011 | ECU_MOTOR_CIRCUIT |
| 0x6012 | ECU_FORCE |
| 0x6013 | ECU_TEMPERATURE |
| 0x6014 | ECU_MASTER |
| 0x6015 | ECU_SLAVE |
| 0x6016 | ECU_SLAVE_FLASH |
| 0x6017 | ECU_SPI |
| 0x6018 | ECU_SECURITY_ACCESS |
| 0x6019 | PER_BUTTON_APPLY |
| 0x601A | ECU_SLAVE_CAN |
| 0x601B | CAN_RX_SIGNAL_GESCHWINDIGKEIT |
| 0x601C | CAN_RX_SIGNAL_GETRIEBEDATEN |
| 0x601D | CAN_RX_SIGNAL_STAT_DSC |
| 0x601E | CAN_RX_SIGNAL_STELLANF |
| 0x6020 | PER_BUTTON_RELEASE |
| 0x6021 | PER_IGN_WAKE |
| 0x6022 | PER_WHEEL_SPEED |
| 0x6023 | PER_POWER_ SUPPLY |
| 0x6024 | ECU_CODING |
| 0x6025 | ECU_WRONG_REQUEST |
| 0x6031 | MECH_MANUAL_MOVED |
| 0x6032 | MECH_FORCE |
| 0x6034 | MECH_MOTION_TIMEOUT |
| 0x6040 | ESP_DEFECT |
| 0x6041 | ESP_CAN_FAULT |
| 0x6042 | ESP_NACHZIEHEN |
| 0x6043 | ESP_SIGNAL |
| 0x6044 | KLEMME30G |
| 0x6045 | ESP_STAT_DSC_SOFT |
| 0xD387 | CAN_BUS |
| 0xD394 | CAN_GESCHWINDIGKEIT_416 |
| 0xD395 | CAN_GETRIEBEDATEN_186 |
| 0xD397 | CAN_KLEMMENSTATUS_304 |
| 0xD398 | CAN_STAT_ DSC_414 |
| 0xD399 | CAN_STELLANF_EMF_423 |
| 0xD39A | CAN_NACHLAUFZEIT_STROMVERSORGUNG_958 |
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
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | Umweltbedingung_D_1 | Umweltbedingung_A_1 | Umweltbedingung_D_2 | Umweltbedingung_D_3 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 127 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x03 | nicht benutzt | 0/1 | - | 0x04 | - | - | - | - |
| 0x0C | nicht benutzt | Volt | - | unsigned char | - | 1 | 10 | 0 |
| 0x0D | nicht benutzt | Volt | - | unsigned char | - | 1 | 10 | 0 |
| 0x0E | nicht benutzt | Volt | - | unsigned char | - | 1 | 10 | 0 |
| 0x0F | nicht benutzt | Volt | - | unsigned char | - | 1 | 10 | 0 |
| 0x14 | nicht benutzt | 0/1 | low | 0x00000010 | - | - | - | - |
| 0x15 | nicht benutzt | 0/1 | low | 0x00000020 | - | - | - | - |
| 0x16 | nicht benutzt | 0/1 | low | 0x00000040 | - | - | - | - |
| 0x17 | nicht benutzt | 0/1 | low | 0x00000080 | - | - | - | - |
| 0x1C | Position Handverstellung | 0/1 | low | 0x00004000 | - | - | - | - |
| 0x1D | Nullposition kalibriert | 0/1 | low | 0x00008000 | - | - | - | - |
| 0x1E | nicht benutzt | 0/1 | low | 0x00010000 | - | - | - | - |
| 0x1F | nicht benutzt | 0/1 | low | 0x00020000 | - | - | - | - |
| 0x20 | nicht benutzt | 0/1 | low | 0x00040000 | - | - | - | - |
| 0x21 | nicht benutzt | 0/1 | low | 0x00080000 | - | - | - | - |
| 0x22 | nicht benutzt | 0/1 | low | 0x00100000 | - | - | - | - |
| 0x23 | nicht benutzt | 0/1 | low | 0x00200000 | - | - | - | - |
| 0x24 | nicht benutzt | 0/1 | low | 0x00400000 | - | - | - | - |
| 0x25 | nicht benutzt | 0/1 | low | 0x00800000 | - | - | - | - |
| 0x26 | Stilllegungsstufen | 0-n | low | 0x07000000 | Activity_Mode | - | - | - |
| 0x3A | EE_Block_0 | 0/1 | low | 0x00000001 | - | - | - | - |
| 0x3B | EE_Block_1 | 0/1 | low | 0x00000002 | - | - | - | - |
| 0x3C | EE_Block_2 | 0/1 | low | 0x00000004 | - | - | - | - |
| 0x3D | EE_Block_3 | 0/1 | low | 0x00000008 | - | - | - | - |
| 0x3E | EE_Block_4 | 0/1 | low | 0x00000010 | - | - | - | - |
| 0x3F | EE_Block_5 | 0/1 | low | 0x00000020 | - | - | - | - |
| 0x40 | EE_Block_6 | 0/1 | low | 0x00000040 | - | - | - | - |
| 0x41 | EE_Block_7 | 0/1 | low | 0x00000080 | - | - | - | - |
| 0x42 | EE_Block_8 | 0/1 | low | 0x00000100 | - | - | - | - |
| 0x43 | EE_Block_9 | 0/1 | low | 0x00000200 | - | - | - | - |
| 0x44 | EE_Block_10 | 0/1 | low | 0x00000400 | - | - | - | - |
| 0x45 | EE_Block_11 | 0/1 | low | 0x00000800 | - | - | - | - |
| 0x46 | EE_Block_12 | 0/1 | low | 0x00001000 | - | - | - | - |
| 0x47 | EE_Block_13 | 0/1 | low | 0x00002000 | - | - | - | - |
| 0x48 | EE_Block_14 | 0/1 | low | 0x00004000 | - | - | - | - |
| 0x49 | EE_Block_15 | 0/1 | low | 0x00008000 | - | - | - | - |
| 0x4A | EE_Block_16 | 0/1 | low | 0x00010000 | - | - | - | - |
| 0x4B | EE_Block_17 | 0/1 | low | 0x00020000 | - | - | - | - |
| 0x4C | EE_Block_18 | 0/1 | low | 0x00040000 | - | - | - | - |
| 0x4D | EE_Block_19 | 0/1 | low | 0x00080000 | - | - | - | - |
| 0x4E | EE_Block_20 | 0/1 | low | 0x00100000 | - | - | - | - |
| 0x4F | EE_Block_21 | 0/1 | low | 0x00200000 | - | - | - | - |
| 0x50 | EE_Block_22 | 0/1 | low | 0x00400000 | - | - | - | - |
| 0x51 | EE_Block_23 | 0/1 | low | 0x00800000 | - | - | - | - |
| 0x52 | EE_Block_24 | 0/1 | low | 0x01000000 | - | - | - | - |
| 0x53 | EE_Block_25 | 0/1 | low | 0x02000000 | - | - | - | - |
| 0x54 | EE_Block_26 | 0/1 | low | 0x04000000 | - | - | - | - |
| 0x55 | EE_Block_27 | 0/1 | low | 0x08000000 | - | - | - | - |
| 0x56 | EE_Block_28 | 0/1 | low | 0x10000000 | - | - | - | - |
| 0x57 | EE_Block_29 | 0/1 | low | 0x20000000 | - | - | - | - |
| 0x58 | EE_Block_30 | 0/1 | low | 0x40000000 | - | - | - | - |
| 0x59 | EE_Block_31 | 0/1 | low | 0x80000000 | - | - | - | - |
| 0x5A | BRP 1 entspricht ungueltig | 0/1 | low | 0x00010000 | - | - | - | - |
| 0x5B | ST_GR_GRB 1 entspricht ungueltig | 0/1 | low | 0x00020000 | - | - | - | - |
| 0x5C | FLLUPT_GPWSUP 1 entspricht ungueltig | 0/1 | low | 0x00040000 | - | - | - | - |
| 0x5D | T_SEC_COU_REL 1 entspricht ungueltig | 0/1 | low | 0x00080000 | - | - | - | - |
| 0x5E | nicht benutzt | 0/1 | low | 0x00100000 | - | - | - | - |
| 0x5F | nicht benutzt | 0/1 | low | 0x00200000 | - | - | - | - |
| 0x60 | nicht benutzt | 0/1 | low | 0x00400000 | - | - | - | - |
| 0x61 | nicht benutzt | 0/1 | low | 0x00800000 | - | - | - | - |
| 0x62 | nicht benutzt | 0/1 | low | 0x01000000 | - | - | - | - |
| 0x63 | nicht benutzt | 0/1 | low | 0x02000000 | - | - | - | - |
| 0x64 | nicht benutzt | 0/1 | low | 0x04000000 | - | - | - | - |
| 0x65 | nicht benutzt | 0/1 | low | 0x08000000 | - | - | - | - |
| 0x66 | nicht benutzt | 0/1 | low | 0x10000000 | - | - | - | - |
| 0x67 | nicht benutzt | 0/1 | low | 0x20000000 | - | - | - | - |
| 0x68 | nicht benutzt | 0/1 | low | 0x40000000 | - | - | - | - |
| 0x69 | nicht benutzt | 0/1 | low | 0x80000000 | - | - | - | - |
| 0x6A | Relativzeit | Sek | - | unsigned int | - | 1 | 1 | 0 |
| 0x80 | Testfall Fehler Master | 0-n | low | 0x000000FF | TestCaseMasterFailed | - | - | - |
| 0x81 | Testfall Fehler Slave | 0-n | low | 0x0000FF00 | TestCaseSlaveFailed | - | - | - |
| 0x82 | Block number Data Error | 0-n | low | 0x00FF0000 | BlockNumberDataError | - | - | - |
| 0x83 | Block number Soft Error | 0-n | low | 0xFF000000 | BlockNumberSoftError | - | - | - |
| 0x85 | Relativzeit | Sek | - | unsigned int | - | 1 | 1 | 0 |
| 0x86 | Klemme 30 Motor Spannung | Volt | - | unsigned char | - | 1 | 10 | 0 |
| 0x87 | Zuendung Spannung | Volt | - | unsigned char | - | 1 | 10 | 0 |
| 0x88 | RDZ | km/h | - | unsigned char | - | 1 | 1 | 0 |
| 0x89 | Leiterplatten Temperatur | Grad Celsius | - | unsigned char | - | 10 | 1 | 0 |
| 0x8A | Motor Ueberwachung Spannung | Volt | - | unsigned char | - | 1 | 10 | 0 |
| 0x90 | Taste Zustand digital S1 | 0-n | low | 0x00000003 | S1 | - | - | - |
| 0x91 | Taste Zustand digital S2 | 0-n | low | 0x0000000C | S2 | - | - | - |
| 0x92 | Taste Zustand digital S3 | 0-n | low | 0x00000030 | S3 | - | - | - |
| 0x93 | Taste Zustand digital S4 | 0-n | low | 0x000000C0 | S4 | - | - | - |
| 0x94 | Motor Zustand | 0-n | low | 0x00000700 | Motor_States | - | - | - |
| 0x95 | Motor blockiert | 0/1 | low | 0x00000800 | - | - | - | - |
| 0x96 | Motor Unterspannung | 0/1 | low | 0x00001000 | - | - | - | - |
| 0x97 | Motor Strom | 0/1 | low | 0x00002000 | - | - | - | - |
| 0x98 | Position Handverstellung | 0/1 | low | 0x00004000 | - | - | - | - |
| 0x99 | Nullposition kalibriert | 0/1 | low | 0x00008000 | - | - | - | - |
| 0x9A | Anziehen Taste gedrueckt | 0/1 | low | 0x00010000 | - | - | - | - |
| 0x9B | Loesen Taste gedrueckt | 0/1 | low | 0x00020000 | - | - | - | - |
| 0x9C | SCS active | 0/1 | low | 0x00040000 | - | - | - | - |
| 0x9D | Zuendung | 0/1 | low | 0x00080000 | - | - | - | - |
| 0x9E | Unterspannung | 0/1 | low | 0x00100000 | - | - | - | - |
| 0x9F | Aktuator Zustand | 0-n | low | 0x00E00000 | Actuator_States | - | - | - |
| 0xA0 | Stilllegungsstufen | 0-n | low | 0x07000000 | Activity_Mode | - | - | - |
| 0xA1 | LOFO_EMF | 0-n | low | 0x18000000 | LOFO_EMF | - | - | - |
| 0xA2 | ENB_STG_ACT | 0-n | low | 0x60000000 | ENB_STG_ACT | - | - | - |
| 0xA3 | HW Freigabe Anziehen | 0-n | low | 0x80000000 | Apply_Permission | - | - | - |
| 0xA5 | MILE_KM ungueltig | 0/1 | low | 0x00000001 | - | - | - | - |
| 0xA6 | ENB_STG_ACT 1 entspricht ungueltig | 0/1 | low | 0x00000002 | - | - | - | - |
| 0xA7 | LOFO_EMF 1 entspricht ungueltig | 0/1 | low | 0x00000004 | - | - | - | - |
| 0xA8 | ST_BRG_DYN_2 1 entspricht ungueltig | 0/1 | low | 0x00000008 | - | - | - | - |
| 0xA9 | ST_CFFU_EMF_2 1 entspricht ungueltig | 0/1 | low | 0x00000010 | - | - | - | - |
| 0xAA | ST_HYD_RETA_2 1 entspricht ungueltig | 0/1 | low | 0x00000020 | - | - | - | - |
| 0xAB | RQ_PPOS_GRB_2 1 entspricht ungueltig | 0/1 | low | 0x00000040 | - | - | - | - |
| 0xAC | ST_VEH_DVCO 1 entspricht ungueltig | 0/1 | low | 0x00000080 | - | - | - | - |
| 0xAD | V_VEH 1 entspricht ungueltig | 0/1 | low | 0x00000100 | - | - | - | - |
| 0xAE | ST_INTF_DSC_EMF 1 entspricht ungueltig | 0/1 | low | 0x00000200 | - | - | - | - |
| 0xAF | ST_KEY_PLGD 1 entspricht ungueltig | 0/1 | low | 0x00000400 | - | - | - | - |
| 0xB0 | ST_KL_15 1 entspricht ungueltig | 0/1 | low | 0x00000800 | - | - | - | - |
| 0xB1 | ST_KL_R 1 entspricht ungueltig | 0/1 | low | 0x00001000 | - | - | - | - |
| 0xB2 | RPM_GRB_NEGL 1 entspricht ungueltig | 0/1 | low | 0x00002000 | - | - | - | - |
| 0xB3 | ST_KL_50 1 entspricht ungueltig | 0/1 | low | 0x00004000 | - | - | - | - |
| 0xB4 | ST_CT_BRPD 1 entspricht ungueltig | 0/1 | low | 0x00008000 | - | - | - | - |
| 0xB5 | BRP1 entspricht ungueltig | 0/1 | low | 0x00010000 | - | - | - | - |
| 0xB6 | ST_GR_GRB 1 entspricht ungueltig | 0/1 | low | 0x00020000 | - | - | - | - |
| 0xB7 | FLLUPT_GPWSUP1 entspricht ungueltig | 0/1 | low | 0x00040000 | - | - | - | - |
| 0xB8 | T_SEC_COU_REL1 entspricht ungueltig | 0/1 | low | 0x00080000 | - | - | - | - |
| 0xB9 | nicht benutzt | 0/1 | low | 0x00100000 | - | - | - | - |
| 0xBA | nicht benutzt | 0/1 | low | 0x00200000 | - | - | - | - |
| 0xBB | nicht benutzt | 0/1 | low | 0x00400000 | - | - | - | - |
| 0xBC | nicht benutzt | 0/1 | low | 0x00800000 | - | - | - | - |
| 0xBD | SlaveGeschwindigkeit | 0-n | low | 0x03000000 | Slave_Geschwindigkeit | - | - | - |
| 0xBE | SlaveStellanforderung | 0-n | low | 0x0C000000 | Slave_Stellanforderung | - | - | - |
| 0xBF | SlaveGetriebedaten | 0-n | low | 0x30000000 | Slave_Getriebedaten | - | - | - |
| 0xC0 | SlaveKlemmenstatus | 0-n | low | 0xC0000000 | Slave_Klemmenstatus | - | - | - |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 43 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x600B | 0x0073 | 0x0072 | 0x0071 | 0x0070 |
| 0x600C | 0x0014 | 0x0013 | 0x0012 | 0x0011 |
| 0x600D | 0x0073 | 0x0072 | 0x0071 | 0x0070 |
| 0x600E | 0x007C | 0x007B | 0x007A | 0x0079 |
| 0x600F | 0xFFFF | 0xFFFF | 0x001C | 0x001B |
| 0x6010 | 0x0017 | 0xFFFF | 0x007E | 0x007D |
| 0x6011 | 0xFFFF | 0x0018 | 0x0019 | 0x001A |
| 0x6012 | 0xFFFF | 0xFFFF | 0x001C | 0x001B |
| 0x6013 | 0x001F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x6014 | 0x0082 | 0x0081 | 0x0080 | 0x007F |
| 0x6015 | 0xFFFF | 0x0081 | 0x0080 | 0x007F |
| 0x6016 | 0xFFFF | 0xFFFF | 0x0028 | 0x0027 |
| 0x6017 | 0xFFFF | 0x0032 | 0x0031 | 0x0030 |
| 0x6018 | 0xFFFF | 0xFFFF | 0x0022 | 0x0020 |
| 0x6019 | 0x0010 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x601A | 0x0078 | 0x0077 | 0x0076 | 0x0075 |
| 0x601B | 0x0010 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x601C | 0x0010 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x601D | 0x0010 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x601E | 0x0010 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x6020 | 0x0010 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x6021 | 0x0015 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x6022 | 0xFFFF | 0x0004 | 0xFFFF | 0x0001 |
| 0x6023 | 0x0043 | 0x0042 | 0x0041 | 0x0040 |
| 0x6024 | 0x0074 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x6025 | 0x0017 | 0x0085 | 0x0084 | 0x0083 |
| 0x6031 | 0xFFFF | 0x0050 | 0xFFFF | 0xFFFF |
| 0x6032 | 0x0053 | 0x0052 | 0xFFFF | 0x0051 |
| 0x6034 | 0x0057 | 0x0056 | 0x0055 | 0x0054 |
| 0x6040 | 0xFFFF | 0x0062 | 0xFFFF | 0xFFFF |
| 0x6041 | 0xFFFF | 0x0060 | 0xFFFF | 0xFFFF |
| 0x6042 | 0xFFFF | 0xFFFF | 0x0063 | 0xFFFF |
| 0x6043 | 0xFFFF | 0xFFFF | 0xFFFF | 0x0061 |
| 0x6044 | 0xFFFF | 0x0069 | 0xFFFF | 0xFFFF |
| 0x6045 | 0xFFFF | 0x0010 | 0xFFFF | 0xFFFF |
| 0xD387 | 0xFFFF | 0x0066 | 0x0065 | 0xFFFF |
| 0xD394 | 0x001E | 0x0069 | 0x0068 | 0xFFFF |
| 0xD395 | 0x001E | 0x0069 | 0x0068 | 0xFFFF |
| 0xD397 | 0x001E | 0x0069 | 0x0068 | 0xFFFF |
| 0xD398 | 0x001E | 0x0069 | 0x0068 | 0xFFFF |
| 0xD399 | 0x001E | 0x0069 | 0x0068 | 0xFFFF |
| 0xD39A | 0xFFFF | 0x0069 | 0xFFFF | 0xFFFF |
| default | 0x0008 | 0x0004 | 0x0002 | 0x0001 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 78 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0004 | kein Signal oder Wert |
| 0x0008 | unplausibles Signal oder Wert |
| 0x0010 | unplausibles Signal |
| 0x0011 | Kurzschluss nach Ubat (S1...S4) |
| 0x0012 | Kurzschluss nach GND (S1...S4) |
| 0x0013 | Leitungsbruch (S1...S4) |
| 0x0014 | Kommunikationsfehler Slave |
| 0x0015 | unplausibel |
| 0x0016 | 2 aus 3 Entscheidung |
| 0x0017 | SCS Leitung unplausibel |
| 0x0018 | Motor getrennt |
| 0x0019 | Motor Ueberstrom |
| 0x001A | Motor Ruhestrom |
| 0x001B | Kurzschluss nach Ubat |
| 0x001C | Kurzschluss nach Masse |
| 0x001D | EEPROM Datenfehler |
| 0x001E | Pruefsummenfehler |
| 0x001F | Uebertemperatur Leiterplatte |
| 0x0020 | SV |
| 0x0021 | OEM |
| 0x0022 | AM |
| 0x0023 | Relais A defekt |
| 0x0024 | Relais B defekt |
| 0x0025 | MOSFET getrennt |
| 0x0026 | MOSFET kurzgeschlossen |
| 0x0027 | Fehler bei Slave-Programmierung |
| 0x0028 | Master-Slave SW-Versions-Widerspruch |
| 0x0030 | Treiberfehler |
| 0x0031 | Protokollfehler |
| 0x0032 | Softwarefehler |
| 0x0040 | Ueberspannung |
| 0x0041 | Unterspannung |
| 0x0042 | KL30 Motor Versorgung fehlt |
| 0x0043 | KL30 Motor Versorgung ungueltig |
| 0x0050 | Notentriegelung festgestellt |
| 0x0051 | fehlerhaftes Signal |
| 0x0052 | physikalisch unplausibel |
| 0x0053 | Kalibrierung unplausibel |
| 0x0054 | Release_Timeout_Ziel |
| 0x0055 | Release_Timeout_Montageposition |
| 0x0056 | Apply_Timeout_Montageposition |
| 0x0057 | Apply_Timeout_Ziel |
| 0x0060 | CAN EHB nicht verfügbar |
| 0x0061 | EHB Anforderung nicht möglich |
| 0x0062 | EHB nicht verfügbar |
| 0x0063 | EHB Nachzieh-Anforderung |
| 0x0064 | Passiv-Fehler (TEC/REC) |
| 0x0065 | Status Bus ausgeschaltet |
| 0x0066 | keine CAN-Nachrichten |
| 0x0067 | ungueltiges CAN-Signal |
| 0x0068 | Alive-Zaehler falsch |
| 0x0069 | Timeout |
| 0x0070 | Kommunikationsfehler mit EEPROM |
| 0x0071 | Programmfehler |
| 0x0072 | Datenfehler |
| 0x0073 | Interfacefehler |
| 0x0074 | Datum außerhalb gültigen Bereich |
| 0x0075 | CanGetriebadaten186 Fehler |
| 0x0076 | CanKlemmenstatus304 Fehler |
| 0x0077 | CanStellanfEmf423 Fehler |
| 0x0078 | CanGeschwindigkeit416 Fehler |
| 0x0079 | Relais defekt |
| 0x007A | Motor Kurzschluss / Masseschluss |
| 0x007B | Mosfet defekt |
| 0x007C | Kommunikationsproblem mit Slave(SCS Leitung) |
| 0x007D | statischer SCS Test |
| 0x007E | dynamischer SCS Test |
| 0x007F | ROM Test / RAM Test |
| 0x0080 | Stack Test |
| 0x0081 | PFM Test |
| 0x0082 | OsekTask Test |
| 0x0083 | SPI Protokoll neg. Resp. |
| 0x0084 | falsche Antwort vom Slave |
| 0x0085 | Timeout Antwort vom Slave |
| 0xFFFF | unbekannte Fehlerart |

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

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

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

<a id="table-actuator-states"></a>
### ACTUATOR_STATES

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | undefiniert |
| 0x00200000 | Geloest |
| 0x00400000 | Angezogen |
| 0x00600000 | waehrend Loesen |
| 0x00800000 | waehrend Anziehen |
| 0x00A00000 | Montage Position |
| 0x00C00000 | tbd |
| 0x00E00000 | unbekannter Fehler |

<a id="table-motor-states"></a>
### MOTOR_STATES

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | Initialisierung |
| 0x00000100 | unbeschaeftigt |
| 0x00000200 | Anziehen_warten auf_Relais |
| 0x00000300 | Anziehen |
| 0x00000400 | Loesen_warten auf_Relais |
| 0x00000500 | Loesen |
| 0x00000600 | warten auf_Motor_Stopp |
| 0x00000700 | Kalibrierung |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-umweltbedingung-d-1"></a>
### UMWELTBEDINGUNG_D_1

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x80 | 0x81 | 0x82 | 0x83 |

<a id="table-umweltbedingung-a-1"></a>
### UMWELTBEDINGUNG_A_1

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x85 | 0x86 | 0x87 | 0x88 | 0x89 | 0x8A |

<a id="table-umweltbedingung-d-2"></a>
### UMWELTBEDINGUNG_D_2

Dimensions: 1 rows × 21 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR | UW17_NR | UW18_NR | UW19_NR | UW20_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20 | 0x90 | 0x91 | 0x92 | 0x93 | 0x94 | 0x95 | 0x96 | 0x97 | 0x98 | 0x99 | 0x9A | 0x9B | 0x9C | 0x9D | 0x9E | 0x9F | 0xA0 | 0xA1 | 0xA2 | 0xA3 |

<a id="table-activity-mode"></a>
### ACTIVITY_MODE

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | Initialisierung |
| 0x01000000 | Normaler Modus |
| 0x02000000 | Eingeschraenkter Modus |
| 0x03000000 | Normaler inaktiver Modus |
| 0x04000000 | Eingeschraenkter inaktiver Modus |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-lofo-emf"></a>
### LOFO_EMF

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | keine Anforderung |
| 0x08000000 | Loesen Anforderung |
| 0x10000000 | Anziehen Anforderung |
| 0x18000000 | Signal ungueltig |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-enb-stg-act"></a>
### ENB_STG_ACT

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | Freigabe Nachziehen |
| 0x20000000 | Stellvorgang sperren |
| 0x40000000 | Stellvorgang erlauben |
| 0x60000000 | Signal ungueltig |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-apply-permission"></a>
### APPLY_PERMISSION

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | V &gt; V_Anziehen_erlaubt |
| 0x80000000 | V &lt; V_Anziehen_erlaubt |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-umweltbedingung-d-3"></a>
### UMWELTBEDINGUNG_D_3

Dimensions: 1 rows × 29 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR | UW17_NR | UW18_NR | UW19_NR | UW20_NR | UW21_NR | UW22_NR | UW23_NR | UW24_NR | UW25_NR | UW26_NR | UW27_NR | UW28_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 28 | 0xA5 | 0xA6 | 0xA7 | 0xA8 | 0xA9 | 0xAA | 0xAB | 0xAC | 0xAD | 0xAE | 0xAF | 0xB0 | 0xB1 | 0xB2 | 0xB3 | 0xB4 | 0xB5 | 0xB6 | 0xB7 | 0xB8 | 0xB9 | 0xBA | 0xBB | 0xBC | 0xBD | 0xBE | 0xBF | 0xC0 |

<a id="table-testcasemasterfailed"></a>
### TESTCASEMASTERFAILED

Dimensions: 12 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | alle Test ok |
| 0x00000001 | RAMTest |
| 0x00000002 | ROM Test Applikation |
| 0x00000003 | ROM Test Bootloader |
| 0x00000004 | Stack Test |
| 0x00000005 | Program Counter |
| 0x00000006 | Trap |
| 0x00000007 | Program Flow Monitoring |
| 0x00000008 | Instruction Test |
| 0x00000009 | Shutdown Label |
| 0x0000000A | OS Task Stack |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-testcaseslavefailed"></a>
### TESTCASESLAVEFAILED

Dimensions: 10 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | alle Test ok |
| 0x00000100 | RAMTest |
| 0x00000200 | ROM Test |
| 0x00000300 | unused |
| 0x00000400 | Stack Test |
| 0x00000500 | Program Counter |
| 0x00000600 | unused |
| 0x00000700 | Program Flow Monitoring |
| 0x00000800 | Instruction Test |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-slave-geschwindigkeit"></a>
### SLAVE_GESCHWINDIGKEIT

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | ok |
| 0x01000000 | alive checksum |
| 0x02000000 | signal |
| 0x03000000 | timeout |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-slave-stellanforderung"></a>
### SLAVE_STELLANFORDERUNG

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | ok |
| 0x04000000 | alive checksum |
| 0x08000000 | signal |
| 0x0C000000 | timeout |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-slave-getriebedaten"></a>
### SLAVE_GETRIEBEDATEN

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | ok |
| 0x10000000 | alive checksum |
| 0x20000000 | signal |
| 0x30000000 | timeout |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-slave-klemmenstatus"></a>
### SLAVE_KLEMMENSTATUS

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | ok |
| 0x40000000 | alive checksum |
| 0x80000000 | signal |
| 0xC0000000 | timeout |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-blocknumberdataerror"></a>
### BLOCKNUMBERDATAERROR

Dimensions: 36 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | 0 |
| 0x00010000 | 1 |
| 0x00020000 | 2 |
| 0x00030000 | 3 |
| 0x00040000 | 4 |
| 0x00050000 | 5 |
| 0x00060000 | 6 |
| 0x00070000 | 7 |
| 0x00080000 | 8 |
| 0x00090000 | 9 |
| 0x000A0000 | 10 |
| 0x000B0000 | 11 |
| 0x000C0000 | 12 |
| 0x000D0000 | 13 |
| 0x000E0000 | 14 |
| 0x000F0000 | 15 |
| 0x00100000 | 16 |
| 0x00110000 | 17 |
| 0x00120000 | 18 |
| 0x00130000 | 19 |
| 0x00140000 | 20 |
| 0x00150000 | 21 |
| 0x00160000 | 22 |
| 0x00170000 | 23 |
| 0x00180000 | 24 |
| 0x00190000 | 25 |
| 0x001A0000 | 26 |
| 0x001B0000 | 27 |
| 0x001C0000 | 28 |
| 0x001D0000 | 29 |
| 0x001E0000 | 30 |
| 0x001F0000 | 31 |
| 0x00200000 | 32 |
| 0x00210000 | 33 |
| 0x00220000 | 34 |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-blocknumbersofterror"></a>
### BLOCKNUMBERSOFTERROR

Dimensions: 36 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | 0 |
| 0x01000000 | 1 |
| 0x02000000 | 2 |
| 0x03000000 | 3 |
| 0x04000000 | 4 |
| 0x05000000 | 5 |
| 0x06000000 | 6 |
| 0x07000000 | 7 |
| 0x08000000 | 8 |
| 0x09000000 | 9 |
| 0x0A000000 | 10 |
| 0x0B000000 | 11 |
| 0x0C000000 | 12 |
| 0x0D000000 | 13 |
| 0x0E000000 | 14 |
| 0x0F000000 | 15 |
| 0x10000000 | 16 |
| 0x11000000 | 17 |
| 0x12000000 | 18 |
| 0x13000000 | 19 |
| 0x14000000 | 20 |
| 0x15000000 | 21 |
| 0x16000000 | 22 |
| 0x17000000 | 23 |
| 0x18000000 | 24 |
| 0x19000000 | 25 |
| 0x1A000000 | 26 |
| 0x1B000000 | 27 |
| 0x1C000000 | 28 |
| 0x1D000000 | 29 |
| 0x1E000000 | 30 |
| 0x1F000000 | 31 |
| 0x20000000 | 32 |
| 0x21000000 | 33 |
| 0x22000000 | 34 |
| 0xFFFFFFFF | unbekannter Fehler |

<a id="table-s1"></a>
### S1

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | open and no failure |
| 0x00000001 | closed and no failure |
| 0x00000002 | short circuit to GND or broken wire |
| 0x00000003 | short circuit to Ubat |

<a id="table-s2"></a>
### S2

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | open and no failure |
| 0x00000004 | closed and no failure |
| 0x00000008 | short circuit to GND |
| 0x0000000C | broken wire or short circuit to Ubat |

<a id="table-s3"></a>
### S3

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | open and no failure |
| 0x00000010 | closed and no failure |
| 0x00000020 | short circuit to GND |
| 0x00000030 | broken wire or short circuit to Ubat |

<a id="table-s4"></a>
### S4

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | open and no failure |
| 0x00000040 | closed and no failure |
| 0x00000080 | short circuit to GND |
| 0x000000C0 | broken wire or short circuit to Ubat |
