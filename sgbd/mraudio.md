# mraudio.prg

- Jobs: [100](#jobs)
- Tables: [35](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Motorrad Audioplattform |
| ORIGIN | BMW UX-EE-2 Dettloff, Günter |
| REVISION | 2.002 |
| AUTHOR | in-tech UX-EE-1 Breitkreutz, Dräxlmaier UX-EE-1 Rätscher |
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
- [STEUERN_RADIO_ONOFF](#job-steuern-radio-onoff) - Simulation Tastendruck ENTERTAINMENT-Taste KWP2000: $3B WriteDataByLocalIdentifier $A0 inputOutputLocalIdentifier  - switch radio on or off Modus  : Default
- [STATUS_RADIO_ONOFF](#job-status-radio-onoff) - Simulation Tastendruck ENTERTAINMENT-Taste KWP2000: $21 ReadDataByLocalIdentifier $A0 inputOutputLocalIdentifier  - switch radio on or off Modus  : Default
- [STATUS_FREQUENZ](#job-status-frequenz) - aktuelle Tunerfrequenz abfragen KWP2000: $21 ReadDataByLocalIdentifier $96 inputOutputLocalIdentifier - tuner frequency Modus  : Default
- [STEUERN_FREQUENZ](#job-steuern-frequenz) - Tunerfrequenz einstellen KWP2000: $3B WriteDataByLocalIdentifier $96 inputOutputLocalIdentifier - tuner frequency Modus  : Default
- [STATUS_RDS](#job-status-rds) - Lesen Status AF-Verfolgung und TP KWP2000: $21 ReadDataByLocalIdentifier $91 inputOutputLocalIdentifier  - - get RDS Modus  : Default
- [STEUERN_RDS](#job-steuern-rds) - Steuern AF-Verfolgung und TP KWP2000: $3B WriteDataByLocalIdentifier $91 inputOutputLocalIdentifier - set RDS Modus  : Default
- [STATUS_ANT_QFS](#job-status-ant-qfs) - Auslesen des Status Quality Fieldstrength KWP2000: $21 ReadDataByLocalIdentifier $92 inputOutputLocalIdentifier - signal quality Modus  : Default
- [STEUERN_TUNER_SUCHLAUF](#job-steuern-tuner-suchlauf) - Sendersuchlauf des AM/FM-Tuner starten KWP2000: $31 StartRoutineByLocalIdentifier $93 RoutineLocalIdentifier  - seek - Tuner_Suchlauf Modus  : Default
- [STOP_STEUERN_TUNER_SUCHLAUF](#job-stop-steuern-tuner-suchlauf) - Sendersuchlauf des AM/FM-Tuner stoppen KWP2000: $32 StopRoutineByLocalIdentifier $93 RoutineLocalIdentifier  - seek - Tuner_Suchlauf Modus  : Default
- [STEUERN_FIND_BEST_STATION](#job-steuern-find-best-station) - Routine zur Suche des besten, verfügberen Senders KWP2000: $31 StartRoutineByLocalIdentifier $94 RoutineLocalIdentifier (find_best_station) Modus  : Default
- [STEUERN_WAVEBAND](#job-steuern-waveband) - Umschalten der Radio-Quelle per Diagnose KWP2000: $31 StartRoutineByLocalIdentifier $95 RoutineLocalIdentifier  - waveband Modus  : Default
- [STATUS_WAVEBAND](#job-status-waveband) - Status der Radio-Quelle per Diagnose KWP2000: $33 RequestRoutineResultsByLocalIdentifier $95 RoutineLocalIdentifier  - waveband Modus  : Default
- [STATUS_VOLUME](#job-status-volume) - Auslesen, welches Lautstärke Inkrement eingestellt ist KWP2000: $21 ReadDataByLocalIdentifier $80 recordLocalIdentifier - Volume audio step Modus  : Default
- [STEUERN_VOLUME](#job-steuern-volume) - Einstellen der Audio-Lautstaerke KWP2000: $3B WriteDataByLocalIdentifier $80 inputOutputLocalIdentifier - set volume Modus  : Default
- [STEUERN_BALANCE](#job-steuern-balance) - Ansteuern eines AudioKanals bzw. Einstellen der Balance KWP2000: $3B WriteDataByLocalIdentifier $83 inputOutputLocalIdentifier  - balance Modus  : Default
- [STATUS_BALANCE](#job-status-balance) - Status eines AudioKanals bzw. Einstellen der Balance KWP2000: $21 ReadDataByLocalIdentifier $83 inputOutputLocalIdentifier  - balance Modus  : Default
- [STATUS_FADER](#job-status-fader) - Status eines AudioKanals bzw. Einstellen des Faders KWP2000: $21 ReadDataByLocalIdentifier $84 inputOutputLocalIdentifier  - fader Modus  : Default
- [STEUERN_FADER](#job-steuern-fader) - Ansteuern eines AudioKanals bzw. Einstellen des Faders KWP2000: $3B WriteDataByLocalIdentifier $84 inputOutputLocalIdentifier  - fader Modus  : Default
- [STATUS_AKTIVE_GAL_KURVE](#job-status-aktive-gal-kurve) - Reads the active coded speed dependent volume control curve  KWP2000: $21 ReadDataByLocalIdentifier $85 RecordLocalIdentifier
- [STEUERN_GAL_KURVE](#job-steuern-gal-kurve) - Schreibt die zu nutzende GAL-Kurve  KWP2000: $3B WriteDataByLocalIdentifier $85 RecordLocalIdentifier
- [STEUERN_SOURCE_CONTROL](#job-steuern-source-control) - Umschalten der Entertainment-Quelle per Diagnose KWP2000: $3B WriteDataByLocalIdentifier $87 RoutineLocalIdentifier  - source control Modus  : Default
- [STATUS_SOURCE_CONTROL](#job-status-source-control) - Status der Entertainment-Quelle per Diagnose KWP2000: $21 RequestRoutineResultsByLocalIdentifier $87 RoutineLocalIdentifier  - source control Modus  : Default
- [STEUERN_BASS](#job-steuern-bass) - Schreiben der Bass-Einstellung KWP2000: $3B writeDataByLocalIdentifier $81 recordLocalIdentifier - bass Modus  : Default
- [STATUS_BASS](#job-status-bass) - Status der Bass-Einstellung KWP2000: $21 writeDataByLocalIdentifier $81 recordLocalIdentifier - bass Modus  : Default
- [STATUS_TREBLE](#job-status-treble) - Status der Treble-Einstellung KWP2000: $21 writeDataByLocalIdentifier $82 recordLocalIdentifier - treble Modus  : Default
- [STEUERN_TREBLE](#job-steuern-treble) - Schreiben der Treble-Einstellung KWP2000: $3B writeDataByLocalIdentifier $82 recordLocalIdentifier - treble Modus  : Default
- [STATUS_MUTE](#job-status-mute) - Auslesen, ob Mute "ein" oder "aus" ist KWP2000: $21 ReadDataByLocalIdentifier $86 recordLocalIdentifier - mute Modus  : Default
- [STEUERN_MUTE](#job-steuern-mute) - Mute "ein" oder "aus" schalten KWP2000: $3B WriteDataByLocalIdentifier $86 recordLocalIdentifier - mute Modus  : Default
- [STATUS_INTERNE_TEMPERATUR](#job-status-interne-temperatur) - Status des SG- Temperaturwertes KWP2000: $21 ReadDataByLocalIdentifier $D1 inputOutputLocalIdentifier - interal temperature Modus  : Default
- [STATUS_INTERNE_SPANNUNG](#job-status-interne-spannung) - Status der internen Batterie-Spannung des MCR KWP2000: $21 ReadDataByLocalIdentifier $D0 inputOutputLocalIdentifier - interal voltage Modus  : Default
- [STATUS_PARROT_SW_HW_VERS_LESEN](#job-status-parrot-sw-hw-vers-lesen) - Lesen der Parrot HW- und SW-Version KWP2000: $21 ReadDataByLocalIdentifier $B1 inputOutputLocalIdentifier - Parrot SW-HW-Version Modus  : Default
- [STATUS_PARROT_BT_ADRESSE_LESEN](#job-status-parrot-bt-adresse-lesen) - Lesen der Parrot BT-Adresse KWP2000: $21 ReadDataByLocalIdentifier $B0 inputOutputLocalIdentifier - Parrot BT-Adresse Modus  : Default
- [STEUERN_PARROT_BT_ADRESSE_SCHREIBEN](#job-steuern-parrot-bt-adresse-schreiben) - Schreiben der Parrot BT-Adresse KWP2000: $3B WriteDataByLocalIdentifier $B0 inputOutputLocalIdentifier - Parrot BT-Adresse Modus  : Default
- [STATUS_FRONT_SPEAKER_ONOFF](#job-status-front-speaker-onoff) - Zustand der vorderen Lautsprecher, sind sie ein oder aus geschalten? KWP2000: $21 ReadDataByLocalIdentifier $88 inputOutputLocalIdentifier  - switch Front Speaker on or off Modus  : Default
- [STEUERN_FRONT_SPEAKER_ONOFF](#job-steuern-front-speaker-onoff) - Zustand der vorderen Lautsprecher, sind sie ein oder aus geschalten? KWP2000: $3B WriteDataByLocalIdentifier $88 inputOutputLocalIdentifier  - switch Front Speaker on or off Modus  : Default
- [STATUS_REAR_SPEAKER_ONOFF](#job-status-rear-speaker-onoff) - Zustand der vorderen Lautsprecher, sind sie ein oder aus geschalten? KWP2000: $21 ReadDataByLocalIdentifier $89 inputOutputLocalIdentifier  - switch Rear Speaker on or off Modus  : Default
- [STEUERN_REAR_SPEAKER_ONOFF](#job-steuern-rear-speaker-onoff) - Zustand der vorderen Lautsprecher, sind sie ein oder aus geschalten? KWP2000: $3B WriteDataByLocalIdentifier $89 inputOutputLocalIdentifier  - switch Rear Speaker on or off Modus  : Default
- [STATUS_LOUDNESS_ONOFF](#job-status-loudness-onoff) - Zustand der Funktion Loudness, ist sie ein oder aus geschalten? KWP2000: $21 ReadDataByLocalIdentifier $8A inputOutputLocalIdentifier  - switch LOUDNESS on or off Modus  : Default
- [STEUERN_LOUDNESS_ONOFF](#job-steuern-loudness-onoff) - Zustand der Funktion Loudness, ist sie ein oder aus geschalten? KWP2000: $3B WriteDataByLocalIdentifier $8A inputOutputLocalIdentifier  - switch Loudness on or off Modus  : Default
- [STATUS_BLUETOOTH_ONOFF](#job-status-bluetooth-onoff) - Zustand der Funktion BLUETOOTH, ist sie ein oder aus geschalten? KWP2000: $21 ReadDataByLocalIdentifier $B2 inputOutputLocalIdentifier  - switch BLUETOOTH on or off Modus  : Default
- [STEUERN_BLUETOOTH_ONOFF](#job-steuern-bluetooth-onoff) - Zustand der Funktion Bluetooth, ist sie ein oder aus geschalten? KWP2000: $3B WriteDataByLocalIdentifier $B2 inputOutputLocalIdentifier  - switch bluetooth on or off Modus  : Default
- [STEUERN_BLUETOOTH_EOL_TEST](#job-steuern-bluetooth-eol-test) - Schreiben der Parrot BT-Adresse KWP2000: $31 StartRoutineByLocalIdentifier $B3 inputOutputLocalIdentifier - Bluetooth EOL Test Modus  : Default
- [STOP_STEUERN_BLUETOOTH_EOL_TEST](#job-stop-steuern-bluetooth-eol-test) - Schreiben der Parrot BT-Adresse KWP2000: $32 StopRoutineByLocalIdentifier $B3 inputOutputLocalIdentifier - Bluetooth EOL Test Modus  : Default
- [STATUS_ROUTINE_BLUETOOTH_EOL_TEST](#job-status-routine-bluetooth-eol-test) - Dieser Routine Service liefert das Ergebnis der Bluetooth Suche nach dem angegebenen Gerät. Ist die Suche abgeschlossen bleibt das Ergebnis solange gültig, bis eine neue Suche gestartet wird. KWP2000: $33 RequestRoutineResultsByLocalIdentifier $B3 inputOutputLocalIdentifier - Bluetooth EOL Test Modus  : Default
- [STATUS_USB_IPOD](#job-status-usb-ipod) - KWP2000: $21 RequestRoutineResultsByLocalIdentifier $B4 RoutineLocalIdentifier (USB/iPod Device Diagnostics) Modus  : Default
- [STATUS_FIND_BEST_STATION](#job-status-find-best-station) - KWP2000: $33 RequestRoutineResultsByLocalIdentifier $94 RoutineLocalIdentifier (find_best_station) Modus  : Default
- [STATUS_SIRIUS_SN_LESEN](#job-status-sirius-sn-lesen) - Lesen der Sirius Seriennummer KWP2000: $21 ReadDataByLocalIdentifier $C0 inputOutputLocalIdentifier - Parrot BT-Adresse Modus  : Default
- [STATUS_SIRIUS_FW](#job-status-sirius-fw) - Lesen der Sirius Firmwarenummer KWP2000: $21 ReadDataByLocalIdentifier $C1 inputOutputLocalIdentifier - Firmwarenummer Modus  : Default
- [STATUS_SIRIUS_SIGNAL](#job-status-sirius-signal) - Status des Sirius Signals per Diagnose KWP2000: $21 RequestRoutineResultsByLocalIdentifier $C2 RoutineLocalIdentifier  - sirius signal Modus  : Default
- [STEUERN_SIRIUS_FACTORYDEFAULT](#job-steuern-sirius-factorydefault) - Sirius Empfaenger auf Werkseinstellung zuruecksetzen KWP2000: $3B WriteDataByLocalIdentifier $C3 inputOutputLocalIdentifier - sirius factory default Modus  : Default
- [STATUS_SIRIUS_FACTORYDEFAULT](#job-status-sirius-factorydefault) - Lesen des Sirius Werkseinstellungsstatus KWP2000: $21 ReadDataByLocalIdentifier $C3 inputOutputLocalIdentifier - Werkseinstellung Modus  : Default
- [STEUERN_SIRIUS_TUNERMODUS](#job-steuern-sirius-tunermodus) - Waehlt den Sirius Tunermodus KWP2000: $3B WriteDataByLocalIdentifier $C4 inputOutputLocalIdentifier  - Sirius tunermode Modus  : Default
- [STATUS_SIRIUS_TUNERMODUS](#job-status-sirius-tunermodus) - Gewaehlter Sirius Tunermodus KWP2000: $21 ReadDataByLocalIdentifier $C4 inputOutputLocalIdentifier  - Sirius tunermode Modus  : Default
- [STATUS_SIRIUS_BITFEHLERRATE](#job-status-sirius-bitfehlerrate) - Lesen der Sirius Bitfehlerrate KWP2000: $21 ReadDataByLocalIdentifier $C5 inputOutputLocalIdentifier - Bitfehlerrate Modus  : Default
- [STEUERN_SIRIUS_SIGNALGEN](#job-steuern-sirius-signalgen) - Ansteuern der Kanaele im Signalgeneratormodus KWP2000: $3B WriteDataByLocalIdentifier $C6 inputOutputLocalIdentifier - Signalgenerator Modus  : Default
- [STATUS_SIRIUS_SIGNALGEN](#job-status-sirius-signalgen) - Lesen der Sirius Bitfehlerrate KWP2000: $21 ReadDataByLocalIdentifier $C6 inputOutputLocalIdentifier - Signalgenerator Modus  : Default

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

<a id="job-steuern-radio-onoff"></a>
### STEUERN_RADIO_ONOFF

Simulation Tastendruck ENTERTAINMENT-Taste KWP2000: $3B WriteDataByLocalIdentifier $A0 inputOutputLocalIdentifier  - switch radio on or off Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHALTMODUS | string | EIN/AUS-Schalten des Radios 0/"no override" = no override, 1/off/aus = off, 2/on/ein = on |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-radio-onoff"></a>
### STATUS_RADIO_ONOFF

Simulation Tastendruck ENTERTAINMENT-Taste KWP2000: $21 ReadDataByLocalIdentifier $A0 inputOutputLocalIdentifier  - switch radio on or off Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MODUS_TEXT | string | Ein/aus-Status des Radios 0 = no override, 1 = off, 2 = on |
| STAT_MODUS | char | Ein/aus-Status des Radios als Wert 0 = no override, 1 = off, 2 = on |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-frequenz"></a>
### STATUS_FREQUENZ

aktuelle Tunerfrequenz abfragen KWP2000: $21 ReadDataByLocalIdentifier $96 inputOutputLocalIdentifier - tuner frequency Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FREQ | unsigned long | Bereich: 150 - 108000 kHz entspricht 0,15 MHz bis 108 MHz |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-frequenz"></a>
### STEUERN_FREQUENZ

Tunerfrequenz einstellen KWP2000: $3B WriteDataByLocalIdentifier $96 inputOutputLocalIdentifier - tuner frequency Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREQUENZ | long | Bereich: 150 - 108000 [kHz] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rds"></a>
### STATUS_RDS

Lesen Status AF-Verfolgung und TP KWP2000: $21 ReadDataByLocalIdentifier $91 inputOutputLocalIdentifier  - - get RDS Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TP | int | Status TP 0 = off, 1 = on |
| STAT_AF | int | Status AF-Verfolgung 0 = off, 1 = on |
| STAT_RDS | int | Status RDS 0 = off, 1 = on |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-rds"></a>
### STEUERN_RDS

Steuern AF-Verfolgung und TP KWP2000: $3B WriteDataByLocalIdentifier $91 inputOutputLocalIdentifier - set RDS Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TP | string | Steuern TP 0 = off, 1 = on Werte siehe table TTunerRDS NAME |
| RDS | string | Steuern AF-Verfolgung und RDS 0 = off, 1 = on Werte siehe table TTunerRDS NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-qfs"></a>
### STATUS_ANT_QFS

Auslesen des Status Quality Fieldstrength KWP2000: $21 ReadDataByLocalIdentifier $92 inputOutputLocalIdentifier - signal quality Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_QUALITY | int | Quality Bereich: 0x00..0x0F(0..15)(der fuer die AF-Verfolgung massgebliche Wert, entspricht der Summe der gewichteten Einzelfaktoren, 15 = beste Qualitaet) 2-Tuner: Quality = 0 ! |
| STAT_FIELDSTRENGTH | int | Satus der Feldstärke Bereich: 0..15 Schritte (4dB-Schritte von 0..60 dBµV) |
| STAT_ANT_PW | int | Antenna Power Supply, Stromversorgung der Aktivantenne über Antennenkabel nur K48 relevant Bereich: 0 = OFF, 1..15 = ON |
| STAT_FIELDSTRENGTH_EXACT | int | Ausgabe der exakten Feldstärke Ausgabe in 1dB-Schritten, wobei 0xFF ungültig bedeutet |
| STAT_FREQUENZ | unsigned long | Bereich: 150 - 108000 kHz |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tuner-suchlauf"></a>
### STEUERN_TUNER_SUCHLAUF

Sendersuchlauf des AM/FM-Tuner starten KWP2000: $31 StartRoutineByLocalIdentifier $93 RoutineLocalIdentifier  - seek - Tuner_Suchlauf Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TUNER_SUCHLAUF | string | Steuern des Suchlaufs (ASC/DEC/STOP) table TTunerSuchlauf NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-steuern-tuner-suchlauf"></a>
### STOP_STEUERN_TUNER_SUCHLAUF

Sendersuchlauf des AM/FM-Tuner stoppen KWP2000: $32 StopRoutineByLocalIdentifier $93 RoutineLocalIdentifier  - seek - Tuner_Suchlauf Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-find-best-station"></a>
### STEUERN_FIND_BEST_STATION

Routine zur Suche des besten, verfügberen Senders KWP2000: $31 StartRoutineByLocalIdentifier $94 RoutineLocalIdentifier (find_best_station) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-waveband"></a>
### STEUERN_WAVEBAND

Umschalten der Radio-Quelle per Diagnose KWP2000: $31 StartRoutineByLocalIdentifier $95 RoutineLocalIdentifier  - waveband Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_WAVEBAND | string | Einzustellende Radioquelle Befehl in Textform einzugeben: z.B.: MW Werte aus table TWaveband Spalte TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-waveband"></a>
### STATUS_WAVEBAND

Status der Radio-Quelle per Diagnose KWP2000: $33 RequestRoutineResultsByLocalIdentifier $95 RoutineLocalIdentifier  - waveband Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WAVEBAND | int | Neue Radioquelle Werte aus table TWaveband |
| STAT_WAVEBAND_TEXT | string | Neue Radioquelle Werte aus table TWaveband |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-volume"></a>
### STATUS_VOLUME

Auslesen, welches Lautstärke Inkrement eingestellt ist KWP2000: $21 ReadDataByLocalIdentifier $80 recordLocalIdentifier - Volume audio step Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VOL_INC_TEXT | string | STATUS des Volume Inkrements in Text-Form table TVOL_INC NAME |
| STAT_VOL_INC | string | STATUS des Volume Inkrements table TVOL_INC WERT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-volume"></a>
### STEUERN_VOLUME

Einstellen der Audio-Lautstaerke KWP2000: $3B WriteDataByLocalIdentifier $80 inputOutputLocalIdentifier - set volume Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VOLUME | int | Ausgewaehlte Audio-Lautstaerke  table TVOL_INC WERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-balance"></a>
### STEUERN_BALANCE

Ansteuern eines AudioKanals bzw. Einstellen der Balance KWP2000: $3B WriteDataByLocalIdentifier $83 inputOutputLocalIdentifier  - balance Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BALANCE | string | Ausgewählte Balance  table TBalance NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-balance"></a>
### STATUS_BALANCE

Status eines AudioKanals bzw. Einstellen der Balance KWP2000: $21 ReadDataByLocalIdentifier $83 inputOutputLocalIdentifier  - balance Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BALANCE | string | Ausgewählte Balance  table TBalance NAME |
| STAT_BALANCE_RAW | char | Rohwert Balance |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fader"></a>
### STATUS_FADER

Status eines AudioKanals bzw. Einstellen des Faders KWP2000: $21 ReadDataByLocalIdentifier $84 inputOutputLocalIdentifier  - fader Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FADER | string | Ausgewählte Fader  table TFader NAME |
| STAT_FADER_RAW | char | Rohwert Fader |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fader"></a>
### STEUERN_FADER

Ansteuern eines AudioKanals bzw. Einstellen des Faders KWP2000: $3B WriteDataByLocalIdentifier $84 inputOutputLocalIdentifier  - fader Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FADER | string | Ausgewählte Fader  table TFader NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktive-gal-kurve"></a>
### STATUS_AKTIVE_GAL_KURVE

Reads the active coded speed dependent volume control curve  KWP2000: $21 ReadDataByLocalIdentifier $85 RecordLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GAL_KURVE | string | Active SDVC curve |
| STAT_GAL_KURVE_HEX | int | Numbert of active SDVC curve |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-gal-kurve"></a>
### STEUERN_GAL_KURVE

Schreibt die zu nutzende GAL-Kurve  KWP2000: $3B WriteDataByLocalIdentifier $85 RecordLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GAL_KURVE | char | Active SDVC curve Eingabe im Bereich 0-3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-source-control"></a>
### STEUERN_SOURCE_CONTROL

Umschalten der Entertainment-Quelle per Diagnose KWP2000: $3B WriteDataByLocalIdentifier $87 RoutineLocalIdentifier  - source control Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ENTSOURCE | int | Einzustellende Entertainment-quelle Werte aus table TEntSource MASKE Eingabe 0 bis 7 0: No source 1: Aux input 2: USB 3: iPod 4: AmFm tuner 5: Sirius tuner 7: Funk input |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-source-control"></a>
### STATUS_SOURCE_CONTROL

Status der Entertainment-Quelle per Diagnose KWP2000: $21 RequestRoutineResultsByLocalIdentifier $87 RoutineLocalIdentifier  - source control Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENTSOURCE | int | Neue Entertainmentquelle Werte aus table TEntSource |
| STAT_ENTSOURCE_TEXT | string | Neue Entertainmentquelle Werte aus table TEntSource |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bass"></a>
### STEUERN_BASS

Schreiben der Bass-Einstellung KWP2000: $3B writeDataByLocalIdentifier $81 recordLocalIdentifier - bass Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BASS | char | Bass-Einstellung Eingabe von -6 bis 6 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bass"></a>
### STATUS_BASS

Status der Bass-Einstellung KWP2000: $21 writeDataByLocalIdentifier $81 recordLocalIdentifier - bass Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BASS | char | Bass-Einstellung von -6 bis 6 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-treble"></a>
### STATUS_TREBLE

Status der Treble-Einstellung KWP2000: $21 writeDataByLocalIdentifier $82 recordLocalIdentifier - treble Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TREBLE | char | Treble-Einstellung von -6 bis 6 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-treble"></a>
### STEUERN_TREBLE

Schreiben der Treble-Einstellung KWP2000: $3B writeDataByLocalIdentifier $82 recordLocalIdentifier - treble Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TREBLE | char | Treble-Einstellung Eingabe von -6 bis 6 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mute"></a>
### STATUS_MUTE

Auslesen, ob Mute "ein" oder "aus" ist KWP2000: $21 ReadDataByLocalIdentifier $86 recordLocalIdentifier - mute Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUTE | string | Status Mute |
| STAT_MUTE_RAW | char | Status Mute 0 = off, 1 = on |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mute"></a>
### STEUERN_MUTE

Mute "ein" oder "aus" schalten KWP2000: $3B WriteDataByLocalIdentifier $86 recordLocalIdentifier - mute Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_MUTE | string | Steuern Mute "ein" oder "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-interne-temperatur"></a>
### STATUS_INTERNE_TEMPERATUR

Status des SG- Temperaturwertes KWP2000: $21 ReadDataByLocalIdentifier $D1 inputOutputLocalIdentifier - interal temperature Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TEMP_WERT | real | Zahlenwert der Temperatur |
| STAT_TEMP_EINH | string | Einheit von STAT_TEMP_WERT (Grad C) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-interne-spannung"></a>
### STATUS_INTERNE_SPANNUNG

Status der internen Batterie-Spannung des MCR KWP2000: $21 ReadDataByLocalIdentifier $D0 inputOutputLocalIdentifier - interal voltage Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPANNUNG_WERT | real | Zahlenwert der Spannung |
| STAT_SPANNUNG_EINH | string | Einheit von STAT_SPANNUNG_WERT (Volt) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-parrot-sw-hw-vers-lesen"></a>
### STATUS_PARROT_SW_HW_VERS_LESEN

Lesen der Parrot HW- und SW-Version KWP2000: $21 ReadDataByLocalIdentifier $B1 inputOutputLocalIdentifier - Parrot SW-HW-Version Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PARROT_HW_SW | string | Parrot HW- und SW-Version |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-parrot-bt-adresse-lesen"></a>
### STATUS_PARROT_BT_ADRESSE_LESEN

Lesen der Parrot BT-Adresse KWP2000: $21 ReadDataByLocalIdentifier $B0 inputOutputLocalIdentifier - Parrot BT-Adresse Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PARROT_BT_ADR | string | Parrot BT-Adresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-steuern-parrot-bt-adresse-schreiben"></a>
### STEUERN_PARROT_BT_ADRESSE_SCHREIBEN

Schreiben der Parrot BT-Adresse KWP2000: $3B WriteDataByLocalIdentifier $B0 inputOutputLocalIdentifier - Parrot BT-Adresse Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARROT_BT_ADR | string | Parrot BT-Adresse Eingabe 12stellig ohne Trennzeichen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-front-speaker-onoff"></a>
### STATUS_FRONT_SPEAKER_ONOFF

Zustand der vorderen Lautsprecher, sind sie ein oder aus geschalten? KWP2000: $21 ReadDataByLocalIdentifier $88 inputOutputLocalIdentifier  - switch Front Speaker on or off Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPEAKER_TEXT | string | Ein/aus-Status der Lautsprecher vorne ("on" oder "off") table TSpeaker NAME |
| STAT_SPEAKER | int | Ein/aus-Status der Lautsprecher vorne als Wert 0 = off, 1 = on |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-front-speaker-onoff"></a>
### STEUERN_FRONT_SPEAKER_ONOFF

Zustand der vorderen Lautsprecher, sind sie ein oder aus geschalten? KWP2000: $3B WriteDataByLocalIdentifier $88 inputOutputLocalIdentifier  - switch Front Speaker on or off Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FRONT_SPEAKER | string | EIN/AUS-Schalten der vorderen Lautsprecher table TSpeaker NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rear-speaker-onoff"></a>
### STATUS_REAR_SPEAKER_ONOFF

Zustand der vorderen Lautsprecher, sind sie ein oder aus geschalten? KWP2000: $21 ReadDataByLocalIdentifier $89 inputOutputLocalIdentifier  - switch Rear Speaker on or off Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPEAKER_TEXT | string | Ein/aus-Status der Lautsprecher hinten ("on" oder "off") table TSpeaker NAME |
| STAT_SPEAKER | char | Ein/aus-Status der Lautsprecher hinten als Wert 0 = off, 1 = on |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-rear-speaker-onoff"></a>
### STEUERN_REAR_SPEAKER_ONOFF

Zustand der vorderen Lautsprecher, sind sie ein oder aus geschalten? KWP2000: $3B WriteDataByLocalIdentifier $89 inputOutputLocalIdentifier  - switch Rear Speaker on or off Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REAR_SPEAKER | string | EIN/AUS-Schalten der hinteren Lautsprecher Tabelle TSpeaker NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-loudness-onoff"></a>
### STATUS_LOUDNESS_ONOFF

Zustand der Funktion Loudness, ist sie ein oder aus geschalten? KWP2000: $21 ReadDataByLocalIdentifier $8A inputOutputLocalIdentifier  - switch LOUDNESS on or off Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LOUDNESS_TEXT | string | Ein/aus-Status der Loudness ("on" oder "off") table TLoudness NAME |
| STAT_LOUDNESS | char | Ein/aus-Status der Lautsprecher hinten als Wert 0 = off, 1 = on |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-loudness-onoff"></a>
### STEUERN_LOUDNESS_ONOFF

Zustand der Funktion Loudness, ist sie ein oder aus geschalten? KWP2000: $3B WriteDataByLocalIdentifier $8A inputOutputLocalIdentifier  - switch Loudness on or off Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOUDNESS | string | EIN/AUS-Schalten der Funktion Loudness Tabelle TLoudness NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bluetooth-onoff"></a>
### STATUS_BLUETOOTH_ONOFF

Zustand der Funktion BLUETOOTH, ist sie ein oder aus geschalten? KWP2000: $21 ReadDataByLocalIdentifier $B2 inputOutputLocalIdentifier  - switch BLUETOOTH on or off Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BLUETOOTH_TEXT | string | Ein/aus-Status der Funktion Bluetooth ("on" oder "off") table TBluetooth NAME |
| STAT_BLUETOOTH | char | Ein/aus-Status der Funktion Bluetooth als Wert 0 = off, 1 = on table TBluetooth MASKE |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bluetooth-onoff"></a>
### STEUERN_BLUETOOTH_ONOFF

Zustand der Funktion Bluetooth, ist sie ein oder aus geschalten? KWP2000: $3B WriteDataByLocalIdentifier $B2 inputOutputLocalIdentifier  - switch bluetooth on or off Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLUETOOTH | string | EIN/AUS-Schalten der Funktion Bluetooth mit "on"/"ein"/"1" oder "off"/"aus"/"0" table TBluetooth NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bluetooth-eol-test"></a>
### STEUERN_BLUETOOTH_EOL_TEST

Schreiben der Parrot BT-Adresse KWP2000: $31 StartRoutineByLocalIdentifier $B3 inputOutputLocalIdentifier - Bluetooth EOL Test Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BT_ADR | string | Parrot BT-Adresse Eingabe 12stellig ohne Trennzeichen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-stop-steuern-bluetooth-eol-test"></a>
### STOP_STEUERN_BLUETOOTH_EOL_TEST

Schreiben der Parrot BT-Adresse KWP2000: $32 StopRoutineByLocalIdentifier $B3 inputOutputLocalIdentifier - Bluetooth EOL Test Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-routine-bluetooth-eol-test"></a>
### STATUS_ROUTINE_BLUETOOTH_EOL_TEST

Dieser Routine Service liefert das Ergebnis der Bluetooth Suche nach dem angegebenen Gerät. Ist die Suche abgeschlossen bleibt das Ergebnis solange gültig, bis eine neue Suche gestartet wird. KWP2000: $33 RequestRoutineResultsByLocalIdentifier $B3 inputOutputLocalIdentifier - Bluetooth EOL Test Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ROUTINE_BLUETOOTH_EOL_TEST_TEXT | string | Ergebnis der BT-Suche nach gesuchtem Geraet table TBluetooth_EOL_Test TEXT |
| STAT_ROUTINE_BLUETOOTH_EOL_TEST | int | Ergebnis der BT-Suche nach gesuchtem Geraet als Wert table TBluetooth_EOL_Test MASKE |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-usb-ipod"></a>
### STATUS_USB_IPOD

KWP2000: $21 RequestRoutineResultsByLocalIdentifier $B4 RoutineLocalIdentifier (USB/iPod Device Diagnostics) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_USB_IPOD | int | Status USB/IPOD |
| STAT_USB_IPOD_TEXT | string | Textausgabe Status USB/IPOD |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-find-best-station"></a>
### STATUS_FIND_BEST_STATION

KWP2000: $33 RequestRoutineResultsByLocalIdentifier $94 RoutineLocalIdentifier (find_best_station) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SEARCHING_PROCESS_STATUS | string | Status des Suchprozesses Werte siehe table TProcessStat TEXT |
| STAT_SEARCHING_PROCESS_STATUS_RAW | unsigned char | Rohwert Status Suchprozess |
| STAT_NAME | string | PS-Name der gefundenen Station |
| STAT_PI | unsigned int | PI der gefundenen Station |
| STAT_FIELDSTRENGTH | unsigned char | Feldstärke der gefundenen Station |
| STAT_QUALITY | unsigned char | PS-Name der gefundenen Station |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sirius-sn-lesen"></a>
### STATUS_SIRIUS_SN_LESEN

Lesen der Sirius Seriennummer KWP2000: $21 ReadDataByLocalIdentifier $C0 inputOutputLocalIdentifier - Parrot BT-Adresse Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SIRIUS_SN | string | Sirius Seriennummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-sirius-fw"></a>
### STATUS_SIRIUS_FW

Lesen der Sirius Firmwarenummer KWP2000: $21 ReadDataByLocalIdentifier $C1 inputOutputLocalIdentifier - Firmwarenummer Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SIRIUS_FW | string | Sirius Firmwarenummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-sirius-signal"></a>
### STATUS_SIRIUS_SIGNAL

Status des Sirius Signals per Diagnose KWP2000: $21 RequestRoutineResultsByLocalIdentifier $C2 RoutineLocalIdentifier  - sirius signal Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SAT_SIG | int | Qualitaet Satellit Signal Werte aus table TSSig |
| STAT_SAT_SIG_TEXT | string | Qualitaet Satellit Signal Werte aus table TSSig |
| STAT_TERR_SIG | int | Qualitaet terrestrisches Signal Werte aus table TSSig |
| STAT_TERR_SIG_TEXT | string | Qualitaet terrestrisches Signal Werte aus table TSSig |
| STAT_ZUS_SIG | int | Qualitaet zusammengesetztes Signal Werte aus table TSSig |
| STAT_ZUS_SIG_TEXT | string | Qualitaet zusammengesetztes Signal Werte aus table TSSig |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sirius-factorydefault"></a>
### STEUERN_SIRIUS_FACTORYDEFAULT

Sirius Empfaenger auf Werkseinstellung zuruecksetzen KWP2000: $3B WriteDataByLocalIdentifier $C3 inputOutputLocalIdentifier - sirius factory default Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DEFAULT_EIN | int | 0 = Empfaenger nicht zuruecksetzen 1 = Empfaenger zuruecksetzen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sirius-factorydefault"></a>
### STATUS_SIRIUS_FACTORYDEFAULT

Lesen des Sirius Werkseinstellungsstatus KWP2000: $21 ReadDataByLocalIdentifier $C3 inputOutputLocalIdentifier - Werkseinstellung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SIRIUS_DEFAULT | char | 0 = Empfaenger nicht zurueckgesetzt 1 = Empfaenger zurueckgesetzt |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-steuern-sirius-tunermodus"></a>
### STEUERN_SIRIUS_TUNERMODUS

Waehlt den Sirius Tunermodus KWP2000: $3B WriteDataByLocalIdentifier $C4 inputOutputLocalIdentifier  - Sirius tunermode Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TUNERMODUS | string | Sirius Modus aus Tabelle TSMode auswaehlen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sirius-tunermodus"></a>
### STATUS_SIRIUS_TUNERMODUS

Gewaehlter Sirius Tunermodus KWP2000: $21 ReadDataByLocalIdentifier $C4 inputOutputLocalIdentifier  - Sirius tunermode Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TUNERMODUS_TEXT | string | Sirius Modus aus Tabelle TSMode |
| STAT_TUNERMODUS | char | Sirius Tunermodus Wert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sirius-bitfehlerrate"></a>
### STATUS_SIRIUS_BITFEHLERRATE

Lesen der Sirius Bitfehlerrate KWP2000: $21 ReadDataByLocalIdentifier $C5 inputOutputLocalIdentifier - Bitfehlerrate Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BITFEHLERRATE | int | Bitfehlerrate in Fehler/50000 bit |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-steuern-sirius-signalgen"></a>
### STEUERN_SIRIUS_SIGNALGEN

Ansteuern der Kanaele im Signalgeneratormodus KWP2000: $3B WriteDataByLocalIdentifier $C6 inputOutputLocalIdentifier - Signalgenerator Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREQUENZ_LINKS | int | Frequenzwert linker Kanal Bereich: 0 - 15999 [Hz] |
| FREQUENZ_RECHTS | int | Frequenzwert rechter Kanal Bereich: 0 - 15999 [Hz] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sirius-signalgen"></a>
### STATUS_SIRIUS_SIGNALGEN

Lesen der Sirius Bitfehlerrate KWP2000: $21 ReadDataByLocalIdentifier $C6 inputOutputLocalIdentifier - Signalgenerator Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FREQUENZ_LINKS | int | Frequenzwert linker Kanal Bereich: 0 - 15999 [Hz] |
| STAT_FREQUENZ_RECHTS | int | Frequenzwert rechter Kanal Bereich: 0 - 15999 [Hz] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

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
- [JOBRESULTEXTENDED](#table-jobresultextended) (7 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (27 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [TSCHALTMODI](#table-tschaltmodi) (8 × 3)
- [TTUNERRDS](#table-ttunerrds) (3 × 3)
- [TTUNERSUCHLAUF](#table-ttunersuchlauf) (4 × 3)
- [TTUNERBESTSTATION](#table-ttunerbeststation) (6 × 3)
- [TWAVEBAND](#table-twaveband) (7 × 2)
- [TVOL_INC](#table-tvol-inc) (23 × 3)
- [TBALANCE](#table-tbalance) (22 × 3)
- [TFADER](#table-tfader) (22 × 3)
- [TENTSOURCE](#table-tentsource) (8 × 2)
- [TPROCESSSTAT](#table-tprocessstat) (6 × 2)
- [TSPEAKER](#table-tspeaker) (7 × 3)
- [TLOUDNESS](#table-tloudness) (7 × 3)
- [TBLUETOOTH](#table-tbluetooth) (7 × 3)
- [TBLUETOOTH_EOL_TEST](#table-tbluetooth-eol-test) (5 × 3)
- [TUSBANSCHLUSS](#table-tusbanschluss) (5 × 3)
- [TUSBFORMATIERT](#table-tusbformatiert) (5 × 3)
- [TSSIG](#table-tssig) (5 × 2)
- [TSMODE](#table-tsmode) (4 × 2)

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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | ERROR_ARGUMENT_NOT_IN_TABLE |
| 0x01 | ERROR_INVALID_ARGUMENT |
| 0x02 | ERROR_MISSING_ARGUMENT |
| 0x03 | ERROR_EXECUTION_LOCALROUTINE |
| 0x04 | ERROR_ARGUMENT_TOO_LONG |
| 0x05 | ERROR_INVALID_RESULT |
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

Dimensions: 27 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9908 | Leitungsunterbrechung Lautsprecher links |
| 0x9909 | Leitungsunterbrechung Lautsprecher rechts |
| 0x990A | Kurzschluss nach Masse Lautsprecher links |
| 0x990B | Kurzschluss nach Masse Lautsprecher rechts |
| 0x990C | Kurzschluss nach plus Lautsprecher links |
| 0x990D | Kurzschluss nach plus Lautsprecher rechts |
| 0x9912 | Connector 2 ist nicht angeschlossen |
| 0x9913 | Connector 4 ist nicht angeschlossen |
| 0x991B | Leitungsunterbrechung BT-Antenne |
| 0x991D | Abschalten nach Überhitzung Audioplattform |
| 0x991E | Übertemperatur Verstärker |
| 0x991F | Überspannung Verstärker |
| 0x9920 | Unterspannung Verstärker |
| 0x9921 | Kurzschluss  USB |
| 0x9922 | Kurzschluss Lautsprecher links |
| 0x9923 | Kurzschluss Lautsprecher rechts |
| 0x9925 | FM/AM Tuner interner Fehler |
| 0x9926 | Überspannung USB |
| 0x9927 | Leitungsunterbrechung Sirius Antenne |
| 0x9928 | Kurzschluss Sirius Antenne |
| 0x9941 | CAN Time Out Bedienung_Radio (750ms) |
| 0x9942 | CAN Time Out Geschwindigkeit (750ms) |
| 0x9943 | CAN Time Out Kombidaten (5000ms) |
| 0x9944 | CAN Time Out Motordaten_1 (750ms) |
| 0x9946 | EEPROM |
| 0x9947 | CAN_BUS_OFF |
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

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xFFFF | 0x01 | 0x02 | 0x03 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Geschwindigkeit | km/h | - | unsigned char | - | 1 | 1 | 0 |
| 0x02 | interne Spannung | Volt | - | unsigned char | - | 1 | 10 | 0 |
| 0x03 | Innentemperatur | Celsius | - | unsigned char | - | 1 | 1 | -40 |
| 0xFF | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

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

<a id="table-tschaltmodi"></a>
### TSCHALTMODI

Dimensions: 8 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| no override | 0x00 | keine Beeinflussung |
| off | 0x01 | Audio Plattform aus |
| aus | 0x01 | Audio Plattform aus |
| 1 | 0x01 | Audio Plattform aus |
| on | 0x02 | Audio Plattform ein |
| ein | 0x02 | Audio Plattform ein |
| 2 | 0x02 | Audio Plattform ein |
| Fehler | 0xXY | Nicht definiert |

<a id="table-ttunerrds"></a>
### TTUNERRDS

Dimensions: 3 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| 0 | 0x00 | aus |
| 1 | 0x01 | ein |
| Fehler | 0xXY | Nicht definiert |

<a id="table-ttunersuchlauf"></a>
### TTUNERSUCHLAUF

Dimensions: 4 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| STOP | 0x02 | Stop searching |
| ASC | 0x01 | Ascending search |
| DEC | 0x00 | Descending search |
| Fehler | 0xXY | - |

<a id="table-ttunerbeststation"></a>
### TTUNERBESTSTATION

Dimensions: 6 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| 0 | 0x00 | process not started |
| 1 | 0x01 | process running |
| 2 | 0x02 | process finished and best station found |
| 3 | 0x03 | process finished and no best station found |
| 4 | 0x04 | searching process halted |
| Fehler | 0xXY | - |

<a id="table-twaveband"></a>
### TWAVEBAND

Dimensions: 7 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | FM |
| 0x01 | LW |
| 0x02 | MW/AM |
| 0x03 | KW/SW |
| 0x04 | WB |
| 0x05 | TRF |
| 0xFF | Entertainmentsource not available |

<a id="table-tvol-inc"></a>
### TVOL_INC

Dimensions: 23 rows × 3 columns

| MASKE | NAME | WERT |
| --- | --- | --- |
| 0x00 | Mute | 0 |
| 0x01 | Inkrement 01 | 1 |
| 0x02 | Inkrement 02 | 2 |
| 0x03 | Inkrement 03 | 3 |
| 0x04 | Inkrement 04 | 4 |
| 0x05 | Inkrement 05 | 5 |
| 0x06 | Inkrement 06 | 6 |
| 0x07 | Inkrement 07 | 7 |
| 0x08 | Inkrement 08 | 8 |
| 0x09 | Inkrement 09 | 9 |
| 0x0A | Inkrement 10 | 10 |
| 0x0B | Inkrement 11 | 11 |
| 0x0C | Inkrement 12 | 12 |
| 0x0D | Inkrement 13 | 13 |
| 0x0E | Inkrement 14 | 14 |
| 0x0F | Inkrement 15 | 15 |
| 0x10 | Inkrement 16 | 16 |
| 0x11 | Inkrement 17 | 17 |
| 0x12 | Inkrement 18 | 18 |
| 0x13 | Inkrement 19 | 19 |
| 0x14 | Maximal | 20 |
| 0xFF | Bluetooth | 21 |
| 0xXY | Nicht definiert | 22 |

<a id="table-tbalance"></a>
### TBALANCE

Dimensions: 22 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| -10 | 0xF6 | Links |
| -9 | 0xF7 | Links -9 |
| -8 | 0xF8 | Links -8 |
| -7 | 0xF9 | Links -7 |
| -6 | 0xFA | Links -6 |
| -5 | 0xFB | Links -5 |
| -4 | 0xFC | Links -4 |
| -3 | 0xFD | Links -3 |
| -2 | 0xFE | Links -2 |
| -1 | 0xFF | Links -1 |
| 0 | 0x00 | Balance |
| 1 | 0x01 | Rechts 1 |
| 2 | 0x02 | Rechts 2 |
| 3 | 0x03 | Rechts 3 |
| 4 | 0x04 | Rechts 4 |
| 5 | 0x05 | Rechts 5 |
| 6 | 0x06 | Rechts 6 |
| 7 | 0x07 | Rechts 7 |
| 8 | 0x08 | Rechts 8 |
| 9 | 0x09 | Rechts 9 |
| 10 | 0x0A | Rechts |
| XY | 0xXY | Nicht definiert |

<a id="table-tfader"></a>
### TFADER

Dimensions: 22 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| -10 | 0xF6 | Hinten |
| -9 | 0xF7 | Hinten -9 |
| -8 | 0xF8 | Hinten -8 |
| -7 | 0xF9 | Hinten -7 |
| -6 | 0xFA | Hinten -6 |
| -5 | 0xFB | Hinten -5 |
| -4 | 0xFC | Hinten -4 |
| -3 | 0xFD | Hinten -3 |
| -2 | 0xFE | Hinten -2 |
| -1 | 0xFF | Hinten -1 |
| 0 | 0x00 | Fader |
| 1 | 0x01 | Vorne 1 |
| 2 | 0x02 | Vorne 2 |
| 3 | 0x03 | Vorne 3 |
| 4 | 0x04 | Vorne 4 |
| 5 | 0x05 | Vorne 5 |
| 6 | 0x06 | Vorne 6 |
| 7 | 0x07 | Vorne 7 |
| 8 | 0x08 | Vorne 8 |
| 9 | 0x09 | Vorne 9 |
| 10 | 0x0A | Vorne |
| XY | 0xXY | Nicht definiert |

<a id="table-tentsource"></a>
### TENTSOURCE

Dimensions: 8 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | no source |
| 0x01 | AUX Input |
| 0x02 | USB |
| 0x03 | iPod |
| 0x04 | AmFm Tuner |
| 0x05 | Sirius Tuner |
| 0x06 | Internal sine generator |
| 0xFF | Entertainmentsource not available |

<a id="table-tprocessstat"></a>
### TPROCESSSTAT

Dimensions: 6 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | process not started |
| 0x01 | process running |
| 0x02 | process finished and best station found |
| 0x03 | process finished and no best station found |
| 0x04 | searching process halted |
| 0xXY | Fehler |

<a id="table-tspeaker"></a>
### TSPEAKER

Dimensions: 7 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| off | 0x00 | Speaker off |
| aus | 0x00 | Lautsprecher aus |
| 0 | 0x00 | Lautsprecher aus |
| on | 0x01 | Speaker on |
| ein | 0x01 | Lautsprecher ein |
| 1 | 0x01 | Lautsprecher ein |
| Fehler | 0xXY | Nicht definiert |

<a id="table-tloudness"></a>
### TLOUDNESS

Dimensions: 7 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| off | 0x00 | Loudness off |
| aus | 0x00 | Loudness aus |
| 0 | 0x00 | Loudness aus |
| on | 0x01 | Loudness on |
| ein | 0x01 | Loudness ein |
| 1 | 0x01 | Loudness ein |
| Fehler | 0xXY | Nicht definiert |

<a id="table-tbluetooth"></a>
### TBLUETOOTH

Dimensions: 7 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| off | 0x00 | Bluetooth off |
| aus | 0x00 | Bluetooth aus |
| 0 | 0x00 | Bluetooth off/aus |
| on | 0x01 | Bluetooth on |
| ein | 0x01 | Bluetooth ein |
| 1 | 0x01 | Bluetooth on/ein |
| Fehler | 0xXY | Nicht definiert |

<a id="table-tbluetooth-eol-test"></a>
### TBLUETOOTH_EOL_TEST

Dimensions: 5 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| 0 | 0x00 | None (a search has not yet been completed, or the last search was aborted before completion) |
| 1 | 0x01 | A search is currently in progress |
| 2 | 0x02 | A search has completed, and the device was found successfully |
| 3 | 0x03 | A search has completed, but it failed to find the device |
| Fehler | 0xXY | - |

<a id="table-tusbanschluss"></a>
### TUSBANSCHLUSS

Dimensions: 5 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| no | 0x00 | no USB device connected |
| nein | 0x00 | keine USB-Quelle vorhanden |
| yes | 0x01 | USB device connected |
| ja | 0x01 | USB-Quelle vorhanden |
| Fehler | 0xXY | Nicht definiert |

<a id="table-tusbformatiert"></a>
### TUSBFORMATIERT

Dimensions: 5 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| no | 0x00 | connected USB device is not formatted |
| nein | 0x00 | verbundene USB-Quelle ist nicht formatiert |
| yes | 0x01 | connected USB device is formatted |
| ja | 0x01 | verbundene USB-Quelle ist formatiert |
| Fehler | 0xXY | Nicht definiert |

<a id="table-tssig"></a>
### TSSIG

Dimensions: 5 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | Kein Signal |
| 0x01 | Schwaches Signal |
| 0x02 | Gutes Signal |
| 0x03 | Hervorragendes Signal |
| 0xFF | Signal ungueltig |

<a id="table-tsmode"></a>
### TSMODE

Dimensions: 4 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | Ungueltig |
| 0x01 | Signalgenerator-Modus |
| 0x02 | Bitfehlerrate-Modus |
| 0x03 | Sender-Modus |
