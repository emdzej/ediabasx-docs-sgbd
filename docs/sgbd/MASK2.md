# MASK2.prg

- Jobs: [103](#jobs)
- Tables: [50](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MASK2 MMI / Tuner / ASK  |
| ORIGIN | BMW EI-44 Toedtmann |
| REVISION | 1.001 |
| AUTHOR | HaysAG EI-44 Hr.Bubb |
| COMMENT | N/A |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
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
- [LESEN_INDIVIDUALDATA_LISTE](#job-lesen-individualdata-liste) - Lesen eines Listeneintrags der Individualisierungsdaten KWP2000: $21 ReadDataByLocalIdentifier $01 recordLocalIdentifier
- [LESE_INDIVIDUALDATA](#job-lese-individualdata) - Lesen von Individualisierungsdaten KWP2000: $21 ReadDataByLocalIdentifier $02 recordLocalIdentifier Modus   : Default
- [SCHREIBEN_INDIVIDUALDATA](#job-schreiben-individualdata) - Schreiben von Individualisierungsdaten KWP2000: $3B WriteDataByLocalIdentifier $02 recordLocalIdentifier Modus   : Default
- [LESEN_ADRESSBUCH](#job-lesen-adressbuch) - Lesen eines Datensatzes des NAVI-Adressbuchs KWP2000: $21 ReadDataByLocalIdentifier $06 recordLocalIdentifier
- [SCHREIBEN_ADRESSBUCH](#job-schreiben-adressbuch) - Schreiben eines Datensatzes des NAVI-Adressbuchs KWP2000: $3B writeDataByLocalIdentifier $06 recordLocalIdentifier Die persistente Abspeicherung erfolgt erst nach einem Reset
- [LESEN_TELEFONNUMMERN](#job-lesen-telefonnummern) - Auslesen der im CHAMP gespeicherten Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline KWP2000: $21 readDataByLocalIdentifier $A2 recordLocalIdentifier Modus  : Default
- [SCHREIBEN_TELEFONNUMMERN](#job-schreiben-telefonnummern) - Schreiben der Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline KWP2000: $3B writeDataByLocalIdentifier $A2 recordLocalIdentifier Modus  : Default
- [LESEN_TELEFONNUMMER_SDARS](#job-lesen-telefonnummer-sdars) - Auslesen der im MASK gespeicherten Telefonnummer für - SDARS KWP2000: $21 readDataByLocalIdentifier $A3 recordLocalIdentifier Modus  : Default
- [SCHREIBEN_TELEFONNUMMER_SDARS](#job-schreiben-telefonnummer-sdars) - Schreiben der Telefonnummer für SDARS KWP2000: $3B writeDataByLocalIdentifier $A3 recordLocalIdentifier Modus  : Default
- [SER_NR_DOM_LESEN](#job-ser-nr-dom-lesen) - Seriennummer 14-stellig lesen Neu für Entertainment-Komponenten ab 2003 KWP2000: $21 ReadDatabyLocalIdentifier $E0 Local ID SER_NR_DOM Modus  : Default
- [LESEN_NAVDVDPIN](#job-lesen-navdvdpin) - Lesen des 4 stelligen PIN-Codes zum Entsperren der NAVI-DVD KWP2000: $21 ReadDataByLocalIdentifier $03 recordLocalIdentifier Modus  : Default
- [SCHREIBEN_NAVDVDPIN](#job-schreiben-navdvdpin) - Schreiben des 4 stelligen PIN-Codes zum Entsperren der NAVI-DVD KWP2000: $3B ReadDataByLocalIdentifier $03 recordLocalIdentifier Modus  : Default
- [STATUS_AKTIVE_GAL_KURVE](#job-status-aktive-gal-kurve) - Reads the active coded speed dependent volume control curve  KWP2000: $21 ReadDataByLocalIdentifier $B9 RecordLocalIdentifier
- [STATUS_ANT_DC](#job-status-ant-dc) - Auslesen ob Ri der Diversity im Toleranzband liegt KWP2000: $30 InputOutputControlByLocalIdentifier $15 inputOutputLocalIdentifier  - get Antenna DC State $01 inputOutputControlParameter - reportCurrentState Modus  : Default
- [STATUS_ANT_EIGEN_DIAG](#job-status-ant-eigen-diag) - Lesen Status Antennendiagnose KWP2000: $30 InputOutputControlByLocalIdentifier $17 inputOutputLocalIdentifier  - get Antenna Diagnosis State $01 inputOutputControlParameter - reportCurrentState Modus  : Default
- [STATUS_ANT_QFS](#job-status-ant-qfs) - Auslesen des Status Quality Fieldstrength KWP2000: $30 InputOutputControlByLocalIdentifier $12 inputOutputLocalIdentifier  - status QFS $01 inputOutputControlParameter - reportCurrentState Modus  : Default
- [STATUS_CPU_AUSLASTUNG](#job-status-cpu-auslastung) - Lesen der CPU Auslastung in % KWP2000: $21 ReadDataByLocalIdentifier $BB Modus  : Default
- [STATUS_FLOTTENMODUS](#job-status-flottenmodus) - Abfrage des aktuell zu aktivierenden Flottenmodus. (Art der NAVI-DVD Sperrung.) KWP2000: $30 InputOutputControlByLocalIdentifier $1B inputOutputLocalIdentifier $01 inputOutputControlParameter - reportCurrentState Modus  : Default
- [STATUS_FREQUENZ](#job-status-frequenz) - aktuelle Tunerfrequenz abfragen KWP2000: $30 InputOutputControlByLocalIdentifier $0F inputOutputLocalIdentifier  - get frequency $01 inputOutputControlParameter - reportCurrentState Modus  : Default
- [STATUS_LESEN_CONNTABLE](#job-status-lesen-conntable) - Auslesen der aktuellen Connectiontable KWP2000: $21 ReadDataByLocalIdentifier $B4 recordLocalIdentifier Modus  : Default
- [STATUS_LESEN_CONNTABLE_DETAIL](#job-status-lesen-conntable-detail) - Genaue Information zur abgefragten Connection ausgeben KWP2000: $21 ReadDataByLocalIdentifier $B5 recordLocalIdentifier Modus  : Default
- [STATUS_LESEN_LAUFWERK](#job-status-lesen-laufwerk) - Auslesen des im MASK verbauten Laufwerkes KWP2000: $21 ReadDataByLocalIdentifier $B3 recordLocalIdentifier Modus  : Default
- [STATUS_LESEN_SYSTEM_AUDIO](#job-status-lesen-system-audio) - Auslesen des verbauten Audiosystemes KWP2000: $21 ReadDataByLocalIdentifier $B2 recordLocalIdentifier Modus  : Default
- [STATUS_RDS](#job-status-rds) - Lesen Status AF-Verfolgung und TP KWP2000: $30 InputOutputControlByLocalIdentifier $0C inputOutputLocalIdentifier  - get RDS $01 inputOutputControlParameter - reportCurrentState Modus  : Default
- [STATUS_TUNER_CODIERUNG](#job-status-tuner-codierung) - Auslesen der Tuner Codierdaten KWP2000: $21 ReadDataByLocalIdentifier $B7 recordLocalIdentifier Modus  : Default
- [STEUERN_ANT_EIGEN_DIAG](#job-steuern-ant-eigen-diag) - Antennen-Eigendiagnose starten KWP2000: $30 InputOutputControlByLocalIdentifier $16 inputOutputLocalIdentifier $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_ANT_SCAN](#job-steuern-ant-scan) - FM-Antennen weiterschalten KWP2000: $30 InputOutputControlByLocalIdentifier $11 inputOutputLocalIdentifier  - Antenna scan $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_AUDIOKANAELE](#job-steuern-audiokanaele) - Ansteuern eines AudioKanals KWP2000: $30 InputOutputControlByLocalIdentifier $01 inputOutputLocalIdentifier  - audio channel $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_CLEAR_CKMDATA](#job-steuern-clear-ckmdata) - Löschen der CKM Daten für Schlüssel X KWP2000: $30 InputOutputControlByLocalIdentifier $18 inputOutputLocalIdentifier  - clear CKM for Key X $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_COPY_CKMDATA](#job-steuern-copy-ckmdata) - Kopieren der CKM Daten von Schlüssel X nach Schlüssel Y KWP2000: $30 InputOutputControlByLocalIdentifier $19 inputOutputLocalIdentifier  - copy CKM from Key X to Key Y $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_EJECT](#job-steuern-eject) - Simulation Tastendruck EJECT-Taste KWP2000: $30 InputOutputControlByLocalIdentifier $0B inputOutputLocalIdentifier  - eject $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_FLOTTENMODUS](#job-steuern-flottenmodus) - Steuern des aktuell zu aktivierenden Flottenmodus. (Art der NAVI-DVD Sperrung.) KWP2000: $30 InputOutputControlByLocalIdentifier $1B inputOutputLocalIdentifier $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_FREQUENZ](#job-steuern-frequenz) - Tunerfrequenz einstellen KWP2000: $30 InputOutputControlByLocalIdentifier $10 inputOutputLocalIdentifier  - set frequency $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_KLANGZEICHEN](#job-steuern-klangzeichen) - Ausloesen eines Klangzeichens KWP2000: $30 InputOutputControlByLocalIdentifier $02 inputOutputLocalIdentifier  - accoustic sign $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_LINEAR](#job-steuern-linear) - Alle Toneinstellungen auf Defaultwerte setzten KWP2000: $30 InputOutputControlByLocalIdentifier $05 inputOutputLocalIdentifier  - device sound linear $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_NEXT_ENTSOURCE](#job-steuern-next-entsource) - Weiterschaltung der Entertainment-Quelle per Diagnose KWP2000: $30 InputOutputControlByLocalIdentifier $1C inputOutputLocalIdentifier $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_RADIO_SCHALTEN](#job-steuern-radio-schalten) - Simulation Tastendruck ENTERTAINMENT-Taste KWP2000: $30 InputOutputControlByLocalIdentifier $0A inputOutputLocalIdentifier  - switch radio on or off $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_RDS](#job-steuern-rds) - Steuern AF-Verfolgung und TP KWP2000: $30 InputOutputControlByLocalIdentifier $14 inputOutputLocalIdentifier  - set RDS $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Ansteuerung des Selbsttests im MASK - Speichertests FLASH_ROM, RAM, Video-RAM, EEPROM Bei Erkennung eines Fehlverhaltens erfolgt ein Eintrag im Primaer- und Shadowfehlerspeicher. KWP2000: $31 startRoutineByLocalIdentifier $04 routineLocalIdentifier (selfTest) Modus  : Default
- [STEUERN_SINUSGENERATOR_AUS](#job-steuern-sinusgenerator-aus) - Ausschalten des Sinusgenerators  KWP2000: $32 StopRoutineByLocalIdentifier $B8 routineLocalIdentifier
- [STEUERN_TESTBILD](#job-steuern-testbild) - Ausgabe eines Testbildes KWP2000: $31 startRoutineByLocalIdentifier $A0 routineLocalIdentifier $XX Musterlänge $XX Farbe1 $XX Farbe2 Modus  : Default
- [STEUERN_TUNER_SUCHLAUF](#job-steuern-tuner-suchlauf) - Sendersuchlauf des AM/FM-Tuner starten KWP2000: $30 InputOutputControlByLocalIdentifier $13 inputOutputLocalIdentifier  - Tuner_Suchlauf $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STEUERN_VOLUMEAUDIO](#job-steuern-volumeaudio) - Einstellen der Audio-Lautstaerke KWP2000: $30 InputOutputControlByLocalIdentifier $03 inputOutputLocalIdentifier  - set volume $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [LLDATENRETTUNG](#job-lldatenrettung) - LowLevel MOST Datenrettungsschnittstelle KWP2000: $21 ReadDataByLocalIdentifier $02 LocalIdentifier Modus  : Default
- [STATUS_LAST_CONNECTION](#job-status-last-connection) - URL der letzen Verbindung wird ausgegeben KWP2000: $21 ReadDataByLocalIdentifier KWP2000: $17 LocalIdentifier Modus  : Default
- [STEUERN_SINUSGENERATOR_EIN](#job-steuern-sinusgenerator-ein) - Aktivieren des Sinusgenerators und Ausgabe auf allen ausgewählten Lautsprechern SELECT_SPEAKER X  KWP2000: $31 StartRoutineByLocalIdentifier $B8 routineLocalIdentifier $xx Lautsprecherkanal Byte high $xx Lautsprecherkanal Byte low - $0001   Kanal links vorne - $0002   Kanal rechts vorne - (nur via AMP_60 -SGBD-&gt; $0004   Kanal Center) - (nur via AMP_60 -SGBD-&gt; $0008   Kanal Surround links) - (nur via AMP_60 -SGBD-&gt; $0010   Kanal Surround rechts) - $0020   Kanal links hinten - $0040   Kanal rechts hinten - $0080   Kanal Subwoofer links - $0100   Kanal Subwoofer rechts $xx Frequenz Byte high $xx Frequenz Byte low $xx Level
- [LESEN_DAR](#job-lesen-dar) - Lesen eines DAR Datensatzes KWP2000: $31 StartRoutineByLocalId	$23 $33 RequestRoutineResults	$23 $21 ReadDataByLocalIdentifier	$1A
- [SCHREIBEN_DAR](#job-schreiben-dar) - Schreiben eines DAR Datensatzes KWP2000: $31 StartRoutineByLocalId	$25,$26 $33 RequestRoutineResults	$26 $3B WriteDataByLocalIdentifier	$A4
- [LESEN_ONLINE_LOGGING](#job-lesen-online-logging) - Lesen einer Zeile Onlinelogging KWP2000: $31 StartRoutineByLocalId	$27 $33 RequestRoutineResults	$27 $21 ReadDataByLocalIdentifier	$1C
- [LESEN_BROWSER_HISTORY](#job-lesen-browser-history) - Lesen einer Zeile der Browser History KWP2000: $31 StartRoutineByLocalId	$29 $33 RequestRoutineResults	$29 $21 ReadDataByLocalIdentifier	$1E
- [LESEN_BROWSER_ERRORS](#job-lesen-browser-errors) - Lesen einer Zeile des Browsererrorlogs KWP2000: $31 StartRoutineByLocalId	$28 $33 RequestRoutineResults	$28 $21 ReadDataByLocalIdentifier	$1D
- [LESEN_ACCESS_RECORDS](#job-lesen-access-records) - Lesen eines AR Datensatzes KWP2000: $31 StartRoutineByLocalId	$24 $33 RequestRoutineResults  $24 $21 ReadDataByLocalIdentifier  $1B
- [STATUS_DAR_INDEX](#job-status-dar-index) - Reading of the actually coded DAR-Index KWP2000: $21 ReadDataByLocalID $18 localID Modus  : Default
- [STATUS_BROWSER_APPL](#job-status-browser-appl) - Check if application coded and check POPUP KWP2000: $21 ReadDataByLocalID $19 localID Modus  : Default

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

<a id="job-lesen-individualdata-liste"></a>
### LESEN_INDIVIDUALDATA_LISTE

Lesen eines Listeneintrags der Individualisierungsdaten KWP2000: $21 ReadDataByLocalIdentifier $01 recordLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LISTENTRY | unsigned int | Nummer des angeforderten Listenelements (0,1,2,...) 0x0000 = Anforderung, das 1. Listelement zu senden 0x0001 = Anforderung, das 2. Listelement zu senden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_ENTRYNR | unsigned int | Nummer des zurückgegebenen Listenelements (0,1,2,...) |
| RET_STATUS | unsigned char | Information ob aktuelles Listenelement das Letzte ist 0xFF	letztes Listenelement 0xFE	Listenelement nicht gefunden 0x00 	nicht letztes Listenelement |
| RET_FROMWHERE | unsigned char | Individualdaten müssen via CAN oder MOST oder XY angesprochen werden. 0x00	via CAN 0x01	via MOST 0x02  via CAN-PIADiensteanfrage 0x03  via Naviadressbuchanfrage ...	via XY... |
| RET_DATA | binary | Listentry zur Individualdaten-Abfrage 1.Byte, Diagnoseadresse (for future use), diese gibt Auskunft von welchem SG die Individualdaten verwaltet werden. z.B. 0x63  2.Byte:	Sind die Daten Car- oder Key- Memory relevant? 0x01	CarMemory relevant 0x02	KeyMemory relevant 0x03	CarMemory relevant und KeyMemory relevant  3.Byte:	Individualdaten können via CAN oder MOST oder XY erreicht werden. 0x00	via CAN 0x01	via MOST 0x02  via CAN-PIADiensteanfrage 0x03  via Naviadressbuchanfrage ...	via XY...  4.Byte und Folgende siehe Spec Datenrettung  |
| RET_COMMENT | string | Kommentarspalte des Entries |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-lese-individualdata"></a>
### LESE_INDIVIDUALDATA

Lesen von Individualisierungsdaten KWP2000: $21 ReadDataByLocalIdentifier $02 recordLocalIdentifier Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KEYID | unsigned char | 0x00       CarMemory 0x01..0x04 Schlüsselnummer dem der RET_DATA zugeordnet ist 0xFF	   Aktuell gesteckter Schlüssel ist RET_DATA zugeordnet |
| ARG_BLOCKNR | unsigned long | Zu übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 (4 Bytes) falls nicht verwendet als Dummy mitschleifen |
| ARG_FROMWHERE | unsigned char | Individualdaten können via CAN oder MOST oder XY erreicht werden 0x00	via CAN 0x01	via MOST 0x02    via CAN-PIADiensteanfrage 0x03    via Naviadressbuchanfrage ...	via XY... |
| ARG_INQY_LEN | unsigned char | Länge des folgenden Anfragedatenstreams z.B. 0x02 für 2 Byte |
| ARG_INQY_DATA | string | ASCII-codiert Anfrage Individualdatenstream z.B via MOST 2000022201 für MOST AudioMaster_MASK.AMBass.Get Format: FBlock    1 Byte InstID    1 Byte FktID     2 Byte rechtsbündig OpType    1 Byte Parameter x Bytes |
| ARG_RESP_LEN | unsigned char | Länge der folgenden Information wie die Antwort erhalten wird. Also ein Antwortfilter bzw. -hinweis z.B. 0x04 für 4 Byte |
| ARG_RESP_DATA | string | ASCII-codiert Information wie die Antwort erhalten wird: Also ein Antwortfilter bzw. -hinweis z.B via MOST 71000400 für MOST Climate.ConfigIHKA Format: FBlock    1 Byte InstID    1 Byte FktID     2 Byte rechtsbündig Parameter x Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | 0xFF letztes oder einziges element des Datenstreams 0x00 es folgen weitere Datenstreamstücke 0x01 komplette Wiederholung erforderlich 0x02 ab letztem Block wiederholen 0x03 fehlgeschlagen, Daten nicht lesbar |
| RET_BLOCKNR | unsigned long | Übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 falls nicht verwendet als Dummy mitschleifen |
| RET_LEN | int | Länge des Individualisierungs Datenstream oder -streamstücks |
| RET_DATA | binary | Individualisierungs Datenstream |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-individualdata"></a>
### SCHREIBEN_INDIVIDUALDATA

Schreiben von Individualisierungsdaten KWP2000: $3B WriteDataByLocalIdentifier $02 recordLocalIdentifier Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KEYID | unsigned char | 0x00       CarMemory 0x01..0x04 Schlüsselnummer dem der ARG_DATA zugeordnet ist 0xFF	   Aktuell gesteckter Schlüssel ist ARG_DATA zugeordnet |
| ARG_BLOCKNR | unsigned long | Zu übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 (4 Bytes) falls nicht verwendet als Dummy mitschleifen |
| ARG_FROMWHERE | unsigned char | Individualdaten können via CAN oder MOST oder XY geschrieben werden 0x00	via CAN 0x01	via MOST 0x02    via CAN-PIADiensteanfrage 0x03    via Naviadressbuchanfrage ...	via XY |
| ARG_STATUS | unsigned char | 0xFF letztes oder einziges element des Datenstreams 0x00 es folgen weitere Datenstreamstücke |
| ARG_WRITE_LEN | unsigned char | Länge des folgenden Schreibauftrags z.B. 0x02 für 2 Byte |
| ARG_WRITE_DATA | string | ASCII-codiert Schreibauftrag für Individualdatenstream Format for MOST FBlock    1 Byte InstID    1 Byte FktID     2 Byte rechtsbündig OpType    1 Byte Parameter x Bytes |
| ARG_W_RESP_LEN | unsigned char | Optional, Laenge des folgenden Antwortfilters z.B. 0x02 für 2 Byte |
| ARG_W_RESP_DATA | string | ASCII-codiert, Optional, Antwortfilter des Schreibauftrags Format: FBlock    1 Byte InstID    1 Byte FktID     2 Byte rechtsbündig OpType    1 Byte Parameter x Bytes |
| ARG_LEN | int | Länge des Individualisierungs Datenstream oder -streamstücks |
| ARG_DATA | string | ASCII-codiert Datenstream |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Rückmeldungen, Fehlercodes z.B. OK 0x00 oder NOTOK 0x01 |
| RET_FORMAT | unsigned char | proprietäre Formatrückmeldung für ABUCH |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-adressbuch"></a>
### LESEN_ADRESSBUCH

Lesen eines Datensatzes des NAVI-Adressbuchs KWP2000: $21 ReadDataByLocalIdentifier $06 recordLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_FORMAT_OR_DATA | unsigned char | Format oder Datenanfrage 0x01	Formatanfrage 0x02	Datenanfrage |
| ARG_LISTE | unsigned char | Welche der verschiedenen Adressbuchlisten soll übertragen werden? |
| ARG_DEBUG | unsigned char | For Debug use |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_FORMAT | unsigned char | Nummer des Formats in dem das Adressbuch übertragen wird |
| RET_ISLAST | unsigned char | Information ob aktueller Datensatz der Letzte ist 0x00 	Es folgen noch Datensätze 0x01	Letzter Datensatz |
| RET_DATA | binary | Unicode-Datensatz mit Steuerzeichen maximal 1 kByte |
| RET_LENCTRL_DEBUG | unsigned char | LenCtrl for Debug use |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-adressbuch"></a>
### SCHREIBEN_ADRESSBUCH

Schreiben eines Datensatzes des NAVI-Adressbuchs KWP2000: $3B writeDataByLocalIdentifier $06 recordLocalIdentifier Die persistente Abspeicherung erfolgt erst nach einem Reset

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_PREPARE_OR_DATA | unsigned char | Vorbereitung oder Daten 0x01	Vorbereitung 0x02	Daten |
| ARG_LISTE | unsigned char | Welche der verschiedenen Adressbuchlisten soll übertragen werden? |
| ARG_ISLAST | unsigned char | Information ob aktueller Datensatz der Letzte ist 0x00 	Es folgen noch Datensätze 0x01	Letzter Datensatz |
| ARG_DATA | string | Unicode-Datensatz mit Steuerzeichen maximal 1 kByte Daten sind als Hex-Array abgelegt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_FORMAT | unsigned char | Nummer des Formats in dem das Adressbuch übertragen werden muss Als Reaktion auf PREPARE_OR_DATA = 0x01 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-telefonnummern"></a>
### LESEN_TELEFONNUMMERN

Auslesen der im CHAMP gespeicherten Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline KWP2000: $21 readDataByLocalIdentifier $A2 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| NR_BEREITSCHAFTSDIENST | string | Nummer des Bereitschaftsdienstes |
| NR_HEIMATHAENDLER | string | Nummer des Heimathändlers |
| NR_PASSO | string | Nummer Passo |
| NR_HOTLINE | string | Nummer der Hotline |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-telefonnummern"></a>
### SCHREIBEN_TELEFONNUMMERN

Schreiben der Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline KWP2000: $3B writeDataByLocalIdentifier $A2 recordLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NR_BEREITSCHAFTSDIENST | string | Nummer des Bereitschaftsdienstes Stringlänge max. 50 Zeichen + Stringende-Zeichen (\0) |
| NR_HEIMATHAENDLER | string | Nummer des Heimathändlers Stringlänge max. 50 Zeichen + Stringende-Zeichen (\0) |
| NR_PASSO | string | Nummer Passo Stringlänge max. 50 Zeichen + Stringende-Zeichen (\0) |
| NR_HOTLINE | string | Nummer der Hotline Stringlänge max. 50 Zeichen + Stringende-Zeichen (\0) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-telefonnummer-sdars"></a>
### LESEN_TELEFONNUMMER_SDARS

Auslesen der im MASK gespeicherten Telefonnummer für - SDARS KWP2000: $21 readDataByLocalIdentifier $A3 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| NR_SDARS | string | Nummer des Bereitschaftsdienstes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-telefonnummer-sdars"></a>
### SCHREIBEN_TELEFONNUMMER_SDARS

Schreiben der Telefonnummer für SDARS KWP2000: $3B writeDataByLocalIdentifier $A3 recordLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NR_SDARS | string | Nummer des Bereitschaftsdienstes Stringlänge max. 35 Zeichen (ohne Endezeichen \0) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ser-nr-dom-lesen"></a>
### SER_NR_DOM_LESEN

Seriennummer 14-stellig lesen Neu für Entertainment-Komponenten ab 2003 KWP2000: $21 ReadDatabyLocalIdentifier $E0 Local ID SER_NR_DOM Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SER_NR_DOM | string | Seriennummer Gerät 14-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-navdvdpin"></a>
### LESEN_NAVDVDPIN

Lesen des 4 stelligen PIN-Codes zum Entsperren der NAVI-DVD KWP2000: $21 ReadDataByLocalIdentifier $03 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_NAVDVDPIN | string | 4 stelliger PIN Code zum entsperren der NAVI-DVD |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-navdvdpin"></a>
### SCHREIBEN_NAVDVDPIN

Schreiben des 4 stelligen PIN-Codes zum Entsperren der NAVI-DVD KWP2000: $3B ReadDataByLocalIdentifier $03 recordLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_NAVDVDPIN | string | 4 stelliger PIN Code zum entsperren der NAVI-DVD |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktive-gal-kurve"></a>
### STATUS_AKTIVE_GAL_KURVE

Reads the active coded speed dependent volume control curve  KWP2000: $21 ReadDataByLocalIdentifier $B9 RecordLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GAL_KURVE | string | Active SDVC curve |
| STAT_GAL_KURVE_WERT | int | Numbert of active SDVC curve |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-dc"></a>
### STATUS_ANT_DC

Auslesen ob Ri der Diversity im Toleranzband liegt KWP2000: $30 InputOutputControlByLocalIdentifier $15 inputOutputLocalIdentifier  - get Antenna DC State $01 inputOutputControlParameter - reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANT_DC | string | Status Ri (Ok / not Ok) table TTunerRi NAME |
| STAT_ANT_DC_VALUE | int | Status Ri (Ok as 1/ not Ok as 0) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-eigen-diag"></a>
### STATUS_ANT_EIGEN_DIAG

Lesen Status Antennendiagnose KWP2000: $30 InputOutputControlByLocalIdentifier $17 inputOutputLocalIdentifier  - get Antenna Diagnosis State $01 inputOutputControlParameter - reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANT_EIGEN_DIAG | string | Status Antennendiagnose table TAntennaDiag VALUE |
| STAT_ANT_EIGEN_DIAG_TEXT | string | Status Antennendiagnose table TAntennaDiag NAME |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-qfs"></a>
### STATUS_ANT_QFS

Auslesen des Status Quality Fieldstrength KWP2000: $30 InputOutputControlByLocalIdentifier $12 inputOutputLocalIdentifier  - status QFS $01 inputOutputControlParameter - reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_QUALITY | int | Quality Bereich: 0..15 (der fuer die AF-Verfolgung massgebliche Wert, entspricht der Summe der gewichteten Einzelfaktoren, 15 = beste Qualitaet) 2-Tuner: Quality = 0 ! |
| STAT_FIELDSTRENGTH | int | Fieldstrength Bereich: 0..15 (4dB-Schritte von 0..60 dBµV) |
| STAT_FIELDSTRENGTH_EXACT | int | Fieldstrength Bereich: 0..60 and more (1dB-Schritte von 0..60 and more dBµV) -1 if not valid |
| STAT_FREQUENZ | string | Bereich: 150 - 108000 kHz |
| STAT_ANT_PW | int | Antenna Power Supply Bereich: 0 = OFF, 1..15 = ON |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cpu-auslastung"></a>
### STATUS_CPU_AUSLASTUNG

Lesen der CPU Auslastung in % KWP2000: $21 ReadDataByLocalIdentifier $BB Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CPU | int | CPU Auslastung in % |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-flottenmodus"></a>
### STATUS_FLOTTENMODUS

Abfrage des aktuell zu aktivierenden Flottenmodus. (Art der NAVI-DVD Sperrung.) KWP2000: $30 InputOutputControlByLocalIdentifier $1B inputOutputLocalIdentifier $01 inputOutputControlParameter - reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MODUS | unsigned char | Aktuell aktiver Flottenmodus 0x00	Keine NAVI-DVD Sperrung 0x01	NAVI-DVD ist mit PIN-Code gesperrt 0x02	NAVI-DVD ist immer gesperrt. |
| STAT_MODUS_TEXT | string | Aktuell aktiver Flottenmodus als Text (s.o.) Werte aus table TFlottenmodus |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-frequenz"></a>
### STATUS_FREQUENZ

aktuelle Tunerfrequenz abfragen KWP2000: $30 InputOutputControlByLocalIdentifier $0F inputOutputLocalIdentifier  - get frequency $01 inputOutputControlParameter - reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FREQ | string | Bereich: 150 - 108000 kHz |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-conntable"></a>
### STATUS_LESEN_CONNTABLE

Auslesen der aktuellen Connectiontable KWP2000: $21 ReadDataByLocalIdentifier $B4 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CONNTABLE | string | Laufwerksvariante |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-conntable-detail"></a>
### STATUS_LESEN_CONNTABLE_DETAIL

Genaue Information zur abgefragten Connection ausgeben KWP2000: $21 ReadDataByLocalIdentifier $B5 recordLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONNECTION | unsigned char | Nummer der gewaehlten Connection |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CONNTABLE_DETAIL | string | Genaue Information zur abgefragten Connection |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-laufwerk"></a>
### STATUS_LESEN_LAUFWERK

Auslesen des im MASK verbauten Laufwerkes KWP2000: $21 ReadDataByLocalIdentifier $B3 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LAUFWERK | string | Laufwerksvariante |
| STAT_LAUFWERK_WERT | int | Laufwerksvariante Wert |
| STAT_FIRMWARE | string | Firmwareversion |
| STAT_TYP | string | Laufwerkstyp |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-system-audio"></a>
### STATUS_LESEN_SYSTEM_AUDIO

Auslesen des verbauten Audiosystemes KWP2000: $21 ReadDataByLocalIdentifier $B2 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AUDIO_SYSTEM | string | table THWVariante NAME |
| STAT_AUDIO_SYSTEM_WERT | int | table THWVariante WERT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rds"></a>
### STATUS_RDS

Lesen Status AF-Verfolgung und TP KWP2000: $30 InputOutputControlByLocalIdentifier $0C inputOutputLocalIdentifier  - get RDS $01 inputOutputControlParameter - reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RDS | string | Status AF-Verfolgung und TP table TTunerRDS NAME |
| STAT_RDS_VALUE | int | Status AF-Verfolgung und TP |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tuner-codierung"></a>
### STATUS_TUNER_CODIERUNG

Auslesen der Tuner Codierdaten KWP2000: $21 ReadDataByLocalIdentifier $B7 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAENDERVARIANTE_TUNER | string |  |
| STAT_TP_FUNKTION | string |  |
| STAT_RDS_AF_FUNKTION | string |  |
| STAT_PTY_TABELLE | string |  |
| STAT_REGIONALISIERUNG | string |  |
| STAT_HIGH_CUT | string |  |
| STAT_SENDER_TAB | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-eigen-diag"></a>
### STEUERN_ANT_EIGEN_DIAG

Antennen-Eigendiagnose starten KWP2000: $30 InputOutputControlByLocalIdentifier $16 inputOutputLocalIdentifier $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-scan"></a>
### STEUERN_ANT_SCAN

FM-Antennen weiterschalten KWP2000: $30 InputOutputControlByLocalIdentifier $11 inputOutputLocalIdentifier  - Antenna scan $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANT_SCAN | int | 0 = auf AM Betrieb/Verstärker schalten 1 = auf nächste FM Antenne weiterschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-audiokanaele"></a>
### STEUERN_AUDIOKANAELE

Ansteuern eines AudioKanals KWP2000: $30 InputOutputControlByLocalIdentifier $01 inputOutputLocalIdentifier  - audio channel $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUDIOKANAL | string | NF Ausgabe nur auf dem gewaehlten Kanal  table TAudioKanal NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| KANAL | string | angesteuerter Kanal |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-clear-ckmdata"></a>
### STEUERN_CLEAR_CKMDATA

Löschen der CKM Daten für Schlüssel X KWP2000: $30 InputOutputControlByLocalIdentifier $18 inputOutputLocalIdentifier  - clear CKM for Key X $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NR_KEY | string | Schlüsselnummer oder all bzw. alle Werte siehe table TKeyNr NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-copy-ckmdata"></a>
### STEUERN_COPY_CKMDATA

Kopieren der CKM Daten von Schlüssel X nach Schlüssel Y KWP2000: $30 InputOutputControlByLocalIdentifier $19 inputOutputLocalIdentifier  - copy CKM from Key X to Key Y $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NR_KEY_SOURCE | string | Quell-Schlüsselnummer (OHNE all bzw. alle) Werte siehe table TKeyNr NAME |
| NR_KEY_DEST | string | Ziel-Schlüsselnummer (auch all bzw. alle) Werte siehe table TKeyNr NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eject"></a>
### STEUERN_EJECT

Simulation Tastendruck EJECT-Taste KWP2000: $30 InputOutputControlByLocalIdentifier $0B inputOutputLocalIdentifier  - eject $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-flottenmodus"></a>
### STEUERN_FLOTTENMODUS

Steuern des aktuell zu aktivierenden Flottenmodus. (Art der NAVI-DVD Sperrung.) KWP2000: $30 InputOutputControlByLocalIdentifier $1B inputOutputLocalIdentifier $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_MODUS | string | Zu aktivierender Flottenmodus 0  ( Keine NAVI-DVD Sperrung ) 1  ( NAVI-DVD ist mit PIN-Code gesperrt ) 2  ( NAVI-DVD ist immer gesperrt. ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-frequenz"></a>
### STEUERN_FREQUENZ

Tunerfrequenz einstellen KWP2000: $30 InputOutputControlByLocalIdentifier $10 inputOutputLocalIdentifier  - set frequency $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREQUENZ | long | Bereich: 150 - 108000 [kHz] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klangzeichen"></a>
### STEUERN_KLANGZEICHEN

Ausloesen eines Klangzeichens KWP2000: $30 InputOutputControlByLocalIdentifier $02 inputOutputLocalIdentifier  - accoustic sign $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLANGZEICHEN | string | Ausloesen des gewaehlten Klangzeichens table TKlangZeichen NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| AUSGELOESTES_KLANGZEICHEN | string | OKAY, wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-linear"></a>
### STEUERN_LINEAR

Alle Toneinstellungen auf Defaultwerte setzten KWP2000: $30 InputOutputControlByLocalIdentifier $05 inputOutputLocalIdentifier  - device sound linear $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-next-entsource"></a>
### STEUERN_NEXT_ENTSOURCE

Weiterschaltung der Entertainment-Quelle per Diagnose KWP2000: $30 InputOutputControlByLocalIdentifier $1C inputOutputLocalIdentifier $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ENTSOURCE | string | Einzustellende Entertainmentquelle Werte aus table TEntSource Wenn weggelassen, dann weiterschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENTSOURCE | int | Neue Entertainmentquelle Werte aus table TEntSource |
| STAT_ENTSOURCE_TEXT | string | Neue Entertainmentquelle Werte aus table TEntSource |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-radio-schalten"></a>
### STEUERN_RADIO_SCHALTEN

Simulation Tastendruck ENTERTAINMENT-Taste KWP2000: $30 InputOutputControlByLocalIdentifier $0A inputOutputLocalIdentifier  - switch radio on or off $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHALTMODUS | string | EIN/AUS-Schalten des Radios table TSchaltmodi NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MODUS | string | Ein/aus-Status |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-rds"></a>
### STEUERN_RDS

Steuern AF-Verfolgung und TP KWP2000: $30 InputOutputControlByLocalIdentifier $14 inputOutputLocalIdentifier  - set RDS $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RDS | string | Steuern AF-Verfolgung und TP Werte siehe table TTunerRDS NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Ansteuerung des Selbsttests im MASK - Speichertests FLASH_ROM, RAM, Video-RAM, EEPROM Bei Erkennung eines Fehlverhaltens erfolgt ein Eintrag im Primaer- und Shadowfehlerspeicher. KWP2000: $31 startRoutineByLocalIdentifier $04 routineLocalIdentifier (selfTest) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT table JobResultExtended STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sinusgenerator-aus"></a>
### STEUERN_SINUSGENERATOR_AUS

Ausschalten des Sinusgenerators  KWP2000: $32 StopRoutineByLocalIdentifier $B8 routineLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-testbild"></a>
### STEUERN_TESTBILD

Ausgabe eines Testbildes KWP2000: $31 startRoutineByLocalIdentifier $A0 routineLocalIdentifier $XX Musterlänge $XX Farbe1 $XX Farbe2 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LAENGE | int | Laenge des Testmusters Bei Laenge 0 wird in den Normalmodus geschaltet Bereich: 0-1023 oder 0x00-0x3FF |
| FARBE_1 | int | Farbe 1 des Testbildes Bereich: 0-255 oder 0x00-0xFF |
| FARBE_2 | int | Farbe 2 des Testbildes Bereich: 0-255 oder 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tuner-suchlauf"></a>
### STEUERN_TUNER_SUCHLAUF

Sendersuchlauf des AM/FM-Tuner starten KWP2000: $30 InputOutputControlByLocalIdentifier $13 inputOutputLocalIdentifier  - Tuner_Suchlauf $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TUNER_SUCHLAUF | string | Steuern des Suchlaufs (INC/DEC/STOP) table TTunerSuchlauf NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-volumeaudio"></a>
### STEUERN_VOLUMEAUDIO

Einstellen der Audio-Lautstaerke KWP2000: $30 InputOutputControlByLocalIdentifier $03 inputOutputLocalIdentifier  - set volume $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VOLUME | string | Ausgewaehlte Audio-Lautstaerke  table TAudioVolume MASKE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| LAUTSTAERKE | string | eingestellte Lautstaerke |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lldatenrettung"></a>
### LLDATENRETTUNG

LowLevel MOST Datenrettungsschnittstelle KWP2000: $21 ReadDataByLocalIdentifier $02 LocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SEQUENCE | string | Abfolgestring zum Lesen/Schreiben der Indivdata via MOST |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_DATA | binary | MOST Antwort Indivdata |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-last-connection"></a>
### STATUS_LAST_CONNECTION

URL der letzen Verbindung wird ausgegeben KWP2000: $21 ReadDataByLocalIdentifier KWP2000: $17 LocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ONLINE_TEXT | string | Online Status als Textausgabe table OnlineStateTable ANZEIGE_TEXT |
| STAT_ONLINE | int | Online Status als Wert table OnlineStateTable WERT |
| STAT_CONNECTION_ATTEMPS | int | Anzahl der Verbindungsversuche |
| STAT_START_TIME_DATE | string | Start der Sitzung |
| STAT_END_TIME_DATE | string | Ende der Sitzung |
| STAT_BYTES_RECEIVED | long | Bytes received within last session (download) |
| STAT_BYTES_SENT | long | Bytes sent within last session (upload) |
| STAT_PHONE_NO | string | Telephone number of the RAS server |
| STAT_MODE | int | Digital, analogues or other dial-in 0x00 = GPRS, 0x01 = CSD |
| STAT_SIM_MNC | string | MNC (mobile network code) of SIM |
| STAT_SIM_MCC | string | MCC (mobile country code) of SIM |
| STAT_NET_MNC | string | MNC of net |
| STAT_NET_MCC | string | MCC of net |
| STAT_IP_NO | string | IP-number of the last connection. The IP-number will be provided by the PPP- RAS server |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sinusgenerator-ein"></a>
### STEUERN_SINUSGENERATOR_EIN

Aktivieren des Sinusgenerators und Ausgabe auf allen ausgewählten Lautsprechern SELECT_SPEAKER X  KWP2000: $31 StartRoutineByLocalIdentifier $B8 routineLocalIdentifier $xx Lautsprecherkanal Byte high $xx Lautsprecherkanal Byte low - $0001   Kanal links vorne - $0002   Kanal rechts vorne - (nur via AMP_60 -SGBD-&gt; $0004   Kanal Center) - (nur via AMP_60 -SGBD-&gt; $0008   Kanal Surround links) - (nur via AMP_60 -SGBD-&gt; $0010   Kanal Surround rechts) - $0020   Kanal links hinten - $0040   Kanal rechts hinten - $0080   Kanal Subwoofer links - $0100   Kanal Subwoofer rechts $xx Frequenz Byte high $xx Frequenz Byte low $xx Level

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREQUENZ | int | Frequenz Werte aus table TFrequSinusgenerator in Hz |
| LEVEL | int | Inkrementwert (Wird automatisch auf codierten Maximalwert begrenzt)) 0 - 255 |
| SELECT_SPEAKER1 | int | 1   Kanal links vorne 2   Kanal rechts vorne 32   Kanal links hinten 64  Kanal rechts hinten 128 Kanal Subwoofer links 256 Kanal Subwoofer rechts Nummer eines ausgewählten Lautsprechers der aktiv sein soll |
| SELECT_SPEAKER2 | int | Nummer eines ausgewählten Lautsprechers der aktiv sein soll (siehe SELECT_SPEAKER1) |
| SELECT_SPEAKER3 | int | Nummer eines ausgewählten Lautsprechers der aktiv sein soll (siehe SELECT_SPEAKER1) |
| SELECT_SPEAKER4 | int | Nummer eines ausgewählten Lautsprechers der aktiv sein soll (siehe SELECT_SPEAKER1) |
| SELECT_SPEAKER5 | int | Nummer eines ausgewählten Lautsprechers der aktiv sein soll (siehe SELECT_SPEAKER1) |
| SELECT_SPEAKER6 | int | Nummer eines ausgewählten Lautsprechers der aktiv sein soll (siehe SELECT_SPEAKER1) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-dar"></a>
### LESEN_DAR

Lesen eines DAR Datensatzes KWP2000: $31 StartRoutineByLocalId	$23 $33 RequestRoutineResults	$23 $21 ReadDataByLocalIdentifier	$1A

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DAR | unsigned char | Requested DAR Index from 0 on |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Status 0x00 OK, &gt;0 Error |
| RET_DAR | binary | DAR-Datensatz maximal 1 kByte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-dar"></a>
### SCHREIBEN_DAR

Schreiben eines DAR Datensatzes KWP2000: $31 StartRoutineByLocalId	$25,$26 $33 RequestRoutineResults	$26 $3B WriteDataByLocalIdentifier	$A4

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DAR | unsigned char | Requested DAR Index from 0 on |
| ARG_FILE | string | DAR read from file to be written |
| ARG_STREAM | string | DAR read from STREAM to be written |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Status 0x00 OK, &gt;0 Error |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-online-logging"></a>
### LESEN_ONLINE_LOGGING

Lesen einer Zeile Onlinelogging KWP2000: $31 StartRoutineByLocalId	$27 $33 RequestRoutineResults	$27 $21 ReadDataByLocalIdentifier	$1C

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LINE | int | Requested LINE Index from 0 on 0xffff (-1) for request maxlines |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Status 0x00 OK, &gt;0 Error |
| RET_LINE | string | Loggingzeile maximal 1 kByte |
| RET_NUMBERLINES | int | Anzahl Loggingzeilen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-browser-history"></a>
### LESEN_BROWSER_HISTORY

Lesen einer Zeile der Browser History KWP2000: $31 StartRoutineByLocalId	$29 $33 RequestRoutineResults	$29 $21 ReadDataByLocalIdentifier	$1E

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LINE | int | Requested LINE Index from 0 on 0xffff (-1) for request maxlines |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Status 0x00 OK, &gt;0 Error |
| RET_LINE | string | Historyzeile maximal 1 kByte |
| RET_NUMBERLINES | int | Anzahl Historyzeilen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-browser-errors"></a>
### LESEN_BROWSER_ERRORS

Lesen einer Zeile des Browsererrorlogs KWP2000: $31 StartRoutineByLocalId	$28 $33 RequestRoutineResults	$28 $21 ReadDataByLocalIdentifier	$1D

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LINE | int | Requested LINE Index from 0 on 0xffff (-1) for request maxlines |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Status 0x00 OK, &gt;0 Error |
| RET_LINE | string | Errorlogzeile maximal 1 kByte |
| RET_NUMBERLINES | int | Anzahl Errorlogzeilen |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-access-records"></a>
### LESEN_ACCESS_RECORDS

Lesen eines AR Datensatzes KWP2000: $31 StartRoutineByLocalId	$24 $33 RequestRoutineResults  $24 $21 ReadDataByLocalIdentifier  $1B

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_AR | int | Requested AR Index from 0 on 0xffff (-1) for request maxlines |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Status 0x00 OK, &gt;0 Error |
| RET_NUMBERARS | int | Anzahl AccessReccords |
| RET_AR | binary | AR-Datensatz maximal 1 kByte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dar-index"></a>
### STATUS_DAR_INDEX

Reading of the actually coded DAR-Index KWP2000: $21 ReadDataByLocalID $18 localID Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DAR_INDEX | int | actually coded DAR-Index |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-browser-appl"></a>
### STATUS_BROWSER_APPL

Check if application coded and check POPUP KWP2000: $21 ReadDataByLocalID $19 localID Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODED | int | Codingstate of application |
| STAT_APPL | int | State of application task |
| STAT_POPUP | int | actual popup state |
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
- [JOBRESULTEXTENDED](#table-jobresultextended) (7 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (6 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (6 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (6 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (4 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (4 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (3 × 9)
- [SHADOWDTC](#table-shadowdtc) (4 × 2)
- [TAUDIOKANAL](#table-taudiokanal) (11 × 3)
- [TAUDIOVOLUME](#table-taudiovolume) (30 × 2)
- [TFBLOCKIDTEXTE](#table-tfblockidtexte) (39 × 2)
- [TANTENNADIAG](#table-tantennadiag) (2 × 3)
- [TTUNERRI](#table-ttunerri) (3 × 2)
- [TTUNERRDS](#table-ttunerrds) (5 × 3)
- [TTUNERSUCHLAUF](#table-ttunersuchlauf) (4 × 2)
- [TSCHALTMODI](#table-tschaltmodi) (5 × 3)
- [LOOKCONNTABLE](#table-lookconntable) (66 × 2)
- [LOOKCONNTABLEDETAIL](#table-lookconntabledetail) (6 × 2)
- [TKLANGZEICHEN](#table-tklangzeichen) (11 × 3)
- [TLAENDERVARIANTETUNER](#table-tlaendervariantetuner) (6 × 2)
- [TTPFUNKTION](#table-ttpfunktion) (3 × 2)
- [TRDSAFFUNKTION](#table-trdsaffunktion) (6 × 2)
- [TPTYTABELLE](#table-tptytabelle) (3 × 2)
- [TREGIONALISIERUNG](#table-tregionalisierung) (4 × 2)
- [THIGHCUT](#table-thighcut) (5 × 2)
- [TSENDERTAB](#table-tsendertab) (3 × 2)
- [TKEYNR](#table-tkeynr) (8 × 2)
- [TFLOTTENMODUS](#table-tflottenmodus) (3 × 2)
- [TENTSOURCE](#table-tentsource) (16 × 2)
- [THWVARIANTE](#table-thwvariante) (4 × 3)
- [TLAUFWERKSVARIANTE](#table-tlaufwerksvariante) (5 × 3)
- [TFREQUSINUSGENERATOR](#table-tfrequsinusgenerator) (25 × 1)
- [LWREASON](#table-lwreason) (4 × 2)
- [ANTREASON](#table-antreason) (3 × 2)
- [ONLINESTATETABLE](#table-onlinestatetable) (3 × 2)
- [TINDIVIDUALDATALISTE](#table-tindividualdataliste) (38 × 17)

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
| 1 | BMW-FAST |
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 6 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xABC8 | 0xABC8: Fehler Speichertest MASK |
| 0xABC9 | 0xABC9: Laufwerk defekt |
| 0xABCA | 0xABCA: Antenne offen oder Kurzschluss |
| 0xABCB | 0xABCB: Fehler in der Antennen-Stromversorgung |
| 0xABCC | 0xABCC: Error Communication TopHiFi |
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

Dimensions: 6 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xABC8 | 0x01 | 0x02 | -- | -- |
| 0xABC9 | 0x01 | 0x03 | -- | -- |
| 0xABCA | 0x01 | 0x04 | -- | -- |
| 0xABCB | 0x01 | 0xFF | -- | -- |
| 0xABCC | 0x01 | 0xFF | - | - |
| default | - | - | -- | -- |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 6 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Temperatur MMI-Rechner | Grad C | H | s int | -- | 1 | 1 | 0 |
| 0x02 | Shadow DTC | 0-n | -- | 0xFFFF | ShadowDTC | -- | -- | -- |
| 0x03 | Laufwerksfehler | 0-n | - | 0xFFFF | LWReason | - | - | - |
| 0x04 | Antennenfehler | 0-n | - | 0xFFFF | ANTReason | - | - | - |
| 0xFF | Dummy | 1 | high | signed int | - | - | - | - |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | u int | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 4 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xABD8 | 0xABD8: Fehler FLASH-ROM |
| 0xABD9 | 0xABD9: Fehler RAM |
| 0xABDA | 0xABDA: Laufwerk Temperatur |
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

Dimensions: 4 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xABD8 | 0x01 | -- | -- | -- |
| 0xABD9 | 0x01 | - | - | - |
| 0xABDA | 0x01 | 0x02 | -- | -- |
| default | -- | -- | -- | -- |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Temperatur MMI-Rechner | Grad C | H | s int | -- | 1 | 1 | 0 |
| 0x02 | Temperatur Laufwerk | Grad C | high | signed int | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | -- | u int | -- | 1 | 1 | 0 |

<a id="table-shadowdtc"></a>
### SHADOWDTC

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0xABD8 | 0xABD8: Fehler FLASH-ROM |
| 0xABD9 | 0xABD9: Fehler RAM |
| 0xABDA | 0xABDA: Laufwerk Temperatur |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-taudiokanal"></a>
### TAUDIOKANAL

Dimensions: 11 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| VL | 0x01 | Lautsprecher Vorne Links |
| VR | 0x02 | Lautsprecher Vorne Rechts |
| HHL | 0x03 | Lautsprecher Hutablage Hinten Links |
| HHR | 0x04 | Lautsprecher Hutablage Hinten Rechts |
| ZBL | 0x05 | Lautsprecher Zentral Bass Links |
| ZBR | 0x06 | Lautsprecher Zentral Bass Rechts |
| SHL | 0x07 | Lautsprecher Surround Hinten Links |
| SHR | 0x08 | Lautsprecher Surround Hinten Rechts |
| CS | 0x09 | Lautsprecher Centerspeaker |
| ALLE | 0x0A | Alle Lautsprecher |
| XY | 0xXY | Nicht definiert |

<a id="table-taudiovolume"></a>
### TAUDIOVOLUME

Dimensions: 30 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | Mute |
| 0x0F | Inkrement 15 |
| 0x10 | Inkrement 16 |
| 0x11 | Inkrement 17 |
| 0x12 | Inkrement 18 |
| 0x13 | Inkrement 19 |
| 0x14 | Inkrement 20 |
| 0x16 | Inkrement 22 |
| 0x18 | Inkrement 24 |
| 0x1A | Inkrement 26 |
| 0x1C | Inkrement 28 |
| 0x1E | Inkrement 30 |
| 0x20 | Inkrement 32 |
| 0x22 | Inkrement 34 |
| 0x24 | Inkrement 36 |
| 0x26 | Inkrement 38 |
| 0x28 | Inkrement 40 |
| 0x2A | Inkrement 42 |
| 0x2C | Inkrement 44 |
| 0x2E | Inkrement 46 |
| 0x30 | Inkrement 48 |
| 0x32 | Inkrement 50 |
| 0x34 | Inkrement 52 |
| 0x36 | Inkrement 54 |
| 0x38 | Inkrement 56 |
| 0x3A | Inkrement 58 |
| 0x3C | Inkrement 60 |
| 0x3E | Inkrement 62 |
| 0x3F | Maximal |
| 0xXY | Nicht definiert |

<a id="table-tfblockidtexte"></a>
### TFBLOCKIDTEXTE

Dimensions: 39 rows × 2 columns

| FBLOCKID | NAME |
| --- | --- |
| 0x02 | NetworkMaster=0x02 |
| 0x03 | ConnectionMaster=0x03 |
| 0x04 | PowerMaster=0x04 |
| 0x05 | Vehicle=0x05 |
| 0x06 | Diagnose=0x06 |
| 0x07 | VideoSwitch=0x07 |
| 0x10 | ManMachineInterface=0x10 |
| 0x11 | Sprachverarbeitungssystem=0x11 |
| 0x15 | ControlElements=0x15 |
| 0x16 | Security=0x16 |
| 0x20 | AudioMaster=0x20 |
| 0x22 | AudioAmplifier=0x22 |
| 0x23 | HeadPhoneAmplifier=0x23 |
| 0x24 | AuxilliaryInput=0x24 |
| 0x26 | MicrophoneInput=0x26 |
| 0x31 | AudioDiscPlayer=0x31 |
| 0x32 | MultiMediaChanger=0x32 |
| 0x40 | AM/FM Tuner=0x40 |
| 0x41 | TMC Tuner=0x41 |
| 0x42 | TVTuner=0x42 |
| 0x43 | ExternSource=0x43 |
| 0x44 | SDARS=0x44 |
| 0x50 | TelefonFix=0x50 |
| 0x51 | PhoneBook=0x51 |
| 0x52 | Navigationssystem=0x52 |
| 0x6F | Monitor=0x6F |
| 0x71 | Climate=0x71 |
| 0x80 | MMI_Terminal=0x80 |
| 0x81 | KOMBI_Terminal=0x81 |
| 0x90 | Telematik=0x90 |
| 0xAB | EDIABAS4MOST=0xAB |
| 0xC9 | Service=0xC9 |
| 0xCA | KombiMiscFkts=0xCA |
| 0xCB | Bordcomputer=0xCB |
| 0xCC | ADASInterface=0xCC |
| 0xE0 | KombiInterface=0xE0 |
| 0xE1 | HUDInterface=0xE1 |
| 0xFD | Sahara=0xFD |
| 0xXY | Unbekannter FBlock |

<a id="table-tantennadiag"></a>
### TANTENNADIAG

Dimensions: 2 rows × 3 columns

| WERT | TEXT | VALUE |
| --- | --- | --- |
| 0x00 | Antenna Diag not Ok | 1 |
| 0x01 | Antenna Diag Ok | 0 |

<a id="table-ttunerri"></a>
### TTUNERRI

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Ri not Ok |
| 0x01 | Ri Ok |
| 0xXY | Fehler |

<a id="table-ttunerrds"></a>
### TTUNERRDS

Dimensions: 5 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| 0 | 0x00 | AF aus / TP aus |
| 1 | 0x01 | AF aus / TP ein |
| 2 | 0x02 | AF ein / TP aus |
| 3 | 0x03 | AF ein / TP ein |
| Fehler | 0xXY | Nicht definiert |

<a id="table-ttunersuchlauf"></a>
### TTUNERSUCHLAUF

Dimensions: 4 rows × 2 columns

| NAME | MASKE |
| --- | --- |
| STOP | 0x00 |
| INC | 0x01 |
| DEC | 0x07 |
| Fehler | 0xXY |

<a id="table-tschaltmodi"></a>
### TSCHALTMODI

Dimensions: 5 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| aus | 0x00 | Radio aus |
| ein | 0x01 | Radio ein |
| off | 0x00 | Radio aus |
| on | 0x01 | Radio ein |
| Fehler | 0xXY | Nicht definiert |

<a id="table-lookconntable"></a>
### LOOKCONNTABLE

Dimensions: 66 rows × 2 columns

| NAME | MASKE |
| --- | --- |
| Tuner/LS = 0x01 | 0x01 |
| Tuner/KHL = 0x02 | 0x02 |
| Tuner/KHR = 0x03 | 0x03 |
| Null-Device/LS = 0x08 | 0x08 |
| Null-Device/KHL = 0x09 | 0x09 |
| Null-Device/KHR = 0x0A | 0x0A |
| Audio-TP/LS = 0x10 | 0x10 |
| Audio-TP/KHL = 0x11 | 0x11 |
| Audio-TP/KHR = 0x12 | 0x12 |
| Audio-DP.01.01/LS = 0x18 | 0x18 |
| Audio-DP.01.01/KHL = 0x19 | 0x19 |
| Audio-DP.01.01/KHR = 0x1A | 0x1A |
| Audio-DP.02.01/LS = 0x20 | 0x20 |
| Audio-DP.02.01/KHL = 0x21 | 0x21 |
| Audio-DP.02.01/KHR = 0x22 | 0x22 |
| Audio-MMP/LS = 0x28 | 0x28 |
| Audio-MMP/KHL = 0x29 | 0x29 |
| Audio-MMP/KHR = 0x2A | 0x2A |
| SES.00.01/LS = 0x30 | 0x30 |
| SES-MISCHEN/LS = 0x31 | 0x31 |
| Microphone.00.01/SES.00.11 = 0x32 | 0x32 |
| TelephoneFix.00.01/LS = 0x40 | 0x40 |
| Telephone-Mix/LS = 0x41 | 0x41 |
| Telephone-Menue/LS = 0x42 | 0x42 |
| Microphone.00.01/Telefon.00.11 = 0x40/41 | 0x40/0x41 |
| Microphone.00.01/SES.00.11 = 0x30/31/32 | 0x30/0x31/0x32 |
| Microphone.00.01/SecurityFunk1 = 0x68 | 0x68 |
| Microphone.00.01/SecurityFunk2 = 0x69 | 0x69 |
| Microphone.00.01/SecurityWSA = 0x6A | 0x6A |
| TVTuner.00.01/LS = 0x50 | 0x50 |
| TVTuner.00.01/KHL = 0x51 | 0x51 |
| TVTuner.00.01/KHR = 0x52 | 0x52 |
| Navigation.00.01-Mix/LS = 0x58 | 0x58 |
| Browser/LS = 0x70 | 0x70 |
| Browser/KHL = 0x71 | 0x71 |
| Browser/KHR = 0x72 | 0x72 |
| TM-Meldung/LS = 0x38 | 0x38 |
| PTY-Meldung/LS = 0x48 | 0x48 |
| AMFM-TapePlayer/LS = 0x60 | 0x60 |
| AMFM-TapePlayer/KHL = 0x61 | 0x61 |
| AMFM-TapePlayer/KHR = 0x62 | 0x62 |
| SecurityFunk_1/LS = 0x68 | 0x68 |
| SecurityFunk_2/LS = 0x69 | 0x69 |
| SecurityWSA/LS = 0x6A | 0x6A |
| SDARS/LS = 0x6b | 0x6B |
| SDARS/KHL = 0x6C | 0x6C |
| SDARS/KHR = 0x6D | 0x6D |
| DAB/LS = 0x90 | 0x90 |
| DAB/KHL = 0x91 | 0x91 |
| DAB/KHR = 0x92 | 0x92 |
| ISDBT/LS = 0xA0 | 0xA0 |
| ISDBT/KHL = 0xA1 | 0xA1 |
| ISDBT/KHR = 0xA2 | 0xA2 |
| MSB/LS = 0x74 | 0x74 |
| MSB/KHL = 0x75 | 0x75 |
| MSB/KHR = 0x76 | 0x76 |
| AUXonMOST/LS = 0x77 | 0x77 |
| AUXonMOST/KHL = 0x78 | 0x78 |
| AUXonMOST/KHR = 0x79 | 0x79 |
| AUX analog/LS = 0x80 | 0x80 |
| AUX analog/KHL = 0x81 | 0x81 |
| AUX analog/KHR = 0x82 | 0x82 |
| Telefon_analog_fix/LS = 0x83 | 0x83 |
| PDC/LS = 0x84 | 0x84 |
| Gong/LS = 0x85 | 0x85 |
| Fehler = 0xXY | 0xXY |

<a id="table-lookconntabledetail"></a>
### LOOKCONNTABLEDETAIL

Dimensions: 6 rows × 2 columns

| NAME | MASKE |
| --- | --- |
| Muted | 0x00 |
| Demuted | 0x01 |
| IN_MEMORY | 0x02 |
| NOT_CONNECTED | 0x03 |
| CONNECTED | 0x04 |
| Error | 0xXY |

<a id="table-tklangzeichen"></a>
### TKLANGZEICHEN

Dimensions: 11 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| off | 0x00 | Off |
| ACC | 0x01 | ACC-Signal |
| CCG | 0x02 | CCG-Signal |
| DG | 0x03 | DG-Signal |
| Std-Signal | 0x04 | Stunden-Signal |
| IMG_Start | 0x05 | Intermetierendes Signal |
| IMG_Stop | 0x06 | Intermetierendes Signal beenden |
| tlc-left | 0x0D | TLC-Left |
| tlc-right | 0x0E | TLC-Right |
| tlc-stop | 0x0F | TLC-Stop |
| XY | 0xXY | Nicht definiert |

<a id="table-tlaendervariantetuner"></a>
### TLAENDERVARIANTETUNER

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ECE |
| 0x01 | US |
| 0x02 | Japan |
| 0x03 | Oceanien |
| 0x07 | No Area |
| 0xXY | nicht definiert |

<a id="table-ttpfunktion"></a>
### TTPFUNKTION

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | TP nicht aktiv |
| 0x01 | TP aktiv |
| 0xXY | nicht definiert |

<a id="table-trdsaffunktion"></a>
### TRDSAFFUNKTION

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | RDS ein; AF aus |
| 0x01 | RDS ein; AF manuell |
| 0x02 | RDS ein; AF automatisch |
| 0x03 | RDS aus |
| 0x07 | Nicht definiert |
| 0xXY | nicht definiert |

<a id="table-tptytabelle"></a>
### TPTYTABELLE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | PTY ECE |
| 0x01 | PTY US |
| 0xXY | nicht definiert |

<a id="table-tregionalisierung"></a>
### TREGIONALISIERUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Wert 0 |
| 0x01 | Wert 1 |
| 0x02 | Wert 2 |
| 0xXY | nicht definiert |

<a id="table-thighcut"></a>
### THIGHCUT

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | High |
| 0x01 | Low |
| 0x02 | Auto |
| 0x03 | Notch |
| 0xXY | nicht definiert |

<a id="table-tsendertab"></a>
### TSENDERTAB

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | HGL |
| 0x01 | FMD |
| 0xXY | nicht definiert |

<a id="table-tkeynr"></a>
### TKEYNR

Dimensions: 8 rows × 2 columns

| NAME | KEYNR |
| --- | --- |
| 0 | 0x00 |
| 1 | 0x01 |
| 2 | 0x02 |
| 3 | 0x03 |
| 15 | 0x0F |
| all | 0xFF |
| alle | 0xFF |
| default | 0xEE |

<a id="table-tflottenmodus"></a>
### TFLOTTENMODUS

Dimensions: 3 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | Keine NAVI-DVD Sperrung |
| 0x01 | NAVI-DVD ist mit PIN-Code gesperrt |
| 0x02 | NAVI-DVD ist immer gesperrt |

<a id="table-tentsource"></a>
### TENTSOURCE

Dimensions: 16 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | next |
| 0x01 | FM |
| 0x02 | AM |
| 0x03 | SCD |
| 0x04 | CDC |
| 0x05 | MD |
| 0x06 | WB |
| 0x07 | SDARS |
| 0x08 | IBOC |
| 0x09 | AUX |
| 0x0A | DVD |
| 0x0B | TV |
| 0x0C | VIDEOTXT |
| 0x0D | AV-AUX |
| 0x0E | DAB |
| 0xFF | Entertainmentsource not available |

<a id="table-thwvariante"></a>
### THWVARIANTE

Dimensions: 4 rows × 3 columns

| NAME | MASKE | WERT |
| --- | --- | --- |
| STEREO | 0x11 | 0 |
| HIFI | 0x01 | 1 |
| TOP-HIFI | 0x02 | 2 |
| Fehler | 0xXY | -1 |

<a id="table-tlaufwerksvariante"></a>
### TLAUFWERKSVARIANTE

Dimensions: 5 rows × 3 columns

| NAME | MASKE | WERT |
| --- | --- | --- |
| CDROM-Laufwerk | 0x01 | 1 |
| CDAudio-Laufwerk | 0x02 | 2 |
| DVD-Laufwerk | 0x03 | 3 |
| MD-Laufwerk | 0x04 | 4 |
| Unbekannt | 0xXY | -1 |

<a id="table-tfrequsinusgenerator"></a>
### TFREQUSINUSGENERATOR

Dimensions: 25 rows × 1 columns

| WERT |
| --- |
| 20000 |
| 18000 |
| 16000 |
| 15000 |
| 14000 |
| 12500 |
| 10000 |
| 8900 |
| 4450 |
| 3550 |
| 2800 |
| 2200 |
| 1800 |
| 1400 |
| 1000 |
| 700 |
| 300 |
| 200 |
| 100 |
| 89 |
| 63 |
| 50 |
| 40 |
| 28 |
| 20 |

<a id="table-lwreason"></a>
### LWREASON

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Mechanikfehler |
| 0x02 | Kommunikationsfehler |
| 0x03 | Flash Programmierfehler |
| 0xFFFF | unbekannter Grund |

<a id="table-antreason"></a>
### ANTREASON

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Offen oder Kurz gegen Vcc |
| 0x02 | Kurz gegen Masse |
| 0xFFFF | unbekannter Grund |

<a id="table-onlinestatetable"></a>
### ONLINESTATETABLE

Dimensions: 3 rows × 2 columns

| WERT | ANZEIGE_TEXT |
| --- | --- |
| 0x00 | Online-Status OK |
| 0x01 | Daten nicht abrufbar |
| 0xXY | nicht definiert |

<a id="table-tindividualdataliste"></a>
### TINDIVIDUALDATALISTE

Dimensions: 38 rows × 17 columns

| ENTRYNR | ISLAST | FROMWHERE | DIAG | CARORKEY | USECASE | TESTER_ALGO | RESERVED | INQY_LEN | INQY_DATA | RESP_LEN | RESP_DATA | WRITE_LEN | WRITE_DATA | W_RESP_LEN | W_RESP_DATA | COMMENT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0000 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 05 | 2000020001 | 04 | 20000200 | 05 | 2000020000 | 00 |  | AudioMaster.VolumeActual |
| 0x0001 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 05 | 2000022001 | 04 | 20000220 | 05 | 2000022000 | 00 |  | AudioMaster.Balance |
| 0x0002 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 05 | 2000022101 | 04 | 20000221 | 05 | 2000022100 | 00 |  | AudioMaster.Fader |
| 0x0003 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 05 | 2000022201 | 04 | 20000222 | 05 | 2000022200 | 00 |  | AudioMaster.Bass |
| 0x0004 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 05 | 2000022301 | 04 | 20000223 | 05 | 2000022300 | 00 |  | AudioMaster.Treble |
| 0x0005 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 05 | 2000026001 | 04 | 20000260 | 05 | 2000026000 | 00 |  | AudioMaster.AMSDVolumeTable(GAL) |
| 0x0006 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 05 | 2000027101 | 04 | 20000271 | 05 | 2000027100 | 00 |  | AudioMaster.AMReverbRoomSize(LOG7) |
| 0x0007 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 2202046301020000 | 04 | 22020463 | 05 | 2202046300 | 00 |  | GraphEqualizerStd(nur an TOPHIFI!!!) |
| 0x0008 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020104 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos1 |
| 0x0009 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C0301 | 00 |  | FMPresetSave.Pos1 |
| 0x000A | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020204 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos2 |
| 0x000B | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C0302 | 00 |  | FMPresetSave.Pos2 |
| 0x000C | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020304 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos3 |
| 0x000D | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C0303 | 00 |  | FMPresetSave.Pos3 |
| 0x000E | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020404 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos4 |
| 0x000F | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C0304 | 00 |  | FMPresetSave.Pos4 |
| 0x0010 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020504 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos5 |
| 0x0011 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C0305 | 00 |  | FMPresetSave.Pos5 |
| 0x0012 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020604 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos6 |
| 0x0013 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C0306 | 00 |  | FMPresetSave.Pos6 |
| 0x0014 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020704 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos7 |
| 0x0015 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C0307 | 00 |  | FMPresetSave.Pos7 |
| 0x0016 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020804 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos8 |
| 0x0017 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C0308 | 00 |  | FMPresetSave.Pos8 |
| 0x0018 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020904 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos9 |
| 0x0019 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C0309 | 00 |  | FMPresetSave.Pos9 |
| 0x001A | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020A04 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos10 |
| 0x001B | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C030A | 00 |  | FMPresetSave.Pos10 |
| 0x001C | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020B04 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos11 |
| 0x001D | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C030B | 00 |  | FMPresetSave.Pos11 |
| 0x001E | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 08 | 40000C0301020C04 | 04 | 40000C03 | 05 | 4000020600 | 00 |  | FMPresetList.Pos12 |
| 0x001F | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 00 |  | 00 |  | 09 | 4000040000030C030C | 00 |  | FMPresetSave.Pos12 |
| 0x0020 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 05 | 1001020201 | 04 | 10010202 | 05 | 1001020200 | 00 |  | MMI.CurrentUnits |
| 0x0021 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 05 | 1001020001 | 04 | 10010200 | 05 | 1001020000 | 00 |  | MMI.CurrentLanguage |
| 0x0022 | 0x00 | 01 | 63 | 02 | 000F | 01 | 00 | 05 | 1001025301 | 04 | 10010253 | 05 | 1001025300 | 00 |  | MMI.ActionSpecialFunctionButtonMFL |
| 0x0023 | 0x00 | 03 | 63 | 02 | 000F | 01 | 00 | 01 | 01 | 00 |  | 01 | 01 | 00 |  | NaviAdressbook.Liste1 |
| 0x0024 | 0x00 | 03 | 63 | 02 | 000F | 01 | 00 | 01 | 02 | 00 |  | 01 | 02 | 00 |  | NaviAdressbook.Liste2(Home) |
| 0x0025 | 0xFF | 03 | 63 | 02 | 000F | 01 | 00 | 01 | 03 | 00 |  | 01 | 03 | 00 |  | NaviAdressbook.Liste3(Last) |
