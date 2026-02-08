# tvm2r.prg

- Jobs: [85](#jobs)
- Tables: [35](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | TVTuner |
| ORIGIN | BMW EI-41 JohannesHafner |
| REVISION | 2.000 |
| AUTHOR | Delphi Delphi-Muenchen Leimbach_Stefan, Delphi Delphi-Muenchen  |
| COMMENT | TVM [16] |
| PACKAGE | 1.61 |
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
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [MOST_VERSION_LESEN](#job-most-version-lesen) - Auslesen von Most Version KWP2000: $21 ReadDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $A0 MOSTVersion MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_MOST_3DB](#job-status-most-3db) - Auslesen des Status der Lichtleistungsabsenkung KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STEUERN_MOST_3DB](#job-steuern-most-3db) - Lichtleistungsabsenkung einschalten KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch $00 S1 geoeffnet = 3dB Absenkung MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_WAKE_UP_STATUS](#job-status-wake-up-status) - Auslesen des Status WakeupStatus KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_ABILITY_TO_WAKE](#job-status-ability-to-wake) - Auslesen des Status AbilityToWake KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STEUERN_ABILITY_TO_WAKE](#job-steuern-ability-to-wake) - AbilityToWake einstellen KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD AbilityToWake $00 of, $01 on, $02 critical MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
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
- [STEUERN_TEST_ANTENNE](#job-steuern-test-antenne) - Start des Antennentests KWP2000: $31 StartRoutineByLocalIdentifier $25 Test Antenna Modus  : Default
- [STATUS_TEST_ANTENNE](#job-status-test-antenne) - Ergebnis des Antennentests KWP2000: $33 StartRoutineByLocalIdentifier $25 Test Antenna Modus  : Default
- [STATUS_ANALOG_TEMPERATUR](#job-status-analog-temperatur) - Abfrage der Temperaturen des Steuergerätes.
- [STATUS_TVSETREGION](#job-status-tvsetregion) - Abfrage der Temperaturen des Steuergerätes.
- [STEUERN_TVSETREGION](#job-steuern-tvsetregion) - Abfrage der Temperaturen des Steuergerätes.
- [STEUERN_TVSETCHANNEL](#job-steuern-tvsetchannel) - Stellt einen bestimmten TV-Kanal ein. Zeit in Sekunden
- [STATUS_TVSETCHANNEL](#job-status-tvsetchannel) - Stellt einen bestimmten TV-Kanal ein. Zeit in Sekunden
- [STEUERN_SIGNALAUSGABE](#job-steuern-signalausgabe) - Steuert die Videosignalausgabe eines Steuergerätes (Videoquelle).
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Selbsttest starten.
- [STATUS_SELBSTTEST](#job-status-selbsttest) - Selbsttest starten.
- [STEUERN_TEST_VIDEOAUSGANG](#job-steuern-test-videoausgang) - Startet den Test der Videoausgänge. KWP2000: $31 StartRoutineByLocalIdentifier $27 Test Videoausgang Modus  : Default
- [STATUS_TEST_VIDEOAUSGANG](#job-status-test-videoausgang) - Wertet den Test der Videoausgänge aus.
- [STATUS_HW_VARIANTE](#job-status-hw-variante) - Liefert die HW-Variante der Headunit, oder von TV/Video-Steuergeräten.
- [STEUERN_WATCHDOG_TRIGGER_STOP](#job-steuern-watchdog-trigger-stop) - Unterbindet das regelmäßige Rücksetzen des Applikations-Watchdogs nach ARG_TIME_WATCHDOG Sekunden. Wenn ARG_TIME_WATCHDOG nicht angegeben wird, wird der Wert 0 benutzt.
- [STATUS_VERSORGUNGSSPANNUNG](#job-status-versorgungsspannung) - Betriebsspannung am SG. Darstellung mit Millivolt-Auflösung.
- [STATUS_VERSION_MOST_CONTROLLER](#job-status-version-most-controller) - Return Version of MOST Controller
- [STEUERN_ANTENNEN_SIGNAL_DIGITAL](#job-steuern-antennen-signal-digital) - Liest die aktuelle Feldstärke auf der angegebenen Antenne aus.
- [STATUS_AVERAGE_MESSAGE_RECEPTION_RATE](#job-status-average-message-reception-rate) - Liest die mittlere Nachrichtenabnahmerate des SGs während dieses Gerät geflasht wird, also in der ProgramminSession Auslesbar muss der Status jederzeit sein
- [STEUERN_SIGNALAUSGABE_AUS](#job-steuern-signalausgabe-aus) - Beendet die mit STEUERN_SIGNALAUSGABE erzwungene Signalausgabe und schaltet auf den Regulärbetrieb.
- [STATUS_KARTENNUMMER_LESEN](#job-status-kartennummer-lesen) - Liest die Kartennummer und den entsprechenden Typ der Karte sofern ein Kartenleser verbaut ist
- [STEUERN_PHANTOM_POWER_SUPPLY](#job-steuern-phantom-power-supply) - Schaltet die Phantom-Spannung der Antennen per Diagnose an oder aus Bei jedem Life-Cycle wird die Pantom-Spannung grundsätzlich eingeschaltest unabhängig vom vorher ausgeführten Diagnosejob
- [STATUS_FIRMWARE_VERSION_LESEN](#job-status-firmware-version-lesen) - liest die Firmware vesion von diversen Komponenten aus
- [_STEUERN_SAVE_RAM_DATA](#job-steuern-save-ram-data) - Speichert die im Speicher liegendenen Daten anaolg eines shut-down Events ohne das Modul herunterfahren zu müssen
- [_STATUS_SAVE_RAM_DATA](#job-status-save-ram-data) - ermittelt on die Daten des mit _STEUERN_SAVE_RAM_DATA gespeicherten Daten korrekt gespeichert wurden
- [STEUERN_FACTORY_DEFAULTS](#job-steuern-factory-defaults) - Löscht alle Benutzerdaten, z.B. zuletzt gesehener Sender, Senderlisten, FBM, Regionen für alle PIA-Profile
- [STATUS_TVM_USB_INTERFACE_TEST](#job-status-tvm-usb-interface-test) - ermittelt ob ein CI-Interface angeschlossen ist 
- [STATUS_PHANTOM_SUPPLY](#job-status-phantom-supply) - Gibt den Status der Phantomspannung zurück --

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

<a id="job-most-version-lesen"></a>
### MOST_VERSION_LESEN

Auslesen von Most Version KWP2000: $21 ReadDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $A0 MOSTVersion MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| TRANSCEIVER_VERSION | string | Version des MOST Transceivers |
| NETSERVICES_VERSION | string | Version der Oasis NetServices |
| NETSERVICES_REVISION | string | Revision der Oasis NetServices |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-most-3db"></a>
### STATUS_MOST_3DB

Auslesen des Status der Lichtleistungsabsenkung KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOST_3DB | int | Status der Lichtleistungsabsenkung 0 = Lichtleistung abgesenkt 1 = Volle Lichtleistung 5s nach Absenkung wird die volle Lichtleistung wieder aktiv |
| STAT_MOST_3DB_TEXT | string | Status der Lichtleistungsabsenkung als Text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-3db"></a>
### STEUERN_MOST_3DB

Lichtleistungsabsenkung einschalten KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch $00 S1 geoeffnet = 3dB Absenkung MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT Nach 5s wieder volle Lichtleistung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wake-up-status"></a>
### STATUS_WAKE_UP_STATUS

Auslesen des Status WakeupStatus KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WAKE_UP_STATUS | int | Status ob Device geweckt hat oder geweckt wurde 0 = nicht initialisiert 1 = SG hat geweckt 2 = SG wurde geweckt |
| STAT_WAKE_UP_STATUS_TEXT | string | Status ob Device geweckt hat oder geweckt wurde als Text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ability-to-wake"></a>
### STATUS_ABILITY_TO_WAKE

Auslesen des Status AbilityToWake KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ABILITY_TO_WAKE | int | Status ob Device wecken darf 0 = off 1 = on 2 = critical |
| STAT_ABILITY_TO_WAKE_TEXT | string | Status ob Device wecken darf als Text |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ability-to-wake"></a>
### STEUERN_ABILITY_TO_WAKE

AbilityToWake einstellen KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD AbilityToWake $00 of, $01 on, $02 critical MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter AbilityToWake Modus table  AbilityToWake Status Defaultwert: DEFAULT 00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
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

<a id="job-steuern-test-antenne"></a>
### STEUERN_TEST_ANTENNE

Start des Antennentests KWP2000: $31 StartRoutineByLocalIdentifier $25 Test Antenna Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ANTENNE | unsigned long | table TAntenne WERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-test-antenne"></a>
### STATUS_TEST_ANTENNE

Ergebnis des Antennentests KWP2000: $33 StartRoutineByLocalIdentifier $25 Test Antenna Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | table JobResult STATUS_TEXT |
| STAT_ANTENNE | unsigned long | Gibt an, welche Antenne(n) getestet wurden. |
| STAT_ANTENNE_TEXT | string | Gibt an, welche Antenne(n) getestet wurden. table TAntenne WERT |
| STAT_TEST_ANTENNE | unsigned char | Gibt den Status des gesamten Tests oder der entsprechenden Antennen wieder. Nach dem Herunterfahren oder Neustart des Steuergerätes wird der Status automatisch auf 0 zurückgesetzt. table TTestStatus WERT |
| STAT_TEST_ANTENNE_TEXT | string | Gibt den Status des gesamten Tests oder der entsprechenden Antennen wieder. Nach dem Herunterfahren oder Neustart des Steuergerätes wird der Status automatisch auf 0 zurückgesetzt. table TTestStatus WERT |
| STAT_ANZAHL_FEHLERHAFTE_ANTENNEN_WERT | unsigned char | Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 2 oder 3 meldet. Gibt wieder, wie viele Fehler während des Tests gefunden wurden. table TAntenne WERT |
| STAT_ANZAHL_FEHLERHAFTE_ANTENNEN_EINH | string | no used, but need to be in SGBD |
| STAT_FEHLER_1_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_2_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_3_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_4_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_5_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_6_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_7_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_8_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_9_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_10_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_11_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_12_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_13_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_14_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_15_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_16_ANTENNE | unsigned long | Gibt die Antenne wieder, bei der der Fehler X auftrat. Dieses Result wird mit 0xFFFFFFFF belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet oder die Antenne nicht existiert. |
| STAT_FEHLER_1_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_2_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_3_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_4_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_5_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_6_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_7_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_8_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_9_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_10_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_11_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_12_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_13_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_14_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_15_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_16_ANTENNE_TEXT | string | Gibt in Textform die Antenne wieder, bei der der Fehler X auftrat. |
| STAT_FEHLER_1_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_2_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_3_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_4_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_5_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_6_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_7_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_8_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_9_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_10_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_11_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_12_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_13_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_14_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_15_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_16_FEHLERART_ANTENNE | unsigned char | Gibt wieder, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_ANTENNE nicht den Wert 3 (Fehler) meldet. |
| STAT_FEHLER_1_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_2_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_3_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_4_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_5_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_6_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_7_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_8_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_9_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_10_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_11_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_12_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_13_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_14_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_15_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_16_FEHLERART_ANTENNE_EINH | string | "" |
| STAT_FEHLER_1_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_2_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_3_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_4_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_5_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_6_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_7_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_8_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_9_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_10_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_11_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_12_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_13_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_14_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_15_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_16_FEHLERART_ANTENNE_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_1_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_2_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_3_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_4_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_5_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_6_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_7_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_8_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_9_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_10_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_11_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_12_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_13_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_14_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_15_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_16_MESSWERT_WIDERSTAND_WERT | unsigned int | Der auf der Antenne X gemessene Widerstand. Maximum (offene Leitung) 5000kOhm |
| STAT_FEHLER_1_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_2_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_3_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_4_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_5_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_6_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_7_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_8_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_9_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_10_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_11_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_12_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_13_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_14_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_15_MESSWERT_WIDERSTAND_EINH | string | "" |
| STAT_FEHLER_16_MESSWERT_WIDERSTAND_EINH | string | "" |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-temperatur"></a>
### STATUS_ANALOG_TEMPERATUR

Abfrage der Temperaturen des Steuergerätes.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMP_FOT_WERT | char | liefert die Temperatur des Fibre Optics Tranceiver Bereich -127 C bis +127 C, -128 C bedeutet ungültig (0xFF) |
| STAT_TEMP_FOT_EINH | string | Einheit der Temperatur |
| STAT_TEMP_ENDSTU_WERT | int | liefert die Temperatur der Endstufe Bereich -32767 C bis +32767 C, -32768 C bedeutet ungültig (0xFFFF) |
| STAT_TEMP_ENDSTU_EINH | string | Einheit der Temperatur |
| STAT_TEMP_GYRO_WERT | char | liefert die Temperatur des Gyro Bereich -127 C bis +127 C, -128 C bedeutet ungültig (0xFF) |
| STAT_TEMP_GYRO_EINH | string | Einheit der Temperatur |
| STAT_TEMP_MOD_WERT | char | liefert die Temperatur des Moduls Bereich -127 C bis +127 C, -128 C bedeutet ungültig (0xFF) |
| STAT_TEMP_MOD_EINH | string | Einheit der Temperatur |
| STAT_TEMP_HDD_WERT | char | liefert die Temperatur des HDD-Laufwerks Bereich -127 C bis +127 C, -128 C bedeutet ungültig (0xFF) |
| STAT_TEMP_HDD_EINH | string | Einheit der Temperatur |
| STAT_TEMP_DVD_WERT | char | liefert die Temperatur des DVD-Laufwerks Bereich -127 C bis +127 C, -128 C bedeutet ungültig (0xFF) |
| STAT_TEMP_DVD_EINH | string | Einheit der Temperatur |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tvsetregion"></a>
### STATUS_TVSETREGION

Abfrage der Temperaturen des Steuergerätes.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_REGION | unsigned char | Eingestellte Region |
| STAT_REGION_TEXT | string | Siehe Tabelle TTvRegion. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tvsetregion"></a>
### STEUERN_TVSETREGION

Abfrage der Temperaturen des Steuergerätes.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_REGION | unsigned char | EEinstellung der Region. table TTvRegion |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tvsetchannel"></a>
### STEUERN_TVSETCHANNEL

Stellt einen bestimmten TV-Kanal ein. Zeit in Sekunden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_CHANNEL | unsigned int | Einstellung des TV-Kanals. |
| ARG_BOUQET | unsigned int | Einstellung des digitalen Bouqets Default: 0 0: analog Mögliche Werte für digital: 1 bis 64 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tvsetchannel"></a>
### STATUS_TVSETCHANNEL

Stellt einen bestimmten TV-Kanal ein. Zeit in Sekunden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CHANNEL_WERT | unsigned int | Einstellung des TV-Kanals. Mögliche Werte: 1-99 |
| STAT_BOUQET_WERT | unsigned int | Einstellung des digitalen Bouqet. 0: analog. Mögliche Werte für digital: 1-64 |
| STAT_BOUQET_EINH | string | "" |
| STAT_CHANNEL_EINH | string | "" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-signalausgabe"></a>
### STEUERN_SIGNALAUSGABE

Steuert die Videosignalausgabe eines Steuergerätes (Videoquelle).

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SIGNALART | unsigned char | Art der Signalausgabe. table TSignalArt |
| ARG_AUSGANG | unsigned int | Default: 0 In den Kommentaren des Jobs muss eine eindeutige Zuweisung des Ausgangs möglich sein. Beispiele: -Headunit: LVDS Leitung zum RSE -Videoswitch: Ausgang1 (PINs X,Y) Alle Ausgänge des Steuergerätes müssen einzeln und kombiniert anwählbar sein. table TVideoAusang |
| ARG_TIMEOUT | unsigned char | Wertebereich: 0-30,255 0 schaltet wieder auf Normalbetrieb. 255 schaltet das Signal ohne einen TIMEOUT. Ansonsten legt dies Zahl die Sekunden fest, die das Testbild ausgegeben wird. Default: 255 Wird dieser Parameter nicht angegeben, erfolgt eine Ausgabe, bis -	der Job erneut mit Parameter 0 aufgeru-fen wird -	das Steuergerät neu startet (Aufwachen, Reset, &) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Selbsttest starten.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SELBSTTEST_ROUTINE | unsigned long | Routinen, die getestet werden sollen. Die Tabelle  TSelbsttestRoutine wird in der SGBD von der Entwicklung gepflegt. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-selbsttest"></a>
### STATUS_SELBSTTEST

Selbsttest starten.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SELBSTTEST_ROUTINE | unsigned long | Routine, die getestet wurde. Tabelle  TSelbsttestRoutine |
| STAT_SELBSTTEST_ROUTINE_TEXT | string | Routine, die getestet wurde. Tabelle  TSelbsttestRoutine |
| STAT_SELBSTTEST | unsigned char | Gibt den Status der Tests wieder. |
| STAT_SELBSTTEST_TEXT | string | Gibt den Status der Tests wieder. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-test-videoausgang"></a>
### STEUERN_TEST_VIDEOAUSGANG

Startet den Test der Videoausgänge. KWP2000: $31 StartRoutineByLocalIdentifier $27 Test Videoausgang Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_AUSGANG | unsigned int | table TVideoAusgang WERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-test-videoausgang"></a>
### STATUS_TEST_VIDEOAUSGANG

Wertet den Test der Videoausgänge aus.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AUSGANG | unsigned int | Gibt wieder, als Integer, welche Ausgänge getestet wurden. In den Kommentaren des Jobs muss eine eindeutige Zuweisung des Ausgangs möglich sein. Es wird der zuletzt getestete Ausgang wiedergegeben. 0 bedeutet alle Ausgänge wurden getestet. Es wird der zuletzt getestete Ausgang wiedergegeben. |
| STAT_AUSGANG_TEXT | string | Siehe Tabelle TVideoAusgang. |
| STAT_TEST_VIDEOAUSGANG | unsigned char | Gibt den Status der getesteten Ausgänge wieder. Nach dem Herunterfahren oder Neustart des Steuergerätes wird der Status automatisch auf 0 zurückgesetzt. Gibt den Status der Tests wieder. |
| STAT_TEST_VIDEOAUSGANG_TEXT | string | Siehe Tabelle TTestStatus. |
| STAT_ANZAHL_FEHLERHAFTE_AUSGAENGE_WERT | unsigned char | Gibt wieder, auf wie vielen Ausgängen Fehler vorlagen. Dieses Result wird mit 255 belegt, wenn STAT_AUSGANG nicht den Wert 2 oder 3 meldet. |
| STAT_ANZAHL_FEHLERHAFTE_AUSGAENGE_EINH | string | " " |
| STAT_FEHLER_1_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_2_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_3_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_4_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_5_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_6_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_7_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_8_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_9_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_10_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_11_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_12_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_13_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_14_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_15_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_16_AUSGANG | unsigned int | Gibt wieder, als Integer, auf welchem Ausgang der X. Fehler gefunden wurde. Dieses Result wird mit 65535 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_1_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_2_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_3_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_4_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_5_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_6_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_7_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_8_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_9_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_10_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_11_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_12_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_13_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_14_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_15_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_16_AUSGANG_TEXT | string | Gibt wieder, als String, auf welchem Ausgang der X. Fehler gefunden wurde. |
| STAT_FEHLER_1_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_2_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_3_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_4_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_5_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_6_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_7_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_8_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_9_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_10_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_11_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_12_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_13_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_14_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_15_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_16_FEHLERART_AUSGANG | unsigned char | Gibt wieder, als Integer, welcher Art der X. Fehler war. Dieses Result wird mit 255 belegt, wenn STAT_TEST_VIDEOAUSGANG nicht den Wert 3 (Fehler) meldet oder der Ausgang nicht existiert. |
| STAT_FEHLER_1_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_2_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_3_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_4_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_5_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_6_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_7_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_8_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_9_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_10_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_11_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_12_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_13_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_14_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_15_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| STAT_FEHLER_16_FEHLERART_AUSGANG_TEXT | string | Gibt wieder, als String, welcher Art der X. Fehler war. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hw-variante"></a>
### STATUS_HW_VARIANTE

Liefert die HW-Variante der Headunit, oder von TV/Video-Steuergeräten.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HW_VARIANTE | unsigned long | liefert, welche Hardware-Variante vorliegt. |
| STAT_HW_VARIANTE_TEXT | string | liefert, welche Hardware-Variante vorliegt. |
| STAT_HW_VARIANTE_LIEFERANT | unsigned int | gibt den Lieferanten aus |
| STAT_HW_VARIANTE_LIEFERANT_TEXT | string | gibt den Lieferanten aus |
| STAT_HW_EINHEIT | unsigned long | liefert eine eindeutige ID der Hardware. |
| STAT_HW_EINHEIT_TEXT | string | liefert eine eindeutige ID der Hardware. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-watchdog-trigger-stop"></a>
### STEUERN_WATCHDOG_TRIGGER_STOP

Unterbindet das regelmäßige Rücksetzen des Applikations-Watchdogs nach ARG_TIME_WATCHDOG Sekunden. Wenn ARG_TIME_WATCHDOG nicht angegeben wird, wird der Wert 0 benutzt.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TIME_WATCHDOG | unsigned int | Beschreibung: z.B. ARG_TIME_WATCHDOG = 4 bedeutet Abschalten des Watchdog-Triggers nach 4 Sekunden. nur positiven Zahlen und die 0. Skalierung: 1 entspricht 1 Sekunde |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-versorgungsspannung"></a>
### STATUS_VERSORGUNGSSPANNUNG

Betriebsspannung am SG. Darstellung mit Millivolt-Auflösung.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_UBAT | real | Versorgunsspannung in Millivolt |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-version-most-controller"></a>
### STATUS_VERSION_MOST_CONTROLLER

Return Version of MOST Controller

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TRANSCEIVER_VERSION | string | Transceiver Version Format DDMMYY |
| STAT_NETSERVICES_VERSION | string | 3 Bytes Netservices Version |
| STAT_NETSERVICES_REVISION | string | 4 Byte Netservices Revision |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-antennen-signal-digital"></a>
### STEUERN_ANTENNEN_SIGNAL_DIGITAL

Liest die aktuelle Feldstärke auf der angegebenen Antenne aus.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ANTENNE | unsigned int | Definiert die Antenne, deren Feldstärke wiedergegeben werden soll. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FELDSTAERKE_ANTENNE_WERT | int | Feldstärke der Antenne in dBµV Bereich: 0..99 Dabei bedeutet eine Rückgabe von 0 immer eine Feldstärke außerhalb des zulässigen Bereichs. |
| STAT_FELDSTAERKE_ANTENNE_EINH | string | "" |
| STAT_BER_WERT | unsigned int | Bitfehlerrate auf der angegebenen Antenne. |
| STAT_BER_EINH | string | "" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-average-message-reception-rate"></a>
### STATUS_AVERAGE_MESSAGE_RECEPTION_RATE

Liest die mittlere Nachrichtenabnahmerate des SGs während dieses Gerät geflasht wird, also in der ProgramminSession Auslesbar muss der Status jederzeit sein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MSG_CMS_SYNC_WERT | unsigned int | Mittl. Nachrichtenabnahmerate des Kontrollkanals [0-1000] |
| STAT_MSG_CMS_SYNC_EINH | string | " " |
| STAT_MSG_CMS_ASYNC_WERT | unsigned int | Mittl. Nachrichtenabnahmerate des async. Kanals. Sollte dieses Gerät nicht Async geflasht werden muss dieser Parameter auf 0 gesetzt sein [0-10000] |
| STAT_MSG_CMS_ASYNC_EINH | string | " " |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-signalausgabe-aus"></a>
### STEUERN_SIGNALAUSGABE_AUS

Beendet die mit STEUERN_SIGNALAUSGABE erzwungene Signalausgabe und schaltet auf den Regulärbetrieb.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_AUSGANG | unsigned int | Default: 0 In den Kommentaren des Jobs muss eine eindeutige Zuweisung des Ausgangs möglich sein. Beispiele: -Headunit: LVDS Leitung zum RSE -Videoswitch: Ausgang1 (PINs X,Y) Alle Ausgänge des Steuergerätes müssen einzeln und kombiniert anwählbar sein. table TVideoAusang |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kartennummer-lesen"></a>
### STATUS_KARTENNUMMER_LESEN

Liest die Kartennummer und den entsprechenden Typ der Karte sofern ein Kartenleser verbaut ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INTERNE_KARTE1_TYP | int | Info welcher Kartentyp in internem Leser 1 sofern verbaut 0x00= keine Karte gesteckt /0x01=MediaFlow / 0x02=CMMB / 0x04=ISDB-T /0xFF = kein Kartenleser verbaut |
| STAT_INTERNE_KARTE1_TYP_TEXT | string | Info welcher Kartentyp in internem Leser 1 als Text aus der Tabelle TAB_TVM_KARTENTYP sofern ein Kartenleser verbaut ist |
| STAT_INTERNE_KARTE1_NUMMER_WERT | string | Liefert die Kartennummer der internen Karte 1 als Text |
| STAT_INTERNE_KARTE2_TYP | int | Info welcher Kartentyp in internem Leser 2 sofern verbaut 0x00= keine Karte gesteckt /0x01=MediaFlow / 0x02=CMMB / 0x04=ISDB-T /0xFF = kein Kartenleser verbaut |
| STAT_INTERNE_KARTE2_TYP_TEXT | string | Info welcher Kartentyp in internem Leser 2 als Text aus der Tabelle TAB_TVM_KARTENTYP sofern ein kartenleser verbaut ist |
| STAT_INTERNE_KARTE2_NUMMER_WERT | string | Liefert die Kartennummer der internen Karte 2 als Text |
| STAT_EXTERNE_KARTE_TYP | int | Info welcher Kartentyp in externem Leser, sofern verbaut 0x00= keine Karte gesteckt /0x01=MediaFlow / 0x02=CMMB / 0x04=ISDB-T /0xFF = kein Kartenleser verbaut |
| STAT_EXTERNE_KARTE_TYP_TEXT | string | Info welcher Kartentyp in externem Leser als Text aus der Tabelle TAB_TVM_KARTENTYP sofern ein Kartenleser verbaut ist |
| STAT_EXTERNE_KARTE_NUMMER_WERT | string | Liefert die Kartennummer der internen Karte 2 als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-phantom-power-supply"></a>
### STEUERN_PHANTOM_POWER_SUPPLY

Schaltet die Phantom-Spannung der Antennen per Diagnose an oder aus Bei jedem Life-Cycle wird die Pantom-Spannung grundsätzlich eingeschaltest unabhängig vom vorher ausgeführten Diagnosejob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ANTENNE | unsigned char | Nummer der Antennefür die zu schaltende Phantomspannung |
| ARG_ON_OFF | unsigned char | 0 = OFF 1 = ON |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHANTOM_POWER_ANTENNA_1_SUPPLY | unsigned char | Rückmeldung, ob die Ansteuerung der Antenne 1 erfolgreich gestartet werden konnte, Siehe TAB_PHANTOM_POWER_SUPPLY |
| STAT_PHANTOM_POWER_ANTENNA_2_SUPPLY | unsigned char | Rückmeldung, ob die Ansteuerung der Antenne 2 erfolgreich gestartet werden konnte, Siehe TAB_PHANTOM_POWER_SUPPLY |
| STAT_PHANTOM_POWER_ANTENNA_3_SUPPLY | unsigned char | Rückmeldung, ob die Ansteuerung der Antenne 3 erfolgreich gestartet werden konnte, Siehe TAB_PHANTOM_POWER_SUPPLY |
| STAT_PHANTOM_POWER_ANTENNA_1_SUPPLY_TEXT | string | Rückmeldung, ob die Ansteuerung der Antenne 1 erfolgreich gestartet werden konnte, Siehe TAB_PHANTOM_POWER_SUPPLY |
| STAT_PHANTOM_POWER_ANTENNA_2_SUPPLY_TEXT | string | Rückmeldung, ob die Ansteuerung der Antenne 2 erfolgreich gestartet werden konnte, Siehe TAB_PHANTOM_POWER_SUPPLY |
| STAT_PHANTOM_POWER_ANTENNA_3_SUPPLY_TEXT | string | Rückmeldung, ob die Ansteuerung der Antenne 3 erfolgreich gestartet werden konnte, Siehe TAB_PHANTOM_POWER_SUPPLY |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-firmware-version-lesen"></a>
### STATUS_FIRMWARE_VERSION_LESEN

liest die Firmware vesion von diversen Komponenten aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FIRMWARE_DIBCOM_TEXT | string | Info welches DIBCOM Firmware version |
| STAT_FIRMWARE_FPGA_TEXT | string | Info welche FPGA Firmware Version |
| STAT_FIRMWARE_INIC_TEXT | string | Info welche INIC Firmware Version |
| STAT_FIRMWARE_INIC_CONFIG_VERSION_TEXT | string | Info welche INIC Config-String Version |
| STAT_DUMMY1_TEXT | string | Dummy-Wert nicht belegt |
| STAT_DUMMY2_TEXT | string | Dummy-Wert nicht belegt |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-save-ram-data"></a>
### _STEUERN_SAVE_RAM_DATA

Speichert die im Speicher liegendenen Daten anaolg eines shut-down Events ohne das Modul herunterfahren zu müssen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-save-ram-data"></a>
### _STATUS_SAVE_RAM_DATA

ermittelt on die Daten des mit _STEUERN_SAVE_RAM_DATA gespeicherten Daten korrekt gespeichert wurden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SAVE_RAM_DATA | unsigned char | Gibt info über den Speicherstatus, Ergebnisse aus der Tabelle TAB_SAVE_RAM_DATA |
| STAT_SAVE_RAM_DATA_TEXT | string | Gibt info über den Speicherstatus als Klartext |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-factory-defaults"></a>
### STEUERN_FACTORY_DEFAULTS

Löscht alle Benutzerdaten, z.B. zuletzt gesehener Sender, Senderlisten, FBM, Regionen für alle PIA-Profile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tvm-usb-interface-test"></a>
### STATUS_TVM_USB_INTERFACE_TEST

ermittelt ob ein CI-Interface angeschlossen ist 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_USB_TEST | unsigned char | Status der USB-Verbindung zur Card-Box als Zahlencode |
| STAT_USB_TEST_TEXT | string | Status der USB-Verbindung zur Card-Box als Klartext |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-phantom-supply"></a>
### STATUS_PHANTOM_SUPPLY

Gibt den Status der Phantomspannung zurück --

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANTENNE_PHANTOM_SUPPLY | unsigned char | Gewählte Antenne(n). Details siehe Tabelle TAB_TVM_ANTENNEN |
| STAT_ANTENNE_1_PHANTOM_SUPPLY_ON | unsigned char | Phantomspannung der Antenne 1 / 0= Augeschaltet / 1= eingeschaltet |
| STAT_ANTENNE_1_PHANTOM_SUPPLY_CURRENT_STATUS | unsigned char | Strommessergebnis der Antenne 1 / 1 = Messung erfolgreich / 0 = Messung nicht erfolgreich |
| STAT_ANTENNE_1_PHANTOM_SUPPLY_CURRENT_WERT | unsigned int | Strom der Antenne 1 in mA |
| STAT_ANTENNE_1_PHANTOM_SUPPLY_CURRENT_EINH | string | "  " |
| STAT_ANTENNE_2_PHANTOM_SUPPLY_ON | unsigned char | Phantomspannung der Antenne 2 / 0= Augeschaltet / 1= eingeschaltet |
| STAT_ANTENNE_2_PHANTOM_SUPPLY_CURRENT_STATUS | unsigned char | Strommessergebnis der Antenne 2 / 1 = Messung erfolgreich / 0 = Messung nicht erfolgreich |
| STAT_ANTENNE_2_PHANTOM_SUPPLY_CURRENT_WERT | unsigned int | Strom der Antenne 2 in mA |
| STAT_ANTENNE_2_PHANTOM_SUPPLY_CURRENT_EINH | string | "  " |
| STAT_ANTENNE_3_PHANTOM_SUPPLY_ON | unsigned char | Phantomspannung der Antenne 3 / 0= Augeschaltet / 1= eingeschaltet |
| STAT_ANTENNE_3_PHANTOM_SUPPLY_CURRENT_STATUS | unsigned char | Strommessergebnis der Antenne 3 / 1 = Messung erfolgreich / 0 = Messung nicht erfolgreich |
| STAT_ANTENNE_3_PHANTOM_SUPPLY_CURRENT_WERT | unsigned int | Strom der Antenne 3 in mA |
| STAT_ANTENNE_3_PHANTOM_SUPPLY_CURRENT_EINH | string | "  " |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (132 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [ABILITY_TO_WAKE](#table-ability-to-wake) (4 × 2)
- [MOST_3DB](#table-most-3db) (3 × 2)
- [WAKE_UP_STATUS](#table-wake-up-status) (4 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (24 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (54 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [TANTENNE](#table-tantenne) (73 × 2)
- [TANTENNEFEHLERART](#table-tantennefehlerart) (5 × 2)
- [TTESTSTATUS](#table-tteststatus) (6 × 2)
- [TTVREGION](#table-ttvregion) (23 × 2)
- [TVIDEOAUSGANG](#table-tvideoausgang) (33 × 2)
- [TSIGNALART](#table-tsignalart) (9 × 2)
- [TSELBSTTESTROUTINE](#table-tselbsttestroutine) (20 × 2)
- [TLEITUNGFEHLERART](#table-tleitungfehlerart) (4 × 2)
- [TAB_HW_VARIANTE](#table-tab-hw-variante) (7 × 2)
- [THWLIEFERANT](#table-thwlieferant) (8 × 2)
- [TAB_PHANTOM_POWER_SUPPLY_RESULT](#table-tab-phantom-power-supply-result) (5 × 2)
- [TAB_SAVE_RAM_DATA](#table-tab-save-ram-data) (6 × 2)
- [TAB_USB_INTERFACE_TEST](#table-tab-usb-interface-test) (3 × 2)
- [TAB_TVM_KARTENTYP](#table-tab-tvm-kartentyp) (6 × 2)

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

Dimensions: 132 rows × 2 columns

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

<a id="table-ability-to-wake"></a>
### ABILITY_TO_WAKE

Dimensions: 4 rows × 2 columns

| ABILITY_TO_WAKE_NR | ABILITY_TO_WAKE_MODE |
| --- | --- |
| 0x00 | off |
| 0x01 | on |
| 0x02 | critical |
| 0xXY | unbekannter Mode |

<a id="table-most-3db"></a>
### MOST_3DB

Dimensions: 3 rows × 2 columns

| MOST_3DB_NR | MOST_3DB_MODE |
| --- | --- |
| 0x00 | Lichtleistung abgesenkt |
| 0x01 | Volle Lichtleistung |
| 0xXY | unbekannter Mode |

<a id="table-wake-up-status"></a>
### WAKE_UP_STATUS

Dimensions: 4 rows × 2 columns

| WAKE_UP_STATUS_NR | WAKE_UP_STATUS_MODE |
| --- | --- |
| 0x00 | nicht initialisiert |
| 0x01 | SG hat geweckt |
| 0x02 | SG wurde geweckt |
| 0xXY | unbekannter Mode |

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

Dimensions: 24 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xAA88 | Dummmy Application DTC |
| 0xAA89 | Überspannung erkannt |
| 0xAA8A | Steuergeraet nicht codiert  |
| 0xAA8B | Codierdaten-Transaktion fehlgeschlagen |
| 0xAA8C | Signatur über Nettocodierdaten ungueltig  |
| 0xAA8D | Steuergeraet falsch codiert |
| 0xAA8E | Codierdaten-Transaktion mit ungueltigen Daten |
| 0xAA8F | Energiesparmode aktiv |
| 0xAA90 | Host hat bei fatalem Fehler vom INIC einen Reset ausgelöst |
| 0xAA9A | Interner Steuergerätefehler Hardware |
| 0xAA9B | Interner Steuergerätefehler Software |
| 0xAA9D | FBAS-Ausgang 1: Kurzschluss |
| 0xAA9E | FBAS-Ausgang 1: Unterbrechung oder fehlerhafte Senke |
| 0xAA9F | Kurzschluss Antenne 1 |
| 0xAAA0 | Antenne 1 nicht verbunden, hohe Impedanz |
| 0xAAA1 | Kurzschluss Antenne 2 |
| 0xAAA2 | Antenne 2 nicht verbunden, hohe Impedanz |
| 0xAAA3 | Kurzschluss Antenne 3 |
| 0xAAA4 | Antenne 3 nicht verbunden, hohe Impedanz |
| 0xAAA5 | FBAS-Ausgang 2: Unterbrechung oder fehlerhafte Senke |
| 0xAAA6 | FBAS-Ausgang 2: Kurzschluss |
| 0xDBD0 | MOST_RING_DIAGNOSIS |
| 0xDBD2 | Sender- Empfängerbaustein (FOT): Temperatur übersteigt kritische Schwelle |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | ja |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | nein |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 54 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9308 | RESET |
| 0x930A | MOST: Licht geht unerwartet aus |
| 0x930C | MOST_UNLOCKSHORT |
| 0x930D | Systemzustand Ok nicht fristgerecht erkannt |
| 0x9310 | Empfängerknoten: hat Nachricht nicht abgenommen; Puffer voll |
| 0x9311 | MOST: Synchronisation (PLL) arbeitet nicht korrekt |
| 0x9320 | COM Flash Error |
| 0x9321 | COM EEPROM Error |
| 0x9340 | Timing-Master: kann Audiokanal nicht reservieren; beschäftigt |
| 0x9341 | Timing-Master: kann Kanal nicht freigeben; beschäftigt |
| 0x9342 | Timing-Master: kann Kanal nicht freigeben; falsches Label |
| 0x9343 | Empfängerknoten: hat Nachricht nicht abgenommen; Empfänger existiert nicht |
| 0x9344 | Empfängerknoten: hat Nachricht nicht abgenommen; fehlerhafte Check- Summe am Empfänger erkannt |
| 0x9345 | Übertragungsfehler im Hardware Abstraction Layer |
| 0x934A | Empfängerknoten: Kommandointerpreter kennt Nachricht nicht |
| 0x934B | Empfängerknoten: mindestens eine Nachricht (Group/Broadcast) nicht abgenommen |
| 0x934D | Senderknoten: adressierter Funktionsblock existiert nicht |
| 0x934E | Senderknoten: falsche Parameter in der Nachricht |
| 0x934F | Senderknoten: Fehler in adressierter Funktion |
| 0x9350 | Senderknoten: Fehler in Segmentierung |
| 0x9351 | Funktionsblock: sendet keine Werte trotz Notifizierung |
| 0x9352 | Funktionsblock: Notifizierung abgelehnt; Spalte der Notifizierungstabelle voll |
| 0x9353 | Funktionsblock: Notifizierung abgelehnt; keine freien Zeilen in Notifizierungstabelle |
| 0x9354 | Funktionsblock: Notifizierung abgelehnt; gewünschte Funktion existiert nicht |
| 0x9355 | Funktionsblock: Notifizierung abgelehnt; Grund unbekannt |
| 0x9356 | Funktionsblock: Notifizierung abgelehnt; Funktionswert momentan nicht vorhanden |
| 0x9360 | Versorgungsspannung: Mindestwert unterschritten |
| 0xDBD0 | MOST: Ringbruch |
| 0x9375 | Timing-Master: kann Kanal nicht reservieren; Ergebnistabelle (RAT) voll |
| 0x9376 | Diagnose-Master-Client: Datenzwischenablage im Active Response Handler übergelaufen |
| 0x9377 | DM_Queue_DELETED?? |
| 0x9378 | Sender- Empfängerbaustein (FOT): Temperatur übersteigt Schwelle 2 |
| 0x9379 | Funktionsblock (Methode mit Handle): Lebenszeichen kommt nicht fristgerecht |
| 0x937A | Funktionsblock (Methode): Lebenszeichen kommt nicht fristgerecht |
| 0x937B | MOST: Ring unerlaubt geweckt |
| 0x937C | DTC zum Ausfall Botschaft |
| 0x9361 | SW Error - MPEG APPL FRONTEND: Frontend: could not be started |
| 0x9362 | SW Error - MPEG APPL STI: STI-Manager: could not started |
| 0x9363 | SW Error - MPEG APPL BWL: BrowserList: could not be started |
| 0x9364 | SW Error - MPEG APPL TVAPI: TV-API: re-started |
| 0x9365 | SW Error - MPEG APPL HMI: HMI Manager: could not be started |
| 0x9366 | SW Error - MPEG APPL TELETEXT: Teletext: could not be started |
| 0x9367 | SW Error - MPEG APPL DATAPOOL: DataPool: could not be started |
| 0x9368 | SW Error - MPEG APPL BML: ISDBT only: BML could not be started |
| 0x9369 | HW Error - FPGA CONFIG: FPGA configuration failed |
| 0x936A | HW Error - ATTACH INIC: attach INIC failed |
| 0x936B | SW Error - WATCHDOG RESET ST STARTUP: watchdog reset ST startup |
| 0x936C | HW Error - MPEG I2C ST: ISDBT only: I2C ST failed |
| 0x936D | HW Error - USB OVERCURRENT: USB overcurrent |
| 0x936F | SW Error - WATCHDOG RESET ST PERIODIC: watchdog reset ST periodic |
| 0x9370 | HW Error - NEC SHARED RAM: NEC access to shared RAM failed |
| 0x9372 | HW Error - NEC EXTERNAL FLASH: NEC access to external RAM failed |
| 0x937D | MPEG_DIBCOM_RESET |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | ja |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | nein |

<a id="table-tantenne"></a>
### TANTENNE

Dimensions: 73 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Antennen |
| 0x00000001 | AM/FM Antenne |
| 0x00000002 | GPS Antenne |
| 0x00000003 | AM/FM Antenne und GPS Antenne |
| 0x00000004 | DAB L-BAND Antenne |
| 0x00000005 | AM/FM Antenne und DAB L-BAND Antenne |
| 0x00000006 | GPS Antenne und DAB L-BAND Antenne |
| 0x00000007 | AM/FM Antenne, GPS Antenne und DAB L-BAND Antenne |
| 0x00000008 | DAB BAND III Antenne |
| 0x00000009 | AM/FM Antenne und DAB BAND III Antenne |
| 0x0000000A | GPS Antenne und DAB BAND III Antenne |
| 0x0000000B | AM/FM Antenne, GPS Antenne und DAB BAND III Antenne |
| 0x0000000C | DAB L-BAND Antenne und DAB BAND III Antenne |
| 0x0000000D | AM/FM Antenne, DAB L-BAND Antenne und DAB BAND III Antenne |
| 0x0000000E | GPS Antenne, DAB L-BAND Antenne und DAB BAND III Antenne |
| 0x0000000F | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne und DAB BAND III Antenne |
| 0x00000010 | VICS FM Antenne |
| 0x00000011 | AM/FM Antenne und VICS FM Antenne |
| 0x00000012 | GPS Antenne und VICS FM Antenne |
| 0x00000013 | AM/FM Antenne, GPS Antenne und VICS FM Antenne |
| 0x00000014 | DAB L-BAND Antenne und VICS FM Antenne |
| 0x00000015 | AM/FM Antenne, DAB L-BAND Antenne und VICS FM Antenne |
| 0x00000016 | GPS Antenne, DAB L-BAND Antenne und VICS FM Antenne |
| 0x00000017 | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne und VICS FM Antenne |
| 0x00000018 | DAB BAND III Antenne und VICS FM Antenne |
| 0x00000019 | AM/FM Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001A | GPS Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001B | AM/FM Antenne, GPS Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001C | DAB L-BAND Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001D | AM/FM Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001E | GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001F | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und |
| 0x00000020 | VICS Beacon Antenne |
| 0x00000021 | AM/FM Antenne und VICS Beacon Antenne |
| 0x00000022 | GPS Antenne und VICS Beacon Antenne |
| 0x00000023 | AM/FM Antenne, GPS Antenne und VICS Beacon Antenne |
| 0x00000024 | DAB L-BAND Antenne und VICS Beacon Antenne |
| 0x00000025 | AM/FM Antenne, DAB L-BAND Antenne und VICS Beacon Antenne |
| 0x00000026 | GPS Antenne, DAB L-BAND Antenne und VICS Beacon Antenne |
| 0x00000027 | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne und VICS Beacon Antenne |
| 0x00000028 | DAB BAND III Antenne und VICS Beacon Antenne |
| 0x00000029 | AM/FM Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002A | GPS Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002B | AM/FM Antenne, GPS Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002C | DAB L-BAND Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002D | AM/FM Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002E | GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002F | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x00000030 | VICS FM Antenne und VICS Beacon Antenne |
| 0x00000031 | AM/FM Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000032 | GPS Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000033 | AM/FM Antenne, GPS Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000034 | DAB L-BAND Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000035 | AM/FM Antenne, DAB L-BAND Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000036 | GPS Antenne, DAB L-BAND Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000037 | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000038 | DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000039 | AM/FM Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003A | GPS Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003B | AM/FM Antenne, GPS Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003C | DAB L-BAND Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003D | AM/FM Antenne, DAB L-BAND Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003E | GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003F | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000040 | TV1 Antenne |
| 0x00000080 | TV2 Antenne |
| 0x000000C0 | TV1 und TV2 Antenne |
| 0x00000100 | TV3 Antenne |
| 0x00000140 | TV1 und TV3 Antenne |
| 0x00000180 | TV2 und TV3 Antenne |
| 0x000001C0 | TV1, TV2 und TV3 Antenne |
| 0x00000200 | SDARS Antenne |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-tantennefehlerart"></a>
### TANTENNEFEHLERART

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzschluss nach Plus |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Leitungsunterbrechung |
| 0x03 | Falscher Antennfuß oder Diversity |
| 0xFF | Nicht definiert |

<a id="table-tteststatus"></a>
### TTESTSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test nicht gestartet |
| 0x01 | Test läuft |
| 0x02 | Test beendet ohne Fehler |
| 0x03 | Test beendet mit Fehlern |
| 0x04 | Test unterbrochen |
| 0xFF | Nicht definiert |

<a id="table-ttvregion"></a>
### TTVREGION

Dimensions: 23 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Nordamerika |
| 0x02 | Mittelamerika |
| 0x03 | Südamerika |
| 0x04 | Karibik |
| 0x05 | Europa/Mitteleuropa |
| 0x06 | Frankreich |
| 0x07 | Russland |
| 0x08 | Afrika/Nordafrika |
| 0x09 | Naher Osten |
| 0x0A | Asien |
| 0x0B | Pazifik |
| 0x0C | Ozeanien/Australien |
| 0x0D | China |
| 0x0E | Hong Kong |
| 0x0F | Taiwan |
| 0x10 | Westeuropa |
| 0x11 | Osteuropa |
| 0x12 | Nordosteuropa |
| 0x13 | Türkei |
| 0x14 | Griechenland |
| 0x15 | Israel |
| 0x16 | Mittel-/Südafrika |
| 0xFF | Nicht definiert |

<a id="table-tvideoausgang"></a>
### TVIDEOAUSGANG

Dimensions: 33 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Alle Ausgänge |
| 0x0001 | Ausgang 1 |
| 0x0002 | Ausgang 2 |
| 0x0003 | Ausgang 1 und 2 |
| 0x0004 | Ausgang 3 |
| 0x0005 | Ausgang 1 und 3 |
| 0x0006 | Ausgang 2 und 3 |
| 0x0007 | Ausgang 1, 2 und 3 |
| 0x0008 | Ausgang 4 |
| 0x0009 | Ausgang 1 und 4 |
| 0x000A | Ausgang 2 und 4 |
| 0x000B | Ausgang 1, 2 und 4 |
| 0x000C | Ausgang 3 und 4 |
| 0x000D | Ausgang 1, 2 und 4 |
| 0x000E | Ausgang 2, 3 und 4 |
| 0x000F | Ausgang 1, 2, 3 und 4 |
| 0x0010 | Ausgang 5 |
| 0x0011 | Ausgang 1 und 5 |
| 0x0012 | Ausgang 2 und 5 |
| 0x0013 | Ausgang 1,2 und 5 |
| 0x0014 | Ausgang 3 und 5 |
| 0x0015 | Ausgang 1,3 und 5 |
| 0x0016 | Ausgang 2,3 und 5 |
| 0x0017 | Ausgang 1, 2 und 3 und 5 |
| 0x0018 | Ausgang 4 und 5 |
| 0x0019 | Ausgang 1, 4 und 5 |
| 0x001A | Ausgang 2, 4 und 5 |
| 0x001B | Ausgang 1, 2, 4 und 5 |
| 0x001C | Ausgang 3, 4 und 5 |
| 0x001D | Ausgang 1, 2, 4 und 5 |
| 0x001E | Ausgang 2, 3, 4 und 5 |
| 0x001F | Ausgang 1, 2, 3, 4 und 5 |
| 0xFFFF | Nicht definiert |

<a id="table-tsignalart"></a>
### TSIGNALART

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Realbild |
| 0x02 | Testbild |
| 0x03 | Signal abschalten |
| 0x04 | Testbild mit Alive Counter (ACNT) |
| 0x05 | Testbild mit stehendem ACNT |
| 0x06 | Testbild mit leicht gestörtem ACNT |
| 0x07 | Testbild mit stark gestörtem ACNT |
| 0x08 | Testbild mit leicht springendem ACNT |
| 0x09 | Testbild mit stark springendem ACNT |

<a id="table-tselbsttestroutine"></a>
### TSELBSTTESTROUTINE

Dimensions: 20 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | alle Routinen |
| 0x00000001 | Internal Supply Voltages |
| 0x00000002 | FOT Temperature |
| 0x00000004 | Board Temperature |
| 0x00000008 | NEC-Flash Checksum |
| 0x00000010 | EEPROM Checksum |
| 0x00000020 | TOSHIBA-Flash Checksum |
| 0x00000040 | TOSHIBA-RAM Integrity |
| 0x00000080 | UART-Interface Communication: NEC / TOSHIBA |
| 0x00000100 | Host-interface Communication: FPGA / TOSHIBA |
| 0x00000200 | SPI-interface Communication: FPGA / NEC |
| 0x00000400 | not used |
| 0x00000800 | Internal PLL lock of Tuner-IC´s |
| 0x00001000 | Internal PLL lock of FPGA |
| 0x00002000 | I2C Device Status |
| 0x00004000 | Antenna Input |
| 0x00008000 | Video Output |
| 0x00010000 | Fan Rotation |
| 0x00020000 | Verify the application status |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-tleitungfehlerart"></a>
### TLEITUNGFEHLERART

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzschluss nach Plus |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Leitungsunterbrechung |
| 0xFF | Nicht definiert |

<a id="table-tab-hw-variante"></a>
### TAB_HW_VARIANTE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000020 | TV-Modul2 ECE Standard |
| 0x00000040 | TV-Modul2 ECE RSE |
| 0x00000080 | TV-Modul2 Japan Standard |
| 0x00000100 | TV-Modul2 Japan RSE |
| 0x00000200 | TV-Modul2 China Standard |
| 0x00000400 | TV-Modul2 China RSE |
| 0xFFFFFFFF | nicht definiert |

<a id="table-thwlieferant"></a>
### THWLIEFERANT

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Harman Becker |
| 0x01 | Siemens VDO |
| 0x02 | Visteon |
| 0x03 | Alpine |
| 0x04 | Lear |
| 0x05 | Fuba |
| 0x06 | Hirschmann Car Communication |
| 0xFF | Nicht definiert |

<a id="table-tab-phantom-power-supply-result"></a>
### TAB_PHANTOM_POWER_SUPPLY_RESULT

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Phantomspannung nicht aktiviert |
| 0x01 | Phantomspannung aktiv |
| 0x02 | Phantomspannung konnte nicht aktiviert werden |
| 0x03 | Phantomspannung konnte nicht deaktiviert werden |
| 0xFF | Ungültiger Wert |

<a id="table-tab-save-ram-data"></a>
### TAB_SAVE_RAM_DATA

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Datensicherung nicht gestartet |
| 0x01 | Datensicherung läuft |
| 0x02 | Datensicherung beendet ohne Fehler |
| 0x03 | Datensicherung beendet mit Fehlern |
| 0x04 | Datensicherung unterbrochen |
| 0xFF | Ungültig |

<a id="table-tab-usb-interface-test"></a>
### TAB_USB_INTERFACE_TEST

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein USB Interface angeschlossen |
| 0x01 | USB Interface angeschlossen |
| 0xFF | Ungültig |

<a id="table-tab-tvm-kartentyp"></a>
### TAB_TVM_KARTENTYP

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Kartenleser vorhanden |
| 0x01 | keine Karte gesteckt |
| 0x02 | MediaFlo-Card |
| 0x03 | CMMB-Card |
| 0x04 | ISBD-T-Card (BCAS) |
| 0xFF | Ungültiger Wert |
