# rdckwp.prg

- Jobs: [72](#jobs)
- Tables: [39](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Reifen Druck Control Low Cost BN2000 |
| ORIGIN | BMW EF-442 Julian_Strang |
| REVISION | 2.001 |
| AUTHOR | Vector_Informatik_GmbH PES Heiko_Meyer, Huf_Electronics_Bretten |
| COMMENT | Reifen-Druck-Kontrolle LowCost |
| PACKAGE | 1.64 |
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
- [STATUS_ASSEMBLY_NUMBER](#job-status-assembly-number) - Zusammenbaunummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $86 Assembly Number Modus  : Default
- [STATUS_HS_INAKTIVEREIGNIS1_LESEN](#job-status-hs-inaktivereignis1-lesen) - Auslesen eines Inaktiveignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2330 Inaktiveignisses 1 Modus  : Default
- [STATUS_HS_INAKTIVEREIGNIS2_LESEN](#job-status-hs-inaktivereignis2-lesen) - Auslesen eines Inaktiveignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2331 Inaktiveignisses 2 Modus  : Default
- [STATUS_HS_INAKTIVEREIGNIS3_LESEN](#job-status-hs-inaktivereignis3-lesen) - Auslesen eines Inaktiveignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2332 Inaktiveignisses 3 Modus  : Default
- [STATUS_HS_KALIBRIEREREIGNIS1_LESEN](#job-status-hs-kalibrierereignis1-lesen) - Auslesen eines Kalibriereignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2320 Kalbrierereignis 1 Modus  : Default
- [STATUS_HS_KALIBRIEREREIGNIS2_LESEN](#job-status-hs-kalibrierereignis2-lesen) - Auslesen eines Kalibriereignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2321 Kalbrierereignis 2 Modus  : Default
- [STATUS_HS_KALIBRIEREREIGNIS3_LESEN](#job-status-hs-kalibrierereignis3-lesen) - Auslesen eines Kalibriereignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2322 Kalbrierereignis 3 Modus  : Default
- [STATUS_HS_WARNEREIGNIS1_LESEN](#job-status-hs-warnereignis1-lesen) - Auslesen eines Warneignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2310 Warnereignis 1 Modus  : Default
- [STATUS_HS_WARNEREIGNIS2_LESEN](#job-status-hs-warnereignis2-lesen) - Auslesen eines Warneignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2311 Warnereignis 2 Modus  : Default
- [STATUS_HS_WARNEREIGNIS3_LESEN](#job-status-hs-warnereignis3-lesen) - Auslesen eines Warneignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2312 Warnereignis 3 Modus  : Default
- [STATUS_HS_WARNEREIGNIS_RUECKNAHME](#job-status-hs-warnereignis-ruecknahme) - Auslesen der Warnungsruecknahme aus dem Historienspeicher KWP2000: $22   ReadDataByCommonIdentifier $2340 Warnungsruecknahme Modus  : Default
- [STATUS_HS_WARNUNGSZAEHLER_LESEN](#job-status-hs-warnungszaehler-lesen) - Auslesen der Warnungszaehler des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2300 Warnungszaehler Modus  : Default
- [STATUS_HS_WARN_RUECKNAHME_ZAEHLER_LESEN](#job-status-hs-warn-ruecknahme-zaehler-lesen) - Auslesen der Zaehler fuer Warnungsruecknahmen durch Luftnachfuellen oder Radtausch KWP2000: $22   ReadDataByCommonIdentifier $2303 Warnungsruecknahmezaehler Modus  : Default
- [STATUS_HS_ZAEHLER_WEICHE_WARNUNG_LESEN](#job-status-hs-zaehler-weiche-warnung-lesen) - Auslesen der Vorwarnzaehler des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2301 Warnungszaehler Modus  : Default
- [STATUS_MESSDATENBLOCK_GEN3_1](#job-status-messdatenblock-gen3-1) - Auslesen von Messdatenblock 1 KWP2000: $21   ReadDataByLocalIdentifier $30   Messdatenblock 1 lesen Modus  : Default
- [STATUS_MESSDATENBLOCK_GEN3_2](#job-status-messdatenblock-gen3-2) - Auslesen von Messdatenblock 2 KWP2000: $21   ReadDataByLocalIdentifier $31   Messdatenblock 2 lesen Modus  : Default
- [STATUS_MESSDATENBLOCK_GEN3_3](#job-status-messdatenblock-gen3-3) - Auslesen von Messdatenblock 3 KWP2000: $21   ReadDataByLocalIdentifier $32   Messdatenblock 3 lesen Modus  : Default
- [STATUS_MESSDATENBLOCK_GEN3_4](#job-status-messdatenblock-gen3-4) - Auslesen von Messdatenblock 4 KWP2000: $21   ReadDataByLocalIdentifier $33   Messdatenblock 4 lesen Modus  : Default
- [STATUS_RDC_GEN3_LESEN](#job-status-rdc-gen3-lesen) - Auslesen Statusinformation KWP2000: $21   ReadDataByLocalIdentifier $36   I/O-Status lesen Modus  : Default
- [STATUS_RE_LESEN_DRUCKCODIERUNG](#job-status-re-lesen-druckcodierung) - Listet alle RE im schnellen Sendemode mit Druckwert über 1,5 bar absolut KWP2000: $21   ReadDataByLocalIdentifier $37   Status_RE_Lesen_Druckcodierung Modus  : Default
- [STEUERN_DIGITAL_RDC](#job-steuern-digital-rdc) - Ansteuern des Systemstatus KWP2000: $3B WriteDataByLocalIdentifier $21 Systemstatus Modus  : Default
- [STEUERN_RADELEKTRONIK_VORGEBEN](#job-steuern-radelektronik-vorgeben) - Radelektronik vorgeben KWP2000: $3B WriteDataByLocalIdentifier $20 Radelektronik vorgeben Modus  : Default
- [STEUERN_SOLLDRUCK_VORGEBEN](#job-steuern-solldruck-vorgeben) - Solldruck vorgeben KWP2000: $3B WriteDataByLocalIdentifier $22 Solldruck vorgeben Modus  : Default
- [STATUS_MESSDATENBLOCK_AK_1](#job-status-messdatenblock-ak-1) - Auslesen von Messdatenblock 1 (Erweiterung AK) KWP2000: $21   ReadDataByLocalIdentifier $38   Messdatenblock 1 (Erweiterung AK) lesen Modus  : Default
- [STATUS_MESSDATENBLOCK_AK_2](#job-status-messdatenblock-ak-2) - Auslesen von Messdatenblock 2 (Erweiterung AK) KWP2000: $21   ReadDataByLocalIdentifier $39   Messdatenblock 2 (Erweiterung AK) lesen Modus  : Default
- [STATUS_MESSDATENBLOCK_AK_3](#job-status-messdatenblock-ak-3) - Auslesen von Messdatenblock 3 (Erweiterung AK) KWP2000: $21   ReadDataByLocalIdentifier $3A   Messdatenblock 3 (Erweiterung AK) lesen Modus  : Default
- [STATUS_MESSDATENBLOCK_AK_4](#job-status-messdatenblock-ak-4) - Auslesen von Messdatenblock 4 (Erweiterung AK) KWP2000: $21   ReadDataByLocalIdentifier $3B   Messdatenblock 4 (Erweiterung AK) lesen Modus  : Default
- [STATUS_CODIERDATEN_LESEN](#job-status-codierdaten-lesen) - Auslesen der vorhandenen Codierdaten KWP2000: $21   ReadDataByLocalIdentifier $35   Messdatenblock 1 (Erweiterung AK) lesen Modus  : Default

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

<a id="job-status-hs-inaktivereignis1-lesen"></a>
### STATUS_HS_INAKTIVEREIGNIS1_LESEN

Auslesen eines Inaktiveignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2330 Inaktiveignisses 1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_DATUM_EINH | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_EINH | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_WARNSTATUS1_TEXT | string | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_BETRIEBSZUSTAND_TEXT | string | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_FAHRZEUGZUSTAND_TEXT | string | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_ZUSTANDSKENNUNG_TEXT | string | Zustandskennung |
| STAT_INTERNER_FEHLERCODE | unsigned int | SG-interner Fehlercode |
| STAT_INTERNER_FEHLERCODE_TEXT | string | SG-interner Fehlercode |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-inaktivereignis2-lesen"></a>
### STATUS_HS_INAKTIVEREIGNIS2_LESEN

Auslesen eines Inaktiveignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2331 Inaktiveignisses 2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_DATUM_EINH | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_EINH | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_WARNSTATUS1_TEXT | string | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_BETRIEBSZUSTAND_TEXT | string | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_FAHRZEUGZUSTAND_TEXT | string | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_ZUSTANDSKENNUNG_TEXT | string | Zustandskennung |
| STAT_INTERNER_FEHLERCODE | unsigned int | SG-interner Fehlercode |
| STAT_INTERNER_FEHLERCODE_TEXT | string | SG-interner Fehlercode |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-inaktivereignis3-lesen"></a>
### STATUS_HS_INAKTIVEREIGNIS3_LESEN

Auslesen eines Inaktiveignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2332 Inaktiveignisses 3 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_DATUM_EINH | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_EINH | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_WARNSTATUS1_TEXT | string | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_BETRIEBSZUSTAND_TEXT | string | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_FAHRZEUGZUSTAND_TEXT | string | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_ZUSTANDSKENNUNG_TEXT | string | Zustandskennung |
| STAT_INTERNER_FEHLERCODE | unsigned int | SG-interner Fehlercode |
| STAT_INTERNER_FEHLERCODE_TEXT | string | SG-interner Fehlercode |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-kalibrierereignis1-lesen"></a>
### STATUS_HS_KALIBRIEREREIGNIS1_LESEN

Auslesen eines Kalibriereignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2320 Kalbrierereignis 1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_DATUM_EINH | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_EINH | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_WARNSTATUS1_TEXT | string | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_BETRIEBSZUSTAND_TEXT | string | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_FAHRZEUGZUSTAND_TEXT | string | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_ZUSTANDSKENNUNG_TEXT | string | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | unsigned long | Radelektronik-Identifier der RE0 |
| STAT_RE_IDENTIFIER_RE0_TEXT | string | Radelektronik-Identifier der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0 | unsigned char | Radelektronik-Status der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0_TEXT | string | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | string | Radposition der RE0 |
| STAT_BEFUELLDRUCKWERT_RE0_WERT | real | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE0_EINH | string | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | unsigned long | Radelektronik-Identifier der RE1 |
| STAT_RE_IDENTIFIER_RE1_TEXT | string | Radelektronik-Identifier der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1 | unsigned char | Radelektronik-Status der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1_TEXT | string | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | string | Radposition der RE1 |
| STAT_BEFUELLDRUCKWERT_RE1_WERT | real | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE1_EINH | string | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | unsigned long | Radelektronik-Identifier der RE2 |
| STAT_RE_IDENTIFIER_RE2_TEXT | string | Radelektronik-Identifier der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2 | unsigned char | Radelektronik-Status der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2_TEXT | string | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | string | Radposition der RE2 |
| STAT_BEFUELLDRUCKWERT_RE2_WERT | real | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE2_EINH | string | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | unsigned long | Radelektronik-Identifier der RE3 |
| STAT_RE_IDENTIFIER_RE3_TEXT | string | Radelektronik-Identifier der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3 | unsigned char | Radelektronik-Status der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3_TEXT | string | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | string | Radposition der RE3 |
| STAT_BEFUELLDRUCKWERT_RE3_WERT | real | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE3_EINH | string | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-kalibrierereignis2-lesen"></a>
### STATUS_HS_KALIBRIEREREIGNIS2_LESEN

Auslesen eines Kalibriereignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2321 Kalbrierereignis 2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_DATUM_EINH | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_EINH | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_WARNSTATUS1_TEXT | string | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_BETRIEBSZUSTAND_TEXT | string | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_FAHRZEUGZUSTAND_TEXT | string | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_ZUSTANDSKENNUNG_TEXT | string | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | unsigned long | Radelektronik-Identifier der RE0 |
| STAT_RE_IDENTIFIER_RE0_TEXT | string | Radelektronik-Identifier der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0 | unsigned char | Radelektronik-Status der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0_TEXT | string | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | string | Radposition der RE0 |
| STAT_BEFUELLDRUCKWERT_RE0_WERT | real | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE0_EINH | string | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | unsigned long | Radelektronik-Identifier der RE1 |
| STAT_RE_IDENTIFIER_RE1_TEXT | string | Radelektronik-Identifier der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1 | unsigned char | Radelektronik-Status der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1_TEXT | string | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | string | Radposition der RE1 |
| STAT_BEFUELLDRUCKWERT_RE1_WERT | real | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE1_EINH | string | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | unsigned long | Radelektronik-Identifier der RE2 |
| STAT_RE_IDENTIFIER_RE2_TEXT | string | Radelektronik-Identifier der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2 | unsigned char | Radelektronik-Status der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2_TEXT | string | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | string | Radposition der RE2 |
| STAT_BEFUELLDRUCKWERT_RE2_WERT | real | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE2_EINH | string | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | unsigned long | Radelektronik-Identifier der RE3 |
| STAT_RE_IDENTIFIER_RE3_TEXT | string | Radelektronik-Identifier der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3 | unsigned char | Radelektronik-Status der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3_TEXT | string | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | string | Radposition der RE3 |
| STAT_BEFUELLDRUCKWERT_RE3_WERT | real | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE3_EINH | string | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-kalibrierereignis3-lesen"></a>
### STATUS_HS_KALIBRIEREREIGNIS3_LESEN

Auslesen eines Kalibriereignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2322 Kalbrierereignis 3 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_DATUM_EINH | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_EINH | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_WARNSTATUS1_TEXT | string | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_BETRIEBSZUSTAND_TEXT | string | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_FAHRZEUGZUSTAND_TEXT | string | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_ZUSTANDSKENNUNG_TEXT | string | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | unsigned long | Radelektronik-Identifier der RE0 |
| STAT_RE_IDENTIFIER_RE0_TEXT | string | Radelektronik-Identifier der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0 | unsigned char | Radelektronik-Status der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0_TEXT | string | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | string | Radposition der RE0 |
| STAT_BEFUELLDRUCKWERT_RE0_WERT | real | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE0_EINH | string | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | unsigned long | Radelektronik-Identifier der RE1 |
| STAT_RE_IDENTIFIER_RE1_TEXT | string | Radelektronik-Identifier der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1 | unsigned char | Radelektronik-Status der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1_TEXT | string | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | string | Radposition der RE1 |
| STAT_BEFUELLDRUCKWERT_RE1_WERT | real | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE1_EINH | string | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | unsigned long | Radelektronik-Identifier der RE2 |
| STAT_RE_IDENTIFIER_RE2_TEXT | string | Radelektronik-Identifier der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2 | unsigned char | Radelektronik-Status der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2_TEXT | string | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | string | Radposition der RE2 |
| STAT_BEFUELLDRUCKWERT_RE2_WERT | real | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE2_EINH | string | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | unsigned long | Radelektronik-Identifier der RE3 |
| STAT_RE_IDENTIFIER_RE3_TEXT | string | Radelektronik-Identifier der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3 | unsigned char | Radelektronik-Status der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3_TEXT | string | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | string | Radposition der RE3 |
| STAT_BEFUELLDRUCKWERT_RE3_WERT | real | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE3_EINH | string | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-warnereignis1-lesen"></a>
### STATUS_HS_WARNEREIGNIS1_LESEN

Auslesen eines Warneignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2310 Warnereignis 1 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_DATUM_EINH | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_EINH | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_WARNSTATUS1_TEXT | string | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_BETRIEBSZUSTAND_TEXT | string | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_FAHRZEUGZUSTAND_TEXT | string | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_ZUSTANDSKENNUNG_TEXT | string | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | unsigned long | Radelektronik-Identifier der RE0 |
| STAT_RE_IDENTIFIER_RE0_TEXT | string | Radelektronik-Identifier der RE0 |
| STAT_REIFENDRUCKWERT_RE0_WERT | real | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE0_EINH | string | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_WERT | char | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_EINH | string | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE0 | unsigned char | Radelektronik-Status der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0_TEXT | string | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | string | Radposition der RE0 |
| STAT_BEFUELLDRUCKWERT_RE0_WERT | real | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE0_EINH | string | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | unsigned long | Radelektronik-Identifier der RE1 |
| STAT_RE_IDENTIFIER_RE1_TEXT | string | Radelektronik-Identifier der RE1 |
| STAT_REIFENDRUCKWERT_RE1_WERT | real | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE1_EINH | string | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_WERT | char | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_EINH | string | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE1 | unsigned char | Radelektronik-Status der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1_TEXT | string | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | string | Radposition der RE1 |
| STAT_BEFUELLDRUCKWERT_RE1_WERT | real | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE1_EINH | string | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | unsigned long | Radelektronik-Identifier der RE2 |
| STAT_RE_IDENTIFIER_RE2_TEXT | string | Radelektronik-Identifier der RE2 |
| STAT_REIFENDRUCKWERT_RE2_WERT | real | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE2_EINH | string | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_WERT | char | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_EINH | string | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE2 | unsigned char | Radelektronik-Status der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2_TEXT | string | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | string | Radposition der RE2 |
| STAT_BEFUELLDRUCKWERT_RE2_WERT | real | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE2_EINH | string | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | unsigned long | Radelektronik-Identifier der RE3 |
| STAT_RE_IDENTIFIER_RE3_TEXT | string | Radelektronik-Identifier der RE3 |
| STAT_REIFENDRUCKWERT_RE3_WERT | real | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE3_EINH | string | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_WERT | char | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_EINH | string | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE3 | unsigned char | Radelektronik-Status der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3_TEXT | string | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | string | Radposition der RE3 |
| STAT_BEFUELLDRUCKWERT_RE3_WERT | real | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE3_EINH | string | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-warnereignis2-lesen"></a>
### STATUS_HS_WARNEREIGNIS2_LESEN

Auslesen eines Warneignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2311 Warnereignis 2 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_DATUM_EINH | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_EINH | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_WARNSTATUS1_TEXT | string | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_BETRIEBSZUSTAND_TEXT | string | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_FAHRZEUGZUSTAND_TEXT | string | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_ZUSTANDSKENNUNG_TEXT | string | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | unsigned long | Radelektronik-Identifier der RE0 |
| STAT_RE_IDENTIFIER_RE0_TEXT | string | Radelektronik-Identifier der RE0 |
| STAT_REIFENDRUCKWERT_RE0_WERT | real | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE0_EINH | string | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_WERT | char | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_EINH | string | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE0 | unsigned char | Radelektronik-Status der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0_TEXT | string | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | string | Radposition der RE0 |
| STAT_BEFUELLDRUCKWERT_RE0_WERT | real | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE0_EINH | string | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | unsigned long | Radelektronik-Identifier der RE1 |
| STAT_RE_IDENTIFIER_RE1_TEXT | string | Radelektronik-Identifier der RE1 |
| STAT_REIFENDRUCKWERT_RE1_WERT | real | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE1_EINH | string | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_WERT | char | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_EINH | string | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE1 | unsigned char | Radelektronik-Status der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1_TEXT | string | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | string | Radposition der RE1 |
| STAT_BEFUELLDRUCKWERT_RE1_WERT | real | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE1_EINH | string | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | unsigned long | Radelektronik-Identifier der RE2 |
| STAT_RE_IDENTIFIER_RE2_TEXT | string | Radelektronik-Identifier der RE2 |
| STAT_REIFENDRUCKWERT_RE2_WERT | real | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE2_EINH | string | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_WERT | char | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_EINH | string | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE2 | unsigned char | Radelektronik-Status der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2_TEXT | string | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | string | Radposition der RE2 |
| STAT_BEFUELLDRUCKWERT_RE2_WERT | real | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE2_EINH | string | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | unsigned long | Radelektronik-Identifier der RE3 |
| STAT_RE_IDENTIFIER_RE3_TEXT | string | Radelektronik-Identifier der RE3 |
| STAT_REIFENDRUCKWERT_RE3_WERT | real | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE3_EINH | string | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_WERT | char | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_EINH | string | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE3 | unsigned char | Radelektronik-Status der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3_TEXT | string | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | string | Radposition der RE3 |
| STAT_BEFUELLDRUCKWERT_RE3_WERT | real | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE3_EINH | string | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-warnereignis3-lesen"></a>
### STATUS_HS_WARNEREIGNIS3_LESEN

Auslesen eines Warneignisses des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2312 Warnereignis 3 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_DATUM_EINH | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_EINH | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_WARNSTATUS1_TEXT | string | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_BETRIEBSZUSTAND_TEXT | string | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_FAHRZEUGZUSTAND_TEXT | string | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_ZUSTANDSKENNUNG_TEXT | string | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | unsigned long | Radelektronik-Identifier der RE0 |
| STAT_RE_IDENTIFIER_RE0_TEXT | string | Radelektronik-Identifier der RE0 |
| STAT_REIFENDRUCKWERT_RE0_WERT | real | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE0_EINH | string | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_WERT | char | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_EINH | string | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE0 | unsigned char | Radelektronik-Status der RE0 |
| STAT_RADELEKTRONIK_STATUS_RE0_TEXT | string | Radelektronik-Status der RE0 |
| STAT_RAD_POSITION_RE0 | string | Radposition der RE0 |
| STAT_BEFUELLDRUCKWERT_RE0_WERT | real | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE0_EINH | string | Befuelldruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE0_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0 | int | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE0_EINH | string | Restlebensdauer der Radelektronik RE0 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE1 | unsigned long | Radelektronik-Identifier der RE1 |
| STAT_RE_IDENTIFIER_RE1_TEXT | string | Radelektronik-Identifier der RE1 |
| STAT_REIFENDRUCKWERT_RE1_WERT | real | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE1_EINH | string | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_WERT | char | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_EINH | string | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE1 | unsigned char | Radelektronik-Status der RE1 |
| STAT_RADELEKTRONIK_STATUS_RE1_TEXT | string | Radelektronik-Status der RE1 |
| STAT_RAD_POSITION_RE1 | string | Radposition der RE1 |
| STAT_BEFUELLDRUCKWERT_RE1_WERT | real | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE1_EINH | string | Befuelldruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE1_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1 | int | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE1_EINH | string | Restlebensdauer der Radelektronik RE1 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE2 | unsigned long | Radelektronik-Identifier der RE2 |
| STAT_RE_IDENTIFIER_RE2_TEXT | string | Radelektronik-Identifier der RE2 |
| STAT_REIFENDRUCKWERT_RE2_WERT | real | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE2_EINH | string | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_WERT | char | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_EINH | string | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE2 | unsigned char | Radelektronik-Status der RE2 |
| STAT_RADELEKTRONIK_STATUS_RE2_TEXT | string | Radelektronik-Status der RE2 |
| STAT_RAD_POSITION_RE2 | string | Radposition der RE2 |
| STAT_BEFUELLDRUCKWERT_RE2_WERT | real | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE2_EINH | string | Befuelldruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE2_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2 | int | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE2_EINH | string | Restlebensdauer der Radelektronik RE2 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE3 | unsigned long | Radelektronik-Identifier der RE3 |
| STAT_RE_IDENTIFIER_RE3_TEXT | string | Radelektronik-Identifier der RE3 |
| STAT_REIFENDRUCKWERT_RE3_WERT | real | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE3_EINH | string | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_WERT | char | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_EINH | string | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RADELEKTRONIK_STATUS_RE3 | unsigned char | Radelektronik-Status der RE3 |
| STAT_RADELEKTRONIK_STATUS_RE3_TEXT | string | Radelektronik-Status der RE3 |
| STAT_RAD_POSITION_RE3 | string | Radposition der RE3 |
| STAT_BEFUELLDRUCKWERT_RE3_WERT | real | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLDRUCKWERT_RE3_EINH | string | Befuelldruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_WERT | char | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_BEFUELLTEMPERATURWERT_RE3_EINH | string | Bezugstemperatur fuer Befuelldruckwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3 | int | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_RE3_EINH | string | Restlebensdauer der Radelektronik RE3 in Monaten Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-warnereignis-ruecknahme"></a>
### STATUS_HS_WARNEREIGNIS_RUECKNAHME

Auslesen der Warnungsruecknahme aus dem Historienspeicher KWP2000: $22   ReadDataByCommonIdentifier $2340 Warnungsruecknahme Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | long | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand Bereich: 0 km bis 524272 km (-999999 km =&gt; ungueltig) |
| STAT_DATUM_WERT | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_DATUM_EINH | string | Datum (99.99.99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_WERT | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_SYSTEMZEIT_EINH | string | Uhrzeit (99:99:99 =&gt; ungueltig) Achtung: Rückgabe als _TEXT!! |
| STAT_WARNSTATUS1 | unsigned int | Warnstatus 1 |
| STAT_WARNSTATUS1_TEXT | string | Warnstatus 1 |
| STAT_BETRIEBSZUSTAND | unsigned int | Betriebszustand |
| STAT_BETRIEBSZUSTAND_TEXT | string | Betriebszustand |
| STAT_FAHRZEUGZUSTAND | unsigned int | Fahrzeugzustand |
| STAT_FAHRZEUGZUSTAND_TEXT | string | Fahrzeugzustand |
| STAT_ZUSTANDSKENNUNG | unsigned int | Zustandskennung |
| STAT_ZUSTANDSKENNUNG_TEXT | string | Zustandskennung |
| STAT_AUSSENTEMPERATUR | char | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_AUSSENTEMPERATUR_EINH | string | Aussentemperatur Bereich: -40 bis 127 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RE_IDENTIFIER_RE0 | unsigned long | Radelektronik-Identifier der RE0 |
| STAT_RE_IDENTIFIER_RE0_TEXT | string | Radelektronik-Identifier der RE0 |
| STAT_REIFENDRUCKWERT_RE0_WERT | real | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE0_EINH | string | Reifendruckwert der RE0 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_WERT | char | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE0_EINH | string | Reifentemperaturwert der RE0 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RAD_POSITION_RE0 | string | Radposition der RE0 |
| STAT_RE_IDENTIFIER_RE1 | unsigned long | Radelektronik-Identifier der RE1 |
| STAT_RE_IDENTIFIER_RE1_TEXT | string | Radelektronik-Identifier der RE1 |
| STAT_REIFENDRUCKWERT_RE1_WERT | real | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE1_EINH | string | Reifendruckwert der RE1 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_WERT | char | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE1_EINH | string | Reifentemperaturwert der RE1 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RAD_POSITION_RE1 | string | Radposition der RE1 |
| STAT_RE_IDENTIFIER_RE2 | unsigned long | Radelektronik-Identifier der RE2 |
| STAT_RE_IDENTIFIER_RE2_TEXT | string | Radelektronik-Identifier der RE2 |
| STAT_REIFENDRUCKWERT_RE2_WERT | real | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE2_EINH | string | Reifendruckwert der RE2 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_WERT | char | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE2_EINH | string | Reifentemperaturwert der RE2 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RAD_POSITION_RE2 | string | Radposition der RE2 |
| STAT_RE_IDENTIFIER_RE3 | unsigned long | Radelektronik-Identifier der RE3 |
| STAT_RE_IDENTIFIER_RE3_TEXT | string | Radelektronik-Identifier der RE3 |
| STAT_REIFENDRUCKWERT_RE3_WERT | real | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_RE3_EINH | string | Reifendruckwert der RE3 Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_WERT | char | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_REIFENTEMPERATURWERT_RE3_EINH | string | Reifentemperaturwert der RE3 Bereich: -40 bis 120 Grad C (-99 °C =&gt; ungueltig) |
| STAT_RAD_POSITION_RE3 | string | Radposition der RE3 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-warnungszaehler-lesen"></a>
### STATUS_HS_WARNUNGSZAEHLER_LESEN

Auslesen der Warnungszaehler des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2300 Warnungszaehler Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZAEHLER_HARTE_WARNUNG_VL | unsigned char | Zaehler der harten Warnungen vorne links |
| STAT_ZAEHLER_HARTE_WARNUNG_VL_TEXT | string | Zaehler der harten Warnungen vorne links |
| STAT_ZAEHLER_HARTE_WARNUNG_VR | unsigned char | Zaehler der harten Warnungen vorne rechts |
| STAT_ZAEHLER_HARTE_WARNUNG_VR_TEXT | string | Zaehler der harten Warnungen vorne rechts |
| STAT_ZAEHLER_HARTE_WARNUNG_HL | unsigned char | Zaehler der harten Warnungen hinten links |
| STAT_ZAEHLER_HARTE_WARNUNG_HL_TEXT | string | Zaehler der harten Warnungen hinten links |
| STAT_ZAEHLER_HARTE_WARNUNG_HR | unsigned char | Zaehler der harten Warnungen hinten rechts |
| STAT_ZAEHLER_HARTE_WARNUNG_HR_TEXT | string | Zaehler der harten Warnungen hinten rechts |
| STAT_ZAEHLER_HARTE_WARNUNG_XX | unsigned char | Zaehler der harten Warnungen waehrend ER Verlust |
| STAT_ZAEHLER_HARTE_WARNUNG_XX_TEXT | string | Zaehler der harten Warnungen waehrend ER Verlust |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-warn-ruecknahme-zaehler-lesen"></a>
### STATUS_HS_WARN_RUECKNAHME_ZAEHLER_LESEN

Auslesen der Zaehler fuer Warnungsruecknahmen durch Luftnachfuellen oder Radtausch KWP2000: $22   ReadDataByCommonIdentifier $2303 Warnungsruecknahmezaehler Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZAEHLER_WARN_RUECKNAHME | unsigned char | Zaehler Warnungsruecknahmen durch Luftnachfuellen oder Radtausch |
| STAT_ZAEHLER_WARN_RUECKNAHME_TEXT | string | Zaehler Warnungsruecknahmen durch Luftnachfuellen oder Radtausch |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hs-zaehler-weiche-warnung-lesen"></a>
### STATUS_HS_ZAEHLER_WEICHE_WARNUNG_LESEN

Auslesen der Vorwarnzaehler des Historienspeichers KWP2000: $22   ReadDataByCommonIdentifier $2301 Warnungszaehler Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZAEHLER_WEICHE_WARNUNG_VL | unsigned char | Zaehler der weichen Warnungen vorne links |
| STAT_ZAEHLER_WEICHE_WARNUNG_VL_TEXT | string | Zaehler der weichen Warnungen vorne links |
| STAT_ZAEHLER_WEICHE_WARNUNG_VR | unsigned char | Zaehler der weichen Warnungen vorne rechts |
| STAT_ZAEHLER_WEICHE_WARNUNG_VR_TEXT | string | Zaehler der weichen Warnungen vorne rechts |
| STAT_ZAEHLER_WEICHE_WARNUNG_HL | unsigned char | Zaehler der weichen Warnungen hinten links |
| STAT_ZAEHLER_WEICHE_WARNUNG_HL_TEXT | string | Zaehler der weichen Warnungen hinten links |
| STAT_ZAEHLER_WEICHE_WARNUNG_HR | unsigned char | Zaehler der weichen Warnungen hinten rechts |
| STAT_ZAEHLER_WEICHE_WARNUNG_HR_TEXT | string | Zaehler der weichen Warnungen hinten rechts |
| STAT_ZAEHLER_WEICHE_WARNUNG_XX | unsigned char | Zaehler der weichen Warnungen waehrend ER Verlust |
| STAT_ZAEHLER_WEICHE_WARNUNG_XX_TEXT | string | Zaehler der weichen Warnungen waehrend ER Verlust |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdatenblock-gen3-1"></a>
### STATUS_MESSDATENBLOCK_GEN3_1

Auslesen von Messdatenblock 1 KWP2000: $21   ReadDataByLocalIdentifier $30   Messdatenblock 1 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik Identifier |
| STAT_RE_IDENTIFIER_TEXT | string | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | unsigned char | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_RAD_POSITION_NR_TEXT | string | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | real | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_SOLLDRUCK_EINH | string | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE | unsigned int | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_GUTEMPFAENGE_TEXT | string | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | unsigned char | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_AUSBEUTE_TEXT | string | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | int | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RSSI_PEGEL_TEXT | string | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | int | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RESTLEBENSDAUER_TEXT | string | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | unsigned char | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_RADELEKTRONIK_STATUS_TEXT | string | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | unsigned char | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_HARTE_WARNUNG_AKTIV_TEXT | string | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | unsigned char | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_POS_CHANGED_TEXT | string | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | unsigned char | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV_TEXT | string | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_DREHRICHTUNG | unsigned char | Drehrichtung des Rades 0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_DREHRICHTUNG_TEXT | string | Drehrichtung des Rades 0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_FOLGEAUSFALL | unsigned char | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| STAT_FOLGEAUSFALL_TEXT | string | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdatenblock-gen3-2"></a>
### STATUS_MESSDATENBLOCK_GEN3_2

Auslesen von Messdatenblock 2 KWP2000: $21   ReadDataByLocalIdentifier $31   Messdatenblock 2 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik Identifier |
| STAT_RE_IDENTIFIER_TEXT | string | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | unsigned char | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_RAD_POSITION_NR_TEXT | string | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | real | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_SOLLDRUCK_EINH | string | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE | unsigned int | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_GUTEMPFAENGE_TEXT | string | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | unsigned char | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_AUSBEUTE_TEXT | string | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | int | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RSSI_PEGEL_TEXT | string | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | int | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RESTLEBENSDAUER_TEXT | string | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | unsigned char | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_RADELEKTRONIK_STATUS_TEXT | string | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | unsigned char | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_HARTE_WARNUNG_AKTIV_TEXT | string | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | unsigned char | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_POS_CHANGED_TEXT | string | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | unsigned char | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV_TEXT | string | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_DREHRICHTUNG | unsigned char | Drehrichtung des Rades 0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_DREHRICHTUNG_TEXT | string | Drehrichtung des Rades 0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_FOLGEAUSFALL | unsigned char | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| STAT_FOLGEAUSFALL_TEXT | string | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdatenblock-gen3-3"></a>
### STATUS_MESSDATENBLOCK_GEN3_3

Auslesen von Messdatenblock 3 KWP2000: $21   ReadDataByLocalIdentifier $32   Messdatenblock 3 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik Identifier |
| STAT_RE_IDENTIFIER_TEXT | string | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | unsigned char | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_RAD_POSITION_NR_TEXT | string | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | real | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_SOLLDRUCK_EINH | string | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE | unsigned int | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_GUTEMPFAENGE_TEXT | string | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | unsigned char | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_AUSBEUTE_TEXT | string | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | int | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RSSI_PEGEL_TEXT | string | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | int | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RESTLEBENSDAUER_TEXT | string | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | unsigned char | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_RADELEKTRONIK_STATUS_TEXT | string | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | unsigned char | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_HARTE_WARNUNG_AKTIV_TEXT | string | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | unsigned char | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_POS_CHANGED_TEXT | string | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | unsigned char | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV_TEXT | string | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_DREHRICHTUNG | unsigned char | Drehrichtung des Rades 0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_DREHRICHTUNG_TEXT | string | Drehrichtung des Rades 0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_FOLGEAUSFALL | unsigned char | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| STAT_FOLGEAUSFALL_TEXT | string | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdatenblock-gen3-4"></a>
### STATUS_MESSDATENBLOCK_GEN3_4

Auslesen von Messdatenblock 4 KWP2000: $21   ReadDataByLocalIdentifier $33   Messdatenblock 4 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RE_IDENTIFIER | unsigned long | Radelektronik Identifier |
| STAT_RE_IDENTIFIER_TEXT | string | Radelektronik Identifier |
| STAT_RAD_POSITION_NR | unsigned char | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_RAD_POSITION_NR_TEXT | string | Ausgelesene Radposition des Identifiers (Messblock) wurde vom SG der jeweiligen Position zugewiesen. Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |
| STAT_LETZTER_REIFENDRUCKWERT_WERT | real | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENDRUCKWERT_EINH | string | Letzer gültiger Reifendruckwert der vom ausgewählten Rad zurückgeliefert wird |
| STAT_LETZTER_REIFENTEMPERATURWERT_WERT | char | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_LETZTER_REIFENTEMPERATURWERT_EINH | string | Letzte gültige Reifentemperatur des ausgewählten Rads |
| STAT_SOLLDRUCK_WERT | real | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_SOLLDRUCK_EINH | string | Vorgegebener Solldruck des ausgewählten Rads |
| STAT_GUTEMPFAENGE | unsigned int | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_GUTEMPFAENGE_TEXT | string | Anzahl korrekt empfangener Telegramme vom ausgewählten Rad |
| STAT_AUSBEUTE | unsigned char | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_AUSBEUTE_TEXT | string | Telegrammausbeute vom ausgewählten Rad in Prozent |
| STAT_RSSI_PEGEL | int | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RSSI_PEGEL_TEXT | string | RSSI - Pegel der ID [Einheit: AD Wandler-Einheiten] |
| STAT_RESTLEBENSDAUER | int | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RESTLEBENSDAUER_TEXT | string | Verbleibende Restlebensdauer der Batterie am Radsensor in Monaten |
| STAT_RADELEKTRONIK_STATUS | unsigned char | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_RADELEKTRONIK_STATUS_TEXT | string | Status Meldung der Radelektronik des angewählten Rads. |
| STAT_HARTE_WARNUNG_AKTIV | unsigned char | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_HARTE_WARNUNG_AKTIV_TEXT | string | Pannen Warnung vom angewählten Rad, 0= Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_POS_CHANGED | unsigned char | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_POS_CHANGED_TEXT | string | Radelektronik ID vom angewählten Rad hat sich geändert, 0 = nicht geändert, 1 = geändert, FF= Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV | unsigned char | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_RE_OVERHEAT_AKTIV_TEXT | string | Überhitzungsmeldung der Radelektronik vom angewählten Rad, 0 = Inaktiv, 1 = aktiv, FF = Signal unbekannt |
| STAT_DREHRICHTUNG | unsigned char | Drehrichtung des Rades 0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_DREHRICHTUNG_TEXT | string | Drehrichtung des Rades 0=Stillstand 1=rechts 2=links 3=unbekannt 255=nicht definiert |
| STAT_FOLGEAUSFALL | unsigned char | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| STAT_FOLGEAUSFALL_TEXT | string | Anzahl Zeitintervalle (typ. 60s) seit letztem Telegrammempfang |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rdc-gen3-lesen"></a>
### STATUS_RDC_GEN3_LESEN

Auslesen Statusinformation KWP2000: $21   ReadDataByLocalIdentifier $36   I/O-Status lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EIGENRAEDER_BEKANNT | unsigned char | Alle Eigenraeder sind bekannt: 0 = nicht bekannt  1 = bekannt |
| STAT_EIGENRAEDER_BEKANNT_TEXT | string | Alle Eigenraeder sind bekannt: 0 = nicht bekannt  1 = bekannt |
| STAT_RADPOS_ER_BEKANNT | unsigned char | Radpositionen aller Eigenraeder sind bekannt: 0 = nicht bekannt  1 = bekannt |
| STAT_RADPOS_ER_BEKANNT_TEXT | string | Radpositionen aller Eigenraeder sind bekannt: 0 = nicht bekannt  1 = bekannt |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT | unsigned char | Alle Radpositionen sind ueberprueft und bestaetigt: 0 = nicht bestätigt  1 = bestätigt |
| STAT_RADPOS_UEBERPRUEFT_BESTAETIGT_TEXT | string | Alle Radpositionen sind ueberprueft und bestaetigt: 0 = nicht bestätigt  1 = bestätigt |
| STAT_DTC_INACTIVE | unsigned char | Aktiver DTC Fehler mit Warnlampe im Fehlerspeicher vorhanden: 0 = DTC inaktiv  1 = DTC aktiv |
| STAT_DTC_INACTIVE_TEXT | string | Aktiver DTC Fehler mit Warnlampe im Fehlerspeicher vorhanden: 0 = DTC inaktiv  1 = DTC aktiv |
| STAT_KAL_ANFORDERUNG_AKTIV | unsigned char | Kalibrieranforderung steht an: 0 = Kalibrieranforderung inaktiv  1 = Kalibrieranforderung aktiv |
| STAT_KAL_ANFORDERUNG_AKTIV_TEXT | string | Kalibrieranforderung steht an: 0 = Kalibrieranforderung inaktiv  1 = Kalibrieranforderung aktiv |
| STAT_RAD_ZUORDNUNG_TIMEOUT | unsigned char | Radzuordnung konnte nicht abgeschlossen werden: 0 = kein Timeout  1 = Timeout |
| STAT_RAD_ZUORDNUNG_TIMEOUT_TEXT | string | Radzuordnung konnte nicht abgeschlossen werden: 0 = kein Timeout  1 = Timeout |
| STAT_BANDMODE_AKTIV | unsigned char | Abfrage ob Bandmode im RDC aktiviert ist: 0 = Bandmode inaktiv   1 = Bandmode aktiv |
| STAT_BANDMODE_AKTIV_TEXT | string | Abfrage ob Bandmode im RDC aktiviert ist: 0 = Bandmode inaktiv   1 = Bandmode aktiv |
| STAT_ER_ERKENNUNG_FAHRT | unsigned char | Eigenraderkennung waehrend der Fahrt wurde gestartet: 0 = nicht gestartet 1 = gestartet |
| STAT_ER_ERKENNUNG_FAHRT_TEXT | string | Eigenraderkennung waehrend der Fahrt wurde gestartet: 0 = nicht gestartet 1 = gestartet |
| STAT_TEST_EIGENRAD_FAHRT | unsigned char | Test-Eigenraderkennung in Fahrt wurde gestartet: 0 = nicht gestartet , 1 = gestartet |
| STAT_TEST_EIGENRAD_FAHRT_TEXT | string | Test-Eigenraderkennung in Fahrt wurde gestartet: 0 = nicht gestartet , 1 = gestartet |
| STAT_TEST_EIGENRAD_STAND | unsigned char | Test-Eigenraderkennung im Stand wurde gestartet: 0 = nicht gestartet, 1 = gestartet |
| STAT_TEST_EIGENRAD_STAND_TEXT | string | Test-Eigenraderkennung im Stand wurde gestartet: 0 = nicht gestartet, 1 = gestartet |
| STAT_ER_FAHRT_VTHRS_AKTIV | unsigned char | Geschwindigkeitsschwelle fuer Eigenraderkennung bei Fahrt aktiviert : 0 = inaktiv , 1 = aktiv |
| STAT_ER_FAHRT_VTHRS_AKTIV_TEXT | string | Geschwindigkeitsschwelle fuer Eigenraderkennung bei Fahrt aktiviert : 0 = inaktiv , 1 = aktiv |
| STAT_BM_TIMEOUT_ACTIVE | unsigned char | Bandmode Timeout laeuft : 0 = inaktiv , 1 = aktiv |
| STAT_BM_TIMEOUT_ACTIVE_TEXT | string | Bandmode Timeout laeuft : 0 = inaktiv , 1 = aktiv |
| STAT_HARTE_WARNUNG_UNSPEZIFISCH_AKTIV | unsigned char | Harte Warnung unspezifisch, aktiv: 0 = inaktiv   1 = aktiv |
| STAT_HARTE_WARNUNG_UNSPEZIFISCH_AKTIV_TEXT | string | Harte Warnung unspezifisch, aktiv: 0 = inaktiv   1 = aktiv |
| STAT_HARTE_WARNUNG_VL_AKTIV | unsigned char | Harte Warnung vorne links, aktiv: 0 = inaktiv   1 = aktiv |
| STAT_HARTE_WARNUNG_VL_AKTIV_TEXT | string | Harte Warnung vorne links, aktiv: 0 = inaktiv   1 = aktiv |
| STAT_HARTE_WARNUNG_VR_AKTIV | unsigned char | Harte Warnung vorne rechts, aktiv: 0 = inaktiv   1 = aktiv |
| STAT_HARTE_WARNUNG_VR_AKTIV_TEXT | string | Harte Warnung vorne rechts, aktiv: 0 = inaktiv   1 = aktiv |
| STAT_HARTE_WARNUNG_HL_AKTIV | unsigned char | Harte Warnung hinten links, aktiv: 0 = inaktiv   1 = aktiv |
| STAT_HARTE_WARNUNG_HL_AKTIV_TEXT | string | Harte Warnung hinten links, aktiv: 0 = inaktiv   1 = aktiv |
| STAT_HARTE_WARNUNG_HR_AKTIV | unsigned char | Harte Warnung hinten rechts, aktiv: 0 = inaktiv   1 = aktiv |
| STAT_HARTE_WARNUNG_HR_AKTIV_TEXT | string | Harte Warnung hinten rechts, aktiv: 0 = inaktiv   1 = aktiv |
| STAT_KL_15_EIN | unsigned char | Klemme 15 EIN : 0 = AUS, 1 = EIN |
| STAT_KL_15_EIN_TEXT | string | Klemme 15 EIN : 0 = AUS, 1 = EIN |
| STAT_MOTOR_LAEUFT_EIN | unsigned char | Motor läuft : 0 = Aus   1 = EIN |
| STAT_MOTOR_LAEUFT_EIN_TEXT | string | Motor läuft : 0 = Aus   1 = EIN |
| STAT_FZG_FAEHRT | unsigned char | Signal Fahrzeug fährt : 0 = steht , 1 = fährt |
| STAT_FZG_FAEHRT_TEXT | string | Signal Fahrzeug fährt : 0 = steht , 1 = fährt |
| STAT_ERKENNUNG_ALLE_RE | unsigned char | Alle Radelektroniken erkannt : 0 = nicht erkannt 1 = erkannt |
| STAT_ERKENNUNG_ALLE_RE_TEXT | string | Alle Radelektroniken erkannt : 0 = nicht erkannt 1 = erkannt |
| STAT_ERKENNUNG_ZUVIELE_RE | unsigned char | Zu viele Radelektroniken erkannt : 0 = nicht erkannt , 1 = erkannt |
| STAT_ERKENNUNG_ZUVIELE_RE_TEXT | string | Zu viele Radelektroniken erkannt : 0 = nicht erkannt , 1 = erkannt |
| STAT_STOERSENDER | unsigned char | Funkstoerung vorhanden : 0 = inaktiv , 1 = aktiv |
| STAT_STOERSENDER_TEXT | string | Funkstoerung vorhanden : 0 = inaktiv , 1 = aktiv |
| STAT_FREQUENZ_WERT | unsigned int | Gibt die aktuelle RF-Frequenz zurück. Die Frequenz ist abhaengig von der Codierung. (315 oder 433). Angabe in MHz |
| STAT_FREQUENZ_EINH | string | Gibt die aktuelle RF-Frequenz zurück. Die Frequenz ist abhaengig von der Codierung. (315 oder 433). Angabe in MHz |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-re-lesen-druckcodierung"></a>
### STATUS_RE_LESEN_DRUCKCODIERUNG

Listet alle RE im schnellen Sendemode mit Druckwert über 1,5 bar absolut KWP2000: $21   ReadDataByLocalIdentifier $37   Status_RE_Lesen_Druckcodierung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RE_IDENTIFIER_0 | unsigned long | Radelektronik Identifier in (Zeile 0) |
| STAT_RE_IDENTIFIER_0_TEXT | string | Radelektronik (RE) Identifier in (Zeile 0) |
| STAT_REIFENDRUCKWERT_0_WERT | real | Reifendruckwert der RE in (Zeile 0) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_0_EINH | string | Reifendruckwert der RE in (Zeile 0) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_0 | int | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 0) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_0_EINH | string | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 0) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_0 | unsigned char | Empfangszaehler der RE in (Zeile 0) |
| STAT_EMPFANGSZAEHLER_0_TEXT | string | Empfangszaehler der RE in (Zeile 0) |
| STAT_RE_IDENTIFIER_1 | unsigned long | Radelektronik Identifier in (Zeile 1) |
| STAT_RE_IDENTIFIER_1_TEXT | string | Radelektronik (RE) Identifier in (Zeile 1) |
| STAT_REIFENDRUCKWERT_1_WERT | real | Reifendruckwert der RE in (Zeile 1) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_1_EINH | string | Reifendruckwert der RE in (Zeile 1) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_1 | int | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 1) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_1_EINH | string | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 1) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_1 | unsigned char | Empfangszaehler der RE in (Zeile 1) |
| STAT_EMPFANGSZAEHLER_1_TEXT | string | Empfangszaehler der RE in (Zeile 1) |
| STAT_RE_IDENTIFIER_2 | unsigned long | Radelektronik Identifier in (Zeile 2) |
| STAT_RE_IDENTIFIER_2_TEXT | string | Radelektronik (RE) Identifier in (Zeile 2) |
| STAT_REIFENDRUCKWERT_2_WERT | real | Reifendruckwert der RE in (Zeile 2) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_2_EINH | string | Reifendruckwert der RE in (Zeile 2) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_2 | int | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 2) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_2_EINH | string | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 2) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_2 | unsigned char | Empfangszaehler der RE in (Zeile 2) |
| STAT_EMPFANGSZAEHLER_2_TEXT | string | Empfangszaehler der RE in (Zeile 2) |
| STAT_RE_IDENTIFIER_3 | unsigned long | Radelektronik Identifier in (Zeile 3) |
| STAT_RE_IDENTIFIER_3_TEXT | string | Radelektronik (RE) Identifier in (Zeile 3) |
| STAT_REIFENDRUCKWERT_3_WERT | real | Reifendruckwert der RE in (Zeile 3) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_3_EINH | string | Reifendruckwert der RE in (Zeile 3) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_3 | int | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 3) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_3_EINH | string | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 3) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_3 | unsigned char | Empfangszaehler der RE in (Zeile 3) |
| STAT_EMPFANGSZAEHLER_3_TEXT | string | Empfangszaehler der RE in (Zeile 3) |
| STAT_RE_IDENTIFIER_4 | unsigned long | Radelektronik Identifier in (Zeile 4) |
| STAT_RE_IDENTIFIER_4_TEXT | string | Radelektronik (RE) Identifier in (Zeile 4) |
| STAT_REIFENDRUCKWERT_4_WERT | real | Reifendruckwert der RE in (Zeile 4) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_4_EINH | string | Reifendruckwert der RE in (Zeile 4) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_4 | int | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 4) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_4_EINH | string | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 4) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_4 | unsigned char | Empfangszaehler der RE in (Zeile 4) |
| STAT_EMPFANGSZAEHLER_4_TEXT | string | Empfangszaehler der RE in (Zeile 4) |
| STAT_RE_IDENTIFIER_5 | unsigned long | Radelektronik Identifier in (Zeile 5) |
| STAT_RE_IDENTIFIER_5_TEXT | string | Radelektronik (RE) Identifier in (Zeile 5) |
| STAT_REIFENDRUCKWERT_5_WERT | real | Reifendruckwert der RE in (Zeile 5) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_5_EINH | string | Reifendruckwert der RE in (Zeile 5) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_5 | int | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 5) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_5_EINH | string | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 5) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_5 | unsigned char | Empfangszaehler der RE in (Zeile 5) |
| STAT_EMPFANGSZAEHLER_5_TEXT | string | Empfangszaehler der RE in (Zeile 5) |
| STAT_RE_IDENTIFIER_6 | unsigned long | Radelektronik Identifier in (Zeile 6) |
| STAT_RE_IDENTIFIER_6_TEXT | string | Radelektronik (RE) Identifier in (Zeile 6) |
| STAT_REIFENDRUCKWERT_6_WERT | real | Reifendruckwert der RE in (Zeile 6) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_6_EINH | string | Reifendruckwert der RE in (Zeile 6) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_6 | int | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 6) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_6_EINH | string | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 6) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_6 | unsigned char | Empfangszaehler der RE in (Zeile 6) |
| STAT_EMPFANGSZAEHLER_6_TEXT | string | Empfangszaehler der RE in (Zeile 6) |
| STAT_RE_IDENTIFIER_7 | unsigned long | Radelektronik Identifier in (Zeile 7) |
| STAT_RE_IDENTIFIER_7_TEXT | string | Radelektronik (RE) Identifier in (Zeile 7) |
| STAT_REIFENDRUCKWERT_7_WERT | real | Reifendruckwert der RE in (Zeile 7) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_REIFENDRUCKWERT_7_EINH | string | Reifendruckwert der RE in (Zeile 7) Bereich: 0 bis 6,35 bar absolut (-9,999 bar absolut =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_7 | int | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 7) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_RESTLEBENSDAUER_7_EINH | string | Verbleibende Batterie-Restlebensdauer in Monaten der RE in (Zeile 7) Bereich: 0 bis 120 Monate (-999 Monate =&gt; ungueltig) |
| STAT_EMPFANGSZAEHLER_7 | unsigned char | Empfangszaehler der RE in (Zeile 7) |
| STAT_EMPFANGSZAEHLER_7_TEXT | string | Empfangszaehler der RE in (Zeile 7) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital-rdc"></a>
### STEUERN_DIGITAL_RDC

Ansteuern des Systemstatus KWP2000: $3B WriteDataByLocalIdentifier $21 Systemstatus Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONSNR | unsigned char | 1 = "BANDMODE" -  Bandmode  2 = "ER_FAHRT" - Eigenraderkennung bei Fahrt  3 = "ER_STAND" - Eigenraderkennung im Stand (Gen2)  4 - "TEST_ER_FAHRT" - Empfang der Eigenraeder bei Fahrt pruefen  5 -  "TEST_ER_STAND" - Empfang der Eigenraeder im Stand pruefen  6 - "RDCBUS_DIAG" - Stromdiagnose LIN-Teilnehmer (Gen2)  7 - "SOLLDRUCK_SCHREIBEN" - aktuelle Reifendruckwerte als Sollwert  8 - "CAL_REQUEST" - Kalibrieranforderung |
| AKTIONSNR | unsigned char | 1 - SET  0 - RESET |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-radelektronik-vorgeben"></a>
### STEUERN_RADELEKTRONIK_VORGEBEN

Radelektronik vorgeben KWP2000: $3B WriteDataByLocalIdentifier $20 Radelektronik vorgeben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RE_ID | unsigned long | ID der Radelektronik |
| RE_POS | unsigned char | Position der Radelektronik: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts, 4 = Reserverad(nur RDC Gen2), 5, 6, 7, 8, 9 = Radposition nicht bekannt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-solldruck-vorgeben"></a>
### STEUERN_SOLLDRUCK_VORGEBEN

Solldruck vorgeben KWP2000: $3B WriteDataByLocalIdentifier $22 Solldruck vorgeben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SOLLDRUCK | real | Sollwert Raddruck für Radelektronik - Zulaessiger Wertebereich von 3.000 bar bis 4.800 bar (Schrittweite 25 mbar, Absolutdruck) |
| RADPOS | unsigned char | Position Rad: 0 = vorne links,  1 = vorne rechts, 2 = hinten links, 3 = hinten rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdatenblock-ak-1"></a>
### STATUS_MESSDATENBLOCK_AK_1

Auslesen von Messdatenblock 1 (Erweiterung AK) KWP2000: $21   ReadDataByLocalIdentifier $38   Messdatenblock 1 (Erweiterung AK) lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RE_HERSTELLER | unsigned char | Radelektronik Hersteller |
| STAT_RE_HERSTELLER_TEXT | string | Radelektronik Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | unsigned char | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_SENDEMODE_TEXT | string | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER | unsigned int | Fehlercode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER_TEXT | string | Fehlercode der Radelektronik |
| STAT_ROLLSWITCH | unsigned char | Status Rollswitch |
| STAT_ROLLSWITCH_TEXT | string | Status Rollswitch |
| STAT_TELEGRAMMTYP | unsigned char | Telegrammtyp |
| STAT_TELEGRAMMTYP_TEXT | string | Telegrammtyp |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdatenblock-ak-2"></a>
### STATUS_MESSDATENBLOCK_AK_2

Auslesen von Messdatenblock 2 (Erweiterung AK) KWP2000: $21   ReadDataByLocalIdentifier $39   Messdatenblock 2 (Erweiterung AK) lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RE_HERSTELLER | unsigned char | Radelektronik Hersteller |
| STAT_RE_HERSTELLER_TEXT | string | Radelektronik Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | unsigned char | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_SENDEMODE_TEXT | string | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER | unsigned int | Fehlercode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER_TEXT | string | Fehlercode der Radelektronik |
| STAT_ROLLSWITCH | unsigned char | Status Rollswitch |
| STAT_ROLLSWITCH_TEXT | string | Status Rollswitch |
| STAT_TELEGRAMMTYP | unsigned char | Telegrammtyp |
| STAT_TELEGRAMMTYP_TEXT | string | Telegrammtyp |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdatenblock-ak-3"></a>
### STATUS_MESSDATENBLOCK_AK_3

Auslesen von Messdatenblock 3 (Erweiterung AK) KWP2000: $21   ReadDataByLocalIdentifier $3A   Messdatenblock 3 (Erweiterung AK) lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RE_HERSTELLER | unsigned char | Radelektronik Hersteller |
| STAT_RE_HERSTELLER_TEXT | string | Radelektronik Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | unsigned char | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_SENDEMODE_TEXT | string | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER | unsigned int | Fehlercode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER_TEXT | string | Fehlercode der Radelektronik |
| STAT_ROLLSWITCH | unsigned char | Status Rollswitch |
| STAT_ROLLSWITCH_TEXT | string | Status Rollswitch |
| STAT_TELEGRAMMTYP | unsigned char | Telegrammtyp |
| STAT_TELEGRAMMTYP_TEXT | string | Telegrammtyp |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messdatenblock-ak-4"></a>
### STATUS_MESSDATENBLOCK_AK_4

Auslesen von Messdatenblock 4 (Erweiterung AK) KWP2000: $21   ReadDataByLocalIdentifier $3B   Messdatenblock 4 (Erweiterung AK) lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RE_HERSTELLER | unsigned char | Radelektronik Hersteller |
| STAT_RE_HERSTELLER_TEXT | string | Radelektronik Hersteller |
| STAT_RADELEKTRONIK_SENDEMODE | unsigned char | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_SENDEMODE_TEXT | string | Sendemode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER | unsigned int | Fehlercode der Radelektronik |
| STAT_RADELEKTRONIK_FEHLER_TEXT | string | Fehlercode der Radelektronik |
| STAT_ROLLSWITCH | unsigned char | Status Rollswitch |
| STAT_ROLLSWITCH_TEXT | string | Status Rollswitch |
| STAT_TELEGRAMMTYP | unsigned char | Telegrammtyp |
| STAT_TELEGRAMMTYP_TEXT | string | Telegrammtyp |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierdaten-lesen"></a>
### STATUS_CODIERDATEN_LESEN

Auslesen der vorhandenen Codierdaten KWP2000: $21   ReadDataByLocalIdentifier $35   Messdatenblock 1 (Erweiterung AK) lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TPMS_MARKET | unsigned char | US oder EU Markt 0 = EU 1 = US |
| STAT_TPMS_MARKET_TEXT | string | US oder EU Markt 0 = EU 1 = US |
| STAT_DELAY_PREWARN_ENABLE | unsigned char | Aktiviert / deaktiviert die Verzoegerung der Vorwarnung auf Basis der Fahrzeuggeschwindigkeit 0 = deaktiviert 1 = aktiviert |
| STAT_DELAY_PREWARN_ENABLE_TEXT | string | Aktiviert / deaktiviert die Verzoegerung der Vorwarnung auf Basis der Fahrzeuggeschwindigkeit 0 = deaktiviert 1 = aktiviert |
| STAT_PREWARN_ENABLE | unsigned char | Aktiviert / deaktiviert die Anzeige der Vorwarnung 0 = deaktiviert 1 = aktiviert |
| STAT_PREWARN_ENABLE_TEXT | string | Aktiviert / deaktiviert die Anzeige der Vorwarnung 0 = deaktiviert 1 = aktiviert |
| STAT_P_CHECK_DISPLAY | unsigned char | Aktiviert / deaktiviert die Meldung bei abgewiesenem Reset 0 = deaktiviert 1 = aktiviert |
| STAT_P_CHECK_DISPLAY_TEXT | string | Aktiviert / deaktiviert die Meldung bei abgewiesenem Reset 0 = deaktiviert 1 = aktiviert |
| STAT_PREWARN_FUELSTOP | unsigned char | Aktiviert / deaktiviert die Vorwarnung beim Tanken 0 = deaktiviert 1 = aktiviert |
| STAT_PREWARN_FUELSTOP_TEXT | string | Aktiviert / deaktiviert die Vorwarnung beim Tanken 0 = deaktiviert 1 = aktiviert |
| STAT_PREWARN_IGNITION | unsigned char | Aktiviert / deaktiviert die Anzeige der Vorwarnung beim Klemmenwechsel 0 = deaktiviert 1 = aktiviert |
| STAT_PREWARN_IGNITION_TEXT | string | Aktiviert / deaktiviert die Anzeige der Vorwarnung beim Klemmenwechsel 0 = deaktiviert 1 = aktiviert |
| STAT_PREC_RESET | unsigned char | Aktiviert / deaktiviert die Solldruckvorgabe durch den Fahrer 0 = deaktiviert 1 = aktiviert |
| STAT_PREC_RESET_TEXT | string | Aktiviert / deaktiviert die Solldruckvorgabe durch den Fahrer 0 = deaktiviert 1 = aktiviert |
| STAT_RDC_WARN_DELAY | unsigned char | Aktiviert / deaktiviert die Verzoegerung einer Pannenwarnung 0 = deaktiviert 1 = aktiviert |
| STAT_RDC_WARN_DELAY_TEXT | string | Aktiviert / deaktiviert die Verzoegerung einer Pannenwarnung 0 = deaktiviert 1 = aktiviert |
| STAT_PREC_RESET_OFFSET | unsigned char | Aktiviert / deaktiviert die Toleranz der Befuellbombe 0 = deaktiviert 1 = aktiviert |
| STAT_PREC_RESET_OFFSET_TEXT | string | Aktiviert / deaktiviert die Toleranz der Befuellbombe 0 = deaktiviert 1 = aktiviert |
| STAT_T_REF_SHIFT_WERT | unsigned char | Temperaturkompensation 0 = maximale Kompensation 1 = keine Kompensation |
| STAT_T_REF_SHIFT_EINH | string | Temperaturkompensation 0 = maximale Kompensation 1 = keine Kompensation |
| STAT_UIA_TH_C_WERT | unsigned char | Temperaturkompensierte Warnschwelle (15 % - 20 %): 255 = ungueltiger Wert |
| STAT_UIA_TH_C_EINH | string | Temperaturkompensierte Warnschwelle (15 % - 20 %): 255 = ungueltiger Wert |
| STAT_UIW_TH_C_WERT | unsigned char | Temperaturkompensierte Vorwarnschwelle (10 % - 100 %): 255 = ungueltiger Wert |
| STAT_UIW_TH_C_EINH | string | Temperaturkompensierte Vorwarnschwelle (10 % - 100 %): 255 = ungueltiger Wert |
| STAT_UIA_TH_NC_WERT | unsigned char | Unkompensierte Warnschwelle (15 % - 50 %): 255 = ungueltiger Wert |
| STAT_UIA_TH_NC_EINH | string | Unkompensierte Warnschwelle (15 % - 50 %): 255 = ungueltiger Wert |
| STAT_UIW_TH_NC_WERT | unsigned char | Unkompensierte Vorwarnschwelle (10 % - 100 %): 255 = ungueltiger Wert |
| STAT_UIW_TH_NC_EINH | string | Unkompensierte Vorwarnschwelle (10 % - 100 %): 255 = ungueltiger Wert |
| STAT_P_DIST_PREWARN_MIN_WERT | real | Minimaler Abstand zwischen Vorwarnschwelle und Solldruck (0 bar - 0,5 bar): 255 = ungueltiger Wert |
| STAT_P_DIST_PREWARN_MIN_EINH | string | Minimaler Abstand zwischen Vorwarnschwelle und Solldruck (0 bar - 0,5 bar): 255 = ungueltiger Wert |
| STAT_MIN_RCP_FA_WERT | real | Mindestdruck fuer die Vorderachse (2,0 bar - 3,5 bar): 255 = ungueltiger Wert |
| STAT_MIN_RCP_FA_EINH | string | Mindestdruck fuer die Vorderachse (2,0 bar - 3,5 bar): 255 = ungueltiger Wert |
| STAT_MIN_RCP_RA_WERT | real | Mindestdruck fuer die Hinterachse (2,0 bar - 3,5 bar): 255 = ungueltiger Wert |
| STAT_MIN_RCP_RA_EINH | string | Mindestdruck fuer die Hinterachse (2,0 bar - 3,5 bar): 255 = ungueltiger Wert |
| STAT_DELTA_P_L_R_WERT | real | Maximale Druckdifferenz zwischen linker und rechter Seite (0,2 bar - 1,0 bar): 255 = ungueltiger Wert |
| STAT_DELTA_P_L_R_EINH | string | Maximale Druckdifferenz zwischen linker und rechter Seite (0,2 bar - 1 bar): 255 = ungueltiger Wert |
| STAT_P_INIT_RANGE_MAX_WERT | real | Maximale Druckdifferenz der Vorder- und Hinterachse zum Tankklappendruck (0,2 bar - 2,0 bar): 255 = ungueltiger Wert |
| STAT_P_INIT_RANGE_MAX_EINH | string | Maximale Druckdifferenz der Vorder- und Hinterachse zum Tankklappendruck (0,2 bar - 2,0 bar): 255 = ungueltiger Wert |
| STAT_TIMEOUT_PREWARN_WERT | unsigned char | Filterzeit zur Ausgabe einer Vorwarnung (2 min - 60 min): 255 = ungueltiger Wert |
| STAT_TIMEOUT_PREWARN_EINH | string | Filterzeit zur Ausgabe einer Vorwarnung (2 min - 60 min): 255 = ungueltiger Wert |
| STAT_DT_AMB_PREWARN_WERT | unsigned char | Temperaturdifferenz Reifen zu Aussentemperatur bei der die Vorwarnung deaktiviert wird (0 K - 254 K): 255 = ungueltiger Wert |
| STAT_DT_AMB_PREWARN_EINH | string | Temperaturdifferenz Reifen zu Aussentemperatur bei der die Vorwarnung deaktiviert wird (0 K - 254 K): 255 = ungueltiger Wert |
| STAT_C_DP_TOL_PMIN_WERT | real | Maximal zulaessige Abweichung vom Mindestdruck (0,1 bar - 0,4 bar): 255 = ungueltiger Wert |
| STAT_C_DP_TOL_PMIN_EINH | string | Maximal zulaessige Abweichung vom Mindestdruck (0,1 bar - 0,4 bar): 255 = ungueltiger Wert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (133 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (36 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (20 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (11 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (6 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [TAB_RDC_AKTIV_INAKTIV](#table-tab-rdc-aktiv-inaktiv) (3 × 2)
- [TAB_RDC_BANDMODE_ACTIVE](#table-tab-rdc-bandmode-active) (3 × 2)
- [TAB_RDC_BEKANNT_NICHT_BEKANNT](#table-tab-rdc-bekannt-nicht-bekannt) (3 × 2)
- [TAB_RDC_CAL_ACTIVE](#table-tab-rdc-cal-active) (3 × 2)
- [TAB_RDC_CHANGED](#table-tab-rdc-changed) (3 × 2)
- [TAB_RDC_CONFIRMED](#table-tab-rdc-confirmed) (3 × 2)
- [TAB_RDC_DETECTED](#table-tab-rdc-detected) (3 × 2)
- [TAB_RDC_DTC_ACTIVE](#table-tab-rdc-dtc-active) (3 × 2)
- [TAB_RDC_ENABLE_DISABLE](#table-tab-rdc-enable-disable) (3 × 2)
- [TAB_RDC_ON_OFF](#table-tab-rdc-on-off) (3 × 2)
- [TAB_RDC_RAD_DREHRICHTUNG](#table-tab-rdc-rad-drehrichtung) (5 × 2)
- [TAB_RDC_RAD_POSITION_NR](#table-tab-rdc-rad-position-nr) (9 × 2)
- [TAB_RDC_STARTED](#table-tab-rdc-started) (3 × 2)
- [TAB_RDC_STEUERFUNKTIONEN](#table-tab-rdc-steuerfunktionen) (9 × 2)
- [TAB_RDC_TIMEOUT](#table-tab-rdc-timeout) (3 × 2)
- [TAB_RDC_TPMS_MARKET](#table-tab-rdc-tpms-market) (3 × 2)
- [TAB_RDC_VEHICLE_RUNNING](#table-tab-rdc-vehicle-running) (3 × 2)
- [TAB_RE_HERSTELLER](#table-tab-re-hersteller) (7 × 2)
- [TAB_RE_ROLLSWITCH](#table-tab-re-rollswitch) (3 × 2)
- [TAB_RE_SENDEMODE](#table-tab-re-sendemode) (10 × 2)
- [TAB_RE_TELEGRAMMTYP](#table-tab-re-telegrammtyp) (5 × 2)

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

Dimensions: 133 rows × 2 columns

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
| 0xAF | Alfmeier |
| 0xB0 | ELTEK VALERE DEUTSCHLAND GMBH |
| 0xB1 | Omron Automotive Electronics Europe Group |
| 0xB2 | ASK |
| 0xB3 | CML Innovative Technologies GmbH & Co. KG |
| 0xB4 | APAG Elektronik AG |
| 0xB5 | Nexteer Automotive World Headquarters |
| 0xB6 | Hans Widmaier |
| 0xB7 | SB LiMotive Germany GmbH |
| 0xB8 | KYOCERA Display Corporation |
| 0xB9 | MAGNA Powertrain AG & Co KG |
| 0xBA | BorgWarner |
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

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 36 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| 00000000 | 000 | Steuergeraet defekt (Betriebsspannung) |
| 00000100 | 004 | Raderkennung nicht moeglich |
| 00000111 | 007 | Steuergeraet defekt (RAM-Fehler) |
| 00001001 | 009 | Steuergeraet defekt (EEPROM-Fehler) |
| 00001011 | 011 | Steuergeraet defekt (ROM-Fehler) |
| 00010000 | 016 | HF-Empfaenger defekt |
| 00010100 | 020 | Raderkennung nicht moeglich (zu viele RE) |
| 00011010 | 026 | Botschaft (KLEMMENSTATUS, 0x130) fehlt, Empfänger RDC, Sender CAS |
| 00011100 | 028 | Botschaft (A_TEMP, 0x2CA) fehlt, Empfänger RDC, Sender Kombi |
| 00011110 | 030 | Botschaft (KILOMETERSTAND, 0x330) fehlt, Empfänger RDC, Sender Kombi |
| 00011111 | 031 | K-CAN Control Module Bus OFF |
| 00100001 | 033 | Botschaft (ENGINE_1, 0x1D0) fehlt, Empfänger RDC, Sender DME1_DDE1 |
| 00100010 | 034 | K-CAN Bus |
| 00100100 | 036 | Botschaft (GESCHWINDIGKEIT, 0x1A0) fehlt, Empfänger RDC, Sender DSC_DXC |
| 00100110 | 038 | Botschaft (STAT_GANG_RUECKWAERTS, 0x3B0) fehlt, Empfänger RDC, Sender FRMFA |
| 00101000 | 040 | Botschaft (STAT_GANG, 0x304) fehlt, Empfänger RDC, Sender DKG |
| 00101010 | 042 | Unterspannung Kl.30 |
| 00101011 | 043 | Ueberspannung Kl.30 |
| 00101101 | 045 | Radelektronik vorne links defekt |
| 00101110 | 046 | Radelektronik vorne links kein Empfang |
| 00110000 | 048 | Radelektronik vorne rechts defekt |
| 00110001 | 049 | Radelektronik vorne rechts kein Empfang |
| 00110011 | 051 | Radelektronik hinten links defekt |
| 00110100 | 052 | Radelektronik hinten links kein Empfang |
| 00110110 | 054 | Radelektronik hinten rechts defekt |
| 00110111 | 055 | Radelektronik hinten rechts kein Empfang |
| 00111100 | 060 | Radelektronik (Position unbekannt) defekt |
| 00111101 | 061 | Radelektronik (Position unbekannt) kein Empfang |
| 01100101 | 101 | Funkverbindung durch Fremdeinfluss gestoert |
| 01111100 | 124 | RDC-Steuergeraet im Bandmodus |
| 10101100 | 172 | Radelektronik falsche Generation - Position unbekannt |
| 10101101 | 173 | Radelektronik nicht kompatibler Hersteller - Position unbekannt |
| 11111001 | 249 | Steuergerät ist nicht codiert |
| 11111010 | 250 | Steuergeraet ist nicht für das Fahrzeug codiert, in welchem es verbaut ist |
| 11111011 | 251 | Die waehrend einer Codierdaten Transaktion gesendeten Daten sind unplausibel |
| xxxxxxxx | 255 | -- |

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 20 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x604C | Bandmode aktiv |
| 0x604D | Fehler Steuergeraet |
| 0x604E | Fehler RDC-System |
| 0x6053 | Fehler Uebertragungskanal Ant |
| 0x6054 | Fehler Radsensor VL |
| 0x6055 | Fehler Radsensor VR |
| 0x6056 | Fehler Radsensor HL |
| 0x6057 | Fehler Radsensor HR |
| 0x6059 | Fehler Radsensor undefiniert |
| 0xD104 | Fehler CAN Eindrahtbetrieb |
| 0xD107 | Fehler CAN Bus Off |
| 0xD110 | Fehler CAN Telegramm Timeout KLEMMENSTATUS |
| 0xD111 | Fehler CAN Telegramm Timeout A_TEMP |
| 0xD112 | Fehler CAN Telegramm Timeout KILOMETERSTAND |
| 0xD113 | Fehler CAN Telegramm Timeout ENGINE_1 |
| 0xD114 | Fehler CAN Telegramm Timeout GESCHWINDIGKEIT |
| 0xD115 | Fehler CAN Telegramm Timeout STAT_GANG_RUECKWAERTS |
| 0xD116 | Fehler CAN Telegramm Timeout STAT_GANG |
| 0xD13E | Fehler CAN Telegramm Timeout beim Empfang |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 11 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xD104 | 0x04 | 0x03 | - | - |
| 0xD107 | 0x04 | 0x03 | - | - |
| 0xD110 | 0x04 | 0x03 | - | - |
| 0xD111 | 0x04 | 0x03 | - | - |
| 0xD112 | 0x04 | 0x03 | - | - |
| 0xD113 | 0x04 | 0x03 | - | - |
| 0xD114 | 0x04 | 0x03 | - | - |
| 0xD115 | 0x04 | 0x03 | - | - |
| 0xD116 | 0x04 | 0x03 | - | - |
| 0xD13E | 0x04 | 0x03 | - | - |
| default | 0x02 | 0x03 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 6 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | Kilometerstand | km | high | unsigned int | - | 8 | 1 | 0 |
| 0x0002 | Geschwindigkeit | km/h | high | unsigned int | - | 1 | 10 | 0 |
| 0x0003 | Temperatur | Grad C | - | unsigned char | - | 1 | 2 | -40 |
| 0x0004 | EmpfangsId | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0x0005 | SendeId | hex | high | unsigned int | - | 1 | 1 | 0 |
| 0xFFFF | ohne Bedeutung | 1 | high | unsigned int | - | 1 | 1 | 0 |

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

<a id="table-tab-rdc-aktiv-inaktiv"></a>
### TAB_RDC_AKTIV_INAKTIV

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | inaktiv |
| 1 | aktiv |
| 255 | Signal unbekannt |

<a id="table-tab-rdc-bandmode-active"></a>
### TAB_RDC_BANDMODE_ACTIVE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bandmode inaktiv |
| 1 | Bandmode aktiv |
| 255 | nicht definiert |

<a id="table-tab-rdc-bekannt-nicht-bekannt"></a>
### TAB_RDC_BEKANNT_NICHT_BEKANNT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht bekannt |
| 1 | bekannt |
| 255 | nicht definiert |

<a id="table-tab-rdc-cal-active"></a>
### TAB_RDC_CAL_ACTIVE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kalibrieranforderung inaktiv |
| 1 | Kalibrieranforderung aktiv |
| 255 | nicht definiert |

<a id="table-tab-rdc-changed"></a>
### TAB_RDC_CHANGED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht geändert |
| 1 | geändert |
| 255 | Signal unbekannt |

<a id="table-tab-rdc-confirmed"></a>
### TAB_RDC_CONFIRMED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht bestätigt |
| 1 | bestätigt |
| 255 | nicht definiert |

<a id="table-tab-rdc-detected"></a>
### TAB_RDC_DETECTED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht erkannt |
| 1 | erkannt |
| 255 | nicht definiert |

<a id="table-tab-rdc-dtc-active"></a>
### TAB_RDC_DTC_ACTIVE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | DTC inaktiv |
| 1 | DTC aktiv |
| 255 | nicht definiert |

<a id="table-tab-rdc-enable-disable"></a>
### TAB_RDC_ENABLE_DISABLE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | deaktiviert |
| 1 | aktiviert |
| 255 | nicht definiert |

<a id="table-tab-rdc-on-off"></a>
### TAB_RDC_ON_OFF

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | aus |
| 1 | ein |
| 255 | nicht definiert |

<a id="table-tab-rdc-rad-drehrichtung"></a>
### TAB_RDC_RAD_DREHRICHTUNG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Stillstand |
| 1 | rechts |
| 2 | links |
| 3 | unbekannt |
| 255 | nicht definiert |

<a id="table-tab-rdc-rad-position-nr"></a>
### TAB_RDC_RAD_POSITION_NR

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | vorne links |
| 1 | vorne rechts |
| 2 | hinten links |
| 3 | hinten rechts |
| 4 | unbekannt |
| 5 | unbekannt 1 |
| 6 | unbekannt 2 |
| 7 | unbekannt 3 |
| 8 | unbekannt 4 |

<a id="table-tab-rdc-started"></a>
### TAB_RDC_STARTED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht gestartet |
| 1 | gestartet |
| 255 | nciht definiert |

<a id="table-tab-rdc-steuerfunktionen"></a>
### TAB_RDC_STEUERFUNKTIONEN

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | BANDMODE |
| 2 | ER_FAHRT |
| 3 | ER_STAND (nur RDC Gen2) |
| 4 | TEST_ER_FAHRT |
| 5 | TEST_ER_STAND |
| 6 | RDCBUS_DIAG (nur RDC Gen2) |
| 7 | SOLLDRUCK_SCHREIBEN |
| 8 | CAL_REQUEST |
| 9 | ER_FAHRT_OHNE_TRIGGER (nur RDC Gen3) |

<a id="table-tab-rdc-timeout"></a>
### TAB_RDC_TIMEOUT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Timeout |
| 1 | Timeout |
| 255 | nicht definiert |

<a id="table-tab-rdc-tpms-market"></a>
### TAB_RDC_TPMS_MARKET

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | EU |
| 1 | US |
| 255 | nicht definiert |

<a id="table-tab-rdc-vehicle-running"></a>
### TAB_RDC_VEHICLE_RUNNING

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Fahrzeug steht |
| 1 | Fahrzeug fährt |
| 255 | nicht definiert |

<a id="table-tab-re-hersteller"></a>
### TAB_RE_HERSTELLER

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht bedient |
| 1 | Autonet |
| 2 | BERU |
| 3 | Conti |
| 4 | TRW |
| 5 | Schrader |
| 15 | Hersteller unbekannt |

<a id="table-tab-re-rollswitch"></a>
### TAB_RE_ROLLSWITCH

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Rollswitch nicht gesetzt |
| 1 | Rollswitch gesetzt |
| 16 | Rollswitch Toggle |

<a id="table-tab-re-sendemode"></a>
### TAB_RE_SENDEMODE

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Mode 0a/b |
| 1 | Mode 1a/b/c/d |
| 2 | Mode 2 |
| 3 | Mode 3 |
| 4 | Mode 4 |
| 8 | Mode 0a/b LF triggered telegram |
| 9 | Mode 1a/b/c/d LF triggered telegram |
| 10 | Mode 2 LF triggered telegram |
| 11 | Mode 3 LF triggered telegram |
| 12 | Mode 4 LF triggered telegram |

<a id="table-tab-re-telegrammtyp"></a>
### TAB_RE_TELEGRAMMTYP

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | AK35 default |
| 130 | BERU G3 only |
| 136 | AK35 BERU long |
| 160 | AK35 BERU medium |
| 193 | AK35 BERU short |
