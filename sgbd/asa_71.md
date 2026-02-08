# asa_71.prg

- Jobs: [64](#jobs)
- Tables: [31](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Aktuator Steuergerät Aktivlenkung |
| ORIGIN | BMW EF-611 Sonja Kutny |
| REVISION | 3.001 |
| AUTHOR | BMW EF-611 Sonja_Kutny |
| COMMENT | N/A |
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
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
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
- [STATUS_TEMPERATUR](#job-status-temperatur) - Auslesen der Steuergeraetetemperatur KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $05 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_MOTORLAGEWINKEL](#job-status-motorlagewinkel) - Auslesen verschiedener Motorlagewinkel KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $09 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_PHASENSPANNUNGEN](#job-status-phasenspannungen) - Auslesen der Phasenspanngen U1,U2,U3 am Stellmotor, Stator KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $10 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_PHASENSTROEME](#job-status-phasenstroeme) - Auslesen der Phasenstrome I1,I2,I3 am Stellmotor, Stator KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $04 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_ALIVE_INFO](#job-status-alive-info) - Auslesen verschiedener ALIVE Zaehler KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $13 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_CAS_INFO](#job-status-cas-info) - Auslesen der vom CAS gesendeten Fahrgestellnummer ueber PT-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $16 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [IDENT_ISTUFE_LESEN](#job-ident-istufe-lesen) - Auslesen der aktuellen Integrationsstufe KWP2000: $1A ReadECUIdentification SubID  : $82 reserved by Document Modus  : Default
- [STATUS_VERSORGUNGEN](#job-status-versorgungen) - Auslesen der aktuellen Spanungspegel KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $01 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default
- [STATUS_PTCAN_SIGNAL_FEHLER](#job-status-ptcan-signal-fehler) - diverse vom ASA eingelesene PTCAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $1B InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_ICMCAN_SIGNAL_FEHLER](#job-status-icmcan-signal-fehler) - diverse vom ASA eingelesene ICMCAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $1C InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_ZFLS_SW_NR_LESEN](#job-status-zfls-sw-nr-lesen) - Auslesen der ZFLS Software-Nummern KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $02 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STATUS_MLW_INIT](#job-status-mlw-init) - Gueltigkeit des Motorlagewinkels auslesen KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $50 Inbetriebnahme Resultat abfragen Modus  : Default
- [STATUS_OPERATINGSYSTEM](#job-status-operatingsystem) - Auslesen verschiedener Betriebssystem (OS, SG) Stati KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $02 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default
- [STEUERN_MOTORLAGEWINKEL_UNGUELTIG](#job-steuern-motorlagewinkel-ungueltig) - Motorlagewinkel wird ungueltig gesetzt KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $21 Motorlagewinkel ungueltig setzen Modus  : Default KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $50 Gueltigkeit Motorlagewinkel abfragen Modus  : Default
- [STEUERN_FAHRGESTELLNUMMER_ABGLEICH](#job-steuern-fahrgestellnummer-abgleich) - Abgleich der Fahrgestellnummer Modus  : Default
- [STATUS_BOOTBLOCKINFO](#job-status-bootblockinfo) - Auslesen der Bootblockinformationen KWP2000: $22 InputOutputControlByLocalIdentifier SubID  : $25 InputOutputLocalIdentifier(IOLI) SubID  : $07 InputOutputControlParameter(IOCP) Modus  : Default
- [STEUERN_RESET_DATA_FLASH](#job-steuern-reset-data-flash) - Reset des DataFlash KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $22 Reset des DataFlash Modus  : Default

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

<a id="job-status-temperatur"></a>
### STATUS_TEMPERATUR

Auslesen der Steuergeraetetemperatur KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $05 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZWK_TEMPERATUR_WERT | real | SG-Innentemperatur an Endstufe auf der Platine gemessen Skalierungsfaktor: ( 1 ) Einheit: ( Grad Celsius ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_TEMPERATUR_EINH | string | Einheit der Temperatur Einheit: ( Grad Celsius ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-motorlagewinkel"></a>
### STATUS_MOTORLAGEWINKEL

Auslesen verschiedener Motorlagewinkel KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $09 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MLW_ISTWERT_NEC_WERT | real | Motorlagewinkel Absoultwert in Grad eingelesen vom NEC Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MLW_ISTWERT_GUELTIGKEIT_NEC_WERT | int | aktueller Zustand des Motorlagewinkels NEC Wertebereich: ( 0,1,2 ) moegliche Zustaende: ( 0 -- &gt; nicht gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; Initialisierung ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MLW_ISTWERT_GUELTIGKEIT_NEC_TEXT | string | aktueller Zustand des Motorlagewinkels NEC moegliche Zustaende: ( 0 -- &gt; nicht gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; Initialisierung ) Textausgabe ueber Tabelle: ( GueRotor ) |
| STAT_MLW_ISTWERT_S12_WERT | real | Motorlagewinkel Absoultwert in Grad eingelesen vom S12X Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MLW_ISTWERT_GUELTIGKEIT_S12_WERT | int | aktueller Zustand des Motorlagewinkels NEC Wertebereich: ( 0,1,2 ) moegliche Zustaende: ( 0 -- &gt; nicht gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; Initialisierung ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_MLW_ISTWERT_GUELTIGKEIT_S12_TEXT | string | aktueller Zustand des Motorlagewinkels NEC moegliche Zustaende: ( 0 -- &gt; nicht gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; Initialisierung ) Textausgabe ueber Tabelle: ( GueRotor ) |
| STAT_MLW_SOLLWERT_NEC_WERT | real | Motorlagewinkel NEC Absoultwert in Grad Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MLW_SOLLWERT_S12_WERT | real | Motorlagewinkel S12X Absoultwert in Grad Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_MOTORLAGEWINKEL_EINH | string | Einheit des Motorwinkels Einheit: ( Grad Motorwinkel ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-phasenspannungen"></a>
### STATUS_PHASENSPANNUNGEN

Auslesen der Phasenspanngen U1,U2,U3 am Stellmotor, Stator KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $10 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHASENSPANNUNG_U1_WERT | long | Spannung U1 am Stator des Stellmotors Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSPANNUNG_U2_WERT | long | Spannung U2 am Stator des Stellmotors Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSPANNUNG_U3_WERT | long | Spannung U3 am Stator des Stellmotors Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSPANNUNG_EINH | string | Einheit der Spannung Einheit: ( Volt ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-phasenstroeme"></a>
### STATUS_PHASENSTROEME

Auslesen der Phasenstrome I1,I2,I3 am Stellmotor, Stator KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $04 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHASENSTROM_I1_WERT | real | Phasenstrom I1 am Stator des Stellmotors Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSTROM_I2_WERT | real | Phasenstrom I2 am Stator des Stellmotors Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSTROM_I3_WERT | real | Phasenstrom I3 am Stator des Stellmotors Telegrammlaenge KWP: ( 4 Byte ) |
| STAT_PHASENSTROM_EINH | string | Einheit des Stroms Einheit: ( Ampere ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-alive-info"></a>
### STATUS_ALIVE_INFO

Auslesen verschiedener ALIVE Zaehler KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $13 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SG_ALIVE_WERT | int | Alivezaehler vom ASA Wertebereich: ( 0..14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SPI_ALIVE_WERT | int | Alivezaehler der SPI Wertebereich: ( 0..14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ICM_ALIVE_WERT | int | Alivezaehler vom ICM Wertebereich: ( 0..14 ) Telegrammlaenge KWP: ( 1 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-cas-info"></a>
### STATUS_CAS_INFO

Auslesen der vom CAS gesendeten Fahrgestellnummer ueber PT-CAN KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $16 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CAS_FAHRGESTELLNR_WERT | string | vom ASA eingelesene Fahrgestellnummer ueber PT-CAN CAN-ID: (896 / 0x380) Telegrammlaenge KWP: ( 8 Byte ) |
| STAT_GUELTIGKEIT_CAS_FAHRGESTELLNR_WERT | int | Gueltigkeit der Fahrgestellnummer CAN Botschaft vom CAS ueber PT-CAN CAN-ID: (896 / 0x380) Wertebereich: ( 00,02,04,08,10,20,40,80 ) moegliche Zustaende: ( 0x00 -- &gt; Botschaft i.o. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) moegliche Zustaende: ( 0x08 -- &gt; Timeout - Botschaft faellt fuer 1 Zyklus aus ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) moegliche Zustaende: ( 0x80 -- &gt; mehrere Fehler ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_CAS_FAHRGESTELLNR_TEXT | string | Gueltigkeit der Fahrgestellnummer CAN Botschaft vom CAS ueber PT-CAN CAN-ID: (896 / 0x380) Wertebereich: ( 00,02,04,08,10,20,40,80 ) moegliche Zustaende: ( 0x00 -- &gt; Botschaft i.o. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) moegliche Zustaende: ( 0x08 -- &gt; Timeout - Botschaft faellt fuer 1 Zyklus aus ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) moegliche Zustaende: ( 0x80 -- &gt; mehrere Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-ident-istufe-lesen"></a>
### IDENT_ISTUFE_LESEN

Auslesen der aktuellen Integrationsstufe KWP2000: $1A ReadECUIdentification SubID  : $82 reserved by Document Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_INTEGRATIONS_STUFE_TEXT | string | aktuelle Interationssufe z.B. 'E070-06-10-310' Telegrammlaenge KWP: ( 14 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-versorgungen"></a>
### STATUS_VERSORGUNGEN

Auslesen der aktuellen Spanungspegel KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $01 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLEMME30_WERT | real | Spannungswert an Klemme 30 Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_KLEMME15N_WERT | real | Spannungswert an Klemme 15N Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SENSOR_VERSORGUNG_WERT | real | Spannungswert des Sensors Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SPANNUNG_ZWISCHENKREIS_WERT | real | Zwischenkreisspannung Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SPANNUNGSUEBERWACHUNG_5V_WERT | real | Spannungsueberwachung 5 Volt Einheit: ( Volt ) Telegrammlaenge KWP: ( 2 Byte ) |
| STAT_SPANNUNGSUEBERWACHUNG_WERT | int | Spannungsueberwachung Einheit: ( ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SPANNUNGSUEBERWACHUNG_TEXT | string | Spannungsueberwachung Textausgabe ueber Tabelle: ( StatusmaschineZustaende ) |
| STAT_SPANNUNG_EINH | string | Einheit der Spannung Einheit: ( Volt ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-ptcan-signal-fehler"></a>
### STATUS_PTCAN_SIGNAL_FEHLER

diverse vom ASA eingelesene PTCAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $1B InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; Botschaft i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) moegliche Zustaende: ( 0x08 -- &gt; Timeout-Fehler ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) moegliche Zustaende: ( 0x80 -- &gt; mehrere Fehler ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Timeout-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KILOMETERSTAND_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (816 / 0x330) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; mehrere Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KLEMMENSTATUS_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; Botschaft i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) moegliche Zustaende: ( 0x08 -- &gt; Timeout-Fehler ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) moegliche Zustaende: ( 0x80 -- &gt; mehrere Fehler ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_KLEMMENSTATUS_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KLEMMENSTATUS_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KLEMMENSTATUS_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Timeout-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KLEMMENSTATUS_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KLEMMENSTATUS_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KLEMMENSTATUS_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_KLEMMENSTATUS_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (304 / 0x130) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; mehrere Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_FGNR_CAN_FEHLER_WERT | int | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; Botschaft i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) moegliche Zustaende: ( 0x08 -- &gt; Timeout-Fehler ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) moegliche Zustaende: ( 0x80 -- &gt; mehrere Fehler ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_FGNR_CAN_FEHLER_BIT1_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT2_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT3_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Timeout-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT4_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT5_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT6_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_FGNR_CAN_FEHLER_BIT7_TEXT | string | PTCAN Signalfehler CAN-ID: (896 / 0x380) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; mehrere Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-icmcan-signal-fehler"></a>
### STATUS_ICMCAN_SIGNAL_FEHLER

diverse vom ASA eingelesene ICMCAN Signale KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $1C InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TAR_STEA_FTAX_ACT_CAN_FEHLER_WERT | int | ICMCAN Signalfehler CAN-ID: (315 / 0x13B) Wertebereich: ( 0,2,4,8,16,32,64,128 ) moegliche Zustaende: ( 0x00 -- &gt; Botschaft i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) moegliche Zustaende: ( 0x08 -- &gt; Timeout-Fehler ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) moegliche Zustaende: ( 0x80 -- &gt; mehrere Fehler ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_TAR_STEA_FTAX_ACT_CAN_FEHLER_BIT1_TEXT | string | ICMCAN Signalfehler CAN-ID: (315 / 0x13B) Wertebereich: ( 0, 2 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 1 i.O. ) moegliche Zustaende: ( 0x02 -- &gt; Botschaft wurde nie empfangen ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_TAR_STEA_FTAX_ACT_CAN_FEHLER_BIT2_TEXT | string | ICMCAN Signalfehler CAN-ID: (315 / 0x13B) Wertebereich: ( 0, 4 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 2 i.O. ) moegliche Zustaende: ( 0x04 -- &gt; Mehrere Botschaften pro Abtastzyklus ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_TAR_STEA_FTAX_ACT_CAN_FEHLER_BIT3_TEXT | string | ICMCAN Signalfehler CAN-ID: (315 / 0x13B) Wertebereich: ( 0, 8 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 3 i.O. ) moegliche Zustaende: ( 0x08 -- &gt; Timeout-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_TAR_STEA_FTAX_ACT_CAN_FEHLER_BIT4_TEXT | string | ICMCAN Signalfehler CAN-ID: (315 / 0x13B) Wertebereich: ( 0, 16 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 4 i.O. ) moegliche Zustaende: ( 0x10 -- &gt; Fehlerwert laut Nachrichtenkatalog ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_TAR_STEA_FTAX_ACT_CAN_FEHLER_BIT5_TEXT | string | ICMCAN Signalfehler CAN-ID: (315 / 0x13B) Wertebereich: ( 0, 32 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 5 i.O. ) moegliche Zustaende: ( 0x20 -- &gt; Alive-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_TAR_STEA_FTAX_ACT_CAN_FEHLER_BIT6_TEXT | string | ICMCAN Signalfehler CAN-ID: (315 / 0x13B) Wertebereich: ( 0, 64 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 6 i.O. ) moegliche Zustaende: ( 0x40 -- &gt; Checksummen-Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| STAT_TAR_STEA_FTAX_ACT_CAN_FEHLER_BIT7_TEXT | string | ICMCAN Signalfehler CAN-ID: (315 / 0x13B) Wertebereich: ( 0, 128 ) moegliche Zustaende: ( 0x00 -- &gt; Bit 7 i.O. ) moegliche Zustaende: ( 0x80 -- &gt; mehrere Fehler ) Textausgabe ueber Tabelle: ( StatusCANFehler ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-zfls-sw-nr-lesen"></a>
### STATUS_ZFLS_SW_NR_LESEN

Auslesen der ZFLS Software-Nummern KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $02 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZFLS_SW_NR_NEC_WERT | string | ZFLS Software-Nummer NEC Telegrammlaenge KWP: ( 19 Byte ) |
| STAT_ZFLS_SW_NR_S12_WERT | string | ZFLS Software-Nummer S12 Telegrammlaenge KWP: ( 19 Byte ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-mlw-init"></a>
### STATUS_MLW_INIT

Gueltigkeit des Motorlagewinkels auslesen KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $50 Inbetriebnahme Resultat abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GUELTIGKEIT_MLW_WERT | int | aktueller Zustand des Motorlagewinkels Wertebereich: ( 0,1,2 ) moegliche Zustaende: ( 0 -- &gt; nicht gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; Initialisierung ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_MLW_TEXT | string | aktueller Zustand des Motorlagewinkels moegliche Zustaende: ( 0 -- &gt; nicht gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; Initialisierung ) Textausgabe ueber Tabelle: ( GueRotor ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-operatingsystem"></a>
### STATUS_OPERATINGSYSTEM

Auslesen verschiedener Betriebssystem (OS, SG) Stati KWP2000: $30 InputOutputControlByLocalIdentifier SubID  : $02 InputOutputLocalIdentifier(IOLI) SubID  : $01 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMZUSTAND_NEC_WERT | int | stellt den Systemzustand des NEC dar Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SYSTEMZUSTAND_NEC_TEXT | string | stellt den Systemzustand des NEC dar Textausgabe ueber Tabelle: ( StatusmaschineZustaende ) |
| STAT_SYSTEMZUSTAND_S12X_WERT | int | stellt den Systemzustand des S12X dar Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_SYSTEMZUSTAND_S12X_TEXT | string | stellt den Systemzustand des S12X dar Textausgabe ueber Tabelle: ( StatusmaschineZustaende ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-steuern-motorlagewinkel-ungueltig"></a>
### STEUERN_MOTORLAGEWINKEL_UNGUELTIG

Motorlagewinkel wird ungueltig gesetzt KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $21 Motorlagewinkel ungueltig setzen Modus  : Default KWP2000: $33 RequestRoutineResultsByLocalIdentifier SubID  : $50 Gueltigkeit Motorlagewinkel abfragen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GUELTIGKEIT_MLW_WERT | int | Wertebereich: ( 0,1,2 ) moegliche Zustaende: ( 0 -- &gt; nicht gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; Initialisierung ) Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_GUELTIGKEIT_MLW_TEXT | string | moegliche Zustaende: ( 0 -- &gt; nicht gueltig ) moegliche Zustaende: ( 1 -- &gt; gueltig ) moegliche Zustaende: ( 2 -- &gt; Initialisierung ) Textausgabe ueber Tabelle: ( GueRotor ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG_1 | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT_1 | binary | Hex - Antwort von SG |
| _TEL_DATEN_1 | binary | Hex - Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex - Antwort von SG |
| _TEL_DATEN_2 | binary | Hex - Antwort von SG |

<a id="job-steuern-fahrgestellnummer-abgleich"></a>
### STEUERN_FAHRGESTELLNUMMER_ABGLEICH

Abgleich der Fahrgestellnummer Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-status-bootblockinfo"></a>
### STATUS_BOOTBLOCKINFO

Auslesen der Bootblockinformationen KWP2000: $22 InputOutputControlByLocalIdentifier SubID  : $25 InputOutputLocalIdentifier(IOLI) SubID  : $07 InputOutputControlParameter(IOCP) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BOOTLOADER_STATUS_WERT | int | Gibt an ob BB ueber Bootloader geflasht wurde Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_BOOTLOADER_STATUS_TEXT | string | stellt den Bootloderstatus dar Textausgabe ueber Tabelle: ( BootloaderZustaende ) |
| STAT_BOOTLOADER_INDEX_WERT | int | Gibt an welcher BB ueber Bootloader geflasht wurde Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ENGINEERING_BB_WERT | int | Gibt an ob BB ein Egineering BB ist Telegrammlaenge KWP: ( 1 Byte ) |
| STAT_ENGINEERING_BB_TEXT | string | stellt den Engineeringstatus dar Textausgabe ueber Tabelle: ( EngineeringZustaende ) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

<a id="job-steuern-reset-data-flash"></a>
### STEUERN_RESET_DATA_FLASH

Reset des DataFlash KWP2000: $31 StartRoutineByLocalIdentifier SubID  : $22 Reset des DataFlash Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Textausgabe ueber Tabelle: ( JobResult ) |
| _TEL_AUFTRAG | binary | Hex - Auftrag an SG |
| _TEL_ANTWORT | binary | Hex - Antwort von SG |
| _TEL_DATEN | binary | Hex - Antwort von SG |

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
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (41 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (6 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (132 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (20 × 9)
- [GUEROTOR](#table-guerotor) (5 × 2)
- [STATUSMASCHINEZUSTAENDE](#table-statusmaschinezustaende) (12 × 2)
- [STATUSCANFEHLER](#table-statuscanfehler) (9 × 2)
- [FEHLERUMWELTBMW](#table-fehlerumweltbmw) (1 × 7)
- [INFOUMWELTBMW](#table-infoumweltbmw) (1 × 21)
- [SPANNUNGSUEBERWACHUNG](#table-spannungsueberwachung) (3 × 2)
- [BOOTLOADERZUSTAENDE](#table-bootloaderzustaende) (2 × 2)
- [ENGINEERINGZUSTAENDE](#table-engineeringzustaende) (2 × 2)

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
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 41 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x612C | Steuergeraet: Hardwarefehler |
| 0x612D | Steuergeraet: Programmablaufueberwachung |
| 0x612E | Steuergeraet: Fahrgestellnummer |
| 0x612F | Steuergeraet: Unterspannung |
| 0x6130 | Steuergeraet: Ueberspannung |
| 0x6131 | Motordynamik |
| 0x6132 | Steuergeraet: Codierfehler |
| 0x6133 | Motorlagesensor |
| 0x6134 | Motorstrom / Motorspannung |
| 0x6135 | Motorlage |
| 0x6136 | Sperrenfehler |
| 0x6137 | Selbsthemmungsueberwachung |
| 0x6138 | Kombinierte Lage- Drehzahlüberwachung |
| 0x6139 | nicht benutzt |
| 0x613A | Steuergeraet: Diversitaeres Rechnen |
| 0x613B | Steuergeraet: Flashfehler |
| 0x613C | Steuergeraet: Betriebssystem |
| 0x613D | Klemme 30 |
| 0x613E | Motorlage initialisieren |
| 0x613F | Steuergeraet: Aufstartverzoegerung |
| 0xCE84 | nicht benutzt |
| 0xCE85 | nicht benutzt |
| 0xCE86 | nicht benutzt |
| 0xCE87 | PT-CAN Kommunikationsfehler |
| 0xCE88 | nicht benutzt |
| 0xCE89 | nicht benutzt |
| 0xCE8A | nicht benutzt |
| 0xCE8B | ICM-CAN Kommunikationsfehler |
| 0xCE8C | nicht benutzt |
| 0xCE8D | nicht benutzt |
| 0xCE8E | nicht benutzt |
| 0xCE8F | nicht benutzt |
| 0xCE90 | nicht benutzt |
| 0xCE91 | nicht benutzt |
| 0xCE92 | nicht benutzt |
| 0xCE93 | nicht benutzt |
| 0xCE94 | Botschaft (Solllenkwinkelvorgabe, ID=0x13B) von ICM auf ICM-CAN |
| 0xCE95 | Botschaft (Klemmenstatus, ID=0x130) von CAS auf PT-CAN |
| 0xCE96 | Boschaft (Fahrgestellnummer, ID=0x130) von CAS auf PT-CAN |
| 0xCE97 | Botschaft (Motordaten, ID=0x1D0) von DME auf PT-CAN |
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

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | FehlerUmweltBMW | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 6 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Absolutzeit | ms | high | signed long | - | 1 | 1 | 0 |
| 0x02 | Fehlercode | -- | - | unsigned char | - | 1 | 1 | 0 |
| 0x03 | Fehlerart | -- | - | unsigned char | - | 1 | 1 | 0 |
| 0x04 | OS Status | -- | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | Spannung Klemme15 | Volt | - | unsigned char | - | 128 | 1000 | 0 |
| 0x06 | Temperatur | °C | - | signed char | - | 1 | 1 | 0 |

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

Dimensions: 132 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x7001 | NVM_E_WRITE_FAILED |
| 0x7002 | NVM_E_READ_FAILED |
| 0x7003 | NVM_E_CONTROL_FAILED |
| 0x7004 | NVM_E_ERASE_FAILED |
| 0x7005 | NVM_E_READ_ALL_FAILED |
| 0x7006 | NVM_E_WRITE_ALL_FAILED |
| 0x7007 | NVM_E_WRONG_CONFIG_ID |
| 0x7008 | nicht benutzt |
| 0x7009 | ERRHDL_MIN |
| 0x700a | KFC_SW |
| 0x700b | KFC_DRLS |
| 0x700c | KFC_ACTIVE_DIAG |
| 0x700d | KFC_S12_RLS_COMPARE |
| 0x700e | KFC_US |
| 0x700f | KFC_SMCURR |
| 0x7010 | KFC_SMPOS |
| 0x7011 | KFC_PROG |
| 0x7012 | KFC_BRAKE |
| 0x7013 | KFC_ADC |
| 0x7014 | KFC_SMCOM |
| 0x7015 | KFC_SELFLOCK |
| 0x7016 | KFC_ACT_KLD |
| 0x7017 | KFC_WRONG_KFC_FROM_ZFLS |
| 0x7018 | KFC_ACT_BLOCK |
| 0x7019 | KFC_WACKEL |
| 0x701a | KFC_SENS_SLGS |
| 0x701b | KFC_TAR_STEA_MSG |
| 0x701c | KFC_DISCHARGE |
| 0x701d | KFC_S12_OS |
| 0x701e | KFC_AGB |
| 0x701f | KFC_PWR_KL30 |
| 0x7020 | KFC_S12_STM_ERROR |
| 0x7021 | KFC_S12_TSACTRL |
| 0x7022 | KFC_TEMP |
| 0x7023 | KFC_TAR_STEA_TIMEOUT |
| 0x7024 | KFC_TSA_BOUND |
| 0x7025 | nicht benutzt |
| 0x7026 | KFC_KL30_UNDERVOLTAGE |
| 0x7027 | KFC_KL30_OVERVOLTAGE |
| 0x7028 | KFC_KL15_UNDERVOLTAGE |
| 0x7029 | KFC_KL15_OVERVOLTAGE |
| 0x702a | KFC_SSW_MOSFET_OC |
| 0x702b | KFC_PCHARGE_OR_SSW_MOSFET_SC |
| 0x702c | KFC_PCHARGE_OC_OR_POWERSTAGE_SC |
| 0x702d | KFC_SAFETY_SWITCH_2_SC |
| 0x702e | KFC_SAFETY_SWITCH_1_SC |
| 0x702f | CODING_EVENT_SIGNATURE_ERROR |
| 0x7030 | CODING_EVENT_WRONG_VEHICLE |
| 0x7031 | CODING_EVENT_TRANSACTION_FAILED |
| 0x7032 | CODING_EVENT_INVALID_DATA |
| 0x7033 | KFC_VINCOMP |
| 0x7034 | KFC_MAXAKTDIFF |
| 0x7035 | KFC_DRIVER |
| 0x7036 | ELMCSI |
| 0x7037 | KFC_CODING_DATA_OUT_OF_BOUNDS_NEC |
| 0x7038 | KFC_CODING_DATA_OUT_OF_BOUNDS_S12X |
| 0x7039 | KFC_S12_AGB |
| 0x703a | KFC_IPC |
| 0x703b | KFC_S12_IPC |
| 0x703c | KFC_RAM |
| 0x703d | KFC_ROM |
| 0x703e | KFC_STM |
| 0x703f | KFC_S12_WATCHDOG |
| 0x7040 | KFC_FLASH |
| 0x7041 | KFC_S12_FLASH |
| 0x7042 | KFC_S12_FR_REC |
| 0x7043 | KFC_S12_FR_SEND |
| 0x7044 | KFC_FR_SEND |
| 0x7045 | KFC_OS_ERROR |
| 0x7046 | KFC_WDG_1MS |
| 0x7047 | KFC_WDG_INT |
| 0x7048 | KFC_D3PDH_ILS |
| 0x7049 | KFC_PHASE_UZK_SC |
| 0x704a | KFC_PHASE_GND_SC |
| 0x704b | KFC_LSSW_U_OC |
| 0x704c | KFC_LSSW_V_OC |
| 0x704d | KFC_LSSW_W_OC |
| 0x704e | KFC_HSSW_U_OC |
| 0x704f | KFC_HSSW_V_OC |
| 0x7050 | KFC_HSSW_W_OC |
| 0x7051 | KFC_PWM3PH_INIT |
| 0x7052 | KFC_ELMOSH_BS_UNDERVOLTAGE |
| 0x7053 | KFC_MOTOR_OC |
| 0x7054 | KFC_TOFF |
| 0x7055 | KFC_ANALOG_SIGNALS_NOT_VALID |
| 0x7056 | KFC_OFFSET_CALIB_FAILED |
| 0x7057 | KFC_ELMOSH_S_E_LINK |
| 0x7058 | KFC_ELMOSH_S_E_SPIBUF_OVL |
| 0x7059 | KFC_ELMOSH_S_E_TIMEOUT |
| 0x705a | KFC_ELMOSH_UNDERVOLTAGE |
| 0x705b | KFC_ELMOSH_OVERCURRENT |
| 0x705c | KFC_ELMOSH_FAULTPIN_LOW |
| 0x705d | KFC_5V0A_UNDERVOLTAGE |
| 0x705e | KFC_3V3A_2_UNDERVOLTAGE |
| 0x705f | KFC_VERS_SLS |
| 0x7060 | KFC_VERS_MLS |
| 0x7061 | KFC_MOTORPHASE_OC |
| 0x7062 | KFC_NOT_CONFIGURED_IN_TRESOS |
| 0x7063 | KFC_PT_CAN |
| 0x7064 | KFC_ICM_CAN |
| 0x7065 | KFC_SET_MLW_INVALID |
| 0x7066 | KFC_REQ_RESTART |
| 0x7067 | KFC_S12_SMCOM |
| 0x7068 | KFC_WR_MEM |
| 0x7069 | KFC_RD_MEM |
| 0x706a | KFC_SLOTFIND |
| 0x706b | KFC_SAS_FAILS |
| 0x706c | KFC_WAIT_FOR_RLW_SET |
| 0x706d | KFC_FR_KLEMMEN |
| 0x706e | KFC_TAR_STEA_MAXTIMEOUTS |
| 0x706f | KFC_EEPROM |
| 0x7070 | KFC_ELMOS_ON |
| 0x7071 | ZFLS_UNDERVOLTAGE |
| 0x7072 | KFC_VINTIMEOUT |
| 0x7073 | KFC_ZWK |
| 0x7074 | KFC_SSW_OFF |
| 0x7075 | KFC_ZFLS_INFO |
| 0x7076 | KFC_PPROT |
| 0x7077 | KFC_AGB_LIMIT |
| 0x7078 | KFC_MOTORDATEN |
| 0x7079 | KFC_SW_WARNING |
| 0x707a | KFC_INFO_ZWK_PL_UNDERVOLTAGE |
| 0x707b | KFC_INFO_ZWK_OVERVOLTAGE |
| 0x707c | KFC_INFO_ZWK_PL_OVERVOLTAGE |
| 0x707d | KFC_INFO_ZWK_LONG_PL |
| 0x707e | KFC_NO_SERVICE_ICM |
| 0x707f | KFC_NO_SERVICE_KL |
| 0x7080 | KFC_S12X_TSA_PLAUS |
| 0x7081 | KFC_PWR_OUT_INIT |
| 0x7082 | KFC_TSENSOR |
| 0x7083 | KFC_INFO_ZWK_UNDERVOLTAGE |
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
| default | InfoUmweltBMW | - | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 20 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Absolutzeit | ms | high | signed long | - | 1 | 1 | 0 |
| 0x02 | Fehlerart | -- | - | unsigned char | - | 1 | 1 | 0 |
| 0x03 | OS Status | -- | - | unsigned char | - | 1 | 1 | 0 |
| 0x04 | state Counter | -- | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | Z State | -- | - | unsigned char | - | 1 | 1 | 0 |
| 0x06 | Compensation Measure | -- | - | unsigned char | - | 1 | 1 | 0 |
| 0x07 | Soll-Lenkwinkel | Grad | high | signed int | - | 1 | 100 | 0 |
| 0x08 | Ist-Lenkwinkel | Grad | high | signed int | - | 1 | 100 | 0 |
| 0x09 | Spannung Klemme 15 | Volt | - | unsigned char | - | 128 | 1000 | 0 |
| 0x0A | Spannung Klemme 30 | Volt | - | unsigned char | - | 128 | 1000 | 0 |
| 0x0B | Spannung Zwischenkreis | Volt | - | unsigned char | - | 128 | 1000 | 0 |
| 0x0C | Temperatur | °C | - | signed char | - | 1 | 1 | 0 |
| 0x0D | Uptime | ms | high | signed long | - | 1 | 1 | 0 |
| 0x0E | Local Condition | Hex | high | signed long | - | 1 | 1 | 0 |
| 0x0F | Sperrenzustand | -- | - | unsigned char | - | 1 | 1 | 0 |
| 0x10 | Sollwertqualifier ICM | Hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x11 | Klemmenstatus | Hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x12 | Fehlercode | -- | - | unsigned char | - | 1 | 1 | 0 |
| 0x13 | Fehlerreihenfolge | -- | - | unsigned char | - | 1 | 1 | 0 |
| 0x14 | Anzahl MLW Verlust | -- | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-guerotor"></a>
### GUEROTOR

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht gueltig |
| 0x01 | gueltig |
| 0x02 | Initialisierung |
| 0x03 | defekt |
| 0xFF | unbekannter Status |

<a id="table-statusmaschinezustaende"></a>
### STATUSMASCHINEZUSTAENDE

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | POWER_OFF |
| 0x01 | INIT |
| 0x02 | READY_FOR_DRIVE |
| 0x03 | WAIT_FOR_RLW_SET |
| 0x04 | DRIVE_STANDBY |
| 0x05 | DRIVE_RAMP_ZERO |
| 0x06 | DRIVE_ACTIVEDIAG |
| 0x07 | DRIVE |
| 0x08 | ERROR |
| 0x09 | POST_RUN |
| 0x0A | RESET |
| 0xFF | unbekannter Status |

<a id="table-statuscanfehler"></a>
### STATUSCANFEHLER

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Botschaft i.O. |
| 0x02 | Botschaft wurde nie empfangen |
| 0x04 | Mehrere Botschaften pro Abtastzyklus |
| 0x08 | Timeout-Fehler |
| 0x10 | Fehlerwert laut Nachrichtenkatalog |
| 0x20 | Alive-Fehler |
| 0x40 | Checksummen-Fehler |
| 0x80 | mehrere Fehler |
| 0xFF | unbekannter Status |

<a id="table-fehlerumweltbmw"></a>
### FEHLERUMWELTBMW

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 |

<a id="table-infoumweltbmw"></a>
### INFOUMWELTBMW

Dimensions: 1 rows × 21 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR | UW17_NR | UW18_NR | UW19_NR | UW20_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B | 0x0C | 0x0D | 0x0E | 0x0F | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 |

<a id="table-spannungsueberwachung"></a>
### SPANNUNGSUEBERWACHUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Spannung OK |
| 0x01 | Unterspannung |
| 0x02 | Ueberspannung |

<a id="table-bootloaderzustaende"></a>
### BOOTLOADERZUSTAENDE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Bootloader original geflasht |
| 0x01 | Bootloader mit BLU geflasht |

<a id="table-engineeringzustaende"></a>
### ENGINEERINGZUSTAENDE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Applizieren moeglich |
| 0x01 | Applizieren moeglich |
