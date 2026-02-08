# mrs5.prg

- Jobs: [63](#jobs)
- Tables: [27](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MRS5 fuer Airbag SG PL2, ausser E93 |
| ORIGIN | BMW EI-62 Ingo Scherer |
| REVISION | 4.08 |
| AUTHOR | BOSCH Kirchschlager, BERATA Mujagic Elmir, BERATA Chafigoulline |
| COMMENT | N/A |
| PACKAGE | 1.40 |
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
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
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
- [IDENT_OC3](#job-ident-oc3) - Identdaten der OC3-Matte KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_LESEN](#job-status-lesen) - Status des MRS5 lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [HERSTELLERDATEN_LESEN](#job-herstellerdaten-lesen) - Kodierte KFZ-Herstellerdaten lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [VERRIEGELUNG_LESEN](#job-verriegelung-lesen) - Auslesen des Pruefstempels / Sind Airbags scharfgeschaltet? KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default  BYTE1=BYTE2=BYTE3 =   0 = 0x00 = SG verriegelt / Airbags sind scharf BYTE1=BYTE2=BYTE3 = 255 = 0xFF = SG nicht verriegelt
- [VERRIEGELUNG_SCHREIBEN](#job-verriegelung-schreiben) - Das Steuergeraet wird verriegelt Oder alternativ ueber PRUEFSTEMPEL_SCHREIBEN verriegelbar.  KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default  Hinweis zu Job PRUEFSTEMPEL_SCHREIBEN: Argument: 0 0 0 , um Steuergeraet zu verriegeln. / Airbags scharfschalten WICHTIG: Werte durch Semikolon getrennt eingeben!! ---Steuergeraet kann NUR durch die Entwicklung entriegelt werden.--- 
- [MRSA_LESEN](#job-mrsa-lesen) - Lesen Seriennummer fuer jeden Satellit Read seriell number of all satellits
- [CONTROLLER_RESET](#job-controller-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [STATUS_AUSSTATTUNG](#job-status-ausstattung) - Ausstattung lesen Read equipment configuration KWP2000: $22   ReadDataByCommonIdentifier $3000 CodingDataSet Modus  : Default
- [STEUERN_NOTRUF](#job-steuern-notruf) - Funktionstest TCU Schnittstelle Telefon-Notruf KWP2000: $31 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_FREIGABE_ZUENDKREISE](#job-status-freigabe-zuendkreise) - Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default
- [STATUS_ZUENDKREISWIDERSTAENDE](#job-status-zuendkreiswiderstaende) - Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default
- [STATUS_GURTKONTAKTE](#job-status-gurtkontakte) - Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default
- [STATUS_LENKSEITE](#job-status-lenkseite) - Auslesen der im Airbagsteuergerät codierten Lenkseite mit dem SGBD-Generator erzeugt

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

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

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

<a id="job-ident-oc3"></a>
### IDENT_OC3

Identdaten der OC3-Matte KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer BCD-codiert |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index BCD-codiert |
| ID_BUS_INDEX | int | Varianten-Index BCD-codiert |
| ID_DATUM_KW | int | Herstelldatum (KWoche) BCD-codiert |
| ID_DATUM_JAHR | int | Herstelldatum (Jahr) BCD-codiert |
| ID_LIEF_NR | int | Lieferanten-Nummer BCD-codiert |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | string | Softwarenummer BCD-codiert |
| ID_SERIEN_NR | string | Seriennummer BCD-codiert |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Status des MRS5 lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| STAT_ZK0 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK1 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK2 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK3 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK4 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK5 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK6 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK7 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK8 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK9 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK10 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK11 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK12 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK13 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK14 | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK15 | int | 0 = n.i.O. (externer Fehler), 1 = i.O., -1 = nicht verbaut ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK16 | int | 0 = n.i.O. (externer Fehler), 1 = i.O., -1 = nicht verbaut ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK17 | int | 0 = n.i.O. (externer Fehler), 1 = i.O., -1 = nicht verbaut ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK18 | int | 0 = n.i.O. (externer Fehler), 1 = i.O., -1 = nicht verbaut ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_ZK19 | int | 0 = n.i.O. (externer Fehler), 1 = i.O., -1 = nicht verbaut ZK = Zündkreis = ignition circuit externer Fehler = external error |
| STAT_GURTSCHLOSS_FA_GESTECKT | int | Gurt - Fahrer Buckle - driver, 1 = plugged in 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GURTSCHLOSS_FA_FEHLER | int | Gurt - Fahrer Buckle - driver, 1 = error 0 =  kein Fehler, 1 = Fehler |
| STAT_GURTSCHLOSS_FA_VERBAUT | int | Gurt - Fahrer Buckle - driver, 1 = assembled 0 = nicht verbaut, 1 = verbaut |
| STAT_GURTSCHLOSS_BF_GESTECKT | int | Gurt - Beifahrer Buckle - passenger, 1 = plugged in 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GURTSCHLOSS_BF_FEHLER | int | Gurt - Beifahrer Buckle - passenger, 1 = error 0 = kein Fehler, 1 = Fehler |
| STAT_GURTSCHLOSS_BF_VERBAUT | int | Gurt - Beifahrer Buckle - passenger, 1 = assembled 0 = nicht verbaut, 1 = verbaut |
| STAT_GURTSCHLOSS_HL_GESTECKT | int | Gurt hinten links Buckle fond left, 1 = plugged in 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GURTSCHLOSS_HL_FEHLER | int | Gurt hinten links Buckle fond left, 1 = error 0 =  kein Fehler, 1 = Fehler |
| STAT_GURTSCHLOSS_HL_VERBAUT | int | Gurt hinten links Buckle fond left, 1 = assembled 0 = nicht verbaut, 1 = verbaut |
| STAT_GURTSCHLOSS_HR_GESTECKT | int | Gurt hinten rechts Buckle fond right, 1 = plugged in 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GURTSCHLOSS_HR_FEHLER | int | Gurt hinten rechts Buckle fond right, 1 = error 0 = kein Fehler, 1 = Fehler |
| STAT_GURTSCHLOSS_HR_VERBAUT | int | Gurt hinten rechts Buckle fond right, 1 = assembled 0 = nicht verbaut, 1 = verbaut |
| STAT_PASSENGER_AIRBAG_OFF | int | Passenger Airbag OFF-Schalter 0 = Airbag on 1 = Airbag off 0 = Airbag Beifahrer eingeschaltet 1 = Airbag Beifahrer ausgeschaltet |
| STAT_PASSENGER_AIRBAG_OFF_SWITCH_FEHLER | int | Passenger Airbag OFF-Schalter 0 = no error, 1 = error 0 = kein Fehler, 1 = Fehler |
| STAT_PASSENGER_AIRBAG_OFF_SWITCH_VERBAUT | int | Passenger Airbag OFF-Schalter 0 = not assembled, 1 = assembled 0 = nicht verbaut, 1 = verbaut |
| STAT_SITZBELEGUNG | int | SBE/SBR/OC3 Sitzbelegung 0: Sitz unbelegt 1: Sitz belegt  ACHTUNG: SBR-Matte zeigt IMMER belegt an! -1: SBE(OC3) nicht verbaut / Fehler SBE(OC3) Bem.: Die SBR-Matte (Baureihe E87) gibt nur zwei Belegungszustaende aus (AIRBAG_ON und AIRBAG_ON_SBR), d.h. bei unbelegtem Sitz wird STAT_SITZBELEGUNG aktiv ausgegeben |
| STAT_FEHLER | int | SBE/SBR/OC3 Sitzbelegung SBE/SBR/OC3 Fehler-Status 0: kein Fehler 1: SBE/SBR/OC3-Fehler |
| STAT_SBE_BEIFAHRER_BELEGT_AIRBAG_ON | int | SBE Beifahrersitz belegt (Airbag On) ab 09/05 Achtung bei Verbau SBR-Matte: Dieses Result gibt den Zustand SBR Beifahrersitz unbelegt aus Airbag_ON aktiv = 1, deaktiviert = 0 |
| STAT_SBE_BEIFAHRER_BELEGT_AIRBAG_ON_SBR | int | SBE Beifahrersitz belegt (Airbag On + SBR) ab 09/05 Airbag_ON + SBR aktiv = 1, deaktiviert = 0 |
| STAT_SBE_VERBAUT | int | SBE Sitzbelegung 0: System nicht verbaut 1: System verbaut 1: Kodiert und nicht physikalisch verbaut bzw. gesteckt 1: nicht Kodiert und physikalisch verbaut bzw. gesteckt 1: Kodiert und physikalisch verbaut bzw. gesteckt |
| STAT_OC3_VERBAUT | int | OC3 Sitzbelegung 0: kein Fehler 1: System verbaut 1: Kodiert und nicht physikalisch verbaut bzw. gesteckt 1: nicht Kodiert und physikalisch verbaut bzw. gesteckt 1: Kodiert und physikalisch verbaut bzw. gesteckt |
| STAT_FREIGABE | int | OC3 Sitzbelegung 0: kein Fehler 1: System nicht freigegeben |
| STAT_DATENSPEICHER | int | OC3 Sitzbelegung OC3 Datenspeicher-Status 0: kein Fehler 1: Datenspeicher voll |
| STAT_GEWICHTSKLASSE | int | OC3 Sitzbelegung OC3 Gewichtsklasse PL2 US 0: Gewichtsklasse "0" (Leerer Sitz) 1: Gewichtsklasse "1" (Kindersitz) 2: Gewichtsklasse "2" (&gt;=5% Frau / 45kg) 3: Gewichtsklasse "3" (95% Mann) Vorgehalten 4: Gewichtsklasse "4" -1: OC3 nicht verbaut / Fehler OC3  Hinweis: Switch von Klasse 0 auf Belegungsstatus erfolgt sofort Switch von Belegungsstatus auf Klasse 0 erfolgt mit einer Verzoegerung von 6 Sekunden. |
| STAT_GEWICHTSKLASSE_KINDERSITZ | int | OC3 Sitzbelegung 0: kein Fehler 1: OC3 Gewichtsklasse 1: (Kindersitz) siehe Hinweis bei Result "STAT_GEWICHTSKLASSE"! |
| STAT_GEWICHTSKLASSE_SITZ_BELEGT | int | OC3 Sitzbelegung 0: kein Fehler OC3 Gewichtsklasse 2: (&gt;=5% Frau / 45kg) siehe Hinweis bei Result "STAT_GEWICHTSKLASSE"! |
| STAT_GEWICHTSKLASSE_UNDEFINIERT | int | OC3 Sitzbelegung 0: OC3 Gewichtsklasse definiert 1: OC3 Gewichtsklasse nicht definiert |
| STAT_UPFRONT_L_FEHLER | int | UPFRONT links Sensor 0: kein Fehler 1: sendet Fehler |
| STAT_UPFRONT_L_FEHLER_KOMMUNIKATION | int | UPFRONT links Sensor 0: kein Fehler 1: Kommunikationsfehler |
| STAT_UPFRONT_L_FEHLER_LEITUNG | int | UPFRONT links Sensor 0: kein Fehler 1: Leitungsfehler |
| STAT_UPFRONT_L_TYP_OKAY | int | UPFRONT links Sensor 0: falscher Typ 1: Typ OKAY |
| STAT_UPFRONT_R_FEHLER | int | UPFRONT rechts Sensor 0: kein Fehler 1: sendet Fehler |
| STAT_UPFRONT_R_FEHLER_KOMMUNIKATION | int | UPFRONT rechts Sensor 0: kein Fehler 1: Kommunikationsfehler |
| STAT_UPFRONT_R_FEHLER_LEITUNG | int | UPFRONT rechts Sensor 0: kein Fehler 1: Leitungsfehler |
| STAT_UPFRONT_R_TYP_OKAY | int | UPFRONT rechts Sensor 0: falscher Typ 1: Typ OKAY |
| STAT_TUER_L_FEHLER | int | Tuer links Sensor 0: kein Fehler 1: sendet Fehler |
| STAT_TUER_L_FEHLER_KOMMUNIKATION | int | Tuer links Sensor 0: kein Fehler 1: Kommunikationsfehler |
| STAT_TUER_L_FEHLER_LEITUNG | int | Tuer links Sensor 0: kein Fehler 1: Leitungsfehler |
| STAT_TUER_L_TYP_OKAY | int | Tuer links Sensor 0: falscher Typ 1: Typ OKAY |
| STAT_TUER_R_FEHLER | int | Tuer rechts Sensor 0: kein Fehler 1: sendet Fehler |
| STAT_TUER_R_FEHLER_KOMMUNIKATION | int | Tuer rechts Sensor 0: kein Fehler 1: Kommunikationsfehler |
| STAT_TUER_R_FEHLER_LEITUNG | int | Tuer rechts Sensor 0: kein Fehler 1: Leitungsfehler |
| STAT_TUER_R_TYP_OKAY | int | Tuer rechts Sensor 0: falscher Typ 1: Typ OKAY |
| STAT_BSAEULE_L_FEHLER | int | B-Saeule links Sensoren 0: kein Fehler 1: sendet Fehler |
| STAT_BSAEULE_L_FEHLER_KOMMUNIKATION | int | B-Saeule links Sensoren 0: kein Fehler 1: Kommunikationsfehler |
| STAT_BSAEULE_L_FEHLER_LEITUNG | int | B-Saeule links Sensoren 0: kein Fehler 1: Leitungsfehler |
| STAT_BSAEULE_L_TYP_OKAY | int | B-Saeule links Sensoren 0: falscher Typ 1: Typ OKAY |
| STAT_BSAEULE_R_FEHLER | int | B-Saeule rechts Sensoren 0: kein Fehler 1: sendet Fehler |
| STAT_BSAEULE_R_FEHLER_KOMMUNIKATION | int | B-Saeule rechts Sensoren 0: kein Fehler 1: Kommunikationsfehler |
| STAT_BSAEULE_R_FEHLER_LEITUNG | int | B-Saeule rechts Sensoren 0: kein Fehler 1: Leitungsfehler |
| STAT_BSAEULE_R_TYP_OKAY | int | B-Saeule rechts Sensoren 0: falscher Typ 1: Typ OKAY |
| STAT_SPSF_VERBAUT | int | Sitzpositionssensor Fahrer bzw. Sitzmemory Fahrer verbaut(nur für MRS5_cd16 und MRS5_cd20) 0 = not assembled, 1 = assembled 0 = nicht verbaut, 1 = verbaut -2 = nicht vorhanden(bei MRS5) |
| STAT_SPSF_SITZPOSITION | int | Sitzmemory Fahrer (nur für MRS5_cd16 und MRS5_cd20) Der Sitzpositionssensor (SPS) hat die Aufgabe, den für eine 5% Frau ausgelegten Bereich des Sitzverstellfeldes in Längsrichtung zu erkennen, um eine 5% Frau von einem 50% Mann auf dem Fahrersitz zu unterscheiden 0 = Sitzposition hinten 1 = Sitzposition vorne -1 = keine Sitzposition detektierbar -2 = nicht vorhanden(bei MRS5) |
| STAT_SPSF_FEHLER | int | Sitzpositionssensor Fahrer oder Sitzmemory Fahrer (nur für MRS5_cd16 und MRS5_cd20) 0 = kein Fehler 1 = Fehler -2 = nicht vorhanden(bei MRS5) |
| STAT_SPSBF_VERBAUT | int | Sitzpositionssensor Beifahrer (nur für MRS5_cd16 und MRS5_cd20) 0 = not assembled, 1 = assembled 0 = nicht verbaut, 1 = verbaut -2 = nicht vorhanden(bei MRS5) |
| STAT_SPSBF_FRAU_MANN | int | Der Sitzpositionssensor (SPS) hat die Aufgabe, den für eine 5% Frau ausgelegten Bereich des Sitzverstellfeldes in Längsrichtung zu erkennen, um eine 5% Frau von einem 50% Mann auf dem Beifahrersitz zu unterscheiden (nur für MRS5_cd16 und MRS5_cd16) 0 = 50% Mann 1 = 5%  Frau -1 = Fehler -2 = nicht vorhanden(bei MRS5) |
| STAT_SPSBF_UNDEFINIERT | int | Sitzpositionssensor Beifahrer (nur für MRS5_cd16 und MRS5_cd16) 0 = Sitzpositionssensor Fahrer Erkennung definiert 1 = Sitzpositionssensor Fahrer Erkennung undefiniert -2 = nicht vorhanden(bei MRS5) |
| STAT_SPSBF_FEHLER | int | Sitzpositionssensor Beifahrer (nur für MRS5_cd16 und MRS5_cd16) 0 = kein Fehler 1 = Fehler -2 = nicht vorhanden(bei MRS5) |

<a id="job-herstellerdaten-lesen"></a>
### HERSTELLERDATEN_LESEN

Kodierte KFZ-Herstellerdaten lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| TYP | string | Baureihe z.B: E31 / 03h , E34 / 01h ... Vehicle e.g: L30, R50... |
| CODIERDATUM | string | z.B: 21.4.93 ... Coding date |
| WERKSKENNUNG | string | 4-stellige Dezimalzahl als String 4 character plant code (decimal) |
| HAENDLERKENNUNG | string | 5-stellige Dezimalzahl als String 5 character supplier code (decimal) |
| FGNUMMER | string | Kurze Fahrgestellnummer Short VIN |

<a id="job-verriegelung-lesen"></a>
### VERRIEGELUNG_LESEN

Auslesen des Pruefstempels / Sind Airbags scharfgeschaltet? KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default  BYTE1=BYTE2=BYTE3 =   0 = 0x00 = SG verriegelt / Airbags sind scharf BYTE1=BYTE2=BYTE3 = 255 = 0xFF = SG nicht verriegelt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| VERRIEGELUNG | string | 'SG verriegelt' 'SG nicht verriegelt' |
| PRUEFSTEMPEL | binary | Gesamter Pruefstempel |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-verriegelung-schreiben"></a>
### VERRIEGELUNG_SCHREIBEN

Das Steuergeraet wird verriegelt Oder alternativ ueber PRUEFSTEMPEL_SCHREIBEN verriegelbar.  KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default  Hinweis zu Job PRUEFSTEMPEL_SCHREIBEN: Argument: 0 0 0 , um Steuergeraet zu verriegeln. / Airbags scharfschalten WICHTIG: Werte durch Semikolon getrennt eingeben!! ---Steuergeraet kann NUR durch die Entwicklung entriegelt werden.--- 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-mrsa-lesen"></a>
### MRSA_LESEN

Lesen Seriennummer fuer jeden Satellit Read seriell number of all satellits

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DOM_DATA_UFR | binary | Ergebnis fuer DOM-Datenbank MRSA1=Upfront rechts Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSTR | binary | Ergebnis fuer DOM-Datenbank MRSA2=MRSA Tuer rechts Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSBRX | binary | Ergebnis fuer DOM-Datenbank MRSA3=MRSA B-Saeule x rechts Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSBRY | binary | Ergebnis fuer DOM-Datenbank MRSA4=MRSA B-Saeule y rechts Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSBLX | binary | Ergebnis fuer DOM-Datenbank MRSA5=MRSA B-Saeule x links Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSBLY | binary | Ergebnis fuer DOM-Datenbank MRSA6=MRSA B-Saeule y links Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_UFL | binary | Ergebnis fuer DOM-Datenbank MRSA7=Upfront links Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSTL | binary | Ergebnis fuer DOM-Datenbank MRSA8=MRSA Tuer links Herstellerdaten: Seriennumer Satelliten |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG Parameterbereich = 08 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG Parameterbereich = 08 |

<a id="job-controller-reset"></a>
### CONTROLLER_RESET

Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ausstattung"></a>
### STATUS_AUSSTATTUNG

Ausstattung lesen Read equipment configuration KWP2000: $22   ReadDataByCommonIdentifier $3000 CodingDataSet Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| STAT_BYTE_0 | int | Byte 0 der 7 Ausstattungsbytes |
| STAT_BYTE_1 | int | Byte 1 der 7 Ausstattungsbytes |
| STAT_BYTE_2 | int | Byte 2 der 7 Ausstattungsbytes |
| STAT_BYTE_3 | int | Byte 3 der 7 Ausstattungsbytes |
| STAT_BYTE_4 | int | Byte 4 der 7 Ausstattungsbytes |
| STAT_BYTE_5 | int | Byte 5 der 7 Ausstattungsbytes |
| STAT_BYTE_6 | int | Byte 6 der 7 Ausstattungsbytes |
| STAT_BYTE_7 | int | Byte 7 der 7 Ausstattungsbytes |
| STAT_ABF1_ZK0_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut 0 = not included,  1 = included ZK = ignition circuit ABF1 = Airbag Fahrer Stufe 1 |
| STAT_GSF_ZK1_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit GSF = Gurtstrammer Fahrer |
| STAT_GSBF_ZK2_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit GSBF = Gurtstrammer Beifahrer |
| STAT_ABBF1_ZK3_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit ABBF1 = Airbag Beifahrer Stufe 1 |
| STAT_SAVL_ZK4_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit SAVL = Sitzairbag vorne links |
| STAT_SAVR_ZK5_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit SAVR = Sitzairbag vorne rechts |
| STAT_SAHL_ZK6_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit SAHL = Sitzairbag hinten links (Vorgehalten) |
| STAT_SAHR_ZK7_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit SAHR =Sitzairbag hinten rechts (Vorgehalten) |
| STAT_AKSL_ZK6_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit AKSL = Aktive Kopfstuetze Links |
| STAT_AKSR_ZK7_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit AKSR =Aktive Kopfstütze Rechts |
| STAT_CURTAIN_L_ZK8_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit Curtain links |
| STAT_KNAF_ZK8_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden ZK = ignition circuit KNAF = Knieairbag Fahrer,am ZK8 bei MRS5 |
| STAT_CURTAIN_R_ZK9_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit Curtain rechts |
| STAT_KNABF_ZK9_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden ZK = ignition circuit KNABF = Knieairbag Beifahrer,am ZK9 bei MRS5 |
| STAT_SBK_1_ZK10_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit SBK = Sicheheitsbatterieklemme |
| STAT_ABBF2_ZK11_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit ABBF2 = Airbag Beifahrer Stufe 2 |
| STAT_ABF2_ZK12_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit ABF2 = Airbag Fahrer Stufe 2 |
| STAT_GSHL_ZK13_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit GSHL = Gurtstrammer hinten links |
| STAT_GSHR_ZK14_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ZK = ignition circuit GSHR = Gurtstrammer hinten rechts |
| STAT_ADAPTIVER_ABBF_ZK15_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut ADAPTIVER_ABBF = Adaptiver Beifahrerairbag, MRS5_cd16 und MRS5_cd20 |
| STAT_AGKBL_ZK16_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden AGKBL = Adaptiver Gurtkraftbegrenzer links, MRS5_cd16 und MRS5_cd20 |
| STAT_AGKBR_ZK17_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden AGKBR = Adaptiver Gurtkraftbegrenzer rechts, MRS5_cd16 und MRS5_cd20 |
| STAT_KNAF_ZK18_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden KNAF = Knieairbag Beifahrer, MRS5_cd16 und MRS5_cd20 |
| STAT_KNAB_ZK19_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden KNAB = Knieairbag Beifahrer, MRS5_cd16 und MRS5_cd20 |
| STAT_ASL_ZK13_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden ASL = Aufrollstrammer Links, MRS5_cd16 und MRS5_cd20 |
| STAT_ASR_ZK14_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden ASR = Aufrollstrammer Rechts, MRS5_cd16 und MRS5_cd20 |
| STAT_UPFRONT_L_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut UPFRONT-Sensor links |
| STAT_UPFRONT_R_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut UPFRONT-Sensor rechts |
| STAT_MRSA_TUERE_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Seitensensor Tür |
| STAT_GKF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Buckle - driver Gurtkontakt Fahrer |
| STAT_GKBF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Buckle - passenger Gurtkontakt Beifahrer |
| STAT_SPSF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden Sitzpositionsensor Fahrer |
| STAT_GKHL_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden Gurtkontakt hinten links, Nur MRS5 |
| STAT_GKHR_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden Gurtkontakt hinten rechts, Nur MRS5 |
| STAT_POS_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Passenger Airbag Off Schalter |
| STAT_NOTRUF_AACN_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut NOTRUF_AACN = Advanced Automatic Crash Notification. Bezeichnet den neuen Notruf, bei dem seitens des Airbag SG Crash Daten an das Telematik SG versendet werden. Ueber die Codierung NOTRUF_AACN_VERBAUT wird unterschieden, ob der Standard-Notruf ACN oder der erweiterte Notruf AACN aktiviert wird. |
| STAT_SBE_1_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Seat occupancy recognition 1 (Sitzmatte) |
| STAT_OC3_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut Occupant Clasification System (Sitzmatte) |
| STAT_SBE_1_STATUS | int | 0 = keine Verzoegerung, 1 = Verzoegerung Seat occupancy recognition status delay |
| STAT_SLVF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut SLV  (Sitzlehnenverriegelung)  Fahrer |
| STAT_SLVBF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut SLV  (Sitzlehnenverriegelung)  Beifahrer |
| STAT_ROLLOVER_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| STAT_POL_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut |
| STAT_AWL_DIREKT_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden nur MRS5 |
| STAT_SBRS_BF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut SBRS (Seat belt reminder Sensor) Beifahrer, nur MRS5_cd16, und MRS5_cd20 |
| STAT_AGW_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut AGW = Akustische Gurtwarnung |
| STAT_SBR_FA_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut SBR (Seat belt reminder) Fahrer |
| STAT_SBR_BF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden SBR (Seat belt reminder) Beifahrer |
| STAT_OGWF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden OGWF = Optische Gurtwarnung Fahrer |
| STAT_OGWBF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden OGWBF = Optische Gurtwarnung Beiahrer |
| STAT_GK_OC3_POL_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut GK_OC3_POL = Aktivierung der Abhängigkeit vom Gurtschloss (gesteckt / Fehler /nicht gesteckt) zur OC3 sowie POL Anzeigen-Logik |
| STAT_SPSBF_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden Sitzpositionsensor Beifahrer |
| STAT_TCU_UEBERWACHUNG_AB_VERBAUT | int | 0 = nicht verbaut, 1 = verbaut, -1 = nicht vorhanden TCU Ueberwachung Abschaltung |

<a id="job-steuern-notruf"></a>
### STEUERN_NOTRUF

Funktionstest TCU Schnittstelle Telefon-Notruf KWP2000: $31 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-freigabe-zuendkreise"></a>
### STATUS_FREIGABE_ZUENDKREISE

Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG Wert = 05 Gruppe = Freigabestatus Zuendkreise |
| _TEL_ANTWORT | binary | Wert = 05 Gruppe = Freigabestatus Zuendkreise |
| _TEL_ANTWORT_1 | binary | Wert = 05 Gruppe = Freigabestatus Zuendkreise |
| STAT_DATEN | binary | Zuendkreise |
| STAT_ABF1_ZK0_FREIGABE | int | 0 = gesperrt, 1 = freigabe ZK = ignition circuit ABF1 = Airbag Fahrer Stufe 1 |
| STAT_GSF_ZK1_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit GSF = Gurtstrammer Fahrer |
| STAT_GSBF_ZK2_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit GSBF = Gurtstrammer Beifahrer |
| STAT_ABBF1_ZK3_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ABBF1 = Airbag Beifahrer Stufe 1 |
| STAT_SAVL_ZK4_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SAVL = Sitzairbag vorne links |
| STAT_SAVR_ZK5_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SAVR = Sitzairbag vorne rechts |
| STAT_AKSL_ZK6_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit AKSL = Aktive Kopfstuetze Links |
| STAT_AKSR_ZK7_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit AKSR = Aktive Kopfstuetze Rechts |
| STAT_CURTAIN_L_ZK8_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit Curtain links (E93 Knieairbag Fahrer) |
| STAT_CURTAIN_R_ZK9_FREIGABE | int | 0 = nicht gesperrt, 1 = freigegeben ZK = ignition circuit Curtain rechts (E93 Knieairbag Beifahrer) |
| STAT_SBK_1_ZK10_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SBK = Sicheheitsbatterieklemme |
| STAT_ABBF2_ZK11_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ABBF2 = Airbag Beifahrer Stufe 2 |
| STAT_ABF2_ZK12_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ABF2 = Airbag Fahrer Stufe 2 |
| STAT_GSHL_ZK13_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit GSHL = Gurtstrammer hinten links |
| STAT_GSHR_ZK14_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit GSHR = Gurtstrammer hinten rechts |
| STAT_ADAPTIVER_ABBF_ZK15_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ADAPTIVER_ABBF = Adaptiver Beifahrerairbag,nur MRS5_cd16,MRS5_cd20 |
| STAT_AGKBL_ZK16_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit AGKBL = Adaptiver Gurtkraftbegrenzer Links,nur MRS5_cd16,MRS5_cd20 |
| STAT_AGKBR_ZK17_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit AGKBL = Adaptiver Gurtkraftbegrenzer Rechts,nur MRS5_cd16,MRS5_cd20 |
| STAT_KNAF_ZK18_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit KNAF = Knieairbag Fahrer, am ZK18 MRS5_cd16,MRS5_cd20 |
| STAT_KNABF_ZK19_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit KNABF = Knieairbag Fahrer, am ZK18 MRS5_cd16,MRS5_cd20 |
| STAT_ASL_ZK13_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ASL = Aufrollstrammer links, am ZK13 MRS5_cd16,MRS5_cd20 |
| STAT_ASR_ZK14_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ASR = Aufrollstrammer rechts, am ZK13 MRS5_cd16,MRS5_cd20 |

<a id="job-status-zuendkreiswiderstaende"></a>
### STATUS_ZUENDKREISWIDERSTAENDE

Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZK0 | real | ZK0=Airbag Fahrer Stufe 1 |
| STAT_ZK0_EINH | string | Einheit: Ohm |
| STAT_ZK1 | real | ZK1=Gurtstrammer Fahrer |
| STAT_ZK1_EINH | string | Einheit: Ohm |
| STAT_ZK2 | real | ZK2=Gurtstrammer Beifahrer |
| STAT_ZK2_EINH | string | Einheit: Ohm |
| STAT_ZK3 | real | ZK3=Airbag Beifahrer Stufe 1 |
| STAT_ZK3_EINH | string | Einheit: Ohm |
| STAT_ZK4 | real | ZK4=Sitzairbag vorne links |
| STAT_ZK4_EINH | string | Einheit: Ohm |
| STAT_ZK5 | real | ZK5=Sitzairbag vorne rechts |
| STAT_ZK5_EINH | string | Einheit: Ohm |
| STAT_ZK6 | real | ZK6=Aktive Kopfstütze Links |
| STAT_ZK6_EINH | string | Einheit: Ohm |
| STAT_ZK7 | real | ZK7=Aktive Kopfstütze Rechts |
| STAT_ZK7_EINH | string | Einheit: Ohm |
| STAT_ZK8 | real | ZK8=Curtain links / Knieairbag Fahrer |
| STAT_ZK8_EINH | string | Einheit: Ohm |
| STAT_ZK9 | real | ZK9=Curtain rechts / Knieairbag Beifahrer |
| STAT_ZK9_EINH | string | Einheit: Ohm |
| STAT_ZK10 | real | ZK10=SBKl |
| STAT_ZK10_EINH | string | Einheit: Ohm |
| STAT_ZK11 | real | ZK11=Airbag Beifahrer Stufe 2 |
| STAT_ZK11_EINH | string | Einheit: Ohm |
| STAT_ZK12 | real | ZK12=Airbag Fahrer Stufe 2 |
| STAT_ZK12_EINH | string | Einheit: Ohm |
| STAT_ZK13 | real | ZK13=Gurtstrammer hinten links / Aufrollstrammer Links |
| STAT_ZK13_EINH | string | Einheit: Ohm |
| STAT_ZK14 | real | ZK14=Gurtstrammer hinten rechts / Aufrollstrammer Rechts |
| STAT_ZK14_EINH | string | Einheit: Ohm |
| STAT_ZK15 | real | ZK15=Adaptiver Beifahrerairbag, nur MRS5_cd20 |
| STAT_ZK15_EINH | string | Einheit: Ohm |
| STAT_ZK16 | real | ZK16=Adaptiver Gurtkraftbegrenzer links, nur MRS5_cd20 |
| STAT_ZK16_EINH | string | Einheit: Ohm |
| STAT_ZK17 | real | ZK17=Adaptiver Gurtkraftbegrenzer rechts,nur MRS5_cd20 |
| STAT_ZK17_EINH | string | Einheit: Ohm |
| STAT_ZK18 | real | ZK18=Knieairbag Fahrer,nur MRS5_cd20 |
| STAT_ZK18_EINH | string | Einheit: Ohm |
| STAT_ZK19 | real | ZK19=Knieairbag Beifahrer,nur MRS5_cd20 |
| STAT_ZK19_EINH | string | Einheit: Ohm |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG Wert = 01 Gruppe = Zuendkreiswiderstaende |
| _TEL_ANTWORT | binary | Wert = 01 Gruppe = Zuendkreiswiderstaende |
| _TEL_ANTWORT_1 | binary | Wert = 01 Gruppe = Zuendkreiswiderstaende |
| STAT_DATEN | binary | Zuendkreiswiderstaende |

<a id="job-status-gurtkontakte"></a>
### STATUS_GURTKONTAKTE

Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG Wert = 02 Gruppe = Gurtkontakte |
| STAT_GKF | real | Gurtkontakt Fahrer |
| STAT_GKF_EINH | string | Einheit: mA |
| STAT_GKBF | real | Gurtkontakt Beifahrer |
| STAT_GKBF_EINH | string | Einheit: mA |
| STAT_GKHL | real | Gurtkontakt hinten links |
| STAT_GKHL_EINH | string | Einheit: mA |
| STAT_GKHR | real | Gurtkontakt hinten rechts |
| STAT_GKHR_EINH | string | Einheit: mA |
| STAT_POS | real | Passenger Airbag Off Schalter |
| STAT_POS_EINH | string | Einheit: mA |
| _TEL_ANTWORT | binary | Wert = 02 Gruppe = Gurtkontakte |
| STAT_DATEN | binary | Gurtkontakte |

<a id="job-status-lenkseite"></a>
### STATUS_LENKSEITE

Auslesen der im Airbagsteuergerät codierten Lenkseite mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RECHTSLENKER | int | Lenkseite: 0 = links/Linkslenker, 1 = rechts/Rechtslenker |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (115 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (95 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (9 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [ZEIT](#table-zeit) (1 × 8)
- [ZEIT2](#table-zeit2) (1 × 3)
- [MONATTAG](#table-monattag) (1 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (12 × 9)
- [MONAT](#table-monat) (13 × 2)
- [WOCHENTAG](#table-wochentag) (8 × 2)
- [JAHRESZEIT](#table-jahreszeit) (3 × 2)
- [IORTTEXTE](#table-iorttexte) (248 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (6 × 2)
- [IARTTEXTEERWEITERT](#table-iarttexteerweitert) (1 × 3)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (12 × 9)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

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

Dimensions: 115 rows × 2 columns

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 95 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x93A8 | ZK0 / Airbag Fahrer 1.Stufe |
| 0x93A9 | ZK1 / Gurtstrammer Fahrer |
| 0x93AA | ZK2 / Gurtstrammer Beifahrer |
| 0x93AB | ZK3 / Airbag Beifahrer 1.Stufe |
| 0x93AC | ZK4 / Sitzairbag vorne Links |
| 0x93AD | ZK5 / Sitzairbag vorne Rechts |
| 0x93AE | ZK6 / Aktive Kopfstuetze Links |
| 0x93AF | ZK7 / Aktive Kopfstuetze Rechts |
| 0x93B0 | ZK8 / Curtainairbag Links |
| 0x93B1 | ZK9 / Curtainairbag Rechts |
| 0x93B2 | ZK10 / Sicherheitsbatterieklemme |
| 0x93B3 | ZK11 / Airbag Beifahrer 2.Stufe |
| 0x93B4 | ZK12 / Airbag Fahrer 2.Stufe |
| 0x93B5 | ZK13 / Gurtstrammer hinten Links |
| 0x93B6 | ZK14 / Gurtstrammer hinten Rechts |
| 0x93B7 | ZK15 / AUX1 |
| 0x9433 | ZK15 / Adaptiver Beifahrer Airbag |
| 0x9416 | ZK13 / Aufrollstrammer links |
| 0x9417 | ZK14 / Aufrollstrammer rechts |
| 0x9419 | ZK16 / Gurtkraftbegrenzer links |
| 0x941A | ZK17 / Gurtkraftbegrenzer rechts |
| 0x941B | ZK18 / Knieairbag links |
| 0x941C | ZK19 / Knieairbag rechts |
| 0x944F | ZK15 / Knieairbag Fahrer |
| 0x9450 | ZK6 / Gurtkraftbegrenzer links |
| 0x9451 | ZK7 / Gurtkraftbegrenzer rechts |
| 0x93C0 | Sitzpositionssensor Beifahrer |
| 0x93BF | Sitzpositionssensor Fahrer |
| 0x9400 | Falschverbau SBR - Sensor |
| 0x93B8 | ZK8 / Knieairbag Fahrer |
| 0x93B9 | ZK9 / Knieairbag Beifahrer |
| 0x93BA | Gurtkontakt Fahrer |
| 0x93BB | Gurtkontakt Beifahrer |
| 0x93BC | Gurtkontakt hinten Links |
| 0x93BD | Gurtkontakt hinten Rechts |
| 0x93BE | Passenger Airbag Off Schalter (POS) |
| 0x93C1 | SBE |
| 0x93C2 | SBE Sitzmatte |
| 0x93C3 | OC3 |
| 0x93C4 | OC3 - Datenspeicher voll |
| 0x93C5 | OC3 - System noch nicht freigegeben |
| 0x93D8 | OC3 - System konnte nicht freigegeben werden |
| 0x93C6 | SLV Fahrer |
| 0x93C7 | SLV Beifahrer |
| 0x93C8 | UPFRONT Links |
| 0x93D9 | UPFRONT Links - falscher Messbereich |
| 0x93DA | UPFRONT Links - Sensor Data Implausible |
| 0x93C9 | UPFRONT Rechts |
| 0x93DB | UPFRONT Rechts - falscher Messbereich |
| 0x93DC | UPFRONT Rechts - Sensor Data Implausible |
| 0x93CA | MRSA B- Säule X  Links |
| 0x93DD | MRSA B- Säule X  Links - falscher Messbereich |
| 0x93DE | MRSA B- Säule X  Links - Sensor Data Implausible |
| 0x93CB | MRSA B- Säule X  Rechts |
| 0x93DF | MRSA B- Säule X  Rechts - falscher Messbereich |
| 0x93E0 | MRSA B- Säule X  Rechts - Sensor Data Implausible |
| 0x93CC | MRSA B- Säule Y  Links |
| 0x93E1 | MRSA B- Säule Y  Links - falscher Messbereich |
| 0x93E2 | MRSA B- Säule Y  Links - Sensor Data Implausible |
| 0x93CD | MRSA B- Säule Y  Rechts |
| 0x93E3 | MRSA B- Säule Y  Rechts - falscher Messbereich |
| 0x93E4 | MRSA B- Säule Y  Rechts - Sensor Data Implausible |
| 0x93CE | MRSA Tür Links |
| 0x93E5 | MRSA Tür Links - falscher Messbereich |
| 0x93E6 | MRSA Tür Links - Sensor Data Implausible |
| 0x93EE | MRSA Tür Links - Drucksensor ausserhalb Messbereich |
| 0x93EF | MRSA Tür Links - Absolutdruck ausserhalb Messbereich |
| 0x93F0 | MRSA Tür Links - Differenz des Absolutdrucks ausserhalb Messbereich |
| 0x93F4 | MRSA Tür Links - Absolutdruck-Uebertragungsstoerung |
| 0x93CF | MRSA Tür Rechts |
| 0x93E7 | MRSA Tür Rechts - falscher Messbereich |
| 0x93E8 | MRSA Tür Rechts - Sensor Data Implausible |
| 0x93F1 | MRSA Tür Rechts - Drucksensor ausserhalb Messbereich |
| 0x93F2 | MRSA Tür Rechts - Absolutdruck ausserhalb Messbereich |
| 0x93F3 | MRSA Tür Rechts - Differenz des Absolutdrucks ausserhalb Messbereich |
| 0x93F5 | MRSA Tür Rechts - Absolutdruck-Uebertragungsstoerung |
| 0x93D0 | Versorgungsspannung - Unterspannung |
| 0x93D1 | Versorgungsspannung - Ueberspannung |
| 0x93D2 | Passenger Airbag Off Leuchte (POL) |
| 0x93EB | TCU-Ausgang |
| 0x93D3 | CBD -Block - CRC Fehler durch Schreiben Codierdaten |
| 0x93EC | EEPROM Layout passt nicht zur SW-Version |
| 0x93D4 | Crashtelegrammspeicher - Mindestens ein Crashtelegramm ist gespeichert |
| 0x93D5 | Crashtelegrammspeicher - Drei Crashtelegramme sind gespeichert |
| 0x93FB | SBR-Funktion - Geschwindigkeitssignal fehlt |
| 0x93D6 | Zentralsteuergeraet - SG ist nicht verriegelt |
| 0x93D7 | Zentralsteuergeraet - Interner Fehler |
| 0x93ED | Zentralsteuergeraet/Satelliten - Unbekannter Fehler |
| 0x93F6 | Alert-Schwelle - Ueberpruefung Ausloeseschwelle |
| 0x9408 | Versorgungsspannung - Unterspannung im PDC |
| 0x940A | Versorgungsspannung - Ueberspannung im PDC |
| 0x940D | LCD_Leuchtdichte - Telegramm mit Helligkeitsinfo nicht empfangen |
| 0xC944 | Bus Leitungsfehler - Allg. |
| 0xC947 | Bus Kommunikationsfehler |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | 11111111 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 9 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| 00000001 | 11 | Widerstand zu gross (ZK) |
| 00000010 | 12 | Widerstand zu klein (ZK) |
| 00000100 | 14 | Widerstand nicht definiert |
| 00001000 | 18 | Verkopplung (Leitungsfehler) |
| 00010000 | 116 | Kommunikations-Stoerung |
| 00100000 | 132 | Sensor / Modul sendet nicht (Kein ID-Telegramm) |
| 01000000 | 164 | Sensor / Modul Fehler |
| 10000000 | 1128 | Falscher Typ |
| xxxxxxxx | 0 | Kein passendes Fehlersymptom |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | ZEIT | MONATTAG | ZEIT2 | 0x0C |

<a id="table-zeit"></a>
### ZEIT

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 |

<a id="table-zeit2"></a>
### ZEIT2

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x0A | 0x0B |

<a id="table-monattag"></a>
### MONATTAG

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x08 | 0x09 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 12 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Power On - Zaehler | zyklus | -- | signed int | -- | -- | -- | -- |
| 0x02 | Systemzeit Fehler - Beginn | Sek. | -- | signed long | -- | -- | -- | -- |
| 0x03 | Systemzeit Fehler - Ende | Sek. | -- | signed long | -- | -- | -- | -- |
| 0x04 | Absolutzeit Fehler - Beginn - Stunden | Std. | -- | signed char | -- | -- | -- | -- |
| 0x05 | Absolutzeit Fehler - Beginn - Minuten | Min. | -- | signed char | -- | -- | -- | -- |
| 0x06 | Absolutzeit Fehler - Beginn - Sekunden | Sek. | -- | signed char | -- | -- | -- | -- |
| 0x07 | Absolutzeit Fehler - Beginn - Tag | Tag | -- | signed char | -- | -- | -- | -- |
| 0x08 | Absolutzeit Fehler - Beginn - Monat | 0-n | -- | 0xF0 | Monat | -- | -- | -- |
| 0x09 | Absolutzeit Fehler - Beginn - Wochentag | 0-n | -- | 0x0F | Wochentag | -- | -- | -- |
| 0x0A | Absolutzeit Fehler - Beginn - Jahr High Byte | Jahr | -- | unsigned char | -- | -- | -- | -- |
| 0x0B | Absolutzeit Fehler - Beginn - Jahr Low Byte | Jahr | -- | unsigned char | -- | -- | -- | -- |
| 0x0C | Absolutzeit Fehler - Beginn - Sommer/Winterzeit | 0-n | -- | 0x02 | Jahreszeit | -- | -- | -- |

<a id="table-monat"></a>
### MONAT

Dimensions: 13 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x10 | Januar |
| 0x20 | Februar |
| 0x30 | Maerz |
| 0x40 | April |
| 0x50 | Mai |
| 0x60 | Juni |
| 0x70 | Juli |
| 0x80 | August |
| 0x90 | September |
| 0xA0 | Oktober |
| 0xB0 | November |
| 0xC0 | Dezember |
| 0xXY | unplausibel |

<a id="table-wochentag"></a>
### WOCHENTAG

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Montag |
| 0x02 | Dienstag |
| 0x03 | Mitwoch |
| 0x04 | Donnerstag |
| 0x05 | Freitag |
| 0x06 | Samstag |
| 0x07 | Sonntag |
| 0xXY | unplausibel |

<a id="table-jahreszeit"></a>
### JAHRESZEIT

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Winterzeit |
| 0x02 | Sommerzeit |
| 0xXY | unplausibel |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 248 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xC000 | ZK0 / Airbag Fahrer 1.Stufe - Endstufenfehler (Plus) |
| 0xC001 | ZK0 / Airbag Fahrer 1.Stufe - Endstufenfehler (Minus) |
| 0xC002 | ZK1 / Gurtstrammer Fahrer - Endstufenfehler (Plus) |
| 0xC003 | ZK1 / Gurtstrammer Fahrer - Endstufenfehler (Minus) |
| 0xC004 | ZK2 / Gurtstrammer Beifahrer - Endstufenfehler (Plus) |
| 0xC005 | ZK2 / Gurtstrammer Beifahrer - Endstufenfehler (Minus) |
| 0xC006 | ZK3 / Airbag Beifahrer 1.Stufe - Endstufenfehler (Plus) |
| 0xC007 | ZK3 / Airbag Beifahrer 1.Stufe - Endstufenfehler (Minus) |
| 0xC008 | ZK4 / Sitzairbag vorne links - Endstufenfehler (Plus) |
| 0xC009 | ZK4 / Sitzairbag vorne links - Endstufenfehler (Minus) |
| 0xC00A | ZK5 / Sitzairbag vorne rechts - Endstufenfehler (Plus) |
| 0xC00B | ZK5 / Sitzairbag vorne rechts - Endstufenfehler (Minus) |
| 0xC00C | ZK6 / Seitenairbag hinten links - Endstufenfehler (Plus) |
| 0xC00D | ZK6 / Seitenairbag hinten links - Endstufenfehler (Minus) |
| 0xC00E | ZK7 / Seitenairbag hinten rechts - Endstufenfehler (Plus) |
| 0xC00F | ZK7 / Seitenairbag hinten rechts - Endstufenfehler (Minus) |
| 0xC010 | ZK8 / Curtainairbag links / Knieairbag Fahrer - Endstufenfehler (Plus) |
| 0xC011 | ZK8 / Curtainairbag links / Knieairbag Fahrer - Endstufenfehler (Minus) |
| 0xC012 | ZK9 / Curtainairbag rechts / Knieairbag Beifahrer - Endstufenfehler (Plus) |
| 0xC013 | ZK9 / Curtainairbag rechts / Knieairbag Beifahrer - Endstufenfehler (Minus) |
| 0xC014 | ZK10 / Sicherheitsbatterieklemme - Endstufenfehler (Plus) |
| 0xC015 | ZK10 / Sicherheitsbatterieklemme - Endstufenfehler (Minus) |
| 0xC016 | ZK11 / Airbag Beifahrer 2.Stufe - Endstufenfehler (Plus) |
| 0xC017 | ZK11 / Airbag Beifahrer 2.Stufe - Endstufenfehler (Minus) |
| 0xC018 | ZK12 / Airbag Fahrer 2.Stufe - Endstufenfehler (Plus) |
| 0xC019 | ZK12 / Airbag Fahrer 2.Stufe - Endstufenfehler (Minus) |
| 0xC01A | ZK13 / Gurtstrammer hinten links - Endstufenfehler (Plus) |
| 0xC01B | ZK13 / Gurtstrammer hinten links - Endstufenfehler (Minus) |
| 0xC01C | ZK14 / Gurtstrammer hinten rechts - Endstufenfehler (Plus) |
| 0xC01D | ZK14 / Gurtstrammer hinten rechts - Endstufenfehler (Minus) |
| 0xC01E | ZK15 / AUX1 - Endstufenfehler (Plus) |
| 0xC01F | ZK15 / AUX1 - Endstufenfehler (Minus) |
| 0xC020 | Flic0 - Eingang Energiereservespannung |
| 0xC021 | Flic0 - Plausibilitaet Referenzwiderstand |
| 0xC022 | Flic0 - Plausibilitaet |
| 0xC023 | Flic0 - FltFLIC0ChpVoltage |
| 0xC024 | Flic0 - FltFLIC0RMVoltage |
| 0xC025 | Flic0 - FltFLIC0Program |
| 0xC026 | Flic0 - FltFLIC0EOP |
| 0xC027 | Flic1 - Eingang Energiereservespannung |
| 0xC028 | Flic1 - Plausibilitaet Referenzwiderstand |
| 0xC029 | Flic1 - Plausibilitaet |
| 0xC02A | Flic1 - FltFLIC1ChpVoltage |
| 0xC02B | Flic1 - FltFLIC1RMVoltage |
| 0xC02C | Flic1 - FltFLIC1Program |
| 0xC02D | Flic1 - FltFLIC1EOP |
| 0xC02E | Sensor1 - FltXPositiveDeflection |
| 0xC02F | Sensor1 - FltXNegativeDeflection |
| 0xC030 | Sensor1 - Grundwert |
| 0xC031 | Sensor1 - sensor data inplausible |
| 0xC032 | Sensor1 - Safety ID |
| 0xC033 | Sensor2 - FltYPositiveDeflection |
| 0xC034 | Sensor2 - FltYNegativeDeflection |
| 0xC035 | Sensor2 - Grundwert |
| 0xC036 | Sensor2 - sensor data inplausible |
| 0xC037 | Sensor2 - Safety ID |
| 0xC038 | Sensor3 - FltZPositiveDeflection |
| 0xC039 | Sensor3 - FltZNegativeDeflection |
| 0xC03A | Sensor3 - FltZFastOffsetCancellation / Grundwert |
| 0xC03B | Sensor3 - FltZPlausibility / sensor data inplausible |
| 0xC03C | Sensor3 - Safety ID |
| 0xC03D | CPU - FltWD1 |
| 0xC03E | CPU - FltWD2 |
| 0xC03F | CPU - FltWD3 |
| 0xC040 | CPU - FltWDF |
| 0xC041 | CPU - WDDis |
| 0xC042 | System - EEPROM communication test failed |
| 0xC043 | Energiereserve - Unterspannung |
| 0xC044 | Energiereserve - Ueberspannung |
| 0xC045 | Energiereserve - Aufwaertswandler |
| 0xC046 | Energiereserve - Abwaertswandler |
| 0xC047 | Energiereserve - Kapazitaet zu gross / klein |
| 0xC049 | Energiereserve - FltERCVzpChargeUp |
| 0xC04A | Energiereserve - FltERCVzpChargeDown |
| 0xC04B | Energiereserve - FltERCVzpTestVoltage |
| 0xC04C | E2Prom - Konfigurationsdaten defekt |
| 0xC04D | E2Prom - CRCDatasetsNotIdent |
| 0xC04E | E2Prom - FltCRCClassFault |
| 0xC04F | E2Prom - FltEEMVerify |
| 0xC050 | E2Prom - Fehler beim Schreibzugriff |
| 0xC051 | CRC RAM fault |
| 0xC052 | FltPOnReset |
| 0xC053 | FltAmuBusy |
| 0xC054 | FltAmuBusy2 |
| 0xC055 | FltAmuADC |
| 0xC056 | FltAmuMulti1 |
| 0xC057 | FltAmuMulti2 |
| 0xC058 | FltAmuMulti3 |
| 0xC059 | FltAmuTim1A |
| 0xC05A | FltAmuTim1B |
| 0xC05B | FltAmuTim2A |
| 0xC05C | FltAmuTim2B |
| 0xC05D | FltAmuTim3 |
| 0xC05E | FltAmuTim4 |
| 0xC05F | Flic2 - Eingang Energiereservespannung |
| 0xC060 | Flic2 - Plausibilitaet Referenzwiderstand |
| 0xC061 | Flic2 - Plausibilitaet |
| 0xC062 | Flic2 - FltFLIC2ChpVoltage |
| 0xC063 | Flic2 - FltFLIC2RMVoltage |
| 0xC066 | Flic3 - Eingang Energiereservespannung |
| 0xC067 | Flic3 - Plausibilitaet Referenzwiderstand |
| 0xC068 | Flic3 - Plausibilitaet |
| 0xC069 | Flic3 - FltFLIC3ChpVoltage |
| 0xC06A | Flic3 - FltFLIC3RMVoltage |
| 0xC06D | FltAB1FDCurrentSink |
| 0xC06E | FltAB1FPCurrentSink |
| 0xC06F | FltAB2FDCurrentSink |
| 0xC070 | FltAB2FPCurrentSink |
| 0xC071 | FltSA1FRCurrentSink |
| 0xC072 | FltBT1RLCurrentSink |
| 0xC073 | FltBT1RRCurrentSink |
| 0xC074 | FltSA1RLCurrentSink |
| 0xC075 | FltSA1RRCurrentSink |
| 0xC076 | FltBT1FDCurrentSink |
| 0xC077 | FltSA1FLCurrentSink |
| 0xC078 | FltBT1FPCurrentSink |
| 0xC079 | FltCA1LCurrentSink |
| 0xC07A | FltKB1FDCurrentSink |
| 0xC07B | FltCA1RCurrentSink |
| 0xC07C | FltKB1FPCurrentSink |
| 0xC07D | FltAUX1CurrentSink |
| 0xC07E | FltBATD1CurrentSink |
| 0xC07F | FltPICVrefHigh |
| 0xC080 | FltPICVrefLow |
| 0xC081 | FltSCONConfiguration |
| 0xC082 | FltSENSORXYConfiguration |
| 0xC083 | FltSENSORMINUSXConfiguration |
| 0xC084 | FltSENSORZConfiguration |
| 0xC085 | FltRollRateSensorConfiguration |
| 0xC086 | FltPASIF0Configuration |
| 0xC087 | FltPASIF1Configuration |
| 0xC088 | FltPASIF2Configuration |
| 0xC089 | FltSPI1Line |
| 0xC08A | Flic 2 - FltFLIC2Program |
| 0xC08B | Flic 2 - FltFLIC2EOP |
| 0xC08C | Flic 3 - FltFLIC3Program |
| 0xC08D | Flic 3 - FltFLIC3EOP |
| 0xC08E | SCON - FltConfigSCON |
| 0xC08F | SCON - FltEOPSCON |
| 0xC090 | FltRAM |
| 0xC091 | FltROMSector0 |
| 0xC092 | FltROMSector1 |
| 0xC093 | FltBISTtest |
| 0xC094 | FltCsCrossCoupling |
| 0xC095 | FltDisableLines |
| 0xC096 | SCON - FltSconSpecialDisableLineState |
| 0xC097 | Flic - FltFlicSpecialDisableLineState |
| 0xC098 | FltSwReset |
| 0xC099 | SCON - FltSCONPlausibilityPath |
| 0xC09A | FltStackOverflow |
| 0xC09B | Flic 0 - FltFLIC0AnalogTest |
| 0xC09C | Flic 1 - FltFLIC1AnalogTest |
| 0xC09D | Flic 2 - FltFLIC2AnalogTest |
| 0xC09E | Flic 3 - FltFLIC3AnalogTest |
| 0xC09F | SCON - FltSconMonitor |
| 0xC0A0 | Energiereserve |
| 0xC0A1 | Energiereserve - FltAutarky |
| 0xC0A2 | UpFront links - Safety ID- Fehler |
| 0xC0A3 | UpFront rechts - Safety ID- Fehler |
| 0xC0A4 | MRSA B- Säule X- Richtung links - Safety ID- Fehler |
| 0xC0A5 | MRSA B- Säule X- Richtung rechts - Safety ID- Fehler |
| 0xC0A6 | MRSA B- Säule Y- Richtung links - Safety ID- Fehler |
| 0xC0A7 | MRSA B- Säule Y- Richtung rechts - Safety ID- Fehler |
| 0xC0A8 | MRSA Tür Y- Richtung links - Safety ID- Fehler |
| 0xC0A9 | MRSA Tür Y- Richtung rechts - Safety ID- Fehler |
| 0xC0BB | FltFLIC0SDLTest- FLIC 0 special disable registers defective |
| 0xC0BC | FltFLIC1SDLTest- FLIC 1 special disable registers defective |
| 0xC0BD | FltFLIC2SDLTest- FLIC 2 special disable registers defective |
| 0xC0BE | FltFLIC0SDLTest- FLIC 3 special disable registers defective |
| 0xC100 | Beschleunigungsaufnehmer 0 - Ruhespannung Fehlerhaft  |
| 0xC101 | Beschleunigungsaufnehmer 0 - BA- zu unempfindlich  |
| 0xC102 | Beschleunigungsaufnehmer 0 - BA- zu empfindlich  |
| 0xC103 | Beschleunigungsaufnehmer 0 - ZP Fehler  |
| 0xC104 | Beschleunigungsaufnehmer 1 - Ruhespannung Fehlerhaft  |
| 0xC105 | Beschleunigungsaufnehmer 1 - BA- zu unempfindlich  |
| 0xC106 | Beschleunigungsaufnehmer 1 - BA- zu empfindlich  |
| 0xC107 | Beschleunigungsaufnehmer 1 - ZP Fehler  |
| 0xC108 | Autarkiekondensator CAS - Spannung zu klein |
| 0xC109 | Autarkiekondensator CAS - Kapazitaet zu klein |
| 0xC10A | Autarkiekondensator CAS - Kapazitaet zu gross |
| 0xC10B | Autarkiekondensator CAZ - Spannung zu klein |
| 0xC10C | Autarkiekondensator CAZ - Kapazitaet zu klein |
| 0xC10D | Autarkiekondensator CAZ - Kapazitaet zu gross |
| 0xC10E | LSS-Schalter ZK0 - Schalter defekt |
| 0xC10F | LSS-Schalter ZK1 - Schalter defekt |
| 0xC110 | LSS-Schalter ZK2 - Schalter defekt |
| 0xC111 | LSS-Schalter ZK3 - Schalter defekt |
| 0xC112 | LSS-Schalter ZK4 - Schalter defekt |
| 0xC113 | LSS-Schalter ZK5 - Schalter defekt |
| 0xC114 | LSS-Schalter ZK6 - Schalter defekt |
| 0xC115 | LSS-Schalter ZK7 - Schalter defekt |
| 0xC116 | LSS-Schalter ZK8 - Schalter defekt |
| 0xC117 | LSS-Schalter ZK9 - Schalter defekt |
| 0xC118 | LSS-Schalter ZK10 - Schalter defekt |
| 0xC119 | LSS-Schalter ZK11 - Schalter defekt |
| 0xC11A | LSS-Schalter ZK12 - Schalter defekt |
| 0xC11B | LSS-Schalter ZK13 - Schalter defekt |
| 0xC11C | LSS-Schalter ZK14 - Schalter defekt |
| 0xC11D | LSS-Schalter ZK15 - Schalter defekt |
| 0xC11E | LSS-Schalter ZK16 - Schalter defekt |
| 0xC11F | LSS-Schalter ZK17 - Schalter defekt |
| 0xC120 | HSS-Schalter ZK0 - Schalter defekt |
| 0xC121 | HSS-Schalter ZK1 - Schalter defekt |
| 0xC122 | HSS-Schalter ZK2 - Schalter defekt |
| 0xC123 | HSS-Schalter ZK3 - Schalter defekt |
| 0xC124 | HSS-Schalter ZK4 - Schalter defekt |
| 0xC125 | HSS-Schalter ZK5 - Schalter defekt |
| 0xC126 | HSS-Schalter ZK6 - Schalter defekt |
| 0xC127 | HSS-Schalter ZK7 - Schalter defekt |
| 0xC128 | HSS-Schalter ZK8 - Schalter defekt |
| 0xC129 | HSS-Schalter ZK9 - Schalter defekt |
| 0xC12A | HSS-Schalter ZK10 - Schalter defekt |
| 0xC12B | HSS-Schalter ZK11 - Schalter defekt |
| 0xC12C | HSS-Schalter ZK12 - Schalter defekt |
| 0xC12D | HSS-Schalter ZK13 - Schalter defekt |
| 0xC12E | HSS-Schalter ZK14 - Schalter defekt |
| 0xC12F | HSS-Schalter ZK15 - Schalter defekt |
| 0xC130 | HSS-Schalter ZK16 - Schalter defekt |
| 0xC131 | HSS-Schalter ZK17 - Schalter defekt |
| 0xC132 | 3.Schalter - Schalter defekt/Ueberwachung defekt |
| 0xC133 | TZ-Pin - Leitung/Ueberwachung defekt |
| 0xC134 | Referenzspannung - Referenzspannung ausserhalb der Toleranz |
| 0xC135 | Ueberwachungsprozessor - PIC meldet Fehler  |
| 0xC136 | Satelliten Autarkiewandler - defekt |
| 0xC137 | Algorithmusparameter - falsche Algokennung |
| 0xC138 | Algorithmusparameter - Pruefsummenfehler  |
| 0xC139 | EEPROM - Konfigurationsdaten Fehlerhaft  |
| 0xC13A | EEPROM - 1AUS2 Fehler  |
| 0xC13B | EEPROM - Fehler beim Zugriff |
| 0xC13C | ASIC - ASIC Kommunikation nicht moeglich |
| 0xC13D | ASIC - ASIC Zuendenergiegrenze konnte nicht geschrieben werden |
| 0xC13E | ASIC - Referenzwiderstand Fehlerhaft  |
| 0xC0AA | FltFlicRegisterMonitoring |
| 0xC0AB | FltRAMDeviceFireStatus - RAM Device Fire Status Invalid |
| 0xC0AC | FltProgrammingSCONPASIF - PAS-Interface within the SCON can not be programmed |
| 0xC0AD | FltProgrammingPASIF0 - Programming Fault PAS Interface 0 |
| 0xC0AE | FltProgrammingPASIF1 - Programming Fault PAS Interface 1 |
| 0xC0AF | FltPASReadEEPROM - Pas configuration data can not be read from EE |
| 0xC0B0 | FltFlic0SpecialRegisterMonitoring - FLIC 0 Special Disable Register |
| 0xC0B2 | FltFlic2SpecialRegisterMonitoring - FLIC 2 Special Disable Register |
| 0xC0B3 | FltFlic3SpecialRegisterMonitoring - FLIC 3 Special Disable Register |
| 0xC0B4 | FltSconRegisterMonitoring - Scon Special Disable Register Monitoring |
| 0xC0B5 | FltSysWLSconPathTest - Scon is unable to switch on the system warning lamp |
| 0xC0B6 | FltADC - ADC Linearity Test |
| 0xC0B7 | FltProgrammingPASIF2 - Programming Fault PAS Interface 2 |
| 0xC0B8 | FltSensorXYProgrFOC - Fast offset cancellation Can t be started (xy |
| 0xC0B9 | FltSensorMinusXProgrFOC - Fast offset cancellation Can t be started (-x |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | 11111111 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iarttexteerweitert"></a>
### IARTTEXTEERWEITERT

Dimensions: 1 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxxx | 0 | Kein passendes Fehlersymptom |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | ZEIT | MONATTAG | ZEIT2 | 0x0C |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 12 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Power On - Zaehler | zyklus | -- | signed int | -- | -- | -- | -- |
| 0x02 | Systemzeit Fehler - Beginn | Sek. | -- | signed long | -- | -- | -- | -- |
| 0x03 | Systemzeit Fehler - Ende | Sek. | -- | signed long | -- | -- | -- | -- |
| 0x04 | Absolutzeit Fehler - Beginn - Stunden | Std. | -- | signed char | -- | -- | -- | -- |
| 0x05 | Absolutzeit Fehler - Beginn - Minuten | Min. | -- | signed char | -- | -- | -- | -- |
| 0x06 | Absolutzeit Fehler - Beginn - Sekunden | Sek. | -- | signed char | -- | -- | -- | -- |
| 0x07 | Absolutzeit Fehler - Beginn - Tag | Tag | -- | signed char | -- | -- | -- | -- |
| 0x08 | Absolutzeit Fehler - Beginn - Monat | 0-n | -- | 0xF0 | Monat | -- | -- | -- |
| 0x09 | Absolutzeit Fehler - Beginn - Wochentag | 0-n | -- | 0x0F | Wochentag | -- | -- | -- |
| 0x0A | Absolutzeit Fehler - Beginn - Jahr High Byte | Jahr | -- | signed char | -- | -- | -- | -- |
| 0x0B | Absolutzeit Fehler - Beginn - Jahr Low Byte | Jahr | -- | signed char | -- | -- | -- | -- |
| 0x0C | Absolutzeit Fehler - Beginn - Sommer/Winterzeit | 0-n | -- | 0x02 | Jahreszeit | -- | -- | -- |
