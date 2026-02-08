# ACSM60.prg

- Jobs: [65](#jobs)
- Tables: [31](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ACSM / Advanced Crash and Safety Management E60, E61, E63, E64, (auch MRS6 Steuergerät benutzt diese SGBD für:  R55, R56, R57) |
| ORIGIN | BMW EI-62 Scherer Ingo |
| REVISION | 3.002 |
| AUTHOR | BERATA EngineeringConsulting Chafigoulline, BERATA EngineeringConsulting Schieferstein |
| COMMENT | Airbag Steuergeraet fuer CAN-Bus Anwendungen fuer E60, E61, E63, E64, R55, R56, R57 |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
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
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [STATUS_AUSSTATTUNG](#job-status-ausstattung) - mit dem SGBD-Generator erzeugt
- [STATUS_FREIGABE_ZUENDKREISE](#job-status-freigabe-zuendkreise) - Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default
- [STATUS_ZUENDKREISWIDERSTAENDE](#job-status-zuendkreiswiderstaende) - Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default
- [STATUS_GURTKONTAKTE](#job-status-gurtkontakte) - Zugriff auf Steuergeraete Ein- und Ausgaenge Gurtkontaktwerte in [mA] Der Gurtkontakt ist als 2-Draht-Hall Sensor ausgeführt und wird über das zentrale Airbagsteuergerät versorgt Der Passenger Airbag Off Schalter ist als 2-Draht-Hall Sensor ausgeführt und wird über das zentrale Airbagsteuergerät versorgt KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default
- [STATUS_BATTERIELEITUNGSDIAGNOSE](#job-status-batterieleitungsdiagnose) - Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default
- [STATUS_SPS_FAHRER](#job-status-sps-fahrer) - Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default
- [IDENT_OC3](#job-ident-oc3) - Identdaten der OC3-Matte KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [IDENT_ROC](#job-ident-roc) - Identdaten des ROC KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_LESEN](#job-status-lesen) - Status des ACSM lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [HERSTELLERDATEN_LESEN](#job-herstellerdaten-lesen) - Kodierte KFZ-Herstellerdaten lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [HERSTELLER_SPEZDATEN_LESEN](#job-hersteller-spezdaten-lesen) - Herstellerspezifischedaten lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [VERRIEGELUNG_LESEN](#job-verriegelung-lesen) - Auslesen des Pruefstempels / Sind Airbags scharfgeschaltet? KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default  BYTE1=BYTE2=BYTE3 =   0 = 0x00 = verriegelt BYTE1=BYTE2=BYTE3 = 255 = 0xFF = nicht verriegelt
- [VERRIEGELUNG_SCHREIBEN](#job-verriegelung-schreiben) - Das Steuergeraet wird verriegelt Oder alternativ ueber PRUEFSTEMPEL_SCHREIBEN verriegelbar.  Hinweis zu Job PRUEFSTEMPEL_SCHREIBEN: Argument: 0 0 0 , um Steuergeraet zu verriegeln. / Airbags scharfschalten WICHTIG: Werte durch Semikolon getrennt eingeben!! ---Steuergeraet kann NUR durch die Entwicklung entriegelt werden.---  KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [MRSA_LESEN](#job-mrsa-lesen) - Lesen Seriennummer fuer jeden Satellit Read seriell number of all satellits
- [CONTROLLER_RESET](#job-controller-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [STATUS_ROC](#job-status-roc) - Status des Rollover Controller lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [STANDARD_LOGIN_ROC](#job-standard-login-roc) - Standard Login Rollover Controller KWP2000: $2E ReadDataByCommonIdentifier Modus  : Default
- [DIAGNOSE_AUFRECHT_ROC](#job-diagnose-aufrecht-roc) - Diagnosemode des SG aufrecht erhalten KWP2000: $2E TesterPresent Modus  : Default
- [DIAGNOSE_ENDE_ROC](#job-diagnose-ende-roc) - Diagnosemode des SG beenden KWP2000: $2E StopDiagnosticSession Modus  : Default
- [TESTAUSLOESUNG_ROC](#job-testausloesung-roc) - Testausloesung KWP2000: $2E StopDiagnosticSession Modus  : Default
- [TCU_NOTRUF](#job-tcu-notruf) - Funktionstest TCU Schnittstelle Telefon-Notruf KWP2000: $31 ReadDataByCommonIdentifier Modus  : Default
- [POL_TEST](#job-pol-test) - Zugriff auf Steuergeräte Ein- und Ausgaenge POL leuchtet unmittelbar nach Ausführung für 1 Sekunde KWP2000: $30 InputOutputControlByLocalIdentifier Modus  : Default

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

<a id="job-status-ausstattung"></a>
### STATUS_AUSSTATTUNG

mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ABF1_ZK0_VERBAUT | int | ABF1 = Airbag Fahrer Stufe 1 Zuendkreis 0, 0=nicht verbaut,1= verbaut |
| STAT_GSF_ZK1_VERBAUT | int | GSF = Gurtstrammer Fahrer Zuendkreis 1, 0=nicht verbaut,1= verbaut |
| STAT_GSBF_ZK2_VERBAUT | int | GSBF = Gurtstrammer Beifahrer Zuendkreis 2, 0=nicht verbaut,1= verbaut |
| STAT_ABBF1_ZK3_VERBAUT | int | ABBF1 = Airbag Beifahrer Stufe 1 Zuendkreis 3, 0=nicht verbaut,1= verbaut |
| STAT_SAVFS_ZK4_VERBAUT | int | SAVFS = Seitenairbag vorne Fahrerseite Zuendkreis 4, 0=nicht verbaut,1= verbaut |
| STAT_SAVBFS_ZK5_VERBAUT | int | SAVBF = Seitenairbag vorne Beifahrerseite Zuendkreis 5, 0=nicht verbaut,1= verbaut |
| STAT_SAHFS_ZK6_VERBAUT | int | SAHFS = Seitenairbag hinten Fahrerseite Zuendkreis 6, 0=nicht verbaut,1= verbaut |
| STAT_SAHBFS_ZK7_VERBAUT | int | SAHBFS = Seitenairbag hinten Beifahrerseite Zuendkreis 7, 0=nicht verbaut,1= verbaut |
| STAT_KAFS_ZK8_VERBAUT | int | KAFS = Kopfairbag Fahrerseite Zuendkreis 8, 0=nicht verbaut,1= verbaut |
| STAT_KABFS_ZK9_VERBAUT | int | KABFS = Kopfairbag Beifahrerseite Zuendkreis 9, 0=nicht verbaut,1= verbaut |
| STAT_SBK1_ZK10_VERBAUT | int | SBK = Sicherheits - Batterie - Klemme Zuendkreis 10, 0=nicht verbaut,1= verbaut |
| STAT_ABBF2_ZK11_VERBAUT | int | ABBF2 = Airbag Beifahrer Stufe 2 Zuendkreis 11, 0=nicht verbaut,1= verbaut |
| STAT_ABF2_ZK12_VERBAUT | int | ABF2 = Airbag Fahrer Stufe 2 Zuendkreis 12, 0=nicht verbaut,1= verbaut |
| STAT_ESHFS_ZK13_VERBAUT | int | ESHFS = Endbeschlagsstrammer hinten Fahrerseite Zuendkreis 13, 0=nicht verbaut,1= verbaut |
| STAT_ESHBFS_ZK14_VERBAUT | int | ESHBFS = Endbeschlagsstrammer hinten Beifahrerseite Zuendkreis 14, 0=nicht verbaut,1= verbaut |
| STAT_KNAF_ZK15_VERBAUT | int | KNAF = Knieairbag Fahrer Zuendkreis 15, 0=nicht verbaut,1= verbaut ZK 15 ZK 15 wurde vor C5-Muster mit KOSF geteilt |
| STAT_KNABF_ZK16_VERBAUT | int | KNABF = Knieairbag Beifahrer Zuendkreis 16, 0=nicht verbaut,1= verbaut ZK 16 wurde vor C5-Muster mit KOSBF geteilt |
| STAT_ESF_ZK17_VERBAUT | int | ESF = Endbeschlagsstrammer Fahrer Zuendkreis 17, 0=nicht verbaut,1= verbaut |
| STAT_ZK18_KOSFS_VERBAUT | int | KOSFS = Kopfstuetze Fahrer Zuendkreis 18, 0=nicht verbaut,1= verbaut ZK18 war vor C5-Muster Reserve mit belegt |
| STAT_ZK19_KOSBFS_VERBAUT | int | KOSBFS = Kopfstuetze Beifahrer Zuendkreis 19, 0=nicht verbaut,1= verbaut ZK19 war vor C5-Muster Reserve mit belegt |
| STAT_UPFRONT_FA_VERBAUT | int | UPFRONT_FA = Upfrontsensor Fahrerseite X- Richtung, 0=nicht verbaut,1= verbaut |
| STAT_UPFRONT_BF_VERBAUT | int | UPFRONT_BF = Upfrontsensor Beifahrerseite X- Richtung, 0=nicht verbaut,1= verbaut |
| STAT_SAT_TUER_VERBAUT | int | SAT_Tuer = Seitensensor Tür, 0=nicht verbaut,1= verbaut |
| STAT_GKF_VERBAUT | int | GKF = Gurtkontakt Fahrer, 0=nicht verbaut,1= verbaut |
| STAT_GKBF_VERBAUT | int | GKBF = Gurtkontakt Beifahrer, 0=nicht verbaut,1= verbaut |
| STAT_GKHFS_VERBAUT | int | GKHFS = Gurtkontakt hinten Fahrerseite, 0=nicht verbaut,1= verbaut |
| STAT_GKHBFS_VERBAUT | int | GKHBFS = Gurtkontakt hinten Beifahrerseite, 0=nicht verbaut,1= verbaut |
| STAT_SPSF_VERBAUT | int | SPSF = Sitzpositionssensor Fahrer (nur für MRS6), 0=nicht verbaut,1= verbaut |
| STAT_POS_VERBAUT | int | POS = Passenger Airbag Off Schalter, 0=nicht verbaut,1= verbaut |
| STAT_NOTRUF_AACN_VERBAUT | int | NOTRUF_AACN = Advanced Automatic Crash Notification. Bezeichnet den neuen Notruf, bei dem seitens des Airbag SG Crash Daten an das Telematik SG versendet werden. Ueber die Codierung NOTRUF_AACN_VERBAUT wird unterschieden, ob der Standard-Notruf ACN oder der erweiterte Notruf AACN aktiviert wird., 0=nicht verbaut,1= verbaut |
| STAT_SBE_BEIFAHRER_VERBAUT | int | SBE = Sitzbelegungserkennung  Beifahrer, 0=nicht verbaut,1= verbaut |
| STAT_OC3_VERBAUT | int | OC3 = Occupant Clasification System, 0=nicht verbaut,1= verbaut |
| STAT_SBE_BEIFAHRER_VERZOEGERUNG | int | SBE_BEIFAHRER_VERZOEGERUNG = Sitzbelegungserkennung Beifahrer Statusverzoegerung, Umschaltung von belegt --&gt; unbelegt : Entprellzeit betraegt fuer die Airbag Beifahrer Ausloesung 2 Minuten !, 0 = keine Verzoegerung, 1 = Verzoegerung |
| STAT_SBR_MATTE_BEIFAHRER_VERBAUT | int | SBR_MATTE_BEIFAHRER_VERBAUT = seat belt reminder Matte Beifahrer dient ausschliesslich zur Ansteuerung der SeatBeltReminder Funktion.Wenn eine SBR Matte in der Ausstattung verbaut ist und das Steuergeraet ein 'unbelegt' Telegramm empfaengt, wird ein Fehlverbau im Fehlerspeicher eingetragen, 0=nicht verbaut,1= verbaut |
| STAT_SLVF_VERBAUT | int | SLVF = Sitzlehnenverriegelung Fahrer, 0=nicht verbaut,1= verbaut |
| STAT_SLVBF_VERBAUT | int | SLVBF = Sitzlehnenverriegelung Beifahrer, 0=nicht verbaut,1= verbaut |
| STAT_ROC_VERBAUT | int | ROC = Rollover Controller, 0=nicht verbaut,1= verbaut |
| STAT_ROLLOVERFUNKTION_SENSORIK_VERBAUT | int | ROLLOVER_FUNKTION_SENSORIK = Rollover Funktion Sensorik, 0=nicht verbaut,1= verbaut |
| STAT_POL_VERBAUT | int | POL = Passenger Airbag Off Leuchte, 0=nicht verbaut,1= verbaut |
| STAT_SBR_MATTE_FAHRER_VERBAUT | int | SBR_MATTE_FAHRER = SBR - Sensor Fahrer. Zur Erkennung einer Sitzbelegung auf der Fahrerseite wird eine SBR-Matte verbaut, die auf der Sitzbelegungserkennung  basiert. Diese Sitzbelegungserkennung wird nur für die Funktion Längsdynamikmanagement  (Stillstandsmanagement) verwendet und hat keinen Einfluss auf die Ansteuerung eines Rückhaltesystems , 0=nicht verbaut,1= verbaut |
| STAT_AGW_VERBAUT | int | AGW = Akkustische Gurtwarnung Diese Warnung wird bei ungegurtetem Fahrer direkt nach Zuendung ein (Klemme_15 aus auf ein) ausgegeben, falls die akustische Warnung aktiv codiert ist., 0=nicht verbaut,1= verbaut |
| STAT_SBR_FUNKTION_FAHRER | int | SBR_FUNKTION_FAHRER = seat belt reminder Fahrer Diese Warnung wird bei ungegurtetem Fahrer während der Fahrt ausgegeben, falls die SBR-Warnung für den Fahrer aktiv codiert ist. In ungegurtetem Zustand wird nach dem Fahrzeugstart erst bei einer zurückgelegten Wegstrecke und während der Fahrt nach Ablauf einer bestimmten Zeit gewarnt., 0=nicht verbaut,1= verbaut |
| STAT_SBR_FUNKTION_BEIFAHRER | int | SBR_FUNKTION_ = seat belt reminder Beifahrer Diese Warnung wird bei ungegurtetem Beifahrer während der Fahrt ausgegeben, falls die SBR-Warnung für den Beifahrer aktiv codiert ist. In ungegurtetem Zustand wird nach dem Fahrzeugstart erst bei einer zurückgelegten Wegstrecke und während der Fahrt nach Ablauf einer bestimmten Zeit gewarnt., 0=nicht verbaut,1= verbaut |
| STAT_KOPPLUNG_SBR_POS_E85 | int | Kopplung_SBR+POS = Gurtschloss im 70 Hex Telegramm, 0=nicht inaktiv,1= aktiv |
| STAT_BAT_VERBAUT | int | BAT = Batterieleitungsdiagnose, 0=nicht verbaut,1= verbaut |
| STAT_GK_OC3_POL | int | GK_OC3_POL = Aktivierung der Abhängigkeit vom Gurtschloss (gesteckt / Fehler /nicht gesteckt) zur OC3 sowie POL Anzeigen-Logik |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
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
| STAT_DATEN | binary | Zuendkreise |
| STAT_ABF1_ZK0_FREIGABE | int | 0 = gesperrt, 1 = freigabe ZK = ignition circuit ABF1 = Airbag Fahrer Stufe 1 |
| STAT_GSF_ZK1_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit GSF = Gurtstrammer Fahrer |
| STAT_GSBF_ZK2_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit GSBF = Gurtstrammer Beifahrer |
| STAT_ABBF1_ZK3_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ABBF1 = Airbag Beifahrer Stufe 1 |
| STAT_SAVFA_ZK4_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SAVL = Seitenairbag vorne Fahrerseite |
| STAT_SAVBF_ZK5_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SAVBF = Seitenairbag vorne Beifahrerseite |
| STAT_SAHFA_ZK6_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SAHFA = Seitenairbag hinten Fahrerseite |
| STAT_SAHBF_ZK7_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SAHR = Seitenairbag hinten Beifahrerseite |
| STAT_KOFA_ZK8_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit KOFA = Kopfairbag Fahrerseite |
| STAT_KOBF_ZK9_FREIGABE | int | 0 = nicht gesperrt, 1 = freigegeben ZK = ignition circuit KOBF = Kopfairbag Beifahrerseite |
| STAT_SBK_1_ZK10_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit SBK = Sicheheitsbatterieklemme |
| STAT_ABBF2_ZK11_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ABBF2 = Airbag Beifahrer Stufe 2 |
| STAT_ABF2_ZK12_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ABF2 = Airbag Fahrer Stufe 2 |
| STAT_ESHFA_ZK13_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ESHFA = Endbesschlagstrammer hinten Fahrerseite |
| STAT_ESHBF_ZK14_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ESHBF = Endbeschlagsstrammer hinten Beifahrerseite |
| STAT_KNAF_ZK15_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit KNAF = Knieairbag Fahrer Vor SW 4.00 wurde dieser ZK mit Kopfstuetze Fahrer geteilt |
| STAT_KNABF_ZK16_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit KNABF = Knieairbag Beifahrer Vor SW 4.00 wurde dieser ZK mit Kopfstuetze Beifahrer geteilt |
| STAT_ESFA_ZK17_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit ESFA = Endbeschlagsstrammer Fahrer |
| STAT_KOSFA_ZK18_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit KOSF = Kopfstuetze Fahrer Vor SW 4.00 wurde dieser Zuendkreis als Reserve genutzt |
| STAT_KOSBF_ZK19_FREIGABE | int | 0 = gesperrt, 1 = freigegeben ZK = ignition circuit KOSBF = Kopfstuetze Beifahrer Vor SW 4.00 wurde dieser Zuendkreis als Reserve genutzt |

<a id="job-status-zuendkreiswiderstaende"></a>
### STATUS_ZUENDKREISWIDERSTAENDE

Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ZK0_WERT | real | ZK0=Airbag Fahrer Stufe 1 |
| STAT_ZK0_EINH | string | Einheit: Ohm |
| STAT_ZK1_WERT | real | ZK1=Gurtstrammer Fahrer |
| STAT_ZK1_EINH | string | Einheit: Ohm |
| STAT_ZK2_WERT | real | ZK2=Gurtstrammer Beifahrer |
| STAT_ZK2_EINH | string | Einheit: Ohm |
| STAT_ZK3_WERT | real | ZK3=Airbag Beifahrer Stufe 1 |
| STAT_ZK3_EINH | string | Einheit: Ohm |
| STAT_ZK4_WERT | real | ZK4=Seitenairbag Thorax vorne Fahrerseite |
| STAT_ZK4_EINH | string | Einheit: Ohm |
| STAT_ZK5_WERT | real | ZK5=Seitenairbag Thorax vorne Beifahrerseite |
| STAT_ZK5_EINH | string | Einheit: Ohm |
| STAT_ZK6_WERT | real | ZK6=Seitenairbag Thorax hinten Fahrerseite |
| STAT_ZK6_EINH | string | Einheit: Ohm |
| STAT_ZK7_WERT | real | ZK7=Seitenairbag Thorax hinten Beifahrerseite |
| STAT_ZK7_EINH | string | Einheit: Ohm |
| STAT_ZK8_WERT | real | ZK8=Kopfairbag Fahrerseite |
| STAT_ZK8_EINH | string | Einheit: Ohm |
| STAT_ZK9_WERT | real | ZK9=Kopfairbag Beifahrerseite |
| STAT_ZK9_EINH | string | Einheit: Ohm |
| STAT_ZK10_WERT | real | ZK10=SBKl |
| STAT_ZK10_EINH | string | Einheit: Ohm |
| STAT_ZK11_WERT | real | ZK11=Airbag Beifahrer Stufe 2 |
| STAT_ZK11_EINH | string | Einheit: Ohm |
| STAT_ZK12_WERT | real | ZK12=Airbag Fahrer Stufe 2 |
| STAT_ZK12_EINH | string | Einheit: Ohm |
| STAT_ZK13_WERT | real | ZK13=Endbeschlagsstrammer hinten Fahrerseite |
| STAT_ZK13_EINH | string | Einheit: Ohm |
| STAT_ZK14_WERT | real | ZK14=Endbeschlagsstrammer hinten Beifahrerseite |
| STAT_ZK14_EINH | string | Einheit: Ohm |
| STAT_ZK15_WERT | real | ZK15=Knieairbag Fahrer |
| STAT_ZK15_EINH | string | Einheit: Ohm |
| STAT_ZK16_WERT | real | ZK16=Knieairbag Beifahrer |
| STAT_ZK16_EINH | string | Einheit: Ohm |
| STAT_ZK17_WERT | real | ZK17=Endbeschlagsstrammer Fahrer |
| STAT_ZK17_EINH | string | Einheit: Ohm |
| STAT_ZK18_WERT | real | ZK18=Kopfstuetze Fahrer |
| STAT_ZK18_EINH | string | Einheit: Ohm |
| STAT_ZK19_WERT | real | ZK19=Kopfstuetze Beifahrer |
| STAT_ZK19_EINH | string | Einheit: Ohm |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG Wert = 01 Gruppe = Zuendkreiswiderstaende |
| _TEL_ANTWORT | binary | Wert = 01 Gruppe = Zuendkreiswiderstaende |
| STAT_DATEN | binary | Zuendkreiswiderstaende |

<a id="job-status-gurtkontakte"></a>
### STATUS_GURTKONTAKTE

Zugriff auf Steuergeraete Ein- und Ausgaenge Gurtkontaktwerte in [mA] Der Gurtkontakt ist als 2-Draht-Hall Sensor ausgeführt und wird über das zentrale Airbagsteuergerät versorgt Der Passenger Airbag Off Schalter ist als 2-Draht-Hall Sensor ausgeführt und wird über das zentrale Airbagsteuergerät versorgt KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG Wert = 02 Gruppe = Gurtkontakte |
| STAT_GKF_WERT | real | Stromwert Gurtkontakt Fahrer |
| STAT_GKF_EINH | string | Einheit: mA |
| STAT_GKBF_WERT | real | Stromwert Gurtkontakt Beifahrer |
| STAT_GKBF_EINH | string | Einheit: mA |
| STAT_GKHFA_WERT | real | Stromwert Gurtkontakt hinten Fahrer |
| STAT_GKHFA_EINH | string | Einheit: mA |
| STAT_GKHBF_WERT | real | Stromwert Gurtkontakt hinten Beifahrer |
| STAT_GKHBF_EINH | string | Einheit: mA |
| STAT_POS_WERT | real | Stromwert Passenger Airbag Off Schalter |
| STAT_POS_EINH | string | Einheit: mA |
| STAT_RESERVE_WERT | real | RESERVE |
| STAT_RESERVE_EINH | string | Einheit: |
| _TEL_ANTWORT | binary | Wert = 02 Gruppe = Gurtkontakte |
| STAT_DATEN | binary | Gurtkontakte |

<a id="job-status-batterieleitungsdiagnose"></a>
### STATUS_BATTERIELEITUNGSDIAGNOSE

Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG Wert = 06 Gruppe = Batterieleitungsdiagnose |
| STAT_EINGANG_1_WERT | real | Ausgabe Eingang 1 |
| STAT_EINGANG_1_EINH | string | Einheit: V |
| STAT_EINGANG_2_WERT | real | Ausgabe Eingang 2 |
| STAT_EINGANG_2_EINH | string | Einheit: V |
| _TEL_ANTWORT | binary | Wert = 06 Gruppe = Batterieleitungsdiagnose |
| STAT_DATEN | binary | Batterieleitungsdiagnose (Data: Eingang 1 und Eingang 2) |

<a id="job-status-sps-fahrer"></a>
### STATUS_SPS_FAHRER

Zugriff auf Steuergeraete Ein- und Ausgaenge KWP2000: $300X01 InputOutputControlByLocalIdentifier X = Gruppe Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG Wert = 07 Gruppe = Sitzpositionssensor Fahrer |
| STAT_SPS_FAHRER_WERT | real | Sitzpositionssensor Fahrer nur für R55,R56 und R57 |
| STAT_SPS_FAHRER_EINH | string | Einheit: mA |
| _TEL_ANTWORT | binary | Wert = 06 Gruppe = Sitzpositionssensor Fahrer |
| STAT_DATEN | binary | Sitzpostionssensor Fahrer |

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

<a id="job-ident-roc"></a>
### IDENT_ROC

Identdaten des ROC KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer BCD-codiert |
| ID_HW_NR | int | BMW-Hardware Versionsnummer (HW-Index) |
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

Status des ACSM lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ZK0_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK0 = Airbag Fahrer Stufe 1 |
| STAT_ZK1_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK1 = Gurtstrammer Fahrer |
| STAT_ZK2_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK2 = Gurtstrammer Beifahrer |
| STAT_ZK3_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK3 = Airbag Beifahrer Stufe 1 |
| STAT_ZK4_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK4 = Seitenairbag Thorax vorne Fahrerseite |
| STAT_ZK5_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK5 = Seitenairbag Thorax vorne Beifahrerseite |
| STAT_ZK6_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK6 = Seitenairbag Thorax hinten Fahrerseite |
| STAT_ZK7_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK7 = Seitenairbag Thorax hinten Beifahrerseite |
| STAT_ZK8_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK8 = Kopfairbag Fahrerseite |
| STAT_ZK9_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK9 = Kopfairbag Beifahrerseite |
| STAT_ZK10_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK10 = SBKl |
| STAT_ZK11_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK11 = Airbag Beifahrer Stufe 2 |
| STAT_ZK12_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK12 = Airbag Fahrer Stufe 2 |
| STAT_ZK13_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK13 = Endbeschlagsstrammer hinten Fahrerseite |
| STAT_ZK14_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK14 = Endbeschlagsstrammer hinten Beifahrerseite |
| STAT_ZK15_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK15 = Knieairbag Fahrer Vor SW 4.00 wurde dieser ZK mit Kopfstuetze Fahrer geteilt |
| STAT_ZK16_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK16 = Knieairbag Beifahrer Vor SW 4.00 wurde dieser ZK mit Kopfstuetze Beifahrer geteilt |
| STAT_ZK17_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK17 = Endbeschlagsstrammer Fahrer |
| STAT_ZK18_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK18 = Kopfstuetze Fahrer Vor SW 4.00 wurde dieser Zuendkreis als Reserve genutzt |
| STAT_ZK19_OKAY | int | 0 = n.i.O. (externer Fehler), 1 = i.O. ZK = Zündkreis = ignition circuit externer Fehler = external error ZK17 = Kopfstuetze Beifahrer Vor SW 4.00 wurde dieser Zuendkreis als Reserve genutzt |
| STAT_GURTSCHLOSS_FA_GESTECKT | int | Gurt - Fahrer Buckle - driver, 1 = plugged in 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GURTSCHLOSS_FA_FEHLER | int | Gurt - Fahrer Buckle - driver, 1 = error 0 =  kein Fehler, 1 = Fehler |
| STAT_GURTSCHLOSS_FA_VERBAUT | int | Gurt - Fahrer Buckle - driver, 1 = assembled 0 = nicht verbaut, 1 = verbaut |
| STAT_GURTSCHLOSS_BF_GESTECKT | int | Gurt - Beifahrer Buckle - passenger, 1 = plugged in 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GURTSCHLOSS_BF_FEHLER | int | Gurt - Beifahrer Buckle - passenger, 1 = error 0 = kein Fehler, 1 = Fehler |
| STAT_GURTSCHLOSS_BF_VERBAUT | int | Gurt - Beifahrer Buckle - passenger, 1 = assembled 0 = nicht verbaut, 1 = verbaut |
| STAT_GURTSCHLOSS_HFA_GESTECKT | int | Gurt hinten Fahrerseite Buckle - passenger, 1 = plugged in 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GURTSCHLOSS_HFA_FEHLER | int | Gurt hinten Fahrerseite Buckle fond left, 1 = error 0 =  kein Fehler, 1 = Fehler |
| STAT_GURTSCHLOSS_HFA_VERBAUT | int | Gurt hinten Fahrerseite Buckle fond left, 1 = assembled 0 = nicht verbaut, 1 = verbaut |
| STAT_GURTSCHLOSS_HBF_GESTECKT | int | Gurt hinten Beifahrerseite Buckle fond right, 1 = plugged in 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GURTSCHLOSS_HBF_FEHLER | int | Gurt hinten Beifahrerseite Buckle fond right, 1 = error 0 = kein Fehler, 1 = Fehler |
| STAT_GURTSCHLOSS_HBF_VERBAUT | int | Gurt hinten Beifahrerseite Buckle fond right, 1 = assembled 0 = nicht verbaut, 1 = verbaut |
| STAT_PASSENGER_AIRBAG_OFF | int | Passenger Airbag OFF-Schalter 0 = Airbag on 1 = Airbag off 0 = Airbag Beifahrer eingeschaltet 1 = Airbag Beifahrer ausgeschaltet |
| STAT_PASSENGER_AIRBAG_OFF_SWITCH_FEHLER | int | Passenger Airbag OFF-Schalter 0 = no error, 1 = error 0 = kein Fehler, 1 = Fehler |
| STAT_PASSENGER_AIRBAG_OFF_SWITCH_VERBAUT | int | Passenger Airbag OFF-Schalter 0 = not assembled, 1 = assembled 0 = nicht verbaut, 1 = verbaut |
| STAT_SPSF_VERBAUT | int | Sitzpositionssensor Fahrer (nur für MRS6) 0 = not assembled, 1 = assembled 0 = nicht verbaut, 1 = verbaut |
| STAT_SPSF_FRAU_MANN | int | Der Sitzpositionssensor (SPS) hat die Aufgabe, den für eine 5% Frau ausgelegten Bereich des Sitzverstellfeldes in Längsrichtung zu erkennen, um eine 5% Frau von einem 50% Mann auf dem Fahrersitz zu unterscheiden (nur MRS6) 0 = 50% Mann 1 = 5%  Frau -1 = Fehler |
| STAT_SPSF_UNDEFINIERT | int | Sitzpositionssensor Fahrer (nur für MRS6) 0 = Sitzpositionssensor Fahrer Erkennung definiert 1 = Sitzpositionssensor Fahrer Erkennung undefiniert |
| STAT_SPSF_FEHLER | int | Sitzpositionssensor Fahrer (nur für MRS6) 0 = kein Fehler 1 = Fehler |
| STAT_SITZBELEGUNG_FAHRER | int | SBE Fahrer Sitzbelegung 0: Fahrersitz unbelegt 1: Fahrersitz belegt -1: SBE Fahrer nicht verbaut / Fehler SBE Fahrer  Uebersicht siehe table SITZBELEGUNG_FAHRER_BEIFAHRER  JOBS RESULTS SBR-MATTE SBE OC3 |
| STAT_SITZBELEGUNG_FAHRER_FEHLER | int | SBE Fahrer SBE Fahrer Fehler-Status 0: kein Fehler 1: SBE Fahrer Fehler |
| STAT_SBE_FAHRER_VERBAUT | int | Sitzbelegungserkennung Fahrer, Zur Erkennung einer Sitzbelegung auf der Fahrerseite wird die Fahrer SBE verbaut. Diese Sitzbelegungserkennung wird nur für die Funktion Längsdynamikmanagement (Stillstandsmanagement) verwendet und hat keinen Einfluss auf die Ansteuerung eines Rückhaltesystems. 0: System nicht verbaut 1: System verbaut  Die Funktion - Fahrer-SBE - wird fuer die Baureihe E6x ab PU 03/07 umgesetzt |
| STAT_SITZBELEGUNG_BEIFAHRER | int | SBE, SBR-Matte -, OC3 - Beifahrer Sitzbelegung 0: Sitz unbelegt, SBE: Beifahrersitz nicht belegt, SBR-Matte Beifahrer: Die SBR-Matte kann diesen Belegungszustand nicht ausgeben, OC3: Beifahrersitz nicht belegt 1: Sitz belegt (keine SBR-Matte) -2: Sitz belegt (SBR-Matte) -1: SBE, SBR-Matte oder OC3 nicht verbaut / Fehler SBE, SBR-Matte oder OC3 SBE: Sitzbelegungserkennung, SBR-Matte : SeatBeltReminder-Matte, OC3: Occupant Classification 3te Generation  Bem.: Die SBR-Matte gibt nur zwei Belegungszustände aus (AIRBAG_ON und AIRBAG_ON_SBR), d.h. bei unbelegten Sitz wird STAT_SITZBELEGUNG aktiv ausgegeben. Uebersicht siehe table SITZBELEGUNG_FAHRER_BEIFAHRER  JOBS RESULTS SBR-MATTE SBE OC3 |
| STAT_SITZBELEGUNG_BEIFAHRER_FEHLER | int | SBE Beifahrer/OC3 Sitzbelegung SBE Beifahrer/OC3 Fehler-Status 0: kein Fehler 1: SBE Beifahrer/OC3-Fehler SBE: Sitzbelegungserkennung, SBR - Matte : SeatBeltReminder-Matte, OC3: Occupant Classification 3te Generation |
| STAT_SBE_BEIFAHRER_BELEGT_AIRBAG_ON | int | SBE Beifahrersitz belegt (Airbag On) ab 09/05 Airbag_ON aktiv = 1, deaktiviert = 0 Bemerkung: Die Belegungsschwelle AIRBAG_ON wird ab einer Belastung von &gt; 12 Kg erreicht Uebersicht siehe table SITZBELEGUNG_FAHRER_BEIFAHRER  JOBS RESULTS SBR-MATTE SBE OC3 |
| STAT_SBE_BEIFAHRER_BELEGT_AIRBAG_ON_SBR | int | SBE Beifahrersitz belegt (Airbag On + SBR) ab E6x-09-05-350 Airbag_ON + SBR aktiv = 1, deaktiviert = 0 Bemerkung: Die Belegungsschwelle AIRBAG_ON_SBR wird erst ab -Person erkannt-  erreicht Uebersicht siehe table SITZBELEGUNG_FAHRER_BEIFAHRER  JOBS RESULTS SBR-MATTE SBE OC3 |
| STAT_SBE_BEIFAHRER_VERBAUT | int | SBE Beifahrer Sitzbelegung 0: System nicht verbaut 1: System verbaut |
| STAT_OC3_VERBAUT | int | OC3 Sitzbelegung 0: System nicht verbaut 1: System verbaut Uebersicht siehe table SITZBELEGUNG_FAHRER_BEIFAHRER  JOBS RESULTS SBR-MATTE SBE OC3 |
| STAT_FREIGABE | int | OC3 Sitzbelegung 0: kein Fehler 1: System nicht freigegeben |
| STAT_DATENSPEICHER | int | OC3 Sitzbelegung OC3 Datenspeicher-Status 0: kein Fehler 1: Datenspeicher voll |
| STAT_GEWICHTSKLASSE | int | OC3 Sitzbelegung OC3 Gewichtsklasse 0: Gewichtsklasse "0" (Leerer Sitz) 1: Gewichtsklasse "1" (Kindersitz) 2: Gewichtsklasse "2" (&gt;=5% Frau / 45kg) 3: Gewichtsklasse "3" (95% Mann Vorgehalten) 4: Gewichtsklasse "4" (RESERVE) -1: OC3 nicht verbaut / Fehler OC3  Hinweis: Switch von Klasse 0 auf Belegungsstatus erfolgt sofort Switch von Belegungsstatus auf Klasse 0 erfolgt mit einer Verzoegerung von 6 Sekunden. |
| STAT_GEWICHTSKLASSE_KINDERSITZ | int | OC3 Sitzbelegung 0: kein Fehler 1: OC3 Gewichtsklasse 1: (Kindersitz oder leerer Sitz) siehe Hinweis bei Result "STAT_GEWICHTSKLASSE"! |
| STAT_GEWICHTSKLASSE_SITZ_BELEGT | int | OC3 Sitzbelegung 0: kein Fehler OC3 Gewichtsklasse 2: (&gt;=5% Frau / 45kg) siehe Hinweis bei Result "STAT_GEWICHTSKLASSE"! |
| STAT_GEWICHTSKLASSE_UNDEFINIERT | int | OC3 Sitzbelegung 0: OC3 Gewichtsklasse definiert 1: OC3 Gewichtsklasse nicht definiert |
| STAT_UPFRONT_FA_FEHLER | int | UPFRONT Fahrerseite 0: kein Fehler 1: sendet Fehler |
| STAT_UPFRONT_FA_FEHLER_KOMMUNIKATION | int | UPFRONT Fahrerseite 0: kein Fehler 1: Kommunikationsfehler |
| STAT_UPFRONT_FA_FEHLER_LEITUNG | int | UPFRONT Fahrerseite 0: kein Fehler 1: Leitungsfehler |
| STAT_UPFRONT_FA_TYP_OKAY | int | UPFRONT Fahrerseite 0: falscher Typ 1: Typ OKAY |
| STAT_UPFRONT_BF_FEHLER | int | UPFRONT Beifahrerseite 0: kein Fehler 1: sendet Fehler |
| STAT_UPFRONT_BF_FEHLER_KOMMUNIKATION | int | UPFRONT Beifahrerseite 0: kein Fehler 1: Kommunikationsfehler |
| STAT_UPFRONT_BF_FEHLER_LEITUNG | int | UPFRONT Beifahrerseite 0: kein Fehler 1: Leitungsfehler |
| STAT_UPFRONT_BF_TYP_OKAY | int | UPFRONT Beifahrerseite 0: falscher Typ 1: Typ OKAY |
| STAT_TUER_FA_FEHLER | int | Tuer Fahrerseite Sensor 0: kein Fehler 1: sendet Fehler |
| STAT_TUER_FA_FEHLER_KOMMUNIKATION | int | Tuer Fahrerseite Sensor 0: kein Fehler 1: Kommunikationsfehler |
| STAT_TUER_FA_FEHLER_LEITUNG | int | Tuer Fahrerseite Sensor 0: kein Fehler 1: Leitungsfehler |
| STAT_TUER_FA_TYP_OKAY | int | Tuer Fahrerseite Sensor 0: falscher Typ 1: Typ OKAY |
| STAT_TUER_BF_FEHLER | int | Tuer Beifahrerseite Sensor 0: kein Fehler 1: sendet Fehler |
| STAT_TUER_BF_FEHLER_KOMMUNIKATION | int | Tuer Beifahrerseite Sensor 0: kein Fehler 1: Kommunikationsfehler |
| STAT_TUER_BF_FEHLER_LEITUNG | int | Tuer Beifahrerseite Sensor 0: kein Fehler 1: Leitungsfehler |
| STAT_TUER_BF_TYP_OKAY | int | Tuer Beifahrerseite Sensor 0: falscher Typ 1: Typ OKAY |
| STAT_BSAEULE_FA_FEHLER | int | B-Saeule Fahrerseite Sensoren 0: kein Fehler 1: sendet Fehler |
| STAT_BSAEULE_FA_FEHLER_KOMMUNIKATION | int | B-Saeule Fahrerseite Sensoren 0: kein Fehler 1: Kommunikationsfehler |
| STAT_BSAEULE_FA_FEHLER_LEITUNG | int | B-Saeule Fahrerseite Sensoren 0: kein Fehler 1: Leitungsfehler |
| STAT_BSAEULE_FA_TYP_OKAY | int | B-Saeule Beifahrerseite Sensoren 0: falscher Typ 1: Typ OKAY |
| STAT_BSAEULE_BF_FEHLER | int | B-Saeule Beifahrerseite Sensoren 0: kein Fehler 1: sendet Fehler |
| STAT_BSAEULE_BF_FEHLER_KOMMUNIKATION | int | B-Saeule Beifahrerseite Sensoren 0: kein Fehler 1: Kommunikationsfehler |
| STAT_BSAEULE_BF_FEHLER_LEITUNG | int | B-Saeule Beifahrerseite Sensoren 0: kein Fehler 1: Leitungsfehler |
| STAT_BSAEULE_BF_TYP_OKAY | int | B-Saeule Beifahrerseite Sensoren 0: falscher Typ 1: Typ OKAY |
| STAT_LEHNE_FA_VERRIEGELT | int | Lehne Fahrer 0: nicht verriegelt 1: verriegelt |
| STAT_LEHNE_FA_DEFEKT | int | Lehne Fahrer 0: nicht defekt 1: Meldet defekt |
| STAT_LEHNE_FA_SIGNAL | int | Lehne Fahrer 0: Signal gueltig 1: Signal ist ungueltig |
| STAT_LEHNE_BF_VERRIEGELT | int | Lehne Beifahrer 0: nicht verriegelt 1: verriegelt |
| STAT_LEHNE_BF_DEFEKT | int | Lehne Beifahrer 0: nicht defekt 1: Meldet defekt |
| STAT_LEHNE_BF_SIGNAL | int | Lehne Beifahrer 0: Signal guelitg 1: Signal ist ungueltig |

<a id="job-herstellerdaten-lesen"></a>
### HERSTELLERDATEN_LESEN

Kodierte KFZ-Herstellerdaten lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| TYP | string | Baureihe z.B: E60 / 20h , E61 / 21h ... Vehicle e.g: E60 / 20h , E61 / 21h ... |
| CODIERDATUM | string | z.B: 21.4.93 ... Coding date |
| WERKSKENNUNG | string | 4-stellige Dezimalzahl als String 4 character plant code (decimal) |
| HAENDLERKENNUNG | string | 5-stellige Dezimalzahl als String 5 character supplier code (decimal) |
| FGNUMMER | string | Kurze Fahrgestellnummer Short VIN |

<a id="job-hersteller-spezdaten-lesen"></a>
### HERSTELLER_SPEZDATEN_LESEN

Herstellerspezifischedaten lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| AKTUELLE_SYSTEMZEIT_HH | long | Aktuelle Systemzeit: Stunden |
| AKTUELLE_SYSTEMZEIT_MM | long | Aktuelle Systemzeit: Minuten |
| AKTUELLE_SYSTEMZEIT_SS | long | Aktuelle Systemzeit: Sekunden |
| POWER_ON_COUNTER | long | Einschaltzähler bzw. Power On - Zaehler |
| ID_PARAMETER | string | Ausgabe Algo - Versionsnummer |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |

<a id="job-verriegelung-lesen"></a>
### VERRIEGELUNG_LESEN

Auslesen des Pruefstempels / Sind Airbags scharfgeschaltet? KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default  BYTE1=BYTE2=BYTE3 =   0 = 0x00 = verriegelt BYTE1=BYTE2=BYTE3 = 255 = 0xFF = nicht verriegelt

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

Das Steuergeraet wird verriegelt Oder alternativ ueber PRUEFSTEMPEL_SCHREIBEN verriegelbar.  Hinweis zu Job PRUEFSTEMPEL_SCHREIBEN: Argument: 0 0 0 , um Steuergeraet zu verriegeln. / Airbags scharfschalten WICHTIG: Werte durch Semikolon getrennt eingeben!! ---Steuergeraet kann NUR durch die Entwicklung entriegelt werden.---  KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default

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
| DOM_DATA_UFR | binary | Ergebnis fuer DOM-Datenbank MRSA1=Upfront Beifahrerseite Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSTR | binary | Ergebnis fuer DOM-Datenbank MRSA2=MRSA Tuer Beifahrerseite Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSBRX | binary | Ergebnis fuer DOM-Datenbank MRSA3=MRSA B-Saeule x Beifahrerseite Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSBRY | binary | Ergebnis fuer DOM-Datenbank MRSA4=MRSA B-Saeule y Beifahrerseite Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSBLX | binary | Ergebnis fuer DOM-Datenbank MRSA5=MRSA B-Saeule x Fahrerseite Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSBLY | binary | Ergebnis fuer DOM-Datenbank MRSA6=MRSA B-Saeule y Fahrerseite Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_UFL | binary | Ergebnis fuer DOM-Datenbank MRSA7=Upfront Fahrerseite Herstellerdaten: Seriennumer Satelliten |
| DOM_DATA_SSTL | binary | Ergebnis fuer DOM-Datenbank MRSA8=MRSA Tuer Fahrerseite Herstellerdaten: Seriennumer Satelliten |
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

<a id="job-status-roc"></a>
### STATUS_ROC

Status des Rollover Controller lesen KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_FEHLER_AUSLOESEKREIS | int | 0 = kein Fehler, 1 = Fehler vorhanden Fehler in Auslösekreis(en) |
| STAT_UNTERSPANNUNG_KL30 | int | 0 = keine Unterspannung, 1 = Unterspannung Unterspannung Kl.30 |
| STAT_AUSLOESEANFORDERUNG | int | 0 = nicht erhalten, 1 = erhalten Auslöseanforderung an ROC |
| STAT_INTERNER_ROC_FEHLER | int | 0 = kein Fehler, 1 = Fehler vorhanden Interner Roll Over Controller - Fehler |
| STAT_PDC | int | 0 = PDC inaktiv, 1 = PDC aktiv PreDriveCheck |
| STAT_MESS_KL30_WERT | real | STAT_MESS_KL30 = Meßwert Kl.30 |
| STAT_MESS_KL30_EINH | string | Einheit: V |
| STAT_MESS_LOW_WERT | real | MESS_LOW = Messwert low zur E-Res. der Betriebssp. |
| STAT_MESS_LOW_EINH | string | Einheit: V |
| STAT_AUSL_WERT | real | STAT_AUSL = Ausloesespannung |
| STAT_AUSL_EINH | string | Einheit: V |
| STAT_MESS_LOWA_WERT | real | MESS_LOWA = Messwert low zur Ausloeskapazitaet |
| STAT_MESS_LOWA_EINH | string | Einheit: mF |
| STAT_MESSWL_WERT | real | MESSW = Messwert des Widerstands Auslösekreis li. |
| STAT_MESSWL_EINH | string | Einheit: Ohm |
| STAT_MESSWR_WERT | real | MESSWR = Messwert des Widerstands Ausloesekreis re. |
| STAT_MESSWR_EINH | string | Einheit: Ohm |

<a id="job-standard-login-roc"></a>
### STANDARD_LOGIN_ROC

Standard Login Rollover Controller KWP2000: $2E ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht-roc"></a>
### DIAGNOSE_AUFRECHT_ROC

Diagnosemode des SG aufrecht erhalten KWP2000: $2E TesterPresent Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende-roc"></a>
### DIAGNOSE_ENDE_ROC

Diagnosemode des SG beenden KWP2000: $2E StopDiagnosticSession Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-testausloesung-roc"></a>
### TESTAUSLOESUNG_ROC

Testausloesung KWP2000: $2E StopDiagnosticSession Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-tcu-notruf"></a>
### TCU_NOTRUF

Funktionstest TCU Schnittstelle Telefon-Notruf KWP2000: $31 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pol-test"></a>
### POL_TEST

Zugriff auf Steuergeräte Ein- und Ausgaenge POL leuchtet unmittelbar nach Ausführung für 1 Sekunde KWP2000: $30 InputOutputControlByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Auftrag an SG |

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
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (93 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (9 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (12 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (69 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (12 × 9)
- [IARTTEXTEERWEITERT](#table-iarttexteerweitert) (1 × 3)
- [ZEIT](#table-zeit) (1 × 8)
- [ZEIT2](#table-zeit2) (1 × 3)
- [MONATTAG](#table-monattag) (1 × 3)
- [MONAT](#table-monat) (13 × 2)
- [WOCHENTAG](#table-wochentag) (8 × 2)
- [JAHRESZEIT](#table-jahreszeit) (3 × 2)
- [SITZBELEGUNG_FAHRER_BEIFAHRER](#table-sitzbelegung-fahrer-beifahrer) (12 × 5)

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
| - | KWP2000 |
| - | KWP2000* |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 93 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x93A8 | ZK0 / Airbag Fahrer 1.Stufe |
| 0x93A9 | ZK1 / Gurtstrammer Fahrer |
| 0x93AA | ZK2 / Gurtstrammer Beifahrer |
| 0x93AB | ZK3 / Airbag Beifahrer 1.Stufe |
| 0x93AC | ZK4 / Seitenairbag Thorax vorne Fahrerseite |
| 0x93AD | ZK5 / Seitenairbag Thorax vorne Beifahrerseite |
| 0x93AE | ZK6 / Seitenairbag Thorax hinten Fahrerseite |
| 0x93AF | ZK7 / Seitenairbag Thorax hinten Beifahrerseite |
| 0x93B0 | ZK8 / Kopfairbag Fahrerseite |
| 0x93B1 | ZK9 / Kopfairbag Beifahrerseite |
| 0x93B2 | ZK10 / Sicherheitsbatterieklemme |
| 0x93B3 | ZK11 / Airbag Beifahrer 2.Stufe |
| 0x93B4 | ZK12 / Airbag Fahrer 2.Stufe |
| 0x93B5 | ZK13 / Endbeschlagstrammer hinten Fahrerseite |
| 0x93B6 | ZK14 / Endbeschlagstrammer hinten Beifahrerseite |
| 0x93B8 | ZK15 / Knieairbag Fahrer |
| 0x93F7 | ZK16 / Knieairbag Beifahrer |
| 0x93F8 | ZK17 / Endbeschlagstrammer Fahrer |
| 0x93F9 | ZK18 / Kopfstuetze Fahrer |
| 0x93FA | ZK19 / Kopfstuetze Beifahrer |
| 0x93BA | Gurtkontakt Fahrer |
| 0x93BB | Gurtkontakt Beifahrer |
| 0x93BC | Gurtkontakt hinten Fahrerseite |
| 0x93BD | Gurtkontakt hinten Beifahrerseite |
| 0x93BE | Passenger Airbag Off Schalter (POS) |
| 0x93BF | Sitzpositionssensor Fahrer SPSF |
| 0x93C1 | SBE Beifahrer |
| 0x93C2 | SBE Sitzmatte Beifahrer |
| 0x93C3 | OC3 |
| 0x93C4 | OC3 - Datenspeicher voll |
| 0x93C5 | OC3 - System noch nicht freigegeben |
| 0x93D8 | OC3 - System konnte nicht freigegeben werden |
| 0x93C6 | SLV Fahrer |
| 0x93C7 | SLV Beifahrer |
| 0x93C8 | UPFRONT Fahrerseite |
| 0x93D9 | UPFRONT Fahrerseite - falscher Messbereich |
| 0x93DA | UPFRONT Fahrerseite - Sensor Daten unplausibel |
| 0x93C9 | UPFRONT Beifahrerseite |
| 0x93DB | UPFRONT Beifahrerseite - falscher Messbereich |
| 0x93DC | UPFRONT Beifahrerseite -Sensor Daten unplausibel |
| 0x93CA | Satellit B- Saeule X Fahrerseite |
| 0x93DD | Satellit B- Saeule X Fahrerseite - falscher Messbereich |
| 0x93DE | Satellit B- Saeule X Fahrerseite - Sensor Daten unplausibel |
| 0x93CB | Satellit B- Saeule X Beifahrerseite |
| 0x93DF | Satellit B- Saeule X Beifahrerseite - falscher Messbereich |
| 0x93E0 | Satellit B- Saeule X Beifahrerseite - Sensor Daten unplausibel |
| 0x93CC | Satellit B- Saeule Y Fahrerseite |
| 0x93E1 | Satellit B- Saeule Y Fahrerseite - falscher Messbereich |
| 0x93E2 | Satellit B- Saeule Y Fahrerseite - Sensor Daten unplausibel |
| 0x93CD | Satellit B- Saeule Y Beifahrerseite |
| 0x93E3 | Satellit B- Saeule Y Beifahrerseite - falscher Messbereich |
| 0x93E4 | Satellit B- Saeule Y Beifahrerseite - Sensor Daten unplausibel |
| 0x93CE | Satellit Tuere Fahrerseite |
| 0x93E5 | Satellit Tuere Fahrerseite - falscher Messbereich |
| 0x93E6 | Satellit Tuere Fahrerseite - Sensor Daten unplausibel |
| 0x93CF | Satellit Tuere Beifahrerseite |
| 0x93E7 | Satellit Tuere Beifahrerseite - falscher Messbereich |
| 0x93E8 | Satellit Tuere Beifahrerseite - Sensor Daten unplausibel |
| 0x93F1 | Satellit Tuere Beifahrerseite - Drucksensor ausser Messbereich |
| 0x93D0 | Versorgungsspannung - Unterspannung |
| 0x93D1 | Versorgungsspannung - Ueberspannung |
| 0x93D2 | Passenger Airbag Off Leuchte (POL) |
| 0x93EB | TCU-Ausgang_(Schnittstelle Telefon - Notruf) |
| 0x93D3 | CBD -Block - CRC Fehler durch Schreiben Codierdaten |
| 0x93EC | EEPROM Layout passt nicht zur SW-Version |
| 0x93ED | Zentralsteuergeraet - Satelilliten unbekannter Fehler |
| 0x93EE | Satellit Tuere Fahrerseite - Drucksensor ausser Messbereich |
| 0x93D4 | Crashtelegrammspeicher - Mindestens ein Crashtelegramm ist gespeichert |
| 0x93D5 | Crashtelegrammspeicher - Drei Crashtelegramme sind gespeichert |
| 0x93FB | Geschwindigkeit - Geschwindigkeitssignal fehlt |
| 0x93FC | B+ - Leitung |
| 0x93FD | B- - Leitung |
| 0x93FE | Roll over Function - Sensor nicht verbaut |
| 0x93FF | RollOverController |
| 0x9401 | RollOverController - Alive-Zaehler fehlerhaft |
| 0x9402 | RollOverController - Interner Fehler |
| 0x9403 | RollOverController - Ausloesekreis links |
| 0x9404 | RolloverController - Ausloesekreis rechts |
| 0x9405 | RollOverController - Datenspeicher voll |
| 0x9406 | RollOverController - Unterspannung |
| 0x9407 | RollOverController - PDC dauert zu lange |
| 0x9409 | RollOverController - Weiterer PDC im Normalbetrieb |
| 0x9400 | SBE Beifahrer - Fehlverbau SBE - Typ |
| 0x940B | Drehratensensor - AD - Wandler übersteuert |
| 0x940C | Drehratensensor - Sensorelement schwingt nicht |
| 0x940D | LCD Leuchtdichte - Telegramm mit Helligkeitsinfo nicht empfangen |
| 0x93D6 | Zentralsteuergeraet - SG ist nicht verriegelt |
| 0x93D7 | Zentralsteuergeraet - Interner Fehler |
| 0xC944 | Bus Leitungsfehler - Allg. |
| 0x940A | Ueberspannung im PDC |
| 0x9408 | Unterspannung im PDC |
| 0xC947 | Bus Kommunikationsfehler |
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

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 69 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xC200 | Interner Beschleunigungsmesser X - Aktiver Selbsttest nicht bestanden |
| 0xC201 | Interner Beschleunigungsmesser X - Offset außerhalb zugelassener Abweichungen |
| 0xC203 | Interner Beschleunigungsmesser Y - Aktiver Selbsttest nicht bestanden |
| 0xC204 | Interner Beschleunigungsmesser Y - Offset außerhalb zugelassener Abweichungen |
| 0xC206 | Interner Low-G Beschleunigungsmesser Y - Aktiver Selbsttest nicht bestanden |
| 0xC207 | Interner Low-G Beschleunigungsmesser Y - Offset außerhalb zugelassener Abweichungen |
| 0xC208 | Interner Low-G Beschleunigungsmesser Y - Plausibilitätsfehler |
| 0xC209 | Interner Low-G Beschleunigungsmesser Z - Aktiver Selbsttest nicht bestanden |
| 0xC20A | Interner Low-G Beschleunigungsmesser Z - Offset außerhalb zugelassener Abweichungen |
| 0xC20B | Interner Low-G Beschleunigungsmesser Z - Plausibilitätsfehler |
| 0xC20C | Gyro - ungueltige Daten |
| 0xC20D | Gyro - Unrealistischer Messwert |
| 0xC20E | Gyro - Offset außerhalb zugelassener Abweichungen |
| 0xC20F | Gyro - Selbsttest nicht bestanden |
| 0xC210 | RSU ASIC 1 - Erhöhte Temperatur im RSU ASIC 1 diagnostisiert |
| 0xC211 | RSU ASIC 2 - Erhöhte Temperatur im RSU ASIC 2 diagnostisiert |
| 0xC212 | ASIC 3 - Fehlerhafte Funktion der internen High Side Transistoren in ASIC3 |
| 0xC213 | ASIC 1 - Fehlerhafte Funktion der internen Low Side Transistoren in ASIC1 |
| 0xC214 | ASIC 2 - Fehlerhafte Funktion der internen Low Side Transistoren in ASIC2 |
| 0xC215 | ASIC 3 - Fehlerhafte Funktion der internen Low Side Transistoren in ASIC3 |
| 0xC216 | ASIC 1 - Missglücktes Entriegeln / Verriegeln des Firing ASIC 1 |
| 0xC217 | ASIC 2 - Missglücktes Entriegeln / Verriegeln des Firing ASIC 2 |
| 0xC218 | ASIC 3 - Missglücktes Entriegeln / Verriegeln des Firing ASIC 3 |
| 0xC219 | ASIC 1 - Messresultat des Referenzstroms, ASIC 1, außerhalb zugelassener Abweichungen |
| 0xC21A | ASIC 2 - Messresultat des Referenzstroms, ASIC 2, außerhalb zugelassener Abweichungen |
| 0xC21B | ASIC 3 - Messresultat des Referenzstroms, ASIC 3, außerhalb zugelassener Abweichungen |
| 0xC21C | EEPROM - Inkorrekte Kontrollsumme |
| 0xC21D | EEPROM - Missglückte Datenablage im EEPROM |
| 0xC21E | Energiereserve - Kapazitaetsmesswert der Energiereserve ermittelt im Startup außerhalb zugelassener Abweichungen |
| 0xC21F | Energiereserve - Kapazitaetsmesswert der Energiereserve ermittelt in der zyklischen Pruefung außerhalb zugelassener Abweichungen |
| 0xC220 | Energiereserve - Spannungswert der Energiereserve unterhalb des unteren Schwellwerts |
| 0xC221 | Power supply - Diode zwischen der Spannungsversorgung und der Energiereserve defekt |
| 0xC222 | Arming- Test des Arming-Signals missglueckt |
| 0xC223 | ASIC 1 - Fehlerhafte Funktion der internen high Side Transistoren in ASIC1 |
| 0xC224 | ASIC 2 - Fehlerhafte Funktion der internen High Side Transistoren in ASIC2 |
| 0xC225 | External HSS - Fehlerhafte Funktion der externen High Side Transistoren |
| 0xC226 | Hilfsprozessor MCU - Armierungsprozessor ( Hilfsprozessor ) detektiert Offset außerhalb zugelassener Abweichungen - High-G X- Sensor |
| 0xC227 | Hilfsprozessor MCU - Armierungsprozessor ( Hilfsprozessor ) detektiert Offset außerhalb zugelassener Abweichungen - High-G Y- Sensor |
| 0xC228 | Hilfsprozessor MCU - Armierungsprozessor ( Hilfsprozessor ) detektiert Offset außerhalb zugelassener Abweichungen - Low-G Y- Sensor |
| 0xC229 | Hilfsprozessor MCU - Armierungsprozessor ( Hilfsprozessor ) detektiert Offset außerhalb zugelassener Abweichungen - Low-G Z- Sensor |
| 0xC22A | Hilfsprozessor MCU - Armierungsprozessor ( Hilfsprozessor ) detektiert: Aktiver Selbsttest nicht bestanden - interner High-G Sensor |
| 0xC22B | Hilfsprozessor MCU - Armierungsprozessor ( Hilfsprozessor ) detektiert: Aktiver Selbsttest nicht bestanden - interner Low-G Sensor |
| 0xC22C | RAM - Test Datenablage im RAM missglueckt |
| 0xC22D | ROM - Inkorrekte Kontrollsumme - ROM |
| 0xC22E | Watchdog - Aktiver Watchdogtest missglückt |
| 0xC22F | MCU - inkorrekte Reihenfolge im Programmablauf |
| 0xC230 | ADC - Timeout bei ADC - Umwandlung |
| 0xC231 | ADC - Referenzfehler bei ADC - Umwandlung |
| 0xc232 | Algo - Zündentscheidung mit Zeitverzögerung durch Arming nicht bestätigt |
| 0xC235 | RSU ASIC 0 Fehler |
| 0xC236 | RSU ASIC 1 Fehler |
| 0xC237 | Aux - Software Version des Hilfscontrollers inkompatibel |
| 0xC238 | Gyro - ADC Überlauf |
| 0xC239 | Gyro - Exc Fehler |
| 0xC23A | Gyro - Arithmetischer Übelauf Drehratensensor |
| 0xC23B | Gyro - OTP Paritätsfehler Drehratensensor |
| 0xC23C | Gyro - Spannung des Drehratensensors ausserhalb des zulässigem Bereichs |
| 0xC23D | EEPROM - Checksummen-Fehler im Bereich der AES Konfigurationsdaten |
| 0xC23E | EEPROM - Checksummen-Fehler direkt nach dem Flashen |
| 0xC23F | Aux MCU - Fehler im Programmablauf im Hilfs-Prozessor |
| 0xC240 | Arming - Zündentscheidung lag vor, aber keine Bestätigung durch Arming |
| 0xC241 | Aux MCU - Hauptkontroller Kommunikationsfehler bzw. Synchronisierungsfehler |
| 0xC242 | Fehler im Control ASIC |
| 0xC243 | Batterieleitungsdiagnose- ECU interner Fehler |
| 0xC244 | Crashparametersatz nur fuer Testzwecke geeignet |
| 0xC245 | Hilfsprozessor MCU -Fehler auf der RSU SPI Leitung |
| 0xC246 | Watchdog - 5V Reset |
| 0xC247 | Hilfsprozessor MCU - Arming Replica Error |
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
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

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

<a id="table-iarttexteerweitert"></a>
### IARTTEXTEERWEITERT

Dimensions: 1 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxxx | 0 | Kein passendes Fehlersymptom |

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

<a id="table-sitzbelegung-fahrer-beifahrer"></a>
### SITZBELEGUNG_FAHRER_BEIFAHRER

Dimensions: 12 rows × 5 columns

| JOBS | RESULTS | SBR-MATTE | SBE | OC3 |
| --- | --- | --- | --- | --- |
| 1. STATUS_LESEN | STAT_SITZBELEGUNG_BEIFAHRER | kann Zustand 'unbelegt' nicht ausgeben | gibt zustaetzlich den Zustand unbelegt aus | gibt den Zustand unbelegt ueber den Zustand Gewichtsklasse 0 aus |
| 2. STATUS_LESEN | STAT_SBE_BEIFAHRER_BELEGT_AIRBAG_ON | Sitzbelegung wird ausgegeben, aber keinen Einfluss auf das Ausloesen von Rueckhaltemitteln | Sitzbelegung wird ausgegeben und Einfluss auf das Ausloesen von Rueckhaltemitteln | Sitzbelegung wird ausgegeben und Einfluss auf das Ausloesen von Rueckhaltemitteln |
| 3. STATUS_LESEN | STAT_SBE_BEIFAHRER_BELEGT_AIRBAG_ON_SBR | Sitzbelegung wird ausgegeben, aber keinen Einfluss auf das Ausloesen von Rueckhaltemitteln | Sitzbelegung wird ausgegeben und Einfluss auf das Ausloesen von Rueckhaltemitteln | Sitzbelegung wird ausgegeben und Einfluss auf das Ausloesen von Rueckhaltemitteln |
| 4. STATUS_LESEN | STAT_SBE_BEIFAHRER_VERBAUT | Info ob SBE im SG codiert ist | Info ob SBE im SG codiert ist | - |
| 5. STATUS_LESEN | STAT_SITZBELEGUNG_FAHRER | kann Zustand 'unbelegt' nicht ausgeben | System fahrerseitig nicht vorhanden | System fahrerseitig nicht vorhanden |
| 6. STATUS_LESEN | STAT_SBE_FAHRER_VERBAUT | Info ob Fahrer-SBE in SG codiert ist | System fahrerseitig nicht vorhanden | System fahrerseitig nicht vorhanden |
| 7. STATUS_LESEN | STAT_OC3_VERBAUT | - | - | Info ob OC3 im SG codiert ist |
| 8. STATUS_LESEN | STAT_FREIGABE | - | - | OC3 System ist noch nicht ueber SG freigegeben worden |
| 9. STATUS_LESEN | STAT_DATENSPEICHER | - | - | Datenspeicher der OC3 muss geloescht werden |
| 10. STATUS_LESEN | STAT_GEWICHTSKLASSE | - | - | Ausgabe der Belegungszustaende |
| 11. STATUS_AUSSTATTUNG | STAT_SBR_MATTE_BEIFAHRER_VERBAUT | Dieses Bit gibt Aufschluss, ob SBE oder SBR Matte verbaut wurde. Wird der Zustand unbelegt ausgegeben, wird im Fehlerspeicher ein Fehlerverbau gesetzt | - | - |
| 12. STATUS_AUSSTATTUNG | STAT_SBR_MATTE_FAHRER_VERBAUT | Dieses Bit gibt Aufschluss, ob SBE oder SBR-Matte verbaut wurde. Wird der Zustand unbelegt ausgegeben, wird ein Plausibilitaetsfehler ueber das K-CAN Telegramm ausgegeben | - | - |
