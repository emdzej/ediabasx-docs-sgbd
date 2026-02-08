# rdc_can.prg

- Jobs: [63](#jobs)
- Tables: [30](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Reifendruck Control (RDC)  |
| ORIGIN | BMW TI-431 Weber |
| REVISION | 1.002 |
| AUTHOR | Beru_Electronics_GmbH BEE Rapp, Vector_Informatik_GmbH PSF Meyer, ESG TI-430 T.Müller |
| COMMENT | RDC-SGBD fuer E65, E6x, E8x, E9x, E7x, RRxx, R55, R56, R60  |
| PACKAGE | 1.37 |
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
- [STATUS_MESSDATEN_BLOCK1_LESEN](#job-status-messdaten-block1-lesen) - Auslesen von Messdatenblock 1 KWP2000: $21   ReadDataByLocalIdentifier $10   Messdatenblock 1 lesen Modus  : Default
- [STATUS_MESSDATEN_BLOCK2_LESEN](#job-status-messdaten-block2-lesen) - Auslesen von Messdatenblock 2 KWP2000: $21   ReadDataByLocalIdentifier $11   Messdatenblock 2 lesen Modus  : Default
- [STATUS_MESSDATEN_BLOCK3_LESEN](#job-status-messdaten-block3-lesen) - Auslesen von Messdatenblock 3 KWP2000: $21   ReadDataByLocalIdentifier $12   Messdatenblock 3 lesen Modus  : Default
- [STATUS_MESSDATEN_BLOCK4_LESEN](#job-status-messdaten-block4-lesen) - Auslesen von Messdatenblock 4 KWP2000: $21   ReadDataByLocalIdentifier $13   Messdatenblock 4 lesen Modus  : Default
- [STATUS_MESSDATEN_BLOCK5_LESEN](#job-status-messdaten-block5-lesen) - Auslesen von Messdatenblock 5 KWP2000: $21   ReadDataByLocalIdentifier $14   Messdatenblock 5 lesen Modus  : Default
- [STATUS_IO_LESEN](#job-status-io-lesen) - Auslesen eines Messdaten-Blocks KWP2000: $21   ReadDataByLocalIdentifier $16   I/O-Status lesen Modus  : Default
- [STATUS_ASSEMBLY_NUMBER](#job-status-assembly-number) - Zusammenbaunummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $86 Assembly Number Modus  : Default
- [STATUS_HS_WARNUNGSZAEHLER_LESEN](#job-status-hs-warnungszaehler-lesen) - Auslesen der Warnungszaehler des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2300 Warnungszaehler Modus  : Default
- [STATUS_HS_WARNEREIGNIS1_LESEN](#job-status-hs-warnereignis1-lesen) - Auslesen eines Warneignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2310 Warnereignis 1 Modus  : Default
- [STATUS_HS_WARNEREIGNIS2_LESEN](#job-status-hs-warnereignis2-lesen) - Auslesen eines Warneignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2311 Warnereignis 2 Modus  : Default
- [STATUS_HS_KALIBRIEREREIGNIS1_LESEN](#job-status-hs-kalibrierereignis1-lesen) - Auslesen eines Kalibriereignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2320 Kalbrierereignis 1 Modus  : Default
- [STATUS_HS_KALIBRIEREREIGNIS2_LESEN](#job-status-hs-kalibrierereignis2-lesen) - Auslesen eines Kalibriereignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2321 Kalbrierereignis 2 Modus  : Default
- [STATUS_HS_INAKTIVEREIGNIS1_LESEN](#job-status-hs-inaktivereignis1-lesen) - Auslesen eines Inaktiveignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2330 Inaktiveignisses 1 Modus  : Default
- [STATUS_HS_INAKTIVEREIGNIS2_LESEN](#job-status-hs-inaktivereignis2-lesen) - Auslesen eines Inaktiveignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2331 Inaktiveignisses 2 Modus  : Default
- [STEUERN_RADELEKTRONIK_VORGEBEN](#job-steuern-radelektronik-vorgeben) - Radelektronik vorgeben KWP2000: $3B WriteDataByLocalIdentifier $20 Radelektronik vorgeben Modus  : Default
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern des Systemstatus KWP2000: $3B WriteDataByLocalIdentifier $21 Systemstatus Modus  : Default

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

<a id="job-status-messdaten-block1-lesen"></a>
### STATUS_MESSDATEN_BLOCK1_LESEN

Auslesen von Messdatenblock 1 KWP2000: $21   ReadDataByLocalIdentifier $10   Messdatenblock 1 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik-Identifier |
| STAT_EIGENRAEDER_BEKANNT | int | Alle Eigenraeder sind bekannt |
| STAT_RADPOS_ER_BEKANNT | int | Radpositionen aller Eigenraeder sind bekannt |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT | int | Alle Radpositionen sind ueberprueft und bestaetigt |
| STAT_DTC_INACTIVE | int | Aktiver Fehler mit Warnlampe im Fehlerspeicher vorhanden |
| STAT_KAL_ANFORDERUNG | int | Kalibrieranforderung steht an |
| STAT_LIN_ON | int | LIN aktiv |
| STAT_RAD_ZUORDNUNG_TIMEOUT | int | Radzuordnung konnte nicht abgeschlossen werden |
| STAT_RAD_POSITION | string | Radposition der ID |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzter Reifendruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | bar |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzter Reifentemperaturwert der ID Bereich: -40 bis 120 Grad C |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Grad C |
| STAT_SOLLDRUCK_WERT | real | Solldruck der ID Bereich: 0 bis 6,375 bar |
| STAT_SOLLDRUCK_EINH | string | bar |
| STAT_GUTEMPFAENGE | int | Anzahl gut empfangener Telegramme der ID |
| STAT_AUSBEUTE_WERT | int | Ausbeute der ID Bereich: 0 bis 100 |
| STAT_AUSBEUTE_EINH | string | Prozent |
| STAT_RSSI_PEGEL | int | RSSI-Pegel der ID Bereich: 0 bis 255 |
| STAT_RESTLEBENSDAUER_WERT | int | Restlebensdauer der ID Bereich: 0 bis 120 Monate |
| STAT_RESTLEBENSDAUER_EINH | string | Monate |
| STAT_RADELEKTRONIK_STATUS | int | Radelektronik-Status der ID |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdaten-block2-lesen"></a>
### STATUS_MESSDATEN_BLOCK2_LESEN

Auslesen von Messdatenblock 2 KWP2000: $21   ReadDataByLocalIdentifier $11   Messdatenblock 2 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik-Identifier |
| STAT_EIGENRAEDER_BEKANNT | int | Alle Eigenraeder sind bekannt |
| STAT_RADPOS_ER_BEKANNT | int | Radpositionen aller Eigenraeder sind bekannt |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT | int | Alle Radpositionen sind ueberprueft und bestaetigt |
| STAT_DTC_INACTIVE | int | Aktiver Fehler mit Warnlampe im Fehlerspeicher vorhanden |
| STAT_KAL_ANFORDERUNG | int | Kalibrieranforderung steht an |
| STAT_LIN_ON | int | LIN aktiv |
| STAT_RAD_ZUORDNUNG_TIMEOUT | int | Radzuordnung konnte nicht abgeschlossen werden |
| STAT_RAD_POSITION | string | Radposition der ID |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzter Reifendruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | bar |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzter Reifentemperaturwert der ID Bereich: -40 bis 120 Grad C |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Grad C |
| STAT_SOLLDRUCK_WERT | real | Solldruck der ID Bereich: 0 bis 6,375 bar |
| STAT_SOLLDRUCK_EINH | string | bar |
| STAT_GUTEMPFAENGE | int | Anzahl gut empfangener Telegramme der ID |
| STAT_AUSBEUTE_WERT | int | Ausbeute der ID Bereich: 0 bis 100 |
| STAT_AUSBEUTE_EINH | string | Prozent |
| STAT_RSSI_PEGEL | int | RSSI-Pegel der ID Bereich: 0 bis 255 |
| STAT_RESTLEBENSDAUER_WERT | int | Restlebensdauer der ID Bereich: 0 bis 120 Monate |
| STAT_RESTLEBENSDAUER_EINH | string | Monate |
| STAT_RADELEKTRONIK_STATUS | int | Radelektronik-Status der ID |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdaten-block3-lesen"></a>
### STATUS_MESSDATEN_BLOCK3_LESEN

Auslesen von Messdatenblock 3 KWP2000: $21   ReadDataByLocalIdentifier $12   Messdatenblock 3 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik-Identifier |
| STAT_EIGENRAEDER_BEKANNT | int | Alle Eigenraeder sind bekannt |
| STAT_RADPOS_ER_BEKANNT | int | Radpositionen aller Eigenraeder sind bekannt |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT | int | Alle Radpositionen sind ueberprueft und bestaetigt |
| STAT_DTC_INACTIVE | int | Aktiver Fehler mit Warnlampe im Fehlerspeicher vorhanden |
| STAT_KAL_ANFORDERUNG | int | Kalibrieranforderung steht an |
| STAT_LIN_ON | int | LIN aktiv |
| STAT_RAD_ZUORDNUNG_TIMEOUT | int | Radzuordnung konnte nicht abgeschlossen werden |
| STAT_RAD_POSITION | string | Radposition der ID |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzter Reifendruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | bar |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzter Reifentemperaturwert der ID Bereich: -40 bis 120 Grad C |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Grad C |
| STAT_SOLLDRUCK_WERT | real | Solldruck der ID Bereich: 0 bis 6,375 bar |
| STAT_SOLLDRUCK_EINH | string | bar |
| STAT_GUTEMPFAENGE | int | Anzahl gut empfangener Telegramme der ID |
| STAT_AUSBEUTE_WERT | int | Ausbeute der ID Bereich: 0 bis 100 |
| STAT_AUSBEUTE_EINH | string | Prozent |
| STAT_RSSI_PEGEL | int | RSSI-Pegel der ID Bereich: 0 bis 255 |
| STAT_RESTLEBENSDAUER_WERT | int | Restlebensdauer der ID Bereich: 0 bis 120 Monate |
| STAT_RESTLEBENSDAUER_EINH | string | Monate |
| STAT_RADELEKTRONIK_STATUS | int | Radelektronik-Status der ID |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdaten-block4-lesen"></a>
### STATUS_MESSDATEN_BLOCK4_LESEN

Auslesen von Messdatenblock 4 KWP2000: $21   ReadDataByLocalIdentifier $13   Messdatenblock 4 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik-Identifier |
| STAT_EIGENRAEDER_BEKANNT | int | Alle Eigenraeder sind bekannt |
| STAT_RADPOS_ER_BEKANNT | int | Radpositionen aller Eigenraeder sind bekannt |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT | int | Alle Radpositionen sind ueberprueft und bestaetigt |
| STAT_DTC_INACTIVE | int | Aktiver Fehler mit Warnlampe im Fehlerspeicher vorhanden |
| STAT_KAL_ANFORDERUNG | int | Kalibrieranforderung steht an |
| STAT_LIN_ON | int | LIN aktiv |
| STAT_RAD_ZUORDNUNG_TIMEOUT | int | Radzuordnung konnte nicht abgeschlossen werden |
| STAT_RAD_POSITION | string | Radposition der ID |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzter Reifendruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | bar |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzter Reifentemperaturwert der ID Bereich: -40 bis 120 Grad C |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Grad C |
| STAT_SOLLDRUCK_WERT | real | Solldruck der ID Bereich: 0 bis 6,375 bar |
| STAT_SOLLDRUCK_EINH | string | bar |
| STAT_GUTEMPFAENGE | int | Anzahl gut empfangener Telegramme der ID |
| STAT_AUSBEUTE_WERT | int | Ausbeute der ID Bereich: 0 bis 100 |
| STAT_AUSBEUTE_EINH | string | Prozent |
| STAT_RSSI_PEGEL | int | RSSI-Pegel der ID Bereich: 0 bis 255 |
| STAT_RESTLEBENSDAUER_WERT | int | Restlebensdauer der ID Bereich: 0 bis 120 Monate |
| STAT_RESTLEBENSDAUER_EINH | string | Monate |
| STAT_RADELEKTRONIK_STATUS | int | Radelektronik-Status der ID |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdaten-block5-lesen"></a>
### STATUS_MESSDATEN_BLOCK5_LESEN

Auslesen von Messdatenblock 5 KWP2000: $21   ReadDataByLocalIdentifier $14   Messdatenblock 5 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik-Identifier |
| STAT_EIGENRAEDER_BEKANNT | int | Alle Eigenraeder sind bekannt |
| STAT_RADPOS_ER_BEKANNT | int | Radpositionen aller Eigenraeder sind bekannt |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT | int | Alle Radpositionen sind ueberprueft und bestaetigt |
| STAT_DTC_INACTIVE | int | Aktiver Fehler mit Warnlampe im Fehlerspeicher vorhanden |
| STAT_KAL_ANFORDERUNG | int | Kalibrieranforderung steht an |
| STAT_LIN_ON | int | LIN aktiv |
| STAT_RAD_ZUORDNUNG_TIMEOUT | int | Radzuordnung konnte nicht abgeschlossen werden |
| STAT_RAD_POSITION | string | Radposition der ID |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzter Reifendruckwert der ID Bereich: 0 bis 6,375 bar |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | bar |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzter Reifentemperaturwert der ID Bereich: -40 bis 120 Grad C |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Grad C |
| STAT_SOLLDRUCK_WERT | real | Solldruck der ID Bereich: 0 bis 6,375 bar |
| STAT_SOLLDRUCK_EINH | string | bar |
| STAT_GUTEMPFAENGE | int | Anzahl gut empfangener Telegramme der ID |
| STAT_AUSBEUTE_WERT | int | Ausbeute der ID Bereich: 0 bis 100 |
| STAT_AUSBEUTE_EINH | string | Prozent |
| STAT_RSSI_PEGEL | int | RSSI-Pegel der ID Bereich: 0 bis 255 |
| STAT_RESTLEBENSDAUER_WERT | int | Restlebensdauer der ID Bereich: 0 bis 120 Monate |
| STAT_RESTLEBENSDAUER_EINH | string | Monate |
| STAT_RADELEKTRONIK_STATUS | int | Radelektronik-Status der ID |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Auslesen eines Messdaten-Blocks KWP2000: $21   ReadDataByLocalIdentifier $16   I/O-Status lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EIGENRAEDER_BEKANNT | int | Alle Eigenraeder sind bekannt |
| STAT_RADPOS_ER_BEKANNT | int | Radpositionen aller Eigenraeder sind bekannt |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT | int | Alle Radpositionen sind ueberprueft und bestaetigt |
| STAT_DTC_INACTIVE | int | Aktiver Fehler mit Warnlampe im Fehlerspeicher vorhanden |
| STAT_KAL_ANFORDERUNG | int | Kalibrieranforderung steht an |
| STAT_LIN_ON | int | LIN aktiv |
| STAT_RAD_ZUORDNUNG_TIMEOUT | int | Radzuordnung konnte nicht abgeschlossen werden |
| STAT_BANDMODE | int | RDC ist im Bandmode |
| STAT_ER_ERKENNUNG_STAND | int | Eigenraderkennung im Stand wurde gestartet |
| STAT_ER_ERKENNUNG_FAHRT | int | Eigenraderkennung waehrend der Fahrt wurde gestartet |
| STAT_TEST_EIGENRAD | int | Test-Eigenraderkennung waehrend der Fahrt wurde gestartet |
| STAT_BUS_DIAGNOSE | int | LIN Bus Diagnose wurde gestartet |
| STAT_ER_FAHRT_VTHRS | int | Geschwindigkeitsschwelle fuer Eigenraderkennung bei Fahrt aktiviert |
| STAT_BM_TIMEOUT_ACTIVE | int | Bandmode Timeout laeuft |
| STAT_TEST_ER_STAND | int | Test-Eigenraderkennung im Stand wurde gestartet |
| STAT_HARTE_WARNUNG_UNSPEZIFISCH | int | Harte Warnung unspezifisch |
| STAT_HARTE_WARNUNG_VL | int | Harte Warnung VL |
| STAT_HARTE_WARNUNG_VR | int | Harte Warnung VR |
| STAT_HARTE_WARNUNG_HL | int | Harte Warnung HL |
| STAT_HARTE_WARNUNG_HR | int | Harte Warnung HR |
| STAT_KL_R_EIN | int | Klemme R |
| STAT_MOTOR_LAEUFT_EIN | int | Motor dreht |
| STAT_FZG_FAEHRT | int | Fahrzeug faehrt |
| STAT_ER_ALLE_TEL_RE | int | Alle Radelektroniken erkannt |
| STAT_ER_ZUVIELE_RE | int | Zu viele Radelektroniken erkannt |
| STAT_STOERSENDER_SCI | int | Funkstoerung vorhanden |
| STAT_STOERSENDER_FF_SCI | int | Funkstoerung hat zu mehrfachen Telegrammausfaellen gefuehrt |
| STAT_STOERSENDER_ZEIT_SCI | int | Funkstoerung ist laenger als die erlaubte Totzeit vorhanden |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-assembly-number"></a>
### STATUS_ASSEMBLY_NUMBER

Zusammenbaunummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $86 Assembly Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AN_NR | string | Zusammenbaunummer 7-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-warnungszaehler-lesen"></a>
### STATUS_HS_WARNUNGSZAEHLER_LESEN

Auslesen der Warnungszaehler des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2300 Warnungszaehler Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZAEHLER_HARTE_WARNUNG_VL | int | Zaehler der harten Warnungen vorne links |
| STAT_ZAEHLER_HARTE_WARNUNG_VR | int | Zaehler der harten Warnungen vorne rechts |
| STAT_ZAEHLER_HARTE_WARNUNG_HL | int | Zaehler der harten Warnungen hinten links |
| STAT_ZAEHLER_HARTE_WARNUNG_HR | int | Zaehler der harten Warnungen hinten rechts |
| STAT_ZAEHLER_HARTE_WARNUNG_XX | int | Zaehler der harten Warnungen waehrend ER Verlust |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-warnereignis1-lesen"></a>
### STATUS_HS_WARNEREIGNIS1_LESEN

Auslesen eines Warneignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2310 Warnereignis 1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| STAT_RE_IDENTIFIER_RE0 | unsigned long | Radelektronik-Identifier der RE0 |
| STAT_REIFENDRUCKWERT_RE0_WERT | real | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE0_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE0_WERT | char | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE0 | int | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | string | Radposition der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | real | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE0_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE1 | unsigned long | Radelektronik-Identifier der RE1 |
| STAT_REIFENDRUCKWERT_RE1_WERT | real | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE1_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE1_WERT | char | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE1 | int | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | string | Radposition der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | real | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE1_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE2 | unsigned long | Radelektronik-Identifier der RE2 |
| STAT_REIFENDRUCKWERT_RE2_WERT | real | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE2_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE2_WERT | char | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE2 | int | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | string | Radposition der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | real | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE2_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE3 | unsigned long | Radelektronik-Identifier der RE3 |
| STAT_REIFENDRUCKWERT_RE3_WERT | real | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE3_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE3_WERT | char | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE3 | int | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | string | Radposition der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | real | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE3_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-warnereignis2-lesen"></a>
### STATUS_HS_WARNEREIGNIS2_LESEN

Auslesen eines Warneignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2311 Warnereignis 2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| STAT_RE_IDENTIFIER_RE0 | unsigned long | Radelektronik-Identifier der RE0 |
| STAT_REIFENDRUCKWERT_RE0_WERT | real | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE0_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE0_WERT | char | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE0 | int | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | string | Radposition der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | real | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE0_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE1 | unsigned long | Radelektronik-Identifier der RE1 |
| STAT_REIFENDRUCKWERT_RE1_WERT | real | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE1_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE1_WERT | char | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE1 | int | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | string | Radposition der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | real | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE1_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE2 | unsigned long | Radelektronik-Identifier der RE2 |
| STAT_REIFENDRUCKWERT_RE2_WERT | real | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE2_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE2_WERT | char | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE2 | int | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | string | Radposition der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | real | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE2_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE3 | unsigned long | Radelektronik-Identifier der RE3 |
| STAT_REIFENDRUCKWERT_RE3_WERT | real | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE3_EINH | string | bar |
| STAT_REIFENTEMPERATURWERT_RE3_WERT | char | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RADELEKTRONIK_STATUS_RE3 | int | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | string | Radposition der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | real | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE3_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-kalibrierereignis1-lesen"></a>
### STATUS_HS_KALIBRIEREREIGNIS1_LESEN

Auslesen eines Kalibriereignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2320 Kalbrierereignis 1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| STAT_RE_IDENTIFIER_RE0 | unsigned long | Radelektronik-Identifier der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0 | int | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | string | Radposition der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | real | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE0_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE1 | unsigned long | Radelektronik-Identifier der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1 | int | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | string | Radposition der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | real | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE1_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE2 | unsigned long | Radelektronik-Identifier der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2 | int | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | string | Radposition der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | real | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE2_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE3 | unsigned long | Radelektronik-Identifier der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3 | int | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | string | Radposition der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | real | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE3_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-kalibrierereignis2-lesen"></a>
### STATUS_HS_KALIBRIEREREIGNIS2_LESEN

Auslesen eines Kalibriereignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2321 Kalbrierereignis 2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| STAT_RE_IDENTIFIER_RE0 | unsigned long | Radelektronik-Identifier der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0 | int | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | string | Radposition der RE0 |
| STAT_SOLLDRUCKWERT_RE0_WERT | real | Solldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE0_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Solldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE0_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE0 | unsigned int | RE0 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE1 | unsigned long | Radelektronik-Identifier der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1 | int | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | string | Radposition der RE1 |
| STAT_SOLLDRUCKWERT_RE1_WERT | real | Solldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE1_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Solldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE1_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE1 | unsigned int | RE1 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE2 | unsigned long | Radelektronik-Identifier der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2 | int | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | string | Radposition der RE2 |
| STAT_SOLLDRUCKWERT_RE2_WERT | real | Solldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE2_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Solldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE2_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE2 | unsigned int | RE2 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| STAT_RE_IDENTIFIER_RE3 | unsigned long | Radelektronik-Identifier der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3 | int | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | string | Radposition der RE3 |
| STAT_SOLLDRUCKWERT_RE3_WERT | real | Solldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_SOLLDRUCKWERT_RE3_EINH | string | bar |
| STAT_SOLLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Solldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_SOLLTEMPERATURWERT_RE3_EINH | string | Grad C |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Monate |
| STAT_CNTR_POWER_MNGMT_HTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer gleich 10°C Bereich: 0 bis 4096 Telegramme |
| STAT_CNTR_POWER_MNGMT_LTEMP_RE3 | unsigned int | RE3 - Zähler Powermanagement größer kleiner gleich 9°C Bereich: 0 bis 4096 Telegramme |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-inaktivereignis1-lesen"></a>
### STATUS_HS_INAKTIVEREIGNIS1_LESEN

Auslesen eines Inaktiveignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2330 Inaktiveignisses 1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_HF_UEBERDECKUNG | unsigned char | HF Ueberdeckung |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_INTERNER_FEHLERCODE | int | SG-interner Fehlercode |
| STAT_FEHLERCODE | int | Fehlercode BMW |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-inaktivereignis2-lesen"></a>
### STATUS_HS_INAKTIVEREIGNIS2_LESEN

Auslesen eines Inaktiveignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2331 Inaktiveignisses 2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KILOMETERSTAND | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) |
| STAT_DATUM_EINH | string | JJ.MM.TT |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_HF_UEBERDECKUNG | unsigned char | HF Ueberdeckung |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_INTERNER_FEHLERCODE | int | SG-interner Fehlercode |
| STAT_FEHLERCODE | int | Fehlercode BMW |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-radelektronik-vorgeben"></a>
### STEUERN_RADELEKTRONIK_VORGEBEN

Radelektronik vorgeben KWP2000: $3B WriteDataByLocalIdentifier $20 Radelektronik vorgeben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RE_ID | unsigned long | Radelektronik-Identifier (10-stellig) |
| RE_POS | int | Radelektronik-Position 0: vorne links,  1: vorne rechts 2: hinten links, 3: hinten rechts 4: Reserverad 5, 6, 7, 8, 9 Radposition nicht bekannt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern des Systemstatus KWP2000: $3B WriteDataByLocalIdentifier $21 Systemstatus Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SET_BANDMODE | unsigned char | 0: Bandmode unveraendert 1: Bandmode setzen |
| RESET_BANDMODE | unsigned char | 0: Bandmode unveraendert 1: Bandmode ruecksetzen |
| SET_ER_FAHRT | unsigned char | 0: Eigenraderkennung bei Fahrt unveraendert 1: Eigenraderkennung bei Fahrt setzen |
| RESET_ER_FAHRT | unsigned char | 0: Eigenraderkennung bei Fahrt unveraendert 1: Eigenraderkennung bei Fahrt ruecksetzen |
| SET_ER_STAND | unsigned char | 0: Eigenraderkennung im Stand unveraendert 1: Eigenraderkennung im Stand setzen |
| RESET_ER_STAND | unsigned char | 0: Eigenraderkennung im Stand unveraendert 1: Eigenraderkennung im Stand ruecksetzen |
| SET_CAL_REQUEST | unsigned char | 0: Kalibrieranforderung unveraendert 1: Kalibrieranforderung setzen |
| RESET_CAL_REQUEST | unsigned char | 0: Kalibrieranforderung unveraendert 1: Kalibrieranforderung ruecksetzen |
| SET_TEST_ER_FAHRT | unsigned char | 0: Empfang der Eigenraeder waehrend der Fahrt pruefen unveraendert 1: Empfang der Eigenraeder waehrend der Fahrt pruefen setzen |
| RESET_TEST_ER_FAHRT | unsigned char | 0: Empfang der Eigenraeder waehrend der Fahrt pruefen unveraendert 1: Empfang der Eigenraeder waehrend der Fahrt pruefen ruecksetzen |
| SET_RDCBUS_DIAG | unsigned char | 0: Stromdiagnose LIN-Teilnehmer unveraendert 1: Stromdiagnose LIN-Teilnehmer setzen |
| RESET_RDCBUS_DIAG | unsigned char | 0: Stromdiagnose LIN-Teilnehmer unveraendert 1: Stromdiagnose LIN-Teilnehmer ruecksetzen |
| SET_SOLLDRUCK_UEBERNEHMEN | unsigned char | 0: Solldruck unveraendert 1: Solldruckuebernahme setzen |
| RESET_SOLLDRUCK_UEBERNEHMEN | unsigned char | 0: Solldruck unveraendert 1: Solldruckuebernahme ruecksetzen |
| SET_TEST_ER_STAND | unsigned char | 0: Empfang der Eigenraeder im Stand pruefen unveraendert 1: Empfang der Eigenraeder im Stand pruefen setzen |
| RESET_TEST_ER_STAND | unsigned char | 0: Empfang der Eigenraeder im Stand pruefen unveraendert 1: Empfang der Eigenraeder im Stand pruefen ruecksetzen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (106 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (17 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (63 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (4 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (7 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (2 × 9)
- [IARTTEXTEERWEITERT](#table-iarttexteerweitert) (1 × 3)
- [RDCSTATUS](#table-rdcstatus) (7 × 4)
- [REPOSITION](#table-reposition) (5 × 2)
- [WARNUNG](#table-warnung) (5 × 4)
- [SGZUSTAND](#table-sgzustand) (5 × 4)
- [KONFIGSTATUS](#table-konfigstatus) (3 × 4)
- [BANDMODE](#table-bandmode) (8 × 4)

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

Dimensions: 106 rows × 2 columns

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
| 2 | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 17 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x604C | Bandmode aktiv |
| 0x604D | Fehler Steuergeraet |
| 0x604E | Fehler RDC-System |
| 0x604F | Fehler Uebertragungskanal VL |
| 0x6050 | Fehler Uebertragungskanal VR |
| 0x6051 | Fehler Uebertragungskanal HL |
| 0x6052 | Fehler Uebertragungskanal HR |
| 0x6053 | Fehler Uebertragungskanal Ant |
| 0x6054 | Fehler Radsensor VL |
| 0x6055 | Fehler Radsensor VR |
| 0x6056 | Fehler Radsensor HL |
| 0x6057 | Fehler Radsensor HR |
| 0x6059 | Fehler Radsensor undefiniert |
| 0xD104 | Fehler CAN Eindrahtbetrieb |
| 0xD107 | Fehler CAN Bus Off |
| 0xD13E | Fehler CAN Telegramm Timeout beim Empfang |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 11111111 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 63 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| 00000000 | 000 | Betriebsspannung AD-Wandler defekt |
| 00000010 | 002 | Schutzschaltung aktiv: Ueberspannung Antennen |
| 00000011 | 003 | Lernvorgang bei externer HF-Stoerung nicht moeglich |
| 00000100 | 004 | Eigenradstatus nicht erreicht |
| 00000111 | 007 | Hardwaredefekt: Speichercheck RAM |
| 00001001 | 009 | Hardwaredefekt: R/W-Check EEPROM |
| 00001011 | 011 | Hardwaredefekt: Speichercheck ROM |
| 00001101 | 013 | Hardwaredefekt: EEPROM-Fehler Kategorie A |
| 00001111 | 015 | Hardwaredefekt: EEPROM-Fehler Kategorie E |
| 00011111 | 031 | CAN Controller Bus Off |
| 00100001 | 033 | CAN Bus Keine Daten 4 |
| 00100010 | 034 | CAN Leitung Low/High defekt (ERRORpin) |
| 00101010 | 042 | Unterspannung Kl.30 |
| 00101011 | 043 | Ueberspannung Kl.30 |
| 00101101 | 045 | RE VL defekt: Sensorfehler |
| 00101110 | 046 | RE VL defekt: Kein Empfang |
| 00110000 | 048 | RE VR defekt: Sensorfehler |
| 00110001 | 049 | RE VR defekt: Kein Empfang |
| 00110011 | 051 | RE HL defekt: Sensorfehler |
| 00110100 | 052 | RE HL defekt: Kein Empfang |
| 00110110 | 054 | RE HR defekt: Sensorfehler |
| 00110111 | 055 | RE HR defekt: Kein Empfang |
| 00111100 | 060 | RE defekt: Sensorfehler |
| 00111101 | 061 | RE defekt: Kein Empfang |
| 01100101 | 101 | Externe HF-Stoerung |
| 01110011 | 115 | Kalibrierungszuordnung nicht moeglich |
| 01111100 | 124 | Bandmode aktiviert |
| 10000000 | 128 | Strom-Diagnose Kanal VL |
| 10000001 | 129 | Kurzschluß auf Kanal VL |
| 10000010 | 130 | TSS-Bus VL: Verbindungsaufbau gescheitert |
| 10000011 | 131 | Strom-Diagnose Kanal VR |
| 10000100 | 132 | Kurzschluß auf Kanal VR |
| 10000101 | 133 | TSS-Bus VR: Verbindungsaufbau gescheitert |
| 10000110 | 134 | Strom-Diagnose Kanal HL |
| 10000111 | 135 | Kurzschluß auf Kanal HL |
| 10001000 | 136 | TSS-Bus HL: Verbindungsaufbau gescheitert |
| 10001001 | 137 | Strom-Diagnose Kanal HR |
| 10001010 | 138 | Kurzschluß auf Kanal HR |
| 10001011 | 139 | TSS-Bus HR: Verbindungsaufbau gescheitert |
| 10001100 | 140 | Strom-Diagnose Kanal Ant |
| 10001101 | 141 | Kurzschluß auf Kanal Ant |
| 10001110 | 142 | TSS-Bus Ant: Verbindungsaufbau gescheitert |
| 10001111 | 143 | Trigger VL defekt: RAM-Fehler |
| 10010000 | 144 | Trigger VL defekt: ROM-Fehler |
| 10010011 | 147 | Trigger VL defekt: LF-Triggerspule |
| 10010101 | 149 | Trigger VR defekt: RAM-Fehler |
| 10010110 | 150 | Trigger VR defekt: ROM-Fehler |
| 10011001 | 153 | Trigger VR defekt: LF-Triggerspule |
| 10011011 | 155 | Trigger HL defekt: RAM-Fehler |
| 10011100 | 156 | Trigger HL defekt: ROM-Fehler |
| 10011111 | 159 | Trigger HL defekt: LF-Triggerspule |
| 10100001 | 161 | Trigger HR defekt: RAM-Fehler |
| 10100010 | 162 | Trigger HR defekt: ROM-Fehler |
| 10100101 | 165 | Trigger HR defekt: LF-Triggerspule |
| 10100111 | 167 | Digitalantenne defekt: RAM-Fehler |
| 10101000 | 168 | Digitalantenne defekt: ROM-Fehler |
| 10101101 | 173 | Kanal VL: falsche Komponente |
| 10101110 | 174 | Kanal VR: falsche Komponente |
| 10101111 | 175 | Kanal HL: falsche Komponente |
| 10110000 | 176 | Kanal HR: falsche Komponente |
| 10110001 | 177 | Kanal Digitalantenne: falsche Komponente |
| 11110000 | 240 | CRC HF-Telegramm n.i.O. (inkompatible Digitalantenne) |
| xxxxxxxx | 255 | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 4 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xD104 | 0x04 | 0x03 | - | - |
| 0xD107 | 0x04 | 0x03 | - | - |
| 0xD13E | 0x04 | 0x03 | - | - |
| default | 0x02 | 0x03 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Kilometerstand | km | high | unsigned int | - | 8 | 1 | 0 |
| 0x02 | Geschwindigkeit | km/h | high | unsigned int | - | 1 | 10 | 0 |
| 0x03 | Temperatur | Grad C | - | unsigned char | - | 1 | 2 | -40 |
| 0x04 | EmpfangsId | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x05 | SendeId | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0xFF | ohne Bedeutung | 1 | high | unsigned int | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

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

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 11111111 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x02 | 0x03 | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 2 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xFF | ohne Bedeutung | 1 | high | unsigned int | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iarttexteerweitert"></a>
### IARTTEXTEERWEITERT

Dimensions: 1 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxxx | 255 | -- |

<a id="table-rdcstatus"></a>
### RDCSTATUS

Dimensions: 7 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| STAT_EIGENRAEDER_BEKANNT | 0 | 0x80 | 0x80 |
| STAT_RADPOS_ER_BEKANNT | 0 | 0x40 | 0x40 |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT | 0 | 0x20 | 0x20 |
| STAT_DTC_INACTIVE | 0 | 0x10 | 0x10 |
| STAT_KAL_ANFORDERUNG | 0 | 0x08 | 0x08 |
| STAT_LIN_ON | 0 | 0x04 | 0x04 |
| STAT_RAD_ZUORDNUNG_TIMEOUT | 0 | 0x02 | 0x02 |

<a id="table-reposition"></a>
### REPOSITION

Dimensions: 5 rows × 2 columns

| NAME | WERT |
| --- | --- |
| VL | 0x00 |
| VR | 0x01 |
| HL | 0x02 |
| HR | 0x03 |
| RR | 0x04 |

<a id="table-warnung"></a>
### WARNUNG

Dimensions: 5 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| W_UNDEF | 0 | 0x80 | 0x80 |
| W_VL | 0 | 0x40 | 0x40 |
| W_VR | 0 | 0x20 | 0x20 |
| W_HL | 0 | 0x10 | 0x10 |
| W_HR | 0 | 0x08 | 0x08 |

<a id="table-sgzustand"></a>
### SGZUSTAND

Dimensions: 5 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| STAT_KL_R | 0 | 0x80 | 0x80 |
| STAT_MOTOR_LAEUFT | 0 | 0x40 | 0x40 |
| STAT_FZG_FAEHRT | 0 | 0x20 | 0x20 |
| STAT_ER_ALLE_TEL_RE | 0 | 0x10 | 0x10 |
| STAT_ER_ZUVIELE_RE | 0 | 0x08 | 0x08 |

<a id="table-konfigstatus"></a>
### KONFIGSTATUS

Dimensions: 3 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| STAT_STOERSENDER_SCI | 0 | 0x80 | 0x80 |
| STAT_STOERSENDER_FF_SCI | 0 | 0x40 | 0x40 |
| STAT_STOERSENDER_ZEIT_SCI | 0 | 0x20 | 0x20 |

<a id="table-bandmode"></a>
### BANDMODE

Dimensions: 8 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| STAT_BANDMODE | 0 | 0x80 | 0x80 |
| STAT_ER_ERKENNUNG_STAND | 0 | 0x40 | 0x40 |
| STAT_ER_ERKENNUNG_FAHRT | 0 | 0x20 | 0x20 |
| STAT_TEST_EIGENRAD | 0 | 0x10 | 0x10 |
| STAT_BUS_DIAGNOSE | 0 | 0x08 | 0x08 |
| STAT_ER_FAHRT_VTHRS | 0 | 0x04 | 0x04 |
| STAT_BM_TIMEOUT_ACTIVE | 0 | 0x02 | 0x02 |
| STAT_TEST_ER_STAND | 0 | 0x01 | 0x01 |
