# SZL_56.prg

- Jobs: [51](#jobs)
- Tables: [22](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Schaltzentrum Lenksäule / Lenkwinkelsensor  |
| ORIGIN | MSF EEK-E Krenn |
| REVISION | 1.001 |
| AUTHOR | Valeo TS Wigger |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
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
- [STATUS_LENKSTOCK](#job-status-lenkstock) - Status der Lenkstock-Funktionen
- [STATUS_TASTER_LENKRAD](#job-status-taster-lenkrad) - Status der einzelnen Tasten am Lenkrad
- [STATUS_LENKWINKELSENSOR](#job-status-lenkwinkelsensor) - Status des Lenkwinkelsensors (nur fuer Variante mit Lenkwinkelsensor)
- [STATUS_BLINKERRUECKSTELLUNG](#job-status-blinkerrueckstellung) - Status der Blinkerrueckstellung (nur fuer Variante ohne Lenkwinkelsensor)
- [STATUS_CAN_SIGNALE](#job-status-can-signale) - Status der empfangenen CAN-Signale
- [STATUS_SOFTWARE_BUILD_INFO](#job-status-software-build-info) - Auslesen der Software Build Informationen
- [STATUS_LENKSTOCK_INTERN](#job-status-lenkstock-intern) - Interner Status der Lenkstock-Funktionen
- [STATUS_TASTER_LENKRAD_INTERN](#job-status-taster-lenkrad-intern) - Interner Status der einzelnen Tasten am Lenkrad
- [STATUS_LENKWINKELSENSOR_INTERN](#job-status-lenkwinkelsensor-intern) - Interner Status des Lenkwinkelsensors (nur fuer Variante mit Lenkwinkelsensor)
- [STATUS_BLINKERRUECKSTELLUNG_INTERN](#job-status-blinkerrueckstellung-intern) - Interner Status der Blinkerrueckstellung (nur fuer Variante ohne Lenkwinkelsensor)
- [STATUS_LWS_NULLPUNKT_OFFSET](#job-status-lws-nullpunkt-offset) - Auslesen des Offsets vom Nullpunkt-Abgleich des Lenkwinkelsensors (nur fuer Variante mit Lenkwinkelsensor)
- [STATUS_LWS_SERIENNUMMER](#job-status-lws-seriennummer) - Auslesen der Seriennummer des Lenkwinkelsensors
- [STATUS_LWS_HALL_SKALIERUNG](#job-status-lws-hall-skalierung) - Auslesen der Skalierungsfaktoren der Hall-Elemente des Lenkwinkelsensors (nur fuer Variante mit Lenkwinkelsensor)
- [STEUERN_LWS_ABGLEICH](#job-steuern-lws-abgleich) - Abgleichen des Lenkwinkelsensors bei Lenkrad-Geradeausstellung (nur fuer Variante mit Lenkwinkelsensor) Vorbedingungen fuer Abgleich: - Aktueller Lenkwinkel im Bereich -15 Grad bis +15 Grad - Alle gueltigen Radgeschwindigkeiten gleich 0 km/h - Hoechstens eine Radgeschwindigkeit ist ungueltig
- [STEUERN_LWS_ABGLEICH_RUECKSETZEN](#job-steuern-lws-abgleich-ruecksetzen) - Abgleichwert wird zurueckgesetzt (nur fuer Variante mit Lenkwinkelsensor) Ist bei R56 vor einem erneuten Abgleich nicht notwendig Dient nur zur Verwendung in der Valeo Fertigung
- [STEUERN_MC2_FLASH_SCHREIBEN](#job-steuern-mc2-flash-schreiben) - Programmcode des MC-2 von MC-1 nach MC-2 schreiben (nur fuer Variante mit Lenkwinkelsensor)
- [_STATUS_FEHLER_LESEN_INTERN](#job-status-fehler-lesen-intern) - Auslesen der internen Fehlercodes und -zaehler

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

<a id="job-status-lenkstock"></a>
### STATUS_LENKSTOCK

Status der Lenkstock-Funktionen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LENKSTOCK_BLINKER_TASTER_AXIAL_OBEN | int | 0: Lenkstock Blinker axialer Taster oben nicht betaetigt 1: Lenkstock Blinker axialer Taster oben betaetigt Hinweis Entspricht bei R56 dem Bordcomputer-Taster |
| STAT_LENKSTOCK_WISCHER_WERT | int | Lenkstock Wischer 0: Lenkstock Wischer in Nullstellung 1: Tippwischen betaetigt 2: Lenkstock Wischer in Stufe 1 betaetigt 3: Lenkstock Wischer in Stufe 2 betaetigt 4: Frontwaschen betaetigt 5: Lenkstock Wischer in Stellung Intervall 6: Heckwischen betaetigt 7: Heckwaschen betaetigt 8: Mehrfachbetaetigung Nummerierung bleibt erhalten, auch bei Entfall mehrerer Funktionen Hinweis Bei R56 sind alle Wischerfunktionen nur bei "Klemme R EIN" aktiv |
| STAT_LENKSTOCK_WISCHER_TEXT | string | Text zu STAT_LENKSTOCK_WISCHER_WERT siehe table STAT_LENKSTOCK_WISCHER VSWERT STATUS_TEXT |
| STAT_LENKSTOCK_WISCHER_TIPPWISCHEN | int | 0: Lenkstock Wischer nicht in Stellung Tippwischen 1: Lenkstock Wischer in Stellung Tippwischen |
| STAT_LENKSTOCK_WISCHER_NULLSTELLUNG | int | 0: Lenkstock Wischer nicht Nullstellung 1: Lenkstock Wischer Nullstellung Hinweis Bei Schalter entspricht die Nullstellung der Stufe Aus, bei einem Taster der Mittelstellung |
| STAT_LENKSTOCK_WISCHER_POS_INTERVALL | int | 0: Lenkstock Wischer nicht in Stellung Intervall 1: Lenkstock Wischer in Stellung Intervall |
| STAT_LENKSTOCK_WISCHER_POS_1 | int | 0: Lenkstock Wischer nicht in Stellung Position 1 1: Lenkstock Wischer in Position 1 |
| STAT_LENKSTOCK_WISCHER_POS_2 | int | 0: Lenkstock Wischer nicht in Stellung Position 2 1: Lenkstock Wischer in Position 2 |
| STAT_LENKSTOCK_WISCHER_FRONTWASCHEN | int | 0: Lenkstock Wischer nicht in Stellung Frontwaschen 1: Lenkstock Wischer in Stellung Frontwaschen |
| STAT_LENKSTOCK_WISCHER_HECKWISCHEN | int | 0: Lenkstock Wischer nicht in Stellung Heckwischen 1: Lenkstock Wischer in Stellung Heckwischen |
| STAT_LENKSTOCK_WISCHER_HECKWASCHEN | int | 0: Lenkstock Wischer nicht in Stellung Heckwaschen 1: Lenkstock Wischer in Stellung Heckwaschen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-taster-lenkrad"></a>
### STATUS_TASTER_LENKRAD

Status der einzelnen Tasten am Lenkrad

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TASTER_LENKRAD_MFL1_WERT | int | 0 : Keine Aktion 1 : Push to talk betaetigt 2 : Volume/Lautstaerke plus betaetigt 3 : Volume/Lautstaerke minus betaetigt 4 : Telefontaste betaetigt 5 : Mehrfachbetaetigung Nummerierung bleibt erhalten, auch bei Entfall mehrerer Funktionen |
| STAT_TASTER_LENKRAD_MFL1_TEXT | string | Text zu STAT_TASTER_LENKRAD_MFL1_WERT siehe table STAT_MFL1 VSWERT STATUS_TEXT |
| STAT_TASTER_LENKRAD_MFL2_WERT | int | 0 : Keine Aktion 1 : Programmierbare Taste 1 gedrueckt 2 : Programmierbare Taste 2 gedrueckt 3 : Suchlauf auf gedrueckt 4 : Suchlauf ab gedrueckt 5 : Mehrfachbetaetigung Nummerierung bleibt erhalten, auch bei Entfall mehrerer Funktionen |
| STAT_TASTER_LENKRAD_MFL2_TEXT | string | Text zu STAT_TASTER_LENKRAD_MFL2_WERT siehe table STAT_MFL2 VSWERT STATUS_TEXT |
| STAT_TASTER_LENKRAD_MFL_PUSH_TO_TALK | int | 0: Push to talk nicht betaetigt 1: Push to talk betaetigt Hinweis Wird bei R56 nur einmalig nach jedem Tastendruck erzeugt |
| STAT_TASTER_LENKRAD_MFL_VOL_PLUS | int | 0: Volume/Lautstaerke plus nicht betaetigt 1: Volume/Lautstaerke plus betaetigt |
| STAT_TASTER_LENKRAD_MFL_VOL_MINUS | int | 0: Volume/Lautstaerke minus nicht betaetigt 1: Volume/Lautstaerke minus betaetigt |
| STAT_TASTER_LENKRAD_MFL_TEL | int | 0: Telefontaste nicht betaetigt 1: Telefontaste betaetigt |
| STAT_TASTER_LENKRAD_MFL_SUCHLAUF_AUF | int | 0: Suchlauf auf nicht gedrueckt 1: Suchlauf auf gedrueckt |
| STAT_TASTER_LENKRAD_MFL_SUCHLAUF_AB | int | 0: Suchlauf ab nicht gedrueckt 1: Suchlauf ab gedrueckt |
| STAT_TASTER_LENKRAD_MFL_FGR_EIN | int | 0: FGR ein nicht gedrueckt 1: FGR ein gedrueckt |
| STAT_TASTER_LENKRAD_MFL_FGR_SETZEN | int | 0: FGR setzen / Wiederaufnahme nicht gedrueckt 1: FGR setzen / Wiederaufnahme gedrueckt |
| STAT_TASTER_LENKRAD_MFL_FGR_GESCHW_PLUS | int | 0: FGR Geschwindigkeit plus nicht gedrueckt 1: FGR Geschwindigkeit plus gedrueckt |
| STAT_TASTER_LENKRAD_MFL_FGR_GESCHW_MINUS | int | 0: FGR Geschwindigkeit minus nicht gedrueckt 1: FGR Geschwindigkeit minus gedrueckt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lenkwinkelsensor"></a>
### STATUS_LENKWINKELSENSOR

Status des Lenkwinkelsensors (nur fuer Variante mit Lenkwinkelsensor)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LENKWINKEL_ABGEGLICHEN | int | 0: LWS nicht abgeglichen 1: LWS abgeglichen |
| STAT_LENKWINKEL_WERT | real | Bereich von -650 Grad bis +650 Grad Aufloesung: 0,04395 [Grad/Bit] -1440,15 = Signal ungueltig |
| STAT_LENKWINKEL_EINH | string | Einheit Grad |
| STAT_LENKWINKELSTATUS_WERT | int | 0: Fehlerhaft 1: Absolut 2: Relativ 3: Ungueltig |
| STAT_LENKWINKELSTATUS_TEXT | string | Text zu STAT_LENKWINKELSTATUS_WERT siehe table STAT_LENKWINKEL VSWERT STATUS_TEXT |
| STAT_LENKRAD_WINKELGESCHWINDIGKEIT_WERT | real | Winkelgeschwindigkeit Bereich von -1440,11 Grad/s bis +1440,11 Grad/s Aufloesung: 0,04395 [(Grad/s)/Bit] -1440,15 = Signal ungueltig |
| STAT_LENKRAD_WINKELGESCHWINDIGKEIT_EINH | string | Einheit Grad/s |
| STAT_ABGLEICH_OFFSET_WERT | real | Bereich von -15 Grad bis +15 Grad Aufloesung: 0,04395 [Grad/Bit] -1440,15 = Signal ungueltig |
| STAT_ABGLEICH_OFFSET_EINH | string | Einheit Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-blinkerrueckstellung"></a>
### STATUS_BLINKERRUECKSTELLUNG

Status der Blinkerrueckstellung (nur fuer Variante ohne Lenkwinkelsensor)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RUECKSTELLUNG_BLINKER_WERT | int | 1: Rueckstellung inaktiv 2: Rueckstellung RE aktiv 3: Rueckstellung LI aktiv 4: RE rueckstellen 5: LI rueckstellen 15: Signal ungueltig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-signale"></a>
### STATUS_CAN_SIGNALE

Status der empfangenen CAN-Signale

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLEMME_R_NR | int | CAN-Signal "Status Klemme R" 0: Klemme R AUS 1: Klemme R EIN 3: Signal ungueltig |
| STAT_KLEMME_R_TEXT | string | Text zu STAT_KLEMME_R_NR |
| STAT_KLEMME_15_NR | int | CAN-Signal "Status Klemme 15" 0: Klemme 15 AUS 1: Klemme 15 EIN 3: Signal ungueltig |
| STAT_KLEMME_15_TEXT | string | Text zu STAT_KLEMME_15_NR |
| STAT_GESCHWINDIGKEIT_RAD_VL_WERT | real | CAN-Signal "Geschwindigkeit Rad VL" Bereich von -300,00 km/h bis +300,00 km/h Aufloesung: 0,0625 [(km/h)/Bit] -2048,00 = Signal ungueltig |
| STAT_GESCHWINDIGKEIT_RAD_VR_WERT | real | CAN-Signal "Geschwindigkeit Rad VR" Bereich von -300,00 km/h bis +300,00 km/h Aufloesung: 0,0625 [(km/h)/Bit] -2048,00 = Signal ungueltig |
| STAT_GESCHWINDIGKEIT_RAD_HL_WERT | real | CAN-Signal "Geschwindigkeit Rad HL" Bereich von -300,00 km/h bis +300,00 km/h Aufloesung: 0,0625 [(km/h)/Bit] -2048,00 = Signal ungueltig |
| STAT_GESCHWINDIGKEIT_RAD_HR_WERT | real | CAN-Signal "Geschwindigkeit Rad HR" Bereich von -300,00 km/h bis +300,00 km/h Aufloesung: 0,0625 [(km/h)/Bit] -2048,00 = Signal ungueltig |
| STAT_GESCHWINDIGKEIT_RAD_EINH | string | Einheit km/h |
| STAT_BELEUCHTUNG_SCHALTER_NR | int | CAN-Signal "Steuerung Beleuchtung Schalter" 0 - 253: Nacht (0..Minimum, 253..Maximum am Poti eingestellt) 254: Tag 255: Signal ungueltig |
| STAT_BELEUCHTUNG_SCHALTER_TEXT | string | Text zu STAT_BELEUCHTUNG_SCHALTER_NR |
| STAT_BLINKEN_NR | int | CAN-Signal "Status Blinken" 0: Beide Blinker AUS 1: Blinker links EIN 2: Blinker rechts EIN 3: Beide Blinker EIN 7: Signal ungueltig |
| STAT_BLINKEN_TEXT | string | Text zu STAT_BLINKEN_NR |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-software-build-info"></a>
### STATUS_SOFTWARE_BUILD_INFO

Auslesen der Software Build Informationen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MC1_BUILD_DATUM_JAHR_NR | int | Build-Datum des MC-1 (Jahr) |
| STAT_MC1_BUILD_DATUM_MONAT_NR | int | Build-Datum des MC-1 (Monat) |
| STAT_MC1_BUILD_DATUM_TAG_NR | int | Build-Datum des MC-1 (Tag) |
| STAT_MC1_BUILD_DATUM_TEXT | string | Text zu Build-Datum des MC-1 |
| STAT_MC1_BUILD_UHRZEIT_STUNDE_NR | int | Build-Uhrzeit des MC-1 (Stunde) |
| STAT_MC1_BUILD_UHRZEIT_MINUTE_NR | int | Build-Uhrzeit des MC-1 (Minute) |
| STAT_MC1_BUILD_UHRZEIT_SEKUNDE_NR | int | Build-Uhrzeit des MC-1 (Sekunde) |
| STAT_MC1_BUILD_UHRZEIT_TEXT | string | Text zu Build-Uhrzeit des MC-1 |
| STAT_MC2_BUILD_DATUM_JAHR_NR | int | Build-Datum des MC-2 (Jahr) |
| STAT_MC2_BUILD_DATUM_MONAT_NR | int | Build-Datum des MC-2 (Monat) |
| STAT_MC2_BUILD_DATUM_TAG_NR | int | Build-Datum des MC-2 (Tag) |
| STAT_MC2_BUILD_DATUM_TEXT | string | Text zu Build-Datum des MC-2 |
| STAT_MC2_BUILD_UHRZEIT_STUNDE_NR | int | Build-Uhrzeit des MC-2 (Stunde) |
| STAT_MC2_BUILD_UHRZEIT_MINUTE_NR | int | Build-Uhrzeit des MC-2 (Minute) |
| STAT_MC2_BUILD_UHRZEIT_SEKUNDE_NR | int | Build-Uhrzeit des MC-2 (Sekunde) |
| STAT_MC2_BUILD_UHRZEIT_TEXT | string | Text zu Build-Uhrzeit des MC-2 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lenkstock-intern"></a>
### STATUS_LENKSTOCK_INTERN

Interner Status der Lenkstock-Funktionen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FRONT_WISCHER_NULL_AKTIV | int | 0: Scheibenwischerschalter nicht Nullstellung 1: Scheibenwischerschalter Nullstellung |
| STAT_FRONT_WISCHER_F1_OBEN_AKTIV | int | 0: Scheibenwischerschalter nicht nach oben getippt 1: Scheibenwischerschalter nach oben getippt |
| STAT_FRONT_WISCHER_F2_OBEN_AKTIV | int | 0: Scheibenwischerschalter nicht nach oben ueberdrueckt 1: Scheibenwischerschalter nach oben ueberdrueckt |
| STAT_FRONT_WISCHER_UNTEN_AKTIV | int | 0: Scheibenwischerschalter nicht nach unten getippt 1: Scheibenwischerschalter nach unten getippt |
| STAT_FRONT_WISCHER_ZIEHEN_AKTIV | int | 0: Scheibenwischerschalter nicht entgegen Fahrtrichtung getippt (gezogen) 1: Scheibenwischerschalter entgegen Fahrtrichtung getippt (gezogen) |
| STAT_BC_TASTE_AKTIV | int | 0: Bordcomputer-Taste nicht getippt 1: Bordcomputer-Taste getippt |
| STAT_HECK_WISCHER_NR | int | Position des Heckwischerschalters 0: Nullstellung 1: Stellung Wischen 2: Stellung Waschen 3: Zwischenstellung |
| STAT_HECK_WISCHER_TEXT | string | Text zu STAT_HECK_WISCHER_NR |
| STAT_SPANNUNG_U_REF_WERT | real | Referenzspannung fuer Schalterauswertung Bereich von 0,00 Volt bis 5,00 Volt Aufloesung: 4,888 [mV] |
| STAT_SPANNUNG_HECK_WISCHER_WERT | real | Spannung an Heckwischerschalter Bereich von 0,00 Volt bis 5,00 Volt Aufloesung: 4,888 [mV] |
| STAT_SPANNUNG_PT_CAN_WAKEUP_WERT | real | Spannung an PT-CAN Weckleitung Bereich von 0,00 Volt bis 5,00 Volt Aufloesung: 4,888 [mV] |
| STAT_SPANNUNG_U_BATT_WERT | real | Versorgungsspannung Bereich von 0,0 Volt bis 17,7 Volt Aufloesung: 0,1 [Volt] |
| STAT_SPANNUNG_EINH | string | Einheit Volt |
| STAT_RATIO_HECK_WISCHER_WERT | real | Verhaeltnis der Spannung an Heckwischerschalter zur Referenzspannung Bereich von 0,0 Prozent bis 100,0 Prozent |
| STAT_RATIO_HECK_WISCHER_EINH | string | Einheit Prozent |
| STAT_KL_15_LOGISCH_AKTIV | int | 0: Signal KL_15_LOGISCH nicht aktiv (Ersatzwertbildung Klemme 15) 1: Signal KL_15_LOGISCH aktiv (Ersatzwertbildung Klemme 15) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-taster-lenkrad-intern"></a>
### STATUS_TASTER_LENKRAD_INTERN

Interner Status der einzelnen Tasten am Lenkrad

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPOMAT_WA_NR | int | Zustand der Taste WA des MFL vom Tempomatbus 0: Taste WA gedrueckt 1, 2: Taste WA ungueltiger Zustand 3: Taste WA nicht gedrueckt |
| STAT_TEMPOMAT_WA_TEXT | string | Text zu STAT_TEMPOMAT_WA_NR |
| STAT_TEMPOMAT_SB_NR | int | Zustand der Taste SB des MFL vom Tempomatbus 0: Taste SB gedrueckt 1, 2: Taste SB ungueltiger Zustand 3: Taste SB nicht gedrueckt |
| STAT_TEMPOMAT_SB_TEXT | string | Text zu STAT_TEMPOMAT_SB_NR |
| STAT_TEMPOMAT_VER_NR | int | Zustand der Taste VER des MFL vom Tempomatbus 0: Taste VER gedrueckt 1: Taste VER nicht gedrueckt |
| STAT_TEMPOMAT_VER_TEXT | string | Text zu STAT_TEMPOMAT_VER_NR |
| STAT_TEMPOMAT_AUS_NR | int | Zustand der Taste AUS des MFL vom Tempomatbus 0: Taste AUS gedrueckt 1, 2: Taste AUS ungueltiger Zustand 3: Taste AUS nicht gedrueckt |
| STAT_TEMPOMAT_AUS_TEXT | string | Text zu STAT_TEMPOMAT_AUS_NR |
| STAT_TEMPOMAT_TOGGLE_BIT | int | Toggle-Bit des MFL vom Tempomatbus |
| STAT_KBUS_VOLUME_UP_AKTIV | int | Zustand der Taste "Lautstaerke plus" des MFL vom K-Bus 0: Taste Lautstaerke plus nicht gedrueckt 1: Taste Lautstaerke plus gedrueckt |
| STAT_KBUS_VOLUME_DOWN_AKTIV | int | Zustand der Taste "Lautstaerke minus" des MFL vom K-Bus 0: Taste Lautstaerke minus nicht gedrueckt 1: Taste Lautstaerke minus gedrueckt |
| STAT_KBUS_SCAN_UP_AKTIV | int | Zustand der Taste "Suchlauf auf" des MFL vom K-Bus 0: Taste Suchlauf auf nicht gedrueckt 1: Taste Suchlauf auf gedrueckt |
| STAT_KBUS_SCAN_DOWN_AKTIV | int | Zustand der Taste "Suchlauf ab" des MFL vom K-Bus 0: Taste Suchlauf ab nicht gedrueckt 1: Taste Suchlauf ab gedrueckt |
| STAT_KBUS_PTT_TASTE_AKTIV | int | Zustand der Taste "Push-to-talk" des MFL vom K-Bus 0: Taste Push-to-talk nicht gedrueckt 1: Taste Push-to-talk gedrueckt Hinweis Wird bei R56 nur einmalig nach jedem Tastendruck erzeugt |
| STAT_KBUS_TELEFON_TASTE_AKTIV | int | Zustand der Taste "Telefon" des MFL vom K-Bus 0: Taste Telefon nicht gedrueckt 1: Taste Telefon gedrueckt |
| STAT_KBUS_SG_STATUS_NR | int | Aktueller Geraetestatus des MFL vom K-Bus 0: Steuergeraet bereit 255: Steuergeraet nicht bereit |
| STAT_KBUS_SG_STATUS_TEXT | string | Text zu STAT_KBUS_SG_STATUS_NR |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lenkwinkelsensor-intern"></a>
### STATUS_LENKWINKELSENSOR_INTERN

Interner Status des Lenkwinkelsensors (nur fuer Variante mit Lenkwinkelsensor)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENCODER_MC1_NR | int | 12-Bit-Codewort des optischen Encoders von MC-1 |
| STAT_ENCODER_MC1_TEXT | string | Text zu STAT_ENCODER_MC1_NR |
| STAT_ENCODER_MC2_NR | int | 12-Bit-Codewort des optischen Encoders von MC-2 |
| STAT_ENCODER_MC2_TEXT | string | Text zu STAT_ENCODER_MC2_NR |
| STAT_SPANNUNG_HALL_A1_WERT | real | Ausgangsspannung 1 von Hall-Element A Bereich von 0,00 Volt bis 5,00 Volt Aufloesung: 4,888 [mV/Bit] |
| STAT_SPANNUNG_HALL_A2_WERT | real | Ausgangsspannung 2 von Hall-Element A Bereich von 0,00 Volt bis 5,00 Volt Aufloesung: 4,888 [mV/Bit] |
| STAT_SPANNUNG_HALL_B1_WERT | real | Ausgangsspannung 1 von Hall-Element B Bereich von 0,00 Volt bis 5,00 Volt Aufloesung: 4,888 [mV/Bit] |
| STAT_SPANNUNG_HALL_B2_WERT | real | Ausgangsspannung 2 von Hall-Element B Bereich von 0,00 Volt bis 5,00 Volt Aufloesung: 4,888 [mV/Bit] |
| STAT_SPANNUNG_HALL_EINH | string | Einheit Volt |
| STAT_WINKEL_ZAHNRAD_WERT | real | Zahnradwinkel Bereich von 0,00 Grad bis 360,00 Grad Aufloesung: 0,0625 [Grad/Bit] |
| STAT_WINKEL_ZAHNRAD_EINH | string | Einheit Grad |
| STAT_TOLERANZ_ZAHNRAD_WERT | real | Zahnradwinkeltoleranz Bereich von 0,00 Grad bis 30,00 Grad Aufloesung: 0,0625 [Grad/Bit] |
| STAT_TOLERANZ_ZAHNRAD_EINH | string | Einheit Grad |
| STAT_WINKEL_LENKRAD_WERT | real | Absoluter Lenkradwinkel (unkalibriert) Bereich von -1080,0 Grad bis +1080,0 Grad Aufloesung: 0,5 [Grad/Bit] |
| STAT_WINKEL_LENKRAD_EINH | string | Einheit Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-blinkerrueckstellung-intern"></a>
### STATUS_BLINKERRUECKSTELLUNG_INTERN

Interner Status der Blinkerrueckstellung (nur fuer Variante ohne Lenkwinkelsensor)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LENKRAD_SEGMENT_NR | int | Aktuelles Segment in dem sich das Lenkrad befindet 0: Segment von -15 Grad bis +15 Grad 1: Segment von +15 Grad bis +30 Grad 2: Segment von -15 Grad bis -30 Grad 3: Segment von -30 Grad bis -180 Grad oder +30 Grad bis +180 Grad 255: Segment ungueltig |
| STAT_LENKRAD_SEGMENT_TEXT | string | Text zu STAT_LENKRAD_SEGMENT_NR |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lws-nullpunkt-offset"></a>
### STATUS_LWS_NULLPUNKT_OFFSET

Auslesen des Offsets vom Nullpunkt-Abgleich des Lenkwinkelsensors (nur fuer Variante mit Lenkwinkelsensor)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NULLPUNKT_OFFSET_WERT | real | Offset vom Nullpunkt-Abgleich des Lenkwinkelsensors Bereich von -15,0 Grad bis +15,0 Grad Aufloesung: 0,5 [Grad/Bit] -64,0 = LWS nicht abgeglichen |
| STAT_NULLPUNKT_OFFSET_EINH | string | Einheit Grad |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lws-seriennummer"></a>
### STATUS_LWS_SERIENNUMMER

Auslesen der Seriennummer des Lenkwinkelsensors

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERIENNUMMER_NR | unsigned long | Seriennummer des Lenkwinkelsensors Exxx-xxxxh = Versuchsteil 0000-0000h & FFFF-FFFFh = Seriennummer ungueltig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lws-hall-skalierung"></a>
### STATUS_LWS_HALL_SKALIERUNG

Auslesen der Skalierungsfaktoren der Hall-Elemente des Lenkwinkelsensors (nur fuer Variante mit Lenkwinkelsensor)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SKALIERUNG_HALL_A_WERT | real | Skalierungsfaktor von Hall-Element A Bereich von 0,016 bis 3,984 Aufloesung: 0,015625 [1/Bit] 0,000 = Kein Skalierungsfaktor gespeichert |
| STAT_SKALIERUNG_HALL_B_WERT | real | Skalierungsfaktor von Hall-Element B Bereich von 0,016 bis 3,984 Aufloesung: 0,015625 [1/Bit] 0,000 = Kein Skalierungsfaktor gespeichert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lws-abgleich"></a>
### STEUERN_LWS_ABGLEICH

Abgleichen des Lenkwinkelsensors bei Lenkrad-Geradeausstellung (nur fuer Variante mit Lenkwinkelsensor) Vorbedingungen fuer Abgleich: - Aktueller Lenkwinkel im Bereich -15 Grad bis +15 Grad - Alle gueltigen Radgeschwindigkeiten gleich 0 km/h - Hoechstens eine Radgeschwindigkeit ist ungueltig

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| JOB_INFO_GELESEN | string | Dient nur zur Sicherheit, wird nicht im Telegramm verwendet "start" -&gt; Job ausfuehren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lws-abgleich-ruecksetzen"></a>
### STEUERN_LWS_ABGLEICH_RUECKSETZEN

Abgleichwert wird zurueckgesetzt (nur fuer Variante mit Lenkwinkelsensor) Ist bei R56 vor einem erneuten Abgleich nicht notwendig Dient nur zur Verwendung in der Valeo Fertigung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| JOB_INFO_GELESEN | string | Dient nur zur Sicherheit, wird nicht im Telegramm verwendet "start" -&gt; Job ausfuehren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mc2-flash-schreiben"></a>
### STEUERN_MC2_FLASH_SCHREIBEN

Programmcode des MC-2 von MC-1 nach MC-2 schreiben (nur fuer Variante mit Lenkwinkelsensor)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| JOB_INFO_GELESEN | string | Dient nur zur Sicherheit, wird nicht im Telegramm verwendet "start" -&gt; Job ausfuehren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MC2_NR | int | Antwort des MC-2 |
| STAT_MC2_TEXT | string | Antwort des MC-2 table SG_Mc2Antwort MC2_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fehler-lesen-intern"></a>
### _STATUS_FEHLER_LESEN_INTERN

Auslesen der internen Fehlercodes und -zaehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FCODE_NR | int | Interner Fehlercode |
| STAT_FCNT1_NR | int | Interner Fehlerzaehler 1 |
| STAT_FCNT2_NR | int | Interner Fehlerzaehler 2 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
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
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (16 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [STAT_LENKSTOCK_WISCHER](#table-stat-lenkstock-wischer) (9 × 3)
- [STAT_MFL1](#table-stat-mfl1) (6 × 3)
- [STAT_MFL2](#table-stat-mfl2) (4 × 3)
- [STAT_LENKWINKEL](#table-stat-lenkwinkel) (5 × 3)
- [SG_ENCODERPOSITION](#table-sg-encoderposition) (242 × 2)
- [SG_MC2ANTWORT](#table-sg-mc2antwort) (14 × 2)

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

Dimensions: 16 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9E28 | SG interner Fehler |
| 0x9E29 | Lenkradwinkel |
| 0x9E2A | Lenkradwinkelgeschwindigkeit |
| 0x9E2C | Multifunktionslenkrad (MFL) - Timeout Telegramm |
| 0x9E2D | Multifunktionslenkrad (MFL) - Togglebitfehler |
| 0x9E2E | Multifunktionslenkrad (MFL) - Timeout Geraetestatus |
| 0x9E2F | PT-CAN Weckleitung - Plausibilitaetsfehler |
| 0x9E30 | Ueberspannung |
| 0x9E31 | Unterspannung |
| 0x9E32 | Flash-Download fuer MC-2 erforderlich |
| 0x9E33 | Nullpunktabgleich fuer Lenkwinkelsensor erforderlich |
| 0xC987 | Bus Kommunikationsfehler (PT-CAN) |
| 0xC98B | Bus Kommunikationsfehler (F-CAN) |
| 0xC994 | Botschaft (Klemmenstatus, 130h) |
| 0xC995 | Signal (ST_KL_15) |
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
| F_UWB_ERW | nein |

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

<a id="table-stat-lenkstock-wischer"></a>
### STAT_LENKSTOCK_WISCHER

Dimensions: 9 rows × 3 columns

| WERT | VSWERT | STATUS_TEXT |
| --- | --- | --- |
| 0x00 | 0 | Lenkstock Wischer in Nullstellung |
| 0x08 | 1 | Tippwischen betaetigt |
| 0x02 | 2 | Lenkstock Wischer in Stufe 1 betaetigt |
| 0x03 | 3 | Lenkstock Wischer in Stufe 2 betaetigt |
| 0x10 | 4 | Frontwaschen betaetigt |
| 0x01 | 5 | Lenkstock Wischer in Stellung Intervall |
| 0x40 | 6 | Heckwischen betaetigt |
| 0x80 | 7 | Heckwaschen betaetigt |
| 0x?? | 8 | Mehrfachbetaetigung |

<a id="table-stat-mfl1"></a>
### STAT_MFL1

Dimensions: 6 rows × 3 columns

| WERT | VSWERT | STATUS_TEXT |
| --- | --- | --- |
| 0x00 | 0 | Keine Betaetigung |
| 0x40 | 1 | Push to talk betaetigt |
| 0x08 | 2 | Volume/Lautstaerke plus betaetigt |
| 0x04 | 3 | Volume/Lautstaerke minus betaetigt |
| 0x01 | 4 | Telefontaste betaetigt |
| 0x?? | 5 | Mehrfachbetaetigung |

<a id="table-stat-mfl2"></a>
### STAT_MFL2

Dimensions: 4 rows × 3 columns

| WERT | VSWERT | STATUS_TEXT |
| --- | --- | --- |
| 0x00 | 0 | Keine Betaetigung |
| 0x20 | 3 | Suchlauf auf betaetigt |
| 0x10 | 4 | Suchlauf ab betaetigt |
| 0x?? | 5 | Mehrfachbetaetigung |

<a id="table-stat-lenkwinkel"></a>
### STAT_LENKWINKEL

Dimensions: 5 rows × 3 columns

| WERT | VSWERT | STATUS_TEXT |
| --- | --- | --- |
| 0x02 | 0 | Fehlerhaft |
| 0x00 | 1 | Absolut |
| 0x?? | 2 | Relativ |
| 0x03 | 3 | Ungueltig |
| 0xFF | 255 | Unbekannter Status |

<a id="table-sg-encoderposition"></a>
### SG_ENCODERPOSITION

Dimensions: 242 rows × 2 columns

| ENC_NR | ENC_TEXT |
| --- | --- |
| 0x0013 |  -21.0 Grad |
| 0x001B |  -22.5 Grad |
| 0x0026 | -129.0 Grad |
| 0x0027 | -130.5 Grad |
| 0x003B |  -24.0 Grad |
| 0x004C |   24.0 Grad |
| 0x004D |   22.5 Grad |
| 0x0067 | -132.0 Grad |
| 0x0082 |   -4.5 Grad |
| 0x008A |   -3.0 Grad |
| 0x00A2 |   -6.0 Grad |
| 0x00CD |   21.0 Grad |
| 0x0108 |    1.5 Grad |
| 0x010A |    0.0 Grad |
| 0x0135 |  -45.0 Grad |
| 0x0137 |  -43.5 Grad |
| 0x0139 |  -27.0 Grad |
| 0x013B |  -25.5 Grad |
| 0x0157 | -151.5 Grad |
| 0x015F | -153.0 Grad |
| 0x0175 |  -46.5 Grad |
| 0x017F | -154.5 Grad |
| 0x018A |   -1.5 Grad |
| 0x018C |  106.5 Grad |
| 0x0193 |  126.0 Grad |
| 0x0198 |  109.5 Grad |
| 0x019B |  127.5 Grad |
| 0x019C |  108.0 Grad |
| 0x01B3 |  124.5 Grad |
| 0x01B9 |  -28.5 Grad |
| 0x0201 |  -16.5 Grad |
| 0x0203 |  -18.0 Grad |
| 0x0213 |  -19.5 Grad |
| 0x0263 | -135.0 Grad |
| 0x0267 | -133.5 Grad |
| 0x026C | -108.0 Grad |
| 0x026E | -106.5 Grad |
| 0x0273 | -136.5 Grad |
| 0x0280 |   34.5 Grad |
| 0x02A0 |   36.0 Grad |
| 0x02A6 | -180.0 Grad |
| 0x02A8 |   37.5 Grad |
| 0x02AE | -178.5 Grad |
| 0x02E6 |  178.5 Grad |
| 0x02EC | -109.5 Grad |
| 0x0315 | -147.0 Grad |
| 0x0317 | -148.5 Grad |
| 0x0318 |  112.5 Grad |
| 0x0319 |  114.0 Grad |
| 0x0328 |   40.5 Grad |
| 0x032A |   42.0 Grad |
| 0x0357 | -150.0 Grad |
| 0x035D |  -51.0 Grad |
| 0x0375 |  -48.0 Grad |
| 0x037D |  -49.5 Grad |
| 0x0391 |  -33.0 Grad |
| 0x0398 |  111.0 Grad |
| 0x03A8 |   39.0 Grad |
| 0x03B1 |  -31.5 Grad |
| 0x03B7 |  -76.5 Grad |
| 0x03B9 |  -30.0 Grad |
| 0x03BF |  -75.0 Grad |
| 0x03F7 |  -78.0 Grad |
| 0x0402 | -124.5 Grad |
| 0x0406 | -126.0 Grad |
| 0x0426 | -127.5 Grad |
| 0x04C6 |  162.0 Grad |
| 0x04C9 |   18.0 Grad |
| 0x04CD |   19.5 Grad |
| 0x04CE |  163.5 Grad |
| 0x04D9 |   16.5 Grad |
| 0x04E6 |  160.5 Grad |
| 0x0519 |  132.0 Grad |
| 0x051B |  130.5 Grad |
| 0x057E | -157.5 Grad |
| 0x057F | -156.0 Grad |
| 0x059B |  129.0 Grad |
| 0x05D7 |  -58.5 Grad |
| 0x05DF |  -57.0 Grad |
| 0x05F7 |  -60.0 Grad |
| 0x05FE | -159.0 Grad |
| 0x062A | -174.0 Grad |
| 0x062E | -175.5 Grad |
| 0x0631 | -141.0 Grad |
| 0x064C |  168.0 Grad |
| 0x064E |  166.5 Grad |
| 0x0671 | -139.5 Grad |
| 0x0673 | -138.0 Grad |
| 0x067D |  148.5 Grad |
| 0x067F |  150.0 Grad |
| 0x06A2 |  -96.0 Grad |
| 0x06AE | -177.0 Grad |
| 0x06C4 | -114.0 Grad |
| 0x06CE |  165.0 Grad |
| 0x06E2 |  -94.5 Grad |
| 0x06E4 | -112.5 Grad |
| 0x06EA |  -93.0 Grad |
| 0x06EC | -111.0 Grad |
| 0x06FD |  147.0 Grad |
| 0x0715 | -145.5 Grad |
| 0x0731 | -142.5 Grad |
| 0x0735 | -144.0 Grad |
| 0x073B |  -70.5 Grad |
| 0x073F |  -72.0 Grad |
| 0x075D |  -52.5 Grad |
| 0x075F |  -54.0 Grad |
| 0x076A |  -90.0 Grad |
| 0x076E |  -88.5 Grad |
| 0x07BF |  -73.5 Grad |
| 0x07D5 |  142.5 Grad |
| 0x07DF |  -55.5 Grad |
| 0x07E6 | -163.5 Grad |
| 0x07EA |  -91.5 Grad |
| 0x07F5 |  144.0 Grad |
| 0x07F6 | -162.0 Grad |
| 0x07FD |  145.5 Grad |
| 0x07FE | -160.5 Grad |
| 0x0804 |   28.5 Grad |
| 0x080C |   27.0 Grad |
| 0x0820 |  -10.5 Grad |
| 0x084C |   25.5 Grad |
| 0x08A0 |   -9.0 Grad |
| 0x08A2 |   -7.5 Grad |
| 0x08AE |   64.5 Grad |
| 0x08AF |   63.0 Grad |
| 0x08CA |   99.0 Grad |
| 0x08CE |  100.5 Grad |
| 0x08EA |   97.5 Grad |
| 0x08EF |   61.5 Grad |
| 0x0908 |    3.0 Grad |
| 0x0910 |    6.0 Grad |
| 0x0913 |  -39.0 Grad |
| 0x0917 |  -40.5 Grad |
| 0x0918 |    4.5 Grad |
| 0x0931 |  120.0 Grad |
| 0x0937 |  -42.0 Grad |
| 0x098C |  105.0 Grad |
| 0x098E |  103.5 Grad |
| 0x09B1 |  121.5 Grad |
| 0x09B3 |  123.0 Grad |
| 0x09CE |  102.0 Grad |
| 0x0A01 |  -15.0 Grad |
| 0x0A04 |   30.0 Grad |
| 0x0A20 |  -12.0 Grad |
| 0x0A21 |  -13.5 Grad |
| 0x0A26 | -102.0 Grad |
| 0x0A2E | -103.5 Grad |
| 0x0A64 |  174.0 Grad |
| 0x0A6E | -105.0 Grad |
| 0x0A80 |   33.0 Grad |
| 0x0A84 |   31.5 Grad |
| 0x0ABD |   85.5 Grad |
| 0x0ABF |   87.0 Grad |
| 0x0AE4 |  175.5 Grad |
| 0x0AE6 |  177.0 Grad |
| 0x0AEB |   58.5 Grad |
| 0x0AEF |   60.0 Grad |
| 0x0AFB |   57.0 Grad |
| 0x0AFD |   84.0 Grad |
| 0x0B13 |  -37.5 Grad |
| 0x0B19 |  115.5 Grad |
| 0x0B2A |   43.5 Grad |
| 0x0B31 |  118.5 Grad |
| 0x0B32 |   46.5 Grad |
| 0x0B39 |  117.0 Grad |
| 0x0B3A |   45.0 Grad |
| 0x0B76 |  -82.5 Grad |
| 0x0B91 |  -34.5 Grad |
| 0x0B93 |  -36.0 Grad |
| 0x0BDC |   79.5 Grad |
| 0x0BF6 |  -81.0 Grad |
| 0x0BF7 |  -79.5 Grad |
| 0x0BFC |   81.0 Grad |
| 0x0BFD |   82.5 Grad |
| 0x0C02 | -123.0 Grad |
| 0x0C40 | -120.0 Grad |
| 0x0C42 | -121.5 Grad |
| 0x0C67 |  156.0 Grad |
| 0x0C8A |   69.0 Grad |
| 0x0C8E |   67.5 Grad |
| 0x0C91 |   12.0 Grad |
| 0x0CAB |   93.0 Grad |
| 0x0CAE |   66.0 Grad |
| 0x0CD1 |   13.5 Grad |
| 0x0CD9 |   15.0 Grad |
| 0x0CE6 |  159.0 Grad |
| 0x0CE7 |  157.5 Grad |
| 0x0CEA |   96.0 Grad |
| 0x0CEB |   94.5 Grad |
| 0x0D10 |    7.5 Grad |
| 0x0D19 |  133.5 Grad |
| 0x0D51 |  136.5 Grad |
| 0x0D59 |  135.0 Grad |
| 0x0D73 |  -64.5 Grad |
| 0x0D8A |   70.5 Grad |
| 0x0D90 |    9.0 Grad |
| 0x0D91 |   10.5 Grad |
| 0x0DC8 |   73.5 Grad |
| 0x0DCA |   72.0 Grad |
| 0x0DF3 |  -63.0 Grad |
| 0x0DF7 |  -61.5 Grad |
| 0x0E26 | -100.5 Grad |
| 0x0E2A | -172.5 Grad |
| 0x0E40 | -118.5 Grad |
| 0x0E4C |  169.5 Grad |
| 0x0E62 | -169.5 Grad |
| 0x0E64 |  172.5 Grad |
| 0x0E67 |  154.5 Grad |
| 0x0E6A | -171.0 Grad |
| 0x0E6C |  171.0 Grad |
| 0x0E6F |  153.0 Grad |
| 0x0E7F |  151.5 Grad |
| 0x0EA2 |  -97.5 Grad |
| 0x0EA6 |  -99.0 Grad |
| 0x0EAB |   91.5 Grad |
| 0x0EAF |   90.0 Grad |
| 0x0EB3 |   52.5 Grad |
| 0x0EBF |   88.5 Grad |
| 0x0EC0 | -117.0 Grad |
| 0x0EC4 | -115.5 Grad |
| 0x0EF3 |   54.0 Grad |
| 0x0EFB |   55.5 Grad |
| 0x0F32 |   48.0 Grad |
| 0x0F3B |  -69.0 Grad |
| 0x0F51 |  138.0 Grad |
| 0x0F62 | -168.0 Grad |
| 0x0F6E |  -87.0 Grad |
| 0x0F73 |  -66.0 Grad |
| 0x0F76 |  -84.0 Grad |
| 0x0F7B |  -67.5 Grad |
| 0x0F7E |  -85.5 Grad |
| 0x0FB2 |   49.5 Grad |
| 0x0FB3 |   51.0 Grad |
| 0x0FC8 |   75.0 Grad |
| 0x0FD1 |  139.5 Grad |
| 0x0FD5 |  141.0 Grad |
| 0x0FD8 |   76.5 Grad |
| 0x0FDC |   78.0 Grad |
| 0x0FE2 | -166.5 Grad |
| 0x0FE6 | -165.0 Grad |
| 0xFFFF | kein Wert vorhanden |
| 0x???? | ungueltiges Codewort |

<a id="table-sg-mc2antwort"></a>
### SG_MC2ANTWORT

Dimensions: 14 rows × 2 columns

| MC2_NR | MC2_TEXT |
| --- | --- |
| 0x00 | MC-2: OKAY |
| 0x01 | MC-2: Timeout beim Flash-Ablauf (1) |
| 0x02 | MC-2: Timeout beim Flash-Ablauf (2) |
| 0x03 | MC-2: Timeout beim Flash-Ablauf (3) |
| 0x04 | MC-2: Timeout beim Flash-Ablauf (4) |
| 0x05 | MC-2: Timeout beim Flash-Ablauf (5) |
| 0x06 | MC-2: Timeout beim Flash-Ablauf (6) |
| 0x07 | MC-2: Timeout beim Flash-Ablauf (7) |
| 0x08 | MC-2: Timeout beim Flash-Ablauf (8) |
| 0x80 | MC-2: Ungueltiger Flash-Service |
| 0x81 | MC-2: Ungueltiger Flash-Bereich |
| 0x82 | MC-2: Fehler im Flash-Ablauf |
| 0x83 | MC-2: Fehler bei Flash-Verifizierung |
| 0x?? | MC-2: Antwort unbekannt |
