# mcgw60.prg

- Jobs: [91](#jobs)
- Tables: [33](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MCGW fuer E60 im Geraet MASK |
| ORIGIN | BMW EE-40  Koenigseder |
| REVISION | 3.31 |
| AUTHOR | BECKER SDE Hr. Kroell,Hr.Bubb EI-44 |
| COMMENT | Stand 24.01.2007 |
| PACKAGE | 1.36 |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
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
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [MOST_VERSION_LESEN](#job-most-version-lesen) - Auslesen von Most Version KWP2000: $21 ReadDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $A0 MOSTVersion MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_MOST_3DB](#job-status-most-3db) - Auslesen des Status der Lichtleistungsabsenkung KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STEUERN_MOST_3DB](#job-steuern-most-3db) - Lichtleistungsabsenkung einschalten KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AF OpticalTransmitPowSwitch $00 S1 geoeffnet = 3dB Absenkung MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_WAKE_UP_STATUS](#job-status-wake-up-status) - Auslesen des Status WakeupStatus KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_ABILITY_TO_WAKE](#job-status-ability-to-wake) - Auslesen des Status AbilityToWake KWP2000: $21 ReadByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD WakeUpStatus MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STEUERN_ABILITY_TO_WAKE](#job-steuern-ability-to-wake) - AbilityToWake einstellen KWP2000: $3B WriteDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $AD AbilityToWake $00 of, $01 on, $02 critical MOST Funktionenkatalog 5.0.0, Januar 2000 Seite 43 
- [STATUS_VERSION_GATEWAYTABELLE](#job-status-version-gatewaytabelle) - Lesen der Versionsnummer der Gateway-Tabelle KWP2000: $22 ReadDataByCommonIdentifier $100D recordCommonIdentifier (gatewayTableVersionNumber) Modus  : Default
- [STATUS_GATEWAY_WAKEUP_SOURCE](#job-status-gateway-wakeup-source) - Liefert die Quelle/Ursache zurück, die zum Wecken des Gateway-Steuergerätes geführt hat. Dieser Job wird von SG ab E60 unterstützt! KWP2000: $21 ReadDataByLocalIdentifier $BB recordLocalIdentifier Modus  : Default
- [STATUS_GATEWAY_OWN_DEVICE_ID](#job-status-gateway-own-device-id) - Information über den Gateway-Dispatcher Eigene logische MOST Device-ID KWP2000: $21 ReadDataByLocalIdentifier $B0 recordLocalIdentifier Modus  : Default
- [STATUS_GATEWAY_MOST_DEVICE_COUNT](#job-status-gateway-most-device-count) - Information über den Gateway-Dispatcher Anzahl der vom Dispatcher erkannten MOST-Teilnehmer im Ring KWP2000: $21 ReadDataByLocalIdentifier $B1 recordLocalIdentifier Modus  : Default
- [STATUS_GATEWAY_MOST_DEVICES](#job-status-gateway-most-devices) - Ausgabe der erkannten MOST-Devices. Die Erkennung erfolgt ueber die InstID der Diagnose-Funktionsbloecke KWP2000: $21 ReadDataByLocalIdentifier $B2 recordLocalIdentifier Modus  : Default
- [STATUS_GATEWAY_LOCAL_REGISTRY_ELEMENTS](#job-status-gateway-local-registry-elements) - Information über den Gateway-Dispatcher Liste aller lokal (im Gateway-Adreßraum) registrierten FBlocks KWP2000: $21 ReadDataByLocalIdentifier $B2 recordLocalIdentifier Modus  : Default
- [STATUS_GATEWAY_EXTERNAL_REGISTRY_ELEMENTS](#job-status-gateway-external-registry-elements) - Information über den Gateway-Dispatcher Liste aller extern (im MMI-Adreßraum) registrierten FBlocks KWP2000: $21 ReadDataByLocalIdentifier $B3 recordLocalIdentifier Modus  : Default
- [STATUS_GATEWAY_EVENT_SINK_COUNT](#job-status-gateway-event-sink-count) - Information über den Gateway-Dispatcher Anzahl der am Dispatcher registrierten Event-Kommunikationsteilnehmer KWP2000: $21 ReadDataByLocalIdentifier $B4 recordLocalIdentifier Modus  : Default
- [STATUS_PRAEPROZESSOR_SWITCH](#job-status-praeprozessor-switch) - Read out status of pre-processor switch KWP2000: $21 ReadDataByLocalIdentifier $BC recordLocalIdentifier - pre-processor switch state Modus  : Default
- [STATUS_INCLUDED_GW_TAB](#job-status-included-gw-tab) - Read out status of included GW table KWP2000: $21 ReadDataByLocalIdentifier $BD recordLocalIdentifier - included GW table state Modus  : Default
- [STATUS_HW_REF_GW](#job-status-hw-ref-gw) - Auslesen der HW-Referenz des Gateways KWP2000: $21 readDataByLocalIdentifier $FB recordLocalIdentifier Modus  : Default
- [STATUS_HW_NUM_GW](#job-status-hw-num-gw) - Auslesen der HW-Nummer des Gateways KWP2000: $21 readDataByLocalIdentifier $FB recordLocalIdentifier Modus  : Default
- [STEUERN_REPAIR_GW_PROGSTATE9](#job-steuern-repair-gw-progstate9) - Reparieren des Programmierstatus 9 beim Gateways KWP2000: $21 readDataByLocalIdentifier $FB recordLocalIdentifier Modus  : Default
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Ansteuerung des Selbsttests Gateway-Rechner - Test der IPC (interprocessor communication) - Speichertests RAM, FLASH_ROM, EEPROM - Test der Werte des Helligkeitssensors auf Plausibilität - Ueberpruefung der Temperatur Bei Erkennung eines Fehlverhaltens erfolgt ein Eintrag im Primaer- und Shadowfehlerspeicher. KWP2000: $31 StartRoutineByLocalIdentifier $04 routineLocalIdentifier (selfTest) Modus  : Default
- [DISABLE_MCGW](#job-disable-mcgw) - Schaltet die Umsetzung im MOST/CAN-Gateway vollständig ab. Die Eigendiagnose des Gateways von MOST und CAN aus ist noch möglich KWP2000: $31 StartRoutineByLocalIdentifier $0F routineLocalIdentifier (disableMCGW) Modus  : Default
- [ENABLE_MCGW](#job-enable-mcgw) - Schaltet die Umsetzung im MOST/CAN-Gateway wieder ein. Damit das MCGW die Nachrichtenumsetzung wieder aufnimmt, muß das MCGW von beiden Testern freigegeben werden KWP2000: $32 StopRoutineByLocalIdentifier $0F routineLocalIdentifier (enableMCGW) Modus  : Default
- [STATUS_ANALOG_SPANNUNG](#job-status-analog-spannung) - Auslesen der Spannungswerte von Board, SH3 und FPGA KWP2000: $30 InputOutputControlByLocalIdentifier $02 inputOutputLocalIdentifier $07 shortTermAdjustment Modus  : Default
- [STATUS_ANALOG_TEMPERATUR](#job-status-analog-temperatur) - Status der Temperaturwerte FOT Board, Mod4020 und Endstufe KWP2000: $30 InputOutputControlByLocalIdentifier $03 inputOutputLocalIdentifier $07 shortTermAdjustment Modus  : Default
- [STEUERN_ZENTRALE_REGISTRY_SOLLKONFIGURATION](#job-steuern-zentrale-registry-sollkonfiguration) - Ausgelesene Zentrale Registry wird als Sollkonfiguration abgespeichert KWP2000: $30 InputOutputControlByLocalIdentifier $06 inputOutputLocalIdentifier $07 ShortTermAdjustment Modus  : Default
- [READ_CURRENT_REGISTRY](#job-read-current-registry) - Auslesen der Registry vom ASK KWP2000: $21 ReadDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $B5 recordLocalIdentifier Modus   : Default
- [READ_DEFAULT_REGISTRY](#job-read-default-registry) - Auslesen der Registry vom ASK KWP2000: $21 ReadDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $B6 recordLocalIdentifier Modus   : Default
- [hw_nummer_lesen](#job-hw-nummer-lesen) - Hardware-Nummer lesen KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber Modus  : Default
- [STEUERN_LUEFTER](#job-steuern-luefter) - Setzen der Lüfterwerte KWP2000: $30 InputOutputControlByLocalIdentifier $04 inputOutputLocalIdentifier Modus  : Default
- [STATUS_LUEFTER](#job-status-luefter) - Lesen der Lüfterwerte KWP2000: $21 ReadDataByLocalIdentifier $B7 recordLocalIdentifier Modus  : Default
- [STEUERN_TEMPERATURABSCHALTWERTE](#job-steuern-temperaturabschaltwerte) - Setzen der Temperaturabschaltwerte Alle Werte sind in °C anzugeben KWP2000: $3B WriteDataByLocalIdentifier $B8 localIdentifier Modus  : Default
- [STATUS_TEMPERATURABSCHALTWERTE](#job-status-temperaturabschaltwerte) - Lesen der Temperaturabschaltwerte KWP2000: $21 ReadDataByLocalIdentifier $B8 recordLocalIdentifier Modus  : Default
- [STATUS_TASTE_GEDRUECKT](#job-status-taste-gedrueckt) - Auslesen, ob gerade eine Taste gedrueckt ist KWP2000: $21 ReadDataByLocalIdentifier $B9 recordLocalIdentifier - any key pressed Modus  : Default
- [STATUS_TEL_MUTE](#job-status-tel-mute) - Ausgabe, ob Tel-Mute-Leitung aktiv oder inaktiv ist KWP2000: $21 ReadDataByLocalIdentifier $BA recordLocalIdentifier Modus  : Default
- [read_sahara_sw_number](#job-read-sahara-sw-number) - Lesen der Sahara Software Version Nummer KWP2000: $21 ReadDataByLocalIdentifier $FD recordLocalIdentifier Modus  : Default
- [STATUS_LUEFTER_CTRL_DATA](#job-status-luefter-ctrl-data) - Lesen der Lüftersteuerungsparameter KWP2000: $21 ReadDataByLocalIdentifier $FC recordLocalIdentifier Modus  : Default
- [STEUERN_LUEFTER_CTRL_DATA](#job-steuern-luefter-ctrl-data) - Setzen der Lüfter Steuer Daten KWP2000: $3B WriteDataByLocalIdentifier $21 localIdentifier Modus  : Default
- [STATUS_IS_POWERFOLLOWUP](#job-status-is-powerfollowup) - Infospeicher u. Details 0xA18B lesen und auswerten KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry
- [READ_DIFF_REGISTRY](#job-read-diff-registry) - Vergleich der Current und Default Registry vom ASK KWP2000: $21 ReadDataByLocalIdentifier $B5 recordLocalIdentifier $B6 recordLocalIdentifier
- [CHECK_1C55](#job-check-1c55) - Datenbyte 0x1C55 prüfen KWP2000: $31 StartRoutineByLocalIdentifier $FA systemSupplierSpecific $39 localIdentifier Modus  : Default
- [READ_RIT](#job-read-rit) - Auslesen der Routing Information Table eines beliebigen MOST-Devices KWP2000: $21 ReadDataByLocalIdentifier $C0 recordLocalIdentifier  (via LESE_MOSTREGISTER) Modus   : Default
- [LESE_MOSTREGISTER](#job-lese-mostregister) - Es wird ein bestimmtes MOST-Register eines bestimmten MOST-Devices ausgelesen KWP2000: $21 ReadDataByLocalIdentifier $C0 recordLocalIdentifier Modus   : Default
- [STATUS_SEARCH_FBLOCK](#job-status-search-fblock) - Suche Fblock,InstID KWP2000: $21 ReadDataByLocalIdentifier $B5 recordLocalIdentifier
- [STATUS_FAN_HISTORY](#job-status-fan-history) - Lesen des Lüfteransteuerungsverlaufs für den Normalbetrieb KWP2000: $21 ReadDataByLocalIdentifier $FB recordLocalIdentifier Modus  : Default
- [STEUERN_CLEAR_FAN_HISTORY](#job-steuern-clear-fan-history) - Löschen des Lüfteransteuerungsverlaufs KWP2000: $31 StartRoutineByLocalIdentifier $FB systemSupplierSpecific Modus  : Default
- [READ_DEVIDS_CURRENT_REGISTRY](#job-read-devids-current-registry) - Auslesen der DEVIDS der Current Registry KWP2000: $21 ReadDataByLocalIdentifier $BC recordLocalIdentifier Modus   : Default
- [READ_DEVIDS_DEFAULT_REGISTRY](#job-read-devids-default-registry) - Auslesen der DEVIDS der Default Registry KWP2000: $21 ReadDataByLocalIdentifier $BE recordLocalIdentifier Modus   : Default
- [READ_FBLOCKS_CURRENT_REGISTRY](#job-read-fblocks-current-registry) - Auslesen der FBlockIDs einer DEVID der Current Registry KWP2000: $21 ReadDataByLocalIdentifier $BD recordLocalIdentifier Modus   : Default
- [READ_FBLOCKS_DEFAULT_REGISTRY](#job-read-fblocks-default-registry) - Auslesen der FBlockIDs einer DEVID der Default Registry KWP2000: $21 ReadDataByLocalIdentifier $BF recordLocalIdentifier Modus   : Default
- [WRITE_NEWSEELAND](#job-write-newseeland) - Neuseeland Tuner Parametersatz ändern Modus  : Default
- [STATUS_CHECK_ADC](#job-status-check-adc) - Datenbyte 0x1E05 prüfen KWP2000: $31 StartRoutineByLocalIdentifier $FA systemSupplierSpecific $39 localIdentifier Modus  : Default
- [STEUERN_ADC_ANHEBUNG](#job-steuern-adc-anhebung) - Datenblock ins EEProm schreiben KWP2000: $31 StartRoutineByLocalIdentifier $FA systemSupplierSpecific $37 localIdentifier Modus  : Default

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

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-blocklaenge-lesen"></a>
### FLASH_BLOCKLAENGE_LESEN

Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_BLOCKLAENGE_GESAMT | int | Flash Blocklaenge inclusive SID |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge |
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
| AUTHENTISIERUNG | string | Authentisierungsart 'Keine'        Keine Authentisierung 'Simple'       Einfache Authentisierung 'Symetrisch'   Symetrische Authentisierung 'Asymetrisch'  Asymetrische Authentisierung |
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
| FLASH_SCHREIBEN_ANZAHL | int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
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
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG AIF schreiben |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG AIF schreiben |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

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

<a id="job-status-version-gatewaytabelle"></a>
### STATUS_VERSION_GATEWAYTABELLE

Lesen der Versionsnummer der Gateway-Tabelle KWP2000: $22 ReadDataByCommonIdentifier $100D recordCommonIdentifier (gatewayTableVersionNumber) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VERSION_GATEWAYTABELLE | string | Versionsnummer der Gateway-Tabelle |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gateway-wakeup-source"></a>
### STATUS_GATEWAY_WAKEUP_SOURCE

Liefert die Quelle/Ursache zurück, die zum Wecken des Gateway-Steuergerätes geführt hat. Dieser Job wird von SG ab E60 unterstützt! KWP2000: $21 ReadDataByLocalIdentifier $BB recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WAKEUP_SOURCE | string | Weckursache table TWakeupSource TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-gateway-own-device-id"></a>
### STATUS_GATEWAY_OWN_DEVICE_ID

Information über den Gateway-Dispatcher Eigene logische MOST Device-ID KWP2000: $21 ReadDataByLocalIdentifier $B0 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LOG_MOST_ID_RECEIVE_STATE | string | Default oder Current. Current, falls zum Zeitpunkt der Abfrage bereits eine gültige MOST Device-ID ermittelt und im Dispatcher gespeichert werden konnte. table TLogMostIdReceiveState TEXT |
| STAT_LOG_MOST_DEV_ID | string | Eigene logische MOST Device-ID des Devices, das den Dispatcher- Funktionsblock enthält. Ermittelt aus der Device-Position im MOST-Ring. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-gateway-most-device-count"></a>
### STATUS_GATEWAY_MOST_DEVICE_COUNT

Information über den Gateway-Dispatcher Anzahl der vom Dispatcher erkannten MOST-Teilnehmer im Ring KWP2000: $21 ReadDataByLocalIdentifier $B1 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOST_DEVICE_COUNT | unsigned char | Anzahl der vom Dispatcher erkannten MOST-Teilnehmer im Ring |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-gateway-most-devices"></a>
### STATUS_GATEWAY_MOST_DEVICES

Ausgabe der erkannten MOST-Devices. Die Erkennung erfolgt ueber die InstID der Diagnose-Funktionsbloecke KWP2000: $21 ReadDataByLocalIdentifier $B2 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOST_DEVICE | string | Bezeichnung des MOST-Devices table TMostDevice TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-gateway-local-registry-elements"></a>
### STATUS_GATEWAY_LOCAL_REGISTRY_ELEMENTS

Information über den Gateway-Dispatcher Liste aller lokal (im Gateway-Adreßraum) registrierten FBlocks KWP2000: $21 ReadDataByLocalIdentifier $B2 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ELEMENT_COUNT | unsigned char | Anzahl der registrierten FBlocks bzw. FBlock-Modells (lokale Gateway-Dispatcher-Registry) |
| STAT_NODE_TYPE | string | Typ des registrierten Funktionsblocks bzw. -Modells table TNodeType TEXT |
| STAT_FBLOCK_ID | string | Funktions-Block-ID des registrierten Funktionsblocks bzw. -Modells |
| STAT_INST_ID | string | Instanz-ID des registrierten Funktionsblocks bzw. -Modells |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-gateway-external-registry-elements"></a>
### STATUS_GATEWAY_EXTERNAL_REGISTRY_ELEMENTS

Information über den Gateway-Dispatcher Liste aller extern (im MMI-Adreßraum) registrierten FBlocks KWP2000: $21 ReadDataByLocalIdentifier $B3 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ELEMENT_COUNT | unsigned char | Anzahl der registrierten FBlocks bzw. FBlock-Modells (externe MMI-Dispatcher-Registry) |
| STAT_NODE_TYPE | string | Typ des registrierten Funktionsblocks bzw. -Modells table TNodeType TEXT |
| STAT_FBLOCK_ID | string | Funktions-Block-ID des registrierten Funktionsblocks bzw. -Modells |
| STAT_INST_ID | string | Instanz-ID des registrierten Funktionsblocks bzw. -Modells |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-gateway-event-sink-count"></a>
### STATUS_GATEWAY_EVENT_SINK_COUNT

Information über den Gateway-Dispatcher Anzahl der am Dispatcher registrierten Event-Kommunikationsteilnehmer KWP2000: $21 ReadDataByLocalIdentifier $B4 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EVENT_SINK_COUNT | unsigned char | Anzahl der am Dispatcher registrierten Event-Kommunikationsteilnehmer (beschränkt auf Gateway-Adreßraum) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-praeprozessor-switch"></a>
### STATUS_PRAEPROZESSOR_SWITCH

Read out status of pre-processor switch KWP2000: $21 ReadDataByLocalIdentifier $BC recordLocalIdentifier - pre-processor switch state Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PRE_PROS_SWI | string | pre-processor switch state |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-included-gw-tab"></a>
### STATUS_INCLUDED_GW_TAB

Read out status of included GW table KWP2000: $21 ReadDataByLocalIdentifier $BD recordLocalIdentifier - included GW table state Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_INC_GW_TAB | string | status of included GW table |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hw-ref-gw"></a>
### STATUS_HW_REF_GW

Auslesen der HW-Referenz des Gateways KWP2000: $21 readDataByLocalIdentifier $FB recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HW_REF1 | string | Hardware-Referenz 1 |
| STAT_HW_REF2 | string | Hardware-Referenz 2 |
| STAT_HW_REF3 | string | Hardware-Referenz3 |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hw-num-gw"></a>
### STATUS_HW_NUM_GW

Auslesen der HW-Nummer des Gateways KWP2000: $21 readDataByLocalIdentifier $FB recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HW_NUM1 | string | HW-Nummer- 1 |
| STAT_HW_NUM2 | string | HW-Nummer- 2 |
| STAT_HW_NUM3 | string | HW-Nummer- 3 |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-repair-gw-progstate9"></a>
### STEUERN_REPAIR_GW_PROGSTATE9

Reparieren des Programmierstatus 9 beim Gateways KWP2000: $21 readDataByLocalIdentifier $FB recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HW_REF | string | OKAY, CORRECTED |
| STAT_HW_NUM | string | OKAY, CORRECTED |
| JOB_STATUS | string | OKAY |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Ansteuerung des Selbsttests Gateway-Rechner - Test der IPC (interprocessor communication) - Speichertests RAM, FLASH_ROM, EEPROM - Test der Werte des Helligkeitssensors auf Plausibilität - Ueberpruefung der Temperatur Bei Erkennung eines Fehlverhaltens erfolgt ein Eintrag im Primaer- und Shadowfehlerspeicher. KWP2000: $31 StartRoutineByLocalIdentifier $04 routineLocalIdentifier (selfTest) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT table JobResultExtended STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-disable-mcgw"></a>
### DISABLE_MCGW

Schaltet die Umsetzung im MOST/CAN-Gateway vollständig ab. Die Eigendiagnose des Gateways von MOST und CAN aus ist noch möglich KWP2000: $31 StartRoutineByLocalIdentifier $0F routineLocalIdentifier (disableMCGW) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REQUEST_TESTER | unsigned char | Gibt an, von welchem Tester die Abschaltung angefordert wurde. Folgende Tester sind erlaubt: $F1: BMW-Tester (Tester auf CAN) $FA: MOST-Tester (Tester auf MOST) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-enable-mcgw"></a>
### ENABLE_MCGW

Schaltet die Umsetzung im MOST/CAN-Gateway wieder ein. Damit das MCGW die Nachrichtenumsetzung wieder aufnimmt, muß das MCGW von beiden Testern freigegeben werden KWP2000: $32 StopRoutineByLocalIdentifier $0F routineLocalIdentifier (enableMCGW) Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REQUEST_TESTER | unsigned char | Gibt an, von welchem Tester die Freigabe angefordert wurde. Folgende Tester sind erlaubt: $F1: BMW-Tester (Tester auf CAN) $FA: MOST-Tester (Tester auf MOST) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-spannung"></a>
### STATUS_ANALOG_SPANNUNG

Auslesen der Spannungswerte von Board, SH3 und FPGA KWP2000: $30 InputOutputControlByLocalIdentifier $02 inputOutputLocalIdentifier $07 shortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SPG_BOARD_WERT | unsigned int | Zahlenwert der Board Spannung Byteorder: High / Low |
| STAT_SPG_BOARD_EINH | string | Einheit von STAT_SPG_BOARD_WERT (mVolt) |
| STAT_SPG_SH3_WERT | unsigned int | Zahlenwert der SH3 Spannung Byteorder: High / Low |
| STAT_SPG_SH3_EINH | string | Einheit von STAT_SPG_SH3_WERT (mVolt) |
| STAT_SPG_FPGA_WERT | unsigned int | Zahlenwert der FPGA Spannung Byteorder: High / Low |
| STAT_SPG_FPGA_EINH | string | Einheit von STAT_SPG_FPGA_WERT (mVolt) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-temperatur"></a>
### STATUS_ANALOG_TEMPERATUR

Status der Temperaturwerte FOT Board, Mod4020 und Endstufe KWP2000: $30 InputOutputControlByLocalIdentifier $03 inputOutputLocalIdentifier $07 shortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TEMP_FOT_WERT | char | Zahlenwert der FOT-Temperatur |
| STAT_TEMP_FOT_EINH | string | Einheit von STAT_TEMP_FOT_WERT (Grad C) |
| STAT_TEMP_MOD_WERT | char | Zahlenwert der Mod4020-Temperatur |
| STAT_TEMP_MOD_EINH | string | Einheit von STAT_TEMP_MOD_WERT (Grad C) |
| STAT_TEMP_ENDSTU_WERT | char | Zahlenwert der Endstufen-Temperatur |
| STAT_TEMP_ENDSTU_EINH | string | Einheit von STAT_TEMP_ENDSTU_WERT (Grad C) |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-steuern-zentrale-registry-sollkonfiguration"></a>
### STEUERN_ZENTRALE_REGISTRY_SOLLKONFIGURATION

Ausgelesene Zentrale Registry wird als Sollkonfiguration abgespeichert KWP2000: $30 InputOutputControlByLocalIdentifier $06 inputOutputLocalIdentifier $07 ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-current-registry"></a>
### READ_CURRENT_REGISTRY

Auslesen der Registry vom ASK KWP2000: $21 ReadDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $B5 recordLocalIdentifier Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DEVICEID_CURRENT | string | Deviceadresse |
| FBLOCKID_CURRENT | string | FunktionsblockID |
| INSTID_CURRENT | string | InstID |
| FBLOCK_NAME_CURRENT | string | Name des FBlocks |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-default-registry"></a>
### READ_DEFAULT_REGISTRY

Auslesen der Registry vom ASK KWP2000: $21 ReadDataByLocalIdentifier LH Diagnose Teil 8, Januar 2000 Seite 67 $B6 recordLocalIdentifier Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DEVICEID_DEFAULT | string | Deviceadresse |
| FBLOCKID_DEFAULT | string | FunktionsblockID |
| INSTID_DEFAULT | string | InstID |
| FBLOCK_NAME_DEFAULT | string | Name des FBlocks |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hw-nummer-lesen"></a>
### hw_nummer_lesen

Hardware-Nummer lesen KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_HW_NR | string | BMW-Hardwarenummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-luefter"></a>
### STEUERN_LUEFTER

Setzen der Lüfterwerte KWP2000: $30 InputOutputControlByLocalIdentifier $04 inputOutputLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPEED_GRADE | unsigned char | Bestimmt die Drehgeschwindigkeit des Lüfters Es sind 4 Geschwindigkeitsstufen definiert: 0: Stop, 1: niedrige, 2: mittlere, 3: maximale |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-luefter"></a>
### STATUS_LUEFTER

Lesen der Lüfterwerte KWP2000: $21 ReadDataByLocalIdentifier $B7 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LUEFTER | string | Lüfter LÄUFT (incl. Stufe) oder STEHT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-temperaturabschaltwerte"></a>
### STEUERN_TEMPERATURABSCHALTWERTE

Setzen der Temperaturabschaltwerte Alle Werte sind in °C anzugeben KWP2000: $3B WriteDataByLocalIdentifier $B8 localIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEMP_RELEASE | unsigned char | Temperaturwert unterschreiten: MMI wird eingeschaltet |
| TEMP_WARM | unsigned char | Hat derzeit keine Bedeutung |
| TEMP_HIGH | unsigned char | Temperaturwert überschreiten: MMI wird abgeschaltet Temperaturwert unterschreiten: MOST wird eingeschaltet |
| TEMP_CRIT | unsigned char | Temperaturwert überschreiten: MOST wird abgeschaltet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temperaturabschaltwerte"></a>
### STATUS_TEMPERATURABSCHALTWERTE

Lesen der Temperaturabschaltwerte KWP2000: $21 ReadDataByLocalIdentifier $B8 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMP_RELEASE | unsigned char | Temperaturwert unterschreiten: MMI wird eingeschaltet |
| STAT_TEMP_WARM | unsigned char | Hat derzeit keine Bedeutung |
| STAT_TEMP_HIGH | unsigned char | Temperaturwert überschreiten: MMI wird abgeschaltet Temperaturwert unterschreiten: MOST wird eingeschaltet |
| STAT_TEMP_CRIT | unsigned char | Temperaturwert überschreiten: MOST wird abgeschaltet |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-taste-gedrueckt"></a>
### STATUS_TASTE_GEDRUECKT

Auslesen, ob gerade eine Taste gedrueckt ist KWP2000: $21 ReadDataByLocalIdentifier $B9 recordLocalIdentifier - any key pressed Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TASTE_GEDRUECKT | string | Gerade Taste gedrückt? |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tel-mute"></a>
### STATUS_TEL_MUTE

Ausgabe, ob Tel-Mute-Leitung aktiv oder inaktiv ist KWP2000: $21 ReadDataByLocalIdentifier $BA recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEL_MUTE | string | Tel-Mute-Leitung aktiv oder inaktiv table TTelMute |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-sahara-sw-number"></a>
### read_sahara_sw_number

Lesen der Sahara Software Version Nummer KWP2000: $21 ReadDataByLocalIdentifier $FD recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_SW_NR_SAHARA | string | Softwarenummer (Sahara software version) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-luefter-ctrl-data"></a>
### STATUS_LUEFTER_CTRL_DATA

Lesen der Lüftersteuerungsparameter KWP2000: $21 ReadDataByLocalIdentifier $FC recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMP_FOT_0 | char | Temperaturwert FOT Lüfter abschalten |
| STAT_TEMP_FOT_1 | char | Temperaturwert FOT Lüfter 1 |
| STAT_TEMP_FOT_2 | char | Temperaturwert FOT Lüfter 2 |
| STAT_TEMP_FOT_3 | char | Temperaturwert FOT Lüfter 3 |
| STAT_HYST_FOT_0 | char | Hysterese FOT Lüfter abschalten |
| STAT_HYST_FOT_1 | char | Hysterese FOT Lüfter 1 |
| STAT_HYST_FOT_2 | char | Hysterese FOT Lüfter 2 |
| STAT_HYST_FOT_3 | char | Hysterese FOT Lüfter 3 |
| STAT_TEMP_MOD | char | Temperaturwert MOD |
| STAT_HYST_MOD | char | Hysterese MOD |
| STAT_TEMP_END | char | Temperaturwert END |
| STAT_HYST_END | char | Hysterese END |
| STAT_PULS_WIDTH_0 | unsigned int | Puls Weite 0 |
| STAT_PULS_WIDTH_1 | unsigned int | Puls Weite 1 |
| STAT_PULS_WIDTH_2 | unsigned int | Puls Weite 2 |
| STAT_PULS_WIDTH_3 | unsigned int | Puls Weite 3 |
| STAT_RPM_0 | unsigned int | Umdrehungen /min 0 |
| STAT_RPM_1 | unsigned int | Umdrehungen /min 1 |
| STAT_RPM_2 | unsigned int | Umdrehungen /min 2 |
| STAT_RPM_3 | unsigned int | Umdrehungen /min 3 |
| STAT_CHECK_TIME | unsigned int | Überprüfungszeitzyklus |
| STAT_SELECT_NUMBER | unsigned char | Auswahlnummer (aus Ediabas _Steuern) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-luefter-ctrl-data"></a>
### STEUERN_LUEFTER_CTRL_DATA

Setzen der Lüfter Steuer Daten KWP2000: $3B WriteDataByLocalIdentifier $21 localIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAN_PARAM_SET | unsigned char | Nummer des Fan Parametersatzes 0: Default 1: xyz1 2: xyz2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-is-powerfollowup"></a>
### STATUS_IS_POWERFOLLOWUP

Infospeicher u. Details 0xA18B lesen und auswerten KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| WAKEUP_REASON | string | Weckgrund table TWakeupReason REASON |
| ASLEEPERROR_REASON | string | Einschlaf Fehlerursache table TASleeperrorReason REASON |
| ASLEEPERROR_FLAGS | string | Additional Flags for ASLEEPERROR_REASON |
| TASK_SIGNATURE | string | Task Signature (only valid if: AsleeperrorReason = 0x02 = 'GW- or MMI task is not ready for sleep') table TTaskSignature TASK |
| DIAGFBLOCK_TEXT | string | DiagFBlock and InstID (only valid if: AsleeperrorReason = 0x08 = 'MOST-Bus is not ready for sleep') |
| DIAGFBLOCK_INSTID | string | InstID (see DIAGFBLOCK_TEXT) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-diff-registry"></a>
### READ_DIFF_REGISTRY

Vergleich der Current und Default Registry vom ASK KWP2000: $21 ReadDataByLocalIdentifier $B5 recordLocalIdentifier $B6 recordLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DIFF_TYPE | string | Current oder Default-FBloecke |
| DEVICEID_DIFF | string | Deviceadresse |
| FBLOCKID_DIFF | string | FunktionsblockID |
| INSTID_DIFF | string | InstID |
| FBLOCK_NAME_DIFF | string | Name des FBlocks |

<a id="job-check-1c55"></a>
### CHECK_1C55

Datenbyte 0x1C55 prüfen KWP2000: $31 StartRoutineByLocalIdentifier $FA systemSupplierSpecific $39 localIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AUSGABE_STR | string | Adressinhaltausgabe |
| STATUS_1C55 | string | ERROR_1C55_EQUAL_0x03 oder OKAY |
| JOB_STATUS | string | OKAY, wenn fehlerfrei oder ERROR_READ_PMBUS_EEPROM |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-rit"></a>
### READ_RIT

Auslesen der Routing Information Table eines beliebigen MOST-Devices KWP2000: $21 ReadDataByLocalIdentifier $C0 recordLocalIdentifier  (via LESE_MOSTREGISTER) Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DEVICEID | string | Logische MOST-Deviceadresse 4-stellig leer lassen wenn DIAG_ADRESSE genutzt wird Beispiel: 0101 |
| DIAG_ADRESSE | unsigned char | Diagnose Steuergeräteadresse (alternativ zu logischer Deviceadresse) Beispiel: 0x62 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RIT_LINE_0xXX | string | Xte-RIT-Zeile |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lese-mostregister"></a>
### LESE_MOSTREGISTER

Es wird ein bestimmtes MOST-Register eines bestimmten MOST-Devices ausgelesen KWP2000: $21 ReadDataByLocalIdentifier $C0 recordLocalIdentifier Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DEVICEID | string | Logische MOST-Deviceadresse 4-stellig leer lassen wenn DIAG_ADRESSE genutzt wird Beispiel: 0101 |
| DIAG_ADRESSE | unsigned char | Diagnose Steuergeräteadresse (alternativ zu logischer Deviceadresse) Beispiel: 0x62 |
| REGISTER | unsigned char | Auszulesende MOST-Registeradresse Beispiel: 0x08 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| REGISTER_CONTENT | string | 8 Bytes des angefragten MOST-Registers (Durchgeschleifte Rückgabe von Remote Read) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-search-fblock"></a>
### STATUS_SEARCH_FBLOCK

Suche Fblock,InstID KWP2000: $21 ReadDataByLocalIdentifier $B5 recordLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FBLOCKID | unsigned char | FunktionsblockID |
| INSTID | unsigned char | InstID |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FBLOCK | unsigned char | 0x00 nicht gefunden, 0x01 gefunden |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fan-history"></a>
### STATUS_FAN_HISTORY

Lesen des Lüfteransteuerungsverlaufs für den Normalbetrieb KWP2000: $21 ReadDataByLocalIdentifier $FB recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME_ALL | unsigned long | Gesamtbetriebszeit in Sekunden |
| STAT_FAN_SWITCH_ON | unsigned int | Anzahl der Lüftereinschaltvorgänge |
| STAT_TIME_FAN_OFF | unsigned int | Zeit Lüfter aus in Sekunden |
| STAT_TIME_FAN_1 | unsigned int | Zeit Lüfterstufe 1 in Sekunden |
| STAT_TIME_FAN_2 | unsigned int | Zeit Lüfterstufe 2 in Sekunden |
| STAT_TIME_FAN_3 | unsigned int | Zeit Lüfterstufe 3 in Sekunden |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-clear-fan-history"></a>
### STEUERN_CLEAR_FAN_HISTORY

Löschen des Lüfteransteuerungsverlaufs KWP2000: $31 StartRoutineByLocalIdentifier $FB systemSupplierSpecific Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-devids-current-registry"></a>
### READ_DEVIDS_CURRENT_REGISTRY

Auslesen der DEVIDS der Current Registry KWP2000: $21 ReadDataByLocalIdentifier $BC recordLocalIdentifier Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DEVICEID_CURRENT | string | Deviceadresse |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-devids-default-registry"></a>
### READ_DEVIDS_DEFAULT_REGISTRY

Auslesen der DEVIDS der Default Registry KWP2000: $21 ReadDataByLocalIdentifier $BE recordLocalIdentifier Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DEVICEID_DEFAULT | string | Deviceadresse |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-fblocks-current-registry"></a>
### READ_FBLOCKS_CURRENT_REGISTRY

Auslesen der FBlockIDs einer DEVID der Current Registry KWP2000: $21 ReadDataByLocalIdentifier $BD recordLocalIdentifier Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DEVNODE | string | Logische MOST-Deviceadresse 4-stellig Beispiel: 0101 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FBLOCKID_CURRENT | string | FBlockID |
| INSTID_CURRENT | string | InstID |
| FBLOCK_NAME_CURRENT | string | Name des FBlocks |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-fblocks-default-registry"></a>
### READ_FBLOCKS_DEFAULT_REGISTRY

Auslesen der FBlockIDs einer DEVID der Default Registry KWP2000: $21 ReadDataByLocalIdentifier $BF recordLocalIdentifier Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DEVNODE | string | Logische MOST-Deviceadresse 4-stellig Beispiel: 0101 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FBLOCKID_DEFAULT | string | FBlockID |
| INSTID_DEFAULT | string | InstID |
| FBLOCK_NAME_DEFAULT | string | Name des FBlocks |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-newseeland"></a>
### WRITE_NEWSEELAND

Neuseeland Tuner Parametersatz ändern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NZ_PARAM_SET | unsigned char | Nummer des Neuseeland Parametersatzes 0: Orginalzustand 1: NZ Codierung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_WRITE_PMBUS_EEPROM, sonst |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-check-adc"></a>
### STATUS_CHECK_ADC

Datenbyte 0x1E05 prüfen KWP2000: $31 StartRoutineByLocalIdentifier $FA systemSupplierSpecific $39 localIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_1E05 | char | OKAY |
| STATUS_1E06 | char | OKAY |
| JOB_STATUS | string | OKAY, wenn fehlerfrei oder ERROR_READ_PMBUS_EEPROM |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-adc-anhebung"></a>
### STEUERN_ADC_ANHEBUNG

Datenblock ins EEProm schreiben KWP2000: $31 StartRoutineByLocalIdentifier $FA systemSupplierSpecific $37 localIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfreI oder ERROR_WRITE_PMBUS_EEPROM, sonst |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (89 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [ABILITY_TO_WAKE](#table-ability-to-wake) (4 × 2)
- [MOST_3DB](#table-most-3db) (3 × 2)
- [WAKE_UP_STATUS](#table-wake-up-status) (4 × 2)
- [TLOGMOSTIDRECEIVESTATE](#table-tlogmostidreceivestate) (2 × 2)
- [TNODETYPE](#table-tnodetype) (6 × 2)
- [TPRE_PRO_SWI_STATE](#table-tpre-pro-swi-state) (4 × 2)
- [TINC_GW_TAB](#table-tinc-gw-tab) (4 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (5 × 2)
- [FORTTEXTE](#table-forttexte) (14 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (6 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (6 × 9)
- [IORTTEXTE](#table-iorttexte) (29 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (21 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (16 × 9)
- [TWAKEUPSOURCE](#table-twakeupsource) (9 × 2)
- [TMOSTDEVICE](#table-tmostdevice) (38 × 2)
- [TFBLOCKIDTEXTE](#table-tfblockidtexte) (42 × 2)
- [TTASTE_GEDRUECKT](#table-ttaste-gedrueckt) (4 × 2)
- [TTELMUTE](#table-ttelmute) (2 × 2)
- [TWAKEUPREASON](#table-twakeupreason) (9 × 2)
- [TASLEEPERRORREASON](#table-tasleeperrorreason) (8 × 2)
- [TTASKSIGNATURE](#table-ttasksignature) (13 × 2)

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

Dimensions: 89 rows × 2 columns

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

<a id="table-tlogmostidreceivestate"></a>
### TLOGMOSTIDRECEIVESTATE

Dimensions: 2 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | Default Value |
| 0x01 | Current Value |

<a id="table-tnodetype"></a>
### TNODETYPE

Dimensions: 6 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | Virtual Function-Block |
| 0x01 | Local Function-Block |
| 0x02 | External Function-Block |
| 0x03 | Virtual Function-Block-Model |
| 0x04 | Local Function-Block-Model |
| 0x05 | External Function-Block-Model |

<a id="table-tpre-pro-swi-state"></a>
### TPRE_PRO_SWI_STATE

Dimensions: 4 rows × 2 columns

| NAME | MASKE |
| --- | --- |
| Classic | 0x00 |
| Compressed Intel | 0x01 |
| Compressed Motorola | 0x02 |
| Unknown | 0xXY |

<a id="table-tinc-gw-tab"></a>
### TINC_GW_TAB

Dimensions: 4 rows × 2 columns

| NAME | MASKE |
| --- | --- |
| Classic / Invalid | 0x00 |
| Compressed Intel | 0x01 |
| Compressed Motorola | 0x02 |
| Unknown | 0xXY |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 5 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | ERROR_ARGUMENT_NOT_IN_TABLE |
| 0x01 | ERROR_INVALID_ARGUMENT |
| 0x02 | ERROR_MISSING_ARGUMENT |
| 0x03 | ERROR_EXECUTION_LOCALROUTINE |
| 0xXY | ERROR_UNKNOWN |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA168 | Hardware-Defekt Gateway-Rechner |
| 0xA169 | Hardware-Defekt LCD |
| 0xA16A | Prüfsummenfehler Gateway-Tabelle |
| 0xA16B | Energiesparmode aktiv |
| 0xE184 | CAN Low |
| 0xE187 | CAN Controller |
| 0xE18C | Device hat die Monitoringnachricht nicht abgenommen oder bestaetigt. (Error_Monitoring). |
| 0xE18D | Weckendes Device hat 3 mal erfolglos versucht das Netzwerk zu wecken. (Error_WakeUp_Failed). |
| 0xE18E | Obwohl Shutdown(Execute) geschickt wurde ging das Licht nicht aus. (Error_Light_Not_Off). |
| 0xE18F | Zentrale Registry stimmt nicht mit der Sollkonfiguration ueberein (Error_Registry_New). |
| 0xE190 | Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose). |
| 0xE191 | Lange und/oder haeufige Unlocks (Error_Unlock_Long). |
| 0xE192 | Ein Device hat sich wegen Uebertemperatur abgeschaltet (Error_Temp_Shutdown). |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 6 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xA168 | 0x01 | 0x03 | 0x04 | -- |
| 0xE18C | 0x21 | -- | -- | -- |
| 0xE18F | 0x21 | -- | -- | -- |
| 0xE190 | 0x22 | -- | -- | -- |
| 0xE192 | 0x21 | -- | -- | -- |
| default | -- | -- | -- | -- |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 6 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Temperatur MMI-Rechner | Grad C | high | signed int | -- | 1 | 1 | 0 |
| 0x03 | Bordnetzspannung | Volt | high | unsigned int | -- | 1 | 10 | 0 |
| 0x04 | Fehlerursache | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x21 | Diagnoseadresse | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x22 | NPR | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | high | unsigned int | -- | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 29 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xA170 | Fehler IPC Startup |
| 0xA171 | Fehler IPC Operation |
| 0xA172 | Fehler Laden FPGA |
| 0xA173 | Fehler OS8805 |
| 0xA174 | Fehler FLASH-ROM |
| 0xA175 | Fehler RAM |
| 0xA176 | Fehler EEPROM |
| 0xA177 | MMI-Rechner Temperatur zu hoch |
| 0xA180 | Pufferueberlauf Empfangspuffer |
| 0xA181 | Pufferueberlauf Sendepuffer |
| 0xA182 | Laenge der CAN Input-Nachricht nicht korrekt |
| 0xA183 | Laenge der MOST Input-Nachricht nicht korrekt |
| 0xA184 | Timeout CAN Input-Nachricht |
| 0xA185 | RAD-ON oder SUB-ON Kurzschluss |
| 0xA186 | Sahara DSP Fehler |
| 0xA187 | Sahara Lüfter defekt |
| 0xA188 | Endstufen Fehler |
| 0xA189 | Fehler SH3 Spannungsversorgung |
| 0xA18A | Fehler FPGA Spannungsversorgung |
| 0xA18B | Nachlauf-Stromversorgung Zeitüberschreitung |
| 0x9308 | Device bekam Reset (Error_Reset). |
| 0x9309 | Bis zum Auftreten des Timeouts konnte kein Licht bzw. kein stabiler Lock erkannt werden (Error_NSInit_Timeout). |
| 0x930A | Device ist im Zustand Normal Operation und das Licht am Eingang geht ohne Vorankuendigung aus (Error_Sudden_light_off). |
| 0x930B | Anfragendes Device bekommt keine Antwort obwohl Partner vorhanden ist (Error_Device_No_Answer). |
| 0x930C | Kurze Unlocks (Error_Unlock_Short). |
| 0x930D | Kein Broadcast Configuration(Status) vom Networkmaster erhalten (Error_t_CfgStatus). |
| 0x930F | Ein Device hat im laufenden Betrieb seinen Bypass All geschlossen (Error_NCE). |
| 0x9310 | Empfaenger hat eine Nachricht nicht abgenommen (Error_NAK). |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 21 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xA170 | 0x01 | 0x03 | -- | -- |
| 0xA171 | 0x01 | 0x03 | -- | -- |
| 0xA172 | 0x01 | 0x03 | -- | -- |
| 0xA173 | 0x01 | 0x03 | -- | -- |
| 0xA174 | 0x01 | 0x03 | -- | -- |
| 0xA175 | 0x01 | 0x03 | -- | -- |
| 0xA176 | 0x01 | 0x03 | -- | -- |
| 0xA177 | 0x01 | 0x03 | -- | -- |
| 0xA180 | 0x08 | -- | -- | -- |
| 0xA181 | 0x08 | -- | -- | -- |
| 0xA182 | 0x04 | 0x07 | -- | -- |
| 0xA183 | 0x05 | 0x06 | 0x07 | -- |
| 0xA184 | 0x04 | -- | -- | -- |
| 0xA185 | 0x01 | -- | -- | -- |
| 0xA186 | 0x01 | -- | -- | -- |
| 0xA187 | 0x01 | 0x03 | -- | -- |
| 0xA18B | 0x26 | 0x27 | 0x28 | 0x25 |
| 0x930B | 0x21 | 0x22 | 0x23 | 0x24 |
| 0x930F | 0x25 | -- | -- | -- |
| 0x9310 | 0x21 | 0x22 | 0x23 | 0x24 |
| default | -- | -- | -- | -- |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 16 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Temperatur MMI-Rechner | Grad C | high | signed int | -- | 1 | 1 | 0 |
| 0x03 | Bordnetzspannung | Volt | high | unsigned int | -- | 1 | 10 | 0 |
| 0x04 | CAN-Identifier | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x05 | FBlockID&InstID | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x06 | FktID&OpType | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x07 | Laenge Nachricht | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x08 | Bustyp | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x21 | Logische-Kotenadresse | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x22 | FBlockID | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x23 | InstID | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x24 | FktID | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x25 | Diagnoseadresse | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x26 | Weckgrund       | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x27 | Einschlaf Fehlerursache | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0x28 | Task-Signatur   | Hex | high | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned int | -- | 1 | 1 | 0 |

<a id="table-twakeupsource"></a>
### TWAKEUPSOURCE

Dimensions: 9 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x01 | Weckursache = CAN |
| 0x02 | Weckursache = MOST |
| 0x03 | Weckursache = IPC |
| 0x04 | Weckursache = INTERN |
| 0x05 | Weckursache = RESET/SWITCH TO POWER |
| 0x40 | Weckursache = ENTERTAINMENT BUTTON |
| 0x41 | Weckursache = CD-EJECT |
| 0x42 | Weckursache = CD-INSERT |
| 0x45 | Weckursache = OTHER |

<a id="table-tmostdevice"></a>
### TMOSTDEVICE

Dimensions: 38 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x15 | TELCO   (TelCommander) |
| 0x31 | MMC     (Multimedia-Changer) |
| 0x32 | MMIC    (MMI/GT Fond CAN-Interface) |
| 0x34 | MMIF    (MMI/GT Fond CAN-Interface) |
| 0x35 | SVS     (Sprachverarbeitungssystem) |
| 0x36 | TEL     (Telefon-Interface) |
| 0x37 | AMP     (Top-Hifi Verstaerker) |
| 0x3A | KH-INT  (Kopfhoerer-Interface) |
| 0x3B | NAV     (Navigationssystem) |
| 0x3C | CDC     (CD-Wechsler) |
| 0x3D | HUD     (Head-Up Display) |
| 0x3F | ASK     (Audio-System-Kontroller) |
| 0x47 | TUNER   (Antennentuner) |
| 0x49 | SEC1    (Security-Modul 1) |
| 0x4A | SEC2    (Security-Modul 2) |
| 0x4B | VID     (Videomodul) |
| 0x60 | KOMBI   (Instrumentenkombination) |
| 0x54 | SDARS   (Satelliten-Radio) |
| 0x61 | FBI     (Flexible Bus-Interface) |
| 0x62 | MCGW    (MOST/CAN-Gateway) |
| 0x63 | MMI     (MMI/GT Front\| M-ASK \| CCC) |
| 0x90 | Sahara DSP |
| 0x91 | Sprachpaket |
| 0x92 | Virtuelles SG Hardware |
| 0x93 | CCC-BT  (BT-Modul im CCC |
| 0x94 | CCC-POS (Pos.-Modul im CCC |
| 0x95 | CCC-RS  (Rear Seat G im CCC |
| 0x96 | CCC-OS  (Betriebssystem SH4 im CCC |
| 0x97 | CCC-JVM (Java Virtual Machine im CCC |
| 0x98 | CCC-MM  (MM-FW im CCC |
| 0x99 | CCC-MMI (MMI Descr im CCC |
| 0x9A | CCC-PFS (PFS-FW im CCC |
| 0x9B | CCC-HUD (HUD-Software im CCC |
| 0x9C | CCC-ONL (Online Pack im CCC |
| 0x9D | CCC-MPG (MPEG2 im CCC |
| 0x9E | CCC-DSP (DPS im CCC |
| 0x9F | CCC-NET (Network im CCC |
| 0xA0 | CCC-APP (Applikation im CCC |

<a id="table-tfblockidtexte"></a>
### TFBLOCKIDTEXTE

Dimensions: 42 rows × 2 columns

| FBLOCKID | NAME |
| --- | --- |
| 0x02 | NetworkMaster |
| 0x03 | ConnectionMaster |
| 0x04 | PowerMaster |
| 0x05 | Vehicle |
| 0x06 | Diagnose |
| 0x07 | VideoSwitch |
| 0x10 | ManMachineInterface |
| 0x11 | Sprachverarbeitungssystem |
| 0x15 | ControlElements |
| 0x16 | Security |
| 0x20 | AudioMaster |
| 0x22 | AudioAmplifier |
| 0x23 | HeadPhoneAmplifier |
| 0x24 | AuxilliaryInput=0x24 |
| 0x26 | MicrophoneInput |
| 0x30 | AudioTapePlayer |
| 0x31 | AudioDiscPlayer |
| 0x32 | MultiMediaChanger |
| 0x40 | AM/FM Tuner |
| 0x41 | TMC Tuner |
| 0x42 | TVTuner |
| 0x43 | ExternSource |
| 0x44 | SDARS |
| 0x50 | TelefonFix |
| 0x51 | PhoneBook |
| 0x52 | Navigationssystem |
| 0x54 | Bluetooth |
| 0x6F | Monitor |
| 0x71 | Climate |
| 0x80 | MMI_Terminal |
| 0x81 | KOMBI_Terminal |
| 0x82 | HUD_Terminal |
| 0x90 | Telematik |
| 0xAB | EDIABAS4MOST |
| 0xC9 | Service |
| 0xCA | KombiMiscFkts |
| 0xCB | Bordcomputer |
| 0xCC | ADASInterface |
| 0xDE | Telematic |
| 0xE0 | KombiInterface |
| 0xE1 | HUDInterface |
| 0xXY | Unbekannter FBlock |

<a id="table-ttaste-gedrueckt"></a>
### TTASTE_GEDRUECKT

Dimensions: 4 rows × 2 columns

| MASKE | NAME |
| --- | --- |
| 0x03 | Eject |
| 0x04 | Entertainment |
| 0x05 | Suchlauf_Ab |
| 0x06 | Suchlauf_Auf |

<a id="table-ttelmute"></a>
### TTELMUTE

Dimensions: 2 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | Tel-Mute-Leitung inaktiv |
| 0x01 | Tel-Mute-Leitung aktiv |

<a id="table-twakeupreason"></a>
### TWAKEUPREASON

Dimensions: 9 rows × 2 columns

| VALUE | REASON |
| --- | --- |
| 0x0001 | CAN - BUS |
| 0x0002 | MOST - BUS |
| 0x0003 | Unused |
| 0x0004 | Unused |
| 0x0005 | POWER - UP - BOOT |
| 0x0040 | KEY_ENTERTAINMENT / MMI_REQUEST |
| 0x0041 | KEY_EJECT |
| 0x0042 | CD_INSERT |
| 0x0045 | UNDEFINED (nur für interne Tests) |

<a id="table-tasleeperrorreason"></a>
### TASLEEPERRORREASON

Dimensions: 8 rows × 2 columns

| VALUE | REASON |
| --- | --- |
| 0x00 | No Sleep-Request Error detected yetLow Byte (xx) is Substate in SleepRequest before WDG. |
| 0x01 | one GW- or MMI task creates Sleep-Request-Timeout |
| 0x02 | GW- or MMI task is not ready for sleep |
| 0x04 | MOST-Bus answer creates Sleep-Request-Timeout |
| 0x08 | MOST-Bus is not ready for sleep |
| 0x10 | CAN-Bus answer creates Sleep-Request-Timeout |
| 0x20 | CAN-Bus is not ready for sleep |
| 0x40 | Repetive Request Restart |

<a id="table-ttasksignature"></a>
### TTASKSIGNATURE

Dimensions: 13 rows × 2 columns

| VALUE | TASK |
| --- | --- |
| 0x77 | CAN - Task |
| 0x78 | EEPROM - Task |
| 0x98 | Analog/Digital Conversion - Task |
| 0x99 | IPC - Task |
| 0x9A | MMI - Task |
| 0x9B | IPC - Task ( development ) |
| 0x9C | IPC - Task MMI wait |
| 0xAA | Gateway Core  - Task |
| 0xAD | Gateway Administrator - Task |
| 0xBB | Viewer - Task |
| 0xBE | MOST - Task |
| 0xCC | Gateway Administrator - Task (Sleep Request) |
| 0xFF | Message Simulator - Task ( development ) |
