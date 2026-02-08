# SZL_60.prg

- Jobs: [59](#jobs)
- Tables: [47](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | SZL |
| ORIGIN | BMW_AG EE-51  Jens Klingseisen |
| REVISION | 3.000 |
| AUTHOR | Kostal AEL3 Peter Lunova, Kostal AEL3 Jie Ma, Kostal AEL3 Andreas Bienstein |
| COMMENT | N/A |
| PACKAGE | 1.29 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
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
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [STATUS_LESEN](#job-status-lesen) - mit dem SGBD-Generator erzeugt
- [STATUS_LENKRADHEIZUNG](#job-status-lenkradheizung) - mit dem SGBD-Generator erzeugt
- [STATUS_FASTA_DATEN_LESEN](#job-status-fasta-daten-lesen) - mit dem SGBD-Generator erzeugt
- [STATUS_SW_VERSION](#job-status-sw-version) - Seriennummer Lenkradelektronik auslesen KWP2000: $22 Steuergeraetespezifische Daten lesen $0006 Seriennummer LRE Modus  : Default
- [ABGLEICH_LENKWINKELSENSOR_RUECKSETZEN](#job-abgleich-lenkwinkelsensor-ruecksetzen) - Abgleichen des Lenkwinkelsensors zuruecksetzen KWP2000: $31 Steuergeraetespezifische Routine starten $44 Lenkwinkelsensor abgleichen ruecksetzen Modus  : Default Vor ABGLEICH_LENKWINKELSENSOR muss dieser Job ausgefuehrt werden!
- [ABGLEICH_LENKWINKELSENSOR](#job-abgleich-lenkwinkelsensor) - Abgleichen des Lenkwinkelsensors bei Lenkrad-Geradeausstellung KWP2000: $31 Steuergeraetespezifische Routine starten $43 Lenkwinkelsensor abgleichen Modus  : Default Vor diesem Job muss ABGLEICH_LENKWINKELSENSOR_RUECKSETZEN ausgefuehrt werden!
- [LWS_OFFSET_KORREKTUR_SCHREIBEN_GRAD](#job-lws-offset-korrektur-schreiben-grad) - Abgleichen des Lenkwinkelsensors bei Lenkrad-Geradeausstellung incl. Wasserwaagenoffset KWP2000: $31 Steuergeraetespezifische Routine starten $47 Lenkwinkelsensor-Feinabgleich Modus  : Default Als Argument wird der Wasserwaagen-Offset uebergeben
- [STEUERN_LENKRADHEIZUNG](#job-steuern-lenkradheizung) - Ansteuern der Lenkradheizung KWP2000: $31 Steuergeraetespezifische Routine starten $45 Funktionsbeleuchtung ansteuern Modus  : Default
- [STEUERN_HUPE](#job-steuern-hupe) - Ansteuern von Hupe KWP2000: $31 Steuergeraetespezifische Routine starten $40 Hupe ansteuern Modus  : Default
- [STEUERN_FUNKTIONSBELEUCHTUNG](#job-steuern-funktionsbeleuchtung) - Ansteuern der Funktionsbeleuchtung KWP2000: $31 Steuergeraetespezifische Routine starten $42 Funktionsbeleuchtung ansteuern Modus  : Default
- [STEUERN_DIMMBELEUCHTUNG](#job-steuern-dimmbeleuchtung) - Ansteuern der Dimmbeleuchtung KWP2000: $31 Steuergeraetespezifische Routine starten $41 Dimmbeleuchtung steuern Modus  : Default
- [STEUERN_BLINKERSCHALTER](#job-steuern-blinkerschalter) - Ansteuern des Blinkerschalters KWP2000: $31 Steuergeraetespezifische Routine starten $42 Funktionsbeleuchtung ansteuern Modus  : Default
- [LUZ_NULL_SETZEN](#job-luz-null-setzen) - Lenkradumdehungszahl auf Null setzen KWP2000: 0x31 0x48 Modus:   Default  Notwendig nach Codierung in der Produktion: umbedingt auf Geradeausstellung der Räder und des Lenkrades achten
- [STATUS_LENKWINKELSENSOR](#job-status-lenkwinkelsensor) - mit dem SGBD-Generator erzeugt

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

<a id="job-status-lesen"></a>
### STATUS_LESEN

mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LENKRADHEIZUNG_ANSTEUERUNG_WERT | int | Status der Lenkradheizung-Ansteuerung table SG_Status_Lenkradheizung_Ansteuerung WERT |
| STAT_LENKRADHEIZUNG_ANSTEUERUNG_TEXT | string | Status der Lenkradheizung-Ansteuerung table SG_Status_Lenkradheizung_Ansteuerung TEXT |
| STAT_LENKRADHEIZUNG_SENSOR_WERT | int | Status der Lenkradheizung Temperatorsensor table SG_Status_Lenkradheizung_Sensor WERT |
| STAT_LENKRADHEIZUNG_SENSOR_TEXT | string | Status der Lenkradheizung Temperatorsensor table SG_Status_Lenkradheizung_Sensor TEXT |
| STAT_LENKRADHEIZUNG_TASTER_LENKRAD | int | Status der Lenkradheizung-Taster |
| STAT_KLEMMENSTATUS_BUS_KL_R_EIN_CAS | int | Klemmestatus Klemme R |
| STAT_KLEMMENSTATUS_BUS_KL_15_EIN_CAS | int | Klemmestatus Klemme 15 |
| STAT_KLEMMENSTATUS_BUS_KL_50_EIN_CAS | int | Klemmestatus Klemme 50 |
| STAT_KM_AKTUELL_WERT | real | aktueller Kilometerstand Bereich von 0 [KM] bis 0xffff [KM] |
| STAT_KM_AKTUELL_EINH | string | aktueller Kilometerstand Einheit: KM |
| STAT_LENKRADTASTER_HORN | int | Hupe Schalterstellung |
| STAT_SCHALTWIPPEN_POS_PLUS | int | SMG einen hoeheren Gang schalten (ziehen) |
| STAT_SCHALTWIPPEN_POS_MINUS | int | SMG einen niedrigeren Gang schalten (druecken) |
| STAT_ABBLENDSCHALT_BLINK_RE | int | Blinkerschalter Tippen rechts |
| STAT_ABBLENDSCHALT_BLINK_RE_DAUER | int | Blinkerschalter Dauerblinken rechts |
| STAT_ABBLENDSCHALT_BLINK_LI | int | Blinkerschalter Tippen links |
| STAT_ABBLENDSCHALT_BLINK_LI_DAUER | int | Blinkerschalter Dauerblinken links |
| STAT_ABBLENDSCHALT_FERNLICHT | int | Bit 4: FL Fernlicht |
| STAT_ABBLENDSCHALT_LICHTHUPE | int | Lichthupe |
| STAT_ABBLENDSCHALT_AXIAL_UNTEN | int | BC-Taste |
| STAT_ABBLENDSCHALT_AXIAL_OBEN | int | Kombi-Taste |
| STAT_ABBLENDSCHALT_UNGUELTIG | int | Blinker-Schalterstellung undefiniert |
| STAT_WISCHER_BEDIENMODI_INTERVALL_AUTOM | int | Scheibenwischerschalter Intervall |
| STAT_WISCHER_BEDIENMODI_STUFE_1 | int | Stufe 1 |
| STAT_WISCHER_BEDIENMODI_STUFE_2 | int | Stufe 2 |
| STAT_WISCHER_BEDIENMODI_TIPPWISCHEN | int | Tippwischen |
| STAT_WISCHER_BEDIENMODI_FRONTWASCHEN | int | Frontwaschen |
| STAT_WISCHER_BEDIENMODI_HECKWISCHEN | int | Heckwischen |
| STAT_WISCHER_BEDIENMODI_HECKWASCHEN | int | Heckwaschen |
| STAT_WISCHER_BEDIENPOTI_STUFE_1 | int | SWS, Wischerpoti Position 1 |
| STAT_WISCHER_BEDIENPOTI_STUFE_2 | int | SWS, Wischerpoti Position 2 |
| STAT_WISCHER_BEDIENPOTI_STUFE_3 | int | SWS, Wischerpoti Position 3 |
| STAT_WISCHER_BEDIENPOTI_STUFE_4 | int | SWS, Wischerpoti Position 4 |
| STAT_WISCHER_ROH_UNGUELTIG | int | Wischer-Schalterstellung undifiniert |
| STAT_WISCHER_KS_NACH_VCC | int | Wischer Kurzschluss Vcc |
| STAT_WISCHER_KS_NACH_MASSE | int | Wischer Kurzschluss Masse |
| STAT_WISCHER_BEDIENPOTI_UNGUELTIG | int | Wischer Potistellung undefiniert |
| STAT_LENKSAEULENVERSTSCHALTER_LAENGE_PLUS | int | Lenksaeulen-Laengenverstellung vor |
| STAT_LENKSAEULENVERSTSCHALTER_LAENGE_MINUS | int | Lenksaeulen-Laengenverstellung zurueck |
| STAT_LENKSAEULENVERSTSCHALTER_NEIGUNG_AUF | int | Lenksaeulen-NeigungsNeigungsverstellung vor |
| STAT_LENKSAEULENVERSTSCHALTER_NEIGUNG_AB | int | Lenksaeulen-Neigungsverstellung ab |
| STAT_LENKSAEULENVERSTSCHALTER_KS_NACH_VDD | int | LSV Kurzschluss nach VDD |
| STAT_LENKSAEULENVERSTSCHALTER_KS_NACH_VSS | int | LSV Kurzschluss nach Masse |
| STAT_LENKSAEULENVERSTSCHALTER_SPGSWERT_NICHT_DEF | int | LSV Schalterstellung undefiniert |
| STAT_LENKRADTASTER_MFL_PUSH_TO_TALK | int | MFL Push To Talk |
| STAT_LENKRADTASTER_MFL_VOL_UP | int | MFL Laustaerke lauter |
| STAT_LENKRADTASTER_MFL_VOL_DOWN | int | MFL Laustaerke leiser |
| STAT_LENKRADTASTER_MFL_TEL | int | MFL Telefon-Taste |
| STAT_LENKRADTASTER_MFL_PROG_2 | int | Prog.-Taste 2 |
| STAT_LENKRADTASTER_MFL_SUCHLAUF_AUF | int | MFL Suchlauf aufwaerts |
| STAT_LENKRADTASTER_MFL_SUCHLAUF_AB | int | MFL Suchlauf abwaerts |
| STAT_LENKRADTASTER_MFL_PROG_1 | int | Prog.-Taste 1 |
| STAT_LENKRADTASTER_MFL_LI_KS | int | MFL Kurzschluss links |
| STAT_LENKRADTASTER_MFL_RE_KS | int | MFL Kurzschluss rechts |
| STAT_LENKRADTASTER_MFL_LI_SPGSWERT_NICHT_DEF | int | MFL Schalterstellung links undefiniert |
| STAT_LENKRADTASTER_MFL_RE_SPGSWERT_NICHT_DEF | int | MFL Schalterstellungrechts undefiniert |
| STAT_LENKRADTASTER_MFL_LI_KS_NACH_VCC | int | MFL Kurzschluss nach Vcc links |
| STAT_LENKRADTASTER_MFL_LI_KS_NACH_MASSE | int | MFL Kurzschluss nach Masse links |
| STAT_LENKRADTASTER_MFL_RE_KS_NACH_VCC | int | MFL Kurzschluss nach Vcc rechts |
| STAT_LENKRADTASTER_MFL_RE_KS_NACH_MASSE | int | MFL Kurzschluss nach Masse rechts |
| STAT_SCHALTER_TEMPOMAT_HOR_TIPPEN_VORNE | int | FGR: Beschleunigen (kleines Inkrement) |
| STAT_SCHALTER_TEMPOMAT_HOR_UEBERDRUECKEN_VORNE | int | FGR: Beschleunigen (grosses Inkrement) |
| STAT_SCHALTER_TEMPOMAT_HOR_TIPPEN_HINTEN | int | FGR: Verzoegern (kleines Inkrement) |
| STAT_SCHALTER_TEMPOMAT_HOR_UEBERDRUECKEN_HINTEN | int | FGR: Verzoegern (grosses Inkrement) |
| STAT_SCHALTER_TEMPOMAT_HOR_TIPPEN_VORNE2 | int | FGR Redundanz: Beschleunigen (kleines Inkrement) |
| STAT_SCHALTER_TEMPOMAT_HOR_UEBERDRUECKEN_VORNE2 | int | FGR Redundanz: Beschleunigen (grosses Inkrement) |
| STAT_SCHALTER_TEMPOMAT_HOR_TIPPEN_HINTEN2 | int | FGR Redundanz: Verzoegern (kleines Inkrement) |
| STAT_SCHALTER_TEMPOMAT_HOR_UEBERDRUECKEN_HINTEN2 | int | FGR Redundanz: Verzoegern (grosses Inkrement) |
| STAT_SCHALTER_TEMPOMAT_VERTIKAL_TIPPEN_UNTEN | int | Tempomat aus |
| STAT_SCHALTER_TEMPOMAT_VERTIKAL_TIPPEN_OBEN | int | Tempomat aus |
| STAT_SCHALTER_ACC_RAENDEL_HOEHERER_ABSTAND | int | ACC: hoeherer Abstand |
| STAT_SCHALTER_ACC_RAENDEL_NIEDRIGERER_ABSTAND | int | ACC: niedrigerer Abstand |
| STAT_SCHALTER_TEMPOMAT_ACC_ABRUF | int | ACC Abruf |
| STAT_SCHALTER_TEMPOMAT_UNDEFINIERT_HORIZONTAL | int | FGR-Schalterstellung horizontal undefiniert |
| STAT_SCHALTER_TEMPOMAT_UNDEFINIERT_VERTIKAL | int | FGR-Schalterstellung vertiktal undefiniert |
| STAT_SCHALTER_TEMPOMAT_UNDEFINIERT_AXIAL | int | FGR-Schalterstellung axial undefiniert |
| STAT_SCHALTER_TEMPOMAT_KS_NACH_PLUS_BESCHLEUNIGEN | int | FGR Beschleunigung Kurzschluss nach Vcc |
| STAT_SCHALTER_TEMPOMAT_KS_NACH_MASSE_BESCHLEUNIGEN | int | FGR Beschleunigung Kurzschluss nach Masse |
| STAT_SCHALTER_TEMPOMAT_KS_NACH_PLUS_VERZOEGERN | int | FGR Verzoegern Kurzschluss nach Vcc |
| STAT_SCHALTER_TEMPOMAT_KS_NACH_MASSE_VERZOEGERN | int | FGR Verzoegern Kurzschluss nach Masse |
| STAT_LENKRADTASTER_ROH_HORN | int | Hupe-Stellung, Invertiert: 1=Aus, 0=Ein |
| STAT_HUPE_ANST_KS_UNTERBR_HOCHTON | int | Hupe Kurzschluss Hochton, 1=Fehler aktiv, 0=Fehler inaktiv |
| STAT_HUPE_ANST_KS_UNTERBR_TIEFTON | int | Hupe Kurzschluss Tiefton, 1=Fehler aktiv, 0=Fehler inaktiv |
| STAT_SCHALTWIPPEN_ROH_PLUS | int | SMG einen hoeheren Gang schalten (Rohdaten) |
| STAT_SCHALTWIPPEN_ROH_MINUS | int | SMG einen niedrigeren Gang schalten (Rohdaten) |
| STAT_LENKRADHEIZUNG_ROH_TASTER_LENKRAD | int | für Entwicklung vorgesehen, Invertiert: 1=Aus, 0=Ein |
| STAT_ABBLENDSCHALT_ROH_DIGITAL_0 | int | Bit 0: FAS Rohdaten Digitalkanal 0 |
| STAT_ABBLENDSCHALT_ROH_DIGITAL_1 | int | Bit 1: FAS Rohdaten Digitalkanal 1 |
| STAT_ABBLENDSCHALT_ROH_DIGITAL_2 | int | Bit 2: FAS Rohdaten Digitalkanal 2 |
| STAT_ABBLENDSCHALT_ROH_FERNLICHT | int | Bit 3: FAS Rohdaten Fernlicht |
| STAT_ABBLENDSCHALT_ROH_LICHTHUPE | int | Bit 4: FAS Rohdaten Lichthupe |
| STAT_ABBLENDSCHALT_ROH_AXIAL_UNTEN | int | Bit 5: FAS Rohdaten BC-Taste |
| STAT_ABBLENDSCHALT_ROH_AXIAL_OBEN | int | Bit 6: FAS Rohdaten Kombi-Taste |
| STAT_WISCHER_ROH_FRONTWASCHEN | int | Bit 0: FAS Rohdaten Frontwaschen |
| STAT_WISCHER_ROH_HECKWISCHEN | int | Bit 1: FAS Rohdaten Heckwischen |
| STAT_WISCHER_ROH_HECKWASCHEN | int | Bit 2: FAS Rohdaten Heckwaschen |
| STAT_WISCHER_ROH_TIPPWISCHEN_STUFE_1 | int | Bit 3: FAS Rohdaten Tippwischen |
| STAT_WISCHER_ROH_STUFE_1_STUFE_2 | int | Bit 4: FAS Rohdaten Stufe 1_2 |
| STAT_WISCHER_ROH_REGENSENSOR | int | Bit 5: FAS Rohdaten Regensensor |
| STAT_WISCHER_ROH_SPANNUNG_WERT | real | SWS Spannung Rohdaten Wertbereich 0..255 entspricht 0..5V Bereich von 0 [Volt] bis 5 [Volt] |
| STAT_WISCHER_ROH_SPANNUNG_EINH | string | SWS Spannung Rohdaten Wertbereich 0..255 entspricht 0..5V Einheit: Volt |
| STAT_SCHALTER_TEMPOMAT_ROH_DIGITAL_0 | int | Bit 0: FGR Rohdaten Digitalkanal 0 |
| STAT_SCHALTER_TEMPOMAT_ROH_DIGITAL_1 | int | Bit 1: FGR Rohdaten Digitalkanal 1 |
| STAT_SCHALTER_TEMPOMAT_ROH_DIGITAL_2 | int | Bit 2: FGR Rohdaten Digitalkanal 2 |
| STAT_SCHALTER_TEMPOMAT_ROH_DIGITAL_3 | int | Bit 3: FGR Rohdaten Digitalkanal 3 |
| STAT_SCHALTER_TEMPOMAT_ROH_DIGITAL_4 | int | Bit 4: FGR Rohdaten Digitalkanal 4 |
| STAT_SCHALTER_TEMPOMAT_ROH_DIGITAL_5 | int | Bit 5: FGR Rohdaten Digitalkanal 5 |
| STAT_SCHALTER_TEMPOMAT_ROH_HOR_SPG_ANALOG_1_WERT | real | FGR Beschleinigen Spannung Rohdaten Wertbereich 0..255 entspricht 0..5V Bereich von 0 [Volt] bis 5 [Volt] |
| STAT_SCHALTER_TEMPOMAT_ROH_HOR_SPG_ANALOG_1_EINH | string | FGR Beschleinigen Spannung Rohdaten Wertbereich 0..255 entspricht 0..5V Einheit: Volt |
| STAT_SCHALTER_TEMPOMAT_ROH_HOR_SPG_ANALOG_2_WERT | real | FGR Verzoegern Spannung Rohdaten Wertbereich 0..255 entspricht 0..5V Bereich von 0 [Volt] bis 5 [Volt] |
| STAT_SCHALTER_TEMPOMAT_ROH_HOR_SPG_ANALOG_2_EINH | string | FGR Verzoegern Spannung Rohdaten Wertbereich 0..255 entspricht 0..5V Einheit: Volt |
| STAT_LENKSAEULENVERSTSCHALTER_ROH_SPG_WERT | real | LSV Horizontal Spannung Rohdaten Wertbereich 0..255 entspricht 0..5V Bereich von 0 [Volt] bis 5 [Volt] |
| STAT_LENKSAEULENVERSTSCHALTER_ROH_SPG_EINH | string | LSV Horizontal Spannung Rohdaten Wertbereich 0..255 entspricht 0..5V Einheit: Volt |
| STAT_LENKRADTASTER_MFL_ROH_LI_SPG_WERT | real | MFL Spannung links Rohdaten Wertbereich 0..255 entspricht 0..5V Bereich von 0 [Volt] bis 5 [Volt] |
| STAT_LENKRADTASTER_MFL_ROH_LI_SPG_EINH | string | MFL Spannung links Rohdaten Wertbereich 0..255 entspricht 0..5V Einheit: Volt |
| STAT_LENKRADTASTER_MFL_ROH_RE_SPG_WERT | real | MFL Spannung rechts Rohdaten Wertbereich 0..255 entspricht 0..5V Bereich von 0 [Volt] bis 5 [Volt] |
| STAT_LENKRADTASTER_MFL_ROH_RE_SPG_EINH | string | MFL Spannung rechts Rohdaten Wertbereich 0..255 entspricht 0..5V Einheit: Volt |
| STAT_ABBLENDS_GESAMT_1_WERT | int | FAS Schalterstellung table SG_Status_FAS_Gesamt1 WERT |
| STAT_ABBLENDS_GESAMT_1_TEXT | string | FAS Schalterstellung table SG_Status_FAS_Gesamt1 TEXT |
| STAT_ABBLENDS_GESAMT_2_WERT | int | FAS Schalterstellung table SG_Status_FAS_Gesamt2 WERT |
| STAT_ABBLENDS_GESAMT_2_TEXT | string | FAS Schalterstellung table SG_Status_FAS_Gesamt2 TEXT |
| STAT_WISCHERS_GESAMT_1_WERT | int | SWS table SG_Status_SWS_Gesamt1 WERT |
| STAT_WISCHERS_GESAMT_1_TEXT | string | SWS table SG_Status_SWS_Gesamt1 TEXT |
| STAT_WISCHERS_GESAMT_2_WERT | int | SWS table SG_Status_SWS_Gesamt2 WERT |
| STAT_WISCHERS_GESAMT_2_TEXT | string | SWS table SG_Status_SWS_Gesamt2 TEXT |
| STAT_WISCHERS_GESAMT_3_WERT | int | SWS table SG_Status_SWS_Gesamt3 WERT |
| STAT_WISCHERS_GESAMT_3_TEXT | string | SWS table SG_Status_SWS_Gesamt3 TEXT |
| STAT_TEMPOMAT_ACC_GESAMT_1_WERT | int | FGR, ACC table SG_Status_FGR_Gesamt1 WERT |
| STAT_TEMPOMAT_ACC_GESAMT_1_TEXT | string | FGR, ACC table SG_Status_FGR_Gesamt1 TEXT |
| STAT_TEMPOMAT_ACC_GESAMT_2_WERT | int | FGR, ACC table SG_Status_FGR_Gesamt2 WERT |
| STAT_TEMPOMAT_ACC_GESAMT_2_TEXT | string | FGR, ACC table SG_Status_FGR_Gesamt2 TEXT |
| STAT_TEMPOMAT_ACC_GESAMT_3_WERT | int | FGR, ACC table SG_Status_FGR_Gesamt3 WERT |
| STAT_TEMPOMAT_ACC_GESAMT_3_TEXT | string | FGR, ACC table SG_Status_FGR_Gesamt3 TEXT |
| STAT_TEMPOMAT_ACC_GESAMT_4_WERT | int | FGR, ACC table SG_Status_FGR_Gesamt4 WERT |
| STAT_TEMPOMAT_ACC_GESAMT_4_TEXT | string | FGR, ACC table SG_Status_FGR_Gesamt4 TEXT |
| STAT_LSVS_GESAMT_1_WERT | int | LSV table SG_Status_LSV_Gesamt1 WERT |
| STAT_LSVS_GESAMT_1_TEXT | string | LSV table SG_Status_LSV_Gesamt1 TEXT |
| STAT_MFL_GESAMT_1_WERT | int | MFL table SG_Status_MFL_Gesamt1 WERT |
| STAT_MFL_GESAMT_1_TEXT | string | MFL table SG_Status_MFL_Gesamt1 TEXT |
| STAT_MFL_GESAMT_2_WERT | int | MFL table SG_Status_MFL_Gesamt2 WERT |
| STAT_MFL_GESAMT_2_TEXT | string | MFL table SG_Status_MFL_Gesamt2 TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lenkradheizung"></a>
### STATUS_LENKRADHEIZUNG

mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LENKRADHEIZUNG_SPNG_TEMPERATURSENSOR_WERT | real | Ausgangsspannung des Temperatursensors Bereich von 0 [Volt] bis 5 [Volt] |
| STAT_LENKRADHEIZUNG_SPNG_TEMPERATURSENSOR_EINH | string | Ausgangsspannung des Temperatursensors Einheit: Volt |
| STAT_LENKRADHEIZUNG_SPNG_STROMSENSOR_WERT | real | Ausgangsspannung des Stromsensors Bereich von 0 [VOLT] bis 5 [VOLT] |
| STAT_LENKRADHEIZUNG_SPNG_STROMSENSOR_EINH | string | Ausgangsspannung des Stromsensors Einheit: VOLT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta-daten-lesen"></a>
### STATUS_FASTA_DATEN_LESEN

mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BELICHTUNGSZEIT_MIN_WERT | real | Belichtungszeit Min Bereich von 0 [ohne] bis 65535 [ohne] |
| STAT_BELICHTUNGSZEIT_MIN_EINH | string | Belichtungszeit Min Einheit: ohne |
| STAT_BELICHTUNGSZEIT_MAX_WERT | real | Belichtungszeit Max Bereich von 0 [ohne] bis 65535 [ohne] |
| STAT_BELICHTUNGSZEIT_MAX_EINH | string | Belichtungszeit Max Einheit: ohne |
| STAT_BELICHTUNGSZEIT_MITTELWERT_WERT | real | Belichtungszeit Mittelwert Bereich von 0 [ohne] bis 65535 [ohne] |
| STAT_BELICHTUNGSZEIT_MITTELWERT_EINH | string | Belichtungszeit Mittelwert Einheit: ohne |
| STAT_LED_STROM_MIN_WERT | real | LED-Strom Min Bereich von 0 [ohne] bis 255 [ohne] |
| STAT_LED_STROM_MIN_EINH | string | LED-Strom Min Einheit: ohne |
| STAT_LED_STROM_MAX_WERT | real | LED-Strom Max Bereich von 0 [ohne] bis 255 [ohne] |
| STAT_LED_STROM_MAX_EINH | string | LED-Strom Max Einheit: ohne |
| STAT_POS_REFERENZSPUR_MIN_WERT | real | Referenzspur Min Bereich von 0 [ohne] bis 255 [ohne] |
| STAT_POS_REFERENZSPUR_MIN_EINH | string | Referenzspur Min Einheit: ohne |
| STAT_POS_REFERENZSPUR_MAX_WERT | real | Referenzspur Max Bereich von 0 [ohne] bis 255 [ohne] |
| STAT_POS_REFERENZSPUR_MAX_EINH | string | Referenzspur Max Einheit: ohne |
| STAT_REFERENZSPUR1_KONTRAST_MIN_WERT | real | Referenzspur1 Kontrast Min Bereich von 0 [ohne] bis 255 [ohne] |
| STAT_REFERENZSPUR1_KONTRAST_MIN_EINH | string | Referenzspur1 Kontrast Min Einheit: ohne |
| STAT_REFERENZSPUR1_KONTRAST_MAX_WERT | real | Referenzspur1 Kontrast Max Bereich von 0 [ohne] bis 255 [ohne] |
| STAT_REFERENZSPUR1_KONTRAST_MAX_EINH | string | Referenzspur1 Kontrast Max Einheit: ohne |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sw-version"></a>
### STATUS_SW_VERSION

Seriennummer Lenkradelektronik auslesen KWP2000: $22 Steuergeraetespezifische Daten lesen $0006 Seriennummer LRE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LK_HW_INDEX | int | Kostal Hardware-Index, 1 Byte |
| STAT_LK_SW_INDEX_MAIN | int | Kostal Software-Index des Main-Controllers, 1 Byte |
| STAT_LK_SW_INDEX_SUB | int | Kostal Software-Index des Sub-Controllers, 1 Byte |
| STAT_LK_SW_INDEX_EEPROM | int | Kostal Software-Index des EEPROM, 1 Byte |
| STAT_SERIENNUMMER | string | Seriennummer des SZL, 4 Byte |
| STAT_SW_BEZEICHNUNG_MAIN | string | Softwarebezeichnung des Main-Controllers, 5 Byte |
| STAT_SW_BEZEICHNUNG_SUB | string | Softwarebezeichnung des Sub-Controllers, 5 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-lenkwinkelsensor-ruecksetzen"></a>
### ABGLEICH_LENKWINKELSENSOR_RUECKSETZEN

Abgleichen des Lenkwinkelsensors zuruecksetzen KWP2000: $31 Steuergeraetespezifische Routine starten $44 Lenkwinkelsensor abgleichen ruecksetzen Modus  : Default Vor ABGLEICH_LENKWINKELSENSOR muss dieser Job ausgefuehrt werden!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-lenkwinkelsensor"></a>
### ABGLEICH_LENKWINKELSENSOR

Abgleichen des Lenkwinkelsensors bei Lenkrad-Geradeausstellung KWP2000: $31 Steuergeraetespezifische Routine starten $43 Lenkwinkelsensor abgleichen Modus  : Default Vor diesem Job muss ABGLEICH_LENKWINKELSENSOR_RUECKSETZEN ausgefuehrt werden!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lws-offset-korrektur-schreiben-grad"></a>
### LWS_OFFSET_KORREKTUR_SCHREIBEN_GRAD

Abgleichen des Lenkwinkelsensors bei Lenkrad-Geradeausstellung incl. Wasserwaagenoffset KWP2000: $31 Steuergeraetespezifische Routine starten $47 Lenkwinkelsensor-Feinabgleich Modus  : Default Als Argument wird der Wasserwaagen-Offset uebergeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OFFSET | real | Wasserwaagen-Offset, Wertebereich: -0.800° bis +0.800° Unbedingt einen Punkt als Dezimaltrennzeichen benutzen Format: -0.200 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lenkradheizung"></a>
### STEUERN_LENKRADHEIZUNG

Ansteuern der Lenkradheizung KWP2000: $31 Steuergeraetespezifische Routine starten $45 Funktionsbeleuchtung ansteuern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LENKRADHEIZUNG | string | "ein" -&gt; Heizung einschalten "aus" -&gt; Heizung ausschalten table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hupe"></a>
### STEUERN_HUPE

Ansteuern von Hupe KWP2000: $31 Steuergeraetespezifische Routine starten $40 Hupe ansteuern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HUPEN_TOENER1 | string | "ein" -&gt; Hupe einschalten "aus" -&gt; Hupe ausschalten Bit 0 table DigitalArgument TEXT |
| HUPEN_TOENER2 | string | "ein" -&gt; Hupe einschalten "aus" -&gt; Hupe ausschalten Bit 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-funktionsbeleuchtung"></a>
### STEUERN_FUNKTIONSBELEUCHTUNG

Ansteuern der Funktionsbeleuchtung KWP2000: $31 Steuergeraetespezifische Routine starten $42 Funktionsbeleuchtung ansteuern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BELEUCHTUNG | string | "ein" -&gt; LEDs einschalten "aus" -&gt; LEDs ausschalten table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dimmbeleuchtung"></a>
### STEUERN_DIMMBELEUCHTUNG

Ansteuern der Dimmbeleuchtung KWP2000: $31 Steuergeraetespezifische Routine starten $41 Dimmbeleuchtung steuern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIMMBELEUCHTUNGSWERT | unsigned int | Beleuchtungswert Bereich: 0 bis 253 -&gt; Nachtbeleuchtung Bereich: 254 -&gt; Tag (Lichtschalter aus) Bereich: 255 -&gt; Signal fehlerhaft, Licht aus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-blinkerschalter"></a>
### STEUERN_BLINKERSCHALTER

Ansteuern des Blinkerschalters KWP2000: $31 Steuergeraetespezifische Routine starten $42 Funktionsbeleuchtung ansteuern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTION | string | "RUHESTELLUNG" -&gt; Ruhestellung "UNGUELTIG" -&gt; Ungueltig "BLINKER_LINKS" -&gt; Blinker links einschalten "BLINKER_RECHTS" -&gt; Blinker rechts einschalten "LICHTHUPE" -&gt; Lichthupe einschalten table SG_Steuern_FAS TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-luz-null-setzen"></a>
### LUZ_NULL_SETZEN

Lenkradumdehungszahl auf Null setzen KWP2000: 0x31 0x48 Modus:   Default  Notwendig nach Codierung in der Produktion: umbedingt auf Geradeausstellung der Räder und des Lenkrades achten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lenkwinkelsensor"></a>
### STATUS_LENKWINKELSENSOR

mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LENKWINKEL_WERT | real | Je nach Lenkwinkelstatus, wird absoluter Lenkwinkeloder relativer Lenkwinkel oder ungueltig (=32768) ausgegeben Bereich von -32767 [Grad/s] bis +32767 [Grad/s] |
| STAT_LENKWINKEL_EINH | string | Je nach Lenkwinkelstatus, wird absoluter Lenkwinkeloder relativer Lenkwinkel oder ungueltig (=32768) ausgegeben Einheit: Grad |
| STAT_LENKWINKELSTATUS_WERT | int | Lenkwinkelstatus: relativ, absolut oder fehlerhaft table SG_Status_Lenkwinkel WERT |
| STAT_LENKWINKELSTATUS_TEXT | string | Lenkwinkelstatus: relativ, absolut oder fehlerhaft table SG_Status_Lenkwinkel TEXT |
| STAT_NULLPUNKT_ABGEGLICHEN | int | Nullpunktabgleich-Status |
| STAT_AUFSETZEN_GESPERRT | int | Aufsetz-Status |
| STAT_AKTUELLE_RUNDE_WERT | real | Aktuelle Softwarerunde Bereich von -2 [Umdrehungen] bis +2 [Umdrehungen], ungueltig: -128 |
| STAT_AKTUELLE_RUNDE_EINH | string | Aktuelle Softwarerunde Einheit: Umdrehungen |
| STAT_KORREKTURRUNDE_WERT | real | Korrekturrunde Bereich von -2 [Umdrehungen] bis +2 [Umdrehungen], ungueltig: -128 |
| STAT_KORREKTURRUNDE_EINH | string | Korrekturrunde Einheit: Umdrehungen |
| STAT_LENKRAD_WINKELGESCHWINDIGKEIT_WERT | real | Lenkwinkelgeschwindigkeit Bereich von -32767 [Grad/s] bis +32767 [Grad/s] |
| STAT_LENKRAD_WINKELGESCHWINDIGKEIT_EINH | string | Lenkwinkelgeschwindigkeit Einheit: Grad/s |
| STAT_ABGLEICH_OFFSET_WERT | real | Abgleich-Offset Bereich von 0 [Grad] bis +360 [Grad], ungueltig: 32768 |
| STAT_ABGLEICH_OFFSET_EINH | string | Abgleich-Offset Einheit: Grad |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
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
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (63 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (5 × 9)
- [FARTTYP](#table-farttyp) (1 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (6 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (24 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (5 × 9)
- [IARTTYP](#table-iarttyp) (1 × 5)
- [IARTTEXTEINDIVIDUELL](#table-iarttexteindividuell) (17 × 2)
- [SG_STATUS_LENKRADHEIZUNG_ANSTEUERUNG](#table-sg-status-lenkradheizung-ansteuerung) (5 × 2)
- [SG_STATUS_LENKRADHEIZUNG_SENSOR](#table-sg-status-lenkradheizung-sensor) (2 × 2)
- [SG_STEUERN_FAS](#table-sg-steuern-fas) (5 × 2)
- [SG_STATUS_LENKWINKEL](#table-sg-status-lenkwinkel) (4 × 2)
- [FUMWELTTEXTE_KLEMMENSTATUS](#table-fumwelttexte-klemmenstatus) (1 × 5)
- [KLEMMENSTATUS_R](#table-klemmenstatus-r) (4 × 2)
- [KLEMMENSTATUS_15](#table-klemmenstatus-15) (4 × 2)
- [KLEMMENSTATUS_50](#table-klemmenstatus-50) (4 × 2)
- [KLEMMENSTATUS_TIMEOUT](#table-klemmenstatus-timeout) (2 × 2)
- [SG_STATUS_FAS_GESAMT1](#table-sg-status-fas-gesamt1) (8 × 2)
- [SG_STATUS_FAS_GESAMT2](#table-sg-status-fas-gesamt2) (4 × 2)
- [SG_STATUS_SWS_GESAMT1](#table-sg-status-sws-gesamt1) (8 × 2)
- [SG_STATUS_SWS_GESAMT2](#table-sg-status-sws-gesamt2) (2 × 2)
- [SG_STATUS_SWS_GESAMT3](#table-sg-status-sws-gesamt3) (6 × 2)
- [SG_STATUS_FGR_GESAMT1](#table-sg-status-fgr-gesamt1) (5 × 2)
- [SG_STATUS_FGR_GESAMT2](#table-sg-status-fgr-gesamt2) (2 × 2)
- [SG_STATUS_FGR_GESAMT3](#table-sg-status-fgr-gesamt3) (3 × 2)
- [SG_STATUS_FGR_GESAMT4](#table-sg-status-fgr-gesamt4) (3 × 2)
- [SG_STATUS_LSV_GESAMT1](#table-sg-status-lsv-gesamt1) (5 × 2)
- [SG_STATUS_MFL_GESAMT1](#table-sg-status-mfl-gesamt1) (5 × 2)
- [SG_STATUS_MFL_GESAMT2](#table-sg-status-mfl-gesamt2) (5 × 2)

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

Dimensions: 63 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x94C1 | Codierdaten CRC Fehler |
| 0x94EC | Multifunktionslenkrad (MFL) Analogport Links Kurzschluß |
| 0x94ED | Multifunktionslenkrad (MFL)  Analogport Rechts Kurzschluß |
| 0x94EE | Multifunktionslenkrad (MFL)  Schalter Links unplausibel |
| 0x94EF | Multifunktionslenkrad (MFL)  Schalter  Rechts unplausibel |
| 0x94F0 | Lenkradheizung (LHZ)  Heizmatte unterbrochen |
| 0x94F1 | Lenkradheizung (LHZ) Heizmatte Kurzschluß nach Masse |
| 0x94F3 | Lenkradheizung (LHZ) Fehler Regelung |
| 0x94F4 | Lenkradheizung (LHZ) Temperatur-Fühler unterbrochen |
| 0x94F5 | Lenksäulenverstellung (LSV)  Analogport Kurzschluß nach Masse |
| 0x94F6 | Lenksäulenverstellung (LSV)  Analogport Kurzschluß nach Plus |
| 0x94F7 | Lenksäulenverstellung (LSV)  Unplausibel |
| 0x94F8 | Hupe Fehler Hochtöner |
| 0x94F9 | Hupe Fehler Tieftöner |
| 0x9501 | Lenkwinkelsensor: Sensor nicht abgeglichen |
| 0x950B | Energiesparmode aktiv |
| 0x951A | System Unterspannung |
| 0x951B | System Ueberspannung |
| 0x951D | Fahrtrichtungsabblendlichtschalter (FAS) Schalter unplausibel |
| 0x951E | Fahrtrichtungsabblendlichtschalter (FAS) Schalter Hängt |
| 0x951F | Multifunktionslenkrad (MFL) Schalter Links Hängt |
| 0x9520 | Multifunktionslenkrad (MFL)  Schalter Rechts Hängt |
| 0x9521 | Schaltwippen (SMG) Schalter Hängt |
| 0xA848 | Tempomatschalter  (FGR/ACC)  Hängt |
| 0xA849 | Tempomatschalter  (FGR/ACC) Horizontal unplausibel |
| 0xA84A | Tempomatschalter  (FGR/ACC) Vertikal Unplausibel |
| 0xA84B | Tempomatschalter  (ACC) ACC-Rändel / Axial Tippen unplausibel |
| 0xA84C | Tempomatschalter  (FGR/ACC) Analogport Kurzschluß Masse |
| 0xA84D | Tempomatschalter  (FGR/ACC) Analogport Kurzschluß Plus |
| 0xA84E | FGR redundanter Analogport Kurzschluß nach Masse |
| 0xA84F | Tempomatschalter  (FGR/ACC) redundanter Analogport Kurzschluß nach Plus |
| 0xA850 | Scheibenwischerschalter (SWS) Hängt |
| 0xA851 | Scheibenwischerschalter (SWS) unplausibel |
| 0xA852 | Scheibenwischerschalter (SWS) Analogport Kurzschluß nach Masse |
| 0xA853 | Scheibenwischerschalter (SWS)  Analogport Kurzschluß nach Plus |
| 0xA854 | Scheibenwischerschalter (SWS)  Intervall-Rändel unplausibel |
| 0xA855 | Lenkradheizung (LHZ) Schalter hängt |
| 0xA856 | Lenksäulenverstellung (LSV) Schalter hängt |
| 0xA857 | Hupe Schalter Hängt |
| 0xA858 | Codierdatenblock des Synthetischen Lenkwinkel ist inkompatibel zur Variante |
| 0xA859 | Softwareindex des Sub ist inkompatibel |
| 0xA85A | Softwareindex des Eprom ist inkompatibel |
| 0xA85B | Softwareindex des Main ist inkompatibel |
| 0xA85C | PT-Wecken Kurzschluss |
| 0xA85D | Lenkwinkelsensor defekt |
| 0xA85E | Fahrgestellnummer unplausibel |
| 0xC987 | PT-CAN SZL keine Botschaften Bus-Off |
| 0xC98B | F-CAN SZL keine Botschaften Bus-Off |
| 0xC994 | F-CAN SZL Radgeschwindigkeit, Kommunikation mit DSC, Timeout |
| 0xC995 | F-CAN SZL Radgeschwindigkeit Plausibilitaet, Kommunikation mit DSC, Radgeschwindigkeit &gt; 320 km/h |
| 0xC996 | F-CAN SZL Radgeschwindigkeit Plausibilitaet, Kommunikation mit DSC, Radgeschwindigkeit &lt; -320 km/h |
| 0xC998 | F-CAN SZL Radtoleranzabgleich Plausibilitaet, Kommunikation mit DSC, Radtoleranzabgleich &lt; -5% |
| 0xC99A | F-CAN SZL Radtoleranzabgleich Plausibilitaet, Kommunikation mit DSC, Radtoleranzabgleich &gt; 5% |
| 0xC99B | F-CAN SZL Sync, keine Kommunikation mit DSC, Timeout... |
| 0xC99C | FCAN Botschaft: Exchange AFS DSC-Timeout |
| 0xC9A4 | PTCAN Botschaft: Außentemperatur/Relativzeit-Timeout |
| 0xC9A5 | PTCAN Botschaft: Bedienung Sonderfunktion-Timeout |
| 0xC9A6 | PTCAN Botschaft: Kilometerstand Timeout |
| 0xC9A7 | PTCAN Botschaft: Dimmung-Timeout |
| 0xC9A8 | PTCAN Botschaft: Powermanagement Verbrauchersteuerung-Timeout |
| 0xC9A9 | PT-CAN SZL, Klemmenstatus, keine Kommunikation mit CAS, Timeout |
| 0xC9AA | PT-CAN Botschaft: Radtoleranzabgleich-Timeout |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | ja |
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
| default | FUmweltTexte_Klemmenstatus | 0x02 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x02 | Betriebsspannung | Volt | - | unsigned char | - | 0,08 | 1 | 0 |
| 0x11 | Klemmenstatus_Klemme_R | 0-n | - | 0x03 | Klemmenstatus_R | - | - | - |
| 0x12 | Klemmenstatus_Klemme_15 | 0-n | - | 0x0C | Klemmenstatus_15 | - | - | - |
| 0x13 | Klemmenstatus_Klemme_50 | 0-n | - | 0x30 | Klemmenstatus_50 | - | - | - |
| 0x14 | Klemmenstatus_Timeout | 0-n | - | 0x40 | Klemmenstatus_Timeout | - | - | - |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 1 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| default | 0x0008 | 0x0004 | 0x0002 | 0x0001 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 6 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | Kein Fehler |
| 0x0001 | oberer Grenzwert ueberschritten |
| 0x0002 | unterer Grenzwert unterschritten |
| 0x0004 | kein Signal Kommunikation |
| 0x0008 | unplausibles Signal |
| 0xFFFF | unbekannte Fehlerart |

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

Dimensions: 24 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x2711 | Lenkwinkelsensor : Sensorfehler - Synchronisation mit Sub nicht möglich |
| 0x2712 | Lenkwinkelsensor : Sensorfehler - Verbindungstest zur PDA |
| 0x2713 | Lenkwinkelsensor : Sensorfehler - Umgebungshelligkeit zu hoch |
| 0x2714 | Lenkwinkelsensor : Sensorfehler - keine Referenzspur gefunden |
| 0x2715 | Lenkwinkelsensor : Sensorfehler - Referenzspurabstand außerhalb Toleranzband |
| 0x2716 | Lenkwinkelsensor : Sensorfehler - Illegaler Code |
| 0x2717 | Lenkwinkelsensor : Sensorfehler - Winkelsprung zu gross |
| 0x2718 | Lenkwinkelsensor : Sensorfehler - Lenkwinkel-Messbereich |
| 0x2719 | Lenkwinkelsensor: Fehler Winkelverifizierung |
| 0x2734 | EEPROM Defekt (Kein Zugriff möglich) |
| 0x2735 | A/D-Wandler des Main Defekt |
| 0x2736 | ROM des Main Defekt |
| 0x2737 | RAM des Main Defekt |
| 0x2738 | Watchdog Defekt |
| 0x273F | CPU Main defekt |
| 0x2742 | A/D-Wandler Sub defekt |
| 0x2743 | ROM Sub defekt |
| 0x2744 | RAM Sub defekt |
| 0x2745 | CPU Sub defekt |
| 0x274D | Synthetischer  Lenkwinkel Unplausibel |
| 0x274E | PT-Wecken unplausibel |
| 0x274F | Power On Reset |
| 0x2750 | Aufsetzen Geschwindigkeit Max |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | ja |
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
| default | FUmweltTexte_Klemmenstatus | 0x02 | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x02 | Betriebsspannung | Volt | - | unsigned char | - | 0,08 | 1 | 0 |
| 0x11 | Klemmenstatus_Klemme_R | 0-n | - | 0x03 | Klemmenstatus_R | - | - | - |
| 0x12 | Klemmenstatus_Klemme_15 | 0-n | - | 0x0C | Klemmenstatus_15 | - | - | - |
| 0x13 | Klemmenstatus_Klemme_50 | 0-n | - | 0x30 | Klemmenstatus_50 | - | - | - |
| 0x14 | Klemmenstatus_Timeout | 0-n | - | 0x40 | Klemmenstatus_Timeout | - | - | - |

<a id="table-iarttyp"></a>
### IARTTYP

Dimensions: 1 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| default | 0x0008 | 0x0004 | 0x0002 | 0x0001 |

<a id="table-iarttexteindividuell"></a>
### IARTTEXTEINDIVIDUELL

Dimensions: 17 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | Kein Fehler |
| 0x0001 | oberer Grenzwert ueberschritten |
| 0x0002 | unterer Grenzwert unterschritten |
| 0x0004 | kein Signal Kommunikation |
| 0x0008 | unplausibles Signal |
| 0x0003 | mechanischer Fehler |
| 0x0005 | keine Grundeinstellung |
| 0x0006 | Kurzschluss nach Plus |
| 0x0007 | Kurzschluss nach Masse |
| 0x0009 | Unterbrechung Kurzschluss Masse |
| 0x000A | Unterbrechung Kurzschluss Plus |
| 0x000B | Unterbrechung |
| 0x000C | elektrischer Fehler im Stromkreis |
| 0x000D | Fehlerspeicher auslesen |
| 0x000E | defekt |
| 0x000F | Zur Zeit nicht pruefbar |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-sg-status-lenkradheizung-ansteuerung"></a>
### SG_STATUS_LENKRADHEIZUNG_ANSTEUERUNG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x10 | KURZSCHLUSS_KL_30 |
| 0x20 | KURZSCHLUSS_KL_31 |
| 0x40 | UNTERBRECHUNG_HEIZMATTE |
| 0x60 | TIMEOUT_REGELUNG |

<a id="table-sg-status-lenkradheizung-sensor"></a>
### SG_STATUS_LENKRADHEIZUNG_SENSOR

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x80 | FEHLERHAFT |

<a id="table-sg-steuern-fas"></a>
### SG_STEUERN_FAS

Dimensions: 5 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| RUHESTELLUNG | 0x00 |
| UNGUELTIG | 0x01 |
| BLINKER_LINKS | 0x02 |
| BLINKER_RECHTS | 0x03 |
| LICHTHUPE | 0x04 |

<a id="table-sg-status-lenkwinkel"></a>
### SG_STATUS_LENKWINKEL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ABSOLUT |
| 0x01 | RELATIV |
| 0x02 | FEHLERHAFT |
| 0x03 | UNGUELTIG |

<a id="table-fumwelttexte-klemmenstatus"></a>
### FUMWELTTEXTE_KLEMMENSTATUS

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x14 | 0x13 | 0x12 | 0x11 |

<a id="table-klemmenstatus-r"></a>
### KLEMMENSTATUS_R

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Aus |
| 0x01 | Ein |
| 0x02 | Ungueltig |
| 0x03 | Ungueltig |

<a id="table-klemmenstatus-15"></a>
### KLEMMENSTATUS_15

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Aus |
| 0x04 | Ein |
| 0x08 | Ungueltig |
| 0x0C | Ungueltig |

<a id="table-klemmenstatus-50"></a>
### KLEMMENSTATUS_50

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Aus |
| 0x10 | Ein |
| 0x20 | Ungueltig |
| 0x30 | Ungueltig |

<a id="table-klemmenstatus-timeout"></a>
### KLEMMENSTATUS_TIMEOUT

Dimensions: 2 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0 | Nicht aktiv |
| 0x1 | Aktiv |

<a id="table-sg-status-fas-gesamt1"></a>
### SG_STATUS_FAS_GESAMT1

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x01 | BLINK_RE_TIPP |
| 0x02 | BLINK_RE_DAUER |
| 0x04 | BLINK_LI_TIPP |
| 0x08 | BLINK_LI_DAUER |
| 0x10 | FERNLICHT |
| 0x20 | LICHTHUPE |
| - | MEHRFACHBETAETIGUNG |

<a id="table-sg-status-fas-gesamt2"></a>
### SG_STATUS_FAS_GESAMT2

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x40 | AXIAL_TASTER_UNTEN_GEDR |
| 0x80 | AXIAL_TASTER_OBEN_GEDR |
| 0xc0 | AXIAL_TASTER_BEIDE_GEDR |

<a id="table-sg-status-sws-gesamt1"></a>
### SG_STATUS_SWS_GESAMT1

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x02 | STUFE1 |
| 0x04 | STUFE2 |
| 0x08 | TIPPWISCHEN_GEDR |
| 0x10 | FRONTWASCHEN_GEDR |
| 0x40 | HECKWISCHEN_GEDR |
| 0x80 | HECKWASCHEN_GEDR |
| - | MEHRFACHBETAETIGUNG |

<a id="table-sg-status-sws-gesamt2"></a>
### SG_STATUS_SWS_GESAMT2

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x01 | REGENSENSOR_TASTE_GEDR |

<a id="table-sg-status-sws-gesamt3"></a>
### SG_STATUS_SWS_GESAMT3

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x01 | STUFE_1 |
| 0x02 | STUFE_2 |
| 0x04 | STUFE_3 |
| 0x08 | STUFE_4 |
| - | MEHRFACHBETAETIGUNG |

<a id="table-sg-status-fgr-gesamt1"></a>
### SG_STATUS_FGR_GESAMT1

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x01 | TIPPEN_VORNE |
| 0x02 | UEBERDRUECKEN_VORNE |
| 0x04 | TIPPEN_HINTEN |
| 0x08 | UEBERDRUECKEN_HINTEN |

<a id="table-sg-status-fgr-gesamt2"></a>
### SG_STATUS_FGR_GESAMT2

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x04 | TIPPEN_AXIAL |

<a id="table-sg-status-fgr-gesamt3"></a>
### SG_STATUS_FGR_GESAMT3

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x01 | ACC_PLUS |
| 0x02 | ACC_MINUS |

<a id="table-sg-status-fgr-gesamt4"></a>
### SG_STATUS_FGR_GESAMT4

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x01 | TIPPEN_UNTEN |
| 0x02 | TIPPEN_OBEN |

<a id="table-sg-status-lsv-gesamt1"></a>
### SG_STATUS_LSV_GESAMT1

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x01 | LAENGE_PLUS |
| 0x02 | LAENGE_MINUS |
| 0x04 | NEIGUNG_AUF |
| 0x08 | NEIGUNG_AB |

<a id="table-sg-status-mfl-gesamt1"></a>
### SG_STATUS_MFL_GESAMT1

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x01 | PTT |
| 0x02 | VOL+ |
| 0x04 | VOL- |
| 0x08 | TEL |

<a id="table-sg-status-mfl-gesamt2"></a>
### SG_STATUS_MFL_GESAMT2

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE_AKTION |
| 0x10 | PROG_2 |
| 0x20 | SUCHLAUF_AUF |
| 0x40 | SUCHLAUF_AB |
| 0x80 | PROG_1 |
