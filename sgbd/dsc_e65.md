# dsc_e65.prg

- Jobs: [64](#jobs)
- Tables: [20](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Dynamische Stabilitaets Control DSC E65 |
| ORIGIN | BMW EF-73 Kusch |
| REVISION | 1.09 |
| AUTHOR | BMW EF-73 Kusch |
| COMMENT | Robert Bosch DSC57 BMW_FAST |
| PACKAGE | 1.23 |
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
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default
- [C_CI_LESEN](#job-c-ci-lesen) - Codierindex lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9B Vehicle Manufacturer Coding Index oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_AEI_LESEN](#job-c-aei-lesen) - Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. Diag_Mode ist integriert KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default
- [C_AEI_SCHREIBEN](#job-c-aei-schreiben) - Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_AUFTRAG](#job-c-aei-auftrag) - Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [STATUS_RADGESCHWINDIGKEIT](#job-status-radgeschwindigkeit) - Radgeschwindigkeiten auslesen KWP2000: $21,$01 ReadDataByLocalIdentifier service Modus  : Default
- [STATUS_ANALOG](#job-status-analog) - Status Eingaenge ABS_DSC57
- [STATUS_DIGITAL](#job-status-digital) - Status Eingaenge ABS_DSC57
- [STATUS_CAN](#job-status-can) - Status CAN ABS_DSC57
- [STATUS_4_DRUCKWERTE](#job-status-4-druckwerte) - 4 aufeinanderfolgende Druckwerte
- [COD_LESEN](#job-cod-lesen) - Auslesen der Codierdaten KWP2000: $22 ReadDataByCommonIdentifier $3000 Codierdaten Modus  : Default
- [COD_SCHREIBEN](#job-cod-schreiben) - Codierdaten schreiben Es muessen 2 Codierbytes als ein Hex_String uebergeben werden Argument: z.B.: 01,13 die CS wird in der ECU berechnet KWP2000: $2E WriteDataByCommonIdentifier $3000 codingDataSet Modus  : Default
- [TEST_AUTO_COD](#job-test-auto-cod) - Autocodierung wird ausgeloest
- [TEST_LZA_FLR](#job-test-lza-flr) - Verbot Langzeitabgleich LZA und Verbot Fahrleistungsreduzierung FLR aktivieren/deaktiviern Es koennen 0,1 oder 2 Argumente uebergeben werden Bsp: "LZA" und/oder "FLR" (durch Strichpunkt getrennt) wird kein Argument uebergeben, dann werden beide Funktionen wieder deaktiviert die CS der Codierbytes wird von der ECU berechnet Diag_Mode ist im Job integriert KWP2000: $2E WriteDataByCommonIdentifier $3000 codingDataSet Modus  : Default
- [TEST_QUERBESCHLEUNIGUNG](#job-test-querbeschleunigung) - wird nur beim Sensorwechsel angewandt setzt die gelernten Werte (Offset) wieder auf 0
- [TEST_DRUCK](#job-test-druck) - wird nur beim Sensorwechsel angewandt setzt die gelernten Werte (Offset) wieder auf 0
- [TEST_LENKWINKEL](#job-test-lenkwinkel) - wird nur beim Sensorwechsel angewandt setzt die gelernten Werte (Offset) wieder auf 0
- [TEST_DREHRATE](#job-test-drehrate) - wird nur beim Sensorwechsel angewandt setzt die gelernten Werte (Offset DRS_Empfindlichkeit und Offset_Giergeschwindigkeit) wieder auf 0
- [STEUERN_D_STELLGLIED](#job-steuern-d-stellglied) - Digitale Stellglieder ansteuern ABS_DSC57
- [STEUERN_D4_STELLGLIED](#job-steuern-d4-stellglied) - Digitale Stellglieder ansteuern ABS_DSC57
- [TEST_EEPROM_LESEN](#job-test-eeprom-lesen) - Lesen EEPROM_DATEN
- [TEST_EEPROM_SCHREIBEN](#job-test-eeprom-schreiben) - Schreiben EEPROM_DATEN
- [STEUERN_DREHZAHLFUEHLER_IMPULS](#job-steuern-drehzahlfuehler-impuls) - Test Fuehler u. Impulsrad
- [STEUERN_DREHZAHLFUEHLER_ALLE](#job-steuern-drehzahlfuehler-alle) - Alle Ansprechschwellen u. Impulsraeder ABS_DSC57
- [TEST_FS_SCHREIBEN](#job-test-fs-schreiben) - Fehlerspeicher zuruecksetzen
- [STEUERN_AKTUATORIK](#job-steuern-aktuatorik) - Statischer Test der Komponenten ABS_DSC57
- [FS_LESEN_SAR](#job-fs-lesen-sar) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [TEST_VAKUUM](#job-test-vakuum) - Digitale Stellglieder ansteuern ABS_DSC57 KWP2000: $31 StartRoutineByLocalIdentifier $FA Testprogramm Start Modus  : Default
- [TEST_VAKUUM_PUMPE](#job-test-vakuum-pumpe) - Digitale Stellglieder ansteuern ABS_DSC57 KWP2000: $31 StartRoutineByLocalIdentifier $FA Testprogramm Start Modus  : Default
- [IDENT_VIN](#job-ident-vin) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [IDENT_BOSCH_HW_NR](#job-ident-bosch-hw-nr) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [IDENT_BOSCH_SW_BB_NR](#job-ident-bosch-sw-bb-nr) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [IDENT_BOSCH_SW_VERSION_NR](#job-ident-bosch-sw-version-nr) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [IDENT_SCHREIBEN](#job-ident-schreiben) - KWP2000: $3B WriteDataByLocalIdentifier $80 BMW Identifikation schreiben
- [FS_LESEN_RB](#job-fs-lesen-rb) - Lesen FS EEPROM_DATEN
- [BBV_INI](#job-bbv-ini) - Setzt alle CBS EEPROM Daten auf 100% (Neuzustand)
- [BBV_CORR_FAKTOR](#job-bbv-corr-faktor) - Setzt die/den Korrekturfaktor(en) der VA und/oder der HA auf den Wert 0x20, dies entspricht dem Neuzustand Es koennen 0,1 oder 2 Argumente uebergeben werden Bsp: "VA" oder "VA_11" und/oder "HA" (durch Strichpunkt getrennt) wird kein Argument uebergeben, dann werden die alten Korrekturfaktoren beibehalten Sonderfall: "VA_11" setzt den  Korrekturfaktor an der VA auf den Wert 1.1 (E67) die CS wird von der SGBD berechnet Diag_Mode und Download ist im Job integriert
- [STATUS_FS_EEPROM](#job-status-fs-eeprom) - Lesen FS EEPROM_DATEN
- [STATUS_BBV](#job-status-bbv) - Lesen  EEPROM_DATEN
- [STATUS_SENSOR_ADAPTION](#job-status-sensor-adaption) - Lesen  EEPROM_DATEN
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (frueher BOS Daten) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (frueher BOS Daten) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
- [_FS_LESEN_INPA](#job-fs-lesen-inpa) - KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes KWP2000: $18 ReadDiagnosticTroubleCodesByStatus kombinierter Job §17 und §18 Fehlerspeicher lesen mit allen Umweltdaten Ausgabe der Results wie INPA

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

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default

_No arguments._

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

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. Diag_Mode ist integriert KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default

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
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

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
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

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
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-c-aei-schreiben"></a>
### C_AEI_SCHREIBEN

Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-c-aei-auftrag"></a>
### C_AEI_AUFTRAG

Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

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
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

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
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-status-radgeschwindigkeit"></a>
### STATUS_RADGESCHWINDIGKEIT

Radgeschwindigkeiten auslesen KWP2000: $21,$01 ReadDataByLocalIdentifier service Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RAD_GESCHW_VL_WERT | long | Radgeschwindigkeit vorne links |
| STAT_RAD_GESCHW_VR_WERT | long | Radgeschwindigkeit vorne rechts |
| STAT_RAD_GESCHW_HL_WERT | long | Radgeschwindigkeit hinten links |
| STAT_RAD_GESCHW_HR_WERT | long | Radgeschwindigkeit hinten rechts |
| STAT_RAD_GESCHW_EINH | string | Einheit = km/h |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Status Eingaenge ABS_DSC57

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_LENKWINKEL_WERT | real | Lenkwinekl in Grad, kann + u.- Wert haben |
| STAT_LENKWINKEL_EINH | string | Einheit = Winkelgrad |
| STAT_DREHRATE_WERT | real | Drehrate in Winkelgrad/sec |
| STAT_DREHRATE_EINH | string | Einheit = Winkelgrad/sec |
| STAT_DRUCK_WERT | real | Druck in bar, kann + u.- Wert haben |
| STAT_DRUCK_EINH | string | Einheit = bar |
| STAT_QUERBESCHLEUNIGUNG_WERT | real | Querbeschleunigung , kann + u.- Wert haben |
| STAT_QUERBESCHLEUNIGUNG_EINH | string | Einheit = m/(s*s) |
| STAT_DSC_PASSIVTASTER_EIN | real | Schlupfschwellenumschalter in V |
| STAT_DSC_PASSIVTASTER_EINH | string | Einheit = 0/1 |
| STAT_BREMSLICHTSCHALTER_SPANNUNG_WERT | real |  |
| STAT_BREMSLICHTSCHALTER_SPANNUNG_EINH | string | Einheit = V |
| STAT_ZUENDUNG_WERT | real | Spannung Kl. 15 in V |
| STAT_ZUENDUNG_EINH | string | Einheit = V |
| STAT_PUMPENMOTOR_SPANNUNG_WERT | real | Spannung Pumpenmotor in Volt |
| STAT_PUMPENMOTOR_SPANNUNG_EINH | string | Einheit = V |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status Eingaenge ABS_DSC57

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_LWS_SIGN_EINGEFROREN_EIN | int | 0 oder 1 |
| STAT_BREMSLICHTSCHALTER_EIN | int | 0 oder 1 |
| STAT_BREMSFLUESSIGKEIT_NIVEAU_EIN | int | 0 oder 1 |
| STAT_DSC_PASSIVTASTER_EIN | int | 0 oder 1 |
| STAT_EVVL_EIN | int | 0 oder 1 |
| STAT_AVVL_EIN | int | 0 oder 1 |
| STAT_EVHR_EIN | int | 0 oder 1 |
| STAT_AVHR_EIN | int | 0 oder 1 |
| STAT_EVVR_EIN | int | 0 oder 1 |
| STAT_AVVR_EIN | int | 0 oder 1 |
| STAT_EVHL_EIN | int | 0 oder 1 |
| STAT_AVHL_EIN | int | 0 oder 1 |
| STAT_UMSCHALTVENTIL_VORDERACHSE_EIN | int | 0 oder 1 |
| STAT_UMSCHALTVENTIL_HINTERACHSE_EIN | int | 0 oder 1 |
| STAT_VORLADEVENTIL_VORDERACHSE_EIN | int | 0 oder 1 |
| STAT_VORLADEVENTIL_HINTERACHSE_EIN | int | 0 oder 1 |
| STAT_VORLADEPUMPE_1_EIN | int | 0 oder 1 |
| STAT_VORLADEPUMPE_2_EIN | int | 0 oder 1 |
| STAT_VENTIL_RELAIS_EIN | int | 0 oder 1 |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-can"></a>
### STATUS_CAN

Status CAN ABS_DSC57

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_MOTORDREHZAHL_WERT | real | Momentane Motordrehzahl in 1/min |
| STAT_MOTORDREHZAHL_EINH | string | Einheit = 1/min |
| STAT_LENKWINKEL_WERT | real | Einschlag Lenkrad [Grad] |
| STAT_LENKWINKEL_EINH | string | [Grad] |
| STAT_VERZOEGERUNGS_ANFORD_EMF_WERT | real | Einschlag Lenkrad [Grad] |
| STAT_VERZOEGERUNGS_ANFORD_EMF_EINH | string | [m/s2] |
| STAT_VERZOEGERUNGS_ANFORD_ACC_WERT | real | Einschlag Lenkrad [Grad] |
| STAT_VERZOEGERUNGS_ANFORD_ACC_EINH | string | [m/s2] |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-4-druckwerte"></a>
### STATUS_4_DRUCKWERTE

4 aufeinanderfolgende Druckwerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_DRUCK_WERT_1 | real | Druck in bar, kann + u.- Wert haben |
| STAT_DRUCK_WERT_2 | real | Druck in bar, kann + u.- Wert haben |
| STAT_DRUCK_WERT_3 | real | Druck in bar, kann + u.- Wert haben |
| STAT_DRUCK_WERT_4 | real | Druck in bar, kann + u.- Wert haben |
| STAT_DRUCK_EINH | string | Einheit = bar |

<a id="job-cod-lesen"></a>
### COD_LESEN

Auslesen der Codierdaten KWP2000: $22 ReadDataByCommonIdentifier $3000 Codierdaten Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cod-schreiben"></a>
### COD_SCHREIBEN

Codierdaten schreiben Es muessen 2 Codierbytes als ein Hex_String uebergeben werden Argument: z.B.: 01,13 die CS wird in der ECU berechnet KWP2000: $2E WriteDataByCommonIdentifier $3000 codingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| C_BYTES | string | Bereich: 00 - FF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary |  |

<a id="job-test-auto-cod"></a>
### TEST_AUTO_COD

Autocodierung wird ausgeloest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-lza-flr"></a>
### TEST_LZA_FLR

Verbot Langzeitabgleich LZA und Verbot Fahrleistungsreduzierung FLR aktivieren/deaktiviern Es koennen 0,1 oder 2 Argumente uebergeben werden Bsp: "LZA" und/oder "FLR" (durch Strichpunkt getrennt) wird kein Argument uebergeben, dann werden beide Funktionen wieder deaktiviert die CS der Codierbytes wird von der ECU berechnet Diag_Mode ist im Job integriert KWP2000: $2E WriteDataByCommonIdentifier $3000 codingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_1 | string | "LZA" oder "FLR" oder kein Argument |
| ARG_2 | string | "LZA" oder "FLR" oder kein Argument |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary |  |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-test-querbeschleunigung"></a>
### TEST_QUERBESCHLEUNIGUNG

wird nur beim Sensorwechsel angewandt setzt die gelernten Werte (Offset) wieder auf 0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-druck"></a>
### TEST_DRUCK

wird nur beim Sensorwechsel angewandt setzt die gelernten Werte (Offset) wieder auf 0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-lenkwinkel"></a>
### TEST_LENKWINKEL

wird nur beim Sensorwechsel angewandt setzt die gelernten Werte (Offset) wieder auf 0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-drehrate"></a>
### TEST_DREHRATE

wird nur beim Sensorwechsel angewandt setzt die gelernten Werte (Offset DRS_Empfindlichkeit und Offset_Giergeschwindigkeit) wieder auf 0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_AUFTRAG_1 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |
| _TEL_ANTWORT3 | binary | Antworttelegramm |

<a id="job-steuern-d-stellglied"></a>
### STEUERN_D_STELLGLIED

Digitale Stellglieder ansteuern ABS_DSC57

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| BEFEHL_1 | string | Ein = FF, Aus = 00 |
| ST_1 | string | Stellglied 1 |
| BEFEHL_2 | string | Ein = FF, Aus = 00 |
| ST_2 | string | Stellglied 2 |
| W_ZEIT | int | Wartezeit vor Ansteuerung 3. u. 4. Stellglied |
| BEFEHL_3 | string | Ein = FF, Aus = 00 |
| ST_3 | string | Stellglied 3 |
| BEFEHL_4 | string | Ein = FF, Aus = 00 |
| ST_4 | string | Stellglied 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_AUFTRAG2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |

<a id="job-steuern-d4-stellglied"></a>
### STEUERN_D4_STELLGLIED

Digitale Stellglieder ansteuern ABS_DSC57

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| BEFEHL_1 | string | Ein = FF, Aus = 00 |
| ST_1 | string | Stellglied 1 |
| BEFEHL_2 | string | Ein = FF, Aus = 00 |
| ST_2 | string | Stellglied 2 |
| BEFEHL_3 | string | Ein = 01, Aus = 00 |
| ST_3 | string | Stellglied 3 |
| BEFEHL_4 | string | Ein = 01, Aus = 00 |
| ST_4 | string | Stellglied 4 |
| W_ZEIT | int | Wartezeit vor Ansteuerung  Stellglied 5-8 |
| BEFEHL_5 | string | Ein = 01, Aus = 00 |
| ST_5 | string | Stellglied 5 |
| BEFEHL_6 | string | Ein = 01, Aus = 00 |
| ST_6 | string | Stellglied 6 |
| BEFEHL_7 | string | Ein = 01, Aus = 00 |
| ST_7 | string | Stellglied 7 |
| BEFEHL_8 | string | Ein = 01, Aus = 00 |
| ST_8 | string | Stellglied 8 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_AUFTRAG2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-eeprom-lesen"></a>
### TEST_EEPROM_LESEN

Lesen EEPROM_DATEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT | string | Adresse u. Anzahl |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RESULT | string | Status EEPROM Zugriff |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| DATEN | binary | Status EEPROM Zugriff |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |
| _TEL_ANTWORT3 | binary | Antworttelegramm |

<a id="job-test-eeprom-schreiben"></a>
### TEST_EEPROM_SCHREIBEN

Schreiben EEPROM_DATEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | Adresse,Anzahl,Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |

<a id="job-steuern-drehzahlfuehler-impuls"></a>
### STEUERN_DREHZAHLFUEHLER_IMPULS

Test Fuehler u. Impulsrad

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAD_NR | string | Radnummer |
| A_ZEIT | int | Ausfuehrungszeit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| GESCHW_V1 | long | Radgeschwindigkeit bei Beginn d. Tests |
| GESCHW_V2 | long | Radgeschwindigkeit waehrend Test |
| GESCHW_EINH | string | Einheit = km/h |
| _TEL_AUFTRAG3 | binary | Anforderungstelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT3 | binary | Antworttelegramm |
| _TEL_ANTWORT4 | binary | Antworttelegramm |

<a id="job-steuern-drehzahlfuehler-alle"></a>
### STEUERN_DREHZAHLFUEHLER_ALLE

Alle Ansprechschwellen u. Impulsraeder ABS_DSC57

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| A_ZEIT | int | Ausfuehrungszeit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| VR_MIN | long | Radgeschwindigkeit vorne rechts min |
| VR_MAX | long | Radgeschwindigkeit vorne rechts max |
| VL_MIN | long | Radgeschwindigkeit vorne links min |
| VL_MAX | long | Radgeschwindigkeit vorne rechts max |
| HR_MIN | long | Radgeschwindigkeit hinten rechts min |
| HR_MAX | long | Radgeschwindigkeit hinten rechts max |
| HL_MIN | long | Radgeschwindigkeit hinten links min |
| HL_MAX | long | Radgeschwindigkeit hinten links max |
| GESCHW_EINH | string | Einheit = km/h |
| _TEL_AUFTRAG3 | binary | Anforderungstelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT3 | binary | Antworttelegramm |
| _TEL_ANTWORT4 | binary | Antworttelegramm |

<a id="job-test-fs-schreiben"></a>
### TEST_FS_SCHREIBEN

Fehlerspeicher zuruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| FS_STATUS | string | Fehlerstatus |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT3 | binary | Antworttelegramm |

<a id="job-steuern-aktuatorik"></a>
### STEUERN_AKTUATORIK

Statischer Test der Komponenten ABS_DSC57

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| WARTEZEIT | int | Wartezeit in msec |
| WARTEZEIT_EINH | string | Einheit = msec |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |
| _TEL_ANTWORT3 | binary | Antworttelegramm |
| _TEL_ANTWORT4 | binary | Antworttelegramm |

<a id="job-fs-lesen-sar"></a>
### FS_LESEN_SAR

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-test-vakuum"></a>
### TEST_VAKUUM

Digitale Stellglieder ansteuern ABS_DSC57 KWP2000: $31 StartRoutineByLocalIdentifier $FA Testprogramm Start Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-test-vakuum-pumpe"></a>
### TEST_VAKUUM_PUMPE

Digitale Stellglieder ansteuern ABS_DSC57 KWP2000: $31 StartRoutineByLocalIdentifier $FA Testprogramm Start Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-ident-vin"></a>
### IDENT_VIN

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-bosch-hw-nr"></a>
### IDENT_BOSCH_HW_NR

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_TT_NR | string | RB-Teilenummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-bosch-sw-bb-nr"></a>
### IDENT_BOSCH_SW_BB_NR

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BB_NR | string | RB-BB-Nummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-bosch-sw-version-nr"></a>
### IDENT_BOSCH_SW_VERSION_NR

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_RB_SW_NR | int | RB-SW-Nummer |
| ID_RB_SW_DATUM | long | RB-SW-Datum |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-schreiben"></a>
### IDENT_SCHREIBEN

KWP2000: $3B WriteDataByLocalIdentifier $80 BMW Identifikation schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muessen 17 Ident_Daten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 18 Bereich:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-rb"></a>
### FS_LESEN_RB

Lesen FS EEPROM_DATEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| F_ZAHL | int | Anzahl Fehler |
| F_ORT_TEXT_RB | string | Fehlerort als Text |
| F_CODE_RB | string | Fehlerort als Text |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-bbv-ini"></a>
### BBV_INI

Setzt alle CBS EEPROM Daten auf 100% (Neuzustand)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG3 | binary | Anforderungstelegramm |
| _TEL_AUFTRAG4 | binary | Anforderungstelegramm |
| _TEL_AUFTRAG5 | binary | Anforderungstelegramm |
| _TEL_AUFTRAG6 | binary | Anforderungstelegramm |
| _TEL_AUFTRAG7 | binary | Anforderungstelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |
| _TEL_ANTWORT3 | binary | Antworttelegramm |
| _TEL_ANTWORT4 | binary | Antworttelegramm |
| _TEL_ANTWORT5 | binary | Antworttelegramm |
| _TEL_ANTWORT6 | binary | Antworttelegramm |
| _TEL_ANTWORT7 | binary | Antworttelegramm |

<a id="job-bbv-corr-faktor"></a>
### BBV_CORR_FAKTOR

Setzt die/den Korrekturfaktor(en) der VA und/oder der HA auf den Wert 0x20, dies entspricht dem Neuzustand Es koennen 0,1 oder 2 Argumente uebergeben werden Bsp: "VA" oder "VA_11" und/oder "HA" (durch Strichpunkt getrennt) wird kein Argument uebergeben, dann werden die alten Korrekturfaktoren beibehalten Sonderfall: "VA_11" setzt den  Korrekturfaktor an der VA auf den Wert 1.1 (E67) die CS wird von der SGBD berechnet Diag_Mode und Download ist im Job integriert

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VA | string | Setzt den Korrekturfaktor der Vorderachse auf den Wert 1 entspricht Neuzustand |
| HA | string | Setzt den Korrekturfaktor der Hinterachse auf den Wert 1 entspricht Neuzustand |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |
| _TEL_ANTWORT3 | binary | Antworttelegramm |

<a id="job-status-fs-eeprom"></a>
### STATUS_FS_EEPROM

Lesen FS EEPROM_DATEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS | string | Status EEPROM Zugriff |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_F_ORT_TEXT_RB | string | Fehlerort als Text |
| STAT_F_CODE_RB | string | Fehlerort als Text |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-bbv"></a>
### STATUS_BBV

Lesen  EEPROM_DATEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RESULT | string | Status EEPROM Zugriff |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_BBV_DICKE_VA_1 | long | Bremsbelagdicke |
| STAT_BBV_DICKE_VA_2 | long | Bremsbelagdicke |
| STAT_BBV_DICKE_HA_1 | long | Bremsbelagdicke |
| STAT_BBV_DICKE_HA_2 | long | Bremsbelagdicke |
| STAT_BBV_PARA_KORR_VA | long | Parameterkorrekturfaktor |
| STAT_BBV_PARA_KORR_HA | long | Parameterkorrekturfaktor |
| STAT_BBV_GLL_VA | long | Gesamtlaufleistung |
| STAT_BBV_GLL_HA | long | Gesamtlaufleistung |
| STAT_EN_INFO_1_VA | int |  |
| STAT_EN_INFO_2_VA | int |  |
| STAT_EN_INFO_1_HA | int |  |
| STAT_EN_INFO_2_HA | int |  |
| STAT_INFO_1_VA | int |  |
| STAT_INFO_2_VA | int |  |
| STAT_INFO_1_HA | int |  |
| STAT_INFO_2_HA | int |  |
| STAT_GLL_STEP | int |  |
| STAT_BITS_EE_POK | int |  |
| STAT_SERV_REQ_VA | int |  |
| STAT_SERV_REQ_HA | int |  |
| STAT_GLL_OFF_VA_1 | int |  |
| STAT_GLL_OFF_VA_2 | int |  |
| STAT_GLL_OFF_HA_1 | int |  |
| STAT_GLL_OFF_HA_2 | int |  |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-sensor-adaption"></a>
### STATUS_SENSOR_ADAPTION

Lesen  EEPROM_DATEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RESULT | string | Status EEPROM Zugriff |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_RTA_VR | long |  |
| STAT_RTA_HL | long |  |
| STAT_RTA_HR | long |  |
| STAT_DRS_OFFSET | long |  |
| STAT_DRS_EMPF | long |  |
| STAT_LWS_OFFSET | long |  |
| STAT_AY_OFFSET | long |  |
| STAT_PVOR_OFFSET | long |  |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-cbs-daten-lesen"></a>
### CBS_DATEN_LESEN

CBS Daten auslesen (frueher BOS Daten) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Hex-String |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| ID_FN_BOS_MESS_WERT | int | CBS-Kennung als Zahl |
| ID_FN_BOS_MESS_HEX | string | CBS-Kennung als Hex-String |
| ID_FN_BOS_MESS_TEXT | string | table CbsKennung CBS_K CBS_K_TEXT CBS-Kennung im Klartext |
| RMMI_BOS_WERT | int | Restlaufleistung |
| RMMI_BOS_EINH | string | km |
| ST_UN_BOS_WERT | int | Einheit Restlaufleistung als Zahl |
| ST_UN_BOS_HEX | string | Einheit Restlaufleistung als Hex-String |
| ST_UN_BOS_TEXT | string | Einheit Restlaufleistung im Klartext |
| COU_RSTG_BOS_MESS_WERT | int | Servicezaehler |
| COU_RSTG_BOS_MESS_EINH | string | Zaehler |
| AVAI_BOS_WERT | int | Verfügbarkeit in % |
| AVAI_BOS_EINH | string | % |
| AVAI_BOS_WERT_OEL | int | Verfügbarkeit OEL in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_FILT | int | Verfügbarkeit FILT in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_BR_V | int | Verfügbarkeit BR_V in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_BR_H | int | Verfügbarkeit BR_H in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_BRFL | int | Verfügbarkeit BRFL in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_ZKRZ | int | Verfügbarkeit ZKRZ in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_SIC | int | Verfügbarkeit SIC in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_KFL | int | Verfügbarkeit KFL in %, für Prüfablauf Bandende |
| ZIEL_MM_WERT | int | Ziel-Monat (HU/AU) |
| ZIEL_MM_EINH | string | Monat |
| ZIEL_YY_WERT | int | Ziel-Jahr (HU/AU) |
| ZIEL_YY_EINH | string | Jahr |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbs-reset"></a>
### CBS_RESET

CBS Daten Zuruecksetzen (frueher BOS Daten) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BOS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte: Oel, Br_v, Brfl, Filt, Batt, Br_h, ZKrz, Sic, Kfl, TUV, AU Defaultwert: 0x00 (ungueltig) |
| BOS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, kein Rueckstellen: 255 Defaultwert: 100 |
| BOS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, keine Aenderung: 31 Defaultwert: 31 |
| BOS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter fuer Monat, keine Aenderung: 255 Defaultwert: 255 |
| BOS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter fuer Jahr, keine Aenderung: 255 Defaultwert: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-inpa"></a>
### _FS_LESEN_INPA

KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes KWP2000: $18 ReadDiagnosticTroubleCodesByStatus kombinierter Job §17 und §18 Fehlerspeicher lesen mit allen Umweltdaten Ausgabe der Results wie INPA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_CODE | string | Fehlercode(hex) |
| F_TEXT | string | Fehlerort als Text |
| F_ZAHL | int | Anzahl Fehler |
| F_READY_TEXT | string | 1. Fehlerart als Text table FArtTexte ARTTEXT |
| F_VORH_TEXT | string | 2. Fehlerart als Text table FArtTexte ARTTEXT |
| F_WARNUNG_TEXT | string | 3. Fehlerart als Text table FArtTexte ARTTEXT |
| HAEUFIGKZAEHLER | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| LOGISTIKZAEHLER | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| KILOMETERSTAND_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| GESCHWINDIGKEIT_KMH | long | Radgeschwindigkeit vRef |
| ACB_ACTIVE_CONTROL_BRAKE | int |  |
| DBC_DYNAMIC_BRAKE_CONTROL | int |  |
| ECD_VERZOEGERUNGSANFORDERUNG_ACC | int |  |
| HDC_RESERVIERT_FUER_DXC | int |  |
| DSC_DYNAMIC_STABILITY_CONTROL | int |  |
| ABS_ANTI_BLOCKIER_SYSTEM | int |  |
| BLS_BREMSLICHTSCHALTER | int |  |
| ASC_AUTOMATIC_STABILITY_CONTROL | int |  |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (67 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [CBSKENNUNG](#table-cbskennung) (13 × 3)
- [FORTTEXTE](#table-forttexte) (94 × 2)
- [RB_FORTTEXTE](#table-rb-forttexte) (204 × 6)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [DIGITAL](#table-digital) (1 × 9)
- [FUMWELTTEXTE](#table-fumwelttexte) (9 × 9)
- [STG_TABELLE](#table-stg-tabelle) (20 × 2)
- [E_A_STATUS](#table-e-a-status) (2 × 2)
- [RAD_NR_TABELLE](#table-rad-nr-tabelle) (4 × 2)
- [BOSKENNUNG](#table-boskennung) (11 × 3)

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

Dimensions: 67 rows × 2 columns

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

Dimensions: 16 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
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

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 13 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x04 | Filt | Mikrofilter |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x07 | DiFi | Dieselpartikelfilter |
| 0x08 | Batt | Batterie |
| 0x10 | ZKrz | Zuendkerzen |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x12 | Kfl | Kuehlfluessigkeit |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 94 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5E90 | Drehzahlfuehler hinten links Plausibilitaet |
| 0x5E91 | Drehzahlfuehler hinten rechts Plausibilitaet |
| 0x5E92 | Drehzahlfuehler vorne rechts Plausibilitaet |
| 0x5E93 | Drehzahlfuehler vorne links Plausibilitaet |
| 0x5E9A | Ventilrelais Fehler |
| 0x5E9B | Rueckfoerderpumpe: (Langzeit-)Ueberwachung |
| 0x5EA1 | Steuergeraet Fehler intern |
| 0x5EA3 | Codierungs Fehler |
| 0x5EA4 | Lambda Fehler: Radschlupf |
| 0x5EAA | Drehzahlfuehler hinten links Leitungsfehler |
| 0x5EAB | Drehzahlfuehler hinten rechts Leitungsfehler |
| 0x5EAC | Drehzahlfuehler vorne rechts Leitungsfehler |
| 0x5EAD | Drehzahlfuehler vorne links Leitungsfehler |
| 0x5EAE | ASC Umschaltventil Vorderachse |
| 0x5EB5 | Lenkwinkel Sensor Plausibilitaet |
| 0x5EBB | Ventil Auslass hinten links |
| 0x5EBC | Ventil Auslass hinten rechts |
| 0x5EBD | Ventil Auslass vorne rechts |
| 0x5EBE | Ventil Auslass vorne links |
| 0x5EBF | Ventil Einlass hinten links |
| 0x5EC0 | Ventil Einlass hinten rechts |
| 0x5EC1 | Ventil Einlass vorne rechts |
| 0x5EC2 | Ventil Einlass vorne links |
| 0x5EC3 | Vorlade Ventil Vorderachse |
| 0xD347 | CAN Fehler: Bus off, CAN Botschaft zu kurz |
| 0x5EC6 | CAN Botschaftsfehler: Getriebe sendet nicht |
| 0x5EC7 | DMER1 CAN Botschaftsfehler |
| 0x5ECB | Lambda Fehler: v-Vergleich |
| 0x5ECC | Lambda Fehler: Dauerregelung |
| 0x5ED0 | DSC passiv, Einstreuung auf Uz |
| 0x5ED1 | DMER2 CAN Botschaftsfehler |
| 0x5EDD | Druck Sensor: Leitungsueberpruefung |
| 0x5EE0 | Drehraten Sensor: Plausibilitaet |
| 0x5EE2 | ASC Umschaltventil Hinterachse |
| 0x5EE3 | Vorlade Ventil Hinterachse |
| 0x5EE4 | Vorladepumpe: Unterbrechung,Kurzschluss,Kleber |
| 0x5EE5 | Unterspannung |
| 0x5EE6 | zeitbegrenzte Passivschaltung: LWS Initialisierung |
| 0x5EE7 | Lenkwinkel Sensor: fehlende CAN Botschaft |
| 0x5EE8 | Druck Sensor (Plausibilitaet Vorladepumpe) |
| 0x5EEA | Drehraten Sensor: statischer Initialierungstest (Bite), dynamische Testauswertung |
| 0x5EEE | zeitbegrenzte Passivschaltung: Bremse drucklos |
| 0x5EEF | zeitbegrenzte Passivschaltung: Dauerregelung |
| 0x5EF3 | Lenkwinkel Sensor: Aufsetzalgorithmus |
| 0x5EF4 | Lenkwinkel Sensor: Steuergeraet intern |
| 0x5EF5 | Bremslichtschalter: Pruefung ueber Plausibilitaet Drucksensor |
| 0x5EF6 | Querbeschleunigungs Sensor: Plausibilitaet, ausserhalb gueltigem Bereich |
| 0x5EF7 | Drehraten Sensor: Gradient |
| 0x5EF8 | SN-Ueberwachung, Niveau Bremsfluessigkeit |
| 0x5EF9 | Bandendetest |
| 0x5EFA | Ueberspannung |
| 0x5EFB | CAN Botschaft: Quittierung ASC kommt nicht |
| 0x5EFE | Druck Sensor (Offset) |
| 0x5EFF | Druck Sensor Einstreuung auf die Spannungsversorgung |
| 0x5F00 | Bremsschalter Fehler |
| 0x5F01 | Bremslichtschalter: dauerhaft aktiviert |
| 0x5F02 | Status DME: Interner Fehler DME |
| 0x5F04 | Drehraten Sensor: falsches Drehraten Signal erkannt |
| 0x5F05 | Drehraten Sensor: Plausibilitaet falsches Drehraten Signal mit Warnlampenansteuerung |
| 0x5F06 | ACC CAN Botschaftsfehler |
| 0x5F07 | ACC Verzoegerungsanforderung Plausibilitaet |
| 0x5F08 | ACC hat abgeschaltet, keine Aenderung Alive Zaehler |
| 0x5F0B | Raddrehzahl Plausibilitaet |
| 0x5F0D | DMER3 CAN Botschaftsfehler |
| 0x5F0E | Drehraten Sensor: CAN Botschaftsfehler |
| 0x5F11 | CS820 Vorsorgungsspannung Sensoren |
| 0x5F12 | CAN Botschaftsfehler EMF |
| 0x5F13 | CAN Botschaftsfehler ARS |
| 0x5F14 | CAN Botschaftsfehler CAS |
| 0x5F15 | CAN Botschaftsfehler Kombi |
| 0x5F16 | zeitbegrenzte Passivschaltung: DRS Initialisierung |
| 0x5F17 | Drehzahlfuehler vorne links falscher Typ |
| 0x5F18 | Drehzahlfuehler vorne links Luftspalt zu gross |
| 0x5F19 | Drehzahlfuehler vorne links Spannungsversorgung oder Signalqualitaet |
| 0x5F20 | Drehzahlfuehler hinten links falscher Typ |
| 0x5F21 | Drehzahlfuehler hinten links Luftspalt zu gross |
| 0x5F22 | Drehzahlfuehler hinten links Spannungsversorgung oder Signalqualitaet |
| 0x5F23 | Fahrleistungsreduzierung |
| 0x5F24 | EMF Fehler Ueberhitzungsgefahr fuer Halbleiterrelais |
| 0x5F25 | EMF Fehler Halbleiterrelais ueberhitzt |
| 0x5F1A | Drehzahlfuehler hinten rechts falscher Typ |
| 0x5F1B | Drehzahlfuehler hinten rechts Luftspalt zu gross |
| 0x5F1C | Drehzahlfuehler hinten rechts Spannungsversorgung oder Signalqualitaet |
| 0x5F1D | Drehzahlfuehler vorne rechts falscher Typ |
| 0x5F1E | Drehzahlfuehler vorne rechts Luftspalt zu gross |
| 0x5F1F | Drehzahlfuehler vorne rechts Spannungsversorgung oder Signalqualitaet |
| 0x5F26 | Bremsbelagverschleiss Servicemeldung VA unplausibel |
| 0x5F27 | Bremsbelagverschleiss Dicke VA &lt; 3mm |
| 0x5F28 | Bremsbelagverschleiss Servicemeldung HA unplausibel |
| 0x5F29 | Bremsbelagverschleiss Dicke HA &lt; 3mm |
| 0x5F2A | DME Signal ungueltig |
| 0x5F2B | Drehraten Sensor: ausbleibende Botschaft bei Zuendung aus waehrend der Fahrt |
| 0x5F0F | Drehraten Sensor: temporaerer Fehler |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-rb-forttexte"></a>
### RB_FORTTEXTE

Dimensions: 204 rows × 6 columns

| F_CODE_BMW | F_WORT | F_REG | F_BIT | F_ART | ORTTEXT |
| --- | --- | --- | --- | --- | --- |
| 0x5ea1 | 0x03c0 | 1 | 0 | 1e | ECU-Fehler: Wrong Code in one Controller |
| 0x5ea1 | 0x03a0 | 1 | 0 | 1d | ECU-Fehler: UDFI |
| 0x5ea1 | 0x0380 | 1 | 0 | 1c | ECU-Fehler: ROM |
| 0x5ea1 | 0x0360 | 1 | 0 | 1b | ECU-Fehler: RAM |
| 0x5ea1 | 0x0340 | 1 | 0 | 1a | ECU-Fehler: Can |
| 0x5ea1 | 0x0300 | 1 | 0 | 18 | ECU-Fehler: Stack Overflow |
| 0x5ea1 | 0x02e0 | 1 | 0 | 17 | ECU-Fehler: UZ intern Test, Spannungsteiler defekt |
| 0x5ea1 | 0x02c0 | 1 | 0 | 16 | ECU-Fehler: UZ intern, Spannungsteiler defekt |
| 0x5ea1 | 0x02a0 | 1 | 0 | 15 | ECU-Fehler: Ventile Nebenschluss |
| 0x5ea1 | 0x0280 | 1 | 0 | 14 | ECU-Fehler: SSIO Timeout |
| 0x5ea1 | 0x0260 | 1 | 0 | 13 | ECU-Fehler: SSIO Hardware |
| 0x5ea1 | 0x0240 | 1 | 0 | 12 | ECU-Fehler: Einstreu Ueberwachung |
| 0x5ea1 | 0x01e0 | 1 | 0 | 0f | ECU-Fehler: EPA for output is working properly |
| 0x5ea1 | 0x01a0 | 1 | 0 | 0d | ECU-Fehler: EPA for 1ms-softwaretimer not working properly |
| 0x5ea1 | 0x0180 | 1 | 0 | 0c | ECU-Fehler: Zyklus Zeit Ueberschreitung |
| 0x5ea1 | 0x0160 | 1 | 0 | 0b | ECU-Fehler: Redundanz Fehler |
| 0x5ea1 | 0x0140 | 1 | 0 | 0a | ECU-Fehler: AD Fehler (MS Vergleich) |
| 0x5ea1 | 0x0120 | 1 | 0 | 09 | ECU-Fehler: Digital Input (MS Vergleich) |
| 0x5ea1 | 0x00dc | 1 | 0 | 06 | ECU-Fehler: Ventilrelais-Kleber |
| 0x5ea1 | 0x0060 | 1 | 0 | 03 | ECU-Fehler: FSA Test: Enable high |
| 0x5ea1 | 0x0040 | 1 | 0 | 02 | ECU-Fehler: FSA Test: Enable low |
| 0x5ea1 | 0x0020 | 1 | 0 | 01 | ECU-Fehler: ohmsche Ueberwachung DF |
| 0x5ea1 | 0x003c | 1 | 0 | 01 | ECU-Fehler: CS820 DFA Output Monitor |
| 0x5ea1 | 0x0020 | 1 | 0 | 01 | ECU-Fehler: CS820 PWM Monitor |
| 0x5ea1 | 0x0020 | 1 | 0 | 01 | ECU-Fehler: CS820 Clock Monitor |
| 0x5ea1 | 0x0000 | 1 | 0 | 00 | ECU-Fehler: Watchdog Control |
| 0x5e9a | 0x06a0 | 1 | 1 | 15 | VR-Fehler: zieht nicht vor FSA Test |
| 0x5e9a | 0x04c0 | 1 | 1 | 06 | VR-Fehler: VR faellt ab im Zyklus, Spg Uvr zu hoch |
| 0x5e9a | 0x04a0 | 1 | 1 | 05 | VR-Fehler: VR faellt ab im Zyklus |
| 0x5e9a | 0x0480 | 1 | 1 | 04 | VR-Fehler: VR faellt ab im Zyklus |
| 0x5ef5 | 0x10ea | 1 | 4 | 07 | BLS-Fehler: Plausbilitaet DGS |
| 0x5f01 | 0x08c4 | 1 | 2 | 06 | BLS-Fehler: BLS dauerhaft eingeschaltet |
| 0x5f00 | 0xb100 | 6 | 4 | 08 | BS-Fehler: Motronic sendet Fehler (BS = Motronic Signal BLS) |
| 0x5edd | 0x1242 | 1 | 4 | 12 | DGS-Fehler: DGS Versorgungsspannung Out of Range |
| 0x5edd | 0x1202 | 1 | 4 | 10 | DGS-Fehler: Leitung |
| 0x5edd | 0x1182 | 1 | 4 | 0c | DGS-Fehler: Power On Selftest |
| 0x5eff | 0x113c | 1 | 4 | 09 | DS-Fehler: temp. Einstreuung auf DGU Versorgung  (Diag.Fehler only) |
| 0x5efe | 0x1108 | 1 | 4 | 08 | DGS-Fehler: Offset |
| 0x5ee8 | 0x1004 | 1 | 4 | 00 | DGS-Fehler: Plausbilitaet Vorladepumpe |
| 0x5ee7 | 0x160a | 1 | 5 | 10 | LWS-Fehler: Ausbleibende CAN-Botschaft 1  Lenkwinkelsensor |
| 0x5eb5 | 0x15e3 | 1 | 5 | 0f | LWS-Fehler: Plausibilitaet Modell 9, wrong LW-sign; incl. Sila-Memory |
| 0x5eb5 | 0x15c2 | 1 | 5 | 0e | LWS-Fehler: Plausibilitaet Modell 8, wrong LW-sign recognised |
| 0x5eb5 | 0x15a2 | 1 | 5 | 0d | LWS-Fehler: Plausibilitaet Modell 7, LW-signal frozen |
| 0x5eb5 | 0x1582 | 1 | 5 | 0c | LWS-Fehler: Bereich Signal |
| 0x5eb5 | 0x14c2 | 1 | 5 | 06 | LWS-Fehler: Gradienten |
| 0x5eb5 | 0x14a2 | 1 | 5 | 05 | LWS-Fehler: Plausibilitaet Modell 1, Offset Langzeitabgleich |
| 0x5eb5 | 0x1482 | 1 | 5 | 04 | LWS-Fehler: Plausibilitaet Modell 2, Plaus. Giergeschwindigkeit |
| 0x5ef4 | 0x1568 | 1 | 5 | 0b | LWS-interner Fehler: allgemeiner, interner Fehler LWS |
| 0x5ef4 | 0x1448 | 1 | 5 | 02 | LWS-Fehler: LWS-Status ungueltig |
| 0x5ef3 | 0x1406 | 1 | 5 | 00 | LWS-interner Fehler: Keine Initialisierung bei Fahrtantritt |
| 0x5f0e | 0x1b6e | 1 | 6 | 1b | DRS-Fehler: Ausbleibende CAN-Botschaft |
| 0x5f0e | 0x1b4e | 1 | 6 | 1a | CAN_DRS-Fehler: DRS meldet error |
| 0x5f0e | 0x1b0e | 1 | 6 | 18 | CAN_DRS-Fehler: DRS meldet calibrierung |
| 0x5f0e | 0x1aee | 1 | 6 | 17 | CAN_DRS-Fehler: IDB unplausibel |
| 0x5f0e | 0x1ace | 1 | 6 | 16 | CAN_DRS-Fehler: DRS Wert ausserhalb Spec |
| 0x5f0e | 0x19ee | 1 | 6 | 0f | CAN_DRS-Fehler: Sensor Flags toggeln dauerhaft |
| 0x5f0f | 0x1b3c | 1 | 6 | 19 | CAN_DRS-Fehler: temporaerer Fehler |
| 0x5f2b | 0x19d0 | 1 | 6 | 0e | DRS-Fehler: ausbleibende Botschaft bei Zuendung aus waehrend der Fahrt |
| 0x5f04 | 0x196a | 1 | 6 | 0b | DRS-Fehler: Plausibilitaet Modell 8, wrong DRS-sign recognised |
| 0x5f05 | 0x19ad | 1 | 6 | 0d | DRS-Fehler: Plausibilitaet Modell 9, wrong DRS-sign; with Sila-memory |
| 0x5eea | 0x1987 | 1 | 6 | 0c | DRS-Fehler: Statischer Initialisierungs Test |
| 0x5eea | 0x18a7 | 1 | 6 | 05 | DRS-Fehler: Bite-Empfindlichkeit (Dynamische Testauswertung) |
| 0x5ee0 | 0x1945 | 1 | 6 | 0a | DRS-Fehler: Plausbilitaet Modell 7, Plausibilitaet Lenkwinkel |
| 0x5ee0 | 0x1925 | 1 | 6 | 09 | DRS-Fehler: Bereich Signal |
| 0x5ee0 | 0x18e5 | 1 | 6 | 07 | DRS-Fehler: Plausbilitaet Modell 3, Offset Stillstandsabgleich |
| 0x5ee0 | 0x1885 | 1 | 6 | 04 | DRS-Fehler: Plausbilitaet Modell 2, Offset Schnellabgleich |
| 0x5ee0 | 0x1864 | 1 | 6 | 03 | DRS-Fehler: Plausbilitaet Modell 5, Empfindlichkeit Drehrate |
| 0x5ee0 | 0x1845 | 1 | 6 | 02 | DRS-Fehler: Plausbilitaet Modell 4, Offset Normalabgleich |
| 0x5ee0 | 0x1825 | 1 | 6 | 01 | DRS-Fehler: Plausbilitaet Modell (1) |
| 0x5ee0 | 0x1805 | 1 | 6 | 00 | DRS-Fehler: Plausbilitaet Modell 6, Sprung/wegdriftende Signale |
| 0x5ef7 | 0x18c9 | 1 | 6 | 06 | DRS-Fehler: Gradient |
| 0x5ef6 | 0x1ec4 | 1 | 7 | 16 | CAN_DRS-Fehler: AY Wert ausserhalb Spec |
| 0x5ef6 | 0x1d24 | 1 | 7 | 09 | AYS-Fehler: Anschlag |
| 0x5ef6 | 0x1ca4 | 1 | 7 | 05 | AYS-Fehler: Offset Langzeitabgleich |
| 0x5ef6 | 0x1c84 | 1 | 7 | 04 | AYS-Fehler: Offset Stillstand |
| 0x5ef6 | 0x1c24 | 1 | 7 | 01 | AYS-Fehler: Plausbilitaet Fz-Modell (innerhalb Modellgueltigkeit) |
| 0x5ef6 | 0x1c04 | 1 | 7 | 00 | AYS-Fehler: Plausbilitaet Fz-Modell (ausserhalb Modellgueltigkeit) |
| 0x5edf | 0x1e02 | 1 | 7 | 10 | AYS-Fehler: Leitung |
| 0x5ef0 | 0x1cc6 | 1 | 7 | 06 | AYS-Fehler: Gradient/ Offener Eingang am Clamp |
| 0x5ec2 | 0x2200 | 2 | 0 | 10 | Ventil-Fehler: EVVL |
| 0x5ebe | 0x2600 | 2 | 1 | 10 | Ventil-Fehler: AVVL |
| 0x5ec0 | 0x2a00 | 2 | 2 | 10 | Ventil-Fehler: EVHR |
| 0x5ebc | 0x2e00 | 2 | 3 | 10 | Ventil-Fehler: AVHR |
| 0x5ec1 | 0x3200 | 2 | 4 | 10 | Ventil-Fehler: EVVR |
| 0x5ebd | 0x3600 | 2 | 5 | 10 | Ventil-Fehler: AVVR |
| 0x5ebf | 0x3a00 | 2 | 6 | 10 | Ventil-Fehler: EVHL |
| 0x5ebb | 0x3e00 | 2 | 7 | 10 | Ventil-Fehler: AVHL |
| 0x5eae | 0x4a00 | 3 | 2 | 10 | Ventil-Fehler: USV1 |
| 0x5ee2 | 0x4e00 | 3 | 3 | 10 | Ventil-Fehler: USV2 |
| 0x5ec3 | 0x5200 | 3 | 4 | 10 | Ventil-Fehler: VLV1/HSV1 |
| 0x5ee3 | 0x5600 | 3 | 5 | 10 | Ventil-Fehler: VLV2/HSV2 |
| 0x5e9b | 0x5a03 | 3 | 6 | 10 | RFP-Fehler: Unterbrechung (laeuft nicht an) |
| 0x5e9b | 0x58e3 | 3 | 6 | 07 | RFP-Fehler: Langzeitueberwachung (laeuft standig) |
| 0x5e9b | 0x58c3 | 3 | 6 | 06 | RFP-Fehler: Nachlauf zu kurz     (steht zu schnell) |
| 0x5e9b | 0x58a3 | 3 | 6 | 05 | RFP-Fehler: PMRelais faellt ab im Zyklus (UM zu niedrig mit PMR Anst) |
| 0x5ee4 | 0x5e40 | 3 | 7 | 12 | VLP-Fehler: Highside Schalter VLP(-) |
| 0x5ee4 | 0x5e20 | 3 | 7 | 11 | VLP-Fehler: Masse Schalter VLP(-) |
| 0x5ee4 | 0x5e00 | 3 | 7 | 10 | VLP-Fehler: VLP(\|) Kurzschluss nach Masse oder Unterbrechung |
| 0x5ee4 | 0x5d00 | 3 | 7 | 08 | VLP-Fehler: VLP(-) Kurzschluss nach Masse (Kleber) oder Unterbrechung |
| 0x5ee4 | 0x5cc0 | 3 | 7 | 06 | VLP-Fehler: Unterbrechung oder VLP(\|) Kleber |
| 0x5ead | 0x6202 | 4 | 0 | 10 | DF VL Fehler: Leitung |
| 0x5f17 | 0x61c6 | 4 | 0 | 0e | DF VL Fehler: DF11 Sensor Type Wrong / Stop pulse monitor |
| 0x5f18 | 0x61a8 | 4 | 0 | 0d | DF VL Fehler: DF11 Air Gap too large |
| 0x5f19 | 0x618a | 4 | 0 | 0c | DF VL Fehler: Versorgung oder Signalqualitaet |
| 0x5e93 | 0x6164 | 4 | 0 | 0b | DF VL Fehler: DF11 Sensor Signal Width VL / Wrong sensor type |
| 0x5e93 | 0x6145 | 4 | 0 | 0a | DF VL Fehler: Anfahr Ueberwachung  High Speed |
| 0x5e93 | 0x6105 | 4 | 0 | 08 | DF VL Fehler: Dynamische Ueberwachung |
| 0x5e93 | 0x60c5 | 4 | 0 | 06 | DF VL Fehler: Anfahr Ueberwachung  Low Speed |
| 0x5e93 | 0x6085 | 4 | 0 | 04 | DF VL Fehler: Einstreuung VL |
| 0x5e93 | 0x6065 | 4 | 0 | 03 | DF VL Fehler: Lambda Radschlupfueberwachung (ilsmoni) |
| 0x5e93 | 0x6045 | 4 | 0 | 02 | DF VL Fehler: Backup Lambda Radschlupfueberwachung (eslpmon) |
| 0x5eab | 0x6602 | 4 | 1 | 10 | DF HR Fehler: Leitung |
| 0x5f1a | 0x65c6 | 4 | 1 | 0e | DF HR Fehler: DF11 Sensor Type Wrong / Stop pulse monitorv |
| 0x5f1b | 0x65a8 | 4 | 1 | 0d | DF HR Fehler: DF11 Air Gap too large |
| 0x5f1c | 0x658a | 4 | 1 | 0c | DF HR Fehler: Versorgung oder Signalqualitaet |
| 0x5e91 | 0x6564 | 4 | 1 | 0b | DF HR Fehler: DF11 Sensor Signal Width HR / Wrong sensor type |
| 0x5e91 | 0x6545 | 4 | 1 | 0a | DF HR Fehler: Anfahr Ueberwachung  High Speed |
| 0x5e91 | 0x6505 | 4 | 1 | 08 | DF HR Fehler: Dynamische Ueberwachung |
| 0x5e91 | 0x64c5 | 4 | 1 | 06 | DF HR Fehler: Anfahr Ueberwachung  Low Speed |
| 0x5e91 | 0x6485 | 4 | 1 | 04 | DF HR Fehler: Einstreuung HR |
| 0x5e91 | 0x6465 | 4 | 1 | 03 | DF HR Fehler: Lambda Radschlupfueberwachung (ilsmoni) |
| 0x5e91 | 0x6445 | 4 | 1 | 02 | DF HR Fehler: Backup Lambda Radschlupfueberwachung (eslpmon) |
| 0x5eac | 0x6a02 | 4 | 2 | 10 | DF VR Fehler: Leitung |
| 0x5f1d | 0x69c6 | 4 | 2 | 0e | DF VR Fehler: DF11 Sensor Type Wrong / Stop pulse monitor |
| 0x5f1e | 0x69a8 | 4 | 2 | 0d | DF VR Fehler: DF11 Air Gap too large |
| 0x5f1f | 0x698a | 4 | 2 | 0c | DF VR Fehler: Versorgung oder Signalqualitaet |
| 0x5e92 | 0x6964 | 4 | 2 | 0b | DF VR Fehler: DF11 Sensor Signal Width VR / Wrong sensor typev |
| 0x5e92 | 0x6945 | 4 | 2 | 0a | DF VR Fehler: Anfahr Ueberwachung  High Speed |
| 0x5e92 | 0x6905 | 4 | 2 | 08 | DF VR Fehler: Dynamische Ueberwachung |
| 0x5e92 | 0x68c5 | 4 | 2 | 06 | DF VR Fehler: Anfahr Ueberwachung  Low Speed |
| 0x5e92 | 0x6885 | 4 | 2 | 04 | DF VR Fehler:  Einstreuung VR |
| 0x5e92 | 0x6865 | 4 | 2 | 03 | DF VR Fehler: Lambda Radschlupfueberwachung (ilsmoni) |
| 0x5e92 | 0x6845 | 4 | 2 | 02 | DF VR Fehler: Backup Lambda Radschlupfueberwachung (eslpmon) |
| 0x5eaa | 0x6e02 | 4 | 3 | 10 | DF HL Fehler: Leitung |
| 0x5f20 | 0x6dc6 | 4 | 3 | 0e | DF HL Fehler: DF11 Sensor Type Wrong / Stop pulse monitorv |
| 0x5f21 | 0x6da8 | 4 | 3 | 0d | DF HL Fehler: DF11 Air Gap too largev |
| 0x5f22 | 0x6d8a | 4 | 3 | 0c | DF HL Fehler: Versorgung oder Signalqualitaet |
| 0x5e90 | 0x6d64 | 4 | 3 | 0b | DF HL Fehler: DF11 Sensor Signal Width HL / Wrong sensor type |
| 0x5e90 | 0x6d45 | 4 | 3 | 0a | DF HL Fehler: Anfahr Ueberwachung High Speed |
| 0x5e90 | 0x6d05 | 4 | 3 | 08 | DF HL Fehler: Dynamische Ueberwachung |
| 0x5e90 | 0x6cc5 | 4 | 3 | 06 | DF HL Fehler: Anfahr Ueberwachung  Low Speed |
| 0x5e90 | 0x6c85 | 4 | 3 | 04 | DF HL Fehler:  Einstreuung HL |
| 0x5e90 | 0x6c65 | 4 | 3 | 03 | DF HL Fehler: Lambda Radschlupfueberwachung (ilsmoni) |
| 0x5e90 | 0x6c45 | 4 | 3 | 02 | DF HL Fehler: Backup Lambda Radschlupfueberwachung (eslpmon) |
| 0x5ecb | 0x7206 | 4 | 4 | 10 | Lambda-Fehler: V-Vergleich |
| 0x5f0b | 0x714a | 4 | 4 | 0a | Fehler: Wheel rotation plausibility |
| 0x5f11 | 0x711c | 4 | 4 | 08 | Fehler: CS820 T0 - Sensor supply reverse powering |
| 0x5ecc | 0x70c4 | 4 | 4 | 06 | Lambda-Fehler: Dauerregelung |
| 0x5ea4 | 0x7042 | 4 | 4 | 02 | Lambda-Fehler: Radschlupfueberwachung  |
| 0x5ea4 | 0x7022 | 4 | 4 | 01 | Lambda-Fehler: Lambda SLP Monitor (Backup Monitor) |
| 0x5eee | 0x7604 | 4 | 5 | 10 | Fehler Notbremse: Fahrzeug drucklos |
| 0x5ee6 | 0x7502 | 4 | 5 | 08 | Fehler Notbremse: LWS-Initialisierung |
| 0x5f16 | 0x7488 | 4 | 5 | 04 | Fehler Notbremse: DRS-Initialisierung |
| 0x5eef | 0x7466 | 4 | 5 | 03 | Fehler Notbremse: Plausibilitaet der Regelung |
| 0xd347 | 0x7a82 | 4 | 6 | 14 | CAN-Fehler: Bus off wahrend Init |
| 0xd347 | 0x7a62 | 4 | 6 | 13 | CAN-Fehler: Bus off wahrend Init (CAN2) |
| 0xd347 | 0x7a42 | 4 | 6 | 12 | CAN-Fehler: Bus off |
| 0xd347 | 0x7a22 | 4 | 6 | 11 | CAN-Fehler: Bus off (CAN2) |
| 0xd347 | 0x7942 | 4 | 6 | 0a | CAN-Fehler: kein Senden im Interrupt |
| 0xd347 | 0x78c2 | 4 | 6 | 06 | CAN-Fehler: kein Senden moeglich |
| 0xd347 | 0x78a2 | 4 | 6 | 05 | CAN-Fehler: kein Senden moeglich (CAN2) |
| 0xd347 | 0x7882 | 4 | 6 | 04 | CAN-Fehler: CAN message too short |
| 0xd347 | 0x7862 | 4 | 6 | 03 | CAN-Fehler: CAN message too short (CAN2) |
| 0x5efa | 0x7ce6 | 4 | 7 | 07 | UZ-Fehler: Ueberspannung (laufender Betrieb) |
| 0x5ee5 | 0x7d02 | 4 | 7 | 08 | UZ-Fehler: Low-Voltage (detected by UZ Measurement) |
| 0x5ee5 | 0x7cc2 | 4 | 7 | 06 | UZ-Fehler: Low-Voltage (detected by CS800) |
| 0x5ec7 | 0x8202 | 5 | 0 | 10 | Motronic-Fehler: Digitale Motorelektronik rechts 1v |
| 0x5ed1 | 0x8144 | 5 | 0 | 0a | CAN-Fehler: Digitale Motorelektronik rechts 2 |
| 0x5f0d | 0x81aa | 5 | 0 | 0d | CAN-Fehler: Digitale Motorelektronik rechts 3 |
| 0x5f02 | 0x8108 | 5 | 0 | 08 | Motronic-Fehler: Status DME: Interner DME-Fehler |
| 0x5efb | 0x80a6 | 5 | 0 | 05 | Motronic-Fehler: Quittierungsbit Q_ASC kommt nicht |
| 0x5f2a | 0x806c | 5 | 0 | 03 | Motronic-Fehler: Signal ungueltig |
| 0x5ec6 | 0x8600 | 5 | 1 | 10 | Elektronische Getriebesteuerung sendet nicht |
| 0x5f23 | 0x9a00 | 5 | 6 | 10 | Fahrleistungsreduzierung |
| 0x5f06 | 0x9202 | 5 | 4 | 10 | ACC-Fault: ACC-Botschaft fehlt |
| 0x5f06 | 0x921c | 5 | 4 | 0e | ACC-Fault: ACC-Anzeige-Botschaft fehlt |
| 0x5f07 | 0x9184 | 5 | 4 | 0c | ACC-Fault: Konsistenzfehler ACC-Botschaft |
| 0x5f08 | 0x9106 | 5 | 4 | 08 | ACC-Fault: Aktivitaetsfehler: Keine Aenderung des Alive-Zaehlers |
| 0x5ef8 | 0x9600 | 5 | 5 | 10 | SN-Fehler : Niveau Bremsfluessigkeit |
| 0x5ea3 | 0x9c80 | 5 | 7 | 14 | Option-Fehler : Nicht codiert |
| 0x5ea3 | 0x9e00 | 5 | 7 | 10 | Option-Fehler : Falsche Variante codiert: Nummer undefiniert |
| 0x5ea3 | 0x9d80 | 5 | 7 | 0c | Option-Fehler : ueber CAN keine Fahrzeugdaten erhalten |
| 0x5ea3 | 0x9d40 | 5 | 7 | 0a | Option-Fehler : ungueltige Fahrgestellnummer empfangen |
| 0x5ea3 | 0x9d00 | 5 | 7 | 08 | Option-Fehler : Falsche Variante codiert: CAN-Kennung falsch |
| 0x5ea3 | 0x9cc0 | 5 | 7 | 06 | Option-Fehler : ueber CAN keine gueltige Variante erkannt |
| 0x5f12 | 0xa21c | 6 | 0 | 10 | CAN-Msg-Fehler: EMF-Steuergeraet sendet nicht |
| 0x5f12 | 0xa1c0 | 6 | 0 | 0e | CAN-Msg-Fehler: Konisitenzfehler EMF-Botschaft |
| 0x5f12 | 0xa180 | 6 | 0 | 0c | CAN-Msg-Fehler: EMF-Botschaft: Keine Aenderung des Alive-Zaehlers |
| 0x5f25 | 0xaa00 | 6 | 2 | 10 | EMF-Fehler: Halbleiterrelais ueberhitzt |
| 0x5f24 | 0xa600 | 6 | 1 | 10 | EMF-Fehler: Ueberhitzungsgefahr fuer Halbleiterrelais |
| 0x5ef9 | 0xaf40 | 6 | 3 | 1a | Bandende-Test : AY-Ueberwachungstest fehlgeschlagen |
| 0x5ef9 | 0xaea0 | 6 | 3 | 15 | Bandende-Test : DRS-Bite fehlgeschlagen |
| 0x5ef9 | 0xae80 | 6 | 3 | 14 | Bandende-Test : DRS-Offsettest fehlgeschlagen |
| 0x5ef9 | 0xad60 | 6 | 3 | 0b | Bandende-Test : Annahme: Lw-Test fehlgeschlagen |
| 0x5ef9 | 0xad20 | 6 | 3 | 09 | Bandende-Test : Annahme DRS-Empfindlichkeitstest fehlgeschlagen |
| 0x5ed0 | 0xb540 | 6 | 5 | 0a | DSC passiv nach UZ wegen Einstreuung |
| 0x5f13 | 0xba02 | 6 | 6 | 10 | CAN-Msg-Fehler: ARS-Steuergeraet sendet nicht |
| 0x5f14 | 0xb984 | 6 | 6 | 0c | CAN-Msg-Fehler: CAS-Steuergeraet sendet nicht |
| 0x5f15 | 0xb946 | 6 | 6 | 0a | CAN-Msg-Fehler: KOMBI-Steuergeraet sendet nicht |
| 0x5F26 | 0xbe44 | 6 | 7 | 12 | Bremsbelagverschleiss Servicemeldung VA unplausibel |
| 0x5F27 | 0xbd86 | 6 | 7 | 0C | Bremsbelagverschleiss Dicke VA &lt; 3mm |
| 0x5F28 | 0xbe00 | 6 | 7 | 10 | Bremsbelagverschleiss Servicemeldung HA unplausibel |
| 0x5F29 | 0xbd42 | 6 | 7 | 0a | Bremsbelagverschleiss Dicke HA &lt; 3mm |
| 0xFFFF | 0xFFFF | 0 | 0 | 00 | unbekannter Fehlerort |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | DIGITAL | - | - |

<a id="table-digital"></a>
### DIGITAL

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 9 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Fahrzeuggeschwindigkeit | km/h | High | unsigned int | - | 1 | 16.0 | 0 |
| 0x02 | ACB | 0/1 | - | 0x01 | - | 1 | 1 | 0 |
| 0x03 | HBA | 0/1 | - | 0x02 | - | 1 | 1 | 0 |
| 0x04 | ECD | 0/1 | - | 0x04 | - | 1 | 1 | 0 |
| 0x05 | EMF | 0/1 | - | 0x08 | - | 1 | 1 | 0 |
| 0x06 | DSC | 0/1 | - | 0x10 | - | 1 | 1 | 0 |
| 0x07 | ABS | 0/1 | - | 0x20 | - | 1 | 1 | 0 |
| 0x08 | BLS | 0/1 | - | 0x40 | - | 1 | 1 | 0 |
| 0x09 | ASC | 0/1 | - | 0x80 | - | 1 | 1 | 0 |

<a id="table-stg-tabelle"></a>
### STG_TABELLE

Dimensions: 20 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| MRA | 0x22 |
| VLP1 | 0x24 |
| EVVL | 0x30 |
| AVVL | 0x32 |
| EVVR | 0x34 |
| AVVR | 0x36 |
| EVHR | 0x38 |
| AVHR | 0x3A |
| EVHL | 0x3C |
| AVHL | 0x3E |
| USV1 | 0x4E |
| USV2 | 0x50 |
| VLV1 | 0x52 |
| VLV2 | 0x54 |
| VLP2 | 0x84 |
| ACC | 0x26 |
| TOG | 0x62 |
| SILGK | 0x64 |
| VLIM | 0x68 |
| NF-ASC | 0x78 |

<a id="table-e-a-status"></a>
### E_A_STATUS

Dimensions: 2 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| EIN | 0xFF |
| AUS | 0x00 |

<a id="table-rad-nr-tabelle"></a>
### RAD_NR_TABELLE

Dimensions: 4 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| V_LINKS | 0xA0 |
| V_RECHTS | 0xA2 |
| H_RECHTS | 0xA4 |
| H_LINKS | 0xA6 |

<a id="table-boskennung"></a>
### BOSKENNUNG

Dimensions: 11 rows × 3 columns

| NR | BOS_K | BOS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Ölqualität |
| 0x02 | Br_v | Bremsbelagverschleiss vorne |
| 0x03 | Brfl | Bremsflüssigkeit |
| 0x04 | Filt | Mikrofilter |
| 0x05 | Batt | Batteriezustand |
| 0x06 | Br_h | Bremsbelagverschleiss hinten |
| 0x10 | ZKrz | Zündkerzen |
| 0x11 | Sic | Sichtprüfung |
| 0x12 | Kfl | Kühlflüssigkeit |
| 0x20 | TUV | TÜV |
| 0x21 | AU | AU |
