# qsg_71.prg

- Jobs: [63](#jobs)
- Tables: [37](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | QSG_71 |
| ORIGIN | BMW EA-715 Frank Kimmich |
| REVISION | 3.001 |
| AUTHOR | Vector_Informatik_GmbH PSF2 Rainer_Lutz, Vector_Informatik_GmbH PSF2 Andre_Baur, Vector_Informatik_GmbH PSF2 Dietmar_Gorenflo, ZF_Friedrichshafen TE_AB Andreas_Kurdum |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
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
- [STATUS_FSV](#job-status-fsv) - Status FSV auslesen mit dem SGBD-Generator erzeugt
- [STATUS_OSV](#job-status-osv) - Status OSV auslesen mit dem SGBD-Generator erzeugt
- [STATUS_QSG](#job-status-qsg) - Status QSG auslesen mit dem SGBD-Generator erzeugt
- [STATUS_TV_EINHEIT_LINKS](#job-status-tv-einheit-links) - Status TV EInheit links auslesen mit dem SGBD-Generator erzeugt
- [STATUS_TV_EINHEIT_RECHTS](#job-status-tv-einheit-rechts) - Status TV EInheit rechts auslesen mit dem SGBD-Generator erzeugt
- [STATUS_KLASSIFIZIERUNG](#job-status-klassifizierung) - PHi-Offset/Klassifizierung auslesen mit dem SGBD-Generator erzeugt
- [STATUS_FUNKTIONEN](#job-status-funktionen) - Status der Funktionen (STEUERN-Jobs) auslesen mit dem SGBD-Generator erzeugt
- [STATUS_TV_MOMENT](#job-status-tv-moment) - Status Momente auslesen mit dem SGBD-Generator erzeugt
- [STATUS_DRLS_EEPROM_LINKS](#job-status-drls-eeprom-links) - DRLS EEPROM links auslesen mit dem SGBD-Generator erzeugt
- [STATUS_DRLS_EEPROM_RECHTS](#job-status-drls-eeprom-rechts) - DRLS EEPROM rechts auslesen mit dem SGBD-Generator erzeugt
- [TEST_JOB](#job-test-job) - Universeller Diagnose Job für Diagnose Tests Modus  : Default
- [STEUERN_ADAPTION](#job-steuern-adaption) - Adaption ueber Diagnose durchfuehren Modus  : Default
- [STEUERN_GETRIEBEDATEN](#job-steuern-getriebedaten) - Uebernahme der Achsgetriebedaten - alle Daten des Senors - in QSG Modus  : Default
- [STEUERN_MOTORTAUSCH](#job-steuern-motortausch) - Uebernahme der Motordaten - alle motorspezifischen Daten des Senors - in das QSG Modus  : Default
- [STEUERN_FUNKTIONSTEST](#job-steuern-funktionstest) - Funktionstest ueber Diagnose starten Modus  : Default
- [STEUERN_MOMENTENVORGABE](#job-steuern-momentenvorgabe) - Ansteuerung des Stellers ueber Diagnose Modus  : Default
- [STATUS_DATEN_GETRIEBEZUSTAND](#job-status-daten-getriebezustand) - STATUS_DATEN_GETRIEBEZUSTAND Modus  : Default
- [STEUERN_GETRIEBEZUSTAND](#job-steuern-getriebezustand) - Getriebzustand steuern Modus  : Default
- [STATUS_FASTA_DATEN_LINKS](#job-status-fasta-daten-links) - FASTA_DATEN_LINKS mit dem SGBD-Generator erzeugt
- [STATUS_FASTA_DATEN_RECHTS](#job-status-fasta-daten-rechts) - FASTA_DATEN_RECHTS mit dem SGBD-Generator erzeugt
- [STEUERN_OELVERSCHLEISS_RUECKSETZEN](#job-steuern-oelverschleiss-ruecksetzen) - OELVERSCHLEISS ruecksetzen  Modus  : Default
- [STATUS_DATEN_GETRIEBEZUSTAND_PU0803](#job-status-daten-getriebezustand-pu0803) - STATUS_DATEN_GETRIEBEZUSTAND_PU0803 Modus  : Default
- [STATUS_FASTA_DATEN_LINKS_PU0803](#job-status-fasta-daten-links-pu0803) - FASTA_DATEN_LINKS_PU0803 mit dem SGBD-Generator erzeugt
- [STATUS_FASTA_DATEN_RECHTS_PU0803](#job-status-fasta-daten-rechts-pu0803) - FASTA_DATEN_RECHTS_PU0803 mit dem SGBD-Generator erzeugt
- [STEUERN_GETRIEBEZUSTAND_PU0803](#job-steuern-getriebezustand-pu0803) - Getriebzustand steuern_PU0803 Modus  : Default

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

<a id="job-status-fsv"></a>
### STATUS_FSV

Status FSV auslesen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FSV_BYTE_1_WERT | real | FSV auslesen Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_FSV_BYTE_1_EINH | string | FSV auslesen Einheit: 0-n |
| STAT_FSV_BYTE_2_WERT | real | FSV auslesen Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_FSV_BYTE_2_EINH | string | FSV auslesen Einheit: 0-n |
| STAT_FSV_BYTE_3_WERT | real | FSV auslesen Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_FSV_BYTE_3_EINH | string | FSV auslesen Einheit: 0-n |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-osv"></a>
### STATUS_OSV

Status OSV auslesen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_OSV_BYTE_1_WERT | real | OSV auslesen Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_OSV_BYTE_1_EINH | string | OSV auslesen Einheit: 0-n |
| STAT_OSV_BYTE_2_WERT | real | OSV auslesen Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_OSV_BYTE_2_EINH | string | OSV auslesen Einheit: 0-n |
| STAT_OSV_BYTE_3_WERT | real | OSV auslesen Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_OSV_BYTE_3_EINH | string | OSV auslesen Einheit: 0-n |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-qsg"></a>
### STATUS_QSG

Status QSG auslesen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_UNUSED_WERT | real | Reserved Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_UNUSED_EINH | string | Reserved Einheit: 0-n |
| STAT_SERVICEQUALIFIER_WERT | int | Service-Qualifier table STAT_QSG_SERVICEQUALIFIER WERT |
| STAT_SERVICEQUALIFIER_TEXT | string | Service-Qualifier table STAT_QSG_SERVICEQUALIFIER TEXT |
| STAT_VERFUEGBARKEIT_QMVH_WERT | real | Verfuegbarkeit QMVH Bereich von 0 [%] bis 100 [%] |
| STAT_VERFUEGBARKEIT_QMVH_EINH | string | Verfuegbarkeit QMVH Einheit: % |
| STAT_ADAPTION_LINKS_WERT | int | Adaption links table STAT_ADAPTION_LINKS WERT |
| STAT_ADAPTION_LINKS_TEXT | string | Adaption links table STAT_ADAPTION_LINKS TEXT |
| STAT_ADAPTION_RECHTS_WERT | int | Adpation rechts table STAT_ADAPTION_RECHTS WERT |
| STAT_ADAPTION_RECHTS_TEXT | string | Adpation rechts table STAT_ADAPTION_RECHTS TEXT |
| STAT_TEMPERATUR_GETRIEBE_WERT | real | Temperaturt Getriebe Bereich von -40 [°C] bis 212 [°C] |
| STAT_TEMPERATUR_GETRIEBE_EINH | string | Temperaturt Getriebe Einheit: °C |
| STAT_VEHICLE_SPEED_WERT | real | Vehicle speed Bereich von -200 [km/h] bis 400 [km/h] |
| STAT_VEHICLE_SPEED_EINH | string | Vehicle speed Einheit: km/h |
| STAT_ENGINE_SPEED_WERT | real | Engine Speed Bereich von 0 [Upm] bis 12000 [Upm] |
| STAT_ENGINE_SPEED_EINH | string | Engine Speed Einheit: Upm |
| STAT_QSG_MESSUNG_UBAT_KL_30_WERT | real | QSG Messung Ubat an Kl. 30 Bereich von 0 [V] bis 20 [V] |
| STAT_QSG_MESSUNG_UBAT_KL_30_EINH | string | QSG Messung Ubat an Kl. 30 Einheit: V |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tv-einheit-links"></a>
### STATUS_TV_EINHEIT_LINKS

Status TV EInheit links auslesen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VERFUEGBARKEIT_TV_LINKS_WERT | int | Verfuegbarkeit TV links table STAT_VERFUEGBARKEIT_TV_XXX WERT |
| STAT_VERFUEGBARKEIT_TV_LINKS_TEXT | string | Verfuegbarkeit TV links table STAT_VERFUEGBARKEIT_TV_XXX TEXT |
| STAT_LAGE_INFO_AKTUATOR_LINKS_WERT | real | Lage Info Aktuator links Bereich von -5000 [°] bis 5000 [°] |
| STAT_LAGE_INFO_AKTUATOR_LINKS_EINH | string | Lage Info Aktuator links Einheit: ° |
| STAT_IST_MOMENT_MOTOR_LINKS_WERT | real | Ist-Moment Motor links Bereich von -0,250 [Nm] bis 0,250 [Nm] |
| STAT_IST_MOMENT_MOTOR_LINKS_EINH | string | Ist-Moment Motor links Einheit: Nm |
| STAT_TEMPERATUR_TV_EINHEIT_LINKS_WERT | real | Temperatur TV-Einheit links Bereich von -40 [°C] bis 200 [°C] |
| STAT_TEMPERATUR_TV_EINHEIT_LINKS_EINH | string | Temperatur TV-Einheit links Einheit: °C |
| STAT_TEMPERATUR_MOTOR_LINKS_WERT | real | Temperatur Motor links Bereich von -40 [°C] bis 200 [°C] |
| STAT_TEMPERATUR_MOTOR_LINKS_EINH | string | Temperatur Motor links Einheit: °C |
| STAT_TEMPERATUR_LAMELLE_LINKS_WERT | real | Temperatur Lamelle links Bereich von -40 [°C] bis 200 [°C] |
| STAT_TEMPERATUR_LAMELLE_LINKS_EINH | string | Temperatur Lamelle links Einheit: °C |
| STAT_SENSORVERSORGUNGSSPANNUNG_LINKS_WERT | real | Sensorversorgungsspannung links Bereich von 0 [V] bis 10 [V] |
| STAT_SENSORVERSORGUNGSSPANNUNG_LINKS_EINH | string | Sensorversorgungsspannung links Einheit: V |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tv-einheit-rechts"></a>
### STATUS_TV_EINHEIT_RECHTS

Status TV EInheit rechts auslesen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VERFUEGBARKEIT_TV_RECHTS_WERT | int | Verfuegbarkeit TV rechts table STAT_VERFUEGBARKEIT_TV_XXX WERT |
| STAT_VERFUEGBARKEIT_TV_RECHTS_TEXT | string | Verfuegbarkeit TV rechts table STAT_VERFUEGBARKEIT_TV_XXX TEXT |
| STAT_LAGE_INFO_AKTUATOR_RECHTS_WERT | real | Lage Info Aktuator rechts Bereich von -5000 [°] bis 5000 [°] |
| STAT_LAGE_INFO_AKTUATOR_RECHTS_EINH | string | Lage Info Aktuator rechts Einheit: ° |
| STAT_IST_MOMENT_MOTOR_RECHTS_WERT | real | Ist-Moment Motor rechts Bereich von -0,250 [Nm] bis 0,250 [Nm] |
| STAT_IST_MOMENT_MOTOR_RECHTS_EINH | string | Ist-Moment Motor rechts Einheit: Nm |
| STAT_TEMPERATUR_TV_EINHEIT_RECHTS_WERT | real | Temperatur TV-Einheit rechts Bereich von -40 [°C] bis 200 [°C] |
| STAT_TEMPERATUR_TV_EINHEIT_RECHTS_EINH | string | Temperatur TV-Einheit rechts Einheit: °C |
| STAT_TEMPERATUR_MOTOR_RECHTS_WERT | real | Temperatur Motor rechts Bereich von -40 [°C] bis 200 [°C] |
| STAT_TEMPERATUR_MOTOR_RECHTS_EINH | string | Temperatur Motor rechts Einheit: °C |
| STAT_TEMPERATUR_LAMELLE_RECHTS_WERT | real | Temperatur Lamelle rechts Bereich von -40 [°C] bis 200 [°C] |
| STAT_TEMPERATUR_LAMELLE_RECHTS_EINH | string | Temperatur Lamelle rechts Einheit: °C |
| STAT_SENSORVERSORGUNGSSPANNUNG_RECHTS_WERT | real | Sensorversorgungsspannung rechts Bereich von 0 [V] bis 10 [V] |
| STAT_SENSORVERSORGUNGSSPANNUNG_RECHTS_EINH | string | Sensorversorgungsspannung rechts Einheit: V |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klassifizierung"></a>
### STATUS_KLASSIFIZIERUNG

PHi-Offset/Klassifizierung auslesen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PHI_OFFSET_LINKS_WERT | real | Phi Offset links Bereich von -4000 [°] bis 4000 [°] |
| STAT_PHI_OFFSET_LINKS_EINH | string | Phi Offset links Einheit: ° |
| STAT_PHI_OFFSET_RECHTS_WERT | real | Phi Offset rechts Bereich von -4000 [°] bis 4000 [°] |
| STAT_PHI_OFFSET_RECHTS_EINH | string | Phi Offset rechts Einheit: ° |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-funktionen"></a>
### STATUS_FUNKTIONEN

Status der Funktionen (STEUERN-Jobs) auslesen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GETRIEBEDATEN_WERT | int | Status Getriebedaten table STAT_FUNKTIONEN_1 WERT |
| STAT_GETRIEBEDATEN_TEXT | string | Status Getriebedaten table STAT_FUNKTIONEN_1 TEXT |
| STAT_GETRIEBEZUSTAND_WERT | int | GETRIEBEZUSTAND table STAT_FUNKTIONEN_1 WERT |
| STAT_GETRIEBEZUSTAND_TEXT | string | GETRIEBEZUSTAND table STAT_FUNKTIONEN_1 TEXT |
| STAT_RESERVED_2_WERT | real | Verschleiss Bereich von 0 [%] bis 100 [%] |
| STAT_RESERVED_2_EINH | string | Verschleiss Einheit: % |
| STAT_RESERVED_3_WERT | int | Status Getriebeuebersetzung table STAT_FUNKTIONEN_2 WERT |
| STAT_RESERVED_3_TEXT | string | Status Getriebeuebersetzung table STAT_FUNKTIONEN_2 TEXT |
| STAT_ADAPTION_WERT | int | Status Adaption table STAT_FUNKTIONEN_2 WERT |
| STAT_ADAPTION_TEXT | string | Status Adaption table STAT_FUNKTIONEN_2 TEXT |
| STAT_FUNKTIONSTEST_WERT | int | Status Funktionstest table STAT_FUNKTIONEN_2 WERT |
| STAT_FUNKTIONSTEST_TEXT | string | Status Funktionstest table STAT_FUNKTIONEN_2 TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tv-moment"></a>
### STATUS_TV_MOMENT

Status Momente auslesen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SOLL_TV_MOMENT_WERT | real | Soll TV Moment Bereich von -2500 [Nm] bis 2500 [Nm] |
| STAT_SOLL_TV_MOMENT_EINH | string | Soll TV Moment Einheit: Nm |
| STAT_IST_TV_MOMENT_WERT | real | Ist TV Moment Bereich von -2500 [Nm] bis 2500 [Nm] |
| STAT_IST_TV_MOMENT_EINH | string | Ist TV Moment Einheit: Nm |
| STAT_MOMENTENVORGABE_WERT | int | Momentenvorgabe table STAT_FUNKTIONEN_2 WERT |
| STAT_MOMENTENVORGABE_TEXT | string | Momentenvorgabe table STAT_FUNKTIONEN_2 TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drls-eeprom-links"></a>
### STATUS_DRLS_EEPROM_LINKS

DRLS EEPROM links auslesen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DRLS_EEPROM_LINKS_1_WERT | real | DRLS EEPROM LINKS Byte 1 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_1_EINH | string | DRLS EEPROM LINKS Byte 1 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_2_WERT | real | DRLS EEPROM LINKS Byte 2 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_2_EINH | string | DRLS EEPROM LINKS Byte 2 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_3_WERT | real | DRLS EEPROM LINKS Byte 3 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_3_EINH | string | DRLS EEPROM LINKS Byte 3 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_4_WERT | real | DRLS EEPROM LINKS Byte 4 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_4_EINH | string | DRLS EEPROM LINKS Byte 4 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_5_WERT | real | DRLS EEPROM LINKS Byte 5 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_5_EINH | string | DRLS EEPROM LINKS Byte 5 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_6_WERT | real | DRLS EEPROM LINKS Byte 6 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_6_EINH | string | DRLS EEPROM LINKS Byte 6 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_7_WERT | real | DRLS EEPROM LINKS Byte 7 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_7_EINH | string | DRLS EEPROM LINKS Byte 7 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_8_WERT | real | DRLS EEPROM LINKS Byte 8 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_8_EINH | string | DRLS EEPROM LINKS Byte 8 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_9_WERT | real | DRLS EEPROM LINKS Byte 9 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_9_EINH | string | DRLS EEPROM LINKS Byte 9 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_10_WERT | real | DRLS EEPROM LINKS Byte 10 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_10_EINH | string | DRLS EEPROM LINKS Byte 10 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_11_WERT | real | DRLS EEPROM LINKS Byte 11 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_11_EINH | string | DRLS EEPROM LINKS Byte 11 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_12_WERT | real | DRLS EEPROM LINKS Byte 12 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_12_EINH | string | DRLS EEPROM LINKS Byte 12 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_13_WERT | real | DRLS EEPROM LINKS Byte 13 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_13_EINH | string | DRLS EEPROM LINKS Byte 13 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_14_WERT | real | DRLS EEPROM LINKS Byte 14 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_14_EINH | string | DRLS EEPROM LINKS Byte 14 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_15_WERT | real | DRLS EEPROM LINKS Byte 15 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_15_EINH | string | DRLS EEPROM LINKS Byte 15 Einheit: 0-n |
| STAT_DRLS_EEPROM_LINKS_16_WERT | real | DRLS EEPROM LINKS Byte 16 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_LINKS_16_EINH | string | DRLS EEPROM LINKS Byte 16 Einheit: 0-n |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drls-eeprom-rechts"></a>
### STATUS_DRLS_EEPROM_RECHTS

DRLS EEPROM rechts auslesen mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DRLS_EEPROM_RECHTS_1_WERT | real | DRLS EEPROM RECHTS Byte 1 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_1_EINH | string | DRLS EEPROM RECHTS Byte 1 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_2_WERT | real | DRLS EEPROM RECHTS Byte 2 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_2_EINH | string | DRLS EEPROM RECHTS Byte 2 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_3_WERT | real | DRLS EEPROM RECHTS Byte 3 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_3_EINH | string | DRLS EEPROM RECHTS Byte 3 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_4_WERT | real | DRLS EEPROM RECHTS Byte 4 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_4_EINH | string | DRLS EEPROM RECHTS Byte 4 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_5_WERT | real | DRLS EEPROM RECHTS Byte 5 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_5_EINH | string | DRLS EEPROM RECHTS Byte 5 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_6_WERT | real | DRLS EEPROM RECHTS Byte 6 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_6_EINH | string | DRLS EEPROM RECHTS Byte 6 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_7_WERT | real | DRLS EEPROM RECHTS Byte 7 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_7_EINH | string | DRLS EEPROM RECHTS Byte 7 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_8_WERT | real | DRLS EEPROM RECHTS Byte 8 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_8_EINH | string | DRLS EEPROM RECHTS Byte 8 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_9_WERT | real | DRLS EEPROM RECHTS Byte 9 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_9_EINH | string | DRLS EEPROM RECHTS Byte 9 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_10_WERT | real | DRLS EEPROM RECHTS Byte 10 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_10_EINH | string | DRLS EEPROM RECHTS Byte 10 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_11_WERT | real | DRLS EEPROM RECHTS Byte 11 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_11_EINH | string | DRLS EEPROM RECHTS Byte 11 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_12_WERT | real | DRLS EEPROM RECHTS Byte 12 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_12_EINH | string | DRLS EEPROM RECHTS Byte 12 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_13_WERT | real | DRLS EEPROM RECHTS Byte 13 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_13_EINH | string | DRLS EEPROM RECHTS Byte 13 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_14_WERT | real | DRLS EEPROM RECHTS Byte 14 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_14_EINH | string | DRLS EEPROM RECHTS Byte 14 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_15_WERT | real | DRLS EEPROM RECHTS Byte 15 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_15_EINH | string | DRLS EEPROM RECHTS Byte 15 Einheit: 0-n |
| STAT_DRLS_EEPROM_RECHTS_16_WERT | real | DRLS EEPROM RECHTS Byte 16 Bereich von 0 [0-n] bis 255 [0-n] |
| STAT_DRLS_EEPROM_RECHTS_16_EINH | string | DRLS EEPROM RECHTS Byte 16 Einheit: 0-n |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-test-job"></a>
### TEST_JOB

Universeller Diagnose Job für Diagnose Tests Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL_DATEN | int | Anzahl Daten der folgenden Diagnose Anfrage |
| DATEN_1 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_2 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_3 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_4 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_5 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_6 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_7 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_8 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_9 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_10 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_11 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_12 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_13 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_14 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_15 | int | Abhängig von Argument ANZAHL_DATEN |
| DATEN_16 | int | Abhängig von Argument ANZAHL_DATEN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-adaption"></a>
### STEUERN_ADAPTION

Adaption ueber Diagnose durchfuehren Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL_ADAPTIONEN | unsigned char | Anzahl der Adaptionen Range: 0 ... 255  0=Erstadaption &gt;0=Anzahl der hintereinander durchzuführenden Adaptionen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-getriebedaten"></a>
### STEUERN_GETRIEBEDATEN

Uebernahme der Achsgetriebedaten - alle Daten des Senors - in QSG Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motortausch"></a>
### STEUERN_MOTORTAUSCH

Uebernahme der Motordaten - alle motorspezifischen Daten des Senors - in das QSG Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-funktionstest"></a>
### STEUERN_FUNKTIONSTEST

Funktionstest ueber Diagnose starten Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-momentenvorgabe"></a>
### STEUERN_MOMENTENVORGABE

Ansteuerung des Stellers ueber Diagnose Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SOLL_QUER_MOMENT_HINTERACHSE_STELLGLIED | int | Vorgabe Quermomentenverteilung Hinterachse Stellglied Range: -2500 ... 2500Nm |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-daten-getriebezustand"></a>
### STATUS_DATEN_GETRIEBEZUSTAND

STATUS_DATEN_GETRIEBEZUSTAND Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KILOMETER_STAND | long | Hex-Antwort von SG |
| STAT_KUPPLUNGSREIBLEISTUNG_LINKS | long | Hex-Antwort von SG |
| STAT_KUPPLUNGSREIBLEISTUNG_RECHTS | long | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Auftrag an SG |

<a id="job-steuern-getriebezustand"></a>
### STEUERN_GETRIEBEZUSTAND

Getriebzustand steuern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KM | long | Vorgabe Km Range: 16777215 |
| KUPPLUNGSREIBLEISTUNG_LINKS | long | tbd Range: tbd |
| KUPPLUNGSREIBLEISTUNG_RECHTS | long | tbd Range: tbd |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta-daten-links"></a>
### STATUS_FASTA_DATEN_LINKS

FASTA_DATEN_LINKS mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DS_ARBEIT_GESAMT_WERT | long | DS_ARBEIT_GESAMMT Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_GESAMT_EINH | string | DS_ARBEIT_GESAMMT Einheit: kJ |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_1_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_1 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_1_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_1 Einheit: s |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_2_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_2 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_2_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_2 Einheit: s |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_3_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_3 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_3_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_3 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_1_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_1 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_1_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_1 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_2_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_2 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_2_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_2 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_3_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_3 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_3_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_3 Einheit: s |
| STAT_DS_ARBEIT_OELTEMP_KL_1_WERT | long | DS_ARBEIT_OELTEMP_KL_1 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_1_EINH | string | DS_ARBEIT_OELTEMP_KL_1 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_2_WERT | long | DS_ARBEIT_OELTEMP_KL_2 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_2_EINH | string | DS_ARBEIT_OELTEMP_KL_2 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_3_WERT | long | DS_ARBEIT_OELTEMP_KL_3 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_3_EINH | string | DS_ARBEIT_OELTEMP_KL_3 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_4_WERT | long | DS_ARBEIT_OELTEMP_KL_4 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_4_EINH | string | DS_ARBEIT_OELTEMP_KL_4 Einheit: kJ |
| STAT_DS_UMDR_KL_1_1_WERT | long | DS_UMDR_KL_1_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_1_EINH | string | DS_UMDR_KL_1_1 Einheit: rpm |
| STAT_DS_UMDR_KL_2_1_WERT | long | DS_UMDR_KL_2_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_1_EINH | string | DS_UMDR_KL_2_1 Einheit: rpm |
| STAT_DS_UMDR_KL_3_1_WERT | long | DS_UMDR_KL_3_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_1_EINH | string | DS_UMDR_KL_3_1 Einheit: rpm |
| STAT_DS_UMDR_KL_4_1_WERT | long | DS_UMDR_KL_4_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_1_EINH | string | DS_UMDR_KL_4_1 Einheit: rpm |
| STAT_DS_UMDR_KL_5_1_WERT | long | DS_UMDR_KL_5_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_1_EINH | string | DS_UMDR_KL_5_1 Einheit: rpm |
| STAT_DS_UMDR_KL_6_1_WERT | long | DS_UMDR_KL_6_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_1_EINH | string | DS_UMDR_KL_6_1 Einheit: rpm |
| STAT_DS_UMDR_KL_1_2_WERT | long | DS_UMDR_KL_1_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_2_EINH | string | DS_UMDR_KL_1_2 Einheit: rpm |
| STAT_DS_UMDR_KL_2_2_WERT | long | DS_UMDR_KL_2_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_2_EINH | string | DS_UMDR_KL_2_2 Einheit: rpm |
| STAT_DS_UMDR_KL_3_2_WERT | long | DS_UMDR_KL_3_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_2_EINH | string | DS_UMDR_KL_3_2 Einheit: rpm |
| STAT_DS_UMDR_KL_4_2_WERT | long | DS_UMDR_KL_4_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_2_EINH | string | DS_UMDR_KL_4_2 Einheit: rpm |
| STAT_DS_UMDR_KL_5_2_WERT | long | DS_UMDR_KL_5_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_2_EINH | string | DS_UMDR_KL_5_2 Einheit: rpm |
| STAT_DS_UMDR_KL_6_2_WERT | long | DS_UMDR_KL_6_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_2_EINH | string | DS_UMDR_KL_6_2 Einheit: rpm |
| STAT_DS_UMDR_KL_1_3_WERT | long | DS_UMDR_KL_1_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_3_EINH | string | DS_UMDR_KL_1_3 Einheit: rpm |
| STAT_DS_UMDR_KL_2_3_WERT | long | DS_UMDR_KL_2_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_3_EINH | string | DS_UMDR_KL_2_3 Einheit: rpm |
| STAT_DS_UMDR_KL_3_3_WERT | long | DS_UMDR_KL_3_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_3_EINH | string | DS_UMDR_KL_3_3 Einheit: rpm |
| STAT_DS_UMDR_KL_4_3_WERT | long | DS_UMDR_KL_4_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_3_EINH | string | DS_UMDR_KL_4_3 Einheit: rpm |
| STAT_DS_UMDR_KL_5_3_WERT | long | DS_UMDR_KL_5_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_3_EINH | string | DS_UMDR_KL_5_3 Einheit: rpm |
| STAT_DS_UMDR_KL_6_3_WERT | long | DS_UMDR_KL_6_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_3_EINH | string | DS_UMDR_KL_6_3 Einheit: rpm |
| STAT_DS_LEISTUNG_MAX_WERT | long | DS_LEISTUNG_MAX Bereich von 0 [W] bis 65535 [W] |
| STAT_DS_LEISTUNG_MAX_EINH | string | DS_LEISTUNG_MAX Einheit: W |
| STAT_DS_GESCHW_FAHRZEUG_MAX_WERT | long | DS_GESCHW_FAHRZEUG_MAX Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_GESCHW_FAHRZEUG_MAX_EINH | string | DS_GESCHW_FAHRZEUG_MAX Einheit: km/h |
| STAT_DS_RADDIFF_GESCHW_MAX_WERT | long | DS_RADDIFF_GESCHW_MAX Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_RADDIFF_GESCHW_MAX_EINH | string | DS_RADDIFF_GESCHW_MAX Einheit: km/h |
| STAT_DS_RADDIFF_EXTREM_GESCHW_WERT | long | DS_RADDIFF_EXTREM_GESCHW Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_RADDIFF_EXTREM_GESCHW_EINH | string | DS_RADDIFF_EXTREM_GESCHW Einheit: km/h |
| STAT_DS_RADDIFF_EXTREM_KUPMOMENT_WERT | long | DS_RADDIFF_EXTREM_KUPMOMENT Bereich von -32768 [Nm] bis 32767 [Nm] |
| STAT_DS_RADDIFF_EXTREM_KUPMOMENT_EINH | string | DS_RADDIFF_EXTREM_KUPMOMENT Einheit: Nm |
| STAT_DS_ENDSTUFENSTOPS_ENDST_WERT | long | DS_ENDSTUFENSTOPS_ENDST Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_ENDST_EINH | string | DS_ENDSTUFENSTOPS_ENDST Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_MOTOR_WERT | long | DS_ENDSTUFENSTOPS_MOTOR Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_MOTOR_EINH | string | DS_ENDSTUFENSTOPS_MOTOR Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_OEL_WERT | long | DS_ENDSTUFENSTOPS_OEL Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_OEL_EINH | string | DS_ENDSTUFENSTOPS_OEL Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_LAM_WERT | long | DS_ENDSTUFENSTOPS_LAM Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_LAM_EINH | string | DS_ENDSTUFENSTOPS_LAM Einheit: 0/1 |
| STAT_DS_ADAPTIONEN_ABGESCHLOSSEN_WERT | long | DS_ADAPTIONEN_ABGESCHLOSSEN Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ADAPTIONEN_ABGESCHLOSSEN_EINH | string | DS_ADAPTIONEN_ABGESCHLOSSEN Einheit: 0/1 |
| STAT_DS_ADAPTIONEN_ABGEBROCHEN_WERT | long | DS_ADAPTIONEN_ABGEBROCHEN Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ADAPTIONEN_ABGEBROCHEN_EINH | string | DS_ADAPTIONEN_ABGEBROCHEN Einheit: 0/1 |
| STAT_DS_KILOMETERSTAND_AKTUELL_WERT | long | DS_KILOMETERSTAND_AKTUELL Bereich von 0 [km] bis 4294967295 [km] |
| STAT_DS_KILOMETERSTAND_AKTUELL_EINH | string | DS_KILOMETERSTAND_AKTUELL Einheit: km |
| STAT_DS_KILOMETERSTAND_EINBAU_WERT | long | DS_KILOMETERSTAND_EINBAU Bereich von 0 [km] bis 4294967295 [km] |
| STAT_DS_KILOMETERSTAND_EINBAU_EINH | string | DS_KILOMETERSTAND_EINBAU Einheit: km |
| STAT_DS_ZEIT_SPANNUNG_KL1_WERT | long | DS_ZEIT_SPANNUNG_KL1_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL1_EINH | string | DS_ZEIT_SPANNUNG_KL1_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL2_WERT | long | DS_ZEIT_SPANNUNG_KL2_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL2_EINH | string | DS_ZEIT_SPANNUNG_KL2_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL3_WERT | long | DS_ZEIT_SPANNUNG_KL3_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL3_EINH | string | DS_ZEIT_SPANNUNG_KL3_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL4_WERT | long | DS_ZEIT_SPANNUNG_KL4_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL4_EINH | string | DS_ZEIT_SPANNUNG_KL4_MOTOR_EIN Einheit: s |
| STAT_DS_ASM_INTEGRAL_WERT | long | DS_ASM_INTEGTRAL Bereich von 0 [Nms] bis 4294967295 [Nms] |
| STAT_DS_ASM_INTEGRAL_EINH | string | DS_ASM_INTEGTRAL Einheit: Nms |
| STAT_DS_ARBEIT_GETRIEBEVERLUST_WERT | long | DS_ARBEIT_GERTRIEBEVERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_GETRIEBEVERLUST_EINH | string | DS_ARBEIT_GERTRIEBEVERLUST Einheit: kJ |
| STAT_DS_ARBEIT_TV_VERLUST_WERT | long | DS_ARBEIT_TV_VERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_TV_VERLUST_EINH | string | DS_ARBEIT_TV_VERLUST Einheit: kJ |
| STAT_DS_KUPMOMENT_EXTREM_GESCHW_WERT | long | DS_KUPMOMENT_EXTREM_GESCHW Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_KUPMOMENT_EXTREM_GESCHW_EINH | string | DS_KUPMOMENT_EXTREM_GESCHW Einheit: km/h |
| STAT_DS_KUPMOMENT_EXTREM_KUPMOMENT_WERT | long | DS_KUPMOMENT_EXTREM_KUPMOMENT Bereich von -32768 [Nm] bis 32767 [Nm] |
| STAT_DS_KUPMOMENT_EXTREM_KUPMOMENT_EINH | string | DS_KUPMOMENT_EXTREM_KUPMOMENT Einheit: Nm |
| STAT_DS_ARBEIT_DIFFERENTIALVERLUST_WERT | long | DS_ARBEIT_DIFFERENTIALVERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_DIFFERENTIALVERLUST_EINH | string | DS_ARBEIT_DIFFERENTIALVERLUST Einheit: kJ |
| STAT_DS_ERSTADAPTIONSWERT_WERT | long | DS_ERSTADAPTIONSWERT Bereich von -32768 [°] bis 32767 [°] |
| STAT_DS_ERSTADAPTIONSWERT_EINH | string | DS_ERSTADAPTIONSWERT Einheit: ° |
| STAT_DS_MAX_ZEIT_LAGE_ZU_HOCH_WERT | long | DS_MAX_ZEIT_LAGE_ZU_HOCH Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_MAX_ZEIT_LAGE_ZU_HOCH_EINH | string | DS_MAX_ZEIT_LAGE_ZU_HOCH Einheit: ms |
| STAT_DS_MAX_ZEIT_LAGE_ZU_NIEDRIG_WERT | long | DS_MAX_ZEIT_LAGE_ZU_NIEDRIG Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_MAX_ZEIT_LAGE_ZU_NIEDRIG_EINH | string | DS_MAX_ZEIT_LAGE_ZU_NIEDRIG Einheit: ms |
| STAT_DS_ABLAGESCHEMA_WERT | long | DS_ABLAGESCHEMA Bereich von 0 [°] bis 255 [°] |
| STAT_DS_ABLAGESCHEMA_EINH | string | DS_ABLAGESCHEMA Einheit: 0/1 |
| STAT_DS_DIFFM_WERT | long | DS_DIFFM Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFM_EINH | string | DS_DIFFM Einheit: ms |
| STAT_DS_DIFFPSI_WERT | long | DS_DIFFPSI Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFPSI_EINH | string | DS_DIFFPSI Einheit: ms |
| STAT_DS_DIFFANGLE_WERT | long | DS_DIFFANGLE Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFANGLE_EINH | string | DS_DIFFANGLE Einheit: ms |
| STAT_DS_DIFFLENGTH_WERT | long | DS_DIFFLENGTH Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFLENGTH_EINH | string | DS_DIFFLENGTH Einheit: ms |
| STAT_DS_PIT01_WERT | long | DS_PIT01 Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_PIT01_EINH | string | DS_PIT01 Einheit: 0/1 |
| STAT_DS_PIT23_WERT | long | DS_PIT23 Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_PIT23_EINH | string | DS_PIT23 Einheit: 0/1 |
| STAT_DS_NUM_PLAUSI_M_ERROR_WERT | long | DS_NUM_PLAUSI_M_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_PLAUSI_M_ERROR_EINH | string | DS_NUM_PLAUSI_M_ERROR Einheit: 0/1 |
| STAT_DS_NUM_PLAUSI_PSI_ERROR_WERT | long | DS_NUM_PLAUSI_PSI_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_PLAUSI_PSI_ERROR_EINH | string | DS_NUM_PLAUSI_PSI_ERROR Einheit: 0/1 |
| STAT_DS_NUM_LENGTH_ERROR_WERT | long | DS_NUM_LENGTH_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_LENGTH_ERROR_EINH | string | DS_NUM_LENGTH_ERROR Einheit: 0/1 |
| STAT_DS_NUM_ANGLE_ERROR_WERT | long | DS_NUM_ANGLE_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_ANGLE_ERROR_EINH | string | DS_NUM_ANGLE_ERROR Einheit: 0/1 |
| STAT_DS_LAGEINIT_PLAUSI_MAX_ZEIT_WERT | long | DS_LAGEINIT_PLAUSI_MAX_ZEIT Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_LAGEINIT_PLAUSI_MAX_ZEIT_EINH | string | DS_LAGEINIT_PLAUSI_MAX_ZEIT Einheit: ms |
| STAT_DS_LAGEINIT_PLAUSI_ASM_MOMENT_WERT | long | DS_LAGEINIT_PLAUSI_ASM_MOMENT Bereich von -32768 [] bis 32767 [] |
| STAT_DS_LAGEINIT_PLAUSI_ASM_MOMENT_EINH | string | DS_LAGEINIT_PLAUSI_ASM_MOMENT Einheit: |
| STAT_DS_ZEIT_OELTEMP_KL_1_WERT | long | DS_ZEIT_OELTEMP_KL_1 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_1_EINH | string | DS_ZEIT_OELTEMP_KL_1 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_2_WERT | long | DS_ZEIT_OELTEMP_KL_2 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_2_EINH | string | DS_ZEIT_OELTEMP_KL_2 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_3_WERT | long | DS_ZEIT_OELTEMP_KL_3 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_3_EINH | string | DS_ZEIT_OELTEMP_KL_3 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_4_WERT | long | DS_ZEIT_OELTEMP_KL_4 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_4_EINH | string | DS_ZEIT_OELTEMP_KL_4 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_5_WERT | long | DS_ZEIT_OELTEMP_KL_5 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_OELTEMP_KL_5_EINH | string | DS_ZEIT_OELTEMP_KL_5 Einheit: s |
| STAT_DS_OELVERSCHLEISS_LETZT_WERT | long | DS_OELVERSCHLEISS_LETZT Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_OELVERSCHLEISS_LETZT_EINH | string | DS_OELVERSCHLEISS_LETZT Einheit: s |
| STAT_DS_ADAPTIONSWERT_AKTUELL_WERT | long | DS_ADAPTIONSWERT_AKTUELL Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_ADAPTIONSWERT_AKTUELL_EINH | string | DS_ADAPTIONSWERT_AKTUELL Einheit: 0/1 |
| STAT_DS_STEIGUNG_ANFANG_WERT | long | DS_STEIGUNG_ANFANG Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_STEIGUNG_ANFANG_EINH | string | DS_STEIGUNG_ANFANG Einheit: 0/1 |
| STAT_DS_STEIGUNG_AKTUELL_WERT | long | DS_STEIGUNG_AKTUELL Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_STEIGUNG_AKTUELL_EINH | string | DS_STEIGUNG_AKTUELL Einheit: 0/1 |
| STAT_DS_KM_LETZT_OELWECHSEL_WERT | long | DS_KM_LETZT_OELWECHSEL Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_KM_LETZT_OELWECHSEL_EINH | string | DS_KM_LETZT_OELWECHSEL Einheit: 0/1 |
| STAT_DS_ZWEIFUSSFAHRER_WERT | long | DS_ZWEIFUSSFAHRER Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZWEIFUSSFAHRER_EINH | string | DS_ZWEIFUSSFAHRER Einheit: 0/1 |
| STAT_RESERVE_WERT | long | RESERVE Bereich von 0 bis 65535 |
| STAT_RESERVE_EINH | string | RESERVE Einheit: 0/1 |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta-daten-rechts"></a>
### STATUS_FASTA_DATEN_RECHTS

FASTA_DATEN_RECHTS mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DS_ARBEIT_GESAMT_WERT | long | DS_ARBEIT_GESAMMT Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_GESAMT_EINH | string | DS_ARBEIT_GESAMMT Einheit: kJ |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_1_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_1 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_1_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_1 Einheit: s |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_2_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_2 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_2_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_2 Einheit: s |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_3_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_3 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_3_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_3 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_1_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_1 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_1_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_1 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_2_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_2 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_2_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_2 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_3_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_3 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_3_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_3 Einheit: s |
| STAT_DS_ARBEIT_OELTEMP_KL_1_WERT | long | DS_ARBEIT_OELTEMP_KL_1 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_1_EINH | string | DS_ARBEIT_OELTEMP_KL_1 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_2_WERT | long | DS_ARBEIT_OELTEMP_KL_2 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_2_EINH | string | DS_ARBEIT_OELTEMP_KL_2 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_3_WERT | long | DS_ARBEIT_OELTEMP_KL_3 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_3_EINH | string | DS_ARBEIT_OELTEMP_KL_3 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_4_WERT | long | DS_ARBEIT_OELTEMP_KL_4 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_4_EINH | string | DS_ARBEIT_OELTEMP_KL_4 Einheit: kJ |
| STAT_DS_UMDR_KL_1_1_WERT | long | DS_UMDR_KL_1_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_1_EINH | string | DS_UMDR_KL_1_1 Einheit: rpm |
| STAT_DS_UMDR_KL_2_1_WERT | long | DS_UMDR_KL_2_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_1_EINH | string | DS_UMDR_KL_2_1 Einheit: rpm |
| STAT_DS_UMDR_KL_3_1_WERT | long | DS_UMDR_KL_3_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_1_EINH | string | DS_UMDR_KL_3_1 Einheit: rpm |
| STAT_DS_UMDR_KL_4_1_WERT | long | DS_UMDR_KL_4_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_1_EINH | string | DS_UMDR_KL_4_1 Einheit: rpm |
| STAT_DS_UMDR_KL_5_1_WERT | long | DS_UMDR_KL_5_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_1_EINH | string | DS_UMDR_KL_5_1 Einheit: rpm |
| STAT_DS_UMDR_KL_6_1_WERT | long | DS_UMDR_KL_6_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_1_EINH | string | DS_UMDR_KL_6_1 Einheit: rpm |
| STAT_DS_UMDR_KL_1_2_WERT | long | DS_UMDR_KL_1_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_2_EINH | string | DS_UMDR_KL_1_2 Einheit: rpm |
| STAT_DS_UMDR_KL_2_2_WERT | long | DS_UMDR_KL_2_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_2_EINH | string | DS_UMDR_KL_2_2 Einheit: rpm |
| STAT_DS_UMDR_KL_3_2_WERT | long | DS_UMDR_KL_3_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_2_EINH | string | DS_UMDR_KL_3_2 Einheit: rpm |
| STAT_DS_UMDR_KL_4_2_WERT | long | DS_UMDR_KL_4_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_2_EINH | string | DS_UMDR_KL_4_2 Einheit: rpm |
| STAT_DS_UMDR_KL_5_2_WERT | long | DS_UMDR_KL_5_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_2_EINH | string | DS_UMDR_KL_5_2 Einheit: rpm |
| STAT_DS_UMDR_KL_6_2_WERT | long | DS_UMDR_KL_6_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_2_EINH | string | DS_UMDR_KL_6_2 Einheit: rpm |
| STAT_DS_UMDR_KL_1_3_WERT | long | DS_UMDR_KL_1_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_3_EINH | string | DS_UMDR_KL_1_3 Einheit: rpm |
| STAT_DS_UMDR_KL_2_3_WERT | long | DS_UMDR_KL_2_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_3_EINH | string | DS_UMDR_KL_2_3 Einheit: rpm |
| STAT_DS_UMDR_KL_3_3_WERT | long | DS_UMDR_KL_3_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_3_EINH | string | DS_UMDR_KL_3_3 Einheit: rpm |
| STAT_DS_UMDR_KL_4_3_WERT | long | DS_UMDR_KL_4_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_3_EINH | string | DS_UMDR_KL_4_3 Einheit: rpm |
| STAT_DS_UMDR_KL_5_3_WERT | long | DS_UMDR_KL_5_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_3_EINH | string | DS_UMDR_KL_5_3 Einheit: rpm |
| STAT_DS_UMDR_KL_6_3_WERT | long | DS_UMDR_KL_6_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_3_EINH | string | DS_UMDR_KL_6_3 Einheit: rpm |
| STAT_DS_LEISTUNG_MAX_WERT | long | DS_LEISTUNG_MAX Bereich von 0 [W] bis 65535 [W] |
| STAT_DS_LEISTUNG_MAX_EINH | string | DS_LEISTUNG_MAX Einheit: W |
| STAT_DS_GESCHW_FAHRZEUG_MAX_WERT | long | DS_GESCHW_FAHRZEUG_MAX Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_GESCHW_FAHRZEUG_MAX_EINH | string | DS_GESCHW_FAHRZEUG_MAX Einheit: km/h |
| STAT_DS_RADDIFF_GESCHW_MAX_WERT | long | DS_RADDIFF_GESCHW_MAX Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_RADDIFF_GESCHW_MAX_EINH | string | DS_RADDIFF_GESCHW_MAX Einheit: km/h |
| STAT_DS_RADDIFF_EXTREM_GESCHW_WERT | long | DS_RADDIFF_EXTREM_GESCHW Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_RADDIFF_EXTREM_GESCHW_EINH | string | DS_RADDIFF_EXTREM_GESCHW Einheit: km/h |
| STAT_DS_RADDIFF_EXTREM_KUPMOMENT_WERT | long | DS_RADDIFF_EXTREM_KUPMOMENT Bereich von -32768 [Nm] bis 32767 [Nm] |
| STAT_DS_RADDIFF_EXTREM_KUPMOMENT_EINH | string | DS_RADDIFF_EXTREM_KUPMOMENT Einheit: Nm |
| STAT_DS_ENDSTUFENSTOPS_ENDST_WERT | long | DS_ENDSTUFENSTOPS_ENDST Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_ENDST_EINH | string | DS_ENDSTUFENSTOPS_ENDST Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_MOTOR_WERT | long | DS_ENDSTUFENSTOPS_MOTOR Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_MOTOR_EINH | string | DS_ENDSTUFENSTOPS_MOTOR Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_OEL_WERT | long | DS_ENDSTUFENSTOPS_OEL Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_OEL_EINH | string | DS_ENDSTUFENSTOPS_OEL Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_LAM_WERT | long | DS_ENDSTUFENSTOPS_LAM Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_LAM_EINH | string | DS_ENDSTUFENSTOPS_LAM Einheit: 0/1 |
| STAT_DS_ADAPTIONEN_ABGESCHLOSSEN_WERT | long | DS_ADAPTIONEN_ABGESCHLOSSEN Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ADAPTIONEN_ABGESCHLOSSEN_EINH | string | DS_ADAPTIONEN_ABGESCHLOSSEN Einheit: 0/1 |
| STAT_DS_ADAPTIONEN_ABGEBROCHEN_WERT | long | DS_ADAPTIONEN_ABGEBROCHEN Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ADAPTIONEN_ABGEBROCHEN_EINH | string | DS_ADAPTIONEN_ABGEBROCHEN Einheit: 0/1 |
| STAT_DS_KILOMETERSTAND_AKTUELL_WERT | long | DS_KILOMETERSTAND_AKTUELL Bereich von 0 [km] bis 4294967295 [km] |
| STAT_DS_KILOMETERSTAND_AKTUELL_EINH | string | DS_KILOMETERSTAND_AKTUELL Einheit: km |
| STAT_DS_KILOMETERSTAND_EINBAU_WERT | long | DS_KILOMETERSTAND_EINBAU Bereich von 0 [km] bis 4294967295 [km] |
| STAT_DS_KILOMETERSTAND_EINBAU_EINH | string | DS_KILOMETERSTAND_EINBAU Einheit: km |
| STAT_DS_ZEIT_SPANNUNG_KL1_WERT | long | DS_ZEIT_SPANNUNG_KL1_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL1_EINH | string | DS_ZEIT_SPANNUNG_KL1_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL2_WERT | long | DS_ZEIT_SPANNUNG_KL2_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL2_EINH | string | DS_ZEIT_SPANNUNG_KL2_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL3_WERT | long | DS_ZEIT_SPANNUNG_KL3_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL3_EINH | string | DS_ZEIT_SPANNUNG_KL3_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL4_WERT | long | DS_ZEIT_SPANNUNG_KL4_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL4_EINH | string | DS_ZEIT_SPANNUNG_KL4_MOTOR_EIN Einheit: s |
| STAT_DS_ASM_INTEGRAL_WERT | long | DS_ASM_INTEGTRAL Bereich von 0 [Nms] bis 4294967295 [Nms] |
| STAT_DS_ASM_INTEGRAL_EINH | string | DS_ASM_INTEGTRAL Einheit: Nms |
| STAT_DS_ARBEIT_GETRIEBEVERLUST_WERT | long | DS_ARBEIT_GERTRIEBEVERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_GETRIEBEVERLUST_EINH | string | DS_ARBEIT_GERTRIEBEVERLUST Einheit: kJ |
| STAT_DS_ARBEIT_TV_VERLUST_WERT | long | DS_ARBEIT_TV_VERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_TV_VERLUST_EINH | string | DS_ARBEIT_TV_VERLUST Einheit: kJ |
| STAT_DS_KUPMOMENT_EXTREM_GESCHW_WERT | long | DS_KUPMOMENT_EXTREM_GESCHW Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_KUPMOMENT_EXTREM_GESCHW_EINH | string | DS_KUPMOMENT_EXTREM_GESCHW Einheit: km/h |
| STAT_DS_KUPMOMENT_EXTREM_KUPMOMENT_WERT | long | DS_KUPMOMENT_EXTREM_KUPMOMENT Bereich von -32768 [Nm] bis 32767 [Nm] |
| STAT_DS_KUPMOMENT_EXTREM_KUPMOMENT_EINH | string | DS_KUPMOMENT_EXTREM_KUPMOMENT Einheit: Nm |
| STAT_DS_ARBEIT_DIFFERENTIALVERLUST_WERT | long | DS_ARBEIT_DIFFERENTIALVERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_DIFFERENTIALVERLUST_EINH | string | DS_ARBEIT_DIFFERENTIALVERLUST Einheit: kJ |
| STAT_DS_ERSTADAPTIONSWERT_WERT | long | DS_ERSTADAPTIONSWERT Bereich von -32768 [°] bis 32767 [°] |
| STAT_DS_ERSTADAPTIONSWERT_EINH | string | DS_ERSTADAPTIONSWERT Einheit: ° |
| STAT_DS_MAX_ZEIT_LAGE_ZU_HOCH_WERT | long | DS_MAX_ZEIT_LAGE_ZU_HOCH Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_MAX_ZEIT_LAGE_ZU_HOCH_EINH | string | DS_MAX_ZEIT_LAGE_ZU_HOCH Einheit: ms |
| STAT_DS_MAX_ZEIT_LAGE_ZU_NIEDRIG_WERT | long | DS_MAX_ZEIT_LAGE_ZU_NIEDRIG Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_MAX_ZEIT_LAGE_ZU_NIEDRIG_EINH | string | DS_MAX_ZEIT_LAGE_ZU_NIEDRIG Einheit: ms |
| STAT_DS_ABLAGESCHEMA_WERT | long | DS_ABLAGESCHEMA Bereich von 0 [°] bis 255 [°] |
| STAT_DS_ABLAGESCHEMA_EINH | string | DS_ABLAGESCHEMA Einheit: 0/1 |
| STAT_DS_DIFFM_WERT | long | DS_DIFFM Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFM_EINH | string | DS_DIFFM Einheit: ms |
| STAT_DS_DIFFPSI_WERT | long | DS_DIFFPSI Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFPSI_EINH | string | DS_DIFFPSI Einheit: ms |
| STAT_DS_DIFFANGLE_WERT | long | DS_DIFFANGLE Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFANGLE_EINH | string | DS_DIFFANGLE Einheit: ms |
| STAT_DS_DIFFLENGTH_WERT | long | DS_DIFFLENGTH Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFLENGTH_EINH | string | DS_DIFFLENGTH Einheit: ms |
| STAT_DS_PIT01_WERT | long | DS_PIT01 Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_PIT01_EINH | string | DS_PIT01 Einheit: 0/1 |
| STAT_DS_PIT23_WERT | long | DS_PIT23 Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_PIT23_EINH | string | DS_PIT23 Einheit: 0/1 |
| STAT_DS_NUM_PLAUSI_M_ERROR_WERT | long | DS_NUM_PLAUSI_M_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_PLAUSI_M_ERROR_EINH | string | DS_NUM_PLAUSI_M_ERROR Einheit: 0/1 |
| STAT_DS_NUM_PLAUSI_PSI_ERROR_WERT | long | DS_NUM_PLAUSI_PSI_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_PLAUSI_PSI_ERROR_EINH | string | DS_NUM_PLAUSI_PSI_ERROR Einheit: 0/1 |
| STAT_DS_NUM_LENGTH_ERROR_WERT | long | DS_NUM_LENGTH_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_LENGTH_ERROR_EINH | string | DS_NUM_LENGTH_ERROR Einheit: 0/1 |
| STAT_DS_NUM_ANGLE_ERROR_WERT | long | DS_NUM_ANGLE_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_ANGLE_ERROR_EINH | string | DS_NUM_ANGLE_ERROR Einheit: 0/1 |
| STAT_DS_LAGEINIT_PLAUSI_MAX_ZEIT_WERT | long | DS_LAGEINIT_PLAUSI_MAX_ZEIT Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_LAGEINIT_PLAUSI_MAX_ZEIT_EINH | string | DS_LAGEINIT_PLAUSI_MAX_ZEIT Einheit: ms |
| STAT_DS_LAGEINIT_PLAUSI_ASM_MOMENT_WERT | long | DS_LAGEINIT_PLAUSI_ASM_MOMENT Bereich von -32768 [] bis 32767 [] |
| STAT_DS_LAGEINIT_PLAUSI_ASM_MOMENT_EINH | string | DS_LAGEINIT_PLAUSI_ASM_MOMENT Einheit: |
| STAT_DS_ZEIT_OELTEMP_KL_1_WERT | long | DS_ZEIT_OELTEMP_KL_1 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_1_EINH | string | DS_ZEIT_OELTEMP_KL_1 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_2_WERT | long | DS_ZEIT_OELTEMP_KL_2 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_2_EINH | string | DS_ZEIT_OELTEMP_KL_2 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_3_WERT | long | DS_ZEIT_OELTEMP_KL_3 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_3_EINH | string | DS_ZEIT_OELTEMP_KL_3 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_4_WERT | long | DS_ZEIT_OELTEMP_KL_4 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_4_EINH | string | DS_ZEIT_OELTEMP_KL_4 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_5_WERT | long | DS_ZEIT_OELTEMP_KL_5 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_OELTEMP_KL_5_EINH | string | DS_ZEIT_OELTEMP_KL_5 Einheit: s |
| STAT_DS_OELVERSCHLEISS_LETZT_WERT | long | DS_OELVERSCHLEISS_LETZT Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_OELVERSCHLEISS_LETZT_EINH | string | DS_OELVERSCHLEISS_LETZT Einheit: s |
| STAT_DS_ADAPTIONSWERT_AKTUELL_WERT | long | DS_ADAPTIONSWERT_AKTUELL Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_ADAPTIONSWERT_AKTUELL_EINH | string | DS_ADAPTIONSWERT_AKTUELL Einheit: 0/1 |
| STAT_DS_STEIGUNG_ANFANG_WERT | long | DS_STEIGUNG_ANFANG Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_STEIGUNG_ANFANG_EINH | string | DS_STEIGUNG_ANFANG Einheit: 0/1 |
| STAT_DS_STEIGUNG_AKTUELL_WERT | long | DS_STEIGUNG_AKTUELL Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_STEIGUNG_AKTUELL_EINH | string | DS_STEIGUNG_AKTUELL Einheit: 0/1 |
| STAT_DS_KM_LETZT_OELWECHSEL_WERT | long | DS_KM_LETZT_OELWECHSEL Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_KM_LETZT_OELWECHSEL_EINH | string | DS_KM_LETZT_OELWECHSEL Einheit: 0/1 |
| STAT_DS_ZWEIFUSSFAHRER_WERT | long | DS_ZWEIFUSSFAHRER Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZWEIFUSSFAHRER_EINH | string | DS_ZWEIFUSSFAHRER Einheit: 0/1 |
| STAT_RESERVE_WERT | long | RESERVE Bereich von 0 bis 65535 |
| STAT_RESERVE_EINH | string | RESERVE Einheit: 0/1 |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-oelverschleiss-ruecksetzen"></a>
### STEUERN_OELVERSCHLEISS_RUECKSETZEN

OELVERSCHLEISS ruecksetzen  Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-daten-getriebezustand-pu0803"></a>
### STATUS_DATEN_GETRIEBEZUSTAND_PU0803

STATUS_DATEN_GETRIEBEZUSTAND_PU0803 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KILOMETER_STAND | long | Hex-Antwort von SG |
| STAT_KUPPLUNGSREIBLEISTUNG_LINKS | long | Hex-Antwort von SG |
| STAT_KUPPLUNGSREIBLEISTUNG_RECHTS | long | Hex-Antwort von SG |
| STAT_KILOMETERSTAND_LETZT_OELWECHSEL | long | Hex-Antwort von SG |
| STAT_OELVERSCHLEISS_GEMITTELT | long | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Auftrag an SG |

<a id="job-status-fasta-daten-links-pu0803"></a>
### STATUS_FASTA_DATEN_LINKS_PU0803

FASTA_DATEN_LINKS_PU0803 mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DS_ARBEIT_GESAMT_WERT | long | DS_ARBEIT_GESAMMT Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_GESAMT_EINH | string | DS_ARBEIT_GESAMMT Einheit: kJ |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_1_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_1 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_1_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_1 Einheit: s |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_2_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_2 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_2_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_2 Einheit: s |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_3_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_3 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_3_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_3 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_1_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_1 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_1_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_1 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_2_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_2 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_2_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_2 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_3_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_3 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_3_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_3 Einheit: s |
| STAT_DS_ARBEIT_OELTEMP_KL_1_WERT | long | DS_ARBEIT_OELTEMP_KL_1 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_1_EINH | string | DS_ARBEIT_OELTEMP_KL_1 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_2_WERT | long | DS_ARBEIT_OELTEMP_KL_2 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_2_EINH | string | DS_ARBEIT_OELTEMP_KL_2 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_3_WERT | long | DS_ARBEIT_OELTEMP_KL_3 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_3_EINH | string | DS_ARBEIT_OELTEMP_KL_3 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_4_WERT | long | DS_ARBEIT_OELTEMP_KL_4 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_4_EINH | string | DS_ARBEIT_OELTEMP_KL_4 Einheit: kJ |
| STAT_DS_UMDR_KL_1_1_WERT | long | DS_UMDR_KL_1_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_1_EINH | string | DS_UMDR_KL_1_1 Einheit: rpm |
| STAT_DS_UMDR_KL_2_1_WERT | long | DS_UMDR_KL_2_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_1_EINH | string | DS_UMDR_KL_2_1 Einheit: rpm |
| STAT_DS_UMDR_KL_3_1_WERT | long | DS_UMDR_KL_3_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_1_EINH | string | DS_UMDR_KL_3_1 Einheit: rpm |
| STAT_DS_UMDR_KL_4_1_WERT | long | DS_UMDR_KL_4_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_1_EINH | string | DS_UMDR_KL_4_1 Einheit: rpm |
| STAT_DS_UMDR_KL_5_1_WERT | long | DS_UMDR_KL_5_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_1_EINH | string | DS_UMDR_KL_5_1 Einheit: rpm |
| STAT_DS_UMDR_KL_6_1_WERT | long | DS_UMDR_KL_6_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_1_EINH | string | DS_UMDR_KL_6_1 Einheit: rpm |
| STAT_DS_UMDR_KL_1_2_WERT | long | DS_UMDR_KL_1_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_2_EINH | string | DS_UMDR_KL_1_2 Einheit: rpm |
| STAT_DS_UMDR_KL_2_2_WERT | long | DS_UMDR_KL_2_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_2_EINH | string | DS_UMDR_KL_2_2 Einheit: rpm |
| STAT_DS_UMDR_KL_3_2_WERT | long | DS_UMDR_KL_3_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_2_EINH | string | DS_UMDR_KL_3_2 Einheit: rpm |
| STAT_DS_UMDR_KL_4_2_WERT | long | DS_UMDR_KL_4_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_2_EINH | string | DS_UMDR_KL_4_2 Einheit: rpm |
| STAT_DS_UMDR_KL_5_2_WERT | long | DS_UMDR_KL_5_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_2_EINH | string | DS_UMDR_KL_5_2 Einheit: rpm |
| STAT_DS_UMDR_KL_6_2_WERT | long | DS_UMDR_KL_6_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_2_EINH | string | DS_UMDR_KL_6_2 Einheit: rpm |
| STAT_DS_UMDR_KL_1_3_WERT | long | DS_UMDR_KL_1_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_3_EINH | string | DS_UMDR_KL_1_3 Einheit: rpm |
| STAT_DS_UMDR_KL_2_3_WERT | long | DS_UMDR_KL_2_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_3_EINH | string | DS_UMDR_KL_2_3 Einheit: rpm |
| STAT_DS_UMDR_KL_3_3_WERT | long | DS_UMDR_KL_3_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_3_EINH | string | DS_UMDR_KL_3_3 Einheit: rpm |
| STAT_DS_UMDR_KL_4_3_WERT | long | DS_UMDR_KL_4_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_3_EINH | string | DS_UMDR_KL_4_3 Einheit: rpm |
| STAT_DS_UMDR_KL_5_3_WERT | long | DS_UMDR_KL_5_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_3_EINH | string | DS_UMDR_KL_5_3 Einheit: rpm |
| STAT_DS_UMDR_KL_6_3_WERT | long | DS_UMDR_KL_6_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_3_EINH | string | DS_UMDR_KL_6_3 Einheit: rpm |
| STAT_DS_LEISTUNG_MAX_WERT | long | DS_LEISTUNG_MAX Bereich von 0 [W] bis 65535 [W] |
| STAT_DS_LEISTUNG_MAX_EINH | string | DS_LEISTUNG_MAX Einheit: W |
| STAT_DS_GESCHW_FAHRZEUG_MAX_WERT | long | DS_GESCHW_FAHRZEUG_MAX Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_GESCHW_FAHRZEUG_MAX_EINH | string | DS_GESCHW_FAHRZEUG_MAX Einheit: km/h |
| STAT_DS_RADDIFF_GESCHW_MAX_WERT | long | DS_RADDIFF_GESCHW_MAX Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_RADDIFF_GESCHW_MAX_EINH | string | DS_RADDIFF_GESCHW_MAX Einheit: km/h |
| STAT_DS_RADDIFF_EXTREM_GESCHW_WERT | long | DS_RADDIFF_EXTREM_GESCHW Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_RADDIFF_EXTREM_GESCHW_EINH | string | DS_RADDIFF_EXTREM_GESCHW Einheit: km/h |
| STAT_DS_RADDIFF_EXTREM_KUPMOMENT_WERT | long | DS_RADDIFF_EXTREM_KUPMOMENT Bereich von -32768 [Nm] bis 32767 [Nm] |
| STAT_DS_RADDIFF_EXTREM_KUPMOMENT_EINH | string | DS_RADDIFF_EXTREM_KUPMOMENT Einheit: Nm |
| STAT_DS_ENDSTUFENSTOPS_ENDST_WERT | long | DS_ENDSTUFENSTOPS_ENDST Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_ENDST_EINH | string | DS_ENDSTUFENSTOPS_ENDST Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_MOTOR_WERT | long | DS_ENDSTUFENSTOPS_MOTOR Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_MOTOR_EINH | string | DS_ENDSTUFENSTOPS_MOTOR Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_OEL_WERT | long | DS_ENDSTUFENSTOPS_OEL Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_OEL_EINH | string | DS_ENDSTUFENSTOPS_OEL Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_LAM_WERT | long | DS_ENDSTUFENSTOPS_LAM Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_LAM_EINH | string | DS_ENDSTUFENSTOPS_LAM Einheit: 0/1 |
| STAT_DS_ADAPTIONEN_ABGESCHLOSSEN_WERT | long | DS_ADAPTIONEN_ABGESCHLOSSEN Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ADAPTIONEN_ABGESCHLOSSEN_EINH | string | DS_ADAPTIONEN_ABGESCHLOSSEN Einheit: 0/1 |
| STAT_DS_ADAPTIONEN_ABGEBROCHEN_WERT | long | DS_ADAPTIONEN_ABGEBROCHEN Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ADAPTIONEN_ABGEBROCHEN_EINH | string | DS_ADAPTIONEN_ABGEBROCHEN Einheit: 0/1 |
| STAT_DS_KILOMETERSTAND_AKTUELL_WERT | long | DS_KILOMETERSTAND_AKTUELL Bereich von 0 [km] bis 4294967295 [km] |
| STAT_DS_KILOMETERSTAND_AKTUELL_EINH | string | DS_KILOMETERSTAND_AKTUELL Einheit: km |
| STAT_DS_KILOMETERSTAND_EINBAU_WERT | long | DS_KILOMETERSTAND_EINBAU Bereich von 0 [km] bis 4294967295 [km] |
| STAT_DS_KILOMETERSTAND_EINBAU_EINH | string | DS_KILOMETERSTAND_EINBAU Einheit: km |
| STAT_DS_ZEIT_SPANNUNG_KL1_WERT | long | DS_ZEIT_SPANNUNG_KL1_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL1_EINH | string | DS_ZEIT_SPANNUNG_KL1_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL2_WERT | long | DS_ZEIT_SPANNUNG_KL2_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL2_EINH | string | DS_ZEIT_SPANNUNG_KL2_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL3_WERT | long | DS_ZEIT_SPANNUNG_KL3_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL3_EINH | string | DS_ZEIT_SPANNUNG_KL3_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL4_WERT | long | DS_ZEIT_SPANNUNG_KL4_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL4_EINH | string | DS_ZEIT_SPANNUNG_KL4_MOTOR_EIN Einheit: s |
| STAT_DS_ASM_INTEGRAL_WERT | long | DS_ASM_INTEGTRAL Bereich von 0 [Nms] bis 4294967295 [Nms] |
| STAT_DS_ASM_INTEGRAL_EINH | string | DS_ASM_INTEGTRAL Einheit: Nms |
| STAT_DS_ARBEIT_GETRIEBEVERLUST_WERT | long | DS_ARBEIT_GERTRIEBEVERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_GETRIEBEVERLUST_EINH | string | DS_ARBEIT_GERTRIEBEVERLUST Einheit: kJ |
| STAT_DS_ARBEIT_TV_VERLUST_WERT | long | DS_ARBEIT_TV_VERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_TV_VERLUST_EINH | string | DS_ARBEIT_TV_VERLUST Einheit: kJ |
| STAT_DS_KUPMOMENT_EXTREM_GESCHW_WERT | long | DS_KUPMOMENT_EXTREM_GESCHW Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_KUPMOMENT_EXTREM_GESCHW_EINH | string | DS_KUPMOMENT_EXTREM_GESCHW Einheit: km/h |
| STAT_DS_KUPMOMENT_EXTREM_KUPMOMENT_WERT | long | DS_KUPMOMENT_EXTREM_KUPMOMENT Bereich von -32768 [Nm] bis 32767 [Nm] |
| STAT_DS_KUPMOMENT_EXTREM_KUPMOMENT_EINH | string | DS_KUPMOMENT_EXTREM_KUPMOMENT Einheit: Nm |
| STAT_DS_ARBEIT_DIFFERENTIALVERLUST_WERT | long | DS_ARBEIT_DIFFERENTIALVERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_DIFFERENTIALVERLUST_EINH | string | DS_ARBEIT_DIFFERENTIALVERLUST Einheit: kJ |
| STAT_DS_ERSTADAPTIONSWERT_WERT | long | DS_ERSTADAPTIONSWERT Bereich von -32768 [°] bis 32767 [°] |
| STAT_DS_ERSTADAPTIONSWERT_EINH | string | DS_ERSTADAPTIONSWERT Einheit: ° |
| STAT_DS_MAX_ZEIT_LAGE_ZU_HOCH_WERT | long | DS_MAX_ZEIT_LAGE_ZU_HOCH Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_MAX_ZEIT_LAGE_ZU_HOCH_EINH | string | DS_MAX_ZEIT_LAGE_ZU_HOCH Einheit: ms |
| STAT_DS_MAX_ZEIT_LAGE_ZU_NIEDRIG_WERT | long | DS_MAX_ZEIT_LAGE_ZU_NIEDRIG Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_MAX_ZEIT_LAGE_ZU_NIEDRIG_EINH | string | DS_MAX_ZEIT_LAGE_ZU_NIEDRIG Einheit: ms |
| STAT_DS_ABLAGESCHEMA_WERT | long | DS_ABLAGESCHEMA Bereich von 0 [°] bis 255 [°] |
| STAT_DS_ABLAGESCHEMA_EINH | string | DS_ABLAGESCHEMA Einheit: 0/1 |
| STAT_DS_DIFFM_WERT | long | DS_DIFFM Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFM_EINH | string | DS_DIFFM Einheit: ms |
| STAT_DS_DIFFPSI_WERT | long | DS_DIFFPSI Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFPSI_EINH | string | DS_DIFFPSI Einheit: ms |
| STAT_DS_DIFFANGLE_WERT | long | DS_DIFFANGLE Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFANGLE_EINH | string | DS_DIFFANGLE Einheit: ms |
| STAT_DS_DIFFLENGTH_WERT | long | DS_DIFFLENGTH Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFLENGTH_EINH | string | DS_DIFFLENGTH Einheit: ms |
| STAT_DS_PIT01_WERT | long | DS_PIT01 Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_PIT01_EINH | string | DS_PIT01 Einheit: 0/1 |
| STAT_DS_PIT23_WERT | long | DS_PIT23 Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_PIT23_EINH | string | DS_PIT23 Einheit: 0/1 |
| STAT_DS_NUM_PLAUSI_M_ERROR_WERT | long | DS_NUM_PLAUSI_M_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_PLAUSI_M_ERROR_EINH | string | DS_NUM_PLAUSI_M_ERROR Einheit: 0/1 |
| STAT_DS_NUM_PLAUSI_PSI_ERROR_WERT | long | DS_NUM_PLAUSI_PSI_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_PLAUSI_PSI_ERROR_EINH | string | DS_NUM_PLAUSI_PSI_ERROR Einheit: 0/1 |
| STAT_DS_NUM_LENGTH_ERROR_WERT | long | DS_NUM_LENGTH_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_LENGTH_ERROR_EINH | string | DS_NUM_LENGTH_ERROR Einheit: 0/1 |
| STAT_DS_NUM_ANGLE_ERROR_WERT | long | DS_NUM_ANGLE_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_ANGLE_ERROR_EINH | string | DS_NUM_ANGLE_ERROR Einheit: 0/1 |
| STAT_DS_LAGEINIT_PLAUSI_MAX_ZEIT_WERT | long | DS_LAGEINIT_PLAUSI_MAX_ZEIT Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_LAGEINIT_PLAUSI_MAX_ZEIT_EINH | string | DS_LAGEINIT_PLAUSI_MAX_ZEIT Einheit: ms |
| STAT_DS_LAGEINIT_PLAUSI_ASM_MOMENT_WERT | long | DS_LAGEINIT_PLAUSI_ASM_MOMENT Bereich von -32768 [] bis 32767 [] |
| STAT_DS_LAGEINIT_PLAUSI_ASM_MOMENT_EINH | string | DS_LAGEINIT_PLAUSI_ASM_MOMENT Einheit: |
| STAT_DS_ZEIT_OELTEMP_KL_1_WERT | long | DS_ZEIT_OELTEMP_KL_1 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_1_EINH | string | DS_ZEIT_OELTEMP_KL_1 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_2_WERT | long | DS_ZEIT_OELTEMP_KL_2 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_2_EINH | string | DS_ZEIT_OELTEMP_KL_2 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_3_WERT | long | DS_ZEIT_OELTEMP_KL_3 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_3_EINH | string | DS_ZEIT_OELTEMP_KL_3 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_4_WERT | long | DS_ZEIT_OELTEMP_KL_4 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_4_EINH | string | DS_ZEIT_OELTEMP_KL_4 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_5_WERT | long | DS_ZEIT_OELTEMP_KL_5 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_OELTEMP_KL_5_EINH | string | DS_ZEIT_OELTEMP_KL_5 Einheit: s |
| STAT_DS_OELVERSCHLEISS_LETZT_WERT | long | DS_OELVERSCHLEISS_LETZT Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_OELVERSCHLEISS_LETZT_EINH | string | DS_OELVERSCHLEISS_LETZT Einheit: s |
| STAT_DS_ADAPTIONSWERT_AKTUELL_WERT | long | DS_ADAPTIONSWERT_AKTUELL Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_ADAPTIONSWERT_AKTUELL_EINH | string | DS_ADAPTIONSWERT_AKTUELL Einheit: 0/1 |
| STAT_DS_STEIGUNG_ANFANG_WERT | long | DS_STEIGUNG_ANFANG Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_STEIGUNG_ANFANG_EINH | string | DS_STEIGUNG_ANFANG Einheit: 0/1 |
| STAT_DS_STEIGUNG_AKTUELL_WERT | long | DS_STEIGUNG_AKTUELL Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_STEIGUNG_AKTUELL_EINH | string | DS_STEIGUNG_AKTUELL Einheit: 0/1 |
| STAT_DS_KM_LETZT_OELWECHSEL_WERT | long | DS_KM_LETZT_OELWECHSEL Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_KM_LETZT_OELWECHSEL_EINH | string | DS_KM_LETZT_OELWECHSEL Einheit: 0/1 |
| STAT_DS_ZWEIFUSSFAHRER_WERT | long | DS_ZWEIFUSSFAHRER Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZWEIFUSSFAHRER_EINH | string | DS_ZWEIFUSSFAHRER Einheit: 0/1 |
| STAT_DS_OELVERSCHLEISS_WERT | long | RESERVE Bereich von 0 bis 65535 |
| STAT_DS_OELVERSCHLEISS_EINH | string | RESERVE Einheit: 0/1 |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta-daten-rechts-pu0803"></a>
### STATUS_FASTA_DATEN_RECHTS_PU0803

FASTA_DATEN_RECHTS_PU0803 mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DS_ARBEIT_GESAMT_WERT | long | DS_ARBEIT_GESAMMT Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_GESAMT_EINH | string | DS_ARBEIT_GESAMMT Einheit: kJ |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_1_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_1 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_1_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_1 Einheit: s |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_2_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_2 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_2_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_2 Einheit: s |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_3_WERT | long | DS_ZEIT_EINDR_LEISTUNG_KL_3 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_EINDR_LEISTUNG_KL_3_EINH | string | DS_ZEIT_EINDR_LEISTUNG_KL_3 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_1_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_1 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_1_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_1 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_2_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_2 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_2_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_2 Einheit: s |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_3_WERT | long | DS_ZEIT_AUSDR_LEISTUNG_KL_3 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_AUSDR_LEISTUNG_KL_3_EINH | string | DS_ZEIT_AUSDR_LEISTUNG_KL_3 Einheit: s |
| STAT_DS_ARBEIT_OELTEMP_KL_1_WERT | long | DS_ARBEIT_OELTEMP_KL_1 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_1_EINH | string | DS_ARBEIT_OELTEMP_KL_1 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_2_WERT | long | DS_ARBEIT_OELTEMP_KL_2 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_2_EINH | string | DS_ARBEIT_OELTEMP_KL_2 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_3_WERT | long | DS_ARBEIT_OELTEMP_KL_3 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_3_EINH | string | DS_ARBEIT_OELTEMP_KL_3 Einheit: kJ |
| STAT_DS_ARBEIT_OELTEMP_KL_4_WERT | long | DS_ARBEIT_OELTEMP_KL_4 Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_OELTEMP_KL_4_EINH | string | DS_ARBEIT_OELTEMP_KL_4 Einheit: kJ |
| STAT_DS_UMDR_KL_1_1_WERT | long | DS_UMDR_KL_1_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_1_EINH | string | DS_UMDR_KL_1_1 Einheit: rpm |
| STAT_DS_UMDR_KL_2_1_WERT | long | DS_UMDR_KL_2_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_1_EINH | string | DS_UMDR_KL_2_1 Einheit: rpm |
| STAT_DS_UMDR_KL_3_1_WERT | long | DS_UMDR_KL_3_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_1_EINH | string | DS_UMDR_KL_3_1 Einheit: rpm |
| STAT_DS_UMDR_KL_4_1_WERT | long | DS_UMDR_KL_4_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_1_EINH | string | DS_UMDR_KL_4_1 Einheit: rpm |
| STAT_DS_UMDR_KL_5_1_WERT | long | DS_UMDR_KL_5_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_1_EINH | string | DS_UMDR_KL_5_1 Einheit: rpm |
| STAT_DS_UMDR_KL_6_1_WERT | long | DS_UMDR_KL_6_1 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_1_EINH | string | DS_UMDR_KL_6_1 Einheit: rpm |
| STAT_DS_UMDR_KL_1_2_WERT | long | DS_UMDR_KL_1_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_2_EINH | string | DS_UMDR_KL_1_2 Einheit: rpm |
| STAT_DS_UMDR_KL_2_2_WERT | long | DS_UMDR_KL_2_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_2_EINH | string | DS_UMDR_KL_2_2 Einheit: rpm |
| STAT_DS_UMDR_KL_3_2_WERT | long | DS_UMDR_KL_3_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_2_EINH | string | DS_UMDR_KL_3_2 Einheit: rpm |
| STAT_DS_UMDR_KL_4_2_WERT | long | DS_UMDR_KL_4_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_2_EINH | string | DS_UMDR_KL_4_2 Einheit: rpm |
| STAT_DS_UMDR_KL_5_2_WERT | long | DS_UMDR_KL_5_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_2_EINH | string | DS_UMDR_KL_5_2 Einheit: rpm |
| STAT_DS_UMDR_KL_6_2_WERT | long | DS_UMDR_KL_6_2 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_2_EINH | string | DS_UMDR_KL_6_2 Einheit: rpm |
| STAT_DS_UMDR_KL_1_3_WERT | long | DS_UMDR_KL_1_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_1_3_EINH | string | DS_UMDR_KL_1_3 Einheit: rpm |
| STAT_DS_UMDR_KL_2_3_WERT | long | DS_UMDR_KL_2_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_2_3_EINH | string | DS_UMDR_KL_2_3 Einheit: rpm |
| STAT_DS_UMDR_KL_3_3_WERT | long | DS_UMDR_KL_3_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_3_3_EINH | string | DS_UMDR_KL_3_3 Einheit: rpm |
| STAT_DS_UMDR_KL_4_3_WERT | long | DS_UMDR_KL_4_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_4_3_EINH | string | DS_UMDR_KL_4_3 Einheit: rpm |
| STAT_DS_UMDR_KL_5_3_WERT | long | DS_UMDR_KL_5_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_5_3_EINH | string | DS_UMDR_KL_5_3 Einheit: rpm |
| STAT_DS_UMDR_KL_6_3_WERT | long | DS_UMDR_KL_6_3 Bereich von 0 [rpm] bis 4294967295 [rpm] |
| STAT_DS_UMDR_KL_6_3_EINH | string | DS_UMDR_KL_6_3 Einheit: rpm |
| STAT_DS_LEISTUNG_MAX_WERT | long | DS_LEISTUNG_MAX Bereich von 0 [W] bis 65535 [W] |
| STAT_DS_LEISTUNG_MAX_EINH | string | DS_LEISTUNG_MAX Einheit: W |
| STAT_DS_GESCHW_FAHRZEUG_MAX_WERT | long | DS_GESCHW_FAHRZEUG_MAX Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_GESCHW_FAHRZEUG_MAX_EINH | string | DS_GESCHW_FAHRZEUG_MAX Einheit: km/h |
| STAT_DS_RADDIFF_GESCHW_MAX_WERT | long | DS_RADDIFF_GESCHW_MAX Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_RADDIFF_GESCHW_MAX_EINH | string | DS_RADDIFF_GESCHW_MAX Einheit: km/h |
| STAT_DS_RADDIFF_EXTREM_GESCHW_WERT | long | DS_RADDIFF_EXTREM_GESCHW Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_RADDIFF_EXTREM_GESCHW_EINH | string | DS_RADDIFF_EXTREM_GESCHW Einheit: km/h |
| STAT_DS_RADDIFF_EXTREM_KUPMOMENT_WERT | long | DS_RADDIFF_EXTREM_KUPMOMENT Bereich von -32768 [Nm] bis 32767 [Nm] |
| STAT_DS_RADDIFF_EXTREM_KUPMOMENT_EINH | string | DS_RADDIFF_EXTREM_KUPMOMENT Einheit: Nm |
| STAT_DS_ENDSTUFENSTOPS_ENDST_WERT | long | DS_ENDSTUFENSTOPS_ENDST Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_ENDST_EINH | string | DS_ENDSTUFENSTOPS_ENDST Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_MOTOR_WERT | long | DS_ENDSTUFENSTOPS_MOTOR Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_MOTOR_EINH | string | DS_ENDSTUFENSTOPS_MOTOR Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_OEL_WERT | long | DS_ENDSTUFENSTOPS_OEL Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_OEL_EINH | string | DS_ENDSTUFENSTOPS_OEL Einheit: 0/1 |
| STAT_DS_ENDSTUFENSTOPS_LAM_WERT | long | DS_ENDSTUFENSTOPS_LAM Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ENDSTUFENSTOPS_LAM_EINH | string | DS_ENDSTUFENSTOPS_LAM Einheit: 0/1 |
| STAT_DS_ADAPTIONEN_ABGESCHLOSSEN_WERT | long | DS_ADAPTIONEN_ABGESCHLOSSEN Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ADAPTIONEN_ABGESCHLOSSEN_EINH | string | DS_ADAPTIONEN_ABGESCHLOSSEN Einheit: 0/1 |
| STAT_DS_ADAPTIONEN_ABGEBROCHEN_WERT | long | DS_ADAPTIONEN_ABGEBROCHEN Bereich von 0 [0/1] bis 65535 [0/1] |
| STAT_DS_ADAPTIONEN_ABGEBROCHEN_EINH | string | DS_ADAPTIONEN_ABGEBROCHEN Einheit: 0/1 |
| STAT_DS_KILOMETERSTAND_AKTUELL_WERT | long | DS_KILOMETERSTAND_AKTUELL Bereich von 0 [km] bis 4294967295 [km] |
| STAT_DS_KILOMETERSTAND_AKTUELL_EINH | string | DS_KILOMETERSTAND_AKTUELL Einheit: km |
| STAT_DS_KILOMETERSTAND_EINBAU_WERT | long | DS_KILOMETERSTAND_EINBAU Bereich von 0 [km] bis 4294967295 [km] |
| STAT_DS_KILOMETERSTAND_EINBAU_EINH | string | DS_KILOMETERSTAND_EINBAU Einheit: km |
| STAT_DS_ZEIT_SPANNUNG_KL1_WERT | long | DS_ZEIT_SPANNUNG_KL1_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL1_EINH | string | DS_ZEIT_SPANNUNG_KL1_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL2_WERT | long | DS_ZEIT_SPANNUNG_KL2_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL2_EINH | string | DS_ZEIT_SPANNUNG_KL2_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL3_WERT | long | DS_ZEIT_SPANNUNG_KL3_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL3_EINH | string | DS_ZEIT_SPANNUNG_KL3_MOTOR_EIN Einheit: s |
| STAT_DS_ZEIT_SPANNUNG_KL4_WERT | long | DS_ZEIT_SPANNUNG_KL4_MOTOR_EIN Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_SPANNUNG_KL4_EINH | string | DS_ZEIT_SPANNUNG_KL4_MOTOR_EIN Einheit: s |
| STAT_DS_ASM_INTEGRAL_WERT | long | DS_ASM_INTEGTRAL Bereich von 0 [Nms] bis 4294967295 [Nms] |
| STAT_DS_ASM_INTEGRAL_EINH | string | DS_ASM_INTEGTRAL Einheit: Nms |
| STAT_DS_ARBEIT_GETRIEBEVERLUST_WERT | long | DS_ARBEIT_GERTRIEBEVERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_GETRIEBEVERLUST_EINH | string | DS_ARBEIT_GERTRIEBEVERLUST Einheit: kJ |
| STAT_DS_ARBEIT_TV_VERLUST_WERT | long | DS_ARBEIT_TV_VERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_TV_VERLUST_EINH | string | DS_ARBEIT_TV_VERLUST Einheit: kJ |
| STAT_DS_KUPMOMENT_EXTREM_GESCHW_WERT | long | DS_KUPMOMENT_EXTREM_GESCHW Bereich von -32768 [km/h] bis 32767 [km/h] |
| STAT_DS_KUPMOMENT_EXTREM_GESCHW_EINH | string | DS_KUPMOMENT_EXTREM_GESCHW Einheit: km/h |
| STAT_DS_KUPMOMENT_EXTREM_KUPMOMENT_WERT | long | DS_KUPMOMENT_EXTREM_KUPMOMENT Bereich von -32768 [Nm] bis 32767 [Nm] |
| STAT_DS_KUPMOMENT_EXTREM_KUPMOMENT_EINH | string | DS_KUPMOMENT_EXTREM_KUPMOMENT Einheit: Nm |
| STAT_DS_ARBEIT_DIFFERENTIALVERLUST_WERT | long | DS_ARBEIT_DIFFERENTIALVERLUST Bereich von 0 [kJ] bis 4294967295 [kJ] |
| STAT_DS_ARBEIT_DIFFERENTIALVERLUST_EINH | string | DS_ARBEIT_DIFFERENTIALVERLUST Einheit: kJ |
| STAT_DS_ERSTADAPTIONSWERT_WERT | long | DS_ERSTADAPTIONSWERT Bereich von -32768 [°] bis 32767 [°] |
| STAT_DS_ERSTADAPTIONSWERT_EINH | string | DS_ERSTADAPTIONSWERT Einheit: ° |
| STAT_DS_MAX_ZEIT_LAGE_ZU_HOCH_WERT | long | DS_MAX_ZEIT_LAGE_ZU_HOCH Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_MAX_ZEIT_LAGE_ZU_HOCH_EINH | string | DS_MAX_ZEIT_LAGE_ZU_HOCH Einheit: ms |
| STAT_DS_MAX_ZEIT_LAGE_ZU_NIEDRIG_WERT | long | DS_MAX_ZEIT_LAGE_ZU_NIEDRIG Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_MAX_ZEIT_LAGE_ZU_NIEDRIG_EINH | string | DS_MAX_ZEIT_LAGE_ZU_NIEDRIG Einheit: ms |
| STAT_DS_ABLAGESCHEMA_WERT | long | DS_ABLAGESCHEMA Bereich von 0 [°] bis 255 [°] |
| STAT_DS_ABLAGESCHEMA_EINH | string | DS_ABLAGESCHEMA Einheit: 0/1 |
| STAT_DS_DIFFM_WERT | long | DS_DIFFM Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFM_EINH | string | DS_DIFFM Einheit: ms |
| STAT_DS_DIFFPSI_WERT | long | DS_DIFFPSI Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFPSI_EINH | string | DS_DIFFPSI Einheit: ms |
| STAT_DS_DIFFANGLE_WERT | long | DS_DIFFANGLE Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFANGLE_EINH | string | DS_DIFFANGLE Einheit: ms |
| STAT_DS_DIFFLENGTH_WERT | long | DS_DIFFLENGTH Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_DIFFLENGTH_EINH | string | DS_DIFFLENGTH Einheit: ms |
| STAT_DS_PIT01_WERT | long | DS_PIT01 Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_PIT01_EINH | string | DS_PIT01 Einheit: 0/1 |
| STAT_DS_PIT23_WERT | long | DS_PIT23 Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_PIT23_EINH | string | DS_PIT23 Einheit: 0/1 |
| STAT_DS_NUM_PLAUSI_M_ERROR_WERT | long | DS_NUM_PLAUSI_M_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_PLAUSI_M_ERROR_EINH | string | DS_NUM_PLAUSI_M_ERROR Einheit: 0/1 |
| STAT_DS_NUM_PLAUSI_PSI_ERROR_WERT | long | DS_NUM_PLAUSI_PSI_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_PLAUSI_PSI_ERROR_EINH | string | DS_NUM_PLAUSI_PSI_ERROR Einheit: 0/1 |
| STAT_DS_NUM_LENGTH_ERROR_WERT | long | DS_NUM_LENGTH_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_LENGTH_ERROR_EINH | string | DS_NUM_LENGTH_ERROR Einheit: 0/1 |
| STAT_DS_NUM_ANGLE_ERROR_WERT | long | DS_NUM_ANGLE_ERROR Bereich von 0 [0/1] bis 255 [0/1] |
| STAT_DS_NUM_ANGLE_ERROR_EINH | string | DS_NUM_ANGLE_ERROR Einheit: 0/1 |
| STAT_DS_LAGEINIT_PLAUSI_MAX_ZEIT_WERT | long | DS_LAGEINIT_PLAUSI_MAX_ZEIT Bereich von 0 [ms] bis 255 [ms] |
| STAT_DS_LAGEINIT_PLAUSI_MAX_ZEIT_EINH | string | DS_LAGEINIT_PLAUSI_MAX_ZEIT Einheit: ms |
| STAT_DS_LAGEINIT_PLAUSI_ASM_MOMENT_WERT | long | DS_LAGEINIT_PLAUSI_ASM_MOMENT Bereich von -32768 [] bis 32767 [] |
| STAT_DS_LAGEINIT_PLAUSI_ASM_MOMENT_EINH | string | DS_LAGEINIT_PLAUSI_ASM_MOMENT Einheit: |
| STAT_DS_ZEIT_OELTEMP_KL_1_WERT | long | DS_ZEIT_OELTEMP_KL_1 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_1_EINH | string | DS_ZEIT_OELTEMP_KL_1 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_2_WERT | long | DS_ZEIT_OELTEMP_KL_2 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_2_EINH | string | DS_ZEIT_OELTEMP_KL_2 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_3_WERT | long | DS_ZEIT_OELTEMP_KL_3 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_3_EINH | string | DS_ZEIT_OELTEMP_KL_3 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_4_WERT | long | DS_ZEIT_OELTEMP_KL_4 Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZEIT_OELTEMP_KL_4_EINH | string | DS_ZEIT_OELTEMP_KL_4 Einheit: 0/1 |
| STAT_DS_ZEIT_OELTEMP_KL_5_WERT | long | DS_ZEIT_OELTEMP_KL_5 Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_ZEIT_OELTEMP_KL_5_EINH | string | DS_ZEIT_OELTEMP_KL_5 Einheit: s |
| STAT_DS_OELVERSCHLEISS_LETZT_WERT | long | DS_OELVERSCHLEISS_LETZT Bereich von 0 [s] bis 4294967295 [s] |
| STAT_DS_OELVERSCHLEISS_LETZT_EINH | string | DS_OELVERSCHLEISS_LETZT Einheit: s |
| STAT_DS_ADAPTIONSWERT_AKTUELL_WERT | long | DS_ADAPTIONSWERT_AKTUELL Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_ADAPTIONSWERT_AKTUELL_EINH | string | DS_ADAPTIONSWERT_AKTUELL Einheit: 0/1 |
| STAT_DS_STEIGUNG_ANFANG_WERT | long | DS_STEIGUNG_ANFANG Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_STEIGUNG_ANFANG_EINH | string | DS_STEIGUNG_ANFANG Einheit: 0/1 |
| STAT_DS_STEIGUNG_AKTUELL_WERT | long | DS_STEIGUNG_AKTUELL Bereich von -32768 [0/1] bis 32767 [0/1] |
| STAT_DS_STEIGUNG_AKTUELL_EINH | string | DS_STEIGUNG_AKTUELL Einheit: 0/1 |
| STAT_DS_KM_LETZT_OELWECHSEL_WERT | long | DS_KM_LETZT_OELWECHSEL Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_KM_LETZT_OELWECHSEL_EINH | string | DS_KM_LETZT_OELWECHSEL Einheit: 0/1 |
| STAT_DS_ZWEIFUSSFAHRER_WERT | long | DS_ZWEIFUSSFAHRER Bereich von 0 [0/1] bis 4294967295 [0/1] |
| STAT_DS_ZWEIFUSSFAHRER_EINH | string | DS_ZWEIFUSSFAHRER Einheit: 0/1 |
| STAT_DS_OELVERSCHLEISS_WERT | long | RESERVE Bereich von 0 bis 65535 |
| STAT_DS_OELVERSCHLEISS_EINH | string | RESERVE Einheit: 0/1 |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-getriebezustand-pu0803"></a>
### STEUERN_GETRIEBEZUSTAND_PU0803

Getriebzustand steuern_PU0803 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KM | long | Vorgabe Km Range: 16777215 |
| KUPPLUNGSREIBLEISTUNG_LINKS | long | tbd Range: tbd |
| KUPPLUNGSREIBLEISTUNG_RECHTS | long | tbd Range: tbd |
| KILOMETERSTAND_LETZT_OELWECHSEL | long | tbd Range: tbd |
| OELVERSCHLEISS_GEMITTELT | long | tbd Range: tbd |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (59 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (30 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (69 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (30 × 9)
- [ENVANALOGSET1](#table-envanalogset1) (1 × 17)
- [ENVTEMPERATURE](#table-envtemperature) (121 × 2)
- [ENVVOLTAGE](#table-envvoltage) (31 × 2)
- [ENVDISCRSET1](#table-envdiscrset1) (1 × 5)
- [ENVDISCRSET2](#table-envdiscrset2) (1 × 9)
- [ENVDISCRSET3](#table-envdiscrset3) (1 × 3)
- [STAT_ADAPTION_LINKS](#table-stat-adaption-links) (4 × 2)
- [STAT_ADAPTION_RECHTS](#table-stat-adaption-rechts) (4 × 2)
- [STAT_VERFUEGBARKEIT_TV_XXX](#table-stat-verfuegbarkeit-tv-xxx) (16 × 2)
- [STAT_FUNKTIONEN_1](#table-stat-funktionen-1) (5 × 2)
- [STAT_FUNKTIONEN_2](#table-stat-funktionen-2) (4 × 2)
- [ENVSTATUS1](#table-envstatus1) (31 × 2)
- [ENVSTATUS3](#table-envstatus3) (61 × 2)
- [STAT_QSG_SERVICEQUALIFIER](#table-stat-qsg-servicequalifier) (21 × 2)
- [ENVSTATUS2](#table-envstatus2) (256 × 2)

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
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 59 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5848 | Steuergerät: Interner ECU Fehler |
| 0x5849 | Versorgungsspannung zu niedrig |
| 0x584A | Versorgungsspannung zu hoch |
| 0x584B | Digitale Klemme 15 und CAN Klemme 15 nicht plausibel |
| 0x5860 | Öltemperatursensor Momenten-Stelleinheit links Kurzschluss nach Masse |
| 0x5861 | Öltemperatursensor Momenten-Stelleinheit links Kurzschluss Plus oder Leitungsunterbrechung |
| 0x5863 | Öltemperatursensor Momenten-Stelleinheit rechts Kurzschluss nach Masse |
| 0x5864 | Öltemperatursensor Momenten-Stelleinheit rechts Kurzschluss Plus oder Leitungsunterbrechung |
| 0x5880 | Motorlagesensor Momenten-Stelleinheit links Versorgungsspannung Kurzschluss Masse oder Unterspannung |
| 0x5881 | Motorlagesensor Momenten-Stelleinheit links Versorgungsspannung Kurzschluss Plus |
| 0x5882 | Motorlagesensor Momenten-Stelleinheit rechts Versorgungsspannung Kurzschluss Masse oder Unterspannung |
| 0x5883 | Motorlagesensor Momenten-Stelleinheit rechts Versorgungsspannung Kurzschluss Plus |
| 0x5885 | Motorlagesensor Momenten-Stelleinheit links Signalverlust |
| 0x5886 | Motorlagesensor Momenten-Stelleinheit links Signalfehler |
| 0x5889 | Motorlagesensor Momenten-Stelleinheit rechts Signalverlust |
| 0x588A | Motorlagesensor Momenten-Stelleinheit rechts Signalfehler |
| 0x58A0 | Temperatursensor Stellmotor links Kurzschluss Masse |
| 0x58A1 | Temperatursensor Stellmotor links Kurzschluss Plus oder Leitungsunterbrechung |
| 0x58A3 | Temperatursensor Stellmotor rechts Kurzschluss Masse |
| 0x58A4 | Temperatursensor Stellmotor rechts Kurzschluss Plus oder Leitungsunterbrechung |
| 0x58A6 | Stellmotor Momenten-Stelleinheit links Phase U, V, W Kurzschluss Plus |
| 0x58A7 | Stellmotor Momenten-Stelleinheit links  Phase U, V, W Kurzschluss Masse |
| 0x58A8 | Stellmotor Momenten-Stelleinheit links  Phase U, V, W Leitungsunterbrechung |
| 0x58A9 | Stellmotoransteuerung links Elektrischer Fehler |
| 0x58AF | Stellmotor Momenten-Stelleinheit rechts Phase U, V, W Kurzschluss Plus |
| 0x58B0 | Stellmotor Momenten-Stelleinheit rechts U, V, W Kurzschluss Masse |
| 0x58B1 | Stellmotor Momenten-Stelleinheit rechts U, V, W Leitungsunterbrechung |
| 0x58B2 | Stellmotoransteuerung rechts Elektrischer Fehler |
| 0x58E2 | Ölalterung |
| 0x57E4 | Adaption ungültig |
| 0x57E6 | Signal Motorlagesensor Daten ungültig |
| 0x57F0 | Signal Motorlagesensor Daten ungültig links |
| 0x57F1 | Signal Motorlagesensor Daten ungültig  rechts |
| 0x57E7 | Signal von der DSC Raddrehzahl unplausibel |
| 0x57E9 | Sollmomentenvorgabe vom ICM unplausibel |
| 0x57EA | Programmierbedingungen nicht erfüllt |
| 0x57EB | Verschleisende erreicht links |
| 0x57EC | Verschleisende erreicht rechts |
| 0x57ED | Mechanischer Fehler links |
| 0x57EE | Mechanischer Fehler rechts |
| 0xCCCB | ICM CAN Kommunikationsfehler |
| 0xCCCF | PT CAN Kommunikationsfehler |
| 0xCCE2 | Botschaft ( Sollmomentenvorgabe , ICM-CAN) von ICM fehlt |
| 0xCCE3 | Botschaft ( Sollmomentenvorgabe , ICM-CAN) von ICM nicht aktuell |
| 0xCCE4 | Botschaft ( Sollmomentenvorgabe , ICM-CAN) von ICM fehlerhaft |
| 0xCCE5 | Botschaft  ( Drehmoment 1, PT-CAN) von Motorsteuerung fehlt |
| 0xCCE6 | Botschaft ( Drehmoment 3, PT-CAN) von Motorsteuerung fehlt |
| 0xCCE7 | Botschaft ( Geschwindigkeit Rad, PT-CAN) von der DSC fehlt |
| 0xCCE8 | Botschaft ( Lenkradwinkel , PT-CAN) von DSC fehlt |
| 0xCCE9 | Botschaft ( Klemmenstatus , PT-CAN) von CAS fehlt |
| 0xCCEA | Botschaft  ( Status DSC, PT-CAN) von DSC fehlt |
| 0xCCEB | Botschaft ( Getriebedaten 2, PT-CAN) von EGS fehlt |
| 0xCCEC | Botschaft ( Uhrzeit - Datum , PT-CAN) von Kombiinstrument fehlt |
| 0xCCED | Botschaft ( Kilometerstand , PT-CAN) von Kombiinstrument fehlt |
| 0xCCEE | Botschaft (Powermanagement-Batteriespannung , PT-CAN) von Motorsteuerung fehlt |
| 0xCCEF | Botschaft ( Daten DSC, ICM-CAN) von ICM fehlt |
| 0xCCF0 | Botschaft ( Daten DSC, ICM-CAN) von ICM nicht aktuell |
| 0xCCF1 | Botschaft  ( Daten DSC, ICM-CAN) von ICM fehlerhaft |
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
| default | EnvAnalogSet1 | EnvDiscrSet1 | EnvDiscrSet2 | EnvDiscrSet3 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 30 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Batteriespannung links | V | - | unsigned char | - | 1 | 10 | 0 |
| 2 | Angefordertes TV Moment | Nm | - | unsigned char | - | 20 | 1 | -2500 |
| 3 | Aktuelles TV Moment | Nm | - | unsigned char | - | 20 | 1 | -2500 |
| 4 | Betriebsart Koordinator | hex | - | unsigned char | - | 1 | 1 | 0 |
| 5 | Aktuelle Position links | Grad | high | unsigned int | - | 1 | 2 | -5000 |
| 6 | Aktuelle Position rechts | Grad | high | unsigned int | - | 1 | 2 | -5000 |
| 7 | Aktuelles Moment Motor links | mNm | - | unsigned char | - | 2 | 1 | -250 |
| 8 | Aktuelles Moment Motor rechts | mNm | - | unsigned char | - | 2 | 1 | -250 |
| 9 | Raddrehzahl HL | km/h | - | unsigned char | - | 2 | 1 | -200 |
| 10 | Raddrehzahl HR | km/h | - | unsigned char | - | 2 | 1 | -200 |
| 11 | Drehzahl Motor | U/min | - | unsigned char | - | 50 | 1 | 0 |
| 12 | Reserviert | - | - | unsigned char | - | 1 | 1 | 0 |
| 13 | Reserviert | - | - | unsigned char | - | 1 | 1 | 0 |
| 14 | Service Qualifier (QU_SER_LTRQD_BAX_ACT) | hex | - | unsigned char | - | 1 | 1 | 0 |
| 15 | Status ICM (QU_TAR_LTRQD_BAX_ACT) | 0-n | - | 0x0f | EnvStatus1 | - | - | - |
| 16 | Status ICM (ST_ECU_TAR_LTRQD_BAX) | 0-n | - | 0xf0 | EnvStatus1 | - | - | - |
| 17 | Signal Qualifier (QU_AVL_LTRQD_BAX_ACT) | 0-n | high | 0x0f00 | EnvStatus3 | - | - | - |
| 18 | ECU Qualifier (ST_ECU_ST_LTRQD_BAX) | 0-n | high | 0xf000 | EnvStatus3 | - | - | - |
| 19 | Betriebsart Aktuator links | 0-n | high | 0x00f0 | EnvStatus3 | - | - | - |
| 20 | Betriebsart Aktuator rechts | 0-n | high | 0x000f | EnvStatus3 | - | - | - |
| 21 | Temperatur Motor links | 0-n | high | 0xf0000000 | EnvTemperature | - | - | - |
| 22 | Temperatur Motor rechts | 0-n | high | 0x0f000000 | EnvTemperature | - | - | - |
| 23 | Temperatur TV Einheit links | 0-n | high | 0x00f00000 | EnvTemperature | - | - | - |
| 24 | Temperatur TV Einheit rechts | 0-n | high | 0x000f0000 | EnvTemperature | - | - | - |
| 25 | Temperatur Lamelle links | 0-n | high | 0x0000f000 | EnvTemperature | - | - | - |
| 26 | Temperatur Lamelle rechts | 0-n | high | 0x00000f00 | EnvTemperature | - | - | - |
| 27 | Reserviert | 0-n | high | 0x000000ff | EnvStatus2 | - | - | - |
| 28 | Reserviert | 0-n | high | 0x00000000 | EnvStatus1 | - | - | - |
| 29 | Sensor Versorgungsspannung links | 0-n | - | 0xf0 | EnvVoltage | - | - | - |
| 30 | Sensor Versorgungsspannung rechts | 0-n | - | 0x0f | EnvVoltage | - | - | - |

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

Dimensions: 69 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x2710 | RAM Fehler links |
| 0x2711 | RAM Fehler rechts |
| 0x2712 | ROM Prüfsummenfehler links |
| 0x2713 | ROM Prüfsummenfehler rechts |
| 0x2714 | EEPROM Integritätsfehler links |
| 0x2715 | EEPROM Integritätsfehler rechts |
| 0x2716 | ICC Fehler links |
| 0x2717 | ICC Fehler rechts |
| 0x2900 | Fehler Redundanz Sollvorgabe TV Einheit links |
| 0x2901 | Fehler Redundanz Sollvorgabe TV Einheit rechts |
| 0x2C08 | Einganggroessen Betriebsartenkoordinator unplausibel links |
| 0x2C0C | Einganggroessen Betriebsartenkoordinator unplausibel rechts |
| 0x2A00 | XGATE Taskverlust Fehler links |
| 0x2A01 | XGATE Taskverlust Fehler rechts |
| 0x2A02 | Sin/Cos- Werte DRLS-EEPROM ungleich dem ermittelten Wert links |
| 0x2A03 | Sin/Cos- Werte DRLS-EEPROM ungleich dem ermittelten Wert rechts |
| 0x2C02 | interner Zustand oder Reaktion unplausibel links |
| 0x2C0A | Notabschaltung fehlgeschlagen links |
| 0x2C03 | interner Zustand oder Reaktion unplausibel rechts |
| 0x2C0B | Notabschaltung fehlgeschlagen rechts |
| 0x2C04 | DRLS TV Einheit links Fehler in redundanter  Signalauswertung |
| 0x2C05 | DRLS TV Einheit rechts Fehler in redundanter  Signalauswertung |
| 0x2D00 | ADC Modulfehler links |
| 0x2D01 | ADC Modulfehler rechts |
| 0x2D04 | Abschaltpfad Aktuator  defekt links |
| 0x2D05 | Abschaltpfad Aktuator defekt rechts |
| 0x2E01 | Reset durch Zugriff auf ungültige Adresse |
| 0x2E02 | Reset durch Clock monitor Fehler |
| 0x2E03 | Reset durch Watchdog |
| 0x2D02 | Programmablauf X-Gate fehlerhaft links |
| 0x2D03 | Programmablauf X-Gate fehlerhaft rechts |
| 0x2C06 | Gradientenbegrenzung Einganggroessen Wirkungskette links |
| 0x2C07 | Gradientenbegrenzung Einganggroessen Wirkungskette rechts |
| 0x2A04 | X-Gate bei Startup nicht bereit links |
| 0x2A05 | X-Gate bei Startup nicht bereit rechts |
| 0x2E08 | Versorgungsspannung kritisch zu niedrig links |
| 0x2E09 | Versorgungsspannung kritisch zu niedrig rechts |
| 0x280A | Öltemperatursensor Momenten-Stelleinheit links Wert nicht plausibel |
| 0x280B | Öltemperatursensor Momenten-Stelleinheit rechts Wert nicht plausibel |
| 0x280C | Temperatursensor Stellmotor links Wert nicht plausibel |
| 0x280D | Temperatursensor Stellmotor rechts Wert nicht plausibel |
| 0x2C00 | Strommessungsfehler TV Einheit links |
| 0x2D06 | Motoransteuerung unplausibel links |
| 0x2D08 | Fehler in Motoransteuerung Erkennung durch UCom links |
| 0x2C01 | Strommessungsfehler TV Einheit rechts |
| 0x2D07 | Motoransteuerung unplausibel rechts |
| 0x2D09 | Fehler in Motoransteuerung Erkennung durch UCom rechts |
| 0x2800 | Übertemperatur Motor TV Einheit links |
| 0x2802 | Übertemperatur TV Einheit links |
| 0x2804 | Übertemperatur Kupplung TV Einheit links |
| 0x2806 | Übertemperatur Endstufe TV Einheit links |
| 0x2801 | Übertemperatur Motor TV Einheit rechts |
| 0x2803 | Übertemperatur TV Einheit rechts |
| 0x2805 | Übertemperatur Kupplung TV Einheit rechts |
| 0x2807 | Übertemperatur Endstufe TV Einheit rechts |
| 0x2B03 | Initialisierung nicht erfolgreich links |
| 0x2B09 | Senkenlage nicht plausibel links |
| 0x2B04 | Flankenspiel unplausibel links |
| 0x2B05 | Adaption unplausibel links |
| 0x2B08 | Fehlererkennung Lageplausibilität TV Einheit links |
| 0x2B00 | Initialisierung nicht erfolgreich rechts |
| 0x2B07 | Senkenlage nicht plausibel rechts |
| 0x2B01 | Flankenspiel unplausibel rechts |
| 0x2B02 | Adaption unplausibel rechts |
| 0x2B06 | Fehlererkennung Lageplausibilität TV Einheit rechts |
| 0x2902 | Fehler Redundanz Empfang ICM/PT CAN |
| 0x58E0 | XGATE Laufzeitüberschreitungsfehler links |
| 0x58E1 | XGATE Laufzeitüberschreitungsfehler rechts |
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

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | EnvAnalogSet1 | EnvDiscrSet1 | EnvDiscrSet2 | EnvDiscrSet3 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 30 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Batteriespannung links | V | - | unsigned char | - | 1 | 10 | 0 |
| 2 | Angefordertes TV Moment | Nm | - | unsigned char | - | 20 | 1 | -2500 |
| 3 | Aktuelles TV Moment | Nm | - | unsigned char | - | 20 | 1 | -2500 |
| 4 | Betriebsart Koordinator | hex | - | unsigned char | - | 1 | 1 | 0 |
| 5 | Aktuelle Position links | Grad | high | unsigned int | - | 1 | 2 | -5000 |
| 6 | Aktuelle Position rechts | Grad | high | unsigned int | - | 1 | 2 | -5000 |
| 7 | Aktuelles Moment Motor links | mNm | - | unsigned char | - | 2 | 1 | -250 |
| 8 | Aktuelles Moment Motor rechts | mNm | - | unsigned char | - | 2 | 1 | -250 |
| 9 | Raddrehzahl HL | km/h | - | unsigned char | - | 2 | 1 | -200 |
| 10 | Raddrehzahl HR | km/h | - | unsigned char | - | 2 | 1 | -200 |
| 11 | Drehzahl Motor | U/min | - | unsigned char | - | 50 | 1 | 0 |
| 12 | Reserviert | - | - | unsigned char | - | 1 | 1 | 0 |
| 13 | Reserviert | - | - | unsigned char | - | 1 | 1 | 0 |
| 14 | Service Qualifier (QU_SER_LTRQD_BAX_ACT) | hex | - | unsigned char | - | 1 | 1 | 0 |
| 15 | Status ICM (QU_TAR_LTRQD_BAX_ACT) | 0-n | - | 0x0f | EnvStatus1 | - | - | - |
| 16 | Status ICM (ST_ECU_TAR_LTRQD_BAX) | 0-n | - | 0xf0 | EnvStatus1 | - | - | - |
| 17 | Signal Qualifier (QU_AVL_LTRQD_BAX_ACT) | 0-n | high | 0x0f00 | EnvStatus3 | - | - | - |
| 18 | ECU Qualifier (ST_ECU_ST_LTRQD_BAX) | 0-n | high | 0xf000 | EnvStatus3 | - | - | - |
| 19 | Betriebsart Aktuator links | 0-n | high | 0x00f0 | EnvStatus3 | - | - | - |
| 20 | Betriebsart Aktuator rechts | 0-n | high | 0x000f | EnvStatus3 | - | - | - |
| 21 | Temperatur Motor links | 0-n | high | 0xf0000000 | EnvTemperature | - | - | - |
| 22 | Temperatur Motor rechts | 0-n | high | 0x0f000000 | EnvTemperature | - | - | - |
| 23 | Temperatur TV Einheit links | 0-n | high | 0x00f00000 | EnvTemperature | - | - | - |
| 24 | Temperatur TV Einheit rechts | 0-n | high | 0x000f0000 | EnvTemperature | - | - | - |
| 25 | Temperatur Lamelle links | 0-n | high | 0x0000f000 | EnvTemperature | - | - | - |
| 26 | Temperatur Lamelle rechts | 0-n | high | 0x00000f00 | EnvTemperature | - | - | - |
| 27 | Reserviert | 0-n | high | 0x000000ff | EnvStatus2 | - | - | - |
| 28 | Reserviert | 0-n | high | 0x00000000 | EnvStatus1 | - | - | - |
| 29 | Sensor Versorgungsspannung links | 0-n | - | 0xf0 | EnvVoltage | - | - | - |
| 30 | Sensor Versorgungsspannung rechts | 0-n | - | 0x0f | EnvVoltage | - | - | - |

<a id="table-envanalogset1"></a>
### ENVANALOGSET1

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 |

<a id="table-envtemperature"></a>
### ENVTEMPERATURE

Dimensions: 121 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0 | -40 °C |
| 1 | -20 °C |
| 2 | 0 °C |
| 3 | 20 °C |
| 4 | 40 °C |
| 5 | 60 °C |
| 6 | 80 °C |
| 7 | 100 °C |
| 8 | 120 °C |
| 9 | 140 °C |
| 10 | 160 °C |
| 11 | 180 °C |
| 12 | 200 °C |
| 13 | 220 °C |
| 14 | 240 °C |
| 15 | SNV |
| 16 | -20 °C |
| 32 | 0 °C |
| 48 | 20 °C |
| 64 | 40 °C |
| 80 | 60 °C |
| 96 | 80 °C |
| 112 | 100 °C |
| 128 | 120 °C |
| 144 | 140 °C |
| 160 | 160 °C |
| 176 | 180 °C |
| 192 | 200 °C |
| 208 | 220 °C |
| 224 | 240 °C |
| 240 | SNV |
| 256 | -20 °C |
| 512 | 0 °C |
| 768 | 20 °C |
| 1024 | 40 °C |
| 1280 | 60 °C |
| 1536 | 80 °C |
| 1792 | 100 °C |
| 2048 | 120 °C |
| 2304 | 140 °C |
| 2560 | 160 °C |
| 2816 | 180 °C |
| 3072 | 200 °C |
| 3328 | 220 °C |
| 3584 | 240 °C |
| 3840 | SNV |
| 4096 | -20 °C |
| 8192 | 0 °C |
| 12288 | 20 °C |
| 16384 | 40 °C |
| 20480 | 60 °C |
| 24576 | 80 °C |
| 28672 | 100 °C |
| 32768 | 120 °C |
| 36864 | 140 °C |
| 40960 | 160 °C |
| 45056 | 180 °C |
| 49152 | 200 °C |
| 53248 | 220 °C |
| 57344 | 240 °C |
| 61440 | SNV |
| 65536 | -20 °C |
| 131072 | 0 °C |
| 196608 | 20 °C |
| 262144 | 40 °C |
| 327680 | 60 °C |
| 393216 | 80 °C |
| 458752 | 100 °C |
| 524288 | 120 °C |
| 589824 | 140 °C |
| 655360 | 160 °C |
| 720896 | 180 °C |
| 786432 | 200 °C |
| 851968 | 220 °C |
| 917504 | 240 °C |
| 983040 | SNV |
| 1048576 | -20 °C |
| 2097152 | 0 °C |
| 3145728 | 20 °C |
| 4194304 | 40 °C |
| 5242880 | 60 °C |
| 6291456 | 80 °C |
| 7340032 | 100 °C |
| 8388608 | 120 °C |
| 9437184 | 140 °C |
| 10485760 | 160 °C |
| 11534336 | 180 °C |
| 12582912 | 200 °C |
| 13631488 | 220 °C |
| 14680064 | 240 °C |
| 15728640 | SNV |
| 16777216 | -20 °C |
| 33554432 | 0 °C |
| 50331648 | 20 °C |
| 67108864 | 40 °C |
| 83886080 | 60 °C |
| 100663296 | 80 °C |
| 117440512 | 100 °C |
| 134217728 | 120 °C |
| 150994944 | 140 °C |
| 167772160 | 160 °C |
| 184549376 | 180 °C |
| 201326592 | 200 °C |
| 218103808 | 220 °C |
| 234881024 | 240 °C |
| 251658240 | SNV |
| 268435456 | -20 °C |
| 536870912 | 0 °C |
| 805306368 | 20 °C |
| 1073741824 | 40 °C |
| 1342177280 | 60 °C |
| 1610612736 | 80 °C |
| 1879048192 | 100 °C |
| 2147483648 | 120 °C |
| 2415919104 | 140 °C |
| 2684354560 | 160 °C |
| 2952790016 | 180 °C |
| 3221225472 | 200 °C |
| 3489660928 | 220 °C |
| 3758096384 | 240 °C |
| 4026531840 | SNV |

<a id="table-envvoltage"></a>
### ENVVOLTAGE

Dimensions: 31 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0 | 0 V |
| 1 | 1 V |
| 2 | 2 V |
| 3 | 3 V |
| 4 | 4 V |
| 5 | 5 V |
| 6 | 6 V |
| 7 | 7 V |
| 8 | 8 V |
| 9 | 9 V |
| 10 | 10 V |
| 11 | 11 V |
| 12 | 12 V |
| 13 | 13 V |
| 14 | 14 V |
| 15 | SNV |
| 16 | 1 V |
| 32 | 2 V |
| 48 | 3 V |
| 64 | 4 V |
| 80 | 5 V |
| 96 | 6 V |
| 112 | 7 V |
| 128 | 8 V |
| 144 | 9 V |
| 160 | 10 V |
| 176 | 11 V |
| 192 | 12 V |
| 208 | 13 V |
| 224 | 14 V |
| 240 | SNV |

<a id="table-envdiscrset1"></a>
### ENVDISCRSET1

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 17 | 18 | 19 | 20 |

<a id="table-envdiscrset2"></a>
### ENVDISCRSET2

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 |

<a id="table-envdiscrset3"></a>
### ENVDISCRSET3

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 29 | 30 |

<a id="table-stat-adaption-links"></a>
### STAT_ADAPTION_LINKS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Adaptionswerte vorhanden links |
| 4 | Adaptionswerte vorhanden, Adaptionswert links |
| 8 | Aenderung Adaptionswert zur Erstadaption links |
| 12 | Aenderung Adaptionswert zur vorherigen Adaption links |

<a id="table-stat-adaption-rechts"></a>
### STAT_ADAPTION_RECHTS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Adaptionswerte vorhanden rechts |
| 1 | Adaptionswerte vorhanden, Adaptionswert rechts |
| 2 | Aenderung Adaptionswert zur Erstadaption rechts |
| 3 | Aenderung Adaptionswert zur vorherigen Adaption rechts |

<a id="table-stat-verfuegbarkeit-tv-xxx"></a>
### STAT_VERFUEGBARKEIT_TV_XXX

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | 0% Availability |
| 1 | 10% Availability |
| 2 | 20% Availability |
| 3 | 30% Availability |
| 4 | 40% Availability |
| 5 | 50% Availability |
| 6 | 60% Availability |
| 7 | 70% Availability |
| 8 | 80% Availability |
| 9 | 90% Availability |
| 10 | 100% Availability |
| 11 | not defined |
| 12 | not defined |
| 13 | not defined |
| 14 | not defined |
| 15 | signal invalid |

<a id="table-stat-funktionen-1"></a>
### STAT_FUNKTIONEN_1

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | NOT_AVAILABLE |
| 2 | RUNNING |
| 3 | AVAILABLE |
| 4 | ERROR |
| XX | Signal Invalid |

<a id="table-stat-funktionen-2"></a>
### STAT_FUNKTIONEN_2

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | IDLE |
| 2 | RUNNING |
| 3 | ERROR |
| XX | Signal Invalid |

<a id="table-envstatus1"></a>
### ENVSTATUS1

Dimensions: 31 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0 | 0 |
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
| 5 | 5 |
| 6 | 6 |
| 7 | 7 |
| 8 | 8 |
| 9 | 9 |
| 10 | 10 |
| 11 | 11 |
| 12 | 12 |
| 13 | 13 |
| 14 | 14 |
| 15 | 15 |
| 16 | 1 |
| 32 | 2 |
| 48 | 3 |
| 64 | 4 |
| 80 | 5 |
| 96 | 6 |
| 112 | 7 |
| 128 | 8 |
| 144 | 9 |
| 160 | 10 |
| 176 | 11 |
| 192 | 12 |
| 208 | 13 |
| 224 | 14 |
| 240 | 15 |

<a id="table-envstatus3"></a>
### ENVSTATUS3

Dimensions: 61 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0 | 0 |
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
| 5 | 5 |
| 6 | 6 |
| 7 | 7 |
| 8 | 8 |
| 9 | 9 |
| 10 | 10 |
| 11 | 11 |
| 12 | 12 |
| 13 | 13 |
| 14 | 14 |
| 15 | 15 |
| 16 | 1 |
| 32 | 2 |
| 48 | 3 |
| 64 | 4 |
| 80 | 5 |
| 96 | 6 |
| 112 | 7 |
| 128 | 8 |
| 144 | 9 |
| 160 | 10 |
| 176 | 11 |
| 192 | 12 |
| 208 | 13 |
| 224 | 14 |
| 240 | 15 |
| 256 | 1 |
| 512 | 2 |
| 768 | 3 |
| 1024 | 4 |
| 1280 | 5 |
| 1536 | 6 |
| 1792 | 7 |
| 2048 | 8 |
| 2304 | 9 |
| 2560 | 10 |
| 2816 | 11 |
| 3072 | 12 |
| 3328 | 13 |
| 3584 | 14 |
| 3840 | 15 |
| 4096 | 1 |
| 8192 | 2 |
| 12288 | 3 |
| 16384 | 4 |
| 20480 | 5 |
| 24576 | 6 |
| 28672 | 7 |
| 32768 | 8 |
| 36864 | 9 |
| 40960 | 10 |
| 45056 | 11 |
| 49152 | 12 |
| 53248 | 13 |
| 57344 | 14 |
| 61440 | 15 |

<a id="table-stat-qsg-servicequalifier"></a>
### STAT_QSG_SERVICEQUALIFIER

Dimensions: 21 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 32 | Operation - Service ist verfügbar |
| 33 | Operation - Service ist verfügbar: HabAcht Stellung rechts |
| 34 | Operation - Service ist verfügbar: HabAcht Stellung links |
| 35 | Operation - Service ist verfügbar: HabAcht Stellung links und rechts |
| 96 | Fehler - Service nicht verfügbar: interner Fehler |
| 97 | Fehler - Service nicht verfügbar: Aktives Rampen auf 0 Nm |
| 112 | Service nicht vorhanden |
| 128 | Initialisierung |
| 224 | Standby - Service nicht verfügbar: WarteCCP bzw. Shutdown 2 |
| 225 | Standby - Service nicht verfügbar: Kupplungsinitialisierung |
| 226 | Standby - Service nicht verfügbar: Schutzaus: fehlende Raddrehzahlinformationen |
| 227 | Standby - Service nicht verfügbar: Schutzaus: fehlende Sollmoment von ICM |
| 228 | Standby - Service nicht verfügbar: Schutzaus: Übertemperatur |
| 229 | Standby - Service nicht verfügbar: Schutzaus: Motordrehzahl zu gering/MSA |
| 230 | Standby - Service nicht verfügbar: Schutzaus: Unterspannung |
| 231 | Standby - Service nicht verfügbar: Schutzaus: Überspannung |
| 232 | Standby - Service nicht verfügbar: Schutzaus: sonstiges |
| 233 | Standby - Service nicht verfügbar: Aktives Rampen auf 0Nm |
| 234 | Standby - Service nicht verfügbar: Adaption |
| 235 | Standby - Service nicht verfügbar: Werkstattfunktionstest |
| 255 | Signal ungültig |

<a id="table-envstatus2"></a>
### ENVSTATUS2

Dimensions: 256 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0 | 0 |
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
| 5 | 5 |
| 6 | 6 |
| 7 | 7 |
| 8 | 8 |
| 9 | 9 |
| 10 | 10 |
| 11 | 11 |
| 12 | 12 |
| 13 | 13 |
| 14 | 14 |
| 15 | 15 |
| 16 | 16 |
| 17 | 17 |
| 18 | 18 |
| 19 | 19 |
| 20 | 20 |
| 21 | 21 |
| 22 | 22 |
| 23 | 23 |
| 24 | 24 |
| 25 | 25 |
| 26 | 26 |
| 27 | 27 |
| 28 | 28 |
| 29 | 29 |
| 30 | 30 |
| 31 | 31 |
| 32 | 32 |
| 33 | 33 |
| 34 | 34 |
| 35 | 35 |
| 36 | 36 |
| 37 | 37 |
| 38 | 38 |
| 39 | 39 |
| 40 | 40 |
| 41 | 41 |
| 42 | 42 |
| 43 | 43 |
| 44 | 44 |
| 45 | 45 |
| 46 | 46 |
| 47 | 47 |
| 48 | 48 |
| 49 | 49 |
| 50 | 50 |
| 51 | 51 |
| 52 | 52 |
| 53 | 53 |
| 54 | 54 |
| 55 | 55 |
| 56 | 56 |
| 57 | 57 |
| 58 | 58 |
| 59 | 59 |
| 60 | 60 |
| 61 | 61 |
| 62 | 62 |
| 63 | 63 |
| 64 | 64 |
| 65 | 65 |
| 66 | 66 |
| 67 | 67 |
| 68 | 68 |
| 69 | 69 |
| 70 | 70 |
| 71 | 71 |
| 72 | 72 |
| 73 | 73 |
| 74 | 74 |
| 75 | 75 |
| 76 | 76 |
| 77 | 77 |
| 78 | 78 |
| 79 | 79 |
| 80 | 80 |
| 81 | 81 |
| 82 | 82 |
| 83 | 83 |
| 84 | 84 |
| 85 | 85 |
| 86 | 86 |
| 87 | 87 |
| 88 | 88 |
| 89 | 89 |
| 90 | 90 |
| 91 | 91 |
| 92 | 92 |
| 93 | 93 |
| 94 | 94 |
| 95 | 95 |
| 96 | 96 |
| 97 | 97 |
| 98 | 98 |
| 99 | 99 |
| 100 | 100 |
| 101 | 101 |
| 102 | 102 |
| 103 | 103 |
| 104 | 104 |
| 105 | 105 |
| 106 | 106 |
| 107 | 107 |
| 108 | 108 |
| 109 | 109 |
| 110 | 110 |
| 111 | 111 |
| 112 | 112 |
| 113 | 113 |
| 114 | 114 |
| 115 | 115 |
| 116 | 116 |
| 117 | 117 |
| 118 | 118 |
| 119 | 119 |
| 120 | 120 |
| 121 | 121 |
| 122 | 122 |
| 123 | 123 |
| 124 | 124 |
| 125 | 125 |
| 126 | 126 |
| 127 | 127 |
| 128 | 128 |
| 129 | 129 |
| 130 | 130 |
| 131 | 131 |
| 132 | 132 |
| 133 | 133 |
| 134 | 134 |
| 135 | 135 |
| 136 | 136 |
| 137 | 137 |
| 138 | 138 |
| 139 | 139 |
| 140 | 140 |
| 141 | 141 |
| 142 | 142 |
| 143 | 143 |
| 144 | 144 |
| 145 | 145 |
| 146 | 146 |
| 147 | 147 |
| 148 | 148 |
| 149 | 149 |
| 150 | 150 |
| 151 | 151 |
| 152 | 152 |
| 153 | 153 |
| 154 | 154 |
| 155 | 155 |
| 156 | 156 |
| 157 | 157 |
| 158 | 158 |
| 159 | 159 |
| 160 | 160 |
| 161 | 161 |
| 162 | 162 |
| 163 | 163 |
| 164 | 164 |
| 165 | 165 |
| 166 | 166 |
| 167 | 167 |
| 168 | 168 |
| 169 | 169 |
| 170 | 170 |
| 171 | 171 |
| 172 | 172 |
| 173 | 173 |
| 174 | 174 |
| 175 | 175 |
| 176 | 176 |
| 177 | 177 |
| 178 | 178 |
| 179 | 179 |
| 180 | 180 |
| 181 | 181 |
| 182 | 182 |
| 183 | 183 |
| 184 | 184 |
| 185 | 185 |
| 186 | 186 |
| 187 | 187 |
| 188 | 188 |
| 189 | 189 |
| 190 | 190 |
| 191 | 191 |
| 192 | 192 |
| 193 | 193 |
| 194 | 194 |
| 195 | 195 |
| 196 | 196 |
| 197 | 197 |
| 198 | 198 |
| 199 | 199 |
| 200 | 200 |
| 201 | 201 |
| 202 | 202 |
| 203 | 203 |
| 204 | 204 |
| 205 | 205 |
| 206 | 206 |
| 207 | 207 |
| 208 | 208 |
| 209 | 209 |
| 210 | 210 |
| 211 | 211 |
| 212 | 212 |
| 213 | 213 |
| 214 | 214 |
| 215 | 215 |
| 216 | 216 |
| 217 | 217 |
| 218 | 218 |
| 219 | 219 |
| 220 | 220 |
| 221 | 221 |
| 222 | 222 |
| 223 | 223 |
| 224 | 224 |
| 225 | 225 |
| 226 | 226 |
| 227 | 227 |
| 228 | 228 |
| 229 | 229 |
| 230 | 230 |
| 231 | 231 |
| 232 | 232 |
| 233 | 233 |
| 234 | 234 |
| 235 | 235 |
| 236 | 236 |
| 237 | 237 |
| 238 | 238 |
| 239 | 239 |
| 240 | 240 |
| 241 | 241 |
| 242 | 242 |
| 243 | 243 |
| 244 | 244 |
| 245 | 245 |
| 246 | 246 |
| 247 | 247 |
| 248 | 248 |
| 249 | 249 |
| 250 | 250 |
| 251 | 251 |
| 252 | 252 |
| 253 | 253 |
| 254 | 254 |
| 255 | 255 |
