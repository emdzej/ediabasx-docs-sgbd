# mrsaf.prg

- Jobs: [85](#jobs)
- Tables: [68](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Semiaktives Fahrwerk |
| ORIGIN | BMW UX-EE-2 Dreifke_Lars |
| REVISION | 3.000 |
| AUTHOR | Dräxlmaier UX-EE-1 Rätscher |
| COMMENT | N/A |
| PACKAGE | 1.62 |
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
- [STATUS_BATTERIESPANNUNG](#job-status-batteriespannung) - Auslesen der aktuellen Batteriespannung KWP2000: $21 ReadDataByLocalIdentifier $02 Batteriespannung Default
- [STATUS_HALLSENSOR](#job-status-hallsensor) - Spannung und Zustand der Hallsensoren KWP2000: $21 ReadDataByLocalIdentifier $03 Hallsensoren Default
- [STATUS_ANALOGSENSOR_ROH](#job-status-analogsensor-roh) - Auslesen der Rohwerte der Analogsensoren KWP2000: $21 ReadDataByLocalIdentifier $0A Analogsensoren Rohwerte Modus  : Default
- [STATUS_ANALOGSENSOR_PHYS](#job-status-analogsensor-phys) - Auslesen der physikalischen Werte der Analogsensoren KWP2000: $21 ReadDataByLocalIdentifier $09 Analogsensoren physikalisch Modus  : Default
- [STATUS_ADAPTIONSWERTE](#job-status-adaptionswerte) - Auslesen der HL-SW Adaptionswerte KWP2000: $21 ReadDataByLocalIdentifier $0D Adaptionswerte HL-SW Modus  : Default
- [STATUS_KOMBISCHALTER](#job-status-kombischalter) - Auslesen der aktuellen Schalterzustaende KWP2000: $21 ReadDataByLocalIdentifier $08 Kombischalter Default
- [STATUS_DC_MOTOR_PWM](#job-status-dc-motor-pwm) - Auslesen PWM Werte DC Motor KWP2000: $21 ReadDataByLocalIdentifier $0B DC Motor PWM Modus  : Default
- [STATUS_TEMPERATURMODELL](#job-status-temperaturmodell) - Auslesen der DC Motor Temperatur KWP2000: $21 ReadDataByLocalIdentifier $0C Temperaturmodell Modus  : Default
- [STEUERN_VENTIL_PWM_START](#job-steuern-ventil-pwm-start) - Uebernahme der IO-Kontrolle vom Steuergeraet und Vorgabe PWM und Frequenz fuer Proportionalventile KWP2000: $30 InputOutputControlByLocalIdentifier $01 Proportionalventile PWM $07 shortTermAdjustment Modus  : Default
- [STEUERN_VENTIL_PWM_STOP](#job-steuern-ventil-pwm-stop) - Rueckgabe der IO-Kontrolle an das Steuergeraet KWP2000: $30 InputOutputControlByLocalIdentifier $01 Proportionalventile PWM $00 returnControlToECU Modus  : Default
- [STATUS_VENTIL_PWM](#job-status-ventil-pwm) - Auslesen des aktuellen Zustands der Proportionalventile KWP2000: $22 ReadDataByCommonIdentifier $E137 Proportionalventile PWM Modus  : Default
- [STEUERN_VENTIL_STROM_START](#job-steuern-ventil-strom-start) - Uebernahme der IO-Kontrolle vom Steuergeraet und Vorgabe Stromwert fuer Proportionalventile KWP2000: $30 InputOutputControlByLocalIdentifier $04 Proportionalventile Strom $07 shortTermAdjustment Modus  : Default
- [STEUERN_VENTIL_STROM_STOP](#job-steuern-ventil-strom-stop) - Rueckgabe der IO-Kontrolle an das Steuergeraet KWP2000: $30 InputOutputControlByLocalIdentifier $04 Proportionalventile Strom $00 returnControlToECU Modus  : Default
- [STATUS_VENTIL_STROM](#job-status-ventil-strom) - Auslesen des aktuellen Zustands der Proportionalventile KWP2000: $22 ReadDataByCommonIdentifier $E138 Proportionalventile Strom Modus  : Default
- [STEUERN_DC_MOTOR_START](#job-steuern-dc-motor-start) - Uebernahme der IO-Kontrolle vom Steuergeraet und Vorgabe Impulse (Inkremente) fuer DC Motor KWP2000: $30 InputOutputControlByLocalIdentifier $05 DC Motor $07 shortTermAdjustment Modus  : Default
- [STEUERN_DC_MOTOR_STOP](#job-steuern-dc-motor-stop) - Uebernahme der IO-Kontrolle vom Steuergeraet und Vorgabe Impulse (Inkremente) fuer DC Motor KWP2000: $30 InputOutputControlByLocalIdentifier $05 DC Motor $00 returnControlToECU Modus  : Default
- [STATUS_DC_MOTOR](#job-status-dc-motor) - Statusabfrage Position DC Motor KWP2000: $22 ReadDataByCommonIdentifier $E114 DC Motor Modus  : Default
- [STEUERN_PRODUKTIONSMODE_START](#job-steuern-produktionsmode-start) - Uebernahme der IO-Kontrolle vom Steuergeraet und Einschalten des Produktionsmodus KWP2000: $30 InputOutputControlByLocalIdentifier $06 Produktionsmode $07 shortTermAdjustment Modus  : Default
- [STEUERN_PRODUKTIONSMODE_STOP](#job-steuern-produktionsmode-stop) - Ausschalten des Produktionsmodus und Zurueckgabe der IO-Steuerung an das SG KWP2000: $30 InputOutputControlByLocalIdentifier $06 Produktionsmode $00 returnControlToECU Modus  : Default
- [STEUERN_DAEMPFER_TEST_MODUS_START](#job-steuern-daempfer-test-modus-start) - Uebernahme der IO-Kontrolle vom Steuergeraet und Einschalten des Daempfer_Test- und Showroommodus KWP2000: $30 InputOutputControlByLocalIdentifier $07 Daempfer_Test_Modus $07 shortTermAdjustment Modus  : Default
- [STEUERN_DAEMPFER_TEST_MODUS_STOP](#job-steuern-daempfer-test-modus-stop) - Ausschalten des Daempfer_Test- und Showroommodus und Uebergabe der IO-Kontrolle ans SG zurueck KWP2000: $30 InputOutputControlByLocalIdentifier $07 Daempfer_Test_Modus $00 returnControlToECU Modus  : Default
- [STEUERN_SENSOR_ABGLEICH_ROUTINE_START](#job-steuern-sensor-abgleich-routine-start) - Startet die Routine fuer den Sensorabgleich KWP2000: $31 StartRoutineByLocalIdentifier $20 Kalibrierung Sensoren Modus  : Default
- [STEUERN_SENSOR_ABGLEICH_ROUTINE_STOP](#job-steuern-sensor-abgleich-routine-stop) - Stoppt die Routine fuer die Sensorkalibrierung KWP2000: $32 StopRoutineByLocalIdentifier $20 Kalibrierung Sensoren Modus  : Default
- [STEUERN_SENSOR_ABGLEICH_ROUTINE_RESULTS](#job-steuern-sensor-abgleich-routine-results) - Status der Routine fuer den Sensorabgleich KWP2000: $33 RequestRoutineResultsByLocalIdentifier $20 Kalibrierung Sensoren Modus  : Default
- [STEUERN_KALIBRIERUNG_FEDERBEIN_ROUTINE_START](#job-steuern-kalibrierung-federbein-routine-start) - Startet die Routine fuer Federbeinkalibrierung KWP2000: $31 StartRoutineByLocalIdentifier $21 Kalibrierung Federbein Modus  : Default
- [STEUERN_KALIBRIERUNG_FEDERBEIN_ROUTINE_STOP](#job-steuern-kalibrierung-federbein-routine-stop) - Stoppt die Routine fuer die Federbeinkalibrierung KWP2000: $32 StopRoutineByLocalIdentifier $21 Kalibrierung Federbein Modus  : Default
- [STEUERN_KALIBRIERUNG_FEDERBEIN_ROUTINE_RESULTS](#job-steuern-kalibrierung-federbein-routine-results) - Status der Routine fuer die Federbeinkalibrierung KWP2000: $33 RequestRoutineResultsByLocalIdentifier $21 Kalibrierung Federbein Modus  : Default
- [STEUERN_FAHREREINSTELLUNG_ROUTINE_START](#job-steuern-fahrereinstellung-routine-start) - Startet die Routine fuer die Fahrereinstellung KWP2000: $31 StartRoutineByLocalIdentifier $22 Fahrereinstellung Modus  : Default
- [STEUERN_FAHREREINSTELLUNG_ROUTINE_RESULTS](#job-steuern-fahrereinstellung-routine-results) - Status der Routine fuer die Fahrereinstellung KWP2000: $33 RequestRoutineResultsByLocalIdentifier $22 Fahrereinstellung Modus  : Default
- [STATUS_RACECAL](#job-status-racecal) - Dieser Job liest den Status des Race Calibration Kits 0xE001 RACECAL_STAT
- [STATUS_RACECAL_DAMP_FAC](#job-status-racecal-damp-fac) - Dieser Job liest die Kalibrierungsdaten fuer die manuelle Verstellung der Zug-/Druckstufe 0xE002 RACECAL_DAMP_FAC
- [STATUS_RACECAL_WHEEL_INF](#job-status-racecal-wheel-inf) - Dieser Job liest die Kalibrierungsdaten fuer die montierte Reifen 0xE003 RACECAL_WHEEL_INF
- [STATUS_RACECAL_TRACK](#job-status-racecal-track) - Dieser Job liest die Kalibrierungsdaten fuer die Rennstrecke 0xE004 RACECAL_TRACK
- [STATUS_RACECAL_SHIMMING](#job-status-racecal-shimming) - Dieser Job liest die Kalibrierungsdaten fuer e-Shimming 0xE005 RACECAL_SHIMMING
- [STATUS_RACECAL_CHKSUM](#job-status-racecal-chksum) - Dieser Job liest die Checksumme der Kalibrierungsdaten 0xE006 RACECAL_CHKSUM
- [STATUS_RACECAL_INFO](#job-status-racecal-info) - Dieser Job liest die Informationen zum aktiven Datensatz 0xE007 RACECAL_INFO
- [STATUS_RACECAL_HIST](#job-status-racecal-hist) - Dieser Job liest die Historie der Kalibrierungssaetze 0xE008 RACECAL_HIST
- [STATUS_RACECAL_SETUP](#job-status-racecal-setup) - Dieser Job liest Verbauzustand des Federwegsensors vorne 0xE009 RACECAL_SETUP

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

<a id="job-status-batteriespannung"></a>
### STATUS_BATTERIESPANNUNG

Auslesen der aktuellen Batteriespannung KWP2000: $21 ReadDataByLocalIdentifier $02 Batteriespannung Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BATTERIESPANNUNG_WERT | real | Batteriespannung in V |
| STAT_BATTERIESPANNUNG_EINH | string | Einheit der gemessenen Spannung |
| _TEL_REQUEST | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hallsensor"></a>
### STATUS_HALLSENSOR

Spannung und Zustand der Hallsensoren KWP2000: $21 ReadDataByLocalIdentifier $03 Hallsensoren Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HALL1_SPANNUNG_HINTEN_WERT | real | Spannung Hall-Sensor 1 Federbein hinten |
| STAT_HALL1_SPANNUNG_HINTEN_EINH | string | Einheit der gemessenen Spannung |
| STAT_HALL2_SPANNUNG_HINTEN_WERT | real | Spannung Hall-Sensor 2 Federbein hinten |
| STAT_HALL2_SPANNUNG_HINTEN_EINH | string | Einheit der gemessenen Spannung |
| STAT_HALL1_SPANNUNG_HINTEN_PEGEL | unsigned char | Status Hall-Sensor 1 Federbein hinten: 0 = niedriger Pegel 1 = hoher Pegel |
| STAT_HALL2_SPANNUNG_HINTEN_PEGEL | unsigned char | Status Hall-Sensor 2 Federbein hinten: 0 = niedriger Pegel 1 = hoher Pegel |
| STAT_HALL_HINTEN_VERBAUT | unsigned char | Verbauzustand Hall-Sensor hinten: 0 = Hallsensor nicht verbaut 1 = Hallsensor verbaut |
| STAT_DC_MOTOR_HINTEN | unsigned char | Zustandswert DC-Motor hinten |
| STAT_DC_MOTOR_HINTEN_TEXT | string | Zustand DC-Motor hinten Werte siehe table TAB_STATUS_DC_MOTOR |
| STAT_MAX_HALL_COUNTS_WERT | unsigned int | Bei einer Vollkalibrierung ermittelte maximale Anzahl von Hallsensor-Impulsen von Endanschlag bis Endanschlag |
| STAT_MAX_HALL_COUNTS_EINH | string | Einheit der ermittelten Impulsanzahl |
| _TEL_REQUEST | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analogsensor-roh"></a>
### STATUS_ANALOGSENSOR_ROH

Auslesen der Rohwerte der Analogsensoren KWP2000: $21 ReadDataByLocalIdentifier $0A Analogsensoren Rohwerte Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SENSOR1_WERT | int | Rohwert Sensor 1 |
| STAT_SENSOR1_EINH | string | Einheit fuer den Rohwert Sensor 1 |
| STAT_SENSOR2_WERT | int | Rohwert Sensor 2 |
| STAT_SENSOR2_EINH | string | Einheit fuer den Rohwert Sensor 2 |
| STAT_SENSOR3_WERT | int | Rohwert Sensor 3 |
| STAT_SENSOR3_EINH | string | Einheit fuer den Rohwert Sensor 3 |
| STAT_SENSOR4_WERT | int | Rohwert Sensor 4 |
| STAT_SENSOR4_EINH | string | Einheit fuer den Rohwert Sensor 4 |
| _TEL_REQUEST | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analogsensor-phys"></a>
### STATUS_ANALOGSENSOR_PHYS

Auslesen der physikalischen Werte der Analogsensoren KWP2000: $21 ReadDataByLocalIdentifier $09 Analogsensoren physikalisch Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SENSOR1_WERT | int | Physikalischer Wert Sensor 1 |
| STAT_SENSOR1_EINH | string | Einheit fuer den physikalischen Wert Sensor 1 |
| STAT_SENSOR2_WERT | int | Physikalischer Wert Sensor 2 |
| STAT_SENSOR2_EINH | string | Einheit fuer den physikalischen Wert Sensor 2 |
| STAT_SENSOR3_WERT | real | Physikalischer Wert Sensor 3 |
| STAT_SENSOR3_EINH | string | Einheit fuer den physikalischen Wert Sensor 3 |
| STAT_SENSOR4_WERT | real | Physikalischer Wert Sensor 4 |
| STAT_SENSOR4_EINH | string | Einheit fuer den physikalischen Wert Sensor 4 |
| _TEL_REQUEST | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-adaptionswerte"></a>
### STATUS_ADAPTIONSWERTE

Auslesen der HL-SW Adaptionswerte KWP2000: $21 ReadDataByLocalIdentifier $0D Adaptionswerte HL-SW Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LVAL_ACTUAL_SENSOR1_WERT | int | Adaptionswert Sensor 1 |
| STAT_LVAL_ACTUAL_SENSOR1_EINH | string | Einheit fuer den Adaptionswert Sensor 1 |
| STAT_LVAL_ACTUAL_SENSOR2_WERT | int | Adaptionswert Sensor 2 |
| STAT_LVAL_ACTUAL_SENSOR2_EINH | string | Einheit fuer den Adaptionswert Sensor 2 |
| STAT_LVAL_ACTUAL_SENSOR3_WERT | real | Adaptionswert Sensor 3 |
| STAT_LVAL_ACTUAL_SENSOR3_EINH | string | Einheit fuer den Adaptionswert Sensor 3 |
| STAT_LVAL_ACTUAL_SENSOR4_WERT | real | Adaptionswert Sensor 4 |
| STAT_LVAL_ACTUAL_SENSOR4_EINH | string | Einheit fuer den Adaptionswert Sensor 4 |
| _TEL_REQUEST | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kombischalter"></a>
### STATUS_KOMBISCHALTER

Auslesen der aktuellen Schalterzustaende KWP2000: $21 ReadDataByLocalIdentifier $08 Kombischalter Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SCHALTER1 | unsigned char | Schalterzustand: 0 = Schalter aus 1 = Schalter ein |
| STAT_SCHALTER2 | unsigned char | Schalterzustand: 0 = Schalter aus 1 = Schalter ein |
| STAT_SCHALTER3 | unsigned char | Schalterzustand: 0 = Schalter aus 1 = Schalter ein |
| STAT_SCHALTER4 | unsigned char | Schalterzustand: 0 = Schalter aus 1 = Schalter ein |
| STAT_SCHALTER5 | unsigned char | Schalterzustand: 0 = Schalter aus 1 = Schalter ein |
| STAT_SCHALTER6 | unsigned char | Schalterzustand: 0 = Schalter aus 1 = Schalter ein |
| _TEL_REQUEST | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dc-motor-pwm"></a>
### STATUS_DC_MOTOR_PWM

Auslesen PWM Werte DC Motor KWP2000: $21 ReadDataByLocalIdentifier $0B DC Motor PWM Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DC_MOTOR_PWM_WERT | int | Vorzeichenbehafteter PWM Wert DC Motor |
| STAT_DC_MOTOR_PWM_EINH | string | Einheit fuer PWM DC Motor |
| STAT_DC_MOTOR_EIN | unsigned char | Aktueller Status der beiden digitalen DC Motor Ausgaenge 0 = beide aus 1 = mindestens ein Ausgang liefert Spannung |
| _TEL_REQUEST | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temperaturmodell"></a>
### STATUS_TEMPERATURMODELL

Auslesen der DC Motor Temperatur KWP2000: $21 ReadDataByLocalIdentifier $0C Temperaturmodell Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DC_MOTOR_TEMP_WERT | int | Temperatur des DC Motors |
| STAT_DC_MOTOR_TEMP_EINH | string | Einheit fuer Temperatur DC Motor |
| STAT_DC_MOTOR_UETEMP | unsigned char | Status Uebertemperatur Federbein 0 = keine Uebertemperatur, Federbeinverstellung moeglich 1 = Uebertemperatur, Federbeinverstellung nicht moeglich |
| _TEL_REQUEST | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ventil-pwm-start"></a>
### STEUERN_VENTIL_PWM_START

Uebernahme der IO-Kontrolle vom Steuergeraet und Vorgabe PWM und Frequenz fuer Proportionalventile KWP2000: $30 InputOutputControlByLocalIdentifier $01 Proportionalventile PWM $07 shortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL | string | Bestimmt das zu steuernde Ventil table TAB_VENTIL_ANSTEUERUNG TEXT |
| PWM | unsigned char | Einzustellender PWM Wert 0..100 [%] |
| FREQ | string | Einzustellende PWM Frequenz table TAB_MR_SAF_FREQ TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VORNE_PWM_WERT | unsigned char | Aktueller PWM Wert Ventil vorne |
| STAT_VORNE_PWM_EINH | string | Einheit des PWM Wertes |
| STAT_VORNE_FREQ | unsigned char | Tabellenwert der Frequenz Ventil vorne |
| STAT_VORNE_FREQ_TEXT | string | Frequenz des Ventils vorne table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_VORNE | unsigned char | Zustandswert des Proportionalventils vorne |
| STAT_VENTIL_VORNE_TEXT | string | Zustand des Proportionalventils vorne table TAB_PROPVENTILSTATUS TEXT |
| STAT_HINTEN_PWM_WERT | unsigned char | Aktueller PWM Wert Ventil hinten |
| STAT_HINTEN_PWM_EINH | string | Einheit des PWM Wertes |
| STAT_HINTEN_FREQ | unsigned char | Tabellenwert der Frequenz Ventil hinten |
| STAT_HINTEN_FREQ_TEXT | string | Frequenz des Ventils hinten table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_HINTEN | unsigned char | Zustandswert des Proportionalventils hinten |
| STAT_VENTIL_HINTEN_TEXT | string | Zustand des Proportionalventils hinten table TAB_PROPVENTILSTATUS TEXT |
| STAT_LENKUNG_PWM_WERT | unsigned char | Aktueller PWM Wert Ventil Lenkung |
| STAT_LENKUNG_PWM_EINH | string | Einheit des PWM Wertes |
| STAT_LENKUNG_FREQ | unsigned char | Tabellenwert der Frequenz Ventil Lenkung |
| STAT_LENKUNG_FREQ_TEXT | string | Frequenz des Ventils Lenkung table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_LENKUNG | unsigned char | Zustandswert des Proportionalventils Lenkung |
| STAT_VENTIL_LENKUNG_TEXT | string | Zustand des Proportionalventils Lenkung table TAB_PROPVENTILSTATUS TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ventil-pwm-stop"></a>
### STEUERN_VENTIL_PWM_STOP

Rueckgabe der IO-Kontrolle an das Steuergeraet KWP2000: $30 InputOutputControlByLocalIdentifier $01 Proportionalventile PWM $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VORNE_PWM_WERT | unsigned char | Aktueller PWM Wert Ventil vorne |
| STAT_VORNE_PWM_EINH | string | Einheit des PWM Wertes |
| STAT_VORNE_FREQ | unsigned char | Tabellenwert der Frequenz Ventil vorne |
| STAT_VORNE_FREQ_TEXT | string | Frequenz des Ventils vorne table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_VORNE | unsigned char | Zustandswert des Proportionalventils vorne |
| STAT_VENTIL_VORNE_TEXT | string | Zustand des Proportionalventils vorne table TAB_PROPVENTILSTATUS TEXT |
| STAT_HINTEN_PWM_WERT | unsigned char | Aktueller PWM Wert Ventil hinten |
| STAT_HINTEN_PWM_EINH | string | Einheit des PWM Wertes |
| STAT_HINTEN_FREQ | unsigned char | Tabellenwert der Frequenz Ventil hinten |
| STAT_HINTEN_FREQ_TEXT | string | Frequenz des Ventils hinten table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_HINTEN | unsigned char | Zustandswert des Proportionalventils hinten |
| STAT_VENTIL_HINTEN_TEXT | string | Zustand des Proportionalventils hinten table TAB_PROPVENTILSTATUS TEXT |
| STAT_LENKUNG_PWM_WERT | unsigned char | Aktueller PWM Wert Ventil Lenkung |
| STAT_LENKUNG_PWM_EINH | string | Einheit des PWM Wertes |
| STAT_LENKUNG_FREQ | unsigned char | Tabellenwert der Frequenz Ventil Lenkung |
| STAT_LENKUNG_FREQ_TEXT | string | Frequenz des Ventils Lenkung table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_LENKUNG | unsigned char | Zustandswert des Proportionalventils Lenkung |
| STAT_VENTIL_LENKUNG_TEXT | string | Zustand des Proportionalventils Lenkung table TAB_PROPVENTILSTATUS TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ventil-pwm"></a>
### STATUS_VENTIL_PWM

Auslesen des aktuellen Zustands der Proportionalventile KWP2000: $22 ReadDataByCommonIdentifier $E137 Proportionalventile PWM Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VORNE_PWM_WERT | unsigned char | Aktueller PWM Wert Ventil vorne |
| STAT_VORNE_PWM_EINH | string | Einheit des PWM Wertes |
| STAT_VORNE_FREQ | unsigned char | Tabellenwert der Frequenz Ventil vorne |
| STAT_VORNE_FREQ_TEXT | string | Frequenz des Ventils vorne table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_VORNE | unsigned char | Zustandswert des Proportionalventils vorne |
| STAT_VENTIL_VORNE_TEXT | string | Zustand des Proportionalventils vorne table TAB_PROPVENTILSTATUS TEXT |
| STAT_HINTEN_PWM_WERT | unsigned char | Aktueller PWM Wert Ventil hinten |
| STAT_HINTEN_PWM_EINH | string | Einheit des PWM Wertes |
| STAT_HINTEN_FREQ | unsigned char | Tabellenwert der Frequenz Ventil hinten |
| STAT_HINTEN_FREQ_TEXT | string | Frequenz des Ventils hinten table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_HINTEN | unsigned char | Zustandswert des Proportionalventils hinten |
| STAT_VENTIL_HINTEN_TEXT | string | Zustand des Proportionalventils hinten table TAB_PROPVENTILSTATUS TEXT |
| STAT_LENKUNG_PWM_WERT | unsigned char | Aktueller PWM Wert Ventil Lenkung |
| STAT_LENKUNG_PWM_EINH | string | Einheit des PWM Wertes |
| STAT_LENKUNG_FREQ | unsigned char | Tabellenwert der Frequenz Ventil Lenkung |
| STAT_LENKUNG_FREQ_TEXT | string | Frequenz des Ventils Lenkung table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_LENKUNG | unsigned char | Zustandswert des Proportionalventils Lenkung |
| STAT_VENTIL_LENKUNG_TEXT | string | Zustand des Proportionalventils Lenkung table TAB_PROPVENTILSTATUS TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ventil-strom-start"></a>
### STEUERN_VENTIL_STROM_START

Uebernahme der IO-Kontrolle vom Steuergeraet und Vorgabe Stromwert fuer Proportionalventile KWP2000: $30 InputOutputControlByLocalIdentifier $04 Proportionalventile Strom $07 shortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL | string | Bestimmt das zu steuernde Ventil table TAB_VENTIL_ANSTEUERUNG TEXT |
| STROMWERT | unsigned int | Vorgegebener Stromwert in mA |
| FREQ | string | Einzustellende PWM Frequenz table TAB_MR_SAF_FREQ TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VENTIL_VORNE | unsigned char | Zustandswert des Proportionalventils vorne |
| STAT_VENTIL_VORNE_TEXT | string | Zustand des Proportionalventils vorne table TAB_PROPVENTILSTATUS TEXT |
| STAT_STROM_VENTIL_VORNE_WERT | unsigned int | Aktueller Stromwert des Proportionalventils vorne in mA |
| STAT_STROM_VENTIL_VORNE_EINH | string | Einheit des gemessenen Stroms |
| STAT_VORNE_FREQ | unsigned char | Tabellenwert der Frequenz Ventil vorne |
| STAT_VORNE_FREQ_TEXT | string | Frequenz des Ventils vorne table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_HINTEN | unsigned char | Zustandswert des Proportionalventils hinten |
| STAT_VENTIL_HINTEN_TEXT | string | Zustand des Proportionalventils hinten table TAB_PROPVENTILSTATUS TEXT |
| STAT_STROM_VENTIL_HINTEN_WERT | unsigned int | Aktueller Stromwert des Proportionalventils hinten in mA |
| STAT_STROM_VENTIL_HINTEN_EINH | string | Einheit des gemessenen Stroms |
| STAT_HINTEN_FREQ | unsigned char | Tabellenwert der Frequenz Ventil hinten |
| STAT_HINTEN_FREQ_TEXT | string | Frequenz des Ventils hinten table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_LENKUNG | unsigned char | Zustandswert des Proportionalventils Lenkung |
| STAT_VENTIL_LENKUNG_TEXT | string | Zustand des Proportionalventils Lenkung table TAB_PROPVENTILSTATUS TEXT |
| STAT_STROM_VENTIL_LENKUNG_WERT | unsigned int | Aktueller Stromwert des Proportionalventils Lenkung in mA |
| STAT_STROM_VENTIL_LENKUNG_EINH | string | Einheit des gemessenen Stroms |
| STAT_LENKUNG_FREQ | unsigned char | Tabellenwert der Frequenz Ventil Lenkung |
| STAT_LENKUNG_FREQ_TEXT | string | Frequenz des Ventils Lenkung table TAB_MR_STAT_SAF_FREQ TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ventil-strom-stop"></a>
### STEUERN_VENTIL_STROM_STOP

Rueckgabe der IO-Kontrolle an das Steuergeraet KWP2000: $30 InputOutputControlByLocalIdentifier $04 Proportionalventile Strom $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VENTIL_VORNE | unsigned char | Zustandswert des Proportionalventils vorne |
| STAT_VENTIL_VORNE_TEXT | string | Zustand des Proportionalventils vorne table TAB_PROPVENTILSTATUS TEXT |
| STAT_STROM_VENTIL_VORNE_WERT | unsigned int | Aktueller Stromwert des Proportionalventils vorne in mA |
| STAT_STROM_VENTIL_VORNE_EINH | string | Einheit des gemessenen Stroms |
| STAT_VORNE_FREQ | unsigned char | Tabellenwert der Frequenz Ventil vorne |
| STAT_VORNE_FREQ_TEXT | string | Frequenz des Ventils vorne table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_HINTEN | unsigned char | Zustandswert des Proportionalventils hinten |
| STAT_VENTIL_HINTEN_TEXT | string | Zustand des Proportionalventils hinten table TAB_PROPVENTILSTATUS TEXT |
| STAT_STROM_VENTIL_HINTEN_WERT | unsigned int | Aktueller Stromwert des Proportionalventils hinten in mA |
| STAT_STROM_VENTIL_HINTEN_EINH | string | Einheit des gemessenen Stroms |
| STAT_HINTEN_FREQ | unsigned char | Tabellenwert der Frequenz Ventil hinten |
| STAT_HINTEN_FREQ_TEXT | string | Frequenz des Ventils hinten table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_LENKUNG | unsigned char | Zustandswert des Proportionalventils Lenkung |
| STAT_VENTIL_LENKUNG_TEXT | string | Zustand des Proportionalventils Lenkung table TAB_PROPVENTILSTATUS TEXT |
| STAT_STROM_VENTIL_LENKUNG_WERT | unsigned int | Aktueller Stromwert des Proportionalventils Lenkung in mA |
| STAT_STROM_VENTIL_LENKUNG_EINH | string | Einheit des gemessenen Stroms |
| STAT_LENKUNG_FREQ | unsigned char | Tabellenwert der Frequenz Ventil Lenkung |
| STAT_LENKUNG_FREQ_TEXT | string | Frequenz des Ventils Lenkung table TAB_MR_STAT_SAF_FREQ TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ventil-strom"></a>
### STATUS_VENTIL_STROM

Auslesen des aktuellen Zustands der Proportionalventile KWP2000: $22 ReadDataByCommonIdentifier $E138 Proportionalventile Strom Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VENTIL_VORNE | unsigned char | Zustandswert des Proportionalventils vorne |
| STAT_VENTIL_VORNE_TEXT | string | Zustand des Proportionalventils vorne table TAB_PROPVENTILSTATUS TEXT |
| STAT_STROM_VENTIL_VORNE_WERT | unsigned int | Aktueller Stromwert des Proportionalventils vorne in mA |
| STAT_STROM_VENTIL_VORNE_EINH | string | Einheit des gemessenen Stroms |
| STAT_VORNE_FREQ | unsigned char | Tabellenwert der Frequenz Ventil vorne |
| STAT_VORNE_FREQ_TEXT | string | Frequenz des Ventils vorne table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_HINTEN | unsigned char | Zustandswert des Proportionalventils hinten |
| STAT_VENTIL_HINTEN_TEXT | string | Zustand des Proportionalventils hinten table TAB_PROPVENTILSTATUS TEXT |
| STAT_STROM_VENTIL_HINTEN_WERT | unsigned int | Aktueller Stromwert des Proportionalventils hinten in mA |
| STAT_STROM_VENTIL_HINTEN_EINH | string | Einheit des gemessenen Stroms |
| STAT_HINTEN_FREQ | unsigned char | Tabellenwert der Frequenz Ventil hinten |
| STAT_HINTEN_FREQ_TEXT | string | Frequenz des Ventils hinten table TAB_MR_STAT_SAF_FREQ TEXT |
| STAT_VENTIL_LENKUNG | unsigned char | Zustandswert des Proportionalventils Lenkung |
| STAT_VENTIL_LENKUNG_TEXT | string | Zustand des Proportionalventils Lenkung table TAB_PROPVENTILSTATUS TEXT |
| STAT_STROM_VENTIL_LENKUNG_WERT | unsigned int | Aktueller Stromwert des Proportionalventils Lenkung in mA |
| STAT_STROM_VENTIL_LENKUNG_EINH | string | Einheit des gemessenen Stroms |
| STAT_LENKUNG_FREQ | unsigned char | Tabellenwert der Frequenz Ventil Lenkung |
| STAT_LENKUNG_FREQ_TEXT | string | Frequenz des Ventils Lenkung table TAB_MR_STAT_SAF_FREQ TEXT |
| _TEL_REQUEST | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dc-motor-start"></a>
### STEUERN_DC_MOTOR_START

Uebernahme der IO-Kontrolle vom Steuergeraet und Vorgabe Impulse (Inkremente) fuer DC Motor KWP2000: $30 InputOutputControlByLocalIdentifier $05 DC Motor $07 shortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RICHTUNG_DC | unsigned char | Verstellrichtung DC Motor: 0 = Feder entspannen 1 = Feder spannen |
| RELATIVWERT | unsigned int | Vorgegebener relativer Verstellweg Bereich: 0..6000 Impulse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DC_MOTOR_WERT | unsigned int | Ist Position DC Motor |
| STAT_DC_MOTOR_EINH | string | Einheit der Ist Position DC Motor |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dc-motor-stop"></a>
### STEUERN_DC_MOTOR_STOP

Uebernahme der IO-Kontrolle vom Steuergeraet und Vorgabe Impulse (Inkremente) fuer DC Motor KWP2000: $30 InputOutputControlByLocalIdentifier $05 DC Motor $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DC_MOTOR_WERT | unsigned int | Ist Position DC Motor |
| STAT_DC_MOTOR_EINH | string | Einheit der Ist Position DC Motor |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dc-motor"></a>
### STATUS_DC_MOTOR

Statusabfrage Position DC Motor KWP2000: $22 ReadDataByCommonIdentifier $E114 DC Motor Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DC_MOTOR_WERT | unsigned int | Ist Position DC Motor |
| STAT_DC_MOTOR_EINH | string | Einheit der Ist Position DC Motor |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-produktionsmode-start"></a>
### STEUERN_PRODUKTIONSMODE_START

Uebernahme der IO-Kontrolle vom Steuergeraet und Einschalten des Produktionsmodus KWP2000: $30 InputOutputControlByLocalIdentifier $06 Produktionsmode $07 shortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-produktionsmode-stop"></a>
### STEUERN_PRODUKTIONSMODE_STOP

Ausschalten des Produktionsmodus und Zurueckgabe der IO-Steuerung an das SG KWP2000: $30 InputOutputControlByLocalIdentifier $06 Produktionsmode $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-daempfer-test-modus-start"></a>
### STEUERN_DAEMPFER_TEST_MODUS_START

Uebernahme der IO-Kontrolle vom Steuergeraet und Einschalten des Daempfer_Test- und Showroommodus KWP2000: $30 InputOutputControlByLocalIdentifier $07 Daempfer_Test_Modus $07 shortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-daempfer-test-modus-stop"></a>
### STEUERN_DAEMPFER_TEST_MODUS_STOP

Ausschalten des Daempfer_Test- und Showroommodus und Uebergabe der IO-Kontrolle ans SG zurueck KWP2000: $30 InputOutputControlByLocalIdentifier $07 Daempfer_Test_Modus $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sensor-abgleich-routine-start"></a>
### STEUERN_SENSOR_ABGLEICH_ROUTINE_START

Startet die Routine fuer den Sensorabgleich KWP2000: $31 StartRoutineByLocalIdentifier $20 Kalibrierung Sensoren Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_KANAL | string | Bestimmt das zu steuernde Ventil table TAB_MR_SENSORKANAL TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sensor-abgleich-routine-stop"></a>
### STEUERN_SENSOR_ABGLEICH_ROUTINE_STOP

Stoppt die Routine fuer die Sensorkalibrierung KWP2000: $32 StopRoutineByLocalIdentifier $20 Kalibrierung Sensoren Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sensor-abgleich-routine-results"></a>
### STEUERN_SENSOR_ABGLEICH_ROUTINE_RESULTS

Status der Routine fuer den Sensorabgleich KWP2000: $33 RequestRoutineResultsByLocalIdentifier $20 Kalibrierung Sensoren Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ROUTINE | unsigned char | Zustandswert der Kalibrierroutine |
| STAT_ROUTINE_TEXT | string | Zustand des Proportionalventils vorne table TAB_MR_ROUTINE_SAF TEXT |
| STAT_KANAL1_WERT | int | Offset Kanal1 |
| STAT_KANAL1_EINH | string | Einheit fuer Offset Kanal1 |
| STAT_KANAL2_WERT | int | Offset Kanal2 |
| STAT_KANAL2_EINH | string | Einheit fuer Offset Kanal2 |
| STAT_KANAL3_WERT | int | Offset Kanal3 |
| STAT_KANAL3_EINH | string | Einheit fuer Offset Kanal3 |
| STAT_KANAL4_WERT | int | Offset Kanal4 |
| STAT_KANAL4_EINH | string | Einheit fuer Offset Kanal4 |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kalibrierung-federbein-routine-start"></a>
### STEUERN_KALIBRIERUNG_FEDERBEIN_ROUTINE_START

Startet die Routine fuer Federbeinkalibrierung KWP2000: $31 StartRoutineByLocalIdentifier $21 Kalibrierung Federbein Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ART_KALIBRIERUNG | string | Auswahl Kalibrierungsart table TAB_MR_ART_KALIBRIERUNG_SAF TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kalibrierung-federbein-routine-stop"></a>
### STEUERN_KALIBRIERUNG_FEDERBEIN_ROUTINE_STOP

Stoppt die Routine fuer die Federbeinkalibrierung KWP2000: $32 StopRoutineByLocalIdentifier $21 Kalibrierung Federbein Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kalibrierung-federbein-routine-results"></a>
### STEUERN_KALIBRIERUNG_FEDERBEIN_ROUTINE_RESULTS

Status der Routine fuer die Federbeinkalibrierung KWP2000: $33 RequestRoutineResultsByLocalIdentifier $21 Kalibrierung Federbein Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VOLLKALIBRIERUNG_DC_MOTOR_HINTEN | unsigned char | Zustandswert Vollkalibrierung DC-Motor hinten |
| STAT_VOLLKALIBRIERUNG_DC_MOTOR_HINTEN_TEXT | string | Zustand Vollkalibrierung DC-Motor hinten table TAB_MR_ESA_STATUS_KALIBRIERUNG TEXT |
| STAT_REKALIBRIERUNG_DC_MOTOR_HINTEN | unsigned char | Zustandswert Rekalibrierung DC-Motor hinten |
| STAT_REKALIBRIERUNG_DC_MOTOR_HINTEN_TEXT | string | Zustand Rekalibrierung DC-Motor hinten table TAB_MR_ESA_STATUS_KALIBRIERUNG TEXT |
| STAT_PROP_VENTIL_VORNE | unsigned char | Zustandswert Proportionalventil vorne |
| STAT_PROP_VENTIL_VORNE_TEXT | string | Zustand Proportionalventil vorne table TAB_MR_STATUS_PROP_VENTILE TEXT |
| STAT_PROP_VENTIL_HINTEN | unsigned char | Zustandswert Proportionalventil hinten |
| STAT_PROP_VENTIL_HINTEN_TEXT | string | Zustand Proportionalventil hinten table TAB_MR_STATUS_PROP_VENTILE TEXT |
| STAT_DC_MOTOR_HINTEN | unsigned char | Zustandswert DC-Motor hinten |
| STAT_DC_MOTOR_HINTEN_TEXT | string | Zustand DC-Motor hinten table TAB_MR_SAF_STATUS_DC_MOTOR TEXT |
| STAT_DC_MOTOR_HINTEN_MAX_HALL_COUNTS_WERT | unsigned int | Bei Vollkalibrierung ermittelte max. Anzahl von Hallsensor-Impulsen von Endanschlag bis Endanschlag (1500..6000 Impulse) |
| STAT_DC_MOTOR_HINTEN_MAX_HALL_COUNTS_EINH | string | Einheit fuer max. Anzahl Hallsensor Impulse |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fahrereinstellung-routine-start"></a>
### STEUERN_FAHREREINSTELLUNG_ROUTINE_START

Startet die Routine fuer die Fahrereinstellung KWP2000: $31 StartRoutineByLocalIdentifier $22 Fahrereinstellung Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SAF_FEDERVORSPANNUNG | string | Waehlt die Federrate table TAB_FEDERVORSPANNUNG_ARG TEXT |
| SAF_DAEMPFUNG | string | Waehlt die Daempfung table TAB_DAEMPFUNG_ARG TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fahrereinstellung-routine-results"></a>
### STEUERN_FAHREREINSTELLUNG_ROUTINE_RESULTS

Status der Routine fuer die Fahrereinstellung KWP2000: $33 RequestRoutineResultsByLocalIdentifier $22 Fahrereinstellung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SAF_FEDERVORSPANNUNG | unsigned char | Zustandswert der Federvorspannung |
| STAT_SAF_FEDERVORSPANNUNG_TEXT | string | Zustand der Federvorspannung table TAB_FEDERVORSPANNUNG TEXT |
| STAT_SAF_DAEMPFUNG | unsigned char | Zustandswert der Daempfung |
| STAT_SAF_DAEMPFUNG_TEXT | string | Zustand der Daempfung table TAB_DAEMPFUNG TEXT |
| STAT_SAF_SG | unsigned char | Zustandswert SAF Steuergeraet |
| STAT_SAF_SG_TEXT | string | Zustand SAF Steuergeraet table TAB_SAF_SG TEXT |
| _TEL_REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-racecal"></a>
### STATUS_RACECAL

Dieser Job liest den Status des Race Calibration Kits 0xE001 RACECAL_STAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RACECAL_DATA | binary | Aktueller Status des Race Calibration Kits als Bytearray Hinweise: - 4 Byte hex-Wert |
| STAT_RACECAL_DATA_EINH | string | Aktueller Status des Race Calibration Kits als Bytearray Hinweise: - 4 Byte hex-Wert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-racecal-damp-fac"></a>
### STATUS_RACECAL_DAMP_FAC

Dieser Job liest die Kalibrierungsdaten fuer die manuelle Verstellung der Zug-/Druckstufe 0xE002 RACECAL_DAMP_FAC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RACECAL_DAMP_DATA | binary | Kalibrierungsdaten fuer die manuelle Zug-/Druckstufe als Bytearray Hinweise: - 19 Byte hex Array |
| STAT_RACECAL_DAMP_DATA_EINH | string | Kalibrierungsdaten fuer die manuelle Zug-/Druckstufe als Bytearray Hinweise: - 19 Byte hex Array |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-racecal-wheel-inf"></a>
### STATUS_RACECAL_WHEEL_INF

Dieser Job liest die Kalibrierungsdaten fuer die montierte Reifen 0xE003 RACECAL_WHEEL_INF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RACECAL_WHEEL_DATA | binary | Kalibrierungsdaten fuer die montierte Reifen Hinweise: - 14 Byte hex Array |
| STAT_RACECAL_WHEEL_DATA_EINH | string | Kalibrierungsdaten fuer die montierte Reifen Hinweise: - 14 Byte hex Array |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-racecal-track"></a>
### STATUS_RACECAL_TRACK

Dieser Job liest die Kalibrierungsdaten fuer die Rennstrecke 0xE004 RACECAL_TRACK

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RACECAL_TRACK_DATA | binary | Kalibrierungsdaten fuer die Rennstrecke Hinweise: - 188 Byte hex Array |
| STAT_RACECAL_TRACK_DATA_EINH | string | Kalibrierungsdaten fuer die Rennstrecke Hinweise: - 188 Byte hex Array |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-racecal-shimming"></a>
### STATUS_RACECAL_SHIMMING

Dieser Job liest die Kalibrierungsdaten fuer e-Shimming 0xE005 RACECAL_SHIMMING

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RACECAL_SHIMMING_DATA | binary | Kalibrierungsdaten fuer e-Shimming Hinweise: - 74 Byte hex Array |
| STAT_RACECAL_SHIMMING_DATA_EINH | string | Kalibrierungsdaten fuer e-Shimming Hinweise: - 74 Byte hex Array |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-racecal-chksum"></a>
### STATUS_RACECAL_CHKSUM

Dieser Job liest die Checksumme der Kalibrierungsdaten 0xE006 RACECAL_CHKSUM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RACECAL_CHKSUM_DATA | binary | Checksumme der Kalibrierungsdaten Hinweise: - 2 Byte hex Array |
| STAT_RACECAL_CHKSUM_DATA_EINH | string | Checksumme der Kalibrierungsdaten Hinweise: - 2 Byte hex Array |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-racecal-info"></a>
### STATUS_RACECAL_INFO

Dieser Job liest die Informationen zum aktiven Datensatz 0xE007 RACECAL_INFO

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RACECAL_INFO_DATA | binary | Informationen zum aktiven Datensatz Hinweise: - 17 Byte hex Array |
| STAT_RACECAL_INFO_DATA_EINH | string | Informationen zum aktiven Datensatz Hinweise: - 17 Byte hex Array |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-racecal-hist"></a>
### STATUS_RACECAL_HIST

Dieser Job liest die Historie der Kalibrierungssaetze 0xE008 RACECAL_HIST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RACECAL_HIST_DATA | binary | Historie der Kalibrierungssaetze Hinweise: - 1 Byte hex |
| STAT_RACECAL_HIST_DATA_EINH | string | Historie der Kalibrierungssaetze Hinweise: - 1 Byte hex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-racecal-setup"></a>
### STATUS_RACECAL_SETUP

Dieser Job liest Verbauzustand des Federwegsensors vorne 0xE009 RACECAL_SETUP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SETUP_DATA | binary | Verbauzustand des Federwegsensors vorne Hinweise: - 1 Byte hex |
| STAT_SETUP_DATA_EINH | string | Verbauzustand des Federwegsensors vorne Hinweise: - 1 Byte hex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (133 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (5 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (93 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (90 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (56 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (21 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (20 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (19 × 9)
- [TAB_DAEMPFUNG](#table-tab-daempfung) (6 × 2)
- [TAB_DAEMPFUNG_ARG](#table-tab-daempfung-arg) (3 × 2)
- [TAB_FEDERVORSPANNUNG](#table-tab-federvorspannung) (8 × 2)
- [TAB_FEDERVORSPANNUNG_ARG](#table-tab-federvorspannung-arg) (5 × 2)
- [TAB_KALIBRIERUNGSART](#table-tab-kalibrierungsart) (2 × 2)
- [TAB_KALIBRIERUNGSSTATUS](#table-tab-kalibrierungsstatus) (4 × 2)
- [TAB_STATUS_DC_MOTOR](#table-tab-status-dc-motor) (9 × 2)
- [TAB_ROUTINESTATUS](#table-tab-routinestatus) (5 × 2)
- [TAB_PROPVENTILSTATUS](#table-tab-propventilstatus) (7 × 2)
- [TAB_SENSORKANAL](#table-tab-sensorkanal) (5 × 2)
- [TAB_SAF_SG](#table-tab-saf-sg) (4 × 2)
- [TAB_VENTIL_ANSTEUERUNG](#table-tab-ventil-ansteuerung) (7 × 2)
- [TAB_SUBFUNKTION_IO](#table-tab-subfunktion-io) (2 × 2)
- [TAB_MR_ESA_STATUS_KALIBRIERUNG](#table-tab-mr-esa-status-kalibrierung) (4 × 2)
- [TAB_WERT_SENSOR_1_VERSSP_ERR](#table-tab-wert-sensor-1-verssp-err) (18 × 2)
- [TAB_WERT_SENSOR_1_TYP](#table-tab-wert-sensor-1-typ) (4 × 2)
- [TAB_REASON_TASK_ERROR](#table-tab-reason-task-error) (3 × 2)
- [TAB_MR_LED_VERBAU_DC_HINTEN](#table-tab-mr-led-verbau-dc-hinten) (10 × 2)
- [TAB_MR_SENSORKANAL](#table-tab-mr-sensorkanal) (5 × 2)
- [TAB_ISTSTROM_DAEMPFER_VORNE_ERR](#table-tab-iststrom-daempfer-vorne-err) (18 × 2)
- [TAB_MR_SAF_PROPORTIONALVENTIL](#table-tab-mr-saf-proportionalventil) (7 × 2)
- [TAB_MR_VENTIL_ANSTEUERUNG](#table-tab-mr-ventil-ansteuerung) (7 × 2)
- [TAB_WERT_SENSOR1_ERR](#table-tab-wert-sensor1-err) (19 × 2)
- [TAB_MR_ROUTINE_SAF](#table-tab-mr-routine-saf) (5 × 2)
- [TAB_MR_SAF_STATUS_DC_MOTOR](#table-tab-mr-saf-status-dc-motor) (9 × 2)
- [TAB_MR_ART_KALIBRIERUNG_SAF](#table-tab-mr-art-kalibrierung-saf) (2 × 2)
- [TAB_MR_STAT_SAF_FREQ](#table-tab-mr-stat-saf-freq) (6 × 2)
- [TAB_FEHLER_KRITISCH](#table-tab-fehler-kritisch) (53 × 2)
- [TAB_WERT_SENSOR_1_KURVE](#table-tab-wert-sensor-1-kurve) (3 × 2)
- [TAB_MR_STATUS_PROP_VENTILE](#table-tab-mr-status-prop-ventile) (4 × 2)
- [TAB_ESA_SG](#table-tab-esa-sg) (4 × 2)
- [TAB_NUMBER_TASK_ERROR](#table-tab-number-task-error) (3 × 2)
- [TAB_MR_SAF_FREQ](#table-tab-mr-saf-freq) (5 × 2)
- [TAB_FEHLER_UNKRITISCH](#table-tab-fehler-unkritisch) (7 × 2)
- [M_DC_MOTOR1](#table-m-dc-motor1) (1 × 3)
- [M_SENSOR1](#table-m-sensor1) (1 × 3)
- [M_SENSOR2](#table-m-sensor2) (1 × 3)
- [M_SENSOR3](#table-m-sensor3) (1 × 3)
- [M_SWITCH1](#table-m-switch1) (1 × 3)
- [M_SENSOR4](#table-m-sensor4) (1 × 3)
- [M_SENSOR1_A](#table-m-sensor1-a) (1 × 3)
- [M_SENSOR2_A](#table-m-sensor2-a) (1 × 3)
- [M_SENSOR3_A](#table-m-sensor3-a) (1 × 3)
- [M_SENSOR4_A](#table-m-sensor4-a) (1 × 3)
- [M_ANALOG](#table-m-analog) (1 × 3)
- [TAB_KLEMME30_ERR](#table-tab-klemme30-err) (19 × 2)
- [TAB_SWITCH_X_ERROR](#table-tab-switch-x-error) (19 × 2)

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

Dimensions: 133 rows × 2 columns

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
| 0xB7 | SB LiMotive Germany GmbH |
| 0xB8 | KYOCERA Display Corporation |
| 0xB9 | MAGNA Powertrain AG & Co KG |
| 0xBA | BorgWarner |
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

Dimensions: 5 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x11 | TI_K2_NRSNS |
| 0x12 | TI_K2_NRSFNS |
| 0x22 | TI_K2_NRCNC |
| 0x77 | TI_K2_NRBTCE |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| - | BMW-FAST |
| - | KWP2000* |
| 1 | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 93 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x670C | Unterspannung Batterie |
| 0x670D | Überspannung Batterie |
| 0x670E | Failsafe Ebene 5: Hardware Failsafe |
| 0x670F | Failsafe Ebene 4: Federwegssensor Fehler |
| 0x6710 | Failsafe Ebene 3: reduziertes SAF-System |
| 0x6711 | Sensorabgleich fehlerhaft |
| 0x6712 | Neustart Ventilendstufe vorne durch Applikationssoftware |
| 0x6713 | Neustart Ventilendstufe hinten durch Applikationssoftware |
| 0x6714 | HL-SW_DTC7 |
| 0x6715 | HL-SW_DTC8 |
| 0x6716 | DC-Motor hinten: Vollkalibrierung fehlgeschlagen |
| 0x6717 | Federverstellung hinten: Position nicht erreicht |
| 0x6718 | Motor, Federverstellung hinten: Kurzschluss |
| 0x6719 | Motor, Federverstellung hinten: Leitungsunterbrechung |
| 0x671A | Motor, Federverstellung hinten:Übertemperatur |
| 0x671B | Proportionalventil hinten: Kurzschluss |
| 0x671C | Proportionalventil hinten: Leitungsunterbrechung |
| 0x671D | Proportionalventil Lenkung: Kurzschluss |
| 0x671E | Proportionalventil Lenkung: Leitungsunterbrechung |
| 0x671F | Proportionalventil vorne: Kurzschluss |
| 0x6720 | Proportionalventil vorne: Leitungsunterbrechung |
| 0x6721 | Sensor, Federverstellung hinten: elektrischer Fehler |
| 0x6722 | Federwegsensor vorne: Messwert hat Maximalwert überschritten |
| 0x6723 | Federwegsensor vorne: Messwert hat Minimalwert unterschritten |
| 0x6724 | Federwegsensor vorne: Messwert unplausibel |
| 0x6725 | Federwegsensor vorne: Nullpunkt nicht gelernt |
| 0x6726 | Federwegsensor vorne: Sensorparameter unplausibel |
| 0x6727 | Federwegsensor vorne: Versorgungsspannung zu niedrig |
| 0x6728 | Federwegsensor vorne: Versorgungsspannung zu hoch |
| 0x6729 | Federwegsensor hinten: Messwert hat Maximalwert überschritten |
| 0x672A | Federwegsensor hinten: Messwert hat Minimalwert unterschritten |
| 0x672B | Federwegsensor hinten: Nullpunkt nicht gelernt |
| 0x672C | Federwegsensor hinten: Messwert unplausibel |
| 0x672D | Federwegsensor hinten: Sensorparameter unplausibel |
| 0x672E | Federwegsensor hinten: Versorgungsspannung zu niedrig |
| 0x672F | Federwegsensor hinten: Versorgungsspannung zu hoch |
| 0x6730 | Beschleunigungssensor vorne: Messwert hat Maximalwert überschritten |
| 0x6731 | Beschleunigungssensor vorne: Messwert hat Minimalwert unterschritten |
| 0x6732 | Beschleunigungssensor vorne: Messwert unplausibel |
| 0x6733 | Beschleunigungssensor vorne: Sensorparameter unplausibel |
| 0x6734 | Beschleunigungssensor vorne: Nullpunkt nicht gelernt |
| 0x6735 | Beschleunigungssensor vorne: Versorgungsspannung zu niedrig |
| 0x6736 | Beschleunigungssensor vorne: Versorgungsspannung zu hoch |
| 0x6738 | Proportionalventil hinten: keine Endstufenfreigabe über Watchdog |
| 0x6739 | Proportionalventil hinten: Strommessung nicht kalibriert |
| 0x673B | Proportionalventil Lenkung: keine Endstufenfreigabe über Watchdog |
| 0x673C | Proportionalventil Lenkung: Strommessung nicht kalibriert |
| 0x673E | Proportionalventil vorne: keine Endstufenfreigabe über Watchdog |
| 0x673F | Proportionalventil vorne: Strommessung nicht kalibriert |
| 0x6745 | Radrehzahlsignal hinten: Sensorsignal unplausibel |
| 0x674A | Radrehzahlsignal vorne: Sensorsignal unplausibel |
| 0x674B | SAF-SG: Übertemperatur |
| 0x674E | Strommessung Lenkung:  Stromreglerplausibilitätsfehler |
| 0x6751 | Strommessung Proportionalventil  hinten:  Stromreglerplausibilitätsfehler |
| 0x6756 | Strommessung Proportionalventil vorne:  Stromreglerplausibilitätsfehler |
| 0x6757 | Taster1: Kurzschluss nach Masse |
| 0x6758 | Taster1: Kurzschluss nach UBatt oder nach 5VSupply |
| 0x6759 | Taster2: Kurzschluss nach Masse |
| 0x675A | Taster2: Kurzschluss nach UBatt oder nach 5VSupply |
| 0x675B | Produktionsmode aktiv |
| 0x675C | Beschleunigungssensor hinten: Messwert unplausibel |
| 0x675D | Beschleunigungssensor hinten: Messwert hat Maximalwert überschritten |
| 0x675E | Beschleunigungssensor hinten: Messwert hat Minimalwert unterschritten |
| 0x675F | Beschleunigungssensor hinten: Versorgungsspannung zu hoch |
| 0x6760 | Beschleunigungssensor hinten: Versorgungsspannung zu niedrig |
| 0x6761 | Beschleunigungssensor hinten: Nullpunkt nicht gelernt |
| 0x6762 | Beschleunigungssensor hinten: Sensorparameter unplausibel |
| 0x6768 | Hardwarefehler Steuergeraet |
| 0x6769 | Softwarefehler Steuergeraet |
| 0x676A | NVM_E_ERASE_FAILED |
| 0x676B | NVM_E_WRONG_CONFIG_ID |
| 0x676C | NVM_E_CONTROL_FAILED |
| 0x676D | NVM_E_READ_ALL_FAILED |
| 0x676E | NVM_E_WRITE_ALL_FAILED |
| 0x676F | NVM_E_WRITE_FAILED |
| 0x6770 | NVM_E_READ_FAILED |
| 0x6771 | Daempfer Testmodus aktiv |
| 0xD744 | ABS Zeitüberschreitung ABS_1_MOTBK |
| 0xD745 | ABS Zeitüberschreitung BRP_MOTBK |
| 0xD746 | BMSK Zeitüberschreitung DTC_DT_MOTBK |
| 0xD747 | BMSK Zeitüberschreitung DRDY_MOTBK |
| 0xD748 | ABS_ZFE_BMSK Zeitüberschreitung SPEED_MOTBK |
| 0xD749 | KOMBI  Zeitüberschreitung KOMBI_DATA_MOTBK |
| 0xD74A | BMSK  Zeitüberschreitung MOD_VEH_MOTBK |
| 0xD74B | BMSK  Zeitüberschreitung ENGINE_1_MOTBK |
| 0xD74C | BMSK  Zeitüberschreitung ENGINE_2_MOTBK |
| 0xD74D | SEB Zeitüberschreitung SEB_ID1_MOTBK |
| 0xD74E | SEB Zeitüberschreitung SEB_ID4_MOTBK |
| 0xD74F | ZFE_BMSK  Zeitüberschreitung ZFE_2_MOTBK |
| 0xD750 | CAN Bus Off |
| 0xD751 | KOMBI Zeitüberschreitung CTR_SUSPD_AD_MOTBK |
| 0xD752 | KOMBI Zeitüberschreitung AUINF_S_MOTBK |
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

Dimensions: 90 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x670C | 0x01 | 0x03 | 0x04 | - |
| 0x670D | 0x01 | 0x03 | 0x04 | - |
| 0x670E | 0x01 | - | - | - |
| 0x670F | 0x01 | - | - | - |
| 0x6710 | 0x01 | - | - | - |
| 0x6711 | 0x01 | - | - | - |
| 0x6712 | 0x01 | - | - | - |
| 0x6713 | 0x01 | - | - | - |
| 0x6714 | 0x01 | - | - | - |
| 0x6715 | 0x01 | - | - | - |
| 0x6716 | 0x01 | 0x03 | 0x24 | M_DC_MOTOR1 |
| 0x6717 | 0x01 | 0x03 | 0x24 | M_DC_MOTOR1 |
| 0x6718 | 0x01 | 0x03 | 0x24 | M_DC_MOTOR1 |
| 0x6719 | 0x01 | 0x03 | 0x24 | M_DC_MOTOR1 |
| 0x671A | 0x01 | 0x03 | 0x24 | M_DC_MOTOR1 |
| 0x671B | 0x01 | 0x1C | 0x1D | 0x1E |
| 0x671C | 0x01 | 0x1C | 0x1D | 0x1E |
| 0x671D | 0x01 | 0x1F | 0x20 | 0x21 |
| 0x671E | 0x01 | 0x1F | 0x20 | 0x21 |
| 0x671F | 0x01 | 0x19 | 0x1A | 0x1B |
| 0x6720 | 0x01 | 0x19 | 0x1A | 0x1B |
| 0x6721 | 0x01 | 0x03 | 0x27 | 0x28 |
| 0x6722 | 0x01 | M_SENSOR1_A | 0x0F | M_SENSOR1 |
| 0x6723 | 0x01 | M_SENSOR1_A | 0x0F | M_SENSOR1 |
| 0x6724 | 0x01 | M_SENSOR1_A | 0x0F | M_SENSOR1 |
| 0x6725 | 0x01 | M_SENSOR1_A | 0x0F | M_SENSOR1 |
| 0x6726 | 0x01 | M_SENSOR1_A | 0x0F | M_SENSOR1 |
| 0x6727 | 0x01 | M_SENSOR1_A | 0x0F | M_SENSOR1 |
| 0x6728 | 0x01 | M_SENSOR1_A | 0x0F | M_SENSOR1 |
| 0x6729 | 0x01 | M_SENSOR2_A | 0x14 | M_SENSOR2 |
| 0x672A | 0x01 | M_SENSOR2_A | 0x14 | M_SENSOR2 |
| 0x672B | 0x01 | M_SENSOR2_A | 0x14 | M_SENSOR2 |
| 0x672C | 0x01 | M_SENSOR2_A | 0x14 | M_SENSOR2 |
| 0x672D | 0x01 | M_SENSOR2_A | 0x14 | M_SENSOR2 |
| 0x672E | 0x01 | M_SENSOR2_A | 0x14 | M_SENSOR2 |
| 0x672F | 0x01 | M_SENSOR2_A | 0x14 | M_SENSOR2 |
| 0x6730 | 0x01 | M_SENSOR3_A | 0x2F | M_SENSOR3 |
| 0x6731 | 0x01 | M_SENSOR3_A | 0x2F | M_SENSOR3 |
| 0x6732 | 0x01 | M_SENSOR3_A | 0x2F | M_SENSOR3 |
| 0x6734 | 0x01 | M_SENSOR3_A | 0x2F | M_SENSOR3 |
| 0x6735 | 0x01 | M_SENSOR3_A | 0x2F | M_SENSOR3 |
| 0x6736 | 0x01 | M_SENSOR3_A | 0x2F | M_SENSOR3 |
| 0x6738 | 0x01 | 0x1C | 0x1D | 0x1E |
| 0x6739 | 0x01 | 0x1C | 0x1D | 0x1E |
| 0x673B | 0x01 | 0x1F | 0x20 | 0x21 |
| 0x673C | 0x01 | 0x1F | 0x20 | 0x21 |
| 0x673E | 0x01 | 0x19 | 0x1A | 0x1B |
| 0x673F | 0x01 | 0x19 | 0x1A | 0x1B |
| 0x6745 | 0x01 | 0x03 | 0x29 | 0x2A |
| 0x674A | 0x01 | 0x03 | 0x29 | 0x2A |
| 0x674B | 0x01 | 0x22 | 0x23 | - |
| 0x674E | 0x01 | 0x1F | 0x20 | 0x21 |
| 0x6751 | 0x01 | 0x1C | 0x1D | 0x1E |
| 0x6756 | 0x01 | 0x19 | 0x1A | 0x1B |
| 0x6757 | M_ANALOG | 0x2C | 0x2D | 0x2E |
| 0x6758 | M_ANALOG | 0x2C | 0x2D | 0x2E |
| 0x6759 | M_ANALOG | 0x2C | 0x2D | 0x2E |
| 0x675A | M_ANALOG | 0x2C | 0x2D | 0x2E |
| 0x675B | 0x01 | - | - | - |
| 0x675C | 0x01 | M_SENSOR4_A | 0x34 | M_SENSOR4 |
| 0x675D | 0x01 | M_SENSOR4_A | 0x34 | M_SENSOR4 |
| 0x675E | 0x01 | M_SENSOR4_A | 0x34 | M_SENSOR4 |
| 0x675F | 0x01 | M_SENSOR4_A | 0x34 | M_SENSOR4 |
| 0x6760 | 0x01 | M_SENSOR4_A | 0x34 | M_SENSOR4 |
| 0x6761 | 0x01 | M_SENSOR4_A | 0x34 | M_SENSOR4 |
| 0x6762 | 0x01 | M_SENSOR4_A | 0x34 | M_SENSOR4 |
| 0x676A | 0x01 | - | - | - |
| 0x676B | 0x01 | - | - | - |
| 0x676C | 0x01 | - | - | - |
| 0x676D | 0x01 | - | - | - |
| 0x676E | 0x01 | - | - | - |
| 0x676F | 0x01 | - | - | - |
| 0x6770 | 0x01 | - | - | - |
| 0x6771 | 0x01 | - | - | - |
| 0xD744 | 0x01 | - | - | - |
| 0xD745 | 0x01 | - | - | - |
| 0xD746 | 0x01 | - | - | - |
| 0xD747 | 0x01 | - | - | - |
| 0xD748 | 0x01 | - | - | - |
| 0xD749 | 0x01 | - | - | - |
| 0xD74A | 0x01 | - | - | - |
| 0xD74B | 0x01 | - | - | - |
| 0xD74D | 0x01 | - | - | - |
| 0xD74E | 0x01 | - | - | - |
| 0xD74F | 0x01 | - | - | - |
| 0xD750 | 0x01 | - | - | - |
| 0x6768 | 0x01 | 0x22 | 0x23 | - |
| 0x6769 | 0x01 | 0x22 | 0x23 | - |
| 0xD751 | 0x01 | - | - | - |
| 0xD752 | 0x01 | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 56 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | STAT_SYSTEMZEIT_WERT | s | high | signed long | - | 1 | 1 | 0 |
| 0x02 | STAT_KM_STAND | km | high | signed long | - | 1 | 1 | 0 |
| 0x03 | KLEMME30 | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x04 | KLEMME30_ERR | 0-n | high | 0xFFFF | TAB_KLEMME30_ERR | - | - | - |
| 0x05 | WERT_SENSOR_1 | V | high | unsigned int | - | 1.0 | 1000 | 0 |
| 0x06 | WERT_SENSOR_1_TYP | 0-n | high | 0xFF | TAB_WERT_SENSOR_1_TYP | - | - | - |
| 0x07 | WERT_SENSOR_1_KURVE | 0-n | high | 0xFF | TAB_WERT_SENSOR_1_KURVE | - | - | - |
| 0x08 | WERT_SENSOR_1_ERR | 0-n | high | 0xFFFF | TAB_WERT_SENSOR1_ERR | - | - | - |
| 0x09 | WERT_SENSOR_1_VERSSP_ERR | 0-n | high | 0xFFFF | TAB_WERT_SENSOR_1_VERSSP_ERR | - | - | - |
| 0x0A | WERT_SENSOR_2 | V | high | unsigned int | - | 1.0 | 1000 | 0 |
| 0x0B | WERT_SENSOR_2_TYP | 0-n | high | 0xFF | TAB_WERT_SENSOR_1_TYP | - | - | - |
| 0x0C | WERT_SENSOR_2_KURVE | 0-n | high | 0xFF | TAB_WERT_SENSOR_1_KURVE | - | - | - |
| 0x0D | WERT_SENSOR_2_ERR | 0-n | high | 0xFFFF | TAB_WERT_SENSOR1_ERR | - | - | - |
| 0x0E | WERT_SENSOR_2_VERSSP_ERR | 0-n | high | 0xFFFF | TAB_WERT_SENSOR_1_VERSSP_ERR | - | - | - |
| 0x0F | WERT_SENSOR_1 | V | high | unsigned int | - | 1.0 | 1000 | 0 |
| 0x10 | WERT_SENSOR_1_TYP | 0-n | high | 0xFF00 | TAB_WERT_SENSOR_1_TYP | - | - | - |
| 0x11 | WERT_SENSOR_1_KURVE | 0-n | high | 0x00FF | TAB_WERT_SENSOR_1_KURVE | - | - | - |
| 0x12 | WERT_SENSOR_1_ERR | 0-n | high | 0xFFFF0000 | TAB_WERT_SENSOR1_ERR | - | - | - |
| 0x13 | WERT_SENSOR_1_VERSSP_ERR | 0-n | high | 0x0000FFFF | TAB_WERT_SENSOR_1_VERSSP_ERR | - | - | - |
| 0x14 | WERT_SENSOR_2 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x15 | WERT_SENSOR_2_TYP | 0-n | high | 0xFF00 | TAB_WERT_SENSOR_1_TYP | - | - | - |
| 0x16 | WERT_SENSOR_2_KURVE | 0-n | high | 0x00FF | TAB_WERT_SENSOR_1_KURVE | - | - | - |
| 0x17 | WERT_SENSOR_2_ERR | 0-n | high | 0xFFFF0000 | TAB_WERT_SENSOR1_ERR | - | - | - |
| 0x18 | WERT_SENSOR_2_VERSSP_ERR | 0-n | high | 0x0000FFFF | TAB_WERT_SENSOR_1_VERSSP_ERR | - | - | - |
| 0x19 | ISTSTROM_DAEMPFER_VORNE | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x1A | SOLLSTROM_DAEMPFER_VORNE | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x1B | ISTSTROM_DAEMPFER_VORNE_ERR | 0-n | High | 0xFFFF | TAB_ISTSTROM_DAEMPFER_VORNE_ERR | - | - | - |
| 0x1C | ISTSTROM_DAEMPFER_HINTEN | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x1D | SOLLSTROM_DAEMPFER_HINTEN | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x1E | ISTSTROM_DAEMPFER_HINTEN_ERR | 0-n | High | 0xFFFF | TAB_ISTSTROM_DAEMPFER_VORNE_ERR | - | - | - |
| 0x1F | ISTSTROM_DAEMPFER_LENKUNG | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x20 | SOLLSTROM_DAEMPFER_LENKUNG | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x21 | ISTSTROM_DAEMPFER_LENKUNG_ERR | 0-n | High | 0xFFFF | TAB_ISTSTROM_DAEMPFER_VORNE_ERR | - | - | - |
| 0x22 | FEHLER_KRITISCH | 0-n | High | 0xFFFF | TAB_FEHLER_KRITISCH | - | - | - |
| 0x23 | FEHLER_UNKRITISCH | 0-n | High | 0xFFFFFFFF | TAB_FEHLER_UNKRITISCH | - | - | - |
| 0x24 | DC_MOTOR_STROM | A | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x25 | DC_MOTOR_IST_POSITION | Inkremente | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x26 | DC_MOTOR_SOLL_POSITION | Inkremente | High | unsigned int | - | 1.0 | 1.0 | 0.0 |
| 0x27 | HALL_SENSOR_1_SPANNUNG | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x28 | HALL_SENSOR_2_SPANNUNG | V | High | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x29 | WHEEL_FRONT_TOOTH_TIME | s | High | unsigned int | - | 1.0 | 1000000.0 | 0.0 |
| 0x2A | WHEEL_REAR_TOOTH_TIME | s | High | unsigned int | - | 1.0 | 1000000.0 | 0.0 |
| 0x2B | SWITCH_1_VOLTAGE | V | high | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x2C | SWITCH_1_ERROR | 0-n | high | 0xFFFF | TAB_SWITCH_X_ERROR | - | - | - |
| 0x2D | SWITCH_2_VOLTAGE | V | high | unsigned int | - | 1.0 | 1000.0 | 0.0 |
| 0x2E | SWITCH_2_ERROR | 0-n | high | 0xFFFF | TAB_SWITCH_X_ERROR | - | - | - |
| 0x2F | WERT_SENSOR_3 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x30 | WERT_SENSOR_3_TYP | 0-n | high | 0xFF00 | TAB_WERT_SENSOR_1_TYP | - | - | - |
| 0x31 | WERT_SENSOR_3_KURVE | 0-n | high | 0x00FF | TAB_WERT_SENSOR_1_KURVE | - | - | - |
| 0x32 | WERT_SENSOR_3_ERR | 0-n | high | 0xFFFF0000 | TAB_WERT_SENSOR1_ERR | - | - | - |
| 0x33 | WERT_SENSOR_3_VERSSP_ERR | 0-n | high | 0x0000FFFF | TAB_WERT_SENSOR_1_VERSSP_ERR | - | - | - |
| 0x34 | WERT_SENSOR_4 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x35 | WERT_SENSOR_4_TYP | 0-n | high | 0xFF00 | TAB_WERT_SENSOR_1_TYP | - | - | - |
| 0x36 | WERT_SENSOR_4_KURVE | 0-n | high | 0x00FF | TAB_WERT_SENSOR_1_KURVE | - | - | - |
| 0x37 | WERT_SENSOR_4_ERR | 0-n | high | 0xFFFF0000 | TAB_WERT_SENSOR1_ERR | - | - | - |
| 0x38 | WERT_SENSOR_4_VERSSP_ERR | 0-n | high | 0x0000FFFF | TAB_WERT_SENSOR_1_VERSSP_ERR | - | - | - |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 21 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x673A | Proportionalventil hinten: Ventilfehler bei Onlineprüfung |
| 0x673D | Proportionalventil Lenkung: Ventilfehler bei Onlineprüfung |
| 0x6740 | Proportionalventil vorne: Ventilfehler bei Onlineprüfung |
| 0x6763 | Exception-Fehler |
| 0x6764 | Task-Fehler |
| 0x6765 | LL-Check-Fehler |
| 0x6766 | SEK Unterspannung Batterie |
| 0x6767 | SEK Ueberspannung Batterie |
| 0xD75D | SEK ABS Zeitüberschreitung ABS_1_MOTBK |
| 0xD75E | SEK ABS Zeitüberschreitung BRP_MOTBK |
| 0xD753 | SEK BMSK Zeitüberschreitung DTC_DT_MOTBK |
| 0xD754 | SEK BMSK Zeitüberschreitung DRDY_MOTBK |
| 0xD755 | SEK ABS_ZFE_BMSK Zeitüberschreitung SPEED_MOTBK |
| 0xD756 | SEK KOMBI  Zeitüberschreitung KOMBI_DATA_MOTBK |
| 0xD757 | SEK BMSK  Zeitüberschreitung MOD_VEH_MOTBK |
| 0xD758 | SEK BMSK  Zeitüberschreitung ENGINE_1_MOTBK |
| 0xD759 | SEK BMSK  Zeitüberschreitung ENGINE_2_MOTBK |
| 0xD75A | SEK SEB Zeitüberschreitung SEB_ID1_MOTBK |
| 0xD75B | SEK SEB Zeitüberschreitung SEB_ID4_MOTBK |
| 0xD75C | SEK ZFE_BMSK  Zeitüberschreitung ZFE_2_MOTBK |
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

Dimensions: 20 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x673A | 0x01 | 0x1C | 0x1D | 0x1E |
| 0x673D | 0x01 | 0x1F | 0x20 | 0x21 |
| 0x6740 | 0x01 | 0x19 | 0x1A | 0x1B |
| 0x6763 | 0x01 | 0x05 | 0x07 | - |
| 0x6764 | 0x01 | 0x08 | 0x09 | 0x0A |
| 0x6765 | 0x01 | 0x05 | 0x06 | - |
| 0x6766 | 0x01 | 0x03 | 0x04 | - |
| 0x6767 | 0x01 | 0x03 | 0x04 | - |
| 0xD751 | 0x01 | - | - | - |
| 0xD752 | 0x01 | - | - | - |
| 0xD753 | 0x01 | - | - | - |
| 0xD754 | 0x01 | - | - | - |
| 0xD755 | 0x01 | - | - | - |
| 0xD756 | 0x01 | - | - | - |
| 0xD757 | 0x01 | - | - | - |
| 0xD758 | 0x01 | - | - | - |
| 0xD759 | 0x01 | - | - | - |
| 0xD75A | 0x01 | - | - | - |
| 0xD75B | 0x01 | - | - | - |
| 0xD75C | 0x01 | - | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 19 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | STAT_SYSTEMZEIT_WERT | s | high | signed long | - | 1 | 1 | 0 |
| 0x02 | STAT_KM_STAND | km | high | signed long | - | 1 | 1 | 0 |
| 0x03 | KLEMME30 | V | - | unsigned char | - | 1 | 10 | 0 |
| 0x04 | KLEMME30_ERR | 0-n | high | 0xFFFF | TAB_KLEMME30_ERR | - | - | - |
| 0x05 | FEHLER_KRITISCH | 0-n | High | 0xFFFF | TAB_FEHLER_KRITISCH | - | - | - |
| 0x06 | FEHLER_UNKRITISCH | 0-n | High | 0xFFFFFFFF | TAB_FEHLER_UNKRITISCH | - | - | - |
| 0x07 | EXCEPTION_ADRESSE | hex | - | signed long | - | - | - | - |
| 0x08 | WCET_TASK_ERROR | µs | high | unsigned int | - | 1 | 1 | 0 |
| 0x09 | NUMBER_TASK_ERROR | 0-n | high | 0xFF | TAB_NUMBER_TASK_ERROR | - | - | - |
| 0x0A | REASON_TASK_ERROR | 0-n | high | 0xFF | TAB_REASON_TASK_ERROR | - | - | - |
| 0x1C | ISTSTROM_DAEMPFER_HINTEN | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x1D | SOLLSTROM_DAEMPFER_HINTEN | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x1E | ISTSTROM_DAEMPFER_HINTEN_ERR | 0-n | High | 0xFFFF | TAB_ISTSTROM_DAEMPFER_VORNE_ERR | - | - | - |
| 0x19 | ISTSTROM_DAEMPFER_VORNE | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x1A | SOLLSTROM_DAEMPFER_VORNE | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x1B | ISTSTROM_DAEMPFER_VORNE_ERR | 0-n | High | 0xFFFF | TAB_ISTSTROM_DAEMPFER_VORNE_ERR | - | - | - |
| 0x1F | ISTSTROM_DAEMPFER_LENKUNG | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x20 | SOLLSTROM_DAEMPFER_LENKUNG | A | High | unsigned int | - | 1 | 1000 | 0 |
| 0x21 | ISTSTROM_DAEMPFER_LENKUNG_ERR | 0-n | High | 0xFFFF | TAB_ISTSTROM_DAEMPFER_VORNE_ERR | - | - | - |

<a id="table-tab-daempfung"></a>
### TAB_DAEMPFUNG

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Verstellung laeuft |
| 0x01 | Komfort |
| 0x02 | Normal |
| 0x03 | Sport |
| 0x04 | nicht verbaut |
| 0xFF | undefiniert |

<a id="table-tab-daempfung-arg"></a>
### TAB_DAEMPFUNG_ARG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Komfort |
| 0x02 | Normal |
| 0x03 | Sport |

<a id="table-tab-federvorspannung"></a>
### TAB_FEDERVORSPANNUNG

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Verstellung laeuft |
| 0x01 | Einzelfahrer |
| 0x02 | Beladen |
| 0x03 | Sozius |
| 0x04 | Gelaende1 |
| 0x05 | Gelaende2 |
| 0x06 | nicht verbaut |
| 0xFF | nicht definiert |

<a id="table-tab-federvorspannung-arg"></a>
### TAB_FEDERVORSPANNUNG_ARG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Einzelfahrer |
| 0x02 | Beladen |
| 0x03 | Sozius |
| 0x04 | Gelaende1 |
| 0x05 | Gelaende2 |

<a id="table-tab-kalibrierungsart"></a>
### TAB_KALIBRIERUNGSART

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Vollkalibrierung DC-Motor hinten |
| 0x01 | Rekalibrierung DC-Motor hinten |

<a id="table-tab-kalibrierungsstatus"></a>
### TAB_KALIBRIERUNGSSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kalibrierung Federbein laeuft |
| 0x01 | Fehler Kalibrierung |
| 0x02 | Kalibrierung Federbein erfolgreich |
| 0xFF | ungueltig |

<a id="table-tab-status-dc-motor"></a>
### TAB_STATUS_DC_MOTOR

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Verstellung laeuft |
| 0x01 | Wiederholter Versuch aktiv |
| 0x02 | Position erreicht |
| 0x03 | Motorposition nicht im Zielfenster |
| 0x04 | Motor nicht verbaut |
| 0x05 | Motor deaktiviert |
| 0x06 | Motor zu heiss |
| 0x07 | Fehler vorhanden |
| 0xFF | ungueltig |

<a id="table-tab-routinestatus"></a>
### TAB_ROUTINESTATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Routine nicht beendet |
| 0x01 | Routine erfolgreich beendet |
| 0x02 | Routine nicht erfolgreich beendet |
| 0x03 | Routine abgebrochen |
| 0xFF | ungueltig |

<a id="table-tab-propventilstatus"></a>
### TAB_PROPVENTILSTATUS

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Zielfenster des Stroms erreicht |
| 0x01 | Zielfenster des Stroms nicht erreicht |
| 0x02 | Proportionalventil nicht verbaut |
| 0x03 | Proportionalventil nicht aktiviert |
| 0x04 | Kurzschluss |
| 0x05 | Leitungsbruch |
| 0xFF | ungueltig |

<a id="table-tab-sensorkanal"></a>
### TAB_SENSORKANAL

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AIN1..AIN4 |
| 0x01 | AIN1 |
| 0x02 | AIN2 |
| 0x03 | AIN3 |
| 0x04 | AIN4 |

<a id="table-tab-saf-sg"></a>
### TAB_SAF_SG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | reserviert |
| 0x01 | SAF in Ordnung |
| 0x02 | SAF defekt: Systemfehler vorhanden |
| 0xFF | undefiniert |

<a id="table-tab-ventil-ansteuerung"></a>
### TAB_VENTIL_ANSTEUERUNG

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Lenkung |
| 0x01 | Daempfung vorne |
| 0x02 | Daempfung hinten |
| 0x03 | Lenkung und Daempfung vorne |
| 0x04 | Lenkung und Daempfung hinten |
| 0x05 | Daempfung vorne und hinten |
| 0x06 | Alle Proportionalventile |

<a id="table-tab-subfunktion-io"></a>
### TAB_SUBFUNKTION_IO

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | returnControlToECU |
| 0x07 | shortTermAdjustment |

<a id="table-tab-mr-esa-status-kalibrierung"></a>
### TAB_MR_ESA_STATUS_KALIBRIERUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kalibrierung Federbein laeuft |
| 0x01 | Fehler Kalibrierung |
| 0x02 | Kalibrierung Federbein erfolgreich |
| 0xFF | ungültig |

<a id="table-tab-wert-sensor-1-verssp-err"></a>
### TAB_WERT_SENSOR_1_VERSSP_ERR

Dimensions: 18 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | kein Fehler festgestellt |
| 0x00000001 | Signal zu hoch |
| 0x00000002 | Signal zu niedrig |
| 0x00000004 | reserviert |
| 0x00000008 | reserviert |
| 0x00000010 | reserviert |
| 0x00000020 | reserviert |
| 0x00000040 | reserviert |
| 0x00000080 | reserviert |
| 0x00000100 | reserviert |
| 0x00000200 | reserviert |
| 0x00000400 | reserviert |
| 0x00000800 | reserviert |
| 0x00001000 | reserviert |
| 0x00002000 | reserviert |
| 0x00004000 | reserviert |
| 0x00008000 | reserviert |
| 0xFFFFFFFF | manuell auswerten |

<a id="table-tab-wert-sensor-1-typ"></a>
### TAB_WERT_SENSOR_1_TYP

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | ungültig |
| 0x0100 | Beschleunigungssensor |
| 0x0200 | Höhenstandssensor |
| 0xFFFF | nicht definiert |

<a id="table-tab-reason-task-error"></a>
### TAB_REASON_TASK_ERROR

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | WCET Überschreitung |
| 0x01 | Taskausfall |
| 0xFF | ungültiger Wert |

<a id="table-tab-mr-led-verbau-dc-hinten"></a>
### TAB_MR_LED_VERBAU_DC_HINTEN

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Verstellung zur Soll-Position laeuft |
| 0x01 | Wiederholter Versuch aktiv |
| 0x02 | Soll-Position erreicht |
| 0x03 | Motorposiition nicht im Zielfenster |
| 0x04 | Ersatzposition: Abgestimmtes Fahrwerk bei Fehler |
| 0x05 | Motor nicht verbaut |
| 0x06 | Motor deaktiviert |
| 0x07 | Motor zu heiss |
| 0x08 | Fehler vorhanden |
| 0xFF | ungültig |

<a id="table-tab-mr-sensorkanal"></a>
### TAB_MR_SENSORKANAL

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AIN1..AIN4 |
| 0x01 | AIN1 |
| 0x02 | AIN2 |
| 0x03 | AIN3 |
| 0x04 | AIN4 |

<a id="table-tab-iststrom-daempfer-vorne-err"></a>
### TAB_ISTSTROM_DAEMPFER_VORNE_ERR

Dimensions: 18 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | kein Fehler festgestellt |
| 0x0001 | Ventil Kurzschluss nach KL30 |
| 0x0002 | Ventil Kurzschluss nach KL31 |
| 0x0004 | Ventil offene Leitung |
| 0x0008 | Ventil Kurzschluss |
| 0x0010 | reserviert |
| 0x0020 | Ventilstrommessung nicht kalibriert |
| 0x0040 | reserviert |
| 0x0080 | reserviert |
| 0x0100 | allgemeiner Ventilfehler bei Onlinepruefung |
| 0x0200 | Hochlaufpruefung nicht durchgefuehrt |
| 0x0400 | Stromplausibilitaetsfehler |
| 0x0800 | reserviert |
| 0x1000 | reserviert |
| 0x2000 | reserviert |
| 0x4000 | reserviert |
| 0x8000 | reserviert |
| 0xFFFF | manuell auswerten |

<a id="table-tab-mr-saf-proportionalventil"></a>
### TAB_MR_SAF_PROPORTIONALVENTIL

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Zielfenster des Stromes erreicht |
| 0x01 | Zielfenster des Stromes nicht erreicht |
| 0x02 | Proportionalventil nicht verbaut |
| 0x03 | Proportionalventil nicht aktiviert |
| 0x04 | Kurzschluss |
| 0x05 | Leitungsbruch |
| 0xFF | ungültig |

<a id="table-tab-mr-ventil-ansteuerung"></a>
### TAB_MR_VENTIL_ANSTEUERUNG

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Lenkung |
| 0x01 | Daempfung vorne |
| 0x02 | Daempfung hinten |
| 0x03 | Lenkung und Daempfung vorne |
| 0x04 | Lenkung und Daempfung hinten |
| 0x05 | Daempfung vorne und hinten |
| 0x06 | Alle Proportionalventile |

<a id="table-tab-wert-sensor1-err"></a>
### TAB_WERT_SENSOR1_ERR

Dimensions: 19 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | kein Fehler festgestellt |
| 0x00010000 | Signal zu hoch |
| 0x00020000 | Signal zu niedrig |
| 0x00040000 | reserviert |
| 0x00080000 | reserviert |
| 0x00100000 | reserviert |
| 0x00200000 | Sensorparameter nicht codiert |
| 0x00400000 | Sensoreinbaulage nicht gelernt |
| 0x00600000 | Sensorparameter nicht codiert und Sensoreinbaulage nicht gelernt |
| 0x00800000 | reserviert |
| 0x01000000 | reserviert |
| 0x02000000 | reserviert |
| 0x04000000 | reserviert |
| 0x08000000 | reserviert |
| 0x10000000 | reserviert |
| 0x20000000 | reserviert |
| 0x40000000 | reserviert |
| 0x80000000 | reserviert |
| 0xFFFFFFFF | manuell auswerten |

<a id="table-tab-mr-routine-saf"></a>
### TAB_MR_ROUTINE_SAF

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Routine nicht beendet |
| 0x01 | Routine erfolgreich beendet |
| 0x02 | Routine nicht erfolgreich beendet |
| 0x03 | Routine abgebrochen |
| 0xFF | Ungültig |

<a id="table-tab-mr-saf-status-dc-motor"></a>
### TAB_MR_SAF_STATUS_DC_MOTOR

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Verstellung laeuft |
| 0x01 | Wiederholter Versuch aktiv |
| 0x02 | Position erreicht |
| 0x03 | Motorposiition nicht im Zielfenster |
| 0x04 | Motor nicht verbaut |
| 0x05 | Motor deaktiviert |
| 0x06 | Motor zu heiss |
| 0x07 | Fehler vorhanden |
| 0xFF | ungültig |

<a id="table-tab-mr-art-kalibrierung-saf"></a>
### TAB_MR_ART_KALIBRIERUNG_SAF

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Vollkalibrierung DC-Motor hinten |
| 0x01 | Rekalibrierung DC-Motor hinten |

<a id="table-tab-mr-stat-saf-freq"></a>
### TAB_MR_STAT_SAF_FREQ

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 400 Hz |
| 0x01 | 800 Hz |
| 0x02 | 1200 Hz |
| 0x03 | 1600 Hz |
| 0x04 | 2000 Hz |
| 0xFF | ungueltig |

<a id="table-tab-fehler-kritisch"></a>
### TAB_FEHLER_KRITISCH

Dimensions: 53 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | kein Fehler festgestellt |
| 0x03 | ADC-Fehler |
| 0x04 | ALU-Fehler |
| 0x05 | Core-Spg.-Fehler |
| 0x07 | TLE Fehler |
| 0x08 | Watchdog Fehler |
| 0x28 | Taskfehler |
| 0x30 | Reset-unbekannte Ursache/unerwartet |
| 0x31 | External Reset (keine Anwendung im ICM-V, da keine Unterscheidung der Ursache möglich) |
| 0x32 | Loss-of-Lock-Reset |
| 0x33 | Loss-of-Clock-Reset |
| 0x34 | CPU WD Reset/Debug-Reset (keine Anwendung im ICM-V) |
| 0x36 | Checkstop-Reset |
| 0x37 | Software-System-Reset (keine Anwendung im ICM-V) |
| 0x38 | Software-external-Reset (keine Anwendung im ICM-V) |
| 0x40 | reserviert |
| 0x41 | Maschine-Check |
| 0x42 | Data-Storage |
| 0x43 | Instruction-Storage |
| 0x44 | External Interupt |
| 0x45 | Alignment |
| 0x46 | Program |
| 0x47 | Floating-point unavailbale |
| 0x48 | System-Call |
| 0x49 | AP unavailable |
| 0x4A | Dekrementer |
| 0x4B | Fixed Interval Timer |
| 0x4C | Watchdog Timer |
| 0x4D | Data TLB Error |
| 0x4E | Instruction TLB Error |
| 0x4F | Debug |
| 0x50 | reserviert |
| 0x51 | reserviert |
| 0x52 | reserviert |
| 0x53 | reserviert |
| 0x54 | reserviert |
| 0x55 | reserviert |
| 0x56 | reserviert |
| 0x57 | reserviert |
| 0x58 | reserviert |
| 0x59 | reserviert |
| 0x5A | reserviert |
| 0x5B | reserviert |
| 0x5C | reserviert |
| 0x5D | reserviert |
| 0x5E | reserviert |
| 0x5F | reserviert |
| 0x60 | SPE unavailbale Exc |
| 0x61 | SPE Data Exc |
| 0x69 | Deadline |
| 0x6B | Stack-Fehler |
| 0x70 | unbekannter OS-Fehler |
| 0xFF | manuell auswerten |

<a id="table-tab-wert-sensor-1-kurve"></a>
### TAB_WERT_SENSOR_1_KURVE

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Kurve1 |
| 0x0001 | Kurve2 |
| 0xFFFF | Nicht definiert |

<a id="table-tab-mr-status-prop-ventile"></a>
### TAB_MR_STATUS_PROP_VENTILE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Sollstrom erreicht |
| 0x01 | Proportionalventil deaktiviert |
| 0x02 | Fehler vorhanden |
| 0x03 | ungueltig |

<a id="table-tab-esa-sg"></a>
### TAB_ESA_SG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | reserviert |
| 0x01 | ESA in Ordnung |
| 0x02 | ESA defekt: Systemfehler vorhanden |
| 0xFF | undefiniert |

<a id="table-tab-number-task-error"></a>
### TAB_NUMBER_TASK_ERROR

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 10ms-Task |
| 0x01 | 2.5ms-Task |
| 0xFF | ungültiger Wert |

<a id="table-tab-mr-saf-freq"></a>
### TAB_MR_SAF_FREQ

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 400 Hz |
| 0x01 | 800 Hz |
| 0x02 | 1200 Hz |
| 0x03 | 1600 Hz |
| 0x04 | 2000 Hz |

<a id="table-tab-fehler-unkritisch"></a>
### TAB_FEHLER_UNKRITISCH

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | kein Fehler festgestellt |
| 0x00000001 | BUS_OFF |
| 0x00000002 | Task_Check_WCET |
| 0x00000004 | EEP-Driver-Failure |
| 0x00000008 | ROM-Check-Failure |
| 0x00000010 | No-Coding-Data |
| 0xFFFFFFFF | manuell auswerten |

<a id="table-m-dc-motor1"></a>
### M_DC_MOTOR1

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x26 | 0x25 |

<a id="table-m-sensor1"></a>
### M_SENSOR1

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x12 | 0x13 |

<a id="table-m-sensor2"></a>
### M_SENSOR2

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x17 | 0x18 |

<a id="table-m-sensor3"></a>
### M_SENSOR3

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x32 | 0x33 |

<a id="table-m-switch1"></a>
### M_SWITCH1

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x2D | 0x2E |

<a id="table-m-sensor4"></a>
### M_SENSOR4

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x37 | 0x38 |

<a id="table-m-sensor1-a"></a>
### M_SENSOR1_A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x10 | 0x11 |

<a id="table-m-sensor2-a"></a>
### M_SENSOR2_A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x15 | 0x16 |

<a id="table-m-sensor3-a"></a>
### M_SENSOR3_A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x30 | 0x31 |

<a id="table-m-sensor4-a"></a>
### M_SENSOR4_A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x35 | 0x36 |

<a id="table-m-analog"></a>
### M_ANALOG

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x01 | 0x2B |

<a id="table-tab-klemme30-err"></a>
### TAB_KLEMME30_ERR

Dimensions: 19 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | kein Fehler festgestellt |
| 0x0001 | Überpannung |
| 0x0002 | Unterspannung |
| 0x0004 | reserviert |
| 0x0008 | reserviert |
| 0x0010 | reserviert |
| 0x0020 | reserviert |
| 0x0040 | reserviert |
| 0x0060 | reserviert |
| 0x0080 | reserviert |
| 0x0100 | reserviert |
| 0x0200 | reserviert |
| 0x0400 | reserviert |
| 0x0800 | reserviert |
| 0x1000 | reserviert |
| 0x2000 | reserviert |
| 0x4000 | reserviert |
| 0x8000 | reserviert |
| 0xFFFF | manuell auswerten |

<a id="table-tab-switch-x-error"></a>
### TAB_SWITCH_X_ERROR

Dimensions: 19 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | kein Fehler festgestellt |
| 0x0001 | Schluss nach UBAT |
| 0x0002 | Schluss nach GND |
| 0x0004 | reserviert |
| 0x0008 | reserviert |
| 0x0010 | reserviert |
| 0x0020 | reserviert |
| 0x0040 | reserviert |
| 0x0060 | reserviert |
| 0x0080 | reserviert |
| 0x0100 | reserviert |
| 0x0200 | reserviert |
| 0x0400 | reserviert |
| 0x0800 | reserviert |
| 0x1000 | reserviert |
| 0x2000 | reserviert |
| 0x4000 | reserviert |
| 0x8000 | reserviert |
| 0xFFFF | manuell auswerten |
