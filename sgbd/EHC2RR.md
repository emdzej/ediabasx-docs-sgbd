# EHC2RR.prg

- Jobs: [97](#jobs)
- Tables: [29](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EHC2RR  |
| ORIGIN | BMW TI-432 Siegfried Helmich |
| REVISION | 1.003 |
| AUTHOR | BMW EF-63 Tobias Schmid, Bertrandt EF-63 Ulrich Strobl |
| COMMENT | Steuergraetebeschreibungsdatei fuer 2-Achs-Luftfeder-SG RR01  |
| PACKAGE | 1.30 |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
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
- [FLASH_PARAMETER_SETZEN](#job-flash-parameter-setzen) - Setzt die SG-spezifischen Flash-Parameter
- [FLASH_PARAMETER_LESEN](#job-flash-parameter-lesen) - Gibt die SG-spezifischen Flash-Parameter zurück
- [READ_BOOT_IDENT](#job-read-boot-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [READ_ANALOG_VALUES](#job-read-analog-values) - Lesen physikalischen Analogwerte der Sensoren
- [READ_DIG_IN](#job-read-dig-in) - Lesen Digitale Eingangssignale
- [READ_LED_STAT](#job-read-led-stat) - Lesen Satus LEDs
- [SET_REGULATOR_STAT](#job-set-regulator-stat) - Schreiben regulator modes
- [READ_AKTOREN_STAT](#job-read-aktoren-stat) - Lesen actuator modes
- [READ_REGULATOR_MODE](#job-read-regulator-mode) - Lesen regulator modi
- [READ_COD_COTOOL](#job-read-cod-cotool) - EEPROM Daten lesen
- [WRITE_COD_COTOOL](#job-write-cod-cotool) - EEPROM Daten schreiben
- [DUMMY_IDENT](#job-dummy-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [READ_CALIBRATION](#job-read-calibration) - Hoehenstand lesen
- [CALIBRATE_VEHICLE_HEIGHT](#job-calibrate-vehicle-height) - automatischer Hoehenabgleich
- [WRITE_HEIGHT_COUNTS](#job-write-height-counts) - Fahrzeughöhe in Counts vorgeben
- [READ_ANALOG_VOLTAGE](#job-read-analog-voltage) - Lesen physikalischen Analogwerte der Sensoren
- [STATUS_BOOT_IDENT](#job-status-boot-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [STEUERN_ACTUATORS](#job-steuern-actuators) - Aktuatoren setzen/ ruecksetzen Check the Pneumatic layout before acivating valves System can be damaged !
- [STEUERN_LEDS](#job-steuern-leds) - LEDs setzen/ ruecksetzen
- [STEUERN_VALVE_SW_LSS](#job-steuern-valve-sw-lss) - set valve switches LSS (Low Side Switch) in full access
- [STEUERN_VALVE_SW_HSS](#job-steuern-valve-sw-hss) - set valve switches HSS (High SIde Switch) in full access
- [STATUS_ANALOG_VALUES](#job-status-analog-values) - Lesen physikalischen Analogwerte der Sensoren
- [STATUS_DIG_IN](#job-status-dig-in) - Lesen Digitale Eingangssignale
- [STATUS_LED_STAT](#job-status-led-stat) - Lesen Satus LEDs
- [STEUERN_REGULATOR](#job-steuern-regulator) - Schreiben regulator modes
- [STATUS_AKTOREN](#job-status-aktoren) - Lesen actuator modes
- [STATUS_REGULATOR_MODE](#job-status-regulator-mode) - Lesen regulator modi
- [STATUS_CALIBRATION](#job-status-calibration) - Hoehenstand lesen
- [STATUS_ECU](#job-status-ecu) - Steuergerätestatus einstellen
- [STATUS_INTERNAL_STATUS](#job-status-internal-status) - Auslesen von internen Reglerinformationen
- [STEUERN_MEMORY_DEFAULT](#job-steuern-memory-default) - Copy default memory from FLASH to EEPROM
- [STATUS_ANALOG_VOLTAGE](#job-status-analog-voltage) - Lesen physikalischen Analogwerte der Sensoren
- [STEUERN_ACTUATORS_TIME](#job-steuern-actuators-time) - Aktuatoren bestimmte Zeit setzen/ ruecksetzen
- [STATUS_DELTA_OFFROAD](#job-status-delta-offroad) - Ausgabe Delta Offroad aus Codierdaten
- [STEUERN_ECU](#job-steuern-ecu) - Steuergerätestatus einstellen
- [SET_ACTUATORS](#job-set-actuators) - Aktuatoren setzen/ ruecksetzen Check the Pneumatic layout before acivating valves System can be damaged !
- [SET_LEDS](#job-set-leds) - LEDs setzen/ ruecksetzen
- [SET_VALVE_SW_LSS](#job-set-valve-sw-lss) - set valve switches LSS (Low Side Switch) in full access
- [SET_VALVE_SW_HSS](#job-set-valve-sw-hss) - set valve switches HSS (High SIde Switch) in full access
- [SET_ECU_STATUS](#job-set-ecu-status) - Steuergerätestatus einstellen
- [READ_ECU_STATUS](#job-read-ecu-status) - Steuergerätestatus einstellen
- [READ_INTERNAL_STATUS](#job-read-internal-status) - Auslesen von internen Reglerinformationen
- [SET_MEMORY_DEFAULT](#job-set-memory-default) - Copy default memory from FLASH to EEPROM
- [SET_ACTUATORS_TIME](#job-set-actuators-time) - Aktuatoren bestimmte Zeit setzen/ ruecksetzen
- [STEUERN_ECU_STATUS](#job-steuern-ecu-status) - Steuergerätestatus einstellen

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

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

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

<a id="job-flash-parameter-setzen"></a>
### FLASH_PARAMETER_SETZEN

Setzt die SG-spezifischen Flash-Parameter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ADRESSE | int | Steuergeräteadresse |
| SG_MAXANZAHL_AIF | int | Anzahl der Anwender-Infofelder 0x00  Nicht zulässig sonst Anzahl der AIF |
| SG_GROESSE_AIF | int | Grösse des Anwender-Infofeldes 0x12  18 dez kleines AIF 0x33  51 dez grosses AIF 0x40  64 dez grosses AIF ( gilt nur für Power-Pc ) sonst Nicht zulässig |
| SG_ENDEKENNUNG_AIF | int | Offset für letztes Anwender-Infofeld 0xFE  Letztes AIF nicht überschreibbar 0x01  Letztes AIF ist überschreibbar sonst Nicht zulässig |
| SG_AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTH_TEXT |
| DIAG_PROT | string | optionaler Parameter Diagnoseprotokoll table KONZEPT_TABELLE KONZEPT_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

<a id="job-flash-parameter-lesen"></a>
### FLASH_PARAMETER_LESEN

Gibt die SG-spezifischen Flash-Parameter zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_DIAG_PROT oder ERROR_SG_AUTHENTISIERUNG |
| SG_ADRESSE | int | Steuergeräteadresse |
| SG_MAXANZAHL_AIF | int | Anzahl der Anwender-Infofelder |
| SG_GROESSE_AIF | int | Grösse des Anwender-Infofeldes |
| SG_ENDEKENNUNG_AIF | int | Offset für letztes Anwender-Infofeld |
| SG_AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTH_TEXT |
| DIAG_PROT_IST | string | Gibt das aktuelle gewählte Protokoll aus table KONZEPT_TABELLE KONZEPT_TEXT |

<a id="job-read-boot-ident"></a>
### READ_BOOT_IDENT

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BOOT_NR | string | Boot Loader version - 4 bytes - first 3 are relevant |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-analog-values"></a>
### READ_ANALOG_VALUES

Lesen physikalischen Analogwerte der Sensoren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| H_FL | int | Höhe VL [mm] |
| H_FR | int | Höhe VR [mm] |
| H_RL | int | Höhe HL [mm] |
| H_RR | int | Höhe HR [mm] |
| P_RES | real | Speicherdruck [bar] |
| T_COMP | int | Kompressortemperatur [°C] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-read-dig-in"></a>
### READ_DIG_IN

Lesen Digitale Eingangssignale

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SWITCH_UP_EIN | int | Tasterwippe rauf [High Aktiv] Digitale Eingangssignale Bit0: SWITCH_ACCESS, Bit1: SWITCH_UP, Bit2: SWITCH_DOWN, Bit3: SWITCH_HOLD Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: STATUS_VA |
| STAT_SWITCH_DOWN_EIN | int | Tasterwippe runter [High Aktiv] |
| STAT_VA_EIN | int | VA (CAN tranceiver inhibit pin) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-read-led-stat"></a>
### READ_LED_STAT

Lesen Satus LEDs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STANDARD_STATIC | int | Standard height |
| STAT_OFFROAD_STATIC | int | offroad height |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-set-regulator-stat"></a>
### SET_REGULATOR_STAT

Schreiben regulator modes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NIVEAU | string | Aktuatoren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-read-aktoren-stat"></a>
### READ_AKTOREN_STAT

Lesen actuator modes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MV_FR | int | Status Regulator |
| STAT_MV_FL | int | Status Regulator |
| STAT_MV_RR | int | Status Regulator |
| STAT_MV_RL | int | Status Regulator Rear Left |
| STAT_MV_RES | int | Status Regulator Reservoir |
| STAT_MV_EX | int | Status Regulator |
| STAT_C_SW | int | Status Regulator |
| STAT_MV_HPEX | int | Status Regulator |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-read-regulator-mode"></a>
### READ_REGULATOR_MODE

Lesen regulator modi

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STANDARD_NIVEAU_EIN | int | Standard height |
| STAT_OFFROAD_NIVEAU_EIN | int | offroad height |
| STAT_REGELUNG_DOWN_EIN | int | Status Regulator |
| STAT_REGELUNG_UP_EIN | int | Status Regulator |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-read-cod-cotool"></a>
### READ_COD_COTOOL

EEPROM Daten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOEHNERT_HEADER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| EEPROM_DATEN_ERROR | binary | Hex Auftrag an SG |

<a id="job-write-cod-cotool"></a>
### WRITE_COD_COTOOL

EEPROM Daten schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOEHNERT_HEADER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| EEPROM_DATEN | binary | Codierdaten |
| EEPROM_DATEN_ERROR | binary | Hex Auftrag an SG |
| TEST1 | binary |  |
| TEST2 | binary |  |

<a id="job-dummy-ident"></a>
### DUMMY_IDENT

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

<a id="job-read-calibration"></a>
### READ_CALIBRATION

Hoehenstand lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| EE_H_FL_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_FR_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_RL_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_RR_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_ZERO_EINH | string | Einheit fuer Nullabgleich [in AD-Counts] |
| EE_H_FR_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_FL_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_RR_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_RL_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_LEAK_EINH | string | Einheit fuer Hoehenstand zur Grobleckagepruefung [mm] |
| _TEL_ANTWORT | binary |  |

<a id="job-calibrate-vehicle-height"></a>
### CALIBRATE_VEHICLE_HEIGHT

automatischer Hoehenabgleich

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DELTA_HOEHE_LINKS | int | mm |
| DELTA_HOEHE_RECHTS | int | mm |
| ACHSE | int | 1 Vorne und 2 Hinten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| OFFSET_LINKS_ALT | int | alter offset |
| OFFSET_RECHTS_ALT | int | alter offset |
| OFFSET_LINKS_NEU | int | alter offset |
| OFFSET_RECHTS_NEU | int | alter offset |
| SG_HOEHE_LINKS | int | aktuelle Fahrzeughoehe laut Fastfilter |
| SG_HOEHE_RECHTS | int | aktuelle Fahrzeughoehe laut Fastfilter |
| AUFLOESUNG_LINKS_WERT | real | Sensoraufloesung links laut Kodierdaten |
| AUFLOESUNG_RECHTS_WERT | real | Sensoraufloesung rechts laut Kodierdaten |
| ABWEICHUNG_LINKS_WERT | int | Abweichung links |
| ABWEICHUNG_RECHTS_WERT | int | Abweichung rechts |
| _TEL_SEND | binary | gesendetes Telegramm |
| _TEL_ANTWORT | binary | empfangenes Telegramm |

<a id="job-write-height-counts"></a>
### WRITE_HEIGHT_COUNTS

Fahrzeughöhe in Counts vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OFFSET_V_LINKS | int | counts |
| OFFSET_V_RECHTS | int | counts |
| OFFSET_H_LINKS | int | counts |
| OFFSET_H_RECHTS | int | counts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_SEND | binary | gesendetes Telegramm |

<a id="job-read-analog-voltage"></a>
### READ_ANALOG_VOLTAGE

Lesen physikalischen Analogwerte der Sensoren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| V_FL | real | Spannung VL [V] |
| V_FR | real | Spannung  [V] |
| V_VA | real | Transceiver inhibit voltage [V] |
| V_RL | real | Spannung  [V] |
| V_RR | real | Spannung  [V] |
| V_KL_30 | real | Spannung  [V] |
| V_COMP | real | Spannung compressor  [V] |
| V_RES | real | Spannung Reservoir [V] |
| V_STAB | real | Spannung  [V] |
| V_SENS1 | real | Spannung  [V] |
| V_SENS2 | real | Spannung  [V] |
| V_SENS3 | real | Spannung  [V] |
| V_12V | real | Spannung  [V] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-status-boot-ident"></a>
### STATUS_BOOT_IDENT

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BOOT_NR | string | Boot Loader version - 4 bytes - first 3 are relevant |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-actuators"></a>
### STEUERN_ACTUATORS

Aktuatoren setzen/ ruecksetzen Check the Pneumatic layout before acivating valves System can be damaged !

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACTUATORS1 | int | Aktuatoren Bit0: MV_FR, Bit1: MV_FL, Bit2: MV_RR, Bit3: MV_RL Bit4: MV_RES, Bit5: MV_EX, Bit6: C_SW, Bit7: reserved MV_FR  = Magnetventil Front Right MV_FL  = Magnetventil Front Left MV_RR  = Magnetventil Rear Right MV_RL  = Magnetventil Rear left MV_RES = Reservoir Valve MV_EX  = Exhaust Valve C_SW   = Compressor Switch |
| ACTUATORS2 | int | Aktuatoren Bit0: MV_HPEX, Bit1: reserved, Bit2: reserved, Bit3: reserved Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved MV_HPEX = Magnetventil High pressure Exhaust Valve |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-steuern-leds"></a>
### STEUERN_LEDS

LEDs setzen/ ruecksetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LEDS1 | int | LEDs Bit0: reserved Bit1: standard Bit2: reserved, Bit3: reserved,Bit4: reserved, Bit5: reserved, Bit6: reserved Bit7: offroad |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-steuern-valve-sw-lss"></a>
### STEUERN_VALVE_SW_LSS

set valve switches LSS (Low Side Switch) in full access

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALVE_SW1 | int | valve switches Bit0: MV_FR, Bit1: MV_FL, Bit2: MV_RR, Bit3: MV_RL Bit4: MV_RES, Bit5: MV_EX, Bit6: C_SW, Bit7: reserved MV_FR  = Magnetventil Front Right MV_FL  = Magnetventil Front Left MV_RR  = Magnetventil Rear Right MV_RL  = Magnetventil Rear left MV_RES = Reservoir Valve MV_EX  = Exhaust Valve C_SW   = Compressor Switch |
| VALVE_SW2 | int | valve switches Bit0: MV_HPEX, Bit1: reserved, Bit2: reserved, Bit3: reserved Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved MV_HPEX = Magnetventil High pressure Exhaust Valve |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-steuern-valve-sw-hss"></a>
### STEUERN_VALVE_SW_HSS

set valve switches HSS (High SIde Switch) in full access

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALVE_SW1 | int | valve switches Bit0: HSS_FRONT, Bit1: HSS_REAR, Bit2: HSS_RES, Bit3: PWR_UPULL Bit4: PWR_SENS1, Bit5: PWR_SENS2, Bit6: PWR_SENS3, Bit7: reserved HSS_FRONT  = Front valves common switch HSS_REAR   = Rear valves common switch HSS_RES    = High Side Switch - Reservoir PWR_UPULL  = PWR_SENS1  = PWR_SENS2  = PWR_SENS3  = |
| VALVE_SW2 | int | valve switches Bit0: reserved, Bit1: reserved, Bit2: reserved, Bit3: reserved Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-status-analog-values"></a>
### STATUS_ANALOG_VALUES

Lesen physikalischen Analogwerte der Sensoren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_H_FL | int | Höhe VL [mm] |
| STAT_H_FR | int | Höhe VR [mm] |
| STAT_H_RL | int | Höhe HL [mm] |
| STAT_H_RR | int | Höhe HR [mm] |
| STAT_P_RES | real | Speicherdruck [bar] |
| STAT_T_COMP | int | Kompressortemperatur [°C] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-status-dig-in"></a>
### STATUS_DIG_IN

Lesen Digitale Eingangssignale

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SWITCH_UP_EIN | int | Tasterwippe rauf [High Aktiv] Digitale Eingangssignale Bit0: SWITCH_ACCESS, Bit1: SWITCH_UP, Bit2: SWITCH_DOWN, Bit3: SWITCH_HOLD Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: STATUS_VA |
| STAT_SWITCH_DOWN_EIN | int | Tasterwippe runter [High Aktiv] |
| STAT_VA_EIN | int | VA (CAN tranceiver inhibit pin) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-status-led-stat"></a>
### STATUS_LED_STAT

Lesen Satus LEDs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STANDARD_STATIC | int | Standard height |
| STAT_OFFROAD_STATIC | int | offroad height |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-steuern-regulator"></a>
### STEUERN_REGULATOR

Schreiben regulator modes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NIVEAU | string | Aktuatoren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-status-aktoren"></a>
### STATUS_AKTOREN

Lesen actuator modes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MV_FR | int | Status Regulator |
| STAT_MV_FL | int | Status Regulator |
| STAT_MV_RR | int | Status Regulator |
| STAT_MV_RL | int | Status Regulator Rear Left |
| STAT_MV_RES | int | Status Regulator Reservoir |
| STAT_MV_EX | int | Status Regulator |
| STAT_C_SW | int | Status Regulator |
| STAT_MV_HPEX | int | Status Regulator |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-status-regulator-mode"></a>
### STATUS_REGULATOR_MODE

Lesen regulator modi

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STANDARD_NIVEAU_EIN | int | Standard height |
| STAT_OFFROAD_NIVEAU_EIN | int | offroad height |
| STAT_REGELUNG_DOWN_EIN | int | Status Regulator |
| STAT_REGELUNG_UP_EIN | int | Status Regulator |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-status-calibration"></a>
### STATUS_CALIBRATION

Hoehenstand lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| EE_H_FL_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_FR_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_RL_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_RR_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_ZERO_EINH | string | Einheit fuer Nullabgleich [in AD-Counts] |
| EE_H_FR_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_FL_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_RR_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_RL_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_LEAK_EINH | string | Einheit fuer Hoehenstand zur Grobleckagepruefung [mm] |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-ecu"></a>
### STATUS_ECU

Steuergerätestatus einstellen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |
| STAT_DUMP_MODUS_EIN | int | Zusatzbotschaften fuer FESTUS [High Aktiv] MODUS 1 |
| STAT_BAND_MODUS_EIN | int | Aktivierungs-Sperre [High Aktiv] MODUS 1 |
| STAT_VERLADE_MODUS_EIN | int | Einstellungen fuer den Transport [High Aktiv] MODUS 1 |
| STAT_LOWTOL_MODUS_EIN | int | Aktiviert sehr enge Toleranzen MODUS 1 |
| STAT_EMV_KUNDEN_MODUS_EIN | int | fuer webaco EMV-Tests [High Aktiv] MODUS 1 |
| STAT_HANDSTEUER_MODUS_EIN | int | Freischaltung fuer I/O Status-Vorgabe [High Aktiv] MODUS 1 |
| STAT_NOPLAU_MODUS_EIN | int | fuer Laborauto Tests [High Aktiv] MODUS 1 |
| STAT_NOUSER_MODUS_EIN | int | SG reagiert nicht mehr auf Benutzeranforderungen MODUS 1 |
| STAT_ZYKEMV_MODUS_EIN | int | Modus um im EMV Test zyklische Ventilansteuerungen zu haben MODUS 2 |
| STAT_TESTMODUS_EIN | int | Modus um Lebensdauertests, etc. durchzufuehren MODUS 2 |
| STAT_NOPREVENTMODUS_EIN | int | Modus um Regelungsverhinderer zu deaktivieren MODUS 2 |
| STATUS1 | int | Status Seuergeraet (Modus) Bit0: Dump Modus, Bit1: Band Modus, Bit2: Verlademodus, Bit3: Lowtolmodus Bit4: EMV Kundenmodus, Bit5: Handsteuermodus, Bit6: Noplausmodus, Bit7: Nousermodus |
| STATUS2 | int | Status Seuergeraet (Modus) Bit0:  CYCLIC EMC , Bit1: reserved, Bit2: reserved, Bit3: reserved Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved |

<a id="job-status-internal-status"></a>
### STATUS_INTERNAL_STATUS

Auslesen von internen Reglerinformationen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PREVENT_CURVE | int | Regelungsverhinderer Kurve Aktiv |
| PREVENT_ACCEL | int | Regelungsverhinderer Laengsbeschleunigung Aktiv |
| PREVENT_PLAUS | int | Regelungsverhinderer Plausibilitaet Aktiv |
| PREVENT_CARLIFT | int | Regelungsverhinderer Wagenheber Aktiv |
| PREVENT_DOOR | int | Regelungsverhinderer Tuer Aktiv |
| PREVENT_ARTIC | int | Regelungsverhinderer Verschraenkung Aktiv |
| PREVENT_VALVE | int | Regelungsverhinderer Ventil ED Aktiv |
| PREVENT_BRAKES | int | Regelungsverhinderer Bremse Aktiv |
| PREVENT_USER | int | Regelungsverhinderer unterbrochenes Absenken Aktiv |
| CAN_V_CAR | int | Empfangsstatus Fahrzeuggeschwindigkeit |
| CAN_ABS | int | Empfangsstatus DSC Aktivitaet |
| CAN_N_MOT | int | Empfangsstatus Motordrehzahl |
| CAN_KM | int | Empfangsstatus Kilometerstand |
| CAN_A_Q | int | Empfangsstatus Querbeschleunigung |
| CAN_BAS_FBR | int | Empfangsstatus Fahrerbremsung |
| CAN_S_ANH | int | Empfangsstatus Anhaenger |
| CAN_S_TNS | int | Empfangsstatus Tag/Nachtumschaltung |
| CAN_S_HBR | int | Empfangsstatus Handbremse |
| CAN_L_ASC_DEF | int | Empfangsstatus Fehlerstatus DSC |
| GMMNGR_OPMODE | int | Global Modemanager Opmode |
| REG_SLOW | int | Slowfilter aktiv |
| REG_NORMTOL | int | Normales Toleranzband aktiv |
| REG_EXTTOL | int | Erweitertes Toleranzband aktiv |
| REG_LOWTOL | int | Enges Toleranzband aktiv |
| REG_WUPTOL | int | Wakeup Toleranzband aktiv |
| REG_KERB | int | Randsteinerkennung aktiv |
| REG_OTEMP_FILL | int | Randsteinerkennung aktiv |
| REG_OTEMP_REG | int | Randsteinerkennung aktiv |
| UNDERVOLTAGE | int | Unterspannung aktiv |
| OVERVOLTAGE | int | Ueberspannung aktiv |
| XXXSTATEFR | int | Zustand des Reglerblocks Vorderachse |
| XXXSTATERR | int | Zustand des Reglerblocks hinten rechts |
| XXXSTATERL | int | Zustand des Reglerblocks hinten links |
| VLVCTRL_STATE | int | Zustand des ValveCtrl Blocks |
| ACTUATOR_BA_WARN | int | actuator_ba_warn Variable |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |
| _TEL_SEND | binary | Interner Reglerstatus |

<a id="job-steuern-memory-default"></a>
### STEUERN_MEMORY_DEFAULT

Copy default memory from FLASH to EEPROM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary |  |

<a id="job-status-analog-voltage"></a>
### STATUS_ANALOG_VOLTAGE

Lesen physikalischen Analogwerte der Sensoren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_V_FL | real | Spannung VL [V] |
| STAT_V_FR | real | Spannung  [V] |
| STAT_V_VA | real | Transceiver inhibit voltage [V] |
| STAT_V_RL | real | Spannung  [V] |
| STAT_V_RR | real | Spannung  [V] |
| STAT_V_KL_30 | real | Spannung  [V] |
| STAT_V_COMP | real | Spannung compressor  [V] |
| STAT_V_RES | real | Spannung Reservoir [V] |
| STAT_V_STAB | real | Spannung  [V] |
| STAT_V_SENS1 | real | Spannung  [V] |
| STAT_V_SENS2 | real | Spannung  [V] |
| STAT_V_SENS3 | real | Spannung  [V] |
| STAT_V_12V | real | Spannung  [V] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-steuern-actuators-time"></a>
### STEUERN_ACTUATORS_TIME

Aktuatoren bestimmte Zeit setzen/ ruecksetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACTUATORS1 | int | Aktuatoren Bit0: MV_FR, Bit1: MV_FL, Bit2: MV_RR, Bit3: MV_RL Bit4: MV_RES, Bit5: MV_EX, Bit6: C_SW, Bit7: reserved MV_FR  = Magnetventil Front Right MV_FL  = Magnetventil Front Left MV_RR  = Magnetventil Rear Right MV_RL  = Magnetventil Rear left MV_RES = Reservoir Valve MV_EX  = Exhaust Valve C_SW   = Compressor Switch |
| ACTUATORS2 | int | Aktuatoren Bit0: MV_HPEX, Bit1: reserved, Bit2: reserved, Bit3: reserved Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved MV_HPEX   = High pressure exhaust |
| TIME | int | Zeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-status-delta-offroad"></a>
### STATUS_DELTA_OFFROAD

Ausgabe Delta Offroad aus Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_DELTA_OFFROAD_WERT | int | Offroad Delta |
| _TEL_ANTWORT | binary | empfangenes Telegramm |

<a id="job-steuern-ecu"></a>
### STEUERN_ECU

Steuergerätestatus einstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STATUS1 | int | Status Steuergeraet (Modus) Bit0: Dump Modus, Bit1: Band Modus, Bit2: Verlademodus, Bit3: Lowtolmodus Bit4: EMV Kundenmodus, Bit5: Handsteuermodus, Bit6: Noplausmodus, Bit7: Nousermodus |
| STATUS2 | int | Status Steuergeraet (Modus) Bit0:  CYCLIC EMC , Bit1: Lebensdauertests, Bit2: Regelungsverhinderer deaktivieren, Bit3: Auto senken Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-set-actuators"></a>
### SET_ACTUATORS

Aktuatoren setzen/ ruecksetzen Check the Pneumatic layout before acivating valves System can be damaged !

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACTUATORS1 | int | Aktuatoren Bit0: MV_FR, Bit1: MV_FL, Bit2: MV_RR, Bit3: MV_RL Bit4: MV_RES, Bit5: MV_EX, Bit6: C_SW, Bit7: reserved MV_FR  = Magnetventil Front Right MV_FL  = Magnetventil Front Left MV_RR  = Magnetventil Rear Right MV_RL  = Magnetventil Rear left MV_RES = Reservoir Valve MV_EX  = Exhaust Valve C_SW   = Compressor Switch |
| ACTUATORS2 | int | Aktuatoren Bit0: MV_HPEX, Bit1: reserved, Bit2: reserved, Bit3: reserved Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved MV_HPEX = Magnetventil High pressure Exhaust Valve |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-set-leds"></a>
### SET_LEDS

LEDs setzen/ ruecksetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LEDS1 | int | LEDs Bit0: reserved, Bit1: standard, Bit2: reserved, Bit3: reserved Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: offroad |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-set-valve-sw-lss"></a>
### SET_VALVE_SW_LSS

set valve switches LSS (Low Side Switch) in full access

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALVE_SW1 | int | valve switches Bit0: MV_FR, Bit1: MV_FL, Bit2: MV_RR, Bit3: MV_RL Bit4: MV_RES, Bit5: MV_EX, Bit6: C_SW, Bit7: reserved MV_FR  = Magnetventil Front Right MV_FL  = Magnetventil Front Left MV_RR  = Magnetventil Rear Right MV_RL  = Magnetventil Rear left MV_RES = Reservoir Valve MV_EX  = Exhaust Valve C_SW   = Compressor Switch |
| VALVE_SW2 | int | valve switches Bit0: MV_HPEX, Bit1: reserved, Bit2: reserved, Bit3: reserved Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved MV_HPEX = Magnetventil High pressure Exhaust Valve |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-set-valve-sw-hss"></a>
### SET_VALVE_SW_HSS

set valve switches HSS (High SIde Switch) in full access

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALVE_SW1 | int | valve switches Bit0: HSS_FRONT, Bit1: HSS_REAR, Bit2: HSS_RES, Bit3: PWR_UPULL Bit4: PWR_SENS1, Bit5: PWR_SENS2, Bit6: PWR_SENS3, Bit7: reserved HSS_FRONT HSS_REAR HSS_RES    = High Side Switch - Reservoir PWR_UPULL PWR_SENS1 PWR_SENS2 PWR_SENS3 |
| VALVE_SW2 | int | valve switches Bit0: reserved, Bit1: reserved, Bit2: reserved, Bit3: reserved Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-set-ecu-status"></a>
### SET_ECU_STATUS

Steuergerätestatus einstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STATUS1 | int | Status Steuergeraet (Modus) Bit0: Dump Modus, Bit1: Band Modus, Bit2: Verlademodus, Bit3: Lowtolmodus Bit4: EMV Kundenmodus, Bit5: Handsteuermodus, Bit6: Noplausmodus, Bit7: Nousermodus |
| STATUS2 | int | Status Steuergeraet (Modus) Bit0:  CYCLIC EMC , Bit1: Lebensdauertests, Bit2: Regelungsverhinderer deaktivieren, Bit3: Auto senken Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-read-ecu-status"></a>
### READ_ECU_STATUS

Steuergerätestatus einstellen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |
| STAT_DUMP_MODUS_EIN | int | Zusatzbotschaften fuer FESTUS [High Aktiv] MODUS 1 |
| STAT_BAND_MODUS_EIN | int | Aktivierungs-Sperre [High Aktiv] MODUS 1 |
| STAT_VERLADE_MODUS_EIN | int | Einstellungen fuer den Transport [High Aktiv] MODUS 1 |
| STAT_LOWTOL_MODUS_EIN | int | Aktiviert sehr enge Toleranzen MODUS 1 |
| STAT_EMV_KUNDEN_MODUS_EIN | int | fuer webaco EMV-Tests [High Aktiv] MODUS 1 |
| STAT_HANDSTEUER_MODUS_EIN | int | Freischaltung fuer I/O Status-Vorgabe [High Aktiv] MODUS 1 |
| STAT_NOPLAU_MODUS_EIN | int | fuer Laborauto Tests [High Aktiv] MODUS 1 |
| STAT_NOUSER_MODUS_EIN | int | SG reagiert nicht mehr auf Benutzeranforderungen MODUS 1 |
| STAT_ZYKEMV_MODUS_EIN | int | Modus um im EMV Test zyklische Ventilansteuerungen zu haben MODUS 2 |
| STAT_TESTMODUS_EIN | int | Modus um Lebensdauertests, etc. durchzufuehren MODUS 2 |
| STAT_NOPREVENTMODUS_EIN | int | Modus um Regelungsverhinderer zu deaktivieren MODUS 2 |
| STAT_SENKEN_EIN | int | Modus um Auto zu senken MODUS 2 |
| STATUS1 | int | Status Seuergeraet (Modus) Bit0: Dump Modus, Bit1: Band Modus, Bit2: Verlademodus, Bit3: Lowtolmodus Bit4: EMV Kundenmodus, Bit5: Handsteuermodus, Bit6: Noplausmodus, Bit7: Nousermodus |
| STATUS2 | int | Status Seuergeraet (Modus) Bit0:  CYCLIC EMC , Bit1: Lebensdauertests, Bit2: Regelungsverhinderer deaktivieren, Bit3: Auto senken Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved |

<a id="job-read-internal-status"></a>
### READ_INTERNAL_STATUS

Auslesen von internen Reglerinformationen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PREVENT_CURVE | int | Regelungsverhinderer Kurve Aktiv |
| PREVENT_ACCEL | int | Regelungsverhinderer Laengsbeschleunigung Aktiv |
| PREVENT_PLAUS | int | Regelungsverhinderer Plausibilitaet Aktiv |
| PREVENT_CARLIFT | int | Regelungsverhinderer Wagenheber Aktiv |
| PREVENT_DOOR | int | Regelungsverhinderer Tuer Aktiv |
| PREVENT_ARTIC | int | Regelungsverhinderer Verschraenkung Aktiv |
| PREVENT_VALVE | int | Regelungsverhinderer Ventil ED Aktiv |
| PREVENT_BRAKES | int | Regelungsverhinderer Bremse Aktiv |
| PREVENT_USER | int | Regelungsverhinderer unterbrochenes Absenken Aktiv |
| CAN_V_CAR | int | Empfangsstatus Fahrzeuggeschwindigkeit |
| CAN_ABS | int | Empfangsstatus DSC Aktivitaet |
| CAN_N_MOT | int | Empfangsstatus Motordrehzahl |
| CAN_KM | int | Empfangsstatus Kilometerstand |
| CAN_A_Q | int | Empfangsstatus Querbeschleunigung |
| CAN_BAS_FBR | int | Empfangsstatus Fahrerbremsung |
| CAN_S_ANH | int | Empfangsstatus Anhaenger |
| CAN_S_TNS | int | Empfangsstatus Tag/Nachtumschaltung |
| CAN_S_HBR | int | Empfangsstatus Handbremse |
| CAN_L_ASC_DEF | int | Empfangsstatus Fehlerstatus DSC |
| GMMNGR_OPMODE | int | Global Modemanager Opmode |
| REG_SLOW | int | Slowfilter aktiv |
| REG_NORMTOL | int | Normales Toleranzband aktiv |
| REG_EXTTOL | int | Erweitertes Toleranzband aktiv |
| REG_LOWTOL | int | Enges Toleranzband aktiv |
| REG_WUPTOL | int | Wakeup Toleranzband aktiv |
| REG_KERB | int | Randsteinerkennung aktiv |
| REG_OTEMP_FILL | int | Randsteinerkennung aktiv |
| REG_OTEMP_REG | int | Randsteinerkennung aktiv |
| UNDERVOLTAGE | int | Unterspannung aktiv |
| OVERVOLTAGE | int | Ueberspannung aktiv |
| XXXSTATEFR | int | Zustand des Reglerblocks Vorderachse |
| XXXSTATERR | int | Zustand des Reglerblocks hinten rechts |
| XXXSTATERL | int | Zustand des Reglerblocks hinten links |
| VLVCTRL_STATE | int | Zustand des ValveCtrl Blocks |
| ACTUATOR_BA_WARN | int | actuator_ba_warn Variable |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary |  |
| _TEL_SEND | binary |  |

<a id="job-set-memory-default"></a>
### SET_MEMORY_DEFAULT

Copy default memory from FLASH to EEPROM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary |  |

<a id="job-set-actuators-time"></a>
### SET_ACTUATORS_TIME

Aktuatoren bestimmte Zeit setzen/ ruecksetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACTUATORS1 | int | Aktuatoren Bit0: MV_FR, Bit1: MV_FL, Bit2: MV_RR, Bit3: MV_RL Bit4: MV_RES, Bit5: MV_EX, Bit6: C_SW, Bit7: reserved MV_FR  = Magnetventil Front Right MV_FL  = Magnetventil Front Left MV_RR  = Magnetventil Rear Right MV_RL  = Magnetventil Rear left MV_RES = Reservoir Valve MV_EX  = Exhaust Valve C_SW   = Compressor Switch |
| ACTUATORS2 | int | Aktuatoren Bit0: MV_HPEX, Bit1: reserved, Bit2: reserved, Bit3: reserved Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved MV_HPEX   = High pressure exhaust |
| TIME | int | Zeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

<a id="job-steuern-ecu-status"></a>
### STEUERN_ECU_STATUS

Steuergerätestatus einstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STATUS1 | int | Status Steuergeraet (Modus) Bit0: Dump Modus, Bit1: Band Modus, Bit2: Verlademodus, Bit3: Lowtolmodus Bit4: EMV Kundenmodus, Bit5: Handsteuermodus, Bit6: Noplausmodus, Bit7: Nousermodus |
| STATUS2 | int | Status Steuergeraet (Modus) Bit0:  CYCLIC EMC , Bit1: Lebensdauertests, Bit2: Regelungsverhinderer deaktivieren, Bit3: Auto senken Bit4: reserved, Bit5: reserved, Bit6: reserved, Bit7: reserved |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_SEND | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
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
- [FORTTEXTE](#table-forttexte) (125 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (13 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (15 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (7 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (3 × 9)
- [SPEZIAL1](#table-spezial1) (1 × 3)
- [SPEZIAL2](#table-spezial2) (1 × 9)
- [SPEZIAL3](#table-spezial3) (1 × 3)
- [SPEZIAL4](#table-spezial4) (1 × 3)
- [HOEHEN](#table-hoehen) (7 × 3)

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

Dimensions: 77 rows × 2 columns

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
| 0x76 | CEL |
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
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 125 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0001 | Balgventil vorne links |
| 0x0002 | Balgventil vorne rechts |
| 0x0003 | Balgventil hinten links |
| 0x0004 | Balgventil hinten rechts |
| 0x0005 | Quersperrventil vorne |
| 0x0006 | Quersperrventil hinten |
| 0x0007 | Ablassventil |
| 0x0008 | Hochdruckablassventil |
| 0x0009 | Speicherventil |
| 0x000A | Kompressorrelais |
| 0x0014 | Versorgung Balgventile vorne |
| 0x0015 | Versorgung Balgventile hinten |
| 0x0016 | Versorgung Quersperrventile |
| 0x0017 | Versorgung Speicherventil/Ablassventil |
| 0x0018 | Versorgung Hochdruckablassventil |
| 0x001E | Hoehenstandssensor vorne links |
| 0x001F | Hoehenstandssensor vorne rechts |
| 0x0020 | Hoehenstandssensor hinten links |
| 0x0021 | Hoehenstandssensor hinten rechts |
| 0x0022 | Speicherdrucksensor |
| 0x0023 | Versorgung Speicherdrucksensor |
| 0x0024 | Kompressortemperatursensor |
| 0x0025 | VA Signal |
| 0x0032 | CAN Bus |
| 0x0034 | Speicherfehler Steuergeraet |
| 0x0035 | interner Fehler Steuergeraet |
| 0x0036 | Codierdatenfehler |
| 0x0037 | interner Abgleichfehler Steuergeraet |
| 0x0064 | Verschraenkungs-Plausibilitaet |
| 0x0065 | Kein/zu langsames Verfahren (ganzes Fzg.) wenn heben angefordert |
| 0x0066 | Kein/zu langsames Verfahren (ganzes Fzg.) wenn absenken angefordert |
| 0x0067 | Zu viel Energie fuer eine Regelung benoetigt: Vorderachse |
| 0x0068 | Zu viel Energie fuer eine Regelung benoetigt: hinten links |
| 0x0069 | Zu viel Energie fuer eine Regelung benoetigt: hinten rechts |
| 0x006A | Zu viel Energie um die Zielhoehe zu erreichen: Vorderachse |
| 0x006B | Zu viel Energie um die Zielhoehe zu erreichen: hinten links |
| 0x006C | Zu viel Energie um die Zielhoehe zu erreichen: hinten rechts |
| 0x006D | Hoehenaenderung in die falsche Richtung (mind. ein Rad), wenn heben angefordert |
| 0x006E | Hoehenaenderung in die falsche Richtung (mind. ein Rad), wenn absenken angefordert |
| 0x006F | Kompressortemperatur steigt, wenn Kompressor nicht angesteuert wird |
| 0x0070 | Kompressortemperatur steigt nicht, wenn Kompressor angesteuert wird |
| 0x0071 | Kompressortemperatur faellt nicht, wenn Kompressor nicht angesteuert wird |
| 0x0072 | Speicherdruck steigt, wenn Speicher nicht aktiv ist |
| 0x0073 | Speicherdruck sinkt, wenn Speicher nicht aktiv ist |
| 0x0074 | Speicherdruck bleibt konstant, wenn Speicherfuellen angefordert wird |
| 0x0075 | Speicherdruck sinkt anfaenglich, wenn Speicherfuellen angefordert wird |
| 0x0076 | Speicherdruck sinkt, wenn Speicherfuellen angefordert wird |
| 0x0077 | Speicherdruck bleibt konstant, wenn Entlueftung angefordert wird |
| 0x0078 | Speicherdruck steigt, wenn Entlueftung angefordert wird |
| 0x0079 | Speicherdruck bleibt konstant, wenn aus dem Speicher nach oben verfahren wird |
| 0x007A | Speicherdruck steigt, wenn aus dem Speicher nach oben verfahren wird |
| 0x007B | Quersperrplausibilitaet Vorderachse |
| 0x007C | Quersperrplausibilitaet Hinterachse |
| 0x007D | links vorne bewegt sich zu langsam |
| 0x007E | rechts vorne bewegt sich zu langsam |
| 0x007F | Aktivitaetsplausibilitaet vorne links |
| 0x0080 | Aktivitaetsplausibilitaet vorne rechts |
| 0x0081 | Aktivitaetsplausibilitaet hinten links |
| 0x0082 | Aktivitaetsplausibilitaet hinten rechts |
| 0x5F8C | Balgventil vorne links |
| 0x5F8D | Balgventil vorne rechts |
| 0x5F8E | Balgventil hinten links |
| 0x5F8F | Balgventil hinten rechts |
| 0x5F90 | Quersperrventil vorne |
| 0x5F91 | Quersperrventil hinten |
| 0x5F92 | Ablassventil |
| 0x5F93 | Hochdruckablassventil |
| 0x5F94 | Speicherventil |
| 0x5F95 | Kompressorrelais |
| 0x5F96 | Versorgung Balgventile vorne |
| 0x5F97 | Versorgung Balgventile hinten |
| 0x5F98 | Versorgung Quersperrventile |
| 0x5F99 | Versorgung Speicherventil/Ablassventil |
| 0x5F9A | Versorgung Hochdruckablassventil |
| 0x5F9B | Hoehenstandssensor vorne links |
| 0x5F9C | Hoehenstandssensor vorne rechts |
| 0x5F9D | Hoehenstandssensor hinten links |
| 0x5F9E | Hoehenstandssensor hinten rechts |
| 0x5F9F | Speicherdrucksensor |
| 0x5FA0 | Versorgung Speicherdrucksensor |
| 0x5FA1 | Kompressortemperatursensor |
| 0x5FA2 | VA Signal |
| 0x5FA4 | Speicherfehler Steuergeraet |
| 0x5FA5 | interner Fehler Steuergeraet |
| 0x5FA6 | Codierdatenfehler |
| 0x5FA7 | interner Abgleichfehler Steuergeraet |
| 0x5FA8 | Verschraenkungs-Plausibilitaet |
| 0x5FA9 | Kein/zu langsames Verfahren (ganzes Fzg.) wenn heben angefordert |
| 0x5FAA | Kein/zu langsames Verfahren (ganzes Fzg.) wenn absenken angefordert |
| 0x5FAB | Zu viel Energie fuer eine Regelung benoetigt: Vorderachse |
| 0x5FAC | Zu viel Energie fuer eine Regelung benoetigt: hinten links |
| 0x5FAD | Zu viel Energie fuer eine Regelung benoetigt: hinten rechts |
| 0x5FAE | Zu viel Energie um die Zielhoehe zu erreichen: Vorderachse |
| 0x5FAF | Zu viel Energie um die Zielhoehe zu erreichen: hinten links |
| 0x5FB0 | Zu viel Energie um die Zielhoehe zu erreichen: hinten rechts |
| 0x5FB1 | Hoehenaenderung in die falsche Richtung (mind. ein Rad), wenn heben angefordert |
| 0x5FB2 | Hoehenaenderung in die falsche Richtung (mind. ein Rad), wenn absenken angefordert |
| 0x5FB3 | Kompressortemperatur steigt, wenn Kompressor nicht angesteuert wird |
| 0x5FB4 | Kompressortemperatur steigt nicht, wenn Kompressor angesteuert wird |
| 0x5FB5 | Kompressortemperatur faellt nicht, wenn Kompressor nicht angesteuert wird |
| 0x5FB6 | Speicherdruck steigt, wenn Speicher nicht aktiv ist |
| 0x5FB7 | Speicherdruck sinkt, wenn Speicher nicht aktiv ist |
| 0x5FB8 | Speicherdruck bleibt konstant, wenn Speicherfuellen angefordert wird |
| 0x5FB9 | Speicherdruck sinkt anfaenglich, wenn Speicherfuellen angefordert wird |
| 0x5FBA | Speicherdruck sinkt, wenn Speicherfuellen angefordert wird |
| 0x5FBB | Speicherdruck bleibt konstant, wenn Entlueftung angefordert wird |
| 0x5FBC | Speicherdruck steigt, wenn Entlueftung angefordert wird |
| 0x5FBD | Speicherdruck bleibt konstant, wenn aus dem Speicher nach oben verfahren wird |
| 0x5FBE | Speicherdruck steigt, wenn aus dem Speicher nach oben verfahren wird |
| 0x5FBF | Quersperrplausibilitaet Vorderachse |
| 0x5FC0 | Quersperrplausibilitaet Hinterachse |
| 0x5FC1 | links vorne bewegt sich zu langsam |
| 0x5FC2 | rechts vorne bewegt sich zu langsam |
| 0x5FC3 | Aktivitaetsplausibilitaet vorne links |
| 0x5FC4 | Aktivitaetsplausibilitaet vorne rechts |
| 0x5FC5 | Aktivitaetsplausibilitaet hinten links |
| 0x5FC6 | Aktivitaetsplausibilitaet hinten rechts |
| 0x5FC7 | Energiesparmode aktiv |
| 0xD704 | K-CAN Transceiver LOW |
| 0xD707 | K-CAN Controller BUS Off |
| 0xD73C | K-CAN Fehlerwert erhalten |
| 0xD73D | K-CAN unplausibles Signal |
| 0xD73E | K-CAN Telegramm Timeout |
| 0xD743 | K-CAN NM Fehlerwert erhalten |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 00001111 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 13 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxx0001 | 10001 | Kurzschluss gegen U-Batt |
| xxxx0010 | 10010 | Kurzschluss gegen Masse |
| xxxx0100 | 10100 | Leitungsunterbrechung |
| xxxx1000 | 11000 | Plausibilitaetsfehler |
| xxxx0011 | 10011 | Eingang Floating Plausibilitaetsfehler |
| xxxx0101 | 10101 | Hardwarefehler |
| xxxx0110 | 10110 | Fehler Sensorversorgung |
| xxxx0111 | 10111 | Busfehler |
| xxxx1001 | 11001 | Memoryfehler |
| xxxx1010 | 11010 | Steuergerätefehler |
| xxxx1011 | 11011 | Konfigurationsfehler |
| xxxx1100 | 11100 | Abgleichfehler |
| xxxx1111 | 11111 | unbekannte Fehlerart |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | SPEZIAL1 | SPEZIAL2 | SPEZIAL3 | SPEZIAL4 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 15 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | -- | signed char | - | 1 | 8 | 0 |
| 0x02 | Speicherdruck | Bar | -- | unsigned char | - | 1 | 8 | 0 |
| 0x03 | Balgventil vorne rechts | 0/1 | -- | 0x0001 | - | - | 1 | - |
| 0x04 | Balgventil vorne links | 0/1 | -- | 0x0002 | - | - | 1 | - |
| 0x05 | Balgventil hinten rechts | 0/1 | -- | 0x0004 | - | - | 1 | - |
| 0x06 | Balgventil hinten links | 0/1 | -- | 0x0008 | - | - | 1 | - |
| 0x07 | Speicherventil | 0/1 | -- | 0x0010 | - | - | 1 | - |
| 0x08 | Ablassventil | 0/1 | -- | 0x0020 | - | - | 1 | - |
| 0x09 | Kompressorschalter | 0/1 | -- | 0x0040 | - | - | 1 | - |
| 0x0A | Hochdruckablassventil | 0/1 | -- | 0x0080 | - | - | 1 | - |
| 0x0B | Fahrzeuggeschwindigkeit | km/h | -- | unsigned char | - | 1 | 1 | 0 |
| 0x0C | Kompressortemperatur | °C | -- | unsigned char | - | 1 | 1 | -40 |
| 0x0E | durchschn. Fahrzeughoehe | mm | -- | signed char | - | 1 | 1 | 0 |
| 0x0F | reserved | - | -- | unsigned char | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | XY | -- | unsigned int | -- | 25 | 255 | 0 |

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

Dimensions: 7 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x1001 | Fehler a |
| 0x1002 | Fehler b |
| 0x1003 | Fehler c |
| 0x1004 | Fehler d |
| 0x1005 | Fehler e |
| 0x1006 | Fehler f |
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

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | -- | -- |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Batteriespannung | Volt | -- | unsigned char | - | 1 | 1 | 0 |
| 0x02 | Aussentemperatur | Grad C | -- | signed char | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | - | 1 | 1 | 0 |

<a id="table-spezial1"></a>
### SPEZIAL1

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x02 | 0x01 |

<a id="table-spezial2"></a>
### SPEZIAL2

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A |

<a id="table-spezial3"></a>
### SPEZIAL3

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x0B | 0x0C |

<a id="table-spezial4"></a>
### SPEZIAL4

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x0F | 0x0E |

<a id="table-hoehen"></a>
### HOEHEN

Dimensions: 7 rows × 3 columns

| HOEHEN | BYTE | BITWERT |
| --- | --- | --- |
| ACCESS | 0 | 0x02 |
| MOTORWAY | 0 | 0x04 |
| STANDARD | 0 | 0x08 |
| OFFROAD | 0 | 0x10 |
| REG_DOWN | 0 | 0x40 |
| REG_UP | 0 | 0x80 |
| XXX | Y | Z |
