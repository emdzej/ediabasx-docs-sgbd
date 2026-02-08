# ldm_60.prg

- Jobs: [83](#jobs)
- Tables: [37](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Längsdynamikmanager E60 |
| ORIGIN | BMW EF-62 Peller |
| REVISION | 1.526 |
| AUTHOR | ContiTemic CCElektronik Apelt, ContiTemic CCElektronik Beierlein, Bertrandt EE Postl, ContiTemic CCElektronik Fettes |
| COMMENT | N/A |
| PACKAGE | 1.36 |
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
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
- [HS_LESEN_DETAIL](#job-hs-lesen-detail) - Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default
- [HS_LOESCHEN](#job-hs-loeschen) - Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default
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
- [STATUS_BEDIENUNG_ACC](#job-status-bedienung-acc) - Auslesen der Botschaft Bedienung_Tempomat/ACC Signale beider Prozessoren KWP 2000: $21 ReadDataByLocalIdentifier $50 status_bedienung_acc
- [STATUS_HL_DIAGNOSE](#job-status-hl-diagnose) - Auslesen der HL-Diagnose KWP 2000: $21 ReadDataByLocalIdentifier $60 status_hl_diagnose
- [STEUERN_HL_DIAGNOSE](#job-steuern-hl-diagnose) - Vorgeben der HL-Diagnose KWP 2000: $3B WriteDataByLocalIdentifier $60 steuern_hl_diagnose
- [STATUS_COMPILER_MPC_URBOOT](#job-status-compiler-mpc-urboot) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des MPC-Urbootloader KWP 2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_COMPILER_MPC_LOWLEVEL_SW](#job-status-compiler-mpc-lowlevel-sw) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der MPC LL-SW KWP 2000: $21 ReadDataByLocalIdentifier $A1 status_compiler_mpc_lowlevel_sw
- [STATUS_COMPILER_MPC_HIGHLEVEL_SW](#job-status-compiler-mpc-highlevel-sw) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der MPC HL-SW KWP 2000: $21 ReadDataByLocalIdentifier $A2 status_compiler_mpc_highlevel_sw
- [STATUS_COMPILER_MPC_DAF](#job-status-compiler-mpc-daf) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des DAF KWP 2000: $21 ReadDataByLocalIdentifier $A3 status_compiler_mpc_daf
- [STATUS_COMPILER_STAR_URBOOT](#job-status-compiler-star-urboot) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des Star-Urbootloader KWP 2000: $21 ReadDataByLocalIdentifier $A5 status_compiler_star_urboot
- [STATUS_COMPILER_STAR_BOOT](#job-status-compiler-star-boot) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des Star-Bootloader KWP 2000: $21 ReadDataByLocalIdentifier $A6 status_compiler_star_boot
- [STATUS_COMPILER_STAR_LOWLEVEL_SW](#job-status-compiler-star-lowlevel-sw) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der Star LL-SW KWP 2000: $21 ReadDataByLocalIdentifier $A7 status_compiler_star_lowlevel_sw
- [STATUS_COMPILER_STAR_HIGHLEVEL_SW](#job-status-compiler-star-highlevel-sw) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der Star HL-SW KWP 2000: $21 ReadDataByLocalIdentifier $A8 status_compiler_star_highlevel_sw
- [STATUS_COMPILER_STAR_DAF](#job-status-compiler-star-daf) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des DAF KWP 2000: $21 ReadDataByLocalIdentifier $A9 status_compiler_star_daf
- [STEUERN_WERKSWINKEL_SRR_RECHTS](#job-steuern-werkswinkel-srr-rechts) - Werksdejustagewinkel beim Nachbereichsradar rechts eintragen KWP2000: $3B WriteDataByLocalIdentifier
- [STEUERN_WERKSWINKEL_SRR_LINKS](#job-steuern-werkswinkel-srr-links) - Werksdejustagewinkel beim Nachbereichsradar links eintragen KWP2000: $3B WriteDataByLocalIdentifier
- [STEUERN_FAHRWINKEL_SRR_RECHTS](#job-steuern-fahrwinkel-srr-rechts) - Fahrdejustagewinkel beim Nachbereichsradar rechts zurücksetzen KWP2000: $3B WriteDataByLocalIdentifier
- [STEUERN_FAHRWINKEL_SRR_LINKS](#job-steuern-fahrwinkel-srr-links) - Fahrdejustagewinkel beim Nachbereichsradar links zurücksetzen KWP2000: $3B WriteDataByLocalIdentifier
- [STATUS_WERKSWINKEL_SRR_RECHTS](#job-status-werkswinkel-srr-rechts) - Werksdejustagewinkel beim Nachbereichsradar rechts auslesen KWP2000: $21 ReadDataByLocalIdentifier
- [STATUS_WERKSWINKEL_SRR_LINKS](#job-status-werkswinkel-srr-links) - Werksdejustagewinkel beim Nachbereichsradar links auslesen KWP2000: $21 ReadDataByLocalIdentifier
- [STATUS_FAHRWINKEL_SRR_RECHTS](#job-status-fahrwinkel-srr-rechts) - Fahrdejustagewinkel beim Nachbereichsradar rechts auslesen KWP2000: $21 ReadDataByLocalIdentifier
- [STATUS_FAHRWINKEL_SRR_LINKS](#job-status-fahrwinkel-srr-links) - Fahrdejustagewinkel beim Nachbereichsradar links auslesen KWP2000: $21 ReadDataByLocalIdentifier
- [STATUS_JUSTAGE_SRR_RECHTS](#job-status-justage-srr-rechts) - Justagewinkel beim Nachbereichsradar rechts auslesen KWP2000: $21 ReadDataByLocalIdentifier
- [STATUS_JUSTAGE_SRR_LINKS](#job-status-justage-srr-links) - Justagewinkel beim Nachbereichsradar links auslesen KWP2000: $21 ReadDataByLocalIdentifier
- [STATUS_HW_NUMMER_SRR_RECHTS](#job-status-hw-nummer-srr-rechts) - Hardwarenummer Nachbereichsradar rechts auslesen KWP2000: $22 ReadDataByCommonIdentifier
- [STATUS_HW_NUMMER_SRR_LINKS](#job-status-hw-nummer-srr-links) - Hardwarenummer Nachbereichsradar links auslesen KWP2000: $22 ReadDataByCommonIdentifier
- [LERNDATEN_LESEN](#job-lerndaten-lesen) - Job um alle Lerndaten auszulesen KWP2000: $21 ReadDataByLocalIdentifier $14 Alle Lerndaten ausgeben
- [STATUS_AKTUELLE_DATEN](#job-status-aktuelle-daten) - Auslesen der aktuellen Statistikdaten Signale beider Prozessoren KWP 2000: $21 ReadDataByLocalIdentifier $40 status_aktuelle_daten
- [STATUS_PROTOKOLLDATEN](#job-status-protokolldaten) - Auslesen der Protokolldaten aus den Statistikdaten Signale beider Prozessoren KWP 2000: $21 ReadDataByLocalIdentifier $41 status_aktuelle_daten
- [STEUERN_RESET_DEJU_DATA_FUS](#job-steuern-reset-deju-data-fus) - Rücksetzen der DEJU Daten der Fusion KWP 2000: $3B WriteDataByLocalIdentifier $60 steuern_hl_diagnose

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

<a id="job-status-bedienung-acc"></a>
### STATUS_BEDIENUNG_ACC

Auslesen der Botschaft Bedienung_Tempomat/ACC Signale beider Prozessoren KWP 2000: $21 ReadDataByLocalIdentifier $50 status_bedienung_acc

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TASTER_TEMPOMAT_ACC | int | Empfangssignal Bedienung_Taster_Tempomat_ACC Signal OP_PUBU_CCTR_ACC 1 -&gt; Keine Aktion 2 -&gt; Tippen nach Vorne 3 -&gt; Überdrücken nach Vorne 4 -&gt; Tippen nach Hinten 5 -&gt; Überdrücken nach Hinten 6 -&gt; Tippen nach Unten 7 -&gt; Axial Tippen 8 -&gt; Tippen nach oben 9 -&gt; Signal ungültig 99 -&gt; nicht definiert |
| STAT_TASTER_TEMPOMAT_ACC_TEXT | string | Empfangssignal Bedienung_Taster_Tempomat_ACC Signal OP_PUBU_CCTR_ACC |
| STAT_ABSTANDSWAHL_ACC | int | Empfangssignal Bedienung_Abstandswahl_ACC Signal OP_GAPC_ACC 1 -&gt; Keine Aktion 2 -&gt; Tippen nach oben 3 -&gt; Tippen nach unten 4 -&gt; Signal ungültig 99 -&gt; nicht definiert |
| STAT_ABSTANDSWAHL_ACC_TEXT | string | Empfangssignal Bedienung_Abstandswahl_ACC Signal OP_GAPC_ACC |
| STAT_EMPFANGSBOTSCHAFT | int | Status der Botschaftsüberwachung für Bedienung_Tempomat/ACC Es handelt sich hierbei um ein Bitfeld, hier die Bedeutung der einzelnen Bits 0x01 -&gt; Timeoutfehler 0x02 -&gt; Signal ungültig 0x04 -&gt; Checksummenfehler 0x08 -&gt; Alivezählerfehler 0x10 -&gt; Signal undefiniert 0x20 -&gt; Initialisierungsfehler 0x40 -&gt; Signal irrelevant |
| STAT_EMPFANGSBOTSCHAFT_TEXT | string | Status der Botschaftsüberwachung für Bedienung_Tempomat/ACC |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hl-diagnose"></a>
### STATUS_HL_DIAGNOSE

Auslesen der HL-Diagnose KWP 2000: $21 ReadDataByLocalIdentifier $60 status_hl_diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HL_DIAGNOSE_HR | binary | Diagnose-Daten der Highlevel-SW vom HR |
| STAT_HL_DIAGNOSE_UR | binary | Diagnose-Daten der Highlevel-SW vom UR |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hl-diagnose"></a>
### STEUERN_HL_DIAGNOSE

Vorgeben der HL-Diagnose KWP 2000: $3B WriteDataByLocalIdentifier $60 steuern_hl_diagnose

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_DATA_1 | char | Diagnosedaten für die Highlevel-SW |
| DIAG_DATA_2 | char | Diagnosedaten für die Highlevel-SW |
| DIAG_DATA_3 | char | Diagnosedaten für die Highlevel-SW |
| DIAG_DATA_4 | char | Diagnosedaten für die Highlevel-SW |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-compiler-mpc-urboot"></a>
### STATUS_COMPILER_MPC_URBOOT

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des MPC-Urbootloader KWP 2000: $21 ReadDataByLocalIdentifier Modus  : Default

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

<a id="job-status-compiler-mpc-lowlevel-sw"></a>
### STATUS_COMPILER_MPC_LOWLEVEL_SW

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der MPC LL-SW KWP 2000: $21 ReadDataByLocalIdentifier $A1 status_compiler_mpc_lowlevel_sw

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

<a id="job-status-compiler-mpc-highlevel-sw"></a>
### STATUS_COMPILER_MPC_HIGHLEVEL_SW

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der MPC HL-SW KWP 2000: $21 ReadDataByLocalIdentifier $A2 status_compiler_mpc_highlevel_sw

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

<a id="job-status-compiler-mpc-daf"></a>
### STATUS_COMPILER_MPC_DAF

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des DAF KWP 2000: $21 ReadDataByLocalIdentifier $A3 status_compiler_mpc_daf

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

<a id="job-status-compiler-star-urboot"></a>
### STATUS_COMPILER_STAR_URBOOT

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des Star-Urbootloader KWP 2000: $21 ReadDataByLocalIdentifier $A5 status_compiler_star_urboot

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

<a id="job-status-compiler-star-boot"></a>
### STATUS_COMPILER_STAR_BOOT

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des Star-Bootloader KWP 2000: $21 ReadDataByLocalIdentifier $A6 status_compiler_star_boot

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

<a id="job-status-compiler-star-lowlevel-sw"></a>
### STATUS_COMPILER_STAR_LOWLEVEL_SW

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der Star LL-SW KWP 2000: $21 ReadDataByLocalIdentifier $A7 status_compiler_star_lowlevel_sw

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

<a id="job-status-compiler-star-highlevel-sw"></a>
### STATUS_COMPILER_STAR_HIGHLEVEL_SW

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der Star HL-SW KWP 2000: $21 ReadDataByLocalIdentifier $A8 status_compiler_star_highlevel_sw

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

<a id="job-status-compiler-star-daf"></a>
### STATUS_COMPILER_STAR_DAF

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des DAF KWP 2000: $21 ReadDataByLocalIdentifier $A9 status_compiler_star_daf

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

<a id="job-steuern-werkswinkel-srr-rechts"></a>
### STEUERN_WERKSWINKEL_SRR_RECHTS

Werksdejustagewinkel beim Nachbereichsradar rechts eintragen KWP2000: $3B WriteDataByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERKSWINKEL | real | Werksdejustagewinkel (Aufloesung 0.2 Grad) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-werkswinkel-srr-links"></a>
### STEUERN_WERKSWINKEL_SRR_LINKS

Werksdejustagewinkel beim Nachbereichsradar links eintragen KWP2000: $3B WriteDataByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERKSWINKEL | real | Werksdejustagewinkel (Aufloesung 0.2 Grad) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fahrwinkel-srr-rechts"></a>
### STEUERN_FAHRWINKEL_SRR_RECHTS

Fahrdejustagewinkel beim Nachbereichsradar rechts zurücksetzen KWP2000: $3B WriteDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fahrwinkel-srr-links"></a>
### STEUERN_FAHRWINKEL_SRR_LINKS

Fahrdejustagewinkel beim Nachbereichsradar links zurücksetzen KWP2000: $3B WriteDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-werkswinkel-srr-rechts"></a>
### STATUS_WERKSWINKEL_SRR_RECHTS

Werksdejustagewinkel beim Nachbereichsradar rechts auslesen KWP2000: $21 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WERKSWINKEL | real | Werksdejustagewinkel |
| STAT_WERKSWINKEL_EINH | string | Werksdejustagewinkel Einheit: Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-werkswinkel-srr-links"></a>
### STATUS_WERKSWINKEL_SRR_LINKS

Werksdejustagewinkel beim Nachbereichsradar links auslesen KWP2000: $21 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WERKSWINKEL | real | Werksdejustagewinkel |
| STAT_WERKSWINKEL_EINH | string | Werksdejustagewinkel Einheit: Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrwinkel-srr-rechts"></a>
### STATUS_FAHRWINKEL_SRR_RECHTS

Fahrdejustagewinkel beim Nachbereichsradar rechts auslesen KWP2000: $21 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAHRWINKEL | real | Fahrdejustagewinkel |
| STAT_FAHRWINKEL_EINH | string | Fahrdejustagewinkel Einheit: Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrwinkel-srr-links"></a>
### STATUS_FAHRWINKEL_SRR_LINKS

Fahrdejustagewinkel beim Nachbereichsradar links auslesen KWP2000: $21 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAHRWINKEL | real | Fahrdejustagewinkel |
| STAT_FAHRWINKEL_EINH | string | Fahrdejustagewinkel Einheit: Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-justage-srr-rechts"></a>
### STATUS_JUSTAGE_SRR_RECHTS

Justagewinkel beim Nachbereichsradar rechts auslesen KWP2000: $21 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WINKEL | real | Ausrichtung Detektion Winkel |
| STAT_WINKEL_EINH | string | Ausrichtung Detektion Winkel Einheit: Grad |
| STAT_ABSTAND | real | Ausrichtung Detektion Abstand |
| STAT_ABSTAND_EINH | string | Ausrichtung Detektion Abstand Einheit: Meter |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-justage-srr-links"></a>
### STATUS_JUSTAGE_SRR_LINKS

Justagewinkel beim Nachbereichsradar links auslesen KWP2000: $21 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WINKEL | real | Ausrichtung Detektion Winkel |
| STAT_WINKEL_EINH | string | Ausrichtung Detektion Winkel Einheit: Grad |
| STAT_ABSTAND | real | Ausrichtung Detektion Abstand |
| STAT_ABSTAND_EINH | string | Ausrichtung Detektion Abstand Einheit: Meter |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hw-nummer-srr-rechts"></a>
### STATUS_HW_NUMMER_SRR_RECHTS

Hardwarenummer Nachbereichsradar rechts auslesen KWP2000: $22 ReadDataByCommonIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HW_NUMMER_SRR_RECHTS | unsigned int | Hardwarenummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | string | Hex-Antwort von SG |

<a id="job-status-hw-nummer-srr-links"></a>
### STATUS_HW_NUMMER_SRR_LINKS

Hardwarenummer Nachbereichsradar links auslesen KWP2000: $22 ReadDataByCommonIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HW_NUMMER_SRR_LINKS | unsigned int | Hardwarenummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lerndaten-lesen"></a>
### LERNDATEN_LESEN

Job um alle Lerndaten auszulesen KWP2000: $21 ReadDataByLocalIdentifier $14 Alle Lerndaten ausgeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| FUS_N_MIS_ANGLE_LEFT_SRR | long | Zaehler Dejustagezustand SRR links |
| FUS_N_MIS_ANGLE_RIGHT_SRR | long | Zaehler Dejustagezustand SRR rechts |
| FUS_N_MIS_ANGLE_LRR | long | Zaehler Dejustagezustand LRR |
| FUS_MIS_ANGLE_LEFT_SRR_PT1 | real | Dejustagewinkel SRR links |
| FUS_MIS_ANGLE_RIGHT_SRR_PT1 | real | Dejustagewinkel SRR rechts |
| LERNDATEN | binary | Alle Lerndaten |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktuelle-daten"></a>
### STATUS_AKTUELLE_DATEN

Auslesen der aktuellen Statistikdaten Signale beider Prozessoren KWP 2000: $21 ReadDataByLocalIdentifier $40 status_aktuelle_daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| STAT_GESAMTKILOMETER_FAHRZEUG_0 | long | Übernahme der Wegstrecke vom Kombi km Einheit km |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_BREMSPEDAL_0 | long | Deaktivierung von ACC wegen Bremseingiff Fahrer Einheit Count |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_BEDIENUNG_0 | long | Deaktivierung von ACC durch Betätigung Lenkstockhebel/Taste OFF, Handbremse, Ausstiegsabsicht, KL15off, Gangwahl Einheit Count |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_REGELFUNKTION_0 | long | Deaktivierung von ACC durch Eingreifen einer Fahrwerkregelfunktion (GPS, ABS, DSC) Einheit Count |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_BLIND_0 | long | Deaktivierung wegen Blindheit von Radarsensoren Einheit Count |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_V_SCHWELLE_0 | long | Deaktivierung von ACC-30plus durch Unterschreiten der unteren ACCGeschwindigkeitsschwelle Einheit Count |
| STAT_ANZAHL_DEAKTIVIERUNG_DCC_0 | long | Zählung anderer Deaktivierungen (Fehler, Überwachung-Sicherheit) Einheit Count |
| STAT_ANZAHL_AKTIVIERUNG_ACC_RESUME_0 | long | Aktivierung von ACC durch Betätigen Resume Einheit Count |
| STAT_ANZAHL_AKTIVIERUNG_ACC_SETZEN_0 | long | Aktivierung von ACC durch Setzen Wunschgeschwindigkeit Einheit Count |
| STAT_ANZAHL_UEBERTRETEN_ACC_0 | long | Zählung von Fahrten über der aktivierten Wuschgeschwindigkeit Einheit Count |
| STAT_GESAMTDAUER_UEBERTRETEN_ACC_0 | long | Betriebszeit von Fahrten über der aktivierten Wuschgeschwindigkeit Einheit s |
| STAT_BETRIEBSZEIT_DCC_0 | long | Betriebszeit im DCC-Mode Einheit s |
| STAT_WUNSCHGESCHWINDIGKEIT_ACC_INTEGRAL_ABSTAND_1_0 | long | Zur Erfassung der Durchschnitts-Wunschgeschwindigkeit 1 Einheit m |
| STAT_WUNSCHGESCHWINDIGKEIT_ACC_INTEGRAL_ABSTAND_2_0 | long | Zur Erfassung der Durchschnitts-Wunschgeschwindigkeit 2 Einheit m |
| STAT_WUNSCHGESCHWINDIGKEIT_ACC_INTEGRAL_ABSTAND_3_0 | long | Zur Erfassung der Durchschnitts-Wunschgeschwindigkeit 3 Einheit m |
| STAT_WUNSCHGESCHWINDIGKEIT_ACC_INTEGRAL_ABSTAND_4_0 | long | Zur Erfassung der Durchschnitts-Wunschgeschwindigkeit 4 Einheit m |
| STAT_BETRIEBSZEIT_ACC_ABSTANDSSTUFE_1_0 | long | ACC Betriebszeit bei Abstand 1 Einheit s |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ABSTAND_1_0 | long | Zählung der Übernahmeaufforderungen bei Abstand 1 Einheit Count |
| STAT_BETRIEBSZEIT_ACC_ABSTANDSSTUFE_2_0 | long | ACC Betriebszeit bei Abstand 2 Einheit s |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ABSTAND_2_0 | long | Zählung der Übernahmeaufforderungen bei Abstand 2 Einheit Count |
| STAT_BETRIEBSZEIT_ACC_ABSTANDSSTUFE_3_0 | long | ACC Betriebszeit bei Abstand 3 Einheit s |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ABSTAND_3_0 | long | Zählung der Übernahmeaufforderungen bei Abstand 3 Einheit Count |
| STAT_BETRIEBSZEIT_ACC_ABSTANDSSTUFE_4_0 | long | ACC Betriebszeit bei Abstand 4 Einheit s |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ABSTAND_4_0 | long | Zählung der Übernahmeaufforderungen bei Abstand 4 Einheit Count |
| STAT_RELATIVER_KILOMETERZAEHLER_0 | unsigned int | Zählung der (positiven) Änderungen des KM-Stands. Wert ist gleich dem Fzg-KM-Stand solange LDM07 nicht geflashed oder getauscht. Einheit 2 km |
| STAT_GESAMTBETRIEBSZEIT_FAHRZEUG_0 | long | KL15 Bertiebszeit Einheit s |
| STAT_GESAMTBETRIEBSZEIT_ACC_0 | long | ACC Betriebszeit Einheit s |
| STAT_GESAMTBETRIEBSZEIT_DCC_0 | long | DCC Betriebszeit Einheit s |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_GESAMT_0 | long | Zählung der Abschaltungen (ist gleich der Aktivierungen) Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHABSTAND_ACC_0 | long | Häufigkeit der Änderung des Wunschabstands (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHGESCHWINDIGKEIT_ACC_0 | long | Häufigkeit der Änderung der Wunschgeschwindigkeit (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ACC_GESAMT_0 | long | Zählung der Übernahmeaufforderungen Einheit Count |
| STAT_ANZAHL_VORBEFUELLUNGEN | unsigned int | Zählung der Vorbefüllungen Einheit Count |
| STAT_ANZAHL_AUSLOESUNGEN_STANDARD_DBC | unsigned int | Zählung der Standardauslösungen Einheit Count |
| STAT_ANZAHL_AUSLOESUNGEN_1_DBC | unsigned int | Zählung der Auslösungen DBC Stufe 1 Einheit Count |
| STAT_ANZAHL_AUSLOESUNGEN_2_DBC | unsigned int | Zählung der Auslösungen DBC Stufe 2 Einheit Count |
| STAT_ANZAHL_AUSLOESUNGEN_3_DBC | unsigned int | Zählung der Auslösungen DBC Stufe 3 Einheit Count |
| STAT_DAUER_AUSLOESUNGEN_DBC_1_3 | long | Dauer der DBC-Auslösungen in den Stufen 1 bis 3 Einheit s |
| STAT_DAUER_VORBEFUELLUNGEN | long | Dauer der Vorbefüllungen Einheit s |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-protokolldaten"></a>
### STATUS_PROTOKOLLDATEN

Auslesen der Protokolldaten aus den Statistikdaten Signale beider Prozessoren KWP 2000: $21 ReadDataByLocalIdentifier $41 status_aktuelle_daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| STAT_RELATIVER_KILOMETERZAEHLER_1 | unsigned int | Zählung der (positiven) Änderungen des KM-Stands. P1 Wert ist gleich dem Fzg-KM-Stand solange LDM07 nicht geflashed oder getauscht. Einheit  2 km |
| STAT_GESAMTBETRIEBSZEIT_FAHRZEUG_1 | long | KL15 Betriebszeit P1 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_ACC_1 | long | ACC Betriebszeit P1 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_DCC_1 | long | DCC Betriebszeit P1 Einheit s |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_GESAMT_1 | long | Zählung der Abschaltungen (ist gleich der Aktivierungen) P1 Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHABSTAND_ACC_1 | long | Häufigkeit der Änderung des Wunschabstands P1 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHGESCHWINDIGKEIT_ACC_1 | long | Häufigkeit der Änderung der Wunschgeschwindigkeit P1 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ACC_GESAMT_1 | long | Zählung der Übernahmeaufforderungen P1 Einheit Count |
| STAT_RELATIVER_KILOMETERZAEHLER_2 | unsigned int | Zählung der (positiven) Änderungen des KM-Stands. P2 Wert ist gleich dem Fzg-KM-Stand solange LDM07 nicht geflashed oder getauscht. Einheit 2 km |
| STAT_GESAMTBETRIEBSZEIT_FAHRZEUG_2 | long | KL15 Betriebszeit P2 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_ACC_2 | long | ACC Betriebszeit P2 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_DCC_2 | long | DCC Betriebszeit P2 Einheit s |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_GESAMT_2 | long | Zählung der Abschaltungen (ist gleich der Aktivierungen) P2 Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHABSTAND_ACC_2 | long | Häufigkeit der Änderung des Wunschabstands P2 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHGESCHWINDIGKEIT_ACC_2 | long | Häufigkeit der Änderung der Wunschgeschwindigkeit P2 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ACC_GESAMT_2 | long | Zählung der Übernahmeaufforderungen P2 Einheit Count |
| STAT_RELATIVER_KILOMETERZAEHLER_3 | unsigned int | Zählung der (positiven) Änderungen des KM-Stands. P3 Wert ist gleich dem Fzg-KM-Stand solange LDM07 nicht geflashed oder getauscht. Einheit 2 km |
| STAT_GESAMTBETRIEBSZEIT_FAHRZEUG_3 | long | KL15 Betriebszeit P3 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_ACC_3 | long | ACC Betriebszeit P3 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_DCC_3 | long | Betriebszeit DCC P3 Einheit s |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_GESAMT_3 | long | Zählung der Abschaltungen (ist gleich der Aktivierungen) P3 Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHABSTAND_ACC_3 | long | Häufigkeit der Änderung des Wunschabstands P3 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHGESCHWINDIGKEIT_ACC_3 | long | Häufigkeit der Änderung der Wunschgeschwindigkeit P3 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ACC_GESAMT_3 | long | Zählung der Übernahmeaufforderungen P3 Einheit Count |
| STAT_RELATIVER_KILOMETERZAEHLER_4 | unsigned int | Zählung der (positiven) Änderungen des KM-Stands. P4 Wert ist gleich dem Fzg-KM-Stand solange LDM07 nicht geflashed oder getauscht. Einheit 2 km |
| STAT_GESAMTBETRIEBSZEIT_FAHRZEUG_4 | long | KL15 Betriebszeit P4 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_ACC_4 | long | ACC Betriebszeit P4 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_DCC_4 | long | DCC Betriebszeit P4 Einheit s |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_GESAMT_4 | long | Zählung der Abschaltungen (ist gleich der Aktivierungen) P4 Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHABSTAND_ACC_4 | long | Häufigkeit der Änderung des Wunschabstands P4 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHGESCHWINDIGKEIT_ACC_4 | long | Häufigkeit der Änderung der Wunschgeschwindigkeit P4 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ACC_GESAMT_4 | long | Zählung der Übernahmeaufforderungen P4 Einheit Count |
| STAT_RELATIVER_KILOMETERZAEHLER_5 | unsigned int | Zählung der (positiven) Änderungen des KM-Stands. P5 Wert ist gleich dem Fzg-KM-Stand solange LDM07 nicht geflashed oder getauscht. Einheit 2 km |
| STAT_GESAMTBETRIEBSZEIT_FAHRZEUG_5 | long | KL15 Bertiebszeit P5 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_ACC_5 | long | ACC Betriebszeit P5 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_DCC_5 | long | DCC Betriebszeit P5 Einheit s |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_GESAMT_5 | long | Zählung der Abschaltungen (ist gleich der Aktivierungen) P5 Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHABSTAND_ACC_5 | long | Häufigkeit der Änderung des Wunschabstands P5 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHGESCHWINDIGKEIT_ACC_5 | long | Häufigkeit der Änderung der Wunschgeschwindigkeit P5 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ACC_GESAMT_5 | long | Zählung der Übernahmeanforderungen P5 Einheit Count |
| STAT_RELATIVER_KILOMETERZAEHLER_6 | unsigned int | Zählung der (positiven) Änderungen des KM-Stands. P6 Wert ist gleich dem Fzg-KM-Stand solange LDM07 nicht geflashed oder getauscht. Einheit 2 km |
| STAT_GESAMTBETRIEBSZEIT_FAHRZEUG_6 | long | KL15 Bertiebszeit P6 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_ACC_6 | long | ACC Betriebszeit P6 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_DCC_6 | long | DCC Betriebszeit P6 Einheit s |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_GESAMT_6 | long | Zählung der Abschaltungen (ist gleich der Aktivierungen) P6 Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHABSTAND_ACC_6 | long | Häufigkeit der Änderung des Wunschabstands P6 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHGESCHWINDIGKEIT_ACC_6 | long | Häufigkeit der Änderung der Wunschgeschwindigkeit P6 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ACC_GESAMT_6 | long | Zählung der Übernahmeanforderungen P6 Einheit Count |
| STAT_RELATIVER_KILOMETERZAEHLER_7 | unsigned int | Zählung der (positiven) Änderungen des KM-Stands. P7 Wert ist gleich dem Fzg-KM-Stand solange LDM07 nicht geflashed oder getauscht. Einheit 2 km |
| STAT_GESAMTBETRIEBSZEIT_FAHRZEUG_7 | long | KL15 Bertiebszeit P7 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_ACC_7 | long | ACC Betriebszeit P7 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_DCC_7 | long | DCC Betriebszeit P7 Einheit s |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_GESAMT_7 | long | Zählung der Abschaltungen (ist gleich der Aktivierungen) P7 Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHABSTAND_ACC_7 | long | Häufigkeit der Änderung des Wunschabstands P7 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHGESCHWINDIGKEIT_ACC_7 | long | Häufigkeit der Änderung der Wunschgeschwindigkeit P7 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ACC_GESAMT_7 | long | Zählung der Übernahmeaufforderungen P7 Einheit Count |
| STAT_RELATIVER_KILOMETERZAEHLER_8 | unsigned int | Zählung der (positiven) Änderungen des KM-Stands. P8 Wert ist gleich dem Fzg-KM-Stand solange LDM07 nicht geflashed oder getauscht. Einheit 2 km |
| STAT_GESAMTBETRIEBSZEIT_FAHRZEUG_8 | long | KL15 Bertiebszeit P8 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_ACC_8 | long | ACC Betriebszeit P8 Einheit s |
| STAT_GESAMTBETRIEBSZEIT_DCC_8 | long | DCC Betriebszeit P8 Einheit s |
| STAT_ANZAHL_DEAKTIVIERUNG_ACC_GESAMT_8 | long | Zählung der Abschaltungen (ist gleich der Aktivierungen) P8 Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHABSTAND_ACC_8 | long | Häufigkeit der Änderung des Wunschabstands P8 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_AENDERUNG_WUNSCHGESCHWINDIGKEIT_ACC_8 | long | Häufigkeit der Änderung der Wunschgeschwindigkeit P8 (wenn keine weitere Änderung in 10s verzögert) Einheit Count |
| STAT_ANZAHL_UEBERNAHMEAUFFORDERUNG_ACC_GESAMT_8 | long | Zählung der Übernahmeaufforderungen P8 Einheit Count |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-reset-deju-data-fus"></a>
### STEUERN_RESET_DEJU_DATA_FUS

Rücksetzen der DEJU Daten der Fusion KWP 2000: $3B WriteDataByLocalIdentifier $60 steuern_hl_diagnose

_No arguments._

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
- [LIEFERANTEN](#table-lieferanten) (100 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [HARTTEXTE](#table-harttexte) (14 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (45 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (120 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (7 × 9)
- [HORTTEXTE](#table-horttexte) (180 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HUMWELTMATRIX](#table-humweltmatrix) (1 × 5)
- [HUMWELTTEXTE](#table-humwelttexte) (7 × 9)
- [IORTTEXTE](#table-iorttexte) (172 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (110 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (14 × 9)
- [JOBRESULTECUSTATE](#table-jobresultecustate) (7 × 2)
- [UMBED1](#table-umbed1) (1 × 3)
- [UMBED2](#table-umbed2) (1 × 3)
- [UMBED3](#table-umbed3) (1 × 3)
- [TEMP_ACC_TASTER](#table-temp-acc-taster) (10 × 3)
- [STAT_BOTSCHAFT](#table-stat-botschaft) (9 × 2)
- [TEMP_ACC_ABSTANDSWAHL](#table-temp-acc-abstandswahl) (5 × 3)
- [NAHBEREICHSRADAR](#table-nahbereichsradar) (2 × 2)
- [UMBEDISP](#table-umbedisp) (1 × 3)

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

Dimensions: 100 rows × 2 columns

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

Dimensions: 45 rows × 3 columns

| ORT | ORTTEXT | LIN_2_FORMAT |
| --- | --- | --- |
| 0x0100 | Batteriesensor | - |
| 0x0200 | Elektrische Wasserpumpe | - |
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
| 0x0F00 | Rearview Kamera hinten | - |
| 0x1000 | Topview Kamera Außenspiegel links | - |
| 0x1100 | Topview Kamera Außenspiegel rechts | - |
| 0x1200 | Sideview Kamera Stoßfänger vorne links | - |
| 0x1300 | Sideview Kamera Stoßfänger vorne rechts | - |
| 0x1400 | Wischermotor | 1 |
| 0x1500 | Regen- Lichtsensor | 1 |
| 0x1600 | Innenspiegel | 1 |
| 0x1700 | Garagentoröffner | 1 |
| 0x1800 | AUC-Sensor | 1 |
| 0x1900 | Druck- Temperatursensor | 1 |
| 0x1A00 | Schalterblock Sitzheizung hinten | 1 |
| 0x1B00 | Schalterblock Sitzmemory/-massage Fahrer | 1 |
| 0x1C00 | Schalterblock Sitzmemory/-massage Beifahrer | 1 |
| 0x1D00 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x1E00 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x1F00 | KAFAS Kamera | 1 |
| 0x2000 | Automatische Anhängevorrichtung | 1 |
| 0x2100 | SINE | 1 |
| 0x2200 | Funkempfänger | 1 |
| 0x2300 | Funkempfänger 2 | 1 |
| 0x2400 | Türgriffelektronik Fahrer | - |
| 0x2500 | Türgriffelektronik Beifahrer | - |
| 0x2600 | Türgriffelektronik Fahrer hinten | - |
| 0x2700 | Türgriffelektronik Beifahrer hinten | - |
| 0x2800 | Telestart-Handsender 1 | - |
| 0x2900 | Telestart-Handsender 2 | - |
| 0x2A00 | RSE-Fernbedienung | - |
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

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| 1 | BMW-FAST |
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 120 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x62CC | 0x62CC - Steuergerätefehler |
| 0x62CD | 0x62CD - Codierdatenfehler |
| 0x62CE | 0x62CE - Überspannungsfehler |
| 0x62CF | 0x62CF - Unterspannungsfehler |
| 0x62D0 | 0x62D0 - Abschaltung Bremsenüberhitzung |
| 0x62D1 | 0x62D1 - Sicherheitsabschaltung durch den Hauptrechner |
| 0x62D2 | 0x62D2 - Plausibilität  Fahrpedal getreten  |
| 0x62D3 | 0x62D3 - V_DSC und V_ANZ unplausibel |
| 0x62D4 | 0x62D4 - Abschaltung durch Motorsteuergerät |
| 0x62D5 | 0x62D5 - Stillstandsmanagement |
| 0x62D6 | 0x62D6 - Abschaltung durch Bremsensteuergerät |
| 0x62D7 | 0x62D7 - OBR Offset Gierrate |
| 0x62D8 | 0x62D8 - Abschaltung durch Kombi |
| 0x62D9 | 0x62D9 - Plausibilität Sitzbelegung Fahrersitz |
| 0x62DA | 0x62DA - Harte Abschaltung Antrieb |
| 0x62DB | 0x62DB - Harte Abschaltung Bremse |
| 0x62DC | 0x62DC - Weckleitungsfehler |
| 0x62DD | 0x62DD - Plausibilität Bremspedal |
| 0x62DE | 0x62DE - Sicherheitsabschaltung PT-CAN |
| 0x62DF | 0x62DF - Steuergerät Aufstartfehler |
| 0x62E0 | 0x62E0 - SRR-R Störung durch Fremdeinwirkung |
| 0x62E1 | 0x62E1 - SRR-L Störung durch Fremdeinwirkung |
| 0x62E2 | 0x62E2 - NVC-Modul Zustand |
| 0x62E3 | 0x62E3 - iBreak-Modul Zustand |
| 0x62E4 | 0x62E4 - Harte Abschaltung Rucküberwachung |
| 0x62E6 | 0x62E6 - Zustand Fahrpedal Signale |
| 0x62E7 | 0x62E7 - Zustand Gierraten Signal |
| 0x62E8 | 0x62E8 - Ungültige oder falsche Fahrgestellnummer |
| 0x62E9 | 0x62E9 - Undokumentierte Fehlerabschaltung |
| 0x62EA | 0x62EA - Vorwarnung Beschleunigungsüberwachung |
| 0x62EB | 0x62EB - Vorwarnung Verzögerungsüberwachung |
| 0x63AC | 0x63AC - Plausibilität KOMBI Signal ungültig |
| 0x63AD | 0x63AD - Plausibilität Beschleunigungssensoren |
| 0x63AE | 0x63AE - Harte Abschaltung durch den UR |
| 0x63AF | 0x63AF - Sicherheitsabschaltung durch den UR |
| 0x63B0 | 0x63B0 - DAF nicht programmiert |
| 0x63B1 | 0x63B1 - Synchronisation Slave (HR) fehlerhaft |
| 0x63B2 | 0x63B2 - Aufstartfehler Sicherheit |
| 0x63B3 | 0x63B3 - Bremsmomentenabbau |
| 0x63CC | 0x63CC - Rückrollüberwachung |
| 0x63CD | 0x63CD - temporärer EEPROM Fehler |
| 0x63CE | 0x63CE - Kalibrierfehler |
| 0x63CF | 0x63CF - Harte Abschaltung Antrieb oder Bremse |
| 0x63D0 | 0x63D0 - LRR Sensor SG Zustand (Hinweiseintrag) |
| 0x63D1 | 0x63D1 - SRR Rechts Sensor SG Fehler |
| 0x63D2 | 0x63D2 - SRR Rechts Sensor temporärer Fehler |
| 0x63D3 | 0x63D3 - SRR Rechts Sensor Dejustage |
| 0x63D4 | 0x63D4 - SRR Links Sensor SG-Fehler |
| 0x63D5 | 0x63D5 - SRR Links Sensor temporärer Fehler |
| 0x63D6 | 0x63D6 - SRR Links Sensor Dejustage |
| 0x63D7 | 0x63D7 - LRR Dejustage (FUSION) |
| 0x63D8 | 0x63D8 - Schnittstelle AHM |
| 0x63D9 | 0x63D9 - Schnittstelle ASE / ACSM / MRSZ |
| 0x63DA | 0x63DA - Schnittstelle CAS |
| 0x63DB | 0x63DB - Schnittstelle CCC_GW |
| 0x63DC | 0x63DC - Schnittstelle DDE / DME |
| 0x63DD | 0x63DD - Schnittstelle DSC |
| 0x63DE | 0x63DE - Schnittstelle EGS |
| 0x63DF | 0x63DF - Schnittstelle KOMBI |
| 0x63E0 | 0x63E0 - Schnittstelle LDM |
| 0x63E1 | 0x63E1 - Schnittstelle LM |
| 0x63E2 | 0x63E2 - Schnittstelle LRR |
| 0x63E3 | 0x63E3 - Schnittstelle RLS / LM |
| 0x63E4 | 0x63E4 - Schnittstelle SRR-L |
| 0x63E5 | 0x63E5 - Schnittstelle SRR-R |
| 0x63E6 | 0x63E6 - Schnittstelle SZL / LWS |
| 0x63E7 | 0x63E7 - Schnittstelle SZM |
| 0x63E8 | 0x63E8 - Schnittstelle DSC - Radgeschwindigkeiten Signal ungültig |
| 0x63E9 | 0x63E9 - Schnittstelle DSC - Radgeschwindigkeiten Zustand ungültig |
| 0xD004 | 0xD004 - Bus Kommunikationsfehler PT-CAN |
| 0xD005 | 0xD005 - Bus Kommunikationsfehler S-CAN |
| 0xD00E | 0xD00E - Botschaft Navigation GPS 1, ID 34Ah |
| 0xD00F | 0xD00F - Botschaft Navigation GPS 2, ID 34Ch |
| 0xD010 | 0xD010 - Botschaft Navigation System Information, ID 34Eh |
| 0xD011 | 0xD011 - Botschaft Übereinstimmung Navigationsgraph, ID 348h |
| 0xD012 | 0xD012 - Botschaft Navigationsgraph, ID 278h |
| 0xD013 | 0xD013 - Botschaft Synchronisation Navigationsgraph, ID 27Ah |
| 0xD014 | 0xD014 - Botschaft Anzeige Getriebedaten, ID 1D2h |
| 0xD015 | 0xD015 - Botschaft Aussentemperatur/Relativzeit, ID 310h |
| 0xD016 | 0xD016 - Botschaft Bedienung Lenkstock, ID 194h |
| 0xD017 | 0xD017 - Botschaft Blinken, ID 1F6h |
| 0xD018 | 0xD018 - Botschaft Drehmoment 1 PT-CAN, ID A8h |
| 0xD019 | 0xD019 - Botschaft Drehmoment 2, ID A9h |
| 0xD01A | 0xD01A - Botschaft Drehmoment 3 PT-CAN, ID AAh |
| 0xD01B | 0xD01B - Botschaft Fahrzeugmodus, ID 315h |
| 0xD01C | 0xD01C - Botschaft Geschwindigkeit PT-CAN, ID 1A0h |
| 0xD01D | 0xD01D - Botschaft Getriebedaten, ID BAh |
| 0xD01E | 0xD01E - Botschaft Kilometerstand/Reichweite, ID 330h |
| 0xD01F | 0xD01F - Botschaft Klemmenstatus, ID 130h |
| 0xD020 | 0xD020 - Botschaft Lenkradwinkel PT-CAN, ID C4h |
| 0xD021 | 0xD021 - Botschaft Anforderung Radmoment Antriebsstrang, ID BFh |
| 0xD022 | 0xD022 - Botschaft Raddrücke, ID 2B2h |
| 0xD023 | 0xD023 - Botschaft Radgeschwindigkeit PT-CAN, ID CEh |
| 0xD024 | 0xD024 - Botschaft Radmoment Antriebsstrang 1, ID B4h |
| 0xD025 | 0xD025 - Botschaft Radmoment Antriebsstrang 2, ID ACh |
| 0xD026 | 0xD026 - Botschaft Radmoment Bremse, ID E1h |
| 0xD027 | 0xD027 - Botschaft Radtoleranzabgleich, ID 374h |
| 0xD028 | 0xD028 - Botschaft Sitzbelegung Gurtkontakte, ID 2F1h |
| 0xD029 | 0xD029 - Botschaft Beschleunigungsdaten, ID 2B3h |
| 0xD02A | 0xD02A - Botschaft Status Anhänger, ID 2E4h |
| 0xD02B | 0xD02B - Botschaft Status DSC PT-CAN, ID 19Eh |
| 0xD02C | 0xD02C - Botschaft ZV und Klappenzustand, ID 2FCh |
| 0xD02D | 0xD02D - Botschaft Bedienung Wischertasten, ID 2A6h |
| 0xD02E | 0xD02E - Botschaft Anforderung Radmoment Bremse, ID D5h |
| 0xD02F | 0xD02F - Botschaft Sollmomentanforderung, ID BBh |
| 0xD030 | 0xD030 - Botschaft Status Kombi, ID 1B4h |
| 0xD031 | 0xD031 - Botschaft Fahrgestellnummer, ID 380h |
| 0xD032 | 0xD032 - Botschaft Fahrzeugtyp, ID 388h |
| 0xD033 | 0xD033 - Botschaft Status SRR Links, ID 72Ah |
| 0xD034 | 0xD034 - Botschaft Status SRR Rechts, ID 73Ah |
| 0xD035 | 0xD035 - Botschaft Objektdaten SRR Links, ID 720h-729h |
| 0xD036 | 0xD036 - Botschaft Objektdaten SRR Rechts, ID 730h-739h |
| 0xD037 | 0xD037 - Botschaft Status LRR, ID 760h |
| 0xD038 | 0xD038 - Botschaft Objektdaten LRR, ID 740h-75Fh |
| 0xD039 | 0xD039 - Botschaft Dynamische Sicherheit LRR, ID 710h |
| 0xD040 | 0xD040 - Botschaft Motordaten, ID 1D0h |
| 0xD041 | 0xD041 - Botschaft Lampenzustand, ID 21Ah |
| 0xD042 | 0xD042 - Botschaft Regensensor - Wischergeschwindigkeit, ID 226h |
| 0xD043 | 0xD043 - Botschaft Fahrlicht, ID 314h |
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

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | Umbed1 | Umbed2 | Umbed3 | 0x07 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Fehlercode intern | Hex | - | unsigned char | - | - | 1 | - |
| 0x02 | Fehlerinfo intern | Hex | - | unsigned char | - | - | 1 | - |
| 0x03 | Klemme30 Spannung | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x04 | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | Antriebsanforderung | Nm | - | unsigned char | - | 20 | 1 | 0 |
| 0x06 | Bremsanforderung | Nm | - | unsigned char | - | 20 | 1 | 0 |
| 0x07 | Betriebszustand | Hex | high | unsigned int | - | - | - | - |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 180 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x62CC | 0x62CC - Steuergerätefehler |
| 0x62CD | 0x62CD - Codierdatenfehler |
| 0x62CE | 0x62CE - Überspannungsfehler |
| 0x62CF | 0x62CF - Unterspannungsfehler |
| 0x62D0 | 0x62D0 - Abschaltung Bremsenüberhitzung |
| 0x62D1 | 0x62D1 - Sicherheitsabschaltung durch den Hauptrechner |
| 0x62D2 | 0x62D2 - Plausibilität  Fahrpedal getreten  |
| 0x62D3 | 0x62D3 - V_DSC und V_ANZ unplausibel |
| 0x62D4 | 0x62D4 - Abschaltung durch Motorsteuergerät |
| 0x62D5 | 0x62D5 - Stillstandsmanagement |
| 0x62D6 | 0x62D6 - Abschaltung durch Bremsensteuergerät |
| 0x62D7 | 0x62D7 - OBR Offset Gierrate |
| 0x62D8 | 0x62D8 - Abschaltung durch Kombi |
| 0x62D9 | 0x62D9 - Plausibilität Sitzbelegung Fahrersitz |
| 0x62DA | 0x62DA - Harte Abschaltung Antrieb |
| 0x62DB | 0x62DB - Harte Abschaltung Bremse |
| 0x62DC | 0x62DC - Weckleitungsfehler |
| 0x62DD | 0x62DD - Plausibilität Bremspedal |
| 0x62DE | 0x62DE - Sicherheitsabschaltung PT-CAN |
| 0x62DF | 0x62DF - Steuergerät Aufstartfehler |
| 0x62E0 | 0x62E0 - SRR-R Störung durch Fremdeinwirkung |
| 0x62E1 | 0x62E1 - SRR-L Störung durch Fremdeinwirkung |
| 0x62E2 | 0x62E2 - NVC-Modul Zustand |
| 0x62E3 | 0x62E3 - iBreak-Modul Zustand |
| 0x62E4 | 0x62E4 - Harte Abschaltung Rucküberwachung |
| 0x62E6 | 0x62E6 - Zustand Fahrpedal Signale |
| 0x62E7 | 0x62E7 - Zustand Gierraten Signal |
| 0x62E8 | 0x62E8 - Ungültige oder falsche Fahrgestellnummer |
| 0x62E9 | 0x62E9 - Undokumentierte Fehlerabschaltung |
| 0x62EA | 0x62EA - Vorwarnung Beschleunigungsüberwachung |
| 0x62EB | 0x62EB - Vorwarnung Verzögerungsüberwachung |
| 0x63AC | 0x63AC - Plausibilität KOMBI Signal ungültig |
| 0x63AD | 0x63AD - Plausibilität Beschleunigungssensoren |
| 0x63AE | 0x63AE - Harte Abschaltung durch den UR |
| 0x63AF | 0x63AF - Sicherheitsabschaltung durch den UR |
| 0x63B0 | 0x63B0 - DAF nicht programmiert |
| 0x63B1 | 0x63B1 - Synchronisation Slave (HR) fehlerhaft |
| 0x63B2 | 0x63B2 - Aufstartfehler Sicherheit |
| 0x63B3 | 0x63B3 - Bremsmomentenabbau |
| 0x63CC | 0x63CC - Rückrollüberwachung |
| 0x63CD | 0x63CD - temporärer EEPROM Fehler |
| 0x63CE | 0x63CE - Kalibrierfehler |
| 0x63CF | 0x63CF - Harte Abschaltung Antrieb oder Bremse |
| 0x63D0 | 0x63D0 - LRR Sensor SG Zustand (Hinweiseintrag) |
| 0x63D1 | 0x63D1 - SRR Rechts Sensor SG Fehler |
| 0x63D2 | 0x63D2 - SRR Rechts Sensor temporärer Fehler |
| 0x63D3 | 0x63D3 - SRR Rechts Sensor Dejustage |
| 0x63D4 | 0x63D4 - SRR Links Sensor SG-Fehler |
| 0x63D5 | 0x63D5 - SRR Links Sensor temporärer Fehler |
| 0x63D6 | 0x63D6 - SRR Links Sensor Dejustage |
| 0x63D7 | 0x63D7 - LRR Dejustage (FUSION) |
| 0x63D8 | 0x63D8 - Schnittstelle AHM |
| 0x63D9 | 0x63D9 - Schnittstelle ASE / ACSM / MRSZ |
| 0x63DA | 0x63DA - Schnittstelle CAS |
| 0x63DB | 0x63DB - Schnittstelle CCC_GW |
| 0x63DC | 0x63DC - Schnittstelle DDE / DME |
| 0x63DD | 0x63DD - Schnittstelle DSC |
| 0x63DE | 0x63DE - Schnittstelle EGS |
| 0x63DF | 0x63DF - Schnittstelle KOMBI |
| 0x63E0 | 0x63E0 - Schnittstelle LDM |
| 0x63E1 | 0x63E1 - Schnittstelle LM |
| 0x63E2 | 0x63E2 - Schnittstelle LRR |
| 0x63E3 | 0x63E3 - Schnittstelle RLS / LM |
| 0x63E4 | 0x63E4 - Schnittstelle SRR-L |
| 0x63E5 | 0x63E5 - Schnittstelle SRR-R |
| 0x63E6 | 0x63E6 - Schnittstelle SZL / LWS |
| 0x63E7 | 0x63E7 - Schnittstelle SZM |
| 0x63E8 | 0x63E8 - Schnittstelle DSC - Radgeschwindigkeiten Signal ungültig |
| 0x63E9 | 0x63E9 - Schnittstelle DSC - Radgeschwindigkeiten Zustand ungültig |
| 0xD004 | 0xD004 - Bus Kommunikationsfehler PT-CAN |
| 0xD005 | 0xD005 - Bus Kommunikationsfehler S-CAN |
| 0xD00E | 0xD00E - Botschaft Navigation GPS 1, ID 34Ah |
| 0xD00F | 0xD00F - Botschaft Navigation GPS 2, ID 34Ch |
| 0xD010 | 0xD010 - Botschaft Navigation System Information, ID 34Eh |
| 0xD011 | 0xD011 - Botschaft Übereinstimmung Navigationsgraph, ID 348h |
| 0xD012 | 0xD012 - Botschaft Navigationsgraph, ID 278h |
| 0xD013 | 0xD013 - Botschaft Synchronisation Navigationsgraph, ID 27Ah |
| 0xD014 | 0xD014 - Botschaft Anzeige Getriebedaten, ID 1D2h |
| 0xD015 | 0xD015 - Botschaft Aussentemperatur/Relativzeit, ID 310h |
| 0xD016 | 0xD016 - Botschaft Bedienung Lenkstock, ID 194h |
| 0xD017 | 0xD017 - Botschaft Blinken, ID 1F6h |
| 0xD018 | 0xD018 - Botschaft Drehmoment 1 PT-CAN, ID A8h |
| 0xD019 | 0xD019 - Botschaft Drehmoment 2, ID A9h |
| 0xD01A | 0xD01A - Botschaft Drehmoment 3 PT-CAN, ID AAh |
| 0xD01B | 0xD01B - Botschaft Fahrzeugmodus, ID 315h |
| 0xD01C | 0xD01C - Botschaft Geschwindigkeit PT-CAN, ID 1A0h |
| 0xD01D | 0xD01D - Botschaft Getriebedaten, ID BAh |
| 0xD01E | 0xD01E - Botschaft Kilometerstand/Reichweite, ID 330h |
| 0xD01F | 0xD01F - Botschaft Klemmenstatus, ID 130h |
| 0xD020 | 0xD020 - Botschaft Lenkradwinkel PT-CAN, ID C4h |
| 0xD021 | 0xD021 - Botschaft Anforderung Radmoment Antriebsstrang, ID BFh |
| 0xD022 | 0xD022 - Botschaft Raddrücke, ID 2B2h |
| 0xD023 | 0xD023 - Botschaft Radgeschwindigkeit PT-CAN, ID CEh |
| 0xD024 | 0xD024 - Botschaft Radmoment Antriebsstrang 1, ID B4h |
| 0xD025 | 0xD025 - Botschaft Radmoment Antriebsstrang 2, ID ACh |
| 0xD026 | 0xD026 - Botschaft Radmoment Bremse, ID E1h |
| 0xD027 | 0xD027 - Botschaft Radtoleranzabgleich, ID 374h |
| 0xD028 | 0xD028 - Botschaft Sitzbelegung Gurtkontakte, ID 2F1h |
| 0xD029 | 0xD029 - Botschaft Beschleunigungsdaten, ID 2B3h |
| 0xD02A | 0xD02A - Botschaft Status Anhänger, ID 2E4h |
| 0xD02B | 0xD02B - Botschaft Status DSC PT-CAN, ID 19Eh |
| 0xD02C | 0xD02C - Botschaft ZV und Klappenzustand, ID 2FCh |
| 0xD02D | 0xD02D - Botschaft Bedienung Wischertasten, ID 2A6h |
| 0xD02E | 0xD02E - Botschaft Anforderung Radmoment Bremse, ID D5h |
| 0xD02F | 0xD02F - Botschaft Sollmomentanforderung, ID BBh |
| 0xD030 | 0xD030 - Botschaft Status Kombi, ID 1B4h |
| 0xD031 | 0xD031 - Botschaft Fahrgestellnummer, ID 380h |
| 0xD032 | 0xD032 - Botschaft Fahrzeugtyp, ID 388h |
| 0xD033 | 0xD033 - Botschaft Status SRR Links, ID 72Ah |
| 0xD034 | 0xD034 - Botschaft Status SRR Rechts, ID 73Ah |
| 0xD035 | 0xD035 - Botschaft Objektdaten SRR Links, ID 720h-729h |
| 0xD036 | 0xD036 - Botschaft Objektdaten SRR Rechts, ID 730h-739h |
| 0xD037 | 0xD037 - Botschaft Status LRR, ID 760h |
| 0xD038 | 0xD038 - Botschaft Objektdaten LRR, ID 740h-75Fh |
| 0xD039 | 0xD039 - Botschaft Dynamische Sicherheit LRR, ID 710h |
| 0xD040 | 0xD040 - Botschaft Motordaten, ID 1D0h |
| 0xD041 | 0xD041 - Botschaft Lampenzustand, ID 21Ah |
| 0xD042 | 0xD042 - Botschaft Regensensor - Wischergeschwindigkeit, ID 226h |
| 0xD043 | 0xD043 - Botschaft Fahrlicht, ID 314h |
| 0x5000 | 0x5000 - Signalfehler (USI) |
| 0x5100 | 0x5100 - Harte Abschaltung durch den Überwachungsrechner (Hinweiseintrag) |
| 0x5101 | 0x5101 - Sicherheitsabschaltung druch den Überwachungsrechner (Hinweiseintrag) |
| 0x5110 | 0x5110 - Vorwarnung Antrieb |
| 0x5111 | 0x5111 - Vorwarnung Bremse |
| 0x5200 | 0x5200 - SRR-R SG Fehler 0 |
| 0x5201 | 0x5201 - SRR-R SG Fehler 1 |
| 0x5202 | 0x5202 - SRR-R SG Fehler 2 |
| 0x5203 | 0x5203 - SRR-R SG Fehler 3 |
| 0x5204 | 0x5204 - SRR-R SG Fehler 4 |
| 0x5205 | 0x5205 - SRR-R SG Fehler 5 |
| 0x5206 | 0x5206 - SRR-R SG Fehler 6 |
| 0x5207 | 0x5207 - SRR-R SG Fehler 7 |
| 0x5208 | 0x5208 - SRR-R SG Fehler 8 |
| 0x5209 | 0x5209 - SRR-R SG Fehler 9 |
| 0x520A | 0x520A - SRR-R SG Fehler 10 |
| 0x520B | 0x520B - SRR-R SG Fehler 11 |
| 0x520C | 0x520C - SRR-R SG Fehler 12 |
| 0x520D | 0x520D - SRR-R SG Fehler 13 |
| 0x520E | 0x520E - SRR-R SG Fehler 14 |
| 0x520F | 0x520F - SRR-R SG Fehler 15 |
| 0x5210 | 0x5210 - SRR-L SG Fehler 0 |
| 0x5211 | 0x5211 - SRR-L SG Fehler 1 |
| 0x5212 | 0x5212 - SRR-L SG Fehler 2 |
| 0x5213 | 0x5213 - SRR-L SG Fehler 3 |
| 0x5214 | 0x5214 - SRR-L SG Fehler 4 |
| 0x5215 | 0x5215 - SRR-L SG Fehler 5 |
| 0x5216 | 0x5216 - SRR-L SG Fehler 6 |
| 0x5217 | 0x5217 - SRR-L SG Fehler 7 |
| 0x5218 | 0x5218 - SRR-L SG Fehler 8 |
| 0x5219 | 0x5219 - SRR-L SG Fehler 9 |
| 0x521A | 0x521A - SRR-L SG Fehler 10 |
| 0x521B | 0x521B - SRR-L SG Fehler 11 |
| 0x521C | 0x521C - SRR-L SG Fehler 12 |
| 0x521D | 0x521D - SRR-L SG Fehler 13 |
| 0x521E | 0x521E - SRR-L SG Fehler 14 |
| 0x521F | 0x521F - SRR-L SG Fehler 15 |
| 0x5220 | 0x5220 - LRR Blindheit (FUSION) |
| 0x5221 | 0x5221 - SRR-L Blindheit (FUSION) |
| 0x5222 | 0x5222 - SRR-R Blindheit (FUSION) |
| 0x5230 | 0x5230 - NVC Fehler 0 |
| 0x5231 | 0x5231 - NVC Fehler 1 |
| 0x5232 | 0x5232 - NVC Fehler 2 |
| 0x5233 | 0x5233 - NVC Fehler 3 |
| 0x5234 | 0x5234 - NVC Fehler 4 |
| 0x5235 | 0x5235 - NVC Fehler 5 |
| 0x5236 | 0x5236 - NVC Fehler 6 |
| 0x5237 | 0x5237 - NVC Fehler 7 |
| 0x5238 | 0x5238 - NVC Fehler 8 |
| 0x5239 | 0x5239 - NVC Fehler 9 |
| 0x523A | 0x523A - NVC Fehler 10 |
| 0x523B | 0x523B - NVC Fehler 11 |
| 0x523C | 0x523C - NVC Fehler 12 |
| 0x523D | 0x523D - NVC Fehler 13 |
| 0x523E | 0x523E - NVC Fehler 14 |
| 0x523F | 0x523F - NVC Fehler 15 |
| 0x5240 | 0x5240 - SG - SHUTDOWN Fehler |
| 0x5241 | 0x5241 - temporaerer EEPROM Fehler |
| 0x5242 | 0x5242 - Falsche oder fehlerhafte Fahrgestellnummer |
| 0x5243 | 0x5243 - Synchronisation Slave (HR) fehlerhaft |
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
| F_UWB_ERW | ja |

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | Umbed1 | Umbed2 | Umbed3 | 0x07 |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Fehlercode intern | Hex | - | unsigned char | - | - | 1 | - |
| 0x02 | Fehlerinfo intern | Hex | - | unsigned char | - | - | 1 | - |
| 0x03 | Klemme30 Spannung | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x04 | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | Antriebsanforderung | Nm | - | unsigned char | - | 20 | 1 | 0 |
| 0x06 | Bremsanforderung | Nm | - | unsigned char | - | 20 | 1 | 0 |
| 0x07 | Betriebszustand | Hex | high | unsigned int | - | - | - | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 172 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5000 | 0x5000 - Signalfehler (USI) |
| 0x5100 | 0x5100 - Harte Abschaltung durch den Überwachungsrechner (Hinweiseintrag) |
| 0x5101 | 0x5101 - Sicherheitsabschaltung druch den Überwachungsrechner (Hinweiseintrag) |
| 0x5110 | 0x5110 - Vorwarnung Antrieb |
| 0x5111 | 0x5111 - Vorwarnung Bremse |
| 0x5200 | 0x5200 - SRR-R SG Fehler 0 |
| 0x5201 | 0x5201 - SRR-R SG Fehler 1 |
| 0x5202 | 0x5202 - SRR-R SG Fehler 2 |
| 0x5203 | 0x5203 - SRR-R SG Fehler 3 |
| 0x5204 | 0x5204 - SRR-R SG Fehler 4 |
| 0x5205 | 0x5205 - SRR-R SG Fehler 5 |
| 0x5206 | 0x5206 - SRR-R SG Fehler 6 |
| 0x5207 | 0x5207 - SRR-R SG Fehler 7 |
| 0x5208 | 0x5208 - SRR-R SG Fehler 8 |
| 0x5209 | 0x5209 - SRR-R SG Fehler 9 |
| 0x520A | 0x520A - SRR-R SG Fehler 10 |
| 0x520B | 0x520B - SRR-R SG Fehler 11 |
| 0x520C | 0x520C - SRR-R SG Fehler 12 |
| 0x520D | 0x520D - SRR-R SG Fehler 13 |
| 0x520E | 0x520E - SRR-R SG Fehler 14 |
| 0x520F | 0x520F - SRR-R SG Fehler 15 |
| 0x5210 | 0x5210 - SRR-L SG Fehler 0 |
| 0x5211 | 0x5211 - SRR-L SG Fehler 1 |
| 0x5212 | 0x5212 - SRR-L SG Fehler 2 |
| 0x5213 | 0x5213 - SRR-L SG Fehler 3 |
| 0x5214 | 0x5214 - SRR-L SG Fehler 4 |
| 0x5215 | 0x5215 - SRR-L SG Fehler 5 |
| 0x5216 | 0x5216 - SRR-L SG Fehler 6 |
| 0x5217 | 0x5217 - SRR-L SG Fehler 7 |
| 0x5218 | 0x5218 - SRR-L SG Fehler 8 |
| 0x5219 | 0x5219 - SRR-L SG Fehler 9 |
| 0x521A | 0x521A - SRR-L SG Fehler 10 |
| 0x521B | 0x521B - SRR-L SG Fehler 11 |
| 0x521C | 0x521C - SRR-L SG Fehler 12 |
| 0x521D | 0x521D - SRR-L SG Fehler 13 |
| 0x521E | 0x521E - SRR-L SG Fehler 14 |
| 0x521F | 0x521F - SRR-L SG Fehler 15 |
| 0x5220 | 0x5220 - LRR Blindheit (FUSION) |
| 0x5221 | 0x5221 - SRR-L Blindheit (FUSION) |
| 0x5222 | 0x5222 - SRR-R Blindheit (FUSION) |
| 0x5230 | 0x5230 - NVC Fehler 0 |
| 0x5231 | 0x5231 - NVC Fehler 1 |
| 0x5232 | 0x5232 - NVC Fehler 2 |
| 0x5233 | 0x5233 - NVC Fehler 3 |
| 0x5234 | 0x5234 - NVC Fehler 4 |
| 0x5235 | 0x5235 - NVC Fehler 5 |
| 0x5236 | 0x5236 - NVC Fehler 6 |
| 0x5237 | 0x5237 - NVC Fehler 7 |
| 0x5238 | 0x5238 - NVC Fehler 8 |
| 0x5239 | 0x5239 - NVC Fehler 9 |
| 0x523A | 0x523A - NVC Fehler 10 |
| 0x523B | 0x523B - NVC Fehler 11 |
| 0x523C | 0x523C - NVC Fehler 12 |
| 0x523D | 0x523D - NVC Fehler 13 |
| 0x523E | 0x523E - NVC Fehler 14 |
| 0x523F | 0x523F - NVC Fehler 15 |
| 0x5240 | 0x5240 - SG - SHUTDOWN Fehler |
| 0x5241 | 0x5241 - temporaerer EEPROM Fehler |
| 0x5242 | 0x5242 - Falsche oder fehlerhafte Fahrgestellnummer |
| 0x5243 | 0x5243 - Synchronisation Slave (HR) fehlerhaft |
| 0x8001 | 0x8001 - Weckleitung dauerhaft EIN |
| 0x8021 | 0x8021 - HL Abschaltung HR |
| 0x8022 | 0x8022 - HL Abschaltung UER |
| 0x8030 | 0x8030 - Startup Handler HR |
| 0x8031 | 0x8031 - Startup Programmierstatus HR |
| 0x8032 | 0x8032 - Startup Verrieglungstestzeit HR |
| 0x8033 | 0x8033 - Startup Testzeit HR |
| 0x8034 | 0x8034 - Startup EEPROM HR |
| 0x8035 | 0x8035 - Startup UERCHECK HR |
| 0x8036 | 0x8036 - Startup IOPIN HR |
| 0x8037 | 0x8037 - Startup UERLOCK HR |
| 0x8038 | 0x8038 - Startup Handler UER |
| 0x8039 | 0x8039 - Startup Programmierstatus UER |
| 0x803A | 0x803A - Startup Verrieglungstest UER |
| 0x803B | 0x803B - Startup Verrieglungstestzeit UER |
| 0x803C | 0x803C - Startup Testzeit UER |
| 0x803D | 0x803D - Startup ADC UER |
| 0x803E | 0x803E - Startup HRLOCK UER |
| 0x803F | 0x803F - Startup HRCHK UER |
| 0x8041 | 0x8041 - SCI1 CHKSUM HR |
| 0x8042 | 0x8042 - SCI1 OVERRUN HR |
| 0x8043 | 0x8043 - SCI1 PARITY HR |
| 0x8044 | 0x8044 - SCI2 CHKSUM HR |
| 0x8045 | 0x8045 - SCI2 OVERRUN HR |
| 0x8046 | 0x8046 - SCI2 PARITY HR |
| 0x8048 | 0x8048 - SCI0 CHKSUM UER |
| 0x8049 | 0x8049 - SCI0 OVERRUN UER |
| 0x804A | 0x804A - SCI0 PARITY UER |
| 0x804B | 0x804B - SCI1 CHKSUM UER |
| 0x804C | 0x804C - SCI1 OVERRUN UER |
| 0x804D | 0x804D - SCI1 PARITY UER |
| 0x8054 | 0x8054 - Task System HR |
| 0x8055 | 0x8055 - Task Master Timeout |
| 0x8056 | 0x8056 - Task Master Task |
| 0x8057 | 0x8057 - Task TimingAll HR |
| 0x8058 | 0x8058 - Stack User HR |
| 0x8059 | 0x8059 - Stack OS HR |
| 0x805A | 0x805A - Task Anzahl 2ms HR |
| 0x805B | 0x805B - Task Anzahl 5ms HR |
| 0x805C | 0x805C - Task Anzahl 10ms HR |
| 0x805D | 0x805D - Task Anzahl Sensor HR |
| 0x805E | 0x805E - Task Anzahl Reglertask HR |
| 0x8060 | 0x8060 - intern HR |
| 0x8061 | 0x8061 - intern ROM HR |
| 0x8062 | 0x8062 - intern RAM HR |
| 0x8063 | 0x8063 - intern VoltageADC HR |
| 0x8064 | 0x8064 - intern VoltageVCC HR |
| 0x8065 | 0x8065 - intern Shutdown HR |
| 0x8066 | 0x8066 - intern CPU HR |
| 0x8067 | 0x8067 - intern Ablauf HR |
| 0x8071 | 0x8071 - Exception Reserved HR |
| 0x8072 | 0x8072 - Exception MachineCheck HR |
| 0x8073 | 0x8073 - Exception DataAccess HR |
| 0x8074 | 0x8074 - Exception InstrAccess HR |
| 0x8075 | 0x8075 - Exception Alignment HR |
| 0x8076 | 0x8076 - Exception Program HR |
| 0x8077 | 0x8077 - Exception FPunavailable HR |
| 0x8078 | 0x8078 - Exception SystemCall HR |
| 0x8079 | 0x8079 - Exception Trace HR |
| 0x807A | 0x807A - Exception FPassist HR |
| 0x807B | 0x807B - Exception PerfMonitor HR |
| 0x807C | 0x807C - Exception SWEmulation HR |
| 0x807D | 0x807D - Exception InstrProtection HR |
| 0x807E | 0x807E - Exception DataProtection HR |
| 0x807F | 0x807F - Exception ImplBreakpoint HR |
| 0x8080 | 0x8080 - Reset Extern HR |
| 0x8081 | 0x8081 - Reset LossLock HR |
| 0x8082 | 0x8082 - Reset COP HR |
| 0x8083 | 0x8083 - Reset Checkstop HR |
| 0x8084 | 0x8084 - Reset DebugHard HR |
| 0x8085 | 0x8085 - Reset DebugSoft HR |
| 0x8086 | 0x8086 - Reset JTAG HR |
| 0x8087 | 0x8087 - Reset ClockSwitch HR |
| 0x8088 | 0x8088 - Reset IllegalBitChange HR |
| 0x8094 | 0x8094 - Task System UER |
| 0x8095 | 0x8095 - Task Slave UER |
| 0x8096 | 0x8096 - Task Slave UER |
| 0x8097 | 0x8097 - Task TimingAll UER |
| 0x8098 | 0x8098 - Stack Stack5 UER |
| 0x8099 | 0x8099 - Stack Stack20 UER |
| 0x809A | 0x809A - Stack StackIRQ UER |
| 0x80A0 | 0x80A0 - intern UER |
| 0x80A1 | 0x80A1 - intern ROM UER |
| 0x80A2 | 0x80A2 - intern RAM UER |
| 0x80A3 | 0x80A3 - intern VoltageADC UER |
| 0x80A4 | 0x80A4 - intern VoltageVCC UER |
| 0x80A6 | 0x80A6 - intern EEPROM |
| 0x80A7 | 0x80A7 - intern CPU  UER |
| 0x80B1 | 0x80B1 - Reset Clock UER |
| 0x80B2 | 0x80B2 - Reset COP UER |
| 0x80B3 | 0x80B3 - Reset IntrTrap UER |
| 0x80B4 | 0x80B4 - Reset SWI UER |
| 0x80D8 | 0x80D8 - Ringbuf StatusKombi |
| 0x80DA | 0x80DA - Ringbuf Geschwindigkeit |
| 0x80DB | 0x80DB - Ringbuf StatusDSC |
| 0x80DC | 0x80DC - Ringbuf BedienungTempomat |
| 0x80DD | 0x80DD - Ringbuf Klemmenstatus |
| 0x80DE | 0x80DE - Ringbuf RadmomBremse |
| 0x80E2 | 0x80E2 - Ringbuf RadmomPT |
| 0x80E4 | 0x80E4 - Ringbuf Torque3 |
| 0x80E6 | 0x80E6 - Ringbuf Torque1 |
| 0x80FC | 0x80FC - Startup Verrieglunstest Senden |
| 0x80FD | 0x80FD - Startup SelfClock UER |
| 0x8140 | 0x8140 - Systemauslastung HR 80 Prozent |
| 0x8141 | 0x8141 - Systemauslastung HR 95 Prozent |
| 0x8142 | 0x8142 - Tick HR ungleich 1us |
| 0x8143 | 0x8143 - Time Check HR Taskfehler |
| 0x8400 | 0x8400 - Unkritische Fehler |
| 0x8510 | 0x8510 - Fehler ext RAM Testmodul |
| 0x8541 | 0x8541 - Warning Stack User HR |
| 0x8542 | 0x8542 - Warning Stack OS HR |
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

Dimensions: 110 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x8001 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8021 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8022 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8030 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8031 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8032 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8033 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8034 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8035 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8036 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8037 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8038 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8039 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x803A | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x803B | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x803C | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x803D | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x803E | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x803F | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8041 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8042 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8043 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8044 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8045 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8046 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8048 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8049 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x804A | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x804B | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x804C | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x804D | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8054 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8055 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8056 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8057 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8058 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8059 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x805A | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x805B | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x805C | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x805D | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x805E | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8060 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8061 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8062 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8063 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8064 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8065 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8066 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8067 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8071 | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x8072 | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x8073 | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x8074 | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x8075 | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x8076 | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x8077 | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x8078 | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x8079 | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x807A | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x807B | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x807C | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x807D | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x807E | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x807F | 0x08 | 0x09 | UmbedISP | 0x0D |
| 0x8080 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8081 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8082 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8083 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8084 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8085 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8086 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8087 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8088 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8094 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8095 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8096 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8097 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8098 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8099 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x809A | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80A0 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80A1 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80A2 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80A3 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80A4 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80A7 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80B1 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80B2 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80B3 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80B4 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80D8 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80DA | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80DB | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80DC | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80DD | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80DE | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80E2 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80E4 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80E6 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80FC | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x80FD | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8140 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8141 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8142 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8143 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8400 | 0x0B | 0x0C | UmbedISP | 0x0D |
| 0x8541 | 0x0A | 0x0A | UmbedISP | 0x0D |
| 0x8542 | 0x0A | 0x0A | UmbedISP | 0x0D |
| default | Umbed1 | Umbed2 | Umbed3 | 0x07 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 14 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Fehlercode intern | Hex | - | unsigned char | - | - | 1 | - |
| 0x02 | Fehlerinfo intern | Hex | - | unsigned char | - | - | 1 | - |
| 0x03 | Klemme30 Spannung | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x04 | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | Antriebsanforderung | Nm | - | unsigned char | - | 20 | 1 | 0 |
| 0x06 | Bremsanforderung | Nm | - | unsigned char | - | 20 | 1 | 0 |
| 0x07 | Betriebszustand | Hex | high | unsigned int | - | - | 1 | - |
| 0x08 | Exception Adresse high | Hex | high | unsigned int | - | - | 1 | - |
| 0x09 | Exception Adresse low | Hex | high | unsigned int | - | - | 1 | - |
| 0x0A | leer | Hex | high | unsigned int | - | - | 1 | - |
| 0x0B | Unkritischer Fehler high | Hex | high | unsigned int | - | - | 1 | - |
| 0x0C | Unkritischer Fehler low | Hex | high | unsigned int | - | - | 1 | - |
| 0x0D | Systemzeit Sekundenteil | s | high | unsigned int | - | - | 1 | - |
| 0x0E | Systemzeit Millisekundenteil | ms | - | unsigned char | - | 4 | - | - |

<a id="table-jobresultecustate"></a>
### JOBRESULTECUSTATE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | INIT |
| 0x01 | RUN |
| 0x02 | Pruefung des Programmierstatus UR |
| 0x04 | Pruefung der CAN-Verriegelung |
| 0x11 | Warten auf Freigabe vom UR |
| 0x12 | SLEEP_INDIKATION UR |
| 0xXY | für diesen Wert ist kein Text hinterlegt |

<a id="table-umbed1"></a>
### UMBED1

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 0x02 | 0x01 | 0x02 |

<a id="table-umbed2"></a>
### UMBED2

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 0x02 | 0x03 | 0x04 |

<a id="table-umbed3"></a>
### UMBED3

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 0x02 | 0x05 | 0x06 |

<a id="table-temp-acc-taster"></a>
### TEMP_ACC_TASTER

Dimensions: 10 rows × 3 columns

| BIT | TEXT_TASTER | WERT |
| --- | --- | --- |
| 0x00 | Keine Aktion | 1 |
| 0x01 | Tippen nach vorne | 2 |
| 0x02 | Überdrücken nach vorne | 3 |
| 0x04 | Tippen nach hinten | 4 |
| 0x08 | Überdrücken nach hinten | 5 |
| 0x10 | Tippen nach unten | 6 |
| 0x40 | Axial Tippen | 7 |
| 0x90 | Tippen nach oben | 8 |
| 0xFF | Signal ungültig | 9 |
| 0xXY | nicht definiert | 99 |

<a id="table-stat-botschaft"></a>
### STAT_BOTSCHAFT

Dimensions: 9 rows × 2 columns

| BIT | STATUS |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Timeoutfehler |
| 0x02 | Signal ungültig |
| 0x04 | Checksummenfehler |
| 0x08 | Alivezählerfehler |
| 0x10 | Signal undefiniert |
| 0x20 | Initialisierungsfehler |
| 0x40 | Signal irrelevant |
| 0xXY | nicht definiert |

<a id="table-temp-acc-abstandswahl"></a>
### TEMP_ACC_ABSTANDSWAHL

Dimensions: 5 rows × 3 columns

| BIT | TEXT_ABSTAND | WERT |
| --- | --- | --- |
| 0x00 | Keine Aktion | 1 |
| 0x01 | Tippen nach oben | 2 |
| 0x02 | Tippen nach unten | 3 |
| 0x03 | Signal ungültig | 4 |
| 0xXY | nichtl definiert | 99 |

<a id="table-nahbereichsradar"></a>
### NAHBEREICHSRADAR

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0600 | linker SRR |
| 0x0700 | rechter SRR |

<a id="table-umbedisp"></a>
### UMBEDISP

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 0x02 | 0x03 | 0x0E |
