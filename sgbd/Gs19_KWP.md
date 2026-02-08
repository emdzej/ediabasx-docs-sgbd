# Gs19_KWP.prg

- Jobs: [71](#jobs)
- Tables: [26](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | GS19.0 C Muster |
| ORIGIN | BMW EA-71 Burkhardt |
| REVISION | 0.08 |
| AUTHOR | BMW EA-71 Burkhardt |
| COMMENT | @SGBD fuer I5 K-Line EGS@ |
| PACKAGE | 0.12 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
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
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [STATUS_GETRIEBETEMPERATUR](#job-status-getriebetemperatur) - Auslesen der Getriebetemperatur KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Auslesen der Motortemperatur KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_FAHRPEDALWINKEL](#job-status-fahrpedalwinkel) - Auslesen des Fahrpedalwinkels KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_ABTRIEBSDREHZAHL](#job-status-abtriebsdrehzahl) - Auslesen der Abtriebsdrehzahl KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_TURBINENDREHZAHL](#job-status-turbinendrehzahl) - Auslesen der Turbinendrehzahl KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Auslesen der Motordrehzahl KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_RADGESCHWINDIGKEITEN](#job-status-radgeschwindigkeiten) - Auslesen der mittleren Radgeschwindigkeiten KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_MOTORISTMOMENT](#job-status-motoristmoment) - Auslesen des Motoristmoments KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_MOTORSOLLMOMENT](#job-status-motorsollmoment) - Auslesen des Motorsollmoments KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_ISTGANG](#job-status-istgang) - Auslesen des ISTGANGS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_WK](#job-status-wk) - Auslesen des Wandlerkupplung KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_BATTERIESPANNUNG](#job-status-batteriespannung) - Auslesen der Batteriespannung KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_DR_MV_SPANNUNG](#job-status-dr-mv-spannung) - Auslesen des DR/MV Versorgungsspannung KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_MAGNETVENTILE](#job-status-magnetventile) - Auslesen des Sollzustandes der MV KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_INPUTPEGEL](#job-status-inputpegel) - Auslesen der Inputpegel KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_SIGNAL_0](#job-status-signal-0) - Auslesen der Signalstati 0 KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_SIGNAL_1](#job-status-signal-1) - Auslesen der Signalstati 1 KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_SIGNAL_2](#job-status-signal-2) - Auslesen der Signalstati 2 KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_SIGNAL_3](#job-status-signal-3) - Auslesen der Signalstati 3 KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_GEAR](#job-status-gear) - Auslesen Status Wandlerkupplung Schaltart KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_STEPTRONIC](#job-status-steptronic) - Auslesen Zustand der aktuellen Steptronictaster KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_WH_POSITION](#job-status-wh-position) - Auslesen Status aktuelle Waehlhebelposition KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_GETRIEBEPOSITION](#job-status-getriebeposition) - Auslesen  aktuelle Getriebeposition KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_AGS](#job-status-ags) - Auslesen  AGS Schaltdiagramm/Kurvenfahrt KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_ERSATZPROGRAMME_3](#job-status-ersatzprogramme-3) - Auslesen  der aktiven Ersatzprogramme im EGS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_ERSATZPROGRAMME_2](#job-status-ersatzprogramme-2) - Auslesen  der aktiven Ersatzprogramme im EGS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_ERSATZPROGRAMME_1](#job-status-ersatzprogramme-1) - Auslesen  der aktiven Ersatzprogramme im EGS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_ERSATZPROGRAMME_0](#job-status-ersatzprogramme-0) - Auslesen  der aktiven Ersatzprogramme im EGS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_IO_LESEN](#job-status-io-lesen) - Auslesen aller Messwerte 0x01..0x7E KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [RESET_EGS](#job-reset-egs) - EGS fuehrt Reset aus KWP2000: $11 EcuResetService Modus  : Default
- [AIF_AKTUELL_LESEN](#job-aif-aktuell-lesen) - aktuelles Anwenderinfofeld lesen KWP2000: $1A ReadEcuIdentification Modus  : Default
- [AUSLESEN_PHYSICAL_ECU_HW_NR](#job-auslesen-physical-ecu-hw-nr) - Auslesen der PHYSICAL_ECU_HW_NR KWP2000: $1A ReadEcuIdentification Modus  : Default
- [AUSLESEN_SYSTEM_SUPPLIER_ECU_SERIAL_NR](#job-auslesen-system-supplier-ecu-serial-nr) - Auslesen der SYSTEM_SUPPLIER_ECU_SERIAL_NR KWP2000: $1A ReadEcuIdentification Modus  : Default
- [AUSLESEN_SW_STAND_ENTWICKLUNG](#job-auslesen-sw-stand-entwicklung) - Auslesen der SYSTEM_SUPPLIER_ECU_SOFTWARE_VERSION_NR KWP2000: $1A ReadEcuIdentification Modus  : Default
- [AUSLESEN_SYSTEM_SUPPLIER_ECU_HW_NR](#job-auslesen-system-supplier-ecu-hw-nr) - Auslesen der SYSTEM_SUPPLIER_ECU_HW_NR KWP2000: $1A ReadEcuIdentification Modus  : Default
- [GANGANZEIGE_STARTEN](#job-ganganzeige-starten) - Anzeige Gang im Kombi KWP2000: $31 StartRoutineByLocalIdentifier Modus  : Default
- [GANGANZEIGE_STOPPEN](#job-ganganzeige-stoppen) - Anzeige Gang im Kombi beenden KWP2000: $32 StopRoutineByLocalIdentifier Modus  : Default
- [BACKUPFEHLERSPEICHER_LESEN](#job-backupfehlerspeicher-lesen) - Backup-Fehlerspeicher lesen KWP2000:  ReadDataByLocalIdentifier Modus  : Default
- [STEUERN_SIGNAL_STELLGLIED](#job-steuern-signal-stellglied) - Status setzen der Signale/Stellglieder KWP2000: $30 InputOutputControlByLocalIdentifier Modus  : Default
- [STATUS_SIGNAL_STELLGLIED](#job-status-signal-stellglied) - Auslesen Status der Signale/Stellglieder KWP2000: $30 InputOutputControlByLocalIdentifier Modus  : Default
- [SEKUNDAERFEHLERSPEICHER_LESEN_1](#job-sekundaerfehlerspeicher-lesen-1) - Auslesen Sekundaerfehlerspeicher KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [SEKUNDAERFEHLERSPEICHER_LESEN_2](#job-sekundaerfehlerspeicher-lesen-2) - Auslesen Sekundaerfehlerspeicher KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [ADAPTIONSWERTE_LESEN_FLARE](#job-adaptionswerte-lesen-flare) - Auslesen der Adaptionswerte Flare KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [ADAPTIONSWERTE_LESEN_GLUE](#job-adaptionswerte-lesen-glue) - Auslesen der Adaptionswerte GLUE KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [ADAPTIONSWERTE_LESEN_GLS](#job-adaptionswerte-lesen-gls) - Auslesen der Adaptionswerte GLS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [ADAPTIONSWERTE_LESEN_SLZ](#job-adaptionswerte-lesen-slz) - Auslesen der Adaptionswerte SLZ KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [ADAPTIONSWERTE_LESEN_SF](#job-adaptionswerte-lesen-sf) - Auslesen der Adaptionswerte SF KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [ADAPTIONSWERTE_LESEN_PF](#job-adaptionswerte-lesen-pf) - Auslesen der Adaptionswerte PF KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [ADAPTIONSWERTE_LESEN_GWK](#job-adaptionswerte-lesen-gwk) - Auslesen der Adaptionswerte GWK KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [ADAPTIONSWERTE_LESEN_SBC](#job-adaptionswerte-lesen-sbc) - Auslesen der Adaptionswerte SBC KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [ADAPTIONSWERTE_RUECKSETZEN](#job-adaptionswerte-ruecksetzen) - alle Adaptionswerte ruecksetzen KWP2000: $31 StartRoutineByLocalIdentifier Modus  : Default
- [QUICKTEST](#job-quicktest) - Anzahl Fehler / Kilometerstand KWP2000: $31 StartRoutineByLocalIdentifier Modus  : Default
- [EGS_DIAGNOSE_TESTJOB](#job-egs-diagnose-testjob) - Job fuer EGS Diagnosetest KWP2000: Modus  : Default
- [HARDWARE_REFERENZ_LESEN](#job-hardware-referenz-lesen) - BRIF Inhalt ausgeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [PROGRAMM_REFERENZ_LESEN](#job-programm-referenz-lesen) - ZIF Inhalt ausgeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [DATEN_REFERENZ_LESEN](#job-daten-referenz-lesen) - DIF Inhalt ausgeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

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
| ECU | string | Steuergeraet im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| PACKAGE | string | Include-Paket-Nummer |
| SPRACHE | string | deutsch, english |

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
| F_ORT_NR | int | Index fuer Fehlerort |
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
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
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

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

<a id="job-status-getriebetemperatur"></a>
### STATUS_GETRIEBETEMPERATUR

Auslesen der Getriebetemperatur KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GETRIEBETEMPERATUR_WERT | real | Getriebeoeltemperatur Bereich: -40 bis 215 |
| STAT_GETRIEBETEMPERATUR_EINH | string | Grad C |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Auslesen der Motortemperatur KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOTORTEMPERATUR_WERT | real | Motortemperatur Bereich: -48 bis 207 |
| STAT_MOTORTEMPERATUR_EINH | string | Grad C |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrpedalwinkel"></a>
### STATUS_FAHRPEDALWINKEL

Auslesen des Fahrpedalwinkels KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FAHRPEDALWINKEL_WERT | real | Fahrpedalwinkel Bereich: 0% bis 100% |
| STAT_FAHRPEDALWINKEL_EINH | string | Prozent |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-abtriebsdrehzahl"></a>
### STATUS_ABTRIEBSDREHZAHL

Auslesen der Abtriebsdrehzahl KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ABTRIEBSDREHZAHL_WERT | real | Abtriebsdrehzahl Bereich: 0 bis 8160 |
| STAT_ABTRIEBSDREHZAHL_EINH | string | U/min |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-turbinendrehzahl"></a>
### STATUS_TURBINENDREHZAHL

Auslesen der Turbinendrehzahl KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TURBINENDREHZAHL_WERT | real | Turbinendrehzahl Bereich: 0 bis 8160 |
| STAT_TURBINENDREHZAHL_EINH | string | U/min |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Auslesen der Motordrehzahl KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOTORDREHZAHL_WERT | real | Motordrehzahl Bereich: 0 bis 8160 |
| STAT_MOTORDREHZAHL_EINH | string | U/min |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-radgeschwindigkeiten"></a>
### STATUS_RADGESCHWINDIGKEITEN

Auslesen der mittleren Radgeschwindigkeiten KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RADGESCHWINDIGKEITEN_WERT | real | Radgeschwindigkeiten Bereich: 0 bis 510 |
| STAT_RADGESCHWINDIGKEITEN_EINH | string | km/h |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motoristmoment"></a>
### STATUS_MOTORISTMOMENT

Auslesen des Motoristmoments KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOTORISTMOMENT_WERT | real | Motoristmoment Bereich: -100 bis 916 |
| STAT_MOTORISTMOMENT_EINH | string | Nm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motorsollmoment"></a>
### STATUS_MOTORSOLLMOMENT

Auslesen des Motorsollmoments KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOTORSOLLMOMENT_WERT | real | Motorsollmoment Bereich: -100 bis 916 |
| STAT_MOTORSOLLMOMENT_EINH | string | Nm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-istgang"></a>
### STATUS_ISTGANG

Auslesen des ISTGANGS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ISTGANG_WERT | string | Istgang Bereich:1...6 Gang, 7 = R |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wk"></a>
### STATUS_WK

Auslesen des Wandlerkupplung KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WK_WERT | string | Wandlerkupplung Bereich:0...2 0=offen 1=geregelt 2=geschlossen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-batteriespannung"></a>
### STATUS_BATTERIESPANNUNG

Auslesen der Batteriespannung KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BATTERIESPANNUNG_WERT | real | Batteriespannung Bereich: 0 bis 20,4 |
| STAT_BATTERIESPANNUNG_EINH | string | Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dr-mv-spannung"></a>
### STATUS_DR_MV_SPANNUNG

Auslesen des DR/MV Versorgungsspannung KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DR_MV_SPANNUNG_WERT | real | DR/MV Versorgungsspannung Bereich: 0 bis 20,4 |
| STAT_DR_MV_SPANNUNG_EINH | string | Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-magnetventile"></a>
### STATUS_MAGNETVENTILE

Auslesen des Sollzustandes der MV KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MV1_WERT | string | Sollzustand MV1 Bereich: 0=aus  1=an |
| STAT_MV2_WERT | string | Sollzustand MV2 Bereich: 0=aus  1=an |
| STAT_MV3_WERT | string | Sollzustand MV3 Bereich: Peek/hold |
| STAT_MV4_WERT | string | Sollzustand MV4 Bereich: 0=aus  1=an |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-inputpegel"></a>
### STATUS_INPUTPEGEL

Auslesen der Inputpegel KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PEGEL_L1_WERT | string | Pegel L1 Pin Bereich: 0=low  1=high |
| STAT_PEGEL_L2_WERT | string | Pegel L2 Pin Bereich: 0=low  1=high |
| STAT_PEGEL_L3_WERT | string | Pegel L3 Pin Bereich: 0=low  1=high |
| STAT_PEGEL_L4_WERT | string | Pegel L4 Pin Bereich: 0=low  1=high |
| STAT_PEGEL_TIP_PLUS_WERT | string | Pegel Tip+ Pin Bereich: 0=low  1=high |
| STAT_PEGEL_TIP_MINUS_WERT | string | Pegel Tip- Pin Bereich: 0=low  1=high |
| STAT_PEGEL_M_GASSE_WERT | string | Pegel M-Gasse Pin Bereich: 0=low  1=high |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-signal-0"></a>
### STATUS_SIGNAL_0

Auslesen der Signalstati 0 KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SIGNAL_SUBSTRATTEMPERATUR_WERT | string | Signalsstatus Substrattemperatursensor Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_GETRIEBEOELTEMPERATUR_WERT | string | Signalsstatus Getriebeoeltemperatur Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_PARKSPERRENSENSOR_WERT | string | Status Parksperrensensor Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_POSITIONSSENOR_WERT | string | Status Positionssensor Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_TURNBINENDREHZAHL_WERT | string | Status Turbinendrehzahl Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_ABTRIEBSDREHZAHL_WERT | string | Status Abtriebsdrehzahl Bereich: 0=in Ordnung 1=nicht in Ordnung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-signal-1"></a>
### STATUS_SIGNAL_1

Auslesen der Signalstati 1 KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SIGNAL_MOTORDREHZAHL_WERT | string | Signalsstatus Motordrehzahl Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_DROSSELKLAPPE_WERT | string | Status Drosselklappe/Fahrpedal Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_PARKSPERRENANFORDERUNG_WERT | string | Status Parksperrenanforderung DME Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_MOMENT1_WERT | string | Status Momententenschnittstelle DME EGS Bereich: 0=in Ordnung 1=nicht in Ordnung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-signal-2"></a>
### STATUS_SIGNAL_2

Auslesen der Signalstati 2 KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SIGNAL_BREMSSIGNAL_WERT | string | Signalsstatus Bremssignal Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_DREHRICHTUNG_WERT | string | Signalstatus Drehrichtungserkennung Rad Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_RADGESCHWINDIGKEIT_HL_WERT | string | Status Radgeschwindigkeit HL Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_RADGESCHWINDIGKEIT_HR_WERT | string | Status Radgeschwindigkeit HR Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_RADGESCHWINDIGKEIT_VL_WERT | string | Status Radgeschwindigkeit VL Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_RADGESCHWINDIGKEIT_VR_WERT | string | Status Radgeschwindigkeit VR Bereich: 0=in Ordnung 1=nicht in Ordnung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-signal-3"></a>
### STATUS_SIGNAL_3

Auslesen der Signalstati 3 KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SIGNAL_S_TASTER_WERT | string | Signalsstatus S-Taster Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_TIP_TASTER_WERT | string | Status Tip-Taster Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_POS_SERIELL_WERT | string | Status SZL WH-Positionsinformation ueber serielle Leitung Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_POS_CAN_WERT | string | Status SZL WH-Positionsinformation ueber CAN Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_FAHRERTUER_WERT | string | Status Fahrertuer Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_FAHRERSITZ_WERT | string | Status Fahrersitz Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_SCHLUESSEL_STECKT_WERT | string | Status Schluessel steckt Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_KL15_WERT | string | Status Klemme 15 CAN Bereich: 0=in Ordnung 1=nicht in Ordnung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gear"></a>
### STATUS_GEAR

Auslesen Status Wandlerkupplung Schaltart KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WK_WERT | string | WK Bereich:0...2 0=offen 1=geregelt 2=geschlossen |
| STAT_SA_WERT | string | Schaltart Bereich:0...25 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-steptronic"></a>
### STATUS_STEPTRONIC

Auslesen Zustand der aktuellen Steptronictaster KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TIP_PLUS_LINKS | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_TIP_MINUS_LINKS | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_TIP_PLUS_RECHTS | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_TIP_MINUS_RECHTS | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_S_TASTER | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_P_TASTER | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_BREMSE_GETRETEN | string | Bremse betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wh-position"></a>
### STATUS_WH_POSITION

Auslesen Status aktuelle Waehlhebelposition KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WH_POSITION | string | WH-Position Bereich:0...12 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-getriebeposition"></a>
### STATUS_GETRIEBEPOSITION

Auslesen  aktuelle Getriebeposition KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GETRIEBEPOSITION | string | Getriebeposition Bereich:6...9 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ags"></a>
### STATUS_AGS

Auslesen  AGS Schaltdiagramm/Kurvenfahrt KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHALTDIAGRAMM_AGS | string | Schaltdiagramm AGS Bereich:0b0000...0b1111 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ersatzprogramme-3"></a>
### STATUS_ERSATZPROGRAMME_3

Auslesen  der aktiven Ersatzprogramme im EGS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| KMN_GRAUS | string | Ersatzprogramm KMN_GRAUS Bereich: 0:nicht aktiv 1:aktiv |
| KMN_CCHIPERS | string | Ersatzprogramm KMN_CCHIPERS Bereich: 0:nicht aktiv 1:aktiv |
| KMN_PMAX | string | Ersatzprogramm KMN_PMAX Bereich: 0:nicht aktiv 1:aktiv |
| KMN_FANZ | string | Ersatzprogramm KMN_FANZ Bereich: 0:nicht aktiv 1:aktiv |
| KMN_MV3AUS | string | Ersatzprogramm KMN_MV3AUS Bereich: 0:nicht aktiv 1:aktiv |
| KMN_MV4AUS | string | Ersatzprogramm KMN_MV4AUS Bereich: 0:nicht aktiv 1:aktiv |
| KMN_CGTERS | string | Ersatzprogramm KMN_CGTERS Bereich: 0:nicht aktiv 1:aktiv |
| KMN_SBCAUS | string | Ersatzprogramm KMN_SBCAUS Bereich: 0:nicht aktiv 1:aktiv |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ersatzprogramme-2"></a>
### STATUS_ERSATZPROGRAMME_2

Auslesen  der aktiven Ersatzprogramme im EGS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| KMN_WKAUF | string | Ersatzprogramm KMN_WKAUF Bereich: 0:nicht aktiv 1:aktiv |
| KMN_AFIX | string | Ersatzprogramm KMN_AFIX Bereich: 0:nicht aktiv 1:aktiv |
| KMN_NRAERS | string | Ersatzprogramm KMN_NRAERS Bereich: 0:nicht aktiv 1:aktiv |
| KMN_NABERS | string | Ersatzprogramm KMN_NABERS Bereich: 0:nicht aktiv 1:aktiv |
| KMN_PNAUS | string | Ersatzprogramm KMN_PNAUS Bereich: 0:nicht aktiv 1:aktiv |
| KMN_GFIX | string | Ersatzprogramm KMN_GFIX Bereich: 0:nicht aktiv 1:aktiv |
| KMN_G5FIX | string | Ersatzprogramm KMN_G5FIX Bereich: 0:nicht aktiv 1:aktiv |
| KMN_G4FIX | string | Ersatzprogramm KMN_G4FIX Bereich: 0:nicht aktiv 1:aktiv |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ersatzprogramme-1"></a>
### STATUS_ERSATZPROGRAMME_1

Auslesen  der aktiven Ersatzprogramme im EGS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| KMN_G13 | string | Ersatzprogramm KMN_G13 Bereich: 0:nicht aktiv 1:aktiv |
| KMN_G46 | string | Ersatzprogramm KMN_G46 Bereich: 0:nicht aktiv 1:aktiv |
| KMN_ENPG5 | string | Ersatzprogramm KMN_ENPG5 Bereich: 0:nicht aktiv 1:aktiv |
| KMN_ENPG35 | string | Ersatzprogramm KMN_ENPG35 Bereich: 0:nicht aktiv 1:aktiv |
| KMN_RNGERS | string | Ersatzprogramm KMN_RNGERS Bereich: 0:nicht aktiv 1:aktiv |
| KMN_GFIXLOW | string | Ersatzprogramm KMN_GFIXLOW Bereich: 0:nicht aktiv 1:aktiv |
| KMN_GRAUSSON | string | Ersatzprogramm KMN_GRAUSSON Bereich: 0:nicht aktiv 1:aktiv |
| KMN_KMN_23 | string | Ersatzprogramm KMN_KMN_23 Bereich: 0:nicht aktiv 1:aktiv |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ersatzprogramme-0"></a>
### STATUS_ERSATZPROGRAMME_0

Auslesen  der aktiven Ersatzprogramme im EGS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| KMN_G3FIX | string | Ersatzprogramm KMN_G3FIX Bereich: 0:nicht aktiv 1:aktiv |
| KMN_BENPG3 | string | Ersatzprogramm KMN_BENPG3 Bereich: 0:nicht aktiv 1:aktiv |
| KMN_BENPG4 | string | Ersatzprogramm KMN_BENPG4 Bereich: 0:nicht aktiv 1:aktiv |
| KMN_BENPG1 | string | Ersatzprogramm KMN_BENPG1 Bereich: 0:nicht aktiv 1:aktiv |
| KMN_BENPG2 | string | Ersatzprogramm KMN_BENPG2 Bereich: 0:nicht aktiv 1:aktiv |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Auslesen aller Messwerte 0x01..0x7E KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GETRIEBETEMPERATUR_WERT | real | Getriebeoeltemperatur Bereich: -40 bis 215 |
| STAT_GETRIEBETEMPERATUR_EINH | string | Grad C |
| STAT_MOTORTEMPERATUR_WERT | real | Motortemperatur Bereich: -48 bis 207 |
| STAT_MOTORTEMPERATUR_EINH | string | Grad C |
| STAT_FAHRPEDALWINKEL_WERT | real | Fahrpedalwinkel Bereich: 0% bis 100% |
| STAT_FAHRPEDALWINKEL_EINH | string | Prozent |
| STAT_ABTRIEBSDREHZAHL_WERT | real | Abtriebsdrehzahl Bereich: 0 bis 8160 |
| STAT_ABTRIEBSDREHZAHL_EINH | string | U/min |
| STAT_TURBINENDREHZAHL_WERT | real | Turbinendrehzahl Bereich: 0 bis 8160 |
| STAT_TURBINENDREHZAHL_EINH | string | U/min |
| STAT_MOTORDREHZAHL_WERT | real | Motordrehzahl Bereich: 0 bis 8160 |
| STAT_MOTORDREHZAHL_EINH | string | U/min |
| STAT_RADGESCHWINDIGKEITEN_WERT | real | Radgeschwindigkeiten Bereich: 0 bis 510 |
| STAT_RADGESCHWINDIGKEITEN_EINH | string | km/h |
| STAT_MOTORISTMOMENT_WERT | real | Motoristmoment Bereich: -100 bis 916 |
| STAT_MOTORISTMOMENT_EINH | string | Nm |
| STAT_MOTORSOLLMOMENT_WERT | real | Motorsollmoment Bereich: -100 bis 916 |
| STAT_MOTORSOLLMOMENT_EINH | string | Nm |
| STAT_ISTGANG_WERT | string | Istgang Bereich:1...6 Gang, 7 = R |
| STAT_WK_WERT | string | Istgang Bereich:0...2 0=offen 1=geregelt 2=geschlossen |
| STAT_BATTERIESPANNUNG_WERT | real | Batteriespannung Bereich: 0 bis 20,4 |
| STAT_BATTERIESPANNUNG_EINH | string | Volt |
| STAT_DR_MV_SPANNUNG_WERT | real | DR/MV Versorgungsspannung Bereich: 0 bis 20,4 |
| STAT_DR_MV_SPANNUNG_EINH | string | Volt |
| STAT_MV1_WERT | string | Sollzustand MV1 Bereich: 0=aus  1=an |
| STAT_MV2_WERT | string | Sollzustand MV2 Bereich: 0=aus  1=an |
| STAT_MV3_WERT | string | Sollzustand MV3 Bereich: Peek/hold |
| STAT_MV4_WERT | string | Sollzustand MV4 Bereich: 0=aus  1=an |
| STAT_PEGEL_L1_WERT | string | Pegel L1 Pin Bereich: 0=low  1=high |
| STAT_PEGEL_L2_WERT | string | Pegel L2 Pin Bereich: 0=low  1=high |
| STAT_PEGEL_L3_WERT | string | Pegel L3 Pin Bereich: 0=low  1=high |
| STAT_PEGEL_L4_WERT | string | Pegel L4 Pin Bereich: 0=low  1=high |
| STAT_PEGEL_TIP_PLUS_WERT | string | Pegel Tip+ Pin Bereich: 0=low  1=high |
| STAT_PEGEL_TIP_MINUS_WERT | string | Pegel Tip- Pin Bereich: 0=low  1=high |
| STAT_PEGEL_M_GASSE_WERT | string | Pegel M-Gasse Pin Bereich: 0=low  1=high |
| STAT_SIGNAL_SUBSTRATTEMPERATUR_WERT | string | Signalsstatus Substrattemperatur Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_GETRIEBEOELTEMPERATUR_WERT | string | Signalsstatus Getriebeoeltemperatur Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_PARKSPERRENSENSOR_WERT | string | Status Parksperrensensor Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_POSITIONSSENOR_WERT | string | Status Positionssensor Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_TURNBINENDREHZAHL_WERT | string | Status Turbinendrehzahl Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_ABTRIEBSDREHZAHL_WERT | string | Status Abtriebsdrehzahl Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_MOTORDREHZAHL_WERT | string | Signalsstatus Motordrehzahl Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_DROSSELKLAPPE_WERT | string | Status Drosselklappe/Fahrpedal Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_PARKSPERENANFORDERUNG_WERT | string | Status Parksperrenanforderung DME Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_MOMENT1_WERT | string | Status Momentenschnittstelle DME EGS Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_BREMSSIGNAL_WERT | string | Signalsstatus Bremssignal Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_DREHRICHTUNG_WERT | string | Signalstatus Drehrichtungserkennung RAD Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_RADGESCHWINDIGKEIT_HL_WERT | string | Status Radgeschwindigkeit HL Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_RADGESCHWINDIGKEIT_HR_WERT | string | Status Radgeschwindigkeit HR Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_RADGESCHWINDIGKEIT_VL_WERT | string | Status Radgeschwindigkeit VL Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_RADGESCHWINDIGKEIT_VR_WERT | string | Status Radgeschwindigkeit VR Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_S_TASTER_WERT | string | Signalsstatus S-Taster Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_TIP_TASTER_WERT | string | Status Tip-Taster Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_POS_SERIELL_WERT | string | Status Position ueber serielle Leitung Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_POS_CAN_WERT | string | Status Position ueber CAN Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_FAHRERTUER_WERT | string | Status Fahrertuer Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_FAHRERSITZ_WERT | string | Status Fahrersitz Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_SCHLUESSEL_STECKT_WERT | string | Status Schluessel steckt Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SIGNAL_KL15_WERT | string | Status Klemme 15 ueber CAN Bereich: 0=in Ordnung 1=nicht in Ordnung |
| STAT_SA_WERT | string | Schaltart Bereich:0...25 |
| STAT_TIP_PLUS_LINKS | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_TIP_MINUS_LINKS | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_TIP_PLUS_RECHTS | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_TIP_MINUS_RECHTS | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_S_TASTER | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_P_TASTER | string | Taste betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_BREMSE_GETRETEN | string | Bremse betaetigt/nicht betaetigt Bereich: 0=nicht betaetigt 1=betaetigt |
| STAT_WH_POSITION | string | WH-Position Bereich:0...12 |
| STAT_GETRIEBEPOSITION | string | Getriebeposition Bereich:6...9 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-reset-egs"></a>
### RESET_EGS

EGS fuehrt Reset aus KWP2000: $11 EcuResetService Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aif-aktuell-lesen"></a>
### AIF_AKTUELL_LESEN

aktuelles Anwenderinfofeld lesen KWP2000: $1A ReadEcuIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| BMW_VehicleIdentificationNr | string | BMW Fahrgestellnummer  |
| BMW_ProgrammingDate | string | Datum Programmierung |
| BMW_AssemblyNr | string | BMW ZUS-BAU Nummer (Zusammenbau-Nummer) |
| BMW_CalibrationDataSetNr | string | BMW SW-Nummer (Datensatznummer)  |
| BMW_ExhaustRegulationOrTypeApprovalNr | string | BMW Behoerdennummer |
| Werkscode_Haendlernummer | string | BMW Werkscode oder Haendlernummer  |
| Tester_Seriennummer | string | Seriennummer BMW Tester |
| KM_Stand_Programmierung | int | Km-Stand Fzg. bei Programmierung  |
| Programmstand | string | Programmstand ZZZPPPxVBBxh |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-auslesen-physical-ecu-hw-nr"></a>
### AUSLESEN_PHYSICAL_ECU_HW_NR

Auslesen der PHYSICAL_ECU_HW_NR KWP2000: $1A ReadEcuIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PHYSICAL_ECU_HW_NR | string | BMW HW-Nummer (Teilenummer) E-Modul+Boot+SW Programm  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-auslesen-system-supplier-ecu-serial-nr"></a>
### AUSLESEN_SYSTEM_SUPPLIER_ECU_SERIAL_NR

Auslesen der SYSTEM_SUPPLIER_ECU_SERIAL_NR KWP2000: $1A ReadEcuIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SYSTEM_SUPPLIER_ECU_SERIAL_NR | string | RB Seriennummer 9 Byte ASCII  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-auslesen-sw-stand-entwicklung"></a>
### AUSLESEN_SW_STAND_ENTWICKLUNG

Auslesen der SYSTEM_SUPPLIER_ECU_SOFTWARE_VERSION_NR KWP2000: $1A ReadEcuIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PROGRAMMSTAND | string | Programmstand Entwicklung  |
| ERSTELLER | string | SW-Stand Ersteller Entwicklung  |
| SONDERSTAND | string | Sonderstand Entwicklung  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-auslesen-system-supplier-ecu-hw-nr"></a>
### AUSLESEN_SYSTEM_SUPPLIER_ECU_HW_NR

Auslesen der SYSTEM_SUPPLIER_ECU_HW_NR KWP2000: $1A ReadEcuIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SYSTEM_SUPPLIER_ECU_HW_NR | string | RB HW-Nummer 10 Byte ASCII  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ganganzeige-starten"></a>
### GANGANZEIGE_STARTEN

Anzeige Gang im Kombi KWP2000: $31 StartRoutineByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ganganzeige-stoppen"></a>
### GANGANZEIGE_STOPPEN

Anzeige Gang im Kombi beenden KWP2000: $32 StopRoutineByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-backupfehlerspeicher-lesen"></a>
### BACKUPFEHLERSPEICHER_LESEN

Backup-Fehlerspeicher lesen KWP2000:  ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom als Text  |
| F_WARNUNG_NR | int | Warnlampen Flag als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag als Text  |
| F_SPORADISCH_NR | int | Fehler sporadisch als Text  |
| F_SPORADISCH_TEXT | string | Fehler sporadisch als Text  |
| F_ERSATZFUNKTION_NR | int | Ersatzfunktion aktiv/deaktiv als Zahl  |
| F_ERSATZFUNKTION_TEXT | string | Ersatzfunktion aktiv/deaktiv als Text  |
| F_VORHANDEN_NR | int | Fehler vorhanden als Nummer  |
| F_VORHANDEN_TEXT | string | Fehler vorhanden als Text  |
| CARB_TRIPS_DRIVING | int | Carb Zaehler fuer Driving Zyklen  |
| CARB_ZAEHLER_WARM_UP | int | Carb Zaehler fuer Warm-Up Zyklen  |
| HAEUFIGKEITSZAEHLER | int | Haeufigkeitszaehler  |
| KILOMETERSTAND | real | Kilometerstand  |
| UW_ANZ | int | Anzahl Umweltbedingungen  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-signal-stellglied"></a>
### STEUERN_SIGNAL_STELLGLIED

Status setzen der Signale/Stellglieder KWP2000: $30 InputOutputControlByLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SIGNAL | string | MV1,MV2,MV3,EDS1,EDS2,EDS3,EDS4,EDS5,EDS6,SHIFTLOCK,INTERLOCK,KOMBI |
| ZUSTAND | string | EIN,EIN/AUS,AUS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-signal-stellglied"></a>
### STATUS_SIGNAL_STELLGLIED

Auslesen Status der Signale/Stellglieder KWP2000: $30 InputOutputControlByLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SIGNAL | string | MV1,MV2,MV3,EDS1,EDS2,EDS3,EDS4,EDS5,EDS6,L1,L2,L3,L4,P_LEITUNG,SHIFTLOCK,INTERLOCK |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| LOCAL_IDENTIFIER | string | MV1,MV2,MV3,EDS1,EDS2,EDS3,EDS4,EDS5,EDS6,L1,L2,L3,L4,P_LEITUNG,SHIFTLOCK,INTERLOCK |
| CONTROLSTATE | string | EIN,EIN/AUS,AUS |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sekundaerfehlerspeicher-lesen-1"></a>
### SEKUNDAERFEHLERSPEICHER_LESEN_1

Auslesen Sekundaerfehlerspeicher KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ORT_NR | int | Fehlerort Nummer  |
| F_ORT_TEXT | string | Fehlerort Text  |
| FILTER_STOERUNGEN | real | Filter fuer Stoerungen (Vorzeichenbehaftet)  |
| ZEITSTEMPEL | real | Zeitpunkt des letzten Aufrufs  |
| SYMTOMZAEHLER | real | Symtomzaehler  |
| STOERUNG | string | Stoerung vorhanden  |
| ZWANGSFILTERUNG_OBD | string | Zwangsfilterung fuer OBD laeuft  |
| ZEITERFASSUNG | string | Zeiterfassung laeuft  |
| FEHLER_NACH_RESET | string | Nach Reset war Fehler mindestens einmal vorhanden  |
| FUNKTION | string | Funktion mindestens einmal vollstaendig gefiltert  |
| PRUEFBEDINGUNG | string | Pruefbedingung erfuellt  |
| SCHUTZFUNKTION | string | Schutzfunktion aktiv  |
| ERSATZFUNKTION | string | Ersatzfunktion aktiv  |
| FEHLER | string | Fehler vorhanden  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sekundaerfehlerspeicher-lesen-2"></a>
### SEKUNDAERFEHLERSPEICHER_LESEN_2

Auslesen Sekundaerfehlerspeicher KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ORT_NR | int | Fehlerort Nummer  |
| F_ORT_TEXT | string | Fehlerort Text  |
| FILTER_STOERUNGEN | real | Filter fuer Stoerungen (Vorzeichenbehaftet)  |
| ZEITSTEMPEL | real | Zeiterfassung laeuft  |
| SYMTOMZAEHLER | real | Symtomzaehler  |
| STOERUNG | string | Stoerung vorhanden  |
| ZWANGSFILTERUNG_OBD | string | Zwangsfilterung fuer OBD laeuft  |
| ZEITERFASSUNG | string | Zeiterfassung laeuft  |
| FEHLER_NACH_RESET | string | Nach Reset war Fehler mindestens einmal vorhanden  |
| FUNKTION | string | Funktion mindestens einmal vollstaendig gefiltert  |
| PRUEFBEDINGUNG | string | Pruefbedingung erfuellt  |
| SCHUTZFUNKTION | string | Schutzfunktion aktiv  |
| ERSATZFUNKTION | string | Ersatzfunktion aktiv  |
| FEHLER | string | Fehler vorhanden  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-lesen-flare"></a>
### ADAPTIONSWERTE_LESEN_FLARE

Auslesen der Adaptionswerte Flare KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLARE | binary | Adaptionswerte  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-lesen-glue"></a>
### ADAPTIONSWERTE_LESEN_GLUE

Auslesen der Adaptionswerte GLUE KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| GLUE | binary | Adaptionswerte  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-lesen-gls"></a>
### ADAPTIONSWERTE_LESEN_GLS

Auslesen der Adaptionswerte GLS KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| GLS | binary | Adaptionswerte  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-lesen-slz"></a>
### ADAPTIONSWERTE_LESEN_SLZ

Auslesen der Adaptionswerte SLZ KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SLZ | binary | Adaptionswerte  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-lesen-sf"></a>
### ADAPTIONSWERTE_LESEN_SF

Auslesen der Adaptionswerte SF KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SF | binary | Adaptionswerte  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-lesen-pf"></a>
### ADAPTIONSWERTE_LESEN_PF

Auslesen der Adaptionswerte PF KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PF | binary | Adaptionswerte  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-lesen-gwk"></a>
### ADAPTIONSWERTE_LESEN_GWK

Auslesen der Adaptionswerte GWK KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| GWK | binary | Adaptionswerte  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-lesen-sbc"></a>
### ADAPTIONSWERTE_LESEN_SBC

Auslesen der Adaptionswerte SBC KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SBC | binary | Adaptionswerte  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adaptionswerte-ruecksetzen"></a>
### ADAPTIONSWERTE_RUECKSETZEN

alle Adaptionswerte ruecksetzen KWP2000: $31 StartRoutineByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-quicktest"></a>
### QUICKTEST

Anzahl Fehler / Kilometerstand KWP2000: $31 StartRoutineByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ANZAHL_FEHLER | int | Anzahl Fehler im Fehlerspeicher  |
| KILOMETERSTAND_AKTUELL | real | Kilometerstand aktuell  |
| KILOMETERSTAND_FS_LOESCHEN | real | Kilometerstand beim letzten FS-Loeschen  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-egs-diagnose-testjob"></a>
### EGS_DIAGNOSE_TESTJOB

Job fuer EGS Diagnosetest KWP2000: Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL_DATEN | int | Anzahl Datenbytes |
| DATEN_1 | int | Daten Byte 1 |
| DATEN_2 | int | Daten Byte 2 |
| DATEN_3 | int | Daten Byte 3 |
| DATEN_4 | int | Daten Byte 4 |
| DATEN_5 | int | Daten Byte 5 |
| DATEN_6 | int | Daten Byte 6 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EGS_OUT | binary | Antwort von EGS  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hardware-referenz-lesen"></a>
### HARDWARE_REFERENZ_LESEN

BRIF Inhalt ausgeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BRIF | string | BRIF Inhalt 7 Byte ASCII  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-programm-referenz-lesen"></a>
### PROGRAMM_REFERENZ_LESEN

ZIF Inhalt ausgeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ZIF | string | ZIF Inhalt 12 Byte ASCII  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-daten-referenz-lesen"></a>
### DATEN_REFERENZ_LESEN

DIF Inhalt ausgeben KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DIF | string | DIF Inhalt 17 Byte ASCII  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [CONTROLSTATEUMRECHNUNG](#table-controlstateumrechnung) (4 × 2)
- [IDENTIFIER_LESEN](#table-identifier-lesen) (17 × 5)
- [IDENTIFIER_SETZEN](#table-identifier-setzen) (14 × 5)
- [FORTRBBMW](#table-fortrbbmw) (85 × 2)
- [ERSTELLER](#table-ersteller) (17 × 2)
- [FARTRBBMW](#table-fartrbbmw) (13 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (66 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (66 × 5)
- [SGT_OUT0](#table-sgt-out0) (1 × 6)
- [SGT_INP0](#table-sgt-inp0) (1 × 8)
- [SGT_GEAR0](#table-sgt-gear0) (1 × 3)
- [SGT_SIG0](#table-sgt-sig0) (1 × 6)
- [SGT_SIG1](#table-sgt-sig1) (1 × 5)
- [SGT_SIG2](#table-sgt-sig2) (1 × 7)
- [SGT_SIG3](#table-sgt-sig3) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (51 × 9)
- [WK_TAB](#table-wk-tab) (4 × 2)
- [SA_TAB](#table-sa-tab) (25 × 2)
- [JOBRESULT](#table-jobresult) (70 × 2)
- [LIEFERANTEN](#table-lieferanten) (50 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (12 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (10 × 3)

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-controlstateumrechnung"></a>
### CONTROLSTATEUMRECHNUNG

Dimensions: 4 rows × 2 columns

| CONTROLSTATE | CS |
| --- | --- |
| EIN | 0x02 |
| EIN/AUS | 0x01 |
| AUS | 0x00 |
|  | 0x03 |

<a id="table-identifier-lesen"></a>
### IDENTIFIER_LESEN

Dimensions: 17 rows × 5 columns

| IDENTIFIER | SIGNAL | 0X00 | 0X01 | 0X02 |
| --- | --- | --- | --- | --- |
| 0x01 | MV1 | AUS    | - | EIN    |
| 0x02 | MV2 | AUS    | - | EIN    |
| 0x03 | MV3 | AUS    | - | EIN    |
| 0x10 | EDS1 | &lt;=100mA | - | &gt;100mA |
| 0x11 | EDS2 | &lt;=100mA | - | &gt;100mA |
| 0x12 | EDS3 | &lt;=100mA | - | &gt;100mA |
| 0x13 | EDS4 | &lt;=100mA | - | &gt;100mA |
| 0x14 | EDS5 | &lt;=100mA | - | &gt;100mA |
| 0x15 | EDS6 | &lt;=100mA | - | &gt;100mA |
| 0x20 | L1 | L-Leitung LOW | - | L-Leitung HIGH |
| 0x21 | L2 | L-Leitung LOW | - | L-Leitung HIGH |
| 0x22 | L3 | L-Leitung LOW | - | L-Leitung HIGH |
| 0x23 | L4 | L-Leitung LOW | - | L-Leitung HIGH |
| 0x24 | P_Leitung | AUS | - | EIN |
| 0x30 | Shiftlock | AUS | - | EIN |
| 0x31 | Interlock | AUS | - | EIN |
| 0x00 |  | - | - | - |

<a id="table-identifier-setzen"></a>
### IDENTIFIER_SETZEN

Dimensions: 14 rows × 5 columns

| IDENTIFIER | SIGNAL | 0X00 | 0X01 | 0X02 |
| --- | --- | --- | --- | --- |
| 0x01 | MV1 | AUS | AUS/EIN 1s | EIN |
| 0x02 | MV2 | AUS | AUS/EIN 1s | EIN |
| 0x03 | MV3 | AUS | AUS/EIN 1s | EIN |
| 0x10 | EDS1 | 50mA | AUS/EIN 1s | EIN |
| 0x11 | EDS2 | 50mA | 50mA/800mA 1s | 800mA |
| 0x12 | EDS3 | 50mA | 50mA/800mA 1s | 800mA |
| 0x13 | EDS4 | 50mA | 50mA/800mA 1s | 800mA |
| 0x14 | EDS5 | 50mA | 50mA/800mA 1s | 800mA |
| 0x15 | EDS6 | 50mA | 50mA/800mA 1s | 800mA |
| 0x24 | P_Leitung | AUS | AUS/EIN 1s | EIN |
| 0x30 | Shiftlock | AUS | AUS/EIN 1s | EIN |
| 0x31 | Interlock | AUS | AUS/EIN 1s | EIN |
| 0x40 | Kombi | Kombi dunkel | - | Kombi an |
| 0x00 |  |  |  |  |

<a id="table-fortrbbmw"></a>
### FORTRBBMW

Dimensions: 85 rows × 2 columns

| RB | BMW |
| --- | --- |
| 0x00 | 0x0000 |
| 0x01 | 0x5096 |
| 0x02 | 0x5090 |
| 0x03 | 0x5080 |
| 0x04 | 0x5022 |
| 0x05 | 0x50B0 |
| 0x06 | 0x5051 |
| 0x07 | 0x5050 |
| 0x08 | 0x5091 |
| 0x09 | 0x5020 |
| 0x0A | 0x5020 |
| 0x0B | 0x5021 |
| 0x0C | 0x503D |
| 0x0D | 0x50A5 |
| 0x0E | 0x50A4 |
| 0x0F | 0x50A9 |
| 0x10 | 0x5060 |
| 0x11 | 0x50B1 |
| 0x12 | 0x5062 |
| 0x13 | 0x5052 |
| 0x14 | 0x503F |
| 0x15 | 0x5001 |
| 0x16 | 0x5001 |
| 0x17 | 0x5002 |
| 0x18 | 0x5002 |
| 0x19 | 0x5003 |
| 0x1A | 0x5003 |
| 0x1B | 0x5004 |
| 0x1C | 0x5004 |
| 0x1D | 0x5005 |
| 0x1E | 0x5005 |
| 0x1F | 0x5006 |
| 0x20 | 0x5006 |
| 0x21 | 0x5010 |
| 0x22 | 0x5010 |
| 0x23 | 0x5011 |
| 0x24 | 0x5011 |
| 0x25 | 0x5012 |
| 0x26 | 0x5012 |
| 0x27 | 0x5013 |
| 0x28 | 0x5013 |
| 0x29 | 0x5030 |
| 0x2A | 0x5031 |
| 0x2B | 0x5032 |
| 0x2C | 0x5033 |
| 0x2D | 0x5034 |
| 0x2E | 0x5035 |
| 0x2F | 0x5036 |
| 0x30 | 0x5040 |
| 0x31 | 0x5041 |
| 0x32 | 0x5041 |
| 0x33 | 0x5042 |
| 0x34 | 0x5042 |
| 0x35 | 0x5043 |
| 0x36 | 0x5043 |
| 0x37 | 0x5044 |
| 0x38 | 0x5044 |
| 0x39 | 0x5045 |
| 0x3A | 0x5046 |
| 0x3B | 0x5046 |
| 0x3C | 0x5047 |
| 0x3D | 0x5048 |
| 0x3E | 0x5049 |
| 0x3F | 0x5049 |
| 0x40 | 0x504A |
| 0x41 | 0x504A |
| 0x42 | 0x5088 |
| 0x43 | 0x5083 |
| 0x44 | 0x5089 |
| 0x45 | 0x5081 |
| 0x46 | 0x5086 |
| 0x47 | 0x5087 |
| 0x48 | 0x5082 |
| 0x49 | 0x50A0 |
| 0x4A | 0x50A1 |
| 0x4B | 0x50A2 |
| 0x4C | 0x50A3 |
| 0x4D | 0x5023 |
| 0x4E | 0x5063 |
| 0x4F | 0x5053 |
| 0x50 | 0x50AA |
| 0x51 | 0x50A7 |
| 0x52 | 0x50A8 |
| 0x53 | 0x50A6 |
| 0X?? | ERROR_UNKNOWN |

<a id="table-ersteller"></a>
### ERSTELLER

Dimensions: 17 rows × 2 columns

| ASCII | NAME |
| --- | --- |
| 0 | Vorbelegung ZF TE-H |
| 1 | Wiest ZF ES32 |
| 2 | Zwingenberger ZF ES32 |
| 3 | Buohlert ZF ES32 |
| 4 | Zimmermann ZF ES32 |
| 5 | Cueppers ZF ES32 |
| 6 | Bader ZF ES22 |
| A | Steinke BMW EA-71 |
| B | Mischnik BMW EA-71 |
| C | Noack BMW EA-71 |
| S | Schmeling BMW EA-71 |
| E | Smirnow BMW EA-71 |
| F | Boeker BMW EA-71 |
| G | Daieff BMW EA-71 |
| H | Meyer BMW EA-71 |
| I | Burkhardt BMW EA-71 |
| 0x?? | ERROR_UNKNOWN |

<a id="table-fartrbbmw"></a>
### FARTRBBMW

Dimensions: 13 rows × 2 columns

| RB | BMW |
| --- | --- |
| 0x00 | 0x00 |
| 0x01 | 0x08 |
| 0x02 | 0x01 |
| 0x03 | 0x02 |
| 0x04 | 0x04 |
| 0x05 | 0x00 |
| 0x06 | 0x00 |
| 0x07 | 0x01 |
| 0x08 | 0x02 |
| 0x09 | 0x00 |
| 0x0A | 0x00 |
| 0x0B | 0x00 |
| 0x?? | ERROR_UNKNOWN |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB |  STATUS_TEXT |
| --- | --- |
| 0XXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 66 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5001 | EDS 1 |
| 0x5002 | EDS 2 |
| 0x5003 | EDS 3 |
| 0x5004 | EDS 4 |
| 0x5005 | EDS 5 |
| 0x5006 | EDS 6 |
| 0x5010 | MV 1 |
| 0x5011 | MV 2 |
| 0x5012 | MV 3 |
| 0x5013 | MV 4 |
| 0x5020 | N_Abtrieb |
| 0x5021 | N_Turbine |
| 0x5022 | Getriebeoeltemperatursensor |
| 0x5023 | Substrattemperatursensor |
| 0x5030 | Symptom Gangueberwachung |
| 0x5031 | Gangueberwachung 1 |
| 0x5032 | Gangueberwachung 2 |
| 0x5033 | Gangueberwachung 3 |
| 0x5034 | Gangueberwachung 4 |
| 0x5035 | Gangueberwachung 5 |
| 0x5036 | Gangueberwachung 6 |
| 0x503d | Oelalterungsschwelle |
| 0x503f | WK fehlerhaft geoeffnet |
| 0x5040 | Symptom Schaltungsueberwachung |
| 0x5041 | Schaltungsueberwachung 12 |
| 0x5042 | Schaltungsueberwachung 23 |
| 0x5043 | Schaltungsueberwachung 34 |
| 0x5044 | Schaltungsueberwachung 45 |
| 0x5045 | Schaltungsueberwachung 56 |
| 0x5046 | Schaltungsueberwachung 21 |
| 0x5047 | Schaltungsueberwachung 32 |
| 0x5048 | Schaltungsueberwachung 43 |
| 0x5049 | Schaltungsueberwachung 54 |
| 0x504A | Schaltungsueberwachung 65 |
| 0x5050 | Interner Fehler EPROM |
| 0x5051 | Interner Fehler EEPROM |
| 0x5052 | Interner Fehler Watchdog |
| 0x5053 | Interner Fehler VRAM |
| 0x5060 | Batteriespannung |
| 0x5062 | Druckregler/Magnetventil Versorgungsspannung |
| 0x5063 | Sensorversorgungsspannung |
| 0x5080 | Ueberwachung CAN-Bus |
| 0x5081 | CAN Timeout DME |
| 0x5082 | CAN Timeout DSC |
| 0x5083 | CAN Timeout Kombi |
| 0x5086 | CAN Timeout ACC |
| 0x5087 | CAN Timeout CAS |
| 0x5088 | CAN Timeout EMF |
| 0x5089 | CAN Timeout SSV |
| 0x5090 | CAN Stand-Fehler  |
| 0x5091 | CAN Momentenschnittstelle |
| 0x5096 | CAN Motordrehzahl |
| 0x50A0 | CAN Timeout SZL |
| 0x50A1 | Serielle Leitung Timeout |
| 0x50A2 | SZL Positionsinfo CAN |
| 0x50A3 | SZL Positionsinfo serielle Ltg. |
| 0x50A4 | Doppelfehler Positionsinfo SZL |
| 0x50A5 | Parksperrensensoren unplausibel |
| 0x50A6 | CAN SZL P-Taster Fehler  |
| 0x50A7 | Parksperre fehlerhaft eingelegt |
| 0x50A8 | Parksperre fehlerhaft ausgelegt |
| 0x50A9 | CAN Schluessel-Steckt |
| 0x50AA | Fehler Steptronic |
| 0x50B0 | Doppelfehler Ersatzfunktion |
| 0x50B1 | Fehler KFC_EGSOFF |
| 0x???? | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 66 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x5001 | sgt_Gear0 | 0x01 | 0x02 | 0x03 |
| 0x5002 | sgt_Gear0 | 0x01 | 0x02 | 0x03 |
| 0x5003 | sgt_Gear0 | 0x01 | 0x02 | 0x03 |
| 0x5004 | sgt_Gear0 | 0x01 | 0x02 | 0x03 |
| 0x5005 | sgt_Gear0 | 0x01 | 0x02 | 0x03 |
| 0x5006 | sgt_Gear0 | 0x01 | 0x02 | 0x03 |
| 0x5010 | sgt_Gear0 | 0x01 | 0x02 | sgt_Out0 |
| 0x5011 | sgt_Gear0 | 0x01 | 0x02 | sgt_Out0 |
| 0x5012 | sgt_Gear0 | 0x01 | 0x02 | sgt_Out0 |
| 0x5013 | sgt_Gear0 | 0x01 | 0x02 | sgt_Out0 |
| 0x5020 | sgt_Gear0 | 0x01 | 0x04 | 0x0E |
| 0x5021 | sgt_Gear0 | 0x01 | 0x04 | 0x05 |
| 0x5022 | 0x04 | 0x05 | 0x06 | 0x03 |
| 0x5023 | 0x04 | 0x05 | 0x01 | 0x03 |
| 0x5030 | sgt_Gear0 | 0x0B | 0x01 | 0x03 |
| 0x5031 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5032 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5033 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5034 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5035 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5036 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x503D | 0x01 | 0x01 | 0x01 | 0x01 |
| 0x503F | sgt_Gear0 | 0x0B | 0x01 | 0x03 |
| 0x5040 | sgt_Gear0 | 0x0B | 0x01 | 0x03 |
| 0x5041 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5042 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5043 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5044 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5045 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5046 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5047 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5048 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5049 | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x504A | 0x0B | 0x01 | 0x03 | 0x07 |
| 0x5050 | 0x01 | 0xFE | 0x04 | 0x04 |
| 0x5051 | 0x01 | 0xFE | 0x04 | 0x04 |
| 0x5052 | 0x01 | 0xFE | 0x04 | 0x04 |
| 0x5053 | 0xFE | 0xFE | 0xFE | 0xFE |
| 0x5060 | 0x04 | 0x05 | 0x01 | 0x03 |
| 0x5062 | 0x04 | 0x05 | 0x01 | 0x03 |
| 0x5063 | 0x04 | 0x05 | 0x01 | 0x03 |
| 0x5080 | 0x0C | 0x04 | 0x01 | 0x05 |
| 0x5081 | 0x0C | 0x04 | 0x01 | 0x05 |
| 0x5082 | 0x0C | 0x04 | 0x01 | 0x05 |
| 0x5083 | 0x0C | 0x04 | 0x01 | 0x05 |
| 0x5086 | 0x0C | 0x04 | 0x01 | 0x05 |
| 0x5087 | 0x0C | 0x04 | 0x01 | 0x05 |
| 0x5088 | 0x0C | 0x04 | 0x01 | 0x05 |
| 0x5089 | 0x0C | 0x04 | 0x01 | 0x05 |
| 0x5090 | 0x0C | 0x04 | 0x01 | 0x0D |
| 0x5091 | 0x0D | 0x05 | 0x08 | 0x04 |
| 0x5096 | 0x0D | 0x0B | 0x08 | 0x04 |
| 0x50A0 | 0x0C | 0x04 | 0x01 | 0x05 |
| 0x50A1 | 0x0C | 0x04 | 0x01 | 0x05 |
| 0x50A2 | 0x0C | 0x04 | 0xFE | 0xFE |
| 0x50A3 | 0x0C | 0x04 | 0xFE | 0xFE |
| 0x50A4 | sgt_Inp0 | 0x04 | 0x01 | 0x05 |
| 0x50A5 | sgt_Inp0 | 0x04 | 0x01 | 0x05 |
| 0x50A6 | sgt_Sig3 | 0x04 | 0xFE | 0xFE |
| 0x50A7 | sgt_sig0 | sgt_Inp0 | 0x01 | 0x05 |
| 0x50A8 | sgt_sig0 | sgt_Inp0 | 0x01 | 0x05 |
| 0x50A9 | 0x04 | 0x04 | 0x0C | 0x0C |
| 0x50AA | sgt_Inp0 | 0x04 | 0x05 | 0xFE |
| 0x50B0 | 0xFE | 0xFE | 0xFE | 0xFE |
| 0x50B1 | 0xFE | 0xFE | 0xFE | 0xFE |
| default | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-sgt-out0"></a>
### SGT_OUT0

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x22 | 0x23 | 0x24 | 0x25 | 0x26 |

<a id="table-sgt-inp0"></a>
### SGT_INP0

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x30 | 0x31 | 0x32 | 0x33 | 0x34 | 0x35 | 0x36 |

<a id="table-sgt-gear0"></a>
### SGT_GEAR0

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x20 | 0x21 |

<a id="table-sgt-sig0"></a>
### SGT_SIG0

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x40 | 0x41 | 0x42 | 0x43 | 0x44 |

<a id="table-sgt-sig1"></a>
### SGT_SIG1

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x50 | 0x51 | 0x52 | 0x53 |

<a id="table-sgt-sig2"></a>
### SGT_SIG2

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x60 | 0x61 | 0x62 | 0x63 | 0x64 | 0x65 |

<a id="table-sgt-sig3"></a>
### SGT_SIG3

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x70 | 0x71 | 0x72 | 0x73 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 51 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Getriebeoeltemperatur | Grad C | - | unsigned char | - | 1 | 1 | -40 |
| 0x02 | Versorgungsspannung DR/MV | Volt | - | unsigned char | - | 0.08 | 1 | 0 |
| 0x03 | Abbtriebsdrehzahl | 1/min | - | unsigned char | - | 32 | 1 | 0 |
| 0x04 | Batteriespannung | Volt | - | unsigned char | - | 0.08 | 1 | 0 |
| 0x05 | Motordrehzahl | 1/min | - | unsigned char | - | 32 | 1 | 0 |
| 0x06 | Substrattemperatur | Grad C | - | unsigned char | - | 1 | 1 | -40 |
| 0x07 | Turbinendrehzahl | 1/min | - | unsigned char | - | 32 | 1 | 0 |
| 0x08 | Motortemperatur | Grad C | - | unsigned char | - | 1 | 1 | -48 |
| 0x0A | Sollmoment Motoreingriff | Nm | - | unsigned char | - | 4 | 1 | 0 |
| 0x0B | Motoristmoment | Nm | - | unsigned char | - | 4 | 1 | 0 |
| 0x0C | Zeit Reset | min | - | unsigned char | - | 1 | 1 | 0 |
| 0x0D | rcn_Stand | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x0E | Mittl. Radgeschw. ang. | km/h | - | unsigned char | - | 2 | 1 | 0 |
| 0x0F | Mittl. Radgeschw. nicht ang. | km/h | - | unsigned char | - | 2 | 1 | 0 |
| 0x10 | Mittl. Radgeschw. alle Raeder | km/h | - | unsigned char | - | 2 | 1 | 0 |
| 0x20 | Zustand WK | 0-n | - | 0x60 | WK_TAB | - | - | - |
| 0x21 | Schaltart | 0-n | - | 0x1F | SA_TAB | - | - | - |
| 0x22 | Sollzustand M1 (0/1 aus/an) | 0/1 | - | 0x80 | - | - | - | - |
| 0x23 | Sollzustand M2 (0/1 aus/an) | 0/1 | - | 0x40 | - | - | - | - |
| 0x24 | Sollzustand M3 (0/1 kein Peak/Peak) | 0/1 | - | 0x20 | - | - | - | - |
| 0x25 | Sollzustand M3 (0/1 kein Hold/Hold) | 0/1 | - | 0x10 | - | - | - | - |
| 0x26 | Sollzustand M4 (0/1 aus/an) | 0/1 | - | 0x08 | - | - | - | - |
| 0x30 | Pegel an L1 Pin (0/1 low/high) | 0/1 | - | 0x80 | - | - | - | - |
| 0x31 | Pegel an L2 Pin (0/1 low/high) | 0/1 | - | 0x40 | - | - | - | - |
| 0x32 | Pegel an L3 Pin (0/1 low/high) | 0/1 | - | 0x20 | - | - | - | - |
| 0x33 | Pegel an L4 Pin ((0/1 low/high) | 0/1 | - | 0x10 | - | - | - | - |
| 0x34 | Pegel an Tip+ Pin (0/1 low/high) | 0/1 | - | 0x08 | - | - | - | - |
| 0x35 | Pegel an Tip- Pin (0/1 low/high) | 0/1 | - | 0x04 | - | - | - | - |
| 0x36 | Pegel an M-Gassen Pin (0/1 low/high) | 0/1 | - | 0x02 | - | - | - | - |
| 0x40 | Status Getriebeoeltemp.  (0=iO, 1=F/ES) | 0/1 | - | 0x10 | - | - | - | - |
| 0x41 | Status Parksperrensensor (0=iO, 1=F/ES) | 0/1 | - | 0x08 | - | - | - | - |
| 0x42 | Status Positionssensor   (0=iO, 1=F/ES) | 0/1 | - | 0x04 | - | - | - | - |
| 0x43 | Status Turbinendrehzahl  (0=iO, 1=F/ES) | 0/1 | - | 0x02 | - | - | - | - |
| 0x44 | Status Abtriebsdrehzahl  (0=iO, 1=F/ES) | 0/1 | - | 0x01 | - | - | - | - |
| 0x50 | Status Motordrehzahl     (0=iO, 1=F/ES) | 0/1 | - | 0x80 | - | - | - | - |
| 0x51 | Status Drosselklappe     (0=iO, 1=F/ES) | 0/1 | - | 0x40 | - | - | - | - |
| 0x52 | Status Parksperrenanf.   (0=iO, 1=F/ES) | 0/1 | - | 0x20 | - | - | - | - |
| 0x53 | Status Moment 1 (MMM)    (0=iO, 1=F/ES) | 0/1 | - | 0x01 | - | - | - | - |
| 0x60 | Status Bremssignal       (0=iO, 1=F/ES) | 0/1 | - | 0x20 | - | - | - | - |
| 0x61 | Status Drehrichtung | 0/1 | - | 0x10 | - | - | - | - |
| 0x62 | Status Radgeschw HL      (0=iO, 1=F/ES) | 0/1 | - | 0x08 | - | - | - | - |
| 0x63 | Status Radgeschw HR      (0=iO, 1=F/ES) | 0/1 | - | 0x04 | - | - | - | - |
| 0x64 | Status Radgeschw VL      (0=iO, 1=F/ES) | 0/1 | - | 0x02 | - | - | - | - |
| 0x65 | Status Radgeschw VR      (0=iO, 1=F/ES) | 0/1 | - | 0x01 | - | - | - | - |
| 0x70 | Status S-Taster CAN      (0=iO, 1=F/ES) | 0/1 | - | 0x80 | - | - | - | - |
| 0x71 | Status Tip-Taster CAN    (0=iO, 1=F/ES) | 0/1 | - | 0x40 | - | - | - | - |
| 0x72 | Status Position ser. Ltg (0=iO, 1=F/ES) | 0/1 | - | 0x20 | - | - | - | - |
| 0x73 | Status Position CAN      (0=iO, 1=F/ES) | 0/1 | - | 0x10 | - | - | - | - |
| 0xFE | nicht definiert | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0xFF | ohne Bedeutung | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0xXY | unbekannte UW | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-wk-tab"></a>
### WK_TAB

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Wandlerkupplung offen              |
| 0x20 | Wandlerkupplung geregelt           |
| 0x40 | Wandlerkupplung zu                 |
| 0xXY | Wandlerkupplung unplausibel        |

<a id="table-sa-tab"></a>
### SA_TAB

Dimensions: 25 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Schaltart nicht definiert |
| 0x01 | Schaltart 1 nach 1 |
| 0x02 | Schaltart 2 nach 2 |
| 0x03 | Schaltart 3 nach 3 |
| 0x04 | Schaltart 4 nach 4 |
| 0x05 | Schaltart 5 nach 5 |
| 0x06 | Schaltart 6 nach 6 |
| 0x07 | Schaltart R nach R |
| 0x0A | Schaltart 1 nach 2 |
| 0x0B | Schaltart 2 nach 3 |
| 0x0C | Schaltart 3 nach 4 |
| 0x0D | Schaltart 4 nach 5 |
| 0x0E | Schaltart 5 nach 6 |
| 0x11 | Schaltart 2 nach 1 |
| 0x12 | Schaltart 3 nach 2 |
| 0x13 | Schaltart 4 nach 3 |
| 0x14 | Schaltart 5 nach 4 |
| 0x15 | Schaltart 6 nach 5 |
| 0x16 | Schaltart 3 nach 1 |
| 0x17 | Schaltart 4 nach 2 |
| 0x18 | Schaltart 5 nach 3 |
| 0x19 | Schaltart 6 nach 4 |
| 0x1A | Schaltart  P/N nach D |
| 0x1B | Schaltart  P/N nach R |
| 0xXY | Schaltart unplausibel |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 70 rows × 2 columns

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
| ?10? | ERROR_F_CODE |
| ?11? | ERROR_TABLE |
| ?12? | ERROR_INTERPRETATION |
| ?13? | ERROR_F_POS |
| ?20? | ERROR_SEGMENT |
| ?21? | ERROR_ADDRESS |
| ?22? | ERROR_NUMBER |
| ?30? | ERROR_DATA |
| ?40? | ERROR_MODE |
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
| ?8A? | ERROR_LARGE_UIF_FOUND |
| ?8B? | ERROR_SMALL_UIF_FOUND |
| ?8C? | ERROR_NO_FREE_UIF |
| ?8D? | ERROR_MAX_UIF |
| ?8E? | ERROR_LEVEL |
| ?8F? | ERROR_KEY |
| ?90? | ERROR_AUTHENTICATION |
| ?91? | ERROR_FLASH_SIGNATURE_METHOD |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 50 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe |
| 0x10 | VDO |
| 0x11 | Valeo |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine |
| 0x18 | Teves |
| 0x19 | Elektromatik Suedafrika |
| 0x20 | Becker |
| 0x21 | Preh |
| 0x22 | Alps |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto |
| 0x26 | MotoMeter |
| 0x27 | Delphi PHI |
| 0x28 | BERU (DODUCO) |
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
| 0x10 | Testbedingungen erfuellt |
| 0x11 | Testbedingungen noch nicht erfuellt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler wuerde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler wuerde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 12 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| yes | 1 |
| no | 0 |
| on | 1 |
| off | 0 |
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

<a id="table-speichersegment"></a>
### SPEICHERSEGMENT

Dimensions: 10 rows × 3 columns

| SEG_BYTE | SEG_NAME | SEG_TEXT |
| --- | --- | --- |
| 0x00 | LAR | linearAdressRange |
| 0x01 | ROMI | ROM / EPROM, internal |
| 0x02 | ROMX | ROM / EPROM, external |
| 0x03 | NVRAM | NV-RAM (characteristic zones, DTC memory |
| 0x04 | RAMIS | RAM, internal (short MOV) |
| 0x05 | RAMXX | RAM, external (x data MOV) |
| 0x06 | FLASH | Flash EPROM |
| 0x07 | UIFM | User Info Field Memory |
| 0x0B | RAMIL | RAM, internal (long MOV / Register) |
| 0xFF | ??? | unbekanntes Speichersegment |
