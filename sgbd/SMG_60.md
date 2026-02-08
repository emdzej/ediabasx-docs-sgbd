# SMG_60.prg

- Jobs: [48](#jobs)
- Tables: [176](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Sequentielles Schaltgetriebe der M-GmbH für den E60 und E63 |
| ORIGIN | BMW TI-430 Ruediger_Gall |
| REVISION | 5.010 |
| AUTHOR | BMW TI-430 Ruediger_Gall |
| COMMENT | GETRAG-7-Gang-Getriebe |
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
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
- [HS_LESEN_DETAIL](#job-hs-lesen-detail) - Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default
- [HS_LOESCHEN](#job-hs-loeschen) - Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_LESEN](#job-zif-lesen) - Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_BACKUP_LESEN](#job-zif-backup-lesen) - Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [PHYSIKALISCHE_HW_NR_LESEN](#job-physikalische-hw-nr-lesen) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [HARDWARE_REFERENZ_LESEN](#job-hardware-referenz-lesen) - Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [DATEN_REFERENZ_LESEN](#job-daten-referenz-lesen) - Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default
- [FLASH_ZEITEN_LESEN](#job-flash-zeiten-lesen) - Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default
- [FLASH_BLOCKLAENGE_LESEN](#job-flash-blocklaenge-lesen) - Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default
- [FLASH_PROGRAMMIER_STATUS_LESEN](#job-flash-programmier-status-lesen) - Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [STATUS_ISTWERTE](#job-status-istwerte) - mit dem SGBD-Generator erzeugt
- [STATUS_FAHRZEUGTESTER](#job-status-fahrzeugtester) - mit dem SGBD-Generator erzeugt
- [PROGRAMMERSTELLUNG](#job-programmerstellung) - Datum der Programmerstellung (speziell fuer GETRAG) (Service ID 0x30, Identifier 0xA4)
- [RBM_RATIO](#job-rbm-ratio) - Dient zum Auslesen der OBD fehlerbezogenen RBM - Ratios (speziell fuer GETRAG) (Service ID 0x22, Identifier 0x53, 0x00)
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes ---zusätzlich für VS: -------------------------- KWP2000: $30 A2 ADAPTIONSWERTE_GETRIEBE KWP2000: $22 10 VERSCHLEISSDATEN_LESEN KWP2000: $30 A0 ADAPTIONSWERTE_KUPPLUNG KWP2000: $30 A1 ADAPTIONSWERTE_KUPPLUNGSKENNLINIE KWP2000: $30 A3 ADAPTIONSWERTE_EINKUPPELZEITEN Modus  : Default
- [ADAPTIONSWERTE_KUPPLUNG](#job-adaptionswerte-kupplung) - Adaptionswerte lesen (Service ID 0x30, Identifier 0xA0)
- [ADAPTIONSWERTE_KUPPLUNGSKENNLINIE](#job-adaptionswerte-kupplungskennlinie) - Adaptionswerte lesen (Service ID 0x30, Identifier 0xA1)
- [ADAPTIONSWERTE_GETRIEBE](#job-adaptionswerte-getriebe) - Adaptionswerte lesen (Service ID 0x30, Identifier 0xA2)
- [ADAPTIONSWERTE_EINKUPPELZEITEN](#job-adaptionswerte-einkuppelzeiten) - Adaptionswerte lesen (Service ID 0x30, Identifier 0xA3)
- [ADAPTIONSWERTE_ZURUECKSETZEN](#job-adaptionswerte-zuruecksetzen) - Adaptionswerte auf Defaultwerte zuruecksetzen von: Kupplungskennlinie (Service ID 0x30)  ACHTUNG: Im Anschluss Zuendung aus, um Defaultwerte abzuspeichern. Steuergeraete Abfall abwarten Ganganzeige im Kombi bleibt ca. 5s erhalten und faellt dann ab. oder Speichern per Diagnose
- [VERSCHLEISSDATEN_LESEN](#job-verschleissdaten-lesen) - Verschleissdaten lesen (Service ID 0x22)
- [VERSCHLEISSDATEN_LOESCHEN](#job-verschleissdaten-loeschen) - Verschleissdaten loeschen (Service ID 0x2E)
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Codierdaten lesen (Service ID 0x22)
- [CODIERDATEN_SCHREIBEN](#job-codierdaten-schreiben) - Codierung schreiben (Service ID 0x2E)
- [STEUERN_STELLGLIED](#job-steuern-stellglied) - Ansteuern der Stellglieder  Argumente durch Semikolon trennen.
- [STEUERN_TESTPRG_STOP](#job-steuern-testprg-stop) - Beenden eines laufenden Testprogrammes (Sowie Zuruecksetzen des Zaehlers.) Muss VOR STEUERN_TESTPRG_STARTEN geschickt werden!
- [STEUERN_TESTPRG_STARTEN](#job-steuern-testprg-starten) - Testprogramm starten Hinweis: Zuvor STEUERN_TESTPRG_STOP schicken! Weitere Istzustaende mittels STEUERN_TESTPRG_ISTZUSTAND auslesen!
- [STATUS_TESTPRG_ISTZUSTAND](#job-status-testprg-istzustand) - Istzustand eines STEUERN_TESTPRG_STARTEN abfragen

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

<a id="job-status-istwerte"></a>
### STATUS_ISTWERTE

mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOTORDREHZAHL_WERT | real | Motordrehzahl Bereich von 0 [1/min] bis 10000 [1/min] |
| STAT_MOTORDREHZAHL_EINH | string | Motordrehzahl Einheit: 1/min |
| STAT_MOTORDREHZAHL_CAN_WERT | real | Motordrehzahl über CAN Bereich von 0 [1/min] bis 10000 [1/min] |
| STAT_MOTORDREHZAHL_CAN_EINH | string | Motordrehzahl über CAN Einheit: 1/min |
| STAT_EINGANGSDREHZAHL_WERT | real | Getriebeeingangsdrehzahl Bereich von 0 [1/min] bis 10000 [1/min] |
| STAT_EINGANGSDREHZAHL_EINH | string | Getriebeeingangsdrehzahl Einheit: 1/min |
| STAT_AUSGANGSDREHZAHL_WERT | real | Getriebeausgangsdrehzal Bereich von 0 [1/min] bis 10000 [1/min] |
| STAT_AUSGANGSDREHZAHL_EINH | string | Getriebeausgangsdrehzal Einheit: 1/min |
| STAT_GESCHWINDIGKEIT_WERT | real | Fahrzeuggeschwindigkeit Bereich von -300 [km/h] bis 300 [km/h] |
| STAT_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit Einheit: km/h |
| STAT_RADGESCHWINDIGKEIT_VL_WERT | real | Radgeschwindigkeit vorne links Bereich von -300 [km/h] bis 300 [km/h] |
| STAT_RADGESCHWINDIGKEIT_VL_EINH | string | Radgeschwindigkeit vorne links Einheit: km/h |
| STAT_RADGESCHWINDIGKEIT_VR_WERT | real | Radgeschwindigkeit vorne rechts Bereich von -300 [km/h] bis 300 [km/h] |
| STAT_RADGESCHWINDIGKEIT_VR_EINH | string | Radgeschwindigkeit vorne rechts Einheit: km/h |
| STAT_RADGESCHWINDIGKEIT_HL_WERT | real | Radgeschwindigkeit hinten links Bereich von -300 [km/h] bis 300 [km/h] |
| STAT_RADGESCHWINDIGKEIT_HL_EINH | string | Radgeschwindigkeit hinten links Einheit: km/h |
| STAT_RADGESCHWINDIGKEIT_HR_WERT | real | Radgeschwindigkeit hinten rechts Bereich von -300 [km/h] bis 300 [km/h] |
| STAT_RADGESCHWINDIGKEIT_HR_EINH | string | Radgeschwindigkeit hinten rechts Einheit: km/h |
| STAT_GESCHWINDIGKEIT_HINTERACHSE_WERT | real | Fahrzeuggeschwindigkeit der Hinterachse Bereich von -300 [km/h] bis 300 [km/h] |
| STAT_GESCHWINDIGKEIT_HINTERACHSE_EINH | string | Fahrzeuggeschwindigkeit der Hinterachse Einheit: km/h |
| STAT_MOTORTEMPERATUR_WERT | real | Motortemperatur Bereich von -48 [Grad C] bis 205 [Grad C] |
| STAT_MOTORTEMPERATUR_EINH | string | Motortemperatur Einheit: Grad C |
| STAT_MOTOROELTEMPERATUR_WERT | real | Motoroeltemperatur Bereich von -48 [Grad C] bis 205 [Grad C] |
| STAT_MOTOROELTEMPERATUR_EINH | string | Motoroeltemperatur Einheit: Grad C |
| STAT_HYDRAULIKTEMPERATUR_WERT | real | Hydrauliktemperatur Bereich von -48 [Grad C] bis 205 [Grad C] |
| STAT_HYDRAULIKTEMPERATUR_EINH | string | Hydrauliktemperatur Einheit: Grad C |
| STAT_UMGEBUNGSTEMPERATUR_WERT | real | Umgebungstemperatur Bereich von -48 [Grad C] bis 205 [Grad C] |
| STAT_UMGEBUNGSTEMPERATUR_EINH | string | Umgebungstemperatur Einheit: Grad C |
| STAT_UBAT_WERT | real | Batteriespannung Klemme 30 Bereich von 0 [V] bis 25,6 [V] |
| STAT_UBAT_EINH | string | Batteriespannung Klemme 30 Einheit: V |
| STAT_USENSA_WERT | real | Sensorspannungsversorgung A Bereich von 0 [V] bis 10 [V] |
| STAT_USENSA_EINH | string | Sensorspannungsversorgung A Einheit: V |
| STAT_USENSB_WERT | real | Sensorspannungsversorgung B Bereich von 0 [V] bis 10 [V] |
| STAT_USENSB_EINH | string | Sensorspannungsversorgung B Einheit: V |
| STAT_STROM_KUP_WERT | real | Iststrom Magnetventil Kupplung Bereich von 0 [mA] bis 3000 [mA] |
| STAT_STROM_KUP_EINH | string | Iststrom Magnetventil Kupplung Einheit: mA |
| STAT_STROM_SCHALTZYLINDER_R_1_WERT | real | Iststrom Magnetventil PWV 1 (Proportional Wegeventil) / Schaltzylinder R/1 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_STROM_SCHALTZYLINDER_R_1_EINH | string | Iststrom Magnetventil PWV 1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: mA |
| STAT_STROM_SCHALTZYLINDER_5_3_WERT | real | Iststrom Magnetventil PWV 2 (Proportional Wegeventil) / Schaltzylinder 5/3 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_STROM_SCHALTZYLINDER_5_3_EINH | string | Iststrom Magnetventil PWV 2 (Proportional Wegeventil) / Schaltzylinder 5/3 Einheit: mA |
| STAT_STROM_SCHALTZYLINDER_2_4_WERT | real | Iststrom Magnetventil PWV 3 (Proportional Wegeventil) / Schaltzylinder 6/7 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_STROM_SCHALTZYLINDER_2_4_EINH | string | Iststrom Magnetventil PWV 3 (Proportional Wegeventil) / Schaltzylinder 6/7 Einheit: mA |
| STAT_STROM_SCHALTZYLINDER_6_7_WERT | real | Iststrom Magnetventil PWV 4 (Proportional Wegeventil) / Schaltzylinder 2/4 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_STROM_SCHALTZYLINDER_6_7_EINH | string | Iststrom Magnetventil PWV 4 (Proportional Wegeventil) / Schaltzylinder 2/4 Einheit: mA |
| STAT_STROM_DRUCK_REGELVENTIL1_WERT | real | Iststrom Magnetventil DRV 1 (Druck Regelventil) Bereich von 0 [mA] bis 3000 [mA] |
| STAT_STROM_DRUCK_REGELVENTIL1_EINH | string | Iststrom Magnetventil DRV 1 (Druck Regelventil) Einheit: mA |
| STAT_STROM_DRUCK_REGELVENTIL2_WERT | real | Iststrom Magnetventil DRV 2 (Druck Regelventil) Bereich von 0 [mA] bis 3000 [mA] |
| STAT_STROM_DRUCK_REGELVENTIL2_EINH | string | Iststrom Magnetventil DRV 2 (Druck Regelventil) Einheit: mA |
| STAT_SOLL_STROM_KUP_WERT | real | Sollstrom Magnetventil Kupplung Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_KUP_EINH | string | Sollstrom Magnetventil Kupplung Einheit: mA |
| STAT_SOLL_STROM_SCHALTZYLINDER_R_1_WERT | real | Sollstrom Magnetventil PWV 1 (Proportional Wegeventil) / Schaltzylinder R/1 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_SCHALTZYLINDER_R_1_EINH | string | Sollstrom Magnetventil PWV 1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: mA |
| STAT_SOLL_STROM_SCHALTZYLINDER_5_3_WERT | real | Sollstrom Magnetventil PWV 2 (Proportional Wegeventil) / Schaltzylinder 5/3 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_SCHALTZYLINDER_5_3_EINH | string | Sollstrom Magnetventil PWV 2 (Proportional Wegeventil) / Schaltzylinder 5/3 Einheit: mA |
| STAT_SOLL_STROM_SCHALTZYLINDER_2_4_WERT | real | Sollstrom Magnetventil PWV 3 (Proportional Wegeventil) / Schaltzylinder 2/4 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_SCHALTZYLINDER_2_4_EINH | string | Sollstrom Magnetventil PWV 3 (Proportional Wegeventil) / Schaltzylinder 2/4 Einheit: mA |
| STAT_SOLL_STROM_SCHALTZYLINDER_6_7_WERT | real | Sollstrom Magnetventil PWV 4 (Proportional Wegeventil) / Schaltzylinder 6/7 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_SCHALTZYLINDER_6_7_EINH | string | Sollstrom Magnetventil PWV 4 (Proportional Wegeventil) / Schaltzylinder 6/7 Einheit: mA |
| STAT_SOLL_STROM_DRUCKREGELVENTIL1_WERT | real | Sollstrom Magnetventil DRV 1 (Druck Regelventil) Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_DRUCKREGELVENTIL1_EINH | string | Sollstrom Magnetventil DRV 1 (Druck Regelventil) Einheit: mA |
| STAT_SOLL_STROM_DRUCKREGELVENTIL2_WERT | real | Sollstrom Magnetventil DRV 2 (Druck Regelventil) Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_DRUCKREGELVENTIL2_EINH | string | Sollstrom Magnetventil DRV 2 (Druck Regelventil) Einheit: mA |
| STAT_POS_SCHALTSTANGE_R_1_WERT | real | Istposition Schaltstange R/1, Bereich: 0-1023 Inkremente Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_POS_SCHALTSTANGE_R_1_EINH | string | Istposition Schaltstange R/1, Bereich: 0-1023 Inkremente Einheit: Ink |
| STAT_POS_SCHALTSTANGE_5_3_WERT | real | Istposition Schaltstange 5/3, Bereich: 0-1023 Inkremente Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_POS_SCHALTSTANGE_5_3_EINH | string | Istposition Schaltstange 5/3, Bereich: 0-1023 Inkremente Einheit: Ink |
| STAT_POS_SCHALTSTANGE_2_4_WERT | real | Istposition Schaltstange 2/4, Bereich: 0-1023 Inkremente Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_POS_SCHALTSTANGE_2_4_EINH | string | Istposition Schaltstange 2/4, Bereich: 0-1023 Inkremente Einheit: Ink |
| STAT_POS_SCHALTSTANGE_6_7_WERT | real | Istposition Schaltstange 6/7, Bereich: 0-1023 Inkremente Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_POS_SCHALTSTANGE_6_7_EINH | string | Istposition Schaltstange 6/7, Bereich: 0-1023 Inkremente Einheit: Ink |
| STAT_POS2_SCHALTSTANGE_R_1_WERT | real | Istposition Schaltstange R/1 Redundant, Bereich: 0-1023 Inkremente Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_POS2_SCHALTSTANGE_R_1_EINH | string | Istposition Schaltstange R/1 Redundant, Bereich: 0-1023 Inkremente Einheit: Ink |
| STAT_POS_KUP_WERT | real | Istposition Kupplung, Bereich: 0-1023 Inkremente Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_POS_KUP_EINH | string | Istposition Kupplung, Bereich: 0-1023 Inkremente Einheit: Ink |
| STAT_SOLL_POS_SCHALTSTANGE_R_1_WERT | real | Sollpostion Schaltstange R/1 Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_SOLL_POS_SCHALTSTANGE_R_1_EINH | string | Sollpostion Schaltstange R/1 Einheit: Ink |
| STAT_SOLL_POS_SCHALTSTANGE_5_3_WERT | real | Sollpostion Schaltstange 5/3 Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_SOLL_POS_SCHALTSTANGE_5_3_EINH | string | Sollpostion Schaltstange 5/3 Einheit: Ink |
| STAT_SOLL_POS_SCHALTSTANGE_2_4_WERT | real | Sollpostion Schaltstange 2/4 Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_SOLL_POS_SCHALTSTANGE_2_4_EINH | string | Sollpostion Schaltstange 2/4 Einheit: Ink |
| STAT_SOLL_POS_SCHALTSTANGE_6_7_WERT | real | Sollpostion Schaltstange 6/7 Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_SOLL_POS_SCHALTSTANGE_6_7_EINH | string | Sollpostion Schaltstange 6/7 Einheit: Ink |
| STAT_SOLL_POS_KUP_WERT | real | Sollposition Kupplung Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_SOLL_POS_KUP_EINH | string | Sollposition Kupplung Einheit: Ink |
| STAT_FAHRPEDAL_WERT | real | Fahrpedalwert Bereich von 0 [%] bis 100 [%] |
| STAT_FAHRPEDAL_EINH | string | Fahrpedalwert Einheit: % |
| STAT_MOTORMOMENT_WERT | real | Motormoment Bereich von -1024 [NM] bis 1024 [NM] |
| STAT_MOTORMOMENT_EINH | string | Motormoment Einheit: NM |
| STAT_AQUER_CAN_WERT | real | Querbeschleunigung von CAN Bereich von -20 [m/s^2] bis 20 [m/s^2] |
| STAT_AQUER_CAN_EINH | string | Querbeschleunigung von CAN Einheit: m/s^2 |
| STAT_ALAENGS_SENSOR_WERT | real | Längsbeschleunigungsensor für SMG in m/s^2 Bereich von -20.0 [m/s^2] bis 20.0 [m/s^2] |
| STAT_ALAENGS_SENSOR_EINH | string | Längsbeschleunigungsensor für SMG in m/s^2 Einheit: m/s^2 |
| STAT_ALAENGS_SMG_WERT | real | Laengsbeschleunigung berechnet vom SMG-Steuergeraet berechnet, da CAN zu schlechte Werte liefert Bereich von -20 [m/s^2] bis 20 [m/s^2] |
| STAT_ALAENGS_SMG_EINH | string | Laengsbeschleunigung berechnet vom SMG-Steuergeraet berechnet, da CAN zu schlechte Werte liefert Einheit: m/s^2 |
| STAT_KILOMETERSTAND_WERT | real | Kilomterstand von CAN Bereich von 0 [km] bis 655350 [km] |
| STAT_KILOMETERSTAND_EINH | string | Kilomterstand von CAN Einheit: km |
| STAT_HYDRAULIKDRUCK_WERT | real | Hydraulikdruck Bereich von 0 [bar] bis 120 [bar] |
| STAT_HYDRAULIKDRUCK_EINH | string | Hydraulikdruck Einheit: bar |
| STAT_SHIFT_LOCK_EIN | int | Shitf-Lock, 0= Waehlhebel gesperrt, 1= Waehlhebel frei |
| STAT_SCHALTER_RUECK_EIN | int | Rueckfahrlichtschalter |
| STAT_ANLASSERFREIGABE_AKTIV | int | Kupplung und Getriebe geben Anlasserfreigabe an DME |
| STAT_HYDRAULIK_PUMPE_EIN | int | Relais Hydraulikpumpe |
| STAT_GETRIEBE_OEL_PUMPE_EIN | int | Relais Getriebeoelpumpe |
| STAT_TREIBER1_NOTANSTEUERUNG_EIN | int | Notansteuerung Treiber 1, Trouble Shot Down Driver, (kommt lowaktiv vom SG, in SGBD invertiert), 0 = aus, 1= ein (lowaktiv!) |
| STAT_TREIBER2_NOTANSTEUERUNG_EIN | int | Notansteuerung Treiber 2, Trouble Shot Down Driver, (kommt lowaktiv vom SG, in SGBD invertiert), 0 = aus, 1= ein (lowaktiv!) |
| STAT_TREIBER3_NOTANSTEUERUNG_EIN | int | Notansteuerung Treiber 3, Trouble Shot Down Driver, (kommt lowaktiv vom SG, in SGBD invertiert), 0 = aus, 1= ein (lowaktiv!) |
| STAT_HANDBREMSE_EIN | int | Handbremse, 0=aus, 1=ein |
| STAT_WAEHLHEBEL_S1_EIN | int | Wählehebelschalter S1 |
| STAT_WAEHLHEBEL_S2_EIN | int | Wählehebelschalter S2 |
| STAT_WAEHLHEBEL_E1_EIN | int | Wählehebelschalter E1 |
| STAT_WAEHLHEBEL_E2_EIN | int | Wählehebelschalter E2 |
| STAT_WAEHLHEBEL_N1_EIN | int | Wählehebelschalter N1 |
| STAT_WAEHLHEBEL_N2_EIN | int | Wählehebelschalter N2 |
| STAT_WAEHLHEBEL_R1_EIN | int | Wählehebelschalter R1 |
| STAT_WAEHLHEBEL_R2_EIN | int | Wählehebelschalter R2 |
| STAT_MOTOR_EIN | int | Engine state. (Motordrehzahlschalter fuer Sicherheitsfunktion. 0 = Motordrehzahl &lt; 200, 1 = Motordrehzahl &gt; 200) |
| STAT_SPORT_ADD_EIN | int | Programmwahlschalter + |
| STAT_SPORT_SUB_EIN | int | Programmwahlschalter - |
| STAT_MOTORHAUBE1_EIN | int | Motorhaubenkontakt 1 (links) 0 = auf oder 1 = zu |
| STAT_MOTORHAUBE2_EIN | int | Motorhaubenkontakt 2 (rechts) 0 = auf oder 1 = zu |
| STAT_WAKE_UP | int | Wake up 0 = aus, 1 = ein |
| STAT_LENKRADTASTER_PLUS_AKTIV | int | Lenkradtaster PLUS (rechts) 0 = nicht gezogen, 1 = gezogen |
| STAT_LENKRADTASTER_MINUS_AKTIV | int | Lenkradtaster MINUS (links) 0 = nicht gezogen, 1 = gezogen |
| STAT_KUPPLUNG_WERT | int | Kupplungsstatus-Text, siehe table FUmweltTexte4 WERT UWTEXT table FUmweltTexte4 WERT |
| STAT_KUPPLUNG_TEXT | string | Kupplungsstatus-Text, siehe table FUmweltTexte4 WERT UWTEXT table FUmweltTexte4 TEXT |
| STAT_ISTGANG_WERT | int | Getriebeuebersetzung: N,1,2,3,4,5,6,R- Text, siehe table FUmweltTexte1 WERT UWTEXT table FUmweltTexte1 WERT |
| STAT_ISTGANG_TEXT | string | Getriebeuebersetzung: N,1,2,3,4,5,6,R- Text, siehe table FUmweltTexte1 WERT UWTEXT table FUmweltTexte1 TEXT |
| STAT_GETRIEBE_WERT | int | Getriebestatus-Text, siehe table FUmweltTexte3 WERT UWTEXT table FUmweltTexte3 WERT |
| STAT_GETRIEBE_TEXT | string | Getriebestatus-Text, siehe table FUmweltTexte3 WERT UWTEXT table FUmweltTexte3 TEXT |
| STAT_WAEHLHEBELSTELLUNG_WERT | int | Waehlhebelstellung: R,0,A,S,+,-,n.def. -Text, siehe table FUmweltTexte5 WERT UWTEXT table FUmweltTexte5 WERT |
| STAT_WAEHLHEBELSTELLUNG_TEXT | string | Waehlhebelstellung: R,0,A,S,+,-,n.def. -Text, siehe table FUmweltTexte5 WERT UWTEXT table FUmweltTexte5 TEXT |
| STAT_FGR_WERT | int | Fahrgeschwingigkeitsregler (FGR) Status-Text table FGR WERT |
| STAT_FGR_TEXT | string | Fahrgeschwingigkeitsregler (FGR) Status-Text table FGR TEXT |
| STAT_WARM_UP_CYCLE_ERFUELLT | int | Warm Up Cycle erfuellt. |
| STAT_TRIP_ERFUELLT | int | Trip erfuellt |
| STAT_DRIVING_CYCLE_ON | int | Driving Cycle erfuellt bzw. begonnen. |
| STAT_FREEZE_FRAME_REFERENZ_WERT | int | Freeze Frame-Text wird verwaltet fuer, siehe table FREEZE_FRAME_REFERENZ WERT ANZEIGE_TEXT table FREEZE_FRAME_REFERENZ WERT |
| STAT_FREEZE_FRAME_REFERENZ_TEXT | string | Freeze Frame-Text wird verwaltet fuer, siehe table FREEZE_FRAME_REFERENZ WERT ANZEIGE_TEXT table FREEZE_FRAME_REFERENZ TEXT |
| STAT_PROGRAMMINFO_WERT | int | 1. - 6. Programm-Text. Muss mit Anzahl der Balken im Kombi uebereinstimmen. Wird ueber Taster vor Waehlhebel eingestellt. siehe table PROGRAMMINFO WERT ANZEIGE_TEXT table PROGRAMMINFO WERT |
| STAT_PROGRAMMINFO_TEXT | string | 1. - 6. Programm-Text. Muss mit Anzahl der Balken im Kombi uebereinstimmen. Wird ueber Taster vor Waehlhebel eingestellt. siehe table PROGRAMMINFO WERT ANZEIGE_TEXT table PROGRAMMINFO TEXT |
| STAT_KOMFORTINDEX_WERT | int | Komfortindex-Text 0 - 12. Ausgabe abhängig von Gang und Fahrweise. siehe table KOMFORTINDEX WERT ANZEIGE_TEXT table KOMFORTINDEX WERT |
| STAT_KOMFORTINDEX_TEXT | string | Komfortindex-Text 0 - 12. Ausgabe abhängig von Gang und Fahrweise. siehe table KOMFORTINDEX WERT ANZEIGE_TEXT table KOMFORTINDEX TEXT |
| STAT_GANGANZEIGE_WERT | int | Ganganzeige-Text im Kombi. siehe table GANGANZEIGE WERT ANZEIGE_TEXT table GANGANZEIGE WERT |
| STAT_GANGANZEIGE_TEXT | string | Ganganzeige-Text im Kombi. siehe table GANGANZEIGE WERT ANZEIGE_TEXT table GANGANZEIGE TEXT |
| STAT_WAEHLHEBELANZEIGE_WERT | int | Waehlhebelanzeige table WAEHLHEBELANZEIGE WERT |
| STAT_WAEHLHEBELANZEIGE_TEXT | string | Waehlhebelanzeige table WAEHLHEBELANZEIGE TEXT |
| STAT_FAHRZUSTAND_WERT | int | Fahrzustand table InfoTexteFahrzeugzustand WERT |
| STAT_FAHRZUSTAND_TEXT | string | Fahrzustand table InfoTexteFahrzeugzustand TEXT |
| STAT_GET_LOCAL_TRIP_ERREICHT | int | GET local Trip erreicht |
| STAT_FREEZE_FRAME_GESPEICHERT | int | Freeze frame gespeichert |
| STAT_MIL_EIN | int | MIL 0 = aus, 1 = ein |
| STAT_MIL_BLINK_EIN | int | MIL blink 0 = aus, 1 = blink |
| STAT_KLR_EIN | int | Klemme R / Radio 0 = aus, 1 = ein (über CAN) |
| STAT_KL15_EIN | int | Klemme 15 / Zuendung 0 = aus, 1 = ein (über CAN) |
| STAT_KL50_EIN | int | Klemme 50 / Anlasser 0 = aus, 1 = ein (über CAN) |
| STAT_EINLERNVORGANG_OFFSET_LAENGSBESCHL_OKAY | int | Einlernvorgang Offset Laengsbeschleunigungssenor: 0=nicht eingelernt, 1=eingelernt |
| STAT_EINLERNVORGANG_KUPPLUNGSVENTILKENNWERTE_OKAY | int | Einlernvorgang Kupplungsventilkennwerte: 0=nicht eingelernt, 1=eingelernt |
| STAT_EINLERNVORGANG_GETRIEBE_OKAY | int | Einlernvorgang Getriebe komplett: 0=nicht eingelernt, 1=eingelernt |
| STAT_EINLERNVORGANG_KUPPLUNGSSCHLEIFPUNKT_OKAY | int | Einlernvorgang Kupplungsschleifpunkt: 0=nicht eingelernt, 1=eingelernt |
| STAT_BREMSLICHTSCHALTER_EIN | int | 1 = Bremslichtschalter betätigt |
| STAT_BREMSLICHTTESTSCHALTER_EIN | int | 1 = Bremslichttestschalter betätigt |
| STAT_ANHAENGERBETRIEB_EIN | int | 1 = Anhängerbetrieb aktiv |
| STAT_KICK_DOWN_EIN | int | 1 = Kick down ist betaetigt |
| STAT_MOTORHAUBE_EIN | int | 1 = beide Motorhaubenkontakte sind geschlossen |
| STAT_TUER_ZU | int | 0 = Fahrertuer offen, 1 = Fahrertuer geschlossen |
| STAT_FGR_SOLLMOMENT | int | 1 = Fahrgeschwindigkeitsregler Sollmoment |
| STAT_POS2_KUP_WERT | real | Istposition Kupplung Redundant, Bereich: 0-1023 Inkremente Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_POS2_KUP_EINH | string | Istposition Kupplung Redundant, Bereich: 0-1023 Inkremente Einheit: Ink |
| STAT_WAEHLHEBEL_LED_N_EIN | int | Waehlhebel LED Neutral, 0=aus, 1=ein |
| STAT_WAEHLHEBEL_LED_R_EIN | int | Waehlhebel LED Rueckwaerts, 0=aus, 1=ein |
| STAT_WAEHLHEBEL_LED_DS_EIN | int | Waehlhebel LED D oder S, 0=aus, 1=ein |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrzeugtester"></a>
### STATUS_FAHRZEUGTESTER

mit dem SGBD-Generator erzeugt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOTORDREHZAHL_ROH_WERT | real | Motordrehzahl Rohwert Bereich von 0 [Ink] bis 10000 [Ink] |
| STAT_MOTORDREHZAHL_ROH_EINH | string | Motordrehzahl Rohwert Einheit: Ink |
| STAT_MOTORDREHZAHL_CAN_WERT | real | Motordrezahl von CAN Bereich von 0 [Ink] bis 10000 [Ink] |
| STAT_MOTORDREHZAHL_CAN_EINH | string | Motordrezahl von CAN Einheit: Ink |
| STAT_EINGANGSDREHZAHL_ROH_WERT | real | Getriebeeingangsdrehzahl, Rohwert Bereich von 0 [Ink] bis 10000 [Ink] |
| STAT_EINGANGSDREHZAHL_ROH_EINH | string | Getriebeeingangsdrehzahl, Rohwert Einheit: Ink |
| STAT_RADGESCHWINDIGKEIT_VL_ROH_WERT | real | Radgeschwindigkeit vorne links, Rohwert Bereich von -300 [Ink] bis 300 [Ink] |
| STAT_RADGESCHWINDIGKEIT_VL_ROH_EINH | string | Radgeschwindigkeit vorne links, Rohwert Einheit: Ink |
| STAT_RADGESCHWINDIGKEIT_VR_ROH_WERT | real | Radgeschwindigkeit vorne rechts, Rohwert Bereich von -300 [Ink] bis 3000 [Ink] |
| STAT_RADGESCHWINDIGKEIT_VR_ROH_EINH | string | Radgeschwindigkeit vorne rechts, Rohwert Einheit: Ink |
| STAT_RADGESCHWINDIGKEIT_HL_ROH_WERT | real | Radgeschwindigkeit hinten links, Rohwert Bereich von -300 [Ink] bis 300 [Ink] |
| STAT_RADGESCHWINDIGKEIT_HL_ROH_EINH | string | Radgeschwindigkeit hinten links, Rohwert Einheit: Ink |
| STAT_RADGESCHWINDIGKEIT_HR_ROH_WERT | real | Radgeschwindigkeit hinten rechts, Rohwert Bereich von -300 [Ink] bis 300 [Ink] |
| STAT_RADGESCHWINDIGKEIT_HR_ROH_EINH | string | Radgeschwindigkeit hinten rechts, Rohwert Einheit: Ink |
| STAT_MOTORTEMPERATUR_ROH_WERT | real | Motortemperatur (Kuehlwasser), Rohwert Bereich von -48 [Ink] bis 205 [Ink] |
| STAT_MOTORTEMPERATUR_ROH_EINH | string | Motortemperatur (Kuehlwasser), Rohwert Einheit: Ink |
| STAT_MOTOROELTEMPERATUR_ROH_WERT | real | Motoroeltemperatur, Rohwert Bereich von -48 [Ink] bis 205 [Ink] |
| STAT_MOTOROELTEMPERATUR_ROH_EINH | string | Motoroeltemperatur, Rohwert Einheit: Ink |
| STAT_HYDRAULIKTEMPERATUR_ROH_WERT | real | Hydrauliktemperatur, Rohwert Bereich von 0 [Ink] bis 5 [Ink] |
| STAT_HYDRAULIKTEMPERATUR_ROH_EINH | string | Hydrauliktemperatur, Rohwert Einheit: Ink |
| STAT_UMGEBUNGSTEMPERATUR_ROH_WERT | real | Umgebungstemperatur/Aussenlufttemperatur, Rohwert Bereich von -48 [Ink] bis 85 [Ink] |
| STAT_UMGEBUNGSTEMPERATUR_ROH_EINH | string | Umgebungstemperatur/Aussenlufttemperatur, Rohwert Einheit: Ink |
| STAT_UBAT_ROH_WERT | real | Batteriespannung (KL.30), Rohwert Bereich von 0 [Ink] bis 25,6 [Ink] |
| STAT_UBAT_ROH_EINH | string | Batteriespannung (KL.30), Rohwert Einheit: Ink |
| STAT_USENSA_ROH_WERT | real | Sensorversorgungsspannung A, Rohwert Bereich von 0 [Ink] bis 10000 [Ink] |
| STAT_USENSA_ROH_EINH | string | Sensorversorgungsspannung A, Rohwert Einheit: Ink |
| STAT_USENSB_ROH_WERT | real | Sensorversorgungsspannung B, Rohwert Bereich von 0 [Ink] bis 10000 [Ink] |
| STAT_USENSB_ROH_EINH | string | Sensorversorgungsspannung B, Rohwert Einheit: Ink |
| STAT_STROM_KUP_ROH_WERT | real | Iststrom Magnetventil Kupplung, Rohwert Bereich von 0 [Ink] bis 3000 [Ink] |
| STAT_STROM_KUP_ROH_EINH | string | Iststrom Magnetventil Kupplung, Rohwert Einheit: Ink |
| STAT_STROM_SCHALTZYLINDER_R_1_ROH_WERT | real | Iststrom Magnetventil PWV 1 (Proportional Wegeventil) / Schaltzylinder R/1, Rohwert Bereich von 0 [V] bis 3000 [V] |
| STAT_STROM_SCHALTZYLINDER_R_1_ROH_EINH | string | Iststrom Magnetventil PWV 1 (Proportional Wegeventil) / Schaltzylinder R/1, Rohwert Einheit: V |
| STAT_STROM_SCHALTZYLINDER_5_3_ROH_WERT | real | Sollstrom Magnetventil PWV 2 (Proportional Wegeventil) / Schaltzylinder 5/3, Rohwert Bereich von 0 [Ink] bis 3000 [Ink] |
| STAT_STROM_SCHALTZYLINDER_5_3_ROH_EINH | string | Sollstrom Magnetventil PWV 2 (Proportional Wegeventil) / Schaltzylinder 5/3, Rohwert Einheit: Ink |
| STAT_STROM_SCHALTZYLINDER_2_4_ROH_WERT | real | Iststrom Magnetventil PWV 3 (Proportional Wegeventil) / Schaltzylinder 2/4, Rohwert Bereich von 0 [Ink] bis 3000 [Ink] |
| STAT_STROM_SCHALTZYLINDER_2_4_ROH_EINH | string | Iststrom Magnetventil PWV 3 (Proportional Wegeventil) / Schaltzylinder 2/4, Rohwert Einheit: Ink |
| STAT_STROM_SCHALTZYLINDER_6_7_ROH_WERT | real | Iststrom Magnetventil PWV 4 (Proportional Wegeventil) / Schaltzylinder 6/7, Rohwert Bereich von 0 [Ink] bis 3000 [Ink] |
| STAT_STROM_SCHALTZYLINDER_6_7_ROH_EINH | string | Iststrom Magnetventil PWV 4 (Proportional Wegeventil) / Schaltzylinder 6/7, Rohwert Einheit: Ink |
| STAT_STROM_DRUCK_REGELVENTIL1_ROH_WERT | real | Iststrom Magnetventil DRV 1 (Druck Regelventil), Rohwert Bereich von 0 [Ink] bis 3000 [Ink] |
| STAT_STROM_DRUCK_REGELVENTIL1_ROH_EINH | string | Iststrom Magnetventil DRV 1 (Druck Regelventil), Rohwert Einheit: Ink |
| STAT_STROM_DRUCK_REGELVENTIL2_ROH_WERT | real | Iststrom Magnetventil DRV 2 (Druck Regelventil), Rohwert Bereich von 0 [Ink] bis 3000 [Ink] |
| STAT_STROM_DRUCK_REGELVENTIL2_ROH_EINH | string | Iststrom Magnetventil DRV 2 (Druck Regelventil), Rohwert Einheit: Ink |
| STAT_POS_SCHALTSTANGE_R_1_ROH_WERT | real | Istposition Schaltstange R/1, Rohwert Bereich von 4 [Ink] bis 96 [Ink] |
| STAT_POS_SCHALTSTANGE_R_1_ROH_EINH | string | Istposition Schaltstange R/1, Rohwert Einheit: Ink |
| STAT_POS_SCHALTSTANGE_5_3_ROH_WERT | real | Istposition Schaltstange 5/3, Rohwert Bereich von 4 [Ink] bis 96 [Ink] |
| STAT_POS_SCHALTSTANGE_5_3_ROH_EINH | string | Istposition Schaltstange 5/3, Rohwert Einheit: Ink |
| STAT_POS_SCHALTSTANGE_2_4_ROH_WERT | real | Istposition Schaltstange 2/4, Rohwert Bereich von 4 [Ink] bis 96 [Ink] |
| STAT_POS_SCHALTSTANGE_2_4_ROH_EINH | string | Istposition Schaltstange 2/4, Rohwert Einheit: Ink |
| STAT_POS_SCHALTSTANGE_6_7_ROH_WERT | real | Istposition Schaltstange 6/7, Rohwert Bereich von 4 [Ink] bis 96 [Ink] |
| STAT_POS_SCHALTSTANGE_6_7_ROH_EINH | string | Istposition Schaltstange 6/7, Rohwert Einheit: Ink |
| STAT_POS2_SCHALTSTANGE_R_1_ROH_WERT | real | Redundante Istposition Schaltstange R/1, Rohwert Bereich von 4 [Ink] bis 96 [Ink] |
| STAT_POS2_SCHALTSTANGE_R_1_ROH_EINH | string | Redundante Istposition Schaltstange R/1, Rohwert Einheit: Ink |
| STAT_POS_KUP_ROH_WERT | real | Istposition Kupplung, Rohwert Bereich von 0 [Ink] bis 5 [Ink] |
| STAT_POS_KUP_ROH_EINH | string | Istposition Kupplung, Rohwert Einheit: Ink |
| STAT_POS_KUP2_ROH_WERT | real | Redundante Istposition Kupplung, Rohwert Bereich von 0 [Ink] bis 5 [Ink] |
| STAT_POS_KUP2_ROH_EINH | string | Redundante Istposition Kupplung, Rohwert Einheit: Ink |
| STAT_FAHRPEDAL_ROH_WERT | real | Fahrpedalwert, Rohwert Bereich von 0 [Ink] bis 254 [Ink] |
| STAT_FAHRPEDAL_ROH_EINH | string | Fahrpedalwert, Rohwert Einheit: Ink |
| STAT_AQUER_CAN_ROH_WERT | real | Querbeschleunigung von CAN, Rohwert Bereich von -20 [m/s^2] bis 20 [m/s^2] |
| STAT_AQUER_CAN_ROH_EINH | string | Querbeschleunigung von CAN, Rohwert Einheit: m/s^2 |
| STAT_ALAENGS_ROH_WERT | real | Laengsbeschleunigungsensor fuer SMG, Rohwert Bereich von 0 [Ink] bis 5 [Ink] |
| STAT_ALAENGS_ROH_EINH | string | Laengsbeschleunigungsensor fuer SMG, Rohwert Einheit: Ink |
| STAT_EINGANGSDREHZAHL_WERT | real | Getriebeeingangsdrehzahl Bereich von 0 [1/min] bis 10000 [1/min] |
| STAT_EINGANGSDREHZAHL_EINH | string | Getriebeeingangsdrehzahl Einheit: 1/min |
| STAT_HYDRAULIKDRUCK_ROH_WERT | real | Hydraulikdruck, Rohwert Bereich von 0 [Ink] bis 5 [Ink] |
| STAT_HYDRAULIKDRUCK_ROH_EINH | string | Hydraulikdruck, Rohwert Einheit: Ink |
| STAT_HANDBREMSE_EIN | int | Handbremse, 0=aus, 1=ein |
| STAT_WAEHLHEBEL_S1_EIN_ROH | int | Waehlehebelschalter S1, Rohwert |
| STAT_WAEHLHEBEL_S2_EIN_ROH | int | Waehlehebelschalter S2, Rohwert |
| STAT_WAEHLHEBEL_E1_EIN_ROH | int | Waehlehebelschalter E1, Rohwert |
| STAT_WAEHLHEBEL_E2_EIN_ROH | int | Waehlehebelschalter E2, Rohwert |
| STAT_WAEHLHEBEL_N1_EIN_ROH | int | Waehlehebelschalter N1, Rohwert |
| STAT_WAEHLHEBEL_N2_EIN_ROH | int | Waehlehebelschalter N2, Rohwert |
| STAT_WAEHLHEBEL_R1_EIN_ROH | int | Waehlehebelschalter R1, Rohwert |
| STAT_WAEHLHEBEL_R2_EIN_ROH | int | Waehlehebelschalter R2, Rohwert |
| STAT_MOTOR_EIN_ROH | int | Engine state. (Motordrehzahlschalter fuer Sicherheitsfunktion. 0 = Motordrehzahl &lt; 200, 1 = Motordrehzahl &gt; 200), Rohwert |
| STAT_SPORT_ADD_EIN_ROH | int | Programmwahlschalter PLUS, Rohwert |
| STAT_SPORT_SUB_EIN_ROH | int | Programmwahlschalter MINUS, Rohwert |
| STAT_MOTORHAUBE1_EIN_ROH | int | Motorhaubenkontakt 1 (links) 0 = auf oder 1 = zu, Rohwert |
| STAT_MOTORHAUBE2_EIN_ROH | int | Motorhaubenkontakt 2 (links) 0 = auf oder 1 = zu, Rohwert |
| STAT_WAKE_UP_ROH | int | Wake up 0 = aus, 1 = ein, Rohwert |
| STAT_LENKRADTASTER_PLUS_AKTIV_ROH | int | Lenkradtaster PLUS (rechts) 0 = nicht gezogen, 1 = gezogen, Rohwert |
| STAT_LENKRADTASTER_MINUS_AKTIV_ROH | int | Lenkradtaster MINUS (links) 0 = nicht gezogen, 1 = gezogen, Rohwert |
| STAT_SHIFT_LOCK_EIN | int | Shitf-Lock, 0= Waehlhebel gesperrt, 1= Waehlhebel frei |
| STAT_SCHALTER_RUECK_EIN | int | Rueckfahrlichtschalter, 0 = aus, 1 = ein |
| STAT_ANLASSERFREIGABE_AKTIV | int | Kupplung und Getriebe geben Anlasserfreigabe an DME |
| STAT_HYDRAULIK_PUMPE_EIN | int | Relais Hydraulikpumpe |
| STAT_TREIBER1_NOTANSTEUERUNG_EIN | int | Notansteuerung Treiber 1 , Trouble Shot Down Driver , (kommt lowaktiv vom SG, in SGBD invertiert), 0 = aus, 1= ein (lowaktiv!) |
| STAT_TREIBER2_NOTANSTEUERUNG_EIN | int | Notansteuerung Treiber 2 , Trouble Shot Down Driver , (kommt lowaktiv vom SG, in SGBD invertiert), 0 = aus, 1= ein (lowaktiv!) |
| STAT_TREIBER3_NOTANSTEUERUNG_EIN | int | Notansteuerung Treiber 3 , Trouble Shot Down Driver , (kommt lowaktiv vom SG, in SGBD invertiert), 0 = aus, 1= ein (lowaktiv!) |
| STAT_BREMSLICHTSCHALTER_EIN | int | Bremslichtschalter, 0 = Bremslichtschalter nicht betätigt,1 = Bremslichtschalter betätigt |
| STAT_BREMSLICHTTESTSCHALTER_EIN | int | Bremslichttestschalter, 0 = Bremslichttestschalter nicht betätigt,1 = Bremslichttestschalter betätigt |
| STAT_STOERANZEIGE_WERT | real | Störanzeige, 0 = aus, 1 = ein Bereich von 0 [--] bis 65535 [--] |
| STAT_STOERANZEIGE_EINH | string | Störanzeige, 0 = aus, 1 = ein Einheit: -- |
| STAT_AUSGANGSDREHZAHL_WERT | real | Getriebeausgangsdrehzahl Bereich von 0 [1/min] bis 10000 [1/min] |
| STAT_AUSGANGSDREHZAHL_EINH | string | Getriebeausgangsdrehzahl Einheit: 1/min |
| STAT_UMGEBUNGSTEMPERATUR_WERT | real | Umgebungstemperatur Bereich von -48 [Grad C] bis 205 [Grad C] |
| STAT_UMGEBUNGSTEMPERATUR_EINH | string | Umgebungstemperatur Einheit: Grad C |
| STAT_KUPPLUNG_WERT | int | Kupplungsstatus-Text, siehe table FUmweltTexte4 WERT UWTEXT table FUmweltTexte4 WERT |
| STAT_KUPPLUNG_TEXT | string | Kupplungsstatus-Text, siehe table FUmweltTexte4 WERT UWTEXT table FUmweltTexte4 TEXT |
| STAT_ISTGANG_WERT | int | Getriebeuebersetzung: N,1,2,3,4,5,6,R- Text, siehe table FUmweltTexte1 WERT UWTEXT table FUmweltTexte1 WERT |
| STAT_ISTGANG_TEXT | string | Getriebeuebersetzung: N,1,2,3,4,5,6,R- Text, siehe table FUmweltTexte1 WERT UWTEXT table FUmweltTexte1 TEXT |
| STAT_GETRIEBE_WERT | int | Getriebestatus-Text, siehe table FUmweltTexte3 WERT UWTEXT table FUmweltTexte3 WERT |
| STAT_GETRIEBE_TEXT | string | Getriebestatus-Text, siehe table FUmweltTexte3 WERT UWTEXT table FUmweltTexte3 TEXT |
| STAT_GANGANZEIGE_WERT | int | Ganganzeige-Text im Kombi. siehe table GANGANZEIGE WERT ANZEIGE_TEXT table GANGANZEIGE WERT |
| STAT_GANGANZEIGE_TEXT | string | Ganganzeige-Text im Kombi. siehe table GANGANZEIGE WERT ANZEIGE_TEXT table GANGANZEIGE TEXT |
| STAT_FAHRZUSTAND_WERT | int | Fahrzustand table InfoTexteFahrzeugzustand WERT |
| STAT_FAHRZUSTAND_TEXT | string | Fahrzustand table InfoTexteFahrzeugzustand TEXT |
| STAT_KLR_EIN_ROH | int | Klemme R / Radio 0 = aus, 1 = ein, Rohwert |
| STAT_KL15_ROH | int | Klemme 15 / Zuendung 0 = aus, 1 = ein, Rohwert |
| STAT_KL50_EIN_ROH | int | Klemme 50 / Anlasser 0 = aus, 1 = ein, Rohwert |
| STAT_SOLLGANG_WERT | int | Getriebeuebersetzung: N,1,2,3,4,5,6,R- Text, siehe table FUmweltTexte1 WERT UWTEXT table FUmweltTexte1 WERT |
| STAT_SOLLGANG_TEXT | string | Getriebeuebersetzung: N,1,2,3,4,5,6,R- Text, siehe table FUmweltTexte1 WERT UWTEXT table FUmweltTexte1 TEXT |
| STAT_GESCHWINDIGKEIT_HINTERACHSE_WERT | real | Fahrzeuggeschwindigkeit der Hinterachse Bereich von -300 [km/h] bis 300 [km/h] |
| STAT_GESCHWINDIGKEIT_HINTERACHSE_EINH | string | Fahrzeuggeschwindigkeit der Hinterachse Einheit: km/h |
| STAT_SOLL_STROM_KUP_WERT | real | Sollstrom Magnetventil Kupplung Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_KUP_EINH | string | Sollstrom Magnetventil Kupplung Einheit: mA |
| STAT_SOLL_STROM_SCHALTZYLINDER_R_1_WERT | real | Sollstrom Magnetventil PWV 1 (Proportional Wegeventil) / Schaltzylinder R/1 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_SCHALTZYLINDER_R_1_EINH | string | Sollstrom Magnetventil PWV 1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: mA |
| STAT_SOLL_STROM_SCHALTZYLINDER_5_3_WERT | real | Sollstrom Magnetventil PWV 2 (Proportional Wegeventil) / Schaltzylinder 5/3 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_SCHALTZYLINDER_5_3_EINH | string | Sollstrom Magnetventil PWV 2 (Proportional Wegeventil) / Schaltzylinder 5/3 Einheit: mA |
| STAT_SOLL_STROM_SCHALTZYLINDER_2_4_WERT | real | Sollstrom Magnetventil PWV 3 (Proportional Wegeventil) / Schaltzylinder 2/4 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_SCHALTZYLINDER_2_4_EINH | string | Sollstrom Magnetventil PWV 3 (Proportional Wegeventil) / Schaltzylinder 2/4 Einheit: mA |
| STAT_SOLL_STROM_SCHALTZYLINDER_6_7_WERT | real | Sollstrom Magnetventil PWV 4 (Proportional Wegeventil) / Schaltzylinder 6/7 Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_SCHALTZYLINDER_6_7_EINH | string | Sollstrom Magnetventil PWV 4 (Proportional Wegeventil) / Schaltzylinder 6/7 Einheit: mA |
| STAT_SOLL_STROM_DRUCKREGELVENTIL1_WERT | real | Sollstrom Magnetventil DRV 1 (Druck Regelventil) Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_DRUCKREGELVENTIL1_EINH | string | Sollstrom Magnetventil DRV 1 (Druck Regelventil) Einheit: mA |
| STAT_SOLL_STROM_DRUCKREGELVENTIL2_WERT | real | Sollstrom Magnetventil DRV 2 (Druck Regelventil) Bereich von 0 [mA] bis 3000 [mA] |
| STAT_SOLL_STROM_DRUCKREGELVENTIL2_EINH | string | Sollstrom Magnetventil DRV 2 (Druck Regelventil) Einheit: mA |
| STAT_SOLL_POS_SCHALTSTANGE_R_1_WERT | real | Sollpostion Schaltstange R/1 Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_SOLL_POS_SCHALTSTANGE_R_1_EINH | string | Sollpostion Schaltstange R/1 Einheit: Ink |
| STAT_SOLL_POS_SCHALTSTANGE_5_3_WERT | real | Sollpostion Schaltstange 5/3 Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_SOLL_POS_SCHALTSTANGE_5_3_EINH | string | Sollpostion Schaltstange 5/3 Einheit: Ink |
| STAT_SOLL_POS_SCHALTSTANGE_2_4_WERT | real | Sollpostion Schaltstange 2/4 Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_SOLL_POS_SCHALTSTANGE_2_4_EINH | string | Sollpostion Schaltstange 2/4 Einheit: Ink |
| STAT_SOLL_POS_SCHALTSTANGE_6_7_WERT | real | Sollpostion Schaltstange 6/7 Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_SOLL_POS_SCHALTSTANGE_6_7_EINH | string | Sollpostion Schaltstange 6/7 Einheit: Ink |
| STAT_SOLL_POS_KUP_WERT | real | Sollposition Kupplung Bereich von 0 [Ink] bis 1023 [Ink] |
| STAT_SOLL_POS_KUP_EINH | string | Sollposition Kupplung Einheit: Ink |
| STAT_MOTORMOMENT_WERT | real | Motormoment Bereich von -1024 [NM] bis 1024 [NM] |
| STAT_MOTORMOMENT_EINH | string | Motormoment Einheit: NM |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-programmerstellung"></a>
### PROGRAMMERSTELLUNG

Datum der Programmerstellung (speziell fuer GETRAG) (Service ID 0x30, Identifier 0xA4)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| PRG_DATUM | string | Programmerstelldatum (Tag.Monat.Jahr) |
| PRG_DATUM_JAHR | int | Programmerstelldatum (Jahr) |
| PRG_DATUM_MONAT | int | Programmerstelldatum (Monat) |
| PRG_DATUM_TAG | int | Programmerstelldatum (TAG) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-rbm-ratio"></a>
### RBM_RATIO

Dient zum Auslesen der OBD fehlerbezogenen RBM - Ratios (speziell fuer GETRAG) (Service ID 0x22, Identifier 0x53, 0x00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN_HEX | binary | Inhalt der Speicherzellen als Hex-Dump |
| IGNITION_CYCLE_COUNTER | unsigned int | Wert= 0..65534 |
| GENERAL_DENOMINATOR | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_1 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_1 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_2 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_2 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_3 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_3 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_4 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_4 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_5 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_5 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_6 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_6 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_7 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_7 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_8 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_8 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_9 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_9 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_10 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_10 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_11 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_11 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_12 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_12 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_13 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_13 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_14 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_14 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_15 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_15 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_16 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_16 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_17 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_17 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_18 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_18 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_19 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_19 | unsigned int | Wert= 0..65534 |
| NUMERATOR_DIAGNOSE_20 | unsigned int | Wert= 0..65534 |
| DENOMINATOR_DIAGNOSE_20 | unsigned int | Wert= 0..65534 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes ---zusätzlich für VS: -------------------------- KWP2000: $30 A2 ADAPTIONSWERTE_GETRIEBE KWP2000: $22 10 VERSCHLEISSDATEN_LESEN KWP2000: $30 A0 ADAPTIONSWERTE_KUPPLUNG KWP2000: $30 A1 ADAPTIONSWERTE_KUPPLUNGSKENNLINIE KWP2000: $30 A3 ADAPTIONSWERTE_EINKUPPELZEITEN Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

<a id="job-adaptionswerte-kupplung"></a>
### ADAPTIONSWERTE_KUPPLUNG

Adaptionswerte lesen (Service ID 0x30, Identifier 0xA0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN_HEX | binary | Inhalt der Speicherzellen |
| KUPPL_SCHLEIF_PKT_WERT | unsigned int | Kupplungsschleifpunkt (GW) ohne Quantisierung/Umrechnung ---ACHTUNG------------------------------------ ---Wert nur bei erfolgreicher----------------- ---Kupplungsschleifpunkt-Adaption gueltig!!--- ---------------------------------------------- Min.: 72, Default: 124 Ink, Max.: 225 |
| I_NULL_VENT_KUPPL_WERT | unsigned int | Nullstrom Kupplungsventil Min.: 900, Default: 1050 mA, Max.: 1300 |
| UEBERDECKUNG_VENT_KUPPL_WERT | unsigned int | Ventilueberdeckung Kupplung Min.: 0, Default: 100 mA, Max.: 300 |
| POS_EINKUP_WERT | unsigned int | Einkuppelstellung (EK) Min.: 550, Default: 650 Ink, Max.: 1150 Hinweis: Differenz AK zu EK ist min.: 360 Ink, Default: 410 Ink, max.: 460 |
| POS_AUSKUP_WERT | unsigned int | Auskuppelstellung (AK) Min.: 100, Default: 200 Ink, Max.: 700 Hinweis: Differenz AK zu EK ist min. 360 Ink, Default: 410 Ink, max.: 460 |
| DIFF_V_ACHS_WERT | real | Geschwindigkeitsdifferenz der Achsen Min.: -8, Default: 0 km/h, Max.: 8 km/h |
| ZAHL_KUPPL_UEBERLAST_WERT | unsigned int | Anzahl der Kupplungsueberlastungen Min.: 0, Default: 0, Max.: 255 |
| M_KUPPL_MAX_WERT | unsigned int | max. uebertragbares Kupplungsmoment Min.: 500, Default: 850 Nm, Max.: 1000 |
| ADAPT_P0_WERT | unsigned int | Adaptionswert Kupplungslageregler P0 Min.: 5, Default: 50, Max.: 150 |
| ADAPT_P1_WERT | unsigned int | Adaptionswert Kupplungslageregler P1 Min.: 10, Default: 80, Max.: 200 |
| ADAPT_P2_WERT | unsigned int | Adaptionswert Kupplungslageregler P2 Min.: 40, Default: 100, Max.: 250 |
| ADAPT_P3_WERT | unsigned int | Adaptionswert Kupplungslageregler P3 Min.: 40, Default: 100, Max.: 250 |
| ADAPT_P4_WERT | unsigned int | Adaptionswert Kupplungslageregler P4 Min.: 10, Default: 80, Max.: 200 |
| ADAPT_P5_WERT | unsigned int | Adaptionswert Kupplungslageregler P5 Min.: 5, Default: 50, Max.: 150 |
| ADAPT_SMIN_WERT | unsigned int | Adaptionswert Nullstromkennlinie smin Min.: 0, Default: 0 mA, Max.: 65535 |
| ADAPT_SMAX_WERT | unsigned int | Adaptionswert Nullstromkennlinie smax Min.: 0, Default: 0 mA, Max.: 65535 |
| ADAPT_IMIN_WERT | unsigned int | Adaptionswert Nullstromkennlinie imin Min.: 0, Default: 0 mA, Max.: 65535 |
| ADAPT_IMAX_WERT | unsigned int | Adaptionswert Nullstromkennlinie imax Min.: 0, Default: 0 mA, Max.: 65535 |
| NULLPUNKT_KUPPL_POS_WERT | int | Nullpunkt der Kupplungsposition Min.: -30, Default: 100 Ink, Max.: 400 |
| KUPPL_SCHLEIF_PKT_EINH | string | Einheit: keine |
| KUPPL_SCHLEIF_PKT_INK_EINH | string | Einheit: (Ink)remente |
| I_NULL_VENT_KUPPL_EINH | string | Einheit |
| UEBERDECKUNG_VENT_KUPPL_EINH | string | Einheit |
| POS_EINKUP_EINH | string | Einheit |
| POS_AUSKUP_EINH | string | Einheit |
| DIFF_V_ACHS_EINH | string | Einheit |
| ZAHL_KUPPL_UEBERLAST_EINH | string | Einheit |
| M_KUPPL_MAX_EINH | string | Einheit |
| ADAPT_P0_EINH | string | Einheit |
| ADAPT_P1_EINH | string | Einheit |
| ADAPT_P2_EINH | string | Einheit |
| ADAPT_P3_EINH | string | Einheit |
| ADAPT_P4_EINH | string | Einheit |
| ADAPT_P5_EINH | string | Einheit |
| ADAPT_SMIN_EINH | string | Einheit |
| ADAPT_SMAX_EINH | string | Einheit |
| ADAPT_IMIN_EINH | string | Einheit |
| ADAPT_IMAX_EINH | string | Einheit |
| NULLPUNKT_KUPPL_POS_EINH | string | Einheit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-kupplungskennlinie"></a>
### ADAPTIONSWERTE_KUPPLUNGSKENNLINIE

Adaptionswerte lesen (Service ID 0x30, Identifier 0xA1)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN_HEX | binary | Inhalt der Speicherzellen als Hex-Dump |
| ADAPT_K1_WERT | unsigned int | Adaptionswert Kupplungskennlinie K1 Min.: 7, Default: 47, Max.: 63 |
| ADAPT_K2_WERT | unsigned int | Adaptionswert Kupplungskennlinie K2 Min.: 17, Default: 69, Max.: 106 |
| ADAPT_K3_WERT | unsigned int | Adaptionswert Kupplungskennlinie K3 Min.: 25, Default: 87, Max.: 145 |
| ADAPT_K4_WERT | unsigned int | Adaptionswert Kupplungskennlinie K4 Min.: 34, Default: 100, Max.: 176 |
| ADAPT_K6_WERT | unsigned int | Adaptionswert Kupplungskennlinie K6 Min.: 49, Default: 121, Max.: 217 |
| ADAPT_K8_WERT | unsigned int | Adaptionswert Kupplungskennlinie K8 Min.: 66, Default: 140, Max.: 231 |
| ADAPT_K11_WERT | unsigned int | Adaptionswert Kupplungskennlinie K11 Min.: 91, Default: 163, Max.: 235 |
| ADAPT_K15_WERT | unsigned int | Adaptionswert Kupplungskennlinie K15 Min.: 128, Default: 190, Max.: 239 |
| ADAPT_K20_WERT | unsigned int | Adaptionswert Kupplungskennlinie K20 Min.: 170, Default: 216, Max.: 244 |
| ADAPT_K25_WERT | unsigned int | Adaptionswert Kupplungskennlinie K25 Min.: 212, Default: 237, Max.: 149 |
| ADAPT_K_EINH | string | Einheit aller K*-Kennlinien |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-getriebe"></a>
### ADAPTIONSWERTE_GETRIEBE

Adaptionswerte lesen (Service ID 0x30, Identifier 0xA2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN_HEX | binary | Inhalt der Speicherzellen als Hex-Dump |
| OFF_LAENGSB_SENSOR_WERT | int | Offsetwert des Längsbeschleunigungssensors min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| OFF_STROM_SCHALTZYLINDER_R_1_VOR_WERT | unsigned int | Offsetstrom PWV1 Richtung Schaltzylinder vor PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 min: 500 mA, Default: 600 mA, max: 700 mA |
| OFF_STROM_SCHALTZYLINDER_R_1_RUECK_WERT | unsigned int | Offsetstrom PWV1 Richtung Schaltzylinder rueck PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 min: 1700 mA, Default: 1800 mA, max: 1900 mA |
| OFF_STROM_SCHALTZYLINDER_R_1_SPERRL_WERT | unsigned int | Offsetstrom PWV1 Richtung Schaltzylinder in Sperrlage PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 min: 1100 mA, Default: 1200 mA, max: 1300 mA |
| OFF_STROM_SCHALTZYLINDER_5_3_VOR_WERT | unsigned int | Offsetstrom PWV2 Richtung Schaltzylinder vor PWV1 (Proportional Wegeventil) / Schaltzylinder 5/3 min: 500 mA, Default: 600 mA, max: 700 mA |
| OFF_STROM_SCHALTZYLINDER_5_3_RUECK_WERT | unsigned int | Offsetstrom PWV2 Richtung Schaltzylinder rueck PWV1 (Proportional Wegeventil) / Schaltzylinder 5/3 min: 1700 mA, Default: 1800 mA, max: 1900 mA |
| OFF_STROM_SCHALTZYLINDER_5_3_SPERRL_WERT | unsigned int | Offsetstrom PWV2 Richtung Schaltzylinder in Sperrlage PWV1 (Proportional Wegeventil) / Schaltzylinder 5/3 min: 1100 mA, Default: 1200 mA, max: 1300 mA |
| OFF_STROM_SCHALTZYLINDER_6_7_VOR_WERT | unsigned int | Offsetstrom PWV3 Richtung Schaltzylinder vor PWV1 (Proportional Wegeventil) / Schaltzylinder 6/7 min: 500 mA, Default: 600 mA, max: 700 mA |
| OFF_STROM_SCHALTZYLINDER_6_7_RUECK_WERT | unsigned int | Offsetstrom PWV3 Richtung Schaltzylinder rueck PWV1 (Proportional Wegeventil) / Schaltzylinder 6/7 min: 1700 mA, Default: 1800 mA, max: 1900 mA |
| OFF_STROM_SCHALTZYLINDER_6_7_SPERRL_WERT | unsigned int | Offsetstrom PWV3 Richtung Schaltzylinder in Sperrlage PWV1 (Proportional Wegeventil) / Schaltzylinder 6/7 min: 1100 mA, Default: 1200 mA, max: 1300 mA |
| OFF_STROM_SCHALTZYLINDER_2_4_VOR_WERT | unsigned int | Offsetstrom PWV3 Richtung Schaltzylinder vor PWV1 (Proportional Wegeventil) / Schaltzylinder 2/4 min: 500 mA, Default: 600 mA, max: 700 mA |
| OFF_STROM_SCHALTZYLINDER_2_4_RUECK_WERT | unsigned int | Offsetstrom PWV3 Richtung Schaltzylinder rueck PWV1 (Proportional Wegeventil) / Schaltzylinder 2/4 min: 1700 mA, Default: 1800 mA, max: 1900 mA |
| OFF_STROM_SCHALTZYLINDER_2_4_SPERRL_WERT | unsigned int | Offsetstrom PWV3 Richtung Schaltzylinder in Sperrlage PWV1 (Proportional Wegeventil) / Schaltzylinder 2/4 min: 1100 mA, Default: 1200 mA, max: 1300 mA |
| POS_SCHALTZYLINDER_R_1_GANG_R_WERT | int | Position Schaltzylinder R/1 Rueckwaertsgang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_VOR_SYNC_SCHALTZYLINDER_R_1_GANG_R_WERT | int | Position vor Synchronisation Schaltzylinder R/1 Rueckwaertsgang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_SCHALTZYLINDER_R_1_GANG_1_WERT | int | Position Schaltzylinder R/1 1. Gang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_VOR_SYNC_SCHALTZYLINDER_R_1_GANG_1_WERT | int | Position vor Synchronisation Schaltzylinder R/1 1. Gang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| KORR_SCHALTZYLINDER_R_1_GANG_R_WERT | unsigned int | Korrekturwert Position Schaltzylinder R/1 Rueckwaertsgang, Wert: signed 16 Bit min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| KORR_SCHALTZYLINDER_R_1_GANG_1_WERT | unsigned int | Korrekturwert Position Schaltzylinder R/1 1. Gang, Wert: signed 16 Bit min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS2_SCHALTZYLINDER_R_1_GANG_R_WERT | int | Redundante Position Schaltzylinder R/1 Rueckwaertsgang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS2_VOR_SYNC_SCHALTZYLINDER_R_1_GANG_R_WERT | int | Redundante Position Schaltzylinder R/1 Rueckwaertsgang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS2_SCHALTZYLINDER_R_1_GANG_1_WERT | int | Redundante Position Schaltzylinder R/1 1. Gang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS2_VOR_SYNC_SCHALTZYLINDER_R_1_GANG_1_WERT | int | Redundante Position vor Synchronisation Schaltzylinder R/1 1. Gang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| KORR2_SCHALTZYLINDER_R_1_GANG_R_WERT | int | Redundanter Korrekturwert Position Schaltzylinder R/1 Rueckwaertsgang, Wert: signed 16 Bit min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| KORR2_SCHALTZYLINDER_R_1_GANG_1_WERT | int | Redundanter Korrekturwert Position Schaltzylinder R/1 1. Gang, Wert: signed 16 Bit min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_SCHALTZYLINDER_5_3_GANG_5_WERT | int | Position Schaltzylinder 5/3 5. Gang PWV2 (Proportional Wegeventil) / Schaltzylinder 5/3 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_VOR_SYNC_SCHALTZYLINDER_5_3_GANG_5_WERT | int | Position Schaltzylinder 5/3 5. Gang PWV2 (Proportional Wegeventil) / Schaltzylinder 5/3 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_SCHALTZYLINDER_5_3_GANG_3_WERT | int | Position Schaltzylinder 5/3 3. Gang PWV2 (Proportional Wegeventil) / Schaltzylinder 5/3 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_VOR_SYNC_SCHALTZYLINDER_5_3_GANG_3_WERT | int | Position vor Synchronisation Schaltzylinder 5/3 3. Gang PWV2 (Proportional Wegeventil) / Schaltzylinder 5/3 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| KORR_SCHALTZYLINDER_5_3_GANG_5_WERT | unsigned int | Korrekturwert Position Schaltzylinder 5/3 5. Gang, Wert: signed 16 Bit min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| KORR_SCHALTZYLINDER_5_3_GANG_3_WERT | unsigned int | Korrekturwert Position Schaltzylinder 5/3 3. Gang, Wert: signed 16 Bit min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_SCHALTZYLINDER_2_4_GANG_2_WERT | int | Position Schaltzylinder 2/4 2. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 2/4 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_VOR_SYNC_SCHALTZYLINDER_2_4_GANG_2_WERT | int | Position vor Synchronisation Schaltzylinder 2/4 2. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 2/4 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_SCHALTZYLINDER_2_4_GANG_4_WERT | int | Position Schaltzylinder 2/4 4. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 2/4 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_VOR_SYNC_SCHALTZYLINDER_2_4_GANG_4_WERT | int | Position vor Synchronisation Schaltzylinder 2/4 4. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 2/4 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| KORR_SCHALTZYLINDER_2_4_GANG_2_WERT | unsigned int | Korrekturwert Position Schaltzylinder 2/4 2. Gang, Wert: signed 16 Bit min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| KORR_SCHALTZYLINDER_2_4_GANG_4_WERT | unsigned int | Korrekturwert Position Schaltzylinder 2/4 4. Gang, Wert: signed 16 Bit min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_SCHALTZYLINDER_6_7_GANG_6_WERT | int | Position Schaltzylinder 6/7 6. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 6/7 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_VOR_SYNC_SCHALTZYLINDER_6_7_GANG_6_WERT | int | Position vor Synchronisation Schaltzylinder 6/7 6. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 6/7 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_SCHALTZYLINDER_6_7_GANG_7_WERT | int | Position Schaltzylinder 6/7 7. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 6/7 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| POS_VOR_SYNC_SCHALTZYLINDER_6_7_GANG_7_WERT | int | Position vor Synchronisation Schaltzylinder 6/7 7. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 6/7 min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| KORR_SCHALTZYLINDER_6_7_GANG_6_WERT | unsigned int | Korrekturwert Position Schaltzylinder 6/7 6. Gang, Wert: signed 16 Bit min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| KORR_SCHALTZYLINDER_6_7_GANG_7_WERT | unsigned int | Korrekturwert Position Schaltzylinder 6/7 7. Gang, Wert: signed 16 Bit min: ??? Ink, Default: ??? Ink, max: ??? Ink |
| OFF_LAENGSB_SENSOR_EINH | string | Offsetwert des Laengsbeschleunigungssensors Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_R_1_VOR_EINH | string | Offsetstrom PWV1 Richtung Schaltzylinder vor PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_R_1_RUECK_EINH | string | Offsetstrom PWV1 Richtung Schaltzylinder rueck PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_R_1_SPERRL_EINH | string | Offsetstrom PWV1 Richtung Schaltzylinder in Sperrlage PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_5_3_VOR_EINH | string | Offsetstrom PWV2 Richtung Schaltzylinder vor PWV1 (Proportional Wegeventil) / Schaltzylinder 5/3 Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_5_3_RUECK_EINH | string | Offsetstrom PWV2 Richtung Schaltzylinder rueck PWV1 (Proportional Wegeventil) / Schaltzylinder 5/3 Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_5_3_SPERRL_EINH | string | Offsetstrom PWV2 Richtung Schaltzylinder in Sperrlage PWV1 (Proportional Wegeventil) / Schaltzylinder 5/3 Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_6_7_VOR_EINH | string | Offsetstrom PWV3 Richtung Schaltzylinder vor PWV1 (Proportional Wegeventil) / Schaltzylinder 6/7 Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_6_7_RUECK_EINH | string | Offsetstrom PWV3 Richtung Schaltzylinder rueck PWV1 (Proportional Wegeventil) / Schaltzylinder 6/7 Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_6_7_SPERRL_EINH | string | Offsetstrom PWV3 Richtung Schaltzylinder in Sperrlage Einheit: Ink (Inkremente) Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_2_4_VOR_EINH | string | Offsetstrom PWV3 Richtung Schaltzylinder vor PWV1 (Proportional Wegeventil) / Schaltzylinder 2/4 Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_2_4_RUECK_EINH | string | Offsetstrom PWV3 Richtung Schaltzylinder rueck PWV1 (Proportional Wegeventil) / Schaltzylinder 2/4 Einheit: Ink (Inkremente) |
| OFF_STROM_SCHALTZYLINDER_2_4_SPERRL_EINH | string | Offsetstrom PWV3 Richtung Schaltzylinder in Sperrlage PWV1 (Proportional Wegeventil) / Schaltzylinder 2/4 Einheit: Ink (Inkremente) |
| POS_SCHALTZYLINDER_R_1_GANG_R_EINH | string | Position Schaltzylinder R/1 Rueckwaertsgang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: Ink (Inkremente) |
| POS_VOR_SYNC_SCHALTZYLINDER_R_1_GANG_R_EINH | string | Position vor Synchronisation Schaltzylinder R/1 Rueckwaertsgang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: Ink (Inkremente) |
| POS_SCHALTZYLINDER_R_1_GANG_1_EINH | string | Position Schaltzylinder R/1 1. Gang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: Ink (Inkremente) |
| POS_VOR_SYNC_SCHALTZYLINDER_R_1_GANG_1_EINH | string | Position Schaltzylinder R/1 1. Gang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: Ink (Inkremente) |
| KORR_SCHALTZYLINDER_R_1_GANG_R_EINH | string | Korrekturwert Position Schaltzylinder R/1 Rueckwaertsgang, Wert: unsigned 8 Bit Einheit: Ink (Inkremente) |
| KORR_SCHALTZYLINDER_R_1_GANG_1_EINH | string | Korrekturwert Position Schaltzylinder R/1 1. Gang, Wert: unsigned 8 Bit Einheit: Ink (Inkremente) |
| POS2_SCHALTZYLINDER_R_1_GANG_R_EINH | string | Redundante Position Schaltzylinder R/1 Rueckwaertsgang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: Ink (Inkremente) |
| POS2_VOR_SYNC_SCHALTZYLINDER_R_1_GANG_R_EINH | string | Redundante Position Schaltzylinder R/1 Rueckwaertsgang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: Ink (Inkremente) |
| POS2_SCHALTZYLINDER_R_1_GANG_1_EINH | string | Redundante Position Schaltzylinder R/1 1. Gang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: Ink (Inkremente) |
| POS2_VOR_SYNC_SCHALTZYLINDER_R_1_GANG_1_EINH | string | Redundante Position vor Synchronisation Schaltzylinder R/1 1. Gang PWV1 (Proportional Wegeventil) / Schaltzylinder R/1 Einheit: Ink (Inkremente) |
| KORR2_SCHALTZYLINDER_R_1_GANG_R_EINH | string | Redundanter Korrekturwert Position Schaltzylinder R/1 Rueckwaertsgang, Wert: signed 16 Bit Einheit: Ink (Inkremente) |
| KORR2_SCHALTZYLINDER_R_1_GANG_1_EINH | string | Redundanter Korrekturwert Position Schaltzylinder R/1 1. Gang, Wert: signed 16 Bit Einheit: Ink (Inkremente) |
| POS_SCHALTZYLINDER_5_3_GANG_5_EINH | string | Position Schaltzylinder 5/3 5. Gang PWV2 (Proportional Wegeventil) / Schaltzylinder 5/3 Einheit: Ink (Inkremente) |
| POS_VOR_SYNC_SCHALTZYLINDER_5_3_GANG_5_EINH | string | Position Schaltzylinder 5/3 5. Gang PWV2 (Proportional Wegeventil) / Schaltzylinder 5/3 Einheit: Ink (Inkremente) |
| POS_SCHALTZYLINDER_5_3_GANG_3_EINH | string | Position Schaltzylinder 5/3 3. Gang PWV2 (Proportional Wegeventil) / Schaltzylinder 5/3 Einheit: Ink (Inkremente) |
| POS_VOR_SYNC_SCHALTZYLINDER_5_3_GANG_3_EINH | string | Position vor Synchronisation Schaltzylinder 5/3 3. Gang PWV2 (Proportional Wegeventil) / Schaltzylinder 5/3 Einheit: Ink (Inkremente) |
| KORR_SCHALTZYLINDER_5_3_GANG_5_EINH | string | Korrekturwert Position Schaltzylinder 5/3 5. Gang, Wert: unsigned 8 Bit Einheit: Ink (Inkremente) |
| KORR_SCHALTZYLINDER_5_3_GANG_1_EINH | string | Korrekturwert Position Schaltzylinder 5/3 3. Gang, Wert: unsigned 8 Bit Einheit: Ink (Inkremente) |
| POS_SCHALTZYLINDER_2_4_GANG_2_EINH | string | Position Schaltzylinder 2/4 2. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 2/4 Einheit: Ink (Inkremente) |
| POS_VOR_SYNC_SCHALTZYLINDER_2_4_GANG_2_EINH | string | Position vor Synchronisation Schaltzylinder 2/4 2. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 2/4 Einheit: Ink (Inkremente) |
| POS_SCHALTZYLINDER_2_4_GANG_4_EINH | string | Position Schaltzylinder 2/4 4. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 2/4 Einheit: Ink (Inkremente) |
| POS_VOR_SYNC_SCHALTZYLINDER_2_4_GANG_4_EINH | string | Position Schaltzylinder 2/4 4. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 2/4 Einheit: Ink (Inkremente) |
| KORR_SCHALTZYLINDER_2_4_GANG_2_EINH | string | Korrekturwert Position Schaltzylinder 2/4 2. Gang, Wert: unsigned 8 Bit Einheit: Ink (Inkremente) |
| KORR_SCHALTZYLINDER_2_4_GANG_4_EINH | string | Korrekturwert Position Schaltzylinder 2/4 4. Gang, Wert: unsigned 8 Bit Einheit: Ink (Inkremente) |
| POS_SCHALTZYLINDER_6_7_GANG_6_EINH | string | Position Schaltzylinder 6/7 6. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 6/7 Einheit: Ink (Inkremente) |
| POS_VOR_SYNC_SCHALTZYLINDER_6_7_GANG_6_EINH | string | Position vor Synchronisation Schaltzylinder 6/7 6. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 6/7 Einheit: Ink (Inkremente) |
| POS_SCHALTZYLINDER_6_7_GANG_7_EINH | string | Position Schaltzylinder 6/7 7. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 6/7 Einheit: Ink (Inkremente) |
| POS_VOR_SYNC_SCHALTZYLINDER_6_7_GANG_7_EINH | string | Position Schaltzylinder 6/7 7. Gang PWV4 (Proportional Wegeventil) / Schaltzylinder 6/7 Einheit: Ink (Inkremente) |
| KORR_SCHALTZYLINDER_6_7_GANG_6_EINH | string | Korrekturwert Position Schaltzylinder 6/7 6. Gang, Wert: unsigned 8 Bit Einheit: Ink (Inkremente) |
| KORR_SCHALTZYLINDER_6_7_GANG_7_EINH | string | Korrekturwert Position Schaltzylinder 6/7 7. Gang, Wert: unsigned 8 Bit Einheit: Ink (Inkremente) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-einkuppelzeiten"></a>
### ADAPTIONSWERTE_EINKUPPELZEITEN

Adaptionswerte lesen (Service ID 0x30, Identifier 0xA3)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN_HEX | binary | Inhalt der Speicherzellen als Hex-Dump |
| T_KL11_EK_ADAPT_1_WERT | unsigned int | Zeiten KL11 EK-Adaption 1.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL11_EK_ADAPT_2_WERT | unsigned int | Zeiten KL11 EK-Adaption 2.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL11_EK_ADAPT_3_WERT | unsigned int | Zeiten KL11 EK-Adaption 3.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL11_EK_ADAPT_4_WERT | unsigned int | Zeiten KL11 EK-Adaption 4.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL11_EK_ADAPT_5_WERT | unsigned int | Zeiten KL11 EK-Adaption 5.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL11_EK_ADAPT_6_WERT | unsigned int | Zeiten KL11 EK-Adaption 6.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL11_EK_ADAPT_7_WERT | unsigned int | Zeiten KL11 EK-Adaption 7.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL12_EK_ADAPT_1_WERT | unsigned int | Zeiten KL12 EK-Adaption 1.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL12_EK_ADAPT_2_WERT | unsigned int | Zeiten KL12 EK-Adaption 2.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL12_EK_ADAPT_3_WERT | unsigned int | Zeiten KL12 EK-Adaption 3.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL12_EK_ADAPT_4_WERT | unsigned int | Zeiten KL12 EK-Adaption 4.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL12_EK_ADAPT_5_WERT | unsigned int | Zeiten KL12 EK-Adaption 5.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL12_EK_ADAPT_6_WERT | unsigned int | Zeiten KL12 EK-Adaption 6.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL12_EK_ADAPT_7_WERT | unsigned int | Zeiten KL12 EK-Adaption 7.Gang, Wert: unsigned 8 Bit Default: 0 ms, min: - ms, max: - ms |
| T_KL11_EK_ADAPT_1_EINH | string | Einheit: -- |
| T_KL11_EK_ADAPT_2_EINH | string | Einheit: -- |
| T_KL11_EK_ADAPT_3_EINH | string | Einheit: -- |
| T_KL11_EK_ADAPT_4_EINH | string | Einheit: -- |
| T_KL11_EK_ADAPT_5_EINH | string | Einheit: -- |
| T_KL11_EK_ADAPT_6_EINH | string | Einheit: -- |
| T_KL11_EK_ADAPT_7_EINH | string | Einheit: -- |
| T_KL12_EK_ADAPT_1_EINH | string | Einheit: -- |
| T_KL12_EK_ADAPT_2_EINH | string | Einheit: -- |
| T_KL12_EK_ADAPT_3_EINH | string | Einheit: -- |
| T_KL12_EK_ADAPT_4_EINH | string | Einheit: -- |
| T_KL12_EK_ADAPT_5_EINH | string | Einheit: -- |
| T_KL12_EK_ADAPT_6_EINH | string | Einheit: -- |
| T_KL12_EK_ADAPT_7_EINH | string | Einheit: -- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-zuruecksetzen"></a>
### ADAPTIONSWERTE_ZURUECKSETZEN

Adaptionswerte auf Defaultwerte zuruecksetzen von: Kupplungskennlinie (Service ID 0x30)  ACHTUNG: Im Anschluss Zuendung aus, um Defaultwerte abzuspeichern. Steuergeraete Abfall abwarten Ganganzeige im Kombi bleibt ca. 5s erhalten und faellt dann ab. oder Speichern per Diagnose

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADAPTION | string | Argumet: KUPPLUNGSKENNLINIE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-verschleissdaten-lesen"></a>
### VERSCHLEISSDATEN_LESEN

Verschleissdaten lesen (Service ID 0x22)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN_HEX | binary | Inhalt der Speicherzellen als Hex-Dump |
| ANZ_LOESCHUNG_VERSCHLEISSDATEN_WERT | unsigned int | Anzahl Loeschungen von Verschleissdaten |
| KM_STAND_LOESCHUNG_VERSCHLEISSDATEN_WERT | unsigned int | KM-Stand der letzten Loeschung von Verschleissdaten |
| ANZ_RENNSTART_WERT | int | Anzahl Rennstarts |
| ANZ_SCHALT_FMAX_1_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 1 |
| ANZ_SCHALT_FMAX_2_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 2 |
| ANZ_SCHALT_FMAX_3_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 3 |
| ANZ_SCHALT_FMAX_4_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 4 |
| ANZ_SCHALT_FMAX_5_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 5 |
| ANZ_SCHALT_FMAX_6_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 6 |
| ANZ_SCHALT_FMAX_7_WERT | unsigned int | Anzahl Schaltungen mit maximaler Schaltkraft Gang 7 |
| KUPPLUNGSVERSCHLEISS_WERT | int | Kupplunsverschleiss in 1/100 mm |
| ANZ_LOESCHUNG_VERSCHLEISSDATEN_EINH | string | Anzahl Loeschungen von Verschleissdaten |
| KM_STAND_LOESCHUNG_VERSCHLEISSDATEN_EINH | string | KM-Stand der letzten Loeschung von Verschleissdaten |
| ANZ_RENNSTART_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_1_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_2_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_3_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_4_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_5_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_6_EINH | string | Einheit |
| ANZ_SCHALT_FMAX_7_EINH | string | Einheit |
| KUPPLUNGSVERSCHLEISS_EINH | string | Kupplunsverschleiss in 1/100 mm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-verschleissdaten-loeschen"></a>
### VERSCHLEISSDATEN_LOESCHEN

Verschleissdaten loeschen (Service ID 0x2E)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOESCHEN | string | "ja" -&gt; Verschleissdaten sollen geloescht werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Codierdaten lesen (Service ID 0x22)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_ROLLENBETRIEB_AKTIV | int | Status Rollenbetrieb Nur fuer M-GmbH (Nur Hinterachse in Rolle fuer Leistungspruefstand) Hinweis: Schaltet sich bei v=35 km/h wieder ab 0=inaktiv, 1=aktiv |
| STAT_RADABRISS_ABSCHALTUNG_AKTIV | int | Nur fuer Linie (um Geberrad-Kurbelwelle einzulernen / DME) Status Radabrissfunktionsabschaltung aktiv Wieder Einschalten (Normalzustand) über Codierdaten schreiben oder Zuendung aus/ein 0=inaktiv, 1=aktiv |
| STAT_AUSW_MOTORHAUBENK_AKTIV | int | Auswertung Motorhaubenkontakte aktiv Für C2-Steuergeräte und ab I-Stand 4.10, muss das Bit auf 1 stehen, für  C-Steuergeräte und ab I-Stand 4.10, muss das Bit auf 0 stehen, damit das Fahrzeug anfahren kann.  C-Steuergeräte unterstüzen hardwareseitg die Auswertung der Motorhaubenkontakte nicht, daher muß die Auswertung deaktiviert werden. C2-Steuergeräte reagieren nicht auf den Job CODIERDATEN_SCHREIBEN  ------- Codierung bleibt auch nach Zündungswechsel erhalten! -------  0=inaktiv, 1=aktiv |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-schreiben"></a>
### CODIERDATEN_SCHREIBEN

Codierung schreiben (Service ID 0x2E)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERUNG | string | Codierdaten fuer Auswahl: Argument: ROLLENBETRIEB oder    : RADABRISS ======NUR FUER ENTWICKLER:====================================================== oder    : AUSWERTUNG_HAUBE ==================================================================================  Rollenbetrieb (Nur Hinterachse in Rolle fuer Motorpruefstand) Hinweis: Schaltet sich bei v=35 km/h wieder ab. Radabrissfunktionsabschaltung Bei Adaption des Geberrades (DME) in der Line kann es zum Radabriss kommen. Deshalb abschalten. Auswertung Motorhaubenkontakte !!!!!!Aktivierung/Deaktivierung nur bei C-Steuergeräten möglich!!!!!!! C2-Steuergeräte reagieren nicht auf dieses Argument  ------- Codierung bleibt auch nach Zündungswechsel erhalten! -------  |
| AKTIVIERUNG | int | Argument: 0=inaktiv 1=aktiv |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an das SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-stellglied"></a>
### STEUERN_STELLGLIED

Ansteuern der Stellglieder  Argumente durch Semikolon trennen.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STELLGL | string | Anzusteuerndes Stellglied Argument siehe: table STELLGLIEDER  STELLGLIED STEUERART1 STEUERART2 aus Spalte: STELLGLIED  Anlasserfreigabe, Hydropumpe, Stoeranzeige und Shiftlock werden ueber INAKTIV ausgeschaltet.  --ACHTUNG------------------------------------------------------------------ Hydropumpe schaltet nicht automatisch ab! Bei 100 bar oeffnet das Ueberdruckventil --Pumpe wird vorgeschaedigt, wenn mehrfach ueber das Ventil abgeblasen wird. Pumpe wird maximal 60 sek. angesteuert!  Argument: "RUECKGABE_AN_SG" gilt fuer alle Stellgieder. Rueckgabe der Kontrolle an das Steuergeraet. Einzelne Stellglieder koennen nicht zurückgenommen werden!  --Fuer Soll-Ist-Vergleich z.B. bei MAGNETVENTIL_KUPPLUNG------------------------- muss Job mehrfach angestossen werden, um endgueltige Position auszugeben (Z.B. einmaliges ausfuehren gibt nur momentane Pos. beim Einregeln zurueck) (Staendiges anstossen ist natuerlich auch moeglich.) (Sollposition=Adaptionswert) |
| STEUERART1 | string | Argument: POSITIONSVORGABE oder      STROMVORGABE oder      INAKTIV oder      AKTIV  Welches Argument fuer welches "STELLGL" moeglich ist siehe: table STELLGLIEDER  STELLGLIED STEUERART1  Besonderheit Kupplungsansteuerung bei POSITIONSVORGABE: 0 = Kupplung öffnen 1 = Kupplung an Schleifpunkt positionieren 2 = Kupplung schließen 3 = Kupplung nach Ablageposition &gt;3 = einzustellende Position |
| STEUERART2 | string | Argument siehe: table STELLGLIEDER  STELLGLIED STEUERART1 STEUERART2 aus Spalte: STEUERART2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANSTEUERUNG | int | Ansteuerergebnis 0 : Ansteuerbedingungen nicht erfuellt 1 : Stellglied wird ordnungsgemaess angesteuert |
| STAT_MESS_ROH | int | Messwert als Rohwert Byte 4, 5 des Antwortelegrammes |
| STAT_MESS_WERT | real | Messwert mit Quantisierung falls notwendig Magnetventil: Kupplung, Schaltstange: R/1, 5/3, 2/4, 6/7, DRV 1, DRV 2 (DRV = Druckregelventil) und Hydropumpe Bei allen anderen Ansteuerungen erfolgt kein Ausgabe (Messwert = 0) |
| STAT_MESS_EINH | string | Einheit, falls vorhanden Bei Magnetventil erfolgt Einheit abhaengig von gewaehlter Ansteuerung (mA oder Ink) Der Hydraulikdruck wird in bar ausgegeben. Auflösung 0,1 bar |
| _TEL_AUFTRAG | binary | Hex-Auftrag an das SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string |  |

<a id="job-steuern-testprg-stop"></a>
### STEUERN_TESTPRG_STOP

Beenden eines laufenden Testprogrammes (Sowie Zuruecksetzen des Zaehlers.) Muss VOR STEUERN_TESTPRG_STARTEN geschickt werden!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-testprg-starten"></a>
### STEUERN_TESTPRG_STARTEN

Testprogramm starten Hinweis: Zuvor STEUERN_TESTPRG_STOP schicken! Weitere Istzustaende mittels STEUERN_TESTPRG_ISTZUSTAND auslesen!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTPRG_NR | int | Argument: siehe: table Testprg  TESTPRG_NR TESTPRG_NAME Dauer typ. Dauer max. aus Spalte: TESTPRG_NR |
| AUSWAHLBYTE | int | Argument: Nur fuer (Testprg:0x21 hex) bel. Gang einlegen: 0 = Neutral, 1-7 = Gang 1-7, 8 = Rueckwaertsgang Alle anderen Testprg benoetigen kein Auswahlbyte. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_TESTPRG_IM_TEST_DEZIMAL | int | Rueckgabewert welches Testprogramm gestartet wurde siehe table TESTPRG_NR  TESTPRG_NAME -&gt; Lastenheft: Parameter 1/Byte 1 |
| STAT_TESTPRG_IM_TEST_TEXT | string | Rueckgabetext welches Testprogramm gestartet wurde siehe table TESTPRG_NR  TESTPRG_NAME -&gt; Lastenheft: Parameter 1/Byte 1 |
| STAT_STATUS_TESTPRG_DEZIMAL | int | Status Testprogramm (Lastenh.: Parameter 2) kann Wert 0, 1, 2, 3 oder 4 annehmen siehe table StatTestTexte  STB TEST_STATUS_TEXT  HINWEIS: Job muss kontinuierlich angestossen werden, um z.B. den aktuellen Status beim Getriebe adaptieren zu erhalten. Job solange anstossen, bis dieses Result ungleich 1 liefert! |
| STAT_STATUS_TESTPRG_TEXT | string | Status Testprogramm als Text kann Wert 0, 1, 2, 3 oder 4 annehmen siehe table StatTestTexte  STB TEST_STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-testprg-istzustand"></a>
### STATUS_TESTPRG_ISTZUSTAND

Istzustand eines STEUERN_TESTPRG_STARTEN abfragen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTPRG_NR | int | Argument: siehe: table Testprg  TESTPRG_NR TESTPRG_NAME Dauer typ. Dauer max. aus Spalte: TESTPRG_NR |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_TESTPRG_IM_TEST_DEZIMAL | int | Rueckgabewert welches Testprogramm gestartet wurde siehe table TESTPRG_NR  TESTPRG_NAME -&gt; Lastenheft: Parameter 1/Byte 1 |
| STAT_TESTPRG_IM_TEST_TEXT | string | Rueckgabewert welches Testprogramm gestartet wurde siehe table TESTPRG_NR  TESTPRG_NAME -&gt; Lastenheft: Parameter 1/Byte 1 |
| STAT_STATUS_TESTPRG_DEZIMAL | int | Status Testprogramm (Lastenh.: Parameter 2) kann Wert 0, 1, 2, 3 oder 4 annehmen siehe table StatTestTexte  STB TEST_STATUS_TEXT  HINWEIS: Job muss kontinuierlich angestossen werden, um z.B. den aktuellen Status beim Getriebe adaptieren zu erhalten. Job solange anstossen, bis dieses Result ungleich 1 liefert! -&gt; Lastenheft: Parameter 2/Byte 2 |
| STAT_STATUS_TESTPRG_TEXT | string | Status Testprogramm als Text kann Wert 0, 1, 2, 3 oder 4 annehmen siehe table StatTestTexte  STB TEST_STATUS_TEXT |
| STAT_ZUSTAND_TESTPRG_DEZIMAL | int | Zustand der Test und Einlernprogramme als Wert -&gt; Byte 3 (Lastenheft: Parameter 3) |
| STAT_ZUSTAND_TESTPRG_TEXT | string | Zustand der Test und Einlernprogramme als Text -&gt; Byte 3 (Lastenheft: Parameter 3) |
| STAT_FEHLERMELDUNG_DEZIMAL | int | Fehlermeldung der Test und Einlernprogramme als Wert -&gt; Lastenheft: Parameter 4/Byte 4 |
| STAT_FEHLERMELDUNG_TEXT | string | Fehlermeldung der Test und Einlernprogramme als Text -&gt; Lastenheft: Parameter 4/Byte 4 |
| STAT_MESS_WERT | real | Messwert(e) der Test und Einlernprogramme -&gt; Lastenheft: Parameter 5/Byte 5 Nur TESTPRG=0x20/Speichervorspanndruck ermitteln und         0x35/Hydraulikdruck abbauen wird mit Quantisierung ausgegeben bei allen anderen Ausgaben existiert keine Quantisierung (Umrechnung)  Hinweis zu Speichervorspanndruck: Im Neuzustand   : Soll laut SACHS nicht gemessen werden, da kein Aussage moeglich. Werkstattbereich: 29-41 bar |
| STAT_MESS_EINH | string | Einheit, falls vorhanden Z.Z. nur Speichervorspanndruck, Hydraulikdruck: bar |
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
- [HARTTEXTE](#table-harttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (128 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (127 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (385 × 9)
- [FARTTYP](#table-farttyp) (124 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (243 × 2)
- [HORTTEXTE](#table-horttexte) (128 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HUMWELTMATRIX](#table-humweltmatrix) (127 × 5)
- [HUMWELTTEXTE](#table-humwelttexte) (384 × 9)
- [HARTTYP](#table-harttyp) (124 × 5)
- [HARTTEXTEINDIVIDUELL](#table-harttexteindividuell) (243 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [FUMWELTTEXTE1](#table-fumwelttexte1) (10 × 2)
- [FUMWELTTEXTE2](#table-fumwelttexte2) (5 × 2)
- [FUMWELTTEXTE3](#table-fumwelttexte3) (12 × 2)
- [FUMWELTTEXTE4](#table-fumwelttexte4) (6 × 2)
- [FUMWELTTEXTE5](#table-fumwelttexte5) (8 × 2)
- [FUMWELTTEXTE6](#table-fumwelttexte6) (6 × 2)
- [FUMWELTTEXTE16](#table-fumwelttexte16) (4 × 2)
- [FUMWELTTEXTE17](#table-fumwelttexte17) (5 × 2)
- [FUMWELTTEXTE18](#table-fumwelttexte18) (4 × 2)
- [FUMWELTTEXTE19](#table-fumwelttexte19) (5 × 2)
- [FUMWELTTEXTE20](#table-fumwelttexte20) (5 × 2)
- [FUMWELTTEXTE21](#table-fumwelttexte21) (13 × 2)
- [FUMWELTTEXTE22](#table-fumwelttexte22) (9 × 2)
- [FUMWELTTEXTE23](#table-fumwelttexte23) (8 × 2)
- [FUMWELTTEXTE24](#table-fumwelttexte24) (5 × 2)
- [FUMWELTTEXTE25](#table-fumwelttexte25) (6 × 2)
- [FUMWELTTEXTE26](#table-fumwelttexte26) (10 × 2)
- [FUMWELTTEXTE27](#table-fumwelttexte27) (5 × 2)
- [FUMWELTTEXTE28](#table-fumwelttexte28) (5 × 2)
- [FUMWELTTEXTE29](#table-fumwelttexte29) (3 × 2)
- [FUMWELTTEXTE30](#table-fumwelttexte30) (17 × 2)
- [FUMWELTTEXTE31](#table-fumwelttexte31) (4 × 2)
- [FUMWELTTEXTE32](#table-fumwelttexte32) (5 × 2)
- [FUMWELTTEXTE33](#table-fumwelttexte33) (3 × 2)
- [FUMWELTTEXTE34](#table-fumwelttexte34) (4 × 2)
- [FUMWELTTEXTE35](#table-fumwelttexte35) (5 × 2)
- [FUMWELTTEXTE36](#table-fumwelttexte36) (8 × 2)
- [FUMWELTTEXTE37](#table-fumwelttexte37) (4 × 2)
- [FUMWELTTEXTE38](#table-fumwelttexte38) (4 × 2)
- [FUMWELTTEXTE39](#table-fumwelttexte39) (4 × 2)
- [FUMWELTTEXTE40](#table-fumwelttexte40) (5 × 2)
- [FUMWELTTEXTE41](#table-fumwelttexte41) (6 × 2)
- [FUMWELTTEXTE42](#table-fumwelttexte42) (5 × 2)
- [FUMWELTTEXTE43](#table-fumwelttexte43) (12 × 2)
- [FUMWELTTEXTE44](#table-fumwelttexte44) (4 × 2)
- [FUMWELTTEXTE45](#table-fumwelttexte45) (5 × 2)
- [FUMWELTTEXTE46](#table-fumwelttexte46) (5 × 2)
- [FUMWELTTEXTE47](#table-fumwelttexte47) (5 × 2)
- [FUMWELTTEXTE48](#table-fumwelttexte48) (3 × 2)
- [STELLGLIEDER](#table-stellglieder) (19 × 5)
- [TESTPRG](#table-testprg) (13 × 4)
- [STATTESTTEXTE](#table-stattesttexte) (6 × 2)
- [INFOTEXTE0X20A](#table-infotexte0x20a) (5 × 2)
- [INFOTEXTE0X20F](#table-infotexte0x20f) (7 × 2)
- [INFOTEXTE0X21A](#table-infotexte0x21a) (6 × 2)
- [INFOTEXTE0X21F](#table-infotexte0x21f) (5 × 2)
- [INFOTEXTE0X22A](#table-infotexte0x22a) (5 × 2)
- [INFOTEXTE0X22F](#table-infotexte0x22f) (4 × 2)
- [INFOTEXTE0X23A](#table-infotexte0x23a) (4 × 2)
- [INFOTEXTE0X23F](#table-infotexte0x23f) (8 × 2)
- [INFOTEXTE0X30A](#table-infotexte0x30a) (4 × 2)
- [INFOTEXTE0X30F](#table-infotexte0x30f) (5 × 2)
- [INFOTEXTE0X31A](#table-infotexte0x31a) (5 × 2)
- [INFOTEXTE0X31F](#table-infotexte0x31f) (8 × 2)
- [INFOTEXTE0X32A](#table-infotexte0x32a) (5 × 2)
- [INFOTEXTE0X32F](#table-infotexte0x32f) (9 × 2)
- [INFOTEXTE0X33A](#table-infotexte0x33a) (4 × 2)
- [INFOTEXTE0X33F](#table-infotexte0x33f) (9 × 2)
- [INFOTEXTE0X34A](#table-infotexte0x34a) (4 × 2)
- [INFOTEXTE0X34F](#table-infotexte0x34f) (5 × 2)
- [INFOTEXTE0X35A](#table-infotexte0x35a) (5 × 2)
- [INFOTEXTE0X35F](#table-infotexte0x35f) (5 × 2)
- [INFOTEXTE0X36A](#table-infotexte0x36a) (19 × 2)
- [INFOTEXTE0X36F](#table-infotexte0x36f) (36 × 2)
- [INFOTEXTE0X37A](#table-infotexte0x37a) (8 × 2)
- [INFOTEXTE0X37F](#table-infotexte0x37f) (5 × 2)
- [INFOTEXTE0X38A](#table-infotexte0x38a) (4 × 2)
- [INFOTEXTE0X38F](#table-infotexte0x38f) (3 × 2)
- [MOTORHAUBENKONTAKTEROH](#table-motorhaubenkontakteroh) (1 × 3)
- [MOTORHAUBENKONTAKTEIST](#table-motorhaubenkontakteist) (1 × 3)
- [WAHLHEBELSIGNALEROH](#table-wahlhebelsignaleroh) (1 × 9)
- [WAHLHEBELSIGNALEIST](#table-wahlhebelsignaleist) (1 × 9)
- [LAENGSBESCHLEUNIGUNG](#table-laengsbeschleunigung) (1 × 4)
- [SENSORSPANNUNG](#table-sensorspannung) (1 × 4)
- [GETRIEBEDREHZAHL](#table-getriebedrehzahl) (1 × 3)
- [KUPPLUNGSPOSITION0X510D_E](#table-kupplungsposition0x510d-e) (1 × 9)
- [RADGESCHWVORNEISTWERT](#table-radgeschwvorneistwert) (1 × 3)
- [LAENGSBESCHL0X520C](#table-laengsbeschl0x520c) (1 × 5)
- [DREHZAHLTEMP10X5218](#table-drehzahltemp10x5218) (1 × 5)
- [DREHZAHLTEMP20X5219](#table-drehzahltemp20x5219) (1 × 6)
- [BEGRENZERDREHZAHL0X521A](#table-begrenzerdrehzahl0x521a) (1 × 5)
- [GETRIEBEVENTILDRV10X5500](#table-getriebeventildrv10x5500) (1 × 11)
- [GETRIEBEVENTILDRV20X5501](#table-getriebeventildrv20x5501) (1 × 11)
- [GETRIEBEVENTILR_10X5502](#table-getriebeventilr-10x5502) (1 × 8)
- [GETRIEBEVENTIL5_30X5503](#table-getriebeventil5-30x5503) (1 × 8)
- [GETRIEBEVENTIL6_70X5504](#table-getriebeventil6-70x5504) (1 × 8)
- [GETRIEBEVENTIL2_40X5505](#table-getriebeventil2-40x5505) (1 × 8)
- [KUPPLUNGSVENTIL0X5506](#table-kupplungsventil0x5506) (1 × 9)
- [MAGNETVENTILE0X5507](#table-magnetventile0x5507) (1 × 11)
- [MAGNETVENTILEDRV1_20X5508](#table-magnetventiledrv1-20x5508) (1 × 8)
- [RADGESCHWCAN0XCF07](#table-radgeschwcan0xcf07) (1 × 5)
- [EBENE2KUPPLUNG0X4F03](#table-ebene2kupplung0x4f03) (1 × 10)
- [EBENE30X4F04](#table-ebene30x4f04) (1 × 6)
- [HYDRAULIK0X4F40BIS42](#table-hydraulik0x4f40bis42) (1 × 7)
- [KUPPLUNG0X4FA0_A1](#table-kupplung0x4fa0-a1) (1 × 8)
- [FGR](#table-fgr) (9 × 2)
- [FREEZE_FRAME_REFERENZ](#table-freeze-frame-referenz) (6 × 2)
- [PROGRAMMINFO](#table-programminfo) (7 × 2)
- [KOMFORTINDEX](#table-komfortindex) (14 × 2)
- [GANGANZEIGE](#table-ganganzeige) (11 × 2)
- [WAEHLHEBELANZEIGE](#table-waehlhebelanzeige) (5 × 2)
- [LED](#table-led) (4 × 2)
- [INFOTEXTEFAHRZEUGZUSTAND](#table-infotextefahrzeugzustand) (48 × 2)
- [EBENE20X4F00BIS02](#table-ebene20x4f00bis02) (1 × 7)
- [NVRAMLADEN0X4F20](#table-nvramladen0x4f20) (1 × 6)
- [ESTATE0X4F21](#table-estate0x4f21) (1 × 8)
- [GETRIEBEPROBLEM0X4F80](#table-getriebeproblem0x4f80) (1 × 10)
- [UEBERSETZUNGSP0X4F81](#table-uebersetzungsp0x4f81) (1 × 12)
- [WAHLHEBEL0X5002](#table-wahlhebel0x5002) (1 × 3)
- [FAHRTRICHTWAHLHEBEL](#table-fahrtrichtwahlhebel) (1 × 12)
- [LENKRAD10X5006_07](#table-lenkrad10x5006-07) (1 × 3)
- [LENKRAD20X5006_07](#table-lenkrad20x5006-07) (1 × 3)
- [LAENGSBESCHL0X5008](#table-laengsbeschl0x5008) (1 × 3)
- [HANDBREMSE0X5008](#table-handbremse0x5008) (1 × 4)
- [HYDRAULIKDRUCKSENS0X5101](#table-hydraulikdrucksens0x5101) (1 × 9)
- [SENSORPOSITION0X5108BIS0A](#table-sensorposition0x5108bis0a) (1 × 9)
- [GETRIEBEEINGANG0X510B](#table-getriebeeingang0x510b) (1 × 9)
- [SCHALTSTANGER10X5106_07](#table-schaltstanger10x5106-07) (1 × 12)
- [MOTORDREHZ0X510C_5200](#table-motordrehz0x510c-5200) (1 × 10)
- [RADGESCHWHL0X5201](#table-radgeschwhl0x5201) (1 × 11)
- [RADGESCHWHR0X5202](#table-radgeschwhr0x5202) (1 × 11)
- [RADGESCHWVL0X5203](#table-radgeschwvl0x5203) (1 × 10)
- [RADGESCHWVR0X5204](#table-radgeschwvr0x5204) (1 × 10)
- [BETRIEBSBREMSSIG0X5206](#table-betriebsbremssig0x5206) (1 × 6)
- [BREMSZUENDSIG0X5206](#table-bremszuendsig0x5206) (1 × 7)
- [GETRIEBEKUPPFUSSSTATUS](#table-getriebekuppfussstatus) (1 × 17)
- [LENKWINKEL0X520A](#table-lenkwinkel0x520a) (1 × 5)
- [DREHMOMENT0X5208](#table-drehmoment0x5208) (1 × 5)
- [KLEMMER_15_500X5210](#table-klemmer-15-500x5210) (1 × 12)
- [STATUSDIGITALEAUSGAENGE](#table-statusdigitaleausgaenge) (1 × 16)
- [SHIFTLOCK0X5400](#table-shiftlock0x5400) (1 × 4)
- [SPG_MDREHZ0X5400_01](#table-spg-mdrehz0x5400-01) (1 × 3)
- [ANLASSERFREIGABE0X5401](#table-anlasserfreigabe0x5401) (1 × 4)
- [HYDPUMPE0X5402](#table-hydpumpe0x5402) (1 × 6)
- [MAGNETVENTIL5_30X5509](#table-magnetventil5-30x5509) (1 × 11)
- [DIGEINRESETFEST](#table-digeinresetfest) (1 × 15)
- [FEHLERSTATUSCANBUS](#table-fehlerstatuscanbus) (1 × 4)
- [GETRIEBETEMP0X4F44](#table-getriebetemp0x4f44) (1 × 8)
- [RELAISGETROELP0X5406_1](#table-relaisgetroelp0x5406-1) (1 × 4)
- [RELAISGETROELP0X5406_2](#table-relaisgetroelp0x5406-2) (1 × 4)
- [GETRIEBETEMP0X4F45](#table-getriebetemp0x4f45) (1 × 5)
- [HYDRAULIK0X4F44](#table-hydraulik0x4f44) (1 × 10)
- [HYDRAULIK0X4F43](#table-hydraulik0x4f43) (1 × 10)
- [PRGWAHL0X5004_05_1](#table-prgwahl0x5004-05-1) (1 × 3)
- [PRGWAHL0X5004_05_2](#table-prgwahl0x5004-05-2) (1 × 3)
- [FUMWELTTEXTE49](#table-fumwelttexte49) (14 × 2)
- [FUMWELTTEXTE52](#table-fumwelttexte52) (61 × 2)
- [FUMWELTTEXTE53](#table-fumwelttexte53) (43 × 2)
- [FUMWELTTEXTE50](#table-fumwelttexte50) (8 × 2)
- [FUMWELTTEXTE51](#table-fumwelttexte51) (13 × 2)

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

Dimensions: 128 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x4F00 | Ebene 2 Getriebe |
| 0x4F01 | Ebene 2 RAM |
| 0x4F02 | Ebene 2 Input |
| 0x4F03 | Ebene 2 Kupplung |
| 0x4F04 | Ebene 3 |
| 0x4F20 | NVRAM Laden unplausibel |
| 0x4F21 | Auswertung ESTATE |
| 0x4F22 | Adaptionswerte Getriebe |
| 0x4F40 | Druckbandunterschreitung HE/Hydraulikeinheit |
| 0x4F41 | Druckbandueberschreitung HE/Hydraulikeinheit |
| 0x4F42 | Baugruppe HE/Hydraulikeinheit |
| 0x4F43 | Einschaltdauer HE/Hydraulikeinheit |
| 0x4F44 | Missbrauch HE/Hydraulikeinheit |
| 0x4F45 | Getriebetemperatur ueberschritten |
| 0x4F60 | Getriebeadaption |
| 0x4F61 | Offsetadaption des Laengsbeschleunigungssensors |
| 0x4F62 | Kupplungsadaption |
| 0x4F63 | Entlueftungen |
| 0x4F64 | Aktionsmodi |
| 0x4F65 | Energiesparmodi |
| 0x4F66 | Adaptionsprogramme Getriebe nicht vollstaendig durchgefuehrt |
| 0x4F67 | Adaptionsprogramme Kupplung nicht vollstaendig durchgefuehrt |
| 0x4F80 | Getriebeproblem |
| 0x4F81 | Uebersetzungspruefung unplausibel |
| 0x4FA0 | Ansteuerung Kupplung |
| 0x4FA1 | Kupplungsueberlastung |
| 0x5000 | Auswertung Motorhaubenkontakt |
| 0x5001 | Auswertung Motorhaubenkontakt im Fahrbetrieb |
| 0x5002 | Auswertung Waehlhebel |
| 0x5003 | Auswertung Wake up |
| 0x5004 | Auswertung Programmwahlschalter Plus |
| 0x5005 | Auswertung Programmwahlschalter Minus |
| 0x5006 | Auswertung Lenkradschalter + |
| 0x5007 | Auswertung Lenkradschalter - |
| 0x5008 | Auswertung Handbremse |
| 0x5100 | Auswertung Hydrauliktemperatur-Sensor |
| 0x5101 | Auswertung Hydraulikdrucksensor |
| 0x5102 | Auswertung Laengsbeschleunigung |
| 0x5103 | Spannungsversorgung Ubatt |
| 0x5104 | Spannungsversorgung A |
| 0x5105 | Spannungsversorgung B |
| 0x5106 | Auswertung Getriebepositionssensor Schaltstange R/1 Hauptsensor |
| 0x5107 | Auswertung Getriebepositionssensor Schaltstange R/1 redundanter Sensor |
| 0x5108 | Auswertung Getriebepositionssensor Schaltstange 5/3 |
| 0x5109 | Auswertung Getriebepositionssensor Schaltstange 2/4 |
| 0x510A | Auswertung Getriebepositionssensor Schaltstange 6/7 |
| 0x510B | Auswertung Getriebeeingangsdrehzahl |
| 0x510C | Auswertung Motordrehzahl (Sensor) |
| 0x510D | Auswertung Kupplungspositionssensor Hauptsensor |
| 0x510E | Auswertung Kupplungspositionssensor redundanter Sensor |
| 0x5200 | Auswertung Motordrehzahl (CAN) |
| 0x5201 | Auswertung Radgeschwindigkeit hinten links |
| 0x5202 | Auswertung Radgeschwindigkeit hinten rechts |
| 0x5203 | Auswertung Radgeschwindigkeit vorne links |
| 0x5204 | Auswertung Radgeschwindigkeit vorne rechts |
| 0x5206 | Auswertung Betriebsbremssignal |
| 0x5208 | Auswertung Drehmoment |
| 0x5209 | Auswertung Fahrpedal |
| 0x520A | Auswertung Lenkwinkel |
| 0x520B | Auswertung Querbeschleunigung |
| 0x520C | Auswertung Laengsbeschleunigung |
| 0x520D | Auswertung Leerlaufdrehzahl |
| 0x520E | Auswertung Status Geschwindigkeitsregelung |
| 0x520F | Auswertung Status Fahrertuer |
| 0x5210 | Auswertung Status Klemme R, 15 und 50 |
| 0x5211 | Auswertung Schluesselnummer |
| 0x5212 | Auswertung Status Anhaenger |
| 0x5213 | Auswertung Status Regelung |
| 0x5214 | Auswertung Status DSC |
| 0x5215 | Auswertung Status Verzoegerung |
| 0x5216 | Auswertung Status Quittierung DSC ASC |
| 0x5217 | Auswertung Bremsdruck |
| 0x5218 | Auswertung Drehzahl Temperaturbereich 1 |
| 0x5219 | Auswertung Drehzahl Temperaturbereich 2 |
| 0x521A | Auswertung Begrenzerdrehzahl |
| 0x521B | Auswertung Status OBD Steuerfunktionen |
| 0x521C | Auswertung Status Schalter Warmlauf |
| 0x5400 | Auswertung Shift Lock |
| 0x5401 | Auswertung Anlasserfreigabe |
| 0x5402 | Auswertung Hydraulikpumpenrelais |
| 0x5403 | Ansteuerung Waehlhebel LED R |
| 0x5404 | Ansteuerung Waehlhebel LED N |
| 0x5405 | Ansteuerung Waehlhebel LED S/D |
| 0x5406 | Ansteuerung Relais Getriebeoelpumpe |
| 0x5500 | Ansteuerung Getriebeventil DRV1 |
| 0x5501 | Ansteuerung Getriebeventil DRV2 |
| 0x5502 | Ansteuerung Getriebeventil PWV1 |
| 0x5503 | Ansteuerung Getriebeventil PWV2 |
| 0x5504 | Ansteuerung Getriebeventil PWV3 |
| 0x5505 | Ansteuerung Getriebeventil PWV4 |
| 0x5506 | Ansteuerung Kupplungsventil |
| 0x5507 | Spannungsversorgung Magnetventile PWV1, PWV3 und PWV4 |
| 0x5508 | Spannungsversorgung Magnetventile DRV1, DRV2 |
| 0x5509 | Spannungsversorgung Magnetventile PWV2 und Kupplungsventil |
| 0xCF07 | Botschaft Bus Off PT CAN |
| 0xCF12 | Botschaft Fahrlicht |
| 0xCF13 | Botschaft Raddruecke |
| 0xCF0B | Bus Off Local CAN |
| 0xCF14 | Botschaft Aussentemperatur Relativzeit |
| 0xCF15 | Botschaft Bedienung Getriebewahlschalter |
| 0xCF16 | Botschaft Geschwindigkeit |
| 0xCF17 | Botschaft Kilometerstand Istwert/Reichweite |
| 0xCF18 | Botschaft Klemmenstatus |
| 0xCF19 | Botschaft Lenkradwinkel |
| 0xCF1A | Botschaft Radgeschwindigkeit |
| 0xCF1B | Botschaft Radtoleranzabgleich |
| 0xCF1C | Botschaft Status Anhaenger |
| 0xCF1D | Botschaft Status DSC |
| 0xCF1E | Botschaft Status Kombi |
| 0xCF1F | Botschaft ZV Klappenzustand |
| 0xCF20 | Botschaft Netzwerk Management |
| 0xCF25 | Botschaft DME 1 |
| 0xCF26 | Botschaft DME 2 |
| 0xCF27 | Botschaft DME 3 |
| 0xCF28 | Botschaft Drehmoment 1 |
| 0xCF29 | Botschaft Drehmoment 3 |
| 0xCF2A | Botschaft Motordaten |
| 0xCF2B | Botschaft M-Drive |
| 0xCF30 | Botschaft Checkcontrol-Meldung |
| 0xCF31 | Botschaft Anzeige Getriebedaten |
| 0xCF32 | Botschaft Drehmomentanforderung EGS |
| 0xCF33 | Botschaft Verzoegerungsanforderung ACC |
| 0xCF34 | Botschaft Getriebedaten |
| 0xCF35 | Botschaft SMG 1 |
| 0xCF36 | Botschaft SMG 2 |
| 0xCF37 | Botschaft SMG 3 |
| 0xCF38 | Botschaft Rohdaten Laengsbeschleunigung |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | nein |
| F_PCODE | ja |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 127 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x4F00 | Ebene20x4F00bis02 | DigeinResetfest | 0x009C | GetriebeKuppFussStatus |
| 0x4F01 | Ebene20x4F00bis02 | DigeinResetfest | 0x009C | GetriebeKuppFussStatus |
| 0x4F02 | Ebene20x4F00bis02 | DigeinResetfest | 0x009C | GetriebeKuppFussStatus |
| 0x4F03 | Ebene2Kupplung0x4F03 | - | - | - |
| 0x4F04 | 0x0094 | Ebene30x4F04 | 0x0180 | - |
| 0x4F20 | 0x0094 | 0x005B | 0x0180 | NvramLaden0x4F20 |
| 0x4F21 | 0x0094 | Estate0x4F21 | GetriebeKuppFussStatus | - |
| 0x4F22 | 0x00F0 | - | - | - |
| 0x4F40 | Hydraulik0x4F40bis42 | 0x00CC | - | - |
| 0x4F41 | Hydraulik0x4F40bis42 | 0x00CC | - | - |
| 0x4F42 | Hydraulik0x4F40bis42 | 0x0098 | 0x0099 | 0x00CC |
| 0x4F43 | Hydraulik0x4F43 | 0x0098 | 0x0099 | 0x00CC |
| 0x4F44 | Hydraulik0x4F44 | 0x0098 | 0x0099 | 0x00CC |
| 0x4F45 | Getriebetemp0x4F45 | 0x0076 | - | - |
| 0x4F60 | 0x00F0 | 0x00E2 | 0x00E3 | 0x00E4 |
| 0x4F61 | 0x00F0 | 0x00E2 | 0x00E3 | 0x00E4 |
| 0x4F62 | 0x00F0 | 0x00E2 | 0x00E3 | 0x00E4 |
| 0x4F63 | 0x00F0 | 0x00E2 | 0x00E3 | 0x00E4 |
| 0x4F64 | 0x00F0 | 0x00E2 | 0x00E3 | 0x00E4 |
| 0x4F65 | - | - | - | - |
| 0x4F66 | 0x00F0 | - | - | - |
| 0x4F67 | 0x00F0 | - | - | - |
| 0x4F80 | 0x00F0 | Getriebeproblem0x4F80 | 0x00F1 | 0x0085 |
| 0x4F81 | Uebersetzungsp0x4F81 | 0x0089 | - | - |
| 0x4FA0 | Kupplung0x4FA0_A1 | 0x0029 | - | - |
| 0x4FA1 | Kupplung0x4FA0_A1 | 0x003E | 0x0029 | - |
| 0x5000 | 0x00F0 | MotorhaubenkontakteRoh | MotorhaubenkontakteIst | 0x0055 |
| 0x5001 | 0x00F0 | MotorhaubenkontakteRoh | MotorhaubenkontakteIst | 0x0055 |
| 0x5002 | Wahlhebel0x5002 | WahlhebelsignaleRoh | WahlhebelsignaleIst | FahrtrichtWahlhebel |
| 0x5003 | 0x00F0 | 0x00C2 | 0x0039 | 0x005B |
| 0x5004 | 0x00F0 | Prgwahl0x5004_05_1 | Prgwahl0x5004_05_2 | 0x005A |
| 0x5005 | 0x00F0 | Prgwahl0x5004_05_1 | Prgwahl0x5004_05_2 | 0x005A |
| 0x5006 | 0x00F0 | Lenkrad10x5006_07 | Lenkrad20x5006_07 | 0x005A |
| 0x5007 | 0x00F0 | Lenkrad10x5006_07 | Lenkrad20x5006_07 | 0x005A |
| 0x5008 | Laengsbeschl0x5008 | 0x0005 | 0x0029 | Handbremse0x5008 |
| 0x5100 | 0x00F0 | 0x0050 | 0x00ED | 0x0051 |
| 0x5101 | Hydraulikdrucksens0x5101 | - | - | - |
| 0x5102 | Laengsbeschleunigung | 0x00EB | 0x0055 | 0x0029 |
| 0x5103 | 0x00F0 | 0x0052 | Sensorspannung | - |
| 0x5104 | 0x00F0 | Sensorspannung | 0x0053 | 0x0065 |
| 0x5105 | 0x00F0 | Sensorspannung | 0x0054 | 0x0066 |
| 0x5106 | SchaltstangeR10x5106_07 | 0x00AD | - | - |
| 0x5107 | SchaltstangeR10x5106_07 | 0x00AD | - | - |
| 0x5108 | Sensorposition0x5108bis0A | 0x0078 | 0x00A6 | 0x0098 |
| 0x5109 | Sensorposition0x5108bis0A | 0x0077 | 0x00A5 | 0x0098 |
| 0x510A | Sensorposition0x5108bis0A | 0x0079 | 0x00A7 | 0x0098 |
| 0x510B | Getriebeeingang0x510B | 0x0098 | 0x0099 | - |
| 0x510C | Motordrehz0x510C_5200 | 0x0143 | 0x0098 | 0x0099 |
| 0x510D | Kupplungsposition0x510D_E | 0x00AC | 0x0099 | - |
| 0x510E | Kupplungsposition0x510D_E | 0x00AC | 0x0099 | - |
| 0x5200 | Motordrehz0x510C_5200 | 0x0143 | 0x0098 | 0x0099 |
| 0x5201 | RadgeschwHL0x5201 | 0x005B | GetriebeKuppFussStatus | - |
| 0x5202 | RadgeschwHR0x5202 | 0x005B | GetriebeKuppFussStatus | - |
| 0x5203 | RadgeschwVL0x5203 | 0x005B | 0x0098 | 0x0099 |
| 0x5204 | RadgeschwVR0x5204 | 0x005B | 0x0098 | 0x0099 |
| 0x5206 | Betriebsbremssig0x5206 | 0x0005 | BremsZuendsig0x5206 | - |
| 0x5208 | Drehmoment0x5208 | 0x005B | - | - |
| 0x5209 | 0x00F0 | 0x0046 | 0x0115 | 0x003D |
| 0x520A | Lenkwinkel0x520A | 0x005B | - | - |
| 0x520B | 0x00F0 | 0x0002 | 0x0027 | 0x005B |
| 0x520C | Laengsbeschl0x520C | 0x005B | - | - |
| 0x520D | 0x00F0 | 0x006B | 0x0045 | 0x006C |
| 0x520E | 0x00F0 | 0x003D | 0x00D9 | 0x004D |
| 0x520F | 0x00F0 | 0x003D | 0x00F2 | 0x0038 |
| 0x5210 | KlemmeR_15_500x5210 | 0x005B | - | - |
| 0x5211 | 0x00F0 | 0x009A | 0x0041 | 0x00D8 |
| 0x5212 | 0x00F0 | 0x0003 | 0x0037 | 0x003E |
| 0x5213 | 0x00F0 | 0x00CF | 0x00D7 | 0x004A |
| 0x5214 | 0x00F0 | 0x00CF | 0x00D7 | 0x004A |
| 0x5215 | 0x00F0 | 0x00DA | 0x004E | - |
| 0x5216 | 0x00F0 | 0x00D6 | 0x004C | - |
| 0x5217 | 0x00F0 | 0x0004 | 0x0028 | 0x00CE |
| 0x5218 | 0x00F0 | DrehzahlTemp10x5218 | 0x0099 | - |
| 0x5219 | 0x00F0 | DrehzahlTemp20x5219 | 0x0099 | - |
| 0x521A | 0x00F0 | Begrenzerdrehzahl0x521A | 0x0099 | - |
| 0x521B | 0x00F0 | 0x00D5 | 0x004B | - |
| 0x521C | 0x00F0 | 0x00DB | 0x004F | - |
| 0x5400 | SPG_MDrehz0x5400_01 | StatusDigitaleAusgaenge | FahrtrichtWahlhebel | ShiftLock0x5400 |
| 0x5401 | SPG_MDrehz0x5400_01 | StatusDigitaleAusgaenge | FahrtrichtWahlhebel | Anlasserfreigabe0x5401 |
| 0x5402 | Hydpumpe0x5402 | 0x0123 | 0x0075 | 0x00AB |
| 0x5403 | 0x00F0 | 0x0181 | 0x013A | FahrtrichtWahlhebel |
| 0x5404 | 0x00F0 | 0x0181 | 0x013B | FahrtrichtWahlhebel |
| 0x5405 | 0x00F0 | 0x0181 | 0x013C | FahrtrichtWahlhebel |
| 0x5406 | RelaisGetrOelp0x5406_1 | 0x00C6 | 0x0076 | 0x017D |
| 0x5500 | GetriebeventilDRV10x5500 | 0x000B | 0x0182 | - |
| 0x5501 | GetriebeventilDRV20x5501 | 0x000C | 0x0182 | - |
| 0x5502 | GetriebeventilR_10x5502 | 0x0010 | 0x00C8 | 0x0182 |
| 0x5503 | Getriebeventil5_30x5503 | 0x000E | 0x00C8 | 0x0182 |
| 0x5504 | Getriebeventil6_70x5504 | 0x000D | 0x00C8 | 0x0182 |
| 0x5505 | Getriebeventil2_40x5505 | 0x000F | 0x00C8 | 0x0182 |
| 0x5506 | Kupplungsventil0x5506 | 0x00CA | 0x0182 | - |
| 0x5507 | 0x00F0 | Magnetventile0x5507 | 0x00C8 | - |
| 0x5508 | MagnetventileDRV1_20x5508 | 0x00C9 | 0x0060 | - |
| 0x5509 | Magnetventil5_30x5509 | 0x00CA | - | - |
| 0xCF07 | FehlerstatusCANBus | - | - | - |
| 0xCF0B | FehlerstatusCANBus | - | - | - |
| 0xCF12 | FehlerstatusCANBus | - | - | - |
| 0xCF13 | FehlerstatusCANBus | - | - | - |
| 0xCF14 | FehlerstatusCANBus | - | - | - |
| 0xCF15 | FehlerstatusCANBus | - | - | - |
| 0xCF16 | FehlerstatusCANBus | - | - | - |
| 0xCF17 | FehlerstatusCANBus | - | - | - |
| 0xCF18 | FehlerstatusCANBus | - | - | - |
| 0xCF19 | FehlerstatusCANBus | - | - | - |
| 0xCF1A | FehlerstatusCANBus | - | - | - |
| 0xCF1B | FehlerstatusCANBus | - | - | - |
| 0xCF1C | FehlerstatusCANBus | - | - | - |
| 0xCF1D | FehlerstatusCANBus | - | - | - |
| 0xCF1E | FehlerstatusCANBus | - | - | - |
| 0xCF1F | FehlerstatusCANBus | - | - | - |
| 0xCF20 | FehlerstatusCANBus | - | - | - |
| 0xCF25 | FehlerstatusCANBus | - | - | - |
| 0xCF26 | FehlerstatusCANBus | - | - | - |
| 0xCF27 | FehlerstatusCANBus | - | - | - |
| 0xCF28 | FehlerstatusCANBus | - | - | - |
| 0xCF29 | FehlerstatusCANBus | - | - | - |
| 0xCF2A | FehlerstatusCANBus | - | - | - |
| 0xCF2B | FehlerstatusCANBus | - | - | - |
| 0xCF30 | FehlerstatusCANBus | - | - | - |
| 0xCF31 | FehlerstatusCANBus | - | - | - |
| 0xCF32 | FehlerstatusCANBus | - | - | - |
| 0xCF33 | FehlerstatusCANBus | - | - | - |
| 0xCF34 | FehlerstatusCANBus | - | - | - |
| 0xCF35 | FehlerstatusCANBus | - | - | - |
| 0xCF36 | FehlerstatusCANBus | - | - | - |
| 0xCF37 | FehlerstatusCANBus | - | - | - |
| 0xCF38 | FehlerstatusCANBus | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 385 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | Laengsbeschleunigung (CAN) | m/s^2 | high | signed int | - | 0.025 | - | - |
| 0x0002 | Querbeschleunigung (CAN) | m/s^2 | high | signed int | - | 0.025 | - | - |
| 0x0003 | Anhaengerstatus (CAN): | 0-n | - | 0xFF | FUmweltTexte16 | - | - | - |
| 0x0004 | Bremsdruck (CAN) | bar | - | unsigned char | - | - | - | - |
| 0x0005 | Bremssignale: | 0-n | - | 0xFF | FUmweltTexte6 | - | - | - |
| 0x0006 | Byte Empfangskennung PT CAN | - | high | unsigned int | - | - | - | - |
| 0x0007 | Byte Sendekennung PT CAN | - | - | unsigned char | - | - | - | - |
| 0x0008 | Byte Empfangskennung Local CAN | - | - | unsigned char | - | - | - | - |
| 0x0009 | Byte Sendekennung Local CAN | - | - | unsigned char | - | - | - | - |
| 0x000A | Duty-Cycle Kupplung | % | high | unsigned int | - | 0.001526 | - | - |
| 0x000B | Duty-Cycle Druckregler 1 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x000C | Duty-Cycle Druckregler 2 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x000D | Duty-Cycle Schaltzylinder 2/4 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x000E | Duty-Cycle Schaltzylinder 5/3 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x000F | Duty-Cycle Schaltzylinder 6/7 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x0010 | Duty-Cycle Schaltzylinder R/1 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x0011 | Fehlercode MU | - | - | unsigned char | - | - | - | - |
| 0x0012 | Fehlercode MC | - | - | unsigned char | - | - | - | - |
| 0x0013 | Status Fahrzeugzustand (CAN): | 0-n | - | 0x00FF | FUmweltTexte17 | - | - | - |
| 0x0014 | Aktueller Gang 0= Neutral, 1-7= Gang, 8= Rueckwaertsgang | - | - | unsigned char | - | - | - | - |
| 0x0015 | Fahrpedalwert (CAN) | % | high | unsigned char | - | - | - | - |
| 0x0016 | Handbremssignal (CAN): | 0-n | - | 0xFF | FUmweltTexte18 | - | - | - |
| 0x0017 | Iststrom DRV1 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x0018 | Iststrom DRV2 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x0019 | Iststrom PWV1 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x001A | Iststrom PWV2 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x001B | Iststrom PWV3 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x001C | Iststrom PWV4 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x001D | Sollstrom DRV1 | mA | high | unsigned int | - | - | - | - |
| 0x001E | Sollstrom DRV2 | mA | high | unsigned int | - | - | - | - |
| 0x001F | Sollstrom PWV1 | mA | high | unsigned int | - | - | - | - |
| 0x0020 | Sollstrom PWV2 | mA | high | unsigned int | - | - | - | - |
| 0x0021 | Sollstrom PWV3 | mA | high | unsigned int | - | - | - | - |
| 0x0022 | Sollstrom PWV4 | mA | high | unsigned int | - | - | - | - |
| 0x0023 | Iststrom Magnetventil Kupplung Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x0024 | Sollstrom Magnetventil Kupplung | mA | high | unsigned int | - | - | - | - |
| 0x0025 | Laengsbeschleunigung Istwert (CAN) | m/s^2 | high | signed int | - | 0.1 | - | - |
| 0x0026 | Laengsbeschleunigung Istwert (Sensor) | m/s^2 | high | signed int | - | 0.00625 | - | - |
| 0x0027 | Querbeschleunigung Istwert (CAN) | m/s^2 | high | signed int | - | 0.01 | - | - |
| 0x0028 | Bremsdruck Istwert | bar | high | unsigned char | - | - | - | - |
| 0x0029 | Bremssignale Istwert: | 0-n | - | 0xFF | FUmweltTexte19 | - | - | - |
| 0x002A | Handbremssignal gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0001 | - | - | - | - |
| 0x002B | Programmwahlschalter Plus gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0800 | - | - | - | - |
| 0x002C | Programmwahlschalter Minus gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x1000 | - | - | - | - |
| 0x002D | Motorhaubenkontakt 1 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x4000 | - | - | - | - |
| 0x002E | Motorhaubenkontakt 2 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x8000 | - | - | - | - |
| 0x002F | Waehlhebelsignal S1 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0030 | Waehlhebelsignal S2 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0008 | - | - | - | - |
| 0x0031 | Waehlhebelsignal E1 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0010 | - | - | - | - |
| 0x0032 | Waehlhebelsignal E2 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0020 | - | - | - | - |
| 0x0033 | Waehlhebelsignal N1 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0040 | - | - | - | - |
| 0x0034 | Waehlhebelsignal N2 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0035 | Waehlhebelsignal R1 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0100 | - | - | - | - |
| 0x0036 | Waehlhebelsignal R2 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0200 | - | - | - | - |
| 0x0037 | Status Anhaenger | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0038 | Status Tuerkontakt (Digitaleingang Ist 1) (0=zu, 1=auf) | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0039 | Wake up gefilterter Istwert | 0/1 | high | 0x0001 | - | - | - | - |
| 0x003A | Lenkradtaster Plus gefilterter Istwert | 0/1 | high | 0x0020 | - | - | - | - |
| 0x003B | Lenkradtaster Minus gefilterter Istwert | 0/1 | high | 0x0040 | - | - | - | - |
| 0x003C | Fahrtrichtung: | 0-n | high | 0xFF | FUmweltTexte2 | - | - | - |
| 0x003D | Fahrpedalwert Istwert | % | high | signed int | - | - | 10 | - |
| 0x003E | Kupplungsschutzklasse: | 0-n | high | 0xFF | FUmweltTexte20 | - | - | - |
| 0x003F | Lenkwinkel Istwert | Grad | high | signed int | - | - | - | - |
| 0x0040 | Drehmoment Motor Istwert | Nm | high | signed int | - | - | - | - |
| 0x0041 | Schluesselnummer Istwert: | 0-n | - | 0xFF | FUmweltTexte21 | - | - | - |
| 0x0042 | Begrenzerdrehzahl Motor Istwert | 1/min | high | unsigned int | - | - | - | - |
| 0x0043 | Getriebeeingangsdrehzahl Istwert | 1/min | high | signed int | - | - | - | - |
| 0x0044 | Getriebeausgangsdrehzahl | 1/min | high | signed int | - | - | - | - |
| 0x0045 | Leerlaufdrehzahl Motor Istwert | 1/min | high | unsigned int | - | - | - | - |
| 0x0046 | Motordrehzahl Istwert | 1/min | high | signed int | - | - | - | - |
| 0x0047 | Drehzahl Temperaturbereich 1 Istwert | 1/min | high | unsigned int | - | - | - | - |
| 0x0048 | Drehzahl Temperaturbereich 2 Istwert | 1/min | high | unsigned int | - | - | - | - |
| 0x0049 | Hydraulikdruck Istwert | bar | high | unsigned int | - | 0.1 | - | - |
| 0x004A | Status Fahrstabilitaetsprogramm Istwert: | 0-n | - | 0xFF | FUmweltTexte22 | - | - | - |
| 0x004B | Byte OBD Steuerfunktionen Istwert | - | - | unsigned char | - | - | - | - |
| 0x004C | Status Quittierung DSC ACC Istwert: | 0-n | - | 0xFF | FUmweltTexte24 | - | - | - |
| 0x004D | Status Geschwindikgeitsregler Istwert: | 0-n | - | 0xFF | FUmweltTexte25 | - | - | - |
| 0x004E | Status Verzoegerung Istwert: | 0-n | - | 0xFF | FUmweltTexte26 | - | - | - |
| 0x004F | Status Schalter Warmlauf Istwert: | 0-n | - | 0xFF | FUmweltTexte27 | - | - | - |
| 0x0050 | Hydrauliktemperatur Istwert | Grad C | - | unsigned char | - | - | - | -48 |
| 0x0051 | Motortemperatur (Kuehlwasser) Istwert | Grad C | - | unsigned char | - | - | - | -48 |
| 0x0052 | Spannungsversorgung Ubatt Istwert | V | high | unsigned int | - | 25 | 1024 | - |
| 0x0053 | Sensorspannungsversorgung A Istwert | V | high | unsigned int | - | - | 1024 | - |
| 0x0054 | Sensorspannungsversorgung B Istwert | V | high | unsigned int | - | - | 1024 | - |
| 0x0055 | Fahrzeuggeschwindigkeit | km/h | high | signed int | - | - | 16 | - |
| 0x0056 | Radgeschwindigkeit hinten links Istwert | km/h | high | signed int | - | - | 16 | - |
| 0x0057 | Radgeschwindigkeit hinten rechts Istwert | km/h | high | signed int | - | - | 16 | - |
| 0x0058 | Radgeschwindigkeit vorne links Istwert | km/h | high | signed int | - | - | 16 | - |
| 0x0059 | Radgeschwindigkeit vorne rechts Istwert | km/h | high | signed int | - | - | 16 | - |
| 0x005A | Waehlhebelposition: | 0-n | high | 0xFF | FUmweltTexte5 | - | - | - |
| 0x005B | Zuendsignal: | 0-n | high | 0xFF | FUmweltTexte28 | - | - | - |
| 0x005C | Kilometerstand | km | high | long[] | - | - | - | - |
| 0x005D | Lenkwinkel (CAN) | Grad | high | signed int | - | 0.04395 | - | - |
| 0x005E | Fehlerstatus ungueltige Checks. der Abgleichwerte: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x005F | Fehlerstatus HSD 1 Schaltzylinder R/1, 6/7 und 2/4: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0060 | Fehlerstatus HSD 2 Druckregler 1 und 2: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0061 | Fehlerstatus HSD 3 Schaltzylinder 5/3 und Kupplung: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0062 | Fehlerstatus EEPROM-Daten: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0063 | Fehlerstatus Oszillatorfrequenz: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0064 | Fehlerstatus SPI Kommunikation: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0065 | Fehlerstatus Sensorversorgung A: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0066 | Fehlerstatus Sensorversorgung B: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0067 | Drehmoment Motor (CAN) | Nm | high | signed int | - | - | 2 | - |
| 0x0068 | Begrenzerdrehzahl Motor (CAN) | 1/min | high | unsigned int | - | - | - | - |
| 0x0069 | Motordrehzahl Rohwert (Sensor) | 1/min | high | signed int | - | - | - | - |
| 0x006A | Getriebeeingangsdrehzahl Rohwert | 1/min | high | signed int | - | - | - | - |
| 0x006B | Leerlaufdrehzahl Motor (CAN) | 1/min | - | unsigned char | - | 5 | - | - |
| 0x006C | Motordrehzahl (CAN) | 1/min | high | signed int | - | - | - | - |
| 0x006D | Drehzahl Temperaturbereich 1 (CAN) | 1/min | - | unsigned char | - | 50 | - | - |
| 0x006E | Drehzahl Temperaturbereich 2 (CAN) | 1/min | - | unsigned char | - | 50 | - | - |
| 0x006F | Duty-Cycle Signal OSC_IN | - | - | unsigned int | - | - | - | - |
| 0x0070 | Periodendauer Signal OSC_IN | - | - | unsigned int | - | - | - | - |
| 0x0071 | Status Shift Lock (Digitaleingang) Sollwert | - | high | 0x0001 | - | - | - | - |
| 0x0072 | Status Waehlhebel LED R (Digitalausgang) Sollwert | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0073 | Status Waehlhebel LED S/D (Digitalausgang) Sollwert | 0/1 | high | 0x0400 | - | - | - | - |
| 0x0074 | Status Anlasserfreigabe (Digitaleingang) Sollwert | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0075 | Status Hydraulikpumpenrelais (Digitaleingang) Sollwert | 0/1 | high | 0x0100 | - | - | - | - |
| 0x0076 | Status Getriebeoelpumperelais Sollwert | 0/1 | high | 0x0200 | - | - | - | - |
| 0x0077 | Getriebepositionssensor Schaltstange 2/4 Istwert | Ink | high | signed int | - | - | - | - |
| 0x0078 | Getriebepositionssensor Schaltstange 5/3 Istwert | Ink | high | signed int | - | - | - | - |
| 0x0079 | Getriebepositionssensor Schaltstange 6/7 Istwert | Ink | high | signed int | - | - | - | - |
| 0x007A | Getriebepositionssensor Schaltstange R/1 Istwert | Ink | high | signed int | - | - | - | - |
| 0x007B | Redundanter Getriebeposionssensor Schaltstange R/1 Istwert | Ink | high | signed int | - | - | - | - |
| 0x007C | Getriebepositionssensor Schaltstange 2/4 Rohwert | Ink | high | signed int | - | - | - | - |
| 0x007D | Getriebepositionssensor Schaltstange 5/3 Rohwert | Ink | high | signed int | - | - | - | - |
| 0x007E | Getriebepositionssensor Schaltstange 6/7 Rohwert | Ink | high | signed int | - | - | - | - |
| 0x007F | Getriebepositionssensor Schaltstange R/1 Rohwert | Ink | high | signed int | - | - | - | - |
| 0x0080 | Redundanter Getriebeposionssensor Schaltstange R/1 Rohwert | Ink | high | signed int | - | - | - | - |
| 0x0081 | Getriebepositionssensor Schaltstange 2/4 Sollwert | Ink | high | signed int | - | - | - | - |
| 0x0082 | Getriebepositionssensor Schaltstange 5/3 Sollwert | Ink | high | signed int | - | - | - | - |
| 0x0083 | Getriebepositionssensor Schaltstange 6/7 Sollwert | Ink | high | signed int | - | - | - | - |
| 0x0084 | Getriebepositionssensor Schaltstange R/1 Sollwert | Ink | high | signed int | - | - | - | - |
| 0x0085 | Kupplungsposition Istwert | Ink | high | signed int | - | - | - | - |
| 0x0086 | Kupplungsposition Rohwert Hauptsensor | Ink | high | signed int | - | - | - | - |
| 0x0087 | Kupplungsposition Rohwert redundanter Sensor | Ink | high | signed int | - | - | - | - |
| 0x0088 | Kupplungsposition Sollwert | Ink | high | signed int | - | - | - | - |
| 0x0089 | Bremssignale resetfest: | 0-n | - | 0xFF | FUmweltTexte19 | - | - | - |
| 0x008A | Digitaleingang 1 resetfest: | 0-n | high | 0xFFFF | FUmweltTexte30 | - | - | - |
| 0x008B | Aktueller Gang resetfest 0= Neutral, 1-7= Gang, 8= Rueckwaertsgang | - | high | unsigned char | - | - | - | - |
| 0x008C | Kilometerstand Istwert resetfest | km | high | unsigned int | - | 8 | - | - |
| 0x008D | Motordrehzahl resetfest | 1/min | high | signed int | - | - | - | - |
| 0x008E | Kupplungsposition Istwert resetfest | Ink | high | signed int | - | - | - | - |
| 0x008F | Kupplungsposition Sollwert resetfest | Ink | high | signed int | - | - | - | - |
| 0x0090 | Getriebestatus resetfest: | 0-n | - | 0xFF | FUmweltTexte3 | - | - | - |
| 0x0091 | Spannungsversorgung Ubatt im resetfesten Bereich | V | high | signed int | - | - | 1024 | - |
| 0x0092 | Radgeschwindigkeit der Hinterachse im resetfesten Bereich | km/h | high | signed int | - | - | 16 | - |
| 0x0093 | Radgeschwindigkeit der Vorderachse im resetfesten Bereich | km/h | high | signed int | - | - | 16 | - |
| 0x0094 | Spannungsversorgung Ubatt Rohwert resetfest | V | high | signed int | - | 25 | 1024 | - |
| 0x0095 | Gewuenschter Gang resetfest 0= Neutral, 1-7= Gang, 8= Rueckwaertsgang | - | - | unsigned char | - | - | - | - |
| 0x0096 | Reset-Counter MC | - | - | unsigned char | - | - | - | - |
| 0x0097 | Reset-Counter MU | - | - | unsigned char | - | - | - | - |
| 0x0098 | Getriebestatus: | 0-n | - | 0xFF | FUmweltTexte3 | - | - | - |
| 0x0099 | Kupplungsstatus: | 0-n | - | 0xFF | FUmweltTexte4 | - | - | - |
| 0x009A | Schluesselnummer (CAN): | 0-n | - | 0xFF | FUmweltTexte21 | - | - | - |
| 0x009B | Resetzaehler Sicherheitskonzept Getriebe | - | - | unsigned char | - | - | - | - |
| 0x009C | Byte Fehlervariable des Sicherheitskonzeptes Getriebe | - | high | unsigned int | - | - | - | - |
| 0x009D | SPI Timeout | - | high | unsigned int | - | - | - | - |
| 0x009E | SPI Hardwarefehler | - | high | unsigned char | - | - | - | - |
| 0x009F | Byte Status BIOS-SW | - | high | unsigned int | - | - | - | - |
| 0x00A0 | Kennzeichnung Fehler Bremssignal | - | - | unsigned char | - | - | - | - |
| 0x00A1 | Fehlerstatus CAN Bus: | 0-n | - | 0xFF | FUmweltTexte31 | - | - | - |
| 0x00A2 | Fehlerstatus PWM-Ausgang Kupplung: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A3 | Fehlerstatus PWM-Ausgang Druckregler 1: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A4 | Fehlerstatus PWM-Ausgang Druckregler 2: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A5 | Fehlerstatus PWM-Ausgang Schaltzylinder 2/4: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A6 | Fehlerstatus PWM-Ausgang Schaltzylinder 5/3: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A7 | Fehlerstatus PWM-Ausgang Schaltzylinder 6/7: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A8 | Fehlerstatus PWM-Ausgang Schaltzylinder R/1: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A9 | Kennzeichnung fehlerhafte Motordrehzahl: | 0-n | - | 0xFF | FUmweltTexte33 | - | - | - |
| 0x00AA | Fehlerstatus Netzwerk Manangement: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x00AB | Fehlerstatus Ansteuerung Hydraulikpumpe: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00AC | Kennzeichnung fehlerhafter Kupplungspositionssensor: | 0-n | - | 0xFF | FUmweltTexte34 | - | - | - |
| 0x00AD | Kennzeichnung fehlerhafter Getriebepositionssensor R/1: | 0-n | - | 0xFF | FUmweltTexte34 | - | - | - |
| 0x00AE | Fehlerstatus Ansteuerung Shift Lock: | 0-n | - | 0xFF | FUmweltTexte34 | - | - | - |
| 0x00AF | Fehlerstatus Ansteuerung Relais Anlasser: | 0-n | - | 0xFF | FUmweltTexte34 | - | - | - |
| 0x00B0 | Kennzeichnung fehlerhafte Fahrzeuggeschwindigkeit | - | - | unsigned char | - | - | - | - |
| 0x00B1 | Kennzeichnung fehlerhafte Raddrehzahl hinten links | - | - | unsigned char | - | - | - | - |
| 0x00B2 | Kennzeichnung fehlerhafte Raddrehzahl hinten rechts | - | - | unsigned char | - | - | - | - |
| 0x00B3 | Kennzeichnung fehlerhafte Raddrehzahl vorne links | - | - | unsigned char | - | - | - | - |
| 0x00B4 | Kennzeichnung fehlerhafte Raddrehzahl vorne rechts | - | - | unsigned char | - | - | - | - |
| 0x00B5 | Handbremssignal gefilterter Rohwert | 0/1 | high | 0x0001 | - | - | - | - |
| 0x00B6 | Programmwahlschalter Plus gefilterter Rohwert (Digitaleingang 1) | 0/1 | high | 0x0800 | - | - | - | - |
| 0x00B7 | Programmwahlschalter Minus gefilterter Rohwert (Digitaleingang 1) | 0/1 | high | 0x1000 | - | - | - | - |
| 0x00B8 | Motorhaubenkontakt 1 gefilterter Rohwert (Digitaleingang 1) | 0/1 | high | 0x4000 | - | - | - | - |
| 0x00B9 | Motorhaubenkontakt 2 gefilterter Rohwert (Digitaleingang 1) | 0/1 | high | 0x8000 | - | - | - | - |
| 0x00BA | Waehlhebelsignal S1 gefilterter Rohwert | 0/1 | high | 0x0004 | - | - | - | - |
| 0x00BB | Waehlhebelsignal S2 gefilterter Rohwert | 0/1 | high | 0x0008 | - | - | - | - |
| 0x00BC | Waehlhebelsignal E1 gefilterter Rohwert | 0/1 | high | 0x0010 | - | - | - | - |
| 0x00BD | Waehlhebelsignal E2 gefilterter Rohwert | 0/1 | high | 0x0020 | - | - | - | - |
| 0x00BE | Waehlhebelsignal N1 gefilterter Rohwert | 0/1 | high | 0x0040 | - | - | - | - |
| 0x00BF | Waehlhebelsignal N2 gefilterter Rohwert | 0/1 | high | 0x0080 | - | - | - | - |
| 0x00C0 | Waehlhebelsignal R1 gefilterter Rohwert | 0/1 | high | 0x0100 | - | - | - | - |
| 0x00C1 | Waehlhebelsignal R2 gefilterter Rohwert | 0/1 | high | 0x0200 | - | - | - | - |
| 0x00C2 | Wake up gefilterter Rohwert (Digitaleingang 2) | 0/1 | high | 0x0001 | - | - | - | - |
| 0x00C3 | Lenkradschalter Plus gefilterter Rohwert (Digitalwert 2) | 0/1 | high | 0x0020 | - | - | - | - |
| 0x00C4 | Lenkradschalter Minus gefilterter Rohwert (Digitalwert 2) | 0/1 | high | 0x0040 | - | - | - | - |
| 0x00C5 | Status Shift Lock (Digitaleingang) Rohwert | 0/1 | high | 0x0001 | - | - | - | - |
| 0x00C6 | Status Getriebeoelpumpenrelais Rohwert | 0/1 | high | 0x0200 | - | - | - | - |
| 0x00C8 | Status Ansteuerung HSD 1 (Digitalausgang) Rohwert | 0/1 | high | 0x2000 | - | - | - | - |
| 0x00C9 | Status Ansteuerung HSD 2 (Digitalausgang) Rohwert | 0/1 | high | 0x4000 | - | - | - | - |
| 0x00CA | Status Ansteuerung HSD 3 (Digitalausgang) Rohwert | 0/1 | high | 0x8000 | - | - | - | - |
| 0x00CB | Status Anlasserfreigabe (Digitalausgang) | 0/1 | high | 0x0080 | - | - | - | - |
| 0x00CC | Status Hydraulikpumpenrelais (Digitalausgang) | 0/1 | high | 0x0100 | - | - | - | - |
| 0x00CD | Status Waehlhebel LED N (Digitalausgang) Rohwert | 0/1 | high | 0x0200 | - | - | - | - |
| 0x00CE | Status Bremsdruck (CAN): | 0-n | - | 0xFF | FUmweltTexte35 | - | - | - |
| 0x00CF | Status DSC (CAN): | 0-n | - | 0xFF | FUmweltTexte36 | - | - | - |
| 0x00D0 | Klemmenstatus 15 (CAN): | 0-n | - | 0xFF | FUmweltTexte37 | - | - | - |
| 0x00D1 | Klemmenstatus 50 (CAN): | 0-n | - | 0xFF | FUmweltTexte38 | - | - | - |
| 0x00D2 | Klemmenstatus R (CAN): | 0-n | - | 0xFF | FUmweltTexte39 | - | - | - |
| 0x00D3 | Status Lenkwinkel (CAN): | 0-n | - | 0xFF | FUmweltTexte40 | - | - | - |
| 0x00D4 | Status Drehmoment Motor (CAN): | 0-n | - | 0xFF | FUmweltTexte41 | - | - | - |
| 0x00D5 | Byte OBD Steuerfunktion (CAN) | - | - | unsigned char | - | - | - | - |
| 0x00D6 | Status Quittierung DSC ACC (CAN): | 0-n | - | 0xFF | FUmweltTexte24 | - | - | - |
| 0x00D7 | Status Regelung (CAN): | 0-n | - | 0xFF | FUmweltTexte22 | - | - | - |
| 0x00D8 | Status Schluesselnummer (CAN): | 0-n | - | 0xFF | FUmweltTexte42 | - | - | - |
| 0x00D9 | Status Geschwindigkeitsregler (CAN): | 0-n | - | 0xFF | FUmweltTexte43 | - | - | - |
| 0x00DA | Status Verzoegerung (CAN): | 0-n | - | 0xFF | FUmweltTexte26 | - | - | - |
| 0x00DB | Status Schalter Warmlauf (CAN): | 0-n | - | 0xFF | FUmweltTexte27 | - | - | - |
| 0x00DC | Byte Fehlerursache Sicherheitskonzept Kupplung | - | - | unsigned char | - | - | - | - |
| 0x00DD | Variable fuers Abschalten | - | - | unsigned char | - | - | - | - |
| 0x00DE | Variable fuers Initialisieren: | 0-n | - | 0xFF | FUmweltTexte48 | - | - | - |
| 0x00DF | Fehlerstatus Ansteuerung Waehlhebel LED R: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00E0 | Fehlerstatus Ansteuerung Waehlhebel LED N: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00E1 | Fehlerstatus Ansteuerung Waehlhebel LED S/D: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00E2 | Adaption bzw. Testprogramm   : | 0-n | - | 0xFF | FUmweltTexte51 | - | - | - |
| 0x00E3 | Fehlermeldung einer Adaption : | 0-n | - | 0xFF | FUmweltTexte52 | - | - | - |
| 0x00E4 | Adaptionzustand im Fehlerfall: | 0-n | - | 0xFF | FUmweltTexte53 | - | - | - |
| 0x00E5 | Laengsbeschleunigung Rohwert | mV | high | signed int | - | 4.833 | - | - |
| 0x00E6 | Radgeschwindigkeit der Hinterachse | km/h | high | signed int | - | - | 16 | - |
| 0x00E7 | Radgeschwindigkeit hinten links (CAN) | km/h | high | signed int | - | - | 16 | - |
| 0x00E8 | Radgeschwindigkeit hinten rechts (CAN) | km/h | high | signed int | - | - | 16 | - |
| 0x00E9 | Radgeschwindigkeit der Vorderachse | km/h | high | signed int | - | - | 16 | - |
| 0x00EA | Hydraulikdruck Rohwert | bar | high | signed int | - | 0.1 | - | - |
| 0x00EB | Sensorspannungsversorgung A Rohwert | V | high | signed int | - | - | 1024 | - |
| 0x00EC | Sensorspannungsversorgung B Rohwert | V | high | signed int | - | - | 1024 | - |
| 0x00ED | Hydrauliktemperatur Rohwert | Grad C | high | unsigned char | - | - | - | -48 |
| 0x00EE | Radgeschwindigkeit vorne links (CAN) | km/h | high | signed int | - | - | 16 | - |
| 0x00EF | Radgeschwindigkeit vorne rechts (CAN) | km/h | high | signed int | - | - | 16 | - |
| 0x00F0 | Spannungsversorgung Ubatt Rohwert | V | high | signed int | - | - | 1024 | - |
| 0x00F1 | Gewuenschter Gang 0=N, 1-7, 8=R | - | - | unsigned char | - | - | - | - |
| 0x00F2 | Status Tuerkontakt (CAN): | 0-n | - | 0xFF | FUmweltTexte45 | - | - | - |
| 0x00F3 | Byte Umgebungsvariable Sicherheitskonzept Kupplung | - | high | unsigned int | - | - | - | - |
| 0x00F4 | Fahrtichtung vorwaerts | 0/1 | high | 0x0001 | - | - | - | - |
| 0x00F5 | Fahrtichtung neutral | 0/1 | high | 0x0002 | - | - | - | - |
| 0x00F6 | Fahrtichtung rueckwaerts | 0/1 | high | 0x0004 | - | - | - | - |
| 0x00F7 | Fahrtichtungsignal ungueltig | 0/1 | high | 0x0010 | - | - | - | - |
| 0x00F8 | Waehlhebel in R (Rueckwaerts) | 0/1 | high | 0x0020 | - | - | - | - |
| 0x00F9 | Waehlhebel in 0 (Neutral) | 0/1 | high | 0x0040 | - | - | - | - |
| 0x00FA | Waehlhebel in A (Automatik) | 0/1 | high | 0x0080 | - | - | - | - |
| 0x00FB | Waehlhebel in S (Sequentiell) | 0/1 | high | 0x0100 | - | - | - | - |
| 0x00FC | Waehlhebel in + (Gang hoch) | 0/1 | high | 0x0200 | - | - | - | - |
| 0x00FD | Waehlhebel in - (Gang runter) | 0/1 | high | 0x0400 | - | - | - | - |
| 0x00FE | Waehlhebelposition nicht definiert | 0/1 | high | 0x0800 | - | - | - | - |
| 0x0100 | Handbremssignal CAN aktiv | 0/1 | high | 0x01 | - | - | - | - |
| 0x0101 | Handbremssignal gefiltert Rohwert aktiv | 0/1 | high | 0x02 | - | - | - | - |
| 0x0102 | Handbremssignal gefiltert Istwert aktiv | 0/1 | high | 0x04 | - | - | - | - |
| 0x0103 | Kennzeichung Fehler Antriebsdrehzahlen 1 | - | high | unsigned char | - | - | - | - |
| 0x0104 | Kennzeichung Fehler Antriebsdrehzahlen 2 | - | high | unsigned char | - | - | - | - |
| 0x0105 | Getriebestatus : geschaltet | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0106 | Getriebestatus : aktiv | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0107 | Getriebestatus : Zwischenkuppeln | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0108 | Getriebestatus : Synchronisation | 0/1 | high | 0x0008 | - | - | - | - |
| 0x0109 | Getriebestatus : Schaltweg Neutral | 0/1 | high | 0x0010 | - | - | - | - |
| 0x010A | Getriebestatus : Vorspannen | 0/1 | high | 0x0020 | - | - | - | - |
| 0x010B | Getriebestatus : Getriebeinitialisierung aktiv | 0/1 | high | 0x0040 | - | - | - | - |
| 0x010C | Getriebestatus : Synchronisation fertig | 0/1 | high | 0x0080 | - | - | - | - |
| 0x010D | Getriebestatus : Vor Synchronisation | 0/1 | high | 0x0100 | - | - | - | - |
| 0x010E | Getriebestatus : Vor Synchronisation aktiv | 0/1 | high | 0x0200 | - | - | - | - |
| 0x010F | Kupplungsstatus: offen | 0/1 | high | 0x0400 | - | - | - | - |
| 0x0110 | Kupplungsstatus: geschlossen | 0/1 | high | 0x0800 | - | - | - | - |
| 0x0111 | Kupplungsstatus: oeffnet | 0/1 | high | 0x1000 | - | - | - | - |
| 0x0112 | Kupplungsstatus: schliesst | 0/1 | high | 0x2000 | - | - | - | - |
| 0x0113 | Kupplungsstatus: Zwischenkuppeln aktiv | 0/1 | high | 0x4000 | - | - | - | - |
| 0x0114 | Fussbremse aktiv | 0/1 | high | 0x8000 | - | - | - | - |
| 0x0115 | Fahrpedal Rohwert | % | high | unsigned char | - | - | - | - |
| 0x0116 | Klemme R aus | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0117 | Klemme R ein | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0118 | Signal Klemme R ungueltig | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0119 | Klemme 15 aus | 0/1 | high | 0x0008 | - | - | - | - |
| 0x011A | Klemme 15 ein | 0/1 | high | 0x0010 | - | - | - | - |
| 0x011B | Signal Klemme 15 ungueltig | 0/1 | high | 0x0020 | - | - | - | - |
| 0x011C | Klemme 50 aus | 0/1 | high | 0x0040 | - | - | - | - |
| 0x011D | Klemme 50 ein | 0/1 | high | 0x0080 | - | - | - | - |
| 0x011E | Signal Klemme 50 ungueltig | 0/1 | high | 0x0100 | - | - | - | - |
| 0x011F | Sollwert Status Shift Lock (0=Waehlhebel gesperrt, 1=nicht gesperrt) | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0120 | Sollwert Status Waehlhebel LED R | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0121 | Sollwert Status Weahlhebel LED S/D | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0122 | Sollwert Status Anlasserfreigabe | 0/1 | high | 0x0008 | - | - | - | - |
| 0x0123 | Sollwert Status Hydraulikpumpenrelais | 0/1 | high | 0x0010 | - | - | - | - |
| 0x0124 | Sollwert Status Waehlhebel LED N | 0/1 | high | 0x0020 | - | - | - | - |
| 0x0125 | Rohwert Status Shift Lock (0=Waehlhebel gesperrt, 1=nicht gesperrt) | 0/1 | high | 0x0040 | - | - | - | - |
| 0x0126 | Rohwert Status Waehlhebel LED R | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0127 | Rohwert Status Waehlhebel LED S/D | 0/1 | high | 0x0100 | - | - | - | - |
| 0x0128 | Rohwert Status Notansteuerung HSD1 | 0/1 | high | 0x0200 | - | - | - | - |
| 0x0129 | Rohwert Status Notansteuerung HSD2 | 0/1 | high | 0x0400 | - | - | - | - |
| 0x012A | Rohwert Status Notansteuerung HSD3 | 0/1 | high | 0x0800 | - | - | - | - |
| 0x012B | Rohwert Status Anlasserfreigabe | 0/1 | high | 0x1000 | - | - | - | - |
| 0x012C | Rohwert Status Hydraulikpumpenrelais | 0/1 | high | 0x2000 | - | - | - | - |
| 0x012D | Rohwert Status Waehlhebel LED N | 0/1 | high | 0x4000 | - | - | - | - |
| 0x012E | Zuendung aus | 0/1 | high | 0x0001 | - | - | - | - |
| 0x012F | Radio Ein-Stellung | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0130 | Fahrtstellung | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0131 | Anlassen | 0/1 | high | 0x0008 | - | - | - | - |
| 0x0132 | Bremssignal: Fussbremse betaetigt | 0/1 | high | 0x0010 | - | - | - | - |
| 0x0133 | Bremssignal: Handbremse betaetigt | 0/1 | high | 0x0020 | - | - | - | - |
| 0x0134 | Fehlerstatus Shift Lock: Kurzschluss nach Masse | 0/1 | high | 0x0040 | - | - | - | - |
| 0x0135 | Fehlerstatus Shift Lock: Kurzschluss nach Ubatt | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0136 | Fehlerstatus Shift Lock: Leitungsunterbrechung | 0/1 | high | 0x0100 | - | - | - | - |
| 0x0137 | Fehlerstatus Anlasserfreigabe: Kurzschluss nach Masse | 0/1 | high | 0x0200 | - | - | - | - |
| 0x0138 | Fehlerstatus Anlasserfreigabe: Kurzschluss nach Ubatt | 0/1 | high | 0x0400 | - | - | - | - |
| 0x0139 | Fehlerstatus Anlasserfreigabe: Leitungsunterbrechung | 0/1 | high | 0x0800 | - | - | - | - |
| 0x013A | Fehlerstatus Ansteuerung Waehlhebel LED R: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x013B | Fehlerstatus Ansteuerung Waehlhebel LED N: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x013C | Fehlerstatus Ansteuerung Waehlhebel LED D/S: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x013D | Ungueltige Checks. der Abgleichwerte | 0/1 | high | 0x01 | - | - | - | - |
| 0x013E | Fehler EEPROM-Daten | 0/1 | high | 0x02 | - | - | - | - |
| 0x013F | Fehler Oszillatorfrequenz | 0/1 | high | 0x04 | - | - | - | - |
| 0x0140 | Fehler SPI Kommunikation | 0/1 | high | 0x08 | - | - | - | - |
| 0x0141 | ESTATE (1=Motor ein) | 0/1 | high | 0x0400 | - | - | - | - |
| 0x0142 | Kennzeichnung Fehler Bremssignal: | 0-n | - | 0xFF | FUmweltTexte46 | - | - | - |
| 0x0143 | Status Motordrehzahl CAN: | 0-n | - | 0xFF | FUmweltTexte47 | - | - | - |
| 0x0144 | Handbremse (1=angezogen) (Digitaleingang resetfest) | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0145 | frei (Digitaleingang resetfest) | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0146 | Waehlhebelschalter S1 (Digitaleingang resetfest) | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0147 | Waehlhebelschalter S2 (Digitaleingang resetfest) | 0/1 | high | 0x0008 | - | - | - | - |
| 0x0148 | Waehlhebelschalter E1 (Digitaleingang resetfest) | 0/1 | high | 0x0010 | - | - | - | - |
| 0x0149 | Waehlhebelschalter E2 (Digitaleingang resetfest) | 0/1 | high | 0x0020 | - | - | - | - |
| 0x014A | Waehlhebelschalter N1 (Digitaleingang resetfest) | 0/1 | high | 0x0040 | - | - | - | - |
| 0x014B | Waehlhebelschalter N2 (Digitaleingang resetfest) | 0/1 | high | 0x0080 | - | - | - | - |
| 0x014C | Waehlhebelschalter R1 (Digitaleingang resetfest) | 0/1 | high | 0x0100 | - | - | - | - |
| 0x014D | Waehlhebelschalter R2 (Digitaleingang resetfest) | 0/1 | high | 0x0200 | - | - | - | - |
| 0x014E | ESTATE (1=Motor ein) (Digitaleingang resetfest) | 0/1 | high | 0x0400 | - | - | - | - |
| 0x014F | Programmwahlschalter PLUS (Digitaleingang resetfest) | 0/1 | high | 0x0800 | - | - | - | - |
| 0x0150 | Programmwahlschalter MINUS (Digitaleingang resetfest) | 0/1 | high | 0x1000 | - | - | - | - |
| 0x0151 | frei (Digitaleingang resetfest) | 0/1 | high | 0x2000 | - | - | - | - |
| 0x0152 | Motorhaubenkontakt 2 (rechts) (1=geschlossen) (Digitaleingang resetfest) | 0/1 | high | 0x4000 | - | - | - | - |
| 0x0153 | Motorhaubenkontakt 1 (links) (1=geschlossen) (Digitaleingang resetfest) | 0/1 | high | 0x8000 | - | - | - | - |
| 0x0154 | Getriebe gibt Abschaltfreigabe | 0/1 | high | 0x01 | - | - | - | - |
| 0x0155 | Kupplung gibt Abschaltfreigabe | 0/1 | high | 0x02 | - | - | - | - |
| 0x0156 | Wird nicht in NVRAM gespeichert | 0/1 | high | 0x04 | - | - | - | - |
| 0x0157 | Sofortabschaltung | 0/1 | high | 0x08 | - | - | - | - |
| 0x0158 | Botschaft Aussentemperatur/Relativzeit korrekt emfangen | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0159 | Botschaft Bedienung Getriebewahlschalter korrekt empfangen | 0/1 | high | 0x0002 | - | - | - | - |
| 0x015A | Botschaft Geschwindigkeit korrekt empfangen | 0/1 | high | 0x0004 | - | - | - | - |
| 0x015B | Botschaft Kilometerstand /Reichweite korrekt empfangen | 0/1 | high | 0x0008 | - | - | - | - |
| 0x015C | Botschaft Klemmenstatus korrekt empfangen | 0/1 | high | 0x0010 | - | - | - | - |
| 0x015D | Botschaft Lenkradwinkel korrekt empfangen | 0/1 | high | 0x0020 | - | - | - | - |
| 0x015E | Botschaft Radgeschwindigkeit korrekt empfangen | 0/1 | high | 0x0040 | - | - | - | - |
| 0x015F | Botschaft Radtoleranzabgleich korrekt empfangen | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0160 | Botschaft Anhaenger korrekt empfangen | 0/1 | high | 0x0100 | - | - | - | - |
| 0x0161 | Botschaft DSC korrekt empfangen | 0/1 | high | 0x0200 | - | - | - | - |
| 0x0162 | Botschaft Kombi korrekt empfangen | 0/1 | high | 0x0400 | - | - | - | - |
| 0x0163 | Botschaft ZV und Klappenzustand korrekt empfangen | 0/1 | high | 0x0800 | - | - | - | - |
| 0x0164 | Botschaft Status Fahrlicht korrekt empfangen | 0/1 | high | 0x1000 | - | - | - | - |
| 0x0165 | Botschaft Raddruecke korrekt empfangen | 0/1 | high | 0x2000 | - | - | - | - |
| 0x0166 | Botschaft Anzeige Checkcontrol Meldung korrekt gesendet | 0/1 | high | 0x01 | - | - | - | - |
| 0x0167 | Botschaft Anzeige Getriebedaten korrekt gesendet | 0/1 | high | 0x02 | - | - | - | - |
| 0x0168 | Botschaft Drehmomentanforderung EGS korrekt gesendet | 0/1 | high | 0x04 | - | - | - | - |
| 0x0169 | Botschaft Verzoergungsanforderung korrekt gesendet | 0/1 | high | 0x08 | - | - | - | - |
| 0x016A | Botschaft Rohdaten Laengsbeschleunigung korrekt Empfangen | 0/1 | high | 0x10 | - | - | - | - |
| 0x016B | Botschaft Getriebedaten korrekt Empfangen | 0/1 | high | 0x20 | - | - | - | - |
| 0x016C | Botschaft DME 1 korrekt empfangen | 0/1 | high | 0x01 | - | - | - | - |
| 0x016D | Botschaft DME 2 korrekt empfangen | 0/1 | high | 0x02 | - | - | - | - |
| 0x016E | Botschaft DME 3 korrekt empfangen | 0/1 | high | 0x04 | - | - | - | - |
| 0x016F | Botschaft Drehmoment 1 korrekt empfangen | 0/1 | high | 0x08 | - | - | - | - |
| 0x0170 | Botschaft Drehmoment 2 korrekt empfangen | 0/1 | high | 0x10 | - | - | - | - |
| 0x0171 | Botschaft Motordaten korrekt empfangen | 0/1 | high | 0x20 | - | - | - | - |
| 0x0172 | Botschaft M-Drive korrekt empfangen | 0/1 | high | 0x40 | - | - | - | - |
| 0x0173 | Botschaft SMG 1 korrekt gesendet | 0/1 | high | 0x01 | - | - | - | - |
| 0x0174 | Botschaft SMG 2 korrekt gesendet | 0/1 | high | 0x02 | - | - | - | - |
| 0x0175 | Botschaft SMG 3 korrekt gesendet | 0/1 | high | 0x04 | - | - | - | - |
| 0x0176 | Getriebetemperatur | Grad | high | unsigned char | - | - | - | -48 |
| 0x0177 | Einschaltdauer HE-Motor, kleine Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x0178 | Einschaltdauer HE-Motor, mittlere Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x0179 | Einschaltdauer HE-Motor, grosse Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x017A | Anzahl Getriebeschaltungen, kleine Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x017B | Anzahl Getriebeschaltungen, mittlere Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x017C | Anzahl Getriebeschaltungen, grosse Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x017D | Fehlerstatus Ansteuerung Getrieboelpumpenrelais: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x017E | Zeitdauer des erkannten Uebersetzungsverhaeltnises | - | high | unsigned int | - | - | - | - |
| 0x017F | Aus Uebersetzungverhältnis erkannter Gang | - | high | unsigned char | - | - | - | - |
| 0x0180 | Status System-Reset: | 0-n | high | 0xFF | FUmweltTexte49 | - | - | - |
| 0x0181 | PWM Wert der LED Ansteuerung | - | high | unsigned int | - | - | - | - |
| 0x0182 | Fehlerstatus Ventil: | 0-n | - | 0xFF | FUmweltTexte50 | - | - | - |
| 0x0183 | Fehlervariable Siemens NVRAM | - | high | unsigned char | - | - | - | - |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 124 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x5000 | 0x00 | 0x00 | 0x09 | 0x00 |
| 0x5001 | 0x0A | 0x00 | 0x00 | 0x00 |
| 0x5002 | 0x0E | 0x0D | 0x0C | 0x0B |
| 0x5003 | 0x00 | 0x00 | 0x00 | 0x0F |
| 0x5004 | 0x00 | 0x00 | 0x10 | 0x00 |
| 0x5005 | 0x00 | 0x00 | 0x11 | 0x00 |
| 0x5006 | 0x00 | 0x00 | 0x12 | 0x00 |
| 0x5007 | 0x00 | 0x00 | 0x13 | 0x00 |
| 0x5008 | 0x00 | 0x00 | 0x14 | 0x00 |
| 0x5100 | 0x00 | 0x00 | 0x17 | 0x16 |
| 0x5101 | 0xF9 | 0x1A | 0x19 | 0x18 |
| 0x5102 | 0x1D | 0x00 | 0x1C | 0x1B |
| 0x5103 | 0x00 | 0x00 | 0x1F | 0x1E |
| 0x5104 | 0x00 | 0x00 | 0x21 | 0x20 |
| 0x5105 | 0x00 | 0x00 | 0x23 | 0x22 |
| 0x5106 | 0x26 | 0xFD | 0x25 | 0x24 |
| 0x5107 | 0x29 | 0xFE | 0x28 | 0x27 |
| 0x5108 | 0x2C | 0xFF | 0x2B | 0x2A |
| 0x5109 | 0x2F | 0x0100 | 0x2E | 0x2D |
| 0x510A | 0x32 | 0x0101 | 0x31 | 0x30 |
| 0x510B | 0x35 | 0x00 | 0x34 | 0x33 |
| 0x510C | 0x38 | 0x00 | 0x37 | 0x36 |
| 0x510D | 0x3B | 0x0106 | 0x3A | 0x39 |
| 0x510E | 0x3E | 0x0107 | 0x3D | 0x3C |
| 0x5200 | 0x41 | 0x00 | 0x40 | 0x3F |
| 0x5201 | 0x44 | 0x00 | 0x43 | 0x42 |
| 0x5202 | 0x47 | 0x00 | 0x46 | 0x45 |
| 0x5203 | 0x4A | 0x00 | 0x49 | 0x48 |
| 0x5204 | 0x4D | 0x00 | 0x4C | 0x4B |
| 0x5206 | 0x4E | 0x00 | 0x00 | 0x00 |
| 0x5208 | 0x4F | 0x00 | 0x00 | 0x00 |
| 0x5209 | 0x50 | 0x00 | 0x00 | 0x00 |
| 0x520A | 0x51 | 0x00 | 0x00 | 0x00 |
| 0x520B | 0x52 | 0x00 | 0x00 | 0x00 |
| 0x520C | 0x53 | 0x00 | 0x00 | 0x00 |
| 0x520D | 0x54 | 0x00 | 0x00 | 0x00 |
| 0x520E | 0x55 | 0x00 | 0x00 | 0x00 |
| 0x520F | 0x56 | 0x00 | 0x00 | 0x00 |
| 0x5210 | 0x57 | 0x00 | 0x00 | 0x00 |
| 0x5211 | 0x58 | 0x00 | 0x00 | 0x00 |
| 0x5212 | 0x59 | 0x00 | 0x00 | 0x00 |
| 0x5213 | 0x5A | 0x00 | 0x00 | 0x00 |
| 0x5214 | 0x5B | 0x00 | 0x00 | 0x00 |
| 0x5215 | 0x5C | 0x00 | 0x00 | 0x00 |
| 0x5217 | 0x5D | 0x00 | 0x00 | 0x00 |
| 0x5218 | 0x5E | 0x00 | 0x00 | 0x00 |
| 0x521A | 0x5F | 0x00 | 0x00 | 0x00 |
| 0x521B | 0x60 | 0x00 | 0x00 | 0x00 |
| 0x521C | 0x61 | 0x00 | 0x00 | 0x00 |
| 0x5400 | 0x00 | 0x64 | 0x63 | 0x62 |
| 0x5401 | 0x00 | 0x67 | 0x66 | 0x65 |
| 0x5402 | 0xFA | 0x6A | 0x69 | 0x68 |
| 0x5403 | 0x00 | 0x00 | 0x6B | 0x00 |
| 0x5404 | 0x00 | 0x00 | 0x6E | 0x00 |
| 0x5405 | 0x00 | 0x00 | 0x71 | 0x00 |
| 0x5406 | 0x00 | 0xF8 | 0xF7 | 0xF6 |
| 0x5500 | 0x77 | 0x76 | 0x75 | 0x74 |
| 0x5501 | 0x7B | 0x7A | 0x79 | 0x78 |
| 0x5502 | 0x7F | 0x7E | 0x7D | 0x7C |
| 0x5503 | 0x83 | 0x82 | 0x81 | 0x80 |
| 0x5504 | 0x87 | 0x86 | 0x85 | 0x84 |
| 0x5505 | 0x8B | 0x8A | 0x89 | 0x88 |
| 0x5506 | 0x8F | 0x8E | 0x8D | 0x8C |
| 0x5507 | 0x00 | 0x00 | 0x90 | 0x00 |
| 0x5508 | 0x00 | 0x00 | 0x91 | 0x00 |
| 0x5509 | 0x00 | 0x00 | 0x92 | 0x00 |
| 0xCF12 | 0x00 | 0x93 | 0x00 | 0x00 |
| 0xCF13 | 0x00 | 0x94 | 0x00 | 0x00 |
| 0xCF14 | 0x00 | 0x95 | 0x00 | 0x00 |
| 0xCF15 | 0x00 | 0x97 | 0x96 | 0x00 |
| 0xCF16 | 0x9A | 0x99 | 0x98 | 0x00 |
| 0xCF17 | 0x00 | 0x9B | 0x00 | 0x00 |
| 0xCF18 | 0x9E | 0x9D | 0x9C | 0x00 |
| 0xCF19 | 0x00 | 0x9F | 0x00 | 0x00 |
| 0xCF1A | 0x00 | 0xA0 | 0x00 | 0x00 |
| 0xCF1B | 0x00 | 0xA1 | 0x00 | 0x00 |
| 0xCF1C | 0x00 | 0xA2 | 0x00 | 0x00 |
| 0xCF1D | 0xA5 | 0xA4 | 0xA3 | 0x00 |
| 0xCF1E | 0xA8 | 0xA7 | 0xA6 | 0x00 |
| 0xCF1F | 0x00 | 0xA9 | 0x00 | 0x00 |
| 0xCF30 | 0x00 | 0xAA | 0x00 | 0x00 |
| 0xCF31 | 0x00 | 0xAB | 0x00 | 0x00 |
| 0xCF32 | 0x00 | 0xAC | 0x00 | 0x00 |
| 0xCF33 | 0x00 | 0xAD | 0x00 | 0x00 |
| 0xCF34 | 0x00 | 0xAE | 0x00 | 0x00 |
| 0xCF38 | 0x00 | 0xAF | 0x00 | 0x00 |
| 0xCF07 | 0x00 | 0xB0 | 0x00 | 0x00 |
| 0xCF25 | 0xB3 | 0xB2 | 0xB1 | 0x00 |
| 0xCF26 | 0xB6 | 0xB5 | 0xB4 | 0x00 |
| 0xCF27 | 0xB9 | 0xB8 | 0xB7 | 0x00 |
| 0xCF28 | 0xBC | 0xBB | 0xBA | 0x00 |
| 0xCF29 | 0xBF | 0xBE | 0xBD | 0x00 |
| 0xCF2A | 0x00 | 0xC1 | 0xC0 | 0x00 |
| 0xCF2B | 0xC4 | 0xC3 | 0xC2 | 0x00 |
| 0xCF35 | 0x00 | 0xC5 | 0x00 | 0x00 |
| 0xCF36 | 0x00 | 0xC6 | 0x00 | 0x00 |
| 0xCF37 | 0x00 | 0xC7 | 0x00 | 0x00 |
| 0xCF0B | 0x00 | 0xC8 | 0x00 | 0x00 |
| 0x4F00 | 0x00 | 0x00 | 0xC9 | 0x00 |
| 0x4F01 | 0x00 | 0x00 | 0xCA | 0x00 |
| 0x4F02 | 0x00 | 0x00 | 0xCB | 0x00 |
| 0x4F03 | 0x00 | 0x00 | 0xCC | 0x00 |
| 0x4F04 | 0x00 | 0x00 | 0xCD | 0x00 |
| 0x4F20 | 0x00 | 0x00 | 0xCE | 0x00 |
| 0x4F21 | 0xCF | 0x00 | 0x00 | 0x00 |
| 0x4F22 | 0xD0 | 0x0103 | 0x0102 | 0x00 |
| 0x4F40 | 0x00 | 0x00 | 0xD1 | 0x00 |
| 0x4F41 | 0x00 | 0x00 | 0x00 | 0xD2 |
| 0x4F42 | 0xFC | 0x00 | 0xFB | 0xD3 |
| 0x4F43 | 0x00 | 0x00 | 0x00 | 0xD4 |
| 0x4F44 | 0x00 | 0x00 | 0x00 | 0xD5 |
| 0x4F60 | 0xD6 | 0x00 | 0x00 | 0x00 |
| 0x4F61 | 0xD7 | 0x00 | 0x00 | 0x00 |
| 0x4F62 | 0x010A | 0xD8 | 0x00 | 0x010B |
| 0x4F63 | 0xD9 | 0x00 | 0x00 | 0x00 |
| 0x4F64 | 0xDA | 0x00 | 0x00 | 0x00 |
| 0x4F65 | 0x00 | 0xDD | 0xDC | 0xDB |
| 0x4F66 | 0x00 | 0x00 | 0x00 | 0xDE |
| 0x4F67 | 0x00 | 0x00 | 0x00 | 0xDF |
| 0x4F80 | 0xF3 | 0xF2 | 0xF1 | 0xF0 |
| 0x4F81 | 0x00 | 0x00 | 0x0105 | 0x0104 |
| 0x4FA0 | 0x0109 | 0x0108 | 0x00 | 0xF4 |
| 0x4FA1 | 0xF5 | 0x00 | 0x00 | 0x00 |
| default | 0x08 | 0x04 | 0x02 | 0x01 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 243 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Signal oder Wert oberhalb Schwelle |
| 0x02 | Signal oder Wert unterhalb Schwelle |
| 0x04 | kein Signal oder Wert |
| 0x08 | unplausibles Signal oder Wert |
| 0x09 | Motorhaubenkontakt im Stand unplausibles Signal |
| 0x0A | Motorhaubenkontakt im Fahrbetrieb unplausibles Signal |
| 0x0B | Waehlhebel Totalausfall |
| 0x0C | Waehlhebel Einzelfehler R |
| 0x0D | Waehlhebel Einzelfehler N/E |
| 0x0E | Waehlhebel Einzelfehler S |
| 0x0F | Wake Up Kurzschluss gegen UBatt |
| 0x10 | Programmwahlschalter Plus Kurzschluss gegen Masse |
| 0x11 | Programmwahlschalter Minus Kurzschluss gegen Masse |
| 0x12 | Lenkradschalter Plus Kurzschluss gegen Masse |
| 0x13 | Lenkradschalter Minus Kurzschluss gegen Masse |
| 0x14 | Handbremssignal Kurzschluss gegen Masse |
| 0x15 | Hydraulikfuellstand |
| 0x16 | Hydrauliktemperatursensor Signal oberhalb Schwelle |
| 0x17 | Hydrauliktemperatursensor Signal unterhalb Schwelle |
| 0x18 | Hydraulikdrucksensor Signal oberhalb Schwelle |
| 0x19 | Hydraulikdrucksensor Signal unterhalb Schwelle |
| 0x1A | Hydraulikdrucksensor Masseleitung gebrochenl |
| 0x1B | Laengsbeschleunigungssensor Signal oberhalb Schwelle |
| 0x1C | Laengsbeschleunigungssensor Signal unterhalb Schwelle |
| 0x1D | Laengsbeschleunigungssensor unplausibles Signal |
| 0x1E | Spannungsversorgung UBatt Signal oberhalb Schwelle |
| 0x1F | Spannungsversorgung UBatt Signal unterhalb Schwelle |
| 0x20 | Sensorspannungsversorgung A Signal oberhalb Schwelle |
| 0x21 | Sensorspannungsversorgung A Signal unterhalb Schwelle |
| 0x22 | Sensorspannungsversorgung B Signal oberhalb Schwelle |
| 0x23 | Sensorspannungsversorgung B Signal unterhalb Schwelle |
| 0x24 | R/1 (Hauptsensor) Signal oberhalb Schwelle |
| 0x25 | R/1 (Hauptsensor) Signal unterhalb Schwelle |
| 0x26 | R/1 (Hauptsensor) unplausibles Signal |
| 0x27 | R/1 (redundanter Sensor) Signal oberhalb Schwelle |
| 0x28 | R/1 (redundanter Sensor) Signal unterhalb Schwelle |
| 0x29 | R/1 (redundanter Sensor) unplausibles Signal |
| 0x2A | 5/3 Signal oberhalb Schwelle |
| 0x2B | 5/3 Signal unterhalb Schwelle |
| 0x2C | 5/3 unplausibles Signal |
| 0x2D | 2/4 Signal oberhalb Schwelle |
| 0x2E | 2/4 Signal unterhalb Schwelle |
| 0x2F | 2/4 unplausibles Signal |
| 0x30 | 6/7 Signal oberhalb Schwelle |
| 0x31 | 6/7 Signal unterhalb Schwelle |
| 0x32 | 6/7 unplausibles Signal |
| 0x33 | Getriebeeingangsdrehzahl Signal oberhalb Schwelle |
| 0x34 | Getriebeeingangsdrehzahl Signal unterhalb Schwelle |
| 0x35 | Getriebeeingangsdrehzahl unplausibles Signal |
| 0x36 | Motordrehzahl (Sensorsignal) Signal oberhalb Schwelle |
| 0x37 | Motordrehzahl (Sensorsignal) Signal unterhalb Schwelle |
| 0x38 | Motordrehzahl (Sensorsignal) unplausibles Signal |
| 0x39 | Kupplungspositionsgeber (Hauptsensor) Signal oberhalb Schwelle |
| 0x3A | Kupplungspositionsgeber (Hauptsensor) Signal unterhalb Schwelle |
| 0x3B | Kupplungspositionsgeber (Hauptsensor) Kurzschluss gegen UBatt |
| 0x3C | Kupplungspositionsgeber (redundanter Sensor) Signal oberhalb Schwelle |
| 0x3D | Kupplungspositionsgeber (redundanter Sensor) Signal unterhalb Schwelle |
| 0x3E | Kupplungspositionsgeber (redundanter Sensor) Kurzschluss gegen UBatt |
| 0x3F | Motordrehzahl (CAN Signal) Signal oberhalb Schwelle |
| 0x40 | Motordrehzahl (CAN Signal) Signal unterhalb Schwelle |
| 0x41 | Motordrehzahl (CAN Signal) unplausibles Signal |
| 0x42 | Radgeschwindigkeit hinten links Signal oberhalb Schwelle |
| 0x43 | Radgeschwindigkeit hinten links Signal unterhalb Schwelle |
| 0x44 | Radgeschwindigkeit hinten links unplausibles Signal |
| 0x45 | Radgeschwindigkeit hinten rechts Signal oberhalb Schwelle |
| 0x46 | Radgeschwindigkeit hinten rechts Signal unterhalb Schwelle |
| 0x47 | Radgeschwindigkeit hinten rechts unplausibles Signal |
| 0x48 | Radgeschwindigkeit vorne links Signal oberhalb Schwelle |
| 0x49 | Radgeschwindigkeit vorne links Signal unterhalb Schwelle |
| 0x4A | Radgeschwindigkeit vorne links unplausibles Signal |
| 0x4B | Radgeschwindigkeit vorne rechts Signal oberhalb Schwelle |
| 0x4C | Radgeschwindigkeit vorne rechts Signal unterhalb Schwelle |
| 0x4D | Radgeschwindigkeit vorne rechts unplausibles Signal |
| 0x4E | Betriebsbremse unplausibles Signal |
| 0x4F | Drehmoment unplausibles Signal |
| 0x50 | Fahrpedal unplausibles Signal |
| 0x51 | Lenkwinkel unplausibles Signal |
| 0x52 | Querbeschleunigung unplausibles Signal |
| 0x53 | Laengsbeschleunigung unplausibles Signal |
| 0x54 | Leerlaufdrehzahl unplausibles Signal |
| 0x55 | Status Geschwindigkeitsregelung unplausibles Signal |
| 0x56 | Status Fahrertuer unplausibles Signal |
| 0x57 | Status Klemme R, 15 und 50 unplausibles Signal |
| 0x58 | Schluesselnummer unplausibles Signal |
| 0x59 | Status Anhaenger unplausibles Signal |
| 0x5A | Status Regelungen unplausibles Signal |
| 0x5B | Status DSC unplausibles Signal |
| 0x5C | Status Verzoegerung unplausibles Signal |
| 0x5D | Bremsdruck unplausibles Signal |
| 0x5E | Drehzahl Temperaturbereich 1 unplausibles Signal |
| 0x5F | Begrenzerdrehzahl unplausibles Signal |
| 0x60 | Status OBD Steuerfunktion unplausibles Signal |
| 0x61 | Status Schalter Warmlauf unplausibles Signal |
| 0x62 | Shift Lock Kurzschluss gegen UBatt |
| 0x63 | Shift Lock Kurzschluss gegen Masse |
| 0x64 | Shift Lock Leitungsunterbrechung |
| 0x65 | Anlasserfreigabe Kurzschluss gegen UBatt |
| 0x66 | Anlasserfreigabe Kurzschluss gegen Masse |
| 0x67 | Anlasserfreigabe Leitungsunterbrechung |
| 0x68 | Hydraulikpumpenrelais Kurzschluss gegen UBatt |
| 0x69 | Hydraulikpumpenrelais Kurzschluss gegen Masse |
| 0x6A | Hydraulikpumpenrelais Leitungsunterbrechung |
| 0x6B | PWM Ausgang Ansteuerung Waehlhebel LED R Symptomspezifisch |
| 0x6E | PWM Ausgang Ansteuerung Wahlhebel LED N Symptomspezifisch |
| 0x71 | PWM Ausgang Ansteuerung Wahlhebel LED S/D Symptomspezifisch |
| 0x74 | Getriebeventil DRV1 Kurzschluss gegen UBatt |
| 0x75 | Getriebeventil DRV1 Kurzschluss gegen Masse |
| 0x76 | Getriebeventil DRV1 Leitungsunterbrechung |
| 0x77 | Getriebeventil DRV1 unplausibles Signal |
| 0x78 | Getriebeventil DRV2 Kurzschluss gegen UBatt |
| 0x79 | Getriebeventil DRV2 Kurzschluss gegen Masse |
| 0x7A | Getriebeventil DRV2 Leitungsunterbrechung |
| 0x7B | Getriebeventil DRV2 unplausibles Signal |
| 0x7C | Getriebeventil PWV1 Kurzschluss gegen UBatt |
| 0x7D | Getriebeventil PWV1 Kurzschluss gegen Masse |
| 0x7E | Getriebeventil PWV1 Leitungsunterbrechung |
| 0x7F | Getriebeventil PWV1 unplausibles Signal |
| 0x80 | Getriebeventil PWV2 Kurzschluss gegen UBatt |
| 0x81 | Getriebeventil PWV2 Kurzschluss gegen Masse |
| 0x82 | Getriebeventil PWV2 Leitungsunterbrechung |
| 0x83 | Getriebeventil PWV2 unplausibles Signal |
| 0x84 | Getriebeventil PWV3 Kurzschluss gegen UBatt |
| 0x85 | Getriebeventil PWV3 Kurzschluss gegen Masse |
| 0x86 | Getriebeventil PWV3 Leitungsunterbrechung |
| 0x87 | Getriebeventil PWV3 unplausibles Signal |
| 0x88 | Getriebeventil PWV4 Kurzschluss gegen UBatt |
| 0x89 | Getriebeventil PWV4 Kurzschluss gegen Masse |
| 0x8A | Getriebeventil PWV4 Leitungsunterbrechung |
| 0x8B | Getriebeventil PWV4 unplausibles Signal |
| 0x8C | Kupplungsventil Kurzschluss gegen UBatt |
| 0x8D | Kupplungsventil Kurzschluss gegen Masse |
| 0x8E | Kupplungsventil Leitungsunterbrechung |
| 0x8F | Kupplungsventil unplausibles Signal |
| 0x90 | Spannungsversorgung Magnetventile PWV1, PWV3 und PWV4 Kurzschluss gegen Masse |
| 0x91 | Spannungsversorgung Magnetventile DRV1und DRV2 Kurzschluss gegen Masse |
| 0x92 | Spannungsversorgung Magnetventile PWV2 und Kupplungsventil Kurzschluss gegen Masse |
| 0x93 | Fahrlicht Timeout |
| 0x94 | Raddrücke Timeout |
| 0x95 | Außentemperatur Relativzeit Timeout |
| 0x96 | Bedienung Getriebewahlschalter Fehler Alivezaehler |
| 0x97 | Bedienung Getriebewahlschalter Timeout |
| 0x98 | Geschwindigkeit Fehler Alivezaehler |
| 0x99 | Geschwindigkeit Timeout |
| 0x9A | Geschwindigkeit Fehler Checksumme |
| 0x9B | Kilometerstand Istwert / Reichweite Timeout |
| 0x9C | Klemmenstatus Fehler Alivezaehler |
| 0x9D | Klemmenstatus Timeout |
| 0x9E | Klemmenstatus Fehler Checksumme |
| 0x9F | Lenkradwinkel Timeout |
| 0xA0 | Radgeschwindigkeit Timeout |
| 0xA1 | Radtoleranzabgleich Timeout |
| 0xA2 | Anhaenger Timeout |
| 0xA3 | DSC Fehler Alivezaehler |
| 0xA4 | DSC Timeout |
| 0xA5 | DSC Fehler Checksumme |
| 0xA6 | Kombi Fehler Alivezaehler |
| 0xA7 | Kombi Timeout |
| 0xA8 | Kombi Fehler Checksumme |
| 0xA9 | ZV Klappenzustand Timeout |
| 0xAA | Checkcontrol Meldungen Timeout |
| 0xAB | Anzeige Getriebedaten Timeout |
| 0xAC | Drehmomentanforderung EGS Timeout |
| 0xAD | Verzoegerungsanforderung ACC Timeout |
| 0xAE | Getriebedaten Timeout |
| 0xAF | Rohdaten Laengsbeschleunigung Timeout |
| 0xB0 | CAN Ueberwachung PT CAN Bus Off |
| 0xB1 | DME 1 Fehler Alivezaehler |
| 0xB2 | DME 1 Timeout |
| 0xB3 | DME 1 Fehler Checksumme |
| 0xB4 | DME 2 Fehler Alivezaehler |
| 0xB5 | DME 2 Timeout |
| 0xB6 | DME 2 Fehler Checksumme |
| 0xB7 | DME 3 Fehler Alivezaehler |
| 0xB8 | DME 3 Timeout |
| 0xB9 | DME 3 Fehler Checksumme |
| 0xBA | Drehmoment 1 Fehler Alivezaehler |
| 0xBB | Drehmoment 1 Timeout |
| 0xBC | Drehmoment 1 Fehler Checksumme |
| 0xBD | Drehmoment 3 Fehler Alivezaehler |
| 0xBE | Drehmoment 3 Timeout |
| 0xBF | Drehmoment 3 Fehler Checksumme |
| 0xC0 | Motordaten Fehler Alivezaehler |
| 0xC1 | Motordaten Timeout |
| 0xC2 | M-Drive Fehler Alivezaehler |
| 0xC3 | M-Drive Timeout |
| 0xC4 | M-Drive Fehler Checksumme |
| 0xC5 | SMG 1 Timeout |
| 0xC6 | SMG 2 Timeout |
| 0xC7 | SMG 3 Timeout |
| 0xC8 | CAN Ueberwachung SMG CAN Bus Off |
| 0xC9 | Sicherheitskonzept Ebene 2 Getriebe fehlerortspezifisch |
| 0xCA | Sicherheitskonzept Ebene 2 RAM fehlerortspezifisch |
| 0xCB | Sicherheitskonzept Ebene 2 Input fehlerortspezifisch |
| 0xCC | Sicherheitskonzept Ebene 2 Kupplung fehlerortspezifisch |
| 0xCD | Sicherheitskonzept Ebene 3 fehlerortspezifisch |
| 0xCE | NVRAM Laden unplausibel |
| 0xCF | Steuergeraet intern Auswertung ESTATE unplausibler Wert |
| 0xD0 | Steuergeraet intern Adaptionswerte Getriebe fehlerhafte Checksumme |
| 0xD1 | Hydraulikeinheit Druckbandunterschreitung Wert unterhalb Schwelle |
| 0xD2 | Hydraulikeinheit Druckbandüberschreitung Wert oberhalb Schwelle |
| 0xD3 | Einschalthaeufigkeit HE Motor oberhalb Schwelle |
| 0xD4 | Hydraulikeinheit Einschaltdauer Wert oberhalb Schwelle |
| 0xD5 | Hydraulikeinheit Missbrauch Wert oberhalb Schwelle |
| 0xD6 | Getriebeadaption unplausibler Wert |
| 0xD7 | Offsetadaption Laengsbeschleunigungssensor unplausibler Wert |
| 0xD8 | Kupplungsschleifpunkt Einlern- und Ansteuerfunktion unplausibler Wert |
| 0xD9 | Entlueftung unplausibler Wert |
| 0xDA | Aktionsmodi unplausibler Wert |
| 0xDB | Energiesparmodi Fertigung aktiv |
| 0xDC | Energiesparmodi Transport aktiv |
| 0xDD | Energiesparmodi Werkstatt aktiv |
| 0xDE | Eines oder mehrere der Getriebeadaptionsprogramme wurden nicht durchgefuehrt |
| 0xDF | Eines oder mehrere der Kupplungsadaptionsprogramme wurden nicht durchgefuehrt |
| 0xF0 | Getriebeproblem: Gang nicht auslegbar |
| 0xF1 | Getriebeproblem: Gang nicht einlegbar |
| 0xF2 | Getriebeproblem: Gangspringer |
| 0xF3 | Getriebeproblem: Drehzahlpruefung |
| 0xF4 | Kupplung Ansteuerung: Statische Soll - Ist Abweichung der Kupplung |
| 0xF5 | Kupplungsueberlastung |
| 0xF6 | Kurzschluss gegen Ubatt |
| 0xF7 | Kurzschluss gegen Masse |
| 0xF8 | Leitungsunterbrechung |
| 0xF9 | Hydraulikdrucksensor ausserhalb Messbereich |
| 0xFA | Hydraulikpumpenrelais klebender Relaiskontakt |
| 0xFB | Druckaufbaugeschwindigkeit unterhalb Schwelle |
| 0xFC | Hydraulikeinheit Baugruppe Leckage |
| 0xFD | R/1 (Hauptsensor) Trägerfrequenz PWM ausserhalb Bereich |
| 0xFE | R/1 (redundanter Sensor)  Trägerfrequenz PWM ausserhalb Bereich |
| 0xFF | 5/3 Trägerfrequenz PWM ausserhalb Bereich |
| 0x0100 | 2/4 Trägerfrequenz PWM ausserhalb Bereich |
| 0x0101 | 6/7 Trägerfrequenz PWM ausserhalb Bereich |
| 0x0102 | Steuergeraet intern Adaptionswerte Getriebe fehlerhafte Stromwerte |
| 0x0103 | Steuergeraet intern Adaptionswerte Getriebe fehlerhafte Positionswerte |
| 0x0104 | Sensor R/1 zu redundantem Signal unplausibel |
| 0x0105 | Uebersetzungsverhältnis beim Synchronisieren unplausibel |
| 0x0106 | Kupplungspositionsgeber (Hauptsensor) Massebruch Sensorversorgung |
| 0x0107 | Kupplungspositionsgeber (redundanter Sensor) Massebruch Sensorversorgung |
| 0x0108 | Kupplung Ansteuerung: Beide Sensoren fehlerhaft |
| 0x0109 | Kupplung Ansteuerung: Summenspannung unplausibel |
| 0x010A | Fehler Checksumme |
| 0x010B | Kupplungsschleifpunkt: Einlern- und Ansteuerfunktion fehlerhaft |
| 0xFFFF | Fehlersymptom nicht definiert |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 128 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x4F00 | Ebene 2 Getriebe |
| 0x4F01 | Ebene 2 RAM |
| 0x4F02 | Ebene 2 Input |
| 0x4F03 | Ebene 2 Kupplung |
| 0x4F04 | Ebene 3 |
| 0x4F20 | NVRAM Laden unplausibel |
| 0x4F21 | Auswertung ESTATE |
| 0x4F22 | Adaptionswerte Getriebe |
| 0x4F40 | Druckbandunterschreitung HE/Hydraulikeinheit |
| 0x4F41 | Druckbandueberschreitung HE/Hydraulikeinheit |
| 0x4F42 | Baugruppe HE/Hydraulikeinheit |
| 0x4F43 | Einschaltdauer HE/Hydraulikeinheit |
| 0x4F44 | Missbrauch HE/Hydraulikeinheit |
| 0x4F45 | Getriebetemperatur ueberschritten |
| 0x4F60 | Getriebeadaption |
| 0x4F61 | Offsetadaption des Laengsbeschleunigungssensors |
| 0x4F62 | Kupplungsadaption |
| 0x4F63 | Entlueftungen |
| 0x4F64 | Aktionsmodi |
| 0x4F65 | Energiesparmodi |
| 0x4F66 | Adaptionsprogramme Getriebe nicht vollstaendig durchgefuehrt |
| 0x4F67 | Adaptionsprogramme Kupplung nicht vollstaendig durchgefuehrt |
| 0x4F80 | Getriebeproblem |
| 0x4F81 | Uebersetzungspruefung unplausibel |
| 0x4FA0 | Ansteuerung Kupplung |
| 0x4FA1 | Kupplungsueberlastung |
| 0x5000 | Auswertung Motorhaubenkontakt |
| 0x5001 | Auswertung Motorhaubenkontakt im Fahrbetrieb |
| 0x5002 | Auswertung Waehlhebel |
| 0x5003 | Auswertung Wake up |
| 0x5004 | Auswertung Programmwahlschalter Plus |
| 0x5005 | Auswertung Programmwahlschalter Minus |
| 0x5006 | Auswertung Lenkradschalter + |
| 0x5007 | Auswertung Lenkradschalter - |
| 0x5008 | Auswertung Handbremse |
| 0x5100 | Auswertung Hydrauliktemperatur-Sensor |
| 0x5101 | Auswertung Hydraulikdrucksensor |
| 0x5102 | Auswertung Laengsbeschleunigung |
| 0x5103 | Spannungsversorgung Ubatt |
| 0x5104 | Spannungsversorgung A |
| 0x5105 | Spannungsversorgung B |
| 0x5106 | Auswertung Getriebepositionssensor Schaltstange R/1 Hauptsensor |
| 0x5107 | Auswertung Getriebepositionssensor Schaltstange R/1 redundanter Sensor |
| 0x5108 | Auswertung Getriebepositionssensor Schaltstange 5/3 |
| 0x5109 | Auswertung Getriebepositionssensor Schaltstange 2/4 |
| 0x510A | Auswertung Getriebepositionssensor Schaltstange 6/7 |
| 0x510B | Auswertung Getriebeeingangsdrehzahl |
| 0x510C | Auswertung Motordrehzahl (Sensor) |
| 0x510D | Auswertung Kupplungspositionssensor Hauptsensor |
| 0x510E | Auswertung Kupplungspositionssensor redundanter Sensor |
| 0x5200 | Auswertung Motordrehzahl (CAN) |
| 0x5201 | Auswertung Radgeschwindigkeit hinten links |
| 0x5202 | Auswertung Radgeschwindigkeit hinten rechts |
| 0x5203 | Auswertung Radgeschwindigkeit vorne links |
| 0x5204 | Auswertung Radgeschwindigkeit vorne rechts |
| 0x5206 | Auswertung Betriebsbremssignal |
| 0x5208 | Auswertung Drehmoment |
| 0x5209 | Auswertung Fahrpedal |
| 0x520A | Auswertung Lenkwinkel |
| 0x520B | Auswertung Querbeschleunigung |
| 0x520C | Auswertung Laengsbeschleunigung |
| 0x520D | Auswertung Leerlaufdrehzahl |
| 0x520E | Auswertung Status Geschwindigkeitsregelung |
| 0x520F | Auswertung Status Fahrertuer |
| 0x5210 | Auswertung Status Klemme R, 15 und 50 |
| 0x5211 | Auswertung Schluesselnummer |
| 0x5212 | Auswertung Status Anhaenger |
| 0x5213 | Auswertung Status Regelung |
| 0x5214 | Auswertung Status DSC |
| 0x5215 | Auswertung Status Verzoegerung |
| 0x5216 | Auswertung Status Quittierung DSC ASC |
| 0x5217 | Auswertung Bremsdruck |
| 0x5218 | Auswertung Drehzahl Temperaturbereich 1 |
| 0x5219 | Auswertung Drehzahl Temperaturbereich 2 |
| 0x521A | Auswertung Begrenzerdrehzahl |
| 0x521B | Auswertung Status OBD Steuerfunktionen |
| 0x521C | Auswertung Status Schalter Warmlauf |
| 0x5400 | Auswertung Shift Lock |
| 0x5401 | Auswertung Anlasserfreigabe |
| 0x5402 | Auswertung Hydraulikpumpenrelais |
| 0x5403 | Ansteuerung Waehlhebel LED R |
| 0x5404 | Ansteuerung Waehlhebel LED N |
| 0x5405 | Ansteuerung Waehlhebel LED S/D |
| 0x5406 | Ansteuerung Relais Getriebeoelpumpe |
| 0x5500 | Ansteuerung Getriebeventil DRV1 |
| 0x5501 | Ansteuerung Getriebeventil DRV2 |
| 0x5502 | Ansteuerung Getriebeventil PWV1 |
| 0x5503 | Ansteuerung Getriebeventil PWV2 |
| 0x5504 | Ansteuerung Getriebeventil PWV3 |
| 0x5505 | Ansteuerung Getriebeventil PWV4 |
| 0x5506 | Ansteuerung Kupplungsventil |
| 0x5507 | Spannungsversorgung Magnetventile PWV1, PWV3 und PWV4 |
| 0x5508 | Spannungsversorgung Magnetventile DRV1, DRV2 |
| 0x5509 | Spannungsversorgung Magnetventile PWV2 und Kupplungsventil |
| 0xCF07 | Botschaft Bus Off PT CAN |
| 0xCF12 | Botschaft Fahrlicht |
| 0xCF13 | Botschaft Raddruecke |
| 0xCF0B | Bus Off Local CAN |
| 0xCF14 | Botschaft Aussentemperatur Relativzeit |
| 0xCF15 | Botschaft Bedienung Getriebewahlschalter |
| 0xCF16 | Botschaft Geschwindigkeit |
| 0xCF17 | Botschaft Kilometerstand Istwert/Reichweite |
| 0xCF18 | Botschaft Klemmenstatus |
| 0xCF19 | Botschaft Lenkradwinkel |
| 0xCF1A | Botschaft Radgeschwindigkeit |
| 0xCF1B | Botschaft Radtoleranzabgleich |
| 0xCF1C | Botschaft Status Anhaenger |
| 0xCF1D | Botschaft Status DSC |
| 0xCF1E | Botschaft Status Kombi |
| 0xCF1F | Botschaft ZV Klappenzustand |
| 0xCF20 | Botschaft Netzwerk Management |
| 0xCF25 | Botschaft DME 1 |
| 0xCF26 | Botschaft DME 2 |
| 0xCF27 | Botschaft DME 3 |
| 0xCF28 | Botschaft Drehmoment 1 |
| 0xCF29 | Botschaft Drehmoment 3 |
| 0xCF2A | Botschaft Motordaten |
| 0xCF2B | Botschaft M-Drive |
| 0xCF30 | Botschaft Checkcontrol-Meldung |
| 0xCF31 | Botschaft Anzeige Getriebedaten |
| 0xCF32 | Botschaft Drehmomentanforderung EGS |
| 0xCF33 | Botschaft Verzoegerungsanforderung ACC |
| 0xCF34 | Botschaft Getriebedaten |
| 0xCF35 | Botschaft SMG 1 |
| 0xCF36 | Botschaft SMG 2 |
| 0xCF37 | Botschaft SMG 3 |
| 0xCF38 | Botschaft Rohdaten Laengsbeschleunigung |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | nein |
| F_PCODE | ja |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 127 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x4F00 | Ebene20x4F00bis02 | DigeinResetfest | 0x009C | GetriebeKuppFussStatus |
| 0x4F01 | Ebene20x4F00bis02 | DigeinResetfest | 0x009C | GetriebeKuppFussStatus |
| 0x4F02 | Ebene20x4F00bis02 | DigeinResetfest | 0x009C | GetriebeKuppFussStatus |
| 0x4F03 | Ebene2Kupplung0x4F03 | - | - | - |
| 0x4F04 | 0x0094 | Ebene30x4F04 | 0x0180 | - |
| 0x4F20 | 0x0094 | 0x005B | 0x0180 | NvramLaden0x4F20 |
| 0x4F21 | 0x0094 | Estate0x4F21 | GetriebeKuppFussStatus | - |
| 0x4F22 | 0x00F0 | - | - | - |
| 0x4F40 | Hydraulik0x4F40bis42 | 0x00CC | - | - |
| 0x4F41 | Hydraulik0x4F40bis42 | 0x00CC | - | - |
| 0x4F42 | Hydraulik0x4F40bis42 | 0x0098 | 0x0099 | 0x00CC |
| 0x4F43 | Hydraulik0x4F43 | 0x0098 | 0x0099 | 0x00CC |
| 0x4F44 | Hydraulik0x4F44 | 0x0098 | 0x0099 | 0x00CC |
| 0x4F45 | Getriebetemp0x4F45 | 0x0076 | - | - |
| 0x4F60 | 0x00F0 | 0x00E2 | 0x00E3 | 0x00E4 |
| 0x4F61 | 0x00F0 | 0x00E2 | 0x00E3 | 0x00E4 |
| 0x4F62 | 0x00F0 | 0x00E2 | 0x00E3 | 0x00E4 |
| 0x4F63 | 0x00F0 | 0x00E2 | 0x00E3 | 0x00E4 |
| 0x4F64 | 0x00F0 | 0x00E2 | 0x00E3 | 0x00E4 |
| 0x4F65 | - | - | - | - |
| 0x4F66 | 0x00F0 | - | - | - |
| 0x4F67 | 0x00F0 | - | - | - |
| 0x4F80 | 0x00F0 | Getriebeproblem0x4F80 | 0x00F1 | 0x0085 |
| 0x4F81 | Uebersetzungsp0x4F81 | 0x0089 | - | - |
| 0x4FA0 | Kupplung0x4FA0_A1 | 0x0029 | - | - |
| 0x4FA1 | Kupplung0x4FA0_A1 | 0x003E | 0x0029 | - |
| 0x5000 | 0x00F0 | MotorhaubenkontakteRoh | MotorhaubenkontakteIst | 0x0055 |
| 0x5001 | 0x00F0 | MotorhaubenkontakteRoh | MotorhaubenkontakteIst | 0x0055 |
| 0x5002 | Wahlhebel0x5002 | WahlhebelsignaleRoh | WahlhebelsignaleIst | FahrtrichtWahlhebel |
| 0x5003 | 0x00F0 | 0x00C2 | 0x0039 | 0x005B |
| 0x5004 | 0x00F0 | Prgwahl0x5004_05_1 | Prgwahl0x5004_05_2 | 0x005A |
| 0x5005 | 0x00F0 | Prgwahl0x5004_05_1 | Prgwahl0x5004_05_2 | 0x005A |
| 0x5006 | 0x00F0 | Lenkrad10x5006_07 | Lenkrad20x5006_07 | 0x005A |
| 0x5007 | 0x00F0 | Lenkrad10x5006_07 | Lenkrad20x5006_07 | 0x005A |
| 0x5008 | Laengsbeschl0x5008 | 0x0005 | 0x0029 | Handbremse0x5008 |
| 0x5100 | 0x00F0 | 0x0050 | 0x00ED | 0x0051 |
| 0x5101 | Hydraulikdrucksens0x5101 | - | - | - |
| 0x5102 | Laengsbeschleunigung | 0x00EB | 0x0055 | 0x0029 |
| 0x5103 | 0x00F0 | 0x0052 | Sensorspannung | - |
| 0x5104 | 0x00F0 | Sensorspannung | 0x0053 | 0x0065 |
| 0x5105 | 0x00F0 | Sensorspannung | 0x0054 | 0x0066 |
| 0x5106 | SchaltstangeR10x5106_07 | 0x00AD | - | - |
| 0x5107 | SchaltstangeR10x5106_07 | 0x00AD | - | - |
| 0x5108 | Sensorposition0x5108bis0A | 0x0078 | 0x00A6 | 0x0098 |
| 0x5109 | Sensorposition0x5108bis0A | 0x0077 | 0x00A5 | 0x0098 |
| 0x510A | Sensorposition0x5108bis0A | 0x0079 | 0x00A7 | 0x0098 |
| 0x510B | Getriebeeingang0x510B | 0x0098 | 0x0099 | - |
| 0x510C | Motordrehz0x510C_5200 | 0x0143 | 0x0098 | 0x0099 |
| 0x510D | Kupplungsposition0x510D_E | 0x00AC | 0x0099 | - |
| 0x510E | Kupplungsposition0x510D_E | 0x00AC | 0x0099 | - |
| 0x5200 | Motordrehz0x510C_5200 | 0x0143 | 0x0098 | 0x0099 |
| 0x5201 | RadgeschwHL0x5201 | 0x005B | GetriebeKuppFussStatus | - |
| 0x5202 | RadgeschwHR0x5202 | 0x005B | GetriebeKuppFussStatus | - |
| 0x5203 | RadgeschwVL0x5203 | 0x005B | 0x0098 | 0x0099 |
| 0x5204 | RadgeschwVR0x5204 | 0x005B | 0x0098 | 0x0099 |
| 0x5206 | Betriebsbremssig0x5206 | 0x0005 | BremsZuendsig0x5206 | - |
| 0x5208 | Drehmoment0x5208 | 0x005B | - | - |
| 0x5209 | 0x00F0 | 0x0046 | 0x0115 | 0x003D |
| 0x520A | Lenkwinkel0x520A | 0x005B | - | - |
| 0x520B | 0x00F0 | 0x0002 | 0x0027 | 0x005B |
| 0x520C | Laengsbeschl0x520C | 0x005B | - | - |
| 0x520D | 0x00F0 | 0x006B | 0x0045 | 0x006C |
| 0x520E | 0x00F0 | 0x003D | 0x00D9 | 0x004D |
| 0x520F | 0x00F0 | 0x003D | 0x00F2 | 0x0038 |
| 0x5210 | KlemmeR_15_500x5210 | 0x005B | - | - |
| 0x5211 | 0x00F0 | 0x009A | 0x0041 | 0x00D8 |
| 0x5212 | 0x00F0 | 0x0003 | 0x0037 | 0x003E |
| 0x5213 | 0x00F0 | 0x00CF | 0x00D7 | 0x004A |
| 0x5214 | 0x00F0 | 0x00CF | 0x00D7 | 0x004A |
| 0x5215 | 0x00F0 | 0x00DA | 0x004E | - |
| 0x5216 | 0x00F0 | 0x00D6 | 0x004C | - |
| 0x5217 | 0x00F0 | 0x0004 | 0x0028 | 0x00CE |
| 0x5218 | 0x00F0 | DrehzahlTemp10x5218 | 0x0099 | - |
| 0x5219 | 0x00F0 | DrehzahlTemp20x5219 | 0x0099 | - |
| 0x521A | 0x00F0 | Begrenzerdrehzahl0x521A | 0x0099 | - |
| 0x521B | 0x00F0 | 0x00D5 | 0x004B | - |
| 0x521C | 0x00F0 | 0x00DB | 0x004F | - |
| 0x5400 | SPG_MDrehz0x5400_01 | StatusDigitaleAusgaenge | FahrtrichtWahlhebel | ShiftLock0x5400 |
| 0x5401 | SPG_MDrehz0x5400_01 | StatusDigitaleAusgaenge | FahrtrichtWahlhebel | Anlasserfreigabe0x5401 |
| 0x5402 | Hydpumpe0x5402 | 0x0123 | 0x0075 | 0x00AB |
| 0x5403 | 0x00F0 | 0x0181 | 0x013A | FahrtrichtWahlhebel |
| 0x5404 | 0x00F0 | 0x0181 | 0x013B | FahrtrichtWahlhebel |
| 0x5405 | 0x00F0 | 0x0181 | 0x013C | FahrtrichtWahlhebel |
| 0x5406 | RelaisGetrOelp0x5406_1 | 0x00C6 | 0x0076 | 0x017D |
| 0x5500 | GetriebeventilDRV10x5500 | 0x000B | 0x0182 | - |
| 0x5501 | GetriebeventilDRV20x5501 | 0x000C | 0x0182 | - |
| 0x5502 | GetriebeventilR_10x5502 | 0x0010 | 0x00C8 | 0x0182 |
| 0x5503 | Getriebeventil5_30x5503 | 0x000E | 0x00C8 | 0x0182 |
| 0x5504 | Getriebeventil6_70x5504 | 0x000D | 0x00C8 | 0x0182 |
| 0x5505 | Getriebeventil2_40x5505 | 0x000F | 0x00C8 | 0x0182 |
| 0x5506 | Kupplungsventil0x5506 | 0x00CA | 0x0182 | - |
| 0x5507 | 0x00F0 | Magnetventile0x5507 | 0x00C8 | - |
| 0x5508 | MagnetventileDRV1_20x5508 | 0x00C9 | 0x0060 | - |
| 0x5509 | Magnetventil5_30x5509 | 0x00CA | - | - |
| 0xCF07 | FehlerstatusCANBus | - | - | - |
| 0xCF0B | FehlerstatusCANBus | - | - | - |
| 0xCF12 | FehlerstatusCANBus | - | - | - |
| 0xCF13 | FehlerstatusCANBus | - | - | - |
| 0xCF14 | FehlerstatusCANBus | - | - | - |
| 0xCF15 | FehlerstatusCANBus | - | - | - |
| 0xCF16 | FehlerstatusCANBus | - | - | - |
| 0xCF17 | FehlerstatusCANBus | - | - | - |
| 0xCF18 | FehlerstatusCANBus | - | - | - |
| 0xCF19 | FehlerstatusCANBus | - | - | - |
| 0xCF1A | FehlerstatusCANBus | - | - | - |
| 0xCF1B | FehlerstatusCANBus | - | - | - |
| 0xCF1C | FehlerstatusCANBus | - | - | - |
| 0xCF1D | FehlerstatusCANBus | - | - | - |
| 0xCF1E | FehlerstatusCANBus | - | - | - |
| 0xCF1F | FehlerstatusCANBus | - | - | - |
| 0xCF20 | FehlerstatusCANBus | - | - | - |
| 0xCF25 | FehlerstatusCANBus | - | - | - |
| 0xCF26 | FehlerstatusCANBus | - | - | - |
| 0xCF27 | FehlerstatusCANBus | - | - | - |
| 0xCF28 | FehlerstatusCANBus | - | - | - |
| 0xCF29 | FehlerstatusCANBus | - | - | - |
| 0xCF2A | FehlerstatusCANBus | - | - | - |
| 0xCF2B | FehlerstatusCANBus | - | - | - |
| 0xCF30 | FehlerstatusCANBus | - | - | - |
| 0xCF31 | FehlerstatusCANBus | - | - | - |
| 0xCF32 | FehlerstatusCANBus | - | - | - |
| 0xCF33 | FehlerstatusCANBus | - | - | - |
| 0xCF34 | FehlerstatusCANBus | - | - | - |
| 0xCF35 | FehlerstatusCANBus | - | - | - |
| 0xCF36 | FehlerstatusCANBus | - | - | - |
| 0xCF37 | FehlerstatusCANBus | - | - | - |
| 0xCF38 | FehlerstatusCANBus | - | - | - |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 384 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | Laengsbeschleunigung (CAN) | m/s^2 | high | signed int | - | 0.025 | - | - |
| 0x0002 | Querbeschleunigung (CAN) | m/s^2 | high | signed int | - | 0.025 | - | - |
| 0x0003 | Anhaengerstatus (CAN): | 0-n | - | 0xFF | FUmweltTexte16 | - | - | - |
| 0x0004 | Bremsdruck (CAN) | bar | - | unsigned char | - | - | - | - |
| 0x0005 | Bremssignale: | 0-n | - | 0xFF | FUmweltTexte6 | - | - | - |
| 0x0006 | Byte Empfangskennung PT CAN | - | high | unsigned int | - | - | - | - |
| 0x0007 | Byte Sendekennung PT CAN | - | - | unsigned char | - | - | - | - |
| 0x0008 | Byte Empfangskennung Local CAN | - | - | unsigned char | - | - | - | - |
| 0x0009 | Byte Sendekennung Local CAN | - | - | unsigned char | - | - | - | - |
| 0x000A | Duty-Cycle Kupplung | % | high | unsigned int | - | 0.001526 | - | - |
| 0x000B | Duty-Cycle Druckregler 1 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x000C | Duty-Cycle Druckregler 2 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x000D | Duty-Cycle Schaltzylinder 2/4 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x000E | Duty-Cycle Schaltzylinder 5/3 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x000F | Duty-Cycle Schaltzylinder 6/7 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x0010 | Duty-Cycle Schaltzylinder R/1 | % | high | unsigned int | - | 0.001526 | - | - |
| 0x0011 | Fehlercode MU | - | - | unsigned char | - | - | - | - |
| 0x0012 | Fehlercode MC | - | - | unsigned char | - | - | - | - |
| 0x0013 | Status Fahrzeugzustand (CAN): | 0-n | - | 0x00FF | FUmweltTexte17 | - | - | - |
| 0x0014 | Aktueller Gang 0= Neutral, 1-7= Gang, 8= Rueckwaertsgang | - | - | unsigned char | - | - | - | - |
| 0x0015 | Fahrpedalwert (CAN) | % | high | unsigned char | - | - | - | - |
| 0x0016 | Handbremssignal (CAN): | 0-n | - | 0xFF | FUmweltTexte18 | - | - | - |
| 0x0017 | Iststrom DRV1 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x0018 | Iststrom DRV2 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x0019 | Iststrom PWV1 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x001A | Iststrom PWV2 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x001B | Iststrom PWV3 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x001C | Iststrom PWV4 Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x001D | Sollstrom DRV1 | mA | high | unsigned int | - | - | - | - |
| 0x001E | Sollstrom DRV2 | mA | high | unsigned int | - | - | - | - |
| 0x001F | Sollstrom PWV1 | mA | high | unsigned int | - | - | - | - |
| 0x0020 | Sollstrom PWV2 | mA | high | unsigned int | - | - | - | - |
| 0x0021 | Sollstrom PWV3 | mA | high | unsigned int | - | - | - | - |
| 0x0022 | Sollstrom PWV4 | mA | high | unsigned int | - | - | - | - |
| 0x0023 | Iststrom Magnetventil Kupplung Rohwert | mA | high | unsigned int | - | - | - | - |
| 0x0024 | Sollstrom Magnetventil Kupplung | mA | high | unsigned int | - | - | - | - |
| 0x0025 | Laengsbeschleunigung Istwert (CAN) | m/s^2 | high | signed int | - | 0.1 | - | - |
| 0x0026 | Laengsbeschleunigung Istwert (Sensor) | m/s^2 | high | signed int | - | 0.00625 | - | - |
| 0x0027 | Querbeschleunigung Istwert (CAN) | m/s^2 | high | signed int | - | 0.01 | - | - |
| 0x0028 | Bremsdruck Istwert | bar | high | unsigned char | - | - | - | - |
| 0x0029 | Bremssignale Istwert: | 0-n | - | 0xFF | FUmweltTexte19 | - | - | - |
| 0x002A | Handbremssignal gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0001 | - | - | - | - |
| 0x002B | Programmwahlschalter Plus gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0800 | - | - | - | - |
| 0x002C | Programmwahlschalter Minus gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x1000 | - | - | - | - |
| 0x002D | Motorhaubenkontakt 1 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x4000 | - | - | - | - |
| 0x002E | Motorhaubenkontakt 2 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x8000 | - | - | - | - |
| 0x002F | Waehlhebelsignal S1 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0030 | Waehlhebelsignal S2 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0008 | - | - | - | - |
| 0x0031 | Waehlhebelsignal E1 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0010 | - | - | - | - |
| 0x0032 | Waehlhebelsignal E2 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0020 | - | - | - | - |
| 0x0033 | Waehlhebelsignal N1 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0040 | - | - | - | - |
| 0x0034 | Waehlhebelsignal N2 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0035 | Waehlhebelsignal R1 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0100 | - | - | - | - |
| 0x0036 | Waehlhebelsignal R2 gefilterter Istwert (Digitaleingang 1) | 0/1 | high | 0x0200 | - | - | - | - |
| 0x0037 | Status Anhaenger | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0038 | Status Tuerkontakt (Digitaleingang Ist 1) (0=zu, 1=auf) | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0039 | Wake up gefilterter Istwert | 0/1 | high | 0x0001 | - | - | - | - |
| 0x003A | Lenkradtaster Plus gefilterter Istwert | 0/1 | high | 0x0020 | - | - | - | - |
| 0x003B | Lenkradtaster Minus gefilterter Istwert | 0/1 | high | 0x0040 | - | - | - | - |
| 0x003C | Fahrtrichtung: | 0-n | high | 0xFF | FUmweltTexte2 | - | - | - |
| 0x003D | Fahrpedalwert Istwert | % | high | signed int | - | - | 10 | - |
| 0x003E | Kupplungsschutzklasse: | 0-n | high | 0xFF | FUmweltTexte20 | - | - | - |
| 0x003F | Lenkwinkel Istwert | Grad | high | signed int | - | - | - | - |
| 0x0040 | Drehmoment Motor Istwert | Nm | high | signed int | - | - | - | - |
| 0x0041 | Schluesselnummer Istwert: | 0-n | - | 0xFF | FUmweltTexte21 | - | - | - |
| 0x0042 | Begrenzerdrehzahl Motor Istwert | 1/min | high | unsigned int | - | - | - | - |
| 0x0043 | Getriebeeingangsdrehzahl Istwert | 1/min | high | signed int | - | - | - | - |
| 0x0044 | Getriebeausgangsdrehzahl | 1/min | high | signed int | - | - | - | - |
| 0x0045 | Leerlaufdrehzahl Motor Istwert | 1/min | high | unsigned int | - | - | - | - |
| 0x0046 | Motordrehzahl Istwert | 1/min | high | signed int | - | - | - | - |
| 0x0047 | Drehzahl Temperaturbereich 1 Istwert | 1/min | high | unsigned int | - | - | - | - |
| 0x0048 | Drehzahl Temperaturbereich 2 Istwert | 1/min | high | unsigned int | - | - | - | - |
| 0x0049 | Hydraulikdruck Istwert | bar | high | unsigned int | - | 0.1 | - | - |
| 0x004A | Status Fahrstabilitaetsprogramm Istwert: | 0-n | - | 0xFF | FUmweltTexte22 | - | - | - |
| 0x004B | Byte OBD Steuerfunktionen Istwert | - | - | unsigned char | - | - | - | - |
| 0x004C | Status Quittierung DSC ACC Istwert: | 0-n | - | 0xFF | FUmweltTexte24 | - | - | - |
| 0x004D | Status Geschwindikgeitsregler Istwert: | 0-n | - | 0xFF | FUmweltTexte25 | - | - | - |
| 0x004E | Status Verzoegerung Istwert: | 0-n | - | 0xFF | FUmweltTexte26 | - | - | - |
| 0x004F | Status Schalter Warmlauf Istwert: | 0-n | - | 0xFF | FUmweltTexte27 | - | - | - |
| 0x0050 | Hydrauliktemperatur Istwert | Grad C | - | unsigned char | - | - | - | -48 |
| 0x0051 | Motortemperatur (Kuehlwasser) Istwert | Grad C | - | unsigned char | - | - | - | -48 |
| 0x0052 | Spannungsversorgung Ubatt Istwert | V | high | unsigned int | - | 25 | 1024 | - |
| 0x0053 | Sensorspannungsversorgung A Istwert | V | high | unsigned int | - | - | 1024 | - |
| 0x0054 | Sensorspannungsversorgung B Istwert | V | high | unsigned int | - | - | 1024 | - |
| 0x0055 | Fahrzeuggeschwindigkeit | km/h | high | signed int | - | - | 16 | - |
| 0x0056 | Radgeschwindigkeit hinten links Istwert | km/h | high | signed int | - | - | 16 | - |
| 0x0057 | Radgeschwindigkeit hinten rechts Istwert | km/h | high | signed int | - | - | 16 | - |
| 0x0058 | Radgeschwindigkeit vorne links Istwert | km/h | high | signed int | - | - | 16 | - |
| 0x0059 | Radgeschwindigkeit vorne rechts Istwert | km/h | high | signed int | - | - | 16 | - |
| 0x005A | Waehlhebelposition: | 0-n | high | 0xFF | FUmweltTexte5 | - | - | - |
| 0x005B | Zuendsignal: | 0-n | high | 0xFF | FUmweltTexte28 | - | - | - |
| 0x005C | Kilometerstand | km | high | long[] | - | - | - | - |
| 0x005D | Lenkwinkel (CAN) | Grad | high | signed int | - | 0.04395 | - | - |
| 0x005E | Fehlerstatus ungueltige Checks. der Abgleichwerte: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x005F | Fehlerstatus HSD 1 Schaltzylinder R/1, 6/7 und 2/4: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0060 | Fehlerstatus HSD 2 Druckregler 1 und 2: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0061 | Fehlerstatus HSD 3 Schaltzylinder 5/3 und Kupplung: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0062 | Fehlerstatus EEPROM-Daten: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0063 | Fehlerstatus Oszillatorfrequenz: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0064 | Fehlerstatus SPI Kommunikation: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0065 | Fehlerstatus Sensorversorgung A: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0066 | Fehlerstatus Sensorversorgung B: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x0067 | Drehmoment Motor (CAN) | Nm | high | signed int | - | - | 2 | - |
| 0x0068 | Begrenzerdrehzahl Motor (CAN) | 1/min | high | unsigned int | - | - | - | - |
| 0x0069 | Motordrehzahl Rohwert (Sensor) | 1/min | high | signed int | - | - | - | - |
| 0x006A | Getriebeeingangsdrehzahl Rohwert | 1/min | high | signed int | - | - | - | - |
| 0x006B | Leerlaufdrehzahl Motor (CAN) | 1/min | - | unsigned char | - | 5 | - | - |
| 0x006C | Motordrehzahl (CAN) | 1/min | high | signed int | - | - | - | - |
| 0x006D | Drehzahl Temperaturbereich 1 (CAN) | 1/min | - | unsigned char | - | 50 | - | - |
| 0x006E | Drehzahl Temperaturbereich 2 (CAN) | 1/min | - | unsigned char | - | 50 | - | - |
| 0x006F | Duty-Cycle Signal OSC_IN | - | - | unsigned int | - | - | - | - |
| 0x0070 | Periodendauer Signal OSC_IN | - | - | unsigned int | - | - | - | - |
| 0x0071 | Status Shift Lock (Digitaleingang) Sollwert | - | high | 0x0001 | - | - | - | - |
| 0x0072 | Status Waehlhebel LED R (Digitalausgang) Sollwert | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0073 | Status Waehlhebel LED S/D (Digitalausgang) Sollwert | 0/1 | high | 0x0400 | - | - | - | - |
| 0x0074 | Status Anlasserfreigabe (Digitaleingang) Sollwert | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0075 | Status Hydraulikpumpenrelais (Digitaleingang) Sollwert | 0/1 | high | 0x0100 | - | - | - | - |
| 0x0076 | Status Getriebeoelpumperelais Sollwert | 0/1 | high | 0x0200 | - | - | - | - |
| 0x0077 | Getriebepositionssensor Schaltstange 2/4 Istwert | Ink | high | signed int | - | - | - | - |
| 0x0078 | Getriebepositionssensor Schaltstange 5/3 Istwert | Ink | high | signed int | - | - | - | - |
| 0x0079 | Getriebepositionssensor Schaltstange 6/7 Istwert | Ink | high | signed int | - | - | - | - |
| 0x007A | Getriebepositionssensor Schaltstange R/1 Istwert | Ink | high | signed int | - | - | - | - |
| 0x007B | Redundanter Getriebeposionssensor Schaltstange R/1 Istwert | Ink | high | signed int | - | - | - | - |
| 0x007C | Getriebepositionssensor Schaltstange 2/4 Rohwert | Ink | high | signed int | - | - | - | - |
| 0x007D | Getriebepositionssensor Schaltstange 5/3 Rohwert | Ink | high | signed int | - | - | - | - |
| 0x007E | Getriebepositionssensor Schaltstange 6/7 Rohwert | Ink | high | signed int | - | - | - | - |
| 0x007F | Getriebepositionssensor Schaltstange R/1 Rohwert | Ink | high | signed int | - | - | - | - |
| 0x0080 | Redundanter Getriebeposionssensor Schaltstange R/1 Rohwert | Ink | high | signed int | - | - | - | - |
| 0x0081 | Getriebepositionssensor Schaltstange 2/4 Sollwert | Ink | high | signed int | - | - | - | - |
| 0x0082 | Getriebepositionssensor Schaltstange 5/3 Sollwert | Ink | high | signed int | - | - | - | - |
| 0x0083 | Getriebepositionssensor Schaltstange 6/7 Sollwert | Ink | high | signed int | - | - | - | - |
| 0x0084 | Getriebepositionssensor Schaltstange R/1 Sollwert | Ink | high | signed int | - | - | - | - |
| 0x0085 | Kupplungsposition Istwert | Ink | high | signed int | - | - | - | - |
| 0x0086 | Kupplungsposition Rohwert Hauptsensor | Ink | high | signed int | - | - | - | - |
| 0x0087 | Kupplungsposition Rohwert redundanter Sensor | Ink | high | signed int | - | - | - | - |
| 0x0088 | Kupplungsposition Sollwert | Ink | high | signed int | - | - | - | - |
| 0x0089 | Bremssignale resetfest: | 0-n | - | 0xFF | FUmweltTexte19 | - | - | - |
| 0x008A | Digitaleingang 1 resetfest: | 0-n | high | 0xFFFF | FUmweltTexte30 | - | - | - |
| 0x008B | Aktueller Gang resetfest 0= Neutral, 1-7= Gang, 8= Rueckwaertsgang | - | high | unsigned char | - | - | - | - |
| 0x008C | Kilometerstand Istwert resetfest | km | high | unsigned int | - | 8 | - | - |
| 0x008D | Motordrehzahl resetfest | 1/min | high | signed int | - | - | - | - |
| 0x008E | Kupplungsposition Istwert resetfest | Ink | high | signed int | - | - | - | - |
| 0x008F | Kupplungsposition Sollwert resetfest | Ink | high | signed int | - | - | - | - |
| 0x0090 | Getriebestatus resetfest: | 0-n | - | 0xFF | FUmweltTexte3 | - | - | - |
| 0x0091 | Spannungsversorgung Ubatt im resetfesten Bereich | V | high | signed int | - | - | 1024 | - |
| 0x0092 | Radgeschwindigkeit der Hinterachse im resetfesten Bereich | km/h | high | signed int | - | - | 16 | - |
| 0x0093 | Radgeschwindigkeit der Vorderachse im resetfesten Bereich | km/h | high | signed int | - | - | 16 | - |
| 0x0094 | Spannungsversorgung Ubatt Rohwert resetfest | V | high | signed int | - | 25 | 1024 | - |
| 0x0095 | Gewuenschter Gang resetfest 0= Neutral, 1-7= Gang, 8= Rueckwaertsgang | - | - | unsigned char | - | - | - | - |
| 0x0096 | Reset-Counter MC | - | - | unsigned char | - | - | - | - |
| 0x0097 | Reset-Counter MU | - | - | unsigned char | - | - | - | - |
| 0x0098 | Getriebestatus: | 0-n | - | 0xFF | FUmweltTexte3 | - | - | - |
| 0x0099 | Kupplungsstatus: | 0-n | - | 0xFF | FUmweltTexte4 | - | - | - |
| 0x009A | Schluesselnummer (CAN): | 0-n | - | 0xFF | FUmweltTexte21 | - | - | - |
| 0x009B | Resetzaehler Sicherheitskonzept Getriebe | - | - | unsigned char | - | - | - | - |
| 0x009C | Byte Fehlervariable des Sicherheitskonzeptes Getriebe | - | high | unsigned int | - | - | - | - |
| 0x009D | SPI Timeout | - | high | unsigned int | - | - | - | - |
| 0x009E | SPI Hardwarefehler | - | high | unsigned char | - | - | - | - |
| 0x009F | Byte Status BIOS-SW | - | high | unsigned int | - | - | - | - |
| 0x00A0 | Kennzeichnung Fehler Bremssignal | - | - | unsigned char | - | - | - | - |
| 0x00A1 | Fehlerstatus CAN Bus: | 0-n | - | 0xFF | FUmweltTexte31 | - | - | - |
| 0x00A2 | Fehlerstatus PWM-Ausgang Kupplung: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A3 | Fehlerstatus PWM-Ausgang Druckregler 1: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A4 | Fehlerstatus PWM-Ausgang Druckregler 2: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A5 | Fehlerstatus PWM-Ausgang Schaltzylinder 2/4: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A6 | Fehlerstatus PWM-Ausgang Schaltzylinder 5/3: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A7 | Fehlerstatus PWM-Ausgang Schaltzylinder 6/7: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A8 | Fehlerstatus PWM-Ausgang Schaltzylinder R/1: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00A9 | Kennzeichnung fehlerhafte Motordrehzahl: | 0-n | - | 0xFF | FUmweltTexte33 | - | - | - |
| 0x00AA | Fehlerstatus Netzwerk Manangement: | 0-n | - | 0xFF | FUmweltTexte29 | - | - | - |
| 0x00AB | Fehlerstatus Ansteuerung Hydraulikpumpe: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00AC | Kennzeichnung fehlerhafter Kupplungspositionssensor: | 0-n | - | 0xFF | FUmweltTexte34 | - | - | - |
| 0x00AD | Kennzeichnung fehlerhafter Getriebepositionssensor R/1: | 0-n | - | 0xFF | FUmweltTexte34 | - | - | - |
| 0x00AE | Fehlerstatus Ansteuerung Shift Lock: | 0-n | - | 0xFF | FUmweltTexte34 | - | - | - |
| 0x00AF | Fehlerstatus Ansteuerung Relais Anlasser: | 0-n | - | 0xFF | FUmweltTexte34 | - | - | - |
| 0x00B0 | Kennzeichnung fehlerhafte Fahrzeuggeschwindigkeit | - | - | unsigned char | - | - | - | - |
| 0x00B1 | Kennzeichnung fehlerhafte Raddrehzahl hinten links | - | - | unsigned char | - | - | - | - |
| 0x00B2 | Kennzeichnung fehlerhafte Raddrehzahl hinten rechts | - | - | unsigned char | - | - | - | - |
| 0x00B3 | Kennzeichnung fehlerhafte Raddrehzahl vorne links | - | - | unsigned char | - | - | - | - |
| 0x00B4 | Kennzeichnung fehlerhafte Raddrehzahl vorne rechts | - | - | unsigned char | - | - | - | - |
| 0x00B5 | Handbremssignal gefilterter Rohwert | 0/1 | high | 0x0001 | - | - | - | - |
| 0x00B6 | Programmwahlschalter Plus gefilterter Rohwert (Digitaleingang 1) | 0/1 | high | 0x0800 | - | - | - | - |
| 0x00B7 | Programmwahlschalter Minus gefilterter Rohwert (Digitaleingang 1) | 0/1 | high | 0x1000 | - | - | - | - |
| 0x00B8 | Motorhaubenkontakt 1 gefilterter Rohwert (Digitaleingang 1) | 0/1 | high | 0x4000 | - | - | - | - |
| 0x00B9 | Motorhaubenkontakt 2 gefilterter Rohwert (Digitaleingang 1) | 0/1 | high | 0x8000 | - | - | - | - |
| 0x00BA | Waehlhebelsignal S1 gefilterter Rohwert | 0/1 | high | 0x0004 | - | - | - | - |
| 0x00BB | Waehlhebelsignal S2 gefilterter Rohwert | 0/1 | high | 0x0008 | - | - | - | - |
| 0x00BC | Waehlhebelsignal E1 gefilterter Rohwert | 0/1 | high | 0x0010 | - | - | - | - |
| 0x00BD | Waehlhebelsignal E2 gefilterter Rohwert | 0/1 | high | 0x0020 | - | - | - | - |
| 0x00BE | Waehlhebelsignal N1 gefilterter Rohwert | 0/1 | high | 0x0040 | - | - | - | - |
| 0x00BF | Waehlhebelsignal N2 gefilterter Rohwert | 0/1 | high | 0x0080 | - | - | - | - |
| 0x00C0 | Waehlhebelsignal R1 gefilterter Rohwert | 0/1 | high | 0x0100 | - | - | - | - |
| 0x00C1 | Waehlhebelsignal R2 gefilterter Rohwert | 0/1 | high | 0x0200 | - | - | - | - |
| 0x00C2 | Wake up gefilterter Rohwert (Digitaleingang 2) | 0/1 | high | 0x0001 | - | - | - | - |
| 0x00C3 | Lenkradschalter Plus gefilterter Rohwert (Digitalwert 2) | 0/1 | high | 0x0020 | - | - | - | - |
| 0x00C4 | Lenkradschalter Minus gefilterter Rohwert (Digitalwert 2) | 0/1 | high | 0x0040 | - | - | - | - |
| 0x00C5 | Status Shift Lock (Digitaleingang) Rohwert | 0/1 | high | 0x0001 | - | - | - | - |
| 0x00C6 | Status Getriebeoelpumpenrelais Rohwert | 0/1 | high | 0x0200 | - | - | - | - |
| 0x00C8 | Status Ansteuerung HSD 1 (Digitalausgang) Rohwert | 0/1 | high | 0x2000 | - | - | - | - |
| 0x00C9 | Status Ansteuerung HSD 2 (Digitalausgang) Rohwert | 0/1 | high | 0x4000 | - | - | - | - |
| 0x00CA | Status Ansteuerung HSD 3 (Digitalausgang) Rohwert | 0/1 | high | 0x8000 | - | - | - | - |
| 0x00CB | Status Anlasserfreigabe (Digitalausgang) | 0/1 | high | 0x0080 | - | - | - | - |
| 0x00CC | Status Hydraulikpumpenrelais (Digitalausgang) | 0/1 | high | 0x0100 | - | - | - | - |
| 0x00CD | Status Waehlhebel LED N (Digitalausgang) Rohwert | 0/1 | high | 0x0200 | - | - | - | - |
| 0x00CE | Status Bremsdruck (CAN): | 0-n | - | 0xFF | FUmweltTexte35 | - | - | - |
| 0x00CF | Status DSC (CAN): | 0-n | - | 0xFF | FUmweltTexte36 | - | - | - |
| 0x00D0 | Klemmenstatus 15 (CAN): | 0-n | - | 0xFF | FUmweltTexte37 | - | - | - |
| 0x00D1 | Klemmenstatus 50 (CAN): | 0-n | - | 0xFF | FUmweltTexte38 | - | - | - |
| 0x00D2 | Klemmenstatus R (CAN): | 0-n | - | 0xFF | FUmweltTexte39 | - | - | - |
| 0x00D3 | Status Lenkwinkel (CAN): | 0-n | - | 0xFF | FUmweltTexte40 | - | - | - |
| 0x00D4 | Status Drehmoment Motor (CAN): | 0-n | - | 0xFF | FUmweltTexte41 | - | - | - |
| 0x00D5 | Byte OBD Steuerfunktion (CAN) | - | - | unsigned char | - | - | - | - |
| 0x00D6 | Status Quittierung DSC ACC (CAN): | 0-n | - | 0xFF | FUmweltTexte24 | - | - | - |
| 0x00D7 | Status Regelung (CAN): | 0-n | - | 0xFF | FUmweltTexte22 | - | - | - |
| 0x00D8 | Status Schluesselnummer (CAN): | 0-n | - | 0xFF | FUmweltTexte42 | - | - | - |
| 0x00D9 | Status Geschwindigkeitsregler (CAN): | 0-n | - | 0xFF | FUmweltTexte43 | - | - | - |
| 0x00DA | Status Verzoegerung (CAN): | 0-n | - | 0xFF | FUmweltTexte26 | - | - | - |
| 0x00DB | Status Schalter Warmlauf (CAN): | 0-n | - | 0xFF | FUmweltTexte27 | - | - | - |
| 0x00DC | Byte Fehlerursache Sicherheitskonzept Kupplung | - | - | unsigned char | - | - | - | - |
| 0x00DD | Variable fuers Abschalten | - | - | unsigned char | - | - | - | - |
| 0x00DE | Variable fuers Initialisieren: | 0-n | - | 0xFF | FUmweltTexte48 | - | - | - |
| 0x00DF | Fehlerstatus Ansteuerung Waehlhebel LED R: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00E0 | Fehlerstatus Ansteuerung Waehlhebel LED N: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00E1 | Fehlerstatus Ansteuerung Waehlhebel LED S/D: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x00E2 | Adaption bzw. Testprogramm   : | 0-n | - | 0xFF | FUmweltTexte51 | - | - | - |
| 0x00E3 | Fehlermeldung einer Adaption : | 0-n | - | 0xFF | FUmweltTexte52 | - | - | - |
| 0x00E4 | Adaptionzustand im Fehlerfall: | 0-n | - | 0xFF | FUmweltTexte53 | - | - | - |
| 0x00E5 | Laengsbeschleunigung Rohwert | mV | high | signed int | - | 4.833 | - | - |
| 0x00E6 | Radgeschwindigkeit der Hinterachse | km/h | high | signed int | - | - | 16 | - |
| 0x00E7 | Radgeschwindigkeit hinten links (CAN) | km/h | high | signed int | - | - | 16 | - |
| 0x00E8 | Radgeschwindigkeit hinten rechts (CAN) | km/h | high | signed int | - | - | 16 | - |
| 0x00E9 | Radgeschwindigkeit der Vorderachse | km/h | high | signed int | - | - | 16 | - |
| 0x00EA | Hydraulikdruck Rohwert | bar | high | signed int | - | 0.1 | - | - |
| 0x00EB | Sensorspannungsversorgung A Rohwert | V | high | signed int | - | - | 1024 | - |
| 0x00EC | Sensorspannungsversorgung B Rohwert | V | high | signed int | - | - | 1024 | - |
| 0x00ED | Hydrauliktemperatur Rohwert | Grad C | high | unsigned char | - | - | - | -48 |
| 0x00EE | Radgeschwindigkeit vorne links (CAN) | km/h | high | signed int | - | - | 16 | - |
| 0x00EF | Radgeschwindigkeit vorne rechts (CAN) | km/h | high | signed int | - | - | 16 | - |
| 0x00F0 | Spannungsversorgung Ubatt Rohwert | V | high | signed int | - | - | 1024 | - |
| 0x00F1 | Gewuenschter Gang 0=N, 1-7, 8=R | - | - | unsigned char | - | - | - | - |
| 0x00F2 | Status Tuerkontakt (CAN): | 0-n | - | 0xFF | FUmweltTexte45 | - | - | - |
| 0x00F3 | Byte Umgebungsvariable Sicherheitskonzept Kupplung | - | high | unsigned int | - | - | - | - |
| 0x00F4 | Fahrtichtung vorwaerts | 0/1 | high | 0x0001 | - | - | - | - |
| 0x00F5 | Fahrtichtung neutral | 0/1 | high | 0x0002 | - | - | - | - |
| 0x00F6 | Fahrtichtung rueckwaerts | 0/1 | high | 0x0004 | - | - | - | - |
| 0x00F7 | Fahrtichtungsignal ungueltig | 0/1 | high | 0x0010 | - | - | - | - |
| 0x00F8 | Waehlhebel in R (Rueckwaerts) | 0/1 | high | 0x0020 | - | - | - | - |
| 0x00F9 | Waehlhebel in 0 (Neutral) | 0/1 | high | 0x0040 | - | - | - | - |
| 0x00FA | Waehlhebel in A (Automatik) | 0/1 | high | 0x0080 | - | - | - | - |
| 0x00FB | Waehlhebel in S (Sequentiell) | 0/1 | high | 0x0100 | - | - | - | - |
| 0x00FC | Waehlhebel in + (Gang hoch) | 0/1 | high | 0x0200 | - | - | - | - |
| 0x00FD | Waehlhebel in - (Gang runter) | 0/1 | high | 0x0400 | - | - | - | - |
| 0x00FE | Waehlhebelposition nicht definiert | 0/1 | high | 0x0800 | - | - | - | - |
| 0x0100 | Handbremssignal CAN aktiv | 0/1 | high | 0x01 | - | - | - | - |
| 0x0101 | Handbremssignal gefiltert Rohwert aktiv | 0/1 | high | 0x02 | - | - | - | - |
| 0x0102 | Handbremssignal gefiltert Istwert aktiv | 0/1 | high | 0x04 | - | - | - | - |
| 0x0103 | Kennzeichung Fehler Antriebsdrehzahlen 1 | - | high | unsigned char | - | - | - | - |
| 0x0104 | Kennzeichung Fehler Antriebsdrehzahlen 2 | - | high | unsigned char | - | - | - | - |
| 0x0105 | Getriebestatus : geschaltet | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0106 | Getriebestatus : aktiv | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0107 | Getriebestatus : Zwischenkuppeln | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0108 | Getriebestatus : Synchronisation | 0/1 | high | 0x0008 | - | - | - | - |
| 0x0109 | Getriebestatus : Schaltweg Neutral | 0/1 | high | 0x0010 | - | - | - | - |
| 0x010A | Getriebestatus : Vorspannen | 0/1 | high | 0x0020 | - | - | - | - |
| 0x010B | Getriebestatus : Getriebeinitialisierung aktiv | 0/1 | high | 0x0040 | - | - | - | - |
| 0x010C | Getriebestatus : Synchronisation fertig | 0/1 | high | 0x0080 | - | - | - | - |
| 0x010D | Getriebestatus : Vor Synchronisation | 0/1 | high | 0x0100 | - | - | - | - |
| 0x010E | Getriebestatus : Vor Synchronisation aktiv | 0/1 | high | 0x0200 | - | - | - | - |
| 0x010F | Kupplungsstatus: offen | 0/1 | high | 0x0400 | - | - | - | - |
| 0x0110 | Kupplungsstatus: geschlossen | 0/1 | high | 0x0800 | - | - | - | - |
| 0x0111 | Kupplungsstatus: oeffnet | 0/1 | high | 0x1000 | - | - | - | - |
| 0x0112 | Kupplungsstatus: schliesst | 0/1 | high | 0x2000 | - | - | - | - |
| 0x0113 | Kupplungsstatus: Zwischenkuppeln aktiv | 0/1 | high | 0x4000 | - | - | - | - |
| 0x0114 | Fussbremse aktiv | 0/1 | high | 0x8000 | - | - | - | - |
| 0x0115 | Fahrpedal Rohwert | % | high | unsigned char | - | - | - | - |
| 0x0116 | Klemme R aus | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0117 | Klemme R ein | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0118 | Signal Klemme R ungueltig | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0119 | Klemme 15 aus | 0/1 | high | 0x0008 | - | - | - | - |
| 0x011A | Klemme 15 ein | 0/1 | high | 0x0010 | - | - | - | - |
| 0x011B | Signal Klemme 15 ungueltig | 0/1 | high | 0x0020 | - | - | - | - |
| 0x011C | Klemme 50 aus | 0/1 | high | 0x0040 | - | - | - | - |
| 0x011D | Klemme 50 ein | 0/1 | high | 0x0080 | - | - | - | - |
| 0x011E | Signal Klemme 50 ungueltig | 0/1 | high | 0x0100 | - | - | - | - |
| 0x011F | Sollwert Status Shift Lock (0=Waehlhebel gesperrt, 1=nicht gesperrt) | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0120 | Sollwert Status Waehlhebel LED R | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0121 | Sollwert Status Weahlhebel LED S/D | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0122 | Sollwert Status Anlasserfreigabe | 0/1 | high | 0x0008 | - | - | - | - |
| 0x0123 | Sollwert Status Hydraulikpumpenrelais | 0/1 | high | 0x0010 | - | - | - | - |
| 0x0124 | Sollwert Status Waehlhebel LED N | 0/1 | high | 0x0020 | - | - | - | - |
| 0x0125 | Rohwert Status Shift Lock (0=Waehlhebel gesperrt, 1=nicht gesperrt) | 0/1 | high | 0x0040 | - | - | - | - |
| 0x0126 | Rohwert Status Waehlhebel LED R | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0127 | Rohwert Status Waehlhebel LED S/D | 0/1 | high | 0x0100 | - | - | - | - |
| 0x0128 | Rohwert Status Notansteuerung HSD1 | 0/1 | high | 0x0200 | - | - | - | - |
| 0x0129 | Rohwert Status Notansteuerung HSD2 | 0/1 | high | 0x0400 | - | - | - | - |
| 0x012A | Rohwert Status Notansteuerung HSD3 | 0/1 | high | 0x0800 | - | - | - | - |
| 0x012B | Rohwert Status Anlasserfreigabe | 0/1 | high | 0x1000 | - | - | - | - |
| 0x012C | Rohwert Status Hydraulikpumpenrelais | 0/1 | high | 0x2000 | - | - | - | - |
| 0x012D | Rohwert Status Waehlhebel LED N | 0/1 | high | 0x4000 | - | - | - | - |
| 0x012E | Zuendung aus | 0/1 | high | 0x0001 | - | - | - | - |
| 0x012F | Radio Ein-Stellung | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0130 | Fahrtstellung | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0131 | Anlassen | 0/1 | high | 0x0008 | - | - | - | - |
| 0x0132 | Bremssignal: Fussbremse betaetigt | 0/1 | high | 0x0010 | - | - | - | - |
| 0x0133 | Bremssignal: Handbremse betaetigt | 0/1 | high | 0x0020 | - | - | - | - |
| 0x0134 | Fehlerstatus Shift Lock: Kurzschluss nach Masse | 0/1 | high | 0x0040 | - | - | - | - |
| 0x0135 | Fehlerstatus Shift Lock: Kurzschluss nach Ubatt | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0136 | Fehlerstatus Shift Lock: Leitungsunterbrechung | 0/1 | high | 0x0100 | - | - | - | - |
| 0x0137 | Fehlerstatus Anlasserfreigabe: Kurzschluss nach Masse | 0/1 | high | 0x0200 | - | - | - | - |
| 0x0138 | Fehlerstatus Anlasserfreigabe: Kurzschluss nach Ubatt | 0/1 | high | 0x0400 | - | - | - | - |
| 0x0139 | Fehlerstatus Anlasserfreigabe: Leitungsunterbrechung | 0/1 | high | 0x0800 | - | - | - | - |
| 0x013A | Fehlerstatus Ansteuerung Waehlhebel LED R: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x013B | Fehlerstatus Ansteuerung Waehlhebel LED N: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x013C | Fehlerstatus Ansteuerung Waehlhebel LED D/S: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x013D | Ungueltige Checks. der Abgleichwerte | 0/1 | high | 0x01 | - | - | - | - |
| 0x013E | Fehler EEPROM-Daten | 0/1 | high | 0x02 | - | - | - | - |
| 0x013F | Fehler Oszillatorfrequenz | 0/1 | high | 0x04 | - | - | - | - |
| 0x0140 | Fehler SPI Kommunikation | 0/1 | high | 0x08 | - | - | - | - |
| 0x0141 | ESTATE (1=Motor ein) | 0/1 | high | 0x0400 | - | - | - | - |
| 0x0142 | Kennzeichnung Fehler Bremssignal: | 0-n | - | 0xFF | FUmweltTexte46 | - | - | - |
| 0x0143 | Status Motordrehzahl CAN: | 0-n | - | 0xFF | FUmweltTexte47 | - | - | - |
| 0x0144 | Handbremse (1=angezogen) (Digitaleingang resetfest) | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0145 | frei (Digitaleingang resetfest) | 0/1 | high | 0x0002 | - | - | - | - |
| 0x0146 | Waehlhebelschalter S1 (Digitaleingang resetfest) | 0/1 | high | 0x0004 | - | - | - | - |
| 0x0147 | Waehlhebelschalter S2 (Digitaleingang resetfest) | 0/1 | high | 0x0008 | - | - | - | - |
| 0x0148 | Waehlhebelschalter E1 (Digitaleingang resetfest) | 0/1 | high | 0x0010 | - | - | - | - |
| 0x0149 | Waehlhebelschalter E2 (Digitaleingang resetfest) | 0/1 | high | 0x0020 | - | - | - | - |
| 0x014A | Waehlhebelschalter N1 (Digitaleingang resetfest) | 0/1 | high | 0x0040 | - | - | - | - |
| 0x014B | Waehlhebelschalter N2 (Digitaleingang resetfest) | 0/1 | high | 0x0080 | - | - | - | - |
| 0x014C | Waehlhebelschalter R1 (Digitaleingang resetfest) | 0/1 | high | 0x0100 | - | - | - | - |
| 0x014D | Waehlhebelschalter R2 (Digitaleingang resetfest) | 0/1 | high | 0x0200 | - | - | - | - |
| 0x014E | ESTATE (1=Motor ein) (Digitaleingang resetfest) | 0/1 | high | 0x0400 | - | - | - | - |
| 0x014F | Programmwahlschalter PLUS (Digitaleingang resetfest) | 0/1 | high | 0x0800 | - | - | - | - |
| 0x0150 | Programmwahlschalter MINUS (Digitaleingang resetfest) | 0/1 | high | 0x1000 | - | - | - | - |
| 0x0151 | frei (Digitaleingang resetfest) | 0/1 | high | 0x2000 | - | - | - | - |
| 0x0152 | Motorhaubenkontakt 2 (rechts) (1=geschlossen) (Digitaleingang resetfest) | 0/1 | high | 0x4000 | - | - | - | - |
| 0x0153 | Motorhaubenkontakt 1 (links) (1=geschlossen) (Digitaleingang resetfest) | 0/1 | high | 0x8000 | - | - | - | - |
| 0x0154 | Getriebe gibt Abschaltfreigabe | 0/1 | high | 0x01 | - | - | - | - |
| 0x0155 | Kupplung gibt Abschaltfreigabe | 0/1 | high | 0x02 | - | - | - | - |
| 0x0156 | Wird nicht in NVRAM gespeichert | 0/1 | high | 0x04 | - | - | - | - |
| 0x0157 | Sofortabschaltung | 0/1 | high | 0x08 | - | - | - | - |
| 0x0158 | Botschaft Aussentemperatur/Relativzeit korrekt emfangen | 0/1 | high | 0x0001 | - | - | - | - |
| 0x0159 | Botschaft Bedienung Getriebewahlschalter korrekt empfangen | 0/1 | high | 0x0002 | - | - | - | - |
| 0x015A | Botschaft Geschwindigkeit korrekt empfangen | 0/1 | high | 0x0004 | - | - | - | - |
| 0x015B | Botschaft Kilometerstand /Reichweite korrekt empfangen | 0/1 | high | 0x0008 | - | - | - | - |
| 0x015C | Botschaft Klemmenstatus korrekt empfangen | 0/1 | high | 0x0010 | - | - | - | - |
| 0x015D | Botschaft Lenkradwinkel korrekt empfangen | 0/1 | high | 0x0020 | - | - | - | - |
| 0x015E | Botschaft Radgeschwindigkeit korrekt empfangen | 0/1 | high | 0x0040 | - | - | - | - |
| 0x015F | Botschaft Radtoleranzabgleich korrekt empfangen | 0/1 | high | 0x0080 | - | - | - | - |
| 0x0160 | Botschaft Anhaenger korrekt empfangen | 0/1 | high | 0x0100 | - | - | - | - |
| 0x0161 | Botschaft DSC korrekt empfangen | 0/1 | high | 0x0200 | - | - | - | - |
| 0x0162 | Botschaft Kombi korrekt empfangen | 0/1 | high | 0x0400 | - | - | - | - |
| 0x0163 | Botschaft ZV und Klappenzustand korrekt empfangen | 0/1 | high | 0x0800 | - | - | - | - |
| 0x0164 | Botschaft Status Fahrlicht korrekt empfangen | 0/1 | high | 0x1000 | - | - | - | - |
| 0x0165 | Botschaft Raddruecke korrekt empfangen | 0/1 | high | 0x2000 | - | - | - | - |
| 0x0166 | Botschaft Anzeige Checkcontrol Meldung korrekt gesendet | 0/1 | high | 0x01 | - | - | - | - |
| 0x0167 | Botschaft Anzeige Getriebedaten korrekt gesendet | 0/1 | high | 0x02 | - | - | - | - |
| 0x0168 | Botschaft Drehmomentanforderung EGS korrekt gesendet | 0/1 | high | 0x04 | - | - | - | - |
| 0x0169 | Botschaft Verzoergungsanforderung korrekt gesendet | 0/1 | high | 0x08 | - | - | - | - |
| 0x016A | Botschaft Rohdaten Laengsbeschleunigung korrekt Empfangen | 0/1 | high | 0x10 | - | - | - | - |
| 0x016B | Botschaft Getriebedaten korrekt Empfangen | 0/1 | high | 0x20 | - | - | - | - |
| 0x016C | Botschaft DME 1 korrekt empfangen | 0/1 | high | 0x01 | - | - | - | - |
| 0x016D | Botschaft DME 2 korrekt empfangen | 0/1 | high | 0x02 | - | - | - | - |
| 0x016E | Botschaft DME 3 korrekt empfangen | 0/1 | high | 0x04 | - | - | - | - |
| 0x016F | Botschaft Drehmoment 1 korrekt empfangen | 0/1 | high | 0x08 | - | - | - | - |
| 0x0170 | Botschaft Drehmoment 2 korrekt empfangen | 0/1 | high | 0x10 | - | - | - | - |
| 0x0171 | Botschaft Motordaten korrekt empfangen | 0/1 | high | 0x20 | - | - | - | - |
| 0x0172 | Botschaft M-Drive korrekt empfangen | 0/1 | high | 0x40 | - | - | - | - |
| 0x0173 | Botschaft SMG 1 korrekt gesendet | 0/1 | high | 0x01 | - | - | - | - |
| 0x0174 | Botschaft SMG 2 korrekt gesendet | 0/1 | high | 0x02 | - | - | - | - |
| 0x0175 | Botschaft SMG 3 korrekt gesendet | 0/1 | high | 0x04 | - | - | - | - |
| 0x0176 | Getriebetemperatur | Grad | high | unsigned char | - | - | - | -48 |
| 0x0177 | Einschaltdauer HE-Motor, kleine Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x0178 | Einschaltdauer HE-Motor, mittlere Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x0179 | Einschaltdauer HE-Motor, grosse Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x017A | Anzahl Getriebeschaltungen, kleine Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x017B | Anzahl Getriebeschaltungen, mittlere Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x017C | Anzahl Getriebeschaltungen, grosse Zeitbasis | - | high | unsigned char | - | - | - | - |
| 0x017D | Fehlerstatus Ansteuerung Getrieboelpumpenrelais: | 0-n | - | 0xFF | FUmweltTexte32 | - | - | - |
| 0x017E | Zeitdauer des erkannten Uebersetzungsverhaeltnises | - | high | unsigned int | - | - | - | - |
| 0x017F | Aus Uebersetzungverhältnis erkannter Gang | - | high | unsigned char | - | - | - | - |
| 0x0180 | Status System-Reset: | 0-n | high | 0xFF | FUmweltTexte49 | - | - | - |
| 0x0181 | PWM Wert der LED Ansteuerung | - | high | unsigned int | - | - | - | - |
| 0x0182 | Fehlerstatus Ventil: | 0-n | - | 0xFF | FUmweltTexte50 | - | - | - |

<a id="table-harttyp"></a>
### HARTTYP

Dimensions: 124 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x5000 | 0x00 | 0x00 | 0x09 | 0x00 |
| 0x5001 | 0x0A | 0x00 | 0x00 | 0x00 |
| 0x5002 | 0x0E | 0x0D | 0x0C | 0x0B |
| 0x5003 | 0x00 | 0x00 | 0x00 | 0x0F |
| 0x5004 | 0x00 | 0x00 | 0x10 | 0x00 |
| 0x5005 | 0x00 | 0x00 | 0x11 | 0x00 |
| 0x5006 | 0x00 | 0x00 | 0x12 | 0x00 |
| 0x5007 | 0x00 | 0x00 | 0x13 | 0x00 |
| 0x5008 | 0x00 | 0x00 | 0x14 | 0x00 |
| 0x5100 | 0x00 | 0x00 | 0x17 | 0x16 |
| 0x5101 | 0xF9 | 0x1A | 0x19 | 0x18 |
| 0x5102 | 0x1D | 0x00 | 0x1C | 0x1B |
| 0x5103 | 0x00 | 0x00 | 0x1F | 0x1E |
| 0x5104 | 0x00 | 0x00 | 0x21 | 0x20 |
| 0x5105 | 0x00 | 0x00 | 0x23 | 0x22 |
| 0x5106 | 0x26 | 0xFD | 0x25 | 0x24 |
| 0x5107 | 0x29 | 0xFE | 0x28 | 0x27 |
| 0x5108 | 0x2C | 0xFF | 0x2B | 0x2A |
| 0x5109 | 0x2F | 0x0100 | 0x2E | 0x2D |
| 0x510A | 0x32 | 0x0101 | 0x31 | 0x30 |
| 0x510B | 0x35 | 0x00 | 0x34 | 0x33 |
| 0x510C | 0x38 | 0x00 | 0x37 | 0x36 |
| 0x510D | 0x3B | 0x0106 | 0x3A | 0x39 |
| 0x510E | 0x3E | 0x0107 | 0x3D | 0x3C |
| 0x5200 | 0x41 | 0x00 | 0x40 | 0x3F |
| 0x5201 | 0x44 | 0x00 | 0x43 | 0x42 |
| 0x5202 | 0x47 | 0x00 | 0x46 | 0x45 |
| 0x5203 | 0x4A | 0x00 | 0x49 | 0x48 |
| 0x5204 | 0x4D | 0x00 | 0x4C | 0x4B |
| 0x5206 | 0x4E | 0x00 | 0x00 | 0x00 |
| 0x5208 | 0x4F | 0x00 | 0x00 | 0x00 |
| 0x5209 | 0x50 | 0x00 | 0x00 | 0x00 |
| 0x520A | 0x51 | 0x00 | 0x00 | 0x00 |
| 0x520B | 0x52 | 0x00 | 0x00 | 0x00 |
| 0x520C | 0x53 | 0x00 | 0x00 | 0x00 |
| 0x520D | 0x54 | 0x00 | 0x00 | 0x00 |
| 0x520E | 0x55 | 0x00 | 0x00 | 0x00 |
| 0x520F | 0x56 | 0x00 | 0x00 | 0x00 |
| 0x5210 | 0x57 | 0x00 | 0x00 | 0x00 |
| 0x5211 | 0x58 | 0x00 | 0x00 | 0x00 |
| 0x5212 | 0x59 | 0x00 | 0x00 | 0x00 |
| 0x5213 | 0x5A | 0x00 | 0x00 | 0x00 |
| 0x5214 | 0x5B | 0x00 | 0x00 | 0x00 |
| 0x5215 | 0x5C | 0x00 | 0x00 | 0x00 |
| 0x5217 | 0x5D | 0x00 | 0x00 | 0x00 |
| 0x5218 | 0x5E | 0x00 | 0x00 | 0x00 |
| 0x521A | 0x5F | 0x00 | 0x00 | 0x00 |
| 0x521B | 0x60 | 0x00 | 0x00 | 0x00 |
| 0x521C | 0x61 | 0x00 | 0x00 | 0x00 |
| 0x5400 | 0x00 | 0x64 | 0x63 | 0x62 |
| 0x5401 | 0x00 | 0x67 | 0x66 | 0x65 |
| 0x5402 | 0xFA | 0x6A | 0x69 | 0x68 |
| 0x5403 | 0x00 | 0x00 | 0x6B | 0x00 |
| 0x5404 | 0x00 | 0x00 | 0x6E | 0x00 |
| 0x5405 | 0x00 | 0x00 | 0x71 | 0x00 |
| 0x5406 | 0x00 | 0xF8 | 0xF7 | 0xF6 |
| 0x5500 | 0x77 | 0x76 | 0x75 | 0x74 |
| 0x5501 | 0x7B | 0x7A | 0x79 | 0x78 |
| 0x5502 | 0x7F | 0x7E | 0x7D | 0x7C |
| 0x5503 | 0x83 | 0x82 | 0x81 | 0x80 |
| 0x5504 | 0x87 | 0x86 | 0x85 | 0x84 |
| 0x5505 | 0x8B | 0x8A | 0x89 | 0x88 |
| 0x5506 | 0x8F | 0x8E | 0x8D | 0x8C |
| 0x5507 | 0x00 | 0x00 | 0x90 | 0x00 |
| 0x5508 | 0x00 | 0x00 | 0x91 | 0x00 |
| 0x5509 | 0x00 | 0x00 | 0x92 | 0x00 |
| 0xCF12 | 0x00 | 0x93 | 0x00 | 0x00 |
| 0xCF13 | 0x00 | 0x94 | 0x00 | 0x00 |
| 0xCF14 | 0x00 | 0x95 | 0x00 | 0x00 |
| 0xCF15 | 0x00 | 0x97 | 0x96 | 0x00 |
| 0xCF16 | 0x9A | 0x99 | 0x98 | 0x00 |
| 0xCF17 | 0x00 | 0x9B | 0x00 | 0x00 |
| 0xCF18 | 0x9E | 0x9D | 0x9C | 0x00 |
| 0xCF19 | 0x00 | 0x9F | 0x00 | 0x00 |
| 0xCF1A | 0x00 | 0xA0 | 0x00 | 0x00 |
| 0xCF1B | 0x00 | 0xA1 | 0x00 | 0x00 |
| 0xCF1C | 0x00 | 0xA2 | 0x00 | 0x00 |
| 0xCF1D | 0xA5 | 0xA4 | 0xA3 | 0x00 |
| 0xCF1E | 0xA8 | 0xA7 | 0xA6 | 0x00 |
| 0xCF1F | 0x00 | 0xA9 | 0x00 | 0x00 |
| 0xCF30 | 0x00 | 0xAA | 0x00 | 0x00 |
| 0xCF31 | 0x00 | 0xAB | 0x00 | 0x00 |
| 0xCF32 | 0x00 | 0xAC | 0x00 | 0x00 |
| 0xCF33 | 0x00 | 0xAD | 0x00 | 0x00 |
| 0xCF34 | 0x00 | 0xAE | 0x00 | 0x00 |
| 0xCF38 | 0x00 | 0xAF | 0x00 | 0x00 |
| 0xCF07 | 0x00 | 0xB0 | 0x00 | 0x00 |
| 0xCF25 | 0xB3 | 0xB2 | 0xB1 | 0x00 |
| 0xCF26 | 0xB6 | 0xB5 | 0xB4 | 0x00 |
| 0xCF27 | 0xB9 | 0xB8 | 0xB7 | 0x00 |
| 0xCF28 | 0xBC | 0xBB | 0xBA | 0x00 |
| 0xCF29 | 0xBF | 0xBE | 0xBD | 0x00 |
| 0xCF2A | 0x00 | 0xC1 | 0xC0 | 0x00 |
| 0xCF2B | 0xC4 | 0xC3 | 0xC2 | 0x00 |
| 0xCF35 | 0x00 | 0xC5 | 0x00 | 0x00 |
| 0xCF36 | 0x00 | 0xC6 | 0x00 | 0x00 |
| 0xCF37 | 0x00 | 0xC7 | 0x00 | 0x00 |
| 0xCF0B | 0x00 | 0xC8 | 0x00 | 0x00 |
| 0x4F00 | 0x00 | 0x00 | 0xC9 | 0x00 |
| 0x4F01 | 0x00 | 0x00 | 0xCA | 0x00 |
| 0x4F02 | 0x00 | 0x00 | 0xCB | 0x00 |
| 0x4F03 | 0x00 | 0x00 | 0xCC | 0x00 |
| 0x4F04 | 0x00 | 0x00 | 0xCD | 0x00 |
| 0x4F20 | 0x00 | 0x00 | 0xCE | 0x00 |
| 0x4F21 | 0xCF | 0x00 | 0x00 | 0x00 |
| 0x4F22 | 0xD0 | 0x0103 | 0x0102 | 0x00 |
| 0x4F40 | 0x00 | 0x00 | 0xD1 | 0x00 |
| 0x4F41 | 0x00 | 0x00 | 0x00 | 0xD2 |
| 0x4F42 | 0xFC | 0x00 | 0xFB | 0xD3 |
| 0x4F43 | 0x00 | 0x00 | 0x00 | 0xD4 |
| 0x4F44 | 0x00 | 0x00 | 0x00 | 0xD5 |
| 0x4F60 | 0xD6 | 0x00 | 0x00 | 0x00 |
| 0x4F61 | 0xD7 | 0x00 | 0x00 | 0x00 |
| 0x4F62 | 0x010A | 0xD8 | 0x00 | 0x010B |
| 0x4F63 | 0xD9 | 0x00 | 0x00 | 0x00 |
| 0x4F64 | 0xDA | 0x00 | 0x00 | 0x00 |
| 0x4F65 | 0x00 | 0xDD | 0xDC | 0xDB |
| 0x4F66 | 0x00 | 0x00 | 0x00 | 0xDE |
| 0x4F67 | 0x00 | 0x00 | 0x00 | 0xDF |
| 0x4F80 | 0xF3 | 0xF2 | 0xF1 | 0xF0 |
| 0x4F81 | 0x00 | 0x00 | 0x0105 | 0x0104 |
| 0x4FA0 | 0x0109 | 0x0108 | 0x00 | 0xF4 |
| 0x4FA1 | 0xF5 | 0x00 | 0x00 | 0x00 |
| default | 0x08 | 0x04 | 0x02 | 0x01 |

<a id="table-harttexteindividuell"></a>
### HARTTEXTEINDIVIDUELL

Dimensions: 243 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Signal oder Wert oberhalb Schwelle |
| 0x02 | Signal oder Wert unterhalb Schwelle |
| 0x04 | kein Signal oder Wert |
| 0x08 | unplausibles Signal oder Wert |
| 0x09 | Motorhaubenkontakt im Stand unplausibles Signal |
| 0x0A | Motorhaubenkontakt im Fahrbetrieb unplausibles Signal |
| 0x0B | Waehlhebel Totalausfall |
| 0x0C | Waehlhebel Einzelfehler R |
| 0x0D | Waehlhebel Einzelfehler N/E |
| 0x0E | Waehlhebel Einzelfehler S |
| 0x0F | Wake Up Kurzschluss gegen UBatt |
| 0x10 | Programmwahlschalter Plus Kurzschluss gegen Masse |
| 0x11 | Programmwahlschalter Minus Kurzschluss gegen Masse |
| 0x12 | Lenkradschalter Plus Kurzschluss gegen Masse |
| 0x13 | Lenkradschalter Minus Kurzschluss gegen Masse |
| 0x14 | Handbremssignal Kurzschluss gegen Masse |
| 0x15 | Hydraulikfuellstand |
| 0x16 | Hydrauliktemperatursensor Signal oberhalb Schwelle |
| 0x17 | Hydrauliktemperatursensor Signal unterhalb Schwelle |
| 0x18 | Hydraulikdrucksensor Signal oberhalb Schwelle |
| 0x19 | Hydraulikdrucksensor Signal unterhalb Schwelle |
| 0x1A | Hydraulikdrucksensor Masseleitung gebrochenl |
| 0x1B | Laengsbeschleunigungssensor Signal oberhalb Schwelle |
| 0x1C | Laengsbeschleunigungssensor Signal unterhalb Schwelle |
| 0x1D | Laengsbeschleunigungssensor unplausibles Signal |
| 0x1E | Spannungsversorgung UBatt Signal oberhalb Schwelle |
| 0x1F | Spannungsversorgung UBatt Signal unterhalb Schwelle |
| 0x20 | Sensorspannungsversorgung A Signal oberhalb Schwelle |
| 0x21 | Sensorspannungsversorgung A Signal unterhalb Schwelle |
| 0x22 | Sensorspannungsversorgung B Signal oberhalb Schwelle |
| 0x23 | Sensorspannungsversorgung B Signal unterhalb Schwelle |
| 0x24 | R/1 (Hauptsensor) Signal oberhalb Schwelle |
| 0x25 | R/1 (Hauptsensor) Signal unterhalb Schwelle |
| 0x26 | R/1 (Hauptsensor) unplausibles Signal |
| 0x27 | R/1 (redundanter Sensor) Signal oberhalb Schwelle |
| 0x28 | R/1 (redundanter Sensor) Signal unterhalb Schwelle |
| 0x29 | R/1 (redundanter Sensor) unplausibles Signal |
| 0x2A | 5/3 Signal oberhalb Schwelle |
| 0x2B | 5/3 Signal unterhalb Schwelle |
| 0x2C | 5/3 unplausibles Signal |
| 0x2D | 2/4 Signal oberhalb Schwelle |
| 0x2E | 2/4 Signal unterhalb Schwelle |
| 0x2F | 2/4 unplausibles Signal |
| 0x30 | 6/7 Signal oberhalb Schwelle |
| 0x31 | 6/7 Signal unterhalb Schwelle |
| 0x32 | 6/7 unplausibles Signal |
| 0x33 | Getriebeeingangsdrehzahl Signal oberhalb Schwelle |
| 0x34 | Getriebeeingangsdrehzahl Signal unterhalb Schwelle |
| 0x35 | Getriebeeingangsdrehzahl unplausibles Signal |
| 0x36 | Motordrehzahl (Sensorsignal) Signal oberhalb Schwelle |
| 0x37 | Motordrehzahl (Sensorsignal) Signal unterhalb Schwelle |
| 0x38 | Motordrehzahl (Sensorsignal) unplausibles Signal |
| 0x39 | Kupplungspositionsgeber (Hauptsensor) Signal oberhalb Schwelle |
| 0x3A | Kupplungspositionsgeber (Hauptsensor) Signal unterhalb Schwelle |
| 0x3B | Kupplungspositionsgeber (Hauptsensor) Kurzschluss gegen UBatt |
| 0x3C | Kupplungspositionsgeber (redundanter Sensor) Signal oberhalb Schwelle |
| 0x3D | Kupplungspositionsgeber (redundanter Sensor) Signal unterhalb Schwelle |
| 0x3E | Kupplungspositionsgeber (redundanter Sensor) Kurzschluss gegen UBatt |
| 0x3F | Motordrehzahl (CAN Signal) Signal oberhalb Schwelle |
| 0x40 | Motordrehzahl (CAN Signal) Signal unterhalb Schwelle |
| 0x41 | Motordrehzahl (CAN Signal) unplausibles Signal |
| 0x42 | Radgeschwindigkeit hinten links Signal oberhalb Schwelle |
| 0x43 | Radgeschwindigkeit hinten links Signal unterhalb Schwelle |
| 0x44 | Radgeschwindigkeit hinten links unplausibles Signal |
| 0x45 | Radgeschwindigkeit hinten rechts Signal oberhalb Schwelle |
| 0x46 | Radgeschwindigkeit hinten rechts Signal unterhalb Schwelle |
| 0x47 | Radgeschwindigkeit hinten rechts unplausibles Signal |
| 0x48 | Radgeschwindigkeit vorne links Signal oberhalb Schwelle |
| 0x49 | Radgeschwindigkeit vorne links Signal unterhalb Schwelle |
| 0x4A | Radgeschwindigkeit vorne links unplausibles Signal |
| 0x4B | Radgeschwindigkeit vorne rechts Signal oberhalb Schwelle |
| 0x4C | Radgeschwindigkeit vorne rechts Signal unterhalb Schwelle |
| 0x4D | Radgeschwindigkeit vorne rechts unplausibles Signal |
| 0x4E | Betriebsbremse unplausibles Signal |
| 0x4F | Drehmoment unplausibles Signal |
| 0x50 | Fahrpedal unplausibles Signal |
| 0x51 | Lenkwinkel unplausibles Signal |
| 0x52 | Querbeschleunigung unplausibles Signal |
| 0x53 | Laengsbeschleunigung unplausibles Signal |
| 0x54 | Leerlaufdrehzahl unplausibles Signal |
| 0x55 | Status Geschwindigkeitsregelung unplausibles Signal |
| 0x56 | Status Fahrertuer unplausibles Signal |
| 0x57 | Status Klemme R, 15 und 50 unplausibles Signal |
| 0x58 | Schluesselnummer unplausibles Signal |
| 0x59 | Status Anhaenger unplausibles Signal |
| 0x5A | Status Regelungen unplausibles Signal |
| 0x5B | Status DSC unplausibles Signal |
| 0x5C | Status Verzoegerung unplausibles Signal |
| 0x5D | Bremsdruck unplausibles Signal |
| 0x5E | Drehzahl Temperaturbereich 1 unplausibles Signal |
| 0x5F | Begrenzerdrehzahl unplausibles Signal |
| 0x60 | Status OBD Steuerfunktion unplausibles Signal |
| 0x61 | Status Schalter Warmlauf unplausibles Signal |
| 0x62 | Shift Lock Kurzschluss gegen UBatt |
| 0x63 | Shift Lock Kurzschluss gegen Masse |
| 0x64 | Shift Lock Leitungsunterbrechung |
| 0x65 | Anlasserfreigabe Kurzschluss gegen UBatt |
| 0x66 | Anlasserfreigabe Kurzschluss gegen Masse |
| 0x67 | Anlasserfreigabe Leitungsunterbrechung |
| 0x68 | Hydraulikpumpenrelais Kurzschluss gegen UBatt |
| 0x69 | Hydraulikpumpenrelais Kurzschluss gegen Masse |
| 0x6A | Hydraulikpumpenrelais Leitungsunterbrechung |
| 0x6B | PWM Ausgang Ansteuerung Waehlhebel LED R Symptomspezifisch |
| 0x6E | PWM Ausgang Ansteuerung Wahlhebel LED N Symptomspezifisch |
| 0x71 | PWM Ausgang Ansteuerung Wahlhebel LED S/D Symptomspezifisch |
| 0x74 | Getriebeventil DRV1 Kurzschluss gegen UBatt |
| 0x75 | Getriebeventil DRV1 Kurzschluss gegen Masse |
| 0x76 | Getriebeventil DRV1 Leitungsunterbrechung |
| 0x77 | Getriebeventil DRV1 unplausibles Signal |
| 0x78 | Getriebeventil DRV2 Kurzschluss gegen UBatt |
| 0x79 | Getriebeventil DRV2 Kurzschluss gegen Masse |
| 0x7A | Getriebeventil DRV2 Leitungsunterbrechung |
| 0x7B | Getriebeventil DRV2 unplausibles Signal |
| 0x7C | Getriebeventil PWV1 Kurzschluss gegen UBatt |
| 0x7D | Getriebeventil PWV1 Kurzschluss gegen Masse |
| 0x7E | Getriebeventil PWV1 Leitungsunterbrechung |
| 0x7F | Getriebeventil PWV1 unplausibles Signal |
| 0x80 | Getriebeventil PWV2 Kurzschluss gegen UBatt |
| 0x81 | Getriebeventil PWV2 Kurzschluss gegen Masse |
| 0x82 | Getriebeventil PWV2 Leitungsunterbrechung |
| 0x83 | Getriebeventil PWV2 unplausibles Signal |
| 0x84 | Getriebeventil PWV3 Kurzschluss gegen UBatt |
| 0x85 | Getriebeventil PWV3 Kurzschluss gegen Masse |
| 0x86 | Getriebeventil PWV3 Leitungsunterbrechung |
| 0x87 | Getriebeventil PWV3 unplausibles Signal |
| 0x88 | Getriebeventil PWV4 Kurzschluss gegen UBatt |
| 0x89 | Getriebeventil PWV4 Kurzschluss gegen Masse |
| 0x8A | Getriebeventil PWV4 Leitungsunterbrechung |
| 0x8B | Getriebeventil PWV4 unplausibles Signal |
| 0x8C | Kupplungsventil Kurzschluss gegen UBatt |
| 0x8D | Kupplungsventil Kurzschluss gegen Masse |
| 0x8E | Kupplungsventil Leitungsunterbrechung |
| 0x8F | Kupplungsventil unplausibles Signal |
| 0x90 | Spannungsversorgung Magnetventile PWV1, PWV3 und PWV4 Kurzschluss gegen Masse |
| 0x91 | Spannungsversorgung Magnetventile DRV1und DRV2 Kurzschluss gegen Masse |
| 0x92 | Spannungsversorgung Magnetventile PWV2 und Kupplungsventil Kurzschluss gegen Masse |
| 0x93 | Fahrlicht Timeout |
| 0x94 | Raddrücke Timeout |
| 0x95 | Außentemperatur Relativzeit Timeout |
| 0x96 | Bedienung Getriebewahlschalter Fehler Alivezaehler |
| 0x97 | Bedienung Getriebewahlschalter Timeout |
| 0x98 | Geschwindigkeit Fehler Alivezaehler |
| 0x99 | Geschwindigkeit Timeout |
| 0x9A | Geschwindigkeit Fehler Checksumme |
| 0x9B | Kilometerstand Istwert / Reichweite Timeout |
| 0x9C | Klemmenstatus Fehler Alivezaehler |
| 0x9D | Klemmenstatus Timeout |
| 0x9E | Klemmenstatus Fehler Checksumme |
| 0x9F | Lenkradwinkel Timeout |
| 0xA0 | Radgeschwindigkeit Timeout |
| 0xA1 | Radtoleranzabgleich Timeout |
| 0xA2 | Anhaenger Timeout |
| 0xA3 | DSC Fehler Alivezaehler |
| 0xA4 | DSC Timeout |
| 0xA5 | DSC Fehler Checksumme |
| 0xA6 | Kombi Fehler Alivezaehler |
| 0xA7 | Kombi Timeout |
| 0xA8 | Kombi Fehler Checksumme |
| 0xA9 | ZV Klappenzustand Timeout |
| 0xAA | Checkcontrol Meldungen Timeout |
| 0xAB | Anzeige Getriebedaten Timeout |
| 0xAC | Drehmomentanforderung EGS Timeout |
| 0xAD | Verzoegerungsanforderung ACC Timeout |
| 0xAE | Getriebedaten Timeout |
| 0xAF | Rohdaten Laengsbeschleunigung Timeout |
| 0xB0 | CAN Ueberwachung PT CAN Bus Off |
| 0xB1 | DME 1 Fehler Alivezaehler |
| 0xB2 | DME 1 Timeout |
| 0xB3 | DME 1 Fehler Checksumme |
| 0xB4 | DME 2 Fehler Alivezaehler |
| 0xB5 | DME 2 Timeout |
| 0xB6 | DME 2 Fehler Checksumme |
| 0xB7 | DME 3 Fehler Alivezaehler |
| 0xB8 | DME 3 Timeout |
| 0xB9 | DME 3 Fehler Checksumme |
| 0xBA | Drehmoment 1 Fehler Alivezaehler |
| 0xBB | Drehmoment 1 Timeout |
| 0xBC | Drehmoment 1 Fehler Checksumme |
| 0xBD | Drehmoment 3 Fehler Alivezaehler |
| 0xBE | Drehmoment 3 Timeout |
| 0xBF | Drehmoment 3 Fehler Checksumme |
| 0xC0 | Motordaten Fehler Alivezaehler |
| 0xC1 | Motordaten Timeout |
| 0xC2 | M-Drive Fehler Alivezaehler |
| 0xC3 | M-Drive Timeout |
| 0xC4 | M-Drive Fehler Checksumme |
| 0xC5 | SMG 1 Timeout |
| 0xC6 | SMG 2 Timeout |
| 0xC7 | SMG 3 Timeout |
| 0xC8 | CAN Ueberwachung SMG CAN Bus Off |
| 0xC9 | Sicherheitskonzept Ebene 2 Getriebe fehlerortspezifisch |
| 0xCA | Sicherheitskonzept Ebene 2 RAM fehlerortspezifisch |
| 0xCB | Sicherheitskonzept Ebene 2 Input fehlerortspezifisch |
| 0xCC | Sicherheitskonzept Ebene 2 Kupplung fehlerortspezifisch |
| 0xCD | Sicherheitskonzept Ebene 3 fehlerortspezifisch |
| 0xCE | NVRAM Laden unplausibel |
| 0xCF | Steuergeraet intern Auswertung ESTATE unplausibler Wert |
| 0xD0 | Steuergeraet intern Adaptionswerte Getriebe fehlerhafte Checksumme |
| 0xD1 | Hydraulikeinheit Druckbandunterschreitung Wert unterhalb Schwelle |
| 0xD2 | Hydraulikeinheit Druckbandüberschreitung Wert oberhalb Schwelle |
| 0xD3 | Einschalthaeufigkeit HE Motor oberhalb Schwelle |
| 0xD4 | Hydraulikeinheit Einschaltdauer Wert oberhalb Schwelle |
| 0xD5 | Hydraulikeinheit Missbrauch Wert oberhalb Schwelle |
| 0xD6 | Getriebeadaption unplausibler Wert |
| 0xD7 | Offsetadaption Laengsbeschleunigungssensor unplausibler Wert |
| 0xD8 | Kupplungsschleifpunkt Einlern- und Ansteuerfunktion unplausibler Wert |
| 0xD9 | Entlueftung unplausibler Wert |
| 0xDA | Aktionsmodi unplausibler Wert |
| 0xDB | Energiesparmodi Fertigung aktiv |
| 0xDC | Energiesparmodi Transport aktiv |
| 0xDD | Energiesparmodi Werkstatt aktiv |
| 0xDE | Eines oder mehrere der Getriebeadaptionsprogramme wurden nicht durchgefuehrt |
| 0xDF | Eines oder mehrere der Kupplungsadaptionsprogramme wurden nicht durchgefuehrt |
| 0xF0 | Getriebeproblem: Gang nicht auslegbar |
| 0xF1 | Getriebeproblem: Gang nicht einlegbar |
| 0xF2 | Getriebeproblem: Gangspringer |
| 0xF3 | Getriebeproblem: Drehzahlpruefung |
| 0xF4 | Kupplung Ansteuerung: Statische Soll - Ist Abweichung der Kupplung |
| 0xF5 | Kupplungsueberlastung |
| 0xF6 | Kurzschluss gegen Ubatt |
| 0xF7 | Kurzschluss gegen Masse |
| 0xF8 | Leitungsunterbrechung |
| 0xF9 | Hydraulikdrucksensor ausserhalb Messbereich |
| 0xFA | Hydraulikpumpenrelais klebender Relaiskontakt |
| 0xFB | Druckaufbaugeschwindigkeit unterhalb Schwelle |
| 0xFC | Hydraulikeinheit Baugruppe Leckage |
| 0xFD | R/1 (Hauptsensor) Trägerfrequenz PWM ausserhalb Bereich |
| 0xFE | R/1 (redundanter Sensor)  Trägerfrequenz PWM ausserhalb Bereich |
| 0xFF | 5/3 Trägerfrequenz PWM ausserhalb Bereich |
| 0x0100 | 2/4 Trägerfrequenz PWM ausserhalb Bereich |
| 0x0101 | 6/7 Trägerfrequenz PWM ausserhalb Bereich |
| 0x0102 | Steuergeraet intern Adaptionswerte Getriebe fehlerhafte Stromwerte |
| 0x0103 | Steuergeraet intern Adaptionswerte Getriebe fehlerhafte Positionswerte |
| 0x0104 | Sensor R/1 zu redundantem Signal unplausibel |
| 0x0105 | Uebersetzungsverhältnis beim Synchronisieren unplausibel |
| 0x0106 | Kupplungspositionsgeber (Hauptsensor) Massebruch Sensorversorgung |
| 0x0107 | Kupplungspositionsgeber (redundanter Sensor) Massebruch Sensorversorgung |
| 0x0108 | Kupplung Ansteuerung: Beide Sensoren fehlerhaft |
| 0x0109 | Kupplung Ansteuerung: Summenspannung unplausibel |
| 0x010A | Fehler Checksumme |
| 0x010B | Kupplungsschleifpunkt: Einlern- und Ansteuerfunktion fehlerhaft |
| 0xFFFF | Fehlersymptom nicht definiert |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fumwelttexte1"></a>
### FUMWELTTEXTE1

Dimensions: 10 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Neutral |
| 0x01 | 1.Gang |
| 0x02 | 2.Gang |
| 0x03 | 3.Gang |
| 0x04 | 4.Gang |
| 0x05 | 5.Gang |
| 0x06 | 6.Gang |
| 0x07 | 7.Gang |
| 0x08 | Rueckwaertsgang |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte2"></a>
### FUMWELTTEXTE2

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | vorwaerts |
| 0x02 | neutral |
| 0x03 | rueckwaerts |
| 0xFF | ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte3"></a>
### FUMWELTTEXTE3

Dimensions: 12 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | geschaltet |
| 0x01 | aktiv |
| 0x02 | Zwischenkuppeln |
| 0x03 | Synchronisation |
| 0x04 | Schaltweg Neutral |
| 0x05 | Waehlwinkel einregeln |
| 0x06 | Vorspannen |
| 0x07 | Waehlwinkel ablegen aus |
| 0x08 | Getriebe init aktiv |
| 0x09 | Synchronisation fertig |
| 0x0A | vor Synchronisation |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte4"></a>
### FUMWELTTEXTE4

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | offen |
| 0x01 | geschlossen |
| 0x02 | oeffnet |
| 0x03 | schliesst |
| 0x04 | Zwischenkuppeln aktiv |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte5"></a>
### FUMWELTTEXTE5

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Waehlhebel in P (Parken) |
| 0x02 | Waehlhebel in R (Rueckwaerts) |
| 0x03 | Waehlhebel in N (Neutral) |
| 0x04 | Waehlhebel in A (Automatik) |
| 0x05 | Waehlhebel in S (Sequentiell) |
| 0x06 | Waehlhebel in + (Gang hoch) |
| 0x07 | Waehlhebel in - (Gang runter) |
| 0xFF | Waehlhebelposition nicht definiert |

<a id="table-fumwelttexte6"></a>
### FUMWELTTEXTE6

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Bremse nicht betaetigt |
| 0x01 | nur Bremslichtschalter geschaltet |
| 0x02 | nur Bremslichttestschalter geschaltet |
| 0x03 | Bremslicht- und -test-schalter |
| 0x07 | Signal unguelitg |
| 0xFF | nicht definiert |

<a id="table-fumwelttexte16"></a>
### FUMWELTTEXTE16

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Anhaenger vorhanden |
| 0x01 | Anhaenger vorhanden |
| 0x03 | Signal ungueltig |
| 0xFF | nicht definiert |

<a id="table-fumwelttexte17"></a>
### FUMWELTTEXTE17

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Fahrzeug steht |
| 0x01 | Fahrzeug faehrt vorwaerts |
| 0x02 | Fahrzeug faehrt rueckwaerts |
| 0x03 | Fahrzeug faehrt (Richtungserkennung nicht moeglich) |
| 0xFF | nicht definiert |

<a id="table-fumwelttexte18"></a>
### FUMWELTTEXTE18

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | inaktiv |
| 0x01 | aktiv |
| 0x03 | Signal ungueltig |
| 0xFF | nicht definiert |

<a id="table-fumwelttexte19"></a>
### FUMWELTTEXTE19

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Fussbremse und Handbremse wurde nicht betaetigt |
| 0x01 | Fussbremse betaetigt |
| 0x02 | Handbremse betaetigt |
| 0x03 | Fussbremse und Handbremse betaetigt |
| 0xFF | nicht definiert |

<a id="table-fumwelttexte20"></a>
### FUMWELTTEXTE20

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Unbelastet |
| 0x01 | Leichte Belastung |
| 0x02 | Mittlere Belastung |
| 0x03 | Hohe Belastung |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte21"></a>
### FUMWELTTEXTE21

Dimensions: 13 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Schluesselnummer 0 |
| 0x01 | Schluesselnummer 1 |
| 0x02 | Schluesselnummer 2 |
| 0x03 | Schluesselnummer 3 |
| 0x04 | Schluesselnummer 4 |
| 0x05 | Schluesselnummer 5 |
| 0x06 | Schluesselnummer 6 |
| 0x07 | Schluesselnummer 7 |
| 0x08 | Schluesselnummer 8 |
| 0x09 | Schluesselnummer 9 |
| 0x0E | Nachlaufschluessel |
| 0x0F | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte22"></a>
### FUMWELTTEXTE22

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Keine Regelung |
| 0x01 | ABS Regelung |
| 0x02 | ASC Regelung |
| 0x04 | DSC Regelung |
| 0x08 | HBA Regelung |
| 0x10 | MSR Regelung |
| 0x20 | EBV Regelung |
| 0x80 | ASC DSC ausgeschaltet |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte23"></a>
### FUMWELTTEXTE23

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Warm up cycle |
| 0x02 | Aktivbedingung fuer Berechnung Drivingcycle in EGS/SMG |
| 0x04 | Freeze Frame verwaltet fuer Master |
| 0x08 | Freeze Frame verwaltet fuer EGS |
| 0x10 | Freeze Frame verwaltet fuer EKP |
| 0x14 | Freeze Frame verwaltet fuer DME links |
| 0xFF | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte24"></a>
### FUMWELTTEXTE24

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | In Ordnung |
| 0x01 | Plausibiltaets-/Aktivitaetsfehler |
| 0x02 | Timeoutfehler |
| 0x03 | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte25"></a>
### FUMWELTTEXTE25

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Keine Anforderung |
| 0x01 | Konstantfahrt |
| 0x02 | Wiederaufnahme |
| 0x04 | Tempomat Setze Beschleunigung |
| 0x08 | Tempomat Setze Verzoegern |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte26"></a>
### FUMWELTTEXTE26

Dimensions: 10 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Keine Anforderung |
| 0x01 | Anforderung ACC akzeptiert |
| 0x02 | Anforderung EMF akzeptiert |
| 0x03 | Anforderung HBA akzeptiert |
| 0x04 | Anforderung ACC umgesetzt |
| 0x05 | Anforderung ACC umgesetzt und Rueckschaltaufforderung ACC (nicht SMG) |
| 0x06 | Anforderung ACC umgesetzt und Rueckschaltaufforderung ACC (nicht SMG) & Schleppmomentunterstuetzung |
| 0x0E | Keine Anforderung umgesetzt |
| 0x0F | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte27"></a>
### FUMWELTTEXTE27

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Motor im Warmlauf |
| 0x01 | Motor betriebswarm |
| 0x02 | Motor Uebertemperatur |
| 0x03 | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte28"></a>
### FUMWELTTEXTE28

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Zuendung aus |
| 0x01 | Radio Ein-Stellung |
| 0x02 | Fahrtstellung |
| 0x03 | Anlassen |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte29"></a>
### FUMWELTTEXTE29

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Fehler vorhanden |
| 0x01 | Fehler |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte30"></a>
### FUMWELTTEXTE30

Dimensions: 17 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0001 | Handbremssignal |
| 0x0002 | frei |
| 0x0004 | Waehlhebelschalter S1 |
| 0x0008 | Waehlhebelschalter S2 |
| 0x0010 | Waehlhebelschalter E1 |
| 0x0020 | Waehlhebelschalter E2 |
| 0x0040 | Waehlhebelschalter N1 |
| 0x0080 | Waehlhebelschalter N2 |
| 0x0100 | Waehlhebelschalter R1 |
| 0x0200 | Waehlhebelschalter R2 |
| 0x0400 | ESTATE |
| 0x0800 | Programmwahlschalter PLUS |
| 0x1000 | Programmwahlschalter MINUS |
| 0x2000 | frei |
| 0x4000 | Motorhaubenkontakt 2 |
| 0x8000 | Motorhaubenkontakt 1 |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte31"></a>
### FUMWELTTEXTE31

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Fehler vorhanden |
| 0x01 | Bus Off local CAN |
| 0x02 | Bus Off local PT CAN |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte32"></a>
### FUMWELTTEXTE32

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Fehler vorhanden |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Kurzschluss nach Ubatt |
| 0x04 | Leitungsunterbrechung |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte33"></a>
### FUMWELTTEXTE33

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Sensorsignal |
| 0x02 | CAN Signal |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte34"></a>
### FUMWELTTEXTE34

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Fehler vorhanden |
| 0x01 | Hauptsensor |
| 0x02 | Redundanter Sensor |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte35"></a>
### FUMWELTTEXTE35

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Bremsdruck |
| 0x01 | Bremsdruck vorhanden |
| 0x02 | Keine Aussage moeglich |
| 0x03 | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte36"></a>
### FUMWELTTEXTE36

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | In Ordnung |
| 0x01 | Passiv |
| 0x02 | Defekt |
| 0x03 | Reserviert |
| 0x04 | Traktionsmodus |
| 0x05 | Reserviert |
| 0x06 | Unterspannung DSC |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte37"></a>
### FUMWELTTEXTE37

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Klemme 15 AUS |
| 0x01 | Klemme 15 EIN |
| 0x03 | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte38"></a>
### FUMWELTTEXTE38

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Klemme 50 AUS |
| 0x01 | Klemme 50 EIN |
| 0x03 | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte39"></a>
### FUMWELTTEXTE39

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Klemme R AUS |
| 0x01 | Klemme R EIN |
| 0x03 | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte40"></a>
### FUMWELTTEXTE40

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | In Ordnung |
| 0x01 | Kein LWS-Signal verfuegbar |
| 0x02 | LWS-Signal fehlerhaft |
| 0x03 | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte41"></a>
### FUMWELTTEXTE41

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Eingriffswunsch wird ausgefuehrt |
| 0x01 | Eingriffswunsch wird nicht vollstaendig ausgefuehrt |
| 0x02 | Eingriffswunsch wird nicht vollstaendig ausgefuehrt |
| 0x03 | Eingriffswunsch wird nicht vollstaendig ausgefuehrt |
| 0x0F | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte42"></a>
### FUMWELTTEXTE42

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Schluessel erkannt |
| 0x01 | Gueltiger Schluessel erkannt |
| 0x02 | Ungueltiger Schluessel erkannt |
| 0x03 | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte43"></a>
### FUMWELTTEXTE43

Dimensions: 12 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | ACC-Regelung PWG nicht getreten |
| 0x01 | ACC-Regelung PWG getreten |
| 0x04 | FGR-Regelung Verzoegern |
| 0x05 | FGR-Regelung Konstantfahrt |
| 0x06 | FGR-Regelung Wiederaufnahme |
| 0x07 | FGR-Regelung Beschleunigen |
| 0x08 | Keine ACC-Regelung PWG nicht getreten |
| 0x09 | Keine ACC-Regelung PWG getreten |
| 0x0A | ACC-Regelung PWG uebertreten |
| 0x0B | PWG Kickdown |
| 0x0F | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte44"></a>
### FUMWELTTEXTE44

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Unerlaubtes Anfahren |
| 0x02 | Unerlaubtes Oeffnen der Kupplung |
| 0x03 | Zu schnelles Schliessen der Kupplung nach Radabriss |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte45"></a>
### FUMWELTTEXTE45

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Fahrertuer ist geschlossen |
| 0x01 | Fahrertuer ist offen |
| 0x02 | Signal unplausibel |
| 0x03 | ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte46"></a>
### FUMWELTTEXTE46

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Bremskontakte identisch |
| 0x01 | Bremskontakte unterschiedlich |
| 0x02 | Verzoegerung aber kein Bremssignal |
| 0x04 | Beschleunigung aber Bremssignal |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte47"></a>
### FUMWELTTEXTE47

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Motordrehzahl CAN in Ordnung |
| 0x01 | Drehzahlgeber defekt |
| 0x02 | Reserve |
| 0x03 | Signal ungueltig |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte48"></a>
### FUMWELTTEXTE48

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Initialisierung laeuft |
| 0x01 | Initialisierung ist beendet |
| 0xXY | nicht definiert |

<a id="table-stellglieder"></a>
### STELLGLIEDER

Dimensions: 19 rows × 5 columns

| STELLGLIED | STEUERART1 | STEUERART2 | PIN | PIN_INK |
| --- | --- | --- | --- | --- |
| MAGNETVENTIL_KUPPLUNG | STROMVORGABE, POSITIONSVORGABE | 0-3000, 0-1023 | 0x67 | 0x7B |
| MAGNETVENTIL_R_1 | STROMVORGABE, POSITIONSVORGABE | 0-3000, 0-1023 | 0x68 | 0x77 |
| MAGNETVENTIL_5_3 | STROMVORGABE, POSITIONSVORGABE | 0-3000, 0-1023 | 0x69 | 0x78 |
| MAGNETVENTIL_2_4 | STROMVORGABE, POSITIONSVORGABE | 0-3000, 0-1023 | 0x6A | 0x79 |
| MAGNETVENTIL_6_7 | STROMVORGABE, POSITIONSVORGABE | 0-3000, 0-1023 | 0x6B | 0x7A |
| MAGNETVENTIL_DRV_1 | STROMVORGABE | 0-3000 | 0x6C | 0x00 |
| MAGNETVENTIL_DRV_2 | STROMVORGABE | 0-3000 | 0x6D | 0x00 |
| ANLASSER_FREIGABE | AKTIV, INAKTIV |  | 0x22 | 0x00 |
| HYDROPUMPE | AKTIV, INAKTIV |  | 0x23 | 0x00 |
| SHIFTLOCK | AKTIV, INAKTIV |  | 0x20 | 0x00 |
| WAEHLHEBEL_ANZEIGE | AKTIV, INAKTIV | AUS, N, R, D | 0x81 | 0x00 |
| GANG_ANZEIGE | AKTIV, INAKTIV | 0-7=Gang, 8=Rueckwaertsgang, 9=Anzeige dunkel | 0x82 | 0x00 |
| KOMBIANZEIGE_KOMFORTINDEX | AKTIV, INAKTIV | 1-6 | 0x80 | 0x00 |
| WAEHLHEBEL_LED_DS | AKTIV, INAKTIV |  | 0x21 | 0x00 |
| WAEHLHEBEL_LED_R | AKTIV, INAKTIV |  | 0x24 | 0x00 |
| WAEHLHEBEL_LED_N | AKTIV, INAKTIV |  | 0x25 | 0x00 |
| STOERANZEIGE_ROT | AKTIV, INAKTIV |  | 0x83 | 0x00 |
| GETRIEBEOELPUMPE | AKTIV, INAKTIV |  | 0x84 | 0x00 |
| RUECKGABE_AN_SG |  |  | 0xFE | 0x00 |

<a id="table-testprg"></a>
### TESTPRG

Dimensions: 13 rows × 4 columns

| TESTPRG_NR | TESTPRG_NAME | DAUER TYP. | DAUER MAX. |
| --- | --- | --- | --- |
| 0x20 | Speichervorspanndruck ermitteln | ? sek | ? sek |
| 0x21 | Beliebigen Gang einlegen |  |  |
| 0x22 | Schaltwegmittellage positionieren |  |  |
| 0x23 | Startbedingungen fuer Motor herstellen |  |  |
| 0x30 | Entlueftung Kuppl.-Nehmerzyl./Hydraulikleit. | ? min | ? min |
| 0x31 | Entlueftung Getriebeakuator | ? min | ? min |
| 0x32 | Kupplungsventilkennwerte einlernen | 89 sek | 180 sek |
| 0x33 | Kupplungsschleifpunkt einlernen | 5,6 sek | 30 sek |
| 0x34 | Offsetstroeme PWV einlernen | ? sek | ? sek |
| 0x35 | Hydraulikdruck abbauen |  |  |
| 0x36 | Getriebe komplett einlernen | 43 sek | 88 sek |
| 0x37 | Offset Laengsbeschleunigungssensor einlernen | 5,6 sek | 20 sek |
| 0x38 | Adaptionswerte in NVRAM speichern | ? sek | ? sek |

<a id="table-stattesttexte"></a>
### STATTESTTEXTE

Dimensions: 6 rows × 2 columns

| STB | TEST_STATUS_TEXT |
| --- | --- |
| 0x00 | Testbedingung nicht erfuellt |
| 0x01 | Testprogramm laeuft |
| 0x02 | Testprogramm beendet |
| 0x03 | Testprogramm nicht ordnungsgemaess beendet |
| 0x04 | Testprogramm durch Bediener abgebrochen |
| 0xFF | Unbekannter Status |

<a id="table-infotexte0x20a"></a>
### INFOTEXTE0X20A

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm Initialisierung |
| 0x14 | Speicher befuellen |
| 0x16 | Speicher leeren |
| 0x18 | Vorspanndruckermittlung beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x20f"></a>
### INFOTEXTE0X20F

Dimensions: 7 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x0A | Vorspanndruckermittlung nicht durchfuehrbar, aufgrund HE relevanter FS-Eintraege |
| 0x0B | HE-Temperatur bei Vorspanndruckermittlung ausserhalb der zulaessigen Grenzen |
| 0x0C | Druckaufbau in der vorgeschriebenen Zeit nicht Mindestdruckschwelle ueberschritten |
| 0x0D | Druckabbau in der vorgeschriebenen Zeit nicht erreicht |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x21a"></a>
### INFOTEXTE0X21A

Dimensions: 6 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x3D | Initialisierung der Funktion |
| 0x3E | Gewuenschten Gang als Zielgang setzen |
| 0x3F | Zeit zum Gangeinlegen abwarten |
| 0x40 | Beliebigen Gang einlegen ist beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x21f"></a>
### INFOTEXTE0X21F

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x50 | Das Einlegen des gewuenschten Ganges ist gescheitert |
| 0x51 | Ungueltige Gangvorgabe |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x22a"></a>
### INFOTEXTE0X22A

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x01 | Kupplung oeffnen |
| 0x28 | Schaltwegmittellage einregeln |
| 0x29 | Schaltwegmittellage einlegen beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x22f"></a>
### INFOTEXTE0X22F

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Der Ablauf des Automatismus ist nicht korrekt |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x23a"></a>
### INFOTEXTE0X23A

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm Initialisierung und Pruefung der Eintrittsbedingungen |
| 0x01 | Ermittlung Ventilkennwerte |
| 0x7F | Adaption Kupplungskennwerte beendet, Startbedingung fuer Motor hergestellt |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x23f"></a>
### INFOTEXTE0X23F

Dimensions: 8 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x81 | Einkuppelposition ausserhalb der zulaessigen Toleranz |
| 0x82 | Auskuppelposition ausserhalb der zulaessigen Toleranz |
| 0x83 | Kupplungsventil-Nullstrom ausserhalb der zulaessigen Toleranz |
| 0x84 | Zeitueberschreitung bei Ermittlung der Ventilueberdeckung |
| 0x85 | Ventilueberdeckung ausserhalb der zulaessigen Toleranz |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x30a"></a>
### INFOTEXTE0X30A

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm Initialisierung |
| 0x01 | Kupplungsentlueftung |
| 0x7F | Entlueftung beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x30f"></a>
### INFOTEXTE0X30F

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Nehmerzylinder-Mindesthub nicht erreicht |
| 0x7F | Abbruch durch Benutzer |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft, oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x31a"></a>
### INFOTEXTE0X31A

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x1B | Initialisierung |
| 0x1C | Durchfuehrung Entlueftung des Stellerblocks |
| 0x1D | Entlueftung beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x31f"></a>
### INFOTEXTE0X31F

Dimensions: 8 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x10 | Vorspanndruckermittlung nicht durchfuehrbar, aufgrund HE relevanter FS-Eintraege |
| 0x11 | Druckaufbau im Pumpenblock in vorgegebener Zeit nicht erreicht |
| 0x12 | Druckabbau im Pumpenblock in vorgegebener Zeit nicht erreicht |
| 0x13 | Druckaufbau im Stellerblock in vorgegebener Zeit nicht erreicht |
| 0x14 | Druckabbau im Stellerblock in vorgegebener Zeit nicht erreicht |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x32a"></a>
### INFOTEXTE0X32A

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm Initialisierung und Pruefung der Eintrittsbedingungen |
| 0x01 | Ermittlung Ventilkennwerte |
| 0x02 | Ermittlung Kupplungs-Lagereglerverstaerkung |
| 0x7F | Adaption Kupplungskennwerte beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x32f"></a>
### INFOTEXTE0X32F

Dimensions: 9 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler erkannt |
| 0x7F | Abbruch durch Benutzer |
| 0x81 | Einkuppelposition ausserhalb der zulaessigen Toleranz |
| 0x82 | Auskuppelposition ausserhalb der zulaessigen Toleranz |
| 0x83 | Kupplungsventil-Nullstrom ausserhalb der zulaessigen Toleranz |
| 0x84 | Zeitueberschreitung bei Ermittlung der Ventilueberdeckung |
| 0x85 | Ventilueberdeckung ausserhalb der zulaessigen Toleranz |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x33a"></a>
### INFOTEXTE0X33A

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm Initialisierung und Pruefung der Eintrittsbedingungen |
| 0x01 | Adaption Kupplungsschleifpunkt |
| 0x7F | Schleifpunktadaption beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x33f"></a>
### INFOTEXTE0X33F

Dimensions: 9 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler erkannt |
| 0x24 | Getriebedrehzahl beim Anfahren des Einlernbereichs oder Schleifpunkt zu niedrig |
| 0x25 | Keine Getriebedrehzahl bei geschlossener Kupplung oder Schleifpunkt zu hoch |
| 0x26 | Keine Getriebedrehzahl bei geschlossener Kupplung |
| 0x27 | Interner Ablauffehler |
| 0x28 | Getriebedrehzahl nach Kupplungsoeffnen nicht in der geforderten Zeit auf Null |
| 0x7F | Abbruch durch Benutzer |
| 0xA0 | Testbedingung nicht erfuellt (Motor ist aus, N nicht eingelegt, Eingangsdrehz. &lt;&gt; 0, Gaspedal betaetigt) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x34a"></a>
### INFOTEXTE0X34A

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x01 | Kupplung oeffnen |
| 0x28 | Schaltwegmittellage einregeln |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x34f"></a>
### INFOTEXTE0X34F

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Der Ablauf des Automatismus ist nicht korrekt |
| 0x46 | Die Schaltwegmittellage laesst sich nicht einregeln |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x35a"></a>
### INFOTEXTE0X35A

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x18 | Initialisierung |
| 0x19 | Hydraulikdruck abbauen |
| 0x1A | Druckabbau beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x35f"></a>
### INFOTEXTE0X35F

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x0E | Vorspanndruckermittlung nicht durchfuehrbar, aufgrund HE relevanter FS-Eintraege |
| 0x0F | Druckabbau in der vorgeschriebenen Zeit nicht erreicht |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x36a"></a>
### INFOTEXTE0X36A

Dimensions: 19 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x01 | Kupplung oeffnen |
| 0x02 | PWV Offsetstromadaption |
| 0x03 | Gang 1 ausmessen |
| 0x04 | Gang 2 ausmessen |
| 0x05 | Gang 3 ausmessen |
| 0x06 | Gang 4 ausmessen |
| 0x07 | Gang 5 ausmessen |
| 0x08 | Gang 6 ausmessen |
| 0x09 | Gang 7 ausmessen |
| 0x0A | Gang R ausmessen |
| 0x0B | Neutralstellung einnehmen |
| 0x0C | Einlernwerte in NVRAM schreiben |
| 0x0D | Einlegehaenger nachbearbeiten |
| 0x0E | Getriebeparameter verarbeiten |
| 0x0F | Getriebe einlernen beendet |
| 0x28 | Schaltwegmittellage einregeln |
| 0x29 | Schaltwegmittellage einlegen beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x36f"></a>
### INFOTEXTE0X36F

Dimensions: 36 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Der Ablauf des Automatismus ist nicht korrekt |
| 0x02 | Max. zulaessige Zeit fuer Adaption wurde ueberschritten |
| 0x28 | Die Zeit zum Einregeln der Schaltwegmitten ist ueberschritten |
| 0x29 | Der Hydraulikdruck ist zu gering |
| 0x2A | Einlegehaenger erkannt |
| 0x2B | Einlegehaenger in Gang 1 vorhanden / Werte wurden substituiert |
| 0x2C | Einlegehaenger in Gang 2 vorhanden / Werte wurden substituiert |
| 0x2D | Einlegehaenger in Gang 3 vorhanden / Werte wurden substituiert |
| 0x2E | Einlegehaenger in Gang 4 vorhanden / Werte wurden substituiert |
| 0x2F | Einlegehaenger in Gang 5 vorhanden / Werte wurden substituiert |
| 0x30 | Einlegehaenger in Gang 6 vorhanden / Werte wurden substituiert |
| 0x31 | Einlegehaenger in Gang 7 vorhanden / Werte wurden substituiert |
| 0x32 | Einlegehaenger in Rueckwaertsgang vorhanden / Werte wurden substituiert |
| 0x33 | Der Schaltweg rueckt in der Gasse nach Wegnahme der Kraft zu weit aus |
| 0x34 | Redundanter Positionsensor Zylinder R/1 ist defekt |
| 0x35 | Positionsensor Zylinder R/1 ist defekt |
| 0x36 | Positionsensor Zylinder 5/3 ist defekt |
| 0x37 | Positionsensor Zylinder 2/4 ist defekt |
| 0x38 | Positionsensor Zylinder 6/7 ist defekt |
| 0x39 | Bei der Adaption eines Ganges rueckt eine weitere Schaltstange ein |
| 0x3A | Eingelegte Position konnte bei der Schaltkraftmessung nicht erreicht werden |
| 0x3B | Min. Grenzwert Gangposition Gang 1 nicht erreicht |
| 0x3C | Min. Grenzwert Gangposition Gang 2 nicht erreicht |
| 0x3D | Min. Grenzwert Gangposition Gang 3 nicht erreicht |
| 0x3E | Min. Grenzwert Gangposition Gang 4 nicht erreicht |
| 0x3F | Min. Grenzwert Gangposition Gang 5 nicht erreicht |
| 0x40 | Min. Grenzwert Gangposition Gang 6 nicht erreicht |
| 0x41 | Min. Grenzwert Gangposition Gang 7 nicht erreicht |
| 0x42 | Min. Grenzwert Gangposition Gang R nicht erreicht |
| 0x46 | Die Schaltwegmitten lassen sich nicht einregeln Schaltstange R/1 |
| 0x47 | Die Schaltwegmitten lassen sich nicht einregeln Schaltstange 5/3 |
| 0x48 | Die Schaltwegmitten lassen sich nicht einregeln Schaltstange 2/4 |
| 0x49 | Die Schaltwegmitten lassen sich nicht einregeln Schaltstange 6/7 |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Fuss betaetigt) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x37a"></a>
### INFOTEXTE0X37A

Dimensions: 8 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x46 | Initialisierung |
| 0x47 | Ersten Wert ermitteln |
| 0x48 | Zeit zwischen zwei Werten abwarten |
| 0x49 | Folgewerte mit 1. Wert vergleichen |
| 0x4A | Offset berechnen |
| 0x4B | Offsetermittlung beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x37f"></a>
### INFOTEXTE0X37F

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x5A | Eingelernter Wert ausserhalb des fuer Laengsbeschleunigung zulaessigen Bereichs |
| 0x5B | Offset des Laengsbeschleunigungssensors in vorgesehener Zeit nicht erfolgreich eingelernt |
| 0xA0 | Testbedingung nicht erfuellt (Raddrehzahlen &lt;&gt; 0 ) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x38a"></a>
### INFOTEXTE0X38A

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Testprogramm noch nicht gestartet |
| 0x01 | Adaptionswerte sind noch nicht gespeichert, Vorgang laeuft |
| 0x02 | Adaptionswerte wurden gespeichert |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte0x38f"></a>
### INFOTEXTE0X38F

Dimensions: 3 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0xA0 | Testbedingung nicht erfuellt (N nicht eingelegt, Motordrehzahl &lt;&gt; 0) |
| 0xFF | Unbekannter Infotext |

<a id="table-motorhaubenkontakteroh"></a>
### MOTORHAUBENKONTAKTEROH

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x00B8 | 0x00B9 |

<a id="table-motorhaubenkontakteist"></a>
### MOTORHAUBENKONTAKTEIST

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x002D | 0x002E |

<a id="table-wahlhebelsignaleroh"></a>
### WAHLHEBELSIGNALEROH

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x00BA | 0x00BB | 0x00BC | 0x00BD | 0x00BE | 0x00BF | 0x00C0 | 0x00C1 |

<a id="table-wahlhebelsignaleist"></a>
### WAHLHEBELSIGNALEIST

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x002F | 0x0030 | 0x0031 | 0x0032 | 0x0033 | 0x0034 | 0x0035 | 0x0036 |

<a id="table-laengsbeschleunigung"></a>
### LAENGSBESCHLEUNIGUNG

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x00F0 | 0x0026 | 0x00E5 |

<a id="table-sensorspannung"></a>
### SENSORSPANNUNG

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x0046 | 0x00EB | 0x00EC |

<a id="table-getriebedrehzahl"></a>
### GETRIEBEDREHZAHL

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x0043 | 0x0044 |

<a id="table-kupplungsposition0x510d-e"></a>
### KUPPLUNGSPOSITION0X510D_E

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x00EB | 0x0086 | 0x0087 | 0x0043 | 0x0046 | 0x0049 | 0x0085 | 0x0088 |

<a id="table-radgeschwvorneistwert"></a>
### RADGESCHWVORNEISTWERT

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x0058 | 0x0059 |

<a id="table-laengsbeschl0x520c"></a>
### LAENGSBESCHL0X520C

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x00F0 | 0x0001 | 0x0026 | 0x0025 |

<a id="table-drehzahltemp10x5218"></a>
### DREHZAHLTEMP10X5218

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x006D | 0x0047 | 0x0046 | 0x0043 |

<a id="table-drehzahltemp20x5219"></a>
### DREHZAHLTEMP20X5219

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x006E | 0x0048 | 0x0047 | 0x0046 | 0x0043 |

<a id="table-begrenzerdrehzahl0x521a"></a>
### BEGRENZERDREHZAHL0X521A

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x0068 | 0x0042 | 0x0046 | 0x0043 |

<a id="table-getriebeventildrv10x5500"></a>
### GETRIEBEVENTILDRV10X5500

Dimensions: 1 rows × 11 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | 0x00F0 | 0x0017 | 0x001D | 0x001F | 0x0020 | 0x0049 | 0x0084 | 0x0082 | 0x007A | 0x0078 |

<a id="table-getriebeventildrv20x5501"></a>
### GETRIEBEVENTILDRV20X5501

Dimensions: 1 rows × 11 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | 0x00F0 | 0x0018 | 0x001E | 0x0021 | 0x0022 | 0x0049 | 0x0081 | 0x0083 | 0x0077 | 0x0079 |

<a id="table-getriebeventilr-10x5502"></a>
### GETRIEBEVENTILR_10X5502

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x00F0 | 0x0019 | 0x001F | 0x001D | 0x0049 | 0x0084 | 0x007A |

<a id="table-getriebeventil5-30x5503"></a>
### GETRIEBEVENTIL5_30X5503

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x00F0 | 0x001A | 0x0020 | 0x001D | 0x0049 | 0x0082 | 0x0078 |

<a id="table-getriebeventil6-70x5504"></a>
### GETRIEBEVENTIL6_70X5504

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x00F0 | 0x001B | 0x0021 | 0x001E | 0x0049 | 0x0081 | 0x0077 |

<a id="table-getriebeventil2-40x5505"></a>
### GETRIEBEVENTIL2_40X5505

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x00F0 | 0x001C | 0x0022 | 0x001E | 0x0049 | 0x0083 | 0x0079 |

<a id="table-kupplungsventil0x5506"></a>
### KUPPLUNGSVENTIL0X5506

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x00F0 | 0x0023 | 0x0024 | 0x0049 | 0x0088 | 0x0085 | 0x000A | 0x00A2 |

<a id="table-magnetventile0x5507"></a>
### MAGNETVENTILE0X5507

Dimensions: 1 rows × 11 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | 0x0019 | 0x001B | 0x001C | 0x001F | 0x0021 | 0x0022 | 0x007A | 0x0077 | 0x0079 | 0x0049 |

<a id="table-magnetventiledrv1-20x5508"></a>
### MAGNETVENTILEDRV1_20X5508

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x00F0 | 0x0017 | 0x0018 | 0x001D | 0x001E | 0x0014 | 0x0049 |

<a id="table-radgeschwcan0xcf07"></a>
### RADGESCHWCAN0XCF07

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x00E7 | 0x00E8 | 0x00EE | 0x00EF |

<a id="table-ebene2kupplung0x4f03"></a>
### EBENE2KUPPLUNG0X4F03

Dimensions: 1 rows × 10 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 9 | 0x0094 | 0x0095 | 0x0014 | 0x0093 | 0x0092 | 0x0088 | 0x0085 | 0x00DC | 0x00F3 |

<a id="table-ebene30x4f04"></a>
### EBENE30X4F04

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x008D | 0x0096 | 0x0097 | 0x0012 | 0x0011 |

<a id="table-hydraulik0x4f40bis42"></a>
### HYDRAULIK0X4F40BIS42

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x00F0 | 0x0023 | 0x0050 | 0x0051 | 0x00EA | 0x0046 |

<a id="table-kupplung0x4fa0-a1"></a>
### KUPPLUNG0X4FA0_A1

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x00F0 | 0x0023 | 0x0050 | 0x0046 | 0x00EA | 0x0085 | 0x0088 |

<a id="table-fgr"></a>
### FGR

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | FGR passiv |
| 0x01 | FGR aktiv, Konstantfahrt |
| 0x02 | ACC-Regelung Standard |
| 0x03 | FGR aktiv, Wiederaufnahme |
| 0x04 | ACC-Regelung erhoehte Dynamik |
| 0x05 | FGR aktiv, Setzen/Beschleunigen |
| 0x06 | FGR/ACC-Abschaltung |
| 0x07 | FGR aktiv, Verzoegern |
| 0xXY | nicht definiert |

<a id="table-freeze-frame-referenz"></a>
### FREEZE_FRAME_REFERENZ

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Freeze Frame gespeichert |
| 0x01 | Freeze Frame wird verwaltet fuer DME (Master) |
| 0x02 | Freeze Frame wird verwaltet fuer EGS od. SMG |
| 0x03 | Freeze Frame wird verwaltet fuer EML |
| 0x04 | Freeze Frame wird verwaltet fuer DME links |
| 0xXY | nicht definiert |

<a id="table-programminfo"></a>
### PROGRAMMINFO

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | 1. Programm |
| 0x02 | 2. Programm |
| 0x03 | 3. Programm |
| 0x04 | 4. Programm |
| 0x05 | 5. Programm |
| 0x06 | 6. Programm |
| 0xXY | nicht definiert |

<a id="table-komfortindex"></a>
### KOMFORTINDEX

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | komfortabel |
| 0x01 | komfortabel+1 |
| 0x02 | komfortabel+2 |
| 0x03 | komfortabel+3 |
| 0x04 | komfortabel+4 |
| 0x05 | komfortabel+5 |
| 0x06 | normal |
| 0x07 | sportiv-5 |
| 0x08 | sportiv-4 |
| 0x09 | sportiv-3 |
| 0x0A | sportiv-2 |
| 0x0B | sportiv-1 |
| 0x0C | sportiv |
| 0xXY | nicht definiert |

<a id="table-ganganzeige"></a>
### GANGANZEIGE

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Neutral |
| 0x01 | 1.Gang |
| 0x02 | 2.Gang |
| 0x03 | 3.Gang |
| 0x04 | 4.Gang |
| 0x05 | 5.Gang |
| 0x06 | 6.Gang |
| 0x07 | 7.Gang |
| 0x08 | Rueckwaertsgang |
| 0x09 | Anzeige dunkel |
| 0xFF | nicht definiert |

<a id="table-waehlhebelanzeige"></a>
### WAEHLHEBELANZEIGE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Anzeige dunkel |
| 0x02 | R |
| 0x04 | N |
| 0x08 | D |
| 0xFF | nicht definiert |

<a id="table-led"></a>
### LED

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine LED |
| 0x01 | 1. LED |
| 0x02 | 1. und 2. LED |
| 0xXY | nicht definiert |

<a id="table-infotextefahrzeugzustand"></a>
### INFOTEXTEFAHRZEUGZUSTAND

Dimensions: 48 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Systemfreigabe |
| 0x01 | Motor aus, Fahrzeug steht |
| 0x02 | Eingekuppelt |
| 0x03 | Abwuergen |
| 0x04 | Anhalten |
| 0x05 | Anschleppen |
| 0x06 | Abschalten |
| 0x07 | Antiblockiersystem |
| 0x08 | Antriebsschlupfregelung |
| 0x09 | Nebenabtrieb |
| 0x0A | Keine Druckluft |
| 0x0B | Starten |
| 0x0C | Abschalten ohne Systemfreigabe |
| 0x10 | Einkuppeln, Schub |
| 0x11 | Einkuppeln, Zug |
| 0x12 | Einkuppeln, Synchron |
| 0x13 | Einkuppeln, Ueberdrehzahl |
| 0x14 | Einkuppeln, Zug, Sport |
| 0x15 | Einkuppeln, Schub, Sport |
| 0x16 | Einkuppeln, Radabriss |
| 0x17 | Einkuppeln, Schub, Eingriff |
| 0x18 | Einkuppeln, Eingriff |
| 0x20 | Anfahren, Vorweg |
| 0x21 | Anfahren, Normal |
| 0x22 | Anfahren, Kick Down |
| 0x23 | Anfahren, Synchron |
| 0x24 | Anfahren, Rennstart |
| 0x25 | Anfahrhilfe |
| 0x26 | Rennstart vorbereiten |
| 0x27 | Anfahren, Moment |
| 0x30 | Schalten |
| 0x40 | Neutral ohne Einlernen, GW |
| 0x41 | Neutral Einlernen, GW |
| 0x42 | Neutral Einlernen GW beendet |
| 0x43 | Neutral, Fahrzeug steht |
| 0x50 | Verschalten, Zug Normal |
| 0x51 | Verschalten, Zug Extrem |
| 0x52 | Verschalten, Zug Synchron |
| 0x60 | Anrollen |
| 0x70 | Notfahr FP Kuppeln |
| 0x71 | Notfahr N Mot Kuppeln |
| 0x72 | System abschalten |
| 0x80 | Schlupf |
| 0x90 | Ansynchronisieren |
| 0x91 | Ansynchronisieren beendet |
| 0xA0 | KKL Einlernen |
| 0xA1 | KKL Einlernen beendet |
| 0xFF | Unbekannter Infotext |

<a id="table-ebene20x4f00bis02"></a>
### EBENE20X4F00BIS02

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x0094 | 0x008D | 0x0095 | 0x0014 | 0x0092 | 0x009B |

<a id="table-nvramladen0x4f20"></a>
### NVRAMLADEN0X4F20

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x0096 | 0x0097 | 0x0012 | 0x0011 | 0x0183 |

<a id="table-estate0x4f21"></a>
### ESTATE0X4F21

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x008D | 0x0095 | 0x0014 | 0x0092 | 0x009B | 0x009C | 0x0141 |

<a id="table-getriebeproblem0x4f80"></a>
### GETRIEBEPROBLEM0X4F80

Dimensions: 1 rows × 10 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 9 | 0x0050 | 0x007A | 0x0078 | 0x0077 | 0x0079 | 0x0084 | 0x0082 | 0x0081 | 0x0083 |

<a id="table-uebersetzungsp0x4f81"></a>
### UEBERSETZUNGSP0X4F81

Dimensions: 1 rows × 12 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 11 | 0x00F0 | 0x0014 | 0x0085 | 0x0043 | 0x0046 | 0x00E6 | 0x00F1 | 0x017E | 0x017F | 0x007F | 0x0080 |

<a id="table-wahlhebel0x5002"></a>
### WAHLHEBEL0X5002

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x00F0 | 0x00F1 |

<a id="table-fahrtrichtwahlhebel"></a>
### FAHRTRICHTWAHLHEBEL

Dimensions: 1 rows × 12 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 11 | 0x00F4 | 0x00F5 | 0x00F6 | 0x00F7 | 0x00F8 | 0x00F9 | 0x00FA | 0x00FB | 0x00FC | 0x00FD | 0x00FE |

<a id="table-lenkrad10x5006-07"></a>
### LENKRAD10X5006_07

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x00C3 | 0x00C4 |

<a id="table-lenkrad20x5006-07"></a>
### LENKRAD20X5006_07

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x003A | 0x003B |

<a id="table-laengsbeschl0x5008"></a>
### LAENGSBESCHL0X5008

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x00F0 | 0x0026 |

<a id="table-handbremse0x5008"></a>
### HANDBREMSE0X5008

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x0100 | 0x0101 | 0x0102 |

<a id="table-hydraulikdrucksens0x5101"></a>
### HYDRAULIKDRUCKSENS0X5101

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x00F0 | 0x0023 | 0x0050 | 0x00EA | 0x0049 | 0x00EB | 0x0053 | 0x0075 |

<a id="table-sensorposition0x5108bis0a"></a>
### SENSORPOSITION0X5108BIS0A

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x0043 | 0x0044 | 0x0014 | 0x00EC | 0x007F | 0x007D | 0x007C | 0x007E |

<a id="table-getriebeeingang0x510b"></a>
### GETRIEBEEINGANG0X510B

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x00F0 | 0x006A | 0x0044 | 0x0046 | 0x0014 | 0x00E6 | 0x0103 | 0x0104 |

<a id="table-schaltstanger10x5106-07"></a>
### SCHALTSTANGER10X5106_07

Dimensions: 1 rows × 12 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 11 | 0x0043 | 0x0044 | 0x008B | 0x00EB | 0x00EC | 0x007F | 0x0080 | 0x007A | 0x007B | 0x007D | 0x0098 |

<a id="table-motordrehz0x510c-5200"></a>
### MOTORDREHZ0X510C_5200

Dimensions: 1 rows × 10 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 9 | 0x00F0 | 0x0103 | 0x0104 | 0x0043 | 0x0046 | 0x0069 | 0x006C | 0x0014 | 0x0044 |

<a id="table-radgeschwhl0x5201"></a>
### RADGESCHWHL0X5201

Dimensions: 1 rows × 11 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | 0x00F0 | 0x0103 | 0x0104 | 0x008B | 0x0043 | 0x00E7 | 0x00E8 | 0x00EE | 0x00EF | 0x0056 |

<a id="table-radgeschwhr0x5202"></a>
### RADGESCHWHR0X5202

Dimensions: 1 rows × 11 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | 0x00F0 | 0x0103 | 0x0104 | 0x008B | 0x0043 | 0x00E7 | 0x00E8 | 0x00EE | 0x00EF | 0x0057 |

<a id="table-radgeschwvl0x5203"></a>
### RADGESCHWVL0X5203

Dimensions: 1 rows × 10 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 9 | 0x00F0 | 0x00B3 | 0x008B | 0x0043 | 0x00E7 | 0x00E8 | 0x00EE | 0x00EF | 0x0058 |

<a id="table-radgeschwvr0x5204"></a>
### RADGESCHWVR0X5204

Dimensions: 1 rows × 10 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 9 | 0x00F0 | 0x00B4 | 0x008B | 0x0043 | 0x00E7 | 0x00E8 | 0x00EE | 0x00EF | 0x0059 |

<a id="table-betriebsbremssig0x5206"></a>
### BETRIEBSBREMSSIG0X5206

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x00F0 | 0x0026 | 0x003D | 0x0055 | 0x0142 |

<a id="table-bremszuendsig0x5206"></a>
### BREMSZUENDSIG0X5206

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x0132 | 0x0133 | 0x012E | 0x012F | 0x0130 | 0x0131 |

<a id="table-getriebekuppfussstatus"></a>
### GETRIEBEKUPPFUSSSTATUS

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x0105 | 0x0106 | 0x0107 | 0x0108 | 0x0109 | 0x010A | 0x010B | 0x010C | 0x010D | 0x010E | 0x010F | 0x0110 | 0x0111 | 0x0112 | 0x0113 | 0x0114 |

<a id="table-lenkwinkel0x520a"></a>
### LENKWINKEL0X520A

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x00F0 | 0x005D | 0x003F | 0x00D3 |

<a id="table-drehmoment0x5208"></a>
### DREHMOMENT0X5208

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x00F0 | 0x0067 | 0x0040 | 0x00D4 |

<a id="table-klemmer-15-500x5210"></a>
### KLEMMER_15_500X5210

Dimensions: 1 rows × 12 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | 0x00F0 | 0x0046 | 0x0116 | 0x0117 | 0x0118 | 0x0119 | 0x011A | 0x011B | 0x011C | 0x011D | 0x011E |

<a id="table-statusdigitaleausgaenge"></a>
### STATUSDIGITALEAUSGAENGE

Dimensions: 1 rows × 16 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 15 | 0x011F | 0x0120 | 0x0121 | 0x0122 | 0x0123 | 0x0124 | 0x0125 | 0x0126 | 0x0127 | 0x0128 | 0x0129 | 0x012A | 0x012B | 0x012C | 0x012D |

<a id="table-shiftlock0x5400"></a>
### SHIFTLOCK0X5400

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x0134 | 0x0135 | 0x0136 |

<a id="table-spg-mdrehz0x5400-01"></a>
### SPG_MDREHZ0X5400_01

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x0F0 | 0x0046 |

<a id="table-anlasserfreigabe0x5401"></a>
### ANLASSERFREIGABE0X5401

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x0137 | 0x0138 | 0x0139 |

<a id="table-hydpumpe0x5402"></a>
### HYDPUMPE0X5402

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x00F0 | 0x0023 | 0x0050 | 0x0049 | 0x0046 |

<a id="table-magnetventil5-30x5509"></a>
### MAGNETVENTIL5_30X5509

Dimensions: 1 rows × 11 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | 0x00F0 | 0x001A | 0x0023 | 0x0020 | 0x0024 | 0x0088 | 0x0085 | 0x0078 | 0x0049 | 0x0061 |

<a id="table-digeinresetfest"></a>
### DIGEINRESETFEST

Dimensions: 1 rows × 15 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 14 | 0x0144 | 0x0146 | 0x0147 | 0x0148 | 0x0149 | 0x014A | 0x014B | 0x014C | 0x014D | 0x014E | 0x014F | 0x0150 | 0x0152 | 0x0153 |

<a id="table-fehlerstatuscanbus"></a>
### FEHLERSTATUSCANBUS

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x00F0 | 0x0069 | 0x00A1 |

<a id="table-getriebetemp0x4f44"></a>
### GETRIEBETEMP0X4F44

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x00F0 | 0x0050 | 0x0176 | 0x0051 | 0x00EA | 0x0046 | 0x0076 |

<a id="table-relaisgetroelp0x5406-1"></a>
### RELAISGETROELP0X5406_1

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x00F0 | 0x0176 | 0x0046 |

<a id="table-relaisgetroelp0x5406-2"></a>
### RELAISGETROELP0X5406_2

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x00C6 | 0x0076 | 0x017D |

<a id="table-getriebetemp0x4f45"></a>
### GETRIEBETEMP0X4F45

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x00F0 | 0x0050 | 0x0176 | 0x0051 |

<a id="table-hydraulik0x4f44"></a>
### HYDRAULIK0X4F44

Dimensions: 1 rows × 10 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 9 | 0x00F0 | 0x0023 | 0x0050 | 0x0051 | 0x00EA | 0x0046 | 0x017A | 0x017B | 0x017C |

<a id="table-hydraulik0x4f43"></a>
### HYDRAULIK0X4F43

Dimensions: 1 rows × 10 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 9 | 0x00F0 | 0x0023 | 0x0050 | 0x0051 | 0x00EA | 0x0046 | 0x0177 | 0x0178 | 0x0179 |

<a id="table-prgwahl0x5004-05-1"></a>
### PRGWAHL0X5004_05_1

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x00B6 | 0x00B7 |

<a id="table-prgwahl0x5004-05-2"></a>
### PRGWAHL0X5004_05_2

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x002B | 0x002C |

<a id="table-fumwelttexte49"></a>
### FUMWELTTEXTE49

Dimensions: 14 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kaltstart |
| 0x01 | NMI (Non Maskable Interrupt) Sicherheitskonzeptreset MU |
| 0x02 | Stack overflow |
| 0x03 | Stack unterflow |
| 0x04 | Undefinierter Opcode |
| 0x05 | Protected Instruction Fault |
| 0x06 | Illegale Wordoperation |
| 0x07 | Illegaler Instruction Access |
| 0x08 | Illegaler Externer Buszugriff |
| 0x09 | Softwarereset |
| 0x10 | Interner Watchdog Reset |
| 0x11 | Sicherheitskonzeptreset MC |
| 0x12 | Diagnoseprotokollreset |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte52"></a>
### FUMWELTTEXTE52

Dimensions: 61 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Der Ablauf eines Automaten ist nicht korrekt |
| 0x02 | Die Maximale Zeit die eine Adaption am Band in Anspruch nehmen darf ist ueberschritten |
| 0x0A | Speichervorspanndruckermittlung nicht durchfuehrbar |
| 0x0B | Powerpack zu warm |
| 0x0C | Druckaufbau fehlerhaft |
| 0x0D | Druckabbau fehlerhaft |
| 0x0E | Entleeren des HE-Systemdrucks nicht durchfuehrbar |
| 0x0F | Bei Entleeren Druckabbau fehlerhaft |
| 0x10 | Entlüften des HE-Systemdrucks nicht durchfuehrbar |
| 0x11 | Druckaufbau Pumpenblock fehlerhaft |
| 0x12 | Druckabbau Pumpenblock fehlerhaft |
| 0x13 | Druckaufbau Stellerblock fehlerhaft |
| 0x14 | Druckabbau Stellerblock fehlerhaft |
| 0x1E | kein gültiger PWV Offsetstrom  |
| 0x28 | die Zeit zum Einlegen der Schaltwegmitten ist ueberschritten |
| 0x29 | Hydraulikdruck ist zu gering  |
| 0x2A | Einlegehaenger erkannt |
| 0x2B | Einlegehaenger in Gang 1 vorhanden / Werte wurden substituiert |
| 0x2C | Einlegehaenger in Gang 2 vorhanden / Werte wurden substituiert |
| 0x2D | Einlegehaenger in Gang 3 vorhanden / Werte wurden substituiert |
| 0x2E | Einlegehaenger in Gang 4 vorhanden / Werte wurden substituiert |
| 0x2F | Einlegehaenger in Gang 5 vorhanden / Werte wurden substituiert |
| 0x30 | Einlegehaenger in Gang 6 vorhanden / Werte wurden substituiert |
| 0x31 | Einlegehaenger in Gang 7 vorhanden / Werte wurden substituiert |
| 0x32 | Einlegehaenger in Rueckwaertsgang vorhanden / Werte wurden substituiert |
| 0x33 | Schaltweg zu weit ausgerueckt |
| 0x34 | Ueberschreitung elektrischer Bereich des redundanten Positionssensors Schaltstange R/1 |
| 0x35 | Ueberschreitung elektrischer Bereich des Positionssensors Schaltstange R/1 |
| 0x36 | Ueberschreitung elektrischer Bereich des Positionssensors Schaltstange 5/3 |
| 0x37 | Ueberschreitung elektrischer Bereich des Positionssensors Schaltstange 2/4 |
| 0x38 | Ueberschreitung elektrischer Bereich des Positionssensors Schaltstange 6/7 |
| 0x39 | Beim Adaptieren einer Schaltstange ist eine weitere Schaltstange verbotenerweise mit eingerueckt |
| 0x3A | Beim Ermitteln der Schaltkraft konnte die zuvor eingelernte Position nicht erreicht werden |
| 0x3B | Beim Adaptieren des 1. Gangs konnte der Positionsgrenzwert nicht erreicht werden |
| 0x3C | Beim Adaptieren des 2. Gangs konnte der Positionsgrenzwert nicht erreicht werden |
| 0x3D | Beim Adaptieren des 3. Gangs konnte der Positionsgrenzwert nicht erreicht werden |
| 0x3E | Beim Adaptieren des 4. Gangs konnte der Positionsgrenzwert nicht erreicht werden |
| 0x3F | Beim Adaptieren des 5. Gangs konnte der Positionsgrenzwert nicht erreicht werden |
| 0x40 | Beim Adaptieren des 6. Gangs konnte der Positionsgrenzwert nicht erreicht werden |
| 0x41 | Beim Adaptieren des 6. Gangs konnte der Positionsgrenzwert nicht erreicht werden |
| 0x42 | Beim Adaptieren des Rueckwaertsgangs konnte der Positionsgrenzwert nicht erreicht werden |
| 0x43 | Wert des Temperatursensors ausserhalb der elektrischen Grenzen |
| 0x46 | Schaltwegmittenpositionierung Schaltstange R/1 gescheitert |
| 0x47 | Schaltwegmittenpositionierung Schaltstange 5/3 gescheitert |
| 0x48 | Schaltwegmittenpositionierung Schaltstange 2/4 gescheitert |
| 0x49 | Schaltwegmittenpositionierung Schaltstange 6/7 gescheitert |
| 0x50 | Beliebigen Gang Einlegen gescheitert |
| 0x51 | Ungueltige Gangvorgabe |
| 0x52 | Dauerlaufabbruch wegen zu heissem Powerpack |
| 0x53 | Dauerlaufabbruch Schaltung konnte nicht ausgefuehrt werden |
| 0x54 | Dauerlaufabbruch ueber extern |
| 0x55 | ???? |
| 0x56 | Dauerlaufabbruch wegen Drehzahldifferenz Soll Ist |
| 0x5A | Eingelernter Wert außerhalb des für Offset zulaessigen Bereichs |
| 0x5B | Zeit zum Offset einlernen abgelaufen ohne dass der Offset ermittelt werden konnte |
| 0x5F | Test Kupplungsventil nicht durchfuehrbar |
| 0x60 | Mindeststartwert für Kupplungsposition nicht gegeben |
| 0x61 | Weg des Kupplungsventils ausserhalb des spezifizierten Bereichs |
| 0x62 | Offsetstromermittlung des Kupplungsventils fehlgeschlagen |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte53"></a>
### FUMWELTTEXTE53

Dimensions: 43 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Adaptionsstatus: Kupplung oeffnen |
| 0x02 | Adaptionsstatus: PWV Offsetstromadaption |
| 0x03 | Adaptionsstatus: Gang 1 ausmessen |
| 0x04 | Adaptionsstatus: Gang 2 ausmessen |
| 0x05 | Adaptionsstatus: Gang 3 ausmessen |
| 0x06 | Adaptionsstatus: Gang 4 ausmessen |
| 0x07 | Adaptionsstatus: Gang 5 ausmessen |
| 0x08 | Adaptionsstatus: Gang 6 ausmessen |
| 0x09 | Adaptionsstatus: Gang 7 ausmessen |
| 0x0A | Adaptionsstatus: Gang R ausmessen |
| 0x0B | Adaptionsstatus: Neutralstellung einnehmen |
| 0x0C | Adaptionsstatus: Adaptionsstatuswerte in NVRAM schreiben |
| 0x0D | Adaptionsstatus: Adaptionsstatus: Einlegehänger nach bearbeiten |
| 0x0E | Adaptionsstatus: Getriebeparameter verarbeiten |
| 0x0F | Adaptionsstatus: Getriebe einlernen beenden |
| 0x14 | Initialisierung Speichervorspanndruckermittlung |
| 0x15 | Druckaufbau |
| 0x16 | Druckabbau |
| 0x17 | Speichervorspanndruckermittlung beendet |
| 0x18 | Initialisierung HE Entleeren |
| 0x19 | HE Entleeren Druckabbau |
| 0x1A | HE Entleeren beendet |
| 0x1B | HE System Aktuatorentlüftung |
| 0x1C | Initialisierung Aktuatorentlueftung |
| 0x1D | Aktuatorentlueftung |
| 0x1E | Aktuatorentlüftung beendet |
| 0x28 | Schaltwegmittellagepositionierung |
| 0x29 | Schaltwegmittellagepositionierung beendet |
| 0x3D | Beliebigen Gang einlegen initialisieren |
| 0x3E | Beliebigen Gang übernehmen |
| 0x3F | Warten bis beliebigen Gang eingelegt |
| 0x40 | Beliebigen Gang einlegen beendet |
| 0x46 | Offset des Laengsbeschleunigungssensors einlernen initialisieren |
| 0x47 | Offset des Laengsbeschleunigungssensors einlernen erster Wert |
| 0x48 | Offset des Laengsbeschleunigungssensors einlernen Warten |
| 0x49 | Offset des Laengsbeschleunigungssensors einlernen folgender Wert |
| 0x4A | Offset des Laengsbeschleunigungssensors einlernen berechnen |
| 0x4B | Offset des Laengsbeschleunigungssensors einlernen beendet |
| 0x50 | Kupplungstest initialisieren |
| 0x51 | Ueberpruefen der Kupplungspositionen |
| 0x52 | Ermitteln und Ueberpruefen des Offsetstroms des Kupplungsventils |
| 0x53 | Kupplungstest beendet |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte50"></a>
### FUMWELTTEXTE50

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Kurzschluss nach Ubatt |
| 0x04 | Leitungsunterbrechung |
| 0x08 | Unerlaubter Strom |
| 0x10 | Ventil fehlerhaft geoeffnet |
| 0x20 | Falsche Verfahrrichtung |
| 0xXY | nicht definiert |

<a id="table-fumwelttexte51"></a>
### FUMWELTTEXTE51

Dimensions: 13 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x20 | 0x20= Speichervorspanndruck ermitteln |
| 0x21 | 0x21= Beliebigen Gang einlegen |
| 0x22 | 0x22= Schaltwegmittellage positionieren |
| 0x23 | 0x23= Startbedingungen fuer Motor herstellen |
| 0x30 | 0x30= Entlueftung Kuppl.-Nehmerzyl./Hydraulikleit. |
| 0x31 | 0x31= Entlueftung Getriebeakuator |
| 0x32 | 0x32= Kupplungsventilkennwerte einlernen |
| 0x33 | 0x33= Kupplungsschleifpunkt einlernen |
| 0x34 | 0x34= Offsetstroeme PWV einlernen |
| 0x35 | 0x35= Hydraulikdruck abbauen |
| 0x36 | 0x36= Getriebe komplett einlernen |
| 0x37 | 0x37= Offset Laengsbeschleunigungssensor einlernen |
| 0x38 | 0x38= Adaptionswerte in NVRAM speichern |
