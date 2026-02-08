# FAH_PLX.prg

- Jobs: [100](#jobs)
- Tables: [26](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Sitzsteuergerät PLx |
| ORIGIN | BMW EI-61 Hellwig |
| REVISION | 4.002 |
| AUTHOR | Temic Komfort Sehr Hermann, Temic Komfort Mayerle Wolfgang, Temic Komfort Kirschner Richard |
| COMMENT | SGBD für Sitzsteuergerät PLx |
| PACKAGE | 1.31 |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus $04 requestIdentifiedShadowMemoryDTCAndStatus
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
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
- [FS_LOESCHEN_EINZELN](#job-fs-loeschen-einzeln) - Fehlerspeicher loeschen, einzelner Fehler KWP2000: $14 ClearDiagnosticInformation $xxxx DTC (SM-spezifisch) SM-spezifischer Job Beispielargument: "0x9E48" siehe auch unter Befehl fs_lesen, Result F_ORT_NR
- [READ_ENERGY_SAVING_STATE](#job-read-energy-saving-state) - Aktuellen FETRAWE-Mode des SG auslesen FETRAWE-Mode: Fertigungs-, Transport- und Werkstatt- Mode KWP2000: $22 ReadDataByCommonIdentifier $100A EnergySavingState
- [START_COMMUNICATION](#job-start-communication) - Kommunikation mit Standard KWP2000 starten KWP2000: $81 StartCommunication
- [STOP_COMMUNICATION](#job-stop-communication) - Kommunikation mit Standard KWP2000 beenden KWP2000: $82 StopCommunication
- [WAIT_N_SECONDS](#job-wait-n-seconds) - Wartet die angeforderte Anzahl von Sekunden -&gt; fuer Testablaeufe mit Toolset
- [IDENT_BMW_NR](#job-ident-bmw-nr) - Auslesen BMW-Teilenummer KWP2000: $1A ReadECUIdentification IO     : $91
- [IDENT_BOOTLOADER_SW_NR](#job-ident-bootloader-sw-nr) - Auslesen der Bootloader SW Versionsnummer KWP2000: $1A ReadECUIdentification IO     : §8A
- [IDENT_CHANGE_INDEX](#job-ident-change-index) - Auslesen BMW-Teilenummer KWP2000: $1A ReadECUIdentification IO     : §88
- [IDENT_READ_CURRENT_UIF_TABLE](#job-ident-read-current-uif-table) - Aktuelles UIF mit $1A $86 auslesen KWP2000: $1A ReadECUIdentification IO     : $86 Read Current ECU-UIF-Table
- [IDENT_TEMIC_HW_NR](#job-ident-temic-hw-nr) - Auslesen TEMIC-Teilenummer KWP2000: $1A ReadECUIdentification IO: §92
- [IDENT_TEMIC_HW_VERS_NR](#job-ident-temic-hw-vers-nr) - Auslesen TEMIC-HW-Versions-Nummern KWP2000: $1A ReadECUIdentification IO: §93
- [IDENT_SVS_SBUS_SW_NR](#job-ident-svs-sbus-sw-nr) - ID-Daten des Sitzverstellschalters links KWP2000: $21 ReadDataByLocalIdentifier  Modus  : all
- [STATUS_AKTIVSITZ_AD_GET](#job-status-aktivsitz-ad-get) - AD-Werte Aktivsitz auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x38 0x04 inputOutputControlParameter: 0x01 (reportCurrentState)
- [STATUS_AKTIVSITZ_SCHALTER_GET](#job-status-aktivsitz-schalter-get) - Status Schalter Aktivsitz auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x38 0x03 inputOutputControlParameter: 0x01 (reportCurrentState) eingelesener Zustand des Druckschalters Aktivsitz Nockenschalter Aktivsitz abhaengig von verbauten System Pneumatisches System Hydraulisches System CS_1, antwort[7]
- [STATUS_FEH_SCHALTER](#job-status-feh-schalter) - Auslesen des Portzustandes für Erkennung Fond-Einstiegshilfe vor/zurueck KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x04
- [STATUS_HALL_AD_LBV_KHV_GET](#job-status-hall-ad-lbv-khv-get) - AD-Werte der Hallsensoren auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0x0C inputOutputControlParameter: 0x01 (reportCurrentState)
- [STATUS_HALL_AD_SHV_SNV_STV_GET](#job-status-hall-ad-shv-snv-stv-get) - AD-Werte der Hallsensoren auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0x0B inputOutputControlParameter: 0x01 (reportCurrentState)
- [STATUS_HALL_AD_SLV_LNV_LKV_GET](#job-status-hall-ad-slv-lnv-lkv-get) - AD-Werte der Hallsensoren auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0x0A inputOutputControlParameter: 0x01 (reportCurrentState)
- [STATUS_HALL_AD](#job-status-hall-ad) - AD-Werte der Hallsensoren auslesen KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x18     , 0x01 (report), 0x0D
- [STATUS_HALL_COUNTER_GET](#job-status-hall-counter-get) - alle Hallzählerstände auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0x0E inputOutputControlParameter: 0x01 (reportCurrentState)
- [STATUS_HEIZ_GET](#job-status-heiz-get) - Auslesen von Heizungs-Temperatur-Werten KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x20 0x05 inputOutputControlParameter: 0x01 (reportCurrentState)
- [STATUS_KLIMA_GET](#job-status-klima-get) - Auslesen von Klimalüfter-AD-Werten KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x28 0x03 inputOutputControlParameter: 0x01 (reportCurrentState)
- [STATUS_LORDOSE_GET](#job-status-lordose-get) - Auslesen von AD-Werten Lordose KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x30 0x05 inputOutputControlParameter: 0x01 (reportCurrentState)
- [STATUS_LP_TEMP_GET](#job-status-lp-temp-get) - Auslesen intern gemessenener Leiterplattentemperatur KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x04
- [STATUS_LVK](#job-status-lvk) - Auslesen des Sitz-Lehne-Verriegelungswertes KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x02 +---------+----------------+ | AD-Wert |  LVK Status    | +---------+----------------+ |   0- 26 | MasseSchluss   | |  27-126 | ungueltig      | | 127-153 | entriegelt     | | 154-210 | ungueltig      | | 211-237 | verriegelt     | | 238-255 | nicht gesteckt | +---------+----------------+
- [STATUS_SITZPOS_GET](#job-status-sitzpos-get) - Auslesen des Portzustandes für Erkennung Sitz vorne/hinten und Fahrer/Beifahrer KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x00
- [STATUS_SPANNUNG_GET](#job-status-spannung-get) - Auslesen interner gemessener Spannungswerte bzw. Zustand KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x08     , 0x01 (report), 0x03
- [STATUS_SVS](#job-status-svs) - Auslesen des Sitz-Verstell-Schalter Wertes KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x04 0x03 inputOutputControlParameter: 0x01 (reportCurrentState) +---------+-------------+-------------+-------------------------+-------------+ | AD-Wert |  Kanal A    |  Kanal B    |  Kanal C                |  Kanal D    | +---------+-------------+-------------+-------------------------+-------------+ |   0- 26 | MasseSchluss| MasseSchluss| MasseSchluss            | MasseSchluss| |  27- 61 | SLVvor      | LNVvor      | SNVtief                 | LBVvor      | |  62- 97 | SLVzurueck  | LNVzurueck  | SNVhoch                 | LBVzurueck  | |  98-133 | SHVtief     | KHVtief     | Memorytaste             | STVvor      | | 134-171 | SHVhoch     | KHVhoch     | -----------             | STVzurueck  | | 172-214 | MemoryPos1  | MemoryPos2  | Schalter gesteckt       | ----------  | | 215-255 | kein Taster | kein Taster | Schalter nicht gesteckt | kein Taster | +---------+-------------+-------------+-------------------------+-------------+
- [STATUS_SVS_SBUS](#job-status-svs-sbus) - Abfrage der betaetigten Tasten links (nur E60) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : ECUDevelopmentMode ECUAdjustmentMode
- [STATUS_NORMIERLAUF](#job-status-normierlauf) - Auslesen Status Normierlauf KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0x0E inputOutputControlParameter: 0x01 (reportCurrentState)
- [STATUS_HUNG_KEY_GET](#job-status-hung-key-get) - Auslesen Status Hung-Key S-Bus SVS KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x00
- [STATUS_VERSTELLCOUNTER_GET](#job-status-verstellcounter-get) - Auslesen Anzahl Verstellungen seit letzter Normierung KWP2000: $30 InputOutputControlByLocalIdentifier letzter Normierung - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x00
- [STEUERN_AKTIVSITZ](#job-steuern-aktivsitz) - Ansteuerung Aktivsitz Magnet und Pumpe KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (Identifier): 0x38 inputOutputControlParameter: 0x06 (executeControlOption) Argument 1: Magnet/Pumpe/Zyklus/Nockenmotor --&gt; 0x00, 0x01, 0x02, 0x06 controlState (Argument 2): 0x01, 0x00, 0x02  Timeoutzeit: 3s
- [STEUERN_HALL_COUNTER_RESET](#job-steuern-hall-counter-reset) - Reset der Hallzähler durchführen KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x18     , 0x06 (exe)   , 0x09
- [STEUERN_HALL_TEST](#job-steuern-hall-test) - Testroutine für Hallzähler starten/stoppen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0xXX (XX = 00..08, Wert zu Argument 1 = Motor-Bezeichnung) inputOutputControlParameter: 0x06 (executeControlOption) controlState (Argument 2): 0x01, 0x00  Timeoutzeit: 10s
- [STEUERN_HEIZ](#job-steuern-heiz) - Ansteuerung der Heizungstreiber über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (Identifier): 0x20 inputOutputControlParameter: 0x06 (executeControlOption) Argument 1: Heiz.-Ausgang --&gt; 0x00..0x03 controlState (Argument 2): 0x01, 0x00  Timeoutzeit: 10s
- [STEUERN_HEIZ_TAKT](#job-steuern-heiz-takt) - Getaktete Ansteuerung der Heizungstreiber über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (Identifier): 0x20 inputOutputControlParameter: 0x06 (executeControlOption) Argument 1: Heiz.-Ausgang --&gt; 0x04.. weitere Argumente: Heizungsstufen und Taktverhältnisse  Funktionsbedingungen für Stufe1, Stufe2 und Stufe3: Klemme R und Klemme 15 an  Timeoutzeit: 250s
- [STEUERN_KLIMA_DREHZAHL](#job-steuern-klima-drehzahl) - Drehzahlumschaltung Klimalüfter über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x28 0x01 (Kissen) 0x28 0x02 (Lehne) inputOutputControlParameter: 0x06 (executeControlOption) controlState (Argument 2): 0x01, 0x00  Timeoutzeit: 60s
- [STEUERN_KLIMA_GESAMT](#job-steuern-klima-gesamt) - Ansteuerung der Klimalüfter über I/O-Control verbunden mit Drehzahlumschaltung Kombination der Jobs STEUERN_KLIMA_MOTOREN und STEUERN_KLIMA_DREHZAHL mit den entsprechenden Telegrammen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x28 0x00/01/02 inputOutputControlParameter: 0x06 (executeControlOption) controlState: jeweils 0x01/0x00
- [STEUERN_KLIMA_MOTOREN](#job-steuern-klima-motoren) - Ansteuerung der Klimalüfter über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x28 0x00 inputOutputControlParameter: 0x06 (executeControlOption) controlState (Argument): 0x01, 0x00  Timeoutzeit: 60s
- [STEUERN_LORDOSE](#job-steuern-lordose) - Ansteuerung Lordose Ventile und Pumpe über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (Identifier): 0x30 inputOutputControlParameter: 0x06 (executeControlOption) Argument 1: Ventil# bzw. Pumpe --&gt; 0x00..0x04 controlState (Argument 2): 0x01, 0x00  Timeoutzeit: 10s
- [STEUERN_MOTOR](#job-steuern-motor) - Ansteuerung der Verstellmotoren über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (Identifier): 0x10 inputOutputControlParameter: 0x06 (executeControlOption) Argument 1: Motor-Bezeichnung --&gt; 0x00..0x07 controlState (Argument 2): 0x01, 0x02, 0x00 Argument 3: Takt für PWM-Ansteuerung --&gt; 0..100 (%) oder 200 (Normierlauf)  Timeoutzeit: 3s
- [STEUERN_NORMIERLAUF](#job-steuern-normierlauf) - Normierlauf fuer SLV und KHV KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x06 (exe)   , 0x0A Argument : "AKTION" - z.B.   : "an" - z.B.   : STEUERN_NORMIERLAUF "an" -          startet den Normierlauf. Timeout  : 4 min
- [STEUERN_SPANNUNG](#job-steuern-spannung) - Ein/Ausschalten von internen Betriebsspannungen KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x08     , 0x06 (exe)   , 0xXX (XX Argument 1: Name d. Spg. --&gt; 0x00..0x04) controlState (Argument 2): 0x01, 0x00  Timeoutzeit: 60s
- [STEUERN_SVS_LED](#job-steuern-svs-led) - Ein/Ausschalten von Sitz-Verstell-Schalter LED KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x06 (exe)   , 0x0B controlState (Argument 1): 0x01, 0x00  Timeoutzeit: 60s
- [STEUERN_SVS_LED_SBUS](#job-steuern-svs-led-sbus) - Ein/Ausschalten von Sitz-Verstell-Schalter LED KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x06 (exe)   , 0x0B controlState (Argument 1): 0x01, 0x00  Timeoutzeit: 60s
- [STEUERN_SVS_SBUS_SLEEP_WAKEUP](#job-steuern-svs-sbus-sleep-wakeup) - Ein/Ausschalten von Sitz-Verstell-Schalter SBUS KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x06 (exe)   , 0x0B controlState (Argument 1): 0x01, 0x00  Timeoutzeit: 30s
- [STEUERN_SET_BLOCK](#job-steuern-set-block) - Setzen von Hartbloecken relativ zur aktuellen Sitzposition KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID IOLI = 0x13 , 0x00 0x01 (reportCurrentState) Timeoutzeit: 60s

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

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus $04 requestIdentifiedShadowMemoryDTCAndStatus

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

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default

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

<a id="job-fs-loeschen-einzeln"></a>
### FS_LOESCHEN_EINZELN

Fehlerspeicher loeschen, einzelner Fehler KWP2000: $14 ClearDiagnosticInformation $xxxx DTC (SM-spezifisch) SM-spezifischer Job Beispielargument: "0x9E48" siehe auch unter Befehl fs_lesen, Result F_ORT_NR

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NR_OF_DTC | int | einzelner zu loeschender Fehler speziell fuer Shadow-Speicher |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-energy-saving-state"></a>
### READ_ENERGY_SAVING_STATE

Aktuellen FETRAWE-Mode des SG auslesen FETRAWE-Mode: Fertigungs-, Transport- und Werkstatt- Mode KWP2000: $22 ReadDataByCommonIdentifier $100A EnergySavingState

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CURRENT_STATE | string | 0x00 = All energy saving modes deactivated 0x01 = Production Mode 0x02 = Shipment Mode 0x04 = Repair Shop Mode |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-communication"></a>
### START_COMMUNICATION

Kommunikation mit Standard KWP2000 starten KWP2000: $81 StartCommunication

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| KEYBYTES | string | Keybytes 1 und 2 vom SG (0x6B, 0x8F) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-communication"></a>
### STOP_COMMUNICATION

Kommunikation mit Standard KWP2000 beenden KWP2000: $82 StopCommunication

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-wait-n-seconds"></a>
### WAIT_N_SECONDS

Wartet die angeforderte Anzahl von Sekunden -&gt; fuer Testablaeufe mit Toolset

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NR_OF_SECONDS | unsigned char | Anzahl der Sekunden, die gewartet werden soll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ident-bmw-nr"></a>
### IDENT_BMW_NR

Auslesen BMW-Teilenummer KWP2000: $1A ReadECUIdentification IO     : $91

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-bootloader-sw-nr"></a>
### IDENT_BOOTLOADER_SW_NR

Auslesen der Bootloader SW Versionsnummer KWP2000: $1A ReadECUIdentification IO     : §8A

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BOOTLOADER | string | Bootloader SW-Version |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-change-index"></a>
### IDENT_CHANGE_INDEX

Auslesen BMW-Teilenummer KWP2000: $1A ReadECUIdentification IO     : §88

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_CHANGE_INDEX | string | drawing change index of BMW part number |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-read-current-uif-table"></a>
### IDENT_READ_CURRENT_UIF_TABLE

Aktuelles UIF mit $1A $86 auslesen KWP2000: $1A ReadECUIdentification IO     : $86 Read Current ECU-UIF-Table

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_VIN | string | BMW-Fahrzeugidentifikation |
| ID_BMW_PROGRAMMING_DATE | string | BMW-Programmierdatum |
| ID_BMW_ASSEMBLY_NR | string | BMW-Montage-Nummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-temic-hw-nr"></a>
### IDENT_TEMIC_HW_NR

Auslesen TEMIC-Teilenummer KWP2000: $1A ReadECUIdentification IO: §92

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_TEMIC_HW_NR | string | TEMIC-Teilenummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-temic-hw-vers-nr"></a>
### IDENT_TEMIC_HW_VERS_NR

Auslesen TEMIC-HW-Versions-Nummern KWP2000: $1A ReadECUIdentification IO: §93

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_TEMIC_LP_NR | string | TEMIC-Leiterplatten-Nummer+Index |
| ID_TEMIC_STL_NR | string | TEMIC-Stuecklisten-Nr.+Index |
| ID_TEMIC_EPR_NR | string | TEMIC-Endprodukt-Nr.+Index |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-svs-sbus-sw-nr"></a>
### IDENT_SVS_SBUS_SW_NR

ID-Daten des Sitzverstellschalters links KWP2000: $21 ReadDataByLocalIdentifier  Modus  : all

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| MFS_ID_PROJEKT | string | Projektbezeichnung |
| MFS_ID_RELEASE | string | Versionsnummer |
| MFS_ID_DELIVERY_DATE | string | Entwicklungstag |
| MFS_ID_CODEGENERATION_DATE | string | Tag der Codegenenierung |
| MFS_ID_BMW_HW_NUMMER | string | BMW HW-Nummer in EE |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktivsitz-ad-get"></a>
### STATUS_AKTIVSITZ_AD_GET

AD-Werte Aktivsitz auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x38 0x04 inputOutputControlParameter: 0x01 (reportCurrentState)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AD_SENSE | unsigned char | eingelesener AD-Wert des Messeinganges Sense 1/2 (Motor AS) CS_1, antwort[7] |
| STAT_AD_MAGNET | unsigned char | eingelesener AD-Wert des Messeinganges Magnet AS CS_2, antwort[8] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktivsitz-schalter-get"></a>
### STATUS_AKTIVSITZ_SCHALTER_GET

Status Schalter Aktivsitz auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x38 0x03 inputOutputControlParameter: 0x01 (reportCurrentState) eingelesener Zustand des Druckschalters Aktivsitz Nockenschalter Aktivsitz abhaengig von verbauten System Pneumatisches System Hydraulisches System CS_1, antwort[7]

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SCHALTER | string | eingelesener Zustand des Druckschalters Aktivsitz CS_1, antwort[7] 0x00 --&gt; beide Schalter geschlossen 0x01 --&gt; mind. ein Schalter offen Status Druckschalters Aktivsitz mit hydraulischen System |
| STAT_TYP_AKTIVSITZ | string | System\|	hydraulisch	    	\|                 pneumatisch ------------------------------------------------------------------ Result  \|	Druckschalter  	\|	Druckschalter \|	Nockenschalter ------------------------------------------------------------------ 0	  \|	beide offen	    	\| 	offen		   \|	offen 1	  \|	mind. einer offen	\| 	geschlossen   \|	geschlossen 2,3	  \|	ungueltig	    	\|	ungueltig	   \|	ungueltig |
| STAT_DRUCKSCHALTER_PNEUMATISCH | string | Status Druckschalters Aktivsitz mit pneumatischen System |
| STAT_NOCKENSCHALTER | string | Status Nockenschalter |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-feh-schalter"></a>
### STATUS_FEH_SCHALTER

Auslesen des Portzustandes für Erkennung Fond-Einstiegshilfe vor/zurueck KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x04

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FEH | string | eingelesener Portzustand des Schalters 0x00 --&gt; unbetaetigt 0x01 --&gt; Fond-Einstiegshilfe VOR 0x02 --&gt; Fond-Einstiegshilfe ZUR 0x03 --&gt; Signal ungültig CS_1, antwort[7] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hall-ad-lbv-khv-get"></a>
### STATUS_HALL_AD_LBV_KHV_GET

AD-Werte der Hallsensoren auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0x0C inputOutputControlParameter: 0x01 (reportCurrentState)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AD_LBV | unsigned char | AD-Wert Halleingang LBV (0..255) CS_1, antwort[7] |
| STAT_AD_KHV | unsigned char | AD-Wert Halleingang KHV	(0..255) CS_2, antwort[8] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hall-ad-shv-snv-stv-get"></a>
### STATUS_HALL_AD_SHV_SNV_STV_GET

AD-Werte der Hallsensoren auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0x0B inputOutputControlParameter: 0x01 (reportCurrentState)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AD_SHV | unsigned char | AD-Wert Halleingang SHV (0..255) CS_1, antwort[7] |
| STAT_AD_SNV | unsigned char | AD-Wert Halleingang SNV	(0..255) CS_2, antwort[8] |
| STAT_AD_STV | unsigned char | AD-Wert Halleingang STV	(0..255) CS_3, antwort[9] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hall-ad-slv-lnv-lkv-get"></a>
### STATUS_HALL_AD_SLV_LNV_LKV_GET

AD-Werte der Hallsensoren auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0x0A inputOutputControlParameter: 0x01 (reportCurrentState)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AD_SLV | unsigned char | AD-Wert Halleingang SLV (0..255) CS_1, antwort[7] |
| STAT_AD_LNV | unsigned char | AD-Wert Halleingang LNV	(0..255) CS_2, antwort[8] |
| STAT_AD_LKV | unsigned char | AD-Wert Halleingang LKV	(0..255) CS_3, antwort[9] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hall-ad"></a>
### STATUS_HALL_AD

AD-Werte der Hallsensoren auslesen KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x18     , 0x01 (report), 0x0D

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AD_SLV | unsigned char | AD-Wert Halleingang SLV (0..255) CS_1, antwort[7] |
| STAT_AD_SHV | unsigned char | AD-Wert Halleingang SHV (0..255) CS_2, antwort[8] |
| STAT_AD_LNV | unsigned char | AD-Wert Halleingang LNV (0..255) CS_3, antwort[9] |
| STAT_AD_SNV | unsigned char | AD-Wert Halleingang SNV (0..255) CS_4, antwort[10] |
| STAT_AD_KHV | unsigned char | AD-Wert Halleingang KHV (0..255) CS_5, antwort[11] |
| STAT_AD_STV | unsigned char | AD-Wert Halleingang STV (0..255) CS_5, antwort[13] |
| STAT_AD_LBV | unsigned char | AD-Wert Halleingang LBV (0..255) CS_5, antwort[14] |
| STAT_AD_LKV | unsigned char | AD-Wert Halleingang LKV (0..255) CS_5, antwort[15] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hall-counter-get"></a>
### STATUS_HALL_COUNTER_GET

alle Hallzählerstände auslesen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0x0E inputOutputControlParameter: 0x01 (reportCurrentState)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_COUNTER_SLV | unsigned int | Hallzaehlerstand SLV (0..65535) CS_1, antwort[7] (High) und antwort[8] (Low) |
| STAT_COUNTER_SHV | unsigned int | Hallzaehlerstand SHV (0..65535) CS_2, antwort[9] (High) und antwort[10] (Low) |
| STAT_COUNTER_LBV | unsigned int | Hallzaehlerstand LBV (0..65535) CS_3, antwort[11] (High) und antwort[12] (Low) |
| STAT_COUNTER_LNV | unsigned int | Hallzaehlerstand LNV (0..65535) CS_4, antwort[13] (High) und antwort[14] (Low) |
| STAT_COUNTER_SNV | unsigned int | Hallzaehlerstand SNV (0..65535) CS_5, antwort[15] (High) und antwort[16] (Low) |
| STAT_COUNTER_KHV | unsigned int | Hallzaehlerstand KHV (0..65535) CS_6, antwort[17] (High) und antwort[18] (Low) |
| STAT_COUNTER_LKV | unsigned int | Hallzaehlerstand LKV (0..65535) CS_7, antwort[19] (High) und antwort[20] (Low) |
| STAT_COUNTER_STV | unsigned int | Hallzaehlerstand STV (0..65535) CS_8, antwort[21] (High) und antwort[22] (Low) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-heiz-get"></a>
### STATUS_HEIZ_GET

Auslesen von Heizungs-Temperatur-Werten KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x20 0x05 inputOutputControlParameter: 0x01 (reportCurrentState)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMP_KISSEN_SCHNELLH_WERT | int | intern gemessene Temperatur Kissen 1 CS_1, antwort[7] |
| STAT_TEMP_KISSEN_RESTH_WERT | int | intern gemessene Temperatur Kissen 2 CS_2, antwort[8] |
| STAT_TEMP_LEHNE_SCHNELLH_WERT | int | intern gemessene Temperatur Lehne 1 CS_3, antwort[9] |
| STAT_TEMP_LEHNE_RESTH_WERT | int | intern gemessene Temperatur Lehne 2 CS_4, antwort[10] |
| STAT_TEMP_EINH | string | Einheit: Grad Celsius |
| STAT_AD_SENSE_KI_WERT | unsigned char | Messwert Sense Heizungstreiber Kissen AD-Wert, 8bit unsigned char CS_5, antwort[11] |
| STAT_AD_SENSE_LE_WERT | unsigned char | Messwert Sense Heizungstreiber Lehne AD-Wert, 8bit unsigned char CS_6, antwort[12] |
| STAT_AD_SENSE_EINH | string | Einheit: AD-Wert, 8bit unsigned char |
| STAT_HEIZ_STUFE | unsigned char | Status Heizungs Stufe CS_3, antwort[14] |
| STAT_PWM_KISSEN_SCHNELLH_WERT | unsigned char | PWM Verhaeltnis Kissen Schnellheizfeld CS_3, antwort[15] |
| STAT_PWM_KISSEN_RESTH_WERT | unsigned char | PWM Verhaeltnis Kissen Restheizfeld CS_3, antwort[16] |
| STAT_PWM_LEHNE_SCHNELLH_WERT | unsigned char | PWM Verhaeltnis Lehne Schnellheizfeld CS_3, antwort[17] |
| STAT_PWM_LEHNE_RESTH_WERT | unsigned char | PWM Verhaeltnis Lehne Restheizfeld CS_3, antwort[18] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klima-get"></a>
### STATUS_KLIMA_GET

Auslesen von Klimalüfter-AD-Werten KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x28 0x03 inputOutputControlParameter: 0x01 (reportCurrentState)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AD_DREHZAHL_KISSEN | unsigned char | eingelesener AD-Wert von Messeingang Drehzahlsteuerung Kissen CS_1, antwort[7] |
| STAT_AD_DREHZAHL_LEHNE | unsigned char | eingelesener AD-Wert von Messeingang Drehzahlsteuerung Kissen CS_2, antwort[8] |
| STAT_AD_VERSORGUNG | unsigned char | eingelesener AD-Wert von Messeingang Versorgung Luefter CS_3, antwort[9] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lordose-get"></a>
### STATUS_LORDOSE_GET

Auslesen von AD-Werten Lordose KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x30 0x05 inputOutputControlParameter: 0x01 (reportCurrentState)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AD_PUMPE | unsigned char | eingelesener AD-Wert von Messeingang Versorgung Pumpe Lordose CS_1, antwort[7] |
| STAT_TREIBER | unsigned char | eingelesener Wert von Statusabfrage Treiber CS_2, antwort[8] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lp-temp-get"></a>
### STATUS_LP_TEMP_GET

Auslesen intern gemessenener Leiterplattentemperatur KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x04

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LP_TEMP_WERT | string | intern gemessene Leiterplattentemperatur CS_1, antwort[7] |
| STAT_LP_TEMP_EINH | string | Einheit: AD-Wert, in Grad Celsius |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lvk"></a>
### STATUS_LVK

Auslesen des Sitz-Lehne-Verriegelungswertes KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x02 +---------+----------------+ | AD-Wert |  LVK Status    | +---------+----------------+ |   0- 26 | MasseSchluss   | |  27-126 | ungueltig      | | 127-153 | entriegelt     | | 154-210 | ungueltig      | | 211-237 | verriegelt     | | 238-255 | nicht gesteckt | +---------+----------------+

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AD_LVK_WERT | unsigned char | Messwert Sense Sitz-Lehne-Verriegelung AD-Wert, 8bit unsigned char CS_1, antwort[7] |
| STAT_AD_LVK_EINH | string | Einheit: AD-Wert, 8bit unsigned char |
| STAT_LVK | string | Bedeutung Ad-Wert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sitzpos-get"></a>
### STATUS_SITZPOS_GET

Auslesen des Portzustandes für Erkennung Sitz vorne/hinten und Fahrer/Beifahrer KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VORNE_HINTEN | string | eingelesener Portzustand der Codierung 0x00 --&gt; Vorne, 0x01 --&gt; Hinten CS_1, antwort[7] |
| STAT_FA_BF | string | eingelesener Portzustand der Codierung 0x00 --&gt; Fahrer, 0x01 --&gt; Beifahrer CS_2, antwort[8] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spannung-get"></a>
### STATUS_SPANNUNG_GET

Auslesen interner gemessener Spannungswerte bzw. Zustand KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x08     , 0x01 (report), 0x03

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AD_UBATT_WERT | real | intern gemessene Batteriespannung UREG CS_1, antwort[7] |
| STAT_AD_UBATT_EINH | string | Einheit: AD-Wert, in Volt |
| STAT_FLASHSP | string | 0x00 --&gt; Fehler, 0x01 --&gt; erfolgreich CS_2, antwort[8] |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-svs"></a>
### STATUS_SVS

Auslesen des Sitz-Verstell-Schalter Wertes KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x04 0x03 inputOutputControlParameter: 0x01 (reportCurrentState) +---------+-------------+-------------+-------------------------+-------------+ | AD-Wert |  Kanal A    |  Kanal B    |  Kanal C                |  Kanal D    | +---------+-------------+-------------+-------------------------+-------------+ |   0- 26 | MasseSchluss| MasseSchluss| MasseSchluss            | MasseSchluss| |  27- 61 | SLVvor      | LNVvor      | SNVtief                 | LBVvor      | |  62- 97 | SLVzurueck  | LNVzurueck  | SNVhoch                 | LBVzurueck  | |  98-133 | SHVtief     | KHVtief     | Memorytaste             | STVvor      | | 134-171 | SHVhoch     | KHVhoch     | -----------             | STVzurueck  | | 172-214 | MemoryPos1  | MemoryPos2  | Schalter gesteckt       | ----------  | | 215-255 | kein Taster | kein Taster | Schalter nicht gesteckt | kein Taster | +---------+-------------+-------------+-------------------------+-------------+

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SVS_AD_WERT_KANAL_A | unsigned char | Ad-Wert Sitz-Verstell-Schalter Kanal A AD-Wert, 8bit unsigned char CS_1, antwort[7] |
| STAT_SVS_AD_WERT_KANAL_B | unsigned char | Ad-Wert Sitz-Verstell-Schalter Kanal B AD-Wert, 8bit unsigned char CS_2, antwort[8] |
| STAT_SVS_AD_WERT_KANAL_C | unsigned char | Ad-Wert Sitz-Verstell-Schalter Kanal C AD-Wert, 8bit unsigned char CS_3, antwort[9] |
| STAT_SVS_AD_WERT_KANAL_D | unsigned char | Ad-Wert Sitz-Verstell-Schalter Kanal D AD-Wert, 8bit unsigned char CS_4, antwort[10] |
| STAT_SVS_KANAL_A | string | Bedeutung Ad-Wert Kanal A |
| STAT_SVS_KANAL_B | string | Bedeutung Ad-Wert Kanal B |
| STAT_SVS_KANAL_C | string | Bedeutung Ad-Wert Kanal C |
| STAT_SVS_KANAL_D | string | Bedeutung Ad-Wert Kanal D |
| STAT_AD_SVS_EINH | string | Einheit: AD-Wert, 8bit unsigned char |
| STAT_SCHALTER_SLV | string | Status des SVS (SLV) |
| STAT_SCHALTER_SNV | string | Status des SVS (SNV) |
| STAT_SCHALTER_SHV | string | Status des SVS (SHV) |
| STAT_SCHALTER_LNV | string | Status des SVS (LNV) |
| STAT_SCHALTER_KHV | string | Status des SVS (KHV) |
| STAT_TASTER_MEM_POS1 | string | Status des SVS (MEM_POS1) |
| STAT_TASTER_MEM_POS2 | string | Status des SVS (MEM_POS2) |
| STAT_TASTER_MEM_AKT | string | Status des SVS (MEM_AKT) |
| STAT_SCHALTER_ANSCHLUSS | string | Status des SVS (ANSCHLUSS) |
| STAT_SCHALTER_LBV | string | Status des SVS (LBV) |
| STAT_SCHALTER_STV | string | Status des SVS (STV) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-svs-sbus"></a>
### STATUS_SVS_SBUS

Abfrage der betaetigten Tasten links (nur E60) KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : ECUDevelopmentMode ECUAdjustmentMode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TASTE_MEM_M | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_MEM_1 | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_MEM_2 | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_SL_UP | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_SL_DWN | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_SL_TLT_FRONT | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_SL_TLT_BACK | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_SEAT_UP | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_SEAT_DWN | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_SEAT_MOVE_FRONT | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_SEAT_MOVE_BACK | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_SEAT_TILT_FRONT | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_SEAT_TILT_BACK | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_BASE_MOVE_FRONT | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_BASE_MOVE_BACK | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_BASE_TILT_DOWN | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_BASE_TILT_UP | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_LD_UP | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_LD_DWN | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_LD_FORWARD | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_LD_BACKWARD | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_LBV_FRONT | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| STAT_TASTE_LBV_BACK | int | 1: Taste betaetigt 0: Taste nicht betaetigt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-normierlauf"></a>
### STATUS_NORMIERLAUF

Auslesen Status Normierlauf KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0x0E inputOutputControlParameter: 0x01 (reportCurrentState)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NORMIERLAUF_AKITV | string | Status Normierlauf aktiv CS_1, antwort[7] |
| STAT_COUNTER_NORMBLOCK_SLV_VORNE | unsigned int | Normblock SLV vorne (0..65535) CS_1, antwort[8] (High) und antwort[9] (Low) |
| STAT_NORMIERSTATUS_SLV_VORNE | string | Status Normierung SLV vorne "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_SLV_HINTEN | unsigned int | Normblock SLV hinten (0..65535) CS_1, antwort[10] (High) und antwort[11] (Low) |
| STAT_NORMIERSTATUS_SLV_HINTEN | string | Status Normierung SLV hinten "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_SLV_ADAPTIONSLAUF_AKTIV | string | Status Adaptionslauf SLV aktiv |
| STAT_SLV_ADAPTIONSLAUF_FEHLER | string | Status SLV Adaptionslauffehler |
| STAT_SLV_NORMIERABSTAND_PLAUSIBEL | string | Normierblockabstand beider Normbloecke SLV-Achse plausibel |
| STAT_SLV_ENTNRM_URSACHE_VORNE | string | Entnormierursache SLV Normblock vorne |
| STAT_SLV_ENTNRM_URSACHE_HINTEN | string | Entnormierursache SLV Normblock hinten |
| STAT_COUNTER_NORMBLOCK_SHV_OBEN | unsigned int | Normblock SHV oben (0..65535) CS_1, antwort[12] (High) und antwort[13] (Low) |
| STAT_NORMIERSTATUS_SHV_OBEN | string | Status Normierung SHV oben "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_SHV_UNTEN | unsigned int | Normblock SHV unten (0..65535) CS_1, antwort[14] (High) und antwort[15] (Low) |
| STAT_NORMIERSTATUS_SHV_UNTEN | string | Status Normierung SHV unten "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_LNV_VORNE | unsigned int | Normblock LNV vorne (0..65535) CS_1, antwort[16] (High) und antwort[17] (Low) |
| STAT_NORMIERSTATUS_LNV_VORNE | string | Status Normierung LNV vorne "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_LNV_HINTEN | unsigned int | Normblock LNV unten (0..65535) CS_1, antwort[18] (High) und antwort[19] (Low) |
| STAT_NORMIERSTATUS_LNV_HINTEN | string | Status Normierung LNV hinten "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_SNV_OBEN | unsigned int | Normblock SNV oben (0..65535) CS_1, antwort[20] (High) und antwort[21] (Low) |
| STAT_NORMIERSTATUS_SNV_OBEN | string | Status Normierung SNV oben "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_SNV_UNNTEN | unsigned int | Normblock SNV unten (0..65535) CS_1, antwort[22] (High) und antwort[23] (Low) |
| STAT_NORMIERSTATUS_SNV_UNTEN | string | Status Normierung SNV unten "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_KHV_OBEN | unsigned int | Normblock KHV oben (0..65535) CS_1, antwort[24] (High) und antwort[25] (Low) |
| STAT_NORMIERSTATUS_KHV_OBEN | string | Status Normierung KHV oben "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_KHV_UNTEN | unsigned int | Normblock KHV unten (0..65535) CS_1, antwort[26] (High) und antwort[27] (Low) |
| STAT_NORMIERSTATUS_KHV_UNTEN | string | Status Normierung KHV unten "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_STV_VORNE | unsigned int | Normblock STV vorne (0..65535) CS_1, antwort[28] (High) und antwort[29] (Low) |
| STAT_NORMIERSTATUS_STV_VORNE | string | Status Normierung STV vorne "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_STV_HINTEN | unsigned int | Normblock STV hinten (0..65535) CS_1, antwort[30] (High) und antwort[31] (Low) |
| STAT_NORMIERSTATUS_STV_HINTEN | string | Status Normierung STV hinten "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_LBV_SCHMAL | unsigned int | Normblock LBV schmal (0..65535) CS_1, antwort[32] (High) und antwort[33] (Low) |
| STAT_NORMIERSTATUS_LBV_SCHMAL | string | Status Normierung LBV schmal "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_LBV_BREIT | unsigned int | Normblock LBV breit (0..65535) CS_1, antwort[34] (High) und antwort[35] (Low) |
| STAT_NORMIERSTATUS_LBV_BREIT | string | Status Normierung LBV breit "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_LKV_VORNE | unsigned int | Normblock LKV vorne (0..65535) CS_1, antwort[36] (High) und antwort[37] (Low) |
| STAT_NORMIERSTATUS_LKV_VORNE | string | Status Normierung LKV vorne "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| STAT_COUNTER_NORMBLOCK_LKV_HINTEN | unsigned int | Normblock LKV hinten (0..65535) CS_1, antwort[38] (High) und antwort[39] (Low) |
| STAT_NORMIERSTATUS_LKV_HINTEN | string | Status Normierung LKV hinten "ACHSE NORMIERT" "ACHSE NICHT NORMIERT" beide Normbloecke hierzu abfragen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hung-key-get"></a>
### STATUS_HUNG_KEY_GET

Auslesen Status Hung-Key S-Bus SVS KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HUNG_KEY_SLV_FRONT | int | 1: Taster SVS-SLV-vor haengt 0: Taster SVS-SLV-vor haengt nicht |
| STAT_HUNG_KEY_SLV_BACK | int | 1: Taster SVS-SLV-zurueck haengt 0: Taster SVS-SLV-zureuck haengt nicht |
| STAT_HUNG_KEY_SHV_UP | int | 1: Taster SVS-SHV-auf haengt 0: Taster SVS-SHV-auf haengt nicht |
| STAT_HUNG_KEY_SHV_DOWN | int | 1: Taster SVS-SHV-ab haengt 0: Taster SVS-SHV-ab haengt nicht |
| STAT_HUNG_KEY_SNV_UP | int | 1: Taster SVS-SNV-auf haengt 0: Taster SVS-SNV-auf haengt nicht |
| STAT_HUNG_KEY_SNV_DOWN | int | 1: Taster SVS-SNV-ab haengt 0: Taster SVS-SNV-ab haengt nicht |
| STAT_HUNG_KEY_LNV_FRONT | int | 1: Taster SVS-LNV-vor haengt 0: Taster SVS-LNV-vor haengt nicht |
| STAT_HUNG_KEY_LNV_BACK | int | 1: Taster SVS-LNV-zur haengt 0: Taster SVS-LNV-zur haengt nicht |
| STAT_HUNG_KEY_LBV_BACK | int | 1: Taster SVS-LBV-breit haengt 0: Taster SVS-LBV-breit haengt nicht |
| STAT_HUNG_KEY_LBV_FRONT | int | 1: Taster SVS-LBV-schmal haengt 0: Taster SVS-LBV-schmal haengt nicht |
| STAT_HUNG_KEY_KHV_UP | int | 1: Taster SVS-KHV-hoch haengt 0: Taster SVS-KHV-hoch nicht |
| STAT_HUNG_KEY_KHV_DOWN | int | 1: Taster SVS-KHV-ab haengt 0: Taster SVS-KHV-ab haengt nicht |
| STAT_HUNG_KEY_STV_FRONT | int | 1: Taster SVS-STV-vor haengt 0: Taster SVS-STV-vor nicht |
| STAT_HUNG_KEY_STV_BACK | int | 1: Taster SVS-STV-zurueck haengt 0: Taster SVS-STV-zurueck haengt nicht |
| STAT_HUNG_KEY_LORDOSE_UP | int | 1: Taster SVS-Lordose-hoch haengt 0: Taster SVS-Lordose_hoch haengt nicht |
| STAT_HUNG_KEY_LORDOSE_DWN | int | 1: Taster SVS-Lordose-tief haengt 0: Taster SVS-Lordose-tief haengt nicht |
| STAT_HUNG_KEY_LORDOSE_FORWARD | int | 1: Taster SVS-Lordose-vorwaerts haengt 0: Taster SVS-Lordose_breit vorwaerts nicht |
| STAT_HUNG_KEY_LORDOSE_BACKWARD | int | 1: Taster SVS-Lordose-zurueck haengt 0: Taster SVS-Lordose-zurueck haengt nicht |
| STAT_HUNG_KEY_MEMORY_AKTIV | int | 1: Taster SVS-Memory Aktiv haengt 0: Taster SVS-Memory Aktiv haengt nicht |
| STAT_HUNG_KEY_MEMORY_POS1 | int | 1: Taster SVS-Memory Taster 1 haengt 0: Taster SVS-Memory Taster 1 haengt nicht |
| STAT_HUNG_KEY_MEMORY_POS2 | int | 1: Taster SVS-Memory Taster 2 haengt 0: Taster SVS-Memory Taster 2 haengt nicht |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-verstellcounter-get"></a>
### STATUS_VERSTELLCOUNTER_GET

Auslesen Anzahl Verstellungen seit letzter Normierung KWP2000: $30 InputOutputControlByLocalIdentifier letzter Normierung - Jobnumber, ControlOption, LocalID - 0x04     , 0x01 (report), 0x00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VERSTELLCOUNTER_SLV | long | Anzahl Verstellungen seit Normierung Achse 0 ... 131070 Verstellungen |
| STAT_VERSTELLCOUNTER_SHV | long | Anzahl Verstellungen ab gueltiger Normierung 0 ... 131070 Verstellungen |
| STAT_VERSTELLCOUNTER_LNV | long | Anzahl Verstellungen ab gueltiger Normierung 0 ... 131070 Verstellungen |
| STAT_VERSTELLCOUNTER_SNV | long | Anzahl Verstellungen ab gueltiger Normierung 0 ...131070 Verstellungen |
| STAT_VERSTELLCOUNTER_KHV | long | Anzahl Verstellungen ab gueltiger Normierung 0 ... 131070 Verstellungen |
| STAT_VERSTELLCOUNTER_STV | long | Anzahl Verstellungen ab gueltiger Normierung 0 ... 131070 Verstellungen |
| STAT_VERSTELLCOUNTER_LBV | long | Anzahl Verstellungen ab gueltiger Normierung 0 ... 131070 Verstellungen |
| STAT_VERSTELLCOUNTER_LKV | long | Anzahl Verstellungen ab gueltiger Normierung 0 ... 131070 Verstellungen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-aktivsitz"></a>
### STEUERN_AKTIVSITZ

Ansteuerung Aktivsitz Magnet und Pumpe KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (Identifier): 0x38 inputOutputControlParameter: 0x06 (executeControlOption) Argument 1: Magnet/Pumpe/Zyklus/Nockenmotor --&gt; 0x00, 0x01, 0x02, 0x06 controlState (Argument 2): 0x01, 0x00, 0x02  Timeoutzeit: 3s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG | string | Name des angesteuerten Ausgangs: "MAGNET" (hydraulisch, pneumatisch mit Lordose) "RECHTS" (= Pumprichtung rechts)(hydr.) "ZYKLUS" (= Entleerzyklus durchlaufen) (hydraulisch: Mittenfindzyklus der AS-Kissen pneumatisch: Entleerzyklus der AS-Kissen) "NOCKENMOTOR" (pneumatisch) (* allgemein        *) table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: "MAGNET" = 0 |
| AKTION | string | "an" oder "aus" für Magnet, Nockenmotor "voll", "leer" oder "stop" bei Pumpen "RECHTS" table IOCTRL_Arg    ARG_TEXT  ARG_WERT Defaultwert: "AUS" bzw. "STOP" = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hall-counter-reset"></a>
### STEUERN_HALL_COUNTER_RESET

Reset der Hallzähler durchführen KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x18     , 0x06 (exe)   , 0x09

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTOR | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: alle Hallzähler loeschen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hall-test"></a>
### STEUERN_HALL_TEST

Testroutine für Hallzähler starten/stoppen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x18 0xXX (XX = 00..08, Wert zu Argument 1 = Motor-Bezeichnung) inputOutputControlParameter: 0x06 (executeControlOption) controlState (Argument 2): 0x01, 0x00  Timeoutzeit: 10s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NAME | string | Motor-Bezeichnung: "SLV", "SHV", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: "SLV" = 0x00 |
| AKTION | string | "start" oder "stop" table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-heiz"></a>
### STEUERN_HEIZ

Ansteuerung der Heizungstreiber über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (Identifier): 0x20 inputOutputControlParameter: 0x06 (executeControlOption) Argument 1: Heiz.-Ausgang --&gt; 0x00..0x03 controlState (Argument 2): 0x01, 0x00  Timeoutzeit: 10s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HEIZUNG | string | Heizungs-Ausgang ("KI_SCHNELLH", "KI_RESTH", "LE_SCHNELLH", "LE_RESTH") table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: KI_SCHNELLH = 0 |
| AKTION | string | "an" oder "aus" table DigitalArgument TEXT WERT Defaultwert: AUS = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-heiz-takt"></a>
### STEUERN_HEIZ_TAKT

Getaktete Ansteuerung der Heizungstreiber über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (Identifier): 0x20 inputOutputControlParameter: 0x06 (executeControlOption) Argument 1: Heiz.-Ausgang --&gt; 0x04.. weitere Argumente: Heizungsstufen und Taktverhältnisse  Funktionsbedingungen für Stufe1, Stufe2 und Stufe3: Klemme R und Klemme 15 an  Timeoutzeit: 250s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HEIZUNG | string | Heizungs-Ausgang ("KISSEN_LEHNE", ) table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: "KISSEN_LEHNE" = 0x04 |
| STUFE | string | Heizungsstufe: "Stufe0", "Stufe1", "Stufe2", "Stufe3", "Stufe255" table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STUFE0" = 0x00 |
| TAKT1 | unsigned char | Taktverhältnis von 0 bis 100 (%) Defaultwert: 0 |
| TAKT2 | unsigned char | Taktverhältnis von 0 bis 100 (%) Defaultwert: 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klima-drehzahl"></a>
### STEUERN_KLIMA_DREHZAHL

Drehzahlumschaltung Klimalüfter über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x28 0x01 (Kissen) 0x28 0x02 (Lehne) inputOutputControlParameter: 0x06 (executeControlOption) controlState (Argument 2): 0x01, 0x00  Timeoutzeit: 60s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LUEFTER | string | Lüfter Kissen oder Lehne ("KI", "LE") table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: KI = 1 |
| AKTION | string | Drehzahlstufe: "DR_NIEDRIG" d.h. Stufe ein --&gt; cS=0x01 "DR_HOCH"    d.h. Stufe aus --&gt; cS=0x00 table IOCTRL_Arg    ARG_TEXT  ARG_WERT Defaultwert: DR_HOCH = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klima-gesamt"></a>
### STEUERN_KLIMA_GESAMT

Ansteuerung der Klimalüfter über I/O-Control verbunden mit Drehzahlumschaltung Kombination der Jobs STEUERN_KLIMA_MOTOREN und STEUERN_KLIMA_DREHZAHL mit den entsprechenden Telegrammen KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x28 0x00/01/02 inputOutputControlParameter: 0x06 (executeControlOption) controlState: jeweils 0x01/0x00

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION_MOTOREN | string | Klimalüfter: "an"  --&gt; cS = 0x01 "aus" --&gt; cS = 0x00 table DigitalArgument TEXT WERT Defaultwert: AUS = 0 |
| AKTION_KISSEN | string | Drehzahlstufe Kissen: "DR_NIEDRIG" d.h. Stufe ein --&gt; cS=0x01 "DR_HOCH"    d.h. Stufe aus --&gt; cS=0x00 table IOCTRL_Arg    ARG_TEXT  ARG_WERT Defaultwert: DR_HOCH = 0 |
| AKTION_LEHNE | string | Drehzahlstufe Lehne: "DR_NIEDRIG" d.h. Stufe ein --&gt; cS=0x01 "DR_HOCH"    d.h. Stufe aus --&gt; cS=0x00 table IOCTRL_Arg    ARG_TEXT  ARG_WERT Defaultwert: DR_HOCH = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort 1 von SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort 2 von SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort 3 von SG |

<a id="job-steuern-klima-motoren"></a>
### STEUERN_KLIMA_MOTOREN

Ansteuerung der Klimalüfter über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (LocalIdentifier): IOLI = 0x28 0x00 inputOutputControlParameter: 0x06 (executeControlOption) controlState (Argument): 0x01, 0x00  Timeoutzeit: 60s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | Klimalüfter: "an"  --&gt; cS = 0x01 "aus" --&gt; cS = 0x00 table DigitalArgument TEXT WERT Defaultwert: AUS = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lordose"></a>
### STEUERN_LORDOSE

Ansteuerung Lordose Ventile und Pumpe über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (Identifier): 0x30 inputOutputControlParameter: 0x06 (executeControlOption) Argument 1: Ventil# bzw. Pumpe --&gt; 0x00..0x04 controlState (Argument 2): 0x01, 0x00  Timeoutzeit: 10s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG | string | Name des angesteuerten Ausgangs: "VENTIL1", "VENTIL2", "VENTIL3", "VENTIL4", "PUMPE" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: "VENTIL1" = 0 |
| AKTION | string | "an" oder "aus" table DigitalArgument TEXT WERT Defaultwert: "AUS" = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-motor"></a>
### STEUERN_MOTOR

Ansteuerung der Verstellmotoren über I/O-Control KWP2000: $30 InputOutputControlByLocalIdentifier Jobnummer (Identifier): 0x10 inputOutputControlParameter: 0x06 (executeControlOption) Argument 1: Motor-Bezeichnung --&gt; 0x00..0x07 controlState (Argument 2): 0x01, 0x02, 0x00 Argument 3: Takt für PWM-Ansteuerung --&gt; 0..100 (%) oder 200 (Normierlauf)  Timeoutzeit: 3s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTOR | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION | string | Bewegungsrichtung bzw. Stop: "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| TAKT | unsigned char | Taktverhältnis von 0 bis 100 (%) oder Wert 200 für Normierlauf Defaultwert: 100 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-normierlauf"></a>
### STEUERN_NORMIERLAUF

Normierlauf fuer SLV und KHV KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x06 (exe)   , 0x0A Argument : "AKTION" - z.B.   : "an" - z.B.   : STEUERN_NORMIERLAUF "an" -          startet den Normierlauf. Timeout  : 4 min

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | AKTION-Bezeichnung z.B. "an" table DigitalArgument \| TEXT      \| WERT ------------------------------------------- - Defaultwert:        \| "aus"     \| 0x0 -                     \| "an"      \| 0x1 |
| MOTOR_1 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_1 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_2 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_2 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_3 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_3 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_4 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_4 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_5 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_5 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_6 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_6 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_7 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_7 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_8 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_8 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_9 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_9 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_10 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_10 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_11 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_11 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_12 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_12 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_13 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_13 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_14 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_14 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_15 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_15 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_16 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_16 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_17 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_17 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_18 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_18 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_19 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_19 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_20 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_20 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_21 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_21 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_22 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_22 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_23 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_23 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |
| MOTOR_24 | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| AKTION_24 | string | Bewegungsrichtung bzw. Stop: "adap_zur"               --&gt; cS=0x05 "adap_vor"               --&gt; cS=0x04 "home"                  --&gt; cS=0x03 "hoch", "vor", "breit"  --&gt; cS=0x01 "tief", "zur", "schmal" --&gt; cS=0x02 "stop"                  --&gt; cS=0x00 table IOCTRL_Arg ARG_TEXT ARG_WERT Defaultwert: "STOP" = 0x00 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-spannung"></a>
### STEUERN_SPANNUNG

Ein/Ausschalten von internen Betriebsspannungen KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x08     , 0x06 (exe)   , 0xXX (XX Argument 1: Name d. Spg. --&gt; 0x00..0x04) controlState (Argument 2): 0x01, 0x00  Timeoutzeit: 60s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPANNUNG | string | Name der internen Spannung ("U12S", "Kl30S", "KL30V","UCP","UNTC") table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: "U12S" = 0x00 |
| AKTION | string | "an" oder "aus" table DigitalArgument TEXT WERT Defaultwert: AUS = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-svs-led"></a>
### STEUERN_SVS_LED

Ein/Ausschalten von Sitz-Verstell-Schalter LED KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x06 (exe)   , 0x0B controlState (Argument 1): 0x01, 0x00  Timeoutzeit: 60s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | "an" oder "aus" table DigitalArgument TEXT WERT Defaultwert: AUS = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-svs-led-sbus"></a>
### STEUERN_SVS_LED_SBUS

Ein/Ausschalten von Sitz-Verstell-Schalter LED KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x06 (exe)   , 0x0B controlState (Argument 1): 0x01, 0x00  Timeoutzeit: 60s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | "an" oder "aus" table DigitalArgument TEXT WERT Defaultwert: AUS = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-svs-sbus-sleep-wakeup"></a>
### STEUERN_SVS_SBUS_SLEEP_WAKEUP

Ein/Ausschalten von Sitz-Verstell-Schalter SBUS KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID - 0x04     , 0x06 (exe)   , 0x0B controlState (Argument 1): 0x01, 0x00  Timeoutzeit: 30s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | "sleep" oder "wakeup" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: wakeup = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-set-block"></a>
### STEUERN_SET_BLOCK

Setzen von Hartbloecken relativ zur aktuellen Sitzposition KWP2000: $30 InputOutputControlByLocalIdentifier - Jobnumber, ControlOption, LocalID IOLI = 0x13 , 0x00 0x01 (reportCurrentState) Timeoutzeit: 60s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTOR | string | Motor-Bezeichnung ("SLV", "SHV", "FEH", "LNV", "SNV", "KHV", "LKV", "STV", "LBV" table IOCTRL_Arg   ARG_TEXT ARG_WERT Defaultwert: SLV = 0 |
| BLOCK_PLUS_REL | unsigned int | Blockabstand relativ zur aktuellen Position vor/hoch/breit in Hallimpulse CS_1, antwort[7] (High) und antwort[8] (Low) Defaultwert: BLOCK_PLUS_REL = 0 |
| BLOCK_MINUS_REL | unsigned int | Blockabstand relativ zur aktuellen Position zurueck/tief/schmal in Hallimpulsen CS_1, antwort[9] (High) und antwort[10] (Low) Defaultwert: BLOCK_MINUS_REL = 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
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
- [JOBRESULTEXTENDED](#table-jobresultextended) (3 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (201 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (49 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (4 × 9)
- [IOCTRL_ARG](#table-ioctrl-arg) (63 × 2)
- [IOCTRL_LP_TEMP_PL1](#table-ioctrl-lp-temp-pl1) (255 × 2)
- [IOCTRL_LP_TEMP_PL2](#table-ioctrl-lp-temp-pl2) (256 × 2)
- [IOCTRL_NORMIERUNG](#table-ioctrl-normierung) (9 × 2)

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

Dimensions: 3 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | ERROR_INVALID_ARGUMENT |
| 0x01 | ERROR_INVALID_RESULT_VALUE |
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

Dimensions: 201 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9E48 | keine Hallimpulse SLV  |
| 0x9E49 | keine Hallimpulse SHV  |
| 0x9E4A | keine Hallimpulse LNV  |
| 0x9E4B | keine Hallimpulse SNV  |
| 0x9E4C | keine Hallimpulse KHV  |
| 0x9E4D | keine Hallimpulse FEH  |
| 0x9E4E | keine Hallimpulse STV  |
| 0x9E4F | keine Hallimpulse LBV  |
| 0x9E50 | keine Hallimpulse LKV  |
| 0x9E51 | Fehler Motor SLV  |
| 0x9E52 | Fehler Motor SHV  |
| 0x9E53 | Fehler Motor LNV  |
| 0x9E54 | Fehler Motor SNV  |
| 0x9E55 | Fehler Motor KHV  |
| 0x9E56 | Fehler Motor FEH  |
| 0x9E57 | Fehler Motor STV  |
| 0x9E58 | Fehler Motor LBV  |
| 0x9E59 | Fehler Motor LKV  |
| 0x9E5A | Fehler Schnellheizfeld NTC Kissen  |
| 0x9E5B | Fehler Schnellheizfeld NTC Lehne  |
| 0x9E5C | Fehler Restheizfeld NTC Kissen  |
| 0x9E5D | Fehler Restheizfeld NTC Lehne  |
| 0x9E5E | Fehler Schnellheizfeld Kissen  |
| 0x9E5F | Fehler Schnellheizfeld Lehne  |
| 0x9E60 | Fehler Restheizfeld Kissen  |
| 0x9E61 | Fehler Restheizfeld Lehne  |
| 0x9E62 | Fehler Heizungstreiber durchlegiert oder NTC defekt  |
| 0x9E63 | Fehler Klima Versorgung Kissen und Lehne  |
| 0x9E64 | Fehler Klima Steuerung Kissen  |
| 0x9E65 | Fehler Klima Steuerung Lehne  |
| 0x9E66 | Fehler Aktivsitz Motor  |
| 0x9E67 | Fehler Aktivsitz Magnet  |
| 0x9E68 | Fehler Aktivsitz Druckschalter  |
| 0x9E69 | Fehler Lordose Ventile  |
| 0x9E6A | Fehler Lordose Pumpe  |
| 0x9E6B | Interner Fehler Versorgungsspannung U12s oder U12h  |
| 0x9E6C | interner Fehler Versorgungsspannung Kl30s  |
| 0x9E6D | Interner Fehler EEPROM  |
| 0x9E6E | Energiesparmode aktiv  |
| 0x9E6F | Fehler Schalter SVS  |
| 0x9E70 | Fehler Schalter FEH  |
| 0x9E71 | Fehler Schalter LVK  |
| 0x9E72 | Fehler Schalter MFS-Schalter |
| 0x9E73 | Fehler UEKB Adaptionsbereichueberschreitung vor |
| 0x9E74 | Fehler UEKB Adaptionsbereichueberschreitung zurueck |
| 0x9E75 | Fehler UEKB EE-Bereich defekt |
| 0x9E76 | FehlerUEKB Stromerfassungsfehler |
| 0x9E77 | Fehler Normierung SLV |
| 0xE444 | K-CAN: Bus Leitungsfehler  |
| 0xE447 | Controller, Bus off  |
| 0x9EA8 | keine Hallimpulse SLV  |
| 0x9EA9 | keine Hallimpulse SHV  |
| 0x9EAA | keine Hallimpulse LNV  |
| 0x9EAB | keine Hallimpulse SNV  |
| 0x9EAC | keine Hallimpulse KHV  |
| 0x9EAD | keine Hallimpulse FEH  |
| 0x9EAE | keine Hallimpulse STV  |
| 0x9EAF | keine Hallimpulse LBV  |
| 0x9EB0 | keine Hallimpulse LKV  |
| 0x9EB1 | Fehler Motor SLV  |
| 0x9EB2 | Fehler Motor SHV  |
| 0x9EB3 | Fehler Motor LNV  |
| 0x9EB4 | Fehler Motor SNV  |
| 0x9EB5 | Fehler Motor KHV  |
| 0x9EB6 | Fehler Motor FEH  |
| 0x9EB7 | Fehler Motor STV  |
| 0x9EB8 | Fehler Motor LBV  |
| 0x9EB9 | Fehler Motor LKV  |
| 0x9EBA | Fehler Schnellheizfeld NTC Kissen  |
| 0x9EBB | Fehler Schnellheizfeld NTC Lehne  |
| 0x9EBC | Fehler Restheizfeld NTC Kissen  |
| 0x9EBD | Fehler Restheizfeld NTC Lehne  |
| 0x9EBE | Fehler Schnellheizfeld Kissen  |
| 0x9EBF | Fehler Schnellheizfeld Lehne  |
| 0x9EC0 | Fehler Restheizfeld Kissen  |
| 0x9EC1 | Fehler Restheizfeld Lehne  |
| 0x9EC2 | Fehler Heizungstreiber durchlegiert oder NTC defekt  |
| 0x9EC3 | Fehler Klima Versorgung Kissen und Lehne  |
| 0x9EC4 | Fehler Klima Steuerung Kissen  |
| 0x9EC5 | Fehler Klima Steuerung Lehne  |
| 0x9EC6 | Fehler Aktivsitz Motor  |
| 0x9EC7 | Fehler Aktivsitz Magnet  |
| 0x9EC8 | Fehler Aktivsitz Druckschalter  |
| 0x9EC9 | Fehler Lordose Ventile  |
| 0x9ECA | Fehler Lordose Pumpe  |
| 0x9ECB | Interner Fehler Versorgungsspannung U12s oder U12h  |
| 0x9ECC | interner Fehler Versorgungsspannung Kl30s  |
| 0x9ECD | Interner Fehler EEPROM  |
| 0x9ECE | Energiesparmode aktiv  |
| 0x9ECF | Fehler Schalter SVS  |
| 0x9ED0 | Fehler Schalter FEH  |
| 0x9ED1 | Fehler Schalter LVK  |
| 0x9ED2 | Fehler Schalter MFS-Schalter |
| 0x9ED3 | Fehler UEKB Adaptionsbereichueberschreitung vor |
| 0x9ED4 | Fehler UEKB Adaptionsbereichueberschreitung zurueck |
| 0x9ED5 | Fehler UEKB EE-Bereich defekt |
| 0x9ED6 | FehlerUEKB Stromerfassungsfehler |
| 0x9ED7 | Fehler Normierung SLV |
| 0xE484 | K-CAN: Bus Leitungsfehler  |
| 0xE487 | Controller, Bus off  |
| 0x9F08 | keine Hallimpulse SLV  |
| 0x9F09 | keine Hallimpulse SHV  |
| 0x9F0A | keine Hallimpulse LNV  |
| 0x9F0B | keine Hallimpulse SNV  |
| 0x9F0C | keine Hallimpulse KHV  |
| 0x9F0D | keine Hallimpulse FEH  |
| 0x9F0E | keine Hallimpulse STV  |
| 0x9F0F | keine Hallimpulse LBV  |
| 0x9F10 | keine Hallimpulse LKV  |
| 0x9F11 | Fehler Motor SLV  |
| 0x9F12 | Fehler Motor SHV  |
| 0x9F13 | Fehler Motor LNV  |
| 0x9F14 | Fehler Motor SNV  |
| 0x9F15 | Fehler Motor KHV  |
| 0x9F16 | Fehler Motor FEH  |
| 0x9F17 | Fehler Motor STV  |
| 0x9F18 | Fehler Motor LBV  |
| 0x9F19 | Fehler Motor LKV  |
| 0x9F1A | Fehler Schnellheizfeld NTC Kissen  |
| 0x9F1B | Fehler Schnellheizfeld NTC Lehne  |
| 0x9F1C | Fehler Restheizfeld NTC Kissen  |
| 0x9F1D | Fehler Restheizfeld NTC Lehne  |
| 0x9F1E | Fehler Schnellheizfeld Kissen  |
| 0x9F1F | Fehler Schnellheizfeld Lehne  |
| 0x9F20 | Fehler Restheizfeld Kissen  |
| 0x9F21 | Fehler Restheizfeld Lehne  |
| 0x9F22 | Fehler Heizungstreiber durchlegiert oder NTC defekt  |
| 0x9F23 | Fehler Klima Versorgung Kissen und Lehne  |
| 0x9F24 | Fehler Klima Steuerung Kissen  |
| 0x9F25 | Fehler Klima Steuerung Lehne  |
| 0x9F26 | Fehler Aktivsitz Motor  |
| 0x9F27 | Fehler Aktivsitz Magnet  |
| 0x9F28 | Fehler Aktivsitz Druckschalter  |
| 0x9F29 | Fehler Lordose Ventile  |
| 0x9F2A | Fehler Lordose Pumpe  |
| 0x9F2B | Interner Fehler Versorgungsspannung U12s oder U12h  |
| 0x9F2C | interner Fehler Versorgungsspannung Kl30s  |
| 0x9F2D | Interner Fehler EEPROM  |
| 0x9F2E | Energiesparmode aktiv  |
| 0x9F2F | Fehler Schalter SVS  |
| 0x9F30 | Fehler Schalter FEH  |
| 0x9F31 | Fehler Schalter LVK  |
| 0x9F32 | Fehler Schalter MFS-Schalter |
| 0x9F33 | Fehler UEKB Adaptionsbereichueberschreitung vor |
| 0x9F34 | Fehler UEKB Adaptionsbereichueberschreitung zurueck |
| 0x9F35 | Fehler UEKB EE-Bereich defekt |
| 0x9F36 | FehlerUEKB Stromerfassungsfehler |
| 0x9F37 | Fehler Normierung SLV |
| 0xE344 | K-CAN: Bus Leitungsfehler  |
| 0xE347 | Controller, Bus off  |
| 0x9F68 | keine Hallimpulse SLV  |
| 0x9F69 | keine Hallimpulse SHV  |
| 0x9F6A | keine Hallimpulse LNV  |
| 0x9F6B | keine Hallimpulse SNV  |
| 0x9F6C | keine Hallimpulse KHV  |
| 0x9F6D | keine Hallimpulse FEH  |
| 0x9F6E | keine Hallimpulse STV  |
| 0x9F6F | keine Hallimpulse LBV  |
| 0x9F70 | keine Hallimpulse LKV  |
| 0x9F71 | Fehler Motor SLV  |
| 0x9F72 | Fehler Motor SHV  |
| 0x9F73 | Fehler Motor LNV  |
| 0x9F74 | Fehler Motor SNV  |
| 0x9F75 | Fehler Motor KHV  |
| 0x9F76 | Fehler Motor FEH  |
| 0x9F77 | Fehler Motor STV  |
| 0x9F78 | Fehler Motor LBV  |
| 0x9F79 | Fehler Motor LKV  |
| 0x9F7A | Fehler Schnellheizfeld NTC Kissen  |
| 0x9F7B | Fehler Schnellheizfeld NTC Lehne  |
| 0x9F7C | Fehler Restheizfeld NTC Kissen  |
| 0x9F7D | Fehler Restheizfeld NTC Lehne  |
| 0x9F7E | Fehler Schnellheizfeld Kissen  |
| 0x9F7F | Fehler Schnellheizfeld Lehne  |
| 0x9F80 | Fehler Restheizfeld Kissen  |
| 0x9F81 | Fehler Restheizfeld Lehne  |
| 0x9F82 | Fehler Heizungstreiber durchlegiert oder NTC defekt  |
| 0x9F83 | Fehler Klima Versorgung Kissen und Lehne  |
| 0x9F84 | Fehler Klima Steuerung Kissen  |
| 0x9F85 | Fehler Klima Steuerung Lehne  |
| 0x9F86 | Fehler Aktivsitz Motor  |
| 0x9F87 | Fehler Aktivsitz Magnet  |
| 0x9F88 | Fehler Aktivsitz Druckschalter  |
| 0x9F89 | Fehler Lordose Ventile  |
| 0x9F8A | Fehler Lordose Pumpe  |
| 0x9F8B | Interner Fehler Versorgungsspannung U12s oder U12h  |
| 0x9F8C | interner Fehler Versorgungsspannung Kl30s  |
| 0x9F8D | Interner Fehler EEPROM  |
| 0x9F8E | Energiesparmode aktiv  |
| 0x9F8F | Fehler Schalter SVS  |
| 0x9F90 | Fehler Schalter FEH  |
| 0x9F91 | Fehler Schalter LVK  |
| 0x9F92 | Fehler Schalter MFS-Schalter |
| 0x9F93 | Fehler UEKB Adaptionsbereichueberschreitung vor |
| 0x9F94 | Fehler UEKB Adaptionsbereichueberschreitung zurueck |
| 0x9F95 | Fehler UEKB EE-Bereich defekt |
| 0x9F96 | FehlerUEKB Stromerfassungsfehler |
| 0x9F97 | Fehler Normierung SLV |
| 0xE384 | K-CAN: Bus Leitungsfehler  |
| 0xE387 | Controller, Bus off  |
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
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | -- | -- | -- |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Aussentemperatur | Grad C | -- | unsigned char | -- | 1 | 2 | -40 |
| 0x02 | Batteriespannung | Volt | -- | unsigned char | -- | 25 | 255 | 0 |
| 0x03 | Motordrehzahl | 1/min | low | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 49 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9E9C | Fehler Motor SLV  |
| 0x9E9D | Fehler Motor SHV  |
| 0x9E9E | Fehler Motor LNV  |
| 0x9E9F | Fehler Motor SNV  |
| 0x9EA0 | Fehler Motor KHV  |
| 0x9EA1 | Fehler Motor FEH  |
| 0x9EA2 | Fehler Motor STV  |
| 0x9EA3 | Fehler Motor LBV  |
| 0x9EA4 | Fehler Motor LKV  |
| 0x9EA5 | Fehler Steuergerätetemperatur  |
| 0x9EA6 | Versorgungsspannungsfehler  |
| 0x9EA7 | Individualfahrzeug aktiv  |
| 0x9EFC | Fehler Motor SLV  |
| 0x9EFD | Fehler Motor SHV  |
| 0x9EFE | Fehler Motor LNV  |
| 0x9EFF | Fehler Motor SNV  |
| 0x9F00 | Fehler Motor KHV  |
| 0x9F01 | Fehler Motor FEH  |
| 0x9F02 | Fehler Motor STV  |
| 0x9F03 | Fehler Motor LBV  |
| 0x9F04 | Fehler Motor LKV  |
| 0x9F05 | Fehler Steuergerätetemperatur  |
| 0x9F06 | Versorgungsspannungsfehler  |
| 0x9F07 | Individualfahrzeug aktiv  |
| 0x9F5C | Fehler Motor SLV  |
| 0x9F5D | Fehler Motor SHV  |
| 0x9F5E | Fehler Motor LNV  |
| 0x9F5F | Fehler Motor SNV  |
| 0x9F60 | Fehler Motor KHV  |
| 0x9F61 | Fehler Motor FEH  |
| 0x9F62 | Fehler Motor STV  |
| 0x9F63 | Fehler Motor LBV  |
| 0x9F64 | Fehler Motor LKV  |
| 0x9F65 | Fehler Steuergerätetemperatur  |
| 0x9F66 | Versorgungsspannungsfehler  |
| 0x9F67 | Individualfahrzeug aktiv  |
| 0x9FBC | Fehler Motor SLV  |
| 0x9FBD | Fehler Motor SHV  |
| 0x9FBE | Fehler Motor LNV  |
| 0x9FBF | Fehler Motor SNV  |
| 0x9FC0 | Fehler Motor KHV  |
| 0x9FC1 | Fehler Motor FEH  |
| 0x9FC2 | Fehler Motor STV  |
| 0x9FC3 | Fehler Motor LBV  |
| 0x9FC4 | Fehler Motor LKV  |
| 0x9FC5 | Fehler Steuergerätetemperatur  |
| 0x9FC6 | Versorgungsspannungsfehler  |
| 0x9FC7 | Individualfahrzeug aktiv  |
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
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | -- | -- | -- |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Aussentemperatur | Grad C | -- | unsigned char | -- | 1 | 2 | -40 |
| 0x02 | Batteriespannung | Volt | -- | unsigned char | -- | 25 | 255 | 0 |
| 0x03 | Motordrehzahl | 1/min | low | unsigned int | -- | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | unsigned char | -- | 1 | 1 | 0 |

<a id="table-ioctrl-arg"></a>
### IOCTRL_ARG

Dimensions: 63 rows × 2 columns

| ARG_TEXT | ARG_WERT |
| --- | --- |
| UNBETAETIGT | 0 |
| VOR | 1 |
| ZUR | 2 |
| HOCH | 1 |
| TIEF | 2 |
| BREIT | 1 |
| SCHMAL | 2 |
| HOME | 3 |
| ADAP_VOR | 4 |
| ADAP_ZUR | 5 |
| VOLL | 1 |
| LEER | 2 |
| AN | 1 |
| AUS | 0 |
| START | 1 |
| STOP | 0 |
| SLV | 0 |
| SHV | 1 |
| LNV | 2 |
| SNV | 3 |
| KHV | 4 |
| LKV | 5 |
| STV | 6 |
| LBV | 7 |
| FEH | 8 |
| AKTSIT | 8 |
| KI_SCHNELLH | 0 |
| KI_RESTH | 1 |
| LE_SCHNELLH | 2 |
| LE_RESTH | 3 |
| U12S | 0 |
| Kl30S | 1 |
| Kl30V | 2 |
| UCP | 4 |
| UNTC | 5 |
| KISSEN_LEHNE | 4 |
| STUFE0 | 0 |
| STUFE1 | 1 |
| STUFE2 | 2 |
| STUFE3 | 3 |
| STUFE255 | 255 |
| KI | 1 |
| LE | 2 |
| DR_NIEDRIG | 1 |
| DR_HOCH | 0 |
| VENTIL1 | 0 |
| VENTIL2 | 1 |
| VENTIL3 | 2 |
| VENTIL4 | 3 |
| PUMPE | 4 |
| MAGNET | 0 |
| RECHTS | 1 |
| ZYKLUS | 2 |
| SCHALTER | 3 |
| AD_SENSE | 4 |
| AD_MAGNET | 5 |
| NOCKENMOTOR | 6 |
| SLEEP | 0 |
| WAKEUP | 1 |
| MEM | 0 |
| M1 | 1 |
| M2 | 2 |
| BUS | 2 |

<a id="table-ioctrl-lp-temp-pl1"></a>
### IOCTRL_LP_TEMP_PL1

Dimensions: 255 rows × 2 columns

| DIGIT_TXT | GRAD_WERT |
| --- | --- |
| 1 | 350.3 |
| 2 | 282.3 |
| 3 | 248.8 |
| 4 | 227.3 |
| 5 | 211.8 |
| 6 | 199.7 |
| 7 | 190.0 |
| 8 | 181.8 |
| 9 | 174.8 |
| 10 | 168.7 |
| 11 | 163.3 |
| 12 | 158.4 |
| 13 | 154.0 |
| 14 | 150.1 |
| 15 | 146.4 |
| 16 | 143.0 |
| 17 | 139.8 |
| 18 | 136.9 |
| 19 | 134.2 |
| 20 | 131.6 |
| 21 | 129.1 |
| 22 | 126.8 |
| 23 | 124.6 |
| 24 | 122.5 |
| 25 | 120.5 |
| 26 | 118.6 |
| 27 | 116.8 |
| 28 | 115.1 |
| 29 | 113.4 |
| 30 | 111.8 |
| 31 | 110.2 |
| 32 | 108.7 |
| 33 | 107.2 |
| 34 | 105.8 |
| 35 | 104.5 |
| 36 | 103.2 |
| 37 | 101.9 |
| 38 | 100.6 |
| 39 | 99.4 |
| 40 | 98.2 |
| 41 | 97.1 |
| 42 | 96.0 |
| 43 | 94.9 |
| 44 | 93.8 |
| 45 | 92.8 |
| 46 | 91.8 |
| 47 | 90.8 |
| 48 | 89.8 |
| 49 | 88.8 |
| 50 | 87.9 |
| 51 | 87.0 |
| 52 | 86.1 |
| 53 | 85.2 |
| 54 | 84.4 |
| 55 | 83.5 |
| 56 | 82.7 |
| 57 | 81.9 |
| 58 | 81.0 |
| 59 | 80.3 |
| 60 | 79.5 |
| 61 | 78.7 |
| 62 | 77.9 |
| 63 | 77.2 |
| 64 | 76.5 |
| 65 | 75.7 |
| 66 | 75.0 |
| 67 | 74.3 |
| 68 | 73.6 |
| 69 | 72.9 |
| 70 | 72.3 |
| 71 | 71.6 |
| 72 | 70.9 |
| 73 | 70.3 |
| 74 | 69.6 |
| 75 | 69.0 |
| 76 | 68.4 |
| 77 | 67.7 |
| 78 | 67.1 |
| 79 | 66.5 |
| 80 | 65.9 |
| 81 | 65.3 |
| 82 | 64.7 |
| 83 | 64.1 |
| 84 | 63.5 |
| 85 | 63.0 |
| 86 | 62.4 |
| 87 | 61.8 |
| 88 | 61.3 |
| 89 | 60.7 |
| 90 | 60.1 |
| 91 | 59.6 |
| 92 | 59.0 |
| 93 | 58.5 |
| 94 | 58.0 |
| 95 | 57.4 |
| 96 | 56.9 |
| 97 | 56.4 |
| 98 | 55.9 |
| 99 | 55.3 |
| 100 | 54.8 |
| 101 | 54.3 |
| 102 | 53.8 |
| 103 | 53.3 |
| 104 | 52.8 |
| 105 | 52.3 |
| 106 | 51.8 |
| 107 | 51.3 |
| 108 | 50.8 |
| 109 | 50.3 |
| 110 | 49.8 |
| 111 | 49.3 |
| 112 | 48.9 |
| 113 | 48.4 |
| 114 | 47.9 |
| 115 | 47.4 |
| 116 | 46.9 |
| 117 | 46.5 |
| 118 | 46.0 |
| 119 | 45.5 |
| 120 | 45.1 |
| 121 | 44.6 |
| 122 | 44.1 |
| 123 | 43.7 |
| 124 | 43.2 |
| 125 | 42.7 |
| 126 | 42.3 |
| 127 | 41.8 |
| 128 | 41.3 |
| 129 | 40.9 |
| 130 | 40.4 |
| 131 | 40.0 |
| 132 | 39.5 |
| 133 | 39.1 |
| 134 | 38.6 |
| 135 | 38.2 |
| 136 | 37.7 |
| 137 | 37.2 |
| 138 | 36.8 |
| 139 | 36.3 |
| 140 | 35.9 |
| 141 | 35.4 |
| 142 | 35.0 |
| 143 | 34.5 |
| 144 | 34.1 |
| 145 | 33.6 |
| 146 | 33.2 |
| 147 | 32.7 |
| 148 | 32.3 |
| 149 | 31.8 |
| 150 | 31.4 |
| 151 | 30.9 |
| 152 | 30.5 |
| 153 | 30.0 |
| 154 | 29.6 |
| 155 | 29.1 |
| 156 | 28.6 |
| 157 | 28.2 |
| 158 | 27.7 |
| 159 | 27.3 |
| 160 | 26.8 |
| 161 | 26.3 |
| 162 | 25.9 |
| 163 | 25.4 |
| 164 | 24.9 |
| 165 | 24.5 |
| 166 | 24.0 |
| 167 | 23.5 |
| 168 | 23.1 |
| 169 | 22.6 |
| 170 | 22.1 |
| 171 | 21.6 |
| 172 | 21.1 |
| 173 | 20.7 |
| 174 | 20.2 |
| 175 | 19.7 |
| 176 | 19.2 |
| 177 | 18.7 |
| 178 | 18.2 |
| 179 | 17.7 |
| 180 | 17.2 |
| 181 | 16.7 |
| 182 | 16.2 |
| 183 | 15.7 |
| 184 | 15.1 |
| 185 | 14.6 |
| 186 | 14.1 |
| 187 | 13.6 |
| 188 | 13.0 |
| 189 | 12.5 |
| 190 | 11.9 |
| 191 | 11.4 |
| 192 | 10.8 |
| 193 | 10.3 |
| 194 | 9.7 |
| 195 | 9.1 |
| 196 | 8.6 |
| 197 | 8.0 |
| 198 | 7.4 |
| 199 | 6.8 |
| 200 | 6.2 |
| 201 | 5.5 |
| 202 | 4.9 |
| 203 | 4.3 |
| 204 | 3.6 |
| 205 | 3.0 |
| 206 | 2.3 |
| 207 | 1.6 |
| 208 | 0.9 |
| 209 | 0.2 |
| 210 | -0.5 |
| 211 | -1.2 |
| 212 | -2.0 |
| 213 | -2.7 |
| 214 | -3.5 |
| 215 | -4.3 |
| 216 | -5.1 |
| 217 | -6.0 |
| 218 | -6.8 |
| 219 | -7.7 |
| 220 | -8.6 |
| 221 | -9.6 |
| 222 | -10.5 |
| 223 | -11.5 |
| 224 | -12.6 |
| 225 | -13.7 |
| 226 | -14.8 |
| 227 | -16.0 |
| 228 | -17.2 |
| 229 | -18.5 |
| 230 | -19.9 |
| 231 | -21.3 |
| 232 | -22.9 |
| 233 | -24.6 |
| 234 | -26.3 |
| 235 | -28.3 |
| 236 | -30.5 |
| 237 | -32.9 |
| 238 | -35.6 |
| 239 | -38.8 |
| 240 | -42.6 |
| 241 | -47.5 |
| 242 | -54.5 |
| 243 | -67.6 |
| 244 | -76.5 |
| 245 | -63.4 |
| 246 | -57.0 |
| 247 | -52.6 |
| 248 | -49.3 |
| 249 | -46.5 |
| 250 | -44.2 |
| 251 | -42.2 |
| 252 | -40.5 |
| 253 | -38.9 |
| 254 | -37.5 |
| 255 | -36.2 |

<a id="table-ioctrl-lp-temp-pl2"></a>
### IOCTRL_LP_TEMP_PL2

Dimensions: 256 rows × 2 columns

| DIGIT_TXT | GRAD_WERT |
| --- | --- |
| 0 | -29.9 |
| 1 | -25.8 |
| 2 | -22.4 |
| 3 | -19.4 |
| 4 | -16.8 |
| 5 | -14.4 |
| 6 | -12.3 |
| 7 | -10.3 |
| 8 | -8.5 |
| 9 | -6.8 |
| 10 | -5.2 |
| 11 | -3.6 |
| 12 | -2.2 |
| 13 | -0.8 |
| 14 | 0.5 |
| 15 | 1.8 |
| 16 | 3.0 |
| 17 | 4.1 |
| 18 | 5.2 |
| 19 | 6.3 |
| 20 | 7.4 |
| 21 | 8.4 |
| 22 | 9.4 |
| 23 | 10.4 |
| 24 | 11.3 |
| 25 | 12.2 |
| 26 | 13.1 |
| 27 | 14.0 |
| 28 | 14.8 |
| 29 | 15.7 |
| 30 | 16.5 |
| 31 | 17.3 |
| 32 | 18.1 |
| 33 | 18.8 |
| 34 | 19.6 |
| 35 | 20.4 |
| 36 | 21.1 |
| 37 | 21.8 |
| 38 | 22.5 |
| 39 | 23.2 |
| 40 | 23.9 |
| 41 | 24.6 |
| 42 | 25.3 |
| 43 | 26.0 |
| 44 | 26.6 |
| 45 | 27.3 |
| 46 | 27.9 |
| 47 | 28.5 |
| 48 | 29.2 |
| 49 | 29.8 |
| 50 | 30.4 |
| 51 | 31.0 |
| 52 | 31.6 |
| 53 | 32.2 |
| 54 | 32.8 |
| 55 | 33.4 |
| 56 | 34.0 |
| 57 | 34.6 |
| 58 | 35.2 |
| 59 | 35.7 |
| 60 | 36.3 |
| 61 | 36.9 |
| 62 | 37.4 |
| 63 | 38.0 |
| 64 | 38.5 |
| 65 | 39.1 |
| 66 | 39.6 |
| 67 | 40.2 |
| 68 | 40.7 |
| 69 | 41.3 |
| 70 | 41.8 |
| 71 | 42.3 |
| 72 | 42.9 |
| 73 | 43.4 |
| 74 | 43.9 |
| 75 | 44.5 |
| 76 | 45.0 |
| 77 | 45.5 |
| 78 | 46.0 |
| 79 | 46.5 |
| 80 | 47.1 |
| 81 | 47.6 |
| 82 | 48.1 |
| 83 | 48.6 |
| 84 | 49.1 |
| 85 | 49.6 |
| 86 | 50.1 |
| 87 | 50.6 |
| 88 | 51.1 |
| 89 | 51.6 |
| 90 | 52.1 |
| 91 | 52.7 |
| 92 | 53.2 |
| 93 | 53.7 |
| 94 | 54.2 |
| 95 | 54.7 |
| 96 | 55.2 |
| 97 | 55.7 |
| 98 | 56.2 |
| 99 | 56.7 |
| 100 | 57.2 |
| 101 | 57.7 |
| 102 | 58.2 |
| 103 | 58.7 |
| 104 | 59.2 |
| 105 | 59.7 |
| 106 | 60.2 |
| 107 | 60.7 |
| 108 | 61.2 |
| 109 | 61.7 |
| 110 | 62.2 |
| 111 | 62.7 |
| 112 | 63.2 |
| 113 | 63.7 |
| 114 | 64.2 |
| 115 | 64.7 |
| 116 | 65.2 |
| 117 | 65.7 |
| 118 | 66.2 |
| 119 | 66.8 |
| 120 | 67.3 |
| 121 | 67.8 |
| 122 | 68.3 |
| 123 | 68.8 |
| 124 | 69.3 |
| 125 | 69.9 |
| 126 | 70.4 |
| 127 | 70.9 |
| 128 | 71.4 |
| 129 | 72.0 |
| 130 | 72.5 |
| 131 | 73.0 |
| 132 | 73.5 |
| 133 | 74.1 |
| 134 | 74.6 |
| 135 | 75.2 |
| 136 | 75.7 |
| 137 | 76.2 |
| 138 | 76.8 |
| 139 | 77.3 |
| 140 | 77.9 |
| 141 | 78.5 |
| 142 | 79.0 |
| 143 | 79.6 |
| 144 | 80.1 |
| 145 | 80.7 |
| 146 | 81.3 |
| 147 | 81.9 |
| 148 | 82.4 |
| 149 | 83.0 |
| 150 | 83.6 |
| 151 | 84.2 |
| 152 | 84.8 |
| 153 | 85.4 |
| 154 | 86.0 |
| 155 | 86.6 |
| 156 | 87.2 |
| 157 | 87.8 |
| 158 | 88.4 |
| 159 | 89.1 |
| 160 | 89.7 |
| 161 | 90.3 |
| 162 | 91.0 |
| 163 | 91.6 |
| 164 | 92.3 |
| 165 | 92.9 |
| 166 | 93.6 |
| 167 | 94.2 |
| 168 | 94.9 |
| 169 | 95.6 |
| 170 | 96.3 |
| 171 | 97.0 |
| 172 | 97.7 |
| 173 | 98.4 |
| 174 | 99.1 |
| 175 | 99.9 |
| 176 | 100.6 |
| 177 | 101.3 |
| 178 | 102.1 |
| 179 | 102.9 |
| 180 | 103.6 |
| 181 | 104.4 |
| 182 | 105.2 |
| 183 | 106.0 |
| 184 | 106.8 |
| 185 | 107.6 |
| 186 | 108.5 |
| 187 | 109.3 |
| 188 | 110.2 |
| 189 | 111.0 |
| 190 | 111.9 |
| 191 | 112.8 |
| 192 | 113.7 |
| 193 | 114.7 |
| 194 | 115.6 |
| 195 | 116.6 |
| 196 | 117.6 |
| 197 | 118.6 |
| 198 | 119.6 |
| 199 | 120.6 |
| 200 | 121.7 |
| 201 | 122.7 |
| 202 | 123.8 |
| 203 | 124.9 |
| 204 | 126.1 |
| 205 | 127.3 |
| 206 | 128.4 |
| 207 | 129.7 |
| 208 | 130.9 |
| 209 | 132.2 |
| 210 | 133.5 |
| 211 | 134.9 |
| 212 | 136.2 |
| 213 | 137.7 |
| 214 | 139.1 |
| 215 | 140.6 |
| 216 | 142.2 |
| 217 | 143.8 |
| 218 | 145.4 |
| 219 | 147.1 |
| 220 | 148.9 |
| 221 | 150.7 |
| 222 | 152.6 |
| 223 | 154.6 |
| 224 | 156.6 |
| 225 | 158.8 |
| 226 | 161.0 |
| 227 | 163.3 |
| 228 | 165.8 |
| 229 | 168.3 |
| 230 | 171.0 |
| 231 | 173.8 |
| 232 | 176.8 |
| 233 | 180.0 |
| 234 | 183.4 |
| 235 | 187.0 |
| 236 | 190.9 |
| 237 | 195.1 |
| 238 | 199.6 |
| 239 | 204.6 |
| 240 | 210.0 |
| 241 | 216.1 |
| 242 | 222.8 |
| 243 | 230.4 |
| 244 | 239.1 |
| 245 | 249.4 |
| 246 | 261.6 |
| 247 | 276.7 |
| 248 | 296.1 |
| 249 | 322.9 |
| 250 | 364.3 |
| 251 | 445.5 |
| 252 | 932.9 |
| 253 | naN |
| 254 | naN |
| 255 | naN |

<a id="table-ioctrl-normierung"></a>
### IOCTRL_NORMIERUNG

Dimensions: 9 rows × 2 columns

| VALUE | NAME |
| --- | --- |
| 0 | INIT_CRC_KO |
| 1 | PLAUSICHECK |
| 2 | HALL_UNGUELTIG |
| 3 | POSITIONSVERLUST |
| 4 | HALL_DEFEKT |
| 5 | HALL_RESET |
| 6 | NORMIERLAUF |
| 7 | ANZ_VSTCNT_STUFE3 |
| 8 | NORMBL_UEBERFAHREN |
