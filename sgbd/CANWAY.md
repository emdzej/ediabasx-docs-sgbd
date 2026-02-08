# CANWAY.prg

- Jobs: [19](#jobs)
- Tables: [51](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | CANWAY |
| ORIGIN | remes_GmbH MDK Brandlmeier |
| REVISION | 1.004 |
| AUTHOR | remes_GmbH MC Brandlmeier |
| COMMENT | N/A |
| PACKAGE | 1.66 |
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
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [_STATUS](#job-status) - Auslesen der Stati nur fuer Entwicklung !!! KWP: $22   ReadDataByIdentifier KWP: $Fxxx CanWay-spezifischer Bereich (für alle Varianten)
- [_STEUERN](#job-steuern) - Vorgeben von Digital-Ausgaengen nur fuer Entwicklung !!! KWP: $2E   WriteDataByCommonIdentifier service KWP: $Fxxx CanWay-spezifischer Bereich (für alle Varianten)
- [STAT_CW_VERSION](#job-stat-cw-version) - Auslesen der CanWay-Versionsinfo nur fuer Entwicklung !!! KWP  : $22   ReadDataByIdentifier KWP  : $Fxxx SG-spezifischer Bereich
- [FLASH_CW](#job-flash-cw) - Flash Daten schreiben XXL-Format Standard Flashjob KWP2000: $36 TransferData Modus  : Default
- [STATUS_LESEN](#job-status-lesen) - Lesen eines oder mehrerer Stati $22 ReadDataByCommonIdentifier
- [STEUERN](#job-steuern) - Vorgeben eines Status $2E WriteDataByCommonIdentifier

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

<a id="job-status"></a>
### _STATUS

Auslesen der Stati nur fuer Entwicklung !!! KWP: $22   ReadDataByIdentifier KWP: $Fxxx CanWay-spezifischer Bereich (für alle Varianten)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARA | int | 2.Parameter |
| OUTBUF | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| INBUF | binary |  |

<a id="job-steuern"></a>
### _STEUERN

Vorgeben von Digital-Ausgaengen nur fuer Entwicklung !!! KWP: $2E   WriteDataByCommonIdentifier service KWP: $Fxxx CanWay-spezifischer Bereich (für alle Varianten)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARA | int | 2.Parameter |
| OUTBUF | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-stat-cw-version"></a>
### STAT_CW_VERSION

Auslesen der CanWay-Versionsinfo nur fuer Entwicklung !!! KWP  : $22   ReadDataByIdentifier KWP  : $Fxxx SG-spezifischer Bereich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VERSIONSSTRING_TEXT | string | die im SG abgelegte Versonsinformation |
| STAT_HW_VERSION | string | die im SG abgelegte HW_Versonsinformation |
| STAT_SW_VERSION | string | die im SG abgelegte SW_Versonsinformation |
| INBUF | binary | Rohdaten |

<a id="job-flash-cw"></a>
### FLASH_CW

Flash Daten schreiben XXL-Format Standard Flashjob KWP2000: $36 TransferData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0,1            : Anzahl Bytedaten (low/high) Byte 2,....         : Flashdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| INBUF | binary | Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Lesen eines oder mehrerer Stati $22 ReadDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Es muss mindestens ein Argument übergeben werden Es wird das zugehörige result erzeugt table SG_Funktionen ARG ID RESULTNAME RES_TABELLE ARG_TABELLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Antwort von SG |

<a id="job-steuern"></a>
### STEUERN

Vorgeben eines Status $2E WriteDataByCommonIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Siehe table SG_Funktionen ARG ID LABEL ARG_TABELLE |
| WERT | string | Es muss mindestens ein Argument übergeben werden Argumente siehe table SG_Funktionen ARG ID ARG_TABELLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (137 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (18 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (6 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (5 × 2)
- [SG_FUNKTIONEN](#table-sg-funktionen) (15 × 16)
- [TAB_EINAUS](#table-tab-einaus) (2 × 2)
- [RES_0XF101](#table-res-0xf101) (7 × 10)
- [RES_0XF106](#table-res-0xf106) (8 × 10)
- [RES_0XF112](#table-res-0xf112) (9 × 10)
- [RES_0XF113](#table-res-0xf113) (7 × 10)
- [RES_0XF114](#table-res-0xf114) (3 × 10)
- [TAB_BED_TEMPOMAT](#table-tab-bed-tempomat) (9 × 2)
- [RES_0XF115](#table-res-0xf115) (6 × 10)
- [TAB_KLEMMENSTATUS](#table-tab-klemmenstatus) (13 × 2)
- [RES_0XF116](#table-res-0xf116) (3 × 10)
- [RES_0XF120](#table-res-0xf120) (6 × 10)
- [RES_0XF121](#table-res-0xf121) (8 × 10)
- [RES_0XF122](#table-res-0xf122) (2 × 10)
- [TAB_WARNLED](#table-tab-warnled) (12 × 10)
- [TAB_LED_ZUSTAND](#table-tab-led-zustand) (4 × 2)
- [RES_0XF124](#table-res-0xf124) (13 × 10)
- [TAB_TUERSTATUS](#table-tab-tuerstatus) (3 × 2)
- [TAB_ZV_STATUS](#table-tab-zv-status) (3 × 2)
- [RES_0XF125](#table-res-0xf125) (4 × 10)
- [RES_0XF126](#table-res-0xf126) (8 × 10)
- [ARG_0XF112](#table-arg-0xf112) (3 × 12)
- [TAB_FH_AUSWAHL](#table-tab-fh-auswahl) (2 × 2)
- [TAB_FH_RICHT](#table-tab-fh-richt) (2 × 2)
- [ARG_0XF113](#table-arg-0xf113) (2 × 12)
- [ARG_0XF116](#table-arg-0xf116) (3 × 12)
- [ARG_0XF118](#table-arg-0xf118) (3 × 12)
- [TAB_INST_AUSWAHL](#table-tab-inst-auswahl) (4 × 2)
- [ARG_0XF121](#table-arg-0xf121) (2 × 12)
- [TAB_OUT_AUSWAHL](#table-tab-out-auswahl) (8 × 2)
- [ARG_0XF122](#table-arg-0xf122) (3 × 12)
- [TAB_LED_AUSWAHL](#table-tab-led-auswahl) (11 × 2)
- [ARG_0XF124](#table-arg-0xf124) (1 × 12)
- [TAB_ZV_STEUERN](#table-tab-zv-steuern) (2 × 2)
- [ARG_0XF125](#table-arg-0xf125) (2 × 12)
- [ARG_0XF126](#table-arg-0xf126) (3 × 12)
- [ARG_0XF132](#table-arg-0xf132) (2 × 12)

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

Dimensions: 137 rows × 2 columns

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
| 0xA5 | Funkwerk Dabendorf GmbH |
| 0xA6 | Lame |
| 0xA7 | Magna/Closures |
| 0xA8 | Wanyu |
| 0xA9 | Thyssen Krupp Presta |
| 0xAA | ArvinMeritor |
| 0xAB | Kongsberg Automotive GmbH |
| 0xAC | SMR Automotive Mirrors |
| 0xAD | So.Ge.Mi. |
| 0xAE | MTA |
| 0xAF | Alfmeier |
| 0xB0 | ELTEK VALERE DEUTSCHLAND GMBH |
| 0xB1 | Omron Automotive Electronics Europe Group |
| 0xB2 | ASK |
| 0xB3 | CML Innovative Technologies GmbH & Co. KG |
| 0xB4 | APAG Elektronik AG |
| 0xB5 | Nexteer Automotive World Headquarters |
| 0xB6 | Hans Widmaier |
| 0xB7 | Robert Bosch Battery Systems GmbH |
| 0xB8 | KYOCERA Display Corporation |
| 0xB9 | MAGNA Powertrain AG & Co KG |
| 0xBA | BorgWarner |
| 0xBB | BMW - Fahrzeugsimulator |
| 0xBC | Benteler Duncan Plant |
| 0xBD | U-Shin |
| 0xBE | Schaeffler Technologies |
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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 18 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA208 | CAN_Bus: PT-CAN off |
| 0xA209 | CAN_Bus: K-CAN off |
| 0xA20A | CAN_Bus: DSPL-CAN off |
| 0xA20B | Versorgung: Spannung zu gering |
| 0xA20C | Display: Ausfall Kommunikation |
| 0xA20D | Außentemperatursensor: Fehler |
| 0xA20E | Raddrehzahlsensor links: Fehler |
| 0xA20F | Raddrehzahlsensor rechts: Fehler |
| 0xA210 | Tankgeber: |
| 0xA211 | Blinker links: defekt |
| 0xA212 | Blinker rechts: defekt |
| 0xA213 | Blinker: Taster Warnblinker Unterbrechung |
| 0xA214 | Blinker: Taster links Unterbrechung |
| 0xA215 | Blinker: Taster rechts Unterbrechung |
| 0xA216 | Wischer: Endkontakt nicht erreicht |
| 0xA217 | Fensterheber: Taster FAT Unterbrechung |
| 0xA218 | Fensterheber: Taster BFT Unterbrechung |
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

Dimensions: 6 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| ?06? | ERROR_ECU_RESPONSE_INCORRECT_DATA_IDENTIFIER |
| ?07? | ERROR_ECU_RESPONSE_TOO_MUCH_DATA |
| ?08? | ERROR_ECU_RESPONSE_TOO_LESS_DATA |
| ?09? | ERROR_ECU_RESPONSE_VALUE_OUT_OF_RANGE |
| ?18? | ERROR_ECU_RESPONSE_NO_STRING_END_CHAR |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 5 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| 1 | D-CAN |
| - | BMW-FAST |
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 15 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PGO_ANALOG | 0xF101 | - | Gibt den aktuellen Wert der Analogeingänge zurück. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xF101 |
| PGO_WEGINFO_RAW | 0xF106 | - | Gibt die Rohdaten der Raddrehzahlsensoren zurück. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xF106 |
| PGO_FENSTERHEBER | 0xF112 | - | Gibt den Status der Fensterheber aus oder steuert diese an. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xF112 | RES_0xF112 |
| PGO_KLIMAANLAGE | 0xF113 | - | Gibt den Status der Klimaanlage aus oder steuert diese an. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xF113 | RES_0xF113 |
| PGO_TEMPOMAT | 0xF114 | - | Gibt den Status des Tempomaten zurück. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xF114 |
| PGO_INTERNE_STATI | 0xF115 | - | Gibt den aktuellen Wert der internen Stati zurück. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xF115 |
| PGO_INNENLICHT | 0xF116 | - | Gibt den aktuellen Wert der Innenlichtansteuerung zurück oder gibt diesen vor. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xF116 | RES_0xF116 |
| PGO_ANALOGINSTRUMENT | 0xF118 | - | Gibt den aktuellen Wert der Analoginstrumente vor. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xF118 | - |
| PGO_EINGAENGE | 0xF120 | - | Gibt den Status der Eingänge zurück. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xF120 |
| PGO_AUSGAENGE | 0xF121 | - | Gibt den Status der Ausgänge zurück oder steuert diese an. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xF121 | RES_0xF121 |
| PGO_WARNLEUCHTEN_KOMBI | 0xF122 | - | Gibt den Status der Warnleuchten im Kombi aus oder steuert diese an. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xF122 | RES_0xF122 |
| PGO_ZENTRALVERRIEGEL | 0xF124 | - | Gibt den Status der Zentralverriegelung aus oder steuert diese an. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xF124 | RES_0xF124 |
| PGO_SCHEIBENWISCHANLAGE | 0xF125 | - | Gibt den Status der Scheibenwischalnage aus oder steuert diese an. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xF125 | RES_0xF125 |
| PGO_AUSSENBELEUCHTUNG | 0xF126 | - | Gibt den Status der Aussenbeleuchtung aus oder steuert diese an. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xF126 | RES_0xF126 |
| PGO_SUMMER_KOMBI | 0xF132 | - | Steuert den Summer im Kombi an. | - | - | - | - | - | - | - | - | - | 2E | ARG_0xF132 | - |

<a id="table-tab-einaus"></a>
### TAB_EINAUS

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |

<a id="table-res-0xf101"></a>
### RES_0XF101

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ADC_VAL_VSUP_WERT | - | h | unsigned int | - | - | - | - | - | - |
| STAT_ADC_VAL_LUFTTEMP_WERT | - | h | unsigned int | - | - | - | - | - | - |
| STAT_ADC_VAL_FUELLEVEL_WERT | - | h | unsigned int | - | - | - | - | - | - |
| STAT_ADC_VAL_A_TEMP_WERT | - | h | unsigned int | - | - | - | - | - | - |
| STAT_ADC_VAL_BKL_LINKS_WERT | - | h | unsigned int | - | - | - | - | - | - |
| STAT_ADC_VAL_BKL_RECHTS_WERT | - | h | unsigned int | - | - | - | - | - | - |
| DUMMY_ADC_VAL_RES | DATA | - | data[8] | - | - | - | - | - | - |

<a id="table-res-0xf106"></a>
### RES_0XF106

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DUMMY_WEG01 | DATA | - | data[4] | - | - | - | - | - | - |
| STAT_KILOMETER_WERT | km | - | long | - | - | - | - | - | aktuell gespeicherter KM-Stand |
| DUMMY_WEG02 | DATA | - | data[6] | - | - | - | - | - | - |
| STAT_GESCHWINDIGKEIT_WERT | km/h | - | int | - | - | - | 9.89 | - | aktuell vorhandene Geschwindigkeit |
| STAT_RADIMPULSE1_WERT | - | - | long | - | - | - | - | - | Radimpulszähler links |
| DUMMY_WEG03 | DATA | - | data[8] | - | - | - | - | - | - |
| STAT_RADIMPULSE2_WERT | - | - | long | - | - | - | - | - | Radimpulszähler rechts |
| DUMMY_WEG04 | DATA | - | data[12] | - | - | - | - | - | - |

<a id="table-res-0xf112"></a>
### RES_0XF112

Dimensions: 9 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANFORDERUNG_FAT_AUF | 0/1 | - | unsigned char | - | - | - | - | - | Eingang Fensterheber FAT auf (A54) |
| STAT_ANFORDERUNG_FAT_ZU | 0/1 | - | unsigned char | - | - | - | - | - | Eingang Fensterheber FAT zu  (A52) |
| STAT_ANFORDERUNG_BFT_AUF | 0/1 | - | unsigned char | - | - | - | - | - | Eingang Fensterheber BFT auf (A53) |
| STAT_ANFORDERUNG_BFT_ZU | 0/1 | - | unsigned char | - | - | - | - | - | Eingang Fensterheber BFT zu  (A16) |
| STAT_ANSTEUERUNG_FAT_AUF | 0/1 | - | unsigned char | - | - | - | - | - | Ausgang Fensterheber FAT auf (B13) |
| STAT_ANSTEUERUNG_FAT_ZU | 0/1 | - | unsigned char | - | - | - | - | - | Ausgang Fensterheber FAT zu  (B31) |
| STAT_ANSTEUERUNG_BFT_AUF | 0/1 | - | unsigned char | - | - | - | - | - | Ausgang Fensterheber BFT auf (B49) |
| STAT_ANSTEUERUNG_BFT_ZU | 0/1 | - | unsigned char | - | - | - | - | - | Ausgang Fensterheber BFT zu  (B14) |
| DUMMY_FH01 | DATA | - | data[2] | - | - | - | - | - | - |

<a id="table-res-0xf113"></a>
### RES_0XF113

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TAST_KLIMAANLAGE | 0/1 | - | unsigned char | - | - | - | - | - | Eingang Taster Klimaanlage       (B46) |
| STAT_TEMPSCHALTER_KLIMA | 0/1 | - | unsigned char | - | - | - | - | - | Eingang Temperaturschalter Klima (B39) |
| STAT_AUSGANG_KLIMAKUPPLUNG | 0/1 | - | unsigned char | - | - | - | - | - | Status Ausgang Klimakupplung     (B24) |
| STAT_AUSGANG_KONTROLLLEUCHTE | 0/1 | - | unsigned char | - | - | - | - | - | Status Ausgang Kontrollleuchte Klimaanlage (B21) |
| STAT_DREHBEGRENZ_KLIMA_WERT | Nm | - | unsigned char | - | - | - | 2 | - | empfangenes Signal 'Klimakompressor_Begrenzung_Drehmoment' |
| STAT_CTR_KLIMA_BEREIT_WERT | - | - | unsigned char | - | - | - | 2 | - | gesendetes  Signal 'Steuerung_Klima_Bereitschaft' |
| DUMMY_KLIMA01 | DATA | - | data[1] | - | - | - | - | - | - |

<a id="table-res-0xf114"></a>
### RES_0XF114

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TEMPOMAT | 0/1 | - | unsigned char | - | - | - | - | - | aktueller Status des Tempomat |
| STAT_BEDIEN_TEMPOMAT | 0-n | - | unsigned char | - | TAB_BED_TEMPOMAT | - | - | - | erfasste Bedienung des Tempomathebels |
| DUMMY_TEMPOMAT | DATA | - | data[3] | - | - | - | - | - | - |

<a id="table-tab-bed-tempomat"></a>
### TAB_BED_TEMPOMAT

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |
| 0x02 | CMD_UP |
| 0x03 | CMD_UP + EIN |
| 0x04 | CMD_DOWN |
| 0x05 | CMD_DOWN + EIN |
| 0x08 | CMD_OFF |
| 0x09 | CMD_OFF + EIN |
| 0xFF | UNBEKANNT |

<a id="table-res-0xf115"></a>
### RES_0XF115

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_KLEMME_INTERN | 0-n | - | unsigned char | - | TAB_KLEMMENSTATUS | - | - | - | interner Klemmenstatus |
| STAT_A_TEMP_WERT | °C | - | unsigned int | - | - | - | 10 | - | Rohwert des Aussentemperatursensors  |
| STAT_TANKINHALT_WERT | ltr | - | unsigned char | - | - | - | - | - | Rohwert des Tankgebers |
| STAT_PTCAN_AKTIV | 0/1 | - | unsigned char | - | - | - | - | - | interner Status 'PT-CAN aktiv' |
| STAT_KCAN_AKTIV | 0/1 | - | unsigned char | - | - | - | - | - | interner Status 'K-CAN aktiv' |
| STAT_DSPLCAN_AKTIV | 0/1 | - | unsigned char | - | - | - | - | - | interner Status 'DSPL-CAN aktiv' |

<a id="table-tab-klemmenstatus"></a>
### TAB_KLEMMENSTATUS

Dimensions: 13 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | KL_VA |
| 0x02 | KL_R |
| 0x03 | KL_R |
| 0x06 | KL_15 |
| 0x07 | KL_15 |
| 0x0E | KL_50 |
| 0x0F | KL_50 |
| 0x16 | KL_61 |
| 0x17 | KL_61 |
| 0x1E | KL_61 |
| 0x1F | KL_61 |
| 0xFF | ungültig |

<a id="table-res-0xf116"></a>
### RES_0XF116

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHALTER_INNENLICHT | 0/1 | - | unsigned char | - | - | - | - | - | Eingang Schalter Innenlicht (B11) |
| STAT_INNENLICHT | 0/1 | - | unsigned char | - | - | - | - | - | Sollzustand Innenlicht |
| STAT_DIMMUNG_WERT | - | h | unsigned int | - | - | - | - | - | aktueller Dimmwert |

<a id="table-res-0xf120"></a>
### RES_0XF120

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHALTER_KLEMME_15 | 0/1 | - | unsigned char | - | - | - | - | - | Schalter 'Klemme 15' |
| STAT_SCHALTER_KLEMME_R | 0/1 | - | unsigned char | - | - | - | - | - | Schalter 'Klemme R' |
| STAT_TAST_SCHEIBENHEIZUNG | 0/1 | - | unsigned char | - | - | - | - | - | Taster 'Scheibenheizung' |
| STAT_BREMSPEDAL | 0/1 | - | unsigned char | - | - | - | - | - | Eingang 'Status Bremse' |
| STAT_SCHALTER_CRASH | 0/1 | - | unsigned char | - | - | - | - | - | Eingang 'Chrashschalter' |
| STAT_SCHALTER_GETRIEBE | 0/1 | - | unsigned char | - | - | - | - | - | Eingang 'release shifter' |

<a id="table-res-0xf121"></a>
### RES_0XF121

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ANST_SCHEIBENHEIZUNG | 0/1 | - | unsigned char | - | - | - | - | - | Ansteuerung Relais Scheibenheizung |
| STAT_ANST_MOTORLUEFTER | 0/1 | - | unsigned char | - | - | - | - | - | Ansteuerung Lüfter Motorraum |
| STAT_ANST_LEUCHTE_MIL | 0/1 | - | unsigned char | - | - | - | - | - | Ansteuerung Leuchte Motorwarnung MIL |
| STAT_ANST_LEUCHTE_OEL | 0/1 | - | unsigned char | - | - | - | - | - | Ansteuerung Leuchte Oeldruck |
| STAT_ANST_LEUCHTE_GEN | 0/1 | - | unsigned char | - | - | - | - | - | Ansteuerung Leuchte Ladekontrolle |
| STAT_ANST_LEUCHTE_WATEMP | 0/1 | - | unsigned char | - | - | - | - | - | Ansteuerung Leuchte Wassertemperatur |
| STAT_ANST_LEUCHTE_TANK | 0/1 | - | unsigned char | - | - | - | - | - | Ansteuerung Leuchte Tankfüllstand |
| STAT_ANST_LEUCHTE_ENGINE | 0/1 | - | unsigned char | - | - | - | - | - | Ansteuerung Leuchte Motorfehler |

<a id="table-res-0xf122"></a>
### RES_0XF122

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_WARNLED_KOMBI | BIT | - | BITFIELD | - | TAB_WARNLED | - | - | - | aktuelle Ansteuerung der Warnleuchten im Kombi |
| DUMMY_TEMPOMAT | DATA | - | data[2] | - | - | - | - | - | - |

<a id="table-tab-warnled"></a>
### TAB_WARNLED

Dimensions: 12 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_LED_GEAR | 0-n | - | long | 0x03000000 | TAB_LED_ZUSTAND | - | 0x01000000 | - | aktuelle Anforderung der LED 'Getriebe' ans Kombi |
| STAT_LED_MIL | 0-n | - | long | 0x0C000000 | TAB_LED_ZUSTAND | - | 0x08000000 | - | aktuelle Anforderung der LED 'MIL' ans Kombi |
| STAT_LED_GEN | 0-n | - | long | 0x30000000 | TAB_LED_ZUSTAND | - | 0x10000000 | - | aktuelle Anforderung der LED 'Ladekontrolle' ans Kombi |
| STAT_LED_OIL | 0-n | - | long | 0xC0000000 | TAB_LED_ZUSTAND | - | 0x80000000 | - | aktuelle Anforderung der LED 'Oel' ans Kombi |
| STAT_LED_FUEL | 0-n | - | long | 0x00030000 | TAB_LED_ZUSTAND | - | 0x00010000 | - | aktuelle Anforderung der LED 'Tankinhalt' ans Kombi |
| STAT_LED_ENG_WAT | 0-n | - | long | 0x000C0000 | TAB_LED_ZUSTAND | - | 0x00040000 | - | aktuelle Anforderung der LED 'Temperatur_Kühlwasser' ans Kombi |
| STAT_LED_ENG_FAULT | 0-n | - | long | 0x00300000 | TAB_LED_ZUSTAND | - | 0x00100000 | - | aktuelle Anforderung der LED 'Motorfehler' ans Kombi |
| STAT_LED_CTR_CRUISE | 0-n | - | long | 0x00C00000 | TAB_LED_ZUSTAND | - | 0x00400000 | - | aktuelle Anforderung der LED 'Tempomat' ans Kombi |
| STAT_LED_AC | 0-n | - | long | 0x00000300 | TAB_LED_ZUSTAND | - | 0x00000100 | - | aktuelle Anforderung der LED 'Klimaanlage' ans Kombi |
| STAT_LED_HEAT_WIND | 0-n | - | long | 0x00000C00 | TAB_LED_ZUSTAND | - | 0x00000400 | - | aktuelle Anforderung der LED 'Frontscheibenheizung' ans Kombi |
| STAT_LED_SEAT_BELT | 0-n | - | long | 0x00003000 | TAB_LED_ZUSTAND | - | 0x00001000 | - | aktuelle Anforderung der LED 'Gurtwarnung' ans Kombi |
| STAT_LED_SHIFT_REL | 0-n | - | long | 0x0000C000 | TAB_LED_ZUSTAND | - | 0x00004000 | - | aktuelle Anforderung der LED 'Gangfreischaltung' ans Kombi |

<a id="table-tab-led-zustand"></a>
### TAB_LED_ZUSTAND

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |
| 0x02 | RESERVIERT |
| 0x03 | UNGUELTIG |

<a id="table-res-0xf124"></a>
### RES_0XF124

Dimensions: 13 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TUER_FAT | 0-n | - | unsigned char | - | TAB_TUERSTATUS | - | - | - | Status_Türkontakt_FAT    (A1) |
| STAT_TUER_BFT | 0-n | - | unsigned char | - | TAB_TUERSTATUS | - | - | - | Status_Türkontakt_BFT    (A19) |
| STAT_HECKKLAPPE | 0-n | - | unsigned char | - | TAB_TUERSTATUS | - | - | - | Status Heckkl. Kontakt   (A2) |
| STAT_ZV_FAT | 0-n | - | unsigned char | - | TAB_ZV_STATUS | - | - | - | Status_ZV_FAT_verriegelt (A37) |
| STAT_ZV_BFT | 0-n | - | unsigned char | - | TAB_ZV_STATUS | - | - | - | Status_ZV_BFT_verriegelt (A24) |
| STAT_KONTROLL_ZV | 0/1 | - | unsigned char | - | - | - | - | - | Status Kontrolleuchte ZV |
| STAT_TAST_CENTERLOCK | 0/1 | - | unsigned char | - | - | - | - | - | Taster 'Centerlock'      (A20) |
| STAT_BEDIEN_ZV_ENTRIEG | 0/1 | - | unsigned char | - | - | - | - | - | Bedienung_ZV_entriegelt  (A34) |
| STAT_BEDIEN_ZV_VERRIEG | 0/1 | - | unsigned char | - | - | - | - | - | Bedienung_ZV_verriegelt  (A33) |
| STAT_AUSGANG_ZV_ENTRIEG | 0/1 | - | unsigned char | - | - | - | - | - | Status Ausgang 'ZV Tueren entriegeln'   (B12) |
| STAT_AUSGANG_ZV_VERRIEG | 0/1 | - | unsigned char | - | - | - | - | - | Status Ausgang 'ZV Tueren verriegeln'   (B47) |
| STAT_AUSGANG_HK_SCHLIESSEN | 0/1 | - | unsigned char | - | - | - | - | - | Status Ausgang 'ZV-Bolzen HK schliessen'(B50) |
| STAT_AUSGANG_HK_OEFFNEN | 0/1 | - | unsigned char | - | - | - | - | - | Status Ausgang 'ZV-Bolzen HK oeffnen'   (B32) |

<a id="table-tab-tuerstatus"></a>
### TAB_TUERSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | GESCHLOSSEN |
| 0x01 | OFFEN |
| 0xFF | UNBEKANNT |

<a id="table-tab-zv-status"></a>
### TAB_ZV_STATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ENTRIEGELT |
| 0x01 | VERRIEGELT |
| 0xFF | UNBEKANNT |

<a id="table-res-0xf125"></a>
### RES_0XF125

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHEIBENWISCHERENDSTELL | 0/1 | - | unsigned char | - | - | - | - | - | Eingang 'Endstellung Scheibenwischer' (A41) |
| STAT_SCHEIBENW_INTERVALL | 0/1 | - | unsigned char | - | - | - | - | - | Eingang 'Scheibenwischer Intervall'   (A22) |
| STAT_SCHWIBENWASCHANL | 0/1 | - | unsigned char | - | - | - | - | - | Eingang 'Scheibenwaschanlage'         (A40) |
| STAT_WISCHERNACHLAUF | 0/1 | - | unsigned char | - | - | - | - | - | Ausgang 'Wischer_Nachlauf'            (B41) |

<a id="table-res-0xf126"></a>
### RES_0XF126

Dimensions: 8 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHALTER_STANDLICHT | 0/1 | - | unsigned char | - | - | - | - | - | Schalter 'Status Standlicht'  (A43) |
| STAT_SCHALTER_ABBLENDLICHT | 0/1 | - | unsigned char | - | - | - | - | - | Schalter 'Abblendlicht ein'   (A25) |
| STAT_TAST_WARNBLINKER | 0/1 | - | unsigned char | - | - | - | - | - | Taster 'Warnblinker'          (A39) |
| STAT_TAST_BLINKER_LI | 0/1 | - | unsigned char | - | - | - | - | - | Taster 'Blinker links'        (A5) |
| STAT_TAST_BLINKER_RE | 0/1 | - | unsigned char | - | - | - | - | - | Taster 'Blinker rechts'       (A23) |
| STAT_KONTROLL_WARNBLINKER | 0/1 | - | unsigned char | - | - | - | - | - | Ausgang Kontrolle Warnblinker (B20) |
| STAT_AUSGANG_BLINKER_LI | 0/1 | - | unsigned char | - | - | - | - | - | Ausgang Blinker links         (A35) |
| STAT_AUSGANG_BLINKER_RE | 0/1 | - | unsigned char | - | - | - | - | - | Ausgang Blinker rechts        (A36) |

<a id="table-arg-0xf112"></a>
### ARG_0XF112

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSWAHL_FENSTERHEBER | 0-n | - | unsigned int | - | TAB_FH_AUSWAHL | - | - | - | - | - | 1=FH_Fahrertür,2=FH_Beifahrertür |
| RICHTUNG_FENSTERHEBER | 0-n | - | unsigned int | - | TAB_FH_RICHT | - | - | - | - | - | Ansteuerrichtung 1=AUF, 2=ZU |
| ANSTEUER_ZEIT | ms | - | unsigned int | - | - | - | - | - | - | - | Ansteuerzeit in ms |

<a id="table-tab-fh-auswahl"></a>
### TAB_FH_AUSWAHL

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | FAHRER |
| 0x02 | BEIFAHRER |

<a id="table-tab-fh-richt"></a>
### TAB_FH_RICHT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | AUF |
| 0x02 | ZU |

<a id="table-arg-0xf113"></a>
### ARG_0XF113

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ANSTEUERUNG_KLIMAKUPPLUNG | 0-n | - | unsigned char | - | TAB_EINAUS | - | - | - | - | - | Ausgang Klimakupplung ansteuern |
| ANSTEUERUNG_KONTROLLLEUCHTE | 0-n | - | unsigned char | - | TAB_EINAUS | - | - | - | - | - | Ausgang Kontrollleuchte Klimaanlage ansteuern |

<a id="table-arg-0xf116"></a>
### ARG_0XF116

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DIMMUNG_INNENLICHT | - | - | unsigned char | - | - | - | - | - | - | - | Ansteuerung Innenlicht 0 -100% |
| DIMMUNG_LED_INNENLICHT | - | - | unsigned char | - | - | - | - | - | - | - | Ansteuerung LED_Innenleuchten 0 -100% |
| ANSTEUER_ZEIT | ms | - | int | - | - | - | - | - | - | - | Ansteuerzeit in ms |

<a id="table-arg-0xf118"></a>
### ARG_0XF118

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSWAHL_ANALOGINSTRUMENT | 0-n | - | unsigned char | - | TAB_INST_AUSWAHL | - | - | - | - | - | 1 = Drehzahlmesser, 2 = Tachoanzeige,3 = Tankanzeige, 4 = Wassertemperatur |
| WERT_ANALOGINSTRUMENT | - | - | unsigned char | - | - | - | - | - | - | - | Ansteuerwert Analoginstrumente 0-100% |
| ANSTEUER_ZEIT | ms | - | int | - | - | - | - | - | - | - | Ansteuerzeit in ms |

<a id="table-tab-inst-auswahl"></a>
### TAB_INST_AUSWAHL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Drehzahlmesser |
| 0x02 | Tachoanzeige |
| 0x03 | Tankanzeige |
| 0x04 | Wassertemperatur |

<a id="table-arg-0xf121"></a>
### ARG_0XF121

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSWAHL_DIGITALAUSGANG | 0-n | - | unsigned char | - | TAB_OUT_AUSWAHL | - | - | - | - | - | Ausgang laut Tabelle |
| ANSTEUER_ZEIT | ms | - | int | - | - | - | - | - | - | - | Ansteuerzeit in ms |

<a id="table-tab-out-auswahl"></a>
### TAB_OUT_AUSWAHL

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | SCHEIBENHEIZUNG |
| 0x02 | MOTORLUEFTER |
| 0x03 | LEUCHTE_MIL |
| 0x04 | LEUCHTE_OEL |
| 0x05 | LEUCHTE_GEN |
| 0x06 | LEUCHTE_WATEMP |
| 0x07 | LEUCHTE_TANK |
| 0x08 | LEUCHTE_ENGINE |

<a id="table-arg-0xf122"></a>
### ARG_0XF122

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSWAHL_LED_KOMBI | 0-n | - | unsigned char | - | TAB_LED_AUSWAHL | - | - | - | - | - | Auswahl der anzusteuernden LED laut Tabelle |
| WERT_LED_KOMBI | 0-n | - | unsigned char | - | TAB_EINAUS | - | - | - | - | - | Schaltwert 0= Aus, 1= Ein   |
| ANSTEUER_ZEIT | ms | - | unsigned int | - | - | - | - | - | - | - | Ansteuerzeit in ms |

<a id="table-tab-led-auswahl"></a>
### TAB_LED_AUSWAHL

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Getriebe |
| 0x02 | MIL |
| 0x03 | Ladekontrolle |
| 0x04 | Oel |
| 0x05 | Tankinhalt |
| 0x06 | Temperatur_Kühlwasser |
| 0x07 | Motorfehler |
| 0x08 | Tempomat |
| 0x09 | Klimaanlage |
| 0x0A | Frontscheibenheizung |
| 0x0B | Gurtwarnung |

<a id="table-arg-0xf124"></a>
### ARG_0XF124

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERN_ZV | 0-n | - | unsigned char | - | TAB_ZV_STEUERN | - | - | - | - | - |  steuert die ZV über Diagnose an |

<a id="table-tab-zv-steuern"></a>
### TAB_ZV_STEUERN

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x51 | ENTRIEGELT |
| 0x52 | VERRIEGELT |

<a id="table-arg-0xf125"></a>
### ARG_0XF125

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERN_WISCHER | 0-n | - | unsigned char | - | TAB_EINAUS | - | - | - | - | - | steuert über den Ausgang 'Wischernachlauf den Wischer an |
| ANSTEUER_ZEIT | ms | - | int | - | - | - | - | - | - | - | Ansteuerzeit in ms |

<a id="table-arg-0xf126"></a>
### ARG_0XF126

Dimensions: 3 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUSGANG_BLINKER_LI | 0-n | - | unsigned char | - | TAB_EINAUS | - | - | - | - | - | steuert den Ausgang Blinker links an |
| AUSGANG_BLINKER_RE | 0-n | - | unsigned char | - | TAB_EINAUS | - | - | - | - | - | steuert den Ausgang Blinker rechts an |
| ANSTEUER_ZEIT | ms | - | int | - | - | - | - | - | - | - | Ansteuerzeit in ms |

<a id="table-arg-0xf132"></a>
### ARG_0XF132

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STEUERN_SUMMER | 0-n | - | unsigned char | - | TAB_EINAUS | - | - | - | - | - | steuert den Summer im Kombi an 1= Ein 0=Aus |
| ANSTEUER_ZEIT | ms | - | int | - | - | - | - | - | - | - | Ansteuerzeit in ms |
