# pdcr3.prg

- Jobs: [62](#jobs)
- Tables: [25](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | PDC |
| ORIGIN | BMW EI-612 Patrick_Matters |
| REVISION | 1.003 |
| AUTHOR | Valeo_Schalter_und_Sensoren_GmbH VUS Werner_Götte, Valeo_Schalt |
| COMMENT | N/A |
| PACKAGE | 1.45 |
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
- [STATUS_ABSTAND](#job-status-abstand) - Auslesen der Stati von errechnete Abstandsmessung KWP2000: $30 InputOutputControlByLocalIdentifier $07 Read Distances Modus  : Default
- [STATUS_AUSSCHWINGZEITEN](#job-status-ausschwingzeiten) - Auslesen der Ausschwingzeiten KWP2000: $30 InputOutputControlByLocalIdentifier $08 Read Attenuation time Modus  : Default
- [STATUS_BUS_NACHRICHTEN](#job-status-bus-nachrichten) - Liefert die Signale/Werte über BUS 22 22 0xD96B BUS_IN_TEMP_AUSSEN_WERT :0xD66E BUS_IN_PDC_TASTE_EIN :0xD240 BUS_IN_GESCHWINDIGKEIT_WERT :0xD66D BUS_IN_ANHAENGER_VORHANDEN :0xD67B BUS_IN_RUECKWAERTSGANG :0xD67A BUS_IN_WEGSTRECKE_WERT :0xD388 AKTIVIERUNGSIGNAL_PDC :0xD679 BUS_IN_STATUS_ROLLEN :0xD670 BUS_IN_KILOMETERSTAND_WERT
- [STATUS_FUNKTIONSANZEIGE](#job-status-funktionsanzeige) - Status der Funktionsanzeige KWP2000: $30 InputOutputControlByLocalIdentifier $0D Status LED Modus  : Default
- [STATUS_KLEMMEN](#job-status-klemmen) - Job zum Auslesen der Klemmensteuerung am Steuergerät. KWP2000: $30 InputOutputControlByLocalIdentifier $0C Read Clamp State Modus  : Default
- [STATUS_KONFIGURATION](#job-status-konfiguration) - KWP2000: $30 InputOutputControlByLocalIdentifier $0B Read Configuration Modus  : Default
- [STATUS_LAST_FUNCTION](#job-status-last-function) - Status Last Function LF KWP2000: $30 InputOutputControlByLocalIdentifier $0F Status LF Modus  : Default
- [STATUS_SENSORTEST](#job-status-sensortest) - Gibt den Status des Sensortests aus KWP2000: $30 InputOutputControlByLocalIdentifier $04 Status Sensortest Modus  : Default
- [STATUS_SYSTEM_PDC](#job-status-system-pdc) - Liefert den Status des Systems KWP2000: $30 InputOutputControlByLocalIdentifier $05 Status PDC Modus  : Default
- [STATUS_SENSORWEGE](#job-status-sensorwege) - Gibt die Signalwege der Ultraschallsensoren der PDC aus. KWP2000: $30 InputOutputControlByLocalIdentifier $06 Direkte Signalwege Modus  : Default
- [STEUERN_BUS_NACHRICHT](#job-steuern-bus-nachricht) - Ansteuerung zum Senden einer Aktivierungsnachricht für Parcslaves KWP2000: $30 InputOutputControlByLocalIdentifier $03 Steuern Bus Nachricht Modus  : Default
- [STEUERN_SENSORTEST](#job-steuern-sensortest) - Ansteuern des Sensortests KWP2000: $30 InputOutputControlByLocalIdentifier $01 Steuern Sensortest Modus  : Default
- [STEUERN_SYSTEM_PDC](#job-steuern-system-pdc) - Ansteuerung zum Senden einer Aktivierungsnachricht für PDC KWP2000: $30 InputOutputControlByLocalIdentifier $02 Steuern System PDC Modus  : Default
- [STATUS_INTERNE_SW_VERSION](#job-status-interne-sw-version) - Auslesen der Stati von errechnete Abstandsmessung KWP2000: $30 InputOutputControlByLocalIdentifier $0E Read internal SW-Version Modus  : Default

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

<a id="job-status-abstand"></a>
### STATUS_ABSTAND

Auslesen der Stati von errechnete Abstandsmessung KWP2000: $30 InputOutputControlByLocalIdentifier $07 Read Distances Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PDC_HAL_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HAL_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HZE_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HZE_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HML_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HML_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HMR_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HMR_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HAR_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HAR_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HSL_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HSL_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HSR_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_HSR_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VAL_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VAL_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VZE_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VZE_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VML_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VML_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VMR_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VMR_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VAR_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VAR_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VSL_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VSL_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VSR_ABSTAND_WERT | unsigned char | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| STAT_PDC_VSR_ABSTAND_EINH | string | Berechneter Abstand: 0 - 252, 253 = kein Objekt im Meßbereich 254 = kein Sensor verbaut 255 = Ungültig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ausschwingzeiten"></a>
### STATUS_AUSSCHWINGZEITEN

Auslesen der Ausschwingzeiten KWP2000: $30 InputOutputControlByLocalIdentifier $08 Read Attenuation time Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PDC_HAL_ASZ_WERT | unsigned int | Ausschwingzeit Sensor hinten außen links |
| STAT_PDC_HAL_ASZ_EINH | string | Ausschwingzeit Sensor hinten außen links |
| STAT_PDC_HZE_ASZ_WERT | unsigned int | Ausschwingzeit Sensor hinten zentral |
| STAT_PDC_HZE_ASZ_EINH | string | Ausschwingzeit Sensor hinten zentral |
| STAT_PDC_HML_ASZ_WERT | unsigned int | Ausschwingzeit Sensor hinten mitte links |
| STAT_PDC_HML_ASZ_EINH | string | Ausschwingzeit Sensor hinten mitte links |
| STAT_PDC_HMR_ASZ_WERT | unsigned int | Ausschwingzeit Sensor hinten mitte rechts |
| STAT_PDC_HMR_ASZ_EINH | string | Ausschwingzeit Sensor hinten mitte rechts |
| STAT_PDC_HAR_ASZ_WERT | unsigned int | Ausschwingzeit Sensor hinten außen rechts |
| STAT_PDC_HAR_ASZ_EINH | string | Ausschwingzeit Sensor hinten außen rechts |
| STAT_PDC_HSL_ASZ_WERT | unsigned int | Ausschwingzeit Sensor hinten seitlich links |
| STAT_PDC_HSL_ASZ_EINH | string | Ausschwingzeit Sensor hinten seitlich links |
| STAT_PDC_HSR_ASZ_WERT | unsigned int | Ausschwingzeit Sensor hinten seitlich rechts |
| STAT_PDC_HSR_ASZ_EINH | string | Ausschwingzeit Sensor hinten seitlich rechts |
| STAT_PDC_VAL_ASZ_WERT | unsigned int | Ausschwingzeit Sensor vorn außen links |
| STAT_PDC_VAL_ASZ_EINH | string | Ausschwingzeit Sensor vorn außen links |
| STAT_PDC_VZE_ASZ_WERT | unsigned int | Ausschwingzeit Sensor vorn zentral |
| STAT_PDC_VZE_ASZ_EINH | string | Ausschwingzeit Sensor vorn zentral |
| STAT_PDC_VML_ASZ_WERT | unsigned int | Ausschwingzeit Sensor vorn mitte links |
| STAT_PDC_VML_ASZ_EINH | string | Ausschwingzeit Sensor vorn mitte links |
| STAT_PDC_VMR_ASZ_WERT | unsigned int | Ausschwingzeit Sensor vorn mitte rechts |
| STAT_PDC_VMR_ASZ_EINH | string | Ausschwingzeit Sensor vorn mitte rechts |
| STAT_PDC_VAR_ASZ_WERT | unsigned int | Ausschwingzeit Sensor vorn außen rechts |
| STAT_PDC_VAR_ASZ_EINH | string | Ausschwingzeit Sensor vorn außen rechts |
| STAT_PDC_VSL_ASZ_WERT | unsigned int | Ausschwingzeit Sensor vorn seitlich links |
| STAT_PDC_VSL_ASZ_EINH | string | Ausschwingzeit Sensor vorn seitlich links |
| STAT_PDC_VSR_ASZ_WERT | unsigned int | Ausschwingzeit Sensor vorn seitlich rechts |
| STAT_PDC_VSR_ASZ_EINH | string | Ausschwingzeit Sensor vorn seitlich rechts |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bus-nachrichten"></a>
### STATUS_BUS_NACHRICHTEN

Liefert die Signale/Werte über BUS 22 22 0xD96B BUS_IN_TEMP_AUSSEN_WERT :0xD66E BUS_IN_PDC_TASTE_EIN :0xD240 BUS_IN_GESCHWINDIGKEIT_WERT :0xD66D BUS_IN_ANHAENGER_VORHANDEN :0xD67B BUS_IN_RUECKWAERTSGANG :0xD67A BUS_IN_WEGSTRECKE_WERT :0xD388 AKTIVIERUNGSIGNAL_PDC :0xD679 BUS_IN_STATUS_ROLLEN :0xD670 BUS_IN_KILOMETERSTAND_WERT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BUS_IN_TEMP_AUSSEN_WERT | unsigned int | Außentemperatur |
| STAT_BUS_IN_TEMP_AUSSEN_EINH | string | Außentemperatur |
| STAT_BUS_IN_PDC_TASTE_EIN | unsigned char | auslesen Status der PDC-Taste über Bus : 0 = AUS, 1 = EIN |
| STAT_BUS_IN_GESCHWINDIGKEIT_WERT | unsigned int | Signal Geschwindigkeit des Fahrzeugs über BUS |
| STAT_BUS_IN_GESCHWINDIGKEIT_EINH | string | Signal Geschwindigkeit des Fahrzeugs über BUS |
| STAT_BUS_IN_ANHAENGER_VORHANDEN | unsigned char | Status des Anhängers: 0 = Anhänger nicht vorhanden 1 = Anhänger vorhanden |
| STAT_BUS_IN_RUECKWAERTSGANG_EIN | unsigned char | Status des Rückwärtsgang: 0 = Rückwärtsgang nicht eingelegt 1 = Rückwärtsgang eingelegt |
| STAT_BUS_IN_WEGSTRECKE_WERT | unsigned int | Signal Wegstrecke des Fahrzeugs über BUS |
| STAT_BUS_IN_WEGSTRECKE_EINH | string | Signal Wegstrecke des Fahrzeugs über BUS |
| STAT_BUS_IN_PDC_EIN | unsigned char | Signal für De-/ Aktivierung PDC über BUS: 0 = nicht aktiviert, 1 = aktiviert |
| STAT_BUS_IN_TV_EIN | unsigned char | Signal für De-/ Aktivierung TV über BUS: 0 = nicht aktiviert, 1 = aktiviert |
| STAT_BUS_IN_RV_EIN | unsigned char | Signal für De-/ Aktivierung Rückfahrkamera über BUS: 0 = nicht aktiviert, 1 = aktiviert |
| STAT_BUS_IN_PMA_EIN | unsigned char | Signal für De-/ Aktivierung PMA über BUS: 0 = nicht aktiviert, 1 = aktiviert |
| STAT_BUS_IN_STATUS_ROLLEN | unsigned char | Status der Fahrzeugbewegung: 0 = Fahrzeug steht, 1 = Fahrzeug fährt vorwärts, 2 = Fahrzeug fährt rückwärts, 3 = Fahrzeug fährt, 255 ungültig |
| STAT_BUS_IN_STATUS_ROLLEN_TEXT | string | Status der Fahrzeugbewegung: 0 = Fahrzeug steht, 1 = Fahrzeug fährt vorwärts, 2 = Fahrzeug fährt rückwärts, 3 = Fahrzeug fährt, 255 ungültig |
| STAT_BUS_IN_KILOMETERSTAND_WERT | unsigned long | Signal Kilometerstand des Fahrzeugs über BUS |
| STAT_BUS_IN_KILOMETERSTAND_EINH | string | Signal Kilometerstand des Fahrzeugs über BUS |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-funktionsanzeige"></a>
### STATUS_FUNKTIONSANZEIGE

Status der Funktionsanzeige KWP2000: $30 InputOutputControlByLocalIdentifier $0D Status LED Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FUNKTIONSANZEIGE_PDC | unsigned char | Status der Funktionsanzeige:  0= AUS  1= EIN |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klemmen"></a>
### STATUS_KLEMMEN

Job zum Auslesen der Klemmensteuerung am Steuergerät. KWP2000: $30 InputOutputControlByLocalIdentifier $0C Read Clamp State Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_KLEMME_15_WERT | unsigned int | Spannungswert am Steuergerät an Klemme 15 (auf eine Nachkommastelle genau) |
| STAT_SPANNUNG_KLEMME_15_EINH | string | Spannungswert am Steuergerät an Klemme 15 (auf eine Nachkommastelle genau) |
| STAT_STATUS_KLEMME_15_EIN | unsigned int | Status Klemme 15 im Steuergerät: 0=AUS  1=EIN |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-konfiguration"></a>
### STATUS_KONFIGURATION

KWP2000: $30 InputOutputControlByLocalIdentifier $0B Read Configuration Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PDC_ANZAHL_LAUTSPRECHER_WERT | unsigned char | Anzahl der direkt am Steuergerät angeschlossenen Lautsprecher |
| STAT_PDC_ANZAHL_LAUTSPRECHER_EINH | string | Anzahl der direkt am Steuergerät angeschlossenen Lautsprecher |
| STAT_PDC_ANZAHL_SENSOREN_VORN_WERT | unsigned char | Anzahl der angeschlossenen PDC Sensoren vorn. |
| STAT_PDC_ANZAHL_SENSOREN_VORN_EINH | string | Anzahl der angeschlossenen PDC Sensoren vorn. |
| STAT_PDC_ANZAHL_SENSOREN_HINTEN_WERT | unsigned char | Anzahl der angeschlossenen PDC Sensoren hinten. |
| STAT_PDC_ANZAHL_SENSOREN_HINTEN_EINH | string | Anzahl der angeschlossenen PDC Sensoren hinten. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-last-function"></a>
### STATUS_LAST_FUNCTION

Status Last Function LF KWP2000: $30 InputOutputControlByLocalIdentifier $0F Status LF Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LF_PDC | unsigned char | Status Last Function LF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sensortest"></a>
### STATUS_SENSORTEST

Gibt den Status des Sensortests aus KWP2000: $30 InputOutputControlByLocalIdentifier $04 Status Sensortest Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PDC_SENSORTEST_NR | unsigned char | Ausgabe des Status des Sensortests: 0 = Test nicht angefordert oder abgeschlossen, 1 = Test läuft |
| STAT_PDC_SENSORTEST_NR_TEXT | string | Ausgabe des Status des Sensortests: 0 = Test nicht angefordert oder abgeschlossen, 1 = Test läuft |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-system-pdc"></a>
### STATUS_SYSTEM_PDC

Liefert den Status des Systems KWP2000: $30 InputOutputControlByLocalIdentifier $05 Status PDC Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PDC_SYSTEM | unsigned char | Status des Systems: 0 = PDC nicht aktiv, 1 = PDC ist aktiv, 2 = PDC hat Fehler erkannt |
| STAT_PDC_SYSTEM_TEXT | string | Status des Systems: 0 = PDC nicht aktiv, 1 = PDC ist aktiv, 2 = PDC hat Fehler erkannt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sensorwege"></a>
### STATUS_SENSORWEGE

Gibt die Signalwege der Ultraschallsensoren der PDC aus. KWP2000: $30 InputOutputControlByLocalIdentifier $06 Direkte Signalwege Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HSL_HSL_WERT | unsigned char | Signalwege der Wandler |
| STAT_HSL_HSL_EINH | string | Signalwege der Wandler |
| STAT_HSL_HAL_WERT | unsigned char | Signalwege der Wandler |
| STAT_HSL_HAL_EINH | string | Signalwege der Wandler |
| STAT_HAL_HSL_WERT | unsigned char | Signalwege der Wandler |
| STAT_HAL_HSL_EINH | string | Signalwege der Wandler |
| STAT_HAL_HAL_WERT | unsigned char | Signalwege der Wandler |
| STAT_HAL_HAL_EINH | string | Signalwege der Wandler |
| STAT_HAL_HML_WERT | unsigned char | Signalwege der Wandler |
| STAT_HAL_HML_EINH | string | Signalwege der Wandler |
| STAT_HML_HAL_WERT | unsigned char | Signalwege der Wandler |
| STAT_HML_HAL_EINH | string | Signalwege der Wandler |
| STAT_HML_HML_WERT | unsigned char | Signalwege der Wandler |
| STAT_HML_HML_EINH | string | Signalwege der Wandler |
| STAT_HML_HMR_WERT | unsigned char | Signalwege der Wandler |
| STAT_HML_HMR_EINH | string | Signalwege der Wandler |
| STAT_HMR_HML_WERT | unsigned char | Signalwege der Wandler |
| STAT_HMR_HML_EINH | string | Signalwege der Wandler |
| STAT_HMR_HMR_WERT | unsigned char | Signalwege der Wandler |
| STAT_HMR_HMR_EINH | string | Signalwege der Wandler |
| STAT_HMR_HAR_WERT | unsigned char | Signalwege der Wandler |
| STAT_HMR_HAR_EINH | string | Signalwege der Wandler |
| STAT_HAR_HMR_WERT | unsigned char | Signalwege der Wandler |
| STAT_HAR_HMR_EINH | string | Signalwege der Wandler |
| STAT_HAR_HAR_WERT | unsigned char | Signalwege der Wandler |
| STAT_HAR_HAR_EINH | string | Signalwege der Wandler |
| STAT_HAR_HSR_WERT | unsigned char | Signalwege der Wandler |
| STAT_HAR_HSR_EINH | string | Signalwege der Wandler |
| STAT_HSR_HAR_WERT | unsigned char | Signalwege der Wandler |
| STAT_HSR_HAR_EINH | string | Signalwege der Wandler |
| STAT_HSR_HSR_WERT | unsigned char | Signalwege der Wandler |
| STAT_HSR_HSR_EINH | string | Signalwege der Wandler |
| STAT_VSL_VSL_WERT | unsigned char | Signalwege der Wandler |
| STAT_VSL_VSL_EINH | string | Signalwege der Wandler |
| STAT_VSL_VAL_WERT | unsigned char | Signalwege der Wandler |
| STAT_VSL_VAL_EINH | string | Signalwege der Wandler |
| STAT_VAL_VSL_WERT | unsigned char | Signalwege der Wandler |
| STAT_VAL_VSL_EINH | string | Signalwege der Wandler |
| STAT_VAL_VAL_WERT | unsigned char | Signalwege der Wandler |
| STAT_VAL_VAL_EINH | string | Signalwege der Wandler |
| STAT_VAL_VML_WERT | unsigned char | Signalwege der Wandler |
| STAT_VAL_VML_EINH | string | Signalwege der Wandler |
| STAT_VML_VAL_WERT | unsigned char | Signalwege der Wandler |
| STAT_VML_VAL_EINH | string | Signalwege der Wandler |
| STAT_VML_VML_WERT | unsigned char | Signalwege der Wandler |
| STAT_VML_VML_EINH | string | Signalwege der Wandler |
| STAT_VML_VMR_WERT | unsigned char | Signalwege der Wandler |
| STAT_VML_VMR_EINH | string | Signalwege der Wandler |
| STAT_VMR_VML_WERT | unsigned char | Signalwege der Wandler |
| STAT_VMR_VML_EINH | string | Signalwege der Wandler |
| STAT_VMR_VMR_WERT | unsigned char | Signalwege der Wandler |
| STAT_VMR_VMR_EINH | string | Signalwege der Wandler |
| STAT_VMR_VAR_WERT | unsigned char | Signalwege der Wandler |
| STAT_VMR_VAR_EINH | string | Signalwege der Wandler |
| STAT_VAR_VMR_WERT | unsigned char | Signalwege der Wandler |
| STAT_VAR_VMR_EINH | string | Signalwege der Wandler |
| STAT_VAR_VAR_WERT | unsigned char | Signalwege der Wandler |
| STAT_VAR_VAR_EINH | string | Signalwege der Wandler |
| STAT_VAR_VSR_WERT | unsigned char | Signalwege der Wandler |
| STAT_VAR_VSR_EINH | string | Signalwege der Wandler |
| STAT_VSR_VAR_WERT | unsigned char | Signalwege der Wandler |
| STAT_VSR_VAR_EINH | string | Signalwege der Wandler |
| STAT_VSR_VSR_WERT | unsigned char | Signalwege der Wandler |
| STAT_VSR_VSR_EINH | string | Signalwege der Wandler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bus-nachricht"></a>
### STEUERN_BUS_NACHRICHT

Ansteuerung zum Senden einer Aktivierungsnachricht für Parcslaves KWP2000: $30 InputOutputControlByLocalIdentifier $03 Steuern Bus Nachricht Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTIVIERUNGSSIGNAL_PDC | unsigned char | Gibt an, wie das Aktivierungssignal für PDC simuliert werden soll: 0 = AUS 1 = EIN |
| AKTIVIERUNGSSIGNAL_TV | unsigned char | Gibt an, wie das Aktivierungssignal für TV simuliert werden soll: 0 = AUS 1 = EIN |
| AKTIVIERUNGSSIGNAL_RV | unsigned char | Gibt an, wie das Aktivierungssignal für Rückfahrkamera simuliert werden soll: 0 = AUS 1 = EIN |
| AKTIVIERUNGSSIGNAL_PMA | unsigned char | Gibt an, wie das Aktivierungssignal für PMA simuliert werden soll: 0 = AUS 1 = EIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sensortest"></a>
### STEUERN_SENSORTEST

Ansteuern des Sensortests KWP2000: $30 InputOutputControlByLocalIdentifier $01 Steuern Sensortest Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | unsigned char | Startet den Sensortest für die Ultraschallsensoren. 1 = Start |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-system-pdc"></a>
### STEUERN_SYSTEM_PDC

Ansteuerung zum Senden einer Aktivierungsnachricht für PDC KWP2000: $30 InputOutputControlByLocalIdentifier $02 Steuern System PDC Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | unsigned char | Ein-/Ausschalten des PDC-System: 0 = AUS = PDC nicht aktiv, 1 = EIN = PDC ist aktiv |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-interne-sw-version"></a>
### STATUS_INTERNE_SW_VERSION

Auslesen der Stati von errechnete Abstandsmessung KWP2000: $30 InputOutputControlByLocalIdentifier $0E Read internal SW-Version Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HAUPTZAEHLER_WERT | string | Gibt den Hauptzaehler der internen Softwareversion zurück |
| STAT_HAUPTZAEHLER_EINH | string | Gibt den Hauptzaehler der internen Softwareversion zurück |
| STAT_NEBENZAEHLER_WERT | string | Gibt den Nebenzaehler der internen Softwareversion zurück |
| STAT_NEBENZAEHLER_EINH | string | Gibt den Nebenzaehler der internen Softwareversion zurück |
| STAT_UNTERZAEHLER_WERT | string | Gibt den Unterzaehler der internen Softwareversion zurück |
| STAT_UNTERZAEHLER_EINH | string | Gibt den Unterzaehler der internen Softwareversion zurück |
| STAT_JAHR_WERT | string | Gibt das Jahr der internen Softwareversion zurück |
| STAT_JAHR_EINH | string | Gibt das Jahr der internen Softwareversion zurück |
| STAT_MONAT_WERT | string | Gibt den Monat der internen Softwareversion zurück |
| STAT_MONAT_EINH | string | Gibt den Monat der internen Softwareversion zurück |
| STAT_TAG_WERT | string | Gibt den Tag der internen Softwareversion zurück |
| STAT_TAG_EINH | string | Gibt den Tag der internen Softwareversion zurück |
| STAT_STUNDE_WERT | string | Gibt die Stunde der internen Softwareversion zurück |
| STAT_STUNDE_EINH | string | Gibt die Stunde der internen Softwareversion zurück |
| STAT_MINUTE_WERT | string | Gibt die Minute der internen Softwareversion zurück |
| STAT_MINUTE_EINH | string | Gibt die Minute der internen Softwareversion zurück |
| STAT_SEKUNDE_WERT | string | Gibt die Sekunde der internen Softwareversion zurück |
| STAT_SEKUNDE_EINH | string | Gibt die Sekunde der internen Softwareversion zurück |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (111 × 2)
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
- [FORTTEXTE](#table-forttexte) (140 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (2 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (108 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTTEXTE](#table-iumwelttexte) (2 × 9)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [TAB_PDC_SENSORTEST](#table-tab-pdc-sensortest) (2 × 2)
- [TAB_PDC_STATUS](#table-tab-pdc-status) (3 × 2)
- [TAB_PDC_ROLLEN](#table-tab-pdc-rollen) (5 × 2)

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

Dimensions: 111 rows × 2 columns

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
| 2 | KWP2000 |
| - | KWP2000* |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 140 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xAAE8 | VSM_EVENT_OPMODE |
| 0xAAE9 | CODING_EVENT_NOT_CODED |
| 0xAAEA | CODING_EVENT_TRANSACTION_FAILED |
| 0xAAEB | CODING_EVENT_SIGNATURE_ERROR |
| 0xAAEC | CODING_EVENT_WRONG_VEHICLE |
| 0xAAED | CODING_EVENT_INVALID_DATA |
| 0xAAEE | Interner Steuergerätefehler |
| 0xAAEF | Unterspannung erkannt |
| 0xAAF0 | Überspannung erkannt |
| 0xAAF1 | Spannungsversorgung Ultraschallsensoren: Kurzschluss zwischen Plus und Minus |
| 0xAAF2 | Ultraschallsensor hinten Seite links, Signalleitung: Kurzschluss nach Plus |
| 0xAAF3 | Ultraschallsensor hinten Seite links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAAF4 | Ultraschallsensor hinten Seite links: Sensor defekt (Ausschwingzeit) |
| 0xAAF5 | Ultraschallsensor hinten Seite links: Sensor defekt (Receivezweig) |
| 0xAAF6 | Ultraschallsensor hinten Seite links: Sensor antwortet nicht |
| 0xAAF7 | Ultraschallsensor hinten Seite links: Sensor defekt (Verify-Fehler) |
| 0xAAF8 | Ultraschallsensor hinten Außen links, Signalleitung: Kurzschluss nach Plus |
| 0xAAF9 | Ultraschallsensor hinten Außen links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAAFA | Ultraschallsensor hinten Außen links: Sensor defekt (Ausschwingzeit) |
| 0xAAFB | Ultraschallsensor hinten Außen links: Sensor defekt (Receivezweig) |
| 0xAAFC | Ultraschallsensor hinten Außen links: Sensor antwortet nicht |
| 0xAAFD | Ultraschallsensor hinten Außen links: Sensor defekt (Verify-Fehler) |
| 0xAAFE | Ultraschallsensor hinten Mitte links, Signalleitung: Kurzschluss nach Plus |
| 0xAAFF | Ultraschallsensor hinten Mitte links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB00 | Ultraschallsensor hinten Mitte links: Sensor defekt (Ausschwingzeit) |
| 0xAB01 | Ultraschallsensor hinten Mitte links: Sensor defekt (Receivezweig) |
| 0xAB02 | Ultraschallsensor hinten Mitte links: Sensor antwortet nicht |
| 0xAB03 | Ultraschallsensor hinten Mitte links: Sensor defekt (Verify-Fehler) |
| 0xAB04 | Ultraschallsensor hinten Mitte rechts, Signalleitung: Kurzschluss nach Plus |
| 0xAB05 | Ultraschallsensor hinten Mitte rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB06 | Ultraschallsensor hinten Mitte rechts: Sensor defekt (Ausschwingzeit) |
| 0xAB07 | Ultraschallsensor hinten Mitte rechts: Sensor defekt (Receivezweig) |
| 0xAB08 | Ultraschallsensor hinten Mitte rechts: Sensor antwortet nicht |
| 0xAB09 | Ultraschallsensor hinten Mitte rechts: Sensor defekt (Verify-Fehler) |
| 0xAB0A | Ultraschallsensor hinten Außen rechts, Signalleitung: Kurzschluss nach Plus |
| 0xAB0B | Ultraschallsensor hinten Außen rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB0C | Ultraschallsensor hinten Außen rechts: Sensor defekt (Ausschwingzeit) |
| 0xAB0D | Ultraschallsensor hinten Außen rechts: Sensor defekt (Receivezweig) |
| 0xAB0E | Ultraschallsensor hinten Außen rechts: Sensor antwortet nicht |
| 0xAB0F | Ultraschallsensor hinten Außen rechts: Sensor defekt (Verify-Fehler) |
| 0xAB10 | Ultraschallsensor hinten Seite rechts, Signalleitung: Kurzschluss nach Plus |
| 0xAB11 | Ultraschallsensor hinten Seite rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB12 | Ultraschallsensor hinten Seite rechts: Sensor defekt (Ausschwingzeit) |
| 0xAB13 | Ultraschallsensor hinten Seite rechts: Sensor defekt (Receivezweig) |
| 0xAB14 | Ultraschallsensor hinten Seite rechts: Sensor antwortet nicht |
| 0xAB15 | Ultraschallsensor hinten Seite rechts: Sensor defekt (Verify-Fehler) |
| 0xAB16 | Ultraschallsensor vorn Seite links, Signalleitung: Kurzschluss nach Plus |
| 0xAB17 | Ultraschallsensor vorn Seite links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB18 | Ultraschallsensor vorn Seite links: Sensor defekt (Ausschwingzeit) |
| 0xAB19 | Ultraschallsensor vorn Seite links: Sensor defekt (Receivezweig) |
| 0xAB1A | Ultraschallsensor vorn Seite links: Sensor antwortet nicht |
| 0xAB1B | Ultraschallsensor vorn Seite links: Sensor defekt (Verify-Fehler) |
| 0xAB1C | Ultraschallsensor vorn Außen links, Signalleitung: Kurzschluss nach Plus |
| 0xAB1D | Ultraschallsensor vorn Außen links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB1E | Ultraschallsensor vorn Außen links: Sensor defekt (Ausschwingzeit) |
| 0xAB1F | Ultraschallsensor vorn Außen links: Sensor defekt (Receivezweig) |
| 0xAB20 | Ultraschallsensor vorn Außen links: Sensor antwortet nicht |
| 0xAB21 | Ultraschallsensor vorn Außen links: Sensor defekt (Verify-Fehler) |
| 0xAB22 | Ultraschallsensor vorn Mitte links, Signalleitung: Kurzschluss nach Plus |
| 0xAB23 | Ultraschallsensor vorn Mitte links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB24 | Ultraschallsensor vorn Mitte links: Sensor defekt (Ausschwingzeit) |
| 0xAB25 | Ultraschallsensor vorn Mitte links: Sensor defekt (Receivezweig) |
| 0xAB26 | Ultraschallsensor vorn Mitte links: Sensor antwortet nicht |
| 0xAB27 | Ultraschallsensor vorn Mitte links: Sensor defekt (Verify-Fehler) |
| 0xAB28 | Ultraschallsensor vorn Mitte rechts, Signalleitung: Kurzschluss nach Plus |
| 0xAB29 | Ultraschallsensor vorn Mitte rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB2A | Ultraschallsensor vorn Mitte rechts: Sensor defekt (Ausschwingzeit) |
| 0xAB2B | Ultraschallsensor vorn Mitte rechts: Sensor defekt (Receivezweig) |
| 0xAB2C | Ultraschallsensor vorn Mitte rechts: Sensor antwortet nicht |
| 0xAB2D | Ultraschallsensor vorn Mitte rechts: Sensor defekt (Verify-Fehler) |
| 0xAB2E | Ultraschallsensor vorn Außen rechts, Signalleitung: Kurzschluss nach Plus |
| 0xAB2F | Ultraschallsensor vorn Außen rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB30 | Ultraschallsensor vorn Außen rechts: Sensor defekt (Ausschwingzeit) |
| 0xAB31 | Ultraschallsensor vorn Außen rechts: Sensor defekt (Receivezweig) |
| 0xAB32 | Ultraschallsensor vorn Außen rechts: Sensor antwortet nicht |
| 0xAB33 | Ultraschallsensor vorn Außen rechts: Sensor defekt (Verify-Fehler) |
| 0xAB34 | Ultraschallsensor vorn Seite rechts, Signalleitung: Kurzschluss nach Plus |
| 0xAB35 | Ultraschallsensor vorn Seite rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB36 | Ultraschallsensor vorn Seite rechts: Sensor defekt (Ausschwingzeit) |
| 0xAB37 | Ultraschallsensor vorn Seite rechts: Sensor defekt (Receivezweig) |
| 0xAB38 | Ultraschallsensor vorn Seite rechts: Sensor antwortet nicht |
| 0xAB39 | Ultraschallsensor vorn Seite rechts: Sensor defekt (Verify-Fehler) |
| 0xAB3A | Ultraschallsensor vorn Zentral, Signalleitung: Kurzschluss nach Plus |
| 0xAB3B | Ultraschallsensor vorn Zentral, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB3C | Ultraschallsensor vorn Zentral: Sensor defekt (Ausschwingzeit) |
| 0xAB3D | Ultraschallsensor vorn Zentral: Sensor defekt (Receivezweig) |
| 0xAB3E | Ultraschallsensor vorn Zentral: Sensor antwortet nicht |
| 0xAB3F | Ultraschallsensor vorn Zentral: Sensor defekt (Verify-Fehler) |
| 0xAB40 | Ultraschallsensor hinten Zentral, Signalleitung: Kurzschluss nach Plus |
| 0xAB41 | Ultraschallsensor hinten Zentral, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0xAB42 | Ultraschallsensor hinten Zentral: Sensor defekt (Ausschwingzeit) |
| 0xAB43 | Ultraschallsensor hinten Zentral: Sensor defekt (Receivezweig) |
| 0xAB44 | Ultraschallsensor hinten Zentral: Sensor antwortet nicht |
| 0xAB45 | Ultraschallsensor hinten Zentral: Sensor defekt (Verify-Fehler) |
| 0xAB46 | Akustische Abstandwarnung nicht möglich |
| 0xAB47 | TOP VIEW nicht verfügbar |
| 0xAB48 | REAR VIEW nicht verfügbar |
| 0xAB49 | Parkassistent nicht verfügbar |
| 0xAB4A | PDC aktiv ohne Aktivierung |
| 0xAB4B | TOP VIEW aktiv ohne Aktivierung |
| 0xAB4C | REAR VIEW aktiv ohne Aktivierung |
| 0xAB4D | Parkassistent aktiv ohne Aktivierung |
| 0xAB4E | Spannungsversorgung Ultraschallsensoren vorn: Kurzschluss zwischen Plus und Minus |
| 0xAB4F | Spannungsversorgung Ultraschallsensoren hinten: Kurzschluss zwischen Plus und Minus |
| 0xE207 | PT-CAN Control Module Bus OFF |
| 0xE214 | Botschaft (130h, Klemmenstatus): Ausfall |
| 0xE215 | Botschaft (317h, Bedienung_Taster_Einparkhilfen): Ausfall |
| 0xE216 | Botschaft (330h, Kilometerstand/Reichweite): Ausfall |
| 0xE217 | Botschaft (310h, Außentemperatur/Relativzeit): Ausfall |
| 0xE218 | Botschaft (379h, Status_Qualifier_Top-View): Ausfall |
| 0xE219 | Botschaft (37Ah, Status_Qualifier_Rear-View): Ausfall |
| 0xE21A | Botschaft (BAh, Getriebedaten): Ausfall |
| 0xE21B | Botschaft (3B0h, Status_Gang_Rückwärts): Ausfall |
| 0xE21C | Botschaft (1A6h, Wegstrecke): Ausfall |
| 0xE21D | Botschaft (2E4h, Status_Anhänger): Ausfall |
| 0xE21E | Botschaft (1A0h, Geschwindigkeit_PT-CAN): Ausfall |
| 0xE21F | Botschaft (379h, Status_Qualifier_Top-View): Alive-Zähler-Fehler |
| 0xE220 | Botschaft (37Ah, Status_Qualifier_Rear-View): Alive-Zähler-Fehler |
| 0xE221 | Botschaft (379h, Status_Qualifier_Top-View): Prüfsummenfehler |
| 0xE222 | Botschaft (37Ah, Status_Qualifier_Rear-View): Prüfsummenfehler |
| 0xE223 | Signal (1A0h) ungültig empfangen: Status_Fahrzeug_Fahrzustand |
| 0xE224 | Signal (3AEh) ungültig empfangen: Anfrage_Aktivierung_Funktion_Parken |
| 0xE225 | Signal (330h) ungültig empfangen: Wegstrecke_Kilometer |
| 0xE226 | Signal (1A6h) ungültig empfangen: Wegstrecke |
| 0xE227 | Signal (317h) ungültig empfangen: Bedienung_Taster_PDC |
| 0xE228 | Signal (37Ah) ungültig empfangen: Qualifier_Funktion_Rear-View |
| 0xE229 | Signal (379h) ungültig empfangen: Qualifier_Funktion_Top-View |
| 0xE22A | Signal (3B0h) ungültig empfangen: Status_Gang_Rückwärts |
| 0xE22B | Signal (BAh) ungültig empfangen: Status_Gang_Getriebe |
| 0xE22C | Signal (130h) ungültig empfangen: Status_Klemme_15 |
| 0xE22D | Signal (2E4h) ungültig empfangen: Status_Anhänger |
| 0xE22E | Signal (310h) ungültig empfangen: Temperatur_Außen |
| 0xE22F | Signal (1A0h) ungültig empfangen: Geschwindigkeit_Fahrzeug |
| 0xE230 | Signal (3A0h) ungültig empfangen: Status_Sperre_Fehlerspeicher_FZM |
| 0xE231 | Signal (379h) ungültig empfangen: Alive_Status_Qualifier_Top-View |
| 0xE232 | Signal (37Ah) ungültig empfangen: Alive_Status_Qualifier_Rear-View |
| 0xE233 | Signal (3AEh) ungültig empfangen: Anzeige_Menu |
| 0xE234 | Signal (38Ah) ungültig empfangen: Status_Anzeige_PDC_Akustisch |
| 0xE235 | Signal (2E4h) ungültig empfangen: Status_Position_AHV |
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

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 2 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4100 | Aussentemperatur | °C | - | unsigned char | - | 0,5 | - | -40 |
| 0x4103 | Batteriespannung | V | - | unsigned char | - | - | 12,6 | - |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 108 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9308 | NVM_E_WRITE_FAILED |
| 0x9309 | NVM_E_READ_FAILED |
| 0x930A | NVM_E_CONTROL_FAILED |
| 0x930B | NVM_E_ERASE_FAILED |
| 0x930C | NVM_E_WRITE_ALL_FAILED |
| 0x930D | NVM_E_WRONG_CONFIG_ID |
| 0x930E | NVM_E_READ_ALL_FAILED |
| 0x930F | PIA_E_IO_ERROR |
| 0x9310 | Unterspannung erkannt |
| 0x9311 | Überspannung erkannt |
| 0x9312 | Spannungsversorgung Ultraschallsensoren: Kurzschluss zwischen Plus und Minus |
| 0x9313 | Ultraschallsensor hinten Seite links, Signalleitung: Kurzschluss nach Plus |
| 0x9314 | Ultraschallsensor hinten Seite links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x9315 | Ultraschallsensor hinten Seite links: Sensor defekt (Ausschwingzeit) |
| 0x9316 | Ultraschallsensor hinten Seite links: Sensor defekt (Receivezweig) |
| 0x9317 | Ultraschallsensor hinten Seite links: Sensor antwortet nicht |
| 0x9318 | Ultraschallsensor hinten Seite links: Sensor defekt (Verify-Fehler) |
| 0x9319 | Ultraschallsensor hinten außen links, Signalleitung: Kurzschluss nach Plus |
| 0x931A | Ultraschallsensor hinten außen links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x931B | Ultraschallsensor hinten außen links: Sensor defekt (Ausschwingzeit) |
| 0x931C | Ultraschallsensor hinten außen links: Sensor defekt (Receivezweig) |
| 0x931D | Ultraschallsensor hinten außen links: Sensor antwortet nicht |
| 0x931E | Ultraschallsensor hinten außen links: Sensor defekt (Verify-Fehler) |
| 0x931F | Ultraschallsensor hinten Mitte links, Signalleitung: Kurzschluss nach Plus |
| 0x9320 | Ultraschallsensor hinten Mitte links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x9321 | Ultraschallsensor hinten Mitte links: Sensor defekt (Ausschwingzeit) |
| 0x9322 | Ultraschallsensor hinten Mitte links: Sensor defekt (Receivezweig) |
| 0x9323 | Ultraschallsensor hinten Mitte links: Sensor antwortet nicht |
| 0x9324 | Ultraschallsensor hinten Mitte links: Sensor defekt (Verify-Fehler) |
| 0x9325 | Ultraschallsensor hinten Mitte rechts, Signalleitung: Kurzschluss nach Plus |
| 0x9326 | Ultraschallsensor hinten Mitte rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x9327 | Ultraschallsensor hinten Mitte rechts: Sensor defekt (Ausschwingzeit) |
| 0x9328 | Ultraschallsensor hinten Mitte rechts: Sensor defekt (Receivezweig) |
| 0x9329 | Ultraschallsensor hinten Mitte rechts: Sensor antwortet nicht |
| 0x932A | Ultraschallsensor hinten Mitte rechts: Sensor defekt (Verify-Fehler) |
| 0x932B | Ultraschallsensor vorn Zentral, Signalleitung: Kurzschluss nach Plus |
| 0x932C | Ultraschallsensor vorn Zentral, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x932D | Ultraschallsensor vorn Zentral: Sensor defekt (Ausschwingzeit) |
| 0x932E | Ultraschallsensor vorn Zentral: Sensor defekt (Receivezweig) |
| 0x932F | Ultraschallsensor vorn Zentral: Sensor antwortet nicht |
| 0x9330 | Ultraschallsensor vorn Zentral: Sensor defekt (Verify-Fehler) |
| 0x9331 | Ultraschallsensor hinten außen rechts, Signalleitung: Kurzschluss nach Plus |
| 0x9332 | Ultraschallsensor hinten außen rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x9333 | Ultraschallsensor hinten außen rechts: Sensor defekt (Ausschwingzeit) |
| 0x9334 | Ultraschallsensor hinten außen rechts: Sensor defekt (Receivezweig) |
| 0x9335 | Ultraschallsensor hinten außen rechts: Sensor antwortet nicht |
| 0x9336 | Ultraschallsensor hinten außen rechts: Sensor defekt (Verify-Fehler) |
| 0x9337 | Ultraschallsensor hinten Seite rechts, Signalleitung: Kurzschluss nach Plus |
| 0x9338 | Ultraschallsensor hinten Seite rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x9339 | Ultraschallsensor hinten Seite rechts: Sensor defekt (Ausschwingzeit) |
| 0x933A | Ultraschallsensor hinten Seite rechts: Sensor defekt (Receivezweig) |
| 0x933B | Ultraschallsensor hinten Seite rechts: Sensor antwortet nicht |
| 0x933C | Ultraschallsensor hinten Seite rechts: Sensor defekt (Verify-Fehler) |
| 0x933D | Ultraschallsensor vorn Seite links, Signalleitung: Kurzschluss nach Plus |
| 0x933E | Ultraschallsensor vorn Seite links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x933F | Ultraschallsensor vorn Seite links: Sensor defekt (Ausschwingzeit) |
| 0x9340 | Ultraschallsensor vorn Seite links: Sensor defekt (Receivezweig) |
| 0x9341 | Ultraschallsensor vorn Seite links: Sensor antwortet nicht |
| 0x9342 | Ultraschallsensor vorn Seite links: Sensor defekt (Verify-Fehler) |
| 0x9343 | Ultraschallsensor vorn außen links, Signalleitung: Kurzschluss nach Plus |
| 0x9344 | Ultraschallsensor vorn außen links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x9345 | Ultraschallsensor vorn außen links: Sensor defekt (Ausschwingzeit) |
| 0x9346 | Ultraschallsensor vorn außen links: Sensor defekt (Receivezweig) |
| 0x9347 | Ultraschallsensor vorn außen links: Sensor antwortet nicht |
| 0x9348 | Ultraschallsensor vorn außen links: Sensor defekt (Verify-Fehler) |
| 0x9349 | Ultraschallsensor vorn Mitte links, Signalleitung: Kurzschluss nach Plus |
| 0x934A | Ultraschallsensor vorn Mitte links, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x934B | Ultraschallsensor vorn Mitte links: Sensor defekt (Ausschwingzeit) |
| 0x934C | Ultraschallsensor vorn Mitte links: Sensor defekt (Receivezweig) |
| 0x934D | Ultraschallsensor vorn Mitte links: Sensor antwortet nicht |
| 0x934E | Ultraschallsensor vorn Mitte links: Sensor defekt (Verify-Fehler) |
| 0x934F | Ultraschallsensor vorn Mitte rechts, Signalleitung: Kurzschluss nach Plus |
| 0x9350 | Ultraschallsensor vorn Mitte rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x9351 | Ultraschallsensor vorn Mitte rechts: Sensor defekt (Ausschwingzeit) |
| 0x9352 | Ultraschallsensor vorn Mitte rechts: Sensor defekt (Receivezweig) |
| 0x9353 | Ultraschallsensor vorn Mitte rechts: Sensor antwortet nicht |
| 0x9354 | Ultraschallsensor vorn Mitte rechts: Sensor defekt (Verify-Fehler) |
| 0x9355 | Ultraschallsensor hinten Zentral, Signalleitung: Kurzschluss nach Plus |
| 0x9356 | Ultraschallsensor hinten Zentral, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x9357 | Ultraschallsensor hinten Zentral: Sensor defekt (Ausschwingzeit) |
| 0x9358 | Ultraschallsensor hinten Zentral: Sensor defekt (Receivezweig) |
| 0x9359 | Ultraschallsensor hinten Zentral: Sensor antwortet nicht |
| 0x935A | Ultraschallsensor hinten Zentral: Sensor defekt (Verify-Fehler) |
| 0x935B | Ultraschallsensor vorn außen rechts, Signalleitung: Kurzschluss nach Plus |
| 0x935C | Ultraschallsensor vorn außen rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x935D | Ultraschallsensor vorn außen rechts: Sensor defekt (Ausschwingzeit) |
| 0x935E | Ultraschallsensor vorn außen rechts: Sensor defekt (Receivezweig) |
| 0x935F | Ultraschallsensor vorn außen rechts: Sensor antwortet nicht |
| 0x9360 | Ultraschallsensor vorn außen rechts: Sensor defekt (Verify-Fehler) |
| 0x9361 | Ultraschallsensor vorn Seite rechts, Signalleitung: Kurzschluss nach Plus |
| 0x9362 | Ultraschallsensor vorn Seite rechts, Signalleitung: Kurzschluss nach Masse oder Unterbrechung |
| 0x9363 | Ultraschallsensor vorn Seite rechts: Sensor defekt (Ausschwingzeit) |
| 0x9364 | Ultraschallsensor vorn Seite rechts: Sensor defekt (Receivezweig) |
| 0x9365 | Ultraschallsensor vorn Seite rechts: Sensor antwortet nicht |
| 0x9366 | Ultraschallsensor vorn Seite rechts: Sensor defekt (Verify-Fehler) |
| 0x9367 | PDC nicht verfügbar |
| 0x9368 | TOP VIEW nicht verfügbar |
| 0x9369 | REAR VIEW nicht verfügbar |
| 0x936A | Parkassistent nicht verfügbar |
| 0x936B | PDC aktiv ohne Aktivierung |
| 0x936C | TOP VIEW aktiv ohne Aktivierung |
| 0x936D | REAR VIEW aktiv ohne Aktivierung |
| 0x936E | Parkassistent aktiv ohne Aktivierung |
| 0x936F | Akustische Abstandwarnung nicht möglich |
| 0x9370 | Botschaft (3A0h, Fahrzeugzustand): Ausfall |
| 0x9371 | Spannungsversorgung Ultraschallsensoren vorn: Kurzschluss zwischen Plus und Minus |
| 0x9372 | Spannungsversorgung Ultraschallsensoren hinten: Kurzschluss zwischen Plus und Minus |
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

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 2 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4100 | Aussentemperatur | °C | - | unsigned char | - | 0,5 | - | -40 |
| 0x4103 | Batteriespannung | V | - | unsigned char | - | - | 12,6 | - |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x4100 | 0x4103 | - | - |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x4100 | 0x4103 | - | - |

<a id="table-tab-pdc-sensortest"></a>
### TAB_PDC_SENSORTEST

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test nicht angefordert oder abgeschlossen |
| 0x01 | Test läuft |

<a id="table-tab-pdc-status"></a>
### TAB_PDC_STATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | PDC nicht aktiv |
| 0x01 | PDC aktiv |
| 0x02 | PDC hat Fehler erkannt |

<a id="table-tab-pdc-rollen"></a>
### TAB_PDC_ROLLEN

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Fahrzeug steht |
| 0x01 | Fahrzeug fährt vorwärts |
| 0x02 | Fahrzeug fährt rückwärts |
| 0x03 | Fahrzeug fährt |
| 0xFF | ungültiger Wert |
