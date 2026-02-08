# ahm_70.prg

- Jobs: [78](#jobs)
- Tables: [35](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Anhängermodul IV R |
| ORIGIN | BMW EI-60 UweLueddeke |
| REVISION | 2.000 |
| AUTHOR | HelbakoGmbH SW-Entwicklung GerritBöger, HelbakoGmbH SW-Entwickl |
| COMMENT | N/A |
| PACKAGE | 1.50 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default
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
- [STATUS_ANALOG_OUTPUT_AHM_ECE](#job-status-analog-output-ahm-ece) - ReadDataByCommonIdentifier 0x22 0xF5F6 AHM_ANALOG_OUTPUT_ECE
- [STATUS_ANALOG_OUTPUT_AHM_SAE](#job-status-analog-output-ahm-sae) - 22 0xF5FF AHM_ANALOG_OUTPUT_SAE
- [STATUS_DIGITAL_AHM_ECE](#job-status-digital-ahm-ece) - Liest den digitalen Status ein 22 0xF5F3 AHM_DIGITAL_ECE
- [STATUS_DIGITAL_AHM_SAE](#job-status-digital-ahm-sae) - Liest den digitalen Status ein 22 0xF5F4 AHM_DIGITAL_SAE
- [INTERNE_DATEN](#job-interne-daten) - interne Daten
- [STATUS_BUS_NACHRICHTEN](#job-status-bus-nachrichten) - Liefert die Signale/Werte über BUS 22 0xF050 internen Status AHM lesen
- [STATUS_INITIALISIERUNG](#job-status-initialisierung) - 22 0xF5EB AHM_INITIALISIERUNG
- [STATUS_DIAGNOSE_AHV](#job-status-diagnose-ahv) - Status der Diagnose des AHV 22 0xF5FD AHV_DIAGNOSE_STATUS
- [STATUS_ANALOGEINGAENGE](#job-status-analogeingaenge) - 22 0xF5EC AHV_ANALOG_EINGANG
- [STATUS_POSITION_AHV](#job-status-position-ahv) - 22 0xF5FB AHV_POSITION_NR
- [STATUS_ANALOGAUSGAENGE](#job-status-analogausgaenge) - 22 0xF5FC AHV_MOTOR_STROM_WERT
- [STEUERN_LAMPEN_FUNKTION_AHM_ECE](#job-steuern-lampen-funktion-ahm-ece) - Steuern der Lampenfunktionen im Anhängermodul 2E 2E 0xF5F1 AHM_STEUERN_LAMPEN_FUNKTION_ECE
- [STEUERN_LAMPEN_FUNKTION_AHM_SAE](#job-steuern-lampen-funktion-ahm-sae) - Steuern der Lampenfunktionen im Anhängermodul 2E 0xF5F2 AHM_STEUERN_LAMPEN_FUNKTION_SAE
- [STEUERN_INITIALISIERUNG_AHV](#job-steuern-initialisierung-ahv) - 2E 0xF5EA AHV_START_INITIALISIERUNG
- [STEUERN_AHV_MOTOR](#job-steuern-ahv-motor) - 2E 0xF5E4 AHV_STEUERN_MOTOR
- [STEUERN_LED_AHV](#job-steuern-led-ahv) - 2E 0xF5FE AHV_LED
- [STATUS_ST_AHV_LIN](#job-status-st-ahv-lin) - 22 0xF500 ST_AHV_LIN
- [STATUS_CTR_AHV_LIN](#job-status-ctr-ahv-lin) - 22 0xF501 CTR_AHV_LIN
- [STATUS_AHV_ENDSENSOREN](#job-status-ahv-endsensoren) - Auslesen des Endlagensensors UDS  : $22   ReadDataByIdentifier UDS  : $F5E0 AHV-Endlagensensor(en) Modus: Default
- [STATUS_TEILELEKTRISCHE_AHV](#job-status-teilelektrische-ahv) - 22 0xF050 READ_DATA_DIGITAL_SIGNALS
- [STATUS_INKREMENTALPOSITION](#job-status-inkrementalposition) - ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Positionszählers (Inkremente) auslesen
- [STATUS_AHV_ABSCHALTSTROM](#job-status-ahv-abschaltstrom) - ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Motorstrom zum Zeitpunkt der Motorabschaltung auslesen
- [STATUS_AHV_CRC_PARAMETER](#job-status-ahv-crc-parameter) - ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Checksumme der Bosal-Parameter auslesen
- [STATUS_AHV_SCHWENKZAEHLER](#job-status-ahv-schwenkzaehler) - ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Schwenkzähler auslesen
- [STATUS_AHV_PERIPHERIEFEHLER](#job-status-ahv-peripheriefehler) - ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV
- [STATUS_AHV_AD_1_2_ROH](#job-status-ahv-ad-1-2-roh) - ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Rohwerte AD-Wandler-Kanal 1 und 2 auslesen
- [STATUS_AHV_AD_3_4_ROH](#job-status-ahv-ad-3-4-roh) - ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Rohwerte AD-Wandler-Kanal 3 und 4 auslesen
- [STATUS_AHV_CONTAINER](#job-status-ahv-container) - ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Container zum Senden beliebiger LIN-Diagnosenachrichten Beispiel 0x7F 0x06 0xB4 0x11 0xFF 0xFF 0xFF 0xFF Werte bei Parametereingabe durch Semikolon trennen
- [AHV_STEUERGERAETE_RESET](#job-ahv-steuergeraete-reset) - ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Reset des AHV2-Steuergerätes

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

<a id="job-sensoren-anzahl-lesen"></a>
### SENSOREN_ANZAHL_LESEN

Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_ANZAHL | long | Anzahl der intelligenten Subbussensoren |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sensoren-ident-lesen"></a>
### SENSOREN_IDENT_LESEN

Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_NR | long | optionales Argument gewuenschter Sensor xx (0x01 - 0xFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_VERBAUORT | string | Verbauort des Sensors table VerbauortTabelle ORTTEXT |
| SENSOR_BMW_NR | string | BMW-Teilenummer des Sensors |
| SENSOR_PART_NR | string | Teilenummer des Sensors optional wenn SENSOR_BMW_NR gueltig wenn vom Teilenummer vom Sensor nicht verfuegbar dann '--' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

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

<a id="job-status-analog-output-ahm-ece"></a>
### STATUS_ANALOG_OUTPUT_AHM_ECE

ReadDataByCommonIdentifier 0x22 0xF5F6 AHM_ANALOG_OUTPUT_ECE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STROM_SL_LI_WERT | real | Liest den Messwert Stromfluß Lastkreis 1 aus |
| STAT_STROM_SL_LI_EINH | string | Liest den Messwert Stromfluß Lastkreis 1 aus |
| STAT_STROM_NSL_WERT | real | Liest den Messwert Stromfluß Lastkreis 2 aus |
| STAT_STROM_NSL_EINH | string | Liest den Messwert Stromfluß Lastkreis 2 aus |
| STAT_STROM_FRA_LI_WERT | real | Liest den Messwert Stromfluß Lastkreis 3 aus |
| STAT_STROM_FRA_LI_EINH | string | Liest den Messwert Stromfluß Lastkreis 3 aus |
| STAT_STROM_FRA_RE_WERT | real | Liest den Messwert Stromfluß Lastkreis 4 aus |
| STAT_STROM_FRA_RE_EINH | string | Liest den Messwert Stromfluß Lastkreis 4 aus |
| STAT_STROM_BRL_WERT | real | Liest den Messwert Stromfluß Lastkreis 5 aus |
| STAT_STROM_BRL_EINH | string | Liest den Messwert Stromfluß Lastkreis 5 aus |
| STAT_STROM_RFL_WERT | real | Liest den Messwert Stromfluß Lastkreis 6 aus |
| STAT_STROM_RFL_EINH | string | Liest den Messwert Stromfluß Lastkreis 6 aus |
| STAT_STROM_SL_RE_WERT | real | Liest den Messwert Stromfluß Lastkreis 7 aus |
| STAT_STROM_SL_RE_EINH | string | Liest den Messwert Stromfluß Lastkreis 7 aus |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-output-ahm-sae"></a>
### STATUS_ANALOG_OUTPUT_AHM_SAE

22 0xF5FF AHM_ANALOG_OUTPUT_SAE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STROM_TAIL_LIGHT_PART1_WERT | real | "Liest den Messwert Stromfluss Tail And License Light Part 1 aus (AHM4: Lastkreis 1)" |
| STAT_STROM_TAIL_LIGHT_PART1_EINH | string | "Liest den Messwert Stromfluss Tail And License Light Part 1 aus (AHM4: Lastkreis 1)" |
| STAT_STROM_TAIL_LIGHT_PART2_WERT | real | "Liest den Messwert Stromfluss Tail And License Light Part 2 aus (AHM4: Lastkreis 2)" |
| STAT_STROM_TAIL_LIGHT_PART2_EINH | string | "Liest den Messwert Stromfluss Tail And License Light Part 2 aus (AHM4: Lastkreis 2)" |
| STAT_STROM_STOP_TURN_LIGHT_LEFT_WERT | real | "Liest den Messwert Stromfluss Stop Turn Light Left aus (AHM4: Lastkreis 3)" |
| STAT_STROM_STOP_TURN_LIGHT_LEFT_EINH | string | "Liest den Messwert Stromfluss Stop Turn Light Left aus (AHM4: Lastkreis 3)" |
| STAT_STROM_STOP_TURN_LIGHT_RIGHT_WERT | real | "Liest den Messwert Stromfluss Stop Turn Light Right aus (AHM4: Lastkreis 4)" |
| STAT_STROM_STOP_TURN_LIGHT_RIGHT_EINH | string | "Liest den Messwert Stromfluss Stop Turn Light Right aus (AHM4: Lastkreis 4)" |
| STAT_STROM_REVERSING_LIGHT_WERT | real | "Liest den Messwert Stromfluss Reversing Light aus (AHM4: Lastkreis 7)" |
| STAT_STROM_REVERSING_LIGHT_EINH | string | "Liest den Messwert Stromfluss Reversing Light aus (AHM4: Lastkreis 7)" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-ahm-ece"></a>
### STATUS_DIGITAL_AHM_ECE

Liest den digitalen Status ein 22 0xF5F3 AHM_DIGITAL_ECE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SL_RECHTS_EIN | char | Liest den Status von Schlusslicht rechts aus  0 = AUS 1 = EIN |
| STAT_SL_LINKS_EIN | char | Liest den Status von Schlusslicht links aus  0 = AUS 1 = EIN |
| STAT_FRA_RECHTS_EIN | char | Liest den Status von Blinklicht rechts aus  "0 = AUS 1 = EIN" |
| STAT_FRA_LINKS_EIN | char | Liest den Status von Blinklicht links aus  "0 = AUS 1 = EIN" |
| STAT_BRL_EIN | char | Liest den Status von Bremslicht aus  "0 = AUS 1 = EIN" |
| STAT_NSL_EIN | char | Liest den Status von Nebelschlusslicht aus  "0 = AUS 1 = EIN" |
| STAT_RFL_EIN | char | Liest den Status von Rückfahrscheinwerfer aus "0 = AUS 1 = EIN" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-ahm-sae"></a>
### STATUS_DIGITAL_AHM_SAE

Liest den digitalen Status ein 22 0xF5F4 AHM_DIGITAL_SAE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TAIL_LIGHT_EIN | char | Liest den Status von Schlusslicht aus  0 = AUS 1 = EIN |
| STAT_STOP_TURN_LIGHT_RIGHT_EIN | char | Liest den Status von Brems-/Blinklicht rechts aus  "0 = AUS 1 = blinkt 2 = EIN" |
| STAT_STOP_TURN_LIGHT_RIGHT_EIN_TEXT | string | Liest den Status von Brems-/Blinklicht rechts aus Siehe Tabelle TAB_AHM_DIGITAL |
| STAT_STOP_TURN_LIGHT_LEFT_EIN | char | Liest den Status von Brems-/Blinklicht links aus  "0 = AUS 1 = blinkt 2 = EIN" |
| STAT_STOP_TURN_LIGHT_LEFT_EIN_TEXT | string | Liest den Status von Brems-/Blinklicht links aus Siehe Tabelle TAB_AHM_DIGITAL |
| STAT_REVERSING_LIGHT_EIN | char | Liest den Status von Rückfahrscheinwerfer aus "0 = AUS 1 = EIN" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-interne-daten"></a>
### INTERNE_DATEN

interne Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW | int | SG-interne SW-Version |
| BTLD | int | SG-interne Bootloader-Version |
| LAYOUT | int | SG-interne HW-Version |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bus-nachrichten"></a>
### STATUS_BUS_NACHRICHTEN

Liefert die Signale/Werte über BUS 22 0xF050 internen Status AHM lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BUS_IN_HK_OFFEN | char | Ausgabe des über CAN gesendeten Heckklappenstatus  "0 = geschlossen 1 = offen" |
| STAT_BUS_IN_HS_OFFEN | char | Ausgabe des über CAN gesendeten Heckscheibenstatus  "0 = geschlossen 1 = offen" |
| STAT_BUS_IN_KL_15_EIN | char | Ausgabe des über CAN gesendeten Kl.15 Status "0 = Kl.15 aus 1 = Kl.15 ein" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-initialisierung"></a>
### STATUS_INITIALISIERUNG

22 0xF5EB AHM_INITIALISIERUNG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INITIALISIERUNG_AHV_INIT | char | Gibt den aktueller Zustand der Initialisierung. Siehe Tabelle "TAB_INIT" |
| STAT_INITIALISIERUNG_AHV_INIT_TEXT | string | Gibt den aktueller Zustand der Initialisierung. Siehe Tabelle "TAB_INIT" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-diagnose-ahv"></a>
### STATUS_DIAGNOSE_AHV

Status der Diagnose des AHV 22 0xF5FD AHV_DIAGNOSE_STATUS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_AHV | char | Status der INITIALISIERUNG. Es muss erst die Initialisierung gestartet werden. |
| STAT_DIAGNOSE_AHV_TEXT | string | Status der INITIALISIERUNG. Es muss erst die Initialisierung gestartet werden. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analogeingaenge"></a>
### STATUS_ANALOGEINGAENGE

22 0xF5EC AHV_ANALOG_EINGANG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TASTER_AHV_EIN | char | Gibt den Status des Taster für die Anhängevorrichtung aus: 0 = Taste nicht gedrückt  1 = Taste gedrückt |
| STAT_SCHALTER_AH_STECKDOSE_GESTECKT | char | Liest den Status des Mikroschalters in der Anhängersteckdose aus dem AHV-SG aus: 0= Nicht gesteckt  1 = Gesteckt. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-position-ahv"></a>
### STATUS_POSITION_AHV

22 0xF5FB AHV_POSITION_NR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POSITION_AHV_NR | char | Position der AHV-Stellung  Siehe Tabelle TAB_AHV_POSITIONEN |
| STAT_POSITION_AHV_NR_TEXT | string | Position der AHV-Stellung  Siehe Tabelle TAB_AHV_POSITIONEN |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analogausgaenge"></a>
### STATUS_ANALOGAUSGAENGE

22 0xF5FC AHV_MOTOR_STROM_WERT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AHV_MOTOR_STROM_WERT | real | Ausgabe des AHV-Motorstroms in Ampere  0 bis 50,8 A |
| STAT_AHV_MOTOR_STROM_EINH | string | Ausgabe des AHV-Motorstroms in Ampere  0 bis 50,8 A |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lampen-funktion-ahm-ece"></a>
### STEUERN_LAMPEN_FUNKTION_AHM_ECE

Steuern der Lampenfunktionen im Anhängermodul 2E 2E 0xF5F1 AHM_STEUERN_LAMPEN_FUNKTION_ECE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ELEMENT | string | Steuert das Anhängemodul an. Tabelle: TAB_AUSSEN_LICHT_HINTEN |
| ZEIT | int | Ansteuerzeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lampen-funktion-ahm-sae"></a>
### STEUERN_LAMPEN_FUNKTION_AHM_SAE

Steuern der Lampenfunktionen im Anhängermodul 2E 0xF5F2 AHM_STEUERN_LAMPEN_FUNKTION_SAE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ELEMENT | string | Steuert das Anhängemodul an. |
| ZEIT | int | Ansteuerzeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-initialisierung-ahv"></a>
### STEUERN_INITIALISIERUNG_AHV

2E 0xF5EA AHV_START_INITIALISIERUNG

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | Steuert die Initialisierung der AHV. Siehe Tabelle "TAB_AHM_INIT" Mögliche Werte keine Aktion AUSSCHWENKEN EINSCHWENKEN Initialisierung abbrechen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ahv-motor"></a>
### STEUERN_AHV_MOTOR

2E 0xF5E4 AHV_STEUERN_MOTOR

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RICHTUNG | string | Steuert den Motor der AHV an. PosSiehe Tabelle "TAB_AHV_VERFAHREN" Mögliche Werte keine Änderung Ansteuerung Richtung Ruheposition Ansteuerung Richtung Arbeitsposition Ansteuerung abbrechen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-led-ahv"></a>
### STEUERN_LED_AHV

2E 0xF5FE AHV_LED

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FARBE | string | Steuert die LED mit der Farbe in Dauerlicht an  "0 = Ansteuerung aus (LED aus) 1 = Ansteuerung Grün 2 = Ansteuerung Rot" |
| ZEIT | char | Ansteuerzeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-st-ahv-lin"></a>
### STATUS_ST_AHV_LIN

22 0xF500 ST_AHV_LIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_I_AHV_LIN_ROH | unsigned char | LIN-Signal I_AHV_LIN Aktuelle Stromaufnahme des Motors 0.2A/Digit |
| STAT_I_AHV_LIN_WERT | real | LIN-Signal I_AHV_LIN Aktuelle Stromaufnahme des Motors in A |
| STAT_I_AHV_LIN_EINH | string | LIN-Signal I_AHV_LIN Aktuelle Stromaufnahme des Motors "A" |
| STAT_ERR_SEN_AHV_LIN | unsigned char | LIN-Signal ERR_SEN_AHV_LIN Signal zur Diagnose des AHV Systems 0 OK 1 Leitungsunterbrechung od.Kurzschluss nach Minus. Führt zu DTC-Eintrag im AHM 2 Kurzschluss nach Plus  Führt zu DTC-Eintrag im AHM 3 Signal ungültig |
| STAT_ST_PO_AHV_LIN | unsigned char | LIN-Signal ST_PO_AHV_LIN Beschreibung der aktuellen Position des Kugelkopfes 0  Endlage ausgefahren  (Arbeitsposition) 1  Endlage eingefahren  (Ruheposition) 2  Zwischenposition 3  Endlage ausgefahren  (keine Nachtaktung) 4  Mechanik schwenkt EIN  Bewegung in Richtung Ruheposition 5  Mechanik schwenkt AUS  Bewegung in Richtung Arbeitsposition 7  Signal ungültig |
| STAT_ST_INIT_AHV_LIN | unsigned char | LIN-Signal ST_INIT_AHV_LIN Aktueller Zustand der Initialisierung der AHV 0 AHV initialisiert 1 AHV nicht initialisiert  Führt zu DTC-Eintrag im AHM (Anlieferungszustand) 2 Initialisierung in Abarbeitung 3 Fehler bei Initialisierung 7 Signal ungültig |
| STAT_ERR_ST_U_AHV_LIN | unsigned char | LIN-Signal ERR_ST_U_AHV_LIN Im AHV-System kam es zu Unter- oder Überspannung und die Funktionalität war nicht mehr gegeben. Im nächsten Zyklus im normalen Spannungsbereich wird dieser Zustand übermittelt 0 kein Über- oder Unterspannung aufgetreten IO Zustand 1 Funktionsabbruch durch Unterspannung Führt zu DTC-Eintrag im AHM 2 Funktionsabbruch durch Überspannung Führt zu DTC-Eintrag im AHM 3 Signal ungültig |
| STAT_ERR_ST_ADMO_AHV_LIN | unsigned char | LIN-Signal ERR_ST_ADMO_AHV_LIN Fehlerstatus des Verstellmotors 0 kein Fehler 1 mechanischer Fehler  Führt zu DTC-Eintrag im AHM 2 Nachspannen Fehlgeschlagen Führt zu DTC-Eintrag im AHM 3 Lösen Fehlgeschlagen  Führt zu DTC-Eintrag im AHM 4 Leitungsunterbrechung  Führt zu DTC-Eintrag im AHM 5 Kurzschluss nach Minus  Führt zu DTC-Eintrag im AHM 6 Kurzschluss nach Plus  Führt zu DTC-Eintrag im AHM 7 Signal ungültig |
| STAT_ERR_ST_ADMO_OCU_AHV_LIN | unsigned char | LIN-Signal ERR_ST_ADMO_OCU_AHV_LIN Signal zur Diagnose des AHV-Systems. Tritt beim Schwenkvorgang der AHV ein Überstrom auf, z. B. durch Festhalten des Kugelkopfes (Einklemmschutz), erfolgt eine Überstromabschaltung 0 kein Fehler 1 Überstromabschaltung Führt zu DTC-Eintrag im AHM 2 Offsetgrenze erreicht Führt zu DTC-Eintrag im AHM 3 Signal ungültig |
| STAT_TOG_AHV_LIN | unsigned char | LIN-Signal TOG_AHV_LIN Alive-Signal des AHV2-Steuergerätes Signal toggelt zwischen 0 und 1 |
| STAT_ST_SW_PLG_AHV_LIN | unsigned char | LIN-Signal ST_SW_PLG_AHV_LIN Anhängererkennung durch den Mikroschalter in der Anhängersteckdose Wird durch den gesteckten Anhängerstecker oder Adapter ausgelöst 0 Mikroschalter nicht betätigt 1 Mikroschalter betätigt  Anhänger erkannt oder Adapter gesteckt 2 Mikroschalter defekt, Leitungsunterbrechung, Kurzschluss nach Plus Führt zu DTC-Eintrag im AHM 3 Signal ungültig |
| STAT_ST_PUBU_AHV_LIN | unsigned char | LIN-Signal ST_PUBU_AHV_LIN Das AHV teilt dem AHM eine Betätigung des Tasters mit 0 Taster nicht gedrückt 1 Taster gedrückt 2 Taster Kurzschluss gegen Masse (Defekt hängend Erkennung während Start UP) Führt zu DTC-Eintrag im AHM 3 Signal ungültig |
| STAT_ERR_ST_INTL_AHV_LIN | unsigned char | LIN-Signal ERR_ST_INTL_AHV_LIN Signal zur Diagnose des AHV-Systems. Tritt bei einem internen Fehler im Steuergerät auf und führt zum Tausch des Steuergerätes 0 kein Fehler 1 Steuergerät defekt  Führt zu DTC-Eintrag im AHM 3 Signal ungültig |
| STAT_NOD_ERR_AHV_LIN | unsigned char | LIN-Signal NOD_ERR_AHV_LIN Fehlerspeichereinträge im AHM werden nur abgespeichert oder der Status geändert wenn dieses Signal den Status Fehler aktiv oder Fehler Statusänderung aufweist 0  Kein Fehler 1  Fehler aktiv 2  Fehler Statusänderung 3  Signal ungültig |
| STAT_ST_DIAG_RQ_AHV_LIN | unsigned char | LIN-Signal ST_DIAG_RQ_AHV_LIN Dieses Signal teilt dem Master SG mit ob die CRC in der Nachricht Gechwindigkeit_Fahrzeug_LIN richtig berechnet wurde und ob die Diagnoseanforderung ausgeführt wurde 0  Kein Fehler 1  Berechnung der CRC Falsch 2  Geschwindigkeitswert größer 0 3  Signal ungültig |
| STAT_ST_ESTP_SEN_01_AHV_LIN | unsigned char | LIN-Signal ST_ESTP_SEN_01_AHV_LIN Fehlerzustände des ersten Mikroschalters. 0 Kein Fehler 1 Leitungsunterbrechung 2 Kurzschluss nach Plus 3 Kurzschluss nach Masse 4 Endanschlag erreicht  AHV2: Mikroschalter in Stellung Arbeitsposition 5 Endanschlag nicht erreicht  AHV2: Mikroschalter in Stellung Ruheposition, bzw. Zwischenposition 7 Signal ungültig |
| STAT_COMM_ERR_AHV_LIN | unsigned char | LIN-Signal COMM_ERR_AHV_LIN Dieses Signal zeigt an, ob ein Fehler in der Kommunikation zwischen AHM und AHV vorliegt, bzw. vorlag. Dies wird durch einen Fehler im CRC erkannt 0 kein Fehler 1 Fehler aktiv |
| STAT_ST_ESTP_SEN_02_AHV_LIN | unsigned char | LIN-Signal ST_ESTP_SEN_02_AHV_LIN Fehlerzustände des zweiten Mikroschalters. 0 Kein Fehler 1 Leitungsunterbrechung 2 Kurzschluss nach Plus 3 Kurzschluss nach Masse 4 Endanschlag erreicht 5 Endanschlag nicht erreicht 7 Signal ungültig |
| STAT_ST_LED_RLS_AHV_LIN | unsigned char | LIN-Signal ST_LED_RLS_AHV_LIN Status der grünen LED 0 LED Aus 1 LED Ein 2 LED defekt 7 Signal ungültig |
| STAT_ST_LED_ILK_AHV_LIN | unsigned char | LIN-Signal ST_LED_ILK_AHV_LIN Status der roten LED 0 LED Aus 1 LED Ein 2 LED defekt 7 Signal ungültig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ctr-ahv-lin"></a>
### STATUS_CTR_AHV_LIN

22 0xF501 CTR_AHV_LIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ST_KL_AHV_LIN | unsigned char | LIN-Signal ST_KL_AHV_LIN Dieses Signal entspricht dem CAN-Signal "Status_Klemme" Alle höherwertigen Codierungs-Werte des Signals  ST_KL implizieren die darunterliegenden Zustände 0 Init 1 Reserve 2 KL30 Alle Klemmen aus 3 KL30F-Änderung 4 KL30F-Ein 5 KL30B-Änderung 6 KL30B-Ein 7 KLR-Änderung 8 KLR-Ein 9 KL15-Änderung 10 KL15-Ein 11 KL50-Verzögerung  Komfortstart aktiv, Diesel vorglühen, Motor-Relais anziehen 12 KL50-Änderung 13 KL50-Ein 14 Fehler 15 Signal ungültig |
| STAT_CTR_LED_AHV_LIN | unsigned char | LIN-Signal CTR_LED_AHV_LIN Signal zum Ansteuern der LEDs am AHV-Taster im Gepäckraum 0 LED Aus  Keine Vorgabe per Diagnose - Ansteuerung durch das AHV Normalbetrieb 1 LED Grün 2 LED Rot 3 Signal ungültig |
| STAT_ST_TRAI_AHV_LIN | unsigned char | LIN-Signal ST_TRAI_AHV_LIN AHM erkennt einen gesteckten Anhängerstecker über eine Strommessung der Lampenstromkreise. Diese Information dient als zusätzliche Bedingung für den Schwenkvorgang der Kugelstange (Plausibilisierung der Anhängererkennung) 0 kein Anhänger erkannt 1 Anhänger erkannt 3 Signal ungültig |
| STAT_CTR_ADMO_AHV_LIN | unsigned char | LIN-Signal CTR_ADMO_AHV_LIN Signal zum Testen des Ein- und Ausschwenkvorgangs 0 keine Aktion  kein Diagnoseeingriff in den Normalbetrieb / keine Änderung einer gestarteten Aktion 1 Einfahren  Einschwenken des Kugelkopfes 2 Ausfahren  Ausschwenken des Kugelkopfes 3 Stopp  Ansteuerung Stopp / gestartete Aktion abbrechen 7 Signal ungültig |
| STAT_ST_CT_BTL_LIN | unsigned char | LIN-Signal ST_CT_BTL_LIN Aktueller Zustand der Heckklappe (HK) 0  HK ist geschlossen 1  HK ist offen 2  HK ist in Vorraste  PL4: Signal unplausibel 3  Signal ungültig |
| STAT_CTR_INIT_AHV_LIN | unsigned char | LIN-Signal CTR_INIT_AHV_LIN Über die AHM Diagnose kann die Initialisierung des AHV-Systems gestartet werden 0 keine Aktion  kein Diagnoseeingriff in den Normalbetrieb / keine Änderung einer gestarteten Aktion 1 Initialisierung starten  Ausschwenken 2 Initialisierung starten  Einschwenken 3 Initialisierung abbrechen  Ansteuerung Stopp / gestartete Aktion abbrechen 7 Signal ungültig |
| STAT_ST_CT_RSCR_LIN | unsigned char | LIN-Signal ST_CT_RSCR_LIN Status der Heckscheibe 0  Heckscheibe ist geschlossen 1  Heckscheibe ist offen 2  Signal unplausibel  Kurzschluss oder offene Leitung an Türkontakt (Hallsensor) 3  Signal ungültig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ahv-endsensoren"></a>
### STATUS_AHV_ENDSENSOREN

Auslesen des Endlagensensors UDS  : $22   ReadDataByIdentifier UDS  : $F5E0 AHV-Endlagensensor(en) Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AHV_ESTP_SENSOR01 | char | Zustand des AHV-Endsensors 01. Siehe Tabelle TAB_AHV_ENDSENSOR "Endanschlag erreicht" bedeutet AHV ausgeschwenkt und verriegelt "Endanschlag nicht erreicht" bedeutet AHV in Zwischenposition ODER eingeschwenkt |
| STAT_AHV_ESTP_SENSOR01_TEXT | string | Zustand des AHV-Endsensors 01. Siehe Tabelle TAB_AHV_ENDSENSOR |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-teilelektrische-ahv"></a>
### STATUS_TEILELEKTRISCHE_AHV

22 0xF050 READ_DATA_DIGITAL_SIGNALS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AHV_KOMU | char | Position der AHV-Stellung  Siehe Tabelle TAB_AHV_KOMU |
| STAT_AHV_KOMU_TEXT | string | Position der AHV-Stellung  Siehe Tabelle TAB_AHV_KOMU |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-inkrementalposition"></a>
### STATUS_INKREMENTALPOSITION

ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Positionszählers (Inkremente) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POSITION_KUPPLUNG | unsigned int | Ist-Position der Kupplung Zählerstand Hallsensor Einheit: Pulse 9000 - 12000 Initialisiert 30000        Teilinitialisiert 50000        Nicht initialisiert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ahv-abschaltstrom"></a>
### STATUS_AHV_ABSCHALTSTROM

ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Motorstrom zum Zeitpunkt der Motorabschaltung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORSTROM_ROH | unsigned int | Rohwert letzter gemessener Motorstrom zum Zeitpunkt der Motorabschaltung |
| STAT_MOTORSTROM_WERT | unsigned int | letzter gemessener Motorstrom zum Zeitpunkt der Motorabschaltung Einheit: mA |
| STAT_MOTORSTROM_EINH | string | mA |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ahv-crc-parameter"></a>
### STATUS_AHV_CRC_PARAMETER

ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Checksumme der Bosal-Parameter auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CRC_BOSAL_PARAMETER | unsigned int | Checksumme der Bosal-Parameter |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ahv-schwenkzaehler"></a>
### STATUS_AHV_SCHWENKZAEHLER

ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Schwenkzähler auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SCHWENKZAEHLER | unsigned int | Zählerstand Schwenkzähler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ahv-peripheriefehler"></a>
### STATUS_AHV_PERIPHERIEFEHLER

ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PERIPHERIEFEHLER_WERT | unsigned int | Fehler-Nummer des Peripheriefehlers Bedeutung Bit 0 = "Fehler Bedientaster 'defekt' oder 'betaetigt bei Startup'" Bit 1 = "Fehler Sicherheitschalter" Bit 2 = "Fehler Mikroschalter Anhänger Erkennung" Bit 3 = "Fehler Relais" Bit 4 = "Hallsensor Versorgung defekt (Schaltzustand ungleich Ist Zustand)" Bit 5 = "Fehler LED" Bit 6 = "Fehler Openload Motor (Unterstrom)" Bit 7 = "Fehler AHV nicht initialisiert" Bit 8 = "Fehler bei Startup Peripherietest Bedientaster festgestellt" Bit 9 = "Fehler bei Startup Peripherietest Sicherheitschalter festgestellt" Bit 10 = "Fehler bei Startup Peripherietest Mikroschalter festgestellt" Bit 11 = "Fehler bei Startup Peripherietest Versorgung Hallsensor festgestellt" Bit 12 = "Fehler bei Startup Peripherietest Signal Hallsensor festgestellt" Bit 13 = "Fehler I2C" Bit 14 = "CRC Fehler im Parameterdatensatz" Bit 15 = "Lowside defekt (Schaltzustand ungleich Ist Zustand)" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ahv-ad-1-2-roh"></a>
### STATUS_AHV_AD_1_2_ROH

ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Rohwerte AD-Wandler-Kanal 1 und 2 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ROHWERT_KANAL1 | unsigned int | Rohwert AD-Wandler Kanal 1 |
| STAT_ROHWERT_KANAL2 | unsigned int | Rohwert AD-Wandler Kanal 2 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ahv-ad-3-4-roh"></a>
### STATUS_AHV_AD_3_4_ROH

ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Rohwerte AD-Wandler-Kanal 3 und 4 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ROHWERT_KANAL3 | unsigned int | Rohwert AD-Wandler Kanal 3 |
| STAT_ROHWERT_KANAL4 | unsigned int | Rohwert AD-Wandler Kanal 4 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ahv-container"></a>
### STATUS_AHV_CONTAINER

ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Container zum Senden beliebiger LIN-Diagnosenachrichten Beispiel 0x7F 0x06 0xB4 0x11 0xFF 0xFF 0xFF 0xFF Werte bei Parametereingabe durch Semikolon trennen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAD | unsigned char | Node-Address |
| PCI | unsigned char | Protocoll Control Information |
| SID | unsigned char | Service-ID |
| DATA_0 | unsigned char | Datenbyte 0 |
| DATA_1 | unsigned char | Datenbyte 1 |
| DATA_2 | unsigned char | Datenbyte 2 |
| DATA_3 | unsigned char | Datenbyte 3 |
| DATA_4 | unsigned char | Datenbyte 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ahv-steuergeraete-reset"></a>
### AHV_STEUERGERAETE_RESET

ReadDataByCommonIdentifier 0x22 0xF502 Diagnosecontainer AHV Reset des AHV2-Steuergerätes

_No arguments._

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
- [LIEFERANTEN](#table-lieferanten) (118 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (132 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (86 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (23 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (5 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [TAB_AHM_LED](#table-tab-ahm-led) (3 × 2)
- [TAB_AHV_POSITIONEN](#table-tab-ahv-positionen) (7 × 2)
- [TAB_AHM_DIGITAL](#table-tab-ahm-digital) (3 × 2)
- [TAB_AHV_VERFAHREN](#table-tab-ahv-verfahren) (4 × 2)
- [TAB_INIT](#table-tab-init) (3 × 2)
- [TAB_AHV_INIT](#table-tab-ahv-init) (5 × 2)
- [TAB_AUSSEN_LICHT_HINTEN](#table-tab-aussen-licht-hinten) (10 × 2)
- [TAB_AHM_INIT](#table-tab-ahm-init) (4 × 2)
- [TAB_STATUS_AHV_INIT](#table-tab-status-ahv-init) (3 × 2)
- [TAB_AHV_ENDSENSOR](#table-tab-ahv-endsensor) (7 × 2)
- [TAB_AHV_KOMU](#table-tab-ahv-komu) (6 × 2)
- [TAB_STAT_PORTPIN](#table-tab-stat-portpin) (3 × 2)
- [TAB_STAT_LED](#table-tab-stat-led) (4 × 2)

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

Dimensions: 118 rows × 2 columns

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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 132 rows × 3 columns

| ORT | ORTTEXT | LIN_2_FORMAT |
| --- | --- | --- |
| 0x0100 | Batteriesensor BSD | - |
| 0x0150 | Ölqualitätsensor BSD | - |
| 0x0200 | Elektrische Wasserpumpe BSD | - |
| 0x0250 | Elektrische Kraftstoffpumpe BSD | - |
| 0x0300 | Generator 1 | - |
| 0x0350 | Generator 2 | - |
| 0x03A0 | Druck- Temperatursensor Tank | 1 |
| 0x03C0 | EAC-Sensor | - |
| 0x0400 | Schaltzentrum Lenksäule | - |
| 0x0500 | DSC Sensor-Cluster | - |
| 0x0600 | Nahbereichsradarsensor links | - |
| 0x0700 | Nahbereichsradarsensor rechts | - |
| 0x0800 | Funkempfänger | - |
| 0x0900 | Elektrische Lenksäulenverriegelung | - |
| 0x0A00 | Regen- Lichtsensor | - |
| 0x290A00 | DSC Hydraulikblock | - |
| 0x0B00 | Nightvision Kamera | - |
| 0x0C00 | TLC Kamera | - |
| 0x0D00 | Spurwechselradarsensor hinten links | - |
| 0x0E00 | Heckklima Bedienteil rechts | 1 |
| 0x0F00 | Rearview Kamera hinten | 1 |
| 0x1000 | Topview Kamera Außenspiegel links | 1 |
| 0x1100 | Topview Kamera Außenspiegel rechts | 1 |
| 0x1200 | Sideview Kamera Stoßfänger vorne links | 1 |
| 0x1300 | Sideview Kamera Stoßfänger vorne rechts | 1 |
| 0x1400 | Wischermotor | 1 |
| 0x1500 | Regen- Lichtsensor | 1 |
| 0x1600 | Innenspiegel | 1 |
| 0x1700 | Garagentoröffner | 1 |
| 0x1800 | AUC-Sensor | 1 |
| 0x1900 | Druck- Temperatursensor | 1 |
| 0x1A20 | Schalterblock Sitzheizung hinten links | 1 |
| 0x1A40 | Schalterblock Sitzheizung hinten rechts | 1 |
| 0x1A60 | Sitzheizung Fahrer | 1 |
| 0x1A80 | Sitzheizung Beifahrer | 1 |
| 0x1AA0 | Sitzheizung Fahrer hinten | 1 |
| 0x1AC0 | Sitzheizung Beifahrer hinten | 1 |
| 0x1B00 | Schalterblock Sitzmemory/-massage Fahrer | 1 |
| 0x1C00 | Schalterblock Sitzmemory/-massage Beifahrer | 1 |
| 0x1C80 | Sitzverstellschalter Beifahrer über Fond | 1 |
| 0x1D00 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x1E00 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x1E40 | Heckklappenemblem | 1 |
| 0x1F00 | KAFAS Kamera | 1 |
| 0x2000 | Automatische Anhängevorrichtung | 1 |
| 0x2100 | SINE | 1 |
| 0x2110 | DWA Mikrowellensensor vorne rechts | 1 |
| 0x2120 | DWA Mikrowellensensor hinten rechts | 1 |
| 0x2130 | DWA Mikrowellensensor hinten links | 1 |
| 0x2140 | DWA Mikrowellensensor vorne links | 1 |
| 0x2150 | DWA Mikrowellensensor hinten | 1 |
| 0x2180 | DWA Ultraschallsensor | 1 |
| 0x2200 | Aussenspiegel Fahrer | - |
| 0x2300 | Aussenspiegel Beifahrer | - |
| 0x2400 | Schaltzentrum Tür | 1 |
| 0x2500 | Schalterblock Sitz Fahrer | 1 |
| 0x2600 | Schalterblock Sitz Beifahrer | 1 |
| 0x2700 | Gurtbringer Fahrer | 1 |
| 0x2800 | Gurtbringer Beifahrer | 1 |
| 0x2900 | Treibermodul Scheinwerfer links | 1 |
| 0x2A00 | Treibermodul Scheinwerfer rechts | 1 |
| 0x2B00 | Bedieneinheit Fahrerassistenzsysteme | 1 |
| 0x2C00 | Bedieneinheit Licht | 1 |
| 0x2D00 | Smart Opener | 1 |
| 0x2E00 | LED-Hauptlicht-Modul links | 1 |
| 0x2F00 | LED-Hauptlicht-Modul rechts | 1 |
| 0x0910 | Elektrische Lenksäulenverriegelung | 1 |
| 0x3200 | Funkempfänger | 1 |
| 0x3300 | Funkempfänger 2 | 1 |
| 0x3400 | Türgriffelektronik Fahrer | - |
| 0x3500 | Türgriffelektronik Beifahrer | - |
| 0x3600 | Türgriffelektronik Fahrer hinten | - |
| 0x3700 | Türgriffelektronik Beifahrer hinten | - |
| 0x3800 | Telestart-Handsender 1 | - |
| 0x3900 | Telestart-Handsender 2 | - |
| 0x3A00 | Fond-Fernbedienung | - |
| 0x3B00 | Elektrische Wasserpumpe | 1 |
| 0x3B10 | Elektrische Wasserpumpe 1 | 1 |
| 0x3B20 | Elektrische Wasserpumpe 2 | 1 |
| 0x3B80 | Elektrische Zusatzwasserpumpe | 1 |
| 0x3C00 | Batteriesensor LIN | - |
| 0x3D00 | Aktives Kühlklappensystem | 1 |
| 0x3E00 | PCU(DCDC) | 1 |
| 0x3F00 | Startergenerator | 1 |
| 0x3F80 | Generator | 1 |
| 0x4000 | Sitzverstellschalter Fahrer | 1 |
| 0x4100 | Sitzverstellschalter Beifahrer | 1 |
| 0x4200 | Sitzverstellschalter Fahrer hinten | 1 |
| 0x4300 | Sitzverstellschalter Beifahrer hinten | 1 |
| 0x4400 | Gepäckraumschalter links | 1 |
| 0x4500 | Gepäckraumschalter rechts | 1 |
| 0x4A00 | Fond-Klimaanlage | 1 |
| 0x4B00 | Elektrischer Klimakompressor | 1 |
| 0x4C00 | Klimabedienteil | 1 |
| 0x4D00 | Gebläseregler | 1 |
| 0x4E00 | Klappenmotor | 0 |
| 0x4F00 | Elektrischer Kältemittelverdichter eKMV | 1 |
| 0x4F80 | Elektrischer Zuheizer PTC | 1 |
| 0x5000 | PMA Sensor links | 1 |
| 0x5100 | PMA Sensor rechts | 1 |
| 0x5200 | CID-Klappe | - |
| 0x5300 | Schaltzentrum Lenksäule | 1 |
| 0x5400 | Multifunktionslenkrad | 1 |
| 0x5500 | Lenkradelektronik | 1 |
| 0x5600 | CID | - |
| 0x5700 | Satellit Upfront links | 0 |
| 0x5708 | Satellit Upfront rechts | 0 |
| 0x5710 | Satellit Tür links | 0 |
| 0x5718 | Satellit Tür rechts | 0 |
| 0x5720 | Satellit B-Säule links X | 0 |
| 0x5728 | Satellit B-Säule rechts X | 0 |
| 0x5730 | Satellit B-Säule links Y | 0 |
| 0x5738 | Satellit B-Säule rechts Y | 0 |
| 0x5740 | Satellit Zentralsensor X | 0 |
| 0x5748 | Satellit Zentralsensor Y | 0 |
| 0x5750 | Satellit Zentralsensor Low g Y | 0 |
| 0x5758 | Satellit Zentralsensor Low g Z | 0 |
| 0x5760 | Satellit Zentralsensor Roll Achse | 0 |
| 0x5768 | Fussgängerschutz Sensor links | 0 |
| 0x5770 | Fussgängerschutz Sensor rechts | 0 |
| 0x5778 | Fussgängerschutz Sensor mitte | 0 |
| 0x5780 | Fussgängerschutzsensor statisch | 0 |
| 0x5788 | Satellit C-Säule links Y | 0 |
| 0x5790 | Satellit C-Säule rechts Y | 0 |
| 0x5798 | Satellit Zentrale Körperschall | 0 |
| 0x57A0 | Kapazitive Insassen- Sensorik CIS | 1 |
| 0x57A8 | Sitzbelegungserkennung Beifahrer SBR | 1 |
| 0x57B0 | Fussgängerschutzsensor dynamisch 1 | 0 |
| 0x57B8 | Fussgängerschutzsensor dynamisch 2 | 0 |
| 0x5800 | HUD | 1 |
| 0x5900 | Audio-Bedienteil | 1 |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

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

Dimensions: 86 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9DFF | AHM Bremslicht: Überlast oder Kurzschluss nach Masse |
| 0x9E00 | AHM Blinklicht links: Überlast oder Kurzschluss nach Masse |
| 0x9E01 | AHM Blinklicht rechts: Überlast oder Kurzschluss nach Masse |
| 0x9E02 | AHM Schlusslicht links:  Überlast oder Kurzschluss nach Masse |
| 0x9E03 | AHM Schlusslicht rechts: Überlast oder Kurzschluss nach Masse |
| 0x9E04 | AHM Rückfahrlicht: Überlast oder Kurzschluss nach Masse |
| 0x9E05 | AHM Nebelschlusslicht: Überlast oder Kurzschluss nach Masse |
| 0x9DEB | AHM Bremslicht: Leuchte defekt oder Leitungsunterbrechung |
| 0x9DEC | AHM Blinklicht links: Leuchte defekt oder Leitungsunterbrechung |
| 0x9DED | AHM Blinklicht rechts: Leuchte defekt oder Leitungsunterbrechung |
| 0x9DEE | AHM Schlusslicht links: Leuchte defekt oder Leitungsunterbrechung |
| 0x9DEF | AHM Schlusslicht rechts: Leuchte defekt oder Leitungsunterbrechung |
| 0x9DF0 | AHM Rückfahrlicht: Leuchte defekt oder Leitungsunterbrechung |
| 0x9DF1 | AHM Nebelschlusslicht: Leuchte defekt oder Leitungsunterbrechung |
| 0x9DF2 | AHM Stop / Turn Light Left: Überlast oder Kurzschluss nach Masse |
| 0x9DF3 | AHM Stop / Turn Light Right: Überlast oder Kurzschluss nach Masse |
| 0x9DF4 | AHM Tail And Licence: Überlast oder Kurzschluss nach Masse |
| 0x9DF5 | AHM Reversing Light: Überlast oder Kurzschluss nach Masse |
| 0x9E06 | AHM Stop / Turn Light Left: Leuchte defekt oder Leitungsunterbrechung |
| 0x9E07 | AHM Stop / Turn Light Right: Leuchte defekt oder Leitungsunterbrechung |
| 0xAAA8 | AHM Tail And Licence: Leuchte defekt oder Leitungsunterbrechung |
| 0xAAA9 | AHM Reversing Light: Leuchte defekt oder Leitungsunterbrechung |
| 0x9DEA | AHM Steuergerätefehler: Treiberfehler / Dauerkurzschluss |
| 0x9DE8 | AHM Steuergerätefehler: Logikfehler / Speicherfehler |
| 0x9DFB | AHM Klemme 30f_a: Spannungsversorgung fehlt / unterbrochen |
| 0x9DFA | AHM Klemme 30f_b: Spannungsversorgung fehlt / unterbrochen |
| 0xAAAA | AHM Klemme 30f_a: Unterspannung &lt; 10,5 Volt |
| 0xAAAB | AHM Klemme 30f_b: Unterspannung &lt; 10,5 Volt |
| 0xAAAC | AHM Klemme 30f_a: Überspannung &gt; 15,5 Volt |
| 0xAAAD | AHM Klemme 30f_b: Überspannung &gt; 15,5 Volt |
| 0xAAAE | AHM Schlusslicht: Abschaltung wegen Unterspannung |
| 0x9DF7 | AHM Hardwaresignal Bremslicht: Leitungsunterbrechung oder Kurzschluss nach Masse |
| 0x9DFC | AHM Hardwaresignal Bremslicht: Leitungsfehler mit Kontakt nach Bordspannung |
| 0x9DF9 | AHM Hardwaresignal Blinklicht: Leitungsunterbrechung oder Kurzschluss nach Masse |
| 0x9DFE | AHM Hardwaresignal Blinklicht: Leitungsfehler mit Kontakt nach Bordspannung |
| 0xAAAF | Coding_Event_Not_Coded |
| 0xAAB0 | AHV: Interner Steuergerätefehler |
| 0xAAB1 | AHV: Unterspannung erkannt |
| 0xAAB2 | AHV: Überspannung erkannt |
| 0xAAB3 | AHV-Hallsensor: Kurzschluss nach Minus oder Unterbrechung |
| 0xAAB4 | AHV-Hallsensor: Kurzschluss nach Plus |
| 0xAAB5 | AHV-Motor: Defekt oder mechanischer Fehler |
| 0xAAB6 | AHV-Motor: Leitungsunterbrechung |
| 0xAAB7 | AHV-Motor: Kurzschluss nach Minus |
| 0xAAB8 | AHV-Motor: Kurzschluss nach Plus |
| 0xAAB9 | AHV-Motor: Überstromabschaltung |
| 0xAABA | AHV-Motor: Offsetstromgrenze erreicht |
| 0xAABB | AHV: Nachspannen fehlgeschlagen |
| 0xAABC | AHV: Lösen fehlgeschlagen |
| 0xAABD | AHV: Nicht initialisiert |
| 0xAABE | Mikroschalter-Steckdose: Leitungsunterbrechung oder Kurzschluss |
| 0x9DF6 | AHV: Zwischenposition erkannt |
| 0x9DF8 | AHV-Schnittstelle: Leitungsunterbrechung oder Kurzschluss nach Masse |
| 0x9DFD | AHV-Schnittstelle: Leitungsfehler mit Kontakt nach Bordspannung |
| 0xE54B | Kommunikationsfehler LIN |
| 0xAABF | AHV: CRC_Berechnung fehlgeschlagen |
| 0xAAC0 | AHV: v &gt; 0 km/h bei Diagnosesteuerung AHV-Motor |
| 0xAAC1 | AHV-Taster: Defekt oder Leitungsfehler mit Kurzschluss nach Minus |
| 0xAAC2 | AHV-Endsensor 1: Leitungsunterbrechung |
| 0xAAC3 | AHV-Endsensor 1: Kurzschluss nach Plus |
| 0xAAC4 | AHV-Endsensor 1: Kurzschluss nach Minus |
| 0xAAC5 | AHV-Endsensor 2: Leitungsunterbrechung |
| 0xAAC6 | AHV-Endsensor 2: Kurzschluss nach Plus |
| 0xAAC7 | AHV-Endsensor 2: Kurzschluss nach Minus |
| 0xE544 | K-CAN Bus: Defekt erkannt |
| 0xE547 | K-CAN: Control Module Bus OFF |
| 0xE548 | LIN-Bus: AHV antwortet nicht |
| 0xE554 | Nachricht Blinken (0x1F6): Ausfall |
| 0xE555 | Nachricht Motordaten (0x1D0): Ausfall |
| 0xE556 | Nachricht Geschwindigkeit K-CAN (0x1A0): Ausfall |
| 0xE557 | Nachricht Kilometerstand/Reichweite (0x330): Ausfall |
| 0xE558 | Nachricht Klemmenstatus (0x130): Ausfall |
| 0xE559 | Nachricht Lampenzustand (0x21A): Ausfall |
| 0xE55A | Nachricht Nachlaufzeit Stromversorgung (0x3BE): Ausfall |
| 0xE55B | Nachricht  Powermanagement Verbrauchersteuerung (0x3B3): Ausfall |
| 0xE55C | Nachricht Status DSC K-CAN (0x19E): Ausfall |
| 0xE55D | Nachricht Status Zentralverriegelung HK (0x0F2): Ausfall |
| 0xAAC8 | AHM hat ungültiges CAN-Signal weitergeleitet: Status_Klemme_15 |
| 0xAAC9 | AHM hat ungültiges CAN-Signal weitergeleitet: Status_Klemme_50 |
| 0xAACA | AHM hat ungültiges CAN-Signal weitergeleitet: Status_Kontakt_Heckklappe |
| 0xAACB | AHM hat ungültiges CAN-Signal weitergeleitet: Status_Kontakt_Heckscheibe |
| 0xAACC | AHM hat ungültiges CAN-Signal weitergeleitet: Alive_Geschwindigkeit |
| 0xAACD | AHM hat ungültiges CAN-Signal weitergeleitet: Geschwindigkeit_Fahrzeug |
| 0xAACE | AHM hat ungültiges CAN-Signal weitergeleitet: Fahrzustand Fahrzeug |
| 0x9DE9 | Energiesparmode aktiv |
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

Dimensions: 23 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9DFF | 1 | 2 | 3 | 5 |
| 0x9E00 | 1 | 2 | 4 | 5 |
| 0x9E01 | 1 | 2 | 3 | 5 |
| 0x9E02 | 1 | 2 | 4 | 5 |
| 0x9E03 | 1 | 2 | 3 | 5 |
| 0x9E04 | 1 | 2 | 4 | 5 |
| 0x9E05 | 1 | 2 | 4 | 5 |
| 0x9DEB | 1 | 2 | 3 | 5 |
| 0x9DEC | 1 | 2 | 4 | 5 |
| 0x9DED | 1 | 2 | 3 | 5 |
| 0x9DEE | 1 | 2 | 4 | 5 |
| 0x9DEF | 1 | 2 | 3 | 5 |
| 0x9DF0 | 1 | 2 | 4 | 5 |
| 0x9DF1 | 1 | 2 | 4 | 5 |
| 0x9DF2 | 1 | 2 | 4 | 5 |
| 0x9DF3 | 1 | 2 | 3 | 5 |
| 0x9DF4 | 1 | 2 | 3 | 5 |
| 0x9DF5 | 1 | 2 | 3 | 5 |
| 0x9E06 | 1 | 2 | 4 | 5 |
| 0x9E07 | 1 | 2 | 3 | 5 |
| 0xAAA8 | 1 | 2 | 3 | 5 |
| 0xAAA9 | 1 | 2 | 3 | 5 |
| 0xFFFF | - | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Erkannte Lasten | - | - | unsigned char | - | 1 | 1 | 0 |
| 2 | Zustand Lastüberwachung | - | - | unsigned char | - | 1 | 1 | 0 |
| 3 | Versorgungsspannung KL30f_a | V | - | unsigned char | - | 139 | 1989 | 0 |
| 4 | Versorgungsspannung KL30f_b | V | - | unsigned char | - | 139 | 1989 | 0 |
| 5 | initialer widerstandsproportionaler Wert | - | - | unsigned int | - | 1 | 1 | 0 |

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

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 2 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | kein Betriebsmode gesetzt | kein Betriebsmode |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-tab-ahm-led"></a>
### TAB_AHM_LED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | Ansteuerung GRÜN |
| 0x02 | Ansteuerung ROT |

<a id="table-tab-ahv-positionen"></a>
### TAB_AHV_POSITIONEN

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Arbeitsposition |
| 0x01 | Ruheposition |
| 0x02 | Zwischenposition |
| 0x03 | Arbeitsposition (keine Nachtaktung) |
| 0x04 | Mechanik schwenkt ein |
| 0x05 | Mechanik schwenkt aus |
| 0xFF | unbekannte Position |

<a id="table-tab-ahm-digital"></a>
### TAB_AHM_DIGITAL

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | blinkt |
| 0x02 | EIN |

<a id="table-tab-ahv-verfahren"></a>
### TAB_AHV_VERFAHREN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Änderung |
| 0x01 | Ansteuerung Richtung Ruheposition |
| 0x02 | Ansteuerung Richtung Arbeitsposition |
| 0x03 | Ansteuerung abbrechen |

<a id="table-tab-init"></a>
### TAB_INIT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht initialisiert |
| 0x01 | Initialisierung in Ordnung |
| 0xFF | Initialisierung nicht in Ordnung |

<a id="table-tab-ahv-init"></a>
### TAB_AHV_INIT

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AHV-Motor gestartet |
| 0x01 | AHV-Motor nicht gestartet: CRC-Fehler |
| 0x02 | AHV-Motor nicht gestartet: Fahrzeuggeschwindigkeit &gt; 0 km/h |
| 0x03 | AHV-Motor nicht gestartet: AHV LIN-Signal ungültig |
| 0xFF | unbekannter Status |

<a id="table-tab-aussen-licht-hinten"></a>
### TAB_AUSSEN_LICHT_HINTEN

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | Bremslicht |
| 0x02 | Blinklicht rechts |
| 0x03 | Blinklicht links |
| 0x04 | Warnblinken |
| 0x05 | Schlusslicht |
| 0x06 | Rückfahrlicht |
| 0x07 | Parklicht rechts |
| 0x08 | Parklicht links |
| 0x09 | Nebelschlusslicht |

<a id="table-tab-ahm-init"></a>
### TAB_AHM_INIT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine Aktion |
| 0x01 | AUSSCHWENKEN |
| 0x02 | EINSCHWENKEN |
| 0x03 | Initialisierung abbrechen |

<a id="table-tab-status-ahv-init"></a>
### TAB_STATUS_AHV_INIT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Init nicht angefordert oder abgeschlossen |
| 0x01 | Init in Abarbeitung |
| 0xFF | Status nicht gefunden |

<a id="table-tab-ahv-endsensor"></a>
### TAB_AHV_ENDSENSOR

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Fehler |
| 0x01 | Leitungsunterbrechung |
| 0x02 | Kurzschluss nach Plus |
| 0x03 | Kurzschluss nach Minus |
| 0x04 | Endanschlag erreicht |
| 0x05 | Endanschlag nicht erreicht |
| 0x07 | Signal ungültig oder Sensor nicht verbaut |

<a id="table-tab-ahv-komu"></a>
### TAB_AHV_KOMU

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Signal nicht bewertet (Kl. 15 AUS oder Funktion nicht aktiv kodiert) |
| 0x01 | AHV verriegelt |
| 0x02 | AHV nicht verriegelt |
| 0x03 | kein Signal oder Kurzschluss nach Minus (nur bei Kl. 15 EIN) |
| 0x04 | Kurzschluss nach Plus (nur bei Kl. 15 AUS) |
| 0xff | Signalwert ungültig |

<a id="table-tab-stat-portpin"></a>
### TAB_STAT_PORTPIN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Portpin hat LOW-Pegel |
| 0x01 | Portpin hat HIGH-Pegel |
| 0xFF | Status unbekannt |

<a id="table-tab-stat-led"></a>
### TAB_STAT_LED

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | LED o.k. |
| 0x7D | Kurzschluss GND |
| 0x7E | Kurzschluss KL30 |
| 0xFF | Status unbekannt |
