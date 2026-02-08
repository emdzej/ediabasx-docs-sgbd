# mrk24.prg

- Jobs: [18](#jobs)
- Tables: [18](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Funktionale Jobs fuer Motorrad |
| ORIGIN | BMW UX-EE-1 Krimmer |
| REVISION | 3.803 |
| AUTHOR | ESG UX-EE-1 Sergl, BMW UX-EE-1 Krimmer, ESG UX-EE-1 Berisha, in |
| COMMENT | N/A |
| PACKAGE | 1.71 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [DIAGNOSEPROTOKOLL_LESEN](#job-diagnoseprotokoll-lesen) - Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück
- [DIAGNOSEPROTOKOLL_SETZEN](#job-diagnoseprotokoll-setzen) - Wählt ein Diagnoseprotokoll aus
- [IDENT_FUNKTIONAL](#job-ident-funktional) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [FS_LESEN_FUNKTIONAL](#job-fs-lesen-funktional) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LOESCHEN_FUNKTIONAL](#job-fs-loeschen-funktional) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [C_AEI_LESEN_FUNKTIONAL](#job-c-aei-lesen-funktional) - Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [FLASH_PROGRAMMIER_STATUS_LESEN_FUNKTIONAL](#job-flash-programmier-status-lesen-funktional) - Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default
- [SERIENNUMMER_LESEN_FUNKTIONAL](#job-seriennummer-lesen-funktional) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber Modus  : Default
- [PHYSIKALISCHE_HW_NR_LESEN_FUNKTIONAL](#job-physikalische-hw-nr-lesen-funktional) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) Modus  : Default
- [ENERGIESPARMODE_FUNKTIONAL](#job-energiesparmode-funktional) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [AIF_LESEN_FUNKTIONAL](#job-aif-lesen-funktional) - Auslesen des Anwender Informations Feldes KWP2000: $1A ReadECUIdentification $86 CurrentUIFDataTable Modus  : Default
- [I_STUFE_LESEN](#job-i-stufe-lesen) - Auslesen des Pruefstempels aus Kombi Wenn Kombi tot bzw. Daten nicht plausibel auch aus ZFE Wenn ZFE tot bzw. Daten nicht plausibel auch aus BMSKP KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [I_STUFE_SCHREIBEN](#job-i-stufe-schreiben) - Beschreiben des Pruefstempels der ZFE und des Kombis und evtl BMSKP Es muessen immer alle drei Argumente uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen zuerst aus Kombi, bei Timeout oder neuem Kombi aus ZFE, dann bei Timeout ZFE oder neue ZFE aus BMSKP bzw BMSE KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F7F Fahrzeugauftrag Modus  : Default
- [STATUS_FAHRGESTELLNUMMER](#job-status-fahrgestellnummer) - 17 ASCII Byte EWS-Fahrgestell-Nummer aus BMSK BMS-K(P): KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $30 BMS-M:    KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier $64, $70 Falls keine Antwort von BMSKP bzw. BMS-M (weil BMS im Bootblock), wird auf die FGNR aus dem FA-Bereich ($22, $10, $10) zurueckgegriffen Modus   : Default
- [NETTODATEN_LESEN_FUNKTIONAL](#job-nettodaten-lesen-funktional) - Nettodaten der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3xxx Codierdaten-Adressen Modus  : Default
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter

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

<a id="job-ident-funktional"></a>
### IDENT_FUNKTIONAL

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT oder spezifische SG-Adresse Defaultwert: ALL |
| GRUPPENDATEI | string | optionales Argument nicht in Verbindung mit FUNKTIONALE_ADRESSE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ECU_GROBNAME | string | Grobname des Steuergeraetes table Grobname GROBNAME |
| ID_SG_ADR | long | Steuergeraeteadresse |
| ECU_NAME | string | Steuergeraete Name table ZuordnungsTabelleMotorrad ADR_VAR_DIAG STEUERGERAET |
| ECU_SGBD | string | Steuergeraete SGBD Name table ZuordnungsTabelleMotorrad ADR_VAR_DIAG SGBD |
| ECU_GRUPPE | string | Steuergeraete Gruppendatei Name table ZuordnungsTabelleMotorrad ADR_VAR_DIAG GRUPPE |
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
| SERIENNUMMER | string | Seriennummer des Steuergeraets Leer, wenn keine Seriennummer im Telegramm vorhanden |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-funktional"></a>
### FS_LESEN_FUNKTIONAL

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |
| FEHLER_GRUPPE | string | gewuenschte funktionale Fehlergruppe table FunktionalerFehlerGruppe F_DTC F_DTC_TEXT Defaultwert: AG ( alle Fehlergruppen ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ECU_GROBNAME | string | Grobname des Steuergeraetes table Grobname GROBNAME |
| ID_SG_ADR | long | Steuergeraeteadresse |
| F_ANZ | int | Anzahl der Fehlereingetraege Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_ORTi_NR        Fehlercode (long)   F_ARTi_NR        Fehlerart |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen-funktional"></a>
### FS_LOESCHEN_FUNKTIONAL

Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |
| FEHLER_GRUPPE | string | gewuenschte funktionale Fehlergruppe table FunktionalerFehlerGruppe F_DTC F_DTC_TEXT Defaultwert: AG ( alle Fehlergruppen ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ECU_GROBNAME | string | Grobname des Steuergeraetes table Grobname GROBNAME |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-lesen-funktional"></a>
### C_AEI_LESEN_FUNKTIONAL

Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ECU_GROBNAME | string | Grobname des Steuergeraetes table Grobname GROBNAME |
| ID_SG_ADR | long | Steuergeraeteadresse |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-programmier-status-lesen-funktional"></a>
### FLASH_PROGRAMMIER_STATUS_LESEN_FUNKTIONAL

Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ECU_GROBNAME | string | Grobname des Steuergeraetes table Grobname GROBNAME |
| ID_SG_ADR | long | Steuergeraeteadresse |
| FLASH_PROGRAMMIER_STATUS_TEXT | string | table ProgrammierStatus STATUS_TEXT |
| FLASH_PROGRAMMIER_STATUS | int | ProgrammierStatus 0 - 255 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-seriennummer-lesen-funktional"></a>
### SERIENNUMMER_LESEN_FUNKTIONAL

Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ECU_GROBNAME | string | Grobname des Steuergeraetes table Grobname GROBNAME |
| ID_SG_ADR | long | Steuergeraeteadresse |
| SERIENNUMMER | string | Seriennummer des Steuergeraets |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-physikalische-hw-nr-lesen-funktional"></a>
### PHYSIKALISCHE_HW_NR_LESEN_FUNKTIONAL

Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ECU_GROBNAME | string | Grobname des Steuergeraetes table Grobname GROBNAME |
| ID_SG_ADR | long | Steuergeraeteadresse |
| PHYSIKALISCHE_HW_NR | string | Physikalische Hardware-Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-energiesparmode-funktional"></a>
### ENERGIESPARMODE_FUNKTIONAL

Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |
| PRODUKTIONSMODE | string | "ein" -&gt; Produktions Mode ein "aus" -&gt; Produktions Mode aus table DigitalArgument TEXT Default: "aus" |
| TRANSPORTMODE | string | "ein" -&gt; Transport Mode ein "aus" -&gt; Transport Mode aus table DigitalArgument TEXT Default: "aus" |
| WERKSTATTMODE | string | "ein" -&gt; Werkstatt Mode ein "aus" -&gt; Werkstatt Mode aus table DigitalArgument TEXT Default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ECU_GROBNAME | string | Grobname des Steuergeraetes table Grobname GROBNAME |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aif-lesen-funktional"></a>
### AIF_LESEN_FUNKTIONAL

Auslesen des Anwender Informations Feldes KWP2000: $1A ReadECUIdentification $86 CurrentUIFDataTable Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ECU_GROBNAME | string | Grobname des Steuergeraetes table Grobname GROBNAME |
| ID_SG_ADR | long | Steuergeraeteadresse |
| AIF_LAENGE | long | Laenge des Aif ( Offset ) |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-i-stufe-lesen"></a>
### I_STUFE_LESEN

Auslesen des Pruefstempels aus Kombi Wenn Kombi tot bzw. Daten nicht plausibel auch aus ZFE Wenn ZFE tot bzw. Daten nicht plausibel auch aus BMSKP KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| I_STUFE_WERK | string | table I_STUFE_K24 I_STUFE_TEXT Entspricht Byte 1 des Pruefstempels |
| I_STUFE_HO | string | table I_STUFE_K24 I_STUFE_TEXT Entspricht Byte 2 des Pruefstempels |
| I_STUFE_HO_BACKUP | string | table I_STUFE_K24 I_STUFE_TEXT Entspricht Byte 3 des Pruefstempels |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-i-stufe-schreiben"></a>
### I_STUFE_SCHREIBEN

Beschreiben des Pruefstempels der ZFE und des Kombis und evtl BMSKP Es muessen immer alle drei Argumente uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_STUFE_WERK | string | kein Argument - es wird 0x00 im Steuergeraet abgelegt table I_STUFE_K24 I_STUFE_TEXT es wird auch 0 akzeptiert, es wird 0x00 geschrieben Entspricht Byte 1 des Pruefstempels |
| I_STUFE_HO | string | kein Argument - es wird 0x00 im Steuergeraet abgelegt table I_STUFE_K24 I_STUFE_TEXT es wird auch 0 akzeptiert, es wird 0x00 geschrieben Entspricht Byte 2 des Pruefstempels |
| I_STUFE_HO_BACKUP | string | kein Argument - es wird 0x00 im Steuergeraet abgelegt table I_STUFE_K24 I_STUFE_TEXT es wird auch 0 akzeptiert, es wird 0x00 geschrieben Entspricht Byte 3 des Pruefstempels |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-lesen"></a>
### C_FA_LESEN

Fahrzeugauftrag lesen zuerst aus Kombi, bei Timeout oder neuem Kombi aus ZFE, dann bei Timeout ZFE oder neue ZFE aus BMSKP bzw BMSE KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F7F Fahrzeugauftrag Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | Daten des Fahrzeugauftrages |
| SPEICHER_STATUS | string | BELEGT bzw. UNBELEGT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrgestellnummer"></a>
### STATUS_FAHRGESTELLNUMMER

17 ASCII Byte EWS-Fahrgestell-Nummer aus BMSK BMS-K(P): KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $30 BMS-M:    KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier $64, $70 Falls keine Antwort von BMSKP bzw. BMS-M (weil BMS im Bootblock), wird auf die FGNR aus dem FA-Bereich ($22, $10, $10) zurueckgegriffen Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FGNUMMER | string | ausgelesene Fahrgestellnummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-nettodaten-lesen-funktional"></a>
### NETTODATEN_LESEN_FUNKTIONAL

Nettodaten der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3xxx Codierdaten-Adressen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ECU_GROBNAME | string | Grobname des Steuergeraetes table Grobname GROBNAME |
| ID_SG_ADR | long | Steuergeraeteadresse |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| NETTODATEN_BLOCK_3000 | binary | Nettodaten der Codierung Block 3000 |
| NETTODATEN_BLOCK_3001 | binary | Nettodaten der Codierung Block 3001 |
| NETTODATEN_BLOCK_3002 | binary | Nettodaten der Codierung Block 3002 |
| NETTODATEN_BLOCK_3003 | binary | Nettodaten der Codierung Block 3003 |
| NETTODATEN_BLOCK_3004 | binary | Nettodaten der Codierung Block 3004 |
| NETTODATEN_BLOCK_3005 | binary | Nettodaten der Codierung Block 3005 |
| NETTODATEN_BLOCK_3006 | binary | Nettodaten der Codierung Block 3006 |
| NETTODATEN_BLOCK_3007 | binary | Nettodaten der Codierung Block 3007 |
| NETTODATEN_BLOCK_3008 | binary | Nettodaten der Codierung Block 3008 |
| NETTODATEN_BLOCK_3009 | binary | Nettodaten der Codierung Block 3009 |
| NETTODATEN_BLOCK_300A | binary | Nettodaten der Codierung Block 300A |
| NETTODATEN_BLOCK_300B | binary | Nettodaten der Codierung Block 300B |
| NETTODATEN_BLOCK_300C | binary | Nettodaten der Codierung Block 300C |
| NETTODATEN_BLOCK_300D | binary | Nettodaten der Codierung Block 300D |
| NETTODATEN_BLOCK_300E | binary | Nettodaten der Codierung Block 300E |
| NETTODATEN_BLOCK_300F | binary | Nettodaten der Codierung Block 300F |
| NETTODATEN_BLOCK_3010 | binary | Nettodaten der Codierung Block 3010 |
| NETTODATEN_BLOCK_3011 | binary | Nettodaten der Codierung Block 3011 |
| NETTODATEN_BLOCK_3012 | binary | Nettodaten der Codierung Block 3012 |
| NETTODATEN_BLOCK_3320 | binary | Nettodaten der Codierung Block 3320 |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

## Tables

### Index

- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (1 × 2)
- [GROBNAME](#table-grobname) (10 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (5 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (140 × 2)
- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [FUNKTIONALEADRESSE](#table-funktionaleadresse) (11 × 3)
- [FUNKTIONALERFEHLERGRUPPE](#table-funktionalerfehlergruppe) (5 × 3)
- [I_STUFE_K24](#table-i-stufe-k24) (121 × 2)

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-grobname"></a>
### GROBNAME

Dimensions: 10 rows × 2 columns

| ADR | GROBNAME |
| --- | --- |
| 0x12 | BMSK |
| 0x29 | ABS |
| 0x39 | SAF |
| 0x41 | DWA |
| 0x47 | RADIO |
| 0x60 | KOMBI |
| 0x63 | AUDIO |
| 0x72 | ZFE |
| 0x73 | RBT |
| 0xXY | ???? |

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
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 5 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| - | BMW-FAST |
| - | KWP2000* |
| 1 | KWP2000 |
| - | DS2 |
| 2 | D-CAN |

<a id="table-authentisierung"></a>
### AUTHENTISIERUNG

Dimensions: 4 rows × 2 columns

| AUTH_NR | AUTH_TEXT |
| --- | --- |
| 0x01 | Simple |
| 0x02 | Symetrisch |
| 0x03 | Asymetrisch |
| 0xFF | Keine |

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

Dimensions: 140 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |

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

<a id="table-funktionaleadresse"></a>
### FUNKTIONALEADRESSE

Dimensions: 11 rows × 3 columns

| NR | F_ADR | F_ADR_TEXT |
| --- | --- | --- |
| 0xE6 | VD-FLEXRAY | Vertikaldynamik Flexray Steuergeräte |
| 0xE7 | SWT | Sweeping technologies Steuergeräte |
| 0xE8 | LIN | LIN-Bus Master Steuergeräte |
| 0xE9 | K-CAN | Karosserie-CAN Steuergeräte |
| 0xEA | PT-CAN | Powertrain-CAN Steuergeräte |
| 0xEB | SI | Sicherheits-BUS Steuergeräte |
| 0xEC | MOST | MOST-BUS Steuergeräte |
| 0xED | BOS | Bedarfsorientierter Service |
| 0xED | CBS | Bedarfsorientierter Service |
| 0xEE | PERSONAL | Personalisierung |
| 0xEF | ALL | alle Steuergeräte |

<a id="table-funktionalerfehlergruppe"></a>
### FUNKTIONALERFEHLERGRUPPE

Dimensions: 5 rows × 3 columns

| NR | F_DTC | F_DTC_TEXT |
| --- | --- | --- |
| 0xFFFB | PG | Antriebsstrang Gruppe |
| 0xFFFC | CG | Fahrwerk Gruppe |
| 0xFFFD | BG | Karosserie Gruppe |
| 0xFFFE | NG | Netzwerk Kommunikation Gruppe |
| 0xFFFF | AG | alle Gruppen |

<a id="table-i-stufe-k24"></a>
### I_STUFE_K24

Dimensions: 121 rows × 2 columns

| NR | I_STUFE_TEXT |
| --- | --- |
| 0x00 |  |
| 0x01 | K024-02-10-100 |
| 0x02 | K024-03-03-200 |
| 0x03 | K024-03-05-310 |
| 0x04 | K024-03-05-311 |
| 0x05 | K024-03-08-420 |
| 0x06 | K024-03-10-500 |
| 0x07 | K024-03-10-510 |
| 0x08 | K024-04-03-400 |
| 0x09 | K024-04-03-500 |
| 0x0A | K024-04-05-510 |
| 0x0B | K024-04-07-500 |
| 0x0C | K024-04-11-500 |
| 0x0F | K024-04-11-510 |
| 0x10 | K024-04-11-520 |
| 0x11 | K024-04-11-530 |
| 0x0E | K024-05-02-500 |
| 0x12 | K024-05-02-510 |
| 0x0D | K024-05-05-400 |
| 0x17 | K024-05-05-500 |
| 0x18 | K024-05-05-510 |
| 0x19 | K024-05-05-520 |
| 0x1A | K024-05-08-500 |
| 0x1D | K024-05-08-510 |
| 0x13 | K024-05-11-300 |
| 0x1C | K024-05-11-500 |
| 0x20 | K024-05-11-510 |
| 0x14 | K024-05-12-300 |
| 0x15 | K024-05-12-310 |
| 0x16 | K024-05-12-320 |
| 0x1B | K024-05-12-400 |
| 0x1E | K024-06-01-300 |
| 0x1F | K024-06-01-500 |
| 0x22 | K024-06-01-510 |
| 0x21 | K024-06-07-500 |
| 0x23 | K024-06-08-400 |
| 0x24 | K024-06-08-500 |
| 0x2F | K024-06-08-510 |
| 0x26 | K024-06-10-500 |
| 0x30 | K024-07-01-500 |
| 0x27 | K024-07-02-500 |
| 0x2E | K024-07-05-500 |
| 0x31 | K024-07-05-510 |
| 0x32 | K024-07-05-520 |
| 0x35 | K024-07-05-530 |
| 0x2C | K024-07-08-500 |
| 0x25 | K024-07-10-200 |
| 0x28 | K024-07-10-210 |
| 0x29 | K024-07-10-220 |
| 0x2A | K024-07-10-300 |
| 0x2B | K024-07-10-400 |
| 0x2D | K024-07-10-500 |
| 0x36 | K024-07-10-505 |
| 0x37 | K024-07-10-510 |
| 0x34 | K024-08-01-500 |
| 0x3A | K024-08-05-500 |
| 0x39 | K024-08-08-400 |
| 0x3B | K024-08-08-500 |
| 0x3E | K024-08-08-550 |
| 0x33 | K024-08-12-300 |
| 0x40 | K024-09-02-500 |
| 0x43 | K024-09-08-500 |
| 0x46 | K024-09-08-550 |
| 0x47 | K024-09-08-560 |
| 0x49 | K024-09-08-570 |
| 0x3C | K024-09-09-200 |
| 0x3F | K024-09-09-300 |
| 0x41 | K024-09-09-350 |
| 0x42 | K024-09-09-400 |
| 0x3D | K024-09-10-300 |
| 0x48 | K024-10-02-500 |
| 0x4A | K024-10-02-550 |
| 0x4B | K024-10-08-500 |
| 0x44 | K024-10-10-200 |
| 0x45 | K024-10-10-250 |
| 0x4C | K024-10-10-500 |
| 0x4F | K024-11-03-500 |
| 0x57 | K024-11-03-510 |
| 0x51 | K024-11-08-500 |
| 0x58 | K024-11-08-510 |
| 0x4D | K024-11-09-300 |
| 0x50 | K024-11-09-400 |
| 0x4E | K024-11-12-300 |
| 0x54 | K024-11-12-500 |
| 0x55 | K024-12-02-500 |
| 0x5B | K024-12-02-510 |
| 0x52 | K024-12-06-300 |
| 0x56 | K024-12-08-490 |
| 0x5A | K024-12-08-500 |
| 0x5C | K024-12-08-510 |
| 0x53 | K024-12-12-300 |
| 0x59 | K024-12-12-350 |
| 0x5D | K024-13-02-400 |
| 0x5E | K024-13-02-500 |
| 0x5F | K024-13-02-510 |
| 0x60 | K024-13-08-400 |
| 0x61 | K024-13-08-500 |
| 0x62 | K024-13-08-510 |
| 0x63 | K024-14-02-400 |
| 0x83 | K024-14-02-500 |
| 0x84 | K024-14-02-501 |
| 0x85 | K024-14-08-500 |
| 0x86 | K024-15-03-500 |
| 0x87 | K024-15-07-400 |
| 0x88 | K024-15-07-500 |
| 0x89 | K024-15-11-490 |
| 0x8A | K024-15-11-500 |
| 0x90 | K024-15-11-501 |
| 0x8B | K024-16-03-500 |
| 0x91 | K024-16-03-501 |
| 0x8C | K024-16-06-400 |
| 0x8D | K024-16-06-490 |
| 0x8E | K024-16-06-500 |
| 0x92 | K024-16-06-510 |
| 0x93 | K024-16-11-490 |
| 0x8F | K024-16-11-500 |
| 0x94 | K024-17-03-500 |
| 0x95 | K024-17-07-500 |
| 0x38 |  |
| 0xFF |  |
| 0xFE | unbekannte I-Stufe |
