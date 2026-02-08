# mrbmse13.prg

- Jobs: [54](#jobs)
- Tables: [25](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Motorsteuerung BMS-E R13 |
| ORIGIN | BMW/ist EA-362 Michael_Ulbricht |
| REVISION | 1.500 |
| AUTHOR | ist_GmbH EA-362 Ulbricht |
| COMMENT | N/A |
| PACKAGE | 1.78 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
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
- [DME_DIAGNOSE_TESTJOB_DATA](#job-dme-diagnose-testjob-data) - KWP-Job für DME Diagnosetest Datenbyteeingabe im Data-Format
- [STATUS_MESSWERTE_BLOCK1](#job-status-messwerte-block1) - Auslesen der Stati des Messwerteblocks 1 KWP2000: $21 ReadDataByLocalIdentifier $10 Messwerteblock 1 lesen Modus  : Default
- [STATUS_MESSWERTE_BLOCK2](#job-status-messwerte-block2) - Auslesen der Stati des Messwerteblocks 2 KWP2000: $21 ReadDataByLocalIdentifier $11 Messwerteblock 2 lesen Modus  : Default
- [STATUS_SCHALTERINFO_BLOCK1](#job-status-schalterinfo-block1) - Auslesen der Stati des Schalterinfoblocks 1 KWP2000: $21 ReadDataByLocalIdentifier $20 Schalterinfoblock 1 lesen Modus  : Default
- [SG_STATUS_VORGEBEN](#job-sg-status-vorgeben) - Vorgeben von steuergeräteinternen Stati zum einzelnen Abschalten der Zündendstufen oder zur Abschaltung oder Störgrößenaufschaltung für Lambdaregler KWP2000: $3B WriteDataByLocalIdentifier $8x SG-interne Stati vorgeben Modus  : Default
- [ADAPTION_LESEN_SETZEN](#job-adaption-lesen-setzen) - Adaptionen lesen oder zurücksetzen Durch das gleichzeitige Setzen mehrerer Bits können auch mehrere Adaptionswerte gleichzeitig zurückgesetzt werden. Gelesen werden kann aber immer nur ein Adaptionswert. KWP2000: $30 InputOutputControlByLocalIdentifier $01 InputOutputLocalIdentifier $04 InputOutputControlParameter (resetToDefault) $09 InputOutputControlParameter (reportIOCalibrationParameters) Modus  : Default
- [IO_STATUS_VORGEBEN](#job-io-status-vorgeben) - Ein-/Ausgabestatus vorgeben zum testweisen Ansteuerung der Endstufen KWP2000: $30 InputOutputControlByLocalIdentifier $1x InputOutputLocalIdentifier $00 InputOutputControlParameter (returnControlToECU) $01 InputOutputControlParameter (reportCurrentState) $06 InputOutputControlParameter (executeControlOption) Modus  : Default
- [STATUS_FAHRGESTELLNUMMER](#job-status-fahrgestellnummer) - Fahrgestellnummer lesen KWP2000: $22 ReadDataByCommonIdentifier $10 $10 fullVehicleIdentificationNumber Modus  : Default
- [STEUERN_FAHRGESTELLNUMMER](#job-steuern-fahrgestellnummer) - Fahrgestellnummer schreiben KWP2000: $2E WriteDataByCommonIdentifier $10 $10 fullVehicleIdentificationNumber Modus  : Default
- [I_STUFE_LESEN](#job-i-stufe-lesen) - Dummy-Job, liefert Leerstrings KWP2000: keine Kommunikation Modus  : Default
- [I_STUFE_SCHREIBEN](#job-i-stufe-schreiben) - Dummy-Job, schreibt nichts ins SG KWP2000: keine Kommunikation Modus  : Default
- [IDENT_FUNKTIONAL](#job-ident-funktional) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [SERIENNUMMER_LESEN_FUNKTIONAL](#job-seriennummer-lesen-funktional) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [FLASH_PROGRAMMIER_STATUS_LESEN_FUNKTIONAL](#job-flash-programmier-status-lesen-funktional) - Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default
- [AIF_LESEN_FUNKTIONAL](#job-aif-lesen-funktional) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen KWP2000: $22 ReadDataByCommonIdentifier $10 $10 fullVehicleIdentificationNumber Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [C_FA_LESEN](#job-c-fa-lesen) - Dummy-Job Fahrzeugauftrag lesen damit wird immer der Standard FA mit Baureihe und Typnummer aus der Fahrgestellnummer ausgegeben KWP2000: $22 ReadDataByCommonIdentifier $10 $10 fullVehicleIdentificationNumber Modus  : Default
- [STEUERN_SNAPSHOT_LOESCHEN](#job-steuern-snapshot-loeschen) - Löschen aller gespeicherten Snapshot-Datensätze KWP2000: $30 InputOutputControlByLocalIdentifier $A0 InputOutputLocalIdentifier $04 InputOutputControlParameter (resetToDefault) Modus  : Default
- [STATUS_SNAPSHOT_LESEN](#job-status-snapshot-lesen) - Auslesen des über SNAPSHOT_NUMMER gewählten Snapshots KWP2000: $21 ReadDataByLocalIdentifier $Ax gewählten Snapshot lesen Modus  : Default

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

<a id="job-dme-diagnose-testjob-data"></a>
### DME_DIAGNOSE_TESTJOB_DATA

KWP-Job für DME Diagnosetest Datenbyteeingabe im Data-Format

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Datenbytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-messwerte-block1"></a>
### STATUS_MESSWERTE_BLOCK1

Auslesen der Stati des Messwerteblocks 1 KWP2000: $21 ReadDataByLocalIdentifier $10 Messwerteblock 1 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RPM10 | int | Motordrehzahl bis 2500 U/min |
| STAT_RPM10_EINH | string | U/min |
| STAT_RPM | int | Motordrehzahl ab 2500 U/min |
| STAT_RPM_EINH | string | U/min |
| STAT_T_MOT | real | Kuehlwasser-(Motor)temperatur |
| STAT_T_MOT_EINH | string | Grad C |
| STAT_T_MOT_ROH | real | Kuehlwasser-(Motor)temperatur |
| STAT_T_MOT_ROH_EINH | string | Grad C |
| STAT_T_ANS | real | Ansauglufttemperatur gefiltert |
| STAT_T_ANS_EINH | string | Grad C |
| STAT_T_ANS_ROH | real | Ansauglufttemperatur |
| STAT_T_ANS_ROH_EINH | string | Grad C |
| STAT_UBATT_ROH | real | Batteriespannung |
| STAT_UBATT_ROH_EINH | string | V |
| STAT_UBATT | real | Batteriespannung gefiltert |
| STAT_UBATT_EINH | string | V |
| STAT_DKW | real | realer Drosselklappenwinkel |
| STAT_DKW_EINH | string | Grad |
| STAT_DKP_ROH | real | Drosselklappenwert ohne Adapter |
| STAT_DKP_ROH_EINH | string | Grad |
| STAT_DKP_1 | real | aufbereiteter DK-Poti-Wert bis 30 Grad (10 Bit) |
| STAT_DKP_1_EINH | string | Grad |
| STAT_DKP_2 | real | aufbereiteter DK-Poti-Wert fuer Winkel &gt;30 Grad (10 Bit) |
| STAT_DKP_2_EINH | string | Grad |
| STAT_DKP_AD | real | adapt. Drosselklappen Nullwert |
| STAT_DKP_AD_EINH | string | Grad |
| STAT_TL | real | Lastsignal |
| STAT_TL_EINH | string | ms |
| STAT_FLR | real | Lambdaregelfaktor |
| STAT_FLR_ADA | real | adapt. Lambdaregelfaktor |
| STAT_US | real | Sondenspannung |
| STAT_US_EINH | string | mV |
| STAT_NSOLL | int | Solldrehzahl (Leerlauf) |
| STAT_NSOLL_EINH | string | U/min |
| STAT_LL_ADP | int | Leerlaufregler-Adaptionswert |
| STAT_LL_ADP_EINH | string | steps |
| STAT_POS | int | Position Steppermotor |
| STAT_POS_EINH | string | steps |
| STAT_PUMG | int | Umgebungsdruck |
| STAT_PUMG_EINH | string | hPa |
| STAT_SPEED | int | Geschwindigkeit |
| STAT_SPEED_EINH | string | km/h |
| STAT_TI | real | Einspritzzeit |
| STAT_TI_EINH | string | ms |
| STAT_ZW | real | Zuendwinkel |
| STAT_ZW_EINH | string | Grad KW |
| STAT_UEXT_2 | real | Externe 5V-Spannung fuer DKP |
| STAT_UEXT_2_EINH | string | Volt |
| STAT_DWELL | real | Schliesswinkel |
| STAT_DWELL_EINH | string | ms |
| STAT_FLRF | real | Gefilteter Lambdaregelfaktor |
| STAT_FNS | real | Nachstartfaktor |
| STAT_FWL | real | Faktor Warmlauf |
| STAT_GANG | int | berechneter aktueller Gang 0   -&gt; bei Fehler Geschwindigkeit 1-5 -&gt; Gang 6   -&gt; bei Geschwindigkeit Null |
| STAT_DN | real | Regelabweichung Leerlaufregler |
| STAT_DN_EINH | string | U/Min |
| STAT_TEZSP_AUS | real | Dauer Zwischenspritzer |
| STAT_TEZSP_AUS_EINH | string | ms |
| STAT_BA_CNT | real | Unbelegt |
| STAT_TPER | real | Periodendauer zwischen zwei Zahnflanken |
| STAT_TPER_EINH | string | ms |
| STAT_TVSLS | real | Unbelegt |
| STAT_TVTE | real | Tastverhaeltnis Tankentlueftung |
| STAT_U_KL50 | real | Unbelegt |
| STAT_U_KL50_EINH | string | V |
| STAT_U_KL50_ROH | real | Unbelegt |
| STAT_U_KL50_ROH_EINH | string | V |
| STAT_UZ | int | Umdrehungszaehler |
| STAT_WEE | real | Winkel Einspritzende |
| STAT_WEE_EINH | string | Grad KW vor OT |
| STAT_WLLR | real | Zuendwinkeleingriff Leerlaufregler |
| STAT_WLLR_EINH | string | Grad KW -128 .. +127 |
| STAT_WWL | real | Zuendwinkeleingriff Warmlauf |
| STAT_WWL_EINH | string | Grad KW 0 .. 255 |
| STAT_ZWDIFF | real | Zuendwinkeldifferenz |
| STAT_ZWDIFF_EINH | string | Grad KW -128 .. +127 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-messwerte-block2"></a>
### STATUS_MESSWERTE_BLOCK2

Auslesen der Stati des Messwerteblocks 2 KWP2000: $21 ReadDataByLocalIdentifier $11 Messwerteblock 2 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_D_TI_WF | real | Einspritzzeit Offset |
| STAT_D_TI_WF_EINH | string | ms |
| STAT_LL_D | int | D-Anteil Leerlaufregler |
| STAT_LL_D_EINH | string | steps |
| STAT_LL_I | real | I-Anteil Leerlaufregler |
| STAT_LL_I_EINH | string | steps |
| STAT_LL_P | int | P-Anteil Leerlaufregler |
| STAT_LL_P_EINH | string | steps |
| STAT_LL_REG | int | Regel-Anteil Leerlaufregler |
| STAT_LL_REG_EINH | string | steps |
| STAT_LL_DASH | int | Drehzahl-Dashpot |
| STAT_LL_DASH_EINH | string | U/min |
| STAT_LLBYADP | real | Faktor Lambdaadaption Luftmenge Leerlauf |
| STAT_LLR_INIT_CNT | int | Init-Zähler |
| STAT_LR_ADAPT_NUMBER | int | Anzahl Messwerte für Adaption |
| STAT_LR_ADAPT_RASTER | binary | Unbelegt |
| STAT_CHECK_SYS_STATE | unsigned char | Zustand Systemprüfung |
| STAT_LL_DKWINI | real | DK-Winkel bei Init |
| STAT_LL_DKWINI_EINH | string | Grad |
| STAT_SYNC_CNTINI | unsigned char | Sync Counter1 Initwert für Stepper Nachlauf |
| STAT_CNT_INITNL | unsigned char | Zähler Stepperini im Nachlauf wegen Startversuch während vorangegangener Stepperini |
| STAT_UZ | unsigned char | Umdrehungszaehler |
| STAT_POS_SOLL | unsigned char | korr. Pos |
| STAT_POS_SOLL_EINH | string | steps |
| STAT_STEP_INI | unsigned char | initiale Stepperposition am Ende des Aufstartens |
| STAT_STEP_INI_EINH | string | steps |
| STAT_STEP_NLPOS | unsigned char | finale Stepperposition am Ende des Nachlaufs |
| STAT_STEP_NLPOS_EINH | string | steps |
| STAT_STEP_POS | unsigned int | rückgemeldete Stepperposition Magneti-Marelli |
| STAT_STEP_POS_EINH | string | steps |
| STAT_STEP_ERR | unsigned char | Hardwarefehler Stepper |
| STAT_STEP_DIFFMAX | unsigned char | maximale Abweichung Stepperpositionen BMW - MM |
| STAT_STEP_DIFFMAX_EINH | string | steps |
| STAT_STEP_HALTMAX | int | maximale Wartezeit MM-Steppertreiber |
| STAT_STEP_HALTMAX_EINH | string | ms |
| STAT_STEP_UBMIN | real | minimale Batteriespannung bei Stepperansteuerung |
| STAT_STEP_UBMIN_EINH | string | Volt |
| STAT_STEP_CNT_HALT_MAX | unsigned char | Zähler, wie oft die BMW-Stepperposition nach maximaler Wartezeit von der MM-Stepperposition abweicht |
| STAT_STEP_CNT_POS_DIFF | unsigned char | Zähler, wie oft die BMW-Stepperposition um mehr als zwei Schritte von der MM-Stepperposition abweicht |
| STAT_STEP_CNT_NL_KL15_KL50 | unsigned char | Zähler für Klemme 50 gedrückt, während Nachlauf noch aktiv aber Klemme 15 bereits wieder an ist |
| STAT_STEP_CNT_NL_UBLOW | unsigned char | Zähler für Unterspannung im Nachlauf |
| STAT_SAL_SYS_MON_RESET_ID | unsigned int | Monitoring MM-Schnittstelle System, letzte Reset-ID |
| STAT_SAL_SYS_MON_RESET_CNT | unsigned int | Monitoring MM-Schnittstelle System, Aufrufzähler |
| STAT_SAL_STP_MON_STATE | unsigned char | Monitoring MM-Schnittstelle Stepperansteuerung, Zustand Treiberbaustein / Softwaretreiber |
| STAT_SAL_STP_MON_DIAG | unsigned char | Monitoring MM-Schnittstelle Stepperansteuerung, Treiberdiagnose |
| STAT_SAL_STP_MON_GET_ERR | unsigned char | Zähler, wie oft die MM-Get-Funktion für den Stepper einen Fehler zurückgemeldet hat |
| STAT_SAL_STP_MON_PUT_ERR | unsigned char | Zähler, wie oft die MM-Put-Funktion für den Stepper einen Fehler zurückgemeldet hat |
| STAT_SAL_STP_MON_CONFIG_ERR | unsigned char | Zähler, wie oft die MM-Config-Funktion für den Stepper einen Fehler zurückgemeldet hat |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-schalterinfo-block1"></a>
### STATUS_SCHALTERINFO_BLOCK1

Auslesen der Stati des Schalterinfoblocks 1 KWP2000: $21 ReadDataByLocalIdentifier $20 Schalterinfoblock 1 lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IO_STATUS | string | Status über Ansteuerung verschiedener Treiber durch Diagnose 0x01   Option Sekundärluftventil entfallen EV_MSK    0x02   Einspritzventil angesteuert TEV_MSK   0x04   Tankentlüftungsventil angesteuert EKP_MSK   0x08   Elektr. Kraftst.-Pumpe angesteuert FAN_MSK   0x10   Elektro-Lüfter angesteuert LLR_MSK   0x20   Leerlaufregler aktiv LSH_MSK   0x40   Lambdasondenheizung angesteuert UTL_MSK   0x80   Übertemperaturlampe |
| STAT_IO_MASTER | string | Besitzerstatus für Ansteuerung verschiedener Treiber 0x01   Option Sekundärluftventil entfallen EV_MSK    0x02   Einspritzventil von Diagnose angesteuert TEV_MSK   0x04   TEV von Diagnose angesteuert EKP_MSK   0x08   EKP von Diagnose angesteuert FAN_MSK   0x10   E-Lüfter von Diagnose angesteuert LLR_MSK   0x20   LLR von Diagnose gesteuert LSH_MSK   0x40   LSH von Diagnose angesteuert UTL_MSK   0x80   UTL von Diagnose angesteuert |
| STAT_ST_DKPAD | string | Status Dkp-Adaption == 0x00   Werksinitialisierung läuft korrekt B_DELTA_DKP_AD   0x01   Dkp_ad hat innerhalb vorgebener Adaptionszeit maximal zulässige Abweichung überschritten B_BEREICH_DKP_AD 0x02   Plausibilitätsfehler: Wert liegt außerhalb der Toleranz B_RPM_DKP_AD     0x04   Drehzahl erkannt (unzulässig) |
| STAT_ST_GLOBAL | string | Unbelegt |
| STAT_ST_LA_AUS | string | Status für Lambdaregelung AUS B_LA_AUS_SA_RPMMAX  0x01   Schubabschaltung oder Nmax-Begr. 0x02   unbelegt B_LA_AUS_TLMAX      0x04   Lastschwelle Tlmax überschritten B_LA_AUS_START_VMAX 0x08   Start, Nachstart oder B_VMAX B_LA_AUS_WE         0x10   Wiedereinsetzfaktor &gt;1,0 B_LA_AUS_VL_TI      0x20   Vollast und n &gt; K_LA_N_VL oder Ti &lt; K_LA_TI_MIN B_LA_AUS_ACU        0x40   Akustikfunktion 0x80   unbelegt |
| STAT_ST_LA_EIN | string | Status für Lambdaregelung EIN B_LR              0x01   Lambdaregler aktiv B_LA_EIN_NOERROR  0x02   kein Sondenfehler erkannt B_LA_EIN_TMOT     0x04   Motortemperaturbedingung erfüllt B_LA_EIN_FREIGABE 0x08   Reglerfreigabe (KWP2000) 0x10   keine Bedeutung 0x20   keine Bedeutung B_LA_EIN_BEREIT   0x40   Lambdasonde ein (=bereit) 0x80   keine Bedeutung |
| STAT_ST_LA_DIAG | string | Status fuer Diagnose Lambdaregelung B_LA_DIAG_2S     0x01   Lambdaadaption gesperrt 0x02   unbelegt 0x04   unbelegt 0x08   unbelegt B_LA_DIAG_MX_FR  0x10   Regelanschlag fett B_LA_DIAG_MN_FR  0x20   Regelanschlag mager B_LA_DIAG_MINMAX 0x40   Lambda-Soll außerhalb gültigem Bereich 0x80   unbelegt |
| STAT_ST_LRA | string | Status Lambdaregeladaption B_LRA    0x01   Teillastadaption aktiv / nicht aktiv B_LRA_LL 0x02   Leerlaufadaption aktiv / nicht aktiv B_LRA_EB 0x04   Einschaltbedingungen Lambdaadaption gegeben |
| STAT_ST_LSH | string | Status Lambda-Sondenheizung B_LSHWT     0x01   Sondensperrzeit abgelaufen B_LSH_AKTIV 0x02   Heizung funktional angesteuert B_LSH_AUTO  0x04   Ansteuerung erfolgt automatisch B_LSH_TEST  0x08   Testansteuerung durch Eigendiagnose aktiv |
| STAT_ST_LLR | string | Status Leerlaufregler B_I_ERLAUBT      0x01  I-Anteil erlaubt B_STOP_LLR       0x02  LLR gestoppt B_DASH_AR        0x04  Dashpot B_FIRST_START    0x08  Erster Start B_NOTINI_NOTKL50 0x10  keine Stepper Initialisierung im Aufstarten, Startschalter nicht betätigt B_NOTINI_KL50    0x20  keine Stepper Initialisierung im Aufstarten, Startschalter betätigt B_INI_NOTKL50    0x40  Stepper Initialisierung im Nachlauf, Startschalter nicht betätigt B_INI_KL50       0x80  Stepper Initialisierung im Nachlauf, Startschalter betätigt |
| STAT_ST_STEP | string | Status Stepperansteuerung B_STEP_FORW  0x01   Stepper fährt vorwärts B_STEP_BACK  0x02   Stepper fährt rückwärts B_STEP_ADAPT 0x04   Stepper lernt Anschlag B_STEP_PAUSE 0x08   Warteschritt nach Erreichen der Zielposition |
| STAT_ST_SA | string | Status Schubabschaltung B_SA      0x01   Schubabschaltung aktiv B_WE      0x02   Wiedereinsetzen 0x04   unbelegt 0x08   unbelegt B_WEH     0x10   hartes Wiedereinsetzen 0x20   unbelegt B_NTIOFF  0x40   Bedingung Abschalten Einspritzung B_WFSA    0x80   Sperrung SA aufgrund nicht abgebautem Wandfilm |
| STAT_ST_TI | string | Status Abschaltung der Einspritzung B_SAOFF     0x01   Schubabschaltung B_NBEGR     0x02   Motordrehzahlbegrenzung B_VMXH      0x04   harte VMAX-Begrenzung B_STPROT    0x08   Anlasserschutzfunktion aktiv B_TI_UBST   0x10   Ubatt &lt; Ustart für K_CNT_USTART Umdrehungen B_TI_IOCTRL 0x20   Testeransteuerung B_INJKL50   0x40   KL50 - Überwachung B_INJKL15   0x80   KL15 - Erkennung |
| STAT_DKLAST | string | Status Lastzustand B_LEERLAUF 0x01  Leerlauf B_TEILLAST 0x02  Teillast B_VOLLAST  0x04  Vollast |
| STAT_ST_WARMLF | string | Status Warmlaufphase B_ESPR    0x01   Einspritzkorrektur WL aktiv, nicht LL B_ZDG     0x02   Zündwinkel-Korrektur WL aktiv, nicht LL B_CTE     0x04   C-t-Phase Einspritzung abgelaufen B_ESPRLL  0x08   Einspritzkorrektur WL aktiv im LL B_CTZ     0x10   C-t-Phase Zündung abgelaufen B_WLW     0x20   Zündwinkel-Korrektur Last,kein C-T B_ZDGLL   0x40   Zündwinkel-Korrektur WL aktiv im LL B_WLEND   0x80   Flag für Ende des Warmlaufs |
| STAT_ST_NST | string | Unbelegt |
| STAT_ST_LBF | string | Status Ladebilanzfunktion B_LBF_A   0x01   LBF aktiv/nicht aktiv B_LBF_T   0x02   Totzeit zwischen zwei aktiven Phasen |
| STAT_FEHLER_ANZAHL | int | Anzahl momentan gespeicherter Fehler |
| STAT_SYSFLG | string | Unbelegt |
| STAT_SYSFLG1 | string | Unbelegt |
| STAT_MERKBIT | string | Merkbit Stepperinitialisierung STEPNACHL 0x01   Bedingung Nachlauf abgeschlossen STEPINIT  0x02   Bedingung vollständiger Nachlauf DKINIT    0x04   Bedingung unvollständiger Nachlauf bei geöffneter Drosselklappe UZNL      0x08   Bedingung Nachlauf wegen Umdrehungszähler SYNCNL    0x10   Bedingung Nachlauf wegen Syncverlust LLINL     0x20   Bedingung Nachlauf unplausibler I-Anteil Leerlaufregler APINIT    0x40   Bedingung provozierter Nachlauf über Drosselklappe |
| STAT_ST_BA | string | Unbelegt |
| STAT_ST_IGN | string | Status Zündungsunterbrechung B_IGNNOZSP1 0x40   Zündungsunterdrückung Zündkerze 1 über Diagnose B_IGNNOZSP2 0x80   Zündungsunterdrückung Zündkerze 2 über Diagnose |
| STAT_ST_INJ | string | Status Einspritzung B_REGINJSET    0x0001  Ausgabe reguläre Einspritzung aufgesetzt B_REGINJACT    0x0002  Ausgabe reguläre Einspritzung läuft B_REGINJEND    0x0004  Ausgabe reguläre Einspritzung beendet B_REGINJWAIT   0x0008  Ausgabe reguläre Einspritzung wartend B_REGINJFORCE  0x0010  Ausgabe reguläre Einspritzung erzwungen B_ADDINJSET    0x0020  Ausgabe zusätzliche Einspritzung aufgesetzt B_ADDINJACT    0x0040  Ausgabe zusätzliche Einspritzung läuft B_ADDINJEND    0x0080  Ausgabe zusätzliche Einspritzung beendet B_ADDINJWAIT   0x0100  Ausgabe zusätzliche Einspritzung wartend B_ADDINJFORCE  0x0200  Ausgabe zusätzliche Einspritzung erzwungen B_REGINJLONG   0x0400  Lange reguläre Einspritzung, deren Ende nach Zahn 3 liegt B_ADDINJLONG   0x0800  Lange zusätzliche Einspritzung, deren Ende nach Zahn 3 liegt B_REGINJOFFSET 0x1000  Anzugskorrektur in letzter regulärer Einspritzung berücksichtigt B_ADDINJOFFSET 0x2000  Anzugskorrektur in letzter zusätzlicher Einspritzung berücksichtigt B_INJOFF       0x4000  Ansteuerung Einspritzventil unterdrückt B_INJERR       0x8000  Unentprellter Fehler Einspritzventil vorhanden |
| STAT_ST_START | string | Status Start B_START  0x01   Start aktiv B_NST    0x02   Nachstart aktiv (Fns &gt; 1.0)) B_TMOTAB 0x04   Abstelltemperatur speichern |
| STAT_ST_TE | string | Status Tankentlüftung B_TE_AKTIV 0x01   Tankentlüftung aktiv / nicht aktiv SA_TE      0x02   Zustand Schubabschalten während TE LA-TE      0x04   Zustand Lambdaregler + Ventil auf LA_LIM     0x08   Zustand Lambdaregler + Ventil zu WL_TE      0x10   Zustand Tl &gt; Tlten + Ventil auf NO_TE      0x20   Zustand Tl &lt; Tlten + Ventil zu TIME_TE    0x40   Zustand Spülzeit abgelaufen, vergessen GA_LA      0x80   Grundadaption Lambda, keine TE |
| STAT_ST_UEK | string | Status Übergangskompensation B_UEK_AKTIV        0x01  Zeigt an, ob die Übergangskompensation aktiv ist. B_UEK_POSITIV      0x02  Zeigt an, ob die Korrektur zur Einspritzzeit Ti positiv ist. B_UEK_NEGATIV      0x04  Zeigt an, ob die Korrektur zur Einspritzzeit Ti negativ ist. B_UEK_BEREITSCHAFT 0x08  Zeigt an, ob die Übergangskompensation in Bereitschaft ist. |
| STAT_ST_UET | string | Status Übertemperatur B_UET_AKTIV     0x01   Lampe an B_UET_AUTO      0x02   Automatikmodus aktiv B_UET_STP_AKTIV 0x04   Blinkmodus durch Stepper an |
| STAT_CNT_DKP_NL | int | Zaehler Nachlauf Drosselklappe |
| STAT_CNT_LLI_NL | int | Zaehler Nachlauf Ll_i |
| STAT_CNT_STP_INI_NL | unsigned int | Zaehler Stepper Initialisierung Nachlauf |
| STAT_CNT_SYNC_NL | int | Zaehler Nachlauf Synchronisation |
| STAT_CNT_UZ_NL | int | Zaehler Nachlauf Umdrehungszaehler |
| STAT_BTR_H | unsigned int | Zaehler Betriebsstunden |
| STAT_BTR_M | int | Zaehler Betriebsminuten |
| STAT_BTR_S | int | Zaehler Betriebssekunden |
| STAT_SYNC_CNT | int | Zaehler fuer Neusynchronisierung |
| STAT_SYNC_CNT1 | int | Zaehler 131 ms Sync-Timeout |
| STAT_UDZ_CNT | int | Unterdrehzahl-Zaehler |
| STAT_UDZ_CNT1 | int | Unbelegt |
| STAT_ST_LA_SENS | string | Status Lambdasonde B_LA_DIAG_UNTBR     0x01   Sonde - Unterbrechung B_LA_DIAG_KSP       0x02   Sonde - Kurzschluß gegen Batterie B_LA_DIAG_KSM       0x04   Sonde - Kurzschluß gegen Masse B_LA_DIAG_THEO_SOBE 0x08   theoretische Sondenbereitschaft |
| STAT_ST_RPM | string | Status Drehzahlerfassung B_RPMHI 0x01   Drehzahl basiert auf halber Umdrehung B_ML    0x02   Motor läuft B_FPER  0x04   erste Periodendauer vorhanden B_PSE   0x08   positive Flanke erkannt B_720   0x10   Phasensynchronisation erfolgt B_ZOT   0x20   Zünd-OT einmal durchlaufen |
| STAT_ST_KL15 | string | Status Klemme 15 B_KL15     0x01   Klemme 15 (Zündschloss) entprellt ein B_KL15_ROH 0x02   Klemme 15 (Zündschloss) unentprellt ein |
| STAT_ST_KL50 | string | Status Klemme 50 B_KL15_ROH 0x10   Klemme 50 (Starttaster) unentprellt ein B_KL15     0x20   Klemme 50 (Starttaster) entprellt ein |
| STAT_ST_EKP | string | Status Kraftstoffpumpe B_EKPOV     0x01   Pumpenvorlauf abgeschlossen B_EKP_AKTIV 0x02   Kraftstoffpumpe momentan ein B_EKP_AUTO  0x04   Kraftstoffpumpe automatisch angesteuert |
| STAT_ST_ELUE | string | Status Lüfter B_ELUE_AKTIV 0x01   Lüfter momentan ein B_ELUE_AUTO  0x02   Lüfter automatisch angesteuert |
| STAT_ST_PROT | string | Status Bauteileschutz B_KL15_START 0x01   Start über Anlasser B_VMXW       0x04   weiche Geschwindigkeitsbegrenzung |
| STAT_ST_ZW | string | Status Zündungsunterdrückung B_IGNKL50 0x01   Zündabschaltung wegen losgelassenem Starttaster B_IGNUBST 0x02   Zündabschaltung wegen Unterspannung im Start B_IGNTPST 0x04   Zündabschaltung wegen Unterdrehzahl im Start B_IGNPROT 0x08   Zündabschaltung wegen Anlasserschutz |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-sg-status-vorgeben"></a>
### SG_STATUS_VORGEBEN

Vorgeben von steuergeräteinternen Stati zum einzelnen Abschalten der Zündendstufen oder zur Abschaltung oder Störgrößenaufschaltung für Lambdaregler KWP2000: $3B WriteDataByLocalIdentifier $8x SG-interne Stati vorgeben Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RECORD_LOCAL_IDENTIFIER | unsigned char | Auswahl des Status 0x80 =&gt; Störgrößenaufschaltung für Lambdaregler 0x81 =&gt; Sperrung des Lambdareglers 0x82 =&gt; Abschaltung einzelner Zündendstufen |
| SG_STATUS | unsigned char | Wert des Status RECORD_LOCAL_IDENTIFIER = 0x80: Grundanpassungsfaktor für Einspritzzeit Ti (Umrechung x/128) RECORD_LOCAL_IDENTIFIER = 0x81: 0 =&gt; Lambdaregler gesperrt 1 =&gt; Lambdaregler freigegeben (Normalzustand) RECORD_LOCAL_IDENTIFIER = 0x82: 0x00 =&gt; Beide Zündendstufen eingeschaltet (Normalzustand) 0x40 =&gt; Zündendstufe 1 abgeschaltet 0x80 =&gt; Zündendstufe 2 abgeschaltet 0xC0 =&gt; Beide Zündendstufen abgeschaltet (wenig sinnvoll) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-adaption-lesen-setzen"></a>
### ADAPTION_LESEN_SETZEN

Adaptionen lesen oder zurücksetzen Durch das gleichzeitige Setzen mehrerer Bits können auch mehrere Adaptionswerte gleichzeitig zurückgesetzt werden. Gelesen werden kann aber immer nur ein Adaptionswert. KWP2000: $30 InputOutputControlByLocalIdentifier $01 InputOutputLocalIdentifier $04 InputOutputControlParameter (resetToDefault) $09 InputOutputControlParameter (reportIOCalibrationParameters) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IOCP_ADAPTION | unsigned char | Auswahlbyte Aktion 0x04 =&gt; Adaptionen selektiv löschen 0x09 =&gt; Adaptionen selektiv lesen |
| CS1_ADAPTION | unsigned char | Adaption Auswahlbyte 1 Bit 0 =&gt; Normale Drosselklappenadaption Bit 1 =&gt; Lambdaadaption für Teil- und Volllast Bit 2 =&gt; Leerlaufregleradaption Bit 3 =&gt; Leerlaufstellernullabgleich Bit 4 =&gt; Lambdaadaption für Leerlauf Bit 5 =&gt; Nicht benutzt Bit 6 =&gt; Nicht benutzt Bit 7 =&gt; Nicht benutzt |
| CS2_ADAPTION | unsigned char | Adaption Auswahlbyte 2 Bit 0 =&gt; Schnelle Drosselklappenadaption Bit 1 =&gt; Nicht benutzt Bit 2 =&gt; Nicht benutzt Bit 3 =&gt; Nicht benutzt Bit 4 =&gt; Nicht benutzt Bit 5 =&gt; Nicht benutzt Bit 6 =&gt; Nicht benutzt Bit 7 =&gt; Nicht benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| R_CS1_IO_STATUS | unsigned char | Adaption Ergebnisbyte 1 CS1_ADAPTION = 0x01: Dkp_ad (Highbyte) CS1_ADAPTION = 0x02: Adresse Kfada (Highbyte) CS1_ADAPTION = 0x04: Adresse Kl_Llr_adp (Highbyte) CS1_ADAPTION = 0x08: St_init_kwp (1=OK, 2=Timeout, 4=Fehler LLR) CS1_ADAPTION = 0x10: Llbyadp (Highbyte) CS2_ADAPTION = 0x01: Dkp_ad_ini (Highbyte) sonst: gleich CS1_ADAPTION |
| R_CS2_IO_STATUS | unsigned char | Adaption Ergebnisbyte 2 CS1_ADAPTION = 0x01: Dkp_ad (Lowbyte) CS1_ADAPTION = 0x02: Adresse Kfada (Midbyte) CS1_ADAPTION = 0x04: Adresse Kl_Llr_adp (Midbyte) CS1_ADAPTION = 0x08: Unbenutzt CS1_ADAPTION = 0x10: Llbyadp (Lowbyte) CS2_ADAPTION = 0x01: Dkp_ad_ini (Lowbyte) sonst: gleich CS1_ADAPTION |
| R_CS3_IO_STATUS | unsigned char | Adaption Ergebnisbyte 3 CS1_ADAPTION = 0x01: Unbenutzt CS1_ADAPTION = 0x02: Adresse Kfada (Lowbyte) CS1_ADAPTION = 0x04: Adresse Kl_Llr_adp (Lowbyte) CS1_ADAPTION = 0x08: Unbenutzt CS1_ADAPTION = 0x10: Unbenutzt CS2_ADAPTION = 0x01: St_dkp_ad (0x01=Max. Abweichung überschritten, 0x02=Wert außerhalb Toleranzgrenzen, 0x04=Drehzahl erkannt) sonst: gleich CS1_ADAPTION |
| R_CS4_IO_STATUS | unsigned char | Adaption Ergebnisbyte 4 CS1_ADAPTION = 0x01: Unbenutzt CS1_ADAPTION = 0x02: Kfada (Size) CS1_ADAPTION = 0x04: Kl_Llr_adp (Size) CS1_ADAPTION = 0x08: Unbenutzt CS1_ADAPTION = 0x10: Unbenutzt CS2_ADAPTION = 0x01: Unbenutzt sonst: gleich CS1_ADAPTION |
| R_CS5_IO_STATUS | binary | Adaption Ergebnisarray 5 CS1_ADAPTION = 0x01: Unbenutzt CS1_ADAPTION = 0x02: Inhalt Kfada CS1_ADAPTION = 0x04: Inhalt Kl_Llr_adp CS1_ADAPTION = 0x08: Unbenutzt CS1_ADAPTION = 0x10: Unbenutzt CS2_ADAPTION = 0x01: Unbenutzt sonst: gleich CS1_ADAPTION |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-io-status-vorgeben"></a>
### IO_STATUS_VORGEBEN

Ein-/Ausgabestatus vorgeben zum testweisen Ansteuerung der Endstufen KWP2000: $30 InputOutputControlByLocalIdentifier $1x InputOutputLocalIdentifier $00 InputOutputControlParameter (returnControlToECU) $01 InputOutputControlParameter (reportCurrentState) $06 InputOutputControlParameter (executeControlOption) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IDENTIFIER_IO_STATUS | unsigned char | Auswahlbyte Endstufe 0x10 =&gt; Elektrolüfter 0x11 =&gt; Elektrische Kraftstoffpumpe 0x12 =&gt; Einspritzventil 0x13 =&gt; Tankentlüftungsventil (falls verbaut) 0x14 =&gt; Übertemperaturanzeige 0x15 =&gt; Leerlaufsteller 0x16 =&gt; Lambdasondenheizung |
| IOCP_IO_STATUS | unsigned char | Auswahlbyte Aktion 0x00 =&gt; Ansteuerung durch Fahrprogramm wieder freigeben (Normalbetrieb) 0x01 =&gt; Ansteuerungszustand durch Diagnose lesen 0x06 =&gt; Ansteuerungszustand durch Diagnose setzen |
| CS1_IO_STATUS | unsigned char | Auswahlbyte 1 zum Setzen eines Zustands IDENTIFIER_IO_STATUS = 0x10: 0x00 =&gt; ELUE aus 0xFF =&gt; ELUE ein IDENTIFIER_IO_STATUS = 0x11: 0x00 =&gt; EKP aus 0xFF =&gt; EKP ein IDENTIFIER_IO_STATUS = 0x12: Ansteuerungsdauer EV mit 100 ms Periode und 1 % Tastverhältnis als Vielfaches von 39,2 ms (0x01 =&gt; 39,2 ms, 0xff =&gt; 10s) IDENTIFIER_IO_STATUS = 0x13: CS2_IO_STATUS = 0x00: Ansteuerungsdauer TEV mit 160 ms Periode und 50 % Tastverhältnis als Vielfaches von 39,2 ms (minimal 100 ms, maximal 10s) CS2_IO_STATUS = 0x01: 0x00 =&gt; TEV-Funktion ausschalten 0x01 =&gt; TEV-Funktion einschalten IDENTIFIER_IO_STATUS = 0x14: 0x00 =&gt; UET aus 0xFF =&gt; UET ein IDENTIFIER_IO_STATUS = 0x15: Anzahl Schritte, um die LLS verfahren werden soll. IDENTIFIER_IO_STATUS = 0x16: 0x00 =&gt; LSH aus 0xFF =&gt; LSH ein |
| CS2_IO_STATUS | unsigned char | Auswahlbyte 2 zum Setzen eines Zustands IDENTIFIER_IO_STATUS = 0x10: Wird nicht ausgewertet IDENTIFIER_IO_STATUS = 0x11: Wird nicht ausgewertet IDENTIFIER_IO_STATUS = 0x12: Wird nicht ausgewertet IDENTIFIER_IO_STATUS = 0x13: 0x00 =&gt; TEV ansteuern 0x01 =&gt; TEV-Funktion ein-/ausschalten IDENTIFIER_IO_STATUS = 0x14: Wird nicht ausgewertet IDENTIFIER_IO_STATUS = 0x15: 0x00 =&gt; LLS verfahren in Richtung auf 0xFF =&gt; LLS verfahren in Richtung zu IDENTIFIER_IO_STATUS = 0x16: Wird nicht ausgewertet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| R_CS1_IO_STATUS | unsigned char | Auswahlbyte 1 beim Abfragen eines Zustands Format wie Auswahlbyte 1 zum Setzen eines Zustands |
| R_CS2_IO_STATUS | unsigned char | Auswahlbyte 2 beim Abfragen eines Zustands Format wie Auswahlbyte 2 zum Setzen eines Zustands |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-fahrgestellnummer"></a>
### STATUS_FAHRGESTELLNUMMER

Fahrgestellnummer lesen KWP2000: $22 ReadDataByCommonIdentifier $10 $10 fullVehicleIdentificationNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| STAT_FGNUMMER | string | Fahrgestellnummer 17-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-fahrgestellnummer"></a>
### STEUERN_FAHRGESTELLNUMMER

Fahrgestellnummer schreiben KWP2000: $2E WriteDataByCommonIdentifier $10 $10 fullVehicleIdentificationNumber Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (17-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-i-stufe-lesen"></a>
### I_STUFE_LESEN

Dummy-Job, liefert Leerstrings KWP2000: keine Kommunikation Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_STUFE_WERK | string | Entspricht Byte 1 des Pruefstempels |
| I_STUFE_HO | string | Entspricht Byte 2 des Pruefstempels |
| I_STUFE_HO_BACKUP | string | Entspricht Byte 3 des Pruefstempels |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-i-stufe-schreiben"></a>
### I_STUFE_SCHREIBEN

Dummy-Job, schreibt nichts ins SG KWP2000: keine Kommunikation Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_STUFE_WERK | string | Entspricht Byte 1 des Pruefstempels |
| I_STUFE_HO | string | Entspricht Byte 2 des Pruefstempels |
| I_STUFE_HO_BACKUP | string | Entspricht Byte 3 des Pruefstempels |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-ident-funktional"></a>
### IDENT_FUNKTIONAL

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

<a id="job-seriennummer-lesen-funktional"></a>
### SERIENNUMMER_LESEN_FUNKTIONAL

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

<a id="job-flash-programmier-status-lesen-funktional"></a>
### FLASH_PROGRAMMIER_STATUS_LESEN_FUNKTIONAL

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

<a id="job-aif-lesen-funktional"></a>
### AIF_LESEN_FUNKTIONAL

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

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen KWP2000: $22 ReadDataByCommonIdentifier $10 $10 fullVehicleIdentificationNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| STAT_FGNUMMER | string | Fahrgestellnummer 17-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

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

<a id="job-c-fa-lesen"></a>
### C_FA_LESEN

Dummy-Job Fahrzeugauftrag lesen damit wird immer der Standard FA mit Baureihe und Typnummer aus der Fahrgestellnummer ausgegeben KWP2000: $22 ReadDataByCommonIdentifier $10 $10 fullVehicleIdentificationNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | Dummy-Standard-FA "???_#0808*????%0N27&0000-ISTA-BMSE" in codierter Form |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-snapshot-loeschen"></a>
### STEUERN_SNAPSHOT_LOESCHEN

Löschen aller gespeicherten Snapshot-Datensätze KWP2000: $30 InputOutputControlByLocalIdentifier $A0 InputOutputLocalIdentifier $04 InputOutputControlParameter (resetToDefault) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| IOCP_SNAPSHOT | unsigned char | Auswahlbyte Aktion 0x04 =&gt; Snapshot-Datensätze löschen |
| CS1_SNAPSHOT | unsigned char | Auswahlbyte 1 =&gt; Nicht benutzt |
| CS2_SNAPSHOT | unsigned char | Auswahlbyte 2 =&gt; Nicht benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-snapshot-lesen"></a>
### STATUS_SNAPSHOT_LESEN

Auslesen des über SNAPSHOT_NUMMER gewählten Snapshots KWP2000: $21 ReadDataByLocalIdentifier $Ax gewählten Snapshot lesen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SNAPSHOT_NUMMER | unsigned char | Auswahlbyte Snapshot |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SNAPSHOT_DATEN | binary | Rohdatenblock des Snapshots |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (141 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (18 × 2)
- [FARTTYP](#table-farttyp) (3 × 5)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (20 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (20 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (20 × 9)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (3 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (3 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (20 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (3 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [TYPSCHLUESSEL](#table-typschluessel) (28 × 3)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)

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

Dimensions: 141 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
| 0x02 | Leopold Kostal GmbH & Co. KG |
| 0x03 | Hella Fahrzeugkomponenten GmbH |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako GmbH |
| 0x08 | Robert Bosch GmbH |
| 0x09 | Lear Corporation |
| 0x10 | VDO |
| 0x11 | Valeo GmbH |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine Electronics GmbH |
| 0x18 | Continental Teves AG & Co. OHG |
| 0x19 | Elektromatik Südafrika |
| 0x20 | Harman Becker Automotive Systems |
| 0x21 | Preh GmbH |
| 0x22 | Alps Electric Co. Ltd. |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto SE |
| 0x26 | MotoMeter |
| 0x27 | Delphi Automotive PLC |
| 0x28 | DODUCO (Beru) |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer Corporation |
| 0x33 | Jatco |
| 0x34 | FUBA Automotive GmbH & Co. KG |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0x38 | Sachs |
| 0x39 | ITT |
| 0x40 | FTE (Fahrzeugtechnik Ebern) |
| 0x41 | Megamos |
| 0x42 | TRW Automotive GmbH |
| 0x43 | WABCO Fahrzeugsysteme GmbH |
| 0x44 | ISAD Electronic Systems |
| 0x45 | HEC Hella Electronics Corporation |
| 0x46 | Gemel |
| 0x47 | ZF Friedrichshafen AG |
| 0x48 | GMPT |
| 0x49 | Harman Becker Automotive Systems GmbH |
| 0x50 | Remes GmbH |
| 0x51 | ZF Lenksysteme GmbH |
| 0x52 | Magneti Marelli S.p.A. |
| 0x53 | Johnson Controls Inc. |
| 0x54 | GETRAG Getriebe- und Zahnradf. Hermann Hagenmeyer GmbH & Co. KG |
| 0x55 | Behr-Hella Thermocontrol GmbH |
| 0x56 | Siemens VDO Automotive |
| 0x57 | Visteon Innovation & Technology GmbH |
| 0x58 | Autoliv AB |
| 0x59 | Haberl Electronic GmbH & Co. KG |
| 0x60 | Magna International Inc. |
| 0x61 | Marquardt GmbH |
| 0x62 | AB Elektronik GmbH |
| 0x63 | SDVO/BORG |
| 0x64 | Hirschmann Car Communication GmbH |
| 0x65 | hoerbiger-electronics |
| 0x66 | Thyssen Krupp Automotive |
| 0x67 | Gentex Corporation |
| 0x68 | Atena GmbH |
| 0x69 | Magna-Donelly |
| 0x70 | Koyo Steeting Europe |
| 0x71 | NSI Beheer B.V. |
| 0x72 | Aisin AW Co. Ltd. |
| 0x73 | Schorlock |
| 0x74 | Schrader Electronics Ltd. |
| 0x75 | Huf-Electronics Bretten GmbH |
| 0x76 | CEL |
| 0x77 | AUDIO MOBIL Elektronik GmbH |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia-Automotive GmbH |
| 0x81 | Tyco Electronics |
| 0x82 | Paragon AG |
| 0x83 | IEE S.A. |
| 0x84 | TEMIC AUTOMOTIVE of NA |
| 0x85 | Sonceboz S.A. |
| 0x86 | Meta System S.p.A. |
| 0x87 | Huf Hülsbeck & Fürst GmbH & Co. KG |
| 0x88 | MANN+HUMMEL GmbH |
| 0x89 | Brose Fahrzeugteile GmbH & Co. |
| 0x90 | Keihin |
| 0x91 | Vimercati S.p.a |
| 0x92 | CRH |
| 0x93 | TPO Display Corp |
| 0x94 | Küster Automotive GmbH |
| 0x95 | Hitachi Automotive |
| 0x96 | Continental AG |
| 0x97 | TI-Automotive |
| 0x98 | Hydro |
| 0x99 | Johnson Controls Inc. |
| 0x9A | Takata-Petri |
| 0x9B | Mitsubishi Electric B.V. (Melco) |
| 0x9C | Autokabel |
| 0x9D | GKN Plc |
| 0x9E | Zollner Elektronik AG |
| 0x9F | peiker acustic GmbH & Co. KG |
| 0xA0 | Bosal-Oris |
| 0xA1 | Cobasys |
| 0xA2 | Automotive Lighting Reutlingen GmbH |
| 0xA3 | CONTI VDO |
| 0xA4 | A.D.C. Automotive Distance Control Systems GmbH |
| 0xA5 | Novero Dabendorf GmbH |
| 0xA6 | LAMES S.p.a. |
| 0xA7 | Magna/Closures |
| 0xA8 | Harbin Wan Yu Technology Co |
| 0xA9 | ThyssenKrupp Presta AG |
| 0xAA | ArvinMeritor |
| 0xAB | Kongsberg Automotive GmbH |
| 0xAC | SMR Automotive Mirrors Stuttgart GmbH |
| 0xAD | So.Ge.Mi. |
| 0xAE | MTA S.p.A. |
| 0xAF | Alfmeier Präzision AG |
| 0xB0 | Eltek Deutechland GmbH |
| 0xB1 | OMRON Automotive Electronics Europe GmbH |
| 0xB2 | ASK Industries GmbH |
| 0xB3 | CML Innovative Technologies GmbH & Co. KG |
| 0xB4 | APAG Elektronik AG |
| 0xB5 | Nexteer Automotive |
| 0xB6 | Hans Widmaier Fernmelde- und Feinwerktechnik |
| 0xB7 | Robert Bosch Battery Systems GmbH |
| 0xB8 | Kyocera Display Europe GmbH |
| 0xB9 | Magna Powertrain AG & Co. KG |
| 0xBA | BorgWarner Beru Systems GmbH |
| 0xBB | BMW AG |
| 0xBC | Benteler Duncan Plant |
| 0xBD | U-Shin Deutschland Zugangssysteme GmbH |
| 0xBE | Schaeffler Technologies AG & Co. KG |
| 0xBF | JTEKT Corporation |
| 0xC0 | VLF |
| 0xC1 | Flextronics |
| 0xC2 | LG Chem |
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

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 18 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0004 | kein Signal oder Wert |
| 0x0008 | unplausibles Signal oder Wert |
| 0x0005 | Übertemperatur |
| 0x0006 | DKP-Adaption Drehzahl |
| 0x0007 | DKP-Adaption Delta überschritten |
| 0x0009 | DKP-Adaption Bereich überschritten |
| 0x000A | Bank 1 fehlerhaft |
| 0x000B | Bank 2 fehlerhaft |
| 0x000C | CRC16 fehlerhaft |
| 0x000D | NVRAM-Test fehlerhaft |
| 0x000E | Flash Device Id |
| 0x0010 | Reset-Grund unzulässig |
| 0x0011 | RAM-Test fehlerhaft |
| 0x0012 | ROM-Test fehlerhaft |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 3 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x0603 | 0x0012 | 0x000D | 0x0011 | 0x0010 |
| 0x0121 | 0xFFFF | 0x0009 | 0x0007 | 0x0006 |
| 0xFFFF | 0x0008 | 0x0004 | 0x0002 | 0x0001 |

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
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 20 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0105 | Umgebungsdrucksensor |
| 0x0110 | Ansauglufttemperaturfühler |
| 0x0115 | Motortemperaturfühler |
| 0x0120 | Drosselklappenpotentiometer |
| 0x0121 | schnelle Drosselklappenadaption |
| 0x0130 | Lambdasonde |
| 0x0135 | Lambdasondenheizung |
| 0x0201 | Einspritzventil |
| 0x0230 | Elektrische Kraftstoffpumpe |
| 0x0335 | KW-Signal |
| 0x0443 | Tankentlüftungsventil |
| 0x0480 | Elektrischer Lüfter |
| 0x0500 | Geschwindigkeitssignal |
| 0x0505 | Leerlaufregler |
| 0x0560 | Ubatt-Signal |
| 0x0561 | Wackelkontakt |
| 0x0603 | Steuergerätetest (SGS) |
| 0x0608 | UEXT Spannungsversorgung DKP |
| 0x0655 | Übertemperatur LED |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 20 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x0110 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0115 | 0x0C | 0x08 | 0x09 | - |
| 0x0120 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0130 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0105 | 0x0A | 0x08 | 0x09 | - |
| 0x0608 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0201 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0230 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0443 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0480 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0505 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0135 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0603 | 0x0D | - | - | - |
| 0x0655 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0335 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0500 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0560 | 0x0B | 0x08 | 0x09 | - |
| 0x0121 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0x0561 | 0x08 | 0x0E | 0x09 | 0x0F |
| 0xFFFF | 0x01 | 0x02 | 0x03 | 0x04 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 20 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | UWB1 unbelegt | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x02 | UWB2 unbelegt | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x03 | UWB3 unbelegt | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x04 | UWB4 unbelegt | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x05 | Systemfehler, Funktionsindex | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x06 | Systemfehler, Fehlernummer | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x07 | Systemfehler, Zeilennummer | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x08 | Drehzahl (Rpm) | 1/min | high | unsigned char | - | 50 | 1 | 0 |
| 0x09 | realer DK-Winkel (Dkw) | Grad | high | unsigned char | - | 8 | 17 | 0 |
| 0x0A | ADC-Wert des Umgebungsdrucksensors | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x0B | ADC-Wert der Batteriespannung | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x0C | ADC-Wert des Motortemperatursensors | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x0D | Selbsttest, Resetgrund oder RAM-Test | - | high | signed long | - | 1 | 1 | 0 |
| 0x0E | Fahrzeuggeschwindigkeit (Speed) | km/h | high | unsigned char | - | 1 | 1 | 0 |
| 0x0F | Last (Tl) | ms | high | unsigned char | - | 0.064 | 1 | 0 |
| 0x10 | Extremwert | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x11 | Zählerwert | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x12 | BMW-Istposition des Steppers | Steps | high | unsigned char | - | 1 | 1 | 0 |
| 0x13 | MM-Istposition des Steppers | Steps | high | unsigned char | - | 1 | 1 | 0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

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

<a id="table-horttexte"></a>
### HORTTEXTE

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
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 3 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x2710 | SYS |
| 0x2720 | Leerlaufstepper Positionsabweichung |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 3 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x2710 | 0x05 | 0x06 | 0x07 | - |
| 0x2720 | 0x10 | 0x11 | 0x12 | 0x13 |
| 0xFFFF | 0x01 | 0x02 | 0x03 | 0x04 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 20 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | UWB1 unbelegt | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x02 | UWB2 unbelegt | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x03 | UWB3 unbelegt | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x04 | UWB4 unbelegt | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x05 | Systemfehler, Funktionsindex | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x06 | Systemfehler, Fehlernummer | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x07 | Systemfehler, Zeilennummer | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x08 | Drehzahl (Rpm) | 1/min | high | unsigned char | - | 50 | 1 | 0 |
| 0x09 | realer DK-Winkel (Dkw) | Grad | high | unsigned char | - | 8 | 17 | 0 |
| 0x0A | ADC-Wert des Umgebungsdrucksensors | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x0B | ADC-Wert der Batteriespannung | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x0C | ADC-Wert des Motortemperatursensors | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x0D | Selbsttest, Resetgrund oder RAM-Test | - | high | signed long | - | 1 | 1 | 0 |
| 0x0E | Fahrzeuggeschwindigkeit (Speed) | km/h | high | unsigned char | - | 1 | 1 | 0 |
| 0x0F | Last (Tl) | ms | high | unsigned char | - | 0.064 | 1 | 0 |
| 0x10 | Extremwert | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x11 | Zählerwert | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x12 | BMW-Istposition des Steppers | Steps | high | unsigned char | - | 1 | 1 | 0 |
| 0x13 | MM-Istposition des Steppers | Steps | high | unsigned char | - | 1 | 1 | 0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 3 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xB6 | ERROR_SG_STATUS |
| 0xC1 | ERROR_RECORD_LOCAL_IDENTIFIER |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| - | BMW-FAST |
| - | KWP2000* |
| 1 | KWP2000 |
| - | DS2 |

<a id="table-typschluessel"></a>
### TYPSCHLUESSEL

Dimensions: 28 rows × 3 columns

| TYPNUMMER | BAUREIHE | INFO |
| --- | --- | --- |
| 0x0175 | 0xC914FF | R13 MÜ |
| 0x0176 | 0xC914FF | R13 DA MÜ |
| 0x0185 | 0xC914FF | R13 US MÜ |
| 0x0186 | 0xC914FF | R13 DA US MÜ |
| 0x0178 | 0xC914FF | R13/31 Behörde |
| 0x0179 | 0xC914FF | R13/31 US |
| 0x0180 | 0xC914FF | R13/31 Zivil |
| 0x0177 | 0xAD153F | K14/02 |
| 0x0187 | 0xAD153F | K14/02 US |
| 0x0164 | 0xAD157F | K15(SCR) |
| 0x0141 | 0xAD157F | K15(Country) |
| 0x0165 | 0xAD157F | K15(HE) |
| 0x0142 | 0xAD157F | K15(Challenge) |
| 0x0167 | 0xAD157F | K15(SM) |
| 0x0143 | 0xAD157F | K15(Moto) |
| 0x0194 | 0xAD157F | K15 US(SCR) |
| 0x0151 | 0xAD157F | K15 US(Country) |
| 0x0195 | 0xAD157F | K15 US(HE) |
| 0x0152 | 0xAD157F | K15 US(Challenge) |
| 0x0197 | 0xAD157F | K15 US(SM) |
| 0x0153 | 0xAD157F | K15 US(Moto) |
| 0x0171 | 0xC914FF | R13/31 CKD Brasilien |
| 0x0188 | 0xC914FF | R13/40 ECE (G650 GS) |
| 0x0189 | 0xC914FF | R13/40 US (G650 GS) |
| 0x0135 | 0xC914FF | R13/40 CKD (G650 GS) |
| 0x0136 | 0xC914FF | R13/40 ECE Sertao (G650 GS Sertao) |
| 0x0146 | 0xC914FF | R13/40 US Sertao (G650 GS Sertao) |
| 0x0137 | 0xC914FF | R13/40 CKD Sertao (G650 GS Sertao) |

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
