# komb65_2.prg

- Jobs: [121](#jobs)
- Tables: [35](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | KOMBI E65 |
| ORIGIN | BMW TI-431 Dennert |
| REVISION | 3.002 |
| AUTHOR | BMW TI-431 Lothar, SiemensVDO EI-42 Neudecker |
| COMMENT | SGBD in KWP2000-format |
| PACKAGE | 1.33 |
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
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS Version 1-3) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS Version 1-3) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
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
- [C_FG_LESEN2](#job-c-fg-lesen2) - Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [SG_RESET_OHNE_UHR_DATUM](#job-sg-reset-ohne-uhr-datum) - Steuergeraete Reset ausloesen Uhrzeit und Datum bleibt dabei im Kombi erhalten KWP2000: $31, $20
- [C_CHECKSUMME](#job-c-checksumme) - Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob
- [STEUERN_LEUCHTE](#job-steuern-leuchte) - Kontrolleuchten einzeln ansteuern Fuer Service-und Testzwecke Es muessen immer sieben Argumente im Bereich von 0x00-0xFF uebergeben werden.  Im Kombi LH Teil 3.1 Kapitel "Diagnose" sind die Übergabeparameter des Diagnosebefehls $30 $07 ausführlich dokumentiert  KWP2000: $30 $07 InputOutputControlByLocalIdentifier Modus  : Default
- [STEUERN_LEUCHTE_AUS](#job-steuern-leuchte-aus) - Wenn vorher der Job STEUERN_LEUCHTE aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_LEUCHTE_ENDE gibt die Kontrolle wieder an das Kombi zurueck KWP2000: $30, $23, $00
- [STEUERN_BLINKER](#job-steuern-blinker) - Blinker, zentrales Warnfeld, Ganganzeigenbeeleuchtung, Fernlicht ansteuern Fuer Service-und Testzwecke Es muessen immer alle zwei Argumente übergeben werden Nach Aufruf dieses Jobs muss der Vorgabemodus durch STEUERN_BLINKER_AUS beendet werden KWP2000: $30 $24  Beschreibung der Arumente: -------------------------- BYTE 0: High Nibble: 0 = beide Blinkkontrolleuchten aus 1 = Blinker links 2 = Blinker rechts 3 = Blinker rechts und links LOW Nibble:  1 = normales Blinken 2 = Blinker defekt (doppelte Blinkgeschwindigkeit) 3 = Doppelblinkimpuls Warnblinken Beispiel: BYTE 1= 0x12h bedeutet: Blinker links blinkt mit doppelter Geschwindigkeit  BYTE 1: 04h = Fernlicht ein 10h = zentr. Warnfeld rot ein 20h = zentr. Warnfeld gelb ein 40h = Beleuchtung Ganganzeigenfeld 80h = zentr. Warnfeld orange ein 00h = Fernlicht aus, zentr. Warnfeld aus, Beleuchtung Ganganzeigenfeld aus
- [STEUERN_BLINKER_AUS](#job-steuern-blinker-aus) - Wenn vorher der Job STEUERN_BLINKER aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_BLINKER_ENDE gibt die Kontrolle wieder an das Kombi zurueck KWP2000: $30, $24, $00
- [STEUERN_PPC_IO_SCHREIBEN](#job-steuern-ppc-io-schreiben) - I/O Ports des MPC555 schreiben Fuer Service-und Testzwecke Es muessen immer alle drei Argumente im Bereich von 0x00-0xFF uebergeben werden. KWP2000: $30 InputOutputControlByLocalIdentifier Modus  : Default
- [STATUS_PPC_IO_LESEN](#job-status-ppc-io-lesen) - I/O Ports des MPC555 lesen Fuer Service-und Testzwecke  KWP2000: $30,$93,$01, $XX -&gt; InputOutputControlByLocalIdentifier
- [STEUERN_PPC_IO_SCHREIBEN_AUS](#job-steuern-ppc-io-schreiben-aus) - Wenn vorher der Job ADC_SCHREIBEN aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_LEUCHTE_ENDE gibt die Kontrolle wieder an das Kombi zurueck KWP2000: $30, $23, $00
- [STEUERN_SELBSTTEST_EIN](#job-steuern-selbsttest-ein) - Schaltet den Selbttest ein KWP2000: $30, $26, $06
- [STEUERN_SELBSTTEST_AUS](#job-steuern-selbsttest-aus) - Schaltet den Selbsttest wieder aus KWP2000: $30, $23, $00
- [STEUERN_TESTBITMAP_ANZEIGEN](#job-steuern-testbitmap-anzeigen) - Anzeige des Testbitmaps im Kombi Zustand ist erst durch Sleep Modus beendet KWP2000: $30, $FD, $06
- [STEUERN_TACHO](#job-steuern-tacho) - Tacho auf einen bel winkel zwischen 0..300 Grad setzen KWP2000: $30 InputOutputControlByLocalIdentifier
- [STEUERN_TACHO_AUS](#job-steuern-tacho-aus) - Schaltet den Tacho-Vorgabemodus wieder aus KWP2000: $30, $20, $00
- [STEUERN_DREHZAHL](#job-steuern-drehzahl) - Tacho auf einen bel winkel zwischen 0..300 Grad setzen KWP2000: $30 InputOutputControlByLocalIdentifier
- [STEUERN_DREHZAHL_AUS](#job-steuern-drehzahl-aus) - Schaltet den Tacho-Vorgabemodus wieder aus KWP2000: $30, $20, $00
- [STATUS_TACHO_LESEN](#job-status-tacho-lesen) - gibt die Anzeigegeschwindigleit aus (Einheit km/h) KWP2000: $21, $05
- [STATUS_DREHZAHL_LESEN](#job-status-drehzahl-lesen) - gibt die Motordrehzahl aus (Einheit Umdrehungen/min) KWP2000: $21, $06
- [STATUS_LENKSTOCK_LESEN](#job-status-lenkstock-lesen) - gibt den Status des Lenkstockschalters aus KWP2000: $21, $07 
- [STATUS_CHECKCONTROL_LESEN](#job-status-checkcontrol-lesen) - gibt die ID Nummern der momentan aktiven CC-Meldungen aus KWP2000: $21, $09 Es bedeudet Rückgabewert ANZAHL     = Anzahl der aktiven Meldungen CC_Nummern = CC-Meldungen als Datenarray (pro Zahl 2 Byte)
- [STATUS_DATE_LAST_CODING_SESSION](#job-status-date-last-coding-session) - Datum, gibt an, wann das Kombi zum letzten mal codiert wurde (bei BMW) KWP2000: $21, $08
- [STATUS_TANKINHALT_LESEN](#job-status-tankinhalt-lesen) - Literwerte der Tank Hebelgeber links und rechts, Summerwert ungedämpft und gedämpft KWP2000: $21, $0A
- [STATUS_KL30_H_OFFSET](#job-status-kl30-h-offset) - Klemme 30 Stundenzaehler Offset auslesen KWP2000: $21, $0C
- [STEUERN_KL30_H_OFFSET](#job-steuern-kl30-h-offset) - Klemme 30 Stundenzaehler Offset schreiben KWP2000: $3B, $0C
- [STEUERN_KL30_H_COUNTER](#job-steuern-kl30-h-counter) - Klemme 30 Stundenzaehler schreiben KWP2000: $3B, $0D
- [CALC_KL30_H_OFFSET](#job-calc-kl30-h-offset) - Klemme 30 Stundenzaehler Offset ab dem momentanen Datum berechnen Dieser Job wird nur in der BMW-Fertigung im Rahmen der Codierung aufgerufen
- [SET_KL30_OFFSET2AKT_DATE](#job-set-kl30-offset2akt-date) - Berechnet den Klemme 30 Stundenzaehler Offset ab dem momentanen Datum und schreibt diesen in das EEPROM des KOMBI BOS funtioniert nur richtig, wenn der KL30_H_OFFSET richtig gesetzt ist. Daher sollte der Job immer aufgerufen werden wenn das Fahrzeug an den Taster angeschlossen wird KWP2000: $3B, $0C
- [UHRZEIT_DATUM_STELLEN](#job-uhrzeit-datum-stellen) - Uhrzeit auf das aktuelle Datum stellen KWP2000: $3B, $0E
- [STATUS_KL30_H_ZAEHLER](#job-status-kl30-h-zaehler) - Klemme 30 Stundenzaehler auslesen KWP2000: $21, $0D
- [STATUS_BETRIEBSDATEN_LESEN](#job-status-betriebsdaten-lesen) - liest ausgewählte Daten aus CBS Betriebsdaten aus KWP2000 $21 $B1 bis $BE
- [STATUS_BETRIEBSDATEN_HEADER](#job-status-betriebsdaten-header) - gibt den KM Stand aus CBS Betriebsdaten Header aus KWP2000 $21 $B0
- [STATUS_ZEITSTRAHL](#job-status-zeitstrahl) - gibt BOS Daten für den Annahmerechner in der Reihenfolge Header BOS Umpfänge, CC Umpfänge KWP2000 $21 $C0 Für die exakte Beschreiung der BOS Zeitstrahldaten siehe LH Teil 3 Kapitel Diagnose, Beschreibung zu $21
- [STEUERN_PPC_ADC_SCHREIBEN](#job-steuern-ppc-adc-schreiben) - AD Kanaele des MPC555 schreiben Fuer Service-und Testzwecke  Es muessen immer alle Argumente im Bereich von 0x00-0xFF uebergeben werden.  Eine exakte Dokumentation der möglichen Argumente kann LH Kombi E65 Teil 3.1 Kapittel "Diagnose" unter Befehl $30 "Lesen/Schreiben der AD Kanäle des MPC555" entnommen werden  KWP2000: $30 $91 InputOutputControlByLocalIdentifier Modus  : Default
- [STATUS_PPC_ADC_LESEN](#job-status-ppc-adc-lesen) - AD Kanaele des MPC555 auslesen Fuer Service-und Testzwecke  Dieser Service liefert die Rohwerte am ADC Converter Die Inkremente gehen dabei von 0 bis 1023 (dies entspricht 0..5V die am ADC anliegen)  KWP2000: $30,$91 -&gt; InputOutputControlByLocalIdentifier
- [STATUS_WASCHWASSER](#job-status-waschwasser) - AD Kanal mit Schalterfunktion des MPC555 lesen (Waschwasser) Fuer Service-und Testzwecke KWP2000: $30,$94,$01, $0D -&gt; InputOutputControlByLocalIdentifier
- [STATUS_KUEHLMITTELSTAND](#job-status-kuehlmittelstand) - AD Kanal mit Schalterfunktion des MPC555 lesen (Kueehlmittelstand) Fuer Service-und Testzwecke KWP2000: $30,$94,$01, $03 -&gt; InputOutputControlByLocalIdentifier
- [STEUERN_PPC_ADC_SCHREIBEN_AUS](#job-steuern-ppc-adc-schreiben-aus) - Wenn vorher der Job ADC_SCHREIBEN aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_LEUCHTE_ENDE gibt die Kontrolle wieder an das Kombi zurueck KWP2000: $30, $91, $00
- [GWSZ_RESET](#job-gwsz-reset) - GWSZ Korrektur-Offset aendern 
- [STATUS_ANGEZEIGTER_GWSZ](#job-status-angezeigter-gwsz) - liefert den angezeigten GWSZ 
- [STATUS_ABSOLUTER_GWSZ](#job-status-absoluter-gwsz) - liefert den absoluten GWSZ 
- [STEUERN_BOS_CODIERUNG](#job-steuern-bos-codierung) - BOS Codierung für alle einzelnen BOS Grössen 
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - GWSZ Korrektur-Offset aendern 
- [STEUERN_MOST_REDUZIERTE_SENDELEIST](#job-steuern-most-reduzierte-sendeleist) - Modus  : Fuer 1 [s] Reduzierte Sendeleistung auf Most Bus
- [BOS_RESET](#job-bos-reset) - BOS Daten Zuruecksetzen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default
- [STATUS_KLEMMEN](#job-status-klemmen) - Klemmenstati auslesen KWP2000: $21, $0E
- [STEUERGERAETE_RESET_DELAY](#job-steuergeraete-reset-delay) - Seuergeraete reset mit Delay ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [STEUERN_CBS_KM_PER_YEAR](#job-steuern-cbs-km-per-year) - Vorgabe Km/Jahr für CBS (ab CBS2) 
- [STEUERN_CBS_SC_CODIERUNG](#job-steuern-cbs-sc-codierung) - CBS Servicecall Enable/Disable Codierung 
- [STEUERN_CBS_SC_STATUS](#job-steuern-cbs-sc-status) - CBS Status Servicecall ändern 
- [STEUERN_CBS_SC_NOTIFIED](#job-steuern-cbs-sc-notified) - CBS Servicecall notification 
- [STATUS_QUARZABGLEICH](#job-status-quarzabgleich) - QUARZABGLEICH Status prüfen (Wert &gt;  860) und (Wert &lt;  32767) fehlerhaft (Wert &lt;= 860) und (Wert &gt;= 32767)  OKAY
- [STATUS_CBS_ERROR_MODE_EXT](#job-status-cbs-error-mode-ext) - gibt fehlende externe CBS-SG aus KWP2000 $22 $30 $18
- [STATUS_DEBUG_SLAVE](#job-status-debug-slave) - gibt Debug-Informationen des Slaves KWP2000 $21 $13 Nur fuer Entwickler
- [STATUS_DEBUG_MASTER](#job-status-debug-master) - gibt Debug-Informationen des Masters KWP2000 $21 $1$ Nur fuer Entwickler
- [STATUS_UHRZEIT_DATUM](#job-status-uhrzeit-datum) - Uhrzeit und Datum lesen KWP2000: $21, $8E
- [STEUERN_CCM_CAS205_EGS169_DIS](#job-steuern-ccm-cas205-egs169-dis) - CC-Meldung CAS ID 205 und EGS ID 169 disable 
- [STATUS_CHECKCONTROL_HISTORY](#job-status-checkcontrol-history) - CC-Meldungsspeicher aus Kombi lesen KWP2000: $21, $0F
- [STATUS_GLOBAL_KM](#job-status-global-km) - liest den GWSZ aus KI RAM, EEPROM & CAS
- [STATUS_RDUE_BLOCK_LESEN](#job-status-rdue-block-lesen) - gibt RDÜ Speicher aus KWP2000 $22 $30 $22 Nur fuer Entwickler
- [STATUS_CHECKCONTROL_HISTORY_CLEAR](#job-status-checkcontrol-history-clear) - CCM Histoty löschen KWP2000 $31 $21 Nur fuer Entwickler

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

<a id="job-cbs-info"></a>
### CBS_INFO

Ausgabe der CBS-Version

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ECU_NAME | string | Steuergeraetename |
| CBS_VERSION_TEXT | string | CBS Version im Klartext |
| CBS_VERSION_HEX | string | CBS Version als Wert |

<a id="job-cbs-daten-lesen"></a>
### CBS_DATEN_LESEN

CBS Daten auslesen (fuer CBS Version 1-3) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Hex-String |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| ANZ_CBS | int | Anzahl der CBS - Umfaenge im Steuergerät |
| ID_FN_BOS_MESS_WERT | int | CBS-Kennung als Zahl |
| ID_FN_BOS_MESS_HEX | string | CBS-Kennung als Hex-String |
| ID_FN_BOS_MESS_TEXT | string | table CbsKennung CBS_K CBS_K_TEXT CBS-Kennung im Klartext |
| RMMI_BOS_WERT | int | Restlaufleistung |
| RMMI_BOS_EINH | string | Information zur Restlaufleistung |
| ST_UN_BOS_WERT | int | Einheit Restlaufleistung als Zahl |
| ST_UN_BOS_HEX | string | Einheit Restlaufleistung als Hex-String |
| ST_UN_BOS_TEXT | string | Einheit Restlaufleistung im Klartext |
| COU_RSTG_BOS_MESS_WERT | int | Servicezaehler |
| COU_RSTG_BOS_MESS_EINH | string | Zaehler |
| AVAI_BOS_WERT | int | Verfügbarkeit in % |
| AVAI_BOS_EINH | string | % |
| AVAI_BOS_WERT_OEL | int | Verfügbarkeit OEL in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_CSF | int | Verfügbarkeit CSF in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_BATT | int | Verfügbarkeit BATT in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_VTG | int | Verfügbarkeit VTG in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_FILT | int | Verfügbarkeit FILT in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_BR_V | int | Verfügbarkeit BR_V in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_BR_H | int | Verfügbarkeit BR_H in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_BRFL | int | Verfügbarkeit BRFL in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_ZKRZ | int | Verfügbarkeit ZKRZ in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_SIC | int | Verfügbarkeit SIC in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_KFL | int | Verfügbarkeit KFL in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_UEB | int | Verfügbarkeit UEB in %, für Prüfablauf Bandende |
| AVAI_BOS_WERT_H2 | int | Verfuegbarkeit H2 in %, fuer Prüfablauf Bandende |
| ZIEL_MM_WERT | int | Ziel-Monat (HU/AU) |
| ZIEL_MM_EINH | string | Monat |
| ZIEL_YY_WERT | int | Ziel-Jahr (HU/AU) |
| ZIEL_YY_EINH | string | Jahr |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbs-reset"></a>
### CBS_RESET

CBS Daten Zuruecksetzen (fuer CBS Version 1-3) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BOS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, ZKrz, Sic, Kfl, TUV, AU, Ueb, H2 Werte externe Umfaenge: Oel, Br_v, Br_h, Filt, CSF, Batt, VTG Defaultwert: 0x00 (ungueltig) |
| BOS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, kein Rueckstellen: 255 Defaultwert: 100 |
| BOS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, Erhoehung der Anzahl um +1: 31 Defaultwert: 31 |
| BOS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter fuer Monat, keine Aenderung: 255 Defaultwert: 255 |
| BOS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter fuer Jahr, keine Aenderung: 255 Defaultwert: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
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

<a id="job-c-fg-lesen2"></a>
### C_FG_LESEN2

Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sg-reset-ohne-uhr-datum"></a>
### SG_RESET_OHNE_UHR_DATUM

Steuergeraete Reset ausloesen Uhrzeit und Datum bleibt dabei im Kombi erhalten KWP2000: $31, $20

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-checksumme"></a>
### C_CHECKSUMME

Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte  21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| OUT_BUFFER | binary | Als Result wird der gefuellte Binaerbuffer zurueckgegeben Der Binaerbuffer hat den Aufbau von BINAER_BUFFER |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-leuchte"></a>
### STEUERN_LEUCHTE

Kontrolleuchten einzeln ansteuern Fuer Service-und Testzwecke Es muessen immer sieben Argumente im Bereich von 0x00-0xFF uebergeben werden.  Im Kombi LH Teil 3.1 Kapitel "Diagnose" sind die Übergabeparameter des Diagnosebefehls $30 $07 ausführlich dokumentiert  KWP2000: $30 $07 InputOutputControlByLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | kann beliebig verwendet werden |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| BYTE4 | int | kann beliebig verwendet werden |
| BYTE5 | int | kann beliebig verwendet werden |
| BYTE6 | int | kann beliebig verwendet werden |
| BYTE7 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-leuchte-aus"></a>
### STEUERN_LEUCHTE_AUS

Wenn vorher der Job STEUERN_LEUCHTE aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_LEUCHTE_ENDE gibt die Kontrolle wieder an das Kombi zurueck KWP2000: $30, $23, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-blinker"></a>
### STEUERN_BLINKER

Blinker, zentrales Warnfeld, Ganganzeigenbeeleuchtung, Fernlicht ansteuern Fuer Service-und Testzwecke Es muessen immer alle zwei Argumente übergeben werden Nach Aufruf dieses Jobs muss der Vorgabemodus durch STEUERN_BLINKER_AUS beendet werden KWP2000: $30 $24  Beschreibung der Arumente: -------------------------- BYTE 0: High Nibble: 0 = beide Blinkkontrolleuchten aus 1 = Blinker links 2 = Blinker rechts 3 = Blinker rechts und links LOW Nibble:  1 = normales Blinken 2 = Blinker defekt (doppelte Blinkgeschwindigkeit) 3 = Doppelblinkimpuls Warnblinken Beispiel: BYTE 1= 0x12h bedeutet: Blinker links blinkt mit doppelter Geschwindigkeit  BYTE 1: 04h = Fernlicht ein 10h = zentr. Warnfeld rot ein 20h = zentr. Warnfeld gelb ein 40h = Beleuchtung Ganganzeigenfeld 80h = zentr. Warnfeld orange ein 00h = Fernlicht aus, zentr. Warnfeld aus, Beleuchtung Ganganzeigenfeld aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int |  |
| BYTE1 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-blinker-aus"></a>
### STEUERN_BLINKER_AUS

Wenn vorher der Job STEUERN_BLINKER aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_BLINKER_ENDE gibt die Kontrolle wieder an das Kombi zurueck KWP2000: $30, $24, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ppc-io-schreiben"></a>
### STEUERN_PPC_IO_SCHREIBEN

I/O Ports des MPC555 schreiben Fuer Service-und Testzwecke Es muessen immer alle drei Argumente im Bereich von 0x00-0xFF uebergeben werden. KWP2000: $30 InputOutputControlByLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Angabe des Ports (0..F) |
| BYTE1 | int | Wert der in das Port geschrieben werden kann |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-ppc-io-lesen"></a>
### STATUS_PPC_IO_LESEN

I/O Ports des MPC555 lesen Fuer Service-und Testzwecke  KWP2000: $30,$93,$01, $XX -&gt; InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PORT | int | Angabe des Ports (0..F) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DEBUGGER1_EIN | int |  |
| STAT_DEBUGGER2_EIN | int |  |
| STAT_OUT_CAN_TRANSCIVER1_EIN | int |  |
| STAT_OUT_CAN_TRANSCIVER2_EIN | int |  |
| STAT_IN_KOMBITASTE_EIN | int |  |
| STAT_OUT_PRG_SPANNUNG_INTERNES_FLASH_EIN | int |  |
| STAT_OUT_SELBSTHALTUNG_MPC_EIN | int |  |
| STAT_OUT_RESET_ASSP3_EIN | int |  |
| STAT_OUT_PRG_SPANNUNG_ASSP3_EIN | int |  |
| STAT_IN_TRANSFER_ACK_EIN | int |  |
| STAT_OUT_DISPLAY_ENABLE | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-ppc-io-schreiben-aus"></a>
### STEUERN_PPC_IO_SCHREIBEN_AUS

Wenn vorher der Job ADC_SCHREIBEN aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_LEUCHTE_ENDE gibt die Kontrolle wieder an das Kombi zurueck KWP2000: $30, $23, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selbsttest-ein"></a>
### STEUERN_SELBSTTEST_EIN

Schaltet den Selbttest ein KWP2000: $30, $26, $06

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selbsttest-aus"></a>
### STEUERN_SELBSTTEST_AUS

Schaltet den Selbsttest wieder aus KWP2000: $30, $23, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-testbitmap-anzeigen"></a>
### STEUERN_TESTBITMAP_ANZEIGEN

Anzeige des Testbitmaps im Kombi Zustand ist erst durch Sleep Modus beendet KWP2000: $30, $FD, $06

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Nummer des Testbitmaps anzeigen (0..0xFE) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tacho"></a>
### STEUERN_TACHO

Tacho auf einen bel winkel zwischen 0..300 Grad setzen KWP2000: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Winkelvorgabe in Grad (0..300 Grad) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-tacho-aus"></a>
### STEUERN_TACHO_AUS

Schaltet den Tacho-Vorgabemodus wieder aus KWP2000: $30, $20, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-drehzahl"></a>
### STEUERN_DREHZAHL

Tacho auf einen bel winkel zwischen 0..300 Grad setzen KWP2000: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Winkelvorgabe: z.B. 180 Grad -&gt; 180 * 17.77=0xC7E |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwor t von SG |

<a id="job-steuern-drehzahl-aus"></a>
### STEUERN_DREHZAHL_AUS

Schaltet den Tacho-Vorgabemodus wieder aus KWP2000: $30, $20, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tacho-lesen"></a>
### STATUS_TACHO_LESEN

gibt die Anzeigegeschwindigleit aus (Einheit km/h) KWP2000: $21, $05

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GESCHWINDIGKEIT_WERT | int | ZAHLENWERT von Geschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit von Geschwindigkeit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drehzahl-lesen"></a>
### STATUS_DREHZAHL_LESEN

gibt die Motordrehzahl aus (Einheit Umdrehungen/min) KWP2000: $21, $06

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DREHZAHL_WERT | int | Zahlenwert von Derehzahl |
| STAT_DREHZAHL_EINH | string | Einheit von Drehzahl |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lenkstock-lesen"></a>
### STATUS_LENKSTOCK_LESEN

gibt den Status des Lenkstockschalters aus KWP2000: $21, $07 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CC_TASTE_EIN | int | gueltige Rueckgabewerte fuer CC_TASTE '1' = CC Taste gedrückt '0' = CC Taste nicht gedrückt |
| STAT_BC_TASTE_EIN | int | gueltige Rueckgabewerte fuer BC_TASTE '1' = BC Taste gedrückt '0' = BC Taste nicht gedrückt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-checkcontrol-lesen"></a>
### STATUS_CHECKCONTROL_LESEN

gibt die ID Nummern der momentan aktiven CC-Meldungen aus KWP2000: $21, $09 Es bedeudet Rückgabewert ANZAHL     = Anzahl der aktiven Meldungen CC_Nummern = CC-Meldungen als Datenarray (pro Zahl 2 Byte)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL | int | Anzahl CC-Meldungen |
| STAT_CC_NUMMERN | binary | Eine Liste von Nummern der aktiven CC-Meldungen (pro Nummer 2 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-date-last-coding-session"></a>
### STATUS_DATE_LAST_CODING_SESSION

Datum, gibt an, wann das Kombi zum letzten mal codiert wurde (bei BMW) KWP2000: $21, $08

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TAG | int | Zahlenwert letztes Codierdatum Tag |
| STAT_MONAT | int | Zahlenwert letztes Codierdatum Tag |
| STAT_JAHR | int | Zahlenwert letzes Codierdatum |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tankinhalt-lesen"></a>
### STATUS_TANKINHALT_LESEN

Literwerte der Tank Hebelgeber links und rechts, Summerwert ungedämpft und gedämpft KWP2000: $21, $0A

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HEBELGEBER1_WERT | int | Zahlenwert Hebelgeber 1 |
| STAT_HEBELGEBER1_EINH | string | Einheit Hebelgeber rechts |
| STAT_HEBELGEBER2_WERT | int | Zahlenwert Hebelgeber links |
| STAT_HEBELGEBER2_EINH | string | Zahlenwert Hebelgeber 2 |
| STAT_SUMMENWERT_WERT | int | Zahlenwert Summe aus Hebelgeber links und rechts |
| STAT_SUMMENWERT_EINH | string | Einheit Summe aus Hebelgeber links und rechts |
| STAT_GEDAEMPFT_ANZ_WERT | int | Zahlenwert gedämpfter Summenwet aus Hebelgeber links und rechts |
| STAT_GEDAEMPFT_ANZ_EINH | string | Einheit gedämpfter Summenwet aus Hebelgeber links und rechts |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kl30-h-offset"></a>
### STATUS_KL30_H_OFFSET

Klemme 30 Stundenzaehler Offset auslesen KWP2000: $21, $0C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KL30_H_OFFSET_WERT | long | ZAHLENWERT von KL30 Stundenzaehler Offset |
| STAT_KL30_H_OFFSET_EINH | string | Einheit von KL30 Stundenzaehler Offset |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kl30-h-offset"></a>
### STEUERN_KL30_H_OFFSET

Klemme 30 Stundenzaehler Offset schreiben KWP2000: $3B, $0C

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KL30_H_OFFSET_WERT | long | ZAHLENWERT von KL30 Stundenzaehler Offset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kl30-h-counter"></a>
### STEUERN_KL30_H_COUNTER

Klemme 30 Stundenzaehler schreiben KWP2000: $3B, $0D

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KL30_H_WERT | long | ZAHLENWERT von KL30 Stundenzaehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-calc-kl30-h-offset"></a>
### CALC_KL30_H_OFFSET

Klemme 30 Stundenzaehler Offset ab dem momentanen Datum berechnen Dieser Job wird nur in der BMW-Fertigung im Rahmen der Codierung aufgerufen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| KL30_H_OFFSET_WERT | string | ZAHLENWERT von KL30 Stundenzaehler Offset als String in Hex Darstellung |
| KL30_H_OFFSET_EINH | string | EINHEIT von KL30 Stundenzaehler Offset (String in Hex Darstellung) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-set-kl30-offset2akt-date"></a>
### SET_KL30_OFFSET2AKT_DATE

Berechnet den Klemme 30 Stundenzaehler Offset ab dem momentanen Datum und schreibt diesen in das EEPROM des KOMBI BOS funtioniert nur richtig, wenn der KL30_H_OFFSET richtig gesetzt ist. Daher sollte der Job immer aufgerufen werden wenn das Fahrzeug an den Taster angeschlossen wird KWP2000: $3B, $0C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-uhrzeit-datum-stellen"></a>
### UHRZEIT_DATUM_STELLEN

Uhrzeit auf das aktuelle Datum stellen KWP2000: $3B, $0E

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kl30-h-zaehler"></a>
### STATUS_KL30_H_ZAEHLER

Klemme 30 Stundenzaehler auslesen KWP2000: $21, $0D

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KL30_H_ZAEHLER_WERT | long | ZAHLENWERT von KL30 Stundenzaehler |
| STAT_KL30_H_ZAEHLER_EINH | string | Einheit von KL30 Stundenzaehler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betriebsdaten-lesen"></a>
### STATUS_BETRIEBSDATEN_LESEN

liest ausgewählte Daten aus CBS Betriebsdaten aus KWP2000 $21 $B1 bis $BE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | CBS ID 1..30h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ID | int | CBS ID zu der die Betriebsdaten gehöhren |
| STAT_EINHEIT_ID | int | 0 bis 2 |
| STAT_FARB_ID | int | 0 bis 3 |
| STAT_UNIT_ABSTAND_ID | int | 0 bis 3 |
| STAT_WERT_ABSTAND_ID | int | -63 bis +63 |
| STAT_WERT_ID | int | -32767 bis 32767 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betriebsdaten-header"></a>
### STATUS_BETRIEBSDATEN_HEADER

gibt den KM Stand aus CBS Betriebsdaten Header aus KWP2000 $21 $B0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AKT_KM_STAND_WERT | long | km-Stand mit Auflösung von 20 km |
| STAT_AKT_KM_STAND_EINH | string |  |
| STAT_BLOCK_KM_PER_WEEK | binary | Block KM/Woche aus CBS Betriebsdaten Header |
| STAT_TAGESZAEHLER_WERT | long | Tageszähler (Kl.30 Stundenzähler + Offset) |
| STAT_TAGESZAEHLER_EINH | string |  |
| STAT_AVKM_W | long | Kilometer/Woche Quartalswert |
| STAT_AVKM_START | long | Kilometer/Woche Startwert (Kodierung) |
| STAT_AKTUELLES_DATUM_WERT | long | Tageszähler abgeleitet vom Datum |
| STAT_AKTUELLES_DATUM_EINH | string |  |
| STAT_MODE_WERT | int | CBS-Mode |
| STAT_MODE_TEXT | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zeitstrahl"></a>
### STATUS_ZEITSTRAHL

gibt BOS Daten für den Annahmerechner in der Reihenfolge Header BOS Umpfänge, CC Umpfänge KWP2000 $21 $C0 Für die exakte Beschreiung der BOS Zeitstrahldaten siehe LH Teil 3 Kapitel Diagnose, Beschreibung zu $21

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BLOCK_C0 | binary | Block 0 der BOS Zeitstrahldaten |
| STAT_BLOCK_C1 | binary | Block 1 der BOS Zeitstrahldaten |
| STAT_BLOCK_C2 | binary | Block 2 der BOS Zeitstrahldaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ppc-adc-schreiben"></a>
### STEUERN_PPC_ADC_SCHREIBEN

AD Kanaele des MPC555 schreiben Fuer Service-und Testzwecke  Es muessen immer alle Argumente im Bereich von 0x00-0xFF uebergeben werden.  Eine exakte Dokumentation der möglichen Argumente kann LH Kombi E65 Teil 3.1 Kapittel "Diagnose" unter Befehl $30 "Lesen/Schreiben der AD Kanäle des MPC555" entnommen werden  KWP2000: $30 $91 InputOutputControlByLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KANAL | int | Angabe des ADC Ports (0..E) |
| MSB | int | MSB-Wert der in den KANAL geschrieben werden kann |
| LSB | int | LSB-Wert der in den KANAL geschrieben werden kann |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-ppc-adc-lesen"></a>
### STATUS_PPC_ADC_LESEN

AD Kanaele des MPC555 auslesen Fuer Service-und Testzwecke  Dieser Service liefert die Rohwerte am ADC Converter Die Inkremente gehen dabei von 0 bis 1023 (dies entspricht 0..5V die am ADC anliegen)  KWP2000: $30,$91 -&gt; InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TANK_HEBELGEBER1_WERT | int | Zahlenwert Hebelgeber1 |
| STAT_TANK_HEBELGEBER1_EINH | string | Einheit Hebelgeber 1 |
| STAT_TANK_HEBELGEBER2_WERT | int | Zahlenwert Hebelgeber 2 |
| STAT_TANK_HEBELGEBER2_EINH | string | Einheit Hebelgeber 2 |
| STAT_A_TEMP_WERT | int | Zahlenwert Aussentemperatur |
| STAT_A_TEMP_EINH | string | Einheit Aussentemperatur |
| STAT_KUEHLMITTELSTAND_WERT | int | Zahlenwert Kühlmittlstand |
| STAT_KUEHLMITTELSTAND_EINH | string | Einheit Kühlmittelstand |
| STAT_VERSORGUNGS_SPANNUNG_KL30_WERT | int | Zahlenwert von Versogungsspannung |
| STAT_VERSORGUNGS_SPANNUNG_KL30_EINH | string | Einheit von Versorgungsspannung |
| STAT_TEMP_GLAS_WERT | int |  |
| STAT_TEMP_GLAS_EINH | string |  |
| STAT_FOTOTRANSISTOR_WERT | int |  |
| STAT_FOTOTRANSISTOR_EINH | string |  |
| STAT_TEMPERATUR_LAMPE_WERT | int |  |
| STAT_TEMPERATUR_LAMPE_EINH | string |  |
| STAT_GANG_ANZ_P_WERT | int |  |
| STAT_GANG_ANZ_P_EINH | string |  |
| STAT_GANG_ANZ_R_WERT | int |  |
| STAT_GANG_ANZ_R_EINH | string |  |
| STAT_GANG_ANZ_D_WERT | int |  |
| STAT_GANG_ANZ_D_EINH | string |  |
| STAT_GANG_ANZ_N_WERT | int |  |
| STAT_GANG_ANZ_N_EINH | string |  |
| STAT_WASCHWASSER_WERT | int |  |
| STAT_WASCHWASSER_EINH | string |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-waschwasser"></a>
### STATUS_WASCHWASSER

AD Kanal mit Schalterfunktion des MPC555 lesen (Waschwasser) Fuer Service-und Testzwecke KWP2000: $30,$94,$01, $0D -&gt; InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WASCHWASSER_VOLL | int | 00 = Leer, 01 = Voll |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-kuehlmittelstand"></a>
### STATUS_KUEHLMITTELSTAND

AD Kanal mit Schalterfunktion des MPC555 lesen (Kueehlmittelstand) Fuer Service-und Testzwecke KWP2000: $30,$94,$01, $03 -&gt; InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KUEHLMITTELSTAND_VOLL | int | 00 = Leer, 01 = Voll |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-ppc-adc-schreiben-aus"></a>
### STEUERN_PPC_ADC_SCHREIBEN_AUS

Wenn vorher der Job ADC_SCHREIBEN aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_LEUCHTE_ENDE gibt die Kontrolle wieder an das Kombi zurueck KWP2000: $30, $91, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-gwsz-reset"></a>
### GWSZ_RESET

GWSZ Korrektur-Offset aendern 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-angezeigter-gwsz"></a>
### STATUS_ANGEZEIGTER_GWSZ

liefert den angezeigten GWSZ 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GWSZ | long | Angezeigter Kilometerstand |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-absoluter-gwsz"></a>
### STATUS_ABSOLUTER_GWSZ

liefert den absoluten GWSZ 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GWSZ | long | Absoluter Kilometerstand |
| STAT_KM | string | Absoluter Kilometerstand grösser oder kleiner als 255 km |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-bos-codierung"></a>
### STEUERN_BOS_CODIERUNG

BOS Codierung für alle einzelnen BOS Grössen 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BOS_ID | int | BOS ID 1..30h |
| BOS_CODIERUNG | int | Codierung passend zu BOS_ID, 0=Anzeige, 1=Sperre, 2=Erprobung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

GWSZ Korrektur-Offset aendern 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_NR | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CODIERDATENBLOCK | binary | Enthält den Codierdatenblock |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-most-reduzierte-sendeleist"></a>
### STEUERN_MOST_REDUZIERTE_SENDELEIST

Modus  : Fuer 1 [s] Reduzierte Sendeleistung auf Most Bus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-bos-reset"></a>
### BOS_RESET

BOS Daten Zuruecksetzen KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BOS_KENNUNG | string | gewuenschte BOS-Kennung table BosKennung BOS_K BOS_K_TEXT Werte: Oel, Br_v, Brfl, Filt, Batt, Br_h, ZKrz, Sic, Kfl, TUV, AU Defaultwert: Oel |
| BOS_VERFUEGBARKEIT | string | gewuenschte Verfuegbarkeit in Prozent: 0-200 Schalter, kein Rueckstellen: 255 Defaultwert: 100 |
| BOS_ANZAHL_SERVICE | string | Anzahl der durchgefuehrten Services: 0-30 Schalter, keine Aenderung: 31 Defaultwert: 31 |
| BOS_ZIEL_MONAT | string | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter fuer Monat, keine AEnderung: 255 Defaultwert: 255 |
| BOS_ZIEL_JAHR | string | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter fuer Jahr, keine AEnderung: 255 Defaultwert: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klemmen"></a>
### STATUS_KLEMMEN

Klemmenstati auslesen KWP2000: $21, $0E

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLR_WERT | char | ZAHLENWERT von Klemmenstatus KL R |
| STAT_KL15_WERT | char | ZAHLENWERT von Klemmenstatus KL 15 |
| STAT_KL50_WERT | char | ZAHLENWERT von Klemmenstatus KL50 |
| STAT_KLR_EINH | string | Einheit von Klemmenstatus KL R |
| STAT_KL15_EINH | string | Einheit von Klemmenstatus KL 15 |
| STAT_KL50_EINH | string | Einheit von Klemmenstatus KL50 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-reset-delay"></a>
### STEUERGERAETE_RESET_DELAY

Seuergeraete reset mit Delay ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DELAY | long | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter fuer Jahr, keine AEnderung: 255 Defaultwert: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cbs-km-per-year"></a>
### STEUERN_CBS_KM_PER_YEAR

Vorgabe Km/Jahr für CBS (ab CBS2) 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KM_VALUE | int | CBS kilometervorgabe (Gültige Grössen: 0... 255) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-cbs-sc-codierung"></a>
### STEUERN_CBS_SC_CODIERUNG

CBS Servicecall Enable/Disable Codierung 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_ID | int | CBS ID 1..30h |
| CBS_CODIERUNG | int | Codierung passend zu CBS_ID, 0=SC inaktiv, 1=SC Aktiv |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-cbs-sc-status"></a>
### STEUERN_CBS_SC_STATUS

CBS Status Servicecall ändern 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SC_STATUS | int | 0x00 = 0  Idle 0x01 = 1  Pending 0x02 = 2  Successfull 0x03 = 3  Error |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-cbs-sc-notified"></a>
### STEUERN_CBS_SC_NOTIFIED

CBS Servicecall notification 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_ID | int | CBS ID 1..30h |
| CBS_CODIERUNG | int | Codierung passend zu CBS_ID, 0=SC notified Inaktiv, 1=SC Notified Aktiv |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-quarzabgleich"></a>
### STATUS_QUARZABGLEICH

QUARZABGLEICH Status prüfen (Wert &gt;  860) und (Wert &lt;  32767) fehlerhaft (Wert &lt;= 860) und (Wert &gt;= 32767)  OKAY

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ABGLEICH | string | Quarzabgleich grösser als 860 und kleiner als 32767 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-cbs-error-mode-ext"></a>
### STATUS_CBS_ERROR_MODE_EXT

gibt fehlende externe CBS-SG aus KWP2000 $22 $30 $18

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ERROR_MODE_WERT | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-debug-slave"></a>
### STATUS_DEBUG_SLAVE

gibt Debug-Informationen des Slaves KWP2000 $21 $13 Nur fuer Entwickler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BLOCK_DEBUG_SLAVE | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-debug-master"></a>
### STATUS_DEBUG_MASTER

gibt Debug-Informationen des Masters KWP2000 $21 $1$ Nur fuer Entwickler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BLOCK_DEBUG_MASTER | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-uhrzeit-datum"></a>
### STATUS_UHRZEIT_DATUM

Uhrzeit und Datum lesen KWP2000: $21, $8E

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HOUR | char | Uhrzeit Stunde |
| STAT_MINUTE | char | Uhrzeit Minute |
| STAT_SECOND | char | Uhrzeit Sekunde |
| STAT_DAY | char | Datum Tag |
| STAT_MONTH | char | Datum Monat |
| STAT_YEAR | int | Datum Jahr |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ccm-cas205-egs169-dis"></a>
### STEUERN_CCM_CAS205_EGS169_DIS

CC-Meldung CAS ID 205 und EGS ID 169 disable 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-checkcontrol-history"></a>
### STATUS_CHECKCONTROL_HISTORY

CC-Meldungsspeicher aus Kombi lesen KWP2000: $21, $0F

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CC_ID | int | ID der CC-Meldung |
| STAT_CC_ID_TEXT | string | CC-Text |
| STAT_GWSZ_STAND_WERT | unsigned long | Kilometerstand beim Auftreten der CC-Meldung Aufloesung: 8km HINWEIS: als Wert wird maximal 524280 ausgegeben. |
| STAT_GWSZ_STAND_EINH | string | Einheit des GWSZ-Standes HINWEIS: immer km |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-global-km"></a>
### STATUS_GLOBAL_KM

liest den GWSZ aus KI RAM, EEPROM & CAS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GWSZ_RAM | long | Kilometerstand aus KI RAM OHNE Offset |
| STAT_GWSZ_EEPROM | long | Kilometerstand aus KI EEPROM |
| STAT_GWSZ_CAS | long | Kilometerstand aus CAS |
| STAT_GWSZ_EINH | string | immer "km" |
| _TEL_ANTWORT | binary | Antwort von SG |
| _TEL_ANTWORT2 | binary | Antwort von SG auf 2. Anfrage |
| _TEL_ANTWORT3 | binary | Antwort von CAS_SG |

<a id="job-status-rdue-block-lesen"></a>
### STATUS_RDUE_BLOCK_LESEN

gibt RDÜ Speicher aus KWP2000 $22 $30 $22 Nur fuer Entwickler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BLOCK_RDUE | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-checkcontrol-history-clear"></a>
### STATUS_CHECKCONTROL_HISTORY_CLEAR

CCM Histoty löschen KWP2000 $31 $21 Nur fuer Entwickler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CCM_CLEAR | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (81 × 2)
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
- [CBSKENNUNG](#table-cbskennung) (17 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (61 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (19 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (32 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (10 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (4 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (10 × 9)
- [RDA](#table-rda) (1 × 13)
- [MOST_NAK](#table-most-nak) (1 × 5)
- [MOST_NO_ANSWER](#table-most-no-answer) (1 × 5)
- [ID_ALIVE_CC](#table-id-alive-cc) (1 × 4)
- [ID_ALIVE_KOMPL](#table-id-alive-kompl) (1 × 4)
- [ID_ARS_SFY](#table-id-ars-sfy) (1 × 5)
- [ID_ALIVE](#table-id-alive) (1 × 3)
- [BOSKENNUNG](#table-boskennung) (11 × 3)
- [CCM_TEXT_TABELLE](#table-ccm-text-tabelle) (378 × 2)

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

Dimensions: 81 rows × 2 columns

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
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
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

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 17 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x04 | Filt | Mikrofilter |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x07 | CSF | Dieselpartikelfilter |
| 0x08 | Batt | Batterie |
| 0x09 | VTG | Verteilergetriebeoel |
| 0x10 | ZKrz | Zuendkerzen |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x12 | Kfl | Kuehlfluessigkeit |
| 0x13 | H2 | H2-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x16 | DAD | Additiv fuer Partikelfilter |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |
| 0x0A | ZKrz_a | Zuendkerzen adaptiv |

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

Dimensions: 61 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x930E | GANGANZEIGE_P |
| 0x930F | GANGANZEIGE_N |
| 0x9310 | GANGANZEIGE_D |
| 0x9311 | GANGANZEIGE_R |
| 0x9313 | TEMPERATURFÜHLER_LCD |
| 0x9315 | GWSZ_FEHLER_CAS_ODER_KOMBI |
| 0x9316 | GWSZ_FEHLER_EEPROM_KOMBI |
| 0x9317 | EEPROM: CHECKSUM ERROR CODING DATA BMW |
| 0x9318 | VMC_COMMUNICATION_ERROR |
| 0x9319 | HEBELGEBER_RECHTS |
| 0x9312 | Energiesparmode aktiv. |
| 0x931A | HEBELGEBER_LINKS |
| 0x931B | AUSSENTEMPERATUR |
| 0x931C | KURZSCHUSS_DISPLAYHEIZUNG |
| 0x931D | BORDNETZSPANNUNG, UEBERSPANNUNG ODER UNTERSPANNUNG |
| 0x931E | EEPROM: CHECKSUM ERROR CODING DATA VDO |
| 0x9327 | ZGM_ALIVE_ERROR |
| 0xA3A8 | CAN_NO_ID_ERROR |
| 0xA3A9 | CAN_ID_1EE_ERROR_Ausfall_Botschaft_LSS |
| 0xA3AA | CAN_ID_1D2_ERROR_Ausfall_Botschaft_Getriebedaten |
| 0xA3AB | CAN_ID_190_ERROR_Ausfall_Botschaft_Anzeige_ACC |
| 0xA3AC | CAN_ID_1A6_ERROR_Ausfall_Botschaft_Wegstrecke |
| 0xA3AD | CAN_ID_1D0_ERROR_Ausfall_Botschaft_Motordaten |
| 0xA3AE | CAN_ID_0AA_ERROR_Ausfall_Botschaft_Drehmoment3 |
| 0xA3AF | CAN_ID_200_ERROR_Ausfall_Botschaft_Regelgeschw_Stufentempomat |
| 0xA3B0 | CAN_ID_202_ERROR_Ausfall_Botschaft_Dimmung |
| 0xA3B1 | CAN_ID_1F6_ERROR_Ausfall_Botschaft_Blinken |
| 0xA3B2 | CAN_ID_130_ERROR_Ausfall_Botschaft_Klemmenstatus |
| 0xA3B3 | CAN_ID_0BE_ERROR_Ausfall_Botschaft_ARS_SSY_Alive_Zaehler |
| 0xA3B4 | CAN_ID_21A_ERROR_Ausfall_Botschaft_Lampenzustand |
| 0xA3B5 | CAN_ID_3B4_ERROR_Ausfall_Botschaft_Powermanagement |
| 0xA3B6 | CAN_ID_394_ERROR_Ausfall_Botschaft_RDA_Anfrage_Datenablage |
| 0xA3B7 | CAN_ID_2E4_ERROR_Ausfall_Botschaft_Status_Anhaenger |
| 0xA3B8 | CAN_ID_326_ERROR_Ausfall_Botschaft_Status_Daempferprogramm |
| 0xA3B9 | CAN_ID_19E_ERROR_Ausfall_Botschaft_Status_DSC |
| 0xA3BA | CAN_ID_0AE_ERROR_Ausfall_Botschaft_Alive_EMF |
| 0xA3BB | CAN_ID_2FC_ERROR_Ausfall_Botschaft_ZV_Klappenzustand |
| 0xA3BC | NO_ANSWER_TO_REQUEST (580h+60h) |
| 0xA3BD | CAN_ID_0C0_ERROR_Ausfall_Botschaft_Alive_ZGM |
| 0xA548 | CAN_ID_1A0_ERROR_Ausfall_Botschaft_Geschwindigkeit |
| 0xA54A | CAN_ID_5C0_ERROR_CAS_Checksumme_Wegstrecke |
| 0xA54C | CAN_ID_2FF_ERROR_Ausfall_Botschaft_CleanEnergy |
| 0xA3BE | CAS_ALIVE_ERROR |
| 0xA3BF | CIM_ALIVE_ERROR |
| 0xA3C0 | AHM_ALIVE_ERROR |
| 0xA3C1 | LSZ_ALIVE_ERROR |
| 0xA3C2 | POWERMODUL_ALIVE_ERROR |
| 0xA3C3 | RDC_ALIVE_ERROR |
| 0xA3C4 | SECURITY1_ALIVE_ERROR |
| 0xA3C5 | SECURITY2_ALIVE_ERROR |
| 0xA3C6 | WISCHERMODUL_ALIVE_ERROR |
| 0xA3C7 | LUFTFEDER_ALIVE_ERROR |
| 0xE104 | CAN LOW ERROR |
| 0xE105 | CAN HIGH ERROR |
| 0xE106 | GROUND SHIFT ERROR |
| 0xE107 | CAN BUS OFF |
| 0xE10C | Empfaenger hat eine Nachricht nicht abgenommen (Error_NAK) |
| 0xE10E | Obwohl Shutdown (Execute) geschickt wurde ging das Licht nicht aus. (Error_Light_Not_Off). |
| 0xE110 | Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose). |
| 0xE111 | Lange und/oder haeufige Unlocks (Error_Unlock_Long). |
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
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 19 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x931E | 0x01 | 0x02 | - | - |
| 0x9317 | 0x01 | 0x02 | - | - |
| 0xE107 | 0x01 | 0xFE | 0xFD | 0xFF |
| 0xE10C | 0x01 | 0xFE | MOST_NAK | - |
| 0xE10E | 0x01 | 0xFE | 0xFF | 0xFD |
| 0xE110 | 0x01 | 0xFE | 0x07 | 0xFF |
| 0xE111 | 0x01 | 0xFE | 0xFF | 0xFD |
| 0xA3AA | 0x01 | ID_ALIVE_KOMPL | - | - |
| 0xA3AB | 0x01 | ID_ALIVE_CC | - | - |
| 0xA3AC | 0x01 | ID_ALIVE | - | - |
| 0xA3AD | 0x01 | ID_ALIVE | - | - |
| 0xA3B3 | 0x01 | ID_ARS_SFY | - | - |
| 0xA3B6 | RDA | - | - | - |
| 0xA3B8 | 0x01 | ID_ALIVE | - | - |
| 0xA3B9 | 0x01 | ID_ALIVE | - | - |
| 0xA3BA | 0x01 | ID_ALIVE | - | - |
| 0xA3BC | 0x1A | - | - | - |
| 0xA3BD | 0x01 | ID_ALIVE | - | - |
| default | 0x01 | 0xFE | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 32 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | BORDNETZSPANNUNG | VOLT | - | unsigned char | - | 1 | 10 | 0 |
| 0x02 | Tachometerfunktion betroffen | 0/1 | - | 0x01 | - | - | - | - |
| 0x03 | DEVICE ADRESSE NAK | HEX | - | unsigned int | - | 1 | 1 | 0 |
| 0x04 | FUNCTION BLOCK | HEX | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | INSTANCE ID | HEX | - | unsigned char | - | 1 | 1 | 0 |
| 0x06 | FUNCTION ID | HEX | - | unsigned int | - | 1 | 1 | 0 |
| 0x07 | POSITION NODE REGISTER | HEX | - | unsigned int | - | 1 | 1 | 0 |
| 0x08 | DEVICE ADRESSE | HEX | - | unsigned int | - | 1 | 1 | 0 |
| 0x09 | RESET MIT RAM ERHALT | 0/1 | - | 0x01 | - | - | - | - |
| 0x0A | NO ID | 0/1 | - | 0x01 | - | - | - | - |
| 0x0B | ALIVE ERROR | 0/1 | - | 0x02 | - | - | - | - |
| 0x0C | CHECKSUM ERROR | 0/1 | - | 0x04 | - | - | - | - |
| 0x0D | KOMPLEMENT FEHLER | 0/1 | - | 0x04 | - | - | - | - |
| 0x0E | ARS ALIVE ERROR | 0/1 | - | 0x10 | - | - | - | - |
| 0x0F | SFY ALIVE ERROR | 0/1 | - | 0x20 | - | - | - | - |
| 0x10 | 00h GWSZ | 0/1 | - | 0x0001 | - | - | - | - |
| 0x11 | 01h ZUENDKERZEN | 0/1 | - | 0x0002 | - | - | - | - |
| 0x12 | 02h FAHRZEUGCHECK | 0/1 | - | 0x0004 | - | - | - | - |
| 0x13 | 03h BREMSFLÜSSIGKEIT | 0/1 | - | 0x0008 | - | - | - | - |
| 0x14 | 04h KUEHLWASSER | 0/1 | - | 0x0010 | - | - | - | - |
| 0x15 | 05h HU | 0/1 | - | 0x0020 | - | - | - | - |
| 0x16 | 06h AU | 0/1 | - | 0x0040 | - | - | - | - |
| 0x17 | 07h RESERVE_1 | 0/1 | - | 0x0080 | - | - | - | - |
| 0x18 | 08h RESERVE_2 | 0/1 | - | 0x0100 | - | - | - | - |
| 0x19 | 0Dh SERVICE_CALL | 0/1 | - | 0x2000 | - | - | - | - |
| 0x20 | 0Eh KM/WOCHE | 0/1 | - | 0x4000 | - | - | - | - |
| 0x21 | 0Fh STUNDENZAEHLER/OFFSET | 0/1 | - | 0x8000 | - | - | - | - |
| 0x1A | ANFRAGE ID | HEX | - | unsigned int | - | 1 | 1 | 0 |
| 0xFE | OHNE BEDEUTUNG | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0xFD | OHNE BEDEUTUNG | 1 | - | unsigned int | - | 1 | 1 | 0 |
| 0xFF | OHNE BEDEUTUNG | 1 | - | signed long | - | 1 | 1 | 0 |
| 0xXY | UNBEKANNTE UW | 1 | - | signed long | - | 1 | 1 | 0 |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 10 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9308 | Device bekam Reset (Error_Reset). |
| 0x9309 | Bis zum Auftreten des Timeouts konnte kein Licht bzw. kein stabiler Lock erkannt werden (Error_NSInit_Timeout). |
| 0x930A | Device ist im Zustand Normal Operation und das Licht am Eingang geht ohne Vorankuendigung aus (Error_Sudden_light_off). |
| 0x930B | Anfragendes Device bekommt keine Antwort obwohl Partner vorhanden ist (Error_Device_No_Answer). |
| 0x930C | Kurze Unlocks (Error_unlock_Short). |
| 0x930D | Kein Broadcast Configuration.Status vom Networkmaster erhalten (Error_t_CfgStatus). |
| 0x930E | Weckendes Device hat erfolglos versucht das Netzwerk zu wecken (Error_WakeUp_Failed). |
| 0x930F | Ein Device hat im laufenden Betrieb seinen Bypass All geschlossen (Error_NCE). |
| 0x9310 | Empfaenger hat eine Nachricht nicht abgenommen (Error_NAK). |
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
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 4 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9308 | 0x01 | 0x02 | 0xFD | 0xFF |
| 0x930B | 0x01 | 0xFE | MOST_NO_ANSWER | - |
| 0x9310 | 0x01 | 0xFE | MOST_NO_ANSWER | - |
| default | 0x01 | 0xFE | 0xFD | 0xFF |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 10 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | BORDNETZSPANNUNG | VOLT | - | unsigned char | - | 1 | 10 | 0 |
| 0x02 | RESET MIT RAM ERHALT | 0/1 | - | 0x01 | - | - | - | - |
| 0x08 | DEVICE ADRESSE | HEX | - | unsigned int | - | 1 | 1 | 0 |
| 0x04 | FUNCTION BLOCK | HEX | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | INSTANCE ID | HEX | - | unsigned char | - | 1 | 1 | 0 |
| 0x06 | FUNCTION ID | HEX | - | unsigned int | - | 1 | 1 | 0 |
| 0xFF | OHNE BEDEUTUNG | 1 | - | signed long | - | 1 | 1 | 0 |
| 0xFE | OHNE BEDEUTUNG | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0xFD | OHNE BEDEUTUNG | 1 | - | unsigned int | - | 1 | 1 | 0 |
| 0xXY | UNBEKANNTE UW | 1 | - | signed long | - | 1 | 1 | 0 |

<a id="table-rda"></a>
### RDA

Dimensions: 1 rows × 13 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 12 | 0x10 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 | 0x16 | 0x17 | 0x18 | 0x19 | 0x20 | 0x21 |

<a id="table-most-nak"></a>
### MOST_NAK

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x03 | 0x04 | 0x05 | 0x06 |

<a id="table-most-no-answer"></a>
### MOST_NO_ANSWER

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x08 | 0x04 | 0x05 | 0x06 |

<a id="table-id-alive-cc"></a>
### ID_ALIVE_CC

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x0A | 0x0B | 0x0C |

<a id="table-id-alive-kompl"></a>
### ID_ALIVE_KOMPL

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x0A | 0x0B | 0x0D |

<a id="table-id-ars-sfy"></a>
### ID_ARS_SFY

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x0A | 0x0B | 0x0E | 0x0F |

<a id="table-id-alive"></a>
### ID_ALIVE

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x0A | 0x0B |

<a id="table-boskennung"></a>
### BOSKENNUNG

Dimensions: 11 rows × 3 columns

| NR | BOS_K | BOS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Oelqualitaet |
| 0x02 | Br_v | Bremsbelagverschleiss vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x04 | Filt | Mikrofilter |
| 0x05 | Batt | Batteriezustand |
| 0x06 | Br_h | Bremsbelagverschleiss hinten |
| 0x10 | ZKrz | Zuendkerzen |
| 0x11 | Sic | Sichtpruefung |
| 0x12 | Kfl | Kuehlfluessigkeit |
| 0x20 | TUV | TUEV |
| 0x21 | AU | AU |

<a id="table-ccm-text-tabelle"></a>
### CCM_TEXT_TABELLE

Dimensions: 378 rows × 2 columns

| CC_NR | CC_TEXT |
| --- | --- |
| 0 | Keine Störungen |
| 1 | ACC deaktiviert! Gemäßigt fahren |
| 2 | ACC deaktiviert! Auf Abstand achten |
| 3 | ACC ausgefallen! Auf Abstand achten |
| 4 | Anhänger, Standlicht links! Prüfen |
| 5 | Anhänger, Standlicht rechts! Prüfen |
| 6 | Anhänger, Blinker links! Prüfen |
| 7 | Anhänger, Blinker rechts! Prüfen |
| 8 | Anhänger, Brems- leuchten! Prüfen |
| 9 | Anhänger, Nebel- leuchte! Prüfen |
| 10 | Dynamic Drive gestört! |
| 11 | Lenkung! |
| 12 | Dynamic Drive ausgefallen! |
| 13 | Fernbedienung identifiziert! |
| 14 | Tür offen! |
| 15 | Tür offen! |
| 16 | Tür offen! |
| 17 | Tür offen! |
| 18 | Motorhaube offen! |
| 19 | Kofferraum offen! |
| 20 | Trigger Start! |
| 21 | Zündung! Vor- sichtig anhalten |
| 22 | Anlasser! Motor ggf. nicht abstellen |
| 23 | Trigger Stop! |
| 24 | DBC ausgefallen! Gemäßigt fahren |
| 25 | Vorglühen! Bitte warten |
| 26 | Geschwindigkeits- regelung! |
| 27 | Motorölstand auf Minimum! |
| 28 | Motorölstand unter Min.! Nachfüllen |
| 29 | Motorstörung! Leistungsabfall |
| 30 | Motor! Vorsichtig anhalten |
| 31 | Erhöhte Emissionen! |
| 32 | Tankverschluss schließen |
| 33 | Motorstörung! Gemäßigt fahren |
| 34 |  |
| 35 | DSC ausgefallen! Gemäßigt fahren |
| 36 | DSC deaktiviert! |
| 37 | Trigger |
| 38 | Falscher Schlüssel! |
| 39 | Motor überhitzt! Vor- sichtig anhalten |
| 40 | Zum Motor Starten Bremse treten |
| 41 | Service fällig! |
| 42 | Brems-/Fahrstabilität! Gemäßigt fahren |
| 43 | Stoßdämpferregelung ausgefallen! |
| 44 | #kein Datensatz# |
| 45 | Niveauregulierung ausgefallen! |
| 46 | Bitte angurten |
| 47 | Servotronic gestört! Gemäßigt fahren |
| 48 |  |
| 49 | Partikelfilter gestört! |
| 50 | Reifen Pannen Anzeige ausgef.! |
| 51 | Parkbremse überhitzt! |
| 52 | Parkbremse ausgefallen! |
| 53 | Automatic Hold gestört! |
| 54 | Parkbremse gestört! |
| 55 | Parkbremse lösen |
| 56 |  |
| 57 |  |
| 58 |  |
| 59 | ACC deaktiviert! Parkbremse |
| 60 | Geschwindigkeits- anzeige gestört! |
| 61 | Reichweite %s |
| 62 | Tempolimit überschritten |
| 63 | Reifenpanne! |
| 64 | Code eingeben |
| 65 | Akku in Fernbedie- nung! Laden |
| 66 | Fernbedienung reagiert nicht! |
| 67 | Fernbedienung Batterie leer! |
| 68 | Batterien Fernbed. Standfunktionen! |
| 69 | ACC deaktiviert! Auf Abstand achten |
| 70 | Servotronic ausgefallen! |
| 71 | Bremsbeläge ersetzen |
| 72 | Kindersicherung ausgefallen! |
| 73 | #kein Datensatz# |
| 74 | Bremsflüssigkeit! Vor- sichtig anhalten |
| 75 | Anhängerelektrik ausgefallen! |
| 76 |  |
| 77 |  |
| 78 | Geschwindigkeitslimit überschritten! |
| 79 | Außentemperatur %s |
| 80 |  |
| 81 | Fehler Fahrer- Frontairbag! |
| 82 | Fehler Fahrer- Frontairbag! |
| 83 | Beifahrer-Frontairbag gestört! |
| 84 | Beifahrer-Frontairbag gestört! |
| 85 | ACC deaktiviert! Selbst bremsen |
| 86 | ACC deaktiviert! Parkbremse |
| 87 | Rückleuchte rechts ausgefallen! |
| 88 | Abblendlicht links ausgefallen! |
| 89 | Abblendlicht rechts ausgefallen! |
| 90 | Anhänger, Rückfahr- scheinwerfer! |
| 91 | Gurt anlegen |
| 92 | Beifahrer-Rückhalte- system gestört! |
| 93 | Fahrer-Rückhalte- system gestört! |
| 94 | Rückhaltesyst. Fond links gestört! |
| 95 | Rückhaltesyst. Fond rechts gestört! |
| 96 | #kein Datensatz# |
| 97 | Sicherheitssystem! |
| 98 | Pre-Crash-Sensoren verschmutzt! |
| 99 | Pre-Crash-Sensor verschmutzt! |
| 100 | Pre-Crash-Sensor verschmutzt! |
| 101 | Pre-Crash-Sensor verschmutzt! |
| 102 | Pre-Crash-Sensor verschmutzt! |
| 103 | CC MSG |
| 104 | Getriebe wird zu heiß! Gemäßigt fahren |
| 105 | Getriebe überhitzt! Vorsichtig halten |
| 106 | Seitenairbag Fond links gestört! |
| 107 | Seitenairbag Fond rechts gestört! |
| 108 | Fahrerairbags gestört! |
| 109 | Beifahrerairbags gestört! |
| 110 | Kindersitzerkennung gestört! |
| 111 | Kennzeichenlicht links ausgefallen! |
| 112 | ACC deaktiviert! Gemäßigt fahren |
| 113 | Standlicht an! |
| 114 | Nebelschlussleuchte links! |
| 115 | Rückfahrscheinwerfer rechts! |
| 116 | Blinker hinten links ausgefallen! |
| 117 | Rückfahrscheinwerfer links ausgefallen! |
| 118 | Rückleuchte rechts ausgefallen! |
| 119 | Blinker vorn rechts ausgefallen! |
| 120 | Abblendlicht links ausgefallen! |
| 121 | Abblendlicht rechts ausgefallen! |
| 122 | Blinker vorn links ausgefallen! |
| 123 | Rückleuchte links ausgefallen! |
| 124 | Seitlicher Blinker rechts! |
| 125 | Blinker hinten rechts ausgefallen! |
| 126 | Nebelscheinwerfer rechts! |
| 127 | Seitlicher Blinker links! |
| 128 | Fernlicht links ausgefallen! |
| 129 | Nebelschlussleuchte rechts! |
| 130 | Fernlicht rechts ausgefallen! |
| 131 | Standlicht vorn links ausgefallen! |
| 132 | Standlicht vorn rechts ausgefallen! |
| 133 | Rückleuchte links ausgefallen! |
| 134 | Bremslicht rechts ausgefallen! |
| 135 | Bremslicht Mitte ausgefallen! |
| 136 | Bremslicht links ausgefallen! |
| 137 | Kennzeichenlicht rechts! |
| 138 | Nebelscheinwerfer links ausgefallen! |
| 139 | Reifenpanne vorn links! |
| 140 | Reifenpanne hinten rechts! |
| 141 | Reifenpanne hinten links! |
| 142 | Reifenfülldruck! Prüfen |
| 143 | Reifenpanne vorn rechts! |
| 144 | Reifen Druck Control gestört! |
| 145 | Reifen Druck Control ausgefallen! |
| 146 | #kein Datensatz# |
| 147 | Reifenpanne! |
| 148 | Bremslichtsteuerung ausgefallen! |
| 149 | Reifen Druck Control ausgefallen! |
| 150 | Panzertür Gepäck- raum offen! |
| 151 | Gaswarnung! Luftanlage ein |
| 152 | Ladekabel abklemmen! |
| 153 | Waffenhalterung Fehler |
| 154 | Fehler Reizgas- Sensor |
| 155 | Zwangsschaltung aktiv (Vorgehalten) |
| 156 | Luftanlage ohne Funktion |
| 157 | Luftanlage, Taste 3 s drücken |
| 158 | ACC deaktiviert! Auf Abstand achten |
| 159 | Türen nicht verriegelt |
| 160 | Fensterheber Notfkt. verwenden! |
| 161 | Kurzschluss Bord- batterieleitung! |
| 162 | Blitzleuchte, Lampe prüfen |
| 163 | Löschanlage, Taster 3 s drücken |
| 164 | Stand Waschflüssig- keit zu niedrig! |
| 165 | Außentemperatur %s |
| 166 | Kühlmittelstand zu niedrig! |
| 167 | Uhrzeit und Datum einstellen |
| 168 | Getriebe gestört! Gemäßigt fahren |
| 169 | Getriebe-Position N nur bei Motor an! |
| 170 | Getriebe- notprogramm! |
| 171 | Getriebenotprogr.! Gemäßigt fahren |
| 172 | Getriebenotprogr.! Gemäßigt fahren |
| 173 | Getriebenotprogr.! Gemäßigt fahren |
| 174 | Getriebe-Position P nur im Stillstand! |
| 175 | Getriebe-Position P gestört! |
| 176 | ACC Sensorsicht! Auf Abstand achten |
| 177 | ACC Sensorsicht! Auf Abstand achten |
| 178 | Getriebe in Position N! |
| 179 | Getriebe gestört! Gemäßigt fahren |
| 180 | Stoßdämpferregelung gestört! |
| 181 |  |
| 182 | Ölniveausensor gestört! |
| 183 | Scheibenwischer gestört! |
| 184 | DTC aktiviert! |
| 185 | Ganganzeige ausgefallen! |
| 186 | #kein Datensatz# |
| 187 | #kein Datensatz# |
| 188 | #kein Datensatz# |
| 189 | #kein Datensatz# |
| 190 | #kein Datensatz# |
| 191 | #kein Datensatz# |
| 192 | RDC wird initialisiert! |
| 193 | Notausstieg gestört! |
| 194 | Fenster offen! |
| 195 | PDC ausgefallen! |
| 196 | Blinker vorn rechts ausgefallen! |
| 197 | Blinker vorn links ausgefallen! |
| 198 | #kein Datensatz# |
| 199 | ACC ausgefallen! Auf Abstand achten |
| 200 | CAN Bus off |
| 201 | Automatic Hold deaktiviert! |
| 202 |  |
| 203 | Getriebe in Position N! |
| 204 | Dynamic Drive deaktiviert! |
| 205 | Fernbedienung! Motor nicht abstellen |
| 206 | Nächster Tastendruck startet Motor! |
| 207 | Vorsichtig anhalten |
| 208 | #kein Datensatz# |
| 209 | Fernbedienung im Innenraum! |
| 210 | Parkbremse ausgefallen! |
| 211 | Parkbremse ausgefallen! |
| 212 | Motoröldruck! Vor- sichtig anhalten |
| 213 | Generator gestört! |
| 214 | #kein Datensatz# |
| 215 |  |
| 216 | Kraftstoffpumpe! Gemäßigt fahren |
| 217 | Fernbedienung nicht vorhanden! |
| 218 | Notprogramm EVS |
| 219 | Batterieschalter auf OFF! |
| 220 | Erhöhter Ruhestrom! |
| 221 | Gaswarnung! Ort verlassen |
| 222 | Standheizung/-lüftung ausgeschaltet! |
| 223 | Elektrik gestört! Gemäßigt fahren |
| 224 | Isolationsfehler |
| 225 | Frontscheibe entriegelt! |
| 226 | Feuerlöschanlage Fehler! |
| 227 | Power Modul! Gemäßigt fahren |
| 228 | Heiz-/Klimafunktionen eingeschränkt! |
| 229 | Batterie nachladen! |
| 230 | Batterie leer! Not- aufladung aktiv |
| 231 | Lichtanlage! Vor- sichtig anhalten! |
| 232 | Schutzsysteme gestört! |
| 233 | Kommunikation gestört! |
| 234 | Überfallalarm gestört! |
| 235 | KSG |
| 236 | Brems-/Fahrstabilität! Gemäßigt fahren |
| 237 | Fahrregelsysteme! Gemäßigt fahren |
| 238 | ACC deaktiviert! Selbst bremsen |
| 239 | Parkbremse ausgefallen! |
| 240 | Parkbremse ausgefallen! |
| 241 | Parkbremse ausgefallen! |
| 242 | Parkbremse ausgefallen! |
| 243 | Parkbremse ausgefallen! |
| 244 | Zum Gangeinlegen Bremse treten |
| 245 | Niveauregulierung gestört! |
| 246 | ACC deaktiviert! Auf Abstand achten |
| 247 | Power Modul ausgefallen! |
| 248 | Gangeinlegen ohne Bremse möglich! |
| 249 | Schaltwunsch wiederholen |
| 250 | #kein Datensatz# |
| 251 | Getriebe-Position P wird eingelegt! |
| 252 |  |
| 253 |  |
| 254 | Getriebenotprogr.! Gemäßigt fahren |
| 255 | Pos. R, N, D nur bei Motor an möglich |
| 256 | Leuchtweitenregu- lierung gestört! |
| 257 | Motor wird zu heiß! Gemäßigt fahren |
| 258 |  |
| 259 | Fensterheber nicht initialisiert! |
| 260 | Schiebe-Hebedach nicht initialisiert! |
| 261 | Fensterheber gestört! |
| 262 | Schiebedach gestört! |
| 263 | Parkbremse gestört! |
| 264 |  |
| 265 | Reifenfülldruck! Erneut prüfen |
| 266 | #kein Datensatz# |
| 267 | #kein Datensatz# |
| 268 | #kein Datensatz# |
| 269 | #kein Datensatz# |
| 270 | #kein Datensatz# |
| 271 | #kein Datensatz# |
| 272 | #kein Datensatz# |
| 273 | #kein Datensatz# |
| 274 | #kein Datensatz# |
| 275 | #kein Datensatz# |
| 276 | #kein Datensatz# |
| 277 | #kein Datensatz# |
| 278 | #kein Datensatz# |
| 279 | #kein Datensatz# |
| 280 | #kein Datensatz# |
| 281 | #kein Datensatz# |
| 282 | #kein Datensatz# |
| 283 | #kein Datensatz# |
| 284 | #kein Datensatz# |
| 285 | #kein Datensatz# |
| 286 | #kein Datensatz# |
| 287 | #kein Datensatz# |
| 288 | #kein Datensatz# |
| 289 | #kein Datensatz# |
| 290 | #kein Datensatz# |
| 291 | #kein Datensatz# |
| 292 | #kein Datensatz# |
| 293 | #kein Datensatz# |
| 294 | #kein Datensatz# |
| 295 | Kurvenlicht ausgefallen! |
| 296 | Kein Notruf! Mobiltelefon? |
| 297 | Assist-Notruf nicht freigeschaltet! |
| 298 | Assist-Notruf nicht verfügbar! |
| 299 | Notruf-Systemfehler! |
| 300 | Assist-Notruf nicht verfügbar! SIM? |
| 301 | #kein Datensatz# |
| 302 | #kein Datensatz# |
| 303 | #kein Datensatz# |
| 304 | #kein Datensatz# |
| 305 | #kein Datensatz# |
| 306 | #kein Datensatz# |
| 307 | #kein Datensatz# |
| 308 | #kein Datensatz# |
| 309 | #kein Datensatz# |
| 310 | Wasserstoff tanken nicht möglich! |
| 311 | Türen und Fenster schließen! |
| 312 | H2-Betrieb nicht möglich! |
| 313 | Benzinbetrieb nicht möglich! |
| 314 | Wasserstoff-System gestört! |
| 315 | H2-System erheblich gestört! |
| 316 | H2-Tankklappe offen! |
| 317 | #kein Datensatz# |
| 318 | Ca. 3 Min. Leistungs- begrenzung! |
| 319 | Tankvorbereitungen treffen! |
| 320 | #kein Datensatz# |
| 321 | #kein Datensatz# |
| 322 | #kein Datensatz# |
| 323 | #kein Datensatz# |
| 324 | Funktion Power Modul eingeschränkt |
| 325 | #kein Datensatz# |
| 326 | Getriebe in Fahrposition |
| 327 | RDC wird initialisiert! |
| 328 | #kein Datensatz# |
| 329 | Reduzierter Batterie- ladezustand! |
| 330 | #kein Datensatz# |
| 331 | #kein Datensatz# |
| 332 | #kein Datensatz# |
| 333 | #kein Datensatz# |
| 334 | #kein Datensatz# |
| 335 | Zündung eingeschaltet |
| 336 |  |
| 337 | #kein Datensatz# |
| 338 | #kein Datensatz# |
| 339 | #kein Datensatz# |
| 340 | #kein Datensatz# |
| 341 | #kein Datensatz# |
| 342 | #kein Datensatz# |
| 343 | #kein Datensatz# |
| 344 | #kein Datensatz# |
| 345 | #kein Datensatz# |
| 346 | #kein Datensatz# |
| 347 | #kein Datensatz# |
| 348 | #kein Datensatz# |
| 349 | #kein Datensatz# |
| 350 | #kein Datensatz# |
| 351 | #kein Datensatz# |
| 352 | #kein Datensatz# |
| 353 | #kein Datensatz# |
| 354 | #kein Datensatz# |
| 355 | #kein Datensatz# |
| 356 | Nachtsicht - Kamera ausgefallen! |
| 357 | #kein Datensatz# |
| 358 | #kein Datensatz# |
| 359 | H2-Betrieb zurzeit nicht möglich! |
| 360 | H2 tanken zurzeit nicht möglich! |
| 361 | Wasserstoffsystem gestört! |
| 362 | Nicht in geschlossene Räume fahren! |
| 363 | #kein Datensatz# |
| 364 | #kein Datensatz# |
| 365 | #kein Datensatz# |
| 366 | #kein Datensatz# |
| 367 | #kein Datensatz# |
| 368 | #kein Datensatz# |
| 369 | #kein Datensatz# |
| 370 | #kein Datensatz# |
| 371 | #kein Datensatz# |
| 372 | #kein Datensatz# |
| 373 | #kein Datensatz# |
| 374 | Fernlicht-Assistent defekt! |
| 375 | Fernlicht-Assistent aktiv! |
| 376 | Fernlicht-Assistent nicht aktiv! |
| 377 | Empfindlichkeit verstellt |
